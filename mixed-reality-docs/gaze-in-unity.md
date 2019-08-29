---
title: Point de regard
description: Le point de regard est un moyen principal pour les utilisateurs de cibler les hologrammes que votre application crée en réalité mixte.
author: thetuvix
ms.author: yoyoz
ms.date: 03/21/2018
ms.topic: article
keywords: oeil-point de regard, point de regard, Unity, hologramme, réalité mixte
ms.openlocfilehash: 43e643bac00e3c889b14000331d2ed95014fdcc5
ms.sourcegitcommit: ff330a7e36e5ff7ae0e9a08c0e99eb7f3f81361f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70122041"
---
# <a name="head-gaze-in-unity"></a><span data-ttu-id="165e0-104">Tête-pointage dans Unity</span><span class="sxs-lookup"><span data-stu-id="165e0-104">Head-gaze in Unity</span></span>

<span data-ttu-id="165e0-105">Le point de [regard](gaze.md) est un moyen principal pour les utilisateurs de cibler les [hologrammes](hologram.md) que votre application crée en [réalité mixte](mixed-reality.md).</span><span class="sxs-lookup"><span data-stu-id="165e0-105">[Gaze](gaze.md) is a primary way for users to target the [holograms](hologram.md) your app creates in [Mixed Reality](mixed-reality.md).</span></span>


## <a name="implementing-head-gaze"></a><span data-ttu-id="165e0-106">Implémentation de la tête en regard</span><span class="sxs-lookup"><span data-stu-id="165e0-106">Implementing head-gaze</span></span>

<span data-ttu-id="165e0-107">D’un point de vue conceptuel, le regard de la [tête](gaze.md) est implémenté en projetant un rayon à partir de la tête de l’utilisateur où le casque est, dans la direction vers l’avant et en déterminant ce que ce rayon entre en conflit.</span><span class="sxs-lookup"><span data-stu-id="165e0-107">Conceptually, [head-gaze](gaze.md) is implemented by projecting a ray from the user's head where the headset is, in the forward direction they are facing and determining what that ray collides with.</span></span> <span data-ttu-id="165e0-108">Dans Unity, la position et la direction de l’en-tête de l’utilisateur sont exposées via l' [appareil photo](camera-in-unity.md)Unity principal, en particulier [UnityEngine. Camera. main](http://docs.unity3d.com/ScriptReference/Camera-main.html). [transformez. Forward](http://docs.unity3d.com/ScriptReference/Transform-forward.html) et [UnityEngine. Camera. main](http://docs.unity3d.com/ScriptReference/Camera-main.html). [transformation. position](http://docs.unity3d.com/ScriptReference/Transform-position.html).</span><span class="sxs-lookup"><span data-stu-id="165e0-108">In Unity, the user's head position and direction are exposed through the Unity Main [Camera](camera-in-unity.md), specifically [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[transform.forward](http://docs.unity3d.com/ScriptReference/Transform-forward.html) and [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[transform.position](http://docs.unity3d.com/ScriptReference/Transform-position.html).</span></span>

<span data-ttu-id="165e0-109">L’appel de [physique. RayCast](http://docs.unity3d.com/ScriptReference/Physics.Raycast.html) génère une structure [RaycastHit](http://docs.unity3d.com/ScriptReference/RaycastHit.html) qui contient des informations sur la collision, y compris le point 3D dans lequel une collision s’est produite et l’autre gameobject le rayon de la tête de regard.</span><span class="sxs-lookup"><span data-stu-id="165e0-109">Calling [Physics.RayCast](http://docs.unity3d.com/ScriptReference/Physics.Raycast.html) results in a [RaycastHit](http://docs.unity3d.com/ScriptReference/RaycastHit.html) structure which contains information about the collision including the 3D point where collision occurred and the other GameObject the head-gaze ray collided with.</span></span>

### <a name="example-implement-head-gaze"></a><span data-ttu-id="165e0-110">Exemple : Implémenter l’en-tête</span><span class="sxs-lookup"><span data-stu-id="165e0-110">Example: Implement head-gaze</span></span>

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

### <a name="best-practices"></a><span data-ttu-id="165e0-111">Bonnes pratiques</span><span class="sxs-lookup"><span data-stu-id="165e0-111">Best practices</span></span>

<span data-ttu-id="165e0-112">Bien que l’exemple ci-dessus montre comment effectuer un raycast unique dans une boucle de mise à jour pour trouver la cible sur laquelle pointe l’utilisateur, il est recommandé de le faire dans un seul objet gérant le point de vue de la tête au lieu de le faire dans un objet potentiellement intéressé par le obje Je suis en regard.</span><span class="sxs-lookup"><span data-stu-id="165e0-112">While the example above demonstrates how to do a single raycast in an update loop to find the target the user's head points at, it is recommended to do this in a single object managing head-gaze instead of doing this in any object that is potentially interested in the object being gazed at.</span></span> <span data-ttu-id="165e0-113">Cela permet à votre application de sauvegarder le traitement en n’exécutant qu’une seule tête de regard raycast chaque cadre.</span><span class="sxs-lookup"><span data-stu-id="165e0-113">This lets your app save processing by doing just one head-gaze raycast each frame.</span></span>

## <a name="visualizing-head-gaze"></a><span data-ttu-id="165e0-114">Visualisation de l’en-tête</span><span class="sxs-lookup"><span data-stu-id="165e0-114">Visualizing head-gaze</span></span>

<span data-ttu-id="165e0-115">Tout comme sur le bureau où vous utilisez un pointeur de souris pour cibler et interagir avec le contenu, vous devez implémenter un [curseur](cursors.md) qui représente le point de regard de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="165e0-115">Just like on the desktop where you use a mouse pointer to target and interact with content, you should implement a [cursor](cursors.md) that represents the user's head-gaze.</span></span> <span data-ttu-id="165e0-116">Cela permet à l’utilisateur de faire confiance à ce qu’il est en train d’interagir avec.</span><span class="sxs-lookup"><span data-stu-id="165e0-116">This gives the user confidence in what they're about to interact with.</span></span>

## <a name="head-gaze-in-the-mixed-reality-toolkit-v2"></a><span data-ttu-id="165e0-117">Tête-pointage dans la réalité mixte Toolkit v2</span><span class="sxs-lookup"><span data-stu-id="165e0-117">Head-gaze in the Mixed Reality Toolkit v2</span></span>
<span data-ttu-id="165e0-118">Vous pouvez accéder au point de regard du [Gestionnaire d’entrée](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html) dans MRTK v2.</span><span class="sxs-lookup"><span data-stu-id="165e0-118">You can access head-gaze from the [Input Manager](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html) in MRTK v2.</span></span>

## <a name="see-also"></a><span data-ttu-id="165e0-119">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="165e0-119">See also</span></span>
* [<span data-ttu-id="165e0-120">Appareil photo</span><span class="sxs-lookup"><span data-stu-id="165e0-120">Camera</span></span>](camera-in-unity.md)
* [<span data-ttu-id="165e0-121">Curseurs</span><span class="sxs-lookup"><span data-stu-id="165e0-121">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="165e0-122">Entrée en regard</span><span class="sxs-lookup"><span data-stu-id="165e0-122">Gaze input</span></span>](gaze.md)
* [<span data-ttu-id="165e0-123">Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="165e0-123">Gaze targeting</span></span>](gaze-targeting.md)
