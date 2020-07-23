---
title: Tutoriels de démarrage - 5. Création de contenu dynamique avec des solveurs
description: Ce cours vous montre comment utiliser Mixed Reality Toolkit (MRTK) pour créer une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: cbeaa8b65b7aecc0600294b3739fedfb903e568e
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86305718"
---
# <a name="5-creating-dynamic-content-using-solvers"></a><span data-ttu-id="7c911-105">5. Création de contenu dynamique avec des solveurs</span><span class="sxs-lookup"><span data-stu-id="7c911-105">5. Creating dynamic content using Solvers</span></span>

## <a name="overview"></a><span data-ttu-id="7c911-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="7c911-106">Overview</span></span>

<span data-ttu-id="7c911-107">Dans ce tutoriel, vous allez explorer différentes façons de placer dynamiquement des hologrammes à l’aide des outils de placement fournis dans le MRTK, appelés « solveurs », pour résoudre des scénarios de placement spatial complexes.</span><span class="sxs-lookup"><span data-stu-id="7c911-107">In this tutorial, you will explore ways to dynamically place holograms using the MRTK's available placement tools, known as Solvers, to solve complex spatial placement scenarios.</span></span> <span data-ttu-id="7c911-108">Dans MRTK, les solveurs sont un système de scripts et de comportements utilisés pour permettre aux objets de suivre l’utilisateur (vous) ou d’autres objets de jeu dans la scène.</span><span class="sxs-lookup"><span data-stu-id="7c911-108">In the MRTK, Solvers are a system of scripts and behaviors used to allow objects to follow you, the user, or other game objects in the scene.</span></span> <span data-ttu-id="7c911-109">Ils peuvent aussi être utilisés pour l’alignement sur certaines positions, rendant votre application plus intuitive.</span><span class="sxs-lookup"><span data-stu-id="7c911-109">They can also be used to snap to certain positions, making your app more intuitive.</span></span>

## <a name="objectives"></a><span data-ttu-id="7c911-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="7c911-110">Objectives</span></span>

* <span data-ttu-id="7c911-111">Introduire les solveurs du MRTK</span><span class="sxs-lookup"><span data-stu-id="7c911-111">Introduce the MRTK's Solvers</span></span>
* <span data-ttu-id="7c911-112">Apprendre à utiliser des solveurs pour diriger l’utilisateur vers des objets</span><span class="sxs-lookup"><span data-stu-id="7c911-112">Learn how to use Solvers to direct the user to objects</span></span>
* <span data-ttu-id="7c911-113">Apprendre à utiliser des solveurs pour repositionner des objets</span><span class="sxs-lookup"><span data-stu-id="7c911-113">Learn how to use Solvers to reposition objects</span></span>

## <a name="location-of-solvers-in-the-mrtk"></a><span data-ttu-id="7c911-114">Emplacement des solveurs dans le MRTK</span><span class="sxs-lookup"><span data-stu-id="7c911-114">Location of Solvers in the MRTK</span></span>

 <span data-ttu-id="7c911-115">Les solveurs du MRTK se trouvent dans le dossier du SDK MRTK.</span><span class="sxs-lookup"><span data-stu-id="7c911-115">The MRTK's Solvers are located in the MRTK SDK folder.</span></span> <span data-ttu-id="7c911-116">Pour voir les solveurs disponibles dans votre projet, dans la fenêtre Project, accédez à **Assets** > **MRTK** > **SDK** > **Features** > **Utilities** > **Solvers** :</span><span class="sxs-lookup"><span data-stu-id="7c911-116">To see the available Solvers in your project, in the Project window, navigate to **Assets** > **MRTK** > **SDK** > **Features** > **Utilities** > **Solvers**:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section1-step1-1.png)

