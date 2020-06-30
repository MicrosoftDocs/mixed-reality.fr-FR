---
title: Mappage spatial dans Unreal
description: Guide d’utilisation du mappage spatial dans Unreal
author: hferrone
ms.author: v-haferr
ms.date: 06/10/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, mappage spatial
ms.openlocfilehash: ffa57749cd96e240ac4812f950f4e13a6dbc68bd
ms.sourcegitcommit: 45da0a056fa42088ff81ccdd11232830fbe8430f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84720405"
---
# <a name="spatial-mapping-in-unreal"></a><span data-ttu-id="f54f4-104">Mappage spatial dans Unreal</span><span class="sxs-lookup"><span data-stu-id="f54f4-104">Spatial Mapping in Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="f54f4-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="f54f4-105">Overview</span></span>
<span data-ttu-id="f54f4-106">Le mappage spatial permet de placer des objets sur des surfaces du monde physique en montrant l’environnement autour d’HoloLens, ce qui fait paraître les hologrammes encore plus réels à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f54f4-106">Spatial mapping makes it possible to place objects on surfaces in the physical world by showing the world around the HoloLens, which makes holograms seem more real to the user.</span></span> <span data-ttu-id="f54f4-107">Le mappage spatial ancre également les objets dans le monde de l’utilisateur en tirant parti des indications de profondeur du monde réel. De cette façon, l’utilisateur a réellement l’impression que ces hologrammes se trouvent autour de lui. Les hologrammes qui flottent dans les airs ou qui se déplacent en même temps que l’utilisateur ne sembleront pas aussi réels.</span><span class="sxs-lookup"><span data-stu-id="f54f4-107">Spatial mapping also anchors objects in the user's world by taking advantage of real world depth cues. This helps convince the user that these holograms are actually in their space; holograms floating in space or moving with the user will not feel as real.</span></span> <span data-ttu-id="f54f4-108">Il est conseillé d’ajouter des éléments à des fins de confort dès que cela vous est possible.</span><span class="sxs-lookup"><span data-stu-id="f54f4-108">You want to place items for comfort whenever possible.</span></span>

