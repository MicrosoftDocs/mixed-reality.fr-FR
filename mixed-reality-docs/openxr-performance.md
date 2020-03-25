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
# <a name="openxr-performance"></a>Performances de OpenXR

Sur HoloLens 2, il existe plusieurs façons d’envoyer des données de composition par le biais de `xrEndFrame`, ce qui entraînera une baisse notable des performances.
Pour éviter de pénaliser les performances, [soumettez un `XrCompositionProjectionLayer`unique](openxr-best-practices.md#use-a-single-projection-layer) avec les caractéristiques suivantes :
* [Utiliser un tableau de textures utilise permutation](openxr-best-practices.md#render-with-texture-array-and-vprt)
* [Utiliser le format utilise permutation de couleurs primaires](openxr-best-practices.md#select-a-swapchain-format)
* [Utiliser les dimensions de la vue recommandée](openxr-best-practices.md#render-with-recommended-rendering-parameters-and-frame-timing)
* Ne pas définir l’indicateur `XR_COMPOSITION_LAYER_UNPREMULTIPLIED_ALPHA_BIT`
* Définissez le `minDepth` `XrCompositionLayerDepthInfoKHR` sur 0.0 f et `maxDepth` sur 1.0 f

Des considérations supplémentaires améliorent les performances :
* [Utiliser le format de profondeur 16 bits](openxr-best-practices.md#choose-a-reasonable-depth-range)
* [Effectuer des appels de dessin instanciés](openxr-best-practices.md#render-with-texture-array-and-vprt)
