---
title: Tutoriels sur les fonctionnalités multiutilisateurs - 3. Connexion de plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multiutilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: a597aadbddb49fefc824d8c5b5193585fa9476a5
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "81610953"
---
# <a name="2-connecting-multiple-users"></a><span data-ttu-id="92efc-105">2. Connexion de plusieurs utilisateurs</span><span class="sxs-lookup"><span data-stu-id="92efc-105">2. Connecting multiple users</span></span>

<span data-ttu-id="92efc-106">Dans ce tutoriel, vous allez apprendre à connecter plusieurs utilisateurs dans le cadre d’une expérience partagée en direct.</span><span class="sxs-lookup"><span data-stu-id="92efc-106">In this tutorial, you will learn how to connect multiple users as part of a live shared experience.</span></span> <span data-ttu-id="92efc-107">À la fin du tutoriel, vous pourrez exécuter l’application sur plusieurs appareils et chaque utilisateur pourra voir l’avatar d’autres utilisateurs se déplacer en temps réel.</span><span class="sxs-lookup"><span data-stu-id="92efc-107">By the end of the tutorial you will be able to run the application on multiple devices and have each user see the avatar of other users move in real-time.</span></span>

## <a name="objectives"></a><span data-ttu-id="92efc-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="92efc-108">Objectives</span></span>

* <span data-ttu-id="92efc-109">Découvrir comment connecter plusieurs utilisateurs dans un environnement partagé</span><span class="sxs-lookup"><span data-stu-id="92efc-109">Learn how to connect multiple users in a shared experience</span></span>

## <a name="preparing-the-scene"></a><span data-ttu-id="92efc-110">Préparation de la scène</span><span class="sxs-lookup"><span data-stu-id="92efc-110">Preparing the scene</span></span>

<span data-ttu-id="92efc-111">Dans cette section, vous allez préparer la scène en ajoutant une partie des préfabriqués du tutoriel.</span><span class="sxs-lookup"><span data-stu-id="92efc-111">In this section, you will prepare the scene by adding some of the tutorial prefabs.</span></span>

<span data-ttu-id="92efc-112">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs**.</span><span class="sxs-lookup"><span data-stu-id="92efc-112">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs** folder.</span></span> <span data-ttu-id="92efc-113">Tout en maintenant le bouton Ctrl enfoncé, cliquez sur **DebugWindow**, **NetworkLobby** et **SharedPlayground** pour sélectionner les trois préfabriqués :</span><span class="sxs-lookup"><span data-stu-id="92efc-113">While holding down the CTRL button, click on **DebugWindow**, **NetworkLobby**, and **SharedPlayground** to select the three prefabs:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section1-step1-1.png)

<span data-ttu-id="92efc-115">Les trois préfabriqués étant sélectionnés, faites-les glisser dans la fenêtre Hierarchy pour les ajouter à la scène :</span><span class="sxs-lookup"><span data-stu-id="92efc-115">With the three prefabs still selected, drag them into the Hierarchy window to add them to the scene:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section1-step1-2.png)

## <a name="creating-the-user-prefab"></a><span data-ttu-id="92efc-117">Création du préfabriqué utilisateur</span><span class="sxs-lookup"><span data-stu-id="92efc-117">Creating the user prefab</span></span>

<span data-ttu-id="92efc-118">Dans cette section, vous allez créer un préfabriqué qui sera utilisé pour représenter les utilisateurs dans l’expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="92efc-118">In this section, you will create a prefab that will be used to represent the users in the shared experience.</span></span>

### <a name="1-create-and-configure-the-user"></a><span data-ttu-id="92efc-119">1. Créer et configurer l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="92efc-119">1. Create and configure the user</span></span>

<span data-ttu-id="92efc-120">Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur une zone vide et sélectionnez **Create Empty** pour ajouter un objet vide à votre scène, nommez l’objet **PhotonUser**, puis configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="92efc-120">In the Hierarchy window, right-click on an empty area and select **Create Empty** to add an empty object to your scene, name the object **PhotonUser**, and configure it as follows:</span></span>

* <span data-ttu-id="92efc-121">Vérifiez que le paramètre **Position** de Transform a les valeurs X = 0, Y = 0, Z = 0 :</span><span class="sxs-lookup"><span data-stu-id="92efc-121">Ensure the Transform **Position** is set to X = 0, Y = 0, Z = 0:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step1-1.png)

