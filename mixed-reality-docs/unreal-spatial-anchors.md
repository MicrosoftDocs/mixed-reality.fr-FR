---
title: Ancres spatiales dans Unreal
description: Guide d’utilisation des ancres spatiales dans Unreal
author: hferrone
ms.author: v-haferr
ms.date: 06/10/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, ancres spatiales
ms.openlocfilehash: 58394f4e27aff5070d55ed5f0d62cd81ff579d1f
ms.sourcegitcommit: 45da0a056fa42088ff81ccdd11232830fbe8430f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84720315"
---
# <a name="spatial-anchors-in-unreal"></a><span data-ttu-id="4dfea-104">Ancres spatiales dans Unreal</span><span class="sxs-lookup"><span data-stu-id="4dfea-104">Spatial Anchors in Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="4dfea-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="4dfea-105">Overview</span></span>

<span data-ttu-id="4dfea-106">Les ancres spatiales sont utilisées pour enregistrer les hologrammes en place dans l’espace réel entre les sessions d’application.</span><span class="sxs-lookup"><span data-stu-id="4dfea-106">Spatial anchors are used to save holograms in real-world space between application sessions.</span></span>  <span data-ttu-id="4dfea-107">Elles sont exposées via Unreal sous forme d’**ARPins** et sont enregistrées dans le magasin d’ancres HoloLens, que vous allez charger dans les sessions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="4dfea-107">These get surfaced through Unreal as **ARPin**s and saved in the HoloLens’ anchor store, which is loaded in future sessions.</span></span> 

## <a name="checking-the-anchor-store"></a><span data-ttu-id="4dfea-108">Vérification du magasin d’ancres</span><span class="sxs-lookup"><span data-stu-id="4dfea-108">Checking the anchor store</span></span>

<span data-ttu-id="4dfea-109">Avant d’enregistrer ou de charger des ancres, vous avez besoin de vérifier si le magasin d’ancres est prêt.</span><span class="sxs-lookup"><span data-stu-id="4dfea-109">Before saving or loading anchors, you need to check if the anchor store is ready.</span></span>  <span data-ttu-id="4dfea-110">Tout appel d’une des fonctions d’ancrage HoloLens échoue si le magasin d’ancres n’est pas prêt.</span><span class="sxs-lookup"><span data-stu-id="4dfea-110">Calling any of the HoloLens anchor functions before the anchor store is ready will not succeed.</span></span>  

![Magasin d’ancres spatiales prêt](images/unreal-spatialanchors-store-ready.PNG)

## <a name="saving-anchors"></a><span data-ttu-id="4dfea-112">Enregistrement des ancres</span><span class="sxs-lookup"><span data-stu-id="4dfea-112">Saving anchors</span></span>

<span data-ttu-id="4dfea-113">Quand l’application a un composant qui doit être relié au monde réel, ce composant peut être enregistré dans le magasin d’ancres avec la séquence suivante :</span><span class="sxs-lookup"><span data-stu-id="4dfea-113">Once the application has a component that needs to be pinned to the world, it can be saved to the anchor store with the following sequence:</span></span> 

![Enregistrer des ancres spatiales](images/unreal-spatialanchors-save.PNG)

<span data-ttu-id="4dfea-115">Décomposons cette séquence :</span><span class="sxs-lookup"><span data-stu-id="4dfea-115">Breaking this down:</span></span>
1. <span data-ttu-id="4dfea-116">Générez un acteur à un emplacement connu.</span><span class="sxs-lookup"><span data-stu-id="4dfea-116">Spawn an actor at a known location.</span></span>
2. <span data-ttu-id="4dfea-117">Créez un **ARPin** avec cet emplacement et un nom basé sur la classe de l’acteur.</span><span class="sxs-lookup"><span data-stu-id="4dfea-117">Create an **ARPin** with that location and a name based on the actor’s class.</span></span> 
3. <span data-ttu-id="4dfea-118">Ajoutez l’acteur au **ARPin** et enregistrez le repère dans le magasin d’ancres HoloLens.</span><span class="sxs-lookup"><span data-stu-id="4dfea-118">Add the actor to the **ARPin** and save the pin to the HoloLens anchor store.</span></span>  
    * <span data-ttu-id="4dfea-119">Le nom d’ancre que vous choisissez doit être unique. Dans cet exemple, il s’agit de l’horodatage actuel.</span><span class="sxs-lookup"><span data-stu-id="4dfea-119">The anchor name you choose must be unique, which in this example is the current timestamp.</span></span> 

