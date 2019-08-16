---
title: Étude de cas-développement des fonctionnalités de mappage spatial de HoloLens
description: Lors de la création de nos premières applications pour Microsoft HoloLens, nous étions impatients de voir à quel moment nous pourrions pousser les limites du mappage spatial sur l’appareil.
author: jevertt
ms.author: jevertt
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, HoloLens, mappage spatial
ms.openlocfilehash: 602b629afa5900ff34c28b3a3a32725af06590b7
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63522718"
---
# <a name="case-study---expanding-the-spatial-mapping-capabilities-of-hololens"></a><span data-ttu-id="82829-104">Étude de cas-développement des fonctionnalités de mappage spatial de HoloLens</span><span class="sxs-lookup"><span data-stu-id="82829-104">Case study - Expanding the spatial mapping capabilities of HoloLens</span></span>

<span data-ttu-id="82829-105">Lors de la création de nos premières applications pour Microsoft HoloLens, nous étions impatients de voir à quel moment nous pourrions pousser les limites du mappage spatial sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="82829-105">When creating our first apps for Microsoft HoloLens, we were eager to see just how far we could push the boundaries of spatial mapping on the device.</span></span> <span data-ttu-id="82829-106">Jeff Evertt, ingénieur logiciel chez Microsoft Studios, explique comment une nouvelle technologie a été développée afin d’avoir davantage de contrôle sur la façon dont les hologrammes sont placés dans l’environnement réel d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="82829-106">Jeff Evertt, a software engineer at Microsoft Studios, explains how a new technology was developed out of the need for more control over how holograms are placed in a user's real-world environment.</span></span>

## <a name="watch-the-video"></a><span data-ttu-id="82829-107">Regarder la vidéo</span><span class="sxs-lookup"><span data-stu-id="82829-107">Watch the video</span></span>

