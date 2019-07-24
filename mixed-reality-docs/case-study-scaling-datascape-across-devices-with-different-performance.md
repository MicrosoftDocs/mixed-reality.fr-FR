---
title: 'Étude de cas: mise à l’échelle des datascape sur les appareils avec des performances différentes'
description: Cette étude de cas vous donne des informations sur la façon dont les développeurs Microsoft ont optimisé l’application datascape pour offrir une expérience attrayante sur les appareils avec un large éventail de fonctionnalités de performances.
author: danandersson
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: casque immersif, optimisation des performances, VR, étude de cas
ms.openlocfilehash: 990a5ee6de07b6416e3150a7885220409a9c8d93
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63523415"
---
# <a name="case-study---scaling-datascape-across-devices-with-different-performance"></a><span data-ttu-id="80233-104">Étude de cas: mise à l’échelle des datascape sur les appareils avec des performances différentes</span><span class="sxs-lookup"><span data-stu-id="80233-104">Case study - Scaling Datascape across devices with different performance</span></span>

<span data-ttu-id="80233-105">Datascape est une application Windows Mixed Reality développée en interne chez Microsoft, où nous nous sommes concentrés sur l’affichage des données météorologiques sur des données de terrain.</span><span class="sxs-lookup"><span data-stu-id="80233-105">Datascape is a Windows Mixed Reality application developed internally at Microsoft where we focused on displaying weather data on top of terrain data.</span></span> <span data-ttu-id="80233-106">L’application explore les Insights uniques que les utilisateurs obtiennent de la découverte de données en réalité mixte en entourant l’utilisateur de la visualisation de données holographiques.</span><span class="sxs-lookup"><span data-stu-id="80233-106">The application explores the unique insights users gain from discovering data in mixed reality by surrounding the user with holographic data visualization.</span></span>

<span data-ttu-id="80233-107">Pour datascape, nous souhaitons cibler une variété de plateformes avec des fonctionnalités matérielles différentes, allant de Microsoft HoloLens aux casques immersifs immersifs de Windows Mixed Real, et des PC moins alimentés aux PC les plus récents avec GPU haut de gamme.</span><span class="sxs-lookup"><span data-stu-id="80233-107">For Datascape we wanted to target a variety of platforms with different hardware capabilities ranging from Microsoft HoloLens to Windows Mixed Reality immersive headsets, and from lower-powered PCs to the very latest PCs with high-end GPU.</span></span> <span data-ttu-id="80233-108">Le principal défi était de rendre notre scène dans un souci visuel des appareils avec des fonctionnalités graphiques bien différentes en cours d’exécution à une fréquence élevée.</span><span class="sxs-lookup"><span data-stu-id="80233-108">The main challenge was rendering our scene in a visually appealing matter on devices with wildly different graphics capabilities while executing at a high framerate.</span></span>

<span data-ttu-id="80233-109">Cette étude de cas vous guidera dans le processus et les techniques utilisés pour créer certains de nos systèmes gourmands en GPU, en décrivant les problèmes que nous avons rencontrés et la façon dont nous les ont surmonté.</span><span class="sxs-lookup"><span data-stu-id="80233-109">This case study will walk through the process and techniques used to create some of our more GPU-intensive systems, describing the problems we encountered and how we overcame them.</span></span>

## <a name="transparency-and-overdraw"></a><span data-ttu-id="80233-110">Transparence et surdessin</span><span class="sxs-lookup"><span data-stu-id="80233-110">Transparency and overdraw</span></span>

<span data-ttu-id="80233-111">Notre principale difficulté de rendu est traitée par la transparence, car la transparence peut être coûteuse sur un GPU.</span><span class="sxs-lookup"><span data-stu-id="80233-111">Our main rendering struggles dealt with transparency, since transparency can be expensive on a GPU.</span></span>

<span data-ttu-id="80233-112">Une géométrie solide peut être rendue de l’avant vers l’arrière lors de l’écriture dans le tampon de profondeur, ce qui empêche la suppression de tout pixel futur situé derrière ce pixel.</span><span class="sxs-lookup"><span data-stu-id="80233-112">Solid geometry can be rendered front to back while writing to the depth buffer, stopping any future pixels located behind that pixel from being discarded.</span></span> <span data-ttu-id="80233-113">Cela empêche les pixels cachés d’exécuter le nuanceur de pixels, ce qui accélère considérablement le processus.</span><span class="sxs-lookup"><span data-stu-id="80233-113">This prevents hidden pixels from executing the pixel shader, speeding up the process significantly.</span></span> <span data-ttu-id="80233-114">Si la géométrie est triée de façon optimale, chaque pixel de l’écran est dessiné une seule fois.</span><span class="sxs-lookup"><span data-stu-id="80233-114">If geometry is sorted optimally, each pixel on the screen will be drawn only once.</span></span>

<span data-ttu-id="80233-115">La géométrie transparente doit être triée de nouveau vers l’avant et s’appuie sur la fusion de la sortie du nuanceur de pixels sur le pixel actuel de l’écran.</span><span class="sxs-lookup"><span data-stu-id="80233-115">Transparent geometry needs to be sorted back to front and relies on blending the output of the pixel shader to the current pixel on the screen.</span></span> <span data-ttu-id="80233-116">Cela peut entraîner le dessin de chaque pixel sur l’écran à plusieurs reprises par cadre, désigné sous le terme de «surdessin».</span><span class="sxs-lookup"><span data-stu-id="80233-116">This can result in each pixel on the screen being drawn to multiple times per frame, referred to as overdraw.</span></span>

