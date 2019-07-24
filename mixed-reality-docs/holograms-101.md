---
title: Notions de base de m. 101-finaliser le projet avec l’appareil
description: Suivez cette procédure pas à pas de codage à l’aide d’Unity, Visual Studio et HoloLens pour apprendre les principes fondamentaux de Windows Mixed Reality.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: réalité mixte, Windows Mixed Reality, HoloLens, hologramme, Academy, didacticiel
ms.openlocfilehash: 043ffac8f30a4e29586478b5dca6ecccc2b5afd3
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63524030"
---
>[!NOTE]
><span data-ttu-id="3be12-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="3be12-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="3be12-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="3be12-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="3be12-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="3be12-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="3be12-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3be12-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="3be12-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="3be12-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="3be12-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="3be12-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-basics-101-complete-project-with-device"></a><span data-ttu-id="3be12-110">Notions de base de m. 101: Terminer le projet avec l’appareil</span><span class="sxs-lookup"><span data-stu-id="3be12-110">MR Basics 101: Complete project with device</span></span>

<br>

>[!VIDEO https://www.youtube.com/embed/XKIIEC5BMWg]

<span data-ttu-id="3be12-111">Ce didacticiel vous guide tout au long d’un projet complet, Unity, qui illustre les fonctionnalités de base de la réalité mixte Windows sur HoloLens [, y compris](gaze.md)le point de présence, les [gestes](gestures.md), l' [entrée vocale](voice-input.md), le [son spatial](spatial-sound.md) et le [mappage spatial](spatial-mapping.md) .</span><span class="sxs-lookup"><span data-stu-id="3be12-111">This tutorial will walk you through a complete project, built in Unity, that demonstrates core Windows Mixed Reality features on HoloLens including [gaze](gaze.md), [gestures](gestures.md), [voice input](voice-input.md), [spatial sound](spatial-sound.md) and [spatial mapping](spatial-mapping.md).</span></span>

<span data-ttu-id="3be12-112">Le didacticiel prendra environ 1 heure.</span><span class="sxs-lookup"><span data-stu-id="3be12-112">The tutorial will take approximately 1 hour to complete.</span></span>

## <a name="device-support"></a><span data-ttu-id="3be12-113">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="3be12-113">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="3be12-114">Course</span><span class="sxs-lookup"><span data-stu-id="3be12-114">Course</span></span></th><th style="width:150px"> <span data-ttu-id="3be12-115"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="3be12-115"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="3be12-116"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="3be12-116"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="3be12-117">Notions de base de m. 101: Terminer le projet avec l’appareil</span><span class="sxs-lookup"><span data-stu-id="3be12-117">MR Basics 101: Complete project with device</span></span></td><td style="text-align: center;"> <span data-ttu-id="3be12-118">✔️</span><span class="sxs-lookup"><span data-stu-id="3be12-118">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="3be12-119">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="3be12-119">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3be12-120">Prérequis</span><span class="sxs-lookup"><span data-stu-id="3be12-120">Prerequisites</span></span>

* <span data-ttu-id="3be12-121">Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="3be12-121">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="3be12-122">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="3be12-122">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="3be12-123">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="3be12-123">Project files</span></span>

* <span data-ttu-id="3be12-124">Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) requis par le projet.</span><span class="sxs-lookup"><span data-stu-id="3be12-124">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) required by the project.</span></span><span data-ttu-id="3be12-125"> Requiert Unity 2017,2 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3be12-125"> Requires Unity 2017.2 or later.</span></span>
  * <span data-ttu-id="3be12-126">Si vous avez encore besoin de la prise en charge d’Unity 5,6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).</span><span class="sxs-lookup"><span data-stu-id="3be12-126">If you still need Unity 5.6 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).</span></span>
  * <span data-ttu-id="3be12-127">Si vous avez encore besoin de la prise en charge d’Unity 5,5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).</span><span class="sxs-lookup"><span data-stu-id="3be12-127">If you still need Unity 5.5 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).</span></span>
  * <span data-ttu-id="3be12-128">Si vous avez encore besoin de la prise en charge d’Unity 5,4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).</span><span class="sxs-lookup"><span data-stu-id="3be12-128">If you still need Unity 5.4 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).</span></span>
* <span data-ttu-id="3be12-129">Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.</span><span class="sxs-lookup"><span data-stu-id="3be12-129">Un-archive the files to your desktop or other easy to reach location.</span></span> <span data-ttu-id="3be12-130">Conservez le nom du dossier **origami**.</span><span class="sxs-lookup"><span data-stu-id="3be12-130">Keep the folder name as **Origami**.</span></span>

>[!NOTE]
><span data-ttu-id="3be12-131">Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).</span><span class="sxs-lookup"><span data-stu-id="3be12-131">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).</span></span>

## <a name="chapter-1---holo-world"></a><span data-ttu-id="3be12-132">Chapitre 1-monde «Holo»</span><span class="sxs-lookup"><span data-stu-id="3be12-132">Chapter 1 - "Holo" world</span></span>

