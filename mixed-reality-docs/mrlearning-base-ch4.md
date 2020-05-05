---
title: Tutoriels de démarrage - 5. Interaction avec les objets 3D
description: Découvrez plus d’informations sur le contenu 3D de base et les expériences utilisateur, comme l’organisation des objets 3D et des zones englobantes pour la manipulation de base.
author: jessemcculloch
ms.author: jemccull
ms.date: 05/02/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: b807ac7e51e4009d2c44d3b7c67fbdf3488ccbd9
ms.sourcegitcommit: 92ff5478a5c55b4e2c5cc2f44f1588702f4ec5d1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82604990"
---
# <a name="5-interacting-with-3d-objects"></a><span data-ttu-id="71b16-105">5. Interaction avec les objets 3D</span><span class="sxs-lookup"><span data-stu-id="71b16-105">5. Interacting with 3D objects</span></span>

<span data-ttu-id="71b16-106">Dans ce tutoriel, vous allez découvrir des informations sur les objets 3D de base et l’expérience utilisateur, comme l’organisation des objets 3D dans le cadre d’une collection, les cadres englobants pour la manipulation de base, l’interaction de près et de loin, les gestes tactiles et de préhension avec le suivi de la main.</span><span class="sxs-lookup"><span data-stu-id="71b16-106">In this tutorial, you will learn about basic 3D content and user experience, such as organizing 3D objects as part of a collection, bounding boxes for basic manipulation, near and far interaction, and touch and grab gestures with hand tracking.</span></span>

## <a name="objectives"></a><span data-ttu-id="71b16-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="71b16-107">Objectives</span></span>

* <span data-ttu-id="71b16-108">Créer un panneau d’objets 3D qui sera utilisé pour les autres objectifs d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="71b16-108">Create a panel of 3D objects which will be used for the other learning objectives</span></span>
* <span data-ttu-id="71b16-109">Implémenter des cadres englobants</span><span class="sxs-lookup"><span data-stu-id="71b16-109">Implement bounding boxes</span></span>
* <span data-ttu-id="71b16-110">Configurer des objets 3D pour la manipulation de base, comme le déplacement, la rotation et la mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="71b16-110">Configure 3D objects for basic manipulation such as move, rotate, and scale</span></span>
* <span data-ttu-id="71b16-111">Explorer l’interaction de près et de loin</span><span class="sxs-lookup"><span data-stu-id="71b16-111">Explore near and far interaction</span></span>
* <span data-ttu-id="71b16-112">Découvrir des informations sur les gestes de suivi de la main, comme la préhension et l’interaction tactile</span><span class="sxs-lookup"><span data-stu-id="71b16-112">Learn about additional hand tracking gestures, such as grab and touch</span></span>

## <a name="importing-the-tutorial-assets"></a><span data-ttu-id="71b16-113">Importation des ressources du tutoriel</span><span class="sxs-lookup"><span data-stu-id="71b16-113">Importing the tutorial assets</span></span>

<span data-ttu-id="71b16-114">Téléchargez et importez le package personnalisé Unity :</span><span class="sxs-lookup"><span data-stu-id="71b16-114">Download and import the Unity custom package:</span></span>

* [<span data-ttu-id="71b16-115">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage</span><span class="sxs-lookup"><span data-stu-id="71b16-115">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.3/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage)

<span data-ttu-id="71b16-116">Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="71b16-116">After you have imported the tutorial assets your Project window should look similar to this:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section1-step1-1.png)

> [!TIP]
> <span data-ttu-id="71b16-118">Pour un rappel de la façon d’importer un package personnalisé Unity, vous pouvez vous référer aux instructions de [Importer le Kit de ressources de réalité mixte](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit).</span><span class="sxs-lookup"><span data-stu-id="71b16-118">For a reminder on how to import a Unity custom package, you can refer to the [Import the Mixed Reality Toolkit](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit) instructions.</span></span>

## <a name="decluttering-the-scene-view"></a><span data-ttu-id="71b16-119">Désencombrement de la vue Scène</span><span class="sxs-lookup"><span data-stu-id="71b16-119">Decluttering the scene view</span></span>

<span data-ttu-id="71b16-120">Pour faciliter l’utilisation de votre scène, définissez **Scene visibility** pour les objets **Cube** et **ButtonCollection** sur Off en cliquant sur l’icône d’**œil** à gauche des objets.</span><span class="sxs-lookup"><span data-stu-id="71b16-120">To make it easier to work with your scene, set the **scene visibility** for the **Cube** and **ButtonCollection** objects to off by clicking the **eye** icon to the left of the objects.</span></span> <span data-ttu-id="71b16-121">Ceci masque l’objet dans la fenêtre Scene sans modifier sa visibilité dans le jeu :</span><span class="sxs-lookup"><span data-stu-id="71b16-121">This hides the object in the Scene window without changing their in-game visibility:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section2-step1-1.png)

> [!TIP]
> <span data-ttu-id="71b16-123">Pour en savoir plus sur les contrôles de visibilité de la scène et sur la façon dont vous pouvez les utiliser pour optimiser l’affichage et le workflow de votre scène, vous pouvez consulter la documentation <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">Scene Visibility</a> d’Unity.</span><span class="sxs-lookup"><span data-stu-id="71b16-123">To learn more about the Scene Visibility controls and how you can use them to optimize your scene view and workflow, you can visit Unity's <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">Scene Visibility</a> documentation.</span></span>

