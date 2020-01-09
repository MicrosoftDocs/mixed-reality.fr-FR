---
title: MRTK 101-utilisation de Mixed Reality Toolkit Unity pour les interactions de base (HoloLens 2, HoloLens, Windows Mixed Reality, Open VR)
description: Comment utiliser le kit de procédures pratiques de réalité mixte pour les interactions de base (HoloLens 2, HoloLens, Windows Mixed Reality, Open VR)
author: cre8ivepark
ms.author: dongpark
ms.date: 08/27/2019
ms.topic: article
keywords: HoloLens, MRTK, kit d’outils de réalité mixte, Windows Mixed Reality, conception, exemple d’application, contrôles
ms.openlocfilehash: ad9d2755522c2610ae051fa61f96605e49404d2d
ms.sourcegitcommit: 5054f5c23965ce56599cb29ac9d9c6e48812dabd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2020
ms.locfileid: "75623496"
---
# <a name="mrtk-101-how-to-use-mixed-reality-toolkit-unity-for-basic-interactions-hololens-2-hololens-windows-mixed-reality-openvr"></a>MRTK 101 : comment utiliser le kit de tâches de la réalité mixte pour les interactions de base (HoloLens 2, HoloLens, Windows Mixed Reality, Open VR)

![MRTK](images/MRTK101/MRTK101Cover.png)

Découvrez comment utiliser MRTK pour obtenir certains des modèles d’interaction les plus couramment utilisés dans la réalité mixte.

- Comment simuler des interactions d’entrée dans l’éditeur Unity ?
- Comment récupérer et déplacer un objet ?
- Comment redimensionner un objet ?
- Comment déplacer ou faire pivoter un objet avec une précision ?
- Comment faire en sorte qu’un objet réponde aux événements d’entrée ?
- Comment ajouter des commentaires visuels ?
- Comment ajouter des commentaires audio ?
- Comment utiliser le bouton de style HoloLens 2 prefabs ?
- Comment faire en sorte qu’un objet suive votre propos ?
- Comment faire face à un objet ?

## <a name="how-to-simulate-input-interactions-in-unityeditor"></a>Comment simuler des interactions d’entrée dans l’éditeur Unity ?
MRTK prend en charge la simulation d’entrée dans l’éditeur. Exécutez simplement votre scène en cliquant sur le bouton de lecture d’Unity. Utilisez ces clés pour simuler l’entrée.
Appuyez sur les touches W, A, S, D pour déplacer l’appareil photo.
Maintenez le bouton droit de la souris et déplacez la souris pour regarder.
Pour faire apparaître les mains simulées, appuyez sur la barre d’espace (droite) ou sur la touche gauche (gauche) pour conserver les mains simulées dans la vue, appuyez sur la touche T ou Y pour faire pivoter les mains simulées, appuyez sur Q ou E (horizontal)/R ou F (vertical)

- [En savoir plus sur la simulation d’entrée dans la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/InputSimulation/InputSimulationService.html)


## <a name="how-to-grab-and-move-anobject"></a>Comment récupérer et déplacer un objet ?
Pour rendre un objet pouvant être extrait, assignez ces deux scripts : ManipulationHandler.cs et NearInteractionGrabbable. cs (pour la saisie directe avec l’entrée de suivi articulé) ManipulationHandler prend en charge les interactions près et éloignées. Vous pouvez saisir et déplacer un objet avec l’entrée de suivi articulé de HoloLens 2 (Near), le rayon de main (FAR), le faisceau de contrôle de mouvement (FAR), le curseur de pointeur HoloLens & le robinet d’air (FAR).

<img alt="NearInteractionGrabbable and ManipulationHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_ManipulationHandler.png">

<img alt="NearInteractionGrabbable and ManipulationHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_GrabMove.gif">