<span data-ttu-id="80233-117">Pour les PC HoloLens et standard, l’écran ne peut être rempli qu’à quelques instants, ce qui rend le rendu transparent problématique.</span><span class="sxs-lookup"><span data-stu-id="80233-117">For HoloLens and mainstream PCs, the screen can only be filled a handful of times, making transparent rendering problematic.</span></span>

## <a name="introduction-to-datascape-scene-components"></a><span data-ttu-id="80233-118">Présentation des composants de scène datascape</span><span class="sxs-lookup"><span data-stu-id="80233-118">Introduction to Datascape scene components</span></span>

<span data-ttu-id="80233-119">Nous avions trois composants principaux pour notre scène. **l’interface utilisateur, la carte**et **la météo**.</span><span class="sxs-lookup"><span data-stu-id="80233-119">We had three major components to our scene; **the UI, the map**, and **the weather**.</span></span> <span data-ttu-id="80233-120">Nous savions très tôt que nos effets météorologiques nécessiteraient tout le temps processeur qu’il pouvait obtenir. nous avons donc conçu l’interface utilisateur et le terrain de manière à réduire tout surplus.</span><span class="sxs-lookup"><span data-stu-id="80233-120">We knew early on that our weather effects would require all the GPU time it could get, so we purposely designed the UI and terrain in a way that would reduce any overdraw.</span></span>

<span data-ttu-id="80233-121">Nous avons retravaillé l’interface utilisateur plusieurs fois afin de réduire le nombre de redessins qu’elle produirait.</span><span class="sxs-lookup"><span data-stu-id="80233-121">We reworked the UI several times to minimize the amount of overdraw it would produce.</span></span> <span data-ttu-id="80233-122">Nous sommes cotés du côté d’une géométrie plus complexe au lieu de superposer des illustrations transparentes les unes par rapport aux autres pour des composants tels que des boutons lumineux et des vues d’ensemble cartographiques.</span><span class="sxs-lookup"><span data-stu-id="80233-122">We erred on the side of more complex geometry rather than overlaying transparent art on top of each other for components like glowing buttons and map overviews.</span></span>

<span data-ttu-id="80233-123">Pour la carte, nous avons utilisé un nuanceur personnalisé qui supprime les fonctionnalités standard Unity, telles que les ombres et l’éclairage complexe, en les remplaçant par un modèle d’éclairage simple et un calcul de brouillard personnalisé.</span><span class="sxs-lookup"><span data-stu-id="80233-123">For the map, we used a custom shader that would strip out standard Unity features such as shadows and complex lighting, replacing them with a simple single sun lighting model and a custom fog calculation.</span></span> <span data-ttu-id="80233-124">Cela a produit un nuanceur de pixels simple et libère des cycles GPU.</span><span class="sxs-lookup"><span data-stu-id="80233-124">This produced a simple pixel shader and free up GPU cycles.</span></span>

<span data-ttu-id="80233-125">Nous sommes parvenus à faire en sorte que l’interface utilisateur et la carte soient rendues au budget, où nous n’avions pas besoin de modifier ces éléments en fonction du matériel; Toutefois, la visualisation des intempéries, en particulier le rendu du Cloud, s’est avérée plus complexe.</span><span class="sxs-lookup"><span data-stu-id="80233-125">We managed to get both the UI and the map to rendering at budget where we did not need any changes to them depending on the hardware; however, the weather visualization, in particular the cloud rendering, proved to be more of a challenge!</span></span>

## <a name="background-on-cloud-data"></a><span data-ttu-id="80233-126">Informations de base sur le Cloud</span><span class="sxs-lookup"><span data-stu-id="80233-126">Background on cloud data</span></span>

<span data-ttu-id="80233-127">Nos données Cloud ont été téléchargées à partir http://nomads.ncep.noaa.gov/) des serveurs NOAA (et nous nous sommes parvenues dans trois couches 2D distinctes, chacune avec la hauteur supérieure et inférieure du Cloud, ainsi que la densité du Cloud pour chaque cellule de la grille.</span><span class="sxs-lookup"><span data-stu-id="80233-127">Our cloud data was downloaded from NOAA servers (http://nomads.ncep.noaa.gov/) and came to us in three distinct 2D layers, each with the top and bottom height of the cloud, as well as the density of the cloud for each cell of the grid.</span></span> <span data-ttu-id="80233-128">Les données ont été traitées dans une texture d’informations de Cloud où chaque composant était stocké dans le composant rouge, vert et bleu de la texture pour un accès facile sur le GPU.</span><span class="sxs-lookup"><span data-stu-id="80233-128">The data got processed into a cloud info texture where each component was stored in the red, green, and blue component of the texture for easy access on the GPU.</span></span>

## <a name="geometry-clouds"></a><span data-ttu-id="80233-129">Clouds Geometry</span><span class="sxs-lookup"><span data-stu-id="80233-129">Geometry clouds</span></span>

<span data-ttu-id="80233-130">Pour vous assurer que nos machines à faible consommation d’énergie pourraient afficher nos Clouds, nous avons décidé de commencer par une approche qui utiliserait une géométrie solide pour réduire le surdessin.</span><span class="sxs-lookup"><span data-stu-id="80233-130">To make sure our lower-powered machines could render our clouds we decided to start with an approach that would use solid geometry to minimize overdraw.</span></span>

