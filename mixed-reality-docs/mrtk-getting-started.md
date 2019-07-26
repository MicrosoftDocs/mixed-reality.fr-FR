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
# <a name="getting-started-with-mrtk-v2"></a>Prise en main de MRTK v2

## <a name="mrtk-getting-started-guide"></a>Guide de Prise en main MRTK
Pour plus d’informations sur la prise en main de MRTK v2, consultez le [Guide de prise](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html) en main de MRTK.

## <a name="what-is-mixed-reality-toolkit-mrtk"></a>Qu’est-ce que Mixed Reality Toolkit (MRTK)?
Le MRTK est une boîte à outils open source incroyable qui existe depuis la sortie de HoloLens, et n’est pas là où elle se trouvait aujourd’hui sans le travail difficile de notre communauté de développeurs qui lui a contribué. Au cours des trois dernières années, nous avons écouté les commentaires de notre communauté de développeurs et créé MRTK v2 pour prendre en compte les plus grands problèmes.  

MRTK v2 avec Unity est un kit de développement multiplateforme Open source pour les applications de réalité mixte.  MRTK version 2 a pour objectif d’accélérer le développement d’applications ciblant Microsoft HoloLens, les casques Windows Mixed Reality (VR) et la plate-forme OpenVR. Le projet a pour but de réduire le nombre d’obstacles qui gênent la création d’applications de réalité mixte et d’apporter une contribution à la Communauté de la réalité mixte. 


Pour en savoir plus, consultez le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html) .

## <a name="feature-areas"></a>Domaines de fonctionnalités

:::row:::
    :::column:::
    <img src="images/MRTK_Icon_InputSystem.png" alt="Input system" title="Système d’entrée" width="105"> Système d’entrée 
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_HandTracking.png" alt="Hand Tracking (HoloLens 2)" title="Suivi des mains (HoloLens 2)" width="105"> Suivi des mains (HoloLens 2)
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_EyeTracking.png" alt="Eye Tracking (HoloLens 2)" title="Suivi des yeux (HoloLens 2)" width="105">
    Suivi des yeux (HoloLens 2)
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_VoiceCommand.png" alt="Voice Commanding" title="Commandes vocales" width="105"> Commandes vocales
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_GazeSelect.png" alt="Gaze + Select (HoloLens (1st gen))" title="Point d' + sélectionner (HoloLens (1re génération))" width="105">
    Point d' + sélectionner (HoloLens (1re génération))
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_Teleportation.png" alt="Teleportation" title="Téléportation" width="105"> Téléportation
    :::column-end:::
:::row-end:::


:::row:::
    :::column:::
    <img src="images/MRTK_Icon_UIControls.png" alt="UI Controls" title="Contrôles d’interface utilisateur" width="105"> Contrôles d’interface utilisateur
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_Solver.png" alt="Solver and Interactions" title="Solveur et interactions" width="105"> Solveur et interactions
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_ControllerVisualization.png" alt="Controller Visualization" title="Visualisation du contrôleur" width="105"> Visualisation du contrôleur
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_SpatialUnderstanding.png" alt="Spatial Understanding" title="Compréhension spatiale" width="105"> Compréhension spatiale
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_Diagnostics.png" alt="Diagnostic Tool" title="Outil de diagnostic" width="105"> Outil de diagnostic
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_StandardShader.png" alt="MRTK Standard Shader" title="Nuanceur standard MRTK" width="105"> Nuanceur standard MRTK
    :::column-end:::
:::row-end:::

## <a name="ui-and-interaction-building-blocks"></a>Blocs de construction interface utilisateur et interaction

:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html"><img src="images/MRTK_Button_Main.png" alt="Button" title="Bouton" width="250"><br>
    **Button**<br>
    Contrôle de bouton qui prend en charge différentes méthodes d’entrée, y compris la main articulée de HoloLens 2<a/>
    :::column-end:::
    :::column:::
