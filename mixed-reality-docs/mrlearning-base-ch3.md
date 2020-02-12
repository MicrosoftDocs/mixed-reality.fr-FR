---
title: Didacticiels de mise en route-4. Placement de contenu dynamique et utilisation de solveurs
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 8275d5a97d7827d34ed3926cabe4032cc7f4cfac
ms.sourcegitcommit: cc61f7ac08f9ac2f2f04e8525c3260ea073e04a7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/11/2020
ms.locfileid: "77129315"
---
# <a name="4-placing-dynamic-content-and-using-solvers"></a><span data-ttu-id="ef5ae-105">4. placement de contenu dynamique et utilisation de solveurs</span><span class="sxs-lookup"><span data-stu-id="ef5ae-105">4. Placing dynamic content and using Solvers</span></span>
<!-- Consider renaming to 'Placing dynamic content using Solvers' -->

<span data-ttu-id="ef5ae-106">Les hologrammes arrivent à la vie dans HoloLens 2 lorsqu’ils suivent intuitivement l’utilisateur et sont placés dans l’environnement physique d’une manière qui rend l’interaction transparente et élégante.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-106">Holograms come to life in HoloLens 2 when they intuitively follow the user and are placed in the physical environment in a way that makes interaction seamless and elegant.</span></span> <span data-ttu-id="ef5ae-107">Dans ce didacticiel, nous explorons les façons de placer dynamiquement des hologrammes à l’aide des outils de positionnement disponibles de MRTK, appelés résolveurs, pour résoudre des scénarios de placement spatial complexes.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-107">In this tutorial, we explore ways to dynamically place holograms using the MRTK’s available placement tools, known as Solvers, to solve complex spatial placement scenarios.</span></span> <span data-ttu-id="ef5ae-108">Dans le MRTK, les solveurs sont un système de scripts et de comportements utilisés pour permettre aux éléments de l’interface utilisateur de suivre, de l’utilisateur ou d’autres objets de jeu dans la scène.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-108">In the MRTK, Solvers are a system of scripts and behaviors that are used to allow UI elements to follow you, the user, or other game objects in the scene.</span></span> <span data-ttu-id="ef5ae-109">Ils servent également à accélérer l’alignement sur certaines positions, rendant votre application plus intuitive.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-109">They can also be used to snap to certain positions quickly, making your application more intuitive.</span></span>

## <a name="objectives"></a><span data-ttu-id="ef5ae-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="ef5ae-110">Objectives</span></span>

* <span data-ttu-id="ef5ae-111">Introduire les solveurs de MRTK</span><span class="sxs-lookup"><span data-stu-id="ef5ae-111">Introduce the MRTK's Solvers</span></span>
* <span data-ttu-id="ef5ae-112">Utiliser des solveurs pour avoir une collection de boutons à la suite de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ef5ae-112">Use Solvers to have a collection of buttons follow the user</span></span>
* <span data-ttu-id="ef5ae-113">Utilisez les solveurs pour avoir un objet de jeu à la suite des mains suivies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ef5ae-113">Use Solvers to have a game object follow the user's tracked hands</span></span>

## <a name="location-of-solvers-in-the-mrtk"></a><span data-ttu-id="ef5ae-114">Emplacement des solveurs dans le MRTK</span><span class="sxs-lookup"><span data-stu-id="ef5ae-114">Location of Solvers in the MRTK</span></span>

 <span data-ttu-id="ef5ae-115">Les solveurs de MRTK se trouvent dans le dossier du kit de développement logiciel (SDK) MRTK.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-115">The MRTK's Solvers are located in the MRTK SDK folder.</span></span> <span data-ttu-id="ef5ae-116">Pour afficher les solveurs disponibles dans votre projet, dans la fenêtre projet, accédez à **ressources** > **MixedRealityToolkit. SDK** > **fonctionnalités** > **utilitaires** > **solveurs**:</span><span class="sxs-lookup"><span data-stu-id="ef5ae-116">To see the available Solvers in your project, in the Project window, navigate to **Assets** > **MixedRealityToolkit.SDK** > **Features** > **Utilities** > **Solvers**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial3-section1-step1-1.png)

