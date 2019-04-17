---
title: MR Spatial 220 - son Spatial
description: Suivez cette procédure pas à pas codage à l’aide de Unity, Visual Studio et HoloLens pour connaître les détails des concepts de sons spatiales.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, academy, didacticiel, son spatial
ms.openlocfilehash: 50d17fe8c9a6e3f18b1309a59c9c41af982a7505
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593831"
---
>[!NOTE]
><span data-ttu-id="2da97-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="2da97-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="2da97-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="2da97-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="2da97-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="2da97-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="2da97-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2da97-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="2da97-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="2da97-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="2da97-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="2da97-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-spatial-220-spatial-sound"></a><span data-ttu-id="2da97-110">MR 220 spatiale : Son spatial</span><span class="sxs-lookup"><span data-stu-id="2da97-110">MR Spatial 220: Spatial sound</span></span>

<span data-ttu-id="2da97-111">[Son spatial](spatial-sound.md) breathes vie dans hologrammes et leur donne la présence dans notre monde.</span><span class="sxs-lookup"><span data-stu-id="2da97-111">[Spatial sound](spatial-sound.md) breathes life into holograms and gives them presence in our world.</span></span> <span data-ttu-id="2da97-112">Hologrammes sont composées de lumière et son, et s’il vous arrive de perdre de votre hologrammes, son spatial peut vous aider à les trouver.</span><span class="sxs-lookup"><span data-stu-id="2da97-112">Holograms are composed of both light and sound, and if you happen to lose sight of your holograms, spatial sound can help you find them.</span></span> <span data-ttu-id="2da97-113">Son spatial n’est pas comme le son classique que vous devez entendre sur la case d’option, il est son qui est positionné dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="2da97-113">Spatial sound is not like the typical sound that you would hear on the radio, it is sound that is positioned in 3D space.</span></span> <span data-ttu-id="2da97-114">Avec son spatial, vous pouvez rendre hologrammes audio comme ils sont derrière vous, en regard de vous, ou même sur votre tête !</span><span class="sxs-lookup"><span data-stu-id="2da97-114">With spatial sound, you can make holograms sound like they're behind you, next to you, or even on your head!</span></span> <span data-ttu-id="2da97-115">Dans ce cours, vous allez :</span><span class="sxs-lookup"><span data-stu-id="2da97-115">In this course, you will:</span></span>

* <span data-ttu-id="2da97-116">Configurer votre environnement de développement pour utiliser Microsoft Spatial Sound.</span><span class="sxs-lookup"><span data-stu-id="2da97-116">Configure your development environment to use Microsoft Spatial Sound.</span></span>
* <span data-ttu-id="2da97-117">Utiliser le son Spatial pour améliorer les interactions.</span><span class="sxs-lookup"><span data-stu-id="2da97-117">Use Spatial Sound to enhance interactions.</span></span>
* <span data-ttu-id="2da97-118">Utiliser le son Spatial conjointement avec le mappage Spatial.</span><span class="sxs-lookup"><span data-stu-id="2da97-118">Use Spatial Sound in conjunction with Spatial Mapping.</span></span>
* <span data-ttu-id="2da97-119">Comprendre sonorisation et en combinant les meilleures pratiques.</span><span class="sxs-lookup"><span data-stu-id="2da97-119">Understand sound design and mixing best practices.</span></span>
* <span data-ttu-id="2da97-120">Utiliser le son pour améliorer les effets spéciaux et placer l’utilisateur dans le monde de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="2da97-120">Use sound to enhance special effects and bring the user into the Mixed Reality world.</span></span>

## <a name="device-support"></a><span data-ttu-id="2da97-121">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="2da97-121">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="2da97-122">Cours</span><span class="sxs-lookup"><span data-stu-id="2da97-122">Course</span></span></th><th style="width:150px"> <span data-ttu-id="2da97-123"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="2da97-123"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="2da97-124"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="2da97-124"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="2da97-125">MR 220 spatiale : Son spatial</span><span class="sxs-lookup"><span data-stu-id="2da97-125">MR Spatial 220: Spatial sound</span></span></td><td style="text-align: center;"> <span data-ttu-id="2da97-126">✔️</span><span class="sxs-lookup"><span data-stu-id="2da97-126">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="2da97-127">✔️</span><span class="sxs-lookup"><span data-stu-id="2da97-127">✔️</span></span></td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="2da97-128">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="2da97-128">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2da97-129">Prérequis</span><span class="sxs-lookup"><span data-stu-id="2da97-129">Prerequisites</span></span>

* <span data-ttu-id="2da97-130">Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="2da97-130">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="2da97-131">Base C# possibilité de programmation.</span><span class="sxs-lookup"><span data-stu-id="2da97-131">Some basic C# programming ability.</span></span>
* <span data-ttu-id="2da97-132">Vous devez avoir terminé [101 de principes de base MR](holograms-101.md).</span><span class="sxs-lookup"><span data-stu-id="2da97-132">You should have completed [MR Basics 101](holograms-101.md).</span></span>
* <span data-ttu-id="2da97-133">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="2da97-133">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="2da97-134">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="2da97-134">Project files</span></span>

* <span data-ttu-id="2da97-135">Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-220-SpatialSound.zip) requise par le projet.</span><span class="sxs-lookup"><span data-stu-id="2da97-135">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-220-SpatialSound.zip) required by the project.</span></span><span data-ttu-id="2da97-136"> Nécessite Unity 2017.2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2da97-136"> Requires Unity 2017.2 or later.</span></span>
  * <span data-ttu-id="2da97-137">Si vous avez besoin de prise en charge de Unity 5.6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-220.zip).</span><span class="sxs-lookup"><span data-stu-id="2da97-137">If you still need Unity 5.6 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-220.zip).</span></span> <span data-ttu-id="2da97-138">Cette version peut ne plus être à jour.</span><span class="sxs-lookup"><span data-stu-id="2da97-138">This release may no longer be up-to-date.</span></span>
  * <span data-ttu-id="2da97-139">Si vous avez besoin de prise en charge de Unity 5.5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-220.zip).</span><span class="sxs-lookup"><span data-stu-id="2da97-139">If you still need Unity 5.5 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-220.zip).</span></span><span data-ttu-id="2da97-140"> Cette version peut ne plus être à jour.</span><span class="sxs-lookup"><span data-stu-id="2da97-140"> This release may no longer be up-to-date.</span></span>
  * <span data-ttu-id="2da97-141">Si vous avez besoin de prise en charge de Unity 5.4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-220.zip).</span><span class="sxs-lookup"><span data-stu-id="2da97-141">If you still need Unity 5.4 support, please use [this release](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-220.zip).</span></span><span data-ttu-id="2da97-142"> Cette version peut ne plus être à jour.</span><span class="sxs-lookup"><span data-stu-id="2da97-142"> This release may no longer be up-to-date.</span></span>
* <span data-ttu-id="2da97-143">Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="2da97-143">Un-archive the files to your desktop or other easy to reach location.</span></span>

>[!NOTE]
><span data-ttu-id="2da97-144">Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-220-SpatialSound).</span><span class="sxs-lookup"><span data-stu-id="2da97-144">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-220-SpatialSound).</span></span>

### <a name="errata-and-notes"></a><span data-ttu-id="2da97-145">Errata et remarques</span><span class="sxs-lookup"><span data-stu-id="2da97-145">Errata and Notes</span></span>

* <span data-ttu-id="2da97-146">« Activer uniquement mon Code » doit être désactivé (*unchecked*) dans Visual Studio sous Outils -> Options -> débogage afin d’atteindre des points d’arrêt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="2da97-146">"Enable Just My Code" needs to be disabled (*unchecked*) in Visual Studio under Tools->Options->Debugging in order to hit breakpoints in your code.</span></span>

## <a name="chapter-1---unity-setup"></a><span data-ttu-id="2da97-147">Chapitre 1 - le programme d’installation Unity</span><span class="sxs-lookup"><span data-stu-id="2da97-147">Chapter 1 - Unity Setup</span></span>

### <a name="objectives"></a><span data-ttu-id="2da97-148">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2da97-148">Objectives</span></span>

* <span data-ttu-id="2da97-149">Modifier la configuration de son d’Unity pour utiliser Microsoft Spatial Sound.</span><span class="sxs-lookup"><span data-stu-id="2da97-149">Change Unity's sound configuration to use Microsoft Spatial Sound.</span></span>
* <span data-ttu-id="2da97-150">Ajouter des sons 3D à un objet dans Unity.</span><span class="sxs-lookup"><span data-stu-id="2da97-150">Add 3D sound to an object in Unity.</span></span>

### <a name="instructions"></a><span data-ttu-id="2da97-151">Instructions</span><span class="sxs-lookup"><span data-stu-id="2da97-151">Instructions</span></span>

* <span data-ttu-id="2da97-152">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="2da97-152">Start Unity.</span></span>
* <span data-ttu-id="2da97-153">Sélectionnez **Open**.</span><span class="sxs-lookup"><span data-stu-id="2da97-153">Select **Open**.</span></span>
* <span data-ttu-id="2da97-154">Accédez à votre bureau et de rechercher le dossier vous précédemment non archivés.</span><span class="sxs-lookup"><span data-stu-id="2da97-154">Navigate to your Desktop and find the folder you previously un-archived.</span></span>
* <span data-ttu-id="2da97-155">Cliquez sur le **Starting\Decibel** dossier et appuyez sur la **sélectionner le dossier** bouton.</span><span class="sxs-lookup"><span data-stu-id="2da97-155">Click on the **Starting\Decibel** folder and then press the **Select Folder** button.</span></span>
* <span data-ttu-id="2da97-156">Attendez que le projet à charger dans Unity.</span><span class="sxs-lookup"><span data-stu-id="2da97-156">Wait for the project to load in Unity.</span></span>
* <span data-ttu-id="2da97-157">Dans le **projet** Panneau de configuration, ouvrez **Scenes\Decibel.unity**.</span><span class="sxs-lookup"><span data-stu-id="2da97-157">In the **Project** panel, open **Scenes\Decibel.unity**.</span></span>
* <span data-ttu-id="2da97-158">Dans le **hiérarchie** volet, développez **HologramCollection** et sélectionnez **P0LY**.</span><span class="sxs-lookup"><span data-stu-id="2da97-158">In the **Hierarchy** panel, expand **HologramCollection** and select **P0LY**.</span></span>
* <span data-ttu-id="2da97-159">Dans l’inspecteur, développez **AudioSource** et notez qu’il y a aucune **Spatialize** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="2da97-159">In the Inspector, expand **AudioSource** and notice that there is no **Spatialize** check box.</span></span>

<span data-ttu-id="2da97-160">Par défaut, Unity ne charge pas un plug-in spatial.</span><span class="sxs-lookup"><span data-stu-id="2da97-160">By default, Unity does not load a spatializer plugin.</span></span> <span data-ttu-id="2da97-161">Les étapes suivantes activera le son de Spatial dans le projet.</span><span class="sxs-lookup"><span data-stu-id="2da97-161">The following steps will enable Spatial Sound in the project.</span></span>