## <a name="organizing-3d-objects-in-a-collection"></a><span data-ttu-id="71b16-124">Organisation des objets 3D dans une collection</span><span class="sxs-lookup"><span data-stu-id="71b16-124">Organizing 3D objects in a collection</span></span>

<span data-ttu-id="71b16-125">Dans cette section, vous allez créer un panneau d’objets 3D que vous allez utiliser pour explorer les différentes façons d’interagir avec les objets 3D dans les sections suivantes de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="71b16-125">In this section, you will create a panel of 3D objects which you will use when exploring various ways of interacting with 3D objects in the following sections of this tutorial.</span></span> <span data-ttu-id="71b16-126">Plus précisément, vous allez configurer les objets 3D de manière à ce qu’ils soient positionnés sur une grille 3 x 3.</span><span class="sxs-lookup"><span data-stu-id="71b16-126">Specifically, you will configure the 3D objects to be positioned on a 3 x 3 grid.</span></span>

<span data-ttu-id="71b16-127">De la même façon que quand vous avez [créé un panneau de boutons](mrlearning-base-ch2.md#creating-a-panel-of-buttons-using-mrtks-grid-object-collection), les principales étapes à suivre pour y parvenir sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="71b16-127">Similarly to when you [created a panel of buttons](mrlearning-base-ch2.md#creating-a-panel-of-buttons-using-mrtks-grid-object-collection), the main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="71b16-128">Rattacher les objets 3D à un objet parent</span><span class="sxs-lookup"><span data-stu-id="71b16-128">Parent the 3D objects to a parent object</span></span>
2. <span data-ttu-id="71b16-129">Ajouter et configurer le composant Grid Object Collection (Script)</span><span class="sxs-lookup"><span data-stu-id="71b16-129">Add and configure the Grid Object Collection (Script) component</span></span>

### <a name="1-parent-the-3d-objects-to-a-parent-object"></a><span data-ttu-id="71b16-130">1. Rattacher les objets 3D à un objet parent</span><span class="sxs-lookup"><span data-stu-id="71b16-130">1. Parent the 3D objects to a parent object</span></span>

<span data-ttu-id="71b16-131">Dans la fenêtre Hierarchy, **créez un objet vide**, donnez-lui un nom approprié, par exemple **3DObjectCollection** et le positionnez-le à un emplacement approprié, par exemple X = 0 ; Y = -0,2 ; Z = 2.</span><span class="sxs-lookup"><span data-stu-id="71b16-131">In the Hierarchy window, **create an empty object**, give it a suitable name, for example, **3DObjectCollection**, and position it in a suitable location, for example, X = 0, Y = -0.2, Z = 2.</span></span>

<span data-ttu-id="71b16-132">Dans la fenêtre Project, accédez à **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs**, puis **rattachez** les préfabriqués suivants à **3DObjectCollection** :</span><span class="sxs-lookup"><span data-stu-id="71b16-132">In the Project window, navigate to **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs**, then **parent** the following prefabs to the **3DObjectCollection**:</span></span>

* <span data-ttu-id="71b16-133">Cheese</span><span class="sxs-lookup"><span data-stu-id="71b16-133">Cheese</span></span>
* <span data-ttu-id="71b16-134">CoffeeCup</span><span class="sxs-lookup"><span data-stu-id="71b16-134">CoffeeCup</span></span>
* <span data-ttu-id="71b16-135">EarthCore</span><span class="sxs-lookup"><span data-stu-id="71b16-135">EarthCore</span></span>
* <span data-ttu-id="71b16-136">Octa</span><span class="sxs-lookup"><span data-stu-id="71b16-136">Octa</span></span>
* <span data-ttu-id="71b16-137">Platonic</span><span class="sxs-lookup"><span data-stu-id="71b16-137">Platonic</span></span>
* <span data-ttu-id="71b16-138">TheModule</span><span class="sxs-lookup"><span data-stu-id="71b16-138">TheModule</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-1.png)

<span data-ttu-id="71b16-140">Dans la fenêtre Hierarchy, **créez trois cubes** en tant qu’objets enfants de **3DObjectCollection** et définissez la valeur **Scale** de leur transformation sur X = 0,15 ; Y = 0,15 ; Z = 0,15 :</span><span class="sxs-lookup"><span data-stu-id="71b16-140">In the Hierarchy window, **create three cubes** as a child objects of the **3DObjectCollection** and set their Transform **Scale** to X = 0.15, Y = 0.15, Z = 0.15:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-2.png)

> [!TIP]
> <span data-ttu-id="71b16-142">Pour un rappel de la façon d’effectuer les étapes listées ci-dessus, vous pouvez vous référer au tutoriel [Création de l’interface utilisateur et configuration du kit d’outils de réalité mixte](mrlearning-base-ch2.md).</span><span class="sxs-lookup"><span data-stu-id="71b16-142">For a reminder on how to do the steps listed above, you can refer to the [Creating user interface and configure Mixed Reality Toolkit](mrlearning-base-ch2.md) tutorial.</span></span>

<span data-ttu-id="71b16-143">Repositionnez les cubes de façon à voir chaque cube :</span><span class="sxs-lookup"><span data-stu-id="71b16-143">Reposition the cubes so you can see each cube:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-3.png)

