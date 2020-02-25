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
# <a name="2-initializing-your-project-and-first-application"></a><span data-ttu-id="37e7c-105">2. Initialisation de votre projet et de votre première application</span><span class="sxs-lookup"><span data-stu-id="37e7c-105">2. Initializing your project and first application</span></span>

## <a name="overview"></a><span data-ttu-id="37e7c-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="37e7c-106">Overview</span></span>

<!-- TODO: Consider expanding to include summary of each tutorial in this tutorial series -->
<span data-ttu-id="37e7c-107">Dans ce premier tutoriel, vous allez découvrir certaines fonctionnalités du <a href="https://github.com/microsoft/MixedRealityToolkit-Unity" target="_blank">Mixed Reality Toolkit (MRTK)</a>. Vous verrez également comment démarrer votre première application pour HoloLens 2 et la déployer sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="37e7c-107">In this first tutorial, you will learn about some of the capabilities the <a href="https://github.com/microsoft/MixedRealityToolkit-Unity" target="_blank">Mixed Reality Toolkit (MRTK)</a> has to offer, start your first application for the HoloLens 2, and deploy it to the device.</span></span>

## <a name="objectives"></a><span data-ttu-id="37e7c-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="37e7c-108">Objectives</span></span>

* <span data-ttu-id="37e7c-109">Configurer Unity pour le développement HoloLens</span><span class="sxs-lookup"><span data-stu-id="37e7c-109">Configure Unity for HoloLens development</span></span>
* <span data-ttu-id="37e7c-110">Importer les ressources et configurer la scène</span><span class="sxs-lookup"><span data-stu-id="37e7c-110">Import assets and set up the scene</span></span>
* <span data-ttu-id="37e7c-111">Visualiser le maillage du mappage spatial, les maillages de la main et le compteur de fréquence d’images</span><span class="sxs-lookup"><span data-stu-id="37e7c-111">Visualization of the spatial mapping mesh, hand meshes, and the framerate counter</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37e7c-112">Prérequis</span><span class="sxs-lookup"><span data-stu-id="37e7c-112">Prerequisites</span></span>

* <span data-ttu-id="37e7c-113">PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="37e7c-113">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="37e7c-114">SDK Windows 10 (10.0.18362.0 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="37e7c-114">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="37e7c-115">Capacité de programmation C# de base</span><span class="sxs-lookup"><span data-stu-id="37e7c-115">Some basic C# programming ability</span></span>
* <span data-ttu-id="37e7c-116">Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)</span><span class="sxs-lookup"><span data-stu-id="37e7c-116">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>
* <span data-ttu-id="37e7c-117"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté</span><span class="sxs-lookup"><span data-stu-id="37e7c-117"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.2.X installed and the Universal Windows Platform Build Support module added</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37e7c-118">La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X.</span><span class="sxs-lookup"><span data-stu-id="37e7c-118">The recommended Unity version for this tutorial series is Unity 2019.2.X.</span></span> <span data-ttu-id="37e7c-119">Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="37e7c-119">This supersedes any Unity version requirements or recommendations stated in the prerequisites linked above.</span></span>

## <a name="create-new-unity-project"></a><span data-ttu-id="37e7c-120">Créer un projet Unity</span><span class="sxs-lookup"><span data-stu-id="37e7c-120">Create new Unity project</span></span>

<span data-ttu-id="37e7c-121">Lancez **Unity Hub**, sélectionnez l’onglet **Projets**, puis cliquez sur la **flèche bas** en regard du bouton **Nouveau** :</span><span class="sxs-lookup"><span data-stu-id="37e7c-121">Launch **Unity Hub**, select the **Projects** tab, and click the **down arrow** next to the **New** button:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section1-step1-1.png)

