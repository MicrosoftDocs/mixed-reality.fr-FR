---
title: Principes fondamentaux de MR 101 - projet complet avec l’appareil
description: Suivez cette procédure pas à pas codage à l’aide de Unity, Visual Studio et HoloLens pour apprendre les principes fondamentaux de Windows Mixed Reality.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: une réalité, la réalité mixte Windows, HoloLens, mixte HOLOGRAMME, academy, didacticiel
ms.openlocfilehash: 043ffac8f30a4e29586478b5dca6ecccc2b5afd3
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593970"
---
>[!NOTE]
><span data-ttu-id="66f62-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="66f62-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="66f62-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="66f62-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="66f62-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="66f62-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="66f62-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="66f62-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="66f62-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="66f62-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="66f62-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="66f62-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-basics-101-complete-project-with-device"></a><span data-ttu-id="66f62-110">Principes de base MR 101 : Projet complet avec l’appareil</span><span class="sxs-lookup"><span data-stu-id="66f62-110">MR Basics 101: Complete project with device</span></span>

<br>

>[!VIDEO https://www.youtube.com/embed/XKIIEC5BMWg]

<span data-ttu-id="66f62-111">Ce didacticiel vous guidera dans un projet complet, créé dans Unity, qui illustre les fonctionnalités de Windows Mixed Reality core, notamment HoloLens [les regards](gaze.md), [mouvements](gestures.md), [entréevoix](voice-input.md), [son spatial](spatial-sound.md) et [mappage spatial](spatial-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="66f62-111">This tutorial will walk you through a complete project, built in Unity, that demonstrates core Windows Mixed Reality features on HoloLens including [gaze](gaze.md), [gestures](gestures.md), [voice input](voice-input.md), [spatial sound](spatial-sound.md) and [spatial mapping](spatial-mapping.md).</span></span>

<span data-ttu-id="66f62-112">Le didacticiel vous prendra environ une heure.</span><span class="sxs-lookup"><span data-stu-id="66f62-112">The tutorial will take approximately 1 hour to complete.</span></span>

## <a name="device-support"></a><span data-ttu-id="66f62-113">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="66f62-113">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="66f62-114">Cours</span><span class="sxs-lookup"><span data-stu-id="66f62-114">Course</span></span></th><th style="width:150px"> <span data-ttu-id="66f62-115"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="66f62-115"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="66f62-116"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="66f62-116"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="66f62-117">Principes de base MR 101 : Projet complet avec l’appareil</span><span class="sxs-lookup"><span data-stu-id="66f62-117">MR Basics 101: Complete project with device</span></span></td><td style="text-align: center;"> <span data-ttu-id="66f62-118">✔️</span><span class="sxs-lookup"><span data-stu-id="66f62-118">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="66f62-119">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="66f62-119">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="66f62-120">Prérequis</span><span class="sxs-lookup"><span data-stu-id="66f62-120">Prerequisites</span></span>

* <span data-ttu-id="66f62-121">Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="66f62-121">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="66f62-122">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="66f62-122">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="66f62-123">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="66f62-123">Project files</span></span>

* <span data-ttu-id="66f62-124">Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) requise par le projet.</span><span class="sxs-lookup"><span data-stu-id="66f62-124">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) required by the project.</span></span><span data-ttu-id="66f62-125"> Nécessite Unity 2017.2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="66f62-125"> Requires Unity 2017.2 or later.</span></span>
  * <span data-ttu-id="66f62-126">Si vous avez besoin de prise en charge de Unity 5.6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).</span><span class="sxs-lookup"><span data-stu-id="66f62-126">If you still need Unity 5.6 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).</span></span>
  * <span data-ttu-id="66f62-127">Si vous avez besoin de prise en charge de Unity 5.5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).</span><span class="sxs-lookup"><span data-stu-id="66f62-127">If you still need Unity 5.5 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).</span></span>
  * <span data-ttu-id="66f62-128">Si vous avez besoin de prise en charge de Unity 5.4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).</span><span class="sxs-lookup"><span data-stu-id="66f62-128">If you still need Unity 5.4 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).</span></span>
* <span data-ttu-id="66f62-129">Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="66f62-129">Un-archive the files to your desktop or other easy to reach location.</span></span> <span data-ttu-id="66f62-130">Conservez le nom de dossier en tant que **Origami**.</span><span class="sxs-lookup"><span data-stu-id="66f62-130">Keep the folder name as **Origami**.</span></span>

>[!NOTE]
><span data-ttu-id="66f62-131">Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).</span><span class="sxs-lookup"><span data-stu-id="66f62-131">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).</span></span>

## <a name="chapter-1---holo-world"></a><span data-ttu-id="66f62-132">Chapitre 1 - « Holo » world</span><span class="sxs-lookup"><span data-stu-id="66f62-132">Chapter 1 - "Holo" world</span></span>

