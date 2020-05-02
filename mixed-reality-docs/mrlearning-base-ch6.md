---
title: Tutoriels de démarrage - 7. Création d’un exemple d’application Module lunaire
description: Dans cette leçon, vous allez combiner plusieurs concepts tirés des leçons précédentes pour créer un exemple d’expérience unique.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 7b432c5ba0ebee5199f5abb1c26715185fc0d70d
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "79031566"
---
# <a name="7-creating-a-lunar-module-sample-application"></a><span data-ttu-id="0915f-105">7. Création d’un exemple d’application Module lunaire</span><span class="sxs-lookup"><span data-stu-id="0915f-105">7. Creating a Lunar Module sample application</span></span>
<!-- TODO: Rename to 'Creating a Rocket Launcher sample application' -->

<span data-ttu-id="0915f-106">Dans ce tutoriel, plusieurs concepts issus des leçons précédentes sont combinés pour créer un exemple d’expérience unique.</span><span class="sxs-lookup"><span data-stu-id="0915f-106">In this tutorial, multiple concepts are combined from previous lessons to create a unique sample experience.</span></span> <span data-ttu-id="0915f-107">Vous allez apprendre à créer une application d’assemblage de composants dans laquelle un utilisateur doit utiliser ses mains, dont les mouvements sont captés, pour saisir des composants et tenter d’assembler un module lunaire.</span><span class="sxs-lookup"><span data-stu-id="0915f-107">You will learn how to create a part assembly application whereby a user needs to use tracked hands to pick up parts and attempt to assemble a lunar module.</span></span> <span data-ttu-id="0915f-108">Vous utiliserez des boutons enfonçables pour activer/désactiver des indicateurs d’emplacement, réinitialiser l’expérience et lancer le module lunaire dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="0915f-108">You will use pressable buttons to toggle placement hints on and off, to reset the experience, and to launch the lunar module into space!</span></span>

<span data-ttu-id="0915f-109">Vous continuerez à développer cette expérience dans les tutoriels à venir, notamment avec des cas d’usage multiutilisateurs complexes qui tirent parti d’Azure Spatial Anchors pour l’alignement spatial.</span><span class="sxs-lookup"><span data-stu-id="0915f-109">In future tutorials, you will continue to build upon this experience, which includes powerful multi-user use cases that leverage Azure Spatial Anchors for spatial alignment.</span></span>

## <a name="objectives"></a><span data-ttu-id="0915f-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="0915f-110">Objectives</span></span>

* <span data-ttu-id="0915f-111">Combiner plusieurs concepts issus des leçons précédentes pour créer une même expérience</span><span class="sxs-lookup"><span data-stu-id="0915f-111">Combine multiple concepts from previous lessons to create a unique experience</span></span>
* <span data-ttu-id="0915f-112">Découvrir comment activer/désactiver des objets</span><span class="sxs-lookup"><span data-stu-id="0915f-112">Learn how to toggle objects</span></span>
* <span data-ttu-id="0915f-113">Déclencher des événements complexes en utilisant des boutons enfonçables</span><span class="sxs-lookup"><span data-stu-id="0915f-113">Trigger complex events using pressable buttons</span></span>
* <span data-ttu-id="0915f-114">Utiliser la physique et les forces des corps rigides</span><span class="sxs-lookup"><span data-stu-id="0915f-114">Use rigidbody physics and forces</span></span>
* <span data-ttu-id="0915f-115">Explorer l’utilisation d’info-bulles</span><span class="sxs-lookup"><span data-stu-id="0915f-115">Explore the use of tool tips</span></span>

## <a name="lunar-module-parts-overview"></a><span data-ttu-id="0915f-116">Vue d’ensemble des composants du module lunaire</span><span class="sxs-lookup"><span data-stu-id="0915f-116">Lunar Module Parts overview</span></span>
<!-- TODO: Rename to 'Implementing the part assembly functionality' -->

