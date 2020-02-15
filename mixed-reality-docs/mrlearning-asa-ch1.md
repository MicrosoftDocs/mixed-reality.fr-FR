---
title: Didacticiels sur les ancres spatiales Azure-1. Prise en main des ancres spatiales Azure
description: Suivez ce cours pour découvrir comment implémenter Reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 21883e95e92f8808bcf270e6d8091f31933ab6fa
ms.sourcegitcommit: a580166a19294f835b8e09c780f663f228dd5de0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2020
ms.locfileid: "77250831"
---
# <a name="1-getting-started-with-azure-spatial-anchors"></a><span data-ttu-id="e2b6d-105">1. prise en main des ancres spatiales Azure</span><span class="sxs-lookup"><span data-stu-id="e2b6d-105">1. Getting started with Azure Spatial Anchors</span></span>

## <a name="overview"></a><span data-ttu-id="e2b6d-106">Overview</span><span class="sxs-lookup"><span data-stu-id="e2b6d-106">Overview</span></span>

<span data-ttu-id="e2b6d-107">Bienvenue dans la deuxième série des didacticiels HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-107">Welcome to the second series of the HoloLens 2 tutorials.</span></span> <span data-ttu-id="e2b6d-108">Dans cette série de didacticiels en trois parties, vous allez apprendre les principes de base des ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-108">In this three-part tutorial series, you will learn the fundamentals of Azure Spatial Anchors.</span></span>

<span data-ttu-id="e2b6d-109">Dans ce premier didacticiel, bien démarrer [avec les ancres spatiales Azure](mrlearning-asa-ch1.md), vous allez explorer les différentes étapes requises pour démarrer et arrêter une session Azure et créer, charger et télécharger des ancres Azure sur un seul appareil.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-109">In this first tutorial, [Getting started with Azure Spatial Anchors](mrlearning-asa-ch1.md), you will explore the various steps required to start and stop an Azure session and create, upload, and download Azure anchors on a single device.</span></span>

<span data-ttu-id="e2b6d-110">Dans le deuxième didacticiel, [l’enregistrement, la récupération et le partage d’ancres spatiales Azure](mrlearning-asa-ch2.md), vous apprendrez à enregistrer les ancres spatiales Azure dans plusieurs sessions d’application en enregistrant les informations d’ancrage dans le stockage de HoloLens 2 et en partageant ces informations d’ancre avec d’autres appareils pour un alignement d’ancrage sur plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-110">In the second tutorial, [Saving, retrieving, and sharing Azure Spatial Anchors](mrlearning-asa-ch2.md), you will learn how to save Azure Spatial Anchors across multiple app sessions by saving anchor information to the HoloLens 2's storage and how to share this anchor information to other devices for a multi-device anchor alignment.</span></span>

<span data-ttu-id="e2b6d-111">Dans le troisième didacticiel, l’affichage de commentaires sur l' [ancrage spatial Azure](mrlearning-asa-ch3.md)vous apprendra à fournir aux utilisateurs des commentaires sur les événements d’ancrage et les États lors de l’utilisation d’ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-111">In the third tutorial, [Displaying Azure Spatial Anchor feedback](mrlearning-asa-ch3.md), you will learn how to provide users with feedback about anchor events and statuses when using Azure Spatial Anchors.</span></span>

## <a name="objectives"></a><span data-ttu-id="e2b6d-112">Objectifs</span><span class="sxs-lookup"><span data-stu-id="e2b6d-112">Objectives</span></span>

* <span data-ttu-id="e2b6d-113">Découvrez les principes de base du développement avec les ancres spatiales Azure pour HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="e2b6d-113">Learn the fundamentals of developing with Azure Spatial Anchors for HoloLens 2</span></span>
* <span data-ttu-id="e2b6d-114">Créer, charger et télécharger des ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="e2b6d-114">Create, upload, and download spatial anchors</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2b6d-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e2b6d-115">Prerequisites</span></span>

>[!TIP]
><span data-ttu-id="e2b6d-116">Si vous n’avez pas encore terminé la série des [didacticiels de mise](mrlearning-base.md) en route, nous vous recommandons d’effectuer d’abord ces didacticiels.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-116">If you have not completed the [Getting started tutorials](mrlearning-base.md) series yet, it's recommended that you complete those tutorials first.</span></span>

