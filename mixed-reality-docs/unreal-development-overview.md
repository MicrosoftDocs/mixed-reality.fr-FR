---
title: Vue d’ensemble du développement Unreal
description: Vue d’ensemble du développement en réalité mixte avec Unreal Engine 4
author: sw5813
ms.author: suwu
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, streaming, communication à distance, réalité mixte, développement, bien démarrer, fonctionnalités, nouveau projet, émulateur, documentation, guides fonctionnalités, hologrammes
ms.openlocfilehash: 08ba760acc1a35d8f47de6a7bf6cbc020c8aca3f
ms.sourcegitcommit: 189a47b8712dd5b620e19815f5cf6d1ac0f29880
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2020
ms.locfileid: "82851563"
---
# <a name="unreal-development-overview"></a>Vue d’ensemble du développement Unreal

Unreal Engine 4 prend désormais entièrement en charge le développement pour les appareils Windows Mixed Reality (VR) et HoloLens 2 (AR) ! Si vous n’avez jamais utilisé Unreal pour développer des applications, découvrez comment <a href="https://docs.unrealengine.com//GettingStarted/index.html" target="_blank">bien démarrer avec Unreal Engine 4</a>. Si vous avez besoin de ressources, Unreal propose une <a href="https://www.unrealengine.com/marketplace//store" target="_blank">place de marché</a> complète. 

Une fois que vous avez acquis une compréhension de base du développement Unreal, consultez le tutoriel dans la section suivante pour découvrir comment créer et exécuter vos applications sur HoloLens. N’hésitez pas à consulter les <a href="https://forums.unrealengine.com/development-discussion/vr-ar-development" target="_blank">forums de réalité mixte Unreal</a> pour dialoguer avec des membres de la communauté qui créent des applications de réalité mixte dans Unreal. C’est l’endroit idéal pour trouver des solutions aux problèmes que vous pouvez rencontrer.

## <a name="tutorial"></a>Tutoriel

Découvrez comment [créer et déployer une application de jeu d’échecs simple](unreal-uxt-ch1.md) pour HoloLens 2 en suivant notre tutoriel de bout en bout. Ce tutoriel utilise le plug-in UX Tools pour accélérer le développement d’applications avec des composants UX interactifs, notamment un bouton et un manipulateur. Pour plus d’informations sur le plug-in UX, consultez la section suivante sur MRTK. 

## <a name="mixed-reality-toolkit-for-unreal"></a>Mixed Reality Toolkit pour Unreal

Le [Mixed Reality Toolkit pour Unreal](https://github.com/microsoft/MixedRealityToolkit-Unreal) est un ensemble de composants sous forme de plug-ins, d’exemples et de documentations, conçus pour accélérer le développement d’applications de réalité mixte avec Unreal Engine. Le premier composant publié dans le cadre de cette boîte à outils est [UX Tools pour Unreal](https://github.com/microsoft/MixedReality-UXTools-Unreal), un plug-in qui peut être ajouté à votre projet HoloLens 2 pour fournir des fonctionnalités UX destinées aux applications HoloLens 2. Vous trouverez la documentation relative à Mixed Reality Toolkit et à UX Tools dans leurs dépôts GitHub respectifs. 

## <a name="performance"></a>Performances

Une application HoloLens 2 doit s’exécuter à 60 images par seconde pour que les hologrammes apparaissent stables et réactifs. Pour y parvenir dans votre application, nous vous recommandons fortement de suivre nos [recommandations en matière de performances pour Unreal](performance-recommendations-for-unreal.md). 

## <a name="guides-to-specific-features"></a>Guides pour des fonctionnalités spécifiques

Pour découvrir comment utiliser des fonctionnalités spécifiques dans Unreal, consultez les guides ci-dessous : 
* [Suivi de la main](unreal-hand-tracking.md)
* [Eye-tracking](unreal-gaze-input.md)
* [Mappage spatial](unreal-spatial-mapping.md)
* [Ancres spatiales](unreal-spatial-anchors.md)
* [Entrée vocale](unreal-voice-input.md)
* [Caméra HoloLens](unreal-hololens-camera.md)
* [Codes QR](unreal-qr-codes.md)

## <a name="supported-features"></a>Fonctionnalités prises en charge

| Fonctionnalité HoloLens 2 | Version la plus ancienne d’Unreal Engine prise en charge |
| ----------- | ----------- |
| Prise en charge d’ARM64 | 4.23 |
| Streaming depuis un PC | 4.23 |
| Mappage spatial | 4.23 |
| Suivi des mains et des articulations | 4.23 |
| Eye-tracking | 4.23 |
| Entrée vocale | 4.23 |
| Ancres spatiales | 4.23 |
| Accès à la caméra | 4.23 |
| Codes QR | 4.23 |
| Audio spatial | 4.23 |
| Prise en charge d’un écran de spectateur pour le streaming | 4.24 |
| LSR plan en streaming | 4.24 |
| Exemples d’applications ([HoloLens2Example](https://github.com/microsoft/MixedReality-Unreal-Samples) et [Mission AR](https://docs.unrealengine.com/en-US/Resources/Showcases/MissionAR/index.html)) | 4.24 |
| Multivue mobile : Les performances atteignent 60 i/s | 4.25 |
| Rendu 3ème caméra | 4.25 |
| Streaming partir d’une application de poste de travail empaquetée | 4.25 |
| Azure Spatial Anchors pour HoloLens 2 (bêta) | 4.25 |
| Prise en charge d’OpenXR (bêta) | 4.25 |
| Prise en charge d’UX Tools (0.8) | 4.25 |
| Documentation et tutoriels pour les développeurs | 4.25 |

## <a name="see-also"></a>Voir aussi
* <a href="https://docs.unrealengine.com//Platforms/AR/HoloLens2/index.html" target="_blank">Documents Unreal pour le streaming, le déploiement sur l’émulateur et l’appareil</a>
* <a href="https://docs.unrealengine.com//Platforms/Mobile/Performance/index.html" target="_blank">Conseils d’optimisation des performances sur les appareils mobiles avec Unreal</a>
