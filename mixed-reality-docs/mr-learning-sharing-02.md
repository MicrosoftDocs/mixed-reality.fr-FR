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
# <a name="2-setting-up-photon-unity-networking"></a><span data-ttu-id="22211-105">2. Configuration de Photon Unity Networking</span><span class="sxs-lookup"><span data-stu-id="22211-105">2. Setting up Photon Unity Networking</span></span>

## <a name="overview"></a><span data-ttu-id="22211-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="22211-106">Overview</span></span>

<span data-ttu-id="22211-107">Dans ce tutoriel, vous allez préparer la création d’une expérience partagée à l’aide de Photon Unity Networking (PUN).</span><span class="sxs-lookup"><span data-stu-id="22211-107">In this tutorial, you will prepare for creating a shared experience using Photon Unity Networking (PUN).</span></span> <span data-ttu-id="22211-108">Vous allez découvrir comment créer une application PUN, importer des ressources PUN dans votre projet Unity et connecter votre projet Unity à l’application PUN.</span><span class="sxs-lookup"><span data-stu-id="22211-108">You will learn how to create a PUN app, import PUN assets into your Unity project, and connect your Unity project to the PUN app.</span></span>

## <a name="objectives"></a><span data-ttu-id="22211-109">Objectifs</span><span class="sxs-lookup"><span data-stu-id="22211-109">Objectives</span></span>

* <span data-ttu-id="22211-110">Apprendre à créer une application PUN</span><span class="sxs-lookup"><span data-stu-id="22211-110">Learn how to create a PUN app</span></span>
* <span data-ttu-id="22211-111">Apprendre à trouver et importer les ressources PUN</span><span class="sxs-lookup"><span data-stu-id="22211-111">Learn how to find and import the PUN assets</span></span>
* <span data-ttu-id="22211-112">Apprendre à connecter votre projet Unity à l’application PUN</span><span class="sxs-lookup"><span data-stu-id="22211-112">Learn how to connect your Unity project to the PUN app</span></span>

## <a name="creating-and-preparing-the-unity-project"></a><span data-ttu-id="22211-113">Création et préparation du projet Unity</span><span class="sxs-lookup"><span data-stu-id="22211-113">Creating and preparing the Unity project</span></span>

<span data-ttu-id="22211-114">Dans cette section, vous allez créer un projet Unity et le préparer au développement avec MRTK.</span><span class="sxs-lookup"><span data-stu-id="22211-114">In this section, you will create a new Unity project and get it ready for MRTK development.</span></span>