<span data-ttu-id="71b16-145">Dans la fenêtre Project, accédez à **Assets** > **MixedRealityToolkit.SDK** > **StandardAssets** > **Materials** pour voir les matériaux fournis par le MRTK.</span><span class="sxs-lookup"><span data-stu-id="71b16-145">In the Project window, navigate to **Assets** > **MixedRealityToolkit.SDK** > **StandardAssets** > **Materials** to see materials provided with the MRTK.</span></span>

<span data-ttu-id="71b16-146">**Cliquez et faites glisser** un matériau approprié sur la propriété Mesh Renderer **Materials** Element 0 de chaque cube, par exemple :</span><span class="sxs-lookup"><span data-stu-id="71b16-146">**Click-and-drag** a suitable material on to each cube's Mesh Renderer **Materials** Element 0 property, for example:</span></span>

* <span data-ttu-id="71b16-147">MRTK_Standard_GlowingCyan</span><span class="sxs-lookup"><span data-stu-id="71b16-147">MRTK_Standard_GlowingCyan</span></span>
* <span data-ttu-id="71b16-148">MRTK_Standard_GlowingOrange</span><span class="sxs-lookup"><span data-stu-id="71b16-148">MRTK_Standard_GlowingOrange</span></span>
* <span data-ttu-id="71b16-149">MRTK_Standard_Green</span><span class="sxs-lookup"><span data-stu-id="71b16-149">MRTK_Standard_Green</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-4.png)

### <a name="2-add-and-configure-the-grid-object-collection-script-component"></a><span data-ttu-id="71b16-151">2. Ajouter et configurer le composant Grid Object Collection (Script)</span><span class="sxs-lookup"><span data-stu-id="71b16-151">2. Add and configure the Grid Object Collection (Script) component</span></span>

<span data-ttu-id="71b16-152">Ajoutez un composant **Grid Object Collection (Script)** à l’objet **3DObjectCollection** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="71b16-152">Add a **Grid Object Collection (Script)** component to the **3DObjectCollection** object, and configure it as follows:</span></span>

* <span data-ttu-id="71b16-153">Changez **Sort Type** en **Child Order** pour que les objets enfants soient triés dans l’ordre où vous les avez placés sous l’objet parent.</span><span class="sxs-lookup"><span data-stu-id="71b16-153">Change **Sort Type** to **Child Order** to ensure the child objects are sorted in the order you have placed them under the parent object</span></span>

<span data-ttu-id="71b16-154">Cliquez ensuite sur le bouton **Update Collection** pour appliquer la nouvelle configuration :</span><span class="sxs-lookup"><span data-stu-id="71b16-154">Then click the **Update Collection** button to apply the new configuration:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step2-1.png)

## <a name="manipulating-3d-objects"></a><span data-ttu-id="71b16-156">Manipulation d’objets 3D</span><span class="sxs-lookup"><span data-stu-id="71b16-156">Manipulating 3D objects</span></span>

<span data-ttu-id="71b16-157">Dans cette section, vous allez ajouter la possibilité de manipuler tous les objets 3D dans le panneau que vous avez créé dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="71b16-157">In this section, you will add the ability to manipulate all the 3D objects in the panel you created in the previous section.</span></span> <span data-ttu-id="71b16-158">En outre, pour les objets préfabriqués, vous allez permettre aux utilisateurs d’accéder à ces objets et de les saisir avec des mains suivies.</span><span class="sxs-lookup"><span data-stu-id="71b16-158">Additionally, for the prefab objects, you will enable users to reach out and grab these objects with tracked hands.</span></span> <span data-ttu-id="71b16-159">Vous allez ensuite explorer quelques comportements de manipulation que vous pouvez appliquer à vos objets.</span><span class="sxs-lookup"><span data-stu-id="71b16-159">Then you will explore a few manipulation behaviors that you can apply to your objects.</span></span>

<span data-ttu-id="71b16-160">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="71b16-160">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="71b16-161">Ajouter le composant Manipulation Handler (Script) à tous les objets</span><span class="sxs-lookup"><span data-stu-id="71b16-161">Add the Manipulation Handler (Script) component to all the objects</span></span>
2. <span data-ttu-id="71b16-162">Ajouter le composant Near Interaction Grabbable (Script) aux objets préfabriqués</span><span class="sxs-lookup"><span data-stu-id="71b16-162">Add the Near Interaction Grabbable (Script) component to the prefab objects</span></span>
3. <span data-ttu-id="71b16-163">Configurer le composant Manipulation Handler (Script)</span><span class="sxs-lookup"><span data-stu-id="71b16-163">Configure the Manipulation Handler (Script) component</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71b16-164">Pour pouvoir **manipuler un objet**, celui-ci doit avoir les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="71b16-164">To be able to **manipulate an object**, the object must have the following components:</span></span>
>
> * <span data-ttu-id="71b16-165">Le composant **Collider**, par exemple un Box Collider</span><span class="sxs-lookup"><span data-stu-id="71b16-165">**Collider** component, for example, a Box Collider</span></span>
> * <span data-ttu-id="71b16-166">Le composant **Manipulation Handler (Script)**</span><span class="sxs-lookup"><span data-stu-id="71b16-166">**Manipulation Handler (Script)** component</span></span>
>
> <span data-ttu-id="71b16-167">Pour pouvoir **manipuler** et **saisir** un objet avec les mains suivies, celui-ci doit avoir les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="71b16-167">To be able to **manipulate** and **grab an object with tracked hands**, the object must have the following components:</span></span>
>
> * <span data-ttu-id="71b16-168">Le composant **Collider**, par exemple un Box Collider</span><span class="sxs-lookup"><span data-stu-id="71b16-168">**Collider** component, for example, a Box Collider</span></span>
> * <span data-ttu-id="71b16-169">Le composant **Manipulation Handler (Script)**</span><span class="sxs-lookup"><span data-stu-id="71b16-169">**Manipulation Handler (Script)** component</span></span>
> * <span data-ttu-id="71b16-170">Le composant **Near Interaction Grabbable (Script)**</span><span class="sxs-lookup"><span data-stu-id="71b16-170">**Near Interaction Grabbable (Script)** component</span></span>

