---
title: Tutoriels de démarrage - 4. Placement de contenu dynamique et utilisation de solveurs
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 2825f99f49eca6fd7277d02828bfe1bc3c23291a
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79031222"
---
# <a name="4-placing-dynamic-content-and-using-solvers"></a><span data-ttu-id="a26d6-105">4. Placement de contenu dynamique et utilisation de solveurs</span><span class="sxs-lookup"><span data-stu-id="a26d6-105">4. Placing dynamic content and using Solvers</span></span>
<!-- Consider renaming to 'Placing dynamic content using Solvers' -->

<span data-ttu-id="a26d6-106">Les hologrammes prennent vie dans HoloLens 2 quand ils suivent intuitivement l’utilisateur et sont placés dans l’environnement physique de manière à rendre l’interaction fluide et élégante.</span><span class="sxs-lookup"><span data-stu-id="a26d6-106">Holograms come to life in HoloLens 2 when they intuitively follow the user and are placed in the physical environment in a way that makes interaction seamless and elegant.</span></span> <span data-ttu-id="a26d6-107">Dans ce tutoriel, nous allons étudier différentes manières de placer dynamiquement des hologrammes à l’aide des outils de placement fournis dans le MRTK, appelés « solveurs », pour résoudre des scénarios de placement spatial complexes.</span><span class="sxs-lookup"><span data-stu-id="a26d6-107">In this tutorial, we explore ways to dynamically place holograms using the MRTK's available placement tools, known as Solvers, to solve complex spatial placement scenarios.</span></span> <span data-ttu-id="a26d6-108">Dans le MRTK, les solveurs sont un système de scripts et de comportements utilisés pour permettre aux éléments de l’interface utilisateur de suivre l’utilisateur (vous) ou d’autres objets de jeu dans la scène.</span><span class="sxs-lookup"><span data-stu-id="a26d6-108">In the MRTK, Solvers are a system of scripts and behaviors that are used to allow UI elements to follow you, the user, or other game objects in the scene.</span></span> <span data-ttu-id="a26d6-109">Ils servent également à accélérer l’alignement sur certaines positions, rendant votre application plus intuitive.</span><span class="sxs-lookup"><span data-stu-id="a26d6-109">They can also be used to snap to certain positions quickly, making your application more intuitive.</span></span>

## <a name="objectives"></a><span data-ttu-id="a26d6-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="a26d6-110">Objectives</span></span>

* <span data-ttu-id="a26d6-111">Introduire les solveurs du MRTK</span><span class="sxs-lookup"><span data-stu-id="a26d6-111">Introduce the MRTK's Solvers</span></span>
* <span data-ttu-id="a26d6-112">Utiliser des solveurs pour qu’une collection de boutons suive l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a26d6-112">Use Solvers to have a collection of buttons follow the user</span></span>
* <span data-ttu-id="a26d6-113">Utiliser des solveurs pour qu’un objet de jeu suive les mouvements captés des mains de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a26d6-113">Use Solvers to have a game object follow the user's tracked hands</span></span>

## <a name="location-of-solvers-in-the-mrtk"></a><span data-ttu-id="a26d6-114">Emplacement des solveurs dans le MRTK</span><span class="sxs-lookup"><span data-stu-id="a26d6-114">Location of Solvers in the MRTK</span></span>

 <span data-ttu-id="a26d6-115">Les solveurs du MRTK se trouvent dans le dossier du SDK MRTK.</span><span class="sxs-lookup"><span data-stu-id="a26d6-115">The MRTK's Solvers are located in the MRTK SDK folder.</span></span> <span data-ttu-id="a26d6-116">Pour voir les solveurs disponibles dans votre projet, dans la fenêtre Project, accédez à **Assets** > **MixedRealityToolkit.SDK** > **Features** > **Utilities** > **Solvers** :</span><span class="sxs-lookup"><span data-stu-id="a26d6-116">To see the available Solvers in your project, in the Project window, navigate to **Assets** > **MixedRealityToolkit.SDK** > **Features** > **Utilities** > **Solvers**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial3-section1-step1-1.png)

