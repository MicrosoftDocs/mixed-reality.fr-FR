---
title: Objet sur
description: Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait 2D. Dans le monde en trois dimensions de réalité mixte, nous n’êtes pas obligé d’être limitées à ce monde d’abstraction plus.
author: cre8ivepark
ms.author: jennyk
ms.date: 06/06/2019
ms.topic: article
keywords: Réalité mixte, contrôles, interaction, l’interface utilisateur, l’expérience utilisateur
ms.openlocfilehash: 57299cbb758a69603fc68ad5d43af8f2216e5104
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67415355"
---
# <a name="interactable-object"></a>Objet sur

Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait 2D. Dans le monde en trois dimensions de réalité mixte, nous n’êtes pas obligé d’être limitées à ce monde d’abstraction plus. Quoi que ce soit peut être un **sur objet** qui déclenche un événement. Un objet sur peut être représenté en tant que quoi que ce soit à partir d’une tasse de café sur la table à une info-bulle flottante en l’air. Que nous apporterons toujours l’utilisation de boutons traditionnel dans certains cas, par exemple, dans la boîte de dialogue interface utilisateur. La représentation visuelle du bouton dépend du contexte.

![Objets interactible](images/640px-interactibleobject-hero-640px.jpg)


## <a name="important-properties-of-the-interactable-object"></a>Propriétés importantes de l’objet sur

### <a name="visual-cue"></a>Signal visuel

Signaux visuels sont des signaux sensoriels reçus par le œil sous la forme de la lumière et traités par le système visual au cours de la perception visuelle. Étant donné que le système visual est dominant de nombreuses espèces, en particulier les humains, signaux visuels sont une grande source d’informations dans la façon dont le monde est perçu.

En réalité mixte, étant donné que les objets HOLOGRAPHIQUE sont combinées avec l’environnement réel, il pourrait être difficile de comprendre quels objets sont sur. Pour les objets sur votre expérience, il est important de fournir des indice visuel différenciée pour chaque d’entrée d’état. Cela permet à l’utilisateur de comprendre quelle partie de votre expérience est sur et fait certain de l’utilisateur avec la méthode d’interaction cohérent.

#### <a name="far-interactions"></a>Interactions lointain

Pour tous les objets que l’utilisateur peut interagir avec pointage de regard, ray de main et ray du contrôleur de mouvement, nous vous recommandons d’avoir différents visuelle de ces trois états d’entrée :
* **Par défaut (Observation)** : État d’inactivité par défaut de l’objet.
* **Ciblé (pointage)** : Pointeur de contrôleur proximité ou de mouvement doigt par quand l’objet est ciblé avec regards curseur.
* **Enfoncé**: Lorsque l’objet est activé avec le geste d’appui de l’air, appuyez sur le doigt ou bouton de sélection du contrôleur de mouvement.

Vous pouvez utiliser des techniques telles que la mise en surbrillance ou de mise à l’échelle pour fournir une indication visuelle aux États d’entrée de l’utilisateur. Dans Windows Mixed Reality, vous pouvez trouver les exemples de visualiser les différents États d’entrée sur le menu Démarrer et des boutons de barre de l’application. 

![Exemple de visualiser l’état de l’observation, ciblées d’état et état enfoncé](images/640px-interactibleobject-states.png)<br>
*Exemple de visualiser l’état de l’observation, ciblées d’état et état enfoncé*

![État de l’observation, ciblées état et état enfoncé sur bouton HOLOGRAPHIQUE](images/MRTK_InteractableState.png)<br>
*État de l’observation, ciblées état et état enfoncé sur bouton HOLOGRAPHIQUE*

#### <a name="neardirect-interactions"></a>Interactions de NEAR(direct)

HoloLens 2 prend en charge la main articulé d’entrée qui vous permet d’interagir avec les objets de suivi. Sans retour haptique et perception de profondeur parfaite parfois, il peut être difficile de déterminer l’éloignement votre main provient d’un objet, ou si vous touche. Il est important de fournir des aides visuelles suffisamment pour communiquer l’état de l’objet et en particulier vos mains par rapport à hologrammes.

Utiliser des commentaires visuels pour communiquer les éléments suivants :
* **Par défaut (Observation)** : État d’inactivité par défaut de l’objet.
* **Placez le curseur**: Lorsque main près un hologramme, modification des éléments visuels pour communiquer la main est ciblé par hologramme. 
* **Distance et le point d’interaction**: Main approche HOLOGRAMME, concevoir des commentaires pour communiquer le point projeté d’interaction, ainsi que la manière dont loin d’être l’objet est le doigt
* **Contactez Begin**: Modification des éléments visuels (clair, couleur) pour communiquer ce tactile s’est produite
* **Fait saisi en**: Modifier les éléments visuels (clair, couleur) lorsque l’objet est saisi.
* **Contactez fin**: Modifier les éléments visuels (clair, couleur) lorsque tactile est terminée.

![Exemple de visualisation de près les États d’interaction](images/640px-interactibleobject-states-near.jpg)<br>
*Exemple de visualisation de près les États d’interaction*

Le [bouton HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html) montre l’exemple de visualiser l’interaction d’entrée différents états.

