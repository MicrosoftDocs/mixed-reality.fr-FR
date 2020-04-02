---
title: OpenXR
description: Générez un moteur à l’aide de la norme de l’API OpenXR portable et déployez-le sur des casques Windows mixtes et des casques HoloLens 2.
author: thetuvix
ms.author: alexturn
ms.date: 7/29/2019
ms.topic: article
keywords: OpenXR, Khronos, BasicXRApp, DirectX, native, application native, moteur personnalisé, intergiciel
ms.openlocfilehash: 04b2404889dc74f191543466beb7ae1e516d0d42
ms.sourcegitcommit: 46bd1a56d272a5880f410751fa8429d65d816431
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/02/2020
ms.locfileid: "80549375"
---
# <a name="openxr"></a>OpenXR

OpenXR est une norme d’API libre de redevance de <a href="https://www.khronos.org/" target="_blank">Khronos</a> qui fournit aux moteurs un accès natif à un large éventail d’appareils de nombreux fournisseurs qui s’étendent sur le spectre de la [réalité mixte](mixed-reality.md).

Vous pouvez développer à l’aide de OpenXR sur un casque de l’architecture HoloLens 2 ou Windows Mixed Reality sur le bureau.  Si vous n’avez pas accès à un casque, vous pouvez utiliser l’émulateur HoloLens 2 ou Windows Mixed Reality Simulator à la place.

## <a name="why-openxr"></a>Pourquoi OpenXR ?

Avec OpenXR, vous pouvez créer des moteurs qui ciblent les deux appareils holographiques (tels que HoloLens 2) qui placent le contenu numérique dans le monde réel comme s’il existait vraiment, ainsi que des appareils immersifs (tels que des casques Windows mixtes de réalité pour ordinateurs de bureau) qui masquent les et remplacez-le par un environnement numérique.  OpenXR vous permet d’écrire du code une fois qui est ensuite portable sur une large gamme de plateformes matérielles.

L’API OpenXR utilise un chargeur qui connecte votre application directement à la prise en charge native de la plateforme de votre casque.  Cela offre aux utilisateurs finaux des performances maximales et une latence minimale, qu’ils utilisent un casque Windows Mixed Reality ou tout autre casque.

## <a name="what-is-openxr"></a>Qu’est-ce que OpenXR ?

L’API OpenXR fournit les fonctionnalités principales de prédiction de pose, de minuterie de trame et de saisie spatiale dont vous aurez besoin pour créer un moteur qui peut cibler des appareils holographiques comme HoloLens 2 et des appareils immersifs tels que les casques de la réalité mixte Windows.

Pour en savoir plus sur l’API OpenXR, consultez la <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html" target="_blank">spécification</a>OpenXR 1,0, informations de <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/man/html/openxr.html" target="_blank">référence</a> sur les API et <a href="https://www.khronos.org/files/openxr-10-reference-guide.pdf" target="_blank">Guide de référence rapide</a>.  Pour plus d’informations, consultez la <a href="https://www.khronos.org/openxr/" target="_blank">page Khronos OpenXR</a>.