### <a name="1-add-the-manipulation-handler-script-component-to-all-the-objects"></a><span data-ttu-id="71b16-171">1. Ajouter le composant Manipulation Handler (Script) à tous les objets</span><span class="sxs-lookup"><span data-stu-id="71b16-171">1. Add the Manipulation Handler (Script) component to all the objects</span></span>

<span data-ttu-id="71b16-172">Dans la fenêtre Hierarchy, sélectionnez l’objet **Cheese**, maintenez la touche **Maj** enfoncée, puis sélectionnez l’objet **Cube () 2** et ajoutez le composant **Manipulation Handler (Script)** à tous les objets :</span><span class="sxs-lookup"><span data-stu-id="71b16-172">In the Hierarchy window, select the **Cheese** object, hold down the **Shift** key, and then select the **Cube () 2** object and add the **Manipulation Handler (Script)** component to all the objects:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step1-1.png)

> [!NOTE]
> <span data-ttu-id="71b16-174">Dans le cadre de ce tutoriel, les colliders ont déjà été ajoutés aux objets préfabriqués.</span><span class="sxs-lookup"><span data-stu-id="71b16-174">For the purpose of this tutorial, colliders have already been added to the prefabs.</span></span> <span data-ttu-id="71b16-175">Pour les primitives Unity, comme les objets Cube, le composant Collider est automatiquement ajouté lors de la création de l’objet.</span><span class="sxs-lookup"><span data-stu-id="71b16-175">For Unity primitives, such as the Cube objects, the Collider component is automatically added when the object is created.</span></span> <span data-ttu-id="71b16-176">Dans l’image ci-dessus, les colliders sont représentés par les contours verts.</span><span class="sxs-lookup"><span data-stu-id="71b16-176">In the image above, the colliders are represented by the green outlines.</span></span> <span data-ttu-id="71b16-177">Pour plus d’informations sur les colliders, vous pouvez consulter la documentation <a href="https://docs.unity3d.com/Manual/CollidersOverview.html" target="_blank">Collider</a> d’Unity.</span><span class="sxs-lookup"><span data-stu-id="71b16-177">To learn more about colliders, you can visit Unity's <a href="https://docs.unity3d.com/Manual/CollidersOverview.html" target="_blank">Collider</a> documentation.</span></span>

### <a name="2-add-the-near-interaction-grabbable-script-component-to-the-prefab-objects"></a><span data-ttu-id="71b16-178">2. Ajouter le composant Near Interaction Grabbable (Script) aux objets préfabriqués</span><span class="sxs-lookup"><span data-stu-id="71b16-178">2. Add the Near Interaction Grabbable (Script) component to the prefab objects</span></span>

<span data-ttu-id="71b16-179">Dans la fenêtre Hierarchy, sélectionnez l’objet **Cheese**, maintenez la touche **Maj** enfoncée, puis sélectionnez l’objet **TheModule** et ajoutez le composant **Near Interaction Grabbable (Script)** à tous les objets :</span><span class="sxs-lookup"><span data-stu-id="71b16-179">In the Hierarchy window, select the **Cheese** object, hold down the **Shift** key, and then select the **TheModule** object and add the **Near Interaction Grabbable (Script)** component to all the objects:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step2-1.png)

### <a name="3-configure-the-manipulation-handler-script-component"></a><span data-ttu-id="71b16-181">3. Configurer le composant Manipulation Handler (Script)</span><span class="sxs-lookup"><span data-stu-id="71b16-181">3. Configure the Manipulation Handler (Script) component</span></span>

#### <a name="default-manipulation"></a><span data-ttu-id="71b16-182">Manipulation par défaut</span><span class="sxs-lookup"><span data-stu-id="71b16-182">Default manipulation</span></span>

<span data-ttu-id="71b16-183">Pour l’objet **Cube**, laissez toutes les propriétés à leurs valeurs par défaut pour expérimenter le comportement de manipulation par défaut :</span><span class="sxs-lookup"><span data-stu-id="71b16-183">For the **Cube** object, leave all properties at default, to experience the default manipulation behavior:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-1.png)

> [!TIP]
> <span data-ttu-id="71b16-185">Pour rétablir les valeurs par défaut d’un composant, vous pouvez sélectionner l’icône Settings du composant, puis sélectionner Reset.</span><span class="sxs-lookup"><span data-stu-id="71b16-185">To reset a component to its default values, you can select the component's Settings icon and select Reset.</span></span>