<span data-ttu-id="80233-131">Nous avons tout d’abord essayé de produire des clouds en générant un maillage relief solide pour chaque couche en utilisant le rayon de la texture d’informations de Cloud par vertex pour générer la forme.</span><span class="sxs-lookup"><span data-stu-id="80233-131">We first tried producing clouds by generating a solid heightmap mesh for each layer using the radius of the cloud info texture per vertex to generate the shape.</span></span> <span data-ttu-id="80233-132">Nous avons utilisé un nuanceur Geometry pour produire les sommets en haut et en bas du Cloud générant des formes Cloud solides.</span><span class="sxs-lookup"><span data-stu-id="80233-132">We used a geometry shader to produce the vertices both at the top and the bottom of the cloud generating solid cloud shapes.</span></span> <span data-ttu-id="80233-133">Nous avons utilisé la valeur de densité de la texture pour colorer le Cloud avec des couleurs plus sombres pour des clouds plus denses.</span><span class="sxs-lookup"><span data-stu-id="80233-133">We used the density value from the texture to color the cloud with darker colors for more dense clouds.</span></span>

<span data-ttu-id="80233-134">**Nuanceur pour la création des vertex:**</span><span class="sxs-lookup"><span data-stu-id="80233-134">**Shader for creating the vertices:**</span></span>

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

<span data-ttu-id="80233-135">Nous avons introduit un petit modèle de bruit pour obtenir plus de détails sur les données réelles.</span><span class="sxs-lookup"><span data-stu-id="80233-135">We introduced a small noise pattern to get more detail on top of the real data.</span></span> <span data-ttu-id="80233-136">Pour produire des bords du Cloud arrondis, nous avons tronqué les pixels dans le nuanceur de pixels lorsque la valeur de rayon interpolée atteint un seuil pour ignorer les valeurs proches de zéro.</span><span class="sxs-lookup"><span data-stu-id="80233-136">To produce round cloud edges, we clipped the pixels in the pixel shader when the interpolated radius value hit a threshold to discard near-zero values.</span></span>

![Clouds Geometry](images/datascape-geometry-clouds-700px.jpg)

<span data-ttu-id="80233-138">Dans la mesure où les clouds sont de géométrie solide, ils peuvent être rendus avant le terrain pour masquer les pixels de la carte onéreux en dessous pour améliorer davantage la fréquence d’images.</span><span class="sxs-lookup"><span data-stu-id="80233-138">Since the clouds are solid geometry, they can be rendered before the terrain to hide any expensive map pixels underneath to further improve framerate.</span></span> <span data-ttu-id="80233-139">Cette solution s’est correctement exécutée sur toutes les cartes graphiques de min-spec aux cartes graphiques haut de gamme, ainsi que sur HoloLens, en raison de l’approche de rendu géométrique solide.</span><span class="sxs-lookup"><span data-stu-id="80233-139">This solution ran well on all graphics cards from min-spec to high-end graphics cards, as well as on HoloLens, because of the solid geometry rendering approach.</span></span>

## <a name="solid-particle-clouds"></a><span data-ttu-id="80233-140">Clouds particulaires solides</span><span class="sxs-lookup"><span data-stu-id="80233-140">Solid particle clouds</span></span>

<span data-ttu-id="80233-141">Nous avions maintenant une solution de sauvegarde qui produisait une représentation correcte de nos données Cloud, mais était un peu lackluster dans le facteur «wow» et n’indiquait pas le sentiment que nous souhaitions pour nos machines haut de gamme.</span><span class="sxs-lookup"><span data-stu-id="80233-141">We now had a backup solution that produced a decent representation of our cloud data, but was a bit lackluster in the “wow” factor and did not convey the volumetric feel that we wanted for our high-end machines.</span></span>

<span data-ttu-id="80233-142">L’étape suivante consistait à créer les clouds en les représentant avec environ 100 000 particules pour produire un look plus organique et volumétrique.</span><span class="sxs-lookup"><span data-stu-id="80233-142">Our next step was creating the clouds by representing them with approximately 100,000 particles to produce a more organic and volumetric look.</span></span>

<span data-ttu-id="80233-143">Si les particules restent solides et sont triées avant l’arrière, nous pouvons toujours tirer parti de l’élimination de la mémoire tampon de profondeur des pixels situés derrière les particules rendues précédemment, réduisant ainsi le surdessin.</span><span class="sxs-lookup"><span data-stu-id="80233-143">If particles stay solid and sort front-to-back, we can still benefit from depth buffer culling of the pixels behind previously rendered particles, reducing the overdraw.</span></span> <span data-ttu-id="80233-144">En outre, avec une solution basée sur les particules, nous pouvons modifier la quantité de particules utilisée pour cibler un matériel différent.</span><span class="sxs-lookup"><span data-stu-id="80233-144">Also, with a particle-based solution, we can alter the amount of particles used to target different hardware.</span></span> <span data-ttu-id="80233-145">Toutefois, tous les pixels doivent toujours être testés de manière approfondie, ce qui entraîne une surcharge supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="80233-145">However, all pixels still need to be depth tested, which results in some additional overhead.</span></span>

