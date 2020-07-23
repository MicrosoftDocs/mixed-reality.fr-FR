---
title: Tutoriels sur les services Azure Speech - 1. Intégration et utilisation de la reconnaissance vocale et de la transcription
description: Suivez ce cours pour découvrir comment implémenter le SDK Azure Speech au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: f376ab268e9c2869e48b325fa728672a16ee6d32
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86303680"
---
# <a name="1-integrating-and-using-speech-recognition-and-transcription"></a><span data-ttu-id="e5ab6-105">1. Intégration et utilisation de la reconnaissance vocale et de la transcription</span><span class="sxs-lookup"><span data-stu-id="e5ab6-105">1. Integrating and using speech recognition and transcription</span></span>

## <a name="overview"></a><span data-ttu-id="e5ab6-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="e5ab6-106">Overview</span></span>


<span data-ttu-id="e5ab6-107">Dans cette série de tutoriels, vous allez créer une application de réalité mixte qui explore l’utilisation des services Azure Speech avec le HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-107">In this tutorial series, you will create a Mixed Reality application that explores the use of Azure Speech Services with the HoloLens 2.</span></span> <span data-ttu-id="e5ab6-108">À la fin de cette série de tutoriels, vous serez en mesure d’utiliser le microphone de votre appareil pour convertir la parole en texte en temps réel, traduire votre parole en d’autres langues et exploiter la fonctionnalité Reconnaissance de l’intention pour comprendre des commandes vocales à l’aide de l’intelligence artificielle.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-108">When you complete this tutorial series, you will be able to use your device's microphone to transcribe speech to text in real time, translate your speech into other languages, and leverage the Intent recognition feature to understand voice commands using artificial intelligence.</span></span>

## <a name="objectives"></a><span data-ttu-id="e5ab6-109">Objectifs</span><span class="sxs-lookup"><span data-stu-id="e5ab6-109">Objectives</span></span>

* <span data-ttu-id="e5ab6-110">Apprendre à intégrer les services Azure Speech à une application HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="e5ab6-110">Learn how to integrate Azure Speech Services with a HoloLens 2 application</span></span>
* <span data-ttu-id="e5ab6-111">Apprendre à utiliser la reconnaissance vocale pour transcrire du texte</span><span class="sxs-lookup"><span data-stu-id="e5ab6-111">Learn how to use speech recognition to transcribe text</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5ab6-112">Prérequis</span><span class="sxs-lookup"><span data-stu-id="e5ab6-112">Prerequisites</span></span>

>[!TIP]
><span data-ttu-id="e5ab6-113">Si vous n’avez pas encore terminé la série de [tutoriels de démarrage](mr-learning-base-01.md), nous vous conseillons de le faire avant d’aller plus loin.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-113">If you have not completed the [Getting started tutorials](mr-learning-base-01.md) series yet, it's recommended that you complete those tutorials first.</span></span>

* <span data-ttu-id="e5ab6-114">PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="e5ab6-114">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="e5ab6-115">SDK Windows 10 (10.0.18362.0 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="e5ab6-115">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="e5ab6-116">Capacité de programmation C# de base</span><span class="sxs-lookup"><span data-stu-id="e5ab6-116">Some basic C# programming ability</span></span>
* <span data-ttu-id="e5ab6-117">Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)</span><span class="sxs-lookup"><span data-stu-id="e5ab6-117">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>
* <span data-ttu-id="e5ab6-118"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté</span><span class="sxs-lookup"><span data-stu-id="e5ab6-118"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.2.X installed and the Universal Windows Platform Build Support module added</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5ab6-119">La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-119">The recommended Unity version for this tutorial series is Unity 2019.2.X.</span></span> <span data-ttu-id="e5ab6-120">Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-120">This supersedes any Unity version requirements or recommendations stated in the prerequisites linked above.</span></span>

## <a name="creating-and-preparing-the-unity-project"></a><span data-ttu-id="e5ab6-121">Création et préparation du projet Unity</span><span class="sxs-lookup"><span data-stu-id="e5ab6-121">Creating and preparing the Unity project</span></span>

<span data-ttu-id="e5ab6-122">Dans cette section, vous allez créer un projet Unity et le préparer au développement avec MRTK.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-122">In this section, you will create a new Unity project and get it ready for MRTK development.</span></span>

