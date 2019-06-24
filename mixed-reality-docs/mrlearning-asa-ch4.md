---
title: Module MR Learning ASA Azure ancre spatiale sur HoloLens 2
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: b29f27284c352d27fb1d4d4de701a1ebc2a7cd1c
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67327082"
---
# <a name="photon-correct-me-if-im-wrong"></a><span data-ttu-id="7afb8-104">Photon (corriger me si je suis incorrect)</span><span class="sxs-lookup"><span data-stu-id="7afb8-104">Photon (correct me if I'm wrong)</span></span>

<span data-ttu-id="7afb8-105">Dans cette leçon,</span><span class="sxs-lookup"><span data-stu-id="7afb8-105">In this lesson,</span></span> 

<span data-ttu-id="7afb8-106">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="7afb8-106">Objectives:</span></span>

* <span data-ttu-id="7afb8-107">Découvrez comment ___</span><span class="sxs-lookup"><span data-stu-id="7afb8-107">Learn how to _____________________________________________</span></span>

* <span data-ttu-id="7afb8-108">Découvrez comment ___</span><span class="sxs-lookup"><span data-stu-id="7afb8-108">Learn how to _________________________________________________</span></span>

  

## <a name="instructions"></a><span data-ttu-id="7afb8-109">Instructions</span><span class="sxs-lookup"><span data-stu-id="7afb8-109">Instructions</span></span>

### <a name="setting-up-photon"></a><span data-ttu-id="7afb8-110">Configuration de Photon</span><span class="sxs-lookup"><span data-stu-id="7afb8-110">Setting Up Photon</span></span>

1. <span data-ttu-id="7afb8-111">Configurer un [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) compte.</span><span class="sxs-lookup"><span data-stu-id="7afb8-111">Set up a [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) account.</span></span> <span data-ttu-id="7afb8-112">Cette opération sera constitué de saisir votre adresse de messagerie et de passer par certaines étapes de vérification.</span><span class="sxs-lookup"><span data-stu-id="7afb8-112">Doing this will consist of imputing your email and going through some verification steps.</span></span>
   

![Module2Chapter4step1im](images/Module2chapter4step1im.png)

2. <span data-ttu-id="7afb8-114">Une fois que vous êtes inscrit, cliquez sur les kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="7afb8-114">Once you are signed up, click on SDKs.</span></span> <span data-ttu-id="7afb8-115">Une fois que vous êtes sur cette page, cliquez sur « server » et vous assurer de l’état est « auto-hébergé. »</span><span class="sxs-lookup"><span data-stu-id="7afb8-115">Once you are on that page, click on "server," and make ensure it says, "self hosted."</span></span> <span data-ttu-id="7afb8-116">Puis faites défiler vers le bas et cliquez sur « server », comme indiqué dans la deuxième image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7afb8-116">Then scroll down and click on "server" as seen in the second image below.</span></span>

   

   ![Module2Chapter2step2aim](images/Module2chapter4step2aim.png)

   ![Module2Chapter2step2bim](images/Module2chapter4step2bim.png)
   
   3. <span data-ttu-id="7afb8-119">Si vous le faites étiqueté, une zone de texte « lire me. »</span><span class="sxs-lookup"><span data-stu-id="7afb8-119">That will cause a text box to appear labeled, "read me."</span></span> <span data-ttu-id="7afb8-120">Continuons et le lire.</span><span class="sxs-lookup"><span data-stu-id="7afb8-120">Go ahead and read it.</span></span> <span data-ttu-id="7afb8-121">Une fois que vous avez terminé, cliquez sur le lien en regard de « downloadSDK » afin de le télécharger.</span><span class="sxs-lookup"><span data-stu-id="7afb8-121">Once finished, click on the link next to "downloadSDK" to download it.</span></span>


![Module2Chapter4step3im](images/Module2chapter4step3im.png)