<span data-ttu-id="a26d6-118">Dans ce tutoriel, nous allons passer en revue l’implémentation des solveurs Orbital et Radial View.</span><span class="sxs-lookup"><span data-stu-id="a26d6-118">In this tutorial, we will review the implementation of the Orbital Solver and the Radial View Solver.</span></span> <span data-ttu-id="a26d6-119">Pour en savoir plus sur l’ensemble des solveurs disponibles dans le MRTK, consultez le [guide des solveurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="a26d6-119">To learn more about the full range of Solvers available in the MRTK, you can visit the the [Solvers](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="use-a-solver-to-follow-the-user"></a><span data-ttu-id="a26d6-120">Utiliser un solveur pour suivre l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a26d6-120">Use a Solver to follow the user</span></span>
<!-- Consider renaming to 'Use a Solver to have an object follow the user' -->

<span data-ttu-id="a26d6-121">Dans cette section, vous allez améliorer la collection de boutons que vous avez créée dans le didacticiel précédent afin qu’elle suive le regard de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a26d6-121">In this section, you will enhance the button collection you created in the previous tutorial so it follows the user's gaze direction.</span></span> <span data-ttu-id="a26d6-122">Vous allez également configurer le solveur pour que la collection de boutons :</span><span class="sxs-lookup"><span data-stu-id="a26d6-122">Additionally, you will also configure the Solver so the button collection is always:</span></span>

* <span data-ttu-id="a26d6-123">pivote parallèlement au sens de lecture de l’utilisateur, pour une lecture naturelle de gauche à droite ;</span><span class="sxs-lookup"><span data-stu-id="a26d6-123">Rotated parallel to the user's reading direction, for natural left to right reading</span></span>
* <span data-ttu-id="a26d6-124">soit positionnée légèrement sous la ligne horizontale du regard de l’utilisateur, de manière à ce qu’elle n’obstrue pas les autres objets que vous ajouterez par la suite dans ce tutoriel ;</span><span class="sxs-lookup"><span data-stu-id="a26d6-124">Positioned slightly below the user horizontal gaze direction, so it's not obstructing the other objects you will add later in this tutorial</span></span>
* <span data-ttu-id="a26d6-125">soit positionnée à environ un demi-bras de l’utilisateur, de manière à ce qu’il puisse appuyer facilement sur les boutons.</span><span class="sxs-lookup"><span data-stu-id="a26d6-125">Positioned approximately a half arm's-length from the user, so the buttons can easily be pressed</span></span>

<span data-ttu-id="a26d6-126">Pour ce faire, vous allez utiliser le solveur **Orbital** qui verrouille l’objet à une position et à un décalage spécifiés par rapport à l’objet référencé.</span><span class="sxs-lookup"><span data-stu-id="a26d6-126">For this, you will use the **Orbital Solver** which locks the object to a specified position and offset from the referenced object.</span></span>

### <a name="1-add-the-orbital-solver"></a><span data-ttu-id="a26d6-127">1. Ajouter le solveur Orbital</span><span class="sxs-lookup"><span data-stu-id="a26d6-127">1. Add the Orbital Solver</span></span>

<span data-ttu-id="a26d6-128">Dans la fenêtre Hierarchy, sélectionnez l’objet **ButtonCollection** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Orbital (Script)** à l’objet ButtonCollection :</span><span class="sxs-lookup"><span data-stu-id="a26d6-128">In the Hierarchy window, select the **ButtonCollection** object, then in the Inspector window, use the **Add Component** button to add the **Orbital (Script)** component to the ButtonCollection object.</span></span>

> [!NOTE]
> <span data-ttu-id="a26d6-129">Quand vous ajoutez un solveur, dans ce cas le composant Orbital (Script), le composant Solver Handler (Script) est automatiquement ajouté car le solveur en a besoin.</span><span class="sxs-lookup"><span data-stu-id="a26d6-129">When you add a Solver, in this case the Orbital (Script) component, the Solver Handler (Script) component is automatically added because it is required by the Solver.</span></span>

### <a name="2-configure-the-orbital-solver"></a><span data-ttu-id="a26d6-130">2. Configurer le solveur Orbital</span><span class="sxs-lookup"><span data-stu-id="a26d6-130">2. Configure the Orbital Solver</span></span>

<span data-ttu-id="a26d6-131">Configurez le composant **Solver Handler (Script)**  :</span><span class="sxs-lookup"><span data-stu-id="a26d6-131">Configure the **Solver Handler (Script)** component:</span></span>

* <span data-ttu-id="a26d6-132">Vérifiez que **Tracked Target Type** indique **Head**.</span><span class="sxs-lookup"><span data-stu-id="a26d6-132">Verify that **Tracked Target Type** is set to **Head**</span></span>

<span data-ttu-id="a26d6-133">Configurez le composant **Orbital (Script)**  :</span><span class="sxs-lookup"><span data-stu-id="a26d6-133">Configure the **Orbital (Script)** component:</span></span>

* <span data-ttu-id="a26d6-134">Vérifiez que **Orientation Type** indique **Follow Tracked Object**.</span><span class="sxs-lookup"><span data-stu-id="a26d6-134">Verify that **Orientation Type** is set to **Follow Tracked Object**</span></span>
* <span data-ttu-id="a26d6-135">Réinitialisez **Local Offset** avec les valeurs X = 0, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="a26d6-135">Reset **Local Offset** to X = 0, Y = 0, Z = 0</span></span>
* <span data-ttu-id="a26d6-136">Définissez **World Offset** avec les valeurs X = 0, Y = -0,4 et Z = 0,3.</span><span class="sxs-lookup"><span data-stu-id="a26d6-136">Change **World Offset** to X = 0, Y = -0.4, Z = 0.3</span></span>

![mrlearning-base](images/mrlearning-base/tutorial3-section2-step2-1.png)

### <a name="3-test-the-orbital-solver-using-the-in-editor-simulation"></a><span data-ttu-id="a26d6-138">3. Tester le solveur Orbital à l’aide de la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="a26d6-138">3. Test the Orbital Solver using the in-editor simulation</span></span>

<span data-ttu-id="a26d6-139">Appuyez sur le bouton de lecture pour passer en mode Game, puis appuyez sur le bouton droit de la souris et maintenez-le enfoncé pour faire pivoter la direction de votre regard. Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="a26d6-139">Press the Play button to enter Game mode and press and hold the right mouse button to rotate your gaze direction, and notice the following:</span></span>

* <span data-ttu-id="a26d6-140">Les valeurs Position du paramètre Transform de ButtonCollection sont maintenant pilotées par les paramètres du solveur.</span><span class="sxs-lookup"><span data-stu-id="a26d6-140">The ButtonCollection's Transform Position is now driven by the Solver settings</span></span>
* <span data-ttu-id="a26d6-141">La position de l’objet Cube, qui n’est pas affecté par le solveur, est inchangée.</span><span class="sxs-lookup"><span data-stu-id="a26d6-141">The Cube, which is not affected by the Solver, remains in the same position</span></span>

![mrlearning-base](images/mrlearning-base/tutorial3-section2-step3-1.png)

> [!TIP]
> <span data-ttu-id="a26d6-143">Si vous ne voyez pas le rayon de l’appareil photo dans votre fenêtre Scene, vérifiez que votre menu Gizmos est activé.</span><span class="sxs-lookup"><span data-stu-id="a26d6-143">If you don't see the camera ray in your Scene window, make sure your Gizmos menu is enabled.</span></span> <span data-ttu-id="a26d6-144">Pour en savoir plus sur le menu Gizmos et sur la façon dont vous pouvez l’utiliser pour optimiser votre vue Scene, consultez la page consacrée au <a href="https://docs.unity3d.com/Manual/GizmosMenu.html" target="_blank">menu Gizmos</a> dans la documentation Unity.</span><span class="sxs-lookup"><span data-stu-id="a26d6-144">To learn more about the Gizmos menu and how you can use it to optimize your scene view, you can visit Unity's <a href="https://docs.unity3d.com/Manual/GizmosMenu.html" target="_blank">Gizmos menu</a> documentation.</span></span>
>
> <span data-ttu-id="a26d6-145">Pour afficher côte à côte les fenêtres Scene et Game comme dans l’image ci-dessus, faites simplement glisser la fenêtre Game à droite de la fenêtre Scene.</span><span class="sxs-lookup"><span data-stu-id="a26d6-145">To display your Scene and Game window side by side as shown in the image above, simply drag the Game window to the right side of the Scene window.</span></span> <span data-ttu-id="a26d6-146">Pour en savoir plus, consultez la page consacrée à la <a href="https://docs.unity3d.com/Manual/CustomizingYourWorkspace.html" target="_blank">personnalisation de votre espace de travail</a> dans la documentation Unity.</span><span class="sxs-lookup"><span data-stu-id="a26d6-146">To learn more about customizing your workspace, you can visit Unity's <a href="https://docs.unity3d.com/Manual/CustomizingYourWorkspace.html" target="_blank">Customizing Your Workspace</a> documentation.</span></span>

## <a name="enabling-objects-to-follow-tracked-hands"></a><span data-ttu-id="a26d6-147">Faire en sorte que les objets suivent les mouvements captés des mains</span><span class="sxs-lookup"><span data-stu-id="a26d6-147">Enabling objects to follow tracked hands</span></span>

<span data-ttu-id="a26d6-148">Dans cette section, vous allez configurer l’objet Cube que vous avez créé dans le tutoriel précédent afin qu’il suive les mouvements captés des mains de l’utilisateur, en particulier le poignet droit.</span><span class="sxs-lookup"><span data-stu-id="a26d6-148">In this section, you will configure the Cube object you created in the previous tutorial so it follows the user's tracked hands, specifically the right hand wrist.</span></span> <span data-ttu-id="a26d6-149">Vous allez également configurer le solveur pour que l’objet Cube :</span><span class="sxs-lookup"><span data-stu-id="a26d6-149">Additionally, you will also configure the Solver so the cube:</span></span>

* <span data-ttu-id="a26d6-150">change son orientation en fonction de la rotation de la main de l’utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="a26d6-150">Changes it's orientation with the user's hand rotation</span></span>
* <span data-ttu-id="a26d6-151">soit positionné sur le poignet de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a26d6-151">Positioned on the user's wrist</span></span>

<span data-ttu-id="a26d6-152">Pour cela, vous allez utiliser le solveur **Radial View** qui maintient l’objet dans un cône de vue projeté par l’objet référencé.</span><span class="sxs-lookup"><span data-stu-id="a26d6-152">For this, you will use the **Radial View Solver** which keeps the object within a view cone cast by the referenced object.</span></span>

### <a name="1-add-the-radial-view-solver"></a><span data-ttu-id="a26d6-153">1. Ajouter le solveur Radial View</span><span class="sxs-lookup"><span data-stu-id="a26d6-153">1. Add the Radial View Solver</span></span>

<span data-ttu-id="a26d6-154">Dans la fenêtre Hierarchy, sélectionnez l’objet **Cube** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter l’objet Cube du composant **Radial View (Script)** .</span><span class="sxs-lookup"><span data-stu-id="a26d6-154">In the Hierarchy window, select the **Cube** object, then in the Inspector window, use the **Add Component** button to add the **Radial View (Script)** component Cube object.</span></span>

### <a name="2-configure-the-radial-view-solver"></a><span data-ttu-id="a26d6-155">2. Ajouter le solveur Radial View</span><span class="sxs-lookup"><span data-stu-id="a26d6-155">2. Configure the Radial View Solver</span></span>

<span data-ttu-id="a26d6-156">Configurez le composant **Solver Handler (Script)**  :</span><span class="sxs-lookup"><span data-stu-id="a26d6-156">Configure the **Solver Handler (Script)** component:</span></span>

* <span data-ttu-id="a26d6-157">En regard de **Tracked Target Type**, sélectionnez **Hand Joint**.</span><span class="sxs-lookup"><span data-stu-id="a26d6-157">Change **Tracked Target Type** to **Hand Joint**</span></span>
* <span data-ttu-id="a26d6-158">En regard de **Tracked Handness**, sélectionnez **Right**.</span><span class="sxs-lookup"><span data-stu-id="a26d6-158">Change **Tracked Handness** to **Right**</span></span>
* <span data-ttu-id="a26d6-159">En regard de **Tracked Hand Joint**, sélectionnez **Wrist**.</span><span class="sxs-lookup"><span data-stu-id="a26d6-159">Change **Tracked Hand Joint** to **Wrist**</span></span>

<span data-ttu-id="a26d6-160">Configurez le composant **Radial View (Script)**  :</span><span class="sxs-lookup"><span data-stu-id="a26d6-160">Configure the **Radial View (Script)** component:</span></span>

* <span data-ttu-id="a26d6-161">En regard de **Reference Direction**, sélectionnez **Object Oriented**, puis cochez la case **Orient To Reference Direction**.</span><span class="sxs-lookup"><span data-stu-id="a26d6-161">Change **Reference Direction** to **Object Oriented**, then check the **Orient To Reference Direction** checkbox</span></span>
* <span data-ttu-id="a26d6-162">Définissez **Min Distance** et **Max Distance** avec la valeur 0.</span><span class="sxs-lookup"><span data-stu-id="a26d6-162">Change **Min Distance** and **Max Distance** to 0</span></span>

![mrlearning-base](images/mrlearning-base/tutorial3-section3-step2-1.png)

### <a name="3-test-the-radial-view-solver-using-the-in-editor-simulation"></a><span data-ttu-id="a26d6-164">3. Tester le solveur Radial View à l’aide de la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="a26d6-164">3. Test the Radial View Solver using the in-editor simulation</span></span>

<span data-ttu-id="a26d6-165">Appuyez sur le bouton de lecture pour passer en mode Game, puis appuyez sur la barre d’espace et maintenez-la enfoncée pour faire apparaître la main.</span><span class="sxs-lookup"><span data-stu-id="a26d6-165">Press the Play button to enter Game mode and then press and hold the spacebar to bring up the hand.</span></span> <span data-ttu-id="a26d6-166">Déplacez le curseur de la souris pour déplacer la main, puis cliquez sur le bouton gauche de la souris et maintenez-le enfoncé pour faire pivoter la main :</span><span class="sxs-lookup"><span data-stu-id="a26d6-166">Move the mouse cursor around to move the hand, and click and hold the left mouse button to rotate the hand:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial3-section3-step3-1.png)

## <a name="congratulations"></a><span data-ttu-id="a26d6-168">Félicitations</span><span class="sxs-lookup"><span data-stu-id="a26d6-168">Congratulations</span></span>

<span data-ttu-id="a26d6-169">Dans ce tutoriel, vous avez appris à utiliser les solveurs du MRTK pour que l’interface utilisateur suive intuitivement l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a26d6-169">In this tutorial, you learned how to use the MRTK's solvers to have a UI intuitively follow the user.</span></span> <span data-ttu-id="a26d6-170">Vous avez également vu comment attacher un solveur à un objet (par exemple, un cube) pour suivre les mouvements captés des mains de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a26d6-170">You also learned how to attach a Solver to an object (i.e., cube) to follow the user's tracked hands.</span></span> <span data-ttu-id="a26d6-171">Pour en savoir plus sur ces solveurs et d’autres fournis avec le MRTK, consultez le [guide des solveurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="a26d6-171">To learn more about these and other solvers included with the MRTK,  you can visit the [Solvers](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

[<span data-ttu-id="a26d6-172">Tutoriel suivant : 5. Interaction avec les objets 3D</span><span class="sxs-lookup"><span data-stu-id="a26d6-172">Next Tutorial: 5. Interacting with 3D objects</span></span>](mrlearning-base-ch4.md)
