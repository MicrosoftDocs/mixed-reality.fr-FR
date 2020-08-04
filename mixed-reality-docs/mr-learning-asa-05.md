---
title: Tutoriels Azure Spatial Anchors - 5. Azure Spatial Anchors pour Android et iOS
description: Suivez ce cours pour découvrir comment déployer un projet Unity avec Mixed Reality Toolkit et Azure Spatial Anchors sur Android et iOS.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens, android, ios
ms.localizationpriority: high
ms.openlocfilehash: 8c63204948b3e4aa3d25e5b2ca948798726f0838
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376541"
---
# <a name="5-azure-spatial-anchors-for-android-and-ios"></a><span data-ttu-id="19b6c-105">5. Azure Spatial Anchors pour Android et iOS</span><span class="sxs-lookup"><span data-stu-id="19b6c-105">5. Azure Spatial Anchors for Android and iOS</span></span>

<span data-ttu-id="19b6c-106">Dans ce tutoriel, vous allez découvrir comment créer votre projet pour des appareils Android et iOS à l’aide des packages AR Foundation, ARCore XR Plugin et ARKit XR Plugin.</span><span class="sxs-lookup"><span data-stu-id="19b6c-106">In this tutorial, you will learn how to build your project to Android and iOS devices using AR Foundation, ARCore XR Plugin, and ARKit XR Plugin.</span></span>

## <a name="objectives"></a><span data-ttu-id="19b6c-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="19b6c-107">Objectives</span></span>

* <span data-ttu-id="19b6c-108">Apprendre à générer votre projet sur votre appareil Android à l’aide des packages AR Foundation et ARCore XR Plugin de Unity</span><span class="sxs-lookup"><span data-stu-id="19b6c-108">Learn how to build your project to your Android device using Unity's AR Foundation and ARCore XR Plugin</span></span>
* <span data-ttu-id="19b6c-109">Apprendre à générer votre projet sur votre appareil iOS à l’aide des packages AR Foundation et ARKit XR Plugin de Unity</span><span class="sxs-lookup"><span data-stu-id="19b6c-109">Learn how to build your project to your iOS device using Unity's AR Foundation and ARKit XR Plugin</span></span>

## <a name="installing-inbuilt-unity-packages"></a><span data-ttu-id="19b6c-110">Installation de packages Unity intégrés</span><span class="sxs-lookup"><span data-stu-id="19b6c-110">Installing inbuilt Unity packages</span></span>

<span data-ttu-id="19b6c-111">Dans cette section, vous allez mettre à niveau et installer les packages intégrés suivants :</span><span class="sxs-lookup"><span data-stu-id="19b6c-111">In this section, you will upgrade and install the following inbuilt packages:</span></span>

* <span data-ttu-id="19b6c-112">AR Foundation 3.1.3</span><span class="sxs-lookup"><span data-stu-id="19b6c-112">AR Foundation 3.1.3</span></span>
* <span data-ttu-id="19b6c-113">Legacy Input Helpers 2.1.4</span><span class="sxs-lookup"><span data-stu-id="19b6c-113">Legacy Input Helpers 2.1.4</span></span>
* <span data-ttu-id="19b6c-114">ARCore XR Plugin 3.1.3 pour la prise en charge d’Android</span><span class="sxs-lookup"><span data-stu-id="19b6c-114">ARCore XR Plugin 3.1.3 for Android support</span></span>
* <span data-ttu-id="19b6c-115">ARKit XR plugin 3.1.3 pour la prise en charge d’iOS</span><span class="sxs-lookup"><span data-stu-id="19b6c-115">ARKit XR plugin 3.1.3 for iOS support</span></span>

> [!CAUTION]
> <span data-ttu-id="19b6c-116">Toutes les versions ne sont pas compatibles avec MRTK et seules certaines versions fonctionnent ensemble ; veillez donc à installer précisément les versions listées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="19b6c-116">Not all version are compatible with MRTK and only certain version works together, so make sure you install the exact versions listed above.</span></span>