<span data-ttu-id="ef5ae-118">Dans ce didacticiel, nous allons examiner l’implémentation du solveur orbital et du solveur de la vue radiale.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-118">In this tutorial, we will review the implementation of the Orbital Solver and the Radial View Solver.</span></span> <span data-ttu-id="ef5ae-119">Pour en savoir plus sur l’ensemble des programmes de résolution disponibles dans le MRTK, vous pouvez consulter le guide des [solveurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) dans le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="ef5ae-119">To learn more about the full range of Solvers available in the MRTK, you can visit the the [Solvers](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="use-a-solver-to-follow-the-user"></a><span data-ttu-id="ef5ae-120">Utiliser un solveur pour suivre l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ef5ae-120">Use a Solver to follow the user</span></span>
<!-- Consider renaming to 'Use a Solver to have an object follow the user' -->

<span data-ttu-id="ef5ae-121">Dans cette section, vous allez améliorer la collection de boutons que vous avez créée dans le didacticiel précédent afin qu’elle suive la direction du regard de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-121">In this section, you will enhance the button collection you created in the previous tutorial so it follows the user’s gaze direction.</span></span> <span data-ttu-id="ef5ae-122">En outre, vous allez également configurer le solveur pour que la collection de boutons soit toujours :</span><span class="sxs-lookup"><span data-stu-id="ef5ae-122">Additionally, you will also configure the Solver so the button collection is always:</span></span>

* <span data-ttu-id="ef5ae-123">Pivoté parallèlement au sens de lecture de l’utilisateur, pour une lecture naturelle de gauche à droite</span><span class="sxs-lookup"><span data-stu-id="ef5ae-123">Rotated parallel to the user's reading direction, for natural left to right reading</span></span>
* <span data-ttu-id="ef5ae-124">Positionné légèrement sous la direction du point d’interposition horizontal de l’utilisateur, il n’obstrue pas les autres objets que vous ajouterez plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-124">Positioned slightly below the user horizontal gaze direction, so it's not obstructing the other objects you will add later in this tutorial</span></span>
* <span data-ttu-id="ef5ae-125">Positionnée approximativement sur la longueur d’un demi-bras de l’utilisateur, les boutons peuvent être facilement enfoncés</span><span class="sxs-lookup"><span data-stu-id="ef5ae-125">Positioned approximately a half arm's-length from the user, so the buttons can easily be pressed</span></span>

<span data-ttu-id="ef5ae-126">Pour ce faire, vous allez utiliser le **Solveur orbital** qui verrouille l’objet à une position et à un décalage spécifiés à partir de l’objet référencé.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-126">For this, you will use the **Orbital Solver** which locks the object to a specified position and offset from the referenced object.</span></span>

### <a name="1-add-the-orbital-solver"></a><span data-ttu-id="ef5ae-127">1. ajouter le solveur orbital</span><span class="sxs-lookup"><span data-stu-id="ef5ae-127">1. Add the Orbital Solver</span></span>

<span data-ttu-id="ef5ae-128">Dans la fenêtre hiérarchie, sélectionnez l’objet **ButtonCollection** , puis dans la fenêtre de l’inspecteur, utilisez le bouton **Ajouter un composant** pour ajouter le composant **orbital (script)** à l’objet ButtonCollection.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-128">In the Hierarchy window, select the **ButtonCollection** object, then in the Inspector window, use the **Add Component** button to add the **Orbital (Script)** component to the ButtonCollection object.</span></span>

> [!NOTE]
> <span data-ttu-id="ef5ae-129">Lorsque vous ajoutez un solveur, dans ce cas le composant orbital (script), le composant du gestionnaire de solveur (script) est automatiquement ajouté, car il est requis par le solveur.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-129">When you add a Solver, in this case the Orbital (Script) component, the Solver Handler (Script) component is automatically added because it is required by the Solver.</span></span>

