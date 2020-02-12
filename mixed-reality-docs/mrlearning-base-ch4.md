---
title: Didacticiels de mise en route-5. Interaction avec les objets 3D
description: ''
author: jessemcculloch
ms.author: jemccull
ms.date: 05/02/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: a1b26d56b4693ef23f2d77ba53e0961693489a3a
ms.sourcegitcommit: cc61f7ac08f9ac2f2f04e8525c3260ea073e04a7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/11/2020
ms.locfileid: "77130262"
---
# <a name="5-interacting-with-3d-objects"></a><span data-ttu-id="2c7e8-104">5. interaction avec les objets 3D</span><span class="sxs-lookup"><span data-stu-id="2c7e8-104">5. Interacting with 3D objects</span></span>

<span data-ttu-id="2c7e8-105">Dans ce didacticiel, vous allez découvrir le contenu 3D de base et l’expérience utilisateur, tels que l’Organisation des objets 3D dans le cadre d’une collection, des zones englobantes pour la manipulation de base, l’interaction proche et éloignée, et les gestes tactiles et de manipulation avec le suivi de la main.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-105">In this tutorial, you will learn about basic 3D content and user experience, such as organizing 3D objects as part of a collection, bounding boxes for basic manipulation, near and far interaction, and touch and grab gestures with hand tracking.</span></span>

## <a name="objectives"></a><span data-ttu-id="2c7e8-106">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2c7e8-106">Objectives</span></span>

* <span data-ttu-id="2c7e8-107">Créer un panneau d’objets 3D qui sera utilisé pour les autres objectifs de formation</span><span class="sxs-lookup"><span data-stu-id="2c7e8-107">Create a panel of 3D objects which will be used for the other learning objectives</span></span>
* <span data-ttu-id="2c7e8-108">Implémenter des cadres englobants</span><span class="sxs-lookup"><span data-stu-id="2c7e8-108">Implement bounding boxes</span></span>
* <span data-ttu-id="2c7e8-109">Configurer des objets 3D pour des manipulations de base telles que déplacer, faire pivoter et mettre à l’échelle</span><span class="sxs-lookup"><span data-stu-id="2c7e8-109">Configure 3D objects for basic manipulation such as move, rotate, and scale</span></span>
* <span data-ttu-id="2c7e8-110">Explorer l’interaction de près et de loin</span><span class="sxs-lookup"><span data-stu-id="2c7e8-110">Explore near and far interaction</span></span>
* <span data-ttu-id="2c7e8-111">En savoir plus sur les gestes supplémentaires de suivi de la main, tels que la manipulation et la saisie tactile</span><span class="sxs-lookup"><span data-stu-id="2c7e8-111">Learn about additional hand tracking gestures, such as grab and touch</span></span>

## <a name="importing-the-tutorial-assets"></a><span data-ttu-id="2c7e8-112">Importation des ressources du didacticiel</span><span class="sxs-lookup"><span data-stu-id="2c7e8-112">Importing the tutorial assets</span></span>

<span data-ttu-id="2c7e8-113">Téléchargez et importez le package personnalisé Unity :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-113">Download and import the Unity custom package:</span></span>

* [<span data-ttu-id="2c7e8-114">MRTK. HoloLens2. Unity. Tutorials. Assets. GettingStarted. 2.2.0.0. pour Unity</span><span class="sxs-lookup"><span data-stu-id="2c7e8-114">MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.2.0.0.unitypackage</span></span>](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.2.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.2.0.0.unitypackage)

<span data-ttu-id="2c7e8-115">Une fois que vous avez importé les ressources du didacticiel, votre fenêtre de projet doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-115">After you have imported the tutorial assets your Project window should look similar to this:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section1-step1-1.png)

> [!TIP]
> <span data-ttu-id="2c7e8-117">Pour obtenir un rappel sur l’importation d’un package personnalisé Unity, vous pouvez vous reporter aux instructions [importez les instructions de la réalité mixte](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit) .</span><span class="sxs-lookup"><span data-stu-id="2c7e8-117">For a reminder on how to import a Unity custom package, you can refer to the [Import the Mixed Reality Toolkit](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit) instructions.</span></span>

## <a name="decluttering-the-scene-view"></a><span data-ttu-id="2c7e8-118">Désencombrement de la vue scène</span><span class="sxs-lookup"><span data-stu-id="2c7e8-118">Decluttering the scene view</span></span>

<span data-ttu-id="2c7e8-119">Pour faciliter l’utilisation de votre scène, définissez la visibilité des **scènes** pour les objets cube et ButtonCollection sur désactivé en cliquant sur l’icône représentant un **œil** à gauche des objets.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-119">To make it easier to work with your scene, set the **scene visibility** for the Cube and ButtonCollection objects to off by clicking the **eye** icon to the left of the objects.</span></span> <span data-ttu-id="2c7e8-120">Cela masque l’objet dans la fenêtre de scène sans modifier sa visibilité dans le jeu :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-120">This hides the object in the Scene window without changing their in-game visibility:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section2-step1-1.png)

