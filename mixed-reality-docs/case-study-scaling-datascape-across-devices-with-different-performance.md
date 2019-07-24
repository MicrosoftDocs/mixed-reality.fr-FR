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
# <a name="case-study---scaling-datascape-across-devices-with-different-performance"></a>Étude de cas: mise à l’échelle des datascape sur les appareils avec des performances différentes

Datascape est une application Windows Mixed Reality développée en interne chez Microsoft, où nous nous sommes concentrés sur l’affichage des données météorologiques sur des données de terrain. L’application explore les Insights uniques que les utilisateurs obtiennent de la découverte de données en réalité mixte en entourant l’utilisateur de la visualisation de données holographiques.

Pour datascape, nous souhaitons cibler une variété de plateformes avec des fonctionnalités matérielles différentes, allant de Microsoft HoloLens aux casques immersifs immersifs de Windows Mixed Real, et des PC moins alimentés aux PC les plus récents avec GPU haut de gamme. Le principal défi était de rendre notre scène dans un souci visuel des appareils avec des fonctionnalités graphiques bien différentes en cours d’exécution à une fréquence élevée.

Cette étude de cas vous guidera dans le processus et les techniques utilisés pour créer certains de nos systèmes gourmands en GPU, en décrivant les problèmes que nous avons rencontrés et la façon dont nous les ont surmonté.

## <a name="transparency-and-overdraw"></a>Transparence et surdessin

Notre principale difficulté de rendu est traitée par la transparence, car la transparence peut être coûteuse sur un GPU.

Une géométrie solide peut être rendue de l’avant vers l’arrière lors de l’écriture dans le tampon de profondeur, ce qui empêche la suppression de tout pixel futur situé derrière ce pixel. Cela empêche les pixels cachés d’exécuter le nuanceur de pixels, ce qui accélère considérablement le processus. Si la géométrie est triée de façon optimale, chaque pixel de l’écran est dessiné une seule fois.

La géométrie transparente doit être triée de nouveau vers l’avant et s’appuie sur la fusion de la sortie du nuanceur de pixels sur le pixel actuel de l’écran. Cela peut entraîner le dessin de chaque pixel sur l’écran à plusieurs reprises par cadre, désigné sous le terme de «surdessin».

Pour les PC HoloLens et standard, l’écran ne peut être rempli qu’à quelques instants, ce qui rend le rendu transparent problématique.

## <a name="introduction-to-datascape-scene-components"></a>Présentation des composants de scène datascape

Nous avions trois composants principaux pour notre scène. **l’interface utilisateur, la carte**et **la météo**. Nous savions très tôt que nos effets météorologiques nécessiteraient tout le temps processeur qu’il pouvait obtenir. nous avons donc conçu l’interface utilisateur et le terrain de manière à réduire tout surplus.

Nous avons retravaillé l’interface utilisateur plusieurs fois afin de réduire le nombre de redessins qu’elle produirait. Nous sommes cotés du côté d’une géométrie plus complexe au lieu de superposer des illustrations transparentes les unes par rapport aux autres pour des composants tels que des boutons lumineux et des vues d’ensemble cartographiques.

Pour la carte, nous avons utilisé un nuanceur personnalisé qui supprime les fonctionnalités standard Unity, telles que les ombres et l’éclairage complexe, en les remplaçant par un modèle d’éclairage simple et un calcul de brouillard personnalisé. Cela a produit un nuanceur de pixels simple et libère des cycles GPU.

Nous sommes parvenus à faire en sorte que l’interface utilisateur et la carte soient rendues au budget, où nous n’avions pas besoin de modifier ces éléments en fonction du matériel; Toutefois, la visualisation des intempéries, en particulier le rendu du Cloud, s’est avérée plus complexe.

## <a name="background-on-cloud-data"></a>Informations de base sur le Cloud

Nos données Cloud ont été téléchargées à partir http://nomads.ncep.noaa.gov/) des serveurs NOAA (et nous nous sommes parvenues dans trois couches 2D distinctes, chacune avec la hauteur supérieure et inférieure du Cloud, ainsi que la densité du Cloud pour chaque cellule de la grille. Les données ont été traitées dans une texture d’informations de Cloud où chaque composant était stocké dans le composant rouge, vert et bleu de la texture pour un accès facile sur le GPU.

## <a name="geometry-clouds"></a>Clouds Geometry

Pour vous assurer que nos machines à faible consommation d’énergie pourraient afficher nos Clouds, nous avons décidé de commencer par une approche qui utiliserait une géométrie solide pour réduire le surdessin.

