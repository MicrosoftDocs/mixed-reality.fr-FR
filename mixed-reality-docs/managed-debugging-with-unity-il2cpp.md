---
title: Le débogage avec Unity IL2CPP managé
description: Cet article explique comment exécuter un débogueur managé sur votre projet Unity IL2CPP UWP.
author: keveleigh
ms.author: kurtie
ms.date: 06/13/19
ms.topic: article
keywords: Unity, il2cpp, de débogage de visual studio
ms.openlocfilehash: eb4655633384fcb5d7f27546134e21857e5c5502
ms.sourcegitcommit: 2f600e5ad00cd447b180b0f89192b4b9d86bbc7e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148854"
---
# <a name="managed-debugging-with-unity-il2cpp"></a>Le débogage avec Unity IL2CPP managé

Suivez ces étapes pour attacher un débogueur managé à votre build Unity IL2CPP UWP. Ce guide a été développé pour HoloLens et HoloLens 2.

1. Vérifiez que **InternetClientServer** et **PrivateNetworkClientServer** sont vérifiées dans Unity sous les fonctionnalités de paramètres de publication UWP.

    ![UWP des fonctionnalités de paramètres de publication](images/il2cpp-debugging-capabilities.png)

1. Configurez les paramètres de build Unity UWP :
    - Génération de développement
    - Débogage des scripts
    - Attendez le débogueur géré (facultatif)

    ![Paramètres de Build UWP](images/il2cpp-debugging-build.png)

1. Build dans Unity.
1. Générer et déployer à partir de la solution Visual Studio sur votre appareil. Vous devez créer avec le **déboguer** ou **version** configurations. Le **Master** configuration désactive le profileur Unity et peut empêcher le débogage optimale. Si vous le souhaitez, vérifiez **Internet (Client & serveur)** et **réseaux privés (Client & serveur)** dans la liste de fonctionnalités dans Package.appxmanifest dans la solution.
1. Démarrer l’application sur votre appareil. Assurez-vous que votre appareil est connecté au même réseau que votre PC.
1. Assurez-vous que l’appareil **n’est pas** connecté à votre PC via une connexion USB.
1. Accédez à la solution Visual Studio qui est créée lorsque vous double-cliquez sur un script dans Unity, où vous pouvez afficher et modifier votre C# scripts.
1. Déboguer -> attacher le débogueur Unity.

    ![Attacher le débogueur Unity](images/il2cpp-debugging-attach.png)

1. Sélectionnez votre appareil dans la liste et cliquez sur « OK » à attacher.

    ![Liste des appareils](images/il2cpp-debugging-machines.png)
