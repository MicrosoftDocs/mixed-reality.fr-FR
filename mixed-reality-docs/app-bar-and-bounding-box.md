---
title: Cadre englobant et barre de l’application
description: La barre de l’application est un menu de niveau objet qui contient une série de boutons qui s’affichent sur le bord inférieur des limites d’un hologramme.
author: radicalad
ms.author: adlinv
ms.date: 06/07/2019
ms.topic: article
keywords: Windows Mixed Reality, barre d’application, cadre englobant
ms.openlocfilehash: f09187bc2a3969a8f844711052e15433f5449d6d
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437056"
---
# <a name="bounding-box-and-app-bar"></a><span data-ttu-id="c7162-104">Cadre englobant et barre de l’application</span><span class="sxs-lookup"><span data-stu-id="c7162-104">Bounding box and App bar</span></span>
![La délimitation est l’interface standard pour la manipulation d’objets en réalité mixte.](images/640px-boundingbox-hero.jpg)<br>

<br>

---

## <a name="what-is-the-bounding-box"></a><span data-ttu-id="c7162-106">Qu’est-ce que le cadre englobant ?</span><span class="sxs-lookup"><span data-stu-id="c7162-106">What is the Bounding box?</span></span>

<span data-ttu-id="c7162-107">La délimitation est l’interface standard pour la manipulation d’objets en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="c7162-107">Bounding is the standard interface for object manipulation in Mixed Reality.</span></span> <span data-ttu-id="c7162-108">Il permet à l’utilisateur de s’assurer que l’objet est actuellement réglable.</span><span class="sxs-lookup"><span data-stu-id="c7162-108">It provides the user an affordance that the object is currently adjustable.</span></span> <span data-ttu-id="c7162-109">Sur HoloLens 2, le cadre englobant fonctionne avec la manipulation directe de la main et répond à la proximité de l’utilisateur finger’s.</span><span class="sxs-lookup"><span data-stu-id="c7162-109">On HoloLens 2, the bounding box works with direct hand manipulation and responds to the user's finger's proximity.</span></span> <span data-ttu-id="c7162-110">Il affiche des commentaires visuels pour aider l’utilisateur à percevoir la distance par rapport à l’objet.</span><span class="sxs-lookup"><span data-stu-id="c7162-110">It shows visual feedback to help the user perceive the distance from the object.</span></span>

:::row:::
    :::column:::
        ### <a name="scaling-an-objectbr"></a><span data-ttu-id="c7162-111">Mise à l’échelle d’un objet</span><span class="sxs-lookup"><span data-stu-id="c7162-111">Scaling an object</span></span><br>
        <span data-ttu-id="c7162-112">Les angles du rectangle englobant indiquent à l’utilisateur que l’objet peut être mis à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="c7162-112">The corners of the bounding box tell the user that the object can scale.</span></span> <span data-ttu-id="c7162-113">Les poignées suivent un modèle largement compréhensible pour ajuster l’échelle.</span><span class="sxs-lookup"><span data-stu-id="c7162-113">The handles follow a widely understood pattern for adjusting scale.</span></span> <span data-ttu-id="c7162-114">Ce visuel offre aux utilisateurs la zone totale de l’objet, même s’ils ne sont pas visibles en dehors d’un mode de réglage.</span><span class="sxs-lookup"><span data-stu-id="c7162-114">This visual affordance shows users the total area of the object – even if it’s not visible outside of an adjustment mode.</span></span> <span data-ttu-id="c7162-115">Ceci est particulièrement important, car s’il n’y figure pas, un objet accroché à un autre objet ou surface peut sembler se comporter comme s’il existait un espace qui ne devrait pas y figurer.</span><span class="sxs-lookup"><span data-stu-id="c7162-115">This is especially important because if it weren’t there, an object snapped to another object or surface may appear to behave as if there was space around it that shouldn’t be there.</span></span><br>
        <br>
        <span data-ttu-id="c7162-116">*Boucle vidéo : mise à l’échelle d’un objet via un cadre englobant*</span><span class="sxs-lookup"><span data-stu-id="c7162-116">*Video loop: Scaling an object via bounding box*</span></span>
    :::column-end:::
        :::column:::
        <span data-ttu-id="c7162-117">espace de ![](images/spacer-20x582.png)</span><span class="sxs-lookup"><span data-stu-id="c7162-117">![space](images/spacer-20x582.png)</span></span><br>
       <span data-ttu-id="c7162-118">![point de vue HoloLens de la mise à l’échelle d’un objet via un cadre englobant](images/HoloLens2_BoundingBox.gif)</span><span class="sxs-lookup"><span data-stu-id="c7162-118">![HoloLens point-of-view of scaling an object via bounding box](images/HoloLens2_BoundingBox.gif)</span></span><br>
    :::column-end:::
