---
title: Étude de cas - développer les capacités de mappage spatial d’HoloLens
description: Lors de la création de nos premières applications pour Microsoft HoloLens, nous avons impatients de voir simplement l’amplitude, nous risquons les limites du mappage spatial sur l’appareil.
author: jevertt
ms.author: jevertt
ms.date: 03/21/2018
ms.topic: article
keywords: Mappage spatial Windows Mixed Reality, HoloLens,
ms.openlocfilehash: 602b629afa5900ff34c28b3a3a32725af06590b7
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595753"
---
# <a name="case-study---expanding-the-spatial-mapping-capabilities-of-hololens"></a><span data-ttu-id="12e42-104">Étude de cas - développer les capacités de mappage spatial d’HoloLens</span><span class="sxs-lookup"><span data-stu-id="12e42-104">Case study - Expanding the spatial mapping capabilities of HoloLens</span></span>

<span data-ttu-id="12e42-105">Lors de la création de nos premières applications pour Microsoft HoloLens, nous avons impatients de voir simplement l’amplitude, nous risquons les limites du mappage spatial sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="12e42-105">When creating our first apps for Microsoft HoloLens, we were eager to see just how far we could push the boundaries of spatial mapping on the device.</span></span> <span data-ttu-id="12e42-106">Jeff Evertt, ingénieur logiciel chez Microsoft Studios, explique comment une nouvelle technologie a été développée en dehors de la nécessité de mieux contrôler comment les hologrammes sont placés dans un environnement d’utilisateur réel.</span><span class="sxs-lookup"><span data-stu-id="12e42-106">Jeff Evertt, a software engineer at Microsoft Studios, explains how a new technology was developed out of the need for more control over how holograms are placed in a user's real-world environment.</span></span>

## <a name="watch-the-video"></a><span data-ttu-id="12e42-107">Regardez la vidéo</span><span class="sxs-lookup"><span data-stu-id="12e42-107">Watch the video</span></span>

