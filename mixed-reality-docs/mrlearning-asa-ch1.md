---
title: Didacticiels sur les ancres spatiales Azure-1. Prise en main des ancres spatiales Azure
description: Suivez ce cours pour découvrir comment implémenter Reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: e62d3626ec6f2dbf8b66378212afab7db2f56422
ms.sourcegitcommit: 23b130d03fea46a50a712b8301fe4e5deed6cf9c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2019
ms.locfileid: "75334458"
---
# <a name="1-getting-started-with-azure-spatial-anchors"></a><span data-ttu-id="a92f7-105">1. prise en main des ancres spatiales Azure</span><span class="sxs-lookup"><span data-stu-id="a92f7-105">1. Getting started with Azure Spatial Anchors</span></span>

## <a name="overview"></a><span data-ttu-id="a92f7-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a92f7-106">Overview</span></span>

<span data-ttu-id="a92f7-107">Bienvenue dans la deuxième série des didacticiels HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="a92f7-107">Welcome to the second series of the HoloLens 2 tutorials.</span></span> <span data-ttu-id="a92f7-108">Dans cette série de didacticiels en trois parties, vous allez apprendre les principes de base des ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="a92f7-108">In this three-part tutorial series, you will learn the fundamentals of Azure Spatial Anchors.</span></span>

<span data-ttu-id="a92f7-109">Dans ce premier didacticiel, bien démarrer [avec les ancres spatiales Azure](mrlearning-asa-ch1.md), vous allez explorer les différentes étapes requises pour démarrer et arrêter une session Azure et créer, charger et télécharger des ancres Azure sur un seul appareil.</span><span class="sxs-lookup"><span data-stu-id="a92f7-109">In this first tutorial, [Getting started with Azure Spatial Anchors](mrlearning-asa-ch1.md), you will explore the various steps required to start and stop an Azure session and create, upload, and download Azure anchors on a single device.</span></span>

<span data-ttu-id="a92f7-110">Dans le deuxième didacticiel, [l’enregistrement, la récupération et le partage d’ancres spatiales Azure](mrlearning-asa-ch2.md), vous apprendrez à enregistrer les ancres spatiales Azure dans plusieurs sessions d’application en enregistrant les informations d’ancrage dans le stockage de HoloLens 2 et en partageant ces informations d’ancre avec d’autres appareils pour un alignement d’ancrage sur plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="a92f7-110">In the second tutorial, [Saving, retrieving, and sharing Azure Spatial Anchors](mrlearning-asa-ch2.md), you will learn how to save Azure Spatial Anchors across multiple app sessions by saving anchor information to the HoloLens 2's storage and how to share this anchor information to other devices for a multi-device anchor alignment.</span></span>

<span data-ttu-id="a92f7-111">Dans le troisième didacticiel, l’affichage de commentaires sur l' [ancrage spatial Azure](mrlearning-asa-ch3.md)vous apprendra à fournir aux utilisateurs des commentaires sur les événements d’ancrage et les États lors de l’utilisation d’ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="a92f7-111">In the third tutorial, [Displaying Azure Spatial Anchor feedback](mrlearning-asa-ch3.md), you will learn how to provide users with feedback about anchor events and statuses when using Azure Spatial Anchors.</span></span>

## <a name="objectives"></a><span data-ttu-id="a92f7-112">Objectifs</span><span class="sxs-lookup"><span data-stu-id="a92f7-112">Objectives</span></span>

* <span data-ttu-id="a92f7-113">Découvrez les principes de base du développement avec les ancres spatiales Azure pour HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="a92f7-113">Learn the fundamentals of developing with Azure Spatial Anchors for HoloLens 2</span></span>
* <span data-ttu-id="a92f7-114">Créer, charger et télécharger des ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="a92f7-114">Create, upload, and download spatial anchors</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a92f7-115">Prérequis</span><span class="sxs-lookup"><span data-stu-id="a92f7-115">Prerequisites</span></span>

>[!TIP]
><span data-ttu-id="a92f7-116">Si vous n’avez pas encore terminé la série des [didacticiels de mise](mrlearning-base.md) en route, nous vous recommandons d’effectuer d’abord ces didacticiels.</span><span class="sxs-lookup"><span data-stu-id="a92f7-116">If you have not completed the [Getting started tutorials](mrlearning-base.md) series yet, it's recommended that you complete those tutorials first.</span></span>

* <span data-ttu-id="a92f7-117">Un PC Windows 10 configuré avec les outils corrects [installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="a92f7-117">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="a92f7-118">Windows 10 SDK 10.0.18362.0 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="a92f7-118">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="a92f7-119">Certaines fonctionnalités C# de programmation de base</span><span class="sxs-lookup"><span data-stu-id="a92f7-119">Some basic C# programming ability</span></span>
* <span data-ttu-id="a92f7-120">Un appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)</span><span class="sxs-lookup"><span data-stu-id="a92f7-120">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>
* <span data-ttu-id="a92f7-121">Complétez la section [créer une ressource d’ancrages spatiaux](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) du Guide de [démarrage rapide : créer une application de l’unité HoloLens qui utilise des ancres spatiales Azure](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) .</span><span class="sxs-lookup"><span data-stu-id="a92f7-121">Complete the [Create a Spatial Anchors resource](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) section of the [Quickstart: Create a Unity HoloLens app that uses Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) tutorial.</span></span>

