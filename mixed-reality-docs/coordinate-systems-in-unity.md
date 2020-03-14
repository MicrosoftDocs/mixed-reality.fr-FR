---
title: Systèmes de coordonnées dans Unity
description: Découvrez comment créer des expériences de réalité mixte assiste, debout, à l’échelle de la place et à l’échelle mondiale dans Unity.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: système de coordonnées, système de coordonnées spatiales, orientation uniquement, à l’échelle assise, à l’échelle debout, à l’échelle de la pièce, à l’échelle mondiale, 360 de degrés, assis, debout, salle, monde, échelle, position, orientation, Unity, ancrage, ancrage spatial, ancrage universel, verrouillé, verrouillage universel, verrouillage du corps, verrouillage du corps, perte de suivi, localisation, limites, recentrer
ms.openlocfilehash: 36d74488b23587e5c89b40faf97921a10be7473b
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79375766"
---
# <a name="coordinate-systems-in-unity"></a><span data-ttu-id="f5370-104">Systèmes de coordonnées dans Unity</span><span class="sxs-lookup"><span data-stu-id="f5370-104">Coordinate systems in Unity</span></span>

<span data-ttu-id="f5370-105">Windows Mixed Reality prend en charge les applications à travers une large gamme d' [expériences](coordinate-systems.md), des applications en orientation seule et à l’échelle à l’échelle jusqu’à des applications à l’échelle de la place.</span><span class="sxs-lookup"><span data-stu-id="f5370-105">Windows Mixed Reality supports apps across a wide range of [experience scales](coordinate-systems.md), from orientation-only and seated-scale apps up through room-scale apps.</span></span> <span data-ttu-id="f5370-106">Sur HoloLens, vous pouvez aller plus loin et créer des applications à l’échelle mondiale qui permettent aux utilisateurs d’aller au-delà de 5 mètres, en explorant un étage entier d’un immeuble et au-delà.</span><span class="sxs-lookup"><span data-stu-id="f5370-106">On HoloLens, you can go further and build world-scale apps that let users walk beyond 5 meters, exploring an entire floor of a building and beyond.</span></span>

<span data-ttu-id="f5370-107">La première étape de la création d’une expérience de réalité mixte dans Unity consiste à déterminer la mise à l' [échelle](coordinate-systems.md) ciblée par votre application.</span><span class="sxs-lookup"><span data-stu-id="f5370-107">Your first step in building a mixed reality experience in Unity is to determine which [experience scale](coordinate-systems.md) your app will target.</span></span>

## <a name="building-an-orientation-only-or-seated-scale-experience"></a><span data-ttu-id="f5370-108">Création d’une expérience d’orientation seule ou de mise à l’échelle installée</span><span class="sxs-lookup"><span data-stu-id="f5370-108">Building an orientation-only or seated-scale experience</span></span>

<span data-ttu-id="f5370-109">**Espace de noms :** *UnityEngine. XR*</span><span class="sxs-lookup"><span data-stu-id="f5370-109">**Namespace:** *UnityEngine.XR*</span></span><br>
<span data-ttu-id="f5370-110">**Type :** *XRDevice*</span><span class="sxs-lookup"><span data-stu-id="f5370-110">**Type:** *XRDevice*</span></span>

