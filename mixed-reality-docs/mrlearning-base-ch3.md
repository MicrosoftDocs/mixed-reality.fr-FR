---
title: Module de base d’apprentissage de la réalité mixte - Placement de contenu dynamique et solveurs
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 4baee7ba8643f5bb80e0456eb97d915405431654
ms.sourcegitcommit: b0b1b8e1182cce93929d409706cdaa99ff24fdee
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68387706"
---
# <a name="4-placing-dynamic-content-and-using-solvers"></a>4. Placement de contenu dynamique et utilisation de solveurs

Les hologrammes prennent vie dans HoloLens 2 quand ils suivent intuitivement l’utilisateur et sont placés dans l’environnement physique de manière à rendre l’interaction fluide et élégante. Dans ce didacticiel, nous explorons les façons de placer dynamiquement des hologrammes à l’aide des outils de positionnement disponibles de MRTK, appelés résolveurs pour la façon dont ils résolvent les scénarios de placement spatial complexes. Dans le MRTK, les solveurs sont un système de scripts et de comportements utilisés pour permettre aux éléments de l’interface utilisateur de suivre, de l’utilisateur ou d’autres objets de jeu dans la scène. Ils servent également à accélérer l’alignement sur certaines positions, rendant votre application plus intuitive. 

## <a name="objectives"></a>Objectifs

* Introduire les solveurs du MRTK
* Utiliser des solveurs pour qu’une collection de boutons suive l’utilisateur
* Utiliser des solveurs pour qu’un objet de jeu suive les mouvements captés des mains de l’utilisateur

## <a name="instructions"></a>Instructions

### <a name="location-of-solvers-in-the-mrtk"></a>Emplacement des solveurs dans le MRTK
 Pour trouver les solveurs disponibles dans votre projet, examinez le dossier du SDK MRTK (MixedRealityToolkit.SDK). Le dossier Solvers se trouve sous le dossier Utilities, comme le montre l’image ci-dessous.

![Solveurs](images/lesson3_chapter1_step1im.PNG)

>Remarque : Dans cette leçon, nous allons passer uniquement par l’implémentation du solveur orbital et du solveur RadialView. Pour en savoir plus sur la gamme complète des solveurs disponibles dans le MRTK, visitez le site suivant : https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html

### <a name="use-a-solver-to-follow-the-user"></a>Utiliser un solveur pour suivre l’utilisateur
L’objectif de ce chapitre est d’améliorer la collection de boutons précédemment créée afin qu’elle suive la direction du regard de l’utilisateur. Dans la version précédente de MRTK et HoloToolkit, il s’agissait d’une fonctionnalité accompagnent.

1. Sélectionnez l’objet parent Button Collection issu de la leçon précédente.

![Leçon 3, chapitre 2, étape 1, image](images/Lesson3_chapter2_step1im.PNG)

2. Dans le volet de l’inspecteur, cliquez sur le bouton Ajouter un composant et recherchez orbital. Le composant orbital doit apparaître. Sélectionnez-le pour ajouter le composant orbital à l’objet de jeu Button Collection.

![Leçon 3, chapitre 2, étape 2, image](images/Lesson3_Chapter2_step2im.PNG)

>Remarque : Quand vous ajoutez le composant, vous pouvez remarquer que le système ajoute le script orbital et le script du gestionnaire de solveur sous l’onglet Inspector, qui est un composant requis. 

3. Pour configurer la collection de boutons de façon à ce qu’elle suive l’utilisateur, nous devons implémenter les ajustements suivants (reportez-vous à l’image ci-dessous):
- Dans le script orbital, définissez la liste déroulante type d’orientation sur lacet uniquement. De cette façon, l’objet tourne sur un seul axe à mesure qu’il suit l’utilisateur.
- Affectez à « Local Offset » la valeur 0 sur tous les axes. Affectez à « World Offset » les valeurs x = 0, y = -0,1 et z = 0,6. Le mouvement de l’objet est verrouillé. Ainsi, quand l’utilisateur change de hauteur, l’objet reste à une hauteur fixe dans l’environnement physique, mais il peut suivre l’utilisateur à mesure que celui-ci se déplace dans l’environnement. Ces valeurs peuvent être ajustées pour obtenir un large éventail de comportements.
- Pour un comportement suivant dans lequel les boutons ne suivent que la vue de l’utilisateur une fois que l’utilisateur a éteint son chef suffisamment loin, vous pouvez sélectionner la case à cocher utiliser l’angle pas à pas pour le décalage universel (Remarque: Ce titre peut être tronqué sur certains écrans, comme dans l’image ci-dessous.) Par exemple, pour que l’objet ne suive l’utilisateur que tous les 90 degrés, définissez un nombre de pas égal à 4 (flèche verte à gauche de l’exemple). 

![Leçon 3, chapitre 2, étape 3, image](images/Lesson3_chapter2_step3im.PNG)

### <a name="enabling-objects-to-follow-tracked-hands"></a>Activation d’objets pour suivre les mains suivies

Dans cette section, nous allons configurer l’objet de jeu Cube créé précédemment pour qu’il suive les mouvements captés des mains de l’utilisateur à l’aide du solveur RadialView.

1. Sélectionnez l’objet Cube dans la hiérarchie BaseScene. Cliquez sur Ajouter un composant dans le panneau Inspecteur. 

![Leçon 3, chapitre 3, étape 1, image](images/Lesson3_Chapter3_step1im.PNG)

2. Tapez RadialView dans la zone de recherche et sélectionnez le composant RadialView pour l’ajouter au cube. Le composant Solver Handler est également ajouté automatiquement au cube.

3. Changez la vue radiale pour qu’elle ne suive pas la tête mais la main gauche. Sélectionnez le menu déroulant en regard de l’option objet suivi à référencer. Sélectionnez ensuite joint à la main gauche dans le menu.

![Leçon 3, chapitre 3, étape 3, image](images/Lesson3_chapter3_step3im.PNG)

4. Une fois que vous avez sélectionné l’articulation de la main, vous pouvez choisir la partie de la main que le cube va suivre. Pour cet exemple, nous allons utiliser le poignet. En regard de l’option jointe à la main, sélectionnez le menu déroulant et sélectionnez poignet. 

![Leçon 3, chapitre 3, étape 4, image](images/Lesson3_chapter3_step4im.PNG)

5. Affectez aux distances minimales et maximales la valeur 0 pour que le cube ne soit pas séparé du poignet de l’utilisateur. Une fois ces valeurs définies, le cube est parfaitement aligné avec le poignet. Vous pouvez également ajuster le champ sens de référence pour ajuster le comportement de l’orientation du cube, par exemple si vous souhaitez autoriser l’objet à pivoter avec la poignet de l’utilisateur en définissant la direction de référence pour orienter avec l’objet suivi.

![Leçon 3, chapitre 3, étape 5, image](images/Lesson3_chapter3_step5im.PNG)

### <a name="congratulations"></a>Félicitations
Dans ce didacticiel, vous avez appris à utiliser les solveurs de MRTK pour qu’une interface utilisateur suive intuitivement l’utilisateur. Vous avez également vu comment attacher un solveur à un objet de jeu (par exemple, un cube) pour suivre les mouvements captés des mains de l’utilisateur. Pour en savoir plus sur ces solveurs et les autres fournis avec le MRTK, n’hésitez pas à visiter la [documentation consacrée aux solveurs du MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html).

[Leçon suivante : Interaction avec des objets 3D](mrlearning-base-ch4.md)

