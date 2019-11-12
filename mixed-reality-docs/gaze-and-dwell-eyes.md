---
title: Pointer du regard et fixer
description: Vue d’ensemble du modèle d’entrée Pointer du regard et fixer
author: sostel
ms.author: sostel
ms.date: 10/29/2019
ms.topic: article
ms.localizationpriority: high
keywords: Suivi du regard, réalité mixte, entrée, suivre du regard, suivi rétinien, suivi du mouvement des yeux, HoloLens 2, sélection basée sur le regard, fixer
ms.openlocfilehash: 5130fd3c1ecd551788f61f8abb8d02cdedeb4181
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437805"
---
# <a name="eye-gaze-and-dwell"></a><span data-ttu-id="bbc1a-104">Pointer du regard et fixer</span><span class="sxs-lookup"><span data-stu-id="bbc1a-104">Eye-gaze and dwell</span></span>

<span data-ttu-id="bbc1a-105">Le modèle d’interaction _« Pointer du regard et fixer »_ est un cas particulier du modèle d’interaction [Pointer du regard et valider](gaze-and-commit.md) :</span><span class="sxs-lookup"><span data-stu-id="bbc1a-105">The _"eye-gaze and dwell"_ interaction model is a special case of the [eye-gaze and commit](gaze-and-commit.md) interaction model:</span></span>
1. <span data-ttu-id="bbc1a-106">Regardez simplement une cible.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-106">Simply look at a target and</span></span> 
2. <span data-ttu-id="bbc1a-107">Pour confirmer votre intention de sélectionner cette cible, effectuez une entrée explicite secondaire : _Continuez simplement de regarder la cible que vous voulez sélectionner_.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-107">To confirm your intention to select the target, perform a secondary explicit input: _Simply keep looking at the target you would like to select_.</span></span>

## <a name="advantages-of-the-eye-gaze-and-dwell-interaction-model"></a><span data-ttu-id="bbc1a-108">Avantages du modèle d’interaction « Pointer du regard et fixer »</span><span class="sxs-lookup"><span data-stu-id="bbc1a-108">Advantages of the "eye-gaze and dwell" interaction model</span></span> 
<span data-ttu-id="bbc1a-109">Lorsque vos mains sont déjà occupées par une tâche ou chargées d’outils, vous ne pouvez probablement pas les utiliser pour interagir avec des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-109">When your hands are already occupied with a task or holding tools, using them for interacting with holograms may not be an option.</span></span>
<span data-ttu-id="bbc1a-110">Une alternative d’interaction sans les mains pour sélectionner des hologrammes consiste à « pointer du regard et fixer », autrement dit, à _« regarder et maintenir son regard »_ .</span><span class="sxs-lookup"><span data-stu-id="bbc1a-110">A hands-free interaction alternative for selecting holograms is "eye-gaze and dwell" or in other words: _"look and stare"_.</span></span> <span data-ttu-id="bbc1a-111">L’avantage de cette approche est que même les utilisateurs soumis à de fortes contraintes, dans l’incapacité de tourner complètement la tête ou le corps, peuvent interagir avec des hologrammes (par exemple, dans un environnement de travail très confiné).</span><span class="sxs-lookup"><span data-stu-id="bbc1a-111">The advantage of this approach is that even severly constrained users who may not be able to fully turn their heads or bodies can interact with holograms (e.g., in a highly confined work environment).</span></span>
<span data-ttu-id="bbc1a-112">L’utilisateur continue simplement de regarder la cible qu’il souhaite sélectionner et une rétroaction différente s’affiche pour indiquer le processus.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-112">The user simply keeps looking at the target they would like to select and different dwell feedback is displayed to indicate the process.</span></span>


## <a name="challenges-of-the-eye-gaze-and-dwell-interaction-model"></a><span data-ttu-id="bbc1a-113">Défis du modèle d’interaction « Pointer du regard et fixer »</span><span class="sxs-lookup"><span data-stu-id="bbc1a-113">Challenges of the "eye-gaze and dwell" interaction model</span></span>
<span data-ttu-id="bbc1a-114">En règle générale, nous vous recommandons de n’utiliser les activations par fixation du regard qu’en dernier recours si aucune entrée vocale ou manuelle n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-114">In general, we  recommend to only use dwell-based activations as a last fall-back if neither voice input nor hand input is available.</span></span> <span data-ttu-id="bbc1a-115">En effet, le choix de la durée de fixation du regard s’avère assez délicat.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-115">The reason is that the choice of dwell time can be pretty tricky.</span></span> <span data-ttu-id="bbc1a-116">Alors que les utilisateurs débutants acceptent de fixer leur regard plus longtemps, les utilisateurs experts préfèrent un parcours rapide et efficace de leurs expériences.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-116">Novice users are ok with longer dwell times, while expert users want to quickly and efficiently navigate through their experiences.</span></span> <span data-ttu-id="bbc1a-117">Cette différence rend difficile la manière d’ajuster la durée du regard selon les besoins spécifiques de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-117">This leads to the challenge of how to adjust the dwell time to the specific needs of a user.</span></span>
<span data-ttu-id="bbc1a-118">Si la durée de fixation du regard est trop courte : L’utilisateur peut finir par se sentir accablé par tous les hologrammes constamment à sa portée.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-118">If the dwell time is too short: The user may feel overwhelmed by having holograms reacht to their eye-gaze all the time.</span></span> <span data-ttu-id="bbc1a-119">Si la durée de fixation du regard est trop longue : L’expérience peut sembler trop lente et hachée, car l’utilisateur doit fixer les cibles pendant trop longtemps.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-119">If the dwell time is too long: The experience may feel too slow and interruptive as the user has to keep looking at targets for a long time.</span></span>

