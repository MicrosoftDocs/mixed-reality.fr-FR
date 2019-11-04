---
title: Notions de base de m. 101-finaliser le projet avec l’appareil
description: Suivez cette procédure pas à pas de codage à l’aide d’Unity, Visual Studio et HoloLens pour apprendre les principes fondamentaux de Windows Mixed Reality.
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: réalité mixte, Windows Mixed Reality, HoloLens, hologramme, Academy, didacticiel
ms.openlocfilehash: 456aeea88b0d7f51acb52156d8139ec2df06883a
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73434721"
---
>[!NOTE]
><span data-ttu-id="2be7e-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="2be7e-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="2be7e-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="2be7e-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="2be7e-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="2be7e-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="2be7e-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2be7e-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="2be7e-108">[Une nouvelle série de didacticiels](mrlearning-base.md) a été publiée pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="2be7e-108">[A new series of tutorials](mrlearning-base.md) has been posted for HoloLens 2.</span></span>

<br>

# <a name="mr-basics-101-complete-project-with-device"></a><span data-ttu-id="2be7e-109">MR Basics 101 : finaliser le projet avec l’appareil</span><span class="sxs-lookup"><span data-stu-id="2be7e-109">MR Basics 101: Complete project with device</span></span>

<br>

>[!VIDEO https://www.youtube.com/embed/XKIIEC5BMWg]

<span data-ttu-id="2be7e-110">Ce didacticiel vous guide tout au long d’un projet complet, Unity, qui illustre les fonctionnalités de base de la réalité mixte Windows sur HoloLens [, y compris](gaze-and-commit.md)le point de présence, les [gestes](gaze-and-commit.md#composite-gestures), l' [entrée vocale](voice-input.md), le [son spatial](spatial-sound.md) et le [mappage spatial](spatial-mapping.md) .</span><span class="sxs-lookup"><span data-stu-id="2be7e-110">This tutorial will walk you through a complete project, built in Unity, that demonstrates core Windows Mixed Reality features on HoloLens including [gaze](gaze-and-commit.md), [gestures](gaze-and-commit.md#composite-gestures), [voice input](voice-input.md), [spatial sound](spatial-sound.md) and [spatial mapping](spatial-mapping.md).</span></span>

<span data-ttu-id="2be7e-111">Le didacticiel prendra environ 1 heure.</span><span class="sxs-lookup"><span data-stu-id="2be7e-111">The tutorial will take approximately 1 hour to complete.</span></span>

## <a name="device-support"></a><span data-ttu-id="2be7e-112">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="2be7e-112">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="2be7e-113">Course</span><span class="sxs-lookup"><span data-stu-id="2be7e-113">Course</span></span></th><th style="width:150px"> <span data-ttu-id="2be7e-114"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="2be7e-114"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="2be7e-115"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="2be7e-115"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="2be7e-116">MR Basics 101 : finaliser le projet avec l’appareil</span><span class="sxs-lookup"><span data-stu-id="2be7e-116">MR Basics 101: Complete project with device</span></span></td><td style="text-align: center;"> <span data-ttu-id="2be7e-117">✔️</span><span class="sxs-lookup"><span data-stu-id="2be7e-117">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="2be7e-118">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="2be7e-118">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2be7e-119">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="2be7e-119">Prerequisites</span></span>

* <span data-ttu-id="2be7e-120">Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="2be7e-120">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="2be7e-121">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="2be7e-121">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="2be7e-122">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="2be7e-122">Project files</span></span>

* <span data-ttu-id="2be7e-123">Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) requis par le projet.</span><span class="sxs-lookup"><span data-stu-id="2be7e-123">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) required by the project.</span></span><span data-ttu-id="2be7e-124"> Requiert Unity 2017,2 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2be7e-124"> Requires Unity 2017.2 or later.</span></span>
  * <span data-ttu-id="2be7e-125">Si vous avez encore besoin de la prise en charge d’Unity 5,6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).</span><span class="sxs-lookup"><span data-stu-id="2be7e-125">If you still need Unity 5.6 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).</span></span>
  * <span data-ttu-id="2be7e-126">Si vous avez encore besoin de la prise en charge d’Unity 5,5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).</span><span class="sxs-lookup"><span data-stu-id="2be7e-126">If you still need Unity 5.5 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).</span></span>
  * <span data-ttu-id="2be7e-127">Si vous avez encore besoin de la prise en charge d’Unity 5,4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).</span><span class="sxs-lookup"><span data-stu-id="2be7e-127">If you still need Unity 5.4 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).</span></span>
* <span data-ttu-id="2be7e-128">Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.</span><span class="sxs-lookup"><span data-stu-id="2be7e-128">Un-archive the files to your desktop or other easy to reach location.</span></span> <span data-ttu-id="2be7e-129">Conservez le nom du dossier **origami**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-129">Keep the folder name as **Origami**.</span></span>

>[!NOTE]
><span data-ttu-id="2be7e-130">Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).</span><span class="sxs-lookup"><span data-stu-id="2be7e-130">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).</span></span>

## <a name="chapter-1---holo-world"></a><span data-ttu-id="2be7e-131">Chapitre 1-monde « Holo »</span><span class="sxs-lookup"><span data-stu-id="2be7e-131">Chapter 1 - "Holo" world</span></span>

