---
title: Configurer un projet Unity pour Windows Mixed Reality
description: configurer le projet Unity sans MRTK
author: yoyoz
ms.author: Yoyoz
ms.date: 04/15/2018
ms.topic: article
keywords: Unity, mixte réalité, de développement, de mise en route, nouveau projet
ms.openlocfilehash: 4ee81eca25109da428d7b3addf59e102ddc5c5cf
ms.sourcegitcommit: aa88f6b42aa8d83e43104b78964afb506a368fb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/02/2019
ms.locfileid: "64993538"
---
# <a name="configure-a-new-unity-project-for-windows-mixed-reality"></a>Configurer un projet Unity pour Windows Mixed Reality 

(ignorez si vous avez déjà importé MRTK v2 dans votre projet Unity)

Si vous souhaitez créé un projet Unity sans importer Toolkit de réalité mixte, il existe un petit ensemble de paramètres de Unity vous devrez modifier manuellement pour Windows Mixed Reality, divisé en deux catégories : par projet et par scène.

## <a name="per-project-settings"></a>Paramètres par projet

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
2. Sélectionnez le **déroulante** sous le **Windows Store** logo, puis sélectionnez **très faible**. Vous saurez que le paramètre est correctement appliqué lorsque la zone de la colonne du Windows Store et **très faible** ligne est verte.

## <a name="per-scene-settings"></a>Paramètres par scène

**Paramètres de la caméra Unity**

![Paramètres de la caméra Unity](images/Unitycamerasettings.png)<br>
*Paramètres de la caméra Unity*

Une fois que vous activez la case à cocher « Virtuel réalité pris en charge », la [Unity caméra](camera-in-unity.md) composant handles [head de suivi et rendu stéréoscopique](rendering.md). Il est inutile de la remplacer par une caméra personnalisée pour ce faire.

Si votre application cible HoloLens plus précisément, il existe quelques paramètres qui doivent être modifiées pour optimiser les affichages transparent de l’appareil, afin de votre application s’affichera à travers le monde physique :
1. Dans le **hiérarchie**, sélectionnez le **Main Camera**
2. Dans le **inspecteur** du panneau, définissez la transformation **position** à **0, 0, 0** pour que l’emplacement de la tête utilisateurs commence à l’origine du monde Unity.
3. Modification **d’effacer les indicateurs** à **couleur unie**.
4. Modifier le **arrière-plan** couleur **RGBA 0,0,0,0**. Noir rend transparente dans HoloLens.
5. Modification **découpage plans - près** à la [HoloLens recommandé](camera-in-unity.md#clip-planes) 0,85 (mètres).

Si vous supprimez et créez un nouvel appareil photo, assurez-vous que votre appareil photo est **balisée** comme **MainCamera**.


## <a name="see-also"></a>Voir aussi
* [Une réalité mixte Toolkit v2](mrtk-getting-started.md)
* [Vue d’ensemble du développement Unity](unity-development-overview.md)
