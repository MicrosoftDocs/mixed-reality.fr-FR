---
title: Entrée M. 212 - Voice
description: Suivez cette procédure pas à pas codage à l’aide de Unity, Visual Studio et HoloLens pour connaître les détails des concepts de voix.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, academy, tutorial, voice
ms.openlocfilehash: 7e792bf40c47d4e1d57898fbe75ad050a030b7e3
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593795"
---
>[!NOTE]
><span data-ttu-id="8c304-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="8c304-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="8c304-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="8c304-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="8c304-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="8c304-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="8c304-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="8c304-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="8c304-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="8c304-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="8c304-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="8c304-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-input-212-voice"></a><span data-ttu-id="8c304-110">Entrée M. 212 : Voix</span><span class="sxs-lookup"><span data-stu-id="8c304-110">MR Input 212: Voice</span></span>

<span data-ttu-id="8c304-111">[Entrée voix](voice-input.md) nous donne une autre façon d’interagir avec notre hologrammes.</span><span class="sxs-lookup"><span data-stu-id="8c304-111">[Voice input](voice-input.md) gives us another way to interact with our holograms.</span></span> <span data-ttu-id="8c304-112">Les commandes vocales fonctionnent de manière très naturelle et facile.</span><span class="sxs-lookup"><span data-stu-id="8c304-112">Voice commands work in a very natural and easy way.</span></span> <span data-ttu-id="8c304-113">Concevez vos commandes vocales afin qu’elles soient :</span><span class="sxs-lookup"><span data-stu-id="8c304-113">Design your voice commands so that they are:</span></span>

* <span data-ttu-id="8c304-114">Natural</span><span class="sxs-lookup"><span data-stu-id="8c304-114">Natural</span></span>
* <span data-ttu-id="8c304-115">Facile à retenir</span><span class="sxs-lookup"><span data-stu-id="8c304-115">Easy to remember</span></span>
* <span data-ttu-id="8c304-116">Contexte approprié</span><span class="sxs-lookup"><span data-stu-id="8c304-116">Context appropriate</span></span>
* <span data-ttu-id="8c304-117">Suffisamment distinctes à partir d’autres options dans le même contexte</span><span class="sxs-lookup"><span data-stu-id="8c304-117">Sufficiently distinct from other options within the same context</span></span>

>[!VIDEO https://www.youtube.com/embed/BYpYsVFYjdw]

<span data-ttu-id="8c304-118">Dans [101 des principes fondamentaux de M.](holograms-101.md), nous avons utilisé le KeywordRecognizer pour générer les deux commandes vocales simples.</span><span class="sxs-lookup"><span data-stu-id="8c304-118">In [MR Basics 101](holograms-101.md), we used the KeywordRecognizer to build two simple voice commands.</span></span> <span data-ttu-id="8c304-119">Dans 212 d’entrée M., nous allons Approfondissez vos connaissances et découvrez comment :</span><span class="sxs-lookup"><span data-stu-id="8c304-119">In MR Input 212, we'll dive deeper and learn how to:</span></span>

* <span data-ttu-id="8c304-120">Concevoir des commandes vocales qui sont optimisés pour le moteur de reconnaissance vocale HoloLens.</span><span class="sxs-lookup"><span data-stu-id="8c304-120">Design voice commands that are optimized for the HoloLens speech engine.</span></span>
* <span data-ttu-id="8c304-121">Informer l’utilisateur du voix des commandes sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="8c304-121">Make the user aware of what voice commands are available.</span></span>
* <span data-ttu-id="8c304-122">Reconnaissez que nous avons entendu commande vocale de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c304-122">Acknowledge that we've heard the user's voice command.</span></span>
* <span data-ttu-id="8c304-123">Comprendre ce qui est l’utilisateur indiquant que, à l’aide d’un module de reconnaissance de dictée.</span><span class="sxs-lookup"><span data-stu-id="8c304-123">Understand what the user is saying, using a Dictation Recognizer.</span></span>
* <span data-ttu-id="8c304-124">Utiliser une grammaire de reconnaissance pour écouter les commandes basées sur un fichier SRGS ou spécification de grammaire de reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="8c304-124">Use a Grammar Recognizer to listen for commands based on an SRGS, or Speech Recognition Grammar Specification, file.</span></span>

<span data-ttu-id="8c304-125">Dans ce cours, nous y reviendrons Explorateur de modèles, nous avons créé dans [210 d’entrée M.](holograms-210.md) et [211 d’entrée M.](holograms-211.md).</span><span class="sxs-lookup"><span data-stu-id="8c304-125">In this course, we'll revisit Model Explorer, which we built in [MR Input 210](holograms-210.md) and [MR Input 211](holograms-211.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="8c304-126">Les vidéos incorporées dans chacun des chapitres ci-dessous ont été enregistrés à l’aide d’une version antérieure de Unity et le Kit de ressources de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="8c304-126">The videos embedded in each of the chapters below were recorded using an older version of Unity and the Mixed Reality Toolkit.</span></span> <span data-ttu-id="8c304-127">Tandis que les instructions pas à pas sont précises et actuelles, vous pouvez voir des scripts et des éléments visuels dans les vidéos correspondantes qui sont obsolètes.</span><span class="sxs-lookup"><span data-stu-id="8c304-127">While the step-by-step instructions are accurate and current, you may see scripts and visuals in the corresponding videos that are out-of-date.</span></span> <span data-ttu-id="8c304-128">Les vidéos restent inclus éternellement et car couvert les concepts s’appliquent toujours.</span><span class="sxs-lookup"><span data-stu-id="8c304-128">The videos remain included for posterity and because the concepts covered still apply.</span></span>


## <a name="device-support"></a><span data-ttu-id="8c304-129">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="8c304-129">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="8c304-130">Cours</span><span class="sxs-lookup"><span data-stu-id="8c304-130">Course</span></span></th><th style="width:150px"> <span data-ttu-id="8c304-131"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c304-131"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c304-132"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c304-132"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="8c304-133">Entrée M. 212 : Voix</span><span class="sxs-lookup"><span data-stu-id="8c304-133">MR Input 212: Voice</span></span></td><td style="text-align: center;"> <span data-ttu-id="8c304-134">✔️</span><span class="sxs-lookup"><span data-stu-id="8c304-134">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="8c304-135">✔️</span><span class="sxs-lookup"><span data-stu-id="8c304-135">✔️</span></span></td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="8c304-136">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8c304-136">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8c304-137">Prérequis</span><span class="sxs-lookup"><span data-stu-id="8c304-137">Prerequisites</span></span>

* <span data-ttu-id="8c304-138">Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="8c304-138">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="8c304-139">Base C# possibilité de programmation.</span><span class="sxs-lookup"><span data-stu-id="8c304-139">Some basic C# programming ability.</span></span>
* <span data-ttu-id="8c304-140">Vous devez avoir terminé [101 de principes de base MR](holograms-101.md).</span><span class="sxs-lookup"><span data-stu-id="8c304-140">You should have completed [MR Basics 101](holograms-101.md).</span></span>
* <span data-ttu-id="8c304-141">Vous devez avoir terminé [210 d’entrée M.](holograms-210.md).</span><span class="sxs-lookup"><span data-stu-id="8c304-141">You should have completed [MR Input 210](holograms-210.md).</span></span>
* <span data-ttu-id="8c304-142">Vous devez avoir terminé [211 d’entrée M.](holograms-211.md).</span><span class="sxs-lookup"><span data-stu-id="8c304-142">You should have completed [MR Input 211](holograms-211.md).</span></span>
* <span data-ttu-id="8c304-143">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="8c304-143">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="8c304-144">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="8c304-144">Project files</span></span>

* <span data-ttu-id="8c304-145">Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-212-Voice.zip) requise par le projet.</span><span class="sxs-lookup"><span data-stu-id="8c304-145">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-212-Voice.zip) required by the project.</span></span> <span data-ttu-id="8c304-146">Nécessite Unity 2017.2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8c304-146">Requires Unity 2017.2 or later.</span></span>
* <span data-ttu-id="8c304-147">Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="8c304-147">Un-archive the files to your desktop or other easy to reach location.</span></span>