<span data-ttu-id="7c911-118">Dans ce tutoriel, nous allons passer en revue l’implémentation du solveur Directional Indicator et Tap To Place.</span><span class="sxs-lookup"><span data-stu-id="7c911-118">In this tutorial, we will review the implementation of the Directional Indicator Solver and the Tap To Place Solver.</span></span> <span data-ttu-id="7c911-119">Pour en savoir plus sur l’ensemble des solveurs disponibles dans MRTK, consultez le guide [Solveurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="7c911-119">To learn more about the full range of Solvers available in the MRTK, you can refer to the [Solvers](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

> [!NOTE]
> <span data-ttu-id="7c911-120">Le solveur Directional Indicator ne se trouve pas dans les dossiers des solveurs référencés ci-dessus, mais dans les dossiers Assets > MRTK > SDK > Experimental > Features > Utilities, car il s’agit d’une fonctionnalité expérimentale.</span><span class="sxs-lookup"><span data-stu-id="7c911-120">The Directional Indicator Solver is not located in the Solvers folders referenced above, but in the Assets > MRTK > SDK > Experimental > Features > Utilities folders, because it is an experimental feature.</span></span>

## <a name="using-the-directional-indicator-solver-to-direct-the-user-to-objects"></a><span data-ttu-id="7c911-121">Utilisation du solveur Directional Indicator pour diriger l’utilisateur vers des objets</span><span class="sxs-lookup"><span data-stu-id="7c911-121">Using the Directional Indicator Solver to direct the user to objects</span></span>

<span data-ttu-id="7c911-122">Dans la fenêtre Project, accédez au dossier à la **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs**, cliquez et faites glisser le préfabriqué **Chevron** dans la fenêtre Hierarchy et définissez sa **Position** de transformation sur X = 0, Y = 0, Z = 2 pour le positionner à proximité de l’objet RoverExplorer :</span><span class="sxs-lookup"><span data-stu-id="7c911-122">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** folder, click-and-drag the **Chevron** prefab into the Hierarchy window, and set it's Transform **Position** to X = 0, Y = 0, Z = 2 to position it near the RoverExplorer object:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section2-step1-1.png)

> [!TIP]
> <span data-ttu-id="7c911-124">Si vous constatez que l’appareil photo ou d’autres icônes de votre scène masquent les objets ou gênent, vous pouvez les masquer en <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">basculant les Gizmos</a> sur la position désactivé, comme illustré dans l’image ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7c911-124">If you find that the camera or any other icons in your scene are hiding the objects or are distracting, you can hide these by <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">toggling the Gizmos</a> to the off position, as shown in the image above.</span></span> <span data-ttu-id="7c911-125">Pour en savoir plus sur le menu Gizmos et sur la façon dont vous pouvez l’utiliser pour optimiser votre vue Scene, consultez la page consacrée au <a href="https://docs.unity3d.com/Manual/GizmosMenu.html" target="_blank">menu Gizmos</a> dans la documentation Unity.</span><span class="sxs-lookup"><span data-stu-id="7c911-125">To learn more about the Gizmos menu and how you can use it to optimize your scene view, you can refer to Unity's <a href="https://docs.unity3d.com/Manual/GizmosMenu.html" target="_blank">Gizmos menu</a> documentation.</span></span>

<span data-ttu-id="7c911-126">Renommez l’objet **Indicator** de Chevron qui vient d’être ajouté puis, dans la fenêtre Inspector, utilisez le bouton **Ajouter un composant** pour ajouter les composants **DirectionalIndicator** et **Directional Indicator Controller (Script)**  :</span><span class="sxs-lookup"><span data-stu-id="7c911-126">Rename the newly added Chevron object **Indicator**, then in the Inspector window, use the **Add Component** button to add the **DirectionalIndicator** and the **Directional Indicator Controller (Script)** component:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section2-step1-2.png)

> [!NOTE]
> <span data-ttu-id="7c911-128">Quand vous ajoutez un solveur, dans ce cas le composant DirectionalIndicator, le composant SolverHandler est ajouté automatiquement car les solveurs en ont besoin.</span><span class="sxs-lookup"><span data-stu-id="7c911-128">When you add a Solver, in this case, the DirectionalIndicator component, the SolverHandler component is automatically added because Solvers require it.</span></span>

> [!NOTE]
> <span data-ttu-id="7c911-129">Directional Indicator Controller (Script) ne fait pas partie du MRTK, mais il a été inclus avec les ressources du tutoriel.</span><span class="sxs-lookup"><span data-stu-id="7c911-129">The Directional Indicator Controller (Script) is not part of the MRTK but was included with the tutorial assets.</span></span>

<span data-ttu-id="7c911-130">Configurez les composants DirectionalIndicator et SolverHandler comme suit :</span><span class="sxs-lookup"><span data-stu-id="7c911-130">Configure the DirectionalIndicator and SolverHandler components as follows:</span></span>

* <span data-ttu-id="7c911-131">Vérifiez que la propriété **Tracked Target Type** du composant **SolverHandler** est définis sur **Head**.</span><span class="sxs-lookup"><span data-stu-id="7c911-131">Verify that the **SolverHandler** component's **Tracked Target Type** is set to **Head**</span></span>
* <span data-ttu-id="7c911-132">Affectez le **RoverExplorer** à la **Directional Target** du composant **DirectionalIndicator**  en le faisant glisser de la fenêtre Hierarchy vers le champ **None (Transform)** .</span><span class="sxs-lookup"><span data-stu-id="7c911-132">Assign the **RoverExplorer** to the **DirectionalIndicator** component's **Directional Target** by dragging it from the Hierarchy window into the **None (Transform)** field</span></span>
* <span data-ttu-id="7c911-133">Changez la valeur de **View Offset** en 0,2</span><span class="sxs-lookup"><span data-stu-id="7c911-133">Change the **View Offset** to 0.2</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section2-step1-3.png)