## <a name="how-to-resize-anobject"></a>Comment redimensionner un objet ?
ManipulationHandler.cs prend en charge la rotation/la mise à l’échelle à deux mains. Cela fonctionne avec différents types d’entrée tels que l’entrée articulée du langage HoloLens 2, le point de contrôle du point d’entrée du regard et du point de présence du point de contrôle de l’entrée de commande du casque Windows Mixed Realing.

- [En savoir plus sur le gestionnaire de manipulation dans la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html)

<img alt="NearInteractionGrabbable and ManipulationHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_ManipulationHandler.gif">

## <a name="how-to-move-or-rotate-an-object-with-precision"></a>Comment déplacer ou faire pivoter un objet avec une précision ?
Assignez BoundingBox.cs à un objet pour utiliser le cadre englobant qui est l’interface pour la mise à l’échelle et la rotation d’un objet. Par défaut, il affiche les handles et les câbles bleus de style HoloLens 1. Pour utiliser des handles animés basés sur le style HoloLens 2, vous devez assigner des prefabs et des matériaux. Pour plus d’informations sur la configuration, reportez-vous à la [documentation du cadre englobant](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) et à la scène BoundingBoxExamples. Unity.

<img alt="BoundingBox.cs assigned to an object" width="800" src="images/MRTK101/MRTK_BoundingBox.png">

<img alt="BoundingBox.cs assigned to an object" width="800" src="images/MRTK101/MRTK_BoundingBox.gif">


- [En savoir plus sur le cadre englobant dans la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)

## <a name="how-to-make-an-object-respond-to-inputevents"></a>Comment faire en sorte qu’un objet réponde aux événements d’entrée ?
Assignez PointerHandler.cs à un objet. Dans l’inspecteur, vous serez en mesure d’utiliser les événements OnPointerDown (), OnPointerUp (), OnPointerClicked (), OnPointerDragged () pour utiliser ces événements dans un script, implémentez IMixedRealityPointerHandler.

<img alt="PointerHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_PointerHandler.png">

- [En savoir plus sur le système d’entrée dans la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html)

## <a name="how-to-add-visual-feedback"></a>Comment ajouter des commentaires visuels ?
Assignez Interactable.cs à un objet. Dans l’inspecteur, créez un nouveau thème. À l’aide des profils de thème interactifs, vous pouvez facilement ajouter des commentaires visuels à tous les États d’interaction d’entrée disponibles.

<img alt="PointerHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_Interactable.png">

<img alt="Interactable" width="800" src="images/MRTK101/MRTK_Interactable.gif">


L’interaction interactive fournit différents types de thèmes, y compris le thème du nuanceur, qui vous permet de contrôler les propriétés de l’état du nuanceur par interaction.

- [En savoir plus sur les informations d’interaction dans la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html)

Un autre bloc de construction important pour les commentaires visuels est le nuanceur standard MRTK. Avec le nuanceur standard MRTK, vous pouvez facilement ajouter des effets de commentaires visuels tels que la lumière de survol et la lumière de proximité. Étant donné que le nuanceur standard MRTK effectue un calcul beaucoup moins important que le nuanceur standard Unity, vous pouvez créer une expérience performante.

Créez un nouveau matériau et sélectionnez le nuanceur « Mixed Reality Toolkit > standard ». Ou vous pouvez choisir l’un des matériaux existants qui utilisent le nuanceur standard MRTK.

<img alt="MRTK Standard Shader" width="400" src="images/MRTK101/MRTK_Shader0.png">
<br/><br/>
<img alt="MRTK Standard Shader" width="800" src="images/MRTK101/MRTK_Shader1.png">

<img alt="MRTK Standard Shader" width="800" src="images/MRTK101/MRTK_Shader.gif">


- [En savoir plus sur le nuanceur MRTK standard dans la documentation de MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_MRTKStandardShader.html)

