---
title: Entrée MR 210-point de regard
description: Suivez cette procédure pas à pas de codage avec Unity, Visual Studio et HoloLens pour apprendre les détails des concepts de regard.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, Academy, didacticiel, point de regard
ms.openlocfilehash: 076314389ec5ed70347c26d50c6a993f55da0758
ms.sourcegitcommit: aa88f6b42aa8d83e43104b78964afb506a368fb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/02/2019
ms.locfileid: "64993545"
---
>[!NOTE]
><span data-ttu-id="d8d87-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="d8d87-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="d8d87-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="d8d87-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="d8d87-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="d8d87-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="d8d87-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d8d87-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="d8d87-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="d8d87-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="d8d87-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="d8d87-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

# <a name="mr-input-210-gaze"></a><span data-ttu-id="d8d87-110">Monsieur 210: Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="d8d87-110">MR Input 210: Gaze</span></span>

<span data-ttu-id="d8d87-111">Le point de [regard](gaze.md) est la première forme d’entrée et révèle l’intention et la sensibilisation de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d8d87-111">[Gaze](gaze.md) is the first form of input and reveals the user's intent and awareness.</span></span> <span data-ttu-id="d8d87-112">Monsieur l’entrée 210 (également appelée l’Explorateur de projets) est une présentation approfondie des concepts liés au regard de Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="d8d87-112">MR Input 210 (aka Project Explorer) is a deep dive into gaze-related concepts for Windows Mixed Reality.</span></span> <span data-ttu-id="d8d87-113">Nous ajouterons une sensibilisation contextuelle à notre curseur et à vos hologrammes, en tirant pleinement parti de ce que votre application connaît sur le regard de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d8d87-113">We will be adding contextual awareness to our cursor and holograms, taking full advantage of what your app knows about the user's gaze.</span></span>

>[!VIDEO https://www.youtube.com/embed/yKAttGduVp0]

<span data-ttu-id="d8d87-114">Nous disposons d’un astronautes convivial pour vous aider à apprendre les concepts de regard.</span><span class="sxs-lookup"><span data-stu-id="d8d87-114">We have a friendly astronaut here to help you learn gaze concepts.</span></span> <span data-ttu-id="d8d87-115">Dans les [notions de base de m. 101](holograms-101.md), nous avions un curseur simple qui vient juste de vous faire suivre le regard.</span><span class="sxs-lookup"><span data-stu-id="d8d87-115">In [MR Basics 101](holograms-101.md), we had a simple cursor that just followed your gaze.</span></span> <span data-ttu-id="d8d87-116">Aujourd’hui, nous allons déplacer une étape au-delà du curseur simple:</span><span class="sxs-lookup"><span data-stu-id="d8d87-116">Today we're moving a step beyond the simple cursor:</span></span>

* <span data-ttu-id="d8d87-117">Nous faisons en sorte que le curseur et nos hologrammes soient orientés vers le regard: les deux varient en fonction de la position de l’utilisateur ou de l’endroit où l’utilisateur *ne cherche pas* .</span><span class="sxs-lookup"><span data-stu-id="d8d87-117">We're making the cursor and our holograms gaze-aware: both will change based on where the user is looking - or where the user is *not* looking.</span></span> <span data-ttu-id="d8d87-118">Cela les rend compatibles avec le contexte.</span><span class="sxs-lookup"><span data-stu-id="d8d87-118">This makes them context-aware.</span></span>
* <span data-ttu-id="d8d87-119">Nous ajouterons des commentaires à notre curseur et à vos hologrammes pour fournir à l’utilisateur davantage de contexte sur ce qui est ciblé.</span><span class="sxs-lookup"><span data-stu-id="d8d87-119">We will add feedback to our cursor and holograms to give the user more context on what is being targeted.</span></span> <span data-ttu-id="d8d87-120">Ce feedback peut être audio et visuel.</span><span class="sxs-lookup"><span data-stu-id="d8d87-120">This feedback can be audio and visual.</span></span>
* <span data-ttu-id="d8d87-121">Nous allons vous montrer comment cibler des techniques pour aider les utilisateurs à atteindre des cibles plus petites.</span><span class="sxs-lookup"><span data-stu-id="d8d87-121">We'll show you targeting techniques to help users hit smaller targets.</span></span>
* <span data-ttu-id="d8d87-122">Nous allons vous montrer comment attirer l’attention de l’utilisateur sur vos hologrammes à l’aide d’un indicateur directionnel.</span><span class="sxs-lookup"><span data-stu-id="d8d87-122">We'll show you how to draw the user's attention to your holograms with a directional indicator.</span></span>
* <span data-ttu-id="d8d87-123">Nous vous enseignerons les techniques permettant de faire passer vos hologrammes à l’utilisateur lorsqu’il se déplace dans votre monde.</span><span class="sxs-lookup"><span data-stu-id="d8d87-123">We'll teach you techniques to take your holograms with the user as she moves around in your world.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d8d87-124">Les vidéos incorporées dans chacun des chapitres ci-dessous ont été enregistrées à l’aide d’une version antérieure d’Unity et de la réalité mixte Toolkit.</span><span class="sxs-lookup"><span data-stu-id="d8d87-124">The videos embedded in each of the chapters below were recorded using an older version of Unity and the Mixed Reality Toolkit.</span></span> <span data-ttu-id="d8d87-125">Alors que les instructions pas à pas sont précises et actuelles, vous pouvez voir des scripts et des visuels dans les vidéos correspondantes qui sont obsolètes.</span><span class="sxs-lookup"><span data-stu-id="d8d87-125">While the step-by-step instructions are accurate and current, you may see scripts and visuals in the corresponding videos that are out-of-date.</span></span> <span data-ttu-id="d8d87-126">Les vidéos restent incluses pour l’affiche et les concepts abordés s’appliquent toujours.</span><span class="sxs-lookup"><span data-stu-id="d8d87-126">The videos remain included for posterity and because the concepts covered still apply.</span></span>

## <a name="device-support"></a><span data-ttu-id="d8d87-127">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="d8d87-127">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="d8d87-128">Course</span><span class="sxs-lookup"><span data-stu-id="d8d87-128">Course</span></span></th><th style="width:150px"> <span data-ttu-id="d8d87-129"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="d8d87-129"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="d8d87-130"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="d8d87-130"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="d8d87-131">Monsieur 210: Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="d8d87-131">MR Input 210: Gaze</span></span></td><td style="text-align: center;"> <span data-ttu-id="d8d87-132">✔️</span><span class="sxs-lookup"><span data-stu-id="d8d87-132">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="d8d87-133">✔️</span><span class="sxs-lookup"><span data-stu-id="d8d87-133">✔️</span></span></td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="d8d87-134">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d8d87-134">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d8d87-135">Prérequis</span><span class="sxs-lookup"><span data-stu-id="d8d87-135">Prerequisites</span></span>

* <span data-ttu-id="d8d87-136">Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="d8d87-136">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="d8d87-137">Certaines fonctionnalités C# de programmation de base.</span><span class="sxs-lookup"><span data-stu-id="d8d87-137">Some basic C# programming ability.</span></span>
* <span data-ttu-id="d8d87-138">Vous devez avoir terminé les [notions de base de m. 101](holograms-101.md).</span><span class="sxs-lookup"><span data-stu-id="d8d87-138">You should have completed [MR Basics 101](holograms-101.md).</span></span>
* <span data-ttu-id="d8d87-139">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="d8d87-139">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="d8d87-140">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="d8d87-140">Project files</span></span>

* <span data-ttu-id="d8d87-141">Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-210-Gaze.zip) requis par le projet.</span><span class="sxs-lookup"><span data-stu-id="d8d87-141">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-210-Gaze.zip) required by the project.</span></span><span data-ttu-id="d8d87-142"> Requiert Unity 2017,2 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d8d87-142"> Requires Unity 2017.2 or later.</span></span>
* <span data-ttu-id="d8d87-143">Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.</span><span class="sxs-lookup"><span data-stu-id="d8d87-143">Un-archive the files to your desktop or other easy to reach location.</span></span>

