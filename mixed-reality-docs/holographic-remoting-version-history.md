---
title: Historique des versions de la communication à distance holographique
description: Historique des versions de la communication à distance holographique sur HoloLens 2.
author: NPohl-MSFT
ms.author: nopohl
ms.date: 10/21/2019
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: f051dbf24cab550470a312933ffb99e1ba595257
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75181959"
---
# <a name="holographic-remoting-version-history"></a><span data-ttu-id="f3d2d-104">Historique des versions de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="f3d2d-104">Holographic Remoting Version History</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3d2d-105">Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="f3d2d-105">This guidance is specific to Holographic Remoting on HoloLens 2.</span></span>

## <span data-ttu-id="f3d2d-106">Version 2.0.18.0 (17 décembre 2019)<a name="v2.0.18"></a></span><span class="sxs-lookup"><span data-stu-id="f3d2d-106">Version 2.0.18.0 (December 17, 2019) <a name="v2.0.18"></a></span></span>
* <span data-ttu-id="f3d2d-107">Ajout de la prise en charge de HolographicViewConfiguration : https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicviewconfiguration</span><span class="sxs-lookup"><span data-stu-id="f3d2d-107">Added support for HolographicViewConfiguration: https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicviewconfiguration</span></span>
* <span data-ttu-id="f3d2d-108">Correction de divers bogues qui mènent à des incidents.</span><span class="sxs-lookup"><span data-stu-id="f3d2d-108">Fixed various bugs that lead to crashes.</span></span>
* <span data-ttu-id="f3d2d-109">Correction d’un bogue où un rappel HolographicSpace. CameraAdded était nécessaire pour qu’un HolographicCamera soit accepté et apparaissait comme caméra ajoutée dans le HoloraphicFrame.</span><span class="sxs-lookup"><span data-stu-id="f3d2d-109">Fixed bug where a HolographicSpace.CameraAdded callback was required for a HolographicCamera to get accepted and show up as added camera in the HoloraphicFrame.</span></span>

## <span data-ttu-id="f3d2d-110">Version 2.0.16 (11 novembre 2019)<a name="2.0.16"></a></span><span class="sxs-lookup"><span data-stu-id="f3d2d-110">Version 2.0.16 (November 11, 2019) <a name="2.0.16"></a></span></span>
* <span data-ttu-id="f3d2d-111">Correction du blocage dans le suivi du code QR.</span><span class="sxs-lookup"><span data-stu-id="f3d2d-111">Fixed deadlock in QR code tracking.</span></span>
* <span data-ttu-id="f3d2d-112">Correction de l’exception unhandeled en raison d’une attente de blocage dans le thread principal.</span><span class="sxs-lookup"><span data-stu-id="f3d2d-112">Fixed unhandeled exception due to blocking wait in main thread.</span></span>

## <span data-ttu-id="f3d2d-113">Version 2.0.14 (26 octobre 2019)<a name="v2.0.14"></a></span><span class="sxs-lookup"><span data-stu-id="f3d2d-113">Version 2.0.14 (October 26, 2019) <a name="v2.0.14"></a></span></span>
* <span data-ttu-id="f3d2d-114">Prise en charge des nouvelles API PerceptionDevice (mise à jour de novembre 2019 de Windows 10).</span><span class="sxs-lookup"><span data-stu-id="f3d2d-114">Support for new PerceptionDevice APIs (Windows 10 November 2019 Update).</span></span>
* <span data-ttu-id="f3d2d-115">Résolution du problème qui empêche les événements de mouvement de maintien déclenchés par SpatialGestureRecognizer.</span><span class="sxs-lookup"><span data-stu-id="f3d2d-115">Fixed issue which prevent hold gesture events being triggered by SpatialGestureRecognizer.</span></span>
* <span data-ttu-id="f3d2d-116">Problème de thread fixe lors de l’utilisation de SpatialSurfaceObserver. SetBoundingVolume.</span><span class="sxs-lookup"><span data-stu-id="f3d2d-116">Fixed threading issue when using SpatialSurfaceObserver.SetBoundingVolume.</span></span>

## <span data-ttu-id="f3d2d-117">Version 2.0.12 (18 octobre 2019)<a name="v2.0.12"></a></span><span class="sxs-lookup"><span data-stu-id="f3d2d-117">Version 2.0.12 (October 18, 2019) <a name="v2.0.12"></a></span></span>
* <span data-ttu-id="f3d2d-118">Correction d’un incident dans SpatialGestureRecognizer lors de l’utilisation de NavigationRail (X/Y/Z).</span><span class="sxs-lookup"><span data-stu-id="f3d2d-118">Fixed crash in SpatialGestureRecognizer when using NavigationRail(X/Y/Z).</span></span>

## <span data-ttu-id="f3d2d-119">Version 2.0.10 (10 octobre 2019)<a name="v2.0.10"></a></span><span class="sxs-lookup"><span data-stu-id="f3d2d-119">Version 2.0.10 (October 10, 2019) <a name="v2.0.10"></a></span></span>
* <span data-ttu-id="f3d2d-120">Résolution d’un incident lors de l’utilisation du bouton déclencheur des contrôleurs VR.</span><span class="sxs-lookup"><span data-stu-id="f3d2d-120">Fixed crash when using trigger button of VR controllers.</span></span> <span data-ttu-id="f3d2d-121">La communication à distance holographique ne prend pas entièrement en charge les contrôleurs, mais uniquement le bouton déclencheur et le bouton Windows fonctionnent s’ils sont associés à HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="f3d2d-121">Holographic Remoting does not fully support controllers, only the trigger button and the Windows button are working if paired with HoloLens 2.</span></span>

