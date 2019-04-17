---
title: Visualisation d’analyse de salle
description: Les applications qui requièrent des données de mappage spatial s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions en tant que l’utilisateur explore leur environnement avec l’appareil actif.
author: mattzmsft
ms.author: alexpf
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, modèles d’application, la conception, HoloLens, analyse de la salle, spatiale de mappage, surface reconstruction, de maillage
ms.openlocfilehash: 8ffde9d476e25016f986321377dce8125ee3a596
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596944"
---
# <a name="room-scan-visualization"></a><span data-ttu-id="727cc-104">Visualisation d’analyse de salle</span><span class="sxs-lookup"><span data-stu-id="727cc-104">Room scan visualization</span></span>

<span data-ttu-id="727cc-105">Les applications qui requièrent des données de mappage spatial s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions en tant que l’utilisateur explore leur environnement avec l’appareil actif.</span><span class="sxs-lookup"><span data-stu-id="727cc-105">Applications that require spatial mapping data rely on the device to automatically collect this data over time and across sessions as the user explores their environment with the device active.</span></span> <span data-ttu-id="727cc-106">Le souci d’exhaustivité et la qualité de ces données dépend de plusieurs facteurs, notamment la quantité d’exploration de l’utilisateur a effectué, combien de temps écoulé depuis l’exploration et indique si les objets tels que des portes et meubles ont déplacés depuis le périphérique analyse la zone.</span><span class="sxs-lookup"><span data-stu-id="727cc-106">The completeness and quality of this data depends on a number of factors including the amount of exploration the user has done, how much time has passed since the exploration and whether objects such as furniture and doors have moved since the device scanned the area.</span></span>

<span data-ttu-id="727cc-107">Pour garantir des données de mappage spatial utiles, les développeurs d’applications ont plusieurs options :</span><span class="sxs-lookup"><span data-stu-id="727cc-107">To ensure useful spatial mapping data, applications developers have several options:</span></span>
* <span data-ttu-id="727cc-108">S’appuient sur ce qui peut avoir déjà été collecté.</span><span class="sxs-lookup"><span data-stu-id="727cc-108">Rely on what may have already been collected.</span></span> <span data-ttu-id="727cc-109">Ces données peuvent être incomplètes initialement.</span><span class="sxs-lookup"><span data-stu-id="727cc-109">This data may be incomplete initially.</span></span>
* <span data-ttu-id="727cc-110">Demandez à l’utilisateur à utiliser le mouvement de bloom pour accéder à la réalité mixte Windows domestique et ensuite Explorer la zone qu’ils souhaitent utiliser pour une expérience.</span><span class="sxs-lookup"><span data-stu-id="727cc-110">Ask the user to use the bloom gesture to get to the Windows Mixed Reality home and then explore the area they wish to use for the experience.</span></span> <span data-ttu-id="727cc-111">Ils peuvent utiliser appui en l’air pour confirmer que la zone nécessaire est connue à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="727cc-111">They can use air-tap to confirm that all the necessary area is known to the device.</span></span>
* <span data-ttu-id="727cc-112">Créer une expérience d’exploration personnalisés dans leur propre application.</span><span class="sxs-lookup"><span data-stu-id="727cc-112">Build a custom exploration experience in their own application.</span></span>

<span data-ttu-id="727cc-113">Notez que dans tous ces cas, les données réelles collectées au cours de l’exploration sont stockées par le système et l’application n’a pas besoin pour ce faire.</span><span class="sxs-lookup"><span data-stu-id="727cc-113">Note that in all these cases the actual data gathered during the exploration is stored by the system and the application does not need to do this.</span></span>

## <a name="device-support"></a><span data-ttu-id="727cc-114">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="727cc-114">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="727cc-115">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="727cc-115">Feature</span></span></th><th style="width:150px"> <span data-ttu-id="727cc-116"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="727cc-116"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="727cc-117"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="727cc-117"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="727cc-118">Visualisation d’analyse de salle</span><span class="sxs-lookup"><span data-stu-id="727cc-118">Room scan visualization</span></span></td><td style="text-align: center;"> <span data-ttu-id="727cc-119">✔️</span><span class="sxs-lookup"><span data-stu-id="727cc-119">✔️</span></span></td><td style="text-align: center;"></td>
</tr>
</table>



## <a name="building-a-custom-scanning-experience"></a><span data-ttu-id="727cc-120">Création d’une expérience d’analyse personnalisée</span><span class="sxs-lookup"><span data-stu-id="727cc-120">Building a custom scanning experience</span></span>

