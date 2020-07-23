---
title: Tutoriel sur le cloud Azure - 1. Azure Cloud Services pour HoloLens 2
description: Suivez ce cours pour découvrir comment implémenter différents services Azure dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: azure, réalité mixte, Unity, tutoriel, hololens, hololens 2, stockage blob azure, stockage table Azure, ancres spatiales azure, azure bot framework
ms.localizationpriority: high
ms.openlocfilehash: 649046f9416c880d6e69b544866fba60d3e43f4c
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86304452"
---
# <a name="1-azure-cloud-services-for-hololens-2"></a>1. Azure Cloud Services pour HoloLens 2

## <a name="overview"></a>Vue d’ensemble

Bienvenue dans cette série de tutoriels consacrés à l’intégration de services **cloud Azure** dans une application **HoloLens 2**. Dans cette série de cinq tutoriels, vous allez apprendre à intégrer plusieurs services **cloud Azure** dans un projet **Unity** pour **HoloLens 2**. Avec chaque chapitre consécutif, vous ajouterez de nouveaux services **cloud Azure** pour étendre les fonctionnalités de l’application et l’expérience utilisateur, tout en apprenant les principes fondamentaux de chaque service **cloud Azure**.

> [!NOTE]
> Cette série de tutoriels se concentrera sur **HoloLens 2**, mais en raison de la nature multiplateforme de Unity, la plus grande partie de ce que vous allez apprendre s’appliquera aussi aux applications pour poste de travail et pour smartphone.

Dans ce premier tutoriel, [Introduction à Azure Cloud Services pour HoloLens 2](mr-learning-azure-01.md), vous commencez par une explication des objectifs de l’application : vous présenter brièvement chaque service cloud Azure et configurer le projet Unity.

Dans le deuxième tutoriel, [Intégration de Stockage Azure](mr-learning-azure-02.md), vous commencez par intégrer le Stockage Azure comme solution de persistance pour l’application de démonstration, vous découvrez les différences entre Stockage Blob et Stockage Table, vous préparez les ressources de projet nécessaires, vous configurez la scène et vous vérifiez les opérations de lecture, de mise à jour et de suppression de données.

En poursuivant avec le troisième tutoriel, [Intégration d’Azure Custom Vision](mr-learning-azure-03.md), vous allez utiliser Azure Custom Vision pour entraîner et détecter des images dans l’application HoloLens 2. Le chapitre commence par la configuration de votre propre ressource Azure Custom Vision, la préparation des composants de la scène, et la mise en œuvre de l’entraînement et de la détection de vos propres images à partir de l’application.

Ensuite, vous passez au quatrième tutoriel, [Intégration d’Azure Spatial Anchors](mr-learning-azure-04.md), avec l’exploration du service Azure Spatial Anchors pour enregistrer et rechercher des emplacements, découvrir les concepts fondamentaux, préparer les ressources nécessaires, configurer la scène et commencer à utiliser la nouvelle fonctionnalité dans l’application.

Avec le cinquième tutoriel, [Intégration d’Azure Bot Service avec LUIS](mr-learning-azure-05.md), vous terminez en ajoutant à l’application une nouvelle méthode d’interaction utilisateur : le langage naturel ! Cette fonctionnalité sera réalisée avec Azure Bot Framework et LUIS (Language Understanding). Ce chapitre final vous fait découvrir les bases d’Azure Bot Service et, pour accélérer le processus, vous allez utiliser le composeur Bot Framework comme solution avec zéro code. Une fois le bot créé, vous allez l’intégrer dans la scène et l’exécuter avec l’application HoloLens 2 dans sa dernière version.

## <a name="application-goals"></a>Objectifs de l’application

Dans cette série de tutoriels, vous allez créer une application **HoloLens 2** capable de détecter des objets à partir d’images et de trouver leur emplacement spatial. Pour définir une terminologie du domaine, vous appelez à partir de maintenant ces entités des **objets suivis**.
L’utilisateur peut créer un **objet suivi** pour associer un ensemble d’images via la vision par ordinateur et/ou un emplacement spatial. Toutes les données doivent être conservées dans le cloud. De plus, certains aspects de l’application seront éventuellement contrôlés par le langage naturel via un bot.