>[!IMPORTANT]
><span data-ttu-id="a92f7-122">Cette série de didacticiels requiert <a href="https://unity3d.com/get-unity/download/archive" target="_blank">unity 2019,1</a> et la version recommandée est Unity 2019.1.14.</span><span class="sxs-lookup"><span data-stu-id="a92f7-122">This tutorial series requires <a href="https://unity3d.com/get-unity/download/archive" target="_blank">Unity 2019.1</a> and the recommended version is Unity 2019.1.14.</span></span> <span data-ttu-id="a92f7-123">Cela remplace toute exigence ou recommandation de version Unity énoncées dans les conditions préalables liées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a92f7-123">This supersedes any Unity version requirements or recommendations stated in the prerequisites linked above.</span></span>

## <a name="creating-the-unity-project"></a><span data-ttu-id="a92f7-124">Création du projet Unity</span><span class="sxs-lookup"><span data-stu-id="a92f7-124">Creating the Unity project</span></span>

<span data-ttu-id="a92f7-125">Dans cette section, vous allez créer un nouveau projet Unity et le configurer pour Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="a92f7-125">In this section, you will create a new Unity project and configure it for Windows Mixed Reality.</span></span>

1. <span data-ttu-id="a92f7-126">Créez un projet Unity et donnez-lui un nom approprié, par exemple le didacticiel sur les _ancres spatiales Azure_.</span><span class="sxs-lookup"><span data-stu-id="a92f7-126">Create a Unity project and give it a suitable name, for example, _Azure Spatial Anchors tutorial_.</span></span>

2. <span data-ttu-id="a92f7-127">Configurez le projet Unity pour Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="a92f7-127">Configure the Unity project for Windows Mixed Reality.</span></span>

    >[!TIP]
    ><span data-ttu-id="a92f7-128">Pour obtenir un rappel sur la façon de créer un projet Unity et de le configurer pour Windows Mixed Reality, vous pouvez consulter les sections créer un projet [Unity](mrlearning-base-ch1.md#create-new-unity-project) et [configurer le projet Unity pour Windows Mixed Reality](mrlearning-base-ch1.md#configure-the-unity-project-for-windows-mixed-reality) dans le didacticiel [initialiser votre projet et votre première application](https://docs.microsoft.com/windows/mixed-reality/mrlearning-base-ch1) , qui fait partie de la série de [didacticiels de mise](mrlearning-base.md) en route.</span><span class="sxs-lookup"><span data-stu-id="a92f7-128">For a reminder on how to create a Unity project and configure it for Windows Mixed Reality, you can refer to the [Create new Unity project](mrlearning-base-ch1.md#create-new-unity-project) and the [Configure the Unity project for Windows Mixed Reality](mrlearning-base-ch1.md#configure-the-unity-project-for-windows-mixed-reality) sections of the [Initializing your project and first application](https://docs.microsoft.com/windows/mixed-reality/mrlearning-base-ch1) tutorial which is part of the the [Getting started tutorials](mrlearning-base.md) series.</span></span>

## <a name="adding-inbuilt-unity-packages"></a><span data-ttu-id="a92f7-129">Ajout de packages Unity incorporés</span><span class="sxs-lookup"><span data-stu-id="a92f7-129">Adding inbuilt Unity packages</span></span>

<span data-ttu-id="a92f7-130">Dans cette section, vous allez ajouter des ressources Unity et des packages requis par les kits de ressources et les kits de développement logiciel (SDK) que vous utiliserez dans le projet.</span><span class="sxs-lookup"><span data-stu-id="a92f7-130">In this section, you will add inbuilt Unity assets and packages required by the toolkits and SDKs you will be using in the project.</span></span>

1. <span data-ttu-id="a92f7-131">Importez des ressources TMP essentielles.</span><span class="sxs-lookup"><span data-stu-id="a92f7-131">Import TMP Essential Resources.</span></span>

    >[!NOTE]
    ><span data-ttu-id="a92f7-132">Nous ajoutons ce package, car il est requis par le kit de la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="a92f7-132">We are adding this package because it is required by the Mixed Reality Toolkit.</span></span>

    <span data-ttu-id="a92f7-133">Dans le menu Unity, sélectionnez **windows** > **TextMeshPro** > **importer des ressources tmp Essential**.</span><span class="sxs-lookup"><span data-stu-id="a92f7-133">In the Unity menu, select **Window** > **TextMeshPro** > **Import TMP Essential Resources**.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-2-1.1.png)

    <span data-ttu-id="a92f7-135">Dans la fenêtre contextuelle importer un package d’Unity, commencez par vérifier que toutes les ressources sont sélectionnées en cliquant sur le bouton **tout** , puis importez les éléments multimédias en cliquant sur le bouton **Importer** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-135">In the Import Unity Package pop-up window, first make sure all the assets are selected by clicking the **All** button, then import the assets by clicking the **Import** button.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-2-1.2.png)

