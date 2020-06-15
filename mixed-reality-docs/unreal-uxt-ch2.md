---
title: 2. Initialisation de votre projet et de votre première application
description: Deuxième tutoriel d’une série de six tutoriels, dans lequel vous apprenez à créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in UX Tools du Mixed Reality Toolkit
author: hferrone
ms.author: v-haferr
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: e8f03a87ec6b92e4c62cf3f88f519146254e7387
ms.sourcegitcommit: 1b8090ba6aed9ff128e4f32d40c96fac2e6a220b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330337"
---
# <a name="2-initializing-your-project-and-first-application"></a><span data-ttu-id="d769c-104">2. Initialisation de votre projet et de votre première application</span><span class="sxs-lookup"><span data-stu-id="d769c-104">2. Initializing your project and first application</span></span>

## <a name="overview"></a><span data-ttu-id="d769c-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="d769c-105">Overview</span></span>

<span data-ttu-id="d769c-106">Dans ce premier tutoriel, vous allez démarrer avec une nouvelle application Unreal pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="d769c-106">In this first tutorial, you'll get started with a new Unreal application for HoloLens 2.</span></span> <span data-ttu-id="d769c-107">Vous allez également ajouter le plug-in HoloLens, créer et éclairer un niveau, puis le remplir avec un échiquier et une pièce de jeu d’échecs.</span><span class="sxs-lookup"><span data-stu-id="d769c-107">This is going to include adding the HoloLens plugin, creating and lighting a level, and populating it with a game board and chess piece.</span></span> <span data-ttu-id="d769c-108">Vous allez utiliser des ressources prédéfinies pour la pièce 3D et les matériaux d’objet, donc vous n’avez pas de modélisation ex nihilo à faire.</span><span class="sxs-lookup"><span data-stu-id="d769c-108">You'll be using pre-made assets for the 3D chess piece and object materials, so don't worry about modeling anything from scratch.</span></span> <span data-ttu-id="d769c-109">D’ici la fin de ce tutoriel, vous disposerez d’une zone de dessin vide prête pour la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="d769c-109">By the end of this tutorial you'll have a blank canvas that's ready for mixed reality.</span></span>

