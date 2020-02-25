---
title: Didacticiels sur les fonctionnalités multi-utilisateur-2. Obtention d’Unity prête pour le développement
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 2bcec7e70949186c6e711120c36ee8649c006ec7
ms.sourcegitcommit: bd536f4f99c71418b55c121b7ba19ecbaf6336bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "77553833"
---
# <a name="2-getting-unity-ready-for-development"></a><span data-ttu-id="109f2-105">2. obtention d’Unity prête pour le développement</span><span class="sxs-lookup"><span data-stu-id="109f2-105">2. Getting Unity ready for development</span></span>

<span data-ttu-id="109f2-106">Dans ce didacticiel, vous allez apprendre à préparer et à configurer Unity pour le développement d’applications, notamment l’importation de la boîte à outils de réalité mixte, la configuration des paramètres de génération et la préparation de votre scène.</span><span class="sxs-lookup"><span data-stu-id="109f2-106">In this tutorial, you will learn how to prepare and configure Unity for application development, including importing the Mixed Reality Toolkit, configuring build settings, and preparing your scene.</span></span>

## <a name="objectives"></a><span data-ttu-id="109f2-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="109f2-107">Objectives</span></span>

* <span data-ttu-id="109f2-108">Configurer Unity pour le développement d’applications</span><span class="sxs-lookup"><span data-stu-id="109f2-108">Configure Unity for application development</span></span>
* <span data-ttu-id="109f2-109">Importer le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="109f2-109">Import the Mixed Reality Toolkit</span></span>
* <span data-ttu-id="109f2-110">Préparer la scène de votre projet</span><span class="sxs-lookup"><span data-stu-id="109f2-110">Prepare your project scene</span></span>

## <a name="instructions"></a><span data-ttu-id="109f2-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="109f2-111">Instructions</span></span>

1. <span data-ttu-id="109f2-112">Téléchargez et enregistrez le package d’Unity pour la réalité mixte en cliquant [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.3.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage)</span><span class="sxs-lookup"><span data-stu-id="109f2-112">Download and save the Mixed Reality Toolkit Foundation unity package by clicking [here.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.3.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage)</span></span>

2. <span data-ttu-id="109f2-113">Dans Unity, cliquez sur le menu composants, sélectionnez Importer un package, puis cliquez sur package personnalisé.</span><span class="sxs-lookup"><span data-stu-id="109f2-113">In Unity, click the Assets menu and select Import Package, then click on Custom Package.</span></span>

    ![Module3Chapter2step2im](images/module3chapter2step2im.PNG)

3. <span data-ttu-id="109f2-115">Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="109f2-115">Select the Unity package you just downloaded from the link provided in step 1.</span></span> <span data-ttu-id="109f2-116">Une fois que la fenêtre contextuelle d’importation s’affiche dans Unity, cliquez sur le bouton Importer pour commencer l’importation de la MRTK.</span><span class="sxs-lookup"><span data-stu-id="109f2-116">Once the import pop-up window appears in Unity, click the Import button to begin importing the MRTK.</span></span> <span data-ttu-id="109f2-117">Cette opération peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="109f2-117">This may take several minutes.</span></span>

    ![Module3Chapter2step3im](images/module3chapter2step3im.PNG)

    >[!NOTE]
    ><span data-ttu-id="109f2-119">Le package téléchargé se trouve dans votre dossier local, où vous avez enregistré le fichier.</span><span class="sxs-lookup"><span data-stu-id="109f2-119">The downloaded package is in your local folder, where you have saved the file.</span></span> <span data-ttu-id="109f2-120">L’image ci-dessus ne décrit pas où se trouve le package.</span><span class="sxs-lookup"><span data-stu-id="109f2-120">The image above does not portray where you will find the package.</span></span>

    <span data-ttu-id="109f2-121">Une fois le package importé, la fenêtre du configurateur de projet MRTK doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="109f2-121">After the package has been imported, the MRTK Project Configurator window should appear.</span></span> <span data-ttu-id="109f2-122">Si ce n’est pas le cas, ouvrez-le en sélectionnant Mixed Reality Toolkit > Utilities > configurer le projet Unity dans le menu Unity.</span><span class="sxs-lookup"><span data-stu-id="109f2-122">If it does not, open it by selecting Mixed Reality Toolkit > Utilities > Configure Unity Project in the Unity menu.</span></span>

    <span data-ttu-id="109f2-123">Dans la fenêtre du Configurateur de projet MRTK, développez la section modifier les configurations, décochez la case Activer MSBuild pour Unity, vérifiez que toutes les autres options sont cochées, puis cliquez sur le bouton appliquer pour appliquer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="109f2-123">In the MRTK Project Configurator window, expand the Modify Configurations section, uncheck the Enable MSBuild for Unity checkbox, ensure all other options are checked, and click the Apply button to apply the settings.</span></span>

    ![Module3Chapter2note1im](images/module3chapter2note1im-missing01.png)

    > [!CAUTION]
    > <span data-ttu-id="109f2-125">MSBuild for Unity ne prend peut-être pas en charge tous les SDK que vous utiliserez et peut être difficile à désactiver une fois qu’il a été activé.</span><span class="sxs-lookup"><span data-stu-id="109f2-125">MSBuild for Unity may not support all SDKs you will be using and can be challenging to disable after it has been enabled.</span></span> <span data-ttu-id="109f2-126">Par conséquent, il est vivement recommandé de ne pas activer MSBuild for Unity.</span><span class="sxs-lookup"><span data-stu-id="109f2-126">Consequently, it is strongly recommended to not enable MSBuild for Unity.</span></span>
    
