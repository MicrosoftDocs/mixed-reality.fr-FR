---
title: RM partageant 240-plusieurs appareils HoloLens
description: Suivez cette procédure pas à pas de codage avec Unity, Visual Studio et HoloLens pour apprendre les détails du partage d’hologrammes.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, partage, mise en réseau, Academy, didacticiel
ms.openlocfilehash: 70a39a739d360a5032bc8df76b6f0bd57521d9ec
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63522330"
---
>[!NOTE]
><span data-ttu-id="fb070-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="fb070-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="fb070-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="fb070-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="fb070-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="fb070-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="fb070-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="fb070-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="fb070-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="fb070-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="fb070-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="fb070-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-sharing-240-multiple-hololens-devices"></a><span data-ttu-id="fb070-110">RM partageant 240: Plusieurs appareils HoloLens</span><span class="sxs-lookup"><span data-stu-id="fb070-110">MR Sharing 240: Multiple HoloLens devices</span></span>

<span data-ttu-id="fb070-111">Les hologrammes sont présents dans notre monde en restant en place au fur et à mesure que nous nous déplacerons dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="fb070-111">Holograms are given presence in our world by remaining in place as we move about in space.</span></span> <span data-ttu-id="fb070-112">HoloLens conserve les hologrammes en place à l’aide de différents [systèmes de coordonnées](coordinate-systems.md) pour effectuer le suivi de l’emplacement et de l’orientation des objets.</span><span class="sxs-lookup"><span data-stu-id="fb070-112">HoloLens keeps holograms in place by using various [coordinate systems](coordinate-systems.md) to keep track of the location and orientation of objects.</span></span> <span data-ttu-id="fb070-113">Lorsque nous partageons ces systèmes de coordonnées entre les appareils, nous pouvons créer une expérience partagée qui nous permet de participer à un monde holographique partagé.</span><span class="sxs-lookup"><span data-stu-id="fb070-113">When we share these coordinate systems between devices, we can create a shared experience that allows us to take part in a shared holographic world.</span></span>

<span data-ttu-id="fb070-114">Dans ce didacticiel, nous allons:</span><span class="sxs-lookup"><span data-stu-id="fb070-114">In this tutorial, we will:</span></span>

* <span data-ttu-id="fb070-115">Configurez un réseau pour une expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="fb070-115">Setup a network for a shared experience.</span></span>
* <span data-ttu-id="fb070-116">Partager des hologrammes sur des appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="fb070-116">Share holograms across HoloLens devices.</span></span>
* <span data-ttu-id="fb070-117">Découvrez d’autres personnes dans notre monde holographique partagé.</span><span class="sxs-lookup"><span data-stu-id="fb070-117">Discover other people in our shared holographic world.</span></span>
* <span data-ttu-id="fb070-118">Créez une expérience interactive partagée où vous pouvez cibler d’autres joueurs et lancer des projectiles!</span><span class="sxs-lookup"><span data-stu-id="fb070-118">Create a shared interactive experience where you can target other players - and launch projectiles at them!</span></span>

## <a name="device-support"></a><span data-ttu-id="fb070-119">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="fb070-119">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="fb070-120">Course</span><span class="sxs-lookup"><span data-stu-id="fb070-120">Course</span></span></th><th style="width:150px"> <span data-ttu-id="fb070-121"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="fb070-121"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="fb070-122"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="fb070-122"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="fb070-123">RM partageant 240: Plusieurs appareils HoloLens</span><span class="sxs-lookup"><span data-stu-id="fb070-123">MR Sharing 240: Multiple HoloLens devices</span></span></td><td style="text-align: center;"> <span data-ttu-id="fb070-124">✔️</span><span class="sxs-lookup"><span data-stu-id="fb070-124">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="fb070-125">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="fb070-125">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fb070-126">Prérequis</span><span class="sxs-lookup"><span data-stu-id="fb070-126">Prerequisites</span></span>

* <span data-ttu-id="fb070-127">Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md) avec l’accès à Internet.</span><span class="sxs-lookup"><span data-stu-id="fb070-127">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md) with Internet access.</span></span>
* <span data-ttu-id="fb070-128">Au moins deux appareils HoloLens [configurés pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="fb070-128">At least two HoloLens devices [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="fb070-129">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="fb070-129">Project files</span></span>

* <span data-ttu-id="fb070-130">Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-240-SharedHolograms.zip) requis par le projet.</span><span class="sxs-lookup"><span data-stu-id="fb070-130">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-240-SharedHolograms.zip) required by the project.</span></span> <span data-ttu-id="fb070-131">Requiert Unity 2017,2 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="fb070-131">Requires Unity 2017.2 or later.</span></span>
  * <span data-ttu-id="fb070-132">Si vous avez encore besoin de la prise en charge d’Unity 5,6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-240.zip).</span><span class="sxs-lookup"><span data-stu-id="fb070-132">If you still need Unity 5.6 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-240.zip).</span></span>
  * <span data-ttu-id="fb070-133">Si vous avez encore besoin de la prise en charge d’Unity 5,5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-240.zip).</span><span class="sxs-lookup"><span data-stu-id="fb070-133">If you still need Unity 5.5 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-240.zip).</span></span>
  * <span data-ttu-id="fb070-134">Si vous avez encore besoin de la prise en charge d’Unity 5,4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-240.zip).</span><span class="sxs-lookup"><span data-stu-id="fb070-134">If you still need Unity 5.4 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-240.zip).</span></span>
* <span data-ttu-id="fb070-135">Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.</span><span class="sxs-lookup"><span data-stu-id="fb070-135">Un-archive the files to your desktop or other easy to reach location.</span></span> <span data-ttu-id="fb070-136">Conservez le nom du dossier en tant que **SharedHolograms**.</span><span class="sxs-lookup"><span data-stu-id="fb070-136">Keep the folder name as **SharedHolograms**.</span></span>

>[!NOTE]
><span data-ttu-id="fb070-137">Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-240-SharedHolograms).</span><span class="sxs-lookup"><span data-stu-id="fb070-137">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-240-SharedHolograms).</span></span>

## <a name="chapter-1---holo-world"></a><span data-ttu-id="fb070-138">Chapitre 1-Holo World</span><span class="sxs-lookup"><span data-stu-id="fb070-138">Chapter 1 - Holo World</span></span>

