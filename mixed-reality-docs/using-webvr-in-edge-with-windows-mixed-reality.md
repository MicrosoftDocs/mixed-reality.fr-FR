---
title: À l’aide de WebVR dans Microsoft Edge avec Windows Mixed Reality
description: Vue d’ensemble de l’utilisation et de développement pour WebVR en réalité mixte Windows
author: YashMaster
ms.author: yabahman
ms.date: 03/21/2018
ms.topic: article
keywords: WebVR, WebXR, WinMR, WebAR, web vr, web xr, web mr, web ar, 360, 360 vidéo 360 vidéos, photo 360, 360 photos, 360, web immersive, du contenu immersiveweb, IW
ms.openlocfilehash: fab17f4dcecc34d8f1ca4836dce6de90522899cd
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596940"
---
# <a name="using-webvr-in-microsoft-edge-with-windows-mixed-reality"></a>À l’aide de WebVR dans Microsoft Edge avec Windows Mixed Reality

## <a name="creating-webvr-content-for-windows-mixed-reality-immersive-headsets"></a>Création des casques IMMERSIFS contenu WebVR pour la réalité mixte Windows

WebVR 1.1 est disponible dans le Windows 10 Fall Creators Update à compter de Microsoft Edge. Les développeurs peuvent maintenant utiliser cette API pour créer des expériences VR IMMERSIFS sur le web.

L’API WebVR fournit des données de pose HMD à la page qui peut être utilisée pour restituer un scène de WebGL stéréo vers le HMD. Plus d’informations sur la prise en charge de l’API est disponible sur le [page de l’état de la plateforme Microsoft Edge](https://developer.microsoft.com/microsoft-edge/platform/status/webvr/). La surface d’exposition WebVR API se trouve sur toutes les heures dans Microsoft Edge. Toutefois, un appel à getVRDisplays() retourne uniquement un casque si un casque est branché ou le simulateur a été activé.

## <a name="viewing-webvr-content-in-windows-mixed-reality-immersive-headsets"></a>Afficher le contenu de WebVR sur des casques IMMERSIFS Windows Mixed Reality

Vous trouverez des instructions pour accéder au contenu WebVR dans votre casque immersif dans le [Guide fans](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/webvr).

## <a name="see-also"></a>Voir aussi
* [Informations de WebVR](http://webvr.info)
* [Spécification de WebVR](https://w3c.github.io/webvr/)
* [WebVR API](https://msdn.microsoft.com/library/mt806281(v=vs.85).aspx)
* [API de WebGL](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)
* [Gamepad API](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) et [Gamepad Extensions](https://w3c.github.io/gamepad/extensions.html)
* [Gestion des perdu le contexte de WebGL](https://www.khronos.org/webgl/wiki/HandlingContextLost)
* [Pointerlock](http://www.w3.org/TR/pointerlock/)
* [glTF](https://www.khronos.org/gltf)
* [Activer WebVR à l’aide de la Babylon.js](https://docs.microsoft.com/windows/uwp/get-started/adding-webvr-to-a-babylonjs-game)

