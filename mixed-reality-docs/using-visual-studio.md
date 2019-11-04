---
title: Utilisation de Visual Studio pour déployer et déboguer
description: Comment générer, déboguer et déployer des applications pour HoloLens et Windows Mixed Reality à l’aide de Visual Studio.
author: pbarnettms
ms.author: pbarnett
ms.date: 10/24/2019
ms.topic: article
keywords: Visual Studio, HoloLens, réalité mixte, débogage, déployer
ms.openlocfilehash: 2b84183417a1bd4eaa90eef58bebe2b65966b933
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437286"
---
# <a name="using-visual-studio-to-deploy-and-debug"></a>Utilisation de Visual Studio pour déployer et déboguer

Que vous souhaitiez utiliser DirectX ou Unity pour développer votre application de réalité mixte, vous allez utiliser Visual Studio pour le débogage et le déploiement. Dans cette section, vous allez apprendre à :
* Guide pratique pour déployer des applications sur votre casque Windows (HoloLens ou Windows Mixed Reality) à l’aide de Visual Studio.
* Comment utiliser l’émulateur HoloLens intégré à Visual Studio.
* Comment déboguer des applications de réalité mixte.

## <a name="prerequisites"></a>Conditions préalables
1. Consultez [installer les outils](install-the-tools.md) pour obtenir des instructions d’installation.
2. Créez un projet d’application Windows universelle dans Visual Studio.  Pour HoloLens (1re génération), utilisez Visual Studio 2017 ou une version plus récente.  Pour Hololens 2, utilisez Visual Studio 2019 16,2 ou une version plus récente. C#et C++ sont pris en charge. (Ou suivez les instructions pour [créer une application dans Unity](holograms-100.md).)

## <a name="enabling-developer-mode"></a>Activation du mode développeur

Commencez par activer le **mode développeur** sur votre appareil afin que Visual Studio puisse s’y connecter.

