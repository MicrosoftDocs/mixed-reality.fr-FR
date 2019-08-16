---
title: Monsieur le son spatial 220-spatial
description: Suivez cette procédure pas à pas de codage à l’aide de Unity, Visual Studio et HoloLens pour apprendre les concepts de son spatial.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, Academy, didacticiel, son spatial
ms.openlocfilehash: 50d17fe8c9a6e3f18b1309a59c9c41af982a7505
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63526930"
---
>[!NOTE]
><span data-ttu-id="ad7ff-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="ad7ff-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="ad7ff-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="ad7ff-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="ad7ff-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="ad7ff-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-spatial-220-spatial-sound"></a><span data-ttu-id="ad7ff-110">Monsieur spatial 220: Son spatial</span><span class="sxs-lookup"><span data-stu-id="ad7ff-110">MR Spatial 220: Spatial sound</span></span>

<span data-ttu-id="ad7ff-111">Le [son spatial](spatial-sound.md) passe par des hologrammes et leur donne la présence dans notre monde.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-111">[Spatial sound](spatial-sound.md) breathes life into holograms and gives them presence in our world.</span></span> <span data-ttu-id="ad7ff-112">Les hologrammes sont composés de la lumière et du son, et si vous perdez la vision de vos hologrammes, le son spatial peut vous aider à les trouver.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-112">Holograms are composed of both light and sound, and if you happen to lose sight of your holograms, spatial sound can help you find them.</span></span> <span data-ttu-id="ad7ff-113">Le son spatial n’est pas comme le son classique que vous entendez sur la radio, il s’agit d’un son positionné dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-113">Spatial sound is not like the typical sound that you would hear on the radio, it is sound that is positioned in 3D space.</span></span> <span data-ttu-id="ad7ff-114">Avec un son spatial, vous pouvez faire en sorte que les hologrammes s’affichent derrière vous, en regard de vous ou même en tête.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-114">With spatial sound, you can make holograms sound like they're behind you, next to you, or even on your head!</span></span> <span data-ttu-id="ad7ff-115">Dans ce cours, vous allez:</span><span class="sxs-lookup"><span data-stu-id="ad7ff-115">In this course, you will:</span></span>

* <span data-ttu-id="ad7ff-116">Configurez votre environnement de développement pour utiliser le son spatial Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-116">Configure your development environment to use Microsoft Spatial Sound.</span></span>
* <span data-ttu-id="ad7ff-117">Utilisez le son spatial pour améliorer les interactions.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-117">Use Spatial Sound to enhance interactions.</span></span>
* <span data-ttu-id="ad7ff-118">Utilisez le son spatial conjointement avec le mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-118">Use Spatial Sound in conjunction with Spatial Mapping.</span></span>
* <span data-ttu-id="ad7ff-119">Comprendre la conception et la combinaison des meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-119">Understand sound design and mixing best practices.</span></span>
* <span data-ttu-id="ad7ff-120">Utilisez le son pour améliorer les effets spéciaux et amener l’utilisateur dans le monde de la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-120">Use sound to enhance special effects and bring the user into the Mixed Reality world.</span></span>

## <a name="device-support"></a><span data-ttu-id="ad7ff-121">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="ad7ff-121">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="ad7ff-122">Course</span><span class="sxs-lookup"><span data-stu-id="ad7ff-122">Course</span></span></th><th style="width:150px"> <span data-ttu-id="ad7ff-123"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="ad7ff-123"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="ad7ff-124"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="ad7ff-124"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="ad7ff-125">Monsieur spatial 220: Son spatial</span><span class="sxs-lookup"><span data-stu-id="ad7ff-125">MR Spatial 220: Spatial sound</span></span></td><td style="text-align: center;"> <span data-ttu-id="ad7ff-126">✔️</span><span class="sxs-lookup"><span data-stu-id="ad7ff-126">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="ad7ff-127">✔️</span><span class="sxs-lookup"><span data-stu-id="ad7ff-127">✔️</span></span></td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="ad7ff-128">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="ad7ff-128">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ad7ff-129">Prérequis</span><span class="sxs-lookup"><span data-stu-id="ad7ff-129">Prerequisites</span></span>

* <span data-ttu-id="ad7ff-130">Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-130">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="ad7ff-131">Certaines fonctionnalités C# de programmation de base.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-131">Some basic C# programming ability.</span></span>
* <span data-ttu-id="ad7ff-132">Vous devez avoir terminé les [notions de base de m. 101](holograms-101.md).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-132">You should have completed [MR Basics 101](holograms-101.md).</span></span>
* <span data-ttu-id="ad7ff-133">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-133">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="ad7ff-134">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="ad7ff-134">Project files</span></span>

* <span data-ttu-id="ad7ff-135">Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-220-SpatialSound.zip) requis par le projet.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-135">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-220-SpatialSound.zip) required by the project.</span></span><span data-ttu-id="ad7ff-136"> Requiert Unity 2017,2 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-136"> Requires Unity 2017.2 or later.</span></span>
  * <span data-ttu-id="ad7ff-137">Si vous avez encore besoin de la prise en charge d’Unity 5,6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-220.zip).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-137">If you still need Unity 5.6 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-220.zip).</span></span> <span data-ttu-id="ad7ff-138">Cette version n’est peut-être plus à jour.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-138">This release may no longer be up-to-date.</span></span>
  * <span data-ttu-id="ad7ff-139">Si vous avez encore besoin de la prise en charge d’Unity 5,5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-220.zip).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-139">If you still need Unity 5.5 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-220.zip).</span></span><span data-ttu-id="ad7ff-140"> Cette version n’est peut-être plus à jour.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-140"> This release may no longer be up-to-date.</span></span>
  * <span data-ttu-id="ad7ff-141">Si vous avez encore besoin de la prise en charge d’Unity 5,4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-220.zip).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-141">If you still need Unity 5.4 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-220.zip).</span></span><span data-ttu-id="ad7ff-142"> Cette version n’est peut-être plus à jour.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-142"> This release may no longer be up-to-date.</span></span>
* <span data-ttu-id="ad7ff-143">Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-143">Un-archive the files to your desktop or other easy to reach location.</span></span>

>[!NOTE]
><span data-ttu-id="ad7ff-144">Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-220-SpatialSound).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-144">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-220-SpatialSound).</span></span>

### <a name="errata-and-notes"></a><span data-ttu-id="ad7ff-145">Errata et notes</span><span class="sxs-lookup"><span data-stu-id="ad7ff-145">Errata and Notes</span></span>

* <span data-ttu-id="ad7ff-146">L’option «Activer Uniquement mon code» doit être désactivée (décochée) dans Visual Studio sous Outils-> Options-> le débogage pour atteindre les points d’arrêt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-146">"Enable Just My Code" needs to be disabled (*unchecked*) in Visual Studio under Tools->Options->Debugging in order to hit breakpoints in your code.</span></span>

## <a name="chapter-1---unity-setup"></a><span data-ttu-id="ad7ff-147">Chapitre 1-Configuration Unity</span><span class="sxs-lookup"><span data-stu-id="ad7ff-147">Chapter 1 - Unity Setup</span></span>

### <a name="objectives"></a><span data-ttu-id="ad7ff-148">Objectifs</span><span class="sxs-lookup"><span data-stu-id="ad7ff-148">Objectives</span></span>

* <span data-ttu-id="ad7ff-149">Modifiez la configuration du son de l’unité pour utiliser un son spatial Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-149">Change Unity's sound configuration to use Microsoft Spatial Sound.</span></span>
* <span data-ttu-id="ad7ff-150">Ajoutez du son 3D à un objet dans Unity.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-150">Add 3D sound to an object in Unity.</span></span>

### <a name="instructions"></a><span data-ttu-id="ad7ff-151">Instructions</span><span class="sxs-lookup"><span data-stu-id="ad7ff-151">Instructions</span></span>

* <span data-ttu-id="ad7ff-152">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-152">Start Unity.</span></span>
* <span data-ttu-id="ad7ff-153">Sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-153">Select **Open**.</span></span>
* <span data-ttu-id="ad7ff-154">Accédez à votre bureau et recherchez le dossier que vous avez précédemment désinstallé.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-154">Navigate to your Desktop and find the folder you previously un-archived.</span></span>
* <span data-ttu-id="ad7ff-155">Cliquez sur le dossier **Starting\Decibel** , puis appuyez sur le bouton **Sélectionner un dossier** .</span><span class="sxs-lookup"><span data-stu-id="ad7ff-155">Click on the **Starting\Decibel** folder and then press the **Select Folder** button.</span></span>
* <span data-ttu-id="ad7ff-156">Attendez que le projet se charge dans Unity.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-156">Wait for the project to load in Unity.</span></span>
* <span data-ttu-id="ad7ff-157">Dans le panneau **projet** , ouvrez **Scenes\Decibel.Unity**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-157">In the **Project** panel, open **Scenes\Decibel.unity**.</span></span>
* <span data-ttu-id="ad7ff-158">Dans le volet **hiérarchie** , développez **HologramCollection** , puis sélectionnez **P0LY**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-158">In the **Hierarchy** panel, expand **HologramCollection** and select **P0LY**.</span></span>
* <span data-ttu-id="ad7ff-159">Dans l’inspecteur, développez **audiosource** et Notez qu’il n’y a pas de case à cocher **spatialiser** .</span><span class="sxs-lookup"><span data-stu-id="ad7ff-159">In the Inspector, expand **AudioSource** and notice that there is no **Spatialize** check box.</span></span>

<span data-ttu-id="ad7ff-160">Par défaut, Unity ne charge pas de plug-in Spatializer.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-160">By default, Unity does not load a spatializer plugin.</span></span> <span data-ttu-id="ad7ff-161">Les étapes suivantes permettent d’activer le son spatial dans le projet.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-161">The following steps will enable Spatial Sound in the project.</span></span>