>[!VIDEO https://www.youtube.com/embed/PmtZGjYFroY]

<span data-ttu-id="66f62-133">Dans ce chapitre, nous le programme d’installation de notre premier projet Unity et les étapes à la build et processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="66f62-133">In this chapter, we'll setup our first Unity project and step through the build and deploy process.</span></span>

### <a name="objectives"></a><span data-ttu-id="66f62-134">Objectifs</span><span class="sxs-lookup"><span data-stu-id="66f62-134">Objectives</span></span>

* <span data-ttu-id="66f62-135">Configurer Unity pour le développement HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="66f62-135">Set up Unity for holographic development.</span></span>
* <span data-ttu-id="66f62-136">Rendre un hologramme.</span><span class="sxs-lookup"><span data-stu-id="66f62-136">Make a hologram.</span></span>
* <span data-ttu-id="66f62-137">Consultez un hologramme que vous avez apportées.</span><span class="sxs-lookup"><span data-stu-id="66f62-137">See a hologram that you made.</span></span>

### <a name="instructions"></a><span data-ttu-id="66f62-138">Instructions</span><span class="sxs-lookup"><span data-stu-id="66f62-138">Instructions</span></span>

* <span data-ttu-id="66f62-139">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="66f62-139">Start Unity.</span></span>
* <span data-ttu-id="66f62-140">Sélectionnez **Open**.</span><span class="sxs-lookup"><span data-stu-id="66f62-140">Select **Open**.</span></span>
* <span data-ttu-id="66f62-141">Entrez l’emplacement que le **Origami** dossier vous précédemment non archivés.</span><span class="sxs-lookup"><span data-stu-id="66f62-141">Enter location as the **Origami** folder you previously un-archived.</span></span>
* <span data-ttu-id="66f62-142">Sélectionnez **Origami** et cliquez sur **sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="66f62-142">Select **Origami** and click **Select Folder**.</span></span>
* <span data-ttu-id="66f62-143">Dans la mesure où le **Origami** projet ne contient pas d’une scène, enregistrer la scène vide par défaut dans un nouveau fichier : **Fichier** / **enregistrer la scène sous**.</span><span class="sxs-lookup"><span data-stu-id="66f62-143">Since the **Origami** project does not contain a scene, save the empty default scene to a new file using: **File** / **Save Scene As**.</span></span>
* <span data-ttu-id="66f62-144">Nommez la nouvelle scène **Origami** et appuyez sur la **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="66f62-144">Name the new scene **Origami** and press the **Save** button.</span></span>

#### <a name="setup-the-main-virtual-camera"></a><span data-ttu-id="66f62-145">Le programme d’installation de la caméra virtuelle principale</span><span class="sxs-lookup"><span data-stu-id="66f62-145">Setup the main virtual camera</span></span>

* <span data-ttu-id="66f62-146">Dans le **hiérarchie panneau**, sélectionnez **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="66f62-146">In the **Hierarchy Panel**, select **Main Camera**.</span></span>
* <span data-ttu-id="66f62-147">Dans le **inspecteur** positionnez sa transformation **0,0,0**.</span><span class="sxs-lookup"><span data-stu-id="66f62-147">In the **Inspector** set its transform position to **0,0,0**.</span></span>
* <span data-ttu-id="66f62-148">Rechercher la **effacer les indicateurs** propriété et modifier la liste déroulante à partir de **Skybox** à **couleur unie**.</span><span class="sxs-lookup"><span data-stu-id="66f62-148">Find the **Clear Flags** property, and change the dropdown from **Skybox** to **Solid color**.</span></span>
* <span data-ttu-id="66f62-149">Cliquez sur le **arrière-plan** champ pour ouvrir un sélecteur de couleurs.</span><span class="sxs-lookup"><span data-stu-id="66f62-149">Click on the **Background** field to open a color picker.</span></span>
* <span data-ttu-id="66f62-150">Définissez **R, G, B et A** à **0**.</span><span class="sxs-lookup"><span data-stu-id="66f62-150">Set **R, G, B, and A** to **0**.</span></span>

#### <a name="setup-the-scene"></a><span data-ttu-id="66f62-151">Le programme d’installation de la scène</span><span class="sxs-lookup"><span data-stu-id="66f62-151">Setup the scene</span></span>

* <span data-ttu-id="66f62-152">Dans le **hiérarchie panneau**, cliquez sur **créer** et **créer vide**.</span><span class="sxs-lookup"><span data-stu-id="66f62-152">In the **Hierarchy Panel**, click on **Create** and **Create Empty**.</span></span>
* <span data-ttu-id="66f62-153">Cliquez sur le nouveau **GameObject** et sélectionnez Renommer.</span><span class="sxs-lookup"><span data-stu-id="66f62-153">Right-click the new **GameObject** and select Rename.</span></span> <span data-ttu-id="66f62-154">Renommer le GameObject à **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="66f62-154">Rename the GameObject to **OrigamiCollection**.</span></span>
* <span data-ttu-id="66f62-155">À partir de la **hologrammes** dossier dans le panneau de configuration de projet (développez actifs et sélectionnez hologrammes ou double-cliquez sur le dossier hologrammes dans le panneau de configuration de projet) :</span><span class="sxs-lookup"><span data-stu-id="66f62-155">From the **Holograms** folder in the Project Panel (expand Assets and select Holograms or double click the Holograms folder in the Project Panel):</span></span>
  * <span data-ttu-id="66f62-156">Faites glisser **étape** dans la hiérarchie soit un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="66f62-156">Drag **Stage** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
  * <span data-ttu-id="66f62-157">Faites glisser **Sphere1** dans la hiérarchie soit un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="66f62-157">Drag **Sphere1** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
  * <span data-ttu-id="66f62-158">Faites glisser **Sphere2** dans la hiérarchie soit un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="66f62-158">Drag **Sphere2** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
* <span data-ttu-id="66f62-159">Avec le bouton droit le **lumière directionnelle** de l’objet dans le **hiérarchie panneau** et sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="66f62-159">Right-click the **Directional Light** object in the **Hierarchy Panel** and select **Delete**.</span></span>
* <span data-ttu-id="66f62-160">À partir de la **hologrammes** dossier, faites glisser **lumières** à la racine de la **hiérarchie panneau**.</span><span class="sxs-lookup"><span data-stu-id="66f62-160">From the **Holograms** folder, drag **Lights** into the root of the **Hierarchy Panel**.</span></span>
* <span data-ttu-id="66f62-161">Dans le **hiérarchie**, sélectionnez le **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="66f62-161">In the **Hierarchy**, select the **OrigamiCollection**.</span></span>
* <span data-ttu-id="66f62-162">Dans le **inspecteur**, positionnez la transformation **0, -0,5, 2.0**.</span><span class="sxs-lookup"><span data-stu-id="66f62-162">In the **Inspector**, set the transform position to **0, -0.5, 2.0**.</span></span>
* <span data-ttu-id="66f62-163">Appuyez sur la **lire** bouton dans Unity pour afficher un aperçu votre hologrammes.</span><span class="sxs-lookup"><span data-stu-id="66f62-163">Press the **Play** button in Unity to preview your holograms.</span></span>
* <span data-ttu-id="66f62-164">Vous devez voir les objets Origami dans la fenêtre d’aperçu.</span><span class="sxs-lookup"><span data-stu-id="66f62-164">You should see the Origami objects in the preview window.</span></span>
* <span data-ttu-id="66f62-165">Appuyez sur **lire** une deuxième fois pour arrêter le mode d’aperçu.</span><span class="sxs-lookup"><span data-stu-id="66f62-165">Press **Play** a second time to stop preview mode.</span></span>

#### <a name="export-the-project-from-unity-to-visual-studio"></a><span data-ttu-id="66f62-166">Exportez le projet à partir d’Unity pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66f62-166">Export the project from Unity to Visual Studio</span></span>

* <span data-ttu-id="66f62-167">Dans, sélectionnez Unity **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="66f62-167">In Unity select **File > Build Settings**.</span></span>
* <span data-ttu-id="66f62-168">Sélectionnez **plateforme Windows universelle** dans le **plateforme** liste et cliquez sur **plateforme de commutation**.</span><span class="sxs-lookup"><span data-stu-id="66f62-168">Select **Universal Windows Platform** in the **Platform** list and click **Switch Platform**.</span></span>
* <span data-ttu-id="66f62-169">Définissez **SDK** à **universelle 10** et **Type de Build** à **D3D**.</span><span class="sxs-lookup"><span data-stu-id="66f62-169">Set **SDK** to **Universal 10** and **Build Type** to **D3D**.</span></span>
* <span data-ttu-id="66f62-170">Vérifiez **Unity C# projets**.</span><span class="sxs-lookup"><span data-stu-id="66f62-170">Check **Unity C# Projects**.</span></span>
* <span data-ttu-id="66f62-171">Cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="66f62-171">Click **Add Open Scenes** to add the scene.</span></span>
* <span data-ttu-id="66f62-172">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="66f62-172">Click **Build**.</span></span>
* <span data-ttu-id="66f62-173">Dans la fenêtre Explorateur de fichiers qui s’affiche, créez un **nouveau dossier** nommé « Application ».</span><span class="sxs-lookup"><span data-stu-id="66f62-173">In the file explorer window that appears, create a **New Folder** named "App".</span></span>
* <span data-ttu-id="66f62-174">Clic le **dossier application**.</span><span class="sxs-lookup"><span data-stu-id="66f62-174">Single click the **App Folder**.</span></span>
* <span data-ttu-id="66f62-175">Appuyez sur **sélectionnez dossier**.</span><span class="sxs-lookup"><span data-stu-id="66f62-175">Press **Select Folder**.</span></span>
* <span data-ttu-id="66f62-176">Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="66f62-176">When Unity is done, a File Explorer window will appear.</span></span>
* <span data-ttu-id="66f62-177">Ouvrez le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="66f62-177">Open the **App** folder.</span></span>
* <span data-ttu-id="66f62-178">Open (double clic) **Origami.sln**.</span><span class="sxs-lookup"><span data-stu-id="66f62-178">Open (double click) **Origami.sln**.</span></span>
* <span data-ttu-id="66f62-179">À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **X86**.</span><span class="sxs-lookup"><span data-stu-id="66f62-179">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **X86**.</span></span>
* <span data-ttu-id="66f62-180">Cliquez sur la flèche en regard du bouton de l’appareil, puis sélectionnez **Machine distante** pour déployer via le Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="66f62-180">Click on the arrow next to the Device button, and select **Remote Machine** to deploy over Wi-Fi.</span></span>
  * <span data-ttu-id="66f62-181">Définir le **adresse** au nom ou adresse IP de votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="66f62-181">Set the **Address** to the name or IP address of your HoloLens.</span></span> <span data-ttu-id="66f62-182">Si vous ne connaissez pas votre adresse IP du périphérique, recherchez dans **Paramètres > réseau & Internet > Options avancées** ou demandez à Cortana **« Hey Cortana, quelle est mon adresse IP ? »**</span><span class="sxs-lookup"><span data-stu-id="66f62-182">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options** or ask Cortana **"Hey Cortana, What's my IP address?"**</span></span>
  * <span data-ttu-id="66f62-183">Si le HoloLens est connecté via USB, vous pouvez sélectionner à la place **appareil** pour déployer via USB.</span><span class="sxs-lookup"><span data-stu-id="66f62-183">If the HoloLens is attached over USB, you may instead select **Device** to deploy over USB.</span></span>
  * <span data-ttu-id="66f62-184">Laissez le **Mode d’authentification** définie sur **universelle**.</span><span class="sxs-lookup"><span data-stu-id="66f62-184">Leave the **Authentication Mode** set to **Universal**.</span></span>
  * <span data-ttu-id="66f62-185">Cliquez sur **sélectionnez**</span><span class="sxs-lookup"><span data-stu-id="66f62-185">Click **Select**</span></span>

* <span data-ttu-id="66f62-186">Cliquez sur **Déboguer > Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="66f62-186">Click **Debug > Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="66f62-187">S’il s’agit de la première fois le déploiement sur votre périphérique, vous devrez [Couplez-le Visual Studio](using-visual-studio.md#pairing-your-device-hololens-(1st-gen)).</span><span class="sxs-lookup"><span data-stu-id="66f62-187">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device-hololens-(1st-gen)).</span></span>

* <span data-ttu-id="66f62-188">Le projet Origami sera désormais générer, déployer sur votre HoloLens, puis exécutez.</span><span class="sxs-lookup"><span data-stu-id="66f62-188">The Origami project will now build, deploy to your HoloLens, and then run.</span></span>
* <span data-ttu-id="66f62-189">Placez sur votre HoloLens et observer cet onglet pour afficher votre nouvelle hologrammes.</span><span class="sxs-lookup"><span data-stu-id="66f62-189">Put on your HoloLens and look around to see your new holograms.</span></span>

## <a name="chapter-2---gaze"></a><span data-ttu-id="66f62-190">Chapitre 2 - regards</span><span class="sxs-lookup"><span data-stu-id="66f62-190">Chapter 2 - Gaze</span></span>

>[!VIDEO https://www.youtube.com/embed/MSO2BoFSQbM]

<span data-ttu-id="66f62-191">Dans ce chapitre, nous allons introduire le premier des trois façons d’interagir avec votre hologrammes-- [les regards](gaze.md).</span><span class="sxs-lookup"><span data-stu-id="66f62-191">In this chapter, we are going to introduce the first of three ways of interacting with your holograms -- [gaze](gaze.md).</span></span>

### <a name="objectives"></a><span data-ttu-id="66f62-192">Objectifs</span><span class="sxs-lookup"><span data-stu-id="66f62-192">Objectives</span></span>

* <span data-ttu-id="66f62-193">Visualiser votre regard à l’aide d’un curseur verrouillé de monde.</span><span class="sxs-lookup"><span data-stu-id="66f62-193">Visualize your gaze using a world-locked cursor.</span></span>

### <a name="instructions"></a><span data-ttu-id="66f62-194">Instructions</span><span class="sxs-lookup"><span data-stu-id="66f62-194">Instructions</span></span>

* <span data-ttu-id="66f62-195">Revenez à votre projet Unity et fermer la fenêtre Paramètres de Build si elle est toujours ouverte.</span><span class="sxs-lookup"><span data-stu-id="66f62-195">Go back to your Unity project, and close the Build Settings window if it's still open.</span></span>
* <span data-ttu-id="66f62-196">Sélectionnez le **Vntana** dossier dans le **panneau projet**.</span><span class="sxs-lookup"><span data-stu-id="66f62-196">Select the **Holograms** folder in the **Project panel**.</span></span>
* <span data-ttu-id="66f62-197">Faites glisser le **curseur** de l’objet dans le **Panneau de la hiérarchie** au niveau racine.</span><span class="sxs-lookup"><span data-stu-id="66f62-197">Drag the **Cursor** object into the **Hierarchy panel** at the root level.</span></span>
* <span data-ttu-id="66f62-198">Double-cliquez sur le **curseur** objet effectue une examiner plus en détail.</span><span class="sxs-lookup"><span data-stu-id="66f62-198">Double-click on the **Cursor** object to take a closer look at it.</span></span>
* <span data-ttu-id="66f62-199">Avec le bouton droit sur le **Scripts** dossier dans le panneau de configuration de projet.</span><span class="sxs-lookup"><span data-stu-id="66f62-199">Right-click on the **Scripts** folder in the Project panel.</span></span>
* <span data-ttu-id="66f62-200">Cliquez sur le **créer** sous-menu.</span><span class="sxs-lookup"><span data-stu-id="66f62-200">Click the **Create** sub-menu.</span></span>
* <span data-ttu-id="66f62-201">Sélectionnez  **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="66f62-201">Select **C# Script**.</span></span>
* <span data-ttu-id="66f62-202">Nommez le script **WorldCursor**.</span><span class="sxs-lookup"><span data-stu-id="66f62-202">Name the script **WorldCursor**.</span></span> <span data-ttu-id="66f62-203">Remarque: Le nom est sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="66f62-203">Note: The name is case-sensitive.</span></span> <span data-ttu-id="66f62-204">Vous n’avez pas besoin ajouter l’extension .cs.</span><span class="sxs-lookup"><span data-stu-id="66f62-204">You do not need to add the .cs extension.</span></span>
* <span data-ttu-id="66f62-205">Sélectionnez le **curseur** de l’objet dans le **Panneau de la hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="66f62-205">Select the **Cursor** object in the **Hierarchy panel**.</span></span>
* <span data-ttu-id="66f62-206">Faites glisser et déposez le **WorldCursor** écrite dans le **panneau Inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="66f62-206">Drag and drop the **WorldCursor** script into the **Inspector panel**.</span></span>
* <span data-ttu-id="66f62-207">Double-cliquez sur le **WorldCursor** script pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66f62-207">Double-click the **WorldCursor** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="66f62-208">Copiez et collez ce code dans **WorldCursor.cs** et **Enregistrer tout**.</span><span class="sxs-lookup"><span data-stu-id="66f62-208">Copy and paste this code into **WorldCursor.cs** and **Save All**.</span></span>

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

* <span data-ttu-id="66f62-209">Régénérer l’application à partir de **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="66f62-209">Rebuild the app from **File > Build Settings**.</span></span>
* <span data-ttu-id="66f62-210">Revenez à la solution Visual Studio utilisée précédemment pour déployer sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="66f62-210">Return to the Visual Studio solution previously used to deploy to your HoloLens.</span></span>
* <span data-ttu-id="66f62-211">Sélectionnez « Recharger All » lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="66f62-211">Select 'Reload All' when prompted.</span></span>
* <span data-ttu-id="66f62-212">Cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="66f62-212">Click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
* <span data-ttu-id="66f62-213">À présent, regardez autour de la scène et notez la façon dont le curseur interagit avec la forme d’objets.</span><span class="sxs-lookup"><span data-stu-id="66f62-213">Now look around the scene and notice how the cursor interacts with the shape of objects.</span></span>

## <a name="chapter-3---gestures"></a><span data-ttu-id="66f62-214">Chapitre 3 - mouvements</span><span class="sxs-lookup"><span data-stu-id="66f62-214">Chapter 3 - Gestures</span></span>

>[!VIDEO https://www.youtube.com/embed/kW3ThJ2MbvQ]

<span data-ttu-id="66f62-215">Dans ce chapitre, nous allons ajouter la prise en charge de [mouvements](gestures.md).</span><span class="sxs-lookup"><span data-stu-id="66f62-215">In this chapter, we'll add support for [gestures](gestures.md).</span></span> <span data-ttu-id="66f62-216">Lorsque l’utilisateur sélectionne une sphère de papier, nous allons rendre la sphère se répartissent en activant la gravité, à l’aide du moteur de physique d’Unity.</span><span class="sxs-lookup"><span data-stu-id="66f62-216">When the user selects a paper sphere, we'll make the sphere fall by turning on gravity using Unity's physics engine.</span></span>

### <a name="objectives"></a><span data-ttu-id="66f62-217">Objectifs</span><span class="sxs-lookup"><span data-stu-id="66f62-217">Objectives</span></span>

* <span data-ttu-id="66f62-218">Contrôler votre hologrammes avec le mouvement de sélection.</span><span class="sxs-lookup"><span data-stu-id="66f62-218">Control your holograms with the Select gesture.</span></span>

### <a name="instructions"></a><span data-ttu-id="66f62-219">Instructions</span><span class="sxs-lookup"><span data-stu-id="66f62-219">Instructions</span></span>

<span data-ttu-id="66f62-220">Nous allons commencer par créer un script puis peut détecter le mouvement de sélection.</span><span class="sxs-lookup"><span data-stu-id="66f62-220">We'll start by creating a script then can detect the Select gesture.</span></span>

* <span data-ttu-id="66f62-221">Dans le **Scripts** dossier, créez un script nommé **GazeGestureManager**.</span><span class="sxs-lookup"><span data-stu-id="66f62-221">In the **Scripts** folder, create a script named **GazeGestureManager**.</span></span>
* <span data-ttu-id="66f62-222">Faites glisser le **GazeGestureManager** de script sur le **OrigamiCollection** objet dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="66f62-222">Drag the **GazeGestureManager** script onto the **OrigamiCollection** object in the Hierarchy.</span></span>
* <span data-ttu-id="66f62-223">Ouvrez le **GazeGestureManager** de script dans Visual Studio et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="66f62-223">Open the **GazeGestureManager** script in Visual Studio and add the following code:</span></span>

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

* <span data-ttu-id="66f62-224">Créer un autre script dans le dossier Scripts, cette fois nommée **SphereCommands**.</span><span class="sxs-lookup"><span data-stu-id="66f62-224">Create another script in the Scripts folder, this time named **SphereCommands**.</span></span>
* <span data-ttu-id="66f62-225">Développez le **OrigamiCollection** objet dans la vue de la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="66f62-225">Expand the **OrigamiCollection** object in the Hierarchy view.</span></span>
* <span data-ttu-id="66f62-226">Faites glisser le **SphereCommands** de script sur le **Sphere1** objet dans le volet de la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="66f62-226">Drag the **SphereCommands** script onto the **Sphere1** object in the Hierarchy panel.</span></span>
* <span data-ttu-id="66f62-227">Faites glisser le **SphereCommands** de script sur le **Sphere2** objet dans le volet de la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="66f62-227">Drag the **SphereCommands** script onto the **Sphere2** object in the Hierarchy panel.</span></span>
* <span data-ttu-id="66f62-228">Ouvrez le script dans Visual Studio pour la modification et remplacez le code par défaut avec ce :</span><span class="sxs-lookup"><span data-stu-id="66f62-228">Open the script in Visual Studio for editing, and replace the default code with this:</span></span>

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

* <span data-ttu-id="66f62-229">Exporter, générer et déployer l’application sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="66f62-229">Export, build and deploy the app to your HoloLens.</span></span>
* <span data-ttu-id="66f62-230">Regarder l’un de la couleur des sphères.</span><span class="sxs-lookup"><span data-stu-id="66f62-230">Look at one of the spheres.</span></span>
* <span data-ttu-id="66f62-231">Effectuez le geste select et regardez la sphère déposer sur l’aire sous.</span><span class="sxs-lookup"><span data-stu-id="66f62-231">Perform the select gesture and watch the sphere drop onto the surface below.</span></span>

## <a name="chapter-4---voice"></a><span data-ttu-id="66f62-232">Chapitre 4 - Voice</span><span class="sxs-lookup"><span data-stu-id="66f62-232">Chapter 4 - Voice</span></span>

>[!VIDEO https://www.youtube.com/embed/1-Aq0VVtHM8]

<span data-ttu-id="66f62-233">Dans ce chapitre, nous allons ajouter la prise en charge pour deux [commandes vocales](voice-input.md): « Réinitialisation world » pour renvoyer la couleur des sphères supprimés à leur emplacement d’origine, « Drop sphère » pour rendre la sphère appartiennent.</span><span class="sxs-lookup"><span data-stu-id="66f62-233">In this chapter, we'll add support for two [voice commands](voice-input.md): "Reset world" to return the dropped spheres to their original location, and "Drop sphere" to make the sphere fall.</span></span>

### <a name="objectives"></a><span data-ttu-id="66f62-234">Objectifs</span><span class="sxs-lookup"><span data-stu-id="66f62-234">Objectives</span></span>

* <span data-ttu-id="66f62-235">Ajouter des commandes vocales qui écoutent toujours en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="66f62-235">Add voice commands that always listen in the background.</span></span>
* <span data-ttu-id="66f62-236">Créer un hologramme qui réagit à une commande vocale.</span><span class="sxs-lookup"><span data-stu-id="66f62-236">Create a hologram that reacts to a voice command.</span></span>

### <a name="instructions"></a><span data-ttu-id="66f62-237">Instructions</span><span class="sxs-lookup"><span data-stu-id="66f62-237">Instructions</span></span>

* <span data-ttu-id="66f62-238">Dans le **Scripts** dossier, créez un script nommé **SpeechManager**.</span><span class="sxs-lookup"><span data-stu-id="66f62-238">In the **Scripts** folder, create a script named **SpeechManager**.</span></span>
* <span data-ttu-id="66f62-239">Faites glisser le **SpeechManager** de script sur le **OrigamiCollection** objet dans la hiérarchie</span><span class="sxs-lookup"><span data-stu-id="66f62-239">Drag the **SpeechManager** script onto the **OrigamiCollection** object in the Hierarchy</span></span>
* <span data-ttu-id="66f62-240">Ouvrez le **SpeechManager** script dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66f62-240">Open the **SpeechManager** script in Visual Studio.</span></span>
* <span data-ttu-id="66f62-241">Copiez et collez ce code dans **SpeechManager.cs** et **Enregistrer tout**:</span><span class="sxs-lookup"><span data-stu-id="66f62-241">Copy and paste this code into **SpeechManager.cs** and **Save All**:</span></span>

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

* <span data-ttu-id="66f62-242">Ouvrez le **SphereCommands** script dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66f62-242">Open the **SphereCommands** script in Visual Studio.</span></span>
* <span data-ttu-id="66f62-243">Mettre à jour le script comme suit :</span><span class="sxs-lookup"><span data-stu-id="66f62-243">Update the script to read as follows:</span></span>

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

* <span data-ttu-id="66f62-244">Exporter, générer et déployer l’application sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="66f62-244">Export, build and deploy the app to your HoloLens.</span></span>
* <span data-ttu-id="66f62-245">Regarder un de la couleur des sphères et dire «**sphère Drop**».</span><span class="sxs-lookup"><span data-stu-id="66f62-245">Look at one of the spheres, and say "**Drop Sphere**".</span></span>
* <span data-ttu-id="66f62-246">Par exemple «**World réinitialiser**» pour les ramener dans leur position initiale.</span><span class="sxs-lookup"><span data-stu-id="66f62-246">Say "**Reset World**" to bring them back to their initial positions.</span></span>

## <a name="chapter-5---spatial-sound"></a><span data-ttu-id="66f62-247">Chapitre 5 - son Spatial</span><span class="sxs-lookup"><span data-stu-id="66f62-247">Chapter 5 - Spatial sound</span></span>

>[!VIDEO https://www.youtube.com/embed/Aj4de5Ncbfo]

<span data-ttu-id="66f62-248">Dans ce chapitre, nous allons ajouter de la musique à l’application et ensuite déclencher effets sonores sur certaines actions.</span><span class="sxs-lookup"><span data-stu-id="66f62-248">In this chapter, we'll add music to the app, and then trigger sound effects on certain actions.</span></span> <span data-ttu-id="66f62-249">Nous allons utiliser [son spatial](spatial-sound.md) afin de donner des sons à un emplacement spécifique dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="66f62-249">We'll be using [spatial sound](spatial-sound.md) to give sounds a specific location in 3D space.</span></span>

### <a name="objectives"></a><span data-ttu-id="66f62-250">Objectifs</span><span class="sxs-lookup"><span data-stu-id="66f62-250">Objectives</span></span>

* <span data-ttu-id="66f62-251">Écoutez hologrammes dans votre monde.</span><span class="sxs-lookup"><span data-stu-id="66f62-251">Hear holograms in your world.</span></span>

### <a name="instructions"></a><span data-ttu-id="66f62-252">Instructions</span><span class="sxs-lookup"><span data-stu-id="66f62-252">Instructions</span></span>

* <span data-ttu-id="66f62-253">Dans Sélectionnez Unity dans le menu supérieur **Modifier > Paramètres du projet > Audio**</span><span class="sxs-lookup"><span data-stu-id="66f62-253">In Unity select from the top menu **Edit > Project Settings > Audio**</span></span>
* <span data-ttu-id="66f62-254">Dans le panneau de l’inspecteur sur le côté droit, recherchez le **plug-in spatial** paramètre et sélectionnez **MS HRTF Spatializer**.</span><span class="sxs-lookup"><span data-stu-id="66f62-254">In the Inspector Panel on the right side, find the **Spatializer Plugin** setting and select **MS HRTF Spatializer**.</span></span>
* <span data-ttu-id="66f62-255">À partir de la **hologrammes** dossier dans le volet de projet, faites glisser le **ambiance** de l’objet sur le **OrigamiCollection** objet dans le volet de la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="66f62-255">From the **Holograms** folder in the Project panel, drag the **Ambience** object onto the **OrigamiCollection** object in the Hierarchy Panel.</span></span>
* <span data-ttu-id="66f62-256">Sélectionnez **OrigamiCollection** et recherchez le **Audio Source** composant dans le panneau de l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="66f62-256">Select **OrigamiCollection** and find the **Audio Source** component in the Inspector panel.</span></span> <span data-ttu-id="66f62-257">Modifier ces propriétés :</span><span class="sxs-lookup"><span data-stu-id="66f62-257">Change these properties:</span></span>
  * <span data-ttu-id="66f62-258">Vérifier le **Spatialize** propriété.</span><span class="sxs-lookup"><span data-stu-id="66f62-258">Check the **Spatialize** property.</span></span>
  * <span data-ttu-id="66f62-259">Vérifier le **jouer sur éveillés**.</span><span class="sxs-lookup"><span data-stu-id="66f62-259">Check the **Play On Awake**.</span></span>
  * <span data-ttu-id="66f62-260">Modification **Blend Spatial** à **3D** en faisant glisser le curseur complètement à droite.</span><span class="sxs-lookup"><span data-stu-id="66f62-260">Change **Spatial Blend** to **3D** by dragging the slider all the way to the right.</span></span> <span data-ttu-id="66f62-261">Lorsque vous déplacez le curseur, la valeur doit changer à partir de 0 à 1.</span><span class="sxs-lookup"><span data-stu-id="66f62-261">The value should change from 0 to 1 when you move the slider.</span></span>
  * <span data-ttu-id="66f62-262">Vérifier le **boucle** propriété.</span><span class="sxs-lookup"><span data-stu-id="66f62-262">Check the **Loop** property.</span></span>
  * <span data-ttu-id="66f62-263">Développez **les paramètres audio 3D**, puis entrez **0.1** pour **niveau Doppler**.</span><span class="sxs-lookup"><span data-stu-id="66f62-263">Expand **3D Sound Settings**, and enter **0.1** for **Doppler Level**.</span></span>
  * <span data-ttu-id="66f62-264">Définissez **Volume écrêtage** à **écrêtage logarithmique**.</span><span class="sxs-lookup"><span data-stu-id="66f62-264">Set **Volume Rolloff** to **Logarithmic Rolloff**.</span></span>
  * <span data-ttu-id="66f62-265">Définissez **Max Distance** à **20**.</span><span class="sxs-lookup"><span data-stu-id="66f62-265">Set **Max Distance** to **20**.</span></span>
* <span data-ttu-id="66f62-266">Dans le **Scripts** dossier, créez un script nommé **SphereSounds**.</span><span class="sxs-lookup"><span data-stu-id="66f62-266">In the **Scripts** folder, create a script named **SphereSounds**.</span></span>
* <span data-ttu-id="66f62-267">Faites glisser et déposez **SphereSounds** à la **Sphere1** et **Sphere2** objets dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="66f62-267">Drag and drop **SphereSounds** to the **Sphere1** and **Sphere2** objects in the Hierarchy.</span></span>
* <span data-ttu-id="66f62-268">Ouvrez **SphereSounds** dans Visual Studio, mettre à jour le code suivant et **Enregistrer tout**.</span><span class="sxs-lookup"><span data-stu-id="66f62-268">Open **SphereSounds** in Visual Studio, update the following code and **Save All**.</span></span>

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

* <span data-ttu-id="66f62-269">Enregistrer le script et revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="66f62-269">Save the script, and return to Unity.</span></span>
* <span data-ttu-id="66f62-270">Exporter, générer et déployer l’application sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="66f62-270">Export, build and deploy the app to your HoloLens.</span></span>
* <span data-ttu-id="66f62-271">Rapproche et plus éloigné de la scène et activer le côte à côte d’entendre les sons à modifier.</span><span class="sxs-lookup"><span data-stu-id="66f62-271">Move closer and further from the Stage and turn side-to-side to hear the sounds change.</span></span>

## <a name="chapter-6---spatial-mapping"></a><span data-ttu-id="66f62-272">Mappage du chapitre 6 – Spatial</span><span class="sxs-lookup"><span data-stu-id="66f62-272">Chapter 6 - Spatial mapping</span></span>

>[!VIDEO https://www.youtube.com/embed/Pkt1_wNLLXY]

<span data-ttu-id="66f62-273">Maintenant nous allons utiliser [mappage spatial](spatial-mapping.md) pour placer le plateau de jeu sur un objet réel dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="66f62-273">Now we are going to use [spatial mapping](spatial-mapping.md) to place the game board on a real object in the real world.</span></span>

### <a name="objectives"></a><span data-ttu-id="66f62-274">Objectifs</span><span class="sxs-lookup"><span data-stu-id="66f62-274">Objectives</span></span>

* <span data-ttu-id="66f62-275">Placez votre monde réel dans le monde virtuel.</span><span class="sxs-lookup"><span data-stu-id="66f62-275">Bring your real world into the virtual world.</span></span>
* <span data-ttu-id="66f62-276">Placez votre hologrammes où ils vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="66f62-276">Place your holograms where they matter most to you.</span></span>

### <a name="instructions"></a><span data-ttu-id="66f62-277">Instructions</span><span class="sxs-lookup"><span data-stu-id="66f62-277">Instructions</span></span>

* <span data-ttu-id="66f62-278">Dans Unity, cliquez sur le **hologrammes** dossier dans le panneau de configuration de projet.</span><span class="sxs-lookup"><span data-stu-id="66f62-278">In Unity, click on the **Holograms** folder in the Project panel.</span></span>
* <span data-ttu-id="66f62-279">Faites glisser le **mappage Spatial** actif à la racine de la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="66f62-279">Drag the **Spatial Mapping** asset into the root of the **Hierarchy**.</span></span>
* <span data-ttu-id="66f62-280">Cliquez sur le **mappage Spatial** objet dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="66f62-280">Click on the **Spatial Mapping** object in the Hierarchy.</span></span>
* <span data-ttu-id="66f62-281">Dans le **panneau Inspecteur**, modifiez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="66f62-281">In the **Inspector panel**, change the following properties:</span></span>
  * <span data-ttu-id="66f62-282">Vérifier le **dessiner les maillages Visual** boîte.</span><span class="sxs-lookup"><span data-stu-id="66f62-282">Check the **Draw Visual Meshes** box.</span></span>
  * <span data-ttu-id="66f62-283">Recherchez **dessiner un matériau** et cliquez sur le cercle sur la droite.</span><span class="sxs-lookup"><span data-stu-id="66f62-283">Locate **Draw Material** and click the circle on the right.</span></span> <span data-ttu-id="66f62-284">Type «**filaire**» dans le champ de recherche en haut.</span><span class="sxs-lookup"><span data-stu-id="66f62-284">Type "**wireframe**" into the search field at the top.</span></span> <span data-ttu-id="66f62-285">Cliquez sur le résultat, puis fermez la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="66f62-285">Click on the result and then close the window.</span></span> <span data-ttu-id="66f62-286">Lorsque vous effectuez cette opération, la valeur pour dessiner le matériel doit définition de maquette.</span><span class="sxs-lookup"><span data-stu-id="66f62-286">When you do this, the value for Draw Material should get set to Wireframe.</span></span>
* <span data-ttu-id="66f62-287">Exporter, générer et déployer l’application sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="66f62-287">Export, build and deploy the app to your HoloLens.</span></span>
* <span data-ttu-id="66f62-288">Lorsque l’application s’exécute, une maille filaire flux de travail superpose votre monde réel.</span><span class="sxs-lookup"><span data-stu-id="66f62-288">When the app runs, a wireframe mesh will overlay your real world.</span></span>
* <span data-ttu-id="66f62-289">Regardez comment une sphère propagée tombera hors de la scène et sur le sol !</span><span class="sxs-lookup"><span data-stu-id="66f62-289">Watch how a rolling sphere will fall off the stage, and onto the floor!</span></span>

<span data-ttu-id="66f62-290">Maintenant nous allons vous montrer comment déplacer la OrigamiCollection vers un nouvel emplacement :</span><span class="sxs-lookup"><span data-stu-id="66f62-290">Now we'll show you how to move the OrigamiCollection to a new location:</span></span>

* <span data-ttu-id="66f62-291">Dans le **Scripts** dossier, créez un script nommé **TapToPlaceParent**.</span><span class="sxs-lookup"><span data-stu-id="66f62-291">In the **Scripts** folder, create a script named **TapToPlaceParent**.</span></span>
* <span data-ttu-id="66f62-292">Dans le **hiérarchie**, développez le **OrigamiCollection** et sélectionnez le **étape** objet.</span><span class="sxs-lookup"><span data-stu-id="66f62-292">In the **Hierarchy**, expand the **OrigamiCollection** and select the **Stage** object.</span></span>
* <span data-ttu-id="66f62-293">Faites glisser le **TapToPlaceParent** script sur l’objet de la scène.</span><span class="sxs-lookup"><span data-stu-id="66f62-293">Drag the **TapToPlaceParent** script onto the Stage object.</span></span>
* <span data-ttu-id="66f62-294">Ouvrez le **TapToPlaceParent** de script dans Visual Studio et mettre à jour pour être ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="66f62-294">Open the **TapToPlaceParent** script in Visual Studio, and update it to be the following:</span></span>

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

* <span data-ttu-id="66f62-295">Exporter, créer et déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="66f62-295">Export, build and deploy the app.</span></span>
* <span data-ttu-id="66f62-296">Maintenant vous devez maintenant être en mesure de placer le jeu dans un emplacement spécifique par gazing à elle, à l’aide du mouvement sélectionnez Déplacer vers un nouvel emplacement et à l’aide du mouvement sélectionnez à nouveau.</span><span class="sxs-lookup"><span data-stu-id="66f62-296">Now you should now be able to place the game in a specific location by gazing at it, using the Select gesture and then moving to a new location, and using the Select gesture again.</span></span>

## <a name="chapter-7---holographic-fun"></a><span data-ttu-id="66f62-297">Chapitre 7 - fun HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="66f62-297">Chapter 7 - Holographic fun</span></span>

### <a name="objectives"></a><span data-ttu-id="66f62-298">Objectifs</span><span class="sxs-lookup"><span data-stu-id="66f62-298">Objectives</span></span>

* <span data-ttu-id="66f62-299">Faire apparaître l’entrée à un underworld HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="66f62-299">Reveal the entrance to a holographic underworld.</span></span>

### <a name="instructions"></a><span data-ttu-id="66f62-300">Instructions</span><span class="sxs-lookup"><span data-stu-id="66f62-300">Instructions</span></span>

<span data-ttu-id="66f62-301">Nous allons maintenant vous montrer comment découvrir l’underworld HOLOGRAPHIQUE :</span><span class="sxs-lookup"><span data-stu-id="66f62-301">Now we'll show you how to uncover the holographic underworld:</span></span>

* <span data-ttu-id="66f62-302">À partir de la **hologrammes** dossier dans le panneau de configuration de projet :</span><span class="sxs-lookup"><span data-stu-id="66f62-302">From the **Holograms** folder in the Project Panel:</span></span>
  * <span data-ttu-id="66f62-303">Faites glisser **Underworld** dans la hiérarchie soit un enfant de **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="66f62-303">Drag **Underworld** into the Hierarchy to be a child of **OrigamiCollection**.</span></span>
* <span data-ttu-id="66f62-304">Dans le **Scripts** dossier, créez un script nommé **HitTarget**.</span><span class="sxs-lookup"><span data-stu-id="66f62-304">In the **Scripts** folder, create a script named **HitTarget**.</span></span>
* <span data-ttu-id="66f62-305">Dans le **hiérarchie**, développez le **OrigamiCollection**.</span><span class="sxs-lookup"><span data-stu-id="66f62-305">In the **Hierarchy**, expand the **OrigamiCollection**.</span></span>
* <span data-ttu-id="66f62-306">Développez le **étape** de l’objet et sélectionnez le **cible** objet (ventilateur bleu).</span><span class="sxs-lookup"><span data-stu-id="66f62-306">Expand the **Stage** object and select the **Target** object (blue fan).</span></span>
* <span data-ttu-id="66f62-307">Faites glisser le **HitTarget** de script sur le **cible** objet.</span><span class="sxs-lookup"><span data-stu-id="66f62-307">Drag the **HitTarget** script onto the **Target** object.</span></span>
* <span data-ttu-id="66f62-308">Ouvrez le **HitTarget** de script dans Visual Studio et mettre à jour pour être ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="66f62-308">Open the **HitTarget** script in Visual Studio, and update it to be the following:</span></span>

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

* <span data-ttu-id="66f62-309">Dans Unity, sélectionnez le **cible** objet.</span><span class="sxs-lookup"><span data-stu-id="66f62-309">In Unity, select the **Target** object.</span></span>
* <span data-ttu-id="66f62-310">Deux propriétés publiques sont désormais visibles sur le **cible atteint** composant et vous devez référencer des objets dans notre scène :</span><span class="sxs-lookup"><span data-stu-id="66f62-310">Two public properties are now visible on the **Hit Target** component and need to reference objects in our scene:</span></span>
  * <span data-ttu-id="66f62-311">Faites glisser **Underworld** à partir de la **hiérarchie** panneau pour le **Underworld** propriété sur le **atteint la cible** composant.</span><span class="sxs-lookup"><span data-stu-id="66f62-311">Drag **Underworld** from the **Hierarchy** panel to the **Underworld** property on the **Hit Target** component.</span></span>
  * <span data-ttu-id="66f62-312">Faites glisser **étape** à partir de la **hiérarchie** panneau à la **objet à masquer** propriété sur le **atteint la cible** composant.</span><span class="sxs-lookup"><span data-stu-id="66f62-312">Drag **Stage** from the **Hierarchy** panel to the **Object to Hide** property on the **Hit Target** component.</span></span>
* <span data-ttu-id="66f62-313">Exporter, créer et déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="66f62-313">Export, build and deploy the app.</span></span>
* <span data-ttu-id="66f62-314">Placer la Collection d’Origami à l’étage et ensuite utiliser le mouvement Sélectionnez pour apporter une sphère à supprimer.</span><span class="sxs-lookup"><span data-stu-id="66f62-314">Place the Origami Collection on the floor, and then use the Select gesture to make a sphere drop.</span></span>
* <span data-ttu-id="66f62-315">Lors de la sphère atteint la cible (ventilateur blue), une explosion se produit.</span><span class="sxs-lookup"><span data-stu-id="66f62-315">When the sphere hits the target (blue fan), an explosion will occur.</span></span> <span data-ttu-id="66f62-316">La collection est masquée et une faille pour l’underworld s’affiche.</span><span class="sxs-lookup"><span data-stu-id="66f62-316">The collection will be hidden and a hole to the underworld will appear.</span></span>

## <a name="the-end"></a><span data-ttu-id="66f62-317">La fin</span><span class="sxs-lookup"><span data-stu-id="66f62-317">The end</span></span>

<span data-ttu-id="66f62-318">Et c’est la fin de ce didacticiel !</span><span class="sxs-lookup"><span data-stu-id="66f62-318">And that's the end of this tutorial!</span></span>

<span data-ttu-id="66f62-319">Vous avez appris :</span><span class="sxs-lookup"><span data-stu-id="66f62-319">You learned:</span></span>

* <span data-ttu-id="66f62-320">Comment créer une application HOLOGRAPHIQUE dans Unity.</span><span class="sxs-lookup"><span data-stu-id="66f62-320">How to create a holographic app in Unity.</span></span>
* <span data-ttu-id="66f62-321">Comment faire utiliser des regards, mouvement, voix, son et mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="66f62-321">How to make use of gaze, gesture, voice, sound, and spatial mapping.</span></span>
* <span data-ttu-id="66f62-322">Comment créer et déployer une application à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66f62-322">How to build and deploy an app using Visual Studio.</span></span>

<span data-ttu-id="66f62-323">Vous êtes maintenant prêt à commencer à créer votre propre expérience HOLOGRAPHIQUE !</span><span class="sxs-lookup"><span data-stu-id="66f62-323">You are now ready to start creating your own holographic experience!</span></span>

## <a name="see-also"></a><span data-ttu-id="66f62-324">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="66f62-324">See also</span></span>

* [<span data-ttu-id="66f62-325">Principes de base MR 101E : Projet complet avec l’émulateur</span><span class="sxs-lookup"><span data-stu-id="66f62-325">MR Basics 101E: Complete project with emulator</span></span>](holograms-101e.md)
* [<span data-ttu-id="66f62-326">Gaze</span><span class="sxs-lookup"><span data-stu-id="66f62-326">Gaze</span></span>](gaze.md)
* [<span data-ttu-id="66f62-327">Mouvements</span><span class="sxs-lookup"><span data-stu-id="66f62-327">Gestures</span></span>](gestures.md)
* [<span data-ttu-id="66f62-328">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="66f62-328">Voice input</span></span>](voice-input.md)
* [<span data-ttu-id="66f62-329">Son spatial</span><span class="sxs-lookup"><span data-stu-id="66f62-329">Spatial sound</span></span>](spatial-sound.md)
* [<span data-ttu-id="66f62-330">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="66f62-330">Spatial mapping</span></span>](spatial-mapping.md)