<span data-ttu-id="0915f-117">Dans cette section, vous allez créer une tâche simple d’assemblage où l’objectif de l’utilisateur est de placer cinq composants répartis sur une table au bon endroit sur le module lunaire.</span><span class="sxs-lookup"><span data-stu-id="0915f-117">In this section, you will create a simple part assembly challenge where the user's goal is to place five parts that are spread out on the table at the correct location on the Lunar Module.</span></span>

<span data-ttu-id="0915f-118">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="0915f-118">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="0915f-119">Ajouter le préfabriqué RocketLauncher à la scène</span><span class="sxs-lookup"><span data-stu-id="0915f-119">Add the Rocket Launcher prefab to the scene</span></span>
2. <span data-ttu-id="0915f-120">Activer la manipulation d’objets pour tous les composants</span><span class="sxs-lookup"><span data-stu-id="0915f-120">Enable object manipulation for all the parts</span></span>
3. <span data-ttu-id="0915f-121">Ajouter et configurer le composant Part Assembly Demo (Script)</span><span class="sxs-lookup"><span data-stu-id="0915f-121">Add and configure the Part Assembly Demo (Script) component</span></span>

> [!NOTE]
> <span data-ttu-id="0915f-122">Le composant Part Assembly Demo (Script) ne fait pas partie du MRTK.</span><span class="sxs-lookup"><span data-stu-id="0915f-122">The Part Assembly Demo (Script) component is not part of MRTK.</span></span> <span data-ttu-id="0915f-123">Il a été fourni avec les ressources de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="0915f-123">It was provided with this tutorial's assets.</span></span>

### <a name="1-add-the-rocket-launcher-prefab-to-the-scene"></a><span data-ttu-id="0915f-124">1. Ajouter le préfabriqué RocketLauncher à la scène</span><span class="sxs-lookup"><span data-stu-id="0915f-124">1. Add the Rocket Launcher prefab to the scene</span></span>

<span data-ttu-id="0915f-125">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** > **RocketLauncher**, faites glisser le préfabriqué **RocketLauncher** dans la fenêtre Hierarchy pour l’ajouter à votre scène, puis positionnez-le à un emplacement approprié. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0915f-125">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** > **RocketLauncher** folder, drag the **RocketLauncher** prefab into the Hierarchy window to add it to your scene, and then position it at a suitable location, for example:</span></span>

* <span data-ttu-id="0915f-126">Sous Transform, définissez Position avec les valeurs X = 1,5, Y =-0,4 et Z = 0 pour le positionner à droite de l’utilisateur à hauteur de taille.</span><span class="sxs-lookup"><span data-stu-id="0915f-126">Transform Position X = 1.5, Y = -0.4, Z = 0, so it is positioned to the right of the user at waist height</span></span>
* <span data-ttu-id="0915f-127">Sous Transform, définissez Rotation avec les valeurs X = 0, Y = 180 et Z = 0 pour que les principales fonctionnalités de l’expérience soient face à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0915f-127">Transform Rotation X = 0, Y = 180, Z = 0, so the main features of the experience faces the user</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step1-1.png)

### <a name="2-enable-object-manipulation-for-all-the-parts"></a><span data-ttu-id="0915f-129">2. Activer la manipulation d’objets pour tous les composants</span><span class="sxs-lookup"><span data-stu-id="0915f-129">2. Enable object manipulation for all the parts</span></span>

<span data-ttu-id="0915f-130">Dans la fenêtre Hierarchy, localisez l’objet RocketLauncher > **LunarModuleParts** et sélectionnez tous les **objets enfants**. Ajoutez les composants **Manipulation Handler (Script)** et **Near Interaction Grabbable (Script)** , puis configurez Manipulation Handler (Script) comme suit :</span><span class="sxs-lookup"><span data-stu-id="0915f-130">In the Hierarchy window, locate the RocketLauncher > **LunarModuleParts** object and select all the **child objects**, add the **Manipulation Handler (Script)** component and the **Near Interaction Grabbable (Script)** component, and then configure the Manipulation Handler (Script) as follows:</span></span>

