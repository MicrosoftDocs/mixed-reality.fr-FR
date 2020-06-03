---
title: Tutoriels Azure Spatial Anchors - 4. Azure Spatial Anchors pour Android et iOS
description: Suivez ce tutoriel pour découvrir comment implémenter Azure Spatial Anchors au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 05/18/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, cours, hololens, azure, spatial anchors
ms.localizationpriority: high
ms.openlocfilehash: a35f73ae5aee493182f0f4990aa345d990c3f513
ms.sourcegitcommit: e65f1463aec3c040a1cd042e61fc2bd156a42ff8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83867621"
---
# <a name="4-azure-spatial-anchors-for-android-and-ios"></a><span data-ttu-id="997bf-105">4. Azure Spatial Anchors pour Android et iOS</span><span class="sxs-lookup"><span data-stu-id="997bf-105">4. Azure Spatial Anchors for Android and iOS</span></span>

<span data-ttu-id="997bf-106">Dans ce tutoriel, vous allez découvrir comment créer votre projet pour des appareils Android et iOS à l’aide des packages AR Foundation, ARCore XR Plugin et ARKit XR Plugin.</span><span class="sxs-lookup"><span data-stu-id="997bf-106">In this tutorial, you will learn how to build your project to Android and iOS devices using AR Foundation, ARCore XR Plugin, and ARKit XR Plugin.</span></span>

## <a name="objectives"></a><span data-ttu-id="997bf-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="997bf-107">Objectives</span></span>

* <span data-ttu-id="997bf-108">Découvrir comment créer votre projet pour un appareil Android à l’aide des packages Unity AR Foundation et ARCore XR Plugin</span><span class="sxs-lookup"><span data-stu-id="997bf-108">Learn how to build your project to Android device using Unity AR Foundation and ARCore XR Plugin.</span></span>
* <span data-ttu-id="997bf-109">Découvrir comment créer votre projet pour un appareil iOS à l’aide des packages Unity AR Foundation et ARKit XR Plugin</span><span class="sxs-lookup"><span data-stu-id="997bf-109">Learn how to build your project to an iOS device using Unity AR Foundation and ARKit XR Plugin.</span></span>

[!NOTE] <span data-ttu-id="997bf-110">Pour suivre ce tutoriel, veillez d’abord à effectuer les étapes des tutoriels Azure Spatial Anchors -> [Bien démarrer avec Azure Spatial Anchors](mrlearning-asa-ch1.md).</span><span class="sxs-lookup"><span data-stu-id="997bf-110">To complete this tutorial, make sure you have completed Azure Spatial Anchors Tutorials -> [Getting started with Azure Spatial Anchors](mrlearning-asa-ch1.md).</span></span>

## <a name="adding-inbuilt-unity-packages"></a><span data-ttu-id="997bf-111">Ajout de packages Unity intégrés</span><span class="sxs-lookup"><span data-stu-id="997bf-111">Adding inbuilt Unity packages</span></span>

<span data-ttu-id="997bf-112">Dans cette section, vous allez installer les packages intégrés AR Foundation, ARCore XR Plugin et ARKit XR Plugin d’Unity nécessaires à la prise en charge des appareils Android et iOS.</span><span class="sxs-lookup"><span data-stu-id="997bf-112">In this section, you will install Unity's inbuilt AR Foundation, ARCore XR Plugin, and ARKit XR Plugin packages required to support Android and iOS devices.</span></span>

<span data-ttu-id="997bf-113">Veillez à installer les versions listées ci-dessous de ces packages Unity :</span><span class="sxs-lookup"><span data-stu-id="997bf-113">Make sure you install the correct version of these Unity packages as listed below:</span></span>

* <span data-ttu-id="997bf-114">**AR Foundation 2.1.4**</span><span class="sxs-lookup"><span data-stu-id="997bf-114">**AR Foundation 2.1.4**</span></span>
* <span data-ttu-id="997bf-115">**ARCore XR Plugin 2.2.0 Preview 2**</span><span class="sxs-lookup"><span data-stu-id="997bf-115">**ARCore XR plugin 2.2.0 preview 2**</span></span>
* <span data-ttu-id="997bf-116">**ARKit XR Plugin 2.1.1**</span><span class="sxs-lookup"><span data-stu-id="997bf-116">**ARKit XR plugin 2.1.1**</span></span>

[!NOTE] <span data-ttu-id="997bf-117">Si vous développez ce projet pour Android, il est inutile d’installer le package ARKit XR Plugin.</span><span class="sxs-lookup"><span data-stu-id="997bf-117">If you are developing this project for Android, there is no need to install the ARKit XR Plugin package.</span></span> <span data-ttu-id="997bf-118">De même, si vous développez ce projet pour iOS, il est inutile d’installer le package ARCore XR Plugin.</span><span class="sxs-lookup"><span data-stu-id="997bf-118">Similarly, if you are developing this project for iOS, you do not need to install the ARCore XR Plugin.</span></span>