#### <a name="restrict-manipulation-to-scale-only"></a><span data-ttu-id="71b16-186">Limiter la manipulation à la mise à l’échelle uniquement</span><span class="sxs-lookup"><span data-stu-id="71b16-186">Restrict manipulation to scale only</span></span>

<span data-ttu-id="71b16-187">Pour l’objet **Cube (1)** , changez **Two Handed Manipulation Type** en **Scale** pour autoriser l’utilisateur à seulement changer la taille de l’objet :</span><span class="sxs-lookup"><span data-stu-id="71b16-187">For the **Cube (1)** object, change **Two Handed Manipulation Type** to **Scale** to only allow the user to change the object's size:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-2.png)

#### <a name="constrain-the-movement-to-a-fixed-distance-from-the-user"></a><span data-ttu-id="71b16-189">Contraindre le mouvement à une distance fixe de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="71b16-189">Constrain the movement to a fixed distance from the user</span></span>

<span data-ttu-id="71b16-190">Pour l’objet **Cube (2)** , changez **Constraint On Movement** en **Fix Distance From Head** pour que, quand l’objet est déplacé, il reste à la même distance de l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="71b16-190">For the **Cube (2)** object, change **Constraint On Movement** to **Fix Distance From Head** so that when the object is moved, it stays at the same distance from the user:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-3.png)

#### <a name="default-grabbable-manipulation"></a><span data-ttu-id="71b16-192">Manipulation de préhension par défaut</span><span class="sxs-lookup"><span data-stu-id="71b16-192">Default grabbable manipulation</span></span>

<span data-ttu-id="71b16-193">Pour les objets **Cheese**, **CoffeCup** et **EarthCore**, laissez toutes les propriétés à leurs valeurs par défaut pour expérimenter le comportement de manipulation de préhension par défaut :</span><span class="sxs-lookup"><span data-stu-id="71b16-193">For the **Cheese**, **CoffeCup**, and **EarthCore** objects, leave all properties at default, to experience the default grabbable manipulation behavior:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-4.png)

#### <a name="remove-the-ability-of-far-manipulation"></a><span data-ttu-id="71b16-195">Supprimer la possibilité de manipulation de loin</span><span class="sxs-lookup"><span data-stu-id="71b16-195">Remove the ability of far manipulation</span></span>

<span data-ttu-id="71b16-196">Pour l’objet **Octa**, décochez la case **Allow Far Manipulation** pour que l’utilisateur puisse interagir avec l’objet seulement en utilisant les mains suivies :</span><span class="sxs-lookup"><span data-stu-id="71b16-196">For the **Octa** object, un-check the **Allow Far Manipulation** checkbox to make it so the user can only interact with the object directly using tracked hands:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-5.png)

#### <a name="make-an-object-rotate-around-its-center"></a><span data-ttu-id="71b16-198">Faire pivoter un objet autour de son centre</span><span class="sxs-lookup"><span data-stu-id="71b16-198">Make an object rotate around its center</span></span>

<span data-ttu-id="71b16-199">Pour l’objet **Platonic**, changez **One Hand Rotation Mode Near** et **One Hand Rotation Mode Far** en **Rotate About Object Center** pour que, quand l’utilisateur fait pivoter l’objet avec une main, il pivote autour de son centre :</span><span class="sxs-lookup"><span data-stu-id="71b16-199">For the **Platonic** object, change **One Hand Rotation Mode Near** and **One Hand Rotation Mode Far** to **Rotate About Object Center** to make it so when the user rotates the object with one hand, it rotates around the object's center:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-6.png)

#### <a name="keep-movement-after-object-is-released"></a><span data-ttu-id="71b16-201">Conserver le mouvement après que l’objet soit relâché</span><span class="sxs-lookup"><span data-stu-id="71b16-201">Keep movement after object is released</span></span>

<span data-ttu-id="71b16-202">Pour l’objet **TheModule**, ajoutez un composant **Rigidbody** pour activer les lois de la physique, puis décochez **Use Gravity** pour que l’objet ne soit pas affecté par la gravité :</span><span class="sxs-lookup"><span data-stu-id="71b16-202">For the **TheModule** object, add a **Rigidbody** component to enable physics, and then un-check the **Use Gravity** checkbox so the object is not affected by gravity:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-7.png)

<span data-ttu-id="71b16-204">De retour dans le composant Manipulation Handler (Script), vérifiez que **Release Behavior** est défini à la fois sur **Keep Velocity** et **Keep Angular Velocity** afin qu’une fois que l’objet est relâché par la main de l’utilisateur, il continue à se déplacer :</span><span class="sxs-lookup"><span data-stu-id="71b16-204">Back on the Manipulation Handler (Script) component, verify that the **Release Behavior** is set to both **Keep Velocity** and **Keep Angular Velocity** so that once the object is released from the user's hand, it continues to move:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-8.png)

