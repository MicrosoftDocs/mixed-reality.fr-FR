---
title: Tutoriel Azure Spatial Anchors - 1. Bien démarrer avec Azure Spatial Anchors
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 2a171d601d094375a56734e8d7890c9d3e17c887
ms.sourcegitcommit: e65f1463aec3c040a1cd042e61fc2bd156a42ff8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83866909"
---
# <a name="1-getting-started-with-azure-spatial-anchors"></a><span data-ttu-id="e4836-105">1. Bien démarrer avec Azure Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="e4836-105">1. Getting started with Azure Spatial Anchors</span></span>

## <a name="overview"></a><span data-ttu-id="e4836-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="e4836-106">Overview</span></span>

<span data-ttu-id="e4836-107">Bienvenue dans la deuxième série des tutoriels HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="e4836-107">Welcome to the second series of the HoloLens 2 tutorials.</span></span> <span data-ttu-id="e4836-108">Dans cette série de tutoriels en quatre parties, vous allez découvrir les principes de base d’Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="e4836-108">In this four-part tutorial series, you will learn the fundamentals of Azure Spatial Anchors.</span></span>

<span data-ttu-id="e4836-109">Dans ce premier tutoriel, [Bien démarrer avec Azure Spatial Anchors](mrlearning-asa-ch1.md), vous allez découvrir les différentes étapes nécessaires pour démarrer et arrêter une session Azure, et pour créer, charger et télécharger des ancres Azure sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="e4836-109">In this first tutorial, [Getting started with Azure Spatial Anchors](mrlearning-asa-ch1.md), you will explore the various steps required to start and stop an Azure session and create, upload, and download Azure anchors on a single device.</span></span>

<span data-ttu-id="e4836-110">Dans le deuxième tutoriel, [Enregistrement, récupération et partage d’ancres spatiales Azure](mrlearning-asa-ch2.md), vous allez découvrir comment enregistrer les ancres spatiales Azure dans plusieurs sessions d’application en enregistrant les informations des ancres dans le stockage d’HoloLens 2 et en partageant ces informations d’ancre sur d’autres appareils pour un alignement des ancres sur plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="e4836-110">In the second tutorial, [Saving, retrieving, and sharing Azure Spatial Anchors](mrlearning-asa-ch2.md), you will learn how to save Azure Spatial Anchors across multiple app sessions by saving anchor information to the HoloLens 2's storage and how to share this anchor information to other devices for a multi-device anchor alignment.</span></span>

<span data-ttu-id="e4836-111">Dans le troisième tutoriel, [Affichage des commentaires sur les ancres spatiales Azure](mrlearning-asa-ch3.md), vous allez découvrir comment fournir aux utilisateurs un feedback sur les événements et les états des ancres lors de l’utilisation d’Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="e4836-111">In the third tutorial, [Displaying Azure Spatial Anchor feedback](mrlearning-asa-ch3.md), you will learn how to provide users with feedback about anchor events and statuses when using Azure Spatial Anchors.</span></span>

<span data-ttu-id="e4836-112">Dans le quatrième tutoriel, [Azure Spatial Anchors pour Android et iOS](mrlearning-asa-ch4.md), vous allez découvrir comment créer votre projet et le déployer sur des appareils Android et iOS.</span><span class="sxs-lookup"><span data-stu-id="e4836-112">In the fourth tutorial, [Azure Spatial Anchors for Android and iOS](mrlearning-asa-ch4.md), you will learn how to build and deploy your project to Android and iOS devices.</span></span>

## <a name="objectives"></a><span data-ttu-id="e4836-113">Objectifs</span><span class="sxs-lookup"><span data-stu-id="e4836-113">Objectives</span></span>

* <span data-ttu-id="e4836-114">Découvrir les principes de base du développement avec Azure Spatial Anchors pour HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="e4836-114">Learn the fundamentals of developing with Azure Spatial Anchors for HoloLens 2</span></span>
* <span data-ttu-id="e4836-115">Créer, charger et télécharger des ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="e4836-115">Create, upload, and download spatial anchors</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4836-116">Prérequis</span><span class="sxs-lookup"><span data-stu-id="e4836-116">Prerequisites</span></span>

>[!TIP]
><span data-ttu-id="e4836-117">Si vous n’avez pas encore terminé la série de [tutoriels de démarrage](mrlearning-base.md), nous vous conseillons de le faire avant d’aller plus loin.</span><span class="sxs-lookup"><span data-stu-id="e4836-117">If you have not completed the [Getting started tutorials](mrlearning-base.md) series yet, it's recommended that you complete those tutorials first.</span></span>