<span data-ttu-id="727cc-121">Les applications peuvent décider d’analyser les données de mappage spatial au début de l’expérience pour déterminer s’ils veulent que l’utilisateur d’effectuer des étapes supplémentaires pour améliorer son exhaustivité et la qualité.</span><span class="sxs-lookup"><span data-stu-id="727cc-121">Applications may decide to analyze the spatial mapping data at the start of the experience to judge whether they want the user to perform additional steps to improve its completeness and quality.</span></span> <span data-ttu-id="727cc-122">Si l’analyse indique la qualité doit être améliorée, les développeurs doivent fournir une visualisation à superposer sur le monde entier pour indiquer :</span><span class="sxs-lookup"><span data-stu-id="727cc-122">If analysis indicates quality should be improved, developers should provide a visualization to overlay on the world to indicate:</span></span>
* <span data-ttu-id="727cc-123">La quantité du volume total à proximité des utilisateurs doit faire partie de l’expérience</span><span class="sxs-lookup"><span data-stu-id="727cc-123">How much of the total volume in the users vicinity needs to be part of the experience</span></span>
* <span data-ttu-id="727cc-124">Où l’utilisateur doit accéder pour améliorer les données</span><span class="sxs-lookup"><span data-stu-id="727cc-124">Where the user should go to improve data</span></span>

<span data-ttu-id="727cc-125">Les utilisateurs ne savent pas ce qui rend une analyse « bonne ».</span><span class="sxs-lookup"><span data-stu-id="727cc-125">Users do not know what makes a "good" scan.</span></span> <span data-ttu-id="727cc-126">Ils doivent être affichés ou dit que ce que vous recherchez s’il leur sont demandés pour évaluer une analyse – apparence à deux dimensions, la distance entre les murs réels, etc. Le développeur doit implémenter une boucle de rétroaction qui inclut l’actualisation des données de mappage spatial pendant la phase d’analyse ou l’exploration.</span><span class="sxs-lookup"><span data-stu-id="727cc-126">They need to be shown or told what to look for if they’re asked to evaluate a scan – flatness, distance from actual walls, etc. The developer should implement a feedback loop that includes refreshing the spatial mapping data during the scanning or exploration phase.</span></span>

<span data-ttu-id="727cc-127">Dans de nombreux cas, il peut être préférable d’indiquer à l’utilisateur de ce qu’ils doivent (par exemple, examinez le plafond, recherchez derrière meubles), afin d’obtenir la qualité d’analyse nécessaires.</span><span class="sxs-lookup"><span data-stu-id="727cc-127">In many cases, it may be best to tell the user what they need to do (e.g. look at the ceiling, look behind furniture), in order to get the necessary scan quality.</span></span>

## <a name="cached-versus-continuous-spatial-mapping"></a><span data-ttu-id="727cc-128">Mise en cache et continue mappage spatial</span><span class="sxs-lookup"><span data-stu-id="727cc-128">Cached versus continuous spatial mapping</span></span>

<span data-ttu-id="727cc-129">Les données de mappage spatial sont le poids de la plus importante des applications de source de données peuvent consommer.</span><span class="sxs-lookup"><span data-stu-id="727cc-129">The spatial mapping data is the most heavy weight data source applications can consume.</span></span> <span data-ttu-id="727cc-130">Pour éviter les problèmes de performances telles que suppression d’images ou interruption du son, la consommation de ces données doit être mûrement.</span><span class="sxs-lookup"><span data-stu-id="727cc-130">To avoid performance issues such as dropped frames or stuttering, consumption of this data should be done carefully.</span></span>

<span data-ttu-id="727cc-131">Analyse active durant une expérience peut être bénéfiques ou nuisibles et le développeur doit décider quelle méthode à utiliser en fonction de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="727cc-131">Active scanning during an experience can be both beneficial or detrimental and the developer will need to decide which method to use based on the experience.</span></span>

### <a name="cached-spatial-mapping"></a><span data-ttu-id="727cc-132">Mise en cache de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="727cc-132">Cached spatial mapping</span></span>

<span data-ttu-id="727cc-133">Dans le cas de mappage spatial mis en cache, l’application est généralement prend un instantané des données de mappage spatial et utilise cette capture instantanée pendant la durée de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="727cc-133">In the case of cached spatial mapping, the application typically takes a snapshot of the spatial mapping data and uses this snapshot for the duration of the experience.</span></span>

<span data-ttu-id="727cc-134">**Avantages**</span><span class="sxs-lookup"><span data-stu-id="727cc-134">**Benefits**</span></span>
* <span data-ttu-id="727cc-135">Réduction des coûts sur le système pendant que l’expérience est en cours d’exécution pointe à une puissance importante, thermique et gains de performance de processeur.</span><span class="sxs-lookup"><span data-stu-id="727cc-135">Reduced overhead on the system while the experience is running leading to dramatic power, thermal and cpu performance gains.</span></span>
* <span data-ttu-id="727cc-136">Une implémentation plus simple de l’expérience principale dans la mesure où il n’est pas interrompu par des modifications dans les données spatiales.</span><span class="sxs-lookup"><span data-stu-id="727cc-136">A simpler implementation of the main experience since it is not interrupted by changes in the spatial data.</span></span>
* <span data-ttu-id="727cc-137">Une seule une fois tout post-traitement des données spatiales pour les graphismes, graphiques et autres à des fins de coûts.</span><span class="sxs-lookup"><span data-stu-id="727cc-137">A single one time cost on any post processing of the spatial data for physics, graphics and other purposes.</span></span>

