---
title: Utilisation de WebVR dans Microsoft Edge avec Windows Mixed Reality
description: Vue d’ensemble de l’utilisation et du développement pour WebVR dans Windows Mixed Reality
author: YashMaster
ms.author: yabahman
ms.date: 03/21/2018
ms.topic: article
keywords: WebVR, WebXR, WinMR, WebAR, Web VR, Web XR, Web Mr, Web AR, 360, 360 Video, 360 vidéos, 360 photo, 360 photos, 360 content, Internet immersif, immersiveweb, IW
ms.openlocfilehash: 87805d2c40e9e63cdf3e432189b9deb7d575a380
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437206"
---
# <a name="using-webvr-in-microsoft-edge-with-windows-mixed-reality"></a><span data-ttu-id="f12cd-104">Utilisation de WebVR dans Microsoft Edge avec Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="f12cd-104">Using WebVR in Microsoft Edge with Windows Mixed Reality</span></span>

## <a name="creating-webvr-content-for-windows-mixed-reality-immersive-headsets"></a><span data-ttu-id="f12cd-105">Création de contenu WebVR pour les casques immersifs Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="f12cd-105">Creating WebVR content for Windows Mixed reality immersive headsets</span></span>

<span data-ttu-id="f12cd-106">WebVR 1,1 est disponible dans Microsoft Edge à partir de la mise à jour de Windows 10 automne Creators.</span><span class="sxs-lookup"><span data-stu-id="f12cd-106">WebVR 1.1 is available in Microsoft Edge beginning with the Windows 10 Fall Creators Update.</span></span> <span data-ttu-id="f12cd-107">Les développeurs peuvent désormais utiliser cette API pour créer des expériences de VR immersif sur le Web.</span><span class="sxs-lookup"><span data-stu-id="f12cd-107">Developers can now use this API to create immersive VR experiences on the web.</span></span>

<span data-ttu-id="f12cd-108">L’API WebVR fournit des données de HMD à la page qui peuvent être utilisées pour restituer une scène WebGL stéréo dans le HMD.</span><span class="sxs-lookup"><span data-stu-id="f12cd-108">The WebVR API provides HMD pose data to the page which can be used to render a stereo WebGL scene back to the HMD.</span></span> <span data-ttu-id="f12cd-109">Des détails sur la prise en charge des API sont disponibles sur la page d’état de la [plateforme Microsoft Edge](https://developer.microsoft.com/microsoft-edge/platform/status/webvr/).</span><span class="sxs-lookup"><span data-stu-id="f12cd-109">Details on API support is available on the [Microsoft Edge Platform Status page](https://developer.microsoft.com/microsoft-edge/platform/status/webvr/).</span></span> <span data-ttu-id="f12cd-110">La surface d’exposition de l’API WebVR est présente à tout moment dans Microsoft Edge.</span><span class="sxs-lookup"><span data-stu-id="f12cd-110">The WebVR API surface area is present at all times within Microsoft Edge.</span></span> <span data-ttu-id="f12cd-111">Toutefois, un appel à getVRDisplays () retourne un casque uniquement si un casque est branché ou si le simulateur a été mis sous tension.</span><span class="sxs-lookup"><span data-stu-id="f12cd-111">However, a call to getVRDisplays() will only return a headset if either a headset is plugged in or the simulator has been turned on.</span></span>

## <a name="viewing-webvr-content-in-windows-mixed-reality-immersive-headsets"></a><span data-ttu-id="f12cd-112">Affichage du contenu WebVR dans les casques immersifs Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="f12cd-112">Viewing WebVR content in Windows Mixed Reality immersive headsets</span></span>

<span data-ttu-id="f12cd-113">Vous trouverez des instructions pour accéder au contenu de WebVR dans votre casque immersif dans le [Guide du passionné](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/webvr).</span><span class="sxs-lookup"><span data-stu-id="f12cd-113">Instructions for accessing WebVR content in your immersive headset can be found in the [Enthusiast's Guide](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/webvr).</span></span>

## <a name="see-also"></a><span data-ttu-id="f12cd-114">Articles associés</span><span class="sxs-lookup"><span data-stu-id="f12cd-114">See Also</span></span>
* [<span data-ttu-id="f12cd-115">Informations WebVR</span><span class="sxs-lookup"><span data-stu-id="f12cd-115">WebVR information</span></span>](https://webvr.info)
* [<span data-ttu-id="f12cd-116">Spécification WebVR</span><span class="sxs-lookup"><span data-stu-id="f12cd-116">WebVR specification</span></span>](https://w3c.github.io/webvr/)
* <span data-ttu-id="f12cd-117">[API WebVR](https://msdn.microsoft.com/library/mt806281(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="f12cd-117">[WebVR API](https://msdn.microsoft.com/library/mt806281(v=vs.85).aspx)</span></span>
* <span data-ttu-id="f12cd-118">[API WebGL](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="f12cd-118">[WebGL API](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)</span></span>
* <span data-ttu-id="f12cd-119">[API du boîtier de manette](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) et les [extensions de boîtier](https://w3c.github.io/gamepad/extensions.html)</span><span class="sxs-lookup"><span data-stu-id="f12cd-119">[Gamepad API](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) and [Gamepad Extensions](https://w3c.github.io/gamepad/extensions.html)</span></span>
* [<span data-ttu-id="f12cd-120">Gestion du contexte perdu dans WebGL</span><span class="sxs-lookup"><span data-stu-id="f12cd-120">Handling Lost Context in WebGL</span></span>](https://www.khronos.org/webgl/wiki/HandlingContextLost)
* [<span data-ttu-id="f12cd-121">Pointerlock</span><span class="sxs-lookup"><span data-stu-id="f12cd-121">Pointerlock</span></span>](https://www.w3.org/TR/pointerlock/)
* [<span data-ttu-id="f12cd-122">glTF</span><span class="sxs-lookup"><span data-stu-id="f12cd-122">glTF</span></span>](https://www.khronos.org/gltf)
* [<span data-ttu-id="f12cd-123">Utilisation de Babylon. js pour activer WebVR</span><span class="sxs-lookup"><span data-stu-id="f12cd-123">Using Babylon.js to enable WebVR</span></span>](https://docs.microsoft.com/windows/uwp/get-started/adding-webvr-to-a-babylonjs-game)

