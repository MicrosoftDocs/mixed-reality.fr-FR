# <a name="2-getting-unity-ready-for-development"></a><span data-ttu-id="275da-101">2. Obtention d’Unity prête pour le développement</span><span class="sxs-lookup"><span data-stu-id="275da-101">2. Getting Unity ready for development</span></span> 


<span data-ttu-id="275da-102">Dans ce didacticiel, nous allons apprendre à préparer et à configurer Unity pour le développement d’applications, notamment l’importation du kit de développement de la réalité mixte, la configuration des paramètres de génération et la préparation de notre scène.</span><span class="sxs-lookup"><span data-stu-id="275da-102">In this tutorial, we learn how to prepare and configure Unity for application development, including importing the Mixed Reality Toolkit, configuring build settings, and preparing our scene.</span></span>

<span data-ttu-id="275da-103">Cherché</span><span class="sxs-lookup"><span data-stu-id="275da-103">Objectives:</span></span>

- <span data-ttu-id="275da-104">Configurer Unity pour le développement d’applications</span><span class="sxs-lookup"><span data-stu-id="275da-104">Configure Unity for application development</span></span>

- <span data-ttu-id="275da-105">Importer le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="275da-105">Import the Mixed Reality Toolkit</span></span>

- <span data-ttu-id="275da-106">Préparer la scène de votre projet</span><span class="sxs-lookup"><span data-stu-id="275da-106">Prepare your project scene</span></span>

## <a name="instructions"></a><span data-ttu-id="275da-107">Instructions</span><span class="sxs-lookup"><span data-stu-id="275da-107">Instructions</span></span>

1. <span data-ttu-id="275da-108">Téléchargez et enregistrez le package Unity du kit d’outils de réalité mixte en cliquant [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC2.1/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC2.1.unitypackage)</span><span class="sxs-lookup"><span data-stu-id="275da-108">Download and save the Mixed Reality Toolkit unity package by clicking [here.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC2.1/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC2.1.unitypackage)</span></span>

2. <span data-ttu-id="275da-109">Dans Unity, cliquez sur le menu composants et sélectionnez Importer un package, puis cliquez sur package personnalisé.</span><span class="sxs-lookup"><span data-stu-id="275da-109">In Unity, click on the assets menu and select Import Package, then click on Custom Package.</span></span>

![Module3Chapter2step2im](images/module3chapter2step2im.PNG)

3. <span data-ttu-id="275da-111">Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="275da-111">Select the Unity package you just downloaded from the link provided in step 1.</span></span> <span data-ttu-id="275da-112">Une fois que la fenêtre contextuelle d’importation s’affiche dans Unity, cliquez sur le bouton Importer pour commencer l’importation.</span><span class="sxs-lookup"><span data-stu-id="275da-112">Once the import pop-up window appears in Unity, click the Import button to begin importing.</span></span> <span data-ttu-id="275da-113">L’importation du MRTK peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="275da-113">Importing the MRTK may take several minutes.</span></span>

![Module3Chapter2step3im](images/module3chapter2step3im.PNG)

> <span data-ttu-id="275da-115">Remarque : Le package téléchargé se trouve dans votre dossier local où vous avez enregistré le fichier.</span><span class="sxs-lookup"><span data-stu-id="275da-115">Note: The downloaded package is in your local folder where you have saved the file.</span></span> <span data-ttu-id="275da-116">L’image ci-dessus ne décrit pas où se trouve le package.</span><span class="sxs-lookup"><span data-stu-id="275da-116">The image above does not portray where you will find the package.</span></span>

4. <span data-ttu-id="275da-117">Créez une nouvelle scène.</span><span class="sxs-lookup"><span data-stu-id="275da-117">Create a new scene.</span></span> <span data-ttu-id="275da-118">Pour ce faire, cliquez sur fichier, puis sélectionnez nouvelle scène».</span><span class="sxs-lookup"><span data-stu-id="275da-118">This can be done by clicking File, and selecting New Scene").</span></span> <span data-ttu-id="275da-119">Enregistrez la scène en tant que HLSharedProjectMain.</span><span class="sxs-lookup"><span data-stu-id="275da-119">Save the scene as HLSharedProjectMain.</span></span>

