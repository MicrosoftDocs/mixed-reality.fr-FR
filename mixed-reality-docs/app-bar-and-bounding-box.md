---
title: Cadre englobant de la zone et la barre de l’application
description: La barre des applications est un menu de niveau de l’objet qui contient une série de boutons qui s’affiche sur le bord inférieur des limites d’un hologramme.
author: radicalad
ms.author: adlinv
ms.date: 06/07/2019
ms.topic: article
keywords: Windows Mixed Reality, barre, zone englobante de l’application
ms.openlocfilehash: d289be31129324c6ff419b69dbce52bd8f62eb64
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829684"
---
# <a name="bounding-box-and-app-bar"></a><span data-ttu-id="38f9f-104">Cadre englobant de la zone et la barre de l’application</span><span class="sxs-lookup"><span data-stu-id="38f9f-104">Bounding box and App bar</span></span>
![La délimitation est l’interface standard pour la manipulation des objets dans la réalité mixte.](images/640px-boundingbox-hero.jpg)<br>

## <a name="what-is-the-bounding-box"></a><span data-ttu-id="38f9f-106">Quelle est la zone englobante ?</span><span class="sxs-lookup"><span data-stu-id="38f9f-106">What is the Bounding box?</span></span>

<span data-ttu-id="38f9f-107">La délimitation est l’interface standard pour la manipulation des objets dans la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="38f9f-107">Bounding is the standard interface for object manipulation in Mixed Reality.</span></span> <span data-ttu-id="38f9f-108">Il fournit à l’utilisateur un intuitif que l’objet est actuellement réglable.</span><span class="sxs-lookup"><span data-stu-id="38f9f-108">It provides the user an affordance that the object is currently adjustable.</span></span> <span data-ttu-id="38f9f-109">Les angles indiquent à l’utilisateur que l’objet peut également mettre à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="38f9f-109">The corners tell the user that the object can also scale.</span></span> <span data-ttu-id="38f9f-110">Ce visuel intuitif affiche les utilisateurs la zone totale de l’objet : même s’il n’est pas visible en dehors d’un mode d’ajustement.</span><span class="sxs-lookup"><span data-stu-id="38f9f-110">This visual affordance shows users the total area of the object – even if it’s not visible outside of an adjustment mode.</span></span> <span data-ttu-id="38f9f-111">Cela est particulièrement important, car si elle n’était pas il, un objet aligné sur un autre objet ou la surface semble se comporte comme si l’espace autour d’elle et qui ne doivent pas être présents.</span><span class="sxs-lookup"><span data-stu-id="38f9f-111">This is especially important because if it weren’t there, an object snapped to another object or surface may appear to behave as if there was space around it that shouldn’t be there.</span></span> <span data-ttu-id="38f9f-112">Sur HoloLens 2, la zone englobante fonctionne avec la manipulation de direct disponible et répond à proximité du doigt de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="38f9f-112">On HoloLens 2, the bounding box works with direct hand manipulation and responds to the user's finger's proximity.</span></span> <span data-ttu-id="38f9f-113">Il montre une rétroaction visuelle pour aider l’utilisateur à percevoir la distance à partir de l’objet.</span><span class="sxs-lookup"><span data-stu-id="38f9f-113">It shows visual feedback to help the user perceive the distance from the object.</span></span> 

<span data-ttu-id="38f9f-114">![HoloLens de point de vue de la mise à l’échelle un objet par le biais de zone englobante](images/HoloLens2_BoundingBox.gif)</span><span class="sxs-lookup"><span data-stu-id="38f9f-114">![HoloLens point-of-view of scaling an object via bounding box](images/HoloLens2_BoundingBox.gif)</span></span><br>
<span data-ttu-id="38f9f-115">*Mise à l’échelle un objet par le biais de zone englobante*</span><span class="sxs-lookup"><span data-stu-id="38f9f-115">*Scaling an object via bounding box*</span></span>

<span data-ttu-id="38f9f-116">Les descripteurs dans les angles du rectangle englobant suivent un modèle très largement compris pour ajuster l’échelle.</span><span class="sxs-lookup"><span data-stu-id="38f9f-116">The handles in the corners of the bounding box follow a widely understood pattern for adjusting scale.</span></span> 

<span data-ttu-id="38f9f-117">![HoloLens de point de vue de faire pivoter un objet par le biais de zone englobante](images/HoloLens2_BoundingBox_Rotate.gif)</span><span class="sxs-lookup"><span data-stu-id="38f9f-117">![HoloLens point-of-view of rotating an object via bounding box](images/HoloLens2_BoundingBox_Rotate.gif)</span></span><br>
<span data-ttu-id="38f9f-118">*Rotation d’un objet par le biais de zone englobante*</span><span class="sxs-lookup"><span data-stu-id="38f9f-118">*Rotating an object via bounding box*</span></span>


<span data-ttu-id="38f9f-119">![Commentaires visuels sur la proximité de main](images/HoloLens2_Proximity.gif)</span><span class="sxs-lookup"><span data-stu-id="38f9f-119">![Visual feedback on hand proximity](images/HoloLens2_Proximity.gif)</span></span><br>
<span data-ttu-id="38f9f-120">*Commentaires visuels en fonction de la proximité*</span><span class="sxs-lookup"><span data-stu-id="38f9f-120">*Visual feedback based on the proximity*</span></span>