## <a name="how-to-add-audio-feedback"></a>Comment ajouter des commentaires audio ?
Ajoutez AudioSource à un objet. Ensuite, dans les scripts qui exposent des événements d’entrée (par exemple, Interactable.cs ou PointerHandler.cs), assignez l’objet à l’événement et sélectionnez AudioSource. PlayOneShot (). Vous pouvez utiliser vos clips audio ou en choisir un à partir des ressources audio de MRTK.

<img alt="Audio Source assigned to an object. AudioSource.PlayOneShot configured in the Interactable's OnPress() and OnRelease() events." width="800" src="images/MRTK101/MRTK_Audio.png">

## <a name="how-to-use-hololens-2-style-buttonprefabs"></a>Comment utiliser le bouton de style HoloLens 2 prefabs ?
MRTK fournit différents types de boutons de style de Shell (système d’exploitation) HoloLens 2. Il fournit des commentaires visuels sophistiqués, tels que la lumière de proximité, la zone de compression et un effet de ondulation sur l’aire du bouton.

<img alt="Interactable" width="800" src="images/MRTK101/MRTK_Button.gif">

Il vous suffit de faire glisser et déposer l’un des boutons Prefab de style HoloLens 2 sur votre scène. Prefab utilise Interactable.cs, qui est présenté ci-dessus. Vous pouvez utiliser des événements exposés tels que OnClick () dans le pour déclencher des actions.

<img alt="HoloLens 2 Button Prefab" width="800" src="images/MRTK101/MRTK_Button.png">

- [En savoir plus sur le bouton prefabs dans la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html)

## <a name="how-to-make-an-object-followyou"></a>Comment faire en sorte qu’un objet suive votre propos ?
Assignez le script RadialView.cs à un objet. Il fait partie de la série de scripts du solveur qui vous permet d’obtenir divers types de positionnement des objets dans l’espace 3D. SolverHandler.cs sera automatiquement ajouté.
Vous trouverez ci-dessous un exemple de configuration de RadialView pour obtenir une balise de suivi tardif, tout comme le menu Démarrer dans l’interpréteur de commandes HoloLens. Vous pouvez spécifier la distance minimale/maximale et les niveaux d’affichage minimal/maximal. L’exemple ci-dessous montre le positionnement de l’objet entre 0,4 mètre et 0,8 m dans la plage de 15 °. Ajustez les valeurs de temps Lerp pour accélérer ou ralentir la mise à jour de position.

<img alt="MRTK Standard Shader" width="400" src="images/MRTK101/MRTK_SolverRadialView.png">

<img alt="Interactable" width="800" src="images/MRTK101/MRTK_RadialViewSolver.gif">

- [En savoir plus sur les programmes de résolution dans la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html)

## <a name="how-to-make-an-object-faceyou"></a>Comment faire face à un objet ?
Assignez le script Billboard.cs à un objet. Elle sera toujours face à vous, quelle que soit votre position. Vous pouvez spécifier l’option d’axe pivot.

<img alt="Billboard.cs script assigned to an object with Pivot Axis option Y" width="800" src="images/MRTK101/MRTK_Billboard.png">

<img alt="Billboard.cs script assigned to an object with Pivot Axis option Y" width="800" src="images/MRTK101/MRTK_Billboard.gif">


Vous êtes prêt à créer des expériences étonnantes pour la réalité mixte ? Visitez les pages ci-dessous et apprenez-en davantage sur MRTK et la réalité mixte.

## <a name="about-the-author"></a>À propos de l'auteur

<table style="border-collapse:collapse" padding-left="0px">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Dong Yoon Park" width="60" height="60" src="images/dongyoonpark.jpg"></td>
<td style="border-style: none"><b>Dong Yoon Park</b><br>@Microsoft du concepteur UX</td>
</tr>
</table>

## <a name="see-also"></a>Articles associés

* [Boîte à outils de réalité mixte-Unity (MRTK) GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity)
* [Portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)
* [Prise en main avec MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html)
* [Indications sur le portage de HoloToolkit à MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/HTKToMRTKPortingGuide.html)
