---
title: Prise en main MRTK version 2
description: Pour les nouveaux développeurs qui souhaitent en tirant parti de MRTK
author: Yoyoz
ms.author: Yoyoz
ms.date: 05/15/19
ms.topic: article
keywords: Windows Mixed Reality, tester, le Kit de ressources de réalité mixte, MRTK version 2, MRTK, outils, SDK, HoloLens, HoloLens 2
ms.openlocfilehash: 249a0ce0e608410983934b75e399d013e1ff1879
ms.sourcegitcommit: c2a5bff423feba7d29d5431c870b6017c2fe1bc2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66750369"
---
# <a name="getting-started-with-mrtk-v2"></a><span data-ttu-id="30833-104">Prise en main MRTK v2</span><span class="sxs-lookup"><span data-stu-id="30833-104">Getting started with MRTK v2</span></span>

## <a name="mrtk-getting-started-guide"></a><span data-ttu-id="30833-105">MRTK Guide de démarrage</span><span class="sxs-lookup"><span data-stu-id="30833-105">MRTK Getting Started Guide</span></span>
<span data-ttu-id="30833-106">Consultez le [MRTK mise en route](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html) pour plus d’informations sur la prise en main MRTK V2.</span><span class="sxs-lookup"><span data-stu-id="30833-106">See the [MRTK getting started guide](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html) for information on getting started with MRTK V2.</span></span>

## <a name="what-is-mixed-reality-toolkit-mrtk"></a><span data-ttu-id="30833-107">Quel est le Kit de ressources de réalité mixte (MRTK) ?</span><span class="sxs-lookup"><span data-stu-id="30833-107">What is Mixed Reality Toolkit (MRTK)?</span></span>
<span data-ttu-id="30833-108">Le MRTK est un kit d’outils open source étonnantes qui existe dans la mesure où le HoloLens est sorti et ne serait pas où il est aujourd'hui sans le gros du travail de notre communauté de développeurs qui ont contribué à ce dernier.</span><span class="sxs-lookup"><span data-stu-id="30833-108">The MRTK is an amazing open source toolkit that has been around since the HoloLens was first released, and would not be where it is today without the hard work of our developer community who have contributed to it.</span></span> <span data-ttu-id="30833-109">Sur les 3 dernières années, nous avons écouté les commentaires de notre communauté de développeurs et généré v2 MRTK pour tenir compte des principales préoccupations.</span><span class="sxs-lookup"><span data-stu-id="30833-109">Over the past 3 years, we have listened to the feedback of our developer community, and built MRTK v2 to take the biggest concerns into account.</span></span>  

<span data-ttu-id="30833-110">Le v2 MRTK avec Unity est un kit de développement multiplateforme open source pour les applications de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="30833-110">The MRTK v2 with Unity is an open source cross-platform development kit for mixed reality applications.</span></span>  <span data-ttu-id="30833-111">MRTK version 2 est destiné à accélérer le développement d’applications qui ciblent Microsoft HoloLens, des casques Windows Mixed Reality IMMERSIFS (VR) et plateforme de OpenVR.</span><span class="sxs-lookup"><span data-stu-id="30833-111">MRTK version 2 is intended to accelerate development of applications targeting Microsoft HoloLens, Windows Mixed Reality immersive (VR) headsets and OpenVR platform.</span></span> <span data-ttu-id="30833-112">Le projet est destiné à réduire les barrières à l’entrée à créer des applications de réalité mixte et contribuer à la Communauté, tous les besoins d’évolution.</span><span class="sxs-lookup"><span data-stu-id="30833-112">The project is aimed at reducing barriers to entry to create mixed reality applications and contribute back to the community as we all grow.</span></span> 


<span data-ttu-id="30833-113">Consultez le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="30833-113">See the [MRTK documentation portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html) to learn more.</span></span>

## <a name="feature-areas"></a><span data-ttu-id="30833-114">Zones de fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="30833-114">Feature areas</span></span>