* <span data-ttu-id="0915f-131">Décochez la case **Allow Far Manipulation** pour autoriser uniquement l’interaction proche.</span><span class="sxs-lookup"><span data-stu-id="0915f-131">Un-check the **Allow Far Manipulation** checkbox to only allow near interaction</span></span>
* <span data-ttu-id="0915f-132">En regard de **Two Handed Manipulation Type**, sélectionnez **Move Rotate** pour désactiver la mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="0915f-132">Change **Two Handed Manipulation Type** to **Move Rotate** so scaling is disabled</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step1-2.png)

> [!TIP]
> <span data-ttu-id="0915f-134">Si vous avez besoin d’un rappel et d’instructions pas à pas sur la façon d’implémenter la manipulation d’objets, consultez [Manipulation des objets 3D](mrlearning-base-ch4.md#manipulating-3d-objects).</span><span class="sxs-lookup"><span data-stu-id="0915f-134">For a reminder, with step by step instructions, on how to implement object manipulation, you can refer to the [Manipulating 3D Objects](mrlearning-base-ch4.md#manipulating-3d-objects) instructions.</span></span>

### <a name="3-add-and-configure-the-part-assembly-demo-script-component"></a><span data-ttu-id="0915f-135">3. Ajouter et configurer le composant Part Assembly Demo (Script)</span><span class="sxs-lookup"><span data-stu-id="0915f-135">3. Add and configure the Part Assembly Demo (Script) component</span></span>

<span data-ttu-id="0915f-136">Tous les objets enfants de LunarModuleParts étant encore sélectionnés, ajoutez un composant **Audio Source** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="0915f-136">With all the LunarModuleParts child objects still selected, add an **Audio Source** component and then configure it as follows:</span></span>

* <span data-ttu-id="0915f-137">Affectez un clip audio approprié au champ **AudioClip**, par exemple, MRKT_Scale_Start.</span><span class="sxs-lookup"><span data-stu-id="0915f-137">Assign a suitable audio clip to the **AudioClip** field, for example, MRKT_Scale_Start</span></span>
* <span data-ttu-id="0915f-138">Décochez la case **Play On Awake** pour ne pas lire automatiquement le clip audio quand la scène se charge.</span><span class="sxs-lookup"><span data-stu-id="0915f-138">Un-check the **Play On Awake** checkbox, so the audio clip does not automatically play when the scene loads</span></span>
* <span data-ttu-id="0915f-139">Définissez **Spatial Blend** avec la valeur 1 pour activer l’audio spatial.</span><span class="sxs-lookup"><span data-stu-id="0915f-139">Change **Spatial Blend** to 1, to enable spatial audio</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-1.png)

<span data-ttu-id="0915f-141">Tous les objets enfants de LunarModuleParts étant encore sélectionnés, ajoutez le composant **Part Assembly Demo (Script)**  :</span><span class="sxs-lookup"><span data-stu-id="0915f-141">With all the LunarModuleParts child objects still selected, add the **Part Assembly Demo  (Script)** component:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-2.png)

<span data-ttu-id="0915f-143">Dans la fenêtre Hierarchy, sélectionnez l’objet **RoverEnclosure** et configurez son composant **Part Assembly Demo (Script)** comme suit :</span><span class="sxs-lookup"><span data-stu-id="0915f-143">In the Hierarchy window, select the **RoverEnclosure** object and configure its **Part Assembly Demo (Script)** component as follows:</span></span>

* <span data-ttu-id="0915f-144">Affectez au champ **Object To Place** l’objet **lui-même**, dans ce cas RoverEnclosure.</span><span class="sxs-lookup"><span data-stu-id="0915f-144">To the **Object To Place** field, assign the object **itself**, in this case, the RoverEnclosure object</span></span>
* <span data-ttu-id="0915f-145">Affectez au champ **Location To Place** l’objet **PlacementHints** correspondant, dans ce cas RoverEnclosure_PlacementHint.</span><span class="sxs-lookup"><span data-stu-id="0915f-145">To the **Location To Place** field, assign the corresponding **PlacementHints** object, in this case, the RoverEnclosure_PlacementHint object</span></span>
* <span data-ttu-id="0915f-146">Affectez au champ **Tool Tip Object** l’objet **ToolTip** correspondant, dans ce cas RoverEnclosure_ToolTip.</span><span class="sxs-lookup"><span data-stu-id="0915f-146">To the **Tool Tip Object** field, assign the corresponding **ToolTip**, in this case, the RoverEnclosure_ToolTip object</span></span>
* <span data-ttu-id="0915f-147">Affectez au champ **Audio Source** l’objet **lui-même**, dans ce cas RoverEnclosure.</span><span class="sxs-lookup"><span data-stu-id="0915f-147">To the **Audio Source** field, assign the object **itself**, in this case, the RoverEnclosure object</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-3.png)

