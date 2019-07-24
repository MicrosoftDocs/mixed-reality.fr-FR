---
title: Module ASA d’apprentissage de la fonction d’ancrage spatial Azure sur HoloLens 2
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
# <a name="photon-correct-me-if-im-wrong"></a><span data-ttu-id="07d20-104">Photonique (corrigez-moi si je ne suis pas correct)</span><span class="sxs-lookup"><span data-stu-id="07d20-104">Photon (correct me if I'm wrong)</span></span>

<span data-ttu-id="07d20-105">Dans cette leçon,</span><span class="sxs-lookup"><span data-stu-id="07d20-105">In this lesson,</span></span> 

<span data-ttu-id="07d20-106">Cherché</span><span class="sxs-lookup"><span data-stu-id="07d20-106">Objectives:</span></span>

* <span data-ttu-id="07d20-107">En savoir plus sur _____________________________________________</span><span class="sxs-lookup"><span data-stu-id="07d20-107">Learn how to _____________________________________________</span></span>

* <span data-ttu-id="07d20-108">En savoir plus sur _________________________________________________</span><span class="sxs-lookup"><span data-stu-id="07d20-108">Learn how to _________________________________________________</span></span>

  

## <a name="instructions"></a><span data-ttu-id="07d20-109">Instructions</span><span class="sxs-lookup"><span data-stu-id="07d20-109">Instructions</span></span>

### <a name="setting-up-photon"></a><span data-ttu-id="07d20-110">Configuration de photons</span><span class="sxs-lookup"><span data-stu-id="07d20-110">Setting Up Photon</span></span>