<span data-ttu-id="37e7c-123">Sélectionnez la version Unity spécifiée dans la section [Prérequis](#prerequisites) ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="37e7c-123">Select the Unity version specified in the [Prerequisites](#prerequisites) section above:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section1-step1-2.png)

<span data-ttu-id="37e7c-125">Dans la fenêtre Créer un projet :</span><span class="sxs-lookup"><span data-stu-id="37e7c-125">In the Create a new project window:</span></span>

* <span data-ttu-id="37e7c-126">Vérifiez que **Modèles** est défini sur **3D**</span><span class="sxs-lookup"><span data-stu-id="37e7c-126">Ensure **Templates** is set to **3D**</span></span>
* <span data-ttu-id="37e7c-127">Entrez un **Nom du projet** approprié, par exemple _Tutoriels MRTK_</span><span class="sxs-lookup"><span data-stu-id="37e7c-127">Enter a suitable **Project Name**, for example, _MRTK Tutorials_</span></span>
* <span data-ttu-id="37e7c-128">Choisissez un **Emplacement** approprié pour stocker votre projet, par exemple _D:\MixedRealityLearning_</span><span class="sxs-lookup"><span data-stu-id="37e7c-128">Choose a suitable **Location** to store your project, for example, _D:\MixedRealityLearning_</span></span>
* <span data-ttu-id="37e7c-129">Cliquez sur le bouton **Créer** pour créer et lancer votre nouveau projet Unity</span><span class="sxs-lookup"><span data-stu-id="37e7c-129">Click the **Create** button to create and launch your new Unity project</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section1-step1-3.png)

> [!CAUTION]
> <span data-ttu-id="37e7c-131">Quand vous utilisez Windows, il existe une limite de 255 caractères pour MAX_PATH.</span><span class="sxs-lookup"><span data-stu-id="37e7c-131">When working on Windows, there is a MAX_PATH limit of 255 characters.</span></span> <span data-ttu-id="37e7c-132">Unity est concerné par ces limites et la compilation risque d’échouer si un chemin de fichier dépasse 255 caractères.</span><span class="sxs-lookup"><span data-stu-id="37e7c-132">Unity is affected by these limits and may fail to compile if any file path is longer than 255 characters.</span></span> <span data-ttu-id="37e7c-133">Par conséquent, il est vivement recommandé de stocker votre projet Unity aussi près que possible de la racine du lecteur.</span><span class="sxs-lookup"><span data-stu-id="37e7c-133">Consequently, it is strongly recommended to store your Unity project as close to the root of the drive as possible.</span></span>

<span data-ttu-id="37e7c-134">Attendez qu’Unity crée le projet :</span><span class="sxs-lookup"><span data-stu-id="37e7c-134">Wait for Unity to create the project:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section1-step1-4.png)

## <a name="configure-the-unity-project-for-windows-mixed-reality"></a><span data-ttu-id="37e7c-136">Configurer le projet Unity pour Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="37e7c-136">Configure the Unity project for Windows Mixed Reality</span></span>

<!-- TODO: Consider adding info about configuring Unity for WMR vs MRTK, or removing WMR section -->

<span data-ttu-id="37e7c-137">Dans cette section, vous allez changer de plateforme de génération, activer la réalité virtuelle et activer la perception spatiale.</span><span class="sxs-lookup"><span data-stu-id="37e7c-137">In this section, you will switch build platform, enable virtual reality, and enable spatial perception.</span></span>

### <a name="1-switch-build-platform"></a><span data-ttu-id="37e7c-138">1. Changer de plateforme de génération</span><span class="sxs-lookup"><span data-stu-id="37e7c-138">1. Switch build platform</span></span>

<span data-ttu-id="37e7c-139">Dans le menu Unity, sélectionnez **Fichier** > **Paramètres de build...** pour ouvrir la fenêtre Paramètres de build :</span><span class="sxs-lookup"><span data-stu-id="37e7c-139">In the Unity menu, select **File** > **Build Settings...** to open the Build Settings window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step1-1.png)

<span data-ttu-id="37e7c-141">Dans la fenêtre Paramètres de build, sélectionnez **Plateforme Windows universelle** , puis cliquez sur le bouton **Switch Platform** (Changer de plateforme) :</span><span class="sxs-lookup"><span data-stu-id="37e7c-141">In the Build Settings window, select **Universal Windows Platform** and click the **Switch Platform** button:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step1-2.png)

<span data-ttu-id="37e7c-143">Attendez qu’Unity termine le changement de plateforme :</span><span class="sxs-lookup"><span data-stu-id="37e7c-143">Wait for Unity to finish switching the platform:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step1-3.png)

