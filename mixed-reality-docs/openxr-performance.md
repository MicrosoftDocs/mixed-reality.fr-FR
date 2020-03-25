---
title: Performances de OpenXR
description: Déboguez les performances du GPU pour vos applications OpenXR.
author: thetuvix
ms.author: alexturn
ms.date: 2/28/2020
ms.topic: article
keywords: OpenXR, Khronos, BasicXRApp, DirectX, native, application native, moteur personnalisé, intergiciel, performances, optimisation, débogage GPU, RenderDoc, PIX
ms.openlocfilehash: 717dc2d534773bd28f5ad2d5c3720bf4177a1480
ms.sourcegitcommit: 9de2cb11321e6517db69e8c93459a205900a2174
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80163343"
---
# <a name="openxr-performance"></a><span data-ttu-id="69b83-104">Performances de OpenXR</span><span class="sxs-lookup"><span data-stu-id="69b83-104">OpenXR performance</span></span>

<span data-ttu-id="69b83-105">Sur HoloLens 2, il existe plusieurs façons d’envoyer des données de composition par le biais de `xrEndFrame`, ce qui entraînera une baisse notable des performances.</span><span class="sxs-lookup"><span data-stu-id="69b83-105">On HoloLens 2, there are a number of ways to submit composition data through `xrEndFrame` which will result in post-processing that will have a noticeable performance penalty.</span></span>
<span data-ttu-id="69b83-106">Pour éviter de pénaliser les performances, [soumettez un `XrCompositionProjectionLayer`unique](openxr-best-practices.md#use-a-single-projection-layer) avec les caractéristiques suivantes :</span><span class="sxs-lookup"><span data-stu-id="69b83-106">To avoid performance penalities, [submit a single `XrCompositionProjectionLayer`](openxr-best-practices.md#use-a-single-projection-layer) with the following characteristics:</span></span>
* [<span data-ttu-id="69b83-107">Utiliser un tableau de textures utilise permutation</span><span class="sxs-lookup"><span data-stu-id="69b83-107">Use a texture array swapchain</span></span>](openxr-best-practices.md#render-with-texture-array-and-vprt)
* [<span data-ttu-id="69b83-108">Utiliser le format utilise permutation de couleurs primaires</span><span class="sxs-lookup"><span data-stu-id="69b83-108">Use the primary color swapchain format</span></span>](openxr-best-practices.md#select-a-swapchain-format)
* [<span data-ttu-id="69b83-109">Utiliser les dimensions de la vue recommandée</span><span class="sxs-lookup"><span data-stu-id="69b83-109">Use the recommended view dimensions</span></span>](openxr-best-practices.md#render-with-recommended-rendering-parameters-and-frame-timing)
* <span data-ttu-id="69b83-110">Ne pas définir l’indicateur `XR_COMPOSITION_LAYER_UNPREMULTIPLIED_ALPHA_BIT`</span><span class="sxs-lookup"><span data-stu-id="69b83-110">Do not set the `XR_COMPOSITION_LAYER_UNPREMULTIPLIED_ALPHA_BIT` flag</span></span>
* <span data-ttu-id="69b83-111">Définissez le `minDepth` `XrCompositionLayerDepthInfoKHR` sur 0.0 f et `maxDepth` sur 1.0 f</span><span class="sxs-lookup"><span data-stu-id="69b83-111">Set the `XrCompositionLayerDepthInfoKHR` `minDepth` to 0.0f and `maxDepth` to 1.0f</span></span>

<span data-ttu-id="69b83-112">Des considérations supplémentaires améliorent les performances :</span><span class="sxs-lookup"><span data-stu-id="69b83-112">Additional considerations will result in better performance:</span></span>
* [<span data-ttu-id="69b83-113">Utiliser le format de profondeur 16 bits</span><span class="sxs-lookup"><span data-stu-id="69b83-113">Use the 16-bit depth format</span></span>](openxr-best-practices.md#choose-a-reasonable-depth-range)
* [<span data-ttu-id="69b83-114">Effectuer des appels de dessin instanciés</span><span class="sxs-lookup"><span data-stu-id="69b83-114">Make instanced draw calls</span></span>](openxr-best-practices.md#render-with-texture-array-and-vprt)