<span data-ttu-id="0915f-149">**Répétez** ces opérations pour chaque objet enfant de LunarModuleParts, comme FuelTank, EnergyCell, DockingPortal et ExternalSensor.</span><span class="sxs-lookup"><span data-stu-id="0915f-149">**Repeat** for each of the other LunarModuleParts child objects, i.e. FuelTank, EnergyCell, DockingPortal, and ExternalSensor.</span></span>

<span data-ttu-id="0915f-150">Si vous passez maintenant en mode Game et déplacez un « Object To Place » à proximité de son « Location To Place » correspondant, voilà ce qui se passe :</span><span class="sxs-lookup"><span data-stu-id="0915f-150">If you now enter Game mode and move an 'Object To Place' close to it's corresponding 'Location To Place' you will notice:</span></span>

* <span data-ttu-id="0915f-151">L’objet est ancré et apparenté à l’objet LunarModule. Il fait donc partie du module lunaire.</span><span class="sxs-lookup"><span data-stu-id="0915f-151">The object will snap into place and be parented under the LunarModule object so it becomes part of the Lunar Module</span></span>
* <span data-ttu-id="0915f-152">La source audio sur l’objet lit le clip audio affecté à l’emplacement de l’objet.</span><span class="sxs-lookup"><span data-stu-id="0915f-152">The Audio Source on the object will play the assigned Audio Clip at the location of the object</span></span>
* <span data-ttu-id="0915f-153">L’objet Tool Tip correspondant est masqué.</span><span class="sxs-lookup"><span data-stu-id="0915f-153">The corresponding Tool Tip object will be hidden</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-4.png)

