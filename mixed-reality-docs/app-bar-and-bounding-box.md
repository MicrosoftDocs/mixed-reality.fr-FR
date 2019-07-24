---
title: Cadre englobant et barre de l’application
description: La barre de l’application est un menu de niveau objet qui contient une série de boutons qui s’affichent sur le bord inférieur des limites d’un hologramme.
author: radicalad
ms.author: adlinv
ms.date: 06/07/2019
ms.topic: article
keywords: Windows Mixed Reality, barre d’application, cadre englobant
ms.openlocfilehash: d289be31129324c6ff419b69dbce52bd8f62eb64
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829684"
---
# <a name="bounding-box-and-app-bar"></a><span data-ttu-id="80920-104">Cadre englobant et barre de l’application</span><span class="sxs-lookup"><span data-stu-id="80920-104">Bounding box and App bar</span></span>
![La délimitation est l’interface standard pour la manipulation d’objets en réalité mixte.](images/640px-boundingbox-hero.jpg)<br>

## <a name="what-is-the-bounding-box"></a><span data-ttu-id="80920-106">Qu’est-ce que le cadre englobant?</span><span class="sxs-lookup"><span data-stu-id="80920-106">What is the Bounding box?</span></span>

<span data-ttu-id="80920-107">La délimitation est l’interface standard pour la manipulation d’objets en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="80920-107">Bounding is the standard interface for object manipulation in Mixed Reality.</span></span> <span data-ttu-id="80920-108">Il permet à l’utilisateur de s’assurer que l’objet est actuellement réglable.</span><span class="sxs-lookup"><span data-stu-id="80920-108">It provides the user an affordance that the object is currently adjustable.</span></span> <span data-ttu-id="80920-109">Les angles indiquent à l’utilisateur que l’objet peut également être mis à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="80920-109">The corners tell the user that the object can also scale.</span></span> <span data-ttu-id="80920-110">Ce visuel offre aux utilisateurs la zone totale de l’objet, même s’ils ne sont pas visibles en dehors d’un mode de réglage.</span><span class="sxs-lookup"><span data-stu-id="80920-110">This visual affordance shows users the total area of the object – even if it’s not visible outside of an adjustment mode.</span></span> <span data-ttu-id="80920-111">Ceci est particulièrement important, car s’il n’y figure pas, un objet accroché à un autre objet ou surface peut sembler se comporter comme s’il existait un espace qui ne devrait pas y figurer.</span><span class="sxs-lookup"><span data-stu-id="80920-111">This is especially important because if it weren’t there, an object snapped to another object or surface may appear to behave as if there was space around it that shouldn’t be there.</span></span> <span data-ttu-id="80920-112">Sur HoloLens 2, le cadre englobant fonctionne avec la manipulation directe de la main et répond à la proximité de l’utilisateur finger’s.</span><span class="sxs-lookup"><span data-stu-id="80920-112">On HoloLens 2, the bounding box works with direct hand manipulation and responds to the user's finger's proximity.</span></span> <span data-ttu-id="80920-113">Il affiche des commentaires visuels pour aider l’utilisateur à percevoir la distance par rapport à l’objet.</span><span class="sxs-lookup"><span data-stu-id="80920-113">It shows visual feedback to help the user perceive the distance from the object.</span></span> 

<span data-ttu-id="80920-114">![HoloLens point de vue de la mise à l’échelle d’un objet à l’aide du cadre englobant](images/HoloLens2_BoundingBox.gif)</span><span class="sxs-lookup"><span data-stu-id="80920-114">![HoloLens point-of-view of scaling an object via bounding box](images/HoloLens2_BoundingBox.gif)</span></span><br>
<span data-ttu-id="80920-115">*Mise à l’échelle d’un objet à l’aide du cadre englobant*</span><span class="sxs-lookup"><span data-stu-id="80920-115">*Scaling an object via bounding box*</span></span>

<span data-ttu-id="80920-116">Les poignées situées aux angles du rectangle englobant suivent un modèle largement compréhensible pour ajuster l’échelle.</span><span class="sxs-lookup"><span data-stu-id="80920-116">The handles in the corners of the bounding box follow a widely understood pattern for adjusting scale.</span></span> 

<span data-ttu-id="80920-117">![HoloLens point de vue de la rotation d’un objet par le biais du cadre englobant](images/HoloLens2_BoundingBox_Rotate.gif)</span><span class="sxs-lookup"><span data-stu-id="80920-117">![HoloLens point-of-view of rotating an object via bounding box](images/HoloLens2_BoundingBox_Rotate.gif)</span></span><br>
<span data-ttu-id="80920-118">*Rotation d’un objet à l’aide du cadre englobant*</span><span class="sxs-lookup"><span data-stu-id="80920-118">*Rotating an object via bounding box*</span></span>


<span data-ttu-id="80920-119">![Commentaires visuels à proximité](images/HoloLens2_Proximity.gif)</span><span class="sxs-lookup"><span data-stu-id="80920-119">![Visual feedback on hand proximity](images/HoloLens2_Proximity.gif)</span></span><br>
<span data-ttu-id="80920-120">*Commentaires visuels en fonction de la proximité*</span><span class="sxs-lookup"><span data-stu-id="80920-120">*Visual feedback based on the proximity*</span></span>

