---
title: Menu de la main
description: Les menus manuels permettent aux utilisateurs d’afficher rapidement une interface utilisateur attachée à la main pour les fonctions fréquemment utilisées. Voici nos meilleures pratiques et recommandations pour les menus manuels.
author: nbarragan23
ms.author: nobarr
ms.date: 08/27/2019
ms.topic: article
keywords: main, menu, bouton, accès rapide, disposition
ms.openlocfilehash: d1d15b36bab2ca2082ca4ba91b9c64862893f80c
ms.sourcegitcommit: fef42e2908e49822f2d13b05d2f9260bf0d72158
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86061165"
---
# <a name="hand-menu"></a>Menu de la main

![Emplacement de la main ulnar](images/UX/UX_Hero_HandMenu.jpg)

Le menu de la main est l’un des modèles d’expérience utilisateur les plus uniques dans HoloLens 2. Elle vous permet d’accéder rapidement à une interface utilisateur jointe à la main. Étant donné qu’il est accessible à tout moment et peut être affiché et masqué facilement, c’est parfait pour les actions rapides.

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4AJAg]

Vous trouverez nos meilleures pratiques recommandées pour l’utilisation des menus manuels dans la liste ci-dessous. Vous trouverez également un exemple de scène illustrant le menu manuel dans [MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_HandMenu.html).

<br>


---

## <a name="best-practices"></a>Meilleures pratiques
**Conserver le nombre de boutons petit** 

En raison de la distance étroite entre un menu verrouillé et les yeux, ainsi que la tendance de l’utilisateur à se concentrer sur une zone visuelle relativement petite à tout moment (le cône de vision est à peu près 10 degrés), nous vous recommandons de laisser le nombre de boutons petit. Sur la base de notre exploration, une colonne avec trois boutons fonctionne bien en conservant tout le contenu dans le champ de vision (l’angle d’accès) même lorsqu’un utilisateur passe au centre de l’angle d’utilisation. 

**Utiliser le menu manuellement pour une action rapide** 

L’élévation d’un bras et la maintenance de la position peuvent facilement entraîner une fatigue du bras. Utilisez une méthode verrouillée à la main pour le menu nécessitant une faible interaction. Si votre menu est complexe et nécessite des temps d’interaction étendus, envisagez d’utiliser à la place un verrou universel ou verrouillé. 

**Angle du bouton/du panneau**

Les menus doivent s’afficher à l’épaule opposé et au milieu de la tête : cela permet à une main naturelle d’interagir avec le menu avec la main opposée et évite les positions difficiles ou inconfortables quand vous touchez des boutons. 

**Envisagez de prendre en charge une opération à la main ou mains libres**

Ne partez pas du principe que les deux mains de l’utilisateur sont toujours disponibles. Considérez un large éventail de contextes quand l’un ou l’autre des mains n’est pas disponible, et assurez-vous que votre conception compte pour ces situations. Pour prendre en charge un menu contextuel à un seul mains, vous pouvez essayer de passer le positionnement du menu de façon à ce qu’il passe à l’état verrouillé à l’extérieur lorsque la main est tournée (s’affiche à l’écran). Pour les scénarios mains libres, envisagez d’utiliser une commande vocale pour appeler le menu de la main.

**Évitez d’ajouter des boutons près du poignet (bouton de démarrage du système)**

Si les boutons de menu de la main sont placés trop près du bouton d’origine, ils peuvent se déclencher accidentellement lors de l’interaction avec le menu de la main.

<br>

## <a name="hand-menu-with-large-and-complex-ui-controls"></a>Menu manuel avec des contrôles d’interface utilisateur volumineux et complexes
<img src="images/UX/HandMenu_SizeExample.png" alt="HoloLens perspective of a menu system that always faces the user" width="940px">
Il est recommandé de limiter le nombre de boutons ou de contrôles d’interface utilisateur dans les menus attachés à la main. Cela est dû au fait que l’interaction étendue avec un grand nombre d’éléments d’interface utilisateur peut entraîner une fatigue ARM. Si votre expérience requiert un grand menu, fournissez un moyen facile pour l’utilisateur de verrouiller le menu. L’une des techniques recommandées est l’utilisation de l’option de verrouillage universel lorsque la main chute ou s’éloigne de l’utilisateur. Une seconde technique consiste à autoriser l’utilisateur à saisir directement le menu en revanche. Quand l’utilisateur relâche le menu, le menu doit être un verrou universel. De cette façon, un utilisateur peut interagir avec les différents éléments de l’interface utilisateur de manière conviviale et en toute confiance sur une période prolongée. 

Lorsque le menu est verrouillé dans le monde entier, veillez à fournir un moyen de déplacer le menu, puis fermez le menu lorsqu’il n’est plus nécessaire. Rendez le menu déplaçable en fournissant des poignées sur les côtés ou en haut du menu. Ajoutez un bouton Fermer pour permettre au menu de se fermer. Autoriser le menu à se rattacher à la main lorsque l’utilisateur est confronté à l’utilisateur. Nous vous recommandons également de demander à ce que les utilisateurs pointent à la main pour empêcher les fausses activations (voir ci-dessous).

**Grand menu présentant un problème d’utilisation**

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4AOPx]

**Menu déroulant à la main**

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4AGZi]

**Récupération manuelle & de l’extraction dans le monde entier-verrouiller le menu**

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4AJAf]


## <a name="how-to-prevent-false-activation"></a>Comment empêcher une fausse activation

Si vous utilisez simplement Palm-up comme événement pour déclencher le menu de la main, il peut s’afficher accidentellement quand vous n’en avez pas besoin (faux positif), car les gens déplacent leurs mains intentionnellement (pour la communication et la manipulation d’objets) et involontairement. Pour réduire les fausses activations, ajoutez une étape supplémentaire en plus de l’événement Palm-up pour appeler le menu de la main (par exemple, des doigts entièrement ouverts ou l’utilisateur intentionnellement Gazing à la main).

