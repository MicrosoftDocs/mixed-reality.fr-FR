---
title: Objet interagi
description: Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait en 2D. Dans le monde de la réalité mixte en trois dimensions, nous n’avons plus à limiter le monde de l’abstraction.
author: cre8ivepark
ms.author: jennyk
ms.date: 06/06/2019
ms.topic: article
keywords: Réalité mixte, contrôles, interaction, interface utilisateur, expérience utilisateur
ms.openlocfilehash: 87979d2d7b7de4a384b42b5059239e9b830a92e8
ms.sourcegitcommit: 6844930427b658ae31f642c395cd8a3b3cdbf857
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75723228"
---
# <a name="interactable-object"></a>Objet interagi

![Objets Interactible](images/UX/UX_Hero_Interactable.jpg)

Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait en 2D. Dans le monde de la réalité mixte en trois dimensions, nous n’avons plus à limiter le monde de l’abstraction. Tout peut être un **objet** pouvant être utilisé qui déclenche un événement. Un objet pouvant être en interaction peut être représenté sous la forme d’un objet à partir d’une tasse de café sur la table. Nous utilisons toujours les boutons traditionnels dans certaines situations, par exemple dans l’interface utilisateur du dialogue. La représentation visuelle du bouton dépend du contexte.

<br>

---


## <a name="important-properties-of-the-interactable-object"></a>Propriétés importantes de l’objet interagiable

### <a name="visual-cues"></a>Signaux visuels

Les signaux visuels sont des signaux sensorielles reçus par l’oeil sous forme de lumière et traités par le système visuel lors de la perception visuelle. Étant donné que le système visuel est dominant dans de nombreuses espèces, en particulier les êtres humains, les signaux visuels constituent une source d’informations importante dans la manière dont le monde est perçu.

Étant donné que les objets holographiques sont mélangés à l’environnement réel dans la réalité mixte, il peut être difficile de comprendre les objets avec lesquels vous pouvez interagir. Pour tous les objets interactifs dans votre expérience, il est important de fournir des signaux visuels différenciés pour chaque État d’entrée. Cela permet à l’utilisateur de comprendre quelle partie de votre expérience est interactive et de rendre l’utilisateur confiant en utilisant une méthode d’interaction cohérente.

<br>

---

### <a name="far-interactions"></a>Interactions lointaines

Pour tous les objets que l’utilisateur peut interagir avec le point de vue du point de vue du regard, du rayon de la main et du contrôleur de mouvement, nous vous recommandons d’avoir un signal visuel différent pour ces trois États d’entrée :

:::row:::
    :::column:::
       ![interactibleobject-States-](images/interactibleobject-states-default.jpg) par défaut<br>
       **État par défaut (observation)**<br>
        État d’inactivité par défaut de l’objet.
    Le curseur ne se trouve pas sur l’objet. La main n’est pas détectée.
    :::column-end:::
    :::column:::
       ![interactibleobject-États-ciblés](images/interactibleobject-states-targeted.jpg)<br>
        **État ciblé (survol)**<br>
        Lorsque l’objet est ciblé avec un curseur en forme de pointage, le pointeur de proximité d’un doigt ou d’un contrôleur de mouvement.
    Le curseur se trouve sur l’objet. La main est détectée, prête.
    :::column-end:::
    :::column:::
       ![interactibleobject-l’utilisateur a appuyé sur](images/interactibleobject-states-pressed.jpg)<br>
       **État appuyé**<br>
        Quand l’objet est enfoncé avec un mouvement d’appui sur l’air, appuyez sur le bouton de sélection du contrôleur de mouvement ou du doigt.
    Le curseur se trouve sur l’objet. La main est détectée, frappée d’air.
    :::column-end:::
:::row-end:::

<br>

---

Vous pouvez utiliser des techniques telles que la mise en surbrillance ou la mise à l’échelle pour fournir des signaux visuels pour l’état d’entrée de l’utilisateur. En réalité mixte, vous trouverez les exemples de visualisation des différents États d’entrée dans le menu Démarrer et avec les boutons de la barre d’application. 

Voici à quoi ressemblent ces États sur un **bouton holographique**:

:::row:::
    :::column:::
       ![interactibleobject-States-](images/MRTK_InteractableState-default.jpg) par défaut<br>
       **État par défaut (observation)**<br>
    :::column-end:::
    :::column:::
       ![interactibleobject-États-ciblés](images/MRTK_InteractableState-targeted.jpg)<br>
        **État ciblé (survol)**<br>
    :::column-end:::
    :::column:::
       ![interactibleobject-l’utilisateur a appuyé sur](images/MRTK_InteractableState-pressed.jpg)<br>
       **État appuyé**<br>
    :::column-end:::
