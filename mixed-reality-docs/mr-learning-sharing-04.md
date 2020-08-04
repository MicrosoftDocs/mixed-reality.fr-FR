---
title: Tutoriels sur les fonctionnalités multi-utilisateurs - 4. Partage de mouvements d’objet avec plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 7dbe25cd1b0329e366fcbd567074018025032f9e
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376561"
---
# <a name="4-sharing-object-movements-with-multiple-users"></a><span data-ttu-id="181d9-105">4. Partage de mouvements d’objet avec plusieurs utilisateurs</span><span class="sxs-lookup"><span data-stu-id="181d9-105">4. Sharing object movements with multiple users</span></span>

<span data-ttu-id="181d9-106">Dans ce tutoriel, vous allez apprendre à partager les mouvements d’objets pour que tous les participants d’une expérience partagée puissent collaborer et voir leurs interactions.</span><span class="sxs-lookup"><span data-stu-id="181d9-106">In this tutorial, you will learn how to share the movements of objects so that all participants of a shared experience can collaborate and view each other's interactions.</span></span>

## <a name="objectives"></a><span data-ttu-id="181d9-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="181d9-107">Objectives</span></span>

* <span data-ttu-id="181d9-108">Configurer votre projet pour partager les mouvements d’objets</span><span class="sxs-lookup"><span data-stu-id="181d9-108">Configure your project to share the movements of objects</span></span>
* <span data-ttu-id="181d9-109">Apprendre à créer une application collaborative multiutilisateur simple</span><span class="sxs-lookup"><span data-stu-id="181d9-109">Learn how to build a basic multi-user collaborative app</span></span>

## <a name="preparing-the-scene"></a><span data-ttu-id="181d9-110">Préparation de la scène</span><span class="sxs-lookup"><span data-stu-id="181d9-110">Preparing the scene</span></span>

<span data-ttu-id="181d9-111">Dans cette section, vous allez préparer la scène en ajoutant le préfabriqué du tutoriel.</span><span class="sxs-lookup"><span data-stu-id="181d9-111">In this section, you will prepare the scene by adding the tutorial prefab.</span></span>

<span data-ttu-id="181d9-112">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs**, puis faites glisser le préfabriqué **TableAnchor** sur l’objet **SharedPlayground** dans la fenêtre Hierarchy afin de l’ajouter à votre scène en tant qu’enfant de l’objet SharedPlayground :</span><span class="sxs-lookup"><span data-stu-id="181d9-112">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs** folder and drag the **TableAnchor** prefab onto the **SharedPlayground** object in the Hierarchy window to add it to your scene as a child of the SharedPlayground object:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-04-section1-step1-1.png)

## <a name="configuring-pun-to-instantiate-the-objects"></a><span data-ttu-id="181d9-114">Configuration de PUN pour instancier les objets</span><span class="sxs-lookup"><span data-stu-id="181d9-114">Configuring PUN to instantiate the objects</span></span>

<span data-ttu-id="181d9-115">Dans cette section, vous allez configurer le projet de façon à utiliser l’expérience Rover Explorer créée pendant les [tutoriels de démarrage](mr-learning-base-01.md) et définir où il sera instancié.</span><span class="sxs-lookup"><span data-stu-id="181d9-115">In this section, you will configure the project to use the Rover Explorer experience created during the [Getting started tutorials](mr-learning-base-01.md) and define where it will be instantiated.</span></span>

<span data-ttu-id="181d9-116">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources**.</span><span class="sxs-lookup"><span data-stu-id="181d9-116">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources** folder.</span></span>

<span data-ttu-id="181d9-117">Dans la fenêtre Hierarchy, développez l’objet **NetworkLobby** et sélectionnez l’objet enfant **NetworkRoom**. Ensuite, dans la fenêtre Inspector, localisez le composant **Photon Room (Script)** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="181d9-117">In the Hierarchy window, expand the **NetworkLobby** object and select the **NetworkRoom** child object, then in the Inspector window, locate the **Photon Room (Script)** component and configure it as follows:</span></span>