>[!VIDEO https://www.youtube.com/embed/c7qHYYW8rxQ]

<span data-ttu-id="fb070-139">Dans ce chapitre, nous allons configurer notre premier projet Unity et effectuer un pas à pas détaillé dans le processus de création et de déploiement.</span><span class="sxs-lookup"><span data-stu-id="fb070-139">In this chapter, we'll setup our first Unity project and step through the build and deploy process.</span></span>

### <a name="objectives"></a><span data-ttu-id="fb070-140">Objectifs</span><span class="sxs-lookup"><span data-stu-id="fb070-140">Objectives</span></span>

* <span data-ttu-id="fb070-141">Configurer Unity pour développer des applications holographiques.</span><span class="sxs-lookup"><span data-stu-id="fb070-141">Setup Unity to develop holographic apps.</span></span>
* <span data-ttu-id="fb070-142">Consultez votre hologramme!</span><span class="sxs-lookup"><span data-stu-id="fb070-142">See your hologram!</span></span>

### <a name="instructions"></a><span data-ttu-id="fb070-143">Instructions</span><span class="sxs-lookup"><span data-stu-id="fb070-143">Instructions</span></span>

* <span data-ttu-id="fb070-144">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="fb070-144">Start Unity.</span></span>
* <span data-ttu-id="fb070-145">Sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="fb070-145">Select **Open**.</span></span>
* <span data-ttu-id="fb070-146">Entrez l’emplacement du dossier **SharedHolograms** que vous avez précédemment désarchivé.</span><span class="sxs-lookup"><span data-stu-id="fb070-146">Enter location as the **SharedHolograms** folder you previously unarchived.</span></span>
* <span data-ttu-id="fb070-147">Sélectionnez le **nom du projet** , puis cliquez sur Sélectionner un **dossier**.</span><span class="sxs-lookup"><span data-stu-id="fb070-147">Select **Project Name** and click **Select Folder**.</span></span>
* <span data-ttu-id="fb070-148">Dans la **hiérarchie**, cliquez avec le bouton droit sur l' **appareil photo principal** et sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="fb070-148">In the **Hierarchy**, right-click the **Main Camera** and select **Delete**.</span></span>
* <span data-ttu-id="fb070-149">Dans le dossier **HoloToolkit-partage-240/Prefabs/Camera** , recherchez la **caméra principale** Prefab.</span><span class="sxs-lookup"><span data-stu-id="fb070-149">In the **HoloToolkit-Sharing-240/Prefabs/Camera** folder, find the **Main Camera** prefab.</span></span>
* <span data-ttu-id="fb070-150">Glissez-déposez la **caméra principale** dans la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="fb070-150">Drag and drop the **Main Camera** into the **Hierarchy**.</span></span>
* <span data-ttu-id="fb070-151">Dans la **hiérarchie**, cliquez sur **créer** et **créez un vide**.</span><span class="sxs-lookup"><span data-stu-id="fb070-151">In the **Hierarchy**, click on **Create** and **Create Empty**.</span></span>
* <span data-ttu-id="fb070-152">Cliquez avec le bouton droit sur le nouveau **gameobject** , puis sélectionnez Renommer.</span><span class="sxs-lookup"><span data-stu-id="fb070-152">Right-click the new **GameObject** and select **Rename**.</span></span>
* <span data-ttu-id="fb070-153">Renommez GameObject en **HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="fb070-153">Rename the GameObject to **HologramCollection**.</span></span>
* <span data-ttu-id="fb070-154">Sélectionnez l’objet **HologramCollection** dans la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="fb070-154">Select the **HologramCollection** object in the **Hierarchy**.</span></span>
* <span data-ttu-id="fb070-155">Dans l' **inspecteur** , définissez la position de la **transformation** sur: **X 0, Y:-0,25, Z: 2**.</span><span class="sxs-lookup"><span data-stu-id="fb070-155">In the **Inspector** set the **transform position** to: **X: 0, Y: -0.25, Z: 2**.</span></span>
* <span data-ttu-id="fb070-156">Dans le  dossier hologrammes du **panneau Projet**, recherchez la ressource **EnergyHub** .</span><span class="sxs-lookup"><span data-stu-id="fb070-156">In the **Holograms** folder in the **Project panel**, find the **EnergyHub** asset.</span></span>
* <span data-ttu-id="fb070-157">Glissez-déplacez l’objet **EnergyHub** du **panneau Projet** vers la **hiérarchie** en tant qu' **enfant de HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="fb070-157">Drag and drop the **EnergyHub** object from the **Project panel** to the **Hierarchy** as a **child of HologramCollection**.</span></span>
* <span data-ttu-id="fb070-158">Sélectionnez le **fichier > enregistrer la scène sous...**</span><span class="sxs-lookup"><span data-stu-id="fb070-158">Select **File > Save Scene As...**</span></span>
* <span data-ttu-id="fb070-159">Nommez la scène **SharedHolograms** , puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fb070-159">Name the scene **SharedHolograms** and click **Save**.</span></span>
* <span data-ttu-id="fb070-160">Appuyez sur le bouton de **lecture** dans Unity pour afficher un aperçu de vos hologrammes.</span><span class="sxs-lookup"><span data-stu-id="fb070-160">Press the **Play** button in Unity to preview your holograms.</span></span>
* <span data-ttu-id="fb070-161">Appuyez sur **lecture** une deuxième fois pour arrêter le mode aperçu.</span><span class="sxs-lookup"><span data-stu-id="fb070-161">Press **Play** a second time to stop preview mode.</span></span>

<span data-ttu-id="fb070-162">**Exporter le projet d’Unity vers Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="fb070-162">**Export the project from Unity to Visual Studio**</span></span>
* <span data-ttu-id="fb070-163">Dans Unity, sélectionnez **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="fb070-163">In Unity select **File > Build Settings**.</span></span>
* <span data-ttu-id="fb070-164">Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="fb070-164">Click **Add Open Scenes** to add the scene.</span></span>
* <span data-ttu-id="fb070-165">Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur basculer la **plateforme**.</span><span class="sxs-lookup"><span data-stu-id="fb070-165">Select **Universal Windows Platform** in the **Platform** list and click **Switch Platform**.</span></span>
* <span data-ttu-id="fb070-166">Affectez à **SDK** la valeur **Universal 10**.</span><span class="sxs-lookup"><span data-stu-id="fb070-166">Set **SDK** to **Universal 10**.</span></span>
* <span data-ttu-id="fb070-167">Définissez le **périphérique cible** sur **HoloLens** et le **type de build UWP** sur **D3D**.</span><span class="sxs-lookup"><span data-stu-id="fb070-167">Set **Target device** to **HoloLens** and **UWP Build Type** to **D3D**.</span></span>
* <span data-ttu-id="fb070-168">Vérifiez **les C# projets Unity**.</span><span class="sxs-lookup"><span data-stu-id="fb070-168">Check **Unity C# Projects**.</span></span>
* <span data-ttu-id="fb070-169">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="fb070-169">Click **Build**.</span></span>
* <span data-ttu-id="fb070-170">Dans la fenêtre de l’Explorateur de fichiers qui s’affiche, créez un **nouveau dossier** nommé «App».</span><span class="sxs-lookup"><span data-stu-id="fb070-170">In the file explorer window that appears, create a **New Folder** named "App".</span></span>
* <span data-ttu-id="fb070-171">Cliquez sur le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="fb070-171">Single click the **App** folder.</span></span>
* <span data-ttu-id="fb070-172">Appuyez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="fb070-172">Press **Select Folder**.</span></span>
* <span data-ttu-id="fb070-173">Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fb070-173">When Unity is done, a File Explorer window will appear.</span></span>
* <span data-ttu-id="fb070-174">Ouvrez le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="fb070-174">Open the **App** folder.</span></span>
* <span data-ttu-id="fb070-175">Ouvrez **SharedHolograms. sln** pour lancer Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb070-175">Open **SharedHolograms.sln** to launch Visual Studio.</span></span>
* <span data-ttu-id="fb070-176">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.</span><span class="sxs-lookup"><span data-stu-id="fb070-176">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **X86**.</span></span>
* <span data-ttu-id="fb070-177">Cliquez sur la flèche déroulante en regard de ordinateur local, puis sélectionnez **périphérique distant**.</span><span class="sxs-lookup"><span data-stu-id="fb070-177">Click on the drop-down arrow next to Local Machine, and select **Remote Device**.</span></span>
    * <span data-ttu-id="fb070-178">Définissez l' **adresse** sur le nom ou l’adresse IP de votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="fb070-178">Set the **Address** to the name or IP address of your HoloLens.</span></span> <span data-ttu-id="fb070-179">Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées** ou demandez à Cortana **«Hey Cortana, qu’est-ce que mon adresse IP?»**</span><span class="sxs-lookup"><span data-stu-id="fb070-179">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options** or ask Cortana **"Hey Cortana, What's my IP address?"**</span></span>
    * <span data-ttu-id="fb070-180">Laissez le **mode d’authentification** défini sur **universel**.</span><span class="sxs-lookup"><span data-stu-id="fb070-180">Leave the **Authentication Mode** set to **Universal**.</span></span>
    * <span data-ttu-id="fb070-181">Cliquez sur **Sélectionner**</span><span class="sxs-lookup"><span data-stu-id="fb070-181">Click **Select**</span></span>
* <span data-ttu-id="fb070-182">Cliquez sur déboguer **> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="fb070-182">Click **Debug > Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="fb070-183">S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le coupler à [Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span><span class="sxs-lookup"><span data-stu-id="fb070-183">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span></span>
* <span data-ttu-id="fb070-184">Placez sur HoloLens et recherchez l’hologramme EnergyHub.</span><span class="sxs-lookup"><span data-stu-id="fb070-184">Put on your HoloLens and find the EnergyHub hologram.</span></span>

## <a name="chapter-2---interaction"></a><span data-ttu-id="fb070-185">Chapitre 2-interaction</span><span class="sxs-lookup"><span data-stu-id="fb070-185">Chapter 2 - Interaction</span></span>

>[!VIDEO https://www.youtube.com/embed/W60xG15a8gc]

<span data-ttu-id="fb070-186">Dans ce chapitre, nous interagissons avec nos hologrammes.</span><span class="sxs-lookup"><span data-stu-id="fb070-186">In this chapter, we'll interact with our holograms.</span></span> <span data-ttu-id="fb070-187">Tout d’abord, nous allons ajouter un curseur pour visualiser notre point de [regard](gaze.md).</span><span class="sxs-lookup"><span data-stu-id="fb070-187">First, we'll add a cursor to visualize our [Gaze](gaze.md).</span></span> <span data-ttu-id="fb070-188">Ensuite, nous ajouterons des [gestes](gestures.md) et utilisons notre main pour placer nos hologrammes dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="fb070-188">Then, we'll add [Gestures](gestures.md) and use our hand to place our holograms in space.</span></span>

### <a name="objectives"></a><span data-ttu-id="fb070-189">Objectifs</span><span class="sxs-lookup"><span data-stu-id="fb070-189">Objectives</span></span>

* <span data-ttu-id="fb070-190">Utilisez l’entrée de regard pour contrôler un curseur.</span><span class="sxs-lookup"><span data-stu-id="fb070-190">Use gaze input to control a cursor.</span></span>
* <span data-ttu-id="fb070-191">Utilisez l’entrée de mouvement pour interagir avec des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="fb070-191">Use gesture input to interact with holograms.</span></span>

### <a name="instructions"></a><span data-ttu-id="fb070-192">Instructions</span><span class="sxs-lookup"><span data-stu-id="fb070-192">Instructions</span></span>

<span data-ttu-id="fb070-193">**Pointage du regard**</span><span class="sxs-lookup"><span data-stu-id="fb070-193">**Gaze**</span></span>
* <span data-ttu-id="fb070-194">Dans le **volet de hiérarchie** , sélectionnez l’objet **HologramCollection** .</span><span class="sxs-lookup"><span data-stu-id="fb070-194">In the **Hierarchy panel** select the **HologramCollection** object.</span></span>
* <span data-ttu-id="fb070-195">Dans le **volet** de l’inspecteur, cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="fb070-195">In the **Inspector panel** click the **Add Component** button.</span></span>
* <span data-ttu-id="fb070-196">Dans le menu, tapez dans la zone de recherche **Gestionnaire de regard**.</span><span class="sxs-lookup"><span data-stu-id="fb070-196">In the menu, type in the search box **Gaze Manager**.</span></span> <span data-ttu-id="fb070-197">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fb070-197">Select the search result.</span></span>
* <span data-ttu-id="fb070-198">Dans le dossier **HoloToolkit-Sharing-240\Prefabs\Input** , recherchez la ressource **curseur** .</span><span class="sxs-lookup"><span data-stu-id="fb070-198">In the **HoloToolkit-Sharing-240\Prefabs\Input** folder, find the **Cursor** asset.</span></span>
* <span data-ttu-id="fb070-199">Faites glisser et déposez la ressource **curseur** dans la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="fb070-199">Drag and drop the **Cursor** asset onto the **Hierarchy**.</span></span>

<span data-ttu-id="fb070-200">**Mouvement**</span><span class="sxs-lookup"><span data-stu-id="fb070-200">**Gesture**</span></span>
* <span data-ttu-id="fb070-201">Dans le **volet de hiérarchie** , sélectionnez l’objet **HologramCollection** .</span><span class="sxs-lookup"><span data-stu-id="fb070-201">In the **Hierarchy panel** select the **HologramCollection** object.</span></span>
* <span data-ttu-id="fb070-202">Cliquez sur **Ajouter un composant** et tapez gestionnaire de **mouvements** dans le champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="fb070-202">Click **Add Component** and type **Gesture Manager** in the search field.</span></span> <span data-ttu-id="fb070-203">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fb070-203">Select the search result.</span></span>
* <span data-ttu-id="fb070-204">Dans le **volet hiérarchie**, développez **HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="fb070-204">In the **Hierarchy panel**, expand **HologramCollection**.</span></span>
* <span data-ttu-id="fb070-205">Sélectionnez l’objet **EnergyHub** enfant.</span><span class="sxs-lookup"><span data-stu-id="fb070-205">Select the child **EnergyHub** object.</span></span>
* <span data-ttu-id="fb070-206">Dans le **volet** de l’inspecteur, cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="fb070-206">In the **Inspector panel** click the **Add Component** button.</span></span>
* <span data-ttu-id="fb070-207">Dans le menu, tapez dans la zone de recherche placement de l' **hologramme**.</span><span class="sxs-lookup"><span data-stu-id="fb070-207">In the menu, type in the search box **Hologram Placement**.</span></span> <span data-ttu-id="fb070-208">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fb070-208">Select the search result.</span></span>
* <span data-ttu-id="fb070-209">Enregistrez la scène en sélectionnant **fichier > enregistrer la scène**.</span><span class="sxs-lookup"><span data-stu-id="fb070-209">Save the scene by selecting **File > Save Scene**.</span></span>

<span data-ttu-id="fb070-210">**Déployer et apprécier**</span><span class="sxs-lookup"><span data-stu-id="fb070-210">**Deploy and enjoy**</span></span>
* <span data-ttu-id="fb070-211">Créez et déployez sur votre HoloLens, en suivant les instructions du chapitre précédent.</span><span class="sxs-lookup"><span data-stu-id="fb070-211">Build and deploy to your HoloLens, using the instructions from the previous chapter.</span></span>
* <span data-ttu-id="fb070-212">Une fois l’application lancée sur votre HoloLens, déplacez votre tête et notez la façon dont la EnergyHub suit votre point de regard.</span><span class="sxs-lookup"><span data-stu-id="fb070-212">Once the app launches on your HoloLens, move your head around and notice how the EnergyHub follows your gaze.</span></span>
* <span data-ttu-id="fb070-213">Notez que le curseur s’affiche lorsque vous pointez sur l’hologramme et qu’il passe à une lumière de point lorsque vous n’êtes pas Gazing à un hologramme.</span><span class="sxs-lookup"><span data-stu-id="fb070-213">Notice how the cursor appears when you gaze upon the hologram, and changes to a point light when not gazing at a hologram.</span></span>
* <span data-ttu-id="fb070-214">Effectuez un TAP-Air pour placer l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="fb070-214">Perform an air-tap to place the hologram.</span></span> <span data-ttu-id="fb070-215">À ce stade de notre projet, vous ne pouvez placer l’hologramme qu’une seule fois (redéployer pour réessayer).</span><span class="sxs-lookup"><span data-stu-id="fb070-215">At this time in our project, you can only place the hologram once (redeploy to try again).</span></span>

## <a name="chapter-3---shared-coordinates"></a><span data-ttu-id="fb070-216">Chapitre 3-coordonnées partagées</span><span class="sxs-lookup"><span data-stu-id="fb070-216">Chapter 3 - Shared Coordinates</span></span>

>[!VIDEO https://www.youtube.com/embed/Ey8yBgWiqtg]

<span data-ttu-id="fb070-217">Il est amusant de voir et d’interagir avec les hologrammes, mais nous allons aller plus loin.</span><span class="sxs-lookup"><span data-stu-id="fb070-217">It's fun to see and interact with holograms, but let's go further.</span></span> <span data-ttu-id="fb070-218">Nous allons configurer notre première expérience partagée: un hologramme tout le monde peut le voir ensemble.</span><span class="sxs-lookup"><span data-stu-id="fb070-218">We'll set up our first shared experience - a hologram everyone can see together.</span></span>

### <a name="objectives"></a><span data-ttu-id="fb070-219">Objectifs</span><span class="sxs-lookup"><span data-stu-id="fb070-219">Objectives</span></span>

* <span data-ttu-id="fb070-220">Configurez un réseau pour une expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="fb070-220">Setup a network for a shared experience.</span></span>
* <span data-ttu-id="fb070-221">Établissez un point de référence commun.</span><span class="sxs-lookup"><span data-stu-id="fb070-221">Establish a common reference point.</span></span>
* <span data-ttu-id="fb070-222">Partager des systèmes de coordonnées entre les appareils.</span><span class="sxs-lookup"><span data-stu-id="fb070-222">Share coordinate systems across devices.</span></span>
* <span data-ttu-id="fb070-223">Tout le monde voit le même hologramme!</span><span class="sxs-lookup"><span data-stu-id="fb070-223">Everyone sees the same hologram!</span></span>

>[!NOTE]
><span data-ttu-id="fb070-224">Les fonctionnalités **InternetClientServer** et **PrivateNetworkClientServer** doivent être déclarées pour qu’une application se connecte au serveur de partage.</span><span class="sxs-lookup"><span data-stu-id="fb070-224">The **InternetClientServer** and **PrivateNetworkClientServer** capabilities must be declared for an app to connect to the sharing server.</span></span> <span data-ttu-id="fb070-225">Cela est fait pour vous déjà dans les hologrammes 240, mais gardez cela à l’esprit pour vos propres projets.</span><span class="sxs-lookup"><span data-stu-id="fb070-225">This is done for you already in Holograms 240, but keep this in mind for your own projects.</span></span>
>1. <span data-ttu-id="fb070-226">Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à «modifier les paramètres du projet > > Player».</span><span class="sxs-lookup"><span data-stu-id="fb070-226">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player"</span></span>
>2. <span data-ttu-id="fb070-227">Cliquer sur l’onglet «Windows Store»</span><span class="sxs-lookup"><span data-stu-id="fb070-227">Click on the "Windows Store" tab</span></span>
>3. <span data-ttu-id="fb070-228">Dans la section «fonctionnalités de > des paramètres de publication», vérifiez la capacité de **InternetClientServer** et la capacité de **PrivateNetworkClientServer**</span><span class="sxs-lookup"><span data-stu-id="fb070-228">In the "Publishing Settings > Capabilities" section, check the **InternetClientServer** capability and the **PrivateNetworkClientServer** capability</span></span>

### <a name="instructions"></a><span data-ttu-id="fb070-229">Instructions</span><span class="sxs-lookup"><span data-stu-id="fb070-229">Instructions</span></span>

* <span data-ttu-id="fb070-230">Dans le **panneau Projet** , accédez au dossier **HoloToolkit-Sharing-240\Prefabs\Sharing** .</span><span class="sxs-lookup"><span data-stu-id="fb070-230">In the **Project panel** navigate to the **HoloToolkit-Sharing-240\Prefabs\Sharing** folder.</span></span>
* <span data-ttu-id="fb070-231">Faites glisser et déposez le Prefab de **partage** dans le **panneau de hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="fb070-231">Drag and drop the **Sharing** prefab into the **Hierarchy panel**.</span></span>

<span data-ttu-id="fb070-232">Nous devons ensuite lancer le service de partage.</span><span class="sxs-lookup"><span data-stu-id="fb070-232">Next we need to launch the sharing service.</span></span> <span data-ttu-id="fb070-233">**Un seul ordinateur** de l’expérience partagée doit effectuer cette étape.</span><span class="sxs-lookup"><span data-stu-id="fb070-233">Only **one PC** in the shared experience needs to do this step.</span></span>
* <span data-ttu-id="fb070-234">Dans Unity, dans le menu de niveau supérieur, sélectionnez le **menu HoloToolkit-Sharing-240**.</span><span class="sxs-lookup"><span data-stu-id="fb070-234">In Unity - in the top-hand menu - select the **HoloToolkit-Sharing-240 menu**.</span></span>
* <span data-ttu-id="fb070-235">Sélectionnez l’élément **Démarrer le partage de service** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="fb070-235">Select the **Launch Sharing Service** item in the drop-down.</span></span>
* <span data-ttu-id="fb070-236">Cochez l’option **réseau privé** , puis cliquez sur **autoriser l’accès** lorsque l’invite de pare-feu s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fb070-236">Check the **Private Network** option and click **Allow Access** when the firewall prompt appears.</span></span>
* <span data-ttu-id="fb070-237">Notez l’adresse IPv4 affichée dans la fenêtre de console du service de partage.</span><span class="sxs-lookup"><span data-stu-id="fb070-237">Note down the IPv4 address displayed in the Sharing Service console window.</span></span> <span data-ttu-id="fb070-238">Il s’agit de la même adresse IP que la machine sur laquelle le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fb070-238">This is the same IP as the machine the service is being run on.</span></span>

<span data-ttu-id="fb070-239">Suivez le reste des instructions sur **tous les PC** qui vont rejoindre l’expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="fb070-239">Follow the rest of the instructions on **all PCs** that will join the shared experience.</span></span>
* <span data-ttu-id="fb070-240">Dans la **hiérarchie**, sélectionnez l’objet de **partage** .</span><span class="sxs-lookup"><span data-stu-id="fb070-240">In the **Hierarchy**, select the **Sharing** object.</span></span>
* <span data-ttu-id="fb070-241">Dans l' **inspecteur**, sur le composant **étape de partage** , remplacez l’adresse du **serveur** «localhost» par l’adresse IPv4 de l’ordinateur exécutant SharingService. exe.</span><span class="sxs-lookup"><span data-stu-id="fb070-241">In the **Inspector**, on the **Sharing Stage** component, change the **Server Address** from 'localhost' to the IPv4 address of the machine running SharingService.exe.</span></span>
* <span data-ttu-id="fb070-242">Dans la **hiérarchie** , sélectionnez l’objet **HologramCollection** .</span><span class="sxs-lookup"><span data-stu-id="fb070-242">In the **Hierarchy** select the **HologramCollection** object.</span></span>
* <span data-ttu-id="fb070-243">Dans l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="fb070-243">In the **Inspector** click the **Add Component** button.</span></span>
* <span data-ttu-id="fb070-244">Dans la zone de recherche, tapez **Import exporter Anchor Manager**.</span><span class="sxs-lookup"><span data-stu-id="fb070-244">In the search box, type **Import Export Anchor Manager**.</span></span> <span data-ttu-id="fb070-245">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fb070-245">Select the search result.</span></span>
* <span data-ttu-id="fb070-246">Dans le **panneau Projet** , accédez au dossier **scripts** .</span><span class="sxs-lookup"><span data-stu-id="fb070-246">In the **Project panel** navigate to the **Scripts** folder.</span></span>
* <span data-ttu-id="fb070-247">Double-cliquez sur le script **HologramPlacement** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb070-247">Double-click the **HologramPlacement** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="fb070-248">Remplacez le contenu par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fb070-248">Replace the contents with the code below.</span></span>

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

* <span data-ttu-id="fb070-249">De retour dans Unity, sélectionnez le **HologramCollection** dans le panneau de la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="fb070-249">Back in Unity, select the **HologramCollection** in the **Hierarchy panel**.</span></span>
* <span data-ttu-id="fb070-250">Dans le **volet** de l’inspecteur, cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="fb070-250">In the **Inspector panel** click the **Add Component** button.</span></span>
* <span data-ttu-id="fb070-251">Dans le menu, tapez dans la zone de recherche **Gestionnaire d’état des applications**.</span><span class="sxs-lookup"><span data-stu-id="fb070-251">In the menu, type in the search box **App State Manager**.</span></span> <span data-ttu-id="fb070-252">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fb070-252">Select the search result.</span></span>

<span data-ttu-id="fb070-253">**Déployer et apprécier**</span><span class="sxs-lookup"><span data-stu-id="fb070-253">**Deploy and enjoy**</span></span>
* <span data-ttu-id="fb070-254">Générez le projet pour vos appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="fb070-254">Build the project for your HoloLens devices.</span></span>
* <span data-ttu-id="fb070-255">Désignez un HoloLens à déployer au préalable.</span><span class="sxs-lookup"><span data-stu-id="fb070-255">Designate one HoloLens to deploy to first.</span></span> <span data-ttu-id="fb070-256">Vous devez attendre que le point d’ancrage soit téléchargé vers le service avant de pouvoir placer le EnergyHub (cette opération peut prendre environ 30-60 secondes).</span><span class="sxs-lookup"><span data-stu-id="fb070-256">You will need to wait for the Anchor to be uploaded to the service before you can place the EnergyHub (this can take ~30-60 seconds).</span></span> <span data-ttu-id="fb070-257">Tant que le téléchargement n’est pas terminé, vos gestes TAP seront ignorés.</span><span class="sxs-lookup"><span data-stu-id="fb070-257">Until the upload is done, your tap gestures will be ignored.</span></span>
* <span data-ttu-id="fb070-258">Une fois que le EnergyHub a été placé, son emplacement est chargé sur le service et vous pouvez le déployer sur tous les autres appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="fb070-258">After the EnergyHub has been placed, its location will be uploaded to the service and you can then deploy to all other HoloLens devices.</span></span>
* <span data-ttu-id="fb070-259">Quand un nouveau HoloLens rejoint pour la première fois dans la session, l’emplacement du EnergyHub peut ne pas être correct sur cet appareil.</span><span class="sxs-lookup"><span data-stu-id="fb070-259">When a new HoloLens first joins the session, the location of the EnergyHub may not be correct on that device.</span></span> <span data-ttu-id="fb070-260">Toutefois, dès que les emplacements d’ancrage et de EnergyHub ont été téléchargés à partir du service, le EnergyHub doit accéder au nouvel emplacement partagé.</span><span class="sxs-lookup"><span data-stu-id="fb070-260">However, as soon as the anchor and EnergyHub locations have been downloaded from the service, the EnergyHub should jump to the new, shared location.</span></span> <span data-ttu-id="fb070-261">Si cela ne se produit pas dans un délai de environ 30-60 secondes, passez à l’emplacement de l’HoloLens d’origine lors de la définition de l’ancre pour obtenir davantage d’indices d’environnement.</span><span class="sxs-lookup"><span data-stu-id="fb070-261">If this does not happen within ~30-60 seconds, walk to where the original HoloLens was when setting the anchor to gather more environment clues.</span></span> <span data-ttu-id="fb070-262">Si l’emplacement ne verrouille toujours pas, redéployez sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="fb070-262">If the location still does not lock on, redeploy to the device.</span></span>
* <span data-ttu-id="fb070-263">Une fois que les appareils sont prêts et que vous exécutez l’application, recherchez EnergyHub.</span><span class="sxs-lookup"><span data-stu-id="fb070-263">When the devices are all ready and running the app, look for the EnergyHub.</span></span> <span data-ttu-id="fb070-264">Pouvez-vous tous les accepter sur l’emplacement de l’hologramme et la direction dans laquelle le texte est dirigé?</span><span class="sxs-lookup"><span data-stu-id="fb070-264">Can you all agree on the hologram's location and which direction the text is facing?</span></span>

## <a name="chapter-4---discovery"></a><span data-ttu-id="fb070-265">Chapitre 4-détection</span><span class="sxs-lookup"><span data-stu-id="fb070-265">Chapter 4 - Discovery</span></span>

>[!VIDEO https://www.youtube.com/embed/5NxJWMV4BP8]

<span data-ttu-id="fb070-266">Tout le monde peut désormais Voir le même hologramme!</span><span class="sxs-lookup"><span data-stu-id="fb070-266">Everyone can now see the same hologram!</span></span> <span data-ttu-id="fb070-267">Voyons à présent tous les autres utilisateurs connectés à notre environnement holographique partagé.</span><span class="sxs-lookup"><span data-stu-id="fb070-267">Now let's see everyone else connected to our shared holographic world.</span></span> <span data-ttu-id="fb070-268">Dans ce chapitre, nous allons récupérer l’emplacement et la rotation de tous les autres appareils HoloLens dans la même session de partage.</span><span class="sxs-lookup"><span data-stu-id="fb070-268">In this chapter, we'll grab the head location and rotation of all other HoloLens devices in the same sharing session.</span></span>

### <a name="objectives"></a><span data-ttu-id="fb070-269">Objectifs</span><span class="sxs-lookup"><span data-stu-id="fb070-269">Objectives</span></span>

* <span data-ttu-id="fb070-270">Découvrez les autres dans notre expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="fb070-270">Discover each other in our shared experience.</span></span>
* <span data-ttu-id="fb070-271">Choisissez et partagez un avatar de joueur.</span><span class="sxs-lookup"><span data-stu-id="fb070-271">Choose and share a player avatar.</span></span>
* <span data-ttu-id="fb070-272">Attachez l’avatar du joueur à côté de tout le monde.</span><span class="sxs-lookup"><span data-stu-id="fb070-272">Attach the player avatar next to everyone's heads.</span></span>

### <a name="instructions"></a><span data-ttu-id="fb070-273">Instructions</span><span class="sxs-lookup"><span data-stu-id="fb070-273">Instructions</span></span>

* <span data-ttu-id="fb070-274">Dans le **panneau Projet** , accédez au  dossier hologrammes.</span><span class="sxs-lookup"><span data-stu-id="fb070-274">In the **Project panel** navigate to the **Holograms** folder.</span></span>
* <span data-ttu-id="fb070-275">Glissez-déplacez le **PlayerAvatarStore** dans la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="fb070-275">Drag and drop the **PlayerAvatarStore** into the **Hierarchy**.</span></span>
* <span data-ttu-id="fb070-276">Dans le **panneau Projet** , accédez au dossier **scripts** .</span><span class="sxs-lookup"><span data-stu-id="fb070-276">In the **Project panel** navigate to the **Scripts** folder.</span></span>
* <span data-ttu-id="fb070-277">Double-cliquez sur le script **AvatarSelector** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb070-277">Double-click the **AvatarSelector** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="fb070-278">Remplacez le contenu par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fb070-278">Replace the contents with the code below.</span></span>

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

* <span data-ttu-id="fb070-279">Dans la **hiérarchie** , sélectionnez l’objet **HologramCollection** .</span><span class="sxs-lookup"><span data-stu-id="fb070-279">In the **Hierarchy** select the **HologramCollection** object.</span></span>
* <span data-ttu-id="fb070-280">Dans l' **inspecteur** , cliquez sur **Ajouter un composant**.</span><span class="sxs-lookup"><span data-stu-id="fb070-280">In the **Inspector** click **Add Component**.</span></span>
* <span data-ttu-id="fb070-281">Dans la zone de recherche, tapez **Gestionnaire de lecteur local**.</span><span class="sxs-lookup"><span data-stu-id="fb070-281">In the search box, type **Local Player Manager**.</span></span> <span data-ttu-id="fb070-282">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fb070-282">Select the search result.</span></span>
* <span data-ttu-id="fb070-283">Dans la **hiérarchie** , sélectionnez l’objet **HologramCollection** .</span><span class="sxs-lookup"><span data-stu-id="fb070-283">In the **Hierarchy** select the **HologramCollection** object.</span></span>
* <span data-ttu-id="fb070-284">Dans l' **inspecteur** , cliquez sur **Ajouter un composant**.</span><span class="sxs-lookup"><span data-stu-id="fb070-284">In the **Inspector** click **Add Component**.</span></span>
* <span data-ttu-id="fb070-285">Dans la zone de recherche, tapez **Gestionnaire de lecteur distant**.</span><span class="sxs-lookup"><span data-stu-id="fb070-285">In the search box, type **Remote Player Manager**.</span></span> <span data-ttu-id="fb070-286">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fb070-286">Select the search result.</span></span>
* <span data-ttu-id="fb070-287">Ouvrez le script **HologramPlacement** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb070-287">Open the **HologramPlacement** script in Visual Studio.</span></span>
* <span data-ttu-id="fb070-288">Remplacez le contenu par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fb070-288">Replace the contents with the code below.</span></span>

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

* <span data-ttu-id="fb070-289">Ouvrez le script **AppStateManager** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb070-289">Open the **AppStateManager** script in Visual Studio.</span></span>
* <span data-ttu-id="fb070-290">Remplacez le contenu par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fb070-290">Replace the contents with the code below.</span></span>

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

<span data-ttu-id="fb070-291">**Déployer et apprécier**</span><span class="sxs-lookup"><span data-stu-id="fb070-291">**Deploy and Enjoy**</span></span>
* <span data-ttu-id="fb070-292">Générez et déployez le projet sur vos appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="fb070-292">Build and deploy the project to your HoloLens devices.</span></span>
* <span data-ttu-id="fb070-293">Quand vous entendez un son de ping, recherchez le menu de sélection d’avatar et sélectionnez un avatar avec le geste de pression d’air.</span><span class="sxs-lookup"><span data-stu-id="fb070-293">When you hear a pinging sound, find the avatar selection menu and select an avatar with the air-tap gesture.</span></span>
* <span data-ttu-id="fb070-294">Si vous n’êtes pas en train de regarder des hologrammes, la lumière du point autour de votre curseur permet de changer de couleur quand votre HoloLens communique avec le service: initialisation (violet foncé), téléchargement de l’ancre (vert), importation/exportation des données d’emplacement (jaune), chargement de l’ancre (bleu).</span><span class="sxs-lookup"><span data-stu-id="fb070-294">If you're not looking at any holograms, the point light around your cursor will turn a different color when your HoloLens is communicating with the service: initializing (dark purple), downloading the anchor (green), importing/exporting location data (yellow), uploading the anchor (blue).</span></span> <span data-ttu-id="fb070-295">Si votre lumière de point autour de votre curseur est la couleur par défaut (violet clair), vous êtes prêt à interagir avec les autres joueurs de votre session.</span><span class="sxs-lookup"><span data-stu-id="fb070-295">If your point light around your cursor is the default color (light purple), then you are ready to interact with other players in your session!</span></span>
* <span data-ttu-id="fb070-296">Regardez les autres personnes connectées à votre espace-un robot holographique flotte au-dessus de son épaule et imitant ses mouvements de tête!</span><span class="sxs-lookup"><span data-stu-id="fb070-296">Look at other people connected to your space - there will be a holographic robot floating above their shoulder and mimicking their head motions!</span></span>

## <a name="chapter-5---placement"></a><span data-ttu-id="fb070-297">Chapitre 5-placement</span><span class="sxs-lookup"><span data-stu-id="fb070-297">Chapter 5 - Placement</span></span>

>[!VIDEO https://www.youtube.com/embed/afFTwHQIw0s]

<span data-ttu-id="fb070-298">Dans ce chapitre, nous allons faire en sorte que l’ancre puisse être placée sur des surfaces réelles.</span><span class="sxs-lookup"><span data-stu-id="fb070-298">In this chapter, we'll make the anchor able to be placed on real-world surfaces.</span></span> <span data-ttu-id="fb070-299">Nous allons utiliser des coordonnées partagées pour placer cette ancre dans le point central entre tout le monde connecté à l’expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="fb070-299">We'll use shared coordinates to place that anchor in the middle point between everyone connected to the shared experience.</span></span>

### <a name="objectives"></a><span data-ttu-id="fb070-300">Objectifs</span><span class="sxs-lookup"><span data-stu-id="fb070-300">Objectives</span></span>

* <span data-ttu-id="fb070-301">Placez les hologrammes sur la carte spatiale en fonction de la position de tête des joueurs.</span><span class="sxs-lookup"><span data-stu-id="fb070-301">Place holograms on the spatial map based on players’ head position.</span></span>

### <a name="instructions"></a><span data-ttu-id="fb070-302">Instructions</span><span class="sxs-lookup"><span data-stu-id="fb070-302">Instructions</span></span>

* <span data-ttu-id="fb070-303">Dans le **panneau Projet** , accédez au  dossier hologrammes.</span><span class="sxs-lookup"><span data-stu-id="fb070-303">In the **Project panel** navigate to the **Holograms** folder.</span></span>
* <span data-ttu-id="fb070-304">Glissez-déplacez le Prefab **CustomSpatialMapping** sur la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="fb070-304">Drag and drop the **CustomSpatialMapping** prefab onto the **Hierarchy**.</span></span>
* <span data-ttu-id="fb070-305">Dans le **panneau Projet** , accédez au dossier **scripts** .</span><span class="sxs-lookup"><span data-stu-id="fb070-305">In the **Project panel** navigate to the **Scripts** folder.</span></span>
* <span data-ttu-id="fb070-306">Double-cliquez sur le script **AppStateManager** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb070-306">Double-click the **AppStateManager** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="fb070-307">Remplacez le contenu par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fb070-307">Replace the contents with the code below.</span></span>

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

* <span data-ttu-id="fb070-308">Dans le **panneau Projet** , accédez au dossier **scripts** .</span><span class="sxs-lookup"><span data-stu-id="fb070-308">In the **Project panel** navigate to the **Scripts** folder.</span></span>
* <span data-ttu-id="fb070-309">Double-cliquez sur le script **HologramPlacement** pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb070-309">Double-click the **HologramPlacement** script to open it in Visual Studio.</span></span>
* <span data-ttu-id="fb070-310">Remplacez le contenu par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fb070-310">Replace the contents with the code below.</span></span>

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

<span data-ttu-id="fb070-311">**Déployer et apprécier**</span><span class="sxs-lookup"><span data-stu-id="fb070-311">**Deploy and enjoy**</span></span>
* <span data-ttu-id="fb070-312">Générez et déployez le projet sur vos appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="fb070-312">Build and deploy the project to your HoloLens devices.</span></span>
* <span data-ttu-id="fb070-313">Lorsque l’application est prête, mettez-la dans un cercle et observez la façon dont le EnergyHub apparaît au centre de tout le monde.</span><span class="sxs-lookup"><span data-stu-id="fb070-313">When the app is ready, stand in a circle and notice how the EnergyHub appears in the center of everyone.</span></span>
* <span data-ttu-id="fb070-314">Appuyez pour placer le EnergyHub.</span><span class="sxs-lookup"><span data-stu-id="fb070-314">Tap to place the EnergyHub.</span></span>
* <span data-ttu-id="fb070-315">Essayez la commande vocale «réinitialiser la cible» pour sélectionner le EnergyHub de sauvegarde et travailler ensemble en tant que groupe pour déplacer l’hologramme vers un nouvel emplacement.</span><span class="sxs-lookup"><span data-stu-id="fb070-315">Try the voice command 'Reset Target' to pick the EnergyHub back up and work together as a group to move the hologram to a new location.</span></span>

## <a name="chapter-6---real-world-physics"></a><span data-ttu-id="fb070-316">Chapitre 6-physique réel</span><span class="sxs-lookup"><span data-stu-id="fb070-316">Chapter 6 - Real-World Physics</span></span>

>[!VIDEO https://www.youtube.com/embed/XNpQVSyXwMo]

<span data-ttu-id="fb070-317">Dans ce chapitre, nous allons ajouter des hologrammes qui rebondissent sur des surfaces réelles.</span><span class="sxs-lookup"><span data-stu-id="fb070-317">In this chapter we'll add holograms that bounce off real-world surfaces.</span></span> <span data-ttu-id="fb070-318">Regardez votre espace plein avec les projets lancés par vous et vos amis!</span><span class="sxs-lookup"><span data-stu-id="fb070-318">Watch your space fill up with projects launched by both you and your friends!</span></span>

### <a name="objectives"></a><span data-ttu-id="fb070-319">Objectifs</span><span class="sxs-lookup"><span data-stu-id="fb070-319">Objectives</span></span>

* <span data-ttu-id="fb070-320">Lancez des projectiles qui rebondissent sur des surfaces réelles.</span><span class="sxs-lookup"><span data-stu-id="fb070-320">Launch projectiles that bounce off real-world surfaces.</span></span>
* <span data-ttu-id="fb070-321">Partagez les projectiles afin que d’autres joueurs puissent les voir.</span><span class="sxs-lookup"><span data-stu-id="fb070-321">Share the projectiles so other players can see them.</span></span>

### <a name="instructions"></a><span data-ttu-id="fb070-322">Instructions</span><span class="sxs-lookup"><span data-stu-id="fb070-322">Instructions</span></span>

* <span data-ttu-id="fb070-323">Dans la **hiérarchie** , sélectionnez l’objet **HologramCollection** .</span><span class="sxs-lookup"><span data-stu-id="fb070-323">In the **Hierarchy** select the **HologramCollection** object.</span></span>
* <span data-ttu-id="fb070-324">Dans l' **inspecteur** , cliquez sur **Ajouter un composant**.</span><span class="sxs-lookup"><span data-stu-id="fb070-324">In the **Inspector** click **Add Component**.</span></span>
* <span data-ttu-id="fb070-325">Dans la zone de recherche, tapez lanceur de projectiles.</span><span class="sxs-lookup"><span data-stu-id="fb070-325">In the search box, type **Projectile Launcher**.</span></span> <span data-ttu-id="fb070-326">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fb070-326">Select the search result.</span></span>

<span data-ttu-id="fb070-327">**Déployer et apprécier**</span><span class="sxs-lookup"><span data-stu-id="fb070-327">**Deploy and enjoy**</span></span>
* <span data-ttu-id="fb070-328">Créez et déployez sur vos appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="fb070-328">Build and deploy to your HoloLens devices.</span></span>
* <span data-ttu-id="fb070-329">Lorsque l’application est en cours d’exécution sur tous les appareils, effectuez un taraudage pour lancer un projectile à des surfaces réelles.</span><span class="sxs-lookup"><span data-stu-id="fb070-329">When the app is running on all devices, perform an air-tap to launch projectile at real world surfaces.</span></span>
* <span data-ttu-id="fb070-330">Voyez ce qui se passe lorsque votre projectile entre en conflit avec un avatar d’un joueur!</span><span class="sxs-lookup"><span data-stu-id="fb070-330">See what happens when your projectile collides with another player's avatar!</span></span>

## <a name="chapter-7---grand-finale"></a><span data-ttu-id="fb070-331">Chapitre 7-finalisation général</span><span class="sxs-lookup"><span data-stu-id="fb070-331">Chapter 7 - Grand Finale</span></span>

>[!VIDEO https://www.youtube.com/embed/kDUPUvZEqRg]

<span data-ttu-id="fb070-332">Dans ce chapitre, nous allons découvrir un portail qui peut être découvert uniquement avec la collaboration.</span><span class="sxs-lookup"><span data-stu-id="fb070-332">In this chapter, we'll uncover a portal that can only be discovered with collaboration.</span></span>

### <a name="objectives"></a><span data-ttu-id="fb070-333">Objectifs</span><span class="sxs-lookup"><span data-stu-id="fb070-333">Objectives</span></span>

* <span data-ttu-id="fb070-334">Collaborez pour lancer suffisamment de projectiles à l’ancre pour découvrir un portail de secret.</span><span class="sxs-lookup"><span data-stu-id="fb070-334">Work together to launch enough projectiles at the anchor to uncover a secret portal!</span></span>

### <a name="instructions"></a><span data-ttu-id="fb070-335">Instructions</span><span class="sxs-lookup"><span data-stu-id="fb070-335">Instructions</span></span>

* <span data-ttu-id="fb070-336">Dans le **panneau Projet** , accédez au  dossier hologrammes.</span><span class="sxs-lookup"><span data-stu-id="fb070-336">In the **Project panel** navigate to the **Holograms** folder.</span></span>
* <span data-ttu-id="fb070-337">Faites glisser et déposez la ressource de sous- **monde** en tant qu' **enfant de HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="fb070-337">Drag and drop the **Underworld** asset as a **child of HologramCollection**.</span></span>
* <span data-ttu-id="fb070-338">Avec **HologramCollection** sélectionné, cliquez sur le bouton **Ajouter un composant** dans l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="fb070-338">With **HologramCollection** selected, click the **Add Component** button in the **Inspector**.</span></span>
* <span data-ttu-id="fb070-339">Dans le menu, tapez dans la zone de recherche **ExplodeTarget**.</span><span class="sxs-lookup"><span data-stu-id="fb070-339">In the menu, type in the search box **ExplodeTarget**.</span></span> <span data-ttu-id="fb070-340">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fb070-340">Select the search result.</span></span>
* <span data-ttu-id="fb070-341">Avec **HologramCollection** sélectionné, dans la **hiérarchie** , faites glisser l’objet **EnergyHub** vers le champ **cible** de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="fb070-341">With **HologramCollection** selected, from the **Hierarchy** drag the **EnergyHub** object to the **Target** field in the **Inspector**.</span></span>
* <span data-ttu-id="fb070-342">Lorsque **HologramCollection** est sélectionné, dans la **hiérarchie** , faites glisser l’objet «sous- **monde** » vers le champ «sous- **monde** » de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="fb070-342">With **HologramCollection** selected, from the **Hierarchy** drag the **Underworld** object to the **Underworld** field in the **Inspector**.</span></span>

<span data-ttu-id="fb070-343">**Déployer et apprécier**</span><span class="sxs-lookup"><span data-stu-id="fb070-343">**Deploy and enjoy**</span></span>
* <span data-ttu-id="fb070-344">Créez et déployez sur vos appareils HoloLens.</span><span class="sxs-lookup"><span data-stu-id="fb070-344">Build and deploy to your HoloLens devices.</span></span>
* <span data-ttu-id="fb070-345">Lorsque l’application a démarré, collaborez pour lancer des projectiles au EnergyHub.</span><span class="sxs-lookup"><span data-stu-id="fb070-345">When the app has launched, collaborate together to launch projectiles at the EnergyHub.</span></span>
* <span data-ttu-id="fb070-346">Quand le sous-monde s’affiche, lancez des projectiles chez les robots du sous-monde (un robot se trouve trois fois plus amusant).</span><span class="sxs-lookup"><span data-stu-id="fb070-346">When the underworld appears, launch projectiles at underworld robots (hit a robot three times for extra fun).</span></span>