<span data-ttu-id="80920-121">Les intuitivité rectangulaires verticaux sur les bords du cadre englobant sont des indicateurs de rotation.</span><span class="sxs-lookup"><span data-stu-id="80920-121">The vertical rectangular affordances on the edges of the bounding box are rotation indicators.</span></span> <span data-ttu-id="80920-122">Cela permet à l’utilisateur d’effectuer des ajustements plus précis sur les hologrammes placés.</span><span class="sxs-lookup"><span data-stu-id="80920-122">This gives the user more fine adjustment over their placed holograms.</span></span> <span data-ttu-id="80920-123">Ils peuvent non seulement les ajuster et les mettre à l’échelle, mais également faire pivoter.</span><span class="sxs-lookup"><span data-stu-id="80920-123">Not only can they adjust and scale, but now rotate as well.</span></span>

* <span data-ttu-id="80920-124">Pour le développement d’applications Unity, consultez cadre [englobant sur la réalité mixte Toolkit-Unity](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)</span><span class="sxs-lookup"><span data-stu-id="80920-124">For Unity app development, see [Bounding box on Mixed Reality Toolkit-Unity](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)</span></span>



## <a name="what-is-the-app-bar"></a><span data-ttu-id="80920-125">Qu’est-ce que la barre d’application?</span><span class="sxs-lookup"><span data-stu-id="80920-125">What is the App bar?</span></span>

<span data-ttu-id="80920-126">La barre de l’application est un menu de niveau objet qui contient une série de boutons qui s’affichent sur le bord inférieur des limites d’un hologramme.</span><span class="sxs-lookup"><span data-stu-id="80920-126">The App bar is a object-level menu containing a series of buttons that displays on the bottom edge of a hologram's bounds.</span></span> <span data-ttu-id="80920-127">Ce modèle est couramment utilisé pour permettre aux utilisateurs de supprimer et d’ajuster des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="80920-127">This pattern is commonly used to give users the ability to remove and adjust holograms.</span></span>

<span data-ttu-id="80920-128">Étant donné que ce modèle est utilisé avec les objets qui sont verrouillés au monde, lorsqu’un utilisateur se déplace autour de l’objet, la barre de l’application s’affichera toujours sur le côté objets le plus proche de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="80920-128">Since this pattern is used with objects that are world locked, as a user moves around the object the App bar will always display on the objects' side closest to the user.</span></span> <span data-ttu-id="80920-129">Même si ce n’est pas le cas, il obtient le même résultat. empêcher la position d’un utilisateur pour occultait ou bloquer les fonctionnalités qui seraient autrement disponibles à partir d’un autre emplacement dans son environnement.</span><span class="sxs-lookup"><span data-stu-id="80920-129">While this isn't billboarding, it effectively achieves the same result; preventing a user's position to occlude or block functionality that would otherwise be available from a different location in their environment.</span></span>

<span data-ttu-id="80920-130">![Parcours d’un hologramme.</span><span class="sxs-lookup"><span data-stu-id="80920-130">![Walking around a hologram.</span></span> <span data-ttu-id="80920-131">La barre de l’application suit.](images/HoloLens2_AppBarFollowing.gif)</span><span class="sxs-lookup"><span data-stu-id="80920-131">The App bar follows.](images/HoloLens2_AppBarFollowing.gif)</span></span><br>
<span data-ttu-id="80920-132">*Si vous vous déplacez autour d’un hologramme, la barre de l’application suit*</span><span class="sxs-lookup"><span data-stu-id="80920-132">*Walking around a hologram, the App bar follows*</span></span>

<span data-ttu-id="80920-133">La barre de l’application a été conçue principalement comme un moyen de gérer les objets placés dans l’environnement d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="80920-133">The App bar was designed primarily as a way to manage placed objects in a user's environment.</span></span> <span data-ttu-id="80920-134">Couplée avec le cadre englobant, un utilisateur dispose d’un contrôle total sur l’emplacement et la manière dont les objets sont orientés en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="80920-134">Coupled with the bounding box, a user has full control over where and how objects are oriented in mixed reality.</span></span>

* <span data-ttu-id="80920-135">Pour le développement d’applications Unity, consultez la [barre d’application sur la réalité mixte Toolkit-Unity](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html)</span><span class="sxs-lookup"><span data-stu-id="80920-135">For Unity app development, see [App bar on Mixed Reality Toolkit-Unity](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html)</span></span>

## <a name="see-also"></a><span data-ttu-id="80920-136">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="80920-136">See also</span></span>
* [<span data-ttu-id="80920-137">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="80920-137">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="80920-138">Texte dans Unity</span><span class="sxs-lookup"><span data-stu-id="80920-138">Text in Unity</span></span>](text-in-unity.md)
* [<span data-ttu-id="80920-139">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="80920-139">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="80920-140">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="80920-140">Displaying progress</span></span>](progress.md)
