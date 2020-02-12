---
title: Didacticiels de mise en route-7. Création d’un exemple d’application de module lunaire
description: Dans cette leçon, vous allez combiner plusieurs concepts appris dans les leçons précédentes pour créer un exemple d’expérience unique.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: b5b1bd0115822449bd6098f78cfc94d909169737
ms.sourcegitcommit: cc61f7ac08f9ac2f2f04e8525c3260ea073e04a7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/11/2020
ms.locfileid: "77129420"
---
# <a name="7-creating-a-lunar-module-sample-application"></a><span data-ttu-id="2de3c-105">7. création d’un exemple d’application de module lunaire</span><span class="sxs-lookup"><span data-stu-id="2de3c-105">7. Creating a Lunar Module sample application</span></span>
<!-- TODO: Rename to 'Creating a Rocket Launcher sample application' -->

<span data-ttu-id="2de3c-106">Dans ce didacticiel, plusieurs concepts sont combinés à partir de leçons précédentes pour créer un exemple d’expérience unique.</span><span class="sxs-lookup"><span data-stu-id="2de3c-106">In this tutorial, multiple concepts are combined from previous lessons to create a unique sample experience.</span></span> <span data-ttu-id="2de3c-107">Vous allez apprendre à créer une application d’assemblage de pièces dans laquelle un utilisateur doit utiliser des mains suivies pour récupérer des pièces et tenter d’assembler un module lunaire.</span><span class="sxs-lookup"><span data-stu-id="2de3c-107">You will learn how to create a part assembly application whereby a user needs to use tracked hands to pick up parts and attempt to assemble a lunar module.</span></span> <span data-ttu-id="2de3c-108">Vous allez utiliser des boutons permettant d’activer et de désactiver les indicateurs de positionnement, de réinitialiser l’expérience et de lancer le module lunaire dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="2de3c-108">You will use pressable buttons to toggle placement hints on and off, to reset the experience, and to launch the lunar module into space!</span></span>

<span data-ttu-id="2de3c-109">Dans les prochains didacticiels, vous continuerez à développer cette expérience, qui comprend des cas d’utilisation multi-utilisateurs puissants qui tirent parti des ancres spatiales Azure pour l’alignement spatial.</span><span class="sxs-lookup"><span data-stu-id="2de3c-109">In future tutorials, you will continue to build upon this experience, which includes powerful multi-user use cases that leverage Azure Spatial Anchors for spatial alignment.</span></span>

## <a name="objectives"></a><span data-ttu-id="2de3c-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2de3c-110">Objectives</span></span>

* <span data-ttu-id="2de3c-111">Combiner plusieurs concepts issus des leçons précédentes pour créer une même expérience</span><span class="sxs-lookup"><span data-stu-id="2de3c-111">Combine multiple concepts from previous lessons to create a unique experience</span></span>
* <span data-ttu-id="2de3c-112">Découvrir comment activer/désactiver des objets</span><span class="sxs-lookup"><span data-stu-id="2de3c-112">Learn how to toggle objects</span></span>
* <span data-ttu-id="2de3c-113">Déclencher des événements complexes en utilisant des boutons enfonçables</span><span class="sxs-lookup"><span data-stu-id="2de3c-113">Trigger complex events using pressable buttons</span></span>
* <span data-ttu-id="2de3c-114">Utiliser la physique et les forces des corps rigides</span><span class="sxs-lookup"><span data-stu-id="2de3c-114">Use rigidbody physics and forces</span></span>
* <span data-ttu-id="2de3c-115">Explorer l’utilisation d’info-bulles</span><span class="sxs-lookup"><span data-stu-id="2de3c-115">Explore the use of tool tips</span></span>

## <a name="lunar-module-parts-overview"></a><span data-ttu-id="2de3c-116">Vue d’ensemble des parties du module lunaire</span><span class="sxs-lookup"><span data-stu-id="2de3c-116">Lunar Module Parts overview</span></span>
<!-- TODO: Rename to 'Implementing the part assembly functionality' -->