<span data-ttu-id="22211-115">Pour cela, suivez d’abord [Initialisation de votre projet et déploiement de votre première application](mr-learning-base-02.md), en excluant les instructions données dans [Générer votre application sur votre appareil](mr-learning-base-02.md#building-your-application-to-your-hololens-2), ce qui inclut les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="22211-115">For this, first follow the [Initializing your project and deploying your first application](mr-learning-base-02.md), excluding the [Build your application to your device](mr-learning-base-02.md#building-your-application-to-your-hololens-2) instructions, which includes the following steps:</span></span>

1. <span data-ttu-id="22211-116">[Création du projet Unity](mr-learning-base-02.md#creating-the-unity-project) et affectation d’un nom pertinent, par exemple *MRTK Tutorials*</span><span class="sxs-lookup"><span data-stu-id="22211-116">[Creating the Unity project](mr-learning-base-02.md#creating-the-unity-project) and give it a suitable name, for example, *MRTK Tutorials*</span></span>
1. [<span data-ttu-id="22211-117">Changement de plateforme de génération</span><span class="sxs-lookup"><span data-stu-id="22211-117">Switching the build platform</span></span>](mr-learning-base-02.md#configuring-the-unity-project)
1. [<span data-ttu-id="22211-118">Importation des ressources TextMeshPro Essential</span><span class="sxs-lookup"><span data-stu-id="22211-118">Importing the TextMeshPro Essential Resources</span></span>](mr-learning-base-02.md#importing-the-textmeshpro-essential-resources)
1. [<span data-ttu-id="22211-119">Importation du Mixed Reality Toolkit</span><span class="sxs-lookup"><span data-stu-id="22211-119">Importing the Mixed Reality Toolkit</span></span>](mr-learning-base-02.md#importing-the-mixed-reality-toolkit)
1. [<span data-ttu-id="22211-120">Configuration du projet Unity</span><span class="sxs-lookup"><span data-stu-id="22211-120">Configuring the Unity project</span></span>](mr-learning-base-02.md#configuring-the-unity-project)
1. <span data-ttu-id="22211-121">[Création et configuration de la scène](mr-learning-base-02.md#creating-and-configuring-the-scene), et affectation d’un nom pertinent à la scène, par exemple *MultiUserCapabilities*</span><span class="sxs-lookup"><span data-stu-id="22211-121">[Creating and configuring the scene](mr-learning-base-02.md#creating-and-configuring-the-scene) and give the scene a suitable name, for example, *MultiUserCapabilities*</span></span>

<span data-ttu-id="22211-122">Ensuite, suivez les instructions fournies dans [Modification de l’option d’affichage de la reconnaissance spatiale](mr-learning-base-03.md#changing-the-spatial-awareness-display-option) pour :</span><span class="sxs-lookup"><span data-stu-id="22211-122">Then follow the [Changing the Spatial Awareness Display Option](mr-learning-base-03.md#changing-the-spatial-awareness-display-option) instructions to:</span></span>

1. <span data-ttu-id="22211-123">Définir le **profil de configuration MRTK** sur **DefaultHoloLens2ConfigurationProfile**.</span><span class="sxs-lookup"><span data-stu-id="22211-123">Change the **MRTK configuration profile** for to the **DefaultHoloLens2ConfigurationProfile**</span></span>
1. <span data-ttu-id="22211-124">Définir les **options d’affichage du maillage spatiale** sur **Occlusion**.</span><span class="sxs-lookup"><span data-stu-id="22211-124">Change the **spatial awareness mesh display options** to **Occlusion**.</span></span>

## <a name="enabling-additional-capabilities"></a><span data-ttu-id="22211-125">Activation de fonctionnalités supplémentaires</span><span class="sxs-lookup"><span data-stu-id="22211-125">Enabling additional capabilities</span></span>

<span data-ttu-id="22211-126">Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings, puis recherchez la section **Player** >  **Publishing Settings** :</span><span class="sxs-lookup"><span data-stu-id="22211-126">In the Unity menu, select **Edit** > **Project Settings...** to open the Player Settings window, then locate the **Player** >  **Publishing Settings** section:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section2-step1-1.png)

<span data-ttu-id="22211-128">Dans la section **Publishing Settings**, accédez à la section **Capabilities** et vérifiez bien que les fonctionnalités **InternetClient**, **Microphone**, **SpatialPerception** et **GazeInput**, que vous avez activées à l’étape [Configuration du projet Unity](mr-learning-base-02.md#configuring-the-unity-project) ci-dessus, sont activées.</span><span class="sxs-lookup"><span data-stu-id="22211-128">In the  **Publishing Settings**, scroll down to the **Capabilities** section and double-check that the **InternetClient**, **Microphone**, **SpatialPerception**, and **GazeInput** capabilities, which you enabled during the [Configuring the Unity project](mr-learning-base-02.md#configuring-the-unity-project) step above, are enabled.</span></span>

<span data-ttu-id="22211-129">Activez ensuite les fonctionnalités supplémentaires suivantes :</span><span class="sxs-lookup"><span data-stu-id="22211-129">Then enable the following additional capabilities:</span></span>

* <span data-ttu-id="22211-130">Fonctionnalité **InternetClientServer**</span><span class="sxs-lookup"><span data-stu-id="22211-130">**InternetClientServer** capability</span></span>
* <span data-ttu-id="22211-131">Fonctionnalité **PrivateNetworkClientServer**</span><span class="sxs-lookup"><span data-stu-id="22211-131">**PrivateNetworkClientServer** capability</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section2-step1-2.png)

## <a name="installing-inbuilt-unity-packages"></a><span data-ttu-id="22211-133">Installation de packages Unity intégrés</span><span class="sxs-lookup"><span data-stu-id="22211-133">Installing inbuilt Unity packages</span></span>

<span data-ttu-id="22211-134">Dans le menu Unity, sélectionnez **Window** > **Package Manager** pour ouvrir la fenêtre Package Manager, sélectionnez **AR Foundation**, puis cliquez sur le bouton **Install** pour installer le package :</span><span class="sxs-lookup"><span data-stu-id="22211-134">In the Unity menu, select **Window** > **Package Manager** to open the Package Manager window, then select **AR Foundation** and click the **Install** button to install the package:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section3-step1-1.png)

> [!NOTE]
> <span data-ttu-id="22211-136">Vous installez le package intégré AR Foundation, car il est nécessaire pour le SDK Azure Spatial Anchors que vous allez importer dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="22211-136">You are installing the AR Foundation package because it is required by the Azure Spatial Anchors SDK you will import in the next section.</span></span>

## <a name="importing-the-tutorial-assets"></a><span data-ttu-id="22211-137">Importation des ressources du tutoriel</span><span class="sxs-lookup"><span data-stu-id="22211-137">Importing the tutorial assets</span></span>

<span data-ttu-id="22211-138">Téléchargez et **importez** les packages personnalisés Unity suivants **dans l’ordre où ils sont listés** :</span><span class="sxs-lookup"><span data-stu-id="22211-138">Download and **import** the following Unity custom packages **in the order they are listed**:</span></span>

* <span data-ttu-id="22211-139">[AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.2.1/AzureSpatialAnchors.unitypackage) (version 2.2.1)</span><span class="sxs-lookup"><span data-stu-id="22211-139">[AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.2.1/AzureSpatialAnchors.unitypackage) (version 2.2.1)</span></span>
* [<span data-ttu-id="22211-140">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.4.0.unitypackage</span><span class="sxs-lookup"><span data-stu-id="22211-140">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.4.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.4.0/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.4.0.unitypackage)
* [<span data-ttu-id="22211-141">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.4.0.unitypackage</span><span class="sxs-lookup"><span data-stu-id="22211-141">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.4.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.4.0/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.4.0.unitypackage)
* [<span data-ttu-id="22211-142">MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.4.0.unitypackage</span><span class="sxs-lookup"><span data-stu-id="22211-142">MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.4.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/multi-user-capabilities-v2.4.0/MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.4.0.unitypackage)

<span data-ttu-id="22211-143">Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="22211-143">After you have imported the tutorial assets your Project window should look similar to this:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section4-step1-1.png)

> [!TIP]
> <span data-ttu-id="22211-145">Pour vous rappeler comment importer un package personnalisé Unity, vous pouvez vous référer aux instructions fournies dans [Importation de Mixed Reality Toolkit](mr-learning-base-02.md#importing-the-mixed-reality-toolkit).</span><span class="sxs-lookup"><span data-stu-id="22211-145">For a reminder on how to import a Unity custom package, you can refer to the [Importing the Mixed Reality Toolkit](mr-learning-base-02.md#importing-the-mixed-reality-toolkit) instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="22211-146">Après l’importation du package de ressources du tutoriel MultiUserCapabilities, la fenêtre de console contient plusieurs erreurs [CS0246](https://docs.microsoft.com/dotnet/csharp/language-reference/compiler-messages/cs0246) qui indiquent que le type ou l’espace de noms est manquant.</span><span class="sxs-lookup"><span data-stu-id="22211-146">After importing the MultiUserCapabilities tutorial assets package, you will see several [CS0246](https://docs.microsoft.com/dotnet/csharp/language-reference/compiler-messages/cs0246) errors in the Console window stating that the type or namespace is missing.</span></span> <span data-ttu-id="22211-147">Ces erreurs sont attendues et seront résolues dans la section suivante quand vous importerez les ressources PUN.</span><span class="sxs-lookup"><span data-stu-id="22211-147">This is expected and will be resolved in the next section when you import the PUN assets.</span></span>

## <a name="importing-the-pun-assets"></a><span data-ttu-id="22211-148">Importation des ressources PUN</span><span class="sxs-lookup"><span data-stu-id="22211-148">Importing the PUN assets</span></span>

<span data-ttu-id="22211-149">Dans le menu Unity, sélectionnez **Window** > **Asset Store** pour ouvrir la fenêtre Asset Store, recherchez et sélectionnez **PUN 2 - FREE** dans Exit Games, puis cliquez sur le bouton **Download** pour télécharger le package de ressources dans votre compte Unity.</span><span class="sxs-lookup"><span data-stu-id="22211-149">In the Unity menu, select **Window** > **Asset Store** to open the Asset Store window, search for and select **PUN 2 - FREE** from Exit Games, click the **Download** button to download the asset package to your Unity account.</span></span>

<span data-ttu-id="22211-150">Une fois le téléchargement terminé, cliquez sur le bouton **Importer** pour ouvrir la fenêtre Import Unity Package :</span><span class="sxs-lookup"><span data-stu-id="22211-150">When the download is complete, click the **Import** button to open the Import Unity Package window:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section5-step1-1.png)

<span data-ttu-id="22211-152">Dans la fenêtre Import Unity Package (Importer un package Unity), cliquez sur le bouton **Tous** pour vous assurer que toutes les ressources sont sélectionnées, puis sur le bouton **Importer** pour importer les ressources :</span><span class="sxs-lookup"><span data-stu-id="22211-152">In the Import Unity Package window, click the **All** button to ensure all the assets are selected, then click the **Import** button to import the assets:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section5-step1-2.png)

<span data-ttu-id="22211-154">Une fois le processus d’importation terminé dans Unity, la fenêtre Pun Wizard apparaît avec le menu PUN Setup chargé. Vous pouvez ignorer ou fermer cette fenêtre pour l’instant :</span><span class="sxs-lookup"><span data-stu-id="22211-154">Once Unity has completed the import process, the Pun Wizard window will appear with the PUN Setup menu loaded, you can ignore or close this window for now:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section5-step1-3.png)

## <a name="creating-the-pun-application"></a><span data-ttu-id="22211-156">Création de l’application PUN</span><span class="sxs-lookup"><span data-stu-id="22211-156">Creating the PUN application</span></span>

<span data-ttu-id="22211-157">Dans cette section, vous allez créer un compte Photon (si vous n’en avez pas encore) et créer une application PUN.</span><span class="sxs-lookup"><span data-stu-id="22211-157">In this section, you will create a Photon account, if you don't already have one, and create a new PUN app.</span></span>

<span data-ttu-id="22211-158">Accédez au<a href="https://dashboard.photonengine.com/account/signin" target="_blank">tableau de bord</a> Photon et connectez-vous si vous disposez déjà d’un compte que vous souhaitez utiliser. Sinon, cliquez sur le lien **Create One** et suivez les instructions pour inscrire un nouveau compte :</span><span class="sxs-lookup"><span data-stu-id="22211-158">Navigate to the Photon <a href="https://dashboard.photonengine.com/account/signin" target="_blank">dashboard</a> and sign in if you already have an account you want to use, otherwise, click the **Create One** link and follow the instructions to register a new account:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section6-step1-1.png)

<span data-ttu-id="22211-160">Une fois connecté, cliquez sur le bouton **Create a New App** :</span><span class="sxs-lookup"><span data-stu-id="22211-160">Once signed in, click the **Create a New App** button:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section6-step1-2.png)

<span data-ttu-id="22211-162">Dans la page Create a New Application, entrez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="22211-162">On the Create a New Application page, enter the following values:</span></span>

* <span data-ttu-id="22211-163">Pour Photon Type, sélectionnez PUN.</span><span class="sxs-lookup"><span data-stu-id="22211-163">For Photon Type, select PUN</span></span>
* <span data-ttu-id="22211-164">Pour Nom, entrez un nom approprié, par exemple _MRTK Tutorials_.</span><span class="sxs-lookup"><span data-stu-id="22211-164">For Name, enter a suitable name, for example, _MRTK Tutorials_</span></span>
* <span data-ttu-id="22211-165">Pour Description, entrez éventuellement une description appropriée.</span><span class="sxs-lookup"><span data-stu-id="22211-165">For Description, optionally enter a suitable description</span></span>
* <span data-ttu-id="22211-166">Laissez le champ URL vide.</span><span class="sxs-lookup"><span data-stu-id="22211-166">For Url, leave the field empty</span></span>

<span data-ttu-id="22211-167">Cliquez ensuite sur le bouton **Create** pour créer l’application :</span><span class="sxs-lookup"><span data-stu-id="22211-167">Then click the **Create** button to create the new app:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section6-step1-3.png)