2. <span data-ttu-id="a92f7-137">Installez AR Foundation.</span><span class="sxs-lookup"><span data-stu-id="a92f7-137">Install AR Foundation.</span></span>

    >[!NOTE]
    ><span data-ttu-id="a92f7-138">Nous ajoutons ce package, car il est requis par le kit de développement logiciel (SDK) d’ancre spatiale Azure.</span><span class="sxs-lookup"><span data-stu-id="a92f7-138">We are adding this package because it is required by the Azure Spatial Anchors SDK.</span></span>

    <span data-ttu-id="a92f7-139">Dans le menu Unity, sélectionnez **fenêtre** > **Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="a92f7-139">In the Unity menu, select **Window** > **Package Manager**.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-2-2.1.png)

    <span data-ttu-id="a92f7-141">Dans la fenêtre du gestionnaire de package, sélectionnez **AR Foundation** et installez le package en cliquant sur le bouton **installer** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-141">In the Package Manager window, select **AR Foundation** and install the package by clicking the **Install** button.</span></span>

    >[!IMPORTANT]
    ><span data-ttu-id="a92f7-142">Il peut s’avérer nécessaire de prendre quelques secondes avant que le package de fondation de base ne s’affiche dans la liste.</span><span class="sxs-lookup"><span data-stu-id="a92f7-142">It might take a few seconds before the AR Foundation package appears in the list.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-2-2.2.png)

## <a name="importing-the-tutorial-assets"></a><span data-ttu-id="a92f7-144">Importation des ressources du didacticiel</span><span class="sxs-lookup"><span data-stu-id="a92f7-144">Importing the tutorial assets</span></span>

<span data-ttu-id="a92f7-145">Dans cette section, vous allez télécharger et importer toutes les ressources du didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a92f7-145">In this section, you will download and import all the tutorial assets.</span></span>

1. <span data-ttu-id="a92f7-146">Téléchargez les ressources.</span><span class="sxs-lookup"><span data-stu-id="a92f7-146">Download the assets.</span></span>

    * <span data-ttu-id="a92f7-147">[AzureSpatialAnchors. pour Unity](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.0.0/AzureSpatialAnchors.unitypackage) (version 2.0.0)</span><span class="sxs-lookup"><span data-stu-id="a92f7-147">[AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.0.0/AzureSpatialAnchors.unitypackage) (version 2.0.0)</span></span>
    * [<span data-ttu-id="a92f7-148">Microsoft. MixedReality. Toolkit. Unity. Foundation. 2.1.0. pour Unity</span><span class="sxs-lookup"><span data-stu-id="a92f7-148">Microsoft.MixedReality.Toolkit.Unity.Foundation.2.1.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.1.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.1.0.unitypackage)
    * [<span data-ttu-id="a92f7-149">MRTK. HoloLens2. Unity. Tutorials. Assets. GettingStarted. 2.1.0.1. pour Unity</span><span class="sxs-lookup"><span data-stu-id="a92f7-149">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.1.0.1.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.1.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.1.0.1.unitypackage)
    * [<span data-ttu-id="a92f7-150">MRTK. HoloLens2. Unity. Tutorials. Assets. AzureSpatialAnchors. 2.1.0.1. pour Unity</span><span class="sxs-lookup"><span data-stu-id="a92f7-150">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.1.0.1.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.1.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.1.0.1.unitypackage)

2. <span data-ttu-id="a92f7-151">Importez les ressources.</span><span class="sxs-lookup"><span data-stu-id="a92f7-151">Import the assets.</span></span>

    <span data-ttu-id="a92f7-152">Dans le menu Unity, sélectionnez **actifs** > **importer un package** > **package personnalisé...** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-152">In the Unity menu, select **Assets** > **Import Package** > **Custom Package...**.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-3-2.1.png)

    <span data-ttu-id="a92f7-154">Dans le package d’importation... dans la fenêtre indépendante, sélectionnez **AzureSpatialAnchors. pour Unity** , puis cliquez sur le bouton **ouvrir** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-154">In the Import package... pop-up window, select the **AzureSpatialAnchors.unitypackage** and click the **Open** button.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-3-2.2.png)

    <span data-ttu-id="a92f7-156">Dans la fenêtre contextuelle importer un package d’Unity, commencez par vérifier que toutes les ressources sont sélectionnées en cliquant sur le bouton **tout** , puis importez les éléments multimédias en cliquant sur le bouton **Importer** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-156">In the Import Unity Package pop-up window, first make sure all the assets are selected by clicking the **All** button, then import the assets by clicking the **Import** button.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-3-2.3.png)

    <span data-ttu-id="a92f7-158">Répétez ces étapes pour importer les packages de ressources restants.</span><span class="sxs-lookup"><span data-stu-id="a92f7-158">Repeat these steps to import the remaining asset packages.</span></span> <span data-ttu-id="a92f7-159">Une fois l’opération terminée, le dossier des **ressources** de votre projet Unity doit contenir ces sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="a92f7-159">Once complete, your Unity project's **Assets** folder should contain these sub-folders.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-3-2.4.png)