>[!NOTE]
><span data-ttu-id="8c304-148">Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-212-Voice).</span><span class="sxs-lookup"><span data-stu-id="8c304-148">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-212-Voice).</span></span>

### <a name="errata-and-notes"></a><span data-ttu-id="8c304-149">Errata et remarques</span><span class="sxs-lookup"><span data-stu-id="8c304-149">Errata and Notes</span></span>

* <span data-ttu-id="8c304-150">« Activer uniquement mon Code » doit être désactivé (*unchecked*) dans Visual Studio sous Outils -> Options -> débogage afin d’atteindre des points d’arrêt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="8c304-150">"Enable Just My Code" needs to be disabled (*unchecked*) in Visual Studio under Tools->Options->Debugging in order to hit breakpoints in your code.</span></span>

## <a name="unity-setup"></a><span data-ttu-id="8c304-151">Programme d’installation Unity</span><span class="sxs-lookup"><span data-stu-id="8c304-151">Unity Setup</span></span>

### <a name="instructions"></a><span data-ttu-id="8c304-152">Instructions</span><span class="sxs-lookup"><span data-stu-id="8c304-152">Instructions</span></span>

1. <span data-ttu-id="8c304-153">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="8c304-153">Start Unity.</span></span>
2. <span data-ttu-id="8c304-154">Sélectionnez **Open**.</span><span class="sxs-lookup"><span data-stu-id="8c304-154">Select **Open**.</span></span>
3. <span data-ttu-id="8c304-155">Accédez à la **HolographicAcademy hologrammes 212 vocaux** dossier vous précédemment non archivés.</span><span class="sxs-lookup"><span data-stu-id="8c304-155">Navigate to the **HolographicAcademy-Holograms-212-Voice** folder you previously un-archived.</span></span>
4. <span data-ttu-id="8c304-156">Recherchez et sélectionnez le **démarrage**/**l’Explorateur de modèles** dossier.</span><span class="sxs-lookup"><span data-stu-id="8c304-156">Find and select the **Starting**/**Model Explorer** folder.</span></span>
5. <span data-ttu-id="8c304-157">Cliquez sur le **sélectionner le dossier** bouton.</span><span class="sxs-lookup"><span data-stu-id="8c304-157">Click the **Select Folder** button.</span></span>
6. <span data-ttu-id="8c304-158">Dans le **projet** volet, développez le **scènes** dossier.</span><span class="sxs-lookup"><span data-stu-id="8c304-158">In the **Project** panel, expand the **Scenes** folder.</span></span>
7. <span data-ttu-id="8c304-159">Double-cliquez sur **ModelExplorer** scène à le charger dans Unity.</span><span class="sxs-lookup"><span data-stu-id="8c304-159">Double-click **ModelExplorer** scene to load it in Unity.</span></span>

### <a name="building"></a><span data-ttu-id="8c304-160">Génération</span><span class="sxs-lookup"><span data-stu-id="8c304-160">Building</span></span>