> [!TIP]
> <span data-ttu-id="2c7e8-122">Pour en savoir plus sur les contrôles de visibilité des scènes et sur la façon dont vous pouvez les utiliser pour optimiser l’affichage et le flux de travail de votre scène, vous pouvez consulter la documentation sur la <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">visibilité des scènes</a> d’Unity.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-122">To learn more about the Scene Visibility controls and how you can use them to optimize your scene view and workflow, you can visit Unity's <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">Scene Visibility</a> documentation.</span></span>

## <a name="organizing-3d-objects-in-a-collection"></a><span data-ttu-id="2c7e8-123">Organisation d’objets 3D dans une collection</span><span class="sxs-lookup"><span data-stu-id="2c7e8-123">Organizing 3D objects in a collection</span></span>

<span data-ttu-id="2c7e8-124">Dans cette section, vous allez créer un panneau d’objets 3D que vous allez utiliser pour explorer les différentes façons d’interagir avec les objets 3D dans les sections suivantes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-124">In this section, you will create a panel of 3D objects which you will use when exploring various ways of interacting with 3D objects in the following sections of this tutorial.</span></span> <span data-ttu-id="2c7e8-125">Plus précisément, vous configurez les objets 3D de manière à ce qu’ils soient positionnés sur une grille 3 x 3.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-125">Specifically, you will configure the 3D objects to be positioned on a 3 x 3 grid.</span></span>

<span data-ttu-id="2c7e8-126">De la même façon que lorsque vous avez [créé un panneau de boutons](mrlearning-base-ch2.md#creating-a-panel-of-buttons-using-mrtks-grid-object-collection), les principales étapes à suivre pour y parvenir sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-126">Similarly to when you [created a panel of buttons](mrlearning-base-ch2.md#creating-a-panel-of-buttons-using-mrtks-grid-object-collection), the main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="2c7e8-127">Parent des objets 3D à un objet parent</span><span class="sxs-lookup"><span data-stu-id="2c7e8-127">Parent the 3D objects to a parent object</span></span>
2. <span data-ttu-id="2c7e8-128">Ajouter et configurer le composant de collection d’objets Grid (script)</span><span class="sxs-lookup"><span data-stu-id="2c7e8-128">Add and configure the Grid Object Collection (Script) component</span></span>

### <a name="1-parent-the-3d-objects-to-a-parent-object"></a><span data-ttu-id="2c7e8-129">1. parent des objets 3D à un objet parent</span><span class="sxs-lookup"><span data-stu-id="2c7e8-129">1. Parent the 3D objects to a parent object</span></span>

<span data-ttu-id="2c7e8-130">Dans la fenêtre hiérarchie, **créez un objet vide**, donnez-lui un nom approprié, par exemple, **3DObjectCollection**, et positionnez-le à un emplacement approprié, par exemple, X = 0, Y =-0,2, Z = 2.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-130">In the Hierarchy window, **create an empty object**, give it a suitable name, for example, **3DObjectCollection**, and position it in a suitable location, for example, X = 0, Y = -0.2, Z = 2.</span></span>

<span data-ttu-id="2c7e8-131">Dans la fenêtre projet, accédez à **ressources** > **MRTK. Tutoriels. GettingStarted** > **Prefabs**, **puis le Prefabs suivant au** **3DObjectCollection**:</span><span class="sxs-lookup"><span data-stu-id="2c7e8-131">In the Project window, navigate to **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs**, then **Parent** the following prefabs to the **3DObjectCollection**:</span></span>

* <span data-ttu-id="2c7e8-132">Fromage</span><span class="sxs-lookup"><span data-stu-id="2c7e8-132">Cheese</span></span>
* <span data-ttu-id="2c7e8-133">CoffeeCup</span><span class="sxs-lookup"><span data-stu-id="2c7e8-133">CoffeeCup</span></span>
* <span data-ttu-id="2c7e8-134">EarthCore</span><span class="sxs-lookup"><span data-stu-id="2c7e8-134">EarthCore</span></span>
* <span data-ttu-id="2c7e8-135">Octa</span><span class="sxs-lookup"><span data-stu-id="2c7e8-135">Octa</span></span>
* <span data-ttu-id="2c7e8-136">Platoniques</span><span class="sxs-lookup"><span data-stu-id="2c7e8-136">Platonic</span></span>
* <span data-ttu-id="2c7e8-137">TheModule</span><span class="sxs-lookup"><span data-stu-id="2c7e8-137">TheModule</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-1.png)

<span data-ttu-id="2c7e8-139">Dans la fenêtre hiérarchie, **créez trois cubes** en tant qu’objets enfants du **3DObjectCollection** et définissez leur **échelle** de transformation sur X = 0,15, Y = 0,15, Z = 0,15 :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-139">In the Hierarchy window, **create three cubes** as a child objects of the **3DObjectCollection** and set their Transform **Scale** to X = 0.15, Y = 0.15, Z = 0.15:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-2.png)

