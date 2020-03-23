---
title: Tutoriels sur les fonctionnalités multiutilisateurs - 1. Configuration de Photon Unity Networking
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multiutilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 94068ff706e0e56ca8ec0f23beaed3a34159b777
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79031328"
---
# <a name="1-setting-up-photon-unity-networking"></a><span data-ttu-id="42b4e-105">1. Configuration de Photon Unity Networking</span><span class="sxs-lookup"><span data-stu-id="42b4e-105">1. Setting up Photon Unity Networking</span></span>

## <a name="overview"></a><span data-ttu-id="42b4e-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="42b4e-106">Overview</span></span>

<span data-ttu-id="42b4e-107">Dans ce tutoriel, vous allez découvrir comment préparer la création d’une expérience partagée en important Photon Unity Networking (PUN) dans votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="42b4e-107">In this tutorial, you will learn how to prepare for creating a shared experience by importing Photon Unity Networking (PUN) into your Unity project.</span></span> <span data-ttu-id="42b4e-108">Photon est l’une des nombreuses options de mise en réseau accessibles aux développeurs de réalité mixte pour créer des expériences partagées.</span><span class="sxs-lookup"><span data-stu-id="42b4e-108">Photon is one of several networking options available to Mixed Reality developers to create shared experiences.</span></span> <span data-ttu-id="42b4e-109">Vous allez découvrir comment créer un compte Photon, importer Photon et créer un serveur local facultatif.</span><span class="sxs-lookup"><span data-stu-id="42b4e-109">You will learn how to create a Photon account, import Photon, and create an optional local server</span></span>

## <a name="objectives"></a><span data-ttu-id="42b4e-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="42b4e-110">Objectives</span></span>

* <span data-ttu-id="42b4e-111">Découvrir comment créer un compte Photon</span><span class="sxs-lookup"><span data-stu-id="42b4e-111">Learn how to create a Photon account</span></span>
* <span data-ttu-id="42b4e-112">Découvrir comment trouver et importer Photon Unity Networking</span><span class="sxs-lookup"><span data-stu-id="42b4e-112">Learn how to find and import Photon Unity Networking</span></span>
* <span data-ttu-id="42b4e-113">Configurer un serveur Photon local</span><span class="sxs-lookup"><span data-stu-id="42b4e-113">Set up a local Photon server</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42b4e-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="42b4e-114">Prerequisites</span></span>

>[!TIP]
><span data-ttu-id="42b4e-115">Si vous n’avez pas encore effectué les [tutoriels de démarrage](mrlearning-base.md) et les [tutoriels sur les ancres spatiales Azure](mrlearning-asa-ch1.md), nous vous conseillons de le faire avant d’aller plus loin.</span><span class="sxs-lookup"><span data-stu-id="42b4e-115">If you have not completed the [Getting started tutorials](mrlearning-base.md) and [Azure Spatial Anchors started tutorials](mrlearning-asa-ch1.md) tutorial series yet, it's recommended that you complete those tutorials first.</span></span>

* <span data-ttu-id="42b4e-116">PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="42b4e-116">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="42b4e-117">SDK Windows 10 (10.0.18362.0 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="42b4e-117">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="42b4e-118">Capacité de programmation C# de base</span><span class="sxs-lookup"><span data-stu-id="42b4e-118">Some basic C# programming ability</span></span>
* <span data-ttu-id="42b4e-119">Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)</span><span class="sxs-lookup"><span data-stu-id="42b4e-119">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="42b4e-120">La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X.</span><span class="sxs-lookup"><span data-stu-id="42b4e-120">The recommended Unity version for this tutorial series is Unity 2019.2.X.</span></span> <span data-ttu-id="42b4e-121">Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="42b4e-121">This supersedes any Unity version requirements or recommendations stated in the prerequisites linked above.</span></span>

## <a name="setting-up-photon"></a><span data-ttu-id="42b4e-122">Configuration de Photon</span><span class="sxs-lookup"><span data-stu-id="42b4e-122">Setting up Photon</span></span>

