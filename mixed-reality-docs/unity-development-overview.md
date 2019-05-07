---
title: Vue d’ensemble du développement Unity
description: Lors de l’obtention de construction prise en main les applications de réalité dans Unity de mixte.
author: thetuvix
ms.author: Yoyoz
ms.date: 04/15/2018
ms.topic: article
keywords: Unity, mixte réalité, développement, mise en route, un nouveau projet, portage, fonctionnalité, appareil photo, simulation, émulation, documentation
ms.openlocfilehash: 2cdcd5e997ab7e3f6d340377464e453a8e7c025c
ms.sourcegitcommit: 90ce9415889e7121dd2fd76a893dc3734672881b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64874005"
---
# <a name="unity-development-overview"></a>Vue d’ensemble du développement Unity

Le chemin d’accès le plus rapide pour créer un [application de réalité mixte](app-views.md) est avec [Unity](http://aka.ms/HoloLensUnity). Nous vous recommandons d’effectuer le temps d’Explorer la [didacticiels Unity sur](https://unity3d.com/learn/tutorials). Si vous avez besoin des éléments multimédias, Unity possède une gamme complète [Asset Store](https://www.assetstore.unity3d.com/). Une fois que vous avez créé d’une connaissance élémentaire de Unity, vous pouvez visiter le [didacticiels](tutorials.md) pour découvrir les spécificités du développement de réalité mixte avec Unity. Veillez à consulter le [forums de réalité mixte Unity](http://forum.unity3d.com/forums/hololens.102/) à engager avec le reste de la Communauté de développement d’applications de réalité mixte dans Unity et trouver des solutions aux problèmes que vous pouvez rencontrer.


Pour commencer à créer des applications de réalité mixte avec Unity, tout d’abord [installer les outils](install-the-tools.md). 

## <a name="new-unity-project-with-mixed-reality-toolkit"></a>Nouveau projet Unity avec le Kit de ressources de réalité mixte 

Pour développer dans Unity, le plus simple consiste à l’aide du Kit de ressources de réalité mixte. Il aide le programme d’installation avec le projet automatiquement et offrent un ensemble de fonctionnalités de réalité mixte pour accélérer votre développement. Consultez [v2 Toolkit de réalité mixte](mrtk-getting-started.md) pour en savoir plus et commencer. 

## <a name="porting-an-existing-unity-app-to-windows-mixed-reality"></a>Portage d’une application existante de Unity à Windows Mixed Reality

Si vous avez un projet Unity existant que vous portez à Windows Mixed Reality, suivre le [guide du portage Unity](porting-guides.md) pour commencer.

## <a name="configuring-new-unity-project-for-windows-mixed-reality"></a>Configuration de projet Unity pour Windows Mixed Reality

Si vous souhaitez créé un projet Unity sans importer Toolkit de réalité mixte, il existe un petit ensemble de paramètres de Unity vous devrez modifier manuellement pour Windows Mixed Reality, divisé en deux catégories : par projet et par scène. Consultez ici pour guide étape par étape [configurer nouveau Unity Project pour Windows Mixed Reality](Configure-Unity-Project.md)

## <a name="adding-mixed-reality-capabilities-and-inputs"></a>Ajout d’entrées et des fonctionnalités de réalité mixte

Une fois que vous avez le programme d’installation MRTK V2 avec votre projet et configuré votre projet comme décrit ci-dessus, les objets de jeu Unity standards (par exemple, l’appareil photo) seront allume immédiatement pour un **assis à l’échelle du expérience**, avec la position de la caméra mis à jour en tant que l’utilisateur déplace automatiquement leur tête dans le monde.

Ajout de prise en charge des fonctionnalités de Windows Mixed Reality comme [étapes spatiales](coordinate-systems.md#spatial-coordinate-systems), [mouvements, les contrôleurs de mouvement](gestures-and-motion-controllers-in-unity.md) ou [entrée voix](voice-input-in-unity.md) est obtenue à l’aide des API directement intégré aux Unity. 

La première étape doit consister pour passer en revue la [expérience échelles](coordinate-systems.md) que votre application peut cibler :
* Si vous avez besoin pour générer un **orientation seule** ou **assis à l’échelle du expérience**, vous devez définir Unity du suivi de type de l’espace à [stationnaire](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience).
* Si vous avez besoin pour générer un **permanent à l’échelle** ou **expérience de l’échelle de la salle**, vous devez vous assurer d’Unity suivi du type de l’espace est défini correctement à [RoomScale](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience).
* Si vous avez besoin pour générer un **à l’échelle du monde** expérience sur HoloLens, permettant aux utilisateurs de se déplacer au-delà de 5 mètres, vous devez utiliser le [WorldAnchor](coordinate-systems-in-unity.md#building-a-world-scale-experience) composant.

Tous les principaux blocs de construction pour les applications de réalité mixte sont exposées de manière cohérente avec d’autres API Unity. Ils sont également disponibles via Toolkit de réalité mixte.
* [Appareil photo](camera-in-unity.md)
* [Systèmes de coordonnées](coordinate-systems-in-unity.md)
* [Pointage du regard](gaze-in-unity.md)
* [Mouvements et les contrôleurs de mouvement](gestures-and-motion-controllers-in-unity.md)
* [Entrée vocale](voice-input-in-unity.md)
* [Persistance](persistence-in-unity.md)
* [Son spatial](spatial-sound-in-unity.md)
* [Mappage spatial](spatial-mapping-in-unity.md)

Il existe d’autres fonctionnalités clées que de nombreuses applications de réalité mixte souhaitez utiliser, qui sont également exposé à des applications Unity :
* [Expériences partagées](shared-experiences-in-unity.md)
* [Appareil photo localisable](locatable-camera-in-unity.md)
* [Point de focus](focus-point-in-unity.md)
* [Suivi de la perte](tracking-loss-in-unity.md)
* [Clavier](keyboard-input-in-unity.md)

## <a name="running-your-unity-project-on-a-real-or-simulated-device"></a>Votre projet Unity en cours d’exécution sur un appareil réel ou simulé

Une fois que vous avez votre projet Unity HOLOGRAPHIQUE prêt à tester, l’étape suivante consiste à [exporter et générer une solution de Unity Visual Studio](exporting-and-building-a-unity-visual-studio-solution.md).

Avec cette solution VS à portée de main, vous pouvez ensuite exécuter votre application dans un des trois manières, à l’aide un appareil réel ou simulé :
* [Déployer sur un casque immersif réel HoloLens ou Windows Mixed Reality](using-visual-studio.md)
* [Déploiement de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Déployer sur le simulateur de casque immersives Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md)

## <a name="unity-documentation"></a>Documentation Unity

Outre cette documentation disponible sur le centre de développement Windows, Unity installe la documentation pour les fonctionnalités de Windows Mixed Reality en même temps que l’éditeur Unity. L’Unity fourni documentation comprend deux sections distinctes :
1. **Référence de script Unity**
    * Cette section de la documentation contient des informations sur l’API de script Unity fournit.
    * Accessible à partir de l’éditeur Unity via **aide > référence de script**
2. **Manuel de Unity**
    * Ce manuel est conçu pour vous aider à apprendre comment utiliser Unity, techniques de base à avancées.
    * Accessible à partir de l’éditeur Unity via **aide > manuel**

## <a name="see-also"></a>Voir aussi
* [Une réalité mixte Toolkit v2](mrtk-getting-started.md)
* [Réalité mixte - Principes fondamentaux - Cours 100 : Bien démarrer avec Unity](holograms-100.md)
* [Paramètres recommandés pour Unity](recommended-settings-for-unity.md)
* [Recommandations de performances pour Unity](performance-recommendations-for-unity.md)
* [Exportation et création de solutions Unity Visual Studio](exporting-and-building-a-unity-visual-studio-solution.md)
* [Utilisation de l’espace de noms Windows avec les applications Unity pour HoloLens](using-the-windows-namespace-with-unity-apps-for-hololens.md)
* [Bonnes pratiques sur l’utilisation d’Unity et de Visual Studio](best-practices-for-working-with-unity-and-visual-studio.md)
* [Mode Lecture Unity](unity-play-mode.md)
* [Portage des repères](porting-guides.md)
