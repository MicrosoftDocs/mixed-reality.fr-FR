---
title: Point de focus dans Unity
description: Réglage manuel de la stabilité des hologrammes dans Unity en définissant le point de focus
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, point de focalisation, plan de focalisation, plan de stabilisation, point de stabilisation, reprojection, LSR, tampon de profondeur
ms.openlocfilehash: 9a7f30b552242b24a9a7b260b6574690a27d2c1d
ms.sourcegitcommit: 7e8b9de561cbc8483e84511f3e9cbd779f3a999f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/27/2019
ms.locfileid: "75502620"
---
# <a name="focus-point-in-unity"></a><span data-ttu-id="04158-104">Point de focus dans Unity</span><span class="sxs-lookup"><span data-stu-id="04158-104">Focus point in Unity</span></span>

<span data-ttu-id="04158-105">**Espace de noms :** *UnityEngine. XR. WSA*</span><span class="sxs-lookup"><span data-stu-id="04158-105">**Namespace:** *UnityEngine.XR.WSA*</span></span><br>
<span data-ttu-id="04158-106">**Type**: *HolographicSettings*</span><span class="sxs-lookup"><span data-stu-id="04158-106">**Type**: *HolographicSettings*</span></span>

<span data-ttu-id="04158-107">Le [point de focus](hologram-stability.md#reprojection) peut être défini pour fournir à HoloLens une indication sur la façon d’effectuer la meilleure stabilisation sur les hologrammes actuellement affichés.</span><span class="sxs-lookup"><span data-stu-id="04158-107">The [focus point](hologram-stability.md#reprojection) can be set to provide HoloLens a hint about how to best perform stabilization on the holograms currently being displayed.</span></span>

<span data-ttu-id="04158-108">Si vous souhaitez définir le point de focus dans Unity, vous devez définir chaque frame à l’aide de *HolographicSettings. SetFocusPointForFrame ()* .</span><span class="sxs-lookup"><span data-stu-id="04158-108">If you want to set the Focus Point in Unity, it needs to be set every frame using *HolographicSettings.SetFocusPointForFrame()*.</span></span> <span data-ttu-id="04158-109">Si le point de focus n’est pas défini pour un frame, le plan de stabilisation par défaut est utilisé.</span><span class="sxs-lookup"><span data-stu-id="04158-109">If the Focus Point is not set for a frame, the default stabilization plane will be used.</span></span>

> [!NOTE]
> <span data-ttu-id="04158-110">Par défaut, l’option « Activer le partage de tampon de profondeur » est définie pour les nouveaux projets Unity.</span><span class="sxs-lookup"><span data-stu-id="04158-110">By default, new Unity projects have the "Enable Depth Buffer Sharing" option set.</span></span>  <span data-ttu-id="04158-111">Avec cette option, une application Unity s’exécutant sur un casque de bureau immersif ou sur un HoloLens exécutant la mise à jour 2018 d’avril de Windows 10 (RS4) ou une version ultérieure envoie votre tampon de profondeur à Windows pour optimiser la stabilité de l’hologramme automatiquement, sans que votre application spécifie un point de Focus :</span><span class="sxs-lookup"><span data-stu-id="04158-111">With this option, a Unity app running on either an immersive desktop headset or a HoloLens running the Windows 10 April 2018 Update (RS4) or later will submit your depth buffer to Windows to optimize hologram stability automatically, without your app specifying a focus point:</span></span>
> * <span data-ttu-id="04158-112">Sur un casque d’un bureau immersif, cela permet une reprojection basée sur la profondeur par pixel.</span><span class="sxs-lookup"><span data-stu-id="04158-112">On an immersive desktop headset, this will enable per-pixel depth-based reprojection.</span></span>
> * <span data-ttu-id="04158-113">Sur un HoloLens exécutant la mise à jour 2018 de Windows 10 avril ou une version ultérieure, le tampon de profondeur est analysé afin de choisir un plan de stabilisation optimal automatiquement.</span><span class="sxs-lookup"><span data-stu-id="04158-113">On a HoloLens running the Windows 10 April 2018 Update or later, this will analyze the depth buffer to pick an optimal stabilization plane automatically.</span></span>
>
> <span data-ttu-id="04158-114">L’une ou l’autre approche devrait offrir une meilleure qualité d’image sans travail explicite de votre application pour sélectionner un point de focus pour chaque frame.</span><span class="sxs-lookup"><span data-stu-id="04158-114">Either approach should provide even better image quality without explicit work by your app to select a focus point for each frame.</span></span>  <span data-ttu-id="04158-115">Notez que si vous fournissez un point de focalisation manuellement, cela remplacera le comportement automatique décrit ci-dessus et réduira généralement la stabilité de l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="04158-115">Note that if you do provide a focus point manually, that will override the automatic behavior described above, and will usually reduce hologram stability.</span></span>  <span data-ttu-id="04158-116">En règle générale, vous devez uniquement spécifier un point de focus manuel lorsque votre application s’exécute sur un HoloLens qui n’a pas encore été mis à jour vers la mise à jour 2018 d’avril de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="04158-116">Generally, you should only specify a manual focus point when your app is running on a HoloLens that has not yet been updated to the Windows 10 April 2018 Update.</span></span>

### <a name="example"></a><span data-ttu-id="04158-117">Exemple</span><span class="sxs-lookup"><span data-stu-id="04158-117">Example</span></span>

<span data-ttu-id="04158-118">Il existe de nombreuses façons de définir le point de focus, comme suggéré par les surcharges disponibles sur la fonction statique *SetFocusPointForFrame* .</span><span class="sxs-lookup"><span data-stu-id="04158-118">There are many ways to set the Focus Point, as suggested by the overloads available on the *SetFocusPointForFrame* static function.</span></span> <span data-ttu-id="04158-119">Vous trouverez ci-dessous un exemple simple pour définir le plan de focus sur l’objet fourni pour chaque frame :</span><span class="sxs-lookup"><span data-stu-id="04158-119">Presented below is a simple example to set the focus plane to the provided object for each frame:</span></span>

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

<span data-ttu-id="04158-120">Notez que le code simple ci-dessus peut finir par réduire la stabilité des hologrammes si l’objet ayant le focus se termine derrière l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="04158-120">Note that the simple code above may end up reducing hologram stability if the focused object ends up behind the user.</span></span>  <span data-ttu-id="04158-121">C’est la raison pour laquelle vous devez généralement définir « activer le partage de mémoire tampon de profondeur » au lieu de spécifier manuellement un point de focus.</span><span class="sxs-lookup"><span data-stu-id="04158-121">This is why you should generally set "Enable Depth Buffer Sharing" instead of manually specifying a focus point.</span></span>

### <a name="see-also"></a><span data-ttu-id="04158-122">Articles associés</span><span class="sxs-lookup"><span data-stu-id="04158-122">See also</span></span>
* [<span data-ttu-id="04158-123">Plan de stabilisation</span><span class="sxs-lookup"><span data-stu-id="04158-123">Stabilization plane</span></span>](hologram-stability.md#reprojection)