<span data-ttu-id="19b6c-117">Dans le menu Unity, sélectionnez **Window** > **Package Manager** pour ouvrir la fenêtre Package Manager, sélectionnez **AR Foundation** > **3.1.3**, puis cliquez sur le bouton **Update to 3.1.3** pour mettre à jour le package :</span><span class="sxs-lookup"><span data-stu-id="19b6c-117">In the Unity menu, select **Window** > **Package Manager** to open the Package Manager window, then select **AR Foundation** > **3.1.3** and click the **Update to 3.1.3** button to update the package:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section1-step1-1.png)

<span data-ttu-id="19b6c-119">Suivez le même processus pour importer les packages restants en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="19b6c-119">Follow the same process to import the remaining packages as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="19b6c-120">Si vous développez ce projet pour Android, il est inutile d’installer le package ARKit XR Plugin.</span><span class="sxs-lookup"><span data-stu-id="19b6c-120">If you are developing this project for Android, there is no need to install the ARKit XR Plugin package.</span></span> <span data-ttu-id="19b6c-121">De même, si vous développez ce projet pour iOS, il est inutile d’installer le package ARCore XR Plugin.</span><span class="sxs-lookup"><span data-stu-id="19b6c-121">Similarly, if you are developing this project for iOS, you do not need to install the ARCore XR Plugin.</span></span>

## <a name="configure-mrtk-for-ar-foundation-camera"></a><span data-ttu-id="19b6c-122">Configurer MRTK pour l’appareil photo AR Foundation</span><span class="sxs-lookup"><span data-stu-id="19b6c-122">Configure MRTK for AR Foundation Camera</span></span>

<span data-ttu-id="19b6c-123">Dans cette section, vous allez découvrir comment configurer MRTK pour le déploiement sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="19b6c-123">In this section, you will learn how to configure MRTK for deploying to a mobile device.</span></span>

<span data-ttu-id="19b6c-124">Dans la fenêtre de hiérarchie, sélectionnez l’objet **MixedRealityToolkit**.</span><span class="sxs-lookup"><span data-stu-id="19b6c-124">In the Hierarchy window, select the **MixedRealityToolkit** object.</span></span> <span data-ttu-id="19b6c-125">Ensuite, dans la fenêtre de l’inspecteur, sélectionnez l’onglet **Camera**, clonez le profil de la caméra et attribuez-lui un nom pertinent, par exemple **AzureSpatialAnchors_ARCameraProfile** :</span><span class="sxs-lookup"><span data-stu-id="19b6c-125">Then in the Inspector window, select the **Camera** tab, clone the camera profile, and give it a suitable name, for example, **AzureSpatialAnchors_ARCameraProfile**:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section2-step1-1.png)

> [!TIP]
> <span data-ttu-id="19b6c-127">Pour vous rappeler comment cloner des profils MRTK, vous pouvez consulter les instructions fournies dans [Configuration des profils Mixed Reality Toolkit](mr-learning-base-03.md).</span><span class="sxs-lookup"><span data-stu-id="19b6c-127">For a reminder on how to clone MRTK profiles, you can refer to the [Configuring the Mixed Reality Toolkit profiles](mr-learning-base-03.md) instructions.</span></span>

<span data-ttu-id="19b6c-128">Avec l’onglet **Camera** toujours sélectionné dans la fenêtre de l’inspecteur, développez **Camera Setting Providers** (Fournisseurs de paramètres d’appareil photo), cliquez sur le bouton **+ Add Camera Setting Provider** (Ajouter un fournisseur de paramètres d’appareil photo), puis développez le **New data provider 1** qui vient d’être ajouté :</span><span class="sxs-lookup"><span data-stu-id="19b6c-128">With the **Camera** tab still selected in the Inspector window, expand the **Camera Setting Providers** and click the **+ Add Camera Setting Provider** button, then expand the newly added **New data provider 1**:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section2-step1-2.png)

<span data-ttu-id="19b6c-130">À l’aide de la liste déroulante **Type**, sélectionnez le type **Microsoft.MixedReality.Toolkit.Experimental.UnityAR** > **UnityARCameraSettings** :</span><span class="sxs-lookup"><span data-stu-id="19b6c-130">Using the **Type** dropdown, change the type to **Microsoft.MixedReality.Toolkit.Experimental.UnityAR** > **UnityARCameraSettings**:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section2-step1-3.png)