:::row-end:::

<br>

---

### <a name="near-interactions-direct"></a>Interactions proches (direct) 

HoloLens 2 prend en charge l’entrée de suivi articulée qui vous permet d’interagir avec les objets. Sans commentaires haptique et perception parfaite de la profondeur, il peut parfois être difficile de savoir à quel moment votre main provient d’un objet ou si vous le touchez. Il est important de fournir suffisamment de signaux visuels pour communiquer l’état de l’objet et, en particulier, l’état de vos mains par rapport à cet objet.

Utilisez les commentaires visuels pour communiquer les éléments suivants :
* **Valeur par défaut (observation)** : état inactif par défaut de l’objet.
* **Survol**: quand une main est proche d’un hologramme, modifiez les éléments visuels pour indiquer que la main cible l’hologramme. 
* **Distance et point d’interaction**: comme la main s’approche d’un hologramme, concevoir des commentaires pour communiquer le point d’interaction projeté, ainsi que la distance entre l’objet et le doigt
* **Début du contact**: modifiez les éléments visuels (Light, Color) pour signaler qu’une pression tactile s’est produite.
* **Saisi**: modifier les éléments visuels (clair, couleur) quand l’objet est saisi
* **Fin du contact**: modifier les éléments visuels (Light, Color) quand Touch est terminé

<br>

---

:::row:::
    :::column:::
        ![pointage (FAR)](images/640px-interactibleobject-states-near-hover.jpg)<br>
        **Pointage (FAR)**<br>
        Mise en surbrillance en fonction de la proximité de la main.
    :::column-end:::
    :::column:::
        Pointage de ![(Near)](images/640px-interactibleobject-states-near-hovernear.jpg)<br>
        **Pointage (Near)**<br>
        Mettez en surbrillance les changements de taille en fonction de la distance à la main.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        ![toucher/appuyer](images/640px-interactibleobject-states-near-press.jpg)<br>
        **Toucher/appuyer**<br>
        Commentaires Audio Visual plus.
    :::column-end:::
    :::column:::
        ![](images/640px-interactibleobject-states-near-grasp.jpg)<br>
        **Maîtriser**<br>
        Commentaires Audio Visual plus.
    :::column-end:::
:::row-end:::

<br>

<br>

---

Un [bouton sur HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html) est un exemple de la façon dont les différents États d’interaction d’entrée sont visualisés :

:::row:::
    :::column:::
        ![Par défaut](images/640px-interactibleobject-pressablebutton-default.jpg)<br>
        **Par défaut**<br>
    :::column-end:::
    :::column:::
        Pointage de ![](images/640px-interactibleobject-pressablebutton-hover.jpg)<br>
        **Pointez**<br>
        Révélez un effet d’éclairage basé sur la proximité.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        ![Interface tactile](images/640px-interactibleobject-pressablebutton-touch.jpg)<br>
        **Interface tactile**<br>
        Afficher l’effet de l’ondulation.
    :::column-end:::
    :::column:::
        ![Appuyez sur](images/640px-interactibleobject-pressablebutton-press.jpg)<br>
        **Appuyez sur**<br>
        Déplacez la plaque avant.
    :::column-end:::
:::row-end:::

<br>

---

:::row:::
    :::column:::
        ### <a name="the-ring-visual-cue-on-hololens-2br"></a>Le signal visuel « Ring » sur HoloLens 2<br>
        Sur HoloLens 2, il existe un signal visuel supplémentaire qui peut aider la perception de l’utilisateur en profondeur. Un anneau proche de son doigt s’affiche et s’adapte à mesure que l’approche est plus proche de l’objet. L’anneau se convergera en un point lorsque l’état appuyé est atteint. Cet accord visuel aide l’utilisateur à comprendre à quel moment il s’agit de l’objet.<br>
        <br>
        *Boucle vidéo : exemple de retour visuel basé sur la proximité d’un cadre englobant*
    :::column-end:::
        :::column:::
        ![space](images/spacer-20x582.png)<br>
       ![des commentaires visuels à proximité](images/HoloLens2_Proximity.gif)<br>
    :::column-end:::
:::row-end:::


<br>

---


### <a name="audio-cues"></a>Signaux audio

