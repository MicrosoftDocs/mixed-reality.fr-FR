---
title: Caméra localisable dans DirectX
description: Explique comment utiliser l’appareil photo (PDV) de point de vue dans une application de HoloLens.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, appareil photo localisable, le point de vue, des PDV, unporoject, foundation media, MF, canal personnalisé, procédure pas à pas, exemple de code
ms.openlocfilehash: 374b61e3d9bb0e97d5f0c5c8e17a5c882a4ebcd3
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595303"
---
# <a name="locatable-camera-in-directx"></a><span data-ttu-id="cf030-104">Caméra localisable dans DirectX</span><span class="sxs-lookup"><span data-stu-id="cf030-104">Locatable camera in DirectX</span></span>

<span data-ttu-id="cf030-105">Cette rubrique décrit comment configurer un [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197(v=vs.85).aspx) de pipeline pour accéder à la [caméra](locatable-camera.md) dans une application DirectX, y compris les métadonnées d’image qui vous permet de localiser les images de produits dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="cf030-105">This topic describes how to set up a [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197(v=vs.85).aspx) pipeline to access the [camera](locatable-camera.md) in a DirectX app, including the frame metadata that will allow you to locate the images produced in the real world.</span></span>

## <a name="windows-media-capture-and-media-foundation-development-imfattributes"></a><span data-ttu-id="cf030-106">Capture de média de Windows et le développement de Media Foundation : IMFAttributes</span><span class="sxs-lookup"><span data-stu-id="cf030-106">Windows Media Capture and Media Foundation Development: IMFAttributes</span></span>

