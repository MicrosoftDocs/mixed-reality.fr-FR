---
title: Principes fondamentaux de M. 101E - projet complet avec l’émulateur
description: Suivez cette procédure pas à pas à l’aide de Unity, Visual Studio et HoloLens émulateur pour apprendre les notions d’une application holographique de codage.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: réalité mixte, réalité mixte Windows, HoloLens, HOLOGRAMME, émulateur didacticiel academy,
ms.openlocfilehash: 77f7d497396937bf471a69fa514cef84ab0b699d
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593987"
---
>[!NOTE]
><span data-ttu-id="3c0b0-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="3c0b0-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="3c0b0-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="3c0b0-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="3c0b0-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="3c0b0-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-basics-101e-complete-project-with-emulator"></a><span data-ttu-id="3c0b0-110">Principes de base MR 101E : Projet complet avec l’émulateur</span><span class="sxs-lookup"><span data-stu-id="3c0b0-110">MR Basics 101E: Complete project with emulator</span></span>

 >[!VIDEO https://www.youtube.com/embed/Xzm8_s05mm8]

<span data-ttu-id="3c0b0-111">Ce didacticiel vous guidera dans un projet complet, créé dans Unity, qui illustre les fonctionnalités de Windows Mixed Reality core, notamment HoloLens [les regards](gaze.md), [mouvements](gestures.md), [entréevoix](voice-input.md), [son spatial](spatial-sound.md) et [mappage spatial](spatial-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="3c0b0-111">This tutorial will walk you through a complete project, built in Unity, that demonstrates core Windows Mixed Reality features on HoloLens including [gaze](gaze.md), [gestures](gestures.md), [voice input](voice-input.md), [spatial sound](spatial-sound.md) and [spatial mapping](spatial-mapping.md).</span></span> <span data-ttu-id="3c0b0-112">Le didacticiel vous prendra environ une heure.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-112">The tutorial will take approximately 1 hour to complete.</span></span>

## <a name="device-support"></a><span data-ttu-id="3c0b0-113">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="3c0b0-113">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="3c0b0-114">Cours</span><span class="sxs-lookup"><span data-stu-id="3c0b0-114">Course</span></span></th><th style="width:150px"> <span data-ttu-id="3c0b0-115"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="3c0b0-115"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="3c0b0-116"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="3c0b0-116"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="3c0b0-117">Principes de base MR 101E : Projet complet avec l’émulateur</span><span class="sxs-lookup"><span data-stu-id="3c0b0-117">MR Basics 101E: Complete project with emulator</span></span></td><td style="text-align: center;"> <span data-ttu-id="3c0b0-118">✔️</span><span class="sxs-lookup"><span data-stu-id="3c0b0-118">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="3c0b0-119">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="3c0b0-119">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3c0b0-120">Prérequis</span><span class="sxs-lookup"><span data-stu-id="3c0b0-120">Prerequisites</span></span>

* <span data-ttu-id="3c0b0-121">Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="3c0b0-121">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>

### <a name="project-files"></a><span data-ttu-id="3c0b0-122">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="3c0b0-122">Project files</span></span>

* <span data-ttu-id="3c0b0-123">Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) requise par le projet.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-123">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) required by the project.</span></span><span data-ttu-id="3c0b0-124"> Nécessite Unity 2017.2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-124"> Requires Unity 2017.2 or later.</span></span>
  * <span data-ttu-id="3c0b0-125">Si vous avez besoin de prise en charge de Unity 5.6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).</span><span class="sxs-lookup"><span data-stu-id="3c0b0-125">If you still need Unity 5.6 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).</span></span>
  * <span data-ttu-id="3c0b0-126">Si vous avez besoin de prise en charge de Unity 5.5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).</span><span class="sxs-lookup"><span data-stu-id="3c0b0-126">If you still need Unity 5.5 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).</span></span>
  * <span data-ttu-id="3c0b0-127">Si vous avez besoin de prise en charge de Unity 5.4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).</span><span class="sxs-lookup"><span data-stu-id="3c0b0-127">If you still need Unity 5.4 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).</span></span>
* <span data-ttu-id="3c0b0-128">Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-128">Un-archive the files to your desktop or other easy to reach location.</span></span> <span data-ttu-id="3c0b0-129">Conservez le nom de dossier en tant que **Origami**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-129">Keep the folder name as **Origami**.</span></span>

>[!NOTE]
><span data-ttu-id="3c0b0-130">Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).</span><span class="sxs-lookup"><span data-stu-id="3c0b0-130">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).</span></span>

## <a name="chapter-1---holo-world"></a><span data-ttu-id="3c0b0-131">Chapitre 1 - « Holo » world</span><span class="sxs-lookup"><span data-stu-id="3c0b0-131">Chapter 1 - "Holo" world</span></span>