<span data-ttu-id="7c911-135">Appuyez sur le bouton de lecture pour passer en mode Game, appuyez sur le bouton droit de la souris et maintenez-le enfoncé tout en déplaçant votre souris vers la droite ou la gauche pour faire pivoter la direction de votre regard, et notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="7c911-135">Press the Play button to enter Game mode, press-and-hold the right mouse button while moving your mouse to the left or right to rotate your gaze direction, and notice the following:</span></span>

* <span data-ttu-id="7c911-136">Quand vous détachez votre regard de l’objet RoverExplorer, l’objet Indicator apparaît et pointe vers l’objet RoverExplorer</span><span class="sxs-lookup"><span data-stu-id="7c911-136">When you look away from the RoverExplorer object, the Indicator object will appear and point towards the RoverExplorer object</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section2-step1-4.png)

> [!NOTE]
> <span data-ttu-id="7c911-138">Si vous ne voyez pas le rayon de la caméra dans votre fenêtre Scene, vérifiez que votre menu Gizmos est activé, comme illustré dans l’image ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7c911-138">If you don't see the camera ray in your Scene window, make sure your Gizmos menu is enabled, as shown in the image above.</span></span>

> [!TIP]
> <span data-ttu-id="7c911-139">Pour découvrir comment utiliser la simulation d’entrée dans l’éditeur, consultez le guide [Utilisation de la simulation d’entrée avec les mains dans l’éditeur pour tester une scène](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="7c911-139">To learn how to use the in-editor input simulation, you can refer to the [Using the In-Editor Hand Input Simulation to test a scene](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

> [!TIP]
> <span data-ttu-id="7c911-140">Si votre ordinateur dispose d’un microphone, vous pouvez facilement basculer l’état actif du volet Diagnostics qui apparaît dans la fenêtre Game avec la commande vocale « toggle diagnostics ».</span><span class="sxs-lookup"><span data-stu-id="7c911-140">If your computer has a microphone, you can easily toggle the active state of the Diagnostics panel that appears in the Game window by using the speech command "toggle diagnostics."</span></span> <span data-ttu-id="7c911-141">Vous pouvez aussi le désactiver dans MRTK Configuration Profile > Diagnostics > Enable Diagnostics System.</span><span class="sxs-lookup"><span data-stu-id="7c911-141">Alternatively, you can disable it in the MRTK Configuration Profile > Diagnostics > Enable Diagnostics System.</span></span> <span data-ttu-id="7c911-142">D’une façon générale, il est cependant recommandé de conserver Diagnostics System actif pendant le développement.</span><span class="sxs-lookup"><span data-stu-id="7c911-142">However, it is generally recommended to keep the Diagnostics System active during development.</span></span>

## <a name="using-the-tap-to-place-solver-to-reposition-objects"></a><span data-ttu-id="7c911-143">Utilisation du solveur Tap to Place pour repositionner des objets</span><span class="sxs-lookup"><span data-stu-id="7c911-143">Using the Tap to Place Solver to reposition objects</span></span>

<span data-ttu-id="7c911-144">Dans la fenêtre Hierarchy, sélectionnez l’objet RoverExplorer > **RoverAssembly** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Tap To Place (Script)** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="7c911-144">In the Hierarchy window, select the RoverExplorer > **RoverAssembly** object, then in the Inspector window, use the **Add Component** button to add the **Tap To Place (Script)** component, and configure it as follows:</span></span>

* <span data-ttu-id="7c911-145">Vérifiez que la propriété **Tracked Target Type** du composant **SolverHandler** est définis sur **Head**.</span><span class="sxs-lookup"><span data-stu-id="7c911-145">Verify that the **SolverHandler** component's **Tracked Target Type** is set to **Head**</span></span>
* <span data-ttu-id="7c911-146">Cochez la case **Keep Orientation Vertical**.</span><span class="sxs-lookup"><span data-stu-id="7c911-146">Check the **Keep Orientation Vertical** checkbox</span></span>
* <span data-ttu-id="7c911-147">Dans la liste déroulante **Magnetic Surfaces** > **Element 0**, décochez toutes les options sauf **Spatial Awareness**.</span><span class="sxs-lookup"><span data-stu-id="7c911-147">From the **Magnetic Surfaces** > **Element 0** dropdown, uncheck all options expect **Spatial Awareness**</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-1.png)

> [!NOTE]
> <span data-ttu-id="7c911-149">Le paramètre Magnetic Surfaces détermine les objets que le composant Tap To Place (Script) peut détecter lors du placement d’un objet.</span><span class="sxs-lookup"><span data-stu-id="7c911-149">The Magnetic Surfaces setting determines which objects the Tap To Place (Script) component can detect when placing an object.</span></span> <span data-ttu-id="7c911-150">Si vous changez le paramètre pour activer seulement Spatial Awareness, le composant Tap To Place (Script) pourra placer le Rover seulement sur les objets de la couche Unity nommée Spatial Awareness qui est par défaut le maillage de la reconnaissance spatiale généré par HoloLens.</span><span class="sxs-lookup"><span data-stu-id="7c911-150">By changing the setting to only Spatial Awareness, the Tap To Place (Script) component will only be able to place the Rover on objects on the Unity Layer named Spatial Awareness, which by default is the Spatial Awareness Mesh generated by the HoloLens.</span></span>
>
><span data-ttu-id="7c911-151">Pour en savoir plus sur les couches, reportez-vous à la documentation <a href="https://docs.unity3d.com/Manual/Layers.html" target="_blank">Couches</a> d’Unity.</span><span class="sxs-lookup"><span data-stu-id="7c911-151">To learn more about Layers, you can refer to Unity's <a href="https://docs.unity3d.com/Manual/Layers.html" target="_blank">Layers</a> documentation.</span></span>

> [!TIP]
> <span data-ttu-id="7c911-152">Si vous voulez voir le maillage de la reconnaissance spatiale lors du test de la fonctionnalité Tap to Place sur votre HoloLens, vous pouvez définir temporairement la propriété Display Option du Spatial Mesh Observer sur Visible.</span><span class="sxs-lookup"><span data-stu-id="7c911-152">If you want to see the Spatial Awareness Mesh when testing the Tap To Place functionality on your HoloLens, you can temporarily set the Spatial Mesh Observer's Display Option to Visible.</span></span> <span data-ttu-id="7c911-153">Pour vous rappeler comment changer l’option d’affichage, reportez-vous aux instructions de [Changer l’option d’affichage de la reconnaissance spatiale](mr-learning-base-03.md#changing-the-spatial-awareness-display-option).</span><span class="sxs-lookup"><span data-stu-id="7c911-153">For a reminder on how to change the Display Option, you can refer to the [Changing the Spatial Awareness Display Option](mr-learning-base-03.md#changing-the-spatial-awareness-display-option) instructions.</span></span>

<span data-ttu-id="7c911-154">Avec l’objet RoverAssembly toujours sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, recherchez l’événement **On Placing Started ()** puis cliquez sur l’icône **+** pour ajouter un nouvel événement :</span><span class="sxs-lookup"><span data-stu-id="7c911-154">With the RoverAssembly object still selected in the Hierarchy window, in the Inspector window, locate the **On Placing Started ()** event and click the **+** icon to add a new event:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-2.png)

