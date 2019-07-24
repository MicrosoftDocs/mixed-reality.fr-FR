---
title: Point de regard
description: Le point de regard est un moyen principal pour les utilisateurs de cibler les hologrammes que votre application crée en réalité mixte.
author: thetuvix
ms.author: yoyoz
ms.date: 03/21/2018
ms.topic: article
keywords: point de présence, Unity, hologramme, réalité mixte
ms.openlocfilehash: b2cc86db156a1e97b013e4cd6debe3abe5ffb6dd
ms.sourcegitcommit: 60060386305eabfac2758a2c861a43c36286b151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453721"
---
# <a name="head-gaze-in-unity"></a><span data-ttu-id="ce28a-104">Point de regard de l’en-tête dans Unity</span><span class="sxs-lookup"><span data-stu-id="ce28a-104">Head gaze in Unity</span></span>

<span data-ttu-id="ce28a-105">Le point de [regard](gaze.md) est un moyen principal pour les utilisateurs de cibler les [hologrammes](hologram.md) que votre application crée en [réalité mixte](mixed-reality.md).</span><span class="sxs-lookup"><span data-stu-id="ce28a-105">[Gaze](gaze.md) is a primary way for users to target the [holograms](hologram.md) your app creates in [Mixed Reality](mixed-reality.md).</span></span>


## <a name="implementing-head-gaze"></a><span data-ttu-id="ce28a-106">Implémentation de la tête en regard</span><span class="sxs-lookup"><span data-stu-id="ce28a-106">Implementing head gaze</span></span>

<span data-ttu-id="ce28a-107">D’un point de vue conceptuel, le point de [regard](gaze.md) est implémenté en projetant un rayon à partir de l’en-tête de l’utilisateur où le casque est, dans la direction vers l’avant et en déterminant ce que ce rayon entre en conflit.</span><span class="sxs-lookup"><span data-stu-id="ce28a-107">Conceptually, [gaze](gaze.md) is implemented by projecting a ray from the user's head where the headset is, in the forward direction they are facing and determining what that ray collides with.</span></span> <span data-ttu-id="ce28a-108">Dans Unity, la position et la direction de l’en-tête de l’utilisateur sont exposées via l' [appareil photo](camera-in-unity.md)Unity principal, en particulier [UnityEngine. Camera. main](http://docs.unity3d.com/ScriptReference/Camera-main.html). [transformez. Forward](http://docs.unity3d.com/ScriptReference/Transform-forward.html) et [UnityEngine. Camera. main](http://docs.unity3d.com/ScriptReference/Camera-main.html). [transformation. position](http://docs.unity3d.com/ScriptReference/Transform-position.html).</span><span class="sxs-lookup"><span data-stu-id="ce28a-108">In Unity, the user's head position and direction are exposed through the Unity Main [Camera](camera-in-unity.md), specifically [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[transform.forward](http://docs.unity3d.com/ScriptReference/Transform-forward.html) and [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[transform.position](http://docs.unity3d.com/ScriptReference/Transform-position.html).</span></span>

<span data-ttu-id="ce28a-109">L’appel de [physique. RayCast](http://docs.unity3d.com/ScriptReference/Physics.Raycast.html) génère une structure [RaycastHit](http://docs.unity3d.com/ScriptReference/RaycastHit.html) qui contient des informations sur la collision, y compris le point 3D où la collision s’est produite et l’autre gameobject le rayon du point de regard.</span><span class="sxs-lookup"><span data-stu-id="ce28a-109">Calling [Physics.RayCast](http://docs.unity3d.com/ScriptReference/Physics.Raycast.html) results in a [RaycastHit](http://docs.unity3d.com/ScriptReference/RaycastHit.html) structure which contains information about the collision including the 3D point where collision occurred and the other GameObject the gaze ray collided with.</span></span>

### <a name="example-implement-head-gaze"></a><span data-ttu-id="ce28a-110">Exemple : Implémenter l’en-tête</span><span class="sxs-lookup"><span data-stu-id="ce28a-110">Example: Implement head gaze</span></span>

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

### <a name="best-practices"></a><span data-ttu-id="ce28a-111">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="ce28a-111">Best Practices</span></span>

<span data-ttu-id="ce28a-112">Bien que l’exemple ci-dessus montre comment effectuer un raycast unique dans une boucle de mise à jour pour rechercher la cible du point d’interdépendance, il est recommandé de le faire dans un seul objet gérant le point de regard au lieu de le faire dans tout objet qui est susceptible d’intéresser l’objet en cours de regard.</span><span class="sxs-lookup"><span data-stu-id="ce28a-112">While the example above demonstrates how to do a single raycast in an update loop to find the Gaze target, it is recommended to do this in a single object managing gaze instead of doing this in any object that is potentially interested in the object being gazed at.</span></span> <span data-ttu-id="ce28a-113">Cela permet à votre application de sauvegarder le traitement en n’appliquant qu’une seule raycast de pointage à chaque cadre.</span><span class="sxs-lookup"><span data-stu-id="ce28a-113">This lets your app save processing by doing just one gaze raycast each frame.</span></span>

## <a name="visualizing-gaze"></a><span data-ttu-id="ce28a-114">Visualisation du regard</span><span class="sxs-lookup"><span data-stu-id="ce28a-114">Visualizing Gaze</span></span>

<span data-ttu-id="ce28a-115">Tout comme sur le bureau où vous utilisez un pointeur de souris pour cibler et interagir avec le contenu, vous devez implémenter un [curseur](cursors.md) qui représente le regard de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ce28a-115">Just like on the desktop where you use a mouse pointer to target and interact with content, you should implement a [cursor](cursors.md) that represents the user's gaze.</span></span> <span data-ttu-id="ce28a-116">Cela permet à l’utilisateur de faire confiance à ce qu’il est en train d’interagir avec.</span><span class="sxs-lookup"><span data-stu-id="ce28a-116">This gives the user confidence in what they're about to interact with.</span></span>

## <a name="gaze-in-mixed-reality-toolkit-v2"></a><span data-ttu-id="ce28a-117">Point d’interversion de la réalité mixte Toolkit v2</span><span class="sxs-lookup"><span data-stu-id="ce28a-117">Gaze in Mixed Reality Toolkit v2</span></span>
<span data-ttu-id="ce28a-118">Vous pouvez accéder au point de regard à partir du [Gestionnaire d’entrée](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html) dans MRTK v2.</span><span class="sxs-lookup"><span data-stu-id="ce28a-118">You can access gaze from the [input Manager](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html) in MRTK v2.</span></span>

## <a name="see-also"></a><span data-ttu-id="ce28a-119">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ce28a-119">See also</span></span>
* [<span data-ttu-id="ce28a-120">Appareil photo</span><span class="sxs-lookup"><span data-stu-id="ce28a-120">Camera</span></span>](camera-in-unity.md)
* [<span data-ttu-id="ce28a-121">Entrée en regard</span><span class="sxs-lookup"><span data-stu-id="ce28a-121">Gaze input</span></span>](gaze.md)
* [<span data-ttu-id="ce28a-122">Curseurs</span><span class="sxs-lookup"><span data-stu-id="ce28a-122">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="ce28a-123">Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="ce28a-123">Gaze targeting</span></span>](gaze-targeting.md)
