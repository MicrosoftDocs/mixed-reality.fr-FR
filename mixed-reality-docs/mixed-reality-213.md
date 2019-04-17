---
title: Entrée M. 213
description: Suivez ce didacticiel de codage à l’aide de Unity, Visual Studio et des casques IMMERSIFS pour connaître les détails de contrôleurs de mouvement.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, immersive, de mouvement contrôleur, academy, didacticiel
ms.openlocfilehash: 85449795a4fb3d182101cb5b4c4ce3fe85b009c0
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596965"
---
>[!NOTE]
><span data-ttu-id="bf003-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="bf003-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="bf003-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="bf003-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="bf003-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="bf003-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="bf003-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="bf003-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="bf003-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="bf003-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="bf003-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="bf003-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-input-213-motion-controllers"></a><span data-ttu-id="bf003-110">Entrée M. 213 : Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="bf003-110">MR Input 213: Motion controllers</span></span>

<span data-ttu-id="bf003-111">Dans le monde de réalité mixte, les contrôleurs de mouvement ajoutent un autre niveau d’interactivité.</span><span class="sxs-lookup"><span data-stu-id="bf003-111">Motion controllers in the mixed reality world add another level of interactivity.</span></span> <span data-ttu-id="bf003-112">Avec [contrôleurs de mouvement](motion-controllers.md), nous pouvons directement interagir avec des objets de façon plus naturelle, similaire à vos interactions physiques dans la vie réelle, augmentant immersion et raviront dans votre expérience d’application.</span><span class="sxs-lookup"><span data-stu-id="bf003-112">With [motion controllers](motion-controllers.md), we can directly interact with objects in a more natural way, similar to our physical interactions in real life, increasing immersion and delight in your app experience.</span></span>

<span data-ttu-id="bf003-113">213 d’entrée M., nous allons explorer les événements d’entrée du contrôleur de mouvement en créant une expérience de peinture spatiale simple.</span><span class="sxs-lookup"><span data-stu-id="bf003-113">In MR Input 213, we will explore the motion controller's input events by creating a simple spatial painting experience.</span></span> <span data-ttu-id="bf003-114">Avec cette application, les utilisateurs peuvent peindre dans un espace tridimensionnel avec différents types de pinceaux et couleurs.</span><span class="sxs-lookup"><span data-stu-id="bf003-114">With this app, users can paint in three-dimensional space with various types of brushes and colors.</span></span>

## <a name="topics-covered-in-this-tutorial"></a><span data-ttu-id="bf003-115">Sujets abordés dans ce didacticiel</span><span class="sxs-lookup"><span data-stu-id="bf003-115">Topics covered in this tutorial</span></span>

|![MixedReality213 Topic1](images/mr213-topic1.png)|![MixedReality213 Topic2](images/mr213-topic2.png)|![MixedReality213 Topic3](images/mr213-topic3.png)|
| :--- | :--- | :--- |
|<span data-ttu-id="bf003-119">**Visualisation du contrôleur**</span><span class="sxs-lookup"><span data-stu-id="bf003-119">**Controller visualization**</span></span>|<span data-ttu-id="bf003-120">**Événements d’entrée de contrôleur**</span><span class="sxs-lookup"><span data-stu-id="bf003-120">**Controller input events**</span></span>|<span data-ttu-id="bf003-121">**Contrôleur personnalisé et l’interface utilisateur**</span><span class="sxs-lookup"><span data-stu-id="bf003-121">**Custom controller and UI**</span></span>|
|<span data-ttu-id="bf003-122">Découvrez comment afficher les modèles de contrôleur de mouvement dans le mode de jeu d’Unity et d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bf003-122">Learn how to render motion controller models in Unity's game mode and runtime.</span></span>|<span data-ttu-id="bf003-123">Comprendre les différents types d’événements de bouton et de leurs applications.</span><span class="sxs-lookup"><span data-stu-id="bf003-123">Understand different types of button events and their applications.</span></span>|<span data-ttu-id="bf003-124">Apprenez à superposer des éléments d’interface utilisateur sur le contrôleur ou de personnaliser entièrement.</span><span class="sxs-lookup"><span data-stu-id="bf003-124">Learn how to overlay UI elements on top of the controller or fully customize it.</span></span>|

## <a name="device-support"></a><span data-ttu-id="bf003-125">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="bf003-125">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="bf003-126">Cours</span><span class="sxs-lookup"><span data-stu-id="bf003-126">Course</span></span></th><th style="width:150px"> <span data-ttu-id="bf003-127"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="bf003-127"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="bf003-128"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="bf003-128"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="bf003-129">Entrée M. 213 : Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="bf003-129">MR Input 213: Motion controllers</span></span></td><td style="text-align: center;"> </td><td style="text-align: center;"> <span data-ttu-id="bf003-130">✔️</span><span class="sxs-lookup"><span data-stu-id="bf003-130">✔️</span></span></td>
</tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="bf003-131">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="bf003-131">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="bf003-132">Prérequis</span><span class="sxs-lookup"><span data-stu-id="bf003-132">Prerequisites</span></span>

