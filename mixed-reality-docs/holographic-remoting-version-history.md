---
title: Historique des versions de la communication à distance holographique
description: Historique des versions de la communication à distance holographique sur HoloLens 2.
author: florianbagarmicrosoft
ms.author: flbagar
ms.date: 03/11/2020
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: 319e76efbbe1085fc9d60251a6f0f38133de6505
ms.sourcegitcommit: 7011ac6fde80e5c45f04192fa1db6e1eb559e3b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/03/2020
ms.locfileid: "84327899"
---
# <a name="holographic-remoting-version-history"></a>Historique des versions de la communication à distance holographique

> [!IMPORTANT]
> Ce guide est spécifique à la communication à distance holographique sur HoloLens 2.

## <a name="version-213-may-25-2020"></a>Version 2.1.3 (25 mai, 2020)<a name="v2.1.3"></a>
* Modification du comportement de l’événement [HolographicSpace. CameraAdded](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace.cameraadded?view=winrt-18362) . Dans les versions précédentes, il n’était **pas** garanti qu’un [HolographicCamera](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera?view=winrt-18362) ajouté ait également un [HolographicCameraPose](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerapose?view=winrt-18362) valide lors de la création du frame suivant via [HolographicSpace. CreateNextFrame](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace.createnextframe?view=winrt-18362#Windows_Graphics_Holographic_HolographicSpace_CreateNextFrame). À compter de la version 2.1.3 [HolographicSpace. CameraAdded](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace.cameraadded?view=winrt-18362) est synchronisé avec les données de pose provenant du joueur de communication à distance holographique et les utilisateurs peuvent s’attendre à ce que, quand une caméra est ajoutée, un [HolographicCameraPose](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerapose?view=winrt-18362) valide soit disponible pour cette caméra dans le cadre suivant.
* Ajout de **désactivé** à DepthBufferStreamResolution qui peut être utilisé pour désactiver la diffusion en continu de tampons de profondeur via RemoteContext. ConfigureDepthVideoStream. Notez que s’il est utilisé, [HolographicCameraRenderingParameters. CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer?view=winrt-18362#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_) échouera avec *E_ILLEGAL_METHOD_CALL*.
* L’écran de démarrage du lecteur de communication à distance holographique a été reconçu et ne bloque pas la vue des utilisateurs.
* Améliorations de la stabilité et correctifs de bogues.

## <a name="version-212-april-5-2020"></a>Version 2.1.2 (5 avril 2020)<a name="v2.1.2"></a>
* Résolution d’un problème de compatibilité descendante audio entre le dernier lecteur de communication à distance holographique et les applications distantes utilisant une version inférieure à 2.1.0.
* Problème fixe d’ancrage spatial qui a fermé de manière inattendue le lecteur de communication à distance holographique. Ce problème affecte également les lecteurs personnalisés.

## <a name="version-211-march-20-2020"></a>Version 2.1.1 (20 mars, 2020)<a name="v2.1.1"></a>
* Résolution d’un problème de codage vidéo avec les applications distantes lors de l’utilisation des GPU AMD.
* Améliorations des performances du lecteur de communication à distance holographique.

## <a name="version-210-march-11-2020"></a>Version 2.1.0 (11 mars, 2020)<a name="v2.1.0"></a>
* Transport réseau commuté pour utiliser [RTP](https://en.wikipedia.org/wiki/Real-time_Transport_Protocol) via UDP. Les connexions sécurisées utilisent [SRTP](https://en.wikipedia.org/wiki/Secure_Real-time_Transport_Protocol) Now. Notez que le [lecteur de communication à distance holographique](holographic-remoting-player.md) est toujours compatible avec toutes les versions de Remoting holographiques antérieures. Pour tirer parti du nouveau transport réseau, le lecteur de communication à distance holographique et l’application distante en question doivent utiliser la version 2.1.0.
* Ajout de la prise en charge de [HolographicCameraRenderingParameters. CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_). 

## <a name="version-2020-february-2-2020"></a>Version 2.0.20 (2 février 2020)<a name="v2.0.20"></a>
* Correction de divers bogues qui mènent à des incidents.

## <a name="version-2018-december-17-2019"></a>Version 2.0.18 (17 décembre 2019)<a name="v2.0.18"></a>
* Ajout de la prise en charge de [HolographicViewConfiguration](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicviewconfiguration)
* Correction de divers bogues qui mènent à des incidents.
* Correction d’un bogue où un rappel HolographicSpace. CameraAdded était nécessaire pour qu’un HolographicCamera soit accepté et apparaissait comme caméra ajoutée dans le HolographicFrame.

## <a name="version-2016-november-11-2019"></a>Version 2.0.16 (11 novembre 2019)<a name="2.0.16"></a>
* Correction du blocage dans le suivi du code QR.
* Correction de l’exception unhandeled en raison d’une attente de blocage dans le thread principal.

## <a name="version-2014-october-26-2019"></a>Version 2.0.14 (26 octobre 2019)<a name="v2.0.14"></a>
* Prise en charge des nouvelles API PerceptionDevice (mise à jour de novembre 2019 de Windows 10).
* Résolution du problème qui empêche les événements de mouvement de maintien déclenchés par SpatialGestureRecognizer.
* Problème de thread fixe lors de l’utilisation de SpatialSurfaceObserver. SetBoundingVolume.

## <a name="version-2012-october-18-2019"></a>Version 2.0.12 (18 octobre 2019)<a name="v2.0.12"></a>
* Correction d’un incident dans SpatialGestureRecognizer lors de l’utilisation de NavigationRail (X/Y/Z).

## <a name="version-2010-october-10-2019"></a>Version 2.0.10 (10 octobre 2019)<a name="v2.0.10"></a>
* Résolution d’un incident lors de l’utilisation du bouton déclencheur des contrôleurs VR. La communication à distance holographique ne prend pas entièrement en charge les contrôleurs, mais uniquement le bouton déclencheur et le bouton Windows fonctionnent s’ils sont associés à HoloLens 2.

## <a name="version-209-september-19-2019"></a>Version 2.0.9 (19 septembre 2019)<a name="v2.0.9"></a>
* Ajout de la prise en charge de [SpatialAnchorExporter](https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchorexporter)
* Ajout ```IPlayerContext2``` d’une nouvelle interface (implémentée par ```PlayerContext``` ) fournissant les membres suivants :
  - Propriété [BlitRemoteFrameTimeout](holographic-remoting-create-player.md#BlitRemoteFrameTimeout) .
* ```Failed_RemoteFrameTooOld```Valeur ajoutée à```BlitResult```
* Améliorations de la stabilité et de la fiabilité

## <a name="version-208-august-20-2019"></a>Version 2.0.8 (20 août, 2019)<a name="v2.0.8"></a>

* Résolution d’un incident lors de l’appel de [HolographicCameraRenderingParameters. CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer) avec un paramètre [IDXGISurface2](https://docs.microsoft.com/windows/win32/api/dxgi1_2/nn-dxgi1_2-idxgisurface2) .
* Améliorations de la stabilité et de la fiabilité

## <a name="version-207-july-26-2019"></a>Version 2.0.7 (26 juillet, 2019)<a name="v2.0.7"></a>

* Première version publique de la communication à distance holographique pour HoloLens 2.

## <a name="see-also"></a>Voir aussi
* [Écriture d’une application de lecteur de communication à distance holographique personnalisée](holographic-remoting-create-player.md)
* [Écriture d’une application hôte de communication à distance holographique](holographic-remoting-create-host.md)
* [Résolution des problèmes et limitations de la communication à distance holographique](holographic-remoting-troubleshooting.md)
* [Termes du contrat de licence de la communication à distance holographique](https://docs.microsoft.com/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [Déclaration de confidentialité Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
