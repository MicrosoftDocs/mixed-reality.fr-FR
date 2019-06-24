---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 8940de029ef5c67c38f427a238f88fcab527d79d
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67327910"
---
# <a name="setting-up-photon"></a><span data-ttu-id="cb04d-104">Configuration de Photon</span><span class="sxs-lookup"><span data-stu-id="cb04d-104">Setting Up Photon</span></span>

<span data-ttu-id="cb04d-105">Dans cette leçon, nous allez apprendre à se préparer pour la création d’une expérience partagée par l’importation de la mise en réseau de Unity Photon (a) dans votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="cb04d-105">In this lesson, we will learn how to get ready for creating a shared experience by importing Photon Unity Networking (PUN) into your Unity project.</span></span> <span data-ttu-id="cb04d-106">Photon est une des options de mise en réseau plusieurs qui permettent aux développeurs de réalité mixte pour créer des expériences partagées.</span><span class="sxs-lookup"><span data-stu-id="cb04d-106">Photon is one of several networking options available to Mixed Reality developers to create shared experiences.</span></span> <span data-ttu-id="cb04d-107">Nous nous allez apprendre à créer un compte de Photon, importer Photon et créer un serveur local facultatif</span><span class="sxs-lookup"><span data-stu-id="cb04d-107">We we will learn how to create a Photon account, import Photon, and create an optional local server</span></span>

<span data-ttu-id="cb04d-108">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="cb04d-108">Objectives:</span></span>

* <span data-ttu-id="cb04d-109">Apprenez à créer le compte de Photon</span><span class="sxs-lookup"><span data-stu-id="cb04d-109">Learn how to create Photon account</span></span>

* <span data-ttu-id="cb04d-110">Découvrez comment rechercher et importer Unity de Photon mise en réseau</span><span class="sxs-lookup"><span data-stu-id="cb04d-110">Learn how to find and import Photon Unity Networking</span></span>

* <span data-ttu-id="cb04d-111">Configurer un serveur local de Photon</span><span class="sxs-lookup"><span data-stu-id="cb04d-111">Set up a local Photon server</span></span>

  

### <a name="setting-up-photon"></a><span data-ttu-id="cb04d-112">Configuration de Photon</span><span class="sxs-lookup"><span data-stu-id="cb04d-112">Setting Up Photon</span></span>