<span data-ttu-id="cf030-107">Chaque trame d’image [inclut un système de coordonnées](locatable-camera.md#images-with-coordinate-systems) , ainsi que les deux transformations importantes.</span><span class="sxs-lookup"><span data-stu-id="cf030-107">Each image frame [includes a coordinate system](locatable-camera.md#images-with-coordinate-systems) , as well as two important transforms.</span></span> <span data-ttu-id="cf030-108">La « vue » transformer des mappages depuis le système de coordonnées fourni à l’appareil photo et « projection » est mappé à partir de l’appareil photo pixels dans l’image.</span><span class="sxs-lookup"><span data-stu-id="cf030-108">The "view" transform maps from the provided coordinate system to the camera, and the "projection" maps from the camera to pixels in the image.</span></span> <span data-ttu-id="cf030-109">Le système de coordonnées et 2 transformations sont incorporées en tant que métadonnées dans chaque trame d’image par le biais de Media Foundation [IMFAttributes](https://msdn.microsoft.com/library/windows/desktop/ms704598(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="cf030-109">The coordinate system and the 2 transforms are embedded as metadata in every image frame via Media Foundation's [IMFAttributes](https://msdn.microsoft.com/library/windows/desktop/ms704598(v=vs.85).aspx).</span></span>

### <a name="sample-usage-of-reading-attributes-with-mf-custom-sink-and-doing-projection"></a><span data-ttu-id="cf030-110">Exemple d’utilisation de la lecture des attributs de récepteur personnalisée MF et faire de projection</span><span class="sxs-lookup"><span data-stu-id="cf030-110">Sample usage of reading attributes with MF custom sink and doing projection</span></span>

<span data-ttu-id="cf030-111">Dans votre flux MF récepteur personnalisée ([IMFStreamSink](https://msdn.microsoft.com/library/windows/desktop/ms705657(v=vs.85).aspx)), vous obtiendrez [IMFSample](https://msdn.microsoft.com/library/windows/desktop/ms702192(v=vs.85).aspx) avec des attributs de l’exemple :</span><span class="sxs-lookup"><span data-stu-id="cf030-111">In your custom MF Sink stream ([IMFStreamSink](https://msdn.microsoft.com/library/windows/desktop/ms705657(v=vs.85).aspx)), you will get [IMFSample](https://msdn.microsoft.com/library/windows/desktop/ms702192(v=vs.85).aspx) with sample attributes:</span></span>

<span data-ttu-id="cf030-112">Les MediaExtensions suivantes doit être définies pour le code de WinRT en :</span><span class="sxs-lookup"><span data-stu-id="cf030-112">The following MediaExtensions must be defined for WinRT based code:</span></span>

```
EXTERN_GUID(MFSampleExtension_Spatial_CameraViewTransform, 0x4e251fa4, 0x830f, 0x4770, 0x85, 0x9a, 0x4b, 0x8d, 0x99, 0xaa, 0x80, 0x9b);
EXTERN_GUID(MFSampleExtension_Spatial_CameraCoordinateSystem, 0x9d13c82f, 0x2199, 0x4e67, 0x91, 0xcd, 0xd1, 0xa4, 0x18, 0x1f, 0x25, 0x34);
EXTERN_GUID(MFSampleExtension_Spatial_CameraProjectionTransform, 0x47f9fcb5, 0x2a02, 0x4f26, 0xa4, 0x77, 0x79, 0x2f, 0xdf, 0x95, 0x88, 0x6a);
```

<span data-ttu-id="cf030-113">Vous ne peut pas accéder à ces attributs à partir de WinRT APIs, mais nécessite l’implémentation d’Extension de support de [IMFTransform](https://msdn.microsoft.com/library/windows/desktop/ms696260(v=vs.85).aspx) (pour l’effet) ou [IMFMediaSink](https://msdn.microsoft.com/library/windows/desktop/ms694262(v=vs.85).aspx) et [IMFStreamSink](https://msdn.microsoft.com/library/windows/desktop/ms705657(v=vs.85).aspx) () pour le récepteur personnalisé).</span><span class="sxs-lookup"><span data-stu-id="cf030-113">You can't access these attributes from WinRT APIs, but requires Media Extension implementation of [IMFTransform](https://msdn.microsoft.com/library/windows/desktop/ms696260(v=vs.85).aspx) (for Effect) or [IMFMediaSink](https://msdn.microsoft.com/library/windows/desktop/ms694262(v=vs.85).aspx) and [IMFStreamSink](https://msdn.microsoft.com/library/windows/desktop/ms705657(v=vs.85).aspx) (for Custom Sink).</span></span> <span data-ttu-id="cf030-114">Lorsque vous traitez l’exemple dans cette extension soit dans [IMFTransform::ProcessInput()](https://msdn.microsoft.com/library/windows/desktop/ms703131(v=vs.85).aspx)/[IMFTransform::ProcessOutput()](https://msdn.microsoft.com/library/windows/desktop/ms704014(v=vs.85).aspx) ou [IMFStreamSink::ProcessSample() ](https://msdn.microsoft.com/library/windows/desktop/ms696208(v=vs.85).aspx), vous pouvez interroger les attributs tels que cet exemple.</span><span class="sxs-lookup"><span data-stu-id="cf030-114">When you process the sample in this extension either in [IMFTransform::ProcessInput()](https://msdn.microsoft.com/library/windows/desktop/ms703131(v=vs.85).aspx)/[IMFTransform::ProcessOutput()](https://msdn.microsoft.com/library/windows/desktop/ms704014(v=vs.85).aspx) or [IMFStreamSink::ProcessSample()](https://msdn.microsoft.com/library/windows/desktop/ms696208(v=vs.85).aspx), you can query attributes like this sample.</span></span>

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

<span data-ttu-id="cf030-115">Pour accéder à la texture à partir de l’appareil photo, vous avez besoin d’un même périphérique D3D qui crée la texture de frame d’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="cf030-115">To access the texture from the camera, you need same D3D device which creates camera frame texture.</span></span> <span data-ttu-id="cf030-116">Ce périphérique D3D est [IMFDXGIDeviceManager](https://msdn.microsoft.com/library/windows/desktop/hh447906(v=vs.85).aspx) dans le pipeline de capture.</span><span class="sxs-lookup"><span data-stu-id="cf030-116">This D3D device is in [IMFDXGIDeviceManager](https://msdn.microsoft.com/library/windows/desktop/hh447906(v=vs.85).aspx) in the capture pipeline.</span></span> <span data-ttu-id="cf030-117">Pour obtenir le Gestionnaire de périphériques de DXGI à partir de la Capture de média que vous pouvez utiliser [IAdvancedMediaCapture](https://msdn.microsoft.com/library/windows/desktop/hh802709(v=vs.85).aspx) et [IAdvancedMediaCaptureSettings](https://msdn.microsoft.com/library/windows/desktop/hh802712(v=vs.85).aspx) interfaces.</span><span class="sxs-lookup"><span data-stu-id="cf030-117">To get the DXGI Device manager from Media Capture you can use [IAdvancedMediaCapture](https://msdn.microsoft.com/library/windows/desktop/hh802709(v=vs.85).aspx) and [IAdvancedMediaCaptureSettings](https://msdn.microsoft.com/library/windows/desktop/hh802712(v=vs.85).aspx) interfaces.</span></span>

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

<span data-ttu-id="cf030-118">Vous pouvez également activer la souris et clavier d’entrée en tant que les méthodes d’entrée facultatifs pour votre application Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="cf030-118">You can also enable mouse and keyboard input as optional input methods for your Windows Mixed Reality app.</span></span> <span data-ttu-id="cf030-119">Cela peut également être une fonctionnalité intéressante de débogage pour les appareils tels que HoloLens et peut être souhaitable pour l’entrée d’utilisateur dans les applications de réalité mixte qui s’exécutent dans des casques IMMERSIFS attachés au PC.</span><span class="sxs-lookup"><span data-stu-id="cf030-119">This can also be a great debugging feature for devices such as HoloLens, and may be desirable for user input in mixed reality apps running in immersive headsets attached to PCs.</span></span>