>[!VIDEO https://www.youtube.com/embed/PmtZGjYFroY]

<span data-ttu-id="3be12-133">Dans ce chapitre, nous allons configurer notre premier projet Unity et effectuer un pas à pas détaillé dans le processus de création et de déploiement.</span><span class="sxs-lookup"><span data-stu-id="3be12-133">In this chapter, we'll setup our first Unity project and step through the build and deploy process.</span></span>

### <a name="objectives"></a><span data-ttu-id="3be12-134">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3be12-134">Objectives</span></span>

* <span data-ttu-id="3be12-135">Configurez Unity pour le développement holographique.</span><span class="sxs-lookup"><span data-stu-id="3be12-135">Set up Unity for holographic development.</span></span>
* <span data-ttu-id="3be12-136">Créez un hologramme.</span><span class="sxs-lookup"><span data-stu-id="3be12-136">Make a hologram.</span></span>
* <span data-ttu-id="3be12-137">Consultez un hologramme que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="3be12-137">See a hologram that you made.</span></span>

### <a name="instructions"></a><span data-ttu-id="3be12-138">Instructions</span><span class="sxs-lookup"><span data-stu-id="3be12-138">Instructions</span></span>

* <span data-ttu-id="3be12-139">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="3be12-139">Start Unity.</span></span>
* <span data-ttu-id="3be12-140">Sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="3be12-140">Select **Open**.</span></span>
* <span data-ttu-id="3be12-141">Entrez l’emplacement du dossier **origami** que vous avez précédemment désinstallé.</span><span class="sxs-lookup"><span data-stu-id="3be12-141">Enter location as the **Origami** folder you previously un-archived.</span></span>
* <span data-ttu-id="3be12-142">Sélectionnez **origami** , puis cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="3be12-142">Select **Origami** and click **Select Folder**.</span></span>
* <span data-ttu-id="3be12-143">Étant donné que le projet **origami** ne contient pas de scène, enregistrez la scène vide par défaut dans un nouveau fichier à l’aide de: Fichier / **enregistrer la scène sous**.</span><span class="sxs-lookup"><span data-stu-id="3be12-143">Since the **Origami** project does not contain a scene, save the empty default scene to a new file using: **File** / **Save Scene As**.</span></span>
* <span data-ttu-id="3be12-144">Nommez le nouvel **origami** de scène et appuyez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="3be12-144">Name the new scene **Origami** and press the **Save** button.</span></span>

#### <a name="setup-the-main-virtual-camera"></a><span data-ttu-id="3be12-145">Configurer la caméra virtuelle principale</span><span class="sxs-lookup"><span data-stu-id="3be12-145">Setup the main virtual camera</span></span>

* <span data-ttu-id="3be12-146">Dans le **panneau hiérarchie**, sélectionnez **caméra principale**.</span><span class="sxs-lookup"><span data-stu-id="3be12-146">In the **Hierarchy Panel**, select **Main Camera**.</span></span>
* <span data-ttu-id="3be12-147">Dans l' **inspecteur** , définissez sa position de transformation sur **0, 0,** 0.</span><span class="sxs-lookup"><span data-stu-id="3be12-147">In the **Inspector** set its transform position to **0,0,0**.</span></span>
* <span data-ttu-id="3be12-148">Recherchez la propriété **effacer les indicateurs** et remplacez la liste déroulante **skybox** par **couleur unie**.</span><span class="sxs-lookup"><span data-stu-id="3be12-148">Find the **Clear Flags** property, and change the dropdown from **Skybox** to **Solid color**.</span></span>
* <span data-ttu-id="3be12-149">Cliquez sur le champ **arrière-plan** pour ouvrir un sélecteur de couleurs.</span><span class="sxs-lookup"><span data-stu-id="3be12-149">Click on the **Background** field to open a color picker.</span></span>
* <span data-ttu-id="3be12-150">Affectez **R, G, B et A** à **0**.</span><span class="sxs-lookup"><span data-stu-id="3be12-150">Set **R, G, B, and A** to **0**.</span></span>

#### <a name="setup-the-scene"></a><span data-ttu-id="3be12-151">Configurer la scène</span><span class="sxs-lookup"><span data-stu-id="3be12-151">Setup the scene</span></span>

* <span data-ttu-id="3be12-152">Dans le **volet hiérarchie**, cliquez sur **créer** et **créez un vide**.</span><span class="sxs-lookup"><span data-stu-id="3be12-152">In the **Hierarchy Panel**, click on **Create** and **Create Empty**.</span></span>
* <span data-ttu-id="3be12-153">Cliquez avec le bouton droit sur le nouveau **gameobject** , puis sélectionnez Renommer.</span><span class="sxs-lookup"><span data-stu-id="3be12-153">Right-click the new **GameObject** and select Rename.</span></span> <span data-ttu-id="3be12-154">Renommez GameObject en **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="3be12-154">Rename the GameObject to **OrigamiCollection**.</span></span>
* <span data-ttu-id="3be12-155">Dans le  dossier hologrammes du panneau projet (développez actifs et sélectionnez hologrammes ou double-cliquez sur le dossier hologrammes dans le panneau projet):</span><span class="sxs-lookup"><span data-stu-id="3be12-155">From the **Holograms** folder in the Project Panel (expand Assets and select Holograms or double click the Holograms folder in the Project Panel):</span></span>
  * <span data-ttu-id="3be12-156">Faites glisser **étape** dans la hiérarchie pour être un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="3be12-156">Drag **Stage** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
  * <span data-ttu-id="3be12-157">Faites glisser **Sphere1** dans la hiérarchie pour être un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="3be12-157">Drag **Sphere1** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
  * <span data-ttu-id="3be12-158">Faites glisser **Sphere2** dans la hiérarchie pour être un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="3be12-158">Drag **Sphere2** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
* <span data-ttu-id="3be12-159">Cliquez avec le bouton droit sur l’objet **Light directionnel** dans le **panneau hiérarchie** , puis sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="3be12-159">Right-click the **Directional Light** object in the **Hierarchy Panel** and select **Delete**.</span></span>
* <span data-ttu-id="3be12-160">À partir  du dossier hologrammes, faites glisser Lights à la racine du **panneau de hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="3be12-160">From the **Holograms** folder, drag **Lights** into the root of the **Hierarchy Panel**.</span></span>
* <span data-ttu-id="3be12-161">Dans la **hiérarchie**, sélectionnez **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="3be12-161">In the **Hierarchy**, select the **OrigamiCollection**.</span></span>
* <span data-ttu-id="3be12-162">Dans l' **inspecteur**, définissez la position de la transformation sur **0,-0,5, 2,0**.</span><span class="sxs-lookup"><span data-stu-id="3be12-162">In the **Inspector**, set the transform position to **0, -0.5, 2.0**.</span></span>
* <span data-ttu-id="3be12-163">Appuyez sur le bouton de **lecture** dans Unity pour afficher un aperçu de vos hologrammes.</span><span class="sxs-lookup"><span data-stu-id="3be12-163">Press the **Play** button in Unity to preview your holograms.</span></span>
* <span data-ttu-id="3be12-164">Les objets origami doivent apparaître dans la fenêtre d’aperçu.</span><span class="sxs-lookup"><span data-stu-id="3be12-164">You should see the Origami objects in the preview window.</span></span>
* <span data-ttu-id="3be12-165">Appuyez sur **lecture** une deuxième fois pour arrêter le mode aperçu.</span><span class="sxs-lookup"><span data-stu-id="3be12-165">Press **Play** a second time to stop preview mode.</span></span>

#### <a name="export-the-project-from-unity-to-visual-studio"></a><span data-ttu-id="3be12-166">Exporter le projet d’Unity vers Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3be12-166">Export the project from Unity to Visual Studio</span></span>

* <span data-ttu-id="3be12-167">Dans Unity, sélectionnez **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="3be12-167">In Unity select **File > Build Settings**.</span></span>
* <span data-ttu-id="3be12-168">Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur basculer la **plateforme**.</span><span class="sxs-lookup"><span data-stu-id="3be12-168">Select **Universal Windows Platform** in the **Platform** list and click **Switch Platform**.</span></span>
* <span data-ttu-id="3be12-169">Affectez à **SDK** la valeur **Universal 10** et **type de build** la valeur **D3D**.</span><span class="sxs-lookup"><span data-stu-id="3be12-169">Set **SDK** to **Universal 10** and **Build Type** to **D3D**.</span></span>
* <span data-ttu-id="3be12-170">Vérifiez **les C# projets Unity**.</span><span class="sxs-lookup"><span data-stu-id="3be12-170">Check **Unity C# Projects**.</span></span>
* <span data-ttu-id="3be12-171">Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="3be12-171">Click **Add Open Scenes** to add the scene.</span></span>
* <span data-ttu-id="3be12-172">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="3be12-172">Click **Build**.</span></span>
* <span data-ttu-id="3be12-173">Dans la fenêtre de l’Explorateur de fichiers qui s’affiche, créez un **nouveau dossier** nommé «App».</span><span class="sxs-lookup"><span data-stu-id="3be12-173">In the file explorer window that appears, create a **New Folder** named "App".</span></span>
* <span data-ttu-id="3be12-174">Cliquez sur le **dossier**de l’application.</span><span class="sxs-lookup"><span data-stu-id="3be12-174">Single click the **App Folder**.</span></span>
* <span data-ttu-id="3be12-175">Appuyez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="3be12-175">Press **Select Folder**.</span></span>
* <span data-ttu-id="3be12-176">Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3be12-176">When Unity is done, a File Explorer window will appear.</span></span>
* <span data-ttu-id="3be12-177">Ouvrez le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="3be12-177">Open the **App** folder.</span></span>
* <span data-ttu-id="3be12-178">Ouvrez (double-clic) **origami. sln**.</span><span class="sxs-lookup"><span data-stu-id="3be12-178">Open (double click) **Origami.sln**.</span></span>
* <span data-ttu-id="3be12-179">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.</span><span class="sxs-lookup"><span data-stu-id="3be12-179">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **X86**.</span></span>
* <span data-ttu-id="3be12-180">Cliquez sur la flèche en regard du bouton périphérique, puis sélectionnez **machine** distante à déployer sur Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="3be12-180">Click on the arrow next to the Device button, and select **Remote Machine** to deploy over Wi-Fi.</span></span>
  * <span data-ttu-id="3be12-181">Définissez l' **adresse** sur le nom ou l’adresse IP de votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3be12-181">Set the **Address** to the name or IP address of your HoloLens.</span></span> <span data-ttu-id="3be12-182">Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées** ou demandez à Cortana **«Hey Cortana, qu’est-ce que mon adresse IP?»**</span><span class="sxs-lookup"><span data-stu-id="3be12-182">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options** or ask Cortana **"Hey Cortana, What's my IP address?"**</span></span>
  * <span data-ttu-id="3be12-183">Si HoloLens est attaché sur USB, vous pouvez sélectionner l' **appareil** à déployer sur USB.</span><span class="sxs-lookup"><span data-stu-id="3be12-183">If the HoloLens is attached over USB, you may instead select **Device** to deploy over USB.</span></span>
  * <span data-ttu-id="3be12-184">Laissez le **mode d’authentification** défini sur **universel**.</span><span class="sxs-lookup"><span data-stu-id="3be12-184">Leave the **Authentication Mode** set to **Universal**.</span></span>
  * <span data-ttu-id="3be12-185">Cliquez sur **Sélectionner**</span><span class="sxs-lookup"><span data-stu-id="3be12-185">Click **Select**</span></span>

* <span data-ttu-id="3be12-186">Cliquez sur déboguer **> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="3be12-186">Click **Debug > Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="3be12-187">S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le coupler à [Visual Studio](using-visual-studio.md#pairing-your-device-hololens-(1st-gen)).</span><span class="sxs-lookup"><span data-stu-id="3be12-187">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device-hololens-(1st-gen)).</span></span>

* <span data-ttu-id="3be12-188">Le projet Origami va maintenant générer, déployer sur votre HoloLens, puis exécuter.</span><span class="sxs-lookup"><span data-stu-id="3be12-188">The Origami project will now build, deploy to your HoloLens, and then run.</span></span>
* <span data-ttu-id="3be12-189">Placez-vous sur HoloLens et recherchez vos nouveaux hologrammes.</span><span class="sxs-lookup"><span data-stu-id="3be12-189">Put on your HoloLens and look around to see your new holograms.</span></span>

## <a name="chapter-2---gaze"></a><span data-ttu-id="3be12-190">Chapitre 2-point de regard</span><span class="sxs-lookup"><span data-stu-id="3be12-190">Chapter 2 - Gaze</span></span>

>[!VIDEO https://www.youtube.com/embed/MSO2BoFSQbM]

<span data-ttu-id="3be12-191">Dans ce chapitre, nous allons présenter la première des trois façons d’interagir avec vos hologrammes, en pointant le [regard](gaze.md).</span><span class="sxs-lookup"><span data-stu-id="3be12-191">In this chapter, we are going to introduce the first of three ways of interacting with your holograms -- [gaze](gaze.md).</span></span>

### <a name="objectives"></a><span data-ttu-id="3be12-192">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3be12-192">Objectives</span></span>

* <span data-ttu-id="3be12-193">Visualisez votre point de regard à l’aide d’un curseur verrouillé.</span><span class="sxs-lookup"><span data-stu-id="3be12-193">Visualize your gaze using a world-locked cursor.</span></span>

### <a name="instructions"></a><span data-ttu-id="3be12-194">Instructions</span><span class="sxs-lookup"><span data-stu-id="3be12-194">Instructions</span></span>

* <span data-ttu-id="3be12-195">Revenez à votre projet Unity et fermez la fenêtre Paramètres de build si elle est toujours ouverte.</span><span class="sxs-lookup"><span data-stu-id="3be12-195">Go back to your Unity project, and close the Build Settings window if it's still open.</span></span>
* <span data-ttu-id="3be12-196">Sélectionnez le  dossier hologrammes dans le **panneau Projet**.</span><span class="sxs-lookup"><span data-stu-id="3be12-196">Select the **Holograms** folder in the **Project panel**.</span></span>
* <span data-ttu-id="3be12-197">Faites glisser l’objet **curseur** dans le volet de la **hiérarchie** au niveau de la racine.</span><span class="sxs-lookup"><span data-stu-id="3be12-197">Drag the **Cursor** object into the **Hierarchy panel** at the root level.</span></span>
* <span data-ttu-id="3be12-198">Double-cliquez sur l’objet **curseur** pour l’examiner en détail.</span><span class="sxs-lookup"><span data-stu-id="3be12-198">Double-click on the **Cursor** object to take a closer look at it.</span></span>
* <span data-ttu-id="3be12-199">Cliquez avec le bouton droit sur le dossier **scripts** dans le panneau projet.</span><span class="sxs-lookup"><span data-stu-id="3be12-199">Right-click on the **Scripts** folder in the Project panel.</span></span>
* <span data-ttu-id="3be12-200">Cliquez sur le sous-menu **créer** .</span><span class="sxs-lookup"><span data-stu-id="3be12-200">Click the **Create** sub-menu.</span></span>
* <span data-ttu-id="3be12-201">Sélectionnez  **C# script**.</span><span class="sxs-lookup"><span data-stu-id="3be12-201">Select **C# Script**.</span></span>
* <span data-ttu-id="3be12-202">Nommez le script **WorldCursor**.</span><span class="sxs-lookup"><span data-stu-id="3be12-202">Name the script **WorldCursor**.</span></span> <span data-ttu-id="3be12-203">Remarque : Le nom est sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="3be12-203">Note: The name is case-sensitive.</span></span> <span data-ttu-id="3be12-204">Vous n’avez pas besoin d’ajouter l’extension. cs.</span><span class="sxs-lookup"><span data-stu-id="3be12-204">You do not need to add the .cs extension.</span></span>
* <span data-ttu-id="3be12-205">Sélectionnez l’objet **curseur** dans le **panneau hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="3be12-205">Select the **Cursor** object in the **Hierarchy panel**.</span></span>
* <span data-ttu-id="3be12-206">Glissez-déplacez le script **WorldCursor** dans le panneau de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="3be12-206">Drag and drop the **WorldCursor** script into the **Inspector panel**.</span></span>
* <span data-ttu-id="3be12-207">Double-cliquez sur le script **WorldCursor** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3be12-207">Double-click the **WorldCursor** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="3be12-208">Copiez et collez ce code dans **WorldCursor.cs** et **Enregistrez All**.</span><span class="sxs-lookup"><span data-stu-id="3be12-208">Copy and paste this code into **WorldCursor.cs** and **Save All**.</span></span>

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

* <span data-ttu-id="3be12-209">Régénérez l’application à partir du **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="3be12-209">Rebuild the app from **File > Build Settings**.</span></span>
* <span data-ttu-id="3be12-210">Revenez à la solution Visual Studio utilisée précédemment pour le déploiement dans votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3be12-210">Return to the Visual Studio solution previously used to deploy to your HoloLens.</span></span>
* <span data-ttu-id="3be12-211">Lorsque vous y êtes invité, sélectionnez «recharger tout».</span><span class="sxs-lookup"><span data-stu-id="3be12-211">Select 'Reload All' when prompted.</span></span>
* <span data-ttu-id="3be12-212">Cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="3be12-212">Click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
* <span data-ttu-id="3be12-213">Examinez maintenant la scène et observez comment le curseur interagit avec la forme d’objets.</span><span class="sxs-lookup"><span data-stu-id="3be12-213">Now look around the scene and notice how the cursor interacts with the shape of objects.</span></span>

## <a name="chapter-3---gestures"></a><span data-ttu-id="3be12-214">Chapitre 3-mouvements</span><span class="sxs-lookup"><span data-stu-id="3be12-214">Chapter 3 - Gestures</span></span>

>[!VIDEO https://www.youtube.com/embed/kW3ThJ2MbvQ]

<span data-ttu-id="3be12-215">Dans ce chapitre, nous allons ajouter la prise en charge des [gestes](gestures.md).</span><span class="sxs-lookup"><span data-stu-id="3be12-215">In this chapter, we'll add support for [gestures](gestures.md).</span></span> <span data-ttu-id="3be12-216">Lorsque l’utilisateur sélectionne une sphère papier, nous allons faire tomber la sphère en activant la gravité en utilisant le moteur physique Unity.</span><span class="sxs-lookup"><span data-stu-id="3be12-216">When the user selects a paper sphere, we'll make the sphere fall by turning on gravity using Unity's physics engine.</span></span>

### <a name="objectives"></a><span data-ttu-id="3be12-217">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3be12-217">Objectives</span></span>

* <span data-ttu-id="3be12-218">Contrôlez vos hologrammes avec le geste Select.</span><span class="sxs-lookup"><span data-stu-id="3be12-218">Control your holograms with the Select gesture.</span></span>

### <a name="instructions"></a><span data-ttu-id="3be12-219">Instructions</span><span class="sxs-lookup"><span data-stu-id="3be12-219">Instructions</span></span>

<span data-ttu-id="3be12-220">Nous allons commencer par créer un script, puis détecter le mouvement Select.</span><span class="sxs-lookup"><span data-stu-id="3be12-220">We'll start by creating a script then can detect the Select gesture.</span></span>

* <span data-ttu-id="3be12-221">Dans le dossier **scripts** , créez un script nommé **GazeGestureManager**.</span><span class="sxs-lookup"><span data-stu-id="3be12-221">In the **Scripts** folder, create a script named **GazeGestureManager**.</span></span>
* <span data-ttu-id="3be12-222">Faites glisser le script **GazeGestureManager** sur l’objet **OrigamiCollection** dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3be12-222">Drag the **GazeGestureManager** script onto the **OrigamiCollection** object in the Hierarchy.</span></span>
* <span data-ttu-id="3be12-223">Ouvrez le script **GazeGestureManager** dans Visual Studio et ajoutez le code suivant:</span><span class="sxs-lookup"><span data-stu-id="3be12-223">Open the **GazeGestureManager** script in Visual Studio and add the following code:</span></span>

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

* <span data-ttu-id="3be12-224">Créez un autre script dans le dossier scripts, cette fois nommé **SphereCommands**.</span><span class="sxs-lookup"><span data-stu-id="3be12-224">Create another script in the Scripts folder, this time named **SphereCommands**.</span></span>
* <span data-ttu-id="3be12-225">Développez l’objet **OrigamiCollection** dans l’affichage des hiérarchies.</span><span class="sxs-lookup"><span data-stu-id="3be12-225">Expand the **OrigamiCollection** object in the Hierarchy view.</span></span>
* <span data-ttu-id="3be12-226">Faites glisser le script **SphereCommands** sur l’objet **Sphere1** dans le panneau hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3be12-226">Drag the **SphereCommands** script onto the **Sphere1** object in the Hierarchy panel.</span></span>
* <span data-ttu-id="3be12-227">Faites glisser le script **SphereCommands** sur l’objet **Sphere2** dans le panneau hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3be12-227">Drag the **SphereCommands** script onto the **Sphere2** object in the Hierarchy panel.</span></span>
* <span data-ttu-id="3be12-228">Ouvrez le script dans Visual Studio pour le modifier, puis remplacez le code par défaut par ce qui suit:</span><span class="sxs-lookup"><span data-stu-id="3be12-228">Open the script in Visual Studio for editing, and replace the default code with this:</span></span>

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

* <span data-ttu-id="3be12-229">Exportez, générez et déployez l’application dans votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3be12-229">Export, build and deploy the app to your HoloLens.</span></span>
* <span data-ttu-id="3be12-230">Examinez l’une des sphères.</span><span class="sxs-lookup"><span data-stu-id="3be12-230">Look at one of the spheres.</span></span>
* <span data-ttu-id="3be12-231">Effectuez le mouvement SELECT et regardez la sphère de la sphère sur l’aire ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3be12-231">Perform the select gesture and watch the sphere drop onto the surface below.</span></span>

## <a name="chapter-4---voice"></a><span data-ttu-id="3be12-232">Chapitre 4-voix</span><span class="sxs-lookup"><span data-stu-id="3be12-232">Chapter 4 - Voice</span></span>

>[!VIDEO https://www.youtube.com/embed/1-Aq0VVtHM8]

<span data-ttu-id="3be12-233">Dans ce chapitre, nous allons ajouter la prise en charge de deux [commandes vocales](voice-input.md): «Réinitialiser le monde» pour ramener les sphères déplacées à leur emplacement d’origine et «déposer la sphère» pour faire tomber la sphère.</span><span class="sxs-lookup"><span data-stu-id="3be12-233">In this chapter, we'll add support for two [voice commands](voice-input.md): "Reset world" to return the dropped spheres to their original location, and "Drop sphere" to make the sphere fall.</span></span>

### <a name="objectives"></a><span data-ttu-id="3be12-234">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3be12-234">Objectives</span></span>

* <span data-ttu-id="3be12-235">Ajoutez des commandes vocales qui écoutent toujours en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="3be12-235">Add voice commands that always listen in the background.</span></span>
* <span data-ttu-id="3be12-236">Créez un hologramme qui réagit à une commande vocale.</span><span class="sxs-lookup"><span data-stu-id="3be12-236">Create a hologram that reacts to a voice command.</span></span>

### <a name="instructions"></a><span data-ttu-id="3be12-237">Instructions</span><span class="sxs-lookup"><span data-stu-id="3be12-237">Instructions</span></span>

* <span data-ttu-id="3be12-238">Dans le dossier **scripts** , créez un script nommé **SpeechManager**.</span><span class="sxs-lookup"><span data-stu-id="3be12-238">In the **Scripts** folder, create a script named **SpeechManager**.</span></span>
* <span data-ttu-id="3be12-239">Faites glisser le script **SpeechManager** sur l’objet **OrigamiCollection** dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3be12-239">Drag the **SpeechManager** script onto the **OrigamiCollection** object in the Hierarchy</span></span>
* <span data-ttu-id="3be12-240">Ouvrez le script **SpeechManager** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3be12-240">Open the **SpeechManager** script in Visual Studio.</span></span>
* <span data-ttu-id="3be12-241">Copiez et collez ce code dans **SpeechManager.cs** et **Enregistrez All**:</span><span class="sxs-lookup"><span data-stu-id="3be12-241">Copy and paste this code into **SpeechManager.cs** and **Save All**:</span></span>

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

* <span data-ttu-id="3be12-242">Ouvrez le script **SphereCommands** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3be12-242">Open the **SphereCommands** script in Visual Studio.</span></span>
* <span data-ttu-id="3be12-243">Mettez à jour le script pour le lire comme suit:</span><span class="sxs-lookup"><span data-stu-id="3be12-243">Update the script to read as follows:</span></span>

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

* <span data-ttu-id="3be12-244">Exportez, générez et déployez l’application dans votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3be12-244">Export, build and deploy the app to your HoloLens.</span></span>
* <span data-ttu-id="3be12-245">Examinez l’une des sphères et dites «**Drop Sphere**».</span><span class="sxs-lookup"><span data-stu-id="3be12-245">Look at one of the spheres, and say "**Drop Sphere**".</span></span>
* <span data-ttu-id="3be12-246">Dites «**Réinitialiser le monde**» pour ramener les positions initiales.</span><span class="sxs-lookup"><span data-stu-id="3be12-246">Say "**Reset World**" to bring them back to their initial positions.</span></span>

## <a name="chapter-5---spatial-sound"></a><span data-ttu-id="3be12-247">Chapitre 5-sons spatiaux</span><span class="sxs-lookup"><span data-stu-id="3be12-247">Chapter 5 - Spatial sound</span></span>

>[!VIDEO https://www.youtube.com/embed/Aj4de5Ncbfo]

<span data-ttu-id="3be12-248">Dans ce chapitre, nous allons ajouter de la musique à l’application, puis déclencher des effets sonores sur certaines actions.</span><span class="sxs-lookup"><span data-stu-id="3be12-248">In this chapter, we'll add music to the app, and then trigger sound effects on certain actions.</span></span> <span data-ttu-id="3be12-249">Nous utiliserons le [son spatial](spatial-sound.md) pour fournir des sons à un emplacement spécifique dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="3be12-249">We'll be using [spatial sound](spatial-sound.md) to give sounds a specific location in 3D space.</span></span>

### <a name="objectives"></a><span data-ttu-id="3be12-250">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3be12-250">Objectives</span></span>

* <span data-ttu-id="3be12-251">Écoutez des hologrammes dans votre monde.</span><span class="sxs-lookup"><span data-stu-id="3be12-251">Hear holograms in your world.</span></span>

### <a name="instructions"></a><span data-ttu-id="3be12-252">Instructions</span><span class="sxs-lookup"><span data-stu-id="3be12-252">Instructions</span></span>

* <span data-ttu-id="3be12-253">Dans Unity, sélectionnez dans le menu supérieur **modifier > paramètres du projet > audio**</span><span class="sxs-lookup"><span data-stu-id="3be12-253">In Unity select from the top menu **Edit > Project Settings > Audio**</span></span>
* <span data-ttu-id="3be12-254">Dans le volet de l’inspecteur situé sur le côté droit, recherchez le paramètre de **plug-in Spatializer** , puis sélectionnez **MS HRTF Spatializer**.</span><span class="sxs-lookup"><span data-stu-id="3be12-254">In the Inspector Panel on the right side, find the **Spatializer Plugin** setting and select **MS HRTF Spatializer**.</span></span>
* <span data-ttu-id="3be12-255">À partir  du dossier hologrammes du panneau projet, faites glisser l’objet **ambiance** sur l’objet **OrigamiCollection** dans le panneau hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3be12-255">From the **Holograms** folder in the Project panel, drag the **Ambience** object onto the **OrigamiCollection** object in the Hierarchy Panel.</span></span>
* <span data-ttu-id="3be12-256">Sélectionnez **OrigamiCollection** et recherchez le composant **audio source** dans le panneau Inspecteur.</span><span class="sxs-lookup"><span data-stu-id="3be12-256">Select **OrigamiCollection** and find the **Audio Source** component in the Inspector panel.</span></span> <span data-ttu-id="3be12-257">Modifiez les propriétés suivantes:</span><span class="sxs-lookup"><span data-stu-id="3be12-257">Change these properties:</span></span>
  * <span data-ttu-id="3be12-258">Vérifiez la propriété **spatial** .</span><span class="sxs-lookup"><span data-stu-id="3be12-258">Check the **Spatialize** property.</span></span>
  * <span data-ttu-id="3be12-259">Vérifiez la **lecture sur éveillé**.</span><span class="sxs-lookup"><span data-stu-id="3be12-259">Check the **Play On Awake**.</span></span>
  * <span data-ttu-id="3be12-260">Remplacez **spatial Blend** par **3D** en faisant glisser le curseur vers la droite.</span><span class="sxs-lookup"><span data-stu-id="3be12-260">Change **Spatial Blend** to **3D** by dragging the slider all the way to the right.</span></span> <span data-ttu-id="3be12-261">La valeur doit passer de 0 à 1 lorsque vous déplacez le curseur.</span><span class="sxs-lookup"><span data-stu-id="3be12-261">The value should change from 0 to 1 when you move the slider.</span></span>
  * <span data-ttu-id="3be12-262">Vérifiez la propriété **Loop** .</span><span class="sxs-lookup"><span data-stu-id="3be12-262">Check the **Loop** property.</span></span>
  * <span data-ttu-id="3be12-263">Développez **paramètres audio 3D**, puis entrez **0,1** pour le **niveau Doppler**.</span><span class="sxs-lookup"><span data-stu-id="3be12-263">Expand **3D Sound Settings**, and enter **0.1** for **Doppler Level**.</span></span>
  * <span data-ttu-id="3be12-264">Définissez **volume Rolloff** sur **Rolloff logarithmique**.</span><span class="sxs-lookup"><span data-stu-id="3be12-264">Set **Volume Rolloff** to **Logarithmic Rolloff**.</span></span>
  * <span data-ttu-id="3be12-265">Définissez **distance maximale** sur **20**.</span><span class="sxs-lookup"><span data-stu-id="3be12-265">Set **Max Distance** to **20**.</span></span>
* <span data-ttu-id="3be12-266">Dans le dossier **scripts** , créez un script nommé **SphereSounds**.</span><span class="sxs-lookup"><span data-stu-id="3be12-266">In the **Scripts** folder, create a script named **SphereSounds**.</span></span>
* <span data-ttu-id="3be12-267">Glissez-déplacez **SphereSounds** vers les objets **Sphere1** et **Sphere2** dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3be12-267">Drag and drop **SphereSounds** to the **Sphere1** and **Sphere2** objects in the Hierarchy.</span></span>
* <span data-ttu-id="3be12-268">Ouvrez **SphereSounds** dans Visual Studio, mettez à jour le code suivant et **Enregistrez All**.</span><span class="sxs-lookup"><span data-stu-id="3be12-268">Open **SphereSounds** in Visual Studio, update the following code and **Save All**.</span></span>

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

* <span data-ttu-id="3be12-269">Enregistrez le script et revenez à Unity.</span><span class="sxs-lookup"><span data-stu-id="3be12-269">Save the script, and return to Unity.</span></span>
* <span data-ttu-id="3be12-270">Exportez, générez et déployez l’application dans votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3be12-270">Export, build and deploy the app to your HoloLens.</span></span>
* <span data-ttu-id="3be12-271">Rapprochez-vous de l’étape et transformez-la en côte à côte pour entendre la modification des sons.</span><span class="sxs-lookup"><span data-stu-id="3be12-271">Move closer and further from the Stage and turn side-to-side to hear the sounds change.</span></span>

## <a name="chapter-6---spatial-mapping"></a><span data-ttu-id="3be12-272">Chapitre 6-mappage spatial</span><span class="sxs-lookup"><span data-stu-id="3be12-272">Chapter 6 - Spatial mapping</span></span>

>[!VIDEO https://www.youtube.com/embed/Pkt1_wNLLXY]

<span data-ttu-id="3be12-273">Nous allons maintenant utiliser le [mappage spatial](spatial-mapping.md) pour placer la grille de jeux sur un objet réel dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="3be12-273">Now we are going to use [spatial mapping](spatial-mapping.md) to place the game board on a real object in the real world.</span></span>

### <a name="objectives"></a><span data-ttu-id="3be12-274">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3be12-274">Objectives</span></span>

* <span data-ttu-id="3be12-275">Intégrez votre monde réel dans le monde virtuel.</span><span class="sxs-lookup"><span data-stu-id="3be12-275">Bring your real world into the virtual world.</span></span>
* <span data-ttu-id="3be12-276">Placez vos hologrammes là où ils vous intéressent le plus.</span><span class="sxs-lookup"><span data-stu-id="3be12-276">Place your holograms where they matter most to you.</span></span>

### <a name="instructions"></a><span data-ttu-id="3be12-277">Instructions</span><span class="sxs-lookup"><span data-stu-id="3be12-277">Instructions</span></span>

* <span data-ttu-id="3be12-278">Dans Unity, cliquez sur  le dossier hologrammes dans le panneau projet.</span><span class="sxs-lookup"><span data-stu-id="3be12-278">In Unity, click on the **Holograms** folder in the Project panel.</span></span>
* <span data-ttu-id="3be12-279">Faites glisser la ressource de **mappage spatial** à la racine de la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="3be12-279">Drag the **Spatial Mapping** asset into the root of the **Hierarchy**.</span></span>
* <span data-ttu-id="3be12-280">Cliquez sur l’objet **mappage spatial** dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="3be12-280">Click on the **Spatial Mapping** object in the Hierarchy.</span></span>
* <span data-ttu-id="3be12-281">Dans le **panneau Inspecteur**, modifiez les propriétés suivantes:</span><span class="sxs-lookup"><span data-stu-id="3be12-281">In the **Inspector panel**, change the following properties:</span></span>
  * <span data-ttu-id="3be12-282">Cochez la case **dessiner des panneaux visuels** .</span><span class="sxs-lookup"><span data-stu-id="3be12-282">Check the **Draw Visual Meshes** box.</span></span>
  * <span data-ttu-id="3be12-283">Recherchez **matériel de dessin** , puis cliquez sur le cercle à droite.</span><span class="sxs-lookup"><span data-stu-id="3be12-283">Locate **Draw Material** and click the circle on the right.</span></span> <span data-ttu-id="3be12-284">Tapez «**Wireframe**» dans le champ de recherche en haut.</span><span class="sxs-lookup"><span data-stu-id="3be12-284">Type "**wireframe**" into the search field at the top.</span></span> <span data-ttu-id="3be12-285">Cliquez sur le résultat, puis fermez la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="3be12-285">Click on the result and then close the window.</span></span> <span data-ttu-id="3be12-286">Lorsque vous effectuez cette opération, la valeur de Draw Material doit être définie sur Wireframe.</span><span class="sxs-lookup"><span data-stu-id="3be12-286">When you do this, the value for Draw Material should get set to Wireframe.</span></span>
* <span data-ttu-id="3be12-287">Exportez, générez et déployez l’application dans votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3be12-287">Export, build and deploy the app to your HoloLens.</span></span>
* <span data-ttu-id="3be12-288">Lorsque l’application s’exécute, un maillage filaire se superpose à votre monde réel.</span><span class="sxs-lookup"><span data-stu-id="3be12-288">When the app runs, a wireframe mesh will overlay your real world.</span></span>
* <span data-ttu-id="3be12-289">Regardez comment une sphère enchaînée va tomber à l’étage, et à l’étage!</span><span class="sxs-lookup"><span data-stu-id="3be12-289">Watch how a rolling sphere will fall off the stage, and onto the floor!</span></span>

<span data-ttu-id="3be12-290">Nous allons maintenant vous montrer comment déplacer le OrigamiCollection vers un nouvel emplacement:</span><span class="sxs-lookup"><span data-stu-id="3be12-290">Now we'll show you how to move the OrigamiCollection to a new location:</span></span>

* <span data-ttu-id="3be12-291">Dans le dossier **scripts** , créez un script nommé **TapToPlaceParent**.</span><span class="sxs-lookup"><span data-stu-id="3be12-291">In the **Scripts** folder, create a script named **TapToPlaceParent**.</span></span>
* <span data-ttu-id="3be12-292">Dans la **hiérarchie**, développez le **OrigamiCollection** et sélectionnez l’objet **stage** .</span><span class="sxs-lookup"><span data-stu-id="3be12-292">In the **Hierarchy**, expand the **OrigamiCollection** and select the **Stage** object.</span></span>
* <span data-ttu-id="3be12-293">Faites glisser le script **TapToPlaceParent** sur l’objet stage.</span><span class="sxs-lookup"><span data-stu-id="3be12-293">Drag the **TapToPlaceParent** script onto the Stage object.</span></span>
* <span data-ttu-id="3be12-294">Ouvrez le script **TapToPlaceParent** dans Visual Studio et mettez-le à jour comme suit:</span><span class="sxs-lookup"><span data-stu-id="3be12-294">Open the **TapToPlaceParent** script in Visual Studio, and update it to be the following:</span></span>

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

* <span data-ttu-id="3be12-295">Exporter, générer et déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="3be12-295">Export, build and deploy the app.</span></span>
* <span data-ttu-id="3be12-296">Vous devez maintenant être en mesure de placer le jeu à un emplacement spécifique par gazing, à l’aide du geste Select, puis en le déplaçant vers un nouvel emplacement et en réutilisant le geste Select.</span><span class="sxs-lookup"><span data-stu-id="3be12-296">Now you should now be able to place the game in a specific location by gazing at it, using the Select gesture and then moving to a new location, and using the Select gesture again.</span></span>

## <a name="chapter-7---holographic-fun"></a><span data-ttu-id="3be12-297">Chapitre 7-divertissement holographique</span><span class="sxs-lookup"><span data-stu-id="3be12-297">Chapter 7 - Holographic fun</span></span>

### <a name="objectives"></a><span data-ttu-id="3be12-298">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3be12-298">Objectives</span></span>

* <span data-ttu-id="3be12-299">Révélez l’entrée à un sous-monde holographique.</span><span class="sxs-lookup"><span data-stu-id="3be12-299">Reveal the entrance to a holographic underworld.</span></span>

### <a name="instructions"></a><span data-ttu-id="3be12-300">Instructions</span><span class="sxs-lookup"><span data-stu-id="3be12-300">Instructions</span></span>

<span data-ttu-id="3be12-301">Nous allons maintenant vous montrer comment dévoiler le sous-monde holographique:</span><span class="sxs-lookup"><span data-stu-id="3be12-301">Now we'll show you how to uncover the holographic underworld:</span></span>

* <span data-ttu-id="3be12-302">Dans le  dossier hologrammes du panneau projet:</span><span class="sxs-lookup"><span data-stu-id="3be12-302">From the **Holograms** folder in the Project Panel:</span></span>
  * <span data-ttu-id="3be12-303">Faites glisser le sous- **monde** dans la hiérarchie pour être un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="3be12-303">Drag **Underworld** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
* <span data-ttu-id="3be12-304">Dans le dossier **scripts** , créez un script nommé **HitTarget**.</span><span class="sxs-lookup"><span data-stu-id="3be12-304">In the **Scripts** folder, create a script named **HitTarget**.</span></span>
* <span data-ttu-id="3be12-305">Dans la **hiérarchie**, développez **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="3be12-305">In the **Hierarchy**, expand the **OrigamiCollection**.</span></span>
* <span data-ttu-id="3be12-306">Développez l’objet **stage** et sélectionnez l’objet **cible** (ventilateur bleu).</span><span class="sxs-lookup"><span data-stu-id="3be12-306">Expand the **Stage** object and select the **Target** object (blue fan).</span></span>
* <span data-ttu-id="3be12-307">Faites glisser le script **HitTarget** sur l’objet **cible** .</span><span class="sxs-lookup"><span data-stu-id="3be12-307">Drag the **HitTarget** script onto the **Target** object.</span></span>
* <span data-ttu-id="3be12-308">Ouvrez le script **HitTarget** dans Visual Studio et mettez-le à jour comme suit:</span><span class="sxs-lookup"><span data-stu-id="3be12-308">Open the **HitTarget** script in Visual Studio, and update it to be the following:</span></span>

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

* <span data-ttu-id="3be12-309">Dans Unity, sélectionnez l’objet **cible** .</span><span class="sxs-lookup"><span data-stu-id="3be12-309">In Unity, select the **Target** object.</span></span>
* <span data-ttu-id="3be12-310">Deux propriétés publiques sont désormais visibles sur le composant **cible d’accès** et doivent référencer des objets dans notre scène:</span><span class="sxs-lookup"><span data-stu-id="3be12-310">Two public properties are now visible on the **Hit Target** component and need to reference objects in our scene:</span></span>
  * <span data-ttu-id="3be12-311">Faites glisser le sous- **monde** du volet de la **hiérarchie** vers **la propriété sous** le composant cible d' **accès** .</span><span class="sxs-lookup"><span data-stu-id="3be12-311">Drag **Underworld** from the **Hierarchy** panel to the **Underworld** property on the **Hit Target** component.</span></span>
  * <span data-ttu-id="3be12-312">Faites glisser **étape** du volet **hiérarchie** vers l' **objet pour masquer** la propriété sur le composant cible d' **accès** .</span><span class="sxs-lookup"><span data-stu-id="3be12-312">Drag **Stage** from the **Hierarchy** panel to the **Object to Hide** property on the **Hit Target** component.</span></span>
* <span data-ttu-id="3be12-313">Exporter, générer et déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="3be12-313">Export, build and deploy the app.</span></span>
* <span data-ttu-id="3be12-314">Placez la collection d’origamis à l’étage, puis utilisez le mouvement SELECT pour faire glisser une sphère.</span><span class="sxs-lookup"><span data-stu-id="3be12-314">Place the Origami Collection on the floor, and then use the Select gesture to make a sphere drop.</span></span>
* <span data-ttu-id="3be12-315">Lorsque la sphère atteint la cible (ventilateur bleu), une explosion se produit.</span><span class="sxs-lookup"><span data-stu-id="3be12-315">When the sphere hits the target (blue fan), an explosion will occur.</span></span> <span data-ttu-id="3be12-316">Le regroupement sera masqué et un trou au sous-monde s’affichera.</span><span class="sxs-lookup"><span data-stu-id="3be12-316">The collection will be hidden and a hole to the underworld will appear.</span></span>

## <a name="the-end"></a><span data-ttu-id="3be12-317">La fin</span><span class="sxs-lookup"><span data-stu-id="3be12-317">The end</span></span>

<span data-ttu-id="3be12-318">Et c’est la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3be12-318">And that's the end of this tutorial!</span></span>

<span data-ttu-id="3be12-319">Vous avez appris à:</span><span class="sxs-lookup"><span data-stu-id="3be12-319">You learned:</span></span>

* <span data-ttu-id="3be12-320">Comment créer une application holographique dans Unity.</span><span class="sxs-lookup"><span data-stu-id="3be12-320">How to create a holographic app in Unity.</span></span>
* <span data-ttu-id="3be12-321">Comment utiliser le point de vue du regard, du geste, de la voix, du son et du mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="3be12-321">How to make use of gaze, gesture, voice, sound, and spatial mapping.</span></span>
* <span data-ttu-id="3be12-322">Comment générer et déployer une application à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3be12-322">How to build and deploy an app using Visual Studio.</span></span>

<span data-ttu-id="3be12-323">Vous êtes maintenant prêt à commencer à créer votre propre expérience holographique!</span><span class="sxs-lookup"><span data-stu-id="3be12-323">You are now ready to start creating your own holographic experience!</span></span>

## <a name="see-also"></a><span data-ttu-id="3be12-324">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3be12-324">See also</span></span>

* [<span data-ttu-id="3be12-325">Réalité mixte - Principes fondamentaux - Cours 101E : Projet complet avec émulateur</span><span class="sxs-lookup"><span data-stu-id="3be12-325">MR Basics 101E: Complete project with emulator</span></span>](holograms-101e.md)
* [<span data-ttu-id="3be12-326">Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="3be12-326">Gaze</span></span>](gaze.md)
* [<span data-ttu-id="3be12-327">Mouvements</span><span class="sxs-lookup"><span data-stu-id="3be12-327">Gestures</span></span>](gestures.md)
* [<span data-ttu-id="3be12-328">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="3be12-328">Voice input</span></span>](voice-input.md)
* [<span data-ttu-id="3be12-329">Son spatial</span><span class="sxs-lookup"><span data-stu-id="3be12-329">Spatial sound</span></span>](spatial-sound.md)
* [<span data-ttu-id="3be12-330">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="3be12-330">Spatial mapping</span></span>](spatial-mapping.md)