<span data-ttu-id="e5ab6-123">Pour cela, suivez d’abord [Initialisation de votre projet et de votre première application](mr-learning-base-02.md), en excluant les instructions données dans [Générer votre application sur votre appareil](mr-learning-base-02.md#building-your-application-to-your-hololens-2), ce qui inclut les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-123">For this, first follow the [Initializing your project and first application](mr-learning-base-02.md), excluding the [Build your application to your device](mr-learning-base-02.md#building-your-application-to-your-hololens-2) instructions, which includes the following steps:</span></span>

1. <span data-ttu-id="e5ab6-124">[Création du projet Unity](mr-learning-base-02.md#creating-the-unity-project) et affectation d’un nom pertinent, par exemple *MRTK Tutorials*</span><span class="sxs-lookup"><span data-stu-id="e5ab6-124">[Creating the Unity project](mr-learning-base-02.md#creating-the-unity-project) and give it a suitable name, for example, *MRTK Tutorials*</span></span>
2. [<span data-ttu-id="e5ab6-125">Changement de plateforme de génération</span><span class="sxs-lookup"><span data-stu-id="e5ab6-125">Switching the build platform</span></span>](mr-learning-base-02.md#configuring-the-unity-project)
3. [<span data-ttu-id="e5ab6-126">Importation des ressources TextMeshPro Essential</span><span class="sxs-lookup"><span data-stu-id="e5ab6-126">Importing the TextMeshPro Essential Resources</span></span>](mr-learning-base-02.md#importing-the-textmeshpro-essential-resources)
4. [<span data-ttu-id="e5ab6-127">Importation du Mixed Reality Toolkit</span><span class="sxs-lookup"><span data-stu-id="e5ab6-127">Importing the Mixed Reality Toolkit</span></span>](mr-learning-base-02.md#importing-the-mixed-reality-toolkit)
5. [<span data-ttu-id="e5ab6-128">Configuration du projet Unity</span><span class="sxs-lookup"><span data-stu-id="e5ab6-128">Configuring the Unity project</span></span>](mr-learning-base-02.md#configuring-the-unity-project)
6. <span data-ttu-id="e5ab6-129">[Création et configuration de la scène](mr-learning-base-02.md#creating-and-configuring-the-scene), et affectation d’un nom pertinent à la scène, par exemple *AzureSpeechServices*</span><span class="sxs-lookup"><span data-stu-id="e5ab6-129">[Creating and configuring the scene](mr-learning-base-02.md#creating-and-configuring-the-scene) and give the scene a suitable name, for example, *AzureSpeechServices*</span></span>

<span data-ttu-id="e5ab6-130">Ensuite, suivez les instructions de [Modification de l’option d’affichage de la reconnaissance spatiale](mr-learning-base-03.md#changing-the-spatial-awareness-display-option) pour remplacer le profil de configuration MRTK de votre scène par **DefaultHoloLens2ConfigurationProfile** et remplacer les options d’affichage du maillage de la reconnaissance spatiale par **Occlusion**.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-130">Then follow the [Changing the Spatial Awareness Display Option](mr-learning-base-03.md#changing-the-spatial-awareness-display-option) instructions to change the MRTK configuration profile for your scene to the **DefaultHoloLens2ConfigurationProfile** and change the display options for the spatial awareness mesh to **Occlusion**.</span></span>

## <a name="configuring-the-speech-commands-start-behavior"></a><span data-ttu-id="e5ab6-131">Configuration du comportement de démarrage des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="e5ab6-131">Configuring the speech commands start behavior</span></span>

<span data-ttu-id="e5ab6-132">Étant donné que vous allez utiliser le SDK Speech pour la reconnaissance vocale et la transcription, vous avez besoin de configurer les commandes vocales MRTK se sorte qu’elles n’interfèrent pas avec la fonctionnalité du SDK Speech.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-132">Because you will use the Speech SDK for speech recognition and transcription you need to configure the MRTK Speech Commands so they do not interfere with the Speech SDK functionality.</span></span> <span data-ttu-id="e5ab6-133">Pour cela, vous pouvez modifier le comportement de démarrage des commandes vocales en passant d’un démarrage automatique à un démarrage manuel.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-133">To achieve this you can change the speech commands start behavior from Auto Start to Manual Start.</span></span>

<span data-ttu-id="e5ab6-134">Avec l’objet **MixedRealityToolkit** sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, sélectionnez l’onglet **Input**, clonez **DefaultHoloLens2InputSystemProfile** et **DefaultMixedRealitySpeechCommandsProfile**, puis remplacez le comportement de démarrage (**Start Behavior**) des commandes vocales en choisissant **Manual Start** :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-134">With the **MixedRealityToolkit** object selected in the Hierarchy window, in the Inspector window, select the **Input** tab, clone the **DefaultHoloLens2InputSystemProfile** and the **DefaultMixedRealitySpeechCommandsProfile**, and then change the speech commands **Start Behavior** to **Manual Start**:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section2-step1-1.png)

> [!TIP]
> <span data-ttu-id="e5ab6-136">Pour vous rappeler comment cloner et configurer des profils MRTK, reportez-vous aux instructions fournies dans [Configuration des profils Mixed Reality Toolkit](mr-learning-base-03.md).</span><span class="sxs-lookup"><span data-stu-id="e5ab6-136">For a reminder on how to clone and configure MRTK profiles, you can refer to the [Configuring the Mixed Reality Toolkit profiles](mr-learning-base-03.md) instructions.</span></span>

## <a name="configuring-the-capabilities"></a><span data-ttu-id="e5ab6-137">Configuration des fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="e5ab6-137">Configuring the capabilities</span></span>

<span data-ttu-id="e5ab6-138">Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings, puis recherchez la section **Player** >  **Publishing Settings** :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-138">In the Unity menu, select **Edit** > **Project Settings...** to open the Player Settings window, then locate the **Player** >  **Publishing Settings** section:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section3-step1-1.png)

<span data-ttu-id="e5ab6-140">Dans la section **Publishing Settings**, accédez à la section **Capabilities** et vérifiez que les fonctionnalités **InternetClient**, **Microphone** et **SpatialPerception**, que vous avez activées lors de la création du projet au début de ce tutoriel, sont cochées.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-140">In the  **Publishing Settings**, scroll down to the **Capabilities** section and double-check that the **InternetClient**, **Microphone**, and **SpatialPerception** capabilities, which you enabled when you created the project at the beginning of the tutorial, are enabled.</span></span> <span data-ttu-id="e5ab6-141">Activez ensuite les fonctionnalités **InternetClientServer** et **PrivateNetworkClientServer** :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-141">Then, enable the **InternetClientServer** and **PrivateNetworkClientServer** capabilities:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section3-step1-2.png)

## <a name="importing-the-tutorial-assets"></a><span data-ttu-id="e5ab6-143">Importation des ressources du tutoriel</span><span class="sxs-lookup"><span data-stu-id="e5ab6-143">Importing the tutorial assets</span></span>

<span data-ttu-id="e5ab6-144">Téléchargez et **importez** les packages personnalisés Unity suivants **dans l’ordre dans lequel ils sont listés** :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-144">Download and **import** the following Unity custom packages **in the order they are listed**:</span></span>

* <span data-ttu-id="e5ab6-145">[Microsoft.CognitiveServices.Speech.N.N.N.unitypackage](https://aka.ms/csspeech/unitypackage) (dernière version)</span><span class="sxs-lookup"><span data-stu-id="e5ab6-145">[Microsoft.CognitiveServices.Speech.N.N.N.unitypackage](https://aka.ms/csspeech/unitypackage) (latest version)</span></span>
* [<span data-ttu-id="e5ab6-146">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage</span><span class="sxs-lookup"><span data-stu-id="e5ab6-146">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.3/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage)
* [<span data-ttu-id="e5ab6-147">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpeechServices.2.3.0.0.unitypackage</span><span class="sxs-lookup"><span data-stu-id="e5ab6-147">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpeechServices.2.3.0.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-speech-services-v2.3.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpeechServices.2.3.0.0.unitypackage)

> [!TIP]
> <span data-ttu-id="e5ab6-148">Pour vous rappeler comment importer un package personnalisé Unity, reportez-vous aux instructions fournies dans [Importation du Mixed Reality Toolkit](mr-learning-base-02.md#importing-the-mixed-reality-toolkit).</span><span class="sxs-lookup"><span data-stu-id="e5ab6-148">For a reminder on how to import a Unity custom package, you can refer to the [Importing the Mixed Reality Toolkit](mr-learning-base-02.md#importing-the-mixed-reality-toolkit) instructions.</span></span>

<span data-ttu-id="e5ab6-149">Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-149">After you have imported the tutorial assets your Project window should look similar to this:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section4-step1-1.png)

## <a name="preparing-the-scene"></a><span data-ttu-id="e5ab6-151">Préparation de la scène</span><span class="sxs-lookup"><span data-stu-id="e5ab6-151">Preparing the scene</span></span>

<span data-ttu-id="e5ab6-152">Dans cette section, vous allez préparer la scène en ajoutant le préfabriqué du tutoriel et configurer le composant Lunarcom Controller (Script) pour contrôler votre scène.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-152">In this section, you will prepare the scene by adding the tutorial prefab and configure the Lunarcom Controller (Script) component to control your scene.</span></span>

<span data-ttu-id="e5ab6-153">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.AzureSpeechServices** > **Prefabs** et faites glisser le préfabriqué **Lunarcom** dans la fenêtre Hierarchy pour l’ajouter à votre scène :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-153">In the Project window, navigate to **Assets** > **MRTK.Tutorials.AzureSpeechServices** > **Prefabs** folder and drag the **Lunarcom** prefab into the Hierarchy window to add it to your scene:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-1.png)

<span data-ttu-id="e5ab6-155">Avec l’objet **Lunarcom** toujours sélectionné dans la fenêtre Hierachy, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Lunarcom Controller (Script)** à l’objet Lunarcom :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-155">With the **Lunarcom** object still selected in the Hierarchy window, in the Inspector window, use the **Add Component** button to add the **Lunarcom Controller (Script)** component to the Lunarcom object:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-2.png)

> [!NOTE]
> <span data-ttu-id="e5ab6-157">Le composant Lunarcom Controller (Script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-157">The Lunarcom Controller (Script) component is not part of MRTK.</span></span> <span data-ttu-id="e5ab6-158">Il a été fourni avec les ressources de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-158">It was provided with this tutorial's assets.</span></span>

<span data-ttu-id="e5ab6-159">L’objet **Lunarcom** étant toujours sélectionné, développez-le pour révéler ses objets enfants, puis faites glisser l’objet **Terminal** dans le champ **Terminal** du composant Lunarcom Controller (Script) :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-159">With the **Lunarcom** object still selected, expand it to reveal its child objects, then drag the **Terminal** object into the Lunarcom Controller (Script) component's **Terminal** field:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-3.png)

<span data-ttu-id="e5ab6-161">Avec l’objet **Lunarcom** toujours sélectionné, développez l’objet Terminal pour révéler ses objets enfants, puis faites glisser l’objet **ConnectionLight** dans le champ **Connection Light** du composant Lunarcom Controller (Script) et l’objet **OutputText** dans le champ **Output Text** :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-161">With the **Lunarcom** object still selected, expand the Terminal object to reveal its child objects, then drag the **ConnectionLight** object into the Lunarcom Controller (Script) component's **Connection Light** field and the **OutputText** object into the **Output Text** field:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-4.png)

<span data-ttu-id="e5ab6-163">Avec l’objet **Lunarcom** toujours sélectionné, développez l’objet Buttons pour révéler ses objets enfants, puis, dans la fenêtre Inspector, développez la liste **Buttons**, définissez **Size** sur 3, puis faites glisser les objets **MicButton**, **SatelliteButton** et **RocketButton** dans les champs **Element** 0, 1 et 2 respectivement :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-163">With the **Lunarcom** object still selected, expand the Buttons object to reveal its child objects, and then in the Inspector window, expand the **Buttons** list, set its **Size** to 3, and drag the **MicButton**, **SatelliteButton**, and **RocketButton** objects into the **Element** 0, 1, and 2 fields respectively:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-5.png)

## <a name="connecting-the-unity-project-to-the-azure-resource"></a><span data-ttu-id="e5ab6-165">Connexion du projet Unity à la ressource Azure</span><span class="sxs-lookup"><span data-stu-id="e5ab6-165">Connecting the Unity project to the Azure resource</span></span>

<span data-ttu-id="e5ab6-166">Pour utiliser les services Azure Speech, vous devez créer une ressource Azure et obtenir une clé API pour le service Speech.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-166">To use Azure Speech Services, you need to create an Azure resource and obtain an API key for the Speech Service.</span></span> <span data-ttu-id="e5ab6-167">Suivez les instructions données dans [Essayer le service Speech gratuitement](https://docs.microsoft.com/azure/cognitive-services/speech-service/get-started) et notez votre région de service (également appelée Emplacement) ainsi que votre clé API (également appelée Key1 ou Key2).</span><span class="sxs-lookup"><span data-stu-id="e5ab6-167">Follow the [Try the Speech service for free](https://docs.microsoft.com/azure/cognitive-services/speech-service/get-started) instructions and make a note of your service region (also known as Location) and API key (also known as Key1 or Key2).</span></span>

<span data-ttu-id="e5ab6-168">Dans la fenêtre Hierarchy, sélectionnez l’objet **Lunarcom**, puis dans la fenêtre Inspector, localisez la section **Speech SDK Credentials** du composant **Lunarcom Controller (Script)** et configurez-la de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-168">In the Hierarchy window, select the **Lunarcom** object, then in the Inspector window, locate the **Lunarcom Controller (Script)** component's **Speech SDK Credentials** section and configure it as follows:</span></span>

* <span data-ttu-id="e5ab6-169">Dans le champ **Speech Service API Key**, entrez votre clé API (Key1 or Key2).</span><span class="sxs-lookup"><span data-stu-id="e5ab6-169">In the **Speech Service API Key** field, enter your API key (Key1 or Key2)</span></span>
* <span data-ttu-id="e5ab6-170">Dans le champ **Speech Service Region**, entrez votre région de service (Emplacement) en utilisant des lettres minuscules et en supprimant les espaces.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-170">In the **Speech Service Region** field, enter your service region (Location) using lowercase letters and spaces removed</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section6-step1-1.png)

## <a name="using-speech-recognition-to-transcribe-speech"></a><span data-ttu-id="e5ab6-172">Utilisation de la reconnaissance vocale pour transcrire la parole</span><span class="sxs-lookup"><span data-stu-id="e5ab6-172">Using speech recognition to transcribe speech</span></span>

<span data-ttu-id="e5ab6-173">Dans la fenêtre Hierachy, sélectionnez l’objet **Lunarcom** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Lunarcom Speech Recognizer (Script)** à l’objet Lunarcom :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-173">In the Hierarchy window, select the **Lunarcom** object, then in the Inspector window, use the **Add Component** button to add the **Lunarcom Speech Recognizer (Script)** component to the Lunarcom object:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section7-step1-1.png)

> [!NOTE]
> <span data-ttu-id="e5ab6-175">Le composant Lunarcom Speech Recognizer (Script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-175">The Lunarcom Speech Recognizer (Script) component is not part of MRTK.</span></span> <span data-ttu-id="e5ab6-176">Il a été fourni avec les ressources de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-176">It was provided with this tutorial's assets.</span></span>

<span data-ttu-id="e5ab6-177">Si vous entrez maintenant en mode Game, vous pouvez tester la reconnaissance vocale en commençant par appuyer sur le bouton du microphone :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-177">If you now enter Game mode, you can test the speech recognition by first pressing the microphone button:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section7-step1-2.png)

<span data-ttu-id="e5ab6-179">Ensuite, en supposant que votre ordinateur est doté d’un microphone, quand vous dites quelque chose, votre parole est transcrite sur le panneau du terminal :</span><span class="sxs-lookup"><span data-stu-id="e5ab6-179">Then, assuming your computer has a microphone, when you say something, your speech will be transcribed on the terminal panel:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial1-section7-step1-3.png)


> [!CAUTION]
> <span data-ttu-id="e5ab6-181">L’application a besoin de se connecter à Azure, donc vérifiez que votre ordinateur/appareil est connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-181">The application needs to connect to Azure, so make sure your computer/device is connected to the internet.</span></span>

## <a name="congratulations"></a><span data-ttu-id="e5ab6-182">Félicitations</span><span class="sxs-lookup"><span data-stu-id="e5ab6-182">Congratulations</span></span>

<span data-ttu-id="e5ab6-183">Vous avez implémenté la technologie Azure de reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-183">You have implemented speech recognition powered by Azure.</span></span> <span data-ttu-id="e5ab6-184">Exécutez l’application sur votre appareil pour vérifier que tout fonctionne bien.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-184">Run the application on your device to ensure the feature is working properly.</span></span>

<span data-ttu-id="e5ab6-185">Dans le tutoriel suivant, vous allez apprendre à exécuter des commandes à l’aide de la reconnaissance vocale Azure.</span><span class="sxs-lookup"><span data-stu-id="e5ab6-185">In the next tutorial, you will learn how to execute commands using Azure speech recognition.</span></span>

[<span data-ttu-id="e5ab6-186">Tutoriel suivant : 2. Utilisation de la reconnaissance vocale pour exécuter des commandes</span><span class="sxs-lookup"><span data-stu-id="e5ab6-186">Next tutorial: 2. Using speech recognition to execute commands</span></span>](mrlearning-speechSDK-ch2.md)
