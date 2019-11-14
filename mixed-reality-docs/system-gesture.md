---
title: Mouvement système
description: Mouvement système pour appeler le menu Démarrer.
author: shengkait
ms.author: cmeekhof
ms.date: 10/22/2019
ms.topic: article
keywords: Réalité mixte, gestes, interaction, conception
ms.openlocfilehash: 417811fff9d98e459dc0047d46ea065acfced4ef
ms.sourcegitcommit: f2b7c6381006fab6d0472fcaa680ff7fb79954d6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74064239"
---
# <a name="system-gesture"></a><span data-ttu-id="7bef7-104">Mouvement système</span><span class="sxs-lookup"><span data-stu-id="7bef7-104">System gesture</span></span>

<span data-ttu-id="7bef7-105">Le mouvement système est un mouvement manuel utilisé pour appeler le menu Démarrer.</span><span class="sxs-lookup"><span data-stu-id="7bef7-105">The system gesture is a hand gesture used to invoke the Start Menu.</span></span> <span data-ttu-id="7bef7-106">Cela revient à appuyer sur la touche Windows du clavier, le bouton Xbox sur un contrôleur Xbox ou le bouton Windows sur le contrôleur de mouvement du casque immersif.</span><span class="sxs-lookup"><span data-stu-id="7bef7-106">It is the equivalent of pressing the Windows key on the keyboard, the Xbox button on an Xbox controller, or the Windows button on the immersive headset motion controller.</span></span> <span data-ttu-id="7bef7-107">Il est important de comprendre quels mouvements sont réservés pour le système sur chaque appareil de réalité mixte afin d’éviter les conflits lors de la conception de vos interactions.</span><span class="sxs-lookup"><span data-stu-id="7bef7-107">It's important to understand which gestures are reserved for the system on each Mixed Reality device to prevent conflicts when designing your interactions.</span></span>

## <a name="device-support"></a><span data-ttu-id="7bef7-108">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="7bef7-108">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="7bef7-109"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="7bef7-109"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="7bef7-110"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="7bef7-110"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="7bef7-111"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="7bef7-111"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="7bef7-112"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="7bef7-112"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="7bef7-113">Fleuri</span><span class="sxs-lookup"><span data-stu-id="7bef7-113">Bloom</span></span></td>
        <td><span data-ttu-id="7bef7-114">✔️</span><span class="sxs-lookup"><span data-stu-id="7bef7-114">✔️</span></span></td>
        <td>❌</td>
        <td>❌</td>
    </tr>
     <tr>
        <td><span data-ttu-id="7bef7-115">Bouton de poignet</span><span class="sxs-lookup"><span data-stu-id="7bef7-115">Wrist button</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="7bef7-116">✔️</span><span class="sxs-lookup"><span data-stu-id="7bef7-116">✔️</span></span></td>
        <td>❌</td>
    </tr>
    <tr>
        <td><span data-ttu-id="7bef7-117">Pince œil et poignet</span><span class="sxs-lookup"><span data-stu-id="7bef7-117">Eye gaze and palm up pinch</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="7bef7-118">✔️</span><span class="sxs-lookup"><span data-stu-id="7bef7-118">✔️</span></span></td>
        <td>❌</td>
    </tr>
</table>

## <a name="bloom"></a><span data-ttu-id="7bef7-119">Fleuri</span><span class="sxs-lookup"><span data-stu-id="7bef7-119">Bloom</span></span>
<span data-ttu-id="7bef7-120">Pour afficher le menu Démarrer dans HoloLens (1ère génération), nous avons conçu « fleuri », qui est un geste symbolique imitant la fleur florale.</span><span class="sxs-lookup"><span data-stu-id="7bef7-120">To bring up the start menu in HoloLens (1st gen), we designed “Bloom”, which is a symbolic gesture mimicking the flower blossom.</span></span> <span data-ttu-id="7bef7-121">Il est propre à l’interaction surefooted, facile à effectuer et rapide à rappeler.</span><span class="sxs-lookup"><span data-stu-id="7bef7-121">It's distinctive for surefooted interaction, easy to perform, and quick to recall.</span></span> <span data-ttu-id="7bef7-122">Pour effectuer le mouvement de floraison sur HoloLens (1ère génération), tenez votre main avec votre paume, puis ouvrez votre main en répartissant vos doigts.</span><span class="sxs-lookup"><span data-stu-id="7bef7-122">To do the bloom gesture on HoloLens (1st gen), hold out your hand with your palm up and fingertips together, then open your hand by spreading your fingers.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="7bef7-123">![](images/bloom-close.png) de fermeture</span><span class="sxs-lookup"><span data-stu-id="7bef7-123">![Bloom close](images/bloom-close.png)</span></span><br>
        <span data-ttu-id="7bef7-124">**Étape 1 : palmier avec les doigts**</span><span class="sxs-lookup"><span data-stu-id="7bef7-124">**Step 1: Palm up with fingertips together**</span></span><br>
    :::column-end:::
    :::column:::
        <span data-ttu-id="7bef7-125">![de fleurs ouvertes](images/bloom-open.png)</span><span class="sxs-lookup"><span data-stu-id="7bef7-125">![Bloom open](images/bloom-open.png)</span></span><br>
        <span data-ttu-id="7bef7-126">**Étape 2 : créer une planche à portée de main**</span><span class="sxs-lookup"><span data-stu-id="7bef7-126">**Step 2: Palm up with fingertips spread**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="wrist-button"></a><span data-ttu-id="7bef7-127">Bouton de poignet</span><span class="sxs-lookup"><span data-stu-id="7bef7-127">Wrist button</span></span>