<span data-ttu-id="19b6c-132">Avec l’objet **MixedRealityToolkit** toujours sélectionné dans la fenêtre de hiérarchie, utilisez le bouton **Add Component** dans la fenêtre de l’inspecteur pour ajouter les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="19b6c-132">With the **MixedRealityToolkit** object still selected in the Hierarchy window, use the **Add Component** button in the Inspector window to add the following components:</span></span>

* <span data-ttu-id="19b6c-133">AR Anchor Manager (Script)</span><span class="sxs-lookup"><span data-stu-id="19b6c-133">AR Anchor Manager (Script)</span></span>
* <span data-ttu-id="19b6c-134">DisableDiagnosticsSystem (Script)</span><span class="sxs-lookup"><span data-stu-id="19b6c-134">DisableDiagnosticsSystem (Script)</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section2-step1-4.png)

> [!NOTE]
> <span data-ttu-id="19b6c-136">Lorsque vous ajoutez le composant AR Reference Point Manager (Script), le composant AR Session Origin (Script) est ajouté automatiquement, car il est demandé par le composant AR Reference Point Manager (Script).</span><span class="sxs-lookup"><span data-stu-id="19b6c-136">When you add the AR Reference Point Manager (Script) component, the AR Session Origin (Script) component is automatically added because it is required by the AR Reference Point Manager (Script) component.</span></span>

## <a name="building-your-application-to-your-android-device"></a><span data-ttu-id="19b6c-137">Génération de votre application sur votre appareil Android</span><span class="sxs-lookup"><span data-stu-id="19b6c-137">Building your application to your Android device</span></span>

<span data-ttu-id="19b6c-138">Dans cette section, vous allez découvrir comment configurer votre projet pour le générer et le déployer sur un appareil Android.</span><span class="sxs-lookup"><span data-stu-id="19b6c-138">In this section, you will learn how to configure your project to build and deploy it to an Android device.</span></span>

<span data-ttu-id="19b6c-139">Dans le menu Unity, sélectionnez **File** > **Build Settings...** pour ouvrir la fenêtre Build Settings, puis basculez vers la plateforme Android :</span><span class="sxs-lookup"><span data-stu-id="19b6c-139">In the Unity menu, select **File** > **Build Settings...** to open the Build Settings window and then switch the platform to Android:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section3-step1-1.png)

> [!TIP]
> <span data-ttu-id="19b6c-141">Pour vous rappeler comment changer de plateforme de génération, consultez les instructions fournies dans [Changement de la plateforme de génération](mr-learning-base-02.md#switching-the-build-platform).</span><span class="sxs-lookup"><span data-stu-id="19b6c-141">For a reminder on how to switch build platform, you can refer to the [Switching the build platform](mr-learning-base-02.md#switching-the-build-platform) instructions.</span></span>

<span data-ttu-id="19b6c-142">Fermez la fenêtre Build Settings.</span><span class="sxs-lookup"><span data-stu-id="19b6c-142">Close the Build Settings window.</span></span>

<span data-ttu-id="19b6c-143">Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project** pour ouvrir la fenêtre **MRTK Project Configurator**, vérifiez que toutes les options sont sélectionnées, puis cliquez sur le bouton **Apply** pour appliquer les paramètres :</span><span class="sxs-lookup"><span data-stu-id="19b6c-143">In the Unity menu, select **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project** to open the **MRTK Project Configurator** window, ensure all options are selected, then click the **Apply** button to apply the settings:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section3-step1-2.png)

<span data-ttu-id="19b6c-145">Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings, recherchez la section **Player** >  **Other Settings**, sélectionnez **Vulkan** et supprimez-le en cliquant sur le symbole **« - »**  :</span><span class="sxs-lookup"><span data-stu-id="19b6c-145">In the Unity menu, select **Edit** > **Project Settings...** to open the Player Settings window, then locate the **Player** >  **Other Settings** section, select **Vulkan** and remove it by clicking the **"-"** symbol:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section3-step1-3.png)

<span data-ttu-id="19b6c-147">Fermez la fenêtre Player Settings et rouvrez la fenêtre Build Settings.</span><span class="sxs-lookup"><span data-stu-id="19b6c-147">Close the Player Settings window and open the Build Settings window again.</span></span>

