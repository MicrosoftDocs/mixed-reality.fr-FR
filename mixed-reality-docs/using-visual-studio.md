---
title: Utilisation de Visual Studio pour le déploiement et le débogage
description: Découvrez comment créer, déboguer et déployer des applications pour HoloLens et Windows Mixed Reality avec Visual Studio.
author: pbarnettms
ms.author: pbarnett
ms.date: 04/13/2020
ms.topic: article
ms.localizationpriority: high
keywords: Visual Studio, HoloLens, Mixed Reality, déboguer, déployer
ms.openlocfilehash: 8708ca39460fbd381bd41f5887e1276291f48b07
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "81484319"
---
# <a name="using-visual-studio-to-deploy-and-debug"></a>Utilisation de Visual Studio pour le déploiement et le débogage

Que vous choisissiez de développer votre application de réalité mixte dans DirectX ou dans Unity, vous utiliserez Visual Studio pour son débogage et son déploiement. Dans cette section, vous allez découvrir comment :
* Déployer des applications sur votre HoloLens ou un casque immersif Windows Mixed Reality à l’aide de Visual Studio.
* Utiliser l’émulateur HoloLens intégré à Visual Studio.
* Déboguer des applications de réalité mixte.

## <a name="prerequisites"></a>Prérequis
1. Consultez [Installer les outils](install-the-tools.md) pour obtenir des instructions d’installation.
2. Créez un projet d’application Windows universelle dans Visual Studio.  Pour HoloLens (1re génération), utilisez Visual Studio 2017 ou une version plus récente.  Pour HoloLens 2, utilisez Visual Studio 2019 version 16.2 ou ultérieure. Les langages C# et C++ sont pris en charge. (Ou suivez les instructions pour [créer une application dans Unity](holograms-100.md).)

## <a name="enabling-developer-mode"></a>Activation du mode développeur

Commencez par activer le **mode développeur** sur votre appareil afin que Visual Studio puisse s’y connecter.

### <a name="hololens"></a>HoloLens
1. Mettez HoloLens sous tension et allumez l’appareil.
2. Effectuez le [mouvement de démarrage](system-gesture.md) pour lancer le menu principal.
3. Sélectionnez la vignette **Settings** pour lancer l’application dans votre environnement.
4. Sélectionnez l’élément de menu **Mettre à jour**.
5. Sélectionnez l’élément de menu **Pour les développeurs**.
6. Activez **Mode développeur**. Ce mode vous permet de [déployer des applications à partir de Visual Studio](using-visual-studio.md) sur votre HoloLens.
7. Facultatif : Faites défiler la page et activez également le **portail d’appareil**. Cela vous permettra également de vous connecter au [portail d’appareil Windows](using-the-windows-device-portal.md) sur votre HoloLens à partir d’un navigateur web.

### <a name="windows-pc"></a>PC Windows

Si vous travaillez avec un casque Windows Mixed Reality connecté à votre PC, vous devez activer le **mode développeur** sur ce PC.
1. Accédez à **Paramètres**
2. Sélectionnez **Mise à jour et sécurité**
3. Sélectionnez **Pour les développeurs**
4. Activez le **mode développeur**, lisez la clause d’exclusion de responsabilité pour le paramètre que vous avez choisi, puis cliquez sur Oui pour accepter la modification.

## <a name="deploying-an-app-over-wi-fi---hololens-1st-gen"></a>Déploiement d’une application via une connexion WiFi - HoloLens (1re génération)
1. Sélectionnez une configuration de build **x86** pour votre application</br>
![Configuration de build x86 dans Visual Studio](images/x86setting.png)</br>
2. Sélectionnez **Machine distante** dans le menu déroulant de la cible de déploiement</br>
![Cible de déploiement de machine distante dans Visual Studio](images/remotemachinesetting.png)</br>
3. Pour les projets C++ et JavaScript, accédez à **Projet > Propriétés > Propriétés de configuration > Débogage**. Pour les projets C#, une boîte de dialogue s’affiche automatiquement, dans laquelle vous pouvez configurer votre connexion.
  a. Entrez l’adresse IP de votre appareil dans le champ **Adresse** ou **Nom de la machine**. Recherchez l’adresse IP sur votre HoloLens sous **Paramètres > Réseau et Internet > Options avancées**, ou demandez à Cortana « Quelle est mon adresse IP ? ».
  b. Définir le mode d’authentification sur **Universel (protocole non chiffré)**</br>
  ![Boîte de dialogue Connexion à distance dans Visual Studio](images/remotedeploy.png)</br>
4. Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et commencer le débogage</br>
![Démarrer sans débogage dans Visual Studio](images/deploywithdebugging.png)</br>
5. La première fois que vous déployez une application sur votre HoloLens à partir de votre PC, vous êtes invité à entrer un code PIN. Suivez les instructions de la section **Appairer votre appareil**, plus loin dans cet article.