## <a name="creating-and-preparing-the-scene"></a><span data-ttu-id="a92f7-161">Création et préparation de la scène</span><span class="sxs-lookup"><span data-stu-id="a92f7-161">Creating and preparing the scene</span></span>

<span data-ttu-id="a92f7-162">Dans cette section, vous allez créer et préparer la scène en ajoutant la boîte à outils de la réalité mixte et une partie du didacticiel prefabs.</span><span class="sxs-lookup"><span data-stu-id="a92f7-162">In this section, you will create and prepare the scene by adding the Mixed Reality Toolkit and some of the tutorial prefabs.</span></span>

1. <span data-ttu-id="a92f7-163">Créez une nouvelle scène.</span><span class="sxs-lookup"><span data-stu-id="a92f7-163">Create a new scene.</span></span>

    <span data-ttu-id="a92f7-164">Dans le menu Unity, sélectionnez **fichier** > **nouvelle scène**.</span><span class="sxs-lookup"><span data-stu-id="a92f7-164">In the Unity menu, select **File** > **New Scene**.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-1.1.png)

    <span data-ttu-id="a92f7-166">Dans le menu Unity, sélectionnez **fichier** > **Enregistrer sous...** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-166">In the Unity menu, select **File** > **Save As...**.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-1.2.png)

    <span data-ttu-id="a92f7-168">Dans la fenêtre contextuelle enregistrer la scène, accédez au dossier **scenes** de votre projet, donnez à votre scène un nom approprié, par exemple, _ASATutorialScene_, puis enregistrez la scène en cliquant sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-168">In the Save Scene pop-up window, navigate to your project's **Scenes** folder, give your scene a suitable name, for example, _ASATutorialScene_, and save the scene by clicking the **Save** button.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-1.3.png)

    >[!TIP]
    ><span data-ttu-id="a92f7-170">Vous pouvez enregistrer la scène à l’emplacement de votre choix, à condition qu’elle se trouve dans le dossier ressources du projet.</span><span class="sxs-lookup"><span data-stu-id="a92f7-170">You can save the scene anywhere you like as long as it is inside the project's Assets folder.</span></span> <span data-ttu-id="a92f7-171">Toutefois, pour que votre projet reste organisé, il est généralement recommandé de l’enregistrer dans le dossier scenes du projet.</span><span class="sxs-lookup"><span data-stu-id="a92f7-171">However, to keep your project organized, it's generally recommended to save it in the project's Scenes folder.</span></span>

2. <span data-ttu-id="a92f7-172">Ajoutez la boîte à outils de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="a92f7-172">Add the Mixed Reality Toolkit.</span></span>

    <span data-ttu-id="a92f7-173">Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Ajouter à la scène et configurer..** ..</span><span class="sxs-lookup"><span data-stu-id="a92f7-173">In the Unity menu, select **Mixed Reality Toolkit** > **Add to Scene and Configure...**.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-2.1.png)

    <span data-ttu-id="a92f7-175">Dans la fenêtre contextuelle sélectionner MixedRealityToolkitConfigurationProfile, cliquez sur **DefaultHoloLens2ConfigurationProfile** pour le définir comme profil de configuration MRTK de la scène.</span><span class="sxs-lookup"><span data-stu-id="a92f7-175">In the Select MixedRealityToolkitConfigurationProfile pop-up window, click the **DefaultHoloLens2ConfigurationProfile** to set it as the scene's MRTK configuration profile.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-2.2.png)

    <span data-ttu-id="a92f7-177">Dans le menu Unity, sélectionnez **File** > **Save** pour enregistrer la scène.</span><span class="sxs-lookup"><span data-stu-id="a92f7-177">In the Unity menu, select **File** > **Save** to save the scene.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-2.3.png)

    >[!TIP]
    ><span data-ttu-id="a92f7-179">Vous pouvez utiliser le raccourci clavier CTRL + S (commande + S sur macOS) pour enregistrer rapidement votre scène au cours de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a92f7-179">You can use the keyboard shortcut CTRL+S (command + S on macOS) to quickly save your scene as you are working through this tutorial.</span></span>

