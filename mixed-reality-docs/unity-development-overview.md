---
title: Vue d’ensemble du développement Unity
description: Commencez à créer des applications de réalité mixte dans Unity.
author: thetuvix
ms.author: kurtie
ms.date: 10/25/2018
ms.topic: article
ms.localizationpriority: high
keywords: Unity, réalité mixte, développement, bien démarrer, nouveau projet, portage, capacité, caméra, simulation, émulation, documentation
ms.openlocfilehash: e0fe775f5fe891416145d91e52a5a801e049c568
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "81433415"
---
# <a name="unity-development-overview"></a>Vue d’ensemble du développement Unity

Rien de tel qu’[Unity](https://unity.com) pour créer rapidement une [application de réalité mixte](app-views.md). Nous vous recommandons de prendre le temps d’explorer les [tutoriels Unity](https://unity3d.com/learn/tutorials). Si vous avez besoin de ressources, Unity dispose d’un [magasin de ressources](https://www.assetstore.unity3d.com/) complet. Une fois que vous avez acquis des connaissances de base sur Unity, consultez les [tutoriels](tutorials.md) pour découvrir les spécificités du développement de réalité mixte avec Unity. N’hésitez pas à visiter les [forums Unity](https://forum.unity3d.com/forums/hololens.102/) pour dialoguer avec des membres de la communauté qui créent des applications de réalité mixte dans Unity et trouver des solutions aux problèmes que vous pouvez rencontrer.

Pour commencer à créer des applications de réalité mixte avec Unity, [installez les outils nécessaires](install-the-tools.md). 

>[!VIDEO https://channel9.msdn.com/Shows/Docs-Mixed-Reality/Setting-up-your-HoloLens-2-development-environment/player?format=ny]

## <a name="new-unity-project-with-mixed-reality-toolkit"></a>Nouveau projet Unity avec Mixed Reality Toolkit 

Le moyen le plus simple de développer dans Unity consiste à utiliser le Mixed Reality Toolkit. Ce kit d’outils vous aide à configurer automatiquement votre projet et fournit un ensemble de fonctionnalités de réalité mixte pour accélérer le développement. Pour en savoir plus et pour démarrer, consultez [Mixed Reality Toolkit v2](mrtk-getting-started.md). 

## <a name="porting-an-existing-unity-app-to-windows-mixed-reality"></a>Portage d’une application Unity existante vers Windows Mixed Reality

Si vous souhaitez porter un projet Unity existant vers Windows Mixed Reality, suivez le [guide de portage Unity](porting-guides.md) pour démarrer.

## <a name="configuring-new-unity-project-for-windows-mixed-reality"></a>Configuration d’un nouveau projet Unity pour Windows Mixed Reality

Si vous souhaitez créer un projet Unity sans importer le Mixed Reality Toolkit, vous devez changer manuellement quelques paramètres dans Unity pour Windows Mixed Reality. Ceux-ci sont divisés en deux catégories : par projet et par scène. Pour obtenir un guide pas à pas, consultez [Configurer un nouveau projet Unity pour Windows Mixed Reality](Configure-Unity-Project.md)

## <a name="adding-mixed-reality-capabilities-and-inputs"></a>Ajout de fonctionnalités et d’entrées de réalité mixte

Une fois que vous avez configuré MRTK v2 avec votre projet ou configuré votre projet comme décrit ci-dessus, les objets de jeu Unity standard (comme la caméra) s’illuminent immédiatement pour une **expérience à l’échelle assise**, la position de la caméra se mettant automatiquement à jour à mesure que l’utilisateur bouge la tête dans le monde.

Pour prendre en charge les fonctionnalités de Windows Mixed Reality comme les [phases spatiales](coordinate-systems.md#spatial-coordinate-systems), les [gestes et contrôleurs de mouvement](gestures-and-motion-controllers-in-unity.md) ou les [entrées vocales](voice-input-in-unity.md), utilisez les API intégrées directement dans Unity. 

Pour commencer, passez en revue les [échelles d’expérience](coordinate-systems.md) que votre application peut cibler :
* Si vous envisagez de créer une expérience **à orientation uniquement** ou **à l’échelle assise**, choisissez le type d’espace de suivi [Stationary](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience) dans Unity.
* Si vous envisagez de créer une expérience **à l’échelle debout** ou **à l’échelle de la pièce**, veillez à définir [RoomScale](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience) comme type d’espace de suivi dans Unity.
* Si vous envisagez de créer sur HoloLens une expérience **à l’échelle du monde**, qui permet aux utilisateurs de se déplacer dans un rayon de plus de 5 mètres, utilisez le composant [WorldAnchor](coordinate-systems-in-unity.md#building-a-world-scale-experience).

Tous les composants principaux pour les applications de réalité mixte sont exposés de manière cohérente avec les autres API Unity. Ils sont également disponibles par le biais du Mixed Reality Toolkit.
* [Appareil photo](camera-in-unity.md)
* [Systèmes de coordonnées](coordinate-systems-in-unity.md)
* [Pointage du regard](gaze-in-unity.md)
* [Mouvements et contrôleurs de mouvement](gestures-and-motion-controllers-in-unity.md)
* [Entrée vocale](voice-input-in-unity.md)
* [Persistance](persistence-in-unity.md)
* [Son spatial](spatial-sound-in-unity.md)
* [Mappage spatial](spatial-mapping-in-unity.md)

D’autres fonctionnalités clés susceptibles d’être utilisées par des applications de réalité mixte sont également exposées aux applications Unity :
* [Expériences partagées](shared-experiences-in-unity.md)
* [Appareil photo localisable](locatable-camera-in-unity.md)
* [Point de focus](focus-point-in-unity.md)
* [Perte de suivi](tracking-loss-in-unity.md)
* [Clavier](keyboard-input-in-unity.md)

## <a name="running-your-unity-project-on-a-real-or-simulated-device"></a>Exécution de votre projet Unity sur un appareil réel ou simulé

Une fois que votre projet Unity holographique est prêt à être testé, l’étape suivante consiste [à exporter et à créer une solution Visual Studio Unity](exporting-and-building-a-unity-visual-studio-solution.md).

Avec cette solution Visual Studio, vous pouvez exécuter votre application de l’une des trois manières suivantes, à l’aide d’un appareil réel ou simulé :
* [Déployer sur un appareil HoloLens ou un casque immersif Windows Mixed Reality réel](using-visual-studio.md)
* [Déployer sur l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Déployer sur le simulateur de casque immersif Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md)

## <a name="unity-documentation"></a>Documentation Unity

En plus de cette documentation disponible sur docs.microsoft.com, Unity installe la documentation sur la fonctionnalité Windows Mixed Reality avec l’éditeur Unity. La documentation fournie par Unity comprend deux sections distinctes :
1. **Informations de référence sur les scripts Unity**
    * Cette section de la documentation contient les détails de l’API de création de script fournie par Unity.
    * Accessible à partir de l’éditeur Unity (**Help > Scripting Reference**).
2. **Manuel Unity**
    * Ce manuel est conçu pour vous aider à utiliser Unity, des notions de base aux techniques avancées.
    * Accessible à partir de l’éditeur Unity (**Help > Manual**).

## <a name="see-also"></a>Voir aussi
* [Mixed Reality Toolkit v2](mrtk-getting-started.md)
* [Réalité mixte - Principes fondamentaux - Cours 100 : Bien démarrer avec Unity](holograms-100.md)
* [Paramètres recommandés pour Unity](recommended-settings-for-unity.md)
* [Recommandations de performances pour Unity](performance-recommendations-for-unity.md)
* [Exportation et création de solutions Unity Visual Studio](exporting-and-building-a-unity-visual-studio-solution.md)
* [Utilisation de l’espace de noms Windows avec les applications Unity pour HoloLens](using-the-windows-namespace-with-unity-apps-for-hololens.md)
* [Bonnes pratiques sur l’utilisation d’Unity et de Visual Studio](best-practices-for-working-with-unity-and-visual-studio.md)
* [Mode Lecture Unity](unity-play-mode.md)
* [Guides de portage](porting-guides.md)
