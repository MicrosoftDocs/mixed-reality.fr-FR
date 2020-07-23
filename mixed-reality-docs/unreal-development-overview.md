---
title: Vue d’ensemble du développement Unreal
description: Vue d’ensemble du développement en réalité mixte avec Unreal Engine 4
author: hferrone
ms.author: v-haferr
ms.date: 7/10/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, streaming, communication à distance, réalité mixte, développement, démarrage, fonctionnalités, nouveau projet, émulateur, documentation, guides, fonctionnalités, hologrammes, développement de jeux
ms.openlocfilehash: ecf982eb5d8128734c862bac2d8be29c1554edfe
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86303620"
---
# <a name="unreal-development-overview"></a>Vue d’ensemble du développement Unreal

Démarrer avec les <a href="https://docs.microsoft.com/windows/mixed-reality" target="_blank" title="Documentation Mixed Reality"> applications de réalité mixte</a> n’est pas chose aisée. Nouveaux concepts, nouvelles plateformes, matériel de pointe : tout cela peut être vu comme un obstacle. Toutefois, si vous êtes développeur Unreal, vous avez de la chance. La prise en charge de <a href="https://www.microsoft.com/windows/windows-mixed-reality" target="_blank" title="Documentation Windows Mixed Reality">Windows Mixed Reality</a> (VR) et de <a href="https://www.microsoft.com/hololens/hardware" target="_blank" title="Documentation HoloLens 2">HoloLens 2</a> (réalité augmentée) est maintenant incluse dans la dernière <a href="https://docs.unrealengine.com/Support/Builds/ReleaseNotes/4_25/index.html" target="_blank" title="Notes de publication Unreal Engine 4.25">version</a> d’Unreal Engine. Voici ce que cette mise à jour comprend :
* Prise en charge du plug-in Mixed Reality UX Tools
* Prise en charge d’OpenXR
* Communication à distance d’application à partir d’une application de bureau
* Meilleures performances
* MRC (Mixed Reality Capture)
* Prise en charge initiale pour Azure Spatial Anchors

Si vous n’avez aucune expérience du développement Unreal, ne vous lancez pas tête baissée. Explorez la <a href="https://docs.unrealengine.com/GettingStarted/index.html" target="_blank">série de tutoriels</a> Unreal pour devenir rapidement opérationnel en recherchant des ressources sur la <a href="https://www.unrealengine.com/marketplace/store" target="_blank">place de marché</a> Unreal et de l’aide sur les <a href="https://forums.unrealengine.com/development-discussion/vr-ar-development" target="_blank">forums</a> de réalité mixte. Ces ressources constituent vos liens avec la communauté de concepteurs et de solutionneurs de problèmes sur le marché de la réalité mixte d’aujourd’hui.

## <a name="mixed-reality-toolkit-for-unreal"></a>Mixed Reality Toolkit pour Unreal

