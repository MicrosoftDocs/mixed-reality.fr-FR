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
# <a name="using-webvr-in-microsoft-edge-with-windows-mixed-reality"></a><span data-ttu-id="49b4d-104">Utilisation de WebVR dans Microsoft Edge avec Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="49b4d-104">Using WebVR in Microsoft Edge with Windows Mixed Reality</span></span>

## <a name="creating-webvr-content-for-windows-mixed-reality-immersive-headsets"></a><span data-ttu-id="49b4d-105">Création de contenu WebVR pour les casques immersifs Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="49b4d-105">Creating WebVR content for Windows Mixed reality immersive headsets</span></span>

<span data-ttu-id="49b4d-106">WebVR 1,1 est disponible dans Microsoft Edge à partir de la mise à jour de Windows 10 automne Creators.</span><span class="sxs-lookup"><span data-stu-id="49b4d-106">WebVR 1.1 is available in Microsoft Edge beginning with the Windows 10 Fall Creators Update.</span></span> <span data-ttu-id="49b4d-107">Les développeurs peuvent désormais utiliser cette API pour créer des expériences de VR immersif sur le Web.</span><span class="sxs-lookup"><span data-stu-id="49b4d-107">Developers can now use this API to create immersive VR experiences on the web.</span></span>

<span data-ttu-id="49b4d-108">L’API WebVR fournit des données de HMD à la page qui peuvent être utilisées pour restituer une scène WebGL stéréo dans le HMD.</span><span class="sxs-lookup"><span data-stu-id="49b4d-108">The WebVR API provides HMD pose data to the page which can be used to render a stereo WebGL scene back to the HMD.</span></span> <span data-ttu-id="49b4d-109">Des détails sur la prise en charge des API sont disponibles sur la page d’état de la [plateforme Microsoft Edge](https://developer.microsoft.com/microsoft-edge/platform/status/webvr/).</span><span class="sxs-lookup"><span data-stu-id="49b4d-109">Details on API support is available on the [Microsoft Edge Platform Status page](https://developer.microsoft.com/microsoft-edge/platform/status/webvr/).</span></span> <span data-ttu-id="49b4d-110">La surface d’exposition de l’API WebVR est présente à tout moment dans Microsoft Edge.</span><span class="sxs-lookup"><span data-stu-id="49b4d-110">The WebVR API surface area is present at all times within Microsoft Edge.</span></span> <span data-ttu-id="49b4d-111">Toutefois, un appel à getVRDisplays () retourne un casque uniquement si un casque est branché ou si le simulateur a été mis sous tension.</span><span class="sxs-lookup"><span data-stu-id="49b4d-111">However, a call to getVRDisplays() will only return a headset if either a headset is plugged in or the simulator has been turned on.</span></span>

## <a name="viewing-webvr-content-in-windows-mixed-reality-immersive-headsets"></a><span data-ttu-id="49b4d-112">Affichage du contenu WebVR dans les casques immersifs Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="49b4d-112">Viewing WebVR content in Windows Mixed Reality immersive headsets</span></span>

<span data-ttu-id="49b4d-113">Vous trouverez des instructions pour accéder au contenu de WebVR dans votre casque immersif dans le [Guide du passionné](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/webvr).</span><span class="sxs-lookup"><span data-stu-id="49b4d-113">Instructions for accessing WebVR content in your immersive headset can be found in the [Enthusiast's Guide](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/webvr).</span></span>

## <a name="see-also"></a><span data-ttu-id="49b4d-114">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="49b4d-114">See Also</span></span>
* [<span data-ttu-id="49b4d-115">Informations WebVR</span><span class="sxs-lookup"><span data-stu-id="49b4d-115">WebVR information</span></span>](http://webvr.info)
* [<span data-ttu-id="49b4d-116">Spécification WebVR</span><span class="sxs-lookup"><span data-stu-id="49b4d-116">WebVR specification</span></span>](https://w3c.github.io/webvr/)
* <span data-ttu-id="49b4d-117">[API WebVR](https://msdn.microsoft.com/library/mt806281(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="49b4d-117">[WebVR API](https://msdn.microsoft.com/library/mt806281(v=vs.85).aspx)</span></span>
* <span data-ttu-id="49b4d-118">[API WebGL](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="49b4d-118">[WebGL API](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)</span></span>
* <span data-ttu-id="49b4d-119">[API du boîtier de manette](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) et les [extensions de boîtier](https://w3c.github.io/gamepad/extensions.html)</span><span class="sxs-lookup"><span data-stu-id="49b4d-119">[Gamepad API](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) and [Gamepad Extensions](https://w3c.github.io/gamepad/extensions.html)</span></span>
* [<span data-ttu-id="49b4d-120">Gestion du contexte perdu dans WebGL</span><span class="sxs-lookup"><span data-stu-id="49b4d-120">Handling Lost Context in WebGL</span></span>](https://www.khronos.org/webgl/wiki/HandlingContextLost)
* [<span data-ttu-id="49b4d-121">Pointerlock</span><span class="sxs-lookup"><span data-stu-id="49b4d-121">Pointerlock</span></span>](http://www.w3.org/TR/pointerlock/)
* [<span data-ttu-id="49b4d-122">glTF</span><span class="sxs-lookup"><span data-stu-id="49b4d-122">glTF</span></span>](https://www.khronos.org/gltf)
* [<span data-ttu-id="49b4d-123">Utilisation de Babylon. js pour activer WebVR</span><span class="sxs-lookup"><span data-stu-id="49b4d-123">Using Babylon.js to enable WebVR</span></span>](https://docs.microsoft.com/windows/uwp/get-started/adding-webvr-to-a-babylonjs-game)

