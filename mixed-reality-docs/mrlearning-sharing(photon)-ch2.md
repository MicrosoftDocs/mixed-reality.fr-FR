---
title: Tutoriels sur les fonctionnalités multi-utilisateurs - 2. Préparation de Unity pour le développement
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: f7ae77d6978b5da860d890bcfe5b6f7c3d4640c8
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79031237"
---
# <a name="2-getting-unity-ready-for-development"></a><span data-ttu-id="2cf2c-105">2. Préparation de Unity pour le développement</span><span class="sxs-lookup"><span data-stu-id="2cf2c-105">2. Getting Unity ready for development</span></span>

<span data-ttu-id="2cf2c-106">Dans ce tutoriel, vous allez apprendre à préparer et à configurer Unity pour le développement d’applications, notamment à importer Mixed Reality Toolkit, à configurer des paramètres de génération et à préparer votre scène.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-106">In this tutorial, you will learn how to prepare and configure Unity for application development, including importing the Mixed Reality Toolkit, configuring build settings, and preparing your scene.</span></span>

## <a name="objectives"></a><span data-ttu-id="2cf2c-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2cf2c-107">Objectives</span></span>

* <span data-ttu-id="2cf2c-108">Configurer Unity pour le développement d’applications</span><span class="sxs-lookup"><span data-stu-id="2cf2c-108">Configure Unity for application development</span></span>
* <span data-ttu-id="2cf2c-109">Importer le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="2cf2c-109">Import the Mixed Reality Toolkit</span></span>
* <span data-ttu-id="2cf2c-110">Préparer la scène de votre projet</span><span class="sxs-lookup"><span data-stu-id="2cf2c-110">Prepare your project scene</span></span>

## <a name="instructions"></a><span data-ttu-id="2cf2c-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="2cf2c-111">Instructions</span></span>

1. <span data-ttu-id="2cf2c-112">Téléchargez et enregistrez le package Unity Mixed Reality Toolkit Foundation en cliquant [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.3.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage)</span><span class="sxs-lookup"><span data-stu-id="2cf2c-112">Download and save the Mixed Reality Toolkit Foundation unity package by clicking [here.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.3.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage)</span></span>

2. <span data-ttu-id="2cf2c-113">Dans Unity, cliquez sur le menu Assets, sélectionnez Import Package, puis cliquez sur Custom Package.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-113">In Unity, click the Assets menu and select Import Package, then click on Custom Package.</span></span>

    ![Module3Chapter2step2im](images/module3chapter2step2im.PNG)

3. <span data-ttu-id="2cf2c-115">Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-115">Select the Unity package you just downloaded from the link provided in step 1.</span></span> <span data-ttu-id="2cf2c-116">Une fois que la fenêtre contextuelle d’importation s’affiche dans Unity, cliquez sur le bouton Import pour commencer l’importation de MRTK.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-116">Once the import pop-up window appears in Unity, click the Import button to begin importing the MRTK.</span></span> <span data-ttu-id="2cf2c-117">Cette opération peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-117">This may take several minutes.</span></span>

    ![Module3Chapter2step3im](images/module3chapter2step3im.PNG)

    >[!NOTE]
    ><span data-ttu-id="2cf2c-119">Le package téléchargé se trouve dans votre dossier local, où vous avez enregistré le fichier.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-119">The downloaded package is in your local folder, where you have saved the file.</span></span> <span data-ttu-id="2cf2c-120">L’image ci-dessus ne reflète pas l’emplacement auquel vous allez trouver le package.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-120">The image above does not portray where you will find the package.</span></span>

    <span data-ttu-id="2cf2c-121">Une fois le package importé, la fenêtre du configurateur de projet MRTK doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-121">After the package has been imported, the MRTK Project Configurator window should appear.</span></span> <span data-ttu-id="2cf2c-122">Si ce n’est pas le cas, ouvrez-la en sélectionnant Mixed Reality Toolkit > Utilities > Configure Unity Project dans le menu Unity.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-122">If it does not, open it by selecting Mixed Reality Toolkit > Utilities > Configure Unity Project in the Unity menu.</span></span>

    <span data-ttu-id="2cf2c-123">Dans la fenêtre MRTK Project Configurator, développez la section Modify Configurations, décochez la case Enable MSBuild for Unity, vérifiez que toutes les autres options sont cochées et cliquez sur le bouton Apply pour appliquer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-123">In the MRTK Project Configurator window, expand the Modify Configurations section, uncheck the Enable MSBuild for Unity checkbox, ensure all other options are checked, and click the Apply button to apply the settings.</span></span>

    ![Module3Chapter2note1im](images/module3chapter2note1im-missing01.png)

    > [!CAUTION]
    > <span data-ttu-id="2cf2c-125">MSBuild for Unity ne prend peut-être pas en charge tous les SDK que vous utiliserez et peut être difficile à désactiver une fois qu’il a été activé.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-125">MSBuild for Unity may not support all SDKs you will be using and can be challenging to disable after it has been enabled.</span></span> <span data-ttu-id="2cf2c-126">Par conséquent, il est vivement recommandé de ne pas activer MSBuild for Unity.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-126">Consequently, it is strongly recommended to not enable MSBuild for Unity.</span></span>
    