* <span data-ttu-id="e4836-118">PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="e4836-118">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="e4836-119">SDK Windows 10 (10.0.18362.0 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="e4836-119">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="e4836-120">Capacité de programmation C# de base</span><span class="sxs-lookup"><span data-stu-id="e4836-120">Some basic C# programming ability</span></span>
* <span data-ttu-id="e4836-121">Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)</span><span class="sxs-lookup"><span data-stu-id="e4836-121">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>
* <span data-ttu-id="e4836-122"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté</span><span class="sxs-lookup"><span data-stu-id="e4836-122"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.2.X installed and the Universal Windows Platform Build Support module added</span></span>
* <span data-ttu-id="e4836-123">Suivez la section [Créer une ressource d’ancres spatiales](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) du tutoriel [Démarrage rapide : Créer une application HoloLens Unity qui utilise Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens).</span><span class="sxs-lookup"><span data-stu-id="e4836-123">Complete the [Create a Spatial Anchors resource](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) section of the [Quickstart: Create a Unity HoloLens app that uses Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) tutorial.</span></span>
* <span data-ttu-id="e4836-124">Si vous envisagez de déployer sur Android :</span><span class="sxs-lookup"><span data-stu-id="e4836-124">If you intend to deploy to Android</span></span>
    * <span data-ttu-id="e4836-125">Appareil Android <a href="https://developer.android.com/studio/debug/dev-options" target="_blank">en mode développeur</a> et <a href="https://developers.google.com/ar/discover/supported-devices" target="_blank">compatible avec ARCore</a> disposant d’une connexion USB à votre ordinateur Windows ou macOS</span><span class="sxs-lookup"><span data-stu-id="e4836-125">A <a href="https://developer.android.com/studio/debug/dev-options" target="_blank">developer enabled</a> and <a href="https://developers.google.com/ar/discover/supported-devices" target="_blank">ARCore capable</a> Android device with USB connection to your Windows or macOS computer</span></span>
    * <span data-ttu-id="e4836-126"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module Android Build Support ajouté</span><span class="sxs-lookup"><span data-stu-id="e4836-126"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.2.X installed and the Android Build Support module added</span></span>
* <span data-ttu-id="e4836-127">Si vous envisagez de déployer sur iOS :</span><span class="sxs-lookup"><span data-stu-id="e4836-127">If you intend to deploy to iOS</span></span>
    * <span data-ttu-id="e4836-128">Ordinateur macOS avec les dernières versions de <a href="https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12" target="_blank">Xcode</a> et de <a href="https://cocoapods.org" target="_blank">CocoaPods</a> installées</span><span class="sxs-lookup"><span data-stu-id="e4836-128">A macOS computer with the the latest version of <a href="https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12" target="_blank">Xcode</a> and <a href="https://cocoapods.org" target="_blank">CocoaPods</a> installed</span></span>
    * <span data-ttu-id="e4836-129">Appareil iOS <a href="https://developer.apple.com/documentation/arkit/verifying_device_support_and_user_permission" target="_blank">compatible avec ARKit</a> disposant d’une connexion USB à votre ordinateur macOS</span><span class="sxs-lookup"><span data-stu-id="e4836-129">An <a href="https://developer.apple.com/documentation/arkit/verifying_device_support_and_user_permission" target="_blank">ARKit compatible</a> iOS device with USB connection to your macOS computer</span></span>
    * <span data-ttu-id="e4836-130"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module iOS Build Support ajouté</span><span class="sxs-lookup"><span data-stu-id="e4836-130"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.2.X installed and the iOS Build Support module added</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4836-131">La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X.</span><span class="sxs-lookup"><span data-stu-id="e4836-131">The recommended Unity version for this tutorial series is Unity 2019.2.X.</span></span> <span data-ttu-id="e4836-132">Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="e4836-132">This supersedes any Unity version requirements or recommendations stated in the prerequisites linked above.</span></span>

## <a name="creating-the-unity-project"></a><span data-ttu-id="e4836-133">Création du projet Unity</span><span class="sxs-lookup"><span data-stu-id="e4836-133">Creating the Unity project</span></span>
<!-- TODO: Consider renaming to 'Creating and preparing the Unity project'-->

<span data-ttu-id="e4836-134">Dans cette section, vous allez créer un projet Unity et le préparer pour le développement avec MRTK.</span><span class="sxs-lookup"><span data-stu-id="e4836-134">In this section, you will create a new Unity project and get it ready for MRTK development.</span></span>

<span data-ttu-id="e4836-135">Pour cela, suivez d’abord [Initialisation de votre projet et de votre première application](mrlearning-base-ch1.md), en excluant les instructions données dans [Générer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device), ce qui inclut les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e4836-135">For this, first follow the [Initializing your project and first application](mrlearning-base-ch1.md), excluding the [Build your application to your device](mrlearning-base-ch1.md#build-your-application-to-your-device) instructions, which includes the following steps:</span></span>

