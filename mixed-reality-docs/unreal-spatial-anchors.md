---
title: Ancres spatiales dans Unreal
description: Guide d’utilisation des ancres spatiales dans Unreal
author: sw5813
ms.author: jacksonf
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, ancres spatiales
ms.openlocfilehash: c35d8efc9998aac5b40de833e5acbf7f80353e6b
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82840138"
---
# <a name="spatial-anchors-in-unreal"></a><span data-ttu-id="25510-104">Ancres spatiales dans Unreal</span><span class="sxs-lookup"><span data-stu-id="25510-104">Spatial Anchors in Unreal</span></span>

<span data-ttu-id="25510-105">Les ancres spatiales sont utilisées pour conserver les hologrammes en place dans l’espace réel entre les sessions d’application.</span><span class="sxs-lookup"><span data-stu-id="25510-105">Spatial anchors are used to persist holograms in real-world space between application sessions.</span></span>  <span data-ttu-id="25510-106">Elles sont exposées via Unreal sous forme d’ARPins et sont enregistrées dans le magasin d’ancres HoloLens en vue de leur chargement dans les sessions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="25510-106">This gets surfaced through Unreal as ARPins and gets saved in the HoloLens’ anchor store to be loaded in future sessions.</span></span> 

<span data-ttu-id="25510-107">Avant d’enregistrer ou de charger des ancres, vérifiez que le magasin d’ancres est prêt.</span><span class="sxs-lookup"><span data-stu-id="25510-107">Before saving or loading anchors, first check that the anchor store is ready.</span></span>  <span data-ttu-id="25510-108">Toute tentative d’appel d’une des fonctions d’ancrage HoloLens échouera si le magasin d’ancres n’est pas prêt.</span><span class="sxs-lookup"><span data-stu-id="25510-108">Attempting to call any of the HoloLens anchor functions before the anchor store is ready will not succeed.</span></span>  

![Magasin d’ancres spatiales prêt](images/unreal-spatialanchors-store-ready.PNG)

## <a name="save-anchors"></a><span data-ttu-id="25510-110">Enregistrer des ancres</span><span class="sxs-lookup"><span data-stu-id="25510-110">Save Anchors</span></span>

<span data-ttu-id="25510-111">Quand l’application a un composant qui doit être relié au monde réel, ce composant peut être enregistré dans le magasin d’ancres avec la séquence suivante :</span><span class="sxs-lookup"><span data-stu-id="25510-111">Once the application has a component that needs to be pinned to the world, it can be saved to the anchor store with the following sequence:</span></span> 

![Enregistrer des ancres spatiales](images/unreal-spatialanchors-save.PNG)

<span data-ttu-id="25510-113">Ici, nous générons un acteur à une position connue, nous créons un ARPin avec cette position et un nom basé sur la classe de l’acteur, nous ajoutons l’acteur à l’ARPin et nous enregistrons la broche dans le magasin d’ancres HoloLens.</span><span class="sxs-lookup"><span data-stu-id="25510-113">Here, we are spawning an actor at a known location, creating an ARPin with that location and a name based on the actor’s class, adding the actor to the ARPin, and saving the pin to the HoloLens anchor store.</span></span>  <span data-ttu-id="25510-114">Nous devons choisir un nom d’ancre unique. C’est pourquoi, dans cet exemple, nous ajoutons l’horodatage actuel.</span><span class="sxs-lookup"><span data-stu-id="25510-114">The anchor name we choose must be unique, so in this example we append the current timestamp.</span></span>  <span data-ttu-id="25510-115">Une fois que l’ancre a été enregistrée dans le magasin d’ancres, elle est visible dans le portail d’appareil pour HoloLens sous System > Map Manager > Anchor Files Saved On Device.</span><span class="sxs-lookup"><span data-stu-id="25510-115">If the anchor successfully saves to the anchor store, it can be inspected in the HoloLens device portal under System > Map manager > Anchor Files Saved On Device.</span></span> 

## <a name="load-anchors"></a><span data-ttu-id="25510-116">Charger des ancres</span><span class="sxs-lookup"><span data-stu-id="25510-116">Load Anchors</span></span>

<span data-ttu-id="25510-117">Au démarrage d’une application, le Blueprint ci-dessous peut être appelé pour rétablir les composants à leurs positions d’ancrage :</span><span class="sxs-lookup"><span data-stu-id="25510-117">When an application starts, the following blueprint can be called to restore components to their anchor locations:</span></span>

![Charger des ancres spatiales](images/unreal-spatialanchors-load.PNG)

<span data-ttu-id="25510-119">Dans cet exemple, nous faisons une itération sur toutes les ancres du magasin d’ancres, nous générons un acteur au niveau de l’identité et nous relions cet acteur à l’ARPin à partir du magasin d’ancres.</span><span class="sxs-lookup"><span data-stu-id="25510-119">In this example, we iterate over all of the anchors in the anchor store, spawn an actor at identity, and pin that actor to the ARPin from the anchor store.</span></span>  <span data-ttu-id="25510-120">Il est important de générer l’acteur au niveau de l’identité, car comme l’ancre repositionne l’hologramme dans le monde réel en fonction de son emplacement d’enregistrement, si une transformation est ajoutée ici, un décalage sera ajouté à l’ancre.</span><span class="sxs-lookup"><span data-stu-id="25510-120">It is important to spawn the actor at identity since the anchor is responsible for repositioning the hologram in the world based on where it was saved, so any transform added here will add an offset to the anchor.</span></span> 

<span data-ttu-id="25510-121">L’ID de l’ancre est également demandé afin que différents acteurs puissent être générés en fonction du nom enregistré de l’ancre.</span><span class="sxs-lookup"><span data-stu-id="25510-121">The anchor ID is also queried so that different actors can be spawned depending on the anchor’s saved name.</span></span> 

## <a name="remove-anchors"></a><span data-ttu-id="25510-122">Supprimer des ancres</span><span class="sxs-lookup"><span data-stu-id="25510-122">Remove Anchors</span></span> 

<span data-ttu-id="25510-123">Lorsque vous n’avez plus besoin d’une ancre, vous pouvez supprimer tout le contenu du magasin d’ancres, ou supprimer individuellement les ancres du magasin que vous ne souhaitez pas inclure dans les sessions ultérieures :</span><span class="sxs-lookup"><span data-stu-id="25510-123">When done with an anchor, the entire anchor store can be cleared, or individual anchors can be removed from the anchor store so they are not included in future sessions:</span></span> 

![Supprimer des ancres spatiales](images/unreal-spatialanchors-remove.PNG)

## <a name="see-also"></a><span data-ttu-id="25510-125">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="25510-125">See also</span></span>
* [<span data-ttu-id="25510-126">Ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="25510-126">Spatial anchors</span></span>](spatial-anchors.md)
* [<span data-ttu-id="25510-127">Systèmes de coordonnées</span><span class="sxs-lookup"><span data-stu-id="25510-127">Coordinate systems</span></span>](coordinate-systems.md)
