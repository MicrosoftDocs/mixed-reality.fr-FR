---
title: Objets natifs de réalité mixte dans Unity
description: Accédez aux objets natifs holographiques sous-jacents dans Unity.
author: vladkol
ms.author: vladkol
ms.date: 05/20/2018
ms.topic: article
keywords: Unity, réalité mixte, native, xrdevice, spatialcoordinatesystem, holographicframe, holographiccamera, ispatialcoordinatesystem, iholographicframe, iholographiccamera, getnativeptr
ms.openlocfilehash: 975775f64a19fe5fff4bc395a3e954cbf529dfa9
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437332"
---
# <a name="mixed-reality-native-objects-in-unity"></a><span data-ttu-id="646ca-104">Objets natifs de réalité mixte dans Unity</span><span class="sxs-lookup"><span data-stu-id="646ca-104">Mixed Reality native objects in Unity</span></span>

<span data-ttu-id="646ca-105">L' [obtention d’un HolographicSpace](getting-a-holographicspace.md) est ce que fait chaque application de réalité mixte avant de commencer à recevoir des données de caméra et des frames de rendu.</span><span class="sxs-lookup"><span data-stu-id="646ca-105">[Getting a HolographicSpace](getting-a-holographicspace.md) is what every Mixed Reality app does before it starts receiving camera data and rendering frames.</span></span> <span data-ttu-id="646ca-106">Dans Unity, le moteur s’occupe de ces étapes pour vous, en gérant les objets holographiques et les mises à jour en interne dans le cadre de sa boucle de rendu.</span><span class="sxs-lookup"><span data-stu-id="646ca-106">In Unity, the engine takes care of those steps for you, handling Holographic objects and updates internally as part of its render loop.</span></span>

<span data-ttu-id="646ca-107">Toutefois, dans les scénarios avancés, vous devrez peut-être accéder aux objets natifs sous-jacents, tels que <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera" target="_blank">HolographicCamera</a> et <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a>actuel.</span><span class="sxs-lookup"><span data-stu-id="646ca-107">However, in advanced scenarios you may need to get access to the underlying native objects, such as the <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera" target="_blank">HolographicCamera</a> and current <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a>.</span></span> <span data-ttu-id="646ca-108"><a href="https://docs.unity3d.com/ScriptReference/XR.XRDevice.html" target="_blank">UnityEngine. XR. XRDevice</a> est ce qui permet d’accéder à ces objets natifs.</span><span class="sxs-lookup"><span data-stu-id="646ca-108"><a href="https://docs.unity3d.com/ScriptReference/XR.XRDevice.html" target="_blank">UnityEngine.XR.XRDevice</a> is what provides access to these native objects.</span></span>

## <a name="xrdevice"></a><span data-ttu-id="646ca-109">XRDevice</span><span class="sxs-lookup"><span data-stu-id="646ca-109">XRDevice</span></span> 

<span data-ttu-id="646ca-110">**Espace de noms :** *UnityEngine. XR*</span><span class="sxs-lookup"><span data-stu-id="646ca-110">**Namespace:** *UnityEngine.XR*</span></span><br>
<span data-ttu-id="646ca-111">**Type :** *XRDevice*</span><span class="sxs-lookup"><span data-stu-id="646ca-111">**Type:** *XRDevice*</span></span>

