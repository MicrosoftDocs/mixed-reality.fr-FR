---
title: 'Étude de cas: création d’un Galaxy en réalité mixte'
description: Avant la sortie de Microsoft HoloLens, nous avons demandé à notre communauté de développeurs quel type d’application il souhaite voir une build d’équipe interne expérimentée pour le nouvel appareil. Plus de 5000 idées ont été partagées et, après une interrogation Twitter de 24 heures, le gagnant était une idée appelée «Galaxy Explorer».
author: KarimLUCCIN
ms.author: kaluccin
ms.date: 03/21/2018
ms.topic: article
keywords: Explorateur Galaxy, HoloLens, Windows Mixed Reality, partager votre idée, étude de cas
ms.openlocfilehash: a478eaa35144a8ee0fbeaeb43cec4b9f901890ab
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63523745"
---
# <a name="case-study---creating-a-galaxy-in-mixed-reality"></a>Étude de cas: création d’un Galaxy en réalité mixte

Avant la sortie de Microsoft HoloLens, nous avons demandé à notre communauté de développeurs quel type d’application il souhaite voir une build d’équipe interne expérimentée pour le nouvel appareil. Plus de 5000 idées ont été partagées et, après une interrogation Twitter de 24 heures, le gagnant était une idée appelée l' [Explorateur Galaxy](galaxy-explorer.md).

Andy Zibits, responsable artistique sur le projet et karim Luccin, l’ingénieur graphique de l’équipe, évoque les efforts de collaboration entre l’art et l’ingénierie qui ont conduit à la création d’une représentation interactive et précise de la manière lactée de Galaxy dans l’Explorateur Galaxy.

## <a name="the-tech"></a>Le Tech

