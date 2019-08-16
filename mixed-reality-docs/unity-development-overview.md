---
title: Vue d’ensemble du développement Unity
description: Prise en main de la création d’applications de réalité mixte dans Unity.
author: thetuvix
ms.author: Yoyoz
ms.date: 04/15/2018
ms.topic: article
keywords: Unity, réalité mixte, développement, prise en main, nouveau projet, Portage, capacité, caméra, simulation, émulation, documentation
ms.openlocfilehash: b1384e886a2b4d0b3ed9f8008fca6af6ad4b78d5
ms.sourcegitcommit: af1602710c1ccb7ed870a491923350d387706129
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68701791"
---
# <a name="unity-development-overview"></a>Vue d’ensemble du développement Unity

Le chemin le plus rapide pour créer une [application de réalité mixte](app-views.md) est avec [Unity](http://aka.ms/HoloLensUnity). Nous vous recommandons de prendre le temps d’explorer les [tutoriels Unity](https://unity3d.com/learn/tutorials). Si vous avez besoin de ressources, Unity dispose d’un [magasin d’actifs](https://www.assetstore.unity3d.com/)complet. Une fois que vous avez acquis des connaissances élémentaires sur Unity, vous  pouvez consulter les [tutoriels](tutorials.md) pour découvrir les spécificités du développement de la réalité mixte avec Unity. Veillez à visiter les [Forums Unity Real realer](http://forum.unity3d.com/forums/hololens.102/) pour faire appel au reste de la communauté création d’applications de réalité mixte dans Unity et trouvez des solutions aux problèmes que vous pourriez rencontrer.

Pour commencer à créer des applications de réalité mixte avec Unity, commencez par [installer les outils](install-the-tools.md). 

## <a name="new-unity-project-with-mixed-reality-toolkit"></a>Nouveau projet Unity avec la réalité mixte Toolkit 

Le moyen le plus simple de développer dans Unity est d’utiliser le kit d’outils de réalité mixte. Il vous aidera à configurer automatiquement Project et à fournir un ensemble de fonctionnalités de réalité mixte pour accélérer votre développement. Consultez la boîte à outils de la [réalité mixte](mrtk-getting-started.md) pour en savoir plus et commencer. 

## <a name="porting-an-existing-unity-app-to-windows-mixed-reality"></a>Portage d’une application Unity existante vers Windows Mixed Reality

Si vous avez un projet Unity dont vous effectuez le portage vers Windows Mixed Reality, suivez le [Guide de Portage Unity](porting-guides.md) pour commencer.

## <a name="configuring-new-unity-project-for-windows-mixed-reality"></a>Configuration d’un nouveau projet Unity pour Windows Mixed Reality

Si vous souhaitez créer un nouveau projet Unity sans importer la boîte à outils de réalité mixte, il existe un petit ensemble de paramètres Unity que vous devrez modifier manuellement pour Windows Mixed Reality. Elles sont divisées en deux catégories: par projet et par scène. Pour obtenir le guide pas à pas pour [configurer le nouveau projet Unity pour Windows Mixed Reality](Configure-Unity-Project.md) , cliquez ici

## <a name="adding-mixed-reality-capabilities-and-inputs"></a>Ajout de fonctionnalités et d’entrées de réalité mixte

Une fois que vous avez configuré MRTK v2 avec votre projet, ou que vous avez configuré votre projet comme décrit ci-dessus, les objets de jeu Unity standard (comme l’appareil photo) s’illuminent immédiatement pour une expérience à l' **échelle**de l’appareil, la position de la caméra étant mise à jour automatiquement en fonction de la l’utilisateur déplace son chef dans le monde entier.

L’ajout de la prise en charge des fonctionnalités Windows Mixed Reality, telles que les [étapes spatiales](coordinate-systems.md#spatial-coordinate-systems), les [gestes,](gestures-and-motion-controllers-in-unity.md) les contrôleurs de mouvement ou l' [entrée vocale](voice-input-in-unity.md) , s’effectue à l’aide d’API intégrées directement dans Unity. 

Tout d’abord, passez en revue les mises à l' [échelle](coordinate-systems.md) que votre applicatioin peut cibler:
* Si vous envisagez de créer une expérience d' **orientation uniquement** ou de mise à l' **échelle installée**, vous devez définir le type d’espace de suivi de l’unité de mesure sur [stationnaire](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience).
* Si vous envisagez de créer **une** expérience à l’échelle de l' **espace**ou de la mise à l’échelle, vous devez vérifier que le type d’espace de suivi Unity est correctement défini sur [RoomScale](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience).
* Si vous envisagez de créer une expérience de mise à l' **échelle mondiale** sur HoloLens qui permet aux utilisateurs d’être itinérants au-delà de 5 mètres, vous devrez utiliser le composant [WorldAnchor](coordinate-systems-in-unity.md#building-a-world-scale-experience) .

Tous les blocs de construction principaux pour les applications de réalité mixte sont exposés de manière cohérente avec les autres API Unity. Ils sont également disponibles via le kit de la réalité mixte.
* [Appareil photo](camera-in-unity.md)
* [Systèmes de coordonnées](coordinate-systems-in-unity.md)
* [Pointage du regard](gaze-in-unity.md)
* [Gestes et contrôleurs de mouvement](gestures-and-motion-controllers-in-unity.md)
* [Entrée vocale](voice-input-in-unity.md)
* [Persistance](persistence-in-unity.md)
* [Son spatial](spatial-sound-in-unity.md)
* [Mappage spatial](spatial-mapping-in-unity.md)

Il existe d’autres fonctionnalités clés que de nombreuses applications de réalité mixte souhaiteront utiliser et qui sont également exposées aux applications Unity:
* [Expériences partagées](shared-experiences-in-unity.md)
* [Appareil photo localisable](locatable-camera-in-unity.md)
* [Point de focus](focus-point-in-unity.md)
* [Perte de suivi](tracking-loss-in-unity.md)
* [Clavier](keyboard-input-in-unity.md)

## <a name="running-your-unity-project-on-a-real-or-simulated-device"></a>Exécution de votre projet Unity sur un appareil réel ou simulé

Une fois votre projet Unity holographique prêt pour le test, l’étape suivante consiste à [exporter et à créer une solution Unity Visual Studio](exporting-and-building-a-unity-visual-studio-solution.md).

Avec cette solution VS, vous pouvez exécuter votre application de l’une des trois manières suivantes, à l’aide d’un appareil réel ou simulé:
* [Déployez sur un véritable casque Windows de la realisation](using-visual-studio.md)
* [Déployer sur l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Déployer dans le simulateur de casque immersif Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md)

## <a name="unity-documentation"></a>Documentation Unity

En plus de cette documentation disponible sur docs.microsoft.com, Unity installe la documentation de la fonctionnalité Windows Mixed Reality en plus de l’éditeur Unity. La documentation fournie par Unity comprend deux sections distinctes:
1. **Référence de script Unity**
    * Cette section de la documentation contient les détails de l’API de script fournie par Unity.
    * Accessible à partir de l’éditeur Unity par le biais de l' **aide > la référence de script**
2. **Manuel Unity**
    * Ce manuel est conçu pour vous aider à apprendre à utiliser Unity, des techniques de base aux techniques avancées.
    * Accessible à partir de l’éditeur Unity via l' **aide > manuelle**

## <a name="see-also"></a>Voir aussi
* [Boîte à outils de réalité mixte v2](mrtk-getting-started.md)
* [Réalité mixte - Principes fondamentaux - Cours 100 : Bien démarrer avec Unity](holograms-100.md)
* [Paramètres recommandés pour Unity](recommended-settings-for-unity.md)
* [Recommandations de performances pour Unity](performance-recommendations-for-unity.md)
* [Exportation et création de solutions Unity Visual Studio](exporting-and-building-a-unity-visual-studio-solution.md)
* [Utilisation de l’espace de noms Windows avec les applications Unity pour HoloLens](using-the-windows-namespace-with-unity-apps-for-hololens.md)
* [Bonnes pratiques sur l’utilisation d’Unity et de Visual Studio](best-practices-for-working-with-unity-and-visual-studio.md)
* [Mode Lecture Unity](unity-play-mode.md)
* [Guides de Portage](porting-guides.md)
