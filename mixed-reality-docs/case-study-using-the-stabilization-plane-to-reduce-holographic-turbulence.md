---
title: 'Étude de cas : utilisation du plan de stabilisation pour réduire la turbulence holographique'
description: Utilisation du plan de stabilisation pour réduire la turbulence holographique
author: bstrukus
ms.author: bestruku
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, stabilisation, étude de cas
ms.openlocfilehash: 039b8f671f02a27393c30c7954cf0e2925635ad0
ms.sourcegitcommit: d0da0214fdd2bbac5a91a5d895bf0e87413b29b2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/01/2020
ms.locfileid: "75597652"
---
# <a name="case-study---using-the-stabilization-plane-to-reduce-holographic-turbulence"></a>Étude de cas : utilisation du plan de stabilisation pour réduire la turbulence holographique

L’utilisation des hologrammes peut être délicate. Le fait que vous puissiez vous déplacer dans votre espace et voir vos hologrammes à partir de tous les angles différents fournit un niveau d’immersion que vous ne pouvez pas obtenir avec un écran d’ordinateur normal. La mise en place de ces hologrammes et la recherche réaliste sont une fonction technique accomplie par le matériel Microsoft HoloLens et la conception intelligente des applications holographiques.

## <a name="the-tech"></a>Le Tech