:::row-end:::

<br>

:::row:::
    :::column:::
        ### <a name="rotating-an-objectbr"></a><span data-ttu-id="c7162-119">Rotation d’un objet</span><span class="sxs-lookup"><span data-stu-id="c7162-119">Rotating an object</span></span><br>
        <span data-ttu-id="c7162-120">Les intuitivité rectangulaires verticaux sur les bords du cadre englobant sont des indicateurs de rotation.</span><span class="sxs-lookup"><span data-stu-id="c7162-120">The vertical rectangular affordances on the edges of the bounding box are rotation indicators.</span></span> <span data-ttu-id="c7162-121">Cela permet à l’utilisateur d’effectuer des ajustements plus précis sur les hologrammes placés.</span><span class="sxs-lookup"><span data-stu-id="c7162-121">This gives the user more fine adjustment over their placed holograms.</span></span> <span data-ttu-id="c7162-122">Ils peuvent non seulement les ajuster et les mettre à l’échelle, mais également faire pivoter.</span><span class="sxs-lookup"><span data-stu-id="c7162-122">Not only can they adjust and scale, but now rotate as well.</span></span><br>
        <br>
        <span data-ttu-id="c7162-123">*Boucle vidéo : rotation d’un objet à l’aide du cadre englobant*</span><span class="sxs-lookup"><span data-stu-id="c7162-123">*Video loop: Rotating an object via bounding box*</span></span>
    :::column-end:::
        :::column:::
        <span data-ttu-id="c7162-124">espace de ![](images/spacer-20x582.png)</span><span class="sxs-lookup"><span data-stu-id="c7162-124">![space](images/spacer-20x582.png)</span></span><br>
       <span data-ttu-id="c7162-125">![point de vue HoloLens de la rotation d’un objet à l’aide d’un cadre englobant](images/HoloLens2_BoundingBox_Rotate.gif)</span><span class="sxs-lookup"><span data-stu-id="c7162-125">![HoloLens point-of-view of rotating an object via bounding box](images/HoloLens2_BoundingBox_Rotate.gif)</span></span><br>
    :::column-end:::
:::row-end:::

<br>

:::row:::
    :::column:::
        ### <a name="visual-feedback-on-hand-proximity-on-hololens-2br"></a><span data-ttu-id="c7162-126">Commentaires visuels sur la proximité de HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="c7162-126">Visual feedback on hand proximity on HoloLens 2</span></span><br>
        <span data-ttu-id="c7162-127">Sur HoloLens 2, il existe un signal visuel supplémentaire qui peut aider la perception de l’utilisateur en profondeur.</span><span class="sxs-lookup"><span data-stu-id="c7162-127">On HoloLens 2, there is an additional visual cue which can help the user's perception of depth.</span></span> <span data-ttu-id="c7162-128">Un anneau proche de son doigt s’affiche et s’adapte à mesure que l’approche est plus proche de l’objet.</span><span class="sxs-lookup"><span data-stu-id="c7162-128">A ring near their fingertip shows up and scales down as the fingertip gets closer to the object.</span></span> <span data-ttu-id="c7162-129">L’anneau se convergera en un point lorsque l’état appuyé est atteint.</span><span class="sxs-lookup"><span data-stu-id="c7162-129">The ring eventually converges into a dot when the pressed state is reached.</span></span> <span data-ttu-id="c7162-130">Cet accord visuel aide l’utilisateur à comprendre à quel moment il s’agit de l’objet.</span><span class="sxs-lookup"><span data-stu-id="c7162-130">This visual affordance helps the user understand how far they are from the object.</span></span><br>
        <br>
        <span data-ttu-id="c7162-131">*Boucle vidéo : exemple de retour visuel basé sur la proximité d’un cadre englobant*</span><span class="sxs-lookup"><span data-stu-id="c7162-131">*Video loop: Example of visual feedback based on proximity to a bounding box*</span></span>
    :::column-end:::
        :::column:::
        <span data-ttu-id="c7162-132">espace de ![](images/spacer-20x582.png)</span><span class="sxs-lookup"><span data-stu-id="c7162-132">![space](images/spacer-20x582.png)</span></span><br>
       <span data-ttu-id="c7162-133">![des commentaires visuels à proximité](images/HoloLens2_Proximity.gif)</span><span class="sxs-lookup"><span data-stu-id="c7162-133">![Visual feedback on hand proximity](images/HoloLens2_Proximity.gif)</span></span><br>
    :::column-end:::
:::row-end:::

<br>

