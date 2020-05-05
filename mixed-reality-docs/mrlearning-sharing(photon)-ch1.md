---
title: Tutoriels sur les fonctionnalités multiutilisateurs - 1. Configuration de Photon Unity Networking
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multiutilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 2f5b55fe9c54e9e2c08177266c04a97d2302230e
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "81610680"
---
# <a name="1-setting-up-photon-unity-networking"></a>1. Configuration de Photon Unity Networking

## <a name="overview"></a>Vue d’ensemble

Dans ce tutoriel, vous allez découvrir comment préparer la création d’une expérience partagée à l’aide de Photon Unity Networking (PUN). Photon est l’une des nombreuses options de mise en réseau accessibles aux développeurs de réalité mixte pour créer des expériences partagées. Vous allez voir comment créer une application Photon PUN, importer des ressources Photon PUN dans votre projet Unity et connecter votre projet Unity à l’application Photon PUN.

## <a name="objectives"></a>Objectifs

* Découvrir comment créer une application Photon PUN
* Découvrir comment trouver et importer les ressources Photon PUN
* Découvrir comment connecter votre projet Unity à l’application Photon PUN

## <a name="prerequisites"></a>Prérequis

>[!TIP]
>Si vous n’avez pas encore effectué les [tutoriels de démarrage](mrlearning-base.md) et les [tutoriels sur les ancres spatiales Azure](mrlearning-asa-ch1.md), nous vous conseillons de le faire avant d’aller plus loin.

* PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)
* SDK Windows 10 (10.0.18362.0 ou version ultérieure)
* Capacité de programmation C# de base
* Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)
* <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté
* Suivez la section [Créer une ressource d’ancres spatiales](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) du tutoriel [Démarrage rapide : Créer une application HoloLens Unity qui utilise Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens).

> [!IMPORTANT]
> La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X. Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.

## <a name="creating-and-preparing-the-unity-project"></a>Création et préparation du projet Unity

Dans cette section, vous allez créer un projet Unity et le préparer au développement avec MRTK.

Pour cela, suivez d’abord [Initialisation de votre projet et de votre première application](mrlearning-base-ch1.md), en excluant les instructions données dans [Générer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device), ce qui inclut les étapes suivantes :

1. [Créer un projet Unity](mrlearning-base-ch1.md#create-new-unity-project) et lui donner un nom approprié, par exemple *MRTK Tutorials*

2. [Configurer le projet Unity pour Windows Mixed Reality](mrlearning-base-ch1.md#configure-the-unity-project-for-windows-mixed-reality)

3. [Importer les ressources essentielles TextMeshPro](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources)

4. [Importer Mixed Reality Toolkit](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit)

5. [Configurer le projet Unity pour Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit)

6. [Ajouter le Mixed Reality Toolkit à la scène Unity](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) et donner à la scène un nom approprié, par exemple *MultiUserCapabilities*

Ensuite, suivez les instructions de [Comment configurer les profils du Kit de ressources de réalité mixte (Modifier l’option d’affichage de la reconnaissance spatiale)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) pour changer le profil de configuration MRTK de votre scène en **DefaultHoloLens2ConfigurationProfile** et pour changer les options d’affichage du maillage de la reconnaissance spatiale en **Occlusion**.

> [!CAUTION]
> Comme mentionné dans les instructions de l’étape [Configurer le projet Unity pour Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit) dont le lien est disponible ci-dessus, il est fortement recommandé de ne pas activer MSBuild pour Unity.

## <a name="configuring-the-capabilities"></a>Configuration des fonctionnalités

Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings, puis recherchez la section **Player** >  **Publishing Settings** :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section2-step1-1.png)

Dans la section **Publishing Settings**, accédez à la section **Capabilities** et vérifiez bien que les fonctionnalités **InternetClient**, **Microphone** et **SpatialPerception**, que vous avez activées lors de la création du projet au début de ce tutoriel, sont activées. Activez ensuite les fonctionnalités **InternetClientServer**, **PrivateNetworkClientServer** et **RemovableStorage** :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section2-step1-2.png)

## <a name="adding-inbuilt-unity-packages"></a>Ajout de packages Unity intégrés
<!-- TODO: Consider renaming to 'Installing AR Foundation' -->

Dans cette section, vous allez installer le package intégré AR Foundation d’Unity, car il est nécessaire pour le SDK Azure Spatial Anchors que vous allez importer dans la section suivante.

Dans le menu Unity, sélectionnez **Window** > **Package Manager** :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section3-step1-1.png)

> [!NOTE]
> Quelques secondes peuvent être nécessaires avant que le package AR Foundation apparaisse dans la liste.

Dans la fenêtre Package Manage, sélectionnez **AR Foundation** et installez le package en cliquant sur le bouton **Install** :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section3-step1-2.png)

## <a name="importing-the-tutorial-assets"></a>Importation des ressources du tutoriel