1. <span data-ttu-id="07d20-111">Configurez un compte de [photons](https://dashboard.photonengine.com/en-US/Account/SignUp) .</span><span class="sxs-lookup"><span data-stu-id="07d20-111">Set up a [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) account.</span></span> <span data-ttu-id="07d20-112">Cela consiste à imputer votre adresse de messagerie et à passer par certaines étapes de vérification.</span><span class="sxs-lookup"><span data-stu-id="07d20-112">Doing this will consist of imputing your email and going through some verification steps.</span></span>
   

![Module2Chapter4step1im](images/Module2chapter4step1im.png)

2. <span data-ttu-id="07d20-114">Une fois que vous êtes inscrit, cliquez sur kits de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="07d20-114">Once you are signed up, click on SDKs.</span></span> <span data-ttu-id="07d20-115">Une fois que vous êtes sur cette page, cliquez sur «serveur» et assurez-vous que le message «auto-hébergé» s’affiche.</span><span class="sxs-lookup"><span data-stu-id="07d20-115">Once you are on that page, click on "server," and make ensure it says, "self hosted."</span></span> <span data-ttu-id="07d20-116">Faites défiler vers le bas et cliquez sur «serveur» comme illustré dans la deuxième image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="07d20-116">Then scroll down and click on "server" as seen in the second image below.</span></span>

   

   ![Module2Chapter2step2aim](images/Module2chapter4step2aim.png)

   ![Module2Chapter2step2bim](images/Module2chapter4step2bim.png)
   
   3. <span data-ttu-id="07d20-119">Cela entraînera l’affichage d’une zone de texte intitulée «Lisez-moi».</span><span class="sxs-lookup"><span data-stu-id="07d20-119">That will cause a text box to appear labeled, "read me."</span></span> <span data-ttu-id="07d20-120">Continuez et lisez-le.</span><span class="sxs-lookup"><span data-stu-id="07d20-120">Go ahead and read it.</span></span> <span data-ttu-id="07d20-121">Une fois que vous avez terminé, cliquez sur le lien en regard de «downloadSDK» pour le télécharger.</span><span class="sxs-lookup"><span data-stu-id="07d20-121">Once finished, click on the link next to "downloadSDK" to download it.</span></span>


![Module2Chapter4step3im](images/Module2chapter4step3im.png)

4. <span data-ttu-id="07d20-123">Double-cliquez sur le dossier une fois son téléchargement terminé.</span><span class="sxs-lookup"><span data-stu-id="07d20-123">Double click the folder once it finishes downloading.</span></span>  <span data-ttu-id="07d20-124">Une fois que votre Explorateur de fichiers s’ouvre et affiche le dossier SDK, copiez le dossier SDK.</span><span class="sxs-lookup"><span data-stu-id="07d20-124">Once your file explorer opens revealing the SDK folder, copy the SDK folder.</span></span>
   
   - <span data-ttu-id="07d20-125">L’étape suivante consiste à accéder au lecteur Windows C: et à créer un nouveau dossier appelé «serveur».</span><span class="sxs-lookup"><span data-stu-id="07d20-125">Your next step would be to go into the windows C: drive and create a new folder called 'server.'</span></span>
   
   ![Module2Chapter4step4im](images/Module2chapter4step4aim.png)
   
   - <span data-ttu-id="07d20-127">Ouvrez maintenant le dossier, puis collez le dossier SDK que vous avez copié précédemment.</span><span class="sxs-lookup"><span data-stu-id="07d20-127">Now open up the folder, and paste the SDK folder you copied earlier.</span></span>
   
   ![Module2Chapter4step4im](images/Module2chapter4step4bim.png)
   
5. <span data-ttu-id="07d20-129">Une fois cette opération terminée, ouvrez le dossier SDK et accédez à «Deploy», puis à «bin_Win64», puis double-cliquez sur «contrôle de photons».</span><span class="sxs-lookup"><span data-stu-id="07d20-129">Once that is completed, open the SDK folder and go to "deploy," then "bin_Win64," then double click on "photon control."</span></span>


![Module2Chapter4step4im](images/Module2chapter4step5im.png)

> <span data-ttu-id="07d20-131">Remarque : Si vous avez des questions concernant l’adresse IP, ou toute autre question similaire, vous trouverez la plupart de vos informations dans la barre d’outils (comme indiqué dans l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="07d20-131">Note: If you have any questions about IP address, or any other similar questions, you can find most of your information in the toolbar (as shown in the image below).</span></span>
>
> ![Module2Chapter4step4im](images/Module2chapter4noteim.png)

6. <span data-ttu-id="07d20-133">Maintenant que le serveur est configuré et lancé, retournez sur le site Web de photons et cliquez sur l’icône de profil (boxed dans l’image ci-dessous), puis sélectionnez «vos applications».</span><span class="sxs-lookup"><span data-stu-id="07d20-133">Now that the server is set up and initiated, go back to the Photon website and click on the profile icon (boxed in the image below) and select "your applications."</span></span>
   

![Module2Chapter3step5im](images/Module2chapter4step6im.png)

7. <span data-ttu-id="07d20-135">Créez un ID d’application en cliquant sur le bouton «créer une application».</span><span class="sxs-lookup"><span data-stu-id="07d20-135">Create an application ID by clicking the "create a new app" button.</span></span>

   ![Module2Chapter3step8im](images/Module2chapter4step7aim.png)

   - <span data-ttu-id="07d20-137">Sélectionnez «série de photons» dans le menu déroulant sous «type de photons».</span><span class="sxs-lookup"><span data-stu-id="07d20-137">Select "Photon RUN" from the dropdown menu under "photon type."</span></span> <span data-ttu-id="07d20-138">Ensuite, donnez-lui un nom (ce qui vous rappellerait).</span><span class="sxs-lookup"><span data-stu-id="07d20-138">Then give it a name, (something you would remember).</span></span> <span data-ttu-id="07d20-139">Dans cet exemple, nous l’avons nommé «HoloLensPhotonProject».</span><span class="sxs-lookup"><span data-stu-id="07d20-139">In this example, we named it "HoloLensPhotonProject."</span></span> <span data-ttu-id="07d20-140">Une fois que vous avez terminé, cliquez sur «créer».</span><span class="sxs-lookup"><span data-stu-id="07d20-140">Once finished, click "create."</span></span>

   ![Module2Chapter3step8im](images/Module2chapter4step7bim.png)

8. <span data-ttu-id="07d20-142">Une fois cette opération effectuée, revenez à la page de votre application et vous devriez voir une image semblable à celle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="07d20-142">Once that is done, return to your applications page and you should see something similar to the picture below.</span></span> <span data-ttu-id="07d20-143">Cliquez sur l’ID d’application et copiez-le.</span><span class="sxs-lookup"><span data-stu-id="07d20-143">Click on the app ID and copy it.</span></span> <span data-ttu-id="07d20-144">Coller est un endroit où vous pouvez accéder facilement à.</span><span class="sxs-lookup"><span data-stu-id="07d20-144">Paste is somewhere you can easily access.</span></span>  
   

![Module2Chapter4step9im](images/Module2chapter4step8im.png)

9. <span data-ttu-id="07d20-146">Créez un nouveau projet Unity.</span><span class="sxs-lookup"><span data-stu-id="07d20-146">Create a new unity project.</span></span> <span data-ttu-id="07d20-147">Ouvrez Unity Hub et cliquez sur «nouveau».</span><span class="sxs-lookup"><span data-stu-id="07d20-147">Open Unity Hub and click on "new."</span></span> <span data-ttu-id="07d20-148">Nommez-la «HLSharingProject».</span><span class="sxs-lookup"><span data-stu-id="07d20-148">Name it "HLSharingProject."</span></span> <span data-ttu-id="07d20-149">Cliquez ensuite sur créer.</span><span class="sxs-lookup"><span data-stu-id="07d20-149">Then click create.</span></span> 

   > <span data-ttu-id="07d20-150">Observe Le chargement peut prendre jusqu’à 2 minutes, en fonction de la vitesse de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="07d20-150">note: This can take up to 2 minutes to load, based on your computer's speed.</span></span>

![Module2Chapter4step9im](images/Module2chapter4step9im.png)

> <span data-ttu-id="07d20-152">Remarque: choisissez un emplacement pour enregistrer votre projet sur votre ordinateur en modifiant l’option «emplacement».</span><span class="sxs-lookup"><span data-stu-id="07d20-152">note: pick a place to save your project in your computer by changing the "location" option.</span></span> <span data-ttu-id="07d20-153">Enregistrez-le à un endroit dont vous vous souviendrez pour accéder facilement à.</span><span class="sxs-lookup"><span data-stu-id="07d20-153">Save it to a place you will remember and have easy access to.</span></span>

10. <span data-ttu-id="07d20-154">Une fois le projet chargé, cliquez sur le «magasin d’actifs».</span><span class="sxs-lookup"><span data-stu-id="07d20-154">Once the project loads, click on the "assets store."</span></span> <span data-ttu-id="07d20-155">Ensuite, dans la zone de recherche présentée dans l’image ci-dessous, tapez «retentissante» et sélectionnez la ressource «photon retentissante-2 FREE».</span><span class="sxs-lookup"><span data-stu-id="07d20-155">Then, in the search box shown in the image below, type in "PUN" and select the "Photon PUN-2 FREE" asset.</span></span> 

    ![Module2Chapter4step10im](images/Module2chapter4step10im.PNG)
    
    11. <span data-ttu-id="07d20-157">Téléchargez et importez!</span><span class="sxs-lookup"><span data-stu-id="07d20-157">Download and import!</span></span>
    
    ![Module2Chapter4step11im](images/Module2chapter4step11im.png)

### <a name="setting-up-the-unity-project"></a><span data-ttu-id="07d20-159">**Configuration du projet Unity**</span><span class="sxs-lookup"><span data-stu-id="07d20-159">**Setting Up the Unity Project**</span></span> 

11. <span data-ttu-id="07d20-160">Téléchargez une nouvelle ressource nécessaire à la configuration de photons dans Unity en cliquant [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1-Refresh/Microsoft.MixedReality.Toolkit.Unity.Examples-v2.0.0-RC1-Refresh.unitypackage)</span><span class="sxs-lookup"><span data-stu-id="07d20-160">download a new asset needed to set up Photon in Unity by clicking [here.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1-Refresh/Microsoft.MixedReality.Toolkit.Unity.Examples-v2.0.0-RC1-Refresh.unitypackage)</span></span>

12. <span data-ttu-id="07d20-161">Dans Unity, cliquez sur le menu composants et sélectionnez «Importer des ressources», puis cliquez sur «ressources personnalisées».</span><span class="sxs-lookup"><span data-stu-id="07d20-161">In Unity, click on the assets menu and select "import assets," then click on "custom assets."</span></span>

![Module2Chapter4step12im](images/Module2chapter4step12im.PNG)

13. <span data-ttu-id="07d20-163">Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="07d20-163">Select the Unity package you just downloaded from the link provided in step 1.</span></span> <span data-ttu-id="07d20-164">Une fois que le bouton Importer apparaît dans Unity, cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="07d20-164">Once the import button appears in Unity, click it.</span></span>

![Module2Chapter4step13im](images/Module2chapter4step13im.png)

> <span data-ttu-id="07d20-166">Remarque: chaque fois que vous avez téléchargé le package dans, vous le trouverez.</span><span class="sxs-lookup"><span data-stu-id="07d20-166">note: wherever you downloaded the package to will be where you find it.</span></span> <span data-ttu-id="07d20-167">L’image ci-dessus ne décrit pas où se trouve le package.</span><span class="sxs-lookup"><span data-stu-id="07d20-167">The image above does not portray where you will find the package.</span></span>

14. <span data-ttu-id="07d20-168">Créez une nouvelle scène (cette opération peut être effectuée à l’aide de Control/Command + N ou en cliquant sur «file» et en sélectionnant «New Scene».)</span><span class="sxs-lookup"><span data-stu-id="07d20-168">Create a new scene (this can be done using control/command+N or by clicking "file" and selecting "new scene.").</span></span> <span data-ttu-id="07d20-169">Enregistrez la scène en tant que «HLSharedProjectMain».</span><span class="sxs-lookup"><span data-stu-id="07d20-169">Save the scene as "HLSharedProjectMain."</span></span>

> <span data-ttu-id="07d20-170">Remarque: vous pouvez recevoir une fenêtre contextuelle qui ressemble à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="07d20-170">note: you may receive a pop-up that looks similar to the image below.</span></span> <span data-ttu-id="07d20-171">Pour le moment, cliquez simplement sur «non».</span><span class="sxs-lookup"><span data-stu-id="07d20-171">For now, just click "no."</span></span>
>
> ![Module2Chapter4note2im](images/Module2chapter4note2im.png)

15. <span data-ttu-id="07d20-173">Sous «Mixed Reality Toolkit», cliquez sur «Ajouter à la scène et configurer».</span><span class="sxs-lookup"><span data-stu-id="07d20-173">Under "Mixed Reality Toolkit" click on "add to scene and configure."</span></span>

![Module2Chapter4step15im](images/Module2chapter4step15im.png)

16. <span data-ttu-id="07d20-175">Une fois cette opération terminée, un nouveau fichier de configuration s’affiche et vous donne la possibilité de personnaliser le profil.</span><span class="sxs-lookup"><span data-stu-id="07d20-175">Once that is complete, a new configuration file will appear, giving you the choice to customize the profile.</span></span> <span data-ttu-id="07d20-176">Cliquez sur «copier et personnaliser».</span><span class="sxs-lookup"><span data-stu-id="07d20-176">Click "copy and customize."</span></span>

![Module2Chapter4step16im](images/Module2chapter4step16im.png)

17. <span data-ttu-id="07d20-178">Faites défiler vers le dessous et décochez «activer le système de diagnostic».</span><span class="sxs-lookup"><span data-stu-id="07d20-178">Scroll down and uncheck "enable diagnostics system."</span></span> <span data-ttu-id="07d20-179">Cela facilitera la configuration de ce projet.</span><span class="sxs-lookup"><span data-stu-id="07d20-179">This will make it easier to set up this project.</span></span>

![Module2Chapter4step17im](images/Module2chapter4step17im.png)

18. <span data-ttu-id="07d20-181">Ouvrez les paramètres de build (Ctrl + Maj + B).</span><span class="sxs-lookup"><span data-stu-id="07d20-181">Open the build settings (control+shift+B).</span></span> <span data-ttu-id="07d20-182">Notez que le programme est actuellement défini sous la plateforme «PC, Mac et Linux standalone».</span><span class="sxs-lookup"><span data-stu-id="07d20-182">Notice that the program is currently set under the "PC, Mac and Linux standalone" platform.</span></span> <span data-ttu-id="07d20-183">Pour ce projet, définissez la plateforme sur «plateforme Windows universelle».</span><span class="sxs-lookup"><span data-stu-id="07d20-183">For this project, set the platform to be "universal windows platform."</span></span> <span data-ttu-id="07d20-184">Sélectionnez-le et cliquez sur «changer de plateforme».</span><span class="sxs-lookup"><span data-stu-id="07d20-184">Select it and click "switch platform."</span></span>

![Module2Chapter4step18im](images/Module2chapter4step18im.png)

19. <span data-ttu-id="07d20-186">Une fois l’opération terminée, cliquez sur la case «Ajouter des scènes ouvertes».</span><span class="sxs-lookup"><span data-stu-id="07d20-186">Once complete, click the box that says "add open scenes."</span></span> <span data-ttu-id="07d20-187">Maintenant, accédez au panneau inspecteur et vérifiez que la case à cocher située à droite de «Virtual Reality pris en charge» (comme indiqué dans l’image ci-dessous) est cochée.</span><span class="sxs-lookup"><span data-stu-id="07d20-187">Now go to the inspector panel and ensure that the check box to the right of "virtual reality supported" (as shown in the image below) is checked.</span></span> 

![Module2Chapter4step19im](images/Module2chapter4step19im.png)

> <span data-ttu-id="07d20-189">Observe Assurez-vous également que la case à cocher en regard de «scènes/HLSharedProjectMain» est également activée.</span><span class="sxs-lookup"><span data-stu-id="07d20-189">note: Also ensure that the check box next to "scenes/HLSharedProjectMain" is also checked.</span></span>

20. <span data-ttu-id="07d20-190">Sous les paramètres de publication dans le volet de l’inspecteur, faites défiler la liste jusqu’à «fonctionnalités» et assurez-vous que seules les cases à cocher suivantes sont activées:</span><span class="sxs-lookup"><span data-stu-id="07d20-190">Under the "publishing settings" in the inspector panel scroll down to "capabilities" and ensure only the following check boxes are marked:</span></span>

- <span data-ttu-id="07d20-191">client Internet</span><span class="sxs-lookup"><span data-stu-id="07d20-191">internet client</span></span>
- <span data-ttu-id="07d20-192">serveur client Internet</span><span class="sxs-lookup"><span data-stu-id="07d20-192">internet client server</span></span>
- <span data-ttu-id="07d20-193">serveur client de réseau privé</span><span class="sxs-lookup"><span data-stu-id="07d20-193">private network client server</span></span>
- <span data-ttu-id="07d20-194">caméra/Webcam</span><span class="sxs-lookup"><span data-stu-id="07d20-194">camera/webcam</span></span>
- <span data-ttu-id="07d20-195">Microphone</span><span class="sxs-lookup"><span data-stu-id="07d20-195">microphone</span></span>

21. <span data-ttu-id="07d20-196">À l’instar de l’étape 12, l’étape suivante consiste à importer un autre package personnalisé appelé «Lesson2», que vous pouvez télécharger [ici.] [lien lesson2. pour Unity ici] Importez ce package.</span><span class="sxs-lookup"><span data-stu-id="07d20-196">Just like step 12, the next step would be to import another custom package called "Lesson2" which can be downloaded [here.][lesson2.unitypackage link goes here] Import that package.</span></span>

![Module2Chapter4step21im](images/Module2chapter4step20im.png)

22. <span data-ttu-id="07d20-198">Maintenant, dans le panneau projet, accédez au dossier «prefabs», car dans les étapes suivantes, vous allez implémenter quelques prefabs dans la scène.</span><span class="sxs-lookup"><span data-stu-id="07d20-198">Now, in the project panel, go to the "prefabs" folder, since in next few steps you will be implementing a few prefabs into the scene.</span></span> <span data-ttu-id="07d20-199">Dans le dossier «prefabs», cliquez et faites glisser Prefab, «DebugWindow» dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="07d20-199">In the "prefabs" folder, click and drag the prefab, "DebugWindow" into the hierarchy.</span></span> <span data-ttu-id="07d20-200">Une fois que vous avez terminé, enregistrez le projet (cliquez sur fichier, puis sur enregistrer ou sur contrôle + S).</span><span class="sxs-lookup"><span data-stu-id="07d20-200">Once finished, save the project (click file, then save, or control+S)</span></span>

![Module2Chapter4step22im](images/Module2chapter4step21im.PNG)

> <span data-ttu-id="07d20-202">Observe Vous pouvez remarquer qu’une fenêtre contextuelle s’affiche lorsque vous cliquez sur le Prefab, qui vous demande des informations sur TMP Essentials.</span><span class="sxs-lookup"><span data-stu-id="07d20-202">note: You may notice a pop-up appear as you click on the prefab, asking you about TMP Essentials.</span></span> <span data-ttu-id="07d20-203">Cliquez sur «Importer TMP Essentials», car ils seront nécessaires.</span><span class="sxs-lookup"><span data-stu-id="07d20-203">Click "Import TMP Essentials" as they will be needed.</span></span>
>
> ![Module2Chapter4note3im](images/Module2chapter4note3im.PNG)

### <a name="connecting-multiple-users"></a><span data-ttu-id="07d20-205">**Connexion de plusieurs utilisateurs**</span><span class="sxs-lookup"><span data-stu-id="07d20-205">**Connecting Multiple Users**</span></span>

23. <span data-ttu-id="07d20-206">Comme dans l’étape 22, dans le dossier «prefabs» du panneau projet, l’étape suivante consiste à faire glisser et déposer le Prefab «NetworkLobby» dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="07d20-206">Like step 22, in the "prefabs" folder in the project panel, the next step is to drag and drop the "NetworkLobby" prefab in to the hierarchy.</span></span> 

![Module2Chapter4step22im](images/Module2chapter4step22im.png)

24. <span data-ttu-id="07d20-208">Lorsque vous ouvrez le Prefab parent, «NetworkLobby», vous devez voir un Prefab enfant, «NetworkRoom».</span><span class="sxs-lookup"><span data-stu-id="07d20-208">When you open up the parent prefab, "NetworkLobby," you should see a child prefab, "NetworkRoom."</span></span> <span data-ttu-id="07d20-209">Une fois l’option sélectionnée, accédez au panneau de l’inspecteur, puis cliquez sur Ajouter un composant.</span><span class="sxs-lookup"><span data-stu-id="07d20-209">With it selected, go into the inspector panel and click "Add Component."</span></span> <span data-ttu-id="07d20-210">Recherchez «PhotonView» et ajoutez le composant.</span><span class="sxs-lookup"><span data-stu-id="07d20-210">Search for "PhotonView" and add the component.</span></span>

![Module2Chapter4step23im](images/Module2chapter4step23im.png)

25. <span data-ttu-id="07d20-212">Créez un nouvel objet de jeu vide dans la hiérarchie (cliquez avec le bouton droit dans la hiérarchie et sélectionnez «vide»).</span><span class="sxs-lookup"><span data-stu-id="07d20-212">Create a new empty game object in the hierarchy (right click in the hierarchy and select "empty").</span></span> <span data-ttu-id="07d20-213">Assurez-vous que le positionnement est défini sur x = 0, y = 0, z = 0 et nommez l’objet, «PhotonUser».</span><span class="sxs-lookup"><span data-stu-id="07d20-213">Ensure the positioning is set to x =0, y=0, z=0 and name the object, "PhotonUser."</span></span>

![Module2Chapter4step24im](images/Module2chapter4step24im.png)

## <a name="congratulations"></a><span data-ttu-id="07d20-215">Félicitations</span><span class="sxs-lookup"><span data-stu-id="07d20-215">Congratulations</span></span>



