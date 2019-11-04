---
title: Point de regard
description: Présentation générale du modèle d’entrée (œil/tête) du regard et du point d’entrée
author: sostel
ms.author: sostel
ms.date: 10/31/2019
ms.topic: article
keywords: La réalité mixte, le regard, le point de présence, l’interaction, la conception, le suivi des yeux, le suivi des têtes
ms.openlocfilehash: d87406d0b2695cd86c40f27cb132af54ed525b25
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73435355"
---
# <a name="gaze-and-dwell"></a><span data-ttu-id="383c2-104">Point de regard</span><span class="sxs-lookup"><span data-stu-id="383c2-104">Gaze and dwell</span></span>

<span data-ttu-id="383c2-105">Quand les mains sont occupées avec des outils et des pièces, les mouvements peuvent être fastidieux, voire impossibles.</span><span class="sxs-lookup"><span data-stu-id="383c2-105">When hands are occupied with tools and parts, gestures can be tedious or impossible.</span></span> <span data-ttu-id="383c2-106">Les commandes vocales peuvent également être peu fiables dans certains contextes, par exemple dans des conditions excessivement intenses.</span><span class="sxs-lookup"><span data-stu-id="383c2-106">Voice commands may also be unreliable in certain contexts, for example under excessively loud conditions.</span></span> <span data-ttu-id="383c2-107">Le point de regard et le point de vue offre un mécanisme familier et facile à maîtriser pour le fonctionnement des têtes et des mains libres sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="383c2-107">Gaze and dwell offers a familiar and easy-to-master mechanism for working heads-up and hands-free on HoloLens.</span></span> <span data-ttu-id="383c2-108">En outre, le point de regard et le bruit est un excellent secours, qui est indépendant des contraintes de bruit ou de silence dans l’environnement d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="383c2-108">Additionally, gaze and dwell is a great fallback which is independent of noise interference or silence constraints in the operating environment.</span></span>
<span data-ttu-id="383c2-109">Nous distingueons deux variantes de point de _regard_et de [tête : le point](gaze-and-dwell-head.md) de regard et le point d’appui [.](gaze-and-dwell-eyes.md)</span><span class="sxs-lookup"><span data-stu-id="383c2-109">We distinguish two variants of _gaze and dwell_: [Head-gaze and dwell](gaze-and-dwell-head.md) and [Eye-gaze and dwell](gaze-and-dwell-eyes.md).</span></span>

## <a name="scenarios"></a><span data-ttu-id="383c2-110">Scénarios</span><span class="sxs-lookup"><span data-stu-id="383c2-110">Scenarios</span></span>

<span data-ttu-id="383c2-111">Le point de vue et le point de vue dans les scénarios où les mains d’une personne sont occupés avec d’autres tâches, et la voix n’est pas 100% fiable ou disponible en raison de contraintes environnementales ou sociales.</span><span class="sxs-lookup"><span data-stu-id="383c2-111">Gaze and dwell excels in scenarios where a person's hands are busy with other tasks, and voice isn't 100% reliable or available due to environmental or social constraints.</span></span> <span data-ttu-id="383c2-112">Un bon exemple est une personne portant un appareil HoloLens pour superposer des informations de référence tout en réparant un moteur de voiture.</span><span class="sxs-lookup"><span data-stu-id="383c2-112">A good example is a person wearing a HoloLens to overlay reference information while repairing a car engine.</span></span> <span data-ttu-id="383c2-113">Ses mains sont occupées par des outils ou supportent son corps quand elle se penche dans le compartiment du moteur.</span><span class="sxs-lookup"><span data-stu-id="383c2-113">Their hands are busy with tools or supporting their body as they lean into the engine compartment.</span></span> <span data-ttu-id="383c2-114">L’espace du garage est bruyant, les coups et bourdonnement constants des outils rendant difficile l’utilisation de commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="383c2-114">The garage space is loud, with the constant banging and buzzing of tools, making voice commands difficult.</span></span> <span data-ttu-id="383c2-115">Le point de regard permet à la personne utilisant HoloLens de parcourir en toute confiance son document de référence sans interrompre son flux de travail.</span><span class="sxs-lookup"><span data-stu-id="383c2-115">Gaze and dwell allows the person using the HoloLens to confidently navigate their reference material without interrupting their workflow.</span></span> 

## <a name="device-support"></a><span data-ttu-id="383c2-116">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="383c2-116">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="383c2-117"><strong>Modèle d’entrée</strong></span><span class="sxs-lookup"><span data-stu-id="383c2-117"><strong>Input model</strong></span></span></td>
        <td><span data-ttu-id="383c2-118"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="383c2-118"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="383c2-119"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="383c2-119"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="383c2-120"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="383c2-120"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="383c2-121">Suivre de la tête et stabiliser</span><span class="sxs-lookup"><span data-stu-id="383c2-121">Head-gaze and dwell</span></span></td>
        <td><span data-ttu-id="383c2-122">✔️ Recommandé</span><span class="sxs-lookup"><span data-stu-id="383c2-122">✔️ Recommended</span></span></td>
        <td><span data-ttu-id="383c2-123">✔️ Recommandé</span><span class="sxs-lookup"><span data-stu-id="383c2-123">✔️ Recommended</span></span></td>
        <td><span data-ttu-id="383c2-124">✔️ Recommandé</span><span class="sxs-lookup"><span data-stu-id="383c2-124">✔️ Recommended</span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="383c2-125">Œil-point de regard</span><span class="sxs-lookup"><span data-stu-id="383c2-125">Eye-gaze and dwell</span></span></td>
        <td><span data-ttu-id="383c2-126">❌ non disponible</span><span class="sxs-lookup"><span data-stu-id="383c2-126">❌ Not available</span></span></td>
        <td><span data-ttu-id="383c2-127">✔️ Recommandé</span><span class="sxs-lookup"><span data-stu-id="383c2-127">✔️ Recommended</span></span></td>
        <td><span data-ttu-id="383c2-128">❌ non disponible</span><span class="sxs-lookup"><span data-stu-id="383c2-128">❌ Not available</span></span></td>
    </tr>
</table>


<br>

---
 
 ## <a name="see-also"></a><span data-ttu-id="383c2-129">Articles associés</span><span class="sxs-lookup"><span data-stu-id="383c2-129">See also</span></span>
* [<span data-ttu-id="383c2-130">Interaction basée sur les yeux</span><span class="sxs-lookup"><span data-stu-id="383c2-130">Eye-based interaction</span></span>](eye-gaze-interaction.md)
* [<span data-ttu-id="383c2-131">Suivi des yeux sur HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="383c2-131">Eye tracking on HoloLens 2</span></span>](eye-tracking.md)
* [<span data-ttu-id="383c2-132">Point de regard et validation</span><span class="sxs-lookup"><span data-stu-id="383c2-132">Gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="383c2-133">Manipulation directe</span><span class="sxs-lookup"><span data-stu-id="383c2-133">Hands - Direct manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="383c2-134">Mouvements pratiques</span><span class="sxs-lookup"><span data-stu-id="383c2-134">Hands - Gestures</span></span>](gaze-and-commit.md#composite-gestures)
* [<span data-ttu-id="383c2-135">Mains et validation</span><span class="sxs-lookup"><span data-stu-id="383c2-135">Hands - Point and commit</span></span>](point-and-commit.md)
* [<span data-ttu-id="383c2-136">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="383c2-136">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="383c2-137">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="383c2-137">Voice input</span></span>](voice-input.md)