## <span data-ttu-id="f3d2d-122">Version 2.0.9 (19 septembre 2019)<a name="v2.0.9"></a></span><span class="sxs-lookup"><span data-stu-id="f3d2d-122">Version 2.0.9 (September 19, 2019) <a name="v2.0.9"></a></span></span>
* <span data-ttu-id="f3d2d-123">Ajout de la prise en charge de [SpatialAnchorExporter](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter)</span><span class="sxs-lookup"><span data-stu-id="f3d2d-123">Added support for [SpatialAnchorExporter](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter)</span></span>
* <span data-ttu-id="f3d2d-124">Ajout d’une nouvelle interface ```IPlayerContext2``` (implémenté par ```PlayerContext```) fournissant les membres suivants :</span><span class="sxs-lookup"><span data-stu-id="f3d2d-124">Added new interface ```IPlayerContext2``` (implemented by ```PlayerContext```) providing the following members:</span></span>
  - <span data-ttu-id="f3d2d-125">Propriété [BlitRemoteFrameTimeout](holographic-remoting-create-player.md#BlitRemoteFrameTimeout) .</span><span class="sxs-lookup"><span data-stu-id="f3d2d-125">[BlitRemoteFrameTimeout](holographic-remoting-create-player.md#BlitRemoteFrameTimeout)  property.</span></span>
* <span data-ttu-id="f3d2d-126">Ajout de la valeur ```Failed_RemoteFrameTooOld``` à ```BlitResult```</span><span class="sxs-lookup"><span data-stu-id="f3d2d-126">Added ```Failed_RemoteFrameTooOld``` value to ```BlitResult```</span></span>
* <span data-ttu-id="f3d2d-127">Améliorations de la stabilité et de la fiabilité</span><span class="sxs-lookup"><span data-stu-id="f3d2d-127">Stability and reliability improvements</span></span>

## <span data-ttu-id="f3d2d-128">Version 2.0.8 (20 août, 2019)<a name="v2.0.8"></a></span><span class="sxs-lookup"><span data-stu-id="f3d2d-128">Version 2.0.8 (August 20, 2019) <a name="v2.0.8"></a></span></span>

* <span data-ttu-id="f3d2d-129">Résolution d’un incident lors de l’appel de [HolographicCameraRenderingParameters. CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer) avec un paramètre [IDXGISurface2](https://docs.microsoft.com/windows/win32/api/dxgi1_2/nn-dxgi1_2-idxgisurface2) .</span><span class="sxs-lookup"><span data-stu-id="f3d2d-129">Fixed crash when calling [HolographicCameraRenderingParameters.CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer) with a [IDXGISurface2](https://docs.microsoft.com/windows/win32/api/dxgi1_2/nn-dxgi1_2-idxgisurface2) as parameter.</span></span>
* <span data-ttu-id="f3d2d-130">Améliorations de la stabilité et de la fiabilité</span><span class="sxs-lookup"><span data-stu-id="f3d2d-130">Stability and reliability improvements</span></span>

## <span data-ttu-id="f3d2d-131">Version 2.0.7 (26 juillet, 2019)<a name="v2.0.7"></a></span><span class="sxs-lookup"><span data-stu-id="f3d2d-131">Version 2.0.7 (July 26, 2019) <a name="v2.0.7"></a></span></span>

* <span data-ttu-id="f3d2d-132">Première version publique de la communication à distance holographique pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="f3d2d-132">First public release of Holographic Remoting for HoloLens 2.</span></span>

## <a name="see-also"></a><span data-ttu-id="f3d2d-133">Articles associés</span><span class="sxs-lookup"><span data-stu-id="f3d2d-133">See Also</span></span>
* [<span data-ttu-id="f3d2d-134">Écriture d’une application de lecteur de communication à distance holographique personnalisée</span><span class="sxs-lookup"><span data-stu-id="f3d2d-134">Writing a custom Holographic Remoting player app</span></span>](holographic-remoting-create-player.md)
* [<span data-ttu-id="f3d2d-135">Écriture d’une application hôte de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="f3d2d-135">Writing a Holographic Remoting host app</span></span>](holographic-remoting-create-host.md)
* [<span data-ttu-id="f3d2d-136">Résolution des problèmes et limitations de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="f3d2d-136">Holographic Remoting troubleshooting and limitations</span></span>](holographic-remoting-troubleshooting.md)
* [<span data-ttu-id="f3d2d-137">Termes du contrat de licence de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="f3d2d-137">Holographic Remoting software license terms</span></span>](https://docs.microsoft.com/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [<span data-ttu-id="f3d2d-138">Déclaration de confidentialité de Microsoft</span><span class="sxs-lookup"><span data-stu-id="f3d2d-138">Microsoft Privacy Statement</span></span>](https://go.microsoft.com/fwlink/?LinkId=521839)
