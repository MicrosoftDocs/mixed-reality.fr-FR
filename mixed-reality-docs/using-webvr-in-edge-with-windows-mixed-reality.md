---
title: Utilisation de WebVR dans Microsoft Edge avec Windows Mixed Reality
description: Vue d’ensemble de l’utilisation et du développement pour WebVR dans Windows Mixed Reality
author: YashMaster
ms.author: yabahman
ms.date: 03/21/2018
ms.topic: article
keywords: WebVR, WebXR, WinMR, WebAR, Web VR, Web XR, Web Mr, Web AR, 360, 360 Video, 360 vidéos, 360 photo, 360 photos, 360 content, Internet immersif, immersiveweb, IW
ms.openlocfilehash: fab17f4dcecc34d8f1ca4836dce6de90522899cd
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63548762"
---
# <a name="using-webvr-in-microsoft-edge-with-windows-mixed-reality"></a>Utilisation de WebVR dans Microsoft Edge avec Windows Mixed Reality

## <a name="creating-webvr-content-for-windows-mixed-reality-immersive-headsets"></a>Création de contenu WebVR pour les casques immersifs Windows Mixed Reality

WebVR 1,1 est disponible dans Microsoft Edge à partir de la mise à jour de Windows 10 automne Creators. Les développeurs peuvent désormais utiliser cette API pour créer des expériences de VR immersif sur le Web.

L’API WebVR fournit des données de HMD à la page qui peuvent être utilisées pour restituer une scène WebGL stéréo dans le HMD. Des détails sur la prise en charge des API sont disponibles sur la page d’état de la [plateforme Microsoft Edge](https://developer.microsoft.com/microsoft-edge/platform/status/webvr/). La surface d’exposition de l’API WebVR est présente à tout moment dans Microsoft Edge. Toutefois, un appel à getVRDisplays () retourne un casque uniquement si un casque est branché ou si le simulateur a été mis sous tension.

## <a name="viewing-webvr-content-in-windows-mixed-reality-immersive-headsets"></a>Affichage du contenu WebVR dans les casques immersifs Windows Mixed Reality

Vous trouverez des instructions pour accéder au contenu de WebVR dans votre casque immersif dans le [Guide du passionné](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/webvr).

## <a name="see-also"></a>Voir aussi
* [Informations WebVR](http://webvr.info)
* [Spécification WebVR](https://w3c.github.io/webvr/)
* [API WebVR](https://msdn.microsoft.com/library/mt806281(v=vs.85).aspx)
* [API WebGL](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)
* [API du boîtier de manette](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) et les [extensions de boîtier](https://w3c.github.io/gamepad/extensions.html)
* [Gestion du contexte perdu dans WebGL](https://www.khronos.org/webgl/wiki/HandlingContextLost)
* [Pointerlock](http://www.w3.org/TR/pointerlock/)
* [glTF](https://www.khronos.org/gltf)
* [Utilisation de Babylon. js pour activer WebVR](https://docs.microsoft.com/windows/uwp/get-started/adding-webvr-to-a-babylonjs-game)

