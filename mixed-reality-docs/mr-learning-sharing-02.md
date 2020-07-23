---
title: Tutoriels sur les fonctionnalités multi-utilisateurs - 2. Configuration de Photon Unity Networking
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multiutilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: e5817338dbed944232664a86f8b0625bc9d3e1e7
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86305711"
---
# <a name="2-setting-up-photon-unity-networking"></a>2. Configuration de Photon Unity Networking

## <a name="overview"></a>Vue d’ensemble

Dans ce tutoriel, vous allez préparer la création d’une expérience partagée à l’aide de Photon Unity Networking (PUN). Vous allez découvrir comment créer une application PUN, importer des ressources PUN dans votre projet Unity et connecter votre projet Unity à l’application PUN.

## <a name="objectives"></a>Objectifs

* Apprendre à créer une application PUN
* Apprendre à trouver et importer les ressources PUN
* Apprendre à connecter votre projet Unity à l’application PUN

## <a name="creating-and-preparing-the-unity-project"></a>Création et préparation du projet Unity

Dans cette section, vous allez créer un projet Unity et le préparer au développement avec MRTK.

Pour cela, suivez d’abord [Initialisation de votre projet et déploiement de votre première application](mr-learning-base-02.md), en excluant les instructions données dans [Générer votre application sur votre appareil](mr-learning-base-02.md#building-your-application-to-your-hololens-2), ce qui inclut les étapes suivantes :

1. [Création du projet Unity](mr-learning-base-02.md#creating-the-unity-project) et affectation d’un nom pertinent, par exemple *MRTK Tutorials*
1. [Changement de plateforme de génération](mr-learning-base-02.md#configuring-the-unity-project)
1. [Importation des ressources TextMeshPro Essential](mr-learning-base-02.md#importing-the-textmeshpro-essential-resources)
1. [Importation du Mixed Reality Toolkit](mr-learning-base-02.md#importing-the-mixed-reality-toolkit)
1. [Configuration du projet Unity](mr-learning-base-02.md#configuring-the-unity-project)
1. [Création et configuration de la scène](mr-learning-base-02.md#creating-and-configuring-the-scene), et affectation d’un nom pertinent à la scène, par exemple *MultiUserCapabilities*

Ensuite, suivez les instructions fournies dans [Modification de l’option d’affichage de la reconnaissance spatiale](mr-learning-base-03.md#changing-the-spatial-awareness-display-option) pour :

1. Définir le **profil de configuration MRTK** sur **DefaultHoloLens2ConfigurationProfile**.
1. Définir les **options d’affichage du maillage spatiale** sur **Occlusion**.

## <a name="enabling-additional-capabilities"></a>Activation de fonctionnalités supplémentaires

Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings, puis recherchez la section **Player** >  **Publishing Settings** :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section2-step1-1.png)

Dans la section **Publishing Settings**, accédez à la section **Capabilities** et vérifiez bien que les fonctionnalités **InternetClient**, **Microphone**, **SpatialPerception** et **GazeInput**, que vous avez activées à l’étape [Configuration du projet Unity](mr-learning-base-02.md#configuring-the-unity-project) ci-dessus, sont activées.

Activez ensuite les fonctionnalités supplémentaires suivantes :

* Fonctionnalité **InternetClientServer**
* Fonctionnalité **PrivateNetworkClientServer**

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section2-step1-2.png)

## <a name="installing-inbuilt-unity-packages"></a>Installation de packages Unity intégrés

Dans le menu Unity, sélectionnez **Window** > **Package Manager** pour ouvrir la fenêtre Package Manager, sélectionnez **AR Foundation**, puis cliquez sur le bouton **Install** pour installer le package :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section3-step1-1.png)

> [!NOTE]
> Vous installez le package intégré AR Foundation, car il est nécessaire pour le SDK Azure Spatial Anchors que vous allez importer dans la section suivante.

## <a name="importing-the-tutorial-assets"></a>Importation des ressources du tutoriel

Téléchargez et **importez** les packages personnalisés Unity suivants **dans l’ordre où ils sont listés** :

* [AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.2.1/AzureSpatialAnchors.unitypackage) (version 2.2.1)
* [MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.4.0.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.4.0/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.4.0.unitypackage)
* [MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.4.0.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.4.0/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.4.0.unitypackage)
* [MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.4.0.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/multi-user-capabilities-v2.4.0/MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.4.0.unitypackage)

Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section4-step1-1.png)

> [!TIP]
> Pour vous rappeler comment importer un package personnalisé Unity, vous pouvez vous référer aux instructions fournies dans [Importation de Mixed Reality Toolkit](mr-learning-base-02.md#importing-the-mixed-reality-toolkit).

> [!NOTE]
> Après l’importation du package de ressources du tutoriel MultiUserCapabilities, la fenêtre de console contient plusieurs erreurs [CS0246](https://docs.microsoft.com/dotnet/csharp/language-reference/compiler-messages/cs0246) qui indiquent que le type ou l’espace de noms est manquant. Ces erreurs sont attendues et seront résolues dans la section suivante quand vous importerez les ressources PUN.

## <a name="importing-the-pun-assets"></a>Importation des ressources PUN

Dans le menu Unity, sélectionnez **Window** > **Asset Store** pour ouvrir la fenêtre Asset Store, recherchez et sélectionnez **PUN 2 - FREE** dans Exit Games, puis cliquez sur le bouton **Download** pour télécharger le package de ressources dans votre compte Unity.

Une fois le téléchargement terminé, cliquez sur le bouton **Importer** pour ouvrir la fenêtre Import Unity Package :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section5-step1-1.png)

Dans la fenêtre Import Unity Package (Importer un package Unity), cliquez sur le bouton **Tous** pour vous assurer que toutes les ressources sont sélectionnées, puis sur le bouton **Importer** pour importer les ressources :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section5-step1-2.png)

Une fois le processus d’importation terminé dans Unity, la fenêtre Pun Wizard apparaît avec le menu PUN Setup chargé. Vous pouvez ignorer ou fermer cette fenêtre pour l’instant :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section5-step1-3.png)

## <a name="creating-the-pun-application"></a>Création de l’application PUN

Dans cette section, vous allez créer un compte Photon (si vous n’en avez pas encore) et créer une application PUN.

Accédez au<a href="https://dashboard.photonengine.com/account/signin" target="_blank">tableau de bord</a> Photon et connectez-vous si vous disposez déjà d’un compte que vous souhaitez utiliser. Sinon, cliquez sur le lien **Create One** et suivez les instructions pour inscrire un nouveau compte :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section6-step1-1.png)

Une fois connecté, cliquez sur le bouton **Create a New App** :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section6-step1-2.png)

Dans la page Create a New Application, entrez les valeurs suivantes :

* Pour Photon Type, sélectionnez PUN.
* Pour Nom, entrez un nom approprié, par exemple _MRTK Tutorials_.
* Pour Description, entrez éventuellement une description appropriée.
* Laissez le champ URL vide.

Cliquez ensuite sur le bouton **Create** pour créer l’application :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section6-step1-3.png)

Une fois le processus de création terminé dans Photon, la nouvelle application PUN apparaît dans votre tableau de bord :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section6-step1-4.png)

