---
title: Ancres spatiales locales dans Unreal
description: Guide d’utilisation des ancres spatiales dans Unreal
author: hferrone
ms.author: v-haferr
ms.date: 06/10/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, ancres spatiales
ms.openlocfilehash: b102d506b1d670291c3b97ca34d277e2597af043
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376044"
---
# <a name="local-spatial-anchors-in-unreal"></a><span data-ttu-id="e6d0c-104">Ancres spatiales locales dans Unreal</span><span class="sxs-lookup"><span data-stu-id="e6d0c-104">Local Spatial Anchors in Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="e6d0c-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="e6d0c-105">Overview</span></span>

<span data-ttu-id="e6d0c-106">Les ancres spatiales sont utilisées pour enregistrer les hologrammes en place dans l’espace réel entre les sessions d’application.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-106">Spatial anchors are used to save holograms in real-world space between application sessions.</span></span> <span data-ttu-id="e6d0c-107">Elles sont exposées via Unreal sous forme d’**ARPins** et sont enregistrées dans le magasin d’ancres HoloLens, que vous allez charger dans les sessions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-107">These get surfaced through Unreal as **ARPin**s and saved in the HoloLens’ anchor store, which is loaded in future sessions.</span></span> <span data-ttu-id="e6d0c-108">Les ancres locales sont idéales comme solutions de secours lorsqu’il n’y a pas de connectivité Internet.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-108">Local anchors are ideal as a fallback when there is no internet connectivity.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6d0c-109">Les ancres locales sont stockées sur l’appareil, alors que les ancres spatiales Azure sont stockées dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-109">Local anchors are stored on device, while Azure Spatial Anchors are stored in the cloud.</span></span> <span data-ttu-id="e6d0c-110">Si vous envisagez d’utiliser les services cloud Azure pour stocker vos ancres, nous avons créé un guide qui vous aidera à intégrer [Azure Spatial Anchors](unreal-azure-spatial-anchors.md).</span><span class="sxs-lookup"><span data-stu-id="e6d0c-110">If you're looking to use Azure cloud services to store your anchors, we have a document that can walk you through integrating [Azure Spatial Anchors](unreal-azure-spatial-anchors.md).</span></span> <span data-ttu-id="e6d0c-111">Notez que vous pouvez avoir des ancres locales et Azure dans le même projet sans conflit.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-111">Note that you can have local and Azure anchors in the same project without conflict.</span></span>

## <a name="checking-the-anchor-store"></a><span data-ttu-id="e6d0c-112">Vérification du magasin d’ancres</span><span class="sxs-lookup"><span data-stu-id="e6d0c-112">Checking the anchor store</span></span>

<span data-ttu-id="e6d0c-113">Avant d’enregistrer ou de charger des ancres, vous avez besoin de vérifier si le magasin d’ancres est prêt.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-113">Before saving or loading anchors, you need to check if the anchor store is ready.</span></span>  <span data-ttu-id="e6d0c-114">Tout appel d’une des fonctions d’ancrage HoloLens échoue si le magasin d’ancres n’est pas prêt.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-114">Calling any of the HoloLens anchor functions before the anchor store is ready will not succeed.</span></span>  

![Magasin d’ancres spatiales prêt](images/unreal-spatialanchors-store-ready.PNG)

## <a name="saving-anchors"></a><span data-ttu-id="e6d0c-116">Enregistrement des ancres</span><span class="sxs-lookup"><span data-stu-id="e6d0c-116">Saving anchors</span></span>

<span data-ttu-id="e6d0c-117">Quand l’application a un composant qui doit être relié au monde réel, ce composant peut être enregistré dans le magasin d’ancres avec la séquence suivante :</span><span class="sxs-lookup"><span data-stu-id="e6d0c-117">Once the application has a component that needs to be pinned to the world, it can be saved to the anchor store with the following sequence:</span></span> 

![Enregistrer des ancres spatiales](images/unreal-spatialanchors-save.PNG)

<span data-ttu-id="e6d0c-119">Décomposons cette séquence :</span><span class="sxs-lookup"><span data-stu-id="e6d0c-119">Breaking this down:</span></span>
1. <span data-ttu-id="e6d0c-120">Générez un acteur à un emplacement connu.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-120">Spawn an actor at a known location.</span></span>
2. <span data-ttu-id="e6d0c-121">Créez un **ARPin** avec cet emplacement et un nom basé sur la classe de l’acteur.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-121">Create an **ARPin** with that location and a name based on the actor’s class.</span></span> 
3. <span data-ttu-id="e6d0c-122">Ajoutez l’acteur au **ARPin** et enregistrez le repère dans le magasin d’ancres HoloLens.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-122">Add the actor to the **ARPin** and save the pin to the HoloLens anchor store.</span></span>  
    * <span data-ttu-id="e6d0c-123">Le nom d’ancre que vous choisissez doit être unique. Dans cet exemple, il s’agit de l’horodatage actuel.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-123">The anchor name you choose must be unique, which in this example is the current timestamp.</span></span> 

