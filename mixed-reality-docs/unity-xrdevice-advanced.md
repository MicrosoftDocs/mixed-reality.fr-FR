---
title: Objets natifs de réalité mixte dans Unity
description: Accédez aux objets natifs holographiques sous-jacents dans Unity.
author: vladkol
ms.author: vladkol
ms.date: 05/20/2018
ms.topic: article
keywords: Unity, réalité mixte, native, xrdevice, spatialcoordinatesystem, holographicframe, holographiccamera, ispatialcoordinatesystem, iholographicframe, iholographiccamera, getnativeptr
ms.openlocfilehash: 76073f5b2adfdf27cfbb153f95bb3a533d02e196
ms.sourcegitcommit: d565a69a9320e736304372b3f010af1a4d286a62
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65942095"
---
# <a name="mixed-reality-native-objects-in-unity"></a><span data-ttu-id="3063f-104">Objets natifs de réalité mixte dans Unity</span><span class="sxs-lookup"><span data-stu-id="3063f-104">Mixed Reality native objects in Unity</span></span>

<span data-ttu-id="3063f-105">L' [obtention d’un HolographicSpace](getting-a-holographicspace.md) est ce que fait chaque application de réalité mixte avant de commencer à recevoir des données de caméra et des frames de rendu.</span><span class="sxs-lookup"><span data-stu-id="3063f-105">[Getting a HolographicSpace](getting-a-holographicspace.md) is what every Mixed Reality app does before it starts receiving camera data and rendering frames.</span></span> <span data-ttu-id="3063f-106">Dans Unity, le moteur s’occupe de ces étapes pour vous, en gérant les objets holographiques et les mises à jour en interne dans le cadre de sa boucle de rendu.</span><span class="sxs-lookup"><span data-stu-id="3063f-106">In Unity, the engine takes care of those steps for you, handling Holographic objects and updates internally as part of its render loop.</span></span>

<span data-ttu-id="3063f-107">Toutefois, dans les scénarios avancés, vous devrez peut-être accéder aux objets natifs sous-jacents, tels que <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera" target="_blank">HolographicCamera</a> et <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a>actuel.</span><span class="sxs-lookup"><span data-stu-id="3063f-107">However, in advanced scenarios you may need to get access to the underlying native objects, such as the <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera" target="_blank">HolographicCamera</a> and current <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a>.</span></span> <span data-ttu-id="3063f-108"><a href="https://docs.unity3d.com/ScriptReference/XR.XRDevice.html" target="_blank">UnityEngine. XR. XRDevice</a> est ce qui permet d’accéder à ces objets natifs.</span><span class="sxs-lookup"><span data-stu-id="3063f-108"><a href="https://docs.unity3d.com/ScriptReference/XR.XRDevice.html" target="_blank">UnityEngine.XR.XRDevice</a> is what provides access to these native objects.</span></span>

## <a name="xrdevice"></a><span data-ttu-id="3063f-109">XRDevice</span><span class="sxs-lookup"><span data-stu-id="3063f-109">XRDevice</span></span> 

<span data-ttu-id="3063f-110">**Espace de noms :** *UnityEngine. XR*</span><span class="sxs-lookup"><span data-stu-id="3063f-110">**Namespace:** *UnityEngine.XR*</span></span><br>
<span data-ttu-id="3063f-111">**Type :** *XRDevice*</span><span class="sxs-lookup"><span data-stu-id="3063f-111">**Type:** *XRDevice*</span></span>

<span data-ttu-id="3063f-112">Le type *XRDevice* vous permet d’accéder aux objets natifs sous-jacents à l’aide de la méthode <a href="https://docs.unity3d.com/ScriptReference/XR.XRDevice.GetNativePtr.html" target="_blank">GetNativePtr</a> .</span><span class="sxs-lookup"><span data-stu-id="3063f-112">The *XRDevice* type allows you to get access to underlying native objects using the <a href="https://docs.unity3d.com/ScriptReference/XR.XRDevice.GetNativePtr.html" target="_blank">GetNativePtr</a> method.</span></span> <span data-ttu-id="3063f-113">Ce que GetNativePtr retourne varie entre différentes plateformes.</span><span class="sxs-lookup"><span data-stu-id="3063f-113">What GetNativePtr returns varies between different platforms.</span></span> <span data-ttu-id="3063f-114">Sur la plateforme Windows universelle, quand vous ciblez le kit de développement logiciel (SDK) XR Windows Mixed Reality, XRDevice. GetNativePtr retourne un pointeur (IntPtr) à la structure suivante:</span><span class="sxs-lookup"><span data-stu-id="3063f-114">On the Universal Windows Platform, when targeting the Windows Mixed Reality XR SDK, XRDevice.GetNativePtr returns a pointer (IntPtr) to the following structure:</span></span> 