<span data-ttu-id="37e7c-145">Quand Unity a terminé le changement de plateforme, cliquez sur l’icône **x** rouge pour fermer la fenêtre Paramètres de build :</span><span class="sxs-lookup"><span data-stu-id="37e7c-145">When Unity has finished switching the platform, click the red **x** icon to close the Build Settings window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step1-4.png)

### <a name="2-enable-virtual-reality"></a><span data-ttu-id="37e7c-147">2. Activer la réalité virtuelle</span><span class="sxs-lookup"><span data-stu-id="37e7c-147">2. Enable virtual reality</span></span>

> [!NOTE]
> <span data-ttu-id="37e7c-148">L’activation de la réalité virtuelle s’applique également aux casques de réalité mixte et de réalité augmentée, car elle fait référence à l’activation de la vision stéréoscopique (rendu d’images différentes pour chaque œil).</span><span class="sxs-lookup"><span data-stu-id="37e7c-148">Enabling virtual reality also applies to mixed reality and augmented reality headsets because it refers to enabling stereoscopic vision, i.e. rendering different images for each eye.</span></span>

<span data-ttu-id="37e7c-149">Dans le menu Unity, sélectionnez **Modifier** > **Paramètres du projet...** pour ouvrir la fenêtre Paramètres du projet :</span><span class="sxs-lookup"><span data-stu-id="37e7c-149">In the Unity menu, select **Edit** > **Project Settings...** to open the Project Settings window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step2-1.png)

<span data-ttu-id="37e7c-151">Dans la fenêtre Paramètres du projet, sélectionnez **Lecteur** > **Paramètres XR** pour développer les paramètres XR :</span><span class="sxs-lookup"><span data-stu-id="37e7c-151">In the Project Settings window, select **Player** > **XR Settings** to expand the XR Settings:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step2-2.png)

<span data-ttu-id="37e7c-153">Dans les paramètres XR, cochez la case **Virtual Reality Supported** (Prise en charge de la réalité virtuelle) pour activer la réalité virtuelle, puis cliquez sur l’icône **+** et sélectionnez **Windows Mixed Reality** pour ajouter le SDK Windows Mixed Reality :</span><span class="sxs-lookup"><span data-stu-id="37e7c-153">In the XR Settings, check the **Virtual Reality Supported** checkbox to enable virtual reality, then click the **+** icon and select **Windows Mixed Reality** to add the Windows Mixed Reality SDK:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step2-3.png)

<span data-ttu-id="37e7c-155">Attendez qu’Unity termine l’ajout du SDK :</span><span class="sxs-lookup"><span data-stu-id="37e7c-155">Wait for Unity to finish adding the SDK:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step2-4.png)

<span data-ttu-id="37e7c-157">Quand Unity a terminé l’ajout du SDK, optimisez les paramètres XR comme suit :</span><span class="sxs-lookup"><span data-stu-id="37e7c-157">When Unity has finished adding the SDK, optimize the XR Settings as follows:</span></span>

* <span data-ttu-id="37e7c-158">Définissez le **format d’intensité**  de Windows Mixed Reality sur une **profondeur de 16 bits**</span><span class="sxs-lookup"><span data-stu-id="37e7c-158">Set Windows Mixed Reality **Depth Format** to **16-bit depth**</span></span>
* <span data-ttu-id="37e7c-159">Cochez la case **Enable Depth Sharing** (Activer le partage de profondeur) de Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="37e7c-159">Check the Windows Mixed Reality **Enable Depth Sharing** checkbox</span></span>
* <span data-ttu-id="37e7c-160">Définissez le **mode de rendu \*** stéréo sur **Single Pass Instanced** (Instanciation en un seul passage)</span><span class="sxs-lookup"><span data-stu-id="37e7c-160">Set Stereo **Rendering Mode\*** to **Single Pass Instanced**</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step2-5.png)

> [!TIP]
> <span data-ttu-id="37e7c-162">Pour en savoir plus sur l’optimisation d’Unity pour Windows Mixed Reality, vous pouvez consulter la documentation [Paramètres recommandés pour Unity](recommended-settings-for-unity.md).</span><span class="sxs-lookup"><span data-stu-id="37e7c-162">To learn more about optimizing Unity for Windows Mixed Reality, you can refer to the [Recommended settings for Unity](recommended-settings-for-unity.md) documentation.</span></span>

