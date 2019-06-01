---
title: Les regards dans Unity
description: Regards est un moyen principal pour les utilisateurs à cibler les hologrammes que votre application crée en réalité mixte.
author: thetuvix
ms.author: yoyoz
ms.date: 03/21/2018
ms.topic: article
keywords: regards, unity, HOLOGRAMME, réalité mixte
ms.openlocfilehash: b2cc86db156a1e97b013e4cd6debe3abe5ffb6dd
ms.sourcegitcommit: 60060386305eabfac2758a2c861a43c36286b151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453721"
---
# <a name="head-gaze-in-unity"></a><span data-ttu-id="d946f-104">Head regards dans Unity</span><span class="sxs-lookup"><span data-stu-id="d946f-104">Head gaze in Unity</span></span>

<span data-ttu-id="d946f-105">[Utilisation](gaze.md) est un moyen principal pour les utilisateurs à cibler le [vntana](hologram.md) votre application crée dans [réalité mixte](mixed-reality.md).</span><span class="sxs-lookup"><span data-stu-id="d946f-105">[Gaze](gaze.md) is a primary way for users to target the [holograms](hologram.md) your app creates in [Mixed Reality](mixed-reality.md).</span></span>


## <a name="implementing-head-gaze"></a><span data-ttu-id="d946f-106">Implémentation des regards principal</span><span class="sxs-lookup"><span data-stu-id="d946f-106">Implementing head gaze</span></span>

<span data-ttu-id="d946f-107">Conceptuellement, [les regards](gaze.md) est implémentée en projetant un rayon à partir de la tête de l’utilisateur où le casque est, dans la direction avant qu’ils sont accessibles et déterminer ce que ray est en conflit avec.</span><span class="sxs-lookup"><span data-stu-id="d946f-107">Conceptually, [gaze](gaze.md) is implemented by projecting a ray from the user's head where the headset is, in the forward direction they are facing and determining what that ray collides with.</span></span> <span data-ttu-id="d946f-108">Dans Unity, position principal de l’utilisateur et la direction sont exposées via les principaux Unity [caméra](camera-in-unity.md), plus précisément [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[ Transform.Forward](http://docs.unity3d.com/ScriptReference/Transform-forward.html) et [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[ Transform.position](http://docs.unity3d.com/ScriptReference/Transform-position.html).</span><span class="sxs-lookup"><span data-stu-id="d946f-108">In Unity, the user's head position and direction are exposed through the Unity Main [Camera](camera-in-unity.md), specifically [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[transform.forward](http://docs.unity3d.com/ScriptReference/Transform-forward.html) and [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[transform.position](http://docs.unity3d.com/ScriptReference/Transform-position.html).</span></span>

<span data-ttu-id="d946f-109">Appel [Physics.RayCast](http://docs.unity3d.com/ScriptReference/Physics.Raycast.html) entraîne une [RaycastHit](http://docs.unity3d.com/ScriptReference/RaycastHit.html) structure qui contient des informations sur la collision, y compris le point 3D où collision s’est produite et autres GameObject le rayon du pointage de regard entrent en conflit avec.</span><span class="sxs-lookup"><span data-stu-id="d946f-109">Calling [Physics.RayCast](http://docs.unity3d.com/ScriptReference/Physics.Raycast.html) results in a [RaycastHit](http://docs.unity3d.com/ScriptReference/RaycastHit.html) structure which contains information about the collision including the 3D point where collision occurred and the other GameObject the gaze ray collided with.</span></span>

### <a name="example-implement-head-gaze"></a><span data-ttu-id="d946f-110">Exemple : Implémentez des regards principal</span><span class="sxs-lookup"><span data-stu-id="d946f-110">Example: Implement head gaze</span></span>

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

### <a name="best-practices"></a><span data-ttu-id="d946f-111">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="d946f-111">Best Practices</span></span>

<span data-ttu-id="d946f-112">Tandis que l’exemple ci-dessus montre comment effectuer un raycast unique dans une boucle de mise à jour pour rechercher la cible du pointage de regard, il est recommandé d’effectuer cette opération dans un seul objet de la gestion des regards au lieu de cela dans n’importe quel objet qui est potentiellement intéressé par l’objet en cours gazed à.</span><span class="sxs-lookup"><span data-stu-id="d946f-112">While the example above demonstrates how to do a single raycast in an update loop to find the Gaze target, it is recommended to do this in a single object managing gaze instead of doing this in any object that is potentially interested in the object being gazed at.</span></span> <span data-ttu-id="d946f-113">Cela permet à votre application d’enregistrer le traitement en procédant comme seul regards raycast chaque frame.</span><span class="sxs-lookup"><span data-stu-id="d946f-113">This lets your app save processing by doing just one gaze raycast each frame.</span></span>

## <a name="visualizing-gaze"></a><span data-ttu-id="d946f-114">Visualisation du pointage de regard</span><span class="sxs-lookup"><span data-stu-id="d946f-114">Visualizing Gaze</span></span>

<span data-ttu-id="d946f-115">Tout comme sur le bureau où vous utilisez un pointeur de la souris pour cibler et interagir avec du contenu, vous devez implémenter un [curseur](cursors.md) qui représente le regard de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d946f-115">Just like on the desktop where you use a mouse pointer to target and interact with content, you should implement a [cursor](cursors.md) that represents the user's gaze.</span></span> <span data-ttu-id="d946f-116">Cela donne la confiance des utilisateurs dans ce que sur le point d’interagir avec elles.</span><span class="sxs-lookup"><span data-stu-id="d946f-116">This gives the user confidence in what they're about to interact with.</span></span>

## <a name="gaze-in-mixed-reality-toolkit-v2"></a><span data-ttu-id="d946f-117">Utilisation en réalité mixte Toolkit v2</span><span class="sxs-lookup"><span data-stu-id="d946f-117">Gaze in Mixed Reality Toolkit v2</span></span>
<span data-ttu-id="d946f-118">Vous pouvez accéder à des regards à partir de la [d’entrée Manager](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html) dans MRTK v2.</span><span class="sxs-lookup"><span data-stu-id="d946f-118">You can access gaze from the [input Manager](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html) in MRTK v2.</span></span>

## <a name="see-also"></a><span data-ttu-id="d946f-119">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d946f-119">See also</span></span>
* [<span data-ttu-id="d946f-120">Appareil photo</span><span class="sxs-lookup"><span data-stu-id="d946f-120">Camera</span></span>](camera-in-unity.md)
* [<span data-ttu-id="d946f-121">Entrée des regards</span><span class="sxs-lookup"><span data-stu-id="d946f-121">Gaze input</span></span>](gaze.md)
* [<span data-ttu-id="d946f-122">Curseurs</span><span class="sxs-lookup"><span data-stu-id="d946f-122">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="d946f-123">Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="d946f-123">Gaze targeting</span></span>](gaze-targeting.md)
