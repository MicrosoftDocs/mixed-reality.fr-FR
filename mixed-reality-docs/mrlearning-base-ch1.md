---
title: Tutoriels de démarrage - 2. Initialisation de votre projet et de votre première application
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 11/01/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: d0c166f760884efab9719ecba1ff83285872e2ef
ms.sourcegitcommit: 23b130d03fea46a50a712b8301fe4e5deed6cf9c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2019
ms.locfileid: "75334413"
---
# <a name="2-initializing-your-project-and-first-application"></a><span data-ttu-id="cd5aa-105">2. Initialisation de votre projet et de votre première application</span><span class="sxs-lookup"><span data-stu-id="cd5aa-105">2. Initializing your project and first application</span></span>

## <a name="overview"></a><span data-ttu-id="cd5aa-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="cd5aa-106">Overview</span></span>

<span data-ttu-id="cd5aa-107">Dans cette première leçon, vous allez découvrir certaines fonctionnalités du <a href="https://github.com/microsoft/MixedRealityToolkit-Unity" target="_blank">Mixed Reality Toolkit (MRTK)</a>. Vous verrez également comment démarrer votre première application pour HoloLens 2 et la déployer sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-107">In this first lesson, you'll learn about some of the capabilities the <a href="https://github.com/microsoft/MixedRealityToolkit-Unity" target="_blank">Mixed Reality Toolkit (MRTK)</a> has to offer, start your first application for the HoloLens 2, and deploy it to the device.</span></span>

## <a name="objectives"></a><span data-ttu-id="cd5aa-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="cd5aa-108">Objectives</span></span>

* <span data-ttu-id="cd5aa-109">Configurer Unity pour le développement HoloLens.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-109">Configure Unity for HoloLens development.</span></span>
* <span data-ttu-id="cd5aa-110">Importer les ressources et configurer la scène.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-110">Import assets and set up the scene.</span></span>
* <span data-ttu-id="cd5aa-111">Visualiser le maillage spatial, les maillages de la main et le compteur de fréquence d’images.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-111">Visualization of the spatial mapping mesh, hand meshes, and the framerate counter.</span></span>

## <a name="create-new-unity-project"></a><span data-ttu-id="cd5aa-112">Créer un projet Unity</span><span class="sxs-lookup"><span data-stu-id="cd5aa-112">Create new Unity project</span></span>

1. <span data-ttu-id="cd5aa-113">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-113">Start Unity.</span></span>

2. <span data-ttu-id="cd5aa-114">Sélectionnez **New**.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-114">Select **New**.</span></span>

    ![Leçon 1, section 1, étape 2](images/mrlearning-base-ch1-1-step2.JPG)

3. <span data-ttu-id="cd5aa-116">Entrez un nom de projet (par exemple, « MixedRealityBase »).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-116">Enter a project name (e.g. "MixedRealityBase").</span></span>

    ![Leçon 1, section 1, étape 3](images/mrlearning-base-ch1-1-step3.JPG)

4. <span data-ttu-id="cd5aa-118">Entrez un emplacement auquel enregistrer votre projet.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-118">Enter a location to save your project.</span></span>

    ![Leçon 1, section 1, étape 4](images/mrlearning-base-ch1-1-step4.JPG)

5. <span data-ttu-id="cd5aa-120">Vérifiez que le projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-120">Make sure the project is set to **3D**.</span></span>

    ![Leçon 1, section 1, étape 5](images/mrlearning-base-ch1-1-step5.JPG)

6. <span data-ttu-id="cd5aa-122">Cliquez sur **Create Project**.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-122">Click **Create Project**.</span></span>

    ![Leçon 1, section 1, étape 6](images/mrlearning-base-ch1-1-step6.JPG)

## <a name="configure-the-unity-project-for-windows-mixed-reality"></a><span data-ttu-id="cd5aa-124">Configurer le projet Unity pour Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="cd5aa-124">Configure the Unity project for Windows Mixed Reality</span></span>