### <a name="3-enable-spatial-perception"></a><span data-ttu-id="37e7c-163">3. Activer la perception spatiale</span><span class="sxs-lookup"><span data-stu-id="37e7c-163">3. Enable spatial perception</span></span>

> [!NOTE]
> <span data-ttu-id="37e7c-164">La perception spatiale permet de visualiser le maillage du mappage spatial sur des appareils Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="37e7c-164">Spatial perception allows visualization of the spatial mapping mesh on Windows Mixed Reality devices.</span></span>

<span data-ttu-id="37e7c-165">Dans la fenêtre Paramètres du projet, sélectionnez **Lecteur** > **Paramètres de publication** pour développer les paramètres de publication :</span><span class="sxs-lookup"><span data-stu-id="37e7c-165">In the Project Settings window, select **Player** > **Publishing Settings** to expand the Publishing Settings:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step3-1.png)

<span data-ttu-id="37e7c-167">Dans les paramètres de publication, faites défiler vers le bas jusqu’à la section **Fonctionnalités**, puis cochez la case **SpatialPerception** :</span><span class="sxs-lookup"><span data-stu-id="37e7c-167">In the Publishing Settings, scroll down to the **Capabilities** section and check the **SpatialPerception** checkbox:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section2-step3-2.png)

<!-- TODO: Consider adding info about audio spatializer plugin setting -->

<span data-ttu-id="37e7c-169">Fermez la fenêtre Paramètres du projet.</span><span class="sxs-lookup"><span data-stu-id="37e7c-169">Close the Project Settings window.</span></span>

## <a name="import-textmesh-pro-essential-resources"></a><span data-ttu-id="37e7c-170">Importer les ressources essentielles TextMeshPro</span><span class="sxs-lookup"><span data-stu-id="37e7c-170">Import TextMesh Pro Essential Resources</span></span>

> [!NOTE]
> <span data-ttu-id="37e7c-171">Nous importons ce package, car il est requis par les éléments d’interface utilisateur de Mixed Reality Toolkit.</span><span class="sxs-lookup"><span data-stu-id="37e7c-171">We are importing this package because it is required by Mixed Reality Toolkit's UI elements.</span></span>

<span data-ttu-id="37e7c-172">Dans le menu Unity, sélectionnez **Fenêtre** > **TextMeshPro** > **Import TMP Essential Resources** (Importer les ressources essentielles TMP) :</span><span class="sxs-lookup"><span data-stu-id="37e7c-172">In the Unity menu, select **Window** > **TextMeshPro** > **Import TMP Essential Resources**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section3-step1-1.png)

<span data-ttu-id="37e7c-174">Dans la fenêtre Import Unity Package (Importer un package Unity), cliquez sur le bouton **Tous** pour vous assurer que toutes les ressources sont sélectionnées, puis sur le bouton **Importer** pour importer les ressources :</span><span class="sxs-lookup"><span data-stu-id="37e7c-174">In the Import Unity Package window, click the **All** button to ensure all the assets are selected, then click the **Import** button to import the assets:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section3-step1-2.png)

## <a name="import-the-mixed-reality-toolkit"></a><span data-ttu-id="37e7c-176">Importer le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="37e7c-176">Import the Mixed Reality Toolkit</span></span>

<span data-ttu-id="37e7c-177">Téléchargez le package personnalisé Unity :</span><span class="sxs-lookup"><span data-stu-id="37e7c-177">Download the Unity custom package:</span></span>

* [<span data-ttu-id="37e7c-178">Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage</span><span class="sxs-lookup"><span data-stu-id="37e7c-178">Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.3.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage)

<span data-ttu-id="37e7c-179">Dans le menu Unity, sélectionnez **Ressources** > **Importer un package** > **Custom Package...** (Package personnalisé) pour ouvrir la fenêtre Importer un package... :</span><span class="sxs-lookup"><span data-stu-id="37e7c-179">In the Unity menu, select **Assets** > **Import Package** > **Custom Package...** to open the Import package... window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section4-step1-1.png)

