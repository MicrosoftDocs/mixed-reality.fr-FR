---
title: Meilleures pratiques relatives à OpenXR
description: Découvrez les meilleures pratiques en matière de qualité, de stabilité et de performances visuelles pour vos applications OpenXR.
author: thetuvix
ms.author: alexturn
ms.date: 2/28/2020
ms.topic: article
keywords: OpenXR, Khronos, BasicXRApp, DirectX, native, application native, moteur personnalisé, intergiciel, meilleures pratiques, performances, qualité, stabilité
ms.openlocfilehash: c0ddbd0604760ccae34d347e93b918be4aead269
ms.sourcegitcommit: 536fd45b48a70bbeca1454cef517ae007225e533
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80362015"
---
# <a name="openxr-app-best-practices"></a>Meilleures pratiques pour les applications OpenXR

Vous pouvez voir un exemple des meilleures pratiques ci-dessous dans le fichier OpenXRProgram. cpp de <a href="https://github.com/microsoft/OpenXR-MixedReality/tree/master/samples/BasicXrApp" target="_blank">BasicXrApp</a>. La fonction Run () au début capture un flot de code d’application OpenXR typique de l’initialisation à l’événement et à la boucle de rendu.

## <a name="best-practices-for-visual-quality-and-stability"></a>Meilleures pratiques en matière de qualité et de stabilité visuelles

Les meilleures pratiques décrites dans cette section expliquent comment obtenir la meilleure qualité visuelle et la meilleure stabilité dans n’importe quelle application OpenXR.

