---
title: Didacticiels sur les fonctionnalités multi-utilisateur-1. Configuration de la mise en réseau photonique Unity
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: efa03c49a9a083d2b8e591e03bccbeb776bb57b2
ms.sourcegitcommit: 2bfe9b1af4ee2cc0d668caeccb8ebc3137cbc20b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2020
ms.locfileid: "75901471"
---
# <a name="1-setting-up-photon-unity-networking"></a><span data-ttu-id="b98cf-105">1. Configuration de la mise en réseau photonique Unity</span><span class="sxs-lookup"><span data-stu-id="b98cf-105">1. Setting up Photon Unity Networking</span></span>

## <a name="overview"></a><span data-ttu-id="b98cf-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b98cf-106">Overview</span></span>

<span data-ttu-id="b98cf-107">Dans ce didacticiel, vous allez apprendre à préparer la création d’une expérience partagée en important la mise en réseau de photons Unity (retentissante) dans votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="b98cf-107">In this tutorial, you will learn how to prepare for creating a shared experience by importing Photon Unity Networking (PUN) into your Unity project.</span></span> <span data-ttu-id="b98cf-108">Photons est l’une des nombreuses options de mise en réseau disponibles pour les développeurs de réalité mixte pour créer des expériences partagées.</span><span class="sxs-lookup"><span data-stu-id="b98cf-108">Photon is one of several networking options available to Mixed Reality developers to create shared experiences.</span></span> <span data-ttu-id="b98cf-109">Vous allez apprendre à créer un compte de photons, à importer un photons et à créer un serveur local facultatif</span><span class="sxs-lookup"><span data-stu-id="b98cf-109">You will learn how to create a Photon account, import Photon, and create an optional local server</span></span>

## <a name="objectives"></a><span data-ttu-id="b98cf-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="b98cf-110">Objectives</span></span>

* <span data-ttu-id="b98cf-111">Découvrez comment créer un compte de photons</span><span class="sxs-lookup"><span data-stu-id="b98cf-111">Learn how to create a Photon account</span></span>
* <span data-ttu-id="b98cf-112">Découvrez comment rechercher et importer une mise en réseau photonique Unity</span><span class="sxs-lookup"><span data-stu-id="b98cf-112">Learn how to find and import Photon Unity Networking</span></span>
* <span data-ttu-id="b98cf-113">Configurer un serveur de photons local</span><span class="sxs-lookup"><span data-stu-id="b98cf-113">Set up a local Photon server</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b98cf-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="b98cf-114">Prerequisites</span></span>

>[!TIP]
><span data-ttu-id="b98cf-115">Si vous n’avez pas encore terminé les didacticiels de [prise](mrlearning-base.md) en main et les didacticiels sur les [ancres spatiales Azure](mrlearning-asa-ch1.md) , nous vous recommandons d’effectuer d’abord ces didacticiels.</span><span class="sxs-lookup"><span data-stu-id="b98cf-115">If you have not completed the [Getting started tutorials](mrlearning-base.md) and [Azure Spatial Anchors started tutorials](mrlearning-asa-ch1.md) tutorial series yet, it's recommended that you complete those tutorials first.</span></span>

* <span data-ttu-id="b98cf-116">Un PC Windows 10 configuré avec les outils corrects [installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="b98cf-116">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="b98cf-117">Windows 10 SDK 10.0.18362.0 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="b98cf-117">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="b98cf-118">Certaines fonctionnalités C# de programmation de base</span><span class="sxs-lookup"><span data-stu-id="b98cf-118">Some basic C# programming ability</span></span>
* <span data-ttu-id="b98cf-119">Un appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)</span><span class="sxs-lookup"><span data-stu-id="b98cf-119">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>

