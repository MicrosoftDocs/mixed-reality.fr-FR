---
title: Résolution des problèmes et limitations de la communication à distance holographique
description: Étapes de dépannage pour la communication à distance holographique sur HoloLens 2.
author: FlorianBagarMicrosoft
ms.author: flbagar
ms.date: 10/28/2019
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, accès distant holographique, rendu à distance, rendu réseau, HoloLens, hologrammes distants, dépannage, aide
ms.openlocfilehash: 7b438d9169c9306e0056655e561c04b62b1662cf
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73434234"
---
# <a name="holographic-remoting-troubleshooting"></a><span data-ttu-id="cd2fa-104">Résolution des problèmes de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="cd2fa-104">Holographic Remoting troubleshooting</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd2fa-105">Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="cd2fa-105">This guidance is specific to Holographic Remoting on HoloLens 2.</span></span>

## <a name="spectre-mitigated-libraries-not-found"></a><span data-ttu-id="cd2fa-106">Bibliothèques atténuées spectre introuvables.</span><span class="sxs-lookup"><span data-stu-id="cd2fa-106">Spectre mitigated libraries not found.</span></span>

<span data-ttu-id="cd2fa-107">Les exemples d’applications de communication à distance holographique ont une atténuation de spectre (/Qspectre) activée dans la configuration Release.</span><span class="sxs-lookup"><span data-stu-id="cd2fa-107">Holographic Remoting sample apps have Spectre mitigation (/Qspectre) enabled in Release configuration.</span></span>

<span data-ttu-id="cd2fa-108">Si vous recevez une erreur irrécupérable de l’éditeur de liens qui indique que « vccorlib. lib » ne peut pas être ouvert, vérifiez que votre charge de travail Visual Studio comprend les bibliothèques atténuées spectre.</span><span class="sxs-lookup"><span data-stu-id="cd2fa-108">If you get a fatal linker error which states that 'vccorlib.lib' cannot be opened, make sure that your Visual Studio Workload includes the Spectre mitigated libraries.</span></span> <span data-ttu-id="cd2fa-109">Pour plus d'informations, consultez https://aka.ms/Ofhn4c.</span><span class="sxs-lookup"><span data-stu-id="cd2fa-109">See https://aka.ms/Ofhn4c for more information.</span></span>

## <a name="limitations"></a><span data-ttu-id="cd2fa-110">Limitations</span><span class="sxs-lookup"><span data-stu-id="cd2fa-110">Limitations</span></span>

<span data-ttu-id="cd2fa-111">Les API suivantes ne sont actuellement **pas** prises en charge lors de l’utilisation de la communication à distance holographique pour HoloLens 2 et déclencheront une erreur ```ERROR_NOT_SUPPORTED```, sauf indication contraire :</span><span class="sxs-lookup"><span data-stu-id="cd2fa-111">The following APIs are currently **not** supported when using Holographic Remoting for HoloLens 2 and will raises an ```ERROR_NOT_SUPPORTED``` error unless otherwise stated:</span></span>

