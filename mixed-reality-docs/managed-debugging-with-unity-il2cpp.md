---
title: Débogage managé avec Unity IL2CPP
description: Cet article explique comment exécuter un débogueur géré sur votre projet UWP IL2CPP Unity.
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: Unity, Visual Studio, débogage, il2cpp
ms.openlocfilehash: 970d3000df995e7c6e331a41d10e25dc5aa370a8
ms.sourcegitcommit: 7e8b9de561cbc8483e84511f3e9cbd779f3a999f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/27/2019
ms.locfileid: "75502660"
---
# <a name="managed-debugging-with-unity-il2cpp"></a>Débogage managé avec Unity IL2CPP

Procédez comme suit pour attacher un débogueur géré à votre Build IL2CPP Unity. Ce guide a été développé à l’origine pour HoloLens et HoloLens 2.

1. Vous devez disposer d’un réseau qui prend en charge la [multidiffusion](https://en.wikipedia.org/wiki/Multicast).
1. Assurez-vous que **InternetClientServer** et **PrivateNetworkClientServer** sont archivés dans Unity sous les fonctionnalités des paramètres de publication UWP.

    ![Fonctionnalités des paramètres de publication UWP](images/il2cpp-debugging-capabilities.png)

1. Configurer les paramètres de build UWP Unity :
    - Development Build
    - Débogage des scripts
    - Attendre le débogueur managé (facultatif)

    ![Paramètres de build UWP](images/il2cpp-debugging-build.png)

1. Créez dans Unity.
1. Générez et déployez à partir de la solution Visual Studio sur votre appareil. Vous devez générer avec les configurations **Debug** ou **Release** . La configuration **principale** désactive le profileur Unity et peut empêcher le débogage optimal. Si vous le souhaitez, vérifiez **Internet (client & Server)** et les **réseaux privés (client & Server)** dans la liste des fonctionnalités dans package. appxmanifest dans la solution.
1. Démarrez l’application sur votre appareil. Assurez-vous que votre appareil est connecté au même réseau que votre ordinateur.
1. Assurez-vous que l’appareil **n’est pas** connecté à votre ordinateur via USB.
1. Accédez à la solution Visual Studio qui est créée lorsque vous double-cliquez sur un script dans Unity, où vous pouvez afficher et C# modifier vos scripts.
1. Debug-> attacher le débogueur Unity.

    ![Attacher le débogueur Unity](images/il2cpp-debugging-attach.png)

1. Sélectionnez votre appareil dans la liste et cliquez sur OK pour l’attacher.

    ![Liste des appareils](images/il2cpp-debugging-machines.png)
