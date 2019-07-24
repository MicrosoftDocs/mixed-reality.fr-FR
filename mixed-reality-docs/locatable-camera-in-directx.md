---
title: Appareil photo localisable dans DirectX
description: Explique comment utiliser l’appareil photo de point de vue dans une application HoloLens.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, appareil photo localisable, point de vue, PDV, unporoject, Media Foundation, MF, récepteur personnalisé, procédure pas à pas, exemple de code
ms.openlocfilehash: 374b61e3d9bb0e97d5f0c5c8e17a5c882a4ebcd3
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63516869"
---
# <a name="locatable-camera-in-directx"></a>Appareil photo localisable dans DirectX

Cette rubrique explique comment configurer un pipeline [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197(v=vs.85).aspx) pour accéder à l' [appareil photo](locatable-camera.md) dans une application DirectX, y compris les métadonnées de frame qui vous permettent de localiser les images produites dans le monde réel.

## <a name="windows-media-capture-and-media-foundation-development-imfattributes"></a>Développement Windows Media capture et Media Foundation: IMFAttributes

Chaque frame [d’image comprend un système de coordonnées](locatable-camera.md#images-with-coordinate-systems) , ainsi que deux transformations importantes. La transformation «vue» est mappée à partir du système de coordonnées fourni à l’appareil photo, et la «projection» est mappée de l’appareil photo aux pixels de l’image. Les transformations système de coordonnées et 2 sont incorporées en tant que métadonnées dans chaque frame d’image via le [IMFAttributes](https://msdn.microsoft.com/library/windows/desktop/ms704598(v=vs.85).aspx)de Media Foundation.

### <a name="sample-usage-of-reading-attributes-with-mf-custom-sink-and-doing-projection"></a>Exemple d’utilisation des attributs de lecture avec récepteur personnalisé MF et projection

Dans votre flux de récepteur MF personnalisé ([IMFStreamSink](https://msdn.microsoft.com/library/windows/desktop/ms705657(v=vs.85).aspx)), vous obtiendrez [IMFSample](https://msdn.microsoft.com/library/windows/desktop/ms702192(v=vs.85).aspx) avec des attributs d’exemple:

Le MediaExtensions suivant doit être défini pour le code basé sur WinRT:

```
EXTERN_GUID(MFSampleExtension_Spatial_CameraViewTransform, 0x4e251fa4, 0x830f, 0x4770, 0x85, 0x9a, 0x4b, 0x8d, 0x99, 0xaa, 0x80, 0x9b);
EXTERN_GUID(MFSampleExtension_Spatial_CameraCoordinateSystem, 0x9d13c82f, 0x2199, 0x4e67, 0x91, 0xcd, 0xd1, 0xa4, 0x18, 0x1f, 0x25, 0x34);
EXTERN_GUID(MFSampleExtension_Spatial_CameraProjectionTransform, 0x47f9fcb5, 0x2a02, 0x4f26, 0xa4, 0x77, 0x79, 0x2f, 0xdf, 0x95, 0x88, 0x6a);
```

Vous ne pouvez pas accéder à ces attributs à partir des API WinRT, mais nécessite l’implémentation d’extension de média de [IMFTransform](https://msdn.microsoft.com/library/windows/desktop/ms696260(v=vs.85).aspx) (pour Effect) ou [IMFMediaSink](https://msdn.microsoft.com/library/windows/desktop/ms694262(v=vs.85).aspx) et [IMFStreamSink](https://msdn.microsoft.com/library/windows/desktop/ms705657(v=vs.85).aspx) (pour un récepteur personnalisé). Lorsque vous traitez l’exemple dans cette extension dans [IMFTransform::P rocessinput ()](https://msdn.microsoft.com/library/windows/desktop/ms703131(v=vs.85).aspx)/[IMFTransform::P rocessoutput ()](https://msdn.microsoft.com/library/windows/desktop/ms704014(v=vs.85).aspx) ou [IMFStreamSink::P rocesssample ()](https://msdn.microsoft.com/library/windows/desktop/ms696208(v=vs.85).aspx), vous pouvez interroger des attributs comme cet exemple.

```
ComPtr<IUnknown> spUnknown;
ComPtr<Windows::Perception::Spatial::ISpatialCoordinateSystem> spSpatialCoordinateSystem;
ComPtr<Windows::Foundation::IReference<Windows::Foundation::Numerics::Matrix4x4>> spTransformRef;
Windows::Foundation::Numerics::Matrix4x4 worldToCameraMatrix;
Windows::Foundation::Numerics::Matrix4x4 viewMatrix;
Windows::Foundation::Numerics::Matrix4x4 projectionMatrix;
UINT32 cbBlobSize = 0;
hr = pSample->GetUnknown(MFSampleExtension_Spatial_CameraCoordinateSystem, IID_PPV_ARGS(&spUnknown));
if (SUCCEEDED(hr))
{
    hr = spUnknown.As(&spSpatialCoordinateSystem);
    if (FAILED(hr))
    {
        return hr;
    }
    hr = pSample->GetBlob(MFSampleExtension_Spatial_CameraViewTransform,
                          (UINT8*)(&viewMatrix),
                          sizeof(viewMatrix),
                          &cbBlobSize);
    if (SUCCEEDED(hr) && cbBlobSize == sizeof(Windows::Foundation::Numerics::Matrix4x4))
    {
        hr = pSample->GetBlob(MFSampleExtension_Spatial_CameraProjectionTransform,
                              (UINT8*)(&projectionMatrix),
                              sizeof(projectionMatrix),
                              &cbBlobSize);
        if (SUCCEEDED(hr) && cbBlobSize == sizeof(Windows::Foundation::Numerics::Matrix4x4))
        {
            // Assume m_spCurrentCoordinateSystem is representing
            // world coordinate system application is using
            hr = m_spCurrentCoordinateSystem->TryGetTransformTo(spSpatialCoordinateSystem.Get(),
                                                                &spTransformRef);
            if (FAILED(hr))
            {
                return hr;
            }
            hr = spTransformRef->get_Value(&worldToCameraMatrix);
            if (FAILED(hr))
            {
                return hr;
            }
        }
    }
}
```

Pour accéder à la texture à partir de l’appareil photo, vous avez besoin d’un même appareil D3D qui crée la texture du cadre de l’appareil photo. Ce périphérique D3D est dans [IMFDXGIDeviceManager](https://msdn.microsoft.com/library/windows/desktop/hh447906(v=vs.85).aspx) dans le pipeline de capture. Pour obtenir DXGI Device Manager à partir de la capture multimédia, vous pouvez utiliser les interfaces [IAdvancedMediaCapture](https://msdn.microsoft.com/library/windows/desktop/hh802709(v=vs.85).aspx) et [IAdvancedMediaCaptureSettings](https://msdn.microsoft.com/library/windows/desktop/hh802712(v=vs.85).aspx) .

```
Microsoft::WRL::ComPtr<IAdvancedMediaCapture> spAdvancedMediaCapture;
Microsoft::WRL::ComPtr<IAdvancedMediaCaptureSettings> spAdvancedMediaCaptureSettings;
Microsoft::WRL::ComPtr<IMFDXGIDeviceManager> spDXGIDeviceManager;
// Assume mediaCapture is Windows::Media::Capture::MediaCapture and initialized
if (SUCCEEDED(((IUnknown *)(mediaCapture))->QueryInterface(IID_PPV_ARGS(&spAdvancedMediaCapture))))
{
    if (SUCCEEDED(spAdvancedMediaCapture->GetAdvancedMediaCaptureSettings(&spAdvancedMediaCaptureSettings)))
    {
        spAdvancedMediaCaptureSettings->GetDirectxDeviceManager(&spDXGIDeviceManager);
    }
}
```

Vous pouvez également activer l’entrée de la souris et du clavier en tant que méthodes d’entrée facultatives pour votre application Windows Mixed Reality. Il peut également s’agir d’une fonctionnalité de débogage idéale pour les appareils tels que HoloLens, et peut être souhaitable pour une entrée d’utilisateur dans des applications de réalité mixte s’exécutant dans des casques immersifs attachés à des PC.