[Mixed Reality Toolkit for Unreal](https://github.com/microsoft/MixedRealityToolkit-Unreal) est un ensemble de composants conçus pour accélérer votre développement dans Unreal. Chaque composant comprend des plug-ins, des exemples et une documentation pour configurer des expériences immersives. 

[UX Tools for Unreal](https://github.com/microsoft/MixedReality-UXTools-Unreal) est le premier composant à être publié et n’est actuellement pris en charge que sur HoloLens 2. Le plug-in de composants comprend du code, des blueprints et des exemples de ressources de fonctionnalités d’expérience utilisateur courantes, notamment :
* Simulation d’entrée
* Acteurs d’interaction manuelle
* Composant bouton sur lequel appuyer
* Composant manipulateur
* Composant comportement suiveur

Vous pouvez explorer le dépôt GitHub [UX Tools for Unreal](https://github.com/microsoft/MixedReality-UXTools-Unreal) pour obtenir des détails sur les fonctionnalités et des informations sur la façon de configurer votre projet.

## <a name="hololens-2-platform-support"></a>Prise en charge de la plateforme HoloLens 2
Si c’est la première fois que vous créez ou que vous déployez une application Unreal pour HoloLens, vous devrez [télécharger les fichiers de prise en charge de la plateforme](unreal-uxt-ch6.md#packaging-and-deploying-the-app-via-device-portal) auprès de Epic Launcher.

## <a name="tutorial"></a>Tutoriel

La meilleure façon d’acquérir une nouvelle compétence est de créer quelque chose de ses propres mains. Apprendre à [créer et déployer une application de jeu d’échecs simple](unreal-uxt-ch1.md) pour HoloLens 2 avec le plug-in UX Tools est une excellente façon de commencer. 

La série complète de tutoriels permet de découvrir d’un point de vue pratique les scénarios et les composants d’expérience utilisateur interactifs courants. Vous procéderez à la configuration d’un projet, en ajoutant des interactions à la scène et en effectuant un déploiement sur un appareil ou un émulateur. Vous avez seulement besoin de Windows 10, d’un émulateur et de Visual Studio 2019.

## <a name="debugging"></a>Débogage

Pour déboguer une application qui s’exécute sur HoloLens 2 avec Visual Studio, suivez les instructions fournies ici pour le [débogage d’une application UWP installée sur un appareil distant](https://docs.microsoft.com/visualstudio/debugger/debug-installed-app-package?view=vs-2019#remote).

## <a name="performance"></a>Performances

Le développement pour la réalité mixte s’accompagne de points de contrôle de performances qui varient en fonction de la plateforme. Une application HoloLens 2 doit s’exécuter à 60 images par seconde pour que les hologrammes apparaissent stables et réactifs. Heureusement, nous avons des [recommandations sur les performances](performance-recommendations-for-unreal.md) pour y parvenir dans vos applications Unreal.

## <a name="guides-to-specific-features"></a>Guides pour des fonctionnalités spécifiques

Notre série de tutoriels n’aborde pas certaines caractéristiques clés du développement en réalité mixte. Consultez les guides suivants pour obtenir des détails et des applications pratiques : 
* [Eye-tracking](unreal-gaze-input.md)
* [Suivi de la main](unreal-hand-tracking.md)
* [Caméra HoloLens](unreal-hololens-camera.md)
* [Ancres spatiales](unreal-spatial-anchors.md)
* [Mappage spatial](unreal-spatial-mapping.md)
* [Audio spatial](unreal-spatial-audio.md)
* [Streaming](unreal-streaming.md)
* [Entrée vocale](unreal-voice-input.md)
* [Codes QR](unreal-qr-codes.md)
* [Recommandations sur les performances](performance-recommendations-for-unreal.md)

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
| Exemples d’applications ([HoloLens2Example](https://github.com/microsoft/MixedReality-Unreal-Samples) et [Mission AR](https://docs.unrealengine.com/Resources/Showcases/MissionAR/index.html)) | 4.24 |
| Multivue mobile : Les performances atteignent 60 i/s | 4.25 |
| Rendu 3ème caméra | 4.25 |
| Streaming partir d’une application de poste de travail empaquetée | 4.25.1 |
| Azure Spatial Anchors pour HoloLens 2 (bêta) | 4.25 |
| Prise en charge d’OpenXR (bêta) | 4.25 |
| Prise en charge d’UX Tools (0.8) | 4.25 |
| Documentation et tutoriels pour les développeurs | 4.25 |

## <a name="see-also"></a>Voir aussi
* <a href="https://docs.unrealengine.com/Platforms/AR/HoloLens2/index.html" target="_blank">Documents Unreal pour le streaming, le déploiement sur l’émulateur et l’appareil</a>
* <a href="https://docs.unrealengine.com/Platforms/Mobile/Performance/index.html" target="_blank">Conseils d’optimisation des performances sur les appareils mobiles avec Unreal</a>