<!-- TODO: Finish -->
> [!TIP]
> <span data-ttu-id="2c7e8-141">Pour obtenir un rappel sur la procédure à suivre pour effectuer les étapes décrites ci-dessus, vous pouvez consulter le didacticiel Création de l' [interface utilisateur et configuration de la réalité mixte](mrlearning-base-ch2.md) .</span><span class="sxs-lookup"><span data-stu-id="2c7e8-141">For a reminder on how to do the steps listed above, you can refer to the [Creating user interface and configure Mixed Reality Toolkit](mrlearning-base-ch2.md) tutorial.</span></span>

<span data-ttu-id="2c7e8-142">Repositionnez les cubes afin de voir chaque cube :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-142">Reposition the cubes so you can see each cube:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-3.png)

<span data-ttu-id="2c7e8-144">Dans la fenêtre projet, accédez à **ressources** > **MixedRealityToolkit. SDK** > **StandardAssets** > **matériaux** pour voir les matériaux fournis avec MRTK.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-144">In the Project window, navigate to **Assets** > **MixedRealityToolkit.SDK** > **StandardAssets** > **Materials** to see materials provided with the MRTK.</span></span>

<span data-ttu-id="2c7e8-145">**Cliquez et faites glisser** un matériau approprié sur la propriété de **l’élément 0** du convertisseur de maillage de chaque cube, par exemple :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-145">**Click-and-drag** a suitable material on to each cube's Mesh Renderer **Materials** Element 0 property, for example:</span></span>

* <span data-ttu-id="2c7e8-146">MRTK_Standard_GlowingCyan</span><span class="sxs-lookup"><span data-stu-id="2c7e8-146">MRTK_Standard_GlowingCyan</span></span>
* <span data-ttu-id="2c7e8-147">MRTK_Standard_GlowingOrange</span><span class="sxs-lookup"><span data-stu-id="2c7e8-147">MRTK_Standard_GlowingOrange</span></span>
* <span data-ttu-id="2c7e8-148">MRTK_Standard_Green :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-148">MRTK_Standard_Green:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-4.png)

### <a name="2-add-and-configure-the-grid-object-collection-script-component"></a><span data-ttu-id="2c7e8-150">2. Ajouter et configurer le composant collection d’objets Grid (script)</span><span class="sxs-lookup"><span data-stu-id="2c7e8-150">2. Add and configure the Grid Object Collection (Script) component</span></span>

<span data-ttu-id="2c7e8-151">Ajoutez un composant de **collection d’objets Grid (script)** à l’objet 3DObjectCollection et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-151">Add a **Grid Object Collection (Script)** component to the 3DObjectCollection object, and configure it as follows:</span></span>

* <span data-ttu-id="2c7e8-152">Changez le **type de tri** en ordre enfant pour vous assurer que les objets enfants sont triés dans l’ordre dans lequel vous les avez placés sous l’objet parent</span><span class="sxs-lookup"><span data-stu-id="2c7e8-152">Change **Sort Type** to Child Order to ensure the child objects are sorted in the order you have placed them under the parent object</span></span>

<span data-ttu-id="2c7e8-153">Cliquez ensuite sur le bouton **mettre à jour la collection** pour appliquer la nouvelle configuration :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-153">Then click the **Update Collection** button to apply the new configuration:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step2-1.png)

## <a name="manipulating-3d-objects"></a><span data-ttu-id="2c7e8-155">Manipulation d’objets 3D</span><span class="sxs-lookup"><span data-stu-id="2c7e8-155">Manipulating 3D objects</span></span>

<span data-ttu-id="2c7e8-156">Dans cette section, vous allez ajouter la possibilité de manipuler tous les objets 3D dans le panneau que vous avez créé dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-156">In this section, you will add the ability to manipulate all the 3D objects in the panel you created in the previous section.</span></span> <span data-ttu-id="2c7e8-157">En outre, pour les objets Prefab, vous permettez aux utilisateurs d’accéder à ces objets et de les saisir avec des mains suivies.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-157">Additionally, for the prefab objects, you will enable users to reach out and grab these objects with tracked hands.</span></span> <span data-ttu-id="2c7e8-158">Vous allez ensuite explorer quelques comportements de manipulation que vous pouvez appliquer à vos objets.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-158">Then you will explore a few manipulation behaviors that you can apply to your objects.</span></span>

