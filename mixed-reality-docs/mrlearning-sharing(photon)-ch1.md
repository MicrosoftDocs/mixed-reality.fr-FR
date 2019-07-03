---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 80cefb36ec1944ec6f537aafcbf4b63f7f812d26
ms.sourcegitcommit: cf9f8ebbca0301e9d277853771ff6e47701ba1c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67523300"
---
#  <a name="setting-up-photon-unity-networking"></a><span data-ttu-id="0ac73-104">Configuration de mise en réseau de Unity Photon</span><span class="sxs-lookup"><span data-stu-id="0ac73-104">Setting up Photon Unity Networking</span></span>

<span data-ttu-id="0ac73-105">Dans ce didacticiel, nous comment se préparer pour la création d’une expérience partagée par l’importation de la mise en réseau de Unity Photon (a) dans votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="0ac73-105">In this tutorial, we learn how to get ready for creating a shared experience by importing Photon Unity Networking (PUN) into your Unity project.</span></span> <span data-ttu-id="0ac73-106">Photon est une des options de mise en réseau plusieurs qui permettent aux développeurs de réalité mixte pour créer des expériences partagées.</span><span class="sxs-lookup"><span data-stu-id="0ac73-106">Photon is one of several networking options available to Mixed Reality developers to create shared experiences.</span></span> <span data-ttu-id="0ac73-107">Nous nous allez apprendre à créer un compte de Photon, importer Photon et créer un serveur local facultatif</span><span class="sxs-lookup"><span data-stu-id="0ac73-107">We we will learn how to create a Photon account, import Photon, and create an optional local server</span></span>

<span data-ttu-id="0ac73-108">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="0ac73-108">Objectives:</span></span>

* <span data-ttu-id="0ac73-109">Découvrez comment créer un compte de Photon</span><span class="sxs-lookup"><span data-stu-id="0ac73-109">Learn how to create a Photon account</span></span>

* <span data-ttu-id="0ac73-110">Découvrez comment rechercher et importer Unity de Photon mise en réseau</span><span class="sxs-lookup"><span data-stu-id="0ac73-110">Learn how to find and import Photon Unity Networking</span></span>

* <span data-ttu-id="0ac73-111">Configurer un serveur local de Photon</span><span class="sxs-lookup"><span data-stu-id="0ac73-111">Set up a local Photon server</span></span>

  

### <a name="setting-up-photon"></a><span data-ttu-id="0ac73-112">Configuration de Photon</span><span class="sxs-lookup"><span data-stu-id="0ac73-112">Setting up Photon</span></span>