<span data-ttu-id="37e7c-181">Dans la fenêtre Importer un package..., sélectionnez le package **Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage** que vous avez téléchargé, puis cliquez sur le bouton **Ouvrir** :</span><span class="sxs-lookup"><span data-stu-id="37e7c-181">In the Import package... window, select the **Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage** you downloaded and click the **Open** button:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section4-step1-2.png)

<span data-ttu-id="37e7c-183">Dans la fenêtre Import Unity Package (Importer un package Unity), cliquez sur le bouton **Tous** pour vous assurer que toutes les ressources sont sélectionnées, puis sur le bouton **Importer** pour importer les ressources :</span><span class="sxs-lookup"><span data-stu-id="37e7c-183">In the Import Unity Package window, click the **All** button to ensure all the assets are selected, then click the **Import** button to import the assets:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section4-step1-3.png)

## <a name="configure-the-unity-project-for-the-mixed-reality-toolkit"></a><span data-ttu-id="37e7c-185">Configurer le projet Unity pour Mixed Reality Toolkit</span><span class="sxs-lookup"><span data-stu-id="37e7c-185">Configure the Unity project for the Mixed Reality Toolkit</span></span>

<!-- TODO: Consider adding info about configuring Unity for WMR vs MRTK, or removing WMR section -->

<span data-ttu-id="37e7c-186">Une fois le package importé, la fenêtre du configurateur de projet MRTK doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="37e7c-186">After the package has been imported, the MRTK Project Configurator window should appear.</span></span> <span data-ttu-id="37e7c-187">Si ce n’est pas le cas, ouvrez-la en sélectionnant **Mixed Reality Toolkit** > **Outils** > **Configure Unity Project** (Configurer un projet Unity) dans le menu Unity.</span><span class="sxs-lookup"><span data-stu-id="37e7c-187">If it does not, open it by selecting **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project** in the Unity menu.</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section5-step1-1.png)

<span data-ttu-id="37e7c-189">Dans la fenêtre du configurateur de projet MRTK, développez la section **Modify Configurations** (Modifier les configurations), <u>décochez</u> la case **Enable MSBuild for Unity** (Activer MSBuild for Unity), vérifiez que toutes les autres options sont cochées et cliquez sur le bouton **Appliquer** pour appliquer les paramètres :</span><span class="sxs-lookup"><span data-stu-id="37e7c-189">In the MRTK Project Configurator window, expand the **Modify Configurations** section, <u>uncheck</u> the **Enable MSBuild for Unity** checkbox, ensure all other options are checked, and click the **Apply** button to apply the settings:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section5-step1-2.png)

> [!CAUTION]
> <span data-ttu-id="37e7c-191">MSBuild for Unity ne prend peut-être pas en charge tous les SDK que vous utiliserez et peut être difficile à désactiver une fois qu’il a été activé.</span><span class="sxs-lookup"><span data-stu-id="37e7c-191">MSBuild for Unity may not support all SDKs you will be using and can be challenging to disable after it has been enabled.</span></span> <span data-ttu-id="37e7c-192">Par conséquent, il est vivement recommandé de ne pas activer MSBuild for Unity.</span><span class="sxs-lookup"><span data-stu-id="37e7c-192">Consequently, it is strongly recommended to not enable MSBuild for Unity.</span></span>

## <a name="configure-the-mixed-reality-toolkit"></a><span data-ttu-id="37e7c-193">Configurer le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="37e7c-193">Configure the Mixed Reality Toolkit</span></span>
<!-- TODO: Consider renaming to 'Add the Mixed Reality Toolkit to the Unity scene' -->

<span data-ttu-id="37e7c-194">Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Add to Scene and Configure...** (Ajouter à la scène et configurer) pour ajouter Mixed Reality Toolkit à votre scène actuelle :</span><span class="sxs-lookup"><span data-stu-id="37e7c-194">In the Unity menu, select **Mixed Reality Toolkit** > **Add to Scene and Configure...** to add the Mixed Reality Toolkit to your current scene:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section6-step1-1.png)

<span data-ttu-id="37e7c-196">Une fois l’objet MixedRealityToolkit sélectionné dans la fenêtre Hiérarchie, dans la fenêtre de l’inspecteur, vérifiez que le profil de configuration Mixed Reality Toolkit est défini sur **DefaultMixedRealityToolkitConfigurationProfile** :</span><span class="sxs-lookup"><span data-stu-id="37e7c-196">With the MixedRealityToolkit object selected in the Hierarchy window, in the Inspector window, verify the Mixed Reality Toolkit configuration profile is set to **DefaultMixedRealityToolkitConfigurationProfile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section6-step1-2.png)