<span data-ttu-id="80233-146">Tout d’abord, nous avons créé des positions de particule autour du point central de l’expérience au démarrage.</span><span class="sxs-lookup"><span data-stu-id="80233-146">First, we created particle positions around the center point of the experience at startup.</span></span> <span data-ttu-id="80233-147">Nous avons distribué les particules de manière plus dense à travers le centre et moins à distance.</span><span class="sxs-lookup"><span data-stu-id="80233-147">We distributed the particles more densely around the center and less so in the distance.</span></span> <span data-ttu-id="80233-148">Nous avons pré-trié toutes les particules du centre vers l’arrière afin que les particules les plus proches s’affichent en premier.</span><span class="sxs-lookup"><span data-stu-id="80233-148">We pre-sorted all particles from the center to the back so that the closest particles would render first.</span></span>

<span data-ttu-id="80233-149">Un nuanceur de calcul échantillonne la texture d’informations Cloud pour positionner chaque particule à une hauteur correcte et la colorier en fonction de la densité.</span><span class="sxs-lookup"><span data-stu-id="80233-149">A compute shader would sample the cloud info texture to position each particle at a correct height and color it based on the density.</span></span>

<span data-ttu-id="80233-150">Nous avons utilisé *DrawProcedural* pour effectuer le rendu d’un quadruple par particule permettant aux données de particule de rester sur le GPU à tout moment.</span><span class="sxs-lookup"><span data-stu-id="80233-150">We used *DrawProcedural* to render a quad per particle allowing the particle data to stay on the GPU at all times.</span></span>

<span data-ttu-id="80233-151">Chaque particule contenait à la fois une hauteur et un rayon.</span><span class="sxs-lookup"><span data-stu-id="80233-151">Each particle contained both a height and a radius.</span></span> <span data-ttu-id="80233-152">La hauteur était basée sur les données Cloud échantillonnées à partir de la texture informations sur le Cloud, et le rayon était basé sur la distribution initiale où il serait calculé pour stocker la distance horizontale sur son voisin le plus proche.</span><span class="sxs-lookup"><span data-stu-id="80233-152">The height was based on the cloud data sampled from the cloud info texture, and the radius was based on the initial distribution where it would be calculated to store the horizontal distance to its closest neighbor.</span></span> <span data-ttu-id="80233-153">Les quadruples utilisent ces données pour s’orienter de manière à s’orienter de façon verticale, de sorte que lorsque les utilisateurs regardent les données horizontalement, la hauteur est indiquée et, lorsque les utilisateurs l’observent de haut en haut, la zone entre ses voisins est couverte.</span><span class="sxs-lookup"><span data-stu-id="80233-153">The quads would use this data to orient itself angled by the height so that when users look at it horizontally, the height would be shown, and when users looked at it top-down, the area between its neighbors would be covered.</span></span>

![Forme de particule](images/particle-shape-700px.png)

<span data-ttu-id="80233-155">**Code du nuanceur présentant la distribution:**</span><span class="sxs-lookup"><span data-stu-id="80233-155">**Shader code showing the distribution:**</span></span>

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

<span data-ttu-id="80233-156">Étant donné que nous triant les particules de l’avant vers l’arrière et que nous avons toujours utilisé un nuanceur de style plein pour découper (pas mélanger) les pixels transparents, cette technique gère une quantité étonnamment importante de particules, ce qui évite les surcharges coûteuses, même sur les machines de faible consommation.</span><span class="sxs-lookup"><span data-stu-id="80233-156">Since we sort the particles front-to-back and we still used a solid style shader to clip (not blend) transparent pixels, this technique handles a surprising amount of particles, avoiding costly over-draw even on the lower-powered machines.</span></span>

## <a name="transparent-particle-clouds"></a><span data-ttu-id="80233-157">Clouds particulaires transparents</span><span class="sxs-lookup"><span data-stu-id="80233-157">Transparent particle clouds</span></span>

<span data-ttu-id="80233-158">Les particules solides offraient une bonne sensation organique à la forme des clouds, tout en nécessitant des choses pour vendre le fluffiness de clouds.</span><span class="sxs-lookup"><span data-stu-id="80233-158">The solid particles provided a good organic feel to the shape of the clouds but still needed something to sell the fluffiness of clouds.</span></span> <span data-ttu-id="80233-159">Nous avons décidé d’essayer une solution personnalisée pour les cartes graphiques haut de gamme où nous pouvons introduire la transparence.</span><span class="sxs-lookup"><span data-stu-id="80233-159">We decided to try a custom solution for the high-end graphics cards where we can introduce transparency.</span></span>

<span data-ttu-id="80233-160">Pour ce faire, nous avons simplement basculé l’ordre de tri initial des particules et modifié le nuanceur pour utiliser les textures alpha.</span><span class="sxs-lookup"><span data-stu-id="80233-160">To do this we simply switched the initial sorting order of the particles and changed the shader to use the textures alpha.</span></span>

![Clouds fluffy](images/fluffy-clouds-700px.jpg)

<span data-ttu-id="80233-162">Il s’est avéré bien, mais il s’est avéré trop lourd pour les machines les plus difficiles, car cela entraînerait le rendu de chaque pixel à l’écran des centaines de fois!</span><span class="sxs-lookup"><span data-stu-id="80233-162">It looked great but proved to be too heavy for even the toughest machines since it would result in rendering each pixel on the screen hundreds of times!</span></span>

