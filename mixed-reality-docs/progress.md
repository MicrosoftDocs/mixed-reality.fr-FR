---
title: Affichage de la progression
description: Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, design, Controls, UI, UX
ms.openlocfilehash: d028b8717dae0e04a9a1104a8a4b7803023334ef
ms.sourcegitcommit: 6844930427b658ae31f642c395cd8a3b3cdbf857
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75723208"
---
# <a name="progress-indicator"></a>Indicateur de progression

<br>

<img src="images/UX/MRTK_ProgressIndicator.gif" alt="Progress ring example in HoloLens" width="940px">

Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours. Cela peut signifier que l’utilisateur ne peut pas interagir avec l’application lorsque l’indicateur de progression est visible et peut également indiquer le temps d’attente en fonction de l’indicateur utilisé.

<br>

---

## <a name="types-of-progress"></a>Types de progression

Il est important de fournir les informations de l’utilisateur sur ce qui se passe. Dans la réalité mixte, les utilisateurs peuvent être facilement gênés par un environnement ou des objets physiques si votre application ne donne pas de bons commentaires visuels. Pour les situations qui prennent quelques secondes, telles que le chargement des données ou la mise à jour d’une scène, il est judicieux d’afficher un indicateur visuel. Il existe deux options pour montrer à l’utilisateur qu’une opération est en cours d’exécution : une **barre de progression** ou un **anneau de progression**.

:::row:::
    :::column:::
        ### <a name="progress-barbr"></a>Barre de progression<br>
        Une barre de progression indique le pourcentage d’achèvement d’une tâche. Elle doit être utilisée pendant une opération dont la durée est connue (arrêt), mais la progression ne doit pas bloquer l’interaction de l’utilisateur avec l’application.<br>
        <br>
        *Image : exemple de barre de progression dans HoloLens*
    :::column-end:::
        :::column:::
        ![space](images/spacer-20x582.png)<br>
       exemple de barre de progression ![dans HoloLens](images/640px-progressbar.jpg)<br>
    :::column-end:::
:::row-end:::

<br>

---

:::row:::
    :::column:::
        ### <a name="progress-ringbr"></a>Anneau de progression<br>
        Un anneau de progression n’a qu’un état indéterminé et doit être utilisé quand une interaction utilisateur supplémentaire est bloquée jusqu’à ce que l’opération soit terminée.<br>
        <br>
        *Image : exemple de sonnerie de progression dans HoloLens*
    :::column-end:::
        :::column:::
        ![space](images/spacer-20x582.png)<br>
       ![exemple de sonnerie de progression dans HoloLens](images/640px-progressring.jpg)<br>
    :::column-end:::
:::row-end:::

<br>

---

:::row:::
    :::column:::
        ### <a name="progress-with-a-custom-objectbr"></a>Progression avec un objet personnalisé<br>
        Vous pouvez ajouter à la personnalité et à l’identité de votre application en personnalisant le contrôle de progression avec vos propres objets 2D/3D personnalisés.<br>
        <br>
        *Image : progression avec un exemple de maillage personnalisé dans HoloLens*
    :::column-end:::
        :::column:::
        ![space](images/spacer-20x582.png)<br>
       ![la progression avec l’exemple de maille personnalisé dans HoloLens](images/640px-progresscustom.jpg)<br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="best-practices"></a>Bonnes pratiques
* Couplez étroitement le [billboarding ou la balise](billboarding-and-tag-along.md) à l’affichage de la progression puisque l’utilisateur peut facilement déplacer son tête dans un espace vide et perdre le contexte. Votre application peut sembler se bloquer si l’utilisateur ne parvient pas à voir quoi que ce soit. Le billboarding et la balise sont intégrés au Prefab Progress.
* Il est toujours judicieux de fournir des informations d’État sur ce qui se passe à l’utilisateur. Le Prefab de progression fournit différents styles visuels, y compris la progression de type Ring Windows standard pour la fourniture de l’État. Vous pouvez également utiliser une maille personnalisée avec une animation si vous souhaitez que le style de la progression s’aligne sur la personnalisation de votre application.

<br>

---

## <a name="progress-indicator-in-mrtk-mixed-reality-toolkit-for-unity"></a>Indicateur de progression dans MRTK (ensemble d’outils de réalité mixte) pour Unity

* [MRTK-indicateur de progression prefabs](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.SDK/Features/UX/Prefabs/ProgressIndicators)
* [MRTK-service de transition de scène](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Extensions/SceneTransitionService/SceneTransitionServiceOverview.html)


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
