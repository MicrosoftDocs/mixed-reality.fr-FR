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
# <a name="mixed-reality-native-objects-in-unity"></a>Objets natifs de réalité mixte dans Unity

L' [obtention d’un HolographicSpace](getting-a-holographicspace.md) est ce que fait chaque application de réalité mixte avant de commencer à recevoir des données de caméra et des frames de rendu. Dans Unity, le moteur s’occupe de ces étapes pour vous, en gérant les objets holographiques et les mises à jour en interne dans le cadre de sa boucle de rendu.

Toutefois, dans les scénarios avancés, vous devrez peut-être accéder aux objets natifs sous-jacents, tels que <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera" target="_blank">HolographicCamera</a> et <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a>actuel. <a href="https://docs.unity3d.com/ScriptReference/XR.XRDevice.html" target="_blank">UnityEngine. XR. XRDevice</a> est ce qui permet d’accéder à ces objets natifs.

## <a name="xrdevice"></a>XRDevice 

**Espace de noms :** *UnityEngine. XR*<br>
**Type :** *XRDevice*

Le type *XRDevice* vous permet d’accéder aux objets natifs sous-jacents à l’aide de la méthode <a href="https://docs.unity3d.com/ScriptReference/XR.XRDevice.GetNativePtr.html" target="_blank">GetNativePtr</a> . Ce que GetNativePtr retourne varie entre différentes plateformes. Sur la plateforme Windows universelle, quand vous ciblez le kit de développement logiciel (SDK) XR Windows Mixed Reality, XRDevice. GetNativePtr retourne un pointeur (IntPtr) à la structure suivante: 

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
Vous pouvez la convertir en HolographicFrameNativeData à l’aide de la méthode Marshal. PtrToStructure provoquent:
```cs
var nativePtr = UnityEngine.XR.XRDevice.GetNativePtr();
HolographicFrameNativeData hfd = Marshal.PtrToStructure<HolographicFrameNativeData>(nativePtr);
```
***IHolographicCameraPtr** est un tableau de IntPtr marshalé en tant que UnmanagedType. ByValArray avec une longueur égale à MaxNumberOfCameras* 


### <a name="using-holographicframenativedata"></a>Utilisation de HolographicFrameNativeData

> [!NOTE]
> La modification de l’état des objets natifs reçus via HolographicFrameNativeData peut entraîner un comportement imprévisible et des artefacts de rendu, en particulier si Unity a également des raisons de ce même État.  Par exemple, vous ne devez pas appeler HolographicFrame. UpdateCurrentPrediction, ou la prédiction de pose que les rendus Unity avec cette image ne seront pas synchronisées avec la pose attendue par Windows, ce qui réduira la stabilité de l' [hologramme](hologram-stability.md).

Vous pouvez utiliser les données de HolographicFrameNativeData lorsque l’accès aux interfaces natives est nécessaire à des fins de rendu ou de débogage, C# dans vos plug-ins natifs ou votre code. 

Voici un exemple de la façon dont vous pouvez utiliser HolographicFrameNativeData pour obtenir la prédiction du frame actuel pour l’heure de la photonique. 
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

## <a name="see-also"></a>Voir aussi
* <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a>
* <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a>
* <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera" target="_blank">HolographicCamera</a>
* [Rendu dans DirectX](rendering-in-directx.md)
