---
title: Utilisation de WebXR avec Windows Mixed Reality
description: Vue d’ensemble de l’utilisation et du développement pour WebXR dans Windows Mixed Reality
author: yonet
ms.author: ayyonet
ms.date: 04/10/2020
ms.topic: article
keywords: WebXR, WinMR, WebAR, WebVR, WindowsMixedReality, HoloLens, Windows Mixed Reality, Web VR, Web XR, Web Mr, Web AR, 360, 360 Video, 360 vidéos, 360 photo, 360 photos, 360 content, Internet immersif, immersiveweb, IW
ms.openlocfilehash: 01e6cd44e9879cd7fd9b11e178134eaf364cc53c
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81278440"
---
# <a name="webxr-overview"></a><span data-ttu-id="4936a-104">Présentation de WebXR</span><span class="sxs-lookup"><span data-stu-id="4936a-104">WebXR Overview</span></span>

## <a name="what-is-webxr"></a><span data-ttu-id="4936a-105">Qu’est-ce que WebXR</span><span class="sxs-lookup"><span data-stu-id="4936a-105">What is WebXR</span></span>

<span data-ttu-id="4936a-106">L' **API d’appareil WebXR** permet d’accéder à des appareils de réalité **virtuelle (VR)** et de **réalité augmentée (AR)** , notamment des **capteurs** et des **affichages montés en tête** sur le **Web**.</span><span class="sxs-lookup"><span data-stu-id="4936a-106">The **WebXR device API** is for accessing **virtual reality (VR)** and **augmented reality (AR)** devices, including **sensors** and **head-mounted displays** on the **Web**.</span></span> <span data-ttu-id="4936a-107">L’API d’appareil WebXR est actuellement disponible sur Microsoft Edge et Chrome version 79 et les versions ultérieures prennent en charge WebXR comme valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="4936a-107">WebXR device API is currently available on Microsoft Edge and Chrome version 79 and later versions supports WebXR as a default.</span></span> <span data-ttu-id="4936a-108">Vous pouvez vérifier l’état de prise en charge du navigateur le plus récent pour WebXR sur [caniuse.com](https://caniuse.com/#search=webxr).</span><span class="sxs-lookup"><span data-stu-id="4936a-108">You can check the latest browser support status for WebXR at [caniuse.com](https://caniuse.com/#search=webxr).</span></span>

<span data-ttu-id="4936a-109">Apprenez-en davantage sur [Windows Mixed Reality et le nouveau Microsoft Edge dans la](https://docs.microsoft.com/windows/mixed-reality/new-microsoft-edge#introducing-the-new-microsoft-edge)section [Nouveautés](https://docs.microsoft.com/windows/mixed-reality/mrtk-porting-guide) .</span><span class="sxs-lookup"><span data-stu-id="4936a-109">Learn more about the [Windows Mixed Reality and the new Microsoft Edge](https://docs.microsoft.com/windows/mixed-reality/new-microsoft-edge#introducing-the-new-microsoft-edge)in [What's new](https://docs.microsoft.com/windows/mixed-reality/mrtk-porting-guide) section.</span></span>

## <a name="viewing-webxr"></a><span data-ttu-id="4936a-110">Affichage de WebXR</span><span class="sxs-lookup"><span data-stu-id="4936a-110">Viewing WebXR</span></span>

<span data-ttu-id="4936a-111">Pour tester si votre navigateur prend en charge WebXR, vous pouvez accéder à des [exemples WebXR](https://immersive-web.github.io/webxr-samples/) dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="4936a-111">To test if your browser supports WebXR, you can navigate to [WebXR Samples](https://immersive-web.github.io/webxr-samples/) in your browser.</span></span>

## <a name="see-also"></a><span data-ttu-id="4936a-112">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4936a-112">See Also</span></span>

* [<span data-ttu-id="4936a-113">Spécification de l’API d’appareil WebXR</span><span class="sxs-lookup"><span data-stu-id="4936a-113">WebXR Device API specification</span></span>](https://immersive-web.github.io/webxr/)
* [<span data-ttu-id="4936a-114">Documentation de l’API d’appareil WebXR</span><span class="sxs-lookup"><span data-stu-id="4936a-114">WebXR Device API documentation</span></span>](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API)
* [<span data-ttu-id="4936a-115">Immersiveweb. dev</span><span class="sxs-lookup"><span data-stu-id="4936a-115">Immersiveweb.dev</span></span>](https://immersiveweb.dev/)
* [<span data-ttu-id="4936a-116">Exemples WebXR</span><span class="sxs-lookup"><span data-stu-id="4936a-116">WebXR Samples</span></span>](https://immersive-web.github.io/webxr-samples/)
* [<span data-ttu-id="4936a-117">Windows Mixed Reality et le nouveau Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="4936a-117">Windows Mixed Reality and the new Microsoft Edge</span></span>](https://docs.microsoft.com/windows/mixed-reality/new-microsoft-edge#introducing-the-new-microsoft-edge)
* [<span data-ttu-id="4936a-118">Github du W3C sur le Web immersif</span><span class="sxs-lookup"><span data-stu-id="4936a-118">Immersive Web W3C Github</span></span>](https://github.com/immersive-web)
* <span data-ttu-id="4936a-119">[API WebGL](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="4936a-119">[WebGL API](https://msdn.microsoft.com/library/bg182648(v=vs.85).aspx)</span></span>
* <span data-ttu-id="4936a-120">[API du boîtier de manette](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) et les [extensions de boîtier](https://w3c.github.io/gamepad/extensions.html)</span><span class="sxs-lookup"><span data-stu-id="4936a-120">[Gamepad API](https://msdn.microsoft.com/library/dn743630(v=vs.85).aspx) and [Gamepad Extensions](https://w3c.github.io/gamepad/extensions.html)</span></span>
* [<span data-ttu-id="4936a-121">Gestion du contexte perdu dans WebGL</span><span class="sxs-lookup"><span data-stu-id="4936a-121">Handling Lost Context in WebGL</span></span>](https://www.khronos.org/webgl/wiki/HandlingContextLost)
* [<span data-ttu-id="4936a-122">Pointerlock</span><span class="sxs-lookup"><span data-stu-id="4936a-122">Pointerlock</span></span>](https://www.w3.org/TR/pointerlock/)
* [<span data-ttu-id="4936a-123">glTF</span><span class="sxs-lookup"><span data-stu-id="4936a-123">glTF</span></span>](https://www.khronos.org/gltf)
* [<span data-ttu-id="4936a-124">Utilisation de Babylon. js pour créer des expériences WebXR</span><span class="sxs-lookup"><span data-stu-id="4936a-124">Using Babylon.js to create WebXR experiences</span></span>](https://doc.babylonjs.com/how_to/introduction_to_webxr)
* [<span data-ttu-id="4936a-125">Groupe de communauté Web immersif</span><span class="sxs-lookup"><span data-stu-id="4936a-125">Immersive web community group</span></span>](https://www.w3.org/community/immersive-web/)