<span data-ttu-id="2de3c-117">Dans cette section, vous allez créer un simple défi d’assemblage de pièces où l’objectif de l’utilisateur est de placer cinq parties qui sont réparties sur la table à l’emplacement approprié sur le module lunaire.</span><span class="sxs-lookup"><span data-stu-id="2de3c-117">In this section, you will create a simple part assembly challenge where the user's goal is to place five parts that are spread out on the table at the correct location on the Lunar Module.</span></span>

<span data-ttu-id="2de3c-118">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="2de3c-118">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="2de3c-119">Ajouter le Prefab du lanceur Rocket à la scène</span><span class="sxs-lookup"><span data-stu-id="2de3c-119">Add the Rocket Launcher prefab to the scene</span></span>
2. <span data-ttu-id="2de3c-120">Activer la manipulation d’objets pour toutes les parties</span><span class="sxs-lookup"><span data-stu-id="2de3c-120">Enable object manipulation for all the parts</span></span>
3. <span data-ttu-id="2de3c-121">Ajouter et configurer le composant de démonstration d’assembly d’un composant (script)</span><span class="sxs-lookup"><span data-stu-id="2de3c-121">Add and configure the Part Assembly Demo (Script) component</span></span>

> [!NOTE]
> <span data-ttu-id="2de3c-122">Le composant de démonstration de l’assembly de composant (script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="2de3c-122">The Part Assembly Demo (Script) component is not part of MRTK.</span></span> <span data-ttu-id="2de3c-123">Il a été fourni avec les ressources de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2de3c-123">It was provided with this tutorial's assets.</span></span>

### <a name="1-add-the-rocket-launcher-prefab-to-the-scene"></a><span data-ttu-id="2de3c-124">1. ajouter le Prefab du lanceur Rocket à la scène</span><span class="sxs-lookup"><span data-stu-id="2de3c-124">1. Add the Rocket Launcher prefab to the scene</span></span>

<span data-ttu-id="2de3c-125">Dans la fenêtre projet, accédez aux **ressources** > **MRTK. Tutoriels. GettingStarted** > **Prefabs** > dossier **RocketLauncher** , faites glisser le Prefab **RocketLauncher** dans la fenêtre hiérarchie pour l’ajouter à votre scène, puis placez-le à un emplacement approprié, par exemple :</span><span class="sxs-lookup"><span data-stu-id="2de3c-125">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** > **RocketLauncher** folder, drag the **RocketLauncher** prefab into the Hierarchy window to add it to your scene, and then position it at a suitable location, for example:</span></span>

* <span data-ttu-id="2de3c-126">Transformer la position X = 1,5, Y =-0,4, Z = 0, afin qu’elle soit positionnée à droite de l’utilisateur à la hauteur de la taille</span><span class="sxs-lookup"><span data-stu-id="2de3c-126">Transform Position X = 1.5, Y = -0.4, Z = 0, so it is positioned to the right of the user at waist height</span></span>
* <span data-ttu-id="2de3c-127">Transform rotation X = 0, Y = 180, Z = 0, les principales fonctionnalités de l’expérience sont-elles l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2de3c-127">Transform Rotation X = 0, Y = 180, Z = 0, so the main features of the experience faces the user</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step1-1.png)

### <a name="2-enable-object-manipulation-for-all-the-parts"></a><span data-ttu-id="2de3c-129">2. activer la manipulation d’objets pour toutes les parties</span><span class="sxs-lookup"><span data-stu-id="2de3c-129">2. Enable object manipulation for all the parts</span></span>

<span data-ttu-id="2de3c-130">Dans la fenêtre hiérarchie, localisez l’objet RocketLauncher > **LunarModuleParts** et sélectionnez tous les **objets enfants**, ajoutez le composant de **Gestionnaire de manipulation (script)** et le composant de script (script) à **proximité d’interaction** , puis configurez le gestionnaire de manipulation (script) comme suit :</span><span class="sxs-lookup"><span data-stu-id="2de3c-130">In the Hierarchy window, locate the RocketLauncher > **LunarModuleParts** object and select all the **child objects**, add the **Manipulation Handler (Script)** component and the **Near Interaction Grabbable (Script)** component, and then configure the Manipulation Handler (Script) as follows:</span></span>

* <span data-ttu-id="2de3c-131">Modifier **deux types de manipulations de droitier** pour déplacer la rotation afin que la mise à l’échelle soit désactivée</span><span class="sxs-lookup"><span data-stu-id="2de3c-131">Change **Two Handed Manipulation Type** to Move Rotate so scaling is disabled</span></span>
* <span data-ttu-id="2de3c-132">Désactivez la case à cocher **autoriser la manipulation Far** pour autoriser uniquement l’interaction proche.</span><span class="sxs-lookup"><span data-stu-id="2de3c-132">Un-check the **Allow Far Manipulation** checkbox to only allow near interaction</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step1-2.png)

