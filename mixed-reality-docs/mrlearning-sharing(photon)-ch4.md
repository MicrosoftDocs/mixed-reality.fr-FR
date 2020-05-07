---
title: Tutoriels sur les fonctionnalités multi-utilisateurs - 5. Intégration d’Azure Spatial Anchors dans une expérience partagée
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: c27ed7327cfe0a61f2b63e309348bdea1a535ea1
ms.sourcegitcommit: 92ff5478a5c55b4e2c5cc2f44f1588702f4ec5d1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82604970"
---
# <a name="4-integrating-azure-spatial-anchors-into-a-shared-experience"></a><span data-ttu-id="9fc4a-105">4. Intégration d’Azure Spatial Anchors dans une expérience partagée</span><span class="sxs-lookup"><span data-stu-id="9fc4a-105">4. Integrating Azure Spatial Anchors into a shared experience</span></span>

<span data-ttu-id="9fc4a-106">Dans ce tutoriel, vous allez apprendre à intégrer Azure Spatial Anchors (ASA) à l’expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-106">In this tutorial, you will learn how to integrate Azure Spatial Anchors (ASA) into the shared experience.</span></span> <span data-ttu-id="9fc4a-107">ASA permet à plusieurs appareils d’avoir une référence commune au monde physique pour que les utilisateurs se voient à leur emplacement physique réel et voient l’expérience partagée au même endroit.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-107">ASA allows multiple devices to have a common reference to the physical world so that the users see each other in their actual physical location and see the shared experience in the same place.</span></span>

## <a name="objectives"></a><span data-ttu-id="9fc4a-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="9fc4a-108">Objectives</span></span>

* <span data-ttu-id="9fc4a-109">Intégrer ASA à une expérience partagée pour l’alignement de plusieurs appareils</span><span class="sxs-lookup"><span data-stu-id="9fc4a-109">Integrate ASA into a shared experience for multi-device alignment</span></span>
* <span data-ttu-id="9fc4a-110">Découvrir les principes de base du fonctionnement d’ASA dans le contexte d’une expérience partagée locale</span><span class="sxs-lookup"><span data-stu-id="9fc4a-110">Learn the fundamentals of how ASA works in the context of a local shared experience</span></span>

## <a name="preparing-the-scene"></a><span data-ttu-id="9fc4a-111">Préparation de la scène</span><span class="sxs-lookup"><span data-stu-id="9fc4a-111">Preparing the scene</span></span>

<span data-ttu-id="9fc4a-112">Dans la fenêtre Hierarchy, développez l’objet **SharedPlayground**, puis l’objet **TableAnchor** pour exposer ses objets enfants :</span><span class="sxs-lookup"><span data-stu-id="9fc4a-112">In the Hierarchy window, expand the **SharedPlayground** object, then expand the **TableAnchor** object to expose its child objects:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section1-step1-1.png)

<span data-ttu-id="9fc4a-114">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs**, puis faites glisser le préfabriqué **Buttons** sur l’objet **TableAnchor** dans la fenêtre Hierarchy pour l’ajouter à votre scène en tant qu’enfant de l’objet TableAnchor :</span><span class="sxs-lookup"><span data-stu-id="9fc4a-114">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs** folder and drag the **Buttons** prefab on top of the **TableAnchor** child object in the Hierarchy window to add it to your scene as a child of the TableAnchor object:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section1-step1-2.png)

## <a name="configuring-the-buttons-to-operate-the-scene"></a><span data-ttu-id="9fc4a-116">Configuration des boutons pour faire fonctionner la scène</span><span class="sxs-lookup"><span data-stu-id="9fc4a-116">Configuring the buttons to operate the scene</span></span>

<span data-ttu-id="9fc4a-117">Dans cette section, vous allez configurer une série d’événements de bouton qui illustrent les principes de base d’Azure Spatial Anchors pour obtenir un alignement spatial dans une expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-117">In this section, you will configure a series of button events that demonstrate the fundamentals of how Azure Spatial Anchors can be used to achieve spatial alignment in a shared experience.</span></span>

<span data-ttu-id="9fc4a-118">Dans la fenêtre Hierarchy, développez l’objet **Button** et sélectionnez le premier bouton enfant nommé **StartAzureSession** :</span><span class="sxs-lookup"><span data-stu-id="9fc4a-118">In the Hierarchy window, expand the **Button** object and select the first child button object named **StartAzureSession**:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section2-step1-1.png)

