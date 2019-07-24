---
title: Entrée MR 211-geste
description: Suivez cette procédure pas à pas de codage à l’aide de Unity, Visual Studio et HoloLens pour apprendre les concepts de mouvement.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, Academy, didacticiel, geste
ms.openlocfilehash: 76d2b4c0ac3d0a3783b091f7dc8c39548a18b548
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63522452"
---
>[!NOTE]
><span data-ttu-id="900c0-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="900c0-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="900c0-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="900c0-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="900c0-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="900c0-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="900c0-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="900c0-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="900c0-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="900c0-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="900c0-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="900c0-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

# <a name="mr-input-211-gesture"></a><span data-ttu-id="900c0-110">Monsieur 211: Mouvement</span><span class="sxs-lookup"><span data-stu-id="900c0-110">MR Input 211: Gesture</span></span>

<span data-ttu-id="900c0-111">Les [gestes](gestures.md) transforment l’intention de l’utilisateur en action.</span><span class="sxs-lookup"><span data-stu-id="900c0-111">[Gestures](gestures.md) turn user intention into action.</span></span> <span data-ttu-id="900c0-112">Avec les gestes, les utilisateurs peuvent interagir avec des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="900c0-112">With gestures, users can interact with holograms.</span></span> <span data-ttu-id="900c0-113">Dans ce cours, nous allons apprendre à suivre les mains de l’utilisateur, à répondre aux entrées de l’utilisateur et à envoyer des commentaires à l’utilisateur en fonction de l’État et de l’emplacement de la main.</span><span class="sxs-lookup"><span data-stu-id="900c0-113">In this course, we'll learn how to track the user's hands, respond to user input, and give feedback to the user based on hand state and location.</span></span>

>[!VIDEO https://www.youtube.com/embed/c9zlpfFeEtc]

<span data-ttu-id="900c0-114">Dans les [notions de base de m. 101](holograms-101.md), nous avons utilisé un simple geste d’appui sur l’air pour interagir avec nos hologrammes.</span><span class="sxs-lookup"><span data-stu-id="900c0-114">In [MR Basics 101](holograms-101.md), we used a simple air-tap gesture to interact with our holograms.</span></span> <span data-ttu-id="900c0-115">À présent, nous allons aller au-delà du geste d’entrée aérienne et explorer de nouveaux concepts pour:</span><span class="sxs-lookup"><span data-stu-id="900c0-115">Now, we'll move beyond the air-tap gesture and explore new concepts to:</span></span>

* <span data-ttu-id="900c0-116">Détectez le moment où l’utilisateur fait l’objet d’un suivi et fournissez des commentaires à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="900c0-116">Detect when the user's hand is being tracked and provide feedback to the user.</span></span>
* <span data-ttu-id="900c0-117">Utilisez un mouvement de navigation pour faire pivoter nos hologrammes.</span><span class="sxs-lookup"><span data-stu-id="900c0-117">Use a navigation gesture to rotate our holograms.</span></span>
* <span data-ttu-id="900c0-118">Fournir des commentaires lorsque la main de l’utilisateur est sur le point de sortir de l’affichage.</span><span class="sxs-lookup"><span data-stu-id="900c0-118">Provide feedback when the user's hand is about to go out of view.</span></span>
* <span data-ttu-id="900c0-119">Utilisez des événements de manipulation pour permettre aux utilisateurs de déplacer des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="900c0-119">Use manipulation events to allow users to move holograms with their hands.</span></span>

<span data-ttu-id="900c0-120">Dans ce cours, nous allons revisiter l' **Explorateur de modèles**de projet Unity, que nous avons créé dans l' [entrée 210](holograms-210.md)de la m.</span><span class="sxs-lookup"><span data-stu-id="900c0-120">In this course, we'll revisit the Unity project **Model Explorer**, which we built in [MR Input 210](holograms-210.md).</span></span> <span data-ttu-id="900c0-121">Notre ami astronautes est en retour pour nous aider dans notre exploration de ces nouveaux concepts de mouvement.</span><span class="sxs-lookup"><span data-stu-id="900c0-121">Our astronaut friend is back to assist us in our exploration of these new gesture concepts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="900c0-122">Les vidéos incorporées dans chacun des chapitres ci-dessous ont été enregistrées à l’aide d’une version antérieure d’Unity et de la réalité mixte Toolkit.</span><span class="sxs-lookup"><span data-stu-id="900c0-122">The videos embedded in each of the chapters below were recorded using an older version of Unity and the Mixed Reality Toolkit.</span></span> <span data-ttu-id="900c0-123">Alors que les instructions pas à pas sont précises et actuelles, vous pouvez voir des scripts et des visuels dans les vidéos correspondantes qui sont obsolètes.</span><span class="sxs-lookup"><span data-stu-id="900c0-123">While the step-by-step instructions are accurate and current, you may see scripts and visuals in the corresponding videos that are out-of-date.</span></span> <span data-ttu-id="900c0-124">Les vidéos restent incluses pour l’affiche et les concepts abordés s’appliquent toujours.</span><span class="sxs-lookup"><span data-stu-id="900c0-124">The videos remain included for posterity and because the concepts covered still apply.</span></span>

## <a name="device-support"></a><span data-ttu-id="900c0-125">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="900c0-125">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="900c0-126">Course</span><span class="sxs-lookup"><span data-stu-id="900c0-126">Course</span></span></th><th style="width:150px"> <span data-ttu-id="900c0-127"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="900c0-127"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="900c0-128"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="900c0-128"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="900c0-129">Monsieur 211: Mouvement</span><span class="sxs-lookup"><span data-stu-id="900c0-129">MR Input 211: Gesture</span></span></td><td style="text-align: center;"> <span data-ttu-id="900c0-130">✔️</span><span class="sxs-lookup"><span data-stu-id="900c0-130">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="900c0-131">✔️</span><span class="sxs-lookup"><span data-stu-id="900c0-131">✔️</span></span></td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="900c0-132">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="900c0-132">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="900c0-133">Prérequis</span><span class="sxs-lookup"><span data-stu-id="900c0-133">Prerequisites</span></span>

* <span data-ttu-id="900c0-134">Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="900c0-134">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="900c0-135">Certaines fonctionnalités C# de programmation de base.</span><span class="sxs-lookup"><span data-stu-id="900c0-135">Some basic C# programming ability.</span></span>
* <span data-ttu-id="900c0-136">Vous devez avoir terminé les [notions de base de m. 101](holograms-101.md).</span><span class="sxs-lookup"><span data-stu-id="900c0-136">You should have completed [MR Basics 101](holograms-101.md).</span></span>
* <span data-ttu-id="900c0-137">Vous devez avoir terminé l' [entrée 210](holograms-210.md).</span><span class="sxs-lookup"><span data-stu-id="900c0-137">You should have completed [MR Input 210](holograms-210.md).</span></span>
* <span data-ttu-id="900c0-138">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="900c0-138">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="900c0-139">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="900c0-139">Project files</span></span>

* <span data-ttu-id="900c0-140">Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-211-Gesture.zip) requis par le projet.</span><span class="sxs-lookup"><span data-stu-id="900c0-140">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-211-Gesture.zip) required by the project.</span></span><span data-ttu-id="900c0-141"> Requiert Unity 2017,2 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="900c0-141"> Requires Unity 2017.2 or later.</span></span>
* <span data-ttu-id="900c0-142">Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.</span><span class="sxs-lookup"><span data-stu-id="900c0-142">Un-archive the files to your desktop or other easy to reach location.</span></span>

>[!NOTE]
><span data-ttu-id="900c0-143">Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-211-Gesture).</span><span class="sxs-lookup"><span data-stu-id="900c0-143">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-211-Gesture).</span></span>

### <a name="errata-and-notes"></a><span data-ttu-id="900c0-144">Errata et notes</span><span class="sxs-lookup"><span data-stu-id="900c0-144">Errata and Notes</span></span>

* <span data-ttu-id="900c0-145">L’option «Activer Uniquement mon code» doit être désactivée (décochée) dans Visual Studio sous Outils-> Options-> le débogage pour atteindre les points d’arrêt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="900c0-145">"Enable Just My Code" needs to be disabled (*unchecked*) in Visual Studio under Tools->Options->Debugging in order to hit breakpoints in your code.</span></span>