* <span data-ttu-id="ad7ff-162">Dans le menu supérieur de Unity, accédez à **modifier > paramètres du projet > audio**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-162">In Unity's top menu, go to **Edit > Project Settings > Audio**.</span></span>
* <span data-ttu-id="ad7ff-163">Recherchez la liste déroulante du **plug-in Spatializer** , puis sélectionnez **MS HRTF Spatializer**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-163">Find the **Spatializer Plugin** dropdown, and select **MS HRTF Spatializer**.</span></span>
* <span data-ttu-id="ad7ff-164">Dans le volet **hiérarchie** , sélectionnez **HologramCollection > P0LY**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-164">In the **Hierarchy** panel, select **HologramCollection > P0LY**.</span></span>
* <span data-ttu-id="ad7ff-165">Dans le panneau **inspecteur** , recherchez le composant **audio source** .</span><span class="sxs-lookup"><span data-stu-id="ad7ff-165">In the **Inspector** panel, find the **Audio Source** component.</span></span>
* <span data-ttu-id="ad7ff-166">Cochez la case spatialiser.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-166">Check the **Spatialize** checkbox.</span></span>
* <span data-ttu-id="ad7ff-167">Faites glisser le curseur de **lissage spatial** jusqu’à la forme **3D**, ou entrez **1** dans la zone d’édition.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-167">Drag the **Spatial Blend** slider all the way to **3D**, or enter **1** in the edit box.</span></span>

<span data-ttu-id="ad7ff-168">Nous allons maintenant générer le projet dans Unity et configurer la solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-168">We will now build the project in Unity and configure the solution in Visual Studio.</span></span>

1. <span data-ttu-id="ad7ff-169">Dans Unity, sélectionnez **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-169">In Unity, select **File > Build Settings**.</span></span>
2. <span data-ttu-id="ad7ff-170">Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-170">Click **Add Open Scenes** to add the scene.</span></span>
3. <span data-ttu-id="ad7ff-171">Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur basculer la **plateforme**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-171">Select **Universal Windows Platform** in the **Platform** list and click **Switch Platform**.</span></span>
4. <span data-ttu-id="ad7ff-172">Si vous développez spécifiquement pour HoloLens, définissez **appareil cible** sur **hololens**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-172">If you're specifically developing for HoloLens, set **Target device** to **HoloLens**.</span></span> <span data-ttu-id="ad7ff-173">Dans le cas contraire, laissez-le sur **un appareil**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-173">Otherwise, leave it on **Any device**.</span></span>
5. <span data-ttu-id="ad7ff-174">Vérifiez que le **type de build** est défini sur **D3D** et que le **Kit de développement logiciel (SDK** ) est défini sur le **dernier installé** (qui doit être le SDK 16299 ou une version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-174">Ensure **Build Type** is set to **D3D** and **SDK** is set to **Latest installed** (which should be SDK 16299 or newer).</span></span>
6. <span data-ttu-id="ad7ff-175">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-175">Click **Build**.</span></span>
7. <span data-ttu-id="ad7ff-176">Créez un **dossier** nommé «App».</span><span class="sxs-lookup"><span data-stu-id="ad7ff-176">Create a **New Folder** named "App".</span></span>
8. <span data-ttu-id="ad7ff-177">Cliquez sur le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="ad7ff-177">Single click the **App** folder.</span></span>
9. <span data-ttu-id="ad7ff-178">Appuyez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-178">Press **Select Folder**.</span></span>

<span data-ttu-id="ad7ff-179">Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-179">When Unity is done, a File Explorer window will appear.</span></span>

1. <span data-ttu-id="ad7ff-180">Ouvrez le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="ad7ff-180">Open the **App** folder.</span></span>
2. <span data-ttu-id="ad7ff-181">Ouvrez la **solution Visual Studio décibels**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-181">Open the **Decibel Visual Studio Solution**.</span></span>

<span data-ttu-id="ad7ff-182">En cas de déploiement dans HoloLens:</span><span class="sxs-lookup"><span data-stu-id="ad7ff-182">If deploying to HoloLens:</span></span>

1. <span data-ttu-id="ad7ff-183">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-183">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x86**.</span></span>
2. <span data-ttu-id="ad7ff-184">Cliquez sur la flèche déroulante en regard du bouton ordinateur local, puis sélectionnez **ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-184">Click on the drop down arrow next to the Local Machine button, and select **Remote Machine**.</span></span>
3. <span data-ttu-id="ad7ff-185">Entrez **l’adresse IP de votre appareil HoloLens** et définissez le mode d’authentification sur **universel (protocole non chiffré)** .</span><span class="sxs-lookup"><span data-stu-id="ad7ff-185">Enter **your HoloLens device IP address** and set Authentication Mode to **Universal (Unencrypted Protocol)**.</span></span> <span data-ttu-id="ad7ff-186">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-186">Click **Select**.</span></span> <span data-ttu-id="ad7ff-187">Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-187">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options**.</span></span>
4. <span data-ttu-id="ad7ff-188">Dans la barre de menus supérieure, cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-188">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="ad7ff-189">S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le coupler à [Visual Studio](using-visual-studio.md#pairing-your-device---hololens-1st-gen).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-189">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device---hololens-1st-gen).</span></span>

<span data-ttu-id="ad7ff-190">En cas de déploiement sur un casque immersif:</span><span class="sxs-lookup"><span data-stu-id="ad7ff-190">If deploying to an immersive headset:</span></span>

1. <span data-ttu-id="ad7ff-191">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x64**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-191">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x64**.</span></span>
2. <span data-ttu-id="ad7ff-192">Assurez-vous que la cible de déploiement est définie sur **ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-192">Make sure the deployment target is set to **Local Machine**.</span></span>
3. <span data-ttu-id="ad7ff-193">Dans la barre de menus supérieure, cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-193">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>

## <a name="chapter-2---spatial-sound-and-interaction"></a><span data-ttu-id="ad7ff-194">Chapitre 2-sons spatiaux et interaction</span><span class="sxs-lookup"><span data-stu-id="ad7ff-194">Chapter 2 - Spatial Sound and Interaction</span></span>

### <a name="objectives"></a><span data-ttu-id="ad7ff-195">Objectifs</span><span class="sxs-lookup"><span data-stu-id="ad7ff-195">Objectives</span></span>

* <span data-ttu-id="ad7ff-196">Améliorez le réalisme des hologrammes à l’aide du son.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-196">Enhance hologram realism using sound.</span></span>
* <span data-ttu-id="ad7ff-197">Dirigez le point de regard de l’utilisateur à l’aide du son.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-197">Direct the user's gaze using sound.</span></span>
* <span data-ttu-id="ad7ff-198">Fournir des commentaires de mouvement en utilisant le son.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-198">Provide gesture feedback using sound.</span></span>

### <a name="part-1---enhancing-realism"></a><span data-ttu-id="ad7ff-199">Partie 1-amélioration du réalisme</span><span class="sxs-lookup"><span data-stu-id="ad7ff-199">Part 1 - Enhancing Realism</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="ad7ff-200">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="ad7ff-200">Key Concepts</span></span>

* <span data-ttu-id="ad7ff-201">Spatialer les sons hologrammes.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-201">Spatialize hologram sounds.</span></span>
* <span data-ttu-id="ad7ff-202">Les sources audio doivent être placées à un emplacement approprié sur l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-202">Sound sources should be placed at an appropriate location on the hologram.</span></span>

<span data-ttu-id="ad7ff-203">L’emplacement approprié pour le son va dépendre de l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-203">The appropriate location for the sound is going to depend on the hologram.</span></span> <span data-ttu-id="ad7ff-204">Par exemple, si l’hologramme est un homme, la source du son doit être située près de la bouche et non pas des pieds.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-204">For example, if the hologram is of a human, the sound source should be located near the mouth and not the feet.</span></span>

#### <a name="instructions"></a><span data-ttu-id="ad7ff-205">Instructions</span><span class="sxs-lookup"><span data-stu-id="ad7ff-205">Instructions</span></span>

<span data-ttu-id="ad7ff-206">Les instructions suivantes attachent un son spatial à un hologramme.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-206">The following instructions will attach a spatialized sound to a hologram.</span></span>

* <span data-ttu-id="ad7ff-207">Dans le volet **hiérarchie** , développez **HologramCollection** , puis sélectionnez **P0LY**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-207">In the **Hierarchy** panel, expand **HologramCollection** and select **P0LY**.</span></span>
* <span data-ttu-id="ad7ff-208">Dans le volet de l' **inspecteur** , dans le **audiosource**, cliquez sur le cercle en regard de **Audioclip** et sélectionnez polypointer dans la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-208">In the **Inspector** panel, in the **AudioSource**, click the circle next to **AudioClip** and select **PolyHover** from the pop-up.</span></span>
* <span data-ttu-id="ad7ff-209">Cliquez sur le cercle en regard de **sortie** et sélectionnez **SoundEffects** dans la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-209">Click the circle next to **Output** and select **SoundEffects** from the pop-up.</span></span>

<span data-ttu-id="ad7ff-210">Project décibel utilise un composant Unity **audiomixer** pour permettre l’ajustement des niveaux sonores pour les groupes de sons.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-210">Project Decibel uses a Unity **AudioMixer** component to enable adjusting sound levels for groups of sounds.</span></span> <span data-ttu-id="ad7ff-211">En regroupant les sons de cette manière, le volume global peut être ajusté tout en conservant le volume relatif de chaque son.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-211">By grouping sounds this way, the overall volume can be adjusted while maintaining the relative volume of each sound.</span></span>

