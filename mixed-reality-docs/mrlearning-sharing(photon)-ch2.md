# <a name="getting-unity-ready-for-development"></a><span data-ttu-id="dec19-101">Préparation de Unity pour le développement</span><span class="sxs-lookup"><span data-stu-id="dec19-101">Getting Unity ready for development</span></span> 

<span data-ttu-id="dec19-102">Dans ce didacticiel, nous Découvrez comment préparer et configurer Unity pour le développement d’applications, y compris l’importation de la boîte à outils de réalité mixte, la configuration des paramètres de build et la préparation de notre scène.</span><span class="sxs-lookup"><span data-stu-id="dec19-102">In this tutorial, we learn how to prepare and configure Unity for applicaiton development, including importing the Mixed Reality Toolkit, configuring build settings, and preparing our scene.</span></span>

<span data-ttu-id="dec19-103">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="dec19-103">Objectives:</span></span>

- <span data-ttu-id="dec19-104">Configurer Unity pour le développement d’applications</span><span class="sxs-lookup"><span data-stu-id="dec19-104">Configure Unity for applicaiton development</span></span>

- <span data-ttu-id="dec19-105">Importer le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="dec19-105">Import the Mixed Reality Toolkit</span></span>

- <span data-ttu-id="dec19-106">Préparer votre scène du projet</span><span class="sxs-lookup"><span data-stu-id="dec19-106">Prepare your project scene</span></span>

### <a name="instructions"></a><span data-ttu-id="dec19-107">Instructions</span><span class="sxs-lookup"><span data-stu-id="dec19-107">Instructions</span></span>

1. <span data-ttu-id="dec19-108">Téléchargez et enregistrez le package unity Toolkit de réalité mixte en cliquant sur [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC2.1/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC2.1.unitypackage)</span><span class="sxs-lookup"><span data-stu-id="dec19-108">Download and save the Mixed Reality Toolkit unity package by clicking [here.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC2.1/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC2.1.unitypackage)</span></span>
2. <span data-ttu-id="dec19-109">Dans Unity, cliquez sur le menu de ressources, puis sélectionnez Importer un Package, cliquez sur le Package personnalisé.</span><span class="sxs-lookup"><span data-stu-id="dec19-109">In Unity, click on the assets menu and select Import Package, then click on Custom Package.</span></span>

![Module3Chapter2step2im](images/module3chapter2step2im.PNG)

3. <span data-ttu-id="dec19-111">Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="dec19-111">Select the Unity package you just downloaded from the link provided in step 1.</span></span> <span data-ttu-id="dec19-112">Une fois que la fenêtre contextuelle d’importation s’affiche dans Unity, cliquez sur le bouton Importer pour commencer l’importation.</span><span class="sxs-lookup"><span data-stu-id="dec19-112">Once the import pop-up window appears in Unity, click the Import button to begin importing.</span></span> <span data-ttu-id="dec19-113">L’importation du MRTK peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="dec19-113">Importing the MRTK may take several minutes.</span></span>

![Module3Chapter2step3im](images/module3chapter2step3im.PNG)

> <span data-ttu-id="dec19-115">Remarque: Le package téléchargé est dans votre dossier local où vous avez enregistré le fichier.</span><span class="sxs-lookup"><span data-stu-id="dec19-115">Note: The downloaded package is in your local folder where you have saved the file.</span></span> <span data-ttu-id="dec19-116">L’image ci-dessus ne transmettent pas où vous trouverez le package.</span><span class="sxs-lookup"><span data-stu-id="dec19-116">The image above does not portray where you will find the package.</span></span>

4. <span data-ttu-id="dec19-117">Créer une nouvelle scène.</span><span class="sxs-lookup"><span data-stu-id="dec19-117">Create a new scene.</span></span> <span data-ttu-id="dec19-118">Cet exemple est possible en cliquant sur fichier, puis en sélectionnant nouvelle scène »).</span><span class="sxs-lookup"><span data-stu-id="dec19-118">Tthis can be done by clicking File, and selecting New Scene").</span></span> <span data-ttu-id="dec19-119">Enregistrer la scène en tant que HLSharedProjectMain.</span><span class="sxs-lookup"><span data-stu-id="dec19-119">Save the scene as HLSharedProjectMain.</span></span>

