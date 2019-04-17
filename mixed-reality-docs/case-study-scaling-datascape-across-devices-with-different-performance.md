---
title: Étude de cas - Datascape de mise à l’échelle sur les appareils avec des performances différentes
description: Cette étude de cas propose un aperçu sur comment les développeurs Microsoft optimisé l’application Datascape pour fournir une expérience attrayante sur les appareils avec un éventail de fonctionnalités de performances.
author: danandersson
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: casque immersif, étude de cas de l’optimisation, VR, performances
ms.openlocfilehash: 990a5ee6de07b6416e3150a7885220409a9c8d93
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597033"
---
# <a name="case-study---scaling-datascape-across-devices-with-different-performance"></a><span data-ttu-id="84170-104">Étude de cas - Datascape de mise à l’échelle sur les appareils avec des performances différentes</span><span class="sxs-lookup"><span data-stu-id="84170-104">Case study - Scaling Datascape across devices with different performance</span></span>

<span data-ttu-id="84170-105">Datascape est une application Windows Mixed Reality développée en interne chez Microsoft où nous nous sommes concentrés sur l’affichage des données météorologiques par-dessus les données de terrain.</span><span class="sxs-lookup"><span data-stu-id="84170-105">Datascape is a Windows Mixed Reality application developed internally at Microsoft where we focused on displaying weather data on top of terrain data.</span></span> <span data-ttu-id="84170-106">L’application explore les insights uniques utilisateurs arrivent à partir de la découverte des données dans la réalité mixte en mettant l’utilisateur avec une visualisation de données HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="84170-106">The application explores the unique insights users gain from discovering data in mixed reality by surrounding the user with holographic data visualization.</span></span>

<span data-ttu-id="84170-107">Pour Datascape que nous souhaitons cibler diverses plateformes avec des fonctionnalités matérielles différentes allant de Microsoft HoloLens à des casques IMMERSIFS réalité mixte Windows et des PC de faible puissance sur les toutes dernières PC avec processeur graphique haut de gamme.</span><span class="sxs-lookup"><span data-stu-id="84170-107">For Datascape we wanted to target a variety of platforms with different hardware capabilities ranging from Microsoft HoloLens to Windows Mixed Reality immersive headsets, and from lower-powered PCs to the very latest PCs with high-end GPU.</span></span> <span data-ttu-id="84170-108">Le défi principal a été rendu notre scène en quelques visuellement agréables sur les appareils avec des capacités graphiques entièrement différent lors de l’exécution à une fréquence d’images élevé.</span><span class="sxs-lookup"><span data-stu-id="84170-108">The main challenge was rendering our scene in a visually appealing matter on devices with wildly different graphics capabilities while executing at a high framerate.</span></span>

<span data-ttu-id="84170-109">Cette étude de cas guidera dans le processus et les techniques utilisées pour créer certaines de nos systèmes GPU gourmandes en plus, qui décrivent les problèmes que nous avons rencontré et comment nous les avons surmontées.</span><span class="sxs-lookup"><span data-stu-id="84170-109">This case study will walk through the process and techniques used to create some of our more GPU-intensive systems, describing the problems we encountered and how we overcame them.</span></span>

## <a name="transparency-and-overdraw"></a><span data-ttu-id="84170-110">La transparence et superposition</span><span class="sxs-lookup"><span data-stu-id="84170-110">Transparency and overdraw</span></span>

<span data-ttu-id="84170-111">Notre connaissait rendu principal traité la transparence, étant donné que la transparence peut s’avérer coûteuse sur un GPU.</span><span class="sxs-lookup"><span data-stu-id="84170-111">Our main rendering struggles dealt with transparency, since transparency can be expensive on a GPU.</span></span>

<span data-ttu-id="84170-112">Géométrie solide peut être rendue avant en arrière pendant l’écriture sur la mémoire tampon de profondeur, l’arrêt de toute futures pixels situés derrière ce pixel d’ignorer.</span><span class="sxs-lookup"><span data-stu-id="84170-112">Solid geometry can be rendered front to back while writing to the depth buffer, stopping any future pixels located behind that pixel from being discarded.</span></span> <span data-ttu-id="84170-113">Cela empêche les pixels masqués à partir de l’exécution du nuanceur de pixels, ce qui accélère considérablement le processus.</span><span class="sxs-lookup"><span data-stu-id="84170-113">This prevents hidden pixels from executing the pixel shader, speeding up the process significantly.</span></span> <span data-ttu-id="84170-114">Si la géométrie est triée de façon optimale, chaque pixel dans l’écran sera dessiné qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="84170-114">If geometry is sorted optimally, each pixel on the screen will be drawn only once.</span></span>

<span data-ttu-id="84170-115">Géométrie transparent doit être triée arrière vers l’avant et s’appuie sur la sortie du nuanceur de pixels pour le pixel actuel dans l’écran de fusion.</span><span class="sxs-lookup"><span data-stu-id="84170-115">Transparent geometry needs to be sorted back to front and relies on blending the output of the pixel shader to the current pixel on the screen.</span></span> <span data-ttu-id="84170-116">Cela peut entraîner dans chaque pixel dans l’écran dessinée dans plusieurs fois par frame, également appelée superposition.</span><span class="sxs-lookup"><span data-stu-id="84170-116">This can result in each pixel on the screen being drawn to multiple times per frame, referred to as overdraw.</span></span>

<span data-ttu-id="84170-117">Pour HoloLens et PC grand public, l’écran peut uniquement être renseigné un certain nombre de fois, ce qui rend transparent rendu problématique.</span><span class="sxs-lookup"><span data-stu-id="84170-117">For HoloLens and mainstream PCs, the screen can only be filled a handful of times, making transparent rendering problematic.</span></span>

## <a name="introduction-to-datascape-scene-components"></a><span data-ttu-id="84170-118">Présentation des composants de scène Datascape de</span><span class="sxs-lookup"><span data-stu-id="84170-118">Introduction to Datascape scene components</span></span>