1. <span data-ttu-id="e4836-136">[Créer un projet Unity](mrlearning-base-ch1.md#create-new-unity-project) et lui donner un nom approprié, par exemple *MRTK Tutorials*</span><span class="sxs-lookup"><span data-stu-id="e4836-136">[Create new Unity project](mrlearning-base-ch1.md#create-new-unity-project) and give it a suitable name, for example, *MRTK Tutorials*</span></span>

2. [<span data-ttu-id="e4836-137">Configurer le projet Unity pour Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="e4836-137">Configure the Unity project for Windows Mixed Reality</span></span>](mrlearning-base-ch1.md#configure-the-unity-project-for-windows-mixed-reality)

3. [<span data-ttu-id="e4836-138">Importer les ressources essentielles TextMeshPro</span><span class="sxs-lookup"><span data-stu-id="e4836-138">Import TextMesh Pro Essential Resources</span></span>](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources)

4. [<span data-ttu-id="e4836-139">Importer Mixed Reality Toolkit</span><span class="sxs-lookup"><span data-stu-id="e4836-139">Import the Mixed Reality Toolkit</span></span>](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit)

5. [<span data-ttu-id="e4836-140">Configurer le projet Unity pour le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="e4836-140">Configure the Unity project for the Mixed Reality Toolkit</span></span>](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit)

6. <span data-ttu-id="e4836-141">[Ajoutez le Kit de ressources de réalité mixte à la scène Unity](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) et donnez à la scène un nom approprié, par exemple *AzureSpatialAnchors*</span><span class="sxs-lookup"><span data-stu-id="e4836-141">[Add the Mixed Reality Toolkit to the Unity scene](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) and give the scene a suitable name, for example, *AzureSpatialAnchors*</span></span>

<span data-ttu-id="e4836-142">Ensuite, suivez les instructions de [Comment configurer les profils du Kit de ressources de réalité mixte (Modifier l’option d’affichage de la reconnaissance spatiale)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) pour changer le profil de configuration MRTK de votre scène en **DefaultHoloLens2ConfigurationProfile** et pour changer les options d’affichage du maillage de la reconnaissance spatiale en **Occlusion**.</span><span class="sxs-lookup"><span data-stu-id="e4836-142">Then follow the [How to configure the Mixed Reality Toolkit Profiles (Change Spatial Awareness Display Option)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) instructions to change the MRTK configuration profile for your scene to the **DefaultHoloLens2ConfigurationProfile** and change the display options for the spatial awareness mesh to **Occlusion**.</span></span>

> [!CAUTION]
> <span data-ttu-id="e4836-143">Comme mentionné dans les instructions de [Configurer le projet Unity pour le Kit de ressources de réalité mixte](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit) en lien ci-dessus, il est fortement recommandé de ne pas activer MSBuild pour Unity.</span><span class="sxs-lookup"><span data-stu-id="e4836-143">As mentioned in the [Configure the Unity project for the Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit) instructions linked above, it is strongly recommended to not enable MSBuild for Unity.</span></span>

## <a name="adding-inbuilt-unity-packages"></a><span data-ttu-id="e4836-144">Ajout de packages Unity intégrés</span><span class="sxs-lookup"><span data-stu-id="e4836-144">Adding inbuilt Unity packages</span></span>
<!-- TODO: Consider renaming to 'Installing AR Foundation' -->

<span data-ttu-id="e4836-145">Dans cette section, vous allez installer le package intégré AR Foundation d’Unity, car il est nécessaire pour le SDK Azure Spatial Anchors que vous allez importer dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="e4836-145">In this section, you will install Unity's inbuilt AR Foundation package because it is required by the Azure Spatial Anchors SDK you will import in the next section.</span></span>

<span data-ttu-id="e4836-146">Dans le menu Unity, sélectionnez **Window** > **Package Manager** :</span><span class="sxs-lookup"><span data-stu-id="e4836-146">In the Unity menu, select **Window** > **Package Manager**:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section2-step1-1.png)

> [!NOTE]
> <span data-ttu-id="e4836-148">Quelques secondes peuvent être nécessaires avant que le package AR Foundation apparaisse dans la liste.</span><span class="sxs-lookup"><span data-stu-id="e4836-148">It might take a few seconds before the AR Foundation package appears in the list.</span></span>

<span data-ttu-id="e4836-149">Dans la fenêtre Package Manage, sélectionnez **AR Foundation** et installez le package en cliquant sur le bouton **Install** :</span><span class="sxs-lookup"><span data-stu-id="e4836-149">In the Package Manager window, select **AR Foundation** and install the package by clicking the **Install** button:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section2-step1-2.png)

## <a name="importing-the-tutorial-assets"></a><span data-ttu-id="e4836-151">Importation des ressources du tutoriel</span><span class="sxs-lookup"><span data-stu-id="e4836-151">Importing the tutorial assets</span></span>