**Exiger un Palm plat**

En exigeant une main ouverte, vous pouvez empêcher une fausse activation qui peut se produire lorsque l’utilisateur manipule des objets ou des gestes tout en communiquant au sein d’un environnement. 

**Exiger le point de regard**

En demandant à l’utilisateur de pointer à sa main (avec un regard ou un point de présence oculaire), il empêche les fausses activations, car l’utilisateur doit intentionnellement attirer son attention sur la main en tant qu’étape d’activation secondaire (avec un seuil de distance réglable utilisé pour permettre le confort de l’utilisateur).  

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4Asn4]

---

## <a name="hand-menu-placement-best-practices"></a>Meilleures pratiques relatives à l’emplacement des menus manuels

Dans l’anatomie humaine, le nerf ulnar est un nerf qui s’exécute près du segment ulna. Le ulna est un long segment trouvé dans le bras qui s’étend du coud au doigt le plus petit.

Vous trouverez ci-dessous deux placements recommandés en fonction de nos explorations :


:::row:::
    :::column:::
        ![Emplacement de la main ulnar](images/UlnarSideHandMenu.gif)<br>
        **A. ulnar dans Palm**<br>
        Cette position est fiable, car les mains ne se chevauchent pas mutuellement. Cela est essentiel pour une détection et un suivi précis des mains.
    :::column-end:::
    :::column:::
        ![Emplacement de la main ulnar](images/UlnarAboveHandMenu.gif)<br>
        **B. ulnar au-dessus de la main**<br>
        Cet emplacement est à l’aise pour les utilisateurs, car ils n’ont pas besoin d’augmenter trop le bras pour interagir avec le menu de la main. Nous vous recommandons de placer les menus **13cm** au-dessus de la paume et d’aligner les boutons à l’intérieur de la paume ulnar. [En savoir plus sur la taille optimale du bouton](interactable-object.md)<br>
        <br>
        Pour des raisons techniques, nous recommandons cet emplacement avec une mise en œuvre obligatoire : le développeur doit geler le menu une fois que la main opposée de l’utilisateur est proche de son interaction. Cela évite à jitteriness de se chevaucher les mains et permet également de cibler plus rapidement les boutons.<br>
        <br>
        Les caméras HoloLens 2 identifient les mains avec précision lorsqu’elles sont séparées les unes des autres. Les mains qui se chevauchent peuvent entraîner un déplacement des menus manuels hors de l’emplacement d’ancrage.<br>
    :::column-end:::
:::row-end:::



<br>

---

## <a name="menu-positions-that-are-not-recommended"></a>Positions de menu non recommandées
Nous avons fait des recherches utilisateur avec différents emplacements et dispositions de menus, les emplacements de menu suivants ne sont **pas recommandés**, recherchez les inconvénients de chaque étude ci-dessous :


:::row:::
    :::column:::
        ![Au-dessus du bras](images/AboveArm.gif)<br>
        **Au-dessus du bras**<br>
        1-difficulté à entretenir un bon suivi des mains<br>
        2-provoque la fatigue de l’utilisateur en raison d’une position non naturelle
    :::column-end:::
    :::column:::
        ![Les doigts ci-dessus](images/AboveFingers.gif)<br>
        **Les doigts ci-dessus**<br>
        fatigue à 1 main en raison de la main pendant une longue période<br>
        2 problèmes de suivi sur l’index et les doigts centraux
    :::column-end:::
:::row-end:::

<br>

:::row:::
    :::column:::
        ![Au-dessus de Center Palm](images/handCenter.gif)<br>
        **Au-dessus-Centre Palm**<br>
        problèmes de suivi de 1 main en raison du chevauchement des mains<br>
        fatigue à deux mains, en raison de la maintenance de longue durée pour interagir avec les menus
    :::column-end:::
    :::column:::
        ![Le haut ](images/TopFingerTip.gif) de **la main**<br>
        1-problèmes de suivi de la main<br>
        2-la fatigue de la main au-dessus de la position normale<br>
        3-problèmes de pression sur les boutons avec d’autres doigts par accident en raison d’un espace limité entre les doigts
    :::column-end:::
:::row-end:::

<br>

:::row:::
    :::column:::
        ![Arrière du bras](images/BackOfTheArm.gif)<br>
        **Arrière du bras**<br>
        1-peut déclencher le bouton d’origine par accident<br>
        2-n’est pas une position naturelle ou confortable
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

<br>

---

## <a name="hand-menu-in-mrtk-mixed-reality-toolkit-for-unity"></a>Menu de la main dans MRTK (ensemble d’outils de réalité mixte) pour Unity
**[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)** fournit des scripts et des exemples de scènes pour le menu de la main. Le script du solveur HandConstraintPalmUp vous permet de joindre des objets aux mains avec différentes options configurables. Les exemples de menu manuel de MRTK incluent des options utiles, telles que le Palm plat et le point de vue du regard pour empêcher l’activation erronée.

* [Documentation des menus contextuels](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_HandMenu.html)
* [Exemple de scène de menu manuel](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Assets/MRTK/Examples/Demos/HandTracking/Scenes/HandMenuExamples.unity)

Vous pouvez essayer des exemples de menu manuel dans HoloLens 2 avec l’application MRTK d’exemples de Hub. 
* [Scène du menu manuel dans MRTK exemples Hub](https://www.microsoft.com/en-us/p/mrtk-examples-hub/9mv8c39l2sj4?activetab=pivot:overviewtab)

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
