---
title: Tutoriels sur les services Azure Speech - 1. Intégration et utilisation de la reconnaissance vocale et de la transcription
description: Suivez ce cours pour découvrir comment implémenter le SDK Azure Speech au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: a72eb808adbc14df65c55e694ea985d97f9ec24c
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79032562"
---
# <a name="1-integrating-and-using-speech-recognition-and-transcription"></a><span data-ttu-id="fe61e-105">1. Intégration et utilisation de la reconnaissance vocale et de la transcription</span><span class="sxs-lookup"><span data-stu-id="fe61e-105">1. Integrating and using speech recognition and transcription</span></span>

## <a name="overview"></a><span data-ttu-id="fe61e-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="fe61e-106">Overview</span></span>


<span data-ttu-id="fe61e-107">Dans cette série de tutoriels, vous allez créer une application de réalité mixte qui explore l’utilisation des services Azure Speech avec le HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="fe61e-107">In this tutorial series, you will create a Mixed Reality application that explores the use of Azure Speech Services with the HoloLens 2.</span></span> <span data-ttu-id="fe61e-108">À la fin de cette série de tutoriels, vous serez en mesure d’utiliser le microphone de votre appareil pour convertir la parole en texte en temps réel, traduire votre parole en d’autres langues et exploiter la fonctionnalité Reconnaissance de l’intention pour comprendre des commandes vocales à l’aide de l’intelligence artificielle.</span><span class="sxs-lookup"><span data-stu-id="fe61e-108">When you complete this tutorial series, you will be able to use your device's microphone to transcribe speech to text in real time, translate your speech into other languages, and leverage the Intent recognition feature to understand voice commands using artificial intelligence.</span></span>

## <a name="objectives"></a><span data-ttu-id="fe61e-109">Objectifs</span><span class="sxs-lookup"><span data-stu-id="fe61e-109">Objectives</span></span>

* <span data-ttu-id="fe61e-110">Apprendre à intégrer les services Azure Speech à une application HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="fe61e-110">Learn how to integrate Azure Speech Services with a HoloLens 2 application</span></span>
* <span data-ttu-id="fe61e-111">Apprendre à utiliser la reconnaissance vocale pour transcrire du texte</span><span class="sxs-lookup"><span data-stu-id="fe61e-111">Learn how to use speech recognition to transcribe text</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe61e-112">Prérequis</span><span class="sxs-lookup"><span data-stu-id="fe61e-112">Prerequisites</span></span>

>[!TIP]
><span data-ttu-id="fe61e-113">Si vous n’avez pas encore terminé la série de [tutoriels de démarrage](mrlearning-base.md), nous vous conseillons de le faire avant d’aller plus loin.</span><span class="sxs-lookup"><span data-stu-id="fe61e-113">If you have not completed the [Getting started tutorials](mrlearning-base.md) series yet, it's recommended that you complete those tutorials first.</span></span>

* <span data-ttu-id="fe61e-114">PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="fe61e-114">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="fe61e-115">SDK Windows 10 (10.0.18362.0 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="fe61e-115">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="fe61e-116">Capacité de programmation C# de base</span><span class="sxs-lookup"><span data-stu-id="fe61e-116">Some basic C# programming ability</span></span>
* <span data-ttu-id="fe61e-117">Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)</span><span class="sxs-lookup"><span data-stu-id="fe61e-117">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>
* <span data-ttu-id="fe61e-118"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté</span><span class="sxs-lookup"><span data-stu-id="fe61e-118"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.2.X installed and the Universal Windows Platform Build Support module added</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe61e-119">La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X.</span><span class="sxs-lookup"><span data-stu-id="fe61e-119">The recommended Unity version for this tutorial series is Unity 2019.2.X.</span></span> <span data-ttu-id="fe61e-120">Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="fe61e-120">This supersedes any Unity version requirements or recommendations stated in the prerequisites linked above.</span></span>