> [!TIP]
> <span data-ttu-id="0915f-155">Si vous avez besoin d’un rappel sur la façon d’utiliser la simulation d’entrée dans l’éditeur, consultez le [guide d’utilisation de la simulation d’entrée avec les mains dans l’éditeur pour tester une scène](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="0915f-155">For a reminder on how to use the in-editor input simulation, you can refer to the [Using the In-Editor Hand Input Simulation to test a scene](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="configuring-the-lunar-module"></a><span data-ttu-id="0915f-156">Configuration du module lunaire</span><span class="sxs-lookup"><span data-stu-id="0915f-156">Configuring the Lunar Module</span></span>

<span data-ttu-id="0915f-157">Dans cette section, vous allez ajouter des fonctionnalités à l’application RocketLauncher pour que l’utilisateur puisse effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="0915f-157">In this section, you will add additional features to the Rocket Launcher application so the user can:</span></span>

* <span data-ttu-id="0915f-158">Interagir avec le module lunaire</span><span class="sxs-lookup"><span data-stu-id="0915f-158">Interact with the Lunar Module</span></span>
* <span data-ttu-id="0915f-159">Lancer le module lunaire dans l’espace et émettre un signal sonore quand il est lancé</span><span class="sxs-lookup"><span data-stu-id="0915f-159">Launch the Lunar Module into space and play a sound when it is launched</span></span>
* <span data-ttu-id="0915f-160">Réinitialiser l’application pour faire revenir le module lunaire et tous les composants à leur position d’origine</span><span class="sxs-lookup"><span data-stu-id="0915f-160">Reset the application so the Lunar Module and all the parts are placed back to their original position</span></span>
* <span data-ttu-id="0915f-161">Masquer les indicateurs de placement pour rendre le test d’assemblage de composants plus difficile</span><span class="sxs-lookup"><span data-stu-id="0915f-161">Hide the placement hints to make the part assembly challenge more difficult.</span></span>

<span data-ttu-id="0915f-162">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="0915f-162">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="0915f-163">Activer la manipulation d’objets</span><span class="sxs-lookup"><span data-stu-id="0915f-163">Enable object manipulation</span></span>
2. <span data-ttu-id="0915f-164">Activer les propriétés physiques</span><span class="sxs-lookup"><span data-stu-id="0915f-164">Enable physics</span></span>
3. <span data-ttu-id="0915f-165">Ajouter un composant Audio Source</span><span class="sxs-lookup"><span data-stu-id="0915f-165">Add an Audio Source component</span></span>
4. <span data-ttu-id="0915f-166">Ajouter et configurer le composant Launch Lunar Module (Script)</span><span class="sxs-lookup"><span data-stu-id="0915f-166">Add and configure the Launch Lunar Module (Script) component</span></span>
5. <span data-ttu-id="0915f-167">Ajouter et configurer le composant Toggle Placement Hints (Script)</span><span class="sxs-lookup"><span data-stu-id="0915f-167">Add and configure the Toggle Placement Hints (Script) component</span></span>

> [!NOTE]
> <span data-ttu-id="0915f-168">Les composants Launch Lunar Module (Script) et Toggle Placement Hints (Script) ne font pas partie du MRTK.</span><span class="sxs-lookup"><span data-stu-id="0915f-168">The Launch Lunar Module (Script) component and the Toggle Placement Hints (Script) component are not part of MRTK.</span></span> <span data-ttu-id="0915f-169">Ils ont été fournis avec les ressources de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="0915f-169">They were provided with this tutorial's assets.</span></span>

### <a name="1-enable-object-manipulation"></a><span data-ttu-id="0915f-170">1. Activer la manipulation d’objets</span><span class="sxs-lookup"><span data-stu-id="0915f-170">1. Enable object manipulation</span></span>

<span data-ttu-id="0915f-171">Dans la fenêtre Hierarchy, sélectionnez l’objet RocketLauncher > **LunarModuleParts**, ajoutez les composants **Manipulation Handler (Script)** et **Near Interaction Grabbable (Script)** , puis configurez Manipulation Handler (Script) comme suit :</span><span class="sxs-lookup"><span data-stu-id="0915f-171">In the Hierarchy window, select the RocketLauncher > **LunarModule** object, add the **Manipulation Handler (Script)** component and the **Near Interaction Grabbable (Script)** component, and then configure the Manipulation Handler (Script) as follows:</span></span>

* <span data-ttu-id="0915f-172">Décochez la case **Allow Far Manipulation** pour autoriser uniquement l’interaction proche.</span><span class="sxs-lookup"><span data-stu-id="0915f-172">Un-check the **Allow Far Manipulation** checkbox to only allow near interaction</span></span>
* <span data-ttu-id="0915f-173">En regard de **Two Handed Manipulation Type**, sélectionnez Move Rotate pour désactiver la mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="0915f-173">Change **Two Handed Manipulation Type** to Move Rotate so scaling is disabled</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step1-1.png)

### <a name="2-enable-physics"></a><span data-ttu-id="0915f-175">2. Activer les propriétés physiques</span><span class="sxs-lookup"><span data-stu-id="0915f-175">2. Enable physics</span></span>

<span data-ttu-id="0915f-176">L’objet RocketLauncher > **LunarModule** étant encore sélectionné, ajoutez un composant **RigidBody**, puis configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="0915f-176">With the RocketLauncher > **LunarModule** object still selected, add a **Rigidbody** component and then configure it as follows:</span></span>

* <span data-ttu-id="0915f-177">Décochez la case **Use Gravity** pour que le module lunaire ne soit pas affecté par la gravité.</span><span class="sxs-lookup"><span data-stu-id="0915f-177">Un-check the **Use Gravity** checkbox so the Lunar Module is not affected by gravity</span></span>
* <span data-ttu-id="0915f-178">Cochez la case **Is Kinematic** pour que le module lunaire ne soit pas initialement affecté par les forces physiques.</span><span class="sxs-lookup"><span data-stu-id="0915f-178">Check the **Is Kinematic** checkbox so the Lunar Module initially isn't affected by physic forces</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step2-1.png)

### <a name="3-add-an-audio-source-component"></a><span data-ttu-id="0915f-180">3. Ajouter un composant Audio Source</span><span class="sxs-lookup"><span data-stu-id="0915f-180">3. Add an Audio Source component</span></span>

<span data-ttu-id="0915f-181">L’objet RocketLauncher > **LunarModule** étant encore sélectionné, ajoutez un composant **Audio Source**, puis configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="0915f-181">With the RocketLauncher > **LunarModule** object still selected, add an **Audio Source** component and then configure it as follows:</span></span>

* <span data-ttu-id="0915f-182">Définissez **Spatial Blend** avec la valeur 1 pour activer l’audio spatial.</span><span class="sxs-lookup"><span data-stu-id="0915f-182">Change **Spatial Blend** to 1 to enable spatial audio</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step3-1.png)

