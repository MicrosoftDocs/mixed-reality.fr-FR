---
title: Point de focus dans Unity
description: Régler manuellement la stabilité hologramme dans Unity en définissant le point de focus
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, point de focus, plan de focus, plan de stabilisation, point de stabilisation, reprojection, LSR, mémoire tampon de profondeur
ms.openlocfilehash: 0f43c37df66ecada86dcb309fcd58d822f0f3481
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597037"
---
# <a name="focus-point-in-unity"></a><span data-ttu-id="43100-104">Point de focus dans Unity</span><span class="sxs-lookup"><span data-stu-id="43100-104">Focus point in Unity</span></span>

<span data-ttu-id="43100-105">**Namespace :** *UnityEngine.XR.WSA*</span><span class="sxs-lookup"><span data-stu-id="43100-105">**Namespace:** *UnityEngine.XR.WSA*</span></span><br>
<span data-ttu-id="43100-106">**Type** : *HolographicSettings*</span><span class="sxs-lookup"><span data-stu-id="43100-106">**Type**: *HolographicSettings*</span></span>

<span data-ttu-id="43100-107">Le [concentrer point](hologram-stability.md#stabilization-plane) peut être définie sur fournir HoloLens un indicateur sur comment effectuer au mieux stabilisation sur les hologrammes actuellement en cours affiche.</span><span class="sxs-lookup"><span data-stu-id="43100-107">The [focus point](hologram-stability.md#stabilization-plane) can be set to provide HoloLens a hint about how to best perform stabilization on the holograms currently being displayed.</span></span>

<span data-ttu-id="43100-108">Si vous souhaitez définir le Point de Focus dans Unity, il doit être définie à chaque image en utilisant le *HolographicSettings.SetFocusPointForFrame()*.</span><span class="sxs-lookup"><span data-stu-id="43100-108">If you want to set the Focus Point in Unity, it needs to be set every frame using *HolographicSettings.SetFocusPointForFrame()*.</span></span> <span data-ttu-id="43100-109">Si le Point de Focus n’est pas défini pour un frame, le plan de stabilisation par défaut sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="43100-109">If the Focus Point is not set for a frame, the default stabilization plane will be used.</span></span>

> [!NOTE]
> <span data-ttu-id="43100-110">Par défaut, nouveaux projets de Unity ont l’option « Activer le partage de mémoire tampon profondeur » définie.</span><span class="sxs-lookup"><span data-stu-id="43100-110">By default, new Unity projects have the "Enable Depth Buffer Sharing" option set.</span></span>  <span data-ttu-id="43100-111">Avec cette option, une application Unity s’exécutant sur un casque immersif de bureau ou un HoloLens exécutant Windows 10 avril 2018 mise à jour (RS4) ou plus tard votre mémoire tampon de profondeur à Windows pour optimiser la stabilité hologramme automatiquement, sans spécifier de votre application envoie un point de focus :</span><span class="sxs-lookup"><span data-stu-id="43100-111">With this option, a Unity app running on either an immersive desktop headset or a HoloLens running the Windows 10 April 2018 Update (RS4) or later will submit your depth buffer to Windows to optimize hologram stability automatically, without your app specifying a focus point:</span></span>
> * <span data-ttu-id="43100-112">Sur un casque bureau immersif, cela permettra reprojection en fonction de profondeur de par pixel.</span><span class="sxs-lookup"><span data-stu-id="43100-112">On an immersive desktop headset, this will enable per-pixel depth-based reprojection.</span></span>
> * <span data-ttu-id="43100-113">Sur un HoloLens exécutant Windows 10 avril 2018 mettre à jour ou une version ultérieure, cette analyse le tampon de profondeur pour choisir un plan de stabilisation optimal automatiquement.</span><span class="sxs-lookup"><span data-stu-id="43100-113">On a HoloLens running the Windows 10 April 2018 Update or later, this will analyze the depth buffer to pick an optimal stabilization plane automatically.</span></span>
>
> <span data-ttu-id="43100-114">Chacune de ces approches doit fournir encore meilleure qualité d’image sans travail explicite par votre application pour sélectionner un point de focus chaque frame.</span><span class="sxs-lookup"><span data-stu-id="43100-114">Either approach should provide even better image quality without explicit work by your app to select a focus point each frame.</span></span>  <span data-ttu-id="43100-115">Notez que si vous fournissez manuellement un point de focus, qui remplacera le comportement automatique décrit ci-dessus et permet généralement de réduire la stabilité hologramme.</span><span class="sxs-lookup"><span data-stu-id="43100-115">Note that if you do provide a focus point manually, that will override the automatic behavior described above, and will usually reduce hologram stability.</span></span>  <span data-ttu-id="43100-116">En règle générale, vous devez spécifier un point de mise au point manuelle uniquement lorsque votre application s’exécute sur un HoloLens n’a pas encore été mis à jour pour les fenêtres de mettre à jour du 10 avril 2018.</span><span class="sxs-lookup"><span data-stu-id="43100-116">Generally, you should only specify a manual focus point when your app is running on a HoloLens that has not yet been updated to the Windows 10 April 2018 Update.</span></span>

### <a name="example"></a><span data-ttu-id="43100-117">Exemple</span><span class="sxs-lookup"><span data-stu-id="43100-117">Example</span></span>

<span data-ttu-id="43100-118">Il existe plusieurs façons de définir le Point de Focus, comme suggéré par les surcharges disponibles sur le *SetFocusPointForFrame* fonction statique.</span><span class="sxs-lookup"><span data-stu-id="43100-118">There are many ways to set the Focus Point, as suggested by the overloads available on the *SetFocusPointForFrame* static function.</span></span> <span data-ttu-id="43100-119">Présentée ci-dessous est un exemple simple de définir le plan de focus à l’objet fourni chaque frame :</span><span class="sxs-lookup"><span data-stu-id="43100-119">Presented below is a simple example to set the focus plane to the provided object each frame:</span></span>

```cs
public GameObject focusedObject;
void Update()
{
    // Normally the normal is best set to be the opposite of the main camera's 
    // forward vector.
    // If the content is actually all on a plane (like text), set the normal to 
    // the normal of the plane and ensure the user does not pass through the 
    // plane.
    var normal = -Camera.main.transform.forward;     
    var position = focusedObject.transform.position;
    UnityEngine.XR.WSA.HolographicSettings.SetFocusPointForFrame(position, normal);
}
```

<span data-ttu-id="43100-120">Notez que le simple code ci-dessus peut retrouver en réduisant la stabilité hologramme si l’objet ayant le focus se retrouve derrière l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="43100-120">Note that the simple code above may end up reducing hologram stability if the focused object ends up behind the user.</span></span>  <span data-ttu-id="43100-121">C’est pourquoi vous devez généralement définir « Activer le partage de mémoire tampon de profondeur » au lieu de spécifier manuellement un point de focus.</span><span class="sxs-lookup"><span data-stu-id="43100-121">This is why you should generally set "Enable Depth Buffer Sharing" instead of manually specifying a focus point.</span></span>

### <a name="see-also"></a><span data-ttu-id="43100-122">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="43100-122">See also</span></span>
* [<span data-ttu-id="43100-123">Plan de stabilisation</span><span class="sxs-lookup"><span data-stu-id="43100-123">Stabilization plane</span></span>](hologram-stability.md#stabilization-plane)
