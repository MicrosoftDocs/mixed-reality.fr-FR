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
# <a name="1-setting-up-photon-unity-networking"></a><span data-ttu-id="83e91-105">1. Configuration de Photon Unity Networking</span><span class="sxs-lookup"><span data-stu-id="83e91-105">1. Setting up Photon Unity Networking</span></span>

## <a name="overview"></a><span data-ttu-id="83e91-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="83e91-106">Overview</span></span>

<span data-ttu-id="83e91-107">Dans ce tutoriel, vous allez découvrir comment préparer la création d’une expérience partagée à l’aide de Photon Unity Networking (PUN).</span><span class="sxs-lookup"><span data-stu-id="83e91-107">In this tutorial, you will learn how to prepare for creating a shared experience using Photon Unity Networking (PUN).</span></span> <span data-ttu-id="83e91-108">Photon est l’une des nombreuses options de mise en réseau accessibles aux développeurs de réalité mixte pour créer des expériences partagées.</span><span class="sxs-lookup"><span data-stu-id="83e91-108">Photon is one of several networking options available to Mixed Reality developers to create shared experiences.</span></span> <span data-ttu-id="83e91-109">Vous allez voir comment créer une application Photon PUN, importer des ressources Photon PUN dans votre projet Unity et connecter votre projet Unity à l’application Photon PUN.</span><span class="sxs-lookup"><span data-stu-id="83e91-109">You will learn how to create a Photon PUN application, import Photon PUN assets into your Unity project, and connect your Unity project to the Photon PUN application.</span></span>

## <a name="objectives"></a><span data-ttu-id="83e91-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="83e91-110">Objectives</span></span>

* <span data-ttu-id="83e91-111">Découvrir comment créer une application Photon PUN</span><span class="sxs-lookup"><span data-stu-id="83e91-111">Learn how to create a Photon PUN application</span></span>
* <span data-ttu-id="83e91-112">Découvrir comment trouver et importer les ressources Photon PUN</span><span class="sxs-lookup"><span data-stu-id="83e91-112">Learn how to find and import the Photon PUN assets</span></span>
* <span data-ttu-id="83e91-113">Découvrir comment connecter votre projet Unity à l’application Photon PUN</span><span class="sxs-lookup"><span data-stu-id="83e91-113">Learn how to connect your Unity project to the Photon PUN application</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83e91-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="83e91-114">Prerequisites</span></span>

>[!TIP]
><span data-ttu-id="83e91-115">Si vous n’avez pas encore effectué les [tutoriels de démarrage](mrlearning-base.md) et les [tutoriels sur les ancres spatiales Azure](mrlearning-asa-ch1.md), nous vous conseillons de le faire avant d’aller plus loin.</span><span class="sxs-lookup"><span data-stu-id="83e91-115">If you have not completed the [Getting started tutorials](mrlearning-base.md) and [Azure Spatial Anchors tutorials](mrlearning-asa-ch1.md) tutorial series yet, it's recommended that you complete those tutorials first.</span></span>

* <span data-ttu-id="83e91-116">PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="83e91-116">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="83e91-117">SDK Windows 10 (10.0.18362.0 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="83e91-117">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="83e91-118">Capacité de programmation C# de base</span><span class="sxs-lookup"><span data-stu-id="83e91-118">Some basic C# programming ability</span></span>
* <span data-ttu-id="83e91-119">Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)</span><span class="sxs-lookup"><span data-stu-id="83e91-119">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>
* <span data-ttu-id="83e91-120"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté</span><span class="sxs-lookup"><span data-stu-id="83e91-120"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.2.X installed and the Universal Windows Platform Build Support module added</span></span>
* <span data-ttu-id="83e91-121">Suivez la section [Créer une ressource d’ancres spatiales](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) du tutoriel [Démarrage rapide : Créer une application HoloLens Unity qui utilise Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens).</span><span class="sxs-lookup"><span data-stu-id="83e91-121">Complete the [Create a Spatial Anchors resource](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) section of the [Quickstart: Create a Unity HoloLens app that uses Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) tutorial</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83e91-122">La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X.</span><span class="sxs-lookup"><span data-stu-id="83e91-122">The recommended Unity version for this tutorial series is Unity 2019.2.X.</span></span> <span data-ttu-id="83e91-123">Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="83e91-123">This supersedes any Unity version requirements or recommendations stated in the prerequisites linked above.</span></span>

