---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: f612fa89db1a3f5ed34f6e0bb7062b53780f09b8
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67416120"
---
# <a name="setting-up-photon"></a><span data-ttu-id="ae2a4-104">Configuration de Photon</span><span class="sxs-lookup"><span data-stu-id="ae2a4-104">Setting Up Photon</span></span>

<span data-ttu-id="ae2a4-105">Dans cette leçon, nous allez apprendre à se préparer pour la création d’une expérience partagée par l’importation de la mise en réseau de Unity Photon (a) dans votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-105">In this lesson, we will learn how to get ready for creating a shared experience by importing Photon Unity Networking (PUN) into your Unity project.</span></span> <span data-ttu-id="ae2a4-106">Photon est une des options de mise en réseau plusieurs qui permettent aux développeurs de réalité mixte pour créer des expériences partagées.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-106">Photon is one of several networking options available to Mixed Reality developers to create shared experiences.</span></span> <span data-ttu-id="ae2a4-107">Nous nous allez apprendre à créer un compte de Photon, importer Photon et créer un serveur local facultatif</span><span class="sxs-lookup"><span data-stu-id="ae2a4-107">We we will learn how to create a Photon account, import Photon, and create an optional local server</span></span>

<span data-ttu-id="ae2a4-108">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="ae2a4-108">Objectives:</span></span>

* <span data-ttu-id="ae2a4-109">Apprenez à créer le compte de Photon</span><span class="sxs-lookup"><span data-stu-id="ae2a4-109">Learn how to create Photon account</span></span>

* <span data-ttu-id="ae2a4-110">Découvrez comment rechercher et importer Unity de Photon mise en réseau</span><span class="sxs-lookup"><span data-stu-id="ae2a4-110">Learn how to find and import Photon Unity Networking</span></span>

* <span data-ttu-id="ae2a4-111">Configurer un serveur local de Photon</span><span class="sxs-lookup"><span data-stu-id="ae2a4-111">Set up a local Photon server</span></span>

  

### <a name="setting-up-photon"></a><span data-ttu-id="ae2a4-112">Configuration de Photon</span><span class="sxs-lookup"><span data-stu-id="ae2a4-112">Setting Up Photon</span></span>

1. <span data-ttu-id="ae2a4-113">Configurer un [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) compte.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-113">Set up a [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) account.</span></span> <span data-ttu-id="ae2a4-114">Accédez à la page d’inscription Photon en cliquant sur [ce lien](https://dashboard.photonengine.com/en-US/Account/SignUp).</span><span class="sxs-lookup"><span data-stu-id="ae2a4-114">Navigate to the Photon Sign-up page by clicking on [this link](https://dashboard.photonengine.com/en-US/Account/SignUp).</span></span> <span data-ttu-id="ae2a4-115">Suivez les instructions sur la page d’inscription pour créer le compte.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-115">Follow the instructions on the sign-up page to create the account.</span></span> 
   

![Module3Chapter1step1im](images/module3chapter1step1im.PNG)



![Module3Chapter1step6im](images/module3chapter1step6im.PNG)

2. <span data-ttu-id="ae2a4-118">Créer un ID d’application en cliquant sur le bouton « Créer une nouvelle application ».</span><span class="sxs-lookup"><span data-stu-id="ae2a4-118">Create an application ID by clicking the "create a new app" button.</span></span>

![Module3Chapter1step7aim](images/module3chapter1step7aim.PNG)

3. <span data-ttu-id="ae2a4-120">Sélectionnez « Photon a » dans le menu déroulant sous « type photon. »</span><span class="sxs-lookup"><span data-stu-id="ae2a4-120">Select "Photon PUN" from the dropdown menu under "photon type."</span></span> <span data-ttu-id="ae2a4-121">Puis donnez-lui un nom, dans cet exemple, nous l’avons appelé « HoloLensPhotonProject ».</span><span class="sxs-lookup"><span data-stu-id="ae2a4-121">Then give it a name, in this example, we named it "HoloLensPhotonProject."</span></span> <span data-ttu-id="ae2a4-122">Une fois que vous avez terminé, cliquez sur le bouton « Créer ».</span><span class="sxs-lookup"><span data-stu-id="ae2a4-122">Once finished, click the "CREATE" button.</span></span>

![Module3Chapter1step7bim](images/module3chapter1step7bim.PNG)

4. <span data-ttu-id="ae2a4-124">Une fois cette opération effectuée, revenez à la page de vos applications et vous devriez voir quelque chose de similaire à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-124">Once that is done, return to your applications page and you should see something similar to the picture below.</span></span> <span data-ttu-id="ae2a4-125">Cliquez sur l’ID d’application et copiez-la.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-125">Click on the app ID and copy it.</span></span> <span data-ttu-id="ae2a4-126">Coller est dans un endroit que facilement accessible.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-126">Paste is somewhere you can easily access.</span></span>  