## <a name="creating-and-preparing-the-unity-project"></a><span data-ttu-id="fe61e-121">Création et préparation du projet Unity</span><span class="sxs-lookup"><span data-stu-id="fe61e-121">Creating and preparing the Unity project</span></span>

<span data-ttu-id="fe61e-122">Dans cette section, vous allez créer un projet Unity et le préparer au développement avec MRTK.</span><span class="sxs-lookup"><span data-stu-id="fe61e-122">In this section, you will create a new Unity project and get it ready for MRTK development.</span></span>

<span data-ttu-id="fe61e-123">Pour cela, suivez d’abord [Initialisation de votre projet et de votre première application](mrlearning-base-ch1.md), en excluant les instructions données dans [Générer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device), ce qui inclut les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="fe61e-123">For this, first follow the [Initializing your project and first application](mrlearning-base-ch1.md), excluding the [Build your application to your device](mrlearning-base-ch1.md#build-your-application-to-your-device) instructions, which includes the following steps:</span></span>

1. <span data-ttu-id="fe61e-124">[Créer un projet Unity](mrlearning-base-ch1.md#create-new-unity-project) et lui donner un nom approprié, par exemple *MRTK Tutorials*</span><span class="sxs-lookup"><span data-stu-id="fe61e-124">[Create new Unity project](mrlearning-base-ch1.md#create-new-unity-project) and give it a suitable name, for example, *MRTK Tutorials*</span></span>

2. [<span data-ttu-id="fe61e-125">Configurer le projet Unity pour Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="fe61e-125">Configure the Unity project for Windows Mixed Reality</span></span>](mrlearning-base-ch1.md#configure-the-unity-project-for-windows-mixed-reality)

3. [<span data-ttu-id="fe61e-126">Importer les ressources essentielles TextMeshPro</span><span class="sxs-lookup"><span data-stu-id="fe61e-126">Import TextMesh Pro Essential Resources</span></span>](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources)

4. [<span data-ttu-id="fe61e-127">Importer Mixed Reality Toolkit</span><span class="sxs-lookup"><span data-stu-id="fe61e-127">Import the Mixed Reality Toolkit</span></span>](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit)

5. [<span data-ttu-id="fe61e-128">Configurer le projet Unity pour Mixed Reality Toolkit</span><span class="sxs-lookup"><span data-stu-id="fe61e-128">Configure the Unity project for the Mixed Reality Toolkit</span></span>](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit)

6. <span data-ttu-id="fe61e-129">[Ajouter Mixed Reality Toolkit à la scène Unity](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) et donner à la scène un nom approprié, par exemple *AzureSpeechServices*</span><span class="sxs-lookup"><span data-stu-id="fe61e-129">[Add the Mixed Reality Toolkit to the Unity scene](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) and give the scene a suitable name, for example, *AzureSpeechServices*</span></span>

<span data-ttu-id="fe61e-130">Ensuite, suivez les instructions du [Guide pratique pour configurer les profils Mixed Reality Toolkit (Modifier l’option d’affichage de la sensibilisation spatiale)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) pour remplacer le profil de configuration MRTK de votre scène par **DefaultHoloLens2ConfigurationProfile** et pour remplacer les options d’affichage du maillage de la sensibilisation spatiale par **Occlusion**.</span><span class="sxs-lookup"><span data-stu-id="fe61e-130">Then follow the [How to configure the Mixed Reality Toolkit Profiles (Change Spatial Awareness Display Option)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) instructions to change the MRTK configuration profile for your scene to the **DefaultHoloLens2ConfigurationProfile** and change the display options for the spatial awareness mesh to **Occlusion**.</span></span>

> [!CAUTION]
> <span data-ttu-id="fe61e-131">Comme mentionné dans les instructions de l’étape [Configurer le projet Unity pour Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit) dont le lien est disponible ci-dessus, il est fortement recommandé de ne pas activer MSBuild pour Unity.</span><span class="sxs-lookup"><span data-stu-id="fe61e-131">As mentioned in the [Configure the Unity project for the Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit) instructions linked above, it is strongly recommended to not enable MSBuild for Unity.</span></span>

## <a name="configuring-the-speech-commands-start-behavior"></a><span data-ttu-id="fe61e-132">Configuration du comportement de démarrage des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="fe61e-132">Configuring the speech commands start behavior</span></span>

<span data-ttu-id="fe61e-133">Étant donné que vous allez utiliser le SDK Speech pour la reconnaissance vocale et la transcription, vous avez besoin de configurer les commandes vocales MRTK se sorte qu’elles n’interfèrent pas avec la fonctionnalité du SDK Speech.</span><span class="sxs-lookup"><span data-stu-id="fe61e-133">Because you will use the Speech SDK for speech recognition and transcription you need to configure the MRTK Speech Commands so they do not interfere with the Speech SDK functionality.</span></span> <span data-ttu-id="fe61e-134">Pour cela, vous pouvez modifier le comportement de démarrage des commandes vocales en passant d’un démarrage automatique à un démarrage manuel.</span><span class="sxs-lookup"><span data-stu-id="fe61e-134">To achieve this you can change the speech commands start behavior from Auto Start to Manual Start.</span></span>

<span data-ttu-id="fe61e-135">Avec l’objet **MixedRealityToolkit** sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, sélectionnez l’onglet **Input**, clonez **DefaultHoloLens2InputSystemProfile** et **DefaultMixedRealitySpeechCommandsProfile**, puis remplacez le comportement de démarrage (**Start Behavior**) des commandes vocales en choisissant **Manual Start** :</span><span class="sxs-lookup"><span data-stu-id="fe61e-135">With the **MixedRealityToolkit** object selected in the Hierarchy window, in the Inspector window, select the **Input** tab, clone the **DefaultHoloLens2InputSystemProfile** and the **DefaultMixedRealitySpeechCommandsProfile**, and then change the speech commands **Start Behavior** to **Manual Start**:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section2-step1-1.png)

> [!TIP]
> <span data-ttu-id="fe61e-137">Pour obtenir un rappel sur la façon de cloner et de configurer des profils MRTK, vous pouvez vous reportez aux instructions données dans le [Guide pratique pour configurer les profils Mixed Reality Toolkit (Modifier l’option d’affichage de la sensibilisation spatiale)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option).</span><span class="sxs-lookup"><span data-stu-id="fe61e-137">For a reminder on how to clone and configure MRTK profiles, you can refer to the [How to configure the Mixed Reality Toolkit Profiles (Change Spatial Awareness Display Option)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) instructions.</span></span>

## <a name="configuring-the-capabilities"></a><span data-ttu-id="fe61e-138">Configuration des fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="fe61e-138">Configuring the capabilities</span></span>

<span data-ttu-id="fe61e-139">Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings, puis recherchez la section **Player** >  **Publishing Settings** :</span><span class="sxs-lookup"><span data-stu-id="fe61e-139">In the Unity menu, select **Edit** > **Project Settings...** to open the Player Settings window, then locate the **Player** >  **Publishing Settings** section:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section3-step1-1.png)

<span data-ttu-id="fe61e-141">Dans la section **Publishing Settings**, accédez à la section **Capabilities** et vérifiez que les fonctionnalités **InternetClient**, **Microphone** et **SpatialPerception**, que vous avez activées lors de la création du projet au début de ce tutoriel, sont cochées.</span><span class="sxs-lookup"><span data-stu-id="fe61e-141">In the  **Publishing Settings**, scroll down to the **Capabilities** section and double-check that the **InternetClient**, **Microphone**, and **SpatialPerception** capabilities, which you enabled when you created the project at the beginning of the tutorial, are enabled.</span></span> <span data-ttu-id="fe61e-142">Activez ensuite les fonctionnalités **InternetClientServer** et **PrivateNetworkClientServer** :</span><span class="sxs-lookup"><span data-stu-id="fe61e-142">Then, enable the **InternetClientServer** and **PrivateNetworkClientServer** capabilities:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section3-step1-2.png)