<span data-ttu-id="7bef7-128">Dans HoloLens 2, nous avons remplacé le geste fleuri par un bouton de poignet virtuel qui permet d’autres interactions instinctual qui ne nécessitent pas d’apprentissage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="7bef7-128">In HoloLens 2, we replaced the Bloom gesture with a virtual wrist button that allows for more instinctual interactions that require no additional teaching.</span></span> <span data-ttu-id="7bef7-129">En présentant les utilisateurs du bouton sur le poignet, ils peuvent accéder de manière intuitive et appuyer dessus.</span><span class="sxs-lookup"><span data-stu-id="7bef7-129">By showing users the button on the wrist, they can intuitively reach out and press it with their other hand.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="7bef7-130">bouton de poignet ![](images/wrist-button-ready.png)</span><span class="sxs-lookup"><span data-stu-id="7bef7-130">![Wrist button ready](images/wrist-button-ready.png)</span></span><br>
        <span data-ttu-id="7bef7-131">**Étape 1 : palmier pour montrer le bouton de poignet**</span><span class="sxs-lookup"><span data-stu-id="7bef7-131">**Step 1: Palm up to show the wrist button**</span></span><br>
    :::column-end:::
    :::column:::
        <span data-ttu-id="7bef7-132">![bouton de poignet](images/wrist-button-press.png)</span><span class="sxs-lookup"><span data-stu-id="7bef7-132">![Wrist button press](images/wrist-button-press.png)</span></span><br>
        <span data-ttu-id="7bef7-133">**Étape 2 : Appuyez sur le bouton du poignet**</span><span class="sxs-lookup"><span data-stu-id="7bef7-133">**Step 2: Press the wrist button**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="eye-gaze-and-palm-up-pinch"></a><span data-ttu-id="7bef7-134">Pincez-vous pour les yeux et les paumes</span><span class="sxs-lookup"><span data-stu-id="7bef7-134">Eye-gaze and palm up pinch</span></span>
<span data-ttu-id="7bef7-135">Nous avons également conçu une solution unique pour faciliter l’accès à HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="7bef7-135">We have also designed a one-handed solution for ease of access in HoloLens 2.</span></span> <span data-ttu-id="7bef7-136">Ce geste oblige les utilisateurs à examiner le bouton de poignet, puis à utiliser la même main pour effectuer un pincement de palmier à l’aide de leur doigt et de leur doigt d’index.</span><span class="sxs-lookup"><span data-stu-id="7bef7-136">This gesture requires users to eye gaze at the wrist button, then use the same hand to perform a palm up pinch using their thumb and index finger.</span></span><br>
:::row:::
    :::column:::
        <span data-ttu-id="7bef7-137">bouton de poignet ![](images/wrist-button-ready.png)</span><span class="sxs-lookup"><span data-stu-id="7bef7-137">![Wrist button ready](images/wrist-button-ready.png)</span></span><br>
        <span data-ttu-id="7bef7-138">**Étape 1 : palmier pour montrer le bouton de poignet**</span><span class="sxs-lookup"><span data-stu-id="7bef7-138">**Step 1: Palm up to show the wrist button**</span></span><br>
    :::column-end:::
    :::column:::
        <span data-ttu-id="7bef7-139">![pincement du bouton de poignet](images/wrist-button-pinch.png)</span><span class="sxs-lookup"><span data-stu-id="7bef7-139">![Wrist button pinch](images/wrist-button-pinch.png)</span></span><br>
        <span data-ttu-id="7bef7-140">**Étape 2 : attirez le regard sur le bouton, puis pincez**</span><span class="sxs-lookup"><span data-stu-id="7bef7-140">**Step 2: Eye gaze at the button then pinch**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="see-also"></a><span data-ttu-id="7bef7-141">Articles associés</span><span class="sxs-lookup"><span data-stu-id="7bef7-141">See also</span></span>

* [<span data-ttu-id="7bef7-142">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="7bef7-142">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="7bef7-143">Suivre du regard</span><span class="sxs-lookup"><span data-stu-id="7bef7-143">Eye-gaze</span></span>](eye-tracking.md)
* [<span data-ttu-id="7bef7-144">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="7bef7-144">Voice input</span></span>](voice-input.md)
