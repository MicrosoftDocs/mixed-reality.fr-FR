---
title: Visualisation d’analyse de salle
description: Les applications qui requièrent des données de mappage spatial s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions en tant que l’utilisateur explore leur environnement avec l’appareil actif.
author: mattzmsft
ms.author: alexpf
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, modèles d’application, la conception, HoloLens, analyse de la salle, spatiale de mappage, surface reconstruction, de maillage
ms.openlocfilehash: 09df4464ea4dac01dfad637886b07b861f468d4d
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829915"
---
# <a name="room-scan-visualization"></a><span data-ttu-id="75db2-104">Visualisation d’analyse de salle</span><span class="sxs-lookup"><span data-stu-id="75db2-104">Room scan visualization</span></span>

<span data-ttu-id="75db2-105">Les applications qui requièrent des données de mappage spatial s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions en tant que l’utilisateur explore leur environnement avec l’appareil actif.</span><span class="sxs-lookup"><span data-stu-id="75db2-105">Applications that require spatial mapping data rely on the device to automatically collect this data over time and across sessions as the user explores their environment with the device active.</span></span> <span data-ttu-id="75db2-106">Le souci d’exhaustivité et la qualité de ces données dépend de plusieurs facteurs, notamment la quantité d’exploration de l’utilisateur a effectué, combien de temps écoulé depuis l’exploration et indique si les objets tels que des portes et meubles ont déplacés depuis le périphérique analyse la zone.</span><span class="sxs-lookup"><span data-stu-id="75db2-106">The completeness and quality of this data depends on a number of factors including the amount of exploration the user has done, how much time has passed since the exploration and whether objects such as furniture and doors have moved since the device scanned the area.</span></span>

<span data-ttu-id="75db2-107">Pour garantir des données de mappage spatial utiles, les développeurs d’applications ont plusieurs options :</span><span class="sxs-lookup"><span data-stu-id="75db2-107">To ensure useful spatial mapping data, applications developers have several options:</span></span>
* <span data-ttu-id="75db2-108">S’appuient sur ce qui peut avoir déjà été collecté.</span><span class="sxs-lookup"><span data-stu-id="75db2-108">Rely on what may have already been collected.</span></span> <span data-ttu-id="75db2-109">Ces données peuvent être incomplètes initialement.</span><span class="sxs-lookup"><span data-stu-id="75db2-109">This data may be incomplete initially.</span></span>
* <span data-ttu-id="75db2-110">Demandez à l’utilisateur à utiliser le mouvement de bloom pour accéder à la réalité mixte Windows domestique et ensuite Explorer la zone qu’ils souhaitent utiliser pour une expérience.</span><span class="sxs-lookup"><span data-stu-id="75db2-110">Ask the user to use the bloom gesture to get to the Windows Mixed Reality home and then explore the area they wish to use for the experience.</span></span> <span data-ttu-id="75db2-111">Ils peuvent utiliser appui en l’air pour confirmer que la zone nécessaire est connue à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="75db2-111">They can use air-tap to confirm that all the necessary area is known to the device.</span></span>
* <span data-ttu-id="75db2-112">Créer une expérience d’exploration personnalisés dans leur propre application.</span><span class="sxs-lookup"><span data-stu-id="75db2-112">Build a custom exploration experience in their own application.</span></span>

<span data-ttu-id="75db2-113">Notez que dans tous ces cas, les données réelles collectées au cours de l’exploration sont stockées par le système et l’application n’a pas besoin pour ce faire.</span><span class="sxs-lookup"><span data-stu-id="75db2-113">Note that in all these cases the actual data gathered during the exploration is stored by the system and the application does not need to do this.</span></span>

## <a name="device-support"></a><span data-ttu-id="75db2-114">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="75db2-114">Device support</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="75db2-115"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="75db2-115"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="75db2-116"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="75db2-116"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="75db2-117"><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></span><span class="sxs-lookup"><span data-stu-id="75db2-117"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="75db2-118">Visualisation d’analyse de salle</span><span class="sxs-lookup"><span data-stu-id="75db2-118">Room scan visualization</span></span></td>
        <td><span data-ttu-id="75db2-119">✔️</span><span class="sxs-lookup"><span data-stu-id="75db2-119">✔️</span></span></td>
        <td><span data-ttu-id="75db2-120">❌</span><span class="sxs-lookup"><span data-stu-id="75db2-120">❌</span></span></td>
    </tr>
</table>



## <a name="building-a-custom-scanning-experience"></a><span data-ttu-id="75db2-121">Création d’une expérience d’analyse personnalisée</span><span class="sxs-lookup"><span data-stu-id="75db2-121">Building a custom scanning experience</span></span>

