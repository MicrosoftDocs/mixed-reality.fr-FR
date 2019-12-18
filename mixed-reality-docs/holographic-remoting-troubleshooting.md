---
title: Résolution des problèmes et limitations de la communication à distance holographique
description: Étapes de dépannage pour la communication à distance holographique sur HoloLens 2.
author: FlorianBagarMicrosoft
ms.author: flbagar
ms.date: 12/17/2019
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, accès distant holographique, rendu à distance, rendu réseau, HoloLens, hologrammes distants, dépannage, aide
ms.openlocfilehash: 05333c8911010945a543cf603b9925eb30c841db
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75181969"
---
# <a name="holographic-remoting-troubleshooting"></a>Résolution des problèmes de communication à distance holographique

> [!IMPORTANT]
> Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.

## <a name="spectre-mitigated-libraries-not-found"></a>Bibliothèques atténuées spectre introuvables.

Les exemples d’applications de communication à distance holographique ont une atténuation de spectre (/Qspectre) activée dans la configuration Release.

Si vous recevez une erreur irrécupérable de l’éditeur de liens qui indique que « vccorlib. lib » ne peut pas être ouvert, vérifiez que votre charge de travail Visual Studio comprend les bibliothèques atténuées spectre. Pour plus d'informations, consultez https://aka.ms/Ofhn4c.

## <a name="limitations"></a>Limitations

Les API suivantes ne sont actuellement **pas** prises en charge lors de l’utilisation de la communication à distance holographique pour HoloLens 2 et déclencheront une erreur ```ERROR_NOT_SUPPORTED```, sauf indication contraire :

[Windows.Graphics.Holographic](https://docs.microsoft.com/uwp/api/windows.graphics.holographic)

* [HolographicCamera.ViewConfiguration](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera.viewconfiguration)
  - Pris en charge à partir de la version [2.0.18](holographic-remoting-version-history.md#v2.0.18)
  - Dans les versions précédentes génère toujours une erreur.
* [HolographicViewConfiguration.RequestRenderTargetSize](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicviewconfiguration.requestrendertargetsize#Windows_Graphics_Holographic_HolographicViewConfiguration_RequestRenderTargetSize_Windows_Foundation_Size_)
  - N’échoue pas, mais la taille de la cible de rendu n’est pas modifiée.
* [HolographicCameraPose.OverrideProjectionTransform](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerapose.overrideprojectiontransform)
* [HolographicCameraPose.OverrideViewport](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerapose.overrideviewport)
* [HolographicCameraPose.OverrideViewTransform](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerapose.overrideviewtransform)
* [HolographicCameraRenderingParameters.CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_)
  - N’échoue pas, mais la mémoire tampon de profondeur ne sera pas distante.
* [HolographicDisplay.TryGetViewConfiguration](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicdisplay.trygetviewconfiguration)
  - L’interrogation de HolographicViewConfigurationKind. PhotoVideoCamera renverra toujours un ```nullptr```.
  - Pris en charge à partir de la version [2.0.18](holographic-remoting-version-history.md#v2.0.18)
  - Dans les versions précédentes génère toujours une erreur.
* [HolographicSpace.CreateFramePresentationMonitor](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace.createframepresentationmonitor)
* [HolographicDisplay.GetDefault](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicdisplay.getdefault#Windows_Graphics_Holographic_HolographicDisplay_GetDefault)
  - Signale une erreur si elle est appelée avant l’établissement d’une connexion.


[Windows.Perception.Spatial](https://docs.microsoft.com/uwp/api/windows.perception.spatial)

* [SpatialLocation. AbsoluteAngularAcceleration](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocation.absoluteangularacceleration)
* [SpatialLocation. AbsoluteAngularAccelerationAxisAngle](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocation.absoluteangularaccelerationaxisangle)
* [SpatialLocation. AbsoluteAngularVelocity](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocation.absoluteangularvelocity)
* [SpatialLocation. AbsoluteAngularVelocityAxisAngle](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocation.absoluteangularvelocityaxisangle)
* [SpatialLocation. AbsoluteLinearAcceleration](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocation.absolutelinearacceleration)
* [SpatialLocation. AbsoluteLinearVelocity](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocation.absolutelinearvelocity)
* [SpatialStageFrameOfReference. Current](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference.current)
  - Retourne toujours ```nullptr```.
* [SpatialStageFrameOfReference.RequestNewStageAsync](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference.requestnewstageasync)
* [SpatialAnchor.RemovedByUser](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.removedbyuser)
* [SpatialAnchorExporter.GetDefault](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter.getdefault
)
  - Pris en charge à partir de la version [2.0.9](holographic-remoting-version-history.md#v2.0.9). 
  - Dans les versions précédentes retourne toujours ```nullptr```. 
* [SpatialAnchorExporter.RequestAccessAsync](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter.requestaccessasync
)
  - Pris en charge à partir de la version [2.0.9](holographic-remoting-version-history.md#v2.0.9). 
  - Dans les versions précédentes, l’opération asynchrone s’est toujours terminée avec ```SpatialPerceptionAccessStatus.DeniedBySystem```.
* [SpatialAnchorTransferManager.RequestAccessAsync](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchortransfermanager.requestaccessasync#Windows_Perception_Spatial_SpatialAnchorTransferManager_RequestAccessAsync)
  - L’opération asynchrone se termine toujours avec ```SpatialPerceptionAccessStatus.DeniedBySystem```.
* [SpatialAnchorTransferManager.TryExportAnchorsAsync](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchortransfermanager.tryexportanchorsasync#Windows_Perception_Spatial_SpatialAnchorTransferManager_TryExportAnchorsAsync_Windows_Foundation_Collections_IIterable_Windows_Foundation_Collections_IKeyValuePair_System_String_Windows_Perception_Spatial_SpatialAnchor___Windows_Storage_Streams_IOutputStream_)
  - L’opération asynchrone se termine toujours avec ```false```.
* [SpatialAnchorTransferManager.TryImportAnchorsAsync](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchortransfermanager.tryimportanchorsasync
)
  - L’opération asynchrone se termine toujours avec ```nullptr```.

[Windows.UI.Input.Spatial](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial)

* [SpatialInteractionSource.TryCreateHandMeshObserver](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsource.trycreatehandmeshobserver#Windows_UI_Input_Spatial_SpatialInteractionSource_TryCreateHandMeshObserver)
* [SpatialInteractionSource.TryCreateHandMeshObserverAsync](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsource.trycreatehandmeshobserverasync)

[Windows.Perception.Spatial.Preview](https://docs.microsoft.com/uwp/api/windows.perception.spatial.preview)

* [SpatialGraphInteropPreview.CreateLocatorForNode](https://docs.microsoft.com/uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview.createlocatorfornode)
* [SpatialGraphInteropPreview.TryCreateFrameOfReference](https://docs.microsoft.com/uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview.trycreateframeofreference)
* [SpatialInteractionSource. Controller](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsource.controller#Windows_UI_Input_Spatial_SpatialInteractionSource_Controller)

## <a name="see-also"></a>Articles associés
* [Historique des versions de la communication à distance holographique](holographic-remoting-version-history.md)
* [Écriture d’une application hôte de communication à distance holographique](holographic-remoting-create-host.md)
* [Écriture d’une application de lecteur de communication à distance holographique personnalisée](holographic-remoting-create-player.md)
* [Termes du contrat de licence de la communication à distance holographique](https://docs.microsoft.com/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [Déclaration de confidentialité de Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