<span data-ttu-id="19b6c-148">Dans la fenêtre Build Settings, cliquez sur le bouton **Add Open Scenes** (Ajouter des scènes ouvertes) pour ajouter votre scène actuelle à la liste des scènes de la build (**Scenes In Build**).</span><span class="sxs-lookup"><span data-stu-id="19b6c-148">In the Build Settings window, click the **Add Open Scenes** button to add your current scene to the **Scenes In Build** list.</span></span> <span data-ttu-id="19b6c-149">Ensuite, utilisez un câble USB pour connecter votre appareil Android à votre ordinateur et sélectionnez-le dans la liste déroulante **Run Device** :</span><span class="sxs-lookup"><span data-stu-id="19b6c-149">Then, use a USB cable, connect your Android device to your computer and select it from the **Run Device** dropdown:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section3-step1-4.png)

>[!NOTE]
> <span data-ttu-id="19b6c-151">Si votre appareil n’apparaît pas dans la liste déroulante Run Device, vous devrez peut-être appuyer sur le bouton Refresh à côté de la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="19b6c-151">If your device does not appear in the Run Device dropdown, you might need to press the Refresh button next to the dropdown.</span></span>

<span data-ttu-id="19b6c-152">Dans la fenêtre Build Settings, cliquez sur le bouton **Build And Run** (Générer et exécuter) pour ouvrir la fenêtre Build Android.</span><span class="sxs-lookup"><span data-stu-id="19b6c-152">In the Build Settings window, click the **Build And Run** button to open the Build Android window.</span></span>

<span data-ttu-id="19b6c-153">Choisissez un emplacement approprié où stocker votre build, par exemple _D:\MixedRealityLearning\Builds_, attribuez un nom pertinent à l’apk, par exemple _MRTKTutorials-AzureSpatialAnchors_, puis cliquez sur le bouton **Save** pour démarrer le processus de génération :</span><span class="sxs-lookup"><span data-stu-id="19b6c-153">Choose a suitable location to store your build, for example, _D:\MixedRealityLearning\Builds_, then give the apk a suitable name, for example, _MRTKTutorials-AzureSpatialAnchors_, and click the **Save** button to start the build process:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section3-step1-5.png)

> [!NOTE]
<span data-ttu-id="19b6c-155">Si vous recevez une erreur dans la fenêtre Unity Console relative aux modules Android SDK, NDK ou JDK, vous devez ouvrir Unity Hub et installer les modules Android Build Support associés.</span><span class="sxs-lookup"><span data-stu-id="19b6c-155">If you get any error in the Unity Console window related to Android SDK, NDK, or JDK modules, you need to open Unity Hub and install the associated Android Build Support modules.</span></span>

<span data-ttu-id="19b6c-156">Une fois le processus de génération terminé, vos applications doivent se charger automatiquement sur votre appareil Android.</span><span class="sxs-lookup"><span data-stu-id="19b6c-156">When the build process is complete, your apps should automatically load on your Android device.</span></span>

## <a name="building-your-application-to-your-ios-device"></a><span data-ttu-id="19b6c-157">Génération de votre application sur votre appareil iOS</span><span class="sxs-lookup"><span data-stu-id="19b6c-157">Building your application to your iOS device</span></span>

<span data-ttu-id="19b6c-158">Dans cette section, vous allez découvrir comment configurer votre projet pour le générer et le déployer sur votre appareil iOS.</span><span class="sxs-lookup"><span data-stu-id="19b6c-158">In this section, you will learn how to configure your project, to build and deploy it to your iOS device.</span></span>

<span data-ttu-id="19b6c-159">Dans le menu Unity, sélectionnez **File** > **Build Settings...** pour ouvrir la fenêtre Build Settings et basculez vers la plateforme iOS :</span><span class="sxs-lookup"><span data-stu-id="19b6c-159">In the Unity menu, select **File** > **Build Settings...** to open the Build Settings window and switch platform to iOS:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section4-step1-1.png)