4. <span data-ttu-id="4dfea-120">Si l’ancre est correctement enregistrée dans le magasin d’ancres, vous pouvez l’inspecter dans le portail d’appareil HoloLens sous **System > Map Manager > Anchor Files Saved On Device**.</span><span class="sxs-lookup"><span data-stu-id="4dfea-120">If the anchor is successfully saved to the anchor store, you can be inspect it in the HoloLens device portal under **System > Map manager > Anchor Files Saved On Device**.</span></span> 

## <a name="loading-anchors"></a><span data-ttu-id="4dfea-121">Chargement des ancres</span><span class="sxs-lookup"><span data-stu-id="4dfea-121">Loading anchors</span></span>

<span data-ttu-id="4dfea-122">Au démarrage d’une application, vous pouvez utiliser le blueprint ci-dessous pour rétablir les composants à leurs positions d’ancrage :</span><span class="sxs-lookup"><span data-stu-id="4dfea-122">When an application starts, you can use the following blueprint to restore components to their anchor locations:</span></span>

![Charger des ancres spatiales](images/unreal-spatialanchors-load.PNG)

<span data-ttu-id="4dfea-124">Décomposons cette séquence :</span><span class="sxs-lookup"><span data-stu-id="4dfea-124">Breaking this down:</span></span>
1. <span data-ttu-id="4dfea-125">Effectuez une itération sur toutes les ancres du magasin d’ancres.</span><span class="sxs-lookup"><span data-stu-id="4dfea-125">Iterate over all of the anchors in the anchor store.</span></span> 
2. <span data-ttu-id="4dfea-126">Générez un acteur au niveau de l’identité.</span><span class="sxs-lookup"><span data-stu-id="4dfea-126">Spawn an actor at identity.</span></span>
3. <span data-ttu-id="4dfea-127">Épinglez cet acteur au **ARPin** à partir du magasin d’ancres.</span><span class="sxs-lookup"><span data-stu-id="4dfea-127">Pin that actor to the **ARPin** from the anchor store.</span></span>  

    * <span data-ttu-id="4dfea-128">Il est important de générer l’acteur au niveau de l’identité, car l’ancre est chargée de repositionner l’hologramme dans l’environnement selon l’emplacement auquel il a été enregistré.</span><span class="sxs-lookup"><span data-stu-id="4dfea-128">It's important to spawn the actor at identity since the anchor is responsible for repositioning the hologram in the world based on where it was saved.</span></span> <span data-ttu-id="4dfea-129">Toute transformation ajoutée ici va ajouter un décalage à l’ancre.</span><span class="sxs-lookup"><span data-stu-id="4dfea-129">Any transform added here will add an offset to the anchor.</span></span> 

<span data-ttu-id="4dfea-130">L’ID de l’ancre est également demandé afin que différents acteurs puissent être générés en fonction du nom enregistré de l’ancre.</span><span class="sxs-lookup"><span data-stu-id="4dfea-130">The anchor ID is also queried so that different actors can be spawned depending on the anchor’s saved name.</span></span> 

## <a name="removing-anchors"></a><span data-ttu-id="4dfea-131">Suppression des ancres</span><span class="sxs-lookup"><span data-stu-id="4dfea-131">Removing anchors</span></span> 

<span data-ttu-id="4dfea-132">Lorsque vous n’avez plus besoin d’une ancre, vous pouvez l’effacer individuellement ou effacer la totalité du magasin d’ancres avec les composants **Remove ARPin from WMRAnchor Store** et **Remove All ARPins from WMRAnchor Store**.</span><span class="sxs-lookup"><span data-stu-id="4dfea-132">When you're done with an anchor you can clear individual anchors or the entire anchor store with the **Remove ARPin from WMRAnchor Store** and **Remove All ARPins from WMRAnchor Store** components.</span></span>

![Supprimer des ancres spatiales](images/unreal-spatialanchors-remove.PNG)

> [!NOTE]
> <span data-ttu-id="4dfea-134">N’oubliez pas que les ancres spatiales sont encore en version bêta, donc n’hésitez pas à vous tenir au courant des dernières informations et fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="4dfea-134">Bear in mind that Spatial Anchors are still in Beta, so be sure to check back for updated information and features.</span></span>

## <a name="see-also"></a><span data-ttu-id="4dfea-135">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4dfea-135">See also</span></span>
* [<span data-ttu-id="4dfea-136">Ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="4dfea-136">Spatial anchors</span></span>](spatial-anchors.md)
* [<span data-ttu-id="4dfea-137">Systèmes de coordonnées</span><span class="sxs-lookup"><span data-stu-id="4dfea-137">Coordinate systems</span></span>](coordinate-systems.md)