3. <span data-ttu-id="a92f7-180">Ajoutez le didacticiel prefabs.</span><span class="sxs-lookup"><span data-stu-id="a92f7-180">Add the tutorial prefabs.</span></span>

    <span data-ttu-id="a92f7-181">Dans le panneau projet, accédez à **ressources** > **MRTK. Tutoriels. AzureSpatialAnchors** > dossier **Prefabs** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-181">In the Project panel, navigate to **Assets** > **MRTK.Tutorials.AzureSpatialAnchors** > **Prefabs** folder.</span></span> <span data-ttu-id="a92f7-182">Tout en maintenant enfoncé le bouton CTRL (commande sur macOS), cliquez sur **ButtonParent**, **DebugWindow**et **ParentAnchor** pour sélectionner les trois prefabs.</span><span class="sxs-lookup"><span data-stu-id="a92f7-182">While holding down the CTRL button (command on macOS), click on **ButtonParent**, **DebugWindow**, and **ParentAnchor** to select the three prefabs.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-3.1.png)

    <span data-ttu-id="a92f7-184">Les trois prefabs étant toujours sélectionnés, faites-les glisser dans le panneau de la hiérarchie pour les ajouter à la scène.</span><span class="sxs-lookup"><span data-stu-id="a92f7-184">With the three prefabs still selected, drag them into the Hierarchy panel to add them to the scene.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-3.2.png)

    <span data-ttu-id="a92f7-186">Pour vous concentrer sur les objets de la scène, vous pouvez double-cliquer sur l’objet ParentAnchor, puis effectuer un zoom légèrement arrière.</span><span class="sxs-lookup"><span data-stu-id="a92f7-186">To focus in on the objects in the scene, you can double-click on the ParentAnchor object, and then zoom slightly out again.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-3.3.png)

    >[!TIP]
    ><span data-ttu-id="a92f7-188">Si vous trouvez les grandes icônes de votre scène, par exemple les icônes « t » de grande taille, vous pouvez les masquer en <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">basculant la gizmos</a> sur la position OFF.</span><span class="sxs-lookup"><span data-stu-id="a92f7-188">If you find the large icons in your scene, for example, the large framed 'T' icons distracting, you can hide these by <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">toggling the Gizmos</a> to the off position.</span></span>

## <a name="configuring-the-buttons-to-operate-the-scene"></a><span data-ttu-id="a92f7-189">Configuration des boutons pour faire fonctionner la scène</span><span class="sxs-lookup"><span data-stu-id="a92f7-189">Configuring the buttons to operate the scene</span></span>

<span data-ttu-id="a92f7-190">Dans cette section, vous allez ajouter des prefabs et des scripts dans la scène pour créer une série de boutons qui illustrent les principes de base de la façon dont les ancres locales et les ancres spatiales Azure se comportent dans une application.</span><span class="sxs-lookup"><span data-stu-id="a92f7-190">In this section, you will add prefabs and scripts into the scene to create a series of buttons that demonstrate the fundamentals of how both local anchors and Azure Spatial Anchors behave in an application.</span></span>

1. <span data-ttu-id="a92f7-191">Configurez le composant Holo lentille 2 (script) du bouton enfoncé.</span><span class="sxs-lookup"><span data-stu-id="a92f7-191">Configure the Pressable Button Holo Lens 2 (script) component.</span></span>

    <span data-ttu-id="a92f7-192">Dans le volet hiérarchie, développez l’objet **ButtonParent** et sélectionnez le premier objet enfant nommé **StartAzureSession**.</span><span class="sxs-lookup"><span data-stu-id="a92f7-192">In the Hierarchy panel, expand the **ButtonParent** object and select the first child object named **StartAzureSession**.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-5-1.1.png)

    <span data-ttu-id="a92f7-194">Dans le volet de l’inspecteur, faites défiler l’écran jusqu’au **bouton enfoncé Holo objectif 2 (script)** et ajoutez un nouvel écouteur d’événements à l’événement **bouton enfoncé ()** en cliquant sur l’icône **+** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-194">In the Inspector panel, scroll down to the **Pressable Button Holo Lens 2 (script)** component and add a new event listener to the **Button Pressed ()** event by clicking the **+** icon.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-5-1.2.png)

    <span data-ttu-id="a92f7-196">Lorsque l’objet StartAzureSession est toujours sélectionné dans le panneau hiérarchie, cliquez et faites glisser l’objet **ParentAnchor** à partir du volet hiérarchie vers le champ **aucun (objet)** vide de l’écouteur d’événements que vous venez d’ajouter pour que l’objet ParentAnchor écoute les événements appuyés sur le bouton à partir de ce bouton.</span><span class="sxs-lookup"><span data-stu-id="a92f7-196">With the StartAzureSession object still selected in the Hierarchy panel, click-and-drag the **ParentAnchor** object from the Hierarchy panel into the empty **None (Object)** field of the event listener you just added to make the ParentAnchor object listen for button pressed events from this button.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-5-1.3.png)

    <span data-ttu-id="a92f7-198">Cliquez sur la liste déroulante **no Function** du même écouteur d’événements, puis sélectionnez **AnchorModuleScript** > **StartAzureSession ()** pour définir la fonction StartAzureSession () comme l’action qui est déclenchée lorsque les événements activés du bouton sont déclenchés à partir de ce bouton.</span><span class="sxs-lookup"><span data-stu-id="a92f7-198">Click the **No Function** dropdown of the same event listener, then select **AnchorModuleScript** > **StartAzureSession ()** to set the StartAzureSession () function as the action that is triggered when the button pressed events is fired from this button.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-5-1.4.png)