* <span data-ttu-id="e2b6d-117">Un PC Windows 10 configuré avec les outils corrects [installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="e2b6d-117">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="e2b6d-118">Windows 10 SDK 10.0.18362.0 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="e2b6d-118">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="e2b6d-119">Certaines fonctionnalités C# de programmation de base</span><span class="sxs-lookup"><span data-stu-id="e2b6d-119">Some basic C# programming ability</span></span>
* <span data-ttu-id="e2b6d-120">Un appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)</span><span class="sxs-lookup"><span data-stu-id="e2b6d-120">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>
* <span data-ttu-id="e2b6d-121"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Hub Unity</a> avec Unity 2019.2. X installé et le module de prise en charge de la build plateforme Windows universelle ajoutée</span><span class="sxs-lookup"><span data-stu-id="e2b6d-121"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.2.X installed and the Universal Windows Platform Build Support module added</span></span>
* <span data-ttu-id="e2b6d-122">Complétez la section [créer une ressource d’ancrages spatiaux](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) du Guide de [démarrage rapide : créer une application de l’unité HoloLens qui utilise des ancres spatiales Azure](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) .</span><span class="sxs-lookup"><span data-stu-id="e2b6d-122">Complete the [Create a Spatial Anchors resource](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) section of the [Quickstart: Create a Unity HoloLens app that uses Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) tutorial.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2b6d-123">La version Unity recommandée pour cette série de didacticiels est Unity 2019.2. X.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-123">The recommended Unity version for this tutorial series is Unity 2019.2.X.</span></span> <span data-ttu-id="e2b6d-124">Cela remplace toute exigence ou recommandation de version Unity énoncées dans les conditions préalables liées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-124">This supersedes any Unity version requirements or recommendations stated in the prerequisites linked above.</span></span>

## <a name="creating-the-unity-project"></a><span data-ttu-id="e2b6d-125">Création du projet Unity</span><span class="sxs-lookup"><span data-stu-id="e2b6d-125">Creating the Unity project</span></span>
<!-- TODO: Consider renaming to 'Creating and preparing the Unity scene and project'-->

