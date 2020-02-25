---
title: Tutoriels de démarrage - 2. Initialisation de votre projet et de votre première application
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 11/01/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 9c219313ad6e73cde78efd8e5e718a466ebd6137
ms.sourcegitcommit: bd536f4f99c71418b55c121b7ba19ecbaf6336bb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "77554398"
---
# <a name="2-initializing-your-project-and-first-application"></a>2. Initialisation de votre projet et de votre première application

## <a name="overview"></a>Vue d’ensemble

<!-- TODO: Consider expanding to include summary of each tutorial in this tutorial series -->
Dans ce premier tutoriel, vous allez découvrir certaines fonctionnalités du <a href="https://github.com/microsoft/MixedRealityToolkit-Unity" target="_blank">Mixed Reality Toolkit (MRTK)</a>. Vous verrez également comment démarrer votre première application pour HoloLens 2 et la déployer sur l’appareil.

## <a name="objectives"></a>Objectifs

* Configurer Unity pour le développement HoloLens
* Importer les ressources et configurer la scène
* Visualiser le maillage du mappage spatial, les maillages de la main et le compteur de fréquence d’images

## <a name="prerequisites"></a>Prérequis

* PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)
* SDK Windows 10 (10.0.18362.0 ou version ultérieure)
* Capacité de programmation C# de base
* Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)
* <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté

> [!IMPORTANT]
> La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X. Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.

## <a name="create-new-unity-project"></a>Créer un projet Unity

Lancez **Unity Hub**, sélectionnez l’onglet **Projets**, puis cliquez sur la **flèche bas** en regard du bouton **Nouveau** :

![mrlearning-base](images/mrlearning-base/tutorial1-section1-step1-1.png)

Sélectionnez la version Unity spécifiée dans la section [Prérequis](#prerequisites) ci-dessus :

![mrlearning-base](images/mrlearning-base/tutorial1-section1-step1-2.png)

Dans la fenêtre Créer un projet :

* Vérifiez que **Modèles** est défini sur **3D**
* Entrez un **Nom du projet** approprié, par exemple _Tutoriels MRTK_
* Choisissez un **Emplacement** approprié pour stocker votre projet, par exemple _D:\MixedRealityLearning_
* Cliquez sur le bouton **Créer** pour créer et lancer votre nouveau projet Unity

![mrlearning-base](images/mrlearning-base/tutorial1-section1-step1-3.png)

> [!CAUTION]
> Quand vous utilisez Windows, il existe une limite de 255 caractères pour MAX_PATH. Unity est concerné par ces limites et la compilation risque d’échouer si un chemin de fichier dépasse 255 caractères. Par conséquent, il est vivement recommandé de stocker votre projet Unity aussi près que possible de la racine du lecteur.

Attendez qu’Unity crée le projet :

![mrlearning-base](images/mrlearning-base/tutorial1-section1-step1-4.png)

## <a name="configure-the-unity-project-for-windows-mixed-reality"></a>Configurer le projet Unity pour Windows Mixed Reality

<!-- TODO: Consider adding info about configuring Unity for WMR vs MRTK, or removing WMR section -->

Dans cette section, vous allez changer de plateforme de génération, activer la réalité virtuelle et activer la perception spatiale.

### <a name="1-switch-build-platform"></a>1. Changer de plateforme de génération

Dans le menu Unity, sélectionnez **Fichier** > **Paramètres de build...** pour ouvrir la fenêtre Paramètres de build :

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step1-1.png)

Dans la fenêtre Paramètres de build, sélectionnez **Plateforme Windows universelle** , puis cliquez sur le bouton **Switch Platform** (Changer de plateforme) :

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step1-2.png)

Attendez qu’Unity termine le changement de plateforme :

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step1-3.png)

Quand Unity a terminé le changement de plateforme, cliquez sur l’icône **x** rouge pour fermer la fenêtre Paramètres de build :

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step1-4.png)

### <a name="2-enable-virtual-reality"></a>2. Activer la réalité virtuelle

> [!NOTE]
> L’activation de la réalité virtuelle s’applique également aux casques de réalité mixte et de réalité augmentée, car elle fait référence à l’activation de la vision stéréoscopique (rendu d’images différentes pour chaque œil).