<a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html"><img src="images/MRTK_BoundingBox_Main.png" alt="Bounding Box" title="Cadre englobant" width="250"><br>
    **Cadre englobant**<br>
    Interface utilisateur standard pour manipuler des objets dans l’espace 3D<a/>
    :::column-end:::
    :::column:::
<a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html"><img src="images/MRTK_Manipulation_Main.png" alt="Manipulation Handler" title="Gestionnaire de manipulation" width="250"><br>
    **Gestionnaire de manipulation**<br>
    Script de manipulation d’objets avec une ou deux mains<a/>
    :::column-end:::
:::row-end:::    
    
:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Slate.html"><img src="images/MRTK_Slate_Main.png" alt="Slate" title="Médias" width="250"><br>
    **Médias** <br>
    plan de style 2D qui prend en charge le défilement avec une entrée articulée<a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_SystemKeyboard.html"><img src="images/MRTK_SystemKeyboard_Main.png" alt="System Keyboard" title="Clavier système" width="250"><br>
    **Clavier système**<br>
    Exemple de script d’utilisation du clavier système dans Unity<a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html"><img src="images/InteractableExamples.png" alt="Interactable" title="Sur" width="250"><br>
     **Sur** <br>
     Script permettant de rendre les objets interactifs avec les États visuels et la prise en charge des thèmes<a/>
    :::column-end:::
:::row-end:::       

:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html"><img src="images/MRTK_Solver_Main.png" alt="Solver" title="Solveur" width="250"><br>
    **Solveur** <br>
    Différents comportements de positionnement des objets, tels que balise, verrouillage de corps, taille de vue constante et magnétisme de surface<a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html"><img src="images/MRTK_ObjectCollection_Main.png" alt="Object Collection" title="Collection d’objets" width="250"><br>
    **Collection d’objets**<br>
    Script pour disposer un tableau d’objets dans une forme en trois dimensions<a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Tooltip.html"><img src="images/MRTK_Tooltip_Main.png" alt="Tooltip" title="Info-bulle" width="250">  <br>
    **Bulle**<br>
    Interface utilisateur d’annotation avec système d’ancrage/pivot flexible qui peut être utilisé pour étiqueter les contrôleurs de mouvement et les objets<a/>
    :::column-end:::
:::row-end:::   
        
:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html"><img src="images/MRTK_AppBar_Main.png" alt="App Bar" title="Barre de l’application" width="250"><br>
    **Barre de l’application**<br>
    Interface utilisateur pour l’activation manuelle du cadre englobant<a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Pointers.html"><img src="images/MRTK_Pointer_Main.png" alt="Pointers" title="Pointeurs" width="250"><br>
    **Pointeurs**<br>
    En savoir plus sur les différents types de pointeurs<a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_FingertipVisualization.html"><img src="images/MRTK_FingertipVisualization_Main.png" alt="Fingertip Visualization" title="Visualisation de portée" width="250"><br>
     **Visualisation de portée**<br>
     Visuel à portée de main, ce qui améliore la confiance pour l’interaction directe<a/>
    :::column-end:::
:::row-end:::   

:::row:::
    :::column:::
    <a href="https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_Sliders.md"><img src="images/MRTK_UX_Slider_Main.jpg" alt="Slider" title="Curseur" width="250"><br>
    **Slider**<br>
    Interface utilisateur du curseur pour l’ajustement des valeurs prenant en charge l’interaction de suivi direct<a/>
    :::column-end:::
    :::column:::
    <a href="https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_MRTKStandardShader.md"><img src="images/MRTK_StandardShader.jpg" alt="MRTK Standard Shader" title="Nuanceur standard MRTK" width="250"><br>
    **Nuanceur standard MRTK**<br>
    Le nuanceur standard de MRTK prend en charge différents éléments de conception Fluent avec des performances<a/>
    :::column-end:::
    :::column:::
    <a href="https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_HandJointChaser.md"><img src="images/MRTK_HandJointChaser_Main.jpg" alt="Hand Joint Chaser" title="Chase joint à la main" width="250"><br>
     **Chase joint à la main**<br>
     Montre comment utiliser le solveur pour attacher des objets aux jointures de la main<a/>
    :::column-end:::