<span data-ttu-id="9fc4a-120">Dans la fenêtre Inspector, localisez le composant **Interactable (Script)** et configurez l’événement **OnClick ()** comme suit :</span><span class="sxs-lookup"><span data-stu-id="9fc4a-120">In the Inspector window, locate the **Interactable (Script)** component and configure the **OnClick ()** event as follows:</span></span>

* <span data-ttu-id="9fc4a-121">Affectez à **None (Object)** l’objet **TableAnchor**.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-121">To **None (Object)** field, assign the **TableAnchor** object</span></span>
* <span data-ttu-id="9fc4a-122">Dans la liste déroulante **No Function**, sélectionnez la fonction **AnchorModuleScript** > **StartAzureSession ()** .</span><span class="sxs-lookup"><span data-stu-id="9fc4a-122">From **No Function** dropdown, select the **AnchorModuleScript** > **StartAzureSession ()** function</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section2-step1-2.png)

<span data-ttu-id="9fc4a-124">Dans la fenêtre Hierarchy, sélectionnez le deuxième objet bouton enfant nommé **CreateAzureAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Interactable (Script)** et configurez l’événement **OnClick ()** comme suit :</span><span class="sxs-lookup"><span data-stu-id="9fc4a-124">In the Hierarchy window, select the second child button object named **CreateAzureAnchor**, then in the Inspector window, locate the **Interactable (Script)** component and configure the **OnClick ()** event as follows:</span></span>

* <span data-ttu-id="9fc4a-125">Affectez au champ **None (Object)** l’objet **TableAnchor**.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-125">To **None (Object)** field, assign the **TableAnchor** object</span></span>
* <span data-ttu-id="9fc4a-126">Dans la liste déroulante **No Function**, sélectionnez la fonction **AnchorModuleScript** > **CreateAzureAnchor ()** .</span><span class="sxs-lookup"><span data-stu-id="9fc4a-126">From **No Function** dropdown, select the **AnchorModuleScript** > **CreateAzureAnchor ()** function</span></span>
* <span data-ttu-id="9fc4a-127">Affectez au nouveau champ **None (Game Object)** qui apparaît l’objet **TableAnchor**.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-127">To the new **None (Game Object)** field that appears, assign the **TableAnchor** object</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section2-step1-3.png)

<span data-ttu-id="9fc4a-129">Dans la fenêtre Hierarchy, sélectionnez le troisième objet bouton enfant nommé **ShareAzureAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Interactable (Script)** et configurez l’événement **OnClick ()** comme suit :</span><span class="sxs-lookup"><span data-stu-id="9fc4a-129">In the Hierarchy window, select the third child button object named **ShareAzureAnchor**, then in the Inspector window, locate the **Interactable (Script)** component and configure the **OnClick ()** event as follows:</span></span>

* <span data-ttu-id="9fc4a-130">Affectez au champ **None (Object)** l’objet **TableAnchor**.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-130">To **None (Object)** field, assign the **TableAnchor** object</span></span>
* <span data-ttu-id="9fc4a-131">Dans la liste déroulante **No Function**, sélectionnez la fonction **SharingModuleScript** > **ShareAzureAnchor ()** .</span><span class="sxs-lookup"><span data-stu-id="9fc4a-131">From **No Function** dropdown, select the **SharingModuleScript** > **ShareAzureAnchor ()** function</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section2-step1-4.png)

<span data-ttu-id="9fc4a-133">Dans la fenêtre Hierarchy, sélectionnez le quatrième objet bouton enfant nommé **GetAzureAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Interactable (Script)** et configurez l’événement **OnClick ()** comme suit :</span><span class="sxs-lookup"><span data-stu-id="9fc4a-133">In the Hierarchy window, select the forth child button object named **GetAzureAnchor**, then in the Inspector window, locate the **Interactable (Script)** component and configure the **OnClick ()** event as follows:</span></span>

* <span data-ttu-id="9fc4a-134">Affectez au champ **None (Object)** l’objet **TableAnchor**.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-134">To **None (Object)** field, assign the **TableAnchor** object</span></span>
* <span data-ttu-id="9fc4a-135">Dans la liste déroulante **No Function**, sélectionnez la fonction **SharingModuleScript** > **GetAzureAnchor ()** .</span><span class="sxs-lookup"><span data-stu-id="9fc4a-135">From **No Function** dropdown, select the **SharingModuleScript** > **GetAzureAnchor ()** function</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section2-step1-5.png)

