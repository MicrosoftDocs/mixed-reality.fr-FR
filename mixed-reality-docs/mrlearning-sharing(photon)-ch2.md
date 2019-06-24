---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 957813d24de95aad52c26b4bd0f0996a60d01358
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67326602"
---
# <a name="getting-unity-ready-for-development"></a><span data-ttu-id="93544-104">**Préparation de Unity pour le développement**</span><span class="sxs-lookup"><span data-stu-id="93544-104">**Getting Unity Ready for Development**</span></span> 

<span data-ttu-id="93544-105">Dans cette leçon, nous allez apprendre à préparer et configurer Unity pour le développement d’applications, y compris l’importation de la boîte à outils de réalité mixte, la configuration des paramètres de build et la préparation de notre scène.</span><span class="sxs-lookup"><span data-stu-id="93544-105">In this lesson, we will learn how to prepare and configure Unity for app development, including importing the Mixed Reality Toolkit, configuring build settings, and preparing our scene.</span></span>

<span data-ttu-id="93544-106">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="93544-106">Objectives:</span></span>

- <span data-ttu-id="93544-107">Configurer Unity pour le développement d’applications</span><span class="sxs-lookup"><span data-stu-id="93544-107">Configure Unity for app development</span></span>

- <span data-ttu-id="93544-108">Importer le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="93544-108">Import the Mixed Reality Toolkit</span></span>

- <span data-ttu-id="93544-109">Préparer votre scène du projet</span><span class="sxs-lookup"><span data-stu-id="93544-109">Prepare your project scene</span></span>

### <a name="instructions"></a><span data-ttu-id="93544-110">Instructions</span><span class="sxs-lookup"><span data-stu-id="93544-110">Instructions</span></span>

1. <span data-ttu-id="93544-111">Téléchargez et enregistrez le package unity Toolkit de réalité mixte en cliquant sur [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1-Refresh/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC1-Refresh.unitypackage)</span><span class="sxs-lookup"><span data-stu-id="93544-111">Download and save the Mixed Reality Toolkit unity package by clicking [here.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1-Refresh/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC1-Refresh.unitypackage)</span></span>
2. <span data-ttu-id="93544-112">Dans Unity, cliquez sur le menu de ressources et sélectionnez « Importer un Package », puis cliquez sur « Custom Package ».</span><span class="sxs-lookup"><span data-stu-id="93544-112">In Unity, click on the assets menu and select "Import Package," then click on "Custom Package."</span></span>

![Module3Chapter2step2im](images/module3chapter2step2im.PNG)

3. <span data-ttu-id="93544-114">Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="93544-114">Select the Unity package you just downloaded from the link provided in step 1.</span></span> <span data-ttu-id="93544-115">Une fois que la fenêtre contextuelle d’importation s’affiche dans Unity, cliquez sur le bouton Importer pour commencer l’importation.</span><span class="sxs-lookup"><span data-stu-id="93544-115">Once the import pop-up window appears in Unity, click the import button to begin importing.</span></span> <span data-ttu-id="93544-116">L’importation du MRTK peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="93544-116">Importing the MRTK may take several minutes.</span></span>

![Module3Chapter2step3im](images/module3chapter2step3im.PNG)

> <span data-ttu-id="93544-118">Remarque: Le package téléchargé sera dans votre dossier local où vous avez enregistré le fichier.</span><span class="sxs-lookup"><span data-stu-id="93544-118">Note: The downloaded package will be in your local folder where you have saved the file.</span></span> <span data-ttu-id="93544-119">L’image ci-dessus ne transmettent pas où vous trouverez le package.</span><span class="sxs-lookup"><span data-stu-id="93544-119">The image above does not portray where you will find the package.</span></span>

4. <span data-ttu-id="93544-120">Créer une nouvelle scène (cela est possible en cliquant sur « fichier » et en sélectionnant « nouvelle scène »).</span><span class="sxs-lookup"><span data-stu-id="93544-120">Create a new scene (this can be done by clicking "file" and selecting "new scene").</span></span> <span data-ttu-id="93544-121">Enregistrer la scène en tant que « HLSharedProjectMain ».</span><span class="sxs-lookup"><span data-stu-id="93544-121">Save the scene as "HLSharedProjectMain."</span></span>

> <span data-ttu-id="93544-122">Remarque : vous pouvez recevoir une fenêtre contextuelle qui ressemble à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="93544-122">Note: you may receive a pop-up that looks similar to the image below.</span></span> <span data-ttu-id="93544-123">Pour l’instant, cliquez simplement sur « non ».</span><span class="sxs-lookup"><span data-stu-id="93544-123">For now, just click "No."</span></span>
>
> ![Module3Chapter2note1im](images/module3chapter2note1im.PNG)

