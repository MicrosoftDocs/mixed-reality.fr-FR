---
title: Historique des versions de la communication à distance holographique
description: Historique des versions de la communication à distance holographique sur HoloLens 2.
author: NPohl-MSFT
ms.author: nopohl
ms.date: 10/21/2019
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: 75e7c276560b4efbbdcbf2ea7579ed5ad7aadb4d
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73439230"
---
# <a name="holographic-remoting-version-history"></a><span data-ttu-id="e53b2-104">Historique des versions de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="e53b2-104">Holographic Remoting Version History</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e53b2-105">Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="e53b2-105">This guidance is specific to Holographic Remoting on HoloLens 2.</span></span>

## <span data-ttu-id="e53b2-106">Version 2.0.14 (26 octobre 2019)<a name="v2.0.14"></a></span><span class="sxs-lookup"><span data-stu-id="e53b2-106">Version 2.0.14 (October 26, 2019) <a name="v2.0.14"></a></span></span>
* <span data-ttu-id="e53b2-107">Prise en charge des nouvelles API PerceptionDevice (mise à jour de novembre 2019 de Windows 10).</span><span class="sxs-lookup"><span data-stu-id="e53b2-107">Support for new PerceptionDevice APIs (Windows 10 November 2019 Update).</span></span>
* <span data-ttu-id="e53b2-108">Résolution du problème qui empêche les événements de mouvement de maintien déclenchés par SpatialGestureRecognizer.</span><span class="sxs-lookup"><span data-stu-id="e53b2-108">Fixed issue which prevent hold gesture events being triggered by SpatialGestureRecognizer.</span></span>
* <span data-ttu-id="e53b2-109">Correction du problème theading lors de l’utilisation de SpatialSurfaceObserver. SetBoundingVolume.</span><span class="sxs-lookup"><span data-stu-id="e53b2-109">Fixed theading issue when using SpatialSurfaceObserver.SetBoundingVolume.</span></span>

## <span data-ttu-id="e53b2-110">Version 2.0.12 (18 octobre 2019)<a name="v2.0.12"></a></span><span class="sxs-lookup"><span data-stu-id="e53b2-110">Version 2.0.12 (October 18, 2019) <a name="v2.0.12"></a></span></span>
* <span data-ttu-id="e53b2-111">Correction d’un incident dans SpatialGestureRecognizer lors de l’utilisation de NavigationRail (X/Y/Z).</span><span class="sxs-lookup"><span data-stu-id="e53b2-111">Fixed crash in SpatialGestureRecognizer when using NavigationRail(X/Y/Z).</span></span>

## <span data-ttu-id="e53b2-112">Version 2.0.10 (10 octobre 2019)<a name="v2.0.10"></a></span><span class="sxs-lookup"><span data-stu-id="e53b2-112">Version 2.0.10 (October 10, 2019) <a name="v2.0.10"></a></span></span>
* <span data-ttu-id="e53b2-113">Résolution d’un incident lors de l’utilisation du bouton déclencheur des contrôleurs VR.</span><span class="sxs-lookup"><span data-stu-id="e53b2-113">Fixed crash when using trigger button of VR controllers.</span></span> <span data-ttu-id="e53b2-114">La communication à distance holographique ne prend pas entièrement en charge les contrôleurs, mais uniquement le bouton déclencheur et le bouton Windows fonctionnent s’ils sont associés à HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="e53b2-114">Holographic Remoting does not fully support controllers, only the trigger button and the Windows button are working if paired with HoloLens 2.</span></span>