## <a name="deploying-an-app-over-wi-fi---hololens-2"></a>Déploiement d’une application via une connexion WiFi - HoloLens 2
1. Sélectionnez une configuration de build **ARM** ou **ARM64** pour votre application</br>
![Configuration de build ARM64 dans Visual Studio](images/arm64setting.png)</br>
2. Sélectionnez **Machine distante** dans le menu déroulant de la cible de déploiement</br>
![Cible de déploiement de machine distante dans Visual Studio](images/remotemachinesetting_arm64.png)</br>
3. Pour les projets C++ et JavaScript, accédez à **Projet > Propriétés > Propriétés de configuration > Débogage**. Pour les projets C#, une boîte de dialogue s’affiche automatiquement, dans laquelle vous pouvez configurer votre connexion.
  a. Entrez l’adresse IP de votre appareil dans le champ **Adresse** ou **Nom de la machine**. Recherchez l’adresse IP sur votre HoloLens sous **Paramètres > Réseau et Internet > Options avancées**, ou demandez à Cortana « Quelle est mon adresse IP ? ».
  b. Définir le mode d’authentification sur **Universel (protocole non chiffré)**</br>
  ![Boîte de dialogue Connexion à distance dans Visual Studio](images/remotedeploy.png)</br>
4. Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et commencer le débogage</br>
![Démarrer sans débogage dans Visual Studio](images/deploywithdebugging.png)</br>
5. La première fois que vous déployez une application sur votre HoloLens à partir de votre PC, vous êtes invité à entrer un code PIN. Suivez les instructions de la section **Appairer votre appareil**, plus loin dans cet article.

Si l’adresse IP de votre HoloLens change, vous pouvez changer l’adresse IP de la machine cible à partir de **Projet > Propriétés > Propriétés de configuration > Débogage**

## <a name="deploying-an-app-over-usb---hololens-1st-gen"></a>Déploiement d’une application via une connexion USB - HoloLens (1re génération)
1. Sélectionnez une configuration de build **x86** pour votre application</br>
![Configuration de build x86 dans Visual Studio](images/x86setting.png)</br>
2. Sélectionnez **Appareil** dans le menu déroulant de la cible de déploiement</br>
![Déploiement d’appareils dans Visual Studio](images/buildsettingsusbdeploy.png)</br>
3. Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et commencer le débogage</br>
![Démarrer sans débogage dans Visual Studio](images/deploywithdebugging.png)</br>
4. La première fois que vous déployez une application sur votre HoloLens à partir de votre PC, vous êtes invité à entrer un code PIN. Suivez les instructions de la section **Appairer votre appareil**, plus loin dans cet article.

## <a name="deploying-an-app-over-usb---hololens-2"></a>Déploiement d’une application via une connexion USB - HoloLens 2

