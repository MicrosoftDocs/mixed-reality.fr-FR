---
title: Entrée M. 211 - mouvement
description: Suivez cette procédure pas à pas codage à l’aide de Unity, Visual Studio et HoloLens pour connaître les détails des concepts de mouvement.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, academy, tutorial, gesture
ms.openlocfilehash: 76d2b4c0ac3d0a3783b091f7dc8c39548a18b548
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596148"
---
>[!NOTE]
><span data-ttu-id="d140e-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="d140e-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="d140e-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="d140e-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="d140e-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="d140e-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="d140e-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d140e-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="d140e-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="d140e-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="d140e-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="d140e-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

# <a name="mr-input-211-gesture"></a><span data-ttu-id="d140e-110">Entrée M. 211 : Mouvement</span><span class="sxs-lookup"><span data-stu-id="d140e-110">MR Input 211: Gesture</span></span>

<span data-ttu-id="d140e-111">[Mouvements](gestures.md) transformer d’intention de l’utilisateur en action.</span><span class="sxs-lookup"><span data-stu-id="d140e-111">[Gestures](gestures.md) turn user intention into action.</span></span> <span data-ttu-id="d140e-112">Les gestes, les utilisateurs peuvent interagir avec hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d140e-112">With gestures, users can interact with holograms.</span></span> <span data-ttu-id="d140e-113">Dans ce cours, nous allons apprendre à effectuer le suivi des mains de l’utilisateur, répondre aux entrées d’utilisateur, et envoyez vos commentaires à l’utilisateur quant à état et l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="d140e-113">In this course, we'll learn how to track the user's hands, respond to user input, and give feedback to the user based on hand state and location.</span></span>

>[!VIDEO https://www.youtube.com/embed/c9zlpfFeEtc]

<span data-ttu-id="d140e-114">Dans [101 des principes fondamentaux de M.](holograms-101.md), nous avons utilisé un mouvement d’appui simple d’interagir avec notre hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d140e-114">In [MR Basics 101](holograms-101.md), we used a simple air-tap gesture to interact with our holograms.</span></span> <span data-ttu-id="d140e-115">Maintenant, nous le mouvement d’appui en l’air au-delà des concepts et explorez les nouveaux concepts à :</span><span class="sxs-lookup"><span data-stu-id="d140e-115">Now, we'll move beyond the air-tap gesture and explore new concepts to:</span></span>

* <span data-ttu-id="d140e-116">Détecter lorsque le suivi de main de l’utilisateur et fournir des commentaires à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d140e-116">Detect when the user's hand is being tracked and provide feedback to the user.</span></span>
* <span data-ttu-id="d140e-117">Utilisez un mouvement de navigation pour faire pivoter notre hologrammes.</span><span class="sxs-lookup"><span data-stu-id="d140e-117">Use a navigation gesture to rotate our holograms.</span></span>
* <span data-ttu-id="d140e-118">Fournir des commentaires lors de la part de l’utilisateur est sur le point de sortir de la vue.</span><span class="sxs-lookup"><span data-stu-id="d140e-118">Provide feedback when the user's hand is about to go out of view.</span></span>
* <span data-ttu-id="d140e-119">Utilisez les événements de manipulation pour permettre aux utilisateurs de déplacer hologrammes avec leurs mains.</span><span class="sxs-lookup"><span data-stu-id="d140e-119">Use manipulation events to allow users to move holograms with their hands.</span></span>

<span data-ttu-id="d140e-120">Dans ce cours, nous y reviendrons le projet Unity **l’Explorateur de modèles**, que nous avons construit dans [210 d’entrée M.](holograms-210.md).</span><span class="sxs-lookup"><span data-stu-id="d140e-120">In this course, we'll revisit the Unity project **Model Explorer**, which we built in [MR Input 210](holograms-210.md).</span></span> <span data-ttu-id="d140e-121">Notre ami astronautes est à nous assister dans notre exploration de ces nouveaux concepts de mouvement.</span><span class="sxs-lookup"><span data-stu-id="d140e-121">Our astronaut friend is back to assist us in our exploration of these new gesture concepts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="d140e-122">Les vidéos incorporées dans chacun des chapitres ci-dessous ont été enregistrés à l’aide d’une version antérieure de Unity et le Kit de ressources de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="d140e-122">The videos embedded in each of the chapters below were recorded using an older version of Unity and the Mixed Reality Toolkit.</span></span> <span data-ttu-id="d140e-123">Tandis que les instructions pas à pas sont précises et actuelles, vous pouvez voir des scripts et des éléments visuels dans les vidéos correspondantes qui sont obsolètes.</span><span class="sxs-lookup"><span data-stu-id="d140e-123">While the step-by-step instructions are accurate and current, you may see scripts and visuals in the corresponding videos that are out-of-date.</span></span> <span data-ttu-id="d140e-124">Les vidéos restent inclus éternellement et car couvert les concepts s’appliquent toujours.</span><span class="sxs-lookup"><span data-stu-id="d140e-124">The videos remain included for posterity and because the concepts covered still apply.</span></span>

## <a name="device-support"></a><span data-ttu-id="d140e-125">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="d140e-125">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="d140e-126">Cours</span><span class="sxs-lookup"><span data-stu-id="d140e-126">Course</span></span></th><th style="width:150px"> <span data-ttu-id="d140e-127"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="d140e-127"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="d140e-128"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="d140e-128"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="d140e-129">Entrée M. 211 : Mouvement</span><span class="sxs-lookup"><span data-stu-id="d140e-129">MR Input 211: Gesture</span></span></td><td style="text-align: center;"> <span data-ttu-id="d140e-130">✔️</span><span class="sxs-lookup"><span data-stu-id="d140e-130">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="d140e-131">✔️</span><span class="sxs-lookup"><span data-stu-id="d140e-131">✔️</span></span></td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="d140e-132">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d140e-132">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d140e-133">Prérequis</span><span class="sxs-lookup"><span data-stu-id="d140e-133">Prerequisites</span></span>

* <span data-ttu-id="d140e-134">Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="d140e-134">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>
* <span data-ttu-id="d140e-135">Base C# possibilité de programmation.</span><span class="sxs-lookup"><span data-stu-id="d140e-135">Some basic C# programming ability.</span></span>
* <span data-ttu-id="d140e-136">Vous devez avoir terminé [101 de principes de base MR](holograms-101.md).</span><span class="sxs-lookup"><span data-stu-id="d140e-136">You should have completed [MR Basics 101](holograms-101.md).</span></span>
* <span data-ttu-id="d140e-137">Vous devez avoir terminé [210 d’entrée M.](holograms-210.md).</span><span class="sxs-lookup"><span data-stu-id="d140e-137">You should have completed [MR Input 210](holograms-210.md).</span></span>
* <span data-ttu-id="d140e-138">Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="d140e-138">A HoloLens device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

### <a name="project-files"></a><span data-ttu-id="d140e-139">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="d140e-139">Project files</span></span>

* <span data-ttu-id="d140e-140">Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-211-Gesture.zip) requise par le projet.</span><span class="sxs-lookup"><span data-stu-id="d140e-140">Download the [files](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-211-Gesture.zip) required by the project.</span></span><span data-ttu-id="d140e-141"> Nécessite Unity 2017.2 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d140e-141"> Requires Unity 2017.2 or later.</span></span>
* <span data-ttu-id="d140e-142">Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="d140e-142">Un-archive the files to your desktop or other easy to reach location.</span></span>

>[!NOTE]
><span data-ttu-id="d140e-143">Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-211-Gesture).</span><span class="sxs-lookup"><span data-stu-id="d140e-143">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-211-Gesture).</span></span>