### <a name="features"></a>Fonctionnalités

* Gestion de base des données et des images
* Entraînement et détection d’images
* Stockage d’un emplacement spatial et conseils pour ce stockage
* Assistant bot pour utiliser certaines fonctionnalités via le langage naturel

## <a name="azure-cloud-services"></a>Services cloud Azure

Pour implémenter les fonctionnalités requises pour l’application, vous devez utiliser ces services **cloud Azure** :

### <a name="azure-storage"></a>Stockage Azure

Vous allez utiliser [Stockage Azure](https://azure.microsoft.com/services/storage/) pour la solution de persistance. Il vous permet de stocker des données sur une table et de charger des données binaires volumineuses, comme des images.

### <a name="azure-custom-vision"></a>Azure Custom Vision

Avec [Azure Custom Vision](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/) (qui fait partie d’[Azure Cognitive Services](https://azure.microsoft.com/services/cognitive-services/)), vous pouvez associer à des *objets suivis* un ensemble d’images, entraîner un modèle Machine Learning sur l’ensemble d’images et détecter l’*objet suivi*.

### <a name="azure-spatial-anchors"></a>Azure Spatial Anchors

Pour stocker un emplacement d’*objet suivi* et donner des directions guidées pour le trouver, vous utilisez [Azure Spatial Anchors](https://azure.microsoft.com/services/spatial-anchors/).

### <a name="azure-bot-service"></a>Azure Bot Service

L’application est pilotée principalement par une interface utilisateur traditionnelle : vous utilisez donc [Azure Bot Service](https://azure.microsoft.com/services/bot-service/) pour ajouter une personnalité et faire office de nouvelle méthode d’interaction.

## <a name="prerequisites"></a>Prérequis

>[!TIP]
>Si vous n’avez pas encore terminé la série de [tutoriels de démarrage](mr-learning-base-01.md), nous vous conseillons de le faire avant d’aller plus loin.

* PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)
* SDK Windows 10 (10.0.18362.0 ou version ultérieure)
* Capacité de programmation C# de base
* Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)
* Une webcam connectée si vous voulez tester depuis l’éditeur Unity
* <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.3.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté

> [!CAUTION]
> La version Unity recommandée pour cette série de tutoriels est Unity 2019.3.X. Elle remplace toutes les versions Unity requises ou recommandées qui sont indiquées dans les prérequis ci-dessus.

## <a name="creating-and-preparing-the-unity-project"></a>Création et préparation du projet Unity

Dans cette section, vous allez créer un projet Unity et le préparer au développement avec MRTK.

Pour cela, suivez d’abord [Initialisation de votre projet et de votre première application](mr-learning-base-02.md), en excluant les instructions données dans [Générer votre application sur votre appareil](mr-learning-base-02.md#building-your-application-to-your-hololens-2), ce qui inclut les étapes suivantes :

1. [Création du projet Unity](mr-learning-base-02.md#creating-the-unity-project) et affectation d’un nom pertinent, par exemple *Azure Cloud Tutorials*
2. [Changement de plateforme de génération](mr-learning-base-02.md#configuring-the-unity-project)
3. [Importation des ressources TextMeshPro Essential](mr-learning-base-02.md#importing-the-textmeshpro-essential-resources)
4. [Importation du Mixed Reality Toolkit](mr-learning-base-02.md#importing-the-mixed-reality-toolkit)
5. [Configuration du projet Unity](mr-learning-base-02.md#configuring-the-unity-project)
6. [Création et configuration de la scène](mr-learning-base-02.md#creating-and-configuring-the-scene), et affectation d’un nom pertinent à la scène, par exemple *AzureCloudServices*

Ensuite, suivez les instructions de [Changer l’option d’affichage de la reconnaissance spatiale](mr-learning-base-03.md#changing-the-spatial-awareness-display-option) pour remplacer le profil de configuration MRTK de votre scène par **DefaultHoloLens2ConfigurationProfile** et remplacer les options d’affichage du maillage de la reconnaissance spatiale par **Occlusion**.

## <a name="installing-inbuilt-unity-packages"></a>Installation de packages Unity intégrés

Dans le menu Unity, sélectionnez **Window** > **Package Manager** pour ouvrir la fenêtre Package Manager, sélectionnez **AR Foundation**, puis cliquez sur le bouton **Install** pour installer le package :

![mr-learning-azure](images/mr-learning-asa/asa-02-section2-step1-1.png)

> [!NOTE]
> Vous installez le package intégré AR Foundation, car il est nécessaire pour le SDK Azure Spatial Anchors que vous allez importer dans la section suivante.

## <a name="importing-the-tutorial-assets"></a>Importation des ressources du tutoriel

Téléchargez et **importez** les packages personnalisés Unity suivants **dans l’ordre où ils sont listés** :

* [Stockage Azure pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/a-tag/AzureStorageForUnity.unitypackage)
* [Azure Spatial Anchors](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.2.1/AzureSpatialAnchors.unitypackage)
* [MRTK.Tutorials.AzureCloudServices](https://github.com/microsoft/MixedRealityLearning/releases/download/a-tag/MRTK.Tutorials.AzureCloudServices.unitypackage)

> [!TIP]
> Pour un rappel de la façon d’importer un package personnalisé Unity, vous pouvez vous référer aux instructions de [Importer le Kit de ressources de réalité mixte](mr-learning-base-02.md#importing-the-mixed-reality-toolkit).

Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :

![mr-learning-azure](images/mr-learning-azure/tutorial1-section4-step1-1.png)

## <a name="creating-and-preparing-the-scene"></a>Création et préparation de la scène
<!-- TODO: Consider renaming to 'Preparing the scene' -->

Dans cette section, vous allez préparer la scène en ajoutant une partie des préfabriqués du tutoriel.

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.AzureCloudServices** > **Prefabs** > **Manager**. Tout en maintenant le bouton Ctrl enfoncé, cliquez sur **SceneController**, **RootMenu** et **DataManager** pour sélectionner les trois préfabriqués :

![mr-learning-azure](images/mr-learning-azure/tutorial1-section5-step1-1.png)

**SceneController (prefab)** contient deux scripts, **SceneController (script)** et **UnityDispatcher (script)** . Le composant de script **SceneController** contient plusieurs fonctions d’expérience utilisateur et facilite la fonctionnalité de capture de photos, **UnityDispatcher** étant une classe helper pour autoriser les actions d’exécution sur le thread Unity principal.

**RootMenu (prefab)** est le préfabriqué d’interface utilisateur principal qui contient toutes les fenêtres d’interface utilisateur qui sont connectées l’une à l’autre via différents petits composants de script et qui contrôlent le flux général de l’interface utilisateur de l’application.

**DataManager (prefab)** est responsable de la communication avec le stockage Azure et il sera expliqué plus en détail dans le tutoriel suivant.

Les trois préfabriqués étant sélectionnés, faites-les maintenant glisser dans la fenêtre Hierarchy pour les ajouter à la scène :

![mr-learning-azure](images/mr-learning-azure/tutorial1-section5-step1-2.png)

Pour vous concentrer sur les objets de la scène, vous pouvez double-cliquer sur l’objet **RootMenu**, puis effectuer à nouveau un léger zoom arrière :

![mr-learning-azure](images/mr-learning-azure/tutorial1-section5-step1-3.png)

> [!TIP]
> Si vous trouvez gênantes les grandes icônes de votre scène, par exemple les grandes icônes « T », vous pouvez les masquer en <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">basculant le gizmos</a> sur la position Off.

## <a name="configuring-the-scene"></a>Configuration de la scène

Dans cette section, vous allez connecter ensemble *SceneManager*, *DataManager* et *RootMenu* pour avoir une scène de travail prête pour le tutoriel suivant, [Intégration de Stockage Azure](mr-learning-azure-01.md).

### <a name="connect-the-objects"></a>Connecter les objets

Dans la fenêtre Hierarchy, sélectionnez l’objet **DataManager** :

![mr-learning-azure](images/mr-learning-azure/tutorial1-section6-step1-1.png)

Dans la fenêtre Inspector, recherchez le composant **DataManager (Script)**  : vous verrez un emplacement vide sur l’événement **On Data Manager Ready ()** . À présent, dans la fenêtre Hierarchy, faites glisser l’objet **SceneController** dans l’événement **On Data Manager Ready ()** .

![mr-learning-azure](images/mr-learning-azure/tutorial1-section6-step1-2.png)

Vous remarquerez que le menu déroulant de l’événement est devenu actif. Cliquez sur le menu déroulant et accédez à **SceneController** puis, dans le sous-menu, sélectionnez l’option **Init ()**  :

![mr-learning-azure](images/mr-learning-azure/tutorial1-section6-step1-3.png)

Dans la fenêtre Hierarchy, sélectionnez l’objet **SceneController** ; dans l’inspecteur, vous trouvez le composant **SceneController** (script).

![mr-learning-azure](images/mr-learning-azure/tutorial1-section6-step1-4.png)

Vous voyez que plusieurs champs ne sont pas remplis : nous allons changer cela. Déplacez l’objet **DataManager** depuis la hiérarchie vers le champ *Data Manager* et déplacez le GameObject **RootMenu** depuis la hiérarchie vers le champ *Main Menu*.

![mr-learning-azure](images/mr-learning-azure/tutorial1-section6-step1-5.png)

Votre scène est maintenant prête pour les tutoriels suivants. N’oubliez pas de l’enregistrer dans votre projet.

## <a name="prepare-project-build-pipeline"></a>Préparer le pipeline de génération du projet

Alors que le projet doit encore être rempli avec du contenu, vous devez effectuer certaines préparations pour que le projet soit prêt à être généré pour **HoloLens 2**.

### <a name="1-add-additional-required-capabilities"></a>1. Ajouter des fonctionnalités supplémentaires nécessaires

Dans le menu Unity, sélectionnez **Modifier** > **Paramètres du projet...** pour ouvrir la fenêtre Paramètres du projet :

![mr-learning-azure](images/mr-learning-azure/tutorial1-section7-step1-1.png)

Dans la fenêtre Project Settings, sélectionnez **Player**, puis **Publishing Settings** :

![mr-learning-azure](images/mr-learning-azure/tutorial1-section7-step1-2.png)

Dans **Publishing Settings**, accédez à la section **Capabilities** et vérifiez bien que les fonctionnalités **InternetClient**, **Microphone** et **SpatialPerception**, que vous avez activées lors de la création du projet au début de ce tutoriel, sont activées. Activez ensuite les fonctionnalités **InternetClientServer**, **PrivateNetworkClientServer** et **Webcam** :

![mr-learning-azure](images/mr-learning-azure/tutorial1-section7-step1-3.png)

### <a name="2-deploy-the-app-to-your-hololens-2"></a>2. Déployer l’application sur votre HoloLens 2

Certaines des fonctionnalités que vous allez utiliser dans cette série de tutoriels ne peuvent pas s’exécuter dans l’éditeur Unity : cela signifie que vous devez être familiarisé avec le déploiement de l’application sur votre appareil HoloLens 2.

> [!TIP]
> Pour vous rappeler comment générer et déployer votre projet Unity sur HoloLens 2, vous pouvez vous référer aux instructions de [Tutoriels de démarrage - Générer votre application sur votre appareil](mr-learning-base-02.md#building-your-application-to-your-hololens-2).

### <a name="3-run-the-app-on-your-hololens-2-and-follow-the-in-app-instructions"></a>3. Exécuter l’application sur votre HoloLens 2 et suivre les instructions dans l’application

> [!CAUTION]
> Comme tous les services Azure utilisent Internet, vérifiez que votre appareil y est connecté.

Quand l’application s’exécute sur votre appareil, acceptez l’accès aux fonctionnalités demandées suivantes :

* Microphone
* Appareil photo

Ces fonctionnalités sont nécessaires pour que des services comme *Chat Bot* et *Custom Vision* fonctionnent correctement.

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez découvert la série de tutoriels, les fonctionnalités que vous allez implémenter et la façon dont les services **cloud Azure** permettent la réalisation de votre application *HoloLens 2*. Vous avez ajouté les composants nécessaires dans le projet et préparé la scène pour cette série de tutoriels.

Dans la leçon suivante, vous allez utiliser Stockage Azure comme solution de persistance cloud pour stocker des données et des images.

[Tutoriel suivant : 2. Intégration de Stockage Azure](mr-learning-azure-02.md)