## <a name="creating-and-preparing-the-unity-project"></a><span data-ttu-id="83e91-124">Création et préparation du projet Unity</span><span class="sxs-lookup"><span data-stu-id="83e91-124">Creating and preparing the Unity project</span></span>

<span data-ttu-id="83e91-125">Dans cette section, vous allez créer un projet Unity et le préparer au développement avec MRTK.</span><span class="sxs-lookup"><span data-stu-id="83e91-125">In this section, you will create a new Unity project and get it ready for MRTK development.</span></span>

<span data-ttu-id="83e91-126">Pour cela, suivez d’abord [Initialisation de votre projet et de votre première application](mrlearning-base-ch1.md), en excluant les instructions données dans [Générer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device), ce qui inclut les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="83e91-126">For this, first follow the [Initializing your project and first application](mrlearning-base-ch1.md), excluding the [Build your application to your device](mrlearning-base-ch1.md#build-your-application-to-your-device) instructions, which includes the following steps:</span></span>

1. <span data-ttu-id="83e91-127">[Créer un projet Unity](mrlearning-base-ch1.md#create-new-unity-project) et lui donner un nom approprié, par exemple *MRTK Tutorials*</span><span class="sxs-lookup"><span data-stu-id="83e91-127">[Create new Unity project](mrlearning-base-ch1.md#create-new-unity-project) and give it a suitable name, for example, *MRTK Tutorials*</span></span>

2. [<span data-ttu-id="83e91-128">Configurer le projet Unity pour Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="83e91-128">Configure the Unity project for Windows Mixed Reality</span></span>](mrlearning-base-ch1.md#configure-the-unity-project-for-windows-mixed-reality)

3. [<span data-ttu-id="83e91-129">Importer les ressources essentielles TextMeshPro</span><span class="sxs-lookup"><span data-stu-id="83e91-129">Import TextMesh Pro Essential Resources</span></span>](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources)

4. [<span data-ttu-id="83e91-130">Importer Mixed Reality Toolkit</span><span class="sxs-lookup"><span data-stu-id="83e91-130">Import the Mixed Reality Toolkit</span></span>](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit)

5. [<span data-ttu-id="83e91-131">Configurer le projet Unity pour Mixed Reality Toolkit</span><span class="sxs-lookup"><span data-stu-id="83e91-131">Configure the Unity project for the Mixed Reality Toolkit</span></span>](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit)

6. <span data-ttu-id="83e91-132">[Ajouter le Mixed Reality Toolkit à la scène Unity](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) et donner à la scène un nom approprié, par exemple *MultiUserCapabilities*</span><span class="sxs-lookup"><span data-stu-id="83e91-132">[Add the Mixed Reality Toolkit to the Unity scene](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) and give the scene a suitable name, for example, *MultiUserCapabilities*</span></span>

<span data-ttu-id="83e91-133">Ensuite, suivez les instructions de [Comment configurer les profils du Kit de ressources de réalité mixte (Modifier l’option d’affichage de la reconnaissance spatiale)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) pour changer le profil de configuration MRTK de votre scène en **DefaultHoloLens2ConfigurationProfile** et pour changer les options d’affichage du maillage de la reconnaissance spatiale en **Occlusion**.</span><span class="sxs-lookup"><span data-stu-id="83e91-133">Then follow the [How to configure the Mixed Reality Toolkit Profiles (Change Spatial Awareness Display Option)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) instructions to change the MRTK configuration profile for your scene to the **DefaultHoloLens2ConfigurationProfile** and change the display options for the spatial awareness mesh to **Occlusion**.</span></span>

> [!CAUTION]
> <span data-ttu-id="83e91-134">Comme mentionné dans les instructions de l’étape [Configurer le projet Unity pour Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit) dont le lien est disponible ci-dessus, il est fortement recommandé de ne pas activer MSBuild pour Unity.</span><span class="sxs-lookup"><span data-stu-id="83e91-134">As mentioned in the [Configure the Unity project for the Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit) instructions linked above, it is strongly recommended to not enable MSBuild for Unity.</span></span>

## <a name="configuring-the-capabilities"></a><span data-ttu-id="83e91-135">Configuration des fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="83e91-135">Configuring the capabilities</span></span>

<span data-ttu-id="83e91-136">Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings, puis recherchez la section **Player** >  **Publishing Settings** :</span><span class="sxs-lookup"><span data-stu-id="83e91-136">In the Unity menu, select **Edit** > **Project Settings...** to open the Player Settings window, then locate the **Player** >  **Publishing Settings** section:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section2-step1-1.png)

<span data-ttu-id="83e91-138">Dans la section **Publishing Settings**, accédez à la section **Capabilities** et vérifiez bien que les fonctionnalités **InternetClient**, **Microphone** et **SpatialPerception**, que vous avez activées lors de la création du projet au début de ce tutoriel, sont activées.</span><span class="sxs-lookup"><span data-stu-id="83e91-138">In the  **Publishing Settings**, scroll down to the **Capabilities** section and double-check that the **InternetClient**, **Microphone**, and **SpatialPerception** capabilities, which you enabled when you created the project at the beginning of the tutorial, are enabled.</span></span> <span data-ttu-id="83e91-139">Activez ensuite les fonctionnalités **InternetClientServer**, **PrivateNetworkClientServer** et **RemovableStorage** :</span><span class="sxs-lookup"><span data-stu-id="83e91-139">Then, enable the **InternetClientServer**, **PrivateNetworkClientServer**, and **RemovableStorage** capabilities:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section2-step1-2.png)

## <a name="adding-inbuilt-unity-packages"></a><span data-ttu-id="83e91-141">Ajout de packages Unity intégrés</span><span class="sxs-lookup"><span data-stu-id="83e91-141">Adding inbuilt Unity packages</span></span>
<!-- TODO: Consider renaming to 'Installing AR Foundation' -->

<span data-ttu-id="83e91-142">Dans cette section, vous allez installer le package intégré AR Foundation d’Unity, car il est nécessaire pour le SDK Azure Spatial Anchors que vous allez importer dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="83e91-142">In this section, you will install Unity's inbuilt AR Foundation package because it is required by the Azure Spatial Anchors SDK you will import in the next section.</span></span>

<span data-ttu-id="83e91-143">Dans le menu Unity, sélectionnez **Window** > **Package Manager** :</span><span class="sxs-lookup"><span data-stu-id="83e91-143">In the Unity menu, select **Window** > **Package Manager**:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section3-step1-1.png)