4. <span data-ttu-id="7afb8-123">Sur le dossier une fois le téléchargement terminé.</span><span class="sxs-lookup"><span data-stu-id="7afb8-123">Double click the folder once it finishes downloading.</span></span>  <span data-ttu-id="7afb8-124">Une fois que l’Explorateur de fichiers s’ouvre, révélant le dossier du Kit de développement logiciel, copiez le dossier SDK.</span><span class="sxs-lookup"><span data-stu-id="7afb8-124">Once your file explorer opens revealing the SDK folder, copy the SDK folder.</span></span>
   
   - <span data-ttu-id="7afb8-125">L’étape suivante consisterait à aller dans le lecteur C: windows et créez un dossier appelé « serveur ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-125">Your next step would be to go into the windows C: drive and create a new folder called 'server.'</span></span>
   
   ![Module2Chapter4step4im](images/Module2chapter4step4aim.png)
   
   - <span data-ttu-id="7afb8-127">Ouvrez le dossier et coller le dossier SDK que vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="7afb8-127">Now open up the folder, and paste the SDK folder you copied earlier.</span></span>
   
   ![Module2Chapter4step4im](images/Module2chapter4step4bim.png)
   
5. <span data-ttu-id="7afb8-129">Une fois cette opération terminée, ouvrez le dossier SDK et accédez à « déployer », puis « bin_Win64 », et double-cliquez sur « contrôle photon ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-129">Once that is completed, open the SDK folder and go to "deploy," then "bin_Win64," then double click on "photon control."</span></span>


![Module2Chapter4step4im](images/Module2chapter4step5im.png)