> <span data-ttu-id="dec19-120">Remarque : vous pouvez recevoir une fenêtre contextuelle qui ressemble à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="dec19-120">Note: you may receive a pop-up that looks similar to the image below.</span></span> <span data-ttu-id="dec19-121">Pour l’instant, cliquez sur non.</span><span class="sxs-lookup"><span data-stu-id="dec19-121">For now, click No.</span></span>
>
> ![Module3Chapter2note1im](images/module3chapter2note1im.PNG)

5. <span data-ttu-id="dec19-123">Sous boîte à outils de réalité mixte, cliquez sur Ajouter à la scène et les configurer.</span><span class="sxs-lookup"><span data-stu-id="dec19-123">Under Mixed Reality Toolkit, click on Add to Scene and Configure.</span></span>

![Module3Chapter2step5im](images/module3chapter2step5im.PNG)

6. <span data-ttu-id="dec19-125">Une fois cette opération terminée, un nouveau fichier de configuration s’affiche, ce qui vous donne la possibilité de personnaliser le profil.</span><span class="sxs-lookup"><span data-stu-id="dec19-125">Once that is complete, a new configuration file appears, giving you the choice to customize the profile.</span></span> <span data-ttu-id="dec19-126">Cliquez sur Copier et personnaliser.</span><span class="sxs-lookup"><span data-stu-id="dec19-126">Click Copy and Customize.</span></span>

   ![Module3Chapter2step6ima](images/module3chapter2step6ima.PNG)

   ![Module3Chapter2step6imb](images/module3chapter2step6imb.PNG)

   ![Module3Chapter2step6imc](images/module3chapter2step6imc.PNG)

7. <span data-ttu-id="dec19-130">Défiler vers le bas et décochez la case Activer la Siagnostics système si vous souhaitez masquer la fenêtre de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="dec19-130">Scroll down and uncheck Enable Siagnostics system if you want to hide the diagnostics window.</span></span> <span data-ttu-id="dec19-131">Nous recommandons de conserver la fenêtre diagnostics activés pendant le développement de l’application pour surveiller les performances et la désactivation lors des démonstrations de production ou d’application.</span><span class="sxs-lookup"><span data-stu-id="dec19-131">We recommend keeping the diagnostics window enabled during applicaiton development to monitor performance, and disabling it during production or application demonstrations.</span></span> 

   ![Module3Chapter2step7ima](images/module3chapter2step7ima.PNG)

8. <span data-ttu-id="dec19-133">Ouvrez les paramètres de build en appuyant sur CTRL + MAJ + B ou en accédant au fichier -> Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="dec19-133">Open the build settings by pressing control+shift+B or going to File->Build Settings.</span></span> <span data-ttu-id="dec19-134">Notez que le programme est actuellement défini sous la plateforme autonome PC, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="dec19-134">Notice that the program is currently set under the PC, Mac and Linux standalone platform.</span></span> <span data-ttu-id="dec19-135">Pour le développement HoloLens 2, définissez la plateforme soit la plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="dec19-135">For HoloLens 2 development, set the platform to be Universal Windows Platform.</span></span> <span data-ttu-id="dec19-136">Sélectionnez-le et cliquez sur la plateforme de commutation.</span><span class="sxs-lookup"><span data-stu-id="dec19-136">Select it and click Switch Platform.</span></span>![Module3Chapter2step8im](images/module3chapter2step8im.PNG)

9. <span data-ttu-id="dec19-138">Une fois terminé, cliquez sur la zone intitulée Ajouter un arrière-plan ouverte.</span><span class="sxs-lookup"><span data-stu-id="dec19-138">Once complete, click the box that says Add Open Scenes.</span></span> <span data-ttu-id="dec19-139">Maintenant passer à la fenêtre d’inspecteur et vérifiez que la case à cocher à droite de virtuel pris en charge de réalité (comme indiqué dans l’image ci-dessous) est cochée.</span><span class="sxs-lookup"><span data-stu-id="dec19-139">Now go to the Inspector panel, and ensure that the check box to the right of Virtual Reality Supported (as shown in the image below) is checked.</span></span> <span data-ttu-id="dec19-140">Assurez-vous également que la case à cocher en regard de l’arrière-plan/HLSharedProjectMain est cochée également de comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="dec19-140">Also ensure that the check box next to scenes/HLSharedProjectMain is also checked as shown in the image below.</span></span>![Module3Chapter2step9im](images/module3chapter2step9im.PNG)