Dans le menu Unity, sélectionnez **Modifier** > **Paramètres du projet...** pour ouvrir la fenêtre Paramètres du projet :

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step2-1.png)

Dans la fenêtre Paramètres du projet, sélectionnez **Lecteur** > **Paramètres XR** pour développer les paramètres XR :

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step2-2.png)

Dans les paramètres XR, cochez la case **Virtual Reality Supported** (Prise en charge de la réalité virtuelle) pour activer la réalité virtuelle, puis cliquez sur l’icône **+** et sélectionnez **Windows Mixed Reality** pour ajouter le SDK Windows Mixed Reality :

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step2-3.png)

Attendez qu’Unity termine l’ajout du SDK :

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step2-4.png)

Quand Unity a terminé l’ajout du SDK, optimisez les paramètres XR comme suit :

* Définissez le **format d’intensité**  de Windows Mixed Reality sur une **profondeur de 16 bits**
* Cochez la case **Enable Depth Sharing** (Activer le partage de profondeur) de Windows Mixed Reality
* Définissez le **mode de rendu \*** stéréo sur **Single Pass Instanced** (Instanciation en un seul passage)

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step2-5.png)

> [!TIP]
> Pour en savoir plus sur l’optimisation d’Unity pour Windows Mixed Reality, vous pouvez consulter la documentation [Paramètres recommandés pour Unity](recommended-settings-for-unity.md).

### <a name="3-enable-spatial-perception"></a>3. Activer la perception spatiale

> [!NOTE]
> La perception spatiale permet de visualiser le maillage du mappage spatial sur des appareils Windows Mixed Reality.

Dans la fenêtre Paramètres du projet, sélectionnez **Lecteur** > **Paramètres de publication** pour développer les paramètres de publication :

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step3-1.png)

Dans les paramètres de publication, faites défiler vers le bas jusqu’à la section **Fonctionnalités**, puis cochez la case **SpatialPerception** :

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step3-2.png)

<!-- TODO: Consider adding info about audio spatializer plugin setting -->

Fermez la fenêtre Paramètres du projet.

## <a name="import-textmesh-pro-essential-resources"></a>Importer les ressources essentielles TextMeshPro

> [!NOTE]
> Nous importons ce package, car il est requis par les éléments d’interface utilisateur de Mixed Reality Toolkit.

Dans le menu Unity, sélectionnez **Fenêtre** > **TextMeshPro** > **Import TMP Essential Resources** (Importer les ressources essentielles TMP) :

![mrlearning-base](images/mrlearning-base/tutorial1-section3-step1-1.png)

Dans la fenêtre Import Unity Package (Importer un package Unity), cliquez sur le bouton **Tous** pour vous assurer que toutes les ressources sont sélectionnées, puis sur le bouton **Importer** pour importer les ressources :

![mrlearning-base](images/mrlearning-base/tutorial1-section3-step1-2.png)

## <a name="import-the-mixed-reality-toolkit"></a>Importer le Kit de ressources de réalité mixte

Téléchargez le package personnalisé Unity :

* [Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.3.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage)

Dans le menu Unity, sélectionnez **Ressources** > **Importer un package** > **Custom Package...** (Package personnalisé) pour ouvrir la fenêtre Importer un package... :

![mrlearning-base](images/mrlearning-base/tutorial1-section4-step1-1.png)

Dans la fenêtre Importer un package..., sélectionnez le package **Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage** que vous avez téléchargé, puis cliquez sur le bouton **Ouvrir** :

![mrlearning-base](images/mrlearning-base/tutorial1-section4-step1-2.png)

Dans la fenêtre Import Unity Package (Importer un package Unity), cliquez sur le bouton **Tous** pour vous assurer que toutes les ressources sont sélectionnées, puis sur le bouton **Importer** pour importer les ressources :

![mrlearning-base](images/mrlearning-base/tutorial1-section4-step1-3.png)

## <a name="configure-the-unity-project-for-the-mixed-reality-toolkit"></a>Configurer le projet Unity pour Mixed Reality Toolkit

<!-- TODO: Consider adding info about configuring Unity for WMR vs MRTK, or removing WMR section -->