### <a name="errata-and-notes"></a><span data-ttu-id="d140e-144">Errata et remarques</span><span class="sxs-lookup"><span data-stu-id="d140e-144">Errata and Notes</span></span>

* <span data-ttu-id="d140e-145">« Activer uniquement mon Code » doit être désactivé (*unchecked*) dans Visual Studio sous Outils -> Options -> débogage afin d’atteindre des points d’arrêt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="d140e-145">"Enable Just My Code" needs to be disabled (*unchecked*) in Visual Studio under Tools->Options->Debugging in order to hit breakpoints in your code.</span></span>

## <a name="chapter-0---unity-setup"></a><span data-ttu-id="d140e-146">Chapitre 0 - le programme d’installation Unity</span><span class="sxs-lookup"><span data-stu-id="d140e-146">Chapter 0 - Unity Setup</span></span>

### <a name="instructions"></a><span data-ttu-id="d140e-147">Instructions</span><span class="sxs-lookup"><span data-stu-id="d140e-147">Instructions</span></span>

1. <span data-ttu-id="d140e-148">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="d140e-148">Start Unity.</span></span>
2. <span data-ttu-id="d140e-149">Sélectionnez **Open**.</span><span class="sxs-lookup"><span data-stu-id="d140e-149">Select **Open**.</span></span>
3. <span data-ttu-id="d140e-150">Accédez à la **mouvement** dossier vous précédemment non archivés.</span><span class="sxs-lookup"><span data-stu-id="d140e-150">Navigate to the **Gesture** folder you previously un-archived.</span></span>
4. <span data-ttu-id="d140e-151">Recherchez et sélectionnez le **démarrage**/**l’Explorateur de modèles** dossier.</span><span class="sxs-lookup"><span data-stu-id="d140e-151">Find and select the **Starting**/**Model Explorer** folder.</span></span>
5. <span data-ttu-id="d140e-152">Cliquez sur le **sélectionner le dossier** bouton.</span><span class="sxs-lookup"><span data-stu-id="d140e-152">Click the **Select Folder** button.</span></span>
6. <span data-ttu-id="d140e-153">Dans le **projet** volet, développez le **scènes** dossier.</span><span class="sxs-lookup"><span data-stu-id="d140e-153">In the **Project** panel, expand the **Scenes** folder.</span></span>
7. <span data-ttu-id="d140e-154">Double-cliquez sur **ModelExplorer** scène à le charger dans Unity.</span><span class="sxs-lookup"><span data-stu-id="d140e-154">Double-click **ModelExplorer** scene to load it in Unity.</span></span>

### <a name="building"></a><span data-ttu-id="d140e-155">Génération</span><span class="sxs-lookup"><span data-stu-id="d140e-155">Building</span></span>