## <a name="importing-the-tutorial-assets"></a><span data-ttu-id="fe61e-144">Importation des ressources du tutoriel</span><span class="sxs-lookup"><span data-stu-id="fe61e-144">Importing the tutorial assets</span></span>

<span data-ttu-id="fe61e-145">Téléchargez et **importez** les packages personnalisés Unity suivants **dans l’ordre dans lequel ils sont listés** :</span><span class="sxs-lookup"><span data-stu-id="fe61e-145">Download and **import** the following Unity custom packages **in the order they are listed**:</span></span>

* <span data-ttu-id="fe61e-146">[Microsoft.CognitiveServices.Speech.N.N.N.unitypackage](https://aka.ms/csspeech/unitypackage) (dernière version)</span><span class="sxs-lookup"><span data-stu-id="fe61e-146">[Microsoft.CognitiveServices.Speech.N.N.N.unitypackage](https://aka.ms/csspeech/unitypackage) (latest version)</span></span>
* [<span data-ttu-id="fe61e-147">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage</span><span class="sxs-lookup"><span data-stu-id="fe61e-147">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.2/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage)
* [<span data-ttu-id="fe61e-148">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpeechServices.2.3.0.0.unitypackage</span><span class="sxs-lookup"><span data-stu-id="fe61e-148">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpeechServices.2.3.0.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-speech-services-v2.3.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpeechServices.2.3.0.0.unitypackage)

> [!TIP]
> <span data-ttu-id="fe61e-149">Pour obtenir un rappel sur la façon d’importer un package personnalisé Unity, vous pouvez vous reporter aux instructions données dans [Importer Mixed Reality Toolkit](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit).</span><span class="sxs-lookup"><span data-stu-id="fe61e-149">For a reminder on how to import a Unity custom package, you can refer to the [Import the Mixed Reality Toolkit](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit) instructions.</span></span>

<span data-ttu-id="fe61e-150">Une fois que vous avez importé les ressources du tutoriel, votre fenêtre de projet doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="fe61e-150">After you have imported the tutorial assets your Project window should look similar to this:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section4-step1-1.png)