4. <span data-ttu-id="2cf2c-127">Créez une scène.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-127">Create a new scene.</span></span> <span data-ttu-id="2cf2c-128">Pour cela, cliquez sur File et sélectionnez New scene.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-128">This can be done by clicking File and selecting New Scene".</span></span> <span data-ttu-id="2cf2c-129">Enregistrez-la sous HLSharedProjectMain.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-129">Save it as HLSharedProjectMain.</span></span>

5. <span data-ttu-id="2cf2c-130">Sous Mixed Reality Toolkit, cliquez sur Add to Scene and Configure.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-130">Under Mixed Reality Toolkit, click on Add to Scene and Configure.</span></span>

    ![Module3Chapter2step5im](images/module3chapter2step5im.PNG)

6. <span data-ttu-id="2cf2c-132">Une fois cette opération terminée, sélectionnez Mixed-Reality Toolkit (MRTK) dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-132">Once that is complete, select Mixed-Reality Toolkit (MRTK) from the hierarchy.</span></span> <span data-ttu-id="2cf2c-133">Dans le panneau de l’inspecteur, remplacez le profil de configuration MRTK par DefaultHoloLens2ConfigurationProfile.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-133">In the inspector panel, change the MRTK configuration profile to DefaultHoloLens2ConfigurationProfile.</span></span>

    ![Module2Chapter1step4ima](images/Module2Chapter1step4ima-missing01.png)

7. <span data-ttu-id="2cf2c-135">Sélectionnez Mixed-Reality Toolkit (MRTK) dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-135">Select Mixed-Reality Toolkit (MRTK) from the  hierarchy.</span></span> <span data-ttu-id="2cf2c-136">Dans le panneau de l’inspecteur, recherchez « Mixed Reality Toolkit Script » et appuyez sur le bouton « Copy & Customize », comme illustré dans la figure ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-136">In the inspector panel, look for the Mixed Reality Toolkit Script and press the "Copy & Customize" button  as shown in the figure below.</span></span>  <span data-ttu-id="2cf2c-137">Une fenêtre s’affiche ensuite. Sélectionnez l’option Clone.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-137">A pop will appear after this and select clone option in the pop up menu.</span></span>

    ![Module3Chapter2step6imc](images/module3chapter2step6imc.PNG)

    ![Module3Chapter2step6imd](images/module3chapter2step6imd.PNG)