<span data-ttu-id="e4836-152">Téléchargez et **importez** les packages personnalisés Unity suivants **dans l’ordre où ils sont listés** :</span><span class="sxs-lookup"><span data-stu-id="e4836-152">Download and **import** the following Unity custom packages **in the order they are listed**:</span></span>

* <span data-ttu-id="e4836-153">[AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)</span><span class="sxs-lookup"><span data-stu-id="e4836-153">[AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)</span></span>
* [<span data-ttu-id="e4836-154">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage</span><span class="sxs-lookup"><span data-stu-id="e4836-154">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.3/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage)
* [<span data-ttu-id="e4836-155">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.1.unitypackage</span><span class="sxs-lookup"><span data-stu-id="e4836-155">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.1.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.3.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.1.unitypackage)

> [!TIP]
> <span data-ttu-id="e4836-156">Pour un rappel de la façon d’importer un package personnalisé Unity, vous pouvez vous référer aux instructions de [Importer le Kit de ressources de réalité mixte](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit).</span><span class="sxs-lookup"><span data-stu-id="e4836-156">For a reminder on how to import a Unity custom package, you can refer to the [Import the Mixed Reality Toolkit](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit) instructions.</span></span>

<span data-ttu-id="e4836-157">Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="e4836-157">After you have imported the tutorial assets your Project window should look similar to this:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section3-step1-1.png)

## <a name="creating-and-preparing-the-scene"></a><span data-ttu-id="e4836-159">Création et préparation de la scène</span><span class="sxs-lookup"><span data-stu-id="e4836-159">Creating and preparing the scene</span></span>
<!-- TODO: Consider renaming to 'Preparing the scene' -->

<span data-ttu-id="e4836-160">Dans cette section, vous allez préparer la scène en ajoutant une partie des préfabriqués du tutoriel.</span><span class="sxs-lookup"><span data-stu-id="e4836-160">In this section, you will prepare the scene by adding some of the tutorial prefabs.</span></span>

<span data-ttu-id="e4836-161">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.AzureSpatialAnchors** > **Prefabs**.</span><span class="sxs-lookup"><span data-stu-id="e4836-161">In the Project window, navigate to **Assets** > **MRTK.Tutorials.AzureSpatialAnchors** > **Prefabs** folder.</span></span> <span data-ttu-id="e4836-162">Tout en maintenant le bouton Ctrl enfoncé, cliquez sur **ButtonParent**, **DebugWindow**, **Instructions** et **ParentAnchor** pour sélectionner les quatre préfabriqués :</span><span class="sxs-lookup"><span data-stu-id="e4836-162">While holding down the CTRL button, click on **ButtonParent**, **DebugWindow**, **Instructions**, and **ParentAnchor** to select the four prefabs:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section4-step1-1.png)

<span data-ttu-id="e4836-164">Les quatre préfabriqués étant sélectionnés, faites-les glisser dans la fenêtre Hierarchy pour les ajouter à la scène :</span><span class="sxs-lookup"><span data-stu-id="e4836-164">With the four prefabs still selected, drag them into the Hierarchy window to add them to the scene:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section4-step1-2.png)

<span data-ttu-id="e4836-166">Pour vous concentrer sur les objets de la scène, vous pouvez double-cliquer sur l’objet ParentAnchor, puis effectuer un léger zoom arrière :</span><span class="sxs-lookup"><span data-stu-id="e4836-166">To focus in on the objects in the scene, you can double-click on the ParentAnchor object, and then zoom slightly out again:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section4-step1-3.png)

> [!TIP]
> <span data-ttu-id="e4836-168">Si vous trouvez gênantes les grandes icônes de votre scène, par exemple les grandes icônes « T », vous pouvez les masquer en <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">basculant le gizmos</a> sur la position Off.</span><span class="sxs-lookup"><span data-stu-id="e4836-168">If you find the large icons in your scene, for example, the large framed 'T' icons distracting, you can hide these by <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">toggling the Gizmos</a> to the off position.</span></span>

## <a name="configuring-the-buttons-to-operate-the-scene"></a><span data-ttu-id="e4836-169">Configuration des boutons pour faire fonctionner la scène</span><span class="sxs-lookup"><span data-stu-id="e4836-169">Configuring the buttons to operate the scene</span></span>

<span data-ttu-id="e4836-170">Dans cette section, vous allez ajouter des scripts dans la scène pour créer une série d’événements de bouton qui montrent les principes de base pour la façon dont les ancres locales et les ancres spatiales Azure se comportent dans une application.</span><span class="sxs-lookup"><span data-stu-id="e4836-170">In this section, you will add scripts into the scene to create a series of button events that demonstrate the fundamentals of how both local anchors and Azure Spatial Anchors behave in an application.</span></span>

### <a name="1-configure-the-pressable-button-holo-lens-2-script-component"></a><span data-ttu-id="e4836-171">1. Configurer le composant Pressable Button Holo Lens 2 (Script)</span><span class="sxs-lookup"><span data-stu-id="e4836-171">1. Configure the Pressable Button Holo Lens 2 (Script) component</span></span>