## <a name="connecting-the-unity-project-to-the-pun-application"></a>Connexion du projet Unity à l’application PUN

Dans cette section, vous allez connecter votre projet Unity à l’application PUN que vous avez créée dans la section précédente.

Dans le tableau de bord Photon, cliquez sur le champ **App ID** pour voir l’ID d’application, puis copiez-le dans le Presse-papiers :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section7-step1-1.png)

Dans le menu Unity, sélectionnez **Window** > **Photon Unity Networking** > **PUN Wizard** pour ouvrir la fenêtre Pun Wizard, puis cliquez sur le bouton **Setup Project** pour ouvrir le menu PUN Setup et configurez-le comme suit :

* Dans le champ **AppId or Email**, collez l’ID d’application PUN que vous avez copié à l’étape précédente.

Cliquez ensuite sur le bouton **Setup Project** pour appliquer l’ID d’application :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section7-step1-2.png)

Une fois le processus d’installation PUN terminé dans Unity, le menu PUN Setup affiche le message **Done!** et sélectionne automatiquement la ressource **PhotonServerSettings** dans la fenêtre Project. Les propriétés de cette ressource sont présentées dans la fenêtre Inspector :

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section7-step1-3.png)

## <a name="congratulations"></a>Félicitations

Vous avez créé une application PUN et l’avez connectée à votre projet Unity. Vous allez à présent autoriser les connexions avec d’autres utilisateurs pour qu’ils puissent se voir.

[Tutoriel suivant : 3. Connexion de plusieurs utilisateurs](mr-learning-sharing-03.md)