> [!NOTE]
> <span data-ttu-id="83e91-145">Quelques secondes peuvent être nécessaires avant que le package AR Foundation apparaisse dans la liste.</span><span class="sxs-lookup"><span data-stu-id="83e91-145">It might take a few seconds before the AR Foundation package appears in the list.</span></span>

<span data-ttu-id="83e91-146">Dans la fenêtre Package Manage, sélectionnez **AR Foundation** et installez le package en cliquant sur le bouton **Install** :</span><span class="sxs-lookup"><span data-stu-id="83e91-146">In the Package Manager window, select **AR Foundation** and install the package by clicking the **Install** button:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section3-step1-2.png)

## <a name="importing-the-tutorial-assets"></a><span data-ttu-id="83e91-148">Importation des ressources du tutoriel</span><span class="sxs-lookup"><span data-stu-id="83e91-148">Importing the tutorial assets</span></span>

<span data-ttu-id="83e91-149">Téléchargez et **importez** les packages personnalisés Unity suivants **dans l’ordre où ils sont listés** :</span><span class="sxs-lookup"><span data-stu-id="83e91-149">Download and **import** the following Unity custom packages **in the order they are listed**:</span></span>

* <span data-ttu-id="83e91-150">[AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)</span><span class="sxs-lookup"><span data-stu-id="83e91-150">[AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)</span></span>
* [<span data-ttu-id="83e91-151">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage</span><span class="sxs-lookup"><span data-stu-id="83e91-151">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.3/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage)
* [<span data-ttu-id="83e91-152">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.1.unitypackage</span><span class="sxs-lookup"><span data-stu-id="83e91-152">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.1.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.3.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.1.unitypackage)
* [<span data-ttu-id="83e91-153">MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.3.0.0.unitypackage</span><span class="sxs-lookup"><span data-stu-id="83e91-153">MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.3.0.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/multi-user-capabilities-v2.3.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.3.0.0.unitypackage)