### <a name="4-add-and-configure-the-launch-lunar-module-script-component"></a><span data-ttu-id="0915f-184">4. Ajouter et configurer le composant Launch Lunar Module (Script)</span><span class="sxs-lookup"><span data-stu-id="0915f-184">4. Add and configure the Launch Lunar Module (Script) component</span></span>

<span data-ttu-id="0915f-185">L’objet RocketLauncher > **LunarModule** étant encore sélectionné, ajoutez le composant **Launch Lunar Module (Script)** , puis configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="0915f-185">With the RocketLauncher > **LunarModule** object still selected, add the **Launch Lunar Module (Script)** component and then configure it as follows:</span></span>

* <span data-ttu-id="0915f-186">Définissez **Thrust** pour que le module lunaire décolle correctement au lancement, par exemple avec la valeur 0,01.</span><span class="sxs-lookup"><span data-stu-id="0915f-186">Change **Thrust** value so the Lunar Module will fly up gracefully when launched, for example, to 0.01</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step4-1.png)

### <a name="5-add-and-configure-the-toggle-placement-hints-script-component"></a><span data-ttu-id="0915f-188">5. Ajouter et configurer le composant Toggle Placement Hints (Script)</span><span class="sxs-lookup"><span data-stu-id="0915f-188">5. Add and configure the Toggle Placement Hints (Script) component</span></span>

<span data-ttu-id="0915f-189">L’objet RocketLauncher > **LunarModule** étant encore sélectionné, ajoutez le composant **Toggle Placement Hints (Script)** , puis configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="0915f-189">With the RocketLauncher > **LunarModule** object still selected, add the **Toggle Placement Hints (Script)** component and then configure it as follows:</span></span>

* <span data-ttu-id="0915f-190">Définissez la propriété **Size** de Game Object Array avec la valeur 5.</span><span class="sxs-lookup"><span data-stu-id="0915f-190">Set the Game Object Array **Size** property to 5</span></span>
* <span data-ttu-id="0915f-191">Affectez chaque **objet enfant** de l’objet RocketLauncher > LunarModule > **PlacementHints** à un champ **Element** de Game Object Array :</span><span class="sxs-lookup"><span data-stu-id="0915f-191">Assign each of the RocketLauncher > LunarModule > **PlacementHints** object's **child objects** to the an **Element** field in the Game Object Array:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step5-1.png)

## <a name="configuring-the-launch-button"></a><span data-ttu-id="0915f-193">Configuration du bouton de lancement</span><span class="sxs-lookup"><span data-stu-id="0915f-193">Configuring the Launch button</span></span>

