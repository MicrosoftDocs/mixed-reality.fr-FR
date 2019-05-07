---
title: MR Spatial 230 - mappage Spatial
description: Suivez cette procédure pas à pas à l’aide de Unity, Visual Studio et HoloLens pour connaître les détails des concepts de mappage spatial de codage.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, academy, didacticiel, mappage spatial, reconstruction aire de conception, de maillage
ms.openlocfilehash: ed58676a0fda660cc6b4c197239aeb53166baa4d
ms.sourcegitcommit: aa88f6b42aa8d83e43104b78964afb506a368fb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/02/2019
ms.locfileid: "64993558"
---
>[!NOTE]
><span data-ttu-id="30762-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="30762-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="30762-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="30762-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="30762-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="30762-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="30762-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="30762-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="30762-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="30762-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="30762-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="30762-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-spatial-230-spatial-mapping"></a><span data-ttu-id="30762-110">MR 230 spatiale : Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="30762-110">MR Spatial 230: Spatial mapping</span></span>

<span data-ttu-id="30762-111">[Mappage spatial](spatial-mapping.md) combine le monde réel et le monde virtuel par hologrammes sur l’environnement d’enseignement.</span><span class="sxs-lookup"><span data-stu-id="30762-111">[Spatial mapping](spatial-mapping.md) combines the real world and virtual world together by teaching holograms about the environment.</span></span> <span data-ttu-id="30762-112">Dans MR Spatial 230 (projet PLANÉTARIUM) nous apprendrons comment :</span><span class="sxs-lookup"><span data-stu-id="30762-112">In MR Spatial 230 (Project Planetarium) we'll learn how to:</span></span>

* <span data-ttu-id="30762-113">Analyser l’environnement et transférer des données à partir de la HoloLens sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="30762-113">Scan the environment and transfer data from the HoloLens to your development machine.</span></span>
* <span data-ttu-id="30762-114">Explorez les nuanceurs et découvrez comment les utiliser pour visualiser votre espace.</span><span class="sxs-lookup"><span data-stu-id="30762-114">Explore shaders and learn how to use them for visualizing your space.</span></span>
* <span data-ttu-id="30762-115">Décomposer la maille de salle dans les plans simples à l’aide du traitement de la maille.</span><span class="sxs-lookup"><span data-stu-id="30762-115">Break down the room mesh into simple planes using mesh processing.</span></span>
* <span data-ttu-id="30762-116">Accédez au-delà les techniques de sélection élective que vous avez appris dans [101 des principes fondamentaux de M.](holograms-101.md)et fournir des commentaires sur où un hologramme peut être placé dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="30762-116">Go beyond the placement techniques we learned in [MR Basics 101](holograms-101.md), and provide feedback about where a hologram can be placed in the environment.</span></span>
* <span data-ttu-id="30762-117">Explorez les effets de l’occlusion, donc lorsque votre hologramme est derrière un objet réel, vous pouvez le voir toujours avec vision rayons x !</span><span class="sxs-lookup"><span data-stu-id="30762-117">Explore occlusion effects, so when your hologram is behind a real-world object, you can still see it with x-ray vision!</span></span>

>[!VIDEO https://www.youtube.com/embed/NSNYRkUX6Mw]

## <a name="device-support"></a><span data-ttu-id="30762-118">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="30762-118">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="30762-119">Cours</span><span class="sxs-lookup"><span data-stu-id="30762-119">Course</span></span></th><th style="width:150px"> <span data-ttu-id="30762-120"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="30762-120"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="30762-121"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="30762-121"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="30762-122">MR 230 spatiale : Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="30762-122">MR Spatial 230: Spatial mapping</span></span></td><td style="text-align: center;"> <span data-ttu-id="30762-123">✔️</span><span class="sxs-lookup"><span data-stu-id="30762-123">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="30762-124">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="30762-124">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="30762-125">Prérequis</span><span class="sxs-lookup"><span data-stu-id="30762-125">Prerequisites</span></span>

* <span data-ttu-id="30762-126">Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="30762-126">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="30762-127">Base C# possibilité de programmation.</span><span class="sxs-lookup"><span data-stu-id="30762-127">Some basic C# programming ability.</span></span>
* <span data-ttu-id="30762-128">Vous devez avoir terminé [101 de principes de base MR](holograms-101.md).</span><span class="sxs-lookup"><span data-stu-id="30762-128">You should have completed [MR Basics 101](holograms-101.md).</span></span>
* <span data-ttu-id="30762-129">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="30762-129">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="30762-130">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="30762-130">Project files</span></span>

* <span data-ttu-id="30762-131">Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-230-SpatialMapping.zip) requise par le projet.</span><span class="sxs-lookup"><span data-stu-id="30762-131">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-230-SpatialMapping.zip) required by the project.</span></span><span data-ttu-id="30762-132"> Nécessite Unity 2017.2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="30762-132"> Requires Unity 2017.2 or later.</span></span>
  * <span data-ttu-id="30762-133">Si vous avez besoin de prise en charge de Unity 5.6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-230.zip).</span><span class="sxs-lookup"><span data-stu-id="30762-133">If you still need Unity 5.6 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-230.zip).</span></span>
  * <span data-ttu-id="30762-134">Si vous avez besoin de prise en charge de Unity 5.5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-230.zip).</span><span class="sxs-lookup"><span data-stu-id="30762-134">If you still need Unity 5.5 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-230.zip).</span></span>
  * <span data-ttu-id="30762-135">Si vous avez besoin de prise en charge de Unity 5.4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-230.zip).</span><span class="sxs-lookup"><span data-stu-id="30762-135">If you still need Unity 5.4 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-230.zip).</span></span>
* <span data-ttu-id="30762-136">Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="30762-136">Un-archive the files to your desktop or other easy to reach location.</span></span>

>[!NOTE]
><span data-ttu-id="30762-137">Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-230-SpatialMapping).</span><span class="sxs-lookup"><span data-stu-id="30762-137">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-230-SpatialMapping).</span></span>

### <a name="notes"></a><span data-ttu-id="30762-138">Notes</span><span class="sxs-lookup"><span data-stu-id="30762-138">Notes</span></span>

* <span data-ttu-id="30762-139">« Activer uniquement mon Code » dans Visual Studio doit être désactivée (*unchecked*) sous Outils > Options > débogage afin d’atteindre des points d’arrêt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="30762-139">"Enable Just My Code" in Visual Studio needs to be disabled (*unchecked*) under Tools > Options > Debugging in order to hit breakpoints in your code.</span></span>

## <a name="unity-setup"></a><span data-ttu-id="30762-140">Programme d’installation Unity</span><span class="sxs-lookup"><span data-stu-id="30762-140">Unity setup</span></span>