> [!TIP]
> <span data-ttu-id="83e91-154">Pour un rappel de la façon d’importer un package personnalisé Unity, vous pouvez vous référer aux instructions de [Importer le Kit de ressources de réalité mixte](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit).</span><span class="sxs-lookup"><span data-stu-id="83e91-154">For a reminder on how to import a Unity custom package, you can refer to the [Import the Mixed Reality Toolkit](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit) instructions.</span></span>

<span data-ttu-id="83e91-155">Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="83e91-155">After you have imported the tutorial assets your Project window should look similar to this:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section4-step1-1.png)

> [!NOTE]
> <span data-ttu-id="83e91-157">Après l’importation du package de ressources du tutoriel MultiUserCapabilities, la fenêtre de console contient plusieurs erreurs [CS0246](https://docs.microsoft.com/dotnet/csharp/language-reference/compiler-messages/cs0246) qui indiquent que le type ou l’espace de noms est manquant.</span><span class="sxs-lookup"><span data-stu-id="83e91-157">After importing the MultiUserCapabilities tutorial assets package, you will see several [CS0246](https://docs.microsoft.com/dotnet/csharp/language-reference/compiler-messages/cs0246) errors in the Console window stating that the type or namespace is missing.</span></span> <span data-ttu-id="83e91-158">Ces erreurs sont attendues et seront résolues dans la section suivante quand vous importerez les ressources Photon.</span><span class="sxs-lookup"><span data-stu-id="83e91-158">This is to be expected and will be resolved in the next section when you import the Photon assets.</span></span>

## <a name="importing-the-photon-assets"></a><span data-ttu-id="83e91-159">Importation des ressources Photon</span><span class="sxs-lookup"><span data-stu-id="83e91-159">Importing the Photon assets</span></span>

<span data-ttu-id="83e91-160">Dans cette section, vous allez importer les ressources Photon Unity Network (PUN) du magasin de ressources d’Unity.</span><span class="sxs-lookup"><span data-stu-id="83e91-160">In this section, you will import the Photon Unity Network (PUN) assets from Unity's Asset Store.</span></span>

<span data-ttu-id="83e91-161">Dans le menu Unity, sélectionnez **Window** > **Asset Store** pour ouvrir la fenêtre Asset Store, recherchez et sélectionnez **PUN 2 - FREE** dans Exit Games, puis cliquez sur le bouton **Download** pour télécharger le package de ressources dans votre compte Unity :</span><span class="sxs-lookup"><span data-stu-id="83e91-161">In the Unity menu, select **Window** > **Asset Store** to open the Asset Store window, search for and select **PUN 2 - FREE** from Exit Games, and then click the **Download** button to download the asset package to your Unity account:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section5-step1-1.png)

<span data-ttu-id="83e91-163">Une fois le téléchargement terminé, cliquez sur le bouton **Importer** pour ouvrir la fenêtre Import Unity Package :</span><span class="sxs-lookup"><span data-stu-id="83e91-163">When the download is complete, click the **Import** button to open the Import Unity Package window:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section5-step1-2.png)

