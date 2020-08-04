---
title: Tutoriels de démarrage - 4. Positionnement des objets dans la scène
description: Ce cours vous montre comment utiliser Mixed Reality Toolkit (MRTK) pour créer une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 71990db23b5154de916f0eda86a978885ab53547
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376631"
---
# <a name="4-positioning-objects-in-the-scene"></a><span data-ttu-id="d8ebd-105">4. Positionnement des objets dans la scène</span><span class="sxs-lookup"><span data-stu-id="d8ebd-105">4. Positioning objects in the scene</span></span>

## <a name="overview"></a><span data-ttu-id="d8ebd-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="d8ebd-106">Overview</span></span>

<span data-ttu-id="d8ebd-107">Dans ce tutoriel, vous allez importer les ressources du tutoriel et positionner les objets fournis dans la scène.</span><span class="sxs-lookup"><span data-stu-id="d8ebd-107">In this tutorial, you will import the tutorial assets and position the provided objects in the scene.</span></span>

## <a name="objectives"></a><span data-ttu-id="d8ebd-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="d8ebd-108">Objectives</span></span>

* <span data-ttu-id="d8ebd-109">Apprendre à positionner des objets dans la scène</span><span class="sxs-lookup"><span data-stu-id="d8ebd-109">Learn how to position objects in the scene</span></span>
* <span data-ttu-id="d8ebd-110">Apprendre à utiliser la fonctionnalité Grid Object Collection du MRTK</span><span class="sxs-lookup"><span data-stu-id="d8ebd-110">Learn how to use MRTK's Grid Object Collection feature</span></span>

## <a name="importing-the-tutorial-assets"></a><span data-ttu-id="d8ebd-111">Importation des ressources du tutoriel</span><span class="sxs-lookup"><span data-stu-id="d8ebd-111">Importing the tutorial assets</span></span>

<span data-ttu-id="d8ebd-112">Téléchargez et importez le package personnalisé Unity suivant :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-112">Download and import the following Unity custom package:</span></span>

* [<span data-ttu-id="d8ebd-113">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.4.0.unitypackage</span><span class="sxs-lookup"><span data-stu-id="d8ebd-113">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.4.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.4.0/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.4.0.unitypackage)

<span data-ttu-id="d8ebd-114">Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-114">After you have imported the tutorial assets your Project window should look similar to this:</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section1-step1-1.png)

> [!TIP]
> <span data-ttu-id="d8ebd-116">Pour vous rappeler comment importer un package personnalisé Unity, reportez-vous aux instructions fournies dans [Importation du MRTK](mr-learning-base-02.md#importing-the-mixed-reality-toolkit).</span><span class="sxs-lookup"><span data-stu-id="d8ebd-116">For a reminder on how to import a Unity custom package, you can refer to the [Importing the MRTK](mr-learning-base-02.md#importing-the-mixed-reality-toolkit) instructions.</span></span>

## <a name="creating-the-parent-object"></a><span data-ttu-id="d8ebd-117">Création de l’objet parent</span><span class="sxs-lookup"><span data-stu-id="d8ebd-117">Creating the parent object</span></span>

<span data-ttu-id="d8ebd-118">Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur une zone vide et sélectionnez **Create Empty** pour ajouter un objet vide à votre scène :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-118">In the Hierarchy window, right-click on an empty spot, and select **Create Empty** to add an empty object to your scene:</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section2-step1-1.png)

> [!TIP]
> <span data-ttu-id="d8ebd-120">Pour afficher côte à côte les fenêtres Scene et Game comme dans l’image ci-dessus, faites glisser la fenêtre Game à droite de la fenêtre Scene.</span><span class="sxs-lookup"><span data-stu-id="d8ebd-120">To display your Scene and Game window side by side as shown in the image above, drag the Game window to the right side of the Scene window.</span></span> <span data-ttu-id="d8ebd-121">Pour en savoir plus, consultez la page consacrée à la <a href="https://docs.unity3d.com/Manual/CustomizingYourWorkspace.html" target="_blank">personnalisation de votre espace de travail</a> dans la documentation Unity.</span><span class="sxs-lookup"><span data-stu-id="d8ebd-121">To learn more about customizing your workspace, you can refer to Unity's <a href="https://docs.unity3d.com/Manual/CustomizingYourWorkspace.html" target="_blank">Customizing Your Workspace</a> documentation.</span></span>

<span data-ttu-id="d8ebd-122">Cliquez avec le bouton droit sur l’objet que vous venez de créer, sélectionnez **Rename**, puis remplacez le nom par **RoverExplorer** :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-122">Right-click on the newly created object, select **Rename**, and change the name to **RoverExplorer**:</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section2-step1-2.png)

<span data-ttu-id="d8ebd-124">L’objet RoverExplorer étant toujours sélectionné, dans la fenêtre Inspector, configurez le composant **Transform** comme ceci :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-124">With the RoverExplorer object still selected, in the Inspector window, configure the **Transform** component as follows:</span></span>

* <span data-ttu-id="d8ebd-125">**Position** : X = 0, Y = -0.6, Z = 2</span><span class="sxs-lookup"><span data-stu-id="d8ebd-125">**Position**: X = 0, Y = -0.6, Z = 2</span></span>
* <span data-ttu-id="d8ebd-126">**Rotation** : X = 0, Y = 0, Z = 0</span><span class="sxs-lookup"><span data-stu-id="d8ebd-126">**Rotation**: X = 0, Y = 0, Z = 0</span></span>
* <span data-ttu-id="d8ebd-127">**Scale** : X = 1, Y = 1, Z = 1</span><span class="sxs-lookup"><span data-stu-id="d8ebd-127">**Scale**: X = 1, Y = 1, Z = 1</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section2-step1-3.png)