<span data-ttu-id="f5370-111">Pour créer une expérience d' **orientation uniquement** ou de mise à l' **échelle assise**, vous devez définir Unity sur le type d’espace de suivi fixe.</span><span class="sxs-lookup"><span data-stu-id="f5370-111">To build an **orientation-only** or **seated-scale experience**, you must set Unity to the Stationary tracking space type.</span></span> <span data-ttu-id="f5370-112">Définit le système de coordonnées universelles de Unity pour suivre le [cadre stationnaire de référence](coordinate-systems.md#spatial-coordinate-systems).</span><span class="sxs-lookup"><span data-stu-id="f5370-112">This sets Unity's world coordinate system to track the [stationary frame of reference](coordinate-systems.md#spatial-coordinate-systems).</span></span> <span data-ttu-id="f5370-113">Dans le mode de suivi fixe, le contenu placé dans l’éditeur juste devant l’emplacement par défaut de l’appareil photo (Forward is-Z) s’affiche devant l’utilisateur au lancement de l’application.</span><span class="sxs-lookup"><span data-stu-id="f5370-113">In the Stationary tracking mode, content placed in the editor just in front of the camera's default location (forward is -Z) will appear in front of the user when the app launches.</span></span>

```cs
XRDevice.SetTrackingSpaceType(TrackingSpaceType.Stationary);
```

<span data-ttu-id="f5370-114">**Espace de noms :** *UnityEngine. XR*</span><span class="sxs-lookup"><span data-stu-id="f5370-114">**Namespace:** *UnityEngine.XR*</span></span><br>
<span data-ttu-id="f5370-115">**Type :** *InputTracking*</span><span class="sxs-lookup"><span data-stu-id="f5370-115">**Type:** *InputTracking*</span></span>

<span data-ttu-id="f5370-116">Pour une expérience purement en **orientation uniquement** telle qu’une visionneuse vidéo de 360 degrés (où les mises à jour de la tête de position dépasseraient l’illusion), vous pouvez définir [XR. InputTracking. disablePositionalTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking-disablePositionalTracking.html) sur true :</span><span class="sxs-lookup"><span data-stu-id="f5370-116">For a pure **orientation-only experience** such as a 360-degree video viewer (where positional head updates would ruin the illusion), you can then set [XR.InputTracking.disablePositionalTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking-disablePositionalTracking.html) to true:</span></span>

```cs
InputTracking.disablePositionalTracking = true;
```

<span data-ttu-id="f5370-117">Pour une expérience de mise à l' **échelle assiste**, pour permettre à l’utilisateur de recentrer plus tard l’origine assise, vous pouvez appeler [XR. Méthode InputTracking. recenter](https://docs.unity3d.com/ScriptReference/XR.InputTracking.Recenter.html) :</span><span class="sxs-lookup"><span data-stu-id="f5370-117">For a **seated-scale experience**, to let the user later recenter the seated origin, you can call the [XR.InputTracking.Recenter](https://docs.unity3d.com/ScriptReference/XR.InputTracking.Recenter.html) method:</span></span>

```cs
InputTracking.Recenter();
```

## <a name="building-a-standing-scale-or-room-scale-experience"></a><span data-ttu-id="f5370-118">Création d’une expérience de mise à l’échelle permanente ou à l’échelle de l’espace</span><span class="sxs-lookup"><span data-stu-id="f5370-118">Building a standing-scale or room-scale experience</span></span>

<span data-ttu-id="f5370-119">**Espace de noms :** *UnityEngine. XR*</span><span class="sxs-lookup"><span data-stu-id="f5370-119">**Namespace:** *UnityEngine.XR*</span></span><br>
<span data-ttu-id="f5370-120">**Type :** *XRDevice*</span><span class="sxs-lookup"><span data-stu-id="f5370-120">**Type:** *XRDevice*</span></span>

<span data-ttu-id="f5370-121">Pour une expérience à l’échelle **permanente** ou à l’échelle de l' **espace**, vous devez placer du contenu par rapport à l’étage.</span><span class="sxs-lookup"><span data-stu-id="f5370-121">For a **standing-scale** or **room-scale experience**, you'll need to place content relative to the floor.</span></span> <span data-ttu-id="f5370-122">Vous avez raison de l’étage de l’utilisateur à l’aide de la **[Phase spatiale](coordinate-systems.md#spatial-coordinate-systems)** , qui représente l’origine de l’utilisateur et la limite facultative de l’espace, configurées lors de la première exécution.</span><span class="sxs-lookup"><span data-stu-id="f5370-122">You reason about the user's floor using the **[spatial stage](coordinate-systems.md#spatial-coordinate-systems)**, which represents the user's defined floor-level origin and optional room boundary, set up during first run.</span></span>

<span data-ttu-id="f5370-123">Pour vous assurer que Unity fonctionne avec son système de coordonnées universel à l’étage, vous pouvez définir Unity sur le type d’espace de suivi RoomScale et vérifier que le jeu est correctement effectué :</span><span class="sxs-lookup"><span data-stu-id="f5370-123">To ensure that Unity is operating with its world coordinate system at floor-level, you can set Unity to the RoomScale tracking space type, and ensure that the set succeeds:</span></span>

```cs
if (XRDevice.SetTrackingSpaceType(TrackingSpaceType.RoomScale))
{
    // RoomScale mode was set successfully.  App can now assume that y=0 in Unity world coordinate represents the floor.
}
else
{
    // RoomScale mode was not set successfully.  App cannot make assumptions about where the floor plane is.
}
```
* <span data-ttu-id="f5370-124">Si SetTrackingSpaceType retourne la valeur true, Unity a correctement basculé son système de coordonnées universel pour suivre le [cadre de la phase de référence](coordinate-systems.md#spatial-coordinate-systems).</span><span class="sxs-lookup"><span data-stu-id="f5370-124">If SetTrackingSpaceType returns true, Unity has successfully switched its world coordinate system to track the [stage frame of reference](coordinate-systems.md#spatial-coordinate-systems).</span></span>
* <span data-ttu-id="f5370-125">Si SetTrackingSpaceType retourne la valeur false, Unity n’a pas pu basculer vers le cadre de la phase de référence, ce qui est probablement dû au fait que l’utilisateur n’a pas configuré un étage dans son environnement.</span><span class="sxs-lookup"><span data-stu-id="f5370-125">If SetTrackingSpaceType returns false, Unity was unable to switch to the stage frame of reference, likely because the user has not set up even a floor in their environment.</span></span> <span data-ttu-id="f5370-126">Ce n’est pas courant, mais cela peut se produire si l’étape a été configurée dans une autre salle et que l’appareil a été déplacé dans la salle active sans que l’utilisateur n’ait configuré une nouvelle phase.</span><span class="sxs-lookup"><span data-stu-id="f5370-126">This is not common, but can happen if the stage was set up in a different room and the device was moved to the current room without the user setting up a new stage.</span></span>

<span data-ttu-id="f5370-127">Une fois que votre application a correctement défini le type d’espace de suivi RoomScale, le contenu placé sur le plan y = 0 s’affiche sur le plancher.</span><span class="sxs-lookup"><span data-stu-id="f5370-127">Once your app successfully sets the RoomScale tracking space type, content placed on the y=0 plane will appear on the floor.</span></span> <span data-ttu-id="f5370-128">L’origine à (0, 0, 0) sera l’emplacement spécifique sur le plancher où l’utilisateur a pris la main pendant la configuration de la salle, avec-Z représentant la direction vers l’avant au cours de l’installation.</span><span class="sxs-lookup"><span data-stu-id="f5370-128">The origin at (0, 0, 0) will be the specific place on the floor where the user stood during room setup, with -Z representing the forward direction they were facing during setup.</span></span>

<span data-ttu-id="f5370-129">**Espace de noms :** *UnityEngine. expérimentale. XR*</span><span class="sxs-lookup"><span data-stu-id="f5370-129">**Namespace:** *UnityEngine.Experimental.XR*</span></span><br>
<span data-ttu-id="f5370-130">**Type :** *limite*</span><span class="sxs-lookup"><span data-stu-id="f5370-130">**Type:** *Boundary*</span></span>

<span data-ttu-id="f5370-131">Dans le code de script, vous pouvez ensuite appeler la méthode TryGetGeometry sur vous êtes le type UnityEngine. expérimental. XR. Boundary pour obtenir un polygone de limite, en spécifiant un type de limite de TrackedArea.</span><span class="sxs-lookup"><span data-stu-id="f5370-131">In script code, you can then call the TryGetGeometry method on your the UnityEngine.Experimental.XR.Boundary type to get a boundary polygon, specifying a boundary type of TrackedArea.</span></span> <span data-ttu-id="f5370-132">Si l’utilisateur a défini une limite (vous récupérez une liste de vertex), vous savez qu’il est possible de fournir une expérience de mise à l’échelle de l' **espace** à l’utilisateur, où il peut se déplacer dans la scène que vous créez.</span><span class="sxs-lookup"><span data-stu-id="f5370-132">If the user defined a boundary (you get back a list of vertices), you know it is safe to deliver a **room-scale experience** to the user, where they can walk around the scene you create.</span></span>

<span data-ttu-id="f5370-133">Notez que le système affiche automatiquement la limite lorsque l’utilisateur l’approche.</span><span class="sxs-lookup"><span data-stu-id="f5370-133">Note that the system will automatically render the boundary when the user approaches it.</span></span> <span data-ttu-id="f5370-134">Votre application n’a pas besoin d’utiliser ce polygone pour restituer la limite elle-même.</span><span class="sxs-lookup"><span data-stu-id="f5370-134">Your app does not need to use this polygon to render the boundary itself.</span></span> <span data-ttu-id="f5370-135">Toutefois, vous pouvez choisir de disposer vos objets de scène à l’aide de ce polygone limite pour vous assurer que l’utilisateur peut atteindre physiquement ces objets sans téléportage :</span><span class="sxs-lookup"><span data-stu-id="f5370-135">However, you may choose to lay out your scene objects using this boundary polygon, to ensure the user can physically reach those objects without teleporting:</span></span>

```cs
var vertices = new List<Vector3>();
if (UnityEngine.Experimental.XR.Boundary.TryGetGeometry(vertices, Boundary.Type.TrackedArea))
{
    // Lay out your app's content within the boundary polygon, to ensure that users can reach it without teleporting.
}
```

## <a name="building-a-world-scale-experience"></a><span data-ttu-id="f5370-136">Création d’une expérience à l’échelle mondiale</span><span class="sxs-lookup"><span data-stu-id="f5370-136">Building a world-scale experience</span></span>

<span data-ttu-id="f5370-137">**Espace de noms :** *UnityEngine. XR. WSA*</span><span class="sxs-lookup"><span data-stu-id="f5370-137">**Namespace:** *UnityEngine.XR.WSA*</span></span><br>
<span data-ttu-id="f5370-138">**Type :** *WorldAnchor*</span><span class="sxs-lookup"><span data-stu-id="f5370-138">**Type:** *WorldAnchor*</span></span>

<span data-ttu-id="f5370-139">Pour les expériences réelles à l' **échelle mondiale** sur HoloLens qui permettent aux utilisateurs d’aller au-delà de 5 mètres, vous aurez besoin de nouvelles techniques au-delà de celles utilisées pour les expériences à l’échelle de la place.</span><span class="sxs-lookup"><span data-stu-id="f5370-139">For true **world-scale experiences** on HoloLens that let users wander beyond 5 meters, you'll need new techniques beyond those used for room-scale experiences.</span></span> <span data-ttu-id="f5370-140">Une technique clé que vous allez utiliser consiste à créer une [ancre spatiale](coordinate-systems.md#spatial-anchors) pour verrouiller un cluster d’hologrammes précisément en place dans le monde physique, quelle que soit la durée d’itinérance de l’utilisateur, puis [retrouvez ces hologrammes dans les sessions ultérieures](coordinate-systems.md#spatial-anchor-persistence).</span><span class="sxs-lookup"><span data-stu-id="f5370-140">One key technique you'll use is to create a [spatial anchor](coordinate-systems.md#spatial-anchors) to lock a cluster of holograms precisely in place in the physical world, regardless of how far the user has roamed, and then [find those holograms again in later sessions](coordinate-systems.md#spatial-anchor-persistence).</span></span>

<span data-ttu-id="f5370-141">Dans Unity, vous créez une ancre spatiale en ajoutant le composant **WorldAnchor** Unity à un GameObject.</span><span class="sxs-lookup"><span data-stu-id="f5370-141">In Unity, you create a spatial anchor by adding the **WorldAnchor** Unity component to a GameObject.</span></span>

### <a name="adding-a-world-anchor"></a><span data-ttu-id="f5370-142">Ajout d’une ancre mondiale</span><span class="sxs-lookup"><span data-stu-id="f5370-142">Adding a World Anchor</span></span>

<span data-ttu-id="f5370-143">Pour ajouter une ancre universelle, appelez AddComponent<WorldAnchor>() sur l’objet de jeu avec la transformation que vous souhaitez ancrer dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="f5370-143">To add a world anchor, call AddComponent<WorldAnchor>() on the game object with the transform you want to anchor in the real world.</span></span>

```cs
WorldAnchor anchor = gameObject.AddComponent<WorldAnchor>();
```

<span data-ttu-id="f5370-144">C’est tout !</span><span class="sxs-lookup"><span data-stu-id="f5370-144">That's it!</span></span> <span data-ttu-id="f5370-145">Cet objet de jeu sera désormais ancré à son emplacement actuel dans le monde physique : vous pouvez constater que ses coordonnées universelles s’ajustent légèrement au fil du temps pour garantir l’alignement physique.</span><span class="sxs-lookup"><span data-stu-id="f5370-145">This game object will now be anchored to its current location in the physical world - you may see its Unity world coordinates adjust slightly over time to ensure that physical alignment.</span></span> <span data-ttu-id="f5370-146">Utilisez la [persistance](persistence-in-unity.md) pour rechercher à nouveau cet emplacement d’ancrage dans une session d’application future.</span><span class="sxs-lookup"><span data-stu-id="f5370-146">Use [persistence](persistence-in-unity.md) to find this anchored location again in a future app session.</span></span>

### <a name="removing-a-world-anchor"></a><span data-ttu-id="f5370-147">Suppression d’une ancre mondiale</span><span class="sxs-lookup"><span data-stu-id="f5370-147">Removing a World Anchor</span></span>

<span data-ttu-id="f5370-148">Si vous ne souhaitez plus que les GameObject soient verrouillés sur un emplacement géographique physique et que vous n’envisagez pas de déplacer ce cadre, vous pouvez simplement appeler Destroy sur le composant d’ancrage du monde.</span><span class="sxs-lookup"><span data-stu-id="f5370-148">If you no longer want the GameObject locked to a physical world location and don't intend on moving it this frame, then you can just call Destroy on the World Anchor component.</span></span>

```cs
Destroy(gameObject.GetComponent<WorldAnchor>());
```

<span data-ttu-id="f5370-149">Si vous souhaitez déplacer le GameObject ce frame, vous devez appeler DestroyImmediate à la place.</span><span class="sxs-lookup"><span data-stu-id="f5370-149">If you want to move the GameObject this frame, you need to call DestroyImmediate instead.</span></span>

```cs
DestroyImmediate(gameObject.GetComponent<WorldAnchor>());
```

### <a name="moving-a-world-anchored-gameobject"></a><span data-ttu-id="f5370-150">Déplacement d’un GameObject ancré dans le monde</span><span class="sxs-lookup"><span data-stu-id="f5370-150">Moving a World Anchored GameObject</span></span>

<span data-ttu-id="f5370-151">Les GameObject ne peuvent pas être déplacées pendant qu’une ancre mondiale y est.</span><span class="sxs-lookup"><span data-stu-id="f5370-151">GameObject's cannot be moved while a World Anchor is on it.</span></span> <span data-ttu-id="f5370-152">Si vous devez déplacer le GameObject ce frame, vous devez :</span><span class="sxs-lookup"><span data-stu-id="f5370-152">If you need to move the GameObject this frame, you need to:</span></span>
1. <span data-ttu-id="f5370-153">DestroyImmediate le composant d’ancrage universel</span><span class="sxs-lookup"><span data-stu-id="f5370-153">DestroyImmediate the World Anchor component</span></span>
2. <span data-ttu-id="f5370-154">Déplacer le GameObject</span><span class="sxs-lookup"><span data-stu-id="f5370-154">Move the GameObject</span></span>
3. <span data-ttu-id="f5370-155">Ajoutez un nouveau composant d’ancrage du monde au GameObject.</span><span class="sxs-lookup"><span data-stu-id="f5370-155">Add a new World Anchor component to the GameObject.</span></span>

```cs
DestroyImmediate(gameObject.GetComponent<WorldAnchor>());
gameObject.transform.position = new Vector3(0, 0, 2);
WorldAnchor anchor = gameObject.AddComponent<WorldAnchor>();
```

### <a name="handling-locatability-changes"></a><span data-ttu-id="f5370-156">Gestion des modifications de localisabilité</span><span class="sxs-lookup"><span data-stu-id="f5370-156">Handling Locatability Changes</span></span>

<span data-ttu-id="f5370-157">Un WorldAnchor peut ne pas être localisable dans le monde physique à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="f5370-157">A WorldAnchor may not be locatable in the physical world at a point in time.</span></span> <span data-ttu-id="f5370-158">Si cela se produit, Unity ne met pas à jour la transformation de l’objet ancré.</span><span class="sxs-lookup"><span data-stu-id="f5370-158">If that occurs, Unity will not be updating the transform of the anchored object.</span></span> <span data-ttu-id="f5370-159">Cela peut également changer pendant l’exécution d’une application.</span><span class="sxs-lookup"><span data-stu-id="f5370-159">This also can change while an app is running.</span></span> <span data-ttu-id="f5370-160">Si la modification de la localisation n’est pas prise en charge, l’objet n’apparaîtra pas à l’emplacement physique approprié dans le monde.</span><span class="sxs-lookup"><span data-stu-id="f5370-160">Failure to handle the change in locatability will cause the object to not appear in the correct physical location in the world.</span></span>

<span data-ttu-id="f5370-161">Pour être informé des changements de localisation :</span><span class="sxs-lookup"><span data-stu-id="f5370-161">To be notified about locatability changes:</span></span>
1. <span data-ttu-id="f5370-162">S’abonner à l’événement OnTrackingChanged</span><span class="sxs-lookup"><span data-stu-id="f5370-162">Subscribe to the OnTrackingChanged event</span></span>
2. <span data-ttu-id="f5370-163">Gérer l’événement</span><span class="sxs-lookup"><span data-stu-id="f5370-163">Handle the event</span></span>

<span data-ttu-id="f5370-164">L’événement **OnTrackingChanged** est appelé chaque fois que l’ancrage spatial sous-jacent change entre un État localisable et n’est pas localisable.</span><span class="sxs-lookup"><span data-stu-id="f5370-164">The **OnTrackingChanged** event will be called whenever the underlying spatial anchor changes between a state of being locatable vs. not being locatable.</span></span>

```cs
anchor.OnTrackingChanged += Anchor_OnTrackingChanged;
```

<span data-ttu-id="f5370-165">Ensuite, gérez l’événement :</span><span class="sxs-lookup"><span data-stu-id="f5370-165">Then handle the event:</span></span>

```cs
private void Anchor_OnTrackingChanged(WorldAnchor self, bool located)
{
    // This simply activates/deactivates this object and all children when tracking changes
    self.gameObject.SetActiveRecursively(located);
}
```

<span data-ttu-id="f5370-166">Parfois, les ancres se trouvent immédiatement.</span><span class="sxs-lookup"><span data-stu-id="f5370-166">Sometimes anchors are located immediately.</span></span> <span data-ttu-id="f5370-167">Dans ce cas, cette propriété isLocated de l’ancre sera définie sur true lorsque AddComponent<WorldAnchor>() retourne.</span><span class="sxs-lookup"><span data-stu-id="f5370-167">In this case, this isLocated property of the anchor will be set to true when AddComponent<WorldAnchor>() returns.</span></span> <span data-ttu-id="f5370-168">Par conséquent, l’événement OnTrackingChanged n’est pas déclenché.</span><span class="sxs-lookup"><span data-stu-id="f5370-168">As a result, the OnTrackingChanged event will not be triggered.</span></span> <span data-ttu-id="f5370-169">Un modèle propre serait d’appeler votre gestionnaire OnTrackingChanged avec l’état initial de IsLocated après avoir attaché une ancre.</span><span class="sxs-lookup"><span data-stu-id="f5370-169">A clean pattern would be to call your OnTrackingChanged handler with the initial IsLocated state after attaching an anchor.</span></span>

```cs
Anchor_OnTrackingChanged(anchor, anchor.isLocated);
```

## <a name="sharing-anchors-across-devices"></a><span data-ttu-id="f5370-170">Partage d’ancres sur plusieurs appareils</span><span class="sxs-lookup"><span data-stu-id="f5370-170">Sharing anchors across devices</span></span>

<span data-ttu-id="f5370-171">Vous pouvez utiliser des <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres spatiales Azure</a> pour créer une ancre Cloud durable à partir d’un WorldAnchor local, que votre application peut ensuite localiser sur plusieurs appareils HoloLens, iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="f5370-171">You can use <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a> to create a durable cloud anchor from a local WorldAnchor, which your app can then locate across multiple HoloLens, iOS and Android devices.</span></span>  <span data-ttu-id="f5370-172">En partageant une ancre spatiale commune sur plusieurs appareils, chaque utilisateur peut voir le contenu affiché par rapport à cette ancre dans le même emplacement physique.</span><span class="sxs-lookup"><span data-stu-id="f5370-172">By sharing a common spatial anchor across multiple devices, each user can see content rendered relative to that anchor in the same physical location.</span></span>  <span data-ttu-id="f5370-173">Cette technique autorise les expériences partagées en temps réel.</span><span class="sxs-lookup"><span data-stu-id="f5370-173">This allows for real-time shared experiences.</span></span>

<span data-ttu-id="f5370-174">Pour commencer à créer des expériences partagées dans Unity, essayez les Démarrages rapides de 5 minutes d' <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Unity spatiales Azure Unity</a>.</span><span class="sxs-lookup"><span data-stu-id="f5370-174">To get started building shared experiences in Unity, try out the 5-minute <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Azure Spatial Anchors Unity quickstarts</a>.</span></span>

<span data-ttu-id="f5370-175">Une fois que vous êtes opérationnel avec les ancres spatiales Azure, vous pouvez <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">créer et localiser des ancres dans Unity</a>.</span><span class="sxs-lookup"><span data-stu-id="f5370-175">Once you're up and running with Azure Spatial Anchors, you can then <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">create and locate anchors in Unity</a>.</span></span>

## <a name="see-also"></a><span data-ttu-id="f5370-176">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f5370-176">See Also</span></span>
* [<span data-ttu-id="f5370-177">Échelle de l’expérience</span><span class="sxs-lookup"><span data-stu-id="f5370-177">Experience scales</span></span>](coordinate-systems.md#mixed-reality-experience-scales)
* [<span data-ttu-id="f5370-178">Étape spatiale</span><span class="sxs-lookup"><span data-stu-id="f5370-178">Spatial stage</span></span>](coordinate-systems.md#stage-frame-of-reference)
* [<span data-ttu-id="f5370-179">Suivi des pertes dans Unity</span><span class="sxs-lookup"><span data-stu-id="f5370-179">Tracking loss in Unity</span></span>](tracking-loss-in-unity.md)
* [<span data-ttu-id="f5370-180">Ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="f5370-180">Spatial anchors</span></span>](spatial-anchors.md)
* [<span data-ttu-id="f5370-181">Persistance dans Unity</span><span class="sxs-lookup"><span data-stu-id="f5370-181">Persistence in Unity</span></span>](persistence-in-unity.md)
* [<span data-ttu-id="f5370-182">Expériences partagées dans Unity</span><span class="sxs-lookup"><span data-stu-id="f5370-182">Shared experiences in Unity</span></span>](shared-experiences-in-unity.md)
* <span data-ttu-id="f5370-183"><a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a></span><span class="sxs-lookup"><span data-stu-id="f5370-183"><a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a></span></span>
* <span data-ttu-id="f5370-184"><a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Kit de développement logiciel (SDK) d’ancre spatiale Azure pour Unity</a></span><span class="sxs-lookup"><span data-stu-id="f5370-184"><a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Azure Spatial Anchors SDK for Unity</a></span></span>