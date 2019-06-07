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
# <a name="getting-started-with-mrtk-v2"></a>Prise en main MRTK v2

## <a name="mrtk-getting-started-guide"></a>MRTK Guide de démarrage
Consultez le [MRTK mise en route](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html) pour plus d’informations sur la prise en main MRTK V2.

## <a name="what-is-mixed-reality-toolkit-mrtk"></a>Quel est le Kit de ressources de réalité mixte (MRTK) ?
Le MRTK est un kit d’outils open source étonnantes qui existe dans la mesure où le HoloLens est sorti et ne serait pas où il est aujourd'hui sans le gros du travail de notre communauté de développeurs qui ont contribué à ce dernier. Sur les 3 dernières années, nous avons écouté les commentaires de notre communauté de développeurs et généré v2 MRTK pour tenir compte des principales préoccupations.  

Le v2 MRTK avec Unity est un kit de développement multiplateforme open source pour les applications de réalité mixte.  MRTK version 2 est destiné à accélérer le développement d’applications qui ciblent Microsoft HoloLens, des casques Windows Mixed Reality IMMERSIFS (VR) et plateforme de OpenVR. Le projet est destiné à réduire les barrières à l’entrée à créer des applications de réalité mixte et contribuer à la Communauté, tous les besoins d’évolution. 


Consultez le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html) pour en savoir plus.

## <a name="feature-areas"></a>Zones de fonctionnalité

:::row:::
    :::column:::
    <img src="images/MRTK_Icon_InputSystem.png" alt="Input system" title="Système d’entrée" width="105"> Système d’entrée 
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_HandTracking.png" alt="Hand Tracking (HoloLens 2)" title="Main (HoloLens 2) de suivi" width="105"> Main (HoloLens 2) de suivi
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_EyeTracking.png" alt="Eye Tracking (HoloLens 2)" title="Yeux (HoloLens 2)" width="105">
    Yeux (HoloLens 2)
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_VoiceCommand.png" alt="Voice Commanding" title="Exécution des commandes vocales" width="105"> Exécution des commandes vocales
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_GazeSelect.png" alt="Gaze + Select (HoloLens (1st gen))" title="Utilisation + sélectionner (HoloLens (1er gen))" width="105">
    Utilisation + sélectionner (HoloLens (1er gen))
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
    <img src="images/MRTK_Icon_Solver.png" alt="Solver and Interactions" title="Solveur et Interactions" width="105"> Solveur et Interactions
    :::column-end:::
    :::column:::
    <img src="images/MRTK_Icon_ControllerVisualization.png" alt="Controller Visualization" title="Visualisation du contrôleur" width="105"> Visualisation du contrôleur
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_SpatialUnderstanding.png" alt="Spatial Understanding" title="Présentation spatiale" width="105"> Présentation spatiale
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_Diagnostics.png" alt="Diagnostic Tool" title="Outil de diagnostic" width="105"> Outil de diagnostic
    :::column-end:::
        :::column:::
    <img src="images/MRTK_Icon_StandardShader.png" alt="MRTK Standard Shader" title="Nuanceur Standard MRTK" width="105"> Nuanceur Standard MRTK
    :::column-end:::
:::row-end:::

## <a name="ui-and-interaction-building-blocks"></a>Blocs d’interface utilisateur et de création de l’Interaction

:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html"><img src="images/MRTK_Button_Main.png" alt="Button" title="Bouton" width="250"><br>
    **Button**<br>
    Un contrôle de bouton qui prend en charge différentes méthodes d’entrée, notamment main articulé HoloLens 2 <a/>
    :::column-end:::
    :::column:::
<a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html"><img src="images/MRTK_BoundingBox_Main.png" alt="Bounding Box" title="Zone englobante" width="250"><br>
    **Zone englobante**<br>
    Interface utilisateur standard pour la manipulation des objets dans l’espace 3D <a/>
    :::column-end:::
    :::column:::
<a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html"><img src="images/MRTK_Manipulation_Main.png" alt="Manipulation Handler" title="Gestionnaire de manipulation" width="250"><br>
    **Gestionnaire de manipulation**<br>
    Script permettant de manipuler des objets avec un ou deux mains <a/>
    :::column-end:::
:::row-end:::    
    
:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Slate.html"><img src="images/MRTK_Slate_Main.png" alt="Slate" title="Ardoise" width="250"><br>
    **Ardoise** <br>
    Plan de style 2D qui prend en charge le défilement avec une entrée bras main <a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_SystemKeyboard.html"><img src="images/MRTK_SystemKeyboard_Main.png" alt="System Keyboard" title="Clavier système" width="250"><br>
    **Clavier système**<br>
    Exemple de script de l’utilisation du clavier système dans Unity <a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html"><img src="images/InteractableExamples.png" alt="Interactable" title="Sur" width="250"><br>
     **Interactable** <br>
     Un script pour rendre les objets sur avec les états visuels et de prise en charge du thème <a/>
    :::column-end:::
:::row-end:::       

:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html"><img src="images/MRTK_Solver_Main.png" alt="Solver" title="Solveur" width="250"><br>
    **Solveur** <br>
    Différents comportements de positionnement telles que tag-along, verrouillage de corps, taille d’affichage constante et magnétisme de l’aire de conception de l’objet <a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html"><img src="images/MRTK_ObjectCollection_Main.png" alt="Object Collection" title="Collection d’objets" width="250"><br>
    **Collection d’objets**<br>
    Script de mise en page un tableau d’objets dans une forme 3D <a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Tooltip.html"><img src="images/MRTK_Tooltip_Main.png" alt="Tooltip" title="Info-bulle" width="250">  <br>
    **Info-bulle**<br>
    Annotation de l’interface utilisateur avec un système souple d’ancrage/tableau croisé dynamique qui peut être utilisé pour l’étiquetage d’objet et les contrôleurs de mouvement <a/>
    :::column-end:::