> [!TIP]
> <span data-ttu-id="2de3c-134">Pour obtenir un rappel, avec des instructions pas à pas sur la façon d’implémenter la manipulation d’objets, vous pouvez consulter les instructions sur la [manipulation d’objets 3D](mrlearning-base-ch4.md#manipulating-3d-objects) .</span><span class="sxs-lookup"><span data-stu-id="2de3c-134">For a reminder, with step by step instructions, on how to implement object manipulation, you can refer to the [Manipulating 3D Objects](mrlearning-base-ch4.md#manipulating-3d-objects) instructions.</span></span>

### <a name="3-add-and-configure-the-part-assembly-demo-script-component"></a><span data-ttu-id="2de3c-135">3. Ajouter et configurer le composant de démonstration d’assembly d’un composant (script)</span><span class="sxs-lookup"><span data-stu-id="2de3c-135">3. Add and configure the Part Assembly Demo (Script) component</span></span>

<span data-ttu-id="2de3c-136">Avec tous les objets enfants LunarModuleParts toujours sélectionnés, ajoutez un composant **audio source** , puis configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="2de3c-136">With all the LunarModuleParts child objects still selected, add an **Audio Source** component and then configure it as follows:</span></span>

* <span data-ttu-id="2de3c-137">Affectez un clip audio approprié au champ **Audioclip** , par exemple, MRKT_Scale_Start</span><span class="sxs-lookup"><span data-stu-id="2de3c-137">Assign a suitable audio clip to the **AudioClip** field, for example, MRKT_Scale_Start</span></span>
* <span data-ttu-id="2de3c-138">Désactivez la case à cocher **lire sur éveil** , afin que le clip audio ne soit pas automatiquement lu lors du chargement de la scène.</span><span class="sxs-lookup"><span data-stu-id="2de3c-138">Un-check the **Play On Awake** checkbox, so the audio clip does not automatically play when the scene loads</span></span>
* <span data-ttu-id="2de3c-139">Remplacez **spatial Blend** par 1 pour activer l’audio spatial</span><span class="sxs-lookup"><span data-stu-id="2de3c-139">Change **Spatial Blend** to 1, to enable spatial audio</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-1.png)

<span data-ttu-id="2de3c-141">Après avoir sélectionné tous les objets enfants LunarModuleParts, ajoutez le composant de **démonstration de l’assembly de composant (script)** :</span><span class="sxs-lookup"><span data-stu-id="2de3c-141">With all the LunarModuleParts child objects still selected, add the **Part Assembly Demo  (Script)** component:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-2.png)

<span data-ttu-id="2de3c-143">Dans la fenêtre hiérarchie, sélectionnez l’objet **RoverEnclosure** et configurez son composant de **démonstration d’assembly (script)** comme suit :</span><span class="sxs-lookup"><span data-stu-id="2de3c-143">In the Hierarchy window, select the **RoverEnclosure** object and configure its **Part Assembly Demo (Script)** component as follows:</span></span>

