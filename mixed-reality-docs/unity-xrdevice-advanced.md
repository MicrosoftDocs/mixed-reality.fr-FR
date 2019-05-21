---
title: Objets natifs réalité mixtes dans Unity
description: Obtenir un accès aux objets sous-jacents HOLOGRAPHIQUE natifs Unity.
author: vladkol
ms.author: vladkol
ms.date: 05/20/2018
ms.topic: article
keywords: Unity, mixte réalité natif, xrdevice, spatialcoordinatesystem, holographicframe, holographiccamera, ispatialcoordinatesystem, iholographicframe, iholographiccamera, getnativeptr
ms.openlocfilehash: 76073f5b2adfdf27cfbb153f95bb3a533d02e196
ms.sourcegitcommit: d565a69a9320e736304372b3f010af1a4d286a62
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65942095"
---
# <a name="mixed-reality-native-objects-in-unity"></a>Objets natifs réalité mixtes dans Unity

[Obtention d’un HolographicSpace](getting-a-holographicspace.md) est ce que chaque réalité mixte fait de l’application avant de démarrer la réception de données de l’appareil photo et le rendu des frames. Dans Unity, le moteur s’occupe de ces étapes pour vous, gestion des objets holographique et met à jour en interne dans le cadre de sa boucle de rendu.

Toutefois, dans les scénarios avancés, vous devrez peut-être accéder aux objets natifs sous-jacents, tels que le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera" target="_blank">HolographicCamera</a> et actuelles <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a>. <a href="https://docs.unity3d.com/ScriptReference/XR.XRDevice.html" target="_blank">UnityEngine.XR.XRDevice</a> fournit l’accès à ces objets natifs.

## <a name="xrdevice"></a>XRDevice 

**Namespace :** *UnityEngine.XR*<br>
**Type :** *XRDevice*

Le *XRDevice* type vous permet d’accéder aux objets natifs sous-jacents à l’aide de la <a href="https://docs.unity3d.com/ScriptReference/XR.XRDevice.GetNativePtr.html" target="_blank">GetNativePtr</a> (méthode). Ce que retourne GetNativePtr varie entre les différentes plateformes. Sur la plate-forme de Windows Universal, lorsque vous ciblez le SDK XR réalité mixte de Windows, XRDevice.GetNativePtr retourne un pointeur (IntPtr) vers la structure suivante : 

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
Vous pouvez la convertir en HolographicFrameNativeData à l’aide de la méthode de Marshal.PtrToStructure :
```cs
var nativePtr = UnityEngine.XR.XRDevice.GetNativePtr();
HolographicFrameNativeData hfd = Marshal.PtrToStructure<HolographicFrameNativeData>(nativePtr);
```
***IHolographicCameraPtr** est un tableau de IntPtr marshalé en tant que UnmanagedType.ByValArray avec une longueur égale à MaxNumberOfCameras* 


### <a name="using-holographicframenativedata"></a>À l’aide de HolographicFrameNativeData

> [!NOTE]
> Modification de l’état des objets natifs reçu via HolographicFrameNativeData risque de comportement imprévisible et des artefacts de rendu, en particulier si Unity raisons également sur ce même état.  Par exemple, vous ne devez pas appeler HolographicFrame.UpdateCurrentPrediction, sans quoi la prédiction de pose Unity s’affiche avec cette image sera pas synchronisée avec la pose que Windows attend, ce qui réduit [stabilité hologramme](hologram-stability.md).

Vous pouvez utiliser des données à partir de HolographicFrameNativeData lors de l’accès aux interfaces natives est requis pour le rendu ou le débogage, dans votre plug-ins natifs ou C# code. 

Voici un exemple de comment vous pouvez utiliser HolographicFrameNativeData pour obtenir la prédiction du frame actif pour le temps de photon. 
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