## <a name="render-off-screen-with-lower-resolution"></a><span data-ttu-id="80233-163">Rendre hors écran avec une résolution inférieure</span><span class="sxs-lookup"><span data-stu-id="80233-163">Render off-screen with lower resolution</span></span>

<span data-ttu-id="80233-164">Pour réduire le nombre de pixels rendus par les Clouds, nous avons commencé à les afficher dans une mémoire tampon de résolution de trimestre (par rapport à l’écran) et à étirer le résultat final sur l’écran une fois que toutes les particules ont été dessinées.</span><span class="sxs-lookup"><span data-stu-id="80233-164">To reduce the number of pixels rendered by the clouds, we started rendering them in a quarter resolution buffer (compared to the screen) and stretching the end result back up onto the screen after all the particles had been drawn.</span></span> <span data-ttu-id="80233-165">Cela nous a donné environ une accélération de 4 fois, mais il a été fourni avec quelques avertissements.</span><span class="sxs-lookup"><span data-stu-id="80233-165">This gave us roughly a 4x speedup, but came with a couple of caveats.</span></span>

<span data-ttu-id="80233-166">**Code pour le rendu hors écran:**</span><span class="sxs-lookup"><span data-stu-id="80233-166">**Code for rendering off-screen:**</span></span>

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

<span data-ttu-id="80233-167">Tout d’abord, lors du rendu dans une mémoire tampon hors écran, nous avons perdu toutes les informations de profondeur de notre scène principale, ce qui a pour résultat des particules sous-jacentes au rendu des montagnes en plus de la montagne.</span><span class="sxs-lookup"><span data-stu-id="80233-167">First, when rendering into an off-screen buffer, we lost all depth information from our main scene, resulting in particles behind mountains rendering on top of the mountain.</span></span>

<span data-ttu-id="80233-168">Deuxièmement, l’étirement de la mémoire tampon a également introduit des artefacts sur les bords de nos Clouds où le changement de résolution était perceptible.</span><span class="sxs-lookup"><span data-stu-id="80233-168">Second, stretching the buffer also introduced artifacts on the edges of our clouds where the resolution change was noticeable.</span></span> <span data-ttu-id="80233-169">Les deux sections suivantes expliquent comment nous avons résolu ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="80233-169">The next two sections talk about how we resolved these issues.</span></span>

## <a name="particle-depth-buffer"></a><span data-ttu-id="80233-170">Mémoire tampon de profondeur des particules</span><span class="sxs-lookup"><span data-stu-id="80233-170">Particle depth buffer</span></span>

<span data-ttu-id="80233-171">Pour faire en sorte que les particules coexistent avec la géométrie du monde où une montagne ou un objet peut couvrir des particules en arrière-plan, nous avons rempli la mémoire tampon hors écran avec une mémoire tampon de profondeur contenant la géométrie de la scène principale.</span><span class="sxs-lookup"><span data-stu-id="80233-171">To make the particles co-exist with the world geometry where a mountain or object could cover particles behind it, we populated the off-screen buffer with a depth buffer containing the geometry of the main scene.</span></span> <span data-ttu-id="80233-172">Pour produire une telle mémoire tampon de profondeur, nous avons créé une deuxième caméra, en rendant uniquement la géométrie solide et la profondeur de la scène.</span><span class="sxs-lookup"><span data-stu-id="80233-172">To produce such depth buffer, we created a second camera, rendering only the solid geometry and depth of the scene.</span></span>

<span data-ttu-id="80233-173">Nous avons ensuite utilisé la nouvelle texture dans le nuanceur de pixels des clouds pour occultait pixels.</span><span class="sxs-lookup"><span data-stu-id="80233-173">We then used the new texture in the pixel shader of the clouds to occlude pixels.</span></span> <span data-ttu-id="80233-174">Nous avons utilisé la même texture pour calculer la distance à la géométrie derrière un pixel du Cloud.</span><span class="sxs-lookup"><span data-stu-id="80233-174">We used the same texture to calculate the distance to the geometry behind a cloud pixel.</span></span> <span data-ttu-id="80233-175">En utilisant cette distance et en l’appliquant à l’alpha du pixel, nous avons à présent vu l’effet des clouds à mesure qu’ils se rapprochent du terrain, éliminant les coupes difficiles où les particules et le terrain se rencontrent.</span><span class="sxs-lookup"><span data-stu-id="80233-175">By using that distance and applying it to the alpha of the pixel, we now had the effect of clouds fading out as they get close to terrain, removing any hard cuts where particles and terrain meet.</span></span>

![Clouds mélangés dans le terrain](images/clouds-blended-to-terrain-700px.jpg)

## <a name="sharpening-the-edges"></a><span data-ttu-id="80233-177">Amélioration de la netteté des bords</span><span class="sxs-lookup"><span data-stu-id="80233-177">Sharpening the edges</span></span>

<span data-ttu-id="80233-178">Les clouds étirés recherchaient presque identiques aux clouds de taille normale au centre des particules ou à l’endroit où ils se chevauchaient, mais affichaient certains artefacts sur les bords du Cloud.</span><span class="sxs-lookup"><span data-stu-id="80233-178">The stretched-up clouds looked almost identical to the normal size clouds at the center of the particles or where they overlapped, but showed some artifacts at the cloud edges.</span></span> <span data-ttu-id="80233-179">Sinon, les bords nets apparaîtraient flous et les effets d’alias ont été introduits lors du déplacement de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="80233-179">Otherwise sharp edges would appear blurry and alias effects were introduced when the camera moved.</span></span>

