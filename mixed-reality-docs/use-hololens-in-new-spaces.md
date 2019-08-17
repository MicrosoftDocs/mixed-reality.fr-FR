---
title: Utiliser HoloLens dans de nouveaux espaces
description: HoloLens apprend à quoi ressemble un espace dans le temps. Les utilisateurs peuvent faciliter ce processus en déplaçant le HoloLens de certaines façons à travers l’espace.
author: dorreneb
ms.author: dobrown
ms.date: 08/16/2019
ms.topic: article
keywords: Windows Mixed Reality, conception, mappage spatial, HoloLens, reconstruction des surfaces, maillage, suivi des têtes, mappage
ms.openlocfilehash: a6a83dfc2c883723e4cd79c0dc46a9cd78f1f604
ms.sourcegitcommit: 60f73ca23023c17c1da833c83d2a02f4dcc4d17b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2019
ms.locfileid: "69566018"
---
# <a name="use-hololens-in-new-spaces"></a><span data-ttu-id="d86e3-105">Utiliser HoloLens dans de nouveaux espaces</span><span class="sxs-lookup"><span data-stu-id="d86e3-105">Use HoloLens in New Spaces</span></span>

<span data-ttu-id="d86e3-106">HoloLens *mappe*, ou apprend sur, son environnement lorsque l’utilisateur se déplace autour d’un espace.</span><span class="sxs-lookup"><span data-stu-id="d86e3-106">HoloLens *maps*, or learns information about, its environment as the user moves around a space.</span></span> <span data-ttu-id="d86e3-107">Au fil du temps, le HoloLens crée une *carte spatiale* de toutes les parties de l’environnement qui ont été observées.</span><span class="sxs-lookup"><span data-stu-id="d86e3-107">Over time, the HoloLens builds up a *spatial map* of all parts of the environment that have been observed.</span></span> <span data-ttu-id="d86e3-108">HoloLens met à jour la carte au fur et à mesure que des modifications sont observées dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="d86e3-108">HoloLens updates the map as changes in the environment are observed.</span></span> <span data-ttu-id="d86e3-109">Cette analyse est automatiquement conservée entre les lancements de l’application.</span><span class="sxs-lookup"><span data-stu-id="d86e3-109">This scan will automatically persist between app launches.</span></span>

<span data-ttu-id="d86e3-110">HoloLens crée et met à jour les mappages tant que l’appareil est sous tension et qu’un utilisateur est connecté.</span><span class="sxs-lookup"><span data-stu-id="d86e3-110">HoloLens will create and update maps as long as the device is on and a user is logged in.</span></span> <span data-ttu-id="d86e3-111">Si vous tenez l’appareil avec les caméras pointant sur un espace, celui-ci essaie de mapper la zone.</span><span class="sxs-lookup"><span data-stu-id="d86e3-111">If you hold or wear the device with the cameras pointed at a space, the device will try to map the area.</span></span> <span data-ttu-id="d86e3-112">Alors que le HoloLens apprend un espace naturellement dans le temps, il existe des conseils et des astuces pour mettre l’espace plus rapidement et plus efficacement.</span><span class="sxs-lookup"><span data-stu-id="d86e3-112">While the HoloLens will learn a space naturally over time, there are tips and tricks available to map the space faster and more efficiently.</span></span> 

<span data-ttu-id="d86e3-113">Si votre HoloLens ne peut pas mapper votre espace ou n’est pas à l’étalonnage, vous pouvez entrer en mode limité.</span><span class="sxs-lookup"><span data-stu-id="d86e3-113">If your HoloLens can’t map your space or is out of calibration, you may enter Limited mode.</span></span> <span data-ttu-id="d86e3-114">En mode limité, vous ne pourrez pas placer des hologrammes dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="d86e3-114">In Limited mode, you won’t be able to place holograms in your surroundings.</span></span>

## <a name="tips-and-tricks-for-mapping-spaces"></a><span data-ttu-id="d86e3-115">Trucs et astuces pour le mappage des espaces</span><span class="sxs-lookup"><span data-stu-id="d86e3-115">Tips and tricks for mapping spaces</span></span>

### <a name="make-sure-the-space-is-set-up-for-mixed-reality"></a><span data-ttu-id="d86e3-116">Assurez-vous que l’espace est configuré pour la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="d86e3-116">Make sure the space is set up for mixed reality</span></span>