>[!VIDEO https://www.youtube.com/embed/y2Y4LhK6TEM]

* <span data-ttu-id="30762-141">Démarrer **Unity**.</span><span class="sxs-lookup"><span data-stu-id="30762-141">Start **Unity**.</span></span>
* <span data-ttu-id="30762-142">Sélectionnez **New** pour créer un nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="30762-142">Select **New** to create a new project.</span></span>
* <span data-ttu-id="30762-143">Nommez le projet **PLANÉTARIUM**.</span><span class="sxs-lookup"><span data-stu-id="30762-143">Name the project **Planetarium**.</span></span>
* <span data-ttu-id="30762-144">Vérifiez que le **3D** paramètre est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="30762-144">Verify that the **3D** setting is selected.</span></span>
* <span data-ttu-id="30762-145">Cliquez sur **créer le projet**.</span><span class="sxs-lookup"><span data-stu-id="30762-145">Click **Create Project**.</span></span>
* <span data-ttu-id="30762-146">Une fois Unity lance, accédez à **Modifier > Paramètres du projet > Lecteur**.</span><span class="sxs-lookup"><span data-stu-id="30762-146">Once Unity launches, go to **Edit > Project Settings > Player**.</span></span>
* <span data-ttu-id="30762-147">Dans le **inspecteur** panneau, recherchez et sélectionnez le vert **Windows Store** icône.</span><span class="sxs-lookup"><span data-stu-id="30762-147">In the **Inspector** panel, find and select the green **Windows Store** icon.</span></span>
* <span data-ttu-id="30762-148">Développez **autres paramètres**.</span><span class="sxs-lookup"><span data-stu-id="30762-148">Expand **Other Settings**.</span></span>
* <span data-ttu-id="30762-149">Dans le **rendu** section, vérifiez le **virtuel pris en charge de réalité** option.</span><span class="sxs-lookup"><span data-stu-id="30762-149">In the **Rendering** section, check the **Virtual Reality Supported** option.</span></span>
* <span data-ttu-id="30762-150">Vérifiez que **Windows HOLOGRAPHIQUE** apparaît dans la liste de **SDK de réalité virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="30762-150">Verify that **Windows Holographic** appears in the list of **Virtual Reality SDKs**.</span></span> <span data-ttu-id="30762-151">Dans le cas contraire, sélectionnez le **+** bouton en bas de la liste et choisissez **Windows HOLOGRAPHIQUE**.</span><span class="sxs-lookup"><span data-stu-id="30762-151">If not, select the **+** button at the bottom of the list and choose **Windows Holographic**.</span></span>
* <span data-ttu-id="30762-152">Développez **paramètres de publication**.</span><span class="sxs-lookup"><span data-stu-id="30762-152">Expand **Publishing Settings**.</span></span>
* <span data-ttu-id="30762-153">Dans le **fonctionnalités** section, vérifiez les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="30762-153">In the **Capabilities** section, check the following settings:</span></span>
    * <span data-ttu-id="30762-154">InternetClientServer</span><span class="sxs-lookup"><span data-stu-id="30762-154">InternetClientServer</span></span>
    * <span data-ttu-id="30762-155">PrivateNetworkClientServer</span><span class="sxs-lookup"><span data-stu-id="30762-155">PrivateNetworkClientServer</span></span>
    * <span data-ttu-id="30762-156">Microphone</span><span class="sxs-lookup"><span data-stu-id="30762-156">Microphone</span></span>
    * <span data-ttu-id="30762-157">SpatialPerception</span><span class="sxs-lookup"><span data-stu-id="30762-157">SpatialPerception</span></span>
* <span data-ttu-id="30762-158">Accédez à **Modifier > Paramètres du projet > qualité**</span><span class="sxs-lookup"><span data-stu-id="30762-158">Go to **Edit > Project Settings > Quality**</span></span>
* <span data-ttu-id="30762-159">Dans le **inspecteur** panneau, sous l’icône Windows Store, sélectionnez la flèche noire de la liste déroulante sous la ligne « Default » et modifiez le paramètre par défaut pour **très faible**.</span><span class="sxs-lookup"><span data-stu-id="30762-159">In the **Inspector** panel, under the Windows Store icon, select the black drop-down arrow under the 'Default' row and change the default setting to **Very Low**.</span></span>
* <span data-ttu-id="30762-160">Accédez à **actifs > Importer un Package > Package personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="30762-160">Go to **Assets > Import Package > Custom Package**.</span></span>
* <span data-ttu-id="30762-161">Accédez à la **...\HolographicAcademy-Holograms-230-SpatialMapping\Starting** dossier.</span><span class="sxs-lookup"><span data-stu-id="30762-161">Navigate to the **...\HolographicAcademy-Holograms-230-SpatialMapping\Starting** folder.</span></span>
* <span data-ttu-id="30762-162">Cliquez sur **Planetarium.unitypackage**.</span><span class="sxs-lookup"><span data-stu-id="30762-162">Click on **Planetarium.unitypackage**.</span></span>
* <span data-ttu-id="30762-163">Cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="30762-163">Click **Open**.</span></span>
* <span data-ttu-id="30762-164">Un **importer un Package Unity** fenêtre s’affiche, cliquez sur le **importation** bouton.</span><span class="sxs-lookup"><span data-stu-id="30762-164">An **Import Unity Package** window should appear, click on the **Import** button.</span></span>
* <span data-ttu-id="30762-165">Attendez que Unity importer toutes les ressources que nous devons mener à bien ce projet.</span><span class="sxs-lookup"><span data-stu-id="30762-165">Wait for Unity to import all of the assets that we will need to complete this project.</span></span>
* <span data-ttu-id="30762-166">Dans le **hiérarchie** panneau, supprimez le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="30762-166">In the **Hierarchy** panel, delete the **Main Camera**.</span></span>
* <span data-ttu-id="30762-167">Dans le **projet** Panneau de configuration, **HoloToolkit-SpatialMapping-230\Utilities\Prefabs** dossier, recherchez le **Main Camera** objet.</span><span class="sxs-lookup"><span data-stu-id="30762-167">In the **Project** panel, **HoloToolkit-SpatialMapping-230\Utilities\Prefabs** folder, find the **Main Camera** object.</span></span>
* <span data-ttu-id="30762-168">Faites glisser et déposez le **Main Camera** prefab dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="30762-168">Drag and drop the **Main Camera** prefab into the **Hierarchy** panel.</span></span>
* <span data-ttu-id="30762-169">Dans le **hiérarchie** panneau, supprimez le **lumière directionnelle** objet.</span><span class="sxs-lookup"><span data-stu-id="30762-169">In the **Hierarchy** panel, delete the **Directional Light** object.</span></span>
* <span data-ttu-id="30762-170">Dans le **projet** Panneau de configuration, **Vntana** dossier, recherchez le **curseur** objet.</span><span class="sxs-lookup"><span data-stu-id="30762-170">In the **Project** panel, **Holograms** folder, locate the **Cursor** object.</span></span>
* <span data-ttu-id="30762-171">Glisser -déplacer le **curseur** prefab dans le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="30762-171">Drag & drop the **Cursor** prefab into the **Hierarchy**.</span></span>
* <span data-ttu-id="30762-172">Dans le **hiérarchie** Panneau de configuration, sélectionnez le **curseur** objet.</span><span class="sxs-lookup"><span data-stu-id="30762-172">In the **Hierarchy** panel, select the **Cursor** object.</span></span>
* <span data-ttu-id="30762-173">Dans le **inspecteur** du panneau, cliquez sur le **couche** liste déroulante et sélectionnez **couches modifier...** .</span><span class="sxs-lookup"><span data-stu-id="30762-173">In the **Inspector** panel, click the **Layer** drop-down and select **Edit Layers...**.</span></span>
* <span data-ttu-id="30762-174">Nom **couche utilisateur 31** en tant que «**SpatialMapping**».</span><span class="sxs-lookup"><span data-stu-id="30762-174">Name **User Layer 31** as "**SpatialMapping**".</span></span>
* <span data-ttu-id="30762-175">Enregistrer la nouvelle scène : **Fichier > Enregistrer la scène sous...**</span><span class="sxs-lookup"><span data-stu-id="30762-175">Save the new scene: **File > Save Scene As...**</span></span>
* <span data-ttu-id="30762-176">Cliquez sur **nouveau dossier** et nommez le dossier **scènes**.</span><span class="sxs-lookup"><span data-stu-id="30762-176">Click **New Folder** and name the folder **Scenes**.</span></span>
* <span data-ttu-id="30762-177">Nommez le fichier «**PLANÉTARIUM**» et l’enregistrer dans le **scènes** dossier.</span><span class="sxs-lookup"><span data-stu-id="30762-177">Name the file "**Planetarium**" and save it in the **Scenes** folder.</span></span>

## <a name="chapter-1---scanning"></a><span data-ttu-id="30762-178">Chapitre 1 - analyse</span><span class="sxs-lookup"><span data-stu-id="30762-178">Chapter 1 - Scanning</span></span>

>[!VIDEO https://www.youtube.com/embed/888oW51z_cE]

<span data-ttu-id="30762-179">**Objectifs**</span><span class="sxs-lookup"><span data-stu-id="30762-179">**Objectives**</span></span>
* <span data-ttu-id="30762-180">Découvrez le SurfaceObserver et comment profiter de son impact sur les paramètres et les performances.</span><span class="sxs-lookup"><span data-stu-id="30762-180">Learn about the SurfaceObserver and how its settings impact experience and performance.</span></span>
* <span data-ttu-id="30762-181">Créer une salle d’expérience pour collecter les panneaux de votre espace d’analyse.</span><span class="sxs-lookup"><span data-stu-id="30762-181">Create a room scanning experience to collect the meshes of your room.</span></span>

<span data-ttu-id="30762-182">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="30762-182">**Instructions**</span></span>
* <span data-ttu-id="30762-183">Dans le **projet** panneau **HoloToolkit-SpatialMapping-230\SpatialMapping\Prefabs** dossier, recherchez le **SpatialMapping** prefab.</span><span class="sxs-lookup"><span data-stu-id="30762-183">In the **Project** panel **HoloToolkit-SpatialMapping-230\SpatialMapping\Prefabs** folder, find the **SpatialMapping** prefab.</span></span>
* <span data-ttu-id="30762-184">Glisser -déplacer le **SpatialMapping** prefab dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="30762-184">Drag & drop the **SpatialMapping** prefab into the **Hierarchy** panel.</span></span>

<span data-ttu-id="30762-185">**Générer et déployer (partie 1)**</span><span class="sxs-lookup"><span data-stu-id="30762-185">**Build and Deploy (part 1)**</span></span>
* <span data-ttu-id="30762-186">Dans Unity, sélectionnez **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="30762-186">In Unity, select **File > Build Settings**.</span></span>
* <span data-ttu-id="30762-187">Cliquez sur **ajouter un arrière-plan Open** pour ajouter le **PLANÉTARIUM** scène à la build.</span><span class="sxs-lookup"><span data-stu-id="30762-187">Click **Add Open Scenes** to add the **Planetarium** scene to the build.</span></span>
* <span data-ttu-id="30762-188">Sélectionnez **plateforme Windows universelle** dans le **plateforme** liste et cliquez sur **plateforme de commutation**.</span><span class="sxs-lookup"><span data-stu-id="30762-188">Select **Universal Windows Platform** in the **Platform** list and click **Switch Platform**.</span></span>
* <span data-ttu-id="30762-189">Définissez **SDK** à **universelle 10** et **Type de Build UWP** à **D3D**.</span><span class="sxs-lookup"><span data-stu-id="30762-189">Set **SDK** to **Universal 10** and **UWP Build Type** to **D3D**.</span></span>
* <span data-ttu-id="30762-190">Vérifiez **Unity C# projets**.</span><span class="sxs-lookup"><span data-stu-id="30762-190">Check **Unity C# Projects**.</span></span>
* <span data-ttu-id="30762-191">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="30762-191">Click **Build**.</span></span>
* <span data-ttu-id="30762-192">Créer un **nouveau dossier** nommé « Application ».</span><span class="sxs-lookup"><span data-stu-id="30762-192">Create a **New Folder** named "App".</span></span>
* <span data-ttu-id="30762-193">Clic le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="30762-193">Single click the **App** folder.</span></span>
* <span data-ttu-id="30762-194">Appuyez sur la **sélectionner le dossier** bouton.</span><span class="sxs-lookup"><span data-stu-id="30762-194">Press the **Select Folder** button.</span></span>
* <span data-ttu-id="30762-195">Quand Unity est terminé, création d’une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="30762-195">When Unity is done building, a File Explorer window will appear.</span></span>
* <span data-ttu-id="30762-196">Double-cliquez sur le **application** dossier pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="30762-196">Double-click on the **App** folder to open it.</span></span>
* <span data-ttu-id="30762-197">Double-cliquez sur **Planetarium.sln** pour charger le projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30762-197">Double-click on **Planetarium.sln** to load the project in Visual Studio.</span></span>
* <span data-ttu-id="30762-198">Dans Visual Studio, utilisez la barre d’outils supérieure pour modifier la Configuration à **version**.</span><span class="sxs-lookup"><span data-stu-id="30762-198">In Visual Studio, use the top toolbar to change the Configuration to **Release**.</span></span>
* <span data-ttu-id="30762-199">Modifier la plateforme à **x86**.</span><span class="sxs-lookup"><span data-stu-id="30762-199">Change the Platform to **x86**.</span></span>
* <span data-ttu-id="30762-200">Cliquez sur la flèche déroulante à droite de le « Ordinateur Local », puis sélectionnez **Machine distante**.</span><span class="sxs-lookup"><span data-stu-id="30762-200">Click on the drop-down arrow to the right of 'Local Machine', and select **Remote Machine**.</span></span>
* <span data-ttu-id="30762-201">Entrez [adresse IP de votre périphérique](connecting-to-wi-fi-on-hololens.md#identifying-the-ip-address-of-your-hololens-on-the-wi-fi-network) dans l’adresse du champ et modifier le Mode d’authentification à **universel (protocole non chiffré)**.</span><span class="sxs-lookup"><span data-stu-id="30762-201">Enter [your device's IP address](connecting-to-wi-fi-on-hololens.md#identifying-the-ip-address-of-your-hololens-on-the-wi-fi-network) in the Address field and change Authentication Mode to **Universal (Unencrypted Protocol)**.</span></span>
* <span data-ttu-id="30762-202">Cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="30762-202">Click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
* <span data-ttu-id="30762-203">Regardez la **sortie** panneau dans Visual Studio pour la génération et l’état du déploiement.</span><span class="sxs-lookup"><span data-stu-id="30762-203">Watch the **Output** panel in Visual Studio for build and deploy status.</span></span>
* <span data-ttu-id="30762-204">Une fois que votre application a été déployée, Guide autour de la pièce.</span><span class="sxs-lookup"><span data-stu-id="30762-204">Once your app has deployed, walk around the room.</span></span> <span data-ttu-id="30762-205">Vous verrez les surfaces environnantes couvertes par les mailles filaire noir et blanc.</span><span class="sxs-lookup"><span data-stu-id="30762-205">You will see the surrounding surfaces covered by black and white wireframe meshes.</span></span>
* <span data-ttu-id="30762-206">Analyser votre environnement.</span><span class="sxs-lookup"><span data-stu-id="30762-206">Scan your surroundings.</span></span> <span data-ttu-id="30762-207">Veillez à examiner les murs, plafonds et étages.</span><span class="sxs-lookup"><span data-stu-id="30762-207">Be sure to look at walls, ceilings, and floors.</span></span>

<span data-ttu-id="30762-208">**Générer et déployer (partie 2)**</span><span class="sxs-lookup"><span data-stu-id="30762-208">**Build and Deploy (part 2)**</span></span>

<span data-ttu-id="30762-209">Maintenant Examinons comment le mappage Spatial peut affecter les performances.</span><span class="sxs-lookup"><span data-stu-id="30762-209">Now let's explore how Spatial Mapping can affect performance.</span></span>
* <span data-ttu-id="30762-210">Dans Unity, sélectionnez **fenêtre > Profiler**.</span><span class="sxs-lookup"><span data-stu-id="30762-210">In Unity, select **Window > Profiler**.</span></span>
* <span data-ttu-id="30762-211">Cliquez sur **ajouter Profiler > GPU**.</span><span class="sxs-lookup"><span data-stu-id="30762-211">Click **Add Profiler > GPU**.</span></span>
* <span data-ttu-id="30762-212">Cliquez sur **Profiler Active > <Enter IP>** .</span><span class="sxs-lookup"><span data-stu-id="30762-212">Click **Active Profiler > <Enter IP>**.</span></span>
* <span data-ttu-id="30762-213">Entrez le **adresse IP** de votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="30762-213">Enter the **IP address** of your HoloLens.</span></span>
* <span data-ttu-id="30762-214">Cliquer sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="30762-214">Click **Connect**.</span></span>
* <span data-ttu-id="30762-215">Observez le nombre de millisecondes que nécessaire pour le GPU afficher un frame.</span><span class="sxs-lookup"><span data-stu-id="30762-215">Observe the number of milliseconds it takes for the GPU to render a frame.</span></span>
* <span data-ttu-id="30762-216">Arrêter l’application de s’exécuter sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="30762-216">Stop the application from running on the device.</span></span>
* <span data-ttu-id="30762-217">Revenez à Visual Studio et ouvrez **SpatialMappingObserver.cs**.</span><span class="sxs-lookup"><span data-stu-id="30762-217">Return to Visual Studio and open **SpatialMappingObserver.cs**.</span></span> <span data-ttu-id="30762-218">Vous le trouverez dans le dossier HoloToolkit\SpatialMapping du projet d’Assembly-CSharp (Universal Windows).</span><span class="sxs-lookup"><span data-stu-id="30762-218">You will find it in the HoloToolkit\SpatialMapping folder of the Assembly-CSharp (Universal Windows) project.</span></span>
* <span data-ttu-id="30762-219">Rechercher la **Awake()** de fonction, puis ajoutez la ligne de code suivante : **TrianglesPerCubicMeter = 1200 ;**</span><span class="sxs-lookup"><span data-stu-id="30762-219">Find the **Awake()** function, and add the following line of code: **TrianglesPerCubicMeter = 1200;**</span></span>
* <span data-ttu-id="30762-220">Redéployez le projet sur votre appareil, puis **reconnecter le profileur**.</span><span class="sxs-lookup"><span data-stu-id="30762-220">Re-deploy the project to your device, and then **reconnect the profiler**.</span></span> <span data-ttu-id="30762-221">Observez la modification du nombre de millisecondes pour afficher un frame.</span><span class="sxs-lookup"><span data-stu-id="30762-221">Observe the change in the number of milliseconds to render a frame.</span></span>
* <span data-ttu-id="30762-222">Arrêter l’application de s’exécuter sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="30762-222">Stop the application from running on the device.</span></span>

<span data-ttu-id="30762-223">**Enregistrer et charger dans Unity**</span><span class="sxs-lookup"><span data-stu-id="30762-223">**Save and load in Unity**</span></span>

<span data-ttu-id="30762-224">Enfin, nous allons enregistrer notre maillage salle et chargez-le dans Unity.</span><span class="sxs-lookup"><span data-stu-id="30762-224">Finally, let's save our room mesh and load it into Unity.</span></span>
* <span data-ttu-id="30762-225">Revenez à Visual Studio et supprimer le **TrianglesPerCubicMeter** ligne que vous avez ajouté dans le **Awake()** fonction lors de la section précédente.</span><span class="sxs-lookup"><span data-stu-id="30762-225">Return to Visual Studio and remove the **TrianglesPerCubicMeter** line that you added in the **Awake()** function during the previous section.</span></span>
* <span data-ttu-id="30762-226">Redéployez le projet sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="30762-226">Redeploy the project to your device.</span></span> <span data-ttu-id="30762-227">Nous devons maintenant être en cours d’exécution avec **500** triangles par mètre.</span><span class="sxs-lookup"><span data-stu-id="30762-227">We should now be running with **500** triangles per cubic meter.</span></span>
* <span data-ttu-id="30762-228">Ouvrez un navigateur et entrez dans votre HoloLens IPAddress pour accéder à la **Windows Device Portal**.</span><span class="sxs-lookup"><span data-stu-id="30762-228">Open a browser and enter in your HoloLens IPAddress to navigate to the **Windows Device Portal**.</span></span>
* <span data-ttu-id="30762-229">Sélectionnez le **affichage 3D** option dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="30762-229">Select the **3D View** option in the left panel.</span></span>
* <span data-ttu-id="30762-230">Sous **Surface reconstruction** sélectionner le **mise à jour** bouton.</span><span class="sxs-lookup"><span data-stu-id="30762-230">Under **Surface reconstruction** select the **Update** button.</span></span>
* <span data-ttu-id="30762-231">Observez que les zones que vous avez analysé sur votre HoloLens s’affichent dans la fenêtre d’affichage.</span><span class="sxs-lookup"><span data-stu-id="30762-231">Watch as the areas that you have scanned on your HoloLens appear in the display window.</span></span>
* <span data-ttu-id="30762-232">Pour enregistrer votre analyse de la salle, appuyez sur la **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="30762-232">To save your room scan, press the **Save** button.</span></span>
* <span data-ttu-id="30762-233">Ouvrez votre **télécharge** dossier pour découvrir le modèle enregistré salle **SRMesh.obj**.</span><span class="sxs-lookup"><span data-stu-id="30762-233">Open your **Downloads** folder to find the saved room model **SRMesh.obj**.</span></span>
* <span data-ttu-id="30762-234">Copie **SRMesh.obj** à la **actifs** dossier de votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="30762-234">Copy **SRMesh.obj** to the **Assets** folder of your Unity project.</span></span>
* <span data-ttu-id="30762-235">Dans Unity, sélectionnez le **SpatialMapping** de l’objet dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="30762-235">In Unity, select the **SpatialMapping** object in the **Hierarchy** panel.</span></span>
* <span data-ttu-id="30762-236">Recherchez le **objet Observateur de Surface (Script)** composant.</span><span class="sxs-lookup"><span data-stu-id="30762-236">Locate the **Object Surface Observer (Script)** component.</span></span>
* <span data-ttu-id="30762-237">Cliquez sur le cercle à droite de la **salle modèle** propriété.</span><span class="sxs-lookup"><span data-stu-id="30762-237">Click the circle to the right of the **Room Model** property.</span></span>
* <span data-ttu-id="30762-238">Recherchez et sélectionnez le **SRMesh** de l’objet, puis fermez la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="30762-238">Find and select the **SRMesh** object and then close the window.</span></span>
* <span data-ttu-id="30762-239">Vérifiez que le **salle modèle** propriété dans le **inspecteur** Panneau de configuration est maintenant définie sur **SRMesh**.</span><span class="sxs-lookup"><span data-stu-id="30762-239">Verify that the **Room Model** property in the **Inspector** panel is now set to **SRMesh**.</span></span>
* <span data-ttu-id="30762-240">Appuyez sur la **lire** bouton pour passer en mode de prévisualisation d’Unity.</span><span class="sxs-lookup"><span data-stu-id="30762-240">Press the **Play** button to enter Unity's preview mode.</span></span>
* <span data-ttu-id="30762-241">Le composant SpatialMapping chargera les panneaux à partir du modèle de salle enregistré, vous pouvez les utiliser dans Unity.</span><span class="sxs-lookup"><span data-stu-id="30762-241">The SpatialMapping component will load the meshes from the saved room model so you can use them in Unity.</span></span>
* <span data-ttu-id="30762-242">Basculez vers **scène** vue pour voir tous les de votre modèle de salle affiché avec le nuanceur filaire.</span><span class="sxs-lookup"><span data-stu-id="30762-242">Switch to **Scene** view to see all of your room model displayed with the wireframe shader.</span></span>
* <span data-ttu-id="30762-243">Appuyez sur la **lire** bouton pour quitter le mode Aperçu.</span><span class="sxs-lookup"><span data-stu-id="30762-243">Press the **Play** button again to exit preview mode.</span></span>

<span data-ttu-id="30762-244">**REMARQUE :** La prochaine fois que vous entrez le mode Aperçu dans Unity, il charge le maillage salle enregistré par défaut.</span><span class="sxs-lookup"><span data-stu-id="30762-244">**NOTE:** The next time that you enter preview mode in Unity, it will load the saved room mesh by default.</span></span>

## <a name="chapter-2---visualization"></a><span data-ttu-id="30762-245">Chapitre 2 - visualisation</span><span class="sxs-lookup"><span data-stu-id="30762-245">Chapter 2 - Visualization</span></span>

>[!VIDEO https://www.youtube.com/embed/RnkvXl-aXD4]

<span data-ttu-id="30762-246">**Objectifs**</span><span class="sxs-lookup"><span data-stu-id="30762-246">**Objectives**</span></span>
* <span data-ttu-id="30762-247">Découvrez les principes fondamentaux de nuanceurs.</span><span class="sxs-lookup"><span data-stu-id="30762-247">Learn the basics of shaders.</span></span>
* <span data-ttu-id="30762-248">Visualiser votre environnement.</span><span class="sxs-lookup"><span data-stu-id="30762-248">Visualize your surroundings.</span></span>

<span data-ttu-id="30762-249">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="30762-249">**Instructions**</span></span>
* <span data-ttu-id="30762-250">Dans Unity **hiérarchie** Panneau de configuration, sélectionnez le **SpatialMapping** objet.</span><span class="sxs-lookup"><span data-stu-id="30762-250">In Unity's **Hierarchy** panel, select the **SpatialMapping** object.</span></span>
* <span data-ttu-id="30762-251">Dans le **inspecteur** panneau, recherchez le **Manager mappage Spatial (Script)** composant.</span><span class="sxs-lookup"><span data-stu-id="30762-251">In the **Inspector** panel, find the **Spatial Mapping Manager (Script)** component.</span></span>
* <span data-ttu-id="30762-252">Cliquez sur le cercle à droite de la **matériau de Surface** propriété.</span><span class="sxs-lookup"><span data-stu-id="30762-252">Click the circle to the right of the **Surface Material** property.</span></span>
* <span data-ttu-id="30762-253">Recherchez et sélectionnez le **BlueLinesOnWalls** matériau et fermer la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="30762-253">Find and select the **BlueLinesOnWalls** material and close the window.</span></span>
* <span data-ttu-id="30762-254">Dans le **projet** panneau **nuanceurs** dossier, double-cliquez sur **BlueLinesOnWalls** pour ouvrir le nuanceur dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30762-254">In the **Project** panel **Shaders** folder, double-click on **BlueLinesOnWalls** to open the shader in Visual Studio.</span></span>
* <span data-ttu-id="30762-255">Il s’agit d’un pixel simple (vertex pour fragmenter) nuanceur, ce qui permet d’effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="30762-255">This is a simple pixel (vertex to fragment) shader, which accomplishes the following tasks:</span></span>
    1. <span data-ttu-id="30762-256">Convertit l’emplacement d’un sommet à l’espace universel.</span><span class="sxs-lookup"><span data-stu-id="30762-256">Converts a vertex's location to world space.</span></span>
    2. <span data-ttu-id="30762-257">Vérifie que le vertex's normal pour déterminer si un pixel est vertical.</span><span class="sxs-lookup"><span data-stu-id="30762-257">Checks the vertex's normal to determine if a pixel is vertical.</span></span>
    3. <span data-ttu-id="30762-258">Définit la couleur du pixel pour le rendu.</span><span class="sxs-lookup"><span data-stu-id="30762-258">Sets the color of the pixel for rendering.</span></span>

<span data-ttu-id="30762-259">**Générer et déployer**</span><span class="sxs-lookup"><span data-stu-id="30762-259">**Build and Deploy**</span></span>
* <span data-ttu-id="30762-260">Revenir à Unity, puis appuyez sur **lire** pour passer en mode Aperçu.</span><span class="sxs-lookup"><span data-stu-id="30762-260">Return to Unity and press **Play** to enter preview mode.</span></span>
* <span data-ttu-id="30762-261">Les lignes bleues seront affichera sur toutes les surfaces verticales de la maille de salle (qui chargés automatiquement à partir de nos données analyse enregistrées).</span><span class="sxs-lookup"><span data-stu-id="30762-261">Blue lines will be rendered on all vertical surfaces of the room mesh (which automatically loaded from our saved scanning data).</span></span>
* <span data-ttu-id="30762-262">Basculez vers le **scène** tab pour ajuster votre affichage de la salle et voir comment la maille local s’affiche dans Unity.</span><span class="sxs-lookup"><span data-stu-id="30762-262">Switch to the **Scene** tab to adjust your view of the room and see how the entire room mesh appears in Unity.</span></span>
* <span data-ttu-id="30762-263">Dans le **projet** panneau, recherchez le **matériaux** dossier et sélectionnez le **BlueLinesOnWalls** matériau.</span><span class="sxs-lookup"><span data-stu-id="30762-263">In the **Project** panel, find the **Materials** folder and select the **BlueLinesOnWalls** material.</span></span>
* <span data-ttu-id="30762-264">Modifier certaines propriétés et voir comment les modifications apparaissent dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="30762-264">Modify some properties and see how the changes appear in the Unity editor.</span></span>
    * <span data-ttu-id="30762-265">Dans le **inspecteur** panneau, ajustez le **LineScale** valeur pour que les lignes apparaissent épaisse ou plus étroit.</span><span class="sxs-lookup"><span data-stu-id="30762-265">In the **Inspector** panel, adjust the **LineScale** value to make the lines appear thicker or thinner.</span></span>
    * <span data-ttu-id="30762-266">Dans le **inspecteur** panneau, ajustez le **LinesPerMeter** valeur pour modifier le nombre de lignes s’affichent sur chaque mur.</span><span class="sxs-lookup"><span data-stu-id="30762-266">In the **Inspector** panel, adjust the **LinesPerMeter** value to change how many lines appear on each wall.</span></span>
* <span data-ttu-id="30762-267">Cliquez sur **lire** pour quitter le mode Aperçu.</span><span class="sxs-lookup"><span data-stu-id="30762-267">Click **Play** again to exit preview mode.</span></span>
* <span data-ttu-id="30762-268">Créer et déployer à l’HoloLens et observer la façon dont le nuanceur de rendu apparaît sur les surfaces réels.</span><span class="sxs-lookup"><span data-stu-id="30762-268">Build and deploy to the HoloLens and observe how the shader rendering appears on real surfaces.</span></span>

<span data-ttu-id="30762-269">Unity fait un travail remarquable afficher un aperçu des documents, mais il est toujours une bonne idée au rendu de l’extraction dans l’appareil.</span><span class="sxs-lookup"><span data-stu-id="30762-269">Unity does a great job of previewing materials, but it's always a good idea to check-out rendering in the device.</span></span>

## <a name="chapter-3---processing"></a><span data-ttu-id="30762-270">Chapitre 3 - traitement</span><span class="sxs-lookup"><span data-stu-id="30762-270">Chapter 3 - Processing</span></span>

>[!VIDEO https://www.youtube.com/embed/kaUKiNiDxwY]

<span data-ttu-id="30762-271">**Objectifs**</span><span class="sxs-lookup"><span data-stu-id="30762-271">**Objectives**</span></span>
* <span data-ttu-id="30762-272">Découvrez des techniques pour traiter les données de mappage spatial pour une utilisation dans votre application.</span><span class="sxs-lookup"><span data-stu-id="30762-272">Learn techniques to process spatial mapping data for use in your application.</span></span>
* <span data-ttu-id="30762-273">Analyser les données de mappage spatial pour rechercher des plans et supprimer des triangles.</span><span class="sxs-lookup"><span data-stu-id="30762-273">Analyze spatial mapping data to find planes and remove triangles.</span></span>
* <span data-ttu-id="30762-274">Utiliser des plans pour la sélection élective hologramme.</span><span class="sxs-lookup"><span data-stu-id="30762-274">Use planes for hologram placement.</span></span>

<span data-ttu-id="30762-275">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="30762-275">**Instructions**</span></span>
* <span data-ttu-id="30762-276">Dans Unity **projet** Panneau de configuration, **hologrammes** dossier, recherchez le **SpatialProcessing** objet.</span><span class="sxs-lookup"><span data-stu-id="30762-276">In Unity's **Project** panel, **Holograms** folder, find the **SpatialProcessing** object.</span></span>
* <span data-ttu-id="30762-277">Glisser -déplacer le **SpatialProcessing** de l’objet dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="30762-277">Drag & drop the **SpatialProcessing** object into the **Hierarchy** panel.</span></span>

<span data-ttu-id="30762-278">Le préfabriqué SpatialProcessing inclut des composants pour traiter les données de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="30762-278">The SpatialProcessing prefab includes components for processing the spatial mapping data.</span></span> <span data-ttu-id="30762-279">**SurfaceMeshesToPlanes.cs** recherche et générer des plans en fonction des données de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="30762-279">**SurfaceMeshesToPlanes.cs** will find and generate planes based on the spatial mapping data.</span></span> <span data-ttu-id="30762-280">Nous allons utiliser des plans dans notre application pour représenter les sols, murs et les plafonds.</span><span class="sxs-lookup"><span data-stu-id="30762-280">We will use planes in our application to represent walls, floors and ceilings.</span></span> <span data-ttu-id="30762-281">Cette préfabriqué inclut également **RemoveSurfaceVertices.cs** qui peut supprimer des sommets de la maille de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="30762-281">This prefab also includes **RemoveSurfaceVertices.cs** which can remove vertices from the spatial mapping mesh.</span></span> <span data-ttu-id="30762-282">Cela peut être utilisé pour créer des trous dans la maille, ou pour supprimer les triangles excessives qui ne sont plus nécessaires (car les plans peuvent être utilisés à la place).</span><span class="sxs-lookup"><span data-stu-id="30762-282">This can be used to create holes in the mesh, or to remove excess triangles that are no longer needed (because planes can be used instead).</span></span>
* <span data-ttu-id="30762-283">Dans Unity **projet** Panneau de configuration, **hologrammes** dossier, recherchez le **SpaceCollection** objet.</span><span class="sxs-lookup"><span data-stu-id="30762-283">In Unity's **Project** panel, **Holograms** folder, find the **SpaceCollection** object.</span></span>
* <span data-ttu-id="30762-284">Faites glisser et déposez le **SpaceCollection** de l’objet dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="30762-284">Drag and drop the **SpaceCollection** object into the **Hierarchy** panel.</span></span>
* <span data-ttu-id="30762-285">Dans le **hiérarchie** Panneau de configuration, sélectionnez le **SpatialProcessing** objet.</span><span class="sxs-lookup"><span data-stu-id="30762-285">In the **Hierarchy** panel, select the **SpatialProcessing** object.</span></span>
* <span data-ttu-id="30762-286">Dans le **inspecteur** panneau, recherchez le **lire Gestionnaire d’espace (Script)** composant.</span><span class="sxs-lookup"><span data-stu-id="30762-286">In the **Inspector** panel, find the **Play Space Manager (Script)** component.</span></span>
* <span data-ttu-id="30762-287">Double-cliquez sur **PlaySpaceManager.cs** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30762-287">Double-click on **PlaySpaceManager.cs** to open it in Visual Studio.</span></span>

<span data-ttu-id="30762-288">PlaySpaceManager.cs contient le code spécifique à l’application.</span><span class="sxs-lookup"><span data-stu-id="30762-288">PlaySpaceManager.cs contains application-specific code.</span></span> <span data-ttu-id="30762-289">Nous allons ajouter des fonctionnalités à ce script pour activer le comportement suivant :</span><span class="sxs-lookup"><span data-stu-id="30762-289">We will add functionality to this script to enable the following behavior:</span></span>
1. <span data-ttu-id="30762-290">Arrêter la collecte des données de mappage spatial après que nous dépassent la limite de temps analyse (10 secondes).</span><span class="sxs-lookup"><span data-stu-id="30762-290">Stop collecting spatial mapping data after we exceed the scanning time limit (10 seconds).</span></span>
2. <span data-ttu-id="30762-291">Traiter les données de mappage spatial :</span><span class="sxs-lookup"><span data-stu-id="30762-291">Process the spatial mapping data:</span></span>
    1. <span data-ttu-id="30762-292">Utilisez SurfaceMeshesToPlanes pour créer une représentation plus simple du monde en tant que plans (murs, étages, plafonds, etc.).</span><span class="sxs-lookup"><span data-stu-id="30762-292">Use SurfaceMeshesToPlanes to create a simpler representation of the world as planes (walls, floors, ceilings, etc).</span></span>
    2. <span data-ttu-id="30762-293">Utilisez RemoveSurfaceVertices pour supprimer les triangles aire de conception qui se situent dans les limites de plan.</span><span class="sxs-lookup"><span data-stu-id="30762-293">Use RemoveSurfaceVertices to remove surface triangles that fall within plane boundaries.</span></span>
3. <span data-ttu-id="30762-294">Générer une collection de hologrammes dans le monde et les placer sur des plans de mur et étage près de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="30762-294">Generate a collection of holograms in the world and place them on wall and floor planes near the user.</span></span>

<span data-ttu-id="30762-295">Effectuer les exercices de codage marqués dans PlaySpaceManager.cs ou remplacez le script avec la solution terminée ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="30762-295">Complete the coding exercises marked in PlaySpaceManager.cs, or replace the script with the finished solution from below:</span></span>

```cs
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Windows.Speech;
using Academy.HoloToolkit.Unity;

/// <summary>
/// The SurfaceManager class allows applications to scan the environment for a specified amount of time 
/// and then process the Spatial Mapping Mesh (find planes, remove vertices) after that time has expired.
/// </summary>
public class PlaySpaceManager : Singleton<PlaySpaceManager>
{
    [Tooltip("When checked, the SurfaceObserver will stop running after a specified amount of time.")]
    public bool limitScanningByTime = true;

    [Tooltip("How much time (in seconds) that the SurfaceObserver will run after being started; used when 'Limit Scanning By Time' is checked.")]
    public float scanTime = 30.0f;

    [Tooltip("Material to use when rendering Spatial Mapping meshes while the observer is running.")]
    public Material defaultMaterial;

    [Tooltip("Optional Material to use when rendering Spatial Mapping meshes after the observer has been stopped.")]
    public Material secondaryMaterial;

    [Tooltip("Minimum number of floor planes required in order to exit scanning/processing mode.")]
    public uint minimumFloors = 1;

    [Tooltip("Minimum number of wall planes required in order to exit scanning/processing mode.")]
    public uint minimumWalls = 1;

    /// <summary>
    /// Indicates if processing of the surface meshes is complete.
    /// </summary>
    private bool meshesProcessed = false;

    /// <summary>
    /// GameObject initialization.
    /// </summary>
    private void Start()
    {
        // Update surfaceObserver and storedMeshes to use the same material during scanning.
        SpatialMappingManager.Instance.SetSurfaceMaterial(defaultMaterial);

        // Register for the MakePlanesComplete event.
        SurfaceMeshesToPlanes.Instance.MakePlanesComplete += SurfaceMeshesToPlanes_MakePlanesComplete;
    }

    /// <summary>
    /// Called once per frame.
    /// </summary>
    private void Update()
    {
        // Check to see if the spatial mapping data has been processed
        // and if we are limiting how much time the user can spend scanning.
        if (!meshesProcessed && limitScanningByTime)
        {
            // If we have not processed the spatial mapping data
            // and scanning time is limited...

            // Check to see if enough scanning time has passed
            // since starting the observer.
            if (limitScanningByTime && ((Time.time - SpatialMappingManager.Instance.StartTime) < scanTime))
            {
                // If we have a limited scanning time, then we should wait until
                // enough time has passed before processing the mesh.
            }
            else
            {
                // The user should be done scanning their environment,
                // so start processing the spatial mapping data...

                /* TODO: 3.a DEVELOPER CODING EXERCISE 3.a */

                // 3.a: Check if IsObserverRunning() is true on the
                // SpatialMappingManager.Instance.
                if(SpatialMappingManager.Instance.IsObserverRunning())
                {
                    // 3.a: If running, Stop the observer by calling
                    // StopObserver() on the SpatialMappingManager.Instance.
                    SpatialMappingManager.Instance.StopObserver();
                }

                // 3.a: Call CreatePlanes() to generate planes.
                CreatePlanes();

                // 3.a: Set meshesProcessed to true.
                meshesProcessed = true;
            }
        }
    }

    /// <summary>
    /// Handler for the SurfaceMeshesToPlanes MakePlanesComplete event.
    /// </summary>
    /// <param name="source">Source of the event.</param>
    /// <param name="args">Args for the event.</param>
    private void SurfaceMeshesToPlanes_MakePlanesComplete(object source, System.EventArgs args)
    {
        /* TODO: 3.a DEVELOPER CODING EXERCISE 3.a */

        // Collection of floor and table planes that we can use to set horizontal items on.
        List<GameObject> horizontal = new List<GameObject>();

        // Collection of wall planes that we can use to set vertical items on.
        List<GameObject> vertical = new List<GameObject>();

        // 3.a: Get all floor and table planes by calling
        // SurfaceMeshesToPlanes.Instance.GetActivePlanes().
        // Assign the result to the 'horizontal' list.
        horizontal = SurfaceMeshesToPlanes.Instance.GetActivePlanes(PlaneTypes.Table | PlaneTypes.Floor);

        // 3.a: Get all wall planes by calling
        // SurfaceMeshesToPlanes.Instance.GetActivePlanes().
        // Assign the result to the 'vertical' list.
        vertical = SurfaceMeshesToPlanes.Instance.GetActivePlanes(PlaneTypes.Wall);

        // Check to see if we have enough horizontal planes (minimumFloors)
        // and vertical planes (minimumWalls), to set holograms on in the world.
        if (horizontal.Count >= minimumFloors && vertical.Count >= minimumWalls)
        {
            // We have enough floors and walls to place our holograms on...

            // 3.a: Let's reduce our triangle count by removing triangles
            // from SpatialMapping meshes that intersect with our active planes.
            // Call RemoveVertices().
            // Pass in all activePlanes found by SurfaceMeshesToPlanes.Instance.
            RemoveVertices(SurfaceMeshesToPlanes.Instance.ActivePlanes);

            // 3.a: We can indicate to the user that scanning is over by
            // changing the material applied to the Spatial Mapping meshes.
            // Call SpatialMappingManager.Instance.SetSurfaceMaterial().
            // Pass in the secondaryMaterial.
            SpatialMappingManager.Instance.SetSurfaceMaterial(secondaryMaterial);

            // 3.a: We are all done processing the mesh, so we can now
            // initialize a collection of Placeable holograms in the world
            // and use horizontal/vertical planes to set their starting positions.
            // Call SpaceCollectionManager.Instance.GenerateItemsInWorld().
            // Pass in the lists of horizontal and vertical planes that we found earlier.
            SpaceCollectionManager.Instance.GenerateItemsInWorld(horizontal, vertical);
        }
        else
        {
            // We do not have enough floors/walls to place our holograms on...

            // 3.a: Re-enter scanning mode so the user can find more surfaces by 
            // calling StartObserver() on the SpatialMappingManager.Instance.
            SpatialMappingManager.Instance.StartObserver();

            // 3.a: Re-process spatial data after scanning completes by
            // re-setting meshesProcessed to false.
            meshesProcessed = false;
        }
    }

    /// <summary>
    /// Creates planes from the spatial mapping surfaces.
    /// </summary>
    private void CreatePlanes()
    {
        // Generate planes based on the spatial map.
        SurfaceMeshesToPlanes surfaceToPlanes = SurfaceMeshesToPlanes.Instance;
        if (surfaceToPlanes != null && surfaceToPlanes.enabled)
        {
            surfaceToPlanes.MakePlanes();
        }
    }

    /// <summary>
    /// Removes triangles from the spatial mapping surfaces.
    /// </summary>
    /// <param name="boundingObjects"></param>
    private void RemoveVertices(IEnumerable<GameObject> boundingObjects)
    {
        RemoveSurfaceVertices removeVerts = RemoveSurfaceVertices.Instance;
        if (removeVerts != null && removeVerts.enabled)
        {
            removeVerts.RemoveSurfaceVerticesWithinBounds(boundingObjects);
        }
    }

    /// <summary>
    /// Called when the GameObject is unloaded.
    /// </summary>
    private void OnDestroy()
    {
        if (SurfaceMeshesToPlanes.Instance != null)
        {
            SurfaceMeshesToPlanes.Instance.MakePlanesComplete -= SurfaceMeshesToPlanes_MakePlanesComplete;
        }
    }
}
```

<span data-ttu-id="30762-296">**Générer et déployer**</span><span class="sxs-lookup"><span data-stu-id="30762-296">**Build and Deploy**</span></span>
* <span data-ttu-id="30762-297">Avant de déployer à l’HoloLens, appuyez sur la **lire** bouton dans Unity pour passer en mode lecture.</span><span class="sxs-lookup"><span data-stu-id="30762-297">Before deploying to the HoloLens, press the **Play** button in Unity to enter play mode.</span></span>
* <span data-ttu-id="30762-298">Une fois le maillage de l’espace est chargé à partir du fichier, attendez 10 secondes avant le démarrage de traitement sur le maillage de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="30762-298">After the room mesh is loaded from file, wait for 10 seconds before processing starts on the spatial mapping mesh.</span></span>
* <span data-ttu-id="30762-299">Lorsque le traitement est terminé, les plans seront affiche pour représenter le sol murs, ceiling, etc.</span><span class="sxs-lookup"><span data-stu-id="30762-299">When processing is complete, planes will appear to represent the floor, walls, ceiling, etc.</span></span>
* <span data-ttu-id="30762-300">Après tout des plans ont été trouvés, un système solaire doit s’afficher sur une table d’étage près de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="30762-300">After all of the planes have been found, you should see a solar system appear on a table of floor near the camera.</span></span>
* <span data-ttu-id="30762-301">Deux posters doivent apparaître trop des murs près de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="30762-301">Two posters should appear on walls near the camera too.</span></span> <span data-ttu-id="30762-302">Basculez vers le **scène** si vous ne pouvez pas les voir dans l’onglet **jeu** mode.</span><span class="sxs-lookup"><span data-stu-id="30762-302">Switch to the **Scene** tab if you cannot see them in **Game** mode.</span></span>
* <span data-ttu-id="30762-303">Appuyez sur la **lire** bouton pour quitter le mode de lecture.</span><span class="sxs-lookup"><span data-stu-id="30762-303">Press the **Play** button again to exit play mode.</span></span>
* <span data-ttu-id="30762-304">Générez et déployez à l’HoloLens, comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="30762-304">Build and deploy to the HoloLens, as usual.</span></span>
* <span data-ttu-id="30762-305">Attendez la numérisation et le traitement des données de mappage spatial pour terminer.</span><span class="sxs-lookup"><span data-stu-id="30762-305">Wait for scanning and processing of the spatial mapping data to complete.</span></span>
* <span data-ttu-id="30762-306">Une fois que vous voyez des plans, essayez de trouver le système solaire et affiches dans votre monde.</span><span class="sxs-lookup"><span data-stu-id="30762-306">Once you see planes, try to find the solar system and posters in your world.</span></span>

## <a name="chapter-4---placement"></a><span data-ttu-id="30762-307">Chapitre 4 - sélection élective</span><span class="sxs-lookup"><span data-stu-id="30762-307">Chapter 4 - Placement</span></span>

>[!VIDEO https://www.youtube.com/embed/Srhtpid1uZc]

<span data-ttu-id="30762-308">**Objectifs**</span><span class="sxs-lookup"><span data-stu-id="30762-308">**Objectives**</span></span>
* <span data-ttu-id="30762-309">Déterminer si un hologramme s’ajusteront sur une surface.</span><span class="sxs-lookup"><span data-stu-id="30762-309">Determine if a hologram will fit on a surface.</span></span>
* <span data-ttu-id="30762-310">Fournir des commentaires à l’utilisateur lorsqu’un hologramme peut/ne tiennent pas sur une surface.</span><span class="sxs-lookup"><span data-stu-id="30762-310">Provide feedback to the user when a hologram can/cannot fit on a surface.</span></span>

<span data-ttu-id="30762-311">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="30762-311">**Instructions**</span></span>
* <span data-ttu-id="30762-312">Dans Unity **hiérarchie** Panneau de configuration, sélectionnez le **SpatialProcessing** objet.</span><span class="sxs-lookup"><span data-stu-id="30762-312">In Unity's **Hierarchy** panel, select the **SpatialProcessing** object.</span></span>
* <span data-ttu-id="30762-313">Dans le **inspecteur** panneau, recherchez le **maillages de plans Surface (Script)** composant.</span><span class="sxs-lookup"><span data-stu-id="30762-313">In the **Inspector** panel, find the **Surface Meshes To Planes (Script)** component.</span></span>
* <span data-ttu-id="30762-314">Modifier le **dessiner les plans** propriété **rien** pour effacer la sélection.</span><span class="sxs-lookup"><span data-stu-id="30762-314">Change the **Draw Planes** property to **Nothing** to clear the selection.</span></span>
* <span data-ttu-id="30762-315">Modifier le **dessiner les plans** propriété **mur**, ce qui seront affichera uniquement les plans de mur.</span><span class="sxs-lookup"><span data-stu-id="30762-315">Change the **Draw Planes** property to **Wall**, so that only wall planes will be rendered.</span></span>
* <span data-ttu-id="30762-316">Dans le **projet** Panneau de configuration, **Scripts** dossier, double-cliquez sur **Placeable.cs** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30762-316">In the **Project** panel, **Scripts** folder, double-click on **Placeable.cs** to open it in Visual Studio.</span></span>

<span data-ttu-id="30762-317">Le **Placeable** script est déjà attaché à l’affiches projection boîte et qui sont créés après la recherche de plan.</span><span class="sxs-lookup"><span data-stu-id="30762-317">The **Placeable** script is already attached to the posters and projection box that are created after plane finding completes.</span></span> <span data-ttu-id="30762-318">Il nous suffit est ne pas commenter du code, et ce script permettent d’obtenir les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="30762-318">All we need to do is uncomment some code, and this script will achieve the following:</span></span>
1. <span data-ttu-id="30762-319">Déterminer si un hologramme s’ajusteront sur une surface par raycasting à partir du centre et les quatre coins du cube englobant.</span><span class="sxs-lookup"><span data-stu-id="30762-319">Determine if a hologram will fit on a surface by raycasting from the center and four corners of the bounding cube.</span></span>
2. <span data-ttu-id="30762-320">Vérification de la surface normale pour déterminer si elle est suffisamment bon pour l’hologramme asseoir vidage.</span><span class="sxs-lookup"><span data-stu-id="30762-320">Check the surface normal to determine if it is smooth enough for the hologram to sit flush on.</span></span>
3. <span data-ttu-id="30762-321">Afficher un cube englobant autour de l’hologramme pour afficher sa taille réelle moment d’être placé.</span><span class="sxs-lookup"><span data-stu-id="30762-321">Render a bounding cube around the hologram to show its actual size while being placed.</span></span>
4. <span data-ttu-id="30762-322">Convertir une ombre sous/derrière le hologramme pour montrer où il sera placé sur le sol/mur.</span><span class="sxs-lookup"><span data-stu-id="30762-322">Cast a shadow under/behind the hologram to show where it will be placed on the floor/wall.</span></span>
5. <span data-ttu-id="30762-323">Afficher l’ombre en rouge et si l’hologramme ne peut pas être placé sur la surface, ou vert, si possible.</span><span class="sxs-lookup"><span data-stu-id="30762-323">Render the shadow as red, if the hologram cannot be placed on the surface, or green, if it can.</span></span>
6. <span data-ttu-id="30762-324">Réorienter l’hologramme pour s’aligner avec le type de surface (vertical ou horizontal) qu’il possède une affinité avec.</span><span class="sxs-lookup"><span data-stu-id="30762-324">Re-orient the hologram to align with the surface type (vertical or horizontal) that it has affinity to.</span></span>
7. <span data-ttu-id="30762-325">Placer correctement l’hologramme sur la surface sélectionnée afin d’éviter le moment du saut ou le comportement d’alignement.</span><span class="sxs-lookup"><span data-stu-id="30762-325">Smoothly place the hologram on the selected surface to avoid jumping or snapping behavior.</span></span>

<span data-ttu-id="30762-326">Supprimez les commentaires de tout le code dans l’exercice de codage ci-dessous, ou utiliser cette solution terminée dans **Placeable.cs**:</span><span class="sxs-lookup"><span data-stu-id="30762-326">Uncomment all code in the coding exercise below, or use this completed solution in **Placeable.cs**:</span></span>

```cs
using System.Collections.Generic;
using UnityEngine;
using Academy.HoloToolkit.Unity;

/// <summary>
/// Enumeration containing the surfaces on which a GameObject
/// can be placed.  For simplicity of this sample, only one
/// surface type is allowed to be selected.
/// </summary>
public enum PlacementSurfaces
{
    // Horizontal surface with an upward pointing normal.    
    Horizontal = 1,

    // Vertical surface with a normal facing the user.
    Vertical = 2,
}

/// <summary>
/// The Placeable class implements the logic used to determine if a GameObject
/// can be placed on a target surface. Constraints for placement include:
/// * No part of the GameObject's box collider impacts with another object in the scene
/// * The object lays flat (within specified tolerances) against the surface
/// * The object would not fall off of the surface if gravity were enabled.
/// This class also provides the following visualizations.
/// * A transparent cube representing the object's box collider.
/// * Shadow on the target surface indicating whether or not placement is valid.
/// </summary>
public class Placeable : MonoBehaviour
{
    [Tooltip("The base material used to render the bounds asset when placement is allowed.")]
    public Material PlaceableBoundsMaterial = null;

    [Tooltip("The base material used to render the bounds asset when placement is not allowed.")]
    public Material NotPlaceableBoundsMaterial = null;

    [Tooltip("The material used to render the placement shadow when placement it allowed.")]
    public Material PlaceableShadowMaterial = null;

    [Tooltip("The material used to render the placement shadow when placement it not allowed.")]
    public Material NotPlaceableShadowMaterial = null;

    [Tooltip("The type of surface on which the object can be placed.")]
    public PlacementSurfaces PlacementSurface = PlacementSurfaces.Horizontal;

    [Tooltip("The child object(s) to hide during placement.")]
    public List<GameObject> ChildrenToHide = new List<GameObject>();

    /// <summary>
    /// Indicates if the object is in the process of being placed.
    /// </summary>
    public bool IsPlacing { get; private set; }

    // The most recent distance to the surface.  This is used to 
    // locate the object when the user's gaze does not intersect
    // with the Spatial Mapping mesh.
    private float lastDistance = 2.0f;

    // The distance away from the target surface that the object should hover prior while being placed.
    private float hoverDistance = 0.15f;

    // Threshold (the closer to 0, the stricter the standard) used to determine if a surface is flat.
    private float distanceThreshold = 0.02f;

    // Threshold (the closer to 1, the stricter the standard) used to determine if a surface is vertical.
    private float upNormalThreshold = 0.9f;

    // Maximum distance, from the object, that placement is allowed.
    // This is used when raycasting to see if the object is near a placeable surface.
    private float maximumPlacementDistance = 5.0f;

    // Speed (1.0 being fastest) at which the object settles to the surface upon placement.
    private float placementVelocity = 0.06f;

    // Indicates whether or not this script manages the object's box collider.
    private bool managingBoxCollider = false;

    // The box collider used to determine of the object will fit in the desired location.
    // It is also used to size the bounding cube.
    private BoxCollider boxCollider = null;

    // Visible asset used to show the dimensions of the object. This asset is sized
    // using the box collider's bounds.
    private GameObject boundsAsset = null;

    // Visible asset used to show the where the object is attempting to be placed.
    // This asset is sized using the box collider's bounds.
    private GameObject shadowAsset = null;

    // The location at which the object will be placed.
    private Vector3 targetPosition;

    /// <summary>
    /// Called when the GameObject is created.
    /// </summary>
    private void Awake()
    {
        targetPosition = gameObject.transform.position;

        // Get the object's collider.
        boxCollider = gameObject.GetComponent<BoxCollider>();
        if (boxCollider == null)
        {
            // The object does not have a collider, create one and remember that
            // we are managing it.
            managingBoxCollider = true;
            boxCollider = gameObject.AddComponent<BoxCollider>();
            boxCollider.enabled = false;
        }

        // Create the object that will be used to indicate the bounds of the GameObject.
        boundsAsset = GameObject.CreatePrimitive(PrimitiveType.Cube);
        boundsAsset.transform.parent = gameObject.transform;
        boundsAsset.SetActive(false);

        // Create a object that will be used as a shadow.
        shadowAsset = GameObject.CreatePrimitive(PrimitiveType.Quad);
        shadowAsset.transform.parent = gameObject.transform;
        shadowAsset.SetActive(false);
    }

    /// <summary>
    /// Called when our object is selected.  Generally called by
    /// a gesture management component.
    /// </summary>
    public void OnSelect()
    {
        /* TODO: 4.a CODE ALONG 4.a */

        if (!IsPlacing)
        {
            OnPlacementStart();
        }
        else
        {
            OnPlacementStop();
        }
    }

    /// <summary>
    /// Called once per frame.
    /// </summary>
    private void Update()
    {
        /* TODO: 4.a CODE ALONG 4.a */

        if (IsPlacing)
        {
            // Move the object.
            Move();

            // Set the visual elements.
            Vector3 targetPosition;
            Vector3 surfaceNormal;
            bool canBePlaced = ValidatePlacement(out targetPosition, out surfaceNormal);
            DisplayBounds(canBePlaced);
            DisplayShadow(targetPosition, surfaceNormal, canBePlaced);
        }
        else
        {
            // Disable the visual elements.
            boundsAsset.SetActive(false);
            shadowAsset.SetActive(false);

            // Gracefully place the object on the target surface.
            float dist = (gameObject.transform.position - targetPosition).magnitude;
            if (dist > 0)
            {
                gameObject.transform.position = Vector3.Lerp(gameObject.transform.position, targetPosition, placementVelocity / dist);
            }
            else
            {
                // Unhide the child object(s) to make placement easier.
                for (int i = 0; i < ChildrenToHide.Count; i++)
                {
                    ChildrenToHide[i].SetActive(true);
                }
            }
        }
    }

    /// <summary>
    /// Verify whether or not the object can be placed.
    /// </summary>
    /// <param name="position">
    /// The target position on the surface.
    /// </param>
    /// <param name="surfaceNormal">
    /// The normal of the surface on which the object is to be placed.
    /// </param>
    /// <returns>
    /// True if the target position is valid for placing the object, otherwise false.
    /// </returns>
    private bool ValidatePlacement(out Vector3 position, out Vector3 surfaceNormal)
    {
        Vector3 raycastDirection = gameObject.transform.forward;

        if (PlacementSurface == PlacementSurfaces.Horizontal)
        {
            // Placing on horizontal surfaces.
            // Raycast from the bottom face of the box collider.
            raycastDirection = -(Vector3.up);
        }

        // Initialize out parameters.
        position = Vector3.zero;
        surfaceNormal = Vector3.zero;

        Vector3[] facePoints = GetColliderFacePoints();

        // The origin points we receive are in local space and we 
        // need to raycast in world space.
        for (int i = 0; i < facePoints.Length; i++)
        {
            facePoints[i] = gameObject.transform.TransformVector(facePoints[i]) + gameObject.transform.position;
        }

        // Cast a ray from the center of the box collider face to the surface.
        RaycastHit centerHit;
        if (!Physics.Raycast(facePoints[0],
                        raycastDirection,
                        out centerHit,
                        maximumPlacementDistance,
                        SpatialMappingManager.Instance.LayerMask))
        {
            // If the ray failed to hit the surface, we are done.
            return false;
        }

        // We have found a surface.  Set position and surfaceNormal.
        position = centerHit.point;
        surfaceNormal = centerHit.normal;

        // Cast a ray from the corners of the box collider face to the surface.
        for (int i = 1; i < facePoints.Length; i++)
        {
            RaycastHit hitInfo;
            if (Physics.Raycast(facePoints[i],
                                raycastDirection,
                                out hitInfo,
                                maximumPlacementDistance,
                                SpatialMappingManager.Instance.LayerMask))
            {
                // To be a valid placement location, each of the corners must have a similar
                // enough distance to the surface as the center point
                if (!IsEquivalentDistance(centerHit.distance, hitInfo.distance))
                {
                    return false;
                }
            }
            else
            {
                // The raycast failed to intersect with the target layer.
                return false;
            }
        }

        return true;
    }

    /// <summary>
    /// Determine the coordinates, in local space, of the box collider face that 
    /// will be placed against the target surface.
    /// </summary>
    /// <returns>
    /// Vector3 array with the center point of the face at index 0.
    /// </returns>
    private Vector3[] GetColliderFacePoints()
    {
        // Get the collider extents.  
        // The size values are twice the extents.
        Vector3 extents = boxCollider.size / 2;

        // Calculate the min and max values for each coordinate.
        float minX = boxCollider.center.x - extents.x;
        float maxX = boxCollider.center.x + extents.x;
        float minY = boxCollider.center.y - extents.y;
        float maxY = boxCollider.center.y + extents.y;
        float minZ = boxCollider.center.z - extents.z;
        float maxZ = boxCollider.center.z + extents.z;

        Vector3 center;
        Vector3 corner0;
        Vector3 corner1;
        Vector3 corner2;
        Vector3 corner3;

        if (PlacementSurface == PlacementSurfaces.Horizontal)
        {
            // Placing on horizontal surfaces.
            center = new Vector3(boxCollider.center.x, minY, boxCollider.center.z);
            corner0 = new Vector3(minX, minY, minZ);
            corner1 = new Vector3(minX, minY, maxZ);
            corner2 = new Vector3(maxX, minY, minZ);
            corner3 = new Vector3(maxX, minY, maxZ);
        }
        else
        {
            // Placing on vertical surfaces.
            center = new Vector3(boxCollider.center.x, boxCollider.center.y, maxZ);
            corner0 = new Vector3(minX, minY, maxZ);
            corner1 = new Vector3(minX, maxY, maxZ);
            corner2 = new Vector3(maxX, minY, maxZ);
            corner3 = new Vector3(maxX, maxY, maxZ);
        }

        return new Vector3[] { center, corner0, corner1, corner2, corner3 };
    }

    /// <summary>
    /// Put the object into placement mode.
    /// </summary>
    public void OnPlacementStart()
    {
        // If we are managing the collider, enable it. 
        if (managingBoxCollider)
        {
            boxCollider.enabled = true;
        }

        // Hide the child object(s) to make placement easier.
        for (int i = 0; i < ChildrenToHide.Count; i++)
        {
            ChildrenToHide[i].SetActive(false);
        }

        // Tell the gesture manager that it is to assume
        // all input is to be given to this object.
        GestureManager.Instance.OverrideFocusedObject = gameObject;

        // Enter placement mode.
        IsPlacing = true;
    }

    /// <summary>
    /// Take the object out of placement mode.
    /// </summary>
    /// <remarks>
    /// This method will leave the object in placement mode if called while
    /// the object is in an invalid location.  To determine whether or not
    /// the object has been placed, check the value of the IsPlacing property.
    /// </remarks>
    public void OnPlacementStop()
    {
        // ValidatePlacement requires a normal as an out parameter.
        Vector3 position;
        Vector3 surfaceNormal;

        // Check to see if we can exit placement mode.
        if (!ValidatePlacement(out position, out surfaceNormal))
        {
            return;
        }

        // The object is allowed to be placed.
        // We are placing at a small buffer away from the surface.
        targetPosition = position + (0.01f * surfaceNormal);

        OrientObject(true, surfaceNormal);

        // If we are managing the collider, disable it. 
        if (managingBoxCollider)
        {
            boxCollider.enabled = false;
        }

        // Tell the gesture manager that it is to resume
        // its normal behavior.
        GestureManager.Instance.OverrideFocusedObject = null;

        // Exit placement mode.
        IsPlacing = false;
    }

    /// <summary>
    /// Positions the object along the surface toward which the user is gazing.
    /// </summary>
    /// <remarks>
    /// If the user's gaze does not intersect with a surface, the object
    /// will remain at the most recently calculated distance.
    /// </remarks>
    private void Move()
    {
        Vector3 moveTo = gameObject.transform.position;
        Vector3 surfaceNormal = Vector3.zero;
        RaycastHit hitInfo;

        bool hit = Physics.Raycast(Camera.main.transform.position,
                                Camera.main.transform.forward,
                                out hitInfo,
                                20f,
                                SpatialMappingManager.Instance.LayerMask);

        if (hit)
        {
            float offsetDistance = hoverDistance;

            // Place the object a small distance away from the surface while keeping 
            // the object from going behind the user.
            if (hitInfo.distance <= hoverDistance)
            {
                offsetDistance = 0f;
            }

            moveTo = hitInfo.point + (offsetDistance * hitInfo.normal);

            lastDistance = hitInfo.distance;
            surfaceNormal = hitInfo.normal;
        }
        else
        {
            // The raycast failed to hit a surface.  In this case, keep the object at the distance of the last
            // intersected surface.
            moveTo = Camera.main.transform.position + (Camera.main.transform.forward * lastDistance);
        }

        // Follow the user's gaze.
        float dist = Mathf.Abs((gameObject.transform.position - moveTo).magnitude);
        gameObject.transform.position = Vector3.Lerp(gameObject.transform.position, moveTo, placementVelocity / dist);

        // Orient the object.
        // We are using the return value from Physics.Raycast to instruct
        // the OrientObject function to align to the vertical surface if appropriate.
        OrientObject(hit, surfaceNormal);
    }

    /// <summary>
    /// Orients the object so that it faces the user.
    /// </summary>
    /// <param name="alignToVerticalSurface">
    /// If true and the object is to be placed on a vertical surface, 
    /// orient parallel to the target surface.  If false, orient the object 
    /// to face the user.
    /// </param>
    /// <param name="surfaceNormal">
    /// The target surface's normal vector.
    /// </param>
    /// <remarks>
    /// The aligntoVerticalSurface parameter is ignored if the object
    /// is to be placed on a horizontalSurface
    /// </remarks>
    private void OrientObject(bool alignToVerticalSurface, Vector3 surfaceNormal)
    {
        Quaternion rotation = Camera.main.transform.localRotation;

        // If the user's gaze does not intersect with the Spatial Mapping mesh,
        // orient the object towards the user.
        if (alignToVerticalSurface && (PlacementSurface == PlacementSurfaces.Vertical))
        {
            // We are placing on a vertical surface.
            // If the normal of the Spatial Mapping mesh indicates that the
            // surface is vertical, orient parallel to the surface.
            if (Mathf.Abs(surfaceNormal.y) <= (1 - upNormalThreshold))
            {
                rotation = Quaternion.LookRotation(-surfaceNormal, Vector3.up);
            }
        }
        else
        {
            rotation.x = 0f;
            rotation.z = 0f;
        }

        gameObject.transform.rotation = rotation;
    }

    /// <summary>
    /// Displays the bounds asset.
    /// </summary>
    /// <param name="canBePlaced">
    /// Specifies if the object is in a valid placement location.
    /// </param>
    private void DisplayBounds(bool canBePlaced)
    {
        // Ensure the bounds asset is sized and positioned correctly.
        boundsAsset.transform.localPosition = boxCollider.center;
        boundsAsset.transform.localScale = boxCollider.size;
        boundsAsset.transform.rotation = gameObject.transform.rotation;

        // Apply the appropriate material.
        if (canBePlaced)
        {
            boundsAsset.GetComponent<Renderer>().sharedMaterial = PlaceableBoundsMaterial;
        }
        else
        {
            boundsAsset.GetComponent<Renderer>().sharedMaterial = NotPlaceableBoundsMaterial;
        }

        // Show the bounds asset.
        boundsAsset.SetActive(true);
    }

    /// <summary>
    /// Displays the placement shadow asset.
    /// </summary>
    /// <param name="position">
    /// The position at which to place the shadow asset.
    /// </param>
    /// <param name="surfaceNormal">
    /// The normal of the surface on which the asset will be placed
    /// </param>
    /// <param name="canBePlaced">
    /// Specifies if the object is in a valid placement location.
    /// </param>
    private void DisplayShadow(Vector3 position,
                            Vector3 surfaceNormal,
                            bool canBePlaced)
    {
        // Rotate and scale the shadow so that it is displayed on the correct surface and matches the object.
        float rotationX = 0.0f;

        if (PlacementSurface == PlacementSurfaces.Horizontal)
        {
            rotationX = 90.0f;
            shadowAsset.transform.localScale = new Vector3(boxCollider.size.x, boxCollider.size.z, 1);
        }
        else
        {
            shadowAsset.transform.localScale = boxCollider.size;
        }

        Quaternion rotation = Quaternion.Euler(rotationX, gameObject.transform.rotation.eulerAngles.y, 0);
        shadowAsset.transform.rotation = rotation;

        // Apply the appropriate material.
        if (canBePlaced)
        {
            shadowAsset.GetComponent<Renderer>().sharedMaterial = PlaceableShadowMaterial;
        }
        else
        {
            shadowAsset.GetComponent<Renderer>().sharedMaterial = NotPlaceableShadowMaterial;
        }

        // Show the shadow asset as appropriate.        
        if (position != Vector3.zero)
        {
            // Position the shadow a small distance from the target surface, along the normal.
            shadowAsset.transform.position = position + (0.01f * surfaceNormal);
            shadowAsset.SetActive(true);
        }
        else
        {
            shadowAsset.SetActive(false);
        }
    }

    /// <summary>
    /// Determines if two distance values should be considered equivalent. 
    /// </summary>
    /// <param name="d1">
    /// Distance to compare.
    /// </param>
    /// <param name="d2">
    /// Distance to compare.
    /// </param>
    /// <returns>
    /// True if the distances are within the desired tolerance, otherwise false.
    /// </returns>
    private bool IsEquivalentDistance(float d1, float d2)
    {
        float dist = Mathf.Abs(d1 - d2);
        return (dist <= distanceThreshold);
    }

    /// <summary>
    /// Called when the GameObject is unloaded.
    /// </summary>
    private void OnDestroy()
    {
        // Unload objects we have created.
        Destroy(boundsAsset);
        boundsAsset = null;
        Destroy(shadowAsset);
        shadowAsset = null;
    }
}
```

<span data-ttu-id="30762-327">**Générer et déployer**</span><span class="sxs-lookup"><span data-stu-id="30762-327">**Build and Deploy**</span></span>
* <span data-ttu-id="30762-328">Comme précédemment, générez le projet et déployer sur le HoloLens.</span><span class="sxs-lookup"><span data-stu-id="30762-328">As before, build the project and deploy to the HoloLens.</span></span>
* <span data-ttu-id="30762-329">Attendez la numérisation et le traitement des données de mappage spatial pour terminer.</span><span class="sxs-lookup"><span data-stu-id="30762-329">Wait for scanning and processing of the spatial mapping data to complete.</span></span>
* <span data-ttu-id="30762-330">Lorsque vous voyez le système solaire, à la zone de projection sous les regards et effectuer un mouvement sélectionnez Déplacer au sein.</span><span class="sxs-lookup"><span data-stu-id="30762-330">When you see the solar system, gaze at the projection box below and perform a select gesture to move it around.</span></span> <span data-ttu-id="30762-331">Alors que la zone de projection est sélectionnée, un cube englobant sera visible autour de la zone de projection.</span><span class="sxs-lookup"><span data-stu-id="30762-331">While the projection box is selected, a bounding cube will be visible around the projection box.</span></span>
* <span data-ttu-id="30762-332">Vous déplacer head pour utilisation dans un autre emplacement dans la salle.</span><span class="sxs-lookup"><span data-stu-id="30762-332">Move you head to gaze at a different location in the room.</span></span> <span data-ttu-id="30762-333">La zone de projection doit suit votre regard.</span><span class="sxs-lookup"><span data-stu-id="30762-333">The projection box should follow your gaze.</span></span> <span data-ttu-id="30762-334">Lors de l’ombre sous la zone de projection devient rouge, vous ne pouvez pas placer l’hologramme sur cette surface.</span><span class="sxs-lookup"><span data-stu-id="30762-334">When the shadow below the projection box turns red, you cannot place the hologram on that surface.</span></span> <span data-ttu-id="30762-335">Lors de l’ombre sous la zone de projection devient verte, vous pouvez placer l’hologramme en effectuant des mouvements de sélectionner un autre.</span><span class="sxs-lookup"><span data-stu-id="30762-335">When the shadow below the projection box turns green, you can place the hologram by performing another select gesture.</span></span>
* <span data-ttu-id="30762-336">Recherchez et sélectionnez une des affiches HOLOGRAPHIQUE sur un mur pour le déplacer vers un nouvel emplacement.</span><span class="sxs-lookup"><span data-stu-id="30762-336">Find and select one of the holographic posters on a wall to move it to a new location.</span></span> <span data-ttu-id="30762-337">Notez que vous ne pouvez pas placer l’affiche sur le plancher ou le plafond, et qu’elle reste correctement orienté vers chaque mur que vous déplacez.</span><span class="sxs-lookup"><span data-stu-id="30762-337">Notice that you cannot place the poster on the floor or ceiling, and that it stays correctly oriented to each wall as you move around.</span></span>

## <a name="chapter-5---occlusion"></a><span data-ttu-id="30762-338">Chapitre 5 - Occlusion</span><span class="sxs-lookup"><span data-stu-id="30762-338">Chapter 5 - Occlusion</span></span>

>[!VIDEO https://www.youtube.com/embed/6Xrzh_w-7SE]

<span data-ttu-id="30762-339">**Objectifs**</span><span class="sxs-lookup"><span data-stu-id="30762-339">**Objectives**</span></span>
* <span data-ttu-id="30762-340">Déterminer si un hologramme est bloqué par la maille de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="30762-340">Determine if a hologram is occluded by the spatial mapping mesh.</span></span>
* <span data-ttu-id="30762-341">Appliquer des techniques d’occlusion différentes pour atteindre un plaisir effet.</span><span class="sxs-lookup"><span data-stu-id="30762-341">Apply different occlusion techniques to achieve a fun effect.</span></span>

<span data-ttu-id="30762-342">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="30762-342">**Instructions**</span></span>

<span data-ttu-id="30762-343">Tout d’abord, nous allons autoriser la maille de mappage spatial occlude autres hologrammes sans OCCLUSION le monde réel :</span><span class="sxs-lookup"><span data-stu-id="30762-343">First, we are going to allow the spatial mapping mesh to occlude other holograms without occluding the real world:</span></span>
* <span data-ttu-id="30762-344">Dans le **hiérarchie** Panneau de configuration, sélectionnez le **SpatialProcessing** objet.</span><span class="sxs-lookup"><span data-stu-id="30762-344">In the **Hierarchy** panel, select the **SpatialProcessing** object.</span></span>
* <span data-ttu-id="30762-345">Dans le **inspecteur** panneau, recherchez le **lire Gestionnaire d’espace (Script)** composant.</span><span class="sxs-lookup"><span data-stu-id="30762-345">In the **Inspector** panel, find the **Play Space Manager (Script)** component.</span></span>
* <span data-ttu-id="30762-346">Cliquez sur le cercle à droite de la **matériau secondaire** propriété.</span><span class="sxs-lookup"><span data-stu-id="30762-346">Click the circle to the right of the **Secondary Material** property.</span></span>
* <span data-ttu-id="30762-347">Recherchez et sélectionnez le **Occlusion** matériau et fermer la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="30762-347">Find and select the **Occlusion** material and close the window.</span></span>

<span data-ttu-id="30762-348">Ensuite, nous allons ajouter un comportement spécial à terre, afin qu’il ait une surbrillance bleue chaque fois qu’il devienne bloqué par un autre hologramme (par exemple, le soleil), ou par la maille de mappage spatial :</span><span class="sxs-lookup"><span data-stu-id="30762-348">Next, we are going to add a special behavior to Earth, so that it has a blue highlight whenever it becomes occluded by another hologram (like the sun), or by the spatial mapping mesh:</span></span>
* <span data-ttu-id="30762-349">Dans le **projet** volet le **Vntana** dossier, développez le **SolarSystem** objet.</span><span class="sxs-lookup"><span data-stu-id="30762-349">In the **Project** panel, in the **Holograms** folder, expand the **SolarSystem** object.</span></span>
* <span data-ttu-id="30762-350">Cliquez sur **Earth**.</span><span class="sxs-lookup"><span data-stu-id="30762-350">Click on **Earth**.</span></span>
* <span data-ttu-id="30762-351">Dans le **inspecteur** panel, trouver les documents de la terre (composant du bas).</span><span class="sxs-lookup"><span data-stu-id="30762-351">In the **Inspector** panel, find the Earth's material (bottom component).</span></span>
* <span data-ttu-id="30762-352">Dans le **déroulante nuanceur**, modifier le nuanceur **personnalisé > OcclusionRim**.</span><span class="sxs-lookup"><span data-stu-id="30762-352">In the **Shader drop-down**, change the shader to **Custom > OcclusionRim**.</span></span> <span data-ttu-id="30762-353">Cela affichera une surbrillance bleue autour de la terre chaque fois qu’il est bloqué par un autre objet.</span><span class="sxs-lookup"><span data-stu-id="30762-353">This will render a blue highlight around Earth whenever it is occluded by another object.</span></span>

<span data-ttu-id="30762-354">Enfin, nous allons activer un effet de vision x-Ray pour planètes dans notre système solaire.</span><span class="sxs-lookup"><span data-stu-id="30762-354">Finally, we are going to enable an x-ray vision effect for planets in our solar system.</span></span> <span data-ttu-id="30762-355">Nous devons modifier **PlanetOcclusion.cs** (figurant dans le dossier Scripts\SolarSystem) afin d’atteindre les objectifs suivants :</span><span class="sxs-lookup"><span data-stu-id="30762-355">We will need to edit **PlanetOcclusion.cs** (found in the Scripts\SolarSystem folder) in order to achieve the following:</span></span>
1. <span data-ttu-id="30762-356">Déterminer si une planète est bloquée par la couche de SpatialMapping (salle mailles et plans).</span><span class="sxs-lookup"><span data-stu-id="30762-356">Determine if a planet is occluded by the SpatialMapping layer (room meshes and planes).</span></span>
2. <span data-ttu-id="30762-357">Afficher la représentation sous forme de maquette d’une planète chaque fois qu’il est bloqué par la couche SpatialMapping.</span><span class="sxs-lookup"><span data-stu-id="30762-357">Show the wireframe representation of a planet whenever it is occluded by the SpatialMapping layer.</span></span>
3. <span data-ttu-id="30762-358">Masquer la représentation sous forme de maquette d’une planète lorsqu’il n’est pas bloqué par la couche SpatialMapping.</span><span class="sxs-lookup"><span data-stu-id="30762-358">Hide the wireframe representation of a planet when it is not blocked by the SpatialMapping layer.</span></span>

<span data-ttu-id="30762-359">Suivez l’exercice de codage dans PlanetOcclusion.cs, ou utiliser la solution suivante :</span><span class="sxs-lookup"><span data-stu-id="30762-359">Follow the coding exercise in PlanetOcclusion.cs, or use the following solution:</span></span>

```cs
using UnityEngine;
using Academy.HoloToolkit.Unity;

/// <summary>
/// Determines when the occluded version of the planet should be visible.
/// This script allows us to do selective occlusion, so the occlusionObject
/// will only be rendered when a Spatial Mapping surface is occluding the planet,
/// not when another hologram is responsible for the occlusion.
/// </summary>
public class PlanetOcclusion : MonoBehaviour
{
    [Tooltip("Object to display when the planet is occluded.")]
    public GameObject occlusionObject;

    /// <summary>
    /// Points to raycast to when checking for occlusion.
    /// </summary>
    private Vector3[] checkPoints;

    // Use this for initialization
    void Start()
    {
        occlusionObject.SetActive(false);

        // Set the check points to use when testing for occlusion.
        MeshFilter filter = gameObject.GetComponent<MeshFilter>();
        Vector3 extents = filter.mesh.bounds.extents;
        Vector3 center = filter.mesh.bounds.center;
        Vector3 top = new Vector3(center.x, center.y + extents.y, center.z);
        Vector3 left = new Vector3(center.x - extents.x, center.y, center.z);
        Vector3 right = new Vector3(center.x + extents.x, center.y, center.z);
        Vector3 bottom = new Vector3(center.x, center.y - extents.y, center.z);

        checkPoints = new Vector3[] { center, top, left, right, bottom };
    }

    // Update is called once per frame
    void Update()
    {
        /* TODO: 5.a DEVELOPER CODING EXERCISE 5.a */

        // Check to see if any of the planet's boundary points are occluded.
        for (int i = 0; i < checkPoints.Length; i++)
        {
            // 5.a: Convert the current checkPoint to world coordinates.
            // Call gameObject.transform.TransformPoint(checkPoints[i]).
            // Assign the result to a new Vector3 variable called 'checkPt'.
            Vector3 checkPt = gameObject.transform.TransformPoint(checkPoints[i]);

            // 5.a: Call Vector3.Distance() to calculate the distance
            // between the Main Camera's position and 'checkPt'.
            // Assign the result to a new float variable called 'distance'.
            float distance = Vector3.Distance(Camera.main.transform.position, checkPt);

            // 5.a: Take 'checkPt' and subtract the Main Camera's position from it.
            // Assign the result to a new Vector3 variable called 'direction'.
            Vector3 direction = checkPt - Camera.main.transform.position;

            // Used to indicate if the call to Physics.Raycast() was successful.
            bool raycastHit = false;

            // 5.a: Check if the planet is occluded by a spatial mapping surface.
            // Call Physics.Raycast() with the following arguments:
            // - Pass in the Main Camera's position as the origin.
            // - Pass in 'direction' for the direction.
            // - Pass in 'distance' for the maxDistance.
            // - Pass in SpatialMappingManager.Instance.LayerMask as layerMask.
            // Assign the result to 'raycastHit'.
            raycastHit = Physics.Raycast(Camera.main.transform.position, direction, distance, SpatialMappingManager.Instance.LayerMask);

            if (raycastHit)
            {
                // 5.a: Our raycast hit a surface, so the planet is occluded.
                // Set the occlusionObject to active.
                occlusionObject.SetActive(true);

                // At least one point is occluded, so break from the loop.
                break;
            }
            else
            {
                // 5.a: The Raycast did not hit, so the planet is not occluded.
                // Deactivate the occlusionObject.
                occlusionObject.SetActive(false);
            }
        }
    }
}
```

<span data-ttu-id="30762-360">**Générer et déployer**</span><span class="sxs-lookup"><span data-stu-id="30762-360">**Build and Deploy**</span></span>
* <span data-ttu-id="30762-361">Générer et déployer l’application sur HoloLens, comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="30762-361">Build and deploy the application to HoloLens, as usual.</span></span>
* <span data-ttu-id="30762-362">Attendre que l’analyse et le traitement des données spatiales de mappage complet (vous devez voir les lignes bleues apparaissent sur les murs).</span><span class="sxs-lookup"><span data-stu-id="30762-362">Wait for scanning and processing of the spatial mapping data to be complete (you should see blue lines appear on walls).</span></span>
* <span data-ttu-id="30762-363">Recherchez et sélectionnez la zone de projection du système solaire puis définissez la zone en regard d’un mur ou derrière un compteur.</span><span class="sxs-lookup"><span data-stu-id="30762-363">Find and select the solar system's projection box and then set the box next to a wall or behind a counter.</span></span>
* <span data-ttu-id="30762-364">Vous pouvez afficher l’occlusion base en se cachant derrière les surfaces à homologuer à la zone affiche ou de projection.</span><span class="sxs-lookup"><span data-stu-id="30762-364">You can view basic occlusion by hiding behind surfaces to peer at the poster or projection box.</span></span>
* <span data-ttu-id="30762-365">Recherchez la terre, il doit y avoir un effet de la surbrillance bleue chaque fois qu’il va derrière un autre hologramme ou surface.</span><span class="sxs-lookup"><span data-stu-id="30762-365">Look for the Earth, there should be a blue highlight effect whenever it goes behind another hologram or surface.</span></span>
* <span data-ttu-id="30762-366">Écoutez les planètes déplacement derrière le mur ou autres surfaces dans la salle.</span><span class="sxs-lookup"><span data-stu-id="30762-366">Watch as the planets move behind the wall or other surfaces in the room.</span></span> <span data-ttu-id="30762-367">Vous avez vision rayons x et pourrez voir leurs squelettes filaire !</span><span class="sxs-lookup"><span data-stu-id="30762-367">You now have x-ray vision and can see their wireframe skeletons!</span></span>

## <a name="the-end"></a><span data-ttu-id="30762-368">La fin</span><span class="sxs-lookup"><span data-stu-id="30762-368">The End</span></span>

<span data-ttu-id="30762-369">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="30762-369">Congratulations!</span></span> <span data-ttu-id="30762-370">Vous avez maintenant terminé **230 Spatial MR : Mappage spatial**.</span><span class="sxs-lookup"><span data-stu-id="30762-370">You have now completed **MR Spatial 230: Spatial mapping**.</span></span>
* <span data-ttu-id="30762-371">Vous savez comment analyser vos données d’environnement et charge le mappage spatial à Unity.</span><span class="sxs-lookup"><span data-stu-id="30762-371">You know how to scan your environment and load spatial mapping data to Unity.</span></span>
* <span data-ttu-id="30762-372">Vous comprenez les principes fondamentaux de nuanceurs et utilisation des supports pour visualiser de nouveau le monde.</span><span class="sxs-lookup"><span data-stu-id="30762-372">You understand the basics of shaders and how materials can be used to re-visualize the world.</span></span>
* <span data-ttu-id="30762-373">Vous avez appris de nouvelles techniques de traitement pour trouver des plans et la suppression des triangles à partir d’une maille.</span><span class="sxs-lookup"><span data-stu-id="30762-373">You learned of new processing techniques for finding planes and removing triangles from a mesh.</span></span>
* <span data-ttu-id="30762-374">Vous avez pu déplacer et placer hologrammes sur les surfaces qui était logique.</span><span class="sxs-lookup"><span data-stu-id="30762-374">You were able to move and place holograms on surfaces that made sense.</span></span>
* <span data-ttu-id="30762-375">Vous a rencontré des techniques différentes occlusion et d’exploiter la puissance de vision rayons x !</span><span class="sxs-lookup"><span data-stu-id="30762-375">You experienced different occlusion techniques and harnessed the power of x-ray vision!</span></span>