<span data-ttu-id="997bf-119">Dans le menu Unity, sélectionnez **Window** > **Package Manager** :</span><span class="sxs-lookup"><span data-stu-id="997bf-119">In the Unity menu, select **Window** > **Package Manager**:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section1-step1-1.png)

<span data-ttu-id="997bf-121">L’affichage de tous les packages dans la liste peut prendre quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="997bf-121">It might take a few seconds before all packages appear in the list.</span></span> <span data-ttu-id="997bf-122">Pour voir les packages en préversion, cliquez sur l’option Advanced, puis sélectionnez **Show preview packages**.</span><span class="sxs-lookup"><span data-stu-id="997bf-122">Display preview packages by clicking on Advanced option and select "**Show preview packages.**"</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section1-step1-2.png)

<span data-ttu-id="997bf-124">Dans la fenêtre Package Manager, sélectionnez **AR Foundation**. Sélectionnez la version 2.1.4 dans la liste, puis mettez à jour le package en cliquant sur le bouton **Update to 2.1.4** :</span><span class="sxs-lookup"><span data-stu-id="997bf-124">In the Package Manager window, select **AR Foundation**, here you see many version and need to select version 2.1.4 and update the package by clicking the **Update to 2.1.4** button:</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section1-step1-3.png)

<span data-ttu-id="997bf-126">Pour prendre en charge les appareils Android, importez le package ARCore XR Plugin 2.2.0 Preview 2 en suivant le même processus.</span><span class="sxs-lookup"><span data-stu-id="997bf-126">To support Android devices, follow the same process to import ARCore XR Plugin 2.2.0 preview 2.</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section1-step1-4.png)

<span data-ttu-id="997bf-128">Pour prendre en charge les appareils iOS, vous devez importer le package Unity **ARKit XR Plugin 2.1.1** dans Package Manager.</span><span class="sxs-lookup"><span data-stu-id="997bf-128">To support iOS devices, you should import the **ARKit XR plugin 2.1.1** Unity package from the Package Manager.</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section1-step1-5.png)

## <a name="customize-mrtk-to-support-ar-foundation-camera"></a><span data-ttu-id="997bf-130">Personnaliser MRTK pour prendre en charge la caméra AR Foundation</span><span class="sxs-lookup"><span data-stu-id="997bf-130">Customize MRTK to support AR Foundation camera</span></span>

<span data-ttu-id="997bf-131">Pour prendre en charge AR Foundation, vous devez personnaliser les paramètres de MRTK. Sélectionnez MixedRealityToolKit dans la fenêtre Hierarchy, puis cliquez sur le bouton **Clone** dans la fenêtre Inspector sous Mixed Reality ToolKit.</span><span class="sxs-lookup"><span data-stu-id="997bf-131">Customize MRTK settings to support AR Foundation by selecting MixedRealityToolKit in the Hierarchy window and click the **Clone** button in Mixed Reality ToolKit in the Inspector window.</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section2-step1-1.png)

<span data-ttu-id="997bf-133">Quand vous cliquez sur le bouton **Clone**, une fenêtre Clone Profile s’ouvre. Cliquez une nouvelle fois sur le bouton Clone pour cloner DefaultMixedRealityToolkitProfile.</span><span class="sxs-lookup"><span data-stu-id="997bf-133">When you click the **Clone** button, a new Clone Profile window will appear, click on the Clone button again to clone the DefaultMixedRealityToolkitProfile.</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section2-step1-2.png)

<span data-ttu-id="997bf-135">De même, clonez le profil de la caméra dans la fenêtre Inspector, renommez le profil en « UnityARConfigurationProfile », puis cliquez sur le bouton **Clone**.</span><span class="sxs-lookup"><span data-stu-id="997bf-135">Similarly, clone the camera profile in the Inspector window and rename the profile to “UnityARConfigurationProfile” and click on the **Clone** button.</span></span> <span data-ttu-id="997bf-136">Dans la fenêtre Inspector, localisez MixedReality et sélectionnez l’onglet Camera. Ensuite, développez Camera Settings Providers dans la fenêtre Inspector, puis cliquez sur **+Add Camera Setting Provider** > développez **New data provider 1** > sélectionnez **None** comme Type > sélectionnez **Microsoft.MixedReality.Toolkit.Experimental.UnityAR** > sélectionnez **UnityARCameraSettings**.</span><span class="sxs-lookup"><span data-stu-id="997bf-136">In the Inspector window, locate the MixedReality, select the Camera tab Expand the camera setting providers in the inspector window and click on **+Add Camera Setting Provider** > expand **New data provider 1**> select Type **None** >select **Microsoft .MixedReality.Toolkit.Experimental.UnityAR** > Select **UnityARCameraSettings**.</span></span>


