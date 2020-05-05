---
title: Tutoriel Azure Spatial Anchors - 1. Bien démarrer avec Azure Spatial Anchors
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: d0fd22ad6fbefc6889373b00847721cfc0655ce3
ms.sourcegitcommit: 92ff5478a5c55b4e2c5cc2f44f1588702f4ec5d1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82605000"
---
# <a name="1-getting-started-with-azure-spatial-anchors"></a>1. Bien démarrer avec Azure Spatial Anchors

## <a name="overview"></a>Vue d’ensemble

Bienvenue dans la deuxième série des tutoriels HoloLens 2. Dans cette série de tutoriels en trois parties, vous allez découvrir les principes de base d’Azure Spatial Anchors.

Dans ce premier tutoriel, [Bien démarrer avec Azure Spatial Anchors](mrlearning-asa-ch1.md), vous allez découvrir les différentes étapes nécessaires pour démarrer et arrêter une session Azure, et pour créer, charger et télécharger des ancres Azure sur un appareil.

Dans le deuxième tutoriel, [Enregistrement, récupération et partage d’ancres spatiales Azure](mrlearning-asa-ch2.md), vous allez découvrir comment enregistrer les ancres spatiales Azure dans plusieurs sessions d’application en enregistrant les informations des ancres dans le stockage d’HoloLens 2 et en partageant ces informations d’ancre sur d’autres appareils pour un alignement des ancres sur plusieurs appareils.

Dans le troisième tutoriel, [Affichage des commentaires sur les ancres spatiales Azure](mrlearning-asa-ch3.md), vous allez découvrir comment fournir aux utilisateurs un feedback sur les événements et les états des ancres lors de l’utilisation d’Azure Spatial Anchors.

## <a name="objectives"></a>Objectifs

* Découvrir les principes de base du développement avec Azure Spatial Anchors pour HoloLens 2
* Créer, charger et télécharger des ancres spatiales

## <a name="prerequisites"></a>Prérequis

>[!TIP]
>Si vous n’avez pas encore terminé la série de [tutoriels de démarrage](mrlearning-base.md), nous vous conseillons de le faire avant d’aller plus loin.

* PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)
* SDK Windows 10 (10.0.18362.0 ou version ultérieure)
* Capacité de programmation C# de base
* Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)
* <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté
* Suivez la section [Créer une ressource d’ancres spatiales](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) du tutoriel [Démarrage rapide : Créer une application HoloLens Unity qui utilise Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens).

> [!IMPORTANT]
> La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X. Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.

## <a name="creating-the-unity-project"></a>Création du projet Unity
<!-- TODO: Consider renaming to 'Creating and preparing the Unity project'-->

Dans cette section, vous allez créer un projet Unity et le préparer pour le développement avec MRTK.

Pour cela, suivez d’abord [Initialisation de votre projet et de votre première application](mrlearning-base-ch1.md), en excluant les instructions données dans [Générer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device), ce qui inclut les étapes suivantes :

1. [Créer un projet Unity](mrlearning-base-ch1.md#create-new-unity-project) et lui donner un nom approprié, par exemple *MRTK Tutorials*

2. [Configurer le projet Unity pour Windows Mixed Reality](mrlearning-base-ch1.md#configure-the-unity-project-for-windows-mixed-reality)

3. [Importer les ressources essentielles TextMeshPro](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources)

4. [Importer Mixed Reality Toolkit](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit)

5. [Configurer le projet Unity pour le Kit de ressources de réalité mixte](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit)

6. [Ajoutez le Kit de ressources de réalité mixte à la scène Unity](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) et donnez à la scène un nom approprié, par exemple *AzureSpatialAnchors*

Ensuite, suivez les instructions de [Comment configurer les profils du Kit de ressources de réalité mixte (Modifier l’option d’affichage de la reconnaissance spatiale)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) pour changer le profil de configuration MRTK de votre scène en **DefaultHoloLens2ConfigurationProfile** et pour changer les options d’affichage du maillage de la reconnaissance spatiale en **Occlusion**.

> [!CAUTION]
> Comme mentionné dans les instructions de [Configurer le projet Unity pour le Kit de ressources de réalité mixte](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit) en lien ci-dessus, il est fortement recommandé de ne pas activer MSBuild pour Unity.

## <a name="adding-inbuilt-unity-packages"></a>Ajout de packages Unity intégrés
<!-- TODO: Consider renaming to 'Installing AR Foundation' -->

Dans cette section, vous allez installer le package intégré AR Foundation d’Unity, car il est nécessaire pour le SDK Azure Spatial Anchors que vous allez importer dans la section suivante.

Dans le menu Unity, sélectionnez **Window** > **Package Manager** :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section2-step1-1.png)

> [!NOTE]
> Quelques secondes peuvent être nécessaires avant que le package AR Foundation apparaisse dans la liste.

Dans la fenêtre Package Manage, sélectionnez **AR Foundation** et installez le package en cliquant sur le bouton **Install** :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section2-step1-2.png)

## <a name="importing-the-tutorial-assets"></a>Importation des ressources du tutoriel

Téléchargez et **importez** les packages personnalisés Unity suivants **dans l’ordre où ils sont listés** :