Pour les interactions directes, les retours audio corrects peuvent améliorer considérablement l’expérience utilisateur. Utilisez les commentaires audio pour communiquer les éléments suivants :
* **Début du contact**: émettre un signal sonore à la début de la saisie tactile
* Fin du **contact**: émettre un signal sonore à l’extrémité tactile
* **Début**de la manipulation : émettre un signal sonore lors du démarrage de la manipulation
* Opérations de **manipulation**: émettre un signal sonore lorsque la sélection est terminée

<br>

---

:::row:::
    :::column:::
        ### <a name="voice-commandingbr"></a>Commander avec la voix<br>
        Pour tous les objets interactifs, il est important de prendre en charge d’autres options d’interaction. Par défaut, nous vous recommandons de prendre en charge les [commandes vocales](voice-design.md) pour tous les objets qui sont interactifs. Pour améliorer la détectabilité, vous pouvez également fournir une info-bulle pendant l’état de survol.<br>
        <br>
        *Image : info-bulle pour la commande vocale*
    :::column-end:::
        :::column:::
       ![commandes vocales](images/640px-interactibleobject-voicecommand.png)<br>
    :::column-end:::
:::row-end:::


<br>

---


## <a name="sizing-recommendations"></a>Recommandations de dimensionnement 

Pour vous assurer que tous les objets interactifs peuvent facilement être manipulés par les utilisateurs, nous vous recommandons de vous assurer que l’interagissant est conforme à une taille minimale (l’angle visuel souvent mesuré en degrés d’arc visuel) en fonction de la distance qu’il est placée par l’utilisateur. L’angle visuel est basé sur la distance entre les yeux de l’utilisateur et l’objet et reste constant, tandis que la taille physique de la cible peut changer en fonction de la distance entre les modifications de l’utilisateur. Pour déterminer la taille physique nécessaire d’un objet en fonction de la distance de l’utilisateur, essayez d’utiliser une calculatrice d’angle visuel telle que celle- [ci](https://elvers.us/perception/visualAngle/).

Vous trouverez ci-dessous les recommandations relatives aux tailles minimales de contenu exploitable.


### <a name="target-size-for-direct-hand-interaction"></a>Taille cible pour l’interaction directe

| Distance | Angle d’affichage | Taille |
|---------|---------|---------|
| 45cm  | non inférieur à 2 ° | 1,6 x 1,6 cm |

![taille cible pour l’interaction directe](images/TargetSizingNear.jpg)<br>
*Taille cible pour l’interaction directe*

<br>

### <a name="target-size-for-buttons"></a>Taille cible pour les boutons

Lorsque vous créez des boutons pour une interaction directe, nous vous recommandons une taille minimale supérieure de 3,2 x 3,2 cm pour garantir qu’il y a suffisamment d’espace pour contenir une icône et éventuellement du texte.

| Distance | Taille minimale |
|---------|---------|
| 45cm  | 3,2 x 3,2 cm |

![taille cible pour les boutons](images/TargetSizingButtons.png)<br>
*Taille cible pour les boutons*

<br>

### <a name="target-size-for-hand-ray-or-gaze-interaction"></a>Taille cible pour un rayon de la main ou une interaction du regard
| Distance | Angle d’affichage | Taille |
|---------|---------|---------|
| dollars  | inférieur à 1 ° | 3,5 x 3,5 cm |

![taille cible pour les](images/TargetSizingFar.jpg) de rayon ou d’interaction de regard<br>
*Taille cible pour un rayon de la main ou une interaction du regard*


<br>

---


## <a name="interactable-object-in-mrtk-mixed-reality-toolkit-for-unity"></a>Objet interactif dans MRTK (ensemble d’outils de réalité mixte) pour Unity

Dans **[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)** , vous pouvez utiliser le script en [**interaction**](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.SDK/Features/UX/Interactable/Scripts) pour faire en sorte que les objets répondent à différents types d’États d’interaction d’entrée. Il prend en charge différents types de thèmes qui vous permettent de définir des États visuels en contrôlant des propriétés d’objet telles que la couleur, la taille, le matériau et le nuanceur.

* [Sur](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html)
* [Button](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html)
* [Scène d’exemples d’interaction manuelle](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_HandInteractionExamples.md)

Le nuanceur standard de MixedRealityToolkit fournit diverses options telles que la **lumière de proximité** qui vous aide à créer des signaux visuels et audio.
* [Nuanceur standard MRTK](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_MRTKStandardShader.md)


<br>

---


## <a name="see-also"></a>Articles associés

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