<span data-ttu-id="71b16-206">Pour en savoir plus sur le composant Manipulation Handler et ses propriétés associées, vous pouvez consulter le guide [Manipulation handler](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="71b16-206">To learn more about the Manipulation handler component and its associated properties, you can visit the [Manipulation handler](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="adding-bounding-boxes"></a><span data-ttu-id="71b16-207">Ajout de cadres englobants</span><span class="sxs-lookup"><span data-stu-id="71b16-207">Adding bounding boxes</span></span>

<span data-ttu-id="71b16-208">Les cadres englobants facilitent et rendent plus intuitive la manipulation d’objets avec une main pour l’interaction proche et de loin en fournissant des poignées qui peuvent être utilisées pour la mise à l’échelle et la rotation.</span><span class="sxs-lookup"><span data-stu-id="71b16-208">Bounding boxes make it easier and more intuitive to manipulate objects with one hand for both near and far interaction by providing handles that can be used for scaling and rotating.</span></span>

<span data-ttu-id="71b16-209">Dans cet exemple, vous allez ajouter un cadre englobant à l’objet EarthCore pour permettre l’interaction avec cet objet en utilisant la manipulation d’objet que vous avez configurée dans la section précédente ainsi que la mise à l’échelle et la rotation, avec les poignées du cadre englobant.</span><span class="sxs-lookup"><span data-stu-id="71b16-209">In this example, you will add a bounding box to the EarthCore object so this object can now be interacted with using the object manipulation you configured in the previous section, as well as, scaled and rotated using the bounding box handles.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71b16-210">Pour pouvoir utiliser un **cadre englobant**, l’objet doit avoir les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="71b16-210">To be able to use a **bounding box**, the object must have the following components:</span></span>
>
> * <span data-ttu-id="71b16-211">Le composant **Collider**, par exemple un Box Collider</span><span class="sxs-lookup"><span data-stu-id="71b16-211">**Collider** component, for example, a Box Collider</span></span>
> * <span data-ttu-id="71b16-212">Le composant **Bounding Box (Script)**</span><span class="sxs-lookup"><span data-stu-id="71b16-212">**Bounding Box (Script)** component</span></span>

### <a name="1-add-the-bounding-box-script-component-to-the-earthcore-object"></a><span data-ttu-id="71b16-213">1. Ajouter le composant Bounding Box (Script) à l’objet EarthCore</span><span class="sxs-lookup"><span data-stu-id="71b16-213">1. Add the Bounding Box (Script) component to the EarthCore object</span></span>

<span data-ttu-id="71b16-214">Dans la fenêtre Inspector, sélectionnez l’objet **EarthCore** et ajoutez le composant **Bounding Box (Script)** à l’objet EarthCore :</span><span class="sxs-lookup"><span data-stu-id="71b16-214">In the Inspector window, select the **EarthCore** object and add the **Bounding Box (Script)** component to the EarthCore object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section5-step1-1.png)

> [!NOTE]
> <span data-ttu-id="71b16-216">La visualisation des cadres englobants est créée au moment de l’exécution et n’est donc pas visible avant l’entrée en mode Game.</span><span class="sxs-lookup"><span data-stu-id="71b16-216">The Bounding Box visualizations is created at run time and therefore not visible before you enter Game mode.</span></span>

### <a name="2-visualize-and-test-the-bounding-box-using-the-in-editor-simulation"></a><span data-ttu-id="71b16-217">2. Visualiser et tester le cadre englobant en utilisant la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="71b16-217">2. Visualize and test the bounding box using the in-editor simulation</span></span>

<span data-ttu-id="71b16-218">Appuyez sur le bouton Play pour entrer en mode Game.</span><span class="sxs-lookup"><span data-stu-id="71b16-218">Press the Play button to enter Game mode.</span></span> <span data-ttu-id="71b16-219">Appuyez ensuite sur la barre d’espace pour faire apparaître la main et utilisez la souris pour interagir avec le cadre englobant :</span><span class="sxs-lookup"><span data-stu-id="71b16-219">Then press and hold the spacebar to bring up the hand and use the mouse to interact with the bounding box:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section5-step2-1.png)