> [!IMPORTANT]
> <span data-ttu-id="37e7c-198">Normalement, vous allez utiliser DefaultHoloLens2ConfigurationProfile lors du développement pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="37e7c-198">Typically, you will use the DefaultHoloLens2ConfigurationProfile when developing for HoloLens 2.</span></span> <span data-ttu-id="37e7c-199">Toutefois, dans le cadre de ce tutoriel, vous allez utiliser DefaultMixedRealityToolkitConfigurationProfile, puis dans le tutoriel suivant, [Création de l’interface utilisateur et configuration du kit d’outils de réalité mixte](mrlearning-base-ch2.md), vous allez passer à DefaultHoloLens2ConfigurationProfile.</span><span class="sxs-lookup"><span data-stu-id="37e7c-199">However, for the purpose of this tutorial, you will use the DefaultMixedRealityToolkitConfigurationProfile, then in the next tutorial, [Creating user interface and configure Mixed Reality Toolkit](mrlearning-base-ch2.md), you will change to the DefaultHoloLens2ConfigurationProfile.</span></span>

<span data-ttu-id="37e7c-200">Dans le menu Unity, sélectionnez **Fichier** > **Enregistrer sous...** pour ouvrir la fenêtre Save Scene (Enregistrer la scène) :</span><span class="sxs-lookup"><span data-stu-id="37e7c-200">In the Unity menu, select **File** > **Save As...** to open the Save Scene window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section6-step1-3.png)

<span data-ttu-id="37e7c-202">Dans la fenêtre Enregistrer la scène, accédez au dossier **Scènes** de votre projet, donnez à votre scène un nom approprié, par exemple _Démarrage_, puis cliquez sur le bouton **Enregistrer** pour enregistrer la scène :</span><span class="sxs-lookup"><span data-stu-id="37e7c-202">In the Save Scene window, navigate to your project's **Scenes** folder, give your scene a suitable name, for example, _GettingStarted_, and click the **Save** button to save the scene:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section6-step1-4.png)

## <a name="build-your-application-to-your-device"></a><span data-ttu-id="37e7c-204">Générer votre application sur votre appareil</span><span class="sxs-lookup"><span data-stu-id="37e7c-204">Build your application to your device</span></span>

### <a name="1-build-the-unity-project"></a><span data-ttu-id="37e7c-205">1. Générer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="37e7c-205">1. Build the Unity project</span></span>

<span data-ttu-id="37e7c-206">Dans le menu Unity, sélectionnez **Fichier** > **Paramètres de build...** pour ouvrir la fenêtre Paramètres de build.</span><span class="sxs-lookup"><span data-stu-id="37e7c-206">In the Unity menu, select **File** > **Build Settings...** to open the Build Settings window.</span></span>

<span data-ttu-id="37e7c-207">Dans la fenêtre Paramètres de build, cliquez sur le bouton **Add Open Scenes** (Ajouter des scènes ouvertes) pour ajouter votre scène actuelle à la liste **Scenes In Build** (Scènes dans la génération), puis cliquez sur le bouton **Générer** pour ouvrir la fenêtre de génération d’applications de plateforme Windows universelle :</span><span class="sxs-lookup"><span data-stu-id="37e7c-207">In the Build Settings window, click the **Add Open Scenes** button to add your current scene to the **Scenes In Build** list, then click the **Build** button to open the Build Universal Windows Platform window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section7-step1-1.png)

<span data-ttu-id="37e7c-209">Dans la fenêtre de génération d’applications de plateforme Windows universelle, choisissez un emplacement approprié pour stocker votre build, par exemple _D:\MixedRealityLearning\Builds_, créez un dossier et attribuez-lui un nom pertinent, par exemple _GettingStarted_, puis cliquez sur le bouton **Sélectionner un dossier** pour démarrer le processus de génération :</span><span class="sxs-lookup"><span data-stu-id="37e7c-209">In the Build Universal Windows Platform window, choose a suitable location to store your build, for example, _D:\MixedRealityLearning\Builds_, create a new folder and give it a suitable name, for example, _GettingStarted_, and then click the **Select Folder** button to start the build process:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section7-step1-2.png)