* <span data-ttu-id="2de3c-144">Pour le champ **objet à placer** , assignez l’objet lui-même, dans ce cas, l’objet **RoverEnclosure**</span><span class="sxs-lookup"><span data-stu-id="2de3c-144">To the **Object To Place** field, assign the object itself, in this case, the **RoverEnclosure** object</span></span>
* <span data-ttu-id="2de3c-145">Dans le champ **emplacement à placer** , assignez l’objet PlacementHints correspondant, dans ce cas, l’objet **RoverEnclosure_PlacementHints**</span><span class="sxs-lookup"><span data-stu-id="2de3c-145">To the **Location To Place** field, assign the corresponding PlacementHints object, in this case, the **RoverEnclosure_PlacementHints** object</span></span>
* <span data-ttu-id="2de3c-146">Dans le champ **objet d’info-bulle** , assignez le ToolTipObject correspondant, dans ce cas, l’objet **RoverEnclosure_ToolTip**</span><span class="sxs-lookup"><span data-stu-id="2de3c-146">To the **Tool Tip Object** field, assign the corresponding ToolTipObject, in this case, the **RoverEnclosure_ToolTip** object</span></span>
* <span data-ttu-id="2de3c-147">Dans le champ **source audio** , assignez l’objet lui-même, dans ce cas, l’objet **RoverEnclosure**</span><span class="sxs-lookup"><span data-stu-id="2de3c-147">To the **Audio Source** field, assign the object itself, in this case, the **RoverEnclosure** object</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-3.png)

<span data-ttu-id="2de3c-149">**Répétez cette opération** pour chacun des autres objets enfants LunarModuleParts, C.-à-d. FuelTank, EnergyCell, DockingPortal et ExternalSensor.</span><span class="sxs-lookup"><span data-stu-id="2de3c-149">**Repeat** for each of the other LunarModuleParts child objects, i.e. FuelTank, EnergyCell, DockingPortal, and ExternalSensor.</span></span>

<span data-ttu-id="2de3c-150">Si vous passez maintenant en mode jeu et que vous déplacez un « objet à placer » proche de son emplacement correspondant à l’emplacement de destination, vous remarquerez que :</span><span class="sxs-lookup"><span data-stu-id="2de3c-150">If you now enter Game mode and move an 'Object To Place' close to it's corresponding 'Location To Place' you will notice:</span></span>

* <span data-ttu-id="2de3c-151">L’objet sera mis en place et sera apparenté sous l’objet LunarModule afin qu’il fasse partie du module lunaire</span><span class="sxs-lookup"><span data-stu-id="2de3c-151">The object will snap into place and be parented under the LunarModule object so it becomes part of the Lunar Module</span></span>
* <span data-ttu-id="2de3c-152">La source audio sur l’objet lira le clip audio affecté à l’emplacement de l’objet.</span><span class="sxs-lookup"><span data-stu-id="2de3c-152">The Audio Source on the object will play the assigned Audio Clip at the location of the object</span></span>
* <span data-ttu-id="2de3c-153">L’objet d’info-bulle correspondant sera masqué</span><span class="sxs-lookup"><span data-stu-id="2de3c-153">The corresponding Tool Tip object will be hidden</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-4.png)