<span data-ttu-id="646ca-112">Le type *XRDevice* vous permet d’accéder aux objets natifs sous-jacents à l’aide de la méthode <a href="https://docs.unity3d.com/ScriptReference/XR.XRDevice.GetNativePtr.html" target="_blank">GetNativePtr</a> .</span><span class="sxs-lookup"><span data-stu-id="646ca-112">The *XRDevice* type allows you to get access to underlying native objects using the <a href="https://docs.unity3d.com/ScriptReference/XR.XRDevice.GetNativePtr.html" target="_blank">GetNativePtr</a> method.</span></span> <span data-ttu-id="646ca-113">Ce que GetNativePtr retourne varie entre différentes plateformes.</span><span class="sxs-lookup"><span data-stu-id="646ca-113">What GetNativePtr returns varies between different platforms.</span></span> <span data-ttu-id="646ca-114">Sur la plateforme Windows universelle, quand vous ciblez le kit de développement logiciel (SDK) XR Windows Mixed Reality, XRDevice. GetNativePtr retourne un pointeur (IntPtr) à la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="646ca-114">On the Universal Windows Platform, when targeting the Windows Mixed Reality XR SDK, XRDevice.GetNativePtr returns a pointer (IntPtr) to the following structure:</span></span> 

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
<span data-ttu-id="646ca-115">Vous pouvez la convertir en HolographicFrameNativeData à l’aide de la méthode Marshal. PtrToStructure provoquent :</span><span class="sxs-lookup"><span data-stu-id="646ca-115">You can convert it to HolographicFrameNativeData using Marshal.PtrToStructure method:</span></span>
```cs
var nativePtr = UnityEngine.XR.XRDevice.GetNativePtr();
HolographicFrameNativeData hfd = Marshal.PtrToStructure<HolographicFrameNativeData>(nativePtr);
```
<span data-ttu-id="646ca-116">***IHolographicCameraPtr** est un tableau de IntPtr marshalé en tant que UnmanagedType. ByValArray avec une longueur égale à MaxNumberOfCameras*</span><span class="sxs-lookup"><span data-stu-id="646ca-116">***IHolographicCameraPtr** is an array of IntPtr marshaled as UnmanagedType.ByValArray with a length equal to MaxNumberOfCameras*</span></span> 

### <a name="unmarshaling-native-pointers"></a><span data-ttu-id="646ca-117">Démarshaler des pointeurs natifs</span><span class="sxs-lookup"><span data-stu-id="646ca-117">Unmarshaling native pointers</span></span>