![Module3Chapter1step8im](images/module3chapter1step8im.PNG)

5. <span data-ttu-id="ae2a4-128">Créez un projet unity et nommez-le « HLSharingProject. »</span><span class="sxs-lookup"><span data-stu-id="ae2a4-128">Create a new unity project and name it "HLSharingProject."</span></span> <span data-ttu-id="ae2a4-129">Pour obtenir des instructions sur la création d’un projet Unity, reportez-vous à [section de « Créer un projet Unity » du Module de Base](https://docs.microsoft.com/en-us/windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project).</span><span class="sxs-lookup"><span data-stu-id="ae2a4-129">For instructions on how to create a new Unity project, please refer to [the Base Module's "Create Unity Project" section](https://docs.microsoft.com/en-us/windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project).</span></span> 

6. <span data-ttu-id="ae2a4-130">Une fois que le projet se charge, cliquez sur l’onglet « ressources store », comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-130">Once the project loads, click on the "assets store" tab, as shown in the image below.</span></span> <span data-ttu-id="ae2a4-131">Puis, dans la zone de recherche en surbrillance dans l’image ci-dessous, tapez « A » et sélectionnez la ressource « Photon a 2 - libre » dans les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-131">Then, in the search box highlighted in the image below, type in "PUN" and select the "Photon PUN 2 - FREE" asset from the search results.</span></span> 

![Module3Chapter1step10im](images/module3chapter1step10im.PNG)

7. <span data-ttu-id="ae2a4-133">Télécharger et importer cette ressource en appuyant sur les boutons « Télécharger » et « Importer ».</span><span class="sxs-lookup"><span data-stu-id="ae2a4-133">Download and import this asset by pressing the "Download" and "Import" buttons.</span></span>

![Module3Chapter1step11im](images/module3chapter1step11im.PNG)

8. <span data-ttu-id="ae2a4-135">Une fois Photon a terminé le processus d’importation, l’Assistant a s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-135">Once Photon has completed the importing process, the Pun Wizard will appear.</span></span> <span data-ttu-id="ae2a4-136">Prendre l’ID d’application (qui doit être dans le Presse-papiers) à partir de l’étape 4 et collez-la dans la zone AppID et appuyez sur le bouton « Le programme d’installation de projet ».</span><span class="sxs-lookup"><span data-stu-id="ae2a4-136">Take the application ID (which should be in your clipboard) from step 4 and paste it into the AppID box and press the "Setup Project" button.</span></span> 
<span data-ttu-id="ae2a4-137">![module3chapter1step12im](images/module3chapter1step12im.PNG)</span><span class="sxs-lookup"><span data-stu-id="ae2a4-137">![module3chapter1step12im](images/module3chapter1step12im.PNG)</span></span>

9. <span data-ttu-id="ae2a4-138">After successfully adding the AppID, navigate to "Photon"->"PhotonUnityNetworking" -> "Resources" ->  "PhotonServerSettings" in Assets.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-138">After successfully adding the AppID, navigate to "Photon"->"PhotonUnityNetworking" -> "Resources" ->  "PhotonServerSettings" in Assets.</span></span> <span data-ttu-id="ae2a4-139">Sélectionnez l’option « Utiliser le serveur de nom » et la valeur est la région fixe « us » ou votre région de service photon.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-139">Select "Use Name Server" option and set the fixed region to "us" or your photon service region.</span></span>

   ![module3chapter1step13im](images/module3chapter1step13im.PNG)

## <a name="congratulations"></a><span data-ttu-id="ae2a4-141">Félicitations</span><span class="sxs-lookup"><span data-stu-id="ae2a4-141">Congratulations</span></span>

<span data-ttu-id="ae2a4-142">Vous avez correctement créé un compte de Photon configurer un serveur local de Photon et importé ce jeu dans Unity.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-142">You have successfully created a Photon account, set up a local Photon server, and imported PUN into Unity.</span></span> <span data-ttu-id="ae2a4-143">L’étape suivante consiste à configurer le projet et ensuite autoriser les connexions avec d’autres utilisateurs afin que plusieurs utilisateurs puissent voir votre travail.</span><span class="sxs-lookup"><span data-stu-id="ae2a4-143">Your next step is to set up the project and then allow connections with other users so that multiple users can see your work.</span></span> 

<span data-ttu-id="ae2a4-144">[Leçon suivante : Sharing(Photon) leçon 2](mrlearning-sharing(photon)-ch2.md)</span><span class="sxs-lookup"><span data-stu-id="ae2a4-144">[Next Lesson: Sharing(Photon) Lesson 2](mrlearning-sharing(photon)-ch2.md)</span></span>