<span data-ttu-id="727cc-138">**Drawbacks**</span><span class="sxs-lookup"><span data-stu-id="727cc-138">**Drawbacks**</span></span>
* <span data-ttu-id="727cc-139">Le déplacement des objets du monde réel ou des personnes n’est pas reflété par les données en cache.</span><span class="sxs-lookup"><span data-stu-id="727cc-139">The movement of real world objects or people is not reflected by the cached data.</span></span> <span data-ttu-id="727cc-140">Exemple</span><span class="sxs-lookup"><span data-stu-id="727cc-140">E.g.</span></span> <span data-ttu-id="727cc-141">l’application peut prendre en compte une porte ouverte lorsqu’il est fermé en fait maintenant.</span><span class="sxs-lookup"><span data-stu-id="727cc-141">the application might consider a door open when it is actually closed now.</span></span>
* <span data-ttu-id="727cc-142">Mémoire potentiellement plus de l’application à mettre à jour la version mise en cache des données.</span><span class="sxs-lookup"><span data-stu-id="727cc-142">Potentially more application memory to maintain the cached version of the data.</span></span>

<span data-ttu-id="727cc-143">Un bon cas pour cette méthode est un environnement contrôlé ou un jeu en haut de la table.</span><span class="sxs-lookup"><span data-stu-id="727cc-143">A good case for this method is a controlled environment or a table top game.</span></span>

### <a name="continuous-spatial-mapping"></a><span data-ttu-id="727cc-144">Mappage spatial continue</span><span class="sxs-lookup"><span data-stu-id="727cc-144">Continuous spatial mapping</span></span>

<span data-ttu-id="727cc-145">Certaines applications peuvent reposer sur poursuit l’analyse pour actualiser les données de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="727cc-145">Certain applications may rely on continues scanning to refresh spatial mapping data.</span></span>

<span data-ttu-id="727cc-146">**Avantages**</span><span class="sxs-lookup"><span data-stu-id="727cc-146">**Benefits**</span></span>
* <span data-ttu-id="727cc-147">Vous n’avez pas besoin de générer un distinct analyse ou l’exploration expérience dès le départ dans votre application.</span><span class="sxs-lookup"><span data-stu-id="727cc-147">You don't need to build in a separate scanning or exploration experience upfront in your application.</span></span>
* <span data-ttu-id="727cc-148">Le déplacement des objets du monde réel peut être reflété par le jeu, mais avec un délai.</span><span class="sxs-lookup"><span data-stu-id="727cc-148">The movement of real world objects can be reflected by the game, although with some delay.</span></span>

<span data-ttu-id="727cc-149">**Drawbacks**</span><span class="sxs-lookup"><span data-stu-id="727cc-149">**Drawbacks**</span></span>
* <span data-ttu-id="727cc-150">Plus haute complexité dans l’implémentation de l’expérience principale.</span><span class="sxs-lookup"><span data-stu-id="727cc-150">Higher complexity in the implementation of the main experience.</span></span>
* <span data-ttu-id="727cc-151">Risque de surcharge du traitement supplémentaire pour le graphique ou physique en tant que modifications doivent être incrémentielle ingérés par ces systèmes.</span><span class="sxs-lookup"><span data-stu-id="727cc-151">Potential overhead of the additional processing for graphic or physics as changes need to be incrementally ingested by these systems.</span></span>
* <span data-ttu-id="727cc-152">Améliorer la puissance, thermique et impact sur le processeur.</span><span class="sxs-lookup"><span data-stu-id="727cc-152">Higher power, thermal and CPU impact.</span></span>

<span data-ttu-id="727cc-153">Un bon cas pour cette méthode est un où les hologrammes sont amenés à interagir avec le déplacement d’objets, par exemple, une voiture HOLOGRAPHIQUE que lecteurs sur le sol souhaitez correctement rencontrent une porte selon qu’il est ouvert ou fermé.</span><span class="sxs-lookup"><span data-stu-id="727cc-153">A good case for this method is one where holograms are expected to interact with moving objects, e.g. a holographic car that drives on the floor may want to correctly bump into a door depending on whether it is open or closed.</span></span>

## <a name="see-also"></a><span data-ttu-id="727cc-154">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="727cc-154">See also</span></span>
* [<span data-ttu-id="727cc-155">Conception de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="727cc-155">Spatial mapping design</span></span>](spatial-mapping-design.md)
* [<span data-ttu-id="727cc-156">Systèmes de coordonnées</span><span class="sxs-lookup"><span data-stu-id="727cc-156">Coordinate systems</span></span>](coordinate-systems.md)
* [<span data-ttu-id="727cc-157">Sonorisation spatiale</span><span class="sxs-lookup"><span data-stu-id="727cc-157">Spatial sound design</span></span>](spatial-sound-design.md)
