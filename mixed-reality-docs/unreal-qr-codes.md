---
title: Codes QR dans Unreal
description: Guide pour utiliser les codes QR dans Unreal
author: hferrone
ms.author: v-haferr
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, codes qr
ms.openlocfilehash: 90a51227ae455389168fb3262e83f34b64a7bfb5
ms.sourcegitcommit: ee7f04148d3608b0284c59e33b394a67f0934255
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428755"
---
# <a name="qr-codes-in-unreal"></a>Codes QR dans Unreal

## <a name="overview"></a>Vue d’ensemble

HoloLens 2 peut voir les codes QR dans l’espace universel à travers la webcam, qui les affiche sous forme d’hologrammes en utilisant un système de coordonnées à la position réelle de chaque code.  En plus des codes QR uniques, HoloLens 2 peut aussi afficher des hologrammes sur plusieurs appareils à la même position pour créer une expérience partagée. Veillez à suivre les bonnes pratiques pour ajouter les codes QR à vos applications :

- Zones calmes
- Éclairage et toile de fond
- Taille, distance et position angulaire

Au moment de placer les codes QR dans votre application, portez une attention particulière aux [considérations liées à l’environnement](environment-considerations-for-hololens.md). Vous trouverez des informations complémentaires sur chacun de ces sujets ainsi que des instructions sur la façon de télécharger le package NuGet nécessaire dans le document [Suivi des codes QR](qr-code-tracking.md). 

## <a name="enabling-qr-detection"></a>Activation de la détection QR
Étant donné que HoloLens 2 doit utiliser la webcam pour voir les codes QR, vous devez l’activer dans les paramètres du projet :
- Ouvrez **Edit > Project Settings**, accédez à la section **Platforms**, puis cliquez sur **HoloLens**.
    + Développez la section **Capabilities** et cochez **Webcam**.  

Vous devez aussi opter pour le suivi des codes QR en [ajoutant une ressource ARSessionConfig](https://docs.microsoft.com/windows/mixed-reality/unreal-uxt-ch3#adding-the-session-asset).

## <a name="setting-up-a-tracked-image"></a>Configuration d’une image suivie

Les codes QR sont exposés sous forme d’image suivie par le biais du système de géométrie suivie de réalité augmentée d’Unreal. Pour que cela fonctionne, vous devez :
1. Créer un blueprint et ajouter un composant **ARTrackableNotify**.

![Composant ARTrackableNotify QR](images/unreal-spatialmapping-artrackablenotify.PNG)

2. Sélectionnez **ARTrackableNotify** et développez la section **Events** dans le panneau **Details**. 

![Événements QR](images/unreal-spatialmapping-events.PNG)

3. Cliquez sur **+** à côté de **On Add Tracked Geometry** pour ajouter le nœud au graphique d’événements.
    - Vous trouverez la liste complète des événements dans l’API du composant [UARTrackableNotify](https://docs.unrealengine.com/API/Runtime/AugmentedReality/UARTrackableNotifyComponent/index.html). 

![Exemple d’affichage QR](images/unreal-qr-codes-tracked-geometry.png)

## <a name="using-a-tracked-image"></a>Utilisation d’une image suivie
Le graphique d’événements dans l’image suivante présente l’événement **OnUpdateTrackedImage** qui est utilisé pour afficher un point au centre d’un code QR et imprimer ses données. 

![Exemple d’affichage QR](images/unreal-qr-render.PNG)

Voici ce qu’il se passe :
1. Tout d’abord, l’image suivie est castée en **ARTrackedQRCode** pour vérifier que l’image mise à jour actuelle est un code QR.  
2. Les données encodées sont récupérées à partir de la variable **QRCode**. Vous pouvez obtenir l’angle supérieur gauche du code QR à partir de l’emplacement de **GetLocalToWorldTransform** et les dimensions avec **GetEstimateSize**. 

Vous pouvez aussi [obtenir le système de coordonnées pour un code QR](https://docs.microsoft.com/windows/mixed-reality/qr-code-tracking#getting-the-coordinate-system-for-a-qr-code) dans le code.

## <a name="finding-the-unique-id"></a>Recherche de l’ID unique
À chaque code QR correspond un ID guid unique, que vous pouvez trouver comme ceci :
- Glissez-déposez le repère **As ARTracked QRCode** et effectuez une recherche sur l’ID unique (**Unique ID**).

![GUID QR](images/unreal-qr-guid.PNG)

Il se passe beaucoup de choses en coulisse avec les codes QR ; ce n’est donc pas terminé. N’hésitez pas à consulter les liens ci-dessous pour en savoir plus sur la mécanique interne.

## <a name="see-also"></a>Voir aussi
* [Mappage spatial](spatial-mapping.md)
* [Hologrammes](hologram.md)
* [Systèmes de coordonnées](coordinate-systems.md)