### <a name="2-configure-the-orbital-solver"></a><span data-ttu-id="ef5ae-130">2. configurer le solveur orbital</span><span class="sxs-lookup"><span data-stu-id="ef5ae-130">2. Configure the Orbital Solver</span></span>

<span data-ttu-id="ef5ae-131">Configurez le composant du **Gestionnaire de solveur (script)** :</span><span class="sxs-lookup"><span data-stu-id="ef5ae-131">Configure the **Solver Handler (Script)** component:</span></span>

* <span data-ttu-id="ef5ae-132">Vérifier que **le type de cible suivi** est défini sur **Head**</span><span class="sxs-lookup"><span data-stu-id="ef5ae-132">Verify that **Tracked Target Type**  is set to **Head**</span></span>

<span data-ttu-id="ef5ae-133">Configurez le composant **orbital (script)** :</span><span class="sxs-lookup"><span data-stu-id="ef5ae-133">Configure the **Orbital (Script)** component:</span></span>

* <span data-ttu-id="ef5ae-134">Modifier le **type d’orientation** pour suivre l' **objet suivi**</span><span class="sxs-lookup"><span data-stu-id="ef5ae-134">Change **Orientation Type** to **Follow Tracked Object**</span></span>
* <span data-ttu-id="ef5ae-135">Réinitialiser le **décalage local** à X = 0, Y = 0, Z = 0</span><span class="sxs-lookup"><span data-stu-id="ef5ae-135">Reset **Local Offset** to X = 0, Y = 0, Z = 0</span></span>
* <span data-ttu-id="ef5ae-136">Remplacez le **décalage universel** par X = 0, Y =-0,4, Z = 0,3</span><span class="sxs-lookup"><span data-stu-id="ef5ae-136">Change **World Offset** to X = 0, Y = -0.4, Z = 0.3</span></span>

![mrlearning-base](images/mrlearning-base/tutorial3-section2-step2-1.png)

### <a name="3-test-the-orbital-solver-using-the-in-editor-simulation"></a><span data-ttu-id="ef5ae-138">3. tester le solveur orbital à l’aide de la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="ef5ae-138">3. Test the Orbital Solver using the in-editor simulation</span></span>

<span data-ttu-id="ef5ae-139">Appuyez sur le bouton lecture pour passer en mode jeu, puis appuyez et maintenez enfoncé le bouton droit de la souris pour faire pivoter la direction du regard et notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="ef5ae-139">Press the Play button to enter Game mode and press and hold the right mouse button to rotate your gaze direction, and notice the following:</span></span>

* <span data-ttu-id="ef5ae-140">La position de la transformation de ButtonCollection est maintenant pilotée par les paramètres du solveur</span><span class="sxs-lookup"><span data-stu-id="ef5ae-140">The ButtonCollection's Transform Position is now driven by the Solver settings</span></span>
* <span data-ttu-id="ef5ae-141">Le cube, qui n’est pas affecté par le solveur, reste à la même position</span><span class="sxs-lookup"><span data-stu-id="ef5ae-141">The Cube, which is not affected by the Solver, remains in the same position</span></span>

![mrlearning-base](images/mrlearning-base/tutorial3-section2-step3-1.png)