## <span data-ttu-id="e53b2-115">Version 2.0.9 (19 septembre 2019)<a name="v2.0.9"></a></span><span class="sxs-lookup"><span data-stu-id="e53b2-115">Version 2.0.9 (September 19, 2019) <a name="v2.0.9"></a></span></span>
* <span data-ttu-id="e53b2-116">Ajout de la prise en charge de [SpatialAnchorExporter](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter)</span><span class="sxs-lookup"><span data-stu-id="e53b2-116">Added support for [SpatialAnchorExporter](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter)</span></span>
* <span data-ttu-id="e53b2-117">Ajout d’une nouvelle interface ```IPlayerContext2``` (implémenté par ```PlayerContext```) fournissant les membres suivants :</span><span class="sxs-lookup"><span data-stu-id="e53b2-117">Added new interface ```IPlayerContext2``` (implemented by ```PlayerContext```) providing the following members:</span></span>
  - <span data-ttu-id="e53b2-118">Propriété [BlitRemoteFrameTimeout](holographic-remoting-create-player.md#BlitRemoteFrameTimeout) .</span><span class="sxs-lookup"><span data-stu-id="e53b2-118">[BlitRemoteFrameTimeout](holographic-remoting-create-player.md#BlitRemoteFrameTimeout)  property.</span></span>
* <span data-ttu-id="e53b2-119">Ajout de la valeur ```Failed_RemoteFrameTooOld``` à ```BlitResult```</span><span class="sxs-lookup"><span data-stu-id="e53b2-119">Added ```Failed_RemoteFrameTooOld``` value to ```BlitResult```</span></span>
* <span data-ttu-id="e53b2-120">Améliorations de la stabilité et de la fiabilité</span><span class="sxs-lookup"><span data-stu-id="e53b2-120">Stability and reliability improvements</span></span>

## <span data-ttu-id="e53b2-121">Version 2.0.8 (20 août, 2019)<a name="v2.0.8"></a></span><span class="sxs-lookup"><span data-stu-id="e53b2-121">Version 2.0.8 (August 20, 2019) <a name="v2.0.8"></a></span></span>

* <span data-ttu-id="e53b2-122">Résolution d’un incident lors de l’appel de [HolographicCameraRenderingParameters. CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer) avec un paramètre [IDXGISurface2](https://docs.microsoft.com/windows/win32/api/dxgi1_2/nn-dxgi1_2-idxgisurface2) .</span><span class="sxs-lookup"><span data-stu-id="e53b2-122">Fixed crash when calling [HolographicCameraRenderingParameters.CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer) with a [IDXGISurface2](https://docs.microsoft.com/windows/win32/api/dxgi1_2/nn-dxgi1_2-idxgisurface2) as parameter.</span></span>
* <span data-ttu-id="e53b2-123">Améliorations de la stabilité et de la fiabilité</span><span class="sxs-lookup"><span data-stu-id="e53b2-123">Stability and reliability improvements</span></span>

## <span data-ttu-id="e53b2-124">Version 2.0.7 (26 juillet, 2019)<a name="v2.0.7"></a></span><span class="sxs-lookup"><span data-stu-id="e53b2-124">Version 2.0.7 (July 26, 2019) <a name="v2.0.7"></a></span></span>

* <span data-ttu-id="e53b2-125">Première version publique de la communication à distance holographique pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="e53b2-125">First public release of Holographic Remoting for HoloLens 2.</span></span>

## <a name="see-also"></a><span data-ttu-id="e53b2-126">Articles associés</span><span class="sxs-lookup"><span data-stu-id="e53b2-126">See Also</span></span>
* [<span data-ttu-id="e53b2-127">Écriture d’une application de lecteur de communication à distance holographique personnalisée</span><span class="sxs-lookup"><span data-stu-id="e53b2-127">Writing a custom Holographic Remoting player app</span></span>](holographic-remoting-create-player.md)
* [<span data-ttu-id="e53b2-128">Écriture d’une application hôte de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="e53b2-128">Writing a Holographic Remoting host app</span></span>](holographic-remoting-create-host.md)
* [<span data-ttu-id="e53b2-129">Résolution des problèmes et limitations de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="e53b2-129">Holographic Remoting troubleshooting and limitations</span></span>](holographic-remoting-troubleshooting.md)
* [<span data-ttu-id="e53b2-130">Termes du contrat de licence de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="e53b2-130">Holographic Remoting software license terms</span></span>](https://docs.microsoft.com/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [<span data-ttu-id="e53b2-131">Déclaration de confidentialité Microsoft</span><span class="sxs-lookup"><span data-stu-id="e53b2-131">Microsoft Privacy Statement</span></span>](https://go.microsoft.com/fwlink/?LinkId=521839)