1. <span data-ttu-id="cb04d-113">Configurer un [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) compte.</span><span class="sxs-lookup"><span data-stu-id="cb04d-113">Set up a [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) account.</span></span> <span data-ttu-id="cb04d-114">Accédez à la page d’inscription Photon en cliquant sur [ce lien](https://dashboard.photonengine.com/en-US/Account/SignUp).</span><span class="sxs-lookup"><span data-stu-id="cb04d-114">Navigate to the Photon Sign-up page by clicking on [this link](https://dashboard.photonengine.com/en-US/Account/SignUp).</span></span> <span data-ttu-id="cb04d-115">Suivez les instructions sur la page d’inscription pour créer le compte.</span><span class="sxs-lookup"><span data-stu-id="cb04d-115">Follow the instructions on the sign-up page to create the account.</span></span> 
   

![Module3Chapter1step1im](images/module3chapter1step1im.PNG)

2. <span data-ttu-id="cb04d-117">Une fois que vous êtes inscrit, cliquez sur les kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="cb04d-117">Once you are signed up, click on SDKs.</span></span> <span data-ttu-id="cb04d-118">Une fois que vous êtes sur cette page, cliquez sur « server » et vous assurer de l’état est « auto-hébergé. »</span><span class="sxs-lookup"><span data-stu-id="cb04d-118">Once you are on that page, click on "server," and make ensure it says, "self hosted."</span></span> <span data-ttu-id="cb04d-119">Puis faites défiler vers le bas et cliquez sur « server », comme indiqué dans la deuxième image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cb04d-119">Then scroll down and click on "server" as seen in the second image below.</span></span>

   

   ![Module3Chapter1step2aim](images/module3chapter1step2aim.PNG)

   ![Module3Chapter1step2bim](images/module3chapter1step2bim.PNG)
   
   3. <span data-ttu-id="cb04d-122">Si vous le faites étiqueté, une zone de texte « lire me. »</span><span class="sxs-lookup"><span data-stu-id="cb04d-122">That will cause a text box to appear labeled, "read me."</span></span> <span data-ttu-id="cb04d-123">Continuons et le lire.</span><span class="sxs-lookup"><span data-stu-id="cb04d-123">Go ahead and read it.</span></span> <span data-ttu-id="cb04d-124">Une fois que vous avez terminé, cliquez sur le lien en regard de « downloadSDK » afin de le télécharger.</span><span class="sxs-lookup"><span data-stu-id="cb04d-124">Once finished, click on the link next to "downloadSDK" to download it.</span></span>


![Module3Chapter1step3im](images/module3chapter1step3im.PNG)

4. <span data-ttu-id="cb04d-126">Sur le dossier une fois le téléchargement terminé.</span><span class="sxs-lookup"><span data-stu-id="cb04d-126">Double click the folder once it finishes downloading.</span></span>  <span data-ttu-id="cb04d-127">Une fois que l’Explorateur de fichiers s’ouvre, révélant le dossier du Kit de développement logiciel, copiez le dossier SDK.</span><span class="sxs-lookup"><span data-stu-id="cb04d-127">Once your file explorer opens revealing the SDK folder, copy the SDK folder.</span></span>
   
   - <span data-ttu-id="cb04d-128">L’étape suivante consisterait à aller dans le lecteur C: windows et créez un dossier appelé « serveur ».</span><span class="sxs-lookup"><span data-stu-id="cb04d-128">Your next step would be to go into the windows C: drive and create a new folder called 'server.'</span></span>
   
   ![Module3Chapter1step4aim](images/module3chapter1step4aim.PNG)
   
   - <span data-ttu-id="cb04d-130">Ouvrez le dossier et coller le dossier SDK que vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="cb04d-130">Now open up the folder, and paste the SDK folder you copied earlier.</span></span>
   
   ![Module3Chapter1step4bim](images/module3chapter1step4bim.PNG)
   
5. <span data-ttu-id="cb04d-132">Une fois cette opération terminée, ouvrez le dossier SDK et accédez à « déployer », puis « bin_Win64 », et double-cliquez sur « contrôle photon ».</span><span class="sxs-lookup"><span data-stu-id="cb04d-132">Once that is completed, open the SDK folder and go to "deploy," then "bin_Win64," then double click on "photon control."</span></span>


![Module3Chapter1step5im](images/module3chapter1step5im.PNG)

> <span data-ttu-id="cb04d-134">Remarque: Si vous avez des questions sur l’adresse IP ou autres questions similaires, vous trouverez la plupart de vos informations dans la barre d’outils (comme indiqué dans l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="cb04d-134">Note: If you have any questions about IP address, or any other similar questions, you can find most of your information in the toolbar (as shown in the image below).</span></span>
>
> ![Module3Chapter1noteim](images/module3chapter1noteim.PNG)

6. <span data-ttu-id="cb04d-136">Maintenant que le serveur est configuré et lancé, revenez en arrière vers le site Web de Photon et vous assurer que vous êtes toujours connecté (ou vous reconnecter, si vous n’êtes pas). Cliquez sur l’icône de profil (converti (boxed) dans l’angle supérieur droit de l’image ci-dessous) et sélectionnez « vos applications. »</span><span class="sxs-lookup"><span data-stu-id="cb04d-136">Now that the server is set up and initiated, go back to the Photon website and ensure that you are still signed in (or sign back in, if you are not.) Click on the profile icon (boxed in the top right corner of the image below) and select "your applications."</span></span>
   

![Module3Chapter1step6im](images/module3chapter1step6im.PNG)

7. <span data-ttu-id="cb04d-138">Créer un ID d’application en cliquant sur le bouton « Créer une nouvelle application ».</span><span class="sxs-lookup"><span data-stu-id="cb04d-138">Create an application ID by clicking the "create a new app" button.</span></span>

   ![Module3Chapter1step7aim](images/module3chapter1step7aim.PNG)

   - <span data-ttu-id="cb04d-140">Sélectionnez « Photon a » dans le menu déroulant sous « type photon. »</span><span class="sxs-lookup"><span data-stu-id="cb04d-140">Select "Photon PUN" from the dropdown menu under "photon type."</span></span> <span data-ttu-id="cb04d-141">Puis donnez-lui un nom, dans cet exemple, nous l’avons appelé « HoloLensPhotonProject ».</span><span class="sxs-lookup"><span data-stu-id="cb04d-141">Then give it a name, in this example, we named it "HoloLensPhotonProject."</span></span> <span data-ttu-id="cb04d-142">Une fois que vous avez terminé, cliquez sur le bouton « Créer ».</span><span class="sxs-lookup"><span data-stu-id="cb04d-142">Once finished, click the "CREATE" button.</span></span>

   ![Module3Chapter1step7bim](images/module3chapter1step7bim.PNG)

8. <span data-ttu-id="cb04d-144">Une fois cette opération effectuée, revenez à la page de vos applications et vous devriez voir quelque chose de similaire à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cb04d-144">Once that is done, return to your applications page and you should see something similar to the picture below.</span></span> <span data-ttu-id="cb04d-145">Cliquez sur l’ID d’application et copiez-la.</span><span class="sxs-lookup"><span data-stu-id="cb04d-145">Click on the app ID and copy it.</span></span> <span data-ttu-id="cb04d-146">Coller est dans un endroit que facilement accessible.</span><span class="sxs-lookup"><span data-stu-id="cb04d-146">Paste is somewhere you can easily access.</span></span>  
   

![Module3Chapter1step8im](images/module3chapter1step8im.PNG)

9. <span data-ttu-id="cb04d-148">Créez un projet unity et nommez-le « HLSharingProject. »</span><span class="sxs-lookup"><span data-stu-id="cb04d-148">Create a new unity project and name it "HLSharingProject."</span></span> <span data-ttu-id="cb04d-149">Pour obtenir des instructions sur la création d’un projet Unity, reportez-vous à [section de « Créer un projet Unity » du Module de Base](https://docs.microsoft.com/en-us/windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project).</span><span class="sxs-lookup"><span data-stu-id="cb04d-149">For instructions on how to create a new Unity project, please refer to [the Base Module's "Create Unity Project" section](https://docs.microsoft.com/en-us/windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project).</span></span> 


10. <span data-ttu-id="cb04d-150">Une fois que le projet se charge, cliquez sur l’onglet « ressources store », comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cb04d-150">Once the project loads, click on the "assets store" tab, as shown in the image below.</span></span> <span data-ttu-id="cb04d-151">Puis, dans la zone de recherche en surbrillance dans l’image ci-dessous, tapez « A » et sélectionnez la ressource « Photon gratuit a-2 » dans les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="cb04d-151">Then, in the search box highlighted in the image below, type in "PUN" and select the "Photon PUN-2 FREE" asset from the search results.</span></span> 

    ![Module3Chapter1step10im](images/module3chapter1step10im.PNG)
    
    11. <span data-ttu-id="cb04d-153">Télécharger et importer cette ressource en appuyant sur les boutons « Télécharger » et « Importer ».</span><span class="sxs-lookup"><span data-stu-id="cb04d-153">Download and import this asset by pressing the "Download" and "Import" buttons.</span></span>
    
    ![Module3Chapter1step11im](images/module3chapter1step11im.PNG)

## <a name="congratulations"></a><span data-ttu-id="cb04d-155">Félicitations</span><span class="sxs-lookup"><span data-stu-id="cb04d-155">Congratulations</span></span>

<span data-ttu-id="cb04d-156">Vous avez correctement créé un compte de Photon configurer un serveur local de Photon et importé ce jeu dans Unity.</span><span class="sxs-lookup"><span data-stu-id="cb04d-156">You have successfully created a Photon account, set up a local Photon server, and imported PUN into Unity.</span></span> <span data-ttu-id="cb04d-157">L’étape suivante consiste à configurer le projet et ensuite autoriser les connexions avec d’autres utilisateurs afin que plusieurs utilisateurs puissent voir votre travail.</span><span class="sxs-lookup"><span data-stu-id="cb04d-157">Your next step is to set up the project and then allow connections with other users so that multiple users can see your work.</span></span> 

<span data-ttu-id="cb04d-158">[Leçon suivante : Sharing(Photon) leçon 2](mrlearning-sharing(photon)-ch2.md)</span><span class="sxs-lookup"><span data-stu-id="cb04d-158">[Next Lesson: Sharing(Photon) Lesson 2](mrlearning-sharing(photon)-ch2.md)</span></span>