<span data-ttu-id="f54f4-109">Vous trouverez plus d’informations sur la qualité du mappage spatial, le positionnement, l’occlusion, le rendu et plus encore, dans le document [Mappage spatial](spatial-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="f54f4-109">You can find more information on spatial mapping quality, placement, occlusion, rendering, and more, in the [Spatial mapping](spatial-mapping.md) document.</span></span>

## <a name="enabling-spatial-mapping"></a><span data-ttu-id="f54f4-110">Activation du mappage spatial</span><span class="sxs-lookup"><span data-stu-id="f54f4-110">Enabling Spatial Mapping</span></span>

<span data-ttu-id="f54f4-111">Pour activer le mappage spatial sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="f54f4-111">To enable spatial mapping on HoloLens:</span></span>
- <span data-ttu-id="f54f4-112">Ouvrez **Edit > Project Settings** , puis faites défiler jusqu’à la section **Platforms**.</span><span class="sxs-lookup"><span data-stu-id="f54f4-112">Open **Edit > Project Settings** and scroll down to the **Platforms** section.</span></span>    
    + <span data-ttu-id="f54f4-113">Sélectionnez **HoloLens**, puis cochez **Spatial Perception**.</span><span class="sxs-lookup"><span data-stu-id="f54f4-113">Select **HoloLens** and check **Spatial Perception**.</span></span>

<span data-ttu-id="f54f4-114">Pour choisir le mappage spatial et déboguer **MRMesh** dans un jeu HoloLens :</span><span class="sxs-lookup"><span data-stu-id="f54f4-114">To opt into spatial mapping and debug the **MRMesh** in a HoloLens game:</span></span>
1. <span data-ttu-id="f54f4-115">Ouvrez **ARSessionConfig**, puis développez la section **ARSettings > World Mapping**.</span><span class="sxs-lookup"><span data-stu-id="f54f4-115">Open the **ARSessionConfig** and expand the **ARSettings > World Mapping** section.</span></span> 

2. <span data-ttu-id="f54f4-116">Cochez **Generate Mesh Data from Tracked Geometry** (Générer les données de maillage à partir de la géométrie suivie), ce qui indique au plug-in HoloLens qu’il doit démarrer de manière asynchrone la récupération des données de mappage spatial et les afficher dans Unreal via **MRMesh**.</span><span class="sxs-lookup"><span data-stu-id="f54f4-116">Check **Generate Mesh Data from Tracked Geometry**, which tells the HoloLens plugin to start asynchronously getting spatial mapping data and surface it to Unreal through the **MRMesh**.</span></span> 
3. <span data-ttu-id="f54f4-117">Cochez **Render Mesh Data in Wireframe** (Afficher les données de maillage dans un contour filaire) pour afficher un contour filaire blanc autour de chaque triangle dans **MRMesh**.</span><span class="sxs-lookup"><span data-stu-id="f54f4-117">Check **Render Mesh Data in Wireframe** to show a white wireframe outline of every triangle in the **MRMesh**.</span></span> 

![Magasin d’ancres spatiales prêt](images/unreal-spatialmapping-arsettings.PNG)


## <a name="spatial-mapping-at-runtime"></a><span data-ttu-id="f54f4-119">Mappage spatial au moment de l’exécution</span><span class="sxs-lookup"><span data-stu-id="f54f4-119">Spatial Mapping at runtime</span></span>
<span data-ttu-id="f54f4-120">Vous pouvez modifier les paramètres suivants pour mettre à jour le comportement du runtime de mappage spatial :</span><span class="sxs-lookup"><span data-stu-id="f54f4-120">You can modify the following parameters to update the spatial mapping runtime behavior:</span></span>

- <span data-ttu-id="f54f4-121">Ouvrez **Edit > Project Settings**, faites défiler jusqu’à la section **Platforms**, puis sélectionnez **HoloLens > Spatial Mapping** :</span><span class="sxs-lookup"><span data-stu-id="f54f4-121">Open **Edit > Project Settings**, scroll down to the **Platforms** section and select **HoloLens > Spatial Mapping**:</span></span> 

![Paramètres projet des ancres spatiales](images/unreal-spatialmapping-projectsettings.PNG)

- <span data-ttu-id="f54f4-123">Le paramètre **Max Triangles Per Cubic Meter** (Nombre maximal de triangles par mètre cube) modifie la densité des triangles dans le maillage de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="f54f4-123">**Max Triangles Per Cubic Meter** updates the density of the triangles in the spatial mapping mesh.</span></span>  
- <span data-ttu-id="f54f4-124">Le paramètre **Spatial Meshing Volume Size** (Volume du maillage spatial) définit la taille du cube autour du joueur utilisé pour le rendu et la mise à jour des données de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="f54f4-124">**Spatial Meshing Volume Size** is the size of the cube around the player to render and update spatial mapping data.</span></span>  
    + <span data-ttu-id="f54f4-125">Si l’environnement d’exécution de l’application est supposé être grand, cette valeur devra être suffisamment grande pour s’adapter à l’espace réel.</span><span class="sxs-lookup"><span data-stu-id="f54f4-125">If the expected application runtime environment is expected to be large, this value may need to be large to match the real-world space.</span></span>  <span data-ttu-id="f54f4-126">À l’inverse, si l’application doit uniquement placer des hologrammes sur des surfaces proches de l’utilisateur, cette valeur pourra être plus petite.</span><span class="sxs-lookup"><span data-stu-id="f54f4-126">On the other hand, this value can be smaller if the application only needs to place holograms on surfaces immediately around the user.</span></span> <span data-ttu-id="f54f4-127">Le volume de mappage spatial bougera en même temps que l’utilisateur se déplacera dans le monde.</span><span class="sxs-lookup"><span data-stu-id="f54f4-127">As the user walks around the world, the spatial mapping volume will move with them.</span></span> 

## <a name="working-with-mrmesh"></a><span data-ttu-id="f54f4-128">Utilisation de MRMesh</span><span class="sxs-lookup"><span data-stu-id="f54f4-128">Working with MRMesh</span></span>
<span data-ttu-id="f54f4-129">Pour accéder à **MRMesh** au moment de l’exécution :</span><span class="sxs-lookup"><span data-stu-id="f54f4-129">To get access to the **MRMesh** at runtime:</span></span>
1. <span data-ttu-id="f54f4-130">Ajoutez un composant **ARTrackableNotify** à l’acteur Blueprint.</span><span class="sxs-lookup"><span data-stu-id="f54f4-130">Add an **ARTrackableNotify** Component to a Blueprint actor.</span></span> 

![Composant ARTrackableNotify pour les ancres spatiales](images/unreal-spatialmapping-artrackablenotify.PNG)

2. <span data-ttu-id="f54f4-132">Sélectionnez le composant **ARTrackableNotify**, puis développez la section **Events** (Événements) dans le panneau **Details**.</span><span class="sxs-lookup"><span data-stu-id="f54f4-132">Select the **ARTrackableNotify** component and expand the **Events** section in the **Details** panel.</span></span> 
    - <span data-ttu-id="f54f4-133">Cliquez sur le bouton **+** pour les événements que vous souhaitez superviser.</span><span class="sxs-lookup"><span data-stu-id="f54f4-133">Click the **+** button on the events you want to monitor.</span></span> 

![Événements d’ancres spatiales](images/unreal-spatialmapping-events.PNG)

<span data-ttu-id="f54f4-135">Dans ce cas, l’événement **On Add Tracked Geometry** (Lors de l’ajout d’une géométrie suivie) est supervisé. Celui-ci recherche les maillages valides de l’environnement qui correspondent aux données de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="f54f4-135">In this case, the **On Add Tracked Geometry** event is being monitored, which looks for valid world meshes matching to spatial mapping data.</span></span> <span data-ttu-id="f54f4-136">Vous trouverez la liste complète des événements dans l’API du composant [UARTrackableNotify](https://docs.unrealengine.com/API/Runtime/AugmentedReality/UARTrackableNotifyComponent/index.html).</span><span class="sxs-lookup"><span data-stu-id="f54f4-136">You can find the full list of events in the [UARTrackableNotify](https://docs.unrealengine.com/API/Runtime/AugmentedReality/UARTrackableNotifyComponent/index.html) component API.</span></span> 

<span data-ttu-id="f54f4-137">Vous pouvez changer le matériau du maillage dans le graphe d’événements Blueprint ou dans le code C++.</span><span class="sxs-lookup"><span data-stu-id="f54f4-137">You can change the mesh’s material in the Blueprint Event Graph or in C++.</span></span> <span data-ttu-id="f54f4-138">La capture d’écran ci-dessous montre la route du blueprint :</span><span class="sxs-lookup"><span data-stu-id="f54f4-138">The screenshot below shows the Blueprint route:</span></span> 

![Exemple d’ancres spatiales](images/unreal-spatialmapping-example.PNG)

<span data-ttu-id="f54f4-140">Dans le code C++, vous pouvez vous abonner au délégué `OnTrackableAdded` pour récupérer `ARTrackedGeometry` dès qu’il est disponible, comme indiqué dans le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f54f4-140">In C++, you can subscribe to the `OnTrackableAdded` delegate to get the `ARTrackedGeometry` as soon as it is available, shown in the code below.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f54f4-141">Le fichier build.cs du projet **DOIT INCLURE** **AugmentedReality** dans la liste **PublicDependencyModuleNames**.</span><span class="sxs-lookup"><span data-stu-id="f54f4-141">The project’s build.cs file **MUST** have **AugmentedReality** in the **PublicDependencyModuleNames** list.</span></span>
> - <span data-ttu-id="f54f4-142">Cela inclut **ARBlueprintLibrary.h** et **MRMeshComponent.h**, ce qui vous permet d’examiner le composant **MRMesh** de **UARTrackedGeometry**.</span><span class="sxs-lookup"><span data-stu-id="f54f4-142">This includes **ARBlueprintLibrary.h** and **MRMeshComponent.h**, which lets you inspect the **MRMesh** component of the **UARTrackedGeometry**.</span></span> 

![Exemple de code C++ pour les ancres spatiales](images/unreal-spatialmapping-examplecode.PNG)

<span data-ttu-id="f54f4-144">Le mappage spatial n’est pas le seul type de données qui est affiché à travers **ARTrackedGeometries**.</span><span class="sxs-lookup"><span data-stu-id="f54f4-144">Spatial mapping is not the only type of data that gets surfaced through **ARTrackedGeometries**.</span></span> <span data-ttu-id="f54f4-145">Vous pouvez vérifier que `EARObjectClassification` est `World`, ce qui signifie qu’il s’agit d’une géométrie de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="f54f4-145">You can check that the `EARObjectClassification` is `World`, which means this is spatial mapping geometry.</span></span> 

<span data-ttu-id="f54f4-146">Il existe des délégués similaires pour les événements de mise à jour et de suppression :</span><span class="sxs-lookup"><span data-stu-id="f54f4-146">There are similar delegates for updated and removed events:</span></span> 
- `AddOnTrackableUpdatedDelegate_Handle` 
- <span data-ttu-id="f54f4-147">`AddOnTrackableRemovedDelegate_Handle`.</span><span class="sxs-lookup"><span data-stu-id="f54f4-147">`AddOnTrackableRemovedDelegate_Handle`.</span></span> 

<span data-ttu-id="f54f4-148">Vous trouverez la liste complète des événements dans l’API [UARTrackedGeometry](https://docs.unrealengine.com/API/Runtime/AugmentedReality/UARTrackedGeometry/index.html).</span><span class="sxs-lookup"><span data-stu-id="f54f4-148">You can find the full list of events in the [UARTrackedGeometry](https://docs.unrealengine.com/API/Runtime/AugmentedReality/UARTrackedGeometry/index.html) API.</span></span>

## <a name="see-also"></a><span data-ttu-id="f54f4-149">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f54f4-149">See also</span></span>
* [<span data-ttu-id="f54f4-150">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="f54f4-150">Spatial mapping</span></span>](spatial-mapping.md)
