---
title: Menu de la main
description: Les menus manuels permettent aux utilisateurs d’afficher rapidement une interface utilisateur attachée à la main pour les fonctions fréquemment utilisées. Voici nos meilleures pratiques et recommandations pour les menus manuels.
author: nbarragan23
ms.author: nobarr
ms.date: 08/27/2019
ms.topic: article
keywords: main, menu, bouton, accès rapide, disposition
ms.openlocfilehash: ee958806ac462535b33164bb4faa4bf1aa29e709
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73439250"
---
# <a name="hand-menu"></a>Menu de la main

![Emplacement de la main ulnar](images/MRTK_UX_HandMenu.png)

Les menus manuels permettent aux utilisateurs d’afficher rapidement une interface utilisateur attachée à la main pour les fonctions fréquemment utilisées. 

Voici les meilleures pratiques que nous avons trouvées pour les menus manuels. Vous trouverez également un exemple de scène illustrant le menu manuel dans [MRTK](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_Solver.md#hand-menu-with-handconstraint-and-handconstraintpalmup).

<br>

---

## <a name="behavior-best-practices"></a>Meilleures pratiques relatives au comportement
**A. conserver le nombre de boutons petit :** en raison de la distance étroite entre un menu verrouillé et les yeux, ainsi que la tendance de l’utilisateur à se concentrer sur une zone visuelle relativement petite à tout moment (le cône de vision est à peu près 10 degrés), nous vous recommandons en réduisant le nombre de boutons. En fonction de notre exploration, une colonne avec trois boutons fonctionne bien en conservant tout le contenu dans le champ de vision (l’angle de vue) même lorsque les utilisateurs passent leur mains au centre de l’aide. 

**B. utilisation du menu pour une action rapide :** l’élévation d’un bras et la maintenance de la position peuvent facilement entraîner une fatigue du bras. Utilisez une méthode verrouillée à la main pour le menu nécessitant une faible interaction. Si votre menu est complexe et nécessite des temps d’interaction étendus, envisagez d’utiliser à la place un verrou universel ou verrouillé. 

**C. angle du bouton/du panneau :** les menus doivent s’afficher à l’épaule opposé et au milieu de la tête : cela permet à une main naturelle d’interagir avec le menu avec la main opposée et d’éviter les positions difficiles ou inconfortables lors de la touche. boutons. 

**D. envisagez de prendre en charge une opération unidirectionnelle ou mains libres :** ne partez pas du principe que les deux mains de l’utilisateur sont toujours disponibles. Considérez un large éventail de contextes quand l’un ou l’autre des mains n’est pas disponible, et assurez-vous que votre conception compte pour ces situations. Pour prendre en charge un menu contextuel à un seul mains, vous pouvez essayer de passer le positionnement du menu de façon à ce qu’il passe à l’état verrouillé à l’extérieur lorsque la main est tournée (s’affiche à l’écran). Pour les scénarios mains libres, envisagez d’utiliser une commande vocale pour appeler les boutons de menu de la main.

**E. appel en deux étapes :** si vous utilisez simplement Palm-up comme événement pour déclencher le menu de la main, il peut s’afficher accidentellement quand vous n’en avez pas besoin (faux positif), car les gens déplacent leurs mains de manière intentionnelle (pour la communication et la manipulation d’objets) et involontairement. Si vous rencontrez des faux positifs dans votre application, envisagez d’ajouter une étape supplémentaire en plus de l’événement Palm-up pour appeler le menu de la main, par exemple les doigts entièrement ouverts.

**F. Évitez d’ajouter des boutons à proximité du poignet (bouton de démarrage du système) :** si les boutons de menu de la main sont placés trop près du bouton d’origine, ils peuvent être déclenchés par inadvertance lors de l’interaction avec le menu de la main.

**G. test, test, test :** les personnes ont des corps différents, avec des seuils différents pour le confort et la gêne, etc. Veillez à tester votre conception et à obtenir des commentaires d’un grand nombre de personnes.

<br>

---

## <a name="hand-menu-placement-best-practices"></a>Meilleures pratiques relatives à l’emplacement des menus manuels

Dans l’anatomie humaine, le nerf ulnar est un nerf qui s’exécute près du segment ulna. Le ulna est un long segment trouvé dans le bras qui s’étend du coud au doigt le plus petit.

Vous trouverez ci-dessous deux placements recommandés en fonction de nos explorations :


:::row:::
    :::column:::
        ![emplacement ulnar](images/UlnarSideHandMenu.gif)<br>
        **A. ulnar dans Palm**<br>
        Cette position est fiable, car les mains ne se chevauchent pas mutuellement. Cela est essentiel pour une détection et un suivi précis des mains.
    :::column-end:::
    :::column:::
        ![emplacement ulnar](images/UlnarAboveHandMenu.gif)<br>
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
        ![](images/AboveArm.gif) ARM<br>
        **Au-dessus du bras**<br>
        1-difficulté à entretenir un bon suivi des mains<br>
        2-provoque la fatigue de l’utilisateur en raison d’une position non naturelle
    :::column-end:::
    :::column:::
        ![les doigts ci-dessus](images/AboveFingers.gif)<br>
        **Les doigts ci-dessus**<br>
        fatigue de la main en raison de la main à long terme<br>
        2 problèmes de suivi sur l’index et le doigt central
    :::column-end:::
:::row-end:::

<br>

:::row:::
    :::column:::
        ![au-dessus de la](images/handCenter.gif) Center Palm<br>
        **Au-dessus-Centre Palm**<br>
        problèmes de suivi de 1 main en raison du chevauchement des mains<br>
        fatigue à deux mains, en raison de la maintenance de longue durée pour interagir avec les menus
    :::column-end:::
    :::column:::
        ![**le haut de la main](images/TopFingerTip.gif)**<br>
        1-problèmes de suivi de la main<br>
        fatigue à deux mains, en tenant au-dessus de la position normale<br>
        3-problèmes de pression sur les boutons avec d’autres doigts par accident en raison d’un espace limité entre les doigts
    :::column-end:::
:::row-end:::

<br>

:::row:::
    :::column:::
        ![arrière du](images/BackOfTheArm.gif) ARM<br>
        **Arrière du bras**<br>
        1-peut déclencher le bouton d’origine par accident<br>
        2-pas de position naturelle ou confortable pour les utilisateurs
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

<br>

---


## <a name="see-also"></a>Articles associés

* [Objet avec interaction possible](interactable-object.md)
* [Manipulation directe avec les mains](direct-manipulation.md)
* [Mains et contrôleurs de mouvement](hands-and-tools.md)