Pour obtenir d’autres recommandations relatives aux performances propres à HoloLens 2, consultez la section [meilleures pratiques en matière de performances sur hololens 2](#best-practices-for-performance-on-hololens-2) ci-dessous.

### <a name="gamma-correct-rendering"></a>Gamma-rendu correct

Vous devez veiller à ce que le pipeline de rendu soit correct pour la valeur gamma. Lors du rendu sur un utilise permutation, le format de la vue de cible de rendu doit correspondre au format utilise permutation (par exemple, DXGI_FORMAT_B8G8R8A8_UNORM_SRGB pour le format utilise permutation et la vue Render-cible).
L’exception est si le pipeline de rendu de l’application effectue une conversion sRVB manuelle dans le code du nuanceur. dans ce cas, l’application doit demander un format utilise permutation sRVB, mais utiliser le format linéaire pour la vue de la cible de rendu (par exemple, DXGI_FORMAT_B8G8R8A8_UNORM_SRGB de demande comme format utilise permutation mais utilisez DXGI_FORMAT_B8G8R8A8_UNORM comme affichage de la cible de rendu) pour empêcher le contenu d’être corrigé par double gamma.

### <a name="submit-depth-buffer-for-projection-layers"></a>Envoyer le tampon de profondeur pour les couches de projection

Utilisez toujours `XR_KHR_composition_layer_depth` extension et soumettez la mémoire tampon de profondeur avec la couche de projection lors de la soumission d’une image à `xrEndFrame`.
Cela améliore la stabilité de l’hologramme en activant la reprojection de la profondeur matérielle sur HoloLens 2.

### <a name="choose-a-reasonable-depth-range"></a>Choisir une plage de profondeur raisonnable

Privilégiez une plage de profondeur plus étroite pour étendre le contenu virtuel afin d’aider à la stabilité de l’hologramme sur HoloLens.
Par exemple, l’exemple OpenXrProgram. cpp utilise 0,1 à 20 mètres.
Utilisez [inversé-Z](https://developer.nvidia.com/content/depth-precision-visualized) pour une résolution de profondeur plus uniforme.
Notez que, sur HoloLens 2, l’utilisation du format de `DXGI_FORMAT_D16_UNORM` par défaut permet d’obtenir un meilleur taux de trames et de meilleures performances, bien que les mémoires tampons de profondeur de 16 bits offrent une résolution moins profonde que les mémoires tampons de profondeur 24 bits.
Par conséquent, le fait de suivre ces meilleures pratiques pour tirer le meilleur parti de la résolution de profondeur devient plus important.

### <a name="prepare-for-different-environment-blend-modes"></a>Préparer les différents modes de fusion de l’environnement

Si votre application s’exécute également sur des casques immersifs qui bloquent complètement le monde, veillez à énumérer les modes de mélange d’environnement pris en charge à l’aide de `xrEnumerateEnvironmentBlendModes` API et à préparer votre contenu de rendu en conséquence.
Par exemple, pour un système avec `XR_ENVIRONMENT_BLEND_MODE_ADDITIVE` tel que le HoloLens, l’application doit utiliser transparent comme couleur claire, tandis que pour un système avec `XR_ENVIRONMENT_BLEND_MODE_OPAQUE`, l’application doit afficher une couleur opaque ou une salle virtuelle en arrière-plan.

### <a name="choose-unbounded-reference-space-as-applications-root-space"></a>Choisir l’espace de référence illimité comme espace racine de l’application

En règle générale, les applications établissent un espace de coordonnées universel pour connecter des vues, des actions et des hologrammes.
Utilisez `XR_REFERENCE_SPACE_TYPE_UNBOUNDED_MSFT` lorsque l’extension est prise en charge pour établir un système de coordonnées à l' [échelle du monde](coordinate-systems.md#building-a-world-scale-experience), ce qui permet à votre application d’éviter la dérive d’hologramme indésirable lorsque l’utilisateur se déplace jusqu’à présent (par exemple, 5 mètres) à partir de l’emplacement où l’application démarre.
Utilisez `XR_REFERENCE_SPACE_TYPE_LOCAL` comme secours si l’extension de l’espace non limité n’existe pas.

### <a name="associate-hologram-with-spatial-anchor"></a>Associer l’hologramme avec l’ancrage spatial

Lors de l’utilisation d’un espace de référence non lié, les hologrammes que vous placez directement dans cet espace de référence [peuvent dériver lorsque l’utilisateur parcourt des salles distantes, puis revient](coordinate-systems.md#building-a-world-scale-experience).
Pour les utilisateurs d’hologrammes placés à un emplacement discret dans le monde, [créez une ancre spatiale](spatial-anchors.md#best-practices) à l’aide de la fonction d’extension `xrCreateSpatialAnchorSpaceMSFT` et positionnez l’hologramme à son origine.
Cela permet de maintenir la stabilité de l’hologramme indépendamment dans le temps.

### <a name="support-mixed-reality-capture"></a>Prendre en charge la capture de réalité mixte

Bien que l’affichage principal de HoloLens 2 utilise la fusion d’environnement additive, lorsque l’utilisateur initie une [capture de réalité mixte](mixed-reality-capture-for-developers.md), le contenu de rendu de l’application est mélangé à l’alpha avec le flux vidéo de l’environnement.
Pour obtenir la meilleure qualité visuelle dans les vidéos de capture de réalité mixte, il est préférable de définir le `XR_COMPOSITION_LAYER_BLEND_TEXTURE_SOURCE_ALPHA_BIT` dans le `layerFlags`de la couche de projection.

## <a name="best-practices-for-performance-on-hololens-2"></a>Meilleures pratiques en matière de performances sur HoloLens 2

En tant qu’appareil mobile avec prise en charge de la reprojection matérielle, HoloLens 2 a des exigences plus strictes pour obtenir des performances optimales.  Il existe plusieurs façons d’envoyer des données de composition par le biais de `xrEndFrame`, ce qui entraînera une baisse notable des performances.

### <a name="select-a-swapchain-format"></a>Sélectionner un format de utilise permutation

Énumérez toujours les formats de pixel pris en charge à l’aide de `xrEnumerateSwapchainFormats`, puis choisissez le premier format de pixel de couleur et de profondeur du runtime pris en charge par l’application, car c’est ce que le runtime préfère pour des performances optimales. Notez que sur HoloLens 2, `DXGI_FORMAT_B8G8R8A8_UNORM_SRGB` et `DXGI_FORMAT_D16_UNORM` est généralement le premier choix pour obtenir de meilleures performances de rendu. Cette préférence peut être différente sur les casques de VR qui s’exécutent sur un PC de bureau, où les mémoires tampons de profondeur de 24 bits ont moins d’impact sur les performances.
  
**Avertissement de performance :** L’utilisation d’un format autre que le format de couleur utilise permutation principal entraîne une baisse significative des performances du Runtime.

### <a name="render-with-recommended-rendering-parameters-and-frame-timing"></a>Rendu avec les paramètres de rendu recommandés et le minutage des frames

Rendez toujours le rendu avec la largeur/hauteur de la configuration de l’affichage recommandé (`recommendedImageRectWidth` et `recommendedImageRectHeight` à partir de `XrViewConfigurationView`) et utilisez toujours `xrLocateViews` API pour interroger la vue recommandée pose, le point d’angle et d’autres paramètres de rendu avant le rendu.
Utilisez toujours le `XrFrameEndInfo.predictedDisplayTime` à partir du dernier appel de `xrWaitFrame` lors de l’interrogation des poses et des vues.
Cela permet à HoloLens d’ajuster le rendu et d’optimiser la qualité visuelle pour la personne qui porte le HoloLens.

### <a name="use-a-single-projection-layer"></a>Utiliser une seule couche de projection

HoloLens 2 offre une puissance GPU limitée pour les applications afin de restituer le contenu et un compositeur matériel optimisé pour une couche de projection unique.
En utilisant toujours une seule couche de projection, vous pouvez améliorer la fréquence de l’application, la stabilité de l’hologramme et la qualité visuelle.  
  
**Avertissement de performance :** L’envoi de tout sauf une seule couche de protection entraînera un traitement postérieur au moment de l’exécution, ce qui se traduit par une baisse significative des performances.

### <a name="render-with-texture-array-and-vprt"></a>Rendu avec un tableau de texture et VPRT

Créez un `xrSwapchain` pour les yeux gauche et droit à l’aide de `arraySize=2` pour utilise permutation de couleur, et un pour la profondeur.
Restituez l’œil gauche dans le segment 0 et l’œil droit dans le segment 1.
Utilisez un nuanceur avec VPRT et des appels de dessin instanciés pour le rendu stéréoscopique afin de réduire la charge GPU.
Cela permet également à l’optimisation du runtime d’obtenir des performances optimales sur HoloLens 2.
Les alternatives à l’utilisation d’un tableau de textures, telles que le rendu à double larges ou un utilise permutation séparé par œil, entraînent un traitement postérieur au moment de l’exécution, ce qui se traduit par une baisse significative des performances.

### <a name="avoid-quad-layers"></a>Éviter les quatre couches

Au lieu d’envoyer des couches Quad en tant que couches de composition avec `XrCompositionLayerQuad`, affichez le contenu Quad directement dans le utilise permutation de projection.

**Avertissement de performance :** Le fait de fournir des couches supplémentaires au-delà d’une seule couche de projection, comme les couches Quad, entraîne un traitement postérieur au moment de l’exécution, ce qui se traduit par une baisse significative des performances.