---
title: OpenXR
description: Générez un moteur à l’aide de la norme de l’API OpenXR portable et déployez-le sur des casques Windows mixtes et des casques HoloLens 2.
author: thetuvix
ms.author: alexturn
ms.date: 7/29/2019
ms.topic: article
keywords: OpenXR, Khronos, BasicXRApp, réalité mixte OpenXR portail des développeurs, DirectX, natif, moteur personnalisé d’application native, intergiciel
ms.openlocfilehash: 67d2ab42a40aa04eb9dcd6881a4392a81c0f3b8f
ms.sourcegitcommit: b6b76275fad90df6d9645dd2bc074b7b2168c7c8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/11/2019
ms.locfileid: "73914391"
---
# <a name="openxr"></a>OpenXR

OpenXR est une norme d’API libre de redevance de <a href="https://www.khronos.org/" target="_blank">Khronos</a> qui fournit aux moteurs un accès natif à un large éventail d’appareils de nombreux fournisseurs qui s’étendent sur le spectre de la [réalité mixte](mixed-reality.md).

Vous pouvez développer à l’aide de OpenXR sur un casque de l’architecture HoloLens 2 ou Windows Mixed Reality sur le bureau.  Si vous n’avez pas accès à un casque, vous pouvez utiliser l’émulateur HoloLens 2 ou Windows Mixed Reality Simulator à la place.

## <a name="why-openxr"></a>Pourquoi OpenXR ?

Avec OpenXR, vous pouvez créer des moteurs qui ciblent les deux appareils holographiques (tels que HoloLens 2) qui placent le contenu numérique dans le monde réel comme s’il existait vraiment, ainsi que des appareils immersifs (tels que des casques Windows mixtes de réalité pour ordinateurs de bureau) qui masquent les et remplacez-le par un environnement numérique.  OpenXR vous permet d’écrire du code une fois qui est ensuite portable sur une large gamme de plateformes matérielles.

L’API OpenXR utilise un chargeur qui connecte votre application directement à la prise en charge native de la plateforme de votre casque.  Cela offre aux utilisateurs finaux des performances maximales et une latence minimale, qu’ils utilisent un casque Windows Mixed Reality ou tout autre casque.

## <a name="what-is-openxr"></a>Qu’est-ce que OpenXR ?

L’API Core OpenXR 1,0 fournit les fonctionnalités de base dont vous aurez besoin pour créer un moteur qui peut cibler des appareils holographiques comme HoloLens 2 et des appareils immersifs tels que les casques de la réalité mixte Windows :
* Systèmes et sessions
* Espaces de référence (vue, local, intermédiaire)
* Afficher les configurations (mono, stéréo)
* Chaînes d’échange + minutage des frames
* Couches de composition
* Entrée et haptique
* API Graphics + intégration de plateforme

Pour en savoir plus sur l’API OpenXR, consultez la <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html" target="_blank">spécification</a>OpenXR 1,0, informations de <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/man/html/openxr.html" target="_blank">référence</a> sur les API et <a href="https://www.khronos.org/files/openxr-10-reference-guide.pdf" target="_blank">Guide de référence rapide</a>.  Pour plus d’informations, consultez la <a href="https://www.khronos.org/openxr/" target="_blank">page Khronos OpenXR</a>.