2. <span data-ttu-id="a92f7-200">Configurez le composant (script) pouvant être interagi.</span><span class="sxs-lookup"><span data-stu-id="a92f7-200">Configure the Interactable (script) component.</span></span>

    <span data-ttu-id="a92f7-201">Avec l’objet StartAzureSession toujours sélectionné dans le panneau hiérarchie, dans le panneau Inspecteur, faites défiler l’écran jusqu’au composant **(script) pouvant être interagi** et répétez le même processus qu’à l’étape 1 ci-dessus pour l’événement **OnClick ()** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-201">With the StartAzureSession object still selected in the Hierarchy panel, in the Inspector panel, scroll down to the **Interactable (Script)** component and repeat the same process as in step 1 above for the **OnClick ()** event.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-5-2.1.png)

3. <span data-ttu-id="a92f7-203">Configurer les autres boutons</span><span class="sxs-lookup"><span data-stu-id="a92f7-203">Configure the remaining buttons</span></span>

    <span data-ttu-id="a92f7-204">Pour chacun des autres boutons, terminez le processus décrit aux étapes 1 et 2 ci-dessus pour affecter des fonctions aux événements bouton appuyé () et OnClick () suivants :</span><span class="sxs-lookup"><span data-stu-id="a92f7-204">For each of the remaining buttons, complete the process outlined in step 1 and 2 above to assign functions to both the Button Pressed () and OnClick () events following:</span></span>

    * <span data-ttu-id="a92f7-205">Pour l’objet **StopAzureSession** , assignez la fonction **StopAzureSession ()** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-205">For the **StopAzureSession** object, assign the **StopAzureSession()** function.</span></span>
    * <span data-ttu-id="a92f7-206">Pour l’objet **CreateAnchor** , assignez la fonction **CreateAzureAnchor ()** , puis faites glisser à nouveau le **ParentAnchor** dans le champ vide **aucun (objet de jeu)** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-206">For the **CreateAnchor** object, assign the **CreateAzureAnchor()** function, then drag the **ParentAnchor** again into the empty **None (Game Object)** field.</span></span>
    * <span data-ttu-id="a92f7-207">Pour le **début de la recherche de l’objet d’ancrage** , assignez la fonction **FindAzureAnchor ()** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-207">For the **Start Looking for Anchor** object, assign the **FindAzureAnchor()** function.</span></span>
    * <span data-ttu-id="a92f7-208">Pour l’objet de **Suppression d’Azure Anchor** , assignez la fonction **DeleteAzureAnchor ()** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-208">For the **Delete Azure Anchor** object, assign the **DeleteAzureAnchor()** function.</span></span>
    * <span data-ttu-id="a92f7-209">Pour l' **objet supprimer l’ancre locale** , assignez la fonction **RemoveLocalAnchor ()** , puis faites glisser à nouveau le **ParentAnchor** dans le champ vide **aucun (objet de jeu)** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-209">For the **Delete Local Anchor** object, assign the **RemoveLocalAnchor()** function, then drag the **ParentAnchor** again into the empty **None (Game Object)** field.</span></span>