5. <span data-ttu-id="93544-125">Sous « Toolkit de réalité mixte », cliquez sur « Ajouter à la scène et configurer ».</span><span class="sxs-lookup"><span data-stu-id="93544-125">Under "Mixed Reality Toolkit" click on "add to scene and configure."</span></span>

![Module3Chapter2step5im](images/module3chapter2step5im.PNG)

6. <span data-ttu-id="93544-127">Une fois cette opération terminée, un nouveau fichier de configuration s’affiche, ce qui vous donne la possibilité de personnaliser le profil.</span><span class="sxs-lookup"><span data-stu-id="93544-127">Once that is complete, a new configuration file will appear, giving you the choice to customize the profile.</span></span> <span data-ttu-id="93544-128">Cliquez sur « Copier et la personnaliser. »</span><span class="sxs-lookup"><span data-stu-id="93544-128">Click "copy and customize."</span></span>

![Module3Chapter2step6im](images/module3chapter2step6im.PNG)

7. <span data-ttu-id="93544-130">Défiler vers le bas et décochez la case « Activer le système de diagnostic » si vous souhaitez masquer la fenêtre diagnostics.</span><span class="sxs-lookup"><span data-stu-id="93544-130">Scroll down and uncheck "enable diagnostics system" if you would like to hide the diagnostics window.</span></span> <span data-ttu-id="93544-131">Nous recommandons de conserver la fenêtre diagnostics activés pendant le développement de l’application pour surveiller les performances et la désactivation lors des démonstrations de production ou d’application.</span><span class="sxs-lookup"><span data-stu-id="93544-131">We recommend keeping the diagnostics window enabled during app development to monitor performance, and disabling it during production or application demonstrations.</span></span>

![Module3Chapter2step7im](images/module3chapter2step7im.PNG)