<span data-ttu-id="75db2-122">Les applications peuvent décider d’analyser les données de mappage spatial au début de l’expérience pour déterminer s’ils veulent que l’utilisateur d’effectuer des étapes supplémentaires pour améliorer son exhaustivité et la qualité.</span><span class="sxs-lookup"><span data-stu-id="75db2-122">Applications may decide to analyze the spatial mapping data at the start of the experience to judge whether they want the user to perform additional steps to improve its completeness and quality.</span></span> <span data-ttu-id="75db2-123">Si l’analyse indique la qualité doit être améliorée, les développeurs doivent fournir une visualisation à superposer sur le monde entier pour indiquer :</span><span class="sxs-lookup"><span data-stu-id="75db2-123">If analysis indicates quality should be improved, developers should provide a visualization to overlay on the world to indicate:</span></span>
* <span data-ttu-id="75db2-124">La quantité du volume total à proximité des utilisateurs doit faire partie de l’expérience</span><span class="sxs-lookup"><span data-stu-id="75db2-124">How much of the total volume in the users vicinity needs to be part of the experience</span></span>
* <span data-ttu-id="75db2-125">Où l’utilisateur doit accéder pour améliorer les données</span><span class="sxs-lookup"><span data-stu-id="75db2-125">Where the user should go to improve data</span></span>

<span data-ttu-id="75db2-126">Les utilisateurs ne savent pas ce qui rend une analyse « bonne ».</span><span class="sxs-lookup"><span data-stu-id="75db2-126">Users do not know what makes a "good" scan.</span></span> <span data-ttu-id="75db2-127">Ils doivent être affichés ou dit que ce que vous recherchez s’il leur sont demandés pour évaluer une analyse – apparence à deux dimensions, la distance entre les murs réels, etc. Le développeur doit implémenter une boucle de rétroaction qui inclut l’actualisation des données de mappage spatial pendant la phase d’analyse ou l’exploration.</span><span class="sxs-lookup"><span data-stu-id="75db2-127">They need to be shown or told what to look for if they’re asked to evaluate a scan – flatness, distance from actual walls, etc. The developer should implement a feedback loop that includes refreshing the spatial mapping data during the scanning or exploration phase.</span></span>

<span data-ttu-id="75db2-128">Dans de nombreux cas, il peut être préférable d’indiquer à l’utilisateur de ce qu’ils doivent (par exemple, examinez le plafond, recherchez derrière meubles), afin d’obtenir la qualité d’analyse nécessaires.</span><span class="sxs-lookup"><span data-stu-id="75db2-128">In many cases, it may be best to tell the user what they need to do (e.g. look at the ceiling, look behind furniture), in order to get the necessary scan quality.</span></span>

## <a name="cached-versus-continuous-spatial-mapping"></a><span data-ttu-id="75db2-129">Mise en cache et continue mappage spatial</span><span class="sxs-lookup"><span data-stu-id="75db2-129">Cached versus continuous spatial mapping</span></span>

<span data-ttu-id="75db2-130">Les données de mappage spatial sont le poids de la plus importante des applications de source de données peuvent consommer.</span><span class="sxs-lookup"><span data-stu-id="75db2-130">The spatial mapping data is the most heavy weight data source applications can consume.</span></span> <span data-ttu-id="75db2-131">Pour éviter les problèmes de performances telles que suppression d’images ou interruption du son, la consommation de ces données doit être mûrement.</span><span class="sxs-lookup"><span data-stu-id="75db2-131">To avoid performance issues such as dropped frames or stuttering, consumption of this data should be done carefully.</span></span>

<span data-ttu-id="75db2-132">Analyse active durant une expérience peut être bénéfiques ou nuisibles et le développeur doit décider quelle méthode à utiliser en fonction de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="75db2-132">Active scanning during an experience can be both beneficial or detrimental and the developer will need to decide which method to use based on the experience.</span></span>

### <a name="cached-spatial-mapping"></a><span data-ttu-id="75db2-133">Mise en cache de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="75db2-133">Cached spatial mapping</span></span>

<span data-ttu-id="75db2-134">Dans le cas de mappage spatial mis en cache, l’application est généralement prend un instantané des données de mappage spatial et utilise cette capture instantanée pendant la durée de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="75db2-134">In the case of cached spatial mapping, the application typically takes a snapshot of the spatial mapping data and uses this snapshot for the duration of the experience.</span></span>

<span data-ttu-id="75db2-135">**Avantages**</span><span class="sxs-lookup"><span data-stu-id="75db2-135">**Benefits**</span></span>
* <span data-ttu-id="75db2-136">Réduction des coûts sur le système pendant que l’expérience est en cours d’exécution pointe à une puissance importante, thermique et gains de performance de processeur.</span><span class="sxs-lookup"><span data-stu-id="75db2-136">Reduced overhead on the system while the experience is running leading to dramatic power, thermal and cpu performance gains.</span></span>
* <span data-ttu-id="75db2-137">Une implémentation plus simple de l’expérience principale dans la mesure où il n’est pas interrompu par des modifications dans les données spatiales.</span><span class="sxs-lookup"><span data-stu-id="75db2-137">A simpler implementation of the main experience since it is not interrupted by changes in the spatial data.</span></span>
* <span data-ttu-id="75db2-138">Une seule une fois tout post-traitement des données spatiales pour les graphismes, graphiques et autres à des fins de coûts.</span><span class="sxs-lookup"><span data-stu-id="75db2-138">A single one time cost on any post processing of the spatial data for physics, graphics and other purposes.</span></span>

