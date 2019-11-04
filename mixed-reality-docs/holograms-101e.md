---
title: Notions de base de 101E-projet complet avec l’émulateur
description: Suivez cette procédure pas à pas de codage à l’aide d’Unity, de Visual Studio et de l’émulateur HoloLens pour apprendre les principes de base d’une application holographique.
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: réalité mixte, Windows Mixed Reality, HoloLens, hologramme, Academy, didacticiel, émulateur
ms.openlocfilehash: b1d8e1f3f272051bdd6f69ab88c3aef4f86f13ef
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73434702"
---
>[!NOTE]
><span data-ttu-id="7b62e-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="7b62e-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="7b62e-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="7b62e-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="7b62e-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="7b62e-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="7b62e-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7b62e-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="7b62e-108">[Une nouvelle série de didacticiels](mrlearning-base.md) a été publiée pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="7b62e-108">[A new series of tutorials](mrlearning-base.md) has been posted for HoloLens 2.</span></span>

<br>

# <a name="mr-basics-101e-complete-project-with-emulator"></a><span data-ttu-id="7b62e-109">Notions de base de 101E : projet complet avec l’émulateur</span><span class="sxs-lookup"><span data-stu-id="7b62e-109">MR Basics 101E: Complete project with emulator</span></span>

 >[!VIDEO https://www.youtube.com/embed/Xzm8_s05mm8]

<span data-ttu-id="7b62e-110">Ce didacticiel vous guide tout au long d’un projet complet, Unity, qui illustre les fonctionnalités de base de la réalité mixte Windows sur HoloLens [, y compris](gaze-and-commit.md)le point de présence, les [gestes](gaze-and-commit.md#composite-gestures), l' [entrée vocale](voice-input.md), le [son spatial](spatial-sound.md) et le [mappage spatial](spatial-mapping.md) .</span><span class="sxs-lookup"><span data-stu-id="7b62e-110">This tutorial will walk you through a complete project, built in Unity, that demonstrates core Windows Mixed Reality features on HoloLens including [gaze](gaze-and-commit.md), [gestures](gaze-and-commit.md#composite-gestures), [voice input](voice-input.md), [spatial sound](spatial-sound.md) and [spatial mapping](spatial-mapping.md).</span></span> <span data-ttu-id="7b62e-111">Le didacticiel prendra environ 1 heure.</span><span class="sxs-lookup"><span data-stu-id="7b62e-111">The tutorial will take approximately 1 hour to complete.</span></span>

## <a name="device-support"></a><span data-ttu-id="7b62e-112">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="7b62e-112">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="7b62e-113">Course</span><span class="sxs-lookup"><span data-stu-id="7b62e-113">Course</span></span></th><th style="width:150px"> <span data-ttu-id="7b62e-114"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="7b62e-114"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="7b62e-115"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="7b62e-115"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="7b62e-116">Notions de base de 101E : projet complet avec l’émulateur</span><span class="sxs-lookup"><span data-stu-id="7b62e-116">MR Basics 101E: Complete project with emulator</span></span></td><td style="text-align: center;"> <span data-ttu-id="7b62e-117">✔️</span><span class="sxs-lookup"><span data-stu-id="7b62e-117">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="7b62e-118">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7b62e-118">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="7b62e-119">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="7b62e-119">Prerequisites</span></span>

* <span data-ttu-id="7b62e-120">Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="7b62e-120">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>

### <a name="project-files"></a><span data-ttu-id="7b62e-121">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="7b62e-121">Project files</span></span>

* <span data-ttu-id="7b62e-122">Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) requis par le projet.</span><span class="sxs-lookup"><span data-stu-id="7b62e-122">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) required by the project.</span></span><span data-ttu-id="7b62e-123"> Requiert Unity 2017,2 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7b62e-123"> Requires Unity 2017.2 or later.</span></span>
  * <span data-ttu-id="7b62e-124">Si vous avez encore besoin de la prise en charge d’Unity 5,6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).</span><span class="sxs-lookup"><span data-stu-id="7b62e-124">If you still need Unity 5.6 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).</span></span>
  * <span data-ttu-id="7b62e-125">Si vous avez encore besoin de la prise en charge d’Unity 5,5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).</span><span class="sxs-lookup"><span data-stu-id="7b62e-125">If you still need Unity 5.5 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).</span></span>
  * <span data-ttu-id="7b62e-126">Si vous avez encore besoin de la prise en charge d’Unity 5,4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).</span><span class="sxs-lookup"><span data-stu-id="7b62e-126">If you still need Unity 5.4 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).</span></span>
* <span data-ttu-id="7b62e-127">Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.</span><span class="sxs-lookup"><span data-stu-id="7b62e-127">Un-archive the files to your desktop or other easy to reach location.</span></span> <span data-ttu-id="7b62e-128">Conservez le nom du dossier **origami**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-128">Keep the folder name as **Origami**.</span></span>

>[!NOTE]
><span data-ttu-id="7b62e-129">Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).</span><span class="sxs-lookup"><span data-stu-id="7b62e-129">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).</span></span>

## <a name="chapter-1---holo-world"></a><span data-ttu-id="7b62e-130">Chapitre 1-monde « Holo »</span><span class="sxs-lookup"><span data-stu-id="7b62e-130">Chapter 1 - "Holo" world</span></span>

