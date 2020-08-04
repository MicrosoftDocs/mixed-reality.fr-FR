---
title: Tutoriels de démarrage - 5. Création de contenu dynamique avec des solveurs
description: Ce cours vous montre comment utiliser Mixed Reality Toolkit (MRTK) pour créer une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 1a5017d8bc18ef239db88ee62cb2b65c77b2ab6f
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376611"
---
# <a name="5-creating-dynamic-content-using-solvers"></a>5. Création de contenu dynamique avec des solveurs

## <a name="overview"></a>Vue d’ensemble

Dans ce tutoriel, vous allez explorer différentes façons de placer dynamiquement des hologrammes à l’aide des outils de placement fournis dans le MRTK, appelés « solveurs », pour résoudre des scénarios de placement spatial complexes. Dans MRTK, les solveurs sont un système de scripts et de comportements utilisés pour permettre aux objets de suivre l’utilisateur (vous) ou d’autres objets de jeu dans la scène. Ils peuvent aussi être utilisés pour l’alignement sur certaines positions, rendant votre application plus intuitive.

## <a name="objectives"></a>Objectifs

* Introduire les solveurs du MRTK
* Apprendre à utiliser des solveurs pour diriger l’utilisateur vers des objets
* Apprendre à utiliser des solveurs pour repositionner des objets

## <a name="location-of-solvers-in-the-mrtk"></a>Emplacement des solveurs dans le MRTK

 Les solveurs du MRTK se trouvent dans le dossier du SDK MRTK. Pour voir les solveurs disponibles dans votre projet, dans la fenêtre Project, accédez à **Assets** > **MRTK** > **SDK** > **Features** > **Utilities** > **Solvers** :

![mr-learning-base](images/mr-learning-base/base-05-section1-step1-1.png)

