---
title: Entrée MR 212-voix
description: Suivez cette procédure pas à pas de codage avec Unity, Visual Studio et HoloLens pour apprendre les détails des concepts vocaux.
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, Academy, didacticiel, vocal
ms.openlocfilehash: 9db503ea4c7db9a3eb272ad9663024ca3a407dda
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73434598"
---
>[!NOTE]
><span data-ttu-id="3d522-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="3d522-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="3d522-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="3d522-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="3d522-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="3d522-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="3d522-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3d522-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="3d522-108">[Une nouvelle série de didacticiels](mrlearning-base.md) a été publiée pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="3d522-108">[A new series of tutorials](mrlearning-base.md) has been posted for HoloLens 2.</span></span>

<br>

# <a name="mr-input-212-voice"></a><span data-ttu-id="3d522-109">Entrée MR 212 : voix</span><span class="sxs-lookup"><span data-stu-id="3d522-109">MR Input 212: Voice</span></span>

<span data-ttu-id="3d522-110">La [saisie vocale](voice-input.md) nous offre une autre manière d’interagir avec nos hologrammes.</span><span class="sxs-lookup"><span data-stu-id="3d522-110">[Voice input](voice-input.md) gives us another way to interact with our holograms.</span></span> <span data-ttu-id="3d522-111">Les commandes vocales fonctionnent de manière très naturelle et simple.</span><span class="sxs-lookup"><span data-stu-id="3d522-111">Voice commands work in a very natural and easy way.</span></span> <span data-ttu-id="3d522-112">Concevez vos commandes vocales de sorte qu’elles soient :</span><span class="sxs-lookup"><span data-stu-id="3d522-112">Design your voice commands so that they are:</span></span>

* <span data-ttu-id="3d522-113">Parfois</span><span class="sxs-lookup"><span data-stu-id="3d522-113">Natural</span></span>
* <span data-ttu-id="3d522-114">Facile à mémoriser</span><span class="sxs-lookup"><span data-stu-id="3d522-114">Easy to remember</span></span>
* <span data-ttu-id="3d522-115">Contexte approprié</span><span class="sxs-lookup"><span data-stu-id="3d522-115">Context appropriate</span></span>
* <span data-ttu-id="3d522-116">Suffisamment distinct des autres options dans le même contexte</span><span class="sxs-lookup"><span data-stu-id="3d522-116">Sufficiently distinct from other options within the same context</span></span>

>[!VIDEO https://www.youtube.com/embed/BYpYsVFYjdw]

<span data-ttu-id="3d522-117">Dans les [notions de base de m. 101](holograms-101.md), nous avons utilisé le KeywordRecognizer pour créer deux commandes vocales simples.</span><span class="sxs-lookup"><span data-stu-id="3d522-117">In [MR Basics 101](holograms-101.md), we used the KeywordRecognizer to build two simple voice commands.</span></span> <span data-ttu-id="3d522-118">Dans l’entrée d’Monsieur 212, nous allons approfondir et apprendre à :</span><span class="sxs-lookup"><span data-stu-id="3d522-118">In MR Input 212, we'll dive deeper and learn how to:</span></span>

* <span data-ttu-id="3d522-119">Concevez des commandes vocales optimisées pour le moteur de reconnaissance vocale HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3d522-119">Design voice commands that are optimized for the HoloLens speech engine.</span></span>
* <span data-ttu-id="3d522-120">Faites savoir aux utilisateurs quelles commandes vocales sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="3d522-120">Make the user aware of what voice commands are available.</span></span>
* <span data-ttu-id="3d522-121">Confirmez que nous avons entendu la commande vocale de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3d522-121">Acknowledge that we've heard the user's voice command.</span></span>
* <span data-ttu-id="3d522-122">Comprendre ce que l’utilisateur dit, à l’aide d’un module de reconnaissance de dictée.</span><span class="sxs-lookup"><span data-stu-id="3d522-122">Understand what the user is saying, using a Dictation Recognizer.</span></span>
* <span data-ttu-id="3d522-123">Utilisez un module de reconnaissance grammatical pour écouter les commandes basées sur un SRGS, ou sur la spécification de la grammaire de la reconnaissance vocale, file.</span><span class="sxs-lookup"><span data-stu-id="3d522-123">Use a Grammar Recognizer to listen for commands based on an SRGS, or Speech Recognition Grammar Specification, file.</span></span>

<span data-ttu-id="3d522-124">Dans ce cours, nous allons revisiter l’Explorateur de modèles, que nous avons créé dans l' [entrée 210](holograms-210.md) et l' [entrée Mr 211](holograms-211.md).</span><span class="sxs-lookup"><span data-stu-id="3d522-124">In this course, we'll revisit Model Explorer, which we built in [MR Input 210](holograms-210.md) and [MR Input 211](holograms-211.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="3d522-125">Les vidéos incorporées dans chacun des chapitres ci-dessous ont été enregistrées à l’aide d’une version antérieure d’Unity et de la réalité mixte Toolkit.</span><span class="sxs-lookup"><span data-stu-id="3d522-125">The videos embedded in each of the chapters below were recorded using an older version of Unity and the Mixed Reality Toolkit.</span></span> <span data-ttu-id="3d522-126">Alors que les instructions pas à pas sont précises et actuelles, vous pouvez voir des scripts et des visuels dans les vidéos correspondantes qui sont obsolètes.</span><span class="sxs-lookup"><span data-stu-id="3d522-126">While the step-by-step instructions are accurate and current, you may see scripts and visuals in the corresponding videos that are out-of-date.</span></span> <span data-ttu-id="3d522-127">Les vidéos restent incluses pour l’affiche et les concepts abordés s’appliquent toujours.</span><span class="sxs-lookup"><span data-stu-id="3d522-127">The videos remain included for posterity and because the concepts covered still apply.</span></span>


## <a name="device-support"></a><span data-ttu-id="3d522-128">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="3d522-128">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="3d522-129">Course</span><span class="sxs-lookup"><span data-stu-id="3d522-129">Course</span></span></th><th style="width:150px"> <span data-ttu-id="3d522-130"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="3d522-130"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="3d522-131"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="3d522-131"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="3d522-132">Entrée MR 212 : voix</span><span class="sxs-lookup"><span data-stu-id="3d522-132">MR Input 212: Voice</span></span></td><td style="text-align: center;"> <span data-ttu-id="3d522-133">✔️</span><span class="sxs-lookup"><span data-stu-id="3d522-133">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="3d522-134">✔️</span><span class="sxs-lookup"><span data-stu-id="3d522-134">✔️</span></span></td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="3d522-135">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="3d522-135">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3d522-136">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="3d522-136">Prerequisites</span></span>

* <span data-ttu-id="3d522-137">Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="3d522-137">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="3d522-138">Certaines fonctionnalités C# de programmation de base.</span><span class="sxs-lookup"><span data-stu-id="3d522-138">Some basic C# programming ability.</span></span>
* <span data-ttu-id="3d522-139">Vous devez avoir terminé les [notions de base de m. 101](holograms-101.md).</span><span class="sxs-lookup"><span data-stu-id="3d522-139">You should have completed [MR Basics 101](holograms-101.md).</span></span>
* <span data-ttu-id="3d522-140">Vous devez avoir terminé l' [entrée 210](holograms-210.md).</span><span class="sxs-lookup"><span data-stu-id="3d522-140">You should have completed [MR Input 210](holograms-210.md).</span></span>
* <span data-ttu-id="3d522-141">Vous devez avoir terminé l' [entrée 211](holograms-211.md).</span><span class="sxs-lookup"><span data-stu-id="3d522-141">You should have completed [MR Input 211](holograms-211.md).</span></span>
* <span data-ttu-id="3d522-142">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="3d522-142">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="3d522-143">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="3d522-143">Project files</span></span>

* <span data-ttu-id="3d522-144">Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-212-Voice.zip) requis par le projet.</span><span class="sxs-lookup"><span data-stu-id="3d522-144">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-212-Voice.zip) required by the project.</span></span> <span data-ttu-id="3d522-145">Requiert Unity 2017,2 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3d522-145">Requires Unity 2017.2 or later.</span></span>
* <span data-ttu-id="3d522-146">Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.</span><span class="sxs-lookup"><span data-stu-id="3d522-146">Un-archive the files to your desktop or other easy to reach location.</span></span>

>[!NOTE]
><span data-ttu-id="3d522-147">Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-212-Voice).</span><span class="sxs-lookup"><span data-stu-id="3d522-147">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-212-Voice).</span></span>

### <a name="errata-and-notes"></a><span data-ttu-id="3d522-148">Errata et notes</span><span class="sxs-lookup"><span data-stu-id="3d522-148">Errata and Notes</span></span>