>[!VIDEO https://www.youtube.com/embed/PmtZGjYFroY]

<span data-ttu-id="2be7e-132">Dans ce chapitre, nous allons configurer notre premier projet Unity et effectuer un pas à pas détaillé dans le processus de création et de déploiement.</span><span class="sxs-lookup"><span data-stu-id="2be7e-132">In this chapter, we'll setup our first Unity project and step through the build and deploy process.</span></span>

### <a name="objectives"></a><span data-ttu-id="2be7e-133">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2be7e-133">Objectives</span></span>

* <span data-ttu-id="2be7e-134">Configurez Unity pour le développement holographique.</span><span class="sxs-lookup"><span data-stu-id="2be7e-134">Set up Unity for holographic development.</span></span>
* <span data-ttu-id="2be7e-135">Créez un hologramme.</span><span class="sxs-lookup"><span data-stu-id="2be7e-135">Make a hologram.</span></span>
* <span data-ttu-id="2be7e-136">Consultez un hologramme que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="2be7e-136">See a hologram that you made.</span></span>

### <a name="instructions"></a><span data-ttu-id="2be7e-137">Instructions</span><span class="sxs-lookup"><span data-stu-id="2be7e-137">Instructions</span></span>

* <span data-ttu-id="2be7e-138">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="2be7e-138">Start Unity.</span></span>
* <span data-ttu-id="2be7e-139">Sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-139">Select **Open**.</span></span>
* <span data-ttu-id="2be7e-140">Entrez l’emplacement du dossier **origami** que vous avez précédemment désinstallé.</span><span class="sxs-lookup"><span data-stu-id="2be7e-140">Enter location as the **Origami** folder you previously un-archived.</span></span>
* <span data-ttu-id="2be7e-141">Sélectionnez **origami** , puis cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-141">Select **Origami** and click **Select Folder**.</span></span>
* <span data-ttu-id="2be7e-142">Étant donné que le projet **origami** ne contient pas de scène, enregistrez la scène par défaut vide dans un nouveau fichier à l’aide de : **file** / **enregistrer la scène sous**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-142">Since the **Origami** project does not contain a scene, save the empty default scene to a new file using: **File** / **Save Scene As**.</span></span>
* <span data-ttu-id="2be7e-143">Nommez le nouvel **origami** de scène et appuyez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2be7e-143">Name the new scene **Origami** and press the **Save** button.</span></span>

#### <a name="setup-the-main-virtual-camera"></a><span data-ttu-id="2be7e-144">Configurer la caméra virtuelle principale</span><span class="sxs-lookup"><span data-stu-id="2be7e-144">Setup the main virtual camera</span></span>

* <span data-ttu-id="2be7e-145">Dans le **panneau hiérarchie**, sélectionnez **caméra principale**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-145">In the **Hierarchy Panel**, select **Main Camera**.</span></span>
* <span data-ttu-id="2be7e-146">Dans l' **inspecteur** , définissez sa position de transformation sur **0, 0,** 0.</span><span class="sxs-lookup"><span data-stu-id="2be7e-146">In the **Inspector** set its transform position to **0,0,0**.</span></span>
* <span data-ttu-id="2be7e-147">Recherchez la propriété **effacer les indicateurs** et remplacez la liste déroulante **skybox** par **couleur unie**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-147">Find the **Clear Flags** property, and change the dropdown from **Skybox** to **Solid color**.</span></span>
* <span data-ttu-id="2be7e-148">Cliquez sur le champ **arrière-plan** pour ouvrir un sélecteur de couleurs.</span><span class="sxs-lookup"><span data-stu-id="2be7e-148">Click on the **Background** field to open a color picker.</span></span>
* <span data-ttu-id="2be7e-149">Affectez **R, G, B et A** à **0**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-149">Set **R, G, B, and A** to **0**.</span></span>

#### <a name="setup-the-scene"></a><span data-ttu-id="2be7e-150">Configurer la scène</span><span class="sxs-lookup"><span data-stu-id="2be7e-150">Setup the scene</span></span>

* <span data-ttu-id="2be7e-151">Dans le **volet hiérarchie**, cliquez sur **créer** et **créez un vide**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-151">In the **Hierarchy Panel**, click on **Create** and **Create Empty**.</span></span>
* <span data-ttu-id="2be7e-152">Cliquez avec le bouton droit sur le nouveau **gameobject** , puis sélectionnez Renommer.</span><span class="sxs-lookup"><span data-stu-id="2be7e-152">Right-click the new **GameObject** and select Rename.</span></span> <span data-ttu-id="2be7e-153">Renommez GameObject en **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-153">Rename the GameObject to **OrigamiCollection**.</span></span>
* <span data-ttu-id="2be7e-154">Dans le dossier **hologrammes** du panneau projet (développez actifs et sélectionnez hologrammes ou double-cliquez sur le dossier hologrammes dans le panneau projet) :</span><span class="sxs-lookup"><span data-stu-id="2be7e-154">From the **Holograms** folder in the Project Panel (expand Assets and select Holograms or double click the Holograms folder in the Project Panel):</span></span>
  * <span data-ttu-id="2be7e-155">Faites glisser **étape** dans la hiérarchie pour être un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-155">Drag **Stage** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
  * <span data-ttu-id="2be7e-156">Faites glisser **Sphere1** dans la hiérarchie pour être un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-156">Drag **Sphere1** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
  * <span data-ttu-id="2be7e-157">Faites glisser **Sphere2** dans la hiérarchie pour être un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-157">Drag **Sphere2** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
* <span data-ttu-id="2be7e-158">Cliquez avec le bouton droit sur l’objet **Light directionnel** dans le **panneau hiérarchie** , puis sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-158">Right-click the **Directional Light** object in the **Hierarchy Panel** and select **Delete**.</span></span>
* <span data-ttu-id="2be7e-159">À partir du dossier **hologrammes** , faites glisser **Lights** à la racine du **panneau de hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-159">From the **Holograms** folder, drag **Lights** into the root of the **Hierarchy Panel**.</span></span>
* <span data-ttu-id="2be7e-160">Dans la **hiérarchie**, sélectionnez **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-160">In the **Hierarchy**, select the **OrigamiCollection**.</span></span>
* <span data-ttu-id="2be7e-161">Dans l' **inspecteur**, définissez la position de la transformation sur **0,-0,5, 2,0**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-161">In the **Inspector**, set the transform position to **0, -0.5, 2.0**.</span></span>
* <span data-ttu-id="2be7e-162">Appuyez sur le bouton de **lecture** dans Unity pour afficher un aperçu de vos hologrammes.</span><span class="sxs-lookup"><span data-stu-id="2be7e-162">Press the **Play** button in Unity to preview your holograms.</span></span>
* <span data-ttu-id="2be7e-163">Les objets origami doivent apparaître dans la fenêtre d’aperçu.</span><span class="sxs-lookup"><span data-stu-id="2be7e-163">You should see the Origami objects in the preview window.</span></span>
* <span data-ttu-id="2be7e-164">Appuyez sur **lecture** une deuxième fois pour arrêter le mode aperçu.</span><span class="sxs-lookup"><span data-stu-id="2be7e-164">Press **Play** a second time to stop preview mode.</span></span>

#### <a name="export-the-project-from-unity-to-visual-studio"></a><span data-ttu-id="2be7e-165">Exporter le projet d’Unity vers Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2be7e-165">Export the project from Unity to Visual Studio</span></span>

* <span data-ttu-id="2be7e-166">Dans Unity, sélectionnez **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-166">In Unity select **File > Build Settings**.</span></span>
* <span data-ttu-id="2be7e-167">Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur **basculer la plateforme**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-167">Select **Universal Windows Platform** in the **Platform** list and click **Switch Platform**.</span></span>
* <span data-ttu-id="2be7e-168">Affectez à **SDK** la valeur **Universal 10** et **type de build** la valeur **D3D**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-168">Set **SDK** to **Universal 10** and **Build Type** to **D3D**.</span></span>
* <span data-ttu-id="2be7e-169">Vérifiez **les C# projets Unity**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-169">Check **Unity C# Projects**.</span></span>
* <span data-ttu-id="2be7e-170">Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="2be7e-170">Click **Add Open Scenes** to add the scene.</span></span>
* <span data-ttu-id="2be7e-171">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-171">Click **Build**.</span></span>
* <span data-ttu-id="2be7e-172">Dans la fenêtre de l’Explorateur de fichiers qui s’affiche, créez un **nouveau dossier** nommé « App ».</span><span class="sxs-lookup"><span data-stu-id="2be7e-172">In the file explorer window that appears, create a **New Folder** named "App".</span></span>
* <span data-ttu-id="2be7e-173">Cliquez sur le **dossier**de l’application.</span><span class="sxs-lookup"><span data-stu-id="2be7e-173">Single click the **App Folder**.</span></span>
* <span data-ttu-id="2be7e-174">Appuyez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-174">Press **Select Folder**.</span></span>
* <span data-ttu-id="2be7e-175">Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2be7e-175">When Unity is done, a File Explorer window will appear.</span></span>
* <span data-ttu-id="2be7e-176">Ouvrez le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="2be7e-176">Open the **App** folder.</span></span>
* <span data-ttu-id="2be7e-177">Ouvrez (double-clic) **origami. sln**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-177">Open (double click) **Origami.sln**.</span></span>
* <span data-ttu-id="2be7e-178">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-178">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **X86**.</span></span>
* <span data-ttu-id="2be7e-179">Cliquez sur la flèche en regard du bouton périphérique, puis sélectionnez **machine distante** à déployer sur Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="2be7e-179">Click on the arrow next to the Device button, and select **Remote Machine** to deploy over Wi-Fi.</span></span>
  * <span data-ttu-id="2be7e-180">Définissez l' **adresse** sur le nom ou l’adresse IP de votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="2be7e-180">Set the **Address** to the name or IP address of your HoloLens.</span></span> <span data-ttu-id="2be7e-181">Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées** ou demandez à Cortana **« Hey Cortana, qu’est-ce que mon adresse IP ? »**</span><span class="sxs-lookup"><span data-stu-id="2be7e-181">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options** or ask Cortana **"Hey Cortana, What's my IP address?"**</span></span>
  * <span data-ttu-id="2be7e-182">Si HoloLens est attaché sur USB, vous pouvez sélectionner l' **appareil** à déployer sur USB.</span><span class="sxs-lookup"><span data-stu-id="2be7e-182">If the HoloLens is attached over USB, you may instead select **Device** to deploy over USB.</span></span>
  * <span data-ttu-id="2be7e-183">Laissez le **mode d’authentification** défini sur **universel**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-183">Leave the **Authentication Mode** set to **Universal**.</span></span>
  * <span data-ttu-id="2be7e-184">Cliquez sur **Sélectionner**</span><span class="sxs-lookup"><span data-stu-id="2be7e-184">Click **Select**</span></span>

* <span data-ttu-id="2be7e-185">Cliquez sur **Déboguer > exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-185">Click **Debug > Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="2be7e-186">S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le [coupler à Visual Studio](using-visual-studio.md#pairing-your-device).</span><span class="sxs-lookup"><span data-stu-id="2be7e-186">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device).</span></span>

* <span data-ttu-id="2be7e-187">Le projet Origami va maintenant générer, déployer sur votre HoloLens, puis exécuter.</span><span class="sxs-lookup"><span data-stu-id="2be7e-187">The Origami project will now build, deploy to your HoloLens, and then run.</span></span>
* <span data-ttu-id="2be7e-188">Placez-vous sur HoloLens et recherchez vos nouveaux hologrammes.</span><span class="sxs-lookup"><span data-stu-id="2be7e-188">Put on your HoloLens and look around to see your new holograms.</span></span>

## <a name="chapter-2---gaze"></a><span data-ttu-id="2be7e-189">Chapitre 2-point de regard</span><span class="sxs-lookup"><span data-stu-id="2be7e-189">Chapter 2 - Gaze</span></span>

>[!VIDEO https://www.youtube.com/embed/MSO2BoFSQbM]

<span data-ttu-id="2be7e-190">Dans ce chapitre, nous allons présenter la première des trois façons d’interagir avec vos hologrammes, en pointant le [regard](gaze-and-commit.md).</span><span class="sxs-lookup"><span data-stu-id="2be7e-190">In this chapter, we are going to introduce the first of three ways of interacting with your holograms -- [gaze](gaze-and-commit.md).</span></span>

### <a name="objectives"></a><span data-ttu-id="2be7e-191">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2be7e-191">Objectives</span></span>

* <span data-ttu-id="2be7e-192">Visualisez votre point de regard à l’aide d’un curseur verrouillé.</span><span class="sxs-lookup"><span data-stu-id="2be7e-192">Visualize your gaze using a world-locked cursor.</span></span>

### <a name="instructions"></a><span data-ttu-id="2be7e-193">Instructions</span><span class="sxs-lookup"><span data-stu-id="2be7e-193">Instructions</span></span>

* <span data-ttu-id="2be7e-194">Revenez à votre projet Unity et fermez la fenêtre Paramètres de build si elle est toujours ouverte.</span><span class="sxs-lookup"><span data-stu-id="2be7e-194">Go back to your Unity project, and close the Build Settings window if it's still open.</span></span>
* <span data-ttu-id="2be7e-195">Sélectionnez le dossier **hologrammes** dans le **panneau Projet**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-195">Select the **Holograms** folder in the **Project panel**.</span></span>
* <span data-ttu-id="2be7e-196">Faites glisser l’objet **curseur** dans le volet de la **hiérarchie** au niveau de la racine.</span><span class="sxs-lookup"><span data-stu-id="2be7e-196">Drag the **Cursor** object into the **Hierarchy panel** at the root level.</span></span>
* <span data-ttu-id="2be7e-197">Double-cliquez sur l’objet **curseur** pour l’examiner en détail.</span><span class="sxs-lookup"><span data-stu-id="2be7e-197">Double-click on the **Cursor** object to take a closer look at it.</span></span>
* <span data-ttu-id="2be7e-198">Cliquez avec le bouton droit sur le dossier **scripts** dans le panneau projet.</span><span class="sxs-lookup"><span data-stu-id="2be7e-198">Right-click on the **Scripts** folder in the Project panel.</span></span>
* <span data-ttu-id="2be7e-199">Cliquez sur le sous-menu **créer** .</span><span class="sxs-lookup"><span data-stu-id="2be7e-199">Click the **Create** sub-menu.</span></span>
* <span data-ttu-id="2be7e-200">Sélectionnez  **C# script**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-200">Select **C# Script**.</span></span>
* <span data-ttu-id="2be7e-201">Nommez le script **WorldCursor**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-201">Name the script **WorldCursor**.</span></span> <span data-ttu-id="2be7e-202">Remarque : le nom respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="2be7e-202">Note: The name is case-sensitive.</span></span> <span data-ttu-id="2be7e-203">Vous n’avez pas besoin d’ajouter l’extension. cs.</span><span class="sxs-lookup"><span data-stu-id="2be7e-203">You do not need to add the .cs extension.</span></span>
* <span data-ttu-id="2be7e-204">Sélectionnez l’objet **curseur** dans le **panneau hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-204">Select the **Cursor** object in the **Hierarchy panel**.</span></span>
* <span data-ttu-id="2be7e-205">Glissez-déplacez le script **WorldCursor** dans le panneau de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-205">Drag and drop the **WorldCursor** script into the **Inspector panel**.</span></span>
* <span data-ttu-id="2be7e-206">Double-cliquez sur le script **WorldCursor** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2be7e-206">Double-click the **WorldCursor** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="2be7e-207">Copiez et collez ce code dans **WorldCursor.cs** et **Enregistrez All**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-207">Copy and paste this code into **WorldCursor.cs** and **Save All**.</span></span>

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

            // Move the cursor to the point where the raycast hit.
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

* <span data-ttu-id="2be7e-208">Régénérez l’application à partir du **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-208">Rebuild the app from **File > Build Settings**.</span></span>
* <span data-ttu-id="2be7e-209">Revenez à la solution Visual Studio utilisée précédemment pour le déploiement dans votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="2be7e-209">Return to the Visual Studio solution previously used to deploy to your HoloLens.</span></span>
* <span data-ttu-id="2be7e-210">Lorsque vous y êtes invité, sélectionnez « recharger tout ».</span><span class="sxs-lookup"><span data-stu-id="2be7e-210">Select 'Reload All' when prompted.</span></span>
* <span data-ttu-id="2be7e-211">Cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-211">Click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
* <span data-ttu-id="2be7e-212">Examinez maintenant la scène et observez comment le curseur interagit avec la forme d’objets.</span><span class="sxs-lookup"><span data-stu-id="2be7e-212">Now look around the scene and notice how the cursor interacts with the shape of objects.</span></span>

## <a name="chapter-3---gestures"></a><span data-ttu-id="2be7e-213">Chapitre 3-mouvements</span><span class="sxs-lookup"><span data-stu-id="2be7e-213">Chapter 3 - Gestures</span></span>

>[!VIDEO https://www.youtube.com/embed/kW3ThJ2MbvQ]

<span data-ttu-id="2be7e-214">Dans ce chapitre, nous allons ajouter la prise en charge des [gestes](gaze-and-commit.md#composite-gestures).</span><span class="sxs-lookup"><span data-stu-id="2be7e-214">In this chapter, we'll add support for [gestures](gaze-and-commit.md#composite-gestures).</span></span> <span data-ttu-id="2be7e-215">Lorsque l’utilisateur sélectionne une sphère papier, nous allons faire tomber la sphère en activant la gravité en utilisant le moteur physique Unity.</span><span class="sxs-lookup"><span data-stu-id="2be7e-215">When the user selects a paper sphere, we'll make the sphere fall by turning on gravity using Unity's physics engine.</span></span>

### <a name="objectives"></a><span data-ttu-id="2be7e-216">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2be7e-216">Objectives</span></span>

* <span data-ttu-id="2be7e-217">Contrôlez vos hologrammes avec le geste Select.</span><span class="sxs-lookup"><span data-stu-id="2be7e-217">Control your holograms with the Select gesture.</span></span>

### <a name="instructions"></a><span data-ttu-id="2be7e-218">Instructions</span><span class="sxs-lookup"><span data-stu-id="2be7e-218">Instructions</span></span>

<span data-ttu-id="2be7e-219">Nous allons commencer par créer un script, puis détecter le mouvement Select.</span><span class="sxs-lookup"><span data-stu-id="2be7e-219">We'll start by creating a script then can detect the Select gesture.</span></span>

* <span data-ttu-id="2be7e-220">Dans le dossier **scripts** , créez un script nommé **GazeGestureManager**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-220">In the **Scripts** folder, create a script named **GazeGestureManager**.</span></span>
* <span data-ttu-id="2be7e-221">Faites glisser le script **GazeGestureManager** sur l’objet **OrigamiCollection** dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="2be7e-221">Drag the **GazeGestureManager** script onto the **OrigamiCollection** object in the Hierarchy.</span></span>
* <span data-ttu-id="2be7e-222">Ouvrez le script **GazeGestureManager** dans Visual Studio et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="2be7e-222">Open the **GazeGestureManager** script in Visual Studio and add the following code:</span></span>

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
    void Awake()
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

* <span data-ttu-id="2be7e-223">Créez un autre script dans le dossier scripts, cette fois nommé **SphereCommands**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-223">Create another script in the Scripts folder, this time named **SphereCommands**.</span></span>
* <span data-ttu-id="2be7e-224">Développez l’objet **OrigamiCollection** dans l’affichage des hiérarchies.</span><span class="sxs-lookup"><span data-stu-id="2be7e-224">Expand the **OrigamiCollection** object in the Hierarchy view.</span></span>
* <span data-ttu-id="2be7e-225">Faites glisser le script **SphereCommands** sur l’objet **Sphere1** dans le panneau hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="2be7e-225">Drag the **SphereCommands** script onto the **Sphere1** object in the Hierarchy panel.</span></span>
* <span data-ttu-id="2be7e-226">Faites glisser le script **SphereCommands** sur l’objet **Sphere2** dans le panneau hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="2be7e-226">Drag the **SphereCommands** script onto the **Sphere2** object in the Hierarchy panel.</span></span>
* <span data-ttu-id="2be7e-227">Ouvrez le script dans Visual Studio pour le modifier, puis remplacez le code par défaut par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="2be7e-227">Open the script in Visual Studio for editing, and replace the default code with this:</span></span>

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

* <span data-ttu-id="2be7e-228">Exportez, générez et déployez l’application dans votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="2be7e-228">Export, build and deploy the app to your HoloLens.</span></span>
* <span data-ttu-id="2be7e-229">Examinez l’une des sphères.</span><span class="sxs-lookup"><span data-stu-id="2be7e-229">Look at one of the spheres.</span></span>
* <span data-ttu-id="2be7e-230">Effectuez le mouvement SELECT et regardez la sphère de la sphère sur l’aire ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2be7e-230">Perform the select gesture and watch the sphere drop onto the surface below.</span></span>

## <a name="chapter-4---voice"></a><span data-ttu-id="2be7e-231">Chapitre 4-voix</span><span class="sxs-lookup"><span data-stu-id="2be7e-231">Chapter 4 - Voice</span></span>

>[!VIDEO https://www.youtube.com/embed/1-Aq0VVtHM8]

<span data-ttu-id="2be7e-232">Dans ce chapitre, nous allons ajouter la prise en charge de deux [commandes vocales](voice-input.md): « réinitialiser le monde » pour ramener les éléments restants à leur emplacement d’origine et « déposer la sphère » pour faire tomber la sphère.</span><span class="sxs-lookup"><span data-stu-id="2be7e-232">In this chapter, we'll add support for two [voice commands](voice-input.md): "Reset world" to return the dropped spheres to their original location, and "Drop sphere" to make the sphere fall.</span></span>

### <a name="objectives"></a><span data-ttu-id="2be7e-233">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2be7e-233">Objectives</span></span>

* <span data-ttu-id="2be7e-234">Ajoutez des commandes vocales qui écoutent toujours en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="2be7e-234">Add voice commands that always listen in the background.</span></span>
* <span data-ttu-id="2be7e-235">Créez un hologramme qui réagit à une commande vocale.</span><span class="sxs-lookup"><span data-stu-id="2be7e-235">Create a hologram that reacts to a voice command.</span></span>

### <a name="instructions"></a><span data-ttu-id="2be7e-236">Instructions</span><span class="sxs-lookup"><span data-stu-id="2be7e-236">Instructions</span></span>

* <span data-ttu-id="2be7e-237">Dans le dossier **scripts** , créez un script nommé **SpeechManager**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-237">In the **Scripts** folder, create a script named **SpeechManager**.</span></span>
* <span data-ttu-id="2be7e-238">Faites glisser le script **SpeechManager** sur l’objet **OrigamiCollection** dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="2be7e-238">Drag the **SpeechManager** script onto the **OrigamiCollection** object in the Hierarchy</span></span>
* <span data-ttu-id="2be7e-239">Ouvrez le script **SpeechManager** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2be7e-239">Open the **SpeechManager** script in Visual Studio.</span></span>
* <span data-ttu-id="2be7e-240">Copiez et collez ce code dans **SpeechManager.cs** et **Enregistrez All**:</span><span class="sxs-lookup"><span data-stu-id="2be7e-240">Copy and paste this code into **SpeechManager.cs** and **Save All**:</span></span>

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

* <span data-ttu-id="2be7e-241">Ouvrez le script **SphereCommands** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2be7e-241">Open the **SphereCommands** script in Visual Studio.</span></span>
* <span data-ttu-id="2be7e-242">Mettez à jour le script pour le lire comme suit :</span><span class="sxs-lookup"><span data-stu-id="2be7e-242">Update the script to read as follows:</span></span>

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

* <span data-ttu-id="2be7e-243">Exportez, générez et déployez l’application dans votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="2be7e-243">Export, build and deploy the app to your HoloLens.</span></span>
* <span data-ttu-id="2be7e-244">Examinez l’une des sphères et dites «**Drop Sphere**».</span><span class="sxs-lookup"><span data-stu-id="2be7e-244">Look at one of the spheres, and say "**Drop Sphere**".</span></span>
* <span data-ttu-id="2be7e-245">Dites «**Réinitialiser le monde**» pour ramener les positions initiales.</span><span class="sxs-lookup"><span data-stu-id="2be7e-245">Say "**Reset World**" to bring them back to their initial positions.</span></span>

## <a name="chapter-5---spatial-sound"></a><span data-ttu-id="2be7e-246">Chapitre 5-sons spatiaux</span><span class="sxs-lookup"><span data-stu-id="2be7e-246">Chapter 5 - Spatial sound</span></span>

>[!VIDEO https://www.youtube.com/embed/Aj4de5Ncbfo]

<span data-ttu-id="2be7e-247">Dans ce chapitre, nous allons ajouter de la musique à l’application, puis déclencher des effets sonores sur certaines actions.</span><span class="sxs-lookup"><span data-stu-id="2be7e-247">In this chapter, we'll add music to the app, and then trigger sound effects on certain actions.</span></span> <span data-ttu-id="2be7e-248">Nous utiliserons le [son spatial](spatial-sound.md) pour fournir des sons à un emplacement spécifique dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="2be7e-248">We'll be using [spatial sound](spatial-sound.md) to give sounds a specific location in 3D space.</span></span>

### <a name="objectives"></a><span data-ttu-id="2be7e-249">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2be7e-249">Objectives</span></span>

* <span data-ttu-id="2be7e-250">Écoutez des hologrammes dans votre monde.</span><span class="sxs-lookup"><span data-stu-id="2be7e-250">Hear holograms in your world.</span></span>

### <a name="instructions"></a><span data-ttu-id="2be7e-251">Instructions</span><span class="sxs-lookup"><span data-stu-id="2be7e-251">Instructions</span></span>

* <span data-ttu-id="2be7e-252">Dans Unity, sélectionnez dans le menu supérieur **modifier > paramètres du projet > audio**</span><span class="sxs-lookup"><span data-stu-id="2be7e-252">In Unity select from the top menu **Edit > Project Settings > Audio**</span></span>
* <span data-ttu-id="2be7e-253">Dans le volet de l’inspecteur situé sur le côté droit, recherchez le paramètre de **plug-in Spatializer** , puis sélectionnez **MS HRTF Spatializer**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-253">In the Inspector Panel on the right side, find the **Spatializer Plugin** setting and select **MS HRTF Spatializer**.</span></span>
* <span data-ttu-id="2be7e-254">À partir du dossier **hologrammes** du panneau projet, faites glisser l’objet **ambiance** sur l’objet **OrigamiCollection** dans le panneau hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="2be7e-254">From the **Holograms** folder in the Project panel, drag the **Ambience** object onto the **OrigamiCollection** object in the Hierarchy Panel.</span></span>
* <span data-ttu-id="2be7e-255">Sélectionnez **OrigamiCollection** et recherchez le composant **audio source** dans le panneau Inspecteur.</span><span class="sxs-lookup"><span data-stu-id="2be7e-255">Select **OrigamiCollection** and find the **Audio Source** component in the Inspector panel.</span></span> <span data-ttu-id="2be7e-256">Modifiez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="2be7e-256">Change these properties:</span></span>
  * <span data-ttu-id="2be7e-257">Vérifiez la propriété **spatial** .</span><span class="sxs-lookup"><span data-stu-id="2be7e-257">Check the **Spatialize** property.</span></span>
  * <span data-ttu-id="2be7e-258">Vérifiez la **lecture sur éveillé**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-258">Check the **Play On Awake**.</span></span>
  * <span data-ttu-id="2be7e-259">Remplacez **spatial Blend** par **3D** en faisant glisser le curseur vers la droite.</span><span class="sxs-lookup"><span data-stu-id="2be7e-259">Change **Spatial Blend** to **3D** by dragging the slider all the way to the right.</span></span> <span data-ttu-id="2be7e-260">La valeur doit passer de 0 à 1 lorsque vous déplacez le curseur.</span><span class="sxs-lookup"><span data-stu-id="2be7e-260">The value should change from 0 to 1 when you move the slider.</span></span>
  * <span data-ttu-id="2be7e-261">Vérifiez la propriété **Loop** .</span><span class="sxs-lookup"><span data-stu-id="2be7e-261">Check the **Loop** property.</span></span>
  * <span data-ttu-id="2be7e-262">Développez **paramètres audio 3D**, puis entrez **0,1** pour le **niveau Doppler**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-262">Expand **3D Sound Settings**, and enter **0.1** for **Doppler Level**.</span></span>
  * <span data-ttu-id="2be7e-263">Définissez **volume Rolloff** sur **Rolloff logarithmique**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-263">Set **Volume Rolloff** to **Logarithmic Rolloff**.</span></span>
  * <span data-ttu-id="2be7e-264">Définissez **distance maximale** sur **20**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-264">Set **Max Distance** to **20**.</span></span>
* <span data-ttu-id="2be7e-265">Dans le dossier **scripts** , créez un script nommé **SphereSounds**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-265">In the **Scripts** folder, create a script named **SphereSounds**.</span></span>
* <span data-ttu-id="2be7e-266">Glissez-déplacez **SphereSounds** vers les objets **Sphere1** et **Sphere2** dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="2be7e-266">Drag and drop **SphereSounds** to the **Sphere1** and **Sphere2** objects in the Hierarchy.</span></span>
* <span data-ttu-id="2be7e-267">Ouvrez **SphereSounds** dans Visual Studio, mettez à jour le code suivant et **Enregistrez All**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-267">Open **SphereSounds** in Visual Studio, update the following code and **Save All**.</span></span>

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

* <span data-ttu-id="2be7e-268">Enregistrez le script et revenez à Unity.</span><span class="sxs-lookup"><span data-stu-id="2be7e-268">Save the script, and return to Unity.</span></span>
* <span data-ttu-id="2be7e-269">Exportez, générez et déployez l’application dans votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="2be7e-269">Export, build and deploy the app to your HoloLens.</span></span>
* <span data-ttu-id="2be7e-270">Rapprochez-vous de l’étape et transformez-la en côte à côte pour entendre la modification des sons.</span><span class="sxs-lookup"><span data-stu-id="2be7e-270">Move closer and further from the Stage and turn side-to-side to hear the sounds change.</span></span>

## <a name="chapter-6---spatial-mapping"></a><span data-ttu-id="2be7e-271">Chapitre 6-mappage spatial</span><span class="sxs-lookup"><span data-stu-id="2be7e-271">Chapter 6 - Spatial mapping</span></span>

>[!VIDEO https://www.youtube.com/embed/Pkt1_wNLLXY]

<span data-ttu-id="2be7e-272">Nous allons maintenant utiliser le [mappage spatial](spatial-mapping.md) pour placer la grille de jeux sur un objet réel dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="2be7e-272">Now we are going to use [spatial mapping](spatial-mapping.md) to place the game board on a real object in the real world.</span></span>

### <a name="objectives"></a><span data-ttu-id="2be7e-273">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2be7e-273">Objectives</span></span>

* <span data-ttu-id="2be7e-274">Intégrez votre monde réel dans le monde virtuel.</span><span class="sxs-lookup"><span data-stu-id="2be7e-274">Bring your real world into the virtual world.</span></span>
* <span data-ttu-id="2be7e-275">Placez vos hologrammes là où ils vous intéressent le plus.</span><span class="sxs-lookup"><span data-stu-id="2be7e-275">Place your holograms where they matter most to you.</span></span>

### <a name="instructions"></a><span data-ttu-id="2be7e-276">Instructions</span><span class="sxs-lookup"><span data-stu-id="2be7e-276">Instructions</span></span>

* <span data-ttu-id="2be7e-277">Dans Unity, cliquez sur le dossier **hologrammes** dans le panneau projet.</span><span class="sxs-lookup"><span data-stu-id="2be7e-277">In Unity, click on the **Holograms** folder in the Project panel.</span></span>
* <span data-ttu-id="2be7e-278">Faites glisser la ressource de **mappage spatial** à la racine de la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-278">Drag the **Spatial Mapping** asset into the root of the **Hierarchy**.</span></span>
* <span data-ttu-id="2be7e-279">Cliquez sur l’objet **mappage spatial** dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="2be7e-279">Click on the **Spatial Mapping** object in the Hierarchy.</span></span>
* <span data-ttu-id="2be7e-280">Dans le **panneau Inspecteur**, modifiez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="2be7e-280">In the **Inspector panel**, change the following properties:</span></span>
  * <span data-ttu-id="2be7e-281">Cochez la case **dessiner des panneaux visuels** .</span><span class="sxs-lookup"><span data-stu-id="2be7e-281">Check the **Draw Visual Meshes** box.</span></span>
  * <span data-ttu-id="2be7e-282">Recherchez **matériel de dessin** , puis cliquez sur le cercle à droite.</span><span class="sxs-lookup"><span data-stu-id="2be7e-282">Locate **Draw Material** and click the circle on the right.</span></span> <span data-ttu-id="2be7e-283">Tapez «**Wireframe**» dans le champ de recherche en haut.</span><span class="sxs-lookup"><span data-stu-id="2be7e-283">Type "**wireframe**" into the search field at the top.</span></span> <span data-ttu-id="2be7e-284">Cliquez sur le résultat, puis fermez la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="2be7e-284">Click on the result and then close the window.</span></span> <span data-ttu-id="2be7e-285">Lorsque vous effectuez cette opération, la valeur de Draw Material doit être définie sur Wireframe.</span><span class="sxs-lookup"><span data-stu-id="2be7e-285">When you do this, the value for Draw Material should get set to Wireframe.</span></span>
* <span data-ttu-id="2be7e-286">Exportez, générez et déployez l’application dans votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="2be7e-286">Export, build and deploy the app to your HoloLens.</span></span>
* <span data-ttu-id="2be7e-287">Lorsque l’application s’exécute, un maillage filaire se superpose à votre monde réel.</span><span class="sxs-lookup"><span data-stu-id="2be7e-287">When the app runs, a wireframe mesh will overlay your real world.</span></span>
* <span data-ttu-id="2be7e-288">Regardez comment une sphère enchaînée va tomber à l’étage, et à l’étage !</span><span class="sxs-lookup"><span data-stu-id="2be7e-288">Watch how a rolling sphere will fall off the stage, and onto the floor!</span></span>

<span data-ttu-id="2be7e-289">Nous allons maintenant vous montrer comment déplacer le OrigamiCollection vers un nouvel emplacement :</span><span class="sxs-lookup"><span data-stu-id="2be7e-289">Now we'll show you how to move the OrigamiCollection to a new location:</span></span>

* <span data-ttu-id="2be7e-290">Dans le dossier **scripts** , créez un script nommé **TapToPlaceParent**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-290">In the **Scripts** folder, create a script named **TapToPlaceParent**.</span></span>
* <span data-ttu-id="2be7e-291">Dans la **hiérarchie**, développez le **OrigamiCollection** et sélectionnez l’objet **stage** .</span><span class="sxs-lookup"><span data-stu-id="2be7e-291">In the **Hierarchy**, expand the **OrigamiCollection** and select the **Stage** object.</span></span>
* <span data-ttu-id="2be7e-292">Faites glisser le script **TapToPlaceParent** sur l’objet stage.</span><span class="sxs-lookup"><span data-stu-id="2be7e-292">Drag the **TapToPlaceParent** script onto the Stage object.</span></span>
* <span data-ttu-id="2be7e-293">Ouvrez le script **TapToPlaceParent** dans Visual Studio et mettez-le à jour comme suit :</span><span class="sxs-lookup"><span data-stu-id="2be7e-293">Open the **TapToPlaceParent** script in Visual Studio, and update it to be the following:</span></span>

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

* <span data-ttu-id="2be7e-294">Exporter, générer et déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="2be7e-294">Export, build and deploy the app.</span></span>
* <span data-ttu-id="2be7e-295">Vous devez maintenant être en mesure de placer le jeu à un emplacement spécifique par gazing, à l’aide du geste Select, puis en le déplaçant vers un nouvel emplacement et en réutilisant le geste Select.</span><span class="sxs-lookup"><span data-stu-id="2be7e-295">Now you should now be able to place the game in a specific location by gazing at it, using the Select gesture and then moving to a new location, and using the Select gesture again.</span></span>

## <a name="chapter-7---holographic-fun"></a><span data-ttu-id="2be7e-296">Chapitre 7-divertissement holographique</span><span class="sxs-lookup"><span data-stu-id="2be7e-296">Chapter 7 - Holographic fun</span></span>

### <a name="objectives"></a><span data-ttu-id="2be7e-297">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2be7e-297">Objectives</span></span>

* <span data-ttu-id="2be7e-298">Révélez l’entrée à un sous-monde holographique.</span><span class="sxs-lookup"><span data-stu-id="2be7e-298">Reveal the entrance to a holographic underworld.</span></span>

### <a name="instructions"></a><span data-ttu-id="2be7e-299">Instructions</span><span class="sxs-lookup"><span data-stu-id="2be7e-299">Instructions</span></span>

<span data-ttu-id="2be7e-300">Nous allons maintenant vous montrer comment dévoiler le sous-monde holographique :</span><span class="sxs-lookup"><span data-stu-id="2be7e-300">Now we'll show you how to uncover the holographic underworld:</span></span>

* <span data-ttu-id="2be7e-301">Dans le dossier **hologrammes** du panneau projet :</span><span class="sxs-lookup"><span data-stu-id="2be7e-301">From the **Holograms** folder in the Project Panel:</span></span>
  * <span data-ttu-id="2be7e-302">Faites glisser le sous- **monde** dans la hiérarchie pour être un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-302">Drag **Underworld** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
* <span data-ttu-id="2be7e-303">Dans le dossier **scripts** , créez un script nommé **HitTarget**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-303">In the **Scripts** folder, create a script named **HitTarget**.</span></span>
* <span data-ttu-id="2be7e-304">Dans la **hiérarchie**, développez **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="2be7e-304">In the **Hierarchy**, expand the **OrigamiCollection**.</span></span>
* <span data-ttu-id="2be7e-305">Développez l’objet **stage** et sélectionnez l’objet **cible** (ventilateur bleu).</span><span class="sxs-lookup"><span data-stu-id="2be7e-305">Expand the **Stage** object and select the **Target** object (blue fan).</span></span>
* <span data-ttu-id="2be7e-306">Faites glisser le script **HitTarget** sur l’objet **cible** .</span><span class="sxs-lookup"><span data-stu-id="2be7e-306">Drag the **HitTarget** script onto the **Target** object.</span></span>
* <span data-ttu-id="2be7e-307">Ouvrez le script **HitTarget** dans Visual Studio et mettez-le à jour comme suit :</span><span class="sxs-lookup"><span data-stu-id="2be7e-307">Open the **HitTarget** script in Visual Studio, and update it to be the following:</span></span>

```cs
using UnityEngine;

public class HitTarget : MonoBehaviour
{
    // These public fields become settable properties in the Unity editor.
    public GameObject underworld;
    public GameObject objectToHide;

    // Occurs when this object starts colliding with another object
    void OnCollisionEnter(Collision collision)
    {
        // Hide the stage and show the underworld.
        objectToHide.SetActive(false);
        underworld.SetActive(true);

        // Disable Spatial Mapping to let the spheres enter the underworld.
        SpatialMapping.Instance.MappingEnabled = false;
    }
}
```

* <span data-ttu-id="2be7e-308">Dans Unity, sélectionnez l’objet **cible** .</span><span class="sxs-lookup"><span data-stu-id="2be7e-308">In Unity, select the **Target** object.</span></span>
* <span data-ttu-id="2be7e-309">Deux propriétés publiques sont désormais visibles sur le composant **cible d’accès** et doivent référencer des objets dans notre scène :</span><span class="sxs-lookup"><span data-stu-id="2be7e-309">Two public properties are now visible on the **Hit Target** component and need to reference objects in our scene:</span></span>
  * <span data-ttu-id="2be7e-310">Faites glisser le sous- **monde** du volet de la **hiérarchie** vers **la propriété sous le composant** cible d' **accès** .</span><span class="sxs-lookup"><span data-stu-id="2be7e-310">Drag **Underworld** from the **Hierarchy** panel to the **Underworld** property on the **Hit Target** component.</span></span>
  * <span data-ttu-id="2be7e-311">Faites glisser **étape** du volet **hiérarchie** vers l' **objet pour masquer** la propriété sur le composant cible d' **accès** .</span><span class="sxs-lookup"><span data-stu-id="2be7e-311">Drag **Stage** from the **Hierarchy** panel to the **Object to Hide** property on the **Hit Target** component.</span></span>
* <span data-ttu-id="2be7e-312">Exporter, générer et déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="2be7e-312">Export, build and deploy the app.</span></span>
* <span data-ttu-id="2be7e-313">Placez la collection d’origamis à l’étage, puis utilisez le mouvement SELECT pour faire glisser une sphère.</span><span class="sxs-lookup"><span data-stu-id="2be7e-313">Place the Origami Collection on the floor, and then use the Select gesture to make a sphere drop.</span></span>
* <span data-ttu-id="2be7e-314">Lorsque la sphère atteint la cible (ventilateur bleu), une explosion se produit.</span><span class="sxs-lookup"><span data-stu-id="2be7e-314">When the sphere hits the target (blue fan), an explosion will occur.</span></span> <span data-ttu-id="2be7e-315">Le regroupement sera masqué et un trou au sous-monde s’affichera.</span><span class="sxs-lookup"><span data-stu-id="2be7e-315">The collection will be hidden and a hole to the underworld will appear.</span></span>

## <a name="the-end"></a><span data-ttu-id="2be7e-316">La fin</span><span class="sxs-lookup"><span data-stu-id="2be7e-316">The end</span></span>

<span data-ttu-id="2be7e-317">Et c’est la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2be7e-317">And that's the end of this tutorial!</span></span>

<span data-ttu-id="2be7e-318">Vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="2be7e-318">You learned:</span></span>

* <span data-ttu-id="2be7e-319">Comment créer une application holographique dans Unity.</span><span class="sxs-lookup"><span data-stu-id="2be7e-319">How to create a holographic app in Unity.</span></span>
* <span data-ttu-id="2be7e-320">Comment utiliser le point de vue du regard, du geste, de la voix, du son et du mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="2be7e-320">How to make use of gaze, gesture, voice, sound, and spatial mapping.</span></span>
* <span data-ttu-id="2be7e-321">Comment générer et déployer une application à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2be7e-321">How to build and deploy an app using Visual Studio.</span></span>

<span data-ttu-id="2be7e-322">Vous êtes maintenant prêt à commencer à créer votre propre expérience holographique !</span><span class="sxs-lookup"><span data-stu-id="2be7e-322">You are now ready to start creating your own holographic experience!</span></span>

## <a name="see-also"></a><span data-ttu-id="2be7e-323">Articles associés</span><span class="sxs-lookup"><span data-stu-id="2be7e-323">See also</span></span>

* [<span data-ttu-id="2be7e-324">Notions de base de 101E : projet complet avec l’émulateur</span><span class="sxs-lookup"><span data-stu-id="2be7e-324">MR Basics 101E: Complete project with emulator</span></span>](holograms-101e.md)
* [<span data-ttu-id="2be7e-325">Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="2be7e-325">Gaze</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="2be7e-326">Pointer du regard vers l’avant et valider</span><span class="sxs-lookup"><span data-stu-id="2be7e-326">Head-gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="2be7e-327">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="2be7e-327">Voice input</span></span>](voice-input.md)
* [<span data-ttu-id="2be7e-328">Son spatial</span><span class="sxs-lookup"><span data-stu-id="2be7e-328">Spatial sound</span></span>](spatial-sound.md)
* [<span data-ttu-id="2be7e-329">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="2be7e-329">Spatial mapping</span></span>](spatial-mapping.md)
