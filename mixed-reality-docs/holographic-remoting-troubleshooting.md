---
title: Résolution des problèmes et limitations de la communication à distance holographique
description: Étapes de dépannage pour la communication à distance holographique sur HoloLens 2.
author: FlorianBagarMicrosoft
ms.author: flbagar
ms.date: 08/01/2019
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, accès distant holographique, rendu à distance, rendu réseau, HoloLens, hologrammes distants, dépannage, aide
ms.openlocfilehash: 86b6979dbfc9b514b3af13ebdcc3d3ece17e6335
ms.sourcegitcommit: ca949efe0279995a376750d89e23d7123eb44846
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68718143"
---
# <a name="holographic-remoting-troubleshooting"></a><span data-ttu-id="488ed-104">Résolution des problèmes de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="488ed-104">Holographic Remoting troubleshooting</span></span>

> [!IMPORTANT]
> <span data-ttu-id="488ed-105">Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="488ed-105">This guidance is specific to Holographic Remoting on HoloLens 2.</span></span>

## <a name="spectre-mitigated-libraries-not-found"></a><span data-ttu-id="488ed-106">Bibliothèques atténuées spectre introuvables.</span><span class="sxs-lookup"><span data-stu-id="488ed-106">Spectre mitigated libraries not found.</span></span>

<span data-ttu-id="488ed-107">Les exemples d’applications de communication à distance holographique ont une atténuation de spectre (/Qspectre) activée dans la configuration Release.</span><span class="sxs-lookup"><span data-stu-id="488ed-107">Holographic Remoting sample apps have Spectre mitigation (/Qspectre) enabled in Release configuration.</span></span>

<span data-ttu-id="488ed-108">Si vous recevez une erreur irrécupérable de l’éditeur de liens qui indique que «vccorlib. lib» ne peut pas être ouvert, vérifiez que votre charge de travail Visual Studio comprend les bibliothèques atténuées spectre.</span><span class="sxs-lookup"><span data-stu-id="488ed-108">If you get a fatal linker error which states that 'vccorlib.lib' cannot be opened, make sure that your Visual Studio Workload includes the Spectre mitigated libraries.</span></span> <span data-ttu-id="488ed-109">Pour plus d'informations, consultez https://aka.ms/Ofhn4c.</span><span class="sxs-lookup"><span data-stu-id="488ed-109">See https://aka.ms/Ofhn4c for more information.</span></span>

# <a name="limitations"></a><span data-ttu-id="488ed-110">Limites</span><span class="sxs-lookup"><span data-stu-id="488ed-110">Limitations</span></span>

<span data-ttu-id="488ed-111">Les API suivantes ne sont actuellement **pas** prises en charge lors de l’utilisation de la communication à distance ```ERROR_NOT_SUPPORTED``` holographique pour HoloLens 2 et génèrent une erreur sauf indication contraire:</span><span class="sxs-lookup"><span data-stu-id="488ed-111">The following APIs are currently **not** supported when using Holographic Remoting for HoloLens 2 and will raises an ```ERROR_NOT_SUPPORTED``` error unless otherwise stated:</span></span>

[<span data-ttu-id="488ed-112">Windows.Graphics.Holographic</span><span class="sxs-lookup"><span data-stu-id="488ed-112">Windows.Graphics.Holographic</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic)

* [<span data-ttu-id="488ed-113">HolographicCamera.ViewConfiguration</span><span class="sxs-lookup"><span data-stu-id="488ed-113">HolographicCamera.ViewConfiguration</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamera.viewconfiguration)
* [<span data-ttu-id="488ed-114">HolographicCameraPose.OverrideProjectionTransform</span><span class="sxs-lookup"><span data-stu-id="488ed-114">HolographicCameraPose.OverrideProjectionTransform</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerapose.overrideprojectiontransform)
* [<span data-ttu-id="488ed-115">HolographicCameraPose.OverrideViewport</span><span class="sxs-lookup"><span data-stu-id="488ed-115">HolographicCameraPose.OverrideViewport</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerapose.overrideviewport)
* [<span data-ttu-id="488ed-116">HolographicCameraPose.OverrideViewTransform</span><span class="sxs-lookup"><span data-stu-id="488ed-116">HolographicCameraPose.OverrideViewTransform</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerapose.overrideviewtransform)
* <span data-ttu-id="488ed-117">[HolographicCameraRenderingParameters. CommitDirect3D11DepthBuffer](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_) : n’échoue pas, mais la mémoire tampon de profondeur ne sera pas distante.</span><span class="sxs-lookup"><span data-stu-id="488ed-117">[HolographicCameraRenderingParameters.CommitDirect3D11DepthBuffer](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_) - Does not fail but depth buffer will not be remoted.</span></span>
* [<span data-ttu-id="488ed-118">HolographicDisplay.TryGetViewConfiguration</span><span class="sxs-lookup"><span data-stu-id="488ed-118">HolographicDisplay.TryGetViewConfiguration</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicdisplay.trygetviewconfiguration)
* [<span data-ttu-id="488ed-119">HolographicSpace.CreateFramePresentationMonitor</span><span class="sxs-lookup"><span data-stu-id="488ed-119">HolographicSpace.CreateFramePresentationMonitor</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicspace.createframepresentationmonitor)