Pour que les hologrammes apparaissent comme s’ils partagent réellement l’espace avec vous, ils doivent s’afficher correctement, sans séparation des couleurs. Cela est possible, en partie, par la technologie intégrée au matériel HoloLens, qui permet aux hologrammes d’être ancrés sur ce que nous appelons un [plan de stabilisation](hologram-stability.md#reprojection).

Un plan est défini par un point et un normal, mais étant donné que nous voulons toujours que le plan fasse face à l’appareil photo, nous sommes simplement soucieux de définir le point du plan. Nous pouvons indiquer à HoloLens le point de se concentrer sur son traitement pour garder tout ce qui est ancré et stable, mais la façon de définir ce point de concentration est spécifique à l’application et peut créer ou rompre votre application en fonction du contenu.

En résumé, les hologrammes fonctionnent mieux lorsque le plan de stabilisation est correctement appliqué, mais ce qui en fait dépend du type d’application que vous créez. Jetons un coup d’œil sur la façon dont certaines des applications actuellement disponibles pour HoloLens peuvent résoudre ce problème.

## <a name="behind-the-scenes"></a>En arrière-plan

Lors du développement des applications suivantes, nous avons remarqué que lorsque nous n’avions pas utilisé le plan, les objets s’affichent lorsque notre tête a été déplacée et nous verrions la séparation des couleurs avec des déplacements rapides ou des mouvements d’hologramme. Au cours de la période de développement, nous avons appris par le biais d’une version d’évaluation et d’une erreur à utiliser au mieux le plan de stabilisation et à concevoir nos applications autour des problèmes qu’il ne peut pas résoudre.

### <a name="galaxy-explorer-stationary-content-3d-interactivity"></a>Explorateur Galaxy : contenu fixe, interactivité 3D

L' [Explorateur Galaxy](galaxy-explorer.md) comporte deux éléments majeurs dans la scène : la vue principale du contenu céleste et la petite barre d’outils d’interface utilisateur qui suit votre point de regard. Pour la logique de stabilisation, nous examinons ce que votre vecteur de pointage actuel croise avec dans chaque frame pour déterminer s’il atteint n’importe quoi sur une couche de collision spécifiée. Dans ce cas, les couches qui nous intéressent sont les planètes. par conséquent, si votre point de vue se trouve sur une planète, le plan de stabilisation est placé là. Si aucun des objets de la couche de collision cible n’est atteint, l’application utilise une couche « plan B » secondaire. Si rien n’est placé dans le regard, le plan de stabilisation est conservé à la même distance que lorsqu’Gazing au contenu. Les outils d’interface utilisateur sont laissés en tant que cible plan, car nous avons trouvé le saut entre presque et beaucoup réduit la stabilité de la scène globale.

La conception de l’Explorateur Galaxy se prête bien à préserver la stabilité des éléments et à réduire l’effet de la séparation des couleurs. L’utilisateur est encouragé à parcourir et à Orbiter le contenu plutôt que de le déplacer d’un côté à l’autre, et les planètes s’orbitent suffisamment lentement pour que la séparation des couleurs ne soit pas perceptible. En outre, une constante de 60 FPS est conservée, ce qui permet d’éviter la séparation des couleurs.

Pour vérifier cela, recherchez un fichier appelé LSRPlaneModifier.cs dans le code de l' [Explorateur Galaxy sur GitHub](https://github.com/Microsoft/GalaxyExplorer/tree/master/Assets/Scripts/Utilities).

### <a name="holostudio-stationary-content-with-a-ui-focus"></a>HoloStudio : contenu stationnaire avec un focus de l’interface utilisateur

Dans HoloStudio, vous passez la majeure partie de votre temps à regarder le même modèle que sur lequel vous travaillez. Votre point de regard ne déplace pas un volume significatif, à l’exception de lorsque vous sélectionnez un nouvel outil ou que vous souhaitez naviguer dans l’interface utilisateur, afin de simplifier la logique de définition du plan. Lorsque vous examinez l’interface utilisateur, le plan est défini sur n’importe quel élément d’interface utilisateur. Lorsque vous examinez le modèle, le plan est une distance définie, correspondant à la distance par défaut entre vous et le modèle.

![Plan de stabilisation visualisé dans HoloStudio lorsque l’utilisateur est en regard du bouton d’hébergement](images/holostudio-stabilization-plane-500px.png)

### <a name="holotour-and-3d-viewer-stationary-content-with-animation-and-movies"></a>Visionneuse HoloTour et 3D : contenu stationnaire avec animation et films

Dans HoloTour et la visionneuse 3D, vous regardez un objet animé solitaires ou un film avec des effets 3D ajoutés par-dessus. La stabilisation dans ces applications est définie sur ce que vous visualisez actuellement.

HoloTour vous empêche également de vous écarter trop loin de votre univers virtuel en le déplaçant avec vous au lieu de rester dans un emplacement fixe. Cela vous permet de vous assurer que vous ne serez pas suffisamment éloigné d’autres hologrammes pour éviter les problèmes de stabilité.

![Dans cet exemple de HoloTour, le plan de stabilisation est défini sur ce film du Pantheon de Hadrian.](images/holotour-stabilization-plane-500px.jpg)

### <a name="roboraid-dynamic-content-and-environmental-interactions"></a>RoboRaid : contenu dynamique et interactions environnementales

La définition du plan de stabilisation dans RoboRaid est étonnamment simple, bien qu’il s’agit de l’application qui nécessite le mouvement le plus soudain. Le plan est conçu pour s’orienter vers les murs ou les objets environnants et flotte à une distance fixe devant vous lorsque vous en êtes suffisamment éloigné.

RoboRaid a été conçu avec le plan de stabilisation à l’esprit. Le réticule, qui se déplace le plus puisqu’il est verrouillé, le contourne en utilisant uniquement le rouge et le bleu, ce qui minimise les traces de couleurs. Il contient également un peu de profondeur entre les pièces, ce qui réduit le risque de débordement de couleur qui se produit en le masquant avec un effet de parallaxe déjà attendu. Les robots ne se déplacent pas très rapidement et ne voyagent que sur de courtes distances à intervalles réguliers. Ils ont tendance à rester autour de 2 mètres devant vous, où la stabilisation est définie par défaut.

### <a name="fragments-and-young-conker-dynamic-content-with-environmental-interaction"></a>Fragments et jeunes Conker : contenu dynamique avec interaction environnementale

Écrit par Asobo Studio dans C++, les fragments et les jeunes Conker adoptent une approche différente pour définir le plan de stabilisation. Les points d’intérêt (d) sont définis dans le code et classés en termes de priorité. Les POI sont du contenu en jeu, comme le modèle Conker dans Conker, les menus, le réticule de visée et les logos. Les POI sont croisés par le point de regard de l’utilisateur et le plan est défini au centre de l’objet avec la priorité la plus élevée. Si aucune intersection n’est effectuée, le plan est défini sur la distance par défaut.

Les fragments et les jeunes Conkers vous informent trop loin des hologrammes en interrompant l’application si vous vous déplacez en dehors de ce qui a été précédemment analysé comme espace de lecture. Par conséquent, ils vous tiennent dans les limites qui sont disponibles pour fournir l’expérience la plus stable.

## <a name="do-it-yourself"></a>Faites-le vous-même

Si vous avez un HoloLens et que vous souhaitez vous lancer avec les concepts de cet article, vous pouvez télécharger une scène de test et essayer les exercices ci-dessous. Elle utilise l’API Gizmo intégrée de Unity et doit vous aider à visualiser l’emplacement où votre plan est défini. Ce code était également utilisé pour capturer les captures d’écran dans cette étude de cas.
1. Synchronisez la dernière version de [MixedRealityToolkit-Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity).
2. Ouvrez la scène [HoloToolkit-examples/Utilities/scenes/StabilizationPlaneSetting. Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Utilities/Scenes/StabilizationPlaneSetting.unity) .
3. Générez et configurez le projet généré.
4. Exécutez sur votre appareil.

### <a name="exercise-1"></a>Exercice 1

Vous verrez plusieurs points blancs à travers les différentes orientations. En face de vous, vous verrez trois points à des profondeurs différentes. Appuyez sur l’air pour changer le point sur lequel le plan est défini. Dans le cadre de cet exercice, et pour les deux autres, déplacez votre espace tout en Gazing les points. Tournez votre tête à gauche, à droite, en haut et en aval. Rapprochez-vous des points et éloignez-les. Découvrez comment ils réagissent lorsque le plan de stabilisation est défini sur des cibles différentes.

### <a name="exercise-2"></a>Exercice 2

À présent, passez à votre droite jusqu’à ce que vous voyez deux points mobiles, l’un oscillant sur un chemin horizontal et l’autre sur un tracé vertical. Une fois encore, appuyez sur l’air pour changer le point sur lequel le plan est défini. Notez la manière dont la séparation des couleurs est atténuée et apparaît sur le point qui est connecté au plan. Appuyez de nouveau pour utiliser la vélocité du point dans la fonction de paramétrage du plan. Ce paramètre donne une indication à HoloLens sur le mouvement prévu de l’objet. Il est important de savoir quand l’utiliser, comme vous pouvez le remarquer lorsque la vélocité est utilisée sur un point, l’autre point mobile affiche une plus grande séparation des couleurs. Gardez cela à l’esprit lors de la conception de vos applications. Si vous avez un flot de mouvements de vos objets, vous pouvez empêcher l’affichage des artefacts.

### <a name="exercise-3"></a>Exercice 3

Retournez à votre droite jusqu’à ce qu’une nouvelle configuration de points s’affiche. Dans ce cas, il y a des points dans la distance et un point en spirale avant. Appuyez pour changer le point sur lequel le plan est défini, en alternant entre les points à l’arrière et le point dans le mouvement. Notez que la définition de la position du plan et de la vélocité à celle du point en spirale fait apparaître les artefacts partout.

**Conseils**
* N’oubliez pas que la logique de définition de votre plan est simple. Comme vous l’avez vu, vous n’avez pas besoin d’algorithmes de paramètre de plan complexes pour effectuer une expérience immersive. Le plan de stabilisation n’est qu’une partie du puzzle.
* Dans la mesure du possible, déplacez toujours le plan entre les cibles en douceur. Le basculement instantané des cibles à distance peut perturber visuellement la scène.
* Envisagez de définir une option dans votre plan pour le verrouillage sur une cible très spécifique. De cette façon, le plan peut être verrouillé sur un objet, tel qu’un logo ou un écran de titre, si nécessaire.

## <a name="about-the-author"></a>À propos de l'auteur

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Ben Strukus" width="60" height="60" src="images/genericusertile.jpg"></td>
<td style="border-style: none"><b>Ben Strukus</b><br>Ingénieur logiciel @Microsoft</td>
</tr>
</table>

## <a name="see-also"></a>Articles associés
* [Notions de base de m. 100 : prise en main d’Unity](holograms-100.md)
* [Point de focus dans Unity](focus-point-in-unity.md)
* [Stabilité des hologrammes](hologram-stability.md)
