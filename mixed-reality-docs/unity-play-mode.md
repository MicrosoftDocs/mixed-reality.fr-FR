---
title: Mode de lecture Unity
description: Utilisation du mode lecture dans l’éditeur Unity pour afficher un aperçu de vos modifications sur un appareil sans déployer une application.
author: jonmlyons
ms.author: jlyons
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, communication à distance, communication à distance holographique, lecteur de communication à distance holographique
ms.openlocfilehash: dca7ffba1270802fcabed8a88fe7428ef2981553
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81277557"
---
# <a name="unity-play-mode"></a>Mode de lecture Unity

Un moyen rapide de travailler sur votre projet Unity consiste à utiliser le « mode lecture ». Cela exécute votre application localement dans l’éditeur Unity sur votre PC. Unity utilise la communication à distance holographique pour offrir un moyen rapide d’afficher un aperçu de votre contenu sur un appareil HoloLens réel. Le mode lecture peut également être utilisé avec un casque Windows Mixed Reality attaché à votre PC de développement.

## <a name="unity-play-mode-with-holographic-remoting"></a>Mode de lecture Unity avec accès distant holographique

Avec la communication à distance holographique, vous pouvez expérimenter votre application sur le HoloLens, pendant qu’elle s’exécute dans l’éditeur Unity sur votre PC. L’entrée de pointage, de mouvement, de voix et de mappage spatial est envoyée de votre HoloLens à votre PC. Les frames rendus sont ensuite renvoyés à votre HoloLens. C’est un excellent moyen de déboguer rapidement votre application sans générer et déployer un projet complet.
1. Sur votre HoloLens, accédez à la **Microsoft Store** et installez l’application de **[lecteur de communication à distance holographique](https://www.microsoft.com/store/p/holographic-remoting-player/9nblggh4sv40)** .
2. Sur votre HoloLens, démarrez l’application de **lecteur de communication à distance holographique** .
3. Dans Unity, accédez au menu **fenêtre** et sélectionnez **émulation holographique**.
4. Définissez le **mode d’émulation** à **distant sur appareil**.
5. Pour **ordinateur distant**, entrez l’adresse IP de votre HoloLens.
6. Cliquez sur **Se connecter**. Le changement d' **État** de la connexion doit être défini sur **connecté** et l’écran s’affichera vide dans HoloLens.
7. Cliquez sur le bouton **lecture** pour démarrer le mode lecture et tester l’application sur votre HoloLens.

La communication à distance holographique requiert une connexion rapide PC et Wi-Fi. Pour plus d’informations, consultez [lecteur de communication à distance holographique](holographic-remoting-player.md) .

Pour de meilleurs résultats, assurez-vous que votre application définit correctement le [point de focus](focus-point-in-unity.md). Cela permet à la communication à distance holographique d’adapter au mieux votre scène à la latence de votre connexion sans fil.

## <a name="see-also"></a>Voir aussi
* [Holographic Remoting Player](holographic-remoting-player.md)