<span data-ttu-id="2c7e8-159">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-159">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="2c7e8-160">Ajouter le composant de gestionnaire de manipulation (script) à tous les objets</span><span class="sxs-lookup"><span data-stu-id="2c7e8-160">Add the Manipulation Handler (Script) component to all the objects</span></span>
2. <span data-ttu-id="2c7e8-161">Ajouter le composant de script (script) à proximité des objets Prefab</span><span class="sxs-lookup"><span data-stu-id="2c7e8-161">Add the Near Interaction Grabbable (Script) component to the prefab objects</span></span>
3. <span data-ttu-id="2c7e8-162">Configurer le composant de gestionnaire de manipulation (script)</span><span class="sxs-lookup"><span data-stu-id="2c7e8-162">Configure the Manipulation Handler (Script) component</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c7e8-163">Pour pouvoir **manipuler un objet**, l’objet doit avoir les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-163">To be able to **manipulate an object**, the object must have the following components:</span></span>
>
> * <span data-ttu-id="2c7e8-164">Composant de **collision** , par exemple, un conflit de boîte</span><span class="sxs-lookup"><span data-stu-id="2c7e8-164">**Collider** component, for example, a Box Collider</span></span>
> * <span data-ttu-id="2c7e8-165">Composant du **Gestionnaire de manipulation (script)**</span><span class="sxs-lookup"><span data-stu-id="2c7e8-165">**Manipulation Handler (Script)** component</span></span>
>
> <span data-ttu-id="2c7e8-166">Pour pouvoir **manipuler** et **récupérer un objet avec des mains suivies**, l’objet doit avoir les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-166">To be able to **manipulate** and **grab an object with tracked hands**, the object must have the following components:</span></span>
>
> * <span data-ttu-id="2c7e8-167">Composant de **collision** , par exemple, un conflit de boîte</span><span class="sxs-lookup"><span data-stu-id="2c7e8-167">**Collider** component, for example, a Box Collider</span></span>
> * <span data-ttu-id="2c7e8-168">Composant du **Gestionnaire de manipulation (script)**</span><span class="sxs-lookup"><span data-stu-id="2c7e8-168">**Manipulation Handler (Script)** component</span></span>
> * <span data-ttu-id="2c7e8-169">Composant **de script (script) à proximité d’interaction**</span><span class="sxs-lookup"><span data-stu-id="2c7e8-169">**Near Interaction Grabbable (Script)** component</span></span>

### <a name="1-add-the-manipulation-handler-script-component-to-all-the-objects"></a><span data-ttu-id="2c7e8-170">1. ajouter le composant de gestionnaire de manipulation (script) à tous les objets</span><span class="sxs-lookup"><span data-stu-id="2c7e8-170">1. Add the Manipulation Handler (Script) component to all the objects</span></span>

<span data-ttu-id="2c7e8-171">Dans la fenêtre hiérarchie, sélectionnez l’objet **fromage** , maintenez la touche **MAJ** enfoncée, puis sélectionnez l’objet **cube ()** et ajoutez le composant **Gestionnaire de manipulation (script)** à tous les objets :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-171">In the Hierarchy window, select the **Cheese** object, hold down the **Shift** key, and then select the **Cube ()** object and add the **Manipulation Handler (Script)** component to all the objects:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step1-1.png)

> [!NOTE]
> <span data-ttu-id="2c7e8-173">Dans le cadre de ce didacticiel, les conflits ont déjà été ajoutés à prefabs.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-173">For the purpose of this tutorial, colliders have already been added to the prefabs.</span></span> <span data-ttu-id="2c7e8-174">Pour les primitives Unity, telles que les objets cube, le composant de conflit est automatiquement ajouté lors de la création de l’objet.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-174">For Unity primitives, such as the Cube objects, the Collider component is automatically added when the object is created.</span></span> <span data-ttu-id="2c7e8-175">Dans l’image ci-dessus, les conflits sont représentés par les contours verts.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-175">In the image above, the colliders are represented by the green outlines.</span></span> <span data-ttu-id="2c7e8-176">Pour en savoir plus sur les conflits, vous pouvez consulter la documentation sur les <a href="https://docs.unity3d.com/Manual/CollidersOverview.html" target="_blank">conflits</a> d’Unity.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-176">To learn more about colliders, you can visit Unity's <a href="https://docs.unity3d.com/Manual/CollidersOverview.html" target="_blank">Collider</a> documentation.</span></span>

### <a name="2-add-the-near-interaction-grabbable-script-component-to-the-prefab-objects"></a><span data-ttu-id="2c7e8-177">2. ajouter le composant de script (script) à proximité des objets Prefab</span><span class="sxs-lookup"><span data-stu-id="2c7e8-177">2. Add the Near Interaction Grabbable (Script) component to the prefab objects</span></span>

<span data-ttu-id="2c7e8-178">Dans la fenêtre hiérarchie, sélectionnez l’objet **fromage** , maintenez la touche **MAJ** enfoncée, puis sélectionnez l’objet **TheModule** et ajoutez le composant de script à **proximité d’interaction** à tous les objets :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-178">In the Hierarchy window, select the **Cheese** object, hold down the **Shift** key, and then select the **TheModule** object and add the **Near Interaction Grabbable (Script)** component to all the objects:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step2-1.png)

### <a name="3-configure-the-manipulation-handler-script-component"></a><span data-ttu-id="2c7e8-180">3. configurer le composant Gestionnaire de manipulation (script)</span><span class="sxs-lookup"><span data-stu-id="2c7e8-180">3. Configure the Manipulation Handler (Script) component</span></span>

#### <a name="default-manipulation"></a><span data-ttu-id="2c7e8-181">Manipulation par défaut</span><span class="sxs-lookup"><span data-stu-id="2c7e8-181">Default manipulation</span></span>