* <span data-ttu-id="3d522-149">L’option « Activer Uniquement mon code » doit être désactivée (*décochée*) dans Visual Studio sous outils-> Options-> le débogage pour atteindre les points d’arrêt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="3d522-149">"Enable Just My Code" needs to be disabled (*unchecked*) in Visual Studio under Tools->Options->Debugging in order to hit breakpoints in your code.</span></span>

## <a name="unity-setup"></a><span data-ttu-id="3d522-150">Configuration de Unity</span><span class="sxs-lookup"><span data-stu-id="3d522-150">Unity Setup</span></span>

### <a name="instructions"></a><span data-ttu-id="3d522-151">Instructions</span><span class="sxs-lookup"><span data-stu-id="3d522-151">Instructions</span></span>

1. <span data-ttu-id="3d522-152">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="3d522-152">Start Unity.</span></span>
2. <span data-ttu-id="3d522-153">Sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="3d522-153">Select **Open**.</span></span>
3. <span data-ttu-id="3d522-154">Accédez au dossier **HolographicAcademy-hologrammees-212-Voice** que vous avez précédemment désinstallé.</span><span class="sxs-lookup"><span data-stu-id="3d522-154">Navigate to the **HolographicAcademy-Holograms-212-Voice** folder you previously un-archived.</span></span>
4. <span data-ttu-id="3d522-155">Recherchez et sélectionnez le dossier **démarrage**/**Explorateur de modèles** .</span><span class="sxs-lookup"><span data-stu-id="3d522-155">Find and select the **Starting**/**Model Explorer** folder.</span></span>
5. <span data-ttu-id="3d522-156">Cliquez sur le bouton **Sélectionner un dossier** .</span><span class="sxs-lookup"><span data-stu-id="3d522-156">Click the **Select Folder** button.</span></span>
6. <span data-ttu-id="3d522-157">Dans le panneau **projet** , développez le dossier **scenes** .</span><span class="sxs-lookup"><span data-stu-id="3d522-157">In the **Project** panel, expand the **Scenes** folder.</span></span>
7. <span data-ttu-id="3d522-158">Double-cliquez sur **ModelExplorer** Scene pour le charger dans Unity.</span><span class="sxs-lookup"><span data-stu-id="3d522-158">Double-click **ModelExplorer** scene to load it in Unity.</span></span>

### <a name="building"></a><span data-ttu-id="3d522-159">Création</span><span class="sxs-lookup"><span data-stu-id="3d522-159">Building</span></span>