<span data-ttu-id="22211-169">Une fois le processus de création terminé dans Photon, la nouvelle application PUN apparaît dans votre tableau de bord :</span><span class="sxs-lookup"><span data-stu-id="22211-169">Once Photon has finished the creation process, the new PUN app will appear on your dashboard:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section6-step1-4.png)

## <a name="connecting-the-unity-project-to-the-pun-application"></a><span data-ttu-id="22211-171">Connexion du projet Unity à l’application PUN</span><span class="sxs-lookup"><span data-stu-id="22211-171">Connecting the Unity project to the PUN application</span></span>

<span data-ttu-id="22211-172">Dans cette section, vous allez connecter votre projet Unity à l’application PUN que vous avez créée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="22211-172">In this section, you will connect your Unity project to the PUN app you created in the previous section.</span></span>

<span data-ttu-id="22211-173">Dans le tableau de bord Photon, cliquez sur le champ **App ID** pour voir l’ID d’application, puis copiez-le dans le Presse-papiers :</span><span class="sxs-lookup"><span data-stu-id="22211-173">On the Photon dashboard, click the **App ID** field to reveal the app ID, then copy it to your clipboard:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section7-step1-1.png)

<span data-ttu-id="22211-175">Dans le menu Unity, sélectionnez **Window** > **Photon Unity Networking** > **PUN Wizard** pour ouvrir la fenêtre Pun Wizard, puis cliquez sur le bouton **Setup Project** pour ouvrir le menu PUN Setup et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="22211-175">In the Unity menu, select **Window** > **Photon Unity Networking** > **PUN Wizard** to open the Pun Wizard window, click the **Setup Project** button to open the PUN Setup menu, and configure it as follows:</span></span>