<span data-ttu-id="bf003-133">Consultez la liste de vérification d’installation pour des casques IMMERSIFS sur [cette page](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="bf003-133">See the installation checklist for immersive headsets on [this page](install-the-tools.md).</span></span>

* <span data-ttu-id="bf003-134">Ce didacticiel requiert [Unity 2017.2.1p2](https://beta.unity3d.com/download/1dc514532f08/UnityDownloadAssistant-2017.2.1p2.exe)</span><span class="sxs-lookup"><span data-stu-id="bf003-134">This tutorial requires [Unity 2017.2.1p2](https://beta.unity3d.com/download/1dc514532f08/UnityDownloadAssistant-2017.2.1p2.exe)</span></span>

### <a name="project-files"></a><span data-ttu-id="bf003-135">Fichiers projet</span><span class="sxs-lookup"><span data-stu-id="bf003-135">Project files</span></span>

* <span data-ttu-id="bf003-136">[Télécharger les fichiers](https://github.com/Microsoft/MixedReality213/archive/master.zip) requise par le projet et extrayez les fichiers sur le bureau.</span><span class="sxs-lookup"><span data-stu-id="bf003-136">[Download the files](https://github.com/Microsoft/MixedReality213/archive/master.zip) required by the project and extract the files to the Desktop.</span></span>

>[!NOTE]
><span data-ttu-id="bf003-137">Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/MixedReality213).</span><span class="sxs-lookup"><span data-stu-id="bf003-137">If you want to look through the source code before downloading, it's [available on GitHub](https://github.com/Microsoft/MixedReality213).</span></span>

## <a name="unity-setup"></a><span data-ttu-id="bf003-138">Programme d’installation Unity</span><span class="sxs-lookup"><span data-stu-id="bf003-138">Unity setup</span></span>

>[!VIDEO https://www.youtube.com/embed/cBAOALaHys4]

### <a name="objectives"></a><span data-ttu-id="bf003-139">Objectifs</span><span class="sxs-lookup"><span data-stu-id="bf003-139">Objectives</span></span>

* <span data-ttu-id="bf003-140">Optimiser le développement de Unity pour Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="bf003-140">Optimize Unity for Windows Mixed Reality development</span></span>
* <span data-ttu-id="bf003-141">Le programme d’installation de caméra de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="bf003-141">Setup Mixed Reality Camera</span></span>
* <span data-ttu-id="bf003-142">Environnement de configuration</span><span class="sxs-lookup"><span data-stu-id="bf003-142">Setup environment</span></span>

### <a name="instructions"></a><span data-ttu-id="bf003-143">Instructions</span><span class="sxs-lookup"><span data-stu-id="bf003-143">Instructions</span></span>

* <span data-ttu-id="bf003-144">Démarrez Unity.</span><span class="sxs-lookup"><span data-stu-id="bf003-144">Start Unity.</span></span>
* <span data-ttu-id="bf003-145">Sélectionnez **Open**.</span><span class="sxs-lookup"><span data-stu-id="bf003-145">Select **Open**.</span></span>
* <span data-ttu-id="bf003-146">Accédez à votre bureau et de rechercher le **MixedReality213-master** dossier vous non précédemment archivé.</span><span class="sxs-lookup"><span data-stu-id="bf003-146">Navigate to your Desktop and find the **MixedReality213-master** folder you previously unarchived.</span></span>
* <span data-ttu-id="bf003-147">Cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="bf003-147">Click **Select Folder**.</span></span>
* <span data-ttu-id="bf003-148">Une fois que Unity a terminé le chargement des fichiers de projet, vous serez en mesure de voir éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="bf003-148">Once Unity finishes loading project files, you will be able to see Unity editor.</span></span>
* <span data-ttu-id="bf003-149">Dans Unity, sélectionnez **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="bf003-149">In Unity, select **File > Build Settings**.</span></span>

![MR213_BuildSettings](images/mr213-buildsettings-450px.png)
* <span data-ttu-id="bf003-151">Sélectionnez **plateforme Windows universelle** dans le **plateforme** liste et cliquez sur le **plateforme de commutation** bouton.</span><span class="sxs-lookup"><span data-stu-id="bf003-151">Select **Universal Windows Platform** in the **Platform** list and click the **Switch Platform** button.</span></span>
* <span data-ttu-id="bf003-152">Appareil cible la valeur **n’importe quel appareil**</span><span class="sxs-lookup"><span data-stu-id="bf003-152">Set Target Device to **Any device**</span></span>
* <span data-ttu-id="bf003-153">Définissez le Type de Build sur **D3D**</span><span class="sxs-lookup"><span data-stu-id="bf003-153">Set Build Type to **D3D**</span></span>
* <span data-ttu-id="bf003-154">Définissez le SDK **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="bf003-154">Set SDK to **Latest Installed**</span></span>
* <span data-ttu-id="bf003-155">Vérifiez **Unity C# projets**</span><span class="sxs-lookup"><span data-stu-id="bf003-155">Check **Unity C# Projects**</span></span>
    * <span data-ttu-id="bf003-156">Cela vous permet de que modifier les fichiers de script dans le projet Visual Studio sans régénération du projet Unity.</span><span class="sxs-lookup"><span data-stu-id="bf003-156">This allows you modify script files in the Visual Studio project without rebuilding Unity project.</span></span>
* <span data-ttu-id="bf003-157">Cliquez sur **paramètres du lecteur**.</span><span class="sxs-lookup"><span data-stu-id="bf003-157">Click **Player Settings**.</span></span>
* <span data-ttu-id="bf003-158">Dans le **inspecteur** Panneau de configuration, faites défiler vers le bas</span><span class="sxs-lookup"><span data-stu-id="bf003-158">In the **Inspector** panel, scroll down to the bottom</span></span>
* <span data-ttu-id="bf003-159">Dans paramètres XR, vérifiez **virtuel pris en charge de réalité**</span><span class="sxs-lookup"><span data-stu-id="bf003-159">In XR Settings, check **Virtual Reality Supported**</span></span>
* <span data-ttu-id="bf003-160">Sous SDK de réalité virtuelle, sélectionnez **Windows Mixed Reality**</span><span class="sxs-lookup"><span data-stu-id="bf003-160">Under Virtual Reality SDKs, select **Windows Mixed Reality**</span></span>

![MR213_XRSettings](images/mr213-xrsettings-500px.png)
* <span data-ttu-id="bf003-162">Fermer **paramètres de Build** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="bf003-162">Close **Build Settings** window.</span></span>

### <a name="project-structure"></a><span data-ttu-id="bf003-163">Structure de projet</span><span class="sxs-lookup"><span data-stu-id="bf003-163">Project structure</span></span>

<span data-ttu-id="bf003-164">Ce didacticiel utilise  **[Toolkit de réalité mixte - Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity)**.</span><span class="sxs-lookup"><span data-stu-id="bf003-164">This tutorial uses **[Mixed Reality Toolkit - Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity)**.</span></span> <span data-ttu-id="bf003-165">Vous pouvez trouver les versions sur [cette page](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases).</span><span class="sxs-lookup"><span data-stu-id="bf003-165">You can find the releases on [this page](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases).</span></span>

![ProjectStructure](images/mr213-projectstructure-650px.png)

<span data-ttu-id="bf003-167">**Arrière-plan terminé pour votre référence**</span><span class="sxs-lookup"><span data-stu-id="bf003-167">**Completed scenes for your reference**</span></span>
* <span data-ttu-id="bf003-168">Vous trouverez deux scènes Unity terminées sous **scènes** dossier.</span><span class="sxs-lookup"><span data-stu-id="bf003-168">You will find two completed Unity scenes under **Scenes** folder.</span></span>
    * <span data-ttu-id="bf003-169">**MixedReality213**: Scène terminée avec un pinceau unique</span><span class="sxs-lookup"><span data-stu-id="bf003-169">**MixedReality213**: Completed scene with single brush</span></span>
    * <span data-ttu-id="bf003-170">**MixedReality213Advanced**: Fin de scène pour conception avancée avec plusieurs pinceaux</span><span class="sxs-lookup"><span data-stu-id="bf003-170">**MixedReality213Advanced**: Completed scene for advanced design with multiple brushes</span></span>

<span data-ttu-id="bf003-171">**Nouvelle installation de scène pour le didacticiel**</span><span class="sxs-lookup"><span data-stu-id="bf003-171">**New Scene setup for the tutorial**</span></span>
* <span data-ttu-id="bf003-172">Dans Unity, cliquez sur **fichier > nouvelle scène**</span><span class="sxs-lookup"><span data-stu-id="bf003-172">In Unity, click **File > New Scene**</span></span>
* <span data-ttu-id="bf003-173">Supprimer **caméra principale** et **lumière directionnelle**</span><span class="sxs-lookup"><span data-stu-id="bf003-173">Delete **Main Camera** and **Directional Light**</span></span>
* <span data-ttu-id="bf003-174">À partir de la **panneau projet**, recherchez et faites glisser les prefabs suivants dans le **hiérarchie** panneau :</span><span class="sxs-lookup"><span data-stu-id="bf003-174">From the **Project panel**, search and drag the following prefabs into the **Hierarchy** panel:</span></span>
    * <span data-ttu-id="bf003-175">Assets/HoloToolkit/Input/Prefabs/**MixedRealityCamera**</span><span class="sxs-lookup"><span data-stu-id="bf003-175">Assets/HoloToolkit/Input/Prefabs/**MixedRealityCamera**</span></span>
    * <span data-ttu-id="bf003-176">Assets/AppPrefabs/**Environment**</span><span class="sxs-lookup"><span data-stu-id="bf003-176">Assets/AppPrefabs/**Environment**</span></span>

![Appareil photo et l’environnement](images/mr213-cameraenvironment-300px.jpg)
* <span data-ttu-id="bf003-178">Il existe deux prefabs appareil photo dans la boîte à outils de réalité mixte :</span><span class="sxs-lookup"><span data-stu-id="bf003-178">There are two camera prefabs in Mixed Reality Toolkit:</span></span>
    * <span data-ttu-id="bf003-179">**MixedRealityCamera.prefab**: Caméra uniquement</span><span class="sxs-lookup"><span data-stu-id="bf003-179">**MixedRealityCamera.prefab**: Camera only</span></span>
    * <span data-ttu-id="bf003-180">**MixedRealityCameraParent.prefab**: Appareil photo + téléportation + limite</span><span class="sxs-lookup"><span data-stu-id="bf003-180">**MixedRealityCameraParent.prefab**: Camera + Teleportation + Boundary</span></span>
    * <span data-ttu-id="bf003-181">Dans ce didacticiel, nous allons utiliser **MixedRealityCamera** sans téléportation fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bf003-181">In this tutorial, we will use **MixedRealityCamera** without teleportation feature.</span></span> <span data-ttu-id="bf003-182">Pour cette raison, nous avons ajouté simple **environnement** préfabriqué qui contient un étage de base pour rendre l’utilisateur se sentent la terre.</span><span class="sxs-lookup"><span data-stu-id="bf003-182">Because of this, we added simple **Environment** prefab which contains a basic floor to make the user feel grounded.</span></span>
    * <span data-ttu-id="bf003-183">Pour en savoir plus sur la téléportation avec **MixedRealityCameraParent**, consultez [conception - téléportation et locomotion avancée](#advanced-design---teleportation-and-locomotion)</span><span class="sxs-lookup"><span data-stu-id="bf003-183">To learn more about the teleportation with **MixedRealityCameraParent**, see [Advanced design - Teleportation and locomotion](#advanced-design---teleportation-and-locomotion)</span></span>

<span data-ttu-id="bf003-184">**Programme d’installation skybox**</span><span class="sxs-lookup"><span data-stu-id="bf003-184">**Skybox setup**</span></span>
* <span data-ttu-id="bf003-185">Cliquez sur **fenêtre > éclairage > Paramètres**</span><span class="sxs-lookup"><span data-stu-id="bf003-185">Click **Window > Lighting > Settings**</span></span>
* <span data-ttu-id="bf003-186">Cliquez sur le cercle sur le côté droit de la **champ de Skybox matériau**</span><span class="sxs-lookup"><span data-stu-id="bf003-186">Click the circle on the right side of the **Skybox Material field**</span></span>
* <span data-ttu-id="bf003-187">Tapez « gris » et sélectionnez **SkyboxGray**</span><span class="sxs-lookup"><span data-stu-id="bf003-187">Type in ‘gray’ and select **SkyboxGray**</span></span>

<span data-ttu-id="bf003-188">(Assets/AppPrefabs/Support/Materials/SkyboxGray.mat)</span><span class="sxs-lookup"><span data-stu-id="bf003-188">(Assets/AppPrefabs/Support/Materials/SkyboxGray.mat)</span></span>

![Paramètre skybox](images/mr123-skyboxsetting-400px.jpg)
* <span data-ttu-id="bf003-190">Vérifiez **Skybox** option pour être en mesure de voir affecté skybox dégradé gris</span><span class="sxs-lookup"><span data-stu-id="bf003-190">Check **Skybox** option to be able to see assigned gray gradient skybox</span></span>

![Activer/désactiver skybox option](images/mr213-skyboxcheck-400px.jpg)
* <span data-ttu-id="bf003-192">La scène avec MixedRealityCamera, environnement et gris skybox se présentera comme suit.</span><span class="sxs-lookup"><span data-stu-id="bf003-192">The scene with MixedRealityCamera, Environment and gray skybox will look like this.</span></span>

![Environnement de MixedReality213](images/mr213-environment-600px.jpg)
* <span data-ttu-id="bf003-194">Cliquez sur **fichier > Enregistrer la scène en tant que**</span><span class="sxs-lookup"><span data-stu-id="bf003-194">Click **File > Save Scene as**</span></span>
* <span data-ttu-id="bf003-195">**Enregistrer** votre scène sous le dossier de scènes avec n’importe quel nom</span><span class="sxs-lookup"><span data-stu-id="bf003-195">**Save** your scene under Scenes folder with any name</span></span>

## <a name="chapter-1---controller-visualization"></a><span data-ttu-id="bf003-196">Chapitre 1 - visualisation du contrôleur</span><span class="sxs-lookup"><span data-stu-id="bf003-196">Chapter 1 - Controller visualization</span></span>

>[!VIDEO https://www.youtube.com/embed/Kw0bf5NqyRg]

### <a name="objectives"></a><span data-ttu-id="bf003-197">Objectifs</span><span class="sxs-lookup"><span data-stu-id="bf003-197">Objectives</span></span>

* <span data-ttu-id="bf003-198">Découvrez comment restituer des modèles de contrôleur en mode de jeu d’Unity et de l’exécution de mouvement.</span><span class="sxs-lookup"><span data-stu-id="bf003-198">Learn how to render motion controller models in Unity's game mode and at runtime.</span></span>

<span data-ttu-id="bf003-199">Réalité mixte Windows fournit un modèle de contrôleur animée pour la visualisation de contrôleur.</span><span class="sxs-lookup"><span data-stu-id="bf003-199">Windows Mixed Reality provides an animated controller model for controller visualization.</span></span> <span data-ttu-id="bf003-200">Il existe plusieurs approches que possibles pour la visualisation de contrôleur dans votre application :</span><span class="sxs-lookup"><span data-stu-id="bf003-200">There are several approaches you can take for controller visualization in your app:</span></span>
* <span data-ttu-id="bf003-201">Par défaut, à l’aide de contrôleur par défaut sans aucune modification</span><span class="sxs-lookup"><span data-stu-id="bf003-201">Default - Using default controller without modification</span></span>
* <span data-ttu-id="bf003-202">Hybride - à l’aide de contrôleur par défaut, mais certains de ses éléments personnalisation ou recouvrir des composants d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="bf003-202">Hybrid - Using default controller, but customizing some of its elements or overlaying UI components</span></span>
* <span data-ttu-id="bf003-203">Remplacement - à l’aide de votre propre personnalisé à un modèle 3D pour le contrôleur</span><span class="sxs-lookup"><span data-stu-id="bf003-203">Replacement - Using your own customized 3D model for the controller</span></span>

<span data-ttu-id="bf003-204">Dans ce chapitre, vous allez apprendre sur les exemples de ces personnalisations de contrôleur.</span><span class="sxs-lookup"><span data-stu-id="bf003-204">In this chapter, we will learn about the examples of these controller customizations.</span></span>

### <a name="instructions"></a><span data-ttu-id="bf003-205">Instructions</span><span class="sxs-lookup"><span data-stu-id="bf003-205">Instructions</span></span>

* <span data-ttu-id="bf003-206">Dans le **projet** panneau, tapez **MotionControllers** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="bf003-206">In the **Project** panel, type **MotionControllers** in the search box .</span></span> <span data-ttu-id="bf003-207">Vous pouvez également le trouver sous ressources/HoloToolkit/Input/Prefabs /.</span><span class="sxs-lookup"><span data-stu-id="bf003-207">You can also find it under Assets/HoloToolkit/Input/Prefabs/.</span></span>
* <span data-ttu-id="bf003-208">Faites glisser le **MotionControllers** prefab dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-208">Drag the **MotionControllers** prefab into the **Hierarchy** panel.</span></span>
* <span data-ttu-id="bf003-209">Cliquez sur le **MotionControllers** prefab dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-209">Click on the **MotionControllers** prefab in the **Hierarchy** panel.</span></span>

<span data-ttu-id="bf003-210">**MotionControllers préfabriqué**</span><span class="sxs-lookup"><span data-stu-id="bf003-210">**MotionControllers prefab**</span></span>

<span data-ttu-id="bf003-211">**MotionControllers** préfabriqué a un **MotionControllerVisualizer** script qui fournit les emplacements pour les modèles de l’autre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="bf003-211">**MotionControllers** prefab has a **MotionControllerVisualizer** script which provides the slots for alternate controller models.</span></span> <span data-ttu-id="bf003-212">Si vous attribuez vos propres modèles 3D personnalisées telles que main ou un mot de passe et que vous vérifiez « Toujours modèle l’utilisation autre gauche/droite », vous les voyez au lieu du modèle par défaut.</span><span class="sxs-lookup"><span data-stu-id="bf003-212">If you assign your own custom 3D models such as a hand or a sword and check 'Always Use Alternate Left/Right Model', you will see them instead of the default model.</span></span> <span data-ttu-id="bf003-213">Nous allons utiliser cet emplacement dans le chapitre 4 pour remplacer le modèle de contrôleur avec un pinceau.</span><span class="sxs-lookup"><span data-stu-id="bf003-213">We will use this slot in Chapter 4 to replace the controller model with a brush.</span></span>

![MR213_ControllerVisualizer](images/mr213-controllervisualizer-600px.png)

<span data-ttu-id="bf003-215">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="bf003-215">**Instructions**</span></span>
* <span data-ttu-id="bf003-216">Dans le **inspecteur** , double-cliquez sur le panneau **MotionControllerVisualizer** script pour afficher le code dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bf003-216">In the **Inspector** panel, double click **MotionControllerVisualizer** script to see the code in the Visual Studio</span></span>

<span data-ttu-id="bf003-217">**Script de MotionControllerVisualizer**</span><span class="sxs-lookup"><span data-stu-id="bf003-217">**MotionControllerVisualizer script**</span></span>

<span data-ttu-id="bf003-218">Le **MotionControllerVisualizer** et **MotionControllerInfo** classes fournissent les moyens d’accéder aux & modifier les modèles de contrôleur par défaut.</span><span class="sxs-lookup"><span data-stu-id="bf003-218">The **MotionControllerVisualizer** and **MotionControllerInfo** classes provide the means to access & modify the default controller models.</span></span> <span data-ttu-id="bf003-219">**MotionControllerVisualizer** s’abonne à Unity **InteractionSourceDetected** événement et instancie automatiquement des modèles de contrôleur quand ils sont trouvent.</span><span class="sxs-lookup"><span data-stu-id="bf003-219">**MotionControllerVisualizer** subscribes to Unity's **InteractionSourceDetected** event and automatically instantiates controller models when they are found.</span></span>

```cs
protected override void Awake()
{
    ...
    InteractionManager.InteractionSourceDetected += InteractionManager_InteractionSourceDetected;
    InteractionManager.InteractionSourceLost += InteractionManager_InteractionSourceLost;
    ...
}
```

<span data-ttu-id="bf003-220">Les modèles de contrôleur sont remis en fonction de [la spécification glTF](https://github.com/KhronosGroup/glTF).</span><span class="sxs-lookup"><span data-stu-id="bf003-220">The controller models are delivered according to [the glTF specification](https://github.com/KhronosGroup/glTF).</span></span> <span data-ttu-id="bf003-221">Ce format a été créé pour fournir un format commun, tout en améliorant le processus derrière la transmission et la décompression des composants 3D.</span><span class="sxs-lookup"><span data-stu-id="bf003-221">This format has been created to provide a common format, while improving the process behind transmitting and unpacking 3D assets.</span></span> <span data-ttu-id="bf003-222">Dans ce cas, nous devons récupérer et charger les modèles de contrôleur lors de l’exécution, comme nous voulons que l’utilisateur expérience aussi transparente que possible, et il n’a pas garanti quelle version des contrôleurs de mouvement de l’utilisateur peut utiliser.</span><span class="sxs-lookup"><span data-stu-id="bf003-222">In this case, we need to retrieve and load the controller models at runtime, as we want to make the user's experience as seamless as possible, and it's not guaranteed which version of the motion controllers the user might be using.</span></span> <span data-ttu-id="bf003-223">Ce cours, par le biais de la boîte à outils de réalité mixte, utilise une version du groupe Khronos [UnityGLTF projet](https://github.com/KhronosGroup/UnityGLTF).</span><span class="sxs-lookup"><span data-stu-id="bf003-223">This course, via the Mixed Reality Toolkit, uses a version of the Khronos Group's [UnityGLTF project](https://github.com/KhronosGroup/UnityGLTF).</span></span>

<span data-ttu-id="bf003-224">Une fois que le contrôleur a été remis, les scripts peuvent utiliser **MotionControllerInfo** pour rechercher les transformations pour les éléments d’un contrôleur spécifique afin qu’ils peuvent se positionner correctement.</span><span class="sxs-lookup"><span data-stu-id="bf003-224">Once the controller has been delivered, scripts can use **MotionControllerInfo** to find the transforms for specific controller elements so they can correctly position themselves.</span></span>

<span data-ttu-id="bf003-225">Dans un chapitre ultérieur, nous allez apprendre à utiliser ces scripts pour joindre des éléments d’interface utilisateur pour les contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="bf003-225">In a later chapter, we will learn how to use these scripts to attach UI elements to the controllers.</span></span>

<span data-ttu-id="bf003-226">*Dans certains scripts, vous trouverez des blocs de code avec **#if ! UNITY_EDITOR** ou **UNITY_WSA**. Ces blocs de code exécutent uniquement sur le runtime UWP lorsque vous déployez pour Windows. Il s’agit, car le jeu d’API utilisées par l’éditeur Unity et le runtime d’application UWP sont différents.*</span><span class="sxs-lookup"><span data-stu-id="bf003-226">*In some scripts, you will find code blocks with **#if !UNITY_EDITOR** or **UNITY_WSA**. These code blocks run only on the UWP runtime when you deploy to Windows. This is because the set of APIs used by the Unity editor and the UWP app runtime are different.*</span></span>
* <span data-ttu-id="bf003-227">**Enregistrer** la scène et cliquez sur le **lire** bouton.</span><span class="sxs-lookup"><span data-stu-id="bf003-227">**Save** the scene and click the **play** button.</span></span>

<span data-ttu-id="bf003-228">Vous serez en mesure de voir la scène avec des contrôleurs de mouvement dans votre casque.</span><span class="sxs-lookup"><span data-stu-id="bf003-228">You will be able to see the scene with motion controllers in your headset.</span></span> <span data-ttu-id="bf003-229">Vous pouvez voir les animations détaillées pour les clics de bouton, de déplacement de stick analogique et mise en surbrillance du tactile pavé tactile.</span><span class="sxs-lookup"><span data-stu-id="bf003-229">You can see detailed animations for button clicks, thumbstick movement, and touchpad touch highlighting.</span></span>

![Par défaut de visualisation MR213_Controller](images/mr213-controllervisualizationdefault-500px.jpg)

## <a name="chapter-2---attaching-ui-elements-to-the-controller"></a><span data-ttu-id="bf003-231">Chapitre 2 : attacher des éléments d’interface utilisateur pour le contrôleur</span><span class="sxs-lookup"><span data-stu-id="bf003-231">Chapter 2 - Attaching UI elements to the controller</span></span>

>[!VIDEO https://www.youtube.com/embed/e-mLlwmTzJo]

### <a name="objectives"></a><span data-ttu-id="bf003-232">Objectifs</span><span class="sxs-lookup"><span data-stu-id="bf003-232">Objectives</span></span>

* <span data-ttu-id="bf003-233">En savoir plus sur les éléments des contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="bf003-233">Learn about the elements of the motion controllers</span></span>
* <span data-ttu-id="bf003-234">Découvrez comment attacher des objets à des parties spécifiques des contrôleurs</span><span class="sxs-lookup"><span data-stu-id="bf003-234">Learn how to attach objects to specific parts of the controllers</span></span>

<span data-ttu-id="bf003-235">Dans ce chapitre, vous allez apprendre à ajouter des éléments d’interface utilisateur pour le contrôleur sur lequel l’utilisateur peut facilement accéder et manipuler à tout moment au.</span><span class="sxs-lookup"><span data-stu-id="bf003-235">In this chapter, you will learn how to add user interface elements to the controller which the user can easily access and manipulate at anytime.</span></span> <span data-ttu-id="bf003-236">Vous allez également apprendre à ajouter un sélecteur de couleurs simple interface utilisateur en utilisant le pavé tactile d’entrée.</span><span class="sxs-lookup"><span data-stu-id="bf003-236">You will also learn how to add a simple color picker UI using the touchpad input.</span></span>

### <a name="instructions"></a><span data-ttu-id="bf003-237">Instructions</span><span class="sxs-lookup"><span data-stu-id="bf003-237">Instructions</span></span>

* <span data-ttu-id="bf003-238">Dans le **projet** du panneau, recherchez **MotionControllerInfo** script.</span><span class="sxs-lookup"><span data-stu-id="bf003-238">In the **Project** panel, search **MotionControllerInfo** script.</span></span>
* <span data-ttu-id="bf003-239">À partir du résultat de recherche, double-cliquez sur **MotionControllerInfo** script pour afficher le code dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf003-239">From the search result, double click **MotionControllerInfo** script to see the code in Visual Studio.</span></span>

<span data-ttu-id="bf003-240">**Script de MotionControllerInfo**</span><span class="sxs-lookup"><span data-stu-id="bf003-240">**MotionControllerInfo script**</span></span>

<span data-ttu-id="bf003-241">La première étape consiste à décider quel élément du contrôleur de l’interface utilisateur à joindre à.</span><span class="sxs-lookup"><span data-stu-id="bf003-241">The first step is to choose which element of the controller you want the UI to attach to.</span></span> <span data-ttu-id="bf003-242">Ces éléments sont définis dans **ControllerElementEnum** dans **MotionControllerInfo.cs**.</span><span class="sxs-lookup"><span data-stu-id="bf003-242">These elements are defined in **ControllerElementEnum** in **MotionControllerInfo.cs**.</span></span>

![MR213 MotionControllerElements](images/mr213-motioncontrollerelements-1000px.jpg)
* <span data-ttu-id="bf003-244">**Accueil**</span><span class="sxs-lookup"><span data-stu-id="bf003-244">**Home**</span></span>
* <span data-ttu-id="bf003-245">**Menu**</span><span class="sxs-lookup"><span data-stu-id="bf003-245">**Menu**</span></span>
* <span data-ttu-id="bf003-246">**Comprendre**</span><span class="sxs-lookup"><span data-stu-id="bf003-246">**Grasp**</span></span>
* <span data-ttu-id="bf003-247">**Stick analogique**</span><span class="sxs-lookup"><span data-stu-id="bf003-247">**Thumbstick**</span></span>
* <span data-ttu-id="bf003-248">**Select**</span><span class="sxs-lookup"><span data-stu-id="bf003-248">**Select**</span></span>
* <span data-ttu-id="bf003-249">**Pavé tactile**</span><span class="sxs-lookup"><span data-stu-id="bf003-249">**Touchpad**</span></span>
* <span data-ttu-id="bf003-250">**Pointage pose** : cet élément représente l’info-bulle du contrôleur qui pointe vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="bf003-250">**Pointing pose** – this element represents the tip of the controller pointing forward direction.</span></span>

<span data-ttu-id="bf003-251">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="bf003-251">**Instructions**</span></span>
* <span data-ttu-id="bf003-252">Dans le **projet** du panneau, recherchez **AttachToController** script.</span><span class="sxs-lookup"><span data-stu-id="bf003-252">In the **Project** panel, search **AttachToController** script.</span></span>
* <span data-ttu-id="bf003-253">À partir du résultat de recherche, double-cliquez sur **AttachToController** script pour afficher le code dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf003-253">From the search result, double click **AttachToController** script to see the code in Visual Studio.</span></span>

<span data-ttu-id="bf003-254">**Script de AttachToController**</span><span class="sxs-lookup"><span data-stu-id="bf003-254">**AttachToController script**</span></span>

<span data-ttu-id="bf003-255">Le **AttachToController** script fournit un moyen simple d’attacher des objets à un caractère gaucher ou droitier de contrôleur spécifié et l’élément.</span><span class="sxs-lookup"><span data-stu-id="bf003-255">The **AttachToController** script provides a simple way to attach any objects to a specified controller handedness and element.</span></span>

<span data-ttu-id="bf003-256">Dans **AttachElementToController()**,</span><span class="sxs-lookup"><span data-stu-id="bf003-256">In **AttachElementToController()**,</span></span>
* <span data-ttu-id="bf003-257">Vérifier à l’aide du caractère gaucher ou droitier **MotionControllerInfo.Handedness**</span><span class="sxs-lookup"><span data-stu-id="bf003-257">Check handedness using **MotionControllerInfo.Handedness**</span></span>
* <span data-ttu-id="bf003-258">Obtenir un élément spécifique du contrôleur en utilisant **MotionControllerInfo.TryGetElement()**</span><span class="sxs-lookup"><span data-stu-id="bf003-258">Get specific element of the controller using **MotionControllerInfo.TryGetElement()**</span></span>
* <span data-ttu-id="bf003-259">Après avoir récupéré l’élément transformer du modèle de contrôleur, le parent de l’objet dans cette section et définir la position locale et la rotation de l’objet à zéro.</span><span class="sxs-lookup"><span data-stu-id="bf003-259">After retrieving the element's transform from the controller model, parent the object under it and set object's local position & rotation to zero.</span></span>

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

<span data-ttu-id="bf003-260">La façon la plus simple d’utiliser **AttachToController** script consiste à hériter de celui-ci, comme nous l’avons fait dans le cas de **ColorPickerWheel.**</span><span class="sxs-lookup"><span data-stu-id="bf003-260">The simplest way to use **AttachToController** script is to inherit from it, as we've done in the case of **ColorPickerWheel.**</span></span> <span data-ttu-id="bf003-261">Il vous suffit de remplacer le **OnAttachToController** et **OnDetatchFromController** fonctions pour effectuer votre installation / répartition lorsque le contrôleur est détecté ou déconnecté.</span><span class="sxs-lookup"><span data-stu-id="bf003-261">Simply override the **OnAttachToController** and **OnDetatchFromController** functions to perform your setup / breakdown when the controller is detected / disconnected.</span></span>

<span data-ttu-id="bf003-262">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="bf003-262">**Instructions**</span></span>
* <span data-ttu-id="bf003-263">Dans le **projet** panneau, tapez dans la zone de recherche **ColorPickerWheel**.</span><span class="sxs-lookup"><span data-stu-id="bf003-263">In the **Project** panel, type in the search box **ColorPickerWheel**.</span></span> <span data-ttu-id="bf003-264">Vous pouvez également le trouver sous ressources/AppPrefabs /.</span><span class="sxs-lookup"><span data-stu-id="bf003-264">You can also find it under Assets/AppPrefabs/.</span></span>
* <span data-ttu-id="bf003-265">Faites glisser **ColorPickerWheel** prefab dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-265">Drag **ColorPickerWheel** prefab into the **Hierarchy** panel.</span></span>
* <span data-ttu-id="bf003-266">Cliquez sur le **ColorPickerWheel** prefab dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-266">Click the **ColorPickerWheel** prefab in the **Hierarchy** panel.</span></span>
* <span data-ttu-id="bf003-267">Dans le **inspecteur** , double-cliquez sur le panneau **ColorPickerWheel** Script pour afficher le code dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf003-267">In the **Inspector** panel, double click **ColorPickerWheel** Script to see the code in Visual Studio.</span></span>

![ColorPickerWheel préfabriqué](images/mr213-colorpickerwheel-1000px.jpg)

<span data-ttu-id="bf003-269">**Script de ColorPickerWheel**</span><span class="sxs-lookup"><span data-stu-id="bf003-269">**ColorPickerWheel script**</span></span>

<span data-ttu-id="bf003-270">Dans la mesure où **ColorPickerWheel** hérite **AttachToController**, il montre **gaucher/droitier** et **élément** dans le  **Inspecteur** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-270">Since **ColorPickerWheel** inherits **AttachToController**, it shows **Handedness** and **Element** in the **Inspector** panel.</span></span> <span data-ttu-id="bf003-271">Nous allons attacher l’interface utilisateur à l’élément du pavé tactile sur le contrôleur de gauche.</span><span class="sxs-lookup"><span data-stu-id="bf003-271">We'll be attaching the UI to the Touchpad element on the left controller.</span></span>

![Script de ColorPickerWheel](images/mr213-attachtocontroller-300px.jpg)

<span data-ttu-id="bf003-273">**ColorPickerWheel** remplace le **OnAttachToController** et **OnDetatchFromController** pour vous abonner à l’événement d’entrée qui sera utilisé dans le chapitre suivant pour la sélection de couleur avec pavé tactile d’entrée.</span><span class="sxs-lookup"><span data-stu-id="bf003-273">**ColorPickerWheel** overrides the **OnAttachToController** and **OnDetatchFromController** to subscribe to the input event which will be used in next chapter for color selection with touchpad input.</span></span>

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
* <span data-ttu-id="bf003-274">**Enregistrer** la scène et cliquez sur le **lire** bouton.</span><span class="sxs-lookup"><span data-stu-id="bf003-274">**Save** the scene and click the **play** button.</span></span>

<span data-ttu-id="bf003-275">**Autre méthode d’attachement d’objets pour les contrôleurs**</span><span class="sxs-lookup"><span data-stu-id="bf003-275">**Alternative method for attaching objects to the controllers**</span></span>

<span data-ttu-id="bf003-276">Nous recommandons que vos scripts héritent **AttachToController** et remplacer **OnAttachToController**.</span><span class="sxs-lookup"><span data-stu-id="bf003-276">We recommend that your scripts inherit from **AttachToController** and override **OnAttachToController**.</span></span> <span data-ttu-id="bf003-277">Toutefois, cela n'est pas toujours possible.</span><span class="sxs-lookup"><span data-stu-id="bf003-277">However, this may not always be possible.</span></span> <span data-ttu-id="bf003-278">Une alternative l’utilise en tant que composant autonome.</span><span class="sxs-lookup"><span data-stu-id="bf003-278">An alternative is using it as a standalone component.</span></span> <span data-ttu-id="bf003-279">Cela peut être utile lorsque vous souhaitez associer un préfabriqué existant à un contrôleur sans refactorisation vos scripts.</span><span class="sxs-lookup"><span data-stu-id="bf003-279">This can be useful when you want to attach an existing prefab to a controller without refactoring your scripts.</span></span> <span data-ttu-id="bf003-280">Simplement que votre classe attendre IsAttached être définie sur true avant d’effectuer tout le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="bf003-280">Simply have your class wait for IsAttached to be set to true before performing any setup.</span></span> <span data-ttu-id="bf003-281">Le plus simple pour ce faire consiste à l’aide d’une coroutine pour 'Start'.</span><span class="sxs-lookup"><span data-stu-id="bf003-281">The simplest way to do this is by using a coroutine for 'Start.'</span></span>

```cs
private IEnumerator Start() {
    AttachToController attach = gameObject.GetComponent<AttachToController>();

    while (!attach.IsAttached) {
        yield return null;
    }

    // Perform setup here
}
```

## <a name="chapter-3---working-with-touchpad-input"></a><span data-ttu-id="bf003-282">Chapitre 3 - utilisation de l’entrée du pavé tactile</span><span class="sxs-lookup"><span data-stu-id="bf003-282">Chapter 3 - Working with touchpad input</span></span>

>[!VIDEO https://www.youtube.com/embed/SUyw0kxZPFw]

### <a name="objectives"></a><span data-ttu-id="bf003-283">Objectifs</span><span class="sxs-lookup"><span data-stu-id="bf003-283">Objectives</span></span>

* <span data-ttu-id="bf003-284">Découvrez comment obtenir les événements de données d’entrée du pavé tactile</span><span class="sxs-lookup"><span data-stu-id="bf003-284">Learn how to get touchpad input data events</span></span>
* <span data-ttu-id="bf003-285">Découvrez comment utiliser les informations de position de l’axe du pavé tactile pour votre expérience d’application</span><span class="sxs-lookup"><span data-stu-id="bf003-285">Learn how to use touchpad axis position information for your app experience</span></span>

### <a name="instructions"></a><span data-ttu-id="bf003-286">Instructions</span><span class="sxs-lookup"><span data-stu-id="bf003-286">Instructions</span></span>

* <span data-ttu-id="bf003-287">Dans le **hiérarchie** du panneau, cliquez sur **ColorPickerWheel**</span><span class="sxs-lookup"><span data-stu-id="bf003-287">In the **Hierarchy** panel, click **ColorPickerWheel**</span></span>
* <span data-ttu-id="bf003-288">Dans le **inspecteur** panneau, sous **Animatior**, double-cliquez sur **ColorPickerWheelController**</span><span class="sxs-lookup"><span data-stu-id="bf003-288">In the **Inspector** panel, under **Animatior**, double click **ColorPickerWheelController**</span></span>
* <span data-ttu-id="bf003-289">Vous serez en mesure de voir **animation** onglet ouvert</span><span class="sxs-lookup"><span data-stu-id="bf003-289">You will be able to see **Animator** tab opened</span></span>

<span data-ttu-id="bf003-290">**Interface utilisateur de l’affichage/masquage avec le contrôleur de l’Animation d’Unity**</span><span class="sxs-lookup"><span data-stu-id="bf003-290">**Showing/hiding UI with Unity's Animation controller**</span></span>

<span data-ttu-id="bf003-291">Pour afficher et masquer le **ColorPickerWheel** l’interface utilisateur avec l’animation, nous utilisons [système d’animation d’Unity](https://docs.unity3d.com/Manual/AnimationOverview.html).</span><span class="sxs-lookup"><span data-stu-id="bf003-291">To show and hide the **ColorPickerWheel** UI with animation, we are using [Unity's animation system](https://docs.unity3d.com/Manual/AnimationOverview.html).</span></span> <span data-ttu-id="bf003-292">Définition de la **ColorPickerWheel**de **Visible** propriété aux déclencheurs true ou false **afficher** et **masquer** les déclencheurs d’animations.</span><span class="sxs-lookup"><span data-stu-id="bf003-292">Setting the **ColorPickerWheel**'s **Visible** property to true or false triggers **Show** and **Hide** animation triggers.</span></span> <span data-ttu-id="bf003-293">**Afficher** et **masquer** paramètres sont définis dans le **ColorPickerWheelController** contrôleur de l’animation.</span><span class="sxs-lookup"><span data-stu-id="bf003-293">**Show** and **Hide** parameters are defined in the **ColorPickerWheelController** animation controller.</span></span>

![Contrôleur de l’Animation Unity](images/mr123-animationcontroller-550px.jpg)

<span data-ttu-id="bf003-295">**Instructions**</span><span class="sxs-lookup"><span data-stu-id="bf003-295">**Instructions**</span></span>
* <span data-ttu-id="bf003-296">Dans le **hiérarchie** panneau, sélectionnez **ColorPickerWheel** prefab</span><span class="sxs-lookup"><span data-stu-id="bf003-296">In the **Hierarchy** panel, select **ColorPickerWheel** prefab</span></span>
* <span data-ttu-id="bf003-297">Dans le **inspecteur** , double-cliquez sur le panneau **ColorPickerWheel** script pour afficher le code dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bf003-297">In the **Inspector** panel, double click **ColorPickerWheel** script to see the code in the Visual Studio</span></span>

<span data-ttu-id="bf003-298">**Script de ColorPickerWheel**</span><span class="sxs-lookup"><span data-stu-id="bf003-298">**ColorPickerWheel script**</span></span>

<span data-ttu-id="bf003-299">**ColorPickerWheel** s’abonne à Unity **InteractionSourceUpdated** événements pour écouter les événements du pavé tactile.</span><span class="sxs-lookup"><span data-stu-id="bf003-299">**ColorPickerWheel** subscribes to Unity's **InteractionSourceUpdated** event to listen for touchpad events.</span></span>

<span data-ttu-id="bf003-300">Dans **InteractionSourceUpdated()**, le script vérifie d’abord pour vous assurer qu’elles :</span><span class="sxs-lookup"><span data-stu-id="bf003-300">In **InteractionSourceUpdated()**, the script first checks to ensure that it:</span></span>
* <span data-ttu-id="bf003-301">est en fait un événement tactile (obj.state. **touchpadTouched**)</span><span class="sxs-lookup"><span data-stu-id="bf003-301">is actually a touchpad event (obj.state.**touchpadTouched**)</span></span>
* <span data-ttu-id="bf003-302">origine à partir du contrôleur de gauche (obj.state.source. **gaucher/droitier**)</span><span class="sxs-lookup"><span data-stu-id="bf003-302">originates from the left controller (obj.state.source.**handedness**)</span></span>

<span data-ttu-id="bf003-303">Si les deux sont true, le pavé tactile positionner (obj.state. **touchpadPosition**) est affectée à **selectorPosition**.</span><span class="sxs-lookup"><span data-stu-id="bf003-303">If both are true, the touchpad position (obj.state.**touchpadPosition**) is assigned to **selectorPosition**.</span></span>

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

<span data-ttu-id="bf003-304">Dans **Update()**, en fonction de **visible** propriété, il déclenche l’affichage et le masquage des déclencheurs d’animation dans le composant d’animation du sélecteur de couleurs</span><span class="sxs-lookup"><span data-stu-id="bf003-304">In **Update()**, based on **visible** property, it triggers Show and Hide animation triggers in the color picker's animator component</span></span>

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

<span data-ttu-id="bf003-305">Dans **Update()**, **selectorPosition** est utilisé pour effectuer un cast d’un rayon à collider de maillage de la roulette de la couleur, qui retourne une position UV.</span><span class="sxs-lookup"><span data-stu-id="bf003-305">In **Update()**, **selectorPosition** is used to cast a ray at the color wheel's mesh collider, which returns a UV position.</span></span> <span data-ttu-id="bf003-306">Cette position peut ensuite servir à trouver les coordonnées de pixel et de couleur de texture de la roue couleur.</span><span class="sxs-lookup"><span data-stu-id="bf003-306">This position can then be used to find the pixel coordinate and color value of the color wheel's texture.</span></span> <span data-ttu-id="bf003-307">Cette valeur est accessible aux autres scripts via la **SelectedColor** propriété.</span><span class="sxs-lookup"><span data-stu-id="bf003-307">This value is accessible to other scripts via the **SelectedColor** property.</span></span>

![Raycasting de roulette de sélecteur de couleurs](images/mr213-colorpickerwheel-raycast-700px.png)

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

## <a name="chapter-4---overriding-controller-model"></a><span data-ttu-id="bf003-309">Chapitre 4 - modèle de contrôleur de remplacement</span><span class="sxs-lookup"><span data-stu-id="bf003-309">Chapter 4 - Overriding controller model</span></span>

>[!VIDEO https://www.youtube.com/embed/8gBFqA_DZ_U]

### <a name="objectives"></a><span data-ttu-id="bf003-310">Objectifs</span><span class="sxs-lookup"><span data-stu-id="bf003-310">Objectives</span></span>

* <span data-ttu-id="bf003-311">Découvrez comment remplacer le modèle de contrôleur avec un modèle 3D personnalisé.</span><span class="sxs-lookup"><span data-stu-id="bf003-311">Learn how to override the controller model with a custom 3D model.</span></span>

![MR213_BrushToolOverride](images/mr213-brushtooloverride-500px.jpg)

### <a name="instructions"></a><span data-ttu-id="bf003-313">Instructions</span><span class="sxs-lookup"><span data-stu-id="bf003-313">Instructions</span></span>

* <span data-ttu-id="bf003-314">Cliquez sur **MotionControllers** dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-314">Click **MotionControllers** in the **Hierarchy** panel.</span></span>
* <span data-ttu-id="bf003-315">Cliquez sur le cercle sur le côté droit de la **autre contrôleur droite** champ.</span><span class="sxs-lookup"><span data-stu-id="bf003-315">Click the circle on the right side of the **Alternate Right Controller** field.</span></span>
* <span data-ttu-id="bf003-316">Tapez dans **' BrushController**» et sélectionnez le préfabriqué à partir du résultat.</span><span class="sxs-lookup"><span data-stu-id="bf003-316">Type in **'BrushController**' and select the prefab from the result.</span></span> <span data-ttu-id="bf003-317">Vous pouvez le trouver sous ressources/AppPrefabs/**BrushController**.</span><span class="sxs-lookup"><span data-stu-id="bf003-317">You can find it under Assets/AppPrefabs/**BrushController**.</span></span>
* <span data-ttu-id="bf003-318">Vérifiez **toujours utiliser le modèle approprié autre**</span><span class="sxs-lookup"><span data-stu-id="bf003-318">Check **Always Use Alternate Right Model**</span></span>

![MR213_BrushToolOverrideSlot](images/mr213-motioncontrollersoverride-700px.jpg)

<span data-ttu-id="bf003-320">Le **BrushController** préfabriqué ne devra pas être inclus dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-320">The **BrushController** prefab does not have to be included in the **Hierarchy** panel.</span></span> <span data-ttu-id="bf003-321">Toutefois, à consulter ses composants enfants :</span><span class="sxs-lookup"><span data-stu-id="bf003-321">However, to check out its child components:</span></span>
* <span data-ttu-id="bf003-322">Dans le **projet** panneau, tapez **BrushController** et faites glisser **BrushController** prefab dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-322">In the **Project** panel, type in **BrushController** and drag **BrushController** prefab into the **Hierarchy** panel.</span></span>

![MR213_BrushTool_Prefab2](images/mr213-brushtool-prefab-1000px.jpg)

<span data-ttu-id="bf003-324">Vous trouverez le **Conseil** composant dans **BrushController**.</span><span class="sxs-lookup"><span data-stu-id="bf003-324">You will find the **Tip** component in **BrushController**.</span></span> <span data-ttu-id="bf003-325">Nous allons utiliser sa transformation pour tracer des lignes de démarrage/arrêt.</span><span class="sxs-lookup"><span data-stu-id="bf003-325">We will use its transform to start/stop drawing lines.</span></span>
* <span data-ttu-id="bf003-326">Supprimer le **BrushController** à partir de la **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-326">Delete the **BrushController** from the **Hierarchy** panel.</span></span>
* <span data-ttu-id="bf003-327">**Enregistrer** la scène et cliquez sur le **lire** bouton.</span><span class="sxs-lookup"><span data-stu-id="bf003-327">**Save** the scene and click the **play** button.</span></span> <span data-ttu-id="bf003-328">Vous serez en mesure de voir que le modèle de pinceau remplacé le contrôleur de mouvement de droite.</span><span class="sxs-lookup"><span data-stu-id="bf003-328">You will be able to see the brush model replaced the right-hand motion controller.</span></span>

## <a name="chapter-5---painting-with-select-input"></a><span data-ttu-id="bf003-329">Chapitre 5 - entrée de peinture avec Select</span><span class="sxs-lookup"><span data-stu-id="bf003-329">Chapter 5 - Painting with Select input</span></span>

>[!VIDEO https://www.youtube.com/embed/QTrYaMHIs7w]

### <a name="objectives"></a><span data-ttu-id="bf003-330">Objectifs</span><span class="sxs-lookup"><span data-stu-id="bf003-330">Objectives</span></span>

* <span data-ttu-id="bf003-331">Découvrez comment utiliser l’événement de bouton Sélectionner pour démarrer et arrêter un dessin au trait</span><span class="sxs-lookup"><span data-stu-id="bf003-331">Learn how to use the Select button event to start and stop a line drawing</span></span>

### <a name="instructions"></a><span data-ttu-id="bf003-332">Instructions</span><span class="sxs-lookup"><span data-stu-id="bf003-332">Instructions</span></span>

* <span data-ttu-id="bf003-333">Recherche **BrushController** prefab dans le **projet** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-333">Search **BrushController** prefab in the **Project** panel.</span></span>
* <span data-ttu-id="bf003-334">Dans le **inspecteur** , double-cliquez sur le panneau **BrushController** Script pour afficher le code dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bf003-334">In the **Inspector** panel, double click **BrushController** Script to see the code in Visual Studio</span></span>

<span data-ttu-id="bf003-335">**Script de BrushController**</span><span class="sxs-lookup"><span data-stu-id="bf003-335">**BrushController script**</span></span>

<span data-ttu-id="bf003-336">**BrushController** s’abonne à la InteractionManager **InteractionSourcePressed** et **InteractionSourceReleased** événements.</span><span class="sxs-lookup"><span data-stu-id="bf003-336">**BrushController** subscribes to the InteractionManager's **InteractionSourcePressed** and **InteractionSourceReleased** events.</span></span> <span data-ttu-id="bf003-337">Lorsque **InteractionSourcePressed** événement est déclenché, le pinceau **dessiner** propriété est définie sur true ; lorsque **InteractionSourceReleased** événement est déclenché, le pinceau **Dessiner** propriété est définie sur false.</span><span class="sxs-lookup"><span data-stu-id="bf003-337">When **InteractionSourcePressed** event is triggered, the brush's **Draw** property is set to true; when **InteractionSourceReleased** event is triggered, the brush's **Draw** property is set to false.</span></span>

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

<span data-ttu-id="bf003-338">Bien que **dessiner** est définie sur true, le pinceau généreront les points dans un Unity instancié **LineRenderer**.</span><span class="sxs-lookup"><span data-stu-id="bf003-338">While **Draw** is set to true, the brush will generate points in an instantiated Unity **LineRenderer**.</span></span> <span data-ttu-id="bf003-339">Une référence à cette préfabriqué est conservée dans le pinceau **Prefab Stroke** champ.</span><span class="sxs-lookup"><span data-stu-id="bf003-339">A reference to this prefab is kept in the brush's **Stroke Prefab** field.</span></span>

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

<span data-ttu-id="bf003-340">Pour utiliser la couleur actuellement sélectionnée à partir de la roulette de sélecteur de couleurs interface utilisateur, **BrushController** doit avoir une référence à la **ColorPickerWheel** objet.</span><span class="sxs-lookup"><span data-stu-id="bf003-340">To use the currently selected color from the color picker wheel UI, **BrushController** needs to have a reference to the **ColorPickerWheel** object.</span></span> <span data-ttu-id="bf003-341">Étant donné que le **BrushController** préfabriqué est instancié lors de l’exécution en tant qu’un contrôleur de remplacement, toutes les références aux objets dans la scène aura à définir lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="bf003-341">Because the **BrushController** prefab is instantiated at runtime as a replacement controller, any references to objects in the scene will have to be set at runtime.</span></span> <span data-ttu-id="bf003-342">Dans ce cas, nous utilisons **GameObject.FindObjectOfType** pour localiser le **ColorPickerWheel**:</span><span class="sxs-lookup"><span data-stu-id="bf003-342">In this case we use **GameObject.FindObjectOfType** to locate the **ColorPickerWheel**:</span></span>

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
* <span data-ttu-id="bf003-343">**Enregistrer** la scène et cliquez sur le **lire** bouton.</span><span class="sxs-lookup"><span data-stu-id="bf003-343">**Save** the scene and click the **play** button.</span></span> <span data-ttu-id="bf003-344">Vous ne pourrez pas dessiner les lignes et peindre à l’aide du bouton de sélection sur le contrôleur de droite.</span><span class="sxs-lookup"><span data-stu-id="bf003-344">You will be able to draw the lines and paint using the select button on the right-hand controller.</span></span>

## <a name="chapter-6---object-spawning-with-select-input"></a><span data-ttu-id="bf003-345">Chapitre 6 - objet lors de la génération avec Select d’entrée</span><span class="sxs-lookup"><span data-stu-id="bf003-345">Chapter 6 - Object spawning with Select input</span></span>

>[!VIDEO https://www.youtube.com/embed/z4IxyzFHP0U]

### <a name="objectives"></a><span data-ttu-id="bf003-346">Objectifs</span><span class="sxs-lookup"><span data-stu-id="bf003-346">Objectives</span></span>

* <span data-ttu-id="bf003-347">Découvrez comment utiliser Select et comprendre les événements d’entrée de bouton</span><span class="sxs-lookup"><span data-stu-id="bf003-347">Learn how to use Select and Grasp button input events</span></span>
* <span data-ttu-id="bf003-348">Découvrez comment instancier des objets</span><span class="sxs-lookup"><span data-stu-id="bf003-348">Learn how to instantiate objects</span></span>

### <a name="instructions"></a><span data-ttu-id="bf003-349">Instructions</span><span class="sxs-lookup"><span data-stu-id="bf003-349">Instructions</span></span>

* <span data-ttu-id="bf003-350">Dans le **projet** panneau, tapez **ObjectSpawner** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="bf003-350">In the **Project** panel, type **ObjectSpawner** in the search box.</span></span> <span data-ttu-id="bf003-351">Vous pouvez également le trouver sous ressources/AppPrefabs /</span><span class="sxs-lookup"><span data-stu-id="bf003-351">You can also find it under Assets/AppPrefabs/</span></span>
* <span data-ttu-id="bf003-352">Faites glisser le **ObjectSpawner** prefab dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-352">Drag the **ObjectSpawner** prefab into the **Hierarchy** panel.</span></span>
* <span data-ttu-id="bf003-353">Cliquez sur **ObjectSpawner** dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-353">Click **ObjectSpawner** in the **Hierarchy** panel.</span></span>
* <span data-ttu-id="bf003-354">**ObjectSpawner** possède un champ nommé **couleur Source**.</span><span class="sxs-lookup"><span data-stu-id="bf003-354">**ObjectSpawner** has a field named **Color Source**.</span></span>
* <span data-ttu-id="bf003-355">À partir de la **hiérarchie** volet, faites glisser le **ColorPickerWheel** référence dans ce champ.</span><span class="sxs-lookup"><span data-stu-id="bf003-355">From the **Hierarchy** panel, drag the **ColorPickerWheel** reference into this field.</span></span>

![Objet Spawner inspecteur](images/mr213-objectspawnercolorpickerwheel-650px.jpg)
* <span data-ttu-id="bf003-357">Cliquez sur le **ObjectSpawner** prefab dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-357">Click the **ObjectSpawner** prefab in the **Hierarchy** panel.</span></span>
* <span data-ttu-id="bf003-358">Dans le **inspecteur** , double-cliquez sur le panneau **ObjectSpawner** Script pour afficher le code dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf003-358">In the **Inspector** panel, double click **ObjectSpawner** Script to see the code in Visual Studio.</span></span>

<span data-ttu-id="bf003-359">**Script de ObjectSpawner**</span><span class="sxs-lookup"><span data-stu-id="bf003-359">**ObjectSpawner script**</span></span>

<span data-ttu-id="bf003-360">Le **ObjectSpawner** instancie des copies d’une maille primitifs (cube, sphère, cylindre) dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="bf003-360">The **ObjectSpawner** instantiates copies of a primitive mesh (cube, sphere, cylinder) into the space.</span></span> <span data-ttu-id="bf003-361">Quand un **InteractionSourcePressed** est détecté qu’il vérifie le caractère gaucher ou droitier et s’il est un **InteractionSourcePressType.Grasp** ou **InteractionSourcePressType.Select** événement.</span><span class="sxs-lookup"><span data-stu-id="bf003-361">When a **InteractionSourcePressed** is detected it checks the handedness and if it's an **InteractionSourcePressType.Grasp** or **InteractionSourcePressType.Select** event.</span></span>

<span data-ttu-id="bf003-362">Pour un **saisir** événement, il incrémente l’index de type maille actuel (sphère, cube, cylindre)</span><span class="sxs-lookup"><span data-stu-id="bf003-362">For a **Grasp** event, it increments the index of current mesh type (sphere, cube, cylinder)</span></span>

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

<span data-ttu-id="bf003-363">Pour un **sélectionnez** événement, dans **SpawnObject()**, un nouvel objet est instancié, non apparentée et publiées dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="bf003-363">For a **Select** event, in **SpawnObject()**, a new object is instantiated, un-parented and released into the world.</span></span>

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

<span data-ttu-id="bf003-364">Le **ObjectSpawner** utilise le **ColorPickerWheel** pour définir la couleur des éléments de l’objet d’affichage.</span><span class="sxs-lookup"><span data-stu-id="bf003-364">The **ObjectSpawner** uses the **ColorPickerWheel** to set the color of the display object's material.</span></span> <span data-ttu-id="bf003-365">Objets engendrés bénéficient d’une instance de ce document afin qu’ils conserveront leur couleur.</span><span class="sxs-lookup"><span data-stu-id="bf003-365">Spawned objects are given an instance of this material so they will retain their color.</span></span>
* <span data-ttu-id="bf003-366">**Enregistrer** la scène et cliquez sur le **lire** bouton.</span><span class="sxs-lookup"><span data-stu-id="bf003-366">**Save** the scene and click the **play** button.</span></span>

<span data-ttu-id="bf003-367">Vous ne pourrez pas modifier les objets avec le bouton de comprendre et de générer dynamiquement des objets avec le bouton de sélection.</span><span class="sxs-lookup"><span data-stu-id="bf003-367">You will be able to change the objects with the Grasp button and spawn objects with the Select button.</span></span>

## <a name="build-and-deploy-app-to-mixed-reality-portal"></a><span data-ttu-id="bf003-368">Créer et déployer l’application au portail de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="bf003-368">Build and deploy app to Mixed Reality Portal</span></span>
* <span data-ttu-id="bf003-369">Dans Unity, sélectionnez **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="bf003-369">In Unity, select **File > Build Settings**.</span></span>
* <span data-ttu-id="bf003-370">Cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène actuelle pour le **scènes dans Build**.</span><span class="sxs-lookup"><span data-stu-id="bf003-370">Click **Add Open Scenes** to add current scene to the **Scenes In Build**.</span></span>
* <span data-ttu-id="bf003-371">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="bf003-371">Click **Build**.</span></span>
* <span data-ttu-id="bf003-372">Créer un **nouveau dossier** nommé « Application ».</span><span class="sxs-lookup"><span data-stu-id="bf003-372">Create a **New Folder** named "App".</span></span>
* <span data-ttu-id="bf003-373">Clic le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="bf003-373">Single click the **App** folder.</span></span>
* <span data-ttu-id="bf003-374">Cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="bf003-374">Click **Select Folder**.</span></span>
* <span data-ttu-id="bf003-375">Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bf003-375">When Unity is done, a File Explorer window will appear.</span></span>
* <span data-ttu-id="bf003-376">Ouvrez le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="bf003-376">Open the **App** folder.</span></span>
* <span data-ttu-id="bf003-377">Double-cliquez sur **YourSceneName.sln** fichier de Solution Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf003-377">Double click **YourSceneName.sln** Visual Studio Solution file.</span></span>
* <span data-ttu-id="bf003-378">À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **X64**.</span><span class="sxs-lookup"><span data-stu-id="bf003-378">Using the top toolbar in Visual Studio, change the target from Debug to **Release** and from ARM to **X64**.</span></span>
* <span data-ttu-id="bf003-379">Cliquez sur la flèche déroulante en regard du bouton de l’appareil, puis sélectionnez **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="bf003-379">Click on the drop-down arrow next to the Device button, and select **Local Machine**.</span></span>
* <span data-ttu-id="bf003-380">Cliquez sur **Déboguer -> Démarrer sans débogage** dans le menu ou appuyez sur **Ctrl + F5**.</span><span class="sxs-lookup"><span data-stu-id="bf003-380">Click **Debug -> Start Without debugging** in the menu or press **Ctrl + F5**.</span></span>

<span data-ttu-id="bf003-381">Maintenant, l’application est créée et installée dans le portail de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="bf003-381">Now the app is built and installed in Mixed Reality Portal.</span></span> <span data-ttu-id="bf003-382">Vous pouvez le lancer à nouveau via le menu Démarrer dans le portail de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="bf003-382">You can launch it again through Start menu in Mixed Reality Portal.</span></span>

## <a name="advanced-design---brush-tools-with-radial-layout"></a><span data-ttu-id="bf003-383">Conception avancée - outils de pinceau avec disposition radial</span><span class="sxs-lookup"><span data-stu-id="bf003-383">Advanced design - Brush tools with radial layout</span></span>

![MixedReality213 Main](images/mr213-main-600px.jpg)

<span data-ttu-id="bf003-385">Dans ce chapitre, vous allez apprendre à remplacer le modèle de contrôleur de mouvement par défaut par une collection d’outil Pinceau personnalisé.</span><span class="sxs-lookup"><span data-stu-id="bf003-385">In this chapter, you will learn how to replace the default motion controller model with a custom brush tool collection.</span></span> <span data-ttu-id="bf003-386">À titre de référence, vous pouvez trouver la scène terminée **MixedReality213Advanced** sous **scènes** dossier.</span><span class="sxs-lookup"><span data-stu-id="bf003-386">For your reference, you can find the completed scene **MixedReality213Advanced** under **Scenes** folder.</span></span>

### <a name="instructions"></a><span data-ttu-id="bf003-387">Instructions</span><span class="sxs-lookup"><span data-stu-id="bf003-387">Instructions</span></span>

* <span data-ttu-id="bf003-388">Dans le **projet** panneau, tapez **BrushSelector** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="bf003-388">In the **Project** panel, type **BrushSelector** in the search box .</span></span> <span data-ttu-id="bf003-389">Vous pouvez également le trouver sous ressources/AppPrefabs /</span><span class="sxs-lookup"><span data-stu-id="bf003-389">You can also find it under Assets/AppPrefabs/</span></span>
* <span data-ttu-id="bf003-390">Faites glisser le **BrushSelector** prefab dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-390">Drag the **BrushSelector** prefab into the **Hierarchy** panel.</span></span>
* <span data-ttu-id="bf003-391">Pour l’organisation, créer un GameObject vide appelé **pinceaux**</span><span class="sxs-lookup"><span data-stu-id="bf003-391">For organization, create an empty GameObject called **Brushes**</span></span>
* <span data-ttu-id="bf003-392">Faites glisser suivantes prefabs à partir de la **projet** panneau dans **pinceaux**</span><span class="sxs-lookup"><span data-stu-id="bf003-392">Drag following prefabs from the **Project** panel into **Brushes**</span></span>
    * <span data-ttu-id="bf003-393">Assets/AppPrefabs/**BrushFat**</span><span class="sxs-lookup"><span data-stu-id="bf003-393">Assets/AppPrefabs/**BrushFat**</span></span>
    * <span data-ttu-id="bf003-394">Assets/AppPrefabs/**BrushThin**</span><span class="sxs-lookup"><span data-stu-id="bf003-394">Assets/AppPrefabs/**BrushThin**</span></span>
    * <span data-ttu-id="bf003-395">Assets/AppPrefabs/**Eraser**</span><span class="sxs-lookup"><span data-stu-id="bf003-395">Assets/AppPrefabs/**Eraser**</span></span>
    * <span data-ttu-id="bf003-396">Assets/AppPrefabs/**MarkerFat**</span><span class="sxs-lookup"><span data-stu-id="bf003-396">Assets/AppPrefabs/**MarkerFat**</span></span>
    * <span data-ttu-id="bf003-397">Assets/AppPrefabs/**MarkerThin**</span><span class="sxs-lookup"><span data-stu-id="bf003-397">Assets/AppPrefabs/**MarkerThin**</span></span>
    * <span data-ttu-id="bf003-398">Assets/AppPrefabs/**Pencil**</span><span class="sxs-lookup"><span data-stu-id="bf003-398">Assets/AppPrefabs/**Pencil**</span></span>

![Pinceaux](images/mixedreality213-brushes-250px.png)
* <span data-ttu-id="bf003-400">Cliquez sur **MotionControllers** prefab dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-400">Click **MotionControllers** prefab in the **Hierarchy** panel.</span></span>
* <span data-ttu-id="bf003-401">Dans le **inspecteur** panneau, décochez la case **toujours modèle l’utilisation autre droit** sur la **visualiseur de contrôleur de mouvement**</span><span class="sxs-lookup"><span data-stu-id="bf003-401">In the **Inspector** panel, uncheck **Always Use Alternate Right Model** on the **Motion Controller Visualizer**</span></span>
* <span data-ttu-id="bf003-402">Dans le **hiérarchie** du panneau, cliquez sur **BrushSelector**</span><span class="sxs-lookup"><span data-stu-id="bf003-402">In the **Hierarchy** panel, click **BrushSelector**</span></span>
* <span data-ttu-id="bf003-403">**BrushSelector** possède un champ nommé **ColorPicker**</span><span class="sxs-lookup"><span data-stu-id="bf003-403">**BrushSelector** has a field named **ColorPicker**</span></span>
* <span data-ttu-id="bf003-404">À partir de la **hiérarchie** volet, faites glisser le **ColorPickerWheel** dans **ColorPicker** champ dans le **inspecteur** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-404">From the **Hierarchy** panel, drag the **ColorPickerWheel** into **ColorPicker** field in the **Inspector** panel.</span></span>

![Affecter ColorPickerWheel de sélecteur de pinceau](images/mr213-brushselector-500px.jpg)
* <span data-ttu-id="bf003-406">Dans le **hiérarchie** panneau, sous **BrushSelector** prefab, sélectionnez le **Menu** objet.</span><span class="sxs-lookup"><span data-stu-id="bf003-406">In the **Hierarchy** panel, under **BrushSelector** prefab, select the **Menu** object.</span></span>
* <span data-ttu-id="bf003-407">Dans le **inspecteur** panneau, sous la **LineObjectCollection** composant, ouvrez le **objets** tableau dropdown.</span><span class="sxs-lookup"><span data-stu-id="bf003-407">In the **Inspector** panel, under the **LineObjectCollection** component, open the **Objects** array dropdown.</span></span> <span data-ttu-id="bf003-408">Vous verrez les emplacements vides 6.</span><span class="sxs-lookup"><span data-stu-id="bf003-408">You will see 6 empty slots.</span></span>
* <span data-ttu-id="bf003-409">À partir de la **hiérarchie** volet, faites glisser chacune des prefabs apparentés sous le **pinceaux** GameObject dans ces emplacements dans n’importe quel ordre.</span><span class="sxs-lookup"><span data-stu-id="bf003-409">From the **Hierarchy** panel, drag each of the prefabs parented under the **Brushes** GameObject into these slots in any order.</span></span> <span data-ttu-id="bf003-410">(Assurez-vous que vous faites glisser les prefabs à partir de la scène, pas les préfabriqués dans le dossier du projet.)</span><span class="sxs-lookup"><span data-stu-id="bf003-410">(Make sure you're dragging the prefabs from the scene, not the prefabs in the project folder.)</span></span>

![Sélecteur de pinceau](images/mr213-brushselectorbrushes-700px.jpg)

<span data-ttu-id="bf003-412">**BrushSelector préfabriqué**</span><span class="sxs-lookup"><span data-stu-id="bf003-412">**BrushSelector prefab**</span></span>

<span data-ttu-id="bf003-413">Dans la mesure où le **BrushSelector** hérite **AttachToController**, il montre **gaucher/droitier** et **élément** options dans le  **Inspecteur** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="bf003-413">Since the **BrushSelector** inherits **AttachToController**, it shows **Handedness** and **Element** options in the **Inspector** panel.</span></span> <span data-ttu-id="bf003-414">Nous avons sélectionné **droite** et **pointant poser** pour attacher les outils de pinceau pour le contrôleur de droite avec la direction vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="bf003-414">We selected **Right** and **Pointing Pose** to attach brush tools to the right hand controller with forward direction.</span></span>

<span data-ttu-id="bf003-415">Le **BrushSelector** utilise deux utilitaires :</span><span class="sxs-lookup"><span data-stu-id="bf003-415">The **BrushSelector** makes use of two utilities:</span></span>
* <span data-ttu-id="bf003-416">**Ellipse**: permet de générer des points dans l’espace le long d’une forme d’ellipse.</span><span class="sxs-lookup"><span data-stu-id="bf003-416">**Ellipse**: used to generate points in space along an ellipse shape.</span></span>
* <span data-ttu-id="bf003-417">**LineObjectCollection**: distribue les objets à l’aide de points générés par n’importe quelle classe de ligne (par exemple, Ellipse).</span><span class="sxs-lookup"><span data-stu-id="bf003-417">**LineObjectCollection**: distributes objects using the points generated by any Line class (eg, Ellipse).</span></span> <span data-ttu-id="bf003-418">C’est ce que nous allons utiliser pour placer notre pinceaux le long de la forme d’Ellipse.</span><span class="sxs-lookup"><span data-stu-id="bf003-418">This is what we'll be using to place our brushes along the Ellipse shape.</span></span>

<span data-ttu-id="bf003-419">Lorsqu’elles sont combinées, ces utilitaires peuvent être utilisés pour créer un menu radial.</span><span class="sxs-lookup"><span data-stu-id="bf003-419">When combined, these utilities can be used to create a radial menu.</span></span>

<span data-ttu-id="bf003-420">**Script de LineObjectCollection**</span><span class="sxs-lookup"><span data-stu-id="bf003-420">**LineObjectCollection script**</span></span>

<span data-ttu-id="bf003-421">**LineObjectCollection** dispose de contrôles pour la taille, la position et la rotation d’objets distribués selon sa ligne.</span><span class="sxs-lookup"><span data-stu-id="bf003-421">**LineObjectCollection** has controls for the size, position and rotation of objects distributed along its line.</span></span> <span data-ttu-id="bf003-422">Cela est utile pour la création de menus radiales telles que le sélecteur de pinceau.</span><span class="sxs-lookup"><span data-stu-id="bf003-422">This is useful for creating radial menus like the brush selector.</span></span> <span data-ttu-id="bf003-423">Pour créer l’apparence de pinceaux cette mise à l’échelle à partir de rien que qu’ils approchent de la position du centre sélectionné, le **ObjectScale** courbe pics dans le centre et le se désactivé à la périphérie.</span><span class="sxs-lookup"><span data-stu-id="bf003-423">To create the appearance of brushes that scale up from nothing as they approach the center selected position, the **ObjectScale** curve peaks in the center and tapers off at the edges.</span></span>

<span data-ttu-id="bf003-424">**Script de BrushSelector**</span><span class="sxs-lookup"><span data-stu-id="bf003-424">**BrushSelector script**</span></span>

<span data-ttu-id="bf003-425">Dans le cas de la **BrushSelector**, nous avons choisi d’utiliser une animation procédurale.</span><span class="sxs-lookup"><span data-stu-id="bf003-425">In the case of the **BrushSelector**, we've chosen to use procedural animation.</span></span> <span data-ttu-id="bf003-426">Tout d’abord, les modèles de pinceau sont distribués dans une ellipse par le **LineObjectCollection** script.</span><span class="sxs-lookup"><span data-stu-id="bf003-426">First, brush models are distributed in an ellipse by the **LineObjectCollection** script.</span></span> <span data-ttu-id="bf003-427">Ensuite, chaque pinceau est responsable du maintien de sa position en main de l’utilisateur selon son **DisplayMode** valeur, en fonction de la sélection.</span><span class="sxs-lookup"><span data-stu-id="bf003-427">Then, each brush is responsible for maintaining its position in the user's hand based on its **DisplayMode** value, which changes based on the selection.</span></span> <span data-ttu-id="bf003-428">Nous avons choisi une approche procédurale en raison de la forte probabilité de transitions de position de pinceau interrompue lorsque l’utilisateur sélectionne des pinceaux.</span><span class="sxs-lookup"><span data-stu-id="bf003-428">We chose a procedural approach because of the high probability of brush position transitions being interrupted as the user selects brushes.</span></span> <span data-ttu-id="bf003-429">Les animations Mecanim peuvent gérer correctement les interruptions, mais il a tendance à être plus compliquée qu’une simple opération Lerp.</span><span class="sxs-lookup"><span data-stu-id="bf003-429">Mecanim animations can handle interruptions gracefully, but it tends to be more complicated than a simple Lerp operation.</span></span>

<span data-ttu-id="bf003-430">**BrushSelector** utilise une combinaison des deux.</span><span class="sxs-lookup"><span data-stu-id="bf003-430">**BrushSelector** uses a combination of both.</span></span> <span data-ttu-id="bf003-431">Lors de l’entrée du pavé tactile est détectée, les options de pinceau deviennent visibles et monter le long du menu radial.</span><span class="sxs-lookup"><span data-stu-id="bf003-431">When touchpad input is detected, brush options become visible and scale up along the radial menu.</span></span> <span data-ttu-id="bf003-432">Après une période de délai d’attente (ce qui indique que l’utilisateur a effectué une sélection) le pinceau des options de mise à l’échelle vers le bas, en laissant uniquement le pinceau sélectionné.</span><span class="sxs-lookup"><span data-stu-id="bf003-432">After a timeout period (which indicates that the user has made a selection) the brush options scale down again, leaving only the selected brush.</span></span>

<span data-ttu-id="bf003-433">**Visualisation d’entrée du pavé tactile**</span><span class="sxs-lookup"><span data-stu-id="bf003-433">**Visualizing touchpad input**</span></span>

<span data-ttu-id="bf003-434">Même dans les cas où le modèle de contrôleur a été entièrement remplacé, il peut être utile afficher d’entrée sur les entrées de modèle d’origine.</span><span class="sxs-lookup"><span data-stu-id="bf003-434">Even in cases where the controller model has been completely replaced, it can be helpful to show input on the original model inputs.</span></span> <span data-ttu-id="bf003-435">Cela permet à la pour terre des actions de l’utilisateur en réalité.</span><span class="sxs-lookup"><span data-stu-id="bf003-435">This helps to ground the user's actions in reality.</span></span> <span data-ttu-id="bf003-436">Pour le **BrushSelector** que nous avons choisi rendre le pavé tactile brièvement visibles lorsque l’entrée est reçue.</span><span class="sxs-lookup"><span data-stu-id="bf003-436">For the **BrushSelector** we've chosen to make the touchpad briefly visible when the input is received.</span></span> <span data-ttu-id="bf003-437">Cela a été effectuée en récupérant l’élément pavé tactile à partir du contrôleur, en remplaçant son matériel avec un matériel personnalisé, puis appliquer un dégradé de couleur de ce matériel basé sur le pavé tactile de heure dernière entrée a été reçue.</span><span class="sxs-lookup"><span data-stu-id="bf003-437">This was done by retrieving the Touchpad element from the controller, replacing its material with a custom material, then applying a gradient to that material's color based on the last time touchpad input was received.</span></span>

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

<span data-ttu-id="bf003-438">**Sélection de l’outil Pinceau avec une entrée tactile**</span><span class="sxs-lookup"><span data-stu-id="bf003-438">**Brush tool selection with touchpad input**</span></span>

<span data-ttu-id="bf003-439">Lorsque le sélecteur de pinceau détecte l’entrée appuyé du pavé tactile, il vérifie la position de l’entrée pour déterminer si elle a été vers la gauche ou droite.</span><span class="sxs-lookup"><span data-stu-id="bf003-439">When the brush selector detects touchpad's pressed input, it checks the position of the input to determine if it was to the left or right.</span></span>

<span data-ttu-id="bf003-440">**Épaisseur du trait avec selectPressedAmount**</span><span class="sxs-lookup"><span data-stu-id="bf003-440">**Stroke thickness with selectPressedAmount**</span></span>

<span data-ttu-id="bf003-441">Au lieu du **InteractionSourcePressType.Select** événement dans le **InteractionSourcePressed()**, vous pouvez obtenir la valeur analogique du montant appuyé via **selectPressedAmount**.</span><span class="sxs-lookup"><span data-stu-id="bf003-441">Instead of the **InteractionSourcePressType.Select** event in the **InteractionSourcePressed()**, you can get the analog value of the pressed amount through **selectPressedAmount**.</span></span> <span data-ttu-id="bf003-442">Cette valeur peut être récupérée dans **InteractionSourceUpdated()**.</span><span class="sxs-lookup"><span data-stu-id="bf003-442">This value can be retrieved in **InteractionSourceUpdated()**.</span></span>

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

<span data-ttu-id="bf003-443">**Script de la gomme**</span><span class="sxs-lookup"><span data-stu-id="bf003-443">**Eraser script**</span></span>

<span data-ttu-id="bf003-444">**Gomme** est un type spécial de pinceau qui remplace la base de **pinceau**de **DrawOverTime()** (fonction).</span><span class="sxs-lookup"><span data-stu-id="bf003-444">**Eraser** is a special type of brush that overrides the base **Brush**'s **DrawOverTime()** function.</span></span> <span data-ttu-id="bf003-445">Bien que le dessin est true, la gomme vérifie si son info-bulle se croise avec des traits de pinceau existant.</span><span class="sxs-lookup"><span data-stu-id="bf003-445">While Draw is true, the eraser checks to see if its tip intersects with any existing brush strokes.</span></span> <span data-ttu-id="bf003-446">Dans l’affirmative, ils sont ajoutés à une file d’attente pour être réduit vers le bas et supprimées.</span><span class="sxs-lookup"><span data-stu-id="bf003-446">If it does, they are added to a queue to be shrunk down and deleted.</span></span>

## <a name="advanced-design---teleportation-and-locomotion"></a><span data-ttu-id="bf003-447">Conception avancée - téléportation et locomotion</span><span class="sxs-lookup"><span data-stu-id="bf003-447">Advanced design - Teleportation and locomotion</span></span>

<span data-ttu-id="bf003-448">Si vous souhaitez autoriser l’utilisateur à déplacer la scène avec téléportation à l’aide de stick analogique, utilisez **MixedRealityCameraParent** au lieu de **MixedRealityCamera**.</span><span class="sxs-lookup"><span data-stu-id="bf003-448">If you want to allow the user to move around the scene with teleportation using thumbstick, use **MixedRealityCameraParent** instead of **MixedRealityCamera**.</span></span> <span data-ttu-id="bf003-449">Vous devez également ajouter **InputManager** et **DefaultCusor**.</span><span class="sxs-lookup"><span data-stu-id="bf003-449">You also need to add **InputManager** and **DefaultCusor**.</span></span> <span data-ttu-id="bf003-450">Dans la mesure où **MixedRealityCameraParent** inclut déjà **MotionControllers** et **limite** en tant que composants enfants, vous devez supprimer existant  **MotionControllers** et **environnement** prefab.</span><span class="sxs-lookup"><span data-stu-id="bf003-450">Since **MixedRealityCameraParent** already includes **MotionControllers** and **Boundary** as child components, you should remove existing **MotionControllers** and **Environment** prefab.</span></span>

### <a name="instructions"></a><span data-ttu-id="bf003-451">Instructions</span><span class="sxs-lookup"><span data-stu-id="bf003-451">Instructions</span></span>

* <span data-ttu-id="bf003-452">Dans le **hiérarchie** panel, supprimer **MixedRealityCamera**, **environnement** et **MotionControllers**</span><span class="sxs-lookup"><span data-stu-id="bf003-452">In the **Hierarchy** panel, delete **MixedRealityCamera**, **Environment** and **MotionControllers**</span></span>
* <span data-ttu-id="bf003-453">À partir de la **panneau projet**, recherchez et faites glisser les prefabs suivants dans le **hiérarchie** panneau :</span><span class="sxs-lookup"><span data-stu-id="bf003-453">From the **Project panel**, search and drag the following prefabs into the **Hierarchy** panel:</span></span>
    * <span data-ttu-id="bf003-454">Assets/AppPrefabs/Input/Prefabs/**MixedRealityCameraParent**</span><span class="sxs-lookup"><span data-stu-id="bf003-454">Assets/AppPrefabs/Input/Prefabs/**MixedRealityCameraParent**</span></span>
    * <span data-ttu-id="bf003-455">Assets/AppPrefabs/Input/Prefabs/**InputManager**</span><span class="sxs-lookup"><span data-stu-id="bf003-455">Assets/AppPrefabs/Input/Prefabs/**InputManager**</span></span>
    * <span data-ttu-id="bf003-456">Assets/AppPrefabs/Input/Prefabs/Cursor/**DefaultCursor**</span><span class="sxs-lookup"><span data-stu-id="bf003-456">Assets/AppPrefabs/Input/Prefabs/Cursor/**DefaultCursor**</span></span>

![Parent de la caméra de réalité mixte](images/mr213-cameraparent-300px.png)
* <span data-ttu-id="bf003-458">Dans le **hiérarchie** du panneau, cliquez sur **Gestionnaire d’entrée**</span><span class="sxs-lookup"><span data-stu-id="bf003-458">In the **Hierarchy** panel, click **Input Manager**</span></span>
* <span data-ttu-id="bf003-459">Dans le **inspecteur** du panneau, faites défiler jusqu'à la **Simple sélecteur de pointeur unique** section</span><span class="sxs-lookup"><span data-stu-id="bf003-459">In the **Inspector** panel, scroll down to the **Simple Single Pointer Selector** section</span></span>
* <span data-ttu-id="bf003-460">À partir de la **hiérarchie** volet, faites glisser **DefaultCursor** dans **curseur** champ</span><span class="sxs-lookup"><span data-stu-id="bf003-460">From the **Hierarchy** panel, drag **DefaultCursor** into **Cursor** field</span></span>

![Affectation de DefaultCursor](images/mr213-defaultcursor-500px.png)
* <span data-ttu-id="bf003-462">**Enregistrer** la scène et cliquez sur le **lire** bouton.</span><span class="sxs-lookup"><span data-stu-id="bf003-462">**Save** the scene and click the **play** button.</span></span> <span data-ttu-id="bf003-463">Vous serez en mesure d’utiliser le stick analogique gauche/droite ou teleport.</span><span class="sxs-lookup"><span data-stu-id="bf003-463">You will be able to use the thumbstick to rotate left/right or teleport.</span></span>

## <a name="the-end"></a><span data-ttu-id="bf003-464">La fin</span><span class="sxs-lookup"><span data-stu-id="bf003-464">The end</span></span>

<span data-ttu-id="bf003-465">Et c’est la fin de ce didacticiel !</span><span class="sxs-lookup"><span data-stu-id="bf003-465">And that's the end of this tutorial!</span></span> <span data-ttu-id="bf003-466">Vous avez appris :</span><span class="sxs-lookup"><span data-stu-id="bf003-466">You learned:</span></span>
* <span data-ttu-id="bf003-467">Comment travailler avec des modèles de contrôleur de mouvement dans le mode de jeu d’Unity et d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bf003-467">How to work with motion controller models in Unity's game mode and runtime.</span></span>
* <span data-ttu-id="bf003-468">Comment utiliser différents types d’événements de bouton et de leurs applications.</span><span class="sxs-lookup"><span data-stu-id="bf003-468">How to use different types of button events and their applications.</span></span>
* <span data-ttu-id="bf003-469">Guide pratique pour superposer des éléments d’interface utilisateur sur le contrôleur ou de personnaliser entièrement.</span><span class="sxs-lookup"><span data-stu-id="bf003-469">How to overlay UI elements on top of the controller or fully customize it.</span></span>

<span data-ttu-id="bf003-470">Vous êtes maintenant prêt à commencer à créer votre propre expérience d’immersion avec des contrôleurs de motion !</span><span class="sxs-lookup"><span data-stu-id="bf003-470">You are now ready to start creating your own immersive experience with motion controllers!</span></span>

## <a name="completed-scenes"></a><span data-ttu-id="bf003-471">Arrière-plan terminée</span><span class="sxs-lookup"><span data-stu-id="bf003-471">Completed scenes</span></span>

* <span data-ttu-id="bf003-472">Dans Unity **projet** panneau, cliquez sur le **scènes** dossier.</span><span class="sxs-lookup"><span data-stu-id="bf003-472">In Unity's **Project** panel click on the **Scenes** folder.</span></span>
* <span data-ttu-id="bf003-473">Vous trouverez deux écrans Unity **MixedReality213** et **MixedReality213Advanced**.</span><span class="sxs-lookup"><span data-stu-id="bf003-473">You will find two Unity sceens **MixedReality213** and **MixedReality213Advanced**.</span></span>
    * <span data-ttu-id="bf003-474">**MixedReality213**: Scène terminée avec un pinceau unique</span><span class="sxs-lookup"><span data-stu-id="bf003-474">**MixedReality213**: Completed scene with single brush</span></span>
    * <span data-ttu-id="bf003-475">**MixedReality213Advanced**: Scène terminé avec plusieurs pinceau avec exemple de quantité appuyez sur bouton sélection</span><span class="sxs-lookup"><span data-stu-id="bf003-475">**MixedReality213Advanced**: Completed scene with multiple brush with select button's press amount example</span></span>

## <a name="see-also"></a><span data-ttu-id="bf003-476">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="bf003-476">See also</span></span>

* [<span data-ttu-id="bf003-477">Fichiers de projet 213 d’entrée M.</span><span class="sxs-lookup"><span data-stu-id="bf003-477">MR Input 213 project files</span></span>](https://github.com/Microsoft/MixedReality213)
* [<span data-ttu-id="bf003-478">Toolkit de réalité mixte - scène de Test de contrôleur de mouvement</span><span class="sxs-lookup"><span data-stu-id="bf003-478">Mixed Reality Toolkit - Motion Controller Test scene</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/Input/Scenes)
* [<span data-ttu-id="bf003-479">Réalité mixte Toolkit - mécanique de manipulation</span><span class="sxs-lookup"><span data-stu-id="bf003-479">Mixed Reality Toolkit - Grab Mechanics</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/MotionControllers-GrabMechanics)
* [<span data-ttu-id="bf003-480">Directives de développement de contrôleur de mouvement</span><span class="sxs-lookup"><span data-stu-id="bf003-480">Motion controller development guidelines</span></span>](motion-controllers.md)
