---
title: Objet interagi
description: Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait en 2D. Dans le monde de la réalité mixte en trois dimensions, nous n’avons plus à limiter le monde de l’abstraction.
author: cre8ivepark
ms.author: jennyk
ms.date: 06/06/2019
ms.topic: article
keywords: Réalité mixte, contrôles, interaction, interface utilisateur, expérience utilisateur
ms.openlocfilehash: 57299cbb758a69603fc68ad5d43af8f2216e5104
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67415355"
---
# <a name="interactable-object"></a>Objet interagi

Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait en 2D. Dans le monde de la réalité mixte en trois dimensions, nous n’avons plus à limiter le monde de l’abstraction. Tout peut être un **objet** pouvant être utilisé qui déclenche un événement. Un objet pouvant être en interaction peut être représenté sous la forme d’un objet à partir d’une tasse de café sur la table. Nous utilisons toujours les boutons traditionnels dans certaines situations, par exemple dans l’interface utilisateur du dialogue. La représentation visuelle du bouton dépend du contexte.

![Objets Interactible](images/640px-interactibleobject-hero-640px.jpg)


## <a name="important-properties-of-the-interactable-object"></a>Propriétés importantes de l’objet interagiable

### <a name="visual-cue"></a>Indicateur visuel

Les signaux visuels sont des signaux sensorielles reçus par l’oeil sous forme de lumière et traités par le système visuel lors de la perception visuelle. Étant donné que le système visuel est dominant dans de nombreuses espèces, en particulier les êtres humains, les signaux visuels constituent une source d’informations importante dans la manière dont le monde est perçu.

En réalité mixte, étant donné que les objets holographiques sont mélangés à l’environnement réel, il peut être difficile de comprendre quels objets sont interactifs. Pour tous les objets interactifs dans votre expérience, il est important de fournir un signal visuel différencié pour chaque État d’entrée. Cela permet à l’utilisateur de comprendre quelle partie de votre expérience est interactive et de faire en sorte que l’utilisateur soit confiant avec la méthode d’interaction cohérente.

#### <a name="far-interactions"></a>Interactions lointaines

Pour tous les objets que l’utilisateur peut interagir avec le point de vue du point de vue du regard, du rayon de la main et du contrôleur de mouvement, nous vous recommandons d’avoir un signal visuel différent pour ces trois États d’entrée:
* **Valeur par défaut (observation)** : État d’inactivité par défaut de l’objet.
* **Ciblé (pointage)** : Lorsque l’objet est ciblé avec un curseur en forme de pointage, le pointeur de proximité d’un doigt ou d’un contrôleur de mouvement.
* **Enfoncé**: Quand l’objet est enfoncé avec un mouvement d’appui sur l’air, appuyez sur le bouton de sélection du contrôleur de mouvement ou de doigt.

Vous pouvez utiliser des techniques telles que la mise en surbrillance ou la mise à l’échelle pour fournir un signal visuel aux États d’entrée de l’utilisateur. Dans Windows Mixed Reality, vous trouverez des exemples de visualisation de différents États d’entrée sur les boutons du menu Démarrer et de la barre de l’application. 

![Exemple de visualisation de l’état d’observation, de l’État ciblé et de l’état appuyé](images/640px-interactibleobject-states.png)<br>
*Exemple de visualisation de l’état d’observation, de l’État ciblé et de l’état appuyé*

![État d’observation, état ciblé et état appuyé sur un bouton holographique](images/MRTK_InteractableState.png)<br>
*État d’observation, état ciblé et état appuyé sur un bouton holographique*

#### <a name="neardirect-interactions"></a>Interactions près (directe)

HoloLens 2 prend en charge l’entrée de suivi articulée qui vous permet d’interagir avec les objets. Sans commentaires haptique et perception parfaite de la profondeur, il peut être difficile de savoir à quel moment votre main provient d’un objet, ou si vous êtes en contact avec vous. Il est important de fournir suffisamment de signaux visuels pour communiquer l’état de l’objet et, en particulier, de vos mains par rapport aux hologrammes.

Utilisez les commentaires visuels pour communiquer les éléments suivants:
* **Valeur par défaut (observation)** : État d’inactivité par défaut de l’objet.
* **Pointage**: Lorsque la main est proche d’un hologramme, modifiez les éléments visuels pour indiquer que la main cible l’hologramme. 
* **Distance et point d’interaction**: À l’approche de l’hologramme, les commentaires de conception pour communiquer le point d’interaction projeté, ainsi que la distance entre l’objet et le doigt
* **Début du contact**: Modifier les éléments visuels (Light, Color) pour indiquer que la fonction tactile s’est produite
* **Saisi**: Modifiez les éléments visuels (clair, couleur) lorsque l’objet est saisi.
* **Fin du contact**: Modifiez les éléments visuels (Light, Color) quand Touch est terminé.

![Exemple de visualisation des États near interaction](images/640px-interactibleobject-states-near.jpg)<br>
*Exemple de visualisation des États near interaction*

Le [bouton dans HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html) montre l’exemple de visualisation de différents États d’interaction d’entrée.

