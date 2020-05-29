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
# <a name="start-gesture"></a><span data-ttu-id="4a13d-104">Démarrer le mouvement</span><span class="sxs-lookup"><span data-stu-id="4a13d-104">Start gesture</span></span>

<span data-ttu-id="4a13d-105">Le mouvement de début est un mouvement manuel utilisé pour appeler le menu Démarrer.</span><span class="sxs-lookup"><span data-stu-id="4a13d-105">The Start gesture is a hand gesture used to invoke the Start Menu.</span></span> <span data-ttu-id="4a13d-106">Cela revient à appuyer sur la touche Windows du clavier, le bouton Xbox sur un contrôleur Xbox ou le bouton Windows sur le contrôleur de mouvement du casque immersif.</span><span class="sxs-lookup"><span data-stu-id="4a13d-106">It is the equivalent of pressing the Windows key on the keyboard, the Xbox button on an Xbox controller, or the Windows button on the immersive headset motion controller.</span></span> <span data-ttu-id="4a13d-107">Il est important de comprendre quels mouvements sont réservés pour le système sur chaque appareil de réalité mixte afin d’éviter les conflits lors de la conception de vos interactions.</span><span class="sxs-lookup"><span data-stu-id="4a13d-107">It's important to understand which gestures are reserved for the system on each Mixed Reality device to prevent conflicts when designing your interactions.</span></span>

## <a name="device-support"></a><span data-ttu-id="4a13d-108">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="4a13d-108">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="4a13d-109"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="4a13d-109"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="4a13d-110"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="4a13d-110"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="4a13d-111"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="4a13d-111"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="4a13d-112"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="4a13d-112"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="4a13d-113">Bourgeon</span><span class="sxs-lookup"><span data-stu-id="4a13d-113">Bloom</span></span></td>
        <td><span data-ttu-id="4a13d-114">✔️</span><span class="sxs-lookup"><span data-stu-id="4a13d-114">✔️</span></span></td>
        <td>❌</td>
        <td>❌</td>
    </tr>
     <tr>
        <td><span data-ttu-id="4a13d-115">Bouton de poignet</span><span class="sxs-lookup"><span data-stu-id="4a13d-115">Wrist button</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="4a13d-116">✔️</span><span class="sxs-lookup"><span data-stu-id="4a13d-116">✔️</span></span></td>
        <td>❌</td>
    </tr>
    <tr>
        <td><span data-ttu-id="4a13d-117">Pince œil et poignet</span><span class="sxs-lookup"><span data-stu-id="4a13d-117">Eye gaze and palm up pinch</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="4a13d-118">✔️</span><span class="sxs-lookup"><span data-stu-id="4a13d-118">✔️</span></span></td>
        <td>❌</td>
    </tr>
</table>

## <a name="bloom"></a><span data-ttu-id="4a13d-119">Bourgeon</span><span class="sxs-lookup"><span data-stu-id="4a13d-119">Bloom</span></span>
<span data-ttu-id="4a13d-120">Pour afficher le menu Démarrer dans HoloLens (1ère génération), nous avons conçu « fleuri », qui est un geste symbolique imitant la fleur florale.</span><span class="sxs-lookup"><span data-stu-id="4a13d-120">To bring up the start menu in HoloLens (1st gen), we designed “Bloom”, which is a symbolic gesture mimicking the flower blossom.</span></span> <span data-ttu-id="4a13d-121">Il est propre à l’interaction surefooted, facile à effectuer et rapide à rappeler.</span><span class="sxs-lookup"><span data-stu-id="4a13d-121">It's distinctive for surefooted interaction, easy to perform, and quick to recall.</span></span> <span data-ttu-id="4a13d-122">Pour effectuer le mouvement de floraison sur HoloLens (1ère génération), tenez votre main avec votre paume, puis ouvrez votre main en répartissant vos doigts.</span><span class="sxs-lookup"><span data-stu-id="4a13d-122">To do the bloom gesture on HoloLens (1st gen), hold out your hand with your palm up and fingertips together, then open your hand by spreading your fingers.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="4a13d-123">![Fermeture de la fleur](images/bloom-close.png)</span><span class="sxs-lookup"><span data-stu-id="4a13d-123">![Bloom close](images/bloom-close.png)</span></span><br>
        <span data-ttu-id="4a13d-124">**Étape 1 : palmier avec les doigts**</span><span class="sxs-lookup"><span data-stu-id="4a13d-124">**Step 1: Palm up with fingertips together**</span></span><br>
    :::column-end:::
    :::column:::
        <span data-ttu-id="4a13d-125">![Ouverture de fleurs](images/bloom-open.png)</span><span class="sxs-lookup"><span data-stu-id="4a13d-125">![Bloom open](images/bloom-open.png)</span></span><br>
        <span data-ttu-id="4a13d-126">**Étape 2 : créer une planche à portée de main**</span><span class="sxs-lookup"><span data-stu-id="4a13d-126">**Step 2: Palm up with fingertips spread**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="start-gesture"></a><span data-ttu-id="4a13d-127">Démarrer le mouvement</span><span class="sxs-lookup"><span data-stu-id="4a13d-127">Start gesture</span></span>
