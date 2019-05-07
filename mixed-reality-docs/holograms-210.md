---
title: Entrée M. 210 - regards
description: Suivez cette procédure pas à pas à l’aide de Unity, Visual Studio et HoloLens pour connaître les détails des regards concepts de codage.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, academy, tutorial, gaze
ms.openlocfilehash: 076314389ec5ed70347c26d50c6a993f55da0758
ms.sourcegitcommit: aa88f6b42aa8d83e43104b78964afb506a368fb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/02/2019
ms.locfileid: "64993545"
---
>[!NOTE]
><span data-ttu-id="d3a92-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="d3a92-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="d3a92-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="d3a92-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="d3a92-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="d3a92-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="d3a92-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d3a92-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="d3a92-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="d3a92-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="d3a92-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="d3a92-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

# <a name="mr-input-210-gaze"></a><span data-ttu-id="d3a92-110">Entrée M. 210 : Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="d3a92-110">MR Input 210: Gaze</span></span>

<span data-ttu-id="d3a92-111">[Utilisation](gaze.md) est la première forme d’entrée et révèle intention et la reconnaissance de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d3a92-111">[Gaze](gaze.md) is the first form of input and reveals the user's intent and awareness.</span></span> <span data-ttu-id="d3a92-112">MR entrée 210 (également appelé Explorateur de projets) est une connaissance approfondie des concepts liés à regards pour la réalité mixte de Windows.</span><span class="sxs-lookup"><span data-stu-id="d3a92-112">MR Input 210 (aka Project Explorer) is a deep dive into gaze-related concepts for Windows Mixed Reality.</span></span> <span data-ttu-id="d3a92-113">Nous ajouterons une reconnaissance contextuelle et notre curseur hologrammes, tirant pleinement parti de ce que votre application connaît des regards de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d3a92-113">We will be adding contextual awareness to our cursor and holograms, taking full advantage of what your app knows about the user's gaze.</span></span>

>[!VIDEO https://www.youtube.com/embed/yKAttGduVp0]

<span data-ttu-id="d3a92-114">Nous avons un astronaut convivial ici pour vous aider à apprendre les concepts du pointage de regard.</span><span class="sxs-lookup"><span data-stu-id="d3a92-114">We have a friendly astronaut here to help you learn gaze concepts.</span></span> <span data-ttu-id="d3a92-115">Dans [101 des principes fondamentaux de M.](holograms-101.md), nous avions un curseur simple qui suivi simplement votre regard.</span><span class="sxs-lookup"><span data-stu-id="d3a92-115">In [MR Basics 101](holograms-101.md), we had a simple cursor that just followed your gaze.</span></span> <span data-ttu-id="d3a92-116">Aujourd'hui, nous voit passer une étape au-delà du simple curseur :</span><span class="sxs-lookup"><span data-stu-id="d3a92-116">Today we're moving a step beyond the simple cursor:</span></span>

* <span data-ttu-id="d3a92-117">Nous simplifions le curseur et nos hologrammes prenant en charge les regards : les deux changent en fonction où l’utilisateur recherche - ou où l’utilisateur est *pas* recherche.</span><span class="sxs-lookup"><span data-stu-id="d3a92-117">We're making the cursor and our holograms gaze-aware: both will change based on where the user is looking - or where the user is *not* looking.</span></span> <span data-ttu-id="d3a92-118">Cela les rend sensible au contexte.</span><span class="sxs-lookup"><span data-stu-id="d3a92-118">This makes them context-aware.</span></span>
* <span data-ttu-id="d3a92-119">Nous allons ajouter des commentaires et notre curseur hologrammes pour donner à l’utilisateur plus de contexte sur ce qui est ciblé.</span><span class="sxs-lookup"><span data-stu-id="d3a92-119">We will add feedback to our cursor and holograms to give the user more context on what is being targeted.</span></span> <span data-ttu-id="d3a92-120">Ces commentaires peuvent être audio et visuels.</span><span class="sxs-lookup"><span data-stu-id="d3a92-120">This feedback can be audio and visual.</span></span>
* <span data-ttu-id="d3a92-121">Nous allons vous montrer des techniques de ciblage pour aider les utilisateurs à atteindre des objectifs plus petits.</span><span class="sxs-lookup"><span data-stu-id="d3a92-121">We'll show you targeting techniques to help users hit smaller targets.</span></span>
* <span data-ttu-id="d3a92-122">Nous allons vous montrer comment attirer l’attention de l’utilisateur sur votre hologrammes avec un indicateur d’orientation.</span><span class="sxs-lookup"><span data-stu-id="d3a92-122">We'll show you how to draw the user's attention to your holograms with a directional indicator.</span></span>
* <span data-ttu-id="d3a92-123">Apprenez les techniques à prendre votre hologrammes avec l’utilisateur, car elle ne se déplace dans le monde.</span><span class="sxs-lookup"><span data-stu-id="d3a92-123">We'll teach you techniques to take your holograms with the user as she moves around in your world.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d3a92-124">Les vidéos incorporées dans chacun des chapitres ci-dessous ont été enregistrés à l’aide d’une version antérieure de Unity et le Kit de ressources de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="d3a92-124">The videos embedded in each of the chapters below were recorded using an older version of Unity and the Mixed Reality Toolkit.</span></span> <span data-ttu-id="d3a92-125">Tandis que les instructions pas à pas sont précises et actuelles, vous pouvez voir des scripts et des éléments visuels dans les vidéos correspondantes qui sont obsolètes.</span><span class="sxs-lookup"><span data-stu-id="d3a92-125">While the step-by-step instructions are accurate and current, you may see scripts and visuals in the corresponding videos that are out-of-date.</span></span> <span data-ttu-id="d3a92-126">Les vidéos restent inclus éternellement et car couvert les concepts s’appliquent toujours.</span><span class="sxs-lookup"><span data-stu-id="d3a92-126">The videos remain included for posterity and because the concepts covered still apply.</span></span>

## <a name="device-support"></a><span data-ttu-id="d3a92-127">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="d3a92-127">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="d3a92-128">Cours</span><span class="sxs-lookup"><span data-stu-id="d3a92-128">Course</span></span></th><th style="width:150px"> <span data-ttu-id="d3a92-129"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="d3a92-129"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="d3a92-130"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="d3a92-130"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="d3a92-131">Entrée M. 210 : Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="d3a92-131">MR Input 210: Gaze</span></span></td><td style="text-align: center;"> <span data-ttu-id="d3a92-132">✔️</span><span class="sxs-lookup"><span data-stu-id="d3a92-132">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="d3a92-133">✔️</span><span class="sxs-lookup"><span data-stu-id="d3a92-133">✔️</span></span></td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="d3a92-134">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d3a92-134">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d3a92-135">Prérequis</span><span class="sxs-lookup"><span data-stu-id="d3a92-135">Prerequisites</span></span>

* <span data-ttu-id="d3a92-136">Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="d3a92-136">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="d3a92-137">Base C# possibilité de programmation.</span><span class="sxs-lookup"><span data-stu-id="d3a92-137">Some basic C# programming ability.</span></span>
* <span data-ttu-id="d3a92-138">Vous devez avoir terminé [101 de principes de base MR](holograms-101.md).</span><span class="sxs-lookup"><span data-stu-id="d3a92-138">You should have completed [MR Basics 101](holograms-101.md).</span></span>
* <span data-ttu-id="d3a92-139">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="d3a92-139">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="d3a92-140">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="d3a92-140">Project files</span></span>

* <span data-ttu-id="d3a92-141">Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-210-Gaze.zip) requise par le projet.</span><span class="sxs-lookup"><span data-stu-id="d3a92-141">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-210-Gaze.zip) required by the project.</span></span><span data-ttu-id="d3a92-142"> Nécessite Unity 2017.2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d3a92-142"> Requires Unity 2017.2 or later.</span></span>
* <span data-ttu-id="d3a92-143">Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="d3a92-143">Un-archive the files to your desktop or other easy to reach location.</span></span>