4. <span data-ttu-id="a92f7-210">Connecter la scène à la ressource Azure</span><span class="sxs-lookup"><span data-stu-id="a92f7-210">Connect the scene to the Azure resource</span></span>

    <span data-ttu-id="a92f7-211">Dans le panneau hiérarchie, sélectionnez l’objet **ParentAnchor** et, dans le panneau Inspecteur, faites défiler jusqu’au composant **Gestionnaire d’ancrage spatial (script)** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-211">In the Hierarchy panel, select the **ParentAnchor** object and in the Inspector panel, scroll down to the **Spatial Anchor Manager (Script)** component.</span></span>

    <span data-ttu-id="a92f7-212">Ensuite, dans la section **informations d’identification** , collez votre ID de compte et votre clé d’ancrage spatial dans les champs **ID de compte d’ancrage** spatial et **ancres spatiales** correspondants.</span><span class="sxs-lookup"><span data-stu-id="a92f7-212">Then, in the **Credentials** section, paste your Spatial Anchors Account ID and Key into the corresponding **Spatial Anchors Account Id** and **Spatial Anchors Account Key** fields.</span></span>

    >[!NOTE]
    ><span data-ttu-id="a92f7-213">Vous avez créé votre ID de compte et votre clé d’ancrage spatial dans le cadre des [conditions préalables](mrlearning-asa-ch1.md#prerequisites)de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a92f7-213">You created your Spatial Anchors Account Id and Key as part of this tutorial's [Prerequisites](mrlearning-asa-ch1.md#prerequisites).</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-5-4.1.png)

    >[!CAUTION]
    ><span data-ttu-id="a92f7-215">Veillez à enregistrer votre scène.</span><span class="sxs-lookup"><span data-stu-id="a92f7-215">Make sure you save your scene.</span></span>

## <a name="trying-the-basic-behaviors-of-azure-spatial-anchors"></a><span data-ttu-id="a92f7-216">Essai des comportements de base des ancres spatiales Azure</span><span class="sxs-lookup"><span data-stu-id="a92f7-216">Trying the basic behaviors of Azure Spatial Anchors</span></span>

<span data-ttu-id="a92f7-217">Maintenant que votre scène est configurée pour illustrer les principes de base des ancres spatiales Azure, il est temps de déployer l’application afin de pouvoir expérimenter les ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="a92f7-217">Now that your scene is configured to demonstrate the basics of Azure Spatial Anchors, it is time to deploy the app so you can experience Azure Spatial Anchors firsthand.</span></span>

1. <span data-ttu-id="a92f7-218">Ajoutez des fonctionnalités supplémentaires requises.</span><span class="sxs-lookup"><span data-stu-id="a92f7-218">Add additional required capabilities.</span></span>

    <span data-ttu-id="a92f7-219">Dans le menu Unity, sélectionnez **modifier** > **paramètres du projet...** pour ouvrir le panneau Paramètres du lecteur.</span><span class="sxs-lookup"><span data-stu-id="a92f7-219">In the Unity menu, select **Edit** > **Project Settings...** to open the Player Settings panel.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-6-1.1.png)

    <span data-ttu-id="a92f7-221">Dans le panneau Paramètres du lecteur, sélectionnez **lecteur** , puis **paramètres de publication**.</span><span class="sxs-lookup"><span data-stu-id="a92f7-221">In the Player Settings panel, select **Player** and then **Publishing Settings**.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-6-1.2.png)

    <span data-ttu-id="a92f7-223">Dans les **paramètres de publication**, faites défiler jusqu’à la section **fonctionnalités** et vérifiez que **SpatialPerception**, que vous avez activé lors de la création du projet au début du didacticiel, est activé.</span><span class="sxs-lookup"><span data-stu-id="a92f7-223">In the  **Publishing Settings**, scroll down to the **Capabilities** section and double-check that **SpatialPerception**, which you enabled when you created the project at the beginning of the tutorial, is enabled.</span></span> <span data-ttu-id="a92f7-224">Ensuite, activez les fonctionnalités **internetclient**, **InternetClientServer**, **PrivateNetworkClientServer**, **RemovableStorage**, **webcam**et **microphone** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-224">Then, enabled the **InternetClient**, **InternetClientServer**, **PrivateNetworkClientServer**, **RemovableStorage**, **Webcam**, and **Microphone** capabilities.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-6-1.3.png)

2. <span data-ttu-id="a92f7-226">Déployez l’application sur votre HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="a92f7-226">Deploy the app to your HoloLens 2.</span></span>

    >[!TIP]
    ><span data-ttu-id="a92f7-227">Pour obtenir un rappel sur la création et le déploiement de votre projet Unity dans HoloLens 2, vous pouvez consulter les sections [créer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device) dans le didacticiel [initialiser votre projet et votre première application](https://docs.microsoft.com/windows/mixed-reality/mrlearning-base-ch1) , qui fait partie de la série de [didacticiels de mise](mrlearning-base.md) en route.</span><span class="sxs-lookup"><span data-stu-id="a92f7-227">For a reminder on how to build and deploy your Unity project to HoloLens 2, you can refer to the [Build your application to your device](mrlearning-base-ch1.md#build-your-application-to-your-device) sections of the [Initializing your project and first application](https://docs.microsoft.com/windows/mixed-reality/mrlearning-base-ch1) tutorial which is part of the the [Getting started tutorials](mrlearning-base.md) series.</span></span>

3. <span data-ttu-id="a92f7-228">Exécutez l’application et suivez les instructions de l’application.</span><span class="sxs-lookup"><span data-stu-id="a92f7-228">Run the app and follow the in-app instructions.</span></span>

    >[!CAUTION]
    ><span data-ttu-id="a92f7-229">Les ancres spatiales Azure utilisent Internet pour enregistrer et charger les données d’ancrage. Assurez-vous que votre appareil est connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="a92f7-229">Azure Spatial Anchors uses the internet to save and load the anchor data so make sure your device is connected to the internet.</span></span>

    <span data-ttu-id="a92f7-230">Lorsque l’application s’exécute sur votre appareil, suivez les instructions à l’écran affichées dans le panneau **instructions du module d’ancrage spatial Azure** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-230">When the application is running on your device, follow the on-screen instructions displayed on the **Azure Spatial Anchor Module Instructions** panel.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-6-3.1.png)

## <a name="anchoring-an-experience"></a><span data-ttu-id="a92f7-232">Ancrage d’une expérience</span><span class="sxs-lookup"><span data-stu-id="a92f7-232">Anchoring an experience</span></span>

<span data-ttu-id="a92f7-233">Dans les sections précédentes, vous avez appris les principes de base des ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="a92f7-233">In the previous sections, you learned the fundamentals of Azure Spatial Anchors.</span></span> <span data-ttu-id="a92f7-234">Nous avons utilisé un cube pour représenter et visualiser l’objet de jeu parent avec l’ancre attachée.</span><span class="sxs-lookup"><span data-stu-id="a92f7-234">We used a cube to represent and visualize the parent game object with the attached anchor.</span></span> <span data-ttu-id="a92f7-235">Dans cette section, vous allez apprendre à ancrer une expérience complète en la plaçant en tant qu’enfant de l’objet ParentAnchor.</span><span class="sxs-lookup"><span data-stu-id="a92f7-235">In this section, you will learn how to anchor an entire experience by placing it as a child of the ParentAnchor object.</span></span>

1. <span data-ttu-id="a92f7-236">Ajoutez l’expérience du lanceur Rocket.</span><span class="sxs-lookup"><span data-stu-id="a92f7-236">Add the Rocket Launcher experience.</span></span>

    <span data-ttu-id="a92f7-237">Dans le panneau projet, accédez à **ressources** > **MRTK. Tutoriels. GettingStarted** > dossier **Prefabs** et sélectionnez le Prefab **Rocket Launcher_Complete** .</span><span class="sxs-lookup"><span data-stu-id="a92f7-237">In the Project panel, navigate to **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** folder and select the **Rocket Launcher_Complete** prefab.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-7-1.1.png)

    <span data-ttu-id="a92f7-239">Avec la Prefab Rocket Launcher_Complete toujours sélectionnée, faites-la glisser sur l’objet **ParentAnchor** dans le panneau de la hiérarchie pour en faire un enfant de l’objet ParentAnchor.</span><span class="sxs-lookup"><span data-stu-id="a92f7-239">With the Rocket Launcher_Complete prefab still selected, drag it on top of the **ParentAnchor** object in the Hierarchy panel to make it a child of the ParentAnchor object.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-7-1.2.png)