<span data-ttu-id="80233-180">Nous avons résolu cela en exécutant un nuanceur simple sur la mémoire tampon hors écran pour déterminer où des changements importants ont été apportés (1).</span><span class="sxs-lookup"><span data-stu-id="80233-180">We solved this by running a simple shader on the off-screen buffer to determine where big changes in contrast occurred (1).</span></span> <span data-ttu-id="80233-181">Nous plaçons les pixels avec des modifications importantes dans une nouvelle mémoire tampon de stencil (2).</span><span class="sxs-lookup"><span data-stu-id="80233-181">We put the pixels with big changes into a new stencil buffer (2).</span></span> <span data-ttu-id="80233-182">Nous avons ensuite utilisé la mémoire tampon stencil pour masquer ces zones à contraste élevé lors de l’application de la mémoire tampon hors écran à l’écran, ce qui entraîne des trous dans et autour des Clouds (3).</span><span class="sxs-lookup"><span data-stu-id="80233-182">We then used the stencil buffer to mask out these high contrast areas when applying the off-screen buffer back to the screen, resulting in holes in and around the clouds (3).</span></span>

<span data-ttu-id="80233-183">Nous avons ensuite rendu toutes les particules en mode plein écran, mais cette fois, il a utilisé la mémoire tampon stencil pour masquer tout ce qui est à l’exception des bords, ce qui entraîne un ensemble minimal de pixels horodatés (4).</span><span class="sxs-lookup"><span data-stu-id="80233-183">We then rendered all the particles again in full-screen mode, but this time used the stencil buffer to mask out everything but the edges, resulting in a minimal set of pixels touched (4).</span></span> <span data-ttu-id="80233-184">Étant donné que la mémoire tampon de commande a déjà été créée pour les particules, nous avons simplement dû la restituer à nouveau à la nouvelle caméra.</span><span class="sxs-lookup"><span data-stu-id="80233-184">Since the command buffer was already created for the particles, we simply had to render it again to the new camera.</span></span>

![Progression du rendu des bords du Cloud](images/cloud-steps-1-4-700px.jpg)

<span data-ttu-id="80233-186">Le résultat final était une arête aiguë avec des sections Centre bon marché des clouds.</span><span class="sxs-lookup"><span data-stu-id="80233-186">The end result was sharp edges with cheap center sections of the clouds.</span></span>

<span data-ttu-id="80233-187">Bien que cela soit beaucoup plus rapide que le rendu de toutes les particules en plein écran, il y a toujours un coût associé au test d’un pixel par rapport à la mémoire tampon des stencils, ce qui entraîne un coût considérable.</span><span class="sxs-lookup"><span data-stu-id="80233-187">While this was much faster than rendering all particles in full screen, there is still a cost associated with testing a pixel against the stencil buffer, so a massive amount of overdraw still came with a cost.</span></span>

## <a name="culling-particles"></a><span data-ttu-id="80233-188">Élimination des particules</span><span class="sxs-lookup"><span data-stu-id="80233-188">Culling particles</span></span>

<span data-ttu-id="80233-189">Pour notre effet vent, nous avons généré des bandes de triangle longues dans un nuanceur de calcul, créant de nombreux WISPs du vent dans le monde.</span><span class="sxs-lookup"><span data-stu-id="80233-189">For our wind effect, we generated long triangle strips in a compute shader, creating many wisps of wind in the world.</span></span> <span data-ttu-id="80233-190">Alors que l’effet vent n’était pas lourd sur le taux de remplissage en raison des bandes de pelures générées, il produisait plusieurs centaines de milliers de vertex, ce qui entraînait une charge importante pour le nuanceur de sommets.</span><span class="sxs-lookup"><span data-stu-id="80233-190">While the wind effect was not heavy on fill rate due to skinny strips generated, it produced many hundreds of thousands of vertices resulting in a heavy load for the vertex shader.</span></span>

<span data-ttu-id="80233-191">Nous avons introduit des tampons d’ajout sur le nuanceur de calcul pour alimenter un sous-ensemble des bandes à dessiner.</span><span class="sxs-lookup"><span data-stu-id="80233-191">We introduced append buffers on the compute shader to feed a subset of the wind strips to be drawn.</span></span> <span data-ttu-id="80233-192">Avec une vue simple frustum l’élimination de la logique dans le nuanceur de calcul, nous pourrions déterminer si une bande était en dehors de la vue caméra et l’empêcher d’être ajoutée à la mémoire tampon d’envoi (push).</span><span class="sxs-lookup"><span data-stu-id="80233-192">With some simple view frustum culling logic in the compute shader, we could determine if a strip was outside of camera view and prevent it from being added to the push buffer.</span></span> <span data-ttu-id="80233-193">Cela a considérablement réduit la quantité de bandes, ce qui libère des cycles nécessaires sur le GPU.</span><span class="sxs-lookup"><span data-stu-id="80233-193">This reduced the amount of strips significantly, freeing up some needed cycles on the GPU.</span></span>

<span data-ttu-id="80233-194">**Code illustrant une mémoire tampon d’ajout:**</span><span class="sxs-lookup"><span data-stu-id="80233-194">**Code demonstrating an append buffer:**</span></span>