<span data-ttu-id="71b16-221">Pour plus d’informations sur le composant Bounding Box et ses propriétés associées, vous pouvez consulter le guide [Bounding Box](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="71b16-221">To learn more about the Bounding Box component and its associated properties, you can visit the [Bounding box](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="adding-touch-effects"></a><span data-ttu-id="71b16-222">Ajout d’effets tactiles</span><span class="sxs-lookup"><span data-stu-id="71b16-222">Adding touch effects</span></span>

<span data-ttu-id="71b16-223">Dans cet exemple, vous allez activer des événements à déclencher quand vous touchez un objet avec votre main.</span><span class="sxs-lookup"><span data-stu-id="71b16-223">In this example, you will enable events to be triggered when you touch an object with your hand.</span></span> <span data-ttu-id="71b16-224">Plus précisément, vous allez configurer l’objet Octa pour qu’il émette un son quand l’utilisateur le touche.</span><span class="sxs-lookup"><span data-stu-id="71b16-224">Specifically, you will configure the Octa object to play a sound effect when the user touches it.</span></span>

<span data-ttu-id="71b16-225">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="71b16-225">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="71b16-226">Ajouter un composant Audio Source à l’objet</span><span class="sxs-lookup"><span data-stu-id="71b16-226">Add an Audio Source component to the object</span></span>
2. <span data-ttu-id="71b16-227">Ajouter le composant Near Interaction Touchable (Script) à l’objet</span><span class="sxs-lookup"><span data-stu-id="71b16-227">Add the Near Interaction Touchable (Script) component to the object</span></span>
3. <span data-ttu-id="71b16-228">Ajouter le composant Hand Interaction Touch (Script) à l’objet</span><span class="sxs-lookup"><span data-stu-id="71b16-228">Add the Hand Interaction Touch (Script) component to the object</span></span>
4. <span data-ttu-id="71b16-229">Implémenter l’événement On Touch Started</span><span class="sxs-lookup"><span data-stu-id="71b16-229">Implement the On Touch Started event</span></span>
5. <span data-ttu-id="71b16-230">Tester l’interaction tactile en utilisant la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="71b16-230">Test the touch interaction using the in-editor simulation</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71b16-231">Pour pouvoir **déclencher des événements tactiles**, l’objet doit avoir les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="71b16-231">To be able to **trigger touch events**, the object must have the following components:</span></span>
>
> * <span data-ttu-id="71b16-232">Le composant **Collider**, de préférence un Box Collider</span><span class="sxs-lookup"><span data-stu-id="71b16-232">**Collider** component, preferably a Box Collider</span></span>
> * <span data-ttu-id="71b16-233">Le composant **Near Interaction Touchable (Script)**</span><span class="sxs-lookup"><span data-stu-id="71b16-233">**Near Interaction Touchable (Script)** component</span></span>
> * <span data-ttu-id="71b16-234">Le composant **Hand Interaction Touch (Script)**</span><span class="sxs-lookup"><span data-stu-id="71b16-234">**Hand Interaction Touch (Script)** component</span></span>

> [!NOTE]
> <span data-ttu-id="71b16-235">Le composant Hand Interaction Touch (Script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="71b16-235">The Hand Interaction Touch (Script) component is not part of MRTK.</span></span> <span data-ttu-id="71b16-236">Il a été importé avec les ressources de ce tutoriel et faisait partie à l’origine des exemples de Unity MixedReality Toolkit.</span><span class="sxs-lookup"><span data-stu-id="71b16-236">It was imported with this tutorial's assets and originally part of the MixedReality Toolkit Unity Examples.</span></span>

### <a name="1-add-an-audio-source-component-to-the-object"></a><span data-ttu-id="71b16-237">1. Ajouter un composant Audio Source à l’objet</span><span class="sxs-lookup"><span data-stu-id="71b16-237">1. Add an Audio Source component to the object</span></span>

<span data-ttu-id="71b16-238">Dans la fenêtre Hierarchy, sélectionnez l’objet **Octa**, ajoutez un composant **Audio Source** à l’objet Octa, puis définissez **Spatial Blend** sur 1 pour activer l’audio spatial :</span><span class="sxs-lookup"><span data-stu-id="71b16-238">In the Hierarchy window, select the **Octa** object, add an **Audio Source** component to the Octa object, and then change **Spatial Blend** to 1 to enable spatial audio:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step1-1.png)

### <a name="2-add-the-near-interaction-touchable-script-component-to-the-object"></a><span data-ttu-id="71b16-240">2. Ajouter le composant Near Interaction Touchable (Script) à l’objet</span><span class="sxs-lookup"><span data-stu-id="71b16-240">2. Add the Near Interaction Touchable (Script) component to the object</span></span>

<span data-ttu-id="71b16-241">Avec l’objet **Octa** sélectionné, ajoutez le composant **Near Interaction Touchable (Script)** à l’objet Octa, puis cliquez sur les boutons **Fix Bounds** et **Fix Center** pour mettre à jour les propriétés Center et Bounds de Near Interaction Touchable (Script) pour qu’elles correspondent au BoxCollider :</span><span class="sxs-lookup"><span data-stu-id="71b16-241">With the **Octa** object still selected, add the **Near Interaction Touchable (Script)** component to the Octa object, and then click the **Fix Bounds** and **Fix Center** buttons to update the Local Center and Bounds properties of the Near Interaction Touchable (Script) to match the BoxCollider:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step2-1.png)

### <a name="3-add-the-hand-interaction-touch-script-component-to-the-object"></a><span data-ttu-id="71b16-243">3. Ajouter le composant Hand Interaction Touch (Script) à l’objet</span><span class="sxs-lookup"><span data-stu-id="71b16-243">3. Add the Hand Interaction Touch (Script) component to the object</span></span>

<span data-ttu-id="71b16-244">Avec l’objet **Octa** sélectionné, ajoutez le composant **Hand Interaction Touch (Script)** à l’objet Octa :</span><span class="sxs-lookup"><span data-stu-id="71b16-244">With the **Octa** object still selected, add the **Hand Interaction Touch (Script)** component to the Octa object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step3-1.png)

### <a name="4-implement-the-on-touch-started-event"></a><span data-ttu-id="71b16-246">4. Implémenter l’événement On Touch Started</span><span class="sxs-lookup"><span data-stu-id="71b16-246">4. Implement the On Touch Started event</span></span>

<span data-ttu-id="71b16-247">Sur le composant **Hand Interaction Touch (Script)** , cliquez sur la petite icône **+** pour créer un événement **On Touch Started ()** .</span><span class="sxs-lookup"><span data-stu-id="71b16-247">On the **Hand Interaction Touch (Script)** component, click the small **+** icon to create a new **On Touch Started ()** event.</span></span> <span data-ttu-id="71b16-248">Configurez ensuite l’objet **Octa** pour recevoir l’événement et définissez **AudioSource.PlayOneShot** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="71b16-248">Then configure the **Octa** object to receive the event and define **AudioSource.PlayOneShot** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step4-1.png)