* [AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)
* [MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.3/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage)
* [MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.1.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.3.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.1.unitypackage)

> [!TIP]
> Pour un rappel de la façon d’importer un package personnalisé Unity, vous pouvez vous référer aux instructions de [Importer le Kit de ressources de réalité mixte](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit).

Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section3-step1-1.png)

## <a name="creating-and-preparing-the-scene"></a>Création et préparation de la scène
<!-- TODO: Consider renaming to 'Preparing the scene' -->

Dans cette section, vous allez préparer la scène en ajoutant une partie des préfabriqués du tutoriel.

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.AzureSpatialAnchors** > **Prefabs**. Tout en maintenant le bouton Ctrl enfoncé, cliquez sur **ButtonParent**, **DebugWindow**, **Instructions** et **ParentAnchor** pour sélectionner les quatre préfabriqués :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section4-step1-1.png)

Les quatre préfabriqués étant sélectionnés, faites-les glisser dans la fenêtre Hierarchy pour les ajouter à la scène :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section4-step1-2.png)

Pour vous concentrer sur les objets de la scène, vous pouvez double-cliquer sur l’objet ParentAnchor, puis effectuer un léger zoom arrière :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section4-step1-3.png)

> [!TIP]
> Si vous trouvez gênantes les grandes icônes de votre scène, par exemple les grandes icônes « T », vous pouvez les masquer en <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">basculant le gizmos</a> sur la position Off.

## <a name="configuring-the-buttons-to-operate-the-scene"></a>Configuration des boutons pour faire fonctionner la scène

Dans cette section, vous allez ajouter des scripts dans la scène pour créer une série d’événements de bouton qui montrent les principes de base pour la façon dont les ancres locales et les ancres spatiales Azure se comportent dans une application.

### <a name="1-configure-the-pressable-button-holo-lens-2-script-component"></a>1. Configurer le composant Pressable Button Holo Lens 2 (Script)

Dans la fenêtre Hierarchy, développez l’objet **ButtonParent** et sélectionnez le premier objet enfant nommé **StartAzureSession** :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section5-step1-1.png)

Dans la fenêtre Inspector, recherchez le composant **Pressable Button Holo Lens 2 (Script)** et ajoutez un nouvel écouteur d’événements à l’événement **Button Pressed ()** en cliquant sur l’icône **+**  :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section5-step1-2.png)

Avec l’objet StartAzureSession sélectionné dans la fenêtre Hierarchy, cliquez avec le bouton droit sur l’objet **ParentAnchor** de la fenêtre Hierarchy, puis faites-le glisser vers le champ vide **None (Object)** de l’écouteur d’événements que vous venez d’ajouter, pour que l’objet ParentAnchor soit à l’écoute des événements Button Pressed () de ce bouton :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section5-step1-3.png)

Cliquez sur la liste déroulante **No Function** du même écouteur d’événements, puis sélectionnez **AnchorModuleScript** > **StartAzureSession ()** pour définir la fonction StartAzureSession () comme action qui est déclenchée quand les événements Button Pressed () du bouton sont déclenchés à partir de ce bouton :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section5-step1-4.png)

### <a name="2-configure-the-interactable-script-component"></a>2. Configurer le composant Interactable (Script)

Avec l’objet StartAzureSession sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, recherchez le composant **Interactable (Script)** et répétez le même processus qu’à l’étape 1 ci-dessus pour l’événement **OnClick ()**  :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section5-step2-1.png)

### <a name="3-configure-the-remaining-buttons"></a>3. Configurer les boutons restants

Pour chacun des boutons restants, effectuez le processus décrit aux étapes 1 et 2 ci-dessus pour affecter des fonctions aux événements **Button Pressed ()** et **OnClick ()**  :

* Pour l’objet **StopAzureSession**, affectez la fonction AnchorModuleScript > **StopAzureSession ()** .
* Pour l’objet **CreateAzureAnchor**, affectez la fonction AnchorModuleScript > **CreateAzureAnchor ()** ,
  * puis faites à nouveau glisser la **ParentAnchor** dans le champ vide **None (Game Object)** .
* Pour l’objet **RemoveLocalAnchor**, affectez la fonction AnchorModuleScript > **RemoveLocalAnchor ()** ,
  * puis faites à nouveau glisser la **ParentAnchor** dans le champ vide **None (Game Object)** .
* Pour l’objet **FindAzureAnchor**, affectez la fonction AnchorModuleScript > **FindAzureAnchor ()** .
* Pour l’objet **DeleteAzureAnchor**, affectez la fonction AnchorModuleScript > **DeleteAzureAnchor ()** .

### <a name="4-connect-the-scene-to-the-azure-resource"></a>4. Connecter la scène à la ressource Azure

Dans la fenêtre Hierarchy, sélectionnez l’objet **ParentAnchor** et, dans la fenêtre Inspector, faites défiler jusqu’au composant **Spatial Anchor Manager (Script)** .