## <a name="preparing-the-scene"></a><span data-ttu-id="fe61e-152">Préparation de la scène</span><span class="sxs-lookup"><span data-stu-id="fe61e-152">Preparing the scene</span></span>

<span data-ttu-id="fe61e-153">Dans cette section, vous allez préparer la scène en ajoutant le préfabriqué du tutoriel et configurer le composant Lunarcom Controller (Script) pour contrôler votre scène.</span><span class="sxs-lookup"><span data-stu-id="fe61e-153">In this section, you will prepare the scene by adding the tutorial prefab and configure the Lunarcom Controller (Script) component to control your scene.</span></span>

<span data-ttu-id="fe61e-154">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.AzureSpeechServices** > **Prefabs** et faites glisser le préfabriqué **Lunarcom** dans la fenêtre Hierarchy pour l’ajouter à votre scène :</span><span class="sxs-lookup"><span data-stu-id="fe61e-154">In the Project window, navigate to **Assets** > **MRTK.Tutorials.AzureSpeechServices** > **Prefabs** folder and drag the **Lunarcom** prefab into the Hierarchy window to add it to your scene:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-1.png)

<span data-ttu-id="fe61e-156">Avec l’objet **Lunarcom** toujours sélectionné dans la fenêtre Hierachy, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Lunarcom Controller (Script)** à l’objet Lunarcom :</span><span class="sxs-lookup"><span data-stu-id="fe61e-156">With the **Lunarcom** object still selected in the Hierarchy window, in the Inspector window, use the **Add Component** button to add the **Lunarcom Controller (Script)** component to the Lunarcom object:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-2.png)