Nous avons tout d’abord essayé de produire des clouds en générant un maillage relief solide pour chaque couche en utilisant le rayon de la texture d’informations de Cloud par vertex pour générer la forme. Nous avons utilisé un nuanceur Geometry pour produire les sommets en haut et en bas du Cloud générant des formes Cloud solides. Nous avons utilisé la valeur de densité de la texture pour colorer le Cloud avec des couleurs plus sombres pour des clouds plus denses.

**Nuanceur pour la création des vertex:**

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

Nous avons introduit un petit modèle de bruit pour obtenir plus de détails sur les données réelles. Pour produire des bords du Cloud arrondis, nous avons tronqué les pixels dans le nuanceur de pixels lorsque la valeur de rayon interpolée atteint un seuil pour ignorer les valeurs proches de zéro.

![Clouds Geometry](images/datascape-geometry-clouds-700px.jpg)

Dans la mesure où les clouds sont de géométrie solide, ils peuvent être rendus avant le terrain pour masquer les pixels de la carte onéreux en dessous pour améliorer davantage la fréquence d’images. Cette solution s’est correctement exécutée sur toutes les cartes graphiques de min-spec aux cartes graphiques haut de gamme, ainsi que sur HoloLens, en raison de l’approche de rendu géométrique solide.

## <a name="solid-particle-clouds"></a>Clouds particulaires solides

Nous avions maintenant une solution de sauvegarde qui produisait une représentation correcte de nos données Cloud, mais était un peu lackluster dans le facteur «wow» et n’indiquait pas le sentiment que nous souhaitions pour nos machines haut de gamme.

L’étape suivante consistait à créer les clouds en les représentant avec environ 100 000 particules pour produire un look plus organique et volumétrique.

Si les particules restent solides et sont triées avant l’arrière, nous pouvons toujours tirer parti de l’élimination de la mémoire tampon de profondeur des pixels situés derrière les particules rendues précédemment, réduisant ainsi le surdessin. En outre, avec une solution basée sur les particules, nous pouvons modifier la quantité de particules utilisée pour cibler un matériel différent. Toutefois, tous les pixels doivent toujours être testés de manière approfondie, ce qui entraîne une surcharge supplémentaire.

Tout d’abord, nous avons créé des positions de particule autour du point central de l’expérience au démarrage. Nous avons distribué les particules de manière plus dense à travers le centre et moins à distance. Nous avons pré-trié toutes les particules du centre vers l’arrière afin que les particules les plus proches s’affichent en premier.

Un nuanceur de calcul échantillonne la texture d’informations Cloud pour positionner chaque particule à une hauteur correcte et la colorier en fonction de la densité.

Nous avons utilisé *DrawProcedural* pour effectuer le rendu d’un quadruple par particule permettant aux données de particule de rester sur le GPU à tout moment.

Chaque particule contenait à la fois une hauteur et un rayon. La hauteur était basée sur les données Cloud échantillonnées à partir de la texture informations sur le Cloud, et le rayon était basé sur la distribution initiale où il serait calculé pour stocker la distance horizontale sur son voisin le plus proche. Les quadruples utilisent ces données pour s’orienter de manière à s’orienter de façon verticale, de sorte que lorsque les utilisateurs regardent les données horizontalement, la hauteur est indiquée et, lorsque les utilisateurs l’observent de haut en haut, la zone entre ses voisins est couverte.

![Forme de particule](images/particle-shape-700px.png)

**Code du nuanceur présentant la distribution:**

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

Étant donné que nous triant les particules de l’avant vers l’arrière et que nous avons toujours utilisé un nuanceur de style plein pour découper (pas mélanger) les pixels transparents, cette technique gère une quantité étonnamment importante de particules, ce qui évite les surcharges coûteuses, même sur les machines de faible consommation.

## <a name="transparent-particle-clouds"></a>Clouds particulaires transparents

Les particules solides offraient une bonne sensation organique à la forme des clouds, tout en nécessitant des choses pour vendre le fluffiness de clouds. Nous avons décidé d’essayer une solution personnalisée pour les cartes graphiques haut de gamme où nous pouvons introduire la transparence.

Pour ce faire, nous avons simplement basculé l’ordre de tri initial des particules et modifié le nuanceur pour utiliser les textures alpha.

![Clouds fluffy](images/fluffy-clouds-700px.jpg)

Il s’est avéré bien, mais il s’est avéré trop lourd pour les machines les plus difficiles, car cela entraînerait le rendu de chaque pixel à l’écran des centaines de fois!

## <a name="render-off-screen-with-lower-resolution"></a>Rendre hors écran avec une résolution inférieure

