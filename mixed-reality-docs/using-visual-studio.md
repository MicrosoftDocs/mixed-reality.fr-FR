---
title: À l’aide de Visual Studio pour déployer et déboguer
description: Comment générer, déboguer et déployer des applications pour HoloLens et Windows Mixed Reality à l’aide de Visual Studio.
author: JonMLyons
ms.author: jlyons
ms.date: 03/21/2018
ms.topic: article
keywords: Visual Studio, HoloLens, réalité mixte, déboguer, déployer
ms.openlocfilehash: 6bd47d7212d321791a11ff4db91c3e172c91f463
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594876"
---
# <a name="using-visual-studio-to-deploy-and-debug"></a>À l’aide de Visual Studio pour déployer et déboguer

Si vous souhaitez utiliser DirectX ou Unity pour développer votre application de réalité mixte, vous allez utiliser Visual Studio pour le débogage et le déploiement. Dans cette section, vous allez apprendre :
* Comment déployer des applications sur votre casque immersive HoloLens ou de réalité mixte Windows via Visual Studio.
* Comment utiliser l’émulateur de HoloLens intégré à Visual Studio.
* Comment déboguer des applications de réalité mixte.

## <a name="prerequisites"></a>Prérequis
1. Consultez [installer les outils](install-the-tools.md) pour obtenir des instructions d’installation.
2. Créer un nouveau projet d’application Windows universelle dans Visual Studio 2015 Update 1 ou Visual Studio 2017. C#, C++, et les projets JavaScript sont toutes prises en charge. (Ou suivez les instructions pour [créer une build d’une application dans Unity](holograms-100.md).)

## <a name="enabling-developer-mode"></a>Activation du mode développeur

Commencer par activer **Mode développeur** sur votre appareil afin que Visual Studio peut se connecter à celui-ci.