<span data-ttu-id="e2b6d-126">Dans cette section, vous allez créer un nouveau projet Unity et le préparer au développement MRTK.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-126">In this section, you will create a new Unity project and get it ready for MRTK development.</span></span> <span data-ttu-id="e2b6d-127">Pour ce faire, suivez les instructions relatives à l’initialisation de votre [projet et de votre première application](mrlearning-base-ch1.md), à l’exclusion de la [création de votre application dans les instructions de votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device) , qui comprend les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-127">For this, please follow the [Initializing your project and first application](mrlearning-base-ch1.md), excluding the [Build your application to your device](mrlearning-base-ch1.md#build-your-application-to-your-device) instructions, which includes the following steps:</span></span>

1. <span data-ttu-id="e2b6d-128">[Créez un nouveau projet Unity](mrlearning-base-ch1.md#create-new-unity-project) et donnez-lui un nom approprié, par exemple, des *didacticiels MRTK*.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-128">[Create new Unity project](mrlearning-base-ch1.md#create-new-unity-project) and give it a suitable name, for example, *MRTK Tutorials*.</span></span>

2. [<span data-ttu-id="e2b6d-129">Configurer le projet Unity pour Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="e2b6d-129">Configure the Unity project for Windows Mixed Reality</span></span>](mrlearning-base-ch1.md#configure-the-unity-project-for-windows-mixed-reality)

3. [<span data-ttu-id="e2b6d-130">Importer des ressources TextMesh Pro Essential</span><span class="sxs-lookup"><span data-stu-id="e2b6d-130">Import TextMesh Pro Essential Resources</span></span>](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources)

4. [<span data-ttu-id="e2b6d-131">Importer la boîte à outils de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="e2b6d-131">Import the Mixed Reality Toolkit</span></span>](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit)

5. [<span data-ttu-id="e2b6d-132">Configurer le projet Unity pour la réalité mixte Toolkit</span><span class="sxs-lookup"><span data-stu-id="e2b6d-132">Configure the Unity project for the Mixed Reality Toolkit</span></span>](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit)

6. <span data-ttu-id="e2b6d-133">[Ajoutez la boîte à outils de réalité mixte à la scène Unity](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) et donnez un nom approprié à la scène, par exemple *AzureSpatialAnchors*</span><span class="sxs-lookup"><span data-stu-id="e2b6d-133">[Add the Mixed Reality Toolkit to the Unity scene](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) and give the scene a suitable name, for example, *AzureSpatialAnchors*</span></span>

> [!CAUTION]
> <span data-ttu-id="e2b6d-134">Comme mentionné dans les instructions [configure the Unity for the Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit) ci-dessus, MSBuild for Unity ne prend peut-être pas en charge tous les kits de développement logiciel (SDK) que vous utiliserez et peut être difficile à désactiver une fois qu’il a été activé.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-134">As mentioned in the [Configure the Unity project for the Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit) instructions linked above, MSBuild for Unity may not support all SDKs you will be using and can be challenging to disable after it has been enabled.</span></span> <span data-ttu-id="e2b6d-135">Par conséquent, il est fortement recommandé de ne pas activer MSBuild pour Unity.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-135">Consequently, it is strongly recommended to not enable MSBuild for Unity.</span></span>

## <a name="adding-inbuilt-unity-packages"></a><span data-ttu-id="e2b6d-136">Ajout de packages Unity incorporés</span><span class="sxs-lookup"><span data-stu-id="e2b6d-136">Adding inbuilt Unity packages</span></span>
<!-- TODO: Consider renaming to 'Installing AR Foundation' -->

<span data-ttu-id="e2b6d-137">Dans cette section, vous allez installer le package d’intégration de fondation d’Unity, car il est requis par le kit de développement logiciel (SDK) d’ancre spatiale Azure que vous allez importer dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-137">In this section, you will install Unity's inbuilt AR Foundation package because it is required by the Azure Spatial Anchors SDK you will import in the next section.</span></span>

<span data-ttu-id="e2b6d-138">Dans le menu Unity, sélectionnez **fenêtre** > **Gestionnaire de package**:</span><span class="sxs-lookup"><span data-stu-id="e2b6d-138">In the Unity menu, select **Window** > **Package Manager**:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section2-step1-1.png)

> [!NOTE]
> <span data-ttu-id="e2b6d-140">Il peut s’avérer nécessaire de prendre quelques secondes avant que le package de fondation de base ne s’affiche dans la liste.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-140">It might take a few seconds before the AR Foundation package appears in the list.</span></span>

<span data-ttu-id="e2b6d-141">Dans la fenêtre du gestionnaire de package, sélectionnez **AR Foundation** et installez le package en cliquant sur le bouton **installer** :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-141">In the Package Manager window, select **AR Foundation** and install the package by clicking the **Install** button:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section2-step1-2.png)

## <a name="importing-the-tutorial-assets"></a><span data-ttu-id="e2b6d-143">Importation des ressources du didacticiel</span><span class="sxs-lookup"><span data-stu-id="e2b6d-143">Importing the tutorial assets</span></span>

<span data-ttu-id="e2b6d-144">Téléchargez et **importez** les packages personnalisés Unity suivants **dans l’ordre dans lequel ils sont répertoriés**:</span><span class="sxs-lookup"><span data-stu-id="e2b6d-144">Download and **import** the following Unity custom packages **in the order they are listed**:</span></span>

* <span data-ttu-id="e2b6d-145">[AzureSpatialAnchors. pour Unity](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)</span><span class="sxs-lookup"><span data-stu-id="e2b6d-145">[AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)</span></span>
* [<span data-ttu-id="e2b6d-146">MRTK. HoloLens2. Unity. Tutorials. Assets. GettingStarted. 2.2.0.1. pour Unity</span><span class="sxs-lookup"><span data-stu-id="e2b6d-146">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.2.0.1.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.2.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.2.0.1.unitypackage)
* [<span data-ttu-id="e2b6d-147">MRTK. HoloLens2. Unity. Tutorials. Assets. AzureSpatialAnchors. 2.2.0.0. pour Unity</span><span class="sxs-lookup"><span data-stu-id="e2b6d-147">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.2.0.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.2.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.2.0.0.unitypackage)

> [!TIP]
> <span data-ttu-id="e2b6d-148">Pour obtenir un rappel sur l’importation d’un package personnalisé Unity, vous pouvez vous reporter aux instructions [importez les instructions de la réalité mixte](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit) .</span><span class="sxs-lookup"><span data-stu-id="e2b6d-148">For a reminder on how to import a Unity custom package, you can refer to the [Import the Mixed Reality Toolkit](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit) instructions.</span></span>

<span data-ttu-id="e2b6d-149">Une fois que vous avez importé les ressources du didacticiel, votre fenêtre de projet doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-149">After you have imported the tutorial assets your Project window should look similar to this:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section3-step1-1.png)

## <a name="creating-and-preparing-the-scene"></a><span data-ttu-id="e2b6d-151">Création et préparation de la scène</span><span class="sxs-lookup"><span data-stu-id="e2b6d-151">Creating and preparing the scene</span></span>
<!-- TODO: Consider renaming to 'Preparing the scene' -->

<span data-ttu-id="e2b6d-152">Dans cette section, vous allez préparer la scène en ajoutant une partie du didacticiel prefabs.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-152">In this section, you will prepare the scene by adding some of the tutorial prefabs.</span></span>

<span data-ttu-id="e2b6d-153">Dans la fenêtre projet, accédez à **ressources** > **MRTK. Tutoriels. AzureSpatialAnchors** > dossier **Prefabs** .</span><span class="sxs-lookup"><span data-stu-id="e2b6d-153">In the Project window, navigate to **Assets** > **MRTK.Tutorials.AzureSpatialAnchors** > **Prefabs** folder.</span></span> <span data-ttu-id="e2b6d-154">Tout en maintenant enfoncé le bouton CTRL, cliquez sur **ButtonParent**, **DebugWindow**, **instructions**et **ParentAnchor** pour sélectionner les quatre prefabs :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-154">While holding down the CTRL button, click on **ButtonParent**, **DebugWindow**, **Instructions**, and **ParentAnchor** to select the four prefabs:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section4-step1-1.png)

<span data-ttu-id="e2b6d-156">Les quatre prefabs étant toujours sélectionnés, faites-les glisser dans la fenêtre de hiérarchie pour les ajouter à la scène :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-156">With the four prefabs still selected, drag them into the Hierarchy window to add them to the scene:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section4-step1-2.png)

<span data-ttu-id="e2b6d-158">Pour vous concentrer sur les objets de la scène, vous pouvez double-cliquer sur l’objet ParentAnchor, puis effectuer un zoom légèrement arrière :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-158">To focus in on the objects in the scene, you can double-click on the ParentAnchor object, and then zoom slightly out again:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section4-step1-3.png)

> [!TIP]
> <span data-ttu-id="e2b6d-160">Si vous trouvez les grandes icônes de votre scène, par exemple les icônes « t » de grande taille, vous pouvez les masquer en <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">basculant la gizmos</a> sur la position OFF.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-160">If you find the large icons in your scene, for example, the large framed 'T' icons distracting, you can hide these by <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">toggling the Gizmos</a> to the off position.</span></span>

## <a name="configuring-the-buttons-to-operate-the-scene"></a><span data-ttu-id="e2b6d-161">Configuration des boutons pour faire fonctionner la scène</span><span class="sxs-lookup"><span data-stu-id="e2b6d-161">Configuring the buttons to operate the scene</span></span>

<span data-ttu-id="e2b6d-162">Dans cette section, vous allez ajouter des scripts dans la scène pour créer une série d’événements de bouton qui illustrent les principes de base de la façon dont les ancres locales et les ancres spatiales Azure se comportent dans une application.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-162">In this section, you will add scripts into the scene to create a series of button events that demonstrate the fundamentals of how both local anchors and Azure Spatial Anchors behave in an application.</span></span>

### <a name="1-configure-the-pressable-button-holo-lens-2-script-component"></a><span data-ttu-id="e2b6d-163">1. configurer le composant Holo lentille 2 (script) du bouton enfoncé</span><span class="sxs-lookup"><span data-stu-id="e2b6d-163">1. Configure the Pressable Button Holo Lens 2 (Script) component</span></span>

<span data-ttu-id="e2b6d-164">Dans la fenêtre hiérarchie, développez l’objet **ButtonParent** et sélectionnez le premier objet enfant nommé **StartAzureSession**:</span><span class="sxs-lookup"><span data-stu-id="e2b6d-164">In the Hierarchy window, expand the **ButtonParent** object and select the first child object named **StartAzureSession**:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section5-step1-1.png)

<span data-ttu-id="e2b6d-166">Dans la fenêtre de l’inspecteur, localisez le **bouton enfoncé Holo lentille 2 (script)** et ajoutez un nouvel écouteur d’événements à l’événement **bouton enfoncé ()** en cliquant sur l’icône **+** :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-166">In the Inspector window, locate the **Pressable Button Holo Lens 2 (Script)** component and add a new event listener to the **Button Pressed ()** event by clicking the **+** icon:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section5-step1-2.png)

<span data-ttu-id="e2b6d-168">Lorsque l’objet StartAzureSession est toujours sélectionné dans la fenêtre hiérarchie, cliquez avec le bouton droit sur l’objet **ParentAnchor** de la fenêtre hiérarchie et faites-le glisser dans le champ **aucun (objet)** vide de l’écouteur d’événements que vous venez d’ajouter pour que l’objet ParentAnchor écoute les événements appuyés sur le bouton :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-168">With the StartAzureSession object still selected in the Hierarchy window, click-and-drag the **ParentAnchor** object from the Hierarchy window into the empty **None (Object)** field of the event listener you just added to make the ParentAnchor object listen for button pressed events from this button:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section5-step1-3.png)

<span data-ttu-id="e2b6d-170">Cliquez sur la liste déroulante **no Function** du même écouteur d’événements, puis sélectionnez **AnchorModuleScript** > **StartAzureSession ()** pour définir la fonction StartAzureSession () comme l’action qui est déclenchée lorsque les événements activés du bouton sont déclenchés à partir de ce bouton :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-170">Click the **No Function** dropdown of the same event listener, then select **AnchorModuleScript** > **StartAzureSession ()** to set the StartAzureSession () function as the action that is triggered when the button pressed events is fired from this button:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section5-step1-4.png)

### <a name="2-configure-the-interactable-script-component"></a><span data-ttu-id="e2b6d-172">2. configurer le composant (script) pouvant être interagi</span><span class="sxs-lookup"><span data-stu-id="e2b6d-172">2. Configure the Interactable (Script) component</span></span>

<span data-ttu-id="e2b6d-173">Lorsque l’objet StartAzureSession est toujours sélectionné dans la fenêtre hiérarchie, dans la fenêtre Inspecteur, localisez le composant **(script) pouvant être interagi** et répétez le même processus que à l’étape 1 ci-dessus pour l’événement **OnClick ()** :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-173">With the StartAzureSession object still selected in the Hierarchy window, in the Inspector window, locate the **Interactable (Script)** component and repeat the same process as in step 1 above for the **OnClick ()** event:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section5-step2-1.png)

### <a name="3-configure-the-remaining-buttons"></a><span data-ttu-id="e2b6d-175">3. configurer les autres boutons</span><span class="sxs-lookup"><span data-stu-id="e2b6d-175">3. Configure the remaining buttons</span></span>

<span data-ttu-id="e2b6d-176">Pour chacun des autres boutons, effectuez le processus décrit aux étapes 1 et 2 ci-dessus pour affecter des fonctions aux événements **bouton appuyé ()** et **OnClick ()** :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-176">For each of the remaining buttons, complete the process outlined in step 1 and 2 above to assign functions to both the **Button Pressed ()** and **OnClick ()** events:</span></span>

* <span data-ttu-id="e2b6d-177">Pour l’objet **StopAzureSession** , assignez la fonction AnchorModuleScript > **StopAzureSession ()** .</span><span class="sxs-lookup"><span data-stu-id="e2b6d-177">For the **StopAzureSession** object, assign the AnchorModuleScript > **StopAzureSession ()** function.</span></span>
* <span data-ttu-id="e2b6d-178">Pour l’objet **CreateAzureAnchor** , assignez la fonction AnchorModuleScript > **CreateAzureAnchor ()** ,</span><span class="sxs-lookup"><span data-stu-id="e2b6d-178">For the **CreateAzureAnchor** object, assign the AnchorModuleScript > **CreateAzureAnchor ()** function,</span></span>
  * <span data-ttu-id="e2b6d-179">Faites ensuite glisser à nouveau le **ParentAnchor** dans le champ vide **aucun (objet de jeu)** .</span><span class="sxs-lookup"><span data-stu-id="e2b6d-179">then drag the **ParentAnchor** again into the empty **None (Game Object)** field.</span></span>
* <span data-ttu-id="e2b6d-180">Pour l’objet **RemoveLocalAnchor** , assignez la fonction AnchorModuleScript > **RemoveLocalAnchor ()** ,</span><span class="sxs-lookup"><span data-stu-id="e2b6d-180">For the **RemoveLocalAnchor** object, assign the AnchorModuleScript > **RemoveLocalAnchor ()** function,</span></span>
  * <span data-ttu-id="e2b6d-181">Faites ensuite glisser à nouveau le **ParentAnchor** dans le champ vide **aucun (objet de jeu)** .</span><span class="sxs-lookup"><span data-stu-id="e2b6d-181">then drag the **ParentAnchor** again into the empty **None (Game Object)** field.</span></span>
* <span data-ttu-id="e2b6d-182">Pour l’objet **FindAzureAnchor** , assignez la fonction AnchorModuleScript > **FindAzureAnchor ()** .</span><span class="sxs-lookup"><span data-stu-id="e2b6d-182">For the **FindAzureAnchor** object, assign the AnchorModuleScript > **FindAzureAnchor ()** function.</span></span>
* <span data-ttu-id="e2b6d-183">Pour l’objet **DeleteAzureAnchor** , assignez la fonction AnchorModuleScript > **DeleteAzureAnchor ()** .</span><span class="sxs-lookup"><span data-stu-id="e2b6d-183">For the **DeleteAzureAnchor** object, assign the AnchorModuleScript > **DeleteAzureAnchor ()** function.</span></span>

### <a name="4-connect-the-scene-to-the-azure-resource"></a><span data-ttu-id="e2b6d-184">4. Connectez la scène à la ressource Azure</span><span class="sxs-lookup"><span data-stu-id="e2b6d-184">4. Connect the scene to the Azure resource</span></span>

<span data-ttu-id="e2b6d-185">Dans la fenêtre hiérarchie, sélectionnez l’objet **ParentAnchor** et, dans la fenêtre de l’inspecteur, faites défiler jusqu’au composant **Gestionnaire d’ancrage spatial (script)** .</span><span class="sxs-lookup"><span data-stu-id="e2b6d-185">In the Hierarchy window, select the **ParentAnchor** object and in the Inspector window, scroll down to the **Spatial Anchor Manager (Script)** component.</span></span>

<span data-ttu-id="e2b6d-186">Ensuite, dans la section **informations d’identification** , collez votre ID de compte et votre clé d’ancrage spatial, que vous avez créés dans le cadre des [conditions préalables](mrlearning-asa-ch1.md#prerequisites)de ce didacticiel, dans les champs de clé du compte d' **ancrage** spatial et des ancres **spatiales** correspondants :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-186">Then, in the **Credentials** section, paste your Spatial Anchors Account ID and Key, which you created as part of this tutorial's [Prerequisites](mrlearning-asa-ch1.md#prerequisites), into the corresponding **Spatial Anchors Account Id** and **Spatial Anchors Account Key** fields:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section5-step4-1.png)

## <a name="trying-the-basic-behaviors-of-azure-spatial-anchors"></a><span data-ttu-id="e2b6d-188">Essai des comportements de base des ancres spatiales Azure</span><span class="sxs-lookup"><span data-stu-id="e2b6d-188">Trying the basic behaviors of Azure Spatial Anchors</span></span>

<span data-ttu-id="e2b6d-189">Maintenant que votre scène est configurée pour illustrer les principes de base des ancres spatiales Azure, il est temps de déployer l’application afin de pouvoir expérimenter les ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-189">Now that your scene is configured to demonstrate the basics of Azure Spatial Anchors, it is time to deploy the app so you can experience Azure Spatial Anchors firsthand.</span></span>

### <a name="1-add-additional-required-capabilities"></a><span data-ttu-id="e2b6d-190">1. ajouter des fonctionnalités supplémentaires requises</span><span class="sxs-lookup"><span data-stu-id="e2b6d-190">1. Add additional required capabilities</span></span>

<span data-ttu-id="e2b6d-191">Dans le menu Unity, sélectionnez **modifier** > **paramètres du projet...** pour ouvrir la fenêtre Paramètres du lecteur :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-191">In the Unity menu, select **Edit** > **Project Settings...** to open the Player Settings window:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section6-step1-1.png)

<span data-ttu-id="e2b6d-193">Dans la fenêtre Paramètres du lecteur, sélectionnez **lecteur** , puis **paramètres de publication**:</span><span class="sxs-lookup"><span data-stu-id="e2b6d-193">In the Player Settings window, select **Player** and then **Publishing Settings**:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section6-step1-2.png)

<span data-ttu-id="e2b6d-195">Dans les **paramètres de publication**, faites défiler jusqu’à la section **fonctionnalités** et vérifiez que les fonctionnalités **internetclient**, **microphone**et **SpatialPerception** , que vous avez activées lors de la création du projet au début du didacticiel, sont activées.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-195">In the  **Publishing Settings**, scroll down to the **Capabilities** section and double-check that the **InternetClient**, **Microphone**, and **SpatialPerception** capabilities, which you enabled when you created the project at the beginning of the tutorial, are enabled.</span></span> <span data-ttu-id="e2b6d-196">Ensuite, activez les fonctionnalités **InternetClientServer**, **PrivateNetworkClientServer**, **RemovableStorage**et **webcam** :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-196">Then, enabled the **InternetClientServer**, **PrivateNetworkClientServer**, **RemovableStorage**, and **Webcam** capabilities:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section6-step1-3.png)

