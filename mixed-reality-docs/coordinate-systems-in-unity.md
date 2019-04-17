---
title: Systèmes de coordonnées dans Unity
description: Apprenez à créer assis, permanent, salle à l’échelle et à l’échelle du monde mixte réalité des expériences dans Unity.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: système de coordonnées, système de coordonnées spatial, orientation, à l’échelle en place et seule permanent à l’échelle, salle à l’échelle, mise à l’échelle mondiale, assis à 360 degrés, debout, salle, monde, à l’échelle, position, orientation, Unity, ancre, spatiale d’ancrage, ancre world, world-verrouillé, verrouillage de monde, body-verrouillée, corps de verrouillage, suivi de perte, locatability, limites, recentrer
ms.openlocfilehash: 36d74488b23587e5c89b40faf97921a10be7473b
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597105"
---
# <a name="coordinate-systems-in-unity"></a><span data-ttu-id="10432-104">Systèmes de coordonnées dans Unity</span><span class="sxs-lookup"><span data-stu-id="10432-104">Coordinate systems in Unity</span></span>

<span data-ttu-id="10432-105">Réalité mixte Windows prend en charge les applications sur une large gamme de [expérience échelles](coordinate-systems.md), à partir d’applications orientation uniquement et à l’échelle en place des via des applications à l’échelle de salle.</span><span class="sxs-lookup"><span data-stu-id="10432-105">Windows Mixed Reality supports apps across a wide range of [experience scales](coordinate-systems.md), from orientation-only and seated-scale apps up through room-scale apps.</span></span> <span data-ttu-id="10432-106">Sur HoloLens, vous pouvez aller plus loin et créer des applications à l’échelle mondiale qui permettent aux utilisateurs de parcourir au-delà de 5 mètres, explorant un étage entier d’un bâtiment et au-delà.</span><span class="sxs-lookup"><span data-stu-id="10432-106">On HoloLens, you can go further and build world-scale apps that let users walk beyond 5 meters, exploring an entire floor of a building and beyond.</span></span>

<span data-ttu-id="10432-107">Votre première étape dans la création d’une expérience de réalité mixte dans Unity consiste à déterminer quel [expérience mise à l’échelle](coordinate-systems.md) votre application ciblera.</span><span class="sxs-lookup"><span data-stu-id="10432-107">Your first step in building a mixed reality experience in Unity is to determine which [experience scale](coordinate-systems.md) your app will target.</span></span>

## <a name="building-an-orientation-only-or-seated-scale-experience"></a><span data-ttu-id="10432-108">Création d’une expérience de l’orientation uniquement ou à l’échelle en place</span><span class="sxs-lookup"><span data-stu-id="10432-108">Building an orientation-only or seated-scale experience</span></span>

<span data-ttu-id="10432-109">**Namespace :** *UnityEngine.XR*</span><span class="sxs-lookup"><span data-stu-id="10432-109">**Namespace:** *UnityEngine.XR*</span></span><br>
<span data-ttu-id="10432-110">**Type :** *XRDevice*</span><span class="sxs-lookup"><span data-stu-id="10432-110">**Type:** *XRDevice*</span></span>

