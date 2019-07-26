---
title: Prise en main de MRTK version 2
description: Pour les nouveaux développeurs qui souhaitent tirer parti de MRTK
author: Yoyoz
ms.author: Yoyoz
ms.date: 05/15/19
ms.topic: article
keywords: Windows Mixed Reality, test, kit de développement logiciel (SDK) de réalité mixte, MRTK version 2, MRTK, Tools, SDK, HoloLens, HoloLens 2
ms.openlocfilehash: 7eded2c766765a5ccebf741eed2f8b7fe8f65a93
ms.sourcegitcommit: 76a7aa6e64e114b63ace058dd6d6d662b3c9f09e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68507932"
---
# <a name="getting-started-with-mrtk-v2"></a><span data-ttu-id="6a9b6-104">Prise en main de MRTK v2</span><span class="sxs-lookup"><span data-stu-id="6a9b6-104">Getting started with MRTK v2</span></span>

## <a name="mrtk-getting-started-guide"></a><span data-ttu-id="6a9b6-105">Guide de Prise en main MRTK</span><span class="sxs-lookup"><span data-stu-id="6a9b6-105">MRTK Getting Started Guide</span></span>
<span data-ttu-id="6a9b6-106">Pour plus d’informations sur la prise en main de MRTK v2, consultez le [Guide de prise](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html) en main de MRTK.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-106">See the [MRTK getting started guide](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html) for information on getting started with MRTK V2.</span></span>

## <a name="what-is-mixed-reality-toolkit-mrtk"></a><span data-ttu-id="6a9b6-107">Qu’est-ce que Mixed Reality Toolkit (MRTK)?</span><span class="sxs-lookup"><span data-stu-id="6a9b6-107">What is Mixed Reality Toolkit (MRTK)?</span></span>
<span data-ttu-id="6a9b6-108">Le MRTK est une boîte à outils open source incroyable qui existe depuis la sortie de HoloLens, et n’est pas là où elle se trouvait aujourd’hui sans le travail difficile de notre communauté de développeurs qui lui a contribué.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-108">The MRTK is an amazing open source toolkit that has been around since the HoloLens was first released, and would not be where it is today without the hard work of our developer community who have contributed to it.</span></span> <span data-ttu-id="6a9b6-109">Au cours des trois dernières années, nous avons écouté les commentaires de notre communauté de développeurs et créé MRTK v2 pour prendre en compte les plus grands problèmes.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-109">Over the past 3 years, we have listened to the feedback of our developer community, and built MRTK v2 to take the biggest concerns into account.</span></span>  

<span data-ttu-id="6a9b6-110">MRTK v2 avec Unity est un kit de développement multiplateforme Open source pour les applications de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-110">The MRTK v2 with Unity is an open source cross-platform development kit for mixed reality applications.</span></span>  <span data-ttu-id="6a9b6-111">MRTK version 2 a pour objectif d’accélérer le développement d’applications ciblant Microsoft HoloLens, les casques Windows Mixed Reality (VR) et la plate-forme OpenVR.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-111">MRTK version 2 is intended to accelerate development of applications targeting Microsoft HoloLens, Windows Mixed Reality immersive (VR) headsets and OpenVR platform.</span></span> <span data-ttu-id="6a9b6-112">Le projet a pour but de réduire le nombre d’obstacles qui gênent la création d’applications de réalité mixte et d’apporter une contribution à la Communauté de la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-112">The project is aimed at reducing barriers to entry to create mixed reality applications and contribute back to the community as we all grow.</span></span> 


<span data-ttu-id="6a9b6-113">Pour en savoir plus, consultez le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html) .</span><span class="sxs-lookup"><span data-stu-id="6a9b6-113">See the [MRTK documentation portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html) to learn more.</span></span>

## <a name="feature-areas"></a><span data-ttu-id="6a9b6-114">Domaines de fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="6a9b6-114">Feature areas</span></span>