<span data-ttu-id="84170-119">Il nous fallait trois principaux composants notre scène ; **l’interface utilisateur, le mappage**, et **la météo**.</span><span class="sxs-lookup"><span data-stu-id="84170-119">We had three major components to our scene; **the UI, the map**, and **the weather**.</span></span> <span data-ttu-id="84170-120">Nous savions dès le début que les effets de la météo nécessiterait tout le temps GPU deviendrait, donc nous avons conçu l’interface utilisateur et un terrain d’une manière qui réduirait les superpositions.</span><span class="sxs-lookup"><span data-stu-id="84170-120">We knew early on that our weather effects would require all the GPU time it could get, so we purposely designed the UI and terrain in a way that would reduce any overdraw.</span></span>

<span data-ttu-id="84170-121">Nous avons remanié l’interface utilisateur plusieurs fois afin de réduire la quantité de superposition il produirait.</span><span class="sxs-lookup"><span data-stu-id="84170-121">We reworked the UI several times to minimize the amount of overdraw it would produce.</span></span> <span data-ttu-id="84170-122">Nous nous sommes trompés sur le côté de géométrie plus complexe au lieu de superposition transparent art, superposées des composants tels que lumineux de vues d’ensemble de boutons et de la carte.</span><span class="sxs-lookup"><span data-stu-id="84170-122">We erred on the side of more complex geometry rather than overlaying transparent art on top of each other for components like glowing buttons and map overviews.</span></span>

<span data-ttu-id="84170-123">Pour le mappage, nous avons utilisé un nuanceur personnalisé qui serait éliminer des fonctionnalités de Unity standard telles que les ombres et l’éclairage complex, en les remplaçant par un modèle d’éclairage simple sun unique et un calcul personnalisé brouillard.</span><span class="sxs-lookup"><span data-stu-id="84170-123">For the map, we used a custom shader that would strip out standard Unity features such as shadows and complex lighting, replacing them with a simple single sun lighting model and a custom fog calculation.</span></span> <span data-ttu-id="84170-124">Cela produit un nuanceur de pixels simple et libérer des cycles GPU.</span><span class="sxs-lookup"><span data-stu-id="84170-124">This produced a simple pixel shader and free up GPU cycles.</span></span>

<span data-ttu-id="84170-125">Nous avons réussi à obtenir l’interface utilisateur et la carte pour le rendu au budget où nous n’avait pas besoin leurs éventuelles modifications selon le matériel ; Toutefois, la visualisation de la météo, en particulier le rendu cloud, s’est avéré pour être plus complexe !</span><span class="sxs-lookup"><span data-stu-id="84170-125">We managed to get both the UI and the map to rendering at budget where we did not need any changes to them depending on the hardware; however, the weather visualization, in particular the cloud rendering, proved to be more of a challenge!</span></span>

## <a name="background-on-cloud-data"></a><span data-ttu-id="84170-126">En arrière-plan sur des données cloud</span><span class="sxs-lookup"><span data-stu-id="84170-126">Background on cloud data</span></span>