![Exemple de bouton PRESSEE dans HoloLens 2](images/640px-interactibleobject-pressablebutton-650px2.jpg)<br>
*Exemple de bouton PRESSEE dans HoloLens 2*

Dans 2 HoloLens, il existe un indice visuel supplémentaire, ce qui améliore le niveau de confiance de l’utilisateur sur la perception de profondeur. L’anneau extérieur sur le bout des doigts s’affiche et met à l’échelle vers le bas comme le bout des doigts se rapproche davantage à l’objet. L’anneau recouvre dans un point sur l’état de la presse. Ce visuel intuitif aide l’utilisateur à comprendre la distance à partir de l’objet.

![Visualisation d’anneau le bout des doigts](images/640px-interactibleobject-pressablebutton-650px3.jpg)<br>
*Visualisation d’anneau le bout des doigts dans HoloLens 2*

![Commentaires visuels sur la proximité de main](images/HoloLens2_Proximity.gif)<br>
*Exemple d’une rétroaction visuelle en fonction de la proximité - le rectangle englobant*


### <a name="audio-cue"></a>Signal audio
Pour les interactions directes main, des commentaires audio approprié peuvent améliorer considérablement l’expérience utilisateur. Utiliser des commentaires audio pour communiquer les éléments suivants :
* **Contact commencer**: Émettre un son lorsque touch commence
* **Fin de contact**: Émettre un son sur tactile principal
* **Manipulation commencer**: Émettre un son au démarrage de manipulation
* **Saisir fin**: Lire le son sur la fin de la manipulation

### <a name="voice-command"></a>Commande vocale
Pour tous les objets sur, il est important prendre en charge les options d’autre interaction. Par défaut, il est recommandé pour prendre en charge les commandes vocales pour tous les objets qui sont sur. Pour améliorer la détectabilité, vous pouvez fournir des info-bulle sur l’état de pointage.

<img src="images/640px-interactibleobject-voicecommand.jpg" alt="Tooltip for the voice command" title="Info-bulle pour les commandes vocales" width="350"><br/>*Info-bulle pour les commandes vocales*

## <a name="sizing"></a>Dimensionnement
Pour vous assurer que tous les objets sur peuvent facilement être manipulés par les utilisateurs, nous vous recommandons de vérifier que le satisfait sur une taille minimale (angle visual souvent mesurée en degrés d’arc visual) basé sur la distance, qu'il est placé à partir de l’utilisateur. Angle Visual est basé sur la distance entre les yeux de l’utilisateur et de l’objet et reste constant, alors que la taille physique de la cible peut changer en tant que la distance à partir de l’utilisateur change. Pour déterminer la taille physique nécessaires d’un objet basé sur la distance à partir de l’utilisateur, essayez d’utiliser une calculatrice visual angle comme [celui-ci](http://elvers.us/perception/visualAngle/).

Voici les recommandations pour les tailles minimale du contenu sur.

### <a name="target-size-for-direct-hand-interaction"></a>Taille cible pour l’interaction directe main
| Distance | Angle de visualisation | Size |
|---------|---------|---------|
| 45cm  | non inférieure à 2° | 1.6 1,6 cm |

![Taille cible pour l’interaction directe main](images/TargetSizingNear.jpg)<br>
*Taille cible pour l’interaction directe main*

Lorsque vous créez des boutons pour l’interaction directe, nous vous recommandons une plus grande taille minimale de cm x 3.2 3.2 pour vous assurer que suffisamment d’espace pour contenir une icône et potentiellement certains texte **

| Distance | Taille minimale |
|---------|---------|
| 45cm  | 3.2 x 3.2 cm |

![Taille cible pour les boutons](images/TargetSizingButtons.png)<br>
*Taille cible pour les boutons*


### <a name="target-size-for-hand-ray-or-gaze-interaction"></a>Taille de rayon de main cible ou l’utilisation d’interaction
| Distance | Angle de visualisation | Size |
|---------|---------|---------|
| 2m  | non inférieure à 1° | 3.5 3,5 cm |

![Taille de rayon de main cible ou l’utilisation d’interaction](images/TargetSizingFar.jpg)<br>
*Taille de rayon de main cible ou l’utilisation d’interaction*

## <a name="creating-interactable-object-with-mixed-reality-toolkit-mrtk"></a>Création d’objet sur avec le Kit de ressources de réalité mixte (MRTK)

Dans le  **[Toolkit de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity)** , vous pouvez trouver la série de scripts Unity et prefabs qui vous aideront à créer des objets sur. Vous pouvez les utiliser pour rendre les objets à répondre aux différents types d’états de l’interaction d’entrée.

* [Interactable](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html)
* [Button](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html)
* [Scène d’exemples main interaction](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_HandInteractionExamples.md)

Nuanceur Standard du MixedRealityToolkit offre différentes options telles que **light de proximité** qui vous permet de créer des signaux visuels et audio.
* [Nuanceur Standard MRTK](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_MRTKStandardShader.md)


## <a name="see-also"></a>Voir aussi

* [zone englobante](app-bar-and-bounding-box.md)
* [Collection d’objets](object-collection.md)
* [Billboarding et tag-along](billboarding-and-tag-along.md)