8. <span data-ttu-id="2cf2c-140">Faites défiler l’écran pour décocher Enable Diagnostics System si vous voulez masquer la fenêtre de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-140">Scroll down and uncheck Enable Diagnostics system if you want to hide the diagnostics window.</span></span> <span data-ttu-id="2cf2c-141">Nous vous recommandons de laisser la fenêtre de diagnostic activée pendant le développement d’applications pour superviser les performances, puis de la désactiver pendant les démonstrations de production ou d’application.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-141">We recommend keeping the diagnostics window enabled during application development to monitor performance, and then disabling it during production or application demonstrations.</span></span> 

    ![Module3Chapter2step7ima](images/module3chapter2step7ima.PNG)

9. <span data-ttu-id="2cf2c-143">Ouvrez les paramètres de build en appuyant sur Ctrl+Maj+B ou en accédant à File->Build Settings.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-143">Open the build settings by pressing control+shift+B or going to File->Build Settings.</span></span> <span data-ttu-id="2cf2c-144">Notez que le programme est actuellement défini sous la plateforme autonome PC, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-144">Notice that the program is currently set under the PC, Mac and Linux standalone platform.</span></span> <span data-ttu-id="2cf2c-145">Pour le développement HoloLens 2, choisissez la plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-145">For HoloLens 2 development, set the platform to be Universal Windows Platform.</span></span> <span data-ttu-id="2cf2c-146">Sélectionnez-la, puis cliquez sur Switch Platform.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-146">Select it and click Switch Platform.</span></span>

    ![Module3Chapter2step8im](images/module3chapter2step8im.PNG)

10. <span data-ttu-id="2cf2c-148">Quand vous avez terminé, cliquez sur la zone nommée Add Open Scenes.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-148">Once complete, click the box called Add Open Scenes.</span></span> <span data-ttu-id="2cf2c-149">Maintenant, accédez au panneau Inspector pour vérifier que la case située à droite de Virtual Reality Supported (comme illustré dans l’image ci-dessous) est cochée.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-149">Now go to the Inspector panel and ensure that the check box to the right of Virtual Reality Supported (as shown in the image below) is checked.</span></span> <span data-ttu-id="2cf2c-150">Vérifiez aussi que la case en regard de scenes/HLSharedProjectMain est aussi cochée, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-150">Also ensure that the check box next to scenes/HLSharedProjectMain is also checked, as shown in the image below.</span></span>

    ![Module3Chapter2step9im](images/module3chapter2step9im.PNG)

11. <span data-ttu-id="2cf2c-152">Dans la section Publishing Settings du panneau Inspector, faites défiler l’écran jusqu’à Capabilities pour vérifier que les cases suivantes sont cochées :</span><span class="sxs-lookup"><span data-stu-id="2cf2c-152">Under the Publishing Settings section in the Inspector panel, scroll down to Capabilities and ensure the following check boxes are marked:</span></span>

    ![Module3Chapter2step9imb](images/module3chapter2step9imb.PNG)