>[!NOTE]
><span data-ttu-id="d8d87-144">Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-210-Gaze).</span><span class="sxs-lookup"><span data-stu-id="d8d87-144">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-210-Gaze).</span></span>

### <a name="errata-and-notes"></a><span data-ttu-id="d8d87-145">Errata et notes</span><span class="sxs-lookup"><span data-stu-id="d8d87-145">Errata and Notes</span></span>

* <span data-ttu-id="d8d87-146">Dans Visual Studio, l’option «Uniquement mon code» doit être désactivée (décochée) sous Outils-> Options-> le débogage pour atteindre les points d’arrêt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="d8d87-146">In Visual Studio, "Just My Code" needs to be disabled (unchecked) under Tools->Options->Debugging in order to hit breakpoints in your code.</span></span>

## <a name="chapter-1---unity-setup"></a><span data-ttu-id="d8d87-147">Chapitre 1-Configuration Unity</span><span class="sxs-lookup"><span data-stu-id="d8d87-147">Chapter 1 - Unity Setup</span></span>

>[!VIDEO https://www.youtube.com/embed/_Ccn6riQ6vU]

### <a name="objectives"></a><span data-ttu-id="d8d87-148">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d8d87-148">Objectives</span></span>

* <span data-ttu-id="d8d87-149">Optimiser Unity pour le développement HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d8d87-149">Optimize Unity for HoloLens development.</span></span>
* <span data-ttu-id="d8d87-150">Importer les ressources et configurer la scène.</span><span class="sxs-lookup"><span data-stu-id="d8d87-150">Import assets and setup the scene.</span></span>
* <span data-ttu-id="d8d87-151">Affichez le astronautes dans HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d8d87-151">View the astronaut in the HoloLens.</span></span>

### <a name="instructions"></a><span data-ttu-id="d8d87-152">Instructions</span><span class="sxs-lookup"><span data-stu-id="d8d87-152">Instructions</span></span>

1. <span data-ttu-id="d8d87-153">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="d8d87-153">Start Unity.</span></span>
2. <span data-ttu-id="d8d87-154">Sélectionnez **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-154">Select **New Project**.</span></span>
3. <span data-ttu-id="d8d87-155">Nommez le projet **ModelExplorer**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-155">Name the project **ModelExplorer**.</span></span>
4. <span data-ttu-id="d8d87-156">Entrez **l’emplacement** du dossier de pointage que vous avez précédemment désinstallé.</span><span class="sxs-lookup"><span data-stu-id="d8d87-156">Enter location as the **Gaze** folder you previously un-archived.</span></span>
5. <span data-ttu-id="d8d87-157">Vérifiez que le projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-157">Make sure the project is set to **3D**.</span></span>
6. <span data-ttu-id="d8d87-158">Cliquez sur **Create Project**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-158">Click **Create Project**.</span></span>

### <a name="unity-settings-for-hololens"></a><span data-ttu-id="d8d87-159">Paramètres Unity pour HoloLens</span><span class="sxs-lookup"><span data-stu-id="d8d87-159">Unity settings for HoloLens</span></span>

<span data-ttu-id="d8d87-160">Nous devons permettre à Unity de savoir que l’application que nous essayons d’exporter doit créer une [vue immersive](app-views.md) au lieu d’une vue 2D.</span><span class="sxs-lookup"><span data-stu-id="d8d87-160">We need to let Unity know that the app we are trying to export should create an [immersive view](app-views.md) instead of a 2D view.</span></span> <span data-ttu-id="d8d87-161">Pour cela, nous ajoutons HoloLens en tant qu’appareil de réalité virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d8d87-161">We do that by adding HoloLens as a virtual reality device.</span></span>

1. <span data-ttu-id="d8d87-162">Accédez à **modifier > paramètres du projet > Player**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-162">Go to **Edit > Project Settings > Player**.</span></span>
2. <span data-ttu-id="d8d87-163">Dans le **panneau Inspecteur** pour les paramètres du lecteur, sélectionnez l’icône du **Windows Store** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-163">In the **Inspector Panel** for Player Settings, select the **Windows Store** icon.</span></span>
3. <span data-ttu-id="d8d87-164">Développez le groupe de **paramètres XR** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-164">Expand the **XR Settings** group.</span></span>
4. <span data-ttu-id="d8d87-165">Dans la section **rendu** , activez la case à cocher **réalité virtuelle prise en charge** pour ajouter une nouvelle liste de **SDK de réalité virtuelle** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-165">In the **Rendering** section, check the **Virtual Reality Supported** checkbox to add a new **Virtual Reality SDKs** list.</span></span>
5. <span data-ttu-id="d8d87-166">Vérifiez que **Windows Mixed Reality** s’affiche dans la liste.</span><span class="sxs-lookup"><span data-stu-id="d8d87-166">Verify that **Windows Mixed Reality** appears in the list.</span></span> <span data-ttu-id="d8d87-167">Si ce n’est pas **+** le cas, sélectionnez le bouton en bas de la liste et choisissez **Windows holographique**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-167">If not, select the **+** button at the bottom of the list and choose **Windows Holographic**.</span></span>

<span data-ttu-id="d8d87-168">Ensuite, nous devons définir notre backend de script sur .NET.</span><span class="sxs-lookup"><span data-stu-id="d8d87-168">Next, we need to set our scripting backend to .NET.</span></span>

1. <span data-ttu-id="d8d87-169">Accédez à **modifier > paramètres du projet > Player** (vous pouvez toujours le faire à l’étape précédente).</span><span class="sxs-lookup"><span data-stu-id="d8d87-169">Go to **Edit > Project Settings > Player** (you may still have this up from the previous step).</span></span>
2. <span data-ttu-id="d8d87-170">Dans le **panneau Inspecteur** pour les paramètres du lecteur, sélectionnez l’icône du **Windows Store** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-170">In the **Inspector Panel** for Player Settings, select the **Windows Store** icon.</span></span>
3. <span data-ttu-id="d8d87-171">Dans la section configuration **des autres paramètres** , assurez-vous que le **serveur principal de script** est défini sur **.net**</span><span class="sxs-lookup"><span data-stu-id="d8d87-171">In the **Other Settings** Configuration section, make sure that **Scripting Backend** is set to **.NET**</span></span>

<span data-ttu-id="d8d87-172">Enfin, nous mettrons à jour nos paramètres de qualité pour obtenir des performances rapides sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d8d87-172">Finally, we'll update our quality settings to achieve a fast performance on HoloLens.</span></span>

1. <span data-ttu-id="d8d87-173">Accédez à **modifier > paramètres du projet > qualité**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-173">Go to **Edit > Project Settings > Quality**.</span></span>
2. <span data-ttu-id="d8d87-174">Cliquez sur la flèche pointant vers le bas dans la ligne **par défaut** sous l’icône Windows Store.</span><span class="sxs-lookup"><span data-stu-id="d8d87-174">Click on downward pointing arrow in the **Default** row under the Windows Store icon.</span></span>
3. <span data-ttu-id="d8d87-175">Sélectionnez **très faible** pour les **applications du Windows Store**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-175">Select **Very Low** for **Windows Store Apps**.</span></span>

### <a name="import-project-assets"></a><span data-ttu-id="d8d87-176">Importer des ressources de projet</span><span class="sxs-lookup"><span data-stu-id="d8d87-176">Import project assets</span></span>

1. <span data-ttu-id="d8d87-177">Cliquez avec le bouton droit sur le dossier **ressources** dans le panneau **projet** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-177">Right click the **Assets** folder in the **Project** panel.</span></span>
2. <span data-ttu-id="d8d87-178">Cliquez sur **Importer un package > package personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-178">Click on **Import Package > Custom Package**.</span></span>
3. <span data-ttu-id="d8d87-179">Accédez aux fichiers de projet que vous avez téléchargés, puis cliquez sur **ModelExplorer. pour Unity**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-179">Navigate to the project files you downloaded and click on **ModelExplorer.unitypackage**.</span></span>
4. <span data-ttu-id="d8d87-180">Cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-180">Click **Open**.</span></span>
5. <span data-ttu-id="d8d87-181">Une fois le package chargé, cliquez sur le bouton **Importer** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-181">After the package loads, click on the **Import** button.</span></span>

### <a name="setup-the-scene"></a><span data-ttu-id="d8d87-182">Configurer la scène</span><span class="sxs-lookup"><span data-stu-id="d8d87-182">Setup the scene</span></span>

1. <span data-ttu-id="d8d87-183">Dans la hiérarchie, supprimez l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-183">In the Hierarchy, delete the **Main Camera**.</span></span>
2. <span data-ttu-id="d8d87-184">Dans le dossier **HoloToolkit** , ouvrez le dossier **d’entrée** , puis ouvrez le dossier **Prefabs** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-184">In the **HoloToolkit** folder, open the **Input** folder, then open the **Prefabs** folder.</span></span>
3. <span data-ttu-id="d8d87-185">Faites glisser et déposez le Prefab **MixedRealityCameraParent** à partir du dossier **Prefabs** dans la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-185">Drag and drop the **MixedRealityCameraParent** prefab from the **Prefabs** folder into the **Hierarchy**.</span></span>
4. <span data-ttu-id="d8d87-186">Cliquez avec le bouton droit sur la **lumière directionnelle** dans la hiérarchie et sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-186">Right-click the **Directional Light** in the Hierarchy and select **Delete**.</span></span>
5. <span data-ttu-id="d8d87-187">Dans le  dossier hologrammes, glissez-déposez les éléments suivants à la racine de la **hiérarchie**:</span><span class="sxs-lookup"><span data-stu-id="d8d87-187">In the **Holograms** folder, drag and drop the following assets into the root of the **Hierarchy**:</span></span>
    * <span data-ttu-id="d8d87-188">**AstroMan**</span><span class="sxs-lookup"><span data-stu-id="d8d87-188">**AstroMan**</span></span>
    * <span data-ttu-id="d8d87-189">**Lampes**</span><span class="sxs-lookup"><span data-stu-id="d8d87-189">**Lights**</span></span>
    * <span data-ttu-id="d8d87-190">**SpaceAudioSource**</span><span class="sxs-lookup"><span data-stu-id="d8d87-190">**SpaceAudioSource**</span></span>
    * <span data-ttu-id="d8d87-191">**SpaceBackground**</span><span class="sxs-lookup"><span data-stu-id="d8d87-191">**SpaceBackground**</span></span>
6. <span data-ttu-id="d8d87-192">Démarrez le **mode lecture** ▶ pour afficher le astronautes.</span><span class="sxs-lookup"><span data-stu-id="d8d87-192">Start **Play Mode** ▶ to view the astronaut.</span></span>
7. <span data-ttu-id="d8d87-193">Cliquez à nouveau sur **mode lecture** ▶ pour **arrêter**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-193">Click **Play Mode** ▶ again to **Stop**.</span></span>
8. <span data-ttu-id="d8d87-194">Dans le  dossier hologrammes, recherchez la ressource **Fitbox** et faites-la glisser jusqu’à la racine de la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-194">In the **Holograms** folder, find the **Fitbox** asset and drag it to the root of the **Hierarchy**.</span></span>
9. <span data-ttu-id="d8d87-195">Sélectionnez le **Fitbox** dans le volet de la **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-195">Select the **Fitbox** in the **Hierarchy** panel.</span></span>
10. <span data-ttu-id="d8d87-196">Faites glisser la collection **AstroMan** de la **hiérarchie** vers la propriété de **collection hologramme** du Fitbox dans le panneau **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-196">Drag the **AstroMan** collection from the **Hierarchy** to the **Hologram Collection** property of the Fitbox in the **Inspector** panel.</span></span>

### <a name="save-the-project"></a><span data-ttu-id="d8d87-197">Enregistrer le projet</span><span class="sxs-lookup"><span data-stu-id="d8d87-197">Save the project</span></span>

1. <span data-ttu-id="d8d87-198">Enregistrez la nouvelle scène: **Fichier > enregistrer la scène sous**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-198">Save the new scene: **File > Save Scene As**.</span></span>
2. <span data-ttu-id="d8d87-199">Cliquez sur **nouveau dossier** et nommez le dossier Scenes.</span><span class="sxs-lookup"><span data-stu-id="d8d87-199">Click **New Folder** and name the folder **Scenes**.</span></span>
3. <span data-ttu-id="d8d87-200">Nommez le fichier «**ModelExplorer**» et enregistrez-le dans le dossier **scenes** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-200">Name the file “**ModelExplorer**” and save it in the **Scenes** folder.</span></span>

### <a name="build-the-project"></a><span data-ttu-id="d8d87-201">Créer le projet</span><span class="sxs-lookup"><span data-stu-id="d8d87-201">Build the project</span></span>

1. <span data-ttu-id="d8d87-202">Dans Unity, sélectionnez **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-202">In Unity, select **File > Build Settings**.</span></span>
2. <span data-ttu-id="d8d87-203">Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="d8d87-203">Click **Add Open Scenes** to add the scene.</span></span>
3. <span data-ttu-id="d8d87-204">Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur basculer la **plateforme**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-204">Select **Universal Windows Platform** in the **Platform** list and click **Switch Platform**.</span></span>
4. <span data-ttu-id="d8d87-205">Si vous développez spécifiquement pour HoloLens, définissez **appareil cible** sur **hololens**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-205">If you're specifically developing for HoloLens, set **Target device** to **HoloLens**.</span></span> <span data-ttu-id="d8d87-206">Dans le cas contraire, laissez-le sur **un appareil**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-206">Otherwise, leave it on **Any device**.</span></span>
5. <span data-ttu-id="d8d87-207">Vérifiez que le **type de build** est défini sur **D3D** et que le **Kit de développement logiciel (SDK** ) est défini sur le **dernier installé** (qui doit être le SDK 16299 ou une version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="d8d87-207">Ensure **Build Type** is set to **D3D** and **SDK** is set to **Latest installed** (which should be SDK 16299 or newer).</span></span>
6. <span data-ttu-id="d8d87-208">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-208">Click **Build**.</span></span>
7. <span data-ttu-id="d8d87-209">Créez un **dossier** nommé «App».</span><span class="sxs-lookup"><span data-stu-id="d8d87-209">Create a **New Folder** named "App".</span></span>
8. <span data-ttu-id="d8d87-210">Cliquez sur le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-210">Single click the **App** folder.</span></span>
9. <span data-ttu-id="d8d87-211">Appuyez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-211">Press **Select Folder**.</span></span>

<span data-ttu-id="d8d87-212">Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d8d87-212">When Unity is done, a File Explorer window will appear.</span></span>

1. <span data-ttu-id="d8d87-213">Ouvrez le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-213">Open the **App** folder.</span></span>
2. <span data-ttu-id="d8d87-214">Ouvrez la **solution Visual Studio ModelExplorer**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-214">Open the **ModelExplorer Visual Studio Solution**.</span></span>

<span data-ttu-id="d8d87-215">En cas de déploiement dans HoloLens:</span><span class="sxs-lookup"><span data-stu-id="d8d87-215">If deploying to HoloLens:</span></span>

1. <span data-ttu-id="d8d87-216">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-216">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x86**.</span></span>
2. <span data-ttu-id="d8d87-217">Cliquez sur la flèche déroulante en regard du bouton ordinateur local, puis sélectionnez **ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-217">Click on the drop down arrow next to the Local Machine button, and select **Remote Machine**.</span></span>
3. <span data-ttu-id="d8d87-218">Entrez **l’adresse IP de votre appareil HoloLens** et définissez le mode d’authentification sur **universel (protocole non chiffré)** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-218">Enter **your HoloLens device IP address** and set Authentication Mode to **Universal (Unencrypted Protocol)**.</span></span> <span data-ttu-id="d8d87-219">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-219">Click **Select**.</span></span> <span data-ttu-id="d8d87-220">Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-220">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options**.</span></span>
4. <span data-ttu-id="d8d87-221">Dans la barre de menus supérieure, cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-221">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="d8d87-222">S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le coupler à [Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span><span class="sxs-lookup"><span data-stu-id="d8d87-222">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span></span>
5. <span data-ttu-id="d8d87-223">Une fois l’application déployée, ignorez le **Fitbox** avec un **mouvement Select**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-223">When the app has deployed, dismiss the **Fitbox** with a **select gesture**.</span></span>

<span data-ttu-id="d8d87-224">En cas de déploiement sur un casque immersif:</span><span class="sxs-lookup"><span data-stu-id="d8d87-224">If deploying to an immersive headset:</span></span>

1. <span data-ttu-id="d8d87-225">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x64**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-225">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x64**.</span></span>
2. <span data-ttu-id="d8d87-226">Assurez-vous que la cible de déploiement est définie sur **ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-226">Make sure the deployment target is set to **Local Machine**.</span></span>
3. <span data-ttu-id="d8d87-227">Dans la barre de menus supérieure, cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-227">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
4. <span data-ttu-id="d8d87-228">Une fois l’application déployée, Faites disparaître le **Fitbox** en tirant le déclencheur sur un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="d8d87-228">When the app has deployed, dismiss the **Fitbox** by pulling the trigger on a motion controller.</span></span>

## <a name="chapter-2---cursor-and-target-feedback"></a><span data-ttu-id="d8d87-229">Chapitre 2-commentaires sur les curseurs et les cibles</span><span class="sxs-lookup"><span data-stu-id="d8d87-229">Chapter 2 - Cursor and target feedback</span></span>

>[!VIDEO https://www.youtube.com/embed/S24u0V_T7ZI]

### <a name="objectives"></a><span data-ttu-id="d8d87-230">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d8d87-230">Objectives</span></span>

* <span data-ttu-id="d8d87-231">Conception visuelle et comportement des curseurs.</span><span class="sxs-lookup"><span data-stu-id="d8d87-231">Cursor visual design and behavior.</span></span>
* <span data-ttu-id="d8d87-232">Commentaires sur le curseur orienté vers le regard.</span><span class="sxs-lookup"><span data-stu-id="d8d87-232">Gaze-based cursor feedback.</span></span>
* <span data-ttu-id="d8d87-233">Commentaires sur l’hologramme en regard.</span><span class="sxs-lookup"><span data-stu-id="d8d87-233">Gaze-based hologram feedback.</span></span>

<span data-ttu-id="d8d87-234">Nous allons baser notre travail sur certains principes de conception de curseur, à savoir:</span><span class="sxs-lookup"><span data-stu-id="d8d87-234">We're going to base our work on some cursor design principles, namely:</span></span>

* <span data-ttu-id="d8d87-235">Le curseur est toujours présent.</span><span class="sxs-lookup"><span data-stu-id="d8d87-235">The cursor is always present.</span></span>
* <span data-ttu-id="d8d87-236">Ne laissez pas le curseur devenir trop petit ou grand.</span><span class="sxs-lookup"><span data-stu-id="d8d87-236">Don't let the cursor get too small or big.</span></span>
* <span data-ttu-id="d8d87-237">Évitez d’obstruer le contenu.</span><span class="sxs-lookup"><span data-stu-id="d8d87-237">Avoid obstructing content.</span></span>

### <a name="instructions"></a><span data-ttu-id="d8d87-238">Instructions</span><span class="sxs-lookup"><span data-stu-id="d8d87-238">Instructions</span></span>

1. <span data-ttu-id="d8d87-239">Dans le dossier **HoloToolkit\Input\Prefabs** , recherchez la ressource **InputManager** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-239">In the **HoloToolkit\Input\Prefabs** folder, find the **InputManager** asset.</span></span>
2. <span data-ttu-id="d8d87-240">Glissez-déplacez le **InputManager** sur la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-240">Drag and drop the **InputManager** onto the **Hierarchy**.</span></span>
3. <span data-ttu-id="d8d87-241">Dans le dossier **HoloToolkit\Input\Prefabs** , recherchez la ressource **curseur** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-241">In the **HoloToolkit\Input\Prefabs** folder, find the **Cursor** asset.</span></span>
4. <span data-ttu-id="d8d87-242">Glissez-déposez le **curseur** sur la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-242">Drag and drop the **Cursor** onto the **Hierarchy**.</span></span>
5. <span data-ttu-id="d8d87-243">Sélectionnez l’objet **InputManager** dans la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-243">Select the **InputManager** object in the **Hierarchy**.</span></span>
6. <span data-ttu-id="d8d87-244">Faites glisser l’objet **Cursor** de la **hiérarchie** vers le champ **Cursor** du **SimpleSinglePointerSelector**de InputManager, en bas de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-244">Drag the **Cursor** object from the **Hierarchy** into the InputManager's **SimpleSinglePointerSelector**'s **Cursor** field, at the bottom of the **Inspector**.</span></span>

![Configuration du sélecteur de pointeur simple simple](images/holograms210-ssps.png)

### <a name="build-and-deploy"></a><span data-ttu-id="d8d87-246">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="d8d87-246">Build and Deploy</span></span>

1. <span data-ttu-id="d8d87-247">Régénérez l’application à partir du **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-247">Rebuild the app from **File > Build Settings**.</span></span>
2. <span data-ttu-id="d8d87-248">Ouvrez le **dossier**de l’application.</span><span class="sxs-lookup"><span data-stu-id="d8d87-248">Open the **App folder**.</span></span>
3. <span data-ttu-id="d8d87-249">Ouvrez la **solution Visual Studio ModelExplorer**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-249">Open the **ModelExplorer Visual Studio Solution**.</span></span>
4. <span data-ttu-id="d8d87-250">Cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-250">Click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
5. <span data-ttu-id="d8d87-251">Observez comment le curseur est dessiné et comment il change d’apparence s’il touche un hologramme.</span><span class="sxs-lookup"><span data-stu-id="d8d87-251">Observe how the cursor is drawn, and how it changes appearance if it is touching a hologram.</span></span>

### <a name="instructions"></a><span data-ttu-id="d8d87-252">Instructions</span><span class="sxs-lookup"><span data-stu-id="d8d87-252">Instructions</span></span>

1. <span data-ttu-id="d8d87-253">Dans le volet **hiérarchie** , développez l’objet **AstroMan**->**GEO_G**->**Back_Center** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-253">In the **Hierarchy** panel, expand the **AstroMan**->**GEO_G**->**Back_Center** object.</span></span>
2. <span data-ttu-id="d8d87-254">Double-cliquez sur **Interactible.cs** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8d87-254">Double click on **Interactible.cs** to open it in Visual Studio.</span></span>
3. <span data-ttu-id="d8d87-255">Supprimez les marques de commentaire des lignes dans les rappels **IFocusable. OnFocusEnter ()** et **IFocusable. OnFocusExit ()** dans **Interactible.cs**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-255">Uncomment the lines in the **IFocusable.OnFocusEnter()** and **IFocusable.OnFocusExit()** callbacks in **Interactible.cs**.</span></span> <span data-ttu-id="d8d87-256">Celles-ci sont appelées par le InputManager du Toolkit de la réalité mixte lorsque le focus (soit par le point de présence ou par le contrôleur pointant) entre et quitte le conflit du GameObject spécifique.</span><span class="sxs-lookup"><span data-stu-id="d8d87-256">These are called by the Mixed Reality Toolkit's InputManager when focus (either by gaze or by controller pointing) enters and exits the specific GameObject's collider.</span></span>

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
><span data-ttu-id="d8d87-257">Nous utilisons `DisableKeyword` et versions ultérieures. `EnableKeyword`</span><span class="sxs-lookup"><span data-stu-id="d8d87-257">We use `EnableKeyword` and `DisableKeyword` above.</span></span> <span data-ttu-id="d8d87-258">Pour pouvoir les utiliser dans votre propre application avec le nuanceur standard du kit de ressources, vous devez suivre les [instructions Unity pour accéder aux documents par le biais](https://docs.unity3d.com/Manual/MaterialsAccessingViaScript.html)d’un script.</span><span class="sxs-lookup"><span data-stu-id="d8d87-258">In order to make use of these in your own app with the Toolkit's Standard shader, you'll need to follow the [Unity guidelines for accessing materials via script](https://docs.unity3d.com/Manual/MaterialsAccessingViaScript.html).</span></span> <span data-ttu-id="d8d87-259">Dans ce cas, nous avons déjà inclus les [trois variantes de matériel mis](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-210-Gaze/Completed/ModelExplorer/Assets/Resources/Models/AstroMan/Materials) en surbrillance nécessaires dans le dossier ressources (recherchez les trois éléments avec la mise en surbrillance dans le nom).</span><span class="sxs-lookup"><span data-stu-id="d8d87-259">In this case, we've already included the [three variants of highlighted material](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-210-Gaze/Completed/ModelExplorer/Assets/Resources/Models/AstroMan/Materials) needed in the Resources folder (look for the three materials with highlight in the name).</span></span>

### <a name="build-and-deploy"></a><span data-ttu-id="d8d87-260">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="d8d87-260">Build and Deploy</span></span>

1. <span data-ttu-id="d8d87-261">Comme précédemment, générez le projet et déployez sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d8d87-261">As before, build the project and deploy to the HoloLens.</span></span>
2. <span data-ttu-id="d8d87-262">Observez ce qui se passe quand le point de regard est destiné à un objet et lorsqu’il ne l’est pas.</span><span class="sxs-lookup"><span data-stu-id="d8d87-262">Observe what happens when the gaze is aimed at an object and when it's not.</span></span>

## <a name="chapter-3---targeting-techniques"></a><span data-ttu-id="d8d87-263">Chapitre 3-techniques de ciblage</span><span class="sxs-lookup"><span data-stu-id="d8d87-263">Chapter 3 - Targeting Techniques</span></span>

>[!VIDEO https://www.youtube.com/embed/TFnuLva4VJ0]

### <a name="objectives"></a><span data-ttu-id="d8d87-264">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d8d87-264">Objectives</span></span>

* <span data-ttu-id="d8d87-265">Facilitez la cible des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d8d87-265">Make it easier to target holograms.</span></span>
* <span data-ttu-id="d8d87-266">Stabiliser les mouvements des têtes naturelles.</span><span class="sxs-lookup"><span data-stu-id="d8d87-266">Stabilize natural head movements.</span></span>

### <a name="instructions"></a><span data-ttu-id="d8d87-267">Instructions</span><span class="sxs-lookup"><span data-stu-id="d8d87-267">Instructions</span></span>

1. <span data-ttu-id="d8d87-268">Dans le volet **hiérarchie** , sélectionnez l’objet **InputManager** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-268">In the **Hierarchy** panel, select the **InputManager** object.</span></span>
2. <span data-ttu-id="d8d87-269">Dans le volet de l' **inspecteur** , recherchez le script de **stabilisation du regard** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-269">In the **Inspector** panel, find the **Gaze Stabilizer** script.</span></span> <span data-ttu-id="d8d87-270">Cliquez dessus pour l’ouvrir dans Visual Studio, si vous souhaitez jeter un coup d’œil.</span><span class="sxs-lookup"><span data-stu-id="d8d87-270">Click it to open in Visual Studio, if you want to take a look.</span></span>
    * <span data-ttu-id="d8d87-271">Ce script itère sur des exemples de données Raycast et permet de stabiliser le regard de la précision de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d8d87-271">This script iterates over samples of Raycast data and helps stabilize the user's gaze for precision targeting.</span></span>
3. <span data-ttu-id="d8d87-272">Dans l' **inspecteur**, vous pouvez modifier la valeur des **exemples de stabilité stockés** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-272">In the **Inspector**, you can edit the **Stored Stability Samples** value.</span></span> <span data-ttu-id="d8d87-273">Cette valeur représente le nombre d’échantillons sur lesquels le stabilisateur effectue une itération pour calculer la valeur stabilisée.</span><span class="sxs-lookup"><span data-stu-id="d8d87-273">This value represents the number of samples that the stabilizer iterates on to calculate the stabilized value.</span></span>

## <a name="chapter-4---directional-indicator"></a><span data-ttu-id="d8d87-274">Chapitre 4-indicateur directionnel</span><span class="sxs-lookup"><span data-stu-id="d8d87-274">Chapter 4 - Directional indicator</span></span>

>[!VIDEO https://www.youtube.com/embed/htVbJCMlj64]

### <a name="objectives"></a><span data-ttu-id="d8d87-275">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d8d87-275">Objectives</span></span>

* <span data-ttu-id="d8d87-276">Ajoutez un indicateur directionnel sur le curseur pour faciliter la recherche des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d8d87-276">Add a directional indicator on the cursor to help find holograms.</span></span>

### <a name="instructions"></a><span data-ttu-id="d8d87-277">Instructions</span><span class="sxs-lookup"><span data-stu-id="d8d87-277">Instructions</span></span>

<span data-ttu-id="d8d87-278">Nous allons utiliser le fichier **DirectionIndicator.cs** , qui:</span><span class="sxs-lookup"><span data-stu-id="d8d87-278">We're going to use the **DirectionIndicator.cs** file which will:</span></span>

1. <span data-ttu-id="d8d87-279">Affichez l’indicateur directionnel si l’utilisateur n’est pas Gazing sur les hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d8d87-279">Show the directional indicator if the user is not gazing at the holograms.</span></span>
2. <span data-ttu-id="d8d87-280">Masquer l’indicateur directionnel si l’utilisateur est Gazing sur les hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d8d87-280">Hide the directional indicator if the user is gazing at the holograms.</span></span>
3. <span data-ttu-id="d8d87-281">Mettez à jour l’indicateur directionnel pour pointer vers les hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d8d87-281">Update the directional indicator to point to the holograms.</span></span>

<span data-ttu-id="d8d87-282">Commençons.</span><span class="sxs-lookup"><span data-stu-id="d8d87-282">Let's get started.</span></span>

1. <span data-ttu-id="d8d87-283">Cliquez sur l’objet **AstroMan** dans le volet de **hiérarchie** , puis **cliquez sur la flèche pour le** développer.</span><span class="sxs-lookup"><span data-stu-id="d8d87-283">Click on the **AstroMan** object in the **Hierarchy** panel and **click the arrow** to expand it.</span></span>
2. <span data-ttu-id="d8d87-284">Dans le volet **hiérarchie** , sélectionnez l’objet **DirectionalIndicator** sous **AstroMan**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-284">In the **Hierarchy** panel, select the **DirectionalIndicator** object under **AstroMan**.</span></span>
3. <span data-ttu-id="d8d87-285">Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-285">In the **Inspector** panel, click the **Add Component** button.</span></span>
4. <span data-ttu-id="d8d87-286">Dans le menu, tapez dans l’indicateur de **direction**de la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="d8d87-286">In the menu, type in the search box **Direction Indicator**.</span></span> <span data-ttu-id="d8d87-287">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="d8d87-287">Select the search result.</span></span>
5. <span data-ttu-id="d8d87-288">Dans le volet **hiérarchie** , faites glisser et déposez l’objet **Cursor** sur la propriété **Cursor** de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-288">In the **Hierarchy** panel, drag and drop the **Cursor** object onto the **Cursor** property in the **Inspector**.</span></span>
6. <span data-ttu-id="d8d87-289">Dans le panneau **projet** , dans le **dossier hologrammes** , faites glisser et déposez l’élément **DirectionalIndicator** sur la propriété **indicateur directionnel** de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-289">In the **Project** panel, in the **Holograms** folder, drag and drop the **DirectionalIndicator** asset onto the **Directional Indicator** property in the **Inspector**.</span></span>
7. <span data-ttu-id="d8d87-290">Générez et déployez l’application.</span><span class="sxs-lookup"><span data-stu-id="d8d87-290">Build and deploy the app.</span></span>
8. <span data-ttu-id="d8d87-291">Regardez comment l’objet indicateur directionnel vous aide à trouver le astronautes.</span><span class="sxs-lookup"><span data-stu-id="d8d87-291">Watch how the directional indicator object helps you find the astronaut.</span></span>

## <a name="chapter-5---billboarding"></a><span data-ttu-id="d8d87-292">Chapitre 5-panneaux</span><span class="sxs-lookup"><span data-stu-id="d8d87-292">Chapter 5 - Billboarding</span></span>

>[!VIDEO https://www.youtube.com/embed/qFiLr_LUACE]

### <a name="objectives"></a><span data-ttu-id="d8d87-293">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d8d87-293">Objectives</span></span>

* <span data-ttu-id="d8d87-294">Utilisez le billboarding pour que les hologrammes soient toujours face à vous.</span><span class="sxs-lookup"><span data-stu-id="d8d87-294">Use billboarding to have holograms always face towards you.</span></span>

<span data-ttu-id="d8d87-295">Nous utiliserons le fichier **Billboard.cs** pour garder un gameobject orienté de manière à ce qu’il soit à tout moment destiné à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d8d87-295">We will be using the **Billboard.cs** file to keep a GameObject oriented such that it is facing the user at all times.</span></span>

1. <span data-ttu-id="d8d87-296">Dans le volet **hiérarchie** , sélectionnez l’objet **AstroMan** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-296">In the **Hierarchy** panel, select the **AstroMan** object.</span></span>
2. <span data-ttu-id="d8d87-297">Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-297">In the **Inspector** panel, click the **Add Component** button.</span></span>
3. <span data-ttu-id="d8d87-298">Dans le menu, tapez dans le **panneau**d’interzone de recherche.</span><span class="sxs-lookup"><span data-stu-id="d8d87-298">In the menu, type in the search box **Billboard**.</span></span> <span data-ttu-id="d8d87-299">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="d8d87-299">Select the search result.</span></span>
4. <span data-ttu-id="d8d87-300">Dans l' **inspecteur** , affectez la valeur **Y**à l' **axe pivot** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-300">In the **Inspector** set the **Pivot Axis** to **Y**.</span></span>
5. <span data-ttu-id="d8d87-301">Essayez !</span><span class="sxs-lookup"><span data-stu-id="d8d87-301">Try it!</span></span> <span data-ttu-id="d8d87-302">Générez et déployez l’application comme auparavant.</span><span class="sxs-lookup"><span data-stu-id="d8d87-302">Build and deploy the app as before.</span></span>
6. <span data-ttu-id="d8d87-303">Découvrez comment l’objet de tableau blanc vous concerne, quelle que soit la façon dont vous modifiez le point de vue.</span><span class="sxs-lookup"><span data-stu-id="d8d87-303">See how the Billboard object faces you no matter how you change the viewpoint.</span></span>
7. <span data-ttu-id="d8d87-304">Supprimez le script du **AstroMan** pour le moment.</span><span class="sxs-lookup"><span data-stu-id="d8d87-304">Delete the script from the **AstroMan** for now.</span></span>

## <a name="chapter-6---tag-along"></a><span data-ttu-id="d8d87-305">Chapitre 6-balises</span><span class="sxs-lookup"><span data-stu-id="d8d87-305">Chapter 6 - Tag-Along</span></span>

>[!VIDEO https://www.youtube.com/embed/Ct8ORZAX5JU]

### <a name="objectives"></a><span data-ttu-id="d8d87-306">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d8d87-306">Objectives</span></span>

* <span data-ttu-id="d8d87-307">Utilisez la balise pour que nos hologrammes suivent la salle.</span><span class="sxs-lookup"><span data-stu-id="d8d87-307">Use Tag-Along to have our holograms follow us around the room.</span></span>

<span data-ttu-id="d8d87-308">À mesure que nous travaillons sur ce problème, nous vous présenterons les contraintes de conception suivantes:</span><span class="sxs-lookup"><span data-stu-id="d8d87-308">As we work on this issue, we'll be guided by the following design constraints:</span></span>

* <span data-ttu-id="d8d87-309">Le contenu doit toujours être un aperçu.</span><span class="sxs-lookup"><span data-stu-id="d8d87-309">Content should always be a glance away.</span></span>
* <span data-ttu-id="d8d87-310">Le contenu ne doit pas être en cours de traitement.</span><span class="sxs-lookup"><span data-stu-id="d8d87-310">Content should not be in the way.</span></span>
* <span data-ttu-id="d8d87-311">Le contenu de verrouillage de la tête est inconfortable.</span><span class="sxs-lookup"><span data-stu-id="d8d87-311">Head-locking content is uncomfortable.</span></span>

<span data-ttu-id="d8d87-312">La solution utilisée ici consiste à utiliser une approche «avec balises».</span><span class="sxs-lookup"><span data-stu-id="d8d87-312">The solution used here is to use a "tag-along" approach.</span></span>

<span data-ttu-id="d8d87-313">Une balise avec un objet ne quitte jamais entièrement la vue de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d8d87-313">A tag-along object never fully leaves the user's view.</span></span> <span data-ttu-id="d8d87-314">Vous pouvez considérer la balise comme un objet attaché à la tête de l’utilisateur par les bandes de caoutchouc.</span><span class="sxs-lookup"><span data-stu-id="d8d87-314">You can think of the a tag-along as being an object attached to the user's head by rubber bands.</span></span> <span data-ttu-id="d8d87-315">Au fur et à mesure que l’utilisateur se déplace, le contenu reste dans un aperçu facile en faisant glisser vers le bord de la vue sans quitter complètement.</span><span class="sxs-lookup"><span data-stu-id="d8d87-315">As the user moves, the content will stay within an easy glance by sliding towards the edge of the view without completely leaving.</span></span> <span data-ttu-id="d8d87-316">Lorsque l’utilisateur fait un regard sur l’objet tag, il est plus complet à afficher.</span><span class="sxs-lookup"><span data-stu-id="d8d87-316">When the user gazes towards the tag-along object, it comes more fully into view.</span></span>

<span data-ttu-id="d8d87-317">Nous allons utiliser le fichier **SimpleTagalong.cs** , qui:</span><span class="sxs-lookup"><span data-stu-id="d8d87-317">We're going to use the **SimpleTagalong.cs** file which will:</span></span>

1. <span data-ttu-id="d8d87-318">Déterminez si l’objet tag est dans les limites de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="d8d87-318">Determine if the Tag-Along object is within the camera bounds.</span></span>
2. <span data-ttu-id="d8d87-319">Si ce n’est pas le cas dans la vue frustum, placez la balise sur la partie de façon partielle dans la vue frustum.</span><span class="sxs-lookup"><span data-stu-id="d8d87-319">If not within the view frustum, position the Tag-Along to partially within the view frustum.</span></span>
3. <span data-ttu-id="d8d87-320">Sinon, placez la balise sur une distance par défaut de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d8d87-320">Otherwise, position the Tag-Along to a default distance from the user.</span></span>

<span data-ttu-id="d8d87-321">Pour ce faire, nous devons d’abord modifier le script **Interactible.cs** pour appeler **TagalongAction**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-321">To do this, we first must change the **Interactible.cs** script to call the **TagalongAction**.</span></span>

1. <span data-ttu-id="d8d87-322">Modifiez **Interactible.cs** en terminant le codage de l’exercice 6. a (supprimer les commentaires des lignes 84 à 87).</span><span class="sxs-lookup"><span data-stu-id="d8d87-322">Edit **Interactible.cs** by completing coding exercise 6.a (uncommenting lines 84 to 87).</span></span>

```cs
/* TODO: DEVELOPER CODING EXERCISE 6.a */
// 6.a: Uncomment the lines below to perform a Tagalong action.
if (interactibleAction != null)
{
    interactibleAction.PerformAction();
}
```

<span data-ttu-id="d8d87-323">Le script **InteractibleAction.cs** , associé à **Interactible.cs** , effectue des actions personnalisées lorsque vous appuyez sur des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d8d87-323">The **InteractibleAction.cs** script, paired with **Interactible.cs** performs custom actions when you tap on holograms.</span></span> <span data-ttu-id="d8d87-324">Dans ce cas, nous allons en utiliser un spécifiquement pour la balise.</span><span class="sxs-lookup"><span data-stu-id="d8d87-324">In this case, we'll use one specifically for tag-along.</span></span>

* <span data-ttu-id="d8d87-325">Dans le dossier **scripts** , cliquez sur la ressource **TagalongAction.cs** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8d87-325">In the **Scripts** folder click on **TagalongAction.cs** asset to open in Visual Studio.</span></span>
* <span data-ttu-id="d8d87-326">Terminez l’exercice de codage ou remplacez-le par ce qui suit:</span><span class="sxs-lookup"><span data-stu-id="d8d87-326">Complete the coding exercise or change it to this:</span></span>
  * <span data-ttu-id="d8d87-327">En haut de la **hiérarchie**, dans la barre de recherche, tapez **ChestButton_Center** et sélectionnez le résultat.</span><span class="sxs-lookup"><span data-stu-id="d8d87-327">At the top of the **Hierarchy**, in the search bar type **ChestButton_Center** and select the result.</span></span>
  * <span data-ttu-id="d8d87-328">Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-328">In the **Inspector** panel, click the **Add Component** button.</span></span>
  * <span data-ttu-id="d8d87-329">Dans le menu, tapez dans la zone de recherche **accompagnent action**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-329">In the menu, type in the search box **Tagalong Action**.</span></span> <span data-ttu-id="d8d87-330">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="d8d87-330">Select the search result.</span></span>
  * <span data-ttu-id="d8d87-331">Dans  le dossier hologrammes, recherchez la ressource **accompagnent** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-331">In **Holograms** folder find the **Tagalong** asset.</span></span>
  * <span data-ttu-id="d8d87-332">Sélectionnez l’objet **ChestButton_Center** dans la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d8d87-332">Select the **ChestButton_Center** object in the **Hierarchy**.</span></span> <span data-ttu-id="d8d87-333">Glissez-déplacez l’objet **accompagnent** à partir du panneau **projet** vers l' **inspecteur** dans la propriété **Object to accompagnent** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-333">Drag and drop the **TagAlong** object from the **Project** panel onto the **Inspector** into the **Object To Tagalong** property.</span></span>
  * <span data-ttu-id="d8d87-334">Faites glisser l’objet d' **action accompagnent** à partir de l' **inspecteur** dans le champ d' **action Interactible** sur le script **Interactible** .</span><span class="sxs-lookup"><span data-stu-id="d8d87-334">Drag the **Tagalong Action** object from the **Inspector** into the **Interactible Action** field on the **Interactible** script.</span></span>
* <span data-ttu-id="d8d87-335">Double-cliquez sur le script **TagalongAction** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8d87-335">Double click the **TagalongAction** script to open it in Visual Studio.</span></span>

![Configuration de Interactible](images/holograms210-interactible.png)

<span data-ttu-id="d8d87-337">Nous devons ajouter ce qui suit:</span><span class="sxs-lookup"><span data-stu-id="d8d87-337">We need to add the following:</span></span>

* <span data-ttu-id="d8d87-338">Ajoutez des fonctionnalités à la fonction PerformAction dans le script TagalongAction (héritée de InteractibleAction).</span><span class="sxs-lookup"><span data-stu-id="d8d87-338">Add functionality to the PerformAction function in the TagalongAction script (inherited from InteractibleAction).</span></span>
* <span data-ttu-id="d8d87-339">Ajoutez un billboarding à l’objet pointant vers le regard et définissez l’axe pivot sur XY.</span><span class="sxs-lookup"><span data-stu-id="d8d87-339">Add billboarding to the gazed-upon object, and set the pivot axis to XY.</span></span>
* <span data-ttu-id="d8d87-340">Ensuite, ajoutez une balise simple, avec l’objet.</span><span class="sxs-lookup"><span data-stu-id="d8d87-340">Then add simple Tag-Along to the object.</span></span>

<span data-ttu-id="d8d87-341">Voici notre solution, de **TagalongAction.cs**:</span><span class="sxs-lookup"><span data-stu-id="d8d87-341">Here's our solution, from **TagalongAction.cs**:</span></span>

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

* <span data-ttu-id="d8d87-342">Essayez !</span><span class="sxs-lookup"><span data-stu-id="d8d87-342">Try it!</span></span> <span data-ttu-id="d8d87-343">Générez et déployez l’application.</span><span class="sxs-lookup"><span data-stu-id="d8d87-343">Build and deploy the app.</span></span>
* <span data-ttu-id="d8d87-344">Regardez comment le contenu suit le centre du point de regard, mais pas en continu et sans le bloquer.</span><span class="sxs-lookup"><span data-stu-id="d8d87-344">Watch how the content follows the center of the gaze point, but not continuously and without blocking it.</span></span>