### <a name="2-deploy-the-app-to-your-hololens-2"></a><span data-ttu-id="e2b6d-198">2. Déployez l’application sur votre HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="e2b6d-198">2. Deploy the app to your HoloLens 2</span></span>

<span data-ttu-id="e2b6d-199">Les ancres spatiales Azure ne peuvent pas s’exécuter dans Unity. pour tester la fonctionnalité d’ancrages spatiaux Azure, vous devez déployer le projet sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-199">Azure Spatial Anchors can not run in Unity, so to test the Azure Spatial Anchors functionality, you need to deploy the project to your device.</span></span>

> [!TIP]
> <span data-ttu-id="e2b6d-200">Pour obtenir un rappel sur la création et le déploiement de votre projet Unity dans HoloLens 2, vous pouvez vous reporter à la rubrique [créer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device) .</span><span class="sxs-lookup"><span data-stu-id="e2b6d-200">For a reminder on how to build and deploy your Unity project to HoloLens 2, you can refer to the [Build your application to your device](mrlearning-base-ch1.md#build-your-application-to-your-device) instructions.</span></span>

### <a name="3-run-the-app-on-your-hololens-2-and-follow-the-in-app-instructions"></a><span data-ttu-id="e2b6d-201">3. Exécutez l’application sur votre HoloLens 2 et suivez les instructions de l’application</span><span class="sxs-lookup"><span data-stu-id="e2b6d-201">3. Run the app on your HoloLens 2 and follow the in-app instructions</span></span>

> [!CAUTION]
> <span data-ttu-id="e2b6d-202">Les ancres spatiales Azure utilisent Internet pour enregistrer et charger les données d’ancrage. Assurez-vous que votre appareil est connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-202">Azure Spatial Anchors uses the internet to save and load the anchor data so make sure your device is connected to the internet.</span></span>

<span data-ttu-id="e2b6d-203">Lorsque l’application est en cours d’exécution sur votre appareil, suivez les instructions à l’écran affichées dans le panneau d’instructions du didacticiel d’ancrage spatial Azure :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-203">When the application is running on your device, follow the on-screen instructions displayed on the Azure Spatial Anchor Tutorial Instructions panel:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section6-step3-1.png)

## <a name="anchoring-an-experience"></a><span data-ttu-id="e2b6d-205">Ancrage d’une expérience</span><span class="sxs-lookup"><span data-stu-id="e2b6d-205">Anchoring an experience</span></span>

<span data-ttu-id="e2b6d-206">Dans les sections précédentes, vous avez appris les principes de base des ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-206">In the previous sections, you learned the fundamentals of Azure Spatial Anchors.</span></span> <span data-ttu-id="e2b6d-207">Nous avons utilisé un cube pour représenter et visualiser l’objet de jeu parent avec l’ancre attachée.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-207">We used a cube to represent and visualize the parent game object with the attached anchor.</span></span> <span data-ttu-id="e2b6d-208">Dans cette section, vous allez apprendre à ancrer une expérience complète en la plaçant en tant qu’enfant de l’objet ParentAnchor.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-208">In this section, you will learn how to anchor an entire experience by placing it as a child of the ParentAnchor object.</span></span>

### <a name="1-add-the-rocket-launcher-experience"></a><span data-ttu-id="e2b6d-209">1. ajouter l’expérience du lanceur Rocket</span><span class="sxs-lookup"><span data-stu-id="e2b6d-209">1. Add the Rocket Launcher experience</span></span>

<span data-ttu-id="e2b6d-210">Dans la fenêtre projet, accédez aux **ressources** > **MRTK. Tutoriels. GettingStarted** > **Prefabs** > dossier **RocketLauncher** et sélectionnez le **RocketLauncher_Complete** Prefab :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-210">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** > **RocketLauncher** folder and select the **RocketLauncher_Complete** prefab:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section7-step1-1.png)

<span data-ttu-id="e2b6d-212">Avec la RocketLauncher_Complete Prefab toujours sélectionnée, faites-la glisser sur l’objet **ParentAnchor** dans la fenêtre hiérarchie pour en faire un enfant de l’objet ParentAnchor :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-212">With the RocketLauncher_Complete prefab still selected, drag it on top of the **ParentAnchor** object in the Hierarchy window to make it a child of the ParentAnchor object:</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section7-step1-2.png)

### <a name="2-reposition-the-rocket-launcher-experience"></a><span data-ttu-id="e2b6d-214">2. repositionner l’expérience du lanceur Rocket</span><span class="sxs-lookup"><span data-stu-id="e2b6d-214">2. Reposition the Rocket Launcher experience</span></span>

<span data-ttu-id="e2b6d-215">Positionner, faire pivoter et mettre à l’échelle l’objet **RocketLauncher_Complete** avec une mise à l’échelle et une orientation appropriées, tout en veillant à ce que l’objet **ParentAnchor** soit toujours exposé, par exemple :</span><span class="sxs-lookup"><span data-stu-id="e2b6d-215">Position, rotate, and scale the **RocketLauncher_Complete** object to a suitable scale and orientation, while also ensuring the **ParentAnchor** object is still exposed, for example:</span></span>

* <span data-ttu-id="e2b6d-216">Transformer la **position** X = 1, Y = 0, Z = 3,75</span><span class="sxs-lookup"><span data-stu-id="e2b6d-216">Transform **Position** X = 1, Y = 0, Z = 3.75</span></span>
* <span data-ttu-id="e2b6d-217">Transformation de **rotation** X = 0, Y = 90, Z = 0</span><span class="sxs-lookup"><span data-stu-id="e2b6d-217">Transform **Rotation** X = 0, Y = 90, Z = 0</span></span>
* <span data-ttu-id="e2b6d-218">Transformation **Scale** X = 10, Y = 10, Z = 10</span><span class="sxs-lookup"><span data-stu-id="e2b6d-218">Transform **Scale** X = 10, Y = 10, Z = 10</span></span>

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section7-step2-1.png)