1. <span data-ttu-id="3d522-160">Dans Unity, sélectionnez **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="3d522-160">In Unity, select **File > Build Settings**.</span></span>
2. <span data-ttu-id="3d522-161">Si **scenes/ModelExplorer** n’est pas listé dans **scenes dans Build**, cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="3d522-161">If **Scenes/ModelExplorer** is not listed in **Scenes In Build**, click **Add Open Scenes** to add the scene.</span></span>
3. <span data-ttu-id="3d522-162">Si vous développez spécifiquement pour HoloLens, définissez **appareil cible** sur **hololens**.</span><span class="sxs-lookup"><span data-stu-id="3d522-162">If you're specifically developing for HoloLens, set **Target device** to **HoloLens**.</span></span> <span data-ttu-id="3d522-163">Dans le cas contraire, laissez-le sur **un appareil**.</span><span class="sxs-lookup"><span data-stu-id="3d522-163">Otherwise, leave it on **Any device**.</span></span>
4. <span data-ttu-id="3d522-164">Vérifiez que le **type de build** est défini sur **D3D** et que le **Kit de développement logiciel (SDK** ) est défini sur le **dernier installé** (qui doit être le SDK 16299 ou une version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="3d522-164">Ensure **Build Type** is set to **D3D** and **SDK** is set to **Latest installed** (which should be SDK 16299 or newer).</span></span>
5. <span data-ttu-id="3d522-165">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="3d522-165">Click **Build**.</span></span>
6. <span data-ttu-id="3d522-166">Créez un **dossier** nommé « App ».</span><span class="sxs-lookup"><span data-stu-id="3d522-166">Create a **New Folder** named "App".</span></span>
7. <span data-ttu-id="3d522-167">Cliquez sur le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="3d522-167">Single click the **App** folder.</span></span>
8. <span data-ttu-id="3d522-168">Appuyez sur **Sélectionner un dossier** et Unity va commencer à générer le projet pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3d522-168">Press **Select Folder** and Unity will start building the project for Visual Studio.</span></span>

<span data-ttu-id="3d522-169">Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3d522-169">When Unity is done, a File Explorer window will appear.</span></span>

1. <span data-ttu-id="3d522-170">Ouvrez le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="3d522-170">Open the **App** folder.</span></span>
2. <span data-ttu-id="3d522-171">Ouvrez la **solution Visual Studio ModelExplorer**.</span><span class="sxs-lookup"><span data-stu-id="3d522-171">Open the **ModelExplorer Visual Studio Solution**.</span></span>

<span data-ttu-id="3d522-172">En cas de déploiement dans HoloLens :</span><span class="sxs-lookup"><span data-stu-id="3d522-172">If deploying to HoloLens:</span></span>

1. <span data-ttu-id="3d522-173">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.</span><span class="sxs-lookup"><span data-stu-id="3d522-173">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x86**.</span></span>
2. <span data-ttu-id="3d522-174">Cliquez sur la flèche déroulante en regard du bouton ordinateur local, puis sélectionnez **ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="3d522-174">Click on the drop down arrow next to the Local Machine button, and select **Remote Machine**.</span></span>
3. <span data-ttu-id="3d522-175">Entrez **l’adresse IP de votre appareil HoloLens** et définissez le mode d’authentification sur **universel (protocole non chiffré)** .</span><span class="sxs-lookup"><span data-stu-id="3d522-175">Enter **your HoloLens device IP address** and set Authentication Mode to **Universal (Unencrypted Protocol)**.</span></span> <span data-ttu-id="3d522-176">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="3d522-176">Click **Select**.</span></span> <span data-ttu-id="3d522-177">Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées**.</span><span class="sxs-lookup"><span data-stu-id="3d522-177">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options**.</span></span>
4. <span data-ttu-id="3d522-178">Dans la barre de menus supérieure, cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="3d522-178">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="3d522-179">S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le [coupler à Visual Studio](using-visual-studio.md#pairing-your-device).</span><span class="sxs-lookup"><span data-stu-id="3d522-179">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device).</span></span>
5. <span data-ttu-id="3d522-180">Une fois l’application déployée, ignorez le **Fitbox** avec un **mouvement Select**.</span><span class="sxs-lookup"><span data-stu-id="3d522-180">When the app has deployed, dismiss the **Fitbox** with a **select gesture**.</span></span>

<span data-ttu-id="3d522-181">En cas de déploiement sur un casque immersif :</span><span class="sxs-lookup"><span data-stu-id="3d522-181">If deploying to an immersive headset:</span></span>

1. <span data-ttu-id="3d522-182">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x64**.</span><span class="sxs-lookup"><span data-stu-id="3d522-182">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x64**.</span></span>
2. <span data-ttu-id="3d522-183">Assurez-vous que la cible de déploiement est définie sur **ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="3d522-183">Make sure the deployment target is set to **Local Machine**.</span></span>
3. <span data-ttu-id="3d522-184">Dans la barre de menus supérieure, cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="3d522-184">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
4. <span data-ttu-id="3d522-185">Une fois l’application déployée, Faites disparaître le **Fitbox** en tirant le déclencheur sur un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="3d522-185">When the app has deployed, dismiss the **Fitbox** by pulling the trigger on a motion controller.</span></span>

>[!NOTE]
><span data-ttu-id="3d522-186">Vous pouvez remarquer des erreurs rouges dans le panneau erreurs de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3d522-186">You might notice some red errors in the Visual Studio Errors panel.</span></span> <span data-ttu-id="3d522-187">Vous pouvez les ignorer en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="3d522-187">It is safe to ignore them.</span></span> <span data-ttu-id="3d522-188">Basculez vers le panneau sortie pour afficher la progression réelle de la génération.</span><span class="sxs-lookup"><span data-stu-id="3d522-188">Switch to the Output panel to view actual build progress.</span></span> <span data-ttu-id="3d522-189">Les erreurs dans le panneau sortie vous obligent à faire un correctif (le plus souvent, elles sont provoquées par une erreur dans un script).</span><span class="sxs-lookup"><span data-stu-id="3d522-189">Errors in the Output panel will require you to make a fix (most often they are caused by a mistake in a script).</span></span>

## <a name="chapter-1---awareness"></a><span data-ttu-id="3d522-190">Chapitre 1-sensibilisation</span><span class="sxs-lookup"><span data-stu-id="3d522-190">Chapter 1 - Awareness</span></span>

>[!VIDEO https://www.youtube.com/embed/fDwijJWuEc0]

### <a name="objectives"></a><span data-ttu-id="3d522-191">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3d522-191">Objectives</span></span>

* <span data-ttu-id="3d522-192">Découvrez les **dénis** de la conception des commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="3d522-192">Learn the **Dos and Don'ts** of voice command design.</span></span>
* <span data-ttu-id="3d522-193">Utilisez **KeywordRecognizer** pour ajouter des commandes vocales en regard.</span><span class="sxs-lookup"><span data-stu-id="3d522-193">Use **KeywordRecognizer** to add gaze based voice commands.</span></span>
* <span data-ttu-id="3d522-194">Faites savoir aux utilisateurs les commandes vocales à l’aide de **Commentaires**sur les curseurs.</span><span class="sxs-lookup"><span data-stu-id="3d522-194">Make users aware of voice commands using cursor **feedback**.</span></span>

### <a name="voice-command-design"></a><span data-ttu-id="3d522-195">Conception de commande vocale</span><span class="sxs-lookup"><span data-stu-id="3d522-195">Voice Command Design</span></span>

<span data-ttu-id="3d522-196">Dans ce chapitre, vous allez apprendre à concevoir des commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="3d522-196">In this chapter, you'll learn about designing voice commands.</span></span> <span data-ttu-id="3d522-197">Lors de la création de commandes vocales :</span><span class="sxs-lookup"><span data-stu-id="3d522-197">When creating voice commands:</span></span>

#### <a name="do"></a><span data-ttu-id="3d522-198">DO</span><span class="sxs-lookup"><span data-stu-id="3d522-198">DO</span></span>

* <span data-ttu-id="3d522-199">Créer des commandes concises.</span><span class="sxs-lookup"><span data-stu-id="3d522-199">Create concise commands.</span></span> <span data-ttu-id="3d522-200">Vous ne souhaitez pas utiliser *« Lire la vidéo actuellement sélectionnée »* , car cette commande n’est pas concise et peut facilement être oubliée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3d522-200">You don't want to use *"Play the currently selected video"*, because that command is not concise and would easily be forgotten by the user.</span></span> <span data-ttu-id="3d522-201">Au lieu de cela, vous devez utiliser : *« Lire la vidéo »* , car elle est concise et comporte plusieurs syllabes.</span><span class="sxs-lookup"><span data-stu-id="3d522-201">Instead, you should use: *"Play Video"*, because it is concise and has multiple syllables.</span></span>
* <span data-ttu-id="3d522-202">Utilisez un vocabulaire simple.</span><span class="sxs-lookup"><span data-stu-id="3d522-202">Use a simple vocabulary.</span></span> <span data-ttu-id="3d522-203">Essayez toujours d’utiliser des mots et des expressions courants qui sont faciles à découvrir et à mémoriser pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3d522-203">Always try to use common words and phrases that are easy for the user to discover and remember.</span></span> <span data-ttu-id="3d522-204">Par exemple, si votre application comporte un objet note qui peut être affiché ou masqué, vous n’utiliseriez pas la commande *« Show pancarte »* , car « pancarte » est un terme rarement utilisé.</span><span class="sxs-lookup"><span data-stu-id="3d522-204">For example, if your application had a note object that could be displayed or hidden from view, you would not use the command *"Show Placard"*, because "placard" is a rarely used term.</span></span> <span data-ttu-id="3d522-205">Au lieu de cela, vous devez utiliser la commande : *« Show note »* pour révéler la remarque dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3d522-205">Instead, you would use the command: *"Show Note"*, to reveal the note in your application.</span></span>
* <span data-ttu-id="3d522-206">Soyez cohérent.</span><span class="sxs-lookup"><span data-stu-id="3d522-206">Be consistent.</span></span> <span data-ttu-id="3d522-207">Les commandes vocales doivent rester cohérentes dans l’ensemble de votre application.</span><span class="sxs-lookup"><span data-stu-id="3d522-207">Voice commands should be kept consistent across your application.</span></span> <span data-ttu-id="3d522-208">Imaginez que vous avez deux scènes dans votre application et que les deux scènes contiennent un bouton pour fermer l’application.</span><span class="sxs-lookup"><span data-stu-id="3d522-208">Imagine that you have two scenes in your application and both scenes contain a button for closing the application.</span></span> <span data-ttu-id="3d522-209">Si la première scène a utilisé la commande *« Exit »* pour déclencher le bouton, alors que la deuxième scène a utilisé la commande *« Close App »* , l’utilisateur va être très confus.</span><span class="sxs-lookup"><span data-stu-id="3d522-209">If the first scene used the command *"Exit"* to trigger the button, but the second scene used the command *"Close App"*, then the user is going to get very confused.</span></span> <span data-ttu-id="3d522-210">Si la même fonctionnalité persiste sur plusieurs scènes, la même commande vocale doit être utilisée pour la déclencher.</span><span class="sxs-lookup"><span data-stu-id="3d522-210">If the same functionality persists across multiple scenes, then the same voice command should be used to trigger it.</span></span>

#### <a name="dont"></a><span data-ttu-id="3d522-211">Ne pas</span><span class="sxs-lookup"><span data-stu-id="3d522-211">DON'T</span></span>

* <span data-ttu-id="3d522-212">Utilisez des commandes d’une seule syllabe.</span><span class="sxs-lookup"><span data-stu-id="3d522-212">Use single syllable commands.</span></span> <span data-ttu-id="3d522-213">Par exemple, si vous créez une commande vocale pour lire une vidéo, vous devez éviter d’utiliser la commande simple *« lecture »* , car il ne s’agit que d’une seule syllabe qui peut être facilement manquée par le système.</span><span class="sxs-lookup"><span data-stu-id="3d522-213">As an example, if you were creating a voice command to play a video, you should avoid using the simple command *"Play"*, as it is only a single syllable and could easily be missed by the system.</span></span> <span data-ttu-id="3d522-214">Au lieu de cela, vous devez utiliser : *« Lire la vidéo »* , car elle est concise et comporte plusieurs syllabes.</span><span class="sxs-lookup"><span data-stu-id="3d522-214">Instead, you should use: *"Play Video"*, because it is concise and has multiple syllables.</span></span>
* <span data-ttu-id="3d522-215">Utilisez les commandes système.</span><span class="sxs-lookup"><span data-stu-id="3d522-215">Use system commands.</span></span> <span data-ttu-id="3d522-216">La commande *« Select »* est réservée par le système pour déclencher un événement TAP pour l’objet actuellement actif.</span><span class="sxs-lookup"><span data-stu-id="3d522-216">The *"Select"* command is reserved by the system to trigger a Tap event for the currently focused object.</span></span> <span data-ttu-id="3d522-217">Ne réutilisez pas la commande *« Select »* dans un mot clé ou une expression, car elle risque de ne pas fonctionner comme prévu.</span><span class="sxs-lookup"><span data-stu-id="3d522-217">Do not re-use the *"Select"* command in a keyword or phrase, as it might not work as you expect.</span></span> <span data-ttu-id="3d522-218">Par exemple, si la commande de voix pour la sélection d’un cube dans votre application était *« Sélectionner un cube »* , mais que l’utilisateur regardait une sphère lorsqu’il a intégré la commande, la sphère serait sélectionnée à la place.</span><span class="sxs-lookup"><span data-stu-id="3d522-218">For example, if the voice command for selecting a cube in your application was *"Select cube"*, but the user was looking at a sphere when they uttered the command, then the sphere would be selected instead.</span></span> <span data-ttu-id="3d522-219">De même, les commandes de la barre d’application sont activées pour la voix.</span><span class="sxs-lookup"><span data-stu-id="3d522-219">Similarly app bar commands are voice enabled.</span></span> <span data-ttu-id="3d522-220">N’utilisez pas les commandes vocales suivantes dans votre vue CoreWindow :</span><span class="sxs-lookup"><span data-stu-id="3d522-220">Don't use the following speech commands in your CoreWindow View:</span></span>
    1. <span data-ttu-id="3d522-221">Retour</span><span class="sxs-lookup"><span data-stu-id="3d522-221">Go Back</span></span>
    2. <span data-ttu-id="3d522-222">Outil de défilement</span><span class="sxs-lookup"><span data-stu-id="3d522-222">Scroll Tool</span></span>
    3. <span data-ttu-id="3d522-223">Outil zoom</span><span class="sxs-lookup"><span data-stu-id="3d522-223">Zoom Tool</span></span>
    4. <span data-ttu-id="3d522-224">Faire glisser l’outil</span><span class="sxs-lookup"><span data-stu-id="3d522-224">Drag Tool</span></span>
    5. <span data-ttu-id="3d522-225">Ajuster</span><span class="sxs-lookup"><span data-stu-id="3d522-225">Adjust</span></span>
    6. <span data-ttu-id="3d522-226">Remove</span><span class="sxs-lookup"><span data-stu-id="3d522-226">Remove</span></span>
* <span data-ttu-id="3d522-227">Utilisez des sons similaires.</span><span class="sxs-lookup"><span data-stu-id="3d522-227">Use similar sounds.</span></span> <span data-ttu-id="3d522-228">Essayez d’éviter d’utiliser des commandes vocales qui agencement.</span><span class="sxs-lookup"><span data-stu-id="3d522-228">Try to avoid using voice commands that rhyme.</span></span> <span data-ttu-id="3d522-229">Si vous aviez une application d’achat qui prenait en charge *« afficher le magasin »* et *« afficher plus »* en tant que commandes vocales, vous souhaiterez désactiver l’une des commandes pendant que l’autre était en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="3d522-229">If you had a shopping application which supported *"Show Store"* and *"Show More"* as voice commands, then you would want to disable one of the commands while the other was in use.</span></span> <span data-ttu-id="3d522-230">Par exemple, vous pouvez utiliser le bouton *« afficher le magasin »* pour ouvrir le magasin, puis désactiver cette commande lors de l’affichage de la Banque afin que la commande *« afficher plus »* puisse être utilisée pour la navigation.</span><span class="sxs-lookup"><span data-stu-id="3d522-230">For example, you could use the *"Show Store"* button to open the store, and then disable that command when the store was displayed so that the *"Show More"* command could be used for browsing.</span></span>

### <a name="instructions"></a><span data-ttu-id="3d522-231">Instructions</span><span class="sxs-lookup"><span data-stu-id="3d522-231">Instructions</span></span>

* <span data-ttu-id="3d522-232">Dans le panneau de la **hiérarchie** Unity, utilisez l’outil de recherche pour Rechercher l’objet **holoComm_screen_mesh** .</span><span class="sxs-lookup"><span data-stu-id="3d522-232">In Unity's **Hierarchy** panel, use the search tool to find the **holoComm_screen_mesh** object.</span></span>
* <span data-ttu-id="3d522-233">Double-cliquez sur l’objet **holoComm_screen_mesh** pour l’afficher dans la **scène**.</span><span class="sxs-lookup"><span data-stu-id="3d522-233">Double-click on the **holoComm_screen_mesh** object to view it in the **Scene**.</span></span> <span data-ttu-id="3d522-234">Il s’agit de la montre de astronautes, qui répondra à nos commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="3d522-234">This is the astronaut's watch, which will respond to our voice commands.</span></span>
* <span data-ttu-id="3d522-235">Dans le volet de l' **inspecteur** , localisez le composant **source d’entrée vocale (script)** .</span><span class="sxs-lookup"><span data-stu-id="3d522-235">In the **Inspector** panel, locate the **Speech Input Source (Script)** component.</span></span>
* <span data-ttu-id="3d522-236">Développez la section **Mots clés** pour voir la commande vocale prise en charge : **ouvrir Communicator**.</span><span class="sxs-lookup"><span data-stu-id="3d522-236">Expand the **Keywords** section to see the supported voice command: **Open Communicator**.</span></span>
* <span data-ttu-id="3d522-237">Cliquez sur le roue dentée situé à droite, puis sélectionnez **modifier le script**.</span><span class="sxs-lookup"><span data-stu-id="3d522-237">Click the cog to the right side, then select **Edit Script**.</span></span>
* <span data-ttu-id="3d522-238">Explorez **SpeechInputSource.cs** pour comprendre comment il utilise **KeywordRecognizer** pour ajouter des commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="3d522-238">Explore **SpeechInputSource.cs** to understand how it uses the **KeywordRecognizer** to add voice commands.</span></span>

### <a name="build-and-deploy"></a><span data-ttu-id="3d522-239">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="3d522-239">Build and Deploy</span></span>

* <span data-ttu-id="3d522-240">Dans Unity, utilisez les **paramètres de build de > de fichiers** pour régénérer l’application.</span><span class="sxs-lookup"><span data-stu-id="3d522-240">In Unity, use **File > Build Settings** to rebuild the application.</span></span>
* <span data-ttu-id="3d522-241">Ouvrez le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="3d522-241">Open the **App** folder.</span></span>
* <span data-ttu-id="3d522-242">Ouvrez la **solution Visual Studio ModelExplorer**.</span><span class="sxs-lookup"><span data-stu-id="3d522-242">Open the **ModelExplorer Visual Studio Solution**.</span></span>

<span data-ttu-id="3d522-243">(Si vous avez déjà généré/déployé ce projet dans Visual Studio au cours de la configuration, vous pouvez ouvrir cette instance de VS et cliquer sur « recharger tout » lorsque vous y êtes invité).</span><span class="sxs-lookup"><span data-stu-id="3d522-243">(If you already built/deployed this project in Visual Studio during set-up, then you can open that instance of VS and click 'Reload All' when prompted).</span></span>

* <span data-ttu-id="3d522-244">Dans Visual Studio, cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="3d522-244">In Visual Studio, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
* <span data-ttu-id="3d522-245">Une fois que l’application a été déployée sur HoloLens, ignorez la zone d’ajustement à l’aide du mouvement d' [appui sur l’air](gaze-and-commit.md#composite-gestures) .</span><span class="sxs-lookup"><span data-stu-id="3d522-245">After the application deploys to the HoloLens, dismiss the fit box using the [air-tap](gaze-and-commit.md#composite-gestures) gesture.</span></span>
* <span data-ttu-id="3d522-246">Pointez le regard de la montre du astronautes.</span><span class="sxs-lookup"><span data-stu-id="3d522-246">Gaze at the astronaut's watch.</span></span>
* <span data-ttu-id="3d522-247">Lorsque la montre a le focus, vérifiez que le curseur se transforme en microphone.</span><span class="sxs-lookup"><span data-stu-id="3d522-247">When the watch has focus, verify that the cursor changes to a microphone.</span></span> <span data-ttu-id="3d522-248">Cela fournit des commentaires que l’application écoute pour les commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="3d522-248">This provides feedback that the application is listening for voice commands.</span></span>
* <span data-ttu-id="3d522-249">Vérifiez qu’une info-bulle apparaît sur la montre.</span><span class="sxs-lookup"><span data-stu-id="3d522-249">Verify that a tooltip appears on the watch.</span></span> <span data-ttu-id="3d522-250">Cela aide les utilisateurs à découvrir la commande *« Open Communicator »* .</span><span class="sxs-lookup"><span data-stu-id="3d522-250">This helps users discover the *"Open Communicator"* command.</span></span>
* <span data-ttu-id="3d522-251">Si Gazing à la montre, dites *« ouvrir Communicator »* pour ouvrir le panneau Communicator.</span><span class="sxs-lookup"><span data-stu-id="3d522-251">While gazing at the watch, say *"Open Communicator"* to open the communicator panel.</span></span>

## <a name="chapter-2---acknowledgement"></a><span data-ttu-id="3d522-252">Chapitre 2-accusé de réception</span><span class="sxs-lookup"><span data-stu-id="3d522-252">Chapter 2 - Acknowledgement</span></span>

>[!VIDEO https://www.youtube.com/embed/87ViteoPpyU]

### <a name="objectives"></a><span data-ttu-id="3d522-253">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3d522-253">Objectives</span></span>

* <span data-ttu-id="3d522-254">Enregistrez un message à l’aide de l’entrée microphone.</span><span class="sxs-lookup"><span data-stu-id="3d522-254">Record a message using the Microphone input.</span></span>
* <span data-ttu-id="3d522-255">Envoyer des commentaires à l’utilisateur que l’application écoute sur sa voix.</span><span class="sxs-lookup"><span data-stu-id="3d522-255">Give feedback to the user that the application is listening to their voice.</span></span>

>[!NOTE]
><span data-ttu-id="3d522-256">La fonctionnalité **microphone** doit être déclarée pour qu’une application soit enregistrée à partir du microphone.</span><span class="sxs-lookup"><span data-stu-id="3d522-256">The **Microphone** capability must be declared for an app to record from the microphone.</span></span> <span data-ttu-id="3d522-257">Cela est fait pour vous déjà dans une entrée de m. 212, mais gardez cela à l’esprit pour vos propres projets.</span><span class="sxs-lookup"><span data-stu-id="3d522-257">This is done for you already in MR Input 212, but keep this in mind for your own projects.</span></span>
>
>1. <span data-ttu-id="3d522-258">Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à « modifier les paramètres du projet > > Player ».</span><span class="sxs-lookup"><span data-stu-id="3d522-258">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player"</span></span>
>2. <span data-ttu-id="3d522-259">Cliquez sur l’onglet « plateforme Windows universelle »</span><span class="sxs-lookup"><span data-stu-id="3d522-259">Click on the "Universal Windows Platform" tab</span></span>
>3. <span data-ttu-id="3d522-260">Dans la section « fonctionnalités de > des paramètres de publication », vérifiez la fonctionnalité du **microphone** .</span><span class="sxs-lookup"><span data-stu-id="3d522-260">In the "Publishing Settings > Capabilities" section, check the **Microphone** capability</span></span>

### <a name="instructions"></a><span data-ttu-id="3d522-261">Instructions</span><span class="sxs-lookup"><span data-stu-id="3d522-261">Instructions</span></span>

* <span data-ttu-id="3d522-262">Dans le panneau de la **hiérarchie** Unity, vérifiez que l’objet **holoComm_screen_mesh** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3d522-262">In Unity's **Hierarchy** panel, verify that the **holoComm_screen_mesh** object is selected.</span></span>
* <span data-ttu-id="3d522-263">Dans le volet de l' **inspecteur** , recherchez le composant **astronautes Watch (script)** .</span><span class="sxs-lookup"><span data-stu-id="3d522-263">In the **Inspector** panel, find the **Astronaut Watch (Script)** component.</span></span>
* <span data-ttu-id="3d522-264">Cliquez sur le petit cube bleu défini comme valeur de la propriété **Communicator Prefab** .</span><span class="sxs-lookup"><span data-stu-id="3d522-264">Click on the small, blue cube which is set as the value of the **Communicator Prefab** property.</span></span>
* <span data-ttu-id="3d522-265">Dans le panneau **projet** , le Prefab **Communicator** doit maintenant avoir le focus.</span><span class="sxs-lookup"><span data-stu-id="3d522-265">In the **Project** panel, the **Communicator** prefab should now have focus.</span></span>
* <span data-ttu-id="3d522-266">Cliquez sur le Prefab **Communicator** dans le panneau **projet** pour afficher ses composants dans l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="3d522-266">Click on the **Communicator** prefab in the **Project** panel to view its components in the **Inspector**.</span></span>
* <span data-ttu-id="3d522-267">Examinez le composant du **Gestionnaire de microphone (script)** , ceci nous permettra d’enregistrer la voix de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3d522-267">Look at the **Microphone Manager (Script)** component, this will allow us to record the user's voice.</span></span>
* <span data-ttu-id="3d522-268">Notez que l’objet **Communicator** possède un composant **Gestionnaire d’entrée vocale (script)** pour répondre à la commande **Envoyer un message** .</span><span class="sxs-lookup"><span data-stu-id="3d522-268">Notice that the **Communicator** object has a **Speech Input Handler (Script)** component for responding to the **Send Message** command.</span></span>
* <span data-ttu-id="3d522-269">Examinez le composant **Communicator (script)** et double-cliquez sur le script pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3d522-269">Look at the **Communicator (Script)** component and double-click on the script to open it in Visual Studio.</span></span>

<span data-ttu-id="3d522-270">Communicator.cs est chargé de définir les États de bouton appropriés sur le périphérique Communicator.</span><span class="sxs-lookup"><span data-stu-id="3d522-270">Communicator.cs is responsible for setting the proper button states on the communicator device.</span></span> <span data-ttu-id="3d522-271">Cela permet à nos utilisateurs d’enregistrer un message, de le lire et d’envoyer le message à astronautes.</span><span class="sxs-lookup"><span data-stu-id="3d522-271">This will allow our users to record a message, play it back, and send the message to the astronaut.</span></span> <span data-ttu-id="3d522-272">Il démarre et arrête également un formulaire d’onde animée, pour accuser réception à l’utilisateur que sa voix a été entendue.</span><span class="sxs-lookup"><span data-stu-id="3d522-272">It will also start and stop an animated wave form, to acknowledge to the user that their voice was heard.</span></span>

* <span data-ttu-id="3d522-273">Dans **Communicator.cs**, supprimez les lignes suivantes (81 et 82) de la méthode **Start** .</span><span class="sxs-lookup"><span data-stu-id="3d522-273">In **Communicator.cs**, delete the following lines (81 and 82) from the **Start** method.</span></span> <span data-ttu-id="3d522-274">Cela active le bouton « enregistrer » sur le Communicator.</span><span class="sxs-lookup"><span data-stu-id="3d522-274">This will enable the 'Record' button on the communicator.</span></span>

```cs
// TODO: 2.a Delete the following two lines:
RecordButton.SetActive(false);
MessageUIRenderer.gameObject.SetActive(false);
```

### <a name="build-and-deploy"></a><span data-ttu-id="3d522-275">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="3d522-275">Build and Deploy</span></span>

* <span data-ttu-id="3d522-276">Dans Visual Studio, régénérez votre application et déployez-la sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3d522-276">In Visual Studio, rebuild your application and deploy to the device.</span></span>
* <span data-ttu-id="3d522-277">Pointez le regard du astronautes et dites *« ouvrir Communicator »* pour afficher le Communicator.</span><span class="sxs-lookup"><span data-stu-id="3d522-277">Gaze at the astronaut's watch and say *"Open Communicator"* to show the communicator.</span></span>
* <span data-ttu-id="3d522-278">Appuyez sur le bouton d' **enregistrement** (microphone) pour démarrer l’enregistrement d’un message verbal pour le astronautes.</span><span class="sxs-lookup"><span data-stu-id="3d522-278">Press the **Record** button (microphone) to start recording a verbal message for the astronaut.</span></span>
* <span data-ttu-id="3d522-279">Commencez à parler et vérifiez que l’animation Wave est jouée sur le Communicator, ce qui fournit des commentaires à l’utilisateur indiquant que sa voix est audible.</span><span class="sxs-lookup"><span data-stu-id="3d522-279">Start speaking, and verify that the wave animation plays on the communicator, which provides feedback to the user that their voice is heard.</span></span>
* <span data-ttu-id="3d522-280">Appuyez sur le bouton **arrêter** (carré gauche) et vérifiez que l’animation Wave cesse de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="3d522-280">Press the **Stop** button (left square), and verify that the wave animation stops running.</span></span>
* <span data-ttu-id="3d522-281">Appuyez sur le bouton de **lecture** (triangle rectangle) pour lire le message enregistré et l’écouter sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3d522-281">Press the **Play** button (right triangle) to play back the recorded message and hear it on the device.</span></span>
* <span data-ttu-id="3d522-282">Appuyez sur le bouton **arrêter** (carré droit) pour arrêter la lecture du message enregistré.</span><span class="sxs-lookup"><span data-stu-id="3d522-282">Press the **Stop** button (right square) to stop playback of the recorded message.</span></span>
* <span data-ttu-id="3d522-283">Dites *« Envoyer un message »* pour fermer le Communicator et recevoir une réponse « message received » de astronautes.</span><span class="sxs-lookup"><span data-stu-id="3d522-283">Say *"Send Message"* to close the communicator and receive a 'Message Received' response from the astronaut.</span></span>

## <a name="chapter-3---understanding-and-the-dictation-recognizer"></a><span data-ttu-id="3d522-284">Chapitre 3 : compréhension et le module de reconnaissance de la dictée</span><span class="sxs-lookup"><span data-stu-id="3d522-284">Chapter 3 - Understanding and the Dictation Recognizer</span></span>

>[!VIDEO https://www.youtube.com/embed/TIMddr-HqEU]

### <a name="objectives"></a><span data-ttu-id="3d522-285">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3d522-285">Objectives</span></span>

* <span data-ttu-id="3d522-286">Utilisez le module de reconnaissance de dictée pour convertir la parole de l’utilisateur en texte.</span><span class="sxs-lookup"><span data-stu-id="3d522-286">Use the Dictation Recognizer to convert the user's speech to text.</span></span>
* <span data-ttu-id="3d522-287">Affichez les résultats de l’hypothèse et du résultat final du module de reconnaissance de dictée dans Communicator.</span><span class="sxs-lookup"><span data-stu-id="3d522-287">Show the Dictation Recognizer's hypothesized and final results in the communicator.</span></span>

<span data-ttu-id="3d522-288">Dans ce chapitre, nous allons utiliser le module de reconnaissance de dictée pour créer un message pour le astronautes.</span><span class="sxs-lookup"><span data-stu-id="3d522-288">In this chapter, we'll use the Dictation Recognizer to create a message for the astronaut.</span></span> <span data-ttu-id="3d522-289">Lorsque vous utilisez le module de reconnaissance de dictée, gardez à l’esprit que :</span><span class="sxs-lookup"><span data-stu-id="3d522-289">When using the Dictation Recognizer, keep in mind that:</span></span>

* <span data-ttu-id="3d522-290">Vous devez être connecté à WiFi pour que le module de reconnaissance de dictée fonctionne.</span><span class="sxs-lookup"><span data-stu-id="3d522-290">You must be connected to WiFi for the Dictation Recognizer to work.</span></span>
* <span data-ttu-id="3d522-291">Les délais d’attente se produisent après un laps de temps défini.</span><span class="sxs-lookup"><span data-stu-id="3d522-291">Timeouts occur after a set period of time.</span></span> <span data-ttu-id="3d522-292">Deux délais d’attente doivent être pris en compte :</span><span class="sxs-lookup"><span data-stu-id="3d522-292">There are two timeouts to be aware of:</span></span>
  * <span data-ttu-id="3d522-293">Si le module de reconnaissance démarre et n’entend aucun audio pendant les cinq premières secondes, il expire.</span><span class="sxs-lookup"><span data-stu-id="3d522-293">If the recognizer starts and doesn't hear any audio for the first five seconds, it will timeout.</span></span>
  * <span data-ttu-id="3d522-294">Si le module de reconnaissance a donné un résultat, mais émet un silence pendant vingt secondes, il expire.</span><span class="sxs-lookup"><span data-stu-id="3d522-294">If the recognizer has given a result but then hears silence for twenty seconds, it will timeout.</span></span>
* <span data-ttu-id="3d522-295">Un seul type de module de reconnaissance (mot clé ou dictée) peut s’exécuter à la fois.</span><span class="sxs-lookup"><span data-stu-id="3d522-295">Only one type of recognizer (Keyword or Dictation) can run at a time.</span></span>

>[!NOTE]
><span data-ttu-id="3d522-296">La fonctionnalité **microphone** doit être déclarée pour qu’une application soit enregistrée à partir du microphone.</span><span class="sxs-lookup"><span data-stu-id="3d522-296">The **Microphone** capability must be declared for an app to record from the microphone.</span></span> <span data-ttu-id="3d522-297">Cela est fait pour vous déjà dans une entrée de m. 212, mais gardez cela à l’esprit pour vos propres projets.</span><span class="sxs-lookup"><span data-stu-id="3d522-297">This is done for you already in MR Input 212, but keep this in mind for your own projects.</span></span>
>
>1. <span data-ttu-id="3d522-298">Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à « modifier les paramètres du projet > > Player ».</span><span class="sxs-lookup"><span data-stu-id="3d522-298">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player"</span></span>
>2. <span data-ttu-id="3d522-299">Cliquez sur l’onglet « plateforme Windows universelle »</span><span class="sxs-lookup"><span data-stu-id="3d522-299">Click on the "Universal Windows Platform" tab</span></span>
>3. <span data-ttu-id="3d522-300">Dans la section « fonctionnalités de > des paramètres de publication », vérifiez la fonctionnalité du **microphone** .</span><span class="sxs-lookup"><span data-stu-id="3d522-300">In the "Publishing Settings > Capabilities" section, check the **Microphone** capability</span></span>

### <a name="instructions"></a><span data-ttu-id="3d522-301">Instructions</span><span class="sxs-lookup"><span data-stu-id="3d522-301">Instructions</span></span>

<span data-ttu-id="3d522-302">Nous allons modifier **MicrophoneManager.cs** pour utiliser le module de reconnaissance de dictée.</span><span class="sxs-lookup"><span data-stu-id="3d522-302">We're going to edit **MicrophoneManager.cs** to use the Dictation Recognizer.</span></span> <span data-ttu-id="3d522-303">Voici ce que nous allons ajouter :</span><span class="sxs-lookup"><span data-stu-id="3d522-303">This is what we'll add:</span></span>

1. <span data-ttu-id="3d522-304">Lorsque vous appuyez sur le **bouton d’enregistrement** , nous allons **Démarrer le DictationRecognizer**.</span><span class="sxs-lookup"><span data-stu-id="3d522-304">When the **Record button** is pressed, we'll **start the DictationRecognizer**.</span></span>
2. <span data-ttu-id="3d522-305">Montrez l' **hypothèse** de ce que le DictationRecognizer a compris.</span><span class="sxs-lookup"><span data-stu-id="3d522-305">Show the **hypothesis** of what the DictationRecognizer understood.</span></span>
3. <span data-ttu-id="3d522-306">Verrouillez les **résultats** de ce que le DictationRecognizer a compris.</span><span class="sxs-lookup"><span data-stu-id="3d522-306">Lock in the **results** of what the DictationRecognizer understood.</span></span>
4. <span data-ttu-id="3d522-307">Vérifiez les délais d’attente à partir du DictationRecognizer.</span><span class="sxs-lookup"><span data-stu-id="3d522-307">Check for timeouts from the DictationRecognizer.</span></span>
5. <span data-ttu-id="3d522-308">Lorsque vous appuyez sur le **bouton arrêter** ou que la session MIC expire, **Arrêtez le DictationRecognizer**.</span><span class="sxs-lookup"><span data-stu-id="3d522-308">When the **Stop button** is pressed, or the mic session times out, **stop the DictationRecognizer**.</span></span>
6. <span data-ttu-id="3d522-309">Redémarrez **KeywordRecognizer**, qui écoutera la commande **Envoyer un message** .</span><span class="sxs-lookup"><span data-stu-id="3d522-309">Restart the **KeywordRecognizer**, which will listen for the **Send Message** command.</span></span>

<span data-ttu-id="3d522-310">Commençons.</span><span class="sxs-lookup"><span data-stu-id="3d522-310">Let's get started.</span></span> <span data-ttu-id="3d522-311">Terminez tous les exercices de codage pour 3. a dans **MicrophoneManager.cs**, ou copiez et collez le code final trouvé ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3d522-311">Complete all coding exercises for 3.a in **MicrophoneManager.cs**, or copy and paste the finished code found below:</span></span>

```cs
// Copyright (c) Microsoft Corporation. All rights reserved.
// Licensed under the MIT License. See LICENSE in the project root for license information.

using System.Collections;
using System.Text;
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.Windows.Speech;

namespace Academy
{
    public class MicrophoneManager : MonoBehaviour
    {
        [Tooltip("A text area for the recognizer to display the recognized strings.")]
        [SerializeField]
        private Text dictationDisplay;

        private DictationRecognizer dictationRecognizer;

        // Use this string to cache the text currently displayed in the text box.
        private StringBuilder textSoFar;

        // Using an empty string specifies the default microphone.
        private static string deviceName = string.Empty;
        private int samplingRate;
        private const int messageLength = 10;

        // Use this to reset the UI once the Microphone is done recording after it was started.
        private bool hasRecordingStarted;

        void Awake()
        {
            /* TODO: DEVELOPER CODING EXERCISE 3.a */

            // 3.a: Create a new DictationRecognizer and assign it to dictationRecognizer variable.
            dictationRecognizer = new DictationRecognizer();

            // 3.a: Register for dictationRecognizer.DictationHypothesis and implement DictationHypothesis below
            // This event is fired while the user is talking. As the recognizer listens, it provides text of what it's heard so far.
            dictationRecognizer.DictationHypothesis += DictationRecognizer_DictationHypothesis;

            // 3.a: Register for dictationRecognizer.DictationResult and implement DictationResult below
            // This event is fired after the user pauses, typically at the end of a sentence. The full recognized string is returned here.
            dictationRecognizer.DictationResult += DictationRecognizer_DictationResult;

            // 3.a: Register for dictationRecognizer.DictationComplete and implement DictationComplete below
            // This event is fired when the recognizer stops, whether from Stop() being called, a timeout occurring, or some other error.
            dictationRecognizer.DictationComplete += DictationRecognizer_DictationComplete;

            // 3.a: Register for dictationRecognizer.DictationError and implement DictationError below
            // This event is fired when an error occurs.
            dictationRecognizer.DictationError += DictationRecognizer_DictationError;

            // Query the maximum frequency of the default microphone. Use 'unused' to ignore the minimum frequency.
            int unused;
            Microphone.GetDeviceCaps(deviceName, out unused, out samplingRate);

            // Use this string to cache the text currently displayed in the text box.
            textSoFar = new StringBuilder();

            // Use this to reset the UI once the Microphone is done recording after it was started.
            hasRecordingStarted = false;
        }

        void Update()
        {
            // 3.a: Add condition to check if dictationRecognizer.Status is Running
            if (hasRecordingStarted && !Microphone.IsRecording(deviceName) && dictationRecognizer.Status == SpeechSystemStatus.Running)
            {
                // Reset the flag now that we're cleaning up the UI.
                hasRecordingStarted = false;

                // This acts like pressing the Stop button and sends the message to the Communicator.
                // If the microphone stops as a result of timing out, make sure to manually stop the dictation recognizer.
                // Look at the StopRecording function.
                SendMessage("RecordStop");
            }
        }

        /// <summary>
        /// Turns on the dictation recognizer and begins recording audio from the default microphone.
        /// </summary>
        /// <returns>The audio clip recorded from the microphone.</returns>
        public AudioClip StartRecording()
        {
            // 3.a Shutdown the PhraseRecognitionSystem. This controls the KeywordRecognizers
            PhraseRecognitionSystem.Shutdown();

            // 3.a: Start dictationRecognizer
            dictationRecognizer.Start();

            // 3.a Uncomment this line
            dictationDisplay.text = "Dictation is starting. It may take time to display your text the first time, but begin speaking now...";

            // Set the flag that we've started recording.
            hasRecordingStarted = true;

            // Start recording from the microphone for 10 seconds.
            return Microphone.Start(deviceName, false, messageLength, samplingRate);
        }

        /// <summary>
        /// Ends the recording session.
        /// </summary>
        public void StopRecording()
        {
            // 3.a: Check if dictationRecognizer.Status is Running and stop it if so
            if (dictationRecognizer.Status == SpeechSystemStatus.Running)
            {
                dictationRecognizer.Stop();
            }

            Microphone.End(deviceName);
        }

        /// <summary>
        /// This event is fired while the user is talking. As the recognizer listens, it provides text of what it's heard so far.
        /// </summary>
        /// <param name="text">The currently hypothesized recognition.</param>
        private void DictationRecognizer_DictationHypothesis(string text)
        {
            // 3.a: Set DictationDisplay text to be textSoFar and new hypothesized text
            // We don't want to append to textSoFar yet, because the hypothesis may have changed on the next event
            dictationDisplay.text = textSoFar.ToString() + " " + text + "...";
        }

        /// <summary>
        /// This event is fired after the user pauses, typically at the end of a sentence. The full recognized string is returned here.
        /// </summary>
        /// <param name="text">The text that was heard by the recognizer.</param>
        /// <param name="confidence">A representation of how confident (rejected, low, medium, high) the recognizer is of this recognition.</param>
        private void DictationRecognizer_DictationResult(string text, ConfidenceLevel confidence)
        {
            // 3.a: Append textSoFar with latest text
            textSoFar.Append(text + ". ");

            // 3.a: Set DictationDisplay text to be textSoFar
            dictationDisplay.text = textSoFar.ToString();
        }

        /// <summary>
        /// This event is fired when the recognizer stops, whether from Stop() being called, a timeout occurring, or some other error.
        /// Typically, this will simply return "Complete". In this case, we check to see if the recognizer timed out.
        /// </summary>
        /// <param name="cause">An enumerated reason for the session completing.</param>
        private void DictationRecognizer_DictationComplete(DictationCompletionCause cause)
        {
            // If Timeout occurs, the user has been silent for too long.
            // With dictation, the default timeout after a recognition is 20 seconds.
            // The default timeout with initial silence is 5 seconds.
            if (cause == DictationCompletionCause.TimeoutExceeded)
            {
                Microphone.End(deviceName);

                dictationDisplay.text = "Dictation has timed out. Please press the record button again.";
                SendMessage("ResetAfterTimeout");
            }
        }

        /// <summary>
        /// This event is fired when an error occurs.
        /// </summary>
        /// <param name="error">The string representation of the error reason.</param>
        /// <param name="hresult">The int representation of the hresult.</param>
        private void DictationRecognizer_DictationError(string error, int hresult)
        {
            // 3.a: Set DictationDisplay text to be the error string
            dictationDisplay.text = error + "\nHRESULT: " + hresult;
        }

        /// <summary>
        /// The dictation recognizer may not turn off immediately, so this call blocks on
        /// the recognizer reporting that it has actually stopped.
        /// </summary>
        public IEnumerator WaitForDictationToStop()
        {
            while (dictationRecognizer != null && dictationRecognizer.Status == SpeechSystemStatus.Running)
            {
                yield return null;
            }
        }
    }
}
```

### <a name="build-and-deploy"></a><span data-ttu-id="3d522-312">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="3d522-312">Build and Deploy</span></span>

* <span data-ttu-id="3d522-313">Régénérez dans Visual Studio et déployez sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="3d522-313">Rebuild in Visual Studio and deploy to your device.</span></span>
* <span data-ttu-id="3d522-314">Faites disparaître la zone d’ajustement avec un mouvement d’appui sur l’air.</span><span class="sxs-lookup"><span data-stu-id="3d522-314">Dismiss the fit box with an air-tap gesture.</span></span>
* <span data-ttu-id="3d522-315">Pointez le regard du astronautes et dites *« ouvrir Communicator »* .</span><span class="sxs-lookup"><span data-stu-id="3d522-315">Gaze at the astronaut's watch and say *"Open Communicator"*.</span></span>
* <span data-ttu-id="3d522-316">Sélectionnez le bouton d' **enregistrement** (microphone) pour enregistrer votre message.</span><span class="sxs-lookup"><span data-stu-id="3d522-316">Select the **Record** button (microphone) to record your message.</span></span>
* <span data-ttu-id="3d522-317">Commencez à parler.</span><span class="sxs-lookup"><span data-stu-id="3d522-317">Start speaking.</span></span> <span data-ttu-id="3d522-318">Le module de **reconnaissance de dictée** interprètera votre discours et affichera le texte de l’hypothèse dans le Communicator.</span><span class="sxs-lookup"><span data-stu-id="3d522-318">The **Dictation Recognizer** will interpret your speech and show the hypothesized text in the communicator.</span></span>
* <span data-ttu-id="3d522-319">Essayez de dire *« Envoyer un message »* lors de l’enregistrement d’un message.</span><span class="sxs-lookup"><span data-stu-id="3d522-319">Try saying *"Send Message"* while you are recording a message.</span></span> <span data-ttu-id="3d522-320">Notez que le module de **reconnaissance de mot clé** ne répond pas, car le module de **reconnaissance de dictée** est toujours actif.</span><span class="sxs-lookup"><span data-stu-id="3d522-320">Notice that the **Keyword Recognizer** does not respond because the **Dictation Recognizer** is still active.</span></span>
* <span data-ttu-id="3d522-321">Arrêtez de parler pendant quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="3d522-321">Stop speaking for a few seconds.</span></span> <span data-ttu-id="3d522-322">Regardez que le module de reconnaissance de dictée termine son hypothèse et montre le résultat final.</span><span class="sxs-lookup"><span data-stu-id="3d522-322">Watch as the Dictation Recognizer completes its hypothesis and shows the final result.</span></span>
* <span data-ttu-id="3d522-323">Commencez à parler, puis suspendez pendant 20 secondes.</span><span class="sxs-lookup"><span data-stu-id="3d522-323">Begin speaking and then pause for 20 seconds.</span></span> <span data-ttu-id="3d522-324">Le module de **reconnaissance de dictée** est alors dépassé.</span><span class="sxs-lookup"><span data-stu-id="3d522-324">This will cause the **Dictation Recognizer** to timeout.</span></span>
* <span data-ttu-id="3d522-325">Notez que le module de **reconnaissance de mot clé** est réactivé après l’expiration du délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="3d522-325">Notice that the **Keyword Recognizer** is re-enabled after the above timeout.</span></span> <span data-ttu-id="3d522-326">Communicator répond alors aux commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="3d522-326">The communicator will now respond to voice commands.</span></span>
* <span data-ttu-id="3d522-327">Dites *« Envoyer un message »* pour envoyer le message à astronautes.</span><span class="sxs-lookup"><span data-stu-id="3d522-327">Say *"Send Message"* to send the message to the astronaut.</span></span>

## <a name="chapter-4---grammar-recognizer"></a><span data-ttu-id="3d522-328">Chapitre 4-module de reconnaissance de la grammaire</span><span class="sxs-lookup"><span data-stu-id="3d522-328">Chapter 4 - Grammar Recognizer</span></span>

>[!VIDEO https://www.youtube.com/embed/J2dYJNSvv18]

### <a name="objectives"></a><span data-ttu-id="3d522-329">Objectifs</span><span class="sxs-lookup"><span data-stu-id="3d522-329">Objectives</span></span>

* <span data-ttu-id="3d522-330">Utilisez le module de reconnaissance grammatical pour reconnaître la parole de l’utilisateur en fonction d’un SRGS, ou de la spécification de la grammaire de la reconnaissance vocale, fichier.</span><span class="sxs-lookup"><span data-stu-id="3d522-330">Use the Grammar Recognizer to recognize the user's speech according to an SRGS, or Speech Recognition Grammar Specification, file.</span></span>

>[!NOTE]
><span data-ttu-id="3d522-331">La fonctionnalité **microphone** doit être déclarée pour qu’une application soit enregistrée à partir du microphone.</span><span class="sxs-lookup"><span data-stu-id="3d522-331">The **Microphone** capability must be declared for an app to record from the microphone.</span></span> <span data-ttu-id="3d522-332">Cela est fait pour vous déjà dans une entrée de m. 212, mais gardez cela à l’esprit pour vos propres projets.</span><span class="sxs-lookup"><span data-stu-id="3d522-332">This is done for you already in MR Input 212, but keep this in mind for your own projects.</span></span>
>
>1. <span data-ttu-id="3d522-333">Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à « modifier les paramètres du projet > > Player ».</span><span class="sxs-lookup"><span data-stu-id="3d522-333">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player"</span></span>
>2. <span data-ttu-id="3d522-334">Cliquez sur l’onglet « plateforme Windows universelle »</span><span class="sxs-lookup"><span data-stu-id="3d522-334">Click on the "Universal Windows Platform" tab</span></span>
>3. <span data-ttu-id="3d522-335">Dans la section « fonctionnalités de > des paramètres de publication », vérifiez la fonctionnalité du **microphone** .</span><span class="sxs-lookup"><span data-stu-id="3d522-335">In the "Publishing Settings > Capabilities" section, check the **Microphone** capability</span></span>

### <a name="instructions"></a><span data-ttu-id="3d522-336">Instructions</span><span class="sxs-lookup"><span data-stu-id="3d522-336">Instructions</span></span>

1. <span data-ttu-id="3d522-337">Dans le volet **hiérarchie** , recherchez **Jetpack_Center** et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="3d522-337">In the **Hierarchy** panel, search for **Jetpack_Center** and select it.</span></span>
2. <span data-ttu-id="3d522-338">Recherchez le script d' **action accompagnent** dans le panneau **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="3d522-338">Look for the **Tagalong Action** script in the **Inspector** panel.</span></span>
3. <span data-ttu-id="3d522-339">Cliquez sur le petit cercle situé à droite de l' **objet à baliser** sur le champ.</span><span class="sxs-lookup"><span data-stu-id="3d522-339">Click the little circle to the right of the **Object To Tag Along** field.</span></span>
4. <span data-ttu-id="3d522-340">Dans la fenêtre qui s’affiche, recherchez **SRGSToolbox** et sélectionnez-le dans la liste.</span><span class="sxs-lookup"><span data-stu-id="3d522-340">In the window that pops up, search for **SRGSToolbox** and select it from the list.</span></span>
5. <span data-ttu-id="3d522-341">Jetez un coup d’œil au fichier **SRGSColor. xml** dans le dossier **StreamingAssets** .</span><span class="sxs-lookup"><span data-stu-id="3d522-341">Take a look at the **SRGSColor.xml** file in the **StreamingAssets** folder.</span></span>
    1. <span data-ttu-id="3d522-342">Les spécifications de conception SRGS se trouvent sur le site Web du W3C [ici](https://www.w3.org/TR/speech-grammar/).</span><span class="sxs-lookup"><span data-stu-id="3d522-342">The SRGS design spec can be found on the W3C website [here](https://www.w3.org/TR/speech-grammar/).</span></span>

<span data-ttu-id="3d522-343">Dans notre fichier SRGS, nous avons trois types de règles :</span><span class="sxs-lookup"><span data-stu-id="3d522-343">In our SRGS file, we have three types of rules:</span></span>

* <span data-ttu-id="3d522-344">Une règle qui vous permet d’indiquer une couleur dans une liste de douze couleurs.</span><span class="sxs-lookup"><span data-stu-id="3d522-344">A rule which lets you say one color from a list of twelve colors.</span></span>
* <span data-ttu-id="3d522-345">Trois règles qui écoutent une combinaison de la règle de couleur et l’une des trois formes.</span><span class="sxs-lookup"><span data-stu-id="3d522-345">Three rules which listen for a combination of the color rule and one of the three shapes.</span></span>
* <span data-ttu-id="3d522-346">La règle racine, colorChooser, qui écoute toutes les combinaisons des trois règles de « couleur et de forme ».</span><span class="sxs-lookup"><span data-stu-id="3d522-346">The root rule, colorChooser, which listens for any combination of the three "color + shape" rules.</span></span> <span data-ttu-id="3d522-347">Les formes peuvent être déclarées dans n’importe quel ordre et dans n’importe quel montant, d’une seule à l’autre.</span><span class="sxs-lookup"><span data-stu-id="3d522-347">The shapes can be said in any order and in any amount from just one to all three.</span></span> <span data-ttu-id="3d522-348">Il s’agit de la seule règle écoutée pour, telle qu’elle est spécifiée en tant que règle racine en haut du fichier dans la balise de&gt; de grammaire initiale &lt;.</span><span class="sxs-lookup"><span data-stu-id="3d522-348">This is the only rule that is listened for, as it's specified as the root rule at the top of the file in the initial &lt;grammar&gt; tag.</span></span>

### <a name="build-and-deploy"></a><span data-ttu-id="3d522-349">Génération et déploiement</span><span class="sxs-lookup"><span data-stu-id="3d522-349">Build and Deploy</span></span>

* <span data-ttu-id="3d522-350">Régénérez l’application dans Unity, puis générez et déployez à partir de Visual Studio pour expérimenter l’application sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3d522-350">Rebuild the application in Unity, then build and deploy from Visual Studio to experience the app on HoloLens.</span></span>
* <span data-ttu-id="3d522-351">Faites disparaître la zone d’ajustement avec un mouvement d’appui sur l’air.</span><span class="sxs-lookup"><span data-stu-id="3d522-351">Dismiss the fit box with an air-tap gesture.</span></span>
* <span data-ttu-id="3d522-352">Pointez le regard du astronautes et effectuez un mouvement d’appui sur l’air.</span><span class="sxs-lookup"><span data-stu-id="3d522-352">Gaze at the astronaut's jetpack and perform an air-tap gesture.</span></span>
* <span data-ttu-id="3d522-353">Commencez à parler.</span><span class="sxs-lookup"><span data-stu-id="3d522-353">Start speaking.</span></span> <span data-ttu-id="3d522-354">Le module de reconnaissance de la **grammaire** interprète votre discours et modifie les couleurs des formes en fonction de la reconnaissance.</span><span class="sxs-lookup"><span data-stu-id="3d522-354">The **Grammar Recognizer** will interpret your speech and change the colors of the shapes based on the recognition.</span></span> <span data-ttu-id="3d522-355">Un exemple de commande est « cercle bleu, carré jaune ».</span><span class="sxs-lookup"><span data-stu-id="3d522-355">An example command is "blue circle, yellow square".</span></span>
* <span data-ttu-id="3d522-356">Effectuez un autre mouvement d’appui sur l’air pour faire disparaître la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="3d522-356">Perform another air-tap gesture to dismiss the toolbox.</span></span>

## <a name="the-end"></a><span data-ttu-id="3d522-357">La fin</span><span class="sxs-lookup"><span data-stu-id="3d522-357">The End</span></span>

<span data-ttu-id="3d522-358">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="3d522-358">Congratulations!</span></span> <span data-ttu-id="3d522-359">Vous avez maintenant terminé l' **entrée 212 : Voice**.</span><span class="sxs-lookup"><span data-stu-id="3d522-359">You have now completed **MR Input 212: Voice**.</span></span>

* <span data-ttu-id="3d522-360">Vous connaissez les dos et les absences de commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="3d522-360">You know the Dos and Don'ts of voice commands.</span></span>
* <span data-ttu-id="3d522-361">Vous avez vu comment les info-bulles étaient utilisées pour que les utilisateurs soient informés des commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="3d522-361">You saw how tooltips were employed to make users aware of voice commands.</span></span>
* <span data-ttu-id="3d522-362">Vous avez vu plusieurs types de commentaires utilisés pour accuser réception de la voix de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3d522-362">You saw several types of feedback used to acknowledge that the user's voice was heard.</span></span>
* <span data-ttu-id="3d522-363">Vous savez comment basculer entre le module de reconnaissance de mot clé et le module de reconnaissance de dictée, et comment ces deux fonctionnalités comprennent et interprètent votre voix.</span><span class="sxs-lookup"><span data-stu-id="3d522-363">You know how to switch between the Keyword Recognizer and the Dictation Recognizer, and how these two features understand and interpret your voice.</span></span>
* <span data-ttu-id="3d522-364">Vous avez appris à utiliser un fichier SRGS et le module de reconnaissance grammaticale pour la reconnaissance vocale dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3d522-364">You learned how to use an SRGS file and the Grammar Recognizer for speech recognition in your application.</span></span>