![mrlearning-asa](images/mrlearning-asa/tutorial4-section2-step1-3.png)

<span data-ttu-id="997bf-138">L’objet MixedRealityToolKit étant sélectionné dans la fenêtre Hierarchy, passez à la fenêtre Inspector pour attacher les scripts de prise en charge. Pour cela, cliquez sur le bouton **Add Component**, tapez AR Reference Point Manager et sélectionnez le script.</span><span class="sxs-lookup"><span data-stu-id="997bf-138">With the MixedRealityToolKit object selected in the Hierarchy window, in the Inspector window, attach supporting scripts by clicking on the **Add component** button and type in AR reference Point manager and select the script.</span></span>

<span data-ttu-id="997bf-139">L’ajout du script « AR Reference Point Manager » ajoute automatiquement « AR Session Origin » dans la fenêtre Inspector.</span><span class="sxs-lookup"><span data-stu-id="997bf-139">Adding the  "AR Reference Point Manager" script will automatically add "AR session origin" along with it in the Inspector window.</span></span> <span data-ttu-id="997bf-140">Une fois les scripts de prise en charge ajoutés, la fenêtre Inspector doit ressembler à ceci.</span><span class="sxs-lookup"><span data-stu-id="997bf-140">After adding the supporting scripts, the Inspector window should look like this.</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section2-step1-4.png)

## <a name="build-application-to-android-device"></a><span data-ttu-id="997bf-142">Créer une application pour un appareil Android</span><span class="sxs-lookup"><span data-stu-id="997bf-142">Build application to Android device</span></span>

<span data-ttu-id="997bf-143">Pour créer cette application pour votre appareil Android, cliquez sur **File** en haut de la fenêtre, puis sélectionnez **Build Settings**.</span><span class="sxs-lookup"><span data-stu-id="997bf-143">To build this application to your Android device, click on **File** at the top of the window and select **Build Settings.**</span></span> <span data-ttu-id="997bf-144">Dans la fenêtre qui s’ouvre, sélectionnez **Android**, puis cliquez sur **Switch Platform**.</span><span class="sxs-lookup"><span data-stu-id="997bf-144">A new window will appear on the screen, select **Android,** and click on the **Switch Platform**.</span></span> <span data-ttu-id="997bf-145">Le changement de plateforme prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="997bf-145">It will take a few minutes to switch platform.</span></span> <span data-ttu-id="997bf-146">Après avoir basculé vers la plateforme Android, cliquez sur **Add Open Scenes** et vérifiez que votre scène actuelle est la seule sélectionnée dans la liste **Scenes In Build**.</span><span class="sxs-lookup"><span data-stu-id="997bf-146">After switching to the Android platform, click on **Add Open Scenes** and make sure your current scene is the only selected scene in the **Scenes In Build** list.</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section3-step1-1.png)

<span data-ttu-id="997bf-148">Fermez la fenêtre **Build Settings**.</span><span class="sxs-lookup"><span data-stu-id="997bf-148">Close the **Build Settings** window.</span></span> <span data-ttu-id="997bf-149">Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project**, puis cliquez sur **Apply** pour configurer le projet Unity pour la plateforme Android.</span><span class="sxs-lookup"><span data-stu-id="997bf-149">In the Unity menu, select **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project** and click on **Apply** to configure the Unity project for the Android platform.</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section3-step1-2.png)

<span data-ttu-id="997bf-151">Dans le menu Unity, sélectionnez **Edit** > **Project Settings** pour ouvrir la fenêtre Project Settings.</span><span class="sxs-lookup"><span data-stu-id="997bf-151">In the Unity menu, select **Edit** > **Project Settings** to open the Project Settings window.</span></span> <span data-ttu-id="997bf-152">Dans la fenêtre Project Settings, sélectionnez l’onglet **Player**, développez la section Other Settings, sélectionnez **Vulkan**, puis supprimez-le en cliquant sur le symbole « - ».</span><span class="sxs-lookup"><span data-stu-id="997bf-152">In the Project Settings, window selects the **Player** tab, expand the Other Settings section, select **Vulkan,** and remove it by clicking the "-" symbol.</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section3-step1-3.png)