## <a name="chapter-0---unity-setup"></a><span data-ttu-id="900c0-146">Chapitre 0-Configuration Unity</span><span class="sxs-lookup"><span data-stu-id="900c0-146">Chapter 0 - Unity Setup</span></span>

### <a name="instructions"></a><span data-ttu-id="900c0-147">Instructions</span><span class="sxs-lookup"><span data-stu-id="900c0-147">Instructions</span></span>

1. <span data-ttu-id="900c0-148">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="900c0-148">Start Unity.</span></span>
2. <span data-ttu-id="900c0-149">Sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="900c0-149">Select **Open**.</span></span>
3. <span data-ttu-id="900c0-150">Accédez au dossier de **mouvements** que vous avez préalablement désinstallé.</span><span class="sxs-lookup"><span data-stu-id="900c0-150">Navigate to the **Gesture** folder you previously un-archived.</span></span>
4. <span data-ttu-id="900c0-151">Recherchez et sélectionnez le dossier de **démarrage**/de l'**Explorateur de modèles** .</span><span class="sxs-lookup"><span data-stu-id="900c0-151">Find and select the **Starting**/**Model Explorer** folder.</span></span>
5. <span data-ttu-id="900c0-152">Cliquez sur le bouton **Sélectionner un dossier** .</span><span class="sxs-lookup"><span data-stu-id="900c0-152">Click the **Select Folder** button.</span></span>
6. <span data-ttu-id="900c0-153">Dans le panneau **projet** , développez le dossier **scenes** .</span><span class="sxs-lookup"><span data-stu-id="900c0-153">In the **Project** panel, expand the **Scenes** folder.</span></span>
7. <span data-ttu-id="900c0-154">Double-cliquez sur **ModelExplorer** Scene pour le charger dans Unity.</span><span class="sxs-lookup"><span data-stu-id="900c0-154">Double-click **ModelExplorer** scene to load it in Unity.</span></span>

### <a name="building"></a><span data-ttu-id="900c0-155">Génération</span><span class="sxs-lookup"><span data-stu-id="900c0-155">Building</span></span>

