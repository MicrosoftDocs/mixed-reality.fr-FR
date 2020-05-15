---
title: Mappage spatial dans Unreal
description: Guide d’utilisation du mappage spatial dans Unreal
author: sw5813
ms.author: jacksonf
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, mappage spatial
ms.openlocfilehash: 32f8247010745b23bf73c5161c378bc1284169ef
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82840078"
---
# <a name="spatial-mapping-in-unreal"></a><span data-ttu-id="b3ae3-104">Mappage spatial dans Unreal</span><span class="sxs-lookup"><span data-stu-id="b3ae3-104">Spatial Mapping in Unreal</span></span>

<span data-ttu-id="b3ae3-105">Pour activer le mappage spatial sur HoloLens, vérifiez que la fonctionnalité « Spatial Perception » est cochée dans l’éditeur Unreal sous Project Settings > Platform > HoloLens > Capabilities.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-105">To enable spatial mapping on HoloLens, ensure that the “Spatial Perception” capability is checked in the Unreal editor under Project Settings > Platform > HoloLens > Capabilities.</span></span>  

<span data-ttu-id="b3ae3-106">Pour activer l’utilisation du mappage spatial dans un jeu HoloLens, activez « Generate Mesh Data from Tracked Geometry » dans ARSessionConfig.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-106">To opt into using spatial mapping in a HoloLens game, enable the “Generate Mesh Data from Tracked Geometry” in the ARSessionConfig.</span></span>  <span data-ttu-id="b3ae3-107">Le plug-in HoloLens pourra alors obtenir de manière asynchrone les données de mappage spatial et les exposer à Unreal par le biais du composant MRMesh.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-107">The HoloLens plugin will then asynchronously get spatial mapping data and surface it to Unreal through the MRMesh.</span></span> 

![Magasin d’ancres spatiales prêt](images/unreal-spatialmapping-arsettings.PNG)

<span data-ttu-id="b3ae3-109">Pour avoir une visualisation de débogage du maillage de mappage spatial, cochez « Render Mesh Data in Wireframe » dans ARSessionConfig. Vous verrez ainsi une maquette (ou wireframe) blanche autour de chaque triangle dans le composant MRMesh.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-109">To see a debug visualization of the spatial mapping mesh, enable the “Render Mesh Data in Wireframe” checkbox in the ARSessionConfig to see a white wireframe outline of every triangle in the MRMesh.</span></span> 

<span data-ttu-id="b3ae3-110">Dans Project Settings > Platform > HoloLens > Spatial Mapping, les paramètres suivants peuvent être modifiés pour changer le comportement d’exécution du mappage spatial :</span><span class="sxs-lookup"><span data-stu-id="b3ae3-110">In Project Settings > Platform > HoloLens > Spatial Mapping, the following parameters can be modified to update spatial mapping’s runtime behavior:</span></span> 

![Paramètres projet des ancres spatiales](images/unreal-spatialmapping-projectsettings.PNG)

<span data-ttu-id="b3ae3-112">Le paramètre « Max Triangles Per Cubic Meter » modifie la densité des triangles dans le maillage de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-112">Max Triangles Per Cubic Meter will update the density of the triangles in the spatial mapping mesh.</span></span>  <span data-ttu-id="b3ae3-113">Le paramètre « Spatial Meshing Volume Size » définit la taille du cube autour du joueur utilisé pour le rendu et la mise à jour des données de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-113">Spatial Meshing Volume Size indicates the size of the cube around the player to render and update spatial mapping data.</span></span>  <span data-ttu-id="b3ae3-114">Si l’environnement d’exécution de l’application est supposé être grand, cette zone devra être suffisamment grande pour s’adapter à l’espace réel.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-114">If the expected application runtime environment is expected to be large, this field may need to be large to match the real-world space.</span></span>  <span data-ttu-id="b3ae3-115">À l’inverse, si l’application doit uniquement placer des hologrammes sur des surfaces proches de l’utilisateur, cette zone pourra être plus petite.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-115">Conversely, if the application only needs to place holograms on surfaces immediately around the user, this field can be smaller.</span></span>  <span data-ttu-id="b3ae3-116">Le volume de mappage spatial bougera en même temps que l’utilisateur se déplacera dans le monde.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-116">As the user walks around the world, the spatial mapping volume will move with them.</span></span> 