> [!TIP]
> <span data-ttu-id="ef5ae-143">Si vous ne voyez pas le rayon de l’appareil photo dans la fenêtre de votre scène, vérifiez que votre menu gizmos est activé.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-143">If you don't see the camera ray in your Scene window, make sure your Gizmos menu is enabled.</span></span> <span data-ttu-id="ef5ae-144">Pour en savoir plus sur le menu gizmos et sur la façon dont vous pouvez l’utiliser pour optimiser votre vue scène, vous pouvez consulter la documentation du <a href="https://docs.unity3d.com/Manual/GizmosMenu.html" target="_blank">menu gizmos</a> d’Unity.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-144">To learn more about the Gizmos menu and how you can use it to optimize your scene view, you can visit Unity's <a href="https://docs.unity3d.com/Manual/GizmosMenu.html" target="_blank">Gizmos menu</a> documentation.</span></span>
>
> <span data-ttu-id="ef5ae-145">Pour afficher côte à côte votre scène et votre fenêtre de jeu, comme indiqué dans l’image ci-dessus, faites simplement glisser la fenêtre du jeu vers le côté droit de la fenêtre de la scène.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-145">To display your Scene and Game window side by side as shown in the image above, simply drag the Game window to the right side of the Scene window.</span></span> <span data-ttu-id="ef5ae-146">Pour en savoir plus sur la personnalisation de votre espace de travail, vous pouvez consulter la documentation sur la personnalisation de l' <a href="https://docs.unity3d.com/Manual/CustomizingYourWorkspace.html" target="_blank">espace de travail</a> .</span><span class="sxs-lookup"><span data-stu-id="ef5ae-146">To learn more about customizing your workspace, you can visit Unity's <a href="https://docs.unity3d.com/Manual/CustomizingYourWorkspace.html" target="_blank">Customizing Your Workspace</a> documentation.</span></span>

## <a name="enabling-objects-to-follow-tracked-hands"></a><span data-ttu-id="ef5ae-147">Activation d’objets pour suivre les mains suivies</span><span class="sxs-lookup"><span data-stu-id="ef5ae-147">Enabling objects to follow tracked hands</span></span>

<span data-ttu-id="ef5ae-148">Dans cette section, vous allez configurer l’objet de cube que vous avez créé dans le didacticiel précédent afin qu’il suive les mains suivies par l’utilisateur, en particulier le poignet de la main droite.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-148">In this section, you will configure the Cube object you created in the previous tutorial so it follows the user’s tracked hands, specifically the right hand wrist.</span></span> <span data-ttu-id="ef5ae-149">En outre, vous allez également configurer le solveur pour que le cube :</span><span class="sxs-lookup"><span data-stu-id="ef5ae-149">Additionally, you will also configure the Solver so the cube:</span></span>

* <span data-ttu-id="ef5ae-150">Change son orientation avec la rotation manuelle de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ef5ae-150">Changes it's orientation with the user's hand rotation</span></span>
* <span data-ttu-id="ef5ae-151">Positionné sur le poignet de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ef5ae-151">Positioned on the user's wrist</span></span>

<span data-ttu-id="ef5ae-152">Pour ce faire, vous allez utiliser le **Solveur vue radiale** qui conserve l’objet dans un cône de vue converti par l’objet référencé.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-152">For this, you will use the **Radial View Solver** which keeps the object within a view cone cast by the referenced object.</span></span>

### <a name="1-add-the-radial-view-solver"></a><span data-ttu-id="ef5ae-153">1. ajouter le solveur vue radiale</span><span class="sxs-lookup"><span data-stu-id="ef5ae-153">1. Add the Radial View Solver</span></span>

<span data-ttu-id="ef5ae-154">Dans la fenêtre hiérarchie, sélectionnez l’objet **cube** , puis dans la fenêtre de l’inspecteur, utilisez le bouton **Ajouter un composant** pour ajouter l’objet de cube du composant **vue transversale (script)** .</span><span class="sxs-lookup"><span data-stu-id="ef5ae-154">In the Hierarchy window, select the **Cube** object, then in the Inspector window, use the **Add Component** button to add the **Radial View (Script)** component Cube object.</span></span>

### <a name="2-configure-the-radial-view-solver"></a><span data-ttu-id="ef5ae-155">2. configurer le solveur vue radiale</span><span class="sxs-lookup"><span data-stu-id="ef5ae-155">2. Configure the Radial View Solver</span></span>

<span data-ttu-id="ef5ae-156">Configurez le composant du **Gestionnaire de solveur (script)** :</span><span class="sxs-lookup"><span data-stu-id="ef5ae-156">Configure the **Solver Handler (Script)** component:</span></span>