> [!NOTE]
> <span data-ttu-id="d8ebd-129">L’appareil photo, qui représente la tête de l’utilisateur, est positionné à l’origine (X = 0, Y = 0, Z = 0).</span><span class="sxs-lookup"><span data-stu-id="d8ebd-129">The camera represents the users head and is positioned at origin, X = 0, Y = 0, Z = 0.</span></span> <span data-ttu-id="d8ebd-130">En règle générale, 1 unité dans Unity correspond à peu près à 1 mètre dans le monde physique.</span><span class="sxs-lookup"><span data-stu-id="d8ebd-130">In general, 1 unit in Unity is roughly 1 meter in the physical world.</span></span> <span data-ttu-id="d8ebd-131">Il y a cependant des exceptions à cela, par exemple quand les objets sont des enfants d’objets mis à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="d8ebd-131">However, there are exceptions to this, for example, when objects are children of scaled objects.</span></span> <span data-ttu-id="d8ebd-132">Dans le scénario ci-dessus, l’objet RoverExplorer est positionné 2 mètres devant la tête de l’utilisateur et 0,6 mètre en dessous.</span><span class="sxs-lookup"><span data-stu-id="d8ebd-132">In the scenario above, the RoverExplorer is positioned 2 meters in front of and 0.6 meters below the user's head.</span></span>

## <a name="adding-the-tutorial-prefabs"></a><span data-ttu-id="d8ebd-133">Ajout des préfabriqués du tutoriel</span><span class="sxs-lookup"><span data-stu-id="d8ebd-133">Adding the tutorial prefabs</span></span>

<span data-ttu-id="d8ebd-134">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-134">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** folder:</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section3-step1-1.png)

> [!TIP]
> <span data-ttu-id="d8ebd-136">Un <a href="https://docs.unity3d.com/Manual/Prefabs.html" target="_blank">préfabriqué</a> (Prefab) est un GameObject préconfiguré stocké en tant que ressource Unity et qui peut être réutilisé dans tout votre projet.</span><span class="sxs-lookup"><span data-stu-id="d8ebd-136">A <a href="https://docs.unity3d.com/Manual/Prefabs.html" target="_blank">prefab</a> is a pre-configured GameObject stored as a Unity Asset and can be reused throughout your project.</span></span>

<span data-ttu-id="d8ebd-137">Dans la fenêtre Project, cliquez sur le préfabriqué **Table** et faites-le glisser sur l’objet **RoverExplorer** pour en faire un enfant de cet objet, puis dans la fenêtre Inspector, configurez le composant **Transform** comme ceci :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-137">From the Project window, click-and-drag the **Table** prefab on to the **RoverExplorer** object to make it a child of the RoverExplorer object, then in the Inspector window, configure the **Transform** component as follows:</span></span>

* <span data-ttu-id="d8ebd-138">**Position** : X = 0, Y = -0.005, Z = 0</span><span class="sxs-lookup"><span data-stu-id="d8ebd-138">**Position**: X = 0, Y = -0.005, Z = 0</span></span>
* <span data-ttu-id="d8ebd-139">**Rotation** : X = 0, Y = 0, Z = 0</span><span class="sxs-lookup"><span data-stu-id="d8ebd-139">**Rotation**: X = 0, Y = 0, Z = 0</span></span>
* <span data-ttu-id="d8ebd-140">**Scale** : X = 1.2, Y = 0.01, Z = 1.2</span><span class="sxs-lookup"><span data-stu-id="d8ebd-140">**Scale**: X = 1.2, Y = 0.01, Z = 1.2</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section3-step1-2.png)

