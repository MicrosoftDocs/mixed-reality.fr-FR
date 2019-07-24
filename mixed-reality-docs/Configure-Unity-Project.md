---
title: Configurer un nouveau projet Unity pour Windows Mixed Reality
description: configurer un projet Unity sans MRTK
author: yoyoz
ms.author: Yoyoz
ms.date: 04/15/2018
ms.topic: article
keywords: Unity, réalité mixte, développement, prise en main, nouveau projet
ms.openlocfilehash: 68dded9d0fc9e861bdda56c4954d72ddafafa686
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67326093"
---
# <a name="configure-a-new-unity-project-for-windows-mixed-reality"></a>Configurer un nouveau projet Unity pour Windows Mixed Reality 

(ignorer si vous avez déjà importé MRTK v2 dans votre projet Unity)

Si vous souhaitez créer un nouveau projet Unity sans importer la boîte à outils de réalité mixte, il existe un petit ensemble de paramètres Unity que vous devrez modifier manuellement pour Windows Mixed Reality, répartis en deux catégories: par projet et par scène.

## <a name="per-project-settings"></a>Paramètres par projet

Pour cibler Windows Mixed Reality, vous devez d’abord définir votre projet Unity pour l’exporter en tant qu’application plateforme Windows universelle: 
1. Sélectionner le **fichier > les paramètres de Build...**
2. Sélectionnez **plateforme Windows universelle** dans la liste plateforme, puis cliquez sur **changer de plateforme** .
3. Définir le **Kit de développement logiciel** sur **Universal 10**
4. Définir un appareil **cible** sur **un appareil** pour prendre en charge les casques immersifs ou basculer vers **HoloLens**
5. Définir le **type de build** sur **D3D**
6. Définir le **SDK UWP** sur le **dernier installé**

Nous devons ensuite permettre à Unity de savoir que l’application que nous essayons d’exporter doit créer un [affichage immersif](app-views.md) au lieu d’une vue 2D. Pour cela, vous devez activer la «réalité virtuelle prise en charge»:
1. Dans la fenêtre **paramètres de Build...** , ouvrez paramètres du **lecteur...**
2. Sélectionner les **paramètres de plateforme Windows universelle** onglet
3. Développez le groupe de **paramètres XR**
4. Dans la section **paramètres XR** , activez la case à cocher **Virtual Reality pris en charge** pour ajouter la liste des **appareils Virtual Reality** .
5. Dans le groupe de **paramètres XR** , vérifiez que **«Windows Mixed Reality»** est listé comme périphérique pris en charge. (cela peut s’afficher sous la forme «Windows holographique» dans les versions antérieures d’Unity)

![Paramètres de qualité Unity](images/getting-started-unity-quality-settings.jpg)<br>
*Paramètres XR Unity*

Votre application peut désormais effectuer un rendu holographique de base et une entrée spatiale. Pour aller plus loin et tirer parti de certaines fonctionnalités, votre application doit déclarer les fonctionnalités appropriées dans son manifeste. Les déclarations de manifeste peuvent être effectuées dans Unity afin qu’elles soient incluses dans chaque exportation de projet suivante. Le paramètre se trouve dans les paramètres du **lecteur > paramètres pour plateforme Windows universelle > paramètres de publication >** . Les fonctionnalités applicables à l’activation des API Unity couramment utilisées pour la réalité mixte sont les suivantes:

|  Fonctionnalité  |  API nécessitant des fonctionnalités | 
|----------|----------|
|  SpatialPerception  |  SurfaceObserver (accès aux maillages de [mappage spatial](spatial-mapping.md) sur HoloLens&mdash;)*aucune fonctionnalité nécessaire pour le suivi spatial général du casque* | 
|  WebCam  |  PhotoCapture et VideoCapture | 
|  PicturesLibrary/VideosLibrary  |  PhotoCapture ou VideoCapture, respectivement (lors du stockage du contenu capturé) | 
|  Microphone  |  VideoCapture (lors de la capture de l’audio), DictationRecognizer, GrammarRecognizer et KeywordRecognizer | 
|  InternetClient  |  DictationRecognizer (et pour utiliser le profileur Unity) | 

**Paramètres de qualité Unity**

![Paramètres de qualité Unity](images/getting-started-unity-quality-settings.jpg)<br>
*Paramètres de qualité Unity*

HoloLens possède un GPU de classe mobile. Si votre application cible HoloLens, vous souhaiterez que les paramètres de qualité soient réglés pour des performances plus rapides afin de garantir que nous maintenons une cadence complète:
1. Sélectionnez **modifier > paramètres du projet > qualité**
2. Sélectionnez la **liste** déroulante sous le logo du **Windows Store** et sélectionnez **très faible**. Vous saurez que le paramètre est appliqué correctement lorsque la zone de la colonne du Windows Store et la ligne **très basse** est verte.

## <a name="per-scene-settings"></a>Paramètres par scène

**Paramètres de l’appareil photo Unity**

![Paramètres de l’appareil photo Unity](images/Unitycamerasettings.png)<br>
*Paramètres de l’appareil photo Unity*

Une fois que vous activez la case à cocher «réalité virtuelle prise en charge», le composant [appareil photo Unity](camera-in-unity.md) gère le [suivi des têtes et le rendu stéréoscopique](rendering.md). Pour ce faire, il est inutile de la remplacer par une caméra personnalisée.

Si votre application cible en particulier HoloLens, il y a quelques paramètres qui doivent être modifiés pour optimiser les affichages transparents de l’appareil, de sorte que votre application s’affichera dans le monde physique:
1. Dans la **hiérarchie**, sélectionnez l' **appareil photo principal** .
2. Dans le panneau **inspecteur** , définissez la **position** de la transformation sur **0, 0, 0** de sorte que l’emplacement de la tête des utilisateurs commence à l’origine Unity World.
3. Remplacez **effacer les indicateurs** par **couleur unie**.
4. Remplacez la couleur d' **arrière-plan** par **RVBA 0, 0,** 0, 0. Le rendu noir est transparent dans HoloLens.
5. Modifiez les plans de découpage **-près** de [HoloLens recommandé](camera-in-unity.md#clip-planes) 0,85 (mètres).

Si vous supprimez et créez un nouvel appareil photo, vérifiez que votre appareil photo est **marqué** comme **MainCamera**.


## <a name="see-also"></a>Voir aussi
* [Boîte à outils de réalité mixte v2](mrtk-getting-started.md)
* [Vue d’ensemble du développement Unity](unity-development-overview.md)
