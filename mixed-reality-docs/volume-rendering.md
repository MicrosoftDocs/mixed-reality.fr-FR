---
title: Rendu de volume
description: Images volumétriques contiennent des informations enrichies avec opacité de couleur dans le volume qui ne peut pas être facilement exprimé en tant que surfaces. Découvrez comment rendre efficacement des images volumétriques dans Windows Mixed Reality.
author: KevinKennedy
ms.author: kkennedy
ms.date: 03/21/2018
ms.topic: article
keywords: image volumétrique, de rendu de volume, de performances, de réalité mixte
ms.openlocfilehash: dc0e75b916ab7cc96be1eccb4ad32ac71f5b75ff
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596682"
---
# <a name="volume-rendering"></a>Rendu de volume

Pour médicales IRM ou d’ingénierie de volumes, consultez [Volume rendu sur Wikipedia](https://en.wikipedia.org/wiki/Volume_rendering). Ces « images volumétriques » contiennent des informations riches avec opacité de couleur dans le volume qui ne peut pas être facilement exprimé en tant que surfaces comme [mailles polygonales](https://en.wikipedia.org/wiki/Polygon_mesh).

Pour améliorer les performances des solutions clés
1. DÉFECTUEUX : Approche naïve : Afficher l’intégralité du Volume, généralement s’exécute trop lentement
2. BON : Plan de coupe : Afficher uniquement un seul secteur du volume
3. BON : Coupe de Volume secondaire : Afficher uniquement quelques couches du volume
4. BON : Réduisez la résolution de la restitution de volume (voir « Rendu de scènes résolution mixte »)

Il n'existe qu’une certaine quantité d’informations qui peuvent être transférées à partir de l’application à l’écran dans une image particulière, c’est la bande passante totale de la mémoire. Tout traitement (ou « trame ») nécessaires pour transformer les données pour la présentation également nécessite également de temps. Les considérations principales lors de rendu de volume sont par conséquent :
* Largeur d’écran * hauteur d’écran * nombre de l’écran * Volume couches-sur-que-Pixel = Total-Volume-exemples-image par image
* 1028 * 720 * 2 * 256 = 378961920 (100 %) (les volumes res complets : trop grand nombre d’exemples)
* 1028 * 720 * 2 * 1 = 1480320 (0.3 % de la pleine) (tranche dynamique : 1 exemple par pixel, s’exécute correctement)
* 1028 * 720 * 2 * 10 = 14803200 (3.9 % de la pleine) (tranche de volume secondaire : 10 échantillons par pixel, assez performante, recherche 3d)
* 200 * 200 * 2 * 256 = 20480000 (5 % de la pleine) (baisser le volume de res : moins de pixels, chiffrement de volume complet, recherche blury 3d mais un peu plus tard)

## <a name="representing-3d-textures"></a>Représentant les Textures 3D

Sur l’UC :

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

## <a name="shading-and-gradients"></a>Ombrage et des dégradés

Guide pratique pour ombrer un volume, telles qu’IRM, pour la visualisation utile. La principale méthode consiste à disposer d’une fenêtre d’intensité (min et max) que vous souhaitez voir intensité dans et simplement mettre à l’échelle dans cet espace pour afficher l’intensité noir et blanche. Une rampe de couleur peut être appliquée aux valeurs dans la plage et stockée en tant qu’une texture, afin que les différentes parties du spectre intensité peuvent être grisées différentes couleurs :

```
float4 ShadeVol( float intensity ) {
   float unitIntensity = saturate( intensity - IntensityMin / ( IntensityMax - IntensityMin ) );
   // Simple two point black and white intensity:
   color.rgba = unitIntensity;
   // Color ramp method:
   color.rgba = tex2d( ColorRampTexture, float2( unitIntensity, 0 ) );
```

Dans de nombreux nos applications nous stockons dans notre volume à la fois une valeur brute intensité et un index de segmentation (pour segmenter les différentes parties telles que l’apparence et le segment, ces segments sont généralement créés par des experts dans les outils dédiés). Cela peut être combiné avec l’approche ci-dessus pour placer une couleur différente ou une bande des couleurs différentes pour chaque index de segment :

```
// Change color to match segment index (fade each segment towards black):
 color.rgb = SegmentColors[ segment_index ] * color.a; // brighter alpha gives brighter color
```

## <a name="volume-slicing-in-a-shader"></a>Volume de découpage dans un nuanceur

Une belle première étape consiste à créer un « plan de découpage » qui peut parcourir le volume, « découpage il », et comment l’analyse des valeurs à chaque point. Cela suppose qu’il existe un cube « VolumeSpace », qui représente où le volume est dans l’espace universel, ce qui peut être utilisé comme référence pour placer les points :

```
// In the vertex shader:
 float4 worldPos = mul(_Object2World, float4(input.vertex.xyz, 1));
 float4 volSpace = mul(_WorldToVolume, float4(worldPos, 1));
```

```
// In the pixel shader:
 float4 color = ShadeVol( SampleVol( volSpace ) );
```

## <a name="volume-tracing-in-shaders"></a>Suivi du volume dans les nuanceurs

Comment utiliser le GPU pour effectuer le suivi de volume secondaire (Guide voxels quelques couches puis approfondie sur les données à partir du serveur au premier plan) :

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

## <a name="whole-volume-rendering"></a>Rendu de l’intégralité du Volume

Modification du code de sous-volume ci-dessus, nous obtenons :

```
float4 volTraceSubVolume(float3 objPosStart, float3 cameraPosVolSpace) {
   float maxDepth = 1.73; // sqrt(3), max distance from point on cube to any other point on cube
   int maxSamples = 400; // just in case, keep this value within bounds
   // not shown: trim front and back positions to both be within the cube
   int distanceInVoxels = length(UnitVolumeToIntVolume(frontPos - backPos)); // measure distance in voxels
   int numLoops = min( distanceInVoxels, maxSamples ); // put a min on the voxels to sample
```

## <a name="mixed-resolution-scene-rendering"></a>Rendu de scènes résolution mixte

Comment afficher une partie de la scène avec une faible résolution et replacer dans la place :
1. Le programme d’installation des deux caméras hors écran, une pour suivre chaque œil qui mettent à jour de chaque image
2. Le programme d’installation deux basse résolution des cibles de rendu (par exemple 200 x 200 chaque), que les caméras de rendu
3. Le programme d’installation un quadruple déplace devant l’utilisateur

Chaque image :
1. Dessiner des cibles de rendu pour chaque œil en basse résolution (données de volume, les nuanceurs coûteuses, etc.)
2. Dessiner la scène normalement en tant que pleine résolution (maille, l’interface utilisateur, etc..)
3. Dessiner un quadruple devant l’utilisateur, sur la scène et de projet les convertisseurs de basse à cette étape.
4. Résultat : la combinaison visual d’éléments de haute résolution avec des données de volume basse résolution mais à haute densité.
