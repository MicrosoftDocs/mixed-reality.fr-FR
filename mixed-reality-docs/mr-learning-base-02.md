---
title: Tutoriels de démarrage - 2. Initialisation de votre projet et déploiement de votre première application
description: Ce cours vous montre comment utiliser Mixed Reality Toolkit (MRTK) pour créer une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 11/01/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 4f72f70b9eaac159f7d9231e61f23d18d708d0c7
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86305255"
---
# <a name="2-initializing-your-project-and-deploying-your-first-application"></a>2. Initialisation de votre projet et déploiement de votre première application

## <a name="overview"></a>Vue d’ensemble

Dans ce tutoriel, vous allez apprendre à créer un nouveau projet Unity, à le configurer pour le développement <a href="https://github.com/microsoft/MixedRealityToolkit-Unity" target="_blank">MRTK (Mixed Reality Toolkit)</a> et à importer MRTK. Vous allez également effectuer la configuration, la génération et le déploiement de l’exemple de scène Unity de base depuis Visual Studio vers votre HoloLens 2 ou votre émulateur.

## <a name="objectives"></a>Objectifs

* Apprendre à configurer Unity pour le développement HoloLens
* Apprendre à créer et déployer votre application sur HoloLens
* Expérimenter le maillage du mappage spatial, les maillages de la main et le compteur de fréquence d’images

## <a name="creating-the-unity-project"></a>Création du projet Unity

Lancez **Unity Hub**, sélectionnez l’onglet **Projets**, puis cliquez sur la **flèche bas** en regard du bouton **Nouveau** :

![mr-learning-base](images/mr-learning-base/base-02-section1-step1-1.png)