>[!VIDEO https://www.youtube.com/embed/qotpUpIQxVU]

<span data-ttu-id="7b62e-131">Dans ce chapitre, nous allons configurer notre premier projet Unity et effectuer un pas à pas détaillé dans le processus de création et de déploiement.</span><span class="sxs-lookup"><span data-stu-id="7b62e-131">In this chapter, we'll setup our first Unity project and step through the build and deploy process.</span></span>

### <a name="objectives"></a><span data-ttu-id="7b62e-132">Objectifs</span><span class="sxs-lookup"><span data-stu-id="7b62e-132">Objectives</span></span>

* <span data-ttu-id="7b62e-133">Configurez Unity pour le développement holographique.</span><span class="sxs-lookup"><span data-stu-id="7b62e-133">Set up Unity for holographic development.</span></span>
* <span data-ttu-id="7b62e-134">Créez un hologramme.</span><span class="sxs-lookup"><span data-stu-id="7b62e-134">Make a hologram.</span></span>
* <span data-ttu-id="7b62e-135">Consultez un hologramme que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="7b62e-135">See a hologram that you made.</span></span>

### <a name="instructions"></a><span data-ttu-id="7b62e-136">Instructions</span><span class="sxs-lookup"><span data-stu-id="7b62e-136">Instructions</span></span>

* <span data-ttu-id="7b62e-137">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="7b62e-137">Start Unity.</span></span>
* <span data-ttu-id="7b62e-138">Sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-138">Select **Open**.</span></span>
* <span data-ttu-id="7b62e-139">Entrez l’emplacement du dossier **origami** que vous avez précédemment désinstallé.</span><span class="sxs-lookup"><span data-stu-id="7b62e-139">Enter location as the **Origami** folder you previously un-archived.</span></span>
* <span data-ttu-id="7b62e-140">Sélectionnez **origami** , puis cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-140">Select **Origami** and click **Select Folder**.</span></span>
* <span data-ttu-id="7b62e-141">Enregistrez la nouvelle scène : **fichier** / **enregistrer la scène sous**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-141">Save the new scene: **File** / **Save Scene As**.</span></span>
* <span data-ttu-id="7b62e-142">Nommez la scène **origami** et appuyez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7b62e-142">Name the scene **Origami** and press the **Save** button.</span></span>

#### <a name="setup-the-main-camera"></a><span data-ttu-id="7b62e-143">Configurer la caméra principale</span><span class="sxs-lookup"><span data-stu-id="7b62e-143">Setup the main camera</span></span>

* <span data-ttu-id="7b62e-144">Dans le **panneau hiérarchie**, sélectionnez **caméra principale**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-144">In the **Hierarchy Panel**, select **Main Camera**.</span></span>
* <span data-ttu-id="7b62e-145">Dans l' **inspecteur** , définissez sa position de transformation sur **0, 0,** 0.</span><span class="sxs-lookup"><span data-stu-id="7b62e-145">In the **Inspector** set its transform position to **0,0,0**.</span></span>
* <span data-ttu-id="7b62e-146">Recherchez la propriété **effacer les indicateurs** et remplacez la liste déroulante **skybox** par **couleur unie**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-146">Find the **Clear Flags** property, and change the dropdown from **Skybox** to **Solid color**.</span></span>
* <span data-ttu-id="7b62e-147">Cliquez sur le champ **arrière-plan** pour ouvrir un sélecteur de couleurs.</span><span class="sxs-lookup"><span data-stu-id="7b62e-147">Click on the **Background** field to open a color picker.</span></span>
* <span data-ttu-id="7b62e-148">Affectez **R, G, B et A** à **0**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-148">Set **R, G, B, and A** to **0**.</span></span>

#### <a name="setup-the-scene"></a><span data-ttu-id="7b62e-149">Configurer la scène</span><span class="sxs-lookup"><span data-stu-id="7b62e-149">Setup the scene</span></span>

* <span data-ttu-id="7b62e-150">Dans le **volet hiérarchie**, cliquez sur **créer** et **créez un vide**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-150">In the **Hierarchy Panel**, click on **Create** and **Create Empty**.</span></span>
* <span data-ttu-id="7b62e-151">Cliquez avec le bouton droit sur le nouveau **gameobject** , puis sélectionnez Renommer.</span><span class="sxs-lookup"><span data-stu-id="7b62e-151">Right-click the new **GameObject** and select Rename.</span></span> <span data-ttu-id="7b62e-152">Renommez GameObject en **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-152">Rename the GameObject to **OrigamiCollection**.</span></span>
* <span data-ttu-id="7b62e-153">Dans le dossier **hologrammes** du **panneau Projet**:</span><span class="sxs-lookup"><span data-stu-id="7b62e-153">From the **Holograms** folder in the **Project Panel**:</span></span>
  * <span data-ttu-id="7b62e-154">Faites glisser **étape** dans la hiérarchie pour être un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-154">Drag **Stage** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
  * <span data-ttu-id="7b62e-155">Faites glisser **Sphere1** dans la hiérarchie pour être un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-155">Drag **Sphere1** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
  * <span data-ttu-id="7b62e-156">Faites glisser **Sphere2** dans la hiérarchie pour être un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-156">Drag **Sphere2** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
* <span data-ttu-id="7b62e-157">Cliquez avec le bouton droit sur l’objet **Light directionnel** dans le **panneau hiérarchie** , puis sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-157">Right-click the **Directional Light** object in the **Hierarchy Panel** and select **Delete**.</span></span>
* <span data-ttu-id="7b62e-158">À partir du dossier **hologrammes** , faites glisser **Lights** à la racine du **panneau de hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-158">From the **Holograms** folder, drag **Lights** into the root of the **Hierarchy Panel**.</span></span>
* <span data-ttu-id="7b62e-159">Dans la **hiérarchie**, sélectionnez **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-159">In the **Hierarchy**, select the **OrigamiCollection**.</span></span>
* <span data-ttu-id="7b62e-160">Dans l' **inspecteur**, définissez la position de la transformation sur **0,-0,5, 2,0**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-160">In the **Inspector**, set the transform position to **0, -0.5, 2.0**.</span></span>
* <span data-ttu-id="7b62e-161">Appuyez sur le bouton de **lecture** dans Unity pour afficher un aperçu de vos hologrammes.</span><span class="sxs-lookup"><span data-stu-id="7b62e-161">Press the **Play** button in Unity to preview your holograms.</span></span>
* <span data-ttu-id="7b62e-162">Les objets origami doivent apparaître dans la fenêtre d’aperçu.</span><span class="sxs-lookup"><span data-stu-id="7b62e-162">You should see the Origami objects in the preview window.</span></span>
* <span data-ttu-id="7b62e-163">Appuyez sur **lecture** une deuxième fois pour arrêter le mode aperçu.</span><span class="sxs-lookup"><span data-stu-id="7b62e-163">Press **Play** a second time to stop preview mode.</span></span>

#### <a name="export-the-project-from-unity-to-visual-studio"></a><span data-ttu-id="7b62e-164">Exporter le projet d’Unity vers Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7b62e-164">Export the project from Unity to Visual Studio</span></span>

* <span data-ttu-id="7b62e-165">Dans Unity, sélectionnez **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-165">In Unity select **File > Build Settings**.</span></span>
* <span data-ttu-id="7b62e-166">Sélectionnez **Windows Store** dans la liste **plateforme** , puis cliquez sur **basculer la plateforme**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-166">Select **Windows Store** in the **Platform** list and click **Switch Platform**.</span></span>
* <span data-ttu-id="7b62e-167">Affectez à **SDK** la valeur **Universal 10** et **type de build** la valeur **D3D**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-167">Set **SDK** to **Universal 10** and **Build Type** to **D3D**.</span></span>
* <span data-ttu-id="7b62e-168">Vérifiez **les C# projets Unity**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-168">Check **Unity C# Projects**.</span></span>
* <span data-ttu-id="7b62e-169">Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="7b62e-169">Click **Add Open Scenes** to add the scene.</span></span>
* <span data-ttu-id="7b62e-170">Cliquez sur **paramètres du lecteur...** .</span><span class="sxs-lookup"><span data-stu-id="7b62e-170">Click **Player Settings...**.</span></span>
* <span data-ttu-id="7b62e-171">Dans le panneau de l’inspecteur, sélectionnez le **logo du Windows Store**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-171">In the Inspector Panel select the **Windows Store logo**.</span></span> <span data-ttu-id="7b62e-172">Sélectionnez ensuite **paramètres de publication**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-172">Then select **Publishing Settings**.</span></span>
* <span data-ttu-id="7b62e-173">Dans la section **fonctionnalités** , sélectionnez les fonctionnalités **microphone** et **SpatialPerception** .</span><span class="sxs-lookup"><span data-stu-id="7b62e-173">In the **Capabilities** section, select the **Microphone** and **SpatialPerception** capabilities.</span></span>
* <span data-ttu-id="7b62e-174">De retour dans la fenêtre Paramètres de build, cliquez sur **générer**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-174">Back in the Build Settings window, click **Build**.</span></span>
* <span data-ttu-id="7b62e-175">Créez un **dossier** nommé « App ».</span><span class="sxs-lookup"><span data-stu-id="7b62e-175">Create a **New Folder** named "App".</span></span>
* <span data-ttu-id="7b62e-176">Cliquez sur le **dossier**de l’application.</span><span class="sxs-lookup"><span data-stu-id="7b62e-176">Single click the **App Folder**.</span></span>
* <span data-ttu-id="7b62e-177">Appuyez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-177">Press **Select Folder**.</span></span>
* <span data-ttu-id="7b62e-178">Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7b62e-178">When Unity is done, a File Explorer window will appear.</span></span>
* <span data-ttu-id="7b62e-179">Ouvrez le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="7b62e-179">Open the **App** folder.</span></span>
* <span data-ttu-id="7b62e-180">Ouvrez la **solution Visual Studio origami**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-180">Open the **Origami Visual Studio Solution**.</span></span>
* <span data-ttu-id="7b62e-181">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-181">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **X86**.</span></span>
  * <span data-ttu-id="7b62e-182">Cliquez sur la flèche en regard du bouton périphérique, puis sélectionnez **émulateur HoloLens**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-182">Click on the arrow next to the Device button, and select **HoloLens Emulator**.</span></span>
  * <span data-ttu-id="7b62e-183">Cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-183">Click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
  * <span data-ttu-id="7b62e-184">Après un certain temps, l’émulateur démarrera avec le projet origami.</span><span class="sxs-lookup"><span data-stu-id="7b62e-184">After some time the emulator will start with the Origami project.</span></span> <span data-ttu-id="7b62e-185">Lors du premier lancement de l' [émulateur](using-the-hololens-emulator.md), le démarrage de l’émulateur peut prendre jusqu’à 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="7b62e-185">When first launching the [emulator](using-the-hololens-emulator.md), it can take as long as 15 minutes for the emulator to start up.</span></span> <span data-ttu-id="7b62e-186">Une fois qu’il a démarré, ne le fermez pas.</span><span class="sxs-lookup"><span data-stu-id="7b62e-186">Once it starts, do not close it.</span></span>

## <a name="chapter-2---gaze"></a><span data-ttu-id="7b62e-187">Chapitre 2-point de regard</span><span class="sxs-lookup"><span data-stu-id="7b62e-187">Chapter 2 - Gaze</span></span>

>[!VIDEO https://www.youtube.com/embed/BPWTbAC210k]

<span data-ttu-id="7b62e-188">Dans ce chapitre, nous allons présenter la première des trois façons d’interagir avec vos hologrammes, en pointant le [regard](gaze-and-commit.md).</span><span class="sxs-lookup"><span data-stu-id="7b62e-188">In this chapter, we are going to introduce the first of three ways of interacting with your holograms -- [gaze](gaze-and-commit.md).</span></span>

### <a name="objectives"></a><span data-ttu-id="7b62e-189">Objectifs</span><span class="sxs-lookup"><span data-stu-id="7b62e-189">Objectives</span></span>

* <span data-ttu-id="7b62e-190">Visualisez votre point de regard à l’aide d’un curseur verrouillé.</span><span class="sxs-lookup"><span data-stu-id="7b62e-190">Visualize your gaze using a world-locked cursor.</span></span>

### <a name="instructions"></a><span data-ttu-id="7b62e-191">Instructions</span><span class="sxs-lookup"><span data-stu-id="7b62e-191">Instructions</span></span>

* <span data-ttu-id="7b62e-192">Revenez à votre projet Unity et fermez la fenêtre Paramètres de build si elle est toujours ouverte.</span><span class="sxs-lookup"><span data-stu-id="7b62e-192">Go back to your Unity project, and close the Build Settings window if it's still open.</span></span>
* <span data-ttu-id="7b62e-193">Sélectionnez le dossier **hologrammes** dans le **panneau Projet**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-193">Select the **Holograms** folder in the **Project panel**.</span></span>
* <span data-ttu-id="7b62e-194">Faites glisser l’objet **curseur** dans le volet de la **hiérarchie** au niveau de la racine.</span><span class="sxs-lookup"><span data-stu-id="7b62e-194">Drag the **Cursor** object into the **Hierarchy panel** at the root level.</span></span>
* <span data-ttu-id="7b62e-195">Double-cliquez sur l’objet **curseur** pour l’examiner en détail.</span><span class="sxs-lookup"><span data-stu-id="7b62e-195">Double-click on the **Cursor** object to take a closer look at it.</span></span>
* <span data-ttu-id="7b62e-196">Cliquez avec le bouton droit sur le dossier **scripts** dans le panneau projet.</span><span class="sxs-lookup"><span data-stu-id="7b62e-196">Right-click on the **Scripts** folder in the Project panel.</span></span>
* <span data-ttu-id="7b62e-197">Cliquez sur le sous-menu **créer** .</span><span class="sxs-lookup"><span data-stu-id="7b62e-197">Click the **Create** sub-menu.</span></span>
* <span data-ttu-id="7b62e-198">Sélectionnez  **C# script**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-198">Select **C# Script**.</span></span>
* <span data-ttu-id="7b62e-199">Nommez le script **WorldCursor**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-199">Name the script **WorldCursor**.</span></span> <span data-ttu-id="7b62e-200">Remarque : le nom respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="7b62e-200">Note: The name is case-sensitive.</span></span> <span data-ttu-id="7b62e-201">Vous n’avez pas besoin d’ajouter l’extension. cs.</span><span class="sxs-lookup"><span data-stu-id="7b62e-201">You do not need to add the .cs extension.</span></span>
* <span data-ttu-id="7b62e-202">Sélectionnez l’objet **curseur** dans le **panneau hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-202">Select the **Cursor** object in the **Hierarchy panel**.</span></span>
* <span data-ttu-id="7b62e-203">Glissez-déplacez le script **WorldCursor** dans le panneau de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-203">Drag and drop the **WorldCursor** script into the **Inspector panel**.</span></span>
* <span data-ttu-id="7b62e-204">Double-cliquez sur le script **WorldCursor** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b62e-204">Double-click the **WorldCursor** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="7b62e-205">Copiez et collez ce code dans **WorldCursor.cs** et **Enregistrez All**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-205">Copy and paste this code into **WorldCursor.cs** and **Save All**.</span></span>

```cs
using UnityEngine;

public class WorldCursor : MonoBehaviour
{
    private MeshRenderer meshRenderer;

    // Use this for initialization
    void Start()
    {
        // Grab the mesh renderer that's on the same object as this script.
        meshRenderer = this.gameObject.GetComponentInChildren<MeshRenderer>();
    }

    // Update is called once per frame
    void Update()
    {
        // Do a raycast into the world based on the user's
        // head position and orientation.
        var headPosition = Camera.main.transform.position;
        var gazeDirection = Camera.main.transform.forward;

        RaycastHit hitInfo;

        if (Physics.Raycast(headPosition, gazeDirection, out hitInfo))
        {
            // If the raycast hit a hologram...
            // Display the cursor mesh.
            meshRenderer.enabled = true;

            // Move thecursor to the point where the raycast hit.
            this.transform.position = hitInfo.point;

            // Rotate the cursor to hug the surface of the hologram.
            this.transform.rotation = Quaternion.FromToRotation(Vector3.up, hitInfo.normal);
        }
        else
        {
            // If the raycast did not hit a hologram, hide the cursor mesh.
            meshRenderer.enabled = false;
        }
    }
}
```

* <span data-ttu-id="7b62e-206">Régénérez l’application à partir du **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-206">Rebuild the app from **File > Build Settings**.</span></span>
* <span data-ttu-id="7b62e-207">Revenez à la solution Visual Studio utilisée précédemment pour le déploiement sur l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="7b62e-207">Return to the Visual Studio solution previously used to deploy to the emulator.</span></span>
* <span data-ttu-id="7b62e-208">Lorsque vous y êtes invité, sélectionnez « recharger tout ».</span><span class="sxs-lookup"><span data-stu-id="7b62e-208">Select 'Reload All' when prompted.</span></span>
* <span data-ttu-id="7b62e-209">Cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-209">Click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
* <span data-ttu-id="7b62e-210">Utilisez le contrôleur Xbox pour parcourir la scène.</span><span class="sxs-lookup"><span data-stu-id="7b62e-210">Use the Xbox controller to look around the scene.</span></span> <span data-ttu-id="7b62e-211">Notez que le curseur interagit avec la forme d’objets.</span><span class="sxs-lookup"><span data-stu-id="7b62e-211">Notice how the cursor interacts with the shape of objects.</span></span>

## <a name="chapter-3---gestures"></a><span data-ttu-id="7b62e-212">Chapitre 3-mouvements</span><span class="sxs-lookup"><span data-stu-id="7b62e-212">Chapter 3 - Gestures</span></span>

>[!VIDEO https://www.youtube.com/embed/6d-0RHeKHq4]

<span data-ttu-id="7b62e-213">Dans ce chapitre, nous allons ajouter la prise en charge des [gestes](gaze-and-commit.md#composite-gestures).</span><span class="sxs-lookup"><span data-stu-id="7b62e-213">In this chapter, we'll add support for [gestures](gaze-and-commit.md#composite-gestures).</span></span> <span data-ttu-id="7b62e-214">Lorsque l’utilisateur sélectionne une sphère papier, nous allons faire tomber la sphère en activant la gravité en utilisant le moteur physique Unity.</span><span class="sxs-lookup"><span data-stu-id="7b62e-214">When the user selects a paper sphere, we'll make the sphere fall by turning on gravity using Unity's physics engine.</span></span>

### <a name="objectives"></a><span data-ttu-id="7b62e-215">Objectifs</span><span class="sxs-lookup"><span data-stu-id="7b62e-215">Objectives</span></span>

* <span data-ttu-id="7b62e-216">Contrôlez vos hologrammes avec le geste Select.</span><span class="sxs-lookup"><span data-stu-id="7b62e-216">Control your holograms with the Select gesture.</span></span>

### <a name="instructions"></a><span data-ttu-id="7b62e-217">Instructions</span><span class="sxs-lookup"><span data-stu-id="7b62e-217">Instructions</span></span>

<span data-ttu-id="7b62e-218">Nous allons commencer par créer un script que peut détecter le mouvement Select.</span><span class="sxs-lookup"><span data-stu-id="7b62e-218">We'll start by creating a script than can detect the Select gesture.</span></span>

* <span data-ttu-id="7b62e-219">Dans le dossier **scripts** , créez un script nommé **GazeGestureManager**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-219">In the **Scripts** folder, create a script named **GazeGestureManager**.</span></span>
* <span data-ttu-id="7b62e-220">Faites glisser le script **GazeGestureManager** sur l’objet **OrigamiCollection** dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="7b62e-220">Drag the **GazeGestureManager** script onto the **OrigamiCollection** object in the Hierarchy.</span></span>
* <span data-ttu-id="7b62e-221">Ouvrez le script **GazeGestureManager** dans Visual Studio et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="7b62e-221">Open the **GazeGestureManager** script in Visual Studio and add the following code:</span></span>

```cs
using UnityEngine;
using UnityEngine.XR.WSA.Input;

public class GazeGestureManager : MonoBehaviour
{
    public static GazeGestureManager Instance { get; private set; }

    // Represents the hologram that is currently being gazed at.
    public GameObject FocusedObject { get; private set; }

    GestureRecognizer recognizer;

    // Use this for initialization
    void Start()
    {
        Instance = this;

        // Set up a GestureRecognizer to detect Select gestures.
        recognizer = new GestureRecognizer();
        recognizer.Tapped += (args) =>
        {
            // Send an OnSelect message to the focused object and its ancestors.
            if (FocusedObject != null)
            {
                FocusedObject.SendMessageUpwards("OnSelect", SendMessageOptions.DontRequireReceiver);
            }
        };
        recognizer.StartCapturingGestures();
    }

    // Update is called once per frame
    void Update()
    {
        // Figure out which hologram is focused this frame.
        GameObject oldFocusObject = FocusedObject;

        // Do a raycast into the world based on the user's
        // head position and orientation.
        var headPosition = Camera.main.transform.position;
        var gazeDirection = Camera.main.transform.forward;

        RaycastHit hitInfo;
        if (Physics.Raycast(headPosition, gazeDirection, out hitInfo))
        {
            // If the raycast hit a hologram, use that as the focused object.
            FocusedObject = hitInfo.collider.gameObject;
        }
        else
        {
            // If the raycast did not hit a hologram, clear the focused object.
            FocusedObject = null;
        }

        // If the focused object changed this frame,
        // start detecting fresh gestures again.
        if (FocusedObject != oldFocusObject)
        {
            recognizer.CancelGestures();
            recognizer.StartCapturingGestures();
        }
    }
}
```

* <span data-ttu-id="7b62e-222">Créez un autre script dans le dossier scripts, cette fois nommé **SphereCommands**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-222">Create another script in the Scripts folder, this time named **SphereCommands**.</span></span>
* <span data-ttu-id="7b62e-223">Développez l’objet **OrigamiCollection** dans l’affichage des hiérarchies.</span><span class="sxs-lookup"><span data-stu-id="7b62e-223">Expand the **OrigamiCollection** object in the Hierarchy view.</span></span>
* <span data-ttu-id="7b62e-224">Faites glisser le script **SphereCommands** sur l’objet **Sphere1** dans le panneau hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="7b62e-224">Drag the **SphereCommands** script onto the **Sphere1** object in the Hierarchy panel.</span></span>
* <span data-ttu-id="7b62e-225">Faites glisser le script **SphereCommands** sur l’objet **Sphere2** dans le panneau hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="7b62e-225">Drag the **SphereCommands** script onto the **Sphere2** object in the Hierarchy panel.</span></span>
* <span data-ttu-id="7b62e-226">Ouvrez le script dans Visual Studio pour le modifier, puis remplacez le code par défaut par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="7b62e-226">Open the script in Visual Studio for editing, and replace the default code with this:</span></span>

```cs
using UnityEngine;

public class SphereCommands : MonoBehaviour
{
    // Called by GazeGestureManager when the user performs a Select gesture
    void OnSelect()
    {
        // If the sphere has no Rigidbody component, add one to enable physics.
        if (!this.GetComponent<Rigidbody>())
        {
            var rigidbody = this.gameObject.AddComponent<Rigidbody>();
            rigidbody.collisionDetectionMode = CollisionDetectionMode.Continuous;
        }
    }
}
```

* <span data-ttu-id="7b62e-227">Exportez, générez et déployez l’application sur l’émulateur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="7b62e-227">Export, build and deploy the app to the HoloLens emulator.</span></span>
* <span data-ttu-id="7b62e-228">Parcourez la scène et centrez-la sur l’un des sphères.</span><span class="sxs-lookup"><span data-stu-id="7b62e-228">Look around the scene, and center on one of the spheres.</span></span>
* <span data-ttu-id="7b62e-229">Appuyez sur le bouton **A** du contrôleur Xbox ou appuyez sur la barre d’espace pour simuler le mouvement Select.</span><span class="sxs-lookup"><span data-stu-id="7b62e-229">Press the **A** button on the Xbox controller or press the Spacebar to simulate the Select gesture.</span></span>

## <a name="chapter-4---voice"></a><span data-ttu-id="7b62e-230">Chapitre 4-voix</span><span class="sxs-lookup"><span data-stu-id="7b62e-230">Chapter 4 - Voice</span></span>

>[!VIDEO https://www.youtube.com/embed/LxbOhnd2_GM]

<span data-ttu-id="7b62e-231">Dans ce chapitre, nous allons ajouter la prise en charge de deux [commandes vocales](voice-input.md): « réinitialiser le monde » pour revenir à leur emplacement d’origine, puis « déposer la sphère » pour faire tomber la sphère.</span><span class="sxs-lookup"><span data-stu-id="7b62e-231">In this chapter, we'll add support for two [voice commands](voice-input.md): "Reset world" to returns the dropped spheres to their original location, and "Drop sphere" to make the sphere fall.</span></span>

### <a name="objectives"></a><span data-ttu-id="7b62e-232">Objectifs</span><span class="sxs-lookup"><span data-stu-id="7b62e-232">Objectives</span></span>

* <span data-ttu-id="7b62e-233">Ajoutez des commandes vocales qui écoutent toujours en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="7b62e-233">Add voice commands that always listen in the background.</span></span>
* <span data-ttu-id="7b62e-234">Créez un hologramme qui réagit à une commande vocale.</span><span class="sxs-lookup"><span data-stu-id="7b62e-234">Create a hologram that reacts to a voice command.</span></span>

### <a name="instructions"></a><span data-ttu-id="7b62e-235">Instructions</span><span class="sxs-lookup"><span data-stu-id="7b62e-235">Instructions</span></span>

* <span data-ttu-id="7b62e-236">Dans le dossier **scripts** , créez un script nommé **SpeechManager**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-236">In the **Scripts** folder, create a script named **SpeechManager**.</span></span>
* <span data-ttu-id="7b62e-237">Faites glisser le script **SpeechManager** sur l’objet **OrigamiCollection** dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="7b62e-237">Drag the **SpeechManager** script onto the **OrigamiCollection** object in the Hierarchy</span></span>
* <span data-ttu-id="7b62e-238">Ouvrez le script **SpeechManager** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b62e-238">Open the **SpeechManager** script in Visual Studio.</span></span>
* <span data-ttu-id="7b62e-239">Copiez et collez ce code dans **SpeechManager.cs** et **Enregistrez All**:</span><span class="sxs-lookup"><span data-stu-id="7b62e-239">Copy and paste this code into **SpeechManager.cs** and **Save All**:</span></span>

```cs
using System.Collections.Generic;
using System.Linq;
using UnityEngine;
using UnityEngine.Windows.Speech;

public class SpeechManager : MonoBehaviour
{
    KeywordRecognizer keywordRecognizer = null;
    Dictionary<string, System.Action> keywords = new Dictionary<string, System.Action>();

    // Use this for initialization
    void Start()
    {
        keywords.Add("Reset world", () =>
        {
            // Call the OnReset method on every descendant object.
            this.BroadcastMessage("OnReset");
        });

        keywords.Add("Drop Sphere", () =>
        {
            var focusObject = GazeGestureManager.Instance.FocusedObject;
            if (focusObject != null)
            {
                // Call the OnDrop method on just the focused object.
                focusObject.SendMessage("OnDrop", SendMessageOptions.DontRequireReceiver);
            }
        });

        // Tell the KeywordRecognizer about our keywords.
        keywordRecognizer = new KeywordRecognizer(keywords.Keys.ToArray());

        // Register a callback for the KeywordRecognizer and start recognizing!
        keywordRecognizer.OnPhraseRecognized += KeywordRecognizer_OnPhraseRecognized;
        keywordRecognizer.Start();
    }

    private void KeywordRecognizer_OnPhraseRecognized(PhraseRecognizedEventArgs args)
    {
        System.Action keywordAction;
        if (keywords.TryGetValue(args.text, out keywordAction))
        {
            keywordAction.Invoke();
        }
    }
}
```

* <span data-ttu-id="7b62e-240">Ouvrez le script **SphereCommands** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b62e-240">Open the **SphereCommands** script in Visual Studio.</span></span>
* <span data-ttu-id="7b62e-241">Mettez à jour le script pour le lire comme suit :</span><span class="sxs-lookup"><span data-stu-id="7b62e-241">Update the script to read as follows:</span></span>

```cs
using UnityEngine;

public class SphereCommands : MonoBehaviour
{
    Vector3 originalPosition;

    // Use this for initialization
    void Start()
    {
        // Grab the original local position of the sphere when the app starts.
        originalPosition = this.transform.localPosition;
    }

    // Called by GazeGestureManager when the user performs a Select gesture
    void OnSelect()
    {
        // If the sphere has no Rigidbody component, add one to enable physics.
        if (!this.GetComponent<Rigidbody>())
        {
            var rigidbody = this.gameObject.AddComponent<Rigidbody>();
            rigidbody.collisionDetectionMode = CollisionDetectionMode.Continuous;
        }
    }

    // Called by SpeechManager when the user says the "Reset world" command
    void OnReset()
    {
        // If the sphere has a Rigidbody component, remove it to disable physics.
        var rigidbody = this.GetComponent<Rigidbody>();
        if (rigidbody != null)
        {
            rigidbody.isKinematic = true;
            Destroy(rigidbody);
        }

        // Put the sphere back into its original local position.
        this.transform.localPosition = originalPosition;
    }

    // Called by SpeechManager when the user says the "Drop sphere" command
    void OnDrop()
    {
        // Just do the same logic as a Select gesture.
        OnSelect();
    }
}
```

* <span data-ttu-id="7b62e-242">Exportez, générez et déployez l’application sur l’émulateur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="7b62e-242">Export, build and deploy the app to the HoloLens emulator.</span></span>
* <span data-ttu-id="7b62e-243">L’émulateur prend en charge le microphone de votre PC et répond à votre voix : Ajustez l’affichage afin que le curseur se trouve sur l’un des deux, et dites « déposer la sphère ».</span><span class="sxs-lookup"><span data-stu-id="7b62e-243">The emulator will support your PC's microphone and respond to your voice: adjust the view so the cursor is on one of the spheres, and say "Drop Sphere".</span></span>
* <span data-ttu-id="7b62e-244">Dites «**Réinitialiser le monde**» pour ramener les positions initiales.</span><span class="sxs-lookup"><span data-stu-id="7b62e-244">Say "**Reset World**" to bring them back to their initial positions.</span></span>

## <a name="chapter-5---spatial-sound"></a><span data-ttu-id="7b62e-245">Chapitre 5-sons spatiaux</span><span class="sxs-lookup"><span data-stu-id="7b62e-245">Chapter 5 - Spatial sound</span></span>

>[!VIDEO https://www.youtube.com/embed/Xc3C4VA10w4]

<span data-ttu-id="7b62e-246">Dans ce chapitre, nous allons ajouter de la musique à l’application, puis déclencher des effets sonores sur certaines actions.</span><span class="sxs-lookup"><span data-stu-id="7b62e-246">In this chapter, we'll add music to the app, and then trigger sound effects on certain actions.</span></span> <span data-ttu-id="7b62e-247">Nous utiliserons le [son spatial](spatial-sound.md) pour fournir des sons à un emplacement spécifique dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="7b62e-247">We'll be using [spatial sound](spatial-sound.md) to give sounds a specific location in 3D space.</span></span>

### <a name="objectives"></a><span data-ttu-id="7b62e-248">Objectifs</span><span class="sxs-lookup"><span data-stu-id="7b62e-248">Objectives</span></span>

* <span data-ttu-id="7b62e-249">Écoutez des hologrammes dans votre monde.</span><span class="sxs-lookup"><span data-stu-id="7b62e-249">Hear holograms in your world.</span></span>

### <a name="instructions"></a><span data-ttu-id="7b62e-250">Instructions</span><span class="sxs-lookup"><span data-stu-id="7b62e-250">Instructions</span></span>

* <span data-ttu-id="7b62e-251">Dans Unity, sélectionnez dans le menu supérieur **modifier > paramètres du projet > audio**</span><span class="sxs-lookup"><span data-stu-id="7b62e-251">In the Unity select from the top menu **Edit > Project Settings > Audio**</span></span>
* <span data-ttu-id="7b62e-252">Recherchez le paramètre de **plug-in Spatializer** et sélectionnez **MS HRTF Spatializer**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-252">Find the **Spatializer Plugin** setting and select **MS HRTF Spatializer**.</span></span>
* <span data-ttu-id="7b62e-253">À partir du dossier **hologrammes** , faites glisser l’objet **ambiance** sur l’objet **OrigamiCollection** dans le panneau hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="7b62e-253">From the **Holograms** folder, drag the **Ambience** object onto the **OrigamiCollection** object in the Hierarchy Panel.</span></span>
* <span data-ttu-id="7b62e-254">Sélectionnez **OrigamiCollection** et recherchez le composant **audio source** .</span><span class="sxs-lookup"><span data-stu-id="7b62e-254">Select **OrigamiCollection** and find the **Audio Source** component.</span></span> <span data-ttu-id="7b62e-255">Modifiez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="7b62e-255">Change these properties:</span></span>
  * <span data-ttu-id="7b62e-256">Vérifiez la propriété **spatial** .</span><span class="sxs-lookup"><span data-stu-id="7b62e-256">Check the **Spatialize** property.</span></span>
  * <span data-ttu-id="7b62e-257">Vérifiez la **lecture sur éveillé**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-257">Check the **Play On Awake**.</span></span>
  * <span data-ttu-id="7b62e-258">Remplacez **spatial Blend** par **3D** en faisant glisser le curseur vers la droite.</span><span class="sxs-lookup"><span data-stu-id="7b62e-258">Change **Spatial Blend** to **3D** by dragging the slider all the way to the right.</span></span>
  * <span data-ttu-id="7b62e-259">Vérifiez la propriété **Loop** .</span><span class="sxs-lookup"><span data-stu-id="7b62e-259">Check the **Loop** property.</span></span>
  * <span data-ttu-id="7b62e-260">Développez **paramètres audio 3D**, puis entrez **0,1** pour le **niveau Doppler**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-260">Expand **3D Sound Settings**, and enter **0.1** for **Doppler Level**.</span></span>
  * <span data-ttu-id="7b62e-261">Définissez **volume Rolloff** sur **Rolloff logarithmique**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-261">Set **Volume Rolloff** to **Logarithmic Rolloff**.</span></span>
  * <span data-ttu-id="7b62e-262">Définissez **distance maximale** sur **20**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-262">Set **Max Distance** to **20**.</span></span>
* <span data-ttu-id="7b62e-263">Dans le dossier **scripts** , créez un script nommé **SphereSounds**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-263">In the **Scripts** folder, create a script named **SphereSounds**.</span></span>
* <span data-ttu-id="7b62e-264">Faites glisser **SphereSounds** vers les objets **Sphere1** et **Sphere2** dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="7b62e-264">Drag **SphereSounds** to the **Sphere1** and **Sphere2** objects in the Hierarchy.</span></span>
* <span data-ttu-id="7b62e-265">Ouvrez **SphereSounds** dans Visual Studio, mettez à jour le code suivant et **Enregistrez All**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-265">Open **SphereSounds** in Visual Studio, update the following code and **Save All**.</span></span>

```cs
using UnityEngine;

public class SphereSounds : MonoBehaviour
{
    AudioSource impactAudioSource = null;
    AudioSource rollingAudioSource = null;

    bool rolling = false;

    void Start()
    {
        // Add an AudioSource component and set up some defaults
        impactAudioSource = gameObject.AddComponent<AudioSource>();
        impactAudioSource.playOnAwake = false;
        impactAudioSource.spatialize = true;
        impactAudioSource.spatialBlend = 1.0f;
        impactAudioSource.dopplerLevel = 0.0f;
        impactAudioSource.rolloffMode = AudioRolloffMode.Logarithmic;
        impactAudioSource.maxDistance = 20f;

        rollingAudioSource = gameObject.AddComponent<AudioSource>();
        rollingAudioSource.playOnAwake = false;
        rollingAudioSource.spatialize = true;
        rollingAudioSource.spatialBlend = 1.0f;
        rollingAudioSource.dopplerLevel = 0.0f;
        rollingAudioSource.rolloffMode = AudioRolloffMode.Logarithmic;
        rollingAudioSource.maxDistance = 20f;
        rollingAudioSource.loop = true;

        // Load the Sphere sounds from the Resources folder
        impactAudioSource.clip = Resources.Load<AudioClip>("Impact");
        rollingAudioSource.clip = Resources.Load<AudioClip>("Rolling");
    }

    // Occurs when this object starts colliding with another object
    void OnCollisionEnter(Collision collision)
    {
        // Play an impact sound if the sphere impacts strongly enough.
        if (collision.relativeVelocity.magnitude >= 0.1f)
        {
            impactAudioSource.Play();
        }
    }

    // Occurs each frame that this object continues to collide with another object
    void OnCollisionStay(Collision collision)
    {
        Rigidbody rigid = gameObject.GetComponent<Rigidbody>();

        // Play a rolling sound if the sphere is rolling fast enough.
        if (!rolling && rigid.velocity.magnitude >= 0.01f)
        {
            rolling = true;
            rollingAudioSource.Play();
        }
        // Stop the rolling sound if rolling slows down.
        else if (rolling && rigid.velocity.magnitude < 0.01f)
        {
            rolling = false;
            rollingAudioSource.Stop();
        }
    }

    // Occurs when this object stops colliding with another object
    void OnCollisionExit(Collision collision)
    {
        // Stop the rolling sound if the object falls off and stops colliding.
        if (rolling)
        {
            rolling = false;
            impactAudioSource.Stop();
            rollingAudioSource.Stop();
        }
    }
}
```

* <span data-ttu-id="7b62e-266">Enregistrez le script et revenez à Unity.</span><span class="sxs-lookup"><span data-stu-id="7b62e-266">Save the script, and return to Unity.</span></span>
* <span data-ttu-id="7b62e-267">Exportez, générez et déployez l’application sur l’émulateur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="7b62e-267">Export, build and deploy the app to the HoloLens emulator.</span></span>
* <span data-ttu-id="7b62e-268">Portez du casque pour obtenir un effet complet, et rapprochez-vous de la phase pour écouter les sons.</span><span class="sxs-lookup"><span data-stu-id="7b62e-268">Wear headphones to get the full effect, and move closer and further from the Stage to hear the sounds change.</span></span>

## <a name="chapter-6---spatial-mapping"></a><span data-ttu-id="7b62e-269">Chapitre 6-mappage spatial</span><span class="sxs-lookup"><span data-stu-id="7b62e-269">Chapter 6 - Spatial mapping</span></span>

>[!VIDEO https://www.youtube.com/embed/S-517Y63Cnk]

<span data-ttu-id="7b62e-270">Nous allons maintenant utiliser le [mappage spatial](spatial-mapping.md) pour placer la grille de jeux sur un objet réel dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="7b62e-270">Now we are going to use [spatial mapping](spatial-mapping.md) to place the game board on a real object in the real world.</span></span>

### <a name="objectives"></a><span data-ttu-id="7b62e-271">Objectifs</span><span class="sxs-lookup"><span data-stu-id="7b62e-271">Objectives</span></span>

* <span data-ttu-id="7b62e-272">Intégrez votre monde réel dans le monde virtuel.</span><span class="sxs-lookup"><span data-stu-id="7b62e-272">Bring your real world into the virtual world.</span></span>
* <span data-ttu-id="7b62e-273">Placez vos hologrammes là où ils vous intéressent le plus.</span><span class="sxs-lookup"><span data-stu-id="7b62e-273">Place your holograms where they matter most to you.</span></span>

### <a name="instructions"></a><span data-ttu-id="7b62e-274">Instructions</span><span class="sxs-lookup"><span data-stu-id="7b62e-274">Instructions</span></span>

* <span data-ttu-id="7b62e-275">Cliquez sur le dossier **hologrammes** dans le panneau projet.</span><span class="sxs-lookup"><span data-stu-id="7b62e-275">Click on the **Holograms** folder in the Project panel.</span></span>
* <span data-ttu-id="7b62e-276">Faites glisser la ressource de **mappage spatial** à la racine de la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-276">Drag the **Spatial Mapping** asset into the root of the **Hierarchy**.</span></span>
* <span data-ttu-id="7b62e-277">Cliquez sur l’objet **mappage spatial** dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="7b62e-277">Click on the **Spatial Mapping** object in the Hierarchy.</span></span>
* <span data-ttu-id="7b62e-278">Dans le **panneau Inspecteur**, modifiez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="7b62e-278">In the **Inspector panel**, change the following properties:</span></span>
  * <span data-ttu-id="7b62e-279">Cochez la case **dessiner des panneaux visuels** .</span><span class="sxs-lookup"><span data-stu-id="7b62e-279">Check the **Draw Visual Meshes** box.</span></span>
  * <span data-ttu-id="7b62e-280">Recherchez **matériel de dessin** , puis cliquez sur le cercle à droite.</span><span class="sxs-lookup"><span data-stu-id="7b62e-280">Locate **Draw Material** and click the circle on the right.</span></span> <span data-ttu-id="7b62e-281">Tapez «**Wireframe**» dans le champ de recherche en haut.</span><span class="sxs-lookup"><span data-stu-id="7b62e-281">Type "**wireframe**" into the search field at the top.</span></span> <span data-ttu-id="7b62e-282">Cliquez sur le résultat, puis fermez la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="7b62e-282">Click on the result and then close the window.</span></span>
* <span data-ttu-id="7b62e-283">Exportez, générez et déployez l’application sur l’émulateur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="7b62e-283">Export, build and deploy the app to the HoloLens emulator.</span></span>
* <span data-ttu-id="7b62e-284">Lorsque l’application s’exécute, une maille d’une salle de vie réelle scannée précédemment est rendue en filaire.</span><span class="sxs-lookup"><span data-stu-id="7b62e-284">When the app runs, a mesh of a previously scanned real-world living room will be rendered in wireframe.</span></span>
* <span data-ttu-id="7b62e-285">Regardez comment une sphère enchaînée va tomber à l’étage, et à l’étage !</span><span class="sxs-lookup"><span data-stu-id="7b62e-285">Watch how a rolling sphere will fall off the stage, and onto the floor!</span></span>

<span data-ttu-id="7b62e-286">Nous allons maintenant vous montrer comment déplacer le OrigamiCollection vers un nouvel emplacement :</span><span class="sxs-lookup"><span data-stu-id="7b62e-286">Now we'll show you how to move the OrigamiCollection to a new location:</span></span>

* <span data-ttu-id="7b62e-287">Dans le dossier **scripts** , créez un script nommé **TapToPlaceParent**.</span><span class="sxs-lookup"><span data-stu-id="7b62e-287">In the **Scripts** folder, create a script named **TapToPlaceParent**.</span></span>
* <span data-ttu-id="7b62e-288">Dans la **hiérarchie**, développez le **OrigamiCollection** et sélectionnez l’objet **stage** .</span><span class="sxs-lookup"><span data-stu-id="7b62e-288">In the **Hierarchy**, expand the **OrigamiCollection** and select the **Stage** object.</span></span>
* <span data-ttu-id="7b62e-289">Faites glisser le script **TapToPlaceParent** sur l’objet stage.</span><span class="sxs-lookup"><span data-stu-id="7b62e-289">Drag the **TapToPlaceParent** script onto the Stage object.</span></span>
* <span data-ttu-id="7b62e-290">Ouvrez le script **TapToPlaceParent** dans Visual Studio et mettez-le à jour comme suit :</span><span class="sxs-lookup"><span data-stu-id="7b62e-290">Open the **TapToPlaceParent** script in Visual Studio, and update it to be the following:</span></span>

```cs
using UnityEngine;

public class TapToPlaceParent : MonoBehaviour
{
    bool placing = false;

    // Called by GazeGestureManager when the user performs a Select gesture
    void OnSelect()
    {
        // On each Select gesture, toggle whether the user is in placing mode.
        placing = !placing;

        // If the user is in placing mode, display the spatial mapping mesh.
        if (placing)
        {
            SpatialMapping.Instance.DrawVisualMeshes = true;
        }
        // If the user is not in placing mode, hide the spatial mapping mesh.
        else
        {
            SpatialMapping.Instance.DrawVisualMeshes = false;
        }
    }

    // Update is called once per frame
    void Update()
    {
        // If the user is in placing mode,
        // update the placement to match the user's gaze.

        if (placing)
        {
            // Do a raycast into the world that will only hit the Spatial Mapping mesh.
            var headPosition = Camera.main.transform.position;
            var gazeDirection = Camera.main.transform.forward;

            RaycastHit hitInfo;
            if (Physics.Raycast(headPosition, gazeDirection, out hitInfo,
                30.0f, SpatialMapping.PhysicsRaycastMask))
            {
                // Move this object's parent object to
                // where the raycast hit the Spatial Mapping mesh.
                this.transform.parent.position = hitInfo.point;

                // Rotate this object's parent object to face the user.
                Quaternion toQuat = Camera.main.transform.localRotation;
                toQuat.x = 0;
                toQuat.z = 0;
                this.transform.parent.rotation = toQuat;
            }
        }
    }
}
```

* <span data-ttu-id="7b62e-291">Exporter, générer et déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="7b62e-291">Export, build and deploy the app.</span></span>
* <span data-ttu-id="7b62e-292">Vous devez maintenant être en mesure de placer le jeu à un emplacement spécifique par gazing, à l’aide du geste Select (**a ou de** l’espace), puis en le déplaçant vers un nouvel emplacement et en réutilisant le geste Select.</span><span class="sxs-lookup"><span data-stu-id="7b62e-292">Now you should now be able to place the game in a specific location by gazing at it, using the Select gesture (**A** or Spacebar) and then moving to a new location, and using the Select gesture again.</span></span>

## <a name="the-end"></a><span data-ttu-id="7b62e-293">La fin</span><span class="sxs-lookup"><span data-stu-id="7b62e-293">The end</span></span>

<span data-ttu-id="7b62e-294">Et c’est la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7b62e-294">And that's the end of this tutorial!</span></span>

<span data-ttu-id="7b62e-295">Vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="7b62e-295">You learned:</span></span>

* <span data-ttu-id="7b62e-296">Comment créer une application holographique dans Unity.</span><span class="sxs-lookup"><span data-stu-id="7b62e-296">How to create a holographic app in Unity.</span></span>
* <span data-ttu-id="7b62e-297">Comment utiliser le point de vue du regard, du mouvement, de la voix, des sons et du mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="7b62e-297">How to make use of gaze, gesture, voice, sounds, and spatial mapping.</span></span>
* <span data-ttu-id="7b62e-298">Comment générer et déployer une application à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b62e-298">How to build and deploy an app using Visual Studio.</span></span>

<span data-ttu-id="7b62e-299">Vous êtes maintenant prêt à commencer à créer vos propres applications holographiques !</span><span class="sxs-lookup"><span data-stu-id="7b62e-299">You are now ready to start creating your own holographic apps!</span></span>

## <a name="see-also"></a><span data-ttu-id="7b62e-300">Articles associés</span><span class="sxs-lookup"><span data-stu-id="7b62e-300">See also</span></span>

* [<span data-ttu-id="7b62e-301">MR Basics 101 : finaliser le projet avec l’appareil</span><span class="sxs-lookup"><span data-stu-id="7b62e-301">MR Basics 101: Complete project with device</span></span>](holograms-101.md)
* [<span data-ttu-id="7b62e-302">Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="7b62e-302">Gaze</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="7b62e-303">Pointer du regard vers l’avant et valider</span><span class="sxs-lookup"><span data-stu-id="7b62e-303">Head-gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="7b62e-304">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="7b62e-304">Voice input</span></span>](voice-input.md)
* [<span data-ttu-id="7b62e-305">Son spatial</span><span class="sxs-lookup"><span data-stu-id="7b62e-305">Spatial sound</span></span>](spatial-sound.md)
* [<span data-ttu-id="7b62e-306">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="7b62e-306">Spatial mapping</span></span>](spatial-mapping.md)