<span data-ttu-id="2c7e8-182">Pour l’objet **cube** , laissez toutes les propriétés par défaut pour connaître le comportement de manipulation par défaut :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-182">For the **Cube** object, leave all properties at default, to experience the default manipulation behavior:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-1.png)

> [!TIP]
> <span data-ttu-id="2c7e8-184">Pour rétablir les valeurs par défaut d’un composant, vous pouvez sélectionner l’icône des paramètres du composant, puis sélectionner réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-184">To reset a component to its default values, you can select the component's Settings icon and select Reset.</span></span>

#### <a name="restrict-manipulation-to-scale-only"></a><span data-ttu-id="2c7e8-185">Limiter la manipulation à l’échelle uniquement</span><span class="sxs-lookup"><span data-stu-id="2c7e8-185">Restrict manipulation to scale only</span></span>

<span data-ttu-id="2c7e8-186">Pour l’objet **cube (1)** , modifiez **deux types de manipulations de type droitier** pour que l’utilisateur n’autorise que la modification de la taille de l’objet :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-186">For the **Cube (1)** object, change **Two Handed Manipulation Type** to Scale to only allow the user to change the object's size:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-2.png)

#### <a name="constrain-the-movement-to-a-fixed-distance-from-the-user"></a><span data-ttu-id="2c7e8-188">Contraindre le mouvement à une distance fixe de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2c7e8-188">Constrain the movement to a fixed distance from the user</span></span>

<span data-ttu-id="2c7e8-189">Pour l’objet **cube (2)** , modifiez la **contrainte de déplacement** pour corriger distance à partir de Head afin que, lorsque l’objet est déplacé, il reste à la même distance de l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-189">For the **Cube (2)** object, change **Constraint On Movement** to Fix Distance From Head so that when the object is moved, it stays at the same distance from the user:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-3.png)

#### <a name="default-grabbable-manipulation"></a><span data-ttu-id="2c7e8-191">Manipulation par défaut de l’option d’accrochage</span><span class="sxs-lookup"><span data-stu-id="2c7e8-191">Default grabbable manipulation</span></span>

<span data-ttu-id="2c7e8-192">Pour les objets **fromage**, **CoffeCup**et **EarthCore** , laissez toutes les propriétés par défaut pour connaître le comportement de manipulation par défaut :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-192">For the **Cheese**, **CoffeCup**, and **EarthCore** objects, leave all properties at default, to experience the default grabbable manipulation behavior:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-4.png)

#### <a name="remove-the-ability-of-far-manipulation"></a><span data-ttu-id="2c7e8-194">Supprimer la capacité de manipulation lointaine</span><span class="sxs-lookup"><span data-stu-id="2c7e8-194">Remove the ability of far manipulation</span></span>

<span data-ttu-id="2c7e8-195">Pour l’objet **octa** , désactivez la case à cocher **autoriser la manipulation lointaine** pour que l’utilisateur puisse interagir uniquement avec l’objet directement à l’aide des mains suivies :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-195">For the **Octa** object, uncheck the **Allow Far Manipulation** checkbox to make it so the user can only interact with the object directly using tracked hands:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-5.png)

#### <a name="make-an-object-rotate-around-its-center"></a><span data-ttu-id="2c7e8-197">Faire pivoter un objet autour de son centre</span><span class="sxs-lookup"><span data-stu-id="2c7e8-197">Make an object rotate around its center</span></span>

<span data-ttu-id="2c7e8-198">Pour l’objet **platoniques** , modifiez le **mode de rotation d’un côté** vers le bas et le mode de rotation d' **un seul** côté pour faire pivoter le centre d’objets pour le faire ainsi lorsque l’utilisateur fait pivoter l’objet d’une main, il pivote autour du centre de l’objet :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-198">For the **Platonic** object, change **One Hand Rotation Mode Near** and **One Hand Rotation Mode Far** to Rotate About Object Center to make it so when the user rotates the object with one hand, it rotates around the object's center:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-6.png)

#### <a name="prevent-movement-after-object-is-released"></a><span data-ttu-id="2c7e8-200">Empêcher le déplacement après la libération de l’objet</span><span class="sxs-lookup"><span data-stu-id="2c7e8-200">Prevent movement after object is released</span></span>

<span data-ttu-id="2c7e8-201">Pour l’objet **TheModule** , remplacez le **comportement Release** par Nothing afin qu’une fois que l’objet est libéré de la main de l’utilisateur, il ne continue pas à se déplacer :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-201">For the **TheModule** object, change **Release Behavior** to Nothing so that once the object is released from the user's hand, it doesn’t continue to move:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-7.png)