* <span data-ttu-id="ad7ff-212">Dans le **audiosource**, développez **paramètres audio 3D**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-212">In the **AudioSource**, expand **3D Sound Settings**.</span></span>
* <span data-ttu-id="ad7ff-213">Affectez au **niveau Doppler** la valeur **0**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-213">Set **Doppler Level** to **0**.</span></span>

<span data-ttu-id="ad7ff-214">Le fait de définir le niveau Doppler sur zéro désactive les modifications du pas en raison du mouvement (de l’hologramme ou de l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-214">Setting Doppler level to zero disables changes in pitch caused by motion (either of the hologram or the user).</span></span> <span data-ttu-id="ad7ff-215">Un exemple classique de Doppler est un véhicule à déplacement rapide.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-215">A classic example of Doppler is a fast-moving car.</span></span> <span data-ttu-id="ad7ff-216">À mesure que la voiture approche un écouteur stationnaire, la hauteur du moteur augmente.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-216">As the car approaches a stationary listener, the pitch of the engine rises.</span></span> <span data-ttu-id="ad7ff-217">Lorsqu’il passe l’écouteur, le pas à pas est inférieur à la distance.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-217">When it passes the listener, the pitch lowers with distance.</span></span>

### <a name="part-2---directing-the-users-gaze"></a><span data-ttu-id="ad7ff-218">Partie 2: diriger le regard de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ad7ff-218">Part 2 - Directing the User's Gaze</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="ad7ff-219">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="ad7ff-219">Key Concepts</span></span>

* <span data-ttu-id="ad7ff-220">Utilisez le son pour attirer l’attention sur des hologrammes importants.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-220">Use sound to call attention to important holograms.</span></span>
* <span data-ttu-id="ad7ff-221">Les oreilles vous aident directement là où les yeux doivent ressembler.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-221">The ears help direct where the eyes should look.</span></span>
* <span data-ttu-id="ad7ff-222">Le cerveau a des attentes apprises.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-222">The brain has some learned expectations.</span></span>

<span data-ttu-id="ad7ff-223">Un exemple de l’expérience acquise est que les oiseaux sont généralement au-dessus des têtes des êtres humains.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-223">One example of learned expectations is that birds are generally above the heads of humans.</span></span> <span data-ttu-id="ad7ff-224">Si un utilisateur entend un son oiseau, sa réaction initiale est de rechercher.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-224">If a user hears a bird sound, their initial reaction is to look up.</span></span> <span data-ttu-id="ad7ff-225">Le fait de placer un oiseau au-dessous de l’utilisateur peut entraîner une direction correcte du son, mais ne parvient pas à trouver l’hologramme en raison de la nécessité d’effectuer des recherches.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-225">Placing a bird below the user can lead to them facing the correct direction of the sound, but being unable to find the hologram based on the expectation of needing to look up.</span></span>

#### <a name="instructions"></a><span data-ttu-id="ad7ff-226">Instructions</span><span class="sxs-lookup"><span data-stu-id="ad7ff-226">Instructions</span></span>

<span data-ttu-id="ad7ff-227">Les instructions suivantes permettent à P0LY de se masquer derrière vous, afin que vous puissiez utiliser le son pour localiser l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-227">The following instructions enable P0LY to hide behind you, so that you can use sound to locate the hologram.</span></span>

* <span data-ttu-id="ad7ff-228">Dans le volet **hiérarchie** , sélectionnez **gestionnaires**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-228">In the **Hierarchy** panel, select **Managers**.</span></span>
* <span data-ttu-id="ad7ff-229">Dans le panneau **inspecteur** , recherchez **Gestionnaire d’entrée vocale**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-229">In the **Inspector** panel, find **Speech Input Handler**.</span></span>
* <span data-ttu-id="ad7ff-230">Dans le **Gestionnaire d’entrée vocal**, développez **Go Hide**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-230">In **Speech Input Handler**, expand **Go Hide**.</span></span>
* <span data-ttu-id="ad7ff-231">**Ne modifiez aucune fonction** en polyactions **. GoHide**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-231">Change **No Function** to **PolyActions.GoHide**.</span></span>

![Mot Go masquer](images/gohide.png)

### <a name="part-3---gesture-feedback"></a><span data-ttu-id="ad7ff-233">Partie 3: commentaires sur les mouvements</span><span class="sxs-lookup"><span data-stu-id="ad7ff-233">Part 3 - Gesture Feedback</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="ad7ff-234">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="ad7ff-234">Key Concepts</span></span>

* <span data-ttu-id="ad7ff-235">Fournir à l’utilisateur une confirmation de mouvement positive à l’aide du son</span><span class="sxs-lookup"><span data-stu-id="ad7ff-235">Provide the user with positive gesture confirmation using sound</span></span>
* <span data-ttu-id="ad7ff-236">N’encombrez pas les sons trop bruyants de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ad7ff-236">Do not overwhelm the user - overly loud sounds get in the way</span></span>
* <span data-ttu-id="ad7ff-237">Les sons subtils fonctionnent mieux: ne assombrissent pas l’expérience</span><span class="sxs-lookup"><span data-stu-id="ad7ff-237">Subtle sounds work best - do not overshadow the experience</span></span>

#### <a name="instructions"></a><span data-ttu-id="ad7ff-238">Instructions</span><span class="sxs-lookup"><span data-stu-id="ad7ff-238">Instructions</span></span>

* <span data-ttu-id="ad7ff-239">Dans le volet **hiérarchie** , développez **HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-239">In the **Hierarchy** panel, expand **HologramCollection**.</span></span>
* <span data-ttu-id="ad7ff-240">Développez **EnergyHub** et sélectionnez **base**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-240">Expand **EnergyHub** and select **Base**.</span></span>
* <span data-ttu-id="ad7ff-241">Dans le panneau **inspecteur** , cliquez sur **Ajouter un composant** et ajouter un gestionnaire de sons de **geste**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-241">In the **Inspector** panel, click **Add Component** and add **Gesture Sound Handler**.</span></span>
* <span data-ttu-id="ad7ff-242">Dans **Gestionnaire de sons de geste**, cliquez sur le cercle en regard de l' **élément de navigation démarré** et de la **navigation mise à jour** , puis sélectionnez **RotateClick** dans la fenêtre contextuelle pour les deux.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-242">In **Gesture Sound Handler**, click the circle next to **Navigation Started Clip** and **Navigation Updated Clip** and select **RotateClick** from the pop-up for both.</span></span>
* <span data-ttu-id="ad7ff-243">Double-cliquez sur «GestureSoundHandler» pour charger dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-243">Double click on "GestureSoundHandler" to load in Visual Studio.</span></span>

<span data-ttu-id="ad7ff-244">Le gestionnaire de son geste effectue les tâches suivantes:</span><span class="sxs-lookup"><span data-stu-id="ad7ff-244">Gesture Sound Handler performs the following tasks:</span></span>

* <span data-ttu-id="ad7ff-245">Créez et configurez un **audiosource**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-245">Create and configure an **AudioSource**.</span></span>
* <span data-ttu-id="ad7ff-246">Placez le **audiosource** à l’emplacement du **gameobject**approprié.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-246">Place the **AudioSource** at the location of the appropriate **GameObject**.</span></span>
* <span data-ttu-id="ad7ff-247">Lit le **Audioclip** associé au geste.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-247">Plays the **AudioClip** associated with the gesture.</span></span>

#### <a name="build-and-deploy"></a><span data-ttu-id="ad7ff-248">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="ad7ff-248">Build and Deploy</span></span>

1. <span data-ttu-id="ad7ff-249">Dans Unity, sélectionnez **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-249">In Unity, select **File > Build Settings**.</span></span>
2. <span data-ttu-id="ad7ff-250">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-250">Click **Build**.</span></span>
3. <span data-ttu-id="ad7ff-251">Cliquez sur le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="ad7ff-251">Single click the **App** folder.</span></span>
4. <span data-ttu-id="ad7ff-252">Appuyez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-252">Press **Select Folder**.</span></span>

<span data-ttu-id="ad7ff-253">Vérifiez que la barre d’outils indique «version finale», «x86» ou «x64», et «périphérique distant».</span><span class="sxs-lookup"><span data-stu-id="ad7ff-253">Check that the Toolbar says "Release", "x86" or "x64", and "Remote Device".</span></span> <span data-ttu-id="ad7ff-254">Dans le cas contraire, il s’agit de l’instance de codage de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-254">If not, this is the coding instance of Visual Studio.</span></span> <span data-ttu-id="ad7ff-255">Vous devrez peut-être rouvrir la solution à partir du dossier de l’application.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-255">You may need to re-open the solution from the App folder.</span></span>

* <span data-ttu-id="ad7ff-256">Si vous y êtes invité, rechargez les fichiers projet.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-256">If prompted, reload the project files.</span></span>
* <span data-ttu-id="ad7ff-257">Comme précédemment, déployez à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-257">As before, deploy from Visual Studio.</span></span>

<span data-ttu-id="ad7ff-258">Une fois l’application déployée:</span><span class="sxs-lookup"><span data-stu-id="ad7ff-258">After the application is deployed:</span></span>

* <span data-ttu-id="ad7ff-259">Observez la façon dont le son change au fur et à mesure que vous vous déplacez autour de P0LY.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-259">Observe how the sound changes as you move around P0LY.</span></span>
* <span data-ttu-id="ad7ff-260">Dites *«Go Hide»* pour faire en sorte que P0LY se déplace vers un emplacement derrière vous.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-260">Say *"Go Hide"* to make P0LY move to a location behind you.</span></span> <span data-ttu-id="ad7ff-261">Recherchez-le par le son.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-261">Find it by the sound.</span></span>
* <span data-ttu-id="ad7ff-262">Pointez le regard de la base du hub d’énergie.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-262">Gaze at the base of the Energy Hub.</span></span> <span data-ttu-id="ad7ff-263">Appuyez et faites glisser vers la gauche ou vers la droite pour faire pivoter l’hologramme et notez la façon dont le bruit de clic confirme le mouvement.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-263">Tap and drag left or right to rotate the hologram and notice how the clicking sound confirms the gesture.</span></span>

<span data-ttu-id="ad7ff-264">Remarque : Un volet de texte s’affiche avec vous.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-264">Note: There is a text panel that will tag-along with you.</span></span> <span data-ttu-id="ad7ff-265">Elle contient les commandes vocales disponibles que vous pouvez utiliser tout au long de ce cours.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-265">This will contain the available voice commands that you can use throughout this course.</span></span>

## <a name="chapter-3---spatial-sound-and-spatial-mapping"></a><span data-ttu-id="ad7ff-266">Chapitre 3-sons spatiaux et mappage spatial</span><span class="sxs-lookup"><span data-stu-id="ad7ff-266">Chapter 3 - Spatial Sound and Spatial Mapping</span></span>

### <a name="objectives"></a><span data-ttu-id="ad7ff-267">Objectifs</span><span class="sxs-lookup"><span data-stu-id="ad7ff-267">Objectives</span></span>

* <span data-ttu-id="ad7ff-268">Confirmez l’interaction entre les hologrammes et le monde réel à l’aide du son.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-268">Confirm interaction between holograms and the real world using sound.</span></span>
* <span data-ttu-id="ad7ff-269">Occultait le son à l’aide du monde physique.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-269">Occlude sound using the physical world.</span></span>

### <a name="part-1---physical-world-interaction"></a><span data-ttu-id="ad7ff-270">Partie 1-interaction du monde physique</span><span class="sxs-lookup"><span data-stu-id="ad7ff-270">Part 1 - Physical World Interaction</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="ad7ff-271">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="ad7ff-271">Key Concepts</span></span>

* <span data-ttu-id="ad7ff-272">En général, les objets physiques font l’objet d’un bruit lorsqu’ils rencontrent une surface ou un autre objet.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-272">Physical objects generally make a sound when encountering a surface or another object.</span></span>
* <span data-ttu-id="ad7ff-273">Les sons doivent être contextuels dans l’expérience.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-273">Sounds should be context appropriate within the experience.</span></span>

<span data-ttu-id="ad7ff-274">Par exemple, la définition d’une tasse sur une table doit rendre un son plus calme que la suppression d’un Boulder sur un morceau de métal.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-274">For example, setting a cup on a table should make a quieter sound than dropping a boulder on a piece of metal.</span></span>

#### <a name="instructions"></a><span data-ttu-id="ad7ff-275">Instructions</span><span class="sxs-lookup"><span data-stu-id="ad7ff-275">Instructions</span></span>

* <span data-ttu-id="ad7ff-276">Dans le volet **hiérarchie** , développez **HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-276">In the **Hierarchy** panel, expand **HologramCollection**.</span></span>
* <span data-ttu-id="ad7ff-277">Développez **EnergyHub**, sélectionnez **base**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-277">Expand **EnergyHub**, select **Base**.</span></span>
* <span data-ttu-id="ad7ff-278">Dans le panneau **inspecteur** , cliquez sur **Ajouter un composant** et ajoutez **TAP pour placer le son et l’action**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-278">In the **Inspector** panel, click **Add Component** and add **Tap To Place With Sound and Action**.</span></span>
* <span data-ttu-id="ad7ff-279">**Appuyez pour placer le son et l’action**:</span><span class="sxs-lookup"><span data-stu-id="ad7ff-279">In **Tap To Place With Sound and Action**:</span></span>
  * <span data-ttu-id="ad7ff-280">Cochez **Placer le parent sur TAP**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-280">Check **Place Parent On Tap**.</span></span>
  * <span data-ttu-id="ad7ff-281">Définissez **son** emplacement sur **place**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-281">Set **Placement Sound** to **Place**.</span></span>
  * <span data-ttu-id="ad7ff-282">Définissez le **son de collecte** sur **Pick**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-282">Set **Pickup Sound** to **Pickup**.</span></span>
  * <span data-ttu-id="ad7ff-283">Appuyez sur le signe + dans le coin inférieur droit, sous à la fois **action de collecte** et **action de placement**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-283">Press the + in the bottom right under both **On Pickup Action** and **On Placement Action**.</span></span> <span data-ttu-id="ad7ff-284">Faites glisser EnergyHub à partir de la scène dans les champs **aucun (objet)** .</span><span class="sxs-lookup"><span data-stu-id="ad7ff-284">Drag EnergyHub from the scene into the **None (Object)** fields.</span></span>
    * <span data-ttu-id="ad7ff-285">Sous **action de cueillette**, cliquez sur **aucune fonction** -> **EnergyHubBase** -> **ResetAnimation**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-285">Under **On Pickup Action**, click on **No Function** -> **EnergyHubBase** -> **ResetAnimation**.</span></span>
    * <span data-ttu-id="ad7ff-286">Sous **action de placement**, cliquez sur **no Function** -> **EnergyHubBase** -> **onselect**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-286">Under **On Placement Action**, click on **No Function** -> **EnergyHubBase** -> **OnSelect**.</span></span>

![Appuyez pour placer le son et l’action](images/holograms220-taptoplace.png)

### <a name="part-2---sound-occlusion"></a><span data-ttu-id="ad7ff-288">Partie 2-occlusion sonore</span><span class="sxs-lookup"><span data-stu-id="ad7ff-288">Part 2 - Sound Occlusion</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="ad7ff-289">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="ad7ff-289">Key Concepts</span></span>

* <span data-ttu-id="ad7ff-290">Un son, comme Light, peut être bloqués.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-290">Sound, like light, can be occluded.</span></span>

<span data-ttu-id="ad7ff-291">Un exemple classique est un hall de concert.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-291">A classic example is a concert hall.</span></span> <span data-ttu-id="ad7ff-292">Lorsqu’un écouteur se trouve en dehors du Hall et que la porte est fermée, la musique est atténuée.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-292">When a listener is standing outside of the hall and the door is closed, the music sounds muffled.</span></span> <span data-ttu-id="ad7ff-293">Il y a également généralement une réduction du volume.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-293">There is also typically a reduction in volume.</span></span> <span data-ttu-id="ad7ff-294">Lorsque la porte est ouverte, le spectre complet du son est audible sur le volume réel.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-294">When the door is opened, the full spectrum of the sound is heard at the actual volume.</span></span> <span data-ttu-id="ad7ff-295">Les sons à fréquence élevée sont généralement absorbés plus que les fréquences basses.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-295">High frequency sounds are generally absorbed more than low frequencies.</span></span>

#### <a name="instructions"></a><span data-ttu-id="ad7ff-296">Instructions</span><span class="sxs-lookup"><span data-stu-id="ad7ff-296">Instructions</span></span>

* <span data-ttu-id="ad7ff-297">Dans le volet **hiérarchie** , développez **HologramCollection** , puis sélectionnez **P0LY**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-297">In the **Hierarchy** panel, expand **HologramCollection** and select **P0LY**.</span></span>
* <span data-ttu-id="ad7ff-298">Dans le panneau **inspecteur** , cliquez sur **Ajouter un composant** et ajouter un **émetteur audio**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-298">In the **Inspector** panel, click **Add Component** and add **Audio Emitter**.</span></span>

<span data-ttu-id="ad7ff-299">La classe d’émetteur audio fournit les fonctionnalités suivantes:</span><span class="sxs-lookup"><span data-stu-id="ad7ff-299">The Audio Emitter class provides the following features:</span></span>

* <span data-ttu-id="ad7ff-300">Restaure toutes les modifications apportées au volume du **audiosource**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-300">Restores any changes to the volume of the **AudioSource**.</span></span>
* <span data-ttu-id="ad7ff-301">Exécute un **physique. RaycastNonAlloc** à partir de la position de l’utilisateur dans la direction du **gameobject** auquel le **AudioEmitter** est attaché.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-301">Performs a **Physics.RaycastNonAlloc** from the user's position in the direction of the **GameObject** to which the **AudioEmitter** is attached.</span></span>

<span data-ttu-id="ad7ff-302">La méthode RaycastNonAlloc est utilisée comme optimisation des performances pour limiter les allocations, ainsi que le nombre de résultats retournés.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-302">The RaycastNonAlloc method is used as a performance optimization to limit allocations as well as the number of results returned.</span></span>

* <span data-ttu-id="ad7ff-303">Pour chaque **IAudioInfluencer** rencontré, appelle la méthode **ApplyEffect** .</span><span class="sxs-lookup"><span data-stu-id="ad7ff-303">For each **IAudioInfluencer** encountered, calls the **ApplyEffect** method.</span></span>
* <span data-ttu-id="ad7ff-304">Pour chaque **IAudioInfluencer** précédent qui n’est plus rencontré, appelez la méthode **RemoveEffect** .</span><span class="sxs-lookup"><span data-stu-id="ad7ff-304">For each previous **IAudioInfluencer** that is no longer encountered, call the **RemoveEffect** method.</span></span>

<span data-ttu-id="ad7ff-305">Notez que AudioEmitter met à jour les échelles de temps humaines, par opposition à des mises à jour par image.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-305">Note that AudioEmitter updates on human time scales, as opposed to on a per frame basis.</span></span> <span data-ttu-id="ad7ff-306">Cela est dû au fait que les êtres humains ne se déplacent pas suffisamment rapidement pour que l’effet doive être mis à jour plus fréquemment que chaque trimestre ou moitié de seconde.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-306">This is done because humans generally do not move fast enough for the effect to need to be updated more frequently than every quarter or half of a second.</span></span> <span data-ttu-id="ad7ff-307">Les hologrammes qui se téléportent rapidement d’un emplacement à un autre peuvent briser l’illusion.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-307">Holograms that teleport rapidly from one location to another can break the illusion.</span></span>

* <span data-ttu-id="ad7ff-308">Dans le volet **hiérarchie** , développez **HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-308">In the **Hierarchy** panel, expand **HologramCollection**.</span></span>
* <span data-ttu-id="ad7ff-309">Développez **EnergyHub** , puis sélectionnez **BlobOutside**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-309">Expand **EnergyHub** and select **BlobOutside**.</span></span>
* <span data-ttu-id="ad7ff-310">Dans le panneau **inspecteur** , cliquez sur **Ajouter un composant** et ajouter des **OCCLUDER audio**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-310">In the **Inspector** panel, click **Add Component** and add **Audio Occluder**.</span></span>
* <span data-ttu-id="ad7ff-311">Dans **OCCLUDER audio**, définissez la **fréquence de coupure** sur **1500**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-311">In **Audio Occluder**, set **Cutoff Frequency** to **1500**.</span></span>

<span data-ttu-id="ad7ff-312">Ce paramètre limite les fréquences AudioSource à 1500 Hz et inférieures.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-312">This setting limits the AudioSource frequencies to 1500 Hz and below.</span></span>

* <span data-ttu-id="ad7ff-313">Définissez **passage du volume** à **0,9**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-313">Set **Volume Pass Through** to **0.9**.</span></span>

<span data-ttu-id="ad7ff-314">Ce paramètre réduit le volume du AudioSource à 90% de son niveau actuel.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-314">This setting reduces the volume of the AudioSource to 90% of it's current level.</span></span>

<span data-ttu-id="ad7ff-315">L’audio OCCLUDER implémente IAudioInfluencer pour:</span><span class="sxs-lookup"><span data-stu-id="ad7ff-315">Audio Occluder implements IAudioInfluencer to:</span></span>

* <span data-ttu-id="ad7ff-316">Appliquez un effet d’occlusion à l’aide d’un **AudioLowPassFilter** qui est attaché à **audiosource** Managed buy the **AudioEmitter**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-316">Apply an occlusion effect using an **AudioLowPassFilter** which gets attached to the **AudioSource** managed buy the **AudioEmitter**.</span></span>
* <span data-ttu-id="ad7ff-317">Applique l’atténuation du volume à AudioSource.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-317">Applies volume attenuation to the AudioSource.</span></span>
* <span data-ttu-id="ad7ff-318">Désactive l’effet en définissant une fréquence de coupure neutre et en désactivant le filtre.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-318">Disables the effect by setting a neutral cutoff frequency and disabling the filter.</span></span>

<span data-ttu-id="ad7ff-319">La fréquence utilisée est neutre est 22 kHz (22000 Hz).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-319">The frequency used as neutral is 22 kHz (22000 Hz).</span></span> <span data-ttu-id="ad7ff-320">Cette fréquence a été choisie car elle se trouve au-dessus de la fréquence maximale nominale pouvant être entendue par l’oreille humaine, ce qui n’a aucun impact perceptible sur le son.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-320">This frequency was chosen due to it being above the nominal maximum frequency that can be heard by the human ear, this making no discernable impact to the sound.</span></span>

* <span data-ttu-id="ad7ff-321">Dans le volet **hiérarchie** , sélectionnez **SpatialMapping**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-321">In the **Hierarchy** panel, select **SpatialMapping**.</span></span>
* <span data-ttu-id="ad7ff-322">Dans le panneau **inspecteur** , cliquez sur **Ajouter un composant** et ajouter des **OCCLUDER audio**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-322">In the **Inspector** panel, click **Add Component** and add **Audio Occluder**.</span></span>
* <span data-ttu-id="ad7ff-323">Dans **OCCLUDER audio**, définissez la **fréquence de coupure** sur **750**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-323">In **Audio Occluder**, set **Cutoff Frequency** to **750**.</span></span>

<span data-ttu-id="ad7ff-324">Lorsque plusieurs Occluders se trouvent dans le chemin d’accès entre l’utilisateur et le **AudioEmitter**, la fréquence la plus faible est appliquée au filtre.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-324">When multiple occluders are in the path between the user and the **AudioEmitter**, the lowest frequency is applied to the filter.</span></span>

* <span data-ttu-id="ad7ff-325">Définissez **passage du volume** à **0,75**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-325">Set **Volume Pass Through** to **0.75**.</span></span>

<span data-ttu-id="ad7ff-326">Lorsque plusieurs Occluders se trouvent dans le chemin d’accès entre l’utilisateur et le **AudioEmitter**, le transfert de volume est appliqué de façon additive.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-326">When multiple occluders are in the path between the user and the **AudioEmitter**, the volume pass through is applied additively.</span></span>

* <span data-ttu-id="ad7ff-327">Dans le volet **hiérarchie** , sélectionnez **gestionnaires**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-327">In the **Hierarchy** panel, select **Managers**.</span></span>
* <span data-ttu-id="ad7ff-328">Dans le panneau **inspecteur** , développez **Gestionnaire d’entrée vocal**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-328">In the **Inspector** panel, expand **Speech Input Handler**.</span></span>
* <span data-ttu-id="ad7ff-329">Dans le **Gestionnaire d’entrée vocal**, développez **frais Go**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-329">In **Speech Input Handler**, expand **Go Charge**.</span></span>
* <span data-ttu-id="ad7ff-330">**Ne modifiez aucune fonction** en polyactions **. GoCharge**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-330">Change **No Function** to **PolyActions.GoCharge**.</span></span>

![Mot Facturation Go](images/gocharge.png)

* <span data-ttu-id="ad7ff-332">Développez-le **ici**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-332">Expand **Come Here**.</span></span>
* <span data-ttu-id="ad7ff-333">**Ne modifiez aucune fonction** en polyactions **. Comeback**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-333">Change **No Function** to **PolyActions.ComeBack**.</span></span>

![Mot Viens ici](images/comehere.png)

#### <a name="build-and-deploy"></a><span data-ttu-id="ad7ff-335">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="ad7ff-335">Build and Deploy</span></span>

* <span data-ttu-id="ad7ff-336">Comme précédemment, générez le projet dans Unity et déployez-le dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-336">As before, build the project in Unity and deploy in Visual Studio.</span></span>

<span data-ttu-id="ad7ff-337">Une fois l’application déployée:</span><span class="sxs-lookup"><span data-stu-id="ad7ff-337">After the application is deployed:</span></span>

* <span data-ttu-id="ad7ff-338">Dites *«Go Fact»* pour que P0LY entre dans le hub d’énergie.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-338">Say *"Go Charge"* to have P0LY enter the Energy Hub.</span></span>

<span data-ttu-id="ad7ff-339">Notez la modification du son.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-339">Note the change in the sound.</span></span> <span data-ttu-id="ad7ff-340">Le bruit doit être atténué et un peu plus calme.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-340">It should sound muffled and a little quieter.</span></span> <span data-ttu-id="ad7ff-341">Si vous êtes en mesure de vous positionner avec un mur ou un autre objet entre vous et le hub d’énergie, vous remarquerez un Muffling supplémentaire du son en raison de l’occlusion par le monde réel.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-341">If you are able to position yourself with a wall or other object between you and the Energy Hub, you should notice a further muffling of the sound due to the occlusion by the real world.</span></span>

* <span data-ttu-id="ad7ff-342">Dites *«venez ici»* pour que P0LY laisse le hub d’énergie et se positionne en face de vous.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-342">Say *"Come Here"* to have P0LY leave the Energy Hub and position itself in front of you.</span></span>

<span data-ttu-id="ad7ff-343">Notez que l’occlusion sonore est supprimée une fois que P0LY a quitté le hub d’énergie.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-343">Note that the sound occlusion is removed once P0LY exits the Energy Hub.</span></span> <span data-ttu-id="ad7ff-344">Si vous entendez encore des occlusions, P0LY peut être bloqués par le monde réel.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-344">If you are still hearing occlusion, P0LY may be occluded by the real world.</span></span> <span data-ttu-id="ad7ff-345">Essayez de vous assurer que vous disposez d’une ligne de vue claire sur P0LY.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-345">Try moving to ensure you have a clear line of sight to P0LY.</span></span>

### <a name="part-3---room-models"></a><span data-ttu-id="ad7ff-346">Partie 3-modèles Room</span><span class="sxs-lookup"><span data-stu-id="ad7ff-346">Part 3 - Room Models</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="ad7ff-347">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="ad7ff-347">Key Concepts</span></span>

* <span data-ttu-id="ad7ff-348">La taille de l’espace fournit des files d’attente subliminal qui contribuent à la localisation du son.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-348">The size of the space provides subliminal queues that contribute to sound localization.</span></span>
* <span data-ttu-id="ad7ff-349">Les modèles de salle sont définis par**audiosource**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-349">Room models are set per-**AudioSource**.</span></span>
* <span data-ttu-id="ad7ff-350">Le [MixedRealityToolkit pour Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity) fournit du code pour définir le modèle de salle.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-350">The [MixedRealityToolkit for Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity) provides code for setting the room model.</span></span>
* <span data-ttu-id="ad7ff-351">Pour les expériences de réalité mixte, sélectionnez le modèle de salle qui correspond le mieux à l’espace de monde réel.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-351">For Mixed Reality experiences, select the room model that best fits the real world space.</span></span>

<span data-ttu-id="ad7ff-352">Si vous créez un scénario de réalité virtuelle, sélectionnez le modèle de salle qui correspond le mieux à l’environnement virtuel.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-352">If you are creating a Virtual Reality scenario, select the room model that best fits the virtual environment.</span></span>

## <a name="chapter-4---sound-design"></a><span data-ttu-id="ad7ff-353">Chapitre 4-conception du son</span><span class="sxs-lookup"><span data-stu-id="ad7ff-353">Chapter 4 - Sound Design</span></span>

### <a name="objectives"></a><span data-ttu-id="ad7ff-354">Objectifs</span><span class="sxs-lookup"><span data-stu-id="ad7ff-354">Objectives</span></span>

* <span data-ttu-id="ad7ff-355">Comprendre les considérations relatives à la conception d’un son efficace.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-355">Understand considerations for effective sound design.</span></span>
* <span data-ttu-id="ad7ff-356">Apprenez à mélanger les techniques et les recommandations.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-356">Learn mixing techniques and guidelines.</span></span>

### <a name="part-1---sound-and-experience-design"></a><span data-ttu-id="ad7ff-357">Partie 1: conception du son et de l’expérience</span><span class="sxs-lookup"><span data-stu-id="ad7ff-357">Part 1 - Sound and Experience Design</span></span>

<span data-ttu-id="ad7ff-358">Cette section décrit les considérations et les recommandations relatives à la conception du son et de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-358">This section discusses key sound and experience design considerations and guidelines.</span></span>

#### <a name="normalize-all-sounds"></a><span data-ttu-id="ad7ff-359">Normaliser tous les sons</span><span class="sxs-lookup"><span data-stu-id="ad7ff-359">Normalize all sounds</span></span>

<span data-ttu-id="ad7ff-360">Cela évite d’avoir à utiliser un code de cas particulier pour ajuster les niveaux de volume par son, ce qui peut prendre du temps et limiter la possibilité de mettre à jour facilement des fichiers audio.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-360">This avoids the need for special case code to adjust volume levels per sound, which can be time consuming and limits the ability to easily update sound files.</span></span>

#### <a name="design-for-an-untethered-experience"></a><span data-ttu-id="ad7ff-361">Conception pour une expérience non attachée</span><span class="sxs-lookup"><span data-stu-id="ad7ff-361">Design for an untethered experience</span></span>

<span data-ttu-id="ad7ff-362">HoloLens est un ordinateur holographique entièrement contenu et non attaché.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-362">HoloLens is a fully contained, untethered holographic computer.</span></span> <span data-ttu-id="ad7ff-363">Vos utilisateurs peuvent et utiliseront vos expériences pendant le déplacement.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-363">Your users can and will use your experiences while moving.</span></span> <span data-ttu-id="ad7ff-364">Veillez à tester votre combinaison audio en vous.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-364">Be sure to test your audio mix by walking around.</span></span>

#### <a name="emit-sound-from-logical-locations-on-your-holograms"></a><span data-ttu-id="ad7ff-365">Émettre du son à partir d’emplacements logiques sur vos hologrammes</span><span class="sxs-lookup"><span data-stu-id="ad7ff-365">Emit sound from logical locations on your holograms</span></span>

<span data-ttu-id="ad7ff-366">Dans le monde réel, un chien n’est pas à l’écorce de sa queue et la voix d’un homme ne provient pas de ses pieds.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-366">In the real world, a dog does not bark from its tail and a human's voice does not come from his/her feet.</span></span> <span data-ttu-id="ad7ff-367">Évitez que vos sons émettent des parties inattendues de vos hologrammes.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-367">Avoid having your sounds emit from unexpected portions of your holograms.</span></span>

<span data-ttu-id="ad7ff-368">Pour les petits hologrammes, il est raisonnable d’émettre un son à partir du centre de la géométrie.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-368">For small holograms, it is reasonable to have sound emit from the center of the geometry.</span></span>

#### <a name="familiar-sounds-are-most-localizable"></a><span data-ttu-id="ad7ff-369">Les sons habituels sont plus localisables</span><span class="sxs-lookup"><span data-stu-id="ad7ff-369">Familiar sounds are most localizable</span></span>

<span data-ttu-id="ad7ff-370">La voix humaine et la musique sont très faciles à localiser.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-370">The human voice and music are very easy to localize.</span></span> <span data-ttu-id="ad7ff-371">Si quelqu’un appelle votre nom, vous pouvez déterminer très précisément le sens de la voix et à quel moment.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-371">If someone calls your name, you are able to very accurately determine from what direction the voice came and from how far away.</span></span> <span data-ttu-id="ad7ff-372">Les sons peu familiers sont plus difficiles à localiser.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-372">Short, unfamiliar sounds are harder to localize.</span></span>

#### <a name="be-cognizant-of-user-expectations"></a><span data-ttu-id="ad7ff-373">Être Cognizant des attentes de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ad7ff-373">Be cognizant of user expectations</span></span>

<span data-ttu-id="ad7ff-374">L’expérience de vie joue un rôle dans notre capacité à identifier l’emplacement d’un son.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-374">Life experience plays a part in our ability to identify the location of a sound.</span></span> <span data-ttu-id="ad7ff-375">C’est l’une des raisons pour lesquelles la voix humaine est particulièrement facile à localiser.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-375">This is one reason why the human voice is particularly easy to localize.</span></span> <span data-ttu-id="ad7ff-376">Il est important de connaître les attentes de vos utilisateurs lors de la mise en place de vos sons.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-376">It is important to be aware of your user's learned expectations when placing your sounds.</span></span>

<span data-ttu-id="ad7ff-377">Par exemple, quand quelqu’un entend un morceau d’oiseau, il recherche généralement des oiseaux au-dessus de la ligne de vue (volant ou dans une arborescence).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-377">For example, when someone hears a bird song they generally look up, as birds tend to be above the line of sight (flying or in a tree).</span></span> <span data-ttu-id="ad7ff-378">Il n’est pas rare pour un utilisateur d’activer la direction correcte d’un son, mais de regarder dans une mauvaise direction verticale et de devenir confus ou frustré lorsqu’ils ne parviennent pas à trouver l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-378">It is not uncommon for a user to turn in the correct direction of a sound, but look in the wrong vertical direction and become confused or frustrated when they are unable to find the hologram.</span></span>

#### <a name="avoid-hidden-emitters"></a><span data-ttu-id="ad7ff-379">Éviter les émetteurs masqués</span><span class="sxs-lookup"><span data-stu-id="ad7ff-379">Avoid hidden emitters</span></span>

<span data-ttu-id="ad7ff-380">Dans le monde réel, si nous entendons un son, nous pouvons généralement identifier l’objet qui émet le son.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-380">In the real world, if we hear a sound, we can generally identify the object that is emitting the sound.</span></span> <span data-ttu-id="ad7ff-381">Cela doit également être vrai dans vos expériences.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-381">This should also hold true in your experiences.</span></span> <span data-ttu-id="ad7ff-382">Il peut être très difficile pour les utilisateurs d’entendre un son, de savoir à quel endroit le son provient et de ne pas voir un objet.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-382">It can be very disconcerting for users to hear a sound, know from where the sound originates and be unable to see an object.</span></span>

<span data-ttu-id="ad7ff-383">Il existe quelques exceptions à cette règle.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-383">There are some exceptions to this guideline.</span></span> <span data-ttu-id="ad7ff-384">Par exemple, les sons ambiants tels que les crickets dans un champ n’ont pas besoin d’être visibles.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-384">For example, ambient sounds such as crickets in a field need not be visible.</span></span> <span data-ttu-id="ad7ff-385">L’expérience de vie nous permet de vous familiariser avec la source de ces sons sans avoir à le voir.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-385">Life experience gives us familiarity with the source of these sounds without the need to see it.</span></span>

### <a name="part-2---sound-mixing"></a><span data-ttu-id="ad7ff-386">Partie 2-mixage audio</span><span class="sxs-lookup"><span data-stu-id="ad7ff-386">Part 2 - Sound Mixing</span></span>

#### <a name="target-your-mix-for-70-volume-on-the-hololens"></a><span data-ttu-id="ad7ff-387">Ciblez votre combinaison pour 70% du volume sur le HoloLens</span><span class="sxs-lookup"><span data-stu-id="ad7ff-387">Target your mix for 70% volume on the HoloLens</span></span>

<span data-ttu-id="ad7ff-388">Les expériences de réalité mixte permettent de voir les hologrammes dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-388">Mixed Reality experiences allow holograms to be seen in the real world.</span></span> <span data-ttu-id="ad7ff-389">Ils doivent également permettre l’entendre des sons réels.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-389">They should also allow real world sounds to be heard.</span></span> <span data-ttu-id="ad7ff-390">Une cible de volume de 70% permet à l’utilisateur d’entendre le monde autour de lui et du son de votre expérience.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-390">A 70% volume target enables the user to hear the world around them along with the sound of your experience.</span></span>

#### <a name="hololens-at-100-volume-should-drown-out-external-sounds"></a><span data-ttu-id="ad7ff-391">HoloLens à 100% du volume doit être submergé de sons externes</span><span class="sxs-lookup"><span data-stu-id="ad7ff-391">HoloLens at 100% volume should drown out external sounds</span></span>

<span data-ttu-id="ad7ff-392">Un niveau de volume de 100% est similaire à une expérience de réalité virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-392">A volume level of 100% is akin to a Virtual Reality experience.</span></span> <span data-ttu-id="ad7ff-393">Visuellement, l’utilisateur est transporté vers un autre monde.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-393">Visually, the user is transported to a different world.</span></span> <span data-ttu-id="ad7ff-394">Il en va de même de la même façon audible.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-394">The same should hold true audibly.</span></span>

#### <a name="use-the-unity-audiomixer-to-adjust-categories-of-sounds"></a><span data-ttu-id="ad7ff-395">Utiliser Unity AudioMixer pour ajuster les catégories de sons</span><span class="sxs-lookup"><span data-stu-id="ad7ff-395">Use the Unity AudioMixer to adjust categories of sounds</span></span>

<span data-ttu-id="ad7ff-396">Lors de la conception de votre combinaison, il est souvent utile de créer des catégories de son et d’augmenter ou de réduire leur volume en tant qu’unité.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-396">When designing your mix, it is often helpful to create sound categories and have the ability to increase or decrease their volume as a unit.</span></span> <span data-ttu-id="ad7ff-397">Cela permet de conserver les niveaux relatifs de chaque son tout en permettant de modifier rapidement et facilement la combinaison globale.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-397">This retains the relative levels of each sound while enabling quick and easy changes to the overall mix.</span></span> <span data-ttu-id="ad7ff-398">Les catégories courantes incluent; effets sonores, ambiance, voix et musique en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-398">Common categories include; sound effects, ambience, voice overs and background music.</span></span>

#### <a name="mix-sounds-based-on-the-users-gaze"></a><span data-ttu-id="ad7ff-399">Mélanger des sons en fonction du point de regard de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ad7ff-399">Mix sounds based on the user's gaze</span></span>

<span data-ttu-id="ad7ff-400">Il peut souvent être utile de modifier la combinaison de sons dans votre expérience en fonction de l’endroit où un utilisateur est (ou n’est pas) à l’origine de la recherche.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-400">It can often be useful to change the sound mix in your experience based on where a user is (or is not) looking.</span></span> <span data-ttu-id="ad7ff-401">Une utilisation courante de cette technique consiste à réduire le volume des hologrammes qui se trouvent en dehors du cadre holographique pour permettre à l’utilisateur de se concentrer plus facilement sur les informations qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-401">One common use for this technique are to reduce the volume level for holograms that are outside of the Holographic Frame to make it easier for the user to focus on the information in front of them.</span></span> <span data-ttu-id="ad7ff-402">Une autre utilisation consiste à augmenter le volume d’un son pour attirer l’attention de l’utilisateur sur un événement important.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-402">Another use is to increase the volume of a sound to draw the user's attention to an important event.</span></span>

#### <a name="building-your-mix"></a><span data-ttu-id="ad7ff-403">Conception de votre combinaison</span><span class="sxs-lookup"><span data-stu-id="ad7ff-403">Building your mix</span></span>

<span data-ttu-id="ad7ff-404">Lors de la création de votre combinaison, il est recommandé de commencer par l’audio d’arrière-plan de votre expérience et d’ajouter des couches en fonction de leur importance.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-404">When building your mix, it is recommended to start with your experience's background audio and add layers based on importance.</span></span> <span data-ttu-id="ad7ff-405">Souvent, cela entraîne une couche plus forte que la précédente.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-405">Often, this results in each layer being louder than the previous.</span></span>

<span data-ttu-id="ad7ff-406">En imaginant votre combinaison comme un entonnoir inversé, avec les moins importants (et généralement les plus calmes) en bas, il est recommandé de structurer votre combinaison comme dans le diagramme suivant.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-406">Imagining your mix as an inverted funnel, with the least important (and generally quietest sounds) at the bottom, it is recommended to structure your mix similar to the following diagram.</span></span>

![Structure de combinaison de sons](images/soundlevels.png)

<span data-ttu-id="ad7ff-408">Les fonctionnalités vocales sont un scénario intéressant.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-408">Voice overs are an interesting scenario.</span></span> <span data-ttu-id="ad7ff-409">En fonction de l’expérience que vous créez, vous souhaiterez peut-être avoir un son stéréo (non localisé) ou pour spatialer votre voix.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-409">Based on the experience you are creating you may wish to have a stereo (not localized) sound or to spatialize your voice overs.</span></span> <span data-ttu-id="ad7ff-410">Deux expériences Microsoft publiées illustrent des exemples excellents de chaque scénario.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-410">Two Microsoft published experiences illustrate excellent examples of each scenario.</span></span>

<span data-ttu-id="ad7ff-411">[HoloTour](http://www.microsoft.com/store/p/holotour/9nblggh5pj87) utilise une voix stéréo.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-411">[HoloTour](http://www.microsoft.com/store/p/holotour/9nblggh5pj87) uses a stereo voice over.</span></span> <span data-ttu-id="ad7ff-412">Lorsque le narrateur décrit l’emplacement affiché, le son est cohérent et ne varie pas en fonction de la position de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-412">When the narrator is describing the location being viewed, the sound is consistent and does not vary based on the user's position.</span></span> <span data-ttu-id="ad7ff-413">Cela permet au narrateur de décrire la scène sans sortir des sons spatiaux de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-413">This enables the narrator to describe the scene without taking away from the spatialized sounds of the environment.</span></span>

<span data-ttu-id="ad7ff-414">[Fragments](https://www.microsoft.com/store/p/fragments/9nblggh5ggm8) utilise une voix spatialisée sous la forme d’un détective.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-414">[Fragments](https://www.microsoft.com/store/p/fragments/9nblggh5ggm8) utilizes a spatialized voice over in the form of a detective.</span></span> <span data-ttu-id="ad7ff-415">La voix du détective est utilisée pour attirer l’attention de l’utilisateur sur un indice important comme si un humain réel était dans la pièce.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-415">The detective's voice is used to help bring the user's attention to an important clue as if an actual human was in the room.</span></span> <span data-ttu-id="ad7ff-416">Cela permet un sens encore plus important de l’immersion dans l’expérience de résolution du mystère.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-416">This enables an even greater sense of immersion into the experience of solving the mystery.</span></span>

### <a name="part-3--performance"></a><span data-ttu-id="ad7ff-417">Partie 3-performances</span><span class="sxs-lookup"><span data-stu-id="ad7ff-417">Part 3 -Performance</span></span>

#### <a name="cpu-usage"></a><span data-ttu-id="ad7ff-418">Utilisation du processeur</span><span class="sxs-lookup"><span data-stu-id="ad7ff-418">CPU usage</span></span>

<span data-ttu-id="ad7ff-419">Lorsque vous utilisez un son spatial, 10-12 émetteurs consomment environ 12% du processeur.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-419">When using Spatial Sound, 10 - 12 emitters will consume approximately 12% of the CPU.</span></span>

#### <a name="stream-long-audio-files"></a><span data-ttu-id="ad7ff-420">Diffuser des fichiers audio longs</span><span class="sxs-lookup"><span data-stu-id="ad7ff-420">Stream long audio files</span></span>

<span data-ttu-id="ad7ff-421">Les données audio peuvent être volumineuses, en particulier aux taux d’échantillonnage courants (44,1 et 48 kHz).</span><span class="sxs-lookup"><span data-stu-id="ad7ff-421">Audio data can be large, especially at common sample rates (44.1 and 48 kHz).</span></span> <span data-ttu-id="ad7ff-422">Une règle générale est que les fichiers audio d’une durée supérieure à 5-10 secondes doivent être diffusés en continu pour réduire l’utilisation de la mémoire de l’application.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-422">A general rule is that audio files longer than 5 - 10 seconds should be streamed to reduce application memory usage.</span></span>

<span data-ttu-id="ad7ff-423">Dans Unity, vous pouvez marquer un fichier audio pour la diffusion en continu dans les paramètres d’importation du fichier.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-423">In Unity, you can mark an audio file for streaming in the file's import settings.</span></span>

![Paramètres d’importation audio](images/audioimportsettings.png)

## <a name="chapter-5---special-effects"></a><span data-ttu-id="ad7ff-425">Chapitre 5-effets spéciaux</span><span class="sxs-lookup"><span data-stu-id="ad7ff-425">Chapter 5 - Special Effects</span></span>

### <a name="objectives"></a><span data-ttu-id="ad7ff-426">Objectifs</span><span class="sxs-lookup"><span data-stu-id="ad7ff-426">Objectives</span></span>

* <span data-ttu-id="ad7ff-427">Ajoutez une profondeur à «Magic Windows».</span><span class="sxs-lookup"><span data-stu-id="ad7ff-427">Add depth to "Magic Windows".</span></span>
* <span data-ttu-id="ad7ff-428">Mettez l’utilisateur dans le monde virtuel.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-428">Bring the user into the virtual world.</span></span>

### <a name="magic-windows"></a><span data-ttu-id="ad7ff-429">Magic Windows</span><span class="sxs-lookup"><span data-stu-id="ad7ff-429">Magic Windows</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="ad7ff-430">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="ad7ff-430">Key Concepts</span></span>

* <span data-ttu-id="ad7ff-431">La création d’affichages dans un monde masqué, est visuellement attrayante.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-431">Creating views into a hidden world, is visually compelling.</span></span>
* <span data-ttu-id="ad7ff-432">Améliorez le réalisme en ajoutant des effets audio quand un hologramme ou l’utilisateur est proche du monde masqué.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-432">Enhance realism by adding audio effects when a hologram or the user is near the hidden world.</span></span>

#### <a name="instructions"></a><span data-ttu-id="ad7ff-433">Instructions</span><span class="sxs-lookup"><span data-stu-id="ad7ff-433">Instructions</span></span>

* <span data-ttu-id="ad7ff-434">Dans le volet **hiérarchie** , développez **HologramCollection** , puis sélectionnez subworld.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-434">In the **Hierarchy** panel, expand **HologramCollection** and select **Underworld**.</span></span>
* <span data-ttu-id="ad7ff-435">Développez le sous- **monde** et sélectionnez **VoiceSource**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-435">Expand **Underworld** and select **VoiceSource**.</span></span>
* <span data-ttu-id="ad7ff-436">Dans le panneau **inspecteur** , cliquez sur **Ajouter un composant** et ajouter un **effet utilisateur vocal**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-436">In the **Inspector** panel, click **Add Component** and add **User Voice Effect**.</span></span>

<span data-ttu-id="ad7ff-437">Un composant **audiosource** sera ajouté à **VoiceSource**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-437">An **AudioSource** component will be added to **VoiceSource**.</span></span>

* <span data-ttu-id="ad7ff-438">Dans **audiosource**, définissez **sortie** sur **UserVoice (Mixer)** .</span><span class="sxs-lookup"><span data-stu-id="ad7ff-438">In **AudioSource**, set **Output** to **UserVoice (Mixer)**.</span></span>
* <span data-ttu-id="ad7ff-439">Cochez la case spatialiser.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-439">Check the **Spatialize** checkbox.</span></span>
* <span data-ttu-id="ad7ff-440">Faites glisser le curseur de **lissage spatial** jusqu’à la forme **3D**, ou entrez **1** dans la zone d’édition.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-440">Drag the **Spatial Blend** slider all the way to **3D**, or enter **1** in the edit box.</span></span>
* <span data-ttu-id="ad7ff-441">Développez **paramètres audio 3D**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-441">Expand **3D Sound Settings**.</span></span>
* <span data-ttu-id="ad7ff-442">Affectez au **niveau Doppler** la valeur **0**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-442">Set **Doppler Level** to **0**.</span></span>
* <span data-ttu-id="ad7ff-443">Dans l' **effet utilisateur vocal**, définissez l' **objet parent** sur le sous- **monde** à partir de la scène.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-443">In **User Voice Effect**, set **Parent Object** to the **Underworld** from the scene.</span></span>
* <span data-ttu-id="ad7ff-444">Définissez **distance maximale** sur **1**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-444">Set **Max Distance** to **1**.</span></span>

<span data-ttu-id="ad7ff-445">La définition de la **distance maximale** indique à l' **utilisateur** qu’il doit être l’objet parent avant l’activation de l’effet.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-445">Setting **Max Distance** tells **User Voice Effect** how close the user must be to the parent object before the effect is enabled.</span></span>

* <span data-ttu-id="ad7ff-446">Dans **effet vocal**de l’utilisateur, développez **paramètres de chœur**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-446">In **User Voice Effect**, expand **Chorus Parameters**.</span></span>
* <span data-ttu-id="ad7ff-447">Définissez **profondeur** sur **0,1**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-447">Set **Depth** to **0.1**.</span></span>
* <span data-ttu-id="ad7ff-448">Définissez **Tap 1 volume**, **Appuyez sur 2 volume** , puis **sur 3 volumes** jusqu’à **0,8**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-448">Set **Tap 1 Volume**, **Tap 2 Volume** and **Tap 3 Volume** to **0.8**.</span></span>
* <span data-ttu-id="ad7ff-449">Définissez le **volume de son original** sur **0,5**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-449">Set **Original Sound Volume** to **0.5**.</span></span>

<span data-ttu-id="ad7ff-450">Les paramètres précédents configurent les paramètres du **AudioChorusFilter** Unity utilisé pour ajouter la richesse à la voix de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-450">The previous settings configure the parameters of the Unity **AudioChorusFilter** used to add richness to the user's voice.</span></span>

* <span data-ttu-id="ad7ff-451">Dans l' **effet utilisateur vocal**, développez **paramètres Echo**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-451">In **User Voice Effect**, expand **Echo Parameters**.</span></span>
* <span data-ttu-id="ad7ff-452">Définir le **délai** sur **300**</span><span class="sxs-lookup"><span data-stu-id="ad7ff-452">Set **Delay** to **300**</span></span>
* <span data-ttu-id="ad7ff-453">Définissez le **taux d’atténuation** sur **0,2**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-453">Set **Decay Ratio** to **0.2**.</span></span>
* <span data-ttu-id="ad7ff-454">Définissez le **volume de son original** sur **0**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-454">Set **Original Sound Volume** to **0**.</span></span>

<span data-ttu-id="ad7ff-455">Les paramètres précédents configurent les paramètres du **AudioEchoFilter** Unity utilisé pour faire écho à la voix de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-455">The previous settings configure the parameters of the Unity **AudioEchoFilter** used to cause the user's voice to echo.</span></span>

<span data-ttu-id="ad7ff-456">Le script de l’effet utilisateur vocal est chargé des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="ad7ff-456">The User Voice Effect script is responsible for:</span></span>

* <span data-ttu-id="ad7ff-457">Mesure de la distance entre l’utilisateur et le **gameobject** auquel le script est attaché.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-457">Measuring the distance between the user and the **GameObject** to which the script is attached.</span></span>
* <span data-ttu-id="ad7ff-458">Déterminer si l’utilisateur est confronté au **gameobject**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-458">Determining whether or not the user is facing the **GameObject**.</span></span>

<span data-ttu-id="ad7ff-459">L’utilisateur doit être orienté GameObject, quelle que soit la distance, pour que l’effet soit activé.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-459">The user must be facing the GameObject, regardless of distance, for the effect to be enabled.</span></span>

* <span data-ttu-id="ad7ff-460">Application et configuration d’un **AudioChorusFilter** et d’un **AudioEchoFilter** à **audiosource**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-460">Applying and configuring an **AudioChorusFilter** and an **AudioEchoFilter** to the **AudioSource**.</span></span>
* <span data-ttu-id="ad7ff-461">La désactivation de l’effet en désactivant les filtres.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-461">Disabling the effect by disabling the filters.</span></span>

<span data-ttu-id="ad7ff-462">L’effet User Voice utilise le composant sélecteur de flux MIC, à partir du [MixedRealityToolkit pour Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity), pour sélectionner le flux vocal de haute qualité et l’acheminer dans le système audio Unity.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-462">User Voice Effect uses the Mic Stream Selector component, from the [MixedRealityToolkit for Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity), to select the high quality voice stream and route it into Unity's audio system.</span></span>

* <span data-ttu-id="ad7ff-463">Dans le volet **hiérarchie** , sélectionnez **gestionnaires**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-463">In the **Hierarchy** panel, select **Managers**.</span></span>
* <span data-ttu-id="ad7ff-464">Dans le panneau **inspecteur** , développez **Gestionnaire d’entrée vocal**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-464">In the **Inspector** panel, expand **Speech Input Handler**.</span></span>
* <span data-ttu-id="ad7ff-465">Dans le **Gestionnaire d’entrée vocal**, développez afficher le sous- **monde**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-465">In **Speech Input Handler**, expand **Show Underworld**.</span></span>
* <span data-ttu-id="ad7ff-466">**Ne modifiez aucune fonction** en **UnderworldBase. OnEnable**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-466">Change **No Function** to **UnderworldBase.OnEnable**.</span></span>

![Mot Afficher le sous-monde](images/showunderworld.png)

* <span data-ttu-id="ad7ff-468">Développez masquer le sous- **monde**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-468">Expand **Hide Underworld**.</span></span>
* <span data-ttu-id="ad7ff-469">**Ne modifiez aucune fonction** en **UnderworldBase. OnDisable**.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-469">Change **No Function** to **UnderworldBase.OnDisable**.</span></span>

![Mot Masquer le sous-monde](images/hideunderworld.png)

#### <a name="build-and-deploy"></a><span data-ttu-id="ad7ff-471">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="ad7ff-471">Build and Deploy</span></span>

* <span data-ttu-id="ad7ff-472">Comme précédemment, générez le projet dans Unity et déployez-le dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-472">As before, build the project in Unity and deploy in Visual Studio.</span></span>

<span data-ttu-id="ad7ff-473">Une fois l’application déployée:</span><span class="sxs-lookup"><span data-stu-id="ad7ff-473">After the application is deployed:</span></span>

* <span data-ttu-id="ad7ff-474">Face à une surface (mur, plancher, table) et dites *«afficher le monde»* .</span><span class="sxs-lookup"><span data-stu-id="ad7ff-474">Face a surface (wall, floor, table) and say *"Show Underworld"*.</span></span>

<span data-ttu-id="ad7ff-475">Le sous-monde s’affiche et tous les autres hologrammes sont masqués.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-475">The underworld will be shown and all other holograms will be hidden.</span></span> <span data-ttu-id="ad7ff-476">Si vous ne voyez pas le sous-monde, assurez-vous que vous êtes face à une surface réaliste.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-476">If you do not see the underworld, ensure that you are facing a real-world surface.</span></span>

* <span data-ttu-id="ad7ff-477">Approche à l’intérieur d’un compteur de l’hologramme de la planète et commencer à parler.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-477">Approach within 1 meter of the underworld hologram and start talking.</span></span>

<span data-ttu-id="ad7ff-478">Des effets audio sont désormais appliqués à votre voix.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-478">There are now audio effects applied to your voice!</span></span>

* <span data-ttu-id="ad7ff-479">Quittez le sous-monde et notez la façon dont l’effet n’est plus appliqué.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-479">Turn away from the underworld and notice how the effect is no longer applied.</span></span>
* <span data-ttu-id="ad7ff-480">Dites *«masquer le monde»* pour masquer le sous-monde.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-480">Say *"Hide Underworld"* to hide the underworld.</span></span>

<span data-ttu-id="ad7ff-481">Le sous-monde est masqué et les hologrammes précédemment masqués réapparaissent.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-481">The underworld will be hidden and the previously hidden holograms will reappear.</span></span>

## <a name="the-end"></a><span data-ttu-id="ad7ff-482">La fin</span><span class="sxs-lookup"><span data-stu-id="ad7ff-482">The End</span></span>

<span data-ttu-id="ad7ff-483">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="ad7ff-483">Congratulations!</span></span> <span data-ttu-id="ad7ff-484">Vous avez maintenant terminé **l’heure spatiale 220: Son**spatial.</span><span class="sxs-lookup"><span data-stu-id="ad7ff-484">You have now completed **MR Spatial 220: Spatial sound**.</span></span>

<span data-ttu-id="ad7ff-485">Écoutez l’univers et donnez vie à vos expériences!</span><span class="sxs-lookup"><span data-stu-id="ad7ff-485">Listen to the world and bring your experiences to life with sound!</span></span>