<span data-ttu-id="e4836-172">Dans la fenêtre Hierarchy, développez l’objet **ButtonParent** et sélectionnez le premier objet enfant nommé **StartAzureSession** :</span><span class="sxs-lookup"><span data-stu-id="e4836-172">In the Hierarchy window, expand the **ButtonParent** object and select the first child object named **StartAzureSession**:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section5-step1-1.png)

<span data-ttu-id="e4836-174">Dans la fenêtre Inspector, recherchez le composant **Pressable Button Holo Lens 2 (Script)** et ajoutez un nouvel écouteur d’événements à l’événement **Button Pressed ()** en cliquant sur l’icône **+**  :</span><span class="sxs-lookup"><span data-stu-id="e4836-174">In the Inspector window, locate the **Pressable Button Holo Lens 2 (Script)** component and add a new event listener to the **Button Pressed ()** event by clicking the **+** icon:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section5-step1-2.png)

<span data-ttu-id="e4836-176">Avec l’objet StartAzureSession sélectionné dans la fenêtre Hierarchy, cliquez avec le bouton droit sur l’objet **ParentAnchor** de la fenêtre Hierarchy, puis faites-le glisser vers le champ vide **None (Object)** de l’écouteur d’événements que vous venez d’ajouter, pour que l’objet ParentAnchor soit à l’écoute des événements Button Pressed () de ce bouton :</span><span class="sxs-lookup"><span data-stu-id="e4836-176">With the StartAzureSession object still selected in the Hierarchy window, click-and-drag the **ParentAnchor** object from the Hierarchy window into the empty **None (Object)** field of the event listener you just added to make the ParentAnchor object listen for button pressed events from this button:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section5-step1-3.png)

<span data-ttu-id="e4836-178">Cliquez sur la liste déroulante **No Function** du même écouteur d’événements, puis sélectionnez **AnchorModuleScript** > **StartAzureSession ()** pour définir la fonction StartAzureSession () comme action qui est déclenchée quand les événements Button Pressed () du bouton sont déclenchés à partir de ce bouton :</span><span class="sxs-lookup"><span data-stu-id="e4836-178">Click the **No Function** dropdown of the same event listener, then select **AnchorModuleScript** > **StartAzureSession ()** to set the StartAzureSession () function as the action that is triggered when the button pressed events is fired from this button:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section5-step1-4.png)

### <a name="2-configure-the-interactable-script-component"></a><span data-ttu-id="e4836-180">2. Configurer le composant Interactable (Script)</span><span class="sxs-lookup"><span data-stu-id="e4836-180">2. Configure the Interactable (Script) component</span></span>

<span data-ttu-id="e4836-181">Avec l’objet StartAzureSession sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, recherchez le composant **Interactable (Script)** et répétez le même processus qu’à l’étape 1 ci-dessus pour l’événement **OnClick ()**  :</span><span class="sxs-lookup"><span data-stu-id="e4836-181">With the StartAzureSession object still selected in the Hierarchy window, in the Inspector window, locate the **Interactable (Script)** component and repeat the same process as in step 1 above for the **OnClick ()** event:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section5-step2-1.png)

### <a name="3-configure-the-remaining-buttons"></a><span data-ttu-id="e4836-183">3. Configurer les boutons restants</span><span class="sxs-lookup"><span data-stu-id="e4836-183">3. Configure the remaining buttons</span></span>

<span data-ttu-id="e4836-184">Pour chacun des boutons restants, effectuez le processus décrit aux étapes 1 et 2 ci-dessus pour affecter des fonctions aux événements **Button Pressed ()** et **OnClick ()**  :</span><span class="sxs-lookup"><span data-stu-id="e4836-184">For each of the remaining buttons, complete the process outlined in step 1 and 2 above to assign functions to both the **Button Pressed ()** and **OnClick ()** events:</span></span>

* <span data-ttu-id="e4836-185">Pour l’objet **StopAzureSession**, affectez la fonction AnchorModuleScript > **StopAzureSession ()** .</span><span class="sxs-lookup"><span data-stu-id="e4836-185">For the **StopAzureSession** object, assign the AnchorModuleScript > **StopAzureSession ()** function.</span></span>
* <span data-ttu-id="e4836-186">Pour l’objet **CreateAzureAnchor**, affectez la fonction AnchorModuleScript > **CreateAzureAnchor ()** ,</span><span class="sxs-lookup"><span data-stu-id="e4836-186">For the **CreateAzureAnchor** object, assign the AnchorModuleScript > **CreateAzureAnchor ()** function,</span></span>
  * <span data-ttu-id="e4836-187">puis faites à nouveau glisser la **ParentAnchor** dans le champ vide **None (Game Object)** .</span><span class="sxs-lookup"><span data-stu-id="e4836-187">then drag the **ParentAnchor** again into the empty **None (Game Object)** field.</span></span>