Téléchargez et **importez** les packages personnalisés Unity suivants **dans l’ordre où ils sont listés** :

* [AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)
* [MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.3/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage)
* [MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.1.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.3.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.1.unitypackage)
* [MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.3.0.0.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/multi-user-capabilities-v2.3.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.3.0.0.unitypackage)

> [!TIP]
> Pour un rappel de la façon d’importer un package personnalisé Unity, vous pouvez vous référer aux instructions de [Importer le Kit de ressources de réalité mixte](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit).

Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section4-step1-1.png)

> [!NOTE]
> Après l’importation du package de ressources du tutoriel MultiUserCapabilities, la fenêtre de console contient plusieurs erreurs [CS0246](https://docs.microsoft.com/dotnet/csharp/language-reference/compiler-messages/cs0246) qui indiquent que le type ou l’espace de noms est manquant. Ces erreurs sont attendues et seront résolues dans la section suivante quand vous importerez les ressources Photon.

## <a name="importing-the-photon-assets"></a>Importation des ressources Photon

Dans cette section, vous allez importer les ressources Photon Unity Network (PUN) du magasin de ressources d’Unity.

Dans le menu Unity, sélectionnez **Window** > **Asset Store** pour ouvrir la fenêtre Asset Store, recherchez et sélectionnez **PUN 2 - FREE** dans Exit Games, puis cliquez sur le bouton **Download** pour télécharger le package de ressources dans votre compte Unity :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section5-step1-1.png)

Une fois le téléchargement terminé, cliquez sur le bouton **Importer** pour ouvrir la fenêtre Import Unity Package :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section5-step1-2.png)

Dans la fenêtre Import Unity Package (Importer un package Unity), cliquez sur le bouton **Tous** pour vous assurer que toutes les ressources sont sélectionnées, puis sur le bouton **Importer** pour importer les ressources :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section5-step1-3.png)

Une fois le processus d’importation terminé dans Unity, la fenêtre Pun Wizard apparaît avec le menu PUN Setup chargé. Vous pouvez ignorer ou fermer cette fenêtre pour l’instant :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section5-step1-4.png)

## <a name="setting-up-photon"></a>Configuration de Photon

Dans cette section, vous allez créer un compte Photon si vous n’en avez pas déjà un, puis créer une application PUN.

Accédez au<a href="https://dashboard.photonengine.com/account/signin" target="_blank">tableau de bord</a> Photon et connectez-vous si vous disposez déjà d’un compte que vous souhaitez utiliser. Sinon, cliquez sur le lien **Create One** et suivez les instructions pour inscrire un nouveau compte :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section6-step1-1.png)

Une fois connecté, cliquez sur le bouton **Create a New App** :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section6-step1-2.png)

Dans la page Create a New Application, entrez les valeurs suivantes :

* Pour Photon Type, sélectionnez Photon PUN.
* Pour Nom, entrez un nom approprié, par exemple _MRTK Tutorials_.
* Pour Description, entrez éventuellement une description appropriée.
* Laissez le champ URL vide.

Cliquez ensuite sur le bouton **Créer** pour créer l’application :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section6-step1-3.png)

Une fois le processus de création terminé dans Photon, la nouvelle application PUN apparaît dans votre tableau de bord :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section6-step1-4.png)

## <a name="connecting-the-unity-project-to-the-pun-application"></a>Connexion du projet Unity à l’application PUN

Dans cette section, vous allez connecter votre projet Unity à l’application PUN que vous avez créée dans la section précédente.

Dans le tableau de bord Photon, cliquez sur le champ **App ID** pour voir l’ID d’application, puis copiez-le dans le Presse-papiers :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section7-step1-1.png)

Dans le menu Unity, sélectionnez **Window** > **Photon Unity Networking** > **PUN Wizard** pour ouvrir la fenêtre Pun Wizard, puis cliquez sur le bouton **Setup Project** pour ouvrir le menu PUN Setup et configurez-le comme suit :

* Dans le champ **AppId or Email**, collez l’ID d’application PUN que vous avez copié à l’étape précédente.

Cliquez ensuite sur le bouton **Setup Project** pour appliquer l’ID d’application :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section7-step1-2.png)

Une fois le processus d’installation PUN terminé dans Unity, le menu PUN Setup affiche le message **Done!** et sélectionne automatiquement la ressource **PhotonServerSettings** dans la fenêtre Project. Les propriétés de cette ressource sont présentées dans la fenêtre Inspector :

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section7-step1-3.png)

## <a name="congratulations"></a>Félicitations

Vous avez créé une application Photon PUN et l’avez connectée à votre projet Unity. Vous allez à présent autoriser les connexions avec d’autres utilisateurs pour qu’ils puissent se voir.

[Tutoriel suivant : 2. Connexion de plusieurs utilisateurs](mrlearning-sharing(photon)-ch2.md)