1. <span data-ttu-id="900c0-156">Dans Unity, sélectionnez **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="900c0-156">In Unity, select **File > Build Settings**.</span></span>
2. <span data-ttu-id="900c0-157">Si **scenes/ModelExplorer** n’est pas listé dans **scenes dans Build**, cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="900c0-157">If **Scenes/ModelExplorer** is not listed in **Scenes In Build**, click **Add Open Scenes** to add the scene.</span></span>
3. <span data-ttu-id="900c0-158">Si vous développez spécifiquement pour HoloLens, définissez **appareil cible** sur **hololens**.</span><span class="sxs-lookup"><span data-stu-id="900c0-158">If you're specifically developing for HoloLens, set **Target device** to **HoloLens**.</span></span> <span data-ttu-id="900c0-159">Dans le cas contraire, laissez-le sur **un appareil**.</span><span class="sxs-lookup"><span data-stu-id="900c0-159">Otherwise, leave it on **Any device**.</span></span>
4. <span data-ttu-id="900c0-160">Vérifiez que le **type de build** est défini sur **D3D** et que le **Kit de développement logiciel (SDK** ) est défini sur le **dernier installé** (qui doit être le SDK 16299 ou une version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="900c0-160">Ensure **Build Type** is set to **D3D** and **SDK** is set to **Latest installed** (which should be SDK 16299 or newer).</span></span>
5. <span data-ttu-id="900c0-161">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="900c0-161">Click **Build**.</span></span>
6. <span data-ttu-id="900c0-162">Créez un **dossier** nommé «App».</span><span class="sxs-lookup"><span data-stu-id="900c0-162">Create a **New Folder** named "App".</span></span>
7. <span data-ttu-id="900c0-163">Cliquez sur le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="900c0-163">Single click the **App** folder.</span></span>
8. <span data-ttu-id="900c0-164">Appuyez sur **Sélectionner un dossier** et Unity va commencer à générer le projet pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="900c0-164">Press **Select Folder** and Unity will start building the project for Visual Studio.</span></span>

<span data-ttu-id="900c0-165">Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="900c0-165">When Unity is done, a File Explorer window will appear.</span></span>

1. <span data-ttu-id="900c0-166">Ouvrez le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="900c0-166">Open the **App** folder.</span></span>
2. <span data-ttu-id="900c0-167">Ouvrez la **solution Visual Studio ModelExplorer**.</span><span class="sxs-lookup"><span data-stu-id="900c0-167">Open the **ModelExplorer Visual Studio Solution**.</span></span>

<span data-ttu-id="900c0-168">En cas de déploiement dans HoloLens:</span><span class="sxs-lookup"><span data-stu-id="900c0-168">If deploying to HoloLens:</span></span>

1. <span data-ttu-id="900c0-169">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.</span><span class="sxs-lookup"><span data-stu-id="900c0-169">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x86**.</span></span>
2. <span data-ttu-id="900c0-170">Cliquez sur la flèche déroulante en regard du bouton ordinateur local, puis sélectionnez **ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="900c0-170">Click on the drop down arrow next to the Local Machine button, and select **Remote Machine**.</span></span>
3. <span data-ttu-id="900c0-171">Entrez **l’adresse IP de votre appareil HoloLens** et définissez le mode d’authentification sur **universel (protocole non chiffré)** .</span><span class="sxs-lookup"><span data-stu-id="900c0-171">Enter **your HoloLens device IP address** and set Authentication Mode to **Universal (Unencrypted Protocol)**.</span></span> <span data-ttu-id="900c0-172">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="900c0-172">Click **Select**.</span></span> <span data-ttu-id="900c0-173">Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées**.</span><span class="sxs-lookup"><span data-stu-id="900c0-173">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options**.</span></span>
4. <span data-ttu-id="900c0-174">Dans la barre de menus supérieure, cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="900c0-174">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="900c0-175">S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le coupler à [Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span><span class="sxs-lookup"><span data-stu-id="900c0-175">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span></span>
5. <span data-ttu-id="900c0-176">Une fois l’application déployée, ignorez le **Fitbox** avec un **mouvement Select**.</span><span class="sxs-lookup"><span data-stu-id="900c0-176">When the app has deployed, dismiss the **Fitbox** with a **select gesture**.</span></span>

<span data-ttu-id="900c0-177">En cas de déploiement sur un casque immersif:</span><span class="sxs-lookup"><span data-stu-id="900c0-177">If deploying to an immersive headset:</span></span>

1. <span data-ttu-id="900c0-178">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x64**.</span><span class="sxs-lookup"><span data-stu-id="900c0-178">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x64**.</span></span>
2. <span data-ttu-id="900c0-179">Assurez-vous que la cible de déploiement est définie sur **ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="900c0-179">Make sure the deployment target is set to **Local Machine**.</span></span>
3. <span data-ttu-id="900c0-180">Dans la barre de menus supérieure, cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="900c0-180">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
4. <span data-ttu-id="900c0-181">Une fois l’application déployée, Faites disparaître le **Fitbox** en tirant le déclencheur sur un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="900c0-181">When the app has deployed, dismiss the **Fitbox** by pulling the trigger on a motion controller.</span></span>

>[!NOTE]
><span data-ttu-id="900c0-182">Vous pouvez remarquer des erreurs rouges dans le panneau erreurs de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="900c0-182">You might notice some red errors in the Visual Studio Errors panel.</span></span> <span data-ttu-id="900c0-183">Vous pouvez les ignorer en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="900c0-183">It is safe to ignore them.</span></span> <span data-ttu-id="900c0-184">Basculez vers le panneau sortie pour afficher la progression réelle de la génération.</span><span class="sxs-lookup"><span data-stu-id="900c0-184">Switch to the Output panel to view actual build progress.</span></span> <span data-ttu-id="900c0-185">Les erreurs dans le panneau sortie vous obligent à faire un correctif (le plus souvent, elles sont provoquées par une erreur dans un script).</span><span class="sxs-lookup"><span data-stu-id="900c0-185">Errors in the Output panel will require you to make a fix (most often they are caused by a mistake in a script).</span></span>

## <a name="chapter-1---hand-detected-feedback"></a><span data-ttu-id="900c0-186">Chapitre 1-commentaires sur la main détectés</span><span class="sxs-lookup"><span data-stu-id="900c0-186">Chapter 1 - Hand detected feedback</span></span>

>[!VIDEO https://www.youtube.com/embed/D1FcIyuFTZQ]

### <a name="objectives"></a><span data-ttu-id="900c0-187">Objectifs</span><span class="sxs-lookup"><span data-stu-id="900c0-187">Objectives</span></span>

* <span data-ttu-id="900c0-188">S’abonner aux événements de suivi de la main.</span><span class="sxs-lookup"><span data-stu-id="900c0-188">Subscribe to hand tracking events.</span></span>
* <span data-ttu-id="900c0-189">Utilisez les commentaires des curseurs pour montrer aux utilisateurs quand une main fait l’objet d’un suivi.</span><span class="sxs-lookup"><span data-stu-id="900c0-189">Use cursor feedback to show users when a hand is being tracked.</span></span>

### <a name="instructions"></a><span data-ttu-id="900c0-190">Instructions</span><span class="sxs-lookup"><span data-stu-id="900c0-190">Instructions</span></span>

* <span data-ttu-id="900c0-191">Dans le volet **hiérarchie** , développez l’objet **InputManager** .</span><span class="sxs-lookup"><span data-stu-id="900c0-191">In the **Hierarchy** panel, expand the **InputManager** object.</span></span>
* <span data-ttu-id="900c0-192">Recherchez et sélectionnez l’objet **GesturesInput** .</span><span class="sxs-lookup"><span data-stu-id="900c0-192">Look for and select the **GesturesInput** object.</span></span>

<span data-ttu-id="900c0-193">Le script **InteractionInputSource.cs** effectue les étapes suivantes:</span><span class="sxs-lookup"><span data-stu-id="900c0-193">The **InteractionInputSource.cs** script performs these steps:</span></span>

1. <span data-ttu-id="900c0-194">S’abonne aux événements InteractionSourceDetected et InteractionSourceLost.</span><span class="sxs-lookup"><span data-stu-id="900c0-194">Subscribes to the InteractionSourceDetected and InteractionSourceLost events.</span></span>
2. <span data-ttu-id="900c0-195">Définit l’État HandDetected.</span><span class="sxs-lookup"><span data-stu-id="900c0-195">Sets the HandDetected state.</span></span>
3. <span data-ttu-id="900c0-196">Annule l’abonnement aux événements InteractionSourceDetected et InteractionSourceLost.</span><span class="sxs-lookup"><span data-stu-id="900c0-196">Unsubscribes from the InteractionSourceDetected and InteractionSourceLost events.</span></span>

<span data-ttu-id="900c0-197">Ensuite, nous allons mettre à niveau notre curseur de l' [entrée 210](holograms-210.md) en une qui affiche les commentaires en fonction des actions de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="900c0-197">Next, we'll upgrade our cursor from [MR Input 210](holograms-210.md) into one that shows feedback depending on the user's actions.</span></span>

1. <span data-ttu-id="900c0-198">Dans le volet **hiérarchie** , sélectionnez l’objet **curseur** et supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="900c0-198">In the **Hierarchy** panel, select the **Cursor** object and delete it.</span></span>
2. <span data-ttu-id="900c0-199">Dans le panneau **projet** , recherchez **CursorWithFeedback** et faites-le glisser dans le panneau **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="900c0-199">In the **Project** panel, search for **CursorWithFeedback** and drag it into the **Hierarchy** panel.</span></span>
3. <span data-ttu-id="900c0-200">Cliquez sur **InputManager** dans le panneau **hiérarchie** , puis faites glisser l’objet **CursorWithFeedback** de la **hiérarchie** vers le champ **curseur** du **SimpleSinglePointerSelector**du InputManager, en bas de l’onglet **Inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="900c0-200">Click on **InputManager** in the **Hierarchy** panel, then drag the **CursorWithFeedback** object from the **Hierarchy** into the InputManager's **SimpleSinglePointerSelector**'s **Cursor** field, at the bottom of the **Inspector**.</span></span>
4. <span data-ttu-id="900c0-201">Cliquez sur **CursorWithFeedback** dans la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="900c0-201">Click on the **CursorWithFeedback** in the **Hierarchy**.</span></span>
5. <span data-ttu-id="900c0-202">Dans le volet de l' **inspecteur** , développez **données d’État du curseur** sur le script du curseur de l' **objet** .</span><span class="sxs-lookup"><span data-stu-id="900c0-202">In the **Inspector** panel, expand **Cursor State Data** on the **Object Cursor** script.</span></span>

<span data-ttu-id="900c0-203">Les **données d’État du curseur** fonctionnent de la manière suivante:</span><span class="sxs-lookup"><span data-stu-id="900c0-203">The **Cursor State Data** works like this:</span></span>

* <span data-ttu-id="900c0-204">Tout état d' **observation** signifie qu’aucune main n’est détectée et que l’utilisateur recherche simplement.</span><span class="sxs-lookup"><span data-stu-id="900c0-204">Any **Observe** state means that no hand is detected and the user is simply looking around.</span></span>
* <span data-ttu-id="900c0-205">Tout état d' **interaction** signifie qu’une main ou un contrôleur est détecté.</span><span class="sxs-lookup"><span data-stu-id="900c0-205">Any **Interact** state means that a hand or controller is detected.</span></span>
* <span data-ttu-id="900c0-206">Tout état de **survol** signifie que l’utilisateur Regarde un hologramme.</span><span class="sxs-lookup"><span data-stu-id="900c0-206">Any **Hover** state means the user is looking at a hologram.</span></span>

### <a name="build-and-deploy"></a><span data-ttu-id="900c0-207">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="900c0-207">Build and Deploy</span></span>

* <span data-ttu-id="900c0-208">Dans Unity, utilisez les **paramètres de build de > de fichiers** pour régénérer l’application.</span><span class="sxs-lookup"><span data-stu-id="900c0-208">In Unity, use **File > Build Settings** to rebuild the application.</span></span>
* <span data-ttu-id="900c0-209">Ouvrez le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="900c0-209">Open the **App** folder.</span></span>
* <span data-ttu-id="900c0-210">S’il n’est pas déjà ouvert, ouvrez la **solution Visual Studio ModelExplorer**.</span><span class="sxs-lookup"><span data-stu-id="900c0-210">If it's not already open, open the **ModelExplorer Visual Studio Solution**.</span></span>
  * <span data-ttu-id="900c0-211">(Si vous avez déjà généré/déployé ce projet dans Visual Studio au cours de la configuration, vous pouvez ouvrir cette instance de VS et cliquer sur «recharger tout» lorsque vous y êtes invité).</span><span class="sxs-lookup"><span data-stu-id="900c0-211">(If you already built/deployed this project in Visual Studio during set-up, then you can open that instance of VS and click 'Reload All' when prompted).</span></span>
* <span data-ttu-id="900c0-212">Dans Visual Studio, cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="900c0-212">In Visual Studio, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
* <span data-ttu-id="900c0-213">Une fois que l’application a été déployée sur HoloLens, Faites disparaître le fitbox à l’aide du geste d’appui sur l’air.</span><span class="sxs-lookup"><span data-stu-id="900c0-213">After the application deploys to the HoloLens, dismiss the fitbox using the air-tap gesture.</span></span>
* <span data-ttu-id="900c0-214">Déplacez votre main en vue et pointez votre index vers le ciel pour démarrer le suivi.</span><span class="sxs-lookup"><span data-stu-id="900c0-214">Move your hand into view and point your index finger to the sky to start hand tracking.</span></span>
* <span data-ttu-id="900c0-215">Déplacez votre main à gauche, à droite, en haut et en aval.</span><span class="sxs-lookup"><span data-stu-id="900c0-215">Move your hand left, right, up and down.</span></span>
* <span data-ttu-id="900c0-216">Regardez comment le curseur change lorsque votre main est détectée, puis perdu de la vue.</span><span class="sxs-lookup"><span data-stu-id="900c0-216">Watch how the cursor changes when your hand is detected and then lost from view.</span></span>
* <span data-ttu-id="900c0-217">Si vous êtes sur un casque immersif, vous devez vous connecter et déconnecter votre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="900c0-217">If you're on an immersive headset, you'll have to connect and disconnect your controller.</span></span> <span data-ttu-id="900c0-218">Ces commentaires deviennent moins intéressants sur un appareil immersif, car un contrôleur connecté est toujours «disponible».</span><span class="sxs-lookup"><span data-stu-id="900c0-218">This feedback becomes less interesting on an immersive device, as a connected controller will always be "available".</span></span>

## <a name="chapter-2---navigation"></a><span data-ttu-id="900c0-219">Chapitre 2-navigation</span><span class="sxs-lookup"><span data-stu-id="900c0-219">Chapter 2 - Navigation</span></span>

>[!VIDEO https://www.youtube.com/embed/sm-kxtKksSo]

### <a name="objectives"></a><span data-ttu-id="900c0-220">Objectifs</span><span class="sxs-lookup"><span data-stu-id="900c0-220">Objectives</span></span>

* <span data-ttu-id="900c0-221">Utilisez les événements de mouvement de navigation pour faire pivoter le astronautes.</span><span class="sxs-lookup"><span data-stu-id="900c0-221">Use Navigation gesture events to rotate the astronaut.</span></span>

### <a name="instructions"></a><span data-ttu-id="900c0-222">Instructions</span><span class="sxs-lookup"><span data-stu-id="900c0-222">Instructions</span></span>

<span data-ttu-id="900c0-223">Pour utiliser des mouvements de navigation dans notre application, nous allons modifier **GestureAction.cs** pour faire pivoter les objets lorsque le mouvement de navigation se produit.</span><span class="sxs-lookup"><span data-stu-id="900c0-223">To use Navigation gestures in our app, we are going to edit **GestureAction.cs** to rotate objects when the Navigation gesture occurs.</span></span> <span data-ttu-id="900c0-224">En outre, nous ajouterons des commentaires au curseur à afficher lorsque la navigation est disponible.</span><span class="sxs-lookup"><span data-stu-id="900c0-224">Additionally, we'll add feedback to the cursor to display when Navigation is available.</span></span>

1. <span data-ttu-id="900c0-225">Dans le volet **hiérarchie** , développez **CursorWithFeedback**.</span><span class="sxs-lookup"><span data-stu-id="900c0-225">In the **Hierarchy** panel, expand **CursorWithFeedback**.</span></span>
2. <span data-ttu-id="900c0-226">Dans le  dossier hologrammes, recherchez la ressource **ScrollFeedback** .</span><span class="sxs-lookup"><span data-stu-id="900c0-226">In the **Holograms** folder, find the **ScrollFeedback** asset.</span></span>
3. <span data-ttu-id="900c0-227">Glissez-déplacez le Prefab **ScrollFeedback** sur le gameobject **CursorWithFeedback** dans la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="900c0-227">Drag and drop the **ScrollFeedback** prefab onto the **CursorWithFeedback** GameObject in the **Hierarchy**.</span></span>
4. <span data-ttu-id="900c0-228">Cliquez sur **CursorWithFeedback**.</span><span class="sxs-lookup"><span data-stu-id="900c0-228">Click on **CursorWithFeedback**.</span></span>
5. <span data-ttu-id="900c0-229">Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="900c0-229">In the **Inspector** panel, click the **Add Component** button.</span></span>
6. <span data-ttu-id="900c0-230">Dans le menu, tapez dans la zone de recherche **CursorFeedback**.</span><span class="sxs-lookup"><span data-stu-id="900c0-230">In the menu, type in the search box **CursorFeedback**.</span></span> <span data-ttu-id="900c0-231">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="900c0-231">Select the search result.</span></span>
7. <span data-ttu-id="900c0-232">Faites glisser et déposez l’objet **ScrollFeedback** à partir de la **hiérarchie** vers la propriété objet de jeu dans le **défilement détectée** dans le composant de **Commentaires de curseur** de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="900c0-232">Drag and drop the **ScrollFeedback** object from the **Hierarchy** onto the **Scroll Detected Game Object** property in the **Cursor Feedback** component in the **Inspector**.</span></span>
8. <span data-ttu-id="900c0-233">Dans le volet **hiérarchie** , sélectionnez l’objet **AstroMan** .</span><span class="sxs-lookup"><span data-stu-id="900c0-233">In the **Hierarchy** panel, select the **AstroMan** object.</span></span>
9. <span data-ttu-id="900c0-234">Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="900c0-234">In the **Inspector** panel, click the **Add Component** button.</span></span>
10. <span data-ttu-id="900c0-235">Dans le menu, tapez dans l’action de **mouvement**de zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="900c0-235">In the menu, type in the search box **Gesture Action**.</span></span> <span data-ttu-id="900c0-236">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="900c0-236">Select the search result.</span></span>

<span data-ttu-id="900c0-237">Ensuite, ouvrez **GestureAction.cs** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="900c0-237">Next, open **GestureAction.cs** in Visual Studio.</span></span> <span data-ttu-id="900c0-238">Dans l’exercice de codage 2. c, modifiez le script pour effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="900c0-238">In coding exercise 2.c, edit the script to do the following:</span></span>

1. <span data-ttu-id="900c0-239">**Faites pivoter l’objet AstroMan** chaque fois qu’un mouvement de navigation est effectué.</span><span class="sxs-lookup"><span data-stu-id="900c0-239">**Rotate the AstroMan** object whenever a Navigation gesture is performed.</span></span>
2. <span data-ttu-id="900c0-240">Calcule le **rotationFactor** pour contrôler la quantité de rotation appliquée à l’objet.</span><span class="sxs-lookup"><span data-stu-id="900c0-240">Calculate the **rotationFactor** to control the amount of rotation applied to the object.</span></span>
3. <span data-ttu-id="900c0-241">**Faire pivoter l’objet** autour de l’axe y lorsque l’utilisateur déplace sa main à gauche ou à droite.</span><span class="sxs-lookup"><span data-stu-id="900c0-241">**Rotate the object** around the y-axis when the user moves their hand left or right.</span></span>

<span data-ttu-id="900c0-242">Effectuez les exercices de codage 2. c dans le script ou remplacez le code par la solution terminée ci-dessous:</span><span class="sxs-lookup"><span data-stu-id="900c0-242">Complete coding exercises 2.c in the script, or replace the code with the completed solution below:</span></span>

```cs
using HoloToolkit.Unity.InputModule;
using UnityEngine;

/// <summary>
/// GestureAction performs custom actions based on
/// which gesture is being performed.
/// </summary>
public class GestureAction : MonoBehaviour, INavigationHandler, IManipulationHandler, ISpeechHandler
{
    [Tooltip("Rotation max speed controls amount of rotation.")]
    [SerializeField]
    private float RotationSensitivity = 10.0f;

    private bool isNavigationEnabled = true;
    public bool IsNavigationEnabled
    {
        get { return isNavigationEnabled; }
        set { isNavigationEnabled = value; }
    }

    private Vector3 manipulationOriginalPosition = Vector3.zero;

    void INavigationHandler.OnNavigationStarted(NavigationEventData eventData)
    {
        InputManager.Instance.PushModalInputHandler(gameObject);
    }

    void INavigationHandler.OnNavigationUpdated(NavigationEventData eventData)
    {
        if (isNavigationEnabled)
        {
            /* TODO: DEVELOPER CODING EXERCISE 2.c */

            // 2.c: Calculate a float rotationFactor based on eventData's NormalizedOffset.x multiplied by RotationSensitivity.
            // This will help control the amount of rotation.
            float rotationFactor = eventData.NormalizedOffset.x * RotationSensitivity;

            // 2.c: transform.Rotate around the Y axis using rotationFactor.
            transform.Rotate(new Vector3(0, -1 * rotationFactor, 0));
        }
    }

    void INavigationHandler.OnNavigationCompleted(NavigationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void INavigationHandler.OnNavigationCanceled(NavigationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void IManipulationHandler.OnManipulationStarted(ManipulationEventData eventData)
    {
        if (!isNavigationEnabled)
        {
            InputManager.Instance.PushModalInputHandler(gameObject);

            manipulationOriginalPosition = transform.position;
        }
    }

    void IManipulationHandler.OnManipulationUpdated(ManipulationEventData eventData)
    {
        if (!isNavigationEnabled)
        {
            /* TODO: DEVELOPER CODING EXERCISE 4.a */

            // 4.a: Make this transform's position be the manipulationOriginalPosition + eventData.CumulativeDelta
        }
    }

    void IManipulationHandler.OnManipulationCompleted(ManipulationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void IManipulationHandler.OnManipulationCanceled(ManipulationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void ISpeechHandler.OnSpeechKeywordRecognized(SpeechEventData eventData)
    {
        if (eventData.RecognizedText.Equals("Move Astronaut"))
        {
            isNavigationEnabled = false;
        }
        else if (eventData.RecognizedText.Equals("Rotate Astronaut"))
        {
            isNavigationEnabled = true;
        }
        else
        {
            return;
        }

        eventData.Use();
    }
}
```

<span data-ttu-id="900c0-243">Vous remarquerez que les autres événements de navigation sont déjà renseignés avec des informations.</span><span class="sxs-lookup"><span data-stu-id="900c0-243">You'll notice that the other navigation events are already filled in with some info.</span></span> <span data-ttu-id="900c0-244">Nous envoyons les GameObject dans la pile modale InputSystem’s de la boîte à outils, de sorte que l’utilisateur n’a pas à maintenir le focus sur le astronautes une fois la rotation commencée.</span><span class="sxs-lookup"><span data-stu-id="900c0-244">We push the GameObject onto the Toolkit's InputSystem's modal stack, so the user doesn't have to maintain focus on the Astronaut once rotation has begun.</span></span> <span data-ttu-id="900c0-245">En conséquence, nous dépilerons le GameObject de la pile une fois le mouvement terminé.</span><span class="sxs-lookup"><span data-stu-id="900c0-245">Correspondingly, we pop the GameObject off the stack once the gesture is completed.</span></span>

### <a name="build-and-deploy"></a><span data-ttu-id="900c0-246">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="900c0-246">Build and Deploy</span></span>

1. <span data-ttu-id="900c0-247">Régénérez l’application dans Unity, puis générez et déployez à partir de Visual Studio pour l’exécuter dans HoloLens.</span><span class="sxs-lookup"><span data-stu-id="900c0-247">Rebuild the application in Unity and then build and deploy from Visual Studio to run it in the HoloLens.</span></span>
2. <span data-ttu-id="900c0-248">Pointez le curseur sur le astronautes, deux flèches doivent apparaître sur l’un ou l’autre côté du curseur.</span><span class="sxs-lookup"><span data-stu-id="900c0-248">Gaze at the astronaut, two arrows should appear on either side of the cursor.</span></span> <span data-ttu-id="900c0-249">Ce nouvel visuel indique que le astronautes peut être pivoté.</span><span class="sxs-lookup"><span data-stu-id="900c0-249">This new visual indicates that the astronaut can be rotated.</span></span>
3. <span data-ttu-id="900c0-250">Placez votre main à la position prête (index Finger pointant vers le ciel) pour que le HoloLens commence à suivre votre main.</span><span class="sxs-lookup"><span data-stu-id="900c0-250">Place your hand in the ready position (index finger pointed towards the sky) so the HoloLens will start tracking your hand.</span></span>
4. <span data-ttu-id="900c0-251">Pour faire pivoter le astronautes, abaissez votre index à la position de pincement, puis déplacez votre main vers la gauche ou vers la droite pour déclencher le mouvement NavigationX.</span><span class="sxs-lookup"><span data-stu-id="900c0-251">To rotate the astronaut, lower your index finger to a pinch position, and then move your hand left or right to trigger the NavigationX gesture.</span></span>

## <a name="chapter-3---hand-guidance"></a><span data-ttu-id="900c0-252">Chapitre 3-Guide de la main</span><span class="sxs-lookup"><span data-stu-id="900c0-252">Chapter 3 - Hand Guidance</span></span>

>[!VIDEO https://www.youtube.com/embed/ULzlVw4e14I]

### <a name="objectives"></a><span data-ttu-id="900c0-253">Objectifs</span><span class="sxs-lookup"><span data-stu-id="900c0-253">Objectives</span></span>

* <span data-ttu-id="900c0-254">Utilisez le score de l’aide à la **main** pour prédire quand le suivi de la main sera perdu.</span><span class="sxs-lookup"><span data-stu-id="900c0-254">Use **hand guidance score** to help predict when hand tracking will be lost.</span></span>
* <span data-ttu-id="900c0-255">Fournissez **des commentaires sur le curseur** pour montrer quand l’utilisateur est près du bord de la vue de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="900c0-255">Provide **feedback on the cursor** to show when the user's hand nears the camera's edge of view.</span></span>

### <a name="instructions"></a><span data-ttu-id="900c0-256">Instructions</span><span class="sxs-lookup"><span data-stu-id="900c0-256">Instructions</span></span>

1. <span data-ttu-id="900c0-257">Dans le volet **hiérarchie** , sélectionnez l’objet **CursorWithFeedback** .</span><span class="sxs-lookup"><span data-stu-id="900c0-257">In the **Hierarchy** panel, select the **CursorWithFeedback** object.</span></span>
2. <span data-ttu-id="900c0-258">Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="900c0-258">In the **Inspector** panel, click the **Add Component** button.</span></span>
3. <span data-ttu-id="900c0-259">Dans le menu, tapez dans la zone de recherche Guide de la **main**.</span><span class="sxs-lookup"><span data-stu-id="900c0-259">In the menu, type in the search box **Hand Guidance**.</span></span> <span data-ttu-id="900c0-260">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="900c0-260">Select the search result.</span></span>
4. <span data-ttu-id="900c0-261">Dans le dossier **hologrammes** du panneau **projet** , recherchez la ressource **HandGuidanceFeedback** .</span><span class="sxs-lookup"><span data-stu-id="900c0-261">In the **Project** panel **Holograms** folder, find the **HandGuidanceFeedback** asset.</span></span>
5. <span data-ttu-id="900c0-262">Faites glisser et déposez la ressource **HandGuidanceFeedback** sur la propriété de l' **indicateur de guide main** dans le panneau **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="900c0-262">Drag and drop the **HandGuidanceFeedback** asset onto the **Hand Guidance Indicator** property in the **Inspector** panel.</span></span>

### <a name="build-and-deploy"></a><span data-ttu-id="900c0-263">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="900c0-263">Build and Deploy</span></span>

* <span data-ttu-id="900c0-264">Régénérez l’application dans Unity, puis générez et déployez à partir de Visual Studio pour expérimenter l’application sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="900c0-264">Rebuild the application in Unity and then build and deploy from Visual Studio to experience the app on HoloLens.</span></span>
* <span data-ttu-id="900c0-265">Affichez votre main et augmentez votre doigt d’index pour obtenir le suivi.</span><span class="sxs-lookup"><span data-stu-id="900c0-265">Bring your hand into view and raise your index finger to get tracked.</span></span>
* <span data-ttu-id="900c0-266">Commencez à faire pivoter le astronautes avec le mouvement de navigation (pincez le doigt et le curseur de l’index).</span><span class="sxs-lookup"><span data-stu-id="900c0-266">Start rotating the astronaut with the Navigation gesture (pinch your index finger and thumb together).</span></span>
* <span data-ttu-id="900c0-267">Déplacez votre main à gauche, à droite, en haut et en baisse.</span><span class="sxs-lookup"><span data-stu-id="900c0-267">Move your hand far left, right, up, and down.</span></span>
* <span data-ttu-id="900c0-268">À mesure que votre main approche du bord du cadre de mouvement, une flèche doit apparaître en regard du curseur pour vous avertir que le suivi des mains sera perdu.</span><span class="sxs-lookup"><span data-stu-id="900c0-268">As your hand nears the edge of the gesture frame, an arrow should appear next to the cursor to warn you that hand tracking will be lost.</span></span> <span data-ttu-id="900c0-269">La flèche indique la direction dans laquelle déplacer votre main afin d’empêcher la perte du suivi.</span><span class="sxs-lookup"><span data-stu-id="900c0-269">The arrow indicates which direction to move your hand in order to prevent tracking from being lost.</span></span>

## <a name="chapter-4---manipulation"></a><span data-ttu-id="900c0-270">Chapitre 4-manipulation</span><span class="sxs-lookup"><span data-stu-id="900c0-270">Chapter 4 - Manipulation</span></span>

>[!VIDEO https://www.youtube.com/embed/f3m8MvU60-I]

### <a name="objectives"></a><span data-ttu-id="900c0-271">Objectifs</span><span class="sxs-lookup"><span data-stu-id="900c0-271">Objectives</span></span>

* <span data-ttu-id="900c0-272">Utilisez des événements de manipulation pour déplacer le astronautes avec vos mains.</span><span class="sxs-lookup"><span data-stu-id="900c0-272">Use Manipulation events to move the astronaut with your hands.</span></span>
* <span data-ttu-id="900c0-273">Fournissez des commentaires sur le curseur pour permettre à l’utilisateur de savoir quand la manipulation peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="900c0-273">Provide feedback on the cursor to let the user know when Manipulation can be used.</span></span>

### <a name="instructions"></a><span data-ttu-id="900c0-274">Instructions</span><span class="sxs-lookup"><span data-stu-id="900c0-274">Instructions</span></span>

<span data-ttu-id="900c0-275">GestureManager.cs et AstronautManager.cs nous permettront d’effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="900c0-275">GestureManager.cs and AstronautManager.cs will allow us to do the following:</span></span>

1. <span data-ttu-id="900c0-276">Utilisez le mot clé Speech «**Move astronautes**» pour activer les gestes de **manipulation** et «**Rotate astronautes**» pour les désactiver.</span><span class="sxs-lookup"><span data-stu-id="900c0-276">Use the speech keyword "**Move Astronaut**" to enable **Manipulation** gestures and "**Rotate Astronaut**" to disable them.</span></span>
2. <span data-ttu-id="900c0-277">Passez à la réponse à la **reconnaissance de mouvement de manipulation**.</span><span class="sxs-lookup"><span data-stu-id="900c0-277">Switch to responding to the **Manipulation Gesture Recognizer**.</span></span>

<span data-ttu-id="900c0-278">Commençons.</span><span class="sxs-lookup"><span data-stu-id="900c0-278">Let's get started.</span></span>

1. <span data-ttu-id="900c0-279">Dans le volet **hiérarchie** , créez un gameobject vide.</span><span class="sxs-lookup"><span data-stu-id="900c0-279">In the **Hierarchy** panel, create a new empty GameObject.</span></span> <span data-ttu-id="900c0-280">Nommez-le «**AstronautManager**».</span><span class="sxs-lookup"><span data-stu-id="900c0-280">Name it "**AstronautManager**".</span></span>
2. <span data-ttu-id="900c0-281">Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="900c0-281">In the **Inspector** panel, click the **Add Component** button.</span></span>
3. <span data-ttu-id="900c0-282">Dans le menu, tapez dans la zone de recherche **astronautes Manager**.</span><span class="sxs-lookup"><span data-stu-id="900c0-282">In the menu, type in the search box **Astronaut Manager**.</span></span> <span data-ttu-id="900c0-283">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="900c0-283">Select the search result.</span></span>
4. <span data-ttu-id="900c0-284">Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="900c0-284">In the **Inspector** panel, click the **Add Component** button.</span></span>
5. <span data-ttu-id="900c0-285">Dans le menu, tapez la **source d’entrée vocale**de la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="900c0-285">In the menu, type in the search box **Speech Input Source**.</span></span> <span data-ttu-id="900c0-286">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="900c0-286">Select the search result.</span></span>

<span data-ttu-id="900c0-287">Nous allons maintenant ajouter les commandes vocales requises pour contrôler l’état d’interaction du astronautes.</span><span class="sxs-lookup"><span data-stu-id="900c0-287">We'll now add the speech commands required to control the interaction state of the astronaut.</span></span>

1. <span data-ttu-id="900c0-288">Développez la section **Mots clés** dans l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="900c0-288">Expand the **Keywords** section in the **Inspector**.</span></span>
2. <span data-ttu-id="900c0-289">Cliquez sur **+** le côté droit pour ajouter un nouveau mot clé.</span><span class="sxs-lookup"><span data-stu-id="900c0-289">Click the **+** on the right hand side to add a new keyword.</span></span>
3. <span data-ttu-id="900c0-290">Tapez le mot clé en tant que **Move astronautes**.</span><span class="sxs-lookup"><span data-stu-id="900c0-290">Type the Keyword as **Move Astronaut**.</span></span> <span data-ttu-id="900c0-291">N’hésitez pas à ajouter un raccourci clavier si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="900c0-291">Feel free to add a Key Shortcut if desired.</span></span>
4. <span data-ttu-id="900c0-292">Cliquez sur **+** le côté droit pour ajouter un nouveau mot clé.</span><span class="sxs-lookup"><span data-stu-id="900c0-292">Click the **+** on the right hand side to add a new keyword.</span></span>
5. <span data-ttu-id="900c0-293">Tapez le mot clé **Rotate astronautes**.</span><span class="sxs-lookup"><span data-stu-id="900c0-293">Type the Keyword as **Rotate Astronaut**.</span></span> <span data-ttu-id="900c0-294">N’hésitez pas à ajouter un raccourci clavier si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="900c0-294">Feel free to add a Key Shortcut if desired.</span></span>
6. <span data-ttu-id="900c0-295">Le code du gestionnaire correspondant se trouve dans **GestureAction.cs**, dans le gestionnaire **ISpeechHandler. OnSpeechKeywordRecognized** .</span><span class="sxs-lookup"><span data-stu-id="900c0-295">The corresponding handler code can be found in **GestureAction.cs**, in the **ISpeechHandler.OnSpeechKeywordRecognized** handler.</span></span>

![Comment configurer la source d’entrée vocale pour le chapitre 4](images/holograms211-speech.png)

<span data-ttu-id="900c0-297">Ensuite, nous allons configurer les commentaires de manipulation sur le curseur.</span><span class="sxs-lookup"><span data-stu-id="900c0-297">Next, we'll setup the manipulation feedback on the cursor.</span></span>

1. <span data-ttu-id="900c0-298">Dans le dossier **hologrammes** du panneau **projet** , recherchez la ressource **PathingFeedback** .</span><span class="sxs-lookup"><span data-stu-id="900c0-298">In the **Project** panel **Holograms** folder, find the **PathingFeedback** asset.</span></span>
2. <span data-ttu-id="900c0-299">Glissez-déplacez le Prefab **PathingFeedback** vers l’objet **CursorWithFeedback** dans la **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="900c0-299">Drag and drop the **PathingFeedback** prefab onto the **CursorWithFeedback** object in the **Hierarchy**.</span></span>
3. <span data-ttu-id="900c0-300">Dans le volet **hiérarchie** , cliquez sur **CursorWithFeedback**.</span><span class="sxs-lookup"><span data-stu-id="900c0-300">In the **Hierarchy** panel, click on **CursorWithFeedback**.</span></span>
4. <span data-ttu-id="900c0-301">Faites glisser et déposez l’objet **PathingFeedback** à partir de la **hiérarchie** vers la propriété **d’objet de jeu Pathing détectée** dans le composant de **retour de curseur** de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="900c0-301">Drag and drop the **PathingFeedback** object from the **Hierarchy** onto the **Pathing Detected Game Object** property in the **Cursor Feedback** component in the **Inspector**.</span></span>

<span data-ttu-id="900c0-302">À présent, nous devons ajouter du code à **GestureAction.cs** pour activer les éléments suivants:</span><span class="sxs-lookup"><span data-stu-id="900c0-302">Now we need to add code to **GestureAction.cs** to enable the following:</span></span>

1. <span data-ttu-id="900c0-303">Ajoutez du code à la fonction **IManipulationHandler. OnManipulationUpdated** , qui déplacera le astronautes lorsqu’un mouvement de **manipulation** sera détecté.</span><span class="sxs-lookup"><span data-stu-id="900c0-303">Add code to the **IManipulationHandler.OnManipulationUpdated** function, which will move the astronaut when a **Manipulation** gesture is detected.</span></span>
2. <span data-ttu-id="900c0-304">Calculez le **vecteur de déplacement** pour déterminer où le astronautes doit être déplacé en fonction de la position de la main.</span><span class="sxs-lookup"><span data-stu-id="900c0-304">Calculate the **movement vector** to determine where the astronaut should be moved to based on hand position.</span></span>
3. <span data-ttu-id="900c0-305">**Déplacez** le astronautes vers la nouvelle position.</span><span class="sxs-lookup"><span data-stu-id="900c0-305">**Move** the astronaut to the new position.</span></span>

<span data-ttu-id="900c0-306">Effectuez le codage de l’exercice 4. a dans **GestureAction.cs**ou utilisez notre solution complète ci-dessous:</span><span class="sxs-lookup"><span data-stu-id="900c0-306">Complete coding exercise 4.a in **GestureAction.cs**, or use our completed solution below:</span></span>

```cs
using HoloToolkit.Unity.InputModule;
using UnityEngine;

/// <summary>
/// GestureAction performs custom actions based on
/// which gesture is being performed.
/// </summary>
public class GestureAction : MonoBehaviour, INavigationHandler, IManipulationHandler, ISpeechHandler
{
    [Tooltip("Rotation max speed controls amount of rotation.")]
    [SerializeField]
    private float RotationSensitivity = 10.0f;

    private bool isNavigationEnabled = true;
    public bool IsNavigationEnabled
    {
        get { return isNavigationEnabled; }
        set { isNavigationEnabled = value; }
    }

    private Vector3 manipulationOriginalPosition = Vector3.zero;

    void INavigationHandler.OnNavigationStarted(NavigationEventData eventData)
    {
        InputManager.Instance.PushModalInputHandler(gameObject);
    }

    void INavigationHandler.OnNavigationUpdated(NavigationEventData eventData)
    {
        if (isNavigationEnabled)
        {
            /* TODO: DEVELOPER CODING EXERCISE 2.c */

            // 2.c: Calculate a float rotationFactor based on eventData's NormalizedOffset.x multiplied by RotationSensitivity.
            // This will help control the amount of rotation.
            float rotationFactor = eventData.NormalizedOffset.x * RotationSensitivity;

            // 2.c: transform.Rotate around the Y axis using rotationFactor.
            transform.Rotate(new Vector3(0, -1 * rotationFactor, 0));
        }
    }

    void INavigationHandler.OnNavigationCompleted(NavigationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void INavigationHandler.OnNavigationCanceled(NavigationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void IManipulationHandler.OnManipulationStarted(ManipulationEventData eventData)
    {
        if (!isNavigationEnabled)
        {
            InputManager.Instance.PushModalInputHandler(gameObject);

            manipulationOriginalPosition = transform.position;
        }
    }

    void IManipulationHandler.OnManipulationUpdated(ManipulationEventData eventData)
    {
        if (!isNavigationEnabled)
        {
            /* TODO: DEVELOPER CODING EXERCISE 4.a */

            // 4.a: Make this transform's position be the manipulationOriginalPosition + eventData.CumulativeDelta
            transform.position = manipulationOriginalPosition + eventData.CumulativeDelta;
        }
    }

    void IManipulationHandler.OnManipulationCompleted(ManipulationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void IManipulationHandler.OnManipulationCanceled(ManipulationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void ISpeechHandler.OnSpeechKeywordRecognized(SpeechEventData eventData)
    {
        if (eventData.RecognizedText.Equals("Move Astronaut"))
        {
            isNavigationEnabled = false;
        }
        else if (eventData.RecognizedText.Equals("Rotate Astronaut"))
        {
            isNavigationEnabled = true;
        }
        else
        {
            return;
        }

        eventData.Use();
    }
}
```

### <a name="build-and-deploy"></a><span data-ttu-id="900c0-307">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="900c0-307">Build and Deploy</span></span>

* <span data-ttu-id="900c0-308">Régénérez dans Unity, puis générez et déployez à partir de Visual Studio pour exécuter l’application dans HoloLens.</span><span class="sxs-lookup"><span data-stu-id="900c0-308">Rebuild in Unity and then build and deploy from Visual Studio to run the app in HoloLens.</span></span>
* <span data-ttu-id="900c0-309">Déplacez votre main devant le HoloLens et augmentez le doigt de votre index afin qu’il puisse être suivi.</span><span class="sxs-lookup"><span data-stu-id="900c0-309">Move your hand in front of the HoloLens and raise your index finger so that it can be tracked.</span></span>
* <span data-ttu-id="900c0-310">Focus sur le curseur sur le astronautes.</span><span class="sxs-lookup"><span data-stu-id="900c0-310">Focus the cursor over the astronaut.</span></span>
* <span data-ttu-id="900c0-311">Dites «Move astronautes» pour déplacer le astronautes avec un mouvement de manipulation.</span><span class="sxs-lookup"><span data-stu-id="900c0-311">Say 'Move Astronaut' to move the astronaut with a Manipulation gesture.</span></span>
* <span data-ttu-id="900c0-312">Quatre flèches doivent apparaître autour du curseur pour indiquer que le programme va maintenant répondre aux événements de manipulation.</span><span class="sxs-lookup"><span data-stu-id="900c0-312">Four arrows should appear around the cursor to indicate that the program will now respond to Manipulation events.</span></span>
* <span data-ttu-id="900c0-313">Abaissez votre index au niveau de votre curseur et empêchez-vous de le pincer.</span><span class="sxs-lookup"><span data-stu-id="900c0-313">Lower your index finger down to your thumb, and keep them pinched together.</span></span>
* <span data-ttu-id="900c0-314">À mesure que vous déplacez votre main, le astronautes se déplace également (manipulation).</span><span class="sxs-lookup"><span data-stu-id="900c0-314">As you move your hand around, the astronaut will move too (this is Manipulation).</span></span>
* <span data-ttu-id="900c0-315">Augmentez le doigt de votre index pour arrêter la manipulation du astronautes.</span><span class="sxs-lookup"><span data-stu-id="900c0-315">Raise your index finger to stop manipulating the astronaut.</span></span>
* <span data-ttu-id="900c0-316">Remarque : Si vous n’indiquez pas «Move astronautes» avant de déplacer votre main, le mouvement de navigation sera utilisé à la place.</span><span class="sxs-lookup"><span data-stu-id="900c0-316">Note: If you do not say 'Move Astronaut' before moving your hand, then the Navigation gesture will be used instead.</span></span>
* <span data-ttu-id="900c0-317">Dites «Rotate astronautes» pour revenir à l’État rotatif.</span><span class="sxs-lookup"><span data-stu-id="900c0-317">Say 'Rotate Astronaut' to return to the rotatable state.</span></span>

## <a name="chapter-5---model-expansion"></a><span data-ttu-id="900c0-318">Chapitre 5-développement d’un modèle</span><span class="sxs-lookup"><span data-stu-id="900c0-318">Chapter 5 - Model expansion</span></span>

>[!VIDEO https://www.youtube.com/embed/dA11P4P0VO8]

### <a name="objectives"></a><span data-ttu-id="900c0-319">Objectifs</span><span class="sxs-lookup"><span data-stu-id="900c0-319">Objectives</span></span>

* <span data-ttu-id="900c0-320">Développez le modèle astronautes en plusieurs éléments plus petits avec lesquels l’utilisateur peut interagir.</span><span class="sxs-lookup"><span data-stu-id="900c0-320">Expand the Astronaut model into multiple, smaller pieces that the user can interact with.</span></span>
* <span data-ttu-id="900c0-321">Déplacez chaque élément individuellement à l’aide de mouvements de navigation et de manipulation.</span><span class="sxs-lookup"><span data-stu-id="900c0-321">Move each piece individually using Navigation and Manipulation gestures.</span></span>

### <a name="instructions"></a><span data-ttu-id="900c0-322">Instructions</span><span class="sxs-lookup"><span data-stu-id="900c0-322">Instructions</span></span>

<span data-ttu-id="900c0-323">Dans cette section, nous allons effectuer les tâches suivantes:</span><span class="sxs-lookup"><span data-stu-id="900c0-323">In this section, we will accomplish the following tasks:</span></span>

1. <span data-ttu-id="900c0-324">Ajoutez un nouveau mot clé «**expand Model**» pour développer le modèle astronautes.</span><span class="sxs-lookup"><span data-stu-id="900c0-324">Add a new keyword "**Expand Model**" to expand the astronaut model.</span></span>
2. <span data-ttu-id="900c0-325">Ajoutez un nouveau mot clé «**Reset Model**» pour ramener le modèle à son formulaire d’origine.</span><span class="sxs-lookup"><span data-stu-id="900c0-325">Add a new Keyword "**Reset Model**" to return the model to its original form.</span></span>

<span data-ttu-id="900c0-326">Pour ce faire, nous allons ajouter deux mots clés supplémentaires à la source d’entrée vocale du chapitre précédent.</span><span class="sxs-lookup"><span data-stu-id="900c0-326">We'll do this by adding two more keywords to the Speech Input Source from the previous chapter.</span></span> <span data-ttu-id="900c0-327">Nous présenterons également une autre façon de gérer les événements de reconnaissance.</span><span class="sxs-lookup"><span data-stu-id="900c0-327">We'll also demonstrate another way to handle recognition events.</span></span>

1. <span data-ttu-id="900c0-328">Cliquez sur **AstronautManager** dans l' **inspecteur** et développez la section **Mots clés** dans l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="900c0-328">Click back on **AstronautManager** in the **Inspector** and expand the **Keywords** section in the **Inspector**.</span></span>
2. <span data-ttu-id="900c0-329">Cliquez sur **+** le côté droit pour ajouter un nouveau mot clé.</span><span class="sxs-lookup"><span data-stu-id="900c0-329">Click the **+** on the right hand side to add a new keyword.</span></span>
3. <span data-ttu-id="900c0-330">Tapez le mot clé **expand Model**.</span><span class="sxs-lookup"><span data-stu-id="900c0-330">Type the Keyword as **Expand Model**.</span></span> <span data-ttu-id="900c0-331">N’hésitez pas à ajouter un raccourci clavier si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="900c0-331">Feel free to add a Key Shortcut if desired.</span></span>
4. <span data-ttu-id="900c0-332">Cliquez sur **+** le côté droit pour ajouter un nouveau mot clé.</span><span class="sxs-lookup"><span data-stu-id="900c0-332">Click the **+** on the right hand side to add a new keyword.</span></span>
5. <span data-ttu-id="900c0-333">Tapez le mot clé en tant que **modèle**de réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="900c0-333">Type the Keyword as **Reset Model**.</span></span> <span data-ttu-id="900c0-334">N’hésitez pas à ajouter un raccourci clavier si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="900c0-334">Feel free to add a Key Shortcut if desired.</span></span>
6. <span data-ttu-id="900c0-335">Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .</span><span class="sxs-lookup"><span data-stu-id="900c0-335">In the **Inspector** panel, click the **Add Component** button.</span></span>
7. <span data-ttu-id="900c0-336">Dans le menu, tapez dans le **Gestionnaire d’entrée**de la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="900c0-336">In the menu, type in the search box **Speech Input Handler**.</span></span> <span data-ttu-id="900c0-337">Sélectionnez le résultat de la recherche.</span><span class="sxs-lookup"><span data-stu-id="900c0-337">Select the search result.</span></span>
8. <span data-ttu-id="900c0-338">Check **est l’écouteur global**, puisque nous voulons que ces commandes fonctionnent, quel que soit le gameobject que nous allons concentrer.</span><span class="sxs-lookup"><span data-stu-id="900c0-338">Check **Is Global Listener**, since we want these commands to work regardless of the GameObject we're focusing.</span></span>
9. <span data-ttu-id="900c0-339">Cliquez sur **+** le bouton et sélectionnez **développer le modèle** dans la liste déroulante mot clé.</span><span class="sxs-lookup"><span data-stu-id="900c0-339">Click the **+** button and select **Expand Model** from the Keyword dropdown.</span></span>
10. <span data-ttu-id="900c0-340">Cliquez sur **+** le sous réponse, puis faites glisser le **AstronautManager** de la **hiérarchie** vers le champ **aucun (objet)** .</span><span class="sxs-lookup"><span data-stu-id="900c0-340">Click the **+** under Response, and drag the **AstronautManager** from the **Hierarchy** into the **None (Object)** field.</span></span>
11. <span data-ttu-id="900c0-341">Maintenant, cliquez sur la liste déroulante **no Function** , sélectionnez **AstronautManager**, puis **ExpandModelCommand**.</span><span class="sxs-lookup"><span data-stu-id="900c0-341">Now, click the **No Function** dropdown, select **AstronautManager**, then **ExpandModelCommand**.</span></span>
12. <span data-ttu-id="900c0-342">Cliquez sur le bouton du **+** gestionnaire d’entrée vocale et sélectionnez Réinitialiser le **modèle** dans la liste déroulante mot clé.</span><span class="sxs-lookup"><span data-stu-id="900c0-342">Click the Speech Input Handler's **+** button and select **Reset Model** from the Keyword dropdown.</span></span>
13. <span data-ttu-id="900c0-343">Cliquez sur **+** le sous réponse, puis faites glisser le **AstronautManager** de la **hiérarchie** vers le champ **aucun (objet)** .</span><span class="sxs-lookup"><span data-stu-id="900c0-343">Click the **+** under Response, and drag the **AstronautManager** from the **Hierarchy** into the **None (Object)** field.</span></span>
14. <span data-ttu-id="900c0-344">Maintenant, cliquez sur la liste déroulante **no Function** , sélectionnez **AstronautManager**, puis **ResetModelCommand**.</span><span class="sxs-lookup"><span data-stu-id="900c0-344">Now, click the **No Function** dropdown, select **AstronautManager**, then **ResetModelCommand**.</span></span>

![Comment configurer la source et le gestionnaire de l’entrée vocale pour le chapitre 5](images/holograms211-speechhandler.png)

### <a name="build-and-deploy"></a><span data-ttu-id="900c0-346">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="900c0-346">Build and Deploy</span></span>

* <span data-ttu-id="900c0-347">Essayez !</span><span class="sxs-lookup"><span data-stu-id="900c0-347">Try it!</span></span> <span data-ttu-id="900c0-348">Générez et déployez l’application sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="900c0-348">Build and deploy the app to the HoloLens.</span></span>
* <span data-ttu-id="900c0-349">Par exemple, **développez modèle** pour voir le modèle astronautes développé.</span><span class="sxs-lookup"><span data-stu-id="900c0-349">Say **Expand Model** to see the expanded astronaut model.</span></span>
* <span data-ttu-id="900c0-350">Utilisez la **navigation** pour faire pivoter des éléments individuels de la couleur astronautes.</span><span class="sxs-lookup"><span data-stu-id="900c0-350">Use **Navigation** to rotate individual pieces of the astronaut suit.</span></span>
* <span data-ttu-id="900c0-351">Par exemple, vous pouvez **déplacer astronautes** , puis utiliser la **manipulation** pour déplacer des éléments individuels de la couleur astronautes.</span><span class="sxs-lookup"><span data-stu-id="900c0-351">Say **Move Astronaut** and then use **Manipulation** to move individual pieces of the astronaut suit.</span></span>
* <span data-ttu-id="900c0-352">Par exemple, **faites pivoter astronautes** pour faire pivoter les éclats.</span><span class="sxs-lookup"><span data-stu-id="900c0-352">Say **Rotate Astronaut** to rotate the pieces again.</span></span>
* <span data-ttu-id="900c0-353">Par exemple, réinitialisez le **modèle** pour retourner le astronautes sous sa forme d’origine.</span><span class="sxs-lookup"><span data-stu-id="900c0-353">Say **Reset Model** to return the astronaut to its original form.</span></span>

## <a name="the-end"></a><span data-ttu-id="900c0-354">La fin</span><span class="sxs-lookup"><span data-stu-id="900c0-354">The End</span></span>

<span data-ttu-id="900c0-355">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="900c0-355">Congratulations!</span></span> <span data-ttu-id="900c0-356">Vous avez maintenant terminé **l’entrée 211: Mouvement**.</span><span class="sxs-lookup"><span data-stu-id="900c0-356">You have now completed **MR Input 211: Gesture**.</span></span>

* <span data-ttu-id="900c0-357">Vous savez comment détecter et répondre aux événements de suivi de la main, de navigation et de manipulation.</span><span class="sxs-lookup"><span data-stu-id="900c0-357">You know how to detect and respond to hand tracking, navigation and manipulation events.</span></span>
* <span data-ttu-id="900c0-358">Vous comprenez la différence entre les gestes de navigation et de manipulation.</span><span class="sxs-lookup"><span data-stu-id="900c0-358">You understand the difference between Navigation and Manipulation gestures.</span></span>
* <span data-ttu-id="900c0-359">Vous savez comment modifier le curseur pour fournir des commentaires visuels quand une main est détectée, quand une main est sur le point d’être perdue et quand un objet prend en charge différentes interactions (navigation et manipulation).</span><span class="sxs-lookup"><span data-stu-id="900c0-359">You know how to change the cursor to provide visual feedback for when a hand is detected, when a hand is about to be lost, and for when an object supports different interactions (Navigation vs Manipulation).</span></span>