> [!TIP]
> <span data-ttu-id="2de3c-155">Pour obtenir un rappel sur l’utilisation de la simulation d’entrée dans l’éditeur, vous pouvez vous reporter au [à l’aide de la simulation d’entrée de l’éditeur pour tester un](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) Guide de scène dans le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="2de3c-155">For a reminder on how to use the in-editor input simulation, you can refer to the [Using the In-Editor Hand Input Simulation to test a scene](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="configuring-the-lunar-module"></a><span data-ttu-id="2de3c-156">Configuration du module lunaire</span><span class="sxs-lookup"><span data-stu-id="2de3c-156">Configuring the Lunar Module</span></span>

<span data-ttu-id="2de3c-157">Dans cette section, vous allez ajouter des fonctionnalités supplémentaires à l’application du lanceur Rocket afin que l’utilisateur puisse :</span><span class="sxs-lookup"><span data-stu-id="2de3c-157">In this section, you will add additional features to the Rocket Launcher application so the user can:</span></span>

* <span data-ttu-id="2de3c-158">Interagir avec le module lunaire</span><span class="sxs-lookup"><span data-stu-id="2de3c-158">Interact with the Lunar Module</span></span>
* <span data-ttu-id="2de3c-159">Lancer le module lunaire dans l’espace et émettre un signal sonore lorsqu’il est lancé</span><span class="sxs-lookup"><span data-stu-id="2de3c-159">Launch the Lunar Module into space and play a sound when it is launched</span></span>
* <span data-ttu-id="2de3c-160">Réinitialisation de l’application pour que le module lunaire et tout le composant soient remis à leur position d’origine</span><span class="sxs-lookup"><span data-stu-id="2de3c-160">Reset the application so the Lunar Module and all the part are placed back to their original position</span></span>
* <span data-ttu-id="2de3c-161">Masquez les indicateurs de placement pour compliquer le défi de l’assembly du composant.</span><span class="sxs-lookup"><span data-stu-id="2de3c-161">Hide the placement hints to make the part assembly challenge more difficult.</span></span>

<span data-ttu-id="2de3c-162">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="2de3c-162">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="2de3c-163">Activer la manipulation d’objets</span><span class="sxs-lookup"><span data-stu-id="2de3c-163">Enable object manipulation</span></span>
2. <span data-ttu-id="2de3c-164">Activer la physique</span><span class="sxs-lookup"><span data-stu-id="2de3c-164">Enable physics</span></span>
3. <span data-ttu-id="2de3c-165">Ajouter un composant source audio</span><span class="sxs-lookup"><span data-stu-id="2de3c-165">Add an Audio Source component</span></span>
4. <span data-ttu-id="2de3c-166">Ajouter et configurer le composant Launch lunaire module (script)</span><span class="sxs-lookup"><span data-stu-id="2de3c-166">Add and configure the Launch Lunar Module (Script) component</span></span>
5. <span data-ttu-id="2de3c-167">Ajouter et configurer le composant activer/désactiver les indicateurs de positionnement (script)</span><span class="sxs-lookup"><span data-stu-id="2de3c-167">Add and configure the Toggle Placement Hints (Script) component</span></span>

> [!NOTE]
> <span data-ttu-id="2de3c-168">Le composant Launch lunaire module (script) et le composant indicateurs de positionnement Toggle (script) ne font pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="2de3c-168">The Launch Lunar Module (Script) component and the Toggle Placement Hints (Script) component are not part of MRTK.</span></span> <span data-ttu-id="2de3c-169">Ils ont été fournis avec les ressources de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2de3c-169">They were provided with this tutorial's assets.</span></span>

### <a name="1-enable-object-manipulation"></a><span data-ttu-id="2de3c-170">1. activer la manipulation d’objets</span><span class="sxs-lookup"><span data-stu-id="2de3c-170">1. Enable object manipulation</span></span>

<span data-ttu-id="2de3c-171">Dans la fenêtre hiérarchie, sélectionnez l’objet RocketLauncher > **LunarModule** , ajoutez le composant de **Gestionnaire de manipulation (script)** et le composant de script (script) à proximité de l' **interaction** , puis configurez le gestionnaire de manipulation (script) comme suit :</span><span class="sxs-lookup"><span data-stu-id="2de3c-171">In the Hierarchy window, select the RocketLauncher > **LunarModule** object, add the **Manipulation Handler (Script)** component and the **Near Interaction Grabbable (Script)** component, and then configure the Manipulation Handler (Script) as follows:</span></span>

* <span data-ttu-id="2de3c-172">Modifier **deux types de manipulations de droitier** pour déplacer la rotation afin que la mise à l’échelle soit désactivée</span><span class="sxs-lookup"><span data-stu-id="2de3c-172">Change **Two Handed Manipulation Type** to Move Rotate so scaling is disabled</span></span>
* <span data-ttu-id="2de3c-173">Désactivez la case à cocher **autoriser la manipulation Far** pour autoriser uniquement l’interaction proche.</span><span class="sxs-lookup"><span data-stu-id="2de3c-173">Un-check the **Allow Far Manipulation** checkbox to only allow near interaction</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step1-1.png)

### <a name="2-enable-physics"></a><span data-ttu-id="2de3c-175">2. activer la physique</span><span class="sxs-lookup"><span data-stu-id="2de3c-175">2. Enable physics</span></span>

<span data-ttu-id="2de3c-176">Avec l’objet RocketLauncher > **LunarModule** toujours sélectionné, ajoutez un composant RigidBody, puis configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="2de3c-176">With the RocketLauncher > **LunarModule** object still selected, add a Rigidbody component and then configure it as follows:</span></span>

