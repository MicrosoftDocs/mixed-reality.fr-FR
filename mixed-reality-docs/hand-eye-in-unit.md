---
title: Suivi des mains et des yeux dans Unity
description: Il existe deux façons principales d’agir sur votre point d’intergression, les gestes manuels et les contrôleurs de mouvement.
author: thetuvix
ms.author: yoyoz
ms.date: 03/21/2018
ms.topic: article
keywords: mouvements, contrôleurs de mouvement, Unity, point de regard, entrée
ms.openlocfilehash: 13016879e47b3b61eb417ce9425e48ea56c1b726
ms.sourcegitcommit: f5c1dedb3b9e29f27f627025b9e7613931a7ce18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2019
ms.locfileid: "64580752"
---
# <a name="articulated-hand-and-eye-tracking-in-unity"></a>Suivi des mains et des yeux dans Unity

HoloLens 2 a introduit de nouvelles fonctionnalités passionnantes: le suivi des mains et des yeux articulés.

Le moyen le plus simple de tirer parti de la nouvelle fonctionnalité dans Unity est d’utiliser MRTK v2. Il existe également des exemples de scènes pour vous aider à commencer. 

* [Prise en main de la main articulée dans MRTK v2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/InputSystem/HandTracking.html)
* [Prise en main du suivi oculaire dans MRTK v2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Main.html)


# <a name="building-blocks-supporting-hands-eyes-and-others-in-mrtk-v2"></a>Blocs de construction prenant en charge les mains, les yeux et autres dans MRTK v2

MRTK v2 fournit un ensemble de contrôles d’interface utilisateur et de blocs de construction pour vous aider à accélérer votre développement. 

|  [![Bouton](images/MRTK_Button_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html) [Bouton](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html) | [![Rectangle englobant](images/MRTK_BoundingBox_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) [Rectangle anglobant](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) | [Gestionnaire de](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html) manipulation du gestionnaire de manipulation [ ![](images/MRTK_Manipulation_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html) |
|:--- | :--- | :--- |
| Contrôle de bouton qui prend en charge différentes méthodes d’entrée, y compris HoloLens2's articulée | Interface utilisateur standard pour manipuler des objets dans l’espace 3D | Script de manipulation d’objets avec une ou deux mains |
|  [![Ardoise](images/MRTK_Slate_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Slate.html) [Ardoise](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Slate.html) | [Clavier système](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_SystemKeyboard.html) du clavier système [ ![](images/MRTK_SystemKeyboard_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_SystemKeyboard.html) | [![Interagissable](images/InteractableExamples.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html) [Interagissable](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html) |
| plan de style 2D qui prend en charge le défilement avec une entrée articulée | Exemple de script d’utilisation du clavier système dans Unity  | Script permettant de rendre les objets interactifs avec les États visuels et la prise en charge des thèmes |
|  [![Solveur](images/MRTK_Solver_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) [Solveur](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) | [![Collecte d’objets](images/MRTK_ObjectCollection_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html) [Collecte d’objets](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html) | [![Info-bulle](images/MRTK_Tooltip_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Tooltip.html) [Info-bulle](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Tooltip.html) |
| Différents comportements de positionnement des objets, tels que balise, verrouillage de corps, taille de vue constante et magnétisme de surface | Script pour disposer un tableau d’objets dans une forme en trois dimensions | Interface utilisateur d’annotation avec système d’ancrage/pivot flexible qui peut être utilisé pour étiqueter les contrôleurs de mouvement et l’objet. |
|  [Barre d'](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html) application de la barre d’application [ ![](images/MRTK_AppBar_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html) | [![Pointeurs](images/MRTK_Pointer_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Pointers.html) [Pointeurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Pointers.html) | [![Visualisation des bouts des doigts](images/MRTK_FingertipVisualization_Main.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_FingertipVisualization.html) [Visualisation des bouts des doigts](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_FingertipVisualization.html) |
| Interface utilisateur pour l’activation manuelle du cadre englobant | En savoir plus sur les différents types de pointeurs | Visuel à portée de main, ce qui améliore la confiance pour l’interaction directe |
|  [![Suivi des yeux: Suivi visuel](images/mrtk_et_targetselect.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html) de la sélection [cible: Sélection de la cible](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html) | [![Suivi des yeux: Suivi](images/mrtk_et_navigation.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html) des yeux de navigation [: Déplacement](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html) | [![Suivi des yeux: Suivi des](images/mrtk_et_heatmaps.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Visualization.html) yeux de la carte [thermique: Carte thermique](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Visualization.html) |
| Combiner les yeux, la voix et la main pour sélectionner rapidement et facilement des hologrammes sur votre scène | Apprenez à faire défiler automatiquement le texte ou à faire un zoom sur le contenu ciblé en fonction de ce que vous cherchez| Exemples de journalisation, de chargement et de visualisation de ce que les utilisateurs ont examiné dans votre application |

# <a name="example-scenes"></a>Exemples de scènes
Explorez les différents types d’interactions et de contrôles d’interface utilisateur de MRTK dans [cet exemple de scène](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_HandInteractionExamples.html).

Vous pouvez trouver d’autres exemples de scènes dans [Mixed Reality Toolkit GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity) sous **ressources/MixedRealityToolkit. exemples/démos**dossier.

[![Exemple de scène](images/MRTK_Examples.png)](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_HandInteractionExamples.html)

## <a name="see-also"></a>Voir aussi

* [Mouvements](gestures.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [UnityEngine. XR. WSA. Input](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.html)
* [UnityEngine. XR. InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html)