* <span data-ttu-id="2da97-162">Dans le menu supérieur de Unity, accédez à **Modifier > Paramètres du projet > Audio**.</span><span class="sxs-lookup"><span data-stu-id="2da97-162">In Unity's top menu, go to **Edit > Project Settings > Audio**.</span></span>
* <span data-ttu-id="2da97-163">Rechercher la **plug-in spatial** liste déroulante, puis sélectionnez **MS HRTF Spatializer**.</span><span class="sxs-lookup"><span data-stu-id="2da97-163">Find the **Spatializer Plugin** dropdown, and select **MS HRTF Spatializer**.</span></span>
* <span data-ttu-id="2da97-164">Dans le **hiérarchie** panneau, sélectionnez **HologramCollection > P0LY**.</span><span class="sxs-lookup"><span data-stu-id="2da97-164">In the **Hierarchy** panel, select **HologramCollection > P0LY**.</span></span>
* <span data-ttu-id="2da97-165">Dans le **inspecteur** panneau, recherchez le **Audio Source** composant.</span><span class="sxs-lookup"><span data-stu-id="2da97-165">In the **Inspector** panel, find the **Audio Source** component.</span></span>
* <span data-ttu-id="2da97-166">Vérifier le **Spatialize** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="2da97-166">Check the **Spatialize** checkbox.</span></span>
* <span data-ttu-id="2da97-167">Faites glisser le **Blend Spatial** curseur jusqu’au **3D**, ou entrez **1** dans la zone d’édition.</span><span class="sxs-lookup"><span data-stu-id="2da97-167">Drag the **Spatial Blend** slider all the way to **3D**, or enter **1** in the edit box.</span></span>

<span data-ttu-id="2da97-168">Maintenant nous générer le projet dans Unity et configurer la solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2da97-168">We will now build the project in Unity and configure the solution in Visual Studio.</span></span>