Pour réduire le nombre de pixels rendus par les Clouds, nous avons commencé à les afficher dans une mémoire tampon de résolution de trimestre (par rapport à l’écran) et à étirer le résultat final sur l’écran une fois que toutes les particules ont été dessinées. Cela nous a donné environ une accélération de 4 fois, mais il a été fourni avec quelques avertissements.

**Code pour le rendu hors écran:**

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

Tout d’abord, lors du rendu dans une mémoire tampon hors écran, nous avons perdu toutes les informations de profondeur de notre scène principale, ce qui a pour résultat des particules sous-jacentes au rendu des montagnes en plus de la montagne.

Deuxièmement, l’étirement de la mémoire tampon a également introduit des artefacts sur les bords de nos Clouds où le changement de résolution était perceptible. Les deux sections suivantes expliquent comment nous avons résolu ces problèmes.

## <a name="particle-depth-buffer"></a>Mémoire tampon de profondeur des particules

Pour faire en sorte que les particules coexistent avec la géométrie du monde où une montagne ou un objet peut couvrir des particules en arrière-plan, nous avons rempli la mémoire tampon hors écran avec une mémoire tampon de profondeur contenant la géométrie de la scène principale. Pour produire une telle mémoire tampon de profondeur, nous avons créé une deuxième caméra, en rendant uniquement la géométrie solide et la profondeur de la scène.

Nous avons ensuite utilisé la nouvelle texture dans le nuanceur de pixels des clouds pour occultait pixels. Nous avons utilisé la même texture pour calculer la distance à la géométrie derrière un pixel du Cloud. En utilisant cette distance et en l’appliquant à l’alpha du pixel, nous avons à présent vu l’effet des clouds à mesure qu’ils se rapprochent du terrain, éliminant les coupes difficiles où les particules et le terrain se rencontrent.

![Clouds mélangés dans le terrain](images/clouds-blended-to-terrain-700px.jpg)

## <a name="sharpening-the-edges"></a>Amélioration de la netteté des bords

Les clouds étirés recherchaient presque identiques aux clouds de taille normale au centre des particules ou à l’endroit où ils se chevauchaient, mais affichaient certains artefacts sur les bords du Cloud. Sinon, les bords nets apparaîtraient flous et les effets d’alias ont été introduits lors du déplacement de l’appareil photo.

Nous avons résolu cela en exécutant un nuanceur simple sur la mémoire tampon hors écran pour déterminer où des changements importants ont été apportés (1). Nous plaçons les pixels avec des modifications importantes dans une nouvelle mémoire tampon de stencil (2). Nous avons ensuite utilisé la mémoire tampon stencil pour masquer ces zones à contraste élevé lors de l’application de la mémoire tampon hors écran à l’écran, ce qui entraîne des trous dans et autour des Clouds (3).

Nous avons ensuite rendu toutes les particules en mode plein écran, mais cette fois, il a utilisé la mémoire tampon stencil pour masquer tout ce qui est à l’exception des bords, ce qui entraîne un ensemble minimal de pixels horodatés (4). Étant donné que la mémoire tampon de commande a déjà été créée pour les particules, nous avons simplement dû la restituer à nouveau à la nouvelle caméra.

![Progression du rendu des bords du Cloud](images/cloud-steps-1-4-700px.jpg)

Le résultat final était une arête aiguë avec des sections Centre bon marché des clouds.

Bien que cela soit beaucoup plus rapide que le rendu de toutes les particules en plein écran, il y a toujours un coût associé au test d’un pixel par rapport à la mémoire tampon des stencils, ce qui entraîne un coût considérable.

## <a name="culling-particles"></a>Élimination des particules

Pour notre effet vent, nous avons généré des bandes de triangle longues dans un nuanceur de calcul, créant de nombreux WISPs du vent dans le monde. Alors que l’effet vent n’était pas lourd sur le taux de remplissage en raison des bandes de pelures générées, il produisait plusieurs centaines de milliers de vertex, ce qui entraînait une charge importante pour le nuanceur de sommets.

Nous avons introduit des tampons d’ajout sur le nuanceur de calcul pour alimenter un sous-ensemble des bandes à dessiner. Avec une vue simple frustum l’élimination de la logique dans le nuanceur de calcul, nous pourrions déterminer si une bande était en dehors de la vue caméra et l’empêcher d’être ajoutée à la mémoire tampon d’envoi (push). Cela a considérablement réduit la quantité de bandes, ce qui libère des cycles nécessaires sur le GPU.

**Code illustrant une mémoire tampon d’ajout:**

