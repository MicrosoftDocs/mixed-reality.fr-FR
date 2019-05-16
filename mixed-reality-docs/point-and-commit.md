---
title: Point et validation des mains
description: Vue d’ensemble du modèle d’entrée point et de validation
author: caseymeekhof
ms.author: cmeekhof
ms.date: 04/05/2019
ms.topic: article
ms.localizationpriority: high
keywords: Une réalité, interaction, conception, hololens, mains, mixte présent, pointez et valider
ms.openlocfilehash: e69c8ff2091beff7d8fbbde4e6f24d909302290a
ms.sourcegitcommit: 1c0fbee8fa887525af6ed92174edc42c05b25f90
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65730803"
---
# <a name="point-and-commit-with-hands"></a>Point et validation des mains
Point et validation des mains est un modèle d’entrée qui permet aux utilisateurs à cibler, sélectionner et manipuler des objets de contenu et 3D 2D dans la distance. Cette technique d’interaction « beaucoup » est unique à la réalité mixte et n’est pas un humains moyen naturellement intereact avec le monde réel. Par exemple, dans le film super héros *X-hommes*, le caractère [magnéto](https://en.wikipedia.org/wiki/Magneto_(comics)) est capable de contacter et de manipulation d’un objet lointain dans la distance à ses mains. Cela n’est pas quelque chose l’homme faire en réalité. Dans les HoloLens (AR) et la réalité mixte (VR), nous équiper les internautes grâce à cette puissance magique, la contrainte physique du monde réel non seulement à une expérience optimale à vos avec contenu HOLOGRAPHIQUE, mais également pour améliorer l’interaction efficace et plus efficace.

## <a name="device-support"></a>Prise en charge des appareils

Modèle d’entrée | [HoloLens (1er gen)](https://docs.microsoft.com/en-us/windows/mixed-reality/hololens-hardware-details) | HoloLens 2 | [Casques IMMERSIFS](https://docs.microsoft.com/en-us/windows/mixed-reality/immersive-headset-hardware-details) |
| ---------| -----| ----- | ---------|
Point et validation (interaction lointain main) | ❌ Ne pas pris en charge | ✔️ Recommandé | ✔️ Recommandé

Point et validation, également appelé mains présent, est une des nouvelles fonctionnalités qui utilise le nouveau système de suivi de la main articulé. Ce modèle d’entrée est également le modèle d’entrée principal sur des casques IMMERSIFS grâce à l’utilisation de contrôleurs de mouvement.

## <a name="hand-rays"></a>Rayons de main

Sur HoloLens 2, nous avons créé un rayon de main qui enverra à partir du centre d’un palm. Cette ray est traité comme une extension de la main. Un curseur en forme de graphique en anneau est attaché à la fin du rayon utilisé pour indiquer l’emplacement où le rayon croise avec un objet cible. L’objet qui le curseur arrive sur peut ensuite recevoir des commandes geste à partir de la main.

Cette commande geste de base est déclenchée en utilisant le curseur de défilement et votre index pour effectuer l’action d’appui en l’air. En utilisant le rayon de main pour pointer et appuyez sur validation, les utilisateurs peuvent activer un bouton ou un lien hypertexte sur un contenu web. Les gestes composites plus, les utilisateurs sont capables de navigation de contenu web et la manipulation des objets 3D à partir d’une distance. La conception visuelle du rayon main doit également réagir à ces États point et de validation, comme décrit et indiqué ci-dessous : 

* Dans le *pointant* d’état, le rayon est une ligne en tirets, et le curseur se trouve une forme de graphique en anneau.
* Dans le *validation* d’état, le rayon se transforme en une ligne pleine et le curseur est réduit à un point.

![](images/Hand-Rays-720px.jpg)

## <a name="transition-between-near-and-far"></a>La transition entre près et lointain

Au lieu d’utiliser le mouvement spécifique, par ex., « pointant avec votre index » pour indiquer le rayon, nous avons conçu le rayon bientôt out à partir du centre de palm, libérer et de réserver les cinq doigts pour les gestes de manipulations plus, tel que pincement et récupérer. Grâce à cette conception, nous ne créer qu’un seul modèle mental, prenant en charge exactement le même ensemble de mouvements de main pour l’interaction proche et lointain. Vous pouvez utiliser le même mouvement de manipulation pour manipuler des objets à des distances différentes. L’appel des rayons est automatique et proximité en fonction :

*  Lorsqu’un objet est dans arm atteint distance (environ 50 cm), les rayons sont désactivées automatiquement encourageant pour l’interaction proche.
*  Lorsque l’objet est plus loin que 50 cm, les rayons sont sous tension. La transition doit être fluide et homogène.

![](images/Transition-Between-Near-And-Far-720px.jpg)

## <a name="2d-slate-interaction"></a>Interaction ardoise 2D

Une ardoise 2D est un conteneur HOLOGRAPHIQUE hébergement de contenu application 2D, comme navigateur web. Le concept de conception pour présent interagir avec une ardoise 2D consiste à utiliser des rayons de main vers tap cible et air à sélectionner. Après la cible avec un rayon de main, les utilisateurs peuvent air tap pour déclencher un lien hypertexte ou un bouton. Ils peuvent utiliser une seule main pour « tap et faites glisser l’air » pour faire défiler un contenu ardoise diminué. Le mouvement relatif de l’utilisation de deux mains pour appuyer et faire glisser l’air peut effectuer un zoom avant et de sortie le contenu ardoise.

Le rayon disponible dans les angles et les bords de ciblage révèle le plus proche intuitif de manipulation. Par « manipulation et faites glisser » l’intuitivité de manipulation, les utilisateurs permettre effectuer des glyphes de largeurs uniformes mise à l’échelle via l’intuitivité de coin et peuvent ajuster dynamiquement l’ardoise via l’intuitivité edge. Les utilisateurs peuvent déplacer l’ardoise entière en saisissant et en faisant glisser le holobar en haut de l’ardoise 2D.

![](images/2D-Slate-Interaction-Far-720px.jpg)

Pour la manipulation 2D d’ardoise lui-même :<br>

* Les utilisateurs pointent le rayon de la main à angles ou sur les bords pour révéler le plus proche intuitif de manipulation. 
* En appliquant un mouvement de manipulation sur l’intuitif, les utilisateurs peuvent effectuer une mise à l’échelle uniforme via intuitif de l’angle et peuvent ajuster dynamiquement l’ardoise via l’intuitif edge. 
* En appliquant un mouvement de manipulation sur la holobar en haut de l’ardoise 2D, les utilisateurs peuvent déplacer l’ardoise entière.<br>

<br>

## <a name="3d-object-manipulation"></a>Manipulation des objets 3D

Dans manipulation directe, il existe deux moyens permettant aux utilisateurs de manipuler l’objet 3D, en fonction du intuitif de manipulation et manipulation en non intuitif. Dans le modèle de point et de validation, les utilisateurs sont capables d’atteindre exactement les mêmes tâches par le biais des rayons de main. Aucun apprentissage supplémentaire n’est nécessaire.<br>

### <a name="affordance-based-manipulation"></a>En fonction du intuitif de manipulation
Les utilisateurs utiliser rayons de main pour pointer et faire apparaître la zone englobante et l’intuitivité de manipulation. Les utilisateurs peuvent appliquer le mouvement de manipulation sur la zone englobante pour déplacer l’objet entier, l’intuitivité edge pour faire pivoter et sur le coner permettant à l’échelle de manière uniforme. <br>

![](images/3D-Object-Manipulation-Far-720px.jpg) <br>


### <a name="non-affordance-based-manipulation"></a>Le caractère non-intuitif en fonction de manipulation
Les utilisateurs point avec des rayons de main pour faire apparaître la zone englobante, puis appliquer directement des mouvements de manipulation sur celui-ci. Une part, la traduction et la rotation de l’objet sont associées au mouvement et l’orientation de la main. Avec deux mains, les utilisateurs peuvent traduire, mettre à l’échelle et faire pivoter en fonction des mouvements relatifs de deux mains.<br>

<br>

## <a name="instinctual-gesturers"></a>Gesturers instinctual
Le concept de mouvements instinctual de point et de validation est semblable à la manipulation directe. Les gestes que les utilisateurs sont censés pour effectuer sur un objet 3D sont guidés par la conception du intuitivité de l’interface utilisateur. Par exemple, un point de contrôle petite peut motiver aux utilisateurs de pincement avec leurs thumb et le doigt de l’index, tandis qu’un utilisateur doit saisir un plus grand objet à l’aide de tous les doigts de 5.

![](images/Instinctual-Gestures-Far-720px.jpg)<br>

## <a name="symmetric-design-between-hands-and-6-dof-controller"></a>Conception symétrique entre les mains et 6 contrôleur DDL 
Le concept de point et de validation pour l’interaction lointain a été initialement créé et défini pour le mixte réalité Portal (MRP), où un utilisateur passionnés un casque immersif et interagit avec les objets 3D par le biais de contrôleurs de mouvement. Les contrôleurs de mouvement dépanner les rayons pour pointant et la manipulation des objets lointain. Il existe des boutons sur les contrôleurs de validation supplémentaire de différentes actions. Nous exploiter le modèle d’interaction des rayons et les joint à deux mains. Grâce à cette conception symétrique, les utilisateurs familiarisés avec MRP ne devront pas apprendre un autre modèle d’interaction pour présent pointant et de manipulation lorsqu’ils utilisent HoloLen 2 et vice versa.    

![](images/Symmetric-Design-For-Rays-720px.jpg)<br>

## <a name="instinctual-gestures"></a>Mouvements instinctual

![](images/Instinctual-Gestures-Far-720px.jpg)

## <a name="see-also"></a>Voir aussi
* [Pointer du regard vers l’avant et valider](gaze-and-commit.md)
* [Manipulation directe avec les mains](direct-manipulation.md)
* [Interactions instinctuelles](interaction-fundamentals.md)