* <span data-ttu-id="2de3c-177">Désactivez la case à cocher **utiliser la gravité** pour que le module lunaire ne soit pas affecté par la gravité</span><span class="sxs-lookup"><span data-stu-id="2de3c-177">Un-check the **Use Gravity** checkbox so the Lunar Module is not affected by gravity</span></span>
* <span data-ttu-id="2de3c-178">Cochez la case **est cinématique** pour que le module lunaire ne soit pas affecté initialement par les forces physico-</span><span class="sxs-lookup"><span data-stu-id="2de3c-178">Check the **Is Kinematic** checkbox so the Lunar Module initially isn't affected by physic forces</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step2-1.png)

### <a name="3-add-an-audio-source-component"></a><span data-ttu-id="2de3c-180">3. Ajouter un composant source audio</span><span class="sxs-lookup"><span data-stu-id="2de3c-180">3. Add an Audio Source component</span></span>

<span data-ttu-id="2de3c-181">Avec l’objet RocketLauncher > **LunarModule** toujours sélectionné, ajoutez un composant **audio source** , puis configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="2de3c-181">With the RocketLauncher > **LunarModule** object still selected, add an **Audio Source** component and then configure it as follows:</span></span>

* <span data-ttu-id="2de3c-182">Remplacez **spatial Blend** par 1 pour activer l’audio spatial</span><span class="sxs-lookup"><span data-stu-id="2de3c-182">Change **Spatial Blend** to 1 to enable spatial audio</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step3-1.png)

### <a name="4-add-and-configure-the-launch-lunar-module-script-component"></a><span data-ttu-id="2de3c-184">4. Ajouter et configurer le composant Launch lunaire module (script)</span><span class="sxs-lookup"><span data-stu-id="2de3c-184">4. Add and configure the Launch Lunar Module (Script) component</span></span>

<span data-ttu-id="2de3c-185">Avec l’objet RocketLauncher > **LunarModule** toujours sélectionné, ajoutez le composant **Launch lunaire module (script)** , puis configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="2de3c-185">With the RocketLauncher > **LunarModule** object still selected, add the **Launch Lunar Module (Script)** component and then configure it as follows:</span></span>

* <span data-ttu-id="2de3c-186">Modifiez la valeur de **Poussée** afin que le module lunaire se déplacera correctement au lancement, par exemple, à 0,01</span><span class="sxs-lookup"><span data-stu-id="2de3c-186">Change **Thrust** value so the Lunar Module will fly up gracefully when launched, for example, to 0.01</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step4-1.png)

### <a name="5-add-and-configure-the-toggle-placement-hints-script-component"></a><span data-ttu-id="2de3c-188">5. Ajouter et configurer le composant activer/désactiver les indicateurs de positionnement (script)</span><span class="sxs-lookup"><span data-stu-id="2de3c-188">5. Add and configure the Toggle Placement Hints (Script) component</span></span>

<span data-ttu-id="2de3c-189">Avec l’objet RocketLauncher > **LunarModule** toujours sélectionné, ajoutez le composant **activer/désactiver les indicateurs de positionnement (script)** , puis configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="2de3c-189">With the RocketLauncher > **LunarModule** object still selected, add the **Toggle Placement Hints (Script)** component and then configure it as follows:</span></span>

* <span data-ttu-id="2de3c-190">Affectez à la propriété **taille** du tableau d’objets de jeu la valeur 5</span><span class="sxs-lookup"><span data-stu-id="2de3c-190">Set the Game Object Array **Size** property to 5</span></span>
* <span data-ttu-id="2de3c-191">Affectez chacun des **objets enfants** de l’objet **PlacementHints** à un champ d' **élément** dans le tableau d’objets de jeu :</span><span class="sxs-lookup"><span data-stu-id="2de3c-191">Assign each of the **PlacementHints** object's **child objects** to the an **Element** field in the Game Object Array:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step5-1.png)

## <a name="configuring-the-launch-button"></a><span data-ttu-id="2de3c-193">Configuration du bouton de lancement</span><span class="sxs-lookup"><span data-stu-id="2de3c-193">Configuring the Launch button</span></span>

