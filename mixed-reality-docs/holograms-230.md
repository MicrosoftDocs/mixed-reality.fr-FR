---
title: MR spatial 230-spatial Mapping
description: Suivez cette procédure pas à pas de codage à l’aide d’Unity, Visual Studio et HoloLens pour apprendre les concepts de mappage spatial.
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, Academy, didacticiel, mappage spatial, reconstruction de surface, maille
ms.openlocfilehash: cf4a2dd3e5eb74c0aaf849442e5f5e404d7cb661
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73434579"
---
>[!NOTE]
><span data-ttu-id="e2081-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="e2081-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="e2081-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="e2081-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="e2081-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="e2081-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="e2081-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e2081-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="e2081-108">[Une nouvelle série de didacticiels](mrlearning-base.md) a été publiée pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="e2081-108">[A new series of tutorials](mrlearning-base.md) has been posted for HoloLens 2.</span></span>

<br>

# <a name="mr-spatial-230-spatial-mapping"></a><span data-ttu-id="e2081-109">MR spatial 230 : mappage spatial</span><span class="sxs-lookup"><span data-stu-id="e2081-109">MR Spatial 230: Spatial mapping</span></span>

<span data-ttu-id="e2081-110">Le [mappage spatial](spatial-mapping.md) combine le monde réel et le monde virtuel ensemble en apprenant des hologrammes sur l’environnement.</span><span class="sxs-lookup"><span data-stu-id="e2081-110">[Spatial mapping](spatial-mapping.md) combines the real world and virtual world together by teaching holograms about the environment.</span></span> <span data-ttu-id="e2081-111">Dans l’spatial spatial 230 (Project Planetarium), nous allons apprendre à :</span><span class="sxs-lookup"><span data-stu-id="e2081-111">In MR Spatial 230 (Project Planetarium) we'll learn how to:</span></span>

* <span data-ttu-id="e2081-112">Analyser l’environnement et transférer des données de HoloLens vers votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="e2081-112">Scan the environment and transfer data from the HoloLens to your development machine.</span></span>
* <span data-ttu-id="e2081-113">Explorez les nuanceurs et apprenez à les utiliser pour visualiser votre espace.</span><span class="sxs-lookup"><span data-stu-id="e2081-113">Explore shaders and learn how to use them for visualizing your space.</span></span>
* <span data-ttu-id="e2081-114">Décomposez le maillage de la pièce en plans simples à l’aide du traitement de maillage.</span><span class="sxs-lookup"><span data-stu-id="e2081-114">Break down the room mesh into simple planes using mesh processing.</span></span>
* <span data-ttu-id="e2081-115">Allez au-delà des techniques de placement que nous avons appris dans les [notions de base de m. 101](holograms-101.md)et fournissez des commentaires sur l’endroit où un hologramme peut être placé dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="e2081-115">Go beyond the placement techniques we learned in [MR Basics 101](holograms-101.md), and provide feedback about where a hologram can be placed in the environment.</span></span>
* <span data-ttu-id="e2081-116">Explorez les effets d’occlusion. par conséquent, lorsque votre hologramme se trouve derrière un objet réel, vous pouvez toujours le voir avec la vision x-ray !</span><span class="sxs-lookup"><span data-stu-id="e2081-116">Explore occlusion effects, so when your hologram is behind a real-world object, you can still see it with x-ray vision!</span></span>

>[!VIDEO https://www.youtube.com/embed/NSNYRkUX6Mw]

## <a name="device-support"></a><span data-ttu-id="e2081-117">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="e2081-117">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="e2081-118">Course</span><span class="sxs-lookup"><span data-stu-id="e2081-118">Course</span></span></th><th style="width:150px"> <span data-ttu-id="e2081-119"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="e2081-119"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="e2081-120"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="e2081-120"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="e2081-121">MR spatial 230 : mappage spatial</span><span class="sxs-lookup"><span data-stu-id="e2081-121">MR Spatial 230: Spatial mapping</span></span></td><td style="text-align: center;"> <span data-ttu-id="e2081-122">✔️</span><span class="sxs-lookup"><span data-stu-id="e2081-122">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="e2081-123">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e2081-123">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e2081-124">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="e2081-124">Prerequisites</span></span>

* <span data-ttu-id="e2081-125">Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="e2081-125">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="e2081-126">Certaines fonctionnalités C# de programmation de base.</span><span class="sxs-lookup"><span data-stu-id="e2081-126">Some basic C# programming ability.</span></span>
* <span data-ttu-id="e2081-127">Vous devez avoir terminé les [notions de base de m. 101](holograms-101.md).</span><span class="sxs-lookup"><span data-stu-id="e2081-127">You should have completed [MR Basics 101](holograms-101.md).</span></span>
* <span data-ttu-id="e2081-128">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="e2081-128">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="e2081-129">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="e2081-129">Project files</span></span>

* <span data-ttu-id="e2081-130">Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-230-SpatialMapping.zip) requis par le projet.</span><span class="sxs-lookup"><span data-stu-id="e2081-130">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-230-SpatialMapping.zip) required by the project.</span></span><span data-ttu-id="e2081-131"> Requiert Unity 2017,2 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e2081-131"> Requires Unity 2017.2 or later.</span></span>
  * <span data-ttu-id="e2081-132">Si vous avez encore besoin de la prise en charge d’Unity 5,6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-230.zip).</span><span class="sxs-lookup"><span data-stu-id="e2081-132">If you still need Unity 5.6 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-230.zip).</span></span>
  * <span data-ttu-id="e2081-133">Si vous avez encore besoin de la prise en charge d’Unity 5,5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-230.zip).</span><span class="sxs-lookup"><span data-stu-id="e2081-133">If you still need Unity 5.5 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-230.zip).</span></span>
  * <span data-ttu-id="e2081-134">Si vous avez encore besoin de la prise en charge d’Unity 5,4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-230.zip).</span><span class="sxs-lookup"><span data-stu-id="e2081-134">If you still need Unity 5.4 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-230.zip).</span></span>
* <span data-ttu-id="e2081-135">Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.</span><span class="sxs-lookup"><span data-stu-id="e2081-135">Un-archive the files to your desktop or other easy to reach location.</span></span>

>[!NOTE]
><span data-ttu-id="e2081-136">Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-230-SpatialMapping).</span><span class="sxs-lookup"><span data-stu-id="e2081-136">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-230-SpatialMapping).</span></span>

### <a name="notes"></a><span data-ttu-id="e2081-137">Notes</span><span class="sxs-lookup"><span data-stu-id="e2081-137">Notes</span></span>

* <span data-ttu-id="e2081-138">Dans Visual Studio, l’option « Activer Uniquement mon code » doit être désactivée (*décochée*) sous Outils > Options > débogage pour atteindre les points d’arrêt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="e2081-138">"Enable Just My Code" in Visual Studio needs to be disabled (*unchecked*) under Tools > Options > Debugging in order to hit breakpoints in your code.</span></span>

## <a name="unity-setup"></a><span data-ttu-id="e2081-139">Configuration de Unity</span><span class="sxs-lookup"><span data-stu-id="e2081-139">Unity setup</span></span>

