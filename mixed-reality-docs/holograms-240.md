---
title: MR partage 240 - plusieurs appareils HoloLens
description: Suivez cette procédure pas à pas à l’aide de Unity, Visual Studio et HoloLens pour connaître les détails du partage hologrammes de codage.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, sharing, networking, academy, tutorial
ms.openlocfilehash: 70a39a739d360a5032bc8df76b6f0bd57521d9ec
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594888"
---
>[!NOTE]
><span data-ttu-id="9cf68-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="9cf68-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="9cf68-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="9cf68-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="9cf68-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="9cf68-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="9cf68-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9cf68-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="9cf68-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="9cf68-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="9cf68-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="9cf68-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-sharing-240-multiple-hololens-devices"></a><span data-ttu-id="9cf68-110">MR 240 de partage : Plusieurs appareils HoloLens</span><span class="sxs-lookup"><span data-stu-id="9cf68-110">MR Sharing 240: Multiple HoloLens devices</span></span>

<span data-ttu-id="9cf68-111">Hologrammes reçoivent présence dans notre monde par reste en place lorsque nous transférerons dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="9cf68-111">Holograms are given presence in our world by remaining in place as we move about in space.</span></span> <span data-ttu-id="9cf68-112">HoloLens conserve hologrammes en place à l’aide de divers [systèmes de coordonnées](coordinate-systems.md) pour effectuer le suivi de l’emplacement et l’orientation des objets.</span><span class="sxs-lookup"><span data-stu-id="9cf68-112">HoloLens keeps holograms in place by using various [coordinate systems](coordinate-systems.md) to keep track of the location and orientation of objects.</span></span> <span data-ttu-id="9cf68-113">Lorsque nous partageons ces systèmes de coordonnées entre les appareils, nous pouvons créer une expérience partagée qui permet de prendre part à un monde HOLOGRAPHIQUE partagé.</span><span class="sxs-lookup"><span data-stu-id="9cf68-113">When we share these coordinate systems between devices, we can create a shared experience that allows us to take part in a shared holographic world.</span></span>

<span data-ttu-id="9cf68-114">Dans ce didacticiel, nous allons :</span><span class="sxs-lookup"><span data-stu-id="9cf68-114">In this tutorial, we will:</span></span>

* <span data-ttu-id="9cf68-115">Configuration d’un réseau pour une expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="9cf68-115">Setup a network for a shared experience.</span></span>
* <span data-ttu-id="9cf68-116">Partager hologrammes entre les appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9cf68-116">Share holograms across HoloLens devices.</span></span>
* <span data-ttu-id="9cf68-117">Découvrir d’autres personnes de notre monde HOLOGRAPHIQUE partagé.</span><span class="sxs-lookup"><span data-stu-id="9cf68-117">Discover other people in our shared holographic world.</span></span>
* <span data-ttu-id="9cf68-118">Créer une expérience interactive partagée où vous pouvez cibler d’autres joueurs - et lancer des projectiles sur leur !</span><span class="sxs-lookup"><span data-stu-id="9cf68-118">Create a shared interactive experience where you can target other players - and launch projectiles at them!</span></span>

## <a name="device-support"></a><span data-ttu-id="9cf68-119">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="9cf68-119">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="9cf68-120">Cours</span><span class="sxs-lookup"><span data-stu-id="9cf68-120">Course</span></span></th><th style="width:150px"> <span data-ttu-id="9cf68-121"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="9cf68-121"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="9cf68-122"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="9cf68-122"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="9cf68-123">MR 240 de partage : Plusieurs appareils HoloLens</span><span class="sxs-lookup"><span data-stu-id="9cf68-123">MR Sharing 240: Multiple HoloLens devices</span></span></td><td style="text-align: center;"> <span data-ttu-id="9cf68-124">✔️</span><span class="sxs-lookup"><span data-stu-id="9cf68-124">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="9cf68-125">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9cf68-125">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9cf68-126">Prérequis</span><span class="sxs-lookup"><span data-stu-id="9cf68-126">Prerequisites</span></span>

* <span data-ttu-id="9cf68-127">Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md) avec accès à Internet.</span><span class="sxs-lookup"><span data-stu-id="9cf68-127">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md) with Internet access.</span></span>
* <span data-ttu-id="9cf68-128">Au moins deux appareils HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="9cf68-128">At least two HoloLens devices [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="9cf68-129">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="9cf68-129">Project files</span></span>

* <span data-ttu-id="9cf68-130">Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-240-SharedHolograms.zip) requise par le projet.</span><span class="sxs-lookup"><span data-stu-id="9cf68-130">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-240-SharedHolograms.zip) required by the project.</span></span> <span data-ttu-id="9cf68-131">Nécessite Unity 2017.2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="9cf68-131">Requires Unity 2017.2 or later.</span></span>
  * <span data-ttu-id="9cf68-132">Si vous avez besoin de prise en charge de Unity 5.6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-240.zip).</span><span class="sxs-lookup"><span data-stu-id="9cf68-132">If you still need Unity 5.6 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-240.zip).</span></span>
  * <span data-ttu-id="9cf68-133">Si vous avez besoin de prise en charge de Unity 5.5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-240.zip).</span><span class="sxs-lookup"><span data-stu-id="9cf68-133">If you still need Unity 5.5 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-240.zip).</span></span>
  * <span data-ttu-id="9cf68-134">Si vous avez besoin de prise en charge de Unity 5.4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-240.zip).</span><span class="sxs-lookup"><span data-stu-id="9cf68-134">If you still need Unity 5.4 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-240.zip).</span></span>
* <span data-ttu-id="9cf68-135">Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="9cf68-135">Un-archive the files to your desktop or other easy to reach location.</span></span> <span data-ttu-id="9cf68-136">Conservez le nom de dossier en tant que **SharedHolograms**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-136">Keep the folder name as **SharedHolograms**.</span></span>

>[!NOTE]
><span data-ttu-id="9cf68-137">Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-240-SharedHolograms).</span><span class="sxs-lookup"><span data-stu-id="9cf68-137">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-240-SharedHolograms).</span></span>

## <a name="chapter-1---holo-world"></a><span data-ttu-id="9cf68-138">Chapitre 1 - Holo World</span><span class="sxs-lookup"><span data-stu-id="9cf68-138">Chapter 1 - Holo World</span></span>

