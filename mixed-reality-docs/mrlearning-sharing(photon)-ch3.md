---
title: Tutoriels sur les fonctionnalités multi-utilisateurs - 4. Partage de mouvements d’objet avec plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 41b62eb2d9f400d0af341c9fcce887c72af7a3aa
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "81610616"
---
# <a name="3-sharing-object-movements-with-multiple-users"></a><span data-ttu-id="ec982-105">3. Partage de mouvements d’objet avec plusieurs utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ec982-105">3. Sharing object movements with multiple users</span></span>

<span data-ttu-id="ec982-106">Dans ce tutoriel, vous allez apprendre à partager les mouvements d’objets pour que tous les participants d’une expérience partagée puissent collaborer et voir leurs interactions.</span><span class="sxs-lookup"><span data-stu-id="ec982-106">In this tutorial, you will learn how to share the movements of objects so that all participants of a shared experience can collaborate and view each others' interactions.</span></span>

## <a name="objectives"></a><span data-ttu-id="ec982-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="ec982-107">Objectives</span></span>

* <span data-ttu-id="ec982-108">Configurer votre projet pour partager les mouvements d’objets</span><span class="sxs-lookup"><span data-stu-id="ec982-108">Configure your project to share the movements of objects</span></span>
* <span data-ttu-id="ec982-109">Apprendre à créer une application collaborative multi-utilisateur de base</span><span class="sxs-lookup"><span data-stu-id="ec982-109">Learn how to build a basic multi-user collaborative application</span></span>

## <a name="preparing-the-scene"></a><span data-ttu-id="ec982-110">Préparation de la scène</span><span class="sxs-lookup"><span data-stu-id="ec982-110">Preparing the scene</span></span>

<span data-ttu-id="ec982-111">Dans cette section, vous allez préparer la scène en ajoutant le préfabriqué du tutoriel.</span><span class="sxs-lookup"><span data-stu-id="ec982-111">In this section, you will prepare the scene by adding the tutorial prefab.</span></span>

<span data-ttu-id="ec982-112">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs**, puis faites glisser le préfabriqué **TableAnchor** sur l’objet **SharedPlayground** dans la fenêtre Hierarchy pour l’ajouter à votre scène en tant qu’enfant de l’objet SharedPlayground :</span><span class="sxs-lookup"><span data-stu-id="ec982-112">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs** folder and drag the **TableAnchor** prefab on top of the **SharedPlayground** object in the Hierarchy window to add it to your scene as a child of the SharedPlayground object:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial3-section1-step1-1.png)

## <a name="configuring-pun-to-instantiate-the-objects"></a><span data-ttu-id="ec982-114">Configuration de PUN pour instancier les objets</span><span class="sxs-lookup"><span data-stu-id="ec982-114">Configuring PUN to instantiate the objects</span></span>

<span data-ttu-id="ec982-115">Dans cette section, vous allez configurer le projet pour qu’il utilise le préfabriqué RocketLauncher_Complete_Variant créé dans la section précédente et définir où il sera instancié.</span><span class="sxs-lookup"><span data-stu-id="ec982-115">In this section, you will configure the project to use the RocketLauncher_Complete_Variant prefab you created in the previous section and define where it will be instantiated.</span></span>

<span data-ttu-id="ec982-116">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources**.</span><span class="sxs-lookup"><span data-stu-id="ec982-116">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources** folder.</span></span>

<span data-ttu-id="ec982-117">Dans la fenêtre Hierarchy, développez l’objet **NetworkLobby** et sélectionnez l’objet enfant **NetworkRoom**. Ensuite, dans la fenêtre Inspector, localisez le composant **Photon Room (Script)** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec982-117">In the Hierarchy window, expand the **NetworkLobby** object and select the **NetworkRoom** child object, then in the Inspector window, locate the **Photon Room (Script)** component and configure it as follows:</span></span>

* <span data-ttu-id="ec982-118">Affectez au champ **Photon User Prefab** le préfabriqué **PhotonUser** du dossier Resources.</span><span class="sxs-lookup"><span data-stu-id="ec982-118">To the **Photon User Prefab** field, assign the **PhotonUser** prefab from the Resources folder</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial3-section2-step1-1.png)

<span data-ttu-id="ec982-120">L’objet enfant **NetworkRoom** étant toujours sélectionné, dans la fenêtre Hierarchy, développez l’objet **TableAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Photon Room (Script)** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="ec982-120">With the **NetworkRoom** child object still selected, in the Hierarchy window, expand the **TableAnchor** object, then in the Inspector window, locate the **Photon Room (Script)** component and configure it as follows:</span></span>

* <span data-ttu-id="ec982-121">Affectez au champ **Rocket Launcher Location** l’objet enfant **Table** à partir de la fenêtre Hierarchy.</span><span class="sxs-lookup"><span data-stu-id="ec982-121">To the **Rocket Launcher Location** field, assign the **Table** child object from the Hierarchy window</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial3-section2-step1-2.png)

## <a name="trying-the-experience-with-shared-object-movement"></a><span data-ttu-id="ec982-123">Essai de l’expérience avec le mouvement d’objet partagé</span><span class="sxs-lookup"><span data-stu-id="ec982-123">Trying the experience with shared object movement</span></span>

<span data-ttu-id="ec982-124">Vous pouvez à présent générer le projet Unity et le déployer sur votre HoloLens. De retour dans Unity, si vous appuyez sur le bouton Play pour passer en mode Game pendant que l’application s’exécute sur votre HoloLens, vous voyez l’objet se déplacer dans Unity quand vous le déplacez dans HoloLens :</span><span class="sxs-lookup"><span data-stu-id="ec982-124">If you now build and deploy the Unity project to your HoloLens, and then, back in Unity, press the Play button to enter Game mode while the application is running on your HoloLens, you will see the object move in Unity when you move the object in HoloLens:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial3-section3-step1-1.gif)

## <a name="congratulations"></a><span data-ttu-id="ec982-126">Félicitations</span><span class="sxs-lookup"><span data-stu-id="ec982-126">Congratulations</span></span>

<span data-ttu-id="ec982-127">Vous venez de configurer votre projet pour synchroniser les mouvements d’objet. Les utilisateurs peuvent ainsi voir les objets se déplacer quand d’autres utilisateurs les déplacent.</span><span class="sxs-lookup"><span data-stu-id="ec982-127">You have successfully configured your project so object movements are synchronized and users can see the objects move when other users move the objects.</span></span> <span data-ttu-id="ec982-128">Dans le tutoriel suivant, vous allez implémenter des fonctionnalités pour aligner l’expérience partagée dans le monde physique, permettre aux utilisateurs de se voir à leur emplacement physique réel et faire en sorte que la position physique et la rotation des objets soient identiques pour tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ec982-128">In the next tutorial, you will implement functionality so the shared experience is aligned in the physical world and the users see each other in their actual physical location and so the objects appear in the same physical position and rotation for all users.</span></span>

<span data-ttu-id="ec982-129">[Tutoriel suivant : 4. Intégration d’ancres spatiales Azure dans une expérience partagée](mrlearning-sharing(photon)-ch4.md)</span><span class="sxs-lookup"><span data-stu-id="ec982-129">[Next tutorial: 4. Integrating Azure Spatial Anchors into a shared experience](mrlearning-sharing(photon)-ch4.md)</span></span>