2. <span data-ttu-id="a92f7-241">Repositionnez l’expérience du lanceur Rocket.</span><span class="sxs-lookup"><span data-stu-id="a92f7-241">Reposition the Rocket Launcher experience.</span></span>

    <span data-ttu-id="a92f7-242">Déplacez le module **Rocket Launcher_Complete** objet afin que le **ParentAnchor** (le cube) soit toujours exposé.</span><span class="sxs-lookup"><span data-stu-id="a92f7-242">Move module **Rocket Launcher_Complete** object so that the **ParentAnchor** (the cube) is still exposed.</span></span>

    ![mrlearning-ASA](images/mrlearning-asa-ch1-7-2.1.png)

    <span data-ttu-id="a92f7-244">Dans l’application, les utilisateurs peuvent maintenant repositionner l’intégralité de l’expérience du lanceur Rocket en déplaçant le cube.</span><span class="sxs-lookup"><span data-stu-id="a92f7-244">In the application, users may now reposition the entire Rocket Launcher experience by moving the cube.</span></span>

    >[!TIP]
    ><span data-ttu-id="a92f7-245">Il existe un grand nombre d’expériences utilisateur pour repositionner les expériences, y compris l’utilisation d’un objet de repositionnement (tel que le cube utilisé dans ce didacticiel), l’utilisation d’un bouton pour basculer un cadre englobant qui entoure l’expérience, l’utilisation de la position et de la rotation. gizmos, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="a92f7-245">There are a variety of user experience flows for repositioning experiences including the use of a repositioning object (such as the cube used in this tutorial), the use of a button to toggle a bounding box that surrounds the experience, the use of position and rotation gizmos, and more.</span></span>

## <a name="congratulations"></a><span data-ttu-id="a92f7-246">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="a92f7-246">Congratulations</span></span>

<span data-ttu-id="a92f7-247">Dans ce didacticiel, vous avez appris les principes de base des ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="a92f7-247">In this tutorial, you learned the fundamentals of Azure Spatial Anchors.</span></span> <span data-ttu-id="a92f7-248">Cette leçon vous a fourni plusieurs boutons qui vous permettent d’explorer les différentes étapes nécessaires au démarrage et à l’arrêt d’une session Azure et à la création, le chargement et le téléchargement d’ancres Azure sur un seul appareil.</span><span class="sxs-lookup"><span data-stu-id="a92f7-248">This Lesson provided you with several buttons that let you  explore the various steps required to start and stop an Azure session and create, upload and download azure anchors on a single device.</span></span>

<span data-ttu-id="a92f7-249">Dans la leçon suivante, vous apprendrez comment enregistrer des ID d’ancrage Azure dans votre HoloLens 2 pour la récupération, même après le redémarrage de l’application, et comment transférer des ID d’ancrage entre plusieurs appareils pour obtenir un alignement spatial.</span><span class="sxs-lookup"><span data-stu-id="a92f7-249">In the next lesson, you will learn how to save Azure anchor IDs to your HoloLens 2 for retrieval, even after the application is restarted, and how to transfer anchor IDs between multiple devices to achieve spatial alignment.</span></span>

[<span data-ttu-id="a92f7-250">Leçon suivante : 2. enregistrement, récupération et partage d’ancres spatiales Azure</span><span class="sxs-lookup"><span data-stu-id="a92f7-250">Next Lesson: 2. Saving, retrieving and sharing Azure Spatial Anchors</span></span>](mrlearning-asa-ch2.md)