1. <span data-ttu-id="8c304-161">Dans Unity, sélectionnez **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="8c304-161">In Unity, select **File > Build Settings**.</span></span>
2. <span data-ttu-id="8c304-162">Si **arrière-plan/ModelExplorer** n’est pas répertorié dans **scènes dans Build**, cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="8c304-162">If **Scenes/ModelExplorer** is not listed in **Scenes In Build**, click **Add Open Scenes** to add the scene.</span></span>
3. <span data-ttu-id="8c304-163">Si vous développez en particulier pour HoloLens, définissez **appareil cible** à **HoloLens**.</span><span class="sxs-lookup"><span data-stu-id="8c304-163">If you're specifically developing for HoloLens, set **Target device** to **HoloLens**.</span></span> <span data-ttu-id="8c304-164">Dans le cas contraire, laissez-le sur **n’importe quel appareil**.</span><span class="sxs-lookup"><span data-stu-id="8c304-164">Otherwise, leave it on **Any device**.</span></span>
4. <span data-ttu-id="8c304-165">Vérifiez **Type Build** a la valeur **D3D** et **SDK** a la valeur **dernière installé** (qui doit être SDK 16299 ou une version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="8c304-165">Ensure **Build Type** is set to **D3D** and **SDK** is set to **Latest installed** (which should be SDK 16299 or newer).</span></span>
5. <span data-ttu-id="8c304-166">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="8c304-166">Click **Build**.</span></span>
6. <span data-ttu-id="8c304-167">Créer un **nouveau dossier** nommé « Application ».</span><span class="sxs-lookup"><span data-stu-id="8c304-167">Create a **New Folder** named "App".</span></span>
7. <span data-ttu-id="8c304-168">Clic le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="8c304-168">Single click the **App** folder.</span></span>
8. <span data-ttu-id="8c304-169">Appuyez sur **sélectionner le dossier** et Unity commence à générer le projet pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c304-169">Press **Select Folder** and Unity will start building the project for Visual Studio.</span></span>

<span data-ttu-id="8c304-170">Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8c304-170">When Unity is done, a File Explorer window will appear.</span></span>

1. <span data-ttu-id="8c304-171">Ouvrez le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="8c304-171">Open the **App** folder.</span></span>
2. <span data-ttu-id="8c304-172">Ouvrez le **ModelExplorer Visual Studio Solution**.</span><span class="sxs-lookup"><span data-stu-id="8c304-172">Open the **ModelExplorer Visual Studio Solution**.</span></span>

<span data-ttu-id="8c304-173">Si le déploiement sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="8c304-173">If deploying to HoloLens:</span></span>

1. <span data-ttu-id="8c304-174">À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x86**.</span><span class="sxs-lookup"><span data-stu-id="8c304-174">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x86**.</span></span>
2. <span data-ttu-id="8c304-175">Cliquez sur la flèche déroulante en regard du bouton de l’ordinateur Local, puis sélectionnez **Machine distante**.</span><span class="sxs-lookup"><span data-stu-id="8c304-175">Click on the drop down arrow next to the Local Machine button, and select **Remote Machine**.</span></span>
3. <span data-ttu-id="8c304-176">Entrez **votre adresse IP du périphérique HoloLens** et définir le Mode d’authentification **universel (protocole non chiffré)**.</span><span class="sxs-lookup"><span data-stu-id="8c304-176">Enter **your HoloLens device IP address** and set Authentication Mode to **Universal (Unencrypted Protocol)**.</span></span> <span data-ttu-id="8c304-177">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="8c304-177">Click **Select**.</span></span> <span data-ttu-id="8c304-178">Si vous ne connaissez pas votre adresse IP du périphérique, recherchez dans **Paramètres > réseau & Internet > Options avancées**.</span><span class="sxs-lookup"><span data-stu-id="8c304-178">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options**.</span></span>
4. <span data-ttu-id="8c304-179">Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="8c304-179">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="8c304-180">S’il s’agit de la première fois le déploiement sur votre périphérique, vous devrez [Couplez-le Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span><span class="sxs-lookup"><span data-stu-id="8c304-180">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span></span>
5. <span data-ttu-id="8c304-181">Lorsque l’application a été déployée, faire disparaître le **Fitbox** avec un **sélectionnez mouvement**.</span><span class="sxs-lookup"><span data-stu-id="8c304-181">When the app has deployed, dismiss the **Fitbox** with a **select gesture**.</span></span>

<span data-ttu-id="8c304-182">Si le déploiement sur un casque immersif :</span><span class="sxs-lookup"><span data-stu-id="8c304-182">If deploying to an immersive headset:</span></span>

1. <span data-ttu-id="8c304-183">À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x64**.</span><span class="sxs-lookup"><span data-stu-id="8c304-183">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x64**.</span></span>
2. <span data-ttu-id="8c304-184">Assurez-vous que la cible de déploiement est définie sur **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="8c304-184">Make sure the deployment target is set to **Local Machine**.</span></span>
3. <span data-ttu-id="8c304-185">Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="8c304-185">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
4. <span data-ttu-id="8c304-186">Lorsque l’application a été déployée, faire disparaître le **Fitbox** en extrayant le déclencheur sur un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="8c304-186">When the app has deployed, dismiss the **Fitbox** by pulling the trigger on a motion controller.</span></span>

>[!NOTE]
><span data-ttu-id="8c304-187">Vous remarquerez peut-être des erreurs rouge dans le panneau erreurs de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c304-187">You might notice some red errors in the Visual Studio Errors panel.</span></span> <span data-ttu-id="8c304-188">Il est possible de les ignorer.</span><span class="sxs-lookup"><span data-stu-id="8c304-188">It is safe to ignore them.</span></span> <span data-ttu-id="8c304-189">Basculer vers le volet de sortie pour afficher les réelle progression de la build.</span><span class="sxs-lookup"><span data-stu-id="8c304-189">Switch to the Output panel to view actual build progress.</span></span> <span data-ttu-id="8c304-190">Erreurs dans le volet de sortie vous obligera à effectuer un correctif (la plus souvent qu’ils sont provoquées par une erreur dans un script).</span><span class="sxs-lookup"><span data-stu-id="8c304-190">Errors in the Output panel will require you to make a fix (most often they are caused by a mistake in a script).</span></span>

## <a name="chapter-1---awareness"></a><span data-ttu-id="8c304-191">Chapitre 1 - sensibilisation</span><span class="sxs-lookup"><span data-stu-id="8c304-191">Chapter 1 - Awareness</span></span>

>[!VIDEO https://www.youtube.com/embed/fDwijJWuEc0]

### <a name="objectives"></a><span data-ttu-id="8c304-192">Objectifs</span><span class="sxs-lookup"><span data-stu-id="8c304-192">Objectives</span></span>

* <span data-ttu-id="8c304-193">Découvrez le **choses à faire et** de conception d’une commande vocale.</span><span class="sxs-lookup"><span data-stu-id="8c304-193">Learn the **Dos and Don'ts** of voice command design.</span></span>
* <span data-ttu-id="8c304-194">Utilisez **KeywordRecognizer** pour ajouter des regards en fonction des commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="8c304-194">Use **KeywordRecognizer** to add gaze based voice commands.</span></span>
* <span data-ttu-id="8c304-195">Informer les utilisateurs des commandes vocales à l’aide du curseur **commentaires**.</span><span class="sxs-lookup"><span data-stu-id="8c304-195">Make users aware of voice commands using cursor **feedback**.</span></span>

### <a name="voice-command-design"></a><span data-ttu-id="8c304-196">Conception d’une commande vocale</span><span class="sxs-lookup"><span data-stu-id="8c304-196">Voice Command Design</span></span>

<span data-ttu-id="8c304-197">Dans ce chapitre, vous allez découvrir les commandes vocales de conception.</span><span class="sxs-lookup"><span data-stu-id="8c304-197">In this chapter, you'll learn about designing voice commands.</span></span> <span data-ttu-id="8c304-198">Lorsque vous créez des commandes vocales :</span><span class="sxs-lookup"><span data-stu-id="8c304-198">When creating voice commands:</span></span>

#### <a name="do"></a><span data-ttu-id="8c304-199">DO</span><span class="sxs-lookup"><span data-stu-id="8c304-199">DO</span></span>

* <span data-ttu-id="8c304-200">Créer des commandes concis.</span><span class="sxs-lookup"><span data-stu-id="8c304-200">Create concise commands.</span></span> <span data-ttu-id="8c304-201">Vous ne souhaitez pas utiliser *« Lire la vidéo actuellement sélectionnée »*, car cette commande n’est pas concise et serait oubliée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c304-201">You don't want to use *"Play the currently selected video"*, because that command is not concise and would easily be forgotten by the user.</span></span> <span data-ttu-id="8c304-202">Au lieu de cela, vous devez utiliser : *« Lire la vidéo »*, car il est concis et a plusieurs syllabes.</span><span class="sxs-lookup"><span data-stu-id="8c304-202">Instead, you should use: *"Play Video"*, because it is concise and has multiple syllables.</span></span>
* <span data-ttu-id="8c304-203">Utiliser un vocabulaire simple.</span><span class="sxs-lookup"><span data-stu-id="8c304-203">Use a simple vocabulary.</span></span> <span data-ttu-id="8c304-204">Toujours essayer d’utiliser des mots et des expressions qui sont faciles à l’utilisateur de découvrir et n’oubliez pas courants.</span><span class="sxs-lookup"><span data-stu-id="8c304-204">Always try to use common words and phrases that are easy for the user to discover and remember.</span></span> <span data-ttu-id="8c304-205">Par exemple, si votre application avait une remarque de l’objet qui peut être affiché ou masqué à partir de la vue, vous ne serez pas utiliser la commande *« Afficher le panneau »*, car le panneau « des » sont un terme rarement utilisé.</span><span class="sxs-lookup"><span data-stu-id="8c304-205">For example, if your application had a note object that could be displayed or hidden from view, you would not use the command *"Show Placard"*, because "placard" is a rarely used term.</span></span> <span data-ttu-id="8c304-206">Au lieu de cela, vous devez utiliser la commande : *« Afficher la Remarque »*, pour afficher la note dans votre application.</span><span class="sxs-lookup"><span data-stu-id="8c304-206">Instead, you would use the command: *"Show Note"*, to reveal the note in your application.</span></span>
* <span data-ttu-id="8c304-207">Soyez cohérent.</span><span class="sxs-lookup"><span data-stu-id="8c304-207">Be consistent.</span></span> <span data-ttu-id="8c304-208">Les commandes vocales doivent être cohérente dans votre application.</span><span class="sxs-lookup"><span data-stu-id="8c304-208">Voice commands should be kept consistent across your application.</span></span> <span data-ttu-id="8c304-209">Imaginez que vous avez deux scènes dans votre application et les deux scènes contiennent un bouton pour fermer l’application.</span><span class="sxs-lookup"><span data-stu-id="8c304-209">Imagine that you have two scenes in your application and both scenes contain a button for closing the application.</span></span> <span data-ttu-id="8c304-210">Si la première scène utilisé la commande *« Exit »* pour déclencher le bouton, mais la deuxième scène utilisé la commande *« Fermer l’application »*, puis l’utilisateur va peu trouble.</span><span class="sxs-lookup"><span data-stu-id="8c304-210">If the first scene used the command *"Exit"* to trigger the button, but the second scene used the command *"Close App"*, then the user is going to get very confused.</span></span> <span data-ttu-id="8c304-211">Si les mêmes fonctionnalités sont conservées dans plusieurs scènes, la même commande voix doit être utilisée pour déclencher l’il.</span><span class="sxs-lookup"><span data-stu-id="8c304-211">If the same functionality persists across multiple scenes, then the same voice command should be used to trigger it.</span></span>

#### <a name="dont"></a><span data-ttu-id="8c304-212">NE PAS</span><span class="sxs-lookup"><span data-stu-id="8c304-212">DON'T</span></span>

* <span data-ttu-id="8c304-213">Utilisez les commandes SYLLABE unique.</span><span class="sxs-lookup"><span data-stu-id="8c304-213">Use single syllable commands.</span></span> <span data-ttu-id="8c304-214">Par exemple, si vous avez créé une commande vocale pour lire une vidéo, vous évitez d’utiliser la commande simple *« Lecture »*, car elle est uniquement un SYLLABE unique et peut facilement être omis par le système.</span><span class="sxs-lookup"><span data-stu-id="8c304-214">As an example, if you were creating a voice command to play a video, you should avoid using the simple command *"Play"*, as it is only a single syllable and could easily be missed by the system.</span></span> <span data-ttu-id="8c304-215">Au lieu de cela, vous devez utiliser : *« Lire la vidéo »*, car il est concis et a plusieurs syllabes.</span><span class="sxs-lookup"><span data-stu-id="8c304-215">Instead, you should use: *"Play Video"*, because it is concise and has multiple syllables.</span></span>
* <span data-ttu-id="8c304-216">Utilisez les commandes du système.</span><span class="sxs-lookup"><span data-stu-id="8c304-216">Use system commands.</span></span> <span data-ttu-id="8c304-217">Le *« Select »* commande est réservée par le système à déclencher un événement de clic pour l’objet ayant actuellement le focus.</span><span class="sxs-lookup"><span data-stu-id="8c304-217">The *"Select"* command is reserved by the system to trigger a Tap event for the currently focused object.</span></span> <span data-ttu-id="8c304-218">Ne réutilisez pas le *« Select »* commande dans un mot clé ou une expression, comme il peut ne pas fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="8c304-218">Do not re-use the *"Select"* command in a keyword or phrase, as it might not work as you expect.</span></span> <span data-ttu-id="8c304-219">Par exemple, si la commande de la voix pour la sélection d’un cube dans votre application a été *« Sélectionnez cube »*, mais l’utilisateur a été de consulter une sphère lorsqu’ils prononcés la commande, puis la sphère est sélectionnée à la place.</span><span class="sxs-lookup"><span data-stu-id="8c304-219">For example, if the voice command for selecting a cube in your application was *"Select cube"*, but the user was looking at a sphere when they uttered the command, then the sphere would be selected instead.</span></span> <span data-ttu-id="8c304-220">De même, la barre de commandes application est voix activée.</span><span class="sxs-lookup"><span data-stu-id="8c304-220">Similarly app bar commands are voice enabled.</span></span> <span data-ttu-id="8c304-221">N’utilisez pas les commandes suivantes de la reconnaissance vocale dans votre affichage CoreWindow :</span><span class="sxs-lookup"><span data-stu-id="8c304-221">Don't use the following speech commands in your CoreWindow View:</span></span>
    1. <span data-ttu-id="8c304-222">Retour</span><span class="sxs-lookup"><span data-stu-id="8c304-222">Go Back</span></span>
    2. <span data-ttu-id="8c304-223">Outil de défilement</span><span class="sxs-lookup"><span data-stu-id="8c304-223">Scroll Tool</span></span>
    3. <span data-ttu-id="8c304-224">Outil zoom</span><span class="sxs-lookup"><span data-stu-id="8c304-224">Zoom Tool</span></span>
    4. <span data-ttu-id="8c304-225">Outil de glisser</span><span class="sxs-lookup"><span data-stu-id="8c304-225">Drag Tool</span></span>
    5. <span data-ttu-id="8c304-226">Réglage</span><span class="sxs-lookup"><span data-stu-id="8c304-226">Adjust</span></span>
    6. <span data-ttu-id="8c304-227">Supprimer</span><span class="sxs-lookup"><span data-stu-id="8c304-227">Remove</span></span>
* <span data-ttu-id="8c304-228">Utilisez les sons similaire.</span><span class="sxs-lookup"><span data-stu-id="8c304-228">Use similar sounds.</span></span> <span data-ttu-id="8c304-229">Essayez d’éviter d’utiliser les commandes vocales entraîner.</span><span class="sxs-lookup"><span data-stu-id="8c304-229">Try to avoid using voice commands that rhyme.</span></span> <span data-ttu-id="8c304-230">Si vous aviez une application d’achat qui pris en charge *« Store afficher »* et *« Afficher plus »* comme vocal de commandes, puis désactivez l’une des commandes alors que l’autre était en cours d’utilisation souhaité.</span><span class="sxs-lookup"><span data-stu-id="8c304-230">If you had a shopping application which supported *"Show Store"* and *"Show More"* as voice commands, then you would want to disable one of the commands while the other was in use.</span></span> <span data-ttu-id="8c304-231">Par exemple, vous pouvez utiliser la *« Afficher Store »* bouton pour ouvrir le magasin et désactivez cette commande lors de l’affichage de la banque afin que le *« Afficher plus »* commande peut être utilisée pour la navigation.</span><span class="sxs-lookup"><span data-stu-id="8c304-231">For example, you could use the *"Show Store"* button to open the store, and then disable that command when the store was displayed so that the *"Show More"* command could be used for browsing.</span></span>

### <a name="instructions"></a><span data-ttu-id="8c304-232">Instructions</span><span class="sxs-lookup"><span data-stu-id="8c304-232">Instructions</span></span>

* <span data-ttu-id="8c304-233">Dans Unity **hiérarchie** du panneau, utilisez l’outil de recherche pour trouver la **holoComm_screen_mesh** objet.</span><span class="sxs-lookup"><span data-stu-id="8c304-233">In Unity's **Hierarchy** panel, use the search tool to find the **holoComm_screen_mesh** object.</span></span>
* <span data-ttu-id="8c304-234">Double-cliquez sur le **holoComm_screen_mesh** objet pour l’afficher dans le **scène**.</span><span class="sxs-lookup"><span data-stu-id="8c304-234">Double-click on the **holoComm_screen_mesh** object to view it in the **Scene**.</span></span> <span data-ttu-id="8c304-235">Il s’agit d’espion de l’astronaut, qui répond à nos commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="8c304-235">This is the astronaut's watch, which will respond to our voice commands.</span></span>
* <span data-ttu-id="8c304-236">Dans le **inspecteur** panneau, recherchez le **Source d’entrée vocale (Script)** composant.</span><span class="sxs-lookup"><span data-stu-id="8c304-236">In the **Inspector** panel, locate the **Speech Input Source (Script)** component.</span></span>
* <span data-ttu-id="8c304-237">Développez le **mots clés** section pour afficher les commandes vocales prises en charge : **Ouvrez Communicator**.</span><span class="sxs-lookup"><span data-stu-id="8c304-237">Expand the **Keywords** section to see the supported voice command: **Open Communicator**.</span></span>
* <span data-ttu-id="8c304-238">Cliquez sur la roue dentée à droite, puis sélectionnez **modifier le Script**.</span><span class="sxs-lookup"><span data-stu-id="8c304-238">Click the cog to the right side, then select **Edit Script**.</span></span>
* <span data-ttu-id="8c304-239">Explorer **SpeechInputSource.cs** de comprendre comment il utilise le **KeywordRecognizer** pour ajouter des commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="8c304-239">Explore **SpeechInputSource.cs** to understand how it uses the **KeywordRecognizer** to add voice commands.</span></span>

### <a name="build-and-deploy"></a><span data-ttu-id="8c304-240">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="8c304-240">Build and Deploy</span></span>

* <span data-ttu-id="8c304-241">Dans Unity, utilisez **fichier > Paramètres de Build** pour régénérer l’application.</span><span class="sxs-lookup"><span data-stu-id="8c304-241">In Unity, use **File > Build Settings** to rebuild the application.</span></span>
* <span data-ttu-id="8c304-242">Ouvrez le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="8c304-242">Open the **App** folder.</span></span>
* <span data-ttu-id="8c304-243">Ouvrez le **ModelExplorer Visual Studio Solution**.</span><span class="sxs-lookup"><span data-stu-id="8c304-243">Open the **ModelExplorer Visual Studio Solution**.</span></span>

<span data-ttu-id="8c304-244">(Si vous avez déjà créé/déployé ce projet dans Visual Studio pendant l’installation, puis vous pouvez ouvrir qu’une instance de Visual Studio et cliquez sur « Recharger All » lorsque vous y êtes invité).</span><span class="sxs-lookup"><span data-stu-id="8c304-244">(If you already built/deployed this project in Visual Studio during set-up, then you can open that instance of VS and click 'Reload All' when prompted).</span></span>

* <span data-ttu-id="8c304-245">Dans Visual Studio, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="8c304-245">In Visual Studio, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
* <span data-ttu-id="8c304-246">Une fois que l’application se déploie sur le HoloLens, faire disparaître la boîte adaptée à l’aide de la [-appui en l’air](gestures.md#air-tap) mouvement.</span><span class="sxs-lookup"><span data-stu-id="8c304-246">After the application deploys to the HoloLens, dismiss the fit box using the [air-tap](gestures.md#air-tap) gesture.</span></span>
* <span data-ttu-id="8c304-247">Fixez du espion de l’astronaut regard.</span><span class="sxs-lookup"><span data-stu-id="8c304-247">Gaze at the astronaut's watch.</span></span>
* <span data-ttu-id="8c304-248">Lors de la surveillance a le focus, vérifiez que le curseur se transforme en un microphone.</span><span class="sxs-lookup"><span data-stu-id="8c304-248">When the watch has focus, verify that the cursor changes to a microphone.</span></span> <span data-ttu-id="8c304-249">Cela fournit des commentaires qui l’application est à l’écoute des commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="8c304-249">This provides feedback that the application is listening for voice commands.</span></span>
* <span data-ttu-id="8c304-250">Vérifiez qu’une info-bulle s’affiche sur la surveillance.</span><span class="sxs-lookup"><span data-stu-id="8c304-250">Verify that a tooltip appears on the watch.</span></span> <span data-ttu-id="8c304-251">Cela permet aux utilisateurs de découvrir le *« Open Communicator »* commande.</span><span class="sxs-lookup"><span data-stu-id="8c304-251">This helps users discover the *"Open Communicator"* command.</span></span>
* <span data-ttu-id="8c304-252">Lors de la gazing à la surveillance, par exemple *« Ouvrir Communicator »* pour ouvrir le panneau de communicator.</span><span class="sxs-lookup"><span data-stu-id="8c304-252">While gazing at the watch, say *"Open Communicator"* to open the communicator panel.</span></span>

## <a name="chapter-2---acknowledgement"></a><span data-ttu-id="8c304-253">Chapitre 2 - accusé de réception</span><span class="sxs-lookup"><span data-stu-id="8c304-253">Chapter 2 - Acknowledgement</span></span>

>[!VIDEO https://www.youtube.com/embed/87ViteoPpyU]

### <a name="objectives"></a><span data-ttu-id="8c304-254">Objectifs</span><span class="sxs-lookup"><span data-stu-id="8c304-254">Objectives</span></span>

* <span data-ttu-id="8c304-255">Enregistrer un message à l’aide de la saisie par Microphone.</span><span class="sxs-lookup"><span data-stu-id="8c304-255">Record a message using the Microphone input.</span></span>
* <span data-ttu-id="8c304-256">Envoyer des commentaires à l’utilisateur que l’application est à l’écoute à leur voix.</span><span class="sxs-lookup"><span data-stu-id="8c304-256">Give feedback to the user that the application is listening to their voice.</span></span>

>[!NOTE]
><span data-ttu-id="8c304-257">Le **Microphone** fonctionnalité doit être déclarée pour une application enregistrer à l’aide du microphone.</span><span class="sxs-lookup"><span data-stu-id="8c304-257">The **Microphone** capability must be declared for an app to record from the microphone.</span></span> <span data-ttu-id="8c304-258">Cela est fait pour vous déjà dans 212 d’entrée M., mais gardez cela à l’esprit pour vos propres projets.</span><span class="sxs-lookup"><span data-stu-id="8c304-258">This is done for you already in MR Input 212, but keep this in mind for your own projects.</span></span>
>
>1. <span data-ttu-id="8c304-259">Dans l’éditeur Unity, accédez aux paramètres player en accédant à « Modifier > projet Paramètres > Player »</span><span class="sxs-lookup"><span data-stu-id="8c304-259">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player"</span></span>
>2. <span data-ttu-id="8c304-260">Cliquez sur l’onglet « Plateforme Windows universelle »</span><span class="sxs-lookup"><span data-stu-id="8c304-260">Click on the "Universal Windows Platform" tab</span></span>
>3. <span data-ttu-id="8c304-261">Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **Microphone** fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="8c304-261">In the "Publishing Settings > Capabilities" section, check the **Microphone** capability</span></span>

### <a name="instructions"></a><span data-ttu-id="8c304-262">Instructions</span><span class="sxs-lookup"><span data-stu-id="8c304-262">Instructions</span></span>

* <span data-ttu-id="8c304-263">Dans Unity **hiérarchie** panneau, vérifiez que le **holoComm_screen_mesh** objet est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="8c304-263">In Unity's **Hierarchy** panel, verify that the **holoComm_screen_mesh** object is selected.</span></span>
* <span data-ttu-id="8c304-264">Dans le **inspecteur** panneau, recherchez le **Astronaut espion (Script)** composant.</span><span class="sxs-lookup"><span data-stu-id="8c304-264">In the **Inspector** panel, find the **Astronaut Watch (Script)** component.</span></span>
* <span data-ttu-id="8c304-265">Cliquez sur le cube petit, bleu, qui est défini comme valeur de la **Prefab Communicator** propriété.</span><span class="sxs-lookup"><span data-stu-id="8c304-265">Click on the small, blue cube which is set as the value of the **Communicator Prefab** property.</span></span>
* <span data-ttu-id="8c304-266">Dans le **projet** Panneau de configuration, le **Communicator** préfabriqué doit maintenant avoir le focus.</span><span class="sxs-lookup"><span data-stu-id="8c304-266">In the **Project** panel, the **Communicator** prefab should now have focus.</span></span>
* <span data-ttu-id="8c304-267">Cliquez sur le **Communicator** prefab dans le **projet** Panneau de configuration pour afficher ses composants dans le **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="8c304-267">Click on the **Communicator** prefab in the **Project** panel to view its components in the **Inspector**.</span></span>
* <span data-ttu-id="8c304-268">Examinez le **Manager Microphone (Script)** composant, cela nous permettra d’enregistrement vocal de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c304-268">Look at the **Microphone Manager (Script)** component, this will allow us to record the user's voice.</span></span>
* <span data-ttu-id="8c304-269">Notez que le **Communicator** objet possède un **Gestionnaire d’entrée vocale (Script)** composant pour répondre à la **envoyer un Message** commande.</span><span class="sxs-lookup"><span data-stu-id="8c304-269">Notice that the **Communicator** object has a **Speech Input Handler (Script)** component for responding to the **Send Message** command.</span></span>
* <span data-ttu-id="8c304-270">Examinez le **Communicator (Script)** composant et double-cliquez sur le script pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c304-270">Look at the **Communicator (Script)** component and double-click on the script to open it in Visual Studio.</span></span>

<span data-ttu-id="8c304-271">Communicator.cs est chargé de définir les États de bouton appropriées sur l’appareil de communicator.</span><span class="sxs-lookup"><span data-stu-id="8c304-271">Communicator.cs is responsible for setting the proper button states on the communicator device.</span></span> <span data-ttu-id="8c304-272">Cela permettra à nos utilisateurs d’enregistrer un message, lire et envoyer le message au astronautes !.</span><span class="sxs-lookup"><span data-stu-id="8c304-272">This will allow our users to record a message, play it back, and send the message to the astronaut.</span></span> <span data-ttu-id="8c304-273">Il sera également commencer et arrêter une forme d’onde animée, pour accuser réception à l’utilisateur qu’il a été entendre leur voix.</span><span class="sxs-lookup"><span data-stu-id="8c304-273">It will also start and stop an animated wave form, to acknowledge to the user that their voice was heard.</span></span>

* <span data-ttu-id="8c304-274">Dans **Communicator.cs**, supprimez les lignes suivantes (81 et 82) de la **Démarrer** (méthode).</span><span class="sxs-lookup"><span data-stu-id="8c304-274">In **Communicator.cs**, delete the following lines (81 and 82) from the **Start** method.</span></span> <span data-ttu-id="8c304-275">Cela active le bouton 'Record' sur le communicator.</span><span class="sxs-lookup"><span data-stu-id="8c304-275">This will enable the 'Record' button on the communicator.</span></span>

```cs
// TODO: 2.a Delete the following two lines:
RecordButton.SetActive(false);
MessageUIRenderer.gameObject.SetActive(false);
```

### <a name="build-and-deploy"></a><span data-ttu-id="8c304-276">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="8c304-276">Build and Deploy</span></span>

* <span data-ttu-id="8c304-277">Dans Visual Studio, régénérez votre application et les déployer sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8c304-277">In Visual Studio, rebuild your application and deploy to the device.</span></span>
* <span data-ttu-id="8c304-278">Fixez du espion de l’astronaut regard et dire *« Open Communicator »* pour afficher le communicator.</span><span class="sxs-lookup"><span data-stu-id="8c304-278">Gaze at the astronaut's watch and say *"Open Communicator"* to show the communicator.</span></span>
* <span data-ttu-id="8c304-279">Appuyez sur la **enregistrement** bouton (microphone) pour commencer l’enregistrement d’un message verbaux pour l’astronautes !.</span><span class="sxs-lookup"><span data-stu-id="8c304-279">Press the **Record** button (microphone) to start recording a verbal message for the astronaut.</span></span>
* <span data-ttu-id="8c304-280">Commencez à parler et vérifiez que l’animation de wave est lue sur communicator, qui fournit des commentaires à l’utilisateur que d’entendre leur voix.</span><span class="sxs-lookup"><span data-stu-id="8c304-280">Start speaking, and verify that the wave animation plays on the communicator, which provides feedback to the user that their voice is heard.</span></span>
* <span data-ttu-id="8c304-281">Appuyez sur la **arrêter** bouton (carré gauche), puis vérifiez que l’animation wave cesse de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="8c304-281">Press the **Stop** button (left square), and verify that the wave animation stops running.</span></span>
* <span data-ttu-id="8c304-282">Appuyez sur la **lire** bouton (triangle rectangle) permettant de lire le message enregistré et avoir votre avis sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8c304-282">Press the **Play** button (right triangle) to play back the recorded message and hear it on the device.</span></span>
* <span data-ttu-id="8c304-283">Appuyez sur la **arrêter** bouton (carré de droite) pour arrêter la lecture du message enregistré.</span><span class="sxs-lookup"><span data-stu-id="8c304-283">Press the **Stop** button (right square) to stop playback of the recorded message.</span></span>
* <span data-ttu-id="8c304-284">Par exemple *« Envoyer un Message »* pour fermer le communicator et de recevoir une réponse « Message reçu » de l’astronaut.</span><span class="sxs-lookup"><span data-stu-id="8c304-284">Say *"Send Message"* to close the communicator and receive a 'Message Received' response from the astronaut.</span></span>

## <a name="chapter-3---understanding-and-the-dictation-recognizer"></a><span data-ttu-id="8c304-285">Chapitre 3 - présentation et le module de reconnaissance de dictée</span><span class="sxs-lookup"><span data-stu-id="8c304-285">Chapter 3 - Understanding and the Dictation Recognizer</span></span>

>[!VIDEO https://www.youtube.com/embed/TIMddr-HqEU]

### <a name="objectives"></a><span data-ttu-id="8c304-286">Objectifs</span><span class="sxs-lookup"><span data-stu-id="8c304-286">Objectives</span></span>

* <span data-ttu-id="8c304-287">Utilisez le module de reconnaissance de dictée pour convertir les voix de l’utilisateur en texte.</span><span class="sxs-lookup"><span data-stu-id="8c304-287">Use the Dictation Recognizer to convert the user's speech to text.</span></span>
* <span data-ttu-id="8c304-288">Afficher les résultats de test d’hypothèse sur et dernière du module de reconnaissance dictée dans l’Office communicator.</span><span class="sxs-lookup"><span data-stu-id="8c304-288">Show the Dictation Recognizer's hypothesized and final results in the communicator.</span></span>

<span data-ttu-id="8c304-289">Dans ce chapitre, nous allons utiliser le module de reconnaissance de dictée pour créer un message pour l’astronautes !.</span><span class="sxs-lookup"><span data-stu-id="8c304-289">In this chapter, we'll use the Dictation Recognizer to create a message for the astronaut.</span></span> <span data-ttu-id="8c304-290">Lorsque vous utilisez le module de reconnaissance de dictée, sachez que :</span><span class="sxs-lookup"><span data-stu-id="8c304-290">When using the Dictation Recognizer, keep in mind that:</span></span>

* <span data-ttu-id="8c304-291">Vous devez être connecté au réseau sans fil pour le module de reconnaissance de dictée fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8c304-291">You must be connected to WiFi for the Dictation Recognizer to work.</span></span>
* <span data-ttu-id="8c304-292">Dépassement du délai après un laps de temps défini.</span><span class="sxs-lookup"><span data-stu-id="8c304-292">Timeouts occur after a set period of time.</span></span> <span data-ttu-id="8c304-293">Il existe deux délais d’expiration à connaître :</span><span class="sxs-lookup"><span data-stu-id="8c304-293">There are two timeouts to be aware of:</span></span>
  * <span data-ttu-id="8c304-294">Si le module de reconnaissance commence et n’entendre des données audio pour les cinq premières secondes, elle dépassera le délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="8c304-294">If the recognizer starts and doesn't hear any audio for the first five seconds, it will timeout.</span></span>
  * <span data-ttu-id="8c304-295">Si le module de reconnaissance a donné un résultat mais puis entend silence pendant 20 secondes, elle dépassera le délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="8c304-295">If the recognizer has given a result but then hears silence for twenty seconds, it will timeout.</span></span>
* <span data-ttu-id="8c304-296">Seul un type de module de reconnaissance (mot clé ou dictée) permettre exécuter à la fois.</span><span class="sxs-lookup"><span data-stu-id="8c304-296">Only one type of recognizer (Keyword or Dictation) can run at a time.</span></span>

>[!NOTE]
><span data-ttu-id="8c304-297">Le **Microphone** fonctionnalité doit être déclarée pour une application enregistrer à l’aide du microphone.</span><span class="sxs-lookup"><span data-stu-id="8c304-297">The **Microphone** capability must be declared for an app to record from the microphone.</span></span> <span data-ttu-id="8c304-298">Cela est fait pour vous déjà dans 212 d’entrée M., mais gardez cela à l’esprit pour vos propres projets.</span><span class="sxs-lookup"><span data-stu-id="8c304-298">This is done for you already in MR Input 212, but keep this in mind for your own projects.</span></span>
>
>1. <span data-ttu-id="8c304-299">Dans l’éditeur Unity, accédez aux paramètres player en accédant à « Modifier > projet Paramètres > Player »</span><span class="sxs-lookup"><span data-stu-id="8c304-299">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player"</span></span>
>2. <span data-ttu-id="8c304-300">Cliquez sur l’onglet « Plateforme Windows universelle »</span><span class="sxs-lookup"><span data-stu-id="8c304-300">Click on the "Universal Windows Platform" tab</span></span>
>3. <span data-ttu-id="8c304-301">Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **Microphone** fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="8c304-301">In the "Publishing Settings > Capabilities" section, check the **Microphone** capability</span></span>

### <a name="instructions"></a><span data-ttu-id="8c304-302">Instructions</span><span class="sxs-lookup"><span data-stu-id="8c304-302">Instructions</span></span>

<span data-ttu-id="8c304-303">Nous allons modifier **MicrophoneManager.cs** à utiliser le module de reconnaissance de dictée.</span><span class="sxs-lookup"><span data-stu-id="8c304-303">We're going to edit **MicrophoneManager.cs** to use the Dictation Recognizer.</span></span> <span data-ttu-id="8c304-304">C’est ce que nous allons ajouter :</span><span class="sxs-lookup"><span data-stu-id="8c304-304">This is what we'll add:</span></span>

1. <span data-ttu-id="8c304-305">Lorsque le **bouton d’enregistrement** est enfoncé, nous allons **démarrer le DictationRecognizer**.</span><span class="sxs-lookup"><span data-stu-id="8c304-305">When the **Record button** is pressed, we'll **start the DictationRecognizer**.</span></span>
2. <span data-ttu-id="8c304-306">Afficher le **hypothèse** de ce que le DictationRecognizer compris.</span><span class="sxs-lookup"><span data-stu-id="8c304-306">Show the **hypothesis** of what the DictationRecognizer understood.</span></span>
3. <span data-ttu-id="8c304-307">Verrouiller le **résultats** de ce que le DictationRecognizer compris.</span><span class="sxs-lookup"><span data-stu-id="8c304-307">Lock in the **results** of what the DictationRecognizer understood.</span></span>
4. <span data-ttu-id="8c304-308">Recherchez les délais d’attente à partir de la DictationRecognizer.</span><span class="sxs-lookup"><span data-stu-id="8c304-308">Check for timeouts from the DictationRecognizer.</span></span>
5. <span data-ttu-id="8c304-309">Lorsque le **bouton Arrêter** est enfoncé, ou la session de mic arrive à expiration, **arrêter le DictationRecognizer**.</span><span class="sxs-lookup"><span data-stu-id="8c304-309">When the **Stop button** is pressed, or the mic session times out, **stop the DictationRecognizer**.</span></span>
6. <span data-ttu-id="8c304-310">Redémarrez le **KeywordRecognizer**, qui écoutera les le **envoyer un Message** commande.</span><span class="sxs-lookup"><span data-stu-id="8c304-310">Restart the **KeywordRecognizer**, which will listen for the **Send Message** command.</span></span>

<span data-ttu-id="8c304-311">Commençons.</span><span class="sxs-lookup"><span data-stu-id="8c304-311">Let's get started.</span></span> <span data-ttu-id="8c304-312">Terminer tous les exercices de codage pour 3.a dans **MicrophoneManager.cs**, ou copiez et collez le code de fin figurant ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8c304-312">Complete all coding exercises for 3.a in **MicrophoneManager.cs**, or copy and paste the finished code found below:</span></span>

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

### <a name="build-and-deploy"></a><span data-ttu-id="8c304-313">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="8c304-313">Build and Deploy</span></span>

* <span data-ttu-id="8c304-314">Régénérez dans Visual Studio et les déployer sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="8c304-314">Rebuild in Visual Studio and deploy to your device.</span></span>
* <span data-ttu-id="8c304-315">Fermez l’adapté avec un mouvement d’appui en l’air.</span><span class="sxs-lookup"><span data-stu-id="8c304-315">Dismiss the fit box with an air-tap gesture.</span></span>
* <span data-ttu-id="8c304-316">Fixez du espion de l’astronaut regard et dire *« Open Communicator »*.</span><span class="sxs-lookup"><span data-stu-id="8c304-316">Gaze at the astronaut's watch and say *"Open Communicator"*.</span></span>
* <span data-ttu-id="8c304-317">Sélectionnez le **enregistrement** bouton (microphone) pour enregistrer votre message.</span><span class="sxs-lookup"><span data-stu-id="8c304-317">Select the **Record** button (microphone) to record your message.</span></span>
* <span data-ttu-id="8c304-318">Commencez à parler.</span><span class="sxs-lookup"><span data-stu-id="8c304-318">Start speaking.</span></span> <span data-ttu-id="8c304-319">Le **module de reconnaissance de dictée** interprétera votre enregistrement vocal et afficher le test d’hypothèse sur texte dans l’Office communicator.</span><span class="sxs-lookup"><span data-stu-id="8c304-319">The **Dictation Recognizer** will interpret your speech and show the hypothesized text in the communicator.</span></span>
* <span data-ttu-id="8c304-320">Essayez de dire *« Envoyer un Message »* pendant que vous enregistrez un message.</span><span class="sxs-lookup"><span data-stu-id="8c304-320">Try saying *"Send Message"* while you are recording a message.</span></span> <span data-ttu-id="8c304-321">Notez que le **mot clé de module de reconnaissance** ne répond pas, car le **module de reconnaissance de dictée** est toujours actif.</span><span class="sxs-lookup"><span data-stu-id="8c304-321">Notice that the **Keyword Recognizer** does not respond because the **Dictation Recognizer** is still active.</span></span>
* <span data-ttu-id="8c304-322">Arrêter de parler de quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="8c304-322">Stop speaking for a few seconds.</span></span> <span data-ttu-id="8c304-323">Écoutez le module de reconnaissance de dictée se termine son hypothèse et affiche le résultat final.</span><span class="sxs-lookup"><span data-stu-id="8c304-323">Watch as the Dictation Recognizer completes its hypothesis and shows the final result.</span></span>
* <span data-ttu-id="8c304-324">Commencez à parler et puis de s’interrompre pendant 20 secondes.</span><span class="sxs-lookup"><span data-stu-id="8c304-324">Begin speaking and then pause for 20 seconds.</span></span> <span data-ttu-id="8c304-325">Cela entraîne le **module de reconnaissance de dictée** au délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="8c304-325">This will cause the **Dictation Recognizer** to timeout.</span></span>
* <span data-ttu-id="8c304-326">Notez que le **module de reconnaissance de mot clé** est réactivé après le délai d’attente ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8c304-326">Notice that the **Keyword Recognizer** is re-enabled after the above timeout.</span></span> <span data-ttu-id="8c304-327">Le communicator est maintenant répondre aux commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="8c304-327">The communicator will now respond to voice commands.</span></span>
* <span data-ttu-id="8c304-328">Par exemple *« Envoyer un Message »* pour envoyer le message au astronautes !.</span><span class="sxs-lookup"><span data-stu-id="8c304-328">Say *"Send Message"* to send the message to the astronaut.</span></span>

## <a name="chapter-4---grammar-recognizer"></a><span data-ttu-id="8c304-329">Chapitre 4 - module de reconnaissance de grammaire</span><span class="sxs-lookup"><span data-stu-id="8c304-329">Chapter 4 - Grammar Recognizer</span></span>

>[!VIDEO https://www.youtube.com/embed/J2dYJNSvv18]

### <a name="objectives"></a><span data-ttu-id="8c304-330">Objectifs</span><span class="sxs-lookup"><span data-stu-id="8c304-330">Objectives</span></span>

* <span data-ttu-id="8c304-331">Utilisez le module de reconnaissance de grammaire voix de l’utilisateur en fonction d’un fichier SRGS ou spécification de grammaire de reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="8c304-331">Use the Grammar Recognizer to recognize the user's speech according to an SRGS, or Speech Recognition Grammar Specification, file.</span></span>

>[!NOTE]
><span data-ttu-id="8c304-332">Le **Microphone** fonctionnalité doit être déclarée pour une application enregistrer à l’aide du microphone.</span><span class="sxs-lookup"><span data-stu-id="8c304-332">The **Microphone** capability must be declared for an app to record from the microphone.</span></span> <span data-ttu-id="8c304-333">Cela est fait pour vous déjà dans 212 d’entrée M., mais gardez cela à l’esprit pour vos propres projets.</span><span class="sxs-lookup"><span data-stu-id="8c304-333">This is done for you already in MR Input 212, but keep this in mind for your own projects.</span></span>
>
>1. <span data-ttu-id="8c304-334">Dans l’éditeur Unity, accédez aux paramètres player en accédant à « Modifier > projet Paramètres > Player »</span><span class="sxs-lookup"><span data-stu-id="8c304-334">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player"</span></span>
>2. <span data-ttu-id="8c304-335">Cliquez sur l’onglet « Plateforme Windows universelle »</span><span class="sxs-lookup"><span data-stu-id="8c304-335">Click on the "Universal Windows Platform" tab</span></span>
>3. <span data-ttu-id="8c304-336">Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **Microphone** fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="8c304-336">In the "Publishing Settings > Capabilities" section, check the **Microphone** capability</span></span>

### <a name="instructions"></a><span data-ttu-id="8c304-337">Instructions</span><span class="sxs-lookup"><span data-stu-id="8c304-337">Instructions</span></span>

1. <span data-ttu-id="8c304-338">Dans le **hiérarchie** du panneau, recherchez **Jetpack_Center** et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="8c304-338">In the **Hierarchy** panel, search for **Jetpack_Center** and select it.</span></span>
2. <span data-ttu-id="8c304-339">Recherchez le **accompagnent Action** de script dans le **inspecteur** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="8c304-339">Look for the **Tagalong Action** script in the **Inspector** panel.</span></span>
3. <span data-ttu-id="8c304-340">Cliquez sur le petit cercle à droite de la **objet de balise le long** champ.</span><span class="sxs-lookup"><span data-stu-id="8c304-340">Click the little circle to the right of the **Object To Tag Along** field.</span></span>
4. <span data-ttu-id="8c304-341">Dans la fenêtre qui s’affiche, recherchez **SRGSToolbox** et sélectionnez-le dans la liste.</span><span class="sxs-lookup"><span data-stu-id="8c304-341">In the window that pops up, search for **SRGSToolbox** and select it from the list.</span></span>
5. <span data-ttu-id="8c304-342">Jetez un coup de œil à la **SRGSColor.xml** de fichiers dans le **StreamingAssets** dossier.</span><span class="sxs-lookup"><span data-stu-id="8c304-342">Take a look at the **SRGSColor.xml** file in the **StreamingAssets** folder.</span></span>
* <span data-ttu-id="8c304-343">La spécification de conception SRGS sont accessibles sur le site Web W3C [ici](https://www.w3.org/TR/speech-grammar/).</span><span class="sxs-lookup"><span data-stu-id="8c304-343">The SRGS design spec can be found on the W3C website [here](https://www.w3.org/TR/speech-grammar/).</span></span>
* <span data-ttu-id="8c304-344">Dans notre fichier SRGS, nous avons trois types de règles :</span><span class="sxs-lookup"><span data-stu-id="8c304-344">In our SRGS file, we have three types of rules:</span></span>
  * <span data-ttu-id="8c304-345">Une règle qui vous permet d’indiquer une couleur à partir d’une liste de douze couleurs.</span><span class="sxs-lookup"><span data-stu-id="8c304-345">A rule which lets you say one color from a list of twelve colors.</span></span>
  * <span data-ttu-id="8c304-346">Trois règles qui écoutent une combinaison de la règle de couleur et l’une des trois formes.</span><span class="sxs-lookup"><span data-stu-id="8c304-346">Three rules which listen for a combination of the color rule and one of the three shapes.</span></span>
  * <span data-ttu-id="8c304-347">La règle racine, colorChooser d’écoute de n’importe quelle combinaison des trois règles « couleur + mettre en forme ».</span><span class="sxs-lookup"><span data-stu-id="8c304-347">The root rule, colorChooser, which listens for any combination of the three "color + shape" rules.</span></span> <span data-ttu-id="8c304-348">Les formes peuvent être désignées dans n’importe quel ordre et dans n’importe quel volume depuis un seul pour les trois.</span><span class="sxs-lookup"><span data-stu-id="8c304-348">The shapes can be said in any order and in any amount from just one to all three.</span></span> <span data-ttu-id="8c304-349">Ceci est la seule règle qui est écoutée, tel qu’il est spécifié comme règle racine en haut du fichier initial &lt;grammaire&gt; balise.</span><span class="sxs-lookup"><span data-stu-id="8c304-349">This is the only rule that is listened for, as it's specified as the root rule at the top of the file in the initial &lt;grammar&gt; tag.</span></span>

### <a name="build-and-deploy"></a><span data-ttu-id="8c304-350">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="8c304-350">Build and Deploy</span></span>

* <span data-ttu-id="8c304-351">Régénérez l’application dans Unity, puis générez et déployez à partir de Visual Studio pour profiter de l’application sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="8c304-351">Rebuild the application in Unity, then build and deploy from Visual Studio to experience the app on HoloLens.</span></span>
* <span data-ttu-id="8c304-352">Fermez l’adapté avec un mouvement d’appui en l’air.</span><span class="sxs-lookup"><span data-stu-id="8c304-352">Dismiss the fit box with an air-tap gesture.</span></span>
* <span data-ttu-id="8c304-353">Fixez du jetpack de l’astronaut regard et effectuez un mouvement d’appui en l’air.</span><span class="sxs-lookup"><span data-stu-id="8c304-353">Gaze at the astronaut's jetpack and perform an air-tap gesture.</span></span>
* <span data-ttu-id="8c304-354">Commencez à parler.</span><span class="sxs-lookup"><span data-stu-id="8c304-354">Start speaking.</span></span> <span data-ttu-id="8c304-355">Le **module de reconnaissance de grammaire** interpréter votre voix et de modifier les couleurs des formes en fonction de la reconnaissance.</span><span class="sxs-lookup"><span data-stu-id="8c304-355">The **Grammar Recognizer** will interpret your speech and change the colors of the shapes based on the recognition.</span></span> <span data-ttu-id="8c304-356">Un exemple de commande est « cercle bleu, jaune carré ».</span><span class="sxs-lookup"><span data-stu-id="8c304-356">An example command is "blue circle, yellow square".</span></span>
* <span data-ttu-id="8c304-357">Effectuez une autre-appui en l’air pour faire disparaître la boîte à outils.</span><span class="sxs-lookup"><span data-stu-id="8c304-357">Perform another air-tap gesture to dismiss the toolbox.</span></span>

## <a name="the-end"></a><span data-ttu-id="8c304-358">La fin</span><span class="sxs-lookup"><span data-stu-id="8c304-358">The End</span></span>

<span data-ttu-id="8c304-359">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="8c304-359">Congratulations!</span></span> <span data-ttu-id="8c304-360">Vous avez maintenant terminé **212 d’entrée M. : Voix**.</span><span class="sxs-lookup"><span data-stu-id="8c304-360">You have now completed **MR Input 212: Voice**.</span></span>

* <span data-ttu-id="8c304-361">Vous connaissez les choses à faire et des commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="8c304-361">You know the Dos and Don'ts of voice commands.</span></span>
* <span data-ttu-id="8c304-362">Vous avez vu comment les info-bulles ont été utilisés pour informer les utilisateurs des commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="8c304-362">You saw how tooltips were employed to make users aware of voice commands.</span></span>
* <span data-ttu-id="8c304-363">Vous avez vu plusieurs types de commentaires permet de confirmer que la voix de l’utilisateur a été émises.</span><span class="sxs-lookup"><span data-stu-id="8c304-363">You saw several types of feedback used to acknowledge that the user's voice was heard.</span></span>
* <span data-ttu-id="8c304-364">Vous savez comment basculer entre le module de reconnaissance du mot clé et le module de reconnaissance de dictée, et comment ces deux fonctionnalités comprennent et interprètent votre voix.</span><span class="sxs-lookup"><span data-stu-id="8c304-364">You know how to switch between the Keyword Recognizer and the Dictation Recognizer, and how these two features understand and interpret your voice.</span></span>
* <span data-ttu-id="8c304-365">Vous avez appris comment utiliser un fichier SRGS et le module de reconnaissance de grammaire de reconnaissance vocale dans votre application.</span><span class="sxs-lookup"><span data-stu-id="8c304-365">You learned how to use an SRGS file and the Grammar Recognizer for speech recognition in your application.</span></span>