<span data-ttu-id="92efc-123">L’objet **PhotonUser** étant toujours sélectionné, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Photon User (Script)** à l’objet PhotonUser :</span><span class="sxs-lookup"><span data-stu-id="92efc-123">With the **PhotonUser** object still selected, in the Inspector window, use the **Add Component** button to add the **Photon User (Script)** component to the PhotonUser object:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step1-2.png)

<span data-ttu-id="92efc-125">Dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Generic Net Sync (Script)** à l’objet PhotonUser et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="92efc-125">In the Inspector window, use the **Add Component** button to add the **Generic Net Sync (Script)** component to the PhotonUser object and configure it as follows:</span></span>

* <span data-ttu-id="92efc-126">Cochez la case **Is User**.</span><span class="sxs-lookup"><span data-stu-id="92efc-126">Check the **Is User** checkbox</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step1-3.png)

<span data-ttu-id="92efc-128">Dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Photon View (Script)** à l’objet PhotonUser et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="92efc-128">In the Inspector window, use the **Add Component** button to add the **Photon View (Script)** component to the PhotonUser object and configure it as follows:</span></span>

* <span data-ttu-id="92efc-129">Affectez au champ **Observed Components** le composant Generic Net Sync (Script).</span><span class="sxs-lookup"><span data-stu-id="92efc-129">To the **Observed Components** field, assign the Generic Net Sync (Script) component</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step1-4.png)

### <a name="2-create-the-avatar"></a><span data-ttu-id="92efc-131">2. Créer l’avatar</span><span class="sxs-lookup"><span data-stu-id="92efc-131">2. Create the avatar</span></span>

<span data-ttu-id="92efc-132">Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur l’objet **PhotonUser**, puis sélectionnez **3D Object** > **Sphere** pour créer un objet Sphere en tant qu’enfant de l’objet PhotonUser et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="92efc-132">In the Hierarchy window, right-click on the **PhotonUser** object and select **3D Object** > **Sphere** to create a sphere object as a child of the PhotonUser object and configure it as follows:</span></span>

* <span data-ttu-id="92efc-133">Vérifiez que le paramètre **Position** de Transform a les valeurs X = 0, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="92efc-133">Ensure the Transform **Position** is set to X = 0, Y = 0, Z = 0</span></span>
* <span data-ttu-id="92efc-134">Changez le paramètre **Scale** de Transform en une taille appropriée, par exemple X = 0,15, Y = 0,15, Z = 0,15.</span><span class="sxs-lookup"><span data-stu-id="92efc-134">Change the Transform **Scale** to a suitable size, for example, X = 0.15, Y = 0.15, Z = 0.15</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step2-1.png)

### <a name="3-create-the-prefab"></a><span data-ttu-id="92efc-136">3. Créer le préfabriqué</span><span class="sxs-lookup"><span data-stu-id="92efc-136">3. Create the prefab</span></span>

<span data-ttu-id="92efc-137">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources** :</span><span class="sxs-lookup"><span data-stu-id="92efc-137">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources** folder:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step3-1.png)

<span data-ttu-id="92efc-139">Le dossier Resources étant toujours sélectionné, **cliquez et faites glisser** l’objet **PhotonUser** de la fenêtre Hierarchy vers le dossier **Resources** pour transformer l’objet PhotonUser en préfabriqué :</span><span class="sxs-lookup"><span data-stu-id="92efc-139">With the Resources folder still selected, **click-and-drag** the **PhotonUser** object from the Hierarchy window into the **Resources** folder to make the PhotonUser object a prefab:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step3-2.png)

<span data-ttu-id="92efc-141">Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur l’objet **PhotonUser** et sélectionnez **Delete** pour le supprimer de la scène :</span><span class="sxs-lookup"><span data-stu-id="92efc-141">In the Hierarchy window, right-click on the **PhotonUser** object and select **Delete** to remove it from the scene:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step3-3.png)

## <a name="configuring-pun-to-instantiate-the-user-prefab"></a><span data-ttu-id="92efc-143">Configuration de PUN pour instancier le préfabriqué utilisateur</span><span class="sxs-lookup"><span data-stu-id="92efc-143">Configuring PUN to instantiate the user prefab</span></span>