## <a name="connecting-the-scene-to-the-azure-resource"></a><span data-ttu-id="9fc4a-137">Connexion de la scène à la ressource Azure</span><span class="sxs-lookup"><span data-stu-id="9fc4a-137">Connecting the scene to the Azure resource</span></span>

<span data-ttu-id="9fc4a-138">Dans la fenêtre Hierarchy, développez l’objet **SharedPlayground**, puis sélectionnez l’objet **TableAnchor**.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-138">In the Hierarchy window, expand the **SharedPlayground** object and select the **TableAnchor** object.</span></span> <span data-ttu-id="9fc4a-139">Ensuite, dans la fenêtre Inspector, localisez le composant **Spatial Anchor Manager (Script)** et configurez la section **Credentials** avec les informations d’identification du compte Azure Spatial Anchors créé dans le cadre des [prérequis](mrlearning-sharing(photon)-ch1.md#prerequisites) pour cette série de tutoriels :</span><span class="sxs-lookup"><span data-stu-id="9fc4a-139">Then in the Inspector window, locate the **Spatial Anchor Manager (Script)** component and configure the **Credentials** section with the credentials from the Azure Spatial Anchors account created as part of the [Prerequisites](mrlearning-sharing(photon)-ch1.md#prerequisites) for this tutorial series:</span></span>

* <span data-ttu-id="9fc4a-140">Dans le champ **Spatial Anchors Account ID**, collez la valeur **Account ID** de votre compte Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-140">In the **Spatial Anchors Account ID** field, paste the **Account ID** from your Azure Spatial Anchors account</span></span>
* <span data-ttu-id="9fc4a-141">Dans le champ **Spatial Anchors Account Key**, collez la valeur **Access Key** (primaire ou secondaire) de votre compte Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-141">In the **Spatial Anchors Account Key** field, paste the primary or secondary **Access Key** from your Azure Spatial Anchors account</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section3-step1-1.png)

<span data-ttu-id="9fc4a-143">L’objet **TableAnchor** étant toujours sélectionné, vérifiez que tous les composants de script sont activés dans la fenêtre Inspector :</span><span class="sxs-lookup"><span data-stu-id="9fc4a-143">With the **TableAnchor** object still selected, in the Inspector window, make sure all the script components are enabled:</span></span>

* <span data-ttu-id="9fc4a-144">Cochez la case en regard du composant **Spatial Anchor Manager (Script)** pour l’activer.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-144">Check the checkbox next to the **Spatial Anchor Manager (Script)** components to enable it</span></span>
* <span data-ttu-id="9fc4a-145">Cochez la case en regard du composant **Anchor Module Script (Script)** pour l’activer.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-145">Check the checkbox next to the **Anchor Module Script (Script)** components to enable it</span></span>
* <span data-ttu-id="9fc4a-146">Cochez la case en regard du composant **Sharing Module Script (Script)** pour l’activer.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-146">Check the checkbox next to the **Sharing Module Script (Script)** components to enable it</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section3-step1-2.png)

## <a name="trying-the-experience-with-spatial-alignment"></a><span data-ttu-id="9fc4a-148">Essai de l’expérience avec l’alignement spatial</span><span class="sxs-lookup"><span data-stu-id="9fc4a-148">Trying the experience with spatial alignment</span></span>

> [!NOTE]
> <span data-ttu-id="9fc4a-149">Azure Spatial Anchors ne peut pas s’exécuter dans Unity.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-149">Azure Spatial Anchors can not run in Unity.</span></span> <span data-ttu-id="9fc4a-150">Pour tester la fonctionnalité Azure Spatial Anchors, vous devez donc déployer le projet sur au moins deux appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-150">Consequently, to test the Azure Spatial Anchors functionality, you need to deploy the project to a minimum of two HoloLens devices.</span></span>

<span data-ttu-id="9fc4a-151">Si vous générez et déployez le projet Unity sur deux appareils HoloLens, vous pouvez obtenir un alignement spatial entre eux en partageant l’ID d’ancre Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-151">If you now build and deploy the Unity project to two HoloLens devices, you can achieve spatial alignment between the devices by sharing the Azure Anchor ID.</span></span> <span data-ttu-id="9fc4a-152">Pour le tester, vous pouvez effectuer ces étapes :</span><span class="sxs-lookup"><span data-stu-id="9fc4a-152">To test it out, you can follow these steps:</span></span>