> [!NOTE]
> <span data-ttu-id="fe61e-158">Le composant Lunarcom Controller (Script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="fe61e-158">The Lunarcom Controller (Script) component is not part of MRTK.</span></span> <span data-ttu-id="fe61e-159">Il a été fourni avec les ressources de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="fe61e-159">It was provided with this tutorial's assets.</span></span>

<span data-ttu-id="fe61e-160">L’objet **Lunarcom** étant toujours sélectionné, développez-le pour révéler ses objets enfants, puis faites glisser l’objet **Terminal** dans le champ **Terminal** du composant Lunarcom Controller (Script) :</span><span class="sxs-lookup"><span data-stu-id="fe61e-160">With the **Lunarcom** object still selected, expand it to reveal its child objects, then drag the **Terminal** object into the Lunarcom Controller (Script) component's **Terminal** field:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-3.png)

<span data-ttu-id="fe61e-162">Avec l’objet **Lunarcom** toujours sélectionné, développez l’objet Terminal pour révéler ses objets enfants, puis faites glisser l’objet **ConnectionLight** dans le champ **Connection Light** du composant Lunarcom Controller (Script) et l’objet **OutputText** dans le champ **Output Text** :</span><span class="sxs-lookup"><span data-stu-id="fe61e-162">With the **Lunarcom** object still selected, expand the Terminal object to reveal its child objects, then drag the **ConnectionLight** object into the Lunarcom Controller (Script) component's **Connection Light** field and the **OutputText** object into the **Output Text** field:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-4.png)

<span data-ttu-id="fe61e-164">Avec l’objet **Lunarcom** toujours sélectionné, développez l’objet Buttons pour révéler ses objets enfants, puis, dans la fenêtre Inspector, développez la liste **Buttons**, définissez **Size** sur 3, puis faites glisser les objets **MicButton**, **SatelliteButton** et **RocketButton** dans les champs **Element** 0, 1 et 2 respectivement :</span><span class="sxs-lookup"><span data-stu-id="fe61e-164">With the **Lunarcom** object still selected, expand the Buttons object to reveal its child objects, and then in the Inspector window, expand the **Buttons** list, set its **Size** to 3, and drag the **MicButton**, **SatelliteButton**, and **RocketButton** objects into the **Element** 0, 1, and 2 fields respectively:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-5.png)

## <a name="connecting-the-unity-project-to-the-azure-resource"></a><span data-ttu-id="fe61e-166">Connexion du projet Unity à la ressource Azure</span><span class="sxs-lookup"><span data-stu-id="fe61e-166">Connecting the Unity project to the Azure resource</span></span>

<span data-ttu-id="fe61e-167">Pour utiliser les services Azure Speech, vous devez créer une ressource Azure et obtenir une clé API pour le service Speech.</span><span class="sxs-lookup"><span data-stu-id="fe61e-167">To use Azure Speech Services, you need to create an Azure resource and obtain an API key for the Speech Service.</span></span> <span data-ttu-id="fe61e-168">Suivez les instructions données dans [Essayer le service Speech gratuitement](https://docs.microsoft.com/azure/cognitive-services/speech-service/get-started) et notez votre région de service (également appelée Emplacement) ainsi que votre clé API (également appelée Key1 ou Key2).</span><span class="sxs-lookup"><span data-stu-id="fe61e-168">Follow the [Try the Speech service for free](https://docs.microsoft.com/azure/cognitive-services/speech-service/get-started) instructions and make a note of your service region (also known as Location) and API key (also known as Key1 or Key2).</span></span>

<span data-ttu-id="fe61e-169">Dans la fenêtre Hierarchy, sélectionnez l’objet **Lunarcom**, puis dans la fenêtre Inspector, localisez la section **Speech SDK Credentials** du composant **Lunarcom Controller (Script)** et configurez-la de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="fe61e-169">In the Hierarchy window, select the **Lunarcom** object, then in the Inspector window, locate the **Lunarcom Controller (Script)** component's **Speech SDK Credentials** section and configure it as follows:</span></span>

* <span data-ttu-id="fe61e-170">Dans le champ **Speech Service API Key**, entrez votre clé API (Key1 or Key2).</span><span class="sxs-lookup"><span data-stu-id="fe61e-170">In the **Speech Service API Key** field, enter your API key (Key1 or Key2)</span></span>
* <span data-ttu-id="fe61e-171">Dans le champ **Speech Service Region**, entrez votre région de service (Emplacement) en utilisant des lettres minuscules et en supprimant les espaces.</span><span class="sxs-lookup"><span data-stu-id="fe61e-171">In the **Speech Service Region** field, enter your service region (Location) using lowercase letters and spaces removed</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section6-step1-1.png)