<span data-ttu-id="c7162-134">**Pour le développement d’applications Unity, consultez [cadre englobant dans le Toolkit de réalité mixte-Unity.](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)**</span><span class="sxs-lookup"><span data-stu-id="c7162-134">**For Unity app development, see [Bounding box in the Mixed Reality Toolkit-Unity.](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)**</span></span>

<br>

---

## <a name="what-is-the-app-bar"></a><span data-ttu-id="c7162-135">Qu’est-ce que la barre d’application ?</span><span class="sxs-lookup"><span data-stu-id="c7162-135">What is the App bar?</span></span>

<span data-ttu-id="c7162-136">La barre de l’application est un menu de niveau objet qui contient une série de boutons qui s’affichent sur le bord inférieur des limites d’un hologramme.</span><span class="sxs-lookup"><span data-stu-id="c7162-136">The App bar is a object-level menu containing a series of buttons that displays on the bottom edge of a hologram's bounds.</span></span> <span data-ttu-id="c7162-137">Ce modèle est couramment utilisé pour permettre aux utilisateurs de supprimer et d’ajuster des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="c7162-137">This pattern is commonly used to give users the ability to remove and adjust holograms.</span></span> <span data-ttu-id="c7162-138">La barre de l’application a été conçue principalement comme un moyen de gérer les objets placés dans l’environnement d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c7162-138">The App bar was designed primarily as a way to manage placed objects in a user's environment.</span></span> <span data-ttu-id="c7162-139">Couplée avec le cadre englobant, un utilisateur dispose d’un contrôle total sur l’emplacement et la manière dont les objets sont orientés en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="c7162-139">Coupled with the bounding box, a user has full control over where and how objects are oriented in mixed reality.</span></span>

:::row:::
    :::column:::
        ### <a name="the-app-bar-follows-the-userbr"></a><span data-ttu-id="c7162-140">La barre de l’application suit l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="c7162-140">The App bar follows the user</span></span><br>
        <span data-ttu-id="c7162-141">Étant donné que ce modèle est utilisé avec les objets qui sont verrouillés au monde, lorsqu’un utilisateur se déplace autour de l’objet, la barre de l’application s’affichera toujours sur le côté objets le plus proche de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c7162-141">Since this pattern is used with objects that are world locked, as a user moves around the object the App bar will always display on the objects' side closest to the user.</span></span> <span data-ttu-id="c7162-142">Même si ce n’est pas le cas, il obtient le même résultat. empêcher la position d’un utilisateur pour occultait ou bloquer les fonctionnalités qui seraient autrement disponibles à partir d’un autre emplacement dans son environnement.</span><span class="sxs-lookup"><span data-stu-id="c7162-142">While this isn't billboarding, it effectively achieves the same result; preventing a user's position to occlude or block functionality that would otherwise be available from a different location in their environment.</span></span> <br>
        <br>
        <span data-ttu-id="c7162-143">*Boucle vidéo : à travers un hologramme, la barre de l’application suit*</span><span class="sxs-lookup"><span data-stu-id="c7162-143">*Video loop: Walking around a hologram, the App bar follows*</span></span>
    :::column-end:::
        :::column:::
        <span data-ttu-id="c7162-144">espace de ![](images/spacer-20x582.png)</span><span class="sxs-lookup"><span data-stu-id="c7162-144">![space](images/spacer-20x582.png)</span></span><br>
       <span data-ttu-id="c7162-145">![la marche autour d’un hologramme.</span><span class="sxs-lookup"><span data-stu-id="c7162-145">![Walking around a hologram.</span></span> <span data-ttu-id="c7162-146">La barre de l’application suit.](images/HoloLens2_AppBarFollowing.gif)</span><span class="sxs-lookup"><span data-stu-id="c7162-146">The App bar follows.](images/HoloLens2_AppBarFollowing.gif)</span></span><br>
    :::column-end:::
:::row-end:::

<br>



<span data-ttu-id="c7162-147">**Pour le développement d’applications Unity, consultez [la barre des applications dans le Toolkit de réalité mixte-Unity.](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html)**</span><span class="sxs-lookup"><span data-stu-id="c7162-147">**For Unity app development, see [App bar in the Mixed Reality Toolkit-Unity.](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html)**</span></span>

<br>

---

## <a name="see-also"></a><span data-ttu-id="c7162-148">Articles associés</span><span class="sxs-lookup"><span data-stu-id="c7162-148">See also</span></span>
* [<span data-ttu-id="c7162-149">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="c7162-149">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="c7162-150">Texte dans Unity</span><span class="sxs-lookup"><span data-stu-id="c7162-150">Text in Unity</span></span>](text-in-unity.md)
* [<span data-ttu-id="c7162-151">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="c7162-151">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="c7162-152">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="c7162-152">Displaying progress</span></span>](progress.md)