<span data-ttu-id="646ca-118">Si vous utilisez [Microsoft. Windows. MixedReality. DotNetWinRT,](https://www.nuget.org/packages/Microsoft.Windows.MixedReality.DotNetWinRT) vous pouvez construire un objet managé à partir d’un pointeur natif à l’aide de la méthode `FromNativePtr()` :</span><span class="sxs-lookup"><span data-stu-id="646ca-118">If you are using [Microsoft.Windows.MixedReality.DotNetWinRT](https://www.nuget.org/packages/Microsoft.Windows.MixedReality.DotNetWinRT) you can construct a managed object from a native pointer using the `FromNativePtr()` method:</span></span>

```cs
var worldOrigin = Microsoft.Windows.Perception.Spatial.SpatialCoordinateSystem.FromNativePtr(hfd.ISpatialCoordinateSystemPtr);
```

<span data-ttu-id="646ca-119">Sinon, utilisez `Marshal.GetObjectForIUnknown()` et effectuez un cast vers le type souhaité :</span><span class="sxs-lookup"><span data-stu-id="646ca-119">Otherwise, use `Marshal.GetObjectForIUnknown()` and cast to the desired type:</span></span>

```cs
#if ENABLE_WINMD_SUPPORT
var worldOrigin = (Windows.Perception.Spatial.SpatialCoordinateSystem)Marshal.GetObjectForIUnknown(hfd.ISpatialCoordinateSystemPtr);
#endif
```

### <a name="converting-between-coordinate-systems"></a><span data-ttu-id="646ca-120">Conversion entre des systèmes de coordonnées</span><span class="sxs-lookup"><span data-stu-id="646ca-120">Converting between coordinate systems</span></span>

<span data-ttu-id="646ca-121">Unity utilise un système de coordonnées gauche, tandis que les API de perception de Windows utilisent des systèmes de coordonnées droitiers.</span><span class="sxs-lookup"><span data-stu-id="646ca-121">Unity uses a left-handed coordinate system, while the Windows Perception APIs use right-handed coordinate systems.</span></span> <span data-ttu-id="646ca-122">Pour effectuer une conversion entre ces deux conventions, vous pouvez utiliser les applications d’assistance suivantes :</span><span class="sxs-lookup"><span data-stu-id="646ca-122">To convert between these two conventions, you can use the following helpers:</span></span>

```cs
namespace NumericsConversion
{
    public static class NumericsConversionExtensions
    {
        public static UnityEngine.Vector3 ToUnity(this System.Numerics.Vector3 v) => new UnityEngine.Vector3(v.X, v.Y, -v.Z);
        public static UnityEngine.Quaternion ToUnity(this System.Numerics.Quaternion q) => new UnityEngine.Quaternion(-q.X, -q.Y, q.Z, q.W);
        public static UnityEngine.Matrix4x4 ToUnity(this System.Numerics.Matrix4x4 m) => new UnityEngine.Matrix4x4(
            new Vector4( m.M11,  m.M12, -m.M13,  m.M14),
            new Vector4( m.M21,  m.M22, -m.M23,  m.M24),
            new Vector4(-m.M31, -m.M32,  m.M33, -m.M34),
            new Vector4( m.M41,  m.M42, -m.M43,  m.M44));

        public static System.Numerics.Vector3 ToSystem(this UnityEngine.Vector3 v) => new System.Numerics.Vector3(v.x, v.y, -v.z);
        public static System.Numerics.Quaternion ToSystem(this UnityEngine.Quaternion q) => new System.Numerics.Quaternion(-q.x, -q.y, q.z, q.w);
        public static System.Numerics.Matrix4x4 ToSystem(this UnityEngine.Matrix4x4 m) => new System.Numerics.Matrix4x4(
            m.m00,  m.m10, -m.m20,  m.m30,
            m.m01,  m.m11, -m.m21,  m.m31,
           -m.m02, -m.m12,  m.m22, -m.m32,
            m.m03,  m.m13, -m.m23,  m.m33);
    }
}
```

### <a name="using-holographicframe-native-data"></a><span data-ttu-id="646ca-123">Utilisation de données natives HolographicFrame</span><span class="sxs-lookup"><span data-stu-id="646ca-123">Using HolographicFrame native data</span></span>

> [!NOTE]
> <span data-ttu-id="646ca-124">La modification de l’état des objets natifs reçus via HolographicFrameNativeData peut entraîner un comportement imprévisible et des artefacts de rendu, en particulier si Unity a également des raisons de ce même État.</span><span class="sxs-lookup"><span data-stu-id="646ca-124">Changing the state of the native objects received via HolographicFrameNativeData may cause unpredictable behaviour and rendering artifacts, especially if Unity also reasons about that same state.</span></span>  <span data-ttu-id="646ca-125">Par exemple, vous ne devez pas appeler HolographicFrame. UpdateCurrentPrediction, ou la prédiction de pose que les rendus Unity avec cette image ne seront pas synchronisées avec la pose attendue par Windows, ce qui réduira la stabilité de l' [hologramme](hologram-stability.md).</span><span class="sxs-lookup"><span data-stu-id="646ca-125">For example, you should not call HolographicFrame.UpdateCurrentPrediction, or else the pose prediction that Unity renders with that frame will be out of sync with the pose that Windows is expecting, which will reduce [hologram stability](hologram-stability.md).</span></span>

<span data-ttu-id="646ca-126">Vous pouvez utiliser les données de HolographicFrameNativeData lorsque l’accès aux interfaces natives est nécessaire à des fins de rendu ou de débogage, C# dans vos plug-ins natifs ou votre code.</span><span class="sxs-lookup"><span data-stu-id="646ca-126">You can use data from HolographicFrameNativeData when access to native interfaces is required for rendering or debugging purposes, in your native plugins or C# code.</span></span> 

<span data-ttu-id="646ca-127">Voici un exemple de la façon dont vous pouvez utiliser HolographicFrameNativeData pour obtenir la prédiction du frame actuel pour l’heure de la photonique.</span><span class="sxs-lookup"><span data-stu-id="646ca-127">Here is an example of how you can use HolographicFrameNativeData to get the current frame's prediction for photon time.</span></span> 
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

## <a name="see-also"></a><span data-ttu-id="646ca-128">Articles associés</span><span class="sxs-lookup"><span data-stu-id="646ca-128">See Also</span></span>
* [<span data-ttu-id="646ca-129">Utilisation de l’espace de noms Windows avec les applications Unity pour HoloLens</span><span class="sxs-lookup"><span data-stu-id="646ca-129">Using the Windows namespace with Unity apps for HoloLens</span></span>](using-the-windows-namespace-with-unity-apps-for-hololens.md)
* <span data-ttu-id="646ca-130"><a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a></span><span class="sxs-lookup"><span data-stu-id="646ca-130"><a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a></span></span>
* <span data-ttu-id="646ca-131"><a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a></span><span class="sxs-lookup"><span data-stu-id="646ca-131"><a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a></span></span>
* <span data-ttu-id="646ca-132"><a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera" target="_blank">HolographicCamera</a></span><span class="sxs-lookup"><span data-stu-id="646ca-132"><a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera" target="_blank">HolographicCamera</a></span></span>
* [<span data-ttu-id="646ca-133">Rendu dans DirectX</span><span class="sxs-lookup"><span data-stu-id="646ca-133">Rendering in DirectX</span></span>](rendering-in-directx.md)