<span data-ttu-id="997bf-154">Fermez la fenêtre Player Settings et rouvrez la fenêtre Build Settings.</span><span class="sxs-lookup"><span data-stu-id="997bf-154">Close the Player Settings window and open the Build Settings window again.</span></span> <span data-ttu-id="997bf-155">Ensuite, à l’aide d’un câble USB, connectez votre appareil Android à votre ordinateur, sélectionnez votre appareil dans la liste déroulante **Build and Run on**, puis cliquez sur **Build And Run**.</span><span class="sxs-lookup"><span data-stu-id="997bf-155">Then, using a USB cable, connect your Android device to your computer and select your device in the **Build and Run on** the dropdown, then click **Build And Run**.</span></span> <span data-ttu-id="997bf-156">Vous êtes alors invité à enregistrer un fichier .apk avec le nom de votre choix.</span><span class="sxs-lookup"><span data-stu-id="997bf-156">You will be asked to save a .apk file, which you can pick any name.</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section3-step1-4.png)

> [!NOTE]
> <span data-ttu-id="997bf-158">Si vous recevez une erreur dans la fenêtre Unity Console relative aux modules Android SDK, NDK et/ou JDK, vous devez ouvrir Unity Hub et installer les modules SDK, NDK et JDK associés pour le module Android Build Support.</span><span class="sxs-lookup"><span data-stu-id="997bf-158">If you get any error in the Unity Console window related to Android SDK, NDK, and or JDK modules, you need to open Unity Hub and install the associated SDK, NDK, and JDK modules for the Android Build Support module.</span></span>

<span data-ttu-id="997bf-159">Une fois le processus de génération terminé, vos applications doivent se charger automatiquement sur votre appareil Android.</span><span class="sxs-lookup"><span data-stu-id="997bf-159">When the build process is complete, your applications should automatically load on your Android device.</span></span>

## <a name="build-application-to-ios-device"></a><span data-ttu-id="997bf-160">Créer une application pour un appareil iOS</span><span class="sxs-lookup"><span data-stu-id="997bf-160">Build application to iOS Device</span></span>

<span data-ttu-id="997bf-161">Pour créer cette application pour votre appareil iOS, cliquez sur **File** en haut de la fenêtre, puis sélectionnez **Build Settings**.</span><span class="sxs-lookup"><span data-stu-id="997bf-161">To build this application to your iOS device, click on **File** at the top of the window and select **Build Settings.**</span></span> <span data-ttu-id="997bf-162">Dans la fenêtre qui s’ouvre, sélectionnez **iOS**, puis cliquez sur **Switch Platform**.</span><span class="sxs-lookup"><span data-stu-id="997bf-162">A new window will appear on the screen, then select **iOS** and click on the **Switch Platform**.</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section4-step1-1.png)

<span data-ttu-id="997bf-164">Fermez la fenêtre **Build Settings**.</span><span class="sxs-lookup"><span data-stu-id="997bf-164">Close the **Build Settings** window.</span></span> <span data-ttu-id="997bf-165">Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project**, puis cliquez sur **Apply** pour configurer le projet Unity pour la plateforme iOS.</span><span class="sxs-lookup"><span data-stu-id="997bf-165">In the Unity menu, select **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project** and click on **Apply** to configure the Unity project for the iOS platform.</span></span>

![mrlearning-asa](images/mrlearning-asa/tutorial4-section4-step1-2.png)

<span data-ttu-id="997bf-167">Pour générer le projet XCode iOS, accédez à Build Settings, puis cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="997bf-167">To build the iOS XCode project, go to Build Settings and, click on **Build**.</span></span>

<span data-ttu-id="997bf-168">Suivez [ce guide](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-ios#export-the-xcode-project) pour découvrir comment déployer ce projet sur votre appareil iOS.</span><span class="sxs-lookup"><span data-stu-id="997bf-168">Follow [this guide](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-ios#export-the-xcode-project) to learn how to deploy this project to your iOS device.</span></span>

## <a name="congratulations"></a><span data-ttu-id="997bf-169">Félicitations</span><span class="sxs-lookup"><span data-stu-id="997bf-169">Congratulations</span></span>

<span data-ttu-id="997bf-170">Dans ce tutoriel, vous avez vu comment créer votre projet pour des appareils Android et iOS.</span><span class="sxs-lookup"><span data-stu-id="997bf-170">In this tutorial, you learned how to build your project for Android and iOS devices.</span></span> <span data-ttu-id="997bf-171">Vous avez également appris à utiliser les packages AR Foundation, ARCore XR Plugin et ARKit XR Plugin pour faire fonctionner votre projet sur des appareils Android et iOS.</span><span class="sxs-lookup"><span data-stu-id="997bf-171">You also learned how to use AR Foundation, ARCore XR Plugin, and ARKit XR Plugin to make your project work for Android and iOS devices.</span></span>