## <a name="design-recommendations"></a><span data-ttu-id="bbc1a-120">Recommandations de conception</span><span class="sxs-lookup"><span data-stu-id="bbc1a-120">Design recommendations</span></span>
<span data-ttu-id="bbc1a-121">Nous vous recommandons d’utiliser une approche avec deux états pour la rétroaction d’un regard fixe :</span><span class="sxs-lookup"><span data-stu-id="bbc1a-121">We recommend using a two-state approach for dwell feedback:</span></span>
1. <span data-ttu-id="bbc1a-122">*Délai initial* : Quand l’utilisateur commence à fixer une cible, rien ne doit se produire immédiatement, sans quoi l’expérience utilisateur risque de devenir désagréable et pesante.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-122">*Onset delay*: When the user starts looking at a target, nothing should immediately happen as this may result in an unpleasant and overwhelming user experience.</span></span> <span data-ttu-id="bbc1a-123">Nous préférons lancer un minuteur pour détecter si l’utilisateur fixe délibérément son regard sur la cible ou s’il ne le pose que machinalement.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-123">Instead we start a timer to detect whether the user is intentionally staring at the target or merely skimming over it.</span></span>
2. <span data-ttu-id="bbc1a-124">*Lancement de la rétroaction du regard fixe :* Après vérification que l’utilisateur regarde délibérément la cible, nous commençons à faire apparaître la rétroaction du regard fixe pour informer l’utilisateur que l’activation par fixation du regard est lancée.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-124">*Start dwell feedback:* After ensuring that the user is intentionally looking at the target, we start showing dwell feedback to inform the user that the dwell activation is being initiated.</span></span> <span data-ttu-id="bbc1a-125">Nous recommandons un délai initial compris entre 150 et 250 ms dans une proximité donnée (ce qui signifie que l’utilisateur pointe son regard et fixe précisément, plutôt qu’il ne regarde vaguement une cible plus large).</span><span class="sxs-lookup"><span data-stu-id="bbc1a-125">We recommend an onset time of 150-250 ms in a given proximity (meaning the user is fixating vs. looking around on a large target).</span></span>  
3. <span data-ttu-id="bbc1a-126">*Rétroaction en continu :* Pendant que l’utilisateur regarde toujours la cible, faites apparaître un indicateur de progression pour que l’utilisateur sache qu’il doit continuer à fixer la cible.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-126">*Continuous Feedback:* While the user keeps looking at the target, show a continous progress indicator so that the user knows that they have to keep looking at the target.</span></span> <span data-ttu-id="bbc1a-127">En particulier pour les entrées par pointage du regard, nous vous recommandons d’_attirer l’attention visuelle de l’utilisateur_ en commençant avec un cercle ou une sphère volumineuse qui rétrécit progressivement.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-127">In particular for eye-gaze input, we recommend _pulling in the user's visual attention_ by starting out with a bigger circle or sphere that contracts into a smaller version.</span></span> <span data-ttu-id="bbc1a-128">L’utilisation d’un indicateur pour l’état final (petit cercle) vous aide à communiquer à l’utilisateur à quel moment la rétroaction est terminée.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-128">Showing an indicator for the final state (small circle) helps to communicate to the user when the dwell will be finished.</span></span> <span data-ttu-id="bbc1a-129">Vous trouverez ci-dessous un exemple d’illustration.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-129">An example illustration is shown below.</span></span> 
4. <span data-ttu-id="bbc1a-130">*Fin :* Si l’utilisateur a continué de fixer la cible (pendant 650 à 850 ms supplémentaires), effectuez l’activation de la rétroaction et sélectionnez la cible fixée.</span><span class="sxs-lookup"><span data-stu-id="bbc1a-130">*Finish:* If the user kept fixating the target (for another 650-850 ms), complete the dwell activation and select the looked-at target.</span></span>

![États de rétroaction](images/eyes_dwellstate_recommendation.png)<br>

## <a name="see-also"></a><span data-ttu-id="bbc1a-132">Voir également</span><span class="sxs-lookup"><span data-stu-id="bbc1a-132">See also</span></span>
* [<span data-ttu-id="bbc1a-133">Eye-tracking</span><span class="sxs-lookup"><span data-stu-id="bbc1a-133">Eye tracking</span></span>](eye-tracking.md)
* [<span data-ttu-id="bbc1a-134">Pointer du regard et valider</span><span class="sxs-lookup"><span data-stu-id="bbc1a-134">Eye-gaze and commit</span></span>](gaze-and-commit-eyes.md)
* [<span data-ttu-id="bbc1a-135">Pointer et valider</span><span class="sxs-lookup"><span data-stu-id="bbc1a-135">Gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="bbc1a-136">Pointer du regard et fixer</span><span class="sxs-lookup"><span data-stu-id="bbc1a-136">Gaze and dwell</span></span>](gaze-and-dwell.md)
* [<span data-ttu-id="bbc1a-137">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="bbc1a-137">Voice input</span></span>](voice-design.md)