<span data-ttu-id="2de3c-194">Dans la fenêtre hiérarchie, sélectionnez les boutons de > RocketLauncher > objet **LaunchButton** , puis sur le composant **bouton enfoncé (script)** , créez un événement **bouton appuyé ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **LaunchLunarModule. StartThruster** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="2de3c-194">In the Hierarchy window, select the RocketLauncher > Buttons > **LaunchButton** object, then on the **Pressable Button (Script)** component, create a new **Button Pressed ()** event, configure the **LunarModule** object to receive the event, and define **LaunchLunarModule.StartThruster** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-1.png)

> [!TIP]
> <span data-ttu-id="2de3c-196">Pour obtenir un rappel sur la façon d’implémenter des événements, vous pouvez consulter les instructions de suivi de la [main et les boutons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) interactifs.</span><span class="sxs-lookup"><span data-stu-id="2de3c-196">For a reminder on how to implement events, you can refer to the [Hand tracking gestures and interactable buttons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) instructions.</span></span>

<span data-ttu-id="2de3c-197">À l’aide des boutons de > RocketLauncher > objet **LaunchButton** toujours sélectionné, sur le composant **bouton appuyé (script)** , créez un événement **bouton enfoncé ()** , configurez l’objet **LunarModule** pour recevoir l’événement, définissez **audiosource. PlayOneShot** comme action à déclencher et affectez un clip audio approprié au champ de **clip** audio, par exemple, le clip audio MRTK_Gem :</span><span class="sxs-lookup"><span data-stu-id="2de3c-197">With the RocketLauncher > Buttons > **LaunchButton** object still selected, on the **Pressable Button (Script)** component, create a new **Button Pressed ()** event, configure the **LunarModule** object to receive the event, define **AudioSource.PlayOneShot** as the action to be triggered, and assign a suitable audio clip to the **Audio Clip** field, for example, the MRTK_Gem audio clip:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-2.png)

<span data-ttu-id="2de3c-199">À l’aide des boutons de > RocketLauncher > objet **LaunchButton** toujours sélectionné, sur le composant bouton de l' **option (script)** , créez un événement de **fin tactile ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **LaunchLunarModule. StopThruster** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="2de3c-199">With the RocketLauncher > Buttons > **LaunchButton** object still selected, on the **Pressable Button (Script)** component, create a new **Touch Ended ()** event, configure the **LunarModule** object to receive the event, and define **LaunchLunarModule.StopThruster** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-3.png)

<span data-ttu-id="2de3c-201">Si vous entrez maintenant le mode jeu et que vous appuyez sur le bouton de lancement, vous entendez le clip audio, et si vous maintenez le bouton de lancement enfoncé pendant environ une seconde ou plus, vous verrez le lancement du module lunaire dans l’espace :</span><span class="sxs-lookup"><span data-stu-id="2de3c-201">If you now enter Game mode and press the Launch button, you will hear the audio clip play, and if you hold the Launch button down for about a second or longer, you will see the Lunar Module launch into space:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-4.png)

## <a name="configuring-the-reset-button"></a><span data-ttu-id="2de3c-203">Configuration du bouton de réinitialisation</span><span class="sxs-lookup"><span data-stu-id="2de3c-203">Configuring the Reset button</span></span>

<span data-ttu-id="2de3c-204">Dans la fenêtre hiérarchie, sélectionnez les boutons de > RocketLauncher > objet **ResetButton** , puis sur le composant **bouton enfoncé (script)** , créez un événement **bouton appuyé ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **LaunchLunarModule. ResetModule** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="2de3c-204">In the Hierarchy window, select the RocketLauncher > Buttons > **ResetButton** object, then on the **Pressable Button (Script)** component, create a new **Button Pressed ()** event, configure the **LunarModule** object to receive the event, and define **LaunchLunarModule.ResetModule** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section4-step1-1.png)

