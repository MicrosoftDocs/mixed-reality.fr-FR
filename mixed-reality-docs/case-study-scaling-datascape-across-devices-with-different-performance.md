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
# <a name="case-study---scaling-datascape-across-devices-with-different-performance"></a>Étude de cas - Datascape de mise à l’échelle sur les appareils avec des performances différentes

Datascape est une application Windows Mixed Reality développée en interne chez Microsoft où nous nous sommes concentrés sur l’affichage des données météorologiques par-dessus les données de terrain. L’application explore les insights uniques utilisateurs arrivent à partir de la découverte des données dans la réalité mixte en mettant l’utilisateur avec une visualisation de données HOLOGRAPHIQUE.

Pour Datascape que nous souhaitons cibler diverses plateformes avec des fonctionnalités matérielles différentes allant de Microsoft HoloLens à des casques IMMERSIFS réalité mixte Windows et des PC de faible puissance sur les toutes dernières PC avec processeur graphique haut de gamme. Le défi principal a été rendu notre scène en quelques visuellement agréables sur les appareils avec des capacités graphiques entièrement différent lors de l’exécution à une fréquence d’images élevé.

Cette étude de cas guidera dans le processus et les techniques utilisées pour créer certaines de nos systèmes GPU gourmandes en plus, qui décrivent les problèmes que nous avons rencontré et comment nous les avons surmontées.

## <a name="transparency-and-overdraw"></a>La transparence et superposition

Notre connaissait rendu principal traité la transparence, étant donné que la transparence peut s’avérer coûteuse sur un GPU.

Géométrie solide peut être rendue avant en arrière pendant l’écriture sur la mémoire tampon de profondeur, l’arrêt de toute futures pixels situés derrière ce pixel d’ignorer. Cela empêche les pixels masqués à partir de l’exécution du nuanceur de pixels, ce qui accélère considérablement le processus. Si la géométrie est triée de façon optimale, chaque pixel dans l’écran sera dessiné qu’une seule fois.

Géométrie transparent doit être triée arrière vers l’avant et s’appuie sur la sortie du nuanceur de pixels pour le pixel actuel dans l’écran de fusion. Cela peut entraîner dans chaque pixel dans l’écran dessinée dans plusieurs fois par frame, également appelée superposition.

Pour HoloLens et PC grand public, l’écran peut uniquement être renseigné un certain nombre de fois, ce qui rend transparent rendu problématique.

## <a name="introduction-to-datascape-scene-components"></a>Présentation des composants de scène Datascape de

Il nous fallait trois principaux composants notre scène ; **l’interface utilisateur, le mappage**, et **la météo**. Nous savions dès le début que les effets de la météo nécessiterait tout le temps GPU deviendrait, donc nous avons conçu l’interface utilisateur et un terrain d’une manière qui réduirait les superpositions.

Nous avons remanié l’interface utilisateur plusieurs fois afin de réduire la quantité de superposition il produirait. Nous nous sommes trompés sur le côté de géométrie plus complexe au lieu de superposition transparent art, superposées des composants tels que lumineux de vues d’ensemble de boutons et de la carte.

Pour le mappage, nous avons utilisé un nuanceur personnalisé qui serait éliminer des fonctionnalités de Unity standard telles que les ombres et l’éclairage complex, en les remplaçant par un modèle d’éclairage simple sun unique et un calcul personnalisé brouillard. Cela produit un nuanceur de pixels simple et libérer des cycles GPU.

Nous avons réussi à obtenir l’interface utilisateur et la carte pour le rendu au budget où nous n’avait pas besoin leurs éventuelles modifications selon le matériel ; Toutefois, la visualisation de la météo, en particulier le rendu cloud, s’est avéré pour être plus complexe !

## <a name="background-on-cloud-data"></a>En arrière-plan sur des données cloud