<span data-ttu-id="7c911-156">Configurez l’événement comme suit :</span><span class="sxs-lookup"><span data-stu-id="7c911-156">Configure the event as follows:</span></span>

* <span data-ttu-id="7c911-157">Affectez l’objet **RoverAssembly** en tant qu’écouteur pour l’événement On Placing Started () en le faisant glisser de la fenêtre Hierarchy dans le champ **None (Object)**</span><span class="sxs-lookup"><span data-stu-id="7c911-157">Assign the **RoverAssembly** object as a listener for the On Placing Started () event by dragging it from the Hierarchy window into the **None (Object)** field</span></span>
* <span data-ttu-id="7c911-158">Dans la liste déroulante **No Function**, sélectionnez **TapToPlace** > **float SurfaceNormalOffset** pour mettre à jour la valeur de la propriété SurfaceNormalOffset quand l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="7c911-158">From the **No Function** dropdown, select **TapToPlace** > **float SurfaceNormalOffset** to update the SurfaceNormalOffset property value when the event is triggered</span></span>
* <span data-ttu-id="7c911-159">Vérifiez que l’argument est défini sur **0**</span><span class="sxs-lookup"><span data-stu-id="7c911-159">Verify that the argument is set to **0**</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-3.png)

<span data-ttu-id="7c911-161">Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur une zone vide, sélectionnez **3D Object** > **Cube** pour créer un objet temporaire représentant le sol, puis configurez le composant **Transform** comme suit :</span><span class="sxs-lookup"><span data-stu-id="7c911-161">In the Hierarchy window, right-click on an empty spot and select **3D Object** > **Cube**, to create a temporary object representing the ground, and configure the **Transform** component as follows:</span></span>