### <a name="hololens"></a>HoloLens
1. Activer votre HoloLens et placé sur l’appareil.
2. Effectuer le geste qui consiste à [maintenir sa paume de main vers le haut en serrant ses doigts et à les ouvrir](gestures.md#bloom) pour lancer le menu principal.
3. Fixez du regard le **paramètres** vignette et effectuer le [-appui en l’air](gestures.md#air-tap) mouvement. Appuyez de nouveau pour placer l’application dans votre environnement. L’application Paramètres démarre une fois placée.
4. Sélectionnez l’élément de menu **Mettre à jour**.
5. Sélectionnez l’élément de menu **Pour les développeurs**.
6. Activez **Mode développeur**. Cela vous permettra de [déployer des applications à partir de Visual Studio](using-visual-studio.md) pour votre HoloLens.
7. Facultatif : Défiler vers le bas et également activer **portail appareils**. Cela permettra également vous connecter à la [Windows Device Portal](using-the-windows-device-portal.md) sur votre HoloLens depuis un navigateur web.

### <a name="windows-pc"></a>PC Windows

Si vous travaillez avec un casque de réalité mixte Windows connecté à votre PC, vous devez activer **Mode développeur** sur le PC.
1. Accédez à **paramètres**
2. Sélectionnez **mise à jour et sécurité**
3. Sélectionnez **pour les développeurs**
4. Activer **Mode développeur**, lisez l’exclusion pour le paramètre que vous avez choisi, puis cliquez sur Oui pour accepter la modification.

## <a name="deploying-an-app-over-wi-fi---hololens-1st-gen"></a>Déploiement d’une application via le Wi-Fi - HoloLens (1er gen)
1. Sélectionnez un **x86** générer la configuration de votre application ![x86 créer la configuration dans Visual Studio](images/x86setting.png)
2. Sélectionnez **Machine distante** dans le menu de liste déroulante de cible de déploiement ![cible de déploiement d’ordinateur distant dans Visual Studio](images/remotemachinesetting.png)
3. Pour C++ et projets JavaScript, accédez à **projet > Propriétés > Propriétés de Configuration > débogage**. Pour C# projets, un boîte de dialogue ne sera automatiquement contextuelle pour configurer votre connexion.
  a. Entrez l’adresse IP de votre appareil dans le **adresse** ou **nom_machine** champ. Rechercher l’adresse IP sur votre HoloLens sous **Paramètres > réseau & Internet > Options avancées**, ou vous pouvez demander à Cortana de « Quel est mon adresse IP ? »
  b. Définir le Mode d’authentification **universel (protocole non chiffré)**![boîte de dialogue de connexion à distance dans Visual Studio](images/remotedeploy.png)
4. Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et de démarrer le débogage![démarrer sans débogage dans Visual Studio](images/deploynodebugging.png)
5. La première fois que vous déployez une application sur votre HoloLens à partir de votre PC, vous demandera un code confidentiel. Suivez le **d’associer votre périphérique** instructions ci-dessous.

Si votre adresse IP de HoloLens change, vous pouvez modifier l’adresse IP de la machine cible en accédant à **projet > Propriétés > Propriétés de Configuration > débogage**

## <a name="deploying-an-app-over-usb---hololens-1st-gen"></a>Déploiement d’une application via USB - HoloLens (1er gen)
1. Sélectionnez un **x86** générer la configuration de votre application ![x86 créer la configuration dans Visual Studio](images/x86setting.png)
2. Sélectionnez **appareil** dans le menu de liste déroulante de cible de déploiement![déploiement de périphérique dans Visual Studio](images/buildsettingsusbdeploy.png)
3. Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et de démarrer le débogage![démarrer sans débogage dans Visual Studio](images/deploynodebugging.png)
4. La première fois que vous déployez une application sur votre HoloLens à partir de votre PC, vous demandera un code confidentiel. Suivez le **d’associer votre périphérique** instructions ci-dessous.

## <a name="deploying-an-app-to-your-local-pc---immersive-headset"></a>Déploiement d’une application sur votre ordinateur Local - casque immersif

Suivez ces instructions lorsque vous utilisez un casque immersif Windows Mixed Reality qui se connecte à votre PC ou [simulateur de réalité mixte](using-the-windows-mixed-reality-simulator.md). Dans ces cas, il vous suffit de déployer et exécuter votre application sur le PC local.
1. Sélectionnez un **x86** ou **x64** générer la configuration de votre application
2. Sélectionnez **ordinateur Local** dans le menu de liste déroulante de cible de déploiement
3. Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et de démarrer le débogage

## <a name="pairing-your-device---hololens-1st-gen"></a>Associer votre périphérique - HoloLens (1er gen)

La première fois que vous déployez une application à partir de Visual Studio à votre HoloLens, vous demandera un code confidentiel. Sur le HoloLens, générer un code confidentiel en lançant l’application paramètres, accédez à **mise à jour > pour les développeurs** et appuyez sur **paire**. Un code confidentiel s’afficheront sur votre HoloLens ; tapez ce code PIN dans Visual Studio. Une fois le jumelage terminé, appuyez sur **fait** sur votre HoloLens pour faire disparaître la boîte de dialogue. Ce PC est désormais associé à la HoloLens et vous serez en mesure de déployer automatiquement des applications. Répétez ces étapes pour chaque PC suivante qui est utilisé pour déployer des applications sur votre HoloLens.

Pour l’annuler-paire votre HoloLens à partir de tous les ordinateurs qu’il a été associé, lancez le **paramètres** application, accédez à **mise à jour > pour les développeurs** et appuyez sur **clair**.

## <a name="deploying-an-app-to-the-hololens-1st-gen-emulator"></a>Déployer une application sur le HoloLens (1er gen) émulateur
1. Vérifiez que vous avez  **[installé l’émulateur de HoloLens](install-the-tools.md)**.
2. Sélectionnez un **x86** générer la configuration de votre application.
![x86 build configuration dans Visual Studio](images/x86setting.png)
3. Sélectionnez **HoloLens émulateur** dans le menu de liste déroulante de cible de déploiement![cible de l’émulateur dans Visual Studio](images/deployemulator.png)
4. Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et de démarrer le débogage![démarrer sans débogage dans Visual Studio](images/deploynodebugging.png)

## <a name="graphics-debugger"></a>Débogueur Graphics

Les outils de Visual Studio Graphics Diagnostics sont très utiles lors de l’écriture et l’optimisation d’une application HOLOGRAPHIQUE. Consultez [Graphics Diagnostics de Visual Studio sur MSDN](https://msdn.microsoft.com/library/hh315751.aspx) pour plus d’informations.

**Pour démarrer le débogueur Graphics**
1. Suivez les instructions ci-dessus pour cibler un appareil ou un émulateur
2. Accédez à **Déboguer > Graphics > Démarrer les Diagnostics**
3. La première fois que vous le faire avec un HoloLens, vous pouvez obtenir une erreur « accès refusé ». Redémarrez votre HoloLens pour autoriser des autorisations mises à jour prennent effet et essayez à nouveau.

## <a name="profiling"></a>Profilage

Les outils de profilage Visual Studio permettent d’analyser l’utilisation de ressources et des performances de votre application. Cela inclut des outils pour optimiser l’UC, mémoire, graphiques et utilisation de réseau. Consultez [exécuter les outils de diagnostic sans débogage sur MSDN](https://msdn.microsoft.com/library/dn957936.aspx) pour plus d’informations.

**Pour démarrer les outils de profilage avec HoloLens**
1. Suivez les instructions ci-dessus pour cibler un appareil ou un émulateur
2. Accédez à **Déboguer > Démarrer les outils de Diagnostic sans débogage...**
3. Sélectionnez les outils que vous souhaitez utiliser
4. Cliquez sur **Démarrer**
5. La première fois que vous le faire avec un HoloLens, vous pouvez obtenir une erreur « accès refusé ». Redémarrez votre HoloLens pour autoriser des autorisations mises à jour prennent effet et essayez à nouveau.

## <a name="debugging-an-installed-or-running-app"></a>Débogage d’une application installée ou en cours d’exécution

Vous pouvez utiliser Visual Studio pour déboguer une application Windows universelle qui est installée sans la déployer à partir d’un projet Visual Studio. Cela est utile si vous souhaitez déboguer un package d’application installée, ou si vous souhaitez déboguer une application qui est déjà en cours d’exécution.
1. Accédez à **Déboguer -> autres débogage cibles -> déboguer le Package d’application installé**
2. Sélectionnez le **Machine distante** cible pour HoloLens ou **ordinateur Local** pour des casques IMMERSIFS.
3. Entrez de votre appareil **adresse IP**
4. Choisissez le **universelle** Mode d’authentification
5. La fenêtre affiche les applications en cours d’exécution et inactives. Choisir celui que vous souhaitez déboguer.
6. Choisissez le type de code à déboguer (géré, natif mixte)
7. Cliquez sur **attacher** ou **Démarrer**

## <a name="see-also"></a>Voir aussi
* [Installer les outils](install-the-tools.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Déployer et déboguer des applications Universal Windows Platform (UWP)](https://msdn.microsoft.com/library/windows/apps/xaml/mt613243.aspx)
* [Activer votre appareil pour le développement](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)