<span data-ttu-id="d769c-110">Avant de continuer, vérifiez que vous avez tous les prérequis mentionnés dans la page [Bien démarrer](https://docs.microsoft.com/windows/mixed-reality/unreal-uxt-ch1).</span><span class="sxs-lookup"><span data-stu-id="d769c-110">Before continuing, make sure you have all the prerequisite from the [Getting Started](https://docs.microsoft.com/windows/mixed-reality/unreal-uxt-ch1) page.</span></span>

## <a name="objectives"></a><span data-ttu-id="d769c-111">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d769c-111">Objectives</span></span>
* <span data-ttu-id="d769c-112">Configuration d’un projet Unreal pour le développement HoloLens</span><span class="sxs-lookup"><span data-stu-id="d769c-112">Configuring an Unreal projet for HoloLens development</span></span>
* <span data-ttu-id="d769c-113">Importation de ressources et configuration d’une scène</span><span class="sxs-lookup"><span data-stu-id="d769c-113">Importing assets and setting up a scene</span></span>
* <span data-ttu-id="d769c-114">Création d’acteurs et d’événements au niveau du script avec des blueprints</span><span class="sxs-lookup"><span data-stu-id="d769c-114">Creating Actors and script-level events with blueprints</span></span>

## <a name="creating-a-new-unreal-project"></a><span data-ttu-id="d769c-115">Création d’un projet Unreal</span><span class="sxs-lookup"><span data-stu-id="d769c-115">Creating a new Unreal project</span></span>
<span data-ttu-id="d769c-116">La première chose dont vous avez besoin est un projet avec lequel travailler.</span><span class="sxs-lookup"><span data-stu-id="d769c-116">The first thing you need is a project to work with.</span></span>

1. <span data-ttu-id="d769c-117">Lancer Unreal Engine</span><span class="sxs-lookup"><span data-stu-id="d769c-117">Launch Unreal Engine</span></span>

2. <span data-ttu-id="d769c-118">Sélectionnez **Games** dans **New Project Categories**, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="d769c-118">Select **Games** in **New Project Categories** and click **Next**.</span></span> 

![Sélectionner le modèle de projet Games](images/unreal-uxt/2-gamestemplate.png)

3. <span data-ttu-id="d769c-120">Sélectionnez le modèle **Blank**, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="d769c-120">Select the **Blank** Template and click **Next**.</span></span> 

![Sélectionner le modèle Blank](images/unreal-uxt/2-template.PNG)

4. <span data-ttu-id="d769c-122">Définissez **C++** , **Scalable 3D or 2D, Mobile/Tablet** et **No Starter Content** dans **Project Settings**.</span><span class="sxs-lookup"><span data-stu-id="d769c-122">Set **C++**, **Scalable 3D or 2D, Mobile/Tablet**, and **No Starter Content** as your **Project Settings**.</span></span> 
    * <span data-ttu-id="d769c-123">Choisissez un emplacement d’enregistrement, puis cliquez sur **Create Project**.</span><span class="sxs-lookup"><span data-stu-id="d769c-123">Choose a save location and click **Create Project**.</span></span> 

![Paramètres du projet initial](images/unreal-uxt/2-project-settings.PNG)

<span data-ttu-id="d769c-125">Le projet doit s’ouvrir automatiquement dans l’éditeur Unreal, ce qui signifie que vous êtes prêt à passer à la section suivante.</span><span class="sxs-lookup"><span data-stu-id="d769c-125">The project should open up automatically in the Unreal editor, which means you're ready for the next section.</span></span>

## <a name="enabling-required-plugins"></a><span data-ttu-id="d769c-126">Activation des plug-ins nécessaires</span><span class="sxs-lookup"><span data-stu-id="d769c-126">Enabling required plugins</span></span>
<span data-ttu-id="d769c-127">Avant de commencer à ajouter des objets à la scène, vous avez besoin d’activer deux plug-ins.</span><span class="sxs-lookup"><span data-stu-id="d769c-127">Before you start adding objects to the scene you'll need to enable two plugins.</span></span>

1. <span data-ttu-id="d769c-128">Ouvrez **Edit > Plugins** et sélectionnez **Augmented Reality** dans la liste des options prédéfinies.</span><span class="sxs-lookup"><span data-stu-id="d769c-128">Open **Edit > Plugins** and select **Augmented Reality** from the built-in options list.</span></span> 
    * <span data-ttu-id="d769c-129">Faites défiler la liste jusqu’à **HoloLens** et cochez la case **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="d769c-129">Scroll down to **HoloLens** and check **Enabled**.</span></span> 

![Activation des plug-ins HoloLens](images/unreal-uxt/2-plugins.PNG)

2. <span data-ttu-id="d769c-131">Sélectionnez **Virtual Reality** dans la liste des options prédéfinies.</span><span class="sxs-lookup"><span data-stu-id="d769c-131">Select **Virtual Reality** from the built-in options list.</span></span> 
    * <span data-ttu-id="d769c-132">Faites défiler la liste jusqu’à **Microsoft Windows Mixed Reality**, cochez la case **Enabled**, puis redémarrez votre éditeur.</span><span class="sxs-lookup"><span data-stu-id="d769c-132">Scroll down to **Microsoft Windows Mixed Reality**., check **Enabled**, and restart your editor.</span></span> 

![Activation du plug-in Windows Mixed Reality](images/unreal-uxt/2-virtual-reality-plugin.PNG)

> [!NOTE]
> <span data-ttu-id="d769c-134">Les deux plug-ins sont nécessaires pour le développement HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="d769c-134">Both plugins are required for HoloLens 2 development.</span></span>

<span data-ttu-id="d769c-135">Une fois que vous avez terminé, votre niveau vide est prêt à avoir de la compagnie.</span><span class="sxs-lookup"><span data-stu-id="d769c-135">With that done you're empty level is ready for company.</span></span>

## <a name="creating-a-level"></a><span data-ttu-id="d769c-136">Création d’un niveau</span><span class="sxs-lookup"><span data-stu-id="d769c-136">Creating a level</span></span>
<span data-ttu-id="d769c-137">La tâche suivante consiste à créer une configuration de joueur simple avec un point de départ et un cube à des fins de référence et de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="d769c-137">Your next task is to create a simple player setup with a starting point and a cube for reference and scale.</span></span>

1. <span data-ttu-id="d769c-138">Sélectionnez **File > New Level**, puis choisissez **Empty Level**.</span><span class="sxs-lookup"><span data-stu-id="d769c-138">Select **File > New Level** and choose **Empty Level**.</span></span> <span data-ttu-id="d769c-139">La scène par défaut dans la fenêtre d’affichage doit maintenant être vide.</span><span class="sxs-lookup"><span data-stu-id="d769c-139">The default scene in the viewport should now be empty.</span></span>

2. <span data-ttu-id="d769c-140">Sélectionnez **Basic** sous l’onglet **Modes**, puis faites glisser **PlayerStart** dans la scène.</span><span class="sxs-lookup"><span data-stu-id="d769c-140">Select **Basic** from the **Modes** tab and drag **PlayerStart** into the scene.</span></span> 
    * <span data-ttu-id="d769c-141">Affectez à **Location** les valeurs **X = 0**, **Y = 0** et **Z = 0** sous l’onglet **Details**. L’utilisateur se situe ainsi au centre de la scène quand l’application démarre.</span><span class="sxs-lookup"><span data-stu-id="d769c-141">Set **Location** to **X = 0**, **Y = 0**, and **Z = 0** in the **Details** tab. This sets the user at the center of the scene when the app starts up.</span></span>

![Fenêtre d’affichage avec PlayerStart](images/unreal-uxt/2-playerstart.PNG)

3. <span data-ttu-id="d769c-143">Faites glisser un **cube** à partir de l’onglet **Basic** dans la scène.</span><span class="sxs-lookup"><span data-stu-id="d769c-143">Drag a **Cube** from the **Basic** tab into the scene.</span></span> 
    * <span data-ttu-id="d769c-144">Affectez à **Location** les valeurs **X = 50**, **Y = 0** et **Z = 0**.</span><span class="sxs-lookup"><span data-stu-id="d769c-144">Set **Location** to **X = 50**, **Y = 0**, and **Z = 0**.</span></span> <span data-ttu-id="d769c-145">Le cube est alors placé à 50 cm du joueur au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="d769c-145">This positions the cube 50 cm away from the player at start time.</span></span> 
    * <span data-ttu-id="d769c-146">Affectez à **Scale** les valeurs **X = 0,2**, **Y = 0,2** et **Z = 0,2** pour réduire le cube.</span><span class="sxs-lookup"><span data-stu-id="d769c-146">Change **Scale** to **X = 0.2**, **Y = 0.2**, and **Z = 0.2** to shrink the cube down.</span></span> 

<span data-ttu-id="d769c-147">Le cube n’est pas visible, sauf si vous ajoutez une lumière à votre scène, ce qui constitue votre dernière tâche avant de tester la scène.</span><span class="sxs-lookup"><span data-stu-id="d769c-147">You won’t be able to see the cube unless you add a light to your scene, which is your last task before testing the scene.</span></span>

4. <span data-ttu-id="d769c-148">Passez à l’onglet **Lights** dans le panneau **Modes**, puis faites glisser un **Directional Light** dans la scène.</span><span class="sxs-lookup"><span data-stu-id="d769c-148">Switch to the **Lights** tab in the **Modes** panel and drag a **Directional Light** into the scene.</span></span> <span data-ttu-id="d769c-149">Placez la lumière au-dessus de **PlayerStart** pour pouvoir la voir.</span><span class="sxs-lookup"><span data-stu-id="d769c-149">Position the light above **PlayerStart** so you can see it.</span></span>

![Fenêtre d’affichage avec une lumière ajoutée](images/unreal-uxt/2-light.PNG)

5. <span data-ttu-id="d769c-151">Accédez à **File > Save Current**, nommez votre niveau **Main**, puis cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="d769c-151">Go to **File > Save Current**, name your level **Main**, and click **Save**.</span></span> 

<span data-ttu-id="d769c-152">Une fois la scène définie, appuyez sur **Play** dans la barre d’outils pour voir votre cube en action !</span><span class="sxs-lookup"><span data-stu-id="d769c-152">With the scene set, press **Play** in the toolbar to see your cube in action!</span></span> <span data-ttu-id="d769c-153">Lorsque vous avez fini d’admirer votre travail, appuyez sur **Échap** pour arrêter l’application.</span><span class="sxs-lookup"><span data-stu-id="d769c-153">When you're finished admiring your work, press **Esc** to stop the application.</span></span>

![Un cube dans la fenêtre d’affichage](images/unreal-uxt/2-cube.PNG)

<span data-ttu-id="d769c-155">Maintenant que la scène est configurée, vous pouvez commencer à y ajouter l’échiquier et la pièce pour compléter l’environnement de l’application.</span><span class="sxs-lookup"><span data-stu-id="d769c-155">Now that the scene is setup, you can start adding in the chess board and piece to round out the application environment.</span></span>

## <a name="importing-assets"></a><span data-ttu-id="d769c-156">Importation de ressources</span><span class="sxs-lookup"><span data-stu-id="d769c-156">Importing assets</span></span>
<span data-ttu-id="d769c-157">La scène a l’air un peu vide pour le moment, mais vous allez y remédier en important les ressources prêtes à l’emploi dans le projet.</span><span class="sxs-lookup"><span data-stu-id="d769c-157">The scene is looking a bit empty at the moment, but you'll fix that by importing the ready-made assets into the project.</span></span>

1. <span data-ttu-id="d769c-158">Téléchargez et décompressez le dossier des ressources [GitHub](https://github.com/microsoft/MixedReality-Unreal-Samples/blob/master/ChessApp/ChessAssets.7z).</span><span class="sxs-lookup"><span data-stu-id="d769c-158">Download and unzip the [GitHub](https://github.com/microsoft/MixedReality-Unreal-Samples/blob/master/ChessApp/ChessAssets.7z) assets folder.</span></span>

2. <span data-ttu-id="d769c-159">Cliquez sur **Add New > New Folder** à partir du **Content Browser** et nommez ce dossier **ChessAssets**.</span><span class="sxs-lookup"><span data-stu-id="d769c-159">Click **Add New > New Folder** from the **Content Browser** and name it **ChessAssets**.</span></span> 
    * <span data-ttu-id="d769c-160">Double-cliquez sur le nouveau dossier. C’est là que vous allez importer les ressources 3D.</span><span class="sxs-lookup"><span data-stu-id="d769c-160">Double-click the new folder - this is where you'll import the 3D assets.</span></span>

![Afficher ou masquer le panneau des sources](images/unreal-uxt/2-showhidesources.PNG)

3. <span data-ttu-id="d769c-162">Cliquez sur **Import** à partir du **Content Browser**, sélectionnez tous les éléments inclus dans le dossier des ressources décompressé, puis cliquez sur **Open**.</span><span class="sxs-lookup"><span data-stu-id="d769c-162">Click **Import** from the **Content Browser**, select all the items in the unzipped assets folder and click **Open**.</span></span> 
    * <span data-ttu-id="d769c-163">Ce dossier contient les maillages d’objets 3D pour l’échiquier et les pièces au format FBX, ainsi que les cartes de texture au format TGA que vous allez utiliser pour les matériaux.</span><span class="sxs-lookup"><span data-stu-id="d769c-163">This folder contains the 3D object meshes for the chess board and pieces in FBX format and texture maps in TGA format that you'll use to for materials.</span></span>  

4. <span data-ttu-id="d769c-164">Lorsque la fenêtre FBX Import Options s’affiche, développez la section **Material** et affectez à **Material Import Method** la valeur **Do Not Create Material**.</span><span class="sxs-lookup"><span data-stu-id="d769c-164">When the FBX Import Options window pops up, expand the **Material** section and change **Material Import Method** to **Do Not Create Material**.</span></span>
    * <span data-ttu-id="d769c-165">Cliquez sur **Import All**.</span><span class="sxs-lookup"><span data-stu-id="d769c-165">Click **Import All**.</span></span>

![Options d’importation FBX](images/unreal-uxt/2-nocreatemat.PNG)

<span data-ttu-id="d769c-167">C’est tout ce que vous devez faire pour les ressources.</span><span class="sxs-lookup"><span data-stu-id="d769c-167">That's all you need to do for the assets.</span></span> <span data-ttu-id="d769c-168">Votre prochaine série de tâches consiste à créer les composants de l’application avec des blueprints.</span><span class="sxs-lookup"><span data-stu-id="d769c-168">Your next set of tasks is to create the building blocks of the application with blueprints.</span></span>

## <a name="adding-blueprints"></a><span data-ttu-id="d769c-169">Ajout de blueprints</span><span class="sxs-lookup"><span data-stu-id="d769c-169">Adding blueprints</span></span>

1. <span data-ttu-id="d769c-170">Cliquez sur **Add New > New Folder** dans le **Content Browser** et nommez ce dossier **Content Browser**.</span><span class="sxs-lookup"><span data-stu-id="d769c-170">Click **Add New > New Folder** in the **Content Browser** and name it **Content Browser**.</span></span> 

> [!NOTE]
> <span data-ttu-id="d769c-171">Si vous ne connaissez pas les [blueprints](https://docs.unrealengine.com/en-US/Engine/Blueprints/index.html), il s’agit de ressources spéciales qui fournissent une interface basée sur des nœuds pour créer des types d’acteurs et d’événements au niveau des scripts.</span><span class="sxs-lookup"><span data-stu-id="d769c-171">If you're new to [blueprints](https://docs.unrealengine.com/en-US/Engine/Blueprints/index.html), they're special assets that provide a node-based interface for creating new types of Actors and script level events.</span></span> 

2. <span data-ttu-id="d769c-172">Double-cliquez dans le dossier **Blueprints**, puis cliquez avec le bouton droit et sélectionnez **Blueprint Class**.</span><span class="sxs-lookup"><span data-stu-id="d769c-172">Double-click into the **Blueprints** folder, then right-click and select **Blueprint Class**.</span></span>         
    * <span data-ttu-id="d769c-173">Sélectionnez **Actor** et nommez le blueprint **Board**.</span><span class="sxs-lookup"><span data-stu-id="d769c-173">Select **Actor** and name the blueprint **Board**.</span></span> 

![Sélectionner une classe parente pour votre blueprint](images/unreal-uxt/2-bpparent.PNG)

<span data-ttu-id="d769c-175">Le nouveau blueprint **Board** apparaît maintenant dans le dossier **Blueprints**, comme l’illustre la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="d769c-175">The new **Board** blueprint now shows up in the **Blueprints** folder as seen in the following screenshot.</span></span> 

![Le nouveau blueprint Board](images/unreal-uxt/2-bpboard.PNG)

<span data-ttu-id="d769c-177">Vous êtes fin prêt pour commencer à ajouter des matériaux aux objets créés.</span><span class="sxs-lookup"><span data-stu-id="d769c-177">You're all set to start adding materials to the created objects.</span></span>

## <a name="working-with-materials"></a><span data-ttu-id="d769c-178">Utilisation de matériaux</span><span class="sxs-lookup"><span data-stu-id="d769c-178">Working with materials</span></span>
<span data-ttu-id="d769c-179">Les objets que vous avez créés sont gris par défaut, ce qui n’est pas très agréable à regarder.</span><span class="sxs-lookup"><span data-stu-id="d769c-179">The objects you've created are default grey, which isn't much fun to look at.</span></span> <span data-ttu-id="d769c-180">L’ajout de matériaux et de maillages à vos objets constitue la dernière série de tâches de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="d769c-180">Adding materials and meshes to your objects is the last set of tasks in this tutorial.</span></span>

1. <span data-ttu-id="d769c-181">Double-cliquez sur **Board** pour ouvrir l’éditeur de blueprint.</span><span class="sxs-lookup"><span data-stu-id="d769c-181">Double-click **Board** to open the blueprint editor.</span></span> 

2. <span data-ttu-id="d769c-182">Cliquez sur **Add Component > Scene** dans le panneau **Components** et nommez le composant **Root**.</span><span class="sxs-lookup"><span data-stu-id="d769c-182">Click **Add Component > Scene** from the **Components** panel and name it **Root**.</span></span> <span data-ttu-id="d769c-183">Notez que **Root** apparaît en tant qu’enfant de **DefaultSceneRoot** dans la capture d’écran ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d769c-183">Notice that **Root** shows up as a child of **DefaultSceneRoot** in the screenshot below:</span></span>

![Remplacement de la racine](images/unreal-uxt/2-root-blueprint.PNG)


3. <span data-ttu-id="d769c-185">Cliquez et faites glisser **Root** sur **DefaultSceneRoot** pour le remplacer et vous débarrasser de la sphère dans la fenêtre d’affichage.</span><span class="sxs-lookup"><span data-stu-id="d769c-185">Click-and-drag **Root** onto **DefaultSceneRoot** to replace it and get rid of the sphere in the viewport.</span></span> 

![Remplacement de la racine](images/unreal-uxt/2-root.PNG)


4. <span data-ttu-id="d769c-187">Cliquez sur **Add Component > Static Mesh** dans le panneau **Components** et nommez le composant **SM_Board**.</span><span class="sxs-lookup"><span data-stu-id="d769c-187">Click **Add Component > Static Mesh** from the **Components** panel and name it **SM_Board**.</span></span> <span data-ttu-id="d769c-188">Il apparaît en tant qu’objet enfant sous **Root**.</span><span class="sxs-lookup"><span data-stu-id="d769c-188">It will appear as a child object under **Root**.</span></span>

![Ajout d’un maillage statique](images/unreal-uxt/2-sm-board.PNG)

4. <span data-ttu-id="d769c-190">Cliquez sur **SM_Board**, faites défiler la page jusqu’à la section **Static Mesh** du panneau **Details**, puis sélectionnez **ChessBoard** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="d769c-190">Click **SM_Board**, scroll down to the **Static Mesh** section of the **Details** panel, and select **ChessBoard** from the dropdown.</span></span> 

![Le maillage de l’échiquier dans la fenêtre d’affichage](images/unreal-uxt/2-sm-board-view.PNG)

5.  <span data-ttu-id="d769c-192">Toujours dans le panneau **Details**, développez la section **Materials** et cliquez sur **Create New Asset > Material** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="d769c-192">Still in the **Details** panel, expand the **Materials** section and click **Create New Asset > Material** from the dropdown.</span></span> 
    * <span data-ttu-id="d769c-193">Nommez le matériau **M_ChessBoard** et enregistrez-le dans le dossier **ChessAssets**.</span><span class="sxs-lookup"><span data-stu-id="d769c-193">Name the material **M_ChessBoard** and save it to the **ChessAssets** folder.</span></span> 

![Créer un matériau](images/unreal-uxt/2-newmat.PNG)

6.  <span data-ttu-id="d769c-195">Double-cliquez sur l’image du matériau **M_ChessBoard** pour ouvrir l’éditeur de matériau.</span><span class="sxs-lookup"><span data-stu-id="d769c-195">Double-click the **M_ChessBoard** material imaged to open the Material Editor.</span></span> 

![Ouvrir l’éditeur de matériau](images/unreal-uxt/2-material-editor.PNG)

7. <span data-ttu-id="d769c-197">Dans l’éditeur de matériau, cliquez avec le bouton droit et recherchez **Texture Sample**.</span><span class="sxs-lookup"><span data-stu-id="d769c-197">In the Material Editor, right-click and search for **Texture Sample**.</span></span> 
    * <span data-ttu-id="d769c-198">Développez la section **Material Expression Texture Base** dans le panneau **Details** et affectez à **Texture** la valeur **ChessBoard_Albedo**.</span><span class="sxs-lookup"><span data-stu-id="d769c-198">Expand the **Material Expression Texture Base** section in the **Details** panel and set **Texture** to **ChessBoard_Albedo**.</span></span> 
    * <span data-ttu-id="d769c-199">Faites glisser le repère de sortie **RGB** vers le repère Base Color de **M_ChessBoard**.</span><span class="sxs-lookup"><span data-stu-id="d769c-199">Drag the **RGB** output pin to the Base Color pin of **M_ChessBoard**.</span></span> 

![Définir la couleur de base](images/unreal-uxt/2-boardalbedomat.PNG)

8.  <span data-ttu-id="d769c-201">Répétez l’étape précédente quatre autres fois pour créer quatre autres nœuds **Texture Sample** avec les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="d769c-201">Repeat the previous step four more times to create four more **Texture Sample** nodes with the following settings:</span></span>
    * <span data-ttu-id="d769c-202">Affectez à **Texture** la valeur **ChessBoard_AO** et liez le repère **RGB** au repère **Ambient Occlusion**.</span><span class="sxs-lookup"><span data-stu-id="d769c-202">Set **Texture** to **ChessBoard_AO** and link the **RGB** to the **Ambient Occlusion** pin.</span></span>
    * <span data-ttu-id="d769c-203">Affectez à **Texture** la valeur **ChessBoard_Metal** et liez le repère **RGB** au repère **Metallic**.</span><span class="sxs-lookup"><span data-stu-id="d769c-203">Set **Texture** to **ChessBoard_Metal** and link the **RGB** to the **Metallic** pin.</span></span> 
    * <span data-ttu-id="d769c-204">Affectez à **Texture** la valeur **ChessBoard_Normal** et liez le repère **RGB** au repère **Normal**.</span><span class="sxs-lookup"><span data-stu-id="d769c-204">Set **Texture** to **ChessBoard_Normal** and link the **RGB** to the **Normal** pin.</span></span>
    * <span data-ttu-id="d769c-205">Affectez à **Texture** la valeur **ChessBoard_Rough** et liez le repère **RGB** au repère **Roughness**.</span><span class="sxs-lookup"><span data-stu-id="d769c-205">Set **Texture** to **ChessBoard_Rough** and link the **RGB** to the **Roughness** pin.</span></span> 
    * <span data-ttu-id="d769c-206">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d769c-206">Click **Save**.</span></span> 

![Raccorder les textures restantes](images/unreal-uxt/2-boardmat.PNG)

<span data-ttu-id="d769c-208">Avant de continuer, vérifiez que la configuration de votre matériau ressemble à la capture d’écran ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d769c-208">Make sure the your material setup looks like the above screenshot before continuing.</span></span>

## <a name="populating-the-scene"></a><span data-ttu-id="d769c-209">Remplissage de la scène</span><span class="sxs-lookup"><span data-stu-id="d769c-209">Populating the scene</span></span>
<span data-ttu-id="d769c-210">Si vous revenez au blueprint **Board**, vous voyez que le matériau que vous venez de créer a été appliqué.</span><span class="sxs-lookup"><span data-stu-id="d769c-210">If you go back to the **Board** blueprint, you'll see that the material you just created has been applied.</span></span> <span data-ttu-id="d769c-211">Il ne vous reste plus qu’à installer la scène !</span><span class="sxs-lookup"><span data-stu-id="d769c-211">All that's left is setting up the scene!</span></span> <span data-ttu-id="d769c-212">Pour commencer, modifiez les propriétés suivantes pour vous assurer que l’échiquier est de taille raisonnable et qu’il est correctement incliné lorsqu’il est placé dans la scène :</span><span class="sxs-lookup"><span data-stu-id="d769c-212">First, change the following properties to make sure the board is a reasonable size and angled correctly when it's placed in the scene:</span></span>
1.  <span data-ttu-id="d769c-213">Affectez à **Scale** la valeur **(0,05, 0,05, 0,05)** et à **Z Rotation** la valeur **90**.</span><span class="sxs-lookup"><span data-stu-id="d769c-213">Set **Scale** to **(0.05, 0.05, 0.05)** and **Z Rotation** to **90**.</span></span> 
    * <span data-ttu-id="d769c-214">Cliquez sur **Compile** dans la barre d’outils supérieure, puis sur **Save** pour revenir à la fenêtre Main.</span><span class="sxs-lookup"><span data-stu-id="d769c-214">Click **Compile** in the top toolbar, then **Save** and return to the Main window.</span></span> 

![Échiquier avec un matériau appliqué](images/unreal-uxt/2-chessboard.PNG)

2.  <span data-ttu-id="d769c-216">Cliquez avec le bouton droit sur **Cube > Edit > Delete**, puis faites glisser **Board** depuis le **Content Browser** dans la fenêtre d’affichage.</span><span class="sxs-lookup"><span data-stu-id="d769c-216">Right-click **Cube > Edit > Delete** and drag **Board** from the **Content Browser** into the viewport.</span></span> 
    * <span data-ttu-id="d769c-217">Affectez à **Location** les valeurs **X = 80**, **Y = 0** et **Z = -20**.</span><span class="sxs-lookup"><span data-stu-id="d769c-217">Set **Location** to **X = 80**, **Y = 0**, and **Z = -20**.</span></span> 

3.  <span data-ttu-id="d769c-218">Cliquez sur le bouton **Play** pour afficher votre nouvel échiquier dans le niveau.</span><span class="sxs-lookup"><span data-stu-id="d769c-218">Click the **Play** button to view your new board in the level.</span></span> <span data-ttu-id="d769c-219">Appuyez sur **Échap** pour revenir à l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="d769c-219">Press **Esc** to return to the editor.</span></span> 

<span data-ttu-id="d769c-220">À présent, vous allez suivre les mêmes étapes pour créer une pièce de jeu d’échecs que celles que vous avez effectuées pour l’échiquier :</span><span class="sxs-lookup"><span data-stu-id="d769c-220">Now you'll follow the same steps to create a chess piece as you did with the board:</span></span>

1. <span data-ttu-id="d769c-221">Accédez au dossier **Blueprints**, cliquez avec le bouton droit et sélectionnez **Blueprint Class**, puis choisissez **Actor**.</span><span class="sxs-lookup"><span data-stu-id="d769c-221">Go to the **Blueprints** folder, right-click and select **Blueprint Class** and choose **Actor**.</span></span> <span data-ttu-id="d769c-222">Nommez cet acteur **WhiteKing**.</span><span class="sxs-lookup"><span data-stu-id="d769c-222">Name the actor **WhiteKing**.</span></span>

2. <span data-ttu-id="d769c-223">Double-cliquez sur **WhiteKing** pour l’ouvrir dans l’éditeur de blueprint, cliquez sur **Add Component > Scene** et nommez-le **Root**.</span><span class="sxs-lookup"><span data-stu-id="d769c-223">Double click **WhiteKing** to open it in the Blueprint Editor, click **Add Component > Scene** and name it **Root**.</span></span> 
    * <span data-ttu-id="d769c-224">Glissez-déposez **Root** dans **DefaultSceneRoot** pour le remplacer.</span><span class="sxs-lookup"><span data-stu-id="d769c-224">Drag-and-drop **Root** onto **DefaultSceneRoot** to replace it.</span></span> 

3. <span data-ttu-id="d769c-225">Cliquez sur **Add Component > Static Mesh** et nommez ce composant **SM_King**.</span><span class="sxs-lookup"><span data-stu-id="d769c-225">Click **Add Component > Static Mesh** and name it **SM_King**.</span></span> 
    * <span data-ttu-id="d769c-226">Affectez à **Static Mesh** la valeur **Chess_King** et à **Material** la valeur d’un nouveau matériau appelé **M_ChessWhite** dans le panneau Details.</span><span class="sxs-lookup"><span data-stu-id="d769c-226">Set **Static Mesh** to **Chess_King** and **Material** to a new Material called **M_ChessWhite** in the Details panel.</span></span> 

4. <span data-ttu-id="d769c-227">Ouvrez **M_ChessWhite** dans l’éditeur de matériau et raccordez les nœuds **Texture Sample** suivants aux éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d769c-227">Open **M_ChessWhite** in the Material editor and hook up the following **Texture Sample** nodes to the following:</span></span>
    * <span data-ttu-id="d769c-228">Affectez à **Texture** la valeur **ChessWhite_AO** et liez le repère **RGB** au repère **Ambient Occlusion**.</span><span class="sxs-lookup"><span data-stu-id="d769c-228">Set **Texture** to **ChessWhite_AO** and link the **RGB** to the **Ambient Occlusion** pin.</span></span>
    * <span data-ttu-id="d769c-229">Affectez à **Texture** la valeur **ChessWhite_Metal** et liez le repère **RGB** au repère **Metallic**.</span><span class="sxs-lookup"><span data-stu-id="d769c-229">Set **Texture** to **ChessWhite_Metal** and link the **RGB** to the **Metallic** pin.</span></span> 
    * <span data-ttu-id="d769c-230">Affectez à **Texture** la valeur **ChessWhite_Normal** et liez le repère **RGB** au repère **Normal**.</span><span class="sxs-lookup"><span data-stu-id="d769c-230">Set **Texture** to **ChessWhite_Normal** and link the **RGB** to the **Normal** pin.</span></span>
    * <span data-ttu-id="d769c-231">Affectez à **Texture** la valeur **ChessWhite_Rough** et liez le repère **RGB** au repère **Roughness**.</span><span class="sxs-lookup"><span data-stu-id="d769c-231">Set **Texture** to **ChessWhite_Rough** and link the **RGB** to the **Roughness** pin.</span></span> 
    * <span data-ttu-id="d769c-232">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d769c-232">Click **Save**.</span></span> 

<span data-ttu-id="d769c-233">Votre matériau **M_ChessKing** doit ressembler à l’image suivante avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="d769c-233">Your **M_ChessKing** material should look like the following image before continuing.</span></span>

![Créer le matériau pour le roi](images/unreal-uxt/2-chesskingmat.PNG)

<span data-ttu-id="d769c-235">Vous y êtes presque, il vous suffit d’ajouter la nouvelle pièce à la scène :</span><span class="sxs-lookup"><span data-stu-id="d769c-235">You're almost there, just need to add the new chess piece into the scene:</span></span> 

1. <span data-ttu-id="d769c-236">Ouvrez le blueprint **WhiteKing** et affectez à **Scale** la valeur **(0,05, 0,05, 0,05)** et à **Z Rotation** la valeur **90**.</span><span class="sxs-lookup"><span data-stu-id="d769c-236">Open the **WhiteKing** blueprint and change the **Scale** to **(0.05, 0.05, 0.05)** and **Z Rotation** to **90**.</span></span>
    * <span data-ttu-id="d769c-237">Compilez et enregistrez votre blueprint, puis revenez à la fenêtre principale.</span><span class="sxs-lookup"><span data-stu-id="d769c-237">Compile and save your blueprint, then head back to the main window.</span></span> 

2.  <span data-ttu-id="d769c-238">Faites glisser **WhiteKing** dans la fenêtre d’affichage, basculez vers le panneau **World Outliner**, faites glisser **WhiteKing** sur **Board** pour en faire un objet enfant.</span><span class="sxs-lookup"><span data-stu-id="d769c-238">Drag **WhiteKing** into the viewport, switch to the **World Outliner** panel drag **WhiteKing** onto **Board** to make it a child object.</span></span>

![World Outliner](images/unreal-uxt/2-child.PNG)

3.  <span data-ttu-id="d769c-240">Dans le panneau **Details** sous **Transform**, affectez au paramètre **Location** de **WhiteKing** les valeurs **X = -26**, **Y = 4** et **Z = 0**.</span><span class="sxs-lookup"><span data-stu-id="d769c-240">In the **Details** panel under **Transform**, set **WhiteKing**'s **Location** to **X = -26**, **Y = 4**, and **Z = 0**.</span></span>

<span data-ttu-id="d769c-241">C’est terminé !</span><span class="sxs-lookup"><span data-stu-id="d769c-241">That's a wrap!</span></span> <span data-ttu-id="d769c-242">Cliquez sur **Play** pour voir à l’œuvre votre niveau rempli, puis appuyez sur **Échap** lorsque vous êtes prêt à fermer la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d769c-242">Click **Play** to see your populated level in action, and press **Esc** when you're ready to exit.</span></span> <span data-ttu-id="d769c-243">Ce tutoriel a abordé de nombreux points liés à la création d’un projet simple, mais votre projet est prêt à passer à la partie suivante de la série : la configuration pour la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="d769c-243">This tutorial covered a lot of ground creating a simple project, but your project is ready to move on to the next part of the series: setting up for mixed reality.</span></span> 

[<span data-ttu-id="d769c-244">Section suivante : 3. Configurer votre projet pour la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="d769c-244">Next Section: 3. Set up your project for mixed reality</span></span>](unreal-uxt-ch3.md)