:::row:::
    :::column:::
    <img src="images/MRTK_Icon_InputSystem.png" alt="Input system" title="Système d’entrée" width="105"> <span data-ttu-id="6a9b6-116">Système d’entrée</span><span class="sxs-lookup"><span data-stu-id="6a9b6-116">Input System</span></span> 
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_HandTracking.png" alt="Hand Tracking (HoloLens 2)" title="Suivi des mains (HoloLens 2)" width="105"> <span data-ttu-id="6a9b6-118">Suivi des mains (HoloLens 2)</span><span class="sxs-lookup"><span data-stu-id="6a9b6-118">Hand Tracking (HoloLens 2)</span></span>
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_EyeTracking.png" alt="Eye Tracking (HoloLens 2)" title="Suivi des yeux (HoloLens 2)" width="105">
    <span data-ttu-id="6a9b6-120">Suivi des yeux (HoloLens 2)</span><span class="sxs-lookup"><span data-stu-id="6a9b6-120">Eye Tracking (HoloLens 2)</span></span>
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_VoiceCommand.png" alt="Voice Commanding" title="Commandes vocales" width="105"> <span data-ttu-id="6a9b6-122">Commandes vocales</span><span class="sxs-lookup"><span data-stu-id="6a9b6-122">Voice Commanding</span></span>
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_GazeSelect.png" alt="Gaze + Select (HoloLens (1st gen))" title="Point d' + sélectionner (HoloLens (1re génération))" width="105">
    <span data-ttu-id="6a9b6-124">Point d' + sélectionner (HoloLens (1re génération))</span><span class="sxs-lookup"><span data-stu-id="6a9b6-124">Gaze + Select (HoloLens (1st gen))</span></span>
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_Teleportation.png" alt="Teleportation" title="Téléportation" width="105"> <span data-ttu-id="6a9b6-126">Téléportation</span><span class="sxs-lookup"><span data-stu-id="6a9b6-126">Teleportation</span></span>
    :::column-end:::
:::row-end:::


:::row:::
    :::column:::
    <img src="images/MRTK_Icon_UIControls.png" alt="UI Controls" title="Contrôles d’interface utilisateur" width="105"> <span data-ttu-id="6a9b6-128">Contrôles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="6a9b6-128">UI Controls</span></span>
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_Solver.png" alt="Solver and Interactions" title="Solveur et interactions" width="105"> <span data-ttu-id="6a9b6-130">Solveur et interactions</span><span class="sxs-lookup"><span data-stu-id="6a9b6-130">Solver and Interactions</span></span>
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_ControllerVisualization.png" alt="Controller Visualization" title="Visualisation du contrôleur" width="105"> <span data-ttu-id="6a9b6-132">Visualisation du contrôleur</span><span class="sxs-lookup"><span data-stu-id="6a9b6-132">Controller Visualization</span></span>
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_SpatialUnderstanding.png" alt="Spatial Understanding" title="Compréhension spatiale" width="105"> <span data-ttu-id="6a9b6-134">Compréhension spatiale</span><span class="sxs-lookup"><span data-stu-id="6a9b6-134">Spatial Understanding</span></span>
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_Diagnostics.png" alt="Diagnostic Tool" title="Outil de diagnostic" width="105"> <span data-ttu-id="6a9b6-136">Outil de diagnostic</span><span class="sxs-lookup"><span data-stu-id="6a9b6-136">Diagnostic Tool</span></span>
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_StandardShader.png" alt="MRTK Standard Shader" title="Nuanceur standard MRTK" width="105"> <span data-ttu-id="6a9b6-138">Nuanceur standard MRTK</span><span class="sxs-lookup"><span data-stu-id="6a9b6-138">MRTK Standard Shader</span></span>
    :::column-end:::
:::row-end:::

## <a name="ui-and-interaction-building-blocks"></a><span data-ttu-id="6a9b6-139">Blocs de construction interface utilisateur et interaction</span><span class="sxs-lookup"><span data-stu-id="6a9b6-139">UI and Interaction Building blocks</span></span>

:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html"><img src="images/MRTK_Button_Main.png" alt="Button" title="Bouton" width="250"><br>
    <span data-ttu-id="6a9b6-141">**Button**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-141">**Button**</span></span><br>
    <span data-ttu-id="6a9b6-142">Contrôle de bouton qui prend en charge différentes méthodes d’entrée, y compris la main articulée de HoloLens 2<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-142">A button control which supports various input methods including HoloLens 2's articulated hand <a/></span></span>
    :::column-end:::
    :::column:::
<a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html"><img src="images/MRTK_BoundingBox_Main.png" alt="Bounding Box" title="Cadre englobant" width="250"><br>
    <span data-ttu-id="6a9b6-144">**Cadre englobant**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-144">**Bounding Box**</span></span><br>
    <span data-ttu-id="6a9b6-145">Interface utilisateur standard pour manipuler des objets dans l’espace 3D<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-145">Standard UI for manipulating objects in 3D space <a/></span></span>
    :::column-end:::
    :::column:::
<a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html"><img src="images/MRTK_Manipulation_Main.png" alt="Manipulation Handler" title="Gestionnaire de manipulation" width="250"><br>
    <span data-ttu-id="6a9b6-147">**Gestionnaire de manipulation**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-147">**Manipulation Handler**</span></span><br>
    <span data-ttu-id="6a9b6-148">Script de manipulation d’objets avec une ou deux mains<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-148">Script for manipulating objects with one or two hands <a/></span></span>
    :::column-end:::
:::row-end:::    
    
:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Slate.html"><img src="images/MRTK_Slate_Main.png" alt="Slate" title="Médias" width="250"><br>
    <span data-ttu-id="6a9b6-150">**Médias**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-150">**Slate**</span></span> <br>
    <span data-ttu-id="6a9b6-151">plan de style 2D qui prend en charge le défilement avec une entrée articulée<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-151">2D style plane which supports scrolling with articulated hand input <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_SystemKeyboard.html"><img src="images/MRTK_SystemKeyboard_Main.png" alt="System Keyboard" title="Clavier système" width="250"><br>
    <span data-ttu-id="6a9b6-153">**Clavier système**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-153">**System Keyboard**</span></span><br>
    <span data-ttu-id="6a9b6-154">Exemple de script d’utilisation du clavier système dans Unity<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-154">Example script of using the system keyboard in Unity <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html"><img src="images/InteractableExamples.png" alt="Interactable" title="Sur" width="250"><br>
     <span data-ttu-id="6a9b6-156">**Sur**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-156">**Interactable**</span></span> <br>
     <span data-ttu-id="6a9b6-157">Script permettant de rendre les objets interactifs avec les États visuels et la prise en charge des thèmes<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-157">A script for making objects interactable with visual states and theme support <a/></span></span>
    :::column-end:::
:::row-end:::       

:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html"><img src="images/MRTK_Solver_Main.png" alt="Solver" title="Solveur" width="250"><br>
    <span data-ttu-id="6a9b6-159">**Solveur**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-159">**Solver**</span></span> <br>
    <span data-ttu-id="6a9b6-160">Différents comportements de positionnement des objets, tels que balise, verrouillage de corps, taille de vue constante et magnétisme de surface<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-160">Various object positioning behaviors such as tag-along, body-lock, constant view size and surface magnetism <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html"><img src="images/MRTK_ObjectCollection_Main.png" alt="Object Collection" title="Collection d’objets" width="250"><br>
    <span data-ttu-id="6a9b6-162">**Collection d’objets**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-162">**Object Collection**</span></span><br>
    <span data-ttu-id="6a9b6-163">Script pour disposer un tableau d’objets dans une forme en trois dimensions<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-163">Script for lay out an array of objects in a three-dimensional shape <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Tooltip.html"><img src="images/MRTK_Tooltip_Main.png" alt="Tooltip" title="Info-bulle" width="250">  <br>
    <span data-ttu-id="6a9b6-165">**Bulle**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-165">**Tooltip**</span></span><br>
    <span data-ttu-id="6a9b6-166">Interface utilisateur d’annotation avec système d’ancrage/pivot flexible qui peut être utilisé pour étiqueter les contrôleurs de mouvement et les objets<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-166">Annotation UI with flexible anchor/pivot system which can be used for labeling motion controllers and object <a/></span></span>
    :::column-end:::