1. <span data-ttu-id="0ac73-113">Configurer un [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) compte.</span><span class="sxs-lookup"><span data-stu-id="0ac73-113">Set up a [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) account.</span></span> <span data-ttu-id="0ac73-114">Accédez à la page d’inscription Photon en cliquant sur [ce lien](https://dashboard.photonengine.com/en-US/Account/SignUp).</span><span class="sxs-lookup"><span data-stu-id="0ac73-114">Navigate to the Photon Sign-up page by clicking on [this link](https://dashboard.photonengine.com/en-US/Account/SignUp).</span></span> <span data-ttu-id="0ac73-115">Suivez les instructions sur la page d’inscription pour créer le compte.</span><span class="sxs-lookup"><span data-stu-id="0ac73-115">Follow the instructions on the sign-up page to create the account.</span></span> 
   

![Module3Chapter1step1im](images/module3chapter1step1im.PNG)



![Module3Chapter1step6im](images/module3chapter1step6im.PNG)

2. <span data-ttu-id="0ac73-118">Créer un ID d’application en cliquant sur Créer un bouton de la nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="0ac73-118">Create an application ID by clicking the Create a New App button.</span></span>

![Module3Chapter1step7aim](images/module3chapter1step7aim.PNG)

3. <span data-ttu-id="0ac73-120">Sélectionnez ce jeu de Photon dans le menu déroulant sous Type de Photon.</span><span class="sxs-lookup"><span data-stu-id="0ac73-120">Select Photon PUN from the dropdown menu under Photon Type.</span></span> <span data-ttu-id="0ac73-121">Ensuite, donnez-lui un nom.</span><span class="sxs-lookup"><span data-stu-id="0ac73-121">Then give it a name.</span></span> <span data-ttu-id="0ac73-122">Dans cet exemple, nous l’avons appelé HoloLensPhotonProject.</span><span class="sxs-lookup"><span data-stu-id="0ac73-122">In this example, we named it HoloLensPhotonProject.</span></span> <span data-ttu-id="0ac73-123">Une fois que vous avez terminé, cliquez sur le bouton Créer.</span><span class="sxs-lookup"><span data-stu-id="0ac73-123">Once finished, click the Create button.</span></span>

![Module3Chapter1step7bim](images/module3chapter1step7bim.PNG)

4. <span data-ttu-id="0ac73-125">Une fois cette opération effectuée, revenez à la page de vos applications et vous devriez voir quelque chose de similaire à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0ac73-125">Once that is done, return to your applications page and you should see something similar to the picture below.</span></span> <span data-ttu-id="0ac73-126">Cliquez sur l’ID d’application et copiez-la.</span><span class="sxs-lookup"><span data-stu-id="0ac73-126">Click on the application ID and copy it.</span></span> <span data-ttu-id="0ac73-127">Coller est dans un endroit que facilement accessible.</span><span class="sxs-lookup"><span data-stu-id="0ac73-127">Paste is somewhere you can easily access.</span></span>  

![Module3Chapter1step8im](images/module3chapter1step8im.PNG)

5. <span data-ttu-id="0ac73-129">Créez un projet unity et nommez-le HLSharingProject.</span><span class="sxs-lookup"><span data-stu-id="0ac73-129">Create a new unity project and name it HLSharingProject.</span></span> <span data-ttu-id="0ac73-130">Pour obtenir des instructions sur la création d’un projet Unity, reportez-vous à [section de « Créer un projet Unity » du Module de Base](https://docs.microsoft.com/en-us/windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project).</span><span class="sxs-lookup"><span data-stu-id="0ac73-130">For instructions on how to create a new Unity project, please refer to [the Base Module's "Create Unity Project" section](https://docs.microsoft.com/en-us/windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project).</span></span> 

6. <span data-ttu-id="0ac73-131">Une fois que le projet se charge, cliquez sur l’onglet ressources Store, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0ac73-131">Once the project loads, click on the Assets Store tab, as shown in the image below.</span></span> <span data-ttu-id="0ac73-132">Ressource puis, dans la zone de recherche en surbrillance dans l’image ci-dessous, tapez dans le jeu de mots, sélectionnez le 2 de ce jeu de Photon - FRE » dans les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="0ac73-132">Then, in the search box highlighted in the image below, type in PUN, and select the Photon PUN 2 - FRE" asset from the search results.</span></span> 

![Module3Chapter1step10im](images/module3chapter1step10im.PNG)

7. <span data-ttu-id="0ac73-134">Télécharger et importer cette ressource en appuyant sur les boutons de téléchargement et importation.</span><span class="sxs-lookup"><span data-stu-id="0ac73-134">Download and import this asset by pressing the Download and Import buttons.</span></span>

![Module3Chapter1step11im](images/module3chapter1step11im.PNG)

8. <span data-ttu-id="0ac73-136">Une fois Photon a terminé le processus d’importation, l’Assistant a s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0ac73-136">Once Photon has completed the importing process, the Pun Wizard appears.</span></span> <span data-ttu-id="0ac73-137">Prend l’ID d’application (qui doit être dans le Presse-papiers) à partir de l’étape 4 et collez-la dans la zone AppID, appuyez sur le bouton de projet d’installation.</span><span class="sxs-lookup"><span data-stu-id="0ac73-137">Take the application ID (which should be in your clipboard) from step 4, and paste it into the AppID box, and press the Setup Project button.</span></span> 
<span data-ttu-id="0ac73-138">![module3chapter1step12im](images/module3chapter1step12im.PNG)</span><span class="sxs-lookup"><span data-stu-id="0ac73-138">![module3chapter1step12im](images/module3chapter1step12im.PNG)</span></span>

9. <span data-ttu-id="0ac73-139">Après avoir ajouté avec succès l’AppID, accédez à Photon -> PhotonUnityNetworking -> ressources -> PhotonServerSettings d’actifs.</span><span class="sxs-lookup"><span data-stu-id="0ac73-139">After successfully adding the AppID, navigate to Photon->PhotonUnityNetworking ->Resources->PhotonServerSettings in Assets.</span></span> <span data-ttu-id="0ac73-140">Sélectionnez l’option utiliser le nom du serveur et définir la région fixe nous ou service yourPphoton.</span><span class="sxs-lookup"><span data-stu-id="0ac73-140">Select the Use Name Server option, and set the fixed region to US or yourPphoton service region.</span></span>

   ![module3chapter1step13im](images/module3chapter1step13im.PNG)

## <a name="congratulations"></a><span data-ttu-id="0ac73-142">Félicitations</span><span class="sxs-lookup"><span data-stu-id="0ac73-142">Congratulations</span></span>

<span data-ttu-id="0ac73-143">Vous avez correctement créé un compte de Photon configurer un serveur local de Photon et importé ce jeu dans Unity.</span><span class="sxs-lookup"><span data-stu-id="0ac73-143">You have successfully created a Photon account, set up a local Photon server, and imported PUN into Unity.</span></span> <span data-ttu-id="0ac73-144">L’étape suivante consiste à configurer le projet et ensuite autoriser les connexions avec d’autres utilisateurs afin que plusieurs utilisateurs puissent voir votre travail.</span><span class="sxs-lookup"><span data-stu-id="0ac73-144">Your next step is to set up the project and then allow connections with other users so that multiple users can see your work.</span></span> 

<span data-ttu-id="0ac73-145">[Didacticiel suivant : Préparation de Unity pour le développement](mrlearning-sharing(photon)-ch2.md)</span><span class="sxs-lookup"><span data-stu-id="0ac73-145">[Next tutorial: Getting Unity ready for development](mrlearning-sharing(photon)-ch2.md)</span></span>