* <span data-ttu-id="e4836-188">Pour l’objet **RemoveLocalAnchor**, affectez la fonction AnchorModuleScript > **RemoveLocalAnchor ()** ,</span><span class="sxs-lookup"><span data-stu-id="e4836-188">For the **RemoveLocalAnchor** object, assign the AnchorModuleScript > **RemoveLocalAnchor ()** function,</span></span>
  * <span data-ttu-id="e4836-189">puis faites à nouveau glisser la **ParentAnchor** dans le champ vide **None (Game Object)** .</span><span class="sxs-lookup"><span data-stu-id="e4836-189">then drag the **ParentAnchor** again into the empty **None (Game Object)** field.</span></span>
* <span data-ttu-id="e4836-190">Pour l’objet **FindAzureAnchor**, affectez la fonction AnchorModuleScript > **FindAzureAnchor ()** .</span><span class="sxs-lookup"><span data-stu-id="e4836-190">For the **FindAzureAnchor** object, assign the AnchorModuleScript > **FindAzureAnchor ()** function.</span></span>
* <span data-ttu-id="e4836-191">Pour l’objet **DeleteAzureAnchor**, affectez la fonction AnchorModuleScript > **DeleteAzureAnchor ()** .</span><span class="sxs-lookup"><span data-stu-id="e4836-191">For the **DeleteAzureAnchor** object, assign the AnchorModuleScript > **DeleteAzureAnchor ()** function.</span></span>

### <a name="4-connect-the-scene-to-the-azure-resource"></a><span data-ttu-id="e4836-192">4. Connecter la scène à la ressource Azure</span><span class="sxs-lookup"><span data-stu-id="e4836-192">4. Connect the scene to the Azure resource</span></span>

<span data-ttu-id="e4836-193">Dans la fenêtre Hierarchy, sélectionnez l’objet **ParentAnchor** et, dans la fenêtre Inspector, faites défiler jusqu’au composant **Spatial Anchor Manager (Script)** .</span><span class="sxs-lookup"><span data-stu-id="e4836-193">In the Hierarchy window, select the **ParentAnchor** object and in the Inspector window, scroll down to the **Spatial Anchor Manager (Script)** component.</span></span>

<span data-ttu-id="e4836-194">Ensuite, dans la section **Credentials**, collez votre ID et votre clé de compte Spatial Anchors, que vous avez créés dans le cadre des [Prérequis](mrlearning-asa-ch1.md#prerequisites) de ce tutoriel dans les champs **Spatial Anchors Account Id** et **Spatial Anchors Account Key** :</span><span class="sxs-lookup"><span data-stu-id="e4836-194">Then, in the **Credentials** section, paste your Spatial Anchors Account ID and Key, which you created as part of this tutorial's [Prerequisites](mrlearning-asa-ch1.md#prerequisites), into the corresponding **Spatial Anchors Account Id** and **Spatial Anchors Account Key** fields:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section5-step4-1.png)

## <a name="trying-the-basic-behaviors-of-azure-spatial-anchors"></a><span data-ttu-id="e4836-196">Essai des comportements de base d’Azure Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="e4836-196">Trying the basic behaviors of Azure Spatial Anchors</span></span>

<span data-ttu-id="e4836-197">Maintenant que votre scène est configurée pour montrer les principes de base d’Azure Spatial Anchors, il est temps de déployer l’application afin de pouvoir expérimenter directement Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="e4836-197">Now that your scene is configured to demonstrate the basics of Azure Spatial Anchors, it is time to deploy the app so you can experience Azure Spatial Anchors firsthand.</span></span>

### <a name="1-add-additional-required-capabilities"></a><span data-ttu-id="e4836-198">1. Ajouter des fonctionnalités supplémentaires nécessaires</span><span class="sxs-lookup"><span data-stu-id="e4836-198">1. Add additional required capabilities</span></span>

<span data-ttu-id="e4836-199">Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings :</span><span class="sxs-lookup"><span data-stu-id="e4836-199">In the Unity menu, select **Edit** > **Project Settings...** to open the Player Settings window:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section6-step1-1.png)

<span data-ttu-id="e4836-201">Dans la fenêtre Player Settings, sélectionnez **Player**, puis **Publishing Settings** :</span><span class="sxs-lookup"><span data-stu-id="e4836-201">In the Player Settings window, select **Player** and then **Publishing Settings**:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section6-step1-2.png)