:::row:::
    :::column:::
    <img src="images/MRTK_Icon_InputSystem.png" alt="Input system" title="Système d’entrée" width="105"> <span data-ttu-id="30833-116">Système d’entrée</span><span class="sxs-lookup"><span data-stu-id="30833-116">Input System</span></span> 
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_HandTracking.png" alt="Hand Tracking (HoloLens 2)" title="Main (HoloLens 2) de suivi" width="105"> <span data-ttu-id="30833-118">Main (HoloLens 2) de suivi</span><span class="sxs-lookup"><span data-stu-id="30833-118">Hand Tracking (HoloLens 2)</span></span>
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_EyeTracking.png" alt="Eye Tracking (HoloLens 2)" title="Yeux (HoloLens 2)" width="105">
    <span data-ttu-id="30833-120">Yeux (HoloLens 2)</span><span class="sxs-lookup"><span data-stu-id="30833-120">Eye Tracking (HoloLens 2)</span></span>
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_VoiceCommand.png" alt="Voice Commanding" title="Exécution des commandes vocales" width="105"> <span data-ttu-id="30833-122">Exécution des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="30833-122">Voice Commanding</span></span>
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_GazeSelect.png" alt="Gaze + Select (HoloLens (1st gen))" title="Utilisation + sélectionner (HoloLens (1er gen))" width="105">
    <span data-ttu-id="30833-124">Utilisation + sélectionner (HoloLens (1er gen))</span><span class="sxs-lookup"><span data-stu-id="30833-124">Gaze + Select (HoloLens (1st gen))</span></span>
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_Teleportation.png" alt="Teleportation" title="Téléportation" width="105"> <span data-ttu-id="30833-126">Téléportation</span><span class="sxs-lookup"><span data-stu-id="30833-126">Teleportation</span></span>
    :::column-end:::
:::row-end:::


:::row:::
    :::column:::
    <img src="images/MRTK_Icon_UIControls.png" alt="UI Controls" title="Contrôles d’interface utilisateur" width="105"> <span data-ttu-id="30833-128">Contrôles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="30833-128">UI Controls</span></span>
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_Solver.png" alt="Solver and Interactions" title="Solveur et Interactions" width="105"> <span data-ttu-id="30833-130">Solveur et Interactions</span><span class="sxs-lookup"><span data-stu-id="30833-130">Solver and Interactions</span></span>
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_ControllerVisualization.png" alt="Controller Visualization" title="Visualisation du contrôleur" width="105"> <span data-ttu-id="30833-132">Visualisation du contrôleur</span><span class="sxs-lookup"><span data-stu-id="30833-132">Controller Visualization</span></span>
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_SpatialUnderstanding.png" alt="Spatial Understanding" title="Présentation spatiale" width="105"> <span data-ttu-id="30833-134">Présentation spatiale</span><span class="sxs-lookup"><span data-stu-id="30833-134">Spatial Understanding</span></span>
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_Diagnostics.png" alt="Diagnostic Tool" title="Outil de diagnostic" width="105"> <span data-ttu-id="30833-136">Outil de diagnostic</span><span class="sxs-lookup"><span data-stu-id="30833-136">Diagnostic Tool</span></span>
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_StandardShader.png" alt="MRTK Standard Shader" title="Nuanceur Standard MRTK" width="105"> <span data-ttu-id="30833-138">Nuanceur Standard MRTK</span><span class="sxs-lookup"><span data-stu-id="30833-138">MRTK Standard Shader</span></span>
    :::column-end:::
:::row-end:::

## <a name="ui-and-interaction-building-blocks"></a><span data-ttu-id="30833-139">Blocs d’interface utilisateur et de création de l’Interaction</span><span class="sxs-lookup"><span data-stu-id="30833-139">UI and Interaction Building blocks</span></span>

:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html"><img src="images/MRTK_Button_Main.png" alt="Button" title="Bouton" width="250"><br>
    <span data-ttu-id="30833-141">**Button**</span><span class="sxs-lookup"><span data-stu-id="30833-141">**Button**</span></span><br>
    <span data-ttu-id="30833-142">Un contrôle de bouton qui prend en charge différentes méthodes d’entrée, notamment main articulé HoloLens 2 <a/></span><span class="sxs-lookup"><span data-stu-id="30833-142">A button control which supports various input methods including HoloLens 2's articulated hand <a/></span></span>
    :::column-end:::
    :::column:::