Ensuite, dans la section **Credentials**, collez votre ID et votre clé de compte Spatial Anchors, que vous avez créés dans le cadre des [Prérequis](mrlearning-asa-ch1.md#prerequisites) de ce tutoriel dans les champs **Spatial Anchors Account Id** et **Spatial Anchors Account Key** :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section5-step4-1.png)

## <a name="trying-the-basic-behaviors-of-azure-spatial-anchors"></a>Essai des comportements de base d’Azure Spatial Anchors

Maintenant que votre scène est configurée pour montrer les principes de base d’Azure Spatial Anchors, il est temps de déployer l’application afin de pouvoir expérimenter directement Azure Spatial Anchors.

### <a name="1-add-additional-required-capabilities"></a>1. Ajouter des fonctionnalités supplémentaires nécessaires

Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section6-step1-1.png)

Dans la fenêtre Player Settings, sélectionnez **Player**, puis **Publishing Settings** :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section6-step1-2.png)

Dans la section **Publishing Settings**, accédez à la section **Capabilities** et vérifiez bien que les fonctionnalités **InternetClient**, **Microphone** et **SpatialPerception**, que vous avez activées lors de la création du projet au début de ce tutoriel, sont activées. Activez ensuite les fonctionnalités **InternetClientServer**, **PrivateNetworkClientServer**, **RemovableStorage** et **Webcam** :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section6-step1-3.png)

### <a name="2-deploy-the-app-to-your-hololens-2"></a>2. Déployer l’application sur votre HoloLens 2

Azure Spatial Anchors ne peut pas s’exécuter dans Unity : pour tester la fonctionnalité Azure Spatial Anchors, vous devez déployer le projet sur votre appareil.

> [!TIP]
> Pour un rappel de la façon de générer et déployer votre projet Unity sur HoloLens 2, vous pouvez vous référer aux instructions de [Générer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device).

### <a name="3-run-the-app-on-your-hololens-2-and-follow-the-in-app-instructions"></a>3. Exécuter l’application sur votre HoloLens 2 et suivre les instructions dans l’application

> [!CAUTION]
> Azure Spatial Anchors utilise Internet pour enregistrer et charger les données des ancres : veillez donc à ce que votre appareil soit connecté à Internet.

Quand l’application s’exécute sur votre appareil, suivez les instructions à l’écran affichées dans le panneau des instructions du tutoriel Azure Spatial Anchors :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section6-step3-1.png)

## <a name="anchoring-an-experience"></a>Ancrage d’une expérience

Dans les sections précédentes, vous avez découverts les principes de base d’Azure Spatial Anchors. Nous avons utilisé un cube pour représenter et visualiser l’objet de jeu parent avec l’ancre attachée. Dans cette section, vous allez découvrir comment ancrer une expérience complète en la plaçant en tant qu’enfant de l’objet ParentAnchor.

### <a name="1-add-the-rocket-launcher-experience"></a>1. Ajouter l’expérience Rocket Launcher

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** > **RocketLauncher** et sélectionnez le préfabriqué **RocketLauncher_Complete** :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section7-step1-1.png)

Le préfabriqué RocketLauncher_Complete étant sélectionné, faites-le glisser par-dessus l’objet **ParentAnchor** dans la fenêtre Hierarchy pour en faire un enfant de l’objet ParentAnchor :

![mrlearning-asa](images/mrlearning-asa/tutorial1-section7-step1-2.png)

### <a name="2-reposition-the-rocket-launcher-experience"></a>2. Repositionner l’expérience Rocket Launcher

Positionnez, faites pivoter et mettez à l’échelle l’objet **RocketLauncher_Complete**  à une échelle et une orientation appropriées, tout en veillant à ce que l’objet **ParentAnchor** soit toujours exposé, par exemple :

* Changez **Position** en X = 0 ; Y = 0 ; Z = 3,75
* Changez **Rotation** en X = 0 ; Y = 90 ; Z = 0
* Changez **Scale** en X = 10 ; Y = 10 ; Z = 10

![mrlearning-asa](images/mrlearning-asa/tutorial1-section7-step2-1.png)

Dans l’application, les utilisateurs peuvent maintenant repositionner l’intégralité de l’expérience Rocket Launcher en déplaçant le cube.

> [!TIP]
> Il existe un grand nombre de flux d’expériences utilisateur pour repositionner les expériences, notamment l’utilisation d’un objet de repositionnement (comme le cube utilisé dans ce tutoriel), l’utilisation d’un bouton pour basculer un cadre englobant qui entoure l’expérience, l’utilisation de gizmos de position et de rotation, etc.

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez découverts les principes de base d’Azure Spatial Anchors. Ce tutoriel vous a fourni plusieurs boutons qui vous permettent d’explorer les différentes étapes nécessaires pour démarrer et arrêter une session Azure Spatial Anchors, et pour créer, charger et télécharger des ancres spatiales Azure sur un appareil.

Dans la leçon suivante, vous allez découvrir comment enregistrer des ID d’ancre Azure dans votre HoloLens 2 pour pouvoir les récupérer même après le redémarrage de l’application, et comment transférer des ID d’ancre entre plusieurs appareils pour obtenir un alignement spatial.

[Leçon suivante : 2. Enregistrement, récupération et partage d’ancres spatiales Azure](mrlearning-asa-ch2.md)