<span data-ttu-id="e4836-203">Dans la section **Publishing Settings**, accédez à la section **Capabilities** et vérifiez bien que les fonctionnalités **InternetClient**, **Microphone** et **SpatialPerception**, que vous avez activées lors de la création du projet au début de ce tutoriel, sont activées.</span><span class="sxs-lookup"><span data-stu-id="e4836-203">In the  **Publishing Settings**, scroll down to the **Capabilities** section and double-check that the **InternetClient**, **Microphone**, and **SpatialPerception** capabilities, which you enabled when you created the project at the beginning of the tutorial, are enabled.</span></span> <span data-ttu-id="e4836-204">Activez ensuite les fonctionnalités **InternetClientServer**, **PrivateNetworkClientServer**, **RemovableStorage** et **Webcam** :</span><span class="sxs-lookup"><span data-stu-id="e4836-204">Then, enable the **InternetClientServer**, **PrivateNetworkClientServer**, **RemovableStorage**, and **Webcam** capabilities:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section6-step1-3.png)

### <a name="2-deploy-the-app-to-your-hololens-2"></a><span data-ttu-id="e4836-206">2. Déployer l’application sur votre HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="e4836-206">2. Deploy the app to your HoloLens 2</span></span>

<span data-ttu-id="e4836-207">Azure Spatial Anchors ne peut pas s’exécuter dans Unity : pour tester la fonctionnalité Azure Spatial Anchors, vous devez déployer le projet sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="e4836-207">Azure Spatial Anchors can not run in Unity, so to test the Azure Spatial Anchors functionality, you need to deploy the project to your device.</span></span>

> [!TIP]
> <span data-ttu-id="e4836-208">Pour un rappel de la façon de générer et déployer votre projet Unity sur HoloLens 2, vous pouvez vous référer aux instructions de [Générer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device).</span><span class="sxs-lookup"><span data-stu-id="e4836-208">For a reminder on how to build and deploy your Unity project to HoloLens 2, you can refer to the [Build your application to your device](mrlearning-base-ch1.md#build-your-application-to-your-device) instructions.</span></span>

### <a name="3-run-the-app-on-your-hololens-2-and-follow-the-in-app-instructions"></a><span data-ttu-id="e4836-209">3. Exécuter l’application sur votre HoloLens 2 et suivre les instructions dans l’application</span><span class="sxs-lookup"><span data-stu-id="e4836-209">3. Run the app on your HoloLens 2 and follow the in-app instructions</span></span>

> [!CAUTION]
> <span data-ttu-id="e4836-210">Azure Spatial Anchors utilise Internet pour enregistrer et charger les données des ancres : veillez donc à ce que votre appareil soit connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="e4836-210">Azure Spatial Anchors uses the internet to save and load the anchor data so make sure your device is connected to the internet.</span></span>

<span data-ttu-id="e4836-211">Quand l’application s’exécute sur votre appareil, suivez les instructions à l’écran affichées dans le panneau des instructions du tutoriel Azure Spatial Anchors :</span><span class="sxs-lookup"><span data-stu-id="e4836-211">When the application is running on your device, follow the on-screen instructions displayed on the Azure Spatial Anchor Tutorial Instructions panel:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section6-step3-1.png)

## <a name="anchoring-an-experience"></a><span data-ttu-id="e4836-213">Ancrage d’une expérience</span><span class="sxs-lookup"><span data-stu-id="e4836-213">Anchoring an experience</span></span>

<span data-ttu-id="e4836-214">Dans les sections précédentes, vous avez découverts les principes de base d’Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="e4836-214">In the previous sections, you learned the fundamentals of Azure Spatial Anchors.</span></span> <span data-ttu-id="e4836-215">Nous avons utilisé un cube pour représenter et visualiser l’objet de jeu parent avec l’ancre attachée.</span><span class="sxs-lookup"><span data-stu-id="e4836-215">We used a cube to represent and visualize the parent game object with the attached anchor.</span></span> <span data-ttu-id="e4836-216">Dans cette section, vous allez découvrir comment ancrer une expérience complète en la plaçant en tant qu’enfant de l’objet ParentAnchor.</span><span class="sxs-lookup"><span data-stu-id="e4836-216">In this section, you will learn how to anchor an entire experience by placing it as a child of the ParentAnchor object.</span></span>

### <a name="1-add-the-rocket-launcher-experience"></a><span data-ttu-id="e4836-217">1. Ajouter l’expérience Rocket Launcher</span><span class="sxs-lookup"><span data-stu-id="e4836-217">1. Add the Rocket Launcher experience</span></span>

<span data-ttu-id="e4836-218">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** > **RocketLauncher** et sélectionnez le préfabriqué **RocketLauncher_Complete** :</span><span class="sxs-lookup"><span data-stu-id="e4836-218">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** > **RocketLauncher** folder and select the **RocketLauncher_Complete** prefab:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section7-step1-1.png)