> [!TIP]
> <span data-ttu-id="d8ebd-142">Pour afficher votre scène comme dans l’image ci-dessus, utilisez le <a href="https://docs.unity3d.com/Manual/SceneViewNavigation.html" target="_blank">gizmo Scene</a> en haut à droite de la fenêtre Scene pour ajuster l’angle de visualisation sur l’axe Z vers l’avant, double-cliquez sur l’objet MixedRealityPlayspace dans la fenêtre Hierarchy pour avoir le focus sur l’appareil photo, puis faites un zoom avant si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d8ebd-142">To display your scene as shown in the image above, use the <a href="https://docs.unity3d.com/Manual/SceneViewNavigation.html" target="_blank">Scene Gizmo</a>, located in the top right corner of the Scene window, to adjust the viewing angle to be along the forward Z axis, double-click the MixedRealityPlayspace object to focus on the camera, and zoom in as needed.</span></span>

<span data-ttu-id="d8ebd-143">Dans la fenêtre Project, cliquez sur le préfabriqué **RoverAssembly** et faites-le glisser sur l’objet **RoverExplorer** pour en faire un enfant de cet objet, puis dans la fenêtre Inspector, configurez le composant **Transform** comme ceci :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-143">From the Project window, click-and-drag the **RoverAssembly** prefab on to the **RoverExplorer** object to make it a child of the RoverExplorer object, then in the Inspector window, configure the **Transform** component as follows:</span></span>

* <span data-ttu-id="d8ebd-144">**Position** : X = -0.1, Y = 0, Z = 0</span><span class="sxs-lookup"><span data-stu-id="d8ebd-144">**Position**: X = -0.1, Y = 0, Z = 0</span></span>
* <span data-ttu-id="d8ebd-145">**Rotation** : X = 0, Y = -135, Z = 0</span><span class="sxs-lookup"><span data-stu-id="d8ebd-145">**Rotation**: X = 0, Y = -135, Z = 0</span></span>
* <span data-ttu-id="d8ebd-146">**Scale** : X = 1, Y = 1, Z = 1</span><span class="sxs-lookup"><span data-stu-id="d8ebd-146">**Scale**: X = 1, Y = 1, Z = 1</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section3-step1-3.png)

## <a name="organizing-objects-in-a-collection"></a><span data-ttu-id="d8ebd-148">Organisation des objets dans une collection</span><span class="sxs-lookup"><span data-stu-id="d8ebd-148">Organizing objects in a collection</span></span>

<span data-ttu-id="d8ebd-149">Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur l’objet **RoverExplorer**, puis sélectionnez **Create Empty** pour ajouter un objet vide en tant qu’enfant de RoverExplorer. Nommez l’objet **RoverParts**, puis configurez le composant **Transform** comme ceci :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-149">In the Hierarchy window, right-click on the **RoverExplorer** object and select **Create Empty** to add an empty object as a child of the RoverExplorer, name the object **RoverParts**, and configure the **Transform** component as follows:</span></span>

* <span data-ttu-id="d8ebd-150">**Position** : X = 0, Y = 0.06, Z = 0</span><span class="sxs-lookup"><span data-stu-id="d8ebd-150">**Position**: X = 0, Y = 0.06, Z = 0</span></span>
* <span data-ttu-id="d8ebd-151">**Rotation** : X = 0, Y = 90, Z = 0</span><span class="sxs-lookup"><span data-stu-id="d8ebd-151">**Rotation**: X = 0, Y = 90, Z = 0</span></span>
* <span data-ttu-id="d8ebd-152">**Scale** : X = 1, Y = 1, Z = 1</span><span class="sxs-lookup"><span data-stu-id="d8ebd-152">**Scale**: X = 1, Y = 1, Z = 1</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-1.png)

<span data-ttu-id="d8ebd-154">Dans la fenêtre Hierarchy, sélectionnez tous les objets enfants RoverExplorer > RoverAssembly > RoverModel > **Parts**, cliquez dessus avec le bouton droit, puis sélectionnez **Duplicate** pour créer une copie de chaque élément :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-154">In the Hierarchy window, select all the RoverExplorer > RoverAssembly > RoverModel > **Parts** child objects, right-click on them and select **Duplicate** to create a copy of each of the parts:</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-2.png)

> [!TIP]
> <span data-ttu-id="d8ebd-156">Pour sélectionner plusieurs objets adjacents, maintenez la touche Maj enfoncée tout en utilisant la souris pour sélectionner le premier et le dernier objet.</span><span class="sxs-lookup"><span data-stu-id="d8ebd-156">To select multiple adjacent objects, press-and-hold the SHIFT key while using the mouse to select the first and last object.</span></span>