1. <span data-ttu-id="9fc4a-153">Sur l’appareil HoloLens 1 : **Démarrez l’application** (le Rocket Launcher est instancié et placé sur la table).</span><span class="sxs-lookup"><span data-stu-id="9fc4a-153">On HoloLens device 1: **Start the application** (the Rocket Launcher is instantiated and placed on the table)</span></span>
2. <span data-ttu-id="9fc4a-154">Sur l’appareil HoloLens 2 : **Démarrez l’application** (les deux utilisateurs voient la table avec le Rocket Launcher, mais la table n’apparaît pas au même endroit et les avatars des utilisateurs n’apparaissent pas là où se trouvent les utilisateurs).</span><span class="sxs-lookup"><span data-stu-id="9fc4a-154">On HoloLens device 2: **Start the application** (both users see the table with the Rocket Launcher, however, the table does not appear in the same place and the user avatars do not appear where the users are)</span></span>
3. <span data-ttu-id="9fc4a-155">Sur l’appareil HoloLens 1 : Appuyez sur le bouton **Start Azure Session**.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-155">On HoloLens device 1: Press the **Start Azure Session** button</span></span>
4. <span data-ttu-id="9fc4a-156">Sur l’appareil HoloLens 1 : Appuyez sur le bouton **Create Azure Anchor** (crée une ancre à l’emplacement de l’objet TableAnchor et stocke les informations d’ancrage dans la ressource Azure).</span><span class="sxs-lookup"><span data-stu-id="9fc4a-156">On HoloLens device 1: Press the **Create Azure Anchor** button (creates anchor at the location of the TableAnchor object and stores the anchor information in the Azure resource).</span></span>
5. <span data-ttu-id="9fc4a-157">Sur l’appareil HoloLens 1 : Appuyez sur le bouton **Share Azure Anchor** (partage l’ID d’ancre avec d’autres utilisateurs en temps réel).</span><span class="sxs-lookup"><span data-stu-id="9fc4a-157">On HoloLens device 1: Press the **Share Azure Anchor** button (shares the anchor ID with other users in real-time)</span></span>
6. <span data-ttu-id="9fc4a-158">Sur l’appareil HoloLens 2 : Appuyez sur le bouton **Start Azure Session**.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-158">On HoloLens device 2: Press the **Start Azure Session** button</span></span>
7. <span data-ttu-id="9fc4a-159">Sur l’appareil HoloLens 2 : Appuyez sur le bouton **Get Azure Anchor** (se connecte à la ressource Azure pour récupérer les informations d’ancrage de l’ID d’ancre partagé, puis déplace l’objet TableAnchor à l’emplacement où l’ancre a été créée avec l’appareil HoloLens 1)</span><span class="sxs-lookup"><span data-stu-id="9fc4a-159">On HoloLens device 2: Press the **Get Azure Anchor** button (connects to the Azure resource to retrieve the anchor information for the shared anchor ID, then moves the TableAnchor object to the location where the anchor was created with the HoloLens device 1)</span></span>

## <a name="congratulations"></a><span data-ttu-id="9fc4a-160">Félicitations</span><span class="sxs-lookup"><span data-stu-id="9fc4a-160">Congratulations</span></span>

<span data-ttu-id="9fc4a-161">Dans ce tutoriel, vous avez appris à intégrer des ancres spatiales, une fonctionnalité puissante d’Azure, pour aligner des appareils dans une expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-161">In this tutorial, you learned how to integrate Azure's powerful Spatial Anchors to align devices in a shared experience.</span></span> <span data-ttu-id="9fc4a-162">Ainsi se conclut cette série de tutoriels où vous avez appris à configurer un compte et une application Photon, à intégrer Photon et PUN dans une application Unity, à configurer des avatars d’utilisateurs et des objets partagés, et enfin à aligner plusieurs participants à l’aide d’ASA.</span><span class="sxs-lookup"><span data-stu-id="9fc4a-162">This also concludes this tutorial series where you have learned how to set up a Photon account and application, integrate Photon and PUN into a Unity application, configure user avatars and shared objects, and finally align multiple participants using ASA.</span></span>