<a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html"><img src="images/MRTK_BoundingBox_Main.png" alt="Bounding Box" title="Zone englobante" width="250"><br>
    <span data-ttu-id="30833-144">**Zone englobante**</span><span class="sxs-lookup"><span data-stu-id="30833-144">**Bounding Box**</span></span><br>
    <span data-ttu-id="30833-145">Interface utilisateur standard pour la manipulation des objets dans l’espace 3D <a/></span><span class="sxs-lookup"><span data-stu-id="30833-145">Standard UI for manipulating objects in 3D space <a/></span></span>
    :::column-end:::
    :::column:::
<a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html"><img src="images/MRTK_Manipulation_Main.png" alt="Manipulation Handler" title="Gestionnaire de manipulation" width="250"><br>
    <span data-ttu-id="30833-147">**Gestionnaire de manipulation**</span><span class="sxs-lookup"><span data-stu-id="30833-147">**Manipulation Handler**</span></span><br>
    <span data-ttu-id="30833-148">Script permettant de manipuler des objets avec un ou deux mains <a/></span><span class="sxs-lookup"><span data-stu-id="30833-148">Script for manipulating objects with one or two hands <a/></span></span>
    :::column-end:::
:::row-end:::    
    
:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Slate.html"><img src="images/MRTK_Slate_Main.png" alt="Slate" title="Ardoise" width="250"><br>
    <span data-ttu-id="30833-150">**Ardoise**</span><span class="sxs-lookup"><span data-stu-id="30833-150">**Slate**</span></span> <br>
    <span data-ttu-id="30833-151">Plan de style 2D qui prend en charge le défilement avec une entrée bras main <a/></span><span class="sxs-lookup"><span data-stu-id="30833-151">2D style plane which supports scrolling with articulated hand input <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_SystemKeyboard.html"><img src="images/MRTK_SystemKeyboard_Main.png" alt="System Keyboard" title="Clavier système" width="250"><br>
    <span data-ttu-id="30833-153">**Clavier système**</span><span class="sxs-lookup"><span data-stu-id="30833-153">**System Keyboard**</span></span><br>
    <span data-ttu-id="30833-154">Exemple de script de l’utilisation du clavier système dans Unity <a/></span><span class="sxs-lookup"><span data-stu-id="30833-154">Example script of using the system keyboard in Unity <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html"><img src="images/InteractableExamples.png" alt="Interactable" title="Sur" width="250"><br>
     <span data-ttu-id="30833-156">**Interactable**</span><span class="sxs-lookup"><span data-stu-id="30833-156">**Interactable**</span></span> <br>
     <span data-ttu-id="30833-157">Un script pour rendre les objets sur avec les états visuels et de prise en charge du thème <a/></span><span class="sxs-lookup"><span data-stu-id="30833-157">A script for making objects interactable with visual states and theme support <a/></span></span>
    :::column-end:::
:::row-end:::       

:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html"><img src="images/MRTK_Solver_Main.png" alt="Solver" title="Solveur" width="250"><br>
    <span data-ttu-id="30833-159">**Solveur**</span><span class="sxs-lookup"><span data-stu-id="30833-159">**Solver**</span></span> <br>
    <span data-ttu-id="30833-160">Différents comportements de positionnement telles que tag-along, verrouillage de corps, taille d’affichage constante et magnétisme de l’aire de conception de l’objet <a/></span><span class="sxs-lookup"><span data-stu-id="30833-160">Various object positioning behaviors such as tag-along, body-lock, constant view size and surface magnetism <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html"><img src="images/MRTK_ObjectCollection_Main.png" alt="Object Collection" title="Collection d’objets" width="250"><br>
    <span data-ttu-id="30833-162">**Collection d’objets**</span><span class="sxs-lookup"><span data-stu-id="30833-162">**Object Collection**</span></span><br>
    <span data-ttu-id="30833-163">Script de mise en page un tableau d’objets dans une forme 3D <a/></span><span class="sxs-lookup"><span data-stu-id="30833-163">Script for lay out an array of objects in a three-dimensional shape <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Tooltip.html"><img src="images/MRTK_Tooltip_Main.png" alt="Tooltip" title="Info-bulle" width="250">  <br>
    <span data-ttu-id="30833-165">**Info-bulle**</span><span class="sxs-lookup"><span data-stu-id="30833-165">**Tooltip**</span></span><br>
    <span data-ttu-id="30833-166">Annotation de l’interface utilisateur avec un système souple d’ancrage/tableau croisé dynamique qui peut être utilisé pour l’étiquetage d’objet et les contrôleurs de mouvement <a/></span><span class="sxs-lookup"><span data-stu-id="30833-166">Annotation UI with flexible anchor/pivot system which can be used for labeling motion controllers and object <a/></span></span>
    :::column-end:::