4. <span data-ttu-id="e6d0c-124">Si l’ancre est correctement enregistrée dans le magasin d’ancres, vous pouvez l’inspecter dans le portail d’appareil HoloLens sous **System > Map Manager > Anchor Files Saved On Device**.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-124">If the anchor is successfully saved to the anchor store, you can be inspect it in the HoloLens device portal under **System > Map manager > Anchor Files Saved On Device**.</span></span> 

## <a name="loading-anchors"></a><span data-ttu-id="e6d0c-125">Chargement des ancres</span><span class="sxs-lookup"><span data-stu-id="e6d0c-125">Loading anchors</span></span>

<span data-ttu-id="e6d0c-126">Au démarrage d’une application, vous pouvez utiliser le blueprint ci-dessous pour rétablir les composants à leurs positions d’ancrage :</span><span class="sxs-lookup"><span data-stu-id="e6d0c-126">When an application starts, you can use the following blueprint to restore components to their anchor locations:</span></span>

![Charger des ancres spatiales](images/unreal-spatialanchors-load.PNG)

<span data-ttu-id="e6d0c-128">Décomposons cette séquence :</span><span class="sxs-lookup"><span data-stu-id="e6d0c-128">Breaking this down:</span></span>
1. <span data-ttu-id="e6d0c-129">Effectuez une itération sur toutes les ancres du magasin d’ancres.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-129">Iterate over all of the anchors in the anchor store.</span></span> 
2. <span data-ttu-id="e6d0c-130">Générez un acteur au niveau de l’identité.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-130">Spawn an actor at identity.</span></span>
3. <span data-ttu-id="e6d0c-131">Épinglez cet acteur au **ARPin** à partir du magasin d’ancres.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-131">Pin that actor to the **ARPin** from the anchor store.</span></span>  

    * <span data-ttu-id="e6d0c-132">Il est important de générer l’acteur au niveau de l’identité, car l’ancre est chargée de repositionner l’hologramme dans l’environnement selon l’emplacement auquel il a été enregistré.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-132">It's important to spawn the actor at identity since the anchor is responsible for repositioning the hologram in the world based on where it was saved.</span></span> <span data-ttu-id="e6d0c-133">Toute transformation ajoutée ici va ajouter un décalage à l’ancre.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-133">Any transform added here will add an offset to the anchor.</span></span> 

<span data-ttu-id="e6d0c-134">L’ID de l’ancre est également demandé afin que différents acteurs puissent être générés en fonction du nom enregistré de l’ancre.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-134">The anchor ID is also queried so that different actors can be spawned depending on the anchor’s saved name.</span></span> 

## <a name="removing-anchors"></a><span data-ttu-id="e6d0c-135">Suppression des ancres</span><span class="sxs-lookup"><span data-stu-id="e6d0c-135">Removing anchors</span></span> 

<span data-ttu-id="e6d0c-136">Lorsque vous n’avez plus besoin d’une ancre, vous pouvez l’effacer individuellement ou effacer la totalité du magasin d’ancres avec les composants **Remove ARPin from WMRAnchor Store** et **Remove All ARPins from WMRAnchor Store**.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-136">When you're done with an anchor you can clear individual anchors or the entire anchor store with the **Remove ARPin from WMRAnchor Store** and **Remove All ARPins from WMRAnchor Store** components.</span></span>

![Supprimer des ancres spatiales](images/unreal-spatialanchors-remove.PNG)

> [!NOTE]
> <span data-ttu-id="e6d0c-138">N’oubliez pas que les ancres spatiales sont encore en version bêta, donc n’hésitez pas à vous tenir au courant des dernières informations et fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="e6d0c-138">Bear in mind that Spatial Anchors are still in Beta, so be sure to check back for updated information and features.</span></span>

## <a name="see-also"></a><span data-ttu-id="e6d0c-139">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e6d0c-139">See also</span></span>
* [<span data-ttu-id="e6d0c-140">Azure Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="e6d0c-140">Azure Spatial Anchors</span></span>](unreal-azure-spatial-anchors.md)
* [<span data-ttu-id="e6d0c-141">Ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="e6d0c-141">Spatial anchors</span></span>](spatial-anchors.md)
* [<span data-ttu-id="e6d0c-142">Systèmes de coordonnées</span><span class="sxs-lookup"><span data-stu-id="e6d0c-142">Coordinate systems</span></span>](coordinate-systems.md)