<span data-ttu-id="d86e3-117">Dans un environnement, les fonctionnalités peuvent compliquer l’interprétation d’un espace par le HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d86e3-117">Features in an environment can make it difficult for the HoloLens to interpret a space.</span></span> <span data-ttu-id="d86e3-118">Les niveaux d’éclairage, les matériaux dans l’espace, la disposition des objets et plus peuvent tous affecter la manière dont HoloLens mappe une zone.</span><span class="sxs-lookup"><span data-stu-id="d86e3-118">Light levels, materials in the space, the layout of objects, and more can all affect how HoloLens maps an area.</span></span>

<span data-ttu-id="d86e3-119">Vous trouverez des conseils sur la configuration de votre espace pour HoloLens et d’autres appareils de réalité mixte dans [considérations environnementales pour hololens](environment-considerations-for-hololens.md).</span><span class="sxs-lookup"><span data-stu-id="d86e3-119">Tips for setting up your space for HoloLens and other mixed reality devices can be found in [Environment considerations for HoloLens](environment-considerations-for-hololens.md).</span></span>

### <a name="understand-the-scenarios-for-the-area"></a><span data-ttu-id="d86e3-120">Comprendre les scénarios de la zone</span><span class="sxs-lookup"><span data-stu-id="d86e3-120">Understand the scenarios for the area</span></span>

<span data-ttu-id="d86e3-121">Il est important de consacrer le plus de temps à l’utilisation du HoloLens afin que la carte soit pertinente et complète.</span><span class="sxs-lookup"><span data-stu-id="d86e3-121">It is important to spend the most time where you will be using the HoloLens so that the map is relevant and complete.</span></span> 

<span data-ttu-id="d86e3-122">Par exemple, si un scénario utilisateur pour HoloLens implique de passer du point A au point B, parcourez ce chemin deux à trois fois, en regardant toutes les directions à mesure que vous déplacez.</span><span class="sxs-lookup"><span data-stu-id="d86e3-122">For example, if a user scenario for HoloLens involves moving from Point A to Point B, walk that path two to three times, looking in all directions as you move.</span></span> 

### <a name="walk-slowly-around-the-space"></a><span data-ttu-id="d86e3-123">Parcourez lentement l’espace</span><span class="sxs-lookup"><span data-stu-id="d86e3-123">Walk slowly around the space</span></span>

<span data-ttu-id="d86e3-124">Si vous parcourez trop rapidement dans la zone, il est probable que le HoloLens ne manquera pas de zones de mappage.</span><span class="sxs-lookup"><span data-stu-id="d86e3-124">If you walk too quickly around the area, it's likely that the HoloLens will miss mapping areas.</span></span> <span data-ttu-id="d86e3-125">Parcourez lentement l’espace, en arrêtant tous les 9 à 5-8 de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="d86e3-125">Walk slowly around the space, stopping every 5-8 feet to look around at your surroundings.</span></span>

<span data-ttu-id="d86e3-126">Les mouvements lisses aident également la carte HoloLens plus efficacement.</span><span class="sxs-lookup"><span data-stu-id="d86e3-126">Smooth movements also help the HoloLens map more effeciently.</span></span>

### <a name="look-in-all-directions"></a><span data-ttu-id="d86e3-127">Rechercher dans toutes les directions</span><span class="sxs-lookup"><span data-stu-id="d86e3-127">Look in all directions</span></span>

<span data-ttu-id="d86e3-128">Si vous recherchez à mesure que vous mappez l’espace, vous obtenez des données supplémentaires sur les emplacements où les points sont relatifs les uns par rapport aux autres.</span><span class="sxs-lookup"><span data-stu-id="d86e3-128">Looking around as you map the space gives the HoloLens more data on where points are relative to each other.</span></span> 

<span data-ttu-id="d86e3-129">Si vous ne parvenez pas à rechercher, par exemple, le HoloLens peut ne pas savoir où se trouve le plafond dans une pièce.</span><span class="sxs-lookup"><span data-stu-id="d86e3-129">If you don't look up, for example, the HoloLens may not know where the ceiling in a room is.</span></span> 

<span data-ttu-id="d86e3-130">N’oubliez pas de regarder au sol au fur et à mesure que vous mappez l’espace.</span><span class="sxs-lookup"><span data-stu-id="d86e3-130">Don't forget to look down at the floor as you map the space.</span></span>