* <span data-ttu-id="22211-176">Dans le champ **AppId or Email**, collez l’ID d’application PUN que vous avez copié à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="22211-176">In the **AppId or Email** field, paste the PUN app ID you copied in the previous step</span></span>

<span data-ttu-id="22211-177">Cliquez ensuite sur le bouton **Setup Project** pour appliquer l’ID d’application :</span><span class="sxs-lookup"><span data-stu-id="22211-177">Then click the **Setup Project** button to apply the app ID:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section7-step1-2.png)

<span data-ttu-id="22211-179">Une fois le processus d’installation PUN terminé dans Unity, le menu PUN Setup affiche le message **Done!**</span><span class="sxs-lookup"><span data-stu-id="22211-179">Once Unity has finished the PUN setup process, the PUN Setup menu will display the message **Done!**</span></span> <span data-ttu-id="22211-180">et sélectionne automatiquement la ressource **PhotonServerSettings** dans la fenêtre Project. Les propriétés de cette ressource sont présentées dans la fenêtre Inspector :</span><span class="sxs-lookup"><span data-stu-id="22211-180">and automatically select the **PhotonServerSettings** asset in the Project window, so its properties are displayed in the Inspector window:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-02-section7-step1-3.png)

## <a name="congratulations"></a><span data-ttu-id="22211-182">Félicitations</span><span class="sxs-lookup"><span data-stu-id="22211-182">Congratulations</span></span>

<span data-ttu-id="22211-183">Vous avez créé une application PUN et l’avez connectée à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="22211-183">You have successfully created a PUN app and connected it to your Unity project.</span></span> <span data-ttu-id="22211-184">Vous allez à présent autoriser les connexions avec d’autres utilisateurs pour qu’ils puissent se voir.</span><span class="sxs-lookup"><span data-stu-id="22211-184">Your next step is to allow connections with other users so that multiple users can see each other.</span></span>

[<span data-ttu-id="22211-185">Tutoriel suivant : 3. Connexion de plusieurs utilisateurs</span><span class="sxs-lookup"><span data-stu-id="22211-185">Next Tutorial: 3. Connecting multiple users</span></span>](mr-learning-sharing-03.md)