Une fois le package importé, la fenêtre du configurateur de projet MRTK doit s’afficher. Si ce n’est pas le cas, ouvrez-la en sélectionnant **Mixed Reality Toolkit** > **Outils** > **Configure Unity Project** (Configurer un projet Unity) dans le menu Unity.

![mrlearning-base](images/mrlearning-base/tutorial1-section5-step1-1.png)

Dans la fenêtre du configurateur de projet MRTK, développez la section **Modify Configurations** (Modifier les configurations), <u>décochez</u> la case **Enable MSBuild for Unity** (Activer MSBuild for Unity), vérifiez que toutes les autres options sont cochées et cliquez sur le bouton **Appliquer** pour appliquer les paramètres :

![mrlearning-base](images/mrlearning-base/tutorial1-section5-step1-2.png)

> [!CAUTION]
> MSBuild for Unity ne prend peut-être pas en charge tous les SDK que vous utiliserez et peut être difficile à désactiver une fois qu’il a été activé. Par conséquent, il est vivement recommandé de ne pas activer MSBuild for Unity.

## <a name="configure-the-mixed-reality-toolkit"></a>Configurer le Kit de ressources de réalité mixte
<!-- TODO: Consider renaming to 'Add the Mixed Reality Toolkit to the Unity scene' -->

Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Add to Scene and Configure...** (Ajouter à la scène et configurer) pour ajouter Mixed Reality Toolkit à votre scène actuelle :

![mrlearning-base](images/mrlearning-base/tutorial1-section6-step1-1.png)

Une fois l’objet MixedRealityToolkit sélectionné dans la fenêtre Hiérarchie, dans la fenêtre de l’inspecteur, vérifiez que le profil de configuration Mixed Reality Toolkit est défini sur **DefaultMixedRealityToolkitConfigurationProfile** :

![mrlearning-base](images/mrlearning-base/tutorial1-section6-step1-2.png)

> [!IMPORTANT]
> Normalement, vous allez utiliser DefaultHoloLens2ConfigurationProfile lors du développement pour HoloLens 2. Toutefois, dans le cadre de ce tutoriel, vous allez utiliser DefaultMixedRealityToolkitConfigurationProfile, puis dans le tutoriel suivant, [Création de l’interface utilisateur et configuration du kit d’outils de réalité mixte](mrlearning-base-ch2.md), vous allez passer à DefaultHoloLens2ConfigurationProfile.

Dans le menu Unity, sélectionnez **Fichier** > **Enregistrer sous...** pour ouvrir la fenêtre Save Scene (Enregistrer la scène) :

![mrlearning-base](images/mrlearning-base/tutorial1-section6-step1-3.png)

Dans la fenêtre Enregistrer la scène, accédez au dossier **Scènes** de votre projet, donnez à votre scène un nom approprié, par exemple _Démarrage_, puis cliquez sur le bouton **Enregistrer** pour enregistrer la scène :

![mrlearning-base](images/mrlearning-base/tutorial1-section6-step1-4.png)

## <a name="build-your-application-to-your-device"></a>Générer votre application sur votre appareil

### <a name="1-build-the-unity-project"></a>1. Générer le projet Unity

Dans le menu Unity, sélectionnez **Fichier** > **Paramètres de build...** pour ouvrir la fenêtre Paramètres de build.

Dans la fenêtre Paramètres de build, cliquez sur le bouton **Add Open Scenes** (Ajouter des scènes ouvertes) pour ajouter votre scène actuelle à la liste **Scenes In Build** (Scènes dans la génération), puis cliquez sur le bouton **Générer** pour ouvrir la fenêtre de génération d’applications de plateforme Windows universelle :

![mrlearning-base](images/mrlearning-base/tutorial1-section7-step1-1.png)

Dans la fenêtre de génération d’applications de plateforme Windows universelle, choisissez un emplacement approprié pour stocker votre build, par exemple _D:\MixedRealityLearning\Builds_, créez un dossier et attribuez-lui un nom pertinent, par exemple _GettingStarted_, puis cliquez sur le bouton **Sélectionner un dossier** pour démarrer le processus de génération :

