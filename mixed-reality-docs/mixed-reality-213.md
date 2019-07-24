---
title: Entrée MR 213
description: Suivez ce didacticiel de codage avec Unity, Visual Studio et les casques immersifs pour apprendre les détails des contrôleurs de mouvement.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, immersion, contrôleur de mouvement, Academy, didacticiel
ms.openlocfilehash: 85449795a4fb3d182101cb5b4c4ce3fe85b009c0
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63516417"
---
>[!NOTE]
><span data-ttu-id="f777e-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="f777e-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="f777e-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="f777e-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="f777e-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="f777e-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="f777e-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f777e-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="f777e-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="f777e-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="f777e-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="f777e-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-input-213-motion-controllers"></a><span data-ttu-id="f777e-110">Monsieur 213: Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="f777e-110">MR Input 213: Motion controllers</span></span>

<span data-ttu-id="f777e-111">Les contrôleurs de mouvement dans le monde de la réalité mixte ajoutent un autre niveau d’interactivité.</span><span class="sxs-lookup"><span data-stu-id="f777e-111">Motion controllers in the mixed reality world add another level of interactivity.</span></span> <span data-ttu-id="f777e-112">Avec les contrôleurs de [mouvement](motion-controllers.md), nous pouvons interagir directement avec les objets de manière plus naturelle, de la même façon que nos interactions physiques en réel, en renforçant l’immersion et le plaisir de l’expérience de votre application.</span><span class="sxs-lookup"><span data-stu-id="f777e-112">With [motion controllers](motion-controllers.md), we can directly interact with objects in a more natural way, similar to our physical interactions in real life, increasing immersion and delight in your app experience.</span></span>

<span data-ttu-id="f777e-113">Dans l’entrée 213, nous explorerons les événements d’entrée du contrôleur de mouvement en créant une expérience de peinture spatiale simple.</span><span class="sxs-lookup"><span data-stu-id="f777e-113">In MR Input 213, we will explore the motion controller's input events by creating a simple spatial painting experience.</span></span> <span data-ttu-id="f777e-114">Avec cette application, les utilisateurs peuvent peindre dans un espace tridimensionnel avec différents types de pinceaux et de couleurs.</span><span class="sxs-lookup"><span data-stu-id="f777e-114">With this app, users can paint in three-dimensional space with various types of brushes and colors.</span></span>

## <a name="topics-covered-in-this-tutorial"></a><span data-ttu-id="f777e-115">Rubriques traitées dans ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="f777e-115">Topics covered in this tutorial</span></span>

|![MixedReality213 Topic1](images/mr213-topic1.png)|![MixedReality213 Topic2](images/mr213-topic2.png)|![MixedReality213 Topic3](images/mr213-topic3.png)|
| :--- | :--- | :--- |
|<span data-ttu-id="f777e-119">**Visualisation du contrôleur**</span><span class="sxs-lookup"><span data-stu-id="f777e-119">**Controller visualization**</span></span>|<span data-ttu-id="f777e-120">**Événements d’entrée du contrôleur**</span><span class="sxs-lookup"><span data-stu-id="f777e-120">**Controller input events**</span></span>|<span data-ttu-id="f777e-121">**Contrôleur personnalisé et interface utilisateur**</span><span class="sxs-lookup"><span data-stu-id="f777e-121">**Custom controller and UI**</span></span>|
|<span data-ttu-id="f777e-122">Découvrez comment restituer les modèles de contrôleur de mouvement dans le mode jeu et le runtime d’Unity.</span><span class="sxs-lookup"><span data-stu-id="f777e-122">Learn how to render motion controller models in Unity's game mode and runtime.</span></span>|<span data-ttu-id="f777e-123">Comprenez les différents types d’événements de bouton et leurs applications.</span><span class="sxs-lookup"><span data-stu-id="f777e-123">Understand different types of button events and their applications.</span></span>|<span data-ttu-id="f777e-124">Découvrez comment superposer des éléments d’interface utilisateur en plus du contrôleur ou le personnaliser entièrement.</span><span class="sxs-lookup"><span data-stu-id="f777e-124">Learn how to overlay UI elements on top of the controller or fully customize it.</span></span>|

## <a name="device-support"></a><span data-ttu-id="f777e-125">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="f777e-125">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="f777e-126">Course</span><span class="sxs-lookup"><span data-stu-id="f777e-126">Course</span></span></th><th style="width:150px"> <span data-ttu-id="f777e-127"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="f777e-127"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="f777e-128"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="f777e-128"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="f777e-129">Monsieur 213: Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="f777e-129">MR Input 213: Motion controllers</span></span></td><td style="text-align: center;"> </td><td style="text-align: center;"> <span data-ttu-id="f777e-130">✔️</span><span class="sxs-lookup"><span data-stu-id="f777e-130">✔️</span></span></td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="f777e-131">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f777e-131">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f777e-132">Prérequis</span><span class="sxs-lookup"><span data-stu-id="f777e-132">Prerequisites</span></span>