[<span data-ttu-id="cd2fa-112">Windows.Graphics.Holographic</span><span class="sxs-lookup"><span data-stu-id="cd2fa-112">Windows.Graphics.Holographic</span></span>](https://docs.microsoft.com/uwp/api/windows.graphics.holographic)

* [<span data-ttu-id="cd2fa-113">HolographicCamera.ViewConfiguration</span><span class="sxs-lookup"><span data-stu-id="cd2fa-113">HolographicCamera.ViewConfiguration</span></span>](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera.viewconfiguration)
* [<span data-ttu-id="cd2fa-114">HolographicCameraPose.OverrideProjectionTransform</span><span class="sxs-lookup"><span data-stu-id="cd2fa-114">HolographicCameraPose.OverrideProjectionTransform</span></span>](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerapose.overrideprojectiontransform)
* [<span data-ttu-id="cd2fa-115">HolographicCameraPose.OverrideViewport</span><span class="sxs-lookup"><span data-stu-id="cd2fa-115">HolographicCameraPose.OverrideViewport</span></span>](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerapose.overrideviewport)
* [<span data-ttu-id="cd2fa-116">HolographicCameraPose.OverrideViewTransform</span><span class="sxs-lookup"><span data-stu-id="cd2fa-116">HolographicCameraPose.OverrideViewTransform</span></span>](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerapose.overrideviewtransform)
* [<span data-ttu-id="cd2fa-117">HolographicCameraRenderingParameters.CommitDirect3D11DepthBuffer</span><span class="sxs-lookup"><span data-stu-id="cd2fa-117">HolographicCameraRenderingParameters.CommitDirect3D11DepthBuffer</span></span>](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_)
  - <span data-ttu-id="cd2fa-118">N’échoue pas, mais la mémoire tampon de profondeur ne sera pas distante.</span><span class="sxs-lookup"><span data-stu-id="cd2fa-118">Does not fail but depth buffer will not be remoted.</span></span>
* [<span data-ttu-id="cd2fa-119">HolographicDisplay.TryGetViewConfiguration</span><span class="sxs-lookup"><span data-stu-id="cd2fa-119">HolographicDisplay.TryGetViewConfiguration</span></span>](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicdisplay.trygetviewconfiguration)
* [<span data-ttu-id="cd2fa-120">HolographicSpace.CreateFramePresentationMonitor</span><span class="sxs-lookup"><span data-stu-id="cd2fa-120">HolographicSpace.CreateFramePresentationMonitor</span></span>](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace.createframepresentationmonitor)

[<span data-ttu-id="cd2fa-121">Windows.Perception.Spatial</span><span class="sxs-lookup"><span data-stu-id="cd2fa-121">Windows.Perception.Spatial</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial)

* [<span data-ttu-id="cd2fa-122">SpatialLocation. AbsoluteAngularAcceleration</span><span class="sxs-lookup"><span data-stu-id="cd2fa-122">SpatialLocation.AbsoluteAngularAcceleration</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocation.absoluteangularacceleration)
* [<span data-ttu-id="cd2fa-123">SpatialLocation. AbsoluteAngularAccelerationAxisAngle</span><span class="sxs-lookup"><span data-stu-id="cd2fa-123">SpatialLocation.AbsoluteAngularAccelerationAxisAngle</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocation.absoluteangularaccelerationaxisangle)
* [<span data-ttu-id="cd2fa-124">SpatialLocation. AbsoluteAngularVelocity</span><span class="sxs-lookup"><span data-stu-id="cd2fa-124">SpatialLocation.AbsoluteAngularVelocity</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocation.absoluteangularvelocity)
* [<span data-ttu-id="cd2fa-125">SpatialLocation. AbsoluteAngularVelocityAxisAngle</span><span class="sxs-lookup"><span data-stu-id="cd2fa-125">SpatialLocation.AbsoluteAngularVelocityAxisAngle</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocation.absoluteangularvelocityaxisangle)
* [<span data-ttu-id="cd2fa-126">SpatialLocation. AbsoluteLinearAcceleration</span><span class="sxs-lookup"><span data-stu-id="cd2fa-126">SpatialLocation.AbsoluteLinearAcceleration</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocation.absolutelinearacceleration)
* [<span data-ttu-id="cd2fa-127">SpatialLocation. AbsoluteLinearVelocity</span><span class="sxs-lookup"><span data-stu-id="cd2fa-127">SpatialLocation.AbsoluteLinearVelocity</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocation.absolutelinearvelocity)
* [<span data-ttu-id="cd2fa-128">SpatialStageFrameOfReference. Current</span><span class="sxs-lookup"><span data-stu-id="cd2fa-128">SpatialStageFrameOfReference.Current</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference.current)
  - <span data-ttu-id="cd2fa-129">Retourne toujours ```nullptr```.</span><span class="sxs-lookup"><span data-stu-id="cd2fa-129">Always returns ```nullptr```.</span></span>
* [<span data-ttu-id="cd2fa-130">SpatialStageFrameOfReference.RequestNewStageAsync</span><span class="sxs-lookup"><span data-stu-id="cd2fa-130">SpatialStageFrameOfReference.RequestNewStageAsync</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference.requestnewstageasync)
* [<span data-ttu-id="cd2fa-131">SpatialAnchor.RemovedByUser</span><span class="sxs-lookup"><span data-stu-id="cd2fa-131">SpatialAnchor.RemovedByUser</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.removedbyuser)
* [<span data-ttu-id="cd2fa-132">SpatialAnchorExporter.GetDefault</span><span class="sxs-lookup"><span data-stu-id="cd2fa-132">SpatialAnchorExporter.GetDefault</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter.getdefault
)
  - <span data-ttu-id="cd2fa-133">Pris en charge à partir de la version [2.0.9](holographic-remoting-version-history.md#v2.0.9).</span><span class="sxs-lookup"><span data-stu-id="cd2fa-133">Supported starting with version [2.0.9](holographic-remoting-version-history.md#v2.0.9).</span></span> 
  - <span data-ttu-id="cd2fa-134">Dans les versions précédentes retourne toujours ```nullptr```.</span><span class="sxs-lookup"><span data-stu-id="cd2fa-134">On previous versions always returns ```nullptr```.</span></span> 
* [<span data-ttu-id="cd2fa-135">SpatialAnchorExporter.RequestAccessAsync</span><span class="sxs-lookup"><span data-stu-id="cd2fa-135">SpatialAnchorExporter.RequestAccessAsync</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter.requestaccessasync
)
  - <span data-ttu-id="cd2fa-136">Pris en charge à partir de la version [2.0.9](holographic-remoting-version-history.md#v2.0.9).</span><span class="sxs-lookup"><span data-stu-id="cd2fa-136">Supported starting with version [2.0.9](holographic-remoting-version-history.md#v2.0.9).</span></span> 
  - <span data-ttu-id="cd2fa-137">Dans les versions précédentes, l’opération asynchrone s’est toujours terminée avec ```SpatialPerceptionAccessStatus.DeniedBySystem```.</span><span class="sxs-lookup"><span data-stu-id="cd2fa-137">On previous versions the async operation always completed with ```SpatialPerceptionAccessStatus.DeniedBySystem```.</span></span>
* [<span data-ttu-id="cd2fa-138">SpatialAnchorTransferManager.RequestAccessAsync</span><span class="sxs-lookup"><span data-stu-id="cd2fa-138">SpatialAnchorTransferManager.RequestAccessAsync</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchortransfermanager.requestaccessasync#Windows_Perception_Spatial_SpatialAnchorTransferManager_RequestAccessAsync)
  - <span data-ttu-id="cd2fa-139">L’opération asynchrone se termine toujours avec ```SpatialPerceptionAccessStatus.DeniedBySystem```.</span><span class="sxs-lookup"><span data-stu-id="cd2fa-139">Async operation always completes with ```SpatialPerceptionAccessStatus.DeniedBySystem```.</span></span>
* [<span data-ttu-id="cd2fa-140">SpatialAnchorTransferManager.TryExportAnchorsAsync</span><span class="sxs-lookup"><span data-stu-id="cd2fa-140">SpatialAnchorTransferManager.TryExportAnchorsAsync</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchortransfermanager.tryexportanchorsasync#Windows_Perception_Spatial_SpatialAnchorTransferManager_TryExportAnchorsAsync_Windows_Foundation_Collections_IIterable_Windows_Foundation_Collections_IKeyValuePair_System_String_Windows_Perception_Spatial_SpatialAnchor___Windows_Storage_Streams_IOutputStream_)
  - <span data-ttu-id="cd2fa-141">L’opération asynchrone se termine toujours avec ```false```.</span><span class="sxs-lookup"><span data-stu-id="cd2fa-141">Async operation always completes with ```false```.</span></span>
* [<span data-ttu-id="cd2fa-142">SpatialAnchorTransferManager.TryImportAnchorsAsync</span><span class="sxs-lookup"><span data-stu-id="cd2fa-142">SpatialAnchorTransferManager.TryImportAnchorsAsync</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchortransfermanager.tryimportanchorsasync
)
  - <span data-ttu-id="cd2fa-143">L’opération asynchrone se termine toujours avec ```nullptr```.</span><span class="sxs-lookup"><span data-stu-id="cd2fa-143">Async operation always completes with ```nullptr```.</span></span>

[<span data-ttu-id="cd2fa-144">Windows.UI.Input.Spatial</span><span class="sxs-lookup"><span data-stu-id="cd2fa-144">Windows.UI.Input.Spatial</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial)

* [<span data-ttu-id="cd2fa-145">SpatialInteractionSource.TryCreateHandMeshObserver</span><span class="sxs-lookup"><span data-stu-id="cd2fa-145">SpatialInteractionSource.TryCreateHandMeshObserver</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsource.trycreatehandmeshobserver#Windows_UI_Input_Spatial_SpatialInteractionSource_TryCreateHandMeshObserver)
* [<span data-ttu-id="cd2fa-146">SpatialInteractionSource.TryCreateHandMeshObserverAsync</span><span class="sxs-lookup"><span data-stu-id="cd2fa-146">SpatialInteractionSource.TryCreateHandMeshObserverAsync</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsource.trycreatehandmeshobserverasync)

[<span data-ttu-id="cd2fa-147">Windows.Perception.Spatial.Preview</span><span class="sxs-lookup"><span data-stu-id="cd2fa-147">Windows.Perception.Spatial.Preview</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.preview)

* [<span data-ttu-id="cd2fa-148">SpatialGraphInteropPreview.CreateLocatorForNode</span><span class="sxs-lookup"><span data-stu-id="cd2fa-148">SpatialGraphInteropPreview.CreateLocatorForNode</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview.createlocatorfornode)
* [<span data-ttu-id="cd2fa-149">SpatialGraphInteropPreview.TryCreateFrameOfReference</span><span class="sxs-lookup"><span data-stu-id="cd2fa-149">SpatialGraphInteropPreview.TryCreateFrameOfReference</span></span>](https://docs.microsoft.com/uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview.trycreateframeofreference)
* [<span data-ttu-id="cd2fa-150">SpatialInteractionSource. Controller</span><span class="sxs-lookup"><span data-stu-id="cd2fa-150">SpatialInteractionSource.Controller</span></span>](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsource.controller#Windows_UI_Input_Spatial_SpatialInteractionSource_Controller)

## <a name="see-also"></a><span data-ttu-id="cd2fa-151">Articles associés</span><span class="sxs-lookup"><span data-stu-id="cd2fa-151">See Also</span></span>
* [<span data-ttu-id="cd2fa-152">Historique des versions de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="cd2fa-152">Holographic Remoting Version History</span></span>](holographic-remoting-version-history.md)
* [<span data-ttu-id="cd2fa-153">Écriture d’une application hôte de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="cd2fa-153">Writing a Holographic Remoting host app</span></span>](holographic-remoting-create-host.md)
* [<span data-ttu-id="cd2fa-154">Écriture d’une application de lecteur de communication à distance holographique personnalisée</span><span class="sxs-lookup"><span data-stu-id="cd2fa-154">Writing a custom Holographic Remoting player app</span></span>](holographic-remoting-create-player.md)
* [<span data-ttu-id="cd2fa-155">Termes du contrat de licence de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="cd2fa-155">Holographic Remoting software license terms</span></span>](https://docs.microsoft.com/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [<span data-ttu-id="cd2fa-156">Déclaration de confidentialité Microsoft</span><span class="sxs-lookup"><span data-stu-id="cd2fa-156">Microsoft Privacy Statement</span></span>](https://go.microsoft.com/fwlink/?LinkId=521839)