Nos données de cloud a été téléchargées à partir de serveurs de NOAA (http://nomads.ncep.noaa.gov/) et est fourni pour nous dans trois couches 2D distinctes, chacune avec la hauteur de haut et bas du cloud, ainsi que la densité du cloud pour chaque cellule de la grille. Les données a été traitées dans une texture d’informations cloud où chaque composant a été stocké dans le composant rouge, vert et bleu de la texture pour pouvoir accéder facilement sur le GPU.

## <a name="geometry-clouds"></a>Clouds de géométrie

Pour vous assurer que nos ordinateurs de faible puissance pourrait rendre nos clouds que nous avons décidé de commencer par une approche par géométrie solide pour réduire la superposition.

Tout d’abord, nous avons essayé production clouds en générant une maille pleine relief pour chaque couche à l’aide de rayon de la texture d’informations cloud par vertex pour générer la forme. Nous avons utilisé un nuanceur de géométrie pour produire les sommets à la fois en haut et bas du cloud générant des formes de cloud solide. Nous avons utilisé la valeur de densité de la texture pour colorer le cloud avec une couleur sombre pour les clouds plus denses.

**Nuanceur pour la création de vertex :**

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

Nous avons introduit un modèle petit bruit pour obtenir plus de détails sur les données réelles. Pour produire les bords arrondis cloud, nous découpé les pixels dans le nuanceur de pixels lorsque la valeur de rayon interpolée atteint un seuil afin d’ignorer les valeurs proches de zéro.

![Clouds de géométrie](images/datascape-geometry-clouds-700px.jpg)

Étant donné que les clouds sont géométrie solide, ils peuvent être rendus avant le terrain pour masquer n’importe quel pixels carte coûteux en dessous pour améliorer encore les taux de trames. Cette solution s’est exécutée correctement sur toutes les cartes graphiques à partir de la spécification de min cartes graphiques haut de gamme, ainsi que sur HoloLens, en raison de l’approche de rendu de géométrie solide.

## <a name="solid-particle-clouds"></a>Clouds de particules solides

Maintenant, nous avions une solution de sauvegarde qui produit une bonne représentation de nos données cloud, mais a été un peu reluisantes dans le facteur de « wow » et s’est pas transmettre le volumétriques sont convaincus que nous voulions pour nos ordinateurs haut de gamme.

Notre prochaine étape créait des nuages en représentant les avec environ 100 000 particules pour produire une apparence plus naturelle et volumétrique.

Si particules pleine et trier l’avant vers l’arrière, nous pouvons bénéficier élimination de mémoire tampon de profondeur des pixels derrière les particules précédemment rendus, ce qui réduit les superpositions. En outre, avec une solution basée sur les particules, nous pouvons modifier la quantité de particules utilisé sur un autre matériel de cible. Toutefois, tous les pixels devront être testé de profondeur, ce qui aboutit à une surcharge supplémentaire.

Tout d’abord, nous avons créé des positions de particules autour du point central de l’expérience au démarrage. Nous avons distribué les particules de façon plus compacte autour du centre et moins c’est le cas dans la distance. Nous prétriées toutes les particules à partir du centre vers l’arrière afin que tout d’abord affichant les particules le plus proche.

Un nuanceur de calcul serait exemples de la texture d’informations cloud afin de positionner chaque particule à une hauteur et une couleur que selon la densité.

Nous avons utilisé *DrawProcedural* permettant de restituer une quadruple par particule autorisant les données de la particule de rester sur le GPU à tout moment.

Chaque particule contenait une hauteur et un rayon. La hauteur était basée sur les données de cloud échantillonnées à partir de la texture info de cloud, et le rayon était basé sur la distribution initiale où elle est calculée pour stocker la distance horizontale et son voisin le plus proche. Les quadrilatères voudraient utiliser ces données pour orienter lui-même inclinées par la hauteur afin que lorsque les utilisateurs regardez horizontalement, la hauteur sont affichée, et lorsque les utilisateurs examiné il haut en bas, la zone entre ses voisins est couverts.

![Forme de particules](images/particle-shape-700px.png)

**Code de nuanceur montrant la distribution :**

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

Dans la mesure où nous trier le particules avant vers l’arrière et nous avons toujours utilisé un nuanceur de style continu sur les pixels transparents clip (pas blend), cette technique permet de gérer une quantité étonnante de particules, évitant les coûteux dessin excessive même sur les machines de faible puissance.

## <a name="transparent-particle-clouds"></a>Clouds de particules transparent

Les particules solides fourni une idée organique à la forme des clouds, mais encore besoin de quelque chose de vendre le fluffiness des clouds. Nous avons décidé d’essayer une solution personnalisée pour les cartes graphiques haut de gamme où nous pouvons introduire la transparence.

Pour cela nous simplement modifiais l’ordre de tri initial des particules et modifié le nuanceur pour utiliser la valeur alpha de textures.

![Fluffy clouds](images/fluffy-clouds-700px.jpg)

Il ressemblait excellent, mais s’est avéré pour être trop lourde pour même les ordinateurs les plus ardues, car elle entraînerait le rendu de chaque pixel dans l’écran des centaines de fois !

## <a name="render-off-screen-with-lower-resolution"></a>Rendu hors écran avec une résolution inférieure

Pour réduire le nombre de pixels affichés par les clouds, nous avons commencé à leur rendu dans la mémoire tampon de résolution d’un trimestre (comparé à l’écran) et étirer le résultat final des sauvegardes sur l’écran après que toutes les particules avaient été dessinés. Cela nous a donné à peu près une accélération 4 x, mais fourni avec quelques inconvénients.

**Code pour le rendu hors écran :**

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

Tout d’abord, lors du rendu dans une mémoire tampon hors écran, nous avons perdu toutes les informations de profondeur à partir de notre scène principale, ce qui entraîne des particules derrière montagnes rendu par-dessus le mountain.

En second lieu, étirement de la mémoire tampon a également introduit les artefacts sur les bords de notre clouds où la modification de la résolution a été notable. Les deux sections suivantes parler de la façon dont nous avons résolu ces problèmes.

## <a name="particle-depth-buffer"></a>Mémoire tampon de profondeur de particules

Pour rendre les particules coexiste avec la géométrie de l’environnement où un mountain ou un objet peut couvrir des particules derrière lui, nous l’avons rempli la mémoire tampon hors écran avec une mémoire tampon de profondeur contenant la géométrie de la scène principale. Pour produire cette mémoire tampon de profondeur, nous avons créé une deuxième caméra, rendu uniquement la géométrie solide et la profondeur de la scène.

Ensuite, nous avons utilisé la nouvelle texture dans le nuanceur de pixels des clouds pour occlude pixels. Nous avons utilisé la même texture pour calculer la distance à la géométrie derrière un pixel de cloud. En utilisant cette distance et appliquer à la valeur alpha du pixel, nous avions maintenant l’effet des clouds fondu lorsqu’ils ont proche de terrain, en supprimant les morceaux dur intersection des particules et le terrain.

![Clouds fusionnés dans un terrain](images/clouds-blended-to-terrain-700px.jpg)

## <a name="sharpening-the-edges"></a>La netteté

Les clouds des étiré ressemblait presque identiques pour les clouds de taille normale au centre des particules ou où ils chevauchent, mais vous a montré certains artefacts sur les bords du cloud. Sinon des bords tranchants apparaîtrait floues et effets d’alias ont été introduites lors de l’appareil photo est déplacé.

Nous avons résolu le problème en exécutant un nuanceur simple sur la mémoire tampon hors écran pour localiser les grands changements à l’inverse (1). Nous mettons les pixels avec de grands changements dans un nouveau tampon stencil (2). Nous avons ensuite utilisé la mémoire tampon stencil pour masquer les ces zones de contraste élevé lors de l’application de la mémoire tampon hors écran à l’écran, ce qui entraîne des failles dans et autour de nuages (3).

Nous avons ensuite toutes les particules une nouvelle fois restitué en mode plein écran, mais cette fois utilisé la mémoire tampon stencil pour masquer tous les éléments, mais les bords, ce qui entraîne un ensemble minimal de pixels utilisé (4). Dans la mesure où le tampon de commande a déjà été créé pour les particules, nous avions simplement pour la rendre à nouveau vers le nouvel appareil photo.

![Progression du rendu des bords du cloud](images/cloud-steps-1-4-700px.jpg)

Le résultat final a été bords tranchants avec des sections center peu onéreuse des clouds.

Cette opération est beaucoup plus rapide que le rendu toutes les particules en plein écran, il est toujours un coût associé à un pixel par rapport à la mémoire tampon stencil, de test pour des quantités massives de superposition toujours fournie avec un coût.

## <a name="culling-particles"></a>Élimination de particules

Pour notre effet du vent, que nous avons générée durée pendant laquelle les bandes de triangles dans un nuanceur de calcul, création de nombreux offraient de vent dans le monde. L’effet du vent n’était pas une charge importante pour les taux de remplissage en raison de bandes réduits généré, il produit plusieurs centaines de milliers de vertex, ce qui entraîne une charge importante pour le nuanceur de sommets.

Nous avons introduit ajouter les mémoires tampons sur le nuanceur de calcul pour alimenter un sous-ensemble de la diagonale du vent à dessiner. Avec une vue simple frustum élimination logique du nuanceur de calcul, nous aurions pu déterminer si une bande était en dehors de la vue de la caméra et empêcher l’ajout à la mémoire tampon push. Cela réduit la quantité de bandes considérablement, libérant des cycles nécessaires sur le GPU.

**Code illustrant une mémoire tampon d’ajouter :**

*Nuanceur de calcul :*

```
AppendStructuredBuffer<int> culledParticleIdx;
 
if (show)
    culledParticleIdx.Append(id.x);
```

*C#code :*

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

Nous avons essayé d’à l’aide de la même technique sur les particules de cloud, où nous sélectionnons les sur le nuanceur de calcul et transmettre uniquement les particules visibles doit être restitué. Cette technique réellement n’avez pas enregistré nous une grande partie sur le GPU dans la mesure où le plus gros goulet d’étranglement a été les pixels de montant affichées sur l’écran et pas le coût de calcul de vertex.

L’autre problème avec cette technique était que la mémoire tampon append rempli dans un ordre aléatoire en raison de sa nature parallélisée de l’informatique les particules, à l’origine les particules triés soit non triée, ce qui entraîne des particules cloud scintillements sont supprimés.

Il existe des techniques pour trier la mémoire tampon push, mais la quantité limitée de gain de performances que provenant de l’élimination de particules serait probablement être décalée avec un tri supplémentaire, nous avons donc décidé de ne pas poursuivre cette optimisation.

## <a name="adaptive-rendering"></a>Rendu adaptatif

Pour garantir une fréquence d’images stable sur une application avec diverses conditions comme un temps nuageux vs de rendu un aperçu clair, nous avons introduit rendu adaptatif à notre application.

La première étape de rendu adaptatif consiste à mesurer le GPU. Nous l’avons fait cela en insérant un code personnalisé dans le tampon de commande GPU au début et à la fin d’une image rendue, capture les deux, gauche et à droite du temps d’écran des yeux.

En mesurant le temps passé de rendu et en la comparant à notre souhaité-fréquence d’actualisation que nous avons une idée de comment fermer nous à la perte de trames.

Lorsque proche de la suppression d’images, nous adapter notre rendu pour le rendre plus rapidement. Un moyen simple d’adaptation change la taille de fenêtre d’affichage de l’écran, nécessitant moins pixels pour obtenir le rendu.

À l’aide de *UnityEngine.XR.XRSettings.renderViewportScale* le système réduit la fenêtre d’affichage ciblé et étire automatiquement le résultat au ajuster l’écran. Une petite modification de la mise à l’échelle est à peine perceptible sur la géométrie de l’environnement, et un facteur d’échelle de 0,7 nécessite la moitié de la quantité de pixels doit être restitué.

![échelle de 70 %, la moitié du nombre de pixels](images/datascape-scaling-700px.jpg)

Lorsque nous détectons que nous sommes sur le point de supprimer des trames nous réduire l’échelle par un nombre fixe et augmenter refaites-le lorsque nous exécutons assez rapidement à nouveau.

Bien que nous avons décidé quelle technique cloud à utiliser selon graphics capacités du matériel au démarrage, il est possible en vous basant sur les données à partir de la mesure du GPU pour empêcher le système de rester au premier plan basse résolution pour un certain temps, mais il s’agit d’un élément sans avoir à temps  pour Explorer les Datascape.

## <a name="final-thoughts"></a>Réflexions finales

Ciblage d’une variété de matériel est complexe et requiert une planification.

Nous vous recommandons de commencer ciblant les ordinateurs de faible puissance pour vous familiariser avec l’espace de problème et de développer une solution de sauvegarde qui s’exécutera sur toutes vos machines. Concevoir votre solution avec des taux de remplissage à l’esprit, dans la mesure où les pixels sera votre ressource plus précieux. Cibler une géométrie solide sur la transparence.

Avec une solution de sauvegarde, vous pouvez ensuite démarrer superposition dans plus de complexité pour les machines de haut de gamme ou peut-être simplement améliorer la résolution de votre solution de sauvegarde.

Concevoir pour le pire des cas et peut-être envisager à l’aide de rendu adaptatif pour des situations lourdes.

## <a name="about-the-authors"></a>À propos des auteurs

<table style="border:0">
<tr>
<td style="border:0" width="60px"><img alt="Picture of Robert Ferrese" width="60" height="60" src="images/robert-ferrese-60px.jpg"></td>
<td style="border:0"><b>Robert Ferrese</b><br>Ingénieur logiciel @Microsoft</td>
</tr>
<tr>
<td style="border:0" width="60px"><img alt="Picture of Dan Andersson" width="60" height="60" src="images/dan-andersson-60px.jpg"></td>
<td style="border:0"><b>Dan Andersson</b><br>Ingénieur logiciel @Microsoft</td>
</tr>
</table>


## <a name="see-also"></a>Voir aussi
* [Comprendre les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Recommandations relatives aux performances pour Unity](performance-recommendations-for-unity.md)

 