[Notre équipe](galaxy-explorer.md#meet-the-team) , composée de deux concepteurs, de trois développeurs, de quatre artistes, d’un producteur et d’un testeur, avait six semaines pour créer une application entièrement fonctionnelle qui permettrait aux utilisateurs d’en savoir plus sur l’immense et la beauté de notre méthode lactée Galaxy.

Nous souhaitons tirer pleinement parti de la capacité de HoloLens à restituer les objets 3D directement dans votre espace de vie. nous avons donc décidé de créer un Galaxy réaliste où les gens seraient en mesure d’effectuer un zoom avant et de voir les étoiles individuelles, chacune sur leurs propres trajectoires .

Au cours de la première semaine de développement, nous avons trouvé quelques objectifs pour notre représentation de la manière lactée de Galaxy: Cela devait avoir un niveau de profondeur, de mouvement et de sensation, avec des étoiles qui vous aideront à créer la forme du Galaxy.

Le problème lié à la création d’un Galaxy animé qui avait des milliards d’étoiles était que le nombre important d’éléments uniques nécessitant une mise à jour serait trop grand par frame pour que HoloLens s’anime à l’aide de l’UC. Notre solution impliquait une combinaison complexe d’art et de science.

## <a name="behind-the-scenes"></a>En arrière-plan

Pour permettre aux utilisateurs d’explorer des étoiles individuelles, notre première étape consistait à déterminer le nombre de particules pouvant être rendues simultanément.

### <a name="rendering-particles"></a>Rendu des particules

Les processeurs actuels sont idéaux pour traiter des tâches en série et jusqu’à quelques tâches parallèles à la fois (selon le nombre de cœurs), mais les GPU sont beaucoup plus efficaces pour traiter des milliers d’opérations en parallèle. Toutefois, étant donné qu’ils ne partagent généralement pas la même mémoire que le processeur, l’échange de données entre l’UC < > GPU peut rapidement devenir un goulot d’étranglement. Notre solution consistait à créer un Galaxy sur le GPU et il devait être entièrement actif sur le GPU.

Nous avons commencé des tests de stress avec des milliers de particules de points dans différents modèles. Cela nous a permis d’obtenir le Galaxy sur HoloLens pour voir ce qui a fonctionné et ce qui ne l’a pas fait.

### <a name="creating-the-position-of-the-stars"></a>Création de la position des étoiles

L’un de nos membres de l’équipe a C# déjà écrit le code qui générerait des étoiles à leur position initiale. Les étoiles se trouvent sur une ellipse et leur position peut être décrite par (**curveOffset**, **ellipseSize**, **Elevation**) où **curveOffset** est l’angle de l’étoile le long de l’ellipse, **ellipseSize** est la dimension de l’ellipse le long de X et de Z, et élever l’altitude appropriée de l’étoile au sein de Galaxy. Par conséquent, nous pouvons créer une mémoire tampon ([ComputeBuffer d’Unity](http://docs.unity3d.com/ScriptReference/ComputeBuffer.html)) qui serait initialisée avec chaque attribut d’étoile et l’envoyer sur le GPU là où il résiderait pour le reste de l’expérience. Pour dessiner ce tampon, nous utilisons [l’DrawProcedural d’Unity](http://docs.unity3d.com/ScriptReference/Graphics.DrawProcedural.html) qui permet d’exécuter un nuanceur (code sur un GPU) sur un ensemble arbitraire de points sans avoir de maillage réel représentant le Galaxy:

**POURCENTAGE**




```
GraphicsDrawProcedural(MeshTopology.Points, starCount, 1);
```

**VIDÉO**




```
v2g vert (uint index : SV_VertexID)
{

 // _Stars is the buffer we created that contains the initial state of the system
 StarDescriptor star = _Stars[index];
 …

}
```

Nous avons commencé avec des modèles circulaires bruts avec des milliers de particules. Nous avons ainsi fourni la preuve que nous avions besoin de gérer de nombreuses particules et de les exécuter à des vitesses performantes, mais nous n’avions pas respecté la forme globale de Galaxy. Pour améliorer la forme, nous avons essayé divers modèles et systèmes de particules avec rotation. Celles-ci ont été initialement prometteuses, car le nombre de particules et de performances est resté cohérent, mais la forme est tombée près du centre et les étoiles ont été émises vers l’extérieur, ce qui n’était pas réaliste. Nous avions besoin d’une émission qui nous permettrait de manipuler le temps et de faire en sorte que les particules se déplacent de façon réaliste, en effectuant une boucle plus proche du centre du Galaxy.

![Nous avons essayé différents modèles et systèmes de particules qui ont pivoté, comme ceux-ci.](images/galaxy-patterns-500px.png)

Nous avons essayé différents modèles et systèmes de particules qui ont pivoté, comme ceux-ci.

Notre équipe a fait des recherches sur la façon dont galaxies fonctionne et nous avons créé un système de particule personnalisé spécifiquement pour la galaxie afin que nous puissions déplacer les particules sur les ellipses en fonction de la «[théorie des vagues de densité](https://en.wikipedia.org/wiki/Density_wave_theory)», qui theorizes que les bras d’un Galaxy sont des zones de densité plus élevée, mais en flux constant, comme un bourrage de trafic. Il semble stable et solide, mais les étoiles sont en fait en déplacement et en provenance des bras lorsqu’ils se déplacent sur leurs ellipses respectives. Dans notre système, les particules n’existent jamais sur le processeur: nous générons les cartes et les orientons toutes sur le GPU, de sorte que le système entier est simplement un état initial + Time. Elle a progressé comme suit:

![Progression du système de particules avec rendu GPU](images/spiral-galaxy-arms-500px.jpg)

Progression du système de particules avec rendu GPU


Une fois que suffisamment de ellipses ont été ajoutées et sont définies pour pivoter, le galaxies a commencé à former des «bras» où le mouvement des étoiles converge. L’espacement des étoiles sur chaque tracé elliptique a été donné à caractère aléatoire, et chaque étoile a ajouté un peu de caractère aléatoire positionnel. Cela a créé une distribution d’aspect plus naturelle du mouvement en étoile et de la forme ARM. Enfin, nous avons ajouté la capacité de piloter la couleur en fonction de la distance par rapport au centre.

### <a name="creating-the-motion-of-the-stars"></a>Création du mouvement des étoiles

Pour animer le mouvement de l’étoile générale, nous avons besoin d’ajouter un angle constant pour chaque image et de faire en sorte que les étoiles se déplacent le long de leurs ellipses à une vélocité radiale constante. Il s’agit de la raison principale de l’utilisation de **curveOffset**. Cela n’est pas techniquement correct, car les étoiles se déplacent plus rapidement sur les longs côtés des ellipses, mais le mouvement général est parfait.

![Les étoiles se déplacent plus rapidement sur l’arc long, plus lentement sur les bords.](images/ellipse-movement.jpg)

Les étoiles se déplacent plus rapidement sur l’arc long, plus lentement sur les bords.


Avec cela, chaque étoile est entièrement décrite par (**curveOffset**, **ellipseSize**, **Elevation**, **Age**) où **Age** est une accumulation du temps total qui s’est écoulé depuis le chargement de la scène.




```
float3 ComputeStarPosition(StarDescriptor star)
{

  float curveOffset = star.curveOffset + Age;
  
  // this will be coded as a “sincos” on the hardware which will compute both sides
  float x = cos(curveOffset) * star.xRadii;
  float z = sin(curveOffset) * star.zRadii;
   
  return float3(x, star.elevation, z);
  
}
```

Cela nous a permis de générer des dizaines de milliers d’étoiles une fois au début de l’application, puis d’animer un ensemble unique d’étoiles le long des courbes établies. Dans la mesure où tout se trouve sur le GPU, le système peut animer toutes les étoiles en parallèle sans coût pour le processeur.

![Voici à quoi elle ressemble lors du dessin de Quad White.](images/drawing-white-quads-300px.jpg)

Voici à quoi elle ressemble lors du dessin de Quad White.



Pour que chaque quadruple fasse face à l’appareil photo, nous avons utilisé un nuanceur Geometry pour transformer chaque position d’étoile en rectangle 2D sur l’écran qui contiendra notre texture en étoile.

![Losanges au lieu de quads.](images/drawing-white-quads-300px.jpg)

Losanges au lieu de quads.


Étant donné que nous voulons limiter le surdessin (nombre de fois où un pixel sera traité) autant que possible, nous avons fait tourner nos quatre cœurs afin qu’ils aient moins de chevauchement.

### <a name="adding-clouds"></a>Ajout de clouds

Il existe de nombreuses façons d’obtenir une sensation volumétrique avec des particules, depuis le défilé de rayons à l’intérieur d’un volume jusqu’au dessin du plus grand nombre de particules possible pour simuler un Cloud. Le défilé de rayon en temps réel était trop onéreux et difficile à créer. nous avons donc essayé de créer un système imposteur à l’aide d’une méthode de rendu des forêts dans les jeux, avec un grand nombre d’images 2D d’arbres dirigés vers l’appareil photo. Lorsque nous faisons cela dans un jeu, nous pouvons avoir des textures d’arborescences rendues à partir d’une caméra qui pivote, enregistrer toutes ces images et, au moment de l’exécution pour chaque carte de tableau blanc, sélectionner l’image qui correspond à la direction de la vue. Cela ne fonctionne pas aussi bien lorsque les images sont des hologrammes. La différence entre l’œil gauche et l’œil droit le rend, afin que nous ayons besoin d’une résolution plus élevée, sinon il semble simple, avec alias ou répétitif.

À la deuxième tentative, nous avons essayé d’avoir autant de particules que possible. Les meilleurs visuels ont été atteints quand nous avons dessiné des particules et les avons floues avant de les ajouter à la scène. Les problèmes typiques de cette approche étaient liés au nombre de particules que nous pourrions tirer en une seule fois et à la zone d’écran couverte tout en maintenant 60fps. Le flou de l’image résultante pour obtenir cette sensation du Cloud était généralement une opération très coûteuse.

![Sans texture, c’est ce à quoi ressemblerait les clouds avec 2% d’opacité.](images/clouds-without-texture-300px.jpg)

Sans texture, c’est ce à quoi ressemblerait les clouds avec 2% d’opacité.



L’addition et l’utilisation d’un grand nombre d’entre elles signifient que nous aurions plusieurs quatre cœurs l’un de l’autre, ce qui permet d’ombrager de façon répétée le même pixel. Au centre de l’Galaxy, le même pixel a des centaines de Quad-Top les uns des autres, ce qui a eu un coût énorme lorsque l’opération est effectuée en mode plein écran.

Le fait d’effectuer des clouds plein écran et d’essayer de les brouiller aurait été une mauvaise idée, donc nous avons décidé de laisser le matériel faire le travail pour nous.

### <a name="a-bit-of-context-first"></a>Un peu de contexte en premier

Lors de l’utilisation des textures dans un jeu de la taille de texture rarement correspond à la zone que nous souhaitons utiliser dans, mais nous pouvons utiliser différents types de filtrage pour obtenir la carte graphique pour interpoler la couleur que nous voulons des pixels de la texture de texture ([defiltragedeTexture<C3/>](https://msdn.microsoft.com/library/dn642451.aspx)). Le filtrage qui nous intéresse est le [Filtrage bilinéaire](https://msdn.microsoft.com/library/windows/desktop/bb172357.aspx) qui calcule la valeur de tout pixel à l’aide des 4 voisins les plus proches.

![Original avant le filtrage](images/texture-1.png)

![Résultat après le filtrage](images/texture-2.png)

À l’aide de cette propriété, nous voyons que chaque fois que nous essayons de dessiner une texture dans une zone deux fois plus grande, le résultat est flou.

Au lieu d’effectuer un rendu en plein écran et de perdre ces millisecondes précieuses, nous pourrions passer à une version minuscule de l’écran. Ensuite, en copiant cette texture et en l’étirant à un facteur de 2 plusieurs fois, nous revenons en mode plein écran tout en brouilleant le contenu dans le processus.

![x3 revient à une résolution complète.](images/galaxy-resolutions-300px.png)

x3 revient à une résolution complète.



Cela nous a permis d’obtenir la partie Cloud avec uniquement une fraction du coût d’origine. Au lieu d’ajouter des clouds à la résolution complète, nous ne dessinons que 1/64th des pixels et remontons la texture à la résolution complète.

![À gauche, avec une mise à l’échelle de 1/8 à la résolution complète; et Right, avec 3 mises à l’échelle à l’aide de la puissance 2.](images/stars-upscaled-300px.jpg)

À gauche, avec une mise à l’échelle de 1/8 à la résolution complète; et Right, avec 3 mises à l’échelle à l’aide de la puissance 2.


Notez que la tentative de passer de 1/64th de la taille à la taille maximale d’un point de vue serait complètement différente, car la carte graphique utiliserait toujours 4 pixels dans notre configuration pour colorer une zone plus grande et les artefacts commencent à apparaître.

Ensuite, si nous ajoutons des étoiles de résolution complète avec des cartes plus petites, nous obtenons l’intégralité de Galaxy:

![Résultat final du rendu Galaxy à l’aide des étoiles de résolution complète](images/full-galaxy-500px.png)

Une fois que nous étions sur la bonne voie avec la forme, nous avons ajouté une couche de Clouds, remplacé les points temporaires par ceux que nous avons peints dans Photoshop, et ajouté des couleurs supplémentaires. Le résultat était une façon lactée de Galaxy nos équipes d’art et d’ingénierie, à la fois en matière de qualité, et a répondu à nos objectifs de profondeur, de volume et de mouvement, le tout sans imposer le processeur.

![Notre dernière méthode de Galaxy en 3D.](images/final-galaxy-500px.jpg)

Notre dernière méthode de Galaxy en 3D.


### <a name="more-to-explore"></a>Plus d’informations à explorer

Nous avons ouvert le code de l’application Galaxy Explorer et nous l’avons rendu disponible sur [GitHub](https://github.com/Microsoft/GalaxyExplorer) pour que les développeurs s’appuient sur.

Vous souhaitez en savoir plus sur le processus de développement de l’Explorateur Galaxy? Consultez toutes les mises à jour précédentes du projet sur le [canal Microsoft HoloLens YouTube](https://www.youtube.com/playlist?list=PLZCHH_4VqpRj0Nl46J0LNRkMyBNU4knbL).

## <a name="about-the-authors"></a>À propos des auteurs

<table style="border:0">
<tr>
<td style="border:0" width="60px"> <img alt="Picture of Karim Luccin at his desk" width="60" height="60" src="images/karim-thumb.jpg" /></td>
<td style="border:0"><b>Karim luccin</b> est ingénieur logiciel et passionné d’éléments visuels. Il était l’ingénieur graphique de l’Explorateur Galaxy.</td>
</tr>
<tr>
<td style="border:0" width="60px"> <img alt="Photo of art lead Andy Zibits" width="60" height="60" src="images/andy-avatar.png" /></td>
<td style="border:0"><b>Andy Zibits</b> est un responsable artistique et le passionné d’espace qui gérait l’équipe de modélisation 3D pour l’Explorateur Galaxy et lutté pour encore plus de particules.</td>
</tr>
</table>


## <a name="see-also"></a>Voir aussi
* [Explorateur Galaxy sur GitHub](https://github.com/Microsoft/GalaxyExplorer)
* [Mises à jour des projets de l’Explorateur Galaxy sur YouTube](https://www.youtube.com/playlist?list=PLZCHH_4VqpRj0Nl46J0LNRkMyBNU4knbL)