> <span data-ttu-id="275da-120">Remarque: vous pouvez recevoir une fenêtre contextuelle qui ressemble à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="275da-120">Note: you may receive a pop-up that looks similar to the image below.</span></span> <span data-ttu-id="275da-121">Pour le moment, cliquez sur non.</span><span class="sxs-lookup"><span data-stu-id="275da-121">For now, click No.</span></span>
>
> ![Module3Chapter2note1im](images/module3chapter2note1im.PNG)

5. <span data-ttu-id="275da-123">Dans la boîte à outils de réalité mixte, cliquez sur Ajouter à la scène et configurer.</span><span class="sxs-lookup"><span data-stu-id="275da-123">Under Mixed Reality Toolkit, click on Add to Scene and Configure.</span></span>

![Module3Chapter2step5im](images/module3chapter2step5im.PNG)

6. <span data-ttu-id="275da-125">Une fois cette opération terminée, un nouveau fichier de configuration s’affiche, vous donnant la possibilité de personnaliser le profil.</span><span class="sxs-lookup"><span data-stu-id="275da-125">Once that is complete, a new configuration file appears, giving you the choice to customize the profile.</span></span> <span data-ttu-id="275da-126">Cliquez sur copier et personnaliser.</span><span class="sxs-lookup"><span data-stu-id="275da-126">Click Copy and Customize.</span></span>

![Module3Chapter2step6ima](images/module3chapter2step6ima.PNG)

![Module3Chapter2step6imb](images/module3chapter2step6imb.PNG)

![Module3Chapter2step6imc](images/module3chapter2step6imc.PNG)

7. <span data-ttu-id="275da-130">Faites défiler vers le dessous et décochez activer le système de diagnostic si vous souhaitez masquer la fenêtre de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="275da-130">Scroll down and uncheck Enable Diagnostics system if you want to hide the diagnostics window.</span></span> <span data-ttu-id="275da-131">Nous vous recommandons de conserver la fenêtre de diagnostic activée pendant le développement d’applications pour surveiller les performances et la désactiver pendant les démonstrations de production ou d’application.</span><span class="sxs-lookup"><span data-stu-id="275da-131">We recommend keeping the diagnostics window enabled during application development to monitor performance, and disabling it during production or application demonstrations.</span></span> 

![Module3Chapter2step7ima](images/module3chapter2step7ima.PNG)

8. <span data-ttu-id="275da-133">Ouvrez les paramètres de build en appuyant sur Ctrl + Maj + B ou en accédant à fichier-> paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="275da-133">Open the build settings by pressing control+shift+B or going to File->Build Settings.</span></span> <span data-ttu-id="275da-134">Notez que le programme est actuellement défini sous la plateforme autonome PC, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="275da-134">Notice that the program is currently set under the PC, Mac and Linux standalone platform.</span></span> <span data-ttu-id="275da-135">Pour le développement HoloLens 2, définissez la plateforme sur plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="275da-135">For HoloLens 2 development, set the platform to be Universal Windows Platform.</span></span> <span data-ttu-id="275da-136">Sélectionnez-le, puis cliquez sur basculer la plateforme.</span><span class="sxs-lookup"><span data-stu-id="275da-136">Select it and click Switch Platform.</span></span>

![Module3Chapter2step8im](images/module3chapter2step8im.PNG)

9. <span data-ttu-id="275da-138">Une fois terminé, cliquez sur la zone qui indique ajouter des scènes ouvertes.</span><span class="sxs-lookup"><span data-stu-id="275da-138">Once complete, click the box that says Add Open Scenes.</span></span> <span data-ttu-id="275da-139">Maintenant, accédez au panneau inspecteur et vérifiez que la case à cocher située à droite de Virtual Reality pris en charge (comme indiqué dans l’image ci-dessous) est cochée.</span><span class="sxs-lookup"><span data-stu-id="275da-139">Now go to the Inspector panel, and ensure that the check box to the right of Virtual Reality Supported (as shown in the image below) is checked.</span></span> <span data-ttu-id="275da-140">Vérifiez également que la case à cocher en regard de scenes/HLSharedProjectMain est également activée comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="275da-140">Also ensure that the check box next to scenes/HLSharedProjectMain is also checked as shown in the image below.</span></span>

![Module3Chapter2step9im](images/module3chapter2step9im.PNG)