<span data-ttu-id="d8ebd-157">Les objets enfants Parts que vous venez de dupliquer étant toujours sélectionnés, cliquez dessus et faites-les glisser sur l’objet **RoverParts** pour en faire des objets enfants de cet objet :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-157">With the newly duplicated Parts child objects still selected, click-and-drag them on to the **RoverParts** object to make them child objects of the RoverParts object:</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-3.png)

<span data-ttu-id="d8ebd-159">Pour faciliter l’utilisation de votre scène, dans la fenêtre Hierarchy, cliquez sur l’icône **œil** à gauche de l’objet pour désactiver la **visibilité de la scène** pour l’objet **RoverExplorer**.</span><span class="sxs-lookup"><span data-stu-id="d8ebd-159">To make it easier to work with your scene, in the Hierarchy window, click the **eye** icon to the left of the object to toggle the **scene visibility** for the **RoverExplorer** object off.</span></span> <span data-ttu-id="d8ebd-160">Cette opération masque l’objet dans la fenêtre Scene sans changer sa visibilité dans le jeu :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-160">This hides the object in the Scene window without changing its in-game visibility:</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-4.png)

> [!TIP]
> <span data-ttu-id="d8ebd-162">Pour en savoir plus sur les contrôles de visibilité de la scène et sur la façon dont vous pouvez les utiliser pour optimiser l’affichage et le workflow de votre scène, reportez-vous à la documentation <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">Scene Visibility</a> d’Unity.</span><span class="sxs-lookup"><span data-stu-id="d8ebd-162">To learn more about the Scene Visibility controls and how you can use them to optimize your scene view and workflow, you can refer to Unity's <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">Scene Visibility</a> documentation.</span></span>

<span data-ttu-id="d8ebd-163">Dans la fenêtre Hierarchy, nettoyez les noms des objets enfants RoverParts en remplaçant le suffixe **(1)** par **_Part** :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-163">In the Hierarchy window, clean up the RoverParts child objects' names by replacing the appended **(1)** with **_Part**:</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-5.png)

<span data-ttu-id="d8ebd-165">Dans la fenêtre Hierarchy, sélectionnez l’objet **RoverParts**. Dans la fenêtre Inspector, cliquez sur le bouton **Add Component**, puis recherchez et sélectionnez **GridObjectCollection** pour ajouter le composant GridObjectCollection à l’objet RoverParts :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-165">In the Hierarchy window, select the **RoverParts** object, then in the Inspector window, click the **Add Component** button, and search for and select **GridObjectCollection** to add the GridObjectCollection component to the RoverParts object:</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-6.png)

<span data-ttu-id="d8ebd-167">Configurez les valeurs du composant **GridObjectCollection** comme ceci :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-167">Configure the **GridObjectCollection** component values as follows:</span></span>

* <span data-ttu-id="d8ebd-168">**Sort Type** : Alphabetic</span><span class="sxs-lookup"><span data-stu-id="d8ebd-168">**Sort Type**: Alphabetic</span></span>
* <span data-ttu-id="d8ebd-169">**Layout** : Horizontale</span><span class="sxs-lookup"><span data-stu-id="d8ebd-169">**Layout**: Horizontal</span></span>
* <span data-ttu-id="d8ebd-170">**Cell Width** : 0.25</span><span class="sxs-lookup"><span data-stu-id="d8ebd-170">**Cell Width**: 0.25</span></span>
* <span data-ttu-id="d8ebd-171">**Distance from parent** : 0.38</span><span class="sxs-lookup"><span data-stu-id="d8ebd-171">**Distance from parent**: 0.38</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-7.png)

<span data-ttu-id="d8ebd-173">Cliquez ensuite sur le bouton **Update Collection** pour mettre à jour la position des objets enfants de RoverParts :</span><span class="sxs-lookup"><span data-stu-id="d8ebd-173">Then click the **Update Collection** button to update the position of the RoverParts child objects:</span></span>

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-8.png)

## <a name="congratulations"></a><span data-ttu-id="d8ebd-175">Félicitations</span><span class="sxs-lookup"><span data-stu-id="d8ebd-175">Congratulations</span></span>

<span data-ttu-id="d8ebd-176">Dans ce tutoriel, vous avez appris à positionner des objets dans la scène par rapport à l’utilisateur et à utiliser la fonctionnalité Grid Object Collection du MRTK pour organiser les objets dans une collection.</span><span class="sxs-lookup"><span data-stu-id="d8ebd-176">In this tutorial, you learned how to position objects in the scene relative to the user and use MRTK's Grid Object Collection feature to organize objects in a collection.</span></span>

[<span data-ttu-id="d8ebd-177">Tutoriel suivant : 5. Création de contenu dynamique avec des solveurs</span><span class="sxs-lookup"><span data-stu-id="d8ebd-177">Next Tutorial: 5. Creating dynamic content using Solvers</span></span>](mr-learning-base-05.md)