<span data-ttu-id="b3ae3-117">Pour pouvoir accéder au composant MRMesh pendant l’exécution, ajoutez d’abord un composant ARTrackableNotify à un acteur Blueprint :</span><span class="sxs-lookup"><span data-stu-id="b3ae3-117">To get access to the MRMesh at runtime, first add an AR Trackable Notify Component to a Blueprint actor:</span></span> 

![Composant ARTrackableNotify pour les ancres spatiales](images/unreal-spatialmapping-artrackablenotify.PNG)

<span data-ttu-id="b3ae3-119">Ensuite, accédez aux détails du composant et cliquez sur le bouton « + » vert dans les événements à surveiller.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-119">Then go to the component’s details and click on the green “+” button on the events to monitor.</span></span> 

![Événements d’ancres spatiales](images/unreal-spatialmapping-events.PNG)

<span data-ttu-id="b3ae3-121">Ici, nous surveillons l’événement On Add Tracked Geometry pour rechercher des maillages universels valides qui correspondent aux données de mappage spatial, puis nous changeons le matériau du maillage :</span><span class="sxs-lookup"><span data-stu-id="b3ae3-121">In this case we monitor the On Add Tracked Geometry event looking for valid world meshes which correspond to spatial mapping data, and change the mesh’s material:</span></span> 

![Exemple d’ancres spatiales](images/unreal-spatialmapping-example.PNG)

<span data-ttu-id="b3ae3-123">Dans C++, nous pouvons nous abonner au délégué OnTrackableAdded pour obtenir ARTrackedGeometry dès qu’il est disponible.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-123">In C++, we can subscribe to the OnTrackableAdded delegate to get the ARTrackedGeometry as soon as it is available.</span></span>  <span data-ttu-id="b3ae3-124">Il existe des délégués similaires pour les événements de mise à jour et de suppression : AddOnTrackableUpdatedDelegate_Handle et AddOnTrackableRemovedDelegate_Handle.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-124">There are similar delegates for updated and removed events: AddOnTrackableUpdatedDelegate_Handle and AddOnTrackableRemovedDelegate_Handle.</span></span> 

![Exemple de code C++ pour les ancres spatiales](images/unreal-spatialmapping-examplecode.PNG)

<span data-ttu-id="b3ae3-126">Dans le fichier build.cs du projet, « AugmentedReality » doit figurer dans la liste PublicDependencyModuleNames pour inclure « ARBlueprintLibrary.h » et « MRMesh » afin d’inspecter le composant MRMesh du UARTrackedGeometry.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-126">The project’s build.cs must have “AugmentedReality” in the PublicDependencyModuleNames list to include “ARBlueprintLibrary.h” and “MRMesh” to inspect the MRMesh component of the UARTrackedGeometry.</span></span> 

<span data-ttu-id="b3ae3-127">Le mappage spatial n’est pas le seul type de données exposées à travers ARTrackedGeometries. Nous devons donc vérifier que EARObjectClassification est défini sur World, ce qui indique qu’il s’agit d’une géométrie de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="b3ae3-127">Spatial mapping is not the only type of data that gets surfaced through ARTrackedGeometries, so we first check that the EARObjectClassification is World, which indicates that this is spatial mapping geometry.</span></span> 

## <a name="see-also"></a><span data-ttu-id="b3ae3-128">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b3ae3-128">See also</span></span>
* [<span data-ttu-id="b3ae3-129">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="b3ae3-129">Spatial mapping</span></span>](spatial-mapping.md)
