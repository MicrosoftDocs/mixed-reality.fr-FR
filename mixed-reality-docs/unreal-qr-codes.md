---
title: Codes QR dans Unreal
description: Guide d’utilisation des codes QR dans Unreal
author: sw5813
ms.author: jacksonf
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, codes qr
ms.openlocfilehash: 67a3a8092ab908cba6768e92ed6a0e7bd2737275
ms.sourcegitcommit: 5b802078090700e06630c8fc665fedeaa0a16eb7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83342657"
---
# <a name="qr-codes-in-unreal"></a>Codes QR dans Unreal

HoloLens peut localiser les codes QR dans l’espace universel afin d’afficher des hologrammes à des positions connues dans le monde réel.  Cela permet également d’afficher des hologrammes sur plusieurs appareils à la même position pour créer une expérience partagée. 

Pour activer la détection QR sur HoloLens, vérifiez que la fonctionnalité « Webcam » est cochée dans l’éditeur Unreal sous Project Settings > Platform > HoloLens > Capabilities.  

Acceptez l’utilisation du suivi des codes QR dans Unreal en démarrant une ARSession avec la fonction StartARSession. 

Les codes QR sont exposés sous forme d’image suivie par le biais du système de géométrie suivie AR dans Unreal.  Pour utiliser cette fonctionnalité, ajoutez un composant ARTrackableNotify à un acteur Blueprint : 

![Composant ARTrackableNotify QR](images/unreal-spatialmapping-artrackablenotify.PNG)

Ensuite, accédez aux détails du composant et cliquez sur le bouton « + » vert dans les événements à surveiller.  

![Événements QR](images/unreal-spatialmapping-events.PNG)

Ici, nous avons un abonnement à OnUpdateTrackedImage pour afficher un point au centre d’un code QR et imprimer les données encodées du code QR. 

![Exemple d’affichage QR](images/unreal-qr-render.PNG)

Tout d’abord, convertissez l’image suivie en ARTrackedQRCode pour vérifier que l’image mise à jour actuelle est un code QR.  Les données encodées peuvent ensuite être récupérées avec la variable QRCode.  La partie en haut à gauche du code QR peut être récupérée de la position de GetLocalToWorldTransform.  Les dimensions peuvent être récupérées avec GetEstimateSize. 

Par ailleurs, chaque code QR a un identificateur GUID unique : 

![GUID QR](images/unreal-qr-guid.PNG)

## <a name="see-also"></a>Voir également
* [Suivi des codes QR](qr-code-tracking.md)