<span data-ttu-id="75db2-139">**Drawbacks**</span><span class="sxs-lookup"><span data-stu-id="75db2-139">**Drawbacks**</span></span>
* <span data-ttu-id="75db2-140">Le déplacement des objets du monde réel ou des personnes n’est pas reflété par les données en cache.</span><span class="sxs-lookup"><span data-stu-id="75db2-140">The movement of real world objects or people is not reflected by the cached data.</span></span> <span data-ttu-id="75db2-141">Exemple</span><span class="sxs-lookup"><span data-stu-id="75db2-141">E.g.</span></span> <span data-ttu-id="75db2-142">l’application peut prendre en compte une porte ouverte lorsqu’il est fermé en fait maintenant.</span><span class="sxs-lookup"><span data-stu-id="75db2-142">the application might consider a door open when it is actually closed now.</span></span>
* <span data-ttu-id="75db2-143">Mémoire potentiellement plus de l’application à mettre à jour la version mise en cache des données.</span><span class="sxs-lookup"><span data-stu-id="75db2-143">Potentially more application memory to maintain the cached version of the data.</span></span>

<span data-ttu-id="75db2-144">Un bon cas pour cette méthode est un environnement contrôlé ou un jeu en haut de la table.</span><span class="sxs-lookup"><span data-stu-id="75db2-144">A good case for this method is a controlled environment or a table top game.</span></span>

### <a name="continuous-spatial-mapping"></a><span data-ttu-id="75db2-145">Mappage spatial continue</span><span class="sxs-lookup"><span data-stu-id="75db2-145">Continuous spatial mapping</span></span>

<span data-ttu-id="75db2-146">Certaines applications peuvent reposer sur poursuit l’analyse pour actualiser les données de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="75db2-146">Certain applications may rely on continues scanning to refresh spatial mapping data.</span></span>

<span data-ttu-id="75db2-147">**Avantages**</span><span class="sxs-lookup"><span data-stu-id="75db2-147">**Benefits**</span></span>
* <span data-ttu-id="75db2-148">Vous n’avez pas besoin de générer un distinct analyse ou l’exploration expérience dès le départ dans votre application.</span><span class="sxs-lookup"><span data-stu-id="75db2-148">You don't need to build in a separate scanning or exploration experience upfront in your application.</span></span>
* <span data-ttu-id="75db2-149">Le déplacement des objets du monde réel peut être reflété par le jeu, mais avec un délai.</span><span class="sxs-lookup"><span data-stu-id="75db2-149">The movement of real world objects can be reflected by the game, although with some delay.</span></span>

<span data-ttu-id="75db2-150">**Drawbacks**</span><span class="sxs-lookup"><span data-stu-id="75db2-150">**Drawbacks**</span></span>
* <span data-ttu-id="75db2-151">Plus haute complexité dans l’implémentation de l’expérience principale.</span><span class="sxs-lookup"><span data-stu-id="75db2-151">Higher complexity in the implementation of the main experience.</span></span>
* <span data-ttu-id="75db2-152">Risque de surcharge du traitement supplémentaire pour le graphique ou physique en tant que modifications doivent être incrémentielle ingérés par ces systèmes.</span><span class="sxs-lookup"><span data-stu-id="75db2-152">Potential overhead of the additional processing for graphic or physics as changes need to be incrementally ingested by these systems.</span></span>
* <span data-ttu-id="75db2-153">Améliorer la puissance, thermique et impact sur le processeur.</span><span class="sxs-lookup"><span data-stu-id="75db2-153">Higher power, thermal and CPU impact.</span></span>

<span data-ttu-id="75db2-154">Un bon cas pour cette méthode est un où les hologrammes sont amenés à interagir avec le déplacement d’objets, par exemple, une voiture HOLOGRAPHIQUE que lecteurs sur le sol souhaitez correctement rencontrent une porte selon qu’il est ouvert ou fermé.</span><span class="sxs-lookup"><span data-stu-id="75db2-154">A good case for this method is one where holograms are expected to interact with moving objects, e.g. a holographic car that drives on the floor may want to correctly bump into a door depending on whether it is open or closed.</span></span>

## <a name="see-also"></a><span data-ttu-id="75db2-155">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="75db2-155">See also</span></span>
* [<span data-ttu-id="75db2-156">Conception du mappage spatial</span><span class="sxs-lookup"><span data-stu-id="75db2-156">Spatial mapping design</span></span>](spatial-mapping-design.md)
* [<span data-ttu-id="75db2-157">Systèmes de coordonnées</span><span class="sxs-lookup"><span data-stu-id="75db2-157">Coordinate systems</span></span>](coordinate-systems.md)
* [<span data-ttu-id="75db2-158">Conception du son spatial</span><span class="sxs-lookup"><span data-stu-id="75db2-158">Spatial sound design</span></span>](spatial-sound-design.md)