>[!VIDEO https://www.youtube.com/embed/c7qHYYW8rxQ]

<span data-ttu-id="9cf68-139">Dans ce chapitre, nous le programme d’installation de notre premier projet Unity et les étapes à la build et processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9cf68-139">In this chapter, we'll setup our first Unity project and step through the build and deploy process.</span></span>

### <a name="objectives"></a><span data-ttu-id="9cf68-140">Objectifs</span><span class="sxs-lookup"><span data-stu-id="9cf68-140">Objectives</span></span>

* <span data-ttu-id="9cf68-141">Le programme d’installation Unity pour développer des applications HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="9cf68-141">Setup Unity to develop holographic apps.</span></span>
* <span data-ttu-id="9cf68-142">Consultez votre HOLOGRAMME !</span><span class="sxs-lookup"><span data-stu-id="9cf68-142">See your hologram!</span></span>

### <a name="instructions"></a><span data-ttu-id="9cf68-143">Instructions</span><span class="sxs-lookup"><span data-stu-id="9cf68-143">Instructions</span></span>

* <span data-ttu-id="9cf68-144">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="9cf68-144">Start Unity.</span></span>
* <span data-ttu-id="9cf68-145">Sélectionnez **Open**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-145">Select **Open**.</span></span>
* <span data-ttu-id="9cf68-146">Entrez l’emplacement que le **SharedHolograms** dossier vous non précédemment archivé.</span><span class="sxs-lookup"><span data-stu-id="9cf68-146">Enter location as the **SharedHolograms** folder you previously unarchived.</span></span>
* <span data-ttu-id="9cf68-147">Sélectionnez **nom_projet** et cliquez sur **sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-147">Select **Project Name** and click **Select Folder**.</span></span>
* <span data-ttu-id="9cf68-148">Dans le **hiérarchie**, avec le bouton droit le **Main Camera** et sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-148">In the **Hierarchy**, right-click the **Main Camera** and select **Delete**.</span></span>
* <span data-ttu-id="9cf68-149">Dans le **HoloToolkit partage-240/Prefabs/caméra** dossier, recherchez le **Main Camera** prefab.</span><span class="sxs-lookup"><span data-stu-id="9cf68-149">In the **HoloToolkit-Sharing-240/Prefabs/Camera** folder, find the **Main Camera** prefab.</span></span>
* <span data-ttu-id="9cf68-150">Faites glisser et déposez le **Main Camera** dans le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-150">Drag and drop the **Main Camera** into the **Hierarchy**.</span></span>
* <span data-ttu-id="9cf68-151">Dans le **hiérarchie**, cliquez sur **créer** et **créer vide**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-151">In the **Hierarchy**, click on **Create** and **Create Empty**.</span></span>
* <span data-ttu-id="9cf68-152">Cliquez sur le nouveau **GameObject** et sélectionnez **renommer**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-152">Right-click the new **GameObject** and select **Rename**.</span></span>
* <span data-ttu-id="9cf68-153">Renommer le GameObject à **HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-153">Rename the GameObject to **HologramCollection**.</span></span>
* <span data-ttu-id="9cf68-154">Sélectionnez le **HologramCollection** de l’objet dans le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-154">Select the **HologramCollection** object in the **Hierarchy**.</span></span>
* <span data-ttu-id="9cf68-155">Dans le **inspecteur** définir le **transformer position** à : **X : 0, Y : -0,25, Z : 2**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-155">In the **Inspector** set the **transform position** to: **X: 0, Y: -0.25, Z: 2**.</span></span>
* <span data-ttu-id="9cf68-156">Dans le **Vntana** dossier dans le **panneau projet**, trouver la **EnergyHub** asset.</span><span class="sxs-lookup"><span data-stu-id="9cf68-156">In the **Holograms** folder in the **Project panel**, find the **EnergyHub** asset.</span></span>
* <span data-ttu-id="9cf68-157">Faites glisser et déposez le **EnergyHub** à partir de l’objet le **panneau projet** à la **hiérarchie** en tant qu’un **enfant de HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-157">Drag and drop the **EnergyHub** object from the **Project panel** to the **Hierarchy** as a **child of HologramCollection**.</span></span>
* <span data-ttu-id="9cf68-158">Sélectionnez **fichier > Enregistrer la scène sous...**</span><span class="sxs-lookup"><span data-stu-id="9cf68-158">Select **File > Save Scene As...**</span></span>
* <span data-ttu-id="9cf68-159">Nommez la scène **SharedHolograms** et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-159">Name the scene **SharedHolograms** and click **Save**.</span></span>
* <span data-ttu-id="9cf68-160">Appuyez sur la **lire** bouton dans Unity pour afficher un aperçu votre hologrammes.</span><span class="sxs-lookup"><span data-stu-id="9cf68-160">Press the **Play** button in Unity to preview your holograms.</span></span>
* <span data-ttu-id="9cf68-161">Appuyez sur **lire** une deuxième fois pour arrêter le mode d’aperçu.</span><span class="sxs-lookup"><span data-stu-id="9cf68-161">Press **Play** a second time to stop preview mode.</span></span>

<span data-ttu-id="9cf68-162">**Exportez le projet à partir d’Unity pour Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="9cf68-162">**Export the project from Unity to Visual Studio**</span></span>
* <span data-ttu-id="9cf68-163">Dans, sélectionnez Unity **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-163">In Unity select **File > Build Settings**.</span></span>
* <span data-ttu-id="9cf68-164">Cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="9cf68-164">Click **Add Open Scenes** to add the scene.</span></span>
* <span data-ttu-id="9cf68-165">Sélectionnez **plateforme Windows universelle** dans le **plateforme** liste et cliquez sur **plateforme de commutation**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-165">Select **Universal Windows Platform** in the **Platform** list and click **Switch Platform**.</span></span>
* <span data-ttu-id="9cf68-166">Définissez **SDK** à **10 universelle**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-166">Set **SDK** to **Universal 10**.</span></span>
* <span data-ttu-id="9cf68-167">Définissez **appareil cible** à **HoloLens** et **Type de Build UWP** à **D3D**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-167">Set **Target device** to **HoloLens** and **UWP Build Type** to **D3D**.</span></span>
* <span data-ttu-id="9cf68-168">Vérifiez **Unity C# projets**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-168">Check **Unity C# Projects**.</span></span>
* <span data-ttu-id="9cf68-169">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-169">Click **Build**.</span></span>
* <span data-ttu-id="9cf68-170">Dans la fenêtre Explorateur de fichiers qui s’affiche, créez un **nouveau dossier** nommé « Application ».</span><span class="sxs-lookup"><span data-stu-id="9cf68-170">In the file explorer window that appears, create a **New Folder** named "App".</span></span>
* <span data-ttu-id="9cf68-171">Clic le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="9cf68-171">Single click the **App** folder.</span></span>
* <span data-ttu-id="9cf68-172">Appuyez sur **sélectionnez dossier**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-172">Press **Select Folder**.</span></span>
* <span data-ttu-id="9cf68-173">Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9cf68-173">When Unity is done, a File Explorer window will appear.</span></span>
* <span data-ttu-id="9cf68-174">Ouvrez le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="9cf68-174">Open the **App** folder.</span></span>
* <span data-ttu-id="9cf68-175">Ouvrez **SharedHolograms.sln** pour lancer Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9cf68-175">Open **SharedHolograms.sln** to launch Visual Studio.</span></span>
* <span data-ttu-id="9cf68-176">À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **X86**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-176">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **X86**.</span></span>
* <span data-ttu-id="9cf68-177">Cliquez sur la flèche déroulante en regard de l’ordinateur Local, puis sélectionnez **périphérique distant**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-177">Click on the drop-down arrow next to Local Machine, and select **Remote Device**.</span></span>
    * <span data-ttu-id="9cf68-178">Définir le **adresse** au nom ou adresse IP de votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9cf68-178">Set the **Address** to the name or IP address of your HoloLens.</span></span> <span data-ttu-id="9cf68-179">Si vous ne connaissez pas votre adresse IP du périphérique, recherchez dans **Paramètres > réseau & Internet > Options avancées** ou demandez à Cortana **« Hey Cortana, quelle est mon adresse IP ? »**</span><span class="sxs-lookup"><span data-stu-id="9cf68-179">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options** or ask Cortana **"Hey Cortana, What's my IP address?"**</span></span>
    * <span data-ttu-id="9cf68-180">Laissez le **Mode d’authentification** définie sur **universelle**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-180">Leave the **Authentication Mode** set to **Universal**.</span></span>
    * <span data-ttu-id="9cf68-181">Cliquez sur **sélectionnez**</span><span class="sxs-lookup"><span data-stu-id="9cf68-181">Click **Select**</span></span>
* <span data-ttu-id="9cf68-182">Cliquez sur **Déboguer > Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-182">Click **Debug > Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="9cf68-183">S’il s’agit de la première fois le déploiement sur votre périphérique, vous devrez [Couplez-le Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span><span class="sxs-lookup"><span data-stu-id="9cf68-183">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span></span>
* <span data-ttu-id="9cf68-184">Placez sur votre HoloLens et trouver l’hologramme EnergyHub.</span><span class="sxs-lookup"><span data-stu-id="9cf68-184">Put on your HoloLens and find the EnergyHub hologram.</span></span>

## <a name="chapter-2---interaction"></a><span data-ttu-id="9cf68-185">Chapitre 2 - Interaction</span><span class="sxs-lookup"><span data-stu-id="9cf68-185">Chapter 2 - Interaction</span></span>

>[!VIDEO https://www.youtube.com/embed/W60xG15a8gc]

<span data-ttu-id="9cf68-186">Dans ce chapitre, nous permettra d’interagir avec notre hologrammes.</span><span class="sxs-lookup"><span data-stu-id="9cf68-186">In this chapter, we'll interact with our holograms.</span></span> <span data-ttu-id="9cf68-187">Tout d’abord, nous allons ajouter un curseur pour visualiser notre [les regards](gaze.md).</span><span class="sxs-lookup"><span data-stu-id="9cf68-187">First, we'll add a cursor to visualize our [Gaze](gaze.md).</span></span> <span data-ttu-id="9cf68-188">Ensuite, nous allons ajouter [mouvements](gestures.md) et utiliser notre main placer notre hologrammes dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="9cf68-188">Then, we'll add [Gestures](gestures.md) and use our hand to place our holograms in space.</span></span>

### <a name="objectives"></a><span data-ttu-id="9cf68-189">Objectifs</span><span class="sxs-lookup"><span data-stu-id="9cf68-189">Objectives</span></span>

* <span data-ttu-id="9cf68-190">Utilisez les regards d’entrée pour contrôler un curseur.</span><span class="sxs-lookup"><span data-stu-id="9cf68-190">Use gaze input to control a cursor.</span></span>
* <span data-ttu-id="9cf68-191">Utiliser le mouvement d’entrée pour interagir avec hologrammes.</span><span class="sxs-lookup"><span data-stu-id="9cf68-191">Use gesture input to interact with holograms.</span></span>

### <a name="instructions"></a><span data-ttu-id="9cf68-192">Instructions</span><span class="sxs-lookup"><span data-stu-id="9cf68-192">Instructions</span></span>

<span data-ttu-id="9cf68-193">**Gaze**</span><span class="sxs-lookup"><span data-stu-id="9cf68-193">**Gaze**</span></span>
* <span data-ttu-id="9cf68-194">Dans le **Panneau de la hiérarchie** sélectionner le **HologramCollection** objet.</span><span class="sxs-lookup"><span data-stu-id="9cf68-194">In the **Hierarchy panel** select the **HologramCollection** object.</span></span>
* <span data-ttu-id="9cf68-195">Dans le **panneau Inspecteur** cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="9cf68-195">In the **Inspector panel** click the **Add Component** button.</span></span>
* <span data-ttu-id="9cf68-196">Dans le menu, tapez dans la zone de recherche **Manager les regards**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-196">In the menu, type in the search box **Gaze Manager**.</span></span> <span data-ttu-id="9cf68-197">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="9cf68-197">Select the search result.</span></span>
* <span data-ttu-id="9cf68-198">Dans le **HoloToolkit partage 240\Prefabs\Input** dossier, recherchez le **curseur** asset.</span><span class="sxs-lookup"><span data-stu-id="9cf68-198">In the **HoloToolkit-Sharing-240\Prefabs\Input** folder, find the **Cursor** asset.</span></span>
* <span data-ttu-id="9cf68-199">Faites glisser et déposez le **curseur** actif sur le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-199">Drag and drop the **Cursor** asset onto the **Hierarchy**.</span></span>

<span data-ttu-id="9cf68-200">**Mouvement**</span><span class="sxs-lookup"><span data-stu-id="9cf68-200">**Gesture**</span></span>
* <span data-ttu-id="9cf68-201">Dans le **Panneau de la hiérarchie** sélectionner le **HologramCollection** objet.</span><span class="sxs-lookup"><span data-stu-id="9cf68-201">In the **Hierarchy panel** select the **HologramCollection** object.</span></span>
* <span data-ttu-id="9cf68-202">Cliquez sur **ajouter un composant** et type **Gestionnaire de mouvements** dans le champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="9cf68-202">Click **Add Component** and type **Gesture Manager** in the search field.</span></span> <span data-ttu-id="9cf68-203">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="9cf68-203">Select the search result.</span></span>
* <span data-ttu-id="9cf68-204">Dans le **Panneau de la hiérarchie**, développez **HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-204">In the **Hierarchy panel**, expand **HologramCollection**.</span></span>
* <span data-ttu-id="9cf68-205">Sélectionnez l’enfant **EnergyHub** objet.</span><span class="sxs-lookup"><span data-stu-id="9cf68-205">Select the child **EnergyHub** object.</span></span>
* <span data-ttu-id="9cf68-206">Dans le **panneau Inspecteur** cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="9cf68-206">In the **Inspector panel** click the **Add Component** button.</span></span>
* <span data-ttu-id="9cf68-207">Dans le menu, tapez dans la zone de recherche **hologramme Placement**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-207">In the menu, type in the search box **Hologram Placement**.</span></span> <span data-ttu-id="9cf68-208">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="9cf68-208">Select the search result.</span></span>
* <span data-ttu-id="9cf68-209">Enregistrer la scène en sélectionnant **fichier > Enregistrer la scène**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-209">Save the scene by selecting **File > Save Scene**.</span></span>

<span data-ttu-id="9cf68-210">**Déployer et profitez de**</span><span class="sxs-lookup"><span data-stu-id="9cf68-210">**Deploy and enjoy**</span></span>
* <span data-ttu-id="9cf68-211">Créer et déployer dans votre HoloLens, en suivant les instructions du chapitre précédent.</span><span class="sxs-lookup"><span data-stu-id="9cf68-211">Build and deploy to your HoloLens, using the instructions from the previous chapter.</span></span>
* <span data-ttu-id="9cf68-212">Une fois que l’application démarre sur votre HoloLens, déplacer votre tête et notez comment le EnergyHub suit votre regard.</span><span class="sxs-lookup"><span data-stu-id="9cf68-212">Once the app launches on your HoloLens, move your head around and notice how the EnergyHub follows your gaze.</span></span>
* <span data-ttu-id="9cf68-213">Remarquez que le curseur s’affiche lorsque vous remplacez l’hologramme et devient une lumière point lorsque ne gazing pas à un hologramme.</span><span class="sxs-lookup"><span data-stu-id="9cf68-213">Notice how the cursor appears when you gaze upon the hologram, and changes to a point light when not gazing at a hologram.</span></span>
* <span data-ttu-id="9cf68-214">Effectuer un appui pour placer l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="9cf68-214">Perform an air-tap to place the hologram.</span></span> <span data-ttu-id="9cf68-215">À ce stade dans notre projet, vous pouvez uniquement placer une fois l’hologramme (redéploiement pour essayer à nouveau).</span><span class="sxs-lookup"><span data-stu-id="9cf68-215">At this time in our project, you can only place the hologram once (redeploy to try again).</span></span>

## <a name="chapter-3---shared-coordinates"></a><span data-ttu-id="9cf68-216">Chapitre 3 - partagé coordonne</span><span class="sxs-lookup"><span data-stu-id="9cf68-216">Chapter 3 - Shared Coordinates</span></span>

>[!VIDEO https://www.youtube.com/embed/Ey8yBgWiqtg]

<span data-ttu-id="9cf68-217">Il est amusant de voir et interagir avec hologrammes, mais allons plus loin.</span><span class="sxs-lookup"><span data-stu-id="9cf68-217">It's fun to see and interact with holograms, but let's go further.</span></span> <span data-ttu-id="9cf68-218">Nous allons configurer notre première expérience partagé - un hologramme tout le monde peut voir ensemble.</span><span class="sxs-lookup"><span data-stu-id="9cf68-218">We'll set up our first shared experience - a hologram everyone can see together.</span></span>

### <a name="objectives"></a><span data-ttu-id="9cf68-219">Objectifs</span><span class="sxs-lookup"><span data-stu-id="9cf68-219">Objectives</span></span>

* <span data-ttu-id="9cf68-220">Configuration d’un réseau pour une expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="9cf68-220">Setup a network for a shared experience.</span></span>
* <span data-ttu-id="9cf68-221">Établir un point de référence commun.</span><span class="sxs-lookup"><span data-stu-id="9cf68-221">Establish a common reference point.</span></span>
* <span data-ttu-id="9cf68-222">Partager des systèmes de coordonnées entre les appareils.</span><span class="sxs-lookup"><span data-stu-id="9cf68-222">Share coordinate systems across devices.</span></span>
* <span data-ttu-id="9cf68-223">Tout le monde voit le même HOLOGRAMME !</span><span class="sxs-lookup"><span data-stu-id="9cf68-223">Everyone sees the same hologram!</span></span>

>[!NOTE]
><span data-ttu-id="9cf68-224">Le **InternetClientServer** et **PrivateNetworkClientServer** fonctionnalités doivent être déclarées pour une application à se connecter au serveur partage.</span><span class="sxs-lookup"><span data-stu-id="9cf68-224">The **InternetClientServer** and **PrivateNetworkClientServer** capabilities must be declared for an app to connect to the sharing server.</span></span> <span data-ttu-id="9cf68-225">Cela est fait pour vous déjà dans hologrammes 240, mais gardez cela à l’esprit pour vos propres projets.</span><span class="sxs-lookup"><span data-stu-id="9cf68-225">This is done for you already in Holograms 240, but keep this in mind for your own projects.</span></span>
>1. <span data-ttu-id="9cf68-226">Dans l’éditeur Unity, accédez aux paramètres player en accédant à « Modifier > projet Paramètres > Player »</span><span class="sxs-lookup"><span data-stu-id="9cf68-226">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player"</span></span>
>2. <span data-ttu-id="9cf68-227">Cliquez sur l’onglet « Windows Store »</span><span class="sxs-lookup"><span data-stu-id="9cf68-227">Click on the "Windows Store" tab</span></span>
>3. <span data-ttu-id="9cf68-228">Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **InternetClientServer** fonctionnalité et la **PrivateNetworkClientServer** fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="9cf68-228">In the "Publishing Settings > Capabilities" section, check the **InternetClientServer** capability and the **PrivateNetworkClientServer** capability</span></span>

### <a name="instructions"></a><span data-ttu-id="9cf68-229">Instructions</span><span class="sxs-lookup"><span data-stu-id="9cf68-229">Instructions</span></span>

* <span data-ttu-id="9cf68-230">Dans le **panneau projet** accédez à la **HoloToolkit partage 240\Prefabs\Sharing** dossier.</span><span class="sxs-lookup"><span data-stu-id="9cf68-230">In the **Project panel** navigate to the **HoloToolkit-Sharing-240\Prefabs\Sharing** folder.</span></span>
* <span data-ttu-id="9cf68-231">Faites glisser et déposez le **partage** prefab dans le **Panneau de la hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-231">Drag and drop the **Sharing** prefab into the **Hierarchy panel**.</span></span>

<span data-ttu-id="9cf68-232">Nous devons ensuite lancer le service de partage.</span><span class="sxs-lookup"><span data-stu-id="9cf68-232">Next we need to launch the sharing service.</span></span> <span data-ttu-id="9cf68-233">Uniquement **un PC** dans le partage rencontrer les besoins d’effectuer cette étape.</span><span class="sxs-lookup"><span data-stu-id="9cf68-233">Only **one PC** in the shared experience needs to do this step.</span></span>
* <span data-ttu-id="9cf68-234">Dans Unity - dans le menu en haut la main, sélectionnez le **HoloToolkit partage 240 menu**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-234">In Unity - in the top-hand menu - select the **HoloToolkit-Sharing-240 menu**.</span></span>
* <span data-ttu-id="9cf68-235">Sélectionnez le **lancer le Service de partage** élément dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="9cf68-235">Select the **Launch Sharing Service** item in the drop-down.</span></span>
* <span data-ttu-id="9cf68-236">Vérifier le **réseau privé** , cliquez sur **autoriser l’accès** lorsque l’invite de pare-feu s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9cf68-236">Check the **Private Network** option and click **Allow Access** when the firewall prompt appears.</span></span>
* <span data-ttu-id="9cf68-237">Notez l’adresse IPv4 affichée dans la fenêtre de console de Service de partage.</span><span class="sxs-lookup"><span data-stu-id="9cf68-237">Note down the IPv4 address displayed in the Sharing Service console window.</span></span> <span data-ttu-id="9cf68-238">Il s’agit de la même adresse IP que l’ordinateur qu'est en cours d’exécution sur le service.</span><span class="sxs-lookup"><span data-stu-id="9cf68-238">This is the same IP as the machine the service is being run on.</span></span>

<span data-ttu-id="9cf68-239">Suivez le reste des instructions **tous les PC** qui joindra l’expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="9cf68-239">Follow the rest of the instructions on **all PCs** that will join the shared experience.</span></span>
* <span data-ttu-id="9cf68-240">Dans le **hiérarchie**, sélectionnez le **partage** objet.</span><span class="sxs-lookup"><span data-stu-id="9cf68-240">In the **Hierarchy**, select the **Sharing** object.</span></span>
* <span data-ttu-id="9cf68-241">Dans le **inspecteur**, dans le **étape partage** composant, modifier le **adresse du serveur** à partir de « localhost » à l’adresse IPv4 de l’ordinateur en cours d’exécution SharingService.exe.</span><span class="sxs-lookup"><span data-stu-id="9cf68-241">In the **Inspector**, on the **Sharing Stage** component, change the **Server Address** from 'localhost' to the IPv4 address of the machine running SharingService.exe.</span></span>
* <span data-ttu-id="9cf68-242">Dans le **hiérarchie** sélectionner le **HologramCollection** objet.</span><span class="sxs-lookup"><span data-stu-id="9cf68-242">In the **Hierarchy** select the **HologramCollection** object.</span></span>
* <span data-ttu-id="9cf68-243">Dans le **inspecteur** cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="9cf68-243">In the **Inspector** click the **Add Component** button.</span></span>
* <span data-ttu-id="9cf68-244">Dans la zone de recherche, tapez **importer exporter d’ancrage Manager**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-244">In the search box, type **Import Export Anchor Manager**.</span></span> <span data-ttu-id="9cf68-245">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="9cf68-245">Select the search result.</span></span>
* <span data-ttu-id="9cf68-246">Dans le **panneau projet** accédez à la **Scripts** dossier.</span><span class="sxs-lookup"><span data-stu-id="9cf68-246">In the **Project panel** navigate to the **Scripts** folder.</span></span>
* <span data-ttu-id="9cf68-247">Double-cliquez sur le **HologramPlacement** script pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9cf68-247">Double-click the **HologramPlacement** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="9cf68-248">Remplacez le contenu par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9cf68-248">Replace the contents with the code below.</span></span>

```cs
using UnityEngine;
using System.Collections.Generic;
using UnityEngine.Windows.Speech;
using Academy.HoloToolkit.Unity;
using Academy.HoloToolkit.Sharing;

public class HologramPlacement : Singleton<HologramPlacement>
{
    /// <summary>
    /// Tracks if we have been sent a transform for the anchor model.
    /// The anchor model is rendered relative to the actual anchor.
    /// </summary>
    public bool GotTransform { get; private set; }

    private bool animationPlayed = false;

    void Start()
    {
        // We care about getting updates for the anchor transform.
        CustomMessages.Instance.MessageHandlers[CustomMessages.TestMessageID.StageTransform] = this.OnStageTransform;

        // And when a new user join we will send the anchor transform we have.
        SharingSessionTracker.Instance.SessionJoined += Instance_SessionJoined;
    }

    /// <summary>
    /// When a new user joins we want to send them the relative transform for the anchor if we have it.
    /// </summary>
    /// <param name="sender"></param>
    /// <param name="e"></param>
    private void Instance_SessionJoined(object sender, SharingSessionTracker.SessionJoinedEventArgs e)
    {
        if (GotTransform)
        {
            CustomMessages.Instance.SendStageTransform(transform.localPosition, transform.localRotation);
        }
    }

    void Update()
    {
        if (GotTransform)
        {
            if (ImportExportAnchorManager.Instance.AnchorEstablished &&
                animationPlayed == false)
            {
                // This triggers the animation sequence for the anchor model and 
                // puts the cool materials on the model.
                GetComponent<EnergyHubBase>().SendMessage("OnSelect");
                animationPlayed = true;
            }
        }
        else
        {
            transform.position = Vector3.Lerp(transform.position, ProposeTransformPosition(), 0.2f);
        }
    }

    Vector3 ProposeTransformPosition()
    {
        // Put the anchor 2m in front of the user.
        Vector3 retval = Camera.main.transform.position + Camera.main.transform.forward * 2;

        return retval;
    }

    public void OnSelect()
    {
        // Note that we have a transform.
        GotTransform = true;
        
        // And send it to our friends.
        CustomMessages.Instance.SendStageTransform(transform.localPosition, transform.localRotation);
    }

    /// <summary>
    /// When a remote system has a transform for us, we'll get it here.
    /// </summary>
    /// <param name="msg"></param>
    void OnStageTransform(NetworkInMessage msg)
    {
        // We read the user ID but we don't use it here.
        msg.ReadInt64();

        transform.localPosition = CustomMessages.Instance.ReadVector3(msg);
        transform.localRotation = CustomMessages.Instance.ReadQuaternion(msg);

        // The first time, we'll want to send the message to the anchor to do its animation and
        // swap its materials.
        if (GotTransform == false)
        {
            GetComponent<EnergyHubBase>().SendMessage("OnSelect");
        }

        GotTransform = true;
    }

    public void ResetStage()
    {
        // We'll use this later.
    }
}
```

* <span data-ttu-id="9cf68-249">Dans Unity, sélectionnez le **HologramCollection** dans le **Panneau de la hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-249">Back in Unity, select the **HologramCollection** in the **Hierarchy panel**.</span></span>
* <span data-ttu-id="9cf68-250">Dans le **panneau Inspecteur** cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="9cf68-250">In the **Inspector panel** click the **Add Component** button.</span></span>
* <span data-ttu-id="9cf68-251">Dans le menu, tapez dans la zone de recherche **Gestionnaire d’état application**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-251">In the menu, type in the search box **App State Manager**.</span></span> <span data-ttu-id="9cf68-252">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="9cf68-252">Select the search result.</span></span>

<span data-ttu-id="9cf68-253">**Déployer et profitez de**</span><span class="sxs-lookup"><span data-stu-id="9cf68-253">**Deploy and enjoy**</span></span>
* <span data-ttu-id="9cf68-254">Générez le projet pour vos appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9cf68-254">Build the project for your HoloLens devices.</span></span>
* <span data-ttu-id="9cf68-255">Désigner un HoloLens à déployer en premier.</span><span class="sxs-lookup"><span data-stu-id="9cf68-255">Designate one HoloLens to deploy to first.</span></span> <span data-ttu-id="9cf68-256">Vous devez attendre que le point d’ancrage être téléchargé vers le service avant de pouvoir placer le EnergyHub (cette opération peut prendre environ 30 à 60 secondes).</span><span class="sxs-lookup"><span data-stu-id="9cf68-256">You will need to wait for the Anchor to be uploaded to the service before you can place the EnergyHub (this can take ~30-60 seconds).</span></span> <span data-ttu-id="9cf68-257">Jusqu'à ce que le téléchargement est terminé, votre mouvements tap seront ignorés.</span><span class="sxs-lookup"><span data-stu-id="9cf68-257">Until the upload is done, your tap gestures will be ignored.</span></span>
* <span data-ttu-id="9cf68-258">Une fois le EnergyHub a été placé, son emplacement sera téléchargé vers le service et vous pouvez ensuite déployer sur tous les autres appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9cf68-258">After the EnergyHub has been placed, its location will be uploaded to the service and you can then deploy to all other HoloLens devices.</span></span>
* <span data-ttu-id="9cf68-259">Lorsqu’un nouveau HoloLens joint tout d’abord la session, l’emplacement de la EnergyHub n’est peut-être pas correct sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="9cf68-259">When a new HoloLens first joins the session, the location of the EnergyHub may not be correct on that device.</span></span> <span data-ttu-id="9cf68-260">Toutefois, dès que l’ancre et les emplacements de EnergyHub ont été téléchargées à partir du service, le EnergyHub doit accéder à l’emplacement partagé, de nouveau.</span><span class="sxs-lookup"><span data-stu-id="9cf68-260">However, as soon as the anchor and EnergyHub locations have been downloaded from the service, the EnergyHub should jump to the new, shared location.</span></span> <span data-ttu-id="9cf68-261">Si cela n’arrive pas dans environ 30 à 60 secondes, remonter où le HoloLens d’origine était lorsque vous définissez le point d’ancrage pour recueillir plusieurs indices d’environnement.</span><span class="sxs-lookup"><span data-stu-id="9cf68-261">If this does not happen within ~30-60 seconds, walk to where the original HoloLens was when setting the anchor to gather more environment clues.</span></span> <span data-ttu-id="9cf68-262">Si l’emplacement ne verrouille pas toujours redéployer, à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="9cf68-262">If the location still does not lock on, redeploy to the device.</span></span>
* <span data-ttu-id="9cf68-263">Lorsque les appareils sont prêts et exécution de l’application, recherchez le EnergyHub.</span><span class="sxs-lookup"><span data-stu-id="9cf68-263">When the devices are all ready and running the app, look for the EnergyHub.</span></span> <span data-ttu-id="9cf68-264">Peuvent tous d’accord sur les emplacement de l’hologramme et le sens dans lequel le texte est face ?</span><span class="sxs-lookup"><span data-stu-id="9cf68-264">Can you all agree on the hologram's location and which direction the text is facing?</span></span>

## <a name="chapter-4---discovery"></a><span data-ttu-id="9cf68-265">Chapitre 4 - découverte</span><span class="sxs-lookup"><span data-stu-id="9cf68-265">Chapter 4 - Discovery</span></span>

>[!VIDEO https://www.youtube.com/embed/5NxJWMV4BP8]

<span data-ttu-id="9cf68-266">Tout le monde peut voir maintenant l’hologramme même !</span><span class="sxs-lookup"><span data-stu-id="9cf68-266">Everyone can now see the same hologram!</span></span> <span data-ttu-id="9cf68-267">Maintenant nous allons voir tout le monde else connecté à notre monde HOLOGRAPHIQUE partagé.</span><span class="sxs-lookup"><span data-stu-id="9cf68-267">Now let's see everyone else connected to our shared holographic world.</span></span> <span data-ttu-id="9cf68-268">Dans ce chapitre, nous allons saisir l’emplacement principal et la rotation de tous les autres appareils HoloLens dans la même session de partage.</span><span class="sxs-lookup"><span data-stu-id="9cf68-268">In this chapter, we'll grab the head location and rotation of all other HoloLens devices in the same sharing session.</span></span>

### <a name="objectives"></a><span data-ttu-id="9cf68-269">Objectifs</span><span class="sxs-lookup"><span data-stu-id="9cf68-269">Objectives</span></span>

* <span data-ttu-id="9cf68-270">Découvrir les uns des autres dans notre expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="9cf68-270">Discover each other in our shared experience.</span></span>
* <span data-ttu-id="9cf68-271">Choisissez et partager un avatar de lecteur.</span><span class="sxs-lookup"><span data-stu-id="9cf68-271">Choose and share a player avatar.</span></span>
* <span data-ttu-id="9cf68-272">Attacher l’avatar de joueur en regard de têtes de tout le monde.</span><span class="sxs-lookup"><span data-stu-id="9cf68-272">Attach the player avatar next to everyone's heads.</span></span>

### <a name="instructions"></a><span data-ttu-id="9cf68-273">Instructions</span><span class="sxs-lookup"><span data-stu-id="9cf68-273">Instructions</span></span>

* <span data-ttu-id="9cf68-274">Dans le **panneau projet** accédez à la **hologrammes** dossier.</span><span class="sxs-lookup"><span data-stu-id="9cf68-274">In the **Project panel** navigate to the **Holograms** folder.</span></span>
* <span data-ttu-id="9cf68-275">Faites glisser et déposez le **PlayerAvatarStore** dans le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-275">Drag and drop the **PlayerAvatarStore** into the **Hierarchy**.</span></span>
* <span data-ttu-id="9cf68-276">Dans le **panneau projet** accédez à la **Scripts** dossier.</span><span class="sxs-lookup"><span data-stu-id="9cf68-276">In the **Project panel** navigate to the **Scripts** folder.</span></span>
* <span data-ttu-id="9cf68-277">Double-cliquez sur le **AvatarSelector** script pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9cf68-277">Double-click the **AvatarSelector** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="9cf68-278">Remplacez le contenu par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9cf68-278">Replace the contents with the code below.</span></span>

```cs
using UnityEngine;
using Academy.HoloToolkit.Unity;

/// <summary>
/// Script to handle the user selecting the avatar.
/// </summary>
public class AvatarSelector : MonoBehaviour
{
    /// <summary>
    /// This is the index set by the PlayerAvatarStore for the avatar.
    /// </summary>
    public int AvatarIndex { get; set; }

    /// <summary>
    /// Called when the user is gazing at this avatar and air-taps it.
    /// This sends the user's selection to the rest of the devices in the experience.
    /// </summary>
    void OnSelect()
    {
        PlayerAvatarStore.Instance.DismissAvatarPicker();

        LocalPlayerManager.Instance.SetUserAvatar(AvatarIndex);        
    }

    void Start()
    {
        // Add Billboard component so the avatar always faces the user.
        Billboard billboard = gameObject.GetComponent<Billboard>();
        if (billboard == null)
        {
            billboard = gameObject.AddComponent<Billboard>();
        }

        // Lock rotation along the Y axis.
        billboard.PivotAxis = PivotAxis.Y;
    }
}
```

* <span data-ttu-id="9cf68-279">Dans le **hiérarchie** sélectionner le **HologramCollection** objet.</span><span class="sxs-lookup"><span data-stu-id="9cf68-279">In the **Hierarchy** select the **HologramCollection** object.</span></span>
* <span data-ttu-id="9cf68-280">Dans le **inspecteur** cliquez sur **ajouter un composant**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-280">In the **Inspector** click **Add Component**.</span></span>
* <span data-ttu-id="9cf68-281">Dans la zone de recherche, tapez **Gestionnaire de lecteur Local**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-281">In the search box, type **Local Player Manager**.</span></span> <span data-ttu-id="9cf68-282">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="9cf68-282">Select the search result.</span></span>
* <span data-ttu-id="9cf68-283">Dans le **hiérarchie** sélectionner le **HologramCollection** objet.</span><span class="sxs-lookup"><span data-stu-id="9cf68-283">In the **Hierarchy** select the **HologramCollection** object.</span></span>
* <span data-ttu-id="9cf68-284">Dans le **inspecteur** cliquez sur **ajouter un composant**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-284">In the **Inspector** click **Add Component**.</span></span>
* <span data-ttu-id="9cf68-285">Dans la zone de recherche, tapez **Gestionnaire de lecteur distant**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-285">In the search box, type **Remote Player Manager**.</span></span> <span data-ttu-id="9cf68-286">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="9cf68-286">Select the search result.</span></span>
* <span data-ttu-id="9cf68-287">Ouvrez le **HologramPlacement** script dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9cf68-287">Open the **HologramPlacement** script in Visual Studio.</span></span>
* <span data-ttu-id="9cf68-288">Remplacez le contenu par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9cf68-288">Replace the contents with the code below.</span></span>

```cs
using UnityEngine;
using System.Collections.Generic;
using UnityEngine.Windows.Speech;
using Academy.HoloToolkit.Unity;
using Academy.HoloToolkit.Sharing;

public class HologramPlacement : Singleton<HologramPlacement>
{
    /// <summary>
    /// Tracks if we have been sent a transform for the model.
    /// The model is rendered relative to the actual anchor.
    /// </summary>
    public bool GotTransform { get; private set; }

    /// <summary>
    /// When the experience starts, we disable all of the rendering of the model.
    /// </summary>
    List<MeshRenderer> disabledRenderers = new List<MeshRenderer>();

    void Start()
    {
        // When we first start, we need to disable the model to avoid it obstructing the user picking a hat.
        DisableModel();

        // We care about getting updates for the model transform.
        CustomMessages.Instance.MessageHandlers[CustomMessages.TestMessageID.StageTransform] = this.OnStageTransform;

        // And when a new user join we will send the model transform we have.
        SharingSessionTracker.Instance.SessionJoined += Instance_SessionJoined;
    }

    /// <summary>
    /// When a new user joins we want to send them the relative transform for the model if we have it.
    /// </summary>
    /// <param name="sender"></param>
    /// <param name="e"></param>
    private void Instance_SessionJoined(object sender, SharingSessionTracker.SessionJoinedEventArgs e)
    {
        if (GotTransform)
        {
            CustomMessages.Instance.SendStageTransform(transform.localPosition, transform.localRotation);
        }
    }

    /// <summary>
    /// Turns off all renderers for the model.
    /// </summary>
    void DisableModel()
    {
        foreach (MeshRenderer renderer in gameObject.GetComponentsInChildren<MeshRenderer>())
        {
            if (renderer.enabled)
            {
                renderer.enabled = false;
                disabledRenderers.Add(renderer);
            }
        }

        foreach (MeshCollider collider in gameObject.GetComponentsInChildren<MeshCollider>())
        {
            collider.enabled = false;
        }
    }

    /// <summary>
    /// Turns on all renderers that were disabled.
    /// </summary>
    void EnableModel()
    {
        foreach (MeshRenderer renderer in disabledRenderers)
        {
            renderer.enabled = true;
        }

        foreach (MeshCollider collider in gameObject.GetComponentsInChildren<MeshCollider>())
        {
            collider.enabled = true;
        }

        disabledRenderers.Clear();
    }


    void Update()
    {
        // Wait till users pick an avatar to enable renderers.
        if (disabledRenderers.Count > 0)
        {
            if (!PlayerAvatarStore.Instance.PickerActive &&
            ImportExportAnchorManager.Instance.AnchorEstablished)
            {
                // After which we want to start rendering.
                EnableModel();

                // And if we've already been sent the relative transform, we will use it.
                if (GotTransform)
                {
                    // This triggers the animation sequence for the model and 
                    // puts the cool materials on the model.
                    GetComponent<EnergyHubBase>().SendMessage("OnSelect");
                }
            }
        }
        else if (GotTransform == false)
        {
            transform.position = Vector3.Lerp(transform.position, ProposeTransformPosition(), 0.2f);
        }
    }

    Vector3 ProposeTransformPosition()
    {
        // Put the model 2m in front of the user.
        Vector3 retval = Camera.main.transform.position + Camera.main.transform.forward * 2;

        return retval;
    }

    public void OnSelect()
    {
        // Note that we have a transform.
        GotTransform = true;

        // And send it to our friends.
        CustomMessages.Instance.SendStageTransform(transform.localPosition, transform.localRotation);
    }

    /// <summary>
    /// When a remote system has a transform for us, we'll get it here.
    /// </summary>
    /// <param name="msg"></param>
    void OnStageTransform(NetworkInMessage msg)
    {
        // We read the user ID but we don't use it here.
        msg.ReadInt64();

        transform.localPosition = CustomMessages.Instance.ReadVector3(msg);
        transform.localRotation = CustomMessages.Instance.ReadQuaternion(msg);

        // The first time, we'll want to send the message to the model to do its animation and
        // swap its materials.
        if (disabledRenderers.Count == 0 && GotTransform == false)
        {
            GetComponent<EnergyHubBase>().SendMessage("OnSelect");
        }

        GotTransform = true;
    }

    public void ResetStage()
    {
        // We'll use this later.
    }
}
```

* <span data-ttu-id="9cf68-289">Ouvrez le **AppStateManager** script dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9cf68-289">Open the **AppStateManager** script in Visual Studio.</span></span>
* <span data-ttu-id="9cf68-290">Remplacez le contenu par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9cf68-290">Replace the contents with the code below.</span></span>

```cs
using UnityEngine;
using Academy.HoloToolkit.Unity;

/// <summary>
/// Keeps track of the current state of the experience.
/// </summary>
public class AppStateManager : Singleton<AppStateManager>
{
    /// <summary>
    /// Enum to track progress through the experience.
    /// </summary>
    public enum AppState
    {
        Starting = 0,
        WaitingForAnchor,
        WaitingForStageTransform,
        PickingAvatar,
        Ready
    }

    /// <summary>
    /// Tracks the current state in the experience.
    /// </summary>
    public AppState CurrentAppState { get; set; }

    void Start()
    {
        // We start in the 'picking avatar' mode.
        CurrentAppState = AppState.PickingAvatar;

        // We start by showing the avatar picker.
        PlayerAvatarStore.Instance.SpawnAvatarPicker();
    }

    void Update()
    {
        switch (CurrentAppState)
        {
            case AppState.PickingAvatar:
                // Avatar picking is done when the avatar picker has been dismissed.
                if (PlayerAvatarStore.Instance.PickerActive == false)
                {
                    CurrentAppState = AppState.WaitingForAnchor;
                }
                break;
            case AppState.WaitingForAnchor:
                if (ImportExportAnchorManager.Instance.AnchorEstablished)
                {
                    CurrentAppState = AppState.WaitingForStageTransform;
                    GestureManager.Instance.OverrideFocusedObject = HologramPlacement.Instance.gameObject;
                }
                break;
            case AppState.WaitingForStageTransform:
                // Now if we have the stage transform we are ready to go.
                if (HologramPlacement.Instance.GotTransform)
                {
                    CurrentAppState = AppState.Ready;
                    GestureManager.Instance.OverrideFocusedObject = null;
                }
                break;
        }
    }
}
```

<span data-ttu-id="9cf68-291">**Déployer et profitez de**</span><span class="sxs-lookup"><span data-stu-id="9cf68-291">**Deploy and Enjoy**</span></span>
* <span data-ttu-id="9cf68-292">Générer et déployer le projet sur vos appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9cf68-292">Build and deploy the project to your HoloLens devices.</span></span>
* <span data-ttu-id="9cf68-293">Lorsque vous entendez un test ping, recherchez le menu de sélection avatar, puis sélectionnez un avatar avec le mouvement d’appui en l’air.</span><span class="sxs-lookup"><span data-stu-id="9cf68-293">When you hear a pinging sound, find the avatar selection menu and select an avatar with the air-tap gesture.</span></span>
* <span data-ttu-id="9cf68-294">Si vous n’êtes pas dans n’importe quel hologrammes, le point de lumière autour de votre curseur activera une couleur différente lorsque votre HoloLens communique avec le service : l’initialisation (violet foncé), le téléchargement de point d’ancrage (vert), l’importation/exportation de données d’emplacement (jaune), charger le point d’ancrage (bleu).</span><span class="sxs-lookup"><span data-stu-id="9cf68-294">If you're not looking at any holograms, the point light around your cursor will turn a different color when your HoloLens is communicating with the service: initializing (dark purple), downloading the anchor (green), importing/exporting location data (yellow), uploading the anchor (blue).</span></span> <span data-ttu-id="9cf68-295">Si votre point clair autour de votre curseur est la couleur par défaut (Violet clair), vous êtes prêt à interagir avec d’autres joueurs dans votre session !</span><span class="sxs-lookup"><span data-stu-id="9cf68-295">If your point light around your cursor is the default color (light purple), then you are ready to interact with other players in your session!</span></span>
* <span data-ttu-id="9cf68-296">Examinez les autres utilisateurs connectés à votre espace - il y aura un robot HOLOGRAPHIQUE flotte au-dessus de son épaule et celle de leurs mouvements principal !</span><span class="sxs-lookup"><span data-stu-id="9cf68-296">Look at other people connected to your space - there will be a holographic robot floating above their shoulder and mimicking their head motions!</span></span>

## <a name="chapter-5---placement"></a><span data-ttu-id="9cf68-297">Chapitre 5 : Placement</span><span class="sxs-lookup"><span data-stu-id="9cf68-297">Chapter 5 - Placement</span></span>

>[!VIDEO https://www.youtube.com/embed/afFTwHQIw0s]

<span data-ttu-id="9cf68-298">Dans ce chapitre, nous veillerons à ce point d’ancrage peuvent pas être placés sur des surfaces du monde réel.</span><span class="sxs-lookup"><span data-stu-id="9cf68-298">In this chapter, we'll make the anchor able to be placed on real-world surfaces.</span></span> <span data-ttu-id="9cf68-299">Nous allons utiliser des coordonnées partagées pour placer ce point d’ancrage dans le point médian entre tous les utilisateurs connectés à l’expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="9cf68-299">We'll use shared coordinates to place that anchor in the middle point between everyone connected to the shared experience.</span></span>

### <a name="objectives"></a><span data-ttu-id="9cf68-300">Objectifs</span><span class="sxs-lookup"><span data-stu-id="9cf68-300">Objectives</span></span>

* <span data-ttu-id="9cf68-301">Placez hologrammes sur la carte spatiale en fonction de la position de tête de joueurs.</span><span class="sxs-lookup"><span data-stu-id="9cf68-301">Place holograms on the spatial map based on players’ head position.</span></span>

### <a name="instructions"></a><span data-ttu-id="9cf68-302">Instructions</span><span class="sxs-lookup"><span data-stu-id="9cf68-302">Instructions</span></span>

* <span data-ttu-id="9cf68-303">Dans le **panneau projet** accédez à la **hologrammes** dossier.</span><span class="sxs-lookup"><span data-stu-id="9cf68-303">In the **Project panel** navigate to the **Holograms** folder.</span></span>
* <span data-ttu-id="9cf68-304">Faites glisser et déposez le **CustomSpatialMapping** prefab sur le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-304">Drag and drop the **CustomSpatialMapping** prefab onto the **Hierarchy**.</span></span>
* <span data-ttu-id="9cf68-305">Dans le **panneau projet** accédez à la **Scripts** dossier.</span><span class="sxs-lookup"><span data-stu-id="9cf68-305">In the **Project panel** navigate to the **Scripts** folder.</span></span>
* <span data-ttu-id="9cf68-306">Double-cliquez sur le **AppStateManager** script pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9cf68-306">Double-click the **AppStateManager** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="9cf68-307">Remplacez le contenu par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9cf68-307">Replace the contents with the code below.</span></span>

```cs
using UnityEngine;
using Academy.HoloToolkit.Unity;

/// <summary>
/// Keeps track of the current state of the experience.
/// </summary>
public class AppStateManager : Singleton<AppStateManager>
{
    /// <summary>
    /// Enum to track progress through the experience.
    /// </summary>
    public enum AppState
    {
        Starting = 0,
        PickingAvatar,
        WaitingForAnchor,
        WaitingForStageTransform,
        Ready
    }

    // The object to call to make a projectile.
    GameObject shootHandler = null;

    /// <summary>
    /// Tracks the current state in the experience.
    /// </summary>
    public AppState CurrentAppState { get; set; }

    void Start()
    {
        // The shootHandler shoots projectiles.
        if (GetComponent<ProjectileLauncher>() != null)
        {
            shootHandler = GetComponent<ProjectileLauncher>().gameObject;
        }

        // We start in the 'picking avatar' mode.
        CurrentAppState = AppState.PickingAvatar;

        // Spatial mapping should be disabled when we start up so as not
        // to distract from the avatar picking.
        SpatialMappingManager.Instance.StopObserver();
        SpatialMappingManager.Instance.gameObject.SetActive(false);

        // On device we start by showing the avatar picker.
        PlayerAvatarStore.Instance.SpawnAvatarPicker();
    }

    public void ResetStage()
    {
        // If we fall back to waiting for anchor, everything needed to 
        // get us into setting the target transform state will be setup.
        if (CurrentAppState != AppState.PickingAvatar)
        {
            CurrentAppState = AppState.WaitingForAnchor;
        }

        // Reset the underworld.
        if (UnderworldBase.Instance)
        {
            UnderworldBase.Instance.ResetUnderworld();
        }
    }

    void Update()
    {
        switch (CurrentAppState)
        {
            case AppState.PickingAvatar:
                // Avatar picking is done when the avatar picker has been dismissed.
                if (PlayerAvatarStore.Instance.PickerActive == false)
                {
                    CurrentAppState = AppState.WaitingForAnchor;
                }
                break;
            case AppState.WaitingForAnchor:
                // Once the anchor is established we need to run spatial mapping for a 
                // little while to build up some meshes.
                if (ImportExportAnchorManager.Instance.AnchorEstablished)
                {
                    CurrentAppState = AppState.WaitingForStageTransform;
                    GestureManager.Instance.OverrideFocusedObject = HologramPlacement.Instance.gameObject;

                    SpatialMappingManager.Instance.gameObject.SetActive(true);
                    SpatialMappingManager.Instance.DrawVisualMeshes = true;
                    SpatialMappingDeformation.Instance.ResetGlobalRendering();
                    SpatialMappingManager.Instance.StartObserver();
                }
                break;
            case AppState.WaitingForStageTransform:
                // Now if we have the stage transform we are ready to go.
                if (HologramPlacement.Instance.GotTransform)
                {
                    CurrentAppState = AppState.Ready;
                    GestureManager.Instance.OverrideFocusedObject = shootHandler;
                }
                break;
        }
    }
}
```

* <span data-ttu-id="9cf68-308">Dans le **panneau projet** accédez à la **Scripts** dossier.</span><span class="sxs-lookup"><span data-stu-id="9cf68-308">In the **Project panel** navigate to the **Scripts** folder.</span></span>
* <span data-ttu-id="9cf68-309">Double-cliquez sur le **HologramPlacement** script pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9cf68-309">Double-click the **HologramPlacement** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="9cf68-310">Remplacez le contenu par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9cf68-310">Replace the contents with the code below.</span></span>

```cs
using UnityEngine;
using System.Collections.Generic;
using UnityEngine.Windows.Speech;
using Academy.HoloToolkit.Unity;
using Academy.HoloToolkit.Sharing;

public class HologramPlacement : Singleton<HologramPlacement>
{
    /// <summary>
    /// Tracks if we have been sent a transform for the model.
    /// The model is rendered relative to the actual anchor.
    /// </summary>
    public bool GotTransform { get; private set; }

    /// <summary>
    /// When the experience starts, we disable all of the rendering of the model.
    /// </summary>
    List<MeshRenderer> disabledRenderers = new List<MeshRenderer>();

    /// <summary>
    /// We use a voice command to enable moving the target.
    /// </summary>
    KeywordRecognizer keywordRecognizer;

    void Start()
    {
        // When we first start, we need to disable the model to avoid it obstructing the user picking a hat.
        DisableModel();

        // We care about getting updates for the model transform.
        CustomMessages.Instance.MessageHandlers[CustomMessages.TestMessageID.StageTransform] = this.OnStageTransform;

        // And when a new user join we will send the model transform we have.
        SharingSessionTracker.Instance.SessionJoined += Instance_SessionJoined;

        // And if the users want to reset the stage transform.
        CustomMessages.Instance.MessageHandlers[CustomMessages.TestMessageID.ResetStage] = this.OnResetStage;

        // Setup a keyword recognizer to enable resetting the target location.
        List<string> keywords = new List<string>();
        keywords.Add("Reset Target");
        keywordRecognizer = new KeywordRecognizer(keywords.ToArray());
        keywordRecognizer.OnPhraseRecognized += KeywordRecognizer_OnPhraseRecognized;
        keywordRecognizer.Start();
    }

    /// <summary>
    /// When the keyword recognizer hears a command this will be called.  
    /// In this case we only have one keyword, which will re-enable moving the 
    /// target.
    /// </summary>
    /// <param name="args">information to help route the voice command.</param>
    private void KeywordRecognizer_OnPhraseRecognized(PhraseRecognizedEventArgs args)
    {
        ResetStage();
    }

    /// <summary>
    /// Resets the stage transform, so users can place the target again.
    /// </summary>
    public void ResetStage()
    {
        GotTransform = false;

        // AppStateManager needs to know about this so that
        // the right objects get input routed to them.
        AppStateManager.Instance.ResetStage();

        // Other devices in the experience need to know about this as well.
        CustomMessages.Instance.SendResetStage();

        // And we need to reset the object to its start animation state.
        GetComponent<EnergyHubBase>().ResetAnimation();
    }

    /// <summary>
    /// When a new user joins we want to send them the relative transform for the model if we have it.
    /// </summary>
    /// <param name="sender"></param>
    /// <param name="e"></param>
    private void Instance_SessionJoined(object sender, SharingSessionTracker.SessionJoinedEventArgs e)
    {
        if (GotTransform)
        {
            CustomMessages.Instance.SendStageTransform(transform.localPosition, transform.localRotation);
        }
    }

    /// <summary>
    /// Turns off all renderers for the model.
    /// </summary>
    void DisableModel()
    {
        foreach (MeshRenderer renderer in gameObject.GetComponentsInChildren<MeshRenderer>())
        {
            if (renderer.enabled)
            {
                renderer.enabled = false;
                disabledRenderers.Add(renderer);
            }
        }

        foreach (MeshCollider collider in gameObject.GetComponentsInChildren<MeshCollider>())
        {
            collider.enabled = false;
        }
    }

    /// <summary>
    /// Turns on all renderers that were disabled.
    /// </summary>
    void EnableModel()
    {
        foreach (MeshRenderer renderer in disabledRenderers)
        {
            renderer.enabled = true;
        }

        foreach (MeshCollider collider in gameObject.GetComponentsInChildren<MeshCollider>())
        {
            collider.enabled = true;
        }

        disabledRenderers.Clear();
    }


    void Update()
    {
        // Wait till users pick an avatar to enable renderers.
        if (disabledRenderers.Count > 0)
        {
            if (!PlayerAvatarStore.Instance.PickerActive &&
            ImportExportAnchorManager.Instance.AnchorEstablished)
            {
                // After which we want to start rendering.
                EnableModel();

                // And if we've already been sent the relative transform, we will use it.
                if (GotTransform)
                {
                    // This triggers the animation sequence for the model and 
                    // puts the cool materials on the model.
                    GetComponent<EnergyHubBase>().SendMessage("OnSelect");
                }
            }
        }
        else if (GotTransform == false)
        {
            transform.position = Vector3.Lerp(transform.position, ProposeTransformPosition(), 0.2f);
        }
    }

    Vector3 ProposeTransformPosition()
    {
        Vector3 retval;
        // We need to know how many users are in the experience with good transforms.
        Vector3 cumulatedPosition = Camera.main.transform.position;
        int playerCount = 1;
        foreach (RemotePlayerManager.RemoteHeadInfo remoteHead in RemotePlayerManager.Instance.remoteHeadInfos)
        {
            if (remoteHead.Anchored && remoteHead.Active)
            {
                playerCount++;
                cumulatedPosition += remoteHead.HeadObject.transform.position;
            }
        }

        // If we have more than one player ...
        if (playerCount > 1)
        {
            // Put the transform in between the players.
            retval = cumulatedPosition / playerCount;
            RaycastHit hitInfo;

            // And try to put the transform on a surface below the midpoint of the players.
            if (Physics.Raycast(retval, Vector3.down, out hitInfo, 5, SpatialMappingManager.Instance.LayerMask))
            {
                retval = hitInfo.point;
            }
        }
        // If we are the only player, have the model act as the 'cursor' ...
        else
        {
            // We prefer to put the model on a real world surface.
            RaycastHit hitInfo;

            if (Physics.Raycast(Camera.main.transform.position, Camera.main.transform.forward, out hitInfo, 30, SpatialMappingManager.Instance.LayerMask))
            {
                retval = hitInfo.point;
            }
            else
            {
                // But if we don't have a ray that intersects the real world, just put the model 2m in
                // front of the user.
                retval = Camera.main.transform.position + Camera.main.transform.forward * 2;
            }
        }
        return retval;
    }

    public void OnSelect()
    {
        // Note that we have a transform.
        GotTransform = true;

        // And send it to our friends.
        CustomMessages.Instance.SendStageTransform(transform.localPosition, transform.localRotation);
    }

    /// <summary>
    /// When a remote system has a transform for us, we'll get it here.
    /// </summary>
    /// <param name="msg"></param>
    void OnStageTransform(NetworkInMessage msg)
    {
        // We read the user ID but we don't use it here.
        msg.ReadInt64();

        transform.localPosition = CustomMessages.Instance.ReadVector3(msg);
        transform.localRotation = CustomMessages.Instance.ReadQuaternion(msg);

        // The first time, we'll want to send the message to the model to do its animation and
        // swap its materials.
        if (disabledRenderers.Count == 0 && GotTransform == false)
        {
            GetComponent<EnergyHubBase>().SendMessage("OnSelect");
        }

        GotTransform = true;
    }

    /// <summary>
    /// When a remote system has a transform for us, we'll get it here.
    /// </summary>
    void OnResetStage(NetworkInMessage msg)
    {
        GotTransform = false;

        GetComponent<EnergyHubBase>().ResetAnimation();
        AppStateManager.Instance.ResetStage();
    }
}
```

<span data-ttu-id="9cf68-311">**Déployer et profitez de**</span><span class="sxs-lookup"><span data-stu-id="9cf68-311">**Deploy and enjoy**</span></span>
* <span data-ttu-id="9cf68-312">Générer et déployer le projet sur vos appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9cf68-312">Build and deploy the project to your HoloLens devices.</span></span>
* <span data-ttu-id="9cf68-313">Lorsque l’application est prête, mettez au point dans un cercle et notez que le EnergyHub apparaît au centre de tout le monde.</span><span class="sxs-lookup"><span data-stu-id="9cf68-313">When the app is ready, stand in a circle and notice how the EnergyHub appears in the center of everyone.</span></span>
* <span data-ttu-id="9cf68-314">Cliquez pour placer le EnergyHub.</span><span class="sxs-lookup"><span data-stu-id="9cf68-314">Tap to place the EnergyHub.</span></span>
* <span data-ttu-id="9cf68-315">Essayez la commande de voix 'Réinitialiser Target' et reprenez le EnergyHub fonctionnent ensemble en tant que groupe pour déplacer l’hologramme vers un nouvel emplacement.</span><span class="sxs-lookup"><span data-stu-id="9cf68-315">Try the voice command 'Reset Target' to pick the EnergyHub back up and work together as a group to move the hologram to a new location.</span></span>

## <a name="chapter-6---real-world-physics"></a><span data-ttu-id="9cf68-316">Chapitre 6 - réel physique</span><span class="sxs-lookup"><span data-stu-id="9cf68-316">Chapter 6 - Real-World Physics</span></span>

>[!VIDEO https://www.youtube.com/embed/XNpQVSyXwMo]

<span data-ttu-id="9cf68-317">Dans ce chapitre, nous allons ajouter hologrammes rebondissent sur les surfaces du monde réel.</span><span class="sxs-lookup"><span data-stu-id="9cf68-317">In this chapter we'll add holograms that bounce off real-world surfaces.</span></span> <span data-ttu-id="9cf68-318">Surveillez votre page se remplisse pas de projets lancés par vous et vos amis !</span><span class="sxs-lookup"><span data-stu-id="9cf68-318">Watch your space fill up with projects launched by both you and your friends!</span></span>

### <a name="objectives"></a><span data-ttu-id="9cf68-319">Objectifs</span><span class="sxs-lookup"><span data-stu-id="9cf68-319">Objectives</span></span>

* <span data-ttu-id="9cf68-320">Lance des projectiles qui rebondissent sur les surfaces du monde réel.</span><span class="sxs-lookup"><span data-stu-id="9cf68-320">Launch projectiles that bounce off real-world surfaces.</span></span>
* <span data-ttu-id="9cf68-321">Partager les projectiles afin d’autres joueurs puissent les voir.</span><span class="sxs-lookup"><span data-stu-id="9cf68-321">Share the projectiles so other players can see them.</span></span>

### <a name="instructions"></a><span data-ttu-id="9cf68-322">Instructions</span><span class="sxs-lookup"><span data-stu-id="9cf68-322">Instructions</span></span>

* <span data-ttu-id="9cf68-323">Dans le **hiérarchie** sélectionner le **HologramCollection** objet.</span><span class="sxs-lookup"><span data-stu-id="9cf68-323">In the **Hierarchy** select the **HologramCollection** object.</span></span>
* <span data-ttu-id="9cf68-324">Dans le **inspecteur** cliquez sur **ajouter un composant**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-324">In the **Inspector** click **Add Component**.</span></span>
* <span data-ttu-id="9cf68-325">Dans la zone de recherche, tapez **PROJECTILES Lanceur**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-325">In the search box, type **Projectile Launcher**.</span></span> <span data-ttu-id="9cf68-326">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="9cf68-326">Select the search result.</span></span>

<span data-ttu-id="9cf68-327">**Déployer et profitez de**</span><span class="sxs-lookup"><span data-stu-id="9cf68-327">**Deploy and enjoy**</span></span>
* <span data-ttu-id="9cf68-328">Générer et déployer sur vos appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9cf68-328">Build and deploy to your HoloLens devices.</span></span>
* <span data-ttu-id="9cf68-329">Lorsque l’application s’exécute sur tous les appareils, effectuez un appui pour lancer des projectiles sur les surfaces du monde réel.</span><span class="sxs-lookup"><span data-stu-id="9cf68-329">When the app is running on all devices, perform an air-tap to launch projectile at real world surfaces.</span></span>
* <span data-ttu-id="9cf68-330">Découvrez ce qui se passe lorsque votre PROJECTILES est en conflit avec les avatar d’un autre lecteur.</span><span class="sxs-lookup"><span data-stu-id="9cf68-330">See what happens when your projectile collides with another player's avatar!</span></span>

## <a name="chapter-7---grand-finale"></a><span data-ttu-id="9cf68-331">Chapitre 7 - aborder</span><span class="sxs-lookup"><span data-stu-id="9cf68-331">Chapter 7 - Grand Finale</span></span>

>[!VIDEO https://www.youtube.com/embed/kDUPUvZEqRg]

<span data-ttu-id="9cf68-332">Dans ce chapitre, nous allons découvrir un portail qui ne peut être détecté à la collaboration.</span><span class="sxs-lookup"><span data-stu-id="9cf68-332">In this chapter, we'll uncover a portal that can only be discovered with collaboration.</span></span>

### <a name="objectives"></a><span data-ttu-id="9cf68-333">Objectifs</span><span class="sxs-lookup"><span data-stu-id="9cf68-333">Objectives</span></span>

* <span data-ttu-id="9cf68-334">Œuvrent ensemble pour lancer suffisamment projectiles sur le point d’ancrage pour découvrir un portail secret !</span><span class="sxs-lookup"><span data-stu-id="9cf68-334">Work together to launch enough projectiles at the anchor to uncover a secret portal!</span></span>

### <a name="instructions"></a><span data-ttu-id="9cf68-335">Instructions</span><span class="sxs-lookup"><span data-stu-id="9cf68-335">Instructions</span></span>

* <span data-ttu-id="9cf68-336">Dans le **panneau projet** accédez à la **hologrammes** dossier.</span><span class="sxs-lookup"><span data-stu-id="9cf68-336">In the **Project panel** navigate to the **Holograms** folder.</span></span>
* <span data-ttu-id="9cf68-337">Faites glisser et déposez le **Underworld** actif comme un **enfant de HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-337">Drag and drop the **Underworld** asset as a **child of HologramCollection**.</span></span>
* <span data-ttu-id="9cf68-338">Avec **HologramCollection** sélectionnée, cliquez sur le **ajouter un composant** situé dans le **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-338">With **HologramCollection** selected, click the **Add Component** button in the **Inspector**.</span></span>
* <span data-ttu-id="9cf68-339">Dans le menu, tapez dans la zone de recherche **ExplodeTarget**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-339">In the menu, type in the search box **ExplodeTarget**.</span></span> <span data-ttu-id="9cf68-340">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="9cf68-340">Select the search result.</span></span>
* <span data-ttu-id="9cf68-341">Avec **HologramCollection** sélectionné, à partir de la **hiérarchie** faites glisser le **EnergyHub** de l’objet à la **cible** champ dans le **Inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-341">With **HologramCollection** selected, from the **Hierarchy** drag the **EnergyHub** object to the **Target** field in the **Inspector**.</span></span>
* <span data-ttu-id="9cf68-342">Avec **HologramCollection** sélectionné, à partir de la **hiérarchie** faites glisser le **Underworld** de l’objet à la **Underworld** champ dans le  **Inspecteur de**.</span><span class="sxs-lookup"><span data-stu-id="9cf68-342">With **HologramCollection** selected, from the **Hierarchy** drag the **Underworld** object to the **Underworld** field in the **Inspector**.</span></span>

<span data-ttu-id="9cf68-343">**Déployer et profitez de**</span><span class="sxs-lookup"><span data-stu-id="9cf68-343">**Deploy and enjoy**</span></span>
* <span data-ttu-id="9cf68-344">Générer et déployer sur vos appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9cf68-344">Build and deploy to your HoloLens devices.</span></span>
* <span data-ttu-id="9cf68-345">Lorsque l’application est lancée, collaborer pour lancer des projectiles sur le EnergyHub.</span><span class="sxs-lookup"><span data-stu-id="9cf68-345">When the app has launched, collaborate together to launch projectiles at the EnergyHub.</span></span>
* <span data-ttu-id="9cf68-346">Lorsque l’underworld s’affiche, lancer des projectiles sur les robots underworld (atteinte un robot trois fois pour le plaisir supplémentaire).</span><span class="sxs-lookup"><span data-stu-id="9cf68-346">When the underworld appears, launch projectiles at underworld robots (hit a robot three times for extra fun).</span></span>