<span data-ttu-id="37e7c-211">Attendez qu’Unity termine le processus de génération :</span><span class="sxs-lookup"><span data-stu-id="37e7c-211">Wait for Unity to finish the build process:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section7-step1-3.png)

### <a name="2-build-and-deploy-the-application"></a><span data-ttu-id="37e7c-213">2. Générer et déployer l’application</span><span class="sxs-lookup"><span data-stu-id="37e7c-213">2. Build and deploy the application</span></span>

<span data-ttu-id="37e7c-214">Une fois le processus de génération terminé, Unity invite l’Explorateur de fichiers Windows à ouvrir l’emplacement où vous avez stocké la build.</span><span class="sxs-lookup"><span data-stu-id="37e7c-214">When the build process is completed, Unity will prompt Windows File Explorer to open the location you stored the build.</span></span> <span data-ttu-id="37e7c-215">Naviguez dans le dossier, puis double-cliquez sur le fichier solution pour l’ouvrir dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="37e7c-215">Navigate inside the folder, and double-click the solution file to open it in Visual Studio:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section7-step2-1.png)

> [!NOTE]
> <span data-ttu-id="37e7c-217">Si Visual Studio vous invite à installer de nouveaux composants, prenez un moment pour vous assurer que tous les composants prérequis sont installés comme spécifié dans la documentation [Installer les outils](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="37e7c-217">If Visual Studio asks you to install new components, take a moment to ensure that all prerequisite components are installed as specified in the [Install the Tools](install-the-tools.md) documentation.</span></span>

<span data-ttu-id="37e7c-218">Configurez Visual Studio pour HoloLens 2 en sélectionnant la configuration **Master** ou **Release**, l’architecture **ARM** et **Appareil** comme cible :</span><span class="sxs-lookup"><span data-stu-id="37e7c-218">Configure Visual Studio for HoloLens 2 by selecting the **Master** or **Release** configuration, the **ARM** architecture, and **Device** as target:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section7-step2-2.png)

<span data-ttu-id="37e7c-220">Connectez votre HoloLens 2 à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="37e7c-220">Connect your HoloLens 2 to your computer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37e7c-221">Avant d’effectuer la génération sur votre appareil, celui-ci doit être en mode développeur et associé à votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="37e7c-221">Before building to your device, the device must be in Developer Mode and paired with your development computer.</span></span> <span data-ttu-id="37e7c-222">Vous pouvez effectuer ces deux étapes en suivant [ces instructions](using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="37e7c-222">Both of these steps can be completed by following [these instructions](using-visual-studio.md).</span></span>

<span data-ttu-id="37e7c-223">L’étape finale consiste à effectuer la génération et le déploiement sur votre appareil. Pour cela, sélectionnez **Déboguer** > **Démarrer sans débogage** :</span><span class="sxs-lookup"><span data-stu-id="37e7c-223">The final step is to build and deploy to your device by selecting **Debug** > **Start Without Debugging**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial1-section7-step2-3.png)