>[!VIDEO https://www.youtube.com/embed/iUmTi3_Ynus]

## <a name="beyond-spatial-mapping"></a><span data-ttu-id="82829-108">Au-delà du mappage spatial</span><span class="sxs-lookup"><span data-stu-id="82829-108">Beyond spatial mapping</span></span>

<span data-ttu-id="82829-109">Alors que nous travaillions sur [Fragments](https://www.microsoft.com/p/fragments/9nblggh5ggm8) et [Young Conker](https://www.microsoft.com/p/young-conker/9nblggh5ggk1), deux des premiers jeux pour HoloLens, nous avons constaté que lorsque nous utilisions des hologrammes dans le monde physique, nous avions besoin d’un niveau de compréhension plus élevé de l’environnement utilisateur.</span><span class="sxs-lookup"><span data-stu-id="82829-109">While we were working on [Fragments](https://www.microsoft.com/p/fragments/9nblggh5ggm8) and [Young Conker](https://www.microsoft.com/p/young-conker/9nblggh5ggk1), two of the first games for HoloLens, we found that when we were doing procedural placement of holograms in the physical world, we needed a higher level of understanding about the user's environment.</span></span> <span data-ttu-id="82829-110">Chaque jeu avait ses propres besoins spécifiques en matière de placement: Par exemple, dans les fragments, nous souhaitons pouvoir faire la distinction entre les différentes surfaces, telles que le plancher ou un tableau, pour placer des indices à des endroits pertinents.</span><span class="sxs-lookup"><span data-stu-id="82829-110">Each game had its own specific placement needs: In Fragments, for example, we wanted to be able to distinguish between different surfaces—such as the floor or a table—to place clues in relevant locations.</span></span> <span data-ttu-id="82829-111">Nous souhaitons également pouvoir identifier les surfaces sur lesquelles les caractères holographiques de taille vie peuvent se trouver, tels qu’un canapé ou une chaise.</span><span class="sxs-lookup"><span data-stu-id="82829-111">We also wanted to be able to identify surfaces that life-size holographic characters could sit on, such as a couch or a chair.</span></span> <span data-ttu-id="82829-112">Dans jeune Conker, nous souhaitons que Conker et ses adversaires soient en mesure d’utiliser des surfaces en relief dans la salle d’un joueur en tant que plateformes.</span><span class="sxs-lookup"><span data-stu-id="82829-112">In Young Conker, we wanted Conker and his opponents to be able to use raised surfaces in a player's room as platforms.</span></span>

<span data-ttu-id="82829-113">[Asobo Studios](http://www.asobostudio.com/index.html), notre partenaire de développement de ces jeux, est confronté à ce problème et a créé une technologie qui étend les fonctionnalités de mappage spatial de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="82829-113">[Asobo Studios](http://www.asobostudio.com/index.html), our development partner for these games, faced this problem head-on and created a technology that extends the spatial mapping capabilities of HoloLens.</span></span> <span data-ttu-id="82829-114">À l’aide de cela, nous pourrions analyser la salle d’un joueur et identifier des surfaces telles que des murs, des tables, des chaises et des sols.</span><span class="sxs-lookup"><span data-stu-id="82829-114">Using this, we could analyze a player's room and identify surfaces such as walls, tables, chairs, and floors.</span></span> <span data-ttu-id="82829-115">Elle nous a également donné la possibilité d’optimiser par rapport à un ensemble de contraintes pour déterminer le meilleur placement pour les objets holographiques.</span><span class="sxs-lookup"><span data-stu-id="82829-115">It also gave us the ability to optimize against a set of constraints to determine the best placement for holographic objects.</span></span>

## <a name="the-spatial-understanding-code"></a><span data-ttu-id="82829-116">Code de la compréhension spatiale</span><span class="sxs-lookup"><span data-stu-id="82829-116">The spatial understanding code</span></span>

<span data-ttu-id="82829-117">Nous avons pris le code d’origine de Asobo et créé une bibliothèque qui encapsule cette technologie.</span><span class="sxs-lookup"><span data-stu-id="82829-117">We took Asobo's original code and created a library that encapsulates this technology.</span></span> <span data-ttu-id="82829-118">Microsoft et Asobo ont à présent ouvert ce code en open source et le rend disponible sur [MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialMapping) pour que vous l’utilisiez dans vos propres projets.</span><span class="sxs-lookup"><span data-stu-id="82829-118">Microsoft and Asobo have now open-sourced this code and made it available on [MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialMapping) for you to use in your own projects.</span></span> <span data-ttu-id="82829-119">Tout le code source est inclus, ce qui vous permet de le personnaliser en fonction de vos besoins et de partager vos améliorations avec la communauté.</span><span class="sxs-lookup"><span data-stu-id="82829-119">All the source code is included, allowing you to customize it to your needs and share your improvements with the community.</span></span> <span data-ttu-id="82829-120">Le code du C++ solveur a été encapsulé dans une dll UWP et exposé à Unity avec une [Prefab de dépôt contenue dans MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/SpatialUnderstanding).</span><span class="sxs-lookup"><span data-stu-id="82829-120">The code for the C++ solver has been wrapped into a UWP DLL and exposed to Unity with a [drop-in prefab contained within MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/SpatialUnderstanding).</span></span>

<span data-ttu-id="82829-121">L’exemple Unity contient de nombreuses requêtes utiles qui vous permettent de rechercher des espaces vides sur les murs, de placer des objets sur le plafond ou sur des grands espaces sur le plancher, d’identifier des emplacements pour les caractères à asseoir et une multitude d’autres requêtes de compréhension spatiale.</span><span class="sxs-lookup"><span data-stu-id="82829-121">There are many useful queries included in the Unity sample that will allow you to find empty spaces on walls, place objects on the ceiling or on large spaces on the floor, identify places for characters to sit, and a myriad of other spatial understanding queries.</span></span>

<span data-ttu-id="82829-122">Bien que la solution de mappage spatial fournie par HoloLens soit conçue pour être suffisamment générique pour répondre aux besoins de la gamme complète des espaces à problème, le module de compréhension spatiale a été conçu pour prendre en charge les besoins de deux jeux spécifiques.</span><span class="sxs-lookup"><span data-stu-id="82829-122">While the spatial mapping solution provided by HoloLens is designed to be generic enough to meet the needs of the entire gamut of problem spaces, the spatial understanding module was built to support the needs of two specific games.</span></span> <span data-ttu-id="82829-123">Par conséquent, sa solution est structurée autour d’un processus et d’un ensemble d’hypothèses spécifiques:</span><span class="sxs-lookup"><span data-stu-id="82829-123">As such, its solution is structured around a specific process and set of assumptions:</span></span>
* <span data-ttu-id="82829-124">**Taille fixe PlaySpace**: L’utilisateur spécifie la taille maximale de PlaySpace dans l’appel init.</span><span class="sxs-lookup"><span data-stu-id="82829-124">**Fixed size playspace**: The user specifies the maximum playspace size in the init call.</span></span>
* <span data-ttu-id="82829-125">**Processus d’analyse à usage unique**: Le processus nécessite une phase d’analyse discrète dans laquelle l’utilisateur se contourne et définit le PlaySpace.</span><span class="sxs-lookup"><span data-stu-id="82829-125">**One-time scan process**: The process requires a discrete scanning phase where the user walks around, defining the playspace.</span></span> <span data-ttu-id="82829-126">Les fonctions de requête ne fonctionneront pas tant que l’analyse n’aura pas été finalisée.</span><span class="sxs-lookup"><span data-stu-id="82829-126">Query functions will not function until after the scan has been finalized.</span></span>
* <span data-ttu-id="82829-127">**«Peinture» PlaySpace pilotée par l’utilisateur**: Pendant la phase d’analyse, l’utilisateur se déplace et recherche des PlaySpace, ce qui a pour effet de peindre les zones qui doivent être incluses.</span><span class="sxs-lookup"><span data-stu-id="82829-127">**User driven playspace “painting”**: During the scanning phase, the user moves and looks around the playspace, effectively painting the areas which should be included.</span></span> <span data-ttu-id="82829-128">La maille générée est importante pour fournir des commentaires de l’utilisateur au cours de cette phase.</span><span class="sxs-lookup"><span data-stu-id="82829-128">The generated mesh is important to provide user feedback during this phase.</span></span>
* <span data-ttu-id="82829-129">**Installation à la page d’hébergement ou d’entreprise**: Les fonctions de requête sont conçues autour des surfaces plates et des parois à des angles droits.</span><span class="sxs-lookup"><span data-stu-id="82829-129">**Indoors home or office setup**: The query functions are designed around flat surfaces and walls at right angles.</span></span> <span data-ttu-id="82829-130">Il s’agit d’une limitation souple.</span><span class="sxs-lookup"><span data-stu-id="82829-130">This is a soft limitation.</span></span> <span data-ttu-id="82829-131">Toutefois, pendant la phase d’analyse, une analyse de l’axe principal est effectuée pour optimiser la facettisation du maillage le long de l’axe principal et de l’axe secondaire.</span><span class="sxs-lookup"><span data-stu-id="82829-131">However, during the scanning phase, a primary axis analysis is completed to optimize the mesh tessellation along major and minor axis.</span></span>

### <a name="room-scanning-process"></a><span data-ttu-id="82829-132">Processus d’analyse de la salle</span><span class="sxs-lookup"><span data-stu-id="82829-132">Room Scanning Process</span></span>

<span data-ttu-id="82829-133">Lorsque vous chargez le module de compréhension spatiale, la première chose à faire est d’analyser votre espace. par conséquent, toutes les surfaces utilisables (telles que le plancher, le plafond et les murs) sont identifiées et étiquetées.</span><span class="sxs-lookup"><span data-stu-id="82829-133">When you load the spatial understanding module, the first thing you'll do is scan your space, so all the usable surfaces—such as the floor, ceiling, and walls—are identified and labeled.</span></span> <span data-ttu-id="82829-134">Pendant le processus d’analyse, vous examinez votre espace et «peignez» les zones qui doivent être incluses dans l’analyse.</span><span class="sxs-lookup"><span data-stu-id="82829-134">During the scanning process, you look around your room and "paint' the areas that should be included in the scan.</span></span>

<span data-ttu-id="82829-135">Le maillage vu pendant cette phase est un élément important de retour visuel qui permet aux utilisateurs de savoir quelles parties de la salle sont analysées.</span><span class="sxs-lookup"><span data-stu-id="82829-135">The mesh seen during this phase is an important piece of visual feedback that lets users know what parts of the room are being scanned.</span></span> <span data-ttu-id="82829-136">La DLL du module de compréhension spatiale stocke en interne le PlaySpace sous la forme d’une grille de cubes voxel de 8cm dimensionnés.</span><span class="sxs-lookup"><span data-stu-id="82829-136">The DLL for the spatial understanding module internally stores the playspace as a grid of 8cm sized voxel cubes.</span></span> <span data-ttu-id="82829-137">Au cours de la phase initiale d’analyse, une analyse de composant principale est effectuée pour déterminer les axes de la salle.</span><span class="sxs-lookup"><span data-stu-id="82829-137">During the initial part of scanning, a primary component analysis is completed to determine the axes of the room.</span></span> <span data-ttu-id="82829-138">En interne, elle stocke son espace voxel aligné sur ces axes.</span><span class="sxs-lookup"><span data-stu-id="82829-138">Internally, it stores its voxel space aligned to these axes.</span></span> <span data-ttu-id="82829-139">Une maille est générée environ chaque seconde en extrayant le isosurface du volume voxel.</span><span class="sxs-lookup"><span data-stu-id="82829-139">A mesh is generated approximately every second by extracting the isosurface from the voxel volume.</span></span>

![Mappage spatial maillage en blanc et compréhension du maillage PlaySpace en vert](images/spatial-mapping-500px.png)

<span data-ttu-id="82829-141">Mappage spatial maillage en blanc et compréhension du maillage PlaySpace en vert</span><span class="sxs-lookup"><span data-stu-id="82829-141">Spatial mapping mesh in white and understanding playspace mesh in green</span></span>



<span data-ttu-id="82829-142">Le fichier SpatialUnderstanding.cs inclus gère le processus de phase d’analyse.</span><span class="sxs-lookup"><span data-stu-id="82829-142">The included SpatialUnderstanding.cs file manages the scanning phase process.</span></span> <span data-ttu-id="82829-143">Il appelle les fonctions suivantes:</span><span class="sxs-lookup"><span data-stu-id="82829-143">It calls the following functions:</span></span>
* <span data-ttu-id="82829-144">**SpatialUnderstanding_Init**: Appelée une fois au début.</span><span class="sxs-lookup"><span data-stu-id="82829-144">**SpatialUnderstanding_Init**: Called once at the start.</span></span>
* <span data-ttu-id="82829-145">**GeneratePlayspace_InitScan**: Indique que la phase d’analyse doit commencer.</span><span class="sxs-lookup"><span data-stu-id="82829-145">**GeneratePlayspace_InitScan**: Indicates that the scan phase should begin.</span></span>
* <span data-ttu-id="82829-146">**GeneratePlayspace_UpdateScan_DynamicScan**: Appelé chaque frame pour mettre à jour le processus d’analyse.</span><span class="sxs-lookup"><span data-stu-id="82829-146">**GeneratePlayspace_UpdateScan_DynamicScan**: Called each frame to update the scanning process.</span></span> <span data-ttu-id="82829-147">La position et l’orientation de la caméra sont transmises et sont utilisées pour le processus de peinture PlaySpace décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="82829-147">The camera position and orientation is passed in and is used for the playspace painting process, described above.</span></span>
* <span data-ttu-id="82829-148">**GeneratePlayspace_RequestFinish**: Appelé pour finaliser le PlaySpace.</span><span class="sxs-lookup"><span data-stu-id="82829-148">**GeneratePlayspace_RequestFinish**: Called to finalize the playspace.</span></span> <span data-ttu-id="82829-149">Cela utilisera les zones «peintes» pendant la phase d’analyse pour définir et verrouiller le PlaySpace.</span><span class="sxs-lookup"><span data-stu-id="82829-149">This will use the areas “painted” during the scan phase to define and lock the playspace.</span></span> <span data-ttu-id="82829-150">L’application peut interroger des statistiques pendant la phase d’analyse et interroger la maille personnalisée pour fournir des commentaires utilisateur.</span><span class="sxs-lookup"><span data-stu-id="82829-150">The application can query statistics during the scanning phase as well as query the custom mesh for providing user feedback.</span></span>
* <span data-ttu-id="82829-151">**Import_UnderstandingMesh**: Au cours de l’analyse, le comportement **SpatialUnderstandingCustomMesh** fourni par le module et placé sur la Prefab de fonctionnement interrogera périodiquement la maille personnalisée générée par le processus.</span><span class="sxs-lookup"><span data-stu-id="82829-151">**Import_UnderstandingMesh**: During scanning, the **SpatialUnderstandingCustomMesh** behavior provided by the module and placed on the understanding prefab will periodically query the custom mesh generated by the process.</span></span> <span data-ttu-id="82829-152">En outre, cette opération est effectuée une fois de plus après la finalisation de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="82829-152">In addition, this is done once more after scanning has been finalized.</span></span>

<span data-ttu-id="82829-153">Le workflow de numérisation, piloté par le comportement **SpatialUnderstanding** appelle **InitScan**, puis **UpdateScan** chaque frame.</span><span class="sxs-lookup"><span data-stu-id="82829-153">The scanning flow, driven by the **SpatialUnderstanding** behavior calls **InitScan**, then **UpdateScan** each frame.</span></span> <span data-ttu-id="82829-154">Lorsque la requête de statistiques signale une couverture raisonnable, l’utilisateur peut airtap d’appeler **RequestFinish** pour indiquer la fin de la phase d’analyse.</span><span class="sxs-lookup"><span data-stu-id="82829-154">When the statistics query reports reasonable coverage, the user can airtap to call **RequestFinish** to indicate the end of the scanning phase.</span></span> <span data-ttu-id="82829-155">**UpdateScan** continue à être appelé jusqu’à ce qu’il retourne la valeur indiquant que la dll a terminé le traitement.</span><span class="sxs-lookup"><span data-stu-id="82829-155">**UpdateScan** continues to be called until it’s return value indicates that the DLL has completed processing.</span></span>

## <a name="the-queries"></a><span data-ttu-id="82829-156">Les requêtes</span><span class="sxs-lookup"><span data-stu-id="82829-156">The queries</span></span>

<span data-ttu-id="82829-157">Une fois l’analyse terminée, vous pouvez accéder à trois types de requêtes différents dans l’interface:</span><span class="sxs-lookup"><span data-stu-id="82829-157">Once the scan is complete, you'll be able to access three different types of queries in the interface:</span></span>
* <span data-ttu-id="82829-158">**Requêtes de topologie**: Il s’agit de requêtes rapides basées sur la topologie de la salle analysée.</span><span class="sxs-lookup"><span data-stu-id="82829-158">**Topology queries**: These are fast queries that are based on the topology of the scanned room.</span></span>
* <span data-ttu-id="82829-159">**Requêtes de forme**: Celles-ci utilisent les résultats de vos requêtes de topologie pour rechercher des surfaces horizontales qui correspondent parfaitement aux formes personnalisées que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="82829-159">**Shape queries**: These utilize the results of your topology queries to find horizontal surfaces that are a good match to custom shapes that you define.</span></span>
* <span data-ttu-id="82829-160">**Requêtes de placement d’objets**: Il s’agit de requêtes plus complexes qui recherchent l’emplacement le mieux adapté en fonction d’un ensemble de règles et de contraintes pour l’objet.</span><span class="sxs-lookup"><span data-stu-id="82829-160">**Object placement queries**: These are more complex queries that find the best-fit location based on a set of rules and constraints for the object.</span></span>

<span data-ttu-id="82829-161">Outre les trois requêtes principales, il existe une interface Raycasting qui peut être utilisée pour récupérer des types de surfaces avec balises et un maillage de salle étanche personnalisé peut être copié.</span><span class="sxs-lookup"><span data-stu-id="82829-161">In addition to the three primary queries, there is a raycasting interface which can be used to retrieve tagged surface types and a custom watertight room mesh can be copied out.</span></span>

### <a name="topology-queries"></a><span data-ttu-id="82829-162">Requêtes de topologie</span><span class="sxs-lookup"><span data-stu-id="82829-162">Topology queries</span></span>

<span data-ttu-id="82829-163">Dans la DLL, le gestionnaire de topologie gère l’étiquetage de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="82829-163">Within the DLL, the topology manager handles labeling of the environment.</span></span> <span data-ttu-id="82829-164">Comme indiqué ci-dessus, la plupart des données sont stockées dans surfels, qui sont contenues dans un volume voxel.</span><span class="sxs-lookup"><span data-stu-id="82829-164">As mentioned above, much of the data is stored within surfels, which are contained within a voxel volume.</span></span> <span data-ttu-id="82829-165">En outre, la structure **PlaySpaceInfos** est utilisée pour stocker des informations sur le PlaySpace, y compris l’alignement universel (plus de détails à ce niveau ci-dessous), le plancher et la hauteur du plafond.</span><span class="sxs-lookup"><span data-stu-id="82829-165">In addition, the **PlaySpaceInfos** structure is used to store information about the playspace, including the world alignment (more details on this below), floor, and ceiling height.</span></span>

<span data-ttu-id="82829-166">Les heuristiques sont utilisées pour déterminer l’étage, le plafond et les murs.</span><span class="sxs-lookup"><span data-stu-id="82829-166">Heuristics are used for determining floor, ceiling, and walls.</span></span> <span data-ttu-id="82829-167">Par exemple, la surface horizontale la plus grande et la plus basse avec une surface d’exposition supérieure à 1 m2 est considérée comme le plancher.</span><span class="sxs-lookup"><span data-stu-id="82829-167">For example, the largest and lowest horizontal surface with greater than 1 m2 surface area is considered the floor.</span></span> <span data-ttu-id="82829-168">Notez que le chemin d’accès de l’appareil photo pendant le processus d’analyse est également utilisé dans ce processus.</span><span class="sxs-lookup"><span data-stu-id="82829-168">Note that the camera path during the scanning process is also used in this process.</span></span>

<span data-ttu-id="82829-169">Un sous-ensemble des requêtes exposées par le gestionnaire de topologie est exposé via la DLL.</span><span class="sxs-lookup"><span data-stu-id="82829-169">A subset of the queries exposed by the Topology manager are exposed out through the DLL.</span></span> <span data-ttu-id="82829-170">Les requêtes de topologie exposées sont les suivantes:</span><span class="sxs-lookup"><span data-stu-id="82829-170">The exposed topology queries are as follows:</span></span>
* <span data-ttu-id="82829-171">QueryTopology_FindPositionsOnWalls</span><span class="sxs-lookup"><span data-stu-id="82829-171">QueryTopology_FindPositionsOnWalls</span></span>
* <span data-ttu-id="82829-172">QueryTopology_FindLargePositionsOnWalls</span><span class="sxs-lookup"><span data-stu-id="82829-172">QueryTopology_FindLargePositionsOnWalls</span></span>
* <span data-ttu-id="82829-173">QueryTopology_FindLargestWall</span><span class="sxs-lookup"><span data-stu-id="82829-173">QueryTopology_FindLargestWall</span></span>
* <span data-ttu-id="82829-174">QueryTopology_FindPositionsOnFloor</span><span class="sxs-lookup"><span data-stu-id="82829-174">QueryTopology_FindPositionsOnFloor</span></span>
* <span data-ttu-id="82829-175">QueryTopology_FindLargestPositionsOnFloor</span><span class="sxs-lookup"><span data-stu-id="82829-175">QueryTopology_FindLargestPositionsOnFloor</span></span>
* <span data-ttu-id="82829-176">QueryTopology_FindPositionsSittable</span><span class="sxs-lookup"><span data-stu-id="82829-176">QueryTopology_FindPositionsSittable</span></span>

<span data-ttu-id="82829-177">Chacune des requêtes a un ensemble de paramètres, spécifique au type de requête.</span><span class="sxs-lookup"><span data-stu-id="82829-177">Each of the queries has a set of parameters, specific to the query type.</span></span> <span data-ttu-id="82829-178">Dans l’exemple suivant, l’utilisateur spécifie la hauteur minimale & largeur du volume souhaité, la hauteur minimale de placement au-dessus du plancher et la quantité minimale d’autorisation devant le volume.</span><span class="sxs-lookup"><span data-stu-id="82829-178">In the following example, the user specifies the minimum height & width of the desired volume, minimum placement height above the floor, and the minimum amount of clearance in front of the volume.</span></span> <span data-ttu-id="82829-179">Toutes les mesures sont en mètres.</span><span class="sxs-lookup"><span data-stu-id="82829-179">All measurements are in meters.</span></span>




```
EXTERN_C __declspec(dllexport) int QueryTopology_FindPositionsOnWalls(
          _In_ float minHeightOfWallSpace,
          _In_ float minWidthOfWallSpace,
          _In_ float minHeightAboveFloor,
          _In_ float minFacingClearance,
          _In_ int locationCount,
          _Inout_ Dll_Interface::TopologyResult* locationData)
```

<span data-ttu-id="82829-180">Chacune de ces requêtes utilise un tableau pré-alloué de structures **TopologyResult** .</span><span class="sxs-lookup"><span data-stu-id="82829-180">Each of these queries takes a pre-allocated array of **TopologyResult** structures.</span></span> <span data-ttu-id="82829-181">Le paramètre **locationCount** spécifie la longueur du tableau transmis.</span><span class="sxs-lookup"><span data-stu-id="82829-181">The **locationCount** parameter specifies the length of the passed-in array.</span></span> <span data-ttu-id="82829-182">La valeur de retour indique le nombre d’emplacements retournés.</span><span class="sxs-lookup"><span data-stu-id="82829-182">The return value reports the number of returned locations.</span></span> <span data-ttu-id="82829-183">Ce nombre n’est jamais supérieur au paramètre **locationCount** passé.</span><span class="sxs-lookup"><span data-stu-id="82829-183">This number is never greater than the passed-in **locationCount** parameter.</span></span>

<span data-ttu-id="82829-184">Le **TopologyResult** contient la position centrale du volume retourné, le sens de face (c’est-à-dire normal) et les dimensions de l’espace trouvé.</span><span class="sxs-lookup"><span data-stu-id="82829-184">The **TopologyResult** contains the center position of the returned volume, the facing direction (i.e. normal), and the dimensions of the found space.</span></span>




```
struct TopologyResult
     {
          DirectX::XMFLOAT3 position;
          DirectX::XMFLOAT3 normal;
          float width;
          float length;
     };
```

<span data-ttu-id="82829-185">Notez que dans l’exemple Unity, chacune de ces requêtes est liée à un bouton dans le panneau de l’interface utilisateur virtuelle.</span><span class="sxs-lookup"><span data-stu-id="82829-185">Note that in the Unity sample, each of these queries is linked up to a button in the virtual UI panel.</span></span> <span data-ttu-id="82829-186">L’exemple code en dur les paramètres de chacune de ces requêtes à des valeurs raisonnables.</span><span class="sxs-lookup"><span data-stu-id="82829-186">The sample hard codes the parameters for each of these queries to reasonable values.</span></span> <span data-ttu-id="82829-187">Pour plus d’exemples, consultez *SpaceVisualizer.cs* dans l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="82829-187">See *SpaceVisualizer.cs* in the sample code for more examples.</span></span>

### <a name="shape-queries"></a><span data-ttu-id="82829-188">Requêtes de forme</span><span class="sxs-lookup"><span data-stu-id="82829-188">Shape queries</span></span>

<span data-ttu-id="82829-189">À l’intérieur de la DLL, l’analyseur de forme (**ShapeAnalyzer_W**) utilise l’analyseur de topologie pour faire correspondre les formes personnalisées définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="82829-189">Inside of the DLL, the shape analyzer (**ShapeAnalyzer_W**) uses the topology analyzer to match against custom shapes defined by the user.</span></span> <span data-ttu-id="82829-190">L’exemple Unity a un ensemble prédéfini de formes qui s’affichent dans le menu requête, sous l’onglet forme.</span><span class="sxs-lookup"><span data-stu-id="82829-190">The Unity sample has a pre-defined set of shapes which are shown in the query menu, on the shape tab.</span></span>

<span data-ttu-id="82829-191">Notez que l’analyse des formes fonctionne uniquement sur des surfaces horizontales.</span><span class="sxs-lookup"><span data-stu-id="82829-191">Note that the shape analysis works on horizontal surfaces only.</span></span> <span data-ttu-id="82829-192">Un canapé, par exemple, est défini par la surface du siège plat et le haut à l’arrière de la canapé.</span><span class="sxs-lookup"><span data-stu-id="82829-192">A couch, for example, is defined by the flat seat surface and the flat top of the couch back.</span></span> <span data-ttu-id="82829-193">La requête Shape recherche deux surfaces d’une taille, d’une hauteur et d’une plage d’aspect spécifiques, les deux surfaces étant alignées et connectées.</span><span class="sxs-lookup"><span data-stu-id="82829-193">The shape query looks for two surfaces of a specific size, height, and aspect range, with the two surfaces aligned and connected.</span></span> <span data-ttu-id="82829-194">À l’aide de la terminologie des API, le siège de la canapé et le haut de l’arrière du canapé sont des composants de forme et les exigences d’alignement sont des contraintes de composant de forme.</span><span class="sxs-lookup"><span data-stu-id="82829-194">Using the APIs terminology, the couch seat and the top of the back of the couch are shape components and the alignment requirements are shape component constraints.</span></span>

<span data-ttu-id="82829-195">Voici un exemple de requête défini dans l’exemple Unity (**ShapeDefinition.cs**) pour les objets «sittable»:</span><span class="sxs-lookup"><span data-stu-id="82829-195">An example query defined in the Unity sample (**ShapeDefinition.cs**), for “sittable” objects is as follows:</span></span>




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

<span data-ttu-id="82829-196">Chaque requête de forme est définie par un ensemble de composants de forme, chacun avec un ensemble de contraintes de composant et un ensemble de contraintes de forme qui répertorie les dépendances entre les composants.</span><span class="sxs-lookup"><span data-stu-id="82829-196">Each shape query is defined by a set of shape components, each with a set of component constraints and a set of shape constraints which lists dependencies between the components.</span></span> <span data-ttu-id="82829-197">Cet exemple inclut trois contraintes dans une définition de composant unique et aucune contrainte de forme entre les composants (étant donné qu’il n’y a qu’un seul composant).</span><span class="sxs-lookup"><span data-stu-id="82829-197">This example includes three constraints in a single component definition and no shape constraints between components (as there is only one component).</span></span>

<span data-ttu-id="82829-198">En revanche, la forme de canapé a deux composants de forme et quatre contraintes de forme.</span><span class="sxs-lookup"><span data-stu-id="82829-198">In contrast, the couch shape has two shape components and four shape constraints.</span></span> <span data-ttu-id="82829-199">Notez que les composants sont identifiés par leur index dans la liste des composants de l’utilisateur (0 et 1 dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="82829-199">Note that components are identified by their index in the user’s component list (0 and 1 in this example).</span></span>




```
shapeConstraints = new List<ShapeConstraint>()
        {
              ShapeConstraint.Create_RectanglesSameLength(0, 1, 0.6f),
              ShapeConstraint.Create_RectanglesParallel(0, 1),
              ShapeConstraint.Create_RectanglesAligned(0, 1, 0.3f),
              ShapeConstraint.Create_AtBackOf(1, 0),
        };
```

<span data-ttu-id="82829-200">Les fonctions wrapper sont fournies dans le module Unity pour faciliter la création de définitions de formes personnalisées.</span><span class="sxs-lookup"><span data-stu-id="82829-200">Wrapper functions are provided in the Unity module for easy creation of custom shape definitions.</span></span> <span data-ttu-id="82829-201">La liste complète des contraintes de composant et de forme se trouve dans **SpatialUnderstandingDll.cs** dans les structures **ShapeComponentConstraint** et **ShapeConstraint** .</span><span class="sxs-lookup"><span data-stu-id="82829-201">The full list of component and shape constraints can be found in **SpatialUnderstandingDll.cs** within the **ShapeComponentConstraint** and the **ShapeConstraint** structures.</span></span>

![Le rectangle bleu met en surbrillance les résultats de la requête de forme de chaise.](images/chair-shape-query-500px.png)

<span data-ttu-id="82829-203">Le rectangle bleu met en surbrillance les résultats de la requête de forme de chaise.</span><span class="sxs-lookup"><span data-stu-id="82829-203">The blue rectangle highlights the results of the chair shape query.</span></span>



### <a name="object-placement-solver"></a><span data-ttu-id="82829-204">Solveur de positionnement des objets</span><span class="sxs-lookup"><span data-stu-id="82829-204">Object placement solver</span></span>

<span data-ttu-id="82829-205">Les requêtes de placement d’objet peuvent être utilisées pour identifier les emplacements idéaux dans la salle physique pour placer vos objets.</span><span class="sxs-lookup"><span data-stu-id="82829-205">Object placement queries can be used to identify ideal locations in the physical room to place your objects.</span></span> <span data-ttu-id="82829-206">Le solveur trouvera l’emplacement le mieux adapté en fonction des contraintes et règles d’objet.</span><span class="sxs-lookup"><span data-stu-id="82829-206">The solver will find the best-fit location given the object rules and constraints.</span></span> <span data-ttu-id="82829-207">En outre, les requêtes d’objet sont conservées jusqu’à ce que l’objet soit supprimé avec des appels **Solver_RemoveObject** ou **Solver_RemoveAllObjects** , ce qui permet le placement de plusieurs objets avec restriction.</span><span class="sxs-lookup"><span data-stu-id="82829-207">In addition, object queries persist until the object is removed with **Solver_RemoveObject** or **Solver_RemoveAllObjects** calls, allowing constrained multi-object placement.</span></span>

<span data-ttu-id="82829-208">Les requêtes de placement d’objet se composent de trois parties: le type de placement avec des paramètres, une liste de règles et une liste de contraintes.</span><span class="sxs-lookup"><span data-stu-id="82829-208">Object placement queries consist of three parts: placement type with parameters, a list of rules, and a list of constraints.</span></span> <span data-ttu-id="82829-209">Pour exécuter une requête, utilisez l’API suivante:</span><span class="sxs-lookup"><span data-stu-id="82829-209">To run a query, use the following API:</span></span>




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
<span data-ttu-id="82829-210">Cette fonction accepte un nom d’objet, une définition de placement et une liste de règles et de contraintes.</span><span class="sxs-lookup"><span data-stu-id="82829-210">This function takes an object name, placement definition, and a list of rules and constraints.</span></span> <span data-ttu-id="82829-211">Les C# wrappers fournissent des fonctions d’assistance de construction pour faciliter la création de règles et de contraintes.</span><span class="sxs-lookup"><span data-stu-id="82829-211">The C# wrappers provide construction helper functions to make rule and constraint construction easy.</span></span> <span data-ttu-id="82829-212">La définition de placement contient le type de requête, à savoir l’un des éléments suivants:</span><span class="sxs-lookup"><span data-stu-id="82829-212">The placement definition contains the query type — that is, one of the following:</span></span>




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

<span data-ttu-id="82829-213">Chacun des types de placement a un ensemble de paramètres propre au type.</span><span class="sxs-lookup"><span data-stu-id="82829-213">Each of the placement types has a set of parameters unique to the type.</span></span> <span data-ttu-id="82829-214">La structure **ObjectPlacementDefinition** contient un jeu de fonctions d’assistance statiques pour la création de ces définitions.</span><span class="sxs-lookup"><span data-stu-id="82829-214">The **ObjectPlacementDefinition** structure contains a set of static helper functions for creating these definitions.</span></span> <span data-ttu-id="82829-215">Par exemple, pour trouver un endroit où placer un objet sur l’étage, vous pouvez utiliser la fonction suivante:</span><span class="sxs-lookup"><span data-stu-id="82829-215">For example, to find a place to put an object on the floor, you can use the following function:</span></span> 


```
public static ObjectPlacementDefinition Create_OnFloor(Vector3 halfDims)
```

<span data-ttu-id="82829-216">Outre le type de placement, vous pouvez fournir un ensemble de règles et de contraintes.</span><span class="sxs-lookup"><span data-stu-id="82829-216">In addition to the placement type, you can provide a set of rules and constraints.</span></span> <span data-ttu-id="82829-217">Les règles ne peuvent pas être violées.</span><span class="sxs-lookup"><span data-stu-id="82829-217">Rules cannot be violated.</span></span> <span data-ttu-id="82829-218">Les emplacements d’emplacement possibles qui satisfont au type et aux règles sont ensuite optimisés par rapport au jeu de contraintes pour sélectionner l’emplacement de positionnement optimal.</span><span class="sxs-lookup"><span data-stu-id="82829-218">Possible placement locations that satisfy the type and rules are then optimized against the set of constraints to select the optimal placement location.</span></span> <span data-ttu-id="82829-219">Chacune des règles et contraintes peut être créée par les fonctions de création statique fournies.</span><span class="sxs-lookup"><span data-stu-id="82829-219">Each of the rules and constraints can be created by the provided static creation functions.</span></span> <span data-ttu-id="82829-220">Vous trouverez ci-dessous un exemple de fonction de construction de règle et de contrainte.</span><span class="sxs-lookup"><span data-stu-id="82829-220">An example rule and constraint construction function is provided below.</span></span>




```
public static ObjectPlacementRule Create_AwayFromPosition(
                    Vector3 position, float minDistance)
               public static ObjectPlacementConstraint Create_NearPoint(
                    Vector3 position, float minDistance = 0.0f, float maxDistance = 0.0f)
```

<span data-ttu-id="82829-221">La requête de placement d’objet ci-dessous recherche un endroit où placer un cube demi-mètre sur le bord d’une surface, à l’écart des autres objets placés précédemment et près du centre de la pièce.</span><span class="sxs-lookup"><span data-stu-id="82829-221">The object placement query below is looking for a place to put a half meter cube on the edge of a surface, away from other previously place objects and near the center of the room.</span></span>




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

<span data-ttu-id="82829-222">En cas de réussite, une structure **ObjectPlacementResult** contenant la position, les dimensions et l’orientation de placement est retournée.</span><span class="sxs-lookup"><span data-stu-id="82829-222">If successful, an **ObjectPlacementResult** structure containing the placement position, dimensions and orientation is returned.</span></span> <span data-ttu-id="82829-223">En outre, le placement est ajouté à la liste interne des objets placés de la DLL.</span><span class="sxs-lookup"><span data-stu-id="82829-223">In addition, the placement is added to the DLL’s internal list of placed objects.</span></span> <span data-ttu-id="82829-224">Les requêtes d’emplacement suivantes prennent en compte cet objet.</span><span class="sxs-lookup"><span data-stu-id="82829-224">Subsequent placement queries will take this object into account.</span></span> <span data-ttu-id="82829-225">Le fichier **LevelSolver.cs** dans l’exemple Unity contient plus d’exemples de requêtes.</span><span class="sxs-lookup"><span data-stu-id="82829-225">The **LevelSolver.cs** file in the Unity sample contains more example queries.</span></span>

![Les zones bleues affichent le résultat de trois emplacements sur les requêtes d’étage avec les règles «éloigner de la position de la caméra».](images/away-from-camera-position-500px.png)

<span data-ttu-id="82829-227">Les zones bleues affichent le résultat de trois emplacements sur les requêtes d’étage avec les règles «éloigner de la position de la caméra».</span><span class="sxs-lookup"><span data-stu-id="82829-227">The blue boxes show the result from three Place On Floor queries with "away from camera position" rules.</span></span>


<span data-ttu-id="82829-228">**Conseil**</span><span class="sxs-lookup"><span data-stu-id="82829-228">**Tips:**</span></span>
* <span data-ttu-id="82829-229">Lors de la résolution de l’emplacement de positionnement de plusieurs objets requis pour un scénario de niveau ou d’application, résolvez tout d’abord les objets indispensables et volumineux pour maximiser la probabilité qu’un espace soit trouvé.</span><span class="sxs-lookup"><span data-stu-id="82829-229">When solving for placement location of multiple objects required for a level or application scenario, first solve indispensable and large objects to maximize the probability that a space can be found.</span></span>
* <span data-ttu-id="82829-230">L’ordre de placement est important.</span><span class="sxs-lookup"><span data-stu-id="82829-230">Placement order is important.</span></span> <span data-ttu-id="82829-231">Si vous ne trouvez pas de placement d’objet, essayez des configurations moins restreintes.</span><span class="sxs-lookup"><span data-stu-id="82829-231">If object placements cannot be found, try less constrained configurations.</span></span> <span data-ttu-id="82829-232">Avoir un ensemble de configurations de secours est essentiel à la prise en charge des fonctionnalités dans de nombreuses configurations de salles.</span><span class="sxs-lookup"><span data-stu-id="82829-232">Having a set of fallback configurations is critical to supporting functionality across many room configurations.</span></span>

### <a name="ray-casting"></a><span data-ttu-id="82829-233">Conversion de rayon</span><span class="sxs-lookup"><span data-stu-id="82829-233">Ray casting</span></span>

<span data-ttu-id="82829-234">En plus des trois requêtes principales, une interface de type Ray peut être utilisée pour récupérer des types de surfaces avec balises et un maillage PlaySpace étanche personnalisé peut être copié après la numérisation et la finalisation de la salle, et les étiquettes sont générées en interne pour les surfaces comme plancher, plafond et murs.</span><span class="sxs-lookup"><span data-stu-id="82829-234">In addition to the three primary queries, a ray casting interface can be used to retrieve tagged surface types and a custom watertight playspace mesh can be copied out After the room has been scanned and finalized, labels are internally generated for surfaces like the floor, ceiling, and walls.</span></span> <span data-ttu-id="82829-235">La fonction **PlayspaceRaycast** prend un rayon et retourne si le rayon entre en conflit avec une surface connue et, le cas échéant, des informations sur cette surface sous la forme d’un **RaycastResult**.</span><span class="sxs-lookup"><span data-stu-id="82829-235">The **PlayspaceRaycast** function takes a ray and returns if the ray collides with a known surface and if so, information about that surface in the form of a **RaycastResult**.</span></span> 


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

<span data-ttu-id="82829-236">En interne, raycast est calculé par rapport à la représentation voxel 8cm cube calculée du PlaySpace.</span><span class="sxs-lookup"><span data-stu-id="82829-236">Internally, the raycast is computed against the computed 8cm cubed voxel representation of the playspace.</span></span> <span data-ttu-id="82829-237">Chaque voxel contient un ensemble d’éléments surface avec des données de topologie traitées (également appelées surfels).</span><span class="sxs-lookup"><span data-stu-id="82829-237">Each voxel contains a set of surface elements with processed topology data (also known as surfels).</span></span> <span data-ttu-id="82829-238">Le surfels contenu dans la cellule voxel intersectée est comparé et la meilleure correspondance est utilisée pour rechercher les informations de topologie.</span><span class="sxs-lookup"><span data-stu-id="82829-238">The surfels contained within the intersected voxel cell are compared and the best match used to look up the topology information.</span></span> <span data-ttu-id="82829-239">Ces données de topologie contiennent l’étiquetage renvoyé sous la forme de l’énumération **SurfaceTypes** , ainsi que la surface d’exposition de la surface intersectée.</span><span class="sxs-lookup"><span data-stu-id="82829-239">This topology data contains the labeling returned in the form of the **SurfaceTypes** enum, as well as the surface area of the intersected surface.</span></span>

<span data-ttu-id="82829-240">Dans l’exemple Unity, le curseur convertit chaque image de rayon.</span><span class="sxs-lookup"><span data-stu-id="82829-240">In the Unity sample, the cursor casts a ray each frame.</span></span> <span data-ttu-id="82829-241">Tout d’abord, contre les conflits avec Unity; Deuxièmement, par rapport à la représentation mondiale du module de présentation; Enfin, sur les éléments d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="82829-241">First, against Unity’s colliders; second, against the understanding module’s world representation; and finally, against the UI elements.</span></span> <span data-ttu-id="82829-242">Dans cette application, l’interface utilisateur est prioritaire, puis le résultat de la compréhension et enfin, les conflits avec Unity.</span><span class="sxs-lookup"><span data-stu-id="82829-242">In this application, UI gets priority, then the understanding result, and finally, Unity’s colliders.</span></span> <span data-ttu-id="82829-243">Le **SurfaceType** est signalé en tant que texte en regard du curseur.</span><span class="sxs-lookup"><span data-stu-id="82829-243">The **SurfaceType** is reported as text next to the cursor.</span></span>

![Raycast intersection de rapports de résultats avec le plancher.](images/raycast-result-500px.jpg)

<span data-ttu-id="82829-245">Raycast intersection de rapports de résultats avec le plancher.</span><span class="sxs-lookup"><span data-stu-id="82829-245">Raycast result reporting intersection with the floor.</span></span>


## <a name="get-the-code"></a><span data-ttu-id="82829-246">Obtenir le code</span><span class="sxs-lookup"><span data-stu-id="82829-246">Get the code</span></span>

<span data-ttu-id="82829-247">Le code open source est disponible dans [MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity).</span><span class="sxs-lookup"><span data-stu-id="82829-247">The open-source code is available in [MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity).</span></span> <span data-ttu-id="82829-248">Faites-le nous savoir sur les [forums de développement HoloLens](https://forums.hololens.com/) si vous utilisez le code dans un projet.</span><span class="sxs-lookup"><span data-stu-id="82829-248">Let us know on the [HoloLens Developer Forums](https://forums.hololens.com/) if you use the code in a project.</span></span> <span data-ttu-id="82829-249">Nous ne pouvons pas attendre pour voir ce que vous faites avec!</span><span class="sxs-lookup"><span data-stu-id="82829-249">We can't wait to see what you do with it!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="82829-250">À propos de l’auteur</span><span class="sxs-lookup"><span data-stu-id="82829-250">About the author</span></span>

<table style="border:0;width:800px">
<tr>
<td style="border:0"> <img alt="Jeff Evertt, Software Engineering Lead at Microsoft" width="200" height="205" src="images/jeff-evertt-200px.jpg" /></td><td style="border:0"> <span data-ttu-id="82829-251"><b>Jeff Evertt</b> est responsable de l’ingénierie logicielle qui a travaillé sur HoloLens depuis les premiers jours, depuis l’incubation jusqu’au développement de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="82829-251"><b>Jeff Evertt</b> is a software engineering lead who has worked on HoloLens since the early days, from incubation to experience development.</span></span> <span data-ttu-id="82829-252">Avant HoloLens, il travaillait sur la Xbox Kinect et dans le secteur des jeux sur un large éventail de plates-formes et de jeux.</span><span class="sxs-lookup"><span data-stu-id="82829-252">Before HoloLens, he worked on the Xbox Kinect and in the games industry on a wide variety of platforms and games.</span></span> <span data-ttu-id="82829-253">Jeff est passionné par la robotique, les graphiques et les choses avec des lumières éclairées.</span><span class="sxs-lookup"><span data-stu-id="82829-253">Jeff is passionate about robotics, graphics, and things with flashy lights that go beep.</span></span> <span data-ttu-id="82829-254">Il aime découvrir de nouveaux éléments et travailler sur des logiciels, du matériel, et en particulier dans l’espace où les deux se croisent.</span><span class="sxs-lookup"><span data-stu-id="82829-254">He enjoys learning new things and working on software, hardware, and particularly in the space where the two intersect.</span></span></td>
</tr>
</table>



## <a name="see-also"></a><span data-ttu-id="82829-255">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="82829-255">See also</span></span>
* [<span data-ttu-id="82829-256">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="82829-256">Spatial mapping</span></span>](spatial-mapping.md)
* [<span data-ttu-id="82829-257">Conception du mappage spatial</span><span class="sxs-lookup"><span data-stu-id="82829-257">Spatial mapping design</span></span>](spatial-mapping-design.md)
* [<span data-ttu-id="82829-258">Visualisation du balayage d’une pièce</span><span class="sxs-lookup"><span data-stu-id="82829-258">Room scan visualization</span></span>](room-scan-visualization.md)
* [<span data-ttu-id="82829-259">MixedRealityToolkit-Unity</span><span class="sxs-lookup"><span data-stu-id="82829-259">MixedRealityToolkit-Unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity)
* [<span data-ttu-id="82829-260">Asobo Studio: Leçons de la Frontline du développement HoloLens</span><span class="sxs-lookup"><span data-stu-id="82829-260">Asobo Studio: Lessons from the frontline of HoloLens development</span></span>](http://www.gamesindustry.biz/articles/2016-05-12-asobo-lessons-from-the-frontline-of-ar-development)