Dans ce tutoriel, nous allons passer en revue l’implémentation du solveur Directional Indicator et Tap To Place. Pour en savoir plus sur l’ensemble des solveurs disponibles dans MRTK, consultez le guide [Solveurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

> [!NOTE]
> Le solveur Directional Indicator ne se trouve pas dans les dossiers des solveurs référencés ci-dessus, mais dans les dossiers Assets > MRTK > SDK > Experimental > Features > Utilities, car il s’agit d’une fonctionnalité expérimentale.

## <a name="using-the-directional-indicator-solver-to-direct-the-user-to-objects"></a>Utilisation du solveur Directional Indicator pour diriger l’utilisateur vers des objets

Dans la fenêtre Project, accédez au dossier à la **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs**, cliquez et faites glisser le préfabriqué **Chevron** dans la fenêtre Hierarchy et définissez sa **Position** de transformation sur X = 0, Y = 0, Z = 2 pour le positionner à proximité de l’objet RoverExplorer :

![mr-learning-base](images/mr-learning-base/base-05-section2-step1-1.png)

> [!TIP]
> Si vous constatez que l’appareil photo ou d’autres icônes de votre scène masquent les objets ou gênent, vous pouvez les masquer en <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">basculant les Gizmos</a> sur la position désactivé, comme illustré dans l’image ci-dessus. Pour en savoir plus sur le menu Gizmos et sur la façon dont vous pouvez l’utiliser pour optimiser votre vue Scene, consultez la page consacrée au <a href="https://docs.unity3d.com/Manual/GizmosMenu.html" target="_blank">menu Gizmos</a> dans la documentation Unity.

Renommez l’objet **Indicator** de Chevron qui vient d’être ajouté puis, dans la fenêtre Inspector, utilisez le bouton **Ajouter un composant** pour ajouter les composants **DirectionalIndicator** et **Directional Indicator Controller (Script)**  :

![mr-learning-base](images/mr-learning-base/base-05-section2-step1-2.png)

> [!NOTE]
> Quand vous ajoutez un solveur, dans ce cas le composant DirectionalIndicator, le composant SolverHandler est ajouté automatiquement car les solveurs en ont besoin.

> [!NOTE]
> Directional Indicator Controller (Script) ne fait pas partie du MRTK, mais il a été inclus avec les ressources du tutoriel.

Configurez les composants DirectionalIndicator et SolverHandler comme suit :

* Vérifiez que la propriété **Tracked Target Type** du composant **SolverHandler** est définis sur **Head**.
* Affectez le **RoverExplorer** à la **Directional Target** du composant **DirectionalIndicator**  en le faisant glisser de la fenêtre Hierarchy vers le champ **None (Transform)** .
* Changez la valeur de **View Offset** en 0,2

![mr-learning-base](images/mr-learning-base/base-05-section2-step1-3.png)

Appuyez sur le bouton de lecture pour passer en mode Game, appuyez sur le bouton droit de la souris et maintenez-le enfoncé tout en déplaçant votre souris vers la droite ou la gauche pour faire pivoter la direction de votre regard, et notez les points suivants :

* Quand vous détachez votre regard de l’objet RoverExplorer, l’objet Indicator apparaît et pointe vers l’objet RoverExplorer

![mr-learning-base](images/mr-learning-base/base-05-section2-step1-4.png)

> [!NOTE]
> Si vous ne voyez pas le rayon de la caméra dans votre fenêtre Scene, vérifiez que votre menu Gizmos est activé, comme illustré dans l’image ci-dessus.

> [!TIP]
> Pour découvrir comment utiliser la simulation d’entrée dans l’éditeur, consultez le guide [Utilisation de la simulation d’entrée avec les mains dans l’éditeur pour tester une scène](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

> [!TIP]
> Si votre ordinateur dispose d’un microphone, vous pouvez facilement basculer l’état actif du volet Diagnostics qui apparaît dans la fenêtre Game avec la commande vocale « toggle diagnostics ». Vous pouvez aussi le désactiver dans MRTK Configuration Profile > Diagnostics > Enable Diagnostics System. D’une façon générale, il est cependant recommandé de conserver Diagnostics System actif pendant le développement.

## <a name="using-the-tap-to-place-solver-to-reposition-objects"></a>Utilisation du solveur Tap to Place pour repositionner des objets

Dans la fenêtre Hierarchy, sélectionnez l’objet RoverExplorer > **RoverAssembly** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Tap To Place (Script)** et configurez-le comme suit :

* Vérifiez que la propriété **Tracked Target Type** du composant **SolverHandler** est définis sur **Head**.
* Cochez la case **Keep Orientation Vertical**.
* Dans la liste déroulante **Magnetic Surfaces** > **Element 0**, décochez toutes les options sauf **Spatial Awareness**.

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-1.png)

> [!NOTE]
> Le paramètre Magnetic Surfaces détermine les objets que le composant Tap To Place (Script) peut détecter lors du placement d’un objet. Si vous changez le paramètre pour activer seulement Spatial Awareness, le composant Tap To Place (Script) pourra placer le Rover seulement sur les objets de la couche Unity nommée Spatial Awareness qui est par défaut le maillage de la reconnaissance spatiale généré par HoloLens.
>
>Pour en savoir plus sur les couches, reportez-vous à la documentation <a href="https://docs.unity3d.com/Manual/Layers.html" target="_blank">Couches</a> d’Unity.

> [!TIP]
> Si vous voulez voir le maillage de la reconnaissance spatiale lors du test de la fonctionnalité Tap to Place sur votre HoloLens, vous pouvez définir temporairement la propriété Display Option du Spatial Mesh Observer sur Visible. Pour vous rappeler comment changer l’option d’affichage, reportez-vous aux instructions de [Changer l’option d’affichage de la reconnaissance spatiale](mr-learning-base-03.md#changing-the-spatial-awareness-display-option).

Avec l’objet RoverAssembly toujours sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, recherchez l’événement **On Placing Started ()** puis cliquez sur l’icône **+** pour ajouter un nouvel événement :

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-2.png)

Configurez l’événement comme suit :

* Affectez l’objet **RoverAssembly** en tant qu’écouteur pour l’événement On Placing Started () en le faisant glisser de la fenêtre Hierarchy dans le champ **None (Object)**
* Dans la liste déroulante **No Function**, sélectionnez **TapToPlace** > **float SurfaceNormalOffset** pour mettre à jour la valeur de la propriété SurfaceNormalOffset quand l’événement est déclenché.
* Vérifiez que l’argument est défini sur **0**

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-3.png)

Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur une zone vide, sélectionnez **3D Object** > **Cube** pour créer un objet temporaire représentant le sol, puis configurez le composant **Transform** comme suit :

* **Position** : X = 0, Y = -1,65, Z = 6
* **Rotation** : X = 0, Y = 0, Z = 0
* **Scale** : X = 10, Y = 0,2, Z = 10

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-4.png)

Le cube temporaire étant toujours sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, utilisez la liste déroulante **Couches** pour changer le paramètre Layer du cube de façon à inclure seulement la couche **Spatial Awareness** :

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-5.png)

Appuyez sur le bouton Play pour passer en mode Game. Ensuite, maintenez enfoncé le bouton droit de la souris tout en déplaçant la souris vers le bas jusqu’à ce que le regard atteigne l’objet RoverAssembly :

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-6.png)

Cliquez avec le bouton gauche de la souris pour démarrer le processus de Tap to Place :

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-7.png)

Appuyez sur le bouton droit de la souris et maintenez-le enfoncé tout en déplaçant votre souris vers la droite ou la gauche pour faire pivoter la direction de votre regard. Quand le placement vous convient, cliquez avec le bouton gauche de la souris :

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-8.png)

Une fois que vous avez fini de tester la fonctionnalité en mode Game, cliquez avec le bouton droit sur l’objet Cube, puis sélectionnez **Delete** pour le supprimer de la scène :

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-9.png)

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez appris à utiliser le solveur Directional Indicator de MRTK pour qu’un élément de l’interface utilisateur dirige intuitivement l’utilisateur vers des objets. Vous avez aussi appris à utiliser le solveur Tap To Place pour repositionner facilement des objets.

Pour en savoir plus sur ces solveurs et sur d’autres solveurs fournis avec le MRTK, consultez le guide [Solveurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

[Tutoriel suivant : 6. Création d’interfaces utilisateur](mr-learning-base-06.md)
