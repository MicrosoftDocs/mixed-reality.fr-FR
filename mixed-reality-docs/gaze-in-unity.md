---
title: Les regards dans Unity
description: Regards est un moyen principal pour les utilisateurs à cibler les hologrammes que votre application crée en réalité mixte.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: regards, unity, HOLOGRAMME, réalité mixte
ms.openlocfilehash: 09915479a9eef95c5ce4533371e113ab6191a331
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597005"
---
# <a name="gaze-in-unity"></a><span data-ttu-id="4a8d2-104">Les regards dans Unity</span><span class="sxs-lookup"><span data-stu-id="4a8d2-104">Gaze in Unity</span></span>

<span data-ttu-id="4a8d2-105">[Utilisation](gaze.md) est un moyen principal pour les utilisateurs à cibler le [vntana](hologram.md) votre application crée dans [une réalité mixte](mixed-reality.md).</span><span class="sxs-lookup"><span data-stu-id="4a8d2-105">[Gaze](gaze.md) is a primary way for users to target the [holograms](hologram.md) your app creates in [mixed reality](mixed-reality.md).</span></span>

## <a name="implementing-gaze"></a><span data-ttu-id="4a8d2-106">Implémentation du pointage de regard</span><span class="sxs-lookup"><span data-stu-id="4a8d2-106">Implementing Gaze</span></span>