<span data-ttu-id="f777e-133">Consultez la liste de vérification de l’installation des casques immersifs sur [cette page](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="f777e-133">See the installation checklist for immersive headsets on [this page](install-the-tools.md).</span></span>

* <span data-ttu-id="f777e-134">Ce didacticiel nécessite [Unity 2017.2.1 P2](https://beta.unity3d.com/download/1dc514532f08/UnityDownloadAssistant-2017.2.1p2.exe)</span><span class="sxs-lookup"><span data-stu-id="f777e-134">This tutorial requires [Unity 2017.2.1p2](https://beta.unity3d.com/download/1dc514532f08/UnityDownloadAssistant-2017.2.1p2.exe)</span></span>

### <a name="project-files"></a><span data-ttu-id="f777e-135">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="f777e-135">Project files</span></span>

* <span data-ttu-id="f777e-136">[Téléchargez les fichiers](https://github.com/Microsoft/MixedReality213/archive/master.zip) requis par le projet et extrayez les fichiers sur le bureau.</span><span class="sxs-lookup"><span data-stu-id="f777e-136">[Download the files](https://github.com/Microsoft/MixedReality213/archive/master.zip) required by the project and extract the files to the Desktop.</span></span>

>[!NOTE]
><span data-ttu-id="f777e-137">Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/MixedReality213).</span><span class="sxs-lookup"><span data-stu-id="f777e-137">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/MixedReality213).</span></span>

## <a name="unity-setup"></a><span data-ttu-id="f777e-138">Configuration de Unity</span><span class="sxs-lookup"><span data-stu-id="f777e-138">Unity setup</span></span>

>[!VIDEO https://www.youtube.com/embed/cBAOALaHys4]

### <a name="objectives"></a><span data-ttu-id="f777e-139">Objectifs</span><span class="sxs-lookup"><span data-stu-id="f777e-139">Objectives</span></span>

* <span data-ttu-id="f777e-140">Optimiser Unity pour le développement Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="f777e-140">Optimize Unity for Windows Mixed Reality development</span></span>
* <span data-ttu-id="f777e-141">Configurer une caméra de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="f777e-141">Setup Mixed Reality Camera</span></span>
* <span data-ttu-id="f777e-142">Environnement d’installation</span><span class="sxs-lookup"><span data-stu-id="f777e-142">Setup environment</span></span>

### <a name="instructions"></a><span data-ttu-id="f777e-143">Instructions</span><span class="sxs-lookup"><span data-stu-id="f777e-143">Instructions</span></span>

* <span data-ttu-id="f777e-144">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="f777e-144">Start Unity.</span></span>
* <span data-ttu-id="f777e-145">Sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="f777e-145">Select **Open**.</span></span>
* <span data-ttu-id="f777e-146">Accédez à votre bureau et recherchez le dossier **MixedReality213-Master** que vous avez précédemment non archivé.</span><span class="sxs-lookup"><span data-stu-id="f777e-146">Navigate to your Desktop and find the **MixedReality213-master** folder you previously unarchived.</span></span>
* <span data-ttu-id="f777e-147">Cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="f777e-147">Click **Select Folder**.</span></span>
* <span data-ttu-id="f777e-148">Une fois que Unity a fini de charger les fichiers projet, vous pouvez voir l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="f777e-148">Once Unity finishes loading project files, you will be able to see Unity editor.</span></span>
* <span data-ttu-id="f777e-149">Dans Unity, sélectionnez **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="f777e-149">In Unity, select **File > Build Settings**.</span></span>

![MR213_BuildSettings](images/mr213-buildsettings-450px.png)
* <span data-ttu-id="f777e-151">Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur le bouton **changer de plateforme** .</span><span class="sxs-lookup"><span data-stu-id="f777e-151">Select **Universal Windows Platform** in the **Platform** list and click the **Switch Platform** button.</span></span>
* <span data-ttu-id="f777e-152">Définir un appareil cible sur **un appareil**</span><span class="sxs-lookup"><span data-stu-id="f777e-152">Set Target Device to **Any device**</span></span>
* <span data-ttu-id="f777e-153">Définir le type de build sur **D3D**</span><span class="sxs-lookup"><span data-stu-id="f777e-153">Set Build Type to **D3D**</span></span>
* <span data-ttu-id="f777e-154">Installer le SDK sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="f777e-154">Set SDK to **Latest Installed**</span></span>
* <span data-ttu-id="f777e-155">Vérifier **les C# projets Unity**</span><span class="sxs-lookup"><span data-stu-id="f777e-155">Check **Unity C# Projects**</span></span>
    * <span data-ttu-id="f777e-156">Cela vous permet de modifier les fichiers de script dans le projet Visual Studio sans reconstruire le projet Unity.</span><span class="sxs-lookup"><span data-stu-id="f777e-156">This allows you modify script files in the Visual Studio project without rebuilding Unity project.</span></span>
* <span data-ttu-id="f777e-157">Cliquez sur **paramètres du lecteur**.</span><span class="sxs-lookup"><span data-stu-id="f777e-157">Click **Player Settings**.</span></span>
* <span data-ttu-id="f777e-158">Dans le volet de l' **inspecteur** , faites défiler l’écran vers le bas</span><span class="sxs-lookup"><span data-stu-id="f777e-158">In the **Inspector** panel, scroll down to the bottom</span></span>
* <span data-ttu-id="f777e-159">Dans les paramètres XR, vérifiez **la réalité virtuelle prise en charge**</span><span class="sxs-lookup"><span data-stu-id="f777e-159">In XR Settings, check **Virtual Reality Supported**</span></span>
* <span data-ttu-id="f777e-160">Sous kits de développement logiciel (SDK) Virtual Reality, sélectionnez **Windows Mixed Reality** .</span><span class="sxs-lookup"><span data-stu-id="f777e-160">Under Virtual Reality SDKs, select **Windows Mixed Reality**</span></span>

![MR213_XRSettings](images/mr213-xrsettings-500px.png)
* <span data-ttu-id="f777e-162">Fermez la fenêtre **paramètres de build** .</span><span class="sxs-lookup"><span data-stu-id="f777e-162">Close **Build Settings** window.</span></span>

### <a name="project-structure"></a><span data-ttu-id="f777e-163">Structure de projet</span><span class="sxs-lookup"><span data-stu-id="f777e-163">Project structure</span></span>

<span data-ttu-id="f777e-164">Ce didacticiel utilise la **[réalité mixte Toolkit-Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity)** .</span><span class="sxs-lookup"><span data-stu-id="f777e-164">This tutorial uses **[Mixed Reality Toolkit - Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity)**.</span></span> <span data-ttu-id="f777e-165">Vous pouvez trouver les versions dans [cette page](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases).</span><span class="sxs-lookup"><span data-stu-id="f777e-165">You can find the releases on [this page](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases).</span></span>

![ProjectStructure](images/mr213-projectstructure-650px.png)

<span data-ttu-id="f777e-167">**Scènes terminées pour votre référence**</span><span class="sxs-lookup"><span data-stu-id="f777e-167">**Completed scenes for your reference**</span></span>
* <span data-ttu-id="f777e-168">Deux scènes Unity terminées s’affichent sous le dossier **scenes** .</span><span class="sxs-lookup"><span data-stu-id="f777e-168">You will find two completed Unity scenes under **Scenes** folder.</span></span>
    * <span data-ttu-id="f777e-169">**MixedReality213**: Scène terminée avec un seul pinceau</span><span class="sxs-lookup"><span data-stu-id="f777e-169">**MixedReality213**: Completed scene with single brush</span></span>
    * <span data-ttu-id="f777e-170">**MixedReality213Advanced**: Scène terminée pour une conception avancée avec plusieurs pinceaux</span><span class="sxs-lookup"><span data-stu-id="f777e-170">**MixedReality213Advanced**: Completed scene for advanced design with multiple brushes</span></span>

<span data-ttu-id="f777e-171">**Nouvelle configuration de scène pour le didacticiel**</span><span class="sxs-lookup"><span data-stu-id="f777e-171">**New Scene setup for the tutorial**</span></span>
* <span data-ttu-id="f777e-172">Dans Unity, cliquez sur **fichier > nouvelle scène**</span><span class="sxs-lookup"><span data-stu-id="f777e-172">In Unity, click **File > New Scene**</span></span>
* <span data-ttu-id="f777e-173">Supprimer la **caméra principale** et la **lumière directionnelle**</span><span class="sxs-lookup"><span data-stu-id="f777e-173">Delete **Main Camera** and **Directional Light**</span></span>
* <span data-ttu-id="f777e-174">Dans le **volet de projet**, recherchez et faites glisser le prefabs suivant dans le volet de **hiérarchie** :</span><span class="sxs-lookup"><span data-stu-id="f777e-174">From the **Project panel**, search and drag the following prefabs into the **Hierarchy** panel:</span></span>
    * <span data-ttu-id="f777e-175">Ressources/HoloToolkit/entrée/Prefabs/**MixedRealityCamera**</span><span class="sxs-lookup"><span data-stu-id="f777e-175">Assets/HoloToolkit/Input/Prefabs/**MixedRealityCamera**</span></span>
    * <span data-ttu-id="f777e-176">Ressources/AppPrefabs/**environnement**</span><span class="sxs-lookup"><span data-stu-id="f777e-176">Assets/AppPrefabs/**Environment**</span></span>

![Appareil photo et environnement](images/mr213-cameraenvironment-300px.jpg)
* <span data-ttu-id="f777e-178">Il existe deux prefabs d’appareil photo dans Mixed Reality Toolkit:</span><span class="sxs-lookup"><span data-stu-id="f777e-178">There are two camera prefabs in Mixed Reality Toolkit:</span></span>
    * <span data-ttu-id="f777e-179">**MixedRealityCamera. Prefab**: Appareil photo uniquement</span><span class="sxs-lookup"><span data-stu-id="f777e-179">**MixedRealityCamera.prefab**: Camera only</span></span>
    * <span data-ttu-id="f777e-180">**MixedRealityCameraParent. Prefab**: Appareil photo + téléportage + limite</span><span class="sxs-lookup"><span data-stu-id="f777e-180">**MixedRealityCameraParent.prefab**: Camera + Teleportation + Boundary</span></span>
    * <span data-ttu-id="f777e-181">Dans ce didacticiel, nous allons utiliser **MixedRealityCamera** sans la fonctionnalité de téléportage.</span><span class="sxs-lookup"><span data-stu-id="f777e-181">In this tutorial, we will use **MixedRealityCamera** without teleportation feature.</span></span> <span data-ttu-id="f777e-182">Pour cette raison, nous avons ajouté un Prefab d' **environnement** simple qui contient un étage de base pour que l’utilisateur ait le sentiment de la terre.</span><span class="sxs-lookup"><span data-stu-id="f777e-182">Because of this, we added simple **Environment** prefab which contains a basic floor to make the user feel grounded.</span></span>
    * <span data-ttu-id="f777e-183">Pour en savoir plus sur la téléportage avec **MixedRealityCameraParent**, consultez [conception avancée-téléportage et locomotion](#advanced-design---teleportation-and-locomotion)</span><span class="sxs-lookup"><span data-stu-id="f777e-183">To learn more about the teleportation with **MixedRealityCameraParent**, see [Advanced design - Teleportation and locomotion](#advanced-design---teleportation-and-locomotion)</span></span>

<span data-ttu-id="f777e-184">**Installation de skybox**</span><span class="sxs-lookup"><span data-stu-id="f777e-184">**Skybox setup**</span></span>
* <span data-ttu-id="f777e-185">Cliquez sur **fenêtre > éclairage > paramètres**</span><span class="sxs-lookup"><span data-stu-id="f777e-185">Click **Window > Lighting > Settings**</span></span>
* <span data-ttu-id="f777e-186">Cliquez sur le cercle sur le côté droit du **champ de matériau skybox** .</span><span class="sxs-lookup"><span data-stu-id="f777e-186">Click the circle on the right side of the **Skybox Material field**</span></span>
* <span data-ttu-id="f777e-187">Tapez «Gray» et sélectionnez **SkyboxGray**</span><span class="sxs-lookup"><span data-stu-id="f777e-187">Type in ‘gray’ and select **SkyboxGray**</span></span>

<span data-ttu-id="f777e-188">(Ressources/AppPrefabs/support/Materials/SkyboxGray. mat)</span><span class="sxs-lookup"><span data-stu-id="f777e-188">(Assets/AppPrefabs/Support/Materials/SkyboxGray.mat)</span></span>

![Définition de skybox](images/mr123-skyboxsetting-400px.jpg)
* <span data-ttu-id="f777e-190">Cochez l’option **skybox** pour afficher le dégradé gris affecté skybox</span><span class="sxs-lookup"><span data-stu-id="f777e-190">Check **Skybox** option to be able to see assigned gray gradient skybox</span></span>

![Activer/désactiver l’option skybox](images/mr213-skyboxcheck-400px.jpg)
* <span data-ttu-id="f777e-192">La scène avec MixedRealityCamera, Environment et Gray skybox ressemblera à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="f777e-192">The scene with MixedRealityCamera, Environment and gray skybox will look like this.</span></span>

![Environnement MixedReality213](images/mr213-environment-600px.jpg)
* <span data-ttu-id="f777e-194">Cliquez sur **fichier > enregistrer la scène sous**</span><span class="sxs-lookup"><span data-stu-id="f777e-194">Click **File > Save Scene as**</span></span>
* <span data-ttu-id="f777e-195">**Enregistrez** votre scène sous le dossier scenes avec n’importe quel nom</span><span class="sxs-lookup"><span data-stu-id="f777e-195">**Save** your scene under Scenes folder with any name</span></span>

## <a name="chapter-1---controller-visualization"></a><span data-ttu-id="f777e-196">Chapitre 1-visualisation du contrôleur</span><span class="sxs-lookup"><span data-stu-id="f777e-196">Chapter 1 - Controller visualization</span></span>

>[!VIDEO https://www.youtube.com/embed/Kw0bf5NqyRg]

### <a name="objectives"></a><span data-ttu-id="f777e-197">Objectifs</span><span class="sxs-lookup"><span data-stu-id="f777e-197">Objectives</span></span>

* <span data-ttu-id="f777e-198">Découvrez comment restituer les modèles de contrôleur de mouvement en mode jeu Unity et au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="f777e-198">Learn how to render motion controller models in Unity's game mode and at runtime.</span></span>

<span data-ttu-id="f777e-199">Windows Mixed Reality fournit un modèle de contrôleur animé pour la visualisation du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="f777e-199">Windows Mixed Reality provides an animated controller model for controller visualization.</span></span> <span data-ttu-id="f777e-200">Vous pouvez prendre plusieurs approches pour la visualisation du contrôleur dans votre application:</span><span class="sxs-lookup"><span data-stu-id="f777e-200">There are several approaches you can take for controller visualization in your app:</span></span>
* <span data-ttu-id="f777e-201">Par défaut-utilisation du contrôleur par défaut sans modification</span><span class="sxs-lookup"><span data-stu-id="f777e-201">Default - Using default controller without modification</span></span>
* <span data-ttu-id="f777e-202">Hybride: à l’aide du contrôleur par défaut, mais en personnalisant certains de ses éléments ou en superposant des composants d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="f777e-202">Hybrid - Using default controller, but customizing some of its elements or overlaying UI components</span></span>
* <span data-ttu-id="f777e-203">Remplacement: utilisation de votre propre modèle 3D personnalisé pour le contrôleur</span><span class="sxs-lookup"><span data-stu-id="f777e-203">Replacement - Using your own customized 3D model for the controller</span></span>

<span data-ttu-id="f777e-204">Dans ce chapitre, nous allons découvrir les exemples de ces personnalisations de contrôleur.</span><span class="sxs-lookup"><span data-stu-id="f777e-204">In this chapter, we will learn about the examples of these controller customizations.</span></span>

### <a name="instructions"></a><span data-ttu-id="f777e-205">Instructions</span><span class="sxs-lookup"><span data-stu-id="f777e-205">Instructions</span></span>

* <span data-ttu-id="f777e-206">Dans le panneau **projet** , tapez **MotionControllers** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="f777e-206">In the **Project** panel, type **MotionControllers** in the search box .</span></span> <span data-ttu-id="f777e-207">Vous pouvez également le trouver sous ressources/HoloToolkit/entrée/Prefabs/.</span><span class="sxs-lookup"><span data-stu-id="f777e-207">You can also find it under Assets/HoloToolkit/Input/Prefabs/.</span></span>
* <span data-ttu-id="f777e-208">Faites glisser le Prefab **MotionControllers** dans le panneau de la **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="f777e-208">Drag the **MotionControllers** prefab into the **Hierarchy** panel.</span></span>
* <span data-ttu-id="f777e-209">Cliquez sur le Prefab **MotionControllers** dans le panneau **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="f777e-209">Click on the **MotionControllers** prefab in the **Hierarchy** panel.</span></span>

<span data-ttu-id="f777e-210">**MotionControllers Prefab**</span><span class="sxs-lookup"><span data-stu-id="f777e-210">**MotionControllers prefab**</span></span>

<span data-ttu-id="f777e-211">**MotionControllers** Prefab a un script **MotionControllerVisualizer** qui fournit les emplacements pour les autres modèles de contrôleur.</span><span class="sxs-lookup"><span data-stu-id="f777e-211">**MotionControllers** prefab has a **MotionControllerVisualizer** script which provides the slots for alternate controller models.</span></span> <span data-ttu-id="f777e-212">Si vous affectez vos propres modèles 3D personnalisés, tels qu’une main ou un épée, et que vous activez la case à cocher «toujours utiliser le modèle de remplacement gauche/droit», vous les verrez à la place du modèle par défaut.</span><span class="sxs-lookup"><span data-stu-id="f777e-212">If you assign your own custom 3D models such as a hand or a sword and check 'Always Use Alternate Left/Right Model', you will see them instead of the default model.</span></span> <span data-ttu-id="f777e-213">Nous allons utiliser cet emplacement dans le chapitre 4 pour remplacer le modèle de contrôleur par un pinceau.</span><span class="sxs-lookup"><span data-stu-id="f777e-213">We will use this slot in Chapter 4 to replace the controller model with a brush.</span></span>

![MR213_ControllerVisualizer](images/mr213-controllervisualizer-600px.png)

<span data-ttu-id="f777e-215">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="f777e-215">**Instructions**</span></span>
* <span data-ttu-id="f777e-216">Dans le panneau **inspecteur** , double-cliquez sur **MotionControllerVisualizer** script pour afficher le code dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f777e-216">In the **Inspector** panel, double click **MotionControllerVisualizer** script to see the code in the Visual Studio</span></span>

<span data-ttu-id="f777e-217">**Script MotionControllerVisualizer**</span><span class="sxs-lookup"><span data-stu-id="f777e-217">**MotionControllerVisualizer script**</span></span>

<span data-ttu-id="f777e-218">Les classes **MotionControllerVisualizer** et **MotionControllerInfo** fournissent les moyens d’accéder à & de modifier les modèles de contrôleur par défaut.</span><span class="sxs-lookup"><span data-stu-id="f777e-218">The **MotionControllerVisualizer** and **MotionControllerInfo** classes provide the means to access & modify the default controller models.</span></span> <span data-ttu-id="f777e-219">**MotionControllerVisualizer** s’abonne à l’événement **InteractionSourceDetected** de Unity et instancie automatiquement les modèles de contrôleur lorsqu’ils sont trouvés.</span><span class="sxs-lookup"><span data-stu-id="f777e-219">**MotionControllerVisualizer** subscribes to Unity's **InteractionSourceDetected** event and automatically instantiates controller models when they are found.</span></span>

```cs
protected override void Awake()
{
    ...
    InteractionManager.InteractionSourceDetected += InteractionManager_InteractionSourceDetected;
    InteractionManager.InteractionSourceLost += InteractionManager_InteractionSourceLost;
    ...
}
```

<span data-ttu-id="f777e-220">Les modèles de contrôleur sont fournis conformément à [la spécification glTF](https://github.com/KhronosGroup/glTF).</span><span class="sxs-lookup"><span data-stu-id="f777e-220">The controller models are delivered according to [the glTF specification](https://github.com/KhronosGroup/glTF).</span></span> <span data-ttu-id="f777e-221">Ce format a été créé pour fournir un format commun, tout en améliorant le processus de transmission et de décompression des ressources 3D.</span><span class="sxs-lookup"><span data-stu-id="f777e-221">This format has been created to provide a common format, while improving the process behind transmitting and unpacking 3D assets.</span></span> <span data-ttu-id="f777e-222">Dans ce cas, nous devons récupérer et charger les modèles de contrôleur lors de l’exécution, car nous souhaitons que l’expérience de l’utilisateur soit aussi transparente que possible, et il n’est pas garanti que la version des contrôleurs de mouvement que l’utilisateur utilise.</span><span class="sxs-lookup"><span data-stu-id="f777e-222">In this case, we need to retrieve and load the controller models at runtime, as we want to make the user's experience as seamless as possible, and it's not guaranteed which version of the motion controllers the user might be using.</span></span> <span data-ttu-id="f777e-223">Ce cours, via le kit d’outils de réalité mixte, utilise une version du [projet UnityGLTF](https://github.com/KhronosGroup/UnityGLTF)du groupe Khronos.</span><span class="sxs-lookup"><span data-stu-id="f777e-223">This course, via the Mixed Reality Toolkit, uses a version of the Khronos Group's [UnityGLTF project](https://github.com/KhronosGroup/UnityGLTF).</span></span>

<span data-ttu-id="f777e-224">Une fois le contrôleur remis, les scripts peuvent utiliser **MotionControllerInfo** pour rechercher les transformations pour des éléments de contrôleur spécifiques afin qu’ils puissent se positionner correctement.</span><span class="sxs-lookup"><span data-stu-id="f777e-224">Once the controller has been delivered, scripts can use **MotionControllerInfo** to find the transforms for specific controller elements so they can correctly position themselves.</span></span>

<span data-ttu-id="f777e-225">Dans un chapitre ultérieur, nous allons apprendre à utiliser ces scripts pour attacher des éléments d’interface utilisateur aux contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="f777e-225">In a later chapter, we will learn how to use these scripts to attach UI elements to the controllers.</span></span>

<span data-ttu-id="f777e-226">*Dans certains scripts, vous trouverez des blocs de code avec **#if! UNITY_EDITOR** ou **UNITY_WSA**. Ces blocs de code s’exécutent uniquement sur le runtime UWP quand vous déployez sur Windows. Cela est dû au fait que l’ensemble d’API utilisé par l’éditeur Unity et le runtime d’application UWP sont différents.*</span><span class="sxs-lookup"><span data-stu-id="f777e-226">*In some scripts, you will find code blocks with **#if !UNITY_EDITOR** or **UNITY_WSA**. These code blocks run only on the UWP runtime when you deploy to Windows. This is because the set of APIs used by the Unity editor and the UWP app runtime are different.*</span></span>
* <span data-ttu-id="f777e-227">**Enregistrez** la scène, puis cliquez sur le bouton **lecture** .</span><span class="sxs-lookup"><span data-stu-id="f777e-227">**Save** the scene and click the **play** button.</span></span>

<span data-ttu-id="f777e-228">Vous pourrez voir la scène avec des contrôleurs de mouvement dans votre casque.</span><span class="sxs-lookup"><span data-stu-id="f777e-228">You will be able to see the scene with motion controllers in your headset.</span></span> <span data-ttu-id="f777e-229">Vous pouvez voir des animations détaillées pour les clics de bouton, le mouvement du joystick et la mise en surbrillance des touches tactiles.</span><span class="sxs-lookup"><span data-stu-id="f777e-229">You can see detailed animations for button clicks, thumbstick movement, and touchpad touch highlighting.</span></span>

![MR213_Controller visualisation par défaut](images/mr213-controllervisualizationdefault-500px.jpg)

## <a name="chapter-2---attaching-ui-elements-to-the-controller"></a><span data-ttu-id="f777e-231">Chapitre 2-attachement des éléments d’interface utilisateur au contrôleur</span><span class="sxs-lookup"><span data-stu-id="f777e-231">Chapter 2 - Attaching UI elements to the controller</span></span>

>[!VIDEO https://www.youtube.com/embed/e-mLlwmTzJo]

### <a name="objectives"></a><span data-ttu-id="f777e-232">Objectifs</span><span class="sxs-lookup"><span data-stu-id="f777e-232">Objectives</span></span>

* <span data-ttu-id="f777e-233">En savoir plus sur les éléments des contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="f777e-233">Learn about the elements of the motion controllers</span></span>
* <span data-ttu-id="f777e-234">Découvrez comment attacher des objets à des parties spécifiques des contrôleurs</span><span class="sxs-lookup"><span data-stu-id="f777e-234">Learn how to attach objects to specific parts of the controllers</span></span>

<span data-ttu-id="f777e-235">Dans ce chapitre, vous allez apprendre à ajouter des éléments d’interface utilisateur au contrôleur que l’utilisateur peut facilement accéder et manipuler à tout moment.</span><span class="sxs-lookup"><span data-stu-id="f777e-235">In this chapter, you will learn how to add user interface elements to the controller which the user can easily access and manipulate at anytime.</span></span> <span data-ttu-id="f777e-236">Vous allez également apprendre à ajouter une interface utilisateur de sélecteur de couleurs simple à l’aide de l’entrée du pavé tactile.</span><span class="sxs-lookup"><span data-stu-id="f777e-236">You will also learn how to add a simple color picker UI using the touchpad input.</span></span>

### <a name="instructions"></a><span data-ttu-id="f777e-237">Instructions</span><span class="sxs-lookup"><span data-stu-id="f777e-237">Instructions</span></span>

* <span data-ttu-id="f777e-238">Dans le panneau **projet** , recherchez script **MotionControllerInfo** .</span><span class="sxs-lookup"><span data-stu-id="f777e-238">In the **Project** panel, search **MotionControllerInfo** script.</span></span>
* <span data-ttu-id="f777e-239">Dans le résultat de la recherche, double-cliquez sur le script **MotionControllerInfo** pour afficher le code dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f777e-239">From the search result, double click **MotionControllerInfo** script to see the code in Visual Studio.</span></span>

<span data-ttu-id="f777e-240">**Script MotionControllerInfo**</span><span class="sxs-lookup"><span data-stu-id="f777e-240">**MotionControllerInfo script**</span></span>

<span data-ttu-id="f777e-241">La première étape consiste à choisir l’élément du contrôleur auquel vous souhaitez attacher l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f777e-241">The first step is to choose which element of the controller you want the UI to attach to.</span></span> <span data-ttu-id="f777e-242">Ces éléments sont définis dans **ControllerElementEnum** dans **MotionControllerInfo.cs**.</span><span class="sxs-lookup"><span data-stu-id="f777e-242">These elements are defined in **ControllerElementEnum** in **MotionControllerInfo.cs**.</span></span>

![MR213 MotionControllerElements](images/mr213-motioncontrollerelements-1000px.jpg)
* <span data-ttu-id="f777e-244">**Accueil**</span><span class="sxs-lookup"><span data-stu-id="f777e-244">**Home**</span></span>
* <span data-ttu-id="f777e-245">**Menu**</span><span class="sxs-lookup"><span data-stu-id="f777e-245">**Menu**</span></span>
* <span data-ttu-id="f777e-246">**Maîtriser**</span><span class="sxs-lookup"><span data-stu-id="f777e-246">**Grasp**</span></span>
* <span data-ttu-id="f777e-247">**Stick**</span><span class="sxs-lookup"><span data-stu-id="f777e-247">**Thumbstick**</span></span>
* <span data-ttu-id="f777e-248">**Sélectionné**</span><span class="sxs-lookup"><span data-stu-id="f777e-248">**Select**</span></span>
* <span data-ttu-id="f777e-249">**Pavé tactile**</span><span class="sxs-lookup"><span data-stu-id="f777e-249">**Touchpad**</span></span>
* <span data-ttu-id="f777e-250">**Pose** de pointage: cet élément représente l’extrémité du point de contrôle de direction vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="f777e-250">**Pointing pose** – this element represents the tip of the controller pointing forward direction.</span></span>

<span data-ttu-id="f777e-251">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="f777e-251">**Instructions**</span></span>
* <span data-ttu-id="f777e-252">Dans le panneau **projet** , recherchez script **AttachToController** .</span><span class="sxs-lookup"><span data-stu-id="f777e-252">In the **Project** panel, search **AttachToController** script.</span></span>
* <span data-ttu-id="f777e-253">Dans le résultat de la recherche, double-cliquez sur le script **AttachToController** pour afficher le code dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f777e-253">From the search result, double click **AttachToController** script to see the code in Visual Studio.</span></span>

<span data-ttu-id="f777e-254">**Script AttachToController**</span><span class="sxs-lookup"><span data-stu-id="f777e-254">**AttachToController script**</span></span>

<span data-ttu-id="f777e-255">Le script **AttachToController** offre un moyen simple d’attacher des objets à un élément et un élément de contrôle.</span><span class="sxs-lookup"><span data-stu-id="f777e-255">The **AttachToController** script provides a simple way to attach any objects to a specified controller handedness and element.</span></span>

<span data-ttu-id="f777e-256">Dans **AttachElementToController ()** ,</span><span class="sxs-lookup"><span data-stu-id="f777e-256">In **AttachElementToController()**,</span></span>
* <span data-ttu-id="f777e-257">Vérifier la main à l’aide de **MotionControllerInfo. main**</span><span class="sxs-lookup"><span data-stu-id="f777e-257">Check handedness using **MotionControllerInfo.Handedness**</span></span>
* <span data-ttu-id="f777e-258">Obtient un élément spécifique du contrôleur à l’aide de **MotionControllerInfo. TryGetElement ()**</span><span class="sxs-lookup"><span data-stu-id="f777e-258">Get specific element of the controller using **MotionControllerInfo.TryGetElement()**</span></span>
* <span data-ttu-id="f777e-259">Après avoir récupéré la transformation de l’élément à partir du modèle de contrôleur, mettez-y le parent de l’objet et définissez position locale de l’objet & la rotation sur zéro.</span><span class="sxs-lookup"><span data-stu-id="f777e-259">After retrieving the element's transform from the controller model, parent the object under it and set object's local position & rotation to zero.</span></span>

```cs
public MotionControllerInfo.ControllerElementEnum Element { get { return element; } }

private void AttachElementToController(MotionControllerInfo newController)
{
     if (!IsAttached && newController.Handedness == handedness)
     {
          if (!newController.TryGetElement(element, out elementTransform))
          {
               Debug.LogError("Unable to find element of type " + element + " under controller " + newController.ControllerParent.name + "; not attaching.");
               return;
          }

          controller = newController;

          SetChildrenActive(true);

          // Parent ourselves under the element and set our offsets
          transform.parent = elementTransform;
          transform.localPosition = positionOffset;
          transform.localEulerAngles = rotationOffset;
          if (setScaleOnAttach)
          {
               transform.localScale = scale;
          }

          // Announce that we're attached
          OnAttachToController();
          IsAttached = true;
     }
}
```

<span data-ttu-id="f777e-260">La façon la plus simple d’utiliser le script **AttachToController** est d’en hériter, comme nous l’avons fait dans le cas de **ColorPickerWheel.**</span><span class="sxs-lookup"><span data-stu-id="f777e-260">The simplest way to use **AttachToController** script is to inherit from it, as we've done in the case of **ColorPickerWheel.**</span></span> <span data-ttu-id="f777e-261">Remplacez simplement les fonctions **OnAttachToController** et **OnDetatchFromController** pour effectuer votre configuration/répartition lorsque le contrôleur est détecté/déconnecté.</span><span class="sxs-lookup"><span data-stu-id="f777e-261">Simply override the **OnAttachToController** and **OnDetatchFromController** functions to perform your setup / breakdown when the controller is detected / disconnected.</span></span>

<span data-ttu-id="f777e-262">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="f777e-262">**Instructions**</span></span>
* <span data-ttu-id="f777e-263">Dans le panneau **projet** , tapez dans la zone de recherche **ColorPickerWheel**.</span><span class="sxs-lookup"><span data-stu-id="f777e-263">In the **Project** panel, type in the search box **ColorPickerWheel**.</span></span> <span data-ttu-id="f777e-264">Vous pouvez également le trouver sous ressources/AppPrefabs/.</span><span class="sxs-lookup"><span data-stu-id="f777e-264">You can also find it under Assets/AppPrefabs/.</span></span>
* <span data-ttu-id="f777e-265">Faites glisser **ColorPickerWheel** Prefab dans le panneau de **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="f777e-265">Drag **ColorPickerWheel** prefab into the **Hierarchy** panel.</span></span>
* <span data-ttu-id="f777e-266">Cliquez sur le Prefab **ColorPickerWheel** dans le panneau **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="f777e-266">Click the **ColorPickerWheel** prefab in the **Hierarchy** panel.</span></span>
* <span data-ttu-id="f777e-267">Dans le panneau **inspecteur** , double-cliquez sur **ColorPickerWheel** script pour afficher le code dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f777e-267">In the **Inspector** panel, double click **ColorPickerWheel** Script to see the code in Visual Studio.</span></span>

![ColorPickerWheel Prefab](images/mr213-colorpickerwheel-1000px.jpg)

<span data-ttu-id="f777e-269">**Script ColorPickerWheel**</span><span class="sxs-lookup"><span data-stu-id="f777e-269">**ColorPickerWheel script**</span></span>

<span data-ttu-id="f777e-270">Étant donné que **ColorPickerWheel** hérite de **AttachToController**, il affiche la **main** et l' **élément** dans le panneau de l' **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="f777e-270">Since **ColorPickerWheel** inherits **AttachToController**, it shows **Handedness** and **Element** in the **Inspector** panel.</span></span> <span data-ttu-id="f777e-271">Nous allons attacher l’interface utilisateur à l’élément Touchpad sur le contrôleur de gauche.</span><span class="sxs-lookup"><span data-stu-id="f777e-271">We'll be attaching the UI to the Touchpad element on the left controller.</span></span>

![Script ColorPickerWheel](images/mr213-attachtocontroller-300px.jpg)

<span data-ttu-id="f777e-273">**ColorPickerWheel** remplace les **OnAttachToController** et **OnDetatchFromController** pour s’abonner à l’événement d’entrée qui sera utilisé dans le chapitre suivant pour la sélection des couleurs avec l’entrée du pavé tactile.</span><span class="sxs-lookup"><span data-stu-id="f777e-273">**ColorPickerWheel** overrides the **OnAttachToController** and **OnDetatchFromController** to subscribe to the input event which will be used in next chapter for color selection with touchpad input.</span></span>

```cs
public class ColorPickerWheel : AttachToController, IPointerTarget
{
    protected override void OnAttachToController()
    {
        // Subscribe to input now that we're parented under the controller
        InteractionManager.InteractionSourceUpdated += InteractionSourceUpdated;
    }

    protected override void OnDetachFromController()
    {
        Visible = false;

        // Unsubscribe from input now that we've detached from the controller
        InteractionManager.InteractionSourceUpdated -= InteractionSourceUpdated;
    }
    ...
}
```
* <span data-ttu-id="f777e-274">**Enregistrez** la scène, puis cliquez sur le bouton **lecture** .</span><span class="sxs-lookup"><span data-stu-id="f777e-274">**Save** the scene and click the **play** button.</span></span>

<span data-ttu-id="f777e-275">**Autre méthode pour attacher des objets aux contrôleurs**</span><span class="sxs-lookup"><span data-stu-id="f777e-275">**Alternative method for attaching objects to the controllers**</span></span>

<span data-ttu-id="f777e-276">Nous recommandons que vos scripts héritent de **AttachToController** et remplacent **OnAttachToController**.</span><span class="sxs-lookup"><span data-stu-id="f777e-276">We recommend that your scripts inherit from **AttachToController** and override **OnAttachToController**.</span></span> <span data-ttu-id="f777e-277">Toutefois, cela n’est pas toujours possible.</span><span class="sxs-lookup"><span data-stu-id="f777e-277">However, this may not always be possible.</span></span> <span data-ttu-id="f777e-278">Une alternative consiste à l’utiliser comme un composant autonome.</span><span class="sxs-lookup"><span data-stu-id="f777e-278">An alternative is using it as a standalone component.</span></span> <span data-ttu-id="f777e-279">Cela peut être utile lorsque vous souhaitez attacher un Prefab existant à un contrôleur sans Refactoriser vos scripts.</span><span class="sxs-lookup"><span data-stu-id="f777e-279">This can be useful when you want to attach an existing prefab to a controller without refactoring your scripts.</span></span> <span data-ttu-id="f777e-280">Faites simplement en sorte que votre classe attende que IsAttached, soit défini sur true avant d’effectuer une installation.</span><span class="sxs-lookup"><span data-stu-id="f777e-280">Simply have your class wait for IsAttached to be set to true before performing any setup.</span></span> <span data-ttu-id="f777e-281">Pour ce faire, la méthode la plus simple consiste à utiliser une Coroutine pour «Start».</span><span class="sxs-lookup"><span data-stu-id="f777e-281">The simplest way to do this is by using a coroutine for 'Start.'</span></span>

```cs
private IEnumerator Start() {
    AttachToController attach = gameObject.GetComponent<AttachToController>();

    while (!attach.IsAttached) {
        yield return null;
    }

    // Perform setup here
}
```

## <a name="chapter-3---working-with-touchpad-input"></a><span data-ttu-id="f777e-282">Chapitre 3-utilisation de l’entrée du pavé tactile</span><span class="sxs-lookup"><span data-stu-id="f777e-282">Chapter 3 - Working with touchpad input</span></span>

>[!VIDEO https://www.youtube.com/embed/SUyw0kxZPFw]

### <a name="objectives"></a><span data-ttu-id="f777e-283">Objectifs</span><span class="sxs-lookup"><span data-stu-id="f777e-283">Objectives</span></span>

* <span data-ttu-id="f777e-284">Découvrez comment obtenir des événements de données d’entrée dans le pavé tactile</span><span class="sxs-lookup"><span data-stu-id="f777e-284">Learn how to get touchpad input data events</span></span>
* <span data-ttu-id="f777e-285">Découvrez comment utiliser les informations de position de l’axe du pavé tactile pour votre expérience d’application</span><span class="sxs-lookup"><span data-stu-id="f777e-285">Learn how to use touchpad axis position information for your app experience</span></span>

### <a name="instructions"></a><span data-ttu-id="f777e-286">Instructions</span><span class="sxs-lookup"><span data-stu-id="f777e-286">Instructions</span></span>

* <span data-ttu-id="f777e-287">Dans le volet **hiérarchie** , cliquez sur **ColorPickerWheel**</span><span class="sxs-lookup"><span data-stu-id="f777e-287">In the **Hierarchy** panel, click **ColorPickerWheel**</span></span>
* <span data-ttu-id="f777e-288">Dans le panneau **inspecteur** , sous **Animatior**, double-cliquez sur **ColorPickerWheelController**</span><span class="sxs-lookup"><span data-stu-id="f777e-288">In the **Inspector** panel, under **Animatior**, double click **ColorPickerWheelController**</span></span>
* <span data-ttu-id="f777e-289">Vous pourrez voir l’onglet **animation** ouvert</span><span class="sxs-lookup"><span data-stu-id="f777e-289">You will be able to see **Animator** tab opened</span></span>

<span data-ttu-id="f777e-290">**Montrer/masquer l’interface utilisateur avec le contrôleur d’animation Unity**</span><span class="sxs-lookup"><span data-stu-id="f777e-290">**Showing/hiding UI with Unity's Animation controller**</span></span>

<span data-ttu-id="f777e-291">Pour afficher et masquer l’interface utilisateur **ColorPickerWheel** avec l’animation, nous utilisons le [système d’animation Unity](https://docs.unity3d.com/Manual/AnimationOverview.html).</span><span class="sxs-lookup"><span data-stu-id="f777e-291">To show and hide the **ColorPickerWheel** UI with animation, we are using [Unity's animation system](https://docs.unity3d.com/Manual/AnimationOverview.html).</span></span> <span data-ttu-id="f777e-292">L’affectation de la valeur true ou false aux déclencheurs de la propriété **visible** de **ColorPickerWheel** **affiche** et **masque** les déclencheurs d’animation.</span><span class="sxs-lookup"><span data-stu-id="f777e-292">Setting the **ColorPickerWheel**'s **Visible** property to true or false triggers **Show** and **Hide** animation triggers.</span></span> <span data-ttu-id="f777e-293">Les paramètres d' **affichage** et de **masquage** sont définis dans le contrôleur d’animation **ColorPickerWheelController** .</span><span class="sxs-lookup"><span data-stu-id="f777e-293">**Show** and **Hide** parameters are defined in the **ColorPickerWheelController** animation controller.</span></span>

![Contrôleur d’animation Unity](images/mr123-animationcontroller-550px.jpg)

<span data-ttu-id="f777e-295">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="f777e-295">**Instructions**</span></span>
* <span data-ttu-id="f777e-296">Dans le volet **hiérarchie** , sélectionnez **ColorPickerWheel** Prefab</span><span class="sxs-lookup"><span data-stu-id="f777e-296">In the **Hierarchy** panel, select **ColorPickerWheel** prefab</span></span>
* <span data-ttu-id="f777e-297">Dans le panneau **inspecteur** , double-cliquez sur **ColorPickerWheel** script pour afficher le code dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f777e-297">In the **Inspector** panel, double click **ColorPickerWheel** script to see the code in the Visual Studio</span></span>

<span data-ttu-id="f777e-298">**Script ColorPickerWheel**</span><span class="sxs-lookup"><span data-stu-id="f777e-298">**ColorPickerWheel script**</span></span>

<span data-ttu-id="f777e-299">**ColorPickerWheel** s’abonne à l’événement **InteractionSourceUpdated** d’Unity pour écouter les événements du pavé tactile.</span><span class="sxs-lookup"><span data-stu-id="f777e-299">**ColorPickerWheel** subscribes to Unity's **InteractionSourceUpdated** event to listen for touchpad events.</span></span>

<span data-ttu-id="f777e-300">Dans **InteractionSourceUpdated ()** , le script commence par vérifier qu’il:</span><span class="sxs-lookup"><span data-stu-id="f777e-300">In **InteractionSourceUpdated()**, the script first checks to ensure that it:</span></span>
* <span data-ttu-id="f777e-301">est en fait un événement de pavé tactile (obj. State). **touchpadTouched**)</span><span class="sxs-lookup"><span data-stu-id="f777e-301">is actually a touchpad event (obj.state.**touchpadTouched**)</span></span>
* <span data-ttu-id="f777e-302">provient du contrôleur gauche (obj. State. source). **droitier**)</span><span class="sxs-lookup"><span data-stu-id="f777e-302">originates from the left controller (obj.state.source.**handedness**)</span></span>

<span data-ttu-id="f777e-303">Si les deux ont la valeur true, la position du pavé tactile (obj. State. **touchpadPosition**) est assignée à **selectorPosition**.</span><span class="sxs-lookup"><span data-stu-id="f777e-303">If both are true, the touchpad position (obj.state.**touchpadPosition**) is assigned to **selectorPosition**.</span></span>

```cs
private void InteractionSourceUpdated(InteractionSourceUpdatedEventArgs obj)
{
    if (obj.state.source.handedness == handedness && obj.state.touchpadTouched)
    {
        Visible = true;
        selectorPosition = obj.state.touchpadPosition;
    }
}
```

<span data-ttu-id="f777e-304">Dans **Update ()** , en fonction de la propriété **visible** , elle déclenche les déclencheurs d’animation afficher et masquer dans le composant d’animation du sélecteur de couleurs</span><span class="sxs-lookup"><span data-stu-id="f777e-304">In **Update()**, based on **visible** property, it triggers Show and Hide animation triggers in the color picker's animator component</span></span>

```cs
if (visible != visibleLastFrame)
{
    if (visible)
    {
        animator.SetTrigger("Show");
    }
    else
    {
        animator.SetTrigger("Hide");
    }
}
```

<span data-ttu-id="f777e-305">Dans **Update ()** , **selectorPosition** est utilisé pour effectuer un cast d’un rayon au niveau du conflit de maillage de la roue de couleur, qui retourne une position UV.</span><span class="sxs-lookup"><span data-stu-id="f777e-305">In **Update()**, **selectorPosition** is used to cast a ray at the color wheel's mesh collider, which returns a UV position.</span></span> <span data-ttu-id="f777e-306">Cette position peut ensuite être utilisée pour rechercher la coordonnée de pixels et la valeur de couleur de la texture de la roue chromatique.</span><span class="sxs-lookup"><span data-stu-id="f777e-306">This position can then be used to find the pixel coordinate and color value of the color wheel's texture.</span></span> <span data-ttu-id="f777e-307">Cette valeur est accessible aux autres scripts via la propriété **SelectedColor** .</span><span class="sxs-lookup"><span data-stu-id="f777e-307">This value is accessible to other scripts via the **SelectedColor** property.</span></span>

![Roulette du sélecteur de couleurs Raycasting](images/mr213-colorpickerwheel-raycast-700px.png)

```cs
...
    // Clamp selector position to a radius of 1
    Vector3 localPosition = new Vector3(selectorPosition.x * inputScale, 0.15f, selectorPosition.y * inputScale);
    if (localPosition.magnitude > 1)
    {
        localPosition = localPosition.normalized;
    }
    selectorTransform.localPosition = localPosition;

    // Raycast the wheel mesh and get its UV coordinates
    Vector3 raycastStart = selectorTransform.position + selectorTransform.up * 0.15f;
    RaycastHit hit;
    Debug.DrawLine(raycastStart, raycastStart - (selectorTransform.up * 0.25f));

    if (Physics.Raycast(raycastStart, -selectorTransform.up, out hit, 0.25f, 1 << colorWheelObject.layer, QueryTriggerInteraction.Ignore))
    {
        // Get pixel from the color wheel texture using UV coordinates
        Vector2 uv = hit.textureCoord;
        int pixelX = Mathf.FloorToInt(colorWheelTexture.width * uv.x);
        int pixelY = Mathf.FloorToInt(colorWheelTexture.height * uv.y);
        selectedColor = colorWheelTexture.GetPixel(pixelX, pixelY);
        selectedColor.a = 1f;
    }
    // Set the selector's color and blend it with white to make it visible on top of the wheel
    selectorRenderer.material.color = Color.Lerp (selectedColor, Color.white, 0.5f);
}
```

## <a name="chapter-4---overriding-controller-model"></a><span data-ttu-id="f777e-309">Chapitre 4-remplacement du modèle de contrôleur</span><span class="sxs-lookup"><span data-stu-id="f777e-309">Chapter 4 - Overriding controller model</span></span>

>[!VIDEO https://www.youtube.com/embed/8gBFqA_DZ_U]

### <a name="objectives"></a><span data-ttu-id="f777e-310">Objectifs</span><span class="sxs-lookup"><span data-stu-id="f777e-310">Objectives</span></span>

* <span data-ttu-id="f777e-311">Découvrez comment remplacer le modèle de contrôleur par un modèle 3D personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f777e-311">Learn how to override the controller model with a custom 3D model.</span></span>

![MR213_BrushToolOverride](images/mr213-brushtooloverride-500px.jpg)

### <a name="instructions"></a><span data-ttu-id="f777e-313">Instructions</span><span class="sxs-lookup"><span data-stu-id="f777e-313">Instructions</span></span>

* <span data-ttu-id="f777e-314">Dans le volet **hiérarchie** , cliquez sur **MotionControllers** .</span><span class="sxs-lookup"><span data-stu-id="f777e-314">Click **MotionControllers** in the **Hierarchy** panel.</span></span>
* <span data-ttu-id="f777e-315">Cliquez sur le cercle sur le côté droit du champ **autre contrôleur de droite** .</span><span class="sxs-lookup"><span data-stu-id="f777e-315">Click the circle on the right side of the **Alternate Right Controller** field.</span></span>
* <span data-ttu-id="f777e-316">Tapez **«BrushController**» et sélectionnez Prefab dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="f777e-316">Type in **'BrushController**' and select the prefab from the result.</span></span> <span data-ttu-id="f777e-317">Vous pouvez le trouver sous actifs/AppPrefabs/**BrushController**.</span><span class="sxs-lookup"><span data-stu-id="f777e-317">You can find it under Assets/AppPrefabs/**BrushController**.</span></span>
* <span data-ttu-id="f777e-318">Cochez **toujours utiliser le modèle de remplacement à droite**</span><span class="sxs-lookup"><span data-stu-id="f777e-318">Check **Always Use Alternate Right Model**</span></span>

![MR213_BrushToolOverrideSlot](images/mr213-motioncontrollersoverride-700px.jpg)

<span data-ttu-id="f777e-320">Le Prefab **BrushController** ne doit pas être inclus dans le panneau de **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="f777e-320">The **BrushController** prefab does not have to be included in the **Hierarchy** panel.</span></span> <span data-ttu-id="f777e-321">Toutefois, pour extraire ses composants enfants:</span><span class="sxs-lookup"><span data-stu-id="f777e-321">However, to check out its child components:</span></span>
* <span data-ttu-id="f777e-322">Dans le panneau **projet** , tapez **BrushController** et faites glisser **BrushController** Prefab dans le volet **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="f777e-322">In the **Project** panel, type in **BrushController** and drag **BrushController** prefab into the **Hierarchy** panel.</span></span>

![MR213_BrushTool_Prefab2](images/mr213-brushtool-prefab-1000px.jpg)

<span data-ttu-id="f777e-324">Vous trouverez le composant **Tip** dans **BrushController**.</span><span class="sxs-lookup"><span data-stu-id="f777e-324">You will find the **Tip** component in **BrushController**.</span></span> <span data-ttu-id="f777e-325">Nous allons utiliser sa transformation pour démarrer/arrêter le dessin de lignes.</span><span class="sxs-lookup"><span data-stu-id="f777e-325">We will use its transform to start/stop drawing lines.</span></span>
* <span data-ttu-id="f777e-326">Supprimez le **BrushController** du panneau de la **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="f777e-326">Delete the **BrushController** from the **Hierarchy** panel.</span></span>
* <span data-ttu-id="f777e-327">**Enregistrez** la scène, puis cliquez sur le bouton **lecture** .</span><span class="sxs-lookup"><span data-stu-id="f777e-327">**Save** the scene and click the **play** button.</span></span> <span data-ttu-id="f777e-328">Vous serez en mesure de voir que le modèle de pinceau a remplacé le contrôleur de mouvement de droite.</span><span class="sxs-lookup"><span data-stu-id="f777e-328">You will be able to see the brush model replaced the right-hand motion controller.</span></span>

## <a name="chapter-5---painting-with-select-input"></a><span data-ttu-id="f777e-329">Chapitre 5-peinture avec l’entrée Select</span><span class="sxs-lookup"><span data-stu-id="f777e-329">Chapter 5 - Painting with Select input</span></span>

>[!VIDEO https://www.youtube.com/embed/QTrYaMHIs7w]

### <a name="objectives"></a><span data-ttu-id="f777e-330">Objectifs</span><span class="sxs-lookup"><span data-stu-id="f777e-330">Objectives</span></span>

* <span data-ttu-id="f777e-331">Découvrez comment utiliser l’événement bouton Sélectionner pour démarrer et arrêter un dessin de ligne</span><span class="sxs-lookup"><span data-stu-id="f777e-331">Learn how to use the Select button event to start and stop a line drawing</span></span>

### <a name="instructions"></a><span data-ttu-id="f777e-332">Instructions</span><span class="sxs-lookup"><span data-stu-id="f777e-332">Instructions</span></span>

* <span data-ttu-id="f777e-333">Recherchez **BrushController** Prefab dans le panneau **projet** .</span><span class="sxs-lookup"><span data-stu-id="f777e-333">Search **BrushController** prefab in the **Project** panel.</span></span>
* <span data-ttu-id="f777e-334">Dans le panneau **inspecteur** , double-cliquez sur **BrushController** script pour afficher le code dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f777e-334">In the **Inspector** panel, double click **BrushController** Script to see the code in Visual Studio</span></span>

<span data-ttu-id="f777e-335">**Script BrushController**</span><span class="sxs-lookup"><span data-stu-id="f777e-335">**BrushController script**</span></span>

<span data-ttu-id="f777e-336">**BrushController** s’abonne aux événements **InteractionSourcePressed** et **InteractionSourceReleased** du InteractionManager.</span><span class="sxs-lookup"><span data-stu-id="f777e-336">**BrushController** subscribes to the InteractionManager's **InteractionSourcePressed** and **InteractionSourceReleased** events.</span></span> <span data-ttu-id="f777e-337">Lorsque l’événement **InteractionSourcePressed** est déclenché, la propriété **Draw** du pinceau est définie sur true; Lorsque l’événement **InteractionSourceReleased** est déclenché, la propriété **Draw** du pinceau est définie sur false.</span><span class="sxs-lookup"><span data-stu-id="f777e-337">When **InteractionSourcePressed** event is triggered, the brush's **Draw** property is set to true; when **InteractionSourceReleased** event is triggered, the brush's **Draw** property is set to false.</span></span>

```cs
private void InteractionSourcePressed(InteractionSourcePressedEventArgs obj)
{
    if (obj.state.source.handedness == InteractionSourceHandedness.Right && obj.pressType == InteractionSourcePressType.Select)
    {
        Draw = true;
    }
}

private void InteractionSourceReleased(InteractionSourceReleasedEventArgs obj)
{
    if (obj.state.source.handedness == InteractionSourceHandedness.Right && obj.pressType == InteractionSourcePressType.Select)
    {
        Draw = false;
    }
}
```

<span data-ttu-id="f777e-338">Bien que **Draw** ait la valeur true, le pinceau génère des points dans une Unity **LineRenderer**instanciée.</span><span class="sxs-lookup"><span data-stu-id="f777e-338">While **Draw** is set to true, the brush will generate points in an instantiated Unity **LineRenderer**.</span></span> <span data-ttu-id="f777e-339">Une référence à ce Prefab est conservée dans le champ **Stroke Prefab** du pinceau.</span><span class="sxs-lookup"><span data-stu-id="f777e-339">A reference to this prefab is kept in the brush's **Stroke Prefab** field.</span></span>

```cs
private IEnumerator DrawOverTime()
{
    // Get the position of the tip
    Vector3 lastPointPosition = tip.position;

    ...

    // Create a new brush stroke
    GameObject newStroke = Instantiate(strokePrefab);
    LineRenderer line = newStroke.GetComponent<LineRenderer>();
    newStroke.transform.position = startPosition;
    line.SetPosition(0, tip.position);
    float initialWidth = line.widthMultiplier;

    // Generate points in an instantiated Unity LineRenderer
    while (draw)
    {
        // Move the last point to the draw point position
        line.SetPosition(line.positionCount - 1, tip.position);
        line.material.color = colorPicker.SelectedColor;
        brushRenderer.material.color = colorPicker.SelectedColor;
        lastPointAddedTime = Time.unscaledTime;
        // Adjust the width between 1x and 2x width based on strength of trigger pull
        line.widthMultiplier = Mathf.Lerp(initialWidth, initialWidth * 2, width);

        if (Vector3.Distance(lastPointPosition, tip.position) > minPositionDelta || Time.unscaledTime > lastPointAddedTime + maxTimeDelta)
        {
            // Spawn a new point
            lastPointAddedTime = Time.unscaledTime;
            lastPointPosition = tip.position;
            line.positionCount += 1;
            line.SetPosition(line.positionCount - 1, lastPointPosition);
        }
        yield return null;
    }
}
```

<span data-ttu-id="f777e-340">Pour utiliser la couleur actuellement sélectionnée à partir de l’interface utilisateur de la roue du sélecteur de couleurs, **BrushController** doit avoir une référence à l’objet **ColorPickerWheel** .</span><span class="sxs-lookup"><span data-stu-id="f777e-340">To use the currently selected color from the color picker wheel UI, **BrushController** needs to have a reference to the **ColorPickerWheel** object.</span></span> <span data-ttu-id="f777e-341">Étant donné que le Prefab **BrushController** est instancié au moment de l’exécution en tant que contrôleur de remplacement, toutes les références aux objets de la scène doivent être définies au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="f777e-341">Because the **BrushController** prefab is instantiated at runtime as a replacement controller, any references to objects in the scene will have to be set at runtime.</span></span> <span data-ttu-id="f777e-342">Dans ce cas, nous utilisons **GameObject. FindObjectOfType** pour localiser le **ColorPickerWheel**:</span><span class="sxs-lookup"><span data-stu-id="f777e-342">In this case we use **GameObject.FindObjectOfType** to locate the **ColorPickerWheel**:</span></span>

```cs
private void OnEnable()
{
    // Locate the ColorPickerWheel
    colorPicker = FindObjectOfType<ColorPickerWheel>();

    // Assign currently selected color to the brush’s material color
    brushRenderer.material.color = colorPicker.SelectedColor;
    ...
}
```
* <span data-ttu-id="f777e-343">**Enregistrez** la scène, puis cliquez sur le bouton **lecture** .</span><span class="sxs-lookup"><span data-stu-id="f777e-343">**Save** the scene and click the **play** button.</span></span> <span data-ttu-id="f777e-344">Vous pourrez dessiner les lignes et peindre à l’aide du bouton Sélectionner sur le contrôleur de droite.</span><span class="sxs-lookup"><span data-stu-id="f777e-344">You will be able to draw the lines and paint using the select button on the right-hand controller.</span></span>

## <a name="chapter-6---object-spawning-with-select-input"></a><span data-ttu-id="f777e-345">Chapitre 6-génération d’objets avec sélection d’entrée</span><span class="sxs-lookup"><span data-stu-id="f777e-345">Chapter 6 - Object spawning with Select input</span></span>

>[!VIDEO https://www.youtube.com/embed/z4IxyzFHP0U]

### <a name="objectives"></a><span data-ttu-id="f777e-346">Objectifs</span><span class="sxs-lookup"><span data-stu-id="f777e-346">Objectives</span></span>

* <span data-ttu-id="f777e-347">Découvrez comment utiliser les événements d’entrée de bouton Sélectionner et ressaisir</span><span class="sxs-lookup"><span data-stu-id="f777e-347">Learn how to use Select and Grasp button input events</span></span>
* <span data-ttu-id="f777e-348">Apprendre à instancier des objets</span><span class="sxs-lookup"><span data-stu-id="f777e-348">Learn how to instantiate objects</span></span>

### <a name="instructions"></a><span data-ttu-id="f777e-349">Instructions</span><span class="sxs-lookup"><span data-stu-id="f777e-349">Instructions</span></span>

* <span data-ttu-id="f777e-350">Dans le panneau **projet** , tapez **ObjectSpawner** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="f777e-350">In the **Project** panel, type **ObjectSpawner** in the search box.</span></span> <span data-ttu-id="f777e-351">Vous pouvez également le trouver sous ressources/AppPrefabs/</span><span class="sxs-lookup"><span data-stu-id="f777e-351">You can also find it under Assets/AppPrefabs/</span></span>
* <span data-ttu-id="f777e-352">Faites glisser le Prefab **ObjectSpawner** dans le panneau de la **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="f777e-352">Drag the **ObjectSpawner** prefab into the **Hierarchy** panel.</span></span>
* <span data-ttu-id="f777e-353">Dans le volet **hiérarchie** , cliquez sur **ObjectSpawner** .</span><span class="sxs-lookup"><span data-stu-id="f777e-353">Click **ObjectSpawner** in the **Hierarchy** panel.</span></span>
* <span data-ttu-id="f777e-354">**ObjectSpawner** a un champ nommé **Color source**.</span><span class="sxs-lookup"><span data-stu-id="f777e-354">**ObjectSpawner** has a field named **Color Source**.</span></span>
* <span data-ttu-id="f777e-355">À partir du panneau **hiérarchie** , faites glisser la référence **ColorPickerWheel** dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="f777e-355">From the **Hierarchy** panel, drag the **ColorPickerWheel** reference into this field.</span></span>

![Inspecteur du Spawn d’objets](images/mr213-objectspawnercolorpickerwheel-650px.jpg)
* <span data-ttu-id="f777e-357">Cliquez sur le Prefab **ObjectSpawner** dans le panneau **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="f777e-357">Click the **ObjectSpawner** prefab in the **Hierarchy** panel.</span></span>
* <span data-ttu-id="f777e-358">Dans le panneau **inspecteur** , double-cliquez sur **ObjectSpawner** script pour afficher le code dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f777e-358">In the **Inspector** panel, double click **ObjectSpawner** Script to see the code in Visual Studio.</span></span>

<span data-ttu-id="f777e-359">**Script ObjectSpawner**</span><span class="sxs-lookup"><span data-stu-id="f777e-359">**ObjectSpawner script**</span></span>

<span data-ttu-id="f777e-360">Le **ObjectSpawner** instancie des copies d’un maillage primitif (cube, sphère, cylindre) dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="f777e-360">The **ObjectSpawner** instantiates copies of a primitive mesh (cube, sphere, cylinder) into the space.</span></span> <span data-ttu-id="f777e-361">Lorsqu’un **InteractionSourcePressed** est détecté, il vérifie la main et s’il s’agit d’un événement **InteractionSourcePressType.** dispose ou **InteractionSourcePressType. Select** .</span><span class="sxs-lookup"><span data-stu-id="f777e-361">When a **InteractionSourcePressed** is detected it checks the handedness and if it's an **InteractionSourcePressType.Grasp** or **InteractionSourcePressType.Select** event.</span></span>

<span data-ttu-id="f777e-362">Pour un événement **saisissant** , il incrémente l’index du type de maillage actuel (Sphere, cube, Cylinder)</span><span class="sxs-lookup"><span data-stu-id="f777e-362">For a **Grasp** event, it increments the index of current mesh type (sphere, cube, cylinder)</span></span>

```cs
private void InteractionSourcePressed(InteractionSourcePressedEventArgs obj)
{
    // Check handedness, see if it is left controller
    if (obj.state.source.handedness == handedness)
    {
        switch (obj.pressType)
        {
            // If it is Select button event, spawn object
            case InteractionSourcePressType.Select:
                if (state == StateEnum.Idle)
                {
                    // We've pressed the grasp - enter spawning state
                    state = StateEnum.Spawning;
                    SpawnObject();
                }
                break;

            // If it is Grasp button event
            case InteractionSourcePressType.Grasp:

                // Increment the index of current mesh type (sphere, cube, cylinder)
                meshIndex++;
                if (meshIndex >= NumAvailableMeshes)
                {
                    meshIndex = 0;
                }
                break;

            default:
                break;
        }
    }
}
```

<span data-ttu-id="f777e-363">Dans le cas d’un événement **Select** , dans **SpawnObject ()** , un nouvel objet est instancié, non apparenté et libéré dans le monde.</span><span class="sxs-lookup"><span data-stu-id="f777e-363">For a **Select** event, in **SpawnObject()**, a new object is instantiated, un-parented and released into the world.</span></span>

```cs
private void SpawnObject()
{
    // Instantiate the spawned object
    GameObject newObject = Instantiate(displayObject.gameObject, spawnParent);
    // Detatch the newly spawned object
    newObject.transform.parent = null;
    // Reset the scale transform to 1
    scaleParent.localScale = Vector3.one;
    // Set its material color so its material gets instantiated
    newObject.GetComponent<Renderer>().material.color = colorSource.SelectedColor;
}
```

<span data-ttu-id="f777e-364">**ObjectSpawner** utilise **ColorPickerWheel** pour définir la couleur du matériau de l’objet d’affichage.</span><span class="sxs-lookup"><span data-stu-id="f777e-364">The **ObjectSpawner** uses the **ColorPickerWheel** to set the color of the display object's material.</span></span> <span data-ttu-id="f777e-365">Les objets générés reçoivent une instance de ce document, de sorte qu’ils conservent leur couleur.</span><span class="sxs-lookup"><span data-stu-id="f777e-365">Spawned objects are given an instance of this material so they will retain their color.</span></span>
* <span data-ttu-id="f777e-366">**Enregistrez** la scène, puis cliquez sur le bouton **lecture** .</span><span class="sxs-lookup"><span data-stu-id="f777e-366">**Save** the scene and click the **play** button.</span></span>

<span data-ttu-id="f777e-367">Vous pouvez modifier les objets avec le bouton de sélection et générer des objets à l’aide du bouton Sélectionner.</span><span class="sxs-lookup"><span data-stu-id="f777e-367">You will be able to change the objects with the Grasp button and spawn objects with the Select button.</span></span>

## <a name="build-and-deploy-app-to-mixed-reality-portal"></a><span data-ttu-id="f777e-368">Créer et déployer une application sur un portail de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="f777e-368">Build and deploy app to Mixed Reality Portal</span></span>
* <span data-ttu-id="f777e-369">Dans Unity, sélectionnez **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="f777e-369">In Unity, select **File > Build Settings**.</span></span>
* <span data-ttu-id="f777e-370">Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène actuelle aux **scènes dans la build**.</span><span class="sxs-lookup"><span data-stu-id="f777e-370">Click **Add Open Scenes** to add current scene to the **Scenes In Build**.</span></span>
* <span data-ttu-id="f777e-371">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="f777e-371">Click **Build**.</span></span>
* <span data-ttu-id="f777e-372">Créez un **dossier** nommé «App».</span><span class="sxs-lookup"><span data-stu-id="f777e-372">Create a **New Folder** named "App".</span></span>
* <span data-ttu-id="f777e-373">Cliquez sur le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="f777e-373">Single click the **App** folder.</span></span>
* <span data-ttu-id="f777e-374">Cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="f777e-374">Click **Select Folder**.</span></span>
* <span data-ttu-id="f777e-375">Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f777e-375">When Unity is done, a File Explorer window will appear.</span></span>
* <span data-ttu-id="f777e-376">Ouvrez le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="f777e-376">Open the **App** folder.</span></span>
* <span data-ttu-id="f777e-377">Double-cliquez sur le fichier solution Visual Studio **YourSceneName. sln** .</span><span class="sxs-lookup"><span data-stu-id="f777e-377">Double click **YourSceneName.sln** Visual Studio Solution file.</span></span>
* <span data-ttu-id="f777e-378">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x64**.</span><span class="sxs-lookup"><span data-stu-id="f777e-378">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **X64**.</span></span>
* <span data-ttu-id="f777e-379">Cliquez sur la flèche déroulante en regard du bouton périphérique, puis sélectionnez **ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="f777e-379">Click on the drop-down arrow next to the Device button, and select **Local Machine**.</span></span>
* <span data-ttu-id="f777e-380">Cliquez sur déboguer **-> exécuter sans débogage** dans le menu ou appuyez sur **CTRL + F5**.</span><span class="sxs-lookup"><span data-stu-id="f777e-380">Click **Debug -> Start Without debugging** in the menu or press **Ctrl + F5**.</span></span>

<span data-ttu-id="f777e-381">L’application est désormais générée et installée dans le portail de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="f777e-381">Now the app is built and installed in Mixed Reality Portal.</span></span> <span data-ttu-id="f777e-382">Vous pouvez le relancer par le biais du menu Démarrer dans le portail de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="f777e-382">You can launch it again through Start menu in Mixed Reality Portal.</span></span>

## <a name="advanced-design---brush-tools-with-radial-layout"></a><span data-ttu-id="f777e-383">Outils de conception avancée avec disposition radiale</span><span class="sxs-lookup"><span data-stu-id="f777e-383">Advanced design - Brush tools with radial layout</span></span>

![Main MixedReality213](images/mr213-main-600px.jpg)

<span data-ttu-id="f777e-385">Dans ce chapitre, vous allez apprendre à remplacer le modèle de contrôleur de mouvement par défaut par une collection d’outils de pinceau personnalisée.</span><span class="sxs-lookup"><span data-stu-id="f777e-385">In this chapter, you will learn how to replace the default motion controller model with a custom brush tool collection.</span></span> <span data-ttu-id="f777e-386">Pour référence, vous pouvez trouver la scène terminée **MixedReality213Advanced** sous le  dossier Scenes.</span><span class="sxs-lookup"><span data-stu-id="f777e-386">For your reference, you can find the completed scene **MixedReality213Advanced** under **Scenes** folder.</span></span>

### <a name="instructions"></a><span data-ttu-id="f777e-387">Instructions</span><span class="sxs-lookup"><span data-stu-id="f777e-387">Instructions</span></span>

* <span data-ttu-id="f777e-388">Dans le panneau **projet** , tapez **BrushSelector** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="f777e-388">In the **Project** panel, type **BrushSelector** in the search box .</span></span> <span data-ttu-id="f777e-389">Vous pouvez également le trouver sous ressources/AppPrefabs/</span><span class="sxs-lookup"><span data-stu-id="f777e-389">You can also find it under Assets/AppPrefabs/</span></span>
* <span data-ttu-id="f777e-390">Faites glisser le Prefab **BrushSelector** dans le panneau de la **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="f777e-390">Drag the **BrushSelector** prefab into the **Hierarchy** panel.</span></span>
* <span data-ttu-id="f777e-391">Pour l’organisation, créez un GameObject vide  appelé pinceaux</span><span class="sxs-lookup"><span data-stu-id="f777e-391">For organization, create an empty GameObject called **Brushes**</span></span>
* <span data-ttu-id="f777e-392">Faites glisser les prefabs suivants du panneau **projet** vers les **pinceaux**</span><span class="sxs-lookup"><span data-stu-id="f777e-392">Drag following prefabs from the **Project** panel into **Brushes**</span></span>
    * <span data-ttu-id="f777e-393">Ressources/AppPrefabs/**BrushFat**</span><span class="sxs-lookup"><span data-stu-id="f777e-393">Assets/AppPrefabs/**BrushFat**</span></span>
    * <span data-ttu-id="f777e-394">Ressources/AppPrefabs/**BrushThin**</span><span class="sxs-lookup"><span data-stu-id="f777e-394">Assets/AppPrefabs/**BrushThin**</span></span>
    * <span data-ttu-id="f777e-395">Ressources/AppPrefabs/**gomme**</span><span class="sxs-lookup"><span data-stu-id="f777e-395">Assets/AppPrefabs/**Eraser**</span></span>
    * <span data-ttu-id="f777e-396">Ressources/AppPrefabs/**MarkerFat**</span><span class="sxs-lookup"><span data-stu-id="f777e-396">Assets/AppPrefabs/**MarkerFat**</span></span>
    * <span data-ttu-id="f777e-397">Ressources/AppPrefabs/**MarkerThin**</span><span class="sxs-lookup"><span data-stu-id="f777e-397">Assets/AppPrefabs/**MarkerThin**</span></span>
    * <span data-ttu-id="f777e-398">Ressources/AppPrefabs/**crayon**</span><span class="sxs-lookup"><span data-stu-id="f777e-398">Assets/AppPrefabs/**Pencil**</span></span>

![Pinceaux](images/mixedreality213-brushes-250px.png)
* <span data-ttu-id="f777e-400">Dans le volet **hiérarchie** , cliquez sur **MotionControllers** Prefab.</span><span class="sxs-lookup"><span data-stu-id="f777e-400">Click **MotionControllers** prefab in the **Hierarchy** panel.</span></span>
* <span data-ttu-id="f777e-401">Dans le panneau de l' **inspecteur** , décochez **toujours utiliser le modèle de remplacement à droite** sur le visualiseur du contrôleur de **mouvement** .</span><span class="sxs-lookup"><span data-stu-id="f777e-401">In the **Inspector** panel, uncheck **Always Use Alternate Right Model** on the **Motion Controller Visualizer**</span></span>
* <span data-ttu-id="f777e-402">Dans le volet **hiérarchie** , cliquez sur **BrushSelector**</span><span class="sxs-lookup"><span data-stu-id="f777e-402">In the **Hierarchy** panel, click **BrushSelector**</span></span>
* <span data-ttu-id="f777e-403">**BrushSelector** a un champ nommé **ColorPicker**</span><span class="sxs-lookup"><span data-stu-id="f777e-403">**BrushSelector** has a field named **ColorPicker**</span></span>
* <span data-ttu-id="f777e-404">À partir du panneau **hiérarchie** , faites glisser le champ **ColorPickerWheel** dans **ColorPicker** dans le panneau **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="f777e-404">From the **Hierarchy** panel, drag the **ColorPickerWheel** into **ColorPicker** field in the **Inspector** panel.</span></span>

![Assigner ColorPickerWheel à un sélecteur de pinceau](images/mr213-brushselector-500px.jpg)
* <span data-ttu-id="f777e-406">Dans le panneau **hiérarchie** , sous **BrushSelector** Prefab, sélectionnez l’objet **menu** .</span><span class="sxs-lookup"><span data-stu-id="f777e-406">In the **Hierarchy** panel, under **BrushSelector** prefab, select the **Menu** object.</span></span>
* <span data-ttu-id="f777e-407">Dans le volet de l' **inspecteur** , sous le composant **LineObjectCollection** , ouvrez la liste déroulante tableau d' **objets** .</span><span class="sxs-lookup"><span data-stu-id="f777e-407">In the **Inspector** panel, under the **LineObjectCollection** component, open the **Objects** array dropdown.</span></span> <span data-ttu-id="f777e-408">Vous verrez 6 emplacements vides.</span><span class="sxs-lookup"><span data-stu-id="f777e-408">You will see 6 empty slots.</span></span>
* <span data-ttu-id="f777e-409">Dans le volet **hiérarchie** , faites glisser chaque prefabs apparenté sous les pinceaux  gameobject dans n’importe quel ordre.</span><span class="sxs-lookup"><span data-stu-id="f777e-409">From the **Hierarchy** panel, drag each of the prefabs parented under the **Brushes** GameObject into these slots in any order.</span></span> <span data-ttu-id="f777e-410">(Assurez-vous de faire glisser le prefabs à partir de la scène, et non prefabs dans le dossier du projet.)</span><span class="sxs-lookup"><span data-stu-id="f777e-410">(Make sure you're dragging the prefabs from the scene, not the prefabs in the project folder.)</span></span>

![Sélecteur de pinceau](images/mr213-brushselectorbrushes-700px.jpg)

<span data-ttu-id="f777e-412">**BrushSelector Prefab**</span><span class="sxs-lookup"><span data-stu-id="f777e-412">**BrushSelector prefab**</span></span>

<span data-ttu-id="f777e-413">Étant donné que **BrushSelector** hérite de **AttachToController**, il affiche les options de **remise** et d' **élément** dans le panneau **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="f777e-413">Since the **BrushSelector** inherits **AttachToController**, it shows **Handedness** and **Element** options in the **Inspector** panel.</span></span> <span data-ttu-id="f777e-414">Nous avons sélectionné la **pose** de **droite** et de pointage pour attacher les outils de pinceau au contrôleur de droite avec la direction vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="f777e-414">We selected **Right** and **Pointing Pose** to attach brush tools to the right hand controller with forward direction.</span></span>

<span data-ttu-id="f777e-415">Le **BrushSelector** utilise deux utilitaires:</span><span class="sxs-lookup"><span data-stu-id="f777e-415">The **BrushSelector** makes use of two utilities:</span></span>
* <span data-ttu-id="f777e-416">**Ellipse**: utilisée pour générer des points dans l’espace le long d’une forme d’ellipse.</span><span class="sxs-lookup"><span data-stu-id="f777e-416">**Ellipse**: used to generate points in space along an ellipse shape.</span></span>
* <span data-ttu-id="f777e-417">**LineObjectCollection**: distribue les objets à l’aide des points générés par n’importe quelle classe de lignes (par ex., ellipse).</span><span class="sxs-lookup"><span data-stu-id="f777e-417">**LineObjectCollection**: distributes objects using the points generated by any Line class (eg, Ellipse).</span></span> <span data-ttu-id="f777e-418">C’est ce que nous allons utiliser pour placer nos pinceaux le long de la forme d’ellipse.</span><span class="sxs-lookup"><span data-stu-id="f777e-418">This is what we'll be using to place our brushes along the Ellipse shape.</span></span>

<span data-ttu-id="f777e-419">Lorsqu’ils sont combinés, ces utilitaires peuvent être utilisés pour créer un menu radial.</span><span class="sxs-lookup"><span data-stu-id="f777e-419">When combined, these utilities can be used to create a radial menu.</span></span>

<span data-ttu-id="f777e-420">**Script LineObjectCollection**</span><span class="sxs-lookup"><span data-stu-id="f777e-420">**LineObjectCollection script**</span></span>

<span data-ttu-id="f777e-421">**LineObjectCollection** possède des contrôles pour la taille, la position et la rotation des objets distribués le long de la ligne.</span><span class="sxs-lookup"><span data-stu-id="f777e-421">**LineObjectCollection** has controls for the size, position and rotation of objects distributed along its line.</span></span> <span data-ttu-id="f777e-422">Cela est utile pour créer des menus radiaux tels que le sélecteur de pinceau.</span><span class="sxs-lookup"><span data-stu-id="f777e-422">This is useful for creating radial menus like the brush selector.</span></span> <span data-ttu-id="f777e-423">Pour créer l’apparence des pinceaux qui s’ajustent à partir de rien, car ils approchent la position sélectionnée au centre, les pics de la courbe **ObjectScale** dans les bords du centre et des bandes.</span><span class="sxs-lookup"><span data-stu-id="f777e-423">To create the appearance of brushes that scale up from nothing as they approach the center selected position, the **ObjectScale** curve peaks in the center and tapers off at the edges.</span></span>

<span data-ttu-id="f777e-424">**Script BrushSelector**</span><span class="sxs-lookup"><span data-stu-id="f777e-424">**BrushSelector script**</span></span>

<span data-ttu-id="f777e-425">Dans le cas de **BrushSelector**, nous avons choisi d’utiliser l’animation procédurale.</span><span class="sxs-lookup"><span data-stu-id="f777e-425">In the case of the **BrushSelector**, we've chosen to use procedural animation.</span></span> <span data-ttu-id="f777e-426">Tout d’abord, les modèles de pinceau sont distribués dans une ellipse par le script **LineObjectCollection** .</span><span class="sxs-lookup"><span data-stu-id="f777e-426">First, brush models are distributed in an ellipse by the **LineObjectCollection** script.</span></span> <span data-ttu-id="f777e-427">Ensuite, chaque pinceau est chargé de conserver sa position dans la main de l’utilisateur en fonction de sa valeur **DisplayMode** , qui change en fonction de la sélection.</span><span class="sxs-lookup"><span data-stu-id="f777e-427">Then, each brush is responsible for maintaining its position in the user's hand based on its **DisplayMode** value, which changes based on the selection.</span></span> <span data-ttu-id="f777e-428">Nous avons choisi une approche procédurale en raison de la probabilité élevée que les transitions de position de pinceau soient interrompues lorsque l’utilisateur sélectionne des pinceaux.</span><span class="sxs-lookup"><span data-stu-id="f777e-428">We chose a procedural approach because of the high probability of brush position transitions being interrupted as the user selects brushes.</span></span> <span data-ttu-id="f777e-429">Les animations Mecanim peuvent gérer les interruptions de manière appropriée, mais elles ont tendance à être plus compliquées qu’une simple opération Lerp.</span><span class="sxs-lookup"><span data-stu-id="f777e-429">Mecanim animations can handle interruptions gracefully, but it tends to be more complicated than a simple Lerp operation.</span></span>

<span data-ttu-id="f777e-430">**BrushSelector** utilise une combinaison des deux.</span><span class="sxs-lookup"><span data-stu-id="f777e-430">**BrushSelector** uses a combination of both.</span></span> <span data-ttu-id="f777e-431">Lorsque l’entrée de pavé tactile est détectée, les options de pinceau deviennent visibles et évoluent le long du menu radial.</span><span class="sxs-lookup"><span data-stu-id="f777e-431">When touchpad input is detected, brush options become visible and scale up along the radial menu.</span></span> <span data-ttu-id="f777e-432">Après un délai d’expiration (qui indique que l’utilisateur a effectué une sélection), les options de pinceau remontent d’une nouvelle échelle, en laissant uniquement le pinceau sélectionné.</span><span class="sxs-lookup"><span data-stu-id="f777e-432">After a timeout period (which indicates that the user has made a selection) the brush options scale down again, leaving only the selected brush.</span></span>

<span data-ttu-id="f777e-433">**Visualisation de l’entrée du pavé tactile**</span><span class="sxs-lookup"><span data-stu-id="f777e-433">**Visualizing touchpad input**</span></span>

<span data-ttu-id="f777e-434">Même dans les cas où le modèle de contrôleur a été complètement remplacé, il peut être utile d’afficher l’entrée sur les entrées du modèle d’origine.</span><span class="sxs-lookup"><span data-stu-id="f777e-434">Even in cases where the controller model has been completely replaced, it can be helpful to show input on the original model inputs.</span></span> <span data-ttu-id="f777e-435">Cela permet de reconstituer les actions de l’utilisateur en réalité.</span><span class="sxs-lookup"><span data-stu-id="f777e-435">This helps to ground the user's actions in reality.</span></span> <span data-ttu-id="f777e-436">Pour le **BrushSelector** , nous avons choisi de rendre le pavé tactile brièvement visible lors de la réception de l’entrée.</span><span class="sxs-lookup"><span data-stu-id="f777e-436">For the **BrushSelector** we've chosen to make the touchpad briefly visible when the input is received.</span></span> <span data-ttu-id="f777e-437">Pour ce faire, récupérez l’élément de pavé tactile à partir du contrôleur, en remplaçant son matériau par un matériau personnalisé, puis en appliquant un dégradé à la couleur de ce matériau en fonction de la dernière entrée de pavé tactile reçue.</span><span class="sxs-lookup"><span data-stu-id="f777e-437">This was done by retrieving the Touchpad element from the controller, replacing its material with a custom material, then applying a gradient to that material's color based on the last time touchpad input was received.</span></span>

```cs
protected override void OnAttachToController()
{
    // Turn off the default controller's renderers
    controller.SetRenderersVisible(false);

    // Get the touchpad and assign our custom material to it
    Transform touchpad;
    if (controller.TryGetElement(MotionControllerInfo.ControllerElementEnum.Touchpad, out touchpad))
    {
        touchpadRenderer = touchpad.GetComponentInChildren<MeshRenderer>();
        originalTouchpadMaterial = touchpadRenderer.material;
        touchpadRenderer.material = touchpadMaterial;
        touchpadRenderer.enabled = true;
    }
            
    // Subscribe to input now that we're parented under the controller
    InteractionManager.InteractionSourceUpdated += InteractionSourceUpdated;
}

private void Update()
{
    ...
    // Update our touchpad material
    Color glowColor = touchpadColor.Evaluate((Time.unscaledTime - touchpadTouchTime) / touchpadGlowLossTime);
    touchpadMaterial.SetColor("_EmissionColor", glowColor);
    touchpadMaterial.SetColor("_Color", glowColor);
    ...
}
```

<span data-ttu-id="f777e-438">**Sélection de l’outil pinceau avec entrée de pavé tactile**</span><span class="sxs-lookup"><span data-stu-id="f777e-438">**Brush tool selection with touchpad input**</span></span>

<span data-ttu-id="f777e-439">Lorsque le sélecteur de pinceau détecte l’entrée appuyée du pavé tactile, il vérifie la position de l’entrée pour déterminer si elle se trouvait à gauche ou à droite.</span><span class="sxs-lookup"><span data-stu-id="f777e-439">When the brush selector detects touchpad's pressed input, it checks the position of the input to determine if it was to the left or right.</span></span>

<span data-ttu-id="f777e-440">**Épaisseur du trait avec selectPressedAmount**</span><span class="sxs-lookup"><span data-stu-id="f777e-440">**Stroke thickness with selectPressedAmount**</span></span>

<span data-ttu-id="f777e-441">Au lieu de l’événement **InteractionSourcePressType. Select** dans le **InteractionSourcePressed ()** , vous pouvez récupérer la valeur analogique du montant appuyé par le biais de **selectPressedAmount**.</span><span class="sxs-lookup"><span data-stu-id="f777e-441">Instead of the **InteractionSourcePressType.Select** event in the **InteractionSourcePressed()**, you can get the analog value of the pressed amount through **selectPressedAmount**.</span></span> <span data-ttu-id="f777e-442">Cette valeur peut être extraite dans **InteractionSourceUpdated ()** .</span><span class="sxs-lookup"><span data-stu-id="f777e-442">This value can be retrieved in **InteractionSourceUpdated()**.</span></span>

```cs
private void InteractionSourceUpdated(InteractionSourceUpdatedEventArgs obj)
{
    if (obj.state.source.handedness == handedness)
    {
        if (obj.state.touchpadPressed)
        {
            // Check which side we clicked
            if (obj.state.touchpadPosition.x < 0)
            {
                currentAction = SwipeEnum.Left;
            }
            else
            {
                currentAction = SwipeEnum.Right;
            }

            // Ping the touchpad material so it gets bright
            touchpadTouchTime = Time.unscaledTime;
        }

        if (activeBrush != null)
        {
            // If the pressed amount is greater than our threshold, draw
            if (obj.state.selectPressedAmount >= selectPressedDrawThreshold)
            {
                activeBrush.Draw = true;
                activeBrush.Width = ProcessSelectPressedAmount(obj.state.selectPressedAmount);
            }
            else
            {
                // Otherwise, stop drawing
                activeBrush.Draw = false;
                selectPressedSmooth = 0f;
            }
        }
    }
}
```

<span data-ttu-id="f777e-443">**Script de la gomme**</span><span class="sxs-lookup"><span data-stu-id="f777e-443">**Eraser script**</span></span>

<span data-ttu-id="f777e-444">**Gomme** est un type spécial de pinceau qui remplace la fonction **DrawOverTime ()** du **pinceau**de base.</span><span class="sxs-lookup"><span data-stu-id="f777e-444">**Eraser** is a special type of brush that overrides the base **Brush**'s **DrawOverTime()** function.</span></span> <span data-ttu-id="f777e-445">Bien que Draw ait la valeur true, la gomme vérifie si son info-bulle croise les traits de pinceau existants.</span><span class="sxs-lookup"><span data-stu-id="f777e-445">While Draw is true, the eraser checks to see if its tip intersects with any existing brush strokes.</span></span> <span data-ttu-id="f777e-446">Si c’est le cas, ils sont ajoutés à une file d’attente pour être réduits et supprimés.</span><span class="sxs-lookup"><span data-stu-id="f777e-446">If it does, they are added to a queue to be shrunk down and deleted.</span></span>

## <a name="advanced-design---teleportation-and-locomotion"></a><span data-ttu-id="f777e-447">Conception avancée-téléportage et locomotion</span><span class="sxs-lookup"><span data-stu-id="f777e-447">Advanced design - Teleportation and locomotion</span></span>

<span data-ttu-id="f777e-448">Si vous souhaitez autoriser l’utilisateur à se déplacer dans la scène avec la téléportage à l’aide du stick analogique, utilisez **MixedRealityCameraParent** au lieu de **MixedRealityCamera**.</span><span class="sxs-lookup"><span data-stu-id="f777e-448">If you want to allow the user to move around the scene with teleportation using thumbstick, use **MixedRealityCameraParent** instead of **MixedRealityCamera**.</span></span> <span data-ttu-id="f777e-449">Vous devez également ajouter **InputManager** et **DefaultCusor**.</span><span class="sxs-lookup"><span data-stu-id="f777e-449">You also need to add **InputManager** and **DefaultCusor**.</span></span> <span data-ttu-id="f777e-450">Étant donné que **MixedRealityCameraParent** contient déjà des **MotionControllers** et des **limites** en tant que composants enfants, vous devez supprimer les Prefab de **MotionControllers** et d' **environnement** existants.</span><span class="sxs-lookup"><span data-stu-id="f777e-450">Since **MixedRealityCameraParent** already includes **MotionControllers** and **Boundary** as child components, you should remove existing **MotionControllers** and **Environment** prefab.</span></span>

### <a name="instructions"></a><span data-ttu-id="f777e-451">Instructions</span><span class="sxs-lookup"><span data-stu-id="f777e-451">Instructions</span></span>

* <span data-ttu-id="f777e-452">Dans le volet **hiérarchie** , supprimez **MixedRealityCamera**, **Environment** et **MotionControllers**</span><span class="sxs-lookup"><span data-stu-id="f777e-452">In the **Hierarchy** panel, delete **MixedRealityCamera**, **Environment** and **MotionControllers**</span></span>
* <span data-ttu-id="f777e-453">Dans le **volet de projet**, recherchez et faites glisser le prefabs suivant dans le volet de **hiérarchie** :</span><span class="sxs-lookup"><span data-stu-id="f777e-453">From the **Project panel**, search and drag the following prefabs into the **Hierarchy** panel:</span></span>
    * <span data-ttu-id="f777e-454">Ressources/AppPrefabs/entrée/Prefabs/**MixedRealityCameraParent**</span><span class="sxs-lookup"><span data-stu-id="f777e-454">Assets/AppPrefabs/Input/Prefabs/**MixedRealityCameraParent**</span></span>
    * <span data-ttu-id="f777e-455">Ressources/AppPrefabs/entrée/Prefabs/**InputManager**</span><span class="sxs-lookup"><span data-stu-id="f777e-455">Assets/AppPrefabs/Input/Prefabs/**InputManager**</span></span>
    * <span data-ttu-id="f777e-456">Ressources/AppPrefabs/entrée/Prefabs/Cursor/**DefaultCursor**</span><span class="sxs-lookup"><span data-stu-id="f777e-456">Assets/AppPrefabs/Input/Prefabs/Cursor/**DefaultCursor**</span></span>

![Parent de la caméra de réalité mixte](images/mr213-cameraparent-300px.png)
* <span data-ttu-id="f777e-458">Dans le volet **hiérarchie** , cliquez sur **Gestionnaire d’entrée** .</span><span class="sxs-lookup"><span data-stu-id="f777e-458">In the **Hierarchy** panel, click **Input Manager**</span></span>
* <span data-ttu-id="f777e-459">Dans le volet de l' **inspecteur** , faites défiler jusqu’à la section du **Sélecteur de pointeur simple simple**</span><span class="sxs-lookup"><span data-stu-id="f777e-459">In the **Inspector** panel, scroll down to the **Simple Single Pointer Selector** section</span></span>
* <span data-ttu-id="f777e-460">À partir du panneau **hiérarchie** , faites glisser **DefaultCursor** dans le champ **Cursor**</span><span class="sxs-lookup"><span data-stu-id="f777e-460">From the **Hierarchy** panel, drag **DefaultCursor** into **Cursor** field</span></span>

![Attribution de DefaultCursor](images/mr213-defaultcursor-500px.png)
* <span data-ttu-id="f777e-462">**Enregistrez** la scène, puis cliquez sur le bouton **lecture** .</span><span class="sxs-lookup"><span data-stu-id="f777e-462">**Save** the scene and click the **play** button.</span></span> <span data-ttu-id="f777e-463">Vous serez en mesure d’utiliser le stick analogique pour faire pivoter vers la gauche/droite ou la téléporter.</span><span class="sxs-lookup"><span data-stu-id="f777e-463">You will be able to use the thumbstick to rotate left/right or teleport.</span></span>

## <a name="the-end"></a><span data-ttu-id="f777e-464">La fin</span><span class="sxs-lookup"><span data-stu-id="f777e-464">The end</span></span>

<span data-ttu-id="f777e-465">Et c’est la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f777e-465">And that's the end of this tutorial!</span></span> <span data-ttu-id="f777e-466">Vous avez appris à:</span><span class="sxs-lookup"><span data-stu-id="f777e-466">You learned:</span></span>
* <span data-ttu-id="f777e-467">Comment utiliser les modèles de contrôleur de mouvement dans le mode jeu et le runtime d’Unity.</span><span class="sxs-lookup"><span data-stu-id="f777e-467">How to work with motion controller models in Unity's game mode and runtime.</span></span>
* <span data-ttu-id="f777e-468">Comment utiliser différents types d’événements de bouton et leurs applications.</span><span class="sxs-lookup"><span data-stu-id="f777e-468">How to use different types of button events and their applications.</span></span>
* <span data-ttu-id="f777e-469">Comment superposer des éléments d’interface utilisateur en plus du contrôleur ou le personnaliser entièrement.</span><span class="sxs-lookup"><span data-stu-id="f777e-469">How to overlay UI elements on top of the controller or fully customize it.</span></span>

<span data-ttu-id="f777e-470">Vous êtes maintenant prêt à commencer à créer votre propre expérience immersive avec les contrôleurs motion.</span><span class="sxs-lookup"><span data-stu-id="f777e-470">You are now ready to start creating your own immersive experience with motion controllers!</span></span>

## <a name="completed-scenes"></a><span data-ttu-id="f777e-471">Scènes terminées</span><span class="sxs-lookup"><span data-stu-id="f777e-471">Completed scenes</span></span>

* <span data-ttu-id="f777e-472">Dans le panneau **projet** d’Unity,  cliquez sur le dossier Scenes.</span><span class="sxs-lookup"><span data-stu-id="f777e-472">In Unity's **Project** panel click on the **Scenes** folder.</span></span>
* <span data-ttu-id="f777e-473">Vous trouverez deux Unity Sceens **MixedReality213** et **MixedReality213Advanced**.</span><span class="sxs-lookup"><span data-stu-id="f777e-473">You will find two Unity sceens **MixedReality213** and **MixedReality213Advanced**.</span></span>
    * <span data-ttu-id="f777e-474">**MixedReality213**: Scène terminée avec un seul pinceau</span><span class="sxs-lookup"><span data-stu-id="f777e-474">**MixedReality213**: Completed scene with single brush</span></span>
    * <span data-ttu-id="f777e-475">**MixedReality213Advanced**: Scène terminée avec un pinceau multiple avec l’exemple de montant de pression du bouton Sélectionner</span><span class="sxs-lookup"><span data-stu-id="f777e-475">**MixedReality213Advanced**: Completed scene with multiple brush with select button's press amount example</span></span>

## <a name="see-also"></a><span data-ttu-id="f777e-476">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f777e-476">See also</span></span>

* [<span data-ttu-id="f777e-477">Fichiers projet d’entrée 213</span><span class="sxs-lookup"><span data-stu-id="f777e-477">MR Input 213 project files</span></span>](https://github.com/Microsoft/MixedReality213)
* [<span data-ttu-id="f777e-478">Boîte à outils de réalité mixte-scène de test du contrôleur de mouvement</span><span class="sxs-lookup"><span data-stu-id="f777e-478">Mixed Reality Toolkit - Motion Controller Test scene</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/Input/Scenes)
* [<span data-ttu-id="f777e-479">Kit de pratiques de réalité mixte-mécanisme de manipulation</span><span class="sxs-lookup"><span data-stu-id="f777e-479">Mixed Reality Toolkit - Grab Mechanics</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/MotionControllers-GrabMechanics)
* [<span data-ttu-id="f777e-480">Instructions de développement du contrôleur motion</span><span class="sxs-lookup"><span data-stu-id="f777e-480">Motion controller development guidelines</span></span>](motion-controllers.md)