1. <span data-ttu-id="2da97-169">Dans Unity, sélectionnez **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="2da97-169">In Unity, select **File > Build Settings**.</span></span>
2. <span data-ttu-id="2da97-170">Cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="2da97-170">Click **Add Open Scenes** to add the scene.</span></span>
3. <span data-ttu-id="2da97-171">Sélectionnez **plateforme Windows universelle** dans le **plateforme** liste et cliquez sur **plateforme de commutation**.</span><span class="sxs-lookup"><span data-stu-id="2da97-171">Select **Universal Windows Platform** in the **Platform** list and click **Switch Platform**.</span></span>
4. <span data-ttu-id="2da97-172">Si vous développez en particulier pour HoloLens, définissez **appareil cible** à **HoloLens**.</span><span class="sxs-lookup"><span data-stu-id="2da97-172">If you're specifically developing for HoloLens, set **Target device** to **HoloLens**.</span></span> <span data-ttu-id="2da97-173">Dans le cas contraire, laissez-le sur **n’importe quel appareil**.</span><span class="sxs-lookup"><span data-stu-id="2da97-173">Otherwise, leave it on **Any device**.</span></span>
5. <span data-ttu-id="2da97-174">Vérifiez **Type Build** a la valeur **D3D** et **SDK** a la valeur **dernière installé** (qui doit être SDK 16299 ou une version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="2da97-174">Ensure **Build Type** is set to **D3D** and **SDK** is set to **Latest installed** (which should be SDK 16299 or newer).</span></span>
6. <span data-ttu-id="2da97-175">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="2da97-175">Click **Build**.</span></span>
7. <span data-ttu-id="2da97-176">Créer un **nouveau dossier** nommé « Application ».</span><span class="sxs-lookup"><span data-stu-id="2da97-176">Create a **New Folder** named "App".</span></span>
8. <span data-ttu-id="2da97-177">Clic le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="2da97-177">Single click the **App** folder.</span></span>
9. <span data-ttu-id="2da97-178">Appuyez sur **sélectionnez dossier**.</span><span class="sxs-lookup"><span data-stu-id="2da97-178">Press **Select Folder**.</span></span>

<span data-ttu-id="2da97-179">Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="2da97-179">When Unity is done, a File Explorer window will appear.</span></span>

1. <span data-ttu-id="2da97-180">Ouvrez le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="2da97-180">Open the **App** folder.</span></span>
2. <span data-ttu-id="2da97-181">Ouvrez le **Solution de Visual Studio en décibels**.</span><span class="sxs-lookup"><span data-stu-id="2da97-181">Open the **Decibel Visual Studio Solution**.</span></span>

<span data-ttu-id="2da97-182">Si le déploiement sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="2da97-182">If deploying to HoloLens:</span></span>

1. <span data-ttu-id="2da97-183">À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x86**.</span><span class="sxs-lookup"><span data-stu-id="2da97-183">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x86**.</span></span>
2. <span data-ttu-id="2da97-184">Cliquez sur la flèche déroulante en regard du bouton de l’ordinateur Local, puis sélectionnez **Machine distante**.</span><span class="sxs-lookup"><span data-stu-id="2da97-184">Click on the drop down arrow next to the Local Machine button, and select **Remote Machine**.</span></span>
3. <span data-ttu-id="2da97-185">Entrez **votre adresse IP du périphérique HoloLens** et définir le Mode d’authentification **universel (protocole non chiffré)**.</span><span class="sxs-lookup"><span data-stu-id="2da97-185">Enter **your HoloLens device IP address** and set Authentication Mode to **Universal (Unencrypted Protocol)**.</span></span> <span data-ttu-id="2da97-186">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="2da97-186">Click **Select**.</span></span> <span data-ttu-id="2da97-187">Si vous ne connaissez pas votre adresse IP du périphérique, recherchez dans **Paramètres > réseau & Internet > Options avancées**.</span><span class="sxs-lookup"><span data-stu-id="2da97-187">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options**.</span></span>
4. <span data-ttu-id="2da97-188">Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="2da97-188">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="2da97-189">S’il s’agit de la première fois le déploiement sur votre périphérique, vous devrez [Couplez-le Visual Studio](using-visual-studio.md#pairing-your-device---hololens-1st-gen).</span><span class="sxs-lookup"><span data-stu-id="2da97-189">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device---hololens-1st-gen).</span></span>

<span data-ttu-id="2da97-190">Si le déploiement sur un casque immersif :</span><span class="sxs-lookup"><span data-stu-id="2da97-190">If deploying to an immersive headset:</span></span>

1. <span data-ttu-id="2da97-191">À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x64**.</span><span class="sxs-lookup"><span data-stu-id="2da97-191">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x64**.</span></span>
2. <span data-ttu-id="2da97-192">Assurez-vous que la cible de déploiement est définie sur **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="2da97-192">Make sure the deployment target is set to **Local Machine**.</span></span>
3. <span data-ttu-id="2da97-193">Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="2da97-193">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>

## <a name="chapter-2---spatial-sound-and-interaction"></a><span data-ttu-id="2da97-194">Chapitre 2 - son Spatial et Interaction</span><span class="sxs-lookup"><span data-stu-id="2da97-194">Chapter 2 - Spatial Sound and Interaction</span></span>

### <a name="objectives"></a><span data-ttu-id="2da97-195">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2da97-195">Objectives</span></span>

* <span data-ttu-id="2da97-196">Améliorer le réalisme hologramme à l’aide de son.</span><span class="sxs-lookup"><span data-stu-id="2da97-196">Enhance hologram realism using sound.</span></span>
* <span data-ttu-id="2da97-197">Diriger le regard de l’utilisateur à l’aide de son.</span><span class="sxs-lookup"><span data-stu-id="2da97-197">Direct the user's gaze using sound.</span></span>
* <span data-ttu-id="2da97-198">Fournir des commentaires de mouvement à l’aide de son.</span><span class="sxs-lookup"><span data-stu-id="2da97-198">Provide gesture feedback using sound.</span></span>

### <a name="part-1---enhancing-realism"></a><span data-ttu-id="2da97-199">Partie 1 - amélioration de réalisme</span><span class="sxs-lookup"><span data-stu-id="2da97-199">Part 1 - Enhancing Realism</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="2da97-200">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="2da97-200">Key Concepts</span></span>

* <span data-ttu-id="2da97-201">Spatialize les sons hologramme.</span><span class="sxs-lookup"><span data-stu-id="2da97-201">Spatialize hologram sounds.</span></span>
* <span data-ttu-id="2da97-202">Sources audio doivent être placés à l’emplacement approprié sur l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="2da97-202">Sound sources should be placed at an appropriate location on the hologram.</span></span>

<span data-ttu-id="2da97-203">L’emplacement approprié pour le son est tout dépendra de l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="2da97-203">The appropriate location for the sound is going to depend on the hologram.</span></span> <span data-ttu-id="2da97-204">Par exemple, si l’hologramme est d’un humain, la source audio doit se trouver près de la bouche et pas les pieds.</span><span class="sxs-lookup"><span data-stu-id="2da97-204">For example, if the hologram is of a human, the sound source should be located near the mouth and not the feet.</span></span>

#### <a name="instructions"></a><span data-ttu-id="2da97-205">Instructions</span><span class="sxs-lookup"><span data-stu-id="2da97-205">Instructions</span></span>

<span data-ttu-id="2da97-206">Les instructions suivantes seront attache un son spatialized un hologramme.</span><span class="sxs-lookup"><span data-stu-id="2da97-206">The following instructions will attach a spatialized sound to a hologram.</span></span>

* <span data-ttu-id="2da97-207">Dans le **hiérarchie** volet, développez **HologramCollection** et sélectionnez **P0LY**.</span><span class="sxs-lookup"><span data-stu-id="2da97-207">In the **Hierarchy** panel, expand **HologramCollection** and select **P0LY**.</span></span>
* <span data-ttu-id="2da97-208">Dans le **inspecteur** volet le **AudioSource**, cliquez sur le cercle en regard **AudioClip** et sélectionnez **PolyHover** à partir de la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="2da97-208">In the **Inspector** panel, in the **AudioSource**, click the circle next to **AudioClip** and select **PolyHover** from the pop-up.</span></span>
* <span data-ttu-id="2da97-209">Cliquez sur le cercle en regard **sortie** et sélectionnez **effets sonores** à partir de la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="2da97-209">Click the circle next to **Output** and select **SoundEffects** from the pop-up.</span></span>

<span data-ttu-id="2da97-210">Projet décibels utilise un Unity **AudioMixer** composant pour activer l’ajustement des niveaux audio pour les groupes de sons.</span><span class="sxs-lookup"><span data-stu-id="2da97-210">Project Decibel uses a Unity **AudioMixer** component to enable adjusting sound levels for groups of sounds.</span></span> <span data-ttu-id="2da97-211">En regroupant des sons de cette façon, le volume total peut être ajusté tout en conservant le volume relatif de chaque son.</span><span class="sxs-lookup"><span data-stu-id="2da97-211">By grouping sounds this way, the overall volume can be adjusted while maintaining the relative volume of each sound.</span></span>

* <span data-ttu-id="2da97-212">Dans le **AudioSource**, développez **les paramètres audio 3D**.</span><span class="sxs-lookup"><span data-stu-id="2da97-212">In the **AudioSource**, expand **3D Sound Settings**.</span></span>
* <span data-ttu-id="2da97-213">Définissez **Doppler niveau** à **0**.</span><span class="sxs-lookup"><span data-stu-id="2da97-213">Set **Doppler Level** to **0**.</span></span>

<span data-ttu-id="2da97-214">La définition Doppler niveau pour zéro désactive les modifications à la tonalité a provoqué par motion (soit de l’hologramme ou de l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="2da97-214">Setting Doppler level to zero disables changes in pitch caused by motion (either of the hologram or the user).</span></span> <span data-ttu-id="2da97-215">Un exemple classique de Doppler est une voiture évoluant rapidement.</span><span class="sxs-lookup"><span data-stu-id="2da97-215">A classic example of Doppler is a fast-moving car.</span></span> <span data-ttu-id="2da97-216">Approche de la voiture un écouteur stationnaire, la tonalité du moteur de données augmente.</span><span class="sxs-lookup"><span data-stu-id="2da97-216">As the car approaches a stationary listener, the pitch of the engine rises.</span></span> <span data-ttu-id="2da97-217">Lorsqu’il passe à l’écouteur, le tangage réduit à distance.</span><span class="sxs-lookup"><span data-stu-id="2da97-217">When it passes the listener, the pitch lowers with distance.</span></span>

### <a name="part-2---directing-the-users-gaze"></a><span data-ttu-id="2da97-218">Partie 2 : diriger du pointage de regard l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2da97-218">Part 2 - Directing the User's Gaze</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="2da97-219">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="2da97-219">Key Concepts</span></span>

* <span data-ttu-id="2da97-220">Utiliser le son pour attirer l’attention sur hologrammes importants.</span><span class="sxs-lookup"><span data-stu-id="2da97-220">Use sound to call attention to important holograms.</span></span>
* <span data-ttu-id="2da97-221">Les oreilles vous permettent de diriger où les yeux doivent se présenter.</span><span class="sxs-lookup"><span data-stu-id="2da97-221">The ears help direct where the eyes should look.</span></span>
* <span data-ttu-id="2da97-222">Le cerveau a certaines attentes appris.</span><span class="sxs-lookup"><span data-stu-id="2da97-222">The brain has some learned expectations.</span></span>

<span data-ttu-id="2da97-223">Un exemple d’attentes appris est qu’oiseaux est généralement ci-dessus les têtes de personnes impliquées.</span><span class="sxs-lookup"><span data-stu-id="2da97-223">One example of learned expectations is that birds are generally above the heads of humans.</span></span> <span data-ttu-id="2da97-224">Si un utilisateur entend un son bird, leur réaction initiale consiste à rechercher.</span><span class="sxs-lookup"><span data-stu-id="2da97-224">If a user hears a bird sound, their initial reaction is to look up.</span></span> <span data-ttu-id="2da97-225">Placer un oiseau ci-dessous l’utilisateur peut entraîner les accessible sur la direction correcte du son, mais l’impossibilité de trouver l’hologramme en fonction de l’attente d’avoir à rechercher.</span><span class="sxs-lookup"><span data-stu-id="2da97-225">Placing a bird below the user can lead to them facing the correct direction of the sound, but being unable to find the hologram based on the expectation of needing to look up.</span></span>

#### <a name="instructions"></a><span data-ttu-id="2da97-226">Instructions</span><span class="sxs-lookup"><span data-stu-id="2da97-226">Instructions</span></span>

<span data-ttu-id="2da97-227">Les instructions suivantes activent P0LY masquer derrière vous, afin que son permet de localiser l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="2da97-227">The following instructions enable P0LY to hide behind you, so that you can use sound to locate the hologram.</span></span>

* <span data-ttu-id="2da97-228">Dans le **hiérarchie** panneau, sélectionnez **gestionnaires**.</span><span class="sxs-lookup"><span data-stu-id="2da97-228">In the **Hierarchy** panel, select **Managers**.</span></span>
* <span data-ttu-id="2da97-229">Dans le **inspecteur** panneau, recherchez **Gestionnaire d’entrée vocale**.</span><span class="sxs-lookup"><span data-stu-id="2da97-229">In the **Inspector** panel, find **Speech Input Handler**.</span></span>
* <span data-ttu-id="2da97-230">Dans **Gestionnaire d’entrée vocale**, développez **accédez masquer**.</span><span class="sxs-lookup"><span data-stu-id="2da97-230">In **Speech Input Handler**, expand **Go Hide**.</span></span>
* <span data-ttu-id="2da97-231">Modification **aucune fonction** à **PolyActions.GoHide**.</span><span class="sxs-lookup"><span data-stu-id="2da97-231">Change **No Function** to **PolyActions.GoHide**.</span></span>

![mot clé : Accédez masquer](images/gohide.png)

### <a name="part-3---gesture-feedback"></a><span data-ttu-id="2da97-233">Partie 3 : les commentaires de mouvement</span><span class="sxs-lookup"><span data-stu-id="2da97-233">Part 3 - Gesture Feedback</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="2da97-234">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="2da97-234">Key Concepts</span></span>

* <span data-ttu-id="2da97-235">Fournir à l’utilisateur avec la confirmation de mouvement positive à l’aide de son</span><span class="sxs-lookup"><span data-stu-id="2da97-235">Provide the user with positive gesture confirmation using sound</span></span>
* <span data-ttu-id="2da97-236">Ne surchargent pas l’utilisateur - get sons trop forts de la façon</span><span class="sxs-lookup"><span data-stu-id="2da97-236">Do not overwhelm the user - overly loud sounds get in the way</span></span>
* <span data-ttu-id="2da97-237">Travail sons subtiles meilleures - assombrissent pas l’expérience</span><span class="sxs-lookup"><span data-stu-id="2da97-237">Subtle sounds work best - do not overshadow the experience</span></span>

#### <a name="instructions"></a><span data-ttu-id="2da97-238">Instructions</span><span class="sxs-lookup"><span data-stu-id="2da97-238">Instructions</span></span>

* <span data-ttu-id="2da97-239">Dans le **hiérarchie** volet, développez **HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="2da97-239">In the **Hierarchy** panel, expand **HologramCollection**.</span></span>
* <span data-ttu-id="2da97-240">Développez **EnergyHub** et sélectionnez **Base**.</span><span class="sxs-lookup"><span data-stu-id="2da97-240">Expand **EnergyHub** and select **Base**.</span></span>
* <span data-ttu-id="2da97-241">Dans le **inspecteur** du panneau, cliquez sur **ajouter un composant** et ajoutez **Gestionnaire de mouvements son**.</span><span class="sxs-lookup"><span data-stu-id="2da97-241">In the **Inspector** panel, click **Add Component** and add **Gesture Sound Handler**.</span></span>
* <span data-ttu-id="2da97-242">Dans **Gestionnaire de mouvements son**, cliquez sur le cercle en regard **Navigation démarré Clip** et **Clip mis à jour de Navigation** et sélectionnez **RotateClick**à partir de la fenêtre contextuelle pour les deux.</span><span class="sxs-lookup"><span data-stu-id="2da97-242">In **Gesture Sound Handler**, click the circle next to **Navigation Started Clip** and **Navigation Updated Clip** and select **RotateClick** from the pop-up for both.</span></span>
* <span data-ttu-id="2da97-243">Double-cliquez sur « GestureSoundHandler » pour charger dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2da97-243">Double click on "GestureSoundHandler" to load in Visual Studio.</span></span>

<span data-ttu-id="2da97-244">Gestionnaire de mouvements son effectue les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="2da97-244">Gesture Sound Handler performs the following tasks:</span></span>

* <span data-ttu-id="2da97-245">Créer et configurer un **AudioSource**.</span><span class="sxs-lookup"><span data-stu-id="2da97-245">Create and configure an **AudioSource**.</span></span>
* <span data-ttu-id="2da97-246">Place le **AudioSource** à l’emplacement du approprié **GameObject**.</span><span class="sxs-lookup"><span data-stu-id="2da97-246">Place the **AudioSource** at the location of the appropriate **GameObject**.</span></span>
* <span data-ttu-id="2da97-247">Lit le **AudioClip** associées au geste.</span><span class="sxs-lookup"><span data-stu-id="2da97-247">Plays the **AudioClip** associated with the gesture.</span></span>

#### <a name="build-and-deploy"></a><span data-ttu-id="2da97-248">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="2da97-248">Build and Deploy</span></span>

1. <span data-ttu-id="2da97-249">Dans Unity, sélectionnez **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="2da97-249">In Unity, select **File > Build Settings**.</span></span>
2. <span data-ttu-id="2da97-250">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="2da97-250">Click **Build**.</span></span>
3. <span data-ttu-id="2da97-251">Clic le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="2da97-251">Single click the **App** folder.</span></span>
4. <span data-ttu-id="2da97-252">Appuyez sur **sélectionnez dossier**.</span><span class="sxs-lookup"><span data-stu-id="2da97-252">Press **Select Folder**.</span></span>

<span data-ttu-id="2da97-253">Vérifiez que la barre d’outils indique « Release », « x 86 » ou « x64 » et « Appareil à distance ».</span><span class="sxs-lookup"><span data-stu-id="2da97-253">Check that the Toolbar says "Release", "x86" or "x64", and "Remote Device".</span></span> <span data-ttu-id="2da97-254">Si ce n’est pas le cas, c’est l’instance de codage de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2da97-254">If not, this is the coding instance of Visual Studio.</span></span> <span data-ttu-id="2da97-255">Vous devrez peut-être ouvrir à nouveau la solution à partir du dossier d’application.</span><span class="sxs-lookup"><span data-stu-id="2da97-255">You may need to re-open the solution from the App folder.</span></span>

* <span data-ttu-id="2da97-256">Si vous y êtes invité, rechargez les fichiers de projet.</span><span class="sxs-lookup"><span data-stu-id="2da97-256">If prompted, reload the project files.</span></span>
* <span data-ttu-id="2da97-257">Comme auparavant, vous déployez à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2da97-257">As before, deploy from Visual Studio.</span></span>

<span data-ttu-id="2da97-258">Une fois que l’application est déployée :</span><span class="sxs-lookup"><span data-stu-id="2da97-258">After the application is deployed:</span></span>

* <span data-ttu-id="2da97-259">Observez comment le son change à mesure que vous déplacez P0LY.</span><span class="sxs-lookup"><span data-stu-id="2da97-259">Observe how the sound changes as you move around P0LY.</span></span>
* <span data-ttu-id="2da97-260">Par exemple *« Accédez masquer »* P0LY pour déplacer vers un emplacement derrière vous.</span><span class="sxs-lookup"><span data-stu-id="2da97-260">Say *"Go Hide"* to make P0LY move to a location behind you.</span></span> <span data-ttu-id="2da97-261">Rechercher le son.</span><span class="sxs-lookup"><span data-stu-id="2da97-261">Find it by the sound.</span></span>
* <span data-ttu-id="2da97-262">Utilisation à la base du Hub d’énergie.</span><span class="sxs-lookup"><span data-stu-id="2da97-262">Gaze at the base of the Energy Hub.</span></span> <span data-ttu-id="2da97-263">Cliquez et faites glisser les gauche ou droite pour faire pivoter l’hologramme et notez la façon dont le son clic confirme le mouvement.</span><span class="sxs-lookup"><span data-stu-id="2da97-263">Tap and drag left or right to rotate the hologram and notice how the clicking sound confirms the gesture.</span></span>

<span data-ttu-id="2da97-264">Remarque: Il existe un volet de texte qui sera tag-along avec vous.</span><span class="sxs-lookup"><span data-stu-id="2da97-264">Note: There is a text panel that will tag-along with you.</span></span> <span data-ttu-id="2da97-265">Il contient les commandes vocales disponibles que vous pouvez utiliser tout au long de ce cours.</span><span class="sxs-lookup"><span data-stu-id="2da97-265">This will contain the available voice commands that you can use throughout this course.</span></span>

## <a name="chapter-3---spatial-sound-and-spatial-mapping"></a><span data-ttu-id="2da97-266">Chapitre 3 - mappage audio et Spatial Spatial</span><span class="sxs-lookup"><span data-stu-id="2da97-266">Chapter 3 - Spatial Sound and Spatial Mapping</span></span>

### <a name="objectives"></a><span data-ttu-id="2da97-267">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2da97-267">Objectives</span></span>

* <span data-ttu-id="2da97-268">Confirmer l’interaction entre hologrammes et le monde réel à l’aide de son.</span><span class="sxs-lookup"><span data-stu-id="2da97-268">Confirm interaction between holograms and the real world using sound.</span></span>
* <span data-ttu-id="2da97-269">Occlude son à l’aide du monde physique.</span><span class="sxs-lookup"><span data-stu-id="2da97-269">Occlude sound using the physical world.</span></span>

### <a name="part-1---physical-world-interaction"></a><span data-ttu-id="2da97-270">1ère partie-Interaction du monde physique</span><span class="sxs-lookup"><span data-stu-id="2da97-270">Part 1 - Physical World Interaction</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="2da97-271">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="2da97-271">Key Concepts</span></span>

* <span data-ttu-id="2da97-272">Objets physiques font généralement un son lorsqu’il rencontre une aire ou un autre objet.</span><span class="sxs-lookup"><span data-stu-id="2da97-272">Physical objects generally make a sound when encountering a surface or another object.</span></span>
* <span data-ttu-id="2da97-273">Sons doivent être le contexte approprié au sein de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="2da97-273">Sounds should be context appropriate within the experience.</span></span>

<span data-ttu-id="2da97-274">Par exemple, définissant une tasse sur une table doit rendre un son moins fort que la suppression d’un boulder sur une pièce de métal.</span><span class="sxs-lookup"><span data-stu-id="2da97-274">For example, setting a cup on a table should make a quieter sound than dropping a boulder on a piece of metal.</span></span>

#### <a name="instructions"></a><span data-ttu-id="2da97-275">Instructions</span><span class="sxs-lookup"><span data-stu-id="2da97-275">Instructions</span></span>

* <span data-ttu-id="2da97-276">Dans le **hiérarchie** volet, développez **HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="2da97-276">In the **Hierarchy** panel, expand **HologramCollection**.</span></span>
* <span data-ttu-id="2da97-277">Développez **EnergyHub**, sélectionnez **Base**.</span><span class="sxs-lookup"><span data-stu-id="2da97-277">Expand **EnergyHub**, select **Base**.</span></span>
* <span data-ttu-id="2da97-278">Dans le **inspecteur** du panneau, cliquez sur **ajouter un composant** et ajoutez **Action et appuyez sur les Place à avec son**.</span><span class="sxs-lookup"><span data-stu-id="2da97-278">In the **Inspector** panel, click **Add Component** and add **Tap To Place With Sound and Action**.</span></span>
* <span data-ttu-id="2da97-279">Dans **appuyez sur à la Place avec Action et son**:</span><span class="sxs-lookup"><span data-stu-id="2da97-279">In **Tap To Place With Sound and Action**:</span></span>
  * <span data-ttu-id="2da97-280">Vérifiez **placer Parent sur Tap**.</span><span class="sxs-lookup"><span data-stu-id="2da97-280">Check **Place Parent On Tap**.</span></span>
  * <span data-ttu-id="2da97-281">Définissez **Placement son** à **Place**.</span><span class="sxs-lookup"><span data-stu-id="2da97-281">Set **Placement Sound** to **Place**.</span></span>
  * <span data-ttu-id="2da97-282">Définissez **Pickup son** à **Pickup**.</span><span class="sxs-lookup"><span data-stu-id="2da97-282">Set **Pickup Sound** to **Pickup**.</span></span>
  * <span data-ttu-id="2da97-283">Appuyez sur le signe + en bas à droite dans les répertoires **sur l’Action Pickup** et **sur l’Action de sélection élective**.</span><span class="sxs-lookup"><span data-stu-id="2da97-283">Press the + in the bottom right under both **On Pickup Action** and **On Placement Action**.</span></span> <span data-ttu-id="2da97-284">Faites glisser EnergyHub à partir de la scène dans la **None (objet)** champs.</span><span class="sxs-lookup"><span data-stu-id="2da97-284">Drag EnergyHub from the scene into the **None (Object)** fields.</span></span>
    * <span data-ttu-id="2da97-285">Sous **sur l’Action Pickup**, cliquez sur **aucune fonction** -> **EnergyHubBase** -> **ResetAnimation**.</span><span class="sxs-lookup"><span data-stu-id="2da97-285">Under **On Pickup Action**, click on **No Function** -> **EnergyHubBase** -> **ResetAnimation**.</span></span>
    * <span data-ttu-id="2da97-286">Sous **sur l’Action de sélection élective**, cliquez sur **aucune fonction** -> **EnergyHubBase** -> **OnSelect**.</span><span class="sxs-lookup"><span data-stu-id="2da97-286">Under **On Placement Action**, click on **No Function** -> **EnergyHubBase** -> **OnSelect**.</span></span>

![Appuyez sur à la Place avec son et Action](images/holograms220-taptoplace.png)

### <a name="part-2---sound-occlusion"></a><span data-ttu-id="2da97-288">2ème partie-Occlusion audio</span><span class="sxs-lookup"><span data-stu-id="2da97-288">Part 2 - Sound Occlusion</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="2da97-289">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="2da97-289">Key Concepts</span></span>

* <span data-ttu-id="2da97-290">Son, comme la lumière, permettre être bloqué.</span><span class="sxs-lookup"><span data-stu-id="2da97-290">Sound, like light, can be occluded.</span></span>

<span data-ttu-id="2da97-291">Un exemple classique est une salle de concert.</span><span class="sxs-lookup"><span data-stu-id="2da97-291">A classic example is a concert hall.</span></span> <span data-ttu-id="2da97-292">Lorsqu’un écouteur est permanent en dehors de la salle et la porte est fermée, les sons de musique muffled.</span><span class="sxs-lookup"><span data-stu-id="2da97-292">When a listener is standing outside of the hall and the door is closed, the music sounds muffled.</span></span> <span data-ttu-id="2da97-293">Il est également généralement une réduction de volume.</span><span class="sxs-lookup"><span data-stu-id="2da97-293">There is also typically a reduction in volume.</span></span> <span data-ttu-id="2da97-294">Lorsque la porte est ouverte, la gamme complète du son est entendue à du volume réel.</span><span class="sxs-lookup"><span data-stu-id="2da97-294">When the door is opened, the full spectrum of the sound is heard at the actual volume.</span></span> <span data-ttu-id="2da97-295">Sons de haute fréquence sont absorbées généralement plus de basses fréquences.</span><span class="sxs-lookup"><span data-stu-id="2da97-295">High frequency sounds are generally absorbed more than low frequencies.</span></span>

#### <a name="instructions"></a><span data-ttu-id="2da97-296">Instructions</span><span class="sxs-lookup"><span data-stu-id="2da97-296">Instructions</span></span>

* <span data-ttu-id="2da97-297">Dans le **hiérarchie** volet, développez **HologramCollection** et sélectionnez **P0LY**.</span><span class="sxs-lookup"><span data-stu-id="2da97-297">In the **Hierarchy** panel, expand **HologramCollection** and select **P0LY**.</span></span>
* <span data-ttu-id="2da97-298">Dans le **inspecteur** du panneau, cliquez sur **ajouter un composant** et ajoutez **Audio émetteur**.</span><span class="sxs-lookup"><span data-stu-id="2da97-298">In the **Inspector** panel, click **Add Component** and add **Audio Emitter**.</span></span>

<span data-ttu-id="2da97-299">La classe de l’émetteur de l’Audio fournit les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="2da97-299">The Audio Emitter class provides the following features:</span></span>

* <span data-ttu-id="2da97-300">Restaure toutes les modifications sur le volume de la **AudioSource**.</span><span class="sxs-lookup"><span data-stu-id="2da97-300">Restores any changes to the volume of the **AudioSource**.</span></span>
* <span data-ttu-id="2da97-301">Effectue un **Physics.RaycastNonAlloc** à partir de la position de l’utilisateur dans la direction de la **GameObject** auquel le **AudioEmitter** est attaché.</span><span class="sxs-lookup"><span data-stu-id="2da97-301">Performs a **Physics.RaycastNonAlloc** from the user's position in the direction of the **GameObject** to which the **AudioEmitter** is attached.</span></span>

<span data-ttu-id="2da97-302">Optimiser les performances, la méthode RaycastNonAlloc permet de limiter les allocations, ainsi que le nombre de résultats retournés.</span><span class="sxs-lookup"><span data-stu-id="2da97-302">The RaycastNonAlloc method is used as a performance optimization to limit allocations as well as the number of results returned.</span></span>

* <span data-ttu-id="2da97-303">Pour chaque **IAudioInfluencer** rencontré, appelle le **ApplyEffect** (méthode).</span><span class="sxs-lookup"><span data-stu-id="2da97-303">For each **IAudioInfluencer** encountered, calls the **ApplyEffect** method.</span></span>
* <span data-ttu-id="2da97-304">Pour chaque précédente **IAudioInfluencer** appel de ne plus s’est produite, autrement dit le **RemoveEffect** (méthode).</span><span class="sxs-lookup"><span data-stu-id="2da97-304">For each previous **IAudioInfluencer** that is no longer encountered, call the **RemoveEffect** method.</span></span>

<span data-ttu-id="2da97-305">Notez que AudioEmitter met à jour sur les échelles de temps humain, par opposition à sur une trame par trame.</span><span class="sxs-lookup"><span data-stu-id="2da97-305">Note that AudioEmitter updates on human time scales, as opposed to on a per frame basis.</span></span> <span data-ttu-id="2da97-306">Pour cela, car l’homme généralement ne se déplace pas assez rapide pour l’effet de mettre à jour plus fréquemment que tous les trimestres ou d’une demie seconde.</span><span class="sxs-lookup"><span data-stu-id="2da97-306">This is done because humans generally do not move fast enough for the effect to need to be updated more frequently than every quarter or half of a second.</span></span> <span data-ttu-id="2da97-307">Hologrammes ce teleport rapidement d’un emplacement vers un autre peut interrompre l’illusion.</span><span class="sxs-lookup"><span data-stu-id="2da97-307">Holograms that teleport rapidly from one location to another can break the illusion.</span></span>

* <span data-ttu-id="2da97-308">Dans le **hiérarchie** volet, développez **HologramCollection**.</span><span class="sxs-lookup"><span data-stu-id="2da97-308">In the **Hierarchy** panel, expand **HologramCollection**.</span></span>
* <span data-ttu-id="2da97-309">Développez **EnergyHub** et sélectionnez **BlobOutside**.</span><span class="sxs-lookup"><span data-stu-id="2da97-309">Expand **EnergyHub** and select **BlobOutside**.</span></span>
* <span data-ttu-id="2da97-310">Dans le **inspecteur** du panneau, cliquez sur **ajouter un composant** et ajoutez **Audio OCCLUSION**.</span><span class="sxs-lookup"><span data-stu-id="2da97-310">In the **Inspector** panel, click **Add Component** and add **Audio Occluder**.</span></span>
* <span data-ttu-id="2da97-311">Dans **Audio OCCLUSION**, affectez la valeur **fréquence de coupure** à **1500**.</span><span class="sxs-lookup"><span data-stu-id="2da97-311">In **Audio Occluder**, set **Cutoff Frequency** to **1500**.</span></span>

<span data-ttu-id="2da97-312">Ce paramètre limite les fréquences AudioSource à 1 500 Hz et versions antérieures.</span><span class="sxs-lookup"><span data-stu-id="2da97-312">This setting limits the AudioSource frequencies to 1500 Hz and below.</span></span>

* <span data-ttu-id="2da97-313">Définissez **Volume passthrough** à **0.9**.</span><span class="sxs-lookup"><span data-stu-id="2da97-313">Set **Volume Pass Through** to **0.9**.</span></span>

<span data-ttu-id="2da97-314">Ce paramètre réduit le volume de la AudioSource à 90 % de son niveau actuel.</span><span class="sxs-lookup"><span data-stu-id="2da97-314">This setting reduces the volume of the AudioSource to 90% of it's current level.</span></span>

<span data-ttu-id="2da97-315">Audio OCCLUSION implémente IAudioInfluencer à :</span><span class="sxs-lookup"><span data-stu-id="2da97-315">Audio Occluder implements IAudioInfluencer to:</span></span>

* <span data-ttu-id="2da97-316">Appliquer un effet d’occlusion à l’aide un **AudioLowPassFilter** qui est attaché à la **AudioSource** managé acheter le **AudioEmitter**.</span><span class="sxs-lookup"><span data-stu-id="2da97-316">Apply an occlusion effect using an **AudioLowPassFilter** which gets attached to the **AudioSource** managed buy the **AudioEmitter**.</span></span>
* <span data-ttu-id="2da97-317">S’applique à atténuation de volume à la AudioSource.</span><span class="sxs-lookup"><span data-stu-id="2da97-317">Applies volume attenuation to the AudioSource.</span></span>
* <span data-ttu-id="2da97-318">Désactive l’effet en définissant une fréquence de coupure neutre et de la désactivation du filtre.</span><span class="sxs-lookup"><span data-stu-id="2da97-318">Disables the effect by setting a neutral cutoff frequency and disabling the filter.</span></span>

<span data-ttu-id="2da97-319">La fréquence utilisée comme neutre est 22 kHz (22000 Hz).</span><span class="sxs-lookup"><span data-stu-id="2da97-319">The frequency used as neutral is 22 kHz (22000 Hz).</span></span> <span data-ttu-id="2da97-320">Cette fréquence a été choisie car elles sont au-dessus de la fréquence maximale nominale pouvant être entendu l’oreille humaine, cette aucun impact notable rendre le son.</span><span class="sxs-lookup"><span data-stu-id="2da97-320">This frequency was chosen due to it being above the nominal maximum frequency that can be heard by the human ear, this making no discernable impact to the sound.</span></span>

* <span data-ttu-id="2da97-321">Dans le **hiérarchie** panneau, sélectionnez **SpatialMapping**.</span><span class="sxs-lookup"><span data-stu-id="2da97-321">In the **Hierarchy** panel, select **SpatialMapping**.</span></span>
* <span data-ttu-id="2da97-322">Dans le **inspecteur** du panneau, cliquez sur **ajouter un composant** et ajoutez **Audio OCCLUSION**.</span><span class="sxs-lookup"><span data-stu-id="2da97-322">In the **Inspector** panel, click **Add Component** and add **Audio Occluder**.</span></span>
* <span data-ttu-id="2da97-323">Dans **Audio OCCLUSION**, affectez la valeur **fréquence de coupure** à **750**.</span><span class="sxs-lookup"><span data-stu-id="2da97-323">In **Audio Occluder**, set **Cutoff Frequency** to **750**.</span></span>

<span data-ttu-id="2da97-324">Lorsque plusieurs occluders se trouvent dans le chemin d’accès entre l’utilisateur et le **AudioEmitter**, la fréquence de la plus basse est appliquée au filtre.</span><span class="sxs-lookup"><span data-stu-id="2da97-324">When multiple occluders are in the path between the user and the **AudioEmitter**, the lowest frequency is applied to the filter.</span></span>

* <span data-ttu-id="2da97-325">Définissez **Volume passthrough** à **0,75**.</span><span class="sxs-lookup"><span data-stu-id="2da97-325">Set **Volume Pass Through** to **0.75**.</span></span>

<span data-ttu-id="2da97-326">Lorsque plusieurs occluders se trouvent dans le chemin d’accès entre l’utilisateur et le **AudioEmitter**, le volume passthrough est appliqué en feu.</span><span class="sxs-lookup"><span data-stu-id="2da97-326">When multiple occluders are in the path between the user and the **AudioEmitter**, the volume pass through is applied additively.</span></span>

* <span data-ttu-id="2da97-327">Dans le **hiérarchie** panneau, sélectionnez **gestionnaires**.</span><span class="sxs-lookup"><span data-stu-id="2da97-327">In the **Hierarchy** panel, select **Managers**.</span></span>
* <span data-ttu-id="2da97-328">Dans le **inspecteur** volet, développez **Gestionnaire d’entrée vocale**.</span><span class="sxs-lookup"><span data-stu-id="2da97-328">In the **Inspector** panel, expand **Speech Input Handler**.</span></span>
* <span data-ttu-id="2da97-329">Dans **Gestionnaire d’entrée vocale**, développez **frais accédez**.</span><span class="sxs-lookup"><span data-stu-id="2da97-329">In **Speech Input Handler**, expand **Go Charge**.</span></span>
* <span data-ttu-id="2da97-330">Modification **aucune fonction** à **PolyActions.GoCharge**.</span><span class="sxs-lookup"><span data-stu-id="2da97-330">Change **No Function** to **PolyActions.GoCharge**.</span></span>

![mot clé : Accédez de frais](images/gocharge.png)

* <span data-ttu-id="2da97-332">Développez **ici**.</span><span class="sxs-lookup"><span data-stu-id="2da97-332">Expand **Come Here**.</span></span>
* <span data-ttu-id="2da97-333">Modification **aucune fonction** à **PolyActions.ComeBack**.</span><span class="sxs-lookup"><span data-stu-id="2da97-333">Change **No Function** to **PolyActions.ComeBack**.</span></span>

![mot clé : Viens ici](images/comehere.png)

#### <a name="build-and-deploy"></a><span data-ttu-id="2da97-335">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="2da97-335">Build and Deploy</span></span>

* <span data-ttu-id="2da97-336">Comme précédemment, générez le projet dans Unity et déployés dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2da97-336">As before, build the project in Unity and deploy in Visual Studio.</span></span>

<span data-ttu-id="2da97-337">Une fois que l’application est déployée :</span><span class="sxs-lookup"><span data-stu-id="2da97-337">After the application is deployed:</span></span>

* <span data-ttu-id="2da97-338">Par exemple *« Accédez frais »* avoir P0LY Entrez le Hub d’énergie.</span><span class="sxs-lookup"><span data-stu-id="2da97-338">Say *"Go Charge"* to have P0LY enter the Energy Hub.</span></span>

<span data-ttu-id="2da97-339">Notez le changement dans le son.</span><span class="sxs-lookup"><span data-stu-id="2da97-339">Note the change in the sound.</span></span> <span data-ttu-id="2da97-340">Cela doit sembler des et un peu plus calme.</span><span class="sxs-lookup"><span data-stu-id="2da97-340">It should sound muffled and a little quieter.</span></span> <span data-ttu-id="2da97-341">Si vous êtes en mesure de vous positionner avec un mur ou un autre objet entre vous et le Hub de l’énergie, vous devriez remarquer un muffling supplémentaire du son en raison de l’occlusion par le monde réel.</span><span class="sxs-lookup"><span data-stu-id="2da97-341">If you are able to position yourself with a wall or other object between you and the Energy Hub, you should notice a further muffling of the sound due to the occlusion by the real world.</span></span>

* <span data-ttu-id="2da97-342">Par exemple *« Sont fournis ici »* avoir P0LY laisser le Hub d’énergie et se positionner devant vous.</span><span class="sxs-lookup"><span data-stu-id="2da97-342">Say *"Come Here"* to have P0LY leave the Energy Hub and position itself in front of you.</span></span>

<span data-ttu-id="2da97-343">Notez que l’occlusion audio est supprimée une fois que P0LY quitte le Hub d’énergie.</span><span class="sxs-lookup"><span data-stu-id="2da97-343">Note that the sound occlusion is removed once P0LY exits the Energy Hub.</span></span> <span data-ttu-id="2da97-344">Si vous êtes toujours occlusion d’Audition, P0LY peuvent être bloqués par le monde réel.</span><span class="sxs-lookup"><span data-stu-id="2da97-344">If you are still hearing occlusion, P0LY may be occluded by the real world.</span></span> <span data-ttu-id="2da97-345">Essayez de déplacer pour vous assurer une délimitation nette à P0LY.</span><span class="sxs-lookup"><span data-stu-id="2da97-345">Try moving to ensure you have a clear line of sight to P0LY.</span></span>

### <a name="part-3---room-models"></a><span data-ttu-id="2da97-346">Partie 3 : modèles de la salle</span><span class="sxs-lookup"><span data-stu-id="2da97-346">Part 3 - Room Models</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="2da97-347">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="2da97-347">Key Concepts</span></span>

* <span data-ttu-id="2da97-348">La taille de l’espace fournit des files d’attente subliminales qui contribuent à la localisation d’un son.</span><span class="sxs-lookup"><span data-stu-id="2da97-348">The size of the space provides subliminal queues that contribute to sound localization.</span></span>
* <span data-ttu-id="2da97-349">Modèles de salle sont définies par-**AudioSource**.</span><span class="sxs-lookup"><span data-stu-id="2da97-349">Room models are set per-**AudioSource**.</span></span>
* <span data-ttu-id="2da97-350">Le [MixedRealityToolkit pour Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity) fournit du code pour la définition du modèle de la salle.</span><span class="sxs-lookup"><span data-stu-id="2da97-350">The [MixedRealityToolkit for Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity) provides code for setting the room model.</span></span>
* <span data-ttu-id="2da97-351">Pour des expériences de réalité mixte, sélectionnez le modèle d’espace qui convient le mieux à l’espace du monde réel.</span><span class="sxs-lookup"><span data-stu-id="2da97-351">For Mixed Reality experiences, select the room model that best fits the real world space.</span></span>

<span data-ttu-id="2da97-352">Si vous créez un scénario de réalité virtuelle, sélectionnez le modèle d’espace qui convient le mieux à l’environnement virtuel.</span><span class="sxs-lookup"><span data-stu-id="2da97-352">If you are creating a Virtual Reality scenario, select the room model that best fits the virtual environment.</span></span>

## <a name="chapter-4---sound-design"></a><span data-ttu-id="2da97-353">Chapitre 4 - sonorisation</span><span class="sxs-lookup"><span data-stu-id="2da97-353">Chapter 4 - Sound Design</span></span>

### <a name="objectives"></a><span data-ttu-id="2da97-354">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2da97-354">Objectives</span></span>

* <span data-ttu-id="2da97-355">Comprendre les considérations relatives à la conception audio efficace.</span><span class="sxs-lookup"><span data-stu-id="2da97-355">Understand considerations for effective sound design.</span></span>
* <span data-ttu-id="2da97-356">Découvrez des techniques et des instructions mixtes.</span><span class="sxs-lookup"><span data-stu-id="2da97-356">Learn mixing techniques and guidelines.</span></span>

### <a name="part-1---sound-and-experience-design"></a><span data-ttu-id="2da97-357">Partie 1 : conception de l’expérience et de son</span><span class="sxs-lookup"><span data-stu-id="2da97-357">Part 1 - Sound and Experience Design</span></span>

<span data-ttu-id="2da97-358">Cette section décrit la bonne clé et de considérations de conception d’expérience et de recommandations.</span><span class="sxs-lookup"><span data-stu-id="2da97-358">This section discusses key sound and experience design considerations and guidelines.</span></span>

#### <a name="normalize-all-sounds"></a><span data-ttu-id="2da97-359">Normaliser toutes les sons</span><span class="sxs-lookup"><span data-stu-id="2da97-359">Normalize all sounds</span></span>

<span data-ttu-id="2da97-360">Cela évite la nécessité d’un code cas spécial régler les niveaux de volume par son, qui peut prendre du temps et limite la possibilité de mettre à jour facilement des fichiers audio.</span><span class="sxs-lookup"><span data-stu-id="2da97-360">This avoids the need for special case code to adjust volume levels per sound, which can be time consuming and limits the ability to easily update sound files.</span></span>

#### <a name="design-for-an-untethered-experience"></a><span data-ttu-id="2da97-361">Conception pour une expérience librement</span><span class="sxs-lookup"><span data-stu-id="2da97-361">Design for an untethered experience</span></span>

<span data-ttu-id="2da97-362">HoloLens est un ordinateur entièrement contenu, librement HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="2da97-362">HoloLens is a fully contained, untethered holographic computer.</span></span> <span data-ttu-id="2da97-363">Vos utilisateurs peuvent et utilisera vos expériences lors du déplacement.</span><span class="sxs-lookup"><span data-stu-id="2da97-363">Your users can and will use your experiences while moving.</span></span> <span data-ttu-id="2da97-364">Veillez à tester votre combinaison audio en parcourant autour.</span><span class="sxs-lookup"><span data-stu-id="2da97-364">Be sure to test your audio mix by walking around.</span></span>

#### <a name="emit-sound-from-logical-locations-on-your-holograms"></a><span data-ttu-id="2da97-365">Émettre le signal sonore à partir d’emplacements logiques sur votre hologrammes</span><span class="sxs-lookup"><span data-stu-id="2da97-365">Emit sound from logical locations on your holograms</span></span>

<span data-ttu-id="2da97-366">Dans le monde réel, un chien ne pas écorce de sa fin et les voix d’un humain ne provient pas de son pieds.</span><span class="sxs-lookup"><span data-stu-id="2da97-366">In the real world, a dog does not bark from its tail and a human's voice does not come from his/her feet.</span></span> <span data-ttu-id="2da97-367">Évitez d’avoir que votre sons émettent à partir de parties inattendues de votre hologrammes.</span><span class="sxs-lookup"><span data-stu-id="2da97-367">Avoid having your sounds emit from unexpected portions of your holograms.</span></span>

<span data-ttu-id="2da97-368">Pour hologrammes petits, il est raisonnable d’avoir son émission à partir du centre de la géométrie.</span><span class="sxs-lookup"><span data-stu-id="2da97-368">For small holograms, it is reasonable to have sound emit from the center of the geometry.</span></span>

#### <a name="familiar-sounds-are-most-localizable"></a><span data-ttu-id="2da97-369">Sons familiers sont plus localisables</span><span class="sxs-lookup"><span data-stu-id="2da97-369">Familiar sounds are most localizable</span></span>

<span data-ttu-id="2da97-370">La voix humaine et la musique sont très faciles à localiser.</span><span class="sxs-lookup"><span data-stu-id="2da97-370">The human voice and music are very easy to localize.</span></span> <span data-ttu-id="2da97-371">Si quelqu'un appelle votre nom, vous êtes en mesure de déterminer très précisément à partir de quel sens provient de la voix et de l’éloignement.</span><span class="sxs-lookup"><span data-stu-id="2da97-371">If someone calls your name, you are able to very accurately determine from what direction the voice came and from how far away.</span></span> <span data-ttu-id="2da97-372">Sons courts et non connus sont plus difficiles à localiser.</span><span class="sxs-lookup"><span data-stu-id="2da97-372">Short, unfamiliar sounds are harder to localize.</span></span>

#### <a name="be-cognizant-of-user-expectations"></a><span data-ttu-id="2da97-373">Être informé des attentes des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="2da97-373">Be cognizant of user expectations</span></span>

<span data-ttu-id="2da97-374">Expérience de la vie joue un rôle dans notre capacité à identifier l’emplacement d’un son.</span><span class="sxs-lookup"><span data-stu-id="2da97-374">Life experience plays a part in our ability to identify the location of a sound.</span></span> <span data-ttu-id="2da97-375">Il s’agit d’une seule raison pour laquelle la voix humaine particulièrement facile à localiser.</span><span class="sxs-lookup"><span data-stu-id="2da97-375">This is one reason why the human voice is particularly easy to localize.</span></span> <span data-ttu-id="2da97-376">Il est important de connaître votre appris attentes des utilisateurs lorsque vous placez votre sons.</span><span class="sxs-lookup"><span data-stu-id="2da97-376">It is important to be aware of your user's learned expectations when placing your sounds.</span></span>

<span data-ttu-id="2da97-377">Par exemple, lorsqu’une personne entend une chanson bird ils généralement recherchent, comme oiseaux ont tendance à être au-dessus de la ligne de vue (flottantes ou dans une arborescence).</span><span class="sxs-lookup"><span data-stu-id="2da97-377">For example, when someone hears a bird song they generally look up, as birds tend to be above the line of sight (flying or in a tree).</span></span> <span data-ttu-id="2da97-378">Il n’est pas rare pour un utilisateur à activer dans la direction correcte d’un son, mais Regarder dans la mauvaise direction verticale et devenir confus ou frustré lorsqu’ils ne peuvent pas trouver l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="2da97-378">It is not uncommon for a user to turn in the correct direction of a sound, but look in the wrong vertical direction and become confused or frustrated when they are unable to find the hologram.</span></span>

#### <a name="avoid-hidden-emitters"></a><span data-ttu-id="2da97-379">Éviter les émetteurs masqués</span><span class="sxs-lookup"><span data-stu-id="2da97-379">Avoid hidden emitters</span></span>

<span data-ttu-id="2da97-380">Dans le monde réel, si nous entendre un son, nous pouvons identifier généralement l’objet qui émet le son.</span><span class="sxs-lookup"><span data-stu-id="2da97-380">In the real world, if we hear a sound, we can generally identify the object that is emitting the sound.</span></span> <span data-ttu-id="2da97-381">Ceci est également valable dans vos expériences.</span><span class="sxs-lookup"><span data-stu-id="2da97-381">This should also hold true in your experiences.</span></span> <span data-ttu-id="2da97-382">Il peut être très déconcertante pour les utilisateurs et émet un son, de savoir où le son provient et pourra consulter un objet.</span><span class="sxs-lookup"><span data-stu-id="2da97-382">It can be very disconcerting for users to hear a sound, know from where the sound originates and be unable to see an object.</span></span>

<span data-ttu-id="2da97-383">Il existe quelques exceptions à cette recommandation.</span><span class="sxs-lookup"><span data-stu-id="2da97-383">There are some exceptions to this guideline.</span></span> <span data-ttu-id="2da97-384">Par exemple, des sons ambiantes comme crickets dans un champ ne sont pas nécessairement visibles.</span><span class="sxs-lookup"><span data-stu-id="2da97-384">For example, ambient sounds such as crickets in a field need not be visible.</span></span> <span data-ttu-id="2da97-385">Expérience de la vie nous donne vous êtes familiarisé avec la source de ces sons sans la nécessité pour l’afficher.</span><span class="sxs-lookup"><span data-stu-id="2da97-385">Life experience gives us familiarity with the source of these sounds without the need to see it.</span></span>

### <a name="part-2---sound-mixing"></a><span data-ttu-id="2da97-386">Partie 2 - mixage</span><span class="sxs-lookup"><span data-stu-id="2da97-386">Part 2 - Sound Mixing</span></span>

#### <a name="target-your-mix-for-70-volume-on-the-hololens"></a><span data-ttu-id="2da97-387">Cibler votre combinaison de volume de 70 % sur le HoloLens</span><span class="sxs-lookup"><span data-stu-id="2da97-387">Target your mix for 70% volume on the HoloLens</span></span>

<span data-ttu-id="2da97-388">Expériences de réalité mixtes autoriser hologrammes être affichés dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="2da97-388">Mixed Reality experiences allow holograms to be seen in the real world.</span></span> <span data-ttu-id="2da97-389">Ils doivent également autoriser sons du monde réel à entendre.</span><span class="sxs-lookup"><span data-stu-id="2da97-389">They should also allow real world sounds to be heard.</span></span> <span data-ttu-id="2da97-390">Une cible de 70 % volume permet à l’utilisateur d’entendre le monde autour d’elles, ainsi que le son de votre expérience.</span><span class="sxs-lookup"><span data-stu-id="2da97-390">A 70% volume target enables the user to hear the world around them along with the sound of your experience.</span></span>

#### <a name="hololens-at-100-volume-should-drown-out-external-sounds"></a><span data-ttu-id="2da97-391">HoloLens à 100 % de volume vous noyer doit les sons externes</span><span class="sxs-lookup"><span data-stu-id="2da97-391">HoloLens at 100% volume should drown out external sounds</span></span>

<span data-ttu-id="2da97-392">Un niveau de volume de 100 % équivaut à une expérience de réalité virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2da97-392">A volume level of 100% is akin to a Virtual Reality experience.</span></span> <span data-ttu-id="2da97-393">Visuellement, l’utilisateur est transféré vers un monde différent.</span><span class="sxs-lookup"><span data-stu-id="2da97-393">Visually, the user is transported to a different world.</span></span> <span data-ttu-id="2da97-394">Les mêmes valable façon audible.</span><span class="sxs-lookup"><span data-stu-id="2da97-394">The same should hold true audibly.</span></span>

#### <a name="use-the-unity-audiomixer-to-adjust-categories-of-sounds"></a><span data-ttu-id="2da97-395">Utiliser le AudioMixer Unity pour ajuster les catégories de sons</span><span class="sxs-lookup"><span data-stu-id="2da97-395">Use the Unity AudioMixer to adjust categories of sounds</span></span>

<span data-ttu-id="2da97-396">Lorsque vous concevez votre combinaison, il est souvent utile de créer des catégories de sons et ont la possibilité d’augmenter ou diminuer leur volume en tant qu’unité.</span><span class="sxs-lookup"><span data-stu-id="2da97-396">When designing your mix, it is often helpful to create sound categories and have the ability to increase or decrease their volume as a unit.</span></span> <span data-ttu-id="2da97-397">Cela conserve les niveaux relatifs de chaque signal sonore lors de l’activation rapides et faciles des modifications à la combinaison générale.</span><span class="sxs-lookup"><span data-stu-id="2da97-397">This retains the relative levels of each sound while enabling quick and easy changes to the overall mix.</span></span> <span data-ttu-id="2da97-398">Incluent des catégories courantes ; effets sonores, ambiance, montages audio et musique de fond.</span><span class="sxs-lookup"><span data-stu-id="2da97-398">Common categories include; sound effects, ambience, voice overs and background music.</span></span>

#### <a name="mix-sounds-based-on-the-users-gaze"></a><span data-ttu-id="2da97-399">Combiner des sons selon le regard de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2da97-399">Mix sounds based on the user's gaze</span></span>

<span data-ttu-id="2da97-400">Il peut souvent être utile d’en modifier la combinaison de sonore dans votre expérience selon où un utilisateur est (ou n’est pas) la recherche.</span><span class="sxs-lookup"><span data-stu-id="2da97-400">It can often be useful to change the sound mix in your experience based on where a user is (or is not) looking.</span></span> <span data-ttu-id="2da97-401">Une utilisation courante de cette technique sont afin de réduire le niveau de volume pour hologrammes qui se trouvent en dehors de la trame HOLOGRAPHIQUE pour faciliter le travail de l’utilisateur pour vous concentrer sur les informations devant eux.</span><span class="sxs-lookup"><span data-stu-id="2da97-401">One common use for this technique are to reduce the volume level for holograms that are outside of the Holographic Frame to make it easier for the user to focus on the information in front of them.</span></span> <span data-ttu-id="2da97-402">Une autre utilisation consiste à augmenter le volume d’un son pour attirer l’attention de l’utilisateur à un événement important.</span><span class="sxs-lookup"><span data-stu-id="2da97-402">Another use is to increase the volume of a sound to draw the user's attention to an important event.</span></span>

#### <a name="building-your-mix"></a><span data-ttu-id="2da97-403">Création de votre combinaison</span><span class="sxs-lookup"><span data-stu-id="2da97-403">Building your mix</span></span>

<span data-ttu-id="2da97-404">Lorsque vous générez votre combinaison, il est recommandé de démarrer avec audio d’arrière-plan de votre expérience et ajouter des couches en fonction de l’importance.</span><span class="sxs-lookup"><span data-stu-id="2da97-404">When building your mix, it is recommended to start with your experience's background audio and add layers based on importance.</span></span> <span data-ttu-id="2da97-405">Souvent, cela entraîne dans chaque couche en cours plus bruyant que le précédent.</span><span class="sxs-lookup"><span data-stu-id="2da97-405">Often, this results in each layer being louder than the previous.</span></span>

<span data-ttu-id="2da97-406">Imaginer votre combinaison comme un entonnoir inversé, avec le moins important (et généralement plus calmes sons) en bas, il est recommandé de structurer votre combinaison similaire au diagramme suivant.</span><span class="sxs-lookup"><span data-stu-id="2da97-406">Imagining your mix as an inverted funnel, with the least important (and generally quietest sounds) at the bottom, it is recommended to structure your mix similar to the following diagram.</span></span>

![Structure de mixage audio](images/soundlevels.png)

<span data-ttu-id="2da97-408">Montages audio sont un scénario intéressant.</span><span class="sxs-lookup"><span data-stu-id="2da97-408">Voice overs are an interesting scenario.</span></span> <span data-ttu-id="2da97-409">Basé sur l’expérience que vous créez, vous pouvez avoir un son stéréo (non localisé) ou spatialize votre montages audio.</span><span class="sxs-lookup"><span data-stu-id="2da97-409">Based on the experience you are creating you may wish to have a stereo (not localized) sound or to spatialize your voice overs.</span></span> <span data-ttu-id="2da97-410">Deux Microsoft a publié des expériences illustrer d’excellents exemples de chaque scénario.</span><span class="sxs-lookup"><span data-stu-id="2da97-410">Two Microsoft published experiences illustrate excellent examples of each scenario.</span></span>

<span data-ttu-id="2da97-411">[HoloTour](http://www.microsoft.com/store/p/holotour/9nblggh5pj87) utilise une voix stéréo sur.</span><span class="sxs-lookup"><span data-stu-id="2da97-411">[HoloTour](http://www.microsoft.com/store/p/holotour/9nblggh5pj87) uses a stereo voice over.</span></span> <span data-ttu-id="2da97-412">Lorsque le Narrateur est décrivant l’emplacement en cours de visualisation, le son est cohérent et ne varie pas en position de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2da97-412">When the narrator is describing the location being viewed, the sound is consistent and does not vary based on the user's position.</span></span> <span data-ttu-id="2da97-413">Ainsi, le Narrateur décrire la scène sans prise de sons spatialized de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="2da97-413">This enables the narrator to describe the scene without taking away from the spatialized sounds of the environment.</span></span>

<span data-ttu-id="2da97-414">[Fragments](https://www.microsoft.com/store/p/fragments/9nblggh5ggm8) utilise une voix spatialized sur sous la forme d’un détective.</span><span class="sxs-lookup"><span data-stu-id="2da97-414">[Fragments](https://www.microsoft.com/store/p/fragments/9nblggh5ggm8) utilizes a spatialized voice over in the form of a detective.</span></span> <span data-ttu-id="2da97-415">Voix de sa est utilisé pour aider à attirer l’attention de l’utilisateur à un indice important comme si un homme réel a été dans la salle.</span><span class="sxs-lookup"><span data-stu-id="2da97-415">The detective's voice is used to help bring the user's attention to an important clue as if an actual human was in the room.</span></span> <span data-ttu-id="2da97-416">Cela permet une encore plu judicieux d’immersion dans l’expérience de résolution le mystère.</span><span class="sxs-lookup"><span data-stu-id="2da97-416">This enables an even greater sense of immersion into the experience of solving the mystery.</span></span>

### <a name="part-3--performance"></a><span data-ttu-id="2da97-417">Partie 3 - performances</span><span class="sxs-lookup"><span data-stu-id="2da97-417">Part 3 -Performance</span></span>

#### <a name="cpu-usage"></a><span data-ttu-id="2da97-418">Utilisation du processeur</span><span class="sxs-lookup"><span data-stu-id="2da97-418">CPU usage</span></span>

<span data-ttu-id="2da97-419">Lorsque vous utilisez Spatial son, 10-12 émetteurs consomme environ 12 % de l’UC.</span><span class="sxs-lookup"><span data-stu-id="2da97-419">When using Spatial Sound, 10 - 12 emitters will consume approximately 12% of the CPU.</span></span>

#### <a name="stream-long-audio-files"></a><span data-ttu-id="2da97-420">Fichiers audio long Stream</span><span class="sxs-lookup"><span data-stu-id="2da97-420">Stream long audio files</span></span>

<span data-ttu-id="2da97-421">Données audio peuvent être volumineuses, en particulier à des taux d’échantillonnage (kHz 44,1 et 48) courants.</span><span class="sxs-lookup"><span data-stu-id="2da97-421">Audio data can be large, especially at common sample rates (44.1 and 48 kHz).</span></span> <span data-ttu-id="2da97-422">Une règle générale est que les fichiers audio plus de 5 à 10 secondes doivent être diffusé en continu afin de réduire l’utilisation mémoire des applications.</span><span class="sxs-lookup"><span data-stu-id="2da97-422">A general rule is that audio files longer than 5 - 10 seconds should be streamed to reduce application memory usage.</span></span>

<span data-ttu-id="2da97-423">Dans Unity, vous pouvez marquer un fichier audio pour la diffusion en continu dans les paramètres d’importation du fichier.</span><span class="sxs-lookup"><span data-stu-id="2da97-423">In Unity, you can mark an audio file for streaming in the file's import settings.</span></span>

![Paramètres d’importation audio](images/audioimportsettings.png)

## <a name="chapter-5---special-effects"></a><span data-ttu-id="2da97-425">Chapitre 5 - effets spéciaux</span><span class="sxs-lookup"><span data-stu-id="2da97-425">Chapter 5 - Special Effects</span></span>

### <a name="objectives"></a><span data-ttu-id="2da97-426">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2da97-426">Objectives</span></span>

* <span data-ttu-id="2da97-427">Ajout de profondeur à « Magic Windows ».</span><span class="sxs-lookup"><span data-stu-id="2da97-427">Add depth to "Magic Windows".</span></span>
* <span data-ttu-id="2da97-428">Placer l’utilisateur dans le monde virtuel.</span><span class="sxs-lookup"><span data-stu-id="2da97-428">Bring the user into the virtual world.</span></span>

### <a name="magic-windows"></a><span data-ttu-id="2da97-429">Magic Windows</span><span class="sxs-lookup"><span data-stu-id="2da97-429">Magic Windows</span></span>

#### <a name="key-concepts"></a><span data-ttu-id="2da97-430">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="2da97-430">Key Concepts</span></span>

* <span data-ttu-id="2da97-431">Création de vues dans un monde masqué, est visuellement attrayante.</span><span class="sxs-lookup"><span data-stu-id="2da97-431">Creating views into a hidden world, is visually compelling.</span></span>
* <span data-ttu-id="2da97-432">Améliorer réalisme en ajoutant des effets audio lorsqu’un hologramme ou l’utilisateur est presque le monde masqué.</span><span class="sxs-lookup"><span data-stu-id="2da97-432">Enhance realism by adding audio effects when a hologram or the user is near the hidden world.</span></span>

#### <a name="instructions"></a><span data-ttu-id="2da97-433">Instructions</span><span class="sxs-lookup"><span data-stu-id="2da97-433">Instructions</span></span>

* <span data-ttu-id="2da97-434">Dans le **hiérarchie** volet, développez **HologramCollection** et sélectionnez **Underworld**.</span><span class="sxs-lookup"><span data-stu-id="2da97-434">In the **Hierarchy** panel, expand **HologramCollection** and select **Underworld**.</span></span>
* <span data-ttu-id="2da97-435">Développez **Underworld** et sélectionnez **VoiceSource**.</span><span class="sxs-lookup"><span data-stu-id="2da97-435">Expand **Underworld** and select **VoiceSource**.</span></span>
* <span data-ttu-id="2da97-436">Dans le **inspecteur** du panneau, cliquez sur **ajouter un composant** et ajoutez **effet de voix utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="2da97-436">In the **Inspector** panel, click **Add Component** and add **User Voice Effect**.</span></span>

<span data-ttu-id="2da97-437">Un **AudioSource** composant sera ajouté à **VoiceSource**.</span><span class="sxs-lookup"><span data-stu-id="2da97-437">An **AudioSource** component will be added to **VoiceSource**.</span></span>

* <span data-ttu-id="2da97-438">Dans **AudioSource**, affectez la valeur **sortie** à **UserVoice (Mixer)**.</span><span class="sxs-lookup"><span data-stu-id="2da97-438">In **AudioSource**, set **Output** to **UserVoice (Mixer)**.</span></span>
* <span data-ttu-id="2da97-439">Vérifier le **Spatialize** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="2da97-439">Check the **Spatialize** checkbox.</span></span>
* <span data-ttu-id="2da97-440">Faites glisser le **Blend Spatial** curseur jusqu’au **3D**, ou entrez **1** dans la zone d’édition.</span><span class="sxs-lookup"><span data-stu-id="2da97-440">Drag the **Spatial Blend** slider all the way to **3D**, or enter **1** in the edit box.</span></span>
* <span data-ttu-id="2da97-441">Développez **paramètres audio 3D**.</span><span class="sxs-lookup"><span data-stu-id="2da97-441">Expand **3D Sound Settings**.</span></span>
* <span data-ttu-id="2da97-442">Définissez **Doppler niveau** à **0**.</span><span class="sxs-lookup"><span data-stu-id="2da97-442">Set **Doppler Level** to **0**.</span></span>
* <span data-ttu-id="2da97-443">Dans **effet de voix utilisateur**, affectez la valeur **objet Parent** à la **Underworld** à partir de la scène.</span><span class="sxs-lookup"><span data-stu-id="2da97-443">In **User Voice Effect**, set **Parent Object** to the **Underworld** from the scene.</span></span>
* <span data-ttu-id="2da97-444">Définissez **Max Distance** à **1**.</span><span class="sxs-lookup"><span data-stu-id="2da97-444">Set **Max Distance** to **1**.</span></span>

<span data-ttu-id="2da97-445">Paramètre **Max Distance** indique **effet de voix utilisateur** comment fermer l’utilisateur doit être l’objet parent avant l’effet est activé.</span><span class="sxs-lookup"><span data-stu-id="2da97-445">Setting **Max Distance** tells **User Voice Effect** how close the user must be to the parent object before the effect is enabled.</span></span>

* <span data-ttu-id="2da97-446">Dans **effet de voix utilisateur**, développez **chaleureusement Robert paramètres**.</span><span class="sxs-lookup"><span data-stu-id="2da97-446">In **User Voice Effect**, expand **Chorus Parameters**.</span></span>
* <span data-ttu-id="2da97-447">Définissez **profondeur** à **0.1**.</span><span class="sxs-lookup"><span data-stu-id="2da97-447">Set **Depth** to **0.1**.</span></span>
* <span data-ttu-id="2da97-448">Définissez **appuyez sur 1 Volume**, **appuyez sur le Volume 2** et **appuyez sur le Volume 3** à **0.8**.</span><span class="sxs-lookup"><span data-stu-id="2da97-448">Set **Tap 1 Volume**, **Tap 2 Volume** and **Tap 3 Volume** to **0.8**.</span></span>
* <span data-ttu-id="2da97-449">Définissez **d’origine son Volume** à **0,5**.</span><span class="sxs-lookup"><span data-stu-id="2da97-449">Set **Original Sound Volume** to **0.5**.</span></span>

<span data-ttu-id="2da97-450">Les paramètres précédents configurent les paramètres de l’unité **AudioChorusFilter** permettant d’ajouter la richesse de voix de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2da97-450">The previous settings configure the parameters of the Unity **AudioChorusFilter** used to add richness to the user's voice.</span></span>

* <span data-ttu-id="2da97-451">Dans **effet de voix utilisateur**, développez **Echo paramètres**.</span><span class="sxs-lookup"><span data-stu-id="2da97-451">In **User Voice Effect**, expand **Echo Parameters**.</span></span>
* <span data-ttu-id="2da97-452">Définissez **délai** à **300**</span><span class="sxs-lookup"><span data-stu-id="2da97-452">Set **Delay** to **300**</span></span>
* <span data-ttu-id="2da97-453">Définissez **Decay, Ratio** à **0.2**.</span><span class="sxs-lookup"><span data-stu-id="2da97-453">Set **Decay Ratio** to **0.2**.</span></span>
* <span data-ttu-id="2da97-454">Définissez **d’origine son Volume** à **0**.</span><span class="sxs-lookup"><span data-stu-id="2da97-454">Set **Original Sound Volume** to **0**.</span></span>

<span data-ttu-id="2da97-455">Les paramètres précédents configurent les paramètres de l’unité **AudioEchoFilter** utilisée pour provoquer la voix de l’utilisateur à renvoyer.</span><span class="sxs-lookup"><span data-stu-id="2da97-455">The previous settings configure the parameters of the Unity **AudioEchoFilter** used to cause the user's voice to echo.</span></span>

<span data-ttu-id="2da97-456">Le script de l’effet de voix utilisateur est chargé de :</span><span class="sxs-lookup"><span data-stu-id="2da97-456">The User Voice Effect script is responsible for:</span></span>

* <span data-ttu-id="2da97-457">Mesure de la distance entre l’utilisateur et le **GameObject** auquel le script est joint.</span><span class="sxs-lookup"><span data-stu-id="2da97-457">Measuring the distance between the user and the **GameObject** to which the script is attached.</span></span>
* <span data-ttu-id="2da97-458">Déterminer si l’utilisateur est accessible sur le **GameObject**.</span><span class="sxs-lookup"><span data-stu-id="2da97-458">Determining whether or not the user is facing the **GameObject**.</span></span>

<span data-ttu-id="2da97-459">L’utilisateur doit être accessible sur le GameObject, quelle que soit la distance, pour l’effet doit être activé.</span><span class="sxs-lookup"><span data-stu-id="2da97-459">The user must be facing the GameObject, regardless of distance, for the effect to be enabled.</span></span>

* <span data-ttu-id="2da97-460">Application et la configuration un **AudioChorusFilter** et un **AudioEchoFilter** à la **AudioSource**.</span><span class="sxs-lookup"><span data-stu-id="2da97-460">Applying and configuring an **AudioChorusFilter** and an **AudioEchoFilter** to the **AudioSource**.</span></span>
* <span data-ttu-id="2da97-461">La désactivation de l’effet en désactivant les filtres.</span><span class="sxs-lookup"><span data-stu-id="2da97-461">Disabling the effect by disabling the filters.</span></span>

<span data-ttu-id="2da97-462">Effet de voix utilisateur utilise le composant de sélecteur de Stream Mic, à partir de la [MixedRealityToolkit pour Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity), pour sélectionner le flux de voix de haute qualité et de la router système audio d’Unity.</span><span class="sxs-lookup"><span data-stu-id="2da97-462">User Voice Effect uses the Mic Stream Selector component, from the [MixedRealityToolkit for Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity), to select the high quality voice stream and route it into Unity's audio system.</span></span>

* <span data-ttu-id="2da97-463">Dans le **hiérarchie** panneau, sélectionnez **gestionnaires**.</span><span class="sxs-lookup"><span data-stu-id="2da97-463">In the **Hierarchy** panel, select **Managers**.</span></span>
* <span data-ttu-id="2da97-464">Dans le **inspecteur** volet, développez **Gestionnaire d’entrée vocale**.</span><span class="sxs-lookup"><span data-stu-id="2da97-464">In the **Inspector** panel, expand **Speech Input Handler**.</span></span>
* <span data-ttu-id="2da97-465">Dans **Gestionnaire d’entrée vocale**, développez **Underworld afficher**.</span><span class="sxs-lookup"><span data-stu-id="2da97-465">In **Speech Input Handler**, expand **Show Underworld**.</span></span>
* <span data-ttu-id="2da97-466">Modification **aucune fonction** à **UnderworldBase.OnEnable**.</span><span class="sxs-lookup"><span data-stu-id="2da97-466">Change **No Function** to **UnderworldBase.OnEnable**.</span></span>

![mot clé : Afficher Underworld](images/showunderworld.png)

* <span data-ttu-id="2da97-468">Développez **masquer Underworld**.</span><span class="sxs-lookup"><span data-stu-id="2da97-468">Expand **Hide Underworld**.</span></span>
* <span data-ttu-id="2da97-469">Modification **aucune fonction** à **UnderworldBase.OnDisable**.</span><span class="sxs-lookup"><span data-stu-id="2da97-469">Change **No Function** to **UnderworldBase.OnDisable**.</span></span>

![mot clé : Masquer Underworld](images/hideunderworld.png)

#### <a name="build-and-deploy"></a><span data-ttu-id="2da97-471">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="2da97-471">Build and Deploy</span></span>

* <span data-ttu-id="2da97-472">Comme précédemment, générez le projet dans Unity et déployés dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2da97-472">As before, build the project in Unity and deploy in Visual Studio.</span></span>

<span data-ttu-id="2da97-473">Une fois que l’application est déployée :</span><span class="sxs-lookup"><span data-stu-id="2da97-473">After the application is deployed:</span></span>

* <span data-ttu-id="2da97-474">Sont confrontés à une surface (mur, floor, table) et le say *« Underworld afficher »*.</span><span class="sxs-lookup"><span data-stu-id="2da97-474">Face a surface (wall, floor, table) and say *"Show Underworld"*.</span></span>

<span data-ttu-id="2da97-475">L’underworld s’affichera et tous les autres hologrammes seront masquées.</span><span class="sxs-lookup"><span data-stu-id="2da97-475">The underworld will be shown and all other holograms will be hidden.</span></span> <span data-ttu-id="2da97-476">Si vous ne voyez pas l’underworld, vérifiez que vous êtes confronté à une surface du monde réel.</span><span class="sxs-lookup"><span data-stu-id="2da97-476">If you do not see the underworld, ensure that you are facing a real-world surface.</span></span>

* <span data-ttu-id="2da97-477">Approche à moins de 1 mètre l’hologramme underworld et commencer à parler.</span><span class="sxs-lookup"><span data-stu-id="2da97-477">Approach within 1 meter of the underworld hologram and start talking.</span></span>

<span data-ttu-id="2da97-478">Il existe désormais des effets audio appliqués à votre voix !</span><span class="sxs-lookup"><span data-stu-id="2da97-478">There are now audio effects applied to your voice!</span></span>

* <span data-ttu-id="2da97-479">Activer en dehors de l’underworld et notez comment l’effet n’est plus appliqué.</span><span class="sxs-lookup"><span data-stu-id="2da97-479">Turn away from the underworld and notice how the effect is no longer applied.</span></span>
* <span data-ttu-id="2da97-480">Par exemple *« Masquer Underworld »* pour masquer l’underworld.</span><span class="sxs-lookup"><span data-stu-id="2da97-480">Say *"Hide Underworld"* to hide the underworld.</span></span>

<span data-ttu-id="2da97-481">L’underworld est masqué et les hologrammes auparavant masqués réapparaît.</span><span class="sxs-lookup"><span data-stu-id="2da97-481">The underworld will be hidden and the previously hidden holograms will reappear.</span></span>

## <a name="the-end"></a><span data-ttu-id="2da97-482">La fin</span><span class="sxs-lookup"><span data-stu-id="2da97-482">The End</span></span>

<span data-ttu-id="2da97-483">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="2da97-483">Congratulations!</span></span> <span data-ttu-id="2da97-484">Vous avez maintenant terminé **220 Spatial MR : Son spatial**.</span><span class="sxs-lookup"><span data-stu-id="2da97-484">You have now completed **MR Spatial 220: Spatial sound**.</span></span>

<span data-ttu-id="2da97-485">Écoutez le monde et faites vivre vos expériences avec son !</span><span class="sxs-lookup"><span data-stu-id="2da97-485">Listen to the world and bring your experiences to life with sound!</span></span>
