---
title: Visualisation de maillage spatial
author: cre8ivepark
ms.author: dongpark
ms.date: 06/19/2020
ms.topic: article
keywords: Réalité mixte, HoloLens, contrôles d’interface utilisateur, interaction, interface utilisateur, expérience utilisateur, conception UX, interface utilisateur spatiale, interaction spatiale, interface utilisateur 3D, expérience utilisateur 3D
ms.openlocfilehash: 17a799dcaba5caf4dd7018f8289cad02b40f1277
ms.sourcegitcommit: 7ca383ef1c5dc895ca2a289435f2e9d4c1ee6e65
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85346112"
---
# <a name="spatial-mesh"></a>Maillage spatial

![Maillage spatial](images/UX/MRTK_PulseShader_SpatialMesh.gif)

Grâce à la visualisation de maillage spatial, l’utilisateur peut apprendre comment un appareil perçoit et comprend l’environnement physique. En plus de fournir un contexte spatial, la visualisation de maillage spatial appropriée peut créer une expérience délicieuse et magique.  

## <a name="design-guideline"></a>Directives de conception
Étant donné qu’il est important d’autoriser l’utilisateur à se concentrer et à interagir avec le contenu, la visualisation continue et répétée du maillage spatial en arrière-plan peut être gênante. Il est recommandé de visualiser l’environnement avec modération, qu’une seule fois au lancement initial ou lorsque l’utilisateur montre clairement l’intention de voir la maille environnementale en ciblant et en appuyant sur de l’air. Vous pouvez observer ce comportement dans l’interpréteur de commandes HoloLens.
<br>


## <a name="spatial-mesh-visualization-in-mrtk-mixed-reality-toolkit-for-unity"></a>Visualisation de maillage spatial dans MRTK (ensemble d’outils de réalité mixte) pour Unity
MRTK fournit plusieurs documents pour la visualisation de maillage spatial.

- **MRTK_Wireframe. mat, MRTK_Wireframe. mat**: matériau de maillage spatial statique par défaut qui affiche les contours de maillage sans animation. Ce document est utile à des fins de débogage, car il affiche les géométries entières du maillage spatial. Toutefois, il n’est pas recommandé pour la production.
<br>
<img src="images/SurfaceReconstruction.jpg" alt="Wireframe spatial mesh visualization" width="640px">

- **MRTK_SurfaceReconstruction. mat**: ce matériau vous donne un effet d’impulsion animée sur le maillage spatial. Vous pouvez utiliser ce document pour visualiser l’environnement à un moment précis de votre expérience ou sur l’entrée d’air de l’utilisateur. Consultez la scène **PulseShaderExamples. Unity** pour obtenir des exemples.
<br>
<img src="images/UX/MRTK_SRMesh_Pulse.jpg" alt="Pulse spatial mesh visualization" width="640px">
* Pour plus d’informations, consultez [MRTK-spatial awarenes](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/SpatialAwareness/SpatialAwarenessGettingStarted.html) et [MRTK-Pulse Shader](https://microsoft.github.io/MixedRealityToolkit-Unity/Assets/MRTK/SDK/Experimental/PulseShader/README.html) .

<br>

---

## <a name="see-also"></a>Voir aussi

* [Curseurs](cursors.md)
* [Rayon émanant de la main](point-and-commit.md)
* [Button](button.md)
* [Objet avec interaction possible](interactable-object.md)
* [Rectangle englobant et barre de l’application](app-bar-and-bounding-box.md)
* [Manipulation](direct-manipulation.md)
* [Menu de la main](hand-menu.md)
* [Menu proche](near-menu.md)
* [Collection d’objets](object-collection.md)
* [Commande vocale](voice-input.md)
* [Clavier](keyboard.md)
* [Info-bulle](tooltip.md)
* [Tablette](slate.md)
* [Curseur](slider.md)
* [Nuanceur](shader.md)
* [Billboarding et tag-along](billboarding-and-tag-along.md)
* [Affichage de la progression](progress.md)
* [Aimantation de surface](surface-magnetism.md)