>[!IMPORTANT]
><span data-ttu-id="b98cf-120">Cette série de didacticiels requiert <a href="https://unity3d.com/get-unity/download/archive" target="_blank">unity 2019,1</a> et la version recommandée est Unity 2019.1.14.</span><span class="sxs-lookup"><span data-stu-id="b98cf-120">This tutorial series requires <a href="https://unity3d.com/get-unity/download/archive" target="_blank">Unity 2019.1</a> and the recommended version is Unity 2019.1.14.</span></span> <span data-ttu-id="b98cf-121">Cela remplace toute exigence ou recommandation de version Unity énoncées dans les conditions préalables liées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b98cf-121">This supersedes any Unity version requirements or recommendations stated in the prerequisites linked above.</span></span>

## <a name="setting-up-photon"></a><span data-ttu-id="b98cf-122">Configuration de photons</span><span class="sxs-lookup"><span data-stu-id="b98cf-122">Setting up Photon</span></span>

1. <span data-ttu-id="b98cf-123">Configurez un compte de [photons](https://dashboard.photonengine.com//Account/SignUp) .</span><span class="sxs-lookup"><span data-stu-id="b98cf-123">Set up a [Photon](https://dashboard.photonengine.com//Account/SignUp) account.</span></span> <span data-ttu-id="b98cf-124">Accédez à la page d’inscription à photons en cliquant sur [ce lien](https://dashboard.photonengine.com//Account/SignUp).</span><span class="sxs-lookup"><span data-stu-id="b98cf-124">Navigate to the Photon Sign-up page by clicking on [this link](https://dashboard.photonengine.com//Account/SignUp).</span></span> <span data-ttu-id="b98cf-125">Suivez les instructions de la page d’inscription pour créer le compte.</span><span class="sxs-lookup"><span data-stu-id="b98cf-125">Follow the instructions on the sign-up page to create the account.</span></span>

    ![Module3Chapter1step1im](images/module3chapter1step1im.PNG)

    ![Module3Chapter1step6im](images/module3chapter1step6im.PNG)

2. <span data-ttu-id="b98cf-128">Créez un ID d’application en cliquant sur le bouton créer une application.</span><span class="sxs-lookup"><span data-stu-id="b98cf-128">Create an application ID by clicking the Create a New App button.</span></span>

    ![Module3Chapter1step7aim](images/module3chapter1step7aim.PNG)

3. <span data-ttu-id="b98cf-130">Sélectionnez photons retentissante dans le menu déroulant sous type de photons.</span><span class="sxs-lookup"><span data-stu-id="b98cf-130">Select Photon PUN from the dropdown menu under Photon Type.</span></span> <span data-ttu-id="b98cf-131">Donnez-lui un nom.</span><span class="sxs-lookup"><span data-stu-id="b98cf-131">Then give it a name.</span></span> <span data-ttu-id="b98cf-132">Dans cet exemple, nous avons nommé IT HoloLensPhotonProject.</span><span class="sxs-lookup"><span data-stu-id="b98cf-132">In this example, we named it HoloLensPhotonProject.</span></span> <span data-ttu-id="b98cf-133">Une fois terminé, cliquez sur le bouton créer.</span><span class="sxs-lookup"><span data-stu-id="b98cf-133">Once finished, click the Create button.</span></span>

    ![Module3Chapter1step7bim](images/module3chapter1step7bim.PNG)

4. <span data-ttu-id="b98cf-135">Revenez à la page de votre application et vous devriez voir une image semblable à celle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b98cf-135">Return to your applications page and you should see something similar to the picture below.</span></span> <span data-ttu-id="b98cf-136">Cliquez sur l’ID d’application et copiez-le.</span><span class="sxs-lookup"><span data-stu-id="b98cf-136">Click the application ID and copy it.</span></span> <span data-ttu-id="b98cf-137">Collez-la quelque part pour y accéder facilement.</span><span class="sxs-lookup"><span data-stu-id="b98cf-137">Paste it somewhere you can easily access.</span></span>  

    ![Module3Chapter1step8im](images/module3chapter1step8im.PNG)

5. <span data-ttu-id="b98cf-139">Créez un nouveau projet Unity et nommez-le HLSharingProject.</span><span class="sxs-lookup"><span data-stu-id="b98cf-139">Create a new unity project and name it HLSharingProject.</span></span> <span data-ttu-id="b98cf-140">Pour obtenir des instructions sur la création d’un nouveau projet Unity, reportez-vous à [la section « créer un projet Unity » du module de base](https://docs.microsoft.com//windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project).</span><span class="sxs-lookup"><span data-stu-id="b98cf-140">For instructions on how to create a new Unity project, please refer to [the Base Module's "Create Unity Project" section](https://docs.microsoft.com//windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project).</span></span> 

6. <span data-ttu-id="b98cf-141">Une fois le projet chargé, cliquez sur l’onglet stockage des ressources, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b98cf-141">Once the project loads, click the Assets Store tab, as shown in the image below.</span></span> <span data-ttu-id="b98cf-142">Ensuite, dans la zone de recherche mise en surbrillance dans l’image ci-dessous, tapez retentissante, puis sélectionnez la ressource photon retentissante 2-FREE» dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="b98cf-142">Then, in the search box highlighted in the image below, type in PUN, and select the Photon PUN 2 - FREE" asset from the search results.</span></span>

    ![Module3Chapter1step10im](images/module3chapter1step10im.PNG)

7. <span data-ttu-id="b98cf-144">Téléchargez et importez cette ressource en appuyant sur les boutons télécharger et importer.</span><span class="sxs-lookup"><span data-stu-id="b98cf-144">Download and import this asset by pressing the Download and Import buttons.</span></span>

    ![Module3Chapter1step11im](images/module3chapter1step11im.PNG)

8. <span data-ttu-id="b98cf-146">Une fois que photon a terminé le processus d’importation, l’Assistant retentissante s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b98cf-146">Once Photon has completed the importing process, the Pun Wizard appears.</span></span> <span data-ttu-id="b98cf-147">Prenez l’ID d’application (qui doit se trouver dans le presse-papiers) de l’étape 4, collez-le dans la zone AppID, puis appuyez sur le bouton du projet d’installation.</span><span class="sxs-lookup"><span data-stu-id="b98cf-147">Take the application ID (which should be in your clipboard) from step 4, paste it into the AppID box, and press the Setup Project button.</span></span>

    ![module3chapter1step12im](images/module3chapter1step12im.PNG)

9. <span data-ttu-id="b98cf-149">Après avoir ajouté avec succès l’AppID, accédez à photons-> PhotonUnityNetworking-> Ressources-> PhotonServerSettings dans ressources.</span><span class="sxs-lookup"><span data-stu-id="b98cf-149">After successfully adding the AppID, navigate to Photon->PhotonUnityNetworking ->Resources->PhotonServerSettings in Assets.</span></span> <span data-ttu-id="b98cf-150">Sélectionnez l’option utiliser le serveur de noms, puis définissez la région fixe sur US ou votre région de service de photons.</span><span class="sxs-lookup"><span data-stu-id="b98cf-150">Select the Use Name Server option, and set the fixed region to US or your photon service region.</span></span>

    ![module3chapter1step13im](images/module3chapter1step13im.PNG)

## <a name="congratulations"></a><span data-ttu-id="b98cf-152">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="b98cf-152">Congratulations</span></span>

<span data-ttu-id="b98cf-153">Vous venez de créer un compte de photons, de configurer un serveur de photons local et d’importer des retentissante dans Unity.</span><span class="sxs-lookup"><span data-stu-id="b98cf-153">You have successfully created a Photon account, set up a local Photon server, and imported PUN into Unity.</span></span> <span data-ttu-id="b98cf-154">L’étape suivante consiste à configurer le projet et à autoriser les connexions avec d’autres utilisateurs afin que plusieurs utilisateurs puissent voir votre travail.</span><span class="sxs-lookup"><span data-stu-id="b98cf-154">Your next step is to set up the project and allow connections with other users so that multiple users can see your work.</span></span>

<span data-ttu-id="b98cf-155">[Didacticiel suivant : 2. l’obtention d’Unity est prête pour le développement](mrlearning-sharing(photon)-ch2.md)</span><span class="sxs-lookup"><span data-stu-id="b98cf-155">[Next tutorial: 2. Getting Unity ready for development](mrlearning-sharing(photon)-ch2.md)</span></span>