:::row-end:::   
        
:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html"><img src="images/MRTK_AppBar_Main.png" alt="App Bar" title="Barre de l’application" width="250"><br>
    <span data-ttu-id="30833-168">**Barre de l’application**</span><span class="sxs-lookup"><span data-stu-id="30833-168">**App Bar**</span></span><br>
    <span data-ttu-id="30833-169">Interface utilisateur pour l’activation manuelle de cadre englobant de la zone <a/></span><span class="sxs-lookup"><span data-stu-id="30833-169">UI for Bounding Box's manual activation <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Pointers.html"><img src="images/MRTK_Pointer_Main.png" alt="Pointers" title="Pointeurs" width="250"><br>
    <span data-ttu-id="30833-171">**Pointeurs**</span><span class="sxs-lookup"><span data-stu-id="30833-171">**Pointers**</span></span><br>
    <span data-ttu-id="30833-172">En savoir plus sur les différents types de pointeurs <a/></span><span class="sxs-lookup"><span data-stu-id="30833-172">Learn about various types of pointers <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_FingertipVisualization.html"><img src="images/MRTK_FingertipVisualization_Main.png" alt="Fingertip Visualization" title="Visualisation du bout des doigts" width="250"><br>
     <span data-ttu-id="30833-174">**Visualisation du bout des doigts**</span><span class="sxs-lookup"><span data-stu-id="30833-174">**Fingertip Visualization**</span></span><br>
     <span data-ttu-id="30833-175">Caractère intuitif Visual sur le bout des doigts qui améliore la confiance pour l’interaction directe <a/></span><span class="sxs-lookup"><span data-stu-id="30833-175">Visual affordance on the fingertip which improves the confidence for the direct interaction <a/></span></span>
    :::column-end:::
:::row-end:::   

:::row:::
    :::column:::
    <a href="https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_Sliders.md"><img src="images/MRTK_UX_Slider_Main.jpg" alt="Slider" title="Curseur" width="250"><br>
    <span data-ttu-id="30833-177">**Slider**</span><span class="sxs-lookup"><span data-stu-id="30833-177">**Slider**</span></span><br>
    <span data-ttu-id="30833-178">L’interface utilisateur de curseur pour ajuster les valeurs prise en charge main direct suivi d’interaction <a/></span><span class="sxs-lookup"><span data-stu-id="30833-178">Slider UI for adjusting values supporting direct hand tracking interaction <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_MRTKStandardShader.md"><img src="images/MRTK_StandardShader.jpg" alt="MRTK Standard Shader" title="Nuanceur Standard MRTK" width="250"><br>
    <span data-ttu-id="30833-180">**Nuanceur Standard MRTK**</span><span class="sxs-lookup"><span data-stu-id="30833-180">**MRTK Standard Shader**</span></span><br>
    <span data-ttu-id="30833-181">Nuanceur Standard de MRTK prend en charge les divers éléments de conception Fluent avec des performances <a/></span><span class="sxs-lookup"><span data-stu-id="30833-181">MRTK's Standard shader supports various Fluent design elements with performance <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_HandJointChaser.md"><img src="images/MRTK_HandJointChaser_Main.jpg" alt="Hand Joint Chaser" title="Chaser commune de main" width="250"><br>
     <span data-ttu-id="30833-183">**Chaser commune de main**</span><span class="sxs-lookup"><span data-stu-id="30833-183">**Hand Joint Chaser**</span></span><br>
     <span data-ttu-id="30833-184">Montre comment utiliser le solveur pour attacher des objets pour les articulations main <a/></span><span class="sxs-lookup"><span data-stu-id="30833-184">Demonstrates how to use Solver to attach objects to the hand joints <a/></span></span>
    :::column-end:::
:::row-end:::   
        
:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html"><img src="images/mrtk_et_targetselect.png" alt="Eye Tracking: Target Selection" title="Suivi de le œil : Sélection de la cible" width="250"><br>
    <span data-ttu-id="30833-186">**Suivi de le œil : Sélection de la cible**</span><span class="sxs-lookup"><span data-stu-id="30833-186">**Eye Tracking: Target Selection**</span></span><br>
    <span data-ttu-id="30833-187">Combiner les yeux, voix et main d’entrée pour rapidement et facilement sélectionner hologrammes entre votre scène <a/></span><span class="sxs-lookup"><span data-stu-id="30833-187">Combine eyes, voice and hand input to quickly and effortlessly select holograms across your scene <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html"><img src="images/mrtk_et_navigation.png" alt="Eye Tracking: Navigation" title="Suivi de le œil : Navigation" width="250"><br>
    <span data-ttu-id="30833-189">**Suivi de le œil : Navigation**</span><span class="sxs-lookup"><span data-stu-id="30833-189">**Eye Tracking: Navigation**</span></span><br>
    <span data-ttu-id="30833-190">Découvrez comment auto faire défiler le texte ou aisément effectuer un zoom avant en contenu concentré selon ce que vous regardez <a/></span><span class="sxs-lookup"><span data-stu-id="30833-190">Learn how to auto scroll text or fluently zoom into focused content based on what you are looking at <a/></span></span>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Visualization.html"><img src="images/mrtk_et_heatmaps.png" alt="Eye Tracking: Heat Map" title="Suivi de le œil : Carte thermique" width="250"><br>
    <span data-ttu-id="30833-192">**Suivi de le œil : Carte thermique**</span><span class="sxs-lookup"><span data-stu-id="30833-192">**Eye Tracking: Heat Map**</span></span><br>
    <span data-ttu-id="30833-193">Exemples pour la journalisation, le chargement et la visualisation de ce que les utilisateurs ont été consultant dans votre application <a/></span><span class="sxs-lookup"><span data-stu-id="30833-193">Examples for logging, loading and visualizing what users have been looking at in your app <a/></span></span>
    :::column-end:::
:::row-end:::           


## <a name="minimum-requirement-for-mrtk-v2"></a><span data-ttu-id="30833-194">Configuration minimale requise pour MRTK v2</span><span class="sxs-lookup"><span data-stu-id="30833-194">Minimum Requirement for MRTK v2</span></span>
* <span data-ttu-id="30833-195">Unity 2018.3.x</span><span class="sxs-lookup"><span data-stu-id="30833-195">Unity 2018.3.x</span></span>
* <span data-ttu-id="30833-196">Microsoft Visual Studio 2017 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="30833-196">Microsoft Visual Studio 2017 or later</span></span>
* <span data-ttu-id="30833-197">Windows SDK 18362 +</span><span class="sxs-lookup"><span data-stu-id="30833-197">Windows SDK 18362+</span></span> 
* <span data-ttu-id="30833-198">Windows 10 1803 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="30833-198">Windows 10 1803 or later</span></span>

## <a name="new-with-mrtk-v2"></a><span data-ttu-id="30833-199">Nouveauté de MRTK v2</span><span class="sxs-lookup"><span data-stu-id="30833-199">New with MRTK v2</span></span>
<span data-ttu-id="30833-200">Nous voulons souligner notre engagement à ces outils de plateforme.</span><span class="sxs-lookup"><span data-stu-id="30833-200">We want to stress our commitment to these platform tools.</span></span>  <span data-ttu-id="30833-201">En fait, nous avons exploité MRTK version 2 pour développer des expériences notre boîte de réception, tels que l’expérience d’installation (OOBE) et notre application Learning de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="30833-201">In fact, we leveraged MRTK version 2 to develop our inbox experiences, such as the setup experience (OOBE) and our Mixed Reality Learning application.</span></span>  <span data-ttu-id="30833-202">Également attendez-vous à voir les nouvelles fonctionnalités de HoloLens 2 d’abord été exposées via MRTK, car nous pensons que c’est le meilleur moyen pour développer sur notre plateforme.</span><span class="sxs-lookup"><span data-stu-id="30833-202">You can also expect to see new HoloLens 2 capabilities first exposed through MRTK because we believe it’s the best way to develop on our platform.</span></span> 