## <a name="using-speech-recognition-to-transcribe-speech"></a><span data-ttu-id="fe61e-173">Utilisation de la reconnaissance vocale pour transcrire la parole</span><span class="sxs-lookup"><span data-stu-id="fe61e-173">Using speech recognition to transcribe speech</span></span>

<span data-ttu-id="fe61e-174">Dans la fenêtre Hierachy, sélectionnez l’objet **Lunarcom** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Lunarcom Speech Recognizer (Script)** à l’objet Lunarcom :</span><span class="sxs-lookup"><span data-stu-id="fe61e-174">In the Hierarchy window, select the **Lunarcom** object, then in the Inspector window, use the **Add Component** button to add the **Lunarcom Speech Recognizer (Script)** component to the Lunarcom object:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section7-step1-1.png)

> [!NOTE]
> <span data-ttu-id="fe61e-176">Le composant Lunarcom Speech Recognizer (Script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="fe61e-176">The Lunarcom Speech Recognizer (Script) component is not part of MRTK.</span></span> <span data-ttu-id="fe61e-177">Il a été fourni avec les ressources de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="fe61e-177">It was provided with this tutorial's assets.</span></span>

<span data-ttu-id="fe61e-178">Si vous entrez maintenant en mode Game, vous pouvez tester la reconnaissance vocale en commençant par appuyer sur le bouton du microphone :</span><span class="sxs-lookup"><span data-stu-id="fe61e-178">If you now enter Game mode, you can test the speech recognition by first pressing the microphone button:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section7-step1-2.png)

<span data-ttu-id="fe61e-180">Ensuite, en supposant que votre ordinateur est doté d’un microphone, quand vous dites quelque chose, votre parole est transcrite sur le panneau du terminal :</span><span class="sxs-lookup"><span data-stu-id="fe61e-180">Then, assuming your computer has a microphone, when you say something, your speech will be transcribed on the terminal panel:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section7-step1-3.png)


> [!CAUTION]
> <span data-ttu-id="fe61e-182">L’application a besoin de se connecter à Azure, donc vérifiez que votre ordinateur/appareil est connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="fe61e-182">The application needs to connect to Azure, so make sure your computer/device is connected to the internet.</span></span>

## <a name="congratulations"></a><span data-ttu-id="fe61e-183">Félicitations</span><span class="sxs-lookup"><span data-stu-id="fe61e-183">Congratulations</span></span>

<span data-ttu-id="fe61e-184">Vous avez implémenté la technologie Azure de reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="fe61e-184">You have implemented speech recognition powered by Azure.</span></span> <span data-ttu-id="fe61e-185">Exécutez l’application sur votre appareil pour vérifier que tout fonctionne bien.</span><span class="sxs-lookup"><span data-stu-id="fe61e-185">Run the application on your device to ensure the feature is working properly.</span></span>

<span data-ttu-id="fe61e-186">Dans le tutoriel suivant, vous allez apprendre à exécuter des commandes à l’aide de la reconnaissance vocale Azure.</span><span class="sxs-lookup"><span data-stu-id="fe61e-186">In the next tutorial, you will learn how to execute commands using Azure speech recognition.</span></span>

[<span data-ttu-id="fe61e-187">Tutoriel suivant : 2. Utilisation de la reconnaissance vocale pour exécuter des commandes</span><span class="sxs-lookup"><span data-stu-id="fe61e-187">Next tutorial: 2. Using speech recognition to execute commands</span></span>](mrlearning-speechSDK-ch2.md)
