---
title: Visualisation de l’analyse de la salle
description: Les applications qui requièrent des données de mappage spatiale s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions lorsque l’utilisateur explore son environnement avec l’appareil actif.
author: mattzmsft
ms.author: alexpf
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, modèles d’application, conception, HoloLens, Scan Room, mappage spatial, maille
ms.openlocfilehash: bdb070407f27d04046bd022894c7a8a01b9658d1
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437512"
---
# <a name="room-scan-visualization"></a><span data-ttu-id="2632b-104">Visualisation de l’analyse de la salle</span><span class="sxs-lookup"><span data-stu-id="2632b-104">Room scan visualization</span></span>

<span data-ttu-id="2632b-105">Les applications qui requièrent des données de mappage spatiale s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions lorsque l’utilisateur explore son environnement avec l’appareil actif.</span><span class="sxs-lookup"><span data-stu-id="2632b-105">Applications that require spatial mapping data rely on the device to automatically collect this data over time and across sessions as the user explores their environment with the device active.</span></span> <span data-ttu-id="2632b-106">L’exhaustivité et la qualité de ces données dépendent d’un certain nombre de facteurs, notamment la quantité d’exploration effectuée par l’utilisateur, le temps écoulé depuis l’exploration et si les objets tels que les meubles et les portes ont été déplacés depuis que l’appareil a analysé la zone.</span><span class="sxs-lookup"><span data-stu-id="2632b-106">The completeness and quality of this data depends on a number of factors including the amount of exploration the user has done, how much time has passed since the exploration and whether objects such as furniture and doors have moved since the device scanned the area.</span></span>

<span data-ttu-id="2632b-107">Pour garantir l’utilité des données de mappage spatiale, les développeurs d’applications disposent de plusieurs options :</span><span class="sxs-lookup"><span data-stu-id="2632b-107">To ensure useful spatial mapping data, applications developers have several options:</span></span>
* <span data-ttu-id="2632b-108">S’appuyer sur ce qui a déjà été collecté.</span><span class="sxs-lookup"><span data-stu-id="2632b-108">Rely on what may have already been collected.</span></span> <span data-ttu-id="2632b-109">Ces données peuvent être incomplètes au départ.</span><span class="sxs-lookup"><span data-stu-id="2632b-109">This data may be incomplete initially.</span></span>
* <span data-ttu-id="2632b-110">Demandez à l’utilisateur d’utiliser le geste fleuri pour accéder à la page d’hébergement Windows Mixed Reality, puis explorez la zone qu’il souhaite utiliser pour l’expérience.</span><span class="sxs-lookup"><span data-stu-id="2632b-110">Ask the user to use the bloom gesture to get to the Windows Mixed Reality home and then explore the area they wish to use for the experience.</span></span> <span data-ttu-id="2632b-111">Ils peuvent utiliser l’utilisation de l’air pour confirmer que toutes les zones nécessaires sont connues de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="2632b-111">They can use air-tap to confirm that all the necessary area is known to the device.</span></span>
* <span data-ttu-id="2632b-112">Créez une expérience d’exploration personnalisée dans leur propre application.</span><span class="sxs-lookup"><span data-stu-id="2632b-112">Build a custom exploration experience in their own application.</span></span>

<span data-ttu-id="2632b-113">Notez que dans tous ces cas, les données réelles recueillies lors de l’exploration sont stockées par le système et que l’application n’a pas besoin de le faire.</span><span class="sxs-lookup"><span data-stu-id="2632b-113">Note that in all these cases the actual data gathered during the exploration is stored by the system and the application does not need to do this.</span></span>

## <a name="device-support"></a><span data-ttu-id="2632b-114">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="2632b-114">Device support</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="2632b-115"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="2632b-115"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="2632b-116"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="2632b-116"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="2632b-117"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="2632b-117"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="2632b-118">Visualisation de l’analyse de la salle</span><span class="sxs-lookup"><span data-stu-id="2632b-118">Room scan visualization</span></span></td>
        <td><span data-ttu-id="2632b-119">✔️</span><span class="sxs-lookup"><span data-stu-id="2632b-119">✔️</span></span></td>
        <td>❌</td>
    </tr>
</table>



## <a name="building-a-custom-scanning-experience"></a><span data-ttu-id="2632b-120">Création d’une expérience d’analyse personnalisée</span><span class="sxs-lookup"><span data-stu-id="2632b-120">Building a custom scanning experience</span></span>