<span data-ttu-id="e4836-220">Le préfabriqué RocketLauncher_Complete étant sélectionné, faites-le glisser par-dessus l’objet **ParentAnchor** dans la fenêtre Hierarchy pour en faire un enfant de l’objet ParentAnchor :</span><span class="sxs-lookup"><span data-stu-id="e4836-220">With the RocketLauncher_Complete prefab still selected, drag it on top of the **ParentAnchor** object in the Hierarchy window to make it a child of the ParentAnchor object:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section7-step1-2.png)

### <a name="2-reposition-the-rocket-launcher-experience"></a><span data-ttu-id="e4836-222">2. Repositionner l’expérience Rocket Launcher</span><span class="sxs-lookup"><span data-stu-id="e4836-222">2. Reposition the Rocket Launcher experience</span></span>

<span data-ttu-id="e4836-223">Positionnez, faites pivoter et mettez à l’échelle l’objet **RocketLauncher_Complete**  à une échelle et une orientation appropriées, tout en veillant à ce que l’objet **ParentAnchor** soit toujours exposé, par exemple :</span><span class="sxs-lookup"><span data-stu-id="e4836-223">Position, rotate, and scale the **RocketLauncher_Complete** object to a suitable scale and orientation, while also ensuring the **ParentAnchor** object is still exposed, for example:</span></span>

* <span data-ttu-id="e4836-224">Changez **Position** en X = 0 ; Y = 0 ; Z = 3,75</span><span class="sxs-lookup"><span data-stu-id="e4836-224">Transform **Position** X = 0, Y = 0, Z = 3.75</span></span>
* <span data-ttu-id="e4836-225">Changez **Rotation** en X = 0 ; Y = 90 ; Z = 0</span><span class="sxs-lookup"><span data-stu-id="e4836-225">Transform **Rotation** X = 0, Y = 90, Z = 0</span></span>
* <span data-ttu-id="e4836-226">Changez **Scale** en X = 10 ; Y = 10 ; Z = 10</span><span class="sxs-lookup"><span data-stu-id="e4836-226">Transform **Scale** X = 10, Y = 10, Z = 10</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial1-section7-step2-1.png)

<span data-ttu-id="e4836-228">Dans l’application, les utilisateurs peuvent maintenant repositionner l’intégralité de l’expérience Rocket Launcher en déplaçant le cube.</span><span class="sxs-lookup"><span data-stu-id="e4836-228">In the application, users may now reposition the entire Rocket Launcher experience by moving the cube.</span></span>

> [!TIP]
> <span data-ttu-id="e4836-229">Il existe un grand nombre de flux d’expériences utilisateur pour repositionner les expériences, notamment l’utilisation d’un objet de repositionnement (comme le cube utilisé dans ce tutoriel), l’utilisation d’un bouton pour basculer un cadre englobant qui entoure l’expérience, l’utilisation de gizmos de position et de rotation, etc.</span><span class="sxs-lookup"><span data-stu-id="e4836-229">There are a variety of user experience flows for repositioning experiences including the use of a repositioning object (such as the cube used in this tutorial), the use of a button to toggle a bounding box that surrounds the experience, the use of position and rotation gizmos, and more.</span></span>

## <a name="congratulations"></a><span data-ttu-id="e4836-230">Félicitations</span><span class="sxs-lookup"><span data-stu-id="e4836-230">Congratulations</span></span>

<span data-ttu-id="e4836-231">Dans ce tutoriel, vous avez découverts les principes de base d’Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="e4836-231">In this tutorial, you learned the fundamentals of Azure Spatial Anchors.</span></span> <span data-ttu-id="e4836-232">Ce tutoriel vous a fourni plusieurs boutons qui vous permettent d’explorer les différentes étapes nécessaires pour démarrer et arrêter une session Azure Spatial Anchors, et pour créer, charger et télécharger des ancres spatiales Azure sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="e4836-232">The tutorial provided you with several buttons that let you explore the various steps required to start and stop an Azure Spatial Anchors session and create, upload and download Azure Spatial Anchors on a single device.</span></span>

<span data-ttu-id="e4836-233">Dans la leçon suivante, vous allez découvrir comment enregistrer des ID d’ancre Azure dans votre HoloLens 2 pour pouvoir les récupérer même après le redémarrage de l’application, et comment transférer des ID d’ancre entre plusieurs appareils pour obtenir un alignement spatial.</span><span class="sxs-lookup"><span data-stu-id="e4836-233">In the next lesson, you will learn how to save Azure anchor IDs to your HoloLens 2 for retrieval, even after the application is restarted, and how to transfer anchor IDs between multiple devices to achieve spatial alignment.</span></span>

[<span data-ttu-id="e4836-234">Leçon suivante : 2. Enregistrement, récupération et partage d’ancres spatiales Azure</span><span class="sxs-lookup"><span data-stu-id="e4836-234">Next Lesson: 2. Saving, retrieving and sharing Azure Spatial Anchors</span></span>](mrlearning-asa-ch2.md)