```cs
using System;
using System.Runtime.InteropServices;

[StructLayout(LayoutKind.Sequential)]
struct HolographicFrameNativeData
{
    public uint VersionNumber;
    public uint MaxNumberOfCameras;
    public IntPtr ISpatialCoordinateSystemPtr; // Windows::Perception::Spatial::ISpatialCoordinateSystem
    public IntPtr IHolographicFramePtr; // Windows::Graphics::Holographic::IHolographicFrame 
    public IntPtr IHolographicCameraPtr; // // Windows::Graphics::Holographic::IHolographicCamera
}
```
<span data-ttu-id="3063f-115">Vous pouvez la convertir en HolographicFrameNativeData à l’aide de la méthode Marshal. PtrToStructure provoquent:</span><span class="sxs-lookup"><span data-stu-id="3063f-115">You can convert it to HolographicFrameNativeData using Marshal.PtrToStructure method:</span></span>
```cs
var nativePtr = UnityEngine.XR.XRDevice.GetNativePtr();
HolographicFrameNativeData hfd = Marshal.PtrToStructure<HolographicFrameNativeData>(nativePtr);
```
<span data-ttu-id="3063f-116">***IHolographicCameraPtr** est un tableau de IntPtr marshalé en tant que UnmanagedType. ByValArray avec une longueur égale à MaxNumberOfCameras*</span><span class="sxs-lookup"><span data-stu-id="3063f-116">***IHolographicCameraPtr** is an array of IntPtr marshaled as UnmanagedType.ByValArray with a length equal to MaxNumberOfCameras*</span></span> 


### <a name="using-holographicframenativedata"></a><span data-ttu-id="3063f-117">Utilisation de HolographicFrameNativeData</span><span class="sxs-lookup"><span data-stu-id="3063f-117">Using HolographicFrameNativeData</span></span>

> [!NOTE]
> <span data-ttu-id="3063f-118">La modification de l’état des objets natifs reçus via HolographicFrameNativeData peut entraîner un comportement imprévisible et des artefacts de rendu, en particulier si Unity a également des raisons de ce même État.</span><span class="sxs-lookup"><span data-stu-id="3063f-118">Changing the state of the native objects received via HolographicFrameNativeData may cause unpredictable behaviour and rendering artifacts, especially if Unity also reasons about that same state.</span></span>  <span data-ttu-id="3063f-119">Par exemple, vous ne devez pas appeler HolographicFrame. UpdateCurrentPrediction, ou la prédiction de pose que les rendus Unity avec cette image ne seront pas synchronisées avec la pose attendue par Windows, ce qui réduira la stabilité de l' [hologramme](hologram-stability.md).</span><span class="sxs-lookup"><span data-stu-id="3063f-119">For example, you should not call HolographicFrame.UpdateCurrentPrediction, or else the pose prediction that Unity renders with that frame will be out of sync with the pose that Windows is expecting, which will reduce [hologram stability](hologram-stability.md).</span></span>

<span data-ttu-id="3063f-120">Vous pouvez utiliser les données de HolographicFrameNativeData lorsque l’accès aux interfaces natives est nécessaire à des fins de rendu ou de débogage, C# dans vos plug-ins natifs ou votre code.</span><span class="sxs-lookup"><span data-stu-id="3063f-120">You can use data from HolographicFrameNativeData when access to native interfaces is required for rendering or debugging purposes, in your native plugins or C# code.</span></span> 

<span data-ttu-id="3063f-121">Voici un exemple de la façon dont vous pouvez utiliser HolographicFrameNativeData pour obtenir la prédiction du frame actuel pour l’heure de la photonique.</span><span class="sxs-lookup"><span data-stu-id="3063f-121">Here is an example of how you can use HolographicFrameNativeData to get the current frame's prediction for photon time.</span></span> 
```cs
using System;
using System.Runtime.InteropServices;

public static bool GetCurrentFrameDateTime(out DateTime frameDateTime)
{
#if (!UNITY_EDITOR && UNITY_WSA) || ENABLE_WINMD_SUPPORT
    IntPtr nativeStruct = UnityEngine.XR.XRDevice.GetNativePtr();

    if (nativeStruct != IntPtr.Zero)
    {
        HolographicFrameNativeData hfd = Marshal.PtrToStructure<HolographicFrameNativeData>(nativeStruct);

        if (hfd.IHolographicFramePtr != IntPtr.Zero)
        {
            var holographicFrame = (Windows.Graphics.Holographic.HolographicFrame)Marshal.GetObjectForIUnknown(hfd.IHolographicFramePtr);
            frameDateTime = holographicFrame.CurrentPrediction.Timestamp.TargetTime.DateTime;
            return true;
        }
    }

#endif

    frameDateTime = DateTime.MinValue;
    return false;
}

```

## <a name="see-also"></a><span data-ttu-id="3063f-122">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3063f-122">See Also</span></span>
* <span data-ttu-id="3063f-123"><a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a></span><span class="sxs-lookup"><span data-stu-id="3063f-123"><a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a></span></span>
* <span data-ttu-id="3063f-124"><a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a></span><span class="sxs-lookup"><span data-stu-id="3063f-124"><a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a></span></span>
* <span data-ttu-id="3063f-125"><a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera" target="_blank">HolographicCamera</a></span><span class="sxs-lookup"><span data-stu-id="3063f-125"><a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera" target="_blank">HolographicCamera</a></span></span>
* [<span data-ttu-id="3063f-126">Rendu dans DirectX</span><span class="sxs-lookup"><span data-stu-id="3063f-126">Rendering in DirectX</span></span>](rendering-in-directx.md)