<span data-ttu-id="83e91-165">Dans la fenêtre Import Unity Package (Importer un package Unity), cliquez sur le bouton **Tous** pour vous assurer que toutes les ressources sont sélectionnées, puis sur le bouton **Importer** pour importer les ressources :</span><span class="sxs-lookup"><span data-stu-id="83e91-165">In the Import Unity Package window, click the **All** button to ensure all the assets are selected, then click the **Import** button to import the assets:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section5-step1-3.png)

<span data-ttu-id="83e91-167">Une fois le processus d’importation terminé dans Unity, la fenêtre Pun Wizard apparaît avec le menu PUN Setup chargé. Vous pouvez ignorer ou fermer cette fenêtre pour l’instant :</span><span class="sxs-lookup"><span data-stu-id="83e91-167">Once Unity has completed the import process, the Pun Wizard window will appear with the PUN Setup menu loaded, you can ignore or close this window for now:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section5-step1-4.png)

## <a name="setting-up-photon"></a><span data-ttu-id="83e91-169">Configuration de Photon</span><span class="sxs-lookup"><span data-stu-id="83e91-169">Setting up Photon</span></span>

<span data-ttu-id="83e91-170">Dans cette section, vous allez créer un compte Photon si vous n’en avez pas déjà un, puis créer une application PUN.</span><span class="sxs-lookup"><span data-stu-id="83e91-170">In this section, you will create a Photon account, if you don't already have one, and create a new PUN application.</span></span>

<span data-ttu-id="83e91-171">Accédez au<a href="https://dashboard.photonengine.com/account/signin" target="_blank">tableau de bord</a> Photon et connectez-vous si vous disposez déjà d’un compte que vous souhaitez utiliser. Sinon, cliquez sur le lien **Create One** et suivez les instructions pour inscrire un nouveau compte :</span><span class="sxs-lookup"><span data-stu-id="83e91-171">Navigate to the Photon <a href="https://dashboard.photonengine.com/account/signin" target="_blank">dashboard</a> and sign in if you already have an account you want to use, otherwise, click the **Create One** link and follow the instructions to register a new account:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section6-step1-1.png)

<span data-ttu-id="83e91-173">Une fois connecté, cliquez sur le bouton **Create a New App** :</span><span class="sxs-lookup"><span data-stu-id="83e91-173">Once signed in, click the **Create a New App** button:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section6-step1-2.png)

<span data-ttu-id="83e91-175">Dans la page Create a New Application, entrez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="83e91-175">On the Create a New Application page, enter the following values:</span></span>

* <span data-ttu-id="83e91-176">Pour Photon Type, sélectionnez Photon PUN.</span><span class="sxs-lookup"><span data-stu-id="83e91-176">For Photon Type, select Photon PUN</span></span>
* <span data-ttu-id="83e91-177">Pour Nom, entrez un nom approprié, par exemple _MRTK Tutorials_.</span><span class="sxs-lookup"><span data-stu-id="83e91-177">For Name, enter a suitable name, for example, _MRTK Tutorials_</span></span>
* <span data-ttu-id="83e91-178">Pour Description, entrez éventuellement une description appropriée.</span><span class="sxs-lookup"><span data-stu-id="83e91-178">For Description, optionally enter a suitable description</span></span>
* <span data-ttu-id="83e91-179">Laissez le champ URL vide.</span><span class="sxs-lookup"><span data-stu-id="83e91-179">For Url, leave the field empty</span></span>

<span data-ttu-id="83e91-180">Cliquez ensuite sur le bouton **Créer** pour créer l’application :</span><span class="sxs-lookup"><span data-stu-id="83e91-180">Then click the **Create** button to create the new application:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section6-step1-3.png)

