---
title: Didacticiels de mise en route-4. Placement de contenu dynamique et utilisation de solveurs
description: Suivez ce cours pour découvrir comment implémenter Reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: e08de0bc769ceda493eafe40158b6aeed87751c7
ms.sourcegitcommit: 23b130d03fea46a50a712b8301fe4e5deed6cf9c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2019
ms.locfileid: "75334361"
---
# <a name="4-placing-dynamic-content-and-using-solvers"></a>4. placement de contenu dynamique et utilisation de solveurs

Les hologrammes arrivent à la vie dans HoloLens 2 lorsqu’ils suivent intuitivement l’utilisateur et sont placés dans l’environnement physique d’une manière qui rend l’interaction transparente et élégante. Dans ce didacticiel, nous explorons les façons de placer dynamiquement des hologrammes à l’aide des outils de placement disponibles de MRTK (appelés solveurs) pour résoudre des scénarios de placement spatial complexes. Dans le MRTK, les solveurs sont un système de scripts et de comportements utilisés pour permettre aux éléments de l’interface utilisateur de suivre, de l’utilisateur ou d’autres objets de jeu dans la scène. Ils servent également à accélérer l’alignement sur certaines positions, rendant votre application plus intuitive.

## <a name="objectives"></a>Objectifs

* Introduire les solveurs du MRTK
* Utiliser des solveurs pour qu’une collection de boutons suive l’utilisateur
* Utiliser des solveurs pour qu’un objet de jeu suive les mouvements captés des mains de l’utilisateur

## <a name="location-of-solvers-in-the-mrtk"></a>Emplacement des solveurs dans le MRTK

 Pour trouver les solveurs disponibles dans votre projet, consultez le dossier MRTK SDK (dossier MixedRealityToolkit. SDK). Dans le dossier Utilitaires, vous verrez le dossier solveurs, comme illustré dans l’image ci-dessous.

![Solveurs](images/lesson3_chapter1_step1im.PNG)

>[!NOTE]
>Dans cette leçon, nous allons uniquement examiner l’implémentation du solveur orbital et du solveur RadialView. Pour en savoir plus sur l’ensemble des programmes de résolution disponibles dans le MRTK, visitez le site : [https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html)

## <a name="use-a-solver-to-follow-the-user"></a>Utiliser un solveur pour suivre l’utilisateur

L’objectif de ce chapitre est d’améliorer la collection de boutons précédemment créée afin qu’elle suive la direction du regard de l’utilisateur. Dans la version précédente de MRTK et HoloToolkit, il s’agissait d’une fonctionnalité accompagnent.

1. Sélectionnez l’objet parent Button Collection issu de la leçon précédente.

    ![Leçon 3, chapitre 2, étape 1, image](images/Lesson3_chapter2_step1im.PNG)

2. Dans le volet de l’inspecteur, cliquez sur le bouton Ajouter un composant et recherchez orbital. Le composant orbital doit apparaître. Sélectionnez-le pour ajouter le composant orbital à l’objet de jeu de collection de boutons.

    ![Leçon 3, chapitre 2, étape 2, image](images/Lesson3_Chapter2_step2im.PNG)

    >[!NOTE]
    >Lorsque vous ajoutez le composant orbital, vous remarquerez que le système ajoute également le composant SolverHandler, qui est un composant obligatoire.

3. Pour configurer la collection de boutons de façon à ce qu’elle suive l’utilisateur, nous devons implémenter les ajustements suivants (reportez-vous à l’image ci-dessous) :

    * Dans le script orbital, définissez la liste déroulante type d’orientation sur lacet uniquement. De cette façon, l’objet tourne sur un seul axe à mesure qu’il suit l’utilisateur.
    * Affectez à « Local Offset » la valeur 0 sur tous les axes. Définissez le décalage universel sur x = 0, y =-0,1 et z = 0,6. Cela verrouille le déplacement de l’objet de sorte que lorsque l’utilisateur change de hauteur, l’objet reste à une hauteur fixe dans l’environnement physique, tout en lui permettant de suivre l’utilisateur lorsque l’utilisateur se déplace sur l’environnement. Ces valeurs peuvent être ajustées pour obtenir un large éventail de comportements.
    * Pour un comportement suivant dans lequel les boutons ne suivent que la vue de l’utilisateur une fois que l’utilisateur a mis son chef suffisamment loin, vous pouvez sélectionner la case à cocher utiliser l’angle pas à pas pour le décalage universel (Remarque : ce titre peut être tronqué sur certains écrans, comme c’est le cas dans l’image ci-dessous). Par exemple, pour que l’objet suive l’utilisateur uniquement tous les 90 degrés, définissez le nombre d’étapes égal à 4 (marqué d’une flèche verte dans l’exemple ci-dessous).

    ![Leçon 3, chapitre 2, étape 3, image](images/Lesson3_chapter2_step3im.PNG)

## <a name="enabling-objects-to-follow-tracked-hands"></a>Activation d’objets pour suivre les mains suivies

Dans cette section, nous allons configurer l’objet de jeu de cube créé précédemment pour suivre les mains suivies par l’utilisateur à l’aide du solveur RadialView.

1. Sélectionnez l’objet de cube dans la hiérarchie BaseScene. Cliquez sur Ajouter un composant dans le panneau Inspecteur. Tapez RadialView dans la zone de recherche et sélectionnez le composant RadialView pour l’ajouter au cube. Le composant SolverHandler sera également ajouté automatiquement au cube.

    ![mrlearning-base-CH3-3-step3. png](images/mrlearning-base-ch3-3-step1.png)

2. Pour modifier le RadialView pour qu’il suive une main au lieu de l’en-tête, sélectionnez le menu déroulant en regard de l’option type de cible suivi et sélectionnez jointure manuelle dans le menu.

    ![mrlearning-base-CH3-3-Step2. png](images/mrlearning-base-ch3-3-step2a.png)

    Vous voyez maintenant deux nouvelles options, le type de disponibilité suivi et l’articulation à la main. Pour cet exemple, vous aurez le RadialView suivre le poignet de la main gauche, comme illustré dans l’image ci-dessous.

    ![mrlearning-base-CH3-3-step2b. png](images/mrlearning-base-ch3-3-step2b.png)

3. Définissez les distances maximale et minimale de la vue radiale sur 0 afin que le cube n’ait pas de distance entre celui-ci et le poignet de l’utilisateur. Une fois ces valeurs définies, le cube est parfaitement aligné avec le poignet. Vous pouvez également ajuster le champ sens de référence pour ajuster le comportement de l’orientation du cube, par exemple si vous souhaitez autoriser l’objet à pivoter avec la poignet de l’utilisateur en définissant le sens de référence sur orienté objet.

    ![mrlearning-base-CH3-3-step3. png](images/mrlearning-base-ch3-3-step3.png)

## <a name="congratulations"></a>Félicitations !

Dans ce didacticiel, vous avez appris à utiliser les solveurs de MRTK pour qu’une interface utilisateur suive intuitivement l’utilisateur. Vous avez également vu comment attacher un solveur à un objet de jeu (par exemple, un cube) pour suivre les mouvements captés des mains de l’utilisateur. Pour en savoir plus sur ces solveurs et les autres fournis avec le MRTK, n’hésitez pas à visiter la [documentation consacrée aux solveurs du MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html).

[Leçon suivante : 5. interaction avec les objets 3D](mrlearning-base-ch4.md)