<span data-ttu-id="2de3c-206">À l’aide des boutons de > RocketLauncher > objet **ResetButton** toujours sélectionné, sur le composant **bouton appuyé (script)** , créez un événement **bouton enfoncé ()** , configurez l’objet **RocketLauncher** pour recevoir l’événement, définissez **GameObject. BroadcastMessage** comme action à déclencher, puis entrez **ResetPlacement** dans le champ message :</span><span class="sxs-lookup"><span data-stu-id="2de3c-206">With the RocketLauncher > Buttons > **ResetButton** object still selected, on the **Pressable Button (Script)** component, create a new **Button Pressed ()** event, configure the **RocketLauncher** object to receive the event, define **GameObject.BroadcastMessage** as the action to be triggered, and enter **ResetPlacement** in message field:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section4-step1-2.png)

> [!TIP]
> <span data-ttu-id="2de3c-208">L’action GameObject. BroadcastMessage envoie le message ResetPlacement de l’objet RocketLauncher à tous ses objets enfants.</span><span class="sxs-lookup"><span data-stu-id="2de3c-208">The GameObject.BroadcastMessage action sends the ResetPlacement message from the RocketLauncher object to all its child object.</span></span> <span data-ttu-id="2de3c-209">Tout objet enfant qui a la fonction ResetPlacement, qui est définie dans le composant de démonstration d’assembly d’élément (script) que vous avez ajouté à tous les objets enfants LunarModuleParts, appellera la fonction ResetPlacement qui réinitialise le placement de cet objet enfant.</span><span class="sxs-lookup"><span data-stu-id="2de3c-209">Any child object that has the ResetPlacement function, which is defined in the Part Assembly Demo (Script) component you added to all the LunarModuleParts child object, will invoke the ResetPlacement function which resets that child object's placement.</span></span>

<span data-ttu-id="2de3c-210">Si vous entrez maintenant le mode jeu et que vous appuyez sur le bouton de réinitialisation, vous entendez le clip audio en cours de lecture et vous voyez le module lunaire en cours de lancement dans l’espace :</span><span class="sxs-lookup"><span data-stu-id="2de3c-210">If you now enter Game mode and press the Reset button you will hear the audio clip being played and see the Lunar Module being launched into space:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section4-step1-3.png)

## <a name="configuring-the-placement-hints-button"></a><span data-ttu-id="2de3c-212">Configuration du bouton indicateurs de positionnement</span><span class="sxs-lookup"><span data-stu-id="2de3c-212">Configuring the Placement Hints button</span></span>
<!-- TODO: Rename to 'Configuring the Hints button'-->

<span data-ttu-id="2de3c-213">Dans la fenêtre hiérarchie, sélectionnez les boutons de > RocketLauncher > objet **HintsButton** , puis sur le composant **bouton enfoncé (script)** , créez un événement **bouton appuyé ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **TogglePlacementHints. ToggleGameObjects** l’action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="2de3c-213">In the Hierarchy window, select the RocketLauncher > Buttons > **HintsButton** object, then on the **Pressable Button (Script)** component, create a new **Button Pressed ()** event, configure the **LunarModule** object to receive the event, and define **TogglePlacementHints.ToggleGameObjects** the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section5-step1-1.png)

<span data-ttu-id="2de3c-215">Si vous passez maintenant en mode jeu, vous remarquerez que les indicateurs d’emplacement translucides sont désactivés par défaut, mais que vous pouvez les activer et les désactiver en appuyant sur le bouton indicateurs :</span><span class="sxs-lookup"><span data-stu-id="2de3c-215">If you now enter Game mode you will notice that the translucent placement hints are disabled by default, but that you can toggle them on and off by pressing the Hints button:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial6-section5-step1-2.png)

## <a name="congratulations"></a><span data-ttu-id="2de3c-217">Félicitations</span><span class="sxs-lookup"><span data-stu-id="2de3c-217">Congratulations</span></span>

<span data-ttu-id="2de3c-218">Vous avez entièrement configuré cette application.</span><span class="sxs-lookup"><span data-stu-id="2de3c-218">You have fully configured this application.</span></span> <span data-ttu-id="2de3c-219">Désormais, votre application permet aux utilisateurs d’assembler entièrement le module lunaire, de lancer le module lunaire, de basculer les indicateurs et de réinitialiser l’application pour redémarrer.</span><span class="sxs-lookup"><span data-stu-id="2de3c-219">Now, your application allows users to fully assemble the Lunar Module, launch the Lunar Module, toggle hints, and reset the application to start again.</span></span>