8. <span data-ttu-id="93544-133">Ouvrez les paramètres de build en appuyant sur CTRL + MAJ + B ou en accédant au fichier > Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="93544-133">Open the build settings by pressing control+shift+B or going to File>Build Settings.</span></span> <span data-ttu-id="93544-134">Notez que le programme est actuellement défini sous la plateforme « PC, Mac et Linux autonome ».</span><span class="sxs-lookup"><span data-stu-id="93544-134">Notice that the program is currently set under the "PC, Mac and Linux standalone" platform.</span></span> <span data-ttu-id="93544-135">Pour le développement HoloLens 2, définissez la plateforme pour être « Plateforme Windows universelle ».</span><span class="sxs-lookup"><span data-stu-id="93544-135">For HoloLens 2 development, set the platform to be "Universal Windows Platform."</span></span> <span data-ttu-id="93544-136">Sélectionnez-le et cliquez sur « commutateur plateforme. »</span><span class="sxs-lookup"><span data-stu-id="93544-136">Select it and click "switch platform."</span></span>

   ![Module3Chapter2step8im](images/module3chapter2step8im.PNG)

   9. <span data-ttu-id="93544-138">Une fois terminé, cliquez sur la zone intitulée « Ajouter des scènes open ».</span><span class="sxs-lookup"><span data-stu-id="93544-138">Once complete, click the box that says "add open scenes."</span></span> <span data-ttu-id="93544-139">Accédez à présent le panneau Inspecteur et vérifiez que la case à cocher à droite de la « réalité virtuelle pris en charge » (comme indiqué dans l’image ci-dessous) est activée.</span><span class="sxs-lookup"><span data-stu-id="93544-139">Now go to the inspector panel and ensure that the check box to the right of "virtual reality supported" (as shown in the image below) is checked.</span></span> <span data-ttu-id="93544-140">Vérifiez également que la case à cocher en regard de « arrière-plan/HLSharedProjectMain » est également activée, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="93544-140">Also ensure that the check box next to "scenes/HLSharedProjectMain" is also checked, as shown in the image below.</span></span>

   ![Module3Chapter2step9im](images/module3chapter2step9im.PNG)

   10. <span data-ttu-id="93544-142">Sous « Paramètres de publication » section dans le panneau d’inspecteur défiler « Fonctionnalités » et vérifiez que les cases à cocher suivantes sont marqués :</span><span class="sxs-lookup"><span data-stu-id="93544-142">Under the "Publishing Settings" section in the inspector panel scroll down to "Capabilities" and ensure the following check boxes are marked:</span></span>
    - <span data-ttu-id="93544-143">client Internet</span><span class="sxs-lookup"><span data-stu-id="93544-143">internet client</span></span>
       
       - <span data-ttu-id="93544-144">internet client server</span><span class="sxs-lookup"><span data-stu-id="93544-144">internet client server</span></span>
       
       - <span data-ttu-id="93544-145">serveur client de réseau privé</span><span class="sxs-lookup"><span data-stu-id="93544-145">private network client server</span></span>
   
       - <span data-ttu-id="93544-146">camera/webcam</span><span class="sxs-lookup"><span data-stu-id="93544-146">camera/webcam</span></span>

       - <span data-ttu-id="93544-147">Microphone</span><span class="sxs-lookup"><span data-stu-id="93544-147">microphone</span></span>
   
   11. <span data-ttu-id="93544-148">Importer le package personnalisé appelé « Lesson2 », qui peut être téléchargé ici.</span><span class="sxs-lookup"><span data-stu-id="93544-148">Import the custom package called "Lesson2" which can be downloaded here.</span></span> <span data-ttu-id="93544-149">TODO : Fournir un lien vers le pack de ressources.</span><span class="sxs-lookup"><span data-stu-id="93544-149">TODO: Provide link to asset pack.</span></span>
   
   ![Module3Chapter2step12im](images/module3chapter2step11im.PNG)
   
   12. <span data-ttu-id="93544-151">Désormais, dans le volet de projet, aller sur le dossier « prefabs », étant donné que dans les prochaines étapes, vous allez implémenter quelques prefabs dans la scène.</span><span class="sxs-lookup"><span data-stu-id="93544-151">Now, in the project panel, go to the "prefabs" folder, since in next few steps you will be implementing a few prefabs into the scene.</span></span> <span data-ttu-id="93544-152">Dans le dossier « prefabs », cliquez et faites glisser le préfabriqué, « DebugWindow » dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="93544-152">In the "prefabs" folder, click and drag the prefab, "DebugWindow" into the hierarchy.</span></span> <span data-ttu-id="93544-153">Une fois que vous avez terminé, enregistrez le projet (cliquez sur fichier, puis enregistrer, ou appuyez sur CTRL + S)</span><span class="sxs-lookup"><span data-stu-id="93544-153">Once finished, save the project (click file, then save, or press control+S)</span></span>
   
       ![Module3Chapter2step12im](images/module3chapter2step12im.PNG)
   
   > <span data-ttu-id="93544-155">Remarque: Vous pouvez remarquer une fenêtre contextuelle s’affichent lorsque vous cliquez sur le préfabriqué, vous demandant sur TMP Essentials.</span><span class="sxs-lookup"><span data-stu-id="93544-155">Note: You may notice a pop-up appear as you click on the prefab, asking you about TMP Essentials.</span></span> <span data-ttu-id="93544-156">Cliquez sur « Importation TMP Essentials » car ils vous seront utiles.</span><span class="sxs-lookup"><span data-stu-id="93544-156">Click "Import TMP Essentials" as they will be needed.</span></span> <span data-ttu-id="93544-157">Si cette fenêtre contextuelle s’affiche, vous devrez peut-être supprimer le préfabriqué à partir de votre hiérarchie et de nouveau la faire glisser vers votre hiérarchie afin d’éviter les erreurs potentielles liées au texte.</span><span class="sxs-lookup"><span data-stu-id="93544-157">If this pop-up appears, you may need to delete the prefab from your hierarchy and re-drag it into your hierarchy to avoid potential text-related errors.</span></span>
   >
   > ![Module3Chapter2note2im](images/module3chapter2note2im.PNG)


## <a name="congratulations"></a><span data-ttu-id="93544-159">Félicitations</span><span class="sxs-lookup"><span data-stu-id="93544-159">Congratulations</span></span>

<span data-ttu-id="93544-160">Votre projet Unity est maintenant prêt pour Photon !</span><span class="sxs-lookup"><span data-stu-id="93544-160">Your Unity Project is now ready for Photon!</span></span> <span data-ttu-id="93544-161">Dans les leçons venir, nous allons créer cette scène et notre projet Unity vers une expérience complète partagée.</span><span class="sxs-lookup"><span data-stu-id="93544-161">In the coming lessons, we'll build upon this scene and our Unity project towards a full shared experience.</span></span>

<span data-ttu-id="93544-162">[Leçon suivante : Sharing(Photon) leçon 3](mrlearning-sharing(photon)-ch3.md)</span><span class="sxs-lookup"><span data-stu-id="93544-162">[Next Lesson: Sharing(Photon) Lesson 3](mrlearning-sharing(photon)-ch3.md)</span></span>