<span data-ttu-id="e2b6d-220">Dans l’application, les utilisateurs peuvent maintenant repositionner l’intégralité de l’expérience du lanceur Rocket en déplaçant le cube.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-220">In the application, users may now reposition the entire Rocket Launcher experience by moving the cube.</span></span>

> [!TIP]
> <span data-ttu-id="e2b6d-221">Il existe un grand nombre d’expériences utilisateur pour repositionner les expériences, y compris l’utilisation d’un objet de repositionnement (tel que le cube utilisé dans ce didacticiel), l’utilisation d’un bouton pour basculer un cadre englobant qui entoure l’expérience, l’utilisation de la position et de la rotation. gizmos, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-221">There are a variety of user experience flows for repositioning experiences including the use of a repositioning object (such as the cube used in this tutorial), the use of a button to toggle a bounding box that surrounds the experience, the use of position and rotation gizmos, and more.</span></span>

## <a name="congratulations"></a><span data-ttu-id="e2b6d-222">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="e2b6d-222">Congratulations</span></span>

<span data-ttu-id="e2b6d-223">Dans ce didacticiel, vous avez appris les principes de base des ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-223">In this tutorial, you learned the fundamentals of Azure Spatial Anchors.</span></span> <span data-ttu-id="e2b6d-224">Ce didacticiel vous a fourni plusieurs boutons qui vous permettent d’explorer les différentes étapes requises pour démarrer et arrêter une session d’ancre spatiale Azure et créer, charger et télécharger des ancres spatiales Azure sur un seul appareil.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-224">The tutorial provided you with several buttons that let you explore the various steps required to start and stop an Azure Spatial Anchors session and create, upload and download Azure Spatial Anchors on a single device.</span></span>

<span data-ttu-id="e2b6d-225">Dans la leçon suivante, vous apprendrez comment enregistrer des ID d’ancrage Azure dans votre HoloLens 2 pour la récupération, même après le redémarrage de l’application, et comment transférer des ID d’ancrage entre plusieurs appareils pour obtenir un alignement spatial.</span><span class="sxs-lookup"><span data-stu-id="e2b6d-225">In the next lesson, you will learn how to save Azure anchor IDs to your HoloLens 2 for retrieval, even after the application is restarted, and how to transfer anchor IDs between multiple devices to achieve spatial alignment.</span></span>

[<span data-ttu-id="e2b6d-226">Leçon suivante : 2. enregistrement, récupération et partage d’ancres spatiales Azure</span><span class="sxs-lookup"><span data-stu-id="e2b6d-226">Next Lesson: 2. Saving, retrieving and sharing Azure Spatial Anchors</span></span>](mrlearning-asa-ch2.md)