4. <span data-ttu-id="109f2-127">Créez une nouvelle scène.</span><span class="sxs-lookup"><span data-stu-id="109f2-127">Create a new scene.</span></span> <span data-ttu-id="109f2-128">Pour ce faire, cliquez sur fichier et sélectionnez nouvelle scène.</span><span class="sxs-lookup"><span data-stu-id="109f2-128">This can be done by clicking File and selecting New Scene".</span></span> <span data-ttu-id="109f2-129">Enregistrez-le en tant que HLSharedProjectMain.</span><span class="sxs-lookup"><span data-stu-id="109f2-129">Save it as HLSharedProjectMain.</span></span>

5. <span data-ttu-id="109f2-130">Dans la boîte à outils de réalité mixte, cliquez sur Ajouter à la scène et configurer.</span><span class="sxs-lookup"><span data-stu-id="109f2-130">Under Mixed Reality Toolkit, click on Add to Scene and Configure.</span></span>

    ![Module3Chapter2step5im](images/module3chapter2step5im.PNG)

6. <span data-ttu-id="109f2-132">Une fois cette opération terminée, sélectionnez la boîte à outils de réalité mixte (MRTK) dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="109f2-132">Once that is complete, select Mixed-Reality Toolkit (MRTK) from the hierarchy.</span></span> <span data-ttu-id="109f2-133">Dans le volet de l’inspecteur, remplacez le profil de configuration MRTK par DefaultHoloLens2ConfigurationProfile.</span><span class="sxs-lookup"><span data-stu-id="109f2-133">In the inspector panel, change the MRTK configuration profile to DefaultHoloLens2ConfigurationProfile.</span></span>

    ![Module2Chapter1step4ima](images/Module2Chapter1step4ima-missing01.png)

7. <span data-ttu-id="109f2-135">Sélectionnez la boîte à outils de réalité mixte (MRTK) dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="109f2-135">Select Mixed-Reality Toolkit (MRTK) from the  hierarchy.</span></span> <span data-ttu-id="109f2-136">Dans le volet de l’inspecteur, recherchez le script Mixed Reality Toolkit, puis appuyez sur le bouton « Copier & Personnaliser », comme indiqué dans la figure ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="109f2-136">In the inspector panel, look for the Mixed Reality Toolkit Script and press the "Copy & Customize" button  as shown in the figure below.</span></span>  <span data-ttu-id="109f2-137">Une liste déroulante s’affiche après cela et sélectionnez l’option cloner dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="109f2-137">A pop will appear after this and select clone option in the pop up menu.</span></span>

    ![Module3Chapter2step6imc](images/module3chapter2step6imc.PNG)

    ![Module3Chapter2step6imd](images/module3chapter2step6imd.PNG)