>[!VIDEO https://www.youtube.com/embed/y2Y4LhK6TEM]

* <span data-ttu-id="e2081-140">Démarrez **Unity**.</span><span class="sxs-lookup"><span data-stu-id="e2081-140">Start **Unity**.</span></span>
* <span data-ttu-id="e2081-141">Sélectionnez **nouveau** pour créer un nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="e2081-141">Select **New** to create a new project.</span></span>
* <span data-ttu-id="e2081-142">Nommez le projet **Planetarium**.</span><span class="sxs-lookup"><span data-stu-id="e2081-142">Name the project **Planetarium**.</span></span>
* <span data-ttu-id="e2081-143">Vérifiez que le paramètre **3D** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e2081-143">Verify that the **3D** setting is selected.</span></span>
* <span data-ttu-id="e2081-144">Cliquez sur **Create Project**.</span><span class="sxs-lookup"><span data-stu-id="e2081-144">Click **Create Project**.</span></span>
* <span data-ttu-id="e2081-145">Une fois Unity lancé, accédez à **modifier > paramètres du projet > Player**.</span><span class="sxs-lookup"><span data-stu-id="e2081-145">Once Unity launches, go to **Edit > Project Settings > Player**.</span></span>
* <span data-ttu-id="e2081-146">Dans le volet de l' **inspecteur** , recherchez et sélectionnez l’icône du **Windows Store** vert.</span><span class="sxs-lookup"><span data-stu-id="e2081-146">In the **Inspector** panel, find and select the green **Windows Store** icon.</span></span>
* <span data-ttu-id="e2081-147">Développez **autres paramètres**.</span><span class="sxs-lookup"><span data-stu-id="e2081-147">Expand **Other Settings**.</span></span>
* <span data-ttu-id="e2081-148">Dans la section **rendu** , activez la case à cocher **prise en charge de la réalité virtuelle** .</span><span class="sxs-lookup"><span data-stu-id="e2081-148">In the **Rendering** section, check the **Virtual Reality Supported** option.</span></span>
* <span data-ttu-id="e2081-149">Vérifiez que **Windows holographique** apparaît dans la liste des kits de développement logiciel (SDK) de **réalité virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="e2081-149">Verify that **Windows Holographic** appears in the list of **Virtual Reality SDKs**.</span></span> <span data-ttu-id="e2081-150">Si ce n’est pas le cas, sélectionnez le bouton **+** au bas de la liste et choisissez **Windows holographique**.</span><span class="sxs-lookup"><span data-stu-id="e2081-150">If not, select the **+** button at the bottom of the list and choose **Windows Holographic**.</span></span>
* <span data-ttu-id="e2081-151">Développez **paramètres de publication**.</span><span class="sxs-lookup"><span data-stu-id="e2081-151">Expand **Publishing Settings**.</span></span>
* <span data-ttu-id="e2081-152">Dans la section **fonctionnalités** , vérifiez les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="e2081-152">In the **Capabilities** section, check the following settings:</span></span>
    * <span data-ttu-id="e2081-153">InternetClientServer</span><span class="sxs-lookup"><span data-stu-id="e2081-153">InternetClientServer</span></span>
    * <span data-ttu-id="e2081-154">PrivateNetworkClientServer</span><span class="sxs-lookup"><span data-stu-id="e2081-154">PrivateNetworkClientServer</span></span>
    * <span data-ttu-id="e2081-155">Microphone</span><span class="sxs-lookup"><span data-stu-id="e2081-155">Microphone</span></span>
    * <span data-ttu-id="e2081-156">SpatialPerception</span><span class="sxs-lookup"><span data-stu-id="e2081-156">SpatialPerception</span></span>
* <span data-ttu-id="e2081-157">Accédez à **modifier > paramètres du projet > qualité**</span><span class="sxs-lookup"><span data-stu-id="e2081-157">Go to **Edit > Project Settings > Quality**</span></span>
* <span data-ttu-id="e2081-158">Dans le volet de l' **inspecteur** , sous l’icône Windows Store, sélectionnez la flèche déroulante noire sous la ligne « default » et définissez le paramètre par défaut sur **très faible**.</span><span class="sxs-lookup"><span data-stu-id="e2081-158">In the **Inspector** panel, under the Windows Store icon, select the black drop-down arrow under the 'Default' row and change the default setting to **Very Low**.</span></span>
* <span data-ttu-id="e2081-159">Accédez à **ressources > importer un package > package personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="e2081-159">Go to **Assets > Import Package > Custom Package**.</span></span>
* <span data-ttu-id="e2081-160">Accédez au dossier **. ..\holographicacademy-holograms-230-SpatialMapping\Starting** .</span><span class="sxs-lookup"><span data-stu-id="e2081-160">Navigate to the **...\HolographicAcademy-Holograms-230-SpatialMapping\Starting** folder.</span></span>
* <span data-ttu-id="e2081-161">Cliquez sur **Planetarium. pour Unity**.</span><span class="sxs-lookup"><span data-stu-id="e2081-161">Click on **Planetarium.unitypackage**.</span></span>
* <span data-ttu-id="e2081-162">Cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="e2081-162">Click **Open**.</span></span>
* <span data-ttu-id="e2081-163">Une fenêtre **Importer un package Unity** doit s’afficher. cliquez sur le bouton **Importer** .</span><span class="sxs-lookup"><span data-stu-id="e2081-163">An **Import Unity Package** window should appear, click on the **Import** button.</span></span>
* <span data-ttu-id="e2081-164">Attendez que Unity importe toutes les ressources dont nous aurons besoin pour terminer ce projet.</span><span class="sxs-lookup"><span data-stu-id="e2081-164">Wait for Unity to import all of the assets that we will need to complete this project.</span></span>
* <span data-ttu-id="e2081-165">Dans le panneau **hiérarchie** , supprimez l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="e2081-165">In the **Hierarchy** panel, delete the **Main Camera**.</span></span>
* <span data-ttu-id="e2081-166">Dans le panneau **projet** , dans le dossier **HoloToolkit-SpatialMapping-230\Utilities\Prefabs** , recherchez l’objet **Camera principal** .</span><span class="sxs-lookup"><span data-stu-id="e2081-166">In the **Project** panel, **HoloToolkit-SpatialMapping-230\Utilities\Prefabs** folder, find the **Main Camera** object.</span></span>
* <span data-ttu-id="e2081-167">Glissez-déplacez le Prefab d' **appareil photo principal** dans le panneau de **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="e2081-167">Drag and drop the **Main Camera** prefab into the **Hierarchy** panel.</span></span>
* <span data-ttu-id="e2081-168">Dans le panneau **hiérarchie** , supprimez l’objet de **lumière directionnelle** .</span><span class="sxs-lookup"><span data-stu-id="e2081-168">In the **Hierarchy** panel, delete the **Directional Light** object.</span></span>
* <span data-ttu-id="e2081-169">Dans le panneau **projet** , dans le dossier **hologrammes** , localisez l’objet **curseur** .</span><span class="sxs-lookup"><span data-stu-id="e2081-169">In the **Project** panel, **Holograms** folder, locate the **Cursor** object.</span></span>
* <span data-ttu-id="e2081-170">Faites glisser & déposez le **curseur** Prefab dans la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="e2081-170">Drag & drop the **Cursor** prefab into the **Hierarchy**.</span></span>
* <span data-ttu-id="e2081-171">Dans le volet **hiérarchie** , sélectionnez l’objet **curseur** .</span><span class="sxs-lookup"><span data-stu-id="e2081-171">In the **Hierarchy** panel, select the **Cursor** object.</span></span>
* <span data-ttu-id="e2081-172">Dans le panneau **inspecteur** , cliquez sur la liste déroulante **couche** , puis sélectionnez **modifier les couches...** .</span><span class="sxs-lookup"><span data-stu-id="e2081-172">In the **Inspector** panel, click the **Layer** drop-down and select **Edit Layers...**.</span></span>
* <span data-ttu-id="e2081-173">Nommez **User Layer 31** en «**SpatialMapping**».</span><span class="sxs-lookup"><span data-stu-id="e2081-173">Name **User Layer 31** as "**SpatialMapping**".</span></span>
* <span data-ttu-id="e2081-174">Enregistrez la nouvelle scène : **fichier > enregistrer la scène sous...**</span><span class="sxs-lookup"><span data-stu-id="e2081-174">Save the new scene: **File > Save Scene As...**</span></span>
* <span data-ttu-id="e2081-175">Cliquez sur **nouveau dossier** et nommez le dossier **scenes**.</span><span class="sxs-lookup"><span data-stu-id="e2081-175">Click **New Folder** and name the folder **Scenes**.</span></span>
* <span data-ttu-id="e2081-176">Nommez le fichier «**Planetarium**» et enregistrez-le dans le dossier **scenes** .</span><span class="sxs-lookup"><span data-stu-id="e2081-176">Name the file "**Planetarium**" and save it in the **Scenes** folder.</span></span>

## <a name="chapter-1---scanning"></a><span data-ttu-id="e2081-177">Chapitre 1-analyse</span><span class="sxs-lookup"><span data-stu-id="e2081-177">Chapter 1 - Scanning</span></span>

>[!VIDEO https://www.youtube.com/embed/888oW51z_cE]

<span data-ttu-id="e2081-178">**Cherché**</span><span class="sxs-lookup"><span data-stu-id="e2081-178">**Objectives**</span></span>

* <span data-ttu-id="e2081-179">Découvrez le SurfaceObserver et comment ses paramètres affectent l’expérience et les performances.</span><span class="sxs-lookup"><span data-stu-id="e2081-179">Learn about the SurfaceObserver and how its settings impact experience and performance.</span></span>
* <span data-ttu-id="e2081-180">Créez une expérience de numérisation de salle pour collecter les mailles de votre salle.</span><span class="sxs-lookup"><span data-stu-id="e2081-180">Create a room scanning experience to collect the meshes of your room.</span></span>

<span data-ttu-id="e2081-181">**Ample**</span><span class="sxs-lookup"><span data-stu-id="e2081-181">**Instructions**</span></span>

* <span data-ttu-id="e2081-182">Dans le dossier **HoloToolkit-SpatialMapping-230\SpatialMapping\Prefabs** du panneau **projet** , recherchez le Prefab **SpatialMapping** .</span><span class="sxs-lookup"><span data-stu-id="e2081-182">In the **Project** panel **HoloToolkit-SpatialMapping-230\SpatialMapping\Prefabs** folder, find the **SpatialMapping** prefab.</span></span>
* <span data-ttu-id="e2081-183">Faites glisser & déposer le Prefab **SpatialMapping** dans le panneau de **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="e2081-183">Drag & drop the **SpatialMapping** prefab into the **Hierarchy** panel.</span></span>

<span data-ttu-id="e2081-184">**Création et déploiement (partie 1)**</span><span class="sxs-lookup"><span data-stu-id="e2081-184">**Build and Deploy (part 1)**</span></span>

* <span data-ttu-id="e2081-185">Dans Unity, sélectionnez **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="e2081-185">In Unity, select **File > Build Settings**.</span></span>
* <span data-ttu-id="e2081-186">Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène **Planetarium** à la Build.</span><span class="sxs-lookup"><span data-stu-id="e2081-186">Click **Add Open Scenes** to add the **Planetarium** scene to the build.</span></span>
* <span data-ttu-id="e2081-187">Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur **basculer la plateforme**.</span><span class="sxs-lookup"><span data-stu-id="e2081-187">Select **Universal Windows Platform** in the **Platform** list and click **Switch Platform**.</span></span>
* <span data-ttu-id="e2081-188">Définissez le **SDK** sur le **type de build** **Universal 10** et UWP sur **D3D**.</span><span class="sxs-lookup"><span data-stu-id="e2081-188">Set **SDK** to **Universal 10** and **UWP Build Type** to **D3D**.</span></span>
* <span data-ttu-id="e2081-189">Vérifiez **les C# projets Unity**.</span><span class="sxs-lookup"><span data-stu-id="e2081-189">Check **Unity C# Projects**.</span></span>
* <span data-ttu-id="e2081-190">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="e2081-190">Click **Build**.</span></span>
* <span data-ttu-id="e2081-191">Créez un **dossier** nommé « App ».</span><span class="sxs-lookup"><span data-stu-id="e2081-191">Create a **New Folder** named "App".</span></span>
* <span data-ttu-id="e2081-192">Cliquez sur le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="e2081-192">Single click the **App** folder.</span></span>
* <span data-ttu-id="e2081-193">Appuyez sur le bouton **Sélectionner un dossier** .</span><span class="sxs-lookup"><span data-stu-id="e2081-193">Press the **Select Folder** button.</span></span>
* <span data-ttu-id="e2081-194">Une fois la création d’Unity terminée, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e2081-194">When Unity is done building, a File Explorer window will appear.</span></span>
* <span data-ttu-id="e2081-195">Double-cliquez sur le dossier de l' **application** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="e2081-195">Double-click on the **App** folder to open it.</span></span>
* <span data-ttu-id="e2081-196">Double-cliquez sur **Planetarium. sln** pour charger le projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2081-196">Double-click on **Planetarium.sln** to load the project in Visual Studio.</span></span>
* <span data-ttu-id="e2081-197">Dans Visual Studio, utilisez la barre d’outils supérieure pour changer la configuration en **Release**.</span><span class="sxs-lookup"><span data-stu-id="e2081-197">In Visual Studio, use the top toolbar to change the Configuration to **Release**.</span></span>
* <span data-ttu-id="e2081-198">Remplacez la plateforme par **x86**.</span><span class="sxs-lookup"><span data-stu-id="e2081-198">Change the Platform to **x86**.</span></span>
* <span data-ttu-id="e2081-199">Cliquez sur la flèche déroulante à droite de « ordinateur local », puis sélectionnez **ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="e2081-199">Click on the drop-down arrow to the right of 'Local Machine', and select **Remote Machine**.</span></span>
* <span data-ttu-id="e2081-200">Entrez l' [adresse IP de votre appareil](connecting-to-wi-fi-on-hololens.md#identifying-the-ip-address-of-your-hololens-on-the-wi-fi-network) dans le champ adresse et changez le mode d’authentification en **protocole universel (protocole non chiffré)** .</span><span class="sxs-lookup"><span data-stu-id="e2081-200">Enter [your device's IP address](connecting-to-wi-fi-on-hololens.md#identifying-the-ip-address-of-your-hololens-on-the-wi-fi-network) in the Address field and change Authentication Mode to **Universal (Unencrypted Protocol)**.</span></span>
* <span data-ttu-id="e2081-201">Cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="e2081-201">Click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
* <span data-ttu-id="e2081-202">Regardez le panneau de **sortie** dans Visual Studio pour l’état de génération et de déploiement.</span><span class="sxs-lookup"><span data-stu-id="e2081-202">Watch the **Output** panel in Visual Studio for build and deploy status.</span></span>
* <span data-ttu-id="e2081-203">Une fois votre application déployée, parcourez la salle.</span><span class="sxs-lookup"><span data-stu-id="e2081-203">Once your app has deployed, walk around the room.</span></span> <span data-ttu-id="e2081-204">Vous verrez les surfaces environnantes couvertes par les maillages filaires noir et blanc.</span><span class="sxs-lookup"><span data-stu-id="e2081-204">You will see the surrounding surfaces covered by black and white wireframe meshes.</span></span>
* <span data-ttu-id="e2081-205">Analysez votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e2081-205">Scan your surroundings.</span></span> <span data-ttu-id="e2081-206">Veillez à examiner les murs, les limites et les étages.</span><span class="sxs-lookup"><span data-stu-id="e2081-206">Be sure to look at walls, ceilings, and floors.</span></span>

<span data-ttu-id="e2081-207">**Génération et déploiement (partie 2)**</span><span class="sxs-lookup"><span data-stu-id="e2081-207">**Build and Deploy (part 2)**</span></span>

<span data-ttu-id="e2081-208">Voyons maintenant comment le mappage spatial peut affecter les performances.</span><span class="sxs-lookup"><span data-stu-id="e2081-208">Now let's explore how Spatial Mapping can affect performance.</span></span>

* <span data-ttu-id="e2081-209">Dans Unity, sélectionnez **windows > Profiler**.</span><span class="sxs-lookup"><span data-stu-id="e2081-209">In Unity, select **Window > Profiler**.</span></span>
* <span data-ttu-id="e2081-210">Cliquez sur **Ajouter profiler > GPU**.</span><span class="sxs-lookup"><span data-stu-id="e2081-210">Click **Add Profiler > GPU**.</span></span>
* <span data-ttu-id="e2081-211">Cliquez sur **> du profileur Active <Enter IP>** .</span><span class="sxs-lookup"><span data-stu-id="e2081-211">Click **Active Profiler > <Enter IP>**.</span></span>
* <span data-ttu-id="e2081-212">Entrez l' **adresse IP** de votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="e2081-212">Enter the **IP address** of your HoloLens.</span></span>
* <span data-ttu-id="e2081-213">Cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="e2081-213">Click **Connect**.</span></span>
* <span data-ttu-id="e2081-214">Observez le nombre de millisecondes nécessaires au rendu d’une trame par le GPU.</span><span class="sxs-lookup"><span data-stu-id="e2081-214">Observe the number of milliseconds it takes for the GPU to render a frame.</span></span>
* <span data-ttu-id="e2081-215">Arrêtez l’exécution de l’application sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="e2081-215">Stop the application from running on the device.</span></span>
* <span data-ttu-id="e2081-216">Revenez à Visual Studio et ouvrez **SpatialMappingObserver.cs**.</span><span class="sxs-lookup"><span data-stu-id="e2081-216">Return to Visual Studio and open **SpatialMappingObserver.cs**.</span></span> <span data-ttu-id="e2081-217">Vous le trouverez dans le dossier HoloToolkit\SpatialMapping du projet assembly-CSharp (universel Windows).</span><span class="sxs-lookup"><span data-stu-id="e2081-217">You will find it in the HoloToolkit\SpatialMapping folder of the Assembly-CSharp (Universal Windows) project.</span></span>
* <span data-ttu-id="e2081-218">Recherchez la fonction **éveillé ()** , puis ajoutez la ligne de code suivante : **TrianglesPerCubicMeter = 1200 ;**</span><span class="sxs-lookup"><span data-stu-id="e2081-218">Find the **Awake()** function, and add the following line of code: **TrianglesPerCubicMeter = 1200;**</span></span>
* <span data-ttu-id="e2081-219">Redéployez le projet sur votre appareil, puis **reconnectez le profileur**.</span><span class="sxs-lookup"><span data-stu-id="e2081-219">Re-deploy the project to your device, and then **reconnect the profiler**.</span></span> <span data-ttu-id="e2081-220">Observez la modification du nombre de millisecondes pour le rendu d’un frame.</span><span class="sxs-lookup"><span data-stu-id="e2081-220">Observe the change in the number of milliseconds to render a frame.</span></span>
* <span data-ttu-id="e2081-221">Arrêtez l’exécution de l’application sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="e2081-221">Stop the application from running on the device.</span></span>

<span data-ttu-id="e2081-222">**Enregistrer et charger dans Unity**</span><span class="sxs-lookup"><span data-stu-id="e2081-222">**Save and load in Unity**</span></span>

<span data-ttu-id="e2081-223">Enfin, nous allons enregistrer notre maillage d’espace et le charger dans Unity.</span><span class="sxs-lookup"><span data-stu-id="e2081-223">Finally, let's save our room mesh and load it into Unity.</span></span>

* <span data-ttu-id="e2081-224">Revenez à Visual Studio et supprimez la ligne **TrianglesPerCubicMeter** que vous avez ajoutée dans la fonction **éveillé ()** au cours de la section précédente.</span><span class="sxs-lookup"><span data-stu-id="e2081-224">Return to Visual Studio and remove the **TrianglesPerCubicMeter** line that you added in the **Awake()** function during the previous section.</span></span>
* <span data-ttu-id="e2081-225">Redéployez le projet sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="e2081-225">Redeploy the project to your device.</span></span> <span data-ttu-id="e2081-226">Nous devons maintenant être en cours d’exécution avec des triangles **500** par mètre cube.</span><span class="sxs-lookup"><span data-stu-id="e2081-226">We should now be running with **500** triangles per cubic meter.</span></span>
* <span data-ttu-id="e2081-227">Ouvrez un navigateur et entrez dans votre adresseIP HoloLens pour accéder au **portail de périphériques Windows**.</span><span class="sxs-lookup"><span data-stu-id="e2081-227">Open a browser and enter in your HoloLens IPAddress to navigate to the **Windows Device Portal**.</span></span>
* <span data-ttu-id="e2081-228">Sélectionnez l’option **vue 3D** dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="e2081-228">Select the **3D View** option in the left panel.</span></span>
* <span data-ttu-id="e2081-229">Sous **reconstruction** de la surface, sélectionnez le bouton **mettre à jour** .</span><span class="sxs-lookup"><span data-stu-id="e2081-229">Under **Surface reconstruction** select the **Update** button.</span></span>
* <span data-ttu-id="e2081-230">Regardez que les zones que vous avez analysées dans votre HoloLens s’affichent dans la fenêtre d’affichage.</span><span class="sxs-lookup"><span data-stu-id="e2081-230">Watch as the areas that you have scanned on your HoloLens appear in the display window.</span></span>
* <span data-ttu-id="e2081-231">Pour enregistrer l’analyse de votre salle, appuyez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e2081-231">To save your room scan, press the **Save** button.</span></span>
* <span data-ttu-id="e2081-232">Ouvrez votre dossier **téléchargements** pour rechercher le modèle de salle enregistré **SRMesh. obj**.</span><span class="sxs-lookup"><span data-stu-id="e2081-232">Open your **Downloads** folder to find the saved room model **SRMesh.obj**.</span></span>
* <span data-ttu-id="e2081-233">Copiez **SRMesh. obj** dans le dossier **composants** de votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="e2081-233">Copy **SRMesh.obj** to the **Assets** folder of your Unity project.</span></span>
* <span data-ttu-id="e2081-234">Dans Unity, sélectionnez l’objet **SpatialMapping** dans le panneau **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="e2081-234">In Unity, select the **SpatialMapping** object in the **Hierarchy** panel.</span></span>
* <span data-ttu-id="e2081-235">Localisez le composant **Observateur de surface d’objet (script)** .</span><span class="sxs-lookup"><span data-stu-id="e2081-235">Locate the **Object Surface Observer (Script)** component.</span></span>
* <span data-ttu-id="e2081-236">Cliquez sur le cercle situé à droite de la propriété **modèle de salle** .</span><span class="sxs-lookup"><span data-stu-id="e2081-236">Click the circle to the right of the **Room Model** property.</span></span>
* <span data-ttu-id="e2081-237">Recherchez et sélectionnez l’objet **SRMesh** , puis fermez la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e2081-237">Find and select the **SRMesh** object and then close the window.</span></span>
* <span data-ttu-id="e2081-238">Vérifiez que la propriété **modèle de salle** dans le panneau **inspecteur** a désormais la valeur **SRMesh**.</span><span class="sxs-lookup"><span data-stu-id="e2081-238">Verify that the **Room Model** property in the **Inspector** panel is now set to **SRMesh**.</span></span>
* <span data-ttu-id="e2081-239">Appuyez sur le bouton de **lecture** pour entrer en mode aperçu Unity.</span><span class="sxs-lookup"><span data-stu-id="e2081-239">Press the **Play** button to enter Unity's preview mode.</span></span>
* <span data-ttu-id="e2081-240">Le composant SpatialMapping charge les maillages à partir du modèle de salle enregistré, afin que vous puissiez les utiliser dans Unity.</span><span class="sxs-lookup"><span data-stu-id="e2081-240">The SpatialMapping component will load the meshes from the saved room model so you can use them in Unity.</span></span>
* <span data-ttu-id="e2081-241">Basculez en vue **scène** pour voir l’ensemble de votre modèle d’espace affiché avec le nuanceur filaire.</span><span class="sxs-lookup"><span data-stu-id="e2081-241">Switch to **Scene** view to see all of your room model displayed with the wireframe shader.</span></span>
* <span data-ttu-id="e2081-242">Appuyez de nouveau sur le bouton **lecture** pour quitter le mode aperçu.</span><span class="sxs-lookup"><span data-stu-id="e2081-242">Press the **Play** button again to exit preview mode.</span></span>

<span data-ttu-id="e2081-243">**Remarque :** La prochaine fois que vous passerez en mode aperçu dans Unity, le maillage Room enregistré sera chargé par défaut.</span><span class="sxs-lookup"><span data-stu-id="e2081-243">**NOTE:** The next time that you enter preview mode in Unity, it will load the saved room mesh by default.</span></span>

## <a name="chapter-2---visualization"></a><span data-ttu-id="e2081-244">Chapitre 2-visualisation</span><span class="sxs-lookup"><span data-stu-id="e2081-244">Chapter 2 - Visualization</span></span>

>[!VIDEO https://www.youtube.com/embed/RnkvXl-aXD4]

<span data-ttu-id="e2081-245">**Cherché**</span><span class="sxs-lookup"><span data-stu-id="e2081-245">**Objectives**</span></span>

* <span data-ttu-id="e2081-246">Découvrez les principes de base des nuanceurs.</span><span class="sxs-lookup"><span data-stu-id="e2081-246">Learn the basics of shaders.</span></span>
* <span data-ttu-id="e2081-247">Visualisez votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e2081-247">Visualize your surroundings.</span></span>

<span data-ttu-id="e2081-248">**Ample**</span><span class="sxs-lookup"><span data-stu-id="e2081-248">**Instructions**</span></span>

* <span data-ttu-id="e2081-249">Dans le panneau de la **hiérarchie** Unity, sélectionnez l’objet **SpatialMapping** .</span><span class="sxs-lookup"><span data-stu-id="e2081-249">In Unity's **Hierarchy** panel, select the **SpatialMapping** object.</span></span>
* <span data-ttu-id="e2081-250">Dans le volet de l' **inspecteur** , recherchez le composant de **Gestionnaire de mappage spatial (script)** .</span><span class="sxs-lookup"><span data-stu-id="e2081-250">In the **Inspector** panel, find the **Spatial Mapping Manager (Script)** component.</span></span>
* <span data-ttu-id="e2081-251">Cliquez sur le cercle situé à droite de la propriété **surface** .</span><span class="sxs-lookup"><span data-stu-id="e2081-251">Click the circle to the right of the **Surface Material** property.</span></span>
* <span data-ttu-id="e2081-252">Recherchez et sélectionnez le matériel **BlueLinesOnWalls** et fermez la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e2081-252">Find and select the **BlueLinesOnWalls** material and close the window.</span></span>
* <span data-ttu-id="e2081-253">Dans le dossier **nuanciers** du panneau **projet** , double-cliquez sur **BlueLinesOnWalls** pour ouvrir le nuanceur dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2081-253">In the **Project** panel **Shaders** folder, double-click on **BlueLinesOnWalls** to open the shader in Visual Studio.</span></span>
* <span data-ttu-id="e2081-254">Il s’agit d’un nuanceur de pixels (vertex à fragment) simple qui effectue les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="e2081-254">This is a simple pixel (vertex to fragment) shader, which accomplishes the following tasks:</span></span>
    1. <span data-ttu-id="e2081-255">Convertit l’emplacement d’un vertex en espace universel.</span><span class="sxs-lookup"><span data-stu-id="e2081-255">Converts a vertex's location to world space.</span></span>
    2. <span data-ttu-id="e2081-256">Vérifie la normale du vertex pour déterminer si un pixel est vertical.</span><span class="sxs-lookup"><span data-stu-id="e2081-256">Checks the vertex's normal to determine if a pixel is vertical.</span></span>
    3. <span data-ttu-id="e2081-257">Définit la couleur du pixel pour le rendu.</span><span class="sxs-lookup"><span data-stu-id="e2081-257">Sets the color of the pixel for rendering.</span></span>

<span data-ttu-id="e2081-258">**Génération et déploiement**</span><span class="sxs-lookup"><span data-stu-id="e2081-258">**Build and Deploy**</span></span>

* <span data-ttu-id="e2081-259">Revenez à Unity et appuyez sur **Play** pour passer en mode aperçu.</span><span class="sxs-lookup"><span data-stu-id="e2081-259">Return to Unity and press **Play** to enter preview mode.</span></span>
* <span data-ttu-id="e2081-260">Les lignes bleues sont affichées sur toutes les surfaces verticales de la maille de la salle (qui sont chargées automatiquement à partir de nos données d’analyse enregistrées).</span><span class="sxs-lookup"><span data-stu-id="e2081-260">Blue lines will be rendered on all vertical surfaces of the room mesh (which automatically loaded from our saved scanning data).</span></span>
* <span data-ttu-id="e2081-261">Basculez vers l’onglet **scène** pour ajuster la vue de la pièce et voir comment l’intégralité du maillage de la salle apparaît dans Unity.</span><span class="sxs-lookup"><span data-stu-id="e2081-261">Switch to the **Scene** tab to adjust your view of the room and see how the entire room mesh appears in Unity.</span></span>
* <span data-ttu-id="e2081-262">Dans le panneau **projet** , recherchez le dossier **matériaux** et sélectionnez le matériel **BlueLinesOnWalls** .</span><span class="sxs-lookup"><span data-stu-id="e2081-262">In the **Project** panel, find the **Materials** folder and select the **BlueLinesOnWalls** material.</span></span>
* <span data-ttu-id="e2081-263">Modifiez certaines propriétés et observez le mode d’affichage des modifications dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="e2081-263">Modify some properties and see how the changes appear in the Unity editor.</span></span>
    * <span data-ttu-id="e2081-264">Dans le panneau **inspecteur** , ajustez la valeur **LineScale** pour que les lignes apparaissent plus épaisses ou plus fines.</span><span class="sxs-lookup"><span data-stu-id="e2081-264">In the **Inspector** panel, adjust the **LineScale** value to make the lines appear thicker or thinner.</span></span>
    * <span data-ttu-id="e2081-265">Dans le panneau **inspecteur** , ajustez la valeur **LinesPerMeter** pour modifier le nombre de lignes qui s’affichent sur chaque mur.</span><span class="sxs-lookup"><span data-stu-id="e2081-265">In the **Inspector** panel, adjust the **LinesPerMeter** value to change how many lines appear on each wall.</span></span>
* <span data-ttu-id="e2081-266">Cliquez à nouveau sur **lire** pour quitter le mode aperçu.</span><span class="sxs-lookup"><span data-stu-id="e2081-266">Click **Play** again to exit preview mode.</span></span>
* <span data-ttu-id="e2081-267">Générez et déployez sur HoloLens et observez la façon dont le rendu du nuanceur apparaît sur les surfaces réelles.</span><span class="sxs-lookup"><span data-stu-id="e2081-267">Build and deploy to the HoloLens and observe how the shader rendering appears on real surfaces.</span></span>

<span data-ttu-id="e2081-268">Unity fait un excellent travail d’aperçu des documents, mais il est toujours judicieux d’extraire le rendu dans l’appareil.</span><span class="sxs-lookup"><span data-stu-id="e2081-268">Unity does a great job of previewing materials, but it's always a good idea to check-out rendering in the device.</span></span>

## <a name="chapter-3---processing"></a><span data-ttu-id="e2081-269">Chapitre 3-traitement</span><span class="sxs-lookup"><span data-stu-id="e2081-269">Chapter 3 - Processing</span></span>

>[!VIDEO https://www.youtube.com/embed/kaUKiNiDxwY]

<span data-ttu-id="e2081-270">**Cherché**</span><span class="sxs-lookup"><span data-stu-id="e2081-270">**Objectives**</span></span>

* <span data-ttu-id="e2081-271">Découvrez les techniques permettant de traiter les données de mappage spatiale pour une utilisation dans votre application.</span><span class="sxs-lookup"><span data-stu-id="e2081-271">Learn techniques to process spatial mapping data for use in your application.</span></span>
* <span data-ttu-id="e2081-272">Analyser les données de mappage spatiale pour rechercher des plans et supprimer des triangles.</span><span class="sxs-lookup"><span data-stu-id="e2081-272">Analyze spatial mapping data to find planes and remove triangles.</span></span>
* <span data-ttu-id="e2081-273">Utilisez des plans pour le placement de l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="e2081-273">Use planes for hologram placement.</span></span>

<span data-ttu-id="e2081-274">**Ample**</span><span class="sxs-lookup"><span data-stu-id="e2081-274">**Instructions**</span></span>

* <span data-ttu-id="e2081-275">Dans le panneau **projet** d’Unity, dans le dossier **hologrammes** , recherchez l’objet **SpatialProcessing** .</span><span class="sxs-lookup"><span data-stu-id="e2081-275">In Unity's **Project** panel, **Holograms** folder, find the **SpatialProcessing** object.</span></span>
* <span data-ttu-id="e2081-276">Faites glisser & déposez l’objet **SpatialProcessing** dans le panneau de **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="e2081-276">Drag & drop the **SpatialProcessing** object into the **Hierarchy** panel.</span></span>

<span data-ttu-id="e2081-277">SpatialProcessing Prefab comprend des composants pour traiter les données de mappage spatiale.</span><span class="sxs-lookup"><span data-stu-id="e2081-277">The SpatialProcessing prefab includes components for processing the spatial mapping data.</span></span> <span data-ttu-id="e2081-278">**SurfaceMeshesToPlanes.cs** trouvera et générera des plans basés sur les données de mappage spatiale.</span><span class="sxs-lookup"><span data-stu-id="e2081-278">**SurfaceMeshesToPlanes.cs** will find and generate planes based on the spatial mapping data.</span></span> <span data-ttu-id="e2081-279">Nous utiliserons des plans dans notre application pour représenter les murs, les étages et les plafonds.</span><span class="sxs-lookup"><span data-stu-id="e2081-279">We will use planes in our application to represent walls, floors and ceilings.</span></span> <span data-ttu-id="e2081-280">Ce Prefab comprend également **RemoveSurfaceVertices.cs** qui peut supprimer des vertex du maillage de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="e2081-280">This prefab also includes **RemoveSurfaceVertices.cs** which can remove vertices from the spatial mapping mesh.</span></span> <span data-ttu-id="e2081-281">Cela peut être utilisé pour créer des trous dans la maille ou pour supprimer les triangles excédentaires qui ne sont plus nécessaires (car les plans peuvent être utilisés à la place).</span><span class="sxs-lookup"><span data-stu-id="e2081-281">This can be used to create holes in the mesh, or to remove excess triangles that are no longer needed (because planes can be used instead).</span></span>

* <span data-ttu-id="e2081-282">Dans le panneau **projet** d’Unity, dans le dossier **hologrammes** , recherchez l’objet **SpaceCollection** .</span><span class="sxs-lookup"><span data-stu-id="e2081-282">In Unity's **Project** panel, **Holograms** folder, find the **SpaceCollection** object.</span></span>
* <span data-ttu-id="e2081-283">Faites glisser et déposez l’objet **SpaceCollection** dans le panneau de **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="e2081-283">Drag and drop the **SpaceCollection** object into the **Hierarchy** panel.</span></span>
* <span data-ttu-id="e2081-284">Dans le volet **hiérarchie** , sélectionnez l’objet **SpatialProcessing** .</span><span class="sxs-lookup"><span data-stu-id="e2081-284">In the **Hierarchy** panel, select the **SpatialProcessing** object.</span></span>
* <span data-ttu-id="e2081-285">Dans le volet de l' **inspecteur** , recherchez le composant **Gestionnaire d’espace de lecture (script)** .</span><span class="sxs-lookup"><span data-stu-id="e2081-285">In the **Inspector** panel, find the **Play Space Manager (Script)** component.</span></span>
* <span data-ttu-id="e2081-286">Double-cliquez sur **PlaySpaceManager.cs** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2081-286">Double-click on **PlaySpaceManager.cs** to open it in Visual Studio.</span></span>

<span data-ttu-id="e2081-287">PlaySpaceManager.cs contient le code spécifique à l’application.</span><span class="sxs-lookup"><span data-stu-id="e2081-287">PlaySpaceManager.cs contains application-specific code.</span></span> <span data-ttu-id="e2081-288">Nous ajouterons des fonctionnalités à ce script pour activer le comportement suivant :</span><span class="sxs-lookup"><span data-stu-id="e2081-288">We will add functionality to this script to enable the following behavior:</span></span>

1. <span data-ttu-id="e2081-289">Arrêtez la collecte des données de mappage spatiale après avoir dépassé la limite de temps d’analyse (10 secondes).</span><span class="sxs-lookup"><span data-stu-id="e2081-289">Stop collecting spatial mapping data after we exceed the scanning time limit (10 seconds).</span></span>
2. <span data-ttu-id="e2081-290">Traiter les données de mappage spatiale :</span><span class="sxs-lookup"><span data-stu-id="e2081-290">Process the spatial mapping data:</span></span>
    1. <span data-ttu-id="e2081-291">Utilisez SurfaceMeshesToPlanes pour créer une représentation plus simple du monde comme plans (murs, étages, plafonds, etc.).</span><span class="sxs-lookup"><span data-stu-id="e2081-291">Use SurfaceMeshesToPlanes to create a simpler representation of the world as planes (walls, floors, ceilings, etc).</span></span>
    2. <span data-ttu-id="e2081-292">Utilisez RemoveSurfaceVertices pour supprimer les triangles de surface qui se trouvent dans les limites du plan.</span><span class="sxs-lookup"><span data-stu-id="e2081-292">Use RemoveSurfaceVertices to remove surface triangles that fall within plane boundaries.</span></span>
3. <span data-ttu-id="e2081-293">Générez un ensemble d’hologrammes dans le monde et placez-les sur des plans muraux et de plancher près de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e2081-293">Generate a collection of holograms in the world and place them on wall and floor planes near the user.</span></span>

<span data-ttu-id="e2081-294">Effectuez les exercices de codage marqués dans PlaySpaceManager.cs ou remplacez le script par la solution terminée ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="e2081-294">Complete the coding exercises marked in PlaySpaceManager.cs, or replace the script with the finished solution from below:</span></span>

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

<span data-ttu-id="e2081-295">**Génération et déploiement**</span><span class="sxs-lookup"><span data-stu-id="e2081-295">**Build and Deploy**</span></span>

* <span data-ttu-id="e2081-296">Avant de déployer sur HoloLens, appuyez sur le bouton de **lecture** dans Unity pour passer en mode lecture.</span><span class="sxs-lookup"><span data-stu-id="e2081-296">Before deploying to the HoloLens, press the **Play** button in Unity to enter play mode.</span></span>
* <span data-ttu-id="e2081-297">Une fois le maillage de la salle chargé à partir du fichier, attendez 10 secondes avant le début du traitement sur le maillage de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="e2081-297">After the room mesh is loaded from file, wait for 10 seconds before processing starts on the spatial mapping mesh.</span></span>
* <span data-ttu-id="e2081-298">Une fois le traitement terminé, les plans s’affichent pour représenter le plancher, les murs, le plafond, etc.</span><span class="sxs-lookup"><span data-stu-id="e2081-298">When processing is complete, planes will appear to represent the floor, walls, ceiling, etc.</span></span>
* <span data-ttu-id="e2081-299">Une fois tous les plans détectés, un système solaire doit s’afficher sur une table de plancher près de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="e2081-299">After all of the planes have been found, you should see a solar system appear on a table of floor near the camera.</span></span>
* <span data-ttu-id="e2081-300">Deux affiches doivent également apparaître sur les murs près de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="e2081-300">Two posters should appear on walls near the camera too.</span></span> <span data-ttu-id="e2081-301">Basculez vers l’onglet **scène** si vous ne les voyez pas en mode **jeu** .</span><span class="sxs-lookup"><span data-stu-id="e2081-301">Switch to the **Scene** tab if you cannot see them in **Game** mode.</span></span>
* <span data-ttu-id="e2081-302">Appuyez de nouveau sur le bouton de **lecture** pour quitter le mode lecture.</span><span class="sxs-lookup"><span data-stu-id="e2081-302">Press the **Play** button again to exit play mode.</span></span>
* <span data-ttu-id="e2081-303">Générez et déployez sur HoloLens, comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="e2081-303">Build and deploy to the HoloLens, as usual.</span></span>
* <span data-ttu-id="e2081-304">Attendez la fin de l’analyse et du traitement des données de mappage spatiale.</span><span class="sxs-lookup"><span data-stu-id="e2081-304">Wait for scanning and processing of the spatial mapping data to complete.</span></span>
* <span data-ttu-id="e2081-305">Une fois que vous voyez des plans, essayez de trouver le système solaire et les affiches dans votre monde.</span><span class="sxs-lookup"><span data-stu-id="e2081-305">Once you see planes, try to find the solar system and posters in your world.</span></span>

## <a name="chapter-4---placement"></a><span data-ttu-id="e2081-306">Chapitre 4-placement</span><span class="sxs-lookup"><span data-stu-id="e2081-306">Chapter 4 - Placement</span></span>

>[!VIDEO https://www.youtube.com/embed/Srhtpid1uZc]

<span data-ttu-id="e2081-307">**Cherché**</span><span class="sxs-lookup"><span data-stu-id="e2081-307">**Objectives**</span></span>

* <span data-ttu-id="e2081-308">Déterminer si un hologramme peut tenir sur une surface.</span><span class="sxs-lookup"><span data-stu-id="e2081-308">Determine if a hologram will fit on a surface.</span></span>
* <span data-ttu-id="e2081-309">Fournir des commentaires à l’utilisateur lorsqu’un hologramme ne peut pas être ajusté sur une surface.</span><span class="sxs-lookup"><span data-stu-id="e2081-309">Provide feedback to the user when a hologram can/cannot fit on a surface.</span></span>

<span data-ttu-id="e2081-310">**Ample**</span><span class="sxs-lookup"><span data-stu-id="e2081-310">**Instructions**</span></span>

* <span data-ttu-id="e2081-311">Dans le panneau de la **hiérarchie** Unity, sélectionnez l’objet **SpatialProcessing** .</span><span class="sxs-lookup"><span data-stu-id="e2081-311">In Unity's **Hierarchy** panel, select the **SpatialProcessing** object.</span></span>
* <span data-ttu-id="e2081-312">Dans le volet de l' **inspecteur** , recherchez les **maillages des surfaces du composant plans (script)** .</span><span class="sxs-lookup"><span data-stu-id="e2081-312">In the **Inspector** panel, find the **Surface Meshes To Planes (Script)** component.</span></span>
* <span data-ttu-id="e2081-313">Remplacez la valeur de la propriété **dessiner des plans** par **Nothing** pour effacer la sélection.</span><span class="sxs-lookup"><span data-stu-id="e2081-313">Change the **Draw Planes** property to **Nothing** to clear the selection.</span></span>
* <span data-ttu-id="e2081-314">Remplacez la propriété **dessiner des plans** par **Wall**, afin que seuls les plans muraux soient rendus.</span><span class="sxs-lookup"><span data-stu-id="e2081-314">Change the **Draw Planes** property to **Wall**, so that only wall planes will be rendered.</span></span>
* <span data-ttu-id="e2081-315">Dans le panneau **projet** , cliquez sur le dossier **scripts** , double-cliquez sur **Placeable.cs** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2081-315">In the **Project** panel, **Scripts** folder, double-click on **Placeable.cs** to open it in Visual Studio.</span></span>

<span data-ttu-id="e2081-316">Le script **positionnable** est déjà associé aux affiches et à la boîte de projection créées après la recherche du plan.</span><span class="sxs-lookup"><span data-stu-id="e2081-316">The **Placeable** script is already attached to the posters and projection box that are created after plane finding completes.</span></span> <span data-ttu-id="e2081-317">Tout ce que nous devons faire, c’est supprimer les marques de commentaire de code, et ce script va obtenir ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="e2081-317">All we need to do is uncomment some code, and this script will achieve the following:</span></span>

1. <span data-ttu-id="e2081-318">Déterminez si un hologramme est ajusté sur une surface par Raycasting à partir du centre et quatre coins du cube englobant.</span><span class="sxs-lookup"><span data-stu-id="e2081-318">Determine if a hologram will fit on a surface by raycasting from the center and four corners of the bounding cube.</span></span>
2. <span data-ttu-id="e2081-319">Vérifiez la normale de la surface pour déterminer si elle est suffisamment lisse pour que l’hologramme se vide.</span><span class="sxs-lookup"><span data-stu-id="e2081-319">Check the surface normal to determine if it is smooth enough for the hologram to sit flush on.</span></span>
3. <span data-ttu-id="e2081-320">Restituez un cube englobant autour de l’hologramme pour afficher sa taille réelle lors de son placement.</span><span class="sxs-lookup"><span data-stu-id="e2081-320">Render a bounding cube around the hologram to show its actual size while being placed.</span></span>
4. <span data-ttu-id="e2081-321">Convertit une ombre sous/derrière l’hologramme pour montrer où il sera placé sur le plancher/le mur.</span><span class="sxs-lookup"><span data-stu-id="e2081-321">Cast a shadow under/behind the hologram to show where it will be placed on the floor/wall.</span></span>
5. <span data-ttu-id="e2081-322">Restitue l’ombre en rouge, si l’hologramme ne peut pas être placé sur l’aire, ou vert, si possible.</span><span class="sxs-lookup"><span data-stu-id="e2081-322">Render the shadow as red, if the hologram cannot be placed on the surface, or green, if it can.</span></span>
6. <span data-ttu-id="e2081-323">Réorienter l’hologramme pour qu’il s’aligne avec le type de surface (vertical ou horizontal) auquel il a une affinité.</span><span class="sxs-lookup"><span data-stu-id="e2081-323">Re-orient the hologram to align with the surface type (vertical or horizontal) that it has affinity to.</span></span>
7. <span data-ttu-id="e2081-324">Placez en douceur l’hologramme sur la surface sélectionnée pour éviter le comportement de saut ou d’alignement.</span><span class="sxs-lookup"><span data-stu-id="e2081-324">Smoothly place the hologram on the selected surface to avoid jumping or snapping behavior.</span></span>

<span data-ttu-id="e2081-325">Supprimez les marques de commentaire de tout le code dans l’exercice de codage ci-dessous, ou utilisez cette solution terminée dans **Placeable.cs**:</span><span class="sxs-lookup"><span data-stu-id="e2081-325">Uncomment all code in the coding exercise below, or use this completed solution in **Placeable.cs**:</span></span>

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
    /// The alignToVerticalSurface parameter is ignored if the object
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

<span data-ttu-id="e2081-326">**Génération et déploiement**</span><span class="sxs-lookup"><span data-stu-id="e2081-326">**Build and Deploy**</span></span>

* <span data-ttu-id="e2081-327">Comme précédemment, générez le projet et déployez sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="e2081-327">As before, build the project and deploy to the HoloLens.</span></span>
* <span data-ttu-id="e2081-328">Attendez la fin de l’analyse et du traitement des données de mappage spatiale.</span><span class="sxs-lookup"><span data-stu-id="e2081-328">Wait for scanning and processing of the spatial mapping data to complete.</span></span>
* <span data-ttu-id="e2081-329">Lorsque vous voyez le système solaire, pointez le curseur en regard de la zone de projection ci-dessous et effectuez un mouvement de sélection pour le déplacer.</span><span class="sxs-lookup"><span data-stu-id="e2081-329">When you see the solar system, gaze at the projection box below and perform a select gesture to move it around.</span></span> <span data-ttu-id="e2081-330">Lorsque la zone de projection est sélectionnée, un cube englobant est visible autour de la zone de projection.</span><span class="sxs-lookup"><span data-stu-id="e2081-330">While the projection box is selected, a bounding cube will be visible around the projection box.</span></span>
* <span data-ttu-id="e2081-331">Déplacez-vous vers le regard d’un autre endroit de la pièce.</span><span class="sxs-lookup"><span data-stu-id="e2081-331">Move you head to gaze at a different location in the room.</span></span> <span data-ttu-id="e2081-332">La zone de projection doit suivre votre point de regard.</span><span class="sxs-lookup"><span data-stu-id="e2081-332">The projection box should follow your gaze.</span></span> <span data-ttu-id="e2081-333">Lorsque l’ombre sous la zone de projection devient rouge, vous ne pouvez pas placer l’hologramme sur cette surface.</span><span class="sxs-lookup"><span data-stu-id="e2081-333">When the shadow below the projection box turns red, you cannot place the hologram on that surface.</span></span> <span data-ttu-id="e2081-334">Lorsque l’ombre sous la zone de projection devient verte, vous pouvez placer l’hologramme en effectuant un autre mouvement Select.</span><span class="sxs-lookup"><span data-stu-id="e2081-334">When the shadow below the projection box turns green, you can place the hologram by performing another select gesture.</span></span>
* <span data-ttu-id="e2081-335">Recherchez et sélectionnez l’une des affiches holographiques sur un mur pour la déplacer vers un nouvel emplacement.</span><span class="sxs-lookup"><span data-stu-id="e2081-335">Find and select one of the holographic posters on a wall to move it to a new location.</span></span> <span data-ttu-id="e2081-336">Notez que vous ne pouvez pas placer l’affiche à l’étage ou au plafond, et qu’il reste correctement orienté vers chaque mur au fur et à mesure que vous vous déplacez.</span><span class="sxs-lookup"><span data-stu-id="e2081-336">Notice that you cannot place the poster on the floor or ceiling, and that it stays correctly oriented to each wall as you move around.</span></span>

## <a name="chapter-5---occlusion"></a><span data-ttu-id="e2081-337">Chapitre 5-occlusion</span><span class="sxs-lookup"><span data-stu-id="e2081-337">Chapter 5 - Occlusion</span></span>

>[!VIDEO https://www.youtube.com/embed/6Xrzh_w-7SE]

<span data-ttu-id="e2081-338">**Cherché**</span><span class="sxs-lookup"><span data-stu-id="e2081-338">**Objectives**</span></span>

* <span data-ttu-id="e2081-339">Détermine si un hologramme est bloqués par le maillage de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="e2081-339">Determine if a hologram is occluded by the spatial mapping mesh.</span></span>
* <span data-ttu-id="e2081-340">Appliquez différentes techniques d’occlusion pour obtenir un effet amusant.</span><span class="sxs-lookup"><span data-stu-id="e2081-340">Apply different occlusion techniques to achieve a fun effect.</span></span>

<span data-ttu-id="e2081-341">**Ample**</span><span class="sxs-lookup"><span data-stu-id="e2081-341">**Instructions**</span></span>

<span data-ttu-id="e2081-342">Tout d’abord, nous allons autoriser le maillage de mappage spatial à occultait d’autres hologrammes sans Boucher le monde réel :</span><span class="sxs-lookup"><span data-stu-id="e2081-342">First, we are going to allow the spatial mapping mesh to occlude other holograms without occluding the real world:</span></span>

* <span data-ttu-id="e2081-343">Dans le volet **hiérarchie** , sélectionnez l’objet **SpatialProcessing** .</span><span class="sxs-lookup"><span data-stu-id="e2081-343">In the **Hierarchy** panel, select the **SpatialProcessing** object.</span></span>
* <span data-ttu-id="e2081-344">Dans le volet de l' **inspecteur** , recherchez le composant **Gestionnaire d’espace de lecture (script)** .</span><span class="sxs-lookup"><span data-stu-id="e2081-344">In the **Inspector** panel, find the **Play Space Manager (Script)** component.</span></span>
* <span data-ttu-id="e2081-345">Cliquez sur le cercle situé à droite de la propriété **matériau secondaire** .</span><span class="sxs-lookup"><span data-stu-id="e2081-345">Click the circle to the right of the **Secondary Material** property.</span></span>
* <span data-ttu-id="e2081-346">Recherchez et sélectionnez le matériel d' **occlusion** , puis fermez la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e2081-346">Find and select the **Occlusion** material and close the window.</span></span>

<span data-ttu-id="e2081-347">Nous allons ensuite ajouter un comportement spécial à la terre, afin qu’elle soit en surbrillance en bleu chaque fois qu’elle est bloqués par un autre hologramme (comme le soleil) ou par le maillage de mappage spatial :</span><span class="sxs-lookup"><span data-stu-id="e2081-347">Next, we are going to add a special behavior to Earth, so that it has a blue highlight whenever it becomes occluded by another hologram (like the sun), or by the spatial mapping mesh:</span></span>

* <span data-ttu-id="e2081-348">Dans le panneau **projet** , dans le dossier **hologrammes** , développez l’objet **SolarSystem** .</span><span class="sxs-lookup"><span data-stu-id="e2081-348">In the **Project** panel, in the **Holograms** folder, expand the **SolarSystem** object.</span></span>
* <span data-ttu-id="e2081-349">Cliquez sur **terre**.</span><span class="sxs-lookup"><span data-stu-id="e2081-349">Click on **Earth**.</span></span>
* <span data-ttu-id="e2081-350">Dans le panneau **inspecteur** , recherchez le matériau de la terre (composant le plus bas).</span><span class="sxs-lookup"><span data-stu-id="e2081-350">In the **Inspector** panel, find the Earth's material (bottom component).</span></span>
* <span data-ttu-id="e2081-351">Dans la **liste déroulante nuanceur**, remplacez le nuanceur par **personnalisé > OcclusionRim**.</span><span class="sxs-lookup"><span data-stu-id="e2081-351">In the **Shader drop-down**, change the shader to **Custom > OcclusionRim**.</span></span> <span data-ttu-id="e2081-352">Cela permet d’afficher une surbrillance bleue autour de la terre chaque fois qu’elle est bloqués par un autre objet.</span><span class="sxs-lookup"><span data-stu-id="e2081-352">This will render a blue highlight around Earth whenever it is occluded by another object.</span></span>

<span data-ttu-id="e2081-353">Enfin, nous allons activer un effet de vision x-ray pour les planètes dans notre système solaire.</span><span class="sxs-lookup"><span data-stu-id="e2081-353">Finally, we are going to enable an x-ray vision effect for planets in our solar system.</span></span> <span data-ttu-id="e2081-354">Nous devons modifier **PlanetOcclusion.cs** (qui se trouve dans le dossier Scripts\SolarSystem) afin d’obtenir les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e2081-354">We will need to edit **PlanetOcclusion.cs** (found in the Scripts\SolarSystem folder) in order to achieve the following:</span></span>

1. <span data-ttu-id="e2081-355">Déterminez si une planète est bloqués par la couche SpatialMapping (maillages et plans d’espace).</span><span class="sxs-lookup"><span data-stu-id="e2081-355">Determine if a planet is occluded by the SpatialMapping layer (room meshes and planes).</span></span>
2. <span data-ttu-id="e2081-356">Affichez la représentation filaire d’une planète chaque fois qu’elle est bloqués par la couche SpatialMapping.</span><span class="sxs-lookup"><span data-stu-id="e2081-356">Show the wireframe representation of a planet whenever it is occluded by the SpatialMapping layer.</span></span>
3. <span data-ttu-id="e2081-357">Masquer la représentation filaire d’une planète lorsqu’elle n’est pas bloquée par la couche SpatialMapping.</span><span class="sxs-lookup"><span data-stu-id="e2081-357">Hide the wireframe representation of a planet when it is not blocked by the SpatialMapping layer.</span></span>

<span data-ttu-id="e2081-358">Suivez l’exercice de codage dans PlanetOcclusion.cs ou utilisez la solution suivante :</span><span class="sxs-lookup"><span data-stu-id="e2081-358">Follow the coding exercise in PlanetOcclusion.cs, or use the following solution:</span></span>

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

<span data-ttu-id="e2081-359">**Génération et déploiement**</span><span class="sxs-lookup"><span data-stu-id="e2081-359">**Build and Deploy**</span></span>

* <span data-ttu-id="e2081-360">Générez et déployez l’application dans HoloLens, comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="e2081-360">Build and deploy the application to HoloLens, as usual.</span></span>
* <span data-ttu-id="e2081-361">Attendez la fin de l’analyse et du traitement des données de mappage spatiale (vous devriez voir apparaître des lignes bleues sur les murs).</span><span class="sxs-lookup"><span data-stu-id="e2081-361">Wait for scanning and processing of the spatial mapping data to be complete (you should see blue lines appear on walls).</span></span>
* <span data-ttu-id="e2081-362">Recherchez et sélectionnez la zone de projection du système solaire, puis activez la case à cocher en regard d’un mur ou derrière un compteur.</span><span class="sxs-lookup"><span data-stu-id="e2081-362">Find and select the solar system's projection box and then set the box next to a wall or behind a counter.</span></span>
* <span data-ttu-id="e2081-363">Vous pouvez afficher l’occlusion de base en masquant derrière les surfaces à l’homologue dans la zone d’affiche ou de projection.</span><span class="sxs-lookup"><span data-stu-id="e2081-363">You can view basic occlusion by hiding behind surfaces to peer at the poster or projection box.</span></span>
* <span data-ttu-id="e2081-364">Si vous recherchez la terre, il doit y avoir un effet de surbrillance bleu lorsqu’il se trouve derrière un autre hologramme ou une autre surface.</span><span class="sxs-lookup"><span data-stu-id="e2081-364">Look for the Earth, there should be a blue highlight effect whenever it goes behind another hologram or surface.</span></span>
* <span data-ttu-id="e2081-365">Regardez que les planètes se déplacent derrière le mur ou d’autres surfaces de la pièce.</span><span class="sxs-lookup"><span data-stu-id="e2081-365">Watch as the planets move behind the wall or other surfaces in the room.</span></span> <span data-ttu-id="e2081-366">Vous avez maintenant une vision x-ray et vous pouvez voir leurs squelettes filaires !</span><span class="sxs-lookup"><span data-stu-id="e2081-366">You now have x-ray vision and can see their wireframe skeletons!</span></span>

## <a name="the-end"></a><span data-ttu-id="e2081-367">La fin</span><span class="sxs-lookup"><span data-stu-id="e2081-367">The End</span></span>

<span data-ttu-id="e2081-368">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="e2081-368">Congratulations!</span></span> <span data-ttu-id="e2081-369">Vous avez maintenant terminé le **mappage spatial 230 : spatial**.</span><span class="sxs-lookup"><span data-stu-id="e2081-369">You have now completed **MR Spatial 230: Spatial mapping**.</span></span>

* <span data-ttu-id="e2081-370">Vous savez comment analyser votre environnement et charger des données de mappage spatiale sur Unity.</span><span class="sxs-lookup"><span data-stu-id="e2081-370">You know how to scan your environment and load spatial mapping data to Unity.</span></span>
* <span data-ttu-id="e2081-371">Vous comprenez les notions de base des nuanceurs et comment les documents peuvent être utilisés pour revisualiser le monde.</span><span class="sxs-lookup"><span data-stu-id="e2081-371">You understand the basics of shaders and how materials can be used to re-visualize the world.</span></span>
* <span data-ttu-id="e2081-372">Vous avez appris les nouvelles techniques de traitement permettant de trouver des plans et de supprimer des triangles d’une maille.</span><span class="sxs-lookup"><span data-stu-id="e2081-372">You learned of new processing techniques for finding planes and removing triangles from a mesh.</span></span>
* <span data-ttu-id="e2081-373">Vous avez pu déplacer et placer des hologrammes sur des surfaces qui ont été rendues logiques.</span><span class="sxs-lookup"><span data-stu-id="e2081-373">You were able to move and place holograms on surfaces that made sense.</span></span>
* <span data-ttu-id="e2081-374">Vous avez connu différentes techniques d’occlusion et vous avez utilisé la puissance de la vision x-ray !</span><span class="sxs-lookup"><span data-stu-id="e2081-374">You experienced different occlusion techniques and harnessed the power of x-ray vision!</span></span>