10. <span data-ttu-id="275da-142">Dans la section paramètres de publication du panneau Inspecteur, faites défiler l’écran jusqu’à fonctionnalités, puis vérifiez que les cases à cocher suivantes sont activées:</span><span class="sxs-lookup"><span data-stu-id="275da-142">Under the Publishing Settings section in the Inspector panel, scroll down to Capabilities, and ensure the following check boxes are marked:</span></span>

![Module3Chapter2step9imb](images/module3chapter2step9imb.PNG)

11. <span data-ttu-id="275da-144">Importez le package personnalisé appelé SharingAssetCollection qui peut être téléchargé [ici.](https://github.com/microsoft/MixedRealityLearning/releases/tag/development)</span><span class="sxs-lookup"><span data-stu-id="275da-144">Import the custom package called SharingAssetCollection which can be downloaded [here.](https://github.com/microsoft/MixedRealityLearning/releases/tag/development)</span></span>

![Module3Chapter2step12im](images/module3chapter2step11im.PNG)

12. <span data-ttu-id="275da-146">Dans le panneau projet, accédez au dossier Prefabs.</span><span class="sxs-lookup"><span data-stu-id="275da-146">In the Project panel, go to the Prefabs folder.</span></span> <span data-ttu-id="275da-147">Dans les étapes suivantes, vous allez implémenter quelques prefabs dans la scène.</span><span class="sxs-lookup"><span data-stu-id="275da-147">In next few steps you implement a few prefabs into the scene.</span></span> <span data-ttu-id="275da-148">Dans le dossier Prefabs, cliquez sur la fenêtre de débogage Prefab, puis faites-la glisser dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="275da-148">In the Prefabs folder, click and drag the prefab, Debug Window into the hierarchy.</span></span> <span data-ttu-id="275da-149">Une fois que vous avez terminé, enregistrez le projet en cliquant sur fichier, puis sur enregistrer ou appuyez sur CTRL + S.</span><span class="sxs-lookup"><span data-stu-id="275da-149">Once finished, save the project by clicking File, then Save or press Control+S.</span></span>

![Module3Chapter2step12im](images/module3chapter2step12im.PNG)

   > <span data-ttu-id="275da-151">Remarque : Vous pouvez remarquer qu’une fenêtre contextuelle s’affiche lorsque vous cliquez sur le Prefab, qui vous demande des informations sur TMP Essentials.</span><span class="sxs-lookup"><span data-stu-id="275da-151">Note: You may notice a pop-up appear as you click on the prefab, asking you about TMP Essentials.</span></span> <span data-ttu-id="275da-152">Cliquez sur Importer les bases TMP comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="275da-152">Click Import TMP Essentials as they are needed.</span></span> <span data-ttu-id="275da-153">Si cette fenêtre contextuelle s’affiche, vous devrez peut-être supprimer le Prefab de votre hiérarchie et le faire glisser à nouveau dans votre hiérarchie pour éviter les erreurs liées au texte potentiel.</span><span class="sxs-lookup"><span data-stu-id="275da-153">If this pop-up appears, you might need to delete the prefab from your hierarchy and re-drag it into your hierarchy to avoid potential text-related errors.</span></span>
   >
>![Module3Chapter2note2im](images/module3chapter2note2im.PNG)


## <a name="congratulations"></a><span data-ttu-id="275da-155">Félicitations</span><span class="sxs-lookup"><span data-stu-id="275da-155">Congratulations</span></span>

<span data-ttu-id="275da-156">Votre projet Unity est maintenant prêt pour la photonique.</span><span class="sxs-lookup"><span data-stu-id="275da-156">Your Unity Project is now ready for Photon.</span></span> <span data-ttu-id="275da-157">Dans les didacticiels à venir, nous nous appuyons sur cette scène et notre projet Unity vers une expérience partagée complète.</span><span class="sxs-lookup"><span data-stu-id="275da-157">In the coming tutorials, we'll build upon this scene and our Unity project towards a full shared experience.</span></span>

<span data-ttu-id="275da-158">[Didacticiel suivant: 3. Connexion de plusieurs utilisateurs](mrlearning-sharing(photon)-ch3.md)</span><span class="sxs-lookup"><span data-stu-id="275da-158">[Next tutorial: 3. Connecting multiple users](mrlearning-sharing(photon)-ch3.md)</span></span>