### <a name="modular"></a><span data-ttu-id="30833-203">Modular</span><span class="sxs-lookup"><span data-stu-id="30833-203">Modular</span></span>
<span data-ttu-id="30833-204">Nous avons l’intégré de manière modulaire, afin que vous n’avez pas besoin de tenir chaque bit du Kit de ressources de votre projet.</span><span class="sxs-lookup"><span data-stu-id="30833-204">We have built it in a modular way, so that you do not need to take every bit of the toolkit into your project.</span></span>  <span data-ttu-id="30833-205">Il existe en fait quelques avantages à cela.</span><span class="sxs-lookup"><span data-stu-id="30833-205">There are actually a few benefits to this.</span></span>  <span data-ttu-id="30833-206">Il conserve la taille de votre projet plus petits, ainsi que des rend plus facile à gérer.</span><span class="sxs-lookup"><span data-stu-id="30833-206">It keeps your project size smaller, as well as makes it easier to manage.</span></span>  <span data-ttu-id="30833-207">En plus de cela, car il est créé avec les objets scriptables et vise l’interface, il est également possible de remplacer les composants qui sont inclus avec votre propre pour prendre en charge d’autres services, les systèmes et plates-formes.</span><span class="sxs-lookup"><span data-stu-id="30833-207">On top of that, because it’s built with scriptable objects and is interface driven, it’s also possible for you to replace the components that are included with your own, to support other services, systems, and platforms.</span></span>


### <a name="cross-platform"></a><span data-ttu-id="30833-208">Système multiplateforme</span><span class="sxs-lookup"><span data-stu-id="30833-208">Cross-platform</span></span>
<span data-ttu-id="30833-209">En parlant d’autres plateformes, il a prise en charge multiplateforme.</span><span class="sxs-lookup"><span data-stu-id="30833-209">Speaking of other platforms, it has cross-platform support.</span></span>  <span data-ttu-id="30833-210">Et, bien que cela ne signifie pas que chaque plateforme unique est prise en charge prête à l’emploi, nous avons veillé à ce que le code du Kit de ressources s’arrête lorsque vous basculez votre cible de build à d’autres plateformes.</span><span class="sxs-lookup"><span data-stu-id="30833-210">And while this doesn’t mean every single platform is supported out of the box, we have made sure none of the toolkit code will break when you switch your build target to other platforms.</span></span>  <span data-ttu-id="30833-211">La robustesse et l’extensibilité avec la conception modulaire configure sur un chemin d’accès bon pour être en mesure de prendre en charge plusieurs plateformes, telles que ARCore, ARKit et OpenVR.</span><span class="sxs-lookup"><span data-stu-id="30833-211">The robustness and extensibility with the modular design sets you up on a good path to be able to support multiple platforms, such as ARCore, ARKit, and OpenVR.</span></span>


### <a name="performant"></a><span data-ttu-id="30833-212">Performant</span><span class="sxs-lookup"><span data-stu-id="30833-212">Performant</span></span>
<span data-ttu-id="30833-213">Utilisation des plateformes mobiles, nous avons construit avec des performances à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="30833-213">Working with mobile platforms, we constructed it with performance in mind.</span></span>  <span data-ttu-id="30833-214">Ceci est très important, et nous souhaitions pour vous assurer que les outils vont pas fonctionner avec vous.</span><span class="sxs-lookup"><span data-stu-id="30833-214">This is super important, and we wanted to ensure that the tools are not going to work against you.</span></span>


## <a name="see-also"></a><span data-ttu-id="30833-215">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="30833-215">See also</span></span>
* [<span data-ttu-id="30833-216">MRTK guide de démarrage</span><span class="sxs-lookup"><span data-stu-id="30833-216">MRTK getting started guide</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html)
* [<span data-ttu-id="30833-217">Documentation MRTK domestique</span><span class="sxs-lookup"><span data-stu-id="30833-217">MRTK documentation home</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)
* [<span data-ttu-id="30833-218">Installer les outils</span><span class="sxs-lookup"><span data-stu-id="30833-218">Install the tools</span></span>](install-the-tools.md)
* [<span data-ttu-id="30833-219">Portage de HTK/MRTK vers MRTK version 2</span><span class="sxs-lookup"><span data-stu-id="30833-219">Porting from HTK/MRTK to MRTK version 2</span></span>](mrtk-porting-guide.md)