* <span data-ttu-id="181d9-118">Dans le champ **Rover Explorer Prefab**, attribuez le préfabriqué **RoverExplorer_Complete_Variant** à partir du dossier Resources.</span><span class="sxs-lookup"><span data-stu-id="181d9-118">To the **Rover Explorer Prefab** field, assign the **RoverExplorer_Complete_Variant** prefab from the Resources folder</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-04-section2-step1-1.png)

<span data-ttu-id="181d9-120">L’objet enfant **NetworkRoom** étant toujours sélectionné, dans la fenêtre Hierarchy, développez l’objet **TableAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Photon Room (Script)** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="181d9-120">With the **NetworkRoom** child object still selected, in the Hierarchy window, expand the **TableAnchor** object, then in the Inspector window, locate the **Photon Room (Script)** component and configure it as follows:</span></span>

* <span data-ttu-id="181d9-121">Affectez au champ **Rover Explorer Location** l’objet enfant TableAnchor > **Table** à partir de la fenêtre Hierarchy.</span><span class="sxs-lookup"><span data-stu-id="181d9-121">To the **Rover Explorer Location** field, assign the TableAnchor > **Table** child object from the Hierarchy window</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-04-section2-step1-2.png)

## <a name="trying-the-experience-with-shared-object-movement"></a><span data-ttu-id="181d9-123">Essai de l’expérience avec le mouvement d’objet partagé</span><span class="sxs-lookup"><span data-stu-id="181d9-123">Trying the experience with shared object movement</span></span>

<span data-ttu-id="181d9-124">Vous pouvez à présent générer le projet Unity et le déployer sur votre HoloLens. De retour dans Unity, si vous appuyez sur le bouton Play pour passer en mode Game pendant que l’application s’exécute sur votre HoloLens, vous voyez l’objet se déplacer dans Unity quand vous le déplacez dans HoloLens :</span><span class="sxs-lookup"><span data-stu-id="181d9-124">If you now build and deploy the Unity project to your HoloLens, and then, back in Unity, press the Play button to enter Game mode while the app is running on your HoloLens, you will see the object move in Unity when you move the object in HoloLens:</span></span>

![mr-learning-sharing](images/mr-learning-sharing/sharing-04-section3-step1-1.gif)

## <a name="congratulations"></a><span data-ttu-id="181d9-126">Félicitations</span><span class="sxs-lookup"><span data-stu-id="181d9-126">Congratulations</span></span>

<span data-ttu-id="181d9-127">Vous venez de configurer votre projet pour synchroniser les mouvements d’objet afin que les utilisateurs puissent voir les objets se déplacer quand d’autres utilisateurs les déplacent.</span><span class="sxs-lookup"><span data-stu-id="181d9-127">You have successfully configured your project to synchronize object movements so users can see the objects move when other users move them.</span></span> <span data-ttu-id="181d9-128">Dans le tutoriel suivant, vous allez implémenter une fonctionnalité afin d’aligner l’expérience dans le monde physique.</span><span class="sxs-lookup"><span data-stu-id="181d9-128">In the next tutorial, you will implement functionality to align the experience in the physical world.</span></span> <span data-ttu-id="181d9-129">Cela permettra de s’assurer que les utilisateurs se voient les uns les autres à leur emplacement physique réel, et que les objets apparaissent dans la même position physique et la même rotation pour tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="181d9-129">This will ensure the users see each other in their actual physical location, and so the objects appear in the same physical position and rotation for all users.</span></span>

[<span data-ttu-id="181d9-130">Tutoriel suivant : 5. Intégration d’ancres spatiales Azure dans une expérience partagée</span><span class="sxs-lookup"><span data-stu-id="181d9-130">Next Tutorial: 5. Integrating Azure Spatial Anchors into a shared experience</span></span>](mr-learning-sharing-05.md)