>[!NOTE]
><span data-ttu-id="d3a92-144">Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-210-Gaze).</span><span class="sxs-lookup"><span data-stu-id="d3a92-144">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-210-Gaze).</span></span>

### <a name="errata-and-notes"></a><span data-ttu-id="d3a92-145">Errata et remarques</span><span class="sxs-lookup"><span data-stu-id="d3a92-145">Errata and Notes</span></span>

* <span data-ttu-id="d3a92-146">Dans Visual Studio, « Uniquement mon Code » doit être désactivé (décoché) sous Outils -> Options -> débogage afin d’atteindre des points d’arrêt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="d3a92-146">In Visual Studio, "Just My Code" needs to be disabled (unchecked) under Tools->Options->Debugging in order to hit breakpoints in your code.</span></span>

## <a name="chapter-1---unity-setup"></a><span data-ttu-id="d3a92-147">Chapitre 1 - le programme d’installation Unity</span><span class="sxs-lookup"><span data-stu-id="d3a92-147">Chapter 1 - Unity Setup</span></span>

>[!VIDEO https://www.youtube.com/embed/_Ccn6riQ6vU]

### <a name="objectives"></a><span data-ttu-id="d3a92-148">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d3a92-148">Objectives</span></span>

* <span data-ttu-id="d3a92-149">Optimiser Unity pour le développement de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d3a92-149">Optimize Unity for HoloLens development.</span></span>
* <span data-ttu-id="d3a92-150">Importer les ressources et le programme d’installation de la scène.</span><span class="sxs-lookup"><span data-stu-id="d3a92-150">Import assets and setup the scene.</span></span>
* <span data-ttu-id="d3a92-151">Afficher l’astronautes dans la HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d3a92-151">View the astronaut in the HoloLens.</span></span>

### <a name="instructions"></a><span data-ttu-id="d3a92-152">Instructions</span><span class="sxs-lookup"><span data-stu-id="d3a92-152">Instructions</span></span>

1. <span data-ttu-id="d3a92-153">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="d3a92-153">Start Unity.</span></span>
2. <span data-ttu-id="d3a92-154">Sélectionnez **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-154">Select **New Project**.</span></span>
3. <span data-ttu-id="d3a92-155">Nommez le projet **ModelExplorer**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-155">Name the project **ModelExplorer**.</span></span>
4. <span data-ttu-id="d3a92-156">Entrez l’emplacement que le **les regards** dossier vous précédemment non archivés.</span><span class="sxs-lookup"><span data-stu-id="d3a92-156">Enter location as the **Gaze** folder you previously un-archived.</span></span>
5. <span data-ttu-id="d3a92-157">Assurez-vous que le projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-157">Make sure the project is set to **3D**.</span></span>
6. <span data-ttu-id="d3a92-158">Cliquez sur **créer le projet**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-158">Click **Create Project**.</span></span>

### <a name="unity-settings-for-hololens"></a><span data-ttu-id="d3a92-159">Paramètres de Unity pour HoloLens</span><span class="sxs-lookup"><span data-stu-id="d3a92-159">Unity settings for HoloLens</span></span>

<span data-ttu-id="d3a92-160">Nous devons informer Unity que l’application que nous tentons de les exporter doit créer un [vue immersive](app-views.md) au lieu d’une vue en 2D.</span><span class="sxs-lookup"><span data-stu-id="d3a92-160">We need to let Unity know that the app we are trying to export should create an [immersive view](app-views.md) instead of a 2D view.</span></span> <span data-ttu-id="d3a92-161">Nous le faire en ajoutant HoloLens comme un périphérique de réalité virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d3a92-161">We do that by adding HoloLens as a virtual reality device.</span></span>

1. <span data-ttu-id="d3a92-162">Accédez à **Modifier > Paramètres du projet > Lecteur**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-162">Go to **Edit > Project Settings > Player**.</span></span>
2. <span data-ttu-id="d3a92-163">Dans le **panneau Inspecteur** pour les paramètres du lecteur, sélectionnez le **Windows Store** icône.</span><span class="sxs-lookup"><span data-stu-id="d3a92-163">In the **Inspector Panel** for Player Settings, select the **Windows Store** icon.</span></span>
3. <span data-ttu-id="d3a92-164">Développez le **XR paramètres** groupe.</span><span class="sxs-lookup"><span data-stu-id="d3a92-164">Expand the **XR Settings** group.</span></span>
4. <span data-ttu-id="d3a92-165">Dans le **rendu** section, vérifiez le **virtuel pris en charge de réalité** case à cocher pour ajouter un nouveau **SDK de réalité virtuelle** liste.</span><span class="sxs-lookup"><span data-stu-id="d3a92-165">In the **Rendering** section, check the **Virtual Reality Supported** checkbox to add a new **Virtual Reality SDKs** list.</span></span>
5. <span data-ttu-id="d3a92-166">Vérifiez que **Windows Mixed Reality** apparaît dans la liste.</span><span class="sxs-lookup"><span data-stu-id="d3a92-166">Verify that **Windows Mixed Reality** appears in the list.</span></span> <span data-ttu-id="d3a92-167">Dans le cas contraire, sélectionnez le **+** bouton en bas de la liste et choisissez **Windows HOLOGRAPHIQUE**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-167">If not, select the **+** button at the bottom of the list and choose **Windows Holographic**.</span></span>

<span data-ttu-id="d3a92-168">Ensuite, nous devons définir notre principal script vers .NET.</span><span class="sxs-lookup"><span data-stu-id="d3a92-168">Next, we need to set our scripting backend to .NET.</span></span>

1. <span data-ttu-id="d3a92-169">Accédez à **Modifier > Paramètres du projet > Lecteur** (que vous deviez toujours cette à partir de l’étape précédente).</span><span class="sxs-lookup"><span data-stu-id="d3a92-169">Go to **Edit > Project Settings > Player** (you may still have this up from the previous step).</span></span>
2. <span data-ttu-id="d3a92-170">Dans le **panneau Inspecteur** pour les paramètres du lecteur, sélectionnez le **Windows Store** icône.</span><span class="sxs-lookup"><span data-stu-id="d3a92-170">In the **Inspector Panel** for Player Settings, select the **Windows Store** icon.</span></span>
3. <span data-ttu-id="d3a92-171">Dans le **autres paramètres** Configuration section, assurez-vous que l’option **Backend Scripting** a la valeur **.NET**</span><span class="sxs-lookup"><span data-stu-id="d3a92-171">In the **Other Settings** Configuration section, make sure that **Scripting Backend** is set to **.NET**</span></span>

<span data-ttu-id="d3a92-172">Enfin, nous mettrons à jour nos paramètres de qualité pour accélérer les performances sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d3a92-172">Finally, we'll update our quality settings to achieve a fast performance on HoloLens.</span></span>

1. <span data-ttu-id="d3a92-173">Accédez à **Modifier > Paramètres du projet > qualité**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-173">Go to **Edit > Project Settings > Quality**.</span></span>
2. <span data-ttu-id="d3a92-174">Cliquez sur la flèche vers le bas dans la **par défaut** ligne sous l’icône du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="d3a92-174">Click on downward pointing arrow in the **Default** row under the Windows Store icon.</span></span>
3. <span data-ttu-id="d3a92-175">Sélectionnez **très faible** pour **applications du Windows Store**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-175">Select **Very Low** for **Windows Store Apps**.</span></span>

### <a name="import-project-assets"></a><span data-ttu-id="d3a92-176">Importer des éléments de projet</span><span class="sxs-lookup"><span data-stu-id="d3a92-176">Import project assets</span></span>

1. <span data-ttu-id="d3a92-177">Bouton droit sur le **actifs** dossier dans le **projet** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="d3a92-177">Right click the **Assets** folder in the **Project** panel.</span></span>
2. <span data-ttu-id="d3a92-178">Cliquez sur **importer un Package > Package personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-178">Click on **Import Package > Custom Package**.</span></span>
3. <span data-ttu-id="d3a92-179">Accédez aux fichiers de projet que vous avez téléchargé, puis cliquez sur **ModelExplorer.unitypackage**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-179">Navigate to the project files you downloaded and click on **ModelExplorer.unitypackage**.</span></span>
4. <span data-ttu-id="d3a92-180">Cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-180">Click **Open**.</span></span>
5. <span data-ttu-id="d3a92-181">Une fois le package chargé, cliquez sur le **importation** bouton.</span><span class="sxs-lookup"><span data-stu-id="d3a92-181">After the package loads, click on the **Import** button.</span></span>

### <a name="setup-the-scene"></a><span data-ttu-id="d3a92-182">Le programme d’installation de la scène</span><span class="sxs-lookup"><span data-stu-id="d3a92-182">Setup the scene</span></span>

1. <span data-ttu-id="d3a92-183">Dans la hiérarchie, supprimez le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-183">In the Hierarchy, delete the **Main Camera**.</span></span>
2. <span data-ttu-id="d3a92-184">Dans le **HoloToolkit** dossier, ouvrez le **entrée** dossier, puis ouvrez le **Prefabs** dossier.</span><span class="sxs-lookup"><span data-stu-id="d3a92-184">In the **HoloToolkit** folder, open the **Input** folder, then open the **Prefabs** folder.</span></span>
3. <span data-ttu-id="d3a92-185">Faites glisser et déposez le **MixedRealityCameraParent** prefab à partir de la **Prefabs** dossier vers le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-185">Drag and drop the **MixedRealityCameraParent** prefab from the **Prefabs** folder into the **Hierarchy**.</span></span>
4. <span data-ttu-id="d3a92-186">Cliquez sur le **lumière directionnelle** dans la hiérarchie et choisissez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-186">Right-click the **Directional Light** in the Hierarchy and select **Delete**.</span></span>
5. <span data-ttu-id="d3a92-187">Dans le **Vntana** dossier, faites glisser et déposez les ressources suivantes dans la racine de la **hiérarchie**:</span><span class="sxs-lookup"><span data-stu-id="d3a92-187">In the **Holograms** folder, drag and drop the following assets into the root of the **Hierarchy**:</span></span>
    * <span data-ttu-id="d3a92-188">**AstroMan**</span><span class="sxs-lookup"><span data-stu-id="d3a92-188">**AstroMan**</span></span>
    * <span data-ttu-id="d3a92-189">**lumières**</span><span class="sxs-lookup"><span data-stu-id="d3a92-189">**Lights**</span></span>
    * <span data-ttu-id="d3a92-190">**SpaceAudioSource**</span><span class="sxs-lookup"><span data-stu-id="d3a92-190">**SpaceAudioSource**</span></span>
    * <span data-ttu-id="d3a92-191">**SpaceBackground**</span><span class="sxs-lookup"><span data-stu-id="d3a92-191">**SpaceBackground**</span></span>
6. <span data-ttu-id="d3a92-192">Démarrer **Mode lecture** ▶ pour afficher l’astronautes !.</span><span class="sxs-lookup"><span data-stu-id="d3a92-192">Start **Play Mode** ▶ to view the astronaut.</span></span>
7. <span data-ttu-id="d3a92-193">Cliquez sur **Mode lecture** ▶ à nouveau à **arrêter**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-193">Click **Play Mode** ▶ again to **Stop**.</span></span>
8. <span data-ttu-id="d3a92-194">Dans le **hologrammes** dossier, rechercher le **Fitbox** asset et faites-le glisser vers la racine de la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-194">In the **Holograms** folder, find the **Fitbox** asset and drag it to the root of the **Hierarchy**.</span></span>
9. <span data-ttu-id="d3a92-195">Sélectionnez le **Fitbox** dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="d3a92-195">Select the **Fitbox** in the **Hierarchy** panel.</span></span>
10. <span data-ttu-id="d3a92-196">Faites glisser le **AstroMan** collection à partir de la **hiérarchie** à la **hologramme Collection** propriété de la Fitbox dans le **inspecteur** panneau.</span><span class="sxs-lookup"><span data-stu-id="d3a92-196">Drag the **AstroMan** collection from the **Hierarchy** to the **Hologram Collection** property of the Fitbox in the **Inspector** panel.</span></span>

### <a name="save-the-project"></a><span data-ttu-id="d3a92-197">Enregistrer le projet</span><span class="sxs-lookup"><span data-stu-id="d3a92-197">Save the project</span></span>

1. <span data-ttu-id="d3a92-198">Enregistrer la nouvelle scène : **Fichier > Enregistrer la scène sous**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-198">Save the new scene: **File > Save Scene As**.</span></span>
2. <span data-ttu-id="d3a92-199">Cliquez sur **nouveau dossier** et nommez le dossier **scènes**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-199">Click **New Folder** and name the folder **Scenes**.</span></span>
3. <span data-ttu-id="d3a92-200">Nommez le fichier «**ModelExplorer**» et l’enregistrer dans le **scènes** dossier.</span><span class="sxs-lookup"><span data-stu-id="d3a92-200">Name the file “**ModelExplorer**” and save it in the **Scenes** folder.</span></span>

### <a name="build-the-project"></a><span data-ttu-id="d3a92-201">Générez le projet</span><span class="sxs-lookup"><span data-stu-id="d3a92-201">Build the project</span></span>

1. <span data-ttu-id="d3a92-202">Dans Unity, sélectionnez **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-202">In Unity, select **File > Build Settings**.</span></span>
2. <span data-ttu-id="d3a92-203">Cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="d3a92-203">Click **Add Open Scenes** to add the scene.</span></span>
3. <span data-ttu-id="d3a92-204">Sélectionnez **plateforme Windows universelle** dans le **plateforme** liste et cliquez sur **plateforme de commutation**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-204">Select **Universal Windows Platform** in the **Platform** list and click **Switch Platform**.</span></span>
4. <span data-ttu-id="d3a92-205">Si vous développez en particulier pour HoloLens, définissez **appareil cible** à **HoloLens**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-205">If you're specifically developing for HoloLens, set **Target device** to **HoloLens**.</span></span> <span data-ttu-id="d3a92-206">Dans le cas contraire, laissez-le sur **n’importe quel appareil**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-206">Otherwise, leave it on **Any device**.</span></span>
5. <span data-ttu-id="d3a92-207">Vérifiez **Type Build** a la valeur **D3D** et **SDK** a la valeur **dernière installé** (qui doit être SDK 16299 ou une version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="d3a92-207">Ensure **Build Type** is set to **D3D** and **SDK** is set to **Latest installed** (which should be SDK 16299 or newer).</span></span>
6. <span data-ttu-id="d3a92-208">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-208">Click **Build**.</span></span>
7. <span data-ttu-id="d3a92-209">Créer un **nouveau dossier** nommé « Application ».</span><span class="sxs-lookup"><span data-stu-id="d3a92-209">Create a **New Folder** named "App".</span></span>
8. <span data-ttu-id="d3a92-210">Clic le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="d3a92-210">Single click the **App** folder.</span></span>
9. <span data-ttu-id="d3a92-211">Appuyez sur **sélectionnez dossier**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-211">Press **Select Folder**.</span></span>

<span data-ttu-id="d3a92-212">Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d3a92-212">When Unity is done, a File Explorer window will appear.</span></span>

1. <span data-ttu-id="d3a92-213">Ouvrez le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="d3a92-213">Open the **App** folder.</span></span>
2. <span data-ttu-id="d3a92-214">Ouvrez le **ModelExplorer Visual Studio Solution**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-214">Open the **ModelExplorer Visual Studio Solution**.</span></span>

<span data-ttu-id="d3a92-215">Si le déploiement sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="d3a92-215">If deploying to HoloLens:</span></span>

1. <span data-ttu-id="d3a92-216">À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x86**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-216">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x86**.</span></span>
2. <span data-ttu-id="d3a92-217">Cliquez sur la flèche déroulante en regard du bouton de l’ordinateur Local, puis sélectionnez **Machine distante**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-217">Click on the drop down arrow next to the Local Machine button, and select **Remote Machine**.</span></span>
3. <span data-ttu-id="d3a92-218">Entrez **votre adresse IP du périphérique HoloLens** et définir le Mode d’authentification **universel (protocole non chiffré)**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-218">Enter **your HoloLens device IP address** and set Authentication Mode to **Universal (Unencrypted Protocol)**.</span></span> <span data-ttu-id="d3a92-219">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-219">Click **Select**.</span></span> <span data-ttu-id="d3a92-220">Si vous ne connaissez pas votre adresse IP du périphérique, recherchez dans **Paramètres > réseau & Internet > Options avancées**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-220">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options**.</span></span>
4. <span data-ttu-id="d3a92-221">Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-221">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="d3a92-222">S’il s’agit de la première fois le déploiement sur votre périphérique, vous devrez [Couplez-le Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span><span class="sxs-lookup"><span data-stu-id="d3a92-222">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span></span>
5. <span data-ttu-id="d3a92-223">Lorsque l’application a été déployée, faire disparaître le **Fitbox** avec un **sélectionnez mouvement**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-223">When the app has deployed, dismiss the **Fitbox** with a **select gesture**.</span></span>

<span data-ttu-id="d3a92-224">Si le déploiement sur un casque immersif :</span><span class="sxs-lookup"><span data-stu-id="d3a92-224">If deploying to an immersive headset:</span></span>

1. <span data-ttu-id="d3a92-225">À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x64**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-225">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x64**.</span></span>
2. <span data-ttu-id="d3a92-226">Assurez-vous que la cible de déploiement est définie sur **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-226">Make sure the deployment target is set to **Local Machine**.</span></span>
3. <span data-ttu-id="d3a92-227">Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-227">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
4. <span data-ttu-id="d3a92-228">Lorsque l’application a été déployée, faire disparaître le **Fitbox** en extrayant le déclencheur sur un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="d3a92-228">When the app has deployed, dismiss the **Fitbox** by pulling the trigger on a motion controller.</span></span>

## <a name="chapter-2---cursor-and-target-feedback"></a><span data-ttu-id="d3a92-229">Chapitre 2 - commentaires curseur et la cible</span><span class="sxs-lookup"><span data-stu-id="d3a92-229">Chapter 2 - Cursor and target feedback</span></span>

>[!VIDEO https://www.youtube.com/embed/S24u0V_T7ZI]

### <a name="objectives"></a><span data-ttu-id="d3a92-230">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d3a92-230">Objectives</span></span>

* <span data-ttu-id="d3a92-231">Conception visuelle du curseur et le comportement.</span><span class="sxs-lookup"><span data-stu-id="d3a92-231">Cursor visual design and behavior.</span></span>
* <span data-ttu-id="d3a92-232">Curseur du pointage de regard.</span><span class="sxs-lookup"><span data-stu-id="d3a92-232">Gaze-based cursor feedback.</span></span>
* <span data-ttu-id="d3a92-233">Commentaires de hologramme basée sur des regards.</span><span class="sxs-lookup"><span data-stu-id="d3a92-233">Gaze-based hologram feedback.</span></span>

<span data-ttu-id="d3a92-234">Nous allons notre travail de base sur quelques principes de conception de curseur, à savoir :</span><span class="sxs-lookup"><span data-stu-id="d3a92-234">We're going to base our work on some cursor design principles, namely:</span></span>

* <span data-ttu-id="d3a92-235">Le curseur est toujours présent.</span><span class="sxs-lookup"><span data-stu-id="d3a92-235">The cursor is always present.</span></span>
* <span data-ttu-id="d3a92-236">Ne laissez pas le curseur obtenir trop petite ou grande.</span><span class="sxs-lookup"><span data-stu-id="d3a92-236">Don't let the cursor get too small or big.</span></span>
* <span data-ttu-id="d3a92-237">Évitez l’obstruction de contenu.</span><span class="sxs-lookup"><span data-stu-id="d3a92-237">Avoid obstructing content.</span></span>

### <a name="instructions"></a><span data-ttu-id="d3a92-238">Instructions</span><span class="sxs-lookup"><span data-stu-id="d3a92-238">Instructions</span></span>

1. <span data-ttu-id="d3a92-239">Dans le **HoloToolkit\Input\Prefabs** dossier, recherchez le **InputManager** actif.</span><span class="sxs-lookup"><span data-stu-id="d3a92-239">In the **HoloToolkit\Input\Prefabs** folder, find the **InputManager** asset.</span></span>
2. <span data-ttu-id="d3a92-240">Faites glisser et déposez le **InputManager** sur le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-240">Drag and drop the **InputManager** onto the **Hierarchy**.</span></span>
3. <span data-ttu-id="d3a92-241">Dans le **HoloToolkit\Input\Prefabs** dossier, recherchez le **curseur** actif.</span><span class="sxs-lookup"><span data-stu-id="d3a92-241">In the **HoloToolkit\Input\Prefabs** folder, find the **Cursor** asset.</span></span>
4. <span data-ttu-id="d3a92-242">Faites glisser et déposez le **curseur** sur le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-242">Drag and drop the **Cursor** onto the **Hierarchy**.</span></span>
5. <span data-ttu-id="d3a92-243">Sélectionnez le **InputManager** de l’objet dans le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-243">Select the **InputManager** object in the **Hierarchy**.</span></span>
6. <span data-ttu-id="d3a92-244">Faites glisser le **curseur** à partir de l’objet le **hiérarchie** dans le InputManager **SimpleSinglePointerSelector**de **curseur** champ, à la en bas de la **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-244">Drag the **Cursor** object from the **Hierarchy** into the InputManager's **SimpleSinglePointerSelector**'s **Cursor** field, at the bottom of the **Inspector**.</span></span>

![Configuration de sélecteur de pointeur unique simple](images/holograms210-ssps.png)

### <a name="build-and-deploy"></a><span data-ttu-id="d3a92-246">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="d3a92-246">Build and Deploy</span></span>

1. <span data-ttu-id="d3a92-247">Régénérer l’application à partir de **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-247">Rebuild the app from **File > Build Settings**.</span></span>
2. <span data-ttu-id="d3a92-248">Ouvrez le **dossier application**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-248">Open the **App folder**.</span></span>
3. <span data-ttu-id="d3a92-249">Ouvrez le **ModelExplorer Visual Studio Solution**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-249">Open the **ModelExplorer Visual Studio Solution**.</span></span>
4. <span data-ttu-id="d3a92-250">Cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-250">Click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
5. <span data-ttu-id="d3a92-251">Observez comment le curseur est dessiné, et comment elles évoluent apparence si elle est toucher un hologramme.</span><span class="sxs-lookup"><span data-stu-id="d3a92-251">Observe how the cursor is drawn, and how it changes appearance if it is touching a hologram.</span></span>

### <a name="instructions"></a><span data-ttu-id="d3a92-252">Instructions</span><span class="sxs-lookup"><span data-stu-id="d3a92-252">Instructions</span></span>

1. <span data-ttu-id="d3a92-253">Dans le **hiérarchie** volet, développez le **AstroMan**->**GEO_G**->**Back_Center** objet.</span><span class="sxs-lookup"><span data-stu-id="d3a92-253">In the **Hierarchy** panel, expand the **AstroMan**->**GEO_G**->**Back_Center** object.</span></span>
2. <span data-ttu-id="d3a92-254">Double-cliquez sur **Interactible.cs** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3a92-254">Double click on **Interactible.cs** to open it in Visual Studio.</span></span>
3. <span data-ttu-id="d3a92-255">Ne pas commenter les lignes dans le **IFocusable.OnFocusEnter()** et **IFocusable.OnFocusExit()** rappels dans **Interactible.cs**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-255">Uncomment the lines in the **IFocusable.OnFocusEnter()** and **IFocusable.OnFocusExit()** callbacks in **Interactible.cs**.</span></span> <span data-ttu-id="d3a92-256">Ceux-ci sont appelées par InputManager du Toolkit de réalité mixte lorsque le focus (soit en regards ou en pointant de contrôleur) entre et sort des collider du GameObject spécifique.</span><span class="sxs-lookup"><span data-stu-id="d3a92-256">These are called by the Mixed Reality Toolkit's InputManager when focus (either by gaze or by controller pointing) enters and exits the specific GameObject's collider.</span></span>

```cs
/* TODO: DEVELOPER CODING EXERCISE 2.d */

void IFocusable.OnFocusEnter()
{
    for (int i = 0; i < defaultMaterials.Length; i++)
    {
        // 2.d: Uncomment the below line to highlight the material when gaze enters.
        defaultMaterials[i].EnableKeyword("_ENVIRONMENT_COLORING");
    }
}

void IFocusable.OnFocusExit()
{
    for (int i = 0; i < defaultMaterials.Length; i++)
    {
        // 2.d: Uncomment the below line to remove highlight on material when gaze exits.
        defaultMaterials[i].DisableKeyword("_ENVIRONMENT_COLORING");
    }
}
```

>[!NOTE]
><span data-ttu-id="d3a92-257">Nous utilisons `EnableKeyword` et `DisableKeyword` ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d3a92-257">We use `EnableKeyword` and `DisableKeyword` above.</span></span> <span data-ttu-id="d3a92-258">Afin de rendre utiliser ces éléments dans votre propre application avec nuanceur Standard de la boîte à outils, vous devrez suivre la [les instructions permettant d’accéder aux documents via un script Unity](https://docs.unity3d.com/Manual/MaterialsAccessingViaScript.html).</span><span class="sxs-lookup"><span data-stu-id="d3a92-258">In order to make use of these in your own app with the Toolkit's Standard shader, you'll need to follow the [Unity guidelines for accessing materials via script](https://docs.unity3d.com/Manual/MaterialsAccessingViaScript.html).</span></span> <span data-ttu-id="d3a92-259">Dans ce cas, nous avons déjà inclus le [trois variantes de matériau en surbrillance](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-210-Gaze/Completed/ModelExplorer/Assets/Resources/Models/AstroMan/Materials) nécessaires dans le dossier de ressources (recherchez les trois documents avec mise en surbrillance dans le nom).</span><span class="sxs-lookup"><span data-stu-id="d3a92-259">In this case, we've already included the [three variants of highlighted material](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-210-Gaze/Completed/ModelExplorer/Assets/Resources/Models/AstroMan/Materials) needed in the Resources folder (look for the three materials with highlight in the name).</span></span>

### <a name="build-and-deploy"></a><span data-ttu-id="d3a92-260">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="d3a92-260">Build and Deploy</span></span>

1. <span data-ttu-id="d3a92-261">Comme précédemment, générez le projet et déployer sur le HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d3a92-261">As before, build the project and deploy to the HoloLens.</span></span>
2. <span data-ttu-id="d3a92-262">Observez que se passe-t-il lorsque les regards vise à un objet et quand il n’est pas.</span><span class="sxs-lookup"><span data-stu-id="d3a92-262">Observe what happens when the gaze is aimed at an object and when it's not.</span></span>

## <a name="chapter-3---targeting-techniques"></a><span data-ttu-id="d3a92-263">Chapitre 3 - Techniques de ciblage</span><span class="sxs-lookup"><span data-stu-id="d3a92-263">Chapter 3 - Targeting Techniques</span></span>

>[!VIDEO https://www.youtube.com/embed/TFnuLva4VJ0]

### <a name="objectives"></a><span data-ttu-id="d3a92-264">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d3a92-264">Objectives</span></span>

* <span data-ttu-id="d3a92-265">Faciliter les hologrammes cible.</span><span class="sxs-lookup"><span data-stu-id="d3a92-265">Make it easier to target holograms.</span></span>
* <span data-ttu-id="d3a92-266">Stabilisez les mouvements de la tête naturelles.</span><span class="sxs-lookup"><span data-stu-id="d3a92-266">Stabilize natural head movements.</span></span>

### <a name="instructions"></a><span data-ttu-id="d3a92-267">Instructions</span><span class="sxs-lookup"><span data-stu-id="d3a92-267">Instructions</span></span>

1. <span data-ttu-id="d3a92-268">Dans le **hiérarchie** Panneau de configuration, sélectionnez le **InputManager** objet.</span><span class="sxs-lookup"><span data-stu-id="d3a92-268">In the **Hierarchy** panel, select the **InputManager** object.</span></span>
2. <span data-ttu-id="d3a92-269">Dans le **inspecteur** panneau, recherchez le **les regards de stabilisation** script.</span><span class="sxs-lookup"><span data-stu-id="d3a92-269">In the **Inspector** panel, find the **Gaze Stabilizer** script.</span></span> <span data-ttu-id="d3a92-270">Cliquez dessus pour l’ouvrir dans Visual Studio, si vous souhaitez jeter un coup de œil.</span><span class="sxs-lookup"><span data-stu-id="d3a92-270">Click it to open in Visual Studio, if you want to take a look.</span></span>
    * <span data-ttu-id="d3a92-271">Ce script effectue une itération sur les échantillons de données de Raycast et vous aide à stabiliser les regards de l’utilisateur pour le ciblage de précision.</span><span class="sxs-lookup"><span data-stu-id="d3a92-271">This script iterates over samples of Raycast data and helps stabilize the user's gaze for precision targeting.</span></span>
3. <span data-ttu-id="d3a92-272">Dans le **inspecteur**, vous pouvez modifier le **stockées des exemples de la stabilité** valeur.</span><span class="sxs-lookup"><span data-stu-id="d3a92-272">In the **Inspector**, you can edit the **Stored Stability Samples** value.</span></span> <span data-ttu-id="d3a92-273">Cette valeur représente le nombre d’échantillons qui la stabilisation effectue une itération à calculer la valeur stabilisée.</span><span class="sxs-lookup"><span data-stu-id="d3a92-273">This value represents the number of samples that the stabilizer iterates on to calculate the stabilized value.</span></span>

## <a name="chapter-4---directional-indicator"></a><span data-ttu-id="d3a92-274">Chapitre 4 - indicateur directionnel</span><span class="sxs-lookup"><span data-stu-id="d3a92-274">Chapter 4 - Directional indicator</span></span>

>[!VIDEO https://www.youtube.com/embed/htVbJCMlj64]

### <a name="objectives"></a><span data-ttu-id="d3a92-275">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d3a92-275">Objectives</span></span>

* <span data-ttu-id="d3a92-276">Ajouter un indicateur directionnel sur le curseur pour aider à trouver hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d3a92-276">Add a directional indicator on the cursor to help find holograms.</span></span>

### <a name="instructions"></a><span data-ttu-id="d3a92-277">Instructions</span><span class="sxs-lookup"><span data-stu-id="d3a92-277">Instructions</span></span>

<span data-ttu-id="d3a92-278">Nous allons utiliser le **DirectionIndicator.cs** fichier qui contiendra :</span><span class="sxs-lookup"><span data-stu-id="d3a92-278">We're going to use the **DirectionIndicator.cs** file which will:</span></span>

1. <span data-ttu-id="d3a92-279">Afficher l’indicateur directionnel si l’utilisateur n’est pas gazing aux hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d3a92-279">Show the directional indicator if the user is not gazing at the holograms.</span></span>
2. <span data-ttu-id="d3a92-280">Masquer l’indicateur directionnel si l’utilisateur est gazing aux hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d3a92-280">Hide the directional indicator if the user is gazing at the holograms.</span></span>
3. <span data-ttu-id="d3a92-281">Mettre à jour l’indicateur directionnel pour pointer vers les hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d3a92-281">Update the directional indicator to point to the holograms.</span></span>

<span data-ttu-id="d3a92-282">Commençons.</span><span class="sxs-lookup"><span data-stu-id="d3a92-282">Let's get started.</span></span>

1. <span data-ttu-id="d3a92-283">Cliquez sur le **AstroMan** de l’objet dans le **hiérarchie** panneau et **cliquez sur la flèche** pour le développer.</span><span class="sxs-lookup"><span data-stu-id="d3a92-283">Click on the **AstroMan** object in the **Hierarchy** panel and **click the arrow** to expand it.</span></span>
2. <span data-ttu-id="d3a92-284">Dans le **hiérarchie** Panneau de configuration, sélectionnez le **DirectionalIndicator** objet sous **AstroMan**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-284">In the **Hierarchy** panel, select the **DirectionalIndicator** object under **AstroMan**.</span></span>
3. <span data-ttu-id="d3a92-285">Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="d3a92-285">In the **Inspector** panel, click the **Add Component** button.</span></span>
4. <span data-ttu-id="d3a92-286">Dans le menu, tapez dans la zone de recherche **indicateur de Direction**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-286">In the menu, type in the search box **Direction Indicator**.</span></span> <span data-ttu-id="d3a92-287">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="d3a92-287">Select the search result.</span></span>
5. <span data-ttu-id="d3a92-288">Dans le **hiérarchie** volet, faites glisser le **curseur** de l’objet sur le **curseur** propriété dans le **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-288">In the **Hierarchy** panel, drag and drop the **Cursor** object onto the **Cursor** property in the **Inspector**.</span></span>
6. <span data-ttu-id="d3a92-289">Dans le **projet** volet le **hologrammes** dossier, faites glisser et déposez le **DirectionalIndicator** actif sur le **indicateur directionnel**propriété dans le **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-289">In the **Project** panel, in the **Holograms** folder, drag and drop the **DirectionalIndicator** asset onto the **Directional Indicator** property in the **Inspector**.</span></span>
7. <span data-ttu-id="d3a92-290">Générez et déployez l’application.</span><span class="sxs-lookup"><span data-stu-id="d3a92-290">Build and deploy the app.</span></span>
8. <span data-ttu-id="d3a92-291">Regardez la façon dont l’objet de l’indicateur directionnel vous permet de trouver l’astronautes !.</span><span class="sxs-lookup"><span data-stu-id="d3a92-291">Watch how the directional indicator object helps you find the astronaut.</span></span>

## <a name="chapter-5---billboarding"></a><span data-ttu-id="d3a92-292">Chapitre 5 - le Billboarding</span><span class="sxs-lookup"><span data-stu-id="d3a92-292">Chapter 5 - Billboarding</span></span>

>[!VIDEO https://www.youtube.com/embed/qFiLr_LUACE]

### <a name="objectives"></a><span data-ttu-id="d3a92-293">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d3a92-293">Objectives</span></span>

* <span data-ttu-id="d3a92-294">Utilisez le billboarding avoir hologrammes toujours faire face vers vous.</span><span class="sxs-lookup"><span data-stu-id="d3a92-294">Use billboarding to have holograms always face towards you.</span></span>

<span data-ttu-id="d3a92-295">Nous allons utiliser le **Billboard.cs** à conserver un GameObject orientée services de sorte qu’il est accessible sur l’utilisateur à tout moment.</span><span class="sxs-lookup"><span data-stu-id="d3a92-295">We will be using the **Billboard.cs** file to keep a GameObject oriented such that it is facing the user at all times.</span></span>

1. <span data-ttu-id="d3a92-296">Dans le **hiérarchie** Panneau de configuration, sélectionnez le **AstroMan** objet.</span><span class="sxs-lookup"><span data-stu-id="d3a92-296">In the **Hierarchy** panel, select the **AstroMan** object.</span></span>
2. <span data-ttu-id="d3a92-297">Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="d3a92-297">In the **Inspector** panel, click the **Add Component** button.</span></span>
3. <span data-ttu-id="d3a92-298">Dans le menu, tapez dans la zone de recherche **Billboard**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-298">In the menu, type in the search box **Billboard**.</span></span> <span data-ttu-id="d3a92-299">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="d3a92-299">Select the search result.</span></span>
4. <span data-ttu-id="d3a92-300">Dans le **inspecteur** définir le **axe de tableau croisé dynamique** à **Y**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-300">In the **Inspector** set the **Pivot Axis** to **Y**.</span></span>
5. <span data-ttu-id="d3a92-301">Essayez !</span><span class="sxs-lookup"><span data-stu-id="d3a92-301">Try it!</span></span> <span data-ttu-id="d3a92-302">Générer et déployer l’application comme avant.</span><span class="sxs-lookup"><span data-stu-id="d3a92-302">Build and deploy the app as before.</span></span>
6. <span data-ttu-id="d3a92-303">Voir comment l’objet Billboard faces, quel que soit la façon dont vous modifiez le point de vue.</span><span class="sxs-lookup"><span data-stu-id="d3a92-303">See how the Billboard object faces you no matter how you change the viewpoint.</span></span>
7. <span data-ttu-id="d3a92-304">Supprimez le script à partir de la **AstroMan** pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="d3a92-304">Delete the script from the **AstroMan** for now.</span></span>

## <a name="chapter-6---tag-along"></a><span data-ttu-id="d3a92-305">Chapitre 6 - Tag-Along</span><span class="sxs-lookup"><span data-stu-id="d3a92-305">Chapter 6 - Tag-Along</span></span>

>[!VIDEO https://www.youtube.com/embed/Ct8ORZAX5JU]

### <a name="objectives"></a><span data-ttu-id="d3a92-306">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d3a92-306">Objectives</span></span>

* <span data-ttu-id="d3a92-307">Utilisez Tag-Along pour que notre hologrammes Suivez-nous autour de la pièce.</span><span class="sxs-lookup"><span data-stu-id="d3a92-307">Use Tag-Along to have our holograms follow us around the room.</span></span>

<span data-ttu-id="d3a92-308">Car nous travaillons à ce problème, nous allons guidées par les contraintes de conception suivantes :</span><span class="sxs-lookup"><span data-stu-id="d3a92-308">As we work on this issue, we'll be guided by the following design constraints:</span></span>

* <span data-ttu-id="d3a92-309">Contenu doit toujours être un coup de œil de suite.</span><span class="sxs-lookup"><span data-stu-id="d3a92-309">Content should always be a glance away.</span></span>
* <span data-ttu-id="d3a92-310">Contenu ne doit pas être de la façon.</span><span class="sxs-lookup"><span data-stu-id="d3a92-310">Content should not be in the way.</span></span>
* <span data-ttu-id="d3a92-311">Verrouillage de tête le contenu est désagréable.</span><span class="sxs-lookup"><span data-stu-id="d3a92-311">Head-locking content is uncomfortable.</span></span>

<span data-ttu-id="d3a92-312">La solution utilisée ici est d’utiliser une approche « tag-along ».</span><span class="sxs-lookup"><span data-stu-id="d3a92-312">The solution used here is to use a "tag-along" approach.</span></span>

<span data-ttu-id="d3a92-313">Un objet tag-along quitte jamais complètement la vue de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d3a92-313">A tag-along object never fully leaves the user's view.</span></span> <span data-ttu-id="d3a92-314">Vous pouvez considérer l’un tag-along comme étant un objet attaché à la tête de l’utilisateur par élastiques.</span><span class="sxs-lookup"><span data-stu-id="d3a92-314">You can think of the a tag-along as being an object attached to the user's head by rubber bands.</span></span> <span data-ttu-id="d3a92-315">Lorsque l’utilisateur se trouve, le contenu reste au sein d’un simple coup de œil en faisant glisser vers le bord de la vue sans quitter complètement.</span><span class="sxs-lookup"><span data-stu-id="d3a92-315">As the user moves, the content will stay within an easy glance by sliding towards the edge of the view without completely leaving.</span></span> <span data-ttu-id="d3a92-316">Lorsque l’utilisateur son rapprocher de l’objet tag-along, il s’agit plus en détail dans la vue.</span><span class="sxs-lookup"><span data-stu-id="d3a92-316">When the user gazes towards the tag-along object, it comes more fully into view.</span></span>

<span data-ttu-id="d3a92-317">Nous allons utiliser le **SimpleTagalong.cs** fichier qui contiendra :</span><span class="sxs-lookup"><span data-stu-id="d3a92-317">We're going to use the **SimpleTagalong.cs** file which will:</span></span>

1. <span data-ttu-id="d3a92-318">Détermine si l’objet Tag-Along dans les limites de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="d3a92-318">Determine if the Tag-Along object is within the camera bounds.</span></span>
2. <span data-ttu-id="d3a92-319">Si ce n’est pas le cas dans le frustum vue, placer le Tag-Along à partiellement dans frustum de la vue.</span><span class="sxs-lookup"><span data-stu-id="d3a92-319">If not within the view frustum, position the Tag-Along to partially within the view frustum.</span></span>
3. <span data-ttu-id="d3a92-320">Sinon, positionnez le Tag-Along à une distance par défaut à partir de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d3a92-320">Otherwise, position the Tag-Along to a default distance from the user.</span></span>

<span data-ttu-id="d3a92-321">Pour ce faire, nous devons changiez le **Interactible.cs** script pour appeler le **TagalongAction**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-321">To do this, we first must change the **Interactible.cs** script to call the **TagalongAction**.</span></span>

1. <span data-ttu-id="d3a92-322">Modifier **Interactible.cs** en effectuant le codage exercice 6.a (suppression de commentaires dans les lignes 84 à 87).</span><span class="sxs-lookup"><span data-stu-id="d3a92-322">Edit **Interactible.cs** by completing coding exercise 6.a (uncommenting lines 84 to 87).</span></span>

```cs
/* TODO: DEVELOPER CODING EXERCISE 6.a */
// 6.a: Uncomment the lines below to perform a Tagalong action.
if (interactibleAction != null)
{
    interactibleAction.PerformAction();
}
```

<span data-ttu-id="d3a92-323">Le **InteractibleAction.cs** script, associé au **Interactible.cs** effectue des actions personnalisées lorsque vous appuyez sur hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d3a92-323">The **InteractibleAction.cs** script, paired with **Interactible.cs** performs custom actions when you tap on holograms.</span></span> <span data-ttu-id="d3a92-324">Dans ce cas, nous utiliserons un en particulier pour tag-along.</span><span class="sxs-lookup"><span data-stu-id="d3a92-324">In this case, we'll use one specifically for tag-along.</span></span>

* <span data-ttu-id="d3a92-325">Dans le **Scripts** dossier, cliquez sur **TagalongAction.cs** asset pour ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3a92-325">In the **Scripts** folder click on **TagalongAction.cs** asset to open in Visual Studio.</span></span>
* <span data-ttu-id="d3a92-326">Terminer l’exercice de codage ou le remplacer par ceci :</span><span class="sxs-lookup"><span data-stu-id="d3a92-326">Complete the coding exercise or change it to this:</span></span>
  * <span data-ttu-id="d3a92-327">En haut de la **hiérarchie**, dans le type de barre de recherche **ChestButton_Center** et sélectionnez le résultat.</span><span class="sxs-lookup"><span data-stu-id="d3a92-327">At the top of the **Hierarchy**, in the search bar type **ChestButton_Center** and select the result.</span></span>
  * <span data-ttu-id="d3a92-328">Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="d3a92-328">In the **Inspector** panel, click the **Add Component** button.</span></span>
  * <span data-ttu-id="d3a92-329">Dans le menu, tapez dans la zone de recherche **accompagnent Action**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-329">In the menu, type in the search box **Tagalong Action**.</span></span> <span data-ttu-id="d3a92-330">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="d3a92-330">Select the search result.</span></span>
  * <span data-ttu-id="d3a92-331">Dans **Vntana** dossier rechercher la **accompagnent** actif.</span><span class="sxs-lookup"><span data-stu-id="d3a92-331">In **Holograms** folder find the **Tagalong** asset.</span></span>
  * <span data-ttu-id="d3a92-332">Sélectionnez le **ChestButton_Center** de l’objet dans le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d3a92-332">Select the **ChestButton_Center** object in the **Hierarchy**.</span></span> <span data-ttu-id="d3a92-333">Faites glisser et déposez le **accompagnent** à partir de l’objet le **projet** panneau sur le **inspecteur** dans le **objet à accompagnent** propriété.</span><span class="sxs-lookup"><span data-stu-id="d3a92-333">Drag and drop the **TagAlong** object from the **Project** panel onto the **Inspector** into the **Object To Tagalong** property.</span></span>
  * <span data-ttu-id="d3a92-334">Faites glisser le **accompagnent Action** à partir de l’objet le **inspecteur** dans le **Action Interactible** champ sur le **Interactible** script.</span><span class="sxs-lookup"><span data-stu-id="d3a92-334">Drag the **Tagalong Action** object from the **Inspector** into the **Interactible Action** field on the **Interactible** script.</span></span>
* <span data-ttu-id="d3a92-335">Double-cliquez sur le **TagalongAction** script pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3a92-335">Double click the **TagalongAction** script to open it in Visual Studio.</span></span>

![Configuration interactible](images/holograms210-interactible.png)

<span data-ttu-id="d3a92-337">Nous devons ajouter les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d3a92-337">We need to add the following:</span></span>

* <span data-ttu-id="d3a92-338">Ajouter des fonctionnalités à la fonction PerformAction dans le script TagalongAction (héritée de InteractibleAction).</span><span class="sxs-lookup"><span data-stu-id="d3a92-338">Add functionality to the PerformAction function in the TagalongAction script (inherited from InteractibleAction).</span></span>
* <span data-ttu-id="d3a92-339">Ajoutez le billboarding à l’objet gazed sur et la valeur de l’axe de tableau croisé dynamique XY.</span><span class="sxs-lookup"><span data-stu-id="d3a92-339">Add billboarding to the gazed-upon object, and set the pivot axis to XY.</span></span>
* <span data-ttu-id="d3a92-340">Ajoutez ensuite Tag-Along simple à l’objet.</span><span class="sxs-lookup"><span data-stu-id="d3a92-340">Then add simple Tag-Along to the object.</span></span>

<span data-ttu-id="d3a92-341">Voici notre solution, à partir de **TagalongAction.cs**:</span><span class="sxs-lookup"><span data-stu-id="d3a92-341">Here's our solution, from **TagalongAction.cs**:</span></span>

```cs
// Copyright (c) Microsoft Corporation. All rights reserved.
// Licensed under the MIT License. See LICENSE in the project root for license information.

using HoloToolkit.Unity;
using UnityEngine;

public class TagalongAction : InteractibleAction
{
    [SerializeField]
    [Tooltip("Drag the Tagalong prefab asset you want to display.")]
    private GameObject objectToTagalong;

    private void Awake()
    {
        if (objectToTagalong != null)
        {
            objectToTagalong = Instantiate(objectToTagalong);
            objectToTagalong.SetActive(false);

            /* TODO: DEVELOPER CODING EXERCISE 6.b */

            // 6.b: AddComponent Billboard to objectToTagAlong,
            // so it's always facing the user as they move.
            Billboard billboard = objectToTagalong.AddComponent<Billboard>();

            // 6.b: AddComponent SimpleTagalong to objectToTagAlong,
            // so it's always following the user as they move.
            objectToTagalong.AddComponent<SimpleTagalong>();

            // 6.b: Set any public properties you wish to experiment with.
            billboard.PivotAxis = PivotAxis.XY; // Already the default, but provided in case you want to edit
        }
    }

    public override void PerformAction()
    {
        // Recommend having only one tagalong.
        if (objectToTagalong == null || objectToTagalong.activeSelf)
        {
            return;
        }

        objectToTagalong.SetActive(true);
    }
}
```

* <span data-ttu-id="d3a92-342">Essayez !</span><span class="sxs-lookup"><span data-stu-id="d3a92-342">Try it!</span></span> <span data-ttu-id="d3a92-343">Générez et déployez l’application.</span><span class="sxs-lookup"><span data-stu-id="d3a92-343">Build and deploy the app.</span></span>
* <span data-ttu-id="d3a92-344">Regardez comment le contenu suit le centre du point du pointage de regard, mais pas en permanence et sans blocage.</span><span class="sxs-lookup"><span data-stu-id="d3a92-344">Watch how the content follows the center of the gaze point, but not continuously and without blocking it.</span></span>