<span data-ttu-id="2c7e8-203">Pour en savoir plus sur le composant de gestionnaire de manipulation et ses propriétés associées, vous pouvez consulter le Guide du [Gestionnaire de manipulation](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html) dans le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="2c7e8-203">To learn more about the Manipulation handler component and its associated properties, you can visit the [Manipulation handler](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="adding-bounding-boxes"></a><span data-ttu-id="2c7e8-204">Ajouter des zones englobantes</span><span class="sxs-lookup"><span data-stu-id="2c7e8-204">Adding bounding boxes</span></span>

<span data-ttu-id="2c7e8-205">Les rectangles englobants facilitent et simplifient la manipulation d’objets avec une main pour une interaction proche et éloignée en fournissant des poignées qui peuvent être utilisées pour la mise à l’échelle et la rotation.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-205">Bounding boxes make it easier and more intuitive to manipulate objects with one hand for both near and far interaction by providing handles that can be used for scaling and rotating.</span></span>

<span data-ttu-id="2c7e8-206">Dans cet exemple, vous allez ajouter un cadre englobant à l’objet EarthCore pour que cet objet puisse être manipulé avec l’utilisation de la manipulation d’objets que vous avez configurée dans la section précédente, ainsi que pour la mise à l’échelle et la rotation à l’aide des poignées de cadre englobant.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-206">In this example, you will add a bounding box to the EarthCore object so this object can now be interacted with using the object manipulation you configured in the previous section, as well as, scaled and rotated using the bounding box handles.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c7e8-207">Pour pouvoir utiliser un **cadre englobant**, l’objet doit avoir les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-207">To be able to use a **bounding box**, the object must have the following components:</span></span>
>
> * <span data-ttu-id="2c7e8-208">Composant de **collision** , par exemple, un conflit de boîte</span><span class="sxs-lookup"><span data-stu-id="2c7e8-208">**Collider** component, for example, a Box Collider</span></span>
> * <span data-ttu-id="2c7e8-209">Composant **de cadre englobant (script)**</span><span class="sxs-lookup"><span data-stu-id="2c7e8-209">**Bounding Box (Script)** component</span></span>

### <a name="1-add-the-bounding-box-script-component-to-the-earthcore-object"></a><span data-ttu-id="2c7e8-210">1. ajouter le composant de cadre englobant (script) à l’objet EarthCore</span><span class="sxs-lookup"><span data-stu-id="2c7e8-210">1. Add the Bounding Box (Script) component to the EarthCore object</span></span>

<span data-ttu-id="2c7e8-211">Dans la fenêtre de l’inspecteur, sélectionnez l’objet **EarthCore** et ajoutez le composant de cadre **englobant (script)** à l’objet EarthCore :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-211">In the Inspector window, select the **EarthCore** object and add the **Bounding Box (Script)** component to the EarthCore object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section5-step1-1.png)

> [!NOTE]
> <span data-ttu-id="2c7e8-213">Les visualisations de cadre englobant sont créées au moment de l’exécution et ne sont donc pas visibles avant l’entrée en mode jeu.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-213">The Bounding Box visualizations is created at run time and therefore not visible before you enter Game mode.</span></span>

### <a name="2-visualize-and-test-the-bounding-box-using-the-in-editor-simulation"></a><span data-ttu-id="2c7e8-214">2. Visualisez et testez le cadre englobant à l’aide de la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="2c7e8-214">2. Visualize and test the bounding box using the in-editor simulation</span></span>

<span data-ttu-id="2c7e8-215">Appuyez sur le bouton lecture pour passer en mode jeu.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-215">Press the Play button to enter Game mode.</span></span> <span data-ttu-id="2c7e8-216">Appuyez sur la barre d’espace et maintenez-la enfoncée pour afficher la main et utilisez la souris pour interagir avec le cadre englobant :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-216">Then press and hold the spacebar to bring up the hand and use the mouse to interact with the bounding box:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section5-step2-1.png)