* <span data-ttu-id="ef5ae-157">Modifier **le type de cible suivi** pour la **jointure manuelle**</span><span class="sxs-lookup"><span data-stu-id="ef5ae-157">Change **Tracked Target Type** to **Hand Joint**</span></span>
* <span data-ttu-id="ef5ae-158">Modifier la **main suivie** vers la **droite**</span><span class="sxs-lookup"><span data-stu-id="ef5ae-158">Change **Tracked Handness** to **Right**</span></span>
* <span data-ttu-id="ef5ae-159">Modifier l' **articulation du suivi sur le** **poignet**</span><span class="sxs-lookup"><span data-stu-id="ef5ae-159">Change **Tracked Hand Joint** to **Wrist**</span></span>

<span data-ttu-id="ef5ae-160">Configurez le composant **vue transversale (script)** :</span><span class="sxs-lookup"><span data-stu-id="ef5ae-160">Configure the **Radial View (Script)** component:</span></span>

* <span data-ttu-id="ef5ae-161">Changez le **sens de référence** en **orienté objet**, puis activez la case à cocher **orienter vers la direction de référence**</span><span class="sxs-lookup"><span data-stu-id="ef5ae-161">Change **Reference Direction** to **Object Oriented**, then check the **Orient To Reference Direction** checkbox</span></span>
* <span data-ttu-id="ef5ae-162">Modifier la **distance minimale** et la **distance maximale** à 0</span><span class="sxs-lookup"><span data-stu-id="ef5ae-162">Change **Min Distance** and **Max Distance** to 0</span></span>

![mrlearning-base](images/mrlearning-base/tutorial3-section3-step2-1.png)

### <a name="3-test-the-radial-view-solver-using-the-in-editor-simulation"></a><span data-ttu-id="ef5ae-164">3. tester le solveur de la vue radiale à l’aide de la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="ef5ae-164">3. Test the Radial View Solver using the in-editor simulation</span></span>

<span data-ttu-id="ef5ae-165">Appuyez sur le bouton lecture pour entrer en mode jeu, puis appuyez sur la barre d’espace et maintenez-la enfoncée pour afficher la main.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-165">Press the Play button to enter Game mode and then press and hold the spacebar to bring up the hand.</span></span> <span data-ttu-id="ef5ae-166">Déplacez le curseur de la souris pour déplacer la main, puis cliquez et maintenez enfoncé le bouton gauche de la souris pour faire pivoter la main :</span><span class="sxs-lookup"><span data-stu-id="ef5ae-166">Move the mouse cursor around to move the hand, and click and hold the left mouse button to rotate the hand:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial3-section3-step3-1.png)

## <a name="congratulations"></a><span data-ttu-id="ef5ae-168">Félicitations</span><span class="sxs-lookup"><span data-stu-id="ef5ae-168">Congratulations</span></span>

<span data-ttu-id="ef5ae-169">Dans ce didacticiel, vous avez appris à utiliser les solveurs de MRTK pour qu’une interface utilisateur suive intuitivement l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-169">In this tutorial, you learned how to use the MRTK’s solvers to have a UI intuitively follow the user.</span></span> <span data-ttu-id="ef5ae-170">Vous avez également appris à attacher un solveur à un objet (par exemple, cube) pour suivre les mains suivies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ef5ae-170">You also learned how to attach a Solver to an object (i.e., cube) to follow the user’s tracked hands.</span></span> <span data-ttu-id="ef5ae-171">Pour en savoir plus sur ces autres programmes de résolution inclus dans le MRTK, vous pouvez consulter le guide des [solveurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) dans le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="ef5ae-171">To learn more about these and other solvers included with the MRTK,  you can visit the [Solvers](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

[<span data-ttu-id="ef5ae-172">Didacticiel suivant : 5. interaction avec les objets 3D</span><span class="sxs-lookup"><span data-stu-id="ef5ae-172">Next Tutorial: 5. Interacting with 3D objects</span></span>](mrlearning-base-ch4.md)