![mrlearning-base](images/mrlearning-base/tutorial1-section7-step1-2.png)

Attendez qu’Unity termine le processus de génération :

![mrlearning-base](images/mrlearning-base/tutorial1-section7-step1-3.png)

### <a name="2-build-and-deploy-the-application"></a>2. Générer et déployer l’application

Une fois le processus de génération terminé, Unity invite l’Explorateur de fichiers Windows à ouvrir l’emplacement où vous avez stocké la build. Naviguez dans le dossier, puis double-cliquez sur le fichier solution pour l’ouvrir dans Visual Studio :

![mrlearning-base](images/mrlearning-base/tutorial1-section7-step2-1.png)

> [!NOTE]
> Si Visual Studio vous invite à installer de nouveaux composants, prenez un moment pour vous assurer que tous les composants prérequis sont installés comme spécifié dans la documentation [Installer les outils](install-the-tools.md).

Configurez Visual Studio pour HoloLens 2 en sélectionnant la configuration **Master** ou **Release**, l’architecture **ARM** et **Appareil** comme cible :

![mrlearning-base](images/mrlearning-base/tutorial1-section7-step2-2.png)

Connectez votre HoloLens 2 à votre ordinateur.

> [!IMPORTANT]
> Avant d’effectuer la génération sur votre appareil, celui-ci doit être en mode développeur et associé à votre ordinateur de développement. Vous pouvez effectuer ces deux étapes en suivant [ces instructions](using-visual-studio.md).

L’étape finale consiste à effectuer la génération et le déploiement sur votre appareil. Pour cela, sélectionnez **Déboguer** > **Démarrer sans débogage** :

![mrlearning-base](images/mrlearning-base/tutorial1-section7-step2-3.png)

Bien que ces instructions supposent que vous déployez sur un appareil HoloLens 2, vous pouvez aussi déployer sur l’[émulateur HoloLens 2](using-the-hololens-emulator.md) ou créer un [package d’application pour effectuer un chargement indépendant](<https://docs.microsoft.com//windows/uwp/packaging/packaging-uwp-apps>).

Quand vous sélectionnez Démarrer sans débogage, l’application démarre immédiatement sur votre appareil si la génération réussit, mais le débogueur n’est pas attaché et les informations n’apparaissent pas dans Visual Studio. Cela signifie également que vous pouvez déconnecter le câble USB pendant que votre application s’exécute sur votre appareil HoloLens 2 sans arrêter celle-ci.

Pour effectuer le déploiement sur votre appareil sans que l’application ne démarre automatiquement, vous pouvez sélectionner Générer > Déployer la solution.

## <a name="congratulations"></a>Félicitations

<!-- TODO: Consider cleanup and adding in app screenshots -->
Vous venez de déployer votre première application HoloLens 2. À mesure que vous vous déplacez, vous devez voir un maillage de mappage spatial couvrant toutes les surfaces qui ont été perçues par HoloLens 2. En outre, vous devez voir des indicateurs sur vos mains et doigts pour le suivi de la main et un compteur de fréquence d’images pour vous tenir informé des performances de l’application. Ce ne sont là que quelques-uns des éléments fondamentaux immédiatement disponibles dans le Kit de ressources de réalité mixte. Au cours des tutoriels à venir, vous commencerez à ajouter du contenu et une interactivité à votre scène afin de pouvoir explorer pleinement les fonctionnalités d’HoloLens 2 et de Mixed Reality Toolkit.

> [!NOTE]
> Dans l’application, vous remarquerez peut-être le profileur de diagnostics, dont vous pouvez activer ou désactiver l’affichage à l’aide de la commande de reconnaissance vocale **Toogle Diagnostics** (Activer/désactiver les diagnostics). Toutefois, il est généralement recommandé de laisser le profileur visible à tout moment pendant le développement afin de comprendre quand les modifications apportées à l’application peuvent avoir un impact sur les performances, par exemple l’application HoloLens 2 doit [s’exécuter en continu à 60 images par seconde](understanding-performance-for-mixed-reality.md).

[Tutoriel suivant : 3. Création de l’interface utilisateur et configuration du kit d’outils de réalité mixte](mrlearning-base-ch2.md)
