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
# <a name="holographic-remoting-version-history"></a>Historique des versions de la communication à distance holographique

> [!IMPORTANT]
> Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.

## Version 2.0.14 (26 octobre 2019)<a name="v2.0.14"></a>
* Prise en charge des nouvelles API PerceptionDevice (mise à jour de novembre 2019 de Windows 10).
* Résolution du problème qui empêche les événements de mouvement de maintien déclenchés par SpatialGestureRecognizer.
* Correction du problème theading lors de l’utilisation de SpatialSurfaceObserver. SetBoundingVolume.

## Version 2.0.12 (18 octobre 2019)<a name="v2.0.12"></a>
* Correction d’un incident dans SpatialGestureRecognizer lors de l’utilisation de NavigationRail (X/Y/Z).

## Version 2.0.10 (10 octobre 2019)<a name="v2.0.10"></a>
* Résolution d’un incident lors de l’utilisation du bouton déclencheur des contrôleurs VR. La communication à distance holographique ne prend pas entièrement en charge les contrôleurs, mais uniquement le bouton déclencheur et le bouton Windows fonctionnent s’ils sont associés à HoloLens 2.

## Version 2.0.9 (19 septembre 2019)<a name="v2.0.9"></a>
* Ajout de la prise en charge de [SpatialAnchorExporter](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter)
* Ajout d’une nouvelle interface ```IPlayerContext2``` (implémenté par ```PlayerContext```) fournissant les membres suivants :
  - Propriété [BlitRemoteFrameTimeout](holographic-remoting-create-player.md#BlitRemoteFrameTimeout) .
* Ajout de la valeur ```Failed_RemoteFrameTooOld``` à ```BlitResult```
* Améliorations de la stabilité et de la fiabilité

## Version 2.0.8 (20 août, 2019)<a name="v2.0.8"></a>

* Résolution d’un incident lors de l’appel de [HolographicCameraRenderingParameters. CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer) avec un paramètre [IDXGISurface2](https://docs.microsoft.com/windows/win32/api/dxgi1_2/nn-dxgi1_2-idxgisurface2) .
* Améliorations de la stabilité et de la fiabilité

## Version 2.0.7 (26 juillet, 2019)<a name="v2.0.7"></a>

* Première version publique de la communication à distance holographique pour HoloLens 2.

## <a name="see-also"></a>Articles associés
* [Écriture d’une application de lecteur de communication à distance holographique personnalisée](holographic-remoting-create-player.md)
* [Écriture d’une application hôte de communication à distance holographique](holographic-remoting-create-host.md)
* [Résolution des problèmes et limitations de la communication à distance holographique](holographic-remoting-troubleshooting.md)
* [Termes du contrat de licence de la communication à distance holographique](https://docs.microsoft.com/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [Déclaration de confidentialité Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