<span data-ttu-id="10432-111">Pour générer un **orientation seule** ou **assis à l’échelle du expérience**, vous devez définir Unity à l’arrêt suivi du type d’espace.</span><span class="sxs-lookup"><span data-stu-id="10432-111">To build an **orientation-only** or **seated-scale experience**, you must set Unity to the Stationary tracking space type.</span></span> <span data-ttu-id="10432-112">Cela définit le système de coordonnées de monde d’Unity pour suivre le [de référence stationnaire](coordinate-systems.md#spatial-coordinate-systems).</span><span class="sxs-lookup"><span data-stu-id="10432-112">This sets Unity's world coordinate system to track the [stationary frame of reference](coordinate-systems.md#spatial-coordinate-systems).</span></span> <span data-ttu-id="10432-113">Dans le mode de suivi stationnaire, contenu placé dans l’éditeur juste devant l’emplacement par défaut de l’appareil photo (-Z est vers l’avant) apparaît devant l’utilisateur quand l’application démarre.</span><span class="sxs-lookup"><span data-stu-id="10432-113">In the Stationary tracking mode, content placed in the editor just in front of the camera's default location (forward is -Z) will appear in front of the user when the app launches.</span></span>

```cs
XRDevice.SetTrackingSpaceType(TrackingSpaceType.Stationary);
```

<span data-ttu-id="10432-114">**Namespace :** *UnityEngine.XR*</span><span class="sxs-lookup"><span data-stu-id="10432-114">**Namespace:** *UnityEngine.XR*</span></span><br>
<span data-ttu-id="10432-115">**Type :** *InputTracking*</span><span class="sxs-lookup"><span data-stu-id="10432-115">**Type:** *InputTracking*</span></span>

<span data-ttu-id="10432-116">Pour une pure **orientation seule expérience** tels que l’Observateur de vidéo à 360 degrés (où les mises à jour principal positionnels seraient endommager l’illusion), vous pouvez ensuite définir [XR. InputTracking.disablePositionalTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking-disablePositionalTracking.html) sur true :</span><span class="sxs-lookup"><span data-stu-id="10432-116">For a pure **orientation-only experience** such as a 360-degree video viewer (where positional head updates would ruin the illusion), you can then set [XR.InputTracking.disablePositionalTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking-disablePositionalTracking.html) to true:</span></span>

```cs
InputTracking.disablePositionalTracking = true;
```

<span data-ttu-id="10432-117">Pour un **assis à l’échelle du expérience**, pour permettre à l’utilisateur plus tard recentrer l’origine assis, vous pouvez appeler la [XR. InputTracking.Recenter](https://docs.unity3d.com/ScriptReference/XR.InputTracking.Recenter.html) méthode :</span><span class="sxs-lookup"><span data-stu-id="10432-117">For a **seated-scale experience**, to let the user later recenter the seated origin, you can call the [XR.InputTracking.Recenter](https://docs.unity3d.com/ScriptReference/XR.InputTracking.Recenter.html) method:</span></span>

```cs
InputTracking.Recenter();
```

## <a name="building-a-standing-scale-or-room-scale-experience"></a><span data-ttu-id="10432-118">Création d’une expérience permanent à l’échelle ou d’échelle de la salle</span><span class="sxs-lookup"><span data-stu-id="10432-118">Building a standing-scale or room-scale experience</span></span>

<span data-ttu-id="10432-119">**Namespace :** *UnityEngine.XR*</span><span class="sxs-lookup"><span data-stu-id="10432-119">**Namespace:** *UnityEngine.XR*</span></span><br>
<span data-ttu-id="10432-120">**Type :** *XRDevice*</span><span class="sxs-lookup"><span data-stu-id="10432-120">**Type:** *XRDevice*</span></span>

<span data-ttu-id="10432-121">Pour un **permanent à l’échelle** ou **expérience de l’échelle de la salle**, vous devez placer le contenu relatif à l’étage.</span><span class="sxs-lookup"><span data-stu-id="10432-121">For a **standing-scale** or **room-scale experience**, you'll need to place content relative to the floor.</span></span> <span data-ttu-id="10432-122">Sur l’utilisateur de la raison floor, à l’aide de la  **[étape spatial](coordinate-systems.md#spatial-coordinate-systems)**, qui représente l’utilisateur défini au niveau du sol origine et les limites de salle facultatif, définissez au cours de première exécution.</span><span class="sxs-lookup"><span data-stu-id="10432-122">You reason about the user's floor using the **[spatial stage](coordinate-systems.md#spatial-coordinate-systems)**, which represents the user's defined floor-level origin and optional room boundary, set up during first run.</span></span>

<span data-ttu-id="10432-123">Pour vous assurer que Unity fonctionne avec son système de coordonnées de monde au niveau du sol, vous pouvez définir que Unity pour le suivi du type de l’espace de RoomScale et vous assurer que le jeu réussit :</span><span class="sxs-lookup"><span data-stu-id="10432-123">To ensure that Unity is operating with its world coordinate system at floor-level, you can set Unity to the RoomScale tracking space type, and ensure that the set succeeds:</span></span>

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
* <span data-ttu-id="10432-124">Si SetTrackingSpaceType retourne la valeur true, Unity a basculé correctement son système de coordonnées de monde pour suivre le [phase de référence](coordinate-systems.md#spatial-coordinate-systems).</span><span class="sxs-lookup"><span data-stu-id="10432-124">If SetTrackingSpaceType returns true, Unity has successfully switched its world coordinate system to track the [stage frame of reference](coordinate-systems.md#spatial-coordinate-systems).</span></span>
* <span data-ttu-id="10432-125">Si SetTrackingSpaceType retourne la valeur false, Unity a été impossible de passer du stade cadre de référence, probablement parce que l’utilisateur n’a pas configuré de même un étage dans leur environnement.</span><span class="sxs-lookup"><span data-stu-id="10432-125">If SetTrackingSpaceType returns false, Unity was unable to switch to the stage frame of reference, likely because the user has not set up even a floor in their environment.</span></span> <span data-ttu-id="10432-126">Cela n’est pas courant, mais peut se produire si l’étape a été configurée dans une autre pièce et que l’appareil a été déplacé vers la salle sans le paramètre de l’utilisateur d’une nouvelle étape.</span><span class="sxs-lookup"><span data-stu-id="10432-126">This is not common, but can happen if the stage was set up in a different room and the device was moved to the current room without the user setting up a new stage.</span></span>

<span data-ttu-id="10432-127">Une fois que votre application définit correctement le RoomScale suivi de type d’espace, contenu placé sur la y = 0 plan s’affiche sur le sol.</span><span class="sxs-lookup"><span data-stu-id="10432-127">Once your app successfully sets the RoomScale tracking space type, content placed on the y=0 plane will appear on the floor.</span></span> <span data-ttu-id="10432-128">L’origine (0, 0, 0) sera l’emplacement spécifique sur le lieu où l’utilisateur a su résister pendant l’installation de la salle, avec -Z qui représente la direction avant qu’ils ont été confrontés pendant l’installation.</span><span class="sxs-lookup"><span data-stu-id="10432-128">The origin at (0, 0, 0) will be the specific place on the floor where the user stood during room setup, with -Z representing the forward direction they were facing during setup.</span></span>

<span data-ttu-id="10432-129">**Namespace :** *UnityEngine.Experimental.XR*</span><span class="sxs-lookup"><span data-stu-id="10432-129">**Namespace:** *UnityEngine.Experimental.XR*</span></span><br>
<span data-ttu-id="10432-130">**Type :** *Limites*</span><span class="sxs-lookup"><span data-stu-id="10432-130">**Type:** *Boundary*</span></span>

<span data-ttu-id="10432-131">Dans le code de script, vous pouvez, puis appelez la méthode TryGetGeometry vous êtes du genre à UnityEngine.Experimental.XR.Boundary pour obtenir un polygone de la limite, en spécifiant un type de limite de TrackedArea.</span><span class="sxs-lookup"><span data-stu-id="10432-131">In script code, you can then call the TryGetGeometry method on your the UnityEngine.Experimental.XR.Boundary type to get a boundary polygon, specifying a boundary type of TrackedArea.</span></span> <span data-ttu-id="10432-132">Si l’utilisateur défini une limite (vous obtenez une liste de sommets), vous savez qu’il fournir un **expérience de l’échelle de la salle** à l’utilisateur, où ils peuvent la scène vous guider créer.</span><span class="sxs-lookup"><span data-stu-id="10432-132">If the user defined a boundary (you get back a list of vertices), you know it is safe to deliver a **room-scale experience** to the user, where they can walk around the scene you create.</span></span>

<span data-ttu-id="10432-133">Notez que le système affiche automatiquement la limite lors de l’utilisateur à l’approche.</span><span class="sxs-lookup"><span data-stu-id="10432-133">Note that the system will automatically render the boundary when the user approaches it.</span></span> <span data-ttu-id="10432-134">Votre application n’a pas besoin d’utiliser ce polygone pour restituer la limite de lui-même.</span><span class="sxs-lookup"><span data-stu-id="10432-134">Your app does not need to use this polygon to render the boundary itself.</span></span> <span data-ttu-id="10432-135">Toutefois, vous pouvez choisir de disposer de vos objets de scène à l’aide de ce polygone limite, pour vous assurer de que l’utilisateur peut atteindre physiquement ces objets sans teleporting :</span><span class="sxs-lookup"><span data-stu-id="10432-135">However, you may choose to lay out your scene objects using this boundary polygon, to ensure the user can physically reach those objects without teleporting:</span></span>

```cs
var vertices = new List<Vector3>();
if (UnityEngine.Experimental.XR.Boundary.TryGetGeometry(vertices, Boundary.Type.TrackedArea))
{
    // Lay out your app's content within the boundary polygon, to ensure that users can reach it without teleporting.
}
```

## <a name="building-a-world-scale-experience"></a><span data-ttu-id="10432-136">Création d’une expérience à l’échelle mondiale</span><span class="sxs-lookup"><span data-stu-id="10432-136">Building a world-scale experience</span></span>

<span data-ttu-id="10432-137">**Namespace :** *UnityEngine.XR.WSA*</span><span class="sxs-lookup"><span data-stu-id="10432-137">**Namespace:** *UnityEngine.XR.WSA*</span></span><br>
<span data-ttu-id="10432-138">**Type :** *WorldAnchor*</span><span class="sxs-lookup"><span data-stu-id="10432-138">**Type:** *WorldAnchor*</span></span>

<span data-ttu-id="10432-139">Pour true **expériences à l’échelle du monde** sur HoloLens qui permettent aux utilisateurs de plate-formes au-delà de 5 mètres, vous devez disposer des nouvelles techniques au-delà de celles utilisées pour les expériences de l’échelle de la salle.</span><span class="sxs-lookup"><span data-stu-id="10432-139">For true **world-scale experiences** on HoloLens that let users wander beyond 5 meters, you'll need new techniques beyond those used for room-scale experiences.</span></span> <span data-ttu-id="10432-140">Une technique clé que vous utiliserez consiste à créer un [ancre spatial](coordinate-systems.md#spatial-anchors) pour verrouiller un cluster de hologrammes précisément en place dans le monde physique, quelle que soit la distance, l’utilisateur est déplacé, puis [suite de retrouver ces hologrammes à nouveau dans sessions](coordinate-systems.md#spatial-anchor-persistence).</span><span class="sxs-lookup"><span data-stu-id="10432-140">One key technique you'll use is to create a [spatial anchor](coordinate-systems.md#spatial-anchors) to lock a cluster of holograms precisely in place in the physical world, regardless of how far the user has roamed, and then [find those holograms again in later sessions](coordinate-systems.md#spatial-anchor-persistence).</span></span>

<span data-ttu-id="10432-141">Dans Unity, vous créez un point d’ancrage spatiale en ajoutant le **WorldAnchor** composant Unity à un GameObject.</span><span class="sxs-lookup"><span data-stu-id="10432-141">In Unity, you create a spatial anchor by adding the **WorldAnchor** Unity component to a GameObject.</span></span>

### <a name="adding-a-world-anchor"></a><span data-ttu-id="10432-142">Ajout d’un point d’ancrage du monde</span><span class="sxs-lookup"><span data-stu-id="10432-142">Adding a World Anchor</span></span>

<span data-ttu-id="10432-143">Pour ajouter un point d’ancrage du monde, appelez AddComponent<WorldAnchor>() sur l’objet de jeu avec la transformation que vous souhaitez ancrer dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="10432-143">To add a world anchor, call AddComponent<WorldAnchor>() on the game object with the transform you want to anchor in the real world.</span></span>

```cs
WorldAnchor anchor = gameObject.AddComponent<WorldAnchor>();
```

<span data-ttu-id="10432-144">C’est tout !</span><span class="sxs-lookup"><span data-stu-id="10432-144">That's it!</span></span> <span data-ttu-id="10432-145">Cet objet de jeu sera désormais être ancré à son emplacement actuel dans le monde physique, vous pouvez voir ses coordonnées de monde Unity ajuster légèrement au fil du temps pour vous assurer qu’alignement physique.</span><span class="sxs-lookup"><span data-stu-id="10432-145">This game object will now be anchored to its current location in the physical world - you may see its Unity world coordinates adjust slightly over time to ensure that physical alignment.</span></span> <span data-ttu-id="10432-146">Utilisez [persistance](persistence-in-unity.md) à trouver cela ancrée emplacement dans une session de futures de l’application.</span><span class="sxs-lookup"><span data-stu-id="10432-146">Use [persistence](persistence-in-unity.md) to find this anchored location again in a future app session.</span></span>

### <a name="removing-a-world-anchor"></a><span data-ttu-id="10432-147">Suppression d’un point d’ancrage du monde</span><span class="sxs-lookup"><span data-stu-id="10432-147">Removing a World Anchor</span></span>

<span data-ttu-id="10432-148">Si n’est plus, vous souhaitez que le GameObject verrouillé sur un emplacement du monde physique et que vous ne prévoyez pas sur le déplacement de ce cadre, vous pouvez simplement appeler Destroy sur le composant de point d’ancrage du monde entier.</span><span class="sxs-lookup"><span data-stu-id="10432-148">If you no longer want the GameObject locked to a physical world location and don't intend on moving it this frame, then you can just call Destroy on the World Anchor component.</span></span>

```cs
Destroy(gameObject.GetComponent<WorldAnchor>());
```

<span data-ttu-id="10432-149">Si vous souhaitez déplacer le GameObject ce cadre, vous devez appeler DestroyImmediate à la place.</span><span class="sxs-lookup"><span data-stu-id="10432-149">If you want to move the GameObject this frame, you need to call DestroyImmediate instead.</span></span>

```cs
DestroyImmediate(gameObject.GetComponent<WorldAnchor>());
```

### <a name="moving-a-world-anchored-gameobject"></a><span data-ttu-id="10432-150">Déplacement d’un monde ancrée GameObject</span><span class="sxs-lookup"><span data-stu-id="10432-150">Moving a World Anchored GameObject</span></span>

<span data-ttu-id="10432-151">Impossible de déplacer du GameObject pendant une ancre de World dessus.</span><span class="sxs-lookup"><span data-stu-id="10432-151">GameObject's cannot be moved while a World Anchor is on it.</span></span> <span data-ttu-id="10432-152">Si vous devez déplacer le GameObject ce frame, vous devez :</span><span class="sxs-lookup"><span data-stu-id="10432-152">If you need to move the GameObject this frame, you need to:</span></span>
1. <span data-ttu-id="10432-153">DestroyImmediate le composant de point d’ancrage du monde</span><span class="sxs-lookup"><span data-stu-id="10432-153">DestroyImmediate the World Anchor component</span></span>
2. <span data-ttu-id="10432-154">Déplacer le GameObject</span><span class="sxs-lookup"><span data-stu-id="10432-154">Move the GameObject</span></span>
3. <span data-ttu-id="10432-155">Ajouter un nouveau composant de point d’ancrage du monde entier pour le GameObject.</span><span class="sxs-lookup"><span data-stu-id="10432-155">Add a new World Anchor component to the GameObject.</span></span>

```cs
DestroyImmediate(gameObject.GetComponent<WorldAnchor>());
gameObject.transform.position = new Vector3(0, 0, 2);
WorldAnchor anchor = gameObject.AddComponent<WorldAnchor>();
```

### <a name="handling-locatability-changes"></a><span data-ttu-id="10432-156">Gestion des modifications de Locatability</span><span class="sxs-lookup"><span data-stu-id="10432-156">Handling Locatability Changes</span></span>

<span data-ttu-id="10432-157">Un WorldAnchor peut-être pas localisable dans le monde physique à un point dans le temps.</span><span class="sxs-lookup"><span data-stu-id="10432-157">A WorldAnchor may not be locatable in the physical world at a point in time.</span></span> <span data-ttu-id="10432-158">Si cela se produit, Unity n'a pas mis à jour la transformation de l’objet ancré.</span><span class="sxs-lookup"><span data-stu-id="10432-158">If that occurs, Unity will not be updating the transform of the anchored object.</span></span> <span data-ttu-id="10432-159">Cela peut également changer pendant l’exécution d’une application.</span><span class="sxs-lookup"><span data-stu-id="10432-159">This also can change while an app is running.</span></span> <span data-ttu-id="10432-160">Gérer les modifications dans locatability provoquera l’objet s’affiche ne pas dans l’emplacement physique approprié dans le monde.</span><span class="sxs-lookup"><span data-stu-id="10432-160">Failure to handle the change in locatability will cause the object to not appear in the correct physical location in the world.</span></span>

<span data-ttu-id="10432-161">Pour être averti des modifications de locatability :</span><span class="sxs-lookup"><span data-stu-id="10432-161">To be notified about locatability changes:</span></span>
1. <span data-ttu-id="10432-162">S’abonner à l’événement OnTrackingChanged</span><span class="sxs-lookup"><span data-stu-id="10432-162">Subscribe to the OnTrackingChanged event</span></span>
2. <span data-ttu-id="10432-163">Gérer l’événement</span><span class="sxs-lookup"><span data-stu-id="10432-163">Handle the event</span></span>

<span data-ttu-id="10432-164">Le **OnTrackingChanged** événement sera appelé chaque fois que le point d’ancrage spatial sous-jacent change entre un état d’être localisables et n’est pas localisable.</span><span class="sxs-lookup"><span data-stu-id="10432-164">The **OnTrackingChanged** event will be called whenever the underlying spatial anchor changes between a state of being locatable vs. not being locatable.</span></span>

```cs
anchor.OnTrackingChanged += Anchor_OnTrackingChanged;
```

<span data-ttu-id="10432-165">Puis gérer l’événement :</span><span class="sxs-lookup"><span data-stu-id="10432-165">Then handle the event:</span></span>

```cs
private void Anchor_OnTrackingChanged(WorldAnchor self, bool located)
{
    // This simply activates/deactivates this object and all children when tracking changes
    self.gameObject.SetActiveRecursively(located);
}
```

<span data-ttu-id="10432-166">Parfois ancres se trouvent immédiatement.</span><span class="sxs-lookup"><span data-stu-id="10432-166">Sometimes anchors are located immediately.</span></span> <span data-ttu-id="10432-167">Dans ce cas, cette propriété isLocated de l’ancrage est fixée à true lorsque AddComponent<WorldAnchor>() retourne.</span><span class="sxs-lookup"><span data-stu-id="10432-167">In this case, this isLocated property of the anchor will be set to true when AddComponent<WorldAnchor>() returns.</span></span> <span data-ttu-id="10432-168">Par conséquent, l’événement OnTrackingChanged ne sera pas déclenchée.</span><span class="sxs-lookup"><span data-stu-id="10432-168">As a result, the OnTrackingChanged event will not be triggered.</span></span> <span data-ttu-id="10432-169">Un modèle propre consisterait à appeler votre gestionnaire OnTrackingChanged avec l’état initial de IsLocated après l’attachement d’un point d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="10432-169">A clean pattern would be to call your OnTrackingChanged handler with the initial IsLocated state after attaching an anchor.</span></span>

```cs
Anchor_OnTrackingChanged(anchor, anchor.isLocated);
```

## <a name="sharing-anchors-across-devices"></a><span data-ttu-id="10432-170">Partage des points d’ancrage sur des appareils</span><span class="sxs-lookup"><span data-stu-id="10432-170">Sharing anchors across devices</span></span>

<span data-ttu-id="10432-171">Vous pouvez utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a> pour créer un point d’ancrage cloud durable à partir d’un WorldAnchor local, lequel votre application peut ensuite localiser dans plusieurs HoloLens, appareils iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="10432-171">You can use <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a> to create a durable cloud anchor from a local WorldAnchor, which your app can then locate across multiple HoloLens, iOS and Android devices.</span></span>  <span data-ttu-id="10432-172">En partageant une ancre spatiale commune sur plusieurs appareils, chaque utilisateur peut voir le contenu restitué par rapport à ce point d’ancrage dans le même emplacement physique.</span><span class="sxs-lookup"><span data-stu-id="10432-172">By sharing a common spatial anchor across multiple devices, each user can see content rendered relative to that anchor in the same physical location.</span></span>  <span data-ttu-id="10432-173">Ainsi, les expériences partagées en temps réel.</span><span class="sxs-lookup"><span data-stu-id="10432-173">This allows for real-time shared experiences.</span></span>

<span data-ttu-id="10432-174">Pour commencer à créer des expériences partagées dans Unity, essayez les 5 minutes <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Démarrages rapides Azure Spatial ancres Unity</a>.</span><span class="sxs-lookup"><span data-stu-id="10432-174">To get started building shared experiences in Unity, try out the 5-minute <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Azure Spatial Anchors Unity quickstarts</a>.</span></span>

<span data-ttu-id="10432-175">Une fois que vous êtes en cours d’exécution ancres spatiale d’Azure, vous pouvez ensuite <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">créer et localiser les points d’ancrage dans Unity</a>.</span><span class="sxs-lookup"><span data-stu-id="10432-175">Once you're up and running with Azure Spatial Anchors, you can then <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">create and locate anchors in Unity</a>.</span></span>

## <a name="see-also"></a><span data-ttu-id="10432-176">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="10432-176">See Also</span></span>
* [<span data-ttu-id="10432-177">Échelles de l’expérience</span><span class="sxs-lookup"><span data-stu-id="10432-177">Experience scales</span></span>](coordinate-systems.md#mixed-reality-experience-scales)
* [<span data-ttu-id="10432-178">Étape spatial</span><span class="sxs-lookup"><span data-stu-id="10432-178">Spatial stage</span></span>](coordinate-systems.md#stage-frame-of-reference)
* [<span data-ttu-id="10432-179">Suivi de la perte dans Unity</span><span class="sxs-lookup"><span data-stu-id="10432-179">Tracking loss in Unity</span></span>](tracking-loss-in-unity.md)
* [<span data-ttu-id="10432-180">Ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="10432-180">Spatial anchors</span></span>](spatial-anchors.md)
* [<span data-ttu-id="10432-181">Persistance dans Unity</span><span class="sxs-lookup"><span data-stu-id="10432-181">Persistence in Unity</span></span>](persistence-in-unity.md)
* [<span data-ttu-id="10432-182">Expériences partagées dans Unity</span><span class="sxs-lookup"><span data-stu-id="10432-182">Shared experiences in Unity</span></span>](shared-experiences-in-unity.md)
* <span data-ttu-id="10432-183"><a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Ancres Spatial Azure</a></span><span class="sxs-lookup"><span data-stu-id="10432-183"><a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a></span></span>
* <span data-ttu-id="10432-184"><a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Ancres Spatial Azure SDK pour Unity</a></span><span class="sxs-lookup"><span data-stu-id="10432-184"><a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Azure Spatial Anchors SDK for Unity</a></span></span>