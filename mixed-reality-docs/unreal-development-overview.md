---
title: Vue d’ensemble du développement Unreal
description: Commencez à créer des applications de réalité mixte dans Unreal.
author: sw5813
ms.author: suwu
ms.date: 10/24/2019
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, bêta, streaming, communication à distance, réalité mixte, développement, bien démarrer, nouveau projet, émulateur, documentation
ms.openlocfilehash: 96b0259e4ac567389f999d3a453fb68bb848b266
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "74491172"
---
# <a name="unreal-development-overview"></a>Vue d’ensemble du développement Unreal

La prise en charge de la réalité mixte pour Unreal Engine 4 est maintenant en version bêta. Si vous n’avez jamais utilisé Unreal pour développer des applications, découvrez comment <a href="https://docs.unrealengine.com//GettingStarted/index.html" target="_blank">bien démarrer avec Unreal Engine 4</a>. Si vous avez besoin de ressources, Unreal propose une <a href="https://www.unrealengine.com/marketplace//store" target="_blank">place de marché</a> complète. 

Une fois que vous avez acquis des connaissances de base sur Unreal Engine 4, visitez la page consacrée au <a href="https://docs.unrealengine.com//Platforms/AR/HoloLens2/index.html" target="_blank">développement pour Microsoft HoloLens</a> sur le site de la documentation Unreal Engine pour apprendre à créer et à exécuter des applications sur HoloLens. N’hésitez pas à consulter les <a href="https://forums.unrealengine.com/development-discussion/vr-ar-development" target="_blank">forums Unreal</a> pour dialoguer avec des membres de la communauté qui créent des applications de réalité mixte dans Unreal. C’est l’endroit idéal pour trouver des solutions aux problèmes que vous pouvez rencontrer.

## <a name="installing-the-prerequisites"></a>Installation des prérequis

Pour commencer à créer une application HoloLens 2 dans Unreal, vous avez besoin de l’[émulateur HoloLens 2](using-the-hololens-emulator.md) ou d’un casque HoloLens. Vous devez également installer la dernière version de Visual Studio avec les charges de travail et les composants listés dans les <a href="https://docs.unrealengine.com//Platforms/AR/HoloLens2/Prerequisites/index.html" target="_blank">prérequis HoloLens 2 pour Unreal</a>.

## <a name="building-and-running-your-unreal-app"></a>Création et exécution de votre application Unreal

Commencez par <a href="https://docs.unrealengine.com//Platforms/AR/HoloLens2/HowTo/PackageApp/index.html" target="_blank">créer un package de votre application pour HoloLens 2</a>. Choisissez ensuite où déployer votre package :
* <a href="https://docs.unrealengine.com//Platforms/AR/HoloLens2/QuickStartEmulator/index.html" target="_blank">Déployer sur l’émulateur HoloLens 2</a>
* <a href="https://docs.unrealengine.com//Platforms/AR/HoloLens2/QuickStartDevice/index.html" target="_blank">Déployer sur un casque HoloLens 2</a>

## <a name="streaming-your-app-to-a-headset-via-the-holographic-remoting-player"></a>Diffusion en streaming de votre application sur un casque via l’application Holographic Remoting Player

La diffusion en streaming d’une application de votre appareil de bureau sur l’application Holographic Remoting Player d’un casque HoloLens présente deux avantages principaux : 
* Accélère le développement. Il est inutile de recréer un package et de charger votre application chaque fois que vous apportez une modification.
* Tire parti de la puissance de votre appareil de bureau. Vous pouvez afficher autant de polygones que votre processeur graphique le permet, sans être limité par l’ordinateur disponible sur le casque.

Pour vous familiariser avec la diffusion en streaming, consultez le <a href="https://docs.unrealengine.com//Platforms/AR/HoloLens2/QuickStartStreaming/index.html" target="_blank">guide de démarrage rapide de la diffusion en streaming sur HoloLens 2</a>[]().

## <a name="see-also"></a>Voir aussi
* <a href="https://docs.unrealengine.com//Platforms/Mobile/Performance/index.html" target="_blank">Conseils d’optimisation des performances sur les appareils mobiles avec Unreal</a>