:::row-end:::   
        
:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html"><img src="images/MRTK_AppBar_Main.png" alt="App Bar" title="Barre de l’application" width="250"><br>
    <span data-ttu-id="6a9b6-168">**Barre de l’application**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-168">**App Bar**</span></span><br>
    <span data-ttu-id="6a9b6-169">Interface utilisateur pour l’activation manuelle du cadre englobant<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-169">UI for Bounding Box's manual activation <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Pointers.html"><img src="images/MRTK_Pointer_Main.png" alt="Pointers" title="Pointeurs" width="250"><br>
    <span data-ttu-id="6a9b6-171">**Pointeurs**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-171">**Pointers**</span></span><br>
    <span data-ttu-id="6a9b6-172">En savoir plus sur les différents types de pointeurs<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-172">Learn about various types of pointers <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_FingertipVisualization.html"><img src="images/MRTK_FingertipVisualization_Main.png" alt="Fingertip Visualization" title="Visualisation de portée" width="250"><br>
     <span data-ttu-id="6a9b6-174">**Visualisation de portée**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-174">**Fingertip Visualization**</span></span><br>
     <span data-ttu-id="6a9b6-175">Visuel à portée de main, ce qui améliore la confiance pour l’interaction directe<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-175">Visual affordance on the fingertip which improves the confidence for the direct interaction <a/></span></span>
    :::column-end:::
:::row-end:::   

:::row:::
    :::column:::
    <a href="https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_Sliders.md"><img src="images/MRTK_UX_Slider_Main.jpg" alt="Slider" title="Curseur" width="250"><br>
    <span data-ttu-id="6a9b6-177">**Slider**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-177">**Slider**</span></span><br>
    <span data-ttu-id="6a9b6-178">Interface utilisateur du curseur pour l’ajustement des valeurs prenant en charge l’interaction de suivi direct<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-178">Slider UI for adjusting values supporting direct hand tracking interaction <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_MRTKStandardShader.md"><img src="images/MRTK_StandardShader.jpg" alt="MRTK Standard Shader" title="Nuanceur standard MRTK" width="250"><br>
    <span data-ttu-id="6a9b6-180">**Nuanceur standard MRTK**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-180">**MRTK Standard Shader**</span></span><br>
    <span data-ttu-id="6a9b6-181">Le nuanceur standard de MRTK prend en charge différents éléments de conception Fluent avec des performances<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-181">MRTK's Standard shader supports various Fluent design elements with performance <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_HandJointChaser.md"><img src="images/MRTK_HandJointChaser_Main.jpg" alt="Hand Joint Chaser" title="Chase joint à la main" width="250"><br>
     <span data-ttu-id="6a9b6-183">**Chase joint à la main**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-183">**Hand Joint Chaser**</span></span><br>
     <span data-ttu-id="6a9b6-184">Montre comment utiliser le solveur pour attacher des objets aux jointures de la main<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-184">Demonstrates how to use Solver to attach objects to the hand joints <a/></span></span>
    :::column-end:::
:::row-end:::   
        
:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html"><img src="images/mrtk_et_targetselect.png" alt="Eye Tracking: Target Selection" title="Suivi des yeux: Sélection de la cible" width="250"><br>
    <span data-ttu-id="6a9b6-186">**Suivi des yeux: Sélection de la cible**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-186">**Eye Tracking: Target Selection**</span></span><br>
    <span data-ttu-id="6a9b6-187">Combiner les yeux, la voix et la main pour sélectionner rapidement et facilement des hologrammes sur votre scène<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-187">Combine eyes, voice and hand input to quickly and effortlessly select holograms across your scene <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html"><img src="images/mrtk_et_navigation.png" alt="Eye Tracking: Navigation" title="Suivi des yeux: Navigation" width="250"><br>
    <span data-ttu-id="6a9b6-189">**Suivi des yeux: Déplacement**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-189">**Eye Tracking: Navigation**</span></span><br>
    <span data-ttu-id="6a9b6-190">Apprenez à faire défiler automatiquement le texte ou à faire un zoom sur le contenu ciblé en fonction de ce que vous cherchez<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-190">Learn how to auto scroll text or fluently zoom into focused content based on what you are looking at <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Visualization.html"><img src="images/mrtk_et_heatmaps.png" alt="Eye Tracking: Heat Map" title="Suivi des yeux: Carte thermique" width="250"><br>
    <span data-ttu-id="6a9b6-192">**Suivi des yeux: Carte thermique**</span><span class="sxs-lookup"><span data-stu-id="6a9b6-192">**Eye Tracking: Heat Map**</span></span><br>
    <span data-ttu-id="6a9b6-193">Exemples de journalisation, de chargement et de visualisation de ce que les utilisateurs ont examiné dans votre application<a/></span><span class="sxs-lookup"><span data-stu-id="6a9b6-193">Examples for logging, loading and visualizing what users have been looking at in your app <a/></span></span>
    :::column-end:::
:::row-end:::           


## <a name="minimum-requirement-for-mrtk-v2"></a><span data-ttu-id="6a9b6-194">Configuration minimale requise pour MRTK v2</span><span class="sxs-lookup"><span data-stu-id="6a9b6-194">Minimum Requirement for MRTK v2</span></span>
* <span data-ttu-id="6a9b6-195">Unity 2018.3.x</span><span class="sxs-lookup"><span data-stu-id="6a9b6-195">Unity 2018.3.x</span></span>
* <span data-ttu-id="6a9b6-196">Microsoft Visual Studio 2017 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="6a9b6-196">Microsoft Visual Studio 2017 or later</span></span>
* <span data-ttu-id="6a9b6-197">SDK Windows 18362 +</span><span class="sxs-lookup"><span data-stu-id="6a9b6-197">Windows SDK 18362+</span></span> 
* <span data-ttu-id="6a9b6-198">Windows 10 1803 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="6a9b6-198">Windows 10 1803 or later</span></span>

## <a name="new-with-mrtk-v2"></a><span data-ttu-id="6a9b6-199">Nouveautés avec MRTK v2</span><span class="sxs-lookup"><span data-stu-id="6a9b6-199">New with MRTK v2</span></span>
<span data-ttu-id="6a9b6-200">Nous souhaitons insister sur notre engagement envers ces outils de plateforme.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-200">We want to stress our commitment to these platform tools.</span></span>  <span data-ttu-id="6a9b6-201">En fait, nous avons utilisé MRTK version 2 pour développer nos expériences de boîte de réception, telles que l’expérience d’installation (OOBE) et notre application d’apprentissage de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-201">In fact, we leveraged MRTK version 2 to develop our inbox experiences, such as the setup experience (OOBE) and our Mixed Reality Learning application.</span></span>  <span data-ttu-id="6a9b6-202">Vous pouvez également vous attendre à voir les nouvelles fonctionnalités HoloLens 2 d’abord exposées par le biais de MRTK, car nous pensons qu’il s’agit de la meilleure façon de développer sur notre plateforme.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-202">You can also expect to see new HoloLens 2 capabilities first exposed through MRTK because we believe it’s the best way to develop on our platform.</span></span> 

