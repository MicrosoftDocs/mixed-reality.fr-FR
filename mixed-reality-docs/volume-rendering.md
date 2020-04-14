---
title: Rendu du volume
description: Les images volumétriques contiennent des informations riches avec opacité et couleur dans tout le volume qui ne peuvent pas être facilement exprimées en tant que surfaces. Découvrez comment restituer efficacement des images volumétriques dans Windows Mixed Reality.
author: kevinkennedy
ms.author: kkennedy
ms.date: 03/21/2018
ms.topic: article
keywords: image volumétrique, rendu volume, performances, réalité mixte
ms.openlocfilehash: 6dbb49c31761d4b7b9da5060d15763c3925be754
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81277947"
---
# <a name="volume-rendering"></a>Rendu du volume

Pour les volumes d’ingénierie ou d’IRM médicaux, consultez [rendu en volume sur Wikipédia](https://en.wikipedia.org/wiki/Volume_rendering). Ces « images volumétriques » contiennent des informations enrichies avec opacité et couleur dans tout le volume qui ne peuvent pas être facilement exprimées comme des surfaces telles que des [maillages polygones](https://en.wikipedia.org/wiki/Polygon_mesh).

Solutions clés pour améliorer les performances
1. MAUVAISE : approche naïve : afficher tout le volume, s’exécute généralement trop lentement
2. BONNE : plan sécant : afficher une seule tranche du volume
3. BONNE : couper le sous-volume : afficher uniquement quelques couches du volume
4. BONNE : réduire la résolution du rendu du volume (voir « Mixed Resolution Scene Rendering »)

Il n’existe qu’une certaine quantité d’informations qui peuvent être transférées de l’application à l’écran dans n’importe quel cadre particulier, ce qui correspond à la bande passante de mémoire totale. En outre, tout traitement (ou « ombrage ») requis pour transformer ces données en vue de leur présentation nécessite du temps. Les principales considérations à prendre en compte lors du rendu du volume sont les suivantes :
* Screen-largeur * Screen-hauteur * Screen-Count * volume-Layers-on-pixel = total-volume-Samples per-Frame
* 1028 * 720 * 2 * 256 = 378961920 (100%) (Full res volume : exemples trop nombreux)
* 1028 * 720 * 2 * 1 = 1480320 (0,3% de l’intégralité) (tranche fine : 1 échantillon par pixel, s’exécute sans heurts)
* 1028 * 720 * 2 * 10 = 14803200 (3,9% de l’intégralité) (sous-volume : 10 échantillons par pixel, s’exécute de manière assez fluide, semble 3D)
* 200 * 200 * 2 * 256 = 20480000 (5% de l’ensemble) (volume de ressources inférieur : moins de pixels, volume complet, semble 3D mais un peu flou)

## <a name="representing-3d-textures"></a>Représentation de textures 3D

Sur le processeur :

```
public struct Int3 { public int X, Y, Z; /* ... */ }
 public class VolumeHeader  {
   public readonly Int3 Size;
   public VolumeHeader(Int3 size) { this.Size = size;  }
   public int CubicToLinearIndex(Int3 index) {
     return index.X + (index.Y * (Size.X)) + (index.Z * (Size.X * Size.Y));
   }
   public Int3 LinearToCubicIndex(int linearIndex)
   {
     return new Int3((linearIndex / 1) % Size.X,
       (linearIndex / Size.X) % Size.Y,
       (linearIndex / (Size.X * Size.Y)) % Size.Z);
   }
   /* ... */
 }
 public class VolumeBuffer<T> {
   public readonly VolumeHeader Header;
   public readonly T[] DataArray;
   public T GetVoxel(Int3 pos)        {
     return this.DataArray[this.Header.CubicToLinearIndex(pos)];
   }
   public void SetVoxel(Int3 pos, T val)        {
     this.DataArray[this.Header.CubicToLinearIndex(pos)] = val;
   }
   public T this[Int3 pos] {
     get { return this.GetVoxel(pos); }
     set { this.SetVoxel(pos, value); }
   }
   /* ... */
 }
```

Sur le GPU :

```
float3 _VolBufferSize;
 int3 UnitVolumeToIntVolume(float3 coord) {
   return (int3)( coord * _VolBufferSize.xyz );
 }
 int IntVolumeToLinearIndex(int3 coord, int3 size) {
   return coord.x + ( coord.y * size.x ) + ( coord.z * ( size.x * size.y ) );
 }
 uniform StructuredBuffer<float> _VolBuffer;
 float SampleVol(float3 coord3 ) {
   int3 intIndex3 = UnitVolumeToIntVolume( coord3 );
   int index1D = IntVolumeToLinearIndex( intIndex3, _VolBufferSize.xyz);
   return __VolBuffer[index1D];
 }
```

## <a name="shading-and-gradients"></a>Ombrage et dégradés

Comment ombrer un volume, par exemple MRI, pour une visualisation utile. La méthode principale consiste à avoir une « fenêtre d’intensité » (un minimum et un maximum) dont vous souhaitez voir les intensités, et simplement mettre à l’échelle dans cet espace pour voir l’intensité en noir et blanc. Une « rampe de couleurs » peut ensuite être appliquée aux valeurs de cette plage et être stockée sous la forme d’une texture, de sorte que différentes parties du spectre d’intensité peuvent avoir des couleurs différentes :

```
float4 ShadeVol( float intensity ) {
   float unitIntensity = saturate( intensity - IntensityMin / ( IntensityMax - IntensityMin ) );
   // Simple two point black and white intensity:
   color.rgba = unitIntensity;
   // Color ramp method:
   color.rgba = tex2d( ColorRampTexture, float2( unitIntensity, 0 ) );
```

Dans la plupart de nos applications, nous stockons dans notre volume à la fois une valeur d’intensité brute et un « index de segmentation » (pour segmenter différentes parties, telles que la peau et le segment ; ces segments sont généralement créés par des experts dans des outils dédiés). Cela peut être combiné avec l’approche ci-dessus pour mettre une couleur différente, ou même une gamme de couleurs différente pour chaque index de segment :

```
// Change color to match segment index (fade each segment towards black):
 color.rgb = SegmentColors[ segment_index ] * color.a; // brighter alpha gives brighter color
```

## <a name="volume-slicing-in-a-shader"></a>Découpage de volume dans un nuanceur

La première étape consiste à créer un « plan de découpage » qui peut se déplacer dans le volume, le découpage et la façon dont les valeurs d’analyse sont à chaque point. Cela suppose qu’il existe un cube « VolumeSpace », qui représente l’endroit où le volume se trouve dans l’espace universel, qui peut être utilisé comme référence pour placer les points :

```
// In the vertex shader:
 float4 worldPos = mul(_Object2World, float4(input.vertex.xyz, 1));
 float4 volSpace = mul(_WorldToVolume, float4(worldPos, 1));
```

```
// In the pixel shader:
 float4 color = ShadeVol( SampleVol( volSpace ) );
```

## <a name="volume-tracing-in-shaders"></a>Suivi de volume dans les nuanceurs

Comment utiliser le GPU pour effectuer le suivi des sous-volumes (en examinant quelques voxels, puis les couches sur les données de l’arrière vers l’avant) :

```
float4 AlphaBlend(float4 dst, float4 src) {
   float4 res = (src * src.a) + (dst - dst * src.a);
   res.a = src.a + (dst.a - dst.a*src.a);
   return res;
 }
 float4 volTraceSubVolume(float3 objPosStart, float3 cameraPosVolSpace) {
   float maxDepth = 0.15; // depth in volume space, customize!!!
   float numLoops = 10; // can be 400 on nice PC
   float4 curColor = float4(0, 0, 0, 0);
   // Figure out front and back volume coords to walk through:
   float3 frontCoord = objPosStart;
   float3 backCoord = frontPos + (normalize(cameraPosVolSpace - objPosStart) * maxDepth);
   float3 stepCoord = (frontCoord - backCoord) / numLoops;
   float3 curCoord = backCoord;
   // Add per-pixel random offset, avoids layer aliasing:
   curCoord += stepCoord * RandomFromPositionFast(objPosStart);
   // Walk from back to front (to make front appear in-front of back):
   for (float i = 0; i < numLoops; i++) {
     float intensity = SampleVol(curCoord);
     float4 shaded = ShadeVol(intensity);
     curColor = AlphaBlend(curColor, shaded);
     curCoord += stepCoord;
   }
   return curColor;
 }
```

```
// In the vertex shader:
 float4 worldPos = mul(_Object2World, float4(input.vertex.xyz, 1));
 float4 volSpace = mul(_WorldToVolume, float4(worldPos.xyz, 1));
 float4 cameraInVolSpace = mul(_WorldToVolume, float4(_WorldSpaceCameraPos.xyz, 1));
```

```
// In the pixel shader:
 float4 color = volTraceSubVolume( volSpace, cameraInVolSpace );
```

## <a name="whole-volume-rendering"></a>Rendu de volume complet

En modifiant le code de sous-volume ci-dessus, nous obtenons :

```
float4 volTraceSubVolume(float3 objPosStart, float3 cameraPosVolSpace) {
   float maxDepth = 1.73; // sqrt(3), max distance from point on cube to any other point on cube
   int maxSamples = 400; // just in case, keep this value within bounds
   // not shown: trim front and back positions to both be within the cube
   int distanceInVoxels = length(UnitVolumeToIntVolume(frontPos - backPos)); // measure distance in voxels
   int numLoops = min( distanceInVoxels, maxSamples ); // put a min on the voxels to sample
```

## <a name="mixed-resolution-scene-rendering"></a>Rendu de scène à résolution mixte

Comment restituer une partie de la scène avec une résolution faible et la remettre en place :
1. Configurer deux caméras hors écran, une pour suivre chaque œil qui met à jour chaque image
2. Configurer deux cibles de rendu basse résolution (par exemple, 200x200 chacune) à laquelle les caméras s’affichent
3. Configurer un Quad qui se déplace devant l’utilisateur

Chaque frame :
1. Dessinez les cibles de rendu pour chaque œil à basse résolution (données de volume, nuanceurs onéreux, etc.).
2. Dessinez la scène normalement en tant que résolution complète (mailles, UI, etc.)
3. Dessinez une quadruple face avant l’utilisateur, sur la scène, et projetez les rendus de faible résolution sur cela
4. Résultat : combinaison visuelle d’éléments à pleine résolution avec des données de volume à faible résolution mais à haute densité