1. <span data-ttu-id="d140e-156">Dans Unity, sélectionnez **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="d140e-156">In Unity, select **File > Build Settings**.</span></span>
2. <span data-ttu-id="d140e-157">Si **arrière-plan/ModelExplorer** n’est pas répertorié dans **scènes dans Build**, cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="d140e-157">If **Scenes/ModelExplorer** is not listed in **Scenes In Build**, click **Add Open Scenes** to add the scene.</span></span>
3. <span data-ttu-id="d140e-158">Si vous développez en particulier pour HoloLens, définissez **appareil cible** à **HoloLens**.</span><span class="sxs-lookup"><span data-stu-id="d140e-158">If you're specifically developing for HoloLens, set **Target device** to **HoloLens**.</span></span> <span data-ttu-id="d140e-159">Dans le cas contraire, laissez-le sur **n’importe quel appareil**.</span><span class="sxs-lookup"><span data-stu-id="d140e-159">Otherwise, leave it on **Any device**.</span></span>
4. <span data-ttu-id="d140e-160">Vérifiez **Type Build** a la valeur **D3D** et **SDK** a la valeur **dernière installé** (qui doit être SDK 16299 ou une version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="d140e-160">Ensure **Build Type** is set to **D3D** and **SDK** is set to **Latest installed** (which should be SDK 16299 or newer).</span></span>
5. <span data-ttu-id="d140e-161">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="d140e-161">Click **Build**.</span></span>
6. <span data-ttu-id="d140e-162">Créer un **nouveau dossier** nommé « Application ».</span><span class="sxs-lookup"><span data-stu-id="d140e-162">Create a **New Folder** named "App".</span></span>
7. <span data-ttu-id="d140e-163">Clic le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="d140e-163">Single click the **App** folder.</span></span>
8. <span data-ttu-id="d140e-164">Appuyez sur **sélectionner le dossier** et Unity commence à générer le projet pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d140e-164">Press **Select Folder** and Unity will start building the project for Visual Studio.</span></span>

<span data-ttu-id="d140e-165">Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d140e-165">When Unity is done, a File Explorer window will appear.</span></span>

1. <span data-ttu-id="d140e-166">Ouvrez le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="d140e-166">Open the **App** folder.</span></span>
2. <span data-ttu-id="d140e-167">Ouvrez le **ModelExplorer Visual Studio Solution**.</span><span class="sxs-lookup"><span data-stu-id="d140e-167">Open the **ModelExplorer Visual Studio Solution**.</span></span>

<span data-ttu-id="d140e-168">Si le déploiement sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="d140e-168">If deploying to HoloLens:</span></span>

1. <span data-ttu-id="d140e-169">À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x86**.</span><span class="sxs-lookup"><span data-stu-id="d140e-169">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x86**.</span></span>
2. <span data-ttu-id="d140e-170">Cliquez sur la flèche déroulante en regard du bouton de l’ordinateur Local, puis sélectionnez **Machine distante**.</span><span class="sxs-lookup"><span data-stu-id="d140e-170">Click on the drop down arrow next to the Local Machine button, and select **Remote Machine**.</span></span>
3. <span data-ttu-id="d140e-171">Entrez **votre adresse IP du périphérique HoloLens** et définir le Mode d’authentification **universel (protocole non chiffré)**.</span><span class="sxs-lookup"><span data-stu-id="d140e-171">Enter **your HoloLens device IP address** and set Authentication Mode to **Universal (Unencrypted Protocol)**.</span></span> <span data-ttu-id="d140e-172">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="d140e-172">Click **Select**.</span></span> <span data-ttu-id="d140e-173">Si vous ne connaissez pas votre adresse IP du périphérique, recherchez dans **Paramètres > réseau & Internet > Options avancées**.</span><span class="sxs-lookup"><span data-stu-id="d140e-173">If you do not know your device IP address, look in **Settings > Network & Internet > Advanced Options**.</span></span>
4. <span data-ttu-id="d140e-174">Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="d140e-174">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span> <span data-ttu-id="d140e-175">S’il s’agit de la première fois le déploiement sur votre périphérique, vous devrez [Couplez-le Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span><span class="sxs-lookup"><span data-stu-id="d140e-175">If this is the first time deploying to your device, you will need to [pair it with Visual Studio](using-visual-studio.md#pairing-your-device-hololens).</span></span>
5. <span data-ttu-id="d140e-176">Lorsque l’application a été déployée, faire disparaître le **Fitbox** avec un **sélectionnez mouvement**.</span><span class="sxs-lookup"><span data-stu-id="d140e-176">When the app has deployed, dismiss the **Fitbox** with a **select gesture**.</span></span>

<span data-ttu-id="d140e-177">Si le déploiement sur un casque immersif :</span><span class="sxs-lookup"><span data-stu-id="d140e-177">If deploying to an immersive headset:</span></span>

1. <span data-ttu-id="d140e-178">À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x64**.</span><span class="sxs-lookup"><span data-stu-id="d140e-178">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **x64**.</span></span>
2. <span data-ttu-id="d140e-179">Assurez-vous que la cible de déploiement est définie sur **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="d140e-179">Make sure the deployment target is set to **Local Machine**.</span></span>
3. <span data-ttu-id="d140e-180">Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="d140e-180">In the top menu bar, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
4. <span data-ttu-id="d140e-181">Lorsque l’application a été déployée, faire disparaître le **Fitbox** en extrayant le déclencheur sur un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="d140e-181">When the app has deployed, dismiss the **Fitbox** by pulling the trigger on a motion controller.</span></span>

>[!NOTE]
><span data-ttu-id="d140e-182">Vous remarquerez peut-être des erreurs rouge dans le panneau erreurs de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d140e-182">You might notice some red errors in the Visual Studio Errors panel.</span></span> <span data-ttu-id="d140e-183">Il est possible de les ignorer.</span><span class="sxs-lookup"><span data-stu-id="d140e-183">It is safe to ignore them.</span></span> <span data-ttu-id="d140e-184">Basculer vers le volet de sortie pour afficher les réelle progression de la build.</span><span class="sxs-lookup"><span data-stu-id="d140e-184">Switch to the Output panel to view actual build progress.</span></span> <span data-ttu-id="d140e-185">Erreurs dans le volet de sortie vous obligera à effectuer un correctif (la plus souvent qu’ils sont provoquées par une erreur dans un script).</span><span class="sxs-lookup"><span data-stu-id="d140e-185">Errors in the Output panel will require you to make a fix (most often they are caused by a mistake in a script).</span></span>

## <a name="chapter-1---hand-detected-feedback"></a><span data-ttu-id="d140e-186">Chapitre 1 - main a détecté des commentaires</span><span class="sxs-lookup"><span data-stu-id="d140e-186">Chapter 1 - Hand detected feedback</span></span>

>[!VIDEO https://www.youtube.com/embed/D1FcIyuFTZQ]

### <a name="objectives"></a><span data-ttu-id="d140e-187">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d140e-187">Objectives</span></span>

* <span data-ttu-id="d140e-188">S’abonner pour transmettre des événements de suivi.</span><span class="sxs-lookup"><span data-stu-id="d140e-188">Subscribe to hand tracking events.</span></span>
* <span data-ttu-id="d140e-189">Utilisez le curseur pour afficher les utilisateurs lors de la main est suivie.</span><span class="sxs-lookup"><span data-stu-id="d140e-189">Use cursor feedback to show users when a hand is being tracked.</span></span>

### <a name="instructions"></a><span data-ttu-id="d140e-190">Instructions</span><span class="sxs-lookup"><span data-stu-id="d140e-190">Instructions</span></span>

* <span data-ttu-id="d140e-191">Dans le **hiérarchie** volet, développez le **InputManager** objet.</span><span class="sxs-lookup"><span data-stu-id="d140e-191">In the **Hierarchy** panel, expand the **InputManager** object.</span></span>
* <span data-ttu-id="d140e-192">Recherchez et sélectionnez le **GesturesInput** objet.</span><span class="sxs-lookup"><span data-stu-id="d140e-192">Look for and select the **GesturesInput** object.</span></span>

<span data-ttu-id="d140e-193">Le **InteractionInputSource.cs** script effectue ces étapes :</span><span class="sxs-lookup"><span data-stu-id="d140e-193">The **InteractionInputSource.cs** script performs these steps:</span></span>

1. <span data-ttu-id="d140e-194">S’abonne aux événements InteractionSourceDetected et InteractionSourceLost.</span><span class="sxs-lookup"><span data-stu-id="d140e-194">Subscribes to the InteractionSourceDetected and InteractionSourceLost events.</span></span>
2. <span data-ttu-id="d140e-195">Définit l’état HandDetected.</span><span class="sxs-lookup"><span data-stu-id="d140e-195">Sets the HandDetected state.</span></span>
3. <span data-ttu-id="d140e-196">Annule l’abonnement à partir des événements InteractionSourceDetected et InteractionSourceLost.</span><span class="sxs-lookup"><span data-stu-id="d140e-196">Unsubscribes from the InteractionSourceDetected and InteractionSourceLost events.</span></span>

<span data-ttu-id="d140e-197">Ensuite, nous allons mettre à niveau notre curseur à partir [210 d’entrée M.](holograms-210.md) en une seule qui affiche des commentaires en fonction des actions de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d140e-197">Next, we'll upgrade our cursor from [MR Input 210](holograms-210.md) into one that shows feedback depending on the user's actions.</span></span>

1. <span data-ttu-id="d140e-198">Dans le **hiérarchie** Panneau de configuration, sélectionnez le **curseur** de l’objet et supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="d140e-198">In the **Hierarchy** panel, select the **Cursor** object and delete it.</span></span>
2. <span data-ttu-id="d140e-199">Dans le **projet** du panneau, recherchez **CursorWithFeedback** et faites-le glisser vers le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="d140e-199">In the **Project** panel, search for **CursorWithFeedback** and drag it into the **Hierarchy** panel.</span></span>
3. <span data-ttu-id="d140e-200">Cliquez sur **InputManager** dans le **hiérarchie** panneau, puis faites glisser le **CursorWithFeedback** de l’objet à partir de la **hiérarchie** dans le De InputManager **SimpleSinglePointerSelector**de **curseur** champ, en bas de la **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="d140e-200">Click on **InputManager** in the **Hierarchy** panel, then drag the **CursorWithFeedback** object from the **Hierarchy** into the InputManager's **SimpleSinglePointerSelector**'s **Cursor** field, at the bottom of the **Inspector**.</span></span>
4. <span data-ttu-id="d140e-201">Cliquez sur le **CursorWithFeedback** dans le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d140e-201">Click on the **CursorWithFeedback** in the **Hierarchy**.</span></span>
5. <span data-ttu-id="d140e-202">Dans le **inspecteur** volet, développez **données d’état de curseur** sur le **objet curseur** script.</span><span class="sxs-lookup"><span data-stu-id="d140e-202">In the **Inspector** panel, expand **Cursor State Data** on the **Object Cursor** script.</span></span>

<span data-ttu-id="d140e-203">Le **données d’état de curseur** fonctionne comme suit :</span><span class="sxs-lookup"><span data-stu-id="d140e-203">The **Cursor State Data** works like this:</span></span>

* <span data-ttu-id="d140e-204">N’importe quel **observer** état signifie qu’aucun main n’est détecté et que l’utilisateur est simplement chercher.</span><span class="sxs-lookup"><span data-stu-id="d140e-204">Any **Observe** state means that no hand is detected and the user is simply looking around.</span></span>
* <span data-ttu-id="d140e-205">N’importe quel **Interact** état signifie qu’une main ou le contrôleur a été détecté.</span><span class="sxs-lookup"><span data-stu-id="d140e-205">Any **Interact** state means that a hand or controller is detected.</span></span>
* <span data-ttu-id="d140e-206">N’importe quel **pointez** état signifie que l’utilisateur consulte un hologramme.</span><span class="sxs-lookup"><span data-stu-id="d140e-206">Any **Hover** state means the user is looking at a hologram.</span></span>

### <a name="build-and-deploy"></a><span data-ttu-id="d140e-207">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="d140e-207">Build and Deploy</span></span>

* <span data-ttu-id="d140e-208">Dans Unity, utilisez **fichier > Paramètres de Build** pour régénérer l’application.</span><span class="sxs-lookup"><span data-stu-id="d140e-208">In Unity, use **File > Build Settings** to rebuild the application.</span></span>
* <span data-ttu-id="d140e-209">Ouvrez le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="d140e-209">Open the **App** folder.</span></span>
* <span data-ttu-id="d140e-210">Si elle n’est pas déjà ouverte, ouvrez le **ModelExplorer Visual Studio Solution**.</span><span class="sxs-lookup"><span data-stu-id="d140e-210">If it's not already open, open the **ModelExplorer Visual Studio Solution**.</span></span>
  * <span data-ttu-id="d140e-211">(Si vous avez déjà créé/déployé ce projet dans Visual Studio pendant l’installation, puis vous pouvez ouvrir qu’une instance de Visual Studio et cliquez sur « Recharger All » lorsque vous y êtes invité).</span><span class="sxs-lookup"><span data-stu-id="d140e-211">(If you already built/deployed this project in Visual Studio during set-up, then you can open that instance of VS and click 'Reload All' when prompted).</span></span>
* <span data-ttu-id="d140e-212">Dans Visual Studio, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="d140e-212">In Visual Studio, click **Debug -> Start Without debugging** or press **Ctrl + F5**.</span></span>
* <span data-ttu-id="d140e-213">Une fois que l’application se déploie sur le HoloLens, faire disparaître le fitbox à l’aide du mouvement d’appui en l’air.</span><span class="sxs-lookup"><span data-stu-id="d140e-213">After the application deploys to the HoloLens, dismiss the fitbox using the air-tap gesture.</span></span>
* <span data-ttu-id="d140e-214">Déplacer votre main dans la vue et pointer votre doigt de l’index vers le ciel pour démarrer manuellement le suivi des.</span><span class="sxs-lookup"><span data-stu-id="d140e-214">Move your hand into view and point your index finger to the sky to start hand tracking.</span></span>
* <span data-ttu-id="d140e-215">Déplacer votre main gauche, droite, haut et bas.</span><span class="sxs-lookup"><span data-stu-id="d140e-215">Move your hand left, right, up and down.</span></span>
* <span data-ttu-id="d140e-216">Regardez comment quand le curseur prend la main est détectée et puis perdue à partir de la vue.</span><span class="sxs-lookup"><span data-stu-id="d140e-216">Watch how the cursor changes when your hand is detected and then lost from view.</span></span>
* <span data-ttu-id="d140e-217">Si vous êtes sur un casque immersif, vous devrez vous connecter et déconnecter votre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="d140e-217">If you're on an immersive headset, you'll have to connect and disconnect your controller.</span></span> <span data-ttu-id="d140e-218">Ces commentaires devient moins intéressants sur un appareil immersif, comme un contrôleur connecté sera toujours « disponible ».</span><span class="sxs-lookup"><span data-stu-id="d140e-218">This feedback becomes less interesting on an immersive device, as a connected controller will always be "available".</span></span>

## <a name="chapter-2---navigation"></a><span data-ttu-id="d140e-219">Chapitre 2 - Navigation</span><span class="sxs-lookup"><span data-stu-id="d140e-219">Chapter 2 - Navigation</span></span>

>[!VIDEO https://www.youtube.com/embed/sm-kxtKksSo]

### <a name="objectives"></a><span data-ttu-id="d140e-220">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d140e-220">Objectives</span></span>

* <span data-ttu-id="d140e-221">Utilisez les événements de mouvement de Navigation pour faire pivoter l’astronautes !.</span><span class="sxs-lookup"><span data-stu-id="d140e-221">Use Navigation gesture events to rotate the astronaut.</span></span>

### <a name="instructions"></a><span data-ttu-id="d140e-222">Instructions</span><span class="sxs-lookup"><span data-stu-id="d140e-222">Instructions</span></span>

<span data-ttu-id="d140e-223">Pour utiliser des gestes de Navigation dans notre application, nous allons modifier **GestureAction.cs** faire pivoter des objets quand le mouvement de Navigation se produit.</span><span class="sxs-lookup"><span data-stu-id="d140e-223">To use Navigation gestures in our app, we are going to edit **GestureAction.cs** to rotate objects when the Navigation gesture occurs.</span></span> <span data-ttu-id="d140e-224">En outre, nous allons ajouter des commentaires pour le curseur à afficher lorsque la Navigation est disponible.</span><span class="sxs-lookup"><span data-stu-id="d140e-224">Additionally, we'll add feedback to the cursor to display when Navigation is available.</span></span>

1. <span data-ttu-id="d140e-225">Dans le **hiérarchie** volet, développez **CursorWithFeedback**.</span><span class="sxs-lookup"><span data-stu-id="d140e-225">In the **Hierarchy** panel, expand **CursorWithFeedback**.</span></span>
2. <span data-ttu-id="d140e-226">Dans le **hologrammes** dossier, recherchez le **ScrollFeedback** actif.</span><span class="sxs-lookup"><span data-stu-id="d140e-226">In the **Holograms** folder, find the **ScrollFeedback** asset.</span></span>
3. <span data-ttu-id="d140e-227">Faites glisser et déposez le **ScrollFeedback** prefab sur le **CursorWithFeedback** GameObject dans le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d140e-227">Drag and drop the **ScrollFeedback** prefab onto the **CursorWithFeedback** GameObject in the **Hierarchy**.</span></span>
4. <span data-ttu-id="d140e-228">Cliquez sur **CursorWithFeedback**.</span><span class="sxs-lookup"><span data-stu-id="d140e-228">Click on **CursorWithFeedback**.</span></span>
5. <span data-ttu-id="d140e-229">Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="d140e-229">In the **Inspector** panel, click the **Add Component** button.</span></span>
6. <span data-ttu-id="d140e-230">Dans le menu, tapez dans la zone de recherche **CursorFeedback**.</span><span class="sxs-lookup"><span data-stu-id="d140e-230">In the menu, type in the search box **CursorFeedback**.</span></span> <span data-ttu-id="d140e-231">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="d140e-231">Select the search result.</span></span>
7. <span data-ttu-id="d140e-232">Faites glisser et déposez le **ScrollFeedback** à partir de l’objet le **hiérarchie** sur le **défilement détecté Game Object** propriété dans le **commentaire du curseur**composant dans le **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="d140e-232">Drag and drop the **ScrollFeedback** object from the **Hierarchy** onto the **Scroll Detected Game Object** property in the **Cursor Feedback** component in the **Inspector**.</span></span>
8. <span data-ttu-id="d140e-233">Dans le **hiérarchie** Panneau de configuration, sélectionnez le **AstroMan** objet.</span><span class="sxs-lookup"><span data-stu-id="d140e-233">In the **Hierarchy** panel, select the **AstroMan** object.</span></span>
9. <span data-ttu-id="d140e-234">Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="d140e-234">In the **Inspector** panel, click the **Add Component** button.</span></span>
10. <span data-ttu-id="d140e-235">Dans le menu, tapez dans la zone de recherche **mouvement Action**.</span><span class="sxs-lookup"><span data-stu-id="d140e-235">In the menu, type in the search box **Gesture Action**.</span></span> <span data-ttu-id="d140e-236">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="d140e-236">Select the search result.</span></span>

<span data-ttu-id="d140e-237">Ensuite, ouvrez **GestureAction.cs** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d140e-237">Next, open **GestureAction.cs** in Visual Studio.</span></span> <span data-ttu-id="d140e-238">De codage dans l’exercice 2.c, modifiez le script pour effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d140e-238">In coding exercise 2.c, edit the script to do the following:</span></span>

1. <span data-ttu-id="d140e-239">**Faire pivoter le AstroMan** objet chaque fois qu’un mouvement de Navigation est effectué.</span><span class="sxs-lookup"><span data-stu-id="d140e-239">**Rotate the AstroMan** object whenever a Navigation gesture is performed.</span></span>
2. <span data-ttu-id="d140e-240">Calculer le **rotationFactor** pour contrôler la quantité de rotation appliquée à l’objet.</span><span class="sxs-lookup"><span data-stu-id="d140e-240">Calculate the **rotationFactor** to control the amount of rotation applied to the object.</span></span>
3. <span data-ttu-id="d140e-241">**Faire pivoter l’objet** autour de l’axe des ordonnées lorsque l’utilisateur déplace la main gauche ou droite.</span><span class="sxs-lookup"><span data-stu-id="d140e-241">**Rotate the object** around the y-axis when the user moves their hand left or right.</span></span>

<span data-ttu-id="d140e-242">Codage complète exerce 2.c du script, ou remplacez le code par la solution terminée ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d140e-242">Complete coding exercises 2.c in the script, or replace the code with the completed solution below:</span></span>

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

<span data-ttu-id="d140e-243">Vous remarquerez que les autres événements de navigation sont déjà renseignés avec des informations.</span><span class="sxs-lookup"><span data-stu-id="d140e-243">You'll notice that the other navigation events are already filled in with some info.</span></span> <span data-ttu-id="d140e-244">Nous envoyons le GameObject sur le Kit de ressources pile modale de InputSystem, afin de l’utilisateur n’a pas à conserver le focus sur l’astronautes une fois la rotation a commencé.</span><span class="sxs-lookup"><span data-stu-id="d140e-244">We push the GameObject onto the Toolkit's InputSystem's modal stack, so the user doesn't have to maintain focus on the Astronaut once rotation has begun.</span></span> <span data-ttu-id="d140e-245">En conséquence, nous pop le GameObject la pile une fois que le geste est terminé.</span><span class="sxs-lookup"><span data-stu-id="d140e-245">Correspondingly, we pop the GameObject off the stack once the gesture is completed.</span></span>

### <a name="build-and-deploy"></a><span data-ttu-id="d140e-246">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="d140e-246">Build and Deploy</span></span>

1. <span data-ttu-id="d140e-247">Régénérez l’application dans Unity puis créer et déployer à partir de Visual Studio pour l’exécuter dans le HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d140e-247">Rebuild the application in Unity and then build and deploy from Visual Studio to run it in the HoloLens.</span></span>
2. <span data-ttu-id="d140e-248">Fixez du regard l’astronaut, deux flèches doivent apparaître sur chaque côté du curseur.</span><span class="sxs-lookup"><span data-stu-id="d140e-248">Gaze at the astronaut, two arrows should appear on either side of the cursor.</span></span> <span data-ttu-id="d140e-249">Ce nouvel élément visuel indique que l’astronautes peut être pivoté.</span><span class="sxs-lookup"><span data-stu-id="d140e-249">This new visual indicates that the astronaut can be rotated.</span></span>
3. <span data-ttu-id="d140e-250">Placez votre main dans la position de prête (votre index pointé vers le ciel) pour que la HoloLens puisse démarrer le suivi de votre main.</span><span class="sxs-lookup"><span data-stu-id="d140e-250">Place your hand in the ready position (index finger pointed towards the sky) so the HoloLens will start tracking your hand.</span></span>
4. <span data-ttu-id="d140e-251">Pour faire pivoter l’astronaut, réduire votre doigt de l’index à une position de pincement et puis déplacez la main gauche ou droite pour déclencher le mouvement NavigationX.</span><span class="sxs-lookup"><span data-stu-id="d140e-251">To rotate the astronaut, lower your index finger to a pinch position, and then move your hand left or right to trigger the NavigationX gesture.</span></span>

## <a name="chapter-3---hand-guidance"></a><span data-ttu-id="d140e-252">Chapitre 3 - conseils de main</span><span class="sxs-lookup"><span data-stu-id="d140e-252">Chapter 3 - Hand Guidance</span></span>

>[!VIDEO https://www.youtube.com/embed/ULzlVw4e14I]

### <a name="objectives"></a><span data-ttu-id="d140e-253">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d140e-253">Objectives</span></span>

* <span data-ttu-id="d140e-254">Utilisez **remettez le score de conseils** pour aider à prédire lorsque main suivi seront perdue.</span><span class="sxs-lookup"><span data-stu-id="d140e-254">Use **hand guidance score** to help predict when hand tracking will be lost.</span></span>
* <span data-ttu-id="d140e-255">Fournir **des commentaires sur le curseur** à afficher lorsque l’approche de bord de la caméra de vue main de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d140e-255">Provide **feedback on the cursor** to show when the user's hand nears the camera's edge of view.</span></span>

### <a name="instructions"></a><span data-ttu-id="d140e-256">Instructions</span><span class="sxs-lookup"><span data-stu-id="d140e-256">Instructions</span></span>

1. <span data-ttu-id="d140e-257">Dans le **hiérarchie** Panneau de configuration, sélectionnez le **CursorWithFeedback** objet.</span><span class="sxs-lookup"><span data-stu-id="d140e-257">In the **Hierarchy** panel, select the **CursorWithFeedback** object.</span></span>
2. <span data-ttu-id="d140e-258">Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="d140e-258">In the **Inspector** panel, click the **Add Component** button.</span></span>
3. <span data-ttu-id="d140e-259">Dans le menu, tapez dans la zone de recherche **main conseils**.</span><span class="sxs-lookup"><span data-stu-id="d140e-259">In the menu, type in the search box **Hand Guidance**.</span></span> <span data-ttu-id="d140e-260">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="d140e-260">Select the search result.</span></span>
4. <span data-ttu-id="d140e-261">Dans le **projet** panneau **hologrammes** dossier, recherchez le **HandGuidanceFeedback** asset.</span><span class="sxs-lookup"><span data-stu-id="d140e-261">In the **Project** panel **Holograms** folder, find the **HandGuidanceFeedback** asset.</span></span>
5. <span data-ttu-id="d140e-262">Faites glisser et déposez le **HandGuidanceFeedback** actif sur le **main conseils indicateur** propriété dans le **inspecteur** panneau.</span><span class="sxs-lookup"><span data-stu-id="d140e-262">Drag and drop the **HandGuidanceFeedback** asset onto the **Hand Guidance Indicator** property in the **Inspector** panel.</span></span>

### <a name="build-and-deploy"></a><span data-ttu-id="d140e-263">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="d140e-263">Build and Deploy</span></span>

* <span data-ttu-id="d140e-264">Régénérez l’application dans Unity puis créer et déployer à partir de Visual Studio pour profiter de l’application sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d140e-264">Rebuild the application in Unity and then build and deploy from Visual Studio to experience the app on HoloLens.</span></span>
* <span data-ttu-id="d140e-265">Afficher votre main dans la vue et déclencher votre doigt de l’index pour obtenir l’objet d’un suivi.</span><span class="sxs-lookup"><span data-stu-id="d140e-265">Bring your hand into view and raise your index finger to get tracked.</span></span>
* <span data-ttu-id="d140e-266">Démarrer la rotation du astronautes avec le mouvement de Navigation (pincement votre doigt de l’index et ensemble de curseur de défilement).</span><span class="sxs-lookup"><span data-stu-id="d140e-266">Start rotating the astronaut with the Navigation gesture (pinch your index finger and thumb together).</span></span>
* <span data-ttu-id="d140e-267">Déplacer votre main gauche, droite, haut et bas.</span><span class="sxs-lookup"><span data-stu-id="d140e-267">Move your hand far left, right, up, and down.</span></span>
* <span data-ttu-id="d140e-268">Lorsque votre main arrive à une flèche doit apparaître à côté du bord de l’image de mouvement, le curseur pour vous avertir que disponible de suivi seront perdu.</span><span class="sxs-lookup"><span data-stu-id="d140e-268">As your hand nears the edge of the gesture frame, an arrow should appear next to the cursor to warn you that hand tracking will be lost.</span></span> <span data-ttu-id="d140e-269">La flèche indique la direction pour déplacer votre main afin d’éviter de suivi à partir de la perte.</span><span class="sxs-lookup"><span data-stu-id="d140e-269">The arrow indicates which direction to move your hand in order to prevent tracking from being lost.</span></span>

## <a name="chapter-4---manipulation"></a><span data-ttu-id="d140e-270">Chapitre 4 - Manipulation</span><span class="sxs-lookup"><span data-stu-id="d140e-270">Chapter 4 - Manipulation</span></span>

>[!VIDEO https://www.youtube.com/embed/f3m8MvU60-I]

### <a name="objectives"></a><span data-ttu-id="d140e-271">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d140e-271">Objectives</span></span>

* <span data-ttu-id="d140e-272">Utiliser des événements de Manipulation pour déplacer l’astronaut avec vos mains.</span><span class="sxs-lookup"><span data-stu-id="d140e-272">Use Manipulation events to move the astronaut with your hands.</span></span>
* <span data-ttu-id="d140e-273">Fournir des commentaires sur le curseur pour informer l’utilisateur lors de la Manipulation peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="d140e-273">Provide feedback on the cursor to let the user know when Manipulation can be used.</span></span>

### <a name="instructions"></a><span data-ttu-id="d140e-274">Instructions</span><span class="sxs-lookup"><span data-stu-id="d140e-274">Instructions</span></span>

<span data-ttu-id="d140e-275">GestureManager.cs et AstronautManager.cs nous permettra d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d140e-275">GestureManager.cs and AstronautManager.cs will allow us to do the following:</span></span>

1. <span data-ttu-id="d140e-276">Utilisez le mot clé vocale »**Astronaut déplacer**» pour activer **Manipulation** mouvements et «**Astronaut faire pivoter**» pour les désactiver.</span><span class="sxs-lookup"><span data-stu-id="d140e-276">Use the speech keyword "**Move Astronaut**" to enable **Manipulation** gestures and "**Rotate Astronaut**" to disable them.</span></span>
2. <span data-ttu-id="d140e-277">Basculez vers la réponse à la **reconnaissance de mouvement de Manipulation**.</span><span class="sxs-lookup"><span data-stu-id="d140e-277">Switch to responding to the **Manipulation Gesture Recognizer**.</span></span>

<span data-ttu-id="d140e-278">Commençons.</span><span class="sxs-lookup"><span data-stu-id="d140e-278">Let's get started.</span></span>

1. <span data-ttu-id="d140e-279">Dans le **hiérarchie** panel, créer un nouveau GameObject vide.</span><span class="sxs-lookup"><span data-stu-id="d140e-279">In the **Hierarchy** panel, create a new empty GameObject.</span></span> <span data-ttu-id="d140e-280">Nommez-le «**AstronautManager**».</span><span class="sxs-lookup"><span data-stu-id="d140e-280">Name it "**AstronautManager**".</span></span>
2. <span data-ttu-id="d140e-281">Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="d140e-281">In the **Inspector** panel, click the **Add Component** button.</span></span>
3. <span data-ttu-id="d140e-282">Dans le menu, tapez dans la zone de recherche **Astronaut Manager**.</span><span class="sxs-lookup"><span data-stu-id="d140e-282">In the menu, type in the search box **Astronaut Manager**.</span></span> <span data-ttu-id="d140e-283">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="d140e-283">Select the search result.</span></span>
4. <span data-ttu-id="d140e-284">Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="d140e-284">In the **Inspector** panel, click the **Add Component** button.</span></span>
5. <span data-ttu-id="d140e-285">Dans le menu, tapez dans la zone de recherche **Source d’entrée vocale**.</span><span class="sxs-lookup"><span data-stu-id="d140e-285">In the menu, type in the search box **Speech Input Source**.</span></span> <span data-ttu-id="d140e-286">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="d140e-286">Select the search result.</span></span>

<span data-ttu-id="d140e-287">Nous allons maintenant ajouter les commandes vocales nécessaires pour contrôler l’état de l’interaction de l’astronaut.</span><span class="sxs-lookup"><span data-stu-id="d140e-287">We'll now add the speech commands required to control the interaction state of the astronaut.</span></span>

1. <span data-ttu-id="d140e-288">Développez le **mots clés** section dans le **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="d140e-288">Expand the **Keywords** section in the **Inspector**.</span></span>
2. <span data-ttu-id="d140e-289">Cliquez sur le **+** sur le côté droit pour ajouter un nouveau mot clé.</span><span class="sxs-lookup"><span data-stu-id="d140e-289">Click the **+** on the right hand side to add a new keyword.</span></span>
3. <span data-ttu-id="d140e-290">Tapez le mot clé en tant que **déplacer astronautes**.</span><span class="sxs-lookup"><span data-stu-id="d140e-290">Type the Keyword as **Move Astronaut**.</span></span> <span data-ttu-id="d140e-291">N’hésitez pas à ajouter un raccourci de la clé si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d140e-291">Feel free to add a Key Shortcut if desired.</span></span>
4. <span data-ttu-id="d140e-292">Cliquez sur le **+** sur le côté droit pour ajouter un nouveau mot clé.</span><span class="sxs-lookup"><span data-stu-id="d140e-292">Click the **+** on the right hand side to add a new keyword.</span></span>
5. <span data-ttu-id="d140e-293">Tapez le mot clé en tant que **pivoter astronautes**.</span><span class="sxs-lookup"><span data-stu-id="d140e-293">Type the Keyword as **Rotate Astronaut**.</span></span> <span data-ttu-id="d140e-294">N’hésitez pas à ajouter un raccourci de la clé si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d140e-294">Feel free to add a Key Shortcut if desired.</span></span>
6. <span data-ttu-id="d140e-295">Vous trouverez le code de gestionnaire correspondant dans **GestureAction.cs**, dans le **ISpeechHandler.OnSpeechKeywordRecognized** gestionnaire.</span><span class="sxs-lookup"><span data-stu-id="d140e-295">The corresponding handler code can be found in **GestureAction.cs**, in the **ISpeechHandler.OnSpeechKeywordRecognized** handler.</span></span>

![Comment configurer la Source d’entrée vocale pour chapitre 4](images/holograms211-speech.png)

<span data-ttu-id="d140e-297">Ensuite, nous allons configurer les commentaires de manipulation sur le curseur.</span><span class="sxs-lookup"><span data-stu-id="d140e-297">Next, we'll setup the manipulation feedback on the cursor.</span></span>

1. <span data-ttu-id="d140e-298">Dans le **projet** panneau **hologrammes** dossier, recherchez le **PathingFeedback** asset.</span><span class="sxs-lookup"><span data-stu-id="d140e-298">In the **Project** panel **Holograms** folder, find the **PathingFeedback** asset.</span></span>
2. <span data-ttu-id="d140e-299">Faites glisser et déposez le **PathingFeedback** prefab sur le **CursorWithFeedback** de l’objet dans le **hiérarchie**.</span><span class="sxs-lookup"><span data-stu-id="d140e-299">Drag and drop the **PathingFeedback** prefab onto the **CursorWithFeedback** object in the **Hierarchy**.</span></span>
3. <span data-ttu-id="d140e-300">Dans le **hiérarchie** du panneau, cliquez sur **CursorWithFeedback**.</span><span class="sxs-lookup"><span data-stu-id="d140e-300">In the **Hierarchy** panel, click on **CursorWithFeedback**.</span></span>
4. <span data-ttu-id="d140e-301">Faites glisser et déposez le **PathingFeedback** à partir de l’objet le **hiérarchie** sur le **chemins détecté Game Object** propriété dans le **commentaire du curseur**composant dans le **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="d140e-301">Drag and drop the **PathingFeedback** object from the **Hierarchy** onto the **Pathing Detected Game Object** property in the **Cursor Feedback** component in the **Inspector**.</span></span>

<span data-ttu-id="d140e-302">Nous devons à présent ajouter de code **GestureAction.cs** pour activer les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d140e-302">Now we need to add code to **GestureAction.cs** to enable the following:</span></span>

1. <span data-ttu-id="d140e-303">Ajouter du code pour le **IManipulationHandler.OnManipulationUpdated** (fonction), qui déplacera l’astronautes lorsqu’un **Manipulation** mouvement est détecté.</span><span class="sxs-lookup"><span data-stu-id="d140e-303">Add code to the **IManipulationHandler.OnManipulationUpdated** function, which will move the astronaut when a **Manipulation** gesture is detected.</span></span>
2. <span data-ttu-id="d140e-304">Calculer le **vecteur de mouvement** pour déterminer où l’astronautes doit être déplacé vers position de base disponible.</span><span class="sxs-lookup"><span data-stu-id="d140e-304">Calculate the **movement vector** to determine where the astronaut should be moved to based on hand position.</span></span>
3. <span data-ttu-id="d140e-305">**Déplacer** l’astronautes vers la nouvelle position.</span><span class="sxs-lookup"><span data-stu-id="d140e-305">**Move** the astronaut to the new position.</span></span>

<span data-ttu-id="d140e-306">Codage complète exercice 4.a dans **GestureAction.cs**, ou utiliser notre solution terminée ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d140e-306">Complete coding exercise 4.a in **GestureAction.cs**, or use our completed solution below:</span></span>

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

### <a name="build-and-deploy"></a><span data-ttu-id="d140e-307">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="d140e-307">Build and Deploy</span></span>

* <span data-ttu-id="d140e-308">Reconstruire dans Unity puis créer et déployer à partir de Visual Studio pour exécuter l’application dans HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d140e-308">Rebuild in Unity and then build and deploy from Visual Studio to run the app in HoloLens.</span></span>
* <span data-ttu-id="d140e-309">Déplacer votre main devant le HoloLens et déclencher votre doigt de l’index afin qu’il peut être suivi.</span><span class="sxs-lookup"><span data-stu-id="d140e-309">Move your hand in front of the HoloLens and raise your index finger so that it can be tracked.</span></span>
* <span data-ttu-id="d140e-310">Concentrer le curseur sur l’astronautes !.</span><span class="sxs-lookup"><span data-stu-id="d140e-310">Focus the cursor over the astronaut.</span></span>
* <span data-ttu-id="d140e-311">Par exemple « Déplacer Astronaut » pour déplacer l’astronaut avec un mouvement de Manipulation.</span><span class="sxs-lookup"><span data-stu-id="d140e-311">Say 'Move Astronaut' to move the astronaut with a Manipulation gesture.</span></span>
* <span data-ttu-id="d140e-312">Quatre flèches doivent apparaître autour du curseur pour indiquer que le programme maintenant répondront aux événements de Manipulation.</span><span class="sxs-lookup"><span data-stu-id="d140e-312">Four arrows should appear around the cursor to indicate that the program will now respond to Manipulation events.</span></span>
* <span data-ttu-id="d140e-313">Réduire votre doigt index jusqu'à votre curseur et de les pincés ensemble.</span><span class="sxs-lookup"><span data-stu-id="d140e-313">Lower your index finger down to your thumb, and keep them pinched together.</span></span>
* <span data-ttu-id="d140e-314">Lorsque vous déplacez votre main sur, l’astronaut déplacera trop (il s’agit de Manipulation).</span><span class="sxs-lookup"><span data-stu-id="d140e-314">As you move your hand around, the astronaut will move too (this is Manipulation).</span></span>
* <span data-ttu-id="d140e-315">Déclencher votre doigt de l’index pour arrêter de manipuler l’astronautes !.</span><span class="sxs-lookup"><span data-stu-id="d140e-315">Raise your index finger to stop manipulating the astronaut.</span></span>
* <span data-ttu-id="d140e-316">Remarque: Si vous ne dites pas « Déplacer astronautes ! » avant de passer votre main, le mouvement de Navigation sera utilisé à la place.</span><span class="sxs-lookup"><span data-stu-id="d140e-316">Note: If you do not say 'Move Astronaut' before moving your hand, then the Navigation gesture will be used instead.</span></span>
* <span data-ttu-id="d140e-317">Par exemple « Faire pivoter des Astronaut » pour revenir à l’état rotatif.</span><span class="sxs-lookup"><span data-stu-id="d140e-317">Say 'Rotate Astronaut' to return to the rotatable state.</span></span>

## <a name="chapter-5---model-expansion"></a><span data-ttu-id="d140e-318">Chapitre 5 - expansion de modèle</span><span class="sxs-lookup"><span data-stu-id="d140e-318">Chapter 5 - Model expansion</span></span>

>[!VIDEO https://www.youtube.com/embed/dA11P4P0VO8]

### <a name="objectives"></a><span data-ttu-id="d140e-319">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d140e-319">Objectives</span></span>

* <span data-ttu-id="d140e-320">Développez le modèle astronautes en plusieurs, en plus petits éléments que l’utilisateur peut interagir avec.</span><span class="sxs-lookup"><span data-stu-id="d140e-320">Expand the Astronaut model into multiple, smaller pieces that the user can interact with.</span></span>
* <span data-ttu-id="d140e-321">Déplacez chaque élément individuellement à l’aide de la Navigation et Manipulation de mouvements.</span><span class="sxs-lookup"><span data-stu-id="d140e-321">Move each piece individually using Navigation and Manipulation gestures.</span></span>

### <a name="instructions"></a><span data-ttu-id="d140e-322">Instructions</span><span class="sxs-lookup"><span data-stu-id="d140e-322">Instructions</span></span>

<span data-ttu-id="d140e-323">Dans cette section, nous allez effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="d140e-323">In this section, we will accomplish the following tasks:</span></span>

1. <span data-ttu-id="d140e-324">Ajouter un nouveau mot clé «**modèle développez**» pour développer le modèle astronautes !.</span><span class="sxs-lookup"><span data-stu-id="d140e-324">Add a new keyword "**Expand Model**" to expand the astronaut model.</span></span>
2. <span data-ttu-id="d140e-325">Ajouter un nouveau mot clé «**modèle réinitialiser**» pour renvoyer le modèle dans sa forme d’origine.</span><span class="sxs-lookup"><span data-stu-id="d140e-325">Add a new Keyword "**Reset Model**" to return the model to its original form.</span></span>

<span data-ttu-id="d140e-326">Pour ce faire, nous allons ajouter deux autres mots clés à la Source d’entrée vocale dans le chapitre précédent.</span><span class="sxs-lookup"><span data-stu-id="d140e-326">We'll do this by adding two more keywords to the Speech Input Source from the previous chapter.</span></span> <span data-ttu-id="d140e-327">Nous illustrerons également une autre façon de gérer les événements de reconnaissance.</span><span class="sxs-lookup"><span data-stu-id="d140e-327">We'll also demonstrate another way to handle recognition events.</span></span>

1. <span data-ttu-id="d140e-328">Cliquez sur précédent dans **AstronautManager** dans le **inspecteur** et développez le **mots clés** section dans le **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="d140e-328">Click back on **AstronautManager** in the **Inspector** and expand the **Keywords** section in the **Inspector**.</span></span>
2. <span data-ttu-id="d140e-329">Cliquez sur le **+** sur le côté droit pour ajouter un nouveau mot clé.</span><span class="sxs-lookup"><span data-stu-id="d140e-329">Click the **+** on the right hand side to add a new keyword.</span></span>
3. <span data-ttu-id="d140e-330">Tapez le mot clé en tant que **développez modèle**.</span><span class="sxs-lookup"><span data-stu-id="d140e-330">Type the Keyword as **Expand Model**.</span></span> <span data-ttu-id="d140e-331">N’hésitez pas à ajouter un raccourci de la clé si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d140e-331">Feel free to add a Key Shortcut if desired.</span></span>
4. <span data-ttu-id="d140e-332">Cliquez sur le **+** sur le côté droit pour ajouter un nouveau mot clé.</span><span class="sxs-lookup"><span data-stu-id="d140e-332">Click the **+** on the right hand side to add a new keyword.</span></span>
5. <span data-ttu-id="d140e-333">Tapez le mot clé en tant que **réinitialiser modèle**.</span><span class="sxs-lookup"><span data-stu-id="d140e-333">Type the Keyword as **Reset Model**.</span></span> <span data-ttu-id="d140e-334">N’hésitez pas à ajouter un raccourci de la clé si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d140e-334">Feel free to add a Key Shortcut if desired.</span></span>
6. <span data-ttu-id="d140e-335">Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.</span><span class="sxs-lookup"><span data-stu-id="d140e-335">In the **Inspector** panel, click the **Add Component** button.</span></span>
7. <span data-ttu-id="d140e-336">Dans le menu, tapez dans la zone de recherche **Gestionnaire d’entrée vocale**.</span><span class="sxs-lookup"><span data-stu-id="d140e-336">In the menu, type in the search box **Speech Input Handler**.</span></span> <span data-ttu-id="d140e-337">Sélectionnez le résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="d140e-337">Select the search result.</span></span>
8. <span data-ttu-id="d140e-338">Vérifiez **est un écouteur Global**, étant donné que nous voulons que ces commandes fonctionnent, quel que soit le GameObject, nous allons aborder.</span><span class="sxs-lookup"><span data-stu-id="d140e-338">Check **Is Global Listener**, since we want these commands to work regardless of the GameObject we're focusing.</span></span>
9. <span data-ttu-id="d140e-339">Cliquez sur le **+** bouton et sélectionnez **développez un modèle** dans la liste déroulante de mot clé.</span><span class="sxs-lookup"><span data-stu-id="d140e-339">Click the **+** button and select **Expand Model** from the Keyword dropdown.</span></span>
10. <span data-ttu-id="d140e-340">Cliquez sur le **+** sous réponse, puis faites glisser le **AstronautManager** à partir de la **hiérarchie** dans le **None (objet)** champ.</span><span class="sxs-lookup"><span data-stu-id="d140e-340">Click the **+** under Response, and drag the **AstronautManager** from the **Hierarchy** into the **None (Object)** field.</span></span>
11. <span data-ttu-id="d140e-341">Maintenant, cliquez sur le **aucune fonction** liste déroulante, sélectionnez **AstronautManager**, puis **ExpandModelCommand**.</span><span class="sxs-lookup"><span data-stu-id="d140e-341">Now, click the **No Function** dropdown, select **AstronautManager**, then **ExpandModelCommand**.</span></span>
12. <span data-ttu-id="d140e-342">Cliquez sur le Gestionnaire d’entrée vocale **+** bouton et sélectionnez **modèle réinitialiser** dans la liste déroulante de mot clé.</span><span class="sxs-lookup"><span data-stu-id="d140e-342">Click the Speech Input Handler's **+** button and select **Reset Model** from the Keyword dropdown.</span></span>
13. <span data-ttu-id="d140e-343">Cliquez sur le **+** sous réponse, puis faites glisser le **AstronautManager** à partir de la **hiérarchie** dans le **None (objet)** champ.</span><span class="sxs-lookup"><span data-stu-id="d140e-343">Click the **+** under Response, and drag the **AstronautManager** from the **Hierarchy** into the **None (Object)** field.</span></span>
14. <span data-ttu-id="d140e-344">Maintenant, cliquez sur le **aucune fonction** liste déroulante, sélectionnez **AstronautManager**, puis **ResetModelCommand**.</span><span class="sxs-lookup"><span data-stu-id="d140e-344">Now, click the **No Function** dropdown, select **AstronautManager**, then **ResetModelCommand**.</span></span>

![Comment configurer la Source d’entrée vocale et de gestionnaire pour le chapitre 5](images/holograms211-speechhandler.png)

### <a name="build-and-deploy"></a><span data-ttu-id="d140e-346">Générer et déployer</span><span class="sxs-lookup"><span data-stu-id="d140e-346">Build and Deploy</span></span>

* <span data-ttu-id="d140e-347">Essayez !</span><span class="sxs-lookup"><span data-stu-id="d140e-347">Try it!</span></span> <span data-ttu-id="d140e-348">Générer et déployer l’application sur le HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d140e-348">Build and deploy the app to the HoloLens.</span></span>
* <span data-ttu-id="d140e-349">Par exemple **modèle développez** pour voir le modèle astronaut développée.</span><span class="sxs-lookup"><span data-stu-id="d140e-349">Say **Expand Model** to see the expanded astronaut model.</span></span>
* <span data-ttu-id="d140e-350">Utilisez **Navigation** pour faire pivoter des éléments individuels de la couleur astronautes !.</span><span class="sxs-lookup"><span data-stu-id="d140e-350">Use **Navigation** to rotate individual pieces of the astronaut suit.</span></span>
* <span data-ttu-id="d140e-351">Par exemple **Astronaut déplacer** , puis utilisez **Manipulation** pour déplacer des éléments individuels de la couleur astronautes !.</span><span class="sxs-lookup"><span data-stu-id="d140e-351">Say **Move Astronaut** and then use **Manipulation** to move individual pieces of the astronaut suit.</span></span>
* <span data-ttu-id="d140e-352">Par exemple **Astronaut pivoter** pour faire pivoter les éléments à nouveau.</span><span class="sxs-lookup"><span data-stu-id="d140e-352">Say **Rotate Astronaut** to rotate the pieces again.</span></span>
* <span data-ttu-id="d140e-353">Par exemple **modèle réinitialiser** pour retourner l’astronaut à sa forme d’origine.</span><span class="sxs-lookup"><span data-stu-id="d140e-353">Say **Reset Model** to return the astronaut to its original form.</span></span>

## <a name="the-end"></a><span data-ttu-id="d140e-354">La fin</span><span class="sxs-lookup"><span data-stu-id="d140e-354">The End</span></span>

<span data-ttu-id="d140e-355">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="d140e-355">Congratulations!</span></span> <span data-ttu-id="d140e-356">Vous avez maintenant terminé **211 d’entrée M. : Mouvement**.</span><span class="sxs-lookup"><span data-stu-id="d140e-356">You have now completed **MR Input 211: Gesture**.</span></span>

* <span data-ttu-id="d140e-357">Vous savez comment détecter et répondre pour transmettre les événements de suivi, de navigation et de manipulation.</span><span class="sxs-lookup"><span data-stu-id="d140e-357">You know how to detect and respond to hand tracking, navigation and manipulation events.</span></span>
* <span data-ttu-id="d140e-358">Vous comprenez la différence entre les mouvements de Navigation et de Manipulation.</span><span class="sxs-lookup"><span data-stu-id="d140e-358">You understand the difference between Navigation and Manipulation gestures.</span></span>
* <span data-ttu-id="d140e-359">Vous savez comment modifier le curseur pour fournir des commentaires visuels quand une main est détectée, quand une main est sur le point d’être perdus et lorsqu’un objet prend en charge des interactions (Navigation vs Manipulation).</span><span class="sxs-lookup"><span data-stu-id="d140e-359">You know how to change the cursor to provide visual feedback for when a hand is detected, when a hand is about to be lost, and for when an object supports different interactions (Navigation vs Manipulation).</span></span>