![Exemple de bouton enfoncé dans HoloLens 2](images/640px-interactibleobject-pressablebutton-650px2.jpg)<br>
*Exemple de bouton enfoncé dans HoloLens 2*

Dans HoloLens 2, il existe un indice visuel supplémentaire qui améliore la perception de la profondeur de l’utilisateur. L’anneau à la main s’affiche et est mis à l’échelle à mesure que le doigt se rapproche de l’objet. L’anneau finit par converger vers un point à l’état d’appui. Cet accord visuel aide l’utilisateur à comprendre la distance de l’objet.

![Visualisation de la sonnerie à portée de main](images/640px-interactibleobject-pressablebutton-650px3.jpg)<br>
*Visualisation de la sonnerie de doigt dans HoloLens 2*

![Commentaires visuels à proximité](images/HoloLens2_Proximity.gif)<br>
*Exemple de retour visuel basé sur le cadre englobant de proximité*


### <a name="audio-cue"></a>Signal audio
Pour les interactions directes, les retours audio corrects peuvent améliorer considérablement l’expérience utilisateur. Utilisez les commentaires audio pour communiquer les éléments suivants:
* **Début du contact**: Émettre un signal sonore lors du démarrage de Touch
* **Fin du contact**: Jouer un son à l’extrémité tactile
* **Début**de la manipulation: Émettre un signal sonore lors du démarrage de la manipulation
* **Extraire la fin**: Lire le son à l’extrémité de la capture

### <a name="voice-command"></a>Commande vocale
Pour tous les objets interactifs, il est important de prendre en charge d’autres options d’interaction. Par défaut, il est recommandé de prendre en charge la commande vocale pour tous les objets qui sont interactifs. Pour améliorer la détectabilité, vous pouvez fournir une info-bulle sur l’état de survol.

<img src="images/640px-interactibleobject-voicecommand.jpg" alt="Tooltip for the voice command" title="Info-bulle pour la commande vocale" width="350"><br/>*Info-bulle pour la commande vocale*

## <a name="sizing"></a>Dimensionnement
Pour vous assurer que tous les objets interactifs peuvent facilement être manipulés par les utilisateurs, nous vous recommandons de vous assurer que l’interagissant est conforme à une taille minimale (l’angle visuel souvent mesuré en degrés d’arc visuel) en fonction de la distance qu’il est placée par l’utilisateur. L’angle visuel est basé sur la distance entre les yeux de l’utilisateur et l’objet et reste constant, tandis que la taille physique de la cible peut changer en fonction de la distance entre les modifications de l’utilisateur. Pour déterminer la taille physique nécessaire d’un objet en fonction de la distance de l’utilisateur, essayez d’utiliser une calculatrice d’angle visuel telle que celle- [ci](http://elvers.us/perception/visualAngle/).

Vous trouverez ci-dessous les recommandations relatives aux tailles minimales de contenu exploitable.

### <a name="target-size-for-direct-hand-interaction"></a>Taille cible pour l’interaction directe
| distance | Angle d’affichage | Size |
|---------|---------|---------|
| 45cm  | non inférieur à 2 ° | 1,6 x 1,6 cm |

![Taille cible pour l’interaction directe](images/TargetSizingNear.jpg)<br>
*Taille cible pour l’interaction directe*

Lorsque vous créez des boutons pour une interaction directe, nous vous recommandons une taille minimale supérieure de 3,2 x 3,2 cm pour garantir qu’il y a suffisamment d’espace pour contenir une icône et éventuellement du texte * *

| distance | Taille minimale |
|---------|---------|
| 45cm  | 3,2 x 3,2 cm |

![Taille cible pour les boutons](images/TargetSizingButtons.png)<br>
*Taille cible pour les boutons*


### <a name="target-size-for-hand-ray-or-gaze-interaction"></a>Taille cible pour un rayon de la main ou une interaction du regard
| distance | Angle d’affichage | Size |
|---------|---------|---------|
| dollars  | inférieur à 1 ° | 3,5 x 3,5 cm |

![Taille cible pour un rayon de la main ou une interaction du regard](images/TargetSizingFar.jpg)<br>
*Taille cible pour un rayon de la main ou une interaction du regard*

## <a name="creating-interactable-object-with-mixed-reality-toolkit-mrtk"></a>Création d’un objet interactif avec Mixed Reality Toolkit (MRTK)

Dans la **[boîte à outils de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity)** , vous trouverez la série de scripts Unity et de prefabs qui vous aideront à créer des objets interactifs. Vous pouvez les utiliser pour faire en sorte que les objets répondent à différents types d’États d’interaction d’entrée.

* [Sur](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html)
* [Button](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html)
* [Scène d’exemples d’interaction manuelle](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_HandInteractionExamples.md)

Le nuanceur standard de MixedRealityToolkit fournit diverses options telles que la **lumière de proximité** qui vous aide à créer des signaux visuels et audio.
* [Nuanceur standard MRTK](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_MRTKStandardShader.md)


## <a name="see-also"></a>Voir aussi

* [Cadre englobant](app-bar-and-bounding-box.md)
* [Collection d’objets](object-collection.md)
* [Billboarding et tag-along](billboarding-and-tag-along.md)