### <a name="hololens"></a>HoloLens
1. Activez votre HoloLens et mettez-le sur l’appareil.
2. Effectuer le geste qui consiste à [maintenir sa paume de main vers le haut en serrant ses doigts et à les ouvrir](system-gesture.md#bloom) pour lancer le menu principal.
3. Pointez avec le regard de la vignette **paramètres** et effectuez le mouvement d' [appui sur l’air](gaze-and-commit.md#composite-gestures) . Appuyez de nouveau pour placer l’application dans votre environnement. L’application Paramètres démarre une fois placée.
4. Sélectionnez l’élément de menu **Mettre à jour**.
5. Sélectionnez l’élément de menu **Pour les développeurs**.
6. Activez **Mode développeur**. Cela vous permettra de [déployer des applications à partir de Visual Studio](using-visual-studio.md) dans votre HoloLens.
7. Facultatif : faites défiler vers le dessous et activez également le **portail des appareils**. Cela vous permettra également de vous connecter au [portail de périphériques Windows](using-the-windows-device-portal.md) sur votre HoloLens à partir d’un navigateur Web.

### <a name="windows-pc"></a>PC Windows

Si vous travaillez avec un casque Windows Mixed Reality connecté à votre PC, vous devez activer le **mode développeur** sur le PC.
1. Accéder aux **paramètres**
2. Sélectionner la **mise à jour et la sécurité**
3. Sélectionnez **pour les développeurs**
4. Activez le **mode développeur**, lisez le démenti pour le paramètre que vous avez choisi, puis cliquez sur Oui pour accepter la modification.

## <a name="deploying-an-app-over-wi-fi---hololens-1st-gen"></a>Déploiement d’une application sur un réseau Wi-Fi-HoloLens (1ère génération)
1. Sélectionnez une configuration de build **x86** pour votre application ![configuration de build x86 dans Visual Studio](images/x86setting.png)
2. Sélectionnez **machine distante** dans le menu déroulant cible de déploiement ![cible de déploiement de l’ordinateur distant dans Visual Studio](images/remotemachinesetting.png)
3. Pour C++ les projets JavaScript et, accédez à **propriétés du projet > > propriétés de configuration > débogage**. Pour C# les projets, une boîte de dialogue s’affiche automatiquement pour configurer votre connexion.
  a. Entrez l’adresse IP de votre appareil dans le champ **adresse** ou nom de l' **ordinateur** . Recherchez l’adresse IP sur votre HoloLens sous **paramètres > réseau & Internet > options avancées**ou demandez à Cortana « qu’est-ce que mon adresse IP ? ».
  b. Définir le mode d’authentification sur le **protocole universel (protocole non chiffré)** ![la boîte de dialogue Connexion à distance dans Visual Studio](images/remotedeploy.png)
4. Sélectionnez **Déboguer > démarrer le débogage** pour déployer votre application et démarrer le débogage![exécuter sans débogage dans Visual Studio](images/deploywithdebugging.png)
5. La première fois que vous déployez une application sur votre HoloLens à partir de votre PC, vous êtes invité à entrer un code confidentiel. Suivez les instructions **de jumelage de vos appareils** ci-dessous.

## <a name="deploying-an-app-over-wi-fi---hololens-2"></a>Déploiement d’une application sur Wi-Fi-HoloLens 2
1. Sélectionnez une configuration de build **ARM** ou **ARM64** pour votre application ![ARM64 configuration de build dans Visual Studio](images/arm64setting.png)
2. Sélectionnez **machine distante** dans le menu déroulant cible de déploiement ![cible de déploiement de l’ordinateur distant dans Visual Studio](images/remotemachinesetting_arm64.png)
3. Pour C++ les projets JavaScript et, accédez à **propriétés du projet > > propriétés de configuration > débogage**. Pour C# les projets, une boîte de dialogue s’affiche automatiquement pour configurer votre connexion.
  a. Entrez l’adresse IP de votre appareil dans le champ **adresse** ou nom de l' **ordinateur** . Recherchez l’adresse IP sur votre HoloLens sous **paramètres > réseau & Internet > options avancées**ou demandez à Cortana « qu’est-ce que mon adresse IP ? ».
  b. Définir le mode d’authentification sur le **protocole universel (protocole non chiffré)** ![la boîte de dialogue Connexion à distance dans Visual Studio](images/remotedeploy.png)
4. Sélectionnez **Déboguer > démarrer le débogage** pour déployer votre application et démarrer le débogage![exécuter sans débogage dans Visual Studio](images/deploywithdebugging.png)
5. La première fois que vous déployez une application sur votre HoloLens à partir de votre PC, vous êtes invité à entrer un code confidentiel. Suivez les instructions **de jumelage de vos appareils** ci-dessous.

Si votre adresse IP HoloLens change, vous pouvez modifier l’adresse IP de l’ordinateur cible en accédant à **Propriétés de projet > > propriétés de Configuration > débogage**

## <a name="deploying-an-app-over-usb---hololens-1st-gen"></a>Déploiement d’une application sur USB-HoloLens (1ère génération)
1. Sélectionnez une configuration de build **x86** pour votre application ![configuration de build x86 dans Visual Studio](images/x86setting.png)
2. Sélectionnez **appareil** dans le menu déroulant cible de déploiement![déploiement d’appareil dans Visual Studio](images/buildsettingsusbdeploy.png)
3. Sélectionnez **Déboguer > démarrer le débogage** pour déployer votre application et démarrer le débogage![exécuter sans débogage dans Visual Studio](images/deploywithdebugging.png)
4. La première fois que vous déployez une application sur votre HoloLens à partir de votre PC, vous êtes invité à entrer un code confidentiel. Suivez les instructions **de jumelage de vos appareils** ci-dessous.

## <a name="deploying-an-app-over-usb---hololens-2"></a>Déploiement d’une application sur USB-HoloLens 2
1. Sélectionnez une configuration de build **ARM** ou **ARM64** pour votre application ![ARM64 configuration de build dans Visual Studio](images/arm64setting.png)
2. Sélectionnez **appareil** dans le menu déroulant cible de déploiement![déploiement d’appareil dans Visual Studio](images/buildsettingsusbdeploy_arm64.png)
3. Sélectionnez **Déboguer > démarrer le débogage** pour déployer votre application et démarrer le débogage![exécuter sans débogage dans Visual Studio](images/deploywithdebugging.png)
4. La première fois que vous déployez une application sur votre HoloLens à partir de votre PC, vous êtes invité à entrer un code confidentiel. Suivez les instructions **de jumelage de vos appareils** ci-dessous.

## <a name="deploying-an-app-to-your-local-pc---immersive-headset"></a>Déploiement d’une application sur votre PC local-casque d’immersion

Suivez ces instructions lors de l’utilisation d’un casque immersif Windows Mixed Reality qui se connecte à votre PC ou au [simulateur de réalité mixte](using-the-windows-mixed-reality-simulator.md). Dans ce cas, il vous suffit de déployer et d’exécuter votre application sur l’ordinateur local.
1. Sélectionner une configuration de build **x86** ou **x64** pour votre application
2. Sélectionnez **ordinateur local** dans le menu déroulant cible de déploiement.
3. Sélectionnez **Déboguer > démarrer le débogage** pour déployer votre application et démarrer le débogage

## <a name="pairing-your-device"></a>Appariement de votre appareil

La première fois que vous déployez une application à partir de Visual Studio dans votre HoloLens, vous êtes invité à entrer un code confidentiel. Sur le HoloLens, générez un code confidentiel en lançant l’application paramètres, accédez à **mettre à jour > pour les développeurs** et appuyez sur **paire**. Un code confidentiel s’affiche sur votre HoloLens ; tapez ce code PIN dans Visual Studio. Une fois le jumelage terminé, appuyez sur **terminé** sur votre HoloLens pour fermer la boîte de dialogue. Cet ordinateur est maintenant associé au HoloLens et vous pouvez déployer des applications automatiquement. Répétez ces étapes pour chaque ordinateur suivant utilisé pour déployer des applications dans votre HoloLens.

Pour annuler l’appariement de votre HoloLens de tous les ordinateurs avec lesquels il a été associé, lancez l’application **paramètres** , accédez à **mettre à jour > pour les développeurs** et appuyez sur **Clear**.

## <a name="deploying-an-app-to-the-hololens-1st-gen-emulator"></a>Déploiement d’une application sur l’émulateur HoloLens (1er génération)
1. Vérifiez que vous avez **[installé l’émulateur HoloLens](install-the-tools.md)** .
2. Sélectionnez une configuration de build **x86** pour votre application.
![configuration de build x86 dans Visual Studio](images/x86setting.png)
3. Sélectionnez **émulateur HoloLens** dans le menu déroulant cible de déploiement![cible de l’émulateur dans Visual Studio](images/deployemulator.png)
4. Sélectionnez **Déboguer > démarrer le débogage** pour déployer votre application et démarrer le débogage![exécuter sans débogage dans Visual Studio](images/deploywithdebugging.png)

## <a name="deploying-an-app-to-the-hololens-2-emulator"></a>Déploiement d’une application sur l’émulateur HoloLens 2
1. Vérifiez que vous avez **[installé l’émulateur HoloLens](install-the-tools.md)** .
2. Sélectionnez une configuration de build **x86** ou **x64** pour votre application.
![configuration de build x86 dans Visual Studio](images/x86setting.png)
3. Sélectionnez **émulateur HoloLens 2** dans le menu déroulant cible de déploiement![cible de l’émulateur dans Visual Studio](images/deployemulator2.png)
4. Sélectionnez **Déboguer > démarrer le débogage** pour déployer votre application et démarrer le débogage![exécuter sans débogage dans Visual Studio](images/deploywithdebugging.png)

## <a name="graphics-debugger-for-hololens-1st-gen"></a>Débogueur Graphics pour HoloLens (1re génération)

Les outils Visual Studio Graphics Diagnostics sont très utiles lors de l’écriture et de l’optimisation d’une application holographique. Pour plus d’informations, consultez [Visual Studio Graphics Diagnostics sur MSDN](https://msdn.microsoft.com/library/hh315751.aspx) .

**Pour démarrer le débogueur Graphics**
1. Suivez les instructions ci-dessus pour cibler un appareil ou un émulateur
2. Accédez à **Déboguer > graphiques > démarrer les diagnostics**
3. La première fois que vous effectuez cette opération avec un HoloLens, vous pouvez obtenir une erreur « Accès refusé ». Redémarrez votre HoloLens pour permettre aux autorisations mises à jour de prendre effet, puis réessayez.

## <a name="profiling"></a>Profilage

Les outils de profilage Visual Studio vous permettent d’analyser les performances et l’utilisation des ressources de votre application. Cela comprend des outils permettant d’optimiser l’utilisation du processeur, de la mémoire, des graphiques et du réseau. Pour plus d’informations, consultez [exécuter les outils de diagnostic sans débogage sur MSDN](https://msdn.microsoft.com/library/dn957936.aspx) .

**Pour démarrer le Outils de profilage avec HoloLens**
1. Suivez les instructions ci-dessus pour cibler un appareil ou un émulateur
2. Accédez à **Déboguer > démarrer la outils de diagnostic sans débogage...**
3. Sélectionnez les outils que vous souhaitez utiliser
4. Cliquez sur **Démarrer**
5. La première fois que vous effectuez cette opération avec un HoloLens, vous pouvez obtenir une erreur « Accès refusé ». Redémarrez votre HoloLens pour permettre aux autorisations mises à jour de prendre effet, puis réessayez.

## <a name="debugging-an-installed-or-running-app"></a>Débogage d’une application installée ou en cours d’exécution

Vous pouvez utiliser Visual Studio pour déboguer une application Windows universelle installée sans déployer à partir d’un projet Visual Studio. Cela est utile si vous souhaitez déboguer un package d’application installé, ou si vous souhaitez déboguer une application qui est déjà en cours d’exécution.
1. Aller à **Déboguer-> autres cibles de débogage-déboguer le package d’application installé >**
2. Sélectionnez la cible de l' **ordinateur distant** pour HoloLens ou la **machine locale** pour les casques immersifs.
3. Entrer l' **adresse IP** de votre appareil
4. Choisir le mode d’authentification **universelle**
5. La fenêtre affiche les applications en cours d’exécution et inactives. Choisissez celui que vous souhaitez déboguer.
6. Choisir le type de code à déboguer (managé, natif, mixte)
7. Cliquez sur **attacher** ou sur **Démarrer** .

## <a name="see-also"></a>Articles associés
* [Installer les outils](install-the-tools.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Déploiement et débogage d’applications plateforme Windows universelle (UWP)](https://msdn.microsoft.com/library/windows/apps/xaml/mt613243.aspx)
* [Activer votre appareil pour le développement](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)