<span data-ttu-id="4a8d2-107">Conceptuellement, [les regards](gaze.md) est implémentée en projetant un rayon à partir de la tête de l’utilisateur où le casque est, dans la direction avant qu’ils sont accessibles et déterminer ce que ray est en conflit avec.</span><span class="sxs-lookup"><span data-stu-id="4a8d2-107">Conceptually, [gaze](gaze.md) is implemented by projecting a ray from the user's head where the headset is, in the forward direction they are facing and determining what that ray collides with.</span></span> <span data-ttu-id="4a8d2-108">Dans Unity, position principal de l’utilisateur et la direction sont exposées via les principaux Unity [caméra](camera-in-unity.md), plus précisément [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[ Transform.Forward](http://docs.unity3d.com/ScriptReference/Transform-forward.html) et [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[ Transform.position](http://docs.unity3d.com/ScriptReference/Transform-position.html).</span><span class="sxs-lookup"><span data-stu-id="4a8d2-108">In Unity, the user's head position and direction are exposed through the Unity Main [Camera](camera-in-unity.md), specifically [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[transform.forward](http://docs.unity3d.com/ScriptReference/Transform-forward.html) and [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[transform.position](http://docs.unity3d.com/ScriptReference/Transform-position.html).</span></span>

<span data-ttu-id="4a8d2-109">Appel [Physics.RayCast](http://docs.unity3d.com/ScriptReference/Physics.Raycast.html) entraîne une [RaycastHit](http://docs.unity3d.com/ScriptReference/RaycastHit.html) structure qui contient des informations sur la collision, y compris le point 3D où collision s’est produite et autres GameObject le rayon du pointage de regard entrent en conflit avec.</span><span class="sxs-lookup"><span data-stu-id="4a8d2-109">Calling [Physics.RayCast](http://docs.unity3d.com/ScriptReference/Physics.Raycast.html) results in a [RaycastHit](http://docs.unity3d.com/ScriptReference/RaycastHit.html) structure which contains information about the collision including the 3D point where collision occurred and the other GameObject the gaze ray collided with.</span></span>

### <a name="example-implement-gaze"></a><span data-ttu-id="4a8d2-110">Exemple : Implémentez regards</span><span class="sxs-lookup"><span data-stu-id="4a8d2-110">Example: Implement Gaze</span></span>

```cs
void Update()
{
       RaycastHit hitInfo;
       if (Physics.Raycast(
               Camera.main.transform.position,
               Camera.main.transform.forward,
               out hitInfo,
               20.0f,
               Physics.DefaultRaycastLayers))
       {
           // If the Raycast has succeeded and hit a hologram
           // hitInfo's point represents the position being gazed at
           // hitInfo's collider GameObject represents the hologram being gazed at
       }
}
```

### <a name="best-practices"></a><span data-ttu-id="4a8d2-111">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="4a8d2-111">Best Practices</span></span>

<span data-ttu-id="4a8d2-112">Tandis que l’exemple ci-dessus montre comment effectuer un raycast unique dans une boucle de mise à jour pour rechercher la cible du pointage de regard, il est recommandé d’effectuer cette opération dans un seul objet de la gestion des regards au lieu de cela dans n’importe quel objet qui est potentiellement intéressé par l’objet en cours gazed à.</span><span class="sxs-lookup"><span data-stu-id="4a8d2-112">While the example above demonstrates how to do a single raycast in an update loop to find the Gaze target, it is recommended to do this in a single object managing gaze instead of doing this in any object that is potentially interested in the object being gazed at.</span></span> <span data-ttu-id="4a8d2-113">Cela permet à votre application d’enregistrer le traitement en procédant comme seul regards raycast chaque frame.</span><span class="sxs-lookup"><span data-stu-id="4a8d2-113">This lets your app save processing by doing just one gaze raycast each frame.</span></span>

## <a name="visualizing-gaze"></a><span data-ttu-id="4a8d2-114">Visualisation du pointage de regard</span><span class="sxs-lookup"><span data-stu-id="4a8d2-114">Visualizing Gaze</span></span>

<span data-ttu-id="4a8d2-115">Tout comme sur le bureau où vous utilisez un pointeur de la souris pour cibler et interagir avec du contenu, vous devez implémenter un [curseur](cursors.md) qui représente le regard de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4a8d2-115">Just like on the desktop where you use a mouse pointer to target and interact with content, you should implement a [cursor](cursors.md) that represents the user's gaze.</span></span> <span data-ttu-id="4a8d2-116">Cela donne la confiance des utilisateurs dans ce que sur le point d’interagir avec elles.</span><span class="sxs-lookup"><span data-stu-id="4a8d2-116">This gives the user confidence in what they're about to interact with.</span></span>

## <a name="gaze-in-mixed-reality-toolkit"></a><span data-ttu-id="4a8d2-117">Utilisation dans le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="4a8d2-117">Gaze in Mixed Reality Toolkit</span></span>
<span data-ttu-id="4a8d2-118">Lorsque vous importez [MRTK publie des packages de Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases) ou cloner le projet à partir de la [référentiel GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity), vous vous apprêtez à trouver un nouveau menu « Toolkit de réalité mixte » dans Unity.</span><span class="sxs-lookup"><span data-stu-id="4a8d2-118">When you import [MRTK release Unity packages](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases) or clone the project from the [GitHub repository](https://github.com/Microsoft/MixedRealityToolkit-Unity), you are going to find a new menu 'Mixed Reality Toolkit' in Unity.</span></span> <span data-ttu-id="4a8d2-119">Sous le menu « Configurer », vous verrez le menu « Application des paramètres de scène réalité mixte ».</span><span class="sxs-lookup"><span data-stu-id="4a8d2-119">Under 'Configure' menu, you will see the menu 'Apply Mixed Reality Scene Settings'.</span></span> <span data-ttu-id="4a8d2-120">Lorsque vous cliquez dessus, il supprime l’appareil photo par défaut et ajoute les composants fondamentaux - [InputManager](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/InputManager.prefab), [MixedRealityCameraParent](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/MixedRealityCameraParent.prefab), et [DefaultCursor](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor/DefaultCursor.prefab).</span><span class="sxs-lookup"><span data-stu-id="4a8d2-120">When you click it, it removes the default camera and adds foundational components - [InputManager](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/InputManager.prefab), [MixedRealityCameraParent](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/MixedRealityCameraParent.prefab), and [DefaultCursor](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor/DefaultCursor.prefab).</span></span>

<span data-ttu-id="4a8d2-121">![Menu MRTK pour le programme d’installation de scène](images/MRTK_Input_Menu.png)</span><span class="sxs-lookup"><span data-stu-id="4a8d2-121">![MRTK Menu for scene setup](images/MRTK_Input_Menu.png)</span></span><br>
<span data-ttu-id="4a8d2-122">*Menu MRTK pour le programme d’installation de scène*</span><span class="sxs-lookup"><span data-stu-id="4a8d2-122">*MRTK Menu for scene setup*</span></span>

<span data-ttu-id="4a8d2-123">![Programme d’installation automatique de scène dans MRTK](images/MRTK_HowTo_Input1.png)</span><span class="sxs-lookup"><span data-stu-id="4a8d2-123">![Automatic scene setup in MRTK](images/MRTK_HowTo_Input1.png)</span></span><br>
<span data-ttu-id="4a8d2-124">*Programme d’installation automatique de scène dans MRTK*</span><span class="sxs-lookup"><span data-stu-id="4a8d2-124">*Automatic scene setup in MRTK*</span></span>

### <a name="gaze-related-scripts-in-mixed-reality-toolkit"></a><span data-ttu-id="4a8d2-125">Utilisation des scripts associés dans le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="4a8d2-125">Gaze related scripts in Mixed Reality Toolkit</span></span>
<span data-ttu-id="4a8d2-126">Mixte réalité la boîte à outils inclut des InputManager prefab [GazeManager.cs](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Gaze/GazeManager.cs) et [les regards de stabilisation](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Gaze/GazeStabilizer.cs).</span><span class="sxs-lookup"><span data-stu-id="4a8d2-126">Mixed Reality Toolkit's InputManager prefab includes [GazeManager.cs](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Gaze/GazeManager.cs) and [Gaze Stabilizer](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Gaze/GazeStabilizer.cs).</span></span> <span data-ttu-id="4a8d2-127">Sous [SimpleSinglePointerSelector](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Focus/SimpleSinglePointerSelector.cs), vous pouvez assigner votre curseur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="4a8d2-127">Under [SimpleSinglePointerSelector](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Focus/SimpleSinglePointerSelector.cs), you can assign your custom Cursor.</span></span> <span data-ttu-id="4a8d2-128">Par défaut, animée [DefaultCursor](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor/DefaultCursor.prefab) est affecté.</span><span class="sxs-lookup"><span data-stu-id="4a8d2-128">In default, animated [DefaultCursor](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor/DefaultCursor.prefab) is assigned.</span></span>

<span data-ttu-id="4a8d2-129">[Cursor.prefab](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor) et [CursorWithFeedback.prefab](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor) vous montre comment visualiser votre regard sur l’utilisation de curseurs.</span><span class="sxs-lookup"><span data-stu-id="4a8d2-129">[Cursor.prefab](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor) and [CursorWithFeedback.prefab](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor) shows you how to visualize your Gaze using Cursors.</span></span>

## <a name="see-also"></a><span data-ttu-id="4a8d2-130">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4a8d2-130">See also</span></span>
* [<span data-ttu-id="4a8d2-131">Appareil photo</span><span class="sxs-lookup"><span data-stu-id="4a8d2-131">Camera</span></span>](camera-in-unity.md)
* [<span data-ttu-id="4a8d2-132">Gaze</span><span class="sxs-lookup"><span data-stu-id="4a8d2-132">Gaze</span></span>](gaze.md)
* [<span data-ttu-id="4a8d2-133">Curseurs</span><span class="sxs-lookup"><span data-stu-id="4a8d2-133">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="4a8d2-134">Ciblage des regards</span><span class="sxs-lookup"><span data-stu-id="4a8d2-134">Gaze targeting</span></span>](gaze-targeting.md)