<span data-ttu-id="92efc-144">Dans cette section, vous allez configurer le projet pour qu’il utilise le préfabriqué PhotonUser créé dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="92efc-144">In this section, you will configure the project to use the PhotonUser prefab you created in the previous section.</span></span>

<span data-ttu-id="92efc-145">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources**.</span><span class="sxs-lookup"><span data-stu-id="92efc-145">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources** folder.</span></span>

<span data-ttu-id="92efc-146">Dans la fenêtre Hierarchy, développez l’objet **NetworkLobby** et sélectionnez l’objet enfant **NetworkRoom**. Ensuite, dans la fenêtre Inspector, localisez le composant **Photon Room (Script)** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="92efc-146">In the Hierarchy window, expand the **NetworkLobby** object and select the **NetworkRoom** child object, then in the Inspector window, locate the **Photon Room (Script)** component and configure it as follows:</span></span>

* <span data-ttu-id="92efc-147">Affectez au champ **Photon User Prefab** le préfabriqué **PhotonUser** du dossier Resources.</span><span class="sxs-lookup"><span data-stu-id="92efc-147">To the **Photon User Prefab** field, assign the **PhotonUser** prefab from the Resources folder</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section3-step1-1.png)

## <a name="trying-the-experience-with-multiple-users"></a><span data-ttu-id="92efc-149">Essai de l’expérience avec plusieurs utilisateurs</span><span class="sxs-lookup"><span data-stu-id="92efc-149">Trying the experience with multiple users</span></span>

<span data-ttu-id="92efc-150">Vous pouvez à présent générer le projet Unity et le déployer sur votre HoloLens. De retour dans Unity, si vous appuyez sur le bouton Play pour passer en mode Game pendant que l’application s’exécute sur votre HoloLens, vous voyez l’avatar de l’utilisateur HoloLens se déplacer quand vous bougez la tête (HoloLens) :</span><span class="sxs-lookup"><span data-stu-id="92efc-150">If you now build and deploy the Unity project to your HoloLens, and then, back in Unity, press the Play button to enter Game mode while the application is running on your HoloLens, you will see the HoloLens user avatar move when you move your head (HoloLens) around:</span></span>

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section4-step1-1.gif)

> [!TIP]
> <span data-ttu-id="92efc-152">Pour un rappel de la façon de générer et déployer votre projet Unity sur HoloLens 2, vous pouvez vous référer aux instructions de [Générer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device).</span><span class="sxs-lookup"><span data-stu-id="92efc-152">For a reminder on how to build and deploy your Unity project to HoloLens 2, you can refer to the [Build your application to your device](mrlearning-base-ch1.md#build-your-application-to-your-device) instructions.</span></span>

> [!CAUTION]
> <span data-ttu-id="92efc-153">L’application a besoin de se connecter à Photon, donc vérifiez que votre ordinateur/appareil est connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="92efc-153">The application needs to connect to Photon, so make sure your computer/device is connected to the internet.</span></span>

## <a name="congratulations"></a><span data-ttu-id="92efc-154">Félicitations</span><span class="sxs-lookup"><span data-stu-id="92efc-154">Congratulations</span></span>

<span data-ttu-id="92efc-155">Votre projet est désormais configuré pour permettre à plusieurs utilisateurs de se connecter à la même expérience et de voir leurs mouvements.</span><span class="sxs-lookup"><span data-stu-id="92efc-155">You have successfully configured your project to allow multiple users to connect to the same experience and see each other's movements.</span></span> <span data-ttu-id="92efc-156">Dans le tutoriel suivant, vous allez implémenter des fonctionnalités pour partager les mouvements d’objets avec plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="92efc-156">In the next tutorial, you will implement functionality so that the movements of objects are also shared across multiple devices.</span></span>

<span data-ttu-id="92efc-157">[Tutoriel suivant : 2. Partage de mouvements d’objet avec plusieurs utilisateurs](mrlearning-sharing(photon)-ch3.md)</span><span class="sxs-lookup"><span data-stu-id="92efc-157">[Next tutorial: 2. Sharing object movements with multiple users](mrlearning-sharing(photon)-ch3.md)</span></span>