> [!TIP]
> <span data-ttu-id="19b6c-161">Pour vous rappeler comment changer de plateforme de génération, consultez les instructions fournies dans [Changement de la plateforme de génération](mr-learning-base-02.md#switching-the-build-platform).</span><span class="sxs-lookup"><span data-stu-id="19b6c-161">For a reminder on how to switch build platform, you can refer to the [Switching the build platform](mr-learning-base-02.md#switching-the-build-platform) instructions.</span></span>

<span data-ttu-id="19b6c-162">Fermez la fenêtre Build Settings.</span><span class="sxs-lookup"><span data-stu-id="19b6c-162">Close the Build Settings window.</span></span>

<span data-ttu-id="19b6c-163">Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project** pour ouvrir la fenêtre **MRTK Project Configurator**, vérifiez que toutes les options sont sélectionnées, puis cliquez sur le bouton **Apply** pour appliquer les paramètres :</span><span class="sxs-lookup"><span data-stu-id="19b6c-163">In the Unity menu, select **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project** to open the **MRTK Project Configurator** window, ensure all options are selected, then click the **Apply** button to apply the settings:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section4-step1-2.png)

<span data-ttu-id="19b6c-165">Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings, recherchez la section **Player** >  **Other Settings**, et décochez la case **Strip Engine Code** (Supprimer le code du moteur) :</span><span class="sxs-lookup"><span data-stu-id="19b6c-165">In the Unity menu, select **Edit** > **Project Settings...** to open the Player Settings window, then locate the **Player** >  **Other Settings** section, uncheck the **Strip Engine Code** checkbox to disable it:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section4-step1-3.png)

<span data-ttu-id="19b6c-167">Fermez la fenêtre Player Settings et rouvrez la fenêtre **Build Settings**.</span><span class="sxs-lookup"><span data-stu-id="19b6c-167">Close the Player Settings window and open the **Build Settings** window again.</span></span>

<span data-ttu-id="19b6c-168">Dans la fenêtre Build Settings, cliquez sur le bouton **Add Open Scenes** (Ajouter des scènes ouvertes) pour ajouter votre scène actuelle à la liste des scènes de la build (**Scenes In Build**) :</span><span class="sxs-lookup"><span data-stu-id="19b6c-168">In the Build Settings window, click the **Add Open Scenes** button to add your current scene to the **Scenes In Build** list:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section4-step1-4.png)

<span data-ttu-id="19b6c-170">Dans la fenêtre Build Settings, cliquez sur le bouton **Build** pour ouvrir la fenêtre Build iOS.</span><span class="sxs-lookup"><span data-stu-id="19b6c-170">In the Build Settings window, click the **Build** button to open the Build iOS window.</span></span>

<span data-ttu-id="19b6c-171">Choisissez un emplacement approprié où stocker votre projet Xcode, par exemple _D:\MixedRealityLearning\Builds_, créez un dossier et attribuez-lui un nom pertinent, par exemple _MRTKTutorials-AzureSpatialAnchors_, puis cliquez sur le bouton **Select Folder** pour démarrer le processus de génération :</span><span class="sxs-lookup"><span data-stu-id="19b6c-171">Choose a suitable location to store your Xcode project, for example, _D:\MixedRealityLearning\Builds_, create a new folder and give it a suitable name, for example, _MRTKTutorials-AzureSpatialAnchors_, and then click the **Select Folder** button to start the build process:</span></span>

![mr-learning-asa](images/mr-learning-asa/asa-05-section4-step1-5.png)

<span data-ttu-id="19b6c-173">Une fois le processus de génération terminé, suivez les instructions fournies dans [Exporter le projet Xcode](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-ios#export-the-xcode-project) pour découvrir comment déployer votre projet Xcode sur votre appareil iOS.</span><span class="sxs-lookup"><span data-stu-id="19b6c-173">When the build process is complete, follow the [Export the Xcode project](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-ios#export-the-xcode-project) instructions to learn to deploy your Xcode project to your iOS device.</span></span>

## <a name="congratulations"></a><span data-ttu-id="19b6c-174">Félicitations</span><span class="sxs-lookup"><span data-stu-id="19b6c-174">Congratulations</span></span>

<span data-ttu-id="19b6c-175">Dans ce tutoriel, vous avez appris à générer votre projet pour des appareils Android et iOS à l’aide des packages AR Foundation, ARCore XR Plugin et ARKit XR Plugin.</span><span class="sxs-lookup"><span data-stu-id="19b6c-175">In this tutorial, you learned how to build your project to Android and iOS devices using AR Foundation, ARCore XR Plugin, and ARKit XR Plugin.</span></span>
