---
title: Démarrer le mouvement
description: Démarrer le mouvement pour appeler le menu Démarrer.
author: shengkait
ms.author: cmeekhof
ms.date: 10/22/2019
ms.topic: article
keywords: Réalité mixte, gestes, interaction, conception
ms.openlocfilehash: 84088156d0c9cdacc421985b922d5e9370f6a87e
ms.sourcegitcommit: fd606e87e3c4785d3ca2a26632be3bb580e39afb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/28/2020
ms.locfileid: "84152514"
---
# <a name="start-gesture"></a>Démarrer le mouvement

Le mouvement de début est un mouvement manuel utilisé pour appeler le menu Démarrer. Cela revient à appuyer sur la touche Windows du clavier, le bouton Xbox sur un contrôleur Xbox ou le bouton Windows sur le contrôleur de mouvement du casque immersif. Il est important de comprendre quels mouvements sont réservés pour le système sur chaque appareil de réalité mixte afin d’éviter les conflits lors de la conception de vos interactions.

## <a name="device-support"></a>Prise en charge des appareils

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
        <td>Bourgeon</td>
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

## <a name="bloom"></a>Bourgeon
Pour afficher le menu Démarrer dans HoloLens (1ère génération), nous avons conçu « fleuri », qui est un geste symbolique imitant la fleur florale. Il est propre à l’interaction surefooted, facile à effectuer et rapide à rappeler. Pour effectuer le mouvement de floraison sur HoloLens (1ère génération), tenez votre main avec votre paume, puis ouvrez votre main en répartissant vos doigts.

:::row:::
    :::column:::
        ![Fermeture de la fleur](images/bloom-close.png)<br>
        **Étape 1 : palmier avec les doigts**<br>
    :::column-end:::
    :::column:::
        ![Ouverture de fleurs](images/bloom-open.png)<br>
        **Étape 2 : créer une planche à portée de main**<br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="start-gesture"></a>Démarrer le mouvement
Dans HoloLens 2, nous avons remplacé le geste fleuri par un bouton de poignet virtuel qui permet d’autres interactions instinctual qui ne nécessitent pas d’apprentissage supplémentaire. En présentant les utilisateurs du bouton sur le poignet, ils peuvent accéder de manière intuitive et appuyer dessus.

:::row:::
    :::column:::
        ![Bouton de poignet prêt](images/wrist-button-ready.png)<br>
        **Étape 1 : palmier pour montrer le bouton de poignet**<br>
    :::column-end:::
    :::column:::
        ![Appui sur le bouton du poignet](images/wrist-button-press.png)<br>
        **Étape 2 : Appuyez sur le bouton du poignet**<br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="one-handed-start-gesture"></a>Mouvement de démarrage à une main

> [!IMPORTANT]
> Pour que le mouvement de démarrage à la main fonctionne :
>
> 1. Vous devez effectuer la mise à jour vers la mise à jour de novembre 2019 (Build 18363,1039) ou version ultérieure.
> 1. Vos yeux doivent être étalonnés sur l’appareil afin que le suivi visuel fonctionne correctement. Si vous ne voyez pas les points d’orbite autour de l’icône de démarrage lorsque vous l’examinez, vos yeux ne sont pas étalonnés sur l’appareil.

Vous pouvez également effectuer le mouvement de démarrage avec une seule main. Pour ce faire, tenez votre main avec votre paume et regardez l' **icône de démarrage** sur votre poignet interne. **Tout en gardant un œil sur l’icône**, pincez votre doigt et votre index ensemble.<br>
:::row:::
    :::column:::
        ![Bouton de poignet prêt](images/wrist-button-ready.png)<br>
        **Étape 1 : palmier pour montrer le bouton de poignet**<br>
    :::column-end:::
    :::column:::
        ![Pince à bouton de poignet](images/wrist-button-pinch.png)<br>
        **Étape 2 : attirez le regard sur le bouton, puis pincez**<br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="see-also"></a>Voir aussi

* [Interactions instinctuelles](interaction-fundamentals.md)
* [Œil-point de regard](eye-tracking.md)
* [Entrée vocale](voice-input.md)