>[!VIDEO https://www.youtube.com/embed/qotpUpIQxVU]

<span data-ttu-id="3c0b0-132">Dans ce chapitre, nous le programme d’installation de notre premier projet Unity et les étapes à la build et processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-132">In this chapter, we'll setup our first Unity project and step through the build and deploy process.</span></span>

### <a name="objectives"></a><span data-ttu-id="3c0b0-133">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3c0b0-133">Objectives</span></span>

* <span data-ttu-id="3c0b0-134">Configurer Unity pour le développement HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-134">Set up Unity for holographic development.</span></span>
* <span data-ttu-id="3c0b0-135">Rendre un hologramme.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-135">Make a hologram.</span></span>
* <span data-ttu-id="3c0b0-136">Consultez un hologramme que vous avez apportées.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-136">See a hologram that you made.</span></span>

### <a name="instructions"></a><span data-ttu-id="3c0b0-137">Instructions</span><span class="sxs-lookup"><span data-stu-id="3c0b0-137">Instructions</span></span>

* <span data-ttu-id="3c0b0-138">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-138">Start Unity.</span></span>
* <span data-ttu-id="3c0b0-139">Sélectionnez **Open**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-139">Select **Open**.</span></span>
* <span data-ttu-id="3c0b0-140">Entrez l’emplacement que le **Origami** dossier vous précédemment non archivés.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-140">Enter location as the **Origami** folder you previously un-archived.</span></span>
* <span data-ttu-id="3c0b0-141">Sélectionnez **Origami** et cliquez sur **sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-141">Select **Origami** and click **Select Folder**.</span></span>
* <span data-ttu-id="3c0b0-142">Enregistrer la nouvelle scène : **Fichier** / **enregistrer la scène sous**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-142">Save the new scene: **File** / **Save Scene As**.</span></span>
* <span data-ttu-id="3c0b0-143">Nommez la scène **Origami** et appuyez sur la **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-143">Name the scene **Origami** and press the **Save** button.</span></span>

#### <a name="setup-the-main-camera"></a><span data-ttu-id="3c0b0-144">Le programme d’installation de la caméra principale</span><span class="sxs-lookup"><span data-stu-id="3c0b0-144">Setup the main camera</span></span>

* <span data-ttu-id="3c0b0-145">Dans le **hiérarchie panneau**, sélectionnez **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-145">In the **Hierarchy Panel**, select **Main Camera**.</span></span>
* <span data-ttu-id="3c0b0-146">Dans le **inspecteur** positionnez sa transformation **0,0,0**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-146">In the **Inspector** set its transform position to **0,0,0**.</span></span>
* <span data-ttu-id="3c0b0-147">Rechercher la **effacer les indicateurs** propriété et modifier la liste déroulante à partir de **Skybox** à **couleur unie**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-147">Find the **Clear Flags** property, and change the dropdown from **Skybox** to **Solid color**.</span></span>
* <span data-ttu-id="3c0b0-148">Cliquez sur le **arrière-plan** champ pour ouvrir un sélecteur de couleurs.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-148">Click on the **Background** field to open a color picker.</span></span>
* <span data-ttu-id="3c0b0-149">Définissez **R, G, B et A** à **0**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-149">Set **R, G, B, and A** to **0**.</span></span>

#### <a name="setup-the-scene"></a><span data-ttu-id="3c0b0-150">Le programme d’installation de la scène</span><span class="sxs-lookup"><span data-stu-id="3c0b0-150">Setup the scene</span></span>

* <span data-ttu-id="3c0b0-151">Dans le **hiérarchie panneau**, cliquez sur **créer** et **créer vide**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-151">In the **Hierarchy Panel**, click on **Create** and **Create Empty**.</span></span>
* <span data-ttu-id="3c0b0-152">Cliquez sur le nouveau **GameObject** et sélectionnez Renommer.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-152">Right-click the new **GameObject** and select Rename.</span></span> <span data-ttu-id="3c0b0-153">Renommer le GameObject à **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-153">Rename the GameObject to **OrigamiCollection**.</span></span>
* <span data-ttu-id="3c0b0-154">À partir de la **Vntana** dossier dans le **panneau projet**:</span><span class="sxs-lookup"><span data-stu-id="3c0b0-154">From the **Holograms** folder in the **Project Panel**:</span></span>
  * <span data-ttu-id="3c0b0-155">Faites glisser **étape** dans la hiérarchie soit un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-155">Drag **Stage** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
  * <span data-ttu-id="3c0b0-156">Faites glisser **Sphere1** dans la hiérarchie soit un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-156">Drag **Sphere1** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
  * <span data-ttu-id="3c0b0-157">Faites glisser **Sphere2** dans la hiérarchie soit un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-157">Drag **Sphere2** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
* <span data-ttu-id="3c0b0-158">Avec le bouton droit le **lumière directionnelle** de l’objet dans le **hiérarchie panneau** et sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-158">Right-click the **Directional Light** object in the **Hierarchy Panel** and select **Delete**.</span></span>
* <span data-ttu-id="3c0b0-159">À partir de la **hologrammes** dossier, faites glisser **lumières** à la racine de la **hiérarchie panneau**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-159">From the **Holograms** folder, drag **Lights** into the root of the **Hierarchy Panel**.</span></span>
* <span data-ttu-id="3c0b0-160">Dans le **hiérarchie**, sélectionnez le **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-160">In the **Hierarchy**, select the **OrigamiCollection**.</span></span>
* <span data-ttu-id="3c0b0-161">Dans le **inspecteur**, positionnez la transformation **0, -0,5, 2.0**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-161">In the **Inspector**, set the transform position to **0, -0.5, 2.0**.</span></span>
* <span data-ttu-id="3c0b0-162">Appuyez sur la **lire** bouton dans Unity pour afficher un aperçu votre hologrammes.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-162">Press the **Play** button in Unity to preview your holograms.</span></span>
* <span data-ttu-id="3c0b0-163">Vous devez voir les objets Origami dans la fenêtre d’aperçu.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-163">You should see the Origami objects in the preview window.</span></span>
* <span data-ttu-id="3c0b0-164">Appuyez sur **lire** une deuxième fois pour arrêter le mode d’aperçu.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-164">Press **Play** a second time to stop preview mode.</span></span>

#### <a name="export-the-project-from-unity-to-visual-studio"></a><span data-ttu-id="3c0b0-165">Exportez le projet à partir d’Unity pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c0b0-165">Export the project from Unity to Visual Studio</span></span>

* <span data-ttu-id="3c0b0-166">Dans, sélectionnez Unity **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-166">In Unity select **File > Build Settings**.</span></span>
* <span data-ttu-id="3c0b0-167">Sélectionnez **Windows Store** dans le **plateforme** liste et cliquez sur **plateforme de commutation**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-167">Select **Windows Store** in the **Platform** list and click **Switch Platform**.</span></span>
* <span data-ttu-id="3c0b0-168">Définissez **SDK** à **universelle 10** et **Type de Build** à **D3D**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-168">Set **SDK** to **Universal 10** and **Build Type** to **D3D**.</span></span>
* <span data-ttu-id="3c0b0-169">Vérifiez **Unity C# projets**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-169">Check **Unity C# Projects**.</span></span>
* <span data-ttu-id="3c0b0-170">Cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-170">Click **Add Open Scenes** to add the scene.</span></span>
* <span data-ttu-id="3c0b0-171">Cliquez sur **paramètres du lecteur...** .</span><span class="sxs-lookup"><span data-stu-id="3c0b0-171">Click **Player Settings...**.</span></span>
* <span data-ttu-id="3c0b0-172">Dans l’instruction select panneau Inspecteur le **logo du Windows Store**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-172">In the Inspector Panel select the **Windows Store logo**.</span></span> <span data-ttu-id="3c0b0-173">Puis sélectionnez **paramètres de publication**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-173">Then select **Publishing Settings**.</span></span>
* <span data-ttu-id="3c0b0-174">Dans le **fonctionnalités** section, sélectionnez le **Microphone** et **SpatialPerception** fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-174">In the **Capabilities** section, select the **Microphone** and **SpatialPerception** capabilities.</span></span>
* <span data-ttu-id="3c0b0-175">Dans la fenêtre Paramètres de Build, cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-175">Back in the Build Settings window, click **Build**.</span></span>
* <span data-ttu-id="3c0b0-176">Créer un **nouveau dossier** nommé « Application ».</span><span class="sxs-lookup"><span data-stu-id="3c0b0-176">Create a **New Folder** named "App".</span></span>
* <span data-ttu-id="3c0b0-177">Clic le **dossier application**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-177">Single click the **App Folder**.</span></span>
* <span data-ttu-id="3c0b0-178">Appuyez sur **sélectionnez dossier**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-178">Press **Select Folder**.</span></span>
* <span data-ttu-id="3c0b0-179">Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-179">When Unity is done, a File Explorer window will appear.</span></span>
* <span data-ttu-id="3c0b0-180">Ouvrez le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-180">Open the **App** folder.</span></span>
* <span data-ttu-id="3c0b0-181">Ouvrez le **Origami Visual Studio Solution**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-181">Open the **Origami Visual Studio Solution**.</span></span>
* <span data-ttu-id="3c0b0-182">À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **X86**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-182">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **X86**.</span></span>
  * <span data-ttu-id="3c0b0-183">Cliquez sur la flèche en regard du bouton de l’appareil, puis sélectionnez **HoloLens émulateur**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-183">Click on the arrow next to the Device button, and select **HoloLens Emulator**.</span></span>
  * <span data-ttu-id="3c0b0-184">Cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-184">Click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
  * <span data-ttu-id="3c0b0-185">Après un certain temps, l’émulateur démarre avec le projet Origami.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-185">After some time the emulator will start with the Origami project.</span></span> <span data-ttu-id="3c0b0-186">Lors du lancement d’abord le [émulateur](using-the-hololens-emulator.md), il peut prendre jusqu'à 15 minutes pour l’émulateur démarre.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-186">When first launching the [emulator](using-the-hololens-emulator.md), it can take as long as 15 minutes for the emulator to start up.</span></span> <span data-ttu-id="3c0b0-187">Une fois qu’il démarre, ne la fermez pas.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-187">Once it starts, do not close it.</span></span>

## <a name="chapter-2---gaze"></a><span data-ttu-id="3c0b0-188">Chapitre 2 - regards</span><span class="sxs-lookup"><span data-stu-id="3c0b0-188">Chapter 2 - Gaze</span></span>

>[!VIDEO https://www.youtube.com/embed/BPWTbAC210k]

<span data-ttu-id="3c0b0-189">Dans ce chapitre, nous allons introduire le premier des trois façons d’interagir avec votre hologrammes-- [les regards](gaze.md).</span><span class="sxs-lookup"><span data-stu-id="3c0b0-189">In this chapter, we are going to introduce the first of three ways of interacting with your holograms -- [gaze](gaze.md).</span></span>

### <a name="objectives"></a><span data-ttu-id="3c0b0-190">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3c0b0-190">Objectives</span></span>

* <span data-ttu-id="3c0b0-191">Visualiser votre regard à l’aide d’un curseur verrouillé de monde.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-191">Visualize your gaze using a world-locked cursor.</span></span>

### <a name="instructions"></a><span data-ttu-id="3c0b0-192">Instructions</span><span class="sxs-lookup"><span data-stu-id="3c0b0-192">Instructions</span></span>

* <span data-ttu-id="3c0b0-193">Revenez à votre projet Unity et fermer la fenêtre Paramètres de Build si elle est toujours ouverte.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-193">Go back to your Unity project, and close the Build Settings window if it's still open.</span></span>
* <span data-ttu-id="3c0b0-194">Sélectionnez le **Vntana** dossier dans le **panneau projet**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-194">Select the **Holograms** folder in the **Project panel**.</span></span>
* <span data-ttu-id="3c0b0-195">Faites glisser le **curseur** de l’objet dans le **Panneau de la hiérarchie** au niveau racine.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-195">Drag the **Cursor** object into the **Hierarchy panel** at the root level.</span></span>
* <span data-ttu-id="3c0b0-196">Double-cliquez sur le **curseur** objet effectue une examiner plus en détail.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-196">Double-click on the **Cursor** object to take a closer look at it.</span></span>
* <span data-ttu-id="3c0b0-197">Avec le bouton droit sur le **Scripts** dossier dans le panneau de configuration de projet.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-197">Right-click on the **Scripts** folder in the Project panel.</span></span>
* <span data-ttu-id="3c0b0-198">Cliquez sur le **créer** sous-menu.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-198">Click the **Create** sub-menu.</span></span>
* <span data-ttu-id="3c0b0-199">Sélectionnez  **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-199">Select **C# Script**.</span></span>
* <span data-ttu-id="3c0b0-200">Nommez le script **WorldCursor**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-200">Name the script **WorldCursor**.</span></span> <span data-ttu-id="3c0b0-201">Remarque: Le nom est sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-201">Note: The name is case-sensitive.</span></span> <span data-ttu-id="3c0b0-202">Vous n’avez pas besoin ajouter l’extension .cs.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-202">You do not need to add the .cs extension.</span></span>
* <span data-ttu-id="3c0b0-203">Sélectionnez le **curseur** de l’objet dans le **Panneau de la hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-203">Select the **Cursor** object in the **Hierarchy panel**.</span></span>
* <span data-ttu-id="3c0b0-204">Faites glisser et déposez le **WorldCursor** écrite dans le **panneau Inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-204">Drag and drop the **WorldCursor** script into the **Inspector panel**.</span></span>
* <span data-ttu-id="3c0b0-205">Double-cliquez sur le **WorldCursor** script pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-205">Double-click the **WorldCursor** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="3c0b0-206">Copiez et collez ce code dans **WorldCursor.cs** et **Enregistrer tout**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-206">Copy and paste this code into **WorldCursor.cs** and **Save All**.</span></span>

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

* <span data-ttu-id="3c0b0-207">Régénérer l’application à partir de **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-207">Rebuild the app from **File > Build Settings**.</span></span>
* <span data-ttu-id="3c0b0-208">Revenez à la solution Visual Studio utilisée précédemment pour déployer sur l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-208">Return to the Visual Studio solution previously used to deploy to the emulator.</span></span>
* <span data-ttu-id="3c0b0-209">Sélectionnez « Recharger All » lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-209">Select 'Reload All' when prompted.</span></span>
* <span data-ttu-id="3c0b0-210">Cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-210">Click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
* <span data-ttu-id="3c0b0-211">Utilisez la manette Xbox pour rechercher la scène.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-211">Use the Xbox controller to look around the scene.</span></span> <span data-ttu-id="3c0b0-212">Notez la façon dont le curseur interagit avec la forme d’objets.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-212">Notice how the cursor interacts with the shape of objects.</span></span>

## <a name="chapter-3---gestures"></a><span data-ttu-id="3c0b0-213">Chapitre 3 - mouvements</span><span class="sxs-lookup"><span data-stu-id="3c0b0-213">Chapter 3 - Gestures</span></span>

>[!VIDEO https://www.youtube.com/embed/6d-0RHeKHq4]

<span data-ttu-id="3c0b0-214">Dans ce chapitre, nous allons ajouter la prise en charge de [mouvements](gestures.md).</span><span class="sxs-lookup"><span data-stu-id="3c0b0-214">In this chapter, we'll add support for [gestures](gestures.md).</span></span> <span data-ttu-id="3c0b0-215">Lorsque l’utilisateur sélectionne une sphère de papier, nous allons rendre la sphère se répartissent en activant la gravité, à l’aide du moteur de physique d’Unity.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-215">When the user selects a paper sphere, we'll make the sphere fall by turning on gravity using Unity's physics engine.</span></span>

### <a name="objectives"></a><span data-ttu-id="3c0b0-216">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3c0b0-216">Objectives</span></span>

* <span data-ttu-id="3c0b0-217">Contrôler votre hologrammes avec le mouvement de sélection.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-217">Control your holograms with the Select gesture.</span></span>

### <a name="instructions"></a><span data-ttu-id="3c0b0-218">Instructions</span><span class="sxs-lookup"><span data-stu-id="3c0b0-218">Instructions</span></span>

<span data-ttu-id="3c0b0-219">Nous allons commencer en créant un script que peut détecter le mouvement de sélection.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-219">We'll start by creating a script than can detect the Select gesture.</span></span>

* <span data-ttu-id="3c0b0-220">Dans le **Scripts** dossier, créez un script nommé **GazeGestureManager**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-220">In the **Scripts** folder, create a script named **GazeGestureManager**.</span></span>
* <span data-ttu-id="3c0b0-221">Faites glisser le **GazeGestureManager** de script sur le **OrigamiCollection** objet dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-221">Drag the **GazeGestureManager** script onto the **OrigamiCollection** object in the Hierarchy.</span></span>
* <span data-ttu-id="3c0b0-222">Ouvrez le **GazeGestureManager** de script dans Visual Studio et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="3c0b0-222">Open the **GazeGestureManager** script in Visual Studio and add the following code:</span></span>

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

* <span data-ttu-id="3c0b0-223">Créer un autre script dans le dossier Scripts, cette fois nommée **SphereCommands**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-223">Create another script in the Scripts folder, this time named **SphereCommands**.</span></span>
* <span data-ttu-id="3c0b0-224">Développez le **OrigamiCollection** objet dans la vue de la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-224">Expand the **OrigamiCollection** object in the Hierarchy view.</span></span>
* <span data-ttu-id="3c0b0-225">Faites glisser le **SphereCommands** de script sur le **Sphere1** objet dans le volet de la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-225">Drag the **SphereCommands** script onto the **Sphere1** object in the Hierarchy panel.</span></span>
* <span data-ttu-id="3c0b0-226">Faites glisser le **SphereCommands** de script sur le **Sphere2** objet dans le volet de la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-226">Drag the **SphereCommands** script onto the **Sphere2** object in the Hierarchy panel.</span></span>
* <span data-ttu-id="3c0b0-227">Ouvrez le script dans Visual Studio pour la modification et remplacez le code par défaut avec ce :</span><span class="sxs-lookup"><span data-stu-id="3c0b0-227">Open the script in Visual Studio for editing, and replace the default code with this:</span></span>

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

* <span data-ttu-id="3c0b0-228">Exporter, générer et déployer l’application sur l’émulateur de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-228">Export, build and deploy the app to the HoloLens emulator.</span></span>
* <span data-ttu-id="3c0b0-229">Regardez autour de la scène et centrer sur l’un de la couleur des sphères.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-229">Look around the scene, and center on one of the spheres.</span></span>
* <span data-ttu-id="3c0b0-230">Appuyez sur la **A** bouton sur le contrôleur Xbox ou appuyez sur la barre d’espace pour simuler le mouvement de sélection.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-230">Press the **A** button on the Xbox controller or press the Spacebar to simulate the Select gesture.</span></span>

## <a name="chapter-4---voice"></a><span data-ttu-id="3c0b0-231">Chapitre 4 - Voice</span><span class="sxs-lookup"><span data-stu-id="3c0b0-231">Chapter 4 - Voice</span></span>

>[!VIDEO https://www.youtube.com/embed/LxbOhnd2_GM]

<span data-ttu-id="3c0b0-232">Dans ce chapitre, nous allons ajouter la prise en charge pour deux [commandes vocales](voice-input.md): « Réinitialisation world » pour retourne les sphères supprimés à leur emplacement d’origine et la « Sphère de dépôt » pour rendre la sphère appartiennent.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-232">In this chapter, we'll add support for two [voice commands](voice-input.md): "Reset world" to returns the dropped spheres to their original location, and "Drop sphere" to make the sphere fall.</span></span>

### <a name="objectives"></a><span data-ttu-id="3c0b0-233">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3c0b0-233">Objectives</span></span>

* <span data-ttu-id="3c0b0-234">Ajouter des commandes vocales qui écoutent toujours en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-234">Add voice commands that always listen in the background.</span></span>
* <span data-ttu-id="3c0b0-235">Créer un hologramme qui réagit à une commande vocale.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-235">Create a hologram that reacts to a voice command.</span></span>

### <a name="instructions"></a><span data-ttu-id="3c0b0-236">Instructions</span><span class="sxs-lookup"><span data-stu-id="3c0b0-236">Instructions</span></span>

* <span data-ttu-id="3c0b0-237">Dans le **Scripts** dossier, créez un script nommé **SpeechManager**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-237">In the **Scripts** folder, create a script named **SpeechManager**.</span></span>
* <span data-ttu-id="3c0b0-238">Faites glisser le **SpeechManager** de script sur le **OrigamiCollection** objet dans la hiérarchie</span><span class="sxs-lookup"><span data-stu-id="3c0b0-238">Drag the **SpeechManager** script onto the **OrigamiCollection** object in the Hierarchy</span></span>
* <span data-ttu-id="3c0b0-239">Ouvrez le **SpeechManager** script dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-239">Open the **SpeechManager** script in Visual Studio.</span></span>
* <span data-ttu-id="3c0b0-240">Copiez et collez ce code dans **SpeechManager.cs** et **Enregistrer tout**:</span><span class="sxs-lookup"><span data-stu-id="3c0b0-240">Copy and paste this code into **SpeechManager.cs** and **Save All**:</span></span>

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

* <span data-ttu-id="3c0b0-241">Ouvrez le **SphereCommands** script dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-241">Open the **SphereCommands** script in Visual Studio.</span></span>
* <span data-ttu-id="3c0b0-242">Mettre à jour le script comme suit :</span><span class="sxs-lookup"><span data-stu-id="3c0b0-242">Update the script to read as follows:</span></span>

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

* <span data-ttu-id="3c0b0-243">Exporter, générer et déployer l’application sur l’émulateur de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-243">Export, build and deploy the app to the HoloLens emulator.</span></span>
* <span data-ttu-id="3c0b0-244">L’émulateur prendra en charge microphone de votre PC et répondre à votre voix : ajuster la vue de sorte que le curseur se trouve sur l’un de la couleur des sphères et dire « Drop sphère ».</span><span class="sxs-lookup"><span data-stu-id="3c0b0-244">The emulator will support your PC's microphone and respond to your voice: adjust the view so the cursor is on one of the spheres, and say "Drop Sphere".</span></span>
* <span data-ttu-id="3c0b0-245">Par exemple «**World réinitialiser**» pour les ramener dans leur position initiale.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-245">Say "**Reset World**" to bring them back to their initial positions.</span></span>

## <a name="chapter-5---spatial-sound"></a><span data-ttu-id="3c0b0-246">Chapitre 5 - son Spatial</span><span class="sxs-lookup"><span data-stu-id="3c0b0-246">Chapter 5 - Spatial sound</span></span>

>[!VIDEO https://www.youtube.com/embed/Xc3C4VA10w4]

<span data-ttu-id="3c0b0-247">Dans ce chapitre, nous allons ajouter de la musique à l’application et ensuite déclencher effets sonores sur certaines actions.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-247">In this chapter, we'll add music to the app, and then trigger sound effects on certain actions.</span></span> <span data-ttu-id="3c0b0-248">Nous allons utiliser [son spatial](spatial-sound.md) afin de donner des sons à un emplacement spécifique dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-248">We'll be using [spatial sound](spatial-sound.md) to give sounds a specific location in 3D space.</span></span>

### <a name="objectives"></a><span data-ttu-id="3c0b0-249">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3c0b0-249">Objectives</span></span>

* <span data-ttu-id="3c0b0-250">Écoutez hologrammes dans votre monde.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-250">Hear holograms in your world.</span></span>

### <a name="instructions"></a><span data-ttu-id="3c0b0-251">Instructions</span><span class="sxs-lookup"><span data-stu-id="3c0b0-251">Instructions</span></span>

* <span data-ttu-id="3c0b0-252">Dans l’instruction select dans le menu supérieur Unity **Modifier > Paramètres du projet > Audio**</span><span class="sxs-lookup"><span data-stu-id="3c0b0-252">In the Unity select from the top menu **Edit > Project Settings > Audio**</span></span>
* <span data-ttu-id="3c0b0-253">Rechercher la **plug-in spatial** paramètre et sélectionnez **MS HRTF Spatializer**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-253">Find the **Spatializer Plugin** setting and select **MS HRTF Spatializer**.</span></span>
* <span data-ttu-id="3c0b0-254">À partir de la **hologrammes** dossier, faites glisser le **ambiance** de l’objet sur le **OrigamiCollection** objet dans le volet de la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-254">From the **Holograms** folder, drag the **Ambience** object onto the **OrigamiCollection** object in the Hierarchy Panel.</span></span>
* <span data-ttu-id="3c0b0-255">Sélectionnez **OrigamiCollection** et recherchez le **Audio Source** composant.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-255">Select **OrigamiCollection** and find the **Audio Source** component.</span></span> <span data-ttu-id="3c0b0-256">Modifier ces propriétés :</span><span class="sxs-lookup"><span data-stu-id="3c0b0-256">Change these properties:</span></span>
  * <span data-ttu-id="3c0b0-257">Vérifier le **Spatialize** propriété.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-257">Check the **Spatialize** property.</span></span>
  * <span data-ttu-id="3c0b0-258">Vérifier le **jouer sur éveillés**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-258">Check the **Play On Awake**.</span></span>
  * <span data-ttu-id="3c0b0-259">Modification **Blend Spatial** à **3D** en faisant glisser le curseur complètement à droite.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-259">Change **Spatial Blend** to **3D** by dragging the slider all the way to the right.</span></span>
  * <span data-ttu-id="3c0b0-260">Vérifier le **boucle** propriété.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-260">Check the **Loop** property.</span></span>
  * <span data-ttu-id="3c0b0-261">Développez **les paramètres audio 3D**, puis entrez **0.1** pour **niveau Doppler**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-261">Expand **3D Sound Settings**, and enter **0.1** for **Doppler Level**.</span></span>
  * <span data-ttu-id="3c0b0-262">Définissez **Volume écrêtage** à **écrêtage logarithmique**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-262">Set **Volume Rolloff** to **Logarithmic Rolloff**.</span></span>
  * <span data-ttu-id="3c0b0-263">Définissez **Max Distance** à **20**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-263">Set **Max Distance** to **20**.</span></span>
* <span data-ttu-id="3c0b0-264">Dans le **Scripts** dossier, créez un script nommé **SphereSounds**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-264">In the **Scripts** folder, create a script named **SphereSounds**.</span></span>
* <span data-ttu-id="3c0b0-265">Faites glisser **SphereSounds** à la **Sphere1** et **Sphere2** objets dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-265">Drag **SphereSounds** to the **Sphere1** and **Sphere2** objects in the Hierarchy.</span></span>
* <span data-ttu-id="3c0b0-266">Ouvrez **SphereSounds** dans Visual Studio, mettre à jour le code suivant et **Enregistrer tout**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-266">Open **SphereSounds** in Visual Studio, update the following code and **Save All**.</span></span>

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

* <span data-ttu-id="3c0b0-267">Enregistrer le script et revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-267">Save the script, and return to Unity.</span></span>
* <span data-ttu-id="3c0b0-268">Exporter, générer et déployer l’application sur l’émulateur de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-268">Export, build and deploy the app to the HoloLens emulator.</span></span>
* <span data-ttu-id="3c0b0-269">Porter un casque pour obtenir l’effet et déplacer le plus proche et plus éloigné de la phase d’entendre les sons à modifier.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-269">Wear headphones to get the full effect, and move closer and further from the Stage to hear the sounds change.</span></span>

## <a name="chapter-6---spatial-mapping"></a><span data-ttu-id="3c0b0-270">Mappage du chapitre 6 – Spatial</span><span class="sxs-lookup"><span data-stu-id="3c0b0-270">Chapter 6 - Spatial mapping</span></span>

>[!VIDEO https://www.youtube.com/embed/S-517Y63Cnk]

<span data-ttu-id="3c0b0-271">Maintenant nous allons utiliser [mappage spatial](spatial-mapping.md) pour placer le plateau de jeu sur un objet réel dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-271">Now we are going to use [spatial mapping](spatial-mapping.md) to place the game board on a real object in the real world.</span></span>

### <a name="objectives"></a><span data-ttu-id="3c0b0-272">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3c0b0-272">Objectives</span></span>

* <span data-ttu-id="3c0b0-273">Placez votre monde réel dans le monde virtuel.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-273">Bring your real world into the virtual world.</span></span>
* <span data-ttu-id="3c0b0-274">Placez votre hologrammes où ils vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-274">Place your holograms where they matter most to you.</span></span>

### <a name="instructions"></a><span data-ttu-id="3c0b0-275">Instructions</span><span class="sxs-lookup"><span data-stu-id="3c0b0-275">Instructions</span></span>

* <span data-ttu-id="3c0b0-276">Cliquez sur le **hologrammes** dossier dans le panneau de configuration de projet.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-276">Click on the **Holograms** folder in the Project panel.</span></span>
* <span data-ttu-id="3c0b0-277">Faites glisser le **mappage Spatial** actif à la racine de la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-277">Drag the **Spatial Mapping** asset into the root of the **Hierarchy**.</span></span>
* <span data-ttu-id="3c0b0-278">Cliquez sur le **mappage Spatial** objet dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-278">Click on the **Spatial Mapping** object in the Hierarchy.</span></span>
* <span data-ttu-id="3c0b0-279">Dans le **panneau Inspecteur**, modifiez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="3c0b0-279">In the **Inspector panel**, change the following properties:</span></span>
  * <span data-ttu-id="3c0b0-280">Vérifier le **dessiner les maillages Visual** boîte.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-280">Check the **Draw Visual Meshes** box.</span></span>
  * <span data-ttu-id="3c0b0-281">Recherchez **dessiner un matériau** et cliquez sur le cercle sur la droite.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-281">Locate **Draw Material** and click the circle on the right.</span></span> <span data-ttu-id="3c0b0-282">Type «**filaire**» dans le champ de recherche en haut.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-282">Type "**wireframe**" into the search field at the top.</span></span> <span data-ttu-id="3c0b0-283">Cliquez sur le résultat, puis fermez la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-283">Click on the result and then close the window.</span></span>
* <span data-ttu-id="3c0b0-284">Exporter, générer et déployer l’application sur l’émulateur de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-284">Export, build and deploy the app to the HoloLens emulator.</span></span>
* <span data-ttu-id="3c0b0-285">Lorsque l’application s’exécute, une maille d’un salon réalistes précédemment analysé s’affichera en filaire.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-285">When the app runs, a mesh of a previously scanned real-world living room will be rendered in wireframe.</span></span>
* <span data-ttu-id="3c0b0-286">Regardez comment une sphère propagée tombera hors de la scène et sur le sol !</span><span class="sxs-lookup"><span data-stu-id="3c0b0-286">Watch how a rolling sphere will fall off the stage, and onto the floor!</span></span>

<span data-ttu-id="3c0b0-287">Maintenant nous allons vous montrer comment déplacer la OrigamiCollection vers un nouvel emplacement :</span><span class="sxs-lookup"><span data-stu-id="3c0b0-287">Now we'll show you how to move the OrigamiCollection to a new location:</span></span>

* <span data-ttu-id="3c0b0-288">Dans le **Scripts** dossier, créez un script nommé **TapToPlaceParent**.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-288">In the **Scripts** folder, create a script named **TapToPlaceParent**.</span></span>
* <span data-ttu-id="3c0b0-289">Dans le **hiérarchie**, développez le **OrigamiCollection** et sélectionnez le **étape** objet.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-289">In the **Hierarchy**, expand the **OrigamiCollection** and select the **Stage** object.</span></span>
* <span data-ttu-id="3c0b0-290">Faites glisser le **TapToPlaceParent** script sur l’objet de la scène.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-290">Drag the **TapToPlaceParent** script onto the Stage object.</span></span>
* <span data-ttu-id="3c0b0-291">Ouvrez le **TapToPlaceParent** de script dans Visual Studio et mettre à jour pour être ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="3c0b0-291">Open the **TapToPlaceParent** script in Visual Studio, and update it to be the following:</span></span>

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

* <span data-ttu-id="3c0b0-292">Exporter, créer et déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-292">Export, build and deploy the app.</span></span>
* <span data-ttu-id="3c0b0-293">Vous devez désormais maintenant être en mesure de placer le jeu dans un emplacement spécifique par gazing à elle, à l’aide du mouvement sélectionnez (**A** ou espace) et déplacer vers un nouvel emplacement, puis à l’aide du mouvement sélectionnez à nouveau.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-293">Now you should now be able to place the game in a specific location by gazing at it, using the Select gesture (**A** or Spacebar) and then moving to a new location, and using the Select gesture again.</span></span>

## <a name="the-end"></a><span data-ttu-id="3c0b0-294">La fin</span><span class="sxs-lookup"><span data-stu-id="3c0b0-294">The end</span></span>

<span data-ttu-id="3c0b0-295">Et c’est la fin de ce didacticiel !</span><span class="sxs-lookup"><span data-stu-id="3c0b0-295">And that's the end of this tutorial!</span></span>

<span data-ttu-id="3c0b0-296">Vous avez appris :</span><span class="sxs-lookup"><span data-stu-id="3c0b0-296">You learned:</span></span>

* <span data-ttu-id="3c0b0-297">Comment créer une application HOLOGRAPHIQUE dans Unity.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-297">How to create a holographic app in Unity.</span></span>
* <span data-ttu-id="3c0b0-298">Comment rendre l’utilisation des regards, mouvement, voix, sons et mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-298">How to make use of gaze, gesture, voice, sounds, and spatial mapping.</span></span>
* <span data-ttu-id="3c0b0-299">Comment créer et déployer une application à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c0b0-299">How to build and deploy an app using Visual Studio.</span></span>

<span data-ttu-id="3c0b0-300">Vous êtes maintenant prêt à commencer à créer vos propres applications HOLOGRAPHIQUE !</span><span class="sxs-lookup"><span data-stu-id="3c0b0-300">You are now ready to start creating your own holographic apps!</span></span>

## <a name="see-also"></a><span data-ttu-id="3c0b0-301">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3c0b0-301">See also</span></span>

* [<span data-ttu-id="3c0b0-302">Principes de base MR 101 : Projet complet avec l’appareil</span><span class="sxs-lookup"><span data-stu-id="3c0b0-302">MR Basics 101: Complete project with device</span></span>](holograms-101.md)
* [<span data-ttu-id="3c0b0-303">Gaze</span><span class="sxs-lookup"><span data-stu-id="3c0b0-303">Gaze</span></span>](gaze.md)
* [<span data-ttu-id="3c0b0-304">Mouvements</span><span class="sxs-lookup"><span data-stu-id="3c0b0-304">Gestures</span></span>](gestures.md)
* [<span data-ttu-id="3c0b0-305">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="3c0b0-305">Voice input</span></span>](voice-input.md)
* [<span data-ttu-id="3c0b0-306">Son spatial</span><span class="sxs-lookup"><span data-stu-id="3c0b0-306">Spatial sound</span></span>](spatial-sound.md)
* [<span data-ttu-id="3c0b0-307">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="3c0b0-307">Spatial mapping</span></span>](spatial-mapping.md)