1. <span data-ttu-id="cd5aa-125">Ouvrez la fenêtre *Build Settings* (Paramètres de génération) en choisissant **File** > **Build Settings**.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-125">Open the *Build Settings* window by going to **File** > **Build Settings**.</span></span>

    ![Leçon 1, section 2, étape 1](images/mrlearning-base-ch1-2-step1.JPG)

2. <span data-ttu-id="cd5aa-127">Sélectionnez *Universal Windows Platform* (Plateforme Windows universelle), puis cliquez sur le bouton **Switch Platform** (Changer de plateforme).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-127">Select the *Universal Windows Platform* and click the **Switch Platform** button to switch platforms.</span></span> <span data-ttu-id="cd5aa-128">Les applications qui s’exécutent sur HoloLens 2 doivent être compatibles avec la plateforme Windows universelle (UWP).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-128">Applications running on HoloLens 2 are required to be Universal Windows Platform (UWP) compatible.</span></span>

    ![Leçon 1, section 2, étape 2](images/mrlearning-base-ch1-2-step2.JPG)

3. <span data-ttu-id="cd5aa-130">Activez la réalité virtuelle en cliquant sur **Player Settings** (Paramètres du lecteur) dans la fenêtre Build (Générer), puis cochez la case *Virtual Reality Supported* (Prise en charge de la réalité virtuelle), sous XR Settings (Paramètres XR) dans le panneau Inspector (Inspecteur), comme le montre l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-130">Enable virtual reality by clicking the **Player Settings** button in the Build Window, and enable the *Virtual Reality Supported* checkbox under XR Settings from the inspector panel, as shown in the image below.</span></span> <span data-ttu-id="cd5aa-131">Notez que vous devrez peut-être faire glisser la fenêtre *Build Settings* pour voir le panneau Inspector.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-131">Note that you might need to drag the *Build Settings* window out of the way in order to see the inspector panel.</span></span> <span data-ttu-id="cd5aa-132">La case à cocher *Virtual Reality Supported* s’applique également aux casques de réalité mixte et de réalité augmentée, car elle fait référence à l’activation de la vision stéréoscopique (rendu d’images différentes pour chaque œil).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-132">The *Virtual Reality Supported* checkbox also applies to Mixed Reality and Augmented Reality headsets because it refers to the enabling of stereoscopic vision (rendering different images for each eye.)</span></span>

    ![Leçon 1, section 2, étape 3](images/mrlearning-base-ch1-2-step3.JPG)