8. <span data-ttu-id="109f2-140">Faites défiler vers le dessous et décochez activer le système de diagnostic si vous souhaitez masquer la fenêtre de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="109f2-140">Scroll down and uncheck Enable Diagnostics system if you want to hide the diagnostics window.</span></span> <span data-ttu-id="109f2-141">Nous vous recommandons de laisser la fenêtre de diagnostics activée pendant le développement d’applications pour surveiller les performances, puis la désactiver pendant les démonstrations de production ou d’application.</span><span class="sxs-lookup"><span data-stu-id="109f2-141">We recommend keeping the diagnostics window enabled during application development to monitor performance, and then disabling it during production or application demonstrations.</span></span> 

    ![Module3Chapter2step7ima](images/module3chapter2step7ima.PNG)

9. <span data-ttu-id="109f2-143">Ouvrez les paramètres de build en appuyant sur Ctrl + Maj + B ou en accédant à fichier-> paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="109f2-143">Open the build settings by pressing control+shift+B or going to File->Build Settings.</span></span> <span data-ttu-id="109f2-144">Notez que le programme est actuellement défini sous la plateforme autonome PC, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="109f2-144">Notice that the program is currently set under the PC, Mac and Linux standalone platform.</span></span> <span data-ttu-id="109f2-145">Pour le développement HoloLens 2, définissez la plateforme sur plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="109f2-145">For HoloLens 2 development, set the platform to be Universal Windows Platform.</span></span> <span data-ttu-id="109f2-146">Sélectionnez-le, puis cliquez sur basculer la plateforme.</span><span class="sxs-lookup"><span data-stu-id="109f2-146">Select it and click Switch Platform.</span></span>

    ![Module3Chapter2step8im](images/module3chapter2step8im.PNG)

10. <span data-ttu-id="109f2-148">Une fois terminé, cliquez sur la zone intitulée ajouter des scènes ouvertes.</span><span class="sxs-lookup"><span data-stu-id="109f2-148">Once complete, click the box called Add Open Scenes.</span></span> <span data-ttu-id="109f2-149">Maintenant, accédez au panneau de l’inspecteur et vérifiez que la case à cocher située à droite de la réalité virtuelle prise en charge (comme indiqué dans l’image ci-dessous) est activée.</span><span class="sxs-lookup"><span data-stu-id="109f2-149">Now go to the Inspector panel and ensure that the check box to the right of Virtual Reality Supported (as shown in the image below) is checked.</span></span> <span data-ttu-id="109f2-150">Assurez-vous également que la case à cocher en regard de scenes/HLSharedProjectMain est également activée, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="109f2-150">Also ensure that the check box next to scenes/HLSharedProjectMain is also checked, as shown in the image below.</span></span>

    ![Module3Chapter2step9im](images/module3chapter2step9im.PNG)

11. <span data-ttu-id="109f2-152">Dans la section paramètres de publication du panneau Inspecteur, faites défiler l’écran jusqu’à fonctionnalités et vérifiez que les cases à cocher suivantes sont activées :</span><span class="sxs-lookup"><span data-stu-id="109f2-152">Under the Publishing Settings section in the Inspector panel, scroll down to Capabilities and ensure the following check boxes are marked:</span></span>

    ![Module3Chapter2step9imb](images/module3chapter2step9imb.PNG)

