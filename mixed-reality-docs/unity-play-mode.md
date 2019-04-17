---
title: Mode de jeu Unity
description: Utilise le Mode de lecture dans l’éditeur Unity pour prévisualiser vos modifications sur un appareil sans déploiement d’une application.
author: JonMLyons
ms.author: jlyons
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, communication à distance, communication à distance HOLOGRAPHIQUE, lecteur de communication à distance HOLOGRAPHIQUE
ms.openlocfilehash: c118c4af61c6eb2706ef851a6654c18ff7313453
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593355"
---
# <a name="unity-play-mode"></a>Mode de jeu Unity

Un moyen rapide pour travailler sur votre projet Unity consiste à utiliser le « Mode de lecture ». Il s’exécute votre application localement dans l’éditeur Unity sur votre PC. Unity utilise holographique de communication à distance pour fournir un moyen rapide pour afficher un aperçu de votre contenu sur un appareil HoloLens réel.

## <a name="unity-play-mode-with-holographic-remoting"></a>Mode de jeu Unity avec Remoting HOLOGRAPHIQUE

Avec la communication à distance HOLOGRAPHIQUE, vous pouvez tester votre application sur le HoloLens, pendant son exécution dans l’éditeur Unity sur votre PC. Regards, mouvement, voix et entrée de mappage spatial est envoyé à partir de votre HoloLens à votre PC. Restituées sont ensuite renvoyées à votre HoloLens. Il s’agit d’un excellent moyen de déboguer rapidement votre application sans générer et déployer un projet complet.
1. Sur votre HoloLens, accédez à la **Microsoft Store** et installer le **[HOLOGRAPHIQUE Player de communication à distance](https://www.microsoft.com/store/p/holographic-remoting-player/9nblggh4sv40)** application.
2. Sur votre HoloLens, démarrez le **HOLOGRAPHIQUE Player de communication à distance** application.
3. Dans Unity, accédez à la **fenêtre** menu et sélectionnez **émulation HOLOGRAPHIQUE**.
4. Définissez **Mode d’émulation** à **à distance au périphérique**.
5. Pour **Machine distante**, entrez l’adresse IP de votre HoloLens.
6. Cliquer sur **Se connecter**. Vous devriez voir **état de la connexion** modifier à **connecté** et voir l’écran vide dans le HoloLens.
7. Cliquez sur le **lire** bouton pour démarrer le Mode de lecture et l’expérience de l’application sur votre HoloLens.

Remoting HOLOGRAPHIQUE requiert une connexion rapide de PC et Wi-Fi. Consultez [HOLOGRAPHIQUE Player de communication à distance](holographic-remoting-player.md) pour plus d’informations.

Pour de meilleurs résultats, assurez-vous que votre application définit correctement le [concentrer point](focus-point-in-unity.md). Cela permet une communication à distance HOLOGRAPHIQUE pour mieux adapter votre scène à la latence de votre connexion sans fil.

## <a name="see-also"></a>Voir aussi
* [Lecteur de communication à distance HOLOGRAPHIQUE](holographic-remoting-player.md)