<span data-ttu-id="2c7e8-218">Pour en savoir plus sur le composant de cadre englobant et ses propriétés associées, vous pouvez consulter le Guide du cadre [englobant](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) dans le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="2c7e8-218">To learn more about the Bounding Box component and its associated properties, you can visit the [Bounding box](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="adding-touch-effects"></a><span data-ttu-id="2c7e8-219">Ajout d’effets tactiles</span><span class="sxs-lookup"><span data-stu-id="2c7e8-219">Adding touch effects</span></span>

<span data-ttu-id="2c7e8-220">Dans cet exemple, vous allez activer les événements à déclencher lorsque vous touchez un objet à votre main.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-220">In this example, you will enable events to be triggered when you touch an object with your hand.</span></span> <span data-ttu-id="2c7e8-221">Plus précisément, vous allez configurer l’objet octa pour qu’il émette un effet sonore lorsque l’utilisateur le touche.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-221">Specifically, you will configure the Octa object to play a sound effect when the user touches it.</span></span>

<span data-ttu-id="2c7e8-222">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-222">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="2c7e8-223">Ajouter un composant source audio à l’objet</span><span class="sxs-lookup"><span data-stu-id="2c7e8-223">Add an Audio Source component to the object</span></span>
2. <span data-ttu-id="2c7e8-224">Ajouter le composant touchable (script) near interaction à l’objet</span><span class="sxs-lookup"><span data-stu-id="2c7e8-224">Add the Near Interaction Touchable (Script) component to the object</span></span>
3. <span data-ttu-id="2c7e8-225">Ajouter le composant tactile d’interaction manuelle (script) à l’objet</span><span class="sxs-lookup"><span data-stu-id="2c7e8-225">Add the Hand Interaction Touch (Script) component to the object</span></span>
4. <span data-ttu-id="2c7e8-226">Implémenter l’événement on Touch Started</span><span class="sxs-lookup"><span data-stu-id="2c7e8-226">Implement the On Touch Started event</span></span>
5. <span data-ttu-id="2c7e8-227">Tester l’interaction tactile à l’aide de la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="2c7e8-227">Test the touch interaction using the in-editor simulation</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c7e8-228">Pour pouvoir déclencher des **événements tactiles**, l’objet doit avoir les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-228">To be able to **trigger touch events**, the object must have the following components:</span></span>
>
> * <span data-ttu-id="2c7e8-229">Composant de **collision** , de préférence un conflit de Box</span><span class="sxs-lookup"><span data-stu-id="2c7e8-229">**Collider** component, preferably a Box Collider</span></span>
> * <span data-ttu-id="2c7e8-230">Composant **touchable (script) near interaction**</span><span class="sxs-lookup"><span data-stu-id="2c7e8-230">**Near Interaction Touchable (Script)** component</span></span>
> * <span data-ttu-id="2c7e8-231">Composant **Touch interaction tactile (script)**</span><span class="sxs-lookup"><span data-stu-id="2c7e8-231">**Hand Interaction Touch (Script)** component</span></span>

> [!NOTE]
> <span data-ttu-id="2c7e8-232">Le composant Touch interaction tactile (script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-232">The Hand Interaction Touch (Script) component is not part of MRTK.</span></span> <span data-ttu-id="2c7e8-233">Il a été importé avec les ressources de ce didacticiel et faisait partie à l’origine des exemples d’Unity MixedReality Toolkit.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-233">It was imported with this tutorial's assets and originally part of the MixedReality Toolkit Unity Examples.</span></span>

### <a name="1-add-an-audio-source-component-to-the-object"></a><span data-ttu-id="2c7e8-234">1. Ajouter un composant audio source à l’objet</span><span class="sxs-lookup"><span data-stu-id="2c7e8-234">1. Add an Audio Source component to the object</span></span>

<span data-ttu-id="2c7e8-235">Dans la fenêtre hiérarchie, sélectionnez l’objet **octa** , ajoutez un composant **audio source** à l’objet octa, puis remplacez **spatial Blend** par 1 pour activer l’audio spatial :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-235">In the Hierarchy window, select the **Octa** object, add an **Audio Source** component to the Octa object, and then change **Spatial Blend** to 1 to enable spatial audio:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step1-1.png)

### <a name="2-add-the-near-interaction-touchable-script-component-to-the-object"></a><span data-ttu-id="2c7e8-237">2. ajouter le composant touchable (script) near-interaction à l’objet</span><span class="sxs-lookup"><span data-stu-id="2c7e8-237">2. Add the Near Interaction Touchable (Script) component to the object</span></span>

<span data-ttu-id="2c7e8-238">L’objet **octa** étant toujours sélectionné, ajoutez le composant **touchable (script) near-interaction** à l’objet octa, puis cliquez sur les boutons **corriger les limites** et le centre de **Correction** pour mettre à jour les propriétés du centre local et des limites du touchable d’interaction Near (script) pour qu’elles correspondent à la BoxCollider :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-238">With the **Octa** object still selected, add the **Near Interaction Touchable (Script)** component to the Octa object, and then click the **Fix Bounds** and **Fix Center** buttons to update the Local Center and Bounds properties of the Near Interaction Touchable (Script) to match the BoxCollider:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step2-1.png)

### <a name="3-add-the-hand-interaction-touch-script-component-to-the-object"></a><span data-ttu-id="2c7e8-240">3. ajouter le composant tactile d’interaction manuelle (script) à l’objet</span><span class="sxs-lookup"><span data-stu-id="2c7e8-240">3. Add the Hand Interaction Touch (Script) component to the object</span></span>

<span data-ttu-id="2c7e8-241">Avec l’objet **octa** toujours sélectionné, ajoutez le composant **Touch interaction tactile (script)** à l’objet octa :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-241">With the **Octa** object still selected, add the **Hand Interaction Touch (Script)** component to the Octa object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step3-1.png)

### <a name="4-implement-the-on-touch-started-event"></a><span data-ttu-id="2c7e8-243">4. implémenter l’événement on Touch Started</span><span class="sxs-lookup"><span data-stu-id="2c7e8-243">4. Implement the On Touch Started event</span></span>

<span data-ttu-id="2c7e8-244">Sur le composant Touch interaction tactile (script), cliquez sur l’icône de petite **+** pour créer un événement **on Touch Started ()** .</span><span class="sxs-lookup"><span data-stu-id="2c7e8-244">On the Hand Interaction Touch (Script) component, click the small **+** icon to create a new **On Touch Started ()** event.</span></span> <span data-ttu-id="2c7e8-245">Configurez ensuite l’objet **octa** pour recevoir l’événement et définissez **audiosource. PlayOneShot** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-245">Then configure the **Octa** object to receive the event and define **AudioSource.PlayOneShot** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step4-1.png)

<span data-ttu-id="2c7e8-247">Accédez à **ressources** > **MixedRealityToolkit. SDK** > **StandardAssets** > matériaux pour voir les clips audio fournis avec le MRTK, puis attribuez un clip audio approprié au champ de **clip audio** , par exemple, le clip audio MRTK_Gem :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-247">Navigate to **Assets** > **MixedRealityToolkit.SDK** > **StandardAssets** > Materials to see audio clips provided with the MRTK, and then assign a suitable audio clip to the **Audio Clip** field, for example, the MRTK_Gem audio clip:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step4-2.png)

> [!TIP]
> <span data-ttu-id="2c7e8-249">Pour obtenir un rappel sur la façon d’implémenter des événements, vous pouvez consulter les instructions de suivi de la [main et les boutons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) interactifs.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-249">For a reminder on how to implement events, you can refer to the [Hand tracking gestures and interactable buttons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) instructions.</span></span>

### <a name="5-test-the-touch-interaction-using-the-in-editor-simulation"></a><span data-ttu-id="2c7e8-250">5. test de l’interaction tactile à l’aide de la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="2c7e8-250">5. Test the touch interaction using the in-editor simulation</span></span>

<span data-ttu-id="2c7e8-251">Appuyez sur le bouton lecture pour passer en mode jeu.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-251">Press the Play button to enter Game mode.</span></span> <span data-ttu-id="2c7e8-252">Appuyez sur la barre d’espace et maintenez-la enfoncée pour afficher la main et utilisez la souris pour toucher l’objet octa et déclencher l’effet sonore :</span><span class="sxs-lookup"><span data-stu-id="2c7e8-252">Then press and hold the spacebar to bring up the hand and use the mouse to touch the Octa object and trigger the sound effect:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step5-1.png)

> [!NOTE]
> <span data-ttu-id="2c7e8-254">Comme vous l’avez vu lors du test de l’interaction tactile, et comme indiqué dans l’image ci-dessus, l’objet octa Color pulsated alors qu’il a été touché.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-254">As you saw when testing the touch interaction, and as shown in the image above, the Octa object color pulsated while it was touched.</span></span> <span data-ttu-id="2c7e8-255">Cet effet est codé en dur dans le composant Touch interaction tactile (script) et non pas dans la configuration d’événement que vous avez effectuée dans les étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-255">This effect is hard coded into the Hand Interaction Touch (Script) component and not a result of the event configuration you completed in the steps above.</span></span>
>
> <span data-ttu-id="2c7e8-256">Si vous souhaitez désactiver cet effet, vous pouvez, par exemple, mettre en commentaire ou ligne 32 « TargetRenderer = GetComponentInChildren<Renderer>(); », ce qui a pour effet que le TargetRenderer reste null et que la couleur n’est pas Pulsating.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-256">If you want to disable this effect, you can, for example, comment out or line 32 'TargetRenderer = GetComponentInChildren<Renderer>();' which will result in the TargetRenderer remaining null and the color not pulsating.</span></span>

## <a name="congratulations"></a><span data-ttu-id="2c7e8-257">Félicitations</span><span class="sxs-lookup"><span data-stu-id="2c7e8-257">Congratulations</span></span>

<span data-ttu-id="2c7e8-258">Dans ce didacticiel, vous avez appris à organiser les objets 3D dans une collection de grilles et à manipuler ces objets (mise à l’échelle, rotation et déplacement) à l’aide de Near interaction (saisie directe des mains) et de l’interaction lointaine (à l’aide de rayons ou de rayons main).</span><span class="sxs-lookup"><span data-stu-id="2c7e8-258">In this tutorial, you learned how to organize 3D objects in a grid collection and how to manipulate these objects (scaling, rotating, and moving) using near interaction (directly grabbing with tracked hands) and far interaction (using gaze rays or hand rays).</span></span> <span data-ttu-id="2c7e8-259">Vous avez également appris à placer des zones englobantes autour des objets 3D et appris à utiliser et à personnaliser les poignées sur les zones englobantes.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-259">You also learned how to put bounding boxes around 3D objects, and learned how to use and customize the handles on the bounding boxes.</span></span> <span data-ttu-id="2c7e8-260">Enfin, vous avez découvert comment déclencher des événements quand l’utilisateur touche un objet.</span><span class="sxs-lookup"><span data-stu-id="2c7e8-260">Finally, you learned how to trigger events when touching an object.</span></span>

[<span data-ttu-id="2c7e8-261">Leçon suivante : 6. exploration des options d’entrée avancées</span><span class="sxs-lookup"><span data-stu-id="2c7e8-261">Next Lesson: 6. Exploring advanced input options</span></span>](mrlearning-base-ch5.md)