Dans la liste déroulante, sélectionnez la **version** Unity spécifiée dans les [prérequis](mr-learning-base-01.md#prerequisites) :

![mr-learning-base](images/mr-learning-base/base-02-section1-step1-2.png)

> [!TIP]
> Si cette version spécifique d’Unity n’est pas disponible dans Unity Hub, vous pouvez lancer l’installation à partir de la page <a href="https://unity3d.com/get-unity/download/archive" target="_blank">Unity download archive</a>.

Dans la fenêtre Créer un projet :

* Vérifiez que **Modèles** est défini sur **3D**
* Entrez un **Nom du projet** approprié, par exemple _Tutoriels MRTK_
* Choisissez un **Emplacement** approprié pour stocker votre projet, par exemple _D:\MixedRealityLearning_
* Cliquez sur le bouton **Créer** pour créer et lancer votre nouveau projet Unity

![mr-learning-base](images/mr-learning-base/base-02-section1-step1-3.png)

> [!CAUTION]
> Quand vous utilisez Windows, il existe une limite de 255 caractères pour MAX_PATH. Par conséquent, vous devez enregistrer le projet Unity près de la racine du lecteur.

Attendez qu’Unity crée le projet :

![mr-learning-base](images/mr-learning-base/base-02-section1-step1-4.png)

## <a name="switching-the-build-platform"></a>Changement de plateforme de génération

Dans le menu Unity, sélectionnez **Fichier** > **Paramètres de build...** pour ouvrir la fenêtre Paramètres de build :

![mr-learning-base](images/mr-learning-base/base-02-section2-step1-1.png)

Dans la fenêtre Paramètres de build, sélectionnez **Plateforme Windows universelle** , puis cliquez sur le bouton **Switch Platform** (Changer de plateforme) :

![mr-learning-base](images/mr-learning-base/base-02-section2-step1-2.png)

Attendez qu’Unity termine le changement de plateforme :

![mr-learning-base](images/mr-learning-base/base-02-section2-step1-3.png)

Quand Unity a terminé le changement de plateforme, cliquez sur l’icône **x** rouge pour fermer la fenêtre Paramètres de build :

![mr-learning-base](images/mr-learning-base/base-02-section2-step1-4.png)

## <a name="importing-the-textmeshpro-essential-resources"></a>Importation des ressources TextMeshPro Essential

Dans le menu Unity, sélectionnez **Window** > **TextMeshPro** > **Import TMP Essential Resources** pour ouvrir la fenêtre Import Unity Package :

![mr-learning-base](images/mr-learning-base/base-02-section3-step1-1.png)

Dans la fenêtre Import Unity Package (Importer un package Unity), cliquez sur le bouton **Tous** pour vous assurer que toutes les ressources sont sélectionnées, puis sur le bouton **Importer** pour importer les ressources :

![mr-learning-base](images/mr-learning-base/base-02-section3-step1-2.png)

> [!TIP]
> Les ressources TextMeshPro Essential sont requises par les éléments de l’interface utilisateur de MRTK. Vous pouvez ignorer cette étape si vous ne prévoyez pas d’utiliser des éléments de l’interface utilisateur de MRTK dans votre projet.

## <a name="importing-the-mixed-reality-toolkit"></a>Importation du Mixed Reality Toolkit

Téléchargez le package personnalisé Unity :

* [Microsoft.MixedReality.Toolkit.Unity.Foundation.2.4.0.unitypackage](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.4.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.4.0.unitypackage)

Dans le menu Unity, sélectionnez **Ressources** > **Importer un package** > **Custom Package...** (Package personnalisé) pour ouvrir la fenêtre Importer un package... :

![mr-learning-base](images/mr-learning-base/base-02-section4-step1-1.png)

Dans la fenêtre Import package..., sélectionnez le package **Microsoft.MixedReality.Toolkit.Unity.Foundation.2.4.0.unitypackage** que vous avez téléchargé, puis cliquez sur le bouton **Open** :

![mr-learning-base](images/mr-learning-base/base-02-section4-step1-2.png)

Dans la fenêtre Import Unity Package (Importer un package Unity), cliquez sur le bouton **Tous** pour vous assurer que toutes les ressources sont sélectionnées, puis sur le bouton **Importer** pour importer les ressources :

![mr-learning-base](images/mr-learning-base/base-02-section4-step1-3.png)

## <a name="configuring-the-unity-project"></a>Configuration du projet Unity

### <a name="1-apply-the-mrtk-project-configurator-settings"></a>1. Appliquer les paramètres du configurateur de projet MRTK

Une fois que Unity a fini d’importer le package de la section précédente, la fenêtre MRTK Project Configurator doit s’afficher. Si ce n’est pas le cas, ouvrez la fenêtre Configurator en accédant au menu Unity et en sélectionnant **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project** :

![mr-learning-base](images/mr-learning-base/base-02-section5-step1-1.png)

Dans la fenêtre MRTK Project Configurator, développez la section **Modify Configurations**, vérifiez que toutes les options sont cochées, puis cliquez sur le bouton **Apply** pour appliquer les paramètres :

![mr-learning-base](images/mr-learning-base/base-02-section5-step1-2.png)

### <a name="2-configure-additional-project-settings"></a>2. Configurer des paramètres de projet supplémentaires

Dans le menu Unity, sélectionnez **Modifier** > **Paramètres du projet...** pour ouvrir la fenêtre Paramètres du projet :

![mr-learning-base](images/mr-learning-base/base-02-section5-step2-1.png)

Dans la fenêtre Project Settings, sélectionnez **Player** > **XR Settings**, cliquez sur l’icône **+** et sélectionnez Windows Mixed Reality pour ajouter le SDK Windows Mixed Reality :

![mr-learning-base](images/mr-learning-base/base-02-section5-step2-2.png)

Une fois que Unity a fini d’importer le SDK Windows Mixed Reality, la fenêtre MRTK Project Configurator doit réapparaître. Si ce n’est pas le cas, utilisez le menu Unity pour l’ouvrir.

Dans la fenêtre MRTK Project Configurator, utilisez la liste déroulante **Audio Spatializer** pour sélectionner le **MS HRTF Spatializer**, puis cliquez sur le bouton **Apply** pour appliquer le paramètre :

![mr-learning-base](images/mr-learning-base/base-02-section5-step2-3.png)

Dans la fenêtre Project Settings, sélectionnez **Player** > **XR Settings**, puis utilisez la liste déroulante **Depth Format** pour sélectionner **16-bit depth** :

![mr-learning-base](images/mr-learning-base/base-02-section5-step2-4.png)

Dans la fenêtre Project Settings, sélectionnez **Player** > **Publishing Settings** puis, dans le champ **Package name**, entrez un nom approprié, par exemple _MRTKTutorials-GettingStarted_ :

![mr-learning-base](images/mr-learning-base/base-02-section5-step2-5.png)

> [!NOTE]
> Le « Package name » est l’identificateur unique de l’application. Vous devez changer cet identificateur avant de déployer l’application afin d’éviter de remplacer des applications déjà installées.

> [!TIP]
> « Product Name » est le nom affiché dans le menu Démarrer de HoloLens. Pour faciliter la localisation de l’application pendant le développement, ajoutez un trait de soulignement devant le nom pour qu’il apparaisse en haut du classement.

## <a name="creating-and-configuring-the-scene"></a>Création et configuration de la scène

Dans le menu Unity, sélectionnez **File** > **New Scene** pour créer une scène :

![mr-learning-base](images/mr-learning-base/base-02-section6-step1-1.png)

Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Add to Scene and Configure...** pour ajouter le MRTK à votre scène actuelle :

![mr-learning-base](images/mr-learning-base/base-02-section6-step1-2.png)

Une fois l’objet **MixedRealityToolkit** sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, vérifiez que le profil de configuration **MixedRealityToolkit** est défini sur **DefaultMixedRealityToolkitConfigurationProfile** :

![mr-learning-base](images/mr-learning-base/base-02-section6-step1-3.png)

> [!IMPORTANT]
> En général, vous allez utiliser DefaultHoloLens2ConfigurationProfile lors du développement pour HoloLens. Cependant, dans le cadre de ce tutoriel, vous allez utiliser DefaultMixedRealityToolkitConfigurationProfile puis, dans le tutoriel suivant, [Configuration des profils MRTK](mr-learning-base-03.md), vous allez passer à DefaultHoloLens2ConfigurationProfile.

Dans le menu Unity, sélectionnez **Fichier** > **Enregistrer sous...** pour ouvrir la fenêtre Save Scene (Enregistrer la scène) :

![mr-learning-base](images/mr-learning-base/base-02-section6-step1-4.png)

Dans la fenêtre Enregistrer la scène, accédez au dossier **Scènes** de votre projet, donnez à votre scène un nom approprié, par exemple _Démarrage_, puis cliquez sur le bouton **Enregistrer** pour enregistrer la scène :

![mr-learning-base](images/mr-learning-base/base-02-section6-step1-5.png)

## <a name="building-your-application-to-your-hololens-2"></a>Génération de votre application sur votre HoloLens 2

### <a name="1-build-the-unity-project"></a>1. Générer le projet Unity

Dans le menu Unity, sélectionnez **Fichier** > **Paramètres de build...** pour ouvrir la fenêtre Paramètres de build.

Dans la fenêtre Paramètres de build, cliquez sur le bouton **Add Open Scenes** (Ajouter des scènes ouvertes) pour ajouter votre scène actuelle à la liste **Scenes In Build** (Scènes dans la génération), puis cliquez sur le bouton **Générer** pour ouvrir la fenêtre de génération d’applications de plateforme Windows universelle :

![mr-learning-base](images/mr-learning-base/base-02-section7-step1-1.png)

Dans la fenêtre de génération d’applications de plateforme Windows universelle, choisissez un emplacement approprié pour stocker votre build, par exemple _D:\MixedRealityLearning\Builds_, créez un dossier et attribuez-lui un nom pertinent, par exemple _GettingStarted_, puis cliquez sur le bouton **Sélectionner un dossier** pour démarrer le processus de génération :

![mr-learning-base](images/mr-learning-base/base-02-section7-step1-2.png)

Attendez qu’Unity termine le processus de génération :

![mr-learning-base](images/mr-learning-base/base-02-section7-step1-3.png)

### <a name="2-build-and-deploy-the-application"></a>2. Générer et déployer l’application

Une fois le processus de génération terminé, Unity invite l’Explorateur de fichiers Windows à ouvrir l’emplacement où vous avez stocké la build. Naviguez dans le dossier, puis double-cliquez sur le fichier solution pour l’ouvrir dans Visual Studio :

![mr-learning-base](images/mr-learning-base/base-02-section8-step1-1.png)

> [!NOTE]
> Si Visual Studio vous demande d’installer de nouveaux composants, prenez un moment pour vérifier que vous avez tous les composants prérequis comme spécifié dans la documentation **[Installer les outils](install-the-tools.md)** .

Configurez Visual Studio pour HoloLens en sélectionnant la configuration **Master** ou **Release**, l’architecture **ARM64** et **Appareil** comme cible :

![mr-learning-base](images/mr-learning-base/base-02-section8-step1-2.png)

> [!TIP]
> Si vous effectuez un déploiement sur HoloLens (1ère génération), sélectionnez l’architecture **x86**.

> [!NOTE]
> En général, pour HoloLens, vous allez générer pour l’architecture ARM. Il y a cependant un <a href="https://github.com/microsoft/MixedRealityToolkit-Unity" target="_blank"><strong>problème connu</strong></a> dans Unity 2019.3 qui provoque des erreurs lors de la sélection de ARM comme architecture de génération dans Visual Studio. La solution de contournement recommandée est de générer pour ARM64. Si ce n’est pas possible, accédez à **Modifier > Paramètres du projet > Lecteur > Autres paramètres** et désactivez **Travaux graphiques**.

> [!NOTE]
> Si vous ne voyez pas Appareil comme choix de cible, il peut être nécessaire de changer le projet de démarrage pour la solution Visual Studio de Projet IL2CPP en Projet UWP. Pour cela, dans l’Explorateur de solutions, cliquez avec le bouton droit sur nom_de_votre_projet (Windows universel), puis sélectionnez **Définir comme projet de démarrage**.

Connectez votre HoloLens à votre ordinateur, puis sélectionnez **Déboguer** > **Démarrer sans débogage** pour générer et déployer sur votre appareil :

![mr-learning-base](images/mr-learning-base/base-02-section8-step1-3.png)

> [!IMPORTANT]
> Avant d’effectuer la génération sur votre appareil, celui-ci doit être en mode développeur et associé à votre ordinateur de développement. Vous pouvez effectuer ces deux étapes en suivant [ces instructions](using-visual-studio.md).

> [!TIP]
> Vous pouvez aussi déployer sur l’[émulateur HoloLens](using-the-hololens-emulator.md) ou créer un [package d’application](https://docs.microsoft.com/windows/uwp/packaging/packaging-uwp-apps) pour un chargement indépendant (sideloading).

L’utilisation de Démarrer sans débogage démarre automatiquement l’application sur votre appareil sans le débogueur Visual Studio attaché.

Sélectionnez **Générer > Déployer la solution** pour déployer sur votre appareil sans que l’application ne démarre automatiquement.

> [!NOTE]
>Vous remarquerez peut-être le profileur de diagnostics dans l’application, que vous pouvez activer ou désactiver avec la commande vocale **Toggle Diagnostics**. Il est recommandé de garder le profileur visible la plupart du temps pendant le développement, de façon à comprendre quand des modifications apportées à l’application peuvent avoir un impact sur les performances. Par exemple, les applications HoloLens doivent [s’exécuter en continu à 60 images/s](understanding-performance-for-mixed-reality.md).

## <a name="congratulations"></a>Félicitations

Vous avez maintenant déployé votre première application HoloLens. À mesure que vous vous déplacez, vous devez voir un maillage de mappage spatial couvrant les surfaces qui sont perçues par HoloLens. En outre, vous devez voir des indicateurs sur vos mains et doigts pour le suivi de la main et un compteur de fréquence d’images pour vous tenir informé des performances de l’application. Ces fonctionnalités sont simplement quelques composants fondamentaux inclus avec MRTK. Dans les tutoriels à venir, vous allez ajouter du contenu à votre scène pour explorer les fonctionnalités HoloLens et MRTK.

[Tutoriel suivant : 3. Configuration des profils MRTK](mr-learning-base-03.md)