*Nuanceur de calcul:*

```
AppendStructuredBuffer<int> culledParticleIdx;
 
if (show)
    culledParticleIdx.Append(id.x);
```

*C#code*

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

Nous avons essayé d’utiliser la même technique sur les particules du Cloud, où nous les sélectionnons dans le nuanceur de calcul et transmettons uniquement les particules visibles pour être rendues. En fait, cette technique ne nous a pas permis de gagner beaucoup de temps sur le GPU puisque le plus grand goulot d’étranglement était le nombre de pixels rendu sur l’écran, et non le coût du calcul des vertex.

L’autre problème avec cette technique était que la mémoire tampon d’ajout était remplie dans un ordre aléatoire en raison de sa nature parallélisée du calcul des particules, provoquant la non-tri des particules triées, entraînant le scintillement des particules du Cloud.

Il existe des techniques permettant de trier la mémoire tampon d’envoi, mais le gain de performances limité que nous avons rencontré pour l’élimination des particules serait probablement compensé par un tri supplémentaire, donc nous avons décidé de ne pas poursuivre cette optimisation.

## <a name="adaptive-rendering"></a>Rendu adaptatif

Pour garantir une cadence constante sur une application avec des conditions de rendu variables telles qu’une vue en clair et une vue claire, nous avons introduit un rendu adaptatif pour notre application.

La première étape du rendu adaptatif consiste à mesurer le GPU. Nous l’avons fait en insérant du code personnalisé dans la mémoire tampon de commande GPU au début et à la fin d’un frame rendu, en capturant à la fois l’heure de gauche et de droite de l’écran.

En mesurant le temps passé à effectuer le rendu et en le comparant au taux d’actualisation souhaité, nous avons un sens de la fermeture des frames.

Lorsque vous approchez de la suppression des frames, nous adaptons notre rendu pour le rendre plus rapide. Une méthode simple d’adaptation consiste à modifier la taille de la fenêtre d’affichage de l’écran, ce qui nécessite moins de pixels pour être rendu.

À l’aide de *UnityEngine. XR. XRSettings. renderViewportScale* le système réduit la fenêtre d’affichage ciblée et étire automatiquement le résultat en fonction de l’écran. Une petite modification de l’échelle est à peine perceptible sur la géométrie universelle et un facteur d’échelle de 0,7 nécessite la moitié du nombre de pixels à afficher.

![échelle de 70%, moitié des pixels](images/datascape-scaling-700px.jpg)

Quand nous détectons que nous nous apprêtons à supprimer des trames, nous réduisons l’échelle d’un nombre fixe, puis nous les augmentons quand nous exécutons à nouveau rapidement.

Bien que nous ayons décidé de la technique Cloud à utiliser en fonction des capacités graphiques du matériel au démarrage, il est possible de la baser sur les données de la mesure GPU pour empêcher le système de se maintenir à une résolution faible pendant une longue période, mais ce n’est pas un temps  pour explorer dans datascape.

## <a name="final-thoughts"></a>Réflexions finales

Le ciblage d’une variété de matériel est difficile et nécessite une certaine planification.

Nous vous recommandons de commencer à cibler des machines à faible consommation pour vous familiariser avec l’espace à problème et de développer une solution de sauvegarde qui s’exécutera sur tous vos ordinateurs. Concevez votre solution avec le taux de remplissage à l’esprit, car les pixels seront vos ressources les plus précieuses. Cible solide Geometry sur la transparence.

Avec une solution de sauvegarde, vous pouvez commencer à superposer des couches plus complexes pour les machines de haut niveau ou peut-être simplement améliorer la résolution de votre solution de sauvegarde.

Conception pour les pires scénarios et peut-être envisager l’utilisation d’un rendu adaptatif pour des situations lourdes.

## <a name="about-the-authors"></a>À propos des auteurs

<table style="border:0">
<tr>
<td style="border:0" width="60px"><img alt="Picture of Robert Ferrese" width="60" height="60" src="images/robert-ferrese-60px.jpg"></td>
<td style="border:0"><b>Robert Ferrese</b><br>Ingénieur logiciel@Microsoft</td>
</tr>
<tr>
<td style="border:0" width="60px"><img alt="Picture of Dan Andersson" width="60" height="60" src="images/dan-andersson-60px.jpg"></td>
<td style="border:0"><b>Dan Andersson</b><br>Ingénieur logiciel@Microsoft</td>
</tr>
</table>


## <a name="see-also"></a>Voir aussi
* [Comprendre les performances de la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Recommandations en matière de performances pour Unity](performance-recommendations-for-unity.md)

 