<span data-ttu-id="4a13d-128">Dans HoloLens 2, nous avons remplacé le geste fleuri par un bouton de poignet virtuel qui permet d’autres interactions instinctual qui ne nécessitent pas d’apprentissage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="4a13d-128">In HoloLens 2, we replaced the Bloom gesture with a virtual wrist button that allows for more instinctual interactions that require no additional teaching.</span></span> <span data-ttu-id="4a13d-129">En présentant les utilisateurs du bouton sur le poignet, ils peuvent accéder de manière intuitive et appuyer dessus.</span><span class="sxs-lookup"><span data-stu-id="4a13d-129">By showing users the button on the wrist, they can intuitively reach out and press it with their other hand.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="4a13d-130">![Bouton de poignet prêt](images/wrist-button-ready.png)</span><span class="sxs-lookup"><span data-stu-id="4a13d-130">![Wrist button ready](images/wrist-button-ready.png)</span></span><br>
        <span data-ttu-id="4a13d-131">**Étape 1 : palmier pour montrer le bouton de poignet**</span><span class="sxs-lookup"><span data-stu-id="4a13d-131">**Step 1: Palm up to show the wrist button**</span></span><br>
    :::column-end:::
    :::column:::
        <span data-ttu-id="4a13d-132">![Appui sur le bouton du poignet](images/wrist-button-press.png)</span><span class="sxs-lookup"><span data-stu-id="4a13d-132">![Wrist button press](images/wrist-button-press.png)</span></span><br>
        <span data-ttu-id="4a13d-133">**Étape 2 : Appuyez sur le bouton du poignet**</span><span class="sxs-lookup"><span data-stu-id="4a13d-133">**Step 2: Press the wrist button**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="one-handed-start-gesture"></a><span data-ttu-id="4a13d-134">Mouvement de démarrage à une main</span><span class="sxs-lookup"><span data-stu-id="4a13d-134">One-handed Start gesture</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a13d-135">Pour que le mouvement de démarrage à la main fonctionne :</span><span class="sxs-lookup"><span data-stu-id="4a13d-135">For the one-handed Start gesture to work:</span></span>
>
> 1. <span data-ttu-id="4a13d-136">Vous devez effectuer la mise à jour vers la mise à jour de novembre 2019 (Build 18363,1039) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4a13d-136">You must update to the November 2019 update (build 18363.1039) or later.</span></span>
> 1. <span data-ttu-id="4a13d-137">Vos yeux doivent être étalonnés sur l’appareil afin que le suivi visuel fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="4a13d-137">Your eyes must be calibrated on the device so that eye tracking functions correctly.</span></span> <span data-ttu-id="4a13d-138">Si vous ne voyez pas les points d’orbite autour de l’icône de démarrage lorsque vous l’examinez, vos yeux ne sont pas étalonnés sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4a13d-138">If you do not see orbiting dots around the Start icon when you look at it, your eyes are not calibrated on the device.</span></span>

<span data-ttu-id="4a13d-139">Vous pouvez également effectuer le mouvement de démarrage avec une seule main.</span><span class="sxs-lookup"><span data-stu-id="4a13d-139">You can also perform the Start gesture with only one hand.</span></span> <span data-ttu-id="4a13d-140">Pour ce faire, tenez votre main avec votre paume et regardez l' **icône de démarrage** sur votre poignet interne.</span><span class="sxs-lookup"><span data-stu-id="4a13d-140">To do this, hold out your hand with your palm facing you and look at the **Start icon** on your inner wrist.</span></span> <span data-ttu-id="4a13d-141">**Tout en gardant un œil sur l’icône**, pincez votre doigt et votre index ensemble.</span><span class="sxs-lookup"><span data-stu-id="4a13d-141">**While keeping your eye on the icon**, pinch your thumb and index finger together.</span></span><br>
:::row:::
    :::column:::
        <span data-ttu-id="4a13d-142">![Bouton de poignet prêt](images/wrist-button-ready.png)</span><span class="sxs-lookup"><span data-stu-id="4a13d-142">![Wrist button ready](images/wrist-button-ready.png)</span></span><br>
        <span data-ttu-id="4a13d-143">**Étape 1 : palmier pour montrer le bouton de poignet**</span><span class="sxs-lookup"><span data-stu-id="4a13d-143">**Step 1: Palm up to show the wrist button**</span></span><br>
    :::column-end:::
    :::column:::
        <span data-ttu-id="4a13d-144">![Pince à bouton de poignet](images/wrist-button-pinch.png)</span><span class="sxs-lookup"><span data-stu-id="4a13d-144">![Wrist button pinch](images/wrist-button-pinch.png)</span></span><br>
        <span data-ttu-id="4a13d-145">**Étape 2 : attirez le regard sur le bouton, puis pincez**</span><span class="sxs-lookup"><span data-stu-id="4a13d-145">**Step 2: Eye gaze at the button then pinch**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="see-also"></a><span data-ttu-id="4a13d-146">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4a13d-146">See also</span></span>

* [<span data-ttu-id="4a13d-147">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="4a13d-147">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="4a13d-148">Œil-point de regard</span><span class="sxs-lookup"><span data-stu-id="4a13d-148">Eye-gaze</span></span>](eye-tracking.md)
* [<span data-ttu-id="4a13d-149">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="4a13d-149">Voice input</span></span>](voice-input.md)