<span data-ttu-id="0915f-194">Dans la fenêtre Hierarchy, sélectionnez l’objet RocketLauncher > Buttons > **LaunchButton**, puis dans le composant **Pressable Button (Script)** , créez un événement **Button Pressed ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **LaunchLunarModule.StartThruster** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="0915f-194">In the Hierarchy window, select the RocketLauncher > Buttons > **LaunchButton** object, then on the **Pressable Button (Script)** component, create a new **Button Pressed ()** event, configure the **LunarModule** object to receive the event, and define **LaunchLunarModule.StartThruster** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-1.png)

> [!TIP]
> <span data-ttu-id="0915f-196">Si vous avez besoin d’un rappel sur la façon d’implémenter des événements, consultez les instructions dans [Gestes de suivi de la main et boutons d’interaction](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons).</span><span class="sxs-lookup"><span data-stu-id="0915f-196">For a reminder on how to implement events, you can refer to the [Hand tracking gestures and interactable buttons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) instructions.</span></span>

<span data-ttu-id="0915f-197">L’objet RocketLauncher > Buttons > **LaunchButton** étant encore sélectionné, dans le composant **Pressable Button (Script)** , créez un événement **Button Pressed ()** , configurez l’objet **LunarModule** pour recevoir l’événement, définissez **AudioSource.PlayOneShot** comme action à déclencher, puis affectez un clip audio approprié au champ **Audio Clip**, par exemple le clip audio MRTK_Gem :</span><span class="sxs-lookup"><span data-stu-id="0915f-197">With the RocketLauncher > Buttons > **LaunchButton** object still selected, on the **Pressable Button (Script)** component, create a new **Button Pressed ()** event, configure the **LunarModule** object to receive the event, define **AudioSource.PlayOneShot** as the action to be triggered, and assign a suitable audio clip to the **Audio Clip** field, for example, the MRTK_Gem audio clip:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-2.png)

<span data-ttu-id="0915f-199">L’objet RocketLauncher > Buttons > **LaunchButton** étant encore sélectionné, dans le composant **Pressable Button (Script)** , créez un événement **Touch End ()** , configurez l’objet **LunarModule** pour recevoir l’événement, puis définissez **LaunchLunarModule.StopThruster** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="0915f-199">With the RocketLauncher > Buttons > **LaunchButton** object still selected, on the **Pressable Button (Script)** component, create a new **Touch End ()** event, configure the **LunarModule** object to receive the event, and define **LaunchLunarModule.StopThruster** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-3.png)

<span data-ttu-id="0915f-201">Si vous passez maintenant en mode Game et que vous appuyez sur le bouton de lancement, vous entendez le clip audio. Si vous maintenez le bouton de lancement enfoncé pendant au moins une seconde, le module lunaire est lancé dans l’espace :</span><span class="sxs-lookup"><span data-stu-id="0915f-201">If you now enter Game mode and press the Launch button, you will hear the audio clip play, and if you hold the Launch button down for about a second or longer, you will see the Lunar Module launch into space:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-4.png)

## <a name="configuring-the-reset-button"></a><span data-ttu-id="0915f-203">Configuration du bouton de réinitialisation</span><span class="sxs-lookup"><span data-stu-id="0915f-203">Configuring the Reset button</span></span>

<span data-ttu-id="0915f-204">Dans la fenêtre Hierarchy, sélectionnez l’objet RocketLauncher > Buttons > **ResetButton**, puis dans le composant **Pressable Button (Script)** , créez un événement **Button Pressed ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **LaunchLunarModule.ResetModule** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="0915f-204">In the Hierarchy window, select the RocketLauncher > Buttons > **ResetButton** object, then on the **Pressable Button (Script)** component, create a new **Button Pressed ()** event, configure the **LunarModule** object to receive the event, and define **LaunchLunarModule.ResetModule** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section4-step1-1.png)

<span data-ttu-id="0915f-206">L’objet RocketLauncher > Buttons > **ResetButton** étant encore sélectionné, dans le composant **Pressable Button (Script)** , créez un événement **Button Pressed ()** , configurez l’objet **RocketLauncher** pour recevoir l’événement, définissez **GameObject.BroadcastMessage** comme action à déclencher, puis entrez **ResetPlacement** dans le champ du message :</span><span class="sxs-lookup"><span data-stu-id="0915f-206">With the RocketLauncher > Buttons > **ResetButton** object still selected, on the **Pressable Button (Script)** component, create a new **Button Pressed ()** event, configure the **RocketLauncher** object to receive the event, define **GameObject.BroadcastMessage** as the action to be triggered, and enter **ResetPlacement** in message field:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section4-step1-2.png)

