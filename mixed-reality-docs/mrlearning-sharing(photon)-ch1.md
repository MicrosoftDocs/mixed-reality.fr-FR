---
title: Didacticiels sur les fonctionnalités multi-utilisateur-1. Configuration de la mise en réseau photonique Unity
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: acb6966ace81180e95e6a0fe447d350572f7c0dd
ms.sourcegitcommit: af1602710c1ccb7ed870a491923350d387706129
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68701973"
---
#  <a name="1-setting-up-photon-unity-networking"></a><span data-ttu-id="a750a-105">1. Configuration de la mise en réseau photonique Unity</span><span class="sxs-lookup"><span data-stu-id="a750a-105">1. Setting up Photon Unity Networking</span></span>

<span data-ttu-id="a750a-106">Dans ce didacticiel, nous allons apprendre à vous préparer à la création d’une expérience partagée en important la mise en réseau de photons Unity (retentissante) dans votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="a750a-106">In this tutorial, we learn how to get ready for creating a shared experience by importing Photon Unity Networking (PUN) into your Unity project.</span></span> <span data-ttu-id="a750a-107">Photons est l’une des nombreuses options de mise en réseau disponibles pour les développeurs de réalité mixte pour créer des expériences partagées.</span><span class="sxs-lookup"><span data-stu-id="a750a-107">Photon is one of several networking options available to Mixed Reality developers to create shared experiences.</span></span> <span data-ttu-id="a750a-108">Nous allons apprendre à créer un compte de photons, à importer une photons et à créer un serveur local facultatif</span><span class="sxs-lookup"><span data-stu-id="a750a-108">We we will learn how to create a Photon account, import Photon, and create an optional local server</span></span>

## <a name="objectives"></a><span data-ttu-id="a750a-109">Objectifs</span><span class="sxs-lookup"><span data-stu-id="a750a-109">Objectives</span></span>

* <span data-ttu-id="a750a-110">Découvrez comment créer un compte de photons</span><span class="sxs-lookup"><span data-stu-id="a750a-110">Learn how to create a Photon account</span></span>

* <span data-ttu-id="a750a-111">Découvrez comment rechercher et importer une mise en réseau photonique Unity</span><span class="sxs-lookup"><span data-stu-id="a750a-111">Learn how to find and import Photon Unity Networking</span></span>

* <span data-ttu-id="a750a-112">Configurer un serveur de photons local</span><span class="sxs-lookup"><span data-stu-id="a750a-112">Set up a local Photon server</span></span>

  

## <a name="setting-up-photon"></a><span data-ttu-id="a750a-113">Configuration de photons</span><span class="sxs-lookup"><span data-stu-id="a750a-113">Setting up Photon</span></span>

