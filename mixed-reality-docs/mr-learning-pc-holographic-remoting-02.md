---
title: Tutoriels sur la communication à distance holographique de PC - 2. Créer une application PC de communication à distance holographique
description: Suivez ce cours pour découvrir comment communiquer à distance une expérience de réalité mixte de votre PC à HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 6d11d91a0e08c48c09f676171dcb9bb8a0ff74de
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376371"
---
# <a name="2-creating-a-holographic-remoting-pc-application"></a>2. Création d’une application PC de communication à distance holographique

Dans ce tutoriel, vous allez apprendre à créer une application PC de communication à distance holographique et à la connecter à HoloLens 2 à tout moment pour visualiser du contenu 3D en réalité mixte.

## <a name="objectives"></a>Objectifs

* Configurer Unity pour la communication à distance holographique
* Apprendre à créer et déployer l’application avec Visual Studio
* Développer une application de communication à distance holographique et la connecter à HoloLens

## <a name="configuring-your-scene-for-holographic-remoting"></a>Configuration de votre scène pour la communication à distance holographique

Dans cette section, vous allez configurer votre projet pour diffuser en streaming et en temps réel une expérience de réalité mixte de votre PC sur votre appareil HoloLens 2 au moyen d’une connexion Wi-Fi.

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.PCHolograhicRemoting** > **Prefabs**, puis cliquez sur le préfabriqué **HolographicRemoting** et faites-le glisser dans votre scène.

![mrlearning-pc-holographic-remoting](images/mrlearning-pc-holographic-remoting/Tutorial2-Section1-Step1-1.png)

## <a name="build-your-application-to-pc"></a>Générer votre application pour PC

Vous pouvez à présent générer votre application de communication à distance holographique sur votre PC. Suivez les étapes ci-dessous et apportez ces modifications pour générer cette application sur votre PC.

### <a name="1-set-the-player-settings"></a>1. Définir les paramètres du lecteur

Dans le menu Unity, sélectionnez Edit > Project Settings pour ouvrir la fenêtre Player Settings.

Dans la section **XR Settings**, cochez la case **WSA Holographic Remoting Supported** et activez la communication à distance holographique.

![mrlearning-pc-holographic-remoting](images/mrlearning-pc-holographic-remoting/Tutorial2-Section2-Step1-1.png)

### <a name="2-build-the-unity-project"></a>2. Générer le projet Unity

Dans le menu Unity, sélectionnez File > Build Settings pour ouvrir la fenêtre Build Settings.

Dans la fenêtre Build Settings, cliquez sur le bouton ***Add Open Scenes*** pour ajouter votre scène actuelle aux scènes. Dans la liste Build, cliquez sur le bouton ***Build*** pour ouvrir la fenêtre Build Universal Windows Platform :

![mrlearning-pc-holographic-remoting](images/mrlearning-pc-holographic-remoting/Tutorial2-Section2-Step2-1.png)

Dans la fenêtre Build Universal Windows Platform, choisissez un emplacement pour stocker votre build, par exemple Documents\MixedRealityLearning. Créez un dossier et donnez-lui un nom approprié, par exemple PCHolographicRemoting. Cliquez ensuite sur le bouton ***Select Folder*** pour démarrer le processus de génération :

![mrlearning-pc-holographic-remoting](images/mrlearning-pc-holographic-remoting/Tutorial2-Section2-Step2-2.png)

Attendez qu’Unity termine le processus de génération.

![mrlearning-pc-holographic-remoting](images/mrlearning-pc-holographic-remoting/Tutorial2-Section2-Step2-3.png)

### <a name="3-build-and-deploy-the-application"></a>3. Générer et déployer l’application

Une fois le processus de génération terminé, Unity invite l’Explorateur de fichiers Windows à ouvrir l’emplacement où vous avez stocké la build. Naviguez dans le dossier, puis double-cliquez sur le fichier .sln pour l’ouvrir dans Visual Studio :

![mrlearning-pc-holographic-remoting](images/mrlearning-pc-holographic-remoting/Tutorial2-Section2-Step3-1.png)

> [!NOTE]
> Si Visual Studio vous invite à installer de nouveaux composants, prenez un moment pour vérifier que tous les composants prérequis sont installés comme spécifié dans la documentation Installer les outils.

Configurez Visual Studio pour PC en sélectionnant la configuration Release, l’architecture x64 et Ordinateur local comme cible :

![mrlearning-pc-holographic-remoting](images/mrlearning-pc-holographic-remoting/Tutorial2-Section2-Step3-2.png)

Cliquez sur le bouton qui indique ***Ordinateur local***. La procédure de génération et de déploiement de l’application sur votre PC démarre. L’application est installée sur votre PC par défaut.

## <a name="testing-holographic-remoting-remote-application"></a>Test d’une application de communication à distance holographique

Pour connecter votre application PC à votre HoloLens 2, effectuez les étapes suivantes :

### <a name="1-install-the-remoting-player-application-on-hololens-2-device"></a>1. Installer l’application Remoting Player sur l’appareil HoloLens 2

* Sur votre HoloLens 2, accédez à l’application Store et recherchez « **Remoting Player** ».
* Sélectionnez l’application **Remoting Player**.
* Appuyez sur **Install** pour télécharger et installer l’application.

### <a name="2-connect-the-holographic-remoting-pc-app-to-the-remoting-player"></a>2. Connecter l’application PC de communication à distance holographique à Remoting Player

* Démarrez **Remoting Player** sur votre HoloLens.
* Notez l’**adresse IP** d’HoloLens. Celle-ci apparaît sous la forme d’un hologramme dès le lancement de **Remoting Player**.
* Ouvrez l’application PC de communication à distance holographique sur votre PC.
* Une fois l’application lancée, entrez l’**adresse IP** , puis cliquez sur le bouton **Connect** pour vous connecter.

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez appris à créer une application PC de communication à distance holographique et à la connecter à HoloLens 2 à tout moment pour visualiser du contenu 3D en réalité mixte. Une fois l’application PC de communication à distance holographique connectée à HoloLens, l’expérience de réalité mixte est diffusée en streaming sur votre appareil HoloLens 2.