>[!VIDEO https://channel9.msdn.com/Shows/Docs-Mixed-Reality/Deploying-your-HoloLens-2-application/player?format=ny]

1. Sélectionnez une configuration de build **ARM** ou **ARM64** pour votre application</br>
![Configuration de build ARM64 dans Visual Studio](images/arm64setting.png)</br>
2. Sélectionnez **Appareil** dans le menu déroulant de la cible de déploiement</br>
![Déploiement d’appareils dans Visual Studio](images/buildsettingsusbdeploy_arm64.png)</br>
3. Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et commencer le débogage</br>
![Démarrer sans débogage dans Visual Studio](images/deploywithdebugging.png)</br>
4. La première fois que vous déployez une application sur votre HoloLens à partir de votre PC, vous êtes invité à entrer un code PIN. Suivez les instructions de la section **Appairer votre appareil**, plus loin dans cet article.

## <a name="deploying-an-app-to-your-local-pc---immersive-headset"></a>Déploiement d’une application sur votre PC local - Casque immersif

Suivez ces instructions si vous utilisez un casque immersif Windows Mixed Reality qui est connecté à votre PC ou au [simulateur Mixed Reality](using-the-windows-mixed-reality-simulator.md). Dans ces deux cas, il vous suffit de déployer et d’exécuter votre application sur le PC local.
1. Sélectionnez une configuration de build **x86** ou **x64** pour votre application
2. Sélectionnez **Machine locale** dans le menu déroulant de la cible de déploiement
3. Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et commencer le débogage

## <a name="pairing-your-device"></a>Appairage de votre appareil

La première fois que vous déployez une application sur votre HoloLens à partir de Visual Studio, vous êtes invité à entrer un code PIN. Sur votre HoloLens, générez un code PIN en lançant l’application Paramètres, en accédant à **Mise à jour > Pour les développeurs** et en appuyant sur **Coupler**. Un code PIN s’affiche sur votre HoloLens. Tapez ce code PIN dans Visual Studio. Une fois l’appairage terminé, appuyez sur **Terminé** sur votre HoloLens pour fermer la boîte de dialogue. Ce PC étant maintenant appairé avec votre HoloLens, vous pouvez y déployer des applications automatiquement. Répétez ces étapes pour chaque autre PC qui est utilisé pour déployer des applications sur votre HoloLens.

Pour annuler l’appairage de votre HoloLens avec tous les ordinateurs avec lesquels il a été appairé, lancez l’application **Paramètres**, accédez à **Mise à jour > Pour les développeurs** et appuyez sur **Effacer**.

## <a name="deploying-an-app-to-the-hololens-1st-gen-emulator"></a>Déploiement d’une application sur l’émulateur HoloLens (1re génération)
1. Vérifiez que **[l’émulateur HoloLens est installé](install-the-tools.md)** .
2. Sélectionnez une configuration de build **x86** pour votre application</br>
![Configuration de build x86 dans Visual Studio](images/x86setting.png)</br>
3. Sélectionnez **Émulateur HoloLens** dans le menu déroulant de la cible de déploiement</br>
![Cible de l’émulateur dans Visual Studio](images/deployemulator.png)</br>
4. Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et commencer le débogage</br>
![Démarrer sans débogage dans Visual Studio](images/deploywithdebugging.png)</br>

## <a name="deploying-an-app-to-the-hololens-2-emulator"></a>Déploiement d’une application sur l’émulateur HoloLens 2
1. Vérifiez que **[l’émulateur HoloLens est installé](install-the-tools.md)** .
2. Sélectionnez une configuration de build **x86** ou **x64** pour votre application</br>
![Configuration de build x86 dans Visual Studio](images/x86setting.png)</br>
3. Sélectionnez **Émulateur HoloLens 2** dans le menu déroulant de la cible de déploiement</br>
![Cible de l’émulateur dans Visual Studio](images/deployemulator2.png)</br>
4. Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et commencer le débogage</br>
![Démarrer sans débogage dans Visual Studio](images/deploywithdebugging.png)</br>

## <a name="graphics-debugger-for-hololens-1st-gen"></a>Débogueur Graphics pour HoloLens (1re génération)

Les outils Graphics Diagnostics de Visual Studio sont très utiles quand vous créez et optimisez une application holographique. Pour plus d’informations, consultez [Visual Studio Graphics Diagnostics sur MSDN](https://msdn.microsoft.com/library/hh315751.aspx).

**Pour démarrer le débogueur Graphics**
1. Suivez les instructions données plus haut pour cibler un appareil ou un émulateur
2. Accédez à **Déboguer > Graphics > Démarrer les diagnostics**
3. La première fois que vous effectuez cette opération avec un HoloLens, vous pouvez obtenir une erreur « Accès refusé ». Redémarrez votre HoloLens pour que les autorisations mises à jour prennent effet, puis réessayez.

## <a name="profiling"></a>Profilage

Les outils de profilage dans Visual Studio vous permettent d’analyser l’utilisation des ressources et les performances de votre application. Ces outils comprennent des outils pour optimiser l’utilisation du processeur, de la mémoire, des graphiques et du réseau. Pour plus d’informations, consultez [Exécuter les outils de diagnostic sans débogage sur MSDN](https://msdn.microsoft.com/library/dn957936.aspx).

**Pour démarrer les outils de profilage avec HoloLens**
1. Suivez les instructions données plus haut pour cibler un appareil ou un émulateur
2. Accédez à **Déboguer > Démarrer les outils de diagnostic sans débogage...**
3. Sélectionnez les outils que vous souhaitez utiliser
4. Cliquez sur **Démarrer**
5. La première fois que vous effectuez cette opération avec un HoloLens, vous pouvez obtenir une erreur « Accès refusé ». Redémarrez votre HoloLens pour que les autorisations mises à jour prennent effet, puis réessayez.

## <a name="debugging-an-installed-or-running-app"></a>Débogage d’une application installée ou en cours d’exécution

Vous pouvez utiliser Visual Studio pour déboguer une application Windows universelle installée sans déploiement à partir d’un projet Visual Studio. Cela est utile si vous souhaitez déboguer un package d’application installé ou déboguer une application en cours d’exécution.
1. Accédez à **Déboguer -> Autres cibles de débogage -> Déboguer le package d’application installé**
2. Sélectionnez la cible **Machine distante** pour HoloLens ou **Machine locale** pour les casques immersifs
3. Entrez l’**adresse IP** de votre appareil
4. Choisissez le mode d’authentification **Universel**
5. La fenêtre affiche les applications en cours d’exécution et les applications inactives. Sélectionnez celle que vous voulez déboguer.
6. Choisissez le type de code à déboguer (managé, natif, mixte)
7. Cliquez sur **Attacher** ou sur **Démarrer**

## <a name="see-also"></a>Voir aussi
* [Installer les outils](install-the-tools.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Déploiement et débogage d’applications de plateforme Windows universelle (UWP)](https://msdn.microsoft.com/library/windows/apps/xaml/mt613243.aspx)
* [Activer votre appareil pour le développement](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)