1. <span data-ttu-id="a750a-114">Configurez un compte de [photons](https://dashboard.photonengine.com/en-US/Account/SignUp) .</span><span class="sxs-lookup"><span data-stu-id="a750a-114">Set up a [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) account.</span></span> <span data-ttu-id="a750a-115">Accédez à la page d’inscription à photons en cliquant sur [ce lien](https://dashboard.photonengine.com/en-US/Account/SignUp).</span><span class="sxs-lookup"><span data-stu-id="a750a-115">Navigate to the Photon Sign-up page by clicking on [this link](https://dashboard.photonengine.com/en-US/Account/SignUp).</span></span> <span data-ttu-id="a750a-116">Suivez les instructions de la page d’inscription pour créer le compte.</span><span class="sxs-lookup"><span data-stu-id="a750a-116">Follow the instructions on the sign-up page to create the account.</span></span> 
   

![Module3Chapter1step1im](images/module3chapter1step1im.PNG)

![Module3Chapter1step6im](images/module3chapter1step6im.PNG)

2. <span data-ttu-id="a750a-119">Créez un ID d’application en cliquant sur le bouton créer une application.</span><span class="sxs-lookup"><span data-stu-id="a750a-119">Create an application ID by clicking the Create a New App button.</span></span>

![Module3Chapter1step7aim](images/module3chapter1step7aim.PNG)

3. <span data-ttu-id="a750a-121">Sélectionnez photons retentissante dans le menu déroulant sous type de photons.</span><span class="sxs-lookup"><span data-stu-id="a750a-121">Select Photon PUN from the dropdown menu under Photon Type.</span></span> <span data-ttu-id="a750a-122">Donnez-lui un nom.</span><span class="sxs-lookup"><span data-stu-id="a750a-122">Then give it a name.</span></span> <span data-ttu-id="a750a-123">Dans cet exemple, nous avons nommé IT HoloLensPhotonProject.</span><span class="sxs-lookup"><span data-stu-id="a750a-123">In this example, we named it HoloLensPhotonProject.</span></span> <span data-ttu-id="a750a-124">Une fois terminé, cliquez sur le bouton créer.</span><span class="sxs-lookup"><span data-stu-id="a750a-124">Once finished, click the Create button.</span></span>

![Module3Chapter1step7bim](images/module3chapter1step7bim.PNG)

4. <span data-ttu-id="a750a-126">Une fois cette opération effectuée, revenez à la page de votre application et vous devriez voir une image semblable à celle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a750a-126">Once that is done, return to your applications page and you should see something similar to the picture below.</span></span> <span data-ttu-id="a750a-127">Cliquez sur l’ID d’application et copiez-le.</span><span class="sxs-lookup"><span data-stu-id="a750a-127">Click on the application ID and copy it.</span></span> <span data-ttu-id="a750a-128">Collez-la quelque part pour y accéder facilement.</span><span class="sxs-lookup"><span data-stu-id="a750a-128">Paste it somewhere you can easily access.</span></span>  

![Module3Chapter1step8im](images/module3chapter1step8im.PNG)

5. <span data-ttu-id="a750a-130">Créez un nouveau projet Unity et nommez-le HLSharingProject.</span><span class="sxs-lookup"><span data-stu-id="a750a-130">Create a new unity project and name it HLSharingProject.</span></span> <span data-ttu-id="a750a-131">Pour obtenir des instructions sur la création d’un nouveau projet Unity, reportez-vous à [la section «créer un projet Unity» du module de base](https://docs.microsoft.com/en-us/windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project).</span><span class="sxs-lookup"><span data-stu-id="a750a-131">For instructions on how to create a new Unity project, please refer to [the Base Module's "Create Unity Project" section](https://docs.microsoft.com/en-us/windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project).</span></span> 

6. <span data-ttu-id="a750a-132">Une fois le projet chargé, cliquez sur l’onglet stockage des ressources, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a750a-132">Once the project loads, click on the Assets Store tab, as shown in the image below.</span></span> <span data-ttu-id="a750a-133">Ensuite, dans la zone de recherche mise en surbrillance dans l’image ci-dessous, tapez retentissante, puis sélectionnez la ressource photon retentissante 2-FREE» dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="a750a-133">Then, in the search box highlighted in the image below, type in PUN, and select the Photon PUN 2 - FREE" asset from the search results.</span></span> 

![Module3Chapter1step10im](images/module3chapter1step10im.PNG)

7. <span data-ttu-id="a750a-135">Téléchargez et importez cette ressource en appuyant sur les boutons télécharger et importer.</span><span class="sxs-lookup"><span data-stu-id="a750a-135">Download and import this asset by pressing the Download and Import buttons.</span></span>

![Module3Chapter1step11im](images/module3chapter1step11im.PNG)

8. <span data-ttu-id="a750a-137">Une fois que photon a terminé le processus d’importation, l’Assistant retentissante s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a750a-137">Once Photon has completed the importing process, the Pun Wizard appears.</span></span> <span data-ttu-id="a750a-138">Prenez l’ID d’application (qui doit se trouver dans le presse-papiers) de l’étape 4 et collez-le dans la zone AppID, puis appuyez sur le bouton du projet d’installation.</span><span class="sxs-lookup"><span data-stu-id="a750a-138">Take the application ID (which should be in your clipboard) from step 4, and paste it into the AppID box, and press the Setup Project button.</span></span> 
<span data-ttu-id="a750a-139">![module3chapter1step12im](images/module3chapter1step12im.PNG)</span><span class="sxs-lookup"><span data-stu-id="a750a-139">![module3chapter1step12im](images/module3chapter1step12im.PNG)</span></span>

9. <span data-ttu-id="a750a-140">Après avoir ajouté avec succès l’AppID, accédez à photons-> PhotonUnityNetworking-> Ressources-> PhotonServerSettings dans ressources.</span><span class="sxs-lookup"><span data-stu-id="a750a-140">After successfully adding the AppID, navigate to Photon->PhotonUnityNetworking ->Resources->PhotonServerSettings in Assets.</span></span> <span data-ttu-id="a750a-141">Sélectionnez l’option utiliser le serveur de noms, puis définissez la région fixe sur US ou votre région de service de photons.</span><span class="sxs-lookup"><span data-stu-id="a750a-141">Select the Use Name Server option, and set the fixed region to US or your photon service region.</span></span>

![module3chapter1step13im](images/module3chapter1step13im.PNG)

## <a name="congratulations"></a><span data-ttu-id="a750a-143">Félicitations</span><span class="sxs-lookup"><span data-stu-id="a750a-143">Congratulations</span></span>

<span data-ttu-id="a750a-144">Vous venez de créer un compte de photons, de configurer un serveur de photons local et d’importer des retentissante dans Unity.</span><span class="sxs-lookup"><span data-stu-id="a750a-144">You have successfully created a Photon account, set up a local Photon server, and imported PUN into Unity.</span></span> <span data-ttu-id="a750a-145">L’étape suivante consiste à configurer le projet, puis à autoriser les connexions avec d’autres utilisateurs afin que plusieurs utilisateurs puissent voir votre travail.</span><span class="sxs-lookup"><span data-stu-id="a750a-145">Your next step is to set up the project and then allow connections with other users so that multiple users can see your work.</span></span> 

<span data-ttu-id="a750a-146">[Didacticiel suivant: 2. Préparation de Unity pour le développement](mrlearning-sharing(photon)-ch2.md)</span><span class="sxs-lookup"><span data-stu-id="a750a-146">[Next tutorial: 2. Getting Unity ready for development](mrlearning-sharing(photon)-ch2.md)</span></span>