<span data-ttu-id="83e91-182">Une fois le processus de création terminé dans Photon, la nouvelle application PUN apparaît dans votre tableau de bord :</span><span class="sxs-lookup"><span data-stu-id="83e91-182">Once Photon has finished the creation process, the new PUN application will appear on your dashboard:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section6-step1-4.png)

## <a name="connecting-the-unity-project-to-the-pun-application"></a><span data-ttu-id="83e91-184">Connexion du projet Unity à l’application PUN</span><span class="sxs-lookup"><span data-stu-id="83e91-184">Connecting the Unity project to the PUN application</span></span>

<span data-ttu-id="83e91-185">Dans cette section, vous allez connecter votre projet Unity à l’application PUN que vous avez créée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="83e91-185">In this section, you will connect your Unity project to the PUN application you created in the previous section.</span></span>

<span data-ttu-id="83e91-186">Dans le tableau de bord Photon, cliquez sur le champ **App ID** pour voir l’ID d’application, puis copiez-le dans le Presse-papiers :</span><span class="sxs-lookup"><span data-stu-id="83e91-186">On the Photon dashboard, click the **App ID** field to reveal the app ID, then copy it to your clipboard:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section7-step1-1.png)

<span data-ttu-id="83e91-188">Dans le menu Unity, sélectionnez **Window** > **Photon Unity Networking** > **PUN Wizard** pour ouvrir la fenêtre Pun Wizard, puis cliquez sur le bouton **Setup Project** pour ouvrir le menu PUN Setup et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="83e91-188">In the Unity menu, select **Window** > **Photon Unity Networking** > **PUN Wizard** to open the Pun Wizard window, click the **Setup Project** button to open the PUN Setup menu, and configure it as follows:</span></span>

* <span data-ttu-id="83e91-189">Dans le champ **AppId or Email**, collez l’ID d’application PUN que vous avez copié à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="83e91-189">In the **AppId or Email** field, paste the PUN app ID you copied in the previous step</span></span>

<span data-ttu-id="83e91-190">Cliquez ensuite sur le bouton **Setup Project** pour appliquer l’ID d’application :</span><span class="sxs-lookup"><span data-stu-id="83e91-190">Then click the **Setup Project** button to apply the app ID:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section7-step1-2.png)

<span data-ttu-id="83e91-192">Une fois le processus d’installation PUN terminé dans Unity, le menu PUN Setup affiche le message **Done!**</span><span class="sxs-lookup"><span data-stu-id="83e91-192">Once Unity has finished the PUN setup process, the PUN Setup menu will display the message **Done!**</span></span> <span data-ttu-id="83e91-193">et sélectionne automatiquement la ressource **PhotonServerSettings** dans la fenêtre Project. Les propriétés de cette ressource sont présentées dans la fenêtre Inspector :</span><span class="sxs-lookup"><span data-stu-id="83e91-193">and automatically select the **PhotonServerSettings** asset in the Project window so its properties are displayed in the Inspector window:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial1-section7-step1-3.png)

## <a name="congratulations"></a><span data-ttu-id="83e91-195">Félicitations</span><span class="sxs-lookup"><span data-stu-id="83e91-195">Congratulations</span></span>

<span data-ttu-id="83e91-196">Vous avez créé une application Photon PUN et l’avez connectée à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="83e91-196">You have successfully created a Photon PUN application and connected it to your Unity project.</span></span> <span data-ttu-id="83e91-197">Vous allez à présent autoriser les connexions avec d’autres utilisateurs pour qu’ils puissent se voir.</span><span class="sxs-lookup"><span data-stu-id="83e91-197">Your next step is to allow connections with other users so that multiple users can see each other.</span></span>

<span data-ttu-id="83e91-198">[Tutoriel suivant : 2. Connexion de plusieurs utilisateurs](mrlearning-sharing(photon)-ch2.md)</span><span class="sxs-lookup"><span data-stu-id="83e91-198">[Next tutorial: 2. Connecting multiple users](mrlearning-sharing(photon)-ch2.md)</span></span>