:::row-end:::   
        
:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html"><img src="images/mrtk_et_targetselect.png" alt="Eye Tracking: Target Selection" title="Suivi des yeux: Sélection de la cible" width="250"><br>
    **Suivi des yeux: Sélection de la cible**<br>
    Combiner les yeux, la voix et la main pour sélectionner rapidement et facilement des hologrammes sur votre scène<a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html"><img src="images/mrtk_et_navigation.png" alt="Eye Tracking: Navigation" title="Suivi des yeux: Navigation" width="250"><br>
    **Suivi des yeux: Déplacement**<br>
    Apprenez à faire défiler automatiquement le texte ou à faire un zoom sur le contenu ciblé en fonction de ce que vous cherchez<a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Visualization.html"><img src="images/mrtk_et_heatmaps.png" alt="Eye Tracking: Heat Map" title="Suivi des yeux: Carte thermique" width="250"><br>
    **Suivi des yeux: Carte thermique**<br>
    Exemples de journalisation, de chargement et de visualisation de ce que les utilisateurs ont examiné dans votre application<a/>
    :::column-end:::
:::row-end:::           


## <a name="minimum-requirement-for-mrtk-v2"></a>Configuration minimale requise pour MRTK v2
* Unity 2018.3.x
* Microsoft Visual Studio 2017 ou version ultérieure
* SDK Windows 18362 + 
* Windows 10 1803 ou version ultérieure

## <a name="new-with-mrtk-v2"></a>Nouveautés avec MRTK v2
Nous souhaitons insister sur notre engagement envers ces outils de plateforme.  En fait, nous avons utilisé MRTK version 2 pour développer nos expériences de boîte de réception, telles que l’expérience d’installation (OOBE) et notre application d’apprentissage de réalité mixte.  Vous pouvez également vous attendre à voir les nouvelles fonctionnalités HoloLens 2 d’abord exposées par le biais de MRTK, car nous pensons qu’il s’agit de la meilleure façon de développer sur notre plateforme. 

### <a name="modular"></a>ADAPT
Nous l’avons créé de manière modulaire, ce qui vous permet de ne pas avoir à prendre chaque partie de la boîte à outils dans votre projet.  Il y en a en fait quelques avantages.  Il permet de réduire la taille de votre projet et de le rendre plus facile à gérer.  En plus de cela, étant donné qu’elle est générée avec des objets scriptables et qu’elle est pilotée par interface, il est également possible de remplacer les composants qui sont inclus avec le vôtre, pour prendre en charge d’autres services, systèmes et plateformes.


### <a name="cross-platform"></a>Système multiplateforme
En parlant d’autres plateformes, la prise en charge multiplateforme est prise en charge.  Et bien que cela ne signifie pas que toutes les plateformes sont prises en charge dès le passage, nous avons fait en sorte qu’aucun code du kit d’outils ne s’arrête lorsque vous basculez votre cible de génération sur d’autres plateformes.  La robustesse et l’extensibilité avec la conception modulaire vous permettent de prendre en charge plusieurs plateformes, telles que ARCore, ARKit et OpenVR.


### <a name="performant"></a>Form
À l’aide de plateformes mobiles, nous avons créé l’informatique avec les performances à l’esprit.  C’est très important, et nous voulons nous assurer que les outils ne vont pas travailler sur vous.


## <a name="see-also"></a>Voir aussi
* [Guide de prise en main de MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html)
* [Page d’hébergement de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)
* [Installer les outils](install-the-tools.md)
* [Portage de HTK/MRTK vers MRTK version 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/HTKToMRTKPortingGuide.html)
