---
title: Rendu du volume
description: Les images volumétriques contiennent des informations riches avec opacité et couleur dans tout le volume qui ne peuvent pas être facilement exprimées en tant que surfaces. Découvrez comment restituer efficacement des images volumétriques dans Windows Mixed Reality.
author: KevinKennedy
ms.author: kkennedy
ms.date: 03/21/2018
ms.topic: article
keywords: image volumétrique, rendu volume, performances, réalité mixte
ms.openlocfilehash: 04931df5e4225225e4c11c3f6d72801e2d58f646
ms.sourcegitcommit: 317653cd8500563c514464f0337c1f230a6f3653
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/28/2019
ms.locfileid: "75503828"
---
# <a name="volume-rendering"></a><span data-ttu-id="54827-105">Rendu du volume</span><span class="sxs-lookup"><span data-stu-id="54827-105">Volume rendering</span></span>

<span data-ttu-id="54827-106">Pour les volumes d’ingénierie ou d’IRM médicaux, consultez [rendu en volume sur Wikipédia](https://en.wikipedia.org/wiki/Volume_rendering).</span><span class="sxs-lookup"><span data-stu-id="54827-106">For medical MRI or engineering volumes, see [Volume Rendering on Wikipedia](https://en.wikipedia.org/wiki/Volume_rendering).</span></span> <span data-ttu-id="54827-107">Ces « images volumétriques » contiennent des informations riches avec de l’opacité et des couleurs dans tout le volume qui ne peuvent pas être facilement exprimées comme surfaces telles que les [maillages polygonaux](https://en.wikipedia.org/wiki/Polygon_mesh).</span><span class="sxs-lookup"><span data-stu-id="54827-107">These 'volumetric images' contain rich information with opacity and color throughout the volume that cannot be easily expressed as surfaces such as [polygonal meshes](https://en.wikipedia.org/wiki/Polygon_mesh).</span></span>

<span data-ttu-id="54827-108">Solutions clés pour améliorer les performances</span><span class="sxs-lookup"><span data-stu-id="54827-108">Key solutions to improve performance</span></span>
1. <span data-ttu-id="54827-109">MAUVAISE : approche naïve : afficher tout le volume, s’exécute généralement trop lentement</span><span class="sxs-lookup"><span data-stu-id="54827-109">BAD: Naïve Approach: Show Whole Volume, generally runs too slowly</span></span>
2. <span data-ttu-id="54827-110">BONNE : plan sécant : afficher une seule tranche du volume</span><span class="sxs-lookup"><span data-stu-id="54827-110">GOOD: Cutting Plane: Show only a single slice of the volume</span></span>
3. <span data-ttu-id="54827-111">BONNE : couper le sous-volume : afficher uniquement quelques couches du volume</span><span class="sxs-lookup"><span data-stu-id="54827-111">GOOD: Cutting Sub-Volume: Show only a few layers of the volume</span></span>
4. <span data-ttu-id="54827-112">BONNE : réduire la résolution du rendu du volume (voir « Mixed Resolution Scene Rendering »)</span><span class="sxs-lookup"><span data-stu-id="54827-112">GOOD: Lower the resolution of the volume rendering (see 'Mixed Resolution Scene Rendering')</span></span>

<span data-ttu-id="54827-113">Il n’existe qu’une certaine quantité d’informations qui peuvent être transférées de l’application à l’écran dans n’importe quel cadre particulier, ce qui correspond à la bande passante de mémoire totale.</span><span class="sxs-lookup"><span data-stu-id="54827-113">There is only a certain amount of information that can be transferred from the application to the screen in any particular frame, which is the total memory bandwidth.</span></span> <span data-ttu-id="54827-114">En outre, tout traitement (ou « ombrage ») requis pour transformer ces données en vue de leur présentation nécessite du temps.</span><span class="sxs-lookup"><span data-stu-id="54827-114">Also, any processing (or 'shading') required to transform that data for presentation requires time.</span></span> <span data-ttu-id="54827-115">Les principales considérations à prendre en compte lors du rendu du volume sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="54827-115">The primary considerations when doing volume rendering are as such:</span></span>
* <span data-ttu-id="54827-116">Screen-largeur \* Screen-hauteur \* Screen-Count \* volume-Layers-on-pixel = total-volume-Samples per-Frame</span><span class="sxs-lookup"><span data-stu-id="54827-116">Screen-Width \* Screen-Height \* Screen-Count \* Volume-Layers-On-That-Pixel = Total-Volume-Samples-Per-Frame</span></span>
* <span data-ttu-id="54827-117">1028 \* 720 \* 2 \* 256 = 378961920 (100%) (Full res volume : exemples trop nombreux)</span><span class="sxs-lookup"><span data-stu-id="54827-117">1028 \* 720 \* 2 \* 256 = 378961920 (100%) (full res volume: too many samples)</span></span>
* <span data-ttu-id="54827-118">1028 \* 720 \* 2 \* 1 = 1480320 (0,3% de l’intégralité) (tranche fine : 1 échantillon par pixel, s’exécute sans heurts)</span><span class="sxs-lookup"><span data-stu-id="54827-118">1028 \* 720 \* 2 \* 1 = 1480320 (0.3% of full) (thin slice: 1 sample per pixel, runs smoothly)</span></span>
* <span data-ttu-id="54827-119">1028 \* 720 \* 2 \* 10 = 14803200 (3,9% de l’intégralité) (sous-volume : 10 échantillons par pixel, s’exécute de manière assez fluide, semble 3D)</span><span class="sxs-lookup"><span data-stu-id="54827-119">1028 \* 720 \* 2 \* 10 = 14803200 (3.9% of full) (sub-volume slice: 10 samples per pixel, runs fairly smoothly, looks 3d)</span></span>
* <span data-ttu-id="54827-120">200 \* 200 \* 2 \* 256 = 20480000 (5% de l’ensemble) (volume de ressources inférieur : moins de pixels, volume complet, semble 3D mais un peu flou)</span><span class="sxs-lookup"><span data-stu-id="54827-120">200 \* 200 \* 2 \* 256 = 20480000 (5% of full) (lower res volume: fewer pixels, full volume, looks 3d but a bit blurry)</span></span>

## <a name="representing-3d-textures"></a><span data-ttu-id="54827-121">Représentation de textures 3D</span><span class="sxs-lookup"><span data-stu-id="54827-121">Representing 3D Textures</span></span>

<span data-ttu-id="54827-122">Sur le processeur :</span><span class="sxs-lookup"><span data-stu-id="54827-122">On the CPU:</span></span>

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

<span data-ttu-id="54827-123">Sur le GPU :</span><span class="sxs-lookup"><span data-stu-id="54827-123">On the GPU:</span></span>

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

## <a name="shading-and-gradients"></a><span data-ttu-id="54827-124">Ombrage et dégradés</span><span class="sxs-lookup"><span data-stu-id="54827-124">Shading and Gradients</span></span>

<span data-ttu-id="54827-125">Comment ombrer un volume, par exemple MRI, pour une visualisation utile.</span><span class="sxs-lookup"><span data-stu-id="54827-125">How to shade a volume, such as MRI, for useful visualization.</span></span> <span data-ttu-id="54827-126">La méthode principale consiste à avoir une « fenêtre d’intensité » (un minimum et un maximum) dont vous souhaitez voir les intensités, et simplement mettre à l’échelle dans cet espace pour voir l’intensité en noir et blanc.</span><span class="sxs-lookup"><span data-stu-id="54827-126">The primary method is to have an 'intensity window' (a min and max) that you want to see intensities within, and simply scale into that space to see the black and white intensity.</span></span> <span data-ttu-id="54827-127">Une « rampe de couleurs » peut ensuite être appliquée aux valeurs de cette plage et être stockée sous la forme d’une texture, de sorte que différentes parties du spectre d’intensité peuvent avoir des couleurs différentes :</span><span class="sxs-lookup"><span data-stu-id="54827-127">A 'color ramp' can then be applied to the values within that range, and stored as a texture, so that different parts of the intensity spectrum can be shaded different colors:</span></span>

```
float4 ShadeVol( float intensity ) {
   float unitIntensity = saturate( intensity - IntensityMin / ( IntensityMax - IntensityMin ) );
   // Simple two point black and white intensity:
   color.rgba = unitIntensity;
   // Color ramp method:
   color.rgba = tex2d( ColorRampTexture, float2( unitIntensity, 0 ) );
```

<span data-ttu-id="54827-128">Dans la plupart de nos applications, nous stockons dans notre volume à la fois une valeur d’intensité brute et un « index de segmentation » (pour segmenter différentes parties, telles que la peau et le segment ; ces segments sont généralement créés par des experts dans des outils dédiés).</span><span class="sxs-lookup"><span data-stu-id="54827-128">In many of our applications, we store in our volume both a raw intensity value and a 'segmentation index' (to segment different parts such as skin and bone; these segments are generally created by experts in dedicated tools).</span></span> <span data-ttu-id="54827-129">Cela peut être combiné avec l’approche ci-dessus pour mettre une couleur différente, ou même une gamme de couleurs différente pour chaque index de segment :</span><span class="sxs-lookup"><span data-stu-id="54827-129">This can be combined with the approach above to put a different color, or even different color ramp for each segment index:</span></span>

```
// Change color to match segment index (fade each segment towards black):
 color.rgb = SegmentColors[ segment_index ] * color.a; // brighter alpha gives brighter color
```

## <a name="volume-slicing-in-a-shader"></a><span data-ttu-id="54827-130">Découpage de volume dans un nuanceur</span><span class="sxs-lookup"><span data-stu-id="54827-130">Volume Slicing in a Shader</span></span>

<span data-ttu-id="54827-131">La première étape consiste à créer un « plan de découpage » qui peut se déplacer dans le volume, le découpage et la façon dont les valeurs d’analyse sont à chaque point.</span><span class="sxs-lookup"><span data-stu-id="54827-131">A great first step is to create a "slicing plane" that can move through the volume, 'slicing it', and how the scan values at each point.</span></span> <span data-ttu-id="54827-132">Cela suppose qu’il existe un cube « VolumeSpace », qui représente l’endroit où le volume se trouve dans l’espace universel, qui peut être utilisé comme référence pour placer les points :</span><span class="sxs-lookup"><span data-stu-id="54827-132">This assumes that there is a 'VolumeSpace' cube, which represents where the volume is in world space, that can be used as a reference for placing the points:</span></span>

```
// In the vertex shader:
 float4 worldPos = mul(_Object2World, float4(input.vertex.xyz, 1));
 float4 volSpace = mul(_WorldToVolume, float4(worldPos, 1));
```

```
// In the pixel shader:
 float4 color = ShadeVol( SampleVol( volSpace ) );
```

## <a name="volume-tracing-in-shaders"></a><span data-ttu-id="54827-133">Suivi de volume dans les nuanceurs</span><span class="sxs-lookup"><span data-stu-id="54827-133">Volume Tracing in Shaders</span></span>

<span data-ttu-id="54827-134">Comment utiliser le GPU pour effectuer le suivi des sous-volumes (en examinant quelques voxels, puis les couches sur les données de l’arrière vers l’avant) :</span><span class="sxs-lookup"><span data-stu-id="54827-134">How to use the GPU to do sub-volume tracing (walks a few voxels deep, then layers on the data from back to front):</span></span>

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

## <a name="whole-volume-rendering"></a><span data-ttu-id="54827-135">Rendu de volume complet</span><span class="sxs-lookup"><span data-stu-id="54827-135">Whole Volume Rendering</span></span>

<span data-ttu-id="54827-136">En modifiant le code de sous-volume ci-dessus, nous obtenons :</span><span class="sxs-lookup"><span data-stu-id="54827-136">Modifying the sub-volume code above, we get:</span></span>

```
float4 volTraceSubVolume(float3 objPosStart, float3 cameraPosVolSpace) {
   float maxDepth = 1.73; // sqrt(3), max distance from point on cube to any other point on cube
   int maxSamples = 400; // just in case, keep this value within bounds
   // not shown: trim front and back positions to both be within the cube
   int distanceInVoxels = length(UnitVolumeToIntVolume(frontPos - backPos)); // measure distance in voxels
   int numLoops = min( distanceInVoxels, maxSamples ); // put a min on the voxels to sample
```

## <a name="mixed-resolution-scene-rendering"></a><span data-ttu-id="54827-137">Rendu de scène à résolution mixte</span><span class="sxs-lookup"><span data-stu-id="54827-137">Mixed Resolution Scene Rendering</span></span>

<span data-ttu-id="54827-138">Comment restituer une partie de la scène avec une résolution faible et la remettre en place :</span><span class="sxs-lookup"><span data-stu-id="54827-138">How to render a part of the scene with a low resolution and put it back in place:</span></span>
1. <span data-ttu-id="54827-139">Configurer deux caméras hors écran, une pour suivre chaque œil qui met à jour chaque image</span><span class="sxs-lookup"><span data-stu-id="54827-139">Setup two off-screen cameras, one to follow each eye that update each frame</span></span>
2. <span data-ttu-id="54827-140">Configurer deux cibles de rendu basse résolution (par exemple, 200x200 chacune) à laquelle les caméras s’affichent</span><span class="sxs-lookup"><span data-stu-id="54827-140">Setup two low-resolution render targets (i.e. 200x200 each) that the cameras render into</span></span>
3. <span data-ttu-id="54827-141">Configurer un Quad qui se déplace devant l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="54827-141">Setup a quad that moves in front of the user</span></span>

<span data-ttu-id="54827-142">Chaque frame :</span><span class="sxs-lookup"><span data-stu-id="54827-142">Each Frame:</span></span>
1. <span data-ttu-id="54827-143">Dessinez les cibles de rendu pour chaque œil à basse résolution (données de volume, nuanceurs onéreux, etc.).</span><span class="sxs-lookup"><span data-stu-id="54827-143">Draw the render targets for each eye at low-resolution (volume data, expensive shaders, etc.)</span></span>
2. <span data-ttu-id="54827-144">Dessinez la scène normalement en tant que résolution complète (mailles, UI, etc.)</span><span class="sxs-lookup"><span data-stu-id="54827-144">Draw the scene normally as full resolution (meshes, UI, etc.)</span></span>
3. <span data-ttu-id="54827-145">Dessinez une quadruple face avant l’utilisateur, sur la scène, et projetez les rendus de faible résolution sur cela</span><span class="sxs-lookup"><span data-stu-id="54827-145">Draw a quad in front of the user, over the scene, and project the low-res renders onto that</span></span>
4. <span data-ttu-id="54827-146">Résultat : combinaison visuelle d’éléments à pleine résolution avec des données de volume à faible résolution mais à haute densité</span><span class="sxs-lookup"><span data-stu-id="54827-146">Result: visual combination of full-resolution elements with low-resolution but high-density volume data</span></span>