<span data-ttu-id="80233-195">*Nuanceur de calcul:*</span><span class="sxs-lookup"><span data-stu-id="80233-195">*Compute shader:*</span></span>

```
AppendStructuredBuffer<int> culledParticleIdx;
 
if (show)
    culledParticleIdx.Append(id.x);
```

<span data-ttu-id="80233-196">*C#code*</span><span class="sxs-lookup"><span data-stu-id="80233-196">*C# code:*</span></span>

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

<span data-ttu-id="80233-197">Nous avons essayé d’utiliser la même technique sur les particules du Cloud, où nous les sélectionnons dans le nuanceur de calcul et transmettons uniquement les particules visibles pour être rendues.</span><span class="sxs-lookup"><span data-stu-id="80233-197">We tried using the same technique on the cloud particles, where we would cull them on the compute shader and only push the visible particles to be rendered.</span></span> <span data-ttu-id="80233-198">En fait, cette technique ne nous a pas permis de gagner beaucoup de temps sur le GPU puisque le plus grand goulot d’étranglement était le nombre de pixels rendu sur l’écran, et non le coût du calcul des vertex.</span><span class="sxs-lookup"><span data-stu-id="80233-198">This technique actually did not save us much on the GPU since the biggest bottleneck was the amount pixels rendered on the screen, and not the cost of calculating the vertices.</span></span>

<span data-ttu-id="80233-199">L’autre problème avec cette technique était que la mémoire tampon d’ajout était remplie dans un ordre aléatoire en raison de sa nature parallélisée du calcul des particules, provoquant la non-tri des particules triées, entraînant le scintillement des particules du Cloud.</span><span class="sxs-lookup"><span data-stu-id="80233-199">The other problem with this technique was that the append buffer populated in random order due to its parallelized nature of computing the particles, causing the sorted particles to be un-sorted, resulting in flickering cloud particles.</span></span>

<span data-ttu-id="80233-200">Il existe des techniques permettant de trier la mémoire tampon d’envoi, mais le gain de performances limité que nous avons rencontré pour l’élimination des particules serait probablement compensé par un tri supplémentaire, donc nous avons décidé de ne pas poursuivre cette optimisation.</span><span class="sxs-lookup"><span data-stu-id="80233-200">There are techniques to sort the push buffer, but the limited amount of performance gain we got out of culling particles would likely be offset with an additional sort, so we decided to not pursue this optimization.</span></span>

## <a name="adaptive-rendering"></a><span data-ttu-id="80233-201">Rendu adaptatif</span><span class="sxs-lookup"><span data-stu-id="80233-201">Adaptive rendering</span></span>

<span data-ttu-id="80233-202">Pour garantir une cadence constante sur une application avec des conditions de rendu variables telles qu’une vue en clair et une vue claire, nous avons introduit un rendu adaptatif pour notre application.</span><span class="sxs-lookup"><span data-stu-id="80233-202">To ensure a steady framerate on an app with varying rendering conditions like a cloudy vs a clear view, we introduced adaptive rendering to our app.</span></span>

<span data-ttu-id="80233-203">La première étape du rendu adaptatif consiste à mesurer le GPU.</span><span class="sxs-lookup"><span data-stu-id="80233-203">The first step of adaptive rendering is to measure GPU.</span></span> <span data-ttu-id="80233-204">Nous l’avons fait en insérant du code personnalisé dans la mémoire tampon de commande GPU au début et à la fin d’un frame rendu, en capturant à la fois l’heure de gauche et de droite de l’écran.</span><span class="sxs-lookup"><span data-stu-id="80233-204">We did this by inserting custom code into the GPU command buffer at the beginning and the end of a rendered frame, capturing both the left and right eye screen time.</span></span>

<span data-ttu-id="80233-205">En mesurant le temps passé à effectuer le rendu et en le comparant au taux d’actualisation souhaité, nous avons un sens de la fermeture des frames.</span><span class="sxs-lookup"><span data-stu-id="80233-205">By measuring the time spent rendering and comparing it to our desired refresh-rate we got a sense of how close we were to dropping frames.</span></span>

<span data-ttu-id="80233-206">Lorsque vous approchez de la suppression des frames, nous adaptons notre rendu pour le rendre plus rapide.</span><span class="sxs-lookup"><span data-stu-id="80233-206">When close to dropping frames, we adapt our rendering to make it faster.</span></span> <span data-ttu-id="80233-207">Une méthode simple d’adaptation consiste à modifier la taille de la fenêtre d’affichage de l’écran, ce qui nécessite moins de pixels pour être rendu.</span><span class="sxs-lookup"><span data-stu-id="80233-207">One simple way of adapting is changing the viewport size of the screen, requiring less pixels to get rendered.</span></span>

<span data-ttu-id="80233-208">À l’aide de *UnityEngine. XR. XRSettings. renderViewportScale* le système réduit la fenêtre d’affichage ciblée et étire automatiquement le résultat en fonction de l’écran.</span><span class="sxs-lookup"><span data-stu-id="80233-208">By using *UnityEngine.XR.XRSettings.renderViewportScale* the system shrinks the targeted viewport and automatically stretches the result back up to fit the screen.</span></span> <span data-ttu-id="80233-209">Une petite modification de l’échelle est à peine perceptible sur la géométrie universelle et un facteur d’échelle de 0,7 nécessite la moitié du nombre de pixels à afficher.</span><span class="sxs-lookup"><span data-stu-id="80233-209">A small change in scale is barely noticeable on world geometry, and a scale factor of 0.7 requires half the amount of pixels to be rendered.</span></span>