>[!VIDEO https://www.youtube.com/embed/iUmTi3_Ynus]

## <a name="beyond-spatial-mapping"></a><span data-ttu-id="12e42-108">Au-delà de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="12e42-108">Beyond spatial mapping</span></span>

<span data-ttu-id="12e42-109">Bien que nous travaillions sur [Fragments](https://www.microsoft.com/p/fragments/9nblggh5ggm8) et [Young pétarade](https://www.microsoft.com/p/young-conker/9nblggh5ggk1), deux des premiers jeux pour HoloLens, nous avons constaté que lorsque nous faisions placement procédurale de hologrammes dans le monde physique, nous avions besoin d’un niveau plus élevé des connaissances sur l’environnement utilisateur.</span><span class="sxs-lookup"><span data-stu-id="12e42-109">While we were working on [Fragments](https://www.microsoft.com/p/fragments/9nblggh5ggm8) and [Young Conker](https://www.microsoft.com/p/young-conker/9nblggh5ggk1), two of the first games for HoloLens, we found that when we were doing procedural placement of holograms in the physical world, we needed a higher level of understanding about the user's environment.</span></span> <span data-ttu-id="12e42-110">Chaque jeu avait ses propres besoins placement spécifique : Dans les Fragments, par exemple, nous souhaitons pouvoir faire la distinction entre les différentes surfaces, telles que la valeur plancher ou une table, pour placer des indices dans des endroits pertinents.</span><span class="sxs-lookup"><span data-stu-id="12e42-110">Each game had its own specific placement needs: In Fragments, for example, we wanted to be able to distinguish between different surfaces—such as the floor or a table—to place clues in relevant locations.</span></span> <span data-ttu-id="12e42-111">Nous souhaitons également être en mesure d’identifier les surfaces qui caractères HOLOGRAPHIQUE taille réelle pourraient se trouvent, par exemple un canapé ou chaise.</span><span class="sxs-lookup"><span data-stu-id="12e42-111">We also wanted to be able to identify surfaces that life-size holographic characters could sit on, such as a couch or a chair.</span></span> <span data-ttu-id="12e42-112">Dans pétarade Young, nous voulions pétarade et ses adversaires pour être en mesure d’utiliser des surfaces déclenchés dans la salle d’un joueur en tant que plateformes.</span><span class="sxs-lookup"><span data-stu-id="12e42-112">In Young Conker, we wanted Conker and his opponents to be able to use raised surfaces in a player's room as platforms.</span></span>

<span data-ttu-id="12e42-113">[Asobo Studios](http://www.asobostudio.com/index.html), notre partenaire de développement pour ces jeux, fait face à ce problème front et créé une technologie qui étend les fonctionnalités de mappage spatial de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="12e42-113">[Asobo Studios](http://www.asobostudio.com/index.html), our development partner for these games, faced this problem head-on and created a technology that extends the spatial mapping capabilities of HoloLens.</span></span> <span data-ttu-id="12e42-114">À l’aide de cela, nous pouvons analyser l’espace d’un joueur et identifier les surfaces, murs, tables, chaises et étages.</span><span class="sxs-lookup"><span data-stu-id="12e42-114">Using this, we could analyze a player's room and identify surfaces such as walls, tables, chairs, and floors.</span></span> <span data-ttu-id="12e42-115">Nous avons reçu également la possibilité d’optimiser par rapport à un ensemble de contraintes pour déterminer le meilleur placement pour les objets HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="12e42-115">It also gave us the ability to optimize against a set of constraints to determine the best placement for holographic objects.</span></span>

## <a name="the-spatial-understanding-code"></a><span data-ttu-id="12e42-116">Le code de présentation spatial</span><span class="sxs-lookup"><span data-stu-id="12e42-116">The spatial understanding code</span></span>

<span data-ttu-id="12e42-117">Nous a pris le code d’origine du Asobo et créé une bibliothèque qui encapsule cette technologie.</span><span class="sxs-lookup"><span data-stu-id="12e42-117">We took Asobo's original code and created a library that encapsulates this technology.</span></span> <span data-ttu-id="12e42-118">Microsoft et Asobo ont maintenant ce code open source et qu’il est disponible sur [MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialMapping) que vous pouvez utiliser dans vos propres projets.</span><span class="sxs-lookup"><span data-stu-id="12e42-118">Microsoft and Asobo have now open-sourced this code and made it available on [MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialMapping) for you to use in your own projects.</span></span> <span data-ttu-id="12e42-119">Tout le code source est inclus, ce qui vous permet de le personnaliser selon vos besoins et partager vos améliorations avec la Communauté.</span><span class="sxs-lookup"><span data-stu-id="12e42-119">All the source code is included, allowing you to customize it to your needs and share your improvements with the community.</span></span> <span data-ttu-id="12e42-120">Le code pour le C++ Solveur a été encapsulé dans une DLL UWP et exposé à Unity avec un [préfabriqué de dernière minute contenue dans MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/SpatialUnderstanding).</span><span class="sxs-lookup"><span data-stu-id="12e42-120">The code for the C++ solver has been wrapped into a UWP DLL and exposed to Unity with a [drop-in prefab contained within MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/SpatialUnderstanding).</span></span>

<span data-ttu-id="12e42-121">Il existe de nombreuses requêtes utiles inclus dans l’exemple Unity qui vous permet de rechercher des espaces vides sur les murs, placer des objets sur le plafond ou sur les espaces de grande taille sur le sol, identifier les endroits pour les caractères dans cet état et une myriade d’autres requêtes spatiales compréhension.</span><span class="sxs-lookup"><span data-stu-id="12e42-121">There are many useful queries included in the Unity sample that will allow you to find empty spaces on walls, place objects on the ceiling or on large spaces on the floor, identify places for characters to sit, and a myriad of other spatial understanding queries.</span></span>

<span data-ttu-id="12e42-122">Alors que la solution de mappage spatial fournie par HoloLens est conçue pour être suffisamment générique pour répondre aux besoins de toute la gamme des espaces de problème, le module de présentation spatial a été créé pour prendre en charge les besoins de deux jeux spécifiques.</span><span class="sxs-lookup"><span data-stu-id="12e42-122">While the spatial mapping solution provided by HoloLens is designed to be generic enough to meet the needs of the entire gamut of problem spaces, the spatial understanding module was built to support the needs of two specific games.</span></span> <span data-ttu-id="12e42-123">Par conséquent, sa solution est structurée autour d’un processus spécifique et des hypothèses :</span><span class="sxs-lookup"><span data-stu-id="12e42-123">As such, its solution is structured around a specific process and set of assumptions:</span></span>
* <span data-ttu-id="12e42-124">**Correction de taille playspace**: L’utilisateur spécifie la taille maximale playspace dans l’appel d’init.</span><span class="sxs-lookup"><span data-stu-id="12e42-124">**Fixed size playspace**: The user specifies the maximum playspace size in the init call.</span></span>
* <span data-ttu-id="12e42-125">**Le processus d’analyse à usage unique**: Le processus nécessite un discrètes phase où l’utilisateur parcourt autour d’analyse, en définissant le playspace.</span><span class="sxs-lookup"><span data-stu-id="12e42-125">**One-time scan process**: The process requires a discrete scanning phase where the user walks around, defining the playspace.</span></span> <span data-ttu-id="12e42-126">Fonctions de requête ne fonctionnera pas tant qu’une fois l’analyse a été finalisé.</span><span class="sxs-lookup"><span data-stu-id="12e42-126">Query functions will not function until after the scan has been finalized.</span></span>
* <span data-ttu-id="12e42-127">**Utilisateur driven playspace « peinture »**: Pendant la phase d’analyse, l’utilisateur déplace et recherche autour de la playspace, peinture efficacement les zones qui doivent être incluses.</span><span class="sxs-lookup"><span data-stu-id="12e42-127">**User driven playspace “painting”**: During the scanning phase, the user moves and looks around the playspace, effectively painting the areas which should be included.</span></span> <span data-ttu-id="12e42-128">Le maillage généré est important de fournir des commentaires des utilisateurs durant cette phase.</span><span class="sxs-lookup"><span data-stu-id="12e42-128">The generated mesh is important to provide user feedback during this phase.</span></span>
* <span data-ttu-id="12e42-129">**À l’intérieur le programme d’installation de votre domicile ou office**: Les fonctions de requête sont conçues autour des surfaces plats et des murs à angle droit.</span><span class="sxs-lookup"><span data-stu-id="12e42-129">**Indoors home or office setup**: The query functions are designed around flat surfaces and walls at right angles.</span></span> <span data-ttu-id="12e42-130">Il s’agit d’une limitation logicielle.</span><span class="sxs-lookup"><span data-stu-id="12e42-130">This is a soft limitation.</span></span> <span data-ttu-id="12e42-131">Toutefois, pendant la phase d’analyse, une analyse de l’axe principal est prévue pour optimiser le pavage de maille le long de l’axe principal et secondaire.</span><span class="sxs-lookup"><span data-stu-id="12e42-131">However, during the scanning phase, a primary axis analysis is completed to optimize the mesh tessellation along major and minor axis.</span></span>

### <a name="room-scanning-process"></a><span data-ttu-id="12e42-132">Processus d’analyse salle</span><span class="sxs-lookup"><span data-stu-id="12e42-132">Room Scanning Process</span></span>

<span data-ttu-id="12e42-133">Lorsque vous chargez le module de présentation spatiales, la première chose que vous effectuerez est analyse votre espace, par conséquent, toutes les surfaces utilisables, telles que le plancher, plafond et murs, sont identifiés et étiquetés.</span><span class="sxs-lookup"><span data-stu-id="12e42-133">When you load the spatial understanding module, the first thing you'll do is scan your space, so all the usable surfaces—such as the floor, ceiling, and walls—are identified and labeled.</span></span> <span data-ttu-id="12e42-134">Pendant le processus d’analyse, vous cherchez votre salle et « paint » les domaines qui doivent être inclus dans l’analyse.</span><span class="sxs-lookup"><span data-stu-id="12e42-134">During the scanning process, you look around your room and "paint' the areas that should be included in the scan.</span></span>

<span data-ttu-id="12e42-135">Le maillage observé pendant cette phase est une composante importante de retour visuel qui permet aux utilisateurs de savoir quelles parties de la salle de conversation sont en cours d’analyse.</span><span class="sxs-lookup"><span data-stu-id="12e42-135">The mesh seen during this phase is an important piece of visual feedback that lets users know what parts of the room are being scanned.</span></span> <span data-ttu-id="12e42-136">La DLL pour le module de présentation spatial stocke en interne la playspace sous forme de grille des cubes de voxel 8cm en taille réelle.</span><span class="sxs-lookup"><span data-stu-id="12e42-136">The DLL for the spatial understanding module internally stores the playspace as a grid of 8cm sized voxel cubes.</span></span> <span data-ttu-id="12e42-137">Au cours de la partie initiale d’analyse, une analyse du composant principal est terminée pour déterminer les axes de la salle.</span><span class="sxs-lookup"><span data-stu-id="12e42-137">During the initial part of scanning, a primary component analysis is completed to determine the axes of the room.</span></span> <span data-ttu-id="12e42-138">En interne, elle stocke son espace voxel alignée sur ces axes.</span><span class="sxs-lookup"><span data-stu-id="12e42-138">Internally, it stores its voxel space aligned to these axes.</span></span> <span data-ttu-id="12e42-139">Une maille est générée environ toutes les secondes en extrayant l’isosurface le volume voxel.</span><span class="sxs-lookup"><span data-stu-id="12e42-139">A mesh is generated approximately every second by extracting the isosurface from the voxel volume.</span></span>

![Spatiales mappage maille en blanc et présentation playspace maillage en vert](images/spatial-mapping-500px.png)

<span data-ttu-id="12e42-141">Spatiales mappage maille en blanc et présentation playspace maillage en vert</span><span class="sxs-lookup"><span data-stu-id="12e42-141">Spatial mapping mesh in white and understanding playspace mesh in green</span></span>



<span data-ttu-id="12e42-142">Le fichier SpatialUnderstanding.cs inclus gère le processus phase d’analyse.</span><span class="sxs-lookup"><span data-stu-id="12e42-142">The included SpatialUnderstanding.cs file manages the scanning phase process.</span></span> <span data-ttu-id="12e42-143">Il appelle les fonctions suivantes :</span><span class="sxs-lookup"><span data-stu-id="12e42-143">It calls the following functions:</span></span>
* <span data-ttu-id="12e42-144">**SpatialUnderstanding_Init**: Appelée une fois au début.</span><span class="sxs-lookup"><span data-stu-id="12e42-144">**SpatialUnderstanding_Init**: Called once at the start.</span></span>
* <span data-ttu-id="12e42-145">**GeneratePlayspace_InitScan**: Indique que la phase d’analyse doit commencer.</span><span class="sxs-lookup"><span data-stu-id="12e42-145">**GeneratePlayspace_InitScan**: Indicates that the scan phase should begin.</span></span>
* <span data-ttu-id="12e42-146">**GeneratePlayspace_UpdateScan_DynamicScan**: Appelé pour chaque trame pour mettre à jour le processus d’analyse.</span><span class="sxs-lookup"><span data-stu-id="12e42-146">**GeneratePlayspace_UpdateScan_DynamicScan**: Called each frame to update the scanning process.</span></span> <span data-ttu-id="12e42-147">La position de la caméra et l’orientation est transmise et est utilisé pour le processus de peinture playspace décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="12e42-147">The camera position and orientation is passed in and is used for the playspace painting process, described above.</span></span>
* <span data-ttu-id="12e42-148">**GeneratePlayspace_RequestFinish**: Appelé pour finaliser le playspace.</span><span class="sxs-lookup"><span data-stu-id="12e42-148">**GeneratePlayspace_RequestFinish**: Called to finalize the playspace.</span></span> <span data-ttu-id="12e42-149">Utiliser les zones « peints » pendant la phase d’analyse pour définir et verrouiller le playspace.</span><span class="sxs-lookup"><span data-stu-id="12e42-149">This will use the areas “painted” during the scan phase to define and lock the playspace.</span></span> <span data-ttu-id="12e42-150">L’application peut interroger les statistiques pendant la phase d’analyse, ainsi qu’une requête la maille personnalisée pour fournir des commentaires des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="12e42-150">The application can query statistics during the scanning phase as well as query the custom mesh for providing user feedback.</span></span>
* <span data-ttu-id="12e42-151">**Import_UnderstandingMesh**: Lors de l’analyse, le **SpatialUnderstandingCustomMesh** comportement fourni par le module et placé sur le préfabriqué compréhension interroge régulièrement le maillage personnalisé généré par le processus.</span><span class="sxs-lookup"><span data-stu-id="12e42-151">**Import_UnderstandingMesh**: During scanning, the **SpatialUnderstandingCustomMesh** behavior provided by the module and placed on the understanding prefab will periodically query the custom mesh generated by the process.</span></span> <span data-ttu-id="12e42-152">En outre, cela une fois de plus après que l’analyse a été finalisée.</span><span class="sxs-lookup"><span data-stu-id="12e42-152">In addition, this is done once more after scanning has been finalized.</span></span>

<span data-ttu-id="12e42-153">Le flux analyse, piloté par le **SpatialUnderstanding** comportement appels **InitScan**, puis **UpdateScan** chaque frame.</span><span class="sxs-lookup"><span data-stu-id="12e42-153">The scanning flow, driven by the **SpatialUnderstanding** behavior calls **InitScan**, then **UpdateScan** each frame.</span></span> <span data-ttu-id="12e42-154">Lorsque la requête de statistiques signale la couverture du raisonnable, l’utilisateur peut airtap pour appeler **RequestFinish** pour indiquer la fin de la phase d’analyse.</span><span class="sxs-lookup"><span data-stu-id="12e42-154">When the statistics query reports reasonable coverage, the user can airtap to call **RequestFinish** to indicate the end of the scanning phase.</span></span> <span data-ttu-id="12e42-155">**UpdateScan** continue à être appelée jusqu'à ce qu’il s’agit de retour la valeur indique que la DLL a terminé le traitement.</span><span class="sxs-lookup"><span data-stu-id="12e42-155">**UpdateScan** continues to be called until it’s return value indicates that the DLL has completed processing.</span></span>

## <a name="the-queries"></a><span data-ttu-id="12e42-156">Les requêtes</span><span class="sxs-lookup"><span data-stu-id="12e42-156">The queries</span></span>

<span data-ttu-id="12e42-157">Une fois que l’analyse est terminée, vous serez en mesure d’accéder aux trois différents types de requêtes dans l’interface :</span><span class="sxs-lookup"><span data-stu-id="12e42-157">Once the scan is complete, you'll be able to access three different types of queries in the interface:</span></span>
* <span data-ttu-id="12e42-158">**Requêtes de topologie**: Il s’agit des requêtes rapides qui reposent sur la topologie de la salle de conversation analysé.</span><span class="sxs-lookup"><span data-stu-id="12e42-158">**Topology queries**: These are fast queries that are based on the topology of the scanned room.</span></span>
* <span data-ttu-id="12e42-159">**Mettre en forme des requêtes**: Ils utilisent les résultats de vos requêtes de topologie pour rechercher des surfaces horizontales qui sont une bonne correspondance avec des formes personnalisées que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="12e42-159">**Shape queries**: These utilize the results of your topology queries to find horizontal surfaces that are a good match to custom shapes that you define.</span></span>
* <span data-ttu-id="12e42-160">**Requêtes de sélection élective de l’objet**: Il s’agit des requêtes plus complexes qui trouver l’emplacement ajusté selon un ensemble de règles et des contraintes pour l’objet.</span><span class="sxs-lookup"><span data-stu-id="12e42-160">**Object placement queries**: These are more complex queries that find the best-fit location based on a set of rules and constraints for the object.</span></span>

<span data-ttu-id="12e42-161">Outre les trois requêtes principales, il existe une interface raycasting qui peut être utilisée pour récupérer les types de surface avec balises et une maille de salle étanches personnalisé peut être copiée.</span><span class="sxs-lookup"><span data-stu-id="12e42-161">In addition to the three primary queries, there is a raycasting interface which can be used to retrieve tagged surface types and a custom watertight room mesh can be copied out.</span></span>

### <a name="topology-queries"></a><span data-ttu-id="12e42-162">Requêtes de topologie</span><span class="sxs-lookup"><span data-stu-id="12e42-162">Topology queries</span></span>

<span data-ttu-id="12e42-163">Dans la DLL, le Gestionnaire de topologie gère l’étiquetage de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="12e42-163">Within the DLL, the topology manager handles labeling of the environment.</span></span> <span data-ttu-id="12e42-164">Comme mentionné ci-dessus, les données sont stockées dans surfels, qui sont contenus dans un volume voxel.</span><span class="sxs-lookup"><span data-stu-id="12e42-164">As mentioned above, much of the data is stored within surfels, which are contained within a voxel volume.</span></span> <span data-ttu-id="12e42-165">En outre, le **PlaySpaceInfos** structure est utilisée pour stocker des informations sur le playspace, y compris l’alignement du monde (plus de détails ci-dessous), floor et au plafond.</span><span class="sxs-lookup"><span data-stu-id="12e42-165">In addition, the **PlaySpaceInfos** structure is used to store information about the playspace, including the world alignment (more details on this below), floor, and ceiling height.</span></span>

<span data-ttu-id="12e42-166">Heuristique utilisée pour déterminer les murs floor et ceiling.</span><span class="sxs-lookup"><span data-stu-id="12e42-166">Heuristics are used for determining floor, ceiling, and walls.</span></span> <span data-ttu-id="12e42-167">Par exemple, la surface plus grande et plus basses horizontale avec plus de 1 la surface d’exposition m2 est considéré comme le plancher.</span><span class="sxs-lookup"><span data-stu-id="12e42-167">For example, the largest and lowest horizontal surface with greater than 1 m2 surface area is considered the floor.</span></span> <span data-ttu-id="12e42-168">Notez que le chemin d’accès de l’appareil photo pendant le processus d’analyse est également utilisé dans ce processus.</span><span class="sxs-lookup"><span data-stu-id="12e42-168">Note that the camera path during the scanning process is also used in this process.</span></span>

<span data-ttu-id="12e42-169">Un sous-ensemble de requêtes exposées par le Gestionnaire de la topologie sont exposés via la DLL.</span><span class="sxs-lookup"><span data-stu-id="12e42-169">A subset of the queries exposed by the Topology manager are exposed out through the DLL.</span></span> <span data-ttu-id="12e42-170">Les requêtes de topologie exposés sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="12e42-170">The exposed topology queries are as follows:</span></span>
* <span data-ttu-id="12e42-171">QueryTopology_FindPositionsOnWalls</span><span class="sxs-lookup"><span data-stu-id="12e42-171">QueryTopology_FindPositionsOnWalls</span></span>
* <span data-ttu-id="12e42-172">QueryTopology_FindLargePositionsOnWalls</span><span class="sxs-lookup"><span data-stu-id="12e42-172">QueryTopology_FindLargePositionsOnWalls</span></span>
* <span data-ttu-id="12e42-173">QueryTopology_FindLargestWall</span><span class="sxs-lookup"><span data-stu-id="12e42-173">QueryTopology_FindLargestWall</span></span>
* <span data-ttu-id="12e42-174">QueryTopology_FindPositionsOnFloor</span><span class="sxs-lookup"><span data-stu-id="12e42-174">QueryTopology_FindPositionsOnFloor</span></span>
* <span data-ttu-id="12e42-175">QueryTopology_FindLargestPositionsOnFloor</span><span class="sxs-lookup"><span data-stu-id="12e42-175">QueryTopology_FindLargestPositionsOnFloor</span></span>
* <span data-ttu-id="12e42-176">QueryTopology_FindPositionsSittable</span><span class="sxs-lookup"><span data-stu-id="12e42-176">QueryTopology_FindPositionsSittable</span></span>

<span data-ttu-id="12e42-177">Chacune des requêtes a un ensemble de paramètres, spécifiques au type de requête.</span><span class="sxs-lookup"><span data-stu-id="12e42-177">Each of the queries has a set of parameters, specific to the query type.</span></span> <span data-ttu-id="12e42-178">Dans l’exemple suivant, l’utilisateur spécifie la hauteur minimale et la largeur du volume de votre choix, à la hauteur minimale de sélection élective au-dessus de la valeur plancher, la quantité minimale de dégagement devant le volume.</span><span class="sxs-lookup"><span data-stu-id="12e42-178">In the following example, the user specifies the minimum height & width of the desired volume, minimum placement height above the floor, and the minimum amount of clearance in front of the volume.</span></span> <span data-ttu-id="12e42-179">Toutes les mesures sont en mètres.</span><span class="sxs-lookup"><span data-stu-id="12e42-179">All measurements are in meters.</span></span>




```
EXTERN_C __declspec(dllexport) int QueryTopology_FindPositionsOnWalls(
          _In_ float minHeightOfWallSpace,
          _In_ float minWidthOfWallSpace,
          _In_ float minHeightAboveFloor,
          _In_ float minFacingClearance,
          _In_ int locationCount,
          _Inout_ Dll_Interface::TopologyResult* locationData)
```

<span data-ttu-id="12e42-180">Chacune de ces requêtes prend un tableau alloué au préalable de **TopologyResult** structures.</span><span class="sxs-lookup"><span data-stu-id="12e42-180">Each of these queries takes a pre-allocated array of **TopologyResult** structures.</span></span> <span data-ttu-id="12e42-181">Le **locationCount** paramètre spécifie la longueur du tableau passé.</span><span class="sxs-lookup"><span data-stu-id="12e42-181">The **locationCount** parameter specifies the length of the passed-in array.</span></span> <span data-ttu-id="12e42-182">La valeur de retour indique le nombre d’emplacements retournés.</span><span class="sxs-lookup"><span data-stu-id="12e42-182">The return value reports the number of returned locations.</span></span> <span data-ttu-id="12e42-183">Ce nombre n’est jamais supérieur à la passé dans **locationCount** paramètre.</span><span class="sxs-lookup"><span data-stu-id="12e42-183">This number is never greater than the passed-in **locationCount** parameter.</span></span>

<span data-ttu-id="12e42-184">Le **TopologyResult** contient la position centrale du volume retourné, la direction accessibles (par exemple, normale) et les dimensions de l’espace est trouvé.</span><span class="sxs-lookup"><span data-stu-id="12e42-184">The **TopologyResult** contains the center position of the returned volume, the facing direction (i.e. normal), and the dimensions of the found space.</span></span>




```
struct TopologyResult
     {
          DirectX::XMFLOAT3 position;
          DirectX::XMFLOAT3 normal;
          float width;
          float length;
     };
```

<span data-ttu-id="12e42-185">Notez que dans l’exemple Unity, chacune de ces requêtes est lié à un bouton dans le panneau de l’interface utilisateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="12e42-185">Note that in the Unity sample, each of these queries is linked up to a button in the virtual UI panel.</span></span> <span data-ttu-id="12e42-186">L’exemple dur codes les paramètres pour chacune de ces requêtes à des valeurs raisonnables.</span><span class="sxs-lookup"><span data-stu-id="12e42-186">The sample hard codes the parameters for each of these queries to reasonable values.</span></span> <span data-ttu-id="12e42-187">Consultez *SpaceVisualizer.cs* dans l’exemple de code pour plus d’exemples.</span><span class="sxs-lookup"><span data-stu-id="12e42-187">See *SpaceVisualizer.cs* in the sample code for more examples.</span></span>

### <a name="shape-queries"></a><span data-ttu-id="12e42-188">Requêtes de forme</span><span class="sxs-lookup"><span data-stu-id="12e42-188">Shape queries</span></span>

<span data-ttu-id="12e42-189">À l’intérieur de la DLL, l’Analyseur de forme (**ShapeAnalyzer_W**) utilise l’Analyseur de topologie à mettre en correspondance des formes personnalisées définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="12e42-189">Inside of the DLL, the shape analyzer (**ShapeAnalyzer_W**) uses the topology analyzer to match against custom shapes defined by the user.</span></span> <span data-ttu-id="12e42-190">L’exemple Unity a un ensemble prédéfini de formes qui figurent dans le menu de la requête, sous l’onglet de la forme.</span><span class="sxs-lookup"><span data-stu-id="12e42-190">The Unity sample has a pre-defined set of shapes which are shown in the query menu, on the shape tab.</span></span>

<span data-ttu-id="12e42-191">Notez que l’analyse de la forme fonctionne sur les surfaces horizontales uniquement.</span><span class="sxs-lookup"><span data-stu-id="12e42-191">Note that the shape analysis works on horizontal surfaces only.</span></span> <span data-ttu-id="12e42-192">Un canapé, par exemple, est défini par l’assise plat et haut plat de retour le canapé.</span><span class="sxs-lookup"><span data-stu-id="12e42-192">A couch, for example, is defined by the flat seat surface and the flat top of the couch back.</span></span> <span data-ttu-id="12e42-193">La requête shape recherche deux surfaces d’une plage de taille, la hauteur et aspect spécifique, avec les deux surfaces alignée et connecté.</span><span class="sxs-lookup"><span data-stu-id="12e42-193">The shape query looks for two surfaces of a specific size, height, and aspect range, with the two surfaces aligned and connected.</span></span> <span data-ttu-id="12e42-194">À l’aide de la terminologie de l’API, le siège canapé et le haut de l’arrière le canapé sont shape composants et l’alignement sur les exigences sont contraintes de composant de forme.</span><span class="sxs-lookup"><span data-stu-id="12e42-194">Using the APIs terminology, the couch seat and the top of the back of the couch are shape components and the alignment requirements are shape component constraints.</span></span>

<span data-ttu-id="12e42-195">Un exemple de requête définie dans l’exemple Unity (**ShapeDefinition.cs**), pour les objets « sittable » se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="12e42-195">An example query defined in the Unity sample (**ShapeDefinition.cs**), for “sittable” objects is as follows:</span></span>




```
shapeComponents = new List<ShapeComponent>()
     {
          new ShapeComponent(
               new List<ShapeComponentConstraint>()
               {
                    ShapeComponentConstraint.Create_SurfaceHeight_Between(0.2f, 0.6f),
                    ShapeComponentConstraint.Create_SurfaceCount_Min(1),
                    ShapeComponentConstraint.Create_SurfaceArea_Min(0.035f),
               }),
     };
     AddShape("Sittable", shapeComponents);
```

<span data-ttu-id="12e42-196">Chaque requête shape est défini par un ensemble de composants de la forme, chacun avec un ensemble de contraintes de composant et un ensemble de contraintes de forme qui répertorie les dépendances entre les composants.</span><span class="sxs-lookup"><span data-stu-id="12e42-196">Each shape query is defined by a set of shape components, each with a set of component constraints and a set of shape constraints which lists dependencies between the components.</span></span> <span data-ttu-id="12e42-197">Cet exemple inclut trois contraintes dans une définition de composant unique et aucune contrainte de forme entre les composants (comme il n’existe qu’un seul composant).</span><span class="sxs-lookup"><span data-stu-id="12e42-197">This example includes three constraints in a single component definition and no shape constraints between components (as there is only one component).</span></span>

<span data-ttu-id="12e42-198">En revanche, la forme de canapé a deux composants de forme et quatre contraintes de forme.</span><span class="sxs-lookup"><span data-stu-id="12e42-198">In contrast, the couch shape has two shape components and four shape constraints.</span></span> <span data-ttu-id="12e42-199">Notez que les composants sont identifiés par leur index dans la liste des composants de l’utilisateur (0 et 1 dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="12e42-199">Note that components are identified by their index in the user’s component list (0 and 1 in this example).</span></span>




```
shapeConstraints = new List<ShapeConstraint>()
        {
              ShapeConstraint.Create_RectanglesSameLength(0, 1, 0.6f),
              ShapeConstraint.Create_RectanglesParallel(0, 1),
              ShapeConstraint.Create_RectanglesAligned(0, 1, 0.3f),
              ShapeConstraint.Create_AtBackOf(1, 0),
        };
```

<span data-ttu-id="12e42-200">Fonctions de wrapper sont fournies dans le module Unity pour simplifier la création de définitions de formes personnalisée.</span><span class="sxs-lookup"><span data-stu-id="12e42-200">Wrapper functions are provided in the Unity module for easy creation of custom shape definitions.</span></span> <span data-ttu-id="12e42-201">Vous trouverez la liste complète des contraintes de composant et de forme dans **SpatialUnderstandingDll.cs** au sein de la **ShapeComponentConstraint** et **ShapeConstraint** structures.</span><span class="sxs-lookup"><span data-stu-id="12e42-201">The full list of component and shape constraints can be found in **SpatialUnderstandingDll.cs** within the **ShapeComponentConstraint** and the **ShapeConstraint** structures.</span></span>

![Rectangle bleu met en évidence les résultats de la requête shape chaise.](images/chair-shape-query-500px.png)

<span data-ttu-id="12e42-203">Rectangle bleu met en évidence les résultats de la requête shape chaise.</span><span class="sxs-lookup"><span data-stu-id="12e42-203">The blue rectangle highlights the results of the chair shape query.</span></span>



### <a name="object-placement-solver"></a><span data-ttu-id="12e42-204">Solveur de sélection élective d’objet</span><span class="sxs-lookup"><span data-stu-id="12e42-204">Object placement solver</span></span>

<span data-ttu-id="12e42-205">Requêtes de sélection élective d’objet peuvent être utilisés pour identifier les emplacements idéale dans la salle physique pour placer vos objets.</span><span class="sxs-lookup"><span data-stu-id="12e42-205">Object placement queries can be used to identify ideal locations in the physical room to place your objects.</span></span> <span data-ttu-id="12e42-206">Le Solveur recherche l’emplacement ajusté, étant donné les règles de l’objet et les contraintes.</span><span class="sxs-lookup"><span data-stu-id="12e42-206">The solver will find the best-fit location given the object rules and constraints.</span></span> <span data-ttu-id="12e42-207">En outre, les requêtes d’objet persistent jusqu'à ce que l’objet est supprimé avec **Solver_RemoveObject** ou **Solver_RemoveAllObjects** appels, ce qui contraint placement d’objets multiples.</span><span class="sxs-lookup"><span data-stu-id="12e42-207">In addition, object queries persist until the object is removed with **Solver_RemoveObject** or **Solver_RemoveAllObjects** calls, allowing constrained multi-object placement.</span></span>

<span data-ttu-id="12e42-208">Requêtes de sélection élective d’objet se composent de trois parties : le type d’emplacement avec les paramètres, une liste de règles et une liste de contraintes.</span><span class="sxs-lookup"><span data-stu-id="12e42-208">Object placement queries consist of three parts: placement type with parameters, a list of rules, and a list of constraints.</span></span> <span data-ttu-id="12e42-209">Pour exécuter une requête, utilisez l’API suivante :</span><span class="sxs-lookup"><span data-stu-id="12e42-209">To run a query, use the following API:</span></span>




```
public static int Solver_PlaceObject(
                [In] string objectName,
                [In] IntPtr placementDefinition,    // ObjectPlacementDefinition
                [In] int placementRuleCount,
                [In] IntPtr placementRules,         // ObjectPlacementRule
                [In] int constraintCount,
                [In] IntPtr placementConstraints,   // ObjectPlacementConstraint
                [Out] IntPtr placementResult)
```
<span data-ttu-id="12e42-210">Cette fonction accepte un nom d’objet, définition de placement et une liste des règles et des contraintes.</span><span class="sxs-lookup"><span data-stu-id="12e42-210">This function takes an object name, placement definition, and a list of rules and constraints.</span></span> <span data-ttu-id="12e42-211">Le C# wrappers fournissent des fonctions d’assistance pour faciliter la construction de règle et de contrainte de construction.</span><span class="sxs-lookup"><span data-stu-id="12e42-211">The C# wrappers provide construction helper functions to make rule and constraint construction easy.</span></span> <span data-ttu-id="12e42-212">La définition de placement contient le type de requête, autrement dit, une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="12e42-212">The placement definition contains the query type — that is, one of the following:</span></span>




```
public enum PlacementType
                {
                    Place_OnFloor,
                    Place_OnWall,
                    Place_OnCeiling,
                    Place_OnShape,
                    Place_OnEdge,
                    Place_OnFloorAndCeiling,
                    Place_RandomInAir,
                    Place_InMidAir,
                    Place_UnderFurnitureEdge,
                };
```

<span data-ttu-id="12e42-213">Chacun des types de sélection élective a un ensemble de paramètres uniques pour le type.</span><span class="sxs-lookup"><span data-stu-id="12e42-213">Each of the placement types has a set of parameters unique to the type.</span></span> <span data-ttu-id="12e42-214">Le **ObjectPlacementDefinition** structure contient un ensemble de fonctions d’assistance statiques pour la création de ces définitions.</span><span class="sxs-lookup"><span data-stu-id="12e42-214">The **ObjectPlacementDefinition** structure contains a set of static helper functions for creating these definitions.</span></span> <span data-ttu-id="12e42-215">Par exemple, pour rechercher un emplacement pour placer un objet sur le sol, vous pouvez utiliser la fonction suivante :</span><span class="sxs-lookup"><span data-stu-id="12e42-215">For example, to find a place to put an object on the floor, you can use the following function:</span></span> 


```
public static ObjectPlacementDefinition Create_OnFloor(Vector3 halfDims)
```

<span data-ttu-id="12e42-216">Outre le type de sélection élective, vous pouvez fournir un ensemble de règles et des contraintes.</span><span class="sxs-lookup"><span data-stu-id="12e42-216">In addition to the placement type, you can provide a set of rules and constraints.</span></span> <span data-ttu-id="12e42-217">Des règles ne peut pas être violées.</span><span class="sxs-lookup"><span data-stu-id="12e42-217">Rules cannot be violated.</span></span> <span data-ttu-id="12e42-218">Emplacements de positionnement possibles qui satisfont les type et les règles sont ensuite optimisés par rapport au jeu de contraintes pour sélectionner l’emplacement de placement optimal.</span><span class="sxs-lookup"><span data-stu-id="12e42-218">Possible placement locations that satisfy the type and rules are then optimized against the set of constraints to select the optimal placement location.</span></span> <span data-ttu-id="12e42-219">Chacune des règles et des contraintes peut être créé par les fonctions de création statique fourni.</span><span class="sxs-lookup"><span data-stu-id="12e42-219">Each of the rules and constraints can be created by the provided static creation functions.</span></span> <span data-ttu-id="12e42-220">Vous trouverez ci-dessous un exemple de fonction construction règle et de contrainte.</span><span class="sxs-lookup"><span data-stu-id="12e42-220">An example rule and constraint construction function is provided below.</span></span>




```
public static ObjectPlacementRule Create_AwayFromPosition(
                    Vector3 position, float minDistance)
               public static ObjectPlacementConstraint Create_NearPoint(
                    Vector3 position, float minDistance = 0.0f, float maxDistance = 0.0f)
```

<span data-ttu-id="12e42-221">La requête de sélection élective d’objet ci-dessous recherche un emplacement pour placer un cube de moitié compteur sur le bord d’une surface, autre précédemment placer des objets et près du centre de la salle.</span><span class="sxs-lookup"><span data-stu-id="12e42-221">The object placement query below is looking for a place to put a half meter cube on the edge of a surface, away from other previously place objects and near the center of the room.</span></span>




```
List<ObjectPlacementRule> rules = 
          new List<ObjectPlacementRule>() {
               ObjectPlacementRule.Create_AwayFromOtherObjects(1.0f),
          };

     List<ObjectPlacementConstraint> constraints = 
          new List<ObjectPlacementConstraint> {
               ObjectPlacementConstraint.Create_NearCenter(),
          };

     Solver_PlaceObject(
          “MyCustomObject”,
          new ObjectPlacementDefinition.Create_OnEdge(
          new Vector3(0.25f, 0.25f, 0.25f), 
          new Vector3(0.25f, 0.25f, 0.25f)),
          rules.Count,
          UnderstandingDLL.PinObject(rules.ToArray()),
          constraints.Count,
          UnderstandingDLL.PinObject(constraints.ToArray()),
          UnderstandingDLL.GetStaticObjectPlacementResultPtr());
```

<span data-ttu-id="12e42-222">En cas de réussite, une **ObjectPlacementResult** structure contenant la position de placement, de dimensions et de l’orientation est retournée.</span><span class="sxs-lookup"><span data-stu-id="12e42-222">If successful, an **ObjectPlacementResult** structure containing the placement position, dimensions and orientation is returned.</span></span> <span data-ttu-id="12e42-223">En outre, le positionnement est ajouté à la liste interne de la DLL d’objets placés.</span><span class="sxs-lookup"><span data-stu-id="12e42-223">In addition, the placement is added to the DLL’s internal list of placed objects.</span></span> <span data-ttu-id="12e42-224">Requêtes de sélection élective ultérieures prennent cet objet en compte.</span><span class="sxs-lookup"><span data-stu-id="12e42-224">Subsequent placement queries will take this object into account.</span></span> <span data-ttu-id="12e42-225">Le **LevelSolver.cs** fichier dans l’exemple Unity contient plusieurs exemples de requêtes.</span><span class="sxs-lookup"><span data-stu-id="12e42-225">The **LevelSolver.cs** file in the Unity sample contains more example queries.</span></span>

![Les cases bleues indiquent les résultats à partir de trois requêtes Place sur Floor avec des règles « suite à partir de la position d’une caméra ».](images/away-from-camera-position-500px.png)

<span data-ttu-id="12e42-227">Les cases bleues indiquent les résultats à partir de trois requêtes Place sur Floor avec des règles « suite à partir de la position d’une caméra ».</span><span class="sxs-lookup"><span data-stu-id="12e42-227">The blue boxes show the result from three Place On Floor queries with "away from camera position" rules.</span></span>


<span data-ttu-id="12e42-228">**Astuces :**</span><span class="sxs-lookup"><span data-stu-id="12e42-228">**Tips:**</span></span>
* <span data-ttu-id="12e42-229">Lors de la résolution pour l’emplacement du positionnement de plusieurs objets requis pour un scénario de niveau ou de l’application, tout d’abord résoudre les objets indispensables et de grande taille pour optimiser la probabilité qu’un espace peut être trouvé.</span><span class="sxs-lookup"><span data-stu-id="12e42-229">When solving for placement location of multiple objects required for a level or application scenario, first solve indispensable and large objects to maximize the probability that a space can be found.</span></span>
* <span data-ttu-id="12e42-230">Ordre de sélection élective est important.</span><span class="sxs-lookup"><span data-stu-id="12e42-230">Placement order is important.</span></span> <span data-ttu-id="12e42-231">Si le placement de l’objet est introuvable, essayez de configurations moins limitées.</span><span class="sxs-lookup"><span data-stu-id="12e42-231">If object placements cannot be found, try less constrained configurations.</span></span> <span data-ttu-id="12e42-232">Il est essentiel de prenant en charge des fonctionnalités sur de nombreuses configurations de salle de disposer d’un ensemble de configurations de secours.</span><span class="sxs-lookup"><span data-stu-id="12e42-232">Having a set of fallback configurations is critical to supporting functionality across many room configurations.</span></span>

### <a name="ray-casting"></a><span data-ttu-id="12e42-233">Ray cast</span><span class="sxs-lookup"><span data-stu-id="12e42-233">Ray casting</span></span>

<span data-ttu-id="12e42-234">Outre les trois requêtes principales, une interface de conversion de ray peut être utilisée pour récupérer des types de surface avec balises et d’une maille playspace étanches personnalisés peut être copiée out après la salle a été analysée et finalisée, étiquettes sont générés de manière interne pour les surfaces tels que le Floor, ceiling et murs.</span><span class="sxs-lookup"><span data-stu-id="12e42-234">In addition to the three primary queries, a ray casting interface can be used to retrieve tagged surface types and a custom watertight playspace mesh can be copied out After the room has been scanned and finalized, labels are internally generated for surfaces like the floor, ceiling, and walls.</span></span> <span data-ttu-id="12e42-235">Le **PlayspaceRaycast** fonction prend un rayon et retourne si le rayon est en conflit avec une surface connue et si tel est le cas, plus d’informations sur cette surface sous la forme d’un **RaycastResult**.</span><span class="sxs-lookup"><span data-stu-id="12e42-235">The **PlayspaceRaycast** function takes a ray and returns if the ray collides with a known surface and if so, information about that surface in the form of a **RaycastResult**.</span></span> 


```
struct RaycastResult
     {
          enum SurfaceTypes
          {
               Invalid, // No intersection
               Other,
               Floor,
               FloorLike,         // Not part of the floor topology, 
                                  //     but close to the floor and looks like the floor
               Platform,          // Horizontal platform between the ground and 
                                  //     the ceiling
               Ceiling,
               WallExternal,
               WallLike,          // Not part of the external wall surface, 
                                  //     but vertical surface that looks like a 
                                  //    wall structure
               };
               SurfaceTypes SurfaceType;
               float SurfaceArea;   // Zero if unknown 
                                        //  (i.e. if not part of the topology analysis)
               DirectX::XMFLOAT3 IntersectPoint;
               DirectX::XMFLOAT3 IntersectNormal;
     };
```

<span data-ttu-id="12e42-236">En interne, le raycast est calculée par rapport à la représentation sous forme de voxel calculée 8cm au cube de la playspace.</span><span class="sxs-lookup"><span data-stu-id="12e42-236">Internally, the raycast is computed against the computed 8cm cubed voxel representation of the playspace.</span></span> <span data-ttu-id="12e42-237">Chaque voxel contient un ensemble d’éléments de surface d’exposition des données de topologie traité (également appelé surfels).</span><span class="sxs-lookup"><span data-stu-id="12e42-237">Each voxel contains a set of surface elements with processed topology data (also known as surfels).</span></span> <span data-ttu-id="12e42-238">Les surfels contenues dans la cellule voxel intersectées sont comparées et la meilleure correspondance est utilisée pour rechercher les informations de topologie.</span><span class="sxs-lookup"><span data-stu-id="12e42-238">The surfels contained within the intersected voxel cell are compared and the best match used to look up the topology information.</span></span> <span data-ttu-id="12e42-239">Les données de cette topologie contient l’étiquetage retournée sous la forme de la **SurfaceTypes** enum, ainsi que de la surface d’exposition de la surface d’intersection.</span><span class="sxs-lookup"><span data-stu-id="12e42-239">This topology data contains the labeling returned in the form of the **SurfaceTypes** enum, as well as the surface area of the intersected surface.</span></span>

<span data-ttu-id="12e42-240">Dans l’exemple Unity, le curseur convertit un rayon chaque frame.</span><span class="sxs-lookup"><span data-stu-id="12e42-240">In the Unity sample, the cursor casts a ray each frame.</span></span> <span data-ttu-id="12e42-241">Tout d’abord, contre colliders de d’Unity ; en second lieu, par rapport à la représentation du monde du module de présentation ; et enfin, sur les éléments d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="12e42-241">First, against Unity’s colliders; second, against the understanding module’s world representation; and finally, against the UI elements.</span></span> <span data-ttu-id="12e42-242">Dans cette application, l’interface utilisateur obtient la priorité, puis le résultat de la présentation et enfin, colliders de d’Unity.</span><span class="sxs-lookup"><span data-stu-id="12e42-242">In this application, UI gets priority, then the understanding result, and finally, Unity’s colliders.</span></span> <span data-ttu-id="12e42-243">Le **SurfaceType** est signalé sous forme de texte en regard du curseur.</span><span class="sxs-lookup"><span data-stu-id="12e42-243">The **SurfaceType** is reported as text next to the cursor.</span></span>

![Résultat Raycast intersection avec la valeur plancher de création de rapports.](images/raycast-result-500px.jpg)

<span data-ttu-id="12e42-245">Résultat Raycast intersection avec la valeur plancher de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="12e42-245">Raycast result reporting intersection with the floor.</span></span>


## <a name="get-the-code"></a><span data-ttu-id="12e42-246">Obtenir le code</span><span class="sxs-lookup"><span data-stu-id="12e42-246">Get the code</span></span>

<span data-ttu-id="12e42-247">Le code open source est disponible dans [MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity).</span><span class="sxs-lookup"><span data-stu-id="12e42-247">The open-source code is available in [MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity).</span></span> <span data-ttu-id="12e42-248">Faites-le nous savoir sur le [Forums des développeurs HoloLens](https://forums.hololens.com/) si vous utilisez le code dans un projet.</span><span class="sxs-lookup"><span data-stu-id="12e42-248">Let us know on the [HoloLens Developer Forums](https://forums.hololens.com/) if you use the code in a project.</span></span> <span data-ttu-id="12e42-249">Nous sommes impatients de voir ce que vous en faire !</span><span class="sxs-lookup"><span data-stu-id="12e42-249">We can't wait to see what you do with it!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="12e42-250">À propos de l’auteur</span><span class="sxs-lookup"><span data-stu-id="12e42-250">About the author</span></span>

<table style="border:0;width:800px">
<tr>
<td style="border:0"> <img alt="Jeff Evertt, Software Engineering Lead at Microsoft" width="200" height="205" src="images/jeff-evertt-200px.jpg" /></td><td style="border:0"> <span data-ttu-id="12e42-251"><b>Jeff Evertt</b> est un prospect d’ingénierie logicielle qui a travaillé sur HoloLens depuis le début, à partir d’incubation en informatique pour expérimenter le développement.</span><span class="sxs-lookup"><span data-stu-id="12e42-251"><b>Jeff Evertt</b> is a software engineering lead who has worked on HoloLens since the early days, from incubation to experience development.</span></span> <span data-ttu-id="12e42-252">Avant de HoloLens, il a travaillé sur le Xbox Kinect et dans l’industrie de jeux sur un large éventail de plateformes et des jeux.</span><span class="sxs-lookup"><span data-stu-id="12e42-252">Before HoloLens, he worked on the Xbox Kinect and in the games industry on a wide variety of platforms and games.</span></span> <span data-ttu-id="12e42-253">Jeff est passionné de la robotique, des graphiques et des choses avec les voyants lumineux qui vont du signal sonore.</span><span class="sxs-lookup"><span data-stu-id="12e42-253">Jeff is passionate about robotics, graphics, and things with flashy lights that go beep.</span></span> <span data-ttu-id="12e42-254">Il aime apprendre de nouvelles choses et fonctionne sur le logiciel, matériel et en particulier dans l’espace où les deux se croisent.</span><span class="sxs-lookup"><span data-stu-id="12e42-254">He enjoys learning new things and working on software, hardware, and particularly in the space where the two intersect.</span></span></td>
</tr>
</table>



## <a name="see-also"></a><span data-ttu-id="12e42-255">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="12e42-255">See also</span></span>
* [<span data-ttu-id="12e42-256">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="12e42-256">Spatial mapping</span></span>](spatial-mapping.md)
* [<span data-ttu-id="12e42-257">Conception de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="12e42-257">Spatial mapping design</span></span>](spatial-mapping-design.md)
* [<span data-ttu-id="12e42-258">Visualisation d’analyse de salle</span><span class="sxs-lookup"><span data-stu-id="12e42-258">Room scan visualization</span></span>](room-scan-visualization.md)
* [<span data-ttu-id="12e42-259">MixedRealityToolkit-Unity</span><span class="sxs-lookup"><span data-stu-id="12e42-259">MixedRealityToolkit-Unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity)
* [<span data-ttu-id="12e42-260">Asobo Studio : Leçons à partir de la première ligne du développement de HoloLens</span><span class="sxs-lookup"><span data-stu-id="12e42-260">Asobo Studio: Lessons from the frontline of HoloLens development</span></span>](http://www.gamesindustry.biz/articles/2016-05-12-asobo-lessons-from-the-frontline-of-ar-development)