<span data-ttu-id="2632b-121">Les applications peuvent décider d’analyser les données de mappage spatiale au début de l’expérience afin de juger si elles souhaitent que l’utilisateur exécute des étapes supplémentaires pour améliorer son exhaustivité et sa qualité.</span><span class="sxs-lookup"><span data-stu-id="2632b-121">Applications may decide to analyze the spatial mapping data at the start of the experience to judge whether they want the user to perform additional steps to improve its completeness and quality.</span></span> <span data-ttu-id="2632b-122">Si l’analyse indique que la qualité doit être améliorée, les développeurs doivent fournir une visualisation à superposer au monde pour indiquer :</span><span class="sxs-lookup"><span data-stu-id="2632b-122">If analysis indicates quality should be improved, developers should provide a visualization to overlay on the world to indicate:</span></span>
* <span data-ttu-id="2632b-123">La quantité totale de volume total des utilisateurs avoisinants doit faire partie de l’expérience</span><span class="sxs-lookup"><span data-stu-id="2632b-123">How much of the total volume in the users vicinity needs to be part of the experience</span></span>
* <span data-ttu-id="2632b-124">Emplacement où l’utilisateur doit accéder à l’amélioration des données</span><span class="sxs-lookup"><span data-stu-id="2632b-124">Where the user should go to improve data</span></span>

<span data-ttu-id="2632b-125">Les utilisateurs ne savent pas ce qui effectue une « bonne » analyse.</span><span class="sxs-lookup"><span data-stu-id="2632b-125">Users do not know what makes a "good" scan.</span></span> <span data-ttu-id="2632b-126">Ils doivent être affichés ou informés des éléments à rechercher s’ils sont invités à évaluer une analyse, à la distance, à la distance par rapport aux murs réels, etc. Le développeur doit implémenter une boucle de commentaires qui comprend l’actualisation des données de mappage spatiale pendant la phase d’analyse ou d’exploration.</span><span class="sxs-lookup"><span data-stu-id="2632b-126">They need to be shown or told what to look for if they’re asked to evaluate a scan – flatness, distance from actual walls, etc. The developer should implement a feedback loop that includes refreshing the spatial mapping data during the scanning or exploration phase.</span></span>

<span data-ttu-id="2632b-127">Dans de nombreux cas, il peut être préférable de dire à l’utilisateur ce qu’il doit faire (par exemple, regarder le plafond, regarder derrière le mobilier), afin d’obtenir la qualité d’analyse nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2632b-127">In many cases, it may be best to tell the user what they need to do (e.g. look at the ceiling, look behind furniture), in order to get the necessary scan quality.</span></span>

## <a name="cached-versus-continuous-spatial-mapping"></a><span data-ttu-id="2632b-128">Mise en cache et mappage spatial continu</span><span class="sxs-lookup"><span data-stu-id="2632b-128">Cached versus continuous spatial mapping</span></span>

<span data-ttu-id="2632b-129">Les données de mappage spatiale sont les applications de source de données les plus lourdes pouvant être consommées.</span><span class="sxs-lookup"><span data-stu-id="2632b-129">The spatial mapping data is the most heavy weight data source applications can consume.</span></span> <span data-ttu-id="2632b-130">Pour éviter des problèmes de performances, tels que des images ignorées ou des interruptions, la consommation de ces données doit être effectuée avec précaution.</span><span class="sxs-lookup"><span data-stu-id="2632b-130">To avoid performance issues such as dropped frames or stuttering, consumption of this data should be done carefully.</span></span>

<span data-ttu-id="2632b-131">L’analyse active au cours d’une expérience peut être à la fois bénéfique ou néfaste et le développeur doit décider de la méthode à utiliser en fonction de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="2632b-131">Active scanning during an experience can be both beneficial or detrimental and the developer will need to decide which method to use based on the experience.</span></span>

### <a name="cached-spatial-mapping"></a><span data-ttu-id="2632b-132">Mappage spatial mis en cache</span><span class="sxs-lookup"><span data-stu-id="2632b-132">Cached spatial mapping</span></span>

<span data-ttu-id="2632b-133">Dans le cas d’un mappage spatial mis en cache, l’application prend généralement un instantané des données de mappage spatiale et utilise cet instantané pour la durée de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="2632b-133">In the case of cached spatial mapping, the application typically takes a snapshot of the spatial mapping data and uses this snapshot for the duration of the experience.</span></span>

<span data-ttu-id="2632b-134">**Avantages**</span><span class="sxs-lookup"><span data-stu-id="2632b-134">**Benefits**</span></span>
* <span data-ttu-id="2632b-135">Réduction de la surcharge sur le système pendant que l’expérience est en cours d’exécution, ce qui entraîne des gains de performances considérables en matière de performances de l’UC</span><span class="sxs-lookup"><span data-stu-id="2632b-135">Reduced overhead on the system while the experience is running leading to dramatic power, thermal and cpu performance gains.</span></span>
* <span data-ttu-id="2632b-136">Une implémentation plus simple de l’expérience principale, car elle n’est pas interrompue par les modifications apportées aux données spatiales.</span><span class="sxs-lookup"><span data-stu-id="2632b-136">A simpler implementation of the main experience since it is not interrupted by changes in the spatial data.</span></span>
* <span data-ttu-id="2632b-137">Un coût unique à un moment donné sur tout traitement des données spatiales pour la physique, les graphiques et autres usages.</span><span class="sxs-lookup"><span data-stu-id="2632b-137">A single one time cost on any post processing of the spatial data for physics, graphics and other purposes.</span></span>