[<span data-ttu-id="488ed-120">Windows.Perception.Spatial</span><span class="sxs-lookup"><span data-stu-id="488ed-120">Windows.Perception.Spatial</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial)

* [<span data-ttu-id="488ed-121">SpatialLocation. AbsoluteAngularAcceleration</span><span class="sxs-lookup"><span data-stu-id="488ed-121">SpatialLocation.AbsoluteAngularAcceleration</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatiallocation.absoluteangularacceleration)
* [<span data-ttu-id="488ed-122">SpatialLocation. AbsoluteAngularAccelerationAxisAngle</span><span class="sxs-lookup"><span data-stu-id="488ed-122">SpatialLocation.AbsoluteAngularAccelerationAxisAngle</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatiallocation.absoluteangularaccelerationaxisangle)
* [<span data-ttu-id="488ed-123">SpatialLocation. AbsoluteAngularVelocity</span><span class="sxs-lookup"><span data-stu-id="488ed-123">SpatialLocation.AbsoluteAngularVelocity</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatiallocation.absoluteangularvelocity)
* [<span data-ttu-id="488ed-124">SpatialLocation. AbsoluteAngularVelocityAxisAngle</span><span class="sxs-lookup"><span data-stu-id="488ed-124">SpatialLocation.AbsoluteAngularVelocityAxisAngle</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatiallocation.absoluteangularvelocityaxisangle)
* [<span data-ttu-id="488ed-125">SpatialLocation. AbsoluteLinearAcceleration</span><span class="sxs-lookup"><span data-stu-id="488ed-125">SpatialLocation.AbsoluteLinearAcceleration</span></span>](https://docs.microsoft.com/is-is/uwp/api/windows.perception.spatial.spatiallocation.absolutelinearacceleration)
* [<span data-ttu-id="488ed-126">SpatialLocation. AbsoluteLinearVelocity</span><span class="sxs-lookup"><span data-stu-id="488ed-126">SpatialLocation.AbsoluteLinearVelocity</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatiallocation.absolutelinearvelocity)
* <span data-ttu-id="488ed-127">[SpatialStageFrameOfReference. Current](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialstageframeofreference.current) -retourne ```nullptr```toujours.</span><span class="sxs-lookup"><span data-stu-id="488ed-127">[SpatialStageFrameOfReference.Current](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialstageframeofreference.current) - Always returns ```nullptr```.</span></span>
* [<span data-ttu-id="488ed-128">SpatialStageFrameOfReference.RequestNewStageAsync</span><span class="sxs-lookup"><span data-stu-id="488ed-128">SpatialStageFrameOfReference.RequestNewStageAsync</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialstageframeofreference.requestnewstageasync)
* [<span data-ttu-id="488ed-129">SpatialAnchor.RemovedByUser</span><span class="sxs-lookup"><span data-stu-id="488ed-129">SpatialAnchor.RemovedByUser</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialanchor.removedbyuser)
* <span data-ttu-id="488ed-130">[SpatialAnchorExporter. GetDefault](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialanchorexporter.getdefault
) : retourne ```nullptr```toujours.</span><span class="sxs-lookup"><span data-stu-id="488ed-130">[SpatialAnchorExporter.GetDefault](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialanchorexporter.getdefault
) - Always returns ```nullptr```.</span></span>
* <span data-ttu-id="488ed-131">[SpatialAnchorExporter. RequestAccessAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialanchorexporter.requestaccessasync
) : l’opération asynchrone se termine ```SpatialPerceptionAccessStatus.DeniedBySystem```toujours par.</span><span class="sxs-lookup"><span data-stu-id="488ed-131">[SpatialAnchorExporter.RequestAccessAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialanchorexporter.requestaccessasync
) - Async operation always completes with ```SpatialPerceptionAccessStatus.DeniedBySystem```.</span></span>
* <span data-ttu-id="488ed-132">[SpatialAnchorTransferManager. RequestAccessAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialanchortransfermanager.requestaccessasync#Windows_Perception_Spatial_SpatialAnchorTransferManager_RequestAccessAsync) : l’opération asynchrone se termine ```SpatialPerceptionAccessStatus.DeniedBySystem```toujours par.</span><span class="sxs-lookup"><span data-stu-id="488ed-132">[SpatialAnchorTransferManager.RequestAccessAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialanchortransfermanager.requestaccessasync#Windows_Perception_Spatial_SpatialAnchorTransferManager_RequestAccessAsync) - Async operation always completes with ```SpatialPerceptionAccessStatus.DeniedBySystem```.</span></span>
* <span data-ttu-id="488ed-133">[SpatialAnchorTransferManager. TryExportAnchorsAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialanchortransfermanager.tryexportanchorsasync#Windows_Perception_Spatial_SpatialAnchorTransferManager_TryExportAnchorsAsync_Windows_Foundation_Collections_IIterable_Windows_Foundation_Collections_IKeyValuePair_System_String_Windows_Perception_Spatial_SpatialAnchor___Windows_Storage_Streams_IOutputStream_) : l’opération asynchrone se termine ```false```toujours par.</span><span class="sxs-lookup"><span data-stu-id="488ed-133">[SpatialAnchorTransferManager.TryExportAnchorsAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialanchortransfermanager.tryexportanchorsasync#Windows_Perception_Spatial_SpatialAnchorTransferManager_TryExportAnchorsAsync_Windows_Foundation_Collections_IIterable_Windows_Foundation_Collections_IKeyValuePair_System_String_Windows_Perception_Spatial_SpatialAnchor___Windows_Storage_Streams_IOutputStream_) - Async operation always completes with ```false```.</span></span>
* <span data-ttu-id="488ed-134">[SpatialAnchorTransferManager. TryImportAnchorsAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialanchortransfermanager.tryimportanchorsasync
) : l’opération asynchrone se termine ```nullptr```toujours par.</span><span class="sxs-lookup"><span data-stu-id="488ed-134">[SpatialAnchorTransferManager.TryImportAnchorsAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialanchortransfermanager.tryimportanchorsasync
) - Async operation always completes with ```nullptr```.</span></span>

[<span data-ttu-id="488ed-135">Windows.UI.Input.Spatial</span><span class="sxs-lookup"><span data-stu-id="488ed-135">Windows.UI.Input.Spatial</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial)

* [<span data-ttu-id="488ed-136">SpatialInteractionSource.TryCreateHandMeshObserver</span><span class="sxs-lookup"><span data-stu-id="488ed-136">SpatialInteractionSource.TryCreateHandMeshObserver</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource.trycreatehandmeshobserver#Windows_UI_Input_Spatial_SpatialInteractionSource_TryCreateHandMeshObserver)
* [<span data-ttu-id="488ed-137">SpatialInteractionSource.TryCreateHandMeshObserverAsync</span><span class="sxs-lookup"><span data-stu-id="488ed-137">SpatialInteractionSource.TryCreateHandMeshObserverAsync</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource.trycreatehandmeshobserverasync)

[<span data-ttu-id="488ed-138">Windows.Perception.Spatial.Preview</span><span class="sxs-lookup"><span data-stu-id="488ed-138">Windows.Perception.Spatial.Preview</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.preview)

* [<span data-ttu-id="488ed-139">SpatialGraphInteropPreview.CreateLocatorForNode</span><span class="sxs-lookup"><span data-stu-id="488ed-139">SpatialGraphInteropPreview.CreateLocatorForNode</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview.createlocatorfornode)
* [<span data-ttu-id="488ed-140">SpatialGraphInteropPreview.TryCreateFrameOfReference</span><span class="sxs-lookup"><span data-stu-id="488ed-140">SpatialGraphInteropPreview.TryCreateFrameOfReference</span></span>](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview.trycreateframeofreference)

## <a name="see-also"></a><span data-ttu-id="488ed-141">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="488ed-141">See Also</span></span>
* [<span data-ttu-id="488ed-142">Écriture d’une application hôte de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="488ed-142">Writing a Holographic Remoting host app</span></span>](holographic-remoting-create-host.md)
* [<span data-ttu-id="488ed-143">Écriture d’une application de lecteur de communication à distance holographique personnalisée</span><span class="sxs-lookup"><span data-stu-id="488ed-143">Writing a custom Holographic Remoting player app</span></span>](holographic-remoting-create-player.md)
* [<span data-ttu-id="488ed-144">Termes du contrat de licence du logiciel de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="488ed-144">Holographic Remoting software license terms</span></span>](https://docs.microsoft.com/en-us/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [<span data-ttu-id="488ed-145">Déclaration de confidentialité Microsoft</span><span class="sxs-lookup"><span data-stu-id="488ed-145">Microsoft Privacy Statement</span></span>](https://go.microsoft.com/fwlink/?LinkId=521839)