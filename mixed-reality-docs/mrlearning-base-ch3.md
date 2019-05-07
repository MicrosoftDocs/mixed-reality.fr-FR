---
title: Module de Base de formation de MR - positionnement du contenu dynamique et solveurs
description: Terminer ce cours pour apprendre à implémenter la reconnaissance faciale de Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, hololens (didacticiel), unity,
ms.openlocfilehash: b212812beeff54bb1f92ccbcc923ab9c301945b7
ms.sourcegitcommit: a32f673814a6cd6ff00f936f448885788b3b882c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2019
ms.locfileid: "64929555"
---
# <a name="mr-learning-base-module---dynamic-content-placement-and-solvers"></a>Module de Base de formation de MR - positionnement du contenu dynamique et solveurs

Hologrammes prennent vie dans les 2 HoloLens lorsqu’ils intuitivement de suivent l’utilisateur et sont placés dans l’environnement physique d’une manière qui facilite l’interaction transparente et élégant. Dans la leçon 3, nous allons examiner les façons de placer dynamiquement hologrammes à l’aide des outils de positionnement disponibles de la MRTK, appelés « solveurs. » Ils sont appelés « solveurs » quant à la manière qu’ils résolvent des algorithmes de positionnement spatial complexes. Dans le MRTK, solveurs forment un système de scripts et les comportements que nous utilisons pour être en mesure de permettre aux éléments d’interface utilisateur vous suivent, l’utilisateur ou autres objets de jeu dans la scène. Ils peuvent également servir à aligner sur certaines positions rapidement, faire de votre application plus intuitive. 

## <a name="objectives"></a>Objectifs

* Introduire des solveurs de la MRTK
* Utilisation des solveurs d’avoir une collection de boutons suivent l’utilisateur
* Utilisation des solveurs d’avoir un objet de jeu suivent mains suivies de l’utilisateur

## <a name="instructions"></a>Instructions

### <a name="location-of-solvers-in-the-mrtk"></a>Emplacement des solveurs dans le MRTK
 Pour rechercher des solveurs disponibles dans votre projet, recherchez dans le dossier MRTK SDK (dossier MixedRealityToolkit.SDK), puis, sous le dossier utilitaires vous verrez le dossier solveurs, comme illustré dans l’image ci-dessous.

![Solveurs](images/lesson3_chapter1_step1im.PNG)

>Remarque: Dans cette leçon, nous allons uniquement par rapport à l’implémentation du solveur « Orbital » et le solveur « RadialView ». Pour en savoir plus sur la gamme complète des solveurs disponibles dans le MRTK, visitez le site : https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html

### <a name="use-a-solver-to-follow-the-user"></a>Utiliser un solveur pour suivre l’utilisateur
L’objectif de ce chapitre consiste à améliorer la collection de boutons que nous avons précédemment créé de sorte qu’elle suive direction du regard de l’utilisateur. Dans la version précédente du MRTK et HoloToolkit, cela a été appelé une fonctionnalité « taglong ».

1. Sélectionnez l’objet parent de Collection de boutons de la leçon précédente.

![Lesson3 Chapter2 Step1im](images/Lesson3_chapter2_step1im.PNG)

2. Dans ce panneau, cliquez sur le bouton « Ajouter un composant » et recherchez « orbitales. » Le composant orbital doit apparaître. Sélectionner pour ajouter le composant orbital à l’objet de jeu de Collection de boutons.

![Lesson3 Chapter2 Step2im](images/Lesson3_Chapter2_step2im.PNG)

>Remarque: Lorsque vous ajoutez un composant, vous remarquerez que le système ajoute le script orbital et le script de gestionnaire de solveur dans l’onglet inspecteur, qui est un composant obligatoire. 