### <a name="cover-key-areas-multiple-times"></a><span data-ttu-id="d86e3-131">Couvrir plusieurs fois les domaines clés</span><span class="sxs-lookup"><span data-stu-id="d86e3-131">Cover key areas multiple times</span></span>

<span data-ttu-id="d86e3-132">Le déplacement de plusieurs fois dans une zone vous aidera à sélectionner les fonctionnalités que vous n’avez peut-être pas manquées lors de la première procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="d86e3-132">Moving through an area multiple times will help pick up features you may have missed on the first walkthrough.</span></span> <span data-ttu-id="d86e3-133">Essayez de parcourir une zone deux à trois fois pour créer une carte idéale.</span><span class="sxs-lookup"><span data-stu-id="d86e3-133">Try traversing an area two to three times to build an ideal map.</span></span>

<span data-ttu-id="d86e3-134">Si possible, lors de la répétition de ces mouvements, consacrez du temps à parcourir une zone dans un sens, puis à vous déplacer et à revenir en arrière.</span><span class="sxs-lookup"><span data-stu-id="d86e3-134">If possible, while repeating these movements, spend time walking through an area in one direction, then turn around and walk back the way you came.</span></span>

### <a name="take-your-time-mapping-the-area"></a><span data-ttu-id="d86e3-135">Prendre votre temps à mapper la zone</span><span class="sxs-lookup"><span data-stu-id="d86e3-135">Take your time mapping the area</span></span>

<span data-ttu-id="d86e3-136">Le schéma HoloLens peut prendre de 15 à 20 minutes pour être entièrement mappé et ajusté à son environnement.</span><span class="sxs-lookup"><span data-stu-id="d86e3-136">It can take between 15 and 20 minutes for the HoloLens to fully map and adjust itself to its surroundings.</span></span> <span data-ttu-id="d86e3-137">Si vous avez un espace dans lequel vous envisagez d’utiliser un HoloLens fréquemment, prendre ce temps en amont pour mapper l’espace peut empêcher des problèmes plus tard.</span><span class="sxs-lookup"><span data-stu-id="d86e3-137">If you have a space in which you plan to use a HoloLens frequently, taking that time up front to map the space can prevent issues later on.</span></span> 

## <a name="possible-errors-in-the-spatial-map"></a><span data-ttu-id="d86e3-138">Erreurs possibles dans la carte spatiale</span><span class="sxs-lookup"><span data-stu-id="d86e3-138">Possible errors in the spatial map</span></span>

<span data-ttu-id="d86e3-139">Les erreurs dans les données de mappage spatiale sont classées dans l’une des trois catégories suivantes:</span><span class="sxs-lookup"><span data-stu-id="d86e3-139">Errors in spatial mapping data fall into one of three categories:</span></span>

* <span data-ttu-id="d86e3-140">*Trous*: Les surfaces réelles sont absentes des données de mappage spatiale.</span><span class="sxs-lookup"><span data-stu-id="d86e3-140">*Holes*: Real-world surfaces are missing from the spatial mapping data.</span></span>
* <span data-ttu-id="d86e3-141">*Hallucinations*: Des surfaces existent dans les données de mappage spatiale qui n’existent pas dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="d86e3-141">*Hallucinations*: Surfaces exist in the spatial mapping data that do not exist in the real world.</span></span>
* <span data-ttu-id="d86e3-142">Repères: L’élément HoloLens «perd» la partie de la carte spatiale en pensant qu’il se trouve dans une autre partie de la carte qu’il ne l’est réellement.</span><span class="sxs-lookup"><span data-stu-id="d86e3-142">*Wormholes*: HoloLens 'loses' part of the spatial map by thinking it is in a different part of the map than it actually is.</span></span>
* <span data-ttu-id="d86e3-143">*Biais*: Les surfaces dans les données de mappage spatiale sont alignées de façon imparfaite avec les surfaces réelles, push dans ou extraites.</span><span class="sxs-lookup"><span data-stu-id="d86e3-143">*Bias*: Surfaces in the spatial mapping data are imperfectly aligned with real-world surfaces, either pushed in or pulled out.</span></span>

<span data-ttu-id="d86e3-144">La plupart de ces erreurs peuvent être atténuées en [supprimant vos hologrammes](environment-considerations-for-hololens.md) et en remappant l’espace.</span><span class="sxs-lookup"><span data-stu-id="d86e3-144">Many of these errors can be mitigated by [deleting your holograms](environment-considerations-for-hololens.md) and re-mapping the space.</span></span>