4. <span data-ttu-id="cd5aa-134">Sous XR Settings, choisissez *Single Pass Instanced* (Instanciation en un seul passage) comme *Stereo Rendering Mode* (Mode de rendu stéréo).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-134">Also under XR Settings, change the *Stereo Rendering Mode* to *Single Pass Instanced*.</span></span> <span data-ttu-id="cd5aa-135">Ce [style de pipeline de rendu](https://docs.unity3d.com/Manual/SinglePassStereoRenderingHoloLens.html) donne généralement de meilleurs résultats avec HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-135">This [rendering pipeline style](https://docs.unity3d.com/Manual/SinglePassStereoRenderingHoloLens.html) is generally most performant for HoloLens 2.</span></span> <span data-ttu-id="cd5aa-136">Si vous souhaitez obtenir d’autres configurations performantes pour votre environnement Unity, suivez [ces instructions](recommended-settings-for-unity.md).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-136">If interested in other performant configurations for your Unity environment, follow [these instructions](recommended-settings-for-unity.md).</span></span>

    ![Leçon 1, section 2, étape 4](images/mrlearning-base-ch1-2-step4.jpg)

5. <span data-ttu-id="cd5aa-138">Dans le même panneau Inspector, sous *Publishing Settings* (Paramètres de publication), dans la section des fonctionnalités, vérifiez que la case *Spatial Perception* (Perception spatiale) est cochée.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-138">From the same inspector panel, ensure that the *Spatial Perception* checkbox in the capabilities section is enabled under *Publishing Settings*.</span></span> <span data-ttu-id="cd5aa-139">La perception spatiale nous permet de visualiser le maillage du mappage spatial sur un appareil de réalité mixte comme HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-139">Spatial Perception allows us to visualize the spatial mapping mesh on a mixed reality device, such as HoloLens 2.</span></span> <span data-ttu-id="cd5aa-140">Les paramètres de publication se trouvent dans le panneau Inspector, au-dessus de XR Settings et sous Other Settings (Autres paramètres).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-140">Publishing Settings are found in the inspector panel, above XR Settings and under Other Settings.</span></span>

    ![Leçon 1, section 2, étape 5](images/mrlearning-base-ch1-2-step5.JPG)

    >[!NOTE]
    ><span data-ttu-id="cd5aa-142">Vous pouvez également activer d’autres fonctionnalités courantes comme *Microphone* (pour les commandes vocales) et *InternetClient* (pour la connexion à des services nécessitant une connexion réseau), même si elles ne sont pas utilisées dans cette section.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-142">While not used in this section, some other common capabilities you might want to enable include the *Microphone* for voice commands, and *InternetClient* for connecting to services requiring a network connection.</span></span>

## <a name="import-the-mixed-reality-toolkit"></a><span data-ttu-id="cd5aa-143">Importer le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="cd5aa-143">Import the Mixed Reality Toolkit</span></span>

1. <span data-ttu-id="cd5aa-144">Téléchargez le [package de base version 2.1.0](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.1.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.1.0.unitypackage) de [Mixed Reality Toolkit](https://github.com/microsoft/MixedRealityToolkit-Unity/releases) pour Unity et enregistrez-le dans un dossier sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-144">Download the [Mixed Reality Toolkit](https://github.com/microsoft/MixedRealityToolkit-Unity/releases) Unity [foundation package version 2.1.0](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.1.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.1.0.unitypackage) and save it to a folder on your PC.</span></span>

2. <span data-ttu-id="cd5aa-145">Importez le package *Mixed Reality Toolkit* que vous avez téléchargé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-145">Import the *Mixed Reality Toolkit* package that you downloaded in the previous step.</span></span> <span data-ttu-id="cd5aa-146">Commencez par cliquer sur **Assets** (Ressources) > **Import** (Importer) > **Custom Package** (Package personnalisé). Ensuite, sélectionnez *Microsoft.MixedReality.Toolkit.Unity.Foundation.2.1.0.unitypackage* et ouvrez-le pour lancer le processus d’importation.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-146">Start by clicking on **Assets** > **Import** > **Custom Package**, select *Microsoft.MixedReality.Toolkit.Unity.Foundation.2.1.0.unitypackage* and open it to begin the importing process.</span></span> <span data-ttu-id="cd5aa-147">Patientez quelques minutes, le temps que le processus d’importation se termine.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-147">Allow a few minutes for the importing process to complete.</span></span>

    ![Leçon 1, section 3, étape 2a](images/mrlearning-base-ch1-3-step2a.JPG)

    ![Leçon 1, section 3, étape 2b](images/mrlearning-base-ch1-3-step2b.JPG)

3. <span data-ttu-id="cd5aa-150">Dans la fenêtre contextuelle suivante, cliquez sur **Import** pour commencer l’importation du package sélectionné dans le projet Unity.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-150">In the next pop-up window, click **Import** to begin importing the selected package into the Unity project.</span></span> <span data-ttu-id="cd5aa-151">Vérifiez que tous les éléments sont cochés, comme illustré dans l’image.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-151">Ensure all items are checked as shown in the image.</span></span>

    ![Leçon 1, section 3, étape 3](images/mrlearning-base-ch1-3-step3.JPG)

    > [!NOTE]
    > <span data-ttu-id="cd5aa-153">Si une boîte de dialogue contextuelle s’affiche pour vous inviter à appliquer les paramètres par défaut de Mixed Reality Toolkit, cliquez sur **Apply** (Appliquer).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-153">If you see a pop-up dialog box asking to apply the Mixed Reality Toolkit default settings, click **Apply**.</span></span> <span data-ttu-id="cd5aa-154">MRTK analyse votre projet à la recherche de paramètres recommandés manquants si vous l’importez pour une installation automatisée.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-154">MRTK analyzes your project for any missing recommended settings when imported for automated setup.</span></span> <span data-ttu-id="cd5aa-155">Selon vos paramètres, la fenêtre contextuelle peut être différente de l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-155">Depending on your settings, the pop-up might look different than the image below.</span></span>

    ![Leçon 1, section 3, étape 4, remarque 1](images/mrlearning-base-ch1-3-step4-note1.JPG)

## <a name="configure-the-mixed-reality-toolkit"></a><span data-ttu-id="cd5aa-157">Configurer le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="cd5aa-157">Configure the Mixed Reality Toolkit</span></span>

1. <span data-ttu-id="cd5aa-158">Ajoutez le *Mixed Reality Toolkit* à votre scène actuelle. Pour cela, sélectionnez **Mixed Reality Toolkit** > **Add to Scene and Configure** (Ajouter à la scène et configurer)</span><span class="sxs-lookup"><span data-stu-id="cd5aa-158">Add the *Mixed Reality Toolkit* to your current scene by selecting **Mixed Reality Toolkit** > **Add to Scene and Configure..**</span></span> <span data-ttu-id="cd5aa-159">à partir de la barre de menus.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-159">from the menu bar.</span></span> <span data-ttu-id="cd5aa-160">Si vous ne voyez pas cet élément de menu après avoir importé le Kit de ressources de réalité mixte, redémarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-160">If you don't see this menu item after importing the mixed reality toolkit, restart Unity.</span></span>

    ![Leçon 1, section 4, étape 1](images/mrlearning-base-ch1-4-step1.JPG)

    > [!NOTE]
    > <span data-ttu-id="cd5aa-162">Une boîte de dialogue contextuelle peut s’afficher pour vous demander de sélectionner un [profil Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Profiles/Profiles.html).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-162">You may see a pop-up dialog box for selecting a [profile for the Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Profiles/Profiles.html).</span></span> <span data-ttu-id="cd5aa-163">Double-cliquez sur le profil nommé *DefaultHoloLens2ConfigurationProfile* pour le choisir.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-163">Choose the profile named *DefaultHoloLens2ConfigurationProfile* by double-clicking it.</span></span>

2. <span data-ttu-id="cd5aa-164">Votre scène comprend de nouveaux éléments et des modifications.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-164">Your scene will have several new items and modifications.</span></span> <span data-ttu-id="cd5aa-165">Enregistrez votre scène sous un autre nom. Pour cela, cliquez sur **File** (Fichier) > **Save As...** (Enregistrer sous) et donnez un nom à votre scène, par exemple *BaseScene*.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-165">Save your scene under a different name by clicking **File** > **Save As...**, and give your scene a name, such as *BaseScene*.</span></span> <span data-ttu-id="cd5aa-166">Dans un souci d’organisation, enregistrez la scène dans le dossier *Scenes* du dossier *Assets* de votre projet.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-166">Keep your scene organized by saving it to the *Scenes* folder in your project’s *Assets* folder.</span></span>

    ![Leçon 1, section 4, étape 2a](images/mrlearning-base-ch1-4-step2a.JPG)

    ![Leçon 1, section 4, étape 2b](images/mrlearning-base-ch1-4-step2b.JPG)

## <a name="build-your-application-to-your-device"></a><span data-ttu-id="cd5aa-169">Générer votre application sur votre appareil</span><span class="sxs-lookup"><span data-stu-id="cd5aa-169">Build your application to your device</span></span>

1. <span data-ttu-id="cd5aa-170">Si vous avez fermé la fenêtre *Build Settings* dans les sections précédentes, rouvrez-la en choisissant **File** > **Build Settings**.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-170">If you closed the *Build Settings* window from the previous sections, open the *Build Settings* window again by going to **File** > **Build Settings**.</span></span>

    ![Leçon 1, section 5, étape 1](images/mrlearning-base-ch1-5-step1.JPG)

2. <span data-ttu-id="cd5aa-172">Vérifiez que la scène que vous venez de créer figure dans la liste *Scenes in Build* (Scènes dans la génération). Pour cela, cliquez sur le bouton **Add Open Scenes** (Ajouter des scènes ouvertes) quand votre scène est ouverte dans Unity.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-172">Ensure the scene you just created is in the *Scenes in Build* list by clicking on the **Add Open Scenes** button while your scene is open in Unity.</span></span>

3. <span data-ttu-id="cd5aa-173">Appuyez sur le bouton **Build** (Générer) pour commencer le processus de génération.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-173">Press the **Build** button to begin the build process.</span></span>

    ![Leçon 1, section 5, étape 3](images/mrlearning-base-ch1-5-step3.JPG)

4. <span data-ttu-id="cd5aa-175">Créez un dossier pour votre application et nommez-le.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-175">Create and name a new folder for your application.</span></span> <span data-ttu-id="cd5aa-176">Dans l’image ci-dessous, un dossier portant le nom App a été créé pour contenir l’application.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-176">In the image below, a folder with the name App was created to contain the application.</span></span> <span data-ttu-id="cd5aa-177">Cliquez sur **Select Folder** (Sélectionner le dossier) pour commencer la génération dans le dossier que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-177">Click **Select Folder** to begin building to the newly created folder.</span></span> <span data-ttu-id="cd5aa-178">Une fois la génération terminée, vous pouvez fermer la fenêtre *Build Settings* dans Unity.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-178">After the build has completed, you can close the *Build Settings* window in Unity.</span></span>

    ![Leçon 1, section 5, étape 4](images/mrlearning-base-ch1-5-step4.JPG)

    >[!IMPORTANT]
    ><span data-ttu-id="cd5aa-180">Si la génération échoue, essayez de renouveler l’opération, éventuellement après avoir redémarré Unity.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-180">If the build fails, try building again or restarting Unity and building again.</span></span> <span data-ttu-id="cd5aa-181">Si vous voyez une erreur du type « Error: CS0246 = The type or namespace name “XX” could not be found (are you missing a using directive or an assembly reference?) » (Erreur : CS0246 = Le type ou le nom de l’espace de noms XX est introuvable [une directive using ou une référence d’assembly est-elle manquante ?]),</span><span class="sxs-lookup"><span data-stu-id="cd5aa-181">If you see an error, such as "Error: CS0246 = The type or namespace name “XX” could not be found (are you missing a using directive or an assembly reference?).</span></span> <span data-ttu-id="cd5aa-182">vous devrez peut-être installer le [SDK Windows 10 (10.0.18362.0)](https://developer.microsoft.com//windows/downloads/windows-10-sdk).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-182">If so, you might need to install [Windows 10 SDK (10.0.18362.0)](https://developer.microsoft.com//windows/downloads/windows-10-sdk)</span></span>

5. <span data-ttu-id="cd5aa-183">Une fois la génération terminée, ouvrez le dossier créé qui contient vos fichiers d’application nouvellement générés.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-183">After the build is completed, open the newly created folder containing your newly built application files.</span></span> <span data-ttu-id="cd5aa-184">Double-cliquez sur la solution *MixedRealityBase.sln* (ou le nom correspondant si vous avez utilisé un autre nom pour votre projet) pour ouvrir le fichier solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-184">Double-click on the *MixedRealityBase.sln* solution, or the corresponding name, if you used an alternative name for your project, to open the solution file in Visual Studio.</span></span>

    >[!NOTE]
    ><span data-ttu-id="cd5aa-185">Veillez à ouvrir le dossier créé (par exemple, le dossier *App* si vous avez suivi les conventions de nommage indiquées aux étapes précédentes), car il existe un fichier .sln portant le même nom en dehors de ce dossier, qui ne doit pas être confondu avec le fichier .sln situé dans le dossier de génération.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-185">Be sure to open the newly created folder (i.e. the *App* folder, if following the naming conventions from the previous steps), as there will be a similarly named .sln file outside of that folder, that is not to be confused with the .sln file inside the build folder.</span></span> <span data-ttu-id="cd5aa-186">La structure de dossiers doit ressembler à celle de l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-186">The folder structure should look similar to the image below.</span></span>
    >
    ><span data-ttu-id="cd5aa-187">Si Visual Studio vous invite à installer de nouveaux composants, prenez un moment pour vous assurer que tous les composants requis sont installés comme spécifié dans la [page « Installer les outils »](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-187">If Visual Studio asks you to install new components, take a moment to ensure that all prerequisite components are installed as specified in [the "Install the Tools" page](install-the-tools.md)</span></span>

    ![Leçon 1, section 5, étape 5](images/mrlearning-base-ch1-5-step5.JPG)

6. <span data-ttu-id="cd5aa-189">Connectez votre HoloLens 2 à votre PC.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-189">Connect your HoloLens 2 into your PC.</span></span> <span data-ttu-id="cd5aa-190">Bien que ces instructions supposent que vous déployez sur un appareil HoloLens 2, vous pouvez choisir de déployer sur l’[émulateur HoloLens 2](using-the-hololens-emulator.md) ou de créer un [package d’application pour effectuer un chargement indépendant](<https://docs.microsoft.com//windows/uwp/packaging/packaging-uwp-apps>).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-190">While these instructions assume you will be deploying to a HoloLens 2 device, you might also choose to deploy to the [HoloLens 2 emulator](using-the-hololens-emulator.md) or choose to create an [app package for sideloading](<https://docs.microsoft.com//windows/uwp/packaging/packaging-uwp-apps>)</span></span>

    >[!IMPORTANT]
    ><span data-ttu-id="cd5aa-191">Avant d’effectuer la génération sur votre appareil, celui-ci doit être en *Mode développeur* et associé à votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-191">Before building to your device, the device must be in *Developer Mode* and paired with your development machine.</span></span> <span data-ttu-id="cd5aa-192">Vous pouvez effectuer ces deux étapes en suivant [ces instructions](using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-192">Both of these steps can be completed by following [these instructions](using-visual-studio.md)</span></span>

7. <span data-ttu-id="cd5aa-193">Configurez Visual Studio pour effectuer la génération sur votre HoloLens 2. Pour cela, sélectionnez la configuration *Release* ou *Master*, l’architecture *ARM* et *Device* comme cible.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-193">Configure Visual Studio for building to your HoloLens 2 by selecting the *Release* or *Master* configuration, the *ARM* architecture, and *Device* as target.</span></span>

    ![Leçon 1, section 5, étape 8](images/mrlearning-base-ch1-5-step7.JPG)

8. <span data-ttu-id="cd5aa-195">L’étape finale consiste à effectuer la génération et le déploiement sur votre appareil. Pour cela, sélectionnez **Déboguer** > **Démarrer sans débogage**.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-195">The final step is to build and deploy to your device by selecting **Debug** > **Start without debugging**.</span></span> <span data-ttu-id="cd5aa-196">Quand vous sélectionnez *Démarrer sans débogage*, l’application démarre immédiatement sur votre appareil si la génération réussit, mais le débogueur attaché et les informations de débogage n’apparaissent pas dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-196">Selecting *Start without Debugging* causes the application to immediately start on your device upon a successful build, but without the debugger attached and information appearing in Visual Studio.</span></span> <span data-ttu-id="cd5aa-197">Cela signifie également que vous pouvez déconnecter le câble USB pendant que votre application s’exécute sur votre appareil HoloLens 2 sans arrêter celle-ci.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-197">This also means that you can disconnect your USB cable while your application is running on your HoloLens 2 without stopping the application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cd5aa-198">Vous pouvez également sélectionner **Générer** > **Déployer la solution** pour effectuer le déploiement sur votre appareil sans que l’application démarre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-198">You might also select **Build** > **Deploy Solution** to deploy to your device without having the application automatically start.</span></span>

    ![Leçon 1, section 5, étape 9](images/mrlearning-base-ch1-5-step8.JPG)

## <a name="congratulations"></a><span data-ttu-id="cd5aa-200">Félicitations</span><span class="sxs-lookup"><span data-stu-id="cd5aa-200">Congratulations</span></span>

<span data-ttu-id="cd5aa-201">Vous venez de déployer votre première application HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-201">You have now deployed your first HoloLens 2 application.</span></span> <span data-ttu-id="cd5aa-202">À mesure que vous vous déplacez, vous devez voir un maillage de mappage spatial couvrant toutes les surfaces qui ont été perçues par HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-202">As you walk around, you should see a spatial mapping mesh covering all the surfaces that have been perceived by the HoloLens 2.</span></span> <span data-ttu-id="cd5aa-203">En outre, vous devez voir des indicateurs sur vos mains et doigts pour le suivi de la main et un compteur de fréquence d’images pour vous tenir informé des performances de l’application.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-203">Additionally, you should see indicators on your hands and fingers for hand tracking and a frame rate counter for keeping an eye on application performance.</span></span> <span data-ttu-id="cd5aa-204">Ce ne sont là que quelques-uns des éléments fondamentaux immédiatement disponibles dans le Kit de ressources de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-204">These are just a few of the foundational pieces, included out of the box, with the Mixed Reality Toolkit.</span></span> <span data-ttu-id="cd5aa-205">Au cours des leçons à venir, vous commencerez à ajouter du contenu et une interactivité à votre scène afin de pouvoir explorer pleinement les fonctionnalités d’HoloLens 2 et de Mixed Reality Toolkit.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-205">In the lessons to come, you will start adding more content and interactivity to your scene so that you can fully explore the capabilities of HoloLens 2 and the Mixed Reality Toolkit.</span></span>

> [!NOTE]
> <span data-ttu-id="cd5aa-206">Dans l’application, vous remarquerez peut-être le profileur visuel.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-206">In the app, you may notice the visual profiler.</span></span> <span data-ttu-id="cd5aa-207">Vous découvrirez comment afficher/masquer le compteur de fréquence d’images à l’aide d’une commande vocale dans la [leçon 5](mrlearning-base-ch5.md).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-207">You will cover how to toggle the frame rate counter using a voice command in [Lesson 5](mrlearning-base-ch5.md).</span></span> <span data-ttu-id="cd5aa-208">Il est généralement recommandé d’afficher le profileur visuel pendant toute la durée du développement pour que vous puissiez voir si des modifications apportées au code impactent les performances.</span><span class="sxs-lookup"><span data-stu-id="cd5aa-208">It is generally recommended to keep the visual profiler visible at all times during development to understand when code changes may have impacted perf.</span></span> <span data-ttu-id="cd5aa-209">L’application HoloLens 2 doit [s’exécuter en continu à 60 images par seconde](understanding-performance-for-mixed-reality.md).</span><span class="sxs-lookup"><span data-stu-id="cd5aa-209">HoloLens 2 application should [continuously run at 60 FPS](understanding-performance-for-mixed-reality.md).</span></span>

[<span data-ttu-id="cd5aa-210">Leçon suivante : 3. Création de l’interface utilisateur et configuration du kit d’outils de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="cd5aa-210">Next Lesson: 3. Creating user interface and configure Mixed Reality Toolkit</span></span>](mrlearning-base-ch2.md)