Pour cibler l’ensemble complet des fonctionnalités de HoloLens 2, vous utiliserez également des extensions OpenXR spécifiques à un fournisseur et à un fournisseur qui activent des fonctionnalités supplémentaires au-delà du OpenXR 1,0 cœurs, telles que le suivi articulé, le suivi oculaire, le mappage spatial et les ancrages spatiaux.  Pour plus d’informations sur les extensions arrivant plus tard cette année, consultez la [section Roadmap](#roadmap) ci-dessous.

Notez que OpenXR n’est pas lui-même un moteur de réalité mixte.  Au lieu de cela, OpenXR permet aux moteurs comme Unity et Unreal d’écrire du code portable une seule fois qui peut ensuite accéder aux fonctionnalités natives de la plateforme de l’appareil holographique ou immersif de l’utilisateur, quel que soit le fournisseur qui a créé cette plateforme.

## <a name="roadmap"></a>Présentation

La spécification OpenXR définit un mécanisme d’extension qui permet aux implémenteurs de runtime d’exposer des fonctionnalités supplémentaires au-delà des [fonctionnalités](#what-is-openxr) de base définies dans la <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html" target="_blank">spécification 1,0 de base OpenXR</a>.

Il existe trois types d’extensions OpenXR :
* **Extensions de fournisseur (par exemple `MSFT`) :** Active l’innovation par fournisseur dans les fonctionnalités matérielles ou logicielles.  N’importe quel fournisseur de Runtime peut introduire et livrer une extension de fournisseur à tout moment.
  * **Extensions de fournisseurs expérimentales (par exemple `MSFT_preview`) :** Extensions de fournisseurs expérimentées prévisualisées pour recueillir des commentaires.  les extensions de `MSFT_preview` sont destinées aux appareils de développement uniquement et seront supprimées lors de la livraison de l’extension réelle.  Pour les expérimenter, vous pouvez [activer les extensions préliminaires sur votre appareil de développement](openxr-getting-started.md#using-preview-extensions).
* **Extensions de `EXT` inter-fournisseurs :** Extensions inter-fournisseurs que plusieurs entreprises définissent et implémentent.  Les groupes de sociétés intéressées peuvent introduire des extensions EXT à tout moment.
* **Extensions `KHR` officielles :** Extensions Khronos officielles ratifiées dans le cadre d’une version de base spec.  Les extensions KHR sont couvertes par la même licence que la spécification principale elle-même.

D’ici le 2020 juillet, le runtime Windows Mixed Reality OpenXR prend en charge un ensemble d’extensions de `MSFT` et `EXT` qui apportent l’ensemble complet de fonctionnalités HoloLens 2 aux applications OpenXR :

| Domaine de fonctionnalité | Disponibilité de l’extension |
|--------------|------------------------|
| Systèmes et sessions | **OpenXR 1,0 Core spec :**<br /><code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#instance" target="_blank">XrInstance</a></code>, <code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#system" target="_blank">XrSystemId</a></code> <code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#session" target="_blank">XrSession</a></code> |
| [Espaces de référence (vue, local, intermédiaire)](coordinate-systems.md) | **OpenXR 1,0 Core spec :**<br /><code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#spaces" target="_blank">XrSpace</a></code> |
| Afficher les configurations (mono, stéréo) | **OpenXR 1,0 Core spec :**<br /><code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#view_configurations" target="_blank">XrView...</a></code> |
| [Chaînes d’échange](rendering.md) + [minutage des frames](understanding-performance-for-mixed-reality.md) | **OpenXR 1,0 Core spec :**<br /><code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#rendering" target="_blank">XrSwapchain...</a></code> + <code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#frame-synchronization" target="_blank">xrWaitFrame</a></code> |
| Couches de composition<br />(projection, quadruple) | **OpenXR 1,0 Core spec :**<br /><code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#compositing" target="_blank">XrCompositionLayer...</a></code> + <code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#frame-submission" target="_blank">xrEndFrame</a></code> |
| [Entrée et haptique](interaction-fundamentals.md) | **OpenXR 1,0 Core spec :**<br /><code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#input" target="_blank">XrAction...</a></code> |
| Intégration de Direct3D 11 | **Extension de `KHR` officielle publiée :**<br /><code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#XR_KHR_D3D11_enable" target="_blank">XR_KHR_D3D11_enable</a></code><br /> |
| Intégration de Direct3D 12 | **Extension de `KHR` officielle définie :** *(pas encore pris en charge)*<br /><code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#XR_KHR_D3D12_enable" target="_blank">XR_KHR_D3D12_enable</a></code><br /><p>**Prise en charge**de la version préliminaire : 2020 avril *(planifié)*</p><p>**Prise en charge complète**: mai 2020 *(planifié)*</p> |
| [Espace de référence non lié<br />(expériences à l’échelle mondiale)](coordinate-systems.md#building-a-world-scale-experience) | **extension de `MSFT` publiée :**<br /><code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#XR_MSFT_unbounded_reference_space" target="_blank">XR_MSFT_unbounded_reference_space</a></code> |
| [Ancres spatiales](spatial-anchors.md) | **extension de `MSFT` publiée :**<br /><code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#XR_MSFT_spatial_anchor">XR_MSFT_spatial_anchor</a></code> |
| [<br />d’interaction de la main (pose/pose, robinet, attrape)](hands-and-tools.md) | **extension de `MSFT_preview` disponible :**<br /><code><a href="https://microsoft.github.io/OpenXR-MixedReality/openxr_preview/specs/openxr.html#XR_MSFT_hand_interaction_preview">XR_MSFT_hand_interaction_preview</a></code><p>**version de`MSFT`** : 2020 avril *(planifié)*</p> |
| [Articulation manuelle + maille](hands-and-tools.md) | **extension de `MSFT_preview` disponible :**<br /><code><a href="https://microsoft.github.io/OpenXR-MixedReality/openxr_preview/specs/openxr.html#XR_MSFT_hand_tracking_preview">XR_MSFT_hand_tracking_preview</a></code><br /><code><a href="https://microsoft.github.io/OpenXR-MixedReality/openxr_preview/specs/openxr.html#XR_MSFT_hand_tracking_mesh_preview">XR_MSFT_hand_tracking_mesh_preview</a></code><p>**version de`MSFT`** : mai 2020 *(planifié)*</p> |
| Interopérabilité avec d’autres kits de développement logiciel (SDK) HoloLens (par exemple, [QR](qr-code-tracking.md)) | **extension de `MSFT_preview` disponible :**<br /><code><a href="https://microsoft.github.io/OpenXR-MixedReality/openxr_preview/specs/openxr.html#XR_MSFT_spatial_graph_bridge_preview">XR_MSFT_spatial_graph_bridge_preview</a></code><p>**version de`MSFT`** : mai 2020 *(planifié)*</p> |
| [Suivre du regard](eye-tracking.md) | <p>**extension de`EXT` définie**: *(pas encore pris en charge)*<br /><code><a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html#XR_EXT_eye_gaze_interaction" target="_blank">XR_EXT_eye_gaze_interaction</a></code><p>**Prise en charge**de la version préliminaire : 2020 avril *(planifié)*</p><p>**Prise en charge complète**: mai 2020 *(planifié)*</p> |
| [<br />de capture de réalité mixte (troisième rendu à partir d’une caméra PV)](mixed-reality-capture-for-developers.md#render-from-the-pv-camera-opt-in) | **extension de `MSFT_preview` disponible :**<br /><code><a href="https://microsoft.github.io/OpenXR-MixedReality/openxr_preview/specs/openxr.html#XR_MSFT_secondary_view_configuration_preview">XR_MSFT_secondary_view_configuration_preview</a></code><br /><code><a href="https://microsoft.github.io/OpenXR-MixedReality/openxr_preview/specs/openxr.html#XR_MSFT_first_person_observer_preview">XR_MSFT_first_person_observer_preview</a></code><br /><p>**version de`MSFT`** : 2020 juin *(planifié)*</p> |
| [Modèles de rendu du contrôleur de mouvement](motion-controllers.md#rendering-the-motion-controller-model) | <p>**`MSFT_preview`** : 2020 avril *(planifié)*</p><p>**version de`MSFT`** : juillet 2020 *(planifié)*</p> |
| [Compréhension des scènes (plans, maillages)](scene-understanding.md) | <p>**`MSFT_preview`** : 2020 mai *(planifié)*</p><p>**version de`MSFT`** : juillet 2020 *(planifié)*</p> |

Alors que certaines de ces extensions peuvent commencer par des extensions `MSFT` spécifiques au fournisseur, Microsoft et d’autres fournisseurs de Runtime OpenXR travaillent ensemble pour concevoir des extensions de `EXT` ou de `KHR` inter-fournisseurs pour la plupart de ces fonctionnalités.  Cela permet au code que vous écrivez pour que ces fonctionnalités soient portables entre les fournisseurs de Runtime, tout comme avec la spécification principale.

## <a name="get-started-with-openxr"></a>Prise en main de OpenXR

Vous pouvez développer à l’aide de OpenXR sur un casque de l’architecture HoloLens 2 ou Windows Mixed Reality sur le bureau.  Si vous n’avez pas accès à un casque, vous pouvez utiliser l’émulateur HoloLens 2 ou Windows Mixed Reality Simulator à la place.

Pour commencer à développer des applications OpenXR pour les casques HoloLens 2 ou Windows Mixed Reality, consultez [la page prise en main du développement OpenXR](openxr-getting-started.md).

## <a name="see-also"></a>Voir aussi

* <a href="https://www.khronos.org/openxr/" target="_blank">Plus d’informations sur OpenXR</a>
* <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html" target="_blank">Spécification OpenXR 1,0</a>
* <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/man/html/openxr.html" target="_blank">Informations de référence sur l’API OpenXR 1,0</a>
* <a href="https://www.khronos.org/files/openxr-10-reference-guide.pdf" target="_blank">Guide de référence rapide de OpenXR 1,0</a>
