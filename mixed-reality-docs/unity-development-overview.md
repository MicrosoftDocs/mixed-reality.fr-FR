---
title: Vue d’ensemble du développement Unity
description: Lors de l’obtention de construction prise en main les applications de réalité dans Unity de mixte.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, mixte réalité, développement, mise en route, un nouveau projet, portage, fonctionnalité, appareil photo, simulation, émulation, documentation
ms.openlocfilehash: fc40ef4eae31cf22f640be2666c5af3afb717ff3
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596904"
---
# <a name="unity-development-overview"></a>Vue d’ensemble du développement Unity

Le chemin d’accès le plus rapide pour créer un [application de réalité mixte](app-views.md) est avec [Unity](http://aka.ms/HoloLensUnity). Nous vous recommandons d’effectuer le temps d’Explorer la [didacticiels Unity sur](https://unity3d.com/learn/tutorials). Si vous avez besoin des éléments multimédias, Unity possède une gamme complète [Asset Store](https://www.assetstore.unity3d.com/). Une fois que vous avez créé d’une connaissance élémentaire de Unity, vous pouvez visiter le [Académie de réalité mixte](academy.md) pour découvrir les spécificités du développement de réalité mixte avec Unity. Veillez à consulter le [forums de réalité mixte Unity](http://forum.unity3d.com/forums/hololens.102/) à engager avec le reste de la Communauté de développement d’applications de réalité mixte dans Unity et trouver des solutions aux problèmes que vous pouvez rencontrer.

## <a name="porting-an-existing-unity-app-to-windows-mixed-reality"></a>Portage d’une application existante de Unity à Windows Mixed Reality

Si vous avez un projet Unity existant que vous portez à Windows Mixed Reality, suivre le [guide du portage Unity](porting-guides.md) pour commencer.

## <a name="configuring-a-new-unity-project-for-windows-mixed-reality"></a>Configuration d’un projet Unity pour Windows Mixed Reality

Pour commencer à créer des applications de réalité mixte avec Unity, tout d’abord [installer les outils](install-the-tools.md). Si vous allez cibler des casques IMMERSIFS Windows Mixed Reality plutôt que HoloLens, vous devez une version spéciale de Unity pour l’instant.

Si vous venez de créer un nouveau projet Unity, il existe un petit ensemble de paramètres de Unity vous devrez modifier pour la réalité mixte Windows, divisé en deux catégories : par projet et par scène.

### <a name="per-project-settings"></a>Paramètres par projet

Pour cibler Windows Mixed Reality, vous devez d’abord configurer votre projet Unity à exporter en tant qu’une application de plateforme Windows universelle :
1. Sélectionnez **fichier > Paramètres de Build...**
2. Sélectionnez **plateforme Windows universelle** dans la plateforme de liste, puis cliquez sur **plateforme de commutation**
3. Définissez **SDK** à **10 universelle**
4. Définissez **appareil cible** à **n’importe quel appareil** pour prendre en charge des casques IMMERSIFS ou basculer vers **HoloLens**
5. Définissez **Type de Build** à **D3D**
6. Définissez **UWP SDK** à **dernière installé**

Nous devons informer Unity que l’application que nous tentons de les exporter doit créer un [vue immersive](app-views.md) au lieu d’une vue en 2D. Pour cela, nous l’activation de « Virtuel réalité pris en charge » :
1. À partir de la **paramètres de Build...**  fenêtre, ouvrez **paramètres du lecteur...**
2. Sélectionnez le **paramètres pour la plateforme Windows universelle** onglet
3. Développez le **XR paramètres** groupe
4. Dans le **XR paramètres** section, vérifiez le **virtuel pris en charge de réalité** case à cocher pour ajouter le **des appareils de réalité virtuelle** liste.
5. Dans le **XR paramètres** de groupe, vérifiez que **« Windows Mixed Reality »** est répertorié comme un appareil pris en charge. (Cela peut apparaître en tant que « Windows HOLOGRAPHIQUE » dans les versions antérieures de Unity)

Votre application peut maintenant faire base rendu holographique et entrée spatiale. Pour aller plus loin et tirer parti de certaines fonctionnalités, votre application doit déclarer les fonctionnalités appropriées dans son manifeste. Les déclarations de manifeste peuvent être rendues Unity, ils sont inclus dans chaque exportation ultérieures du projet. Le paramètre se trouvent dans **paramètres du lecteur > Paramètres de plateforme Windows universelle > Paramètres de publication > fonctionnalités**. Les fonctionnalités applicables pour l’activation des API de Unity couramment utilisés pour la réalité mixte sont :

|  Fonctionnalité  |  API nécessitant une fonctionnalité | 
|----------|----------|
|  SpatialPerception  |  SurfaceObserver (l’accès à [mappage spatial](spatial-mapping.md) maillages sur HoloLens)&mdash;*aucune fonctionnalité nécessaire pour le suivi spatial générales du casque* | 
|  WebCam  |  PhotoCapture et VideoCapture | 
|  Bibliothèque d’images / VideosLibrary  |  PhotoCapture ou VideoCapture, respectivement (lorsque vous stockez le contenu capturé) | 
|  Microphone  |  VideoCapture (lors de la capture audio), DictationRecognizer, GrammarRecognizer et KeywordRecognizer | 
|  InternetClient  |  DictationRecognizer (et à utiliser le Profiler Unity) | 

**Paramètres de qualité de Unity**

![Paramètres de qualité de Unity](images/unityqualitysettings-350px.png)<br>
*Paramètres de qualité de Unity*

HoloLens a un GPU mobile-classe. Si votre application cible HoloLens, vous pourrez les paramètres de qualité afin de que nous mettons en place une fréquence d’images complète est optimisés pour les performances le plus rapide :
1. Sélectionnez **Modifier > Paramètres du projet > qualité**
2. Sélectionnez le **déroulante** sous le **Windows Store** logo, puis sélectionnez **Fastest**. Vous saurez que le paramètre est correctement appliqué lorsque la zone de la colonne du Windows Store et **Fastest** ligne est verte.

### <a name="per-scene-settings"></a>Paramètres par scène

**Paramètres de la caméra Unity**

![Paramètres de la caméra Unity](images/unitycamerasettings.png)<br>
*Paramètres de la caméra Unity*

Une fois que vous activez la case à cocher « Virtuel réalité pris en charge », la [Unity caméra](camera-in-unity.md) composant handles [head de suivi et rendu stéréoscopique](rendering.md). Il est inutile de la remplacer par une caméra personnalisée pour ce faire.

Si votre application cible HoloLens plus précisément, il existe quelques paramètres qui doivent être modifiées pour optimiser les affichages transparent de l’appareil, afin de votre application s’affichera à travers le monde physique :
1. Dans le **hiérarchie**, sélectionnez le **Main Camera**
2. Dans le **inspecteur** du panneau, définissez la transformation **position** à **0, 0, 0** pour que l’emplacement de la tête utilisateurs commence à l’origine du monde Unity.
3. Modification **d’effacer les indicateurs** à **couleur unie**.
4. Modifier le **arrière-plan** couleur **RGBA 0,0,0,0**. Noir rend transparente dans HoloLens.
5. Modification **découpage plans - près** à la [HoloLens recommandé](camera-in-unity.md#clip-planes) 0,85 (mètres).

Si vous supprimez et créez un nouvel appareil photo, assurez-vous que votre appareil photo est **balisée** comme **MainCamera**.

## <a name="adding-mixed-reality-capabilities-and-inputs"></a>Ajout d’entrées et des fonctionnalités de réalité mixte

Une fois que vous avez configuré votre projet comme décrit ci-dessus, les objets de jeu Unity standards (par exemple, l’appareil photo) seront allume immédiatement pour un **assis à l’échelle du expérience**, avec la position de la caméra mis à jour automatiquement en tant que l’utilisateur déplace leur tête dans le monde.

Ajout de prise en charge des fonctionnalités de Windows Mixed Reality comme [étapes spatiales](coordinate-systems.md#spatial-coordinate-systems), [mouvements, les contrôleurs de mouvement](gestures-and-motion-controllers-in-unity.md) ou [entrée voix](voice-input-in-unity.md) est obtenue à l’aide des API directement intégré aux Unity.

La première étape doit consister pour passer en revue la [expérience échelles](coordinate-systems.md) que votre application peut cibler :
* Si vous avez besoin pour générer un **orientation seule** ou **assis à l’échelle du expérience**, vous devez définir Unity du suivi de type de l’espace à [stationnaire](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience).
* Si vous avez besoin pour générer un **permanent à l’échelle** ou **expérience de l’échelle de la salle**, vous devez vous assurer d’Unity suivi du type de l’espace est défini correctement à [RoomScale](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience).
* Si vous avez besoin pour générer un **à l’échelle du monde** expérience sur HoloLens, permettant aux utilisateurs de se déplacer au-delà de 5 mètres, vous devez utiliser le [WorldAnchor](coordinate-systems-in-unity.md#building-a-world-scale-experience) composant.

Tous les principaux blocs de construction pour les applications de réalité mixte sont exposées de manière cohérente avec d’autres API Unity :
* [Appareil photo](camera-in-unity.md)
* [Systèmes de coordonnées](coordinate-systems-in-unity.md)
* [Gaze](gaze-in-unity.md)
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
* [Principes de base MR 100 : Mise en route avec Unity](holograms-100.md)
* [Paramètres recommandés pour Unity](recommended-settings-for-unity.md)
* [Recommandations relatives aux performances pour Unity](performance-recommendations-for-unity.md)
* [Exportation et création d’une solution de Unity Visual Studio](exporting-and-building-a-unity-visual-studio-solution.md)
* [À l’aide de l’espace de noms Windows avec les applications Unity pour HoloLens](using-the-windows-namespace-with-unity-apps-for-hololens.md)
* [Meilleures pratiques pour travailler avec Unity et Visual Studio](best-practices-for-working-with-unity-and-visual-studio.md)
* [Mode de jeu Unity](unity-play-mode.md)
* [Portage des repères](porting-guides.md)