<span data-ttu-id="38f9f-121">L’intuitivité rectangulaire verticale sur les bords du rectangle englobant est des indicateurs de rotation.</span><span class="sxs-lookup"><span data-stu-id="38f9f-121">The vertical rectangular affordances on the edges of the bounding box are rotation indicators.</span></span> <span data-ttu-id="38f9f-122">Ainsi, l’utilisateur plus un réglage sur leurs hologrammes placés.</span><span class="sxs-lookup"><span data-stu-id="38f9f-122">This gives the user more fine adjustment over their placed holograms.</span></span> <span data-ttu-id="38f9f-123">Non seulement peuvent ils ajuster et mettre à l’échelle, mais maintenant, faites tourner également.</span><span class="sxs-lookup"><span data-stu-id="38f9f-123">Not only can they adjust and scale, but now rotate as well.</span></span>

* <span data-ttu-id="38f9f-124">Pour le développement d’applications Unity, consultez [englobant sur des Toolkit-Unity de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)</span><span class="sxs-lookup"><span data-stu-id="38f9f-124">For Unity app development, see [Bounding box on Mixed Reality Toolkit-Unity](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)</span></span>



## <a name="what-is-the-app-bar"></a><span data-ttu-id="38f9f-125">Quelle est la barre des applications ?</span><span class="sxs-lookup"><span data-stu-id="38f9f-125">What is the App bar?</span></span>

<span data-ttu-id="38f9f-126">La barre des applications est un menu de niveau de l’objet qui contient une série de boutons qui s’affiche sur le bord inférieur des limites d’un hologramme.</span><span class="sxs-lookup"><span data-stu-id="38f9f-126">The App bar is a object-level menu containing a series of buttons that displays on the bottom edge of a hologram's bounds.</span></span> <span data-ttu-id="38f9f-127">Ce modèle est généralement utilisé pour permettre aux utilisateurs la possibilité de supprimer et ajuster hologrammes.</span><span class="sxs-lookup"><span data-stu-id="38f9f-127">This pattern is commonly used to give users the ability to remove and adjust holograms.</span></span>

<span data-ttu-id="38f9f-128">Dans la mesure où ce modèle est utilisé avec des objets qui sont world verrouillé, comme un utilisateur se déplace l’objet de que la barre de l’application affiche toujours sur le côté de l’objet le plus proche de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="38f9f-128">Since this pattern is used with objects that are world locked, as a user moves around the object the App bar will always display on the objects' side closest to the user.</span></span> <span data-ttu-id="38f9f-129">Bien que cela n’est pas le billboarding, elle efficacement permet d’obtenir le même résultat ; empêche la position d’occlude d’un utilisateur ou une fonctionnalité de bloc qui serait disponible à partir d’un autre emplacement dans leur environnement.</span><span class="sxs-lookup"><span data-stu-id="38f9f-129">While this isn't billboarding, it effectively achieves the same result; preventing a user's position to occlude or block functionality that would otherwise be available from a different location in their environment.</span></span>

<span data-ttu-id="38f9f-130">![Vous épargne un hologramme.</span><span class="sxs-lookup"><span data-stu-id="38f9f-130">![Walking around a hologram.</span></span> <span data-ttu-id="38f9f-131">La barre des applications suit.](images/HoloLens2_AppBarFollowing.gif)</span><span class="sxs-lookup"><span data-stu-id="38f9f-131">The App bar follows.](images/HoloLens2_AppBarFollowing.gif)</span></span><br>
<span data-ttu-id="38f9f-132">*Vous épargne un hologramme, suit de la barre des applications*</span><span class="sxs-lookup"><span data-stu-id="38f9f-132">*Walking around a hologram, the App bar follows*</span></span>

<span data-ttu-id="38f9f-133">La barre de l’application a été conçue principalement comme un moyen de gérer les objets placés dans un environnement d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="38f9f-133">The App bar was designed primarily as a way to manage placed objects in a user's environment.</span></span> <span data-ttu-id="38f9f-134">Associé à la zone englobante, un utilisateur a un contrôle total sur où et comment les objets sont orientées en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="38f9f-134">Coupled with the bounding box, a user has full control over where and how objects are oriented in mixed reality.</span></span>

* <span data-ttu-id="38f9f-135">Pour le développement d’applications Unity, consultez [barre de l’application sur des Toolkit-Unity de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html)</span><span class="sxs-lookup"><span data-stu-id="38f9f-135">For Unity app development, see [App bar on Mixed Reality Toolkit-Unity](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html)</span></span>

## <a name="see-also"></a><span data-ttu-id="38f9f-136">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="38f9f-136">See also</span></span>
* [<span data-ttu-id="38f9f-137">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="38f9f-137">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="38f9f-138">Texte dans Unity</span><span class="sxs-lookup"><span data-stu-id="38f9f-138">Text in Unity</span></span>](text-in-unity.md)
* [<span data-ttu-id="38f9f-139">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="38f9f-139">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="38f9f-140">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="38f9f-140">Displaying progress</span></span>](progress.md)