10. <span data-ttu-id="dec19-142">Dans la section Paramètres de publication dans le panneau d’inspecteur, faites défiler jusqu'à fonctionnalités et vérifiez que les cases à cocher suivantes sont marquées :</span><span class="sxs-lookup"><span data-stu-id="dec19-142">Under the Publishing Settings section in the Inspector panel, scroll down to Capabilities, and ensure the following check boxes are marked:</span></span>![Module3Chapter2step9imb](images/module3chapter2step9imb.PNG)

11. <span data-ttu-id="dec19-144">Importer le package personnalisé appelé SharingAssetCollection qui peut être téléchargée [ici.](https://github.com/microsoft/MixedRealityLearning/releases/download/Sharing_2/SharingAssetCollection.unitypackage) ![Module3Chapter2step12im](images/module3chapter2step11im.PNG)</span><span class="sxs-lookup"><span data-stu-id="dec19-144">Import the custom package called SharingAssetCollection which can be downloaded [here.](https://github.com/microsoft/MixedRealityLearning/releases/download/Sharing_2/SharingAssetCollection.unitypackage)![Module3Chapter2step12im](images/module3chapter2step11im.PNG)</span></span>

12. <span data-ttu-id="dec19-145">Dans le volet de projet, accédez au dossier Prefabs.</span><span class="sxs-lookup"><span data-stu-id="dec19-145">In the Project panel, go to the Prefabs folder.</span></span> <span data-ttu-id="dec19-146">Dans les prochaines étapes vous implémenter quelques prefabs dans la scène.</span><span class="sxs-lookup"><span data-stu-id="dec19-146">In next few steps you implement a few prefabs into the scene.</span></span> <span data-ttu-id="dec19-147">Dans le dossier Prefabs, cliquez et faites glisser le préfabriqué, DebugWindow dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="dec19-147">In the Prefabs folder, click and drag the prefab, DebugWindow into the hierarchy.</span></span> <span data-ttu-id="dec19-148">Une fois que vous avez terminé, enregistrez le projet en clckin fichier, puis enregistrer ou appuyez sur CTRL + + S.</span><span class="sxs-lookup"><span data-stu-id="dec19-148">Once finished, save the project by clckin File, then Save or press Control+S.</span></span>

    ![Module3Chapter2step12im](images/module3chapter2step12im.PNG)

   > <span data-ttu-id="dec19-150">Remarque: Vous pouvez remarquer une fenêtre contextuelle s’affichent lorsque vous cliquez sur le préfabriqué, vous demandant sur TMP Essentials.</span><span class="sxs-lookup"><span data-stu-id="dec19-150">Note: You may notice a pop-up appear as you click on the prefab, asking you about TMP Essentials.</span></span> <span data-ttu-id="dec19-151">Cliquez sur Importer TMP Essentials car ils sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="dec19-151">Click Import TMP Essentials as they are needed.</span></span> <span data-ttu-id="dec19-152">Si cette fenêtre contextuelle s’affiche, vous devrez peut-être supprimer le préfabriqué à partir de votre hiérarchie et de nouveau la faire glisser vers votre hiérarchie afin d’éviter les erreurs potentielles liées au texte.</span><span class="sxs-lookup"><span data-stu-id="dec19-152">If this pop-up appears, you might need to delete the prefab from your hierarchy and re-drag it into your hierarchy to avoid potential text-related errors.</span></span>
   >
   > ![Module3Chapter2note2im](images/module3chapter2note2im.PNG)


## <a name="congratulations"></a><span data-ttu-id="dec19-154">Félicitations</span><span class="sxs-lookup"><span data-stu-id="dec19-154">Congratulations</span></span>

<span data-ttu-id="dec19-155">Votre projet Unity est maintenant prêt pour Photon.</span><span class="sxs-lookup"><span data-stu-id="dec19-155">Your Unity Project is now ready for Photon.</span></span> <span data-ttu-id="dec19-156">Dans les didacticiels venir, nous allons créer cette scène et notre projet Unity vers une expérience complète partagée.</span><span class="sxs-lookup"><span data-stu-id="dec19-156">In the coming tutorials, we'll build upon this scene and our Unity project towards a full shared experience.</span></span>

<span data-ttu-id="dec19-157">[Didacticiel suivant : Plusieurs utilisateurs qui se connectent](mrlearning-sharing(photon)-ch3.md)</span><span class="sxs-lookup"><span data-stu-id="dec19-157">[Next tutorial: Connecting multiple users](mrlearning-sharing(photon)-ch3.md)</span></span>