<span data-ttu-id="37e7c-225">Bien que ces instructions supposent que vous déployez sur un appareil HoloLens 2, vous pouvez aussi déployer sur l’[émulateur HoloLens 2](using-the-hololens-emulator.md) ou créer un [package d’application pour effectuer un chargement indépendant](<https://docs.microsoft.com//windows/uwp/packaging/packaging-uwp-apps>).</span><span class="sxs-lookup"><span data-stu-id="37e7c-225">While these instructions assume you will be deploying to a HoloLens 2 device, you can also deploy to the [HoloLens 2 emulator](using-the-hololens-emulator.md) or create an [app package for sideloading](<https://docs.microsoft.com//windows/uwp/packaging/packaging-uwp-apps>).</span></span>

<span data-ttu-id="37e7c-226">Quand vous sélectionnez Démarrer sans débogage, l’application démarre immédiatement sur votre appareil si la génération réussit, mais le débogueur n’est pas attaché et les informations n’apparaissent pas dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="37e7c-226">Selecting Start without Debugging causes the application to immediately start on your device upon a successful build, but without the debugger attached and information appearing in Visual Studio.</span></span> <span data-ttu-id="37e7c-227">Cela signifie également que vous pouvez déconnecter le câble USB pendant que votre application s’exécute sur votre appareil HoloLens 2 sans arrêter celle-ci.</span><span class="sxs-lookup"><span data-stu-id="37e7c-227">This also means that you can disconnect your USB cable while your application is running on your HoloLens 2 without stopping the application.</span></span>

<span data-ttu-id="37e7c-228">Pour effectuer le déploiement sur votre appareil sans que l’application ne démarre automatiquement, vous pouvez sélectionner Générer > Déployer la solution.</span><span class="sxs-lookup"><span data-stu-id="37e7c-228">To deploy to your device without having the application start automatically, you can select Build > Deploy Solution.</span></span>

## <a name="congratulations"></a><span data-ttu-id="37e7c-229">Félicitations</span><span class="sxs-lookup"><span data-stu-id="37e7c-229">Congratulations</span></span>

<!-- TODO: Consider cleanup and adding in app screenshots -->
<span data-ttu-id="37e7c-230">Vous venez de déployer votre première application HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="37e7c-230">You have now deployed your first HoloLens 2 application.</span></span> <span data-ttu-id="37e7c-231">À mesure que vous vous déplacez, vous devez voir un maillage de mappage spatial couvrant toutes les surfaces qui ont été perçues par HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="37e7c-231">As you walk around, you should see a spatial mapping mesh covering all the surfaces that have been perceived by the HoloLens 2.</span></span> <span data-ttu-id="37e7c-232">En outre, vous devez voir des indicateurs sur vos mains et doigts pour le suivi de la main et un compteur de fréquence d’images pour vous tenir informé des performances de l’application.</span><span class="sxs-lookup"><span data-stu-id="37e7c-232">Additionally, you should see indicators on your hands and fingers for hand tracking and a frame rate counter for keeping an eye on application performance.</span></span> <span data-ttu-id="37e7c-233">Ce ne sont là que quelques-uns des éléments fondamentaux immédiatement disponibles dans le Kit de ressources de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="37e7c-233">These are just a few of the foundational pieces, included out of the box, with the Mixed Reality Toolkit.</span></span> <span data-ttu-id="37e7c-234">Au cours des tutoriels à venir, vous commencerez à ajouter du contenu et une interactivité à votre scène afin de pouvoir explorer pleinement les fonctionnalités d’HoloLens 2 et de Mixed Reality Toolkit.</span><span class="sxs-lookup"><span data-stu-id="37e7c-234">In the tutorials to come, you will start adding more content and interactivity to your scene so that you can fully explore the capabilities of HoloLens 2 and the Mixed Reality Toolkit.</span></span>

> [!NOTE]
> <span data-ttu-id="37e7c-235">Dans l’application, vous remarquerez peut-être le profileur de diagnostics, dont vous pouvez activer ou désactiver l’affichage à l’aide de la commande de reconnaissance vocale **Toogle Diagnostics** (Activer/désactiver les diagnostics).</span><span class="sxs-lookup"><span data-stu-id="37e7c-235">In the app, you may notice the Diagnostics profiler, you can toggle it's visibility using the speech command **Toogle Diagnostics**.</span></span> <span data-ttu-id="37e7c-236">Toutefois, il est généralement recommandé de laisser le profileur visible à tout moment pendant le développement afin de comprendre quand les modifications apportées à l’application peuvent avoir un impact sur les performances, par exemple l’application HoloLens 2 doit [s’exécuter en continu à 60 images par seconde](understanding-performance-for-mixed-reality.md).</span><span class="sxs-lookup"><span data-stu-id="37e7c-236">However, it is generally recommended to keep the profiler visible at all times during development to understand when changes to the app may have impacted performance, for example, HoloLens 2 application should [continuously run at 60 FPS](understanding-performance-for-mixed-reality.md).</span></span>

[<span data-ttu-id="37e7c-237">Tutoriel suivant : 3. Création de l’interface utilisateur et configuration du kit d’outils de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="37e7c-237">Next Tutorial: 3. Creating user interface and configure Mixed Reality Toolkit</span></span>](mrlearning-base-ch2.md)