<span data-ttu-id="84170-127">Nos données de cloud a été téléchargées à partir de serveurs de NOAA (http://nomads.ncep.noaa.gov/) et est fourni pour nous dans trois couches 2D distinctes, chacune avec la hauteur de haut et bas du cloud, ainsi que la densité du cloud pour chaque cellule de la grille.</span><span class="sxs-lookup"><span data-stu-id="84170-127">Our cloud data was downloaded from NOAA servers (http://nomads.ncep.noaa.gov/) and came to us in three distinct 2D layers, each with the top and bottom height of the cloud, as well as the density of the cloud for each cell of the grid.</span></span> <span data-ttu-id="84170-128">Les données a été traitées dans une texture d’informations cloud où chaque composant a été stocké dans le composant rouge, vert et bleu de la texture pour pouvoir accéder facilement sur le GPU.</span><span class="sxs-lookup"><span data-stu-id="84170-128">The data got processed into a cloud info texture where each component was stored in the red, green, and blue component of the texture for easy access on the GPU.</span></span>

## <a name="geometry-clouds"></a><span data-ttu-id="84170-129">Clouds de géométrie</span><span class="sxs-lookup"><span data-stu-id="84170-129">Geometry clouds</span></span>

<span data-ttu-id="84170-130">Pour vous assurer que nos ordinateurs de faible puissance pourrait rendre nos clouds que nous avons décidé de commencer par une approche par géométrie solide pour réduire la superposition.</span><span class="sxs-lookup"><span data-stu-id="84170-130">To make sure our lower-powered machines could render our clouds we decided to start with an approach that would use solid geometry to minimize overdraw.</span></span>

<span data-ttu-id="84170-131">Tout d’abord, nous avons essayé production clouds en générant une maille pleine relief pour chaque couche à l’aide de rayon de la texture d’informations cloud par vertex pour générer la forme.</span><span class="sxs-lookup"><span data-stu-id="84170-131">We first tried producing clouds by generating a solid heightmap mesh for each layer using the radius of the cloud info texture per vertex to generate the shape.</span></span> <span data-ttu-id="84170-132">Nous avons utilisé un nuanceur de géométrie pour produire les sommets à la fois en haut et bas du cloud générant des formes de cloud solide.</span><span class="sxs-lookup"><span data-stu-id="84170-132">We used a geometry shader to produce the vertices both at the top and the bottom of the cloud generating solid cloud shapes.</span></span> <span data-ttu-id="84170-133">Nous avons utilisé la valeur de densité de la texture pour colorer le cloud avec une couleur sombre pour les clouds plus denses.</span><span class="sxs-lookup"><span data-stu-id="84170-133">We used the density value from the texture to color the cloud with darker colors for more dense clouds.</span></span>

<span data-ttu-id="84170-134">**Nuanceur pour la création de vertex :**</span><span class="sxs-lookup"><span data-stu-id="84170-134">**Shader for creating the vertices:**</span></span>

```
v2g vert (appdata v)
{
    v2g o;
    o.height = tex2Dlod(_MainTex, float4(v.uv, 0, 0)).x;
    o.vertex = v.vertex;
    return o;
}
 
g2f GetOutput(v2g input, float heightDirection)
{
    g2f ret;
    float4 newBaseVert = input.vertex;
    newBaseVert.y += input.height * heightDirection * _HeigthScale;
    ret.vertex = UnityObjectToClipPos(newBaseVert);
    ret.height = input.height;
    return ret;
}
 
[maxvertexcount(6)]
void geo(triangle v2g p[3], inout TriangleStream<g2f> triStream)
{
    float heightTotal = p[0].height + p[1].height + p[2].height;
    if (heightTotal > 0)
    {
        triStream.Append(GetOutput(p[0], 1));
        triStream.Append(GetOutput(p[1], 1));
        triStream.Append(GetOutput(p[2], 1));
 
        triStream.RestartStrip();
 
        triStream.Append(GetOutput(p[2], -1));
        triStream.Append(GetOutput(p[1], -1));
        triStream.Append(GetOutput(p[0], -1));
    }
}
fixed4 frag (g2f i) : SV_Target
{
    clip(i.height - 0.1f);
 
    float3 finalColor = lerp(_LowColor, _HighColor, i.height);
    return float4(finalColor, 1);
}
```

<span data-ttu-id="84170-135">Nous avons introduit un modèle petit bruit pour obtenir plus de détails sur les données réelles.</span><span class="sxs-lookup"><span data-stu-id="84170-135">We introduced a small noise pattern to get more detail on top of the real data.</span></span> <span data-ttu-id="84170-136">Pour produire les bords arrondis cloud, nous découpé les pixels dans le nuanceur de pixels lorsque la valeur de rayon interpolée atteint un seuil afin d’ignorer les valeurs proches de zéro.</span><span class="sxs-lookup"><span data-stu-id="84170-136">To produce round cloud edges, we clipped the pixels in the pixel shader when the interpolated radius value hit a threshold to discard near-zero values.</span></span>

![Clouds de géométrie](images/datascape-geometry-clouds-700px.jpg)

<span data-ttu-id="84170-138">Étant donné que les clouds sont géométrie solide, ils peuvent être rendus avant le terrain pour masquer n’importe quel pixels carte coûteux en dessous pour améliorer encore les taux de trames.</span><span class="sxs-lookup"><span data-stu-id="84170-138">Since the clouds are solid geometry, they can be rendered before the terrain to hide any expensive map pixels underneath to further improve framerate.</span></span> <span data-ttu-id="84170-139">Cette solution s’est exécutée correctement sur toutes les cartes graphiques à partir de la spécification de min cartes graphiques haut de gamme, ainsi que sur HoloLens, en raison de l’approche de rendu de géométrie solide.</span><span class="sxs-lookup"><span data-stu-id="84170-139">This solution ran well on all graphics cards from min-spec to high-end graphics cards, as well as on HoloLens, because of the solid geometry rendering approach.</span></span>

## <a name="solid-particle-clouds"></a><span data-ttu-id="84170-140">Clouds de particules solides</span><span class="sxs-lookup"><span data-stu-id="84170-140">Solid particle clouds</span></span>

<span data-ttu-id="84170-141">Maintenant, nous avions une solution de sauvegarde qui produit une bonne représentation de nos données cloud, mais a été un peu reluisantes dans le facteur de « wow » et s’est pas transmettre le volumétriques sont convaincus que nous voulions pour nos ordinateurs haut de gamme.</span><span class="sxs-lookup"><span data-stu-id="84170-141">We now had a backup solution that produced a decent representation of our cloud data, but was a bit lackluster in the “wow” factor and did not convey the volumetric feel that we wanted for our high-end machines.</span></span>

<span data-ttu-id="84170-142">Notre prochaine étape créait des nuages en représentant les avec environ 100 000 particules pour produire une apparence plus naturelle et volumétrique.</span><span class="sxs-lookup"><span data-stu-id="84170-142">Our next step was creating the clouds by representing them with approximately 100,000 particles to produce a more organic and volumetric look.</span></span>

<span data-ttu-id="84170-143">Si particules pleine et trier l’avant vers l’arrière, nous pouvons bénéficier élimination de mémoire tampon de profondeur des pixels derrière les particules précédemment rendus, ce qui réduit les superpositions.</span><span class="sxs-lookup"><span data-stu-id="84170-143">If particles stay solid and sort front-to-back, we can still benefit from depth buffer culling of the pixels behind previously rendered particles, reducing the overdraw.</span></span> <span data-ttu-id="84170-144">En outre, avec une solution basée sur les particules, nous pouvons modifier la quantité de particules utilisé sur un autre matériel de cible.</span><span class="sxs-lookup"><span data-stu-id="84170-144">Also, with a particle-based solution, we can alter the amount of particles used to target different hardware.</span></span> <span data-ttu-id="84170-145">Toutefois, tous les pixels devront être testé de profondeur, ce qui aboutit à une surcharge supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="84170-145">However, all pixels still need to be depth tested, which results in some additional overhead.</span></span>

<span data-ttu-id="84170-146">Tout d’abord, nous avons créé des positions de particules autour du point central de l’expérience au démarrage.</span><span class="sxs-lookup"><span data-stu-id="84170-146">First, we created particle positions around the center point of the experience at startup.</span></span> <span data-ttu-id="84170-147">Nous avons distribué les particules de façon plus compacte autour du centre et moins c’est le cas dans la distance.</span><span class="sxs-lookup"><span data-stu-id="84170-147">We distributed the particles more densely around the center and less so in the distance.</span></span> <span data-ttu-id="84170-148">Nous prétriées toutes les particules à partir du centre vers l’arrière afin que tout d’abord affichant les particules le plus proche.</span><span class="sxs-lookup"><span data-stu-id="84170-148">We pre-sorted all particles from the center to the back so that the closest particles would render first.</span></span>

<span data-ttu-id="84170-149">Un nuanceur de calcul serait exemples de la texture d’informations cloud afin de positionner chaque particule à une hauteur et une couleur que selon la densité.</span><span class="sxs-lookup"><span data-stu-id="84170-149">A compute shader would sample the cloud info texture to position each particle at a correct height and color it based on the density.</span></span>

<span data-ttu-id="84170-150">Nous avons utilisé *DrawProcedural* permettant de restituer une quadruple par particule autorisant les données de la particule de rester sur le GPU à tout moment.</span><span class="sxs-lookup"><span data-stu-id="84170-150">We used *DrawProcedural* to render a quad per particle allowing the particle data to stay on the GPU at all times.</span></span>

<span data-ttu-id="84170-151">Chaque particule contenait une hauteur et un rayon.</span><span class="sxs-lookup"><span data-stu-id="84170-151">Each particle contained both a height and a radius.</span></span> <span data-ttu-id="84170-152">La hauteur était basée sur les données de cloud échantillonnées à partir de la texture info de cloud, et le rayon était basé sur la distribution initiale où elle est calculée pour stocker la distance horizontale et son voisin le plus proche.</span><span class="sxs-lookup"><span data-stu-id="84170-152">The height was based on the cloud data sampled from the cloud info texture, and the radius was based on the initial distribution where it would be calculated to store the horizontal distance to its closest neighbor.</span></span> <span data-ttu-id="84170-153">Les quadrilatères voudraient utiliser ces données pour orienter lui-même inclinées par la hauteur afin que lorsque les utilisateurs regardez horizontalement, la hauteur sont affichée, et lorsque les utilisateurs examiné il haut en bas, la zone entre ses voisins est couverts.</span><span class="sxs-lookup"><span data-stu-id="84170-153">The quads would use this data to orient itself angled by the height so that when users look at it horizontally, the height would be shown, and when users looked at it top-down, the area between its neighbors would be covered.</span></span>

![Forme de particules](images/particle-shape-700px.png)

<span data-ttu-id="84170-155">**Code de nuanceur montrant la distribution :**</span><span class="sxs-lookup"><span data-stu-id="84170-155">**Shader code showing the distribution:**</span></span>

```
ComputeBuffer cloudPointBuffer = new ComputeBuffer(6, quadPointsStride);
cloudPointBuffer.SetData(new[]
{
    new Vector2(-.5f, .5f),
    new Vector2(.5f, .5f),
    new Vector2(.5f, -.5f),
    new Vector2(.5f, -.5f),
    new Vector2(-.5f, -.5f),
    new Vector2(-.5f, .5f)
});
 
StructuredBuffer<float2> quadPoints;
StructuredBuffer<float3> particlePositions;
v2f vert(uint id : SV_VertexID, uint inst : SV_InstanceID)
{
    // Find the center of the quad, from local to world space
    float4 centerPoint = mul(unity_ObjectToWorld, float4(particlePositions[inst], 1));
 
    // Calculate y offset for each quad point
    float3 cameraForward = normalize(centerPoint - _WorldSpaceCameraPos);
    float y = dot(quadPoints[id].xy, cameraForward.xz);
 
    // Read out the particle data
    float radius = ...;
    float height = ...;
 
    // Set the position of the vert
    float4 finalPos = centerPoint + float4(quadPoints[id].x, y * height, quadPoints[id].y, 0) * radius;
    o.pos = mul(UNITY_MATRIX_VP, float4(finalPos.xyz, 1));
    o.uv = quadPoints[id].xy + 0.5;
 
    return o;
}
```

<span data-ttu-id="84170-156">Dans la mesure où nous trier le particules avant vers l’arrière et nous avons toujours utilisé un nuanceur de style continu sur les pixels transparents clip (pas blend), cette technique permet de gérer une quantité étonnante de particules, évitant les coûteux dessin excessive même sur les machines de faible puissance.</span><span class="sxs-lookup"><span data-stu-id="84170-156">Since we sort the particles front-to-back and we still used a solid style shader to clip (not blend) transparent pixels, this technique handles a surprising amount of particles, avoiding costly over-draw even on the lower-powered machines.</span></span>

## <a name="transparent-particle-clouds"></a><span data-ttu-id="84170-157">Clouds de particules transparent</span><span class="sxs-lookup"><span data-stu-id="84170-157">Transparent particle clouds</span></span>

<span data-ttu-id="84170-158">Les particules solides fourni une idée organique à la forme des clouds, mais encore besoin de quelque chose de vendre le fluffiness des clouds.</span><span class="sxs-lookup"><span data-stu-id="84170-158">The solid particles provided a good organic feel to the shape of the clouds but still needed something to sell the fluffiness of clouds.</span></span> <span data-ttu-id="84170-159">Nous avons décidé d’essayer une solution personnalisée pour les cartes graphiques haut de gamme où nous pouvons introduire la transparence.</span><span class="sxs-lookup"><span data-stu-id="84170-159">We decided to try a custom solution for the high-end graphics cards where we can introduce transparency.</span></span>

<span data-ttu-id="84170-160">Pour cela nous simplement modifiais l’ordre de tri initial des particules et modifié le nuanceur pour utiliser la valeur alpha de textures.</span><span class="sxs-lookup"><span data-stu-id="84170-160">To do this we simply switched the initial sorting order of the particles and changed the shader to use the textures alpha.</span></span>

![Fluffy clouds](images/fluffy-clouds-700px.jpg)

<span data-ttu-id="84170-162">Il ressemblait excellent, mais s’est avéré pour être trop lourde pour même les ordinateurs les plus ardues, car elle entraînerait le rendu de chaque pixel dans l’écran des centaines de fois !</span><span class="sxs-lookup"><span data-stu-id="84170-162">It looked great but proved to be too heavy for even the toughest machines since it would result in rendering each pixel on the screen hundreds of times!</span></span>

## <a name="render-off-screen-with-lower-resolution"></a><span data-ttu-id="84170-163">Rendu hors écran avec une résolution inférieure</span><span class="sxs-lookup"><span data-stu-id="84170-163">Render off-screen with lower resolution</span></span>

<span data-ttu-id="84170-164">Pour réduire le nombre de pixels affichés par les clouds, nous avons commencé à leur rendu dans la mémoire tampon de résolution d’un trimestre (comparé à l’écran) et étirer le résultat final des sauvegardes sur l’écran après que toutes les particules avaient été dessinés.</span><span class="sxs-lookup"><span data-stu-id="84170-164">To reduce the number of pixels rendered by the clouds, we started rendering them in a quarter resolution buffer (compared to the screen) and stretching the end result back up onto the screen after all the particles had been drawn.</span></span> <span data-ttu-id="84170-165">Cela nous a donné à peu près une accélération 4 x, mais fourni avec quelques inconvénients.</span><span class="sxs-lookup"><span data-stu-id="84170-165">This gave us roughly a 4x speedup, but came with a couple of caveats.</span></span>

<span data-ttu-id="84170-166">**Code pour le rendu hors écran :**</span><span class="sxs-lookup"><span data-stu-id="84170-166">**Code for rendering off-screen:**</span></span>

```
cloudBlendingCommand = new CommandBuffer();
Camera.main.AddCommandBuffer(whenToComposite, cloudBlendingCommand);
 
cloudCamera.CopyFrom(Camera.main);
cloudCamera.rect = new Rect(0, 0, 1, 1);    //Adaptive rendering can set the main camera to a smaller rect
cloudCamera.clearFlags = CameraClearFlags.Color;
cloudCamera.backgroundColor = new Color(0, 0, 0, 1);
 
currentCloudTexture = RenderTexture.GetTemporary(Camera.main.pixelWidth / 2, Camera.main.pixelHeight / 2, 0);
cloudCamera.targetTexture = currentCloudTexture;
 
// Render clouds to the offscreen buffer
cloudCamera.Render();
cloudCamera.targetTexture = null;
 
// Blend low-res clouds to the main target
cloudBlendingCommand.Blit(currentCloudTexture, new RenderTargetIdentifier(BuiltinRenderTextureType.CurrentActive), blitMaterial);
```

<span data-ttu-id="84170-167">Tout d’abord, lors du rendu dans une mémoire tampon hors écran, nous avons perdu toutes les informations de profondeur à partir de notre scène principale, ce qui entraîne des particules derrière montagnes rendu par-dessus le mountain.</span><span class="sxs-lookup"><span data-stu-id="84170-167">First, when rendering into an off-screen buffer, we lost all depth information from our main scene, resulting in particles behind mountains rendering on top of the mountain.</span></span>

<span data-ttu-id="84170-168">En second lieu, étirement de la mémoire tampon a également introduit les artefacts sur les bords de notre clouds où la modification de la résolution a été notable.</span><span class="sxs-lookup"><span data-stu-id="84170-168">Second, stretching the buffer also introduced artifacts on the edges of our clouds where the resolution change was noticeable.</span></span> <span data-ttu-id="84170-169">Les deux sections suivantes parler de la façon dont nous avons résolu ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="84170-169">The next two sections talk about how we resolved these issues.</span></span>

## <a name="particle-depth-buffer"></a><span data-ttu-id="84170-170">Mémoire tampon de profondeur de particules</span><span class="sxs-lookup"><span data-stu-id="84170-170">Particle depth buffer</span></span>

<span data-ttu-id="84170-171">Pour rendre les particules coexiste avec la géométrie de l’environnement où un mountain ou un objet peut couvrir des particules derrière lui, nous l’avons rempli la mémoire tampon hors écran avec une mémoire tampon de profondeur contenant la géométrie de la scène principale.</span><span class="sxs-lookup"><span data-stu-id="84170-171">To make the particles co-exist with the world geometry where a mountain or object could cover particles behind it, we populated the off-screen buffer with a depth buffer containing the geometry of the main scene.</span></span> <span data-ttu-id="84170-172">Pour produire cette mémoire tampon de profondeur, nous avons créé une deuxième caméra, rendu uniquement la géométrie solide et la profondeur de la scène.</span><span class="sxs-lookup"><span data-stu-id="84170-172">To produce such depth buffer, we created a second camera, rendering only the solid geometry and depth of the scene.</span></span>

<span data-ttu-id="84170-173">Ensuite, nous avons utilisé la nouvelle texture dans le nuanceur de pixels des clouds pour occlude pixels.</span><span class="sxs-lookup"><span data-stu-id="84170-173">We then used the new texture in the pixel shader of the clouds to occlude pixels.</span></span> <span data-ttu-id="84170-174">Nous avons utilisé la même texture pour calculer la distance à la géométrie derrière un pixel de cloud.</span><span class="sxs-lookup"><span data-stu-id="84170-174">We used the same texture to calculate the distance to the geometry behind a cloud pixel.</span></span> <span data-ttu-id="84170-175">En utilisant cette distance et appliquer à la valeur alpha du pixel, nous avions maintenant l’effet des clouds fondu lorsqu’ils ont proche de terrain, en supprimant les morceaux dur intersection des particules et le terrain.</span><span class="sxs-lookup"><span data-stu-id="84170-175">By using that distance and applying it to the alpha of the pixel, we now had the effect of clouds fading out as they get close to terrain, removing any hard cuts where particles and terrain meet.</span></span>

![Clouds fusionnés dans un terrain](images/clouds-blended-to-terrain-700px.jpg)

## <a name="sharpening-the-edges"></a><span data-ttu-id="84170-177">La netteté</span><span class="sxs-lookup"><span data-stu-id="84170-177">Sharpening the edges</span></span>

<span data-ttu-id="84170-178">Les clouds des étiré ressemblait presque identiques pour les clouds de taille normale au centre des particules ou où ils chevauchent, mais vous a montré certains artefacts sur les bords du cloud.</span><span class="sxs-lookup"><span data-stu-id="84170-178">The stretched-up clouds looked almost identical to the normal size clouds at the center of the particles or where they overlapped, but showed some artifacts at the cloud edges.</span></span> <span data-ttu-id="84170-179">Sinon des bords tranchants apparaîtrait floues et effets d’alias ont été introduites lors de l’appareil photo est déplacé.</span><span class="sxs-lookup"><span data-stu-id="84170-179">Otherwise sharp edges would appear blurry and alias effects were introduced when the camera moved.</span></span>

<span data-ttu-id="84170-180">Nous avons résolu le problème en exécutant un nuanceur simple sur la mémoire tampon hors écran pour localiser les grands changements à l’inverse (1).</span><span class="sxs-lookup"><span data-stu-id="84170-180">We solved this by running a simple shader on the off-screen buffer to determine where big changes in contrast occurred (1).</span></span> <span data-ttu-id="84170-181">Nous mettons les pixels avec de grands changements dans un nouveau tampon stencil (2).</span><span class="sxs-lookup"><span data-stu-id="84170-181">We put the pixels with big changes into a new stencil buffer (2).</span></span> <span data-ttu-id="84170-182">Nous avons ensuite utilisé la mémoire tampon stencil pour masquer les ces zones de contraste élevé lors de l’application de la mémoire tampon hors écran à l’écran, ce qui entraîne des failles dans et autour de nuages (3).</span><span class="sxs-lookup"><span data-stu-id="84170-182">We then used the stencil buffer to mask out these high contrast areas when applying the off-screen buffer back to the screen, resulting in holes in and around the clouds (3).</span></span>

<span data-ttu-id="84170-183">Nous avons ensuite toutes les particules une nouvelle fois restitué en mode plein écran, mais cette fois utilisé la mémoire tampon stencil pour masquer tous les éléments, mais les bords, ce qui entraîne un ensemble minimal de pixels utilisé (4).</span><span class="sxs-lookup"><span data-stu-id="84170-183">We then rendered all the particles again in full-screen mode, but this time used the stencil buffer to mask out everything but the edges, resulting in a minimal set of pixels touched (4).</span></span> <span data-ttu-id="84170-184">Dans la mesure où le tampon de commande a déjà été créé pour les particules, nous avions simplement pour la rendre à nouveau vers le nouvel appareil photo.</span><span class="sxs-lookup"><span data-stu-id="84170-184">Since the command buffer was already created for the particles, we simply had to render it again to the new camera.</span></span>

![Progression du rendu des bords du cloud](images/cloud-steps-1-4-700px.jpg)

<span data-ttu-id="84170-186">Le résultat final a été bords tranchants avec des sections center peu onéreuse des clouds.</span><span class="sxs-lookup"><span data-stu-id="84170-186">The end result was sharp edges with cheap center sections of the clouds.</span></span>

<span data-ttu-id="84170-187">Cette opération est beaucoup plus rapide que le rendu toutes les particules en plein écran, il est toujours un coût associé à un pixel par rapport à la mémoire tampon stencil, de test pour des quantités massives de superposition toujours fournie avec un coût.</span><span class="sxs-lookup"><span data-stu-id="84170-187">While this was much faster than rendering all particles in full screen, there is still a cost associated with testing a pixel against the stencil buffer, so a massive amount of overdraw still came with a cost.</span></span>

## <a name="culling-particles"></a><span data-ttu-id="84170-188">Élimination de particules</span><span class="sxs-lookup"><span data-stu-id="84170-188">Culling particles</span></span>

<span data-ttu-id="84170-189">Pour notre effet du vent, que nous avons générée durée pendant laquelle les bandes de triangles dans un nuanceur de calcul, création de nombreux offraient de vent dans le monde.</span><span class="sxs-lookup"><span data-stu-id="84170-189">For our wind effect, we generated long triangle strips in a compute shader, creating many wisps of wind in the world.</span></span> <span data-ttu-id="84170-190">L’effet du vent n’était pas une charge importante pour les taux de remplissage en raison de bandes réduits généré, il produit plusieurs centaines de milliers de vertex, ce qui entraîne une charge importante pour le nuanceur de sommets.</span><span class="sxs-lookup"><span data-stu-id="84170-190">While the wind effect was not heavy on fill rate due to skinny strips generated, it produced many hundreds of thousands of vertices resulting in a heavy load for the vertex shader.</span></span>

<span data-ttu-id="84170-191">Nous avons introduit ajouter les mémoires tampons sur le nuanceur de calcul pour alimenter un sous-ensemble de la diagonale du vent à dessiner.</span><span class="sxs-lookup"><span data-stu-id="84170-191">We introduced append buffers on the compute shader to feed a subset of the wind strips to be drawn.</span></span> <span data-ttu-id="84170-192">Avec une vue simple frustum élimination logique du nuanceur de calcul, nous aurions pu déterminer si une bande était en dehors de la vue de la caméra et empêcher l’ajout à la mémoire tampon push.</span><span class="sxs-lookup"><span data-stu-id="84170-192">With some simple view frustum culling logic in the compute shader, we could determine if a strip was outside of camera view and prevent it from being added to the push buffer.</span></span> <span data-ttu-id="84170-193">Cela réduit la quantité de bandes considérablement, libérant des cycles nécessaires sur le GPU.</span><span class="sxs-lookup"><span data-stu-id="84170-193">This reduced the amount of strips significantly, freeing up some needed cycles on the GPU.</span></span>

<span data-ttu-id="84170-194">**Code illustrant une mémoire tampon d’ajouter :**</span><span class="sxs-lookup"><span data-stu-id="84170-194">**Code demonstrating an append buffer:**</span></span>

<span data-ttu-id="84170-195">*Nuanceur de calcul :*</span><span class="sxs-lookup"><span data-stu-id="84170-195">*Compute shader:*</span></span>

```
AppendStructuredBuffer<int> culledParticleIdx;
 
if (show)
    culledParticleIdx.Append(id.x);
```

<span data-ttu-id="84170-196">*C#code :*</span><span class="sxs-lookup"><span data-stu-id="84170-196">*C# code:*</span></span>

```
protected void Awake() 
{
    // Create an append buffer, setting the maximum size and the contents stride length
    culledParticlesIdxBuffer = new ComputeBuffer(ParticleCount, sizeof(int), ComputeBufferType.Append);
 
    // Set up Args Buffer for Draw Procedural Indirect
    argsBuffer = new ComputeBuffer(4, sizeof(int), ComputeBufferType.IndirectArguments);
    argsBuffer.SetData(new int[] { DataVertCount, 0, 0, 0 });
}
 
protected void Update()
{
    // Reset the append buffer, and dispatch the compute shader normally
    culledParticlesIdxBuffer.SetCounterValue(0);
 
    computer.Dispatch(...)
 
    // Copy the append buffer count into the args buffer used by the Draw Procedural Indirect call
    ComputeBuffer.CopyCount(culledParticlesIdxBuffer, argsBuffer, dstOffset: 1);
    ribbonRenderCommand.DrawProceduralIndirect(Matrix4x4.identity, renderMaterial, 0, MeshTopology.Triangles, dataBuffer);
}
```

<span data-ttu-id="84170-197">Nous avons essayé d’à l’aide de la même technique sur les particules de cloud, où nous sélectionnons les sur le nuanceur de calcul et transmettre uniquement les particules visibles doit être restitué.</span><span class="sxs-lookup"><span data-stu-id="84170-197">We tried using the same technique on the cloud particles, where we would cull them on the compute shader and only push the visible particles to be rendered.</span></span> <span data-ttu-id="84170-198">Cette technique réellement n’avez pas enregistré nous une grande partie sur le GPU dans la mesure où le plus gros goulet d’étranglement a été les pixels de montant affichées sur l’écran et pas le coût de calcul de vertex.</span><span class="sxs-lookup"><span data-stu-id="84170-198">This technique actually did not save us much on the GPU since the biggest bottleneck was the amount pixels rendered on the screen, and not the cost of calculating the vertices.</span></span>

<span data-ttu-id="84170-199">L’autre problème avec cette technique était que la mémoire tampon append rempli dans un ordre aléatoire en raison de sa nature parallélisée de l’informatique les particules, à l’origine les particules triés soit non triée, ce qui entraîne des particules cloud scintillements sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="84170-199">The other problem with this technique was that the append buffer populated in random order due to its parallelized nature of computing the particles, causing the sorted particles to be un-sorted, resulting in flickering cloud particles.</span></span>

<span data-ttu-id="84170-200">Il existe des techniques pour trier la mémoire tampon push, mais la quantité limitée de gain de performances que provenant de l’élimination de particules serait probablement être décalée avec un tri supplémentaire, nous avons donc décidé de ne pas poursuivre cette optimisation.</span><span class="sxs-lookup"><span data-stu-id="84170-200">There are techniques to sort the push buffer, but the limited amount of performance gain we got out of culling particles would likely be offset with an additional sort, so we decided to not pursue this optimization.</span></span>

## <a name="adaptive-rendering"></a><span data-ttu-id="84170-201">Rendu adaptatif</span><span class="sxs-lookup"><span data-stu-id="84170-201">Adaptive rendering</span></span>

<span data-ttu-id="84170-202">Pour garantir une fréquence d’images stable sur une application avec diverses conditions comme un temps nuageux vs de rendu un aperçu clair, nous avons introduit rendu adaptatif à notre application.</span><span class="sxs-lookup"><span data-stu-id="84170-202">To ensure a steady framerate on an app with varying rendering conditions like a cloudy vs a clear view, we introduced adaptive rendering to our app.</span></span>

<span data-ttu-id="84170-203">La première étape de rendu adaptatif consiste à mesurer le GPU.</span><span class="sxs-lookup"><span data-stu-id="84170-203">The first step of adaptive rendering is to measure GPU.</span></span> <span data-ttu-id="84170-204">Nous l’avons fait cela en insérant un code personnalisé dans le tampon de commande GPU au début et à la fin d’une image rendue, capture les deux, gauche et à droite du temps d’écran des yeux.</span><span class="sxs-lookup"><span data-stu-id="84170-204">We did this by inserting custom code into the GPU command buffer at the beginning and the end of a rendered frame, capturing both the left and right eye screen time.</span></span>

<span data-ttu-id="84170-205">En mesurant le temps passé de rendu et en la comparant à notre souhaité-fréquence d’actualisation que nous avons une idée de comment fermer nous à la perte de trames.</span><span class="sxs-lookup"><span data-stu-id="84170-205">By measuring the time spent rendering and comparing it to our desired refresh-rate we got a sense of how close we were to dropping frames.</span></span>

<span data-ttu-id="84170-206">Lorsque proche de la suppression d’images, nous adapter notre rendu pour le rendre plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="84170-206">When close to dropping frames, we adapt our rendering to make it faster.</span></span> <span data-ttu-id="84170-207">Un moyen simple d’adaptation change la taille de fenêtre d’affichage de l’écran, nécessitant moins pixels pour obtenir le rendu.</span><span class="sxs-lookup"><span data-stu-id="84170-207">One simple way of adapting is changing the viewport size of the screen, requiring less pixels to get rendered.</span></span>

<span data-ttu-id="84170-208">À l’aide de *UnityEngine.XR.XRSettings.renderViewportScale* le système réduit la fenêtre d’affichage ciblé et étire automatiquement le résultat au ajuster l’écran.</span><span class="sxs-lookup"><span data-stu-id="84170-208">By using *UnityEngine.XR.XRSettings.renderViewportScale* the system shrinks the targeted viewport and automatically stretches the result back up to fit the screen.</span></span> <span data-ttu-id="84170-209">Une petite modification de la mise à l’échelle est à peine perceptible sur la géométrie de l’environnement, et un facteur d’échelle de 0,7 nécessite la moitié de la quantité de pixels doit être restitué.</span><span class="sxs-lookup"><span data-stu-id="84170-209">A small change in scale is barely noticeable on world geometry, and a scale factor of 0.7 requires half the amount of pixels to be rendered.</span></span>

![échelle de 70 %, la moitié du nombre de pixels](images/datascape-scaling-700px.jpg)

<span data-ttu-id="84170-211">Lorsque nous détectons que nous sommes sur le point de supprimer des trames nous réduire l’échelle par un nombre fixe et augmenter refaites-le lorsque nous exécutons assez rapidement à nouveau.</span><span class="sxs-lookup"><span data-stu-id="84170-211">When we detect that we are about to drop frames we lower the scale by a fixed number, and increase it back when we are running fast enough again.</span></span>

<span data-ttu-id="84170-212">Bien que nous avons décidé quelle technique cloud à utiliser selon graphics capacités du matériel au démarrage, il est possible en vous basant sur les données à partir de la mesure du GPU pour empêcher le système de rester au premier plan basse résolution pour un certain temps, mais il s’agit d’un élément sans avoir à temps  pour Explorer les Datascape.</span><span class="sxs-lookup"><span data-stu-id="84170-212">While we decided what cloud technique to use based on graphics capabilities of the hardware at startup, it is possible to base it on data from the GPU measurement to prevent the system from staying at low resolution for a long time, but this is something we did not have time to explore in Datascape.</span></span>

## <a name="final-thoughts"></a><span data-ttu-id="84170-213">Réflexions finales</span><span class="sxs-lookup"><span data-stu-id="84170-213">Final thoughts</span></span>

<span data-ttu-id="84170-214">Ciblage d’une variété de matériel est complexe et requiert une planification.</span><span class="sxs-lookup"><span data-stu-id="84170-214">Targeting a variety of hardware is challenging and requires some planning.</span></span>

<span data-ttu-id="84170-215">Nous vous recommandons de commencer ciblant les ordinateurs de faible puissance pour vous familiariser avec l’espace de problème et de développer une solution de sauvegarde qui s’exécutera sur toutes vos machines.</span><span class="sxs-lookup"><span data-stu-id="84170-215">We recommend that you start targeting lower-powered machines to get familiar with the problem space and develop a backup solution that will run on all your machines.</span></span> <span data-ttu-id="84170-216">Concevoir votre solution avec des taux de remplissage à l’esprit, dans la mesure où les pixels sera votre ressource plus précieux.</span><span class="sxs-lookup"><span data-stu-id="84170-216">Design your solution with fill rate in mind, since pixels will be your most precious resource.</span></span> <span data-ttu-id="84170-217">Cibler une géométrie solide sur la transparence.</span><span class="sxs-lookup"><span data-stu-id="84170-217">Target solid geometry over transparency.</span></span>

<span data-ttu-id="84170-218">Avec une solution de sauvegarde, vous pouvez ensuite démarrer superposition dans plus de complexité pour les machines de haut de gamme ou peut-être simplement améliorer la résolution de votre solution de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="84170-218">With a backup solution, you can then start layering in more complexity for high end machines or maybe just enhance resolution of your backup solution.</span></span>

<span data-ttu-id="84170-219">Concevoir pour le pire des cas et peut-être envisager à l’aide de rendu adaptatif pour des situations lourdes.</span><span class="sxs-lookup"><span data-stu-id="84170-219">Design for worst case scenarios, and maybe consider using adaptive rendering for heavy situations.</span></span>

## <a name="about-the-authors"></a><span data-ttu-id="84170-220">À propos des auteurs</span><span class="sxs-lookup"><span data-stu-id="84170-220">About the authors</span></span>

<table style="border:0">
<tr>
<td style="border:0" width="60px"><img alt="Picture of Robert Ferrese" width="60" height="60" src="images/robert-ferrese-60px.jpg"></td>
<td style="border:0"><span data-ttu-id="84170-221"><b>Robert Ferrese</b></span><span class="sxs-lookup"><span data-stu-id="84170-221"><b>Robert Ferrese</b></span></span><br><span data-ttu-id="84170-222">Ingénieur logiciel @Microsoft</span><span class="sxs-lookup"><span data-stu-id="84170-222">Software engineer @Microsoft</span></span></td>
</tr>
<tr>
<td style="border:0" width="60px"><img alt="Picture of Dan Andersson" width="60" height="60" src="images/dan-andersson-60px.jpg"></td>
<td style="border:0"><span data-ttu-id="84170-223"><b>Dan Andersson</b></span><span class="sxs-lookup"><span data-stu-id="84170-223"><b>Dan Andersson</b></span></span><br><span data-ttu-id="84170-224">Ingénieur logiciel @Microsoft</span><span class="sxs-lookup"><span data-stu-id="84170-224">Software engineer @Microsoft</span></span></td>
</tr>
</table>


## <a name="see-also"></a><span data-ttu-id="84170-225">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="84170-225">See also</span></span>
* [<span data-ttu-id="84170-226">Comprendre les performances pour la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="84170-226">Understanding Performance for Mixed Reality</span></span>](understanding-performance-for-mixed-reality.md)
* [<span data-ttu-id="84170-227">Recommandations relatives aux performances pour Unity</span><span class="sxs-lookup"><span data-stu-id="84170-227">Performance Recommendations for Unity</span></span>](performance-recommendations-for-unity.md)

 
