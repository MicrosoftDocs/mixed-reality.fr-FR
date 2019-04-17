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
# <a name="using-webvr-in-microsoft-edge-with-windows-mixed-reality"></a><span data-ttu-id="8ed27-104">À l’aide de WebVR dans Microsoft Edge avec Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="8ed27-104">Using WebVR in Microsoft Edge with Windows Mixed Reality</span></span>

## <a name="creating-webvr-content-for-windows-mixed-reality-immersive-headsets"></a><span data-ttu-id="8ed27-105">Création des casques IMMERSIFS contenu WebVR pour la réalité mixte Windows</span><span class="sxs-lookup"><span data-stu-id="8ed27-105">Creating WebVR content for Windows Mixed reality immersive headsets</span></span>

<span data-ttu-id="8ed27-106">WebVR 1.1 est disponible dans le Windows 10 Fall Creators Update à compter de Microsoft Edge.</span><span class="sxs-lookup"><span data-stu-id="8ed27-106">WebVR 1.1 is available in Microsoft Edge beginning with the Windows 10 Fall Creators Update.</span></span> <span data-ttu-id="8ed27-107">Les développeurs peuvent maintenant utiliser cette API pour créer des expériences VR IMMERSIFS sur le web.</span><span class="sxs-lookup"><span data-stu-id="8ed27-107">Developers can now use this API to create immersive VR experiences on the web.</span></span>

<span data-ttu-id="8ed27-108">L’API WebVR fournit des données de pose HMD à la page qui peut être utilisée pour restituer un scène de WebGL stéréo vers le HMD.</span><span class="sxs-lookup"><span data-stu-id="8ed27-108">The WebVR API provides HMD pose data to the page which can be used to render a stereo WebGL scene back to the HMD.</span></span> <span data-ttu-id="8ed27-109">Plus d’informations sur la prise en charge de l’API est disponible sur le [page de l’état de la plateforme Microsoft Edge](https://developer.microsoft.com/microsoft-edge/platform/status/webvr/).</span><span class="sxs-lookup"><span data-stu-id="8ed27-109">Details on API support is available on the [Microsoft Edge Platform Status page](https://developer.microsoft.com/microsoft-edge/platform/status/webvr/).</span></span> <span data-ttu-id="8ed27-110">La surface d’exposition WebVR API se trouve sur toutes les heures dans Microsoft Edge.</span><span class="sxs-lookup"><span data-stu-id="8ed27-110">The WebVR API surface area is present at all times within Microsoft Edge.</span></span> <span data-ttu-id="8ed27-111">Toutefois, un appel à getVRDisplays() retourne uniquement un casque si un casque est branché ou le simulateur a été activé.</span><span class="sxs-lookup"><span data-stu-id="8ed27-111">However, a call to getVRDisplays() will only return a headset if either a headset is plugged in or the simulator has been turned on.</span></span>

## <a name="viewing-webvr-content-in-windows-mixed-reality-immersive-headsets"></a><span data-ttu-id="8ed27-112">Afficher le contenu de WebVR sur des casques IMMERSIFS Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="8ed27-112">Viewing WebVR content in Windows Mixed Reality immersive headsets</span></span>

<span data-ttu-id="8ed27-113">Vous trouverez des instructions pour accéder au contenu WebVR dans votre casque immersif dans le [Guide fans](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/webvr).</span><span class="sxs-lookup"><span data-stu-id="8ed27-113">Instructions for accessing WebVR content in your immersive headset can be found in the [Enthusiast's Guide](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/webvr).</span></span>

## <a name="see-also"></a><span data-ttu-id="8ed27-114">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8ed27-114">See Also</span></span>
* [<span data-ttu-id="8ed27-115">Informations de WebVR</span><span class="sxs-lookup"><span data-stu-id="8ed27-115">WebVR information</span></span>](http://webvr.info)
* [<span data-ttu-id="8ed27-116">Spécification de WebVR</span><span class="sxs-lookup"><span data-stu-id="8ed27-116">WebVR specification</span></span>](https://w3c.github.io/webvr/)
* <span data-ttu-id="8ed27-117">[WebVR API](https://msdn.microsoft.com/library/mt806281(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="8ed27-117">[WebVR API](https://msdn.microsoft.com/library/mt806281(v=vs.85).aspx)</span></span>
* <span data-ttu-id="8ed27-118">[API de WebGL](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="8ed27-118">[WebGL API](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)</span></span>
* <span data-ttu-id="8ed27-119">[Gamepad API](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) et [Gamepad Extensions](https://w3c.github.io/gamepad/extensions.html)</span><span class="sxs-lookup"><span data-stu-id="8ed27-119">[Gamepad API](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) and [Gamepad Extensions](https://w3c.github.io/gamepad/extensions.html)</span></span>
* [<span data-ttu-id="8ed27-120">Gestion des perdu le contexte de WebGL</span><span class="sxs-lookup"><span data-stu-id="8ed27-120">Handling Lost Context in WebGL</span></span>](https://www.khronos.org/webgl/wiki/HandlingContextLost)
* [<span data-ttu-id="8ed27-121">Pointerlock</span><span class="sxs-lookup"><span data-stu-id="8ed27-121">Pointerlock</span></span>](http://www.w3.org/TR/pointerlock/)
* [<span data-ttu-id="8ed27-122">glTF</span><span class="sxs-lookup"><span data-stu-id="8ed27-122">glTF</span></span>](https://www.khronos.org/gltf)
* [<span data-ttu-id="8ed27-123">Activer WebVR à l’aide de la Babylon.js</span><span class="sxs-lookup"><span data-stu-id="8ed27-123">Using Babylon.js to enable WebVR</span></span>](https://docs.microsoft.com/windows/uwp/get-started/adding-webvr-to-a-babylonjs-game)