> [!TIP]
> <span data-ttu-id="0915f-208">L’action GameObject.BroadcastMessage envoie le message ResetPlacement de l’objet RocketLauncher à tous ses objets enfants.</span><span class="sxs-lookup"><span data-stu-id="0915f-208">The GameObject.BroadcastMessage action sends the ResetPlacement message from the RocketLauncher object to all its child object.</span></span> <span data-ttu-id="0915f-209">Tout objet enfant ayant la fonction ResetPlacement, qui est définie dans le composant Part Assembly Demo (Script) que vous avez ajouté à tous les objets enfants de LunarModuleParts, appelle la fonction ResetPlacement qui réinitialise le placement de l’objet enfant.</span><span class="sxs-lookup"><span data-stu-id="0915f-209">Any child object that has the ResetPlacement function, which is defined in the Part Assembly Demo (Script) component you added to all the LunarModuleParts child object, will invoke the ResetPlacement function which resets that child object's placement.</span></span>

<span data-ttu-id="0915f-210">Si vous passez maintenant en mode Game, déplacez certains composants et/ou lancez le module lunaire, puis appuyez sur le bouton Reset, la position d’origine des composants et/ou du module lunaire est rétablie :</span><span class="sxs-lookup"><span data-stu-id="0915f-210">If you now enter Game mode, move some parts and/or launch the Lunar Module, and then press the Reset button you will see the parts and/or the Lunar Module being reset to their original position:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section4-step1-3.png)

## <a name="configuring-the-placement-hints-button"></a><span data-ttu-id="0915f-212">Configuration du bouton d’indicateurs de placement</span><span class="sxs-lookup"><span data-stu-id="0915f-212">Configuring the Placement Hints button</span></span>
<!-- TODO: Rename to 'Configuring the Hints button'-->

<span data-ttu-id="0915f-213">Dans la fenêtre Hierarchy, sélectionnez l’objet RocketLauncher > Buttons > **HintsButton**, puis dans le composant **Pressable Button (Script)** , créez un événement **Button Pressed ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **TogglePlacementHints.ToggleGameObjects** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="0915f-213">In the Hierarchy window, select the RocketLauncher > Buttons > **HintsButton** object, then on the **Pressable Button (Script)** component, create a new **Button Pressed ()** event, configure the **LunarModule** object to receive the event, and define **TogglePlacementHints.ToggleGameObjects** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section5-step1-1.png)

<span data-ttu-id="0915f-215">Si vous passez maintenant en mode Game, vous pouvez constater que les indicateurs d’emplacement translucides sont désactivés par défaut. Vous pouvez toutefois les activer et les désactiver en appuyant sur le bouton d’indicateurs de placement :</span><span class="sxs-lookup"><span data-stu-id="0915f-215">If you now enter Game mode you will notice that the translucent placement hints are disabled by default, but that you can toggle them on and off by pressing the Hints button:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section5-step1-2.png)

## <a name="congratulations"></a><span data-ttu-id="0915f-217">Félicitations</span><span class="sxs-lookup"><span data-stu-id="0915f-217">Congratulations</span></span>

<span data-ttu-id="0915f-218">Vous avez entièrement configuré cette application.</span><span class="sxs-lookup"><span data-stu-id="0915f-218">You have fully configured this application.</span></span> <span data-ttu-id="0915f-219">Les utilisateurs peuvent désormais assembler entièrement le module lunaire, le lancer, activer/désactiver les indicateurs et réinitialiser l’application pour recommencer.</span><span class="sxs-lookup"><span data-stu-id="0915f-219">Now, your application allows users to fully assemble the Lunar Module, launch the Lunar Module, toggle hints, and reset the application to start again.</span></span>
