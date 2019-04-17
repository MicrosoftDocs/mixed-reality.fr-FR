---
title: Étude de cas - à l’aide du plan de stabilisation pour réduire des turbulences HOLOGRAPHIQUE
description: À l’aide du plan de stabilisation pour réduire des turbulences HOLOGRAPHIQUE
author: bstrukus
ms.author: bestruku
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, stabilisation, étude de cas
ms.openlocfilehash: a084ede5f9bf3d5f058cc81ec75840e2c2e75af2
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593238"
---
# <a name="case-study---using-the-stabilization-plane-to-reduce-holographic-turbulence"></a>Étude de cas - à l’aide du plan de stabilisation pour réduire des turbulences HOLOGRAPHIQUE

Utilisation de hologrammes peut être difficile. Le fait que vous pouvez déplacer votre espace et voir votre hologrammes à partir de tous les différents angles fournit un niveau d’immersion Impossible d’obtenir un écran d’ordinateur normal. En conservant ces hologrammes en place et en recherchant réaliste sont une prouesse technique effectuée par le matériel de Microsoft HoloLens et la conception intelligente des applications HOLOGRAPHIQUE.

## <a name="the-tech"></a>Les technologies

Pour rendre hologrammes s’affichent comme s’ils partagez en fait l’espace avec vous, ils doivent être restituées correctement, sans séparation des couleurs. Pour cela, en partie par la technologie intégrée pour le matériel de HoloLens qui conserve hologrammes ancrés sur ce que nous appelons un [plan de stabilisation](hologram-stability.md#stabilization-plane).

Un plan est défini par un point et un élément normal, mais étant donné que nous voulons toujours que le plan à relever l’appareil photo, nous nous intéressons simplement la définition de point du plan. Nous pouvons dire HoloLens qui pointent vers concentrer son traitement à conserver que tous les éléments ancrée et stable, mais comment définir ce point de focus est propre aux applications et effectuer des ou de bloquer votre application en fonction du contenu.

En bref, hologrammes fonctionnent quand le plan de la stabilisation est appliqué correctement, mais ce que signifie dépend en fait du type d’application que vous créez. Jetons un œil à la façon dont certaines applications actuellement disponibles pour HoloLens s’attaquer à ce problème.

## <a name="behind-the-scenes"></a>En arrière-plan

Lorsque vous développez des applications suivantes, nous avons remarqué que lorsque nous n’avons utilisé le plan, les objets seraient sway lorsque notre début allé et nous verrions une séparation de couleur avec tête rapide ou les mouvements hologramme. Au cours de l’intervalle de temps de développement, nous avons appris par le biais des tâtonnements comment utiliser au mieux le plan de stabilisation et la conception de nos applications dans le cadre les problèmes qu’il ne peut pas corriger.

### <a name="galaxy-explorer-stationary-content-3d-interactivity"></a>Galaxy Explorer : Contenu stationnaire, interactivité en 3D

[Explorateur de Galaxy](galaxy-explorer.md) comporte deux phases principales dans la scène : La vue principale du contenu célestes et la petite barre d’outils de l’interface utilisateur qui suit votre regard. Pour la logique de stabilisation, nous examinons ce que votre objet vector actuel du pointage de regard entre en intersection avec dans chaque frame pour déterminer si elle accède à quoi que ce soit sur une couche de collision spécifié. Dans ce cas, les couches qui nous intéressent sont planètes, donc si votre regard tombe une planète, le plan de stabilisation placé là. Si aucun des objets dans la couche de collision cible sont atteints, l’application utilise une couche secondaire « plan B ». Si rien n’est en cours gazed au, le plan de la stabilisation est conservé sur la même distance qu’il était quand gazing le contenu. Les outils d’interface utilisateur sont omis en tant que plan cible que nous trouvé le passage près et présent réduit la stabilité de la scène globale.

La conception de l’Explorateur de Galaxy se prête bien à favoriser le stable et de réduire l’effet de séparation des couleurs. L’utilisateur est encouragé à parcourir et orbite le contenu plutôt que déplacer le long de chaque côté et planètes sont a orbite suffisamment lentement pour que la séparation de couleur n’est pas perceptible. En outre, une constante 60 FPS est conservée, ce qui permet de prévenir la séparation des couleurs ne se produise.

Pour le vérifier par vous-même, recherchez un fichier appelé LSRPlaneModifier.cs dans le [code de l’Explorateur de Galaxy sur GitHub](https://github.com/Microsoft/GalaxyExplorer/tree/master/Assets/Scripts/Utilities).

### <a name="holostudio-stationary-content-with-a-ui-focus"></a>HoloStudio : Contenu fixe avec un focus de l’interface utilisateur

Dans HoloStudio, vous passez la majeure partie de votre temps à rechercher sur le même modèle sur lequel vous travaillez. Votre regard ne déplace pas une quantité importante, à l’exception de lorsque vous activez un nouvel outil ou que vous souhaitez accéder l’interface utilisateur, donc nous pouvons simplifier la logique de définition de plan. Lorsque vous examinez l’interface utilisateur, le plan est défini sur l’élément d’interface utilisateur dans quelle que soit votre regard s’aligne sur. Lorsque vous examinez le modèle, le plan est une certaine distance, correspondant à la distance entre vous et le modèle par défaut.

![Le plan de stabilisation visualisées dans HoloStudio en tant que l’utilisateur son sur le bouton Accueil](images/holostudio-stabilization-plane-500px.png)

### <a name="holotour-and-3d-viewer-stationary-content-with-animation-and-movies"></a>HoloTour et visionneuse 3D : Contenu stationnaire avec l’animation et des films

Dans HoloTour et visionneuse 3D, vous examinez un objet animé Solitaire ou une séquence avec des effets 3D ajoutés par-dessus. La stabilisation dans ces applications est définie sur tout ce qui en cours d’affichage.

HoloTour vous empêche également errants trop loin de votre monde virtuel en le faisant passer avec vous, au lieu de rester dans un emplacement fixe. Cela garantit que vous n’obtiendrez pas assez loin autres hologrammes pour les problèmes de stabilité glissent.

![Dans cet exemple à partir de HoloTour, le plan de stabilisation serait défini à ce film de Pantheon de Hadrian.](images/holotour-stabilization-plane-500px.jpg)

### <a name="roboraid-dynamic-content-and-environmental-interactions"></a>RoboRaid : Interactions de contenu et l’environnement dynamiques

Définition du plan de stabilisation dans RoboRaid est étonnamment simple, en dépit d’en cours de l’application qui requiert le déplacement plus soudain. Le plan est orienté vers la conserver les murs ou la qui entoure les objets et flotte à une distance fixe devant vous lorsque vous êtes assez loin de leur.

RoboRaid a été conçu avec le plan de stabilisation esprit. La réticule, qui déplace le meilleur parti, car il est verrouillé en tête, cela contourne en utilisant uniquement rouge et bleu, ce qui réduit les traces de couleur. Il contient également un peu de profondeur entre les éléments, en réduisant les débordements de couleurs qui se produisent en les masquant avec un effet parallaxe déjà attendu. Les robots ne déplacez très rapidement et voyagent seulement les distances courtes dans des intervalles réguliers. Ils ont tendance à rester environ 2 mètres devant vous, où la stabilisation a la valeur par défaut.

### <a name="fragments-and-young-conker-dynamic-content-with-environmental-interaction"></a>Fragments et pétarade jeune : Contenu dynamique sans interaction de l’environnement

Écrit par Asobo Studio dans C++, Fragments et Young pétarade adoptent une approche différente à la définition du plan de stabilisation. Points d’intérêt (POI) sont définis dans le code et classées en termes de priorité. POI est contenus dans le jeu tels que le modèle pétarade dans Young pétarade, les menus, le réticule visée et les logos. Les points d’intérêts sont croisées en regard de l’utilisateur et le plan est défini sur le centre de l’objet avec la priorité la plus élevée. Si aucune intersection se produit, le plan est défini sur la distance par défaut.

Fragments et Young pétarade également concevoir autour de vous errants trop loin à partir des hologrammes en suspendant l’application si vous déplacez en dehors de ce qui est encore été analysé en tant que votre espace de lecture. Par conséquent, ils vous tenir dans les limites qui sont trouvent pour fournir une expérience plus stable.

## <a name="do-it-yourself"></a>Faites-le vous-même

Si vous avez un HoloLens et que vous souhaitez jouer avec les concepts que j’ai abordés, vous pouvez télécharger une scène de test et essayer des exercices ci-dessous. Elle utilise gizmo d’intégrés d’Unity API et il doit vous aider à visualiser où votre plan est défini. Ce code a été également utilisé pour capturer les captures d’écran dans cette étude de cas.
1. Synchroniser la dernière version de [MixedRealityToolkit-Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity).
2. Ouvrez le [HoloToolkit-Examples/Utilities/Scenes/StabilizationPlaneSetting.unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Utilities/Scenes/StabilizationPlaneSetting.unity) scène.
3. Créez et configurez le projet généré.
4. Exécuter sur votre appareil.

### <a name="exercise-1"></a>Exercice 1

Vous verrez plusieurs points blancs autour de vous à différentes orientations. Devant vous, vous verrez trois points à différentes profondeurs. Appui en l’air pour modifier qui dot le plan est défini sur. Pour cet exercice et pour les deux autres, déplacer votre espace tout gazing sur les points. Activez votre principale gauche, la droite, haut et bas. Déplacer le plus proche et père des points. Voir comment ils réagissent lorsque le plan de la stabilisation est défini sur différentes cibles.

### <a name="exercise-2"></a>Exercice 2

Activer maintenant, à votre droite jusqu'à ce que vous voyez deux points de déplacement, un modifiée à plusieurs reprises sur un chemin d’accès horizontal et l’autre sur un chemin d’accès vertical. Une fois encore,-appui en l’air pour modifier le point le plan est défini sur. Notez comment la séparation des couleurs est atténuée apparaît sur le point qui est connecté au plan. Appuyez à nouveau pour utiliser vélocité du point dans la fonction de définition de plan. Ce paramètre fournit un Conseil pour HoloLens sur motion prévue de l’objet. Il est important de savoir quand l’utiliser, comme vous le remarquerez quand la vélocité est utilisée sur un seul point, l’autre point de déplacement affichera une plus grande séparation de couleur. Gardez cela à l’esprit lorsque vous concevez vos applications — ayant un flux cohérent pour le mouvement de vos objets peut aider à empêcher l’affichage des artefacts.

### <a name="exercise-3"></a>Exercice 3

Activer une fois de plus à votre droite jusqu'à ce que vous voyiez une nouvelle configuration de points. Dans ce cas il existe des points dans la distance et un seul point en augmentation constante et l’extraction devant eux. Appuyez pour modifier le point le plan a la valeur, alternant entre les points de la restauration automatique et le point dans le mouvement de l’air. Notez comment définir la position de plan et la rapidité à celle du point spirale, les artefacts apparaissent partout.

**Conseils**
* Simplifiez votre logique de définition de plan. Comme vous l’avez vu, vous n’avez pas besoin des algorithmes de paramètre de plan complexe pour rendre une expérience d’immersion. Le plan de la stabilisation n'est qu’une seule pièce du puzzle.
* Cela est possible, au toujours déplacer le plan entre les cibles sans heurts. Commutation instantanément cibles distants peut interrompre visuellement la scène.
* Envisagez de disposer d’une option dans votre logique de définition de plan pour verrouiller sur une cible très spécifique. De cette façon, vous pouvez avoir le plan verrouillé sur un objet, par exemple un écran logo ou le titre, si nécessaire.

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Ben Strukus" width="60" height="60" src="images/genericusertile.jpg"></td>
<td style="border-style: none"><b>Ben Strukus</b><br>Ingénieur logiciel @Microsoft</td>
</tr>
</table>

## <a name="see-also"></a>Voir aussi
* [Principes de base MR 100 : Mise en route avec Unity](holograms-100.md)
* [Point de focus dans Unity](focus-point-in-unity.md)
* [Stabilité HOLOGRAMME](hologram-stability.md)