* <span data-ttu-id="7c911-162">**Position** : X = 0, Y = -1,65, Z = 6</span><span class="sxs-lookup"><span data-stu-id="7c911-162">**Position**: X = 0, Y = -1.65, Z = 6</span></span>
* <span data-ttu-id="7c911-163">**Rotation** : X = 0, Y = 0, Z = 0</span><span class="sxs-lookup"><span data-stu-id="7c911-163">**Rotation**: X = 0, Y = 0, Z = 0</span></span>
* <span data-ttu-id="7c911-164">**Scale** : X = 10, Y = 0,2, Z = 10</span><span class="sxs-lookup"><span data-stu-id="7c911-164">**Scale**: X = 10, Y = 0.2, Z = 10</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-4.png)

<span data-ttu-id="7c911-166">Le cube temporaire étant toujours sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, utilisez la liste déroulante **Couches** pour changer le paramètre Layer du cube de façon à inclure seulement la couche **Spatial Awareness** :</span><span class="sxs-lookup"><span data-stu-id="7c911-166">With the temporary Cube still selected in the Hierarchy window, in the Inspector window, use the **Layers** dropdown to change the Cube's Layer setting only to include the **Spatial Awareness** layer:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-5.png)

<span data-ttu-id="7c911-168">Appuyez sur le bouton Play pour passer en mode Game. Ensuite, maintenez enfoncé le bouton droit de la souris tout en déplaçant la souris vers le bas jusqu’à ce que le regard atteigne l’objet RoverAssembly :</span><span class="sxs-lookup"><span data-stu-id="7c911-168">Press the Play button to enter Game mode, then press-and-hold the right mouse button while moving your mouse down until the gaze hit's the RoverAssembly object:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-6.png)

<span data-ttu-id="7c911-170">Cliquez avec le bouton gauche de la souris pour démarrer le processus de Tap to Place :</span><span class="sxs-lookup"><span data-stu-id="7c911-170">Click the left mouse button to start the tap-to-place process:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-7.png)

<span data-ttu-id="7c911-172">Appuyez sur le bouton droit de la souris et maintenez-le enfoncé tout en déplaçant votre souris vers la droite ou la gauche pour faire pivoter la direction de votre regard. Quand le placement vous convient, cliquez avec le bouton gauche de la souris :</span><span class="sxs-lookup"><span data-stu-id="7c911-172">Press-and-hold the right mouse button while moving your mouse to the left or right to rotate your gaze direction, when you are happy with the placement, click the left mouse button:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-8.png)

<span data-ttu-id="7c911-174">Une fois que vous avez fini de tester la fonctionnalité en mode Game, cliquez avec le bouton droit sur l’objet Cube, puis sélectionnez **Delete** pour le supprimer de la scène :</span><span class="sxs-lookup"><span data-stu-id="7c911-174">Once you are done testing the feature in the Game mode, right-click on the Cube object and select **Delete** to remove it from the scene:</span></span>

![mr-learning-base](images/mr-learning-base/base-05-section3-step1-9.png)

## <a name="congratulations"></a><span data-ttu-id="7c911-176">Félicitations</span><span class="sxs-lookup"><span data-stu-id="7c911-176">Congratulations</span></span>

<span data-ttu-id="7c911-177">Dans ce tutoriel, vous avez appris à utiliser le solveur Directional Indicator de MRTK pour qu’un élément de l’interface utilisateur dirige intuitivement l’utilisateur vers des objets.</span><span class="sxs-lookup"><span data-stu-id="7c911-177">In this tutorial, you learned how to use the MRTK's Directional Indicator Solver to have a UI element intuitively direct the user to objects.</span></span> <span data-ttu-id="7c911-178">Vous avez aussi appris à utiliser le solveur Tap To Place pour repositionner facilement des objets.</span><span class="sxs-lookup"><span data-stu-id="7c911-178">You also learned how to use the Tap To Place Solver to reposition objects easily.</span></span>

<span data-ttu-id="7c911-179">Pour en savoir plus sur ces solveurs et sur d’autres solveurs fournis avec le MRTK, consultez le guide [Solveurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="7c911-179">To learn more about these and other solvers included with the MRTK,  you can refer to the [Solvers](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

[<span data-ttu-id="7c911-180">Tutoriel suivant : 6. Création d’interfaces utilisateur</span><span class="sxs-lookup"><span data-stu-id="7c911-180">Next Tutorial: 6. Creating user interfaces</span></span>](mr-learning-base-06.md)