### <a name="modular"></a><span data-ttu-id="6a9b6-203">ADAPT</span><span class="sxs-lookup"><span data-stu-id="6a9b6-203">Modular</span></span>
<span data-ttu-id="6a9b6-204">Nous l’avons créé de manière modulaire, ce qui vous permet de ne pas avoir à prendre chaque partie de la boîte à outils dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-204">We have built it in a modular way, so that you do not need to take every bit of the toolkit into your project.</span></span>  <span data-ttu-id="6a9b6-205">Il y en a en fait quelques avantages.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-205">There are actually a few benefits to this.</span></span>  <span data-ttu-id="6a9b6-206">Il permet de réduire la taille de votre projet et de le rendre plus facile à gérer.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-206">It keeps your project size smaller, as well as makes it easier to manage.</span></span>  <span data-ttu-id="6a9b6-207">En plus de cela, étant donné qu’elle est générée avec des objets scriptables et qu’elle est pilotée par interface, il est également possible de remplacer les composants qui sont inclus avec le vôtre, pour prendre en charge d’autres services, systèmes et plateformes.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-207">On top of that, because it’s built with scriptable objects and is interface driven, it’s also possible for you to replace the components that are included with your own, to support other services, systems, and platforms.</span></span>


### <a name="cross-platform"></a><span data-ttu-id="6a9b6-208">Système multiplateforme</span><span class="sxs-lookup"><span data-stu-id="6a9b6-208">Cross-platform</span></span>
<span data-ttu-id="6a9b6-209">En parlant d’autres plateformes, la prise en charge multiplateforme est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-209">Speaking of other platforms, it has cross-platform support.</span></span>  <span data-ttu-id="6a9b6-210">Et bien que cela ne signifie pas que toutes les plateformes sont prises en charge dès le passage, nous avons fait en sorte qu’aucun code du kit d’outils ne s’arrête lorsque vous basculez votre cible de génération sur d’autres plateformes.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-210">And while this doesn’t mean every single platform is supported out of the box, we have made sure none of the toolkit code will break when you switch your build target to other platforms.</span></span>  <span data-ttu-id="6a9b6-211">La robustesse et l’extensibilité avec la conception modulaire vous permettent de prendre en charge plusieurs plateformes, telles que ARCore, ARKit et OpenVR.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-211">The robustness and extensibility with the modular design sets you up on a good path to be able to support multiple platforms, such as ARCore, ARKit, and OpenVR.</span></span>


### <a name="performant"></a><span data-ttu-id="6a9b6-212">Form</span><span class="sxs-lookup"><span data-stu-id="6a9b6-212">Performant</span></span>
<span data-ttu-id="6a9b6-213">À l’aide de plateformes mobiles, nous avons créé l’informatique avec les performances à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-213">Working with mobile platforms, we constructed it with performance in mind.</span></span>  <span data-ttu-id="6a9b6-214">C’est très important, et nous voulons nous assurer que les outils ne vont pas travailler sur vous.</span><span class="sxs-lookup"><span data-stu-id="6a9b6-214">This is super important, and we wanted to ensure that the tools are not going to work against you.</span></span>


## <a name="see-also"></a><span data-ttu-id="6a9b6-215">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6a9b6-215">See also</span></span>
* [<span data-ttu-id="6a9b6-216">Guide de prise en main de MRTK</span><span class="sxs-lookup"><span data-stu-id="6a9b6-216">MRTK getting started guide</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html)
* [<span data-ttu-id="6a9b6-217">Page d’hébergement de la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="6a9b6-217">MRTK documentation home</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)
* [<span data-ttu-id="6a9b6-218">Installer les outils</span><span class="sxs-lookup"><span data-stu-id="6a9b6-218">Install the tools</span></span>](install-the-tools.md)
* [<span data-ttu-id="6a9b6-219">Portage de HTK/MRTK vers MRTK version 2</span><span class="sxs-lookup"><span data-stu-id="6a9b6-219">Porting from HTK/MRTK to MRTK version 2</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/HTKToMRTKPortingGuide.html)