![échelle de 70%, moitié des pixels](images/datascape-scaling-700px.jpg)

<span data-ttu-id="80233-211">Quand nous détectons que nous nous apprêtons à supprimer des trames, nous réduisons l’échelle d’un nombre fixe, puis nous les augmentons quand nous exécutons à nouveau rapidement.</span><span class="sxs-lookup"><span data-stu-id="80233-211">When we detect that we are about to drop frames we lower the scale by a fixed number, and increase it back when we are running fast enough again.</span></span>

<span data-ttu-id="80233-212">Bien que nous ayons décidé de la technique Cloud à utiliser en fonction des capacités graphiques du matériel au démarrage, il est possible de la baser sur les données de la mesure GPU pour empêcher le système de se maintenir à une résolution faible pendant une longue période, mais ce n’est pas un temps  pour explorer dans datascape.</span><span class="sxs-lookup"><span data-stu-id="80233-212">While we decided what cloud technique to use based on graphics capabilities of the hardware at startup, it is possible to base it on data from the GPU measurement to prevent the system from staying at low resolution for a long time, but this is something we did not have time to explore in Datascape.</span></span>

## <a name="final-thoughts"></a><span data-ttu-id="80233-213">Réflexions finales</span><span class="sxs-lookup"><span data-stu-id="80233-213">Final thoughts</span></span>

<span data-ttu-id="80233-214">Le ciblage d’une variété de matériel est difficile et nécessite une certaine planification.</span><span class="sxs-lookup"><span data-stu-id="80233-214">Targeting a variety of hardware is challenging and requires some planning.</span></span>

<span data-ttu-id="80233-215">Nous vous recommandons de commencer à cibler des machines à faible consommation pour vous familiariser avec l’espace à problème et de développer une solution de sauvegarde qui s’exécutera sur tous vos ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="80233-215">We recommend that you start targeting lower-powered machines to get familiar with the problem space and develop a backup solution that will run on all your machines.</span></span> <span data-ttu-id="80233-216">Concevez votre solution avec le taux de remplissage à l’esprit, car les pixels seront vos ressources les plus précieuses.</span><span class="sxs-lookup"><span data-stu-id="80233-216">Design your solution with fill rate in mind, since pixels will be your most precious resource.</span></span> <span data-ttu-id="80233-217">Cible solide Geometry sur la transparence.</span><span class="sxs-lookup"><span data-stu-id="80233-217">Target solid geometry over transparency.</span></span>

<span data-ttu-id="80233-218">Avec une solution de sauvegarde, vous pouvez commencer à superposer des couches plus complexes pour les machines de haut niveau ou peut-être simplement améliorer la résolution de votre solution de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="80233-218">With a backup solution, you can then start layering in more complexity for high end machines or maybe just enhance resolution of your backup solution.</span></span>

<span data-ttu-id="80233-219">Conception pour les pires scénarios et peut-être envisager l’utilisation d’un rendu adaptatif pour des situations lourdes.</span><span class="sxs-lookup"><span data-stu-id="80233-219">Design for worst case scenarios, and maybe consider using adaptive rendering for heavy situations.</span></span>

## <a name="about-the-authors"></a><span data-ttu-id="80233-220">À propos des auteurs</span><span class="sxs-lookup"><span data-stu-id="80233-220">About the authors</span></span>

<table style="border:0">
<tr>
<td style="border:0" width="60px"><img alt="Picture of Robert Ferrese" width="60" height="60" src="images/robert-ferrese-60px.jpg"></td>
<td style="border:0"><span data-ttu-id="80233-221"><b>Robert Ferrese</b></span><span class="sxs-lookup"><span data-stu-id="80233-221"><b>Robert Ferrese</b></span></span><br><span data-ttu-id="80233-222">Ingénieur logiciel@Microsoft</span><span class="sxs-lookup"><span data-stu-id="80233-222">Software engineer @Microsoft</span></span></td>
</tr>
<tr>
<td style="border:0" width="60px"><img alt="Picture of Dan Andersson" width="60" height="60" src="images/dan-andersson-60px.jpg"></td>
<td style="border:0"><span data-ttu-id="80233-223"><b>Dan Andersson</b></span><span class="sxs-lookup"><span data-stu-id="80233-223"><b>Dan Andersson</b></span></span><br><span data-ttu-id="80233-224">Ingénieur logiciel@Microsoft</span><span class="sxs-lookup"><span data-stu-id="80233-224">Software engineer @Microsoft</span></span></td>
</tr>
</table>


## <a name="see-also"></a><span data-ttu-id="80233-225">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="80233-225">See also</span></span>
* [<span data-ttu-id="80233-226">Comprendre les performances de la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="80233-226">Understanding Performance for Mixed Reality</span></span>](understanding-performance-for-mixed-reality.md)
* [<span data-ttu-id="80233-227">Recommandations en matière de performances pour Unity</span><span class="sxs-lookup"><span data-stu-id="80233-227">Performance Recommendations for Unity</span></span>](performance-recommendations-for-unity.md)

 