1. <span data-ttu-id="42b4e-123">Configurez un compte [Photon](https://dashboard.photonengine.com//Account/SignUp).</span><span class="sxs-lookup"><span data-stu-id="42b4e-123">Set up a [Photon](https://dashboard.photonengine.com//Account/SignUp) account.</span></span> <span data-ttu-id="42b4e-124">Cliquez sur [ce lien](https://dashboard.photonengine.com//Account/SignUp) pour accéder à la page d’inscription à Photon.</span><span class="sxs-lookup"><span data-stu-id="42b4e-124">Navigate to the Photon Sign-up page by clicking on [this link](https://dashboard.photonengine.com//Account/SignUp).</span></span> <span data-ttu-id="42b4e-125">Suivez les instructions de la page d’inscription pour créer le compte.</span><span class="sxs-lookup"><span data-stu-id="42b4e-125">Follow the instructions on the sign-up page to create the account.</span></span>

    ![Module3Chapter1step1im](images/module3chapter1step1im.PNG)

    ![Module3Chapter1step6im](images/module3chapter1step6im.PNG)

2. <span data-ttu-id="42b4e-128">Cliquez sur le bouton Create a New App pour créer un ID d’application.</span><span class="sxs-lookup"><span data-stu-id="42b4e-128">Create an application ID by clicking the Create a New App button.</span></span>

    ![Module3Chapter1step7aim](images/module3chapter1step7aim.PNG)

3. <span data-ttu-id="42b4e-130">Sélectionnez Photon PUN dans le menu déroulant sous Photon Type.</span><span class="sxs-lookup"><span data-stu-id="42b4e-130">Select Photon PUN from the dropdown menu under Photon Type.</span></span> <span data-ttu-id="42b4e-131">Nommez ensuite l’application.</span><span class="sxs-lookup"><span data-stu-id="42b4e-131">Then give it a name.</span></span> <span data-ttu-id="42b4e-132">Dans cet exemple, nous la nommons HoloLensPhotonProject.</span><span class="sxs-lookup"><span data-stu-id="42b4e-132">In this example, we named it HoloLensPhotonProject.</span></span> <span data-ttu-id="42b4e-133">Quand vous avez terminé, cliquez sur le bouton Create.</span><span class="sxs-lookup"><span data-stu-id="42b4e-133">Once finished, click the Create button.</span></span>

    ![Module3Chapter1step7bim](images/module3chapter1step7bim.PNG)

4. <span data-ttu-id="42b4e-135">Revenez à la page des applications. Vous devriez voir quelque chose de semblable à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="42b4e-135">Return to your applications page and you should see something similar to the picture below.</span></span> <span data-ttu-id="42b4e-136">Cliquez sur l’ID d’application et copiez-le.</span><span class="sxs-lookup"><span data-stu-id="42b4e-136">Click the application ID and copy it.</span></span> <span data-ttu-id="42b4e-137">Collez-le dans un endroit facilement accessible.</span><span class="sxs-lookup"><span data-stu-id="42b4e-137">Paste it somewhere you can easily access.</span></span>  

    ![Module3Chapter1step8im](images/module3chapter1step8im.PNG)

5. <span data-ttu-id="42b4e-139">Créez un projet Unity et nommez-le HLSharingProject.</span><span class="sxs-lookup"><span data-stu-id="42b4e-139">Create a new unity project and name it HLSharingProject.</span></span> <span data-ttu-id="42b4e-140">Pour obtenir des instructions sur la création d’un projet Unity, consultez la [section « Créer un projet Unity » du module de base](https://docs.microsoft.com//windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project).</span><span class="sxs-lookup"><span data-stu-id="42b4e-140">For instructions on how to create a new Unity project, please refer to [the Base Module's "Create Unity Project" section](https://docs.microsoft.com//windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project).</span></span> 

6. <span data-ttu-id="42b4e-141">Une fois le projet chargé, cliquez sur l’onglet Assets Store, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="42b4e-141">Once the project loads, click the Assets Store tab, as shown in the image below.</span></span> <span data-ttu-id="42b4e-142">Ensuite, dans la zone de recherche mise en évidence dans l’image ci-dessous, tapez PUN, puis sélectionnez la ressource Photon « PUN 2 - FREE » dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="42b4e-142">Then, in the search box highlighted in the image below, type in PUN, and select the Photon PUN 2 - FREE" asset from the search results.</span></span>

    ![Module3Chapter1step10im](images/module3chapter1step10im.PNG)

7. <span data-ttu-id="42b4e-144">Téléchargez et importez cette ressource en appuyant sur les boutons Download et Import.</span><span class="sxs-lookup"><span data-stu-id="42b4e-144">Download and import this asset by pressing the Download and Import buttons.</span></span>

    ![Module3Chapter1step11im](images/module3chapter1step11im.PNG)

8. <span data-ttu-id="42b4e-146">Une fois que Photon a terminé le processus d’importation, l’Assistant PUN apparaît.</span><span class="sxs-lookup"><span data-stu-id="42b4e-146">Once Photon has completed the importing process, the Pun Wizard appears.</span></span> <span data-ttu-id="42b4e-147">Collez l’ID d’application (que vous avez copié dans votre Presse-papiers à l’étape 4) dans la zone AppID, puis appuyez sur le bouton Setup Project.</span><span class="sxs-lookup"><span data-stu-id="42b4e-147">Take the application ID (which should be in your clipboard) from step 4, paste it into the AppID box, and press the Setup Project button.</span></span>

    ![module3chapter1step12im](images/module3chapter1step12im.PNG)

9. <span data-ttu-id="42b4e-149">Une fois l’AppID ajouté, accédez à Photon > PhotonUnityNetworking > Resources > PhotonServerSettings dans Assets.</span><span class="sxs-lookup"><span data-stu-id="42b4e-149">After successfully adding the AppID, navigate to Photon->PhotonUnityNetworking ->Resources->PhotonServerSettings in Assets.</span></span> <span data-ttu-id="42b4e-150">Sélectionnez l’option Use Name Server, puis sélectionnez US ou la région de votre service Photon en regard de Fixed Region.</span><span class="sxs-lookup"><span data-stu-id="42b4e-150">Select the Use Name Server option, and set the fixed region to US or your photon service region.</span></span>

    ![module3chapter1step13im](images/module3chapter1step13im.PNG)

## <a name="congratulations"></a><span data-ttu-id="42b4e-152">Félicitations</span><span class="sxs-lookup"><span data-stu-id="42b4e-152">Congratulations</span></span>

<span data-ttu-id="42b4e-153">Vous venez de créer un compte Photon, de configurer un serveur Photon local et d’importer PUN dans Unity.</span><span class="sxs-lookup"><span data-stu-id="42b4e-153">You have successfully created a Photon account, set up a local Photon server, and imported PUN into Unity.</span></span> <span data-ttu-id="42b4e-154">Vous allez à présent configurer le projet et autoriser les connexions avec d’autres utilisateurs pour qu’ils puissent voir votre travail.</span><span class="sxs-lookup"><span data-stu-id="42b4e-154">Your next step is to set up the project and allow connections with other users so that multiple users can see your work.</span></span>

<span data-ttu-id="42b4e-155">[Tutoriel suivant : 2. Préparation de Unity pour le développement](mrlearning-sharing(photon)-ch2.md)</span><span class="sxs-lookup"><span data-stu-id="42b4e-155">[Next tutorial: 2. Getting Unity ready for development](mrlearning-sharing(photon)-ch2.md)</span></span>
