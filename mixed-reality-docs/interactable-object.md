---
title: Objet sur
description: Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait 2D. Dans le monde en trois dimensions de réalité mixte, nous n’êtes pas obligé d’être limitées à ce monde d’abstraction plus.
author: cre8ivepark
ms.author: jennyk
ms.date: 02/24/2019
ms.topic: article
keywords: Réalité mixte, contrôles, interaction, l’interface utilisateur, l’expérience utilisateur
ms.openlocfilehash: f349d21707375690e00b0f7e465634c62be1537e
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594762"
---
# <a name="interactable-object"></a>Objet sur

Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait 2D. Dans le monde en trois dimensions de réalité mixte, nous n’êtes pas obligé d’être limitées à ce monde d’abstraction plus. Quoi que ce soit peut être un **sur objet** qui déclenche un événement. Un objet sur peut être représenté en tant que quoi que ce soit à partir d’une tasse de café sur la table à une info-bulle flottante en l’air. Que nous apporterons toujours l’utilisation de boutons traditionnel dans certains cas, par exemple, dans la boîte de dialogue interface utilisateur. La représentation visuelle du bouton dépend du contexte.

![Image de héros objet interactible](images/640px-interactibleobject-hero-640px.jpg)


Dans le  **[Toolkit de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity)**, nous avons créé une série de scripts Unity et prefabs qui vous aideront à créer des objets sur. Vous pouvez les utiliser pour créer n’importe quel type d’objet que l’utilisateur peut interagir avec, à l’aide de ces États interaction standard : observation, ciblés et enfoncé. Vous pouvez facilement personnaliser la conception visuelle avec vos propres ressources. Animations détaillées peuvent être personnalisées en créant et affectation des clips d’animation correspondant pour les États d’interaction dans le contrôleur de l’animation d’Unity ou à l’aide de décalage et mise à l’échelle. 


## <a name="visual-feedback-for-the-different-input-interaction-states"></a>Commentaires visuels pour les États de l’interaction d’entrée différents

En réalité mixte, étant donné que les objets HOLOGRAPHIQUE sont combinées avec l’environnement réel, il pourrait être difficile de comprendre quels objets sont sur. Pour les objets sur votre expérience, il est important de fournir des commentaires visuels différenciées pour chaque état d’entrée. Cela permet à l’utilisateur de comprendre quelle partie de votre expérience est sur et fait certain de l’utilisateur avec la méthode d’interaction cohérent.

Pour tous les objets que l’utilisateur peut interagir avec, il est recommandé d’avoir des commentaires visuels différents pour ces trois d’entrée des États :
* **Observation**: État d’inactivité par défaut de l’objet.
* **Ciblés**: Pointeur de contrôleur proximité ou de mouvement doigt par quand l’objet est ciblé avec regards curseur.
* **Enfoncé**: Lorsque l’objet est activé avec le geste d’appui de l’air, appuyez sur le doigt ou bouton de sélection du contrôleur de mouvement.

![Bouton HOLOGRAPHIQUE](images/640px-interactibleobject-holographicbutton-650px.jpg)<br>
*État de l’observation, ciblées d’état et état enfoncé*

Dans Windows Mixed Reality, vous pouvez trouver les exemples de visualiser les différents États d’entrée sur le menu Démarrer et des boutons de barre de l’application. Vous pouvez utiliser des techniques telles que la mise en surbrillance ou de mise à l’échelle pour fournir des commentaires visuels aux États d’entrée de l’utilisateur.

Dans les 2 HoloLens, dans la mesure où il prend en charge entièrement articulé main suivi d’entrée, nous pouvons fournir intuitivité supplémentaires en fonction de la proximité entre les mains. Le [bouton HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html) montre cet exemple.

![Bouton PRESSEE](images/640px-interactibleobject-pressablebutton-650px.jpg)<br>




## <a name="interactable-object-samples"></a>Exemples de l’objet sur

### <a name="mesh-button"></a>Bouton de maillage

![Bouton de maillage](images/640px-interactibleobject-meshbutton.jpg)

Voici des exemples à l’aide de primitives et des maillages 3D importés en tant qu’objets sur. Vous pouvez facilement attribuer différentes valeurs de couleur, le décalage et mise à l’échelle pour répondre à chaque état de l’interaction d’entrée.

### <a name="toolbar"></a>Barre d’outils

![Barre d’outils](images/640px-interactibleobject-toolbar.jpg)

Une barre d’outils est un modèle largement utilisé dans les expériences de réalité mixte. Il est une simple collection de boutons avec des comportements supplémentaires telles que [Billboarding et tag-along](billboarding-and-tag-along.md). Cet exemple utilise un script Billboarding et tag-along à partir de la MixedRealityToolkit. Vous pouvez contrôler les comportements détaillées, y compris la distance, déplacer des valeurs de vitesse et de seuil.

### <a name="traditional-button"></a>Bouton classique

![Bouton classique](images/640px-interactibleobject-traditionalbutton.jpg)

Cet exemple montre un bouton de style 2D traditionnel. Chaque état d’entrée a une profondeur légèrement différente et la propriété d’animation.

### <a name="other-examples"></a>Autres exemples

![Bouton de commande](images/640px-interactibleobject-pushbutton.jpg)<br>
*Bouton de commande*
<br>
![Objet de durée de vie réel](images/640px-interactibleobject-reallifeobject.jpg)<br>
*Objet de la vie réelle*

Avec HoloLens, vous pouvez tirer parti d’espace physique. Imaginez un bouton de commande HOLOGRAPHIQUE sur un mur physique. Ou est-il une tasse de café sur une table réelle ? À l’aide des modèles 3D importés de modéliser le logiciel, nous pouvons créer un objet sur qui ressemble à des objets de la vie réelle. Dans la mesure où il s’agit d’un objet numérique, nous pouvons ajouter des interactions magiques à celui-ci.

## <a name="interactable-object-in-mixed-reality-toolkit"></a>Objet sur dans la boîte à outils de réalité mixte
Vous pouvez trouver le [exemples de Interactable de l’objet dans la boîte à outils de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html)


## <a name="see-also"></a>Voir aussi
* [Bouton PRESSEE de réalité mixte Toolkit-Unity](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html)
* [Collection d’objets](object-collection.md)
* [Le billboarding et tag-along](billboarding-and-tag-along.md)