<span data-ttu-id="71b16-250">Accédez à **Assets** > **MixedRealityToolkit.SDK** > **StandardAssets** > **Audio** pour voir les clips audio fournis avec le MRTK, puis affectez un clip audio approprié au champ **Audio Clip**, par exemple le clip audio MRTK_Gem :</span><span class="sxs-lookup"><span data-stu-id="71b16-250">Navigate to **Assets** > **MixedRealityToolkit.SDK** > **StandardAssets** > **Audio** to see audio clips provided with the MRTK, and then assign a suitable audio clip to the **Audio Clip** field, for example, the MRTK_Gem audio clip:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step4-2.png)

> [!TIP]
> <span data-ttu-id="71b16-252">Pour un rappel de la façon d’implémenter des événements, vous pouvez vous référer aux instructions de [Gestes de suivi de la main et boutons d’interaction](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons).</span><span class="sxs-lookup"><span data-stu-id="71b16-252">For a reminder on how to implement events, you can refer to the [Hand tracking gestures and interactable buttons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) instructions.</span></span>

### <a name="5-test-the-touch-interaction-using-the-in-editor-simulation"></a><span data-ttu-id="71b16-253">5. Tester l’interaction tactile en utilisant la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="71b16-253">5. Test the touch interaction using the in-editor simulation</span></span>

<span data-ttu-id="71b16-254">Appuyez sur le bouton Play pour entrer en mode Game.</span><span class="sxs-lookup"><span data-stu-id="71b16-254">Press the Play button to enter Game mode.</span></span> <span data-ttu-id="71b16-255">Appuyez ensuite sur la barre d’espace et maintenez-la enfoncée pour faire apparaître la main, et utilisez la souris pour toucher l’objet Octa et déclencher l’effet sonore :</span><span class="sxs-lookup"><span data-stu-id="71b16-255">Then press and hold the spacebar to bring up the hand and use the mouse to touch the Octa object and trigger the sound effect:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step5-1.png)

> [!NOTE]
> <span data-ttu-id="71b16-257">Comme vous l’avez vu lors du test de l’interaction tactile et comme illustré dans l’image ci-dessus, la couleur de l’objet Octa a subi un effet de pulsations alors qu’il était touché.</span><span class="sxs-lookup"><span data-stu-id="71b16-257">As you saw when testing the touch interaction, and as shown in the image above, the Octa object color pulsated while it was touched.</span></span> <span data-ttu-id="71b16-258">Cet effet est codé en dur dans le composant Hand Interaction Touch (Script) et ne résulte pas de la configuration des événements que vous avez effectuée dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="71b16-258">This effect is hard coded into the Hand Interaction Touch (Script) component and not a result of the event configuration you completed in the steps above.</span></span>
>
> <span data-ttu-id="71b16-259">Si vous voulez désactiver cet effet, vous pouvez par exemple mettre en commentaire la ligne 32 « TargetRenderer = GetComponentInChildren<Renderer>(); », ce qui fait que le TargetRenderer reste null et que la couleur ne subit pas l’effet de pulsations.</span><span class="sxs-lookup"><span data-stu-id="71b16-259">If you want to disable this effect, you can, for example, comment out or line 32 'TargetRenderer = GetComponentInChildren<Renderer>();' which will result in the TargetRenderer remaining null and the color not pulsating.</span></span>

## <a name="congratulations"></a><span data-ttu-id="71b16-260">Félicitations</span><span class="sxs-lookup"><span data-stu-id="71b16-260">Congratulations</span></span>

<span data-ttu-id="71b16-261">Dans ce tutoriel, vous avez découvert comment organiser des objets 3D dans une collection de grille et comment manipuler ces objets (mise à l’échelle, rotation et déplacement) en utilisant l’interaction de près (en saisissant directement avec les mains suivies) et l’interaction de loin (en utilisant des rayons de pointage du regard ou des rayons de main).</span><span class="sxs-lookup"><span data-stu-id="71b16-261">In this tutorial, you learned how to organize 3D objects in a grid collection and how to manipulate these objects (scaling, rotating, and moving) using near interaction (directly grabbing with tracked hands) and far interaction (using gaze rays or hand rays).</span></span> <span data-ttu-id="71b16-262">Vous avez aussi découvert comment placer des cadres englobants autour des objets 3D, et comment utiliser et personnaliser les poignées sur les cadres englobants.</span><span class="sxs-lookup"><span data-stu-id="71b16-262">You also learned how to put bounding boxes around 3D objects, and learned how to use and customize the handles on the bounding boxes.</span></span> <span data-ttu-id="71b16-263">Enfin, vous avez découvert comment déclencher des événements quand l’utilisateur touche un objet.</span><span class="sxs-lookup"><span data-stu-id="71b16-263">Finally, you learned how to trigger events when touching an object.</span></span>

[<span data-ttu-id="71b16-264">Leçon suivante : 6. Exploration des options d’entrée avancées</span><span class="sxs-lookup"><span data-stu-id="71b16-264">Next Lesson: 6. Exploring advanced input options</span></span>](mrlearning-base-ch5.md)
