---
title: Mouvement système
description: Mouvement système pour appeler le menu Démarrer.
author: shengkait
ms.author: cmeekhof
ms.date: 10/22/2019
ms.topic: article
keywords: Réalité mixte, gestes, interaction, conception
ms.openlocfilehash: b46f642babb18387da2e76d5bdbb7631577c85de
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73439820"
---
# <a name="system-gesture"></a>Mouvement système

Le mouvement système est un mouvement manuel utilisé pour appeler le menu Démarrer. Cela revient à appuyer sur la touche Windows du clavier, le bouton Xbox sur un contrôleur Xbox ou le bouton Windows sur le contrôleur de mouvement du casque immersif. Il est important de comprendre quels mouvements sont réservés pour le système sur chaque appareil de réalité mixte afin d’éviter les conflits lors de la conception de vos interactions.

## <a name="device-support"></a>Périphériques pris en charge

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Fleuri</td>
        <td>✔️</td>
        <td>❌</td>
        <td>❌</td>
    </tr>
     <tr>
        <td>Bouton de poignet</td>
        <td>❌</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
    <tr>
        <td>Pince œil et poignet</td>
        <td>❌</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

## <a name="bloom"></a>Fleuri
Pour afficher le menu Démarrer dans HoloLens (1ère génération), nous avons conçu « fleuri », qui est un geste symbolique imitant la fleur florale. Il est propre à l’interaction surefooted, facile à effectuer et rapide à rappeler. Pour effectuer le mouvement de floraison sur HoloLens (1ère génération), tenez votre main avec votre paume, puis ouvrez votre main en répartissant vos doigts.

:::row:::
    :::column:::
        ![](images/bloom-close.png) de fermeture<br>
        **Étape 1 : palmier avec les doigts**<br>
    :::column-end:::
    :::column:::
        ![de fleurs ouvertes](images/bloom-open.png)<br>
        **Étape 2 : paumes avec les doigts**<br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="wrist-button"></a>Bouton de poignet
Dans HoloLens 2, nous avons remplacé le geste fleuri par un bouton de poignet virtuel qui permet d’autres interactions instinctual qui ne nécessitent pas d’apprentissage supplémentaire. En présentant les utilisateurs du bouton sur le poignet, ils peuvent accéder de manière intuitive et appuyer dessus.

:::row:::
    :::column:::
        bouton de poignet ![](images/wrist-button-ready.png)<br>
        **Étape 1 : palmier pour montrer le bouton de poignet**<br>
    :::column-end:::
    :::column:::
        ![bouton de poignet](images/wrist-button-press.png)<br>
        **Étape 2 : Appuyez sur le bouton du poignet**<br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="eye-gaze-and-palm-up-pinch"></a>Pincez-vous pour les yeux et les paumes
Nous avons également conçu une solution unique pour faciliter l’accès à HoloLens 2. Ce geste oblige les utilisateurs à examiner le bouton de poignet, puis à utiliser la même main pour effectuer un pincement de palmier à l’aide de leur doigt et de leur doigt d’index.<br>
:::row:::
    :::column:::
        bouton de poignet ![](images/wrist-button-ready.png)<br>
        **Étape 1 : palmier pour montrer le bouton de poignet**<br>
    :::column-end:::
    :::column:::
        ![pincement du bouton de poignet](images/wrist-button-pinch.png)<br>
        **Étape : attirez le regard sur le bouton, puis pincez**<br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="see-also"></a>Articles associés

* [Interactions instinctuelles](interaction-fundamentals.md)
* [Suivre du regard](eye-tracking.md)
* [Entrée vocale](voice-input.md)