:::row-end:::   
        
:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html"><img src="images/MRTK_AppBar_Main.png" alt="App Bar" title="Barre de l’application" width="250"><br>
    **Barre de l’application**<br>
    Interface utilisateur pour l’activation manuelle de cadre englobant de la zone <a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Pointers.html"><img src="images/MRTK_Pointer_Main.png" alt="Pointers" title="Pointeurs" width="250"><br>
    **Pointeurs**<br>
    En savoir plus sur les différents types de pointeurs <a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_FingertipVisualization.html"><img src="images/MRTK_FingertipVisualization_Main.png" alt="Fingertip Visualization" title="Visualisation du bout des doigts" width="250"><br>
     **Visualisation du bout des doigts**<br>
     Caractère intuitif Visual sur le bout des doigts qui améliore la confiance pour l’interaction directe <a/>
    :::column-end:::
:::row-end:::   

:::row:::
    :::column:::
    <a href="https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_Sliders.md"><img src="images/MRTK_UX_Slider_Main.jpg" alt="Slider" title="Curseur" width="250"><br>
    **Slider**<br>
    L’interface utilisateur de curseur pour ajuster les valeurs prise en charge main direct suivi d’interaction <a/>
    :::column-end:::
    :::column:::
    <a href="https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_MRTKStandardShader.md"><img src="images/MRTK_StandardShader.jpg" alt="MRTK Standard Shader" title="Nuanceur Standard MRTK" width="250"><br>
    **Nuanceur Standard MRTK**<br>
    Nuanceur Standard de MRTK prend en charge les divers éléments de conception Fluent avec des performances <a/>
    :::column-end:::
    :::column:::
    <a href="https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_HandJointChaser.md"><img src="images/MRTK_HandJointChaser_Main.jpg" alt="Hand Joint Chaser" title="Chaser commune de main" width="250"><br>
     **Chaser commune de main**<br>
     Montre comment utiliser le solveur pour attacher des objets pour les articulations main <a/>
    :::column-end:::
:::row-end:::   
        
:::row:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html"><img src="images/mrtk_et_targetselect.png" alt="Eye Tracking: Target Selection" title="Suivi de le œil : Sélection de la cible" width="250"><br>
    **Suivi de le œil : Sélection de la cible**<br>
    Combiner les yeux, voix et main d’entrée pour rapidement et facilement sélectionner hologrammes entre votre scène <a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html"><img src="images/mrtk_et_navigation.png" alt="Eye Tracking: Navigation" title="Suivi de le œil : Navigation" width="250"><br>
    **Suivi de le œil : Navigation**<br>
    Découvrez comment auto faire défiler le texte ou aisément effectuer un zoom avant en contenu concentré selon ce que vous regardez <a/>
    :::column-end:::
    :::column:::
    <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Visualization.html"><img src="images/mrtk_et_heatmaps.png" alt="Eye Tracking: Heat Map" title="Suivi de le œil : Carte thermique" width="250"><br>
    **Suivi de le œil : Carte thermique**<br>
    Exemples pour la journalisation, le chargement et la visualisation de ce que les utilisateurs ont été consultant dans votre application <a/>
    :::column-end:::
:::row-end:::           


## <a name="minimum-requirement-for-mrtk-v2"></a>Configuration minimale requise pour MRTK v2
* Unity 2018.3.x
* Microsoft Visual Studio 2017 ou version ultérieure
* Windows SDK 18362 + 
* Windows 10 1803 ou version ultérieure

## <a name="new-with-mrtk-v2"></a>Nouveauté de MRTK v2
Nous voulons souligner notre engagement à ces outils de plateforme.  En fait, nous avons exploité MRTK version 2 pour développer des expériences notre boîte de réception, tels que l’expérience d’installation (OOBE) et notre application Learning de réalité mixte.  Également attendez-vous à voir les nouvelles fonctionnalités de HoloLens 2 d’abord été exposées via MRTK, car nous pensons que c’est le meilleur moyen pour développer sur notre plateforme. 

### <a name="modular"></a>Modular
Nous avons l’intégré de manière modulaire, afin que vous n’avez pas besoin de tenir chaque bit du Kit de ressources de votre projet.  Il existe en fait quelques avantages à cela.  Il conserve la taille de votre projet plus petits, ainsi que des rend plus facile à gérer.  En plus de cela, car il est créé avec les objets scriptables et vise l’interface, il est également possible de remplacer les composants qui sont inclus avec votre propre pour prendre en charge d’autres services, les systèmes et plates-formes.


### <a name="cross-platform"></a>Système multiplateforme
En parlant d’autres plateformes, il a prise en charge multiplateforme.  Et, bien que cela ne signifie pas que chaque plateforme unique est prise en charge prête à l’emploi, nous avons veillé à ce que le code du Kit de ressources s’arrête lorsque vous basculez votre cible de build à d’autres plateformes.  La robustesse et l’extensibilité avec la conception modulaire configure sur un chemin d’accès bon pour être en mesure de prendre en charge plusieurs plateformes, telles que ARCore, ARKit et OpenVR.


### <a name="performant"></a>Performant
Utilisation des plateformes mobiles, nous avons construit avec des performances à l’esprit.  Ceci est très important, et nous souhaitions pour vous assurer que les outils vont pas fonctionner avec vous.


## <a name="see-also"></a>Voir aussi
* [MRTK guide de démarrage](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html)
* [Documentation MRTK domestique](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)
* [Installer les outils](install-the-tools.md)
* [Portage de HTK/MRTK vers MRTK version 2](mrtk-porting-guide.md)