12. <span data-ttu-id="109f2-154">Importez les packages personnalisés listés :</span><span class="sxs-lookup"><span data-stu-id="109f2-154">Import the listed custom packages:</span></span>

    * <span data-ttu-id="109f2-155">[AzureSpatialAnchors. pour Unity](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)</span><span class="sxs-lookup"><span data-stu-id="109f2-155">[AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)</span></span>
    * [<span data-ttu-id="109f2-156">MRTK. HoloLens2. Unity. Tutorials. Assets. GettingStarted. 2.3.0.2. pour Unity</span><span class="sxs-lookup"><span data-stu-id="109f2-156">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.2/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage)
    * [<span data-ttu-id="109f2-157">MRTK. HoloLens2. Unity. Tutorials. Assets. AzureSpatialAnchors. 2.3.0.0. pour Unity</span><span class="sxs-lookup"><span data-stu-id="109f2-157">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.3.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.0.unitypackage)
    * [<span data-ttu-id="109f2-158">MRTK. HoloLens2. Unity. Tutorials. Assets. MultiUserCapabilities. 2.1.0.1. pour Unity</span><span class="sxs-lookup"><span data-stu-id="109f2-158">MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.1.0.1.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/multi-user-capabilities-v2.1.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.1.0.1.unitypackage)

    >[!TIP]
    ><span data-ttu-id="109f2-159">Pour obtenir un rappel sur la configuration d’un projet Unity pour les ancres spatiales Azure, vous pouvez consulter le didacticiel [prise en main d’ancres spatiales](https://docs.microsoft.com/windows/mixed-reality/mrlearning-asa-ch1) Azure, qui fait partie de la série de didacticiels sur les [ancres spatiales Azure](https://docs.microsoft.com/windows/mixed-reality/mrlearning-asa-ch1) .</span><span class="sxs-lookup"><span data-stu-id="109f2-159">For a reminder on how to configure a Unity project for Azure Spatial Anchors, you can refer to the [Getting started with Azure Spatial Anchors](https://docs.microsoft.com/windows/mixed-reality/mrlearning-asa-ch1) tutorial which is part of the the [Azure Spatial Anchors](https://docs.microsoft.com/windows/mixed-reality/mrlearning-asa-ch1) tutorial series.</span></span>


13. <span data-ttu-id="109f2-160">Dans le panneau projet, accédez au dossier Prefabs.</span><span class="sxs-lookup"><span data-stu-id="109f2-160">In the Project panel, go to the Prefabs folder.</span></span> <span data-ttu-id="109f2-161">Dans les étapes suivantes, vous allez implémenter quelques prefabs dans la scène.</span><span class="sxs-lookup"><span data-stu-id="109f2-161">In the following steps, you will implement a few prefabs into the scene.</span></span> <span data-ttu-id="109f2-162">Dans le dossier Prefabs, cliquez sur la fenêtre de débogage Prefab, puis faites-la glisser dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="109f2-162">In the Prefabs folder, click and drag the prefab, Debug Window into the hierarchy.</span></span> <span data-ttu-id="109f2-163">Une fois que vous avez terminé, enregistrez le projet en cliquant sur fichier, puis sur enregistrer ou appuyez sur CTRL + S.</span><span class="sxs-lookup"><span data-stu-id="109f2-163">Once finished, save the project by clicking File, then Save or press Control+S.</span></span>

    ![Module3Chapter2step12im](images/module3chapter2step12im.PNG)

    <span data-ttu-id="109f2-165">Vous pouvez remarquer qu’une fenêtre contextuelle s’affiche lorsque vous cliquez sur le Prefab, qui vous demande des informations sur TMP Essentials.</span><span class="sxs-lookup"><span data-stu-id="109f2-165">You may notice a pop-up appear as you click on the prefab, asking you about TMP Essentials.</span></span> <span data-ttu-id="109f2-166">Cliquez sur Importer les bases TMP comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="109f2-166">Click Import TMP Essentials as they are needed.</span></span> <span data-ttu-id="109f2-167">Si cette fenêtre contextuelle s’affiche, vous devrez peut-être supprimer le Prefab de votre hiérarchie et le faire glisser à nouveau dans votre hiérarchie pour éviter les erreurs liées au texte potentiel.</span><span class="sxs-lookup"><span data-stu-id="109f2-167">If this pop-up appears, you might need to delete the prefab from your hierarchy and re-drag it into your hierarchy to avoid potential text-related errors.</span></span>

    ![Module3Chapter2note2im](images/module3chapter2note2im.PNG)

## <a name="congratulations"></a><span data-ttu-id="109f2-169">Félicitations</span><span class="sxs-lookup"><span data-stu-id="109f2-169">Congratulations</span></span>

<span data-ttu-id="109f2-170">Votre projet Unity est maintenant prêt pour la photonique.</span><span class="sxs-lookup"><span data-stu-id="109f2-170">Your Unity Project is now ready for Photon.</span></span> <span data-ttu-id="109f2-171">Dans les didacticiels à venir, nous nous appuyons sur cette scène et notre projet Unity vers une expérience partagée complète.</span><span class="sxs-lookup"><span data-stu-id="109f2-171">In the coming tutorials, we'll build upon this scene and our Unity project towards a full shared experience.</span></span>

<span data-ttu-id="109f2-172">[Didacticiel suivant : 3. connexion de plusieurs utilisateurs](mrlearning-sharing(photon)-ch3.md)</span><span class="sxs-lookup"><span data-stu-id="109f2-172">[Next tutorial: 3. Connecting multiple users](mrlearning-sharing(photon)-ch3.md)</span></span>
