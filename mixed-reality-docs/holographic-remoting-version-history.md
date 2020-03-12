---
title: Historique des versions de la communication à distance holographique
description: Historique des versions de la communication à distance holographique sur HoloLens 2.
author: FlorianBagarMicrosoft
ms.author: flbagar
ms.date: 03/11/2020
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: 62f54dbcf5327cdd5f13622704684a2cb0606d7d
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092306"
---
# <a name="holographic-remoting-version-history"></a><span data-ttu-id="146cc-104">Historique des versions de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="146cc-104">Holographic Remoting Version History</span></span>

> [!IMPORTANT]
> <span data-ttu-id="146cc-105">Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="146cc-105">This guidance is specific to Holographic Remoting on HoloLens 2.</span></span>

## <span data-ttu-id="146cc-106">Version 2.1.0 (11 mars, 2020)<a name="v2.1.0"></a></span><span class="sxs-lookup"><span data-stu-id="146cc-106">Version 2.1.0 (March 11, 2020) <a name="v2.1.0"></a></span></span>
* <span data-ttu-id="146cc-107">Transport réseau commuté pour utiliser [RTP](https://en.wikipedia.org/wiki/Real-time_Transport_Protocol) via UDP.</span><span class="sxs-lookup"><span data-stu-id="146cc-107">Switched network transport to use [RTP](https://en.wikipedia.org/wiki/Real-time_Transport_Protocol) via UDP.</span></span> <span data-ttu-id="146cc-108">Les connexions sécurisées utilisent [SRTP](https://en.wikipedia.org/wiki/Secure_Real-time_Transport_Protocol) Now.</span><span class="sxs-lookup"><span data-stu-id="146cc-108">Secure connections use [SRTP](https://en.wikipedia.org/wiki/Secure_Real-time_Transport_Protocol) now.</span></span> <span data-ttu-id="146cc-109">Notez que le [lecteur de communication à distance holographique](holographic-remoting-player.md) est toujours compatible avec toutes les versions de Remoting holographiques antérieures.</span><span class="sxs-lookup"><span data-stu-id="146cc-109">Note, the [Holographic Remoting Player](holographic-remoting-player.md) is still compatible with all previously release Holographic Remoting versions.</span></span> <span data-ttu-id="146cc-110">Pour tirer parti du nouveau transport réseau, le lecteur de communication à distance holographique et l’application distante en question doivent utiliser la version 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="146cc-110">To benefit from the new network transport both, the Holographic Remoting Player and the remote app in question, have to use version 2.1.0.</span></span>
* <span data-ttu-id="146cc-111">Ajout de la prise en charge de [HolographicCameraRenderingParameters. CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_).</span><span class="sxs-lookup"><span data-stu-id="146cc-111">Added support for [HolographicCameraRenderingParameters.CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_).</span></span> 

## <span data-ttu-id="146cc-112">Version 2.0.20 (2 février 2020)<a name="v2.0.20"></a></span><span class="sxs-lookup"><span data-stu-id="146cc-112">Version 2.0.20 (February 2, 2020) <a name="v2.0.20"></a></span></span>
* <span data-ttu-id="146cc-113">Correction de divers bogues qui mènent à des incidents.</span><span class="sxs-lookup"><span data-stu-id="146cc-113">Fixed various bugs that lead to crashes.</span></span>

## <span data-ttu-id="146cc-114">Version 2.0.18 (17 décembre 2019)<a name="v2.0.18"></a></span><span class="sxs-lookup"><span data-stu-id="146cc-114">Version 2.0.18 (December 17, 2019) <a name="v2.0.18"></a></span></span>
* <span data-ttu-id="146cc-115">Ajout de la prise en charge de [HolographicViewConfiguration](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicviewconfiguration)</span><span class="sxs-lookup"><span data-stu-id="146cc-115">Added support for [HolographicViewConfiguration](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicviewconfiguration)</span></span>
* <span data-ttu-id="146cc-116">Correction de divers bogues qui mènent à des incidents.</span><span class="sxs-lookup"><span data-stu-id="146cc-116">Fixed various bugs that lead to crashes.</span></span>
* <span data-ttu-id="146cc-117">Correction d’un bogue où un rappel HolographicSpace. CameraAdded était nécessaire pour qu’un HolographicCamera soit accepté et apparaissait comme caméra ajoutée dans le HoloraphicFrame.</span><span class="sxs-lookup"><span data-stu-id="146cc-117">Fixed bug where a HolographicSpace.CameraAdded callback was required for a HolographicCamera to get accepted and show up as added camera in the HoloraphicFrame.</span></span>

## <span data-ttu-id="146cc-118">Version 2.0.16 (11 novembre 2019)<a name="2.0.16"></a></span><span class="sxs-lookup"><span data-stu-id="146cc-118">Version 2.0.16 (November 11, 2019) <a name="2.0.16"></a></span></span>
* <span data-ttu-id="146cc-119">Correction du blocage dans le suivi du code QR.</span><span class="sxs-lookup"><span data-stu-id="146cc-119">Fixed deadlock in QR code tracking.</span></span>
* <span data-ttu-id="146cc-120">Correction de l’exception unhandeled en raison d’une attente de blocage dans le thread principal.</span><span class="sxs-lookup"><span data-stu-id="146cc-120">Fixed unhandeled exception due to blocking wait in main thread.</span></span>

## <span data-ttu-id="146cc-121">Version 2.0.14 (26 octobre 2019)<a name="v2.0.14"></a></span><span class="sxs-lookup"><span data-stu-id="146cc-121">Version 2.0.14 (October 26, 2019) <a name="v2.0.14"></a></span></span>
* <span data-ttu-id="146cc-122">Prise en charge des nouvelles API PerceptionDevice (mise à jour de novembre 2019 de Windows 10).</span><span class="sxs-lookup"><span data-stu-id="146cc-122">Support for new PerceptionDevice APIs (Windows 10 November 2019 Update).</span></span>
* <span data-ttu-id="146cc-123">Résolution du problème qui empêche les événements de mouvement de maintien déclenchés par SpatialGestureRecognizer.</span><span class="sxs-lookup"><span data-stu-id="146cc-123">Fixed issue which prevent hold gesture events being triggered by SpatialGestureRecognizer.</span></span>
* <span data-ttu-id="146cc-124">Problème de thread fixe lors de l’utilisation de SpatialSurfaceObserver. SetBoundingVolume.</span><span class="sxs-lookup"><span data-stu-id="146cc-124">Fixed threading issue when using SpatialSurfaceObserver.SetBoundingVolume.</span></span>

## <span data-ttu-id="146cc-125">Version 2.0.12 (18 octobre 2019)<a name="v2.0.12"></a></span><span class="sxs-lookup"><span data-stu-id="146cc-125">Version 2.0.12 (October 18, 2019) <a name="v2.0.12"></a></span></span>
* <span data-ttu-id="146cc-126">Correction d’un incident dans SpatialGestureRecognizer lors de l’utilisation de NavigationRail (X/Y/Z).</span><span class="sxs-lookup"><span data-stu-id="146cc-126">Fixed crash in SpatialGestureRecognizer when using NavigationRail(X/Y/Z).</span></span>

## <span data-ttu-id="146cc-127">Version 2.0.10 (10 octobre 2019)<a name="v2.0.10"></a></span><span class="sxs-lookup"><span data-stu-id="146cc-127">Version 2.0.10 (October 10, 2019) <a name="v2.0.10"></a></span></span>
* <span data-ttu-id="146cc-128">Résolution d’un incident lors de l’utilisation du bouton déclencheur des contrôleurs VR.</span><span class="sxs-lookup"><span data-stu-id="146cc-128">Fixed crash when using trigger button of VR controllers.</span></span> <span data-ttu-id="146cc-129">La communication à distance holographique ne prend pas entièrement en charge les contrôleurs, mais uniquement le bouton déclencheur et le bouton Windows fonctionnent s’ils sont associés à HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="146cc-129">Holographic Remoting does not fully support controllers, only the trigger button and the Windows button are working if paired with HoloLens 2.</span></span>

## <span data-ttu-id="146cc-130">Version 2.0.9 (19 septembre 2019)<a name="v2.0.9"></a></span><span class="sxs-lookup"><span data-stu-id="146cc-130">Version 2.0.9 (September 19, 2019) <a name="v2.0.9"></a></span></span>
* <span data-ttu-id="146cc-131">Ajout de la prise en charge de [SpatialAnchorExporter](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter)</span><span class="sxs-lookup"><span data-stu-id="146cc-131">Added support for [SpatialAnchorExporter](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter)</span></span>
* <span data-ttu-id="146cc-132">Ajout d’une nouvelle interface ```IPlayerContext2``` (implémenté par ```PlayerContext```) fournissant les membres suivants :</span><span class="sxs-lookup"><span data-stu-id="146cc-132">Added new interface ```IPlayerContext2``` (implemented by ```PlayerContext```) providing the following members:</span></span>
  - <span data-ttu-id="146cc-133">Propriété [BlitRemoteFrameTimeout](holographic-remoting-create-player.md#BlitRemoteFrameTimeout) .</span><span class="sxs-lookup"><span data-stu-id="146cc-133">[BlitRemoteFrameTimeout](holographic-remoting-create-player.md#BlitRemoteFrameTimeout)  property.</span></span>
* <span data-ttu-id="146cc-134">Ajout de la valeur ```Failed_RemoteFrameTooOld``` à ```BlitResult```</span><span class="sxs-lookup"><span data-stu-id="146cc-134">Added ```Failed_RemoteFrameTooOld``` value to ```BlitResult```</span></span>
* <span data-ttu-id="146cc-135">Améliorations de la stabilité et de la fiabilité</span><span class="sxs-lookup"><span data-stu-id="146cc-135">Stability and reliability improvements</span></span>

## <span data-ttu-id="146cc-136">Version 2.0.8 (20 août, 2019)<a name="v2.0.8"></a></span><span class="sxs-lookup"><span data-stu-id="146cc-136">Version 2.0.8 (August 20, 2019) <a name="v2.0.8"></a></span></span>

* <span data-ttu-id="146cc-137">Résolution d’un incident lors de l’appel de [HolographicCameraRenderingParameters. CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer) avec un paramètre [IDXGISurface2](https://docs.microsoft.com/windows/win32/api/dxgi1_2/nn-dxgi1_2-idxgisurface2) .</span><span class="sxs-lookup"><span data-stu-id="146cc-137">Fixed crash when calling [HolographicCameraRenderingParameters.CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer) with a [IDXGISurface2](https://docs.microsoft.com/windows/win32/api/dxgi1_2/nn-dxgi1_2-idxgisurface2) as parameter.</span></span>
* <span data-ttu-id="146cc-138">Améliorations de la stabilité et de la fiabilité</span><span class="sxs-lookup"><span data-stu-id="146cc-138">Stability and reliability improvements</span></span>

## <span data-ttu-id="146cc-139">Version 2.0.7 (26 juillet, 2019)<a name="v2.0.7"></a></span><span class="sxs-lookup"><span data-stu-id="146cc-139">Version 2.0.7 (July 26, 2019) <a name="v2.0.7"></a></span></span>

* <span data-ttu-id="146cc-140">Première version publique de la communication à distance holographique pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="146cc-140">First public release of Holographic Remoting for HoloLens 2.</span></span>

## <a name="see-also"></a><span data-ttu-id="146cc-141">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="146cc-141">See Also</span></span>
* [<span data-ttu-id="146cc-142">Écriture d’une application de lecteur de communication à distance holographique personnalisée</span><span class="sxs-lookup"><span data-stu-id="146cc-142">Writing a custom Holographic Remoting player app</span></span>](holographic-remoting-create-player.md)
* [<span data-ttu-id="146cc-143">Écriture d’une application hôte de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="146cc-143">Writing a Holographic Remoting host app</span></span>](holographic-remoting-create-host.md)
* [<span data-ttu-id="146cc-144">Résolution des problèmes et limitations de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="146cc-144">Holographic Remoting troubleshooting and limitations</span></span>](holographic-remoting-troubleshooting.md)
* [<span data-ttu-id="146cc-145">Termes du contrat de licence de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="146cc-145">Holographic Remoting software license terms</span></span>](https://docs.microsoft.com/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [<span data-ttu-id="146cc-146">Déclaration de confidentialité Microsoft</span><span class="sxs-lookup"><span data-stu-id="146cc-146">Microsoft Privacy Statement</span></span>](https://go.microsoft.com/fwlink/?LinkId=521839)