3. Pour configurer la collection de boutons pour suivre l’utilisateur, nous devons effectuer les ajustements suivants (reportez-vous à l’image ci-dessous) :
- Dans le script Orbital, définissez la liste déroulante « type orientation » à « Lacet uniquement ». Cela rend afin qu’un seul axe en question de l’objet pivote comme il suit l’utilisateur.
- La valeur est l’offset local 0 sur tous les axes. La valeur est le décalage du monde x = 0, y = -0,1 et z = 0.6. Ceci verrouille le déplacement de l’objet tel que lorsque l’utilisateur modifie la hauteur, l’objet reste à une hauteur fixe dans l’environnement physique, tout en permettant à suivre l’utilisateur quand l’utilisateur se déplace sur l’environnement. Ces valeurs peuvent être ajustés pour obtenir une plage wade de comportements.
- Pour un comportement de suivi par laquelle les boutons uniquement suivent l’utilisateur une fois que l’utilisateur principal de son propre suffisamment loin, vous pouvez sélectionner la case à cocher « Utiliser Angle exécution pas à pas pour le décalage du monde » (Remarque : Ce titre peut être tronqué sur certains écrans, car il est dans l’image ci-dessous.) Par exemple, pour que l’objet à suivre l’utilisateur uniquement tous les 90 degrés, définissez le nombre d’étapes égal à 4 (marqués par une flèche verte dans l’exemple à gauche). 

![Lesson3 Chapter2 Step3im](images/Lesson3_chapter2_step3im.PNG)

### <a name="enabling-objects-to-follow-tracked-hands"></a>L’activation d’objets à suivre les mains suivies

Dans cette section, nous allons configurer l’objet de jeu de cube créé précédemment pour suivre les mains de suivi de l’utilisateur avec le solveur RadialView.

1. Sélectionnez l’objet de cube dans la hiérarchie BaseScene. Cliquez sur « Ajouter un composant » dans le panneau de l’inspecteur. 

![Lesson3 chapitre3 Step1im](images/Lesson3_Chapter3_step1im.PNG)

2. Tapez « RadialView » dans la zone de recherche et sélectionnez le composant RadialView pour l’ajouter au cube. Le composant de gestionnaire de solveur sera également être ajouté automatiquement au cube.

3. Modifier la vue radiale pour ne respecte pas la tête, mais suivez la main gauche. Sélectionnez le menu déroulant en regard de l’option « objet à référencer les suivies ». Puis sélectionnez « transférer joint gauche » dans le menu.

![Lesson3 chapitre3 Step3im](images/Lesson3_chapter3_step3im.PNG)

4. Une fois que vous sélectionnez la jointure manuellement, vous pouvez choisir quelle partie de la main, vous souhaitez que le cube à suivre. Pour cet exemple, nous allons utiliser le poignet. En regard de l’option « joint main suivies » sélectionnez le menu déroulant et poignet. 

![Lesson3 chapitre3 Step4im](images/Lesson3_chapter3_step4im.PNG)

5. Définissez les distances minimales et maximales sur 0 afin que le cube n’aura pas n’importe quelle distance entre elle et poignet de l’utilisateur. Une fois définie, le cube sera parfaitement aligné avec le poignet. Vous pouvez également ajuster le champ « Direction de référence » pour ajuster le comportement de la façon dont le cube est orienté (par exemple, si vous souhaitez permettre à l’objet faire pivoter avec poignet de l’utilisateur, définissez la direction de la référence à « Orient avec objet suivies »)

![Lesson3 chapitre3 Step5im](images/Lesson3_chapter3_step5im.PNG)

### <a name="congratulations"></a>Félicitations !
Félicitations ! Dans cette leçon, vous avez appris à utiliser des solveurs de la MRTK pour avoir une interface utilisateur intuitive suivre l’utilisateur. Vous avez également appris comment attacher un solveur à un objet de jeu (par exemple, le cube) à suivre les mains de suivi de l’utilisateur. Pour en savoir plus sur ces autres solveurs inclus avec le MRTK, n’hésitez pas à visiter le [page de documentation solveurs MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html).

[Leçon suivante : Interaction des objets 3D](mrlearning-base-ch4.md)