<span data-ttu-id="2632b-138">**Inconvénients**</span><span class="sxs-lookup"><span data-stu-id="2632b-138">**Drawbacks**</span></span>
* <span data-ttu-id="2632b-139">Le déplacement d’objets ou de personnes réels n’est pas reflété par les données mises en cache.</span><span class="sxs-lookup"><span data-stu-id="2632b-139">The movement of real world objects or people is not reflected by the cached data.</span></span> <span data-ttu-id="2632b-140">Exemple</span><span class="sxs-lookup"><span data-stu-id="2632b-140">E.g.</span></span> <span data-ttu-id="2632b-141">l’application peut considérer une porte ouverte lorsqu’elle est actuellement fermée.</span><span class="sxs-lookup"><span data-stu-id="2632b-141">the application might consider a door open when it is actually closed now.</span></span>
* <span data-ttu-id="2632b-142">Potentiellement plus de mémoire d’application pour gérer la version mise en cache des données.</span><span class="sxs-lookup"><span data-stu-id="2632b-142">Potentially more application memory to maintain the cached version of the data.</span></span>

<span data-ttu-id="2632b-143">Une bonne casse pour cette méthode est un environnement contrôlé ou un jeu en haut de la table.</span><span class="sxs-lookup"><span data-stu-id="2632b-143">A good case for this method is a controlled environment or a table top game.</span></span>

### <a name="continuous-spatial-mapping"></a><span data-ttu-id="2632b-144">Mappage spatial continu</span><span class="sxs-lookup"><span data-stu-id="2632b-144">Continuous spatial mapping</span></span>

<span data-ttu-id="2632b-145">Certaines applications peuvent reposer sur poursuivre l’analyse pour actualiser les données de mappage spatiale.</span><span class="sxs-lookup"><span data-stu-id="2632b-145">Certain applications may rely on continues scanning to refresh spatial mapping data.</span></span>

<span data-ttu-id="2632b-146">**Avantages**</span><span class="sxs-lookup"><span data-stu-id="2632b-146">**Benefits**</span></span>
* <span data-ttu-id="2632b-147">Vous n’avez pas besoin de créer une expérience d’analyse ou d’exploration distincte dans votre application.</span><span class="sxs-lookup"><span data-stu-id="2632b-147">You don't need to build in a separate scanning or exploration experience upfront in your application.</span></span>
* <span data-ttu-id="2632b-148">Le déplacement d’objets réels peut être reflété par le jeu, bien qu’avec un certain délai.</span><span class="sxs-lookup"><span data-stu-id="2632b-148">The movement of real world objects can be reflected by the game, although with some delay.</span></span>

<span data-ttu-id="2632b-149">**Inconvénients**</span><span class="sxs-lookup"><span data-stu-id="2632b-149">**Drawbacks**</span></span>
* <span data-ttu-id="2632b-150">Plus grande complexité dans l’implémentation de l’expérience principale.</span><span class="sxs-lookup"><span data-stu-id="2632b-150">Higher complexity in the implementation of the main experience.</span></span>
* <span data-ttu-id="2632b-151">La surcharge potentielle du traitement supplémentaire pour le graphique ou la physique au fur et à mesure que des modifications doivent être ingérées de manière incrémentielle par ces systèmes.</span><span class="sxs-lookup"><span data-stu-id="2632b-151">Potential overhead of the additional processing for graphic or physics as changes need to be incrementally ingested by these systems.</span></span>
* <span data-ttu-id="2632b-152">Impact plus élevé, thermique et processeur.</span><span class="sxs-lookup"><span data-stu-id="2632b-152">Higher power, thermal and CPU impact.</span></span>

<span data-ttu-id="2632b-153">Un bon cas pour cette méthode est celui où les hologrammes sont censés interagir avec les objets mobiles, par exemple, une voiture holographique dont les lecteurs sont susceptibles d’être amenés à s’intégrer correctement dans une porte, selon qu’elle est ouverte ou fermée.</span><span class="sxs-lookup"><span data-stu-id="2632b-153">A good case for this method is one where holograms are expected to interact with moving objects, e.g. a holographic car that drives on the floor may want to correctly bump into a door depending on whether it is open or closed.</span></span>

## <a name="see-also"></a><span data-ttu-id="2632b-154">Articles associés</span><span class="sxs-lookup"><span data-stu-id="2632b-154">See also</span></span>
* [<span data-ttu-id="2632b-155">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="2632b-155">Spatial mapping</span></span>](spatial-mapping.md)
* [<span data-ttu-id="2632b-156">Systèmes de coordonnées</span><span class="sxs-lookup"><span data-stu-id="2632b-156">Coordinate systems</span></span>](coordinate-systems.md)
* [<span data-ttu-id="2632b-157">Conception du son spatial</span><span class="sxs-lookup"><span data-stu-id="2632b-157">Spatial sound design</span></span>](spatial-sound-design.md)