Pour cibler l’ensemble complet des fonctionnalités de HoloLens 2, vous utiliserez également des extensions OpenXR spécifiques à un fournisseur et à un fournisseur qui activent des fonctionnalités supplémentaires au-delà du OpenXR 1,0 cœurs, telles que le suivi articulé, le suivi oculaire, le mappage spatial et les ancrages spatiaux.  Pour plus d’informations sur les extensions arrivant plus tard cette année, consultez la section de la feuille de [route](openxr.md#roadmap) ci-dessous.

Notez que OpenXR n’est pas lui-même un moteur de réalité mixte.  Au lieu de cela, OpenXR permet aux moteurs comme Unity et Unreal d’écrire du code portable une seule fois qui peut ensuite accéder aux fonctionnalités natives de la plateforme de l’appareil holographique ou immersif de l’utilisateur, quel que soit le fournisseur qui a créé cette plateforme.

## <a name="getting-started-with-openxr-for-hololens-2"></a>Prise en main de OpenXR pour HoloLens 2

Pour commencer à développer des applications OpenXR pour HoloLens 2 :

1. Configurez un HoloLens 2 ou suivez les instructions pour [installer l’émulateur hololens 2](using-the-hololens-emulator.md).
1. Lancez l’application du Windows Store à partir de l’appareil ou de l’émulateur et assurez-vous que toutes les applications sont mises à jour.  Cela permet de s’assurer que le runtime OpenXR sur votre HoloLens est mis à jour vers OpenXR 1,0.  Si vous utilisez l’émulateur, vous souhaiterez consulter les [instructions d’entrée](using-the-hololens-emulator.md#basic-emulator-input) de l’émulateur pour vous aider à utiliser l’application du Windows Store dans l’émulateur.

## <a name="getting-started-with-openxr-for-windows-mixed-reality-headsets"></a>Prise en main de OpenXR pour les casques Windows Mixed Reality

Pour commencer à développer des applications OpenXR pour des casques Windows mixtes immersifs :

1. Assurez-vous que vous exécutez la mise à jour Windows 10 2019 (1903), qui est la configuration minimale requise pour que les utilisateurs finaux Windows Mixed realisation exécutent des applications OpenXR.  Si vous utilisez une version antérieure de Windows 10, vous pouvez effectuer la mise à niveau vers la mise à jour 2019 de mai à l’aide de l' <a href="https://www.microsoft.com//software-download/windows10" target="_blank">Assistant Mise à jour de Windows 10</a>.  Si vous n’êtes pas en mesure de mettre à jour votre PC, il est également possible de [développer votre application OpenXR à l’aide de la mise à jour 2018 (1809) de Windows 10 octobre](openxr.md#developing-on-windows-10-october-2018-update), bien que vous puissiez constater une baisse des performances ou d’autres problèmes.
2. Configurez un casque Windows Mixed Reality ou suivez les instructions pour [activer le simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md).  Après la configuration de Windows Mixed Reality, le portail de réalité mixte installe automatiquement le runtime OpenXR Windows Mixed Reality.  Le Microsoft Store garde alors le runtime à jour.
3. Rendez le runtime OpenXR Windows Mixed Reality actif en lançant le portail de réalité mixte à partir du menu Démarrer, en cliquant sur le bouton... dans l’angle inférieur gauche, puis en sélectionnant « Configurer OpenXR ».<br>
![la configuration de OpenXR dans le portail de réalité mixte](images/mixed-reality-portal-set-up-openxr.png)

Si vous devez faire en sorte que le runtime OpenXR Windows Mixed Reality soit à nouveau actif, répétez l’étape 3.

> [!NOTE]
> Le runtime Windows Mixed Reality OpenXR sera bientôt configuré automatiquement pour tous les utilisateurs finaux Windows Mixed Reality.

## <a name="getting-the-mixed-reality-openxr-developer-portal"></a>Obtention du portail des développeurs OpenXR de la réalité mixte

Pour tester le runtime OpenXR Windows Mixed Reality, vous pouvez installer l' <a href="https://www.microsoft.com/store/productId/9n5cvvl23qbt" target="_blank">application [Mixed Reality OpenXR Developer Portal</a>.  Cette application fournit une scène de démonstration qui exerce diverses fonctionnalités de OpenXR, ainsi qu’une page d’État du système qui fournit des informations clés sur le runtime actif et le casque actuel.

![Application du portail des développeurs OpenXR de la réalité mixte](images/mixed-reality-openxr-developer-portal.png)

## <a name="building-a-sample-openxr-app"></a>Création d’un exemple d’application OpenXR

Le projet <a href="https://github.com/Microsoft/OpenXR-SDK-VisualStudio/tree/master/samples/BasicXrApp" target="_blank">BasicXrApp</a> illustre un exemple OpenXR simple avec deux fichiers projet Visual Studio, un pour une application de bureau Win32 et un pour une application UWP 2 UWP.  Étant donné que la solution contient un projet UWP HoloLens, vous avez besoin de la [charge de travail de développement plateforme Windows universelle](install-the-tools.md#installation-checklist) installée dans Visual Studio pour l’ouvrir entièrement.

Notez que, bien que les fichiers de projet Win32 et UWP soient distincts en raison des différences d’empaquetage et de déploiement, le code de l’application à l’intérieur de chaque projet est de 100% le même !

## <a name="openxr-app-best-practices-for-hololens-2"></a>Meilleures pratiques pour les applications OpenXR pour HoloLens 2

Vous pouvez voir un exemple des meilleures pratiques ci-dessous dans le fichier [OpenXRProgram. cpp](https://github.com/microsoft/OpenXR-SDK-VisualStudio/blob/master/samples/BasicXrApp/OpenXrProgram.cpp) de BasicXrApp. La fonction Run () au début capture un flot de code d’application OpenXR typique de l’initialisation à l’événement et à la boucle de rendu.

### <a name="select-a-pixel-format"></a>Sélectionner un format de pixel

Énumérez toujours les formats de pixel pris en charge à l’aide de `xrEnumerateSwapchainFormats`, puis choisissez le premier format de pixel de couleur et de profondeur du runtime pris en charge par l’application, car c’est ce que le runtime préfère. Notez que sur HoloLens 2, `DXGI_FORMAT_B8G8R8A8_UNORM_SRGB` et `DXGI_FORMAT_D16_UNORM` est généralement le premier choix pour obtenir de meilleures performances de rendu. Cette préférence peut être différente sur les casques VR s’exécutant sur un PC de bureau.  
  
**Avertissement de performance :** L’utilisation d’un format autre que le format de couleur utilise permutation principal entraîne une baisse significative des performances du Runtime.

### <a name="gamma-correct-rendering"></a>Gamma-rendu correct

Bien que cela s’applique à tous les runtimes OpenXR, il est nécessaire de veiller à ce que le pipeline de rendu soit correct pour la gamma. Lors du rendu sur un utilise permutation, le format de la vue de cible de rendu doit correspondre au format utilise permutation (par exemple, DXGI_FORMAT_B8G8R8A8_UNORM_SRGB pour le format utilise permutation et la vue Render-cible).
L’exception est si le pipeline de rendu de l’application effectue une conversion sRVB manuelle dans le code du nuanceur. dans ce cas, l’application doit demander un format utilise permutation sRVB, mais utiliser le format linéaire pour la vue de la cible de rendu (par exemple, DXGI_FORMAT_B8G8R8A8_UNORM_SRGB de demande comme format utilise permutation mais utilisez DXGI_FORMAT_B8G8R8A8_UNORM comme affichage de la cible de rendu) pour empêcher le contenu d’être corrigé par double gamma.

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

### <a name="render-with-recommended-rendering-parameters-and-frame-timing"></a>Rendu avec les paramètres de rendu recommandés et le minutage des frames

Rendez toujours le rendu avec la largeur/hauteur de la configuration de l’affichage recommandé (`recommendedImageRectWidth` et `recommendedImageRectHeight` à partir de `XrViewConfigurationView`) et utilisez toujours `xrLocateViews` API pour interroger la vue recommandée pose, le point d’angle et d’autres paramètres de rendu avant le rendu.
Utilisez toujours le `XrFrameEndInfo.predictedDisplayTime` à partir du dernier appel de `xrWaitFrame` lors de l’interrogation des poses et des vues.
Cela permet à HoloLens d’ajuster le rendu et d’optimiser la qualité visuelle pour la personne qui porte le HoloLens.

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

**Avertissement de performance :** L’omission de l’indicateur `XR_COMPOSITION_LAYER_BLEND_TEXTURE_SOURCE_ALPHA_BIT` sur la couche de projection unique entraînera un traitement postérieur au moment de l’exécution, ce qui se traduit par une baisse significative des performances.

### <a name="avoid-quad-layers"></a>Éviter les quatre couches

Au lieu d’envoyer des couches Quad en tant que couches de composition avec `XrCompositionLayerQuad`, affichez le contenu Quad directement dans le utilise permutation de projection.

**Avertissement de performance :** Le fait de fournir des couches supplémentaires au-delà d’une seule couche de projection, comme les couches Quad, entraîne un traitement postérieur au moment de l’exécution, ce qui se traduit par une baisse significative des performances.

## <a name="openxr-app-performance-on-hololens-2"></a>Performances des applications OpenXR sur HoloLens 2

Sur HoloLens 2, il existe plusieurs façons d’envoyer des données de composition par le biais de `xrEndFrame`, ce qui entraînera une baisse notable des performances.
Pour éviter de pénaliser les performances, [soumettez un `XrCompositionProjectionLayer`unique](#use-a-single-projection-layer) avec les caractéristiques suivantes :
* [Utiliser un tableau de textures utilise permutation](#render-with-texture-array-and-vprt)
* [Utiliser le format utilise permutation de couleurs primaires](#select-a-pixel-format)
* [Définir l’indicateur de fusion de texture-source-alpha](#support-mixed-reality-capture)
* [Utiliser les dimensions de la vue recommandée](#render-with-recommended-rendering-parameters-and-frame-timing)
* Ne pas définir l’indicateur `XR_COMPOSITION_LAYER_UNPREMULTIPLIED_ALPHA_BIT`
* Définissez le `minDepth` `XrCompositionLayerDepthInfoKHR` sur 0.0 f et `maxDepth` sur 1.0 f

Des considérations supplémentaires améliorent les performances :
* [Utiliser le format de profondeur 16 bits](#choose-a-reasonable-depth-range)
* [Effectuer des appels de dessin instanciés](#render-with-texture-array-and-vprt)

## <a name="roadmap"></a>Feuille de route

La spécification OpenXR définit un mécanisme d’extension qui permet aux implémenteurs de runtime d’exposer des fonctionnalités supplémentaires au-delà des [fonctionnalités](openxr.md#what-is-openxr) de base définies dans la <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html" target="_blank">spécification 1,0 de base OpenXR</a>.

Il existe trois types d’extensions OpenXR :
* **Extensions de fournisseur (par exemple, MSFT) :** Active l’innovation par fournisseur dans les fonctionnalités matérielles ou logicielles.  N’importe quel fournisseur de Runtime peut introduire et livrer une extension de fournisseur à tout moment.
* **Extensions ext :** Extensions inter-fournisseurs que plusieurs entreprises définissent et implémentent.  Les groupes de sociétés intéressées peuvent introduire des extensions EXT à tout moment.
* **Extensions KHR :** Extensions Khronos officielles ratifiées dans le cadre d’une version de base spec.  Les extensions KHR sont couvertes par la même licence que la spécification principale elle-même.

À la fin de l’année, le runtime OpenXR Windows Mixed Reality prendra en charge un ensemble d’extensions MSFT et EXT qui apportent l’ensemble complet des fonctionnalités HoloLens 2 aux applications OpenXR :
* [Espace de référence non lié (expériences à l’échelle mondiale)](coordinate-systems.md#building-a-world-scale-experience)
* [Ancres spatiales + stockage](spatial-anchors.md)
* [Articulation manuelle + maille](hands-and-tools.md)
* [Suivre du regard](eye-tracking.md)
* [Configurations d’affichage secondaire (capture de réalité mixte)](mixed-reality-capture-for-developers.md#render-from-the-pv-camera-opt-in)
* [Compréhension des scènes](scene-understanding.md)
* Interopérabilité avec les API SDK Windows

Bien que certaines de ces extensions puissent démarrer en tant qu’extensions MSFT spécifiques au fournisseur, Microsoft et d’autres fournisseurs de Runtime OpenXR travaillent ensemble pour concevoir des extensions EXT ou KHR inter-fournisseurs pour la plupart de ces fonctionnalités.  Cela permet au code que vous écrivez pour que ces fonctionnalités soient portables entre les fournisseurs de Runtime, tout comme avec la spécification principale.

## <a name="troubleshooting"></a>Dépannage

Voici quelques conseils de dépannage pour le runtime OpenXR Windows Mixed Reality.  Si vous avez d’autres questions sur la <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html" target="_blank">spécification OpenXR 1,0</a>, visitez les <a href="https://community.khronos.org/c/openxr" target="_blank">Forums Khronos OpenXR</a> ou la <a href="https://khr.io/slack" target="_blank">marge #openxr canal</a>.

### <a name="developing-on-windows-10-october-2018-update"></a>Mise à jour du développement sur Windows 10 octobre 2018

Si vous n’êtes pas en mesure de [mettre à niveau votre PC de développement vers la mise à jour 2019 de mai](https://www.microsoft.com//software-download/windows10), vous pouvez configurer votre PC Windows 10 octobre 2018 update (1809) pour le développement en suivant une étape supplémentaire :

1. Suivez les étapes ci-dessus pour commencer à utiliser OpenXR sur votre ordinateur de bureau.
1. Pour définir le runtime Windows Mixed Reality OpenXR comme le runtime OpenXR actif de votre système, installez le [Pack de compatibilité des développeurs Windows Mixed Reality OpenXR](https://aka.ms/openxr-compat).

> [!NOTE]
> Bien que la mise à jour 2018 (1809) de Windows 10 octobre puisse être utilisée lors du développement de vos applications OpenXR, la mise à jour Windows 10 mai 2019 (1903) est la configuration minimale requise pour que les utilisateurs finaux utilisent OpenXR avec Windows Mixed Reality.  Vous pouvez constater une baisse des performances ou d’autres problèmes lors de l’exécution de votre application OpenXR sur la mise à jour d’octobre 2018.  Il est fortement recommandé de mettre à niveau votre PC de développement vers la mise à jour 2019 de Windows 10 (1903).

### <a name="openxr-app-not-starting-windows-mixed-reality"></a>Application OpenXR ne démarrant pas Windows Mixed Reality

Si votre application OpenXR ne démarre pas Windows Mixed Reality quand vous l’exécutez, le runtime Windows Mixed Reality OpenXR peut ne pas être défini comme le runtime actif.  Veillez à suivre les instructions ci-dessus pour bien [Démarrer avec OpenXR pour les casques Windows Mixed Reality](#getting-started-with-openxr-for-windows-mixed-reality-headsets) pour rendre le runtime actif.

Vous pouvez également exécuter le [portail des développeurs OpenXR de la réalité mixte](#getting-the-mixed-reality-openxr-developer-portal) pour obtenir une aide supplémentaire sur l’état du runtime Windows Mixed Reality OpenXR sur votre système.

### <a name="mixed-reality-portal-not-showing-set-up-openxr-menu-item"></a>Le portail de réalité mixte n’indique pas l’élément de menu « configurer OpenXR »

Assurez-vous que vous exécutez au moins la mise à jour 2018 de Windows 10 octobre (1809).  Si vous utilisez une version antérieure de Windows 10, vous pouvez effectuer la mise à niveau vers la mise à jour 2019 (1903) à l’aide de l' [Assistant Mise à jour de Windows 10](https://www.microsoft.com//software-download/windows10).

L’élément de menu « configurer OpenXR » peut ne pas être disponible si vous disposez d’une version antérieure de l’application portail de réalité mixte.  Recherchez une [mise à jour de l’application portail de réalité mixte](https://www.microsoft.com/p/mixed-reality-portal/9ng1h8b3zc7m) pour vous assurer que vous disposez de la dernière version.

Notez que l’élément de menu « configurer OpenXR » n’apparaît pas si le runtime Windows Mixed Reality OpenXR est déjà installé et actif.  Vous pouvez installer le [portail des développeurs OpenXR de la réalité mixte](#getting-the-mixed-reality-openxr-developer-portal) pour déterminer l’état actuel du runtime OpenXR sur votre système.

## <a name="see-also"></a>Articles associés

* <a href="https://www.khronos.org/openxr/" target="_blank">Plus d’informations sur OpenXR</a>
* <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html" target="_blank">Spécification OpenXR 1,0</a>
* <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/man/html/openxr.html" target="_blank">Informations de référence sur l’API OpenXR 1,0</a>
* <a href="https://www.khronos.org/files/openxr-10-reference-guide.pdf" target="_blank">Guide de référence rapide de OpenXR 1,0</a>