> <span data-ttu-id="7afb8-131">Remarque: Si vous avez des questions sur l’adresse IP ou autres questions similaires, vous trouverez la plupart de vos informations dans la barre d’outils (comme indiqué dans l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="7afb8-131">Note: If you have any questions about IP address, or any other similar questions, you can find most of your information in the toolbar (as shown in the image below).</span></span>
>
> ![Module2Chapter4step4im](images/Module2chapter4noteim.png)

6. <span data-ttu-id="7afb8-133">Maintenant que le serveur est configuré et lancé, revenez en arrière vers le site Web de Photon et cliquez sur l’icône de profil (converti (boxed) dans l’image ci-dessous) et sélectionnez « vos applications. »</span><span class="sxs-lookup"><span data-stu-id="7afb8-133">Now that the server is set up and initiated, go back to the Photon website and click on the profile icon (boxed in the image below) and select "your applications."</span></span>
   

![Module2Chapter3step5im](images/Module2chapter4step6im.png)

7. <span data-ttu-id="7afb8-135">Créer un ID d’application en cliquant sur le bouton « Créer une nouvelle application ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-135">Create an application ID by clicking the "create a new app" button.</span></span>

   ![Module2Chapter3step8im](images/Module2chapter4step7aim.png)

   - <span data-ttu-id="7afb8-137">Sélectionnez « Exécuter Photon » dans le menu déroulant sous « type photon. »</span><span class="sxs-lookup"><span data-stu-id="7afb8-137">Select "Photon RUN" from the dropdown menu under "photon type."</span></span> <span data-ttu-id="7afb8-138">Puis lui donner un nom (quelque chose que vous devez vous rappeler).</span><span class="sxs-lookup"><span data-stu-id="7afb8-138">Then give it a name, (something you would remember).</span></span> <span data-ttu-id="7afb8-139">Dans cet exemple, nous l’avons appelé « HoloLensPhotonProject ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-139">In this example, we named it "HoloLensPhotonProject."</span></span> <span data-ttu-id="7afb8-140">Une fois que vous avez terminé, cliquez sur « Créer ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-140">Once finished, click "create."</span></span>

   ![Module2Chapter3step8im](images/Module2chapter4step7bim.png)

8. <span data-ttu-id="7afb8-142">Une fois cette opération effectuée, revenez à la page de vos applications et vous devriez voir quelque chose de similaire à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7afb8-142">Once that is done, return to your applications page and you should see something similar to the picture below.</span></span> <span data-ttu-id="7afb8-143">Cliquez sur l’ID d’application et copiez-la.</span><span class="sxs-lookup"><span data-stu-id="7afb8-143">Click on the app ID and copy it.</span></span> <span data-ttu-id="7afb8-144">Coller est dans un endroit que facilement accessible.</span><span class="sxs-lookup"><span data-stu-id="7afb8-144">Paste is somewhere you can easily access.</span></span>  
   

![Module2Chapter4step9im](images/Module2chapter4step8im.png)

9. <span data-ttu-id="7afb8-146">Créez un projet unity.</span><span class="sxs-lookup"><span data-stu-id="7afb8-146">Create a new unity project.</span></span> <span data-ttu-id="7afb8-147">Ouvrez le Hub de Unity, puis cliquez sur « Nouveau ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-147">Open Unity Hub and click on "new."</span></span> <span data-ttu-id="7afb8-148">Nommez-le « HLSharingProject. »</span><span class="sxs-lookup"><span data-stu-id="7afb8-148">Name it "HLSharingProject."</span></span> <span data-ttu-id="7afb8-149">Cliquez ensuite sur Créer.</span><span class="sxs-lookup"><span data-stu-id="7afb8-149">Then click create.</span></span> 

   > <span data-ttu-id="7afb8-150">Remarque : Cela peut prendre jusqu'à 2 minutes à charger, selon la vitesse de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7afb8-150">note: This can take up to 2 minutes to load, based on your computer's speed.</span></span>

![Module2Chapter4step9im](images/Module2chapter4step9im.png)

> <span data-ttu-id="7afb8-152">Remarque : choisir un emplacement pour enregistrer votre projet sur votre ordinateur en modifiant l’option « emplacement ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-152">note: pick a place to save your project in your computer by changing the "location" option.</span></span> <span data-ttu-id="7afb8-153">Enregistrez-le dans un emplacement conserve et ont un accès facile aux.</span><span class="sxs-lookup"><span data-stu-id="7afb8-153">Save it to a place you will remember and have easy access to.</span></span>

10. <span data-ttu-id="7afb8-154">Une fois le projet se charge, cliquez sur le « magasin de ressources ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-154">Once the project loads, click on the "assets store."</span></span> <span data-ttu-id="7afb8-155">Puis, dans la zone de recherche illustrée dans l’image ci-dessous, tapez « A » et sélectionnez la ressource « Photon gratuit a-2 ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-155">Then, in the search box shown in the image below, type in "PUN" and select the "Photon PUN-2 FREE" asset.</span></span> 

    ![Module2Chapter4step10im](images/Module2chapter4step10im.PNG)
    
    11. <span data-ttu-id="7afb8-157">Téléchargez et importez !</span><span class="sxs-lookup"><span data-stu-id="7afb8-157">Download and import!</span></span>
    
    ![Module2Chapter4step11im](images/Module2chapter4step11im.png)

### <a name="setting-up-the-unity-project"></a><span data-ttu-id="7afb8-159">**Configuration du projet Unity**</span><span class="sxs-lookup"><span data-stu-id="7afb8-159">**Setting Up the Unity Project**</span></span> 

11. <span data-ttu-id="7afb8-160">télécharger une nouvelle ressource nécessaire pour configurer Photon dans Unity en cliquant sur [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1-Refresh/Microsoft.MixedReality.Toolkit.Unity.Examples-v2.0.0-RC1-Refresh.unitypackage)</span><span class="sxs-lookup"><span data-stu-id="7afb8-160">download a new asset needed to set up Photon in Unity by clicking [here.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1-Refresh/Microsoft.MixedReality.Toolkit.Unity.Examples-v2.0.0-RC1-Refresh.unitypackage)</span></span>

12. <span data-ttu-id="7afb8-161">Dans Unity, cliquez sur le menu de ressources et sélectionnez « Importer des actifs », puis cliquez sur « ressources personnalisées ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-161">In Unity, click on the assets menu and select "import assets," then click on "custom assets."</span></span>

![Module2Chapter4step12im](images/Module2chapter4step12im.PNG)

13. <span data-ttu-id="7afb8-163">Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="7afb8-163">Select the Unity package you just downloaded from the link provided in step 1.</span></span> <span data-ttu-id="7afb8-164">Une fois que le bouton Importer s’affiche dans Unity, cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="7afb8-164">Once the import button appears in Unity, click it.</span></span>

![Module2Chapter4step13im](images/Module2chapter4step13im.png)

> <span data-ttu-id="7afb8-166">Remarque :, là où vous avez téléchargé le package sera où vous le trouver.</span><span class="sxs-lookup"><span data-stu-id="7afb8-166">note: wherever you downloaded the package to will be where you find it.</span></span> <span data-ttu-id="7afb8-167">L’image ci-dessus ne transmettent pas où vous trouverez le package.</span><span class="sxs-lookup"><span data-stu-id="7afb8-167">The image above does not portray where you will find the package.</span></span>

14. <span data-ttu-id="7afb8-168">Créer une nouvelle scène (Cela peut être effectuée à l’aide de contrôle / commande + N ou en cliquant sur « fichier » et sélectionnez « nouvelle scène. »).</span><span class="sxs-lookup"><span data-stu-id="7afb8-168">Create a new scene (this can be done using control/command+N or by clicking "file" and selecting "new scene.").</span></span> <span data-ttu-id="7afb8-169">Enregistrer la scène en tant que « HLSharedProjectMain ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-169">Save the scene as "HLSharedProjectMain."</span></span>

> <span data-ttu-id="7afb8-170">Remarque : vous pouvez recevoir une fenêtre contextuelle qui ressemble à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7afb8-170">note: you may receive a pop-up that looks similar to the image below.</span></span> <span data-ttu-id="7afb8-171">Pour l’instant, cliquez simplement sur « non ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-171">For now, just click "no."</span></span>
>
> ![Module2Chapter4note2im](images/Module2chapter4note2im.png)

15. <span data-ttu-id="7afb8-173">Sous « Toolkit de réalité mixte », cliquez sur « Ajouter à la scène et configurer ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-173">Under "Mixed Reality Toolkit" click on "add to scene and configure."</span></span>

![Module2Chapter4step15im](images/Module2chapter4step15im.png)

16. <span data-ttu-id="7afb8-175">Une fois cette opération terminée, un nouveau fichier de configuration s’affiche, ce qui vous donne la possibilité de personnaliser le profil.</span><span class="sxs-lookup"><span data-stu-id="7afb8-175">Once that is complete, a new configuration file will appear, giving you the choice to customize the profile.</span></span> <span data-ttu-id="7afb8-176">Cliquez sur « Copier et la personnaliser. »</span><span class="sxs-lookup"><span data-stu-id="7afb8-176">Click "copy and customize."</span></span>

![Module2Chapter4step16im](images/Module2chapter4step16im.png)

17. <span data-ttu-id="7afb8-178">Défiler vers le bas et décochez la case « Activer le système de diagnostic ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-178">Scroll down and uncheck "enable diagnostics system."</span></span> <span data-ttu-id="7afb8-179">Cela rend plus facile de configurer ce projet.</span><span class="sxs-lookup"><span data-stu-id="7afb8-179">This will make it easier to set up this project.</span></span>

![Module2Chapter4step17im](images/Module2chapter4step17im.png)

18. <span data-ttu-id="7afb8-181">Ouvrez les paramètres de build (contrôle + MAJ + B).</span><span class="sxs-lookup"><span data-stu-id="7afb8-181">Open the build settings (control+shift+B).</span></span> <span data-ttu-id="7afb8-182">Notez que le programme est actuellement défini sous la plateforme « PC, Mac et Linux autonome ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-182">Notice that the program is currently set under the "PC, Mac and Linux standalone" platform.</span></span> <span data-ttu-id="7afb8-183">Pour ce projet, définissez la plateforme pour être « plateforme windows universelle. »</span><span class="sxs-lookup"><span data-stu-id="7afb8-183">For this project, set the platform to be "universal windows platform."</span></span> <span data-ttu-id="7afb8-184">Sélectionnez-le et cliquez sur « commutateur plateforme. »</span><span class="sxs-lookup"><span data-stu-id="7afb8-184">Select it and click "switch platform."</span></span>

![Module2Chapter4step18im](images/Module2chapter4step18im.png)

19. <span data-ttu-id="7afb8-186">Une fois terminé, cliquez sur la zone intitulée « Ajouter des scènes open ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-186">Once complete, click the box that says "add open scenes."</span></span> <span data-ttu-id="7afb8-187">Accédez à présent le panneau Inspecteur et vérifiez que la case à cocher à droite de la « réalité virtuelle pris en charge » (comme indiqué dans l’image ci-dessous) est activée.</span><span class="sxs-lookup"><span data-stu-id="7afb8-187">Now go to the inspector panel and ensure that the check box to the right of "virtual reality supported" (as shown in the image below) is checked.</span></span> 

![Module2Chapter4step19im](images/Module2chapter4step19im.png)

> <span data-ttu-id="7afb8-189">Remarque : Assurez-vous également que la case à cocher en regard de « arrière-plan/HLSharedProjectMain » est également cochée.</span><span class="sxs-lookup"><span data-stu-id="7afb8-189">note: Also ensure that the check box next to "scenes/HLSharedProjectMain" is also checked.</span></span>

20. <span data-ttu-id="7afb8-190">Sous « paramètres de publication » dans le panneau Inspecteur faites défiler jusqu'à « fonctionnalités » et vous assurer seulement les cases à cocher suivantes sont marquées :</span><span class="sxs-lookup"><span data-stu-id="7afb8-190">Under the "publishing settings" in the inspector panel scroll down to "capabilities" and ensure only the following check boxes are marked:</span></span>

- <span data-ttu-id="7afb8-191">client Internet</span><span class="sxs-lookup"><span data-stu-id="7afb8-191">internet client</span></span>
- <span data-ttu-id="7afb8-192">internet client server</span><span class="sxs-lookup"><span data-stu-id="7afb8-192">internet client server</span></span>
- <span data-ttu-id="7afb8-193">serveur client de réseau privé</span><span class="sxs-lookup"><span data-stu-id="7afb8-193">private network client server</span></span>
- <span data-ttu-id="7afb8-194">camera/webcam</span><span class="sxs-lookup"><span data-stu-id="7afb8-194">camera/webcam</span></span>
- <span data-ttu-id="7afb8-195">Microphone</span><span class="sxs-lookup"><span data-stu-id="7afb8-195">microphone</span></span>

21. <span data-ttu-id="7afb8-196">Comme étape 12, l’étape suivante serait pour importer un autre package personnalisé appelé « Lesson2 », qui peut être téléchargé [ici]. [lesson2.unitypackage lien ici] Importez ce package.</span><span class="sxs-lookup"><span data-stu-id="7afb8-196">Just like step 12, the next step would be to import another custom package called "Lesson2" which can be downloaded [here.][lesson2.unitypackage link goes here] Import that package.</span></span>

![Module2Chapter4step21im](images/Module2chapter4step20im.png)

22. <span data-ttu-id="7afb8-198">Désormais, dans le volet de projet, aller sur le dossier « prefabs », étant donné que dans les prochaines étapes, vous allez implémenter quelques prefabs dans la scène.</span><span class="sxs-lookup"><span data-stu-id="7afb8-198">Now, in the project panel, go to the "prefabs" folder, since in next few steps you will be implementing a few prefabs into the scene.</span></span> <span data-ttu-id="7afb8-199">Dans le dossier « prefabs », cliquez et faites glisser le préfabriqué, « DebugWindow » dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="7afb8-199">In the "prefabs" folder, click and drag the prefab, "DebugWindow" into the hierarchy.</span></span> <span data-ttu-id="7afb8-200">Une fois que vous avez terminé, enregistrez le projet (cliquez sur fichier, puis l’enregistrer, ou CTRL + S)</span><span class="sxs-lookup"><span data-stu-id="7afb8-200">Once finished, save the project (click file, then save, or control+S)</span></span>

![Module2Chapter4step22im](images/Module2chapter4step21im.PNG)

> <span data-ttu-id="7afb8-202">Remarque : Vous pouvez remarquer une fenêtre contextuelle s’affichent lorsque vous cliquez sur le préfabriqué, vous demandant sur TMP Essentials.</span><span class="sxs-lookup"><span data-stu-id="7afb8-202">note: You may notice a pop-up appear as you click on the prefab, asking you about TMP Essentials.</span></span> <span data-ttu-id="7afb8-203">Cliquez sur « Importation TMP Essentials » car ils vous seront utiles.</span><span class="sxs-lookup"><span data-stu-id="7afb8-203">Click "Import TMP Essentials" as they will be needed.</span></span>
>
> ![Module2Chapter4note3im](images/Module2chapter4note3im.PNG)

### <a name="connecting-multiple-users"></a><span data-ttu-id="7afb8-205">**Plusieurs utilisateurs qui se connectent**</span><span class="sxs-lookup"><span data-stu-id="7afb8-205">**Connecting Multiple Users**</span></span>

23. <span data-ttu-id="7afb8-206">À l’étape 22, dans le dossier « prefabs » dans le volet de projet, l’étape suivante consiste à glisser -déplacer le préfabriqué « NetworkLobby » à la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="7afb8-206">Like step 22, in the "prefabs" folder in the project panel, the next step is to drag and drop the "NetworkLobby" prefab in to the hierarchy.</span></span> 

![Module2Chapter4step22im](images/Module2chapter4step22im.png)

24. <span data-ttu-id="7afb8-208">Lorsque vous ouvrez le préfabriqué parent, « NetworkLobby », vous devez voir un enfant prefab, « NetworkRoom ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-208">When you open up the parent prefab, "NetworkLobby," you should see a child prefab, "NetworkRoom."</span></span> <span data-ttu-id="7afb8-209">Avec qu’elle est sélectionnée, accédez au volet d’inspecteur, puis cliquez sur « Ajouter le composant ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-209">With it selected, go into the inspector panel and click "Add Component."</span></span> <span data-ttu-id="7afb8-210">Recherchez « PhotonView » et ajouter le composant.</span><span class="sxs-lookup"><span data-stu-id="7afb8-210">Search for "PhotonView" and add the component.</span></span>

![Module2Chapter4step23im](images/Module2chapter4step23im.png)

25. <span data-ttu-id="7afb8-212">Créer un nouvel objet de jeu vide dans la hiérarchie (clic droit dans la hiérarchie et choisissez « vide »).</span><span class="sxs-lookup"><span data-stu-id="7afb8-212">Create a new empty game object in the hierarchy (right click in the hierarchy and select "empty").</span></span> <span data-ttu-id="7afb8-213">Vérifiez le positionnement est défini sur x = 0, y = 0, z = 0 et nommer l’objet, « PhotonUser ».</span><span class="sxs-lookup"><span data-stu-id="7afb8-213">Ensure the positioning is set to x =0, y=0, z=0 and name the object, "PhotonUser."</span></span>

![Module2Chapter4step24im](images/Module2chapter4step24im.png)

## <a name="congratulations"></a><span data-ttu-id="7afb8-215">Félicitations</span><span class="sxs-lookup"><span data-stu-id="7afb8-215">Congratulations</span></span>