12. <span data-ttu-id="2cf2c-154">Importez les packages personnalisés listés :</span><span class="sxs-lookup"><span data-stu-id="2cf2c-154">Import the listed custom packages:</span></span>

    * <span data-ttu-id="2cf2c-155">[AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)</span><span class="sxs-lookup"><span data-stu-id="2cf2c-155">[AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)</span></span>
    * [<span data-ttu-id="2cf2c-156">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage</span><span class="sxs-lookup"><span data-stu-id="2cf2c-156">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.2/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage)
    * [<span data-ttu-id="2cf2c-157">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.0.unitypackage</span><span class="sxs-lookup"><span data-stu-id="2cf2c-157">MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.3.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.0.unitypackage)
    * [<span data-ttu-id="2cf2c-158">MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.1.0.1.unitypackage</span><span class="sxs-lookup"><span data-stu-id="2cf2c-158">MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.1.0.1.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/multi-user-capabilities-v2.1.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.1.0.1.unitypackage)

    >[!TIP]
    ><span data-ttu-id="2cf2c-159">Pour obtenir un rappel sur la façon de configurer un projet Unity pour Azure Spatial Anchors, vous pouvez vous reporter au tutoriel [Bien démarrer avec Azure Spatial Anchors](https://docs.microsoft.com/windows/mixed-reality/mrlearning-asa-ch1) qui fait partie de la série de tutoriels sur [Azure Spatial Anchors](https://docs.microsoft.com/windows/mixed-reality/mrlearning-asa-ch1).</span><span class="sxs-lookup"><span data-stu-id="2cf2c-159">For a reminder on how to configure a Unity project for Azure Spatial Anchors, you can refer to the [Getting started with Azure Spatial Anchors](https://docs.microsoft.com/windows/mixed-reality/mrlearning-asa-ch1) tutorial which is part of the the [Azure Spatial Anchors](https://docs.microsoft.com/windows/mixed-reality/mrlearning-asa-ch1) tutorial series.</span></span>


13. <span data-ttu-id="2cf2c-160">Dans le panneau Project, accédez au dossier Prefabs.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-160">In the Project panel, go to the Prefabs folder.</span></span> <span data-ttu-id="2cf2c-161">Dans les étapes suivantes, vous allez implémenter quelques préfabriqués dans la scène.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-161">In the following steps, you will implement a few prefabs into the scene.</span></span> <span data-ttu-id="2cf2c-162">Dans le dossier Prefabs, cliquez sur le préfabriqué Debug Window pour le faire glisser dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-162">In the Prefabs folder, click and drag the prefab, Debug Window into the hierarchy.</span></span> <span data-ttu-id="2cf2c-163">Quand vous avez terminé, enregistrez le projet en cliquant sur File, puis sur Save ou en appuyant sur Ctrl+S.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-163">Once finished, save the project by clicking File, then Save or press Control+S.</span></span>

    ![Module3Chapter2step12im](images/module3chapter2step12im.PNG)

    <span data-ttu-id="2cf2c-165">Vous remarquerez peu-être qu’une fenêtre contextuelle s’affiche quand vous cliquez sur le préfabriqué, pour vous donner des informations sur TMP Essentials.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-165">You may notice a pop-up appear as you click on the prefab, asking you about TMP Essentials.</span></span> <span data-ttu-id="2cf2c-166">Cliquez sur Import TMP Essentials car cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-166">Click Import TMP Essentials as they are needed.</span></span> <span data-ttu-id="2cf2c-167">Si cette fenêtre contextuelle s’affiche, vous devrez peut-être supprimer le préfabriqué de votre hiérarchie et le faire glisser à nouveau dans votre hiérarchie pour éviter d’éventuelles erreurs liées au texte.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-167">If this pop-up appears, you might need to delete the prefab from your hierarchy and re-drag it into your hierarchy to avoid potential text-related errors.</span></span>

    ![Module3Chapter2note2im](images/module3chapter2note2im.PNG)

## <a name="congratulations"></a><span data-ttu-id="2cf2c-169">Félicitations</span><span class="sxs-lookup"><span data-stu-id="2cf2c-169">Congratulations</span></span>

<span data-ttu-id="2cf2c-170">Votre projet Unity est maintenant prêt pour Photon.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-170">Your Unity Project is now ready for Photon.</span></span> <span data-ttu-id="2cf2c-171">Dans les tutoriels à venir, nous allons nous appuyer sur cette scène pour faire de notre projet Unity une expérience partagée complète.</span><span class="sxs-lookup"><span data-stu-id="2cf2c-171">In the coming tutorials, we'll build upon this scene and our Unity project towards a full shared experience.</span></span>

<span data-ttu-id="2cf2c-172">[Tutoriel suivant : 3. Connexion de plusieurs utilisateurs](mrlearning-sharing(photon)-ch3.md)</span><span class="sxs-lookup"><span data-stu-id="2cf2c-172">[Next tutorial: 3. Connecting multiple users](mrlearning-sharing(photon)-ch3.md)</span></span>
