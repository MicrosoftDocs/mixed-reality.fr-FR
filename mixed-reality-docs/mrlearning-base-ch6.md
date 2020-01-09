---
title: Didacticiels de mise en route-7. Création d’un exemple d’application de module lunaire
description: Dans cette leçon, vous allez combiner plusieurs concepts appris dans les leçons précédentes pour créer un exemple d’expérience unique.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 3127ffceea08202fe9d978ad77f8fddb6fba60a3
ms.sourcegitcommit: 23b130d03fea46a50a712b8301fe4e5deed6cf9c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2019
ms.locfileid: "75334373"
---
# <a name="7-creating-a-lunar-module-sample-application"></a><span data-ttu-id="68442-105">7. création d’un exemple d’application de module lunaire</span><span class="sxs-lookup"><span data-stu-id="68442-105">7. Creating a Lunar Module sample application</span></span>

<span data-ttu-id="68442-106">Dans ce didacticiel, plusieurs concepts sont combinés à partir de leçons précédentes pour créer un exemple d’expérience unique.</span><span class="sxs-lookup"><span data-stu-id="68442-106">In this tutorial, multiple concepts are combined from previous lessons to create a unique sample experience.</span></span> <span data-ttu-id="68442-107">Vous allez apprendre à créer une application d’assembly de module lunaire permettant à un utilisateur d’utiliser des mains suivies pour récupérer des parties du module lunaire et tenter d’assembler un module lunaire.</span><span class="sxs-lookup"><span data-stu-id="68442-107">You will learn how to create a lunar module assembly application whereby a user needs to use tracked hands to pick up lunar module parts and attempt to assemble a lunar module.</span></span> <span data-ttu-id="68442-108">Nous utilisons des boutons permettant de basculer les indicateurs de placement, de réinitialiser notre expérience et de lancer notre module lunaire dans l’espace !</span><span class="sxs-lookup"><span data-stu-id="68442-108">We use pressable buttons to toggle placement hints, to reset our experience, and to launch our lunar module into space!</span></span> <span data-ttu-id="68442-109">Dans les prochains didacticiels, nous continuerons à développer cette expérience, qui comprend des cas d’utilisation multi-utilisateurs puissants qui tirent parti des ancres spatiales Azure pour l’alignement spatial.</span><span class="sxs-lookup"><span data-stu-id="68442-109">In future tutorials, we will continue to build upon this experience, which includes powerful multi-user use cases that leverage Azure Spatial Anchors for spatial alignment.</span></span>

## <a name="objectives"></a><span data-ttu-id="68442-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="68442-110">Objectives</span></span>

- <span data-ttu-id="68442-111">Combiner plusieurs concepts issus des leçons précédentes pour créer une même expérience</span><span class="sxs-lookup"><span data-stu-id="68442-111">Combine multiple concepts from previous lessons to create a unique experience</span></span>
- <span data-ttu-id="68442-112">Découvrir comment activer/désactiver des objets</span><span class="sxs-lookup"><span data-stu-id="68442-112">Learn how to toggle objects</span></span>
- <span data-ttu-id="68442-113">Déclencher des événements complexes en utilisant des boutons enfonçables</span><span class="sxs-lookup"><span data-stu-id="68442-113">Trigger complex events using pressable buttons</span></span>
- <span data-ttu-id="68442-114">Utiliser la physique et les forces des corps rigides</span><span class="sxs-lookup"><span data-stu-id="68442-114">Use rigidbody physics and forces</span></span>
- <span data-ttu-id="68442-115">Explorer l’utilisation d’info-bulles</span><span class="sxs-lookup"><span data-stu-id="68442-115">Explore the use of tool tips</span></span>

## <a name="configuring-the-lunar-module"></a><span data-ttu-id="68442-116">Configuration du module lunaire</span><span class="sxs-lookup"><span data-stu-id="68442-116">Configuring the Lunar Module</span></span>

<span data-ttu-id="68442-117">Dans cette section, nous présentons les différents composants nécessaires pour créer notre exemple d’expérience.</span><span class="sxs-lookup"><span data-stu-id="68442-117">In this section, we introduce the various components needed to create our sample experience.</span></span>

1. <span data-ttu-id="68442-118">Ajoutez l’assembly de module lunaire Prefab à votre scène de base.</span><span class="sxs-lookup"><span data-stu-id="68442-118">Add the Lunar Module Assembly prefab to your base scene.</span></span> <span data-ttu-id="68442-119">Pour ce faire, sous l’onglet projet, accédez à ressources > BaseModuleAssets > Prefabs.</span><span class="sxs-lookup"><span data-stu-id="68442-119">To do this, in the Project tab navigate to Assets > BaseModuleAssets > Prefabs.</span></span> <span data-ttu-id="68442-120">Vous verrez deux prefabs de lanceur fusée, faire glisser la Prefab Rocket Launcher_Tutorial dans votre scène et la positionner comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="68442-120">You will see two rocket launcher prefabs, drag the Rocket Launcher_Tutorial prefab into your scene, and position as you wish.</span></span>

    >[!NOTE]
    ><span data-ttu-id="68442-121">Le Prefab Rocket Launcher_Complete est le lanceur terminé, fourni à des fins de référence.</span><span class="sxs-lookup"><span data-stu-id="68442-121">The Rocket Launcher_Complete prefab is the completed launcher, provided for reference.</span></span>

    ![Lesson6 Chapter1 Step1im](images/Lesson6_Chapter1_step1im.PNG)

    <span data-ttu-id="68442-123">Si vous développez l’objet de jeu de fusée Launcher_Tutorial dans votre hiérarchie et que vous développez davantage l’objet de module lunaire, vous trouverez plusieurs objets enfants qui ont un matériau appelé « x-ray ».</span><span class="sxs-lookup"><span data-stu-id="68442-123">If you expand the Rocket Launcher_Tutorial game object in your hierarchy and further expand the Lunar Module object, you find several child objects that have a material called "x-ray."</span></span> <span data-ttu-id="68442-124">Le matériau « x-ray » autorise une couleur légèrement translucide qui sera utilisée comme indicateurs de placement pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="68442-124">The "x-ray" material allows for a slightly translucent color that will be used as placement hints for the user.</span></span>

    ![Lesson6 fichier chapter1 Noteaim](images/Lesson6_Chapter1_noteaim.PNG)

    <span data-ttu-id="68442-126">Le module lunaire utilise cinq parties avec lesquelles l’utilisateur interagit, comme illustré dans l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="68442-126">There are five parts to the lunar module that the user will interact with, as shown in the image below:</span></span>

    1. <span data-ttu-id="68442-127">Le boîtier du rover (Rover Enclosure)</span><span class="sxs-lookup"><span data-stu-id="68442-127">The Rover Enclosure</span></span>
    2. <span data-ttu-id="68442-128">Le réservoir de carburant (Fuel Tank)</span><span class="sxs-lookup"><span data-stu-id="68442-128">The Fuel Tank</span></span>
    3. <span data-ttu-id="68442-129">La batterie (Energy Cell)</span><span class="sxs-lookup"><span data-stu-id="68442-129">The Energy Cell</span></span>
    4. <span data-ttu-id="68442-130">Le portail d’accueil (Docking Portal)</span><span class="sxs-lookup"><span data-stu-id="68442-130">The Docking Portal</span></span>
    5. <span data-ttu-id="68442-131">Le capteur externe (External sensor)</span><span class="sxs-lookup"><span data-stu-id="68442-131">The External sensor</span></span>

    ![Lesson6 Chapter1 Notebim](images/Lesson6_Chapter1_notebim.PNG)

    >[!NOTE]
    ><span data-ttu-id="68442-133">Les noms des objets de jeu que vous voyez dans la hiérarchie de votre scène de base ne correspondent pas aux noms des objets dans la scène.</span><span class="sxs-lookup"><span data-stu-id="68442-133">The game object names that you see in your base scene hierarchy do not correspond to the names of the objects in the scene.</span></span>

2. <span data-ttu-id="68442-134">Ajoutez une source audio à l’objet de jeu LunarModule.</span><span class="sxs-lookup"><span data-stu-id="68442-134">Add an audio source to the LunarModule game object.</span></span> <span data-ttu-id="68442-135">Assurez-vous que LunarModule est sélectionné dans votre hiérarchie de scènes, puis cliquez sur Ajouter un composant.</span><span class="sxs-lookup"><span data-stu-id="68442-135">Make sure the LunarModule is selected in your scene hierarchy and click Add Component.</span></span> <span data-ttu-id="68442-136">Recherchez la source audio et ajoutez-la à l’objet de jeu.</span><span class="sxs-lookup"><span data-stu-id="68442-136">Search for Audio Source and add it to the game object.</span></span> <span data-ttu-id="68442-137">Laissez le champ AudioClip vide pour le moment, mais changez le paramètre spécial Blend de 0 en 1 pour activer l’audio spatial.</span><span class="sxs-lookup"><span data-stu-id="68442-137">Leave the AudioClip field blank for now, but change the Special Blend setting from 0 to 1 so to enable spatial audio.</span></span> <span data-ttu-id="68442-138">Vous allez utiliser cette source audio pour jouer un son de lancement plus tard.</span><span class="sxs-lookup"><span data-stu-id="68442-138">You will use this audio source to play the launching sound later.</span></span>

    ![Lesson6 fichier chapter1 Step2im](images/Lesson6_Chapter1_step2im.PNG)

3. <span data-ttu-id="68442-140">Ajoutez le script activer les indicateurs de positionnement.</span><span class="sxs-lookup"><span data-stu-id="68442-140">Add the script Toggle Placement Hints.</span></span> <span data-ttu-id="68442-141">Cliquez sur Ajouter un composant et recherchez les indicateurs de positionnement bascule.</span><span class="sxs-lookup"><span data-stu-id="68442-141">Click Add Component and search for Toggle Placement Hints.</span></span> <span data-ttu-id="68442-142">Il s’agit d’un script personnalisé qui vous permet d’activer et de désactiver les indicateurs translucides (objets avec la matière de rayons x), comme mentionné précédemment.</span><span class="sxs-lookup"><span data-stu-id="68442-142">This is a custom script that lets you turn on and off the translucent hints (objects with the x-ray material), as mentioned earlier.</span></span>

    ![Lesson6 fichier chapter1 Step3im](images/Lesson6_Chapter1_step3im.PNG)

4. <span data-ttu-id="68442-144">Étant donné que nous avons cinq objets, tapez « 5 » pour la taille du tableau d’objets de jeu.</span><span class="sxs-lookup"><span data-stu-id="68442-144">Since we have five objects, type "5" for the game object array size.</span></span> <span data-ttu-id="68442-145">Vous verrez alors cinq nouveaux éléments s’affichent.</span><span class="sxs-lookup"><span data-stu-id="68442-145">You will then see five new elements appear.</span></span>

    ![Lesson6 Chapter1 Step4bim](images/Lesson6_Chapter1_step4bim.PNG)

    <span data-ttu-id="68442-147">Faites glisser chacun des objets translucides dans toutes les zones Nom (objet de jeu).</span><span class="sxs-lookup"><span data-stu-id="68442-147">Drag each of the translucent objects into all the Name (Game Object) boxes.</span></span> <span data-ttu-id="68442-148">Faites glisser les objets suivants du module lunaire de votre scène vers les champs du tableau d’objets, comme indiqué dans l’image ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="68442-148">Drag the following objects from the lunar module in your scene into the object array fields as shown in the image above:</span></span>

    ![Lesson6 Chapter1 Step4aim](images/Lesson6_Chapter1_step4aim.PNG)

    <span data-ttu-id="68442-150">Le script activer/désactiver les indicateurs de positionnement est maintenant configuré, ce qui nous permet d’activer et de désactiver les indicateurs.</span><span class="sxs-lookup"><span data-stu-id="68442-150">The Toggle Placement Hints script is now configured, which allows us to turn hints on and off.</span></span>

5. <span data-ttu-id="68442-151">Ajoutez le script Launch lunaire module.</span><span class="sxs-lookup"><span data-stu-id="68442-151">Add the Launch Lunar Module script.</span></span> <span data-ttu-id="68442-152">Cliquez sur le bouton Ajouter un composant, recherchez « lancer le module lunaire » et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="68442-152">Click the Add Component button, search for "launch lunar module" and select it.</span></span> <span data-ttu-id="68442-153">Ce script lance le module lunaire.</span><span class="sxs-lookup"><span data-stu-id="68442-153">This script launches the lunar module.</span></span> <span data-ttu-id="68442-154">Quand vous appuyez sur un bouton configuré, il ajoute une force vers le haut au composant de corps rigide du module lunaire et provoque le lancement du module vers le haut.</span><span class="sxs-lookup"><span data-stu-id="68442-154">When we press a configured button, it adds an upward force to the lunar module's rigid body component and causes the module to launch upwards.</span></span> <span data-ttu-id="68442-155">Si vous êtes à l’intérieur, le module lunaire peut se crasher sur le maillage de votre plafond.</span><span class="sxs-lookup"><span data-stu-id="68442-155">If you are indoors, the lunar module may crash against your ceiling mesh.</span></span> <span data-ttu-id="68442-156">Si vous vous trouvez dans une zone avec des plafonds élevés ou aucun plafond, le module lunaire se déplacera indéfiniment dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="68442-156">If you are in an area with high ceilings or no ceilings, the lunar module will fly into space indefinitely.</span></span>

    ![Lesson6 Chapter1 Step5im](images/Lesson6_Chapter1_step5im.PNG)

6. <span data-ttu-id="68442-158">Ajustez la poussée afin que le module lunaire vole de façon fluide.</span><span class="sxs-lookup"><span data-stu-id="68442-158">Adjust the thrust so that the lunar module will fly up gracefully.</span></span> <span data-ttu-id="68442-159">Essayez une valeur de 0,01.</span><span class="sxs-lookup"><span data-stu-id="68442-159">Try a value of 0.01.</span></span> <span data-ttu-id="68442-160">Laissez le champ « Rb » vide.</span><span class="sxs-lookup"><span data-stu-id="68442-160">Leave the "Rb" field blank.</span></span> <span data-ttu-id="68442-161">RB représente le corps rigide et ce champ est automatiquement rempli lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="68442-161">Rb stands for Rigid body and this field will be automatically populated during runtime.</span></span>

    ![Lesson6 Chapter1 Step6im](images/Lesson6_Chapter1_step6im.PNG)

## <a name="lunar-module-parts-overview"></a><span data-ttu-id="68442-163">Vue d’ensemble des parties du module lunaire</span><span class="sxs-lookup"><span data-stu-id="68442-163">Lunar Module Parts overview</span></span>

<span data-ttu-id="68442-164">L’objet parent des composants de module lunaire est la collection des objets avec lesquels l’utilisateur interagit.</span><span class="sxs-lookup"><span data-stu-id="68442-164">The Lunar Module Parts parent object is the collection of the objects that the user interacts with.</span></span> <span data-ttu-id="68442-165">Les noms des objets de jeu avec des noms de scènes libellés entre parenthèses, sont fournis dans la liste ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="68442-165">The Game object names with scene labeled names in parentheses, are provided in the list below:</span></span>

- <span data-ttu-id="68442-166">Sac à dos (cellule Energy)</span><span class="sxs-lookup"><span data-stu-id="68442-166">Backpack (Energy Cell)</span></span>
- <span data-ttu-id="68442-167">GasTank (réservoir de carburant)</span><span class="sxs-lookup"><span data-stu-id="68442-167">GasTank (Fuel Tank)</span></span>
- <span data-ttu-id="68442-168">TopLeftBody (Rover Enclosure)</span><span class="sxs-lookup"><span data-stu-id="68442-168">TopLeftBody (Rover Enclosure)</span></span>
- <span data-ttu-id="68442-169">Nose (Docking Portal)</span><span class="sxs-lookup"><span data-stu-id="68442-169">Nose (Docking Portal)</span></span>
- <span data-ttu-id="68442-170">LeftTwirler (External Sensor)</span><span class="sxs-lookup"><span data-stu-id="68442-170">LeftTwirler (External Sensor)</span></span>

<span data-ttu-id="68442-171">Notez que chacun de ces objets a un gestionnaire de manipulation, comme expliqué dans la leçon 4.</span><span class="sxs-lookup"><span data-stu-id="68442-171">Notice that each of these objects has a manipulation handler, as explained in Lesson 4.</span></span> <span data-ttu-id="68442-172">Cette fonctionnalité permet aux utilisateurs de saisir et de manipuler l’objet.</span><span class="sxs-lookup"><span data-stu-id="68442-172">This feature enables users to grab and manipulate the object.</span></span> <span data-ttu-id="68442-173">Notez également que le paramètre, deux types de manipulation de la main, est défini sur déplacer et faire pivoter.</span><span class="sxs-lookup"><span data-stu-id="68442-173">Also note that the setting, Two Handed Manipulation Type, is set to Move and Rotate.</span></span> <span data-ttu-id="68442-174">Cette option permet uniquement à l’utilisateur de déplacer l’objet sans modifier sa taille, ce qui est la fonctionnalité souhaitée pour une application d’assembly.</span><span class="sxs-lookup"><span data-stu-id="68442-174">This option only permits the user to move the object and not change its size, which is the desired functionality for an assembly application.</span></span>
<span data-ttu-id="68442-175">En outre, la manipulation Far n’est pas vérifiée pour autoriser uniquement l’interaction directe des parties de module.</span><span class="sxs-lookup"><span data-stu-id="68442-175">In addition, Far Manipulation is unchecked to allow only for direct interaction of module parts.</span></span>

![Lesson6 Chapter2im](images/Lesson6_Chapter2im.PNG)

<span data-ttu-id="68442-177">Le script de démonstration d’assembly d’un composant (illustré ci-dessus) est le script qui gère les objets que l’utilisateur place sur le module lunaire par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="68442-177">The Part Assembly Demo script (shown above) is the script that manages the objects that the user places on the lunar module by the user.</span></span>

<span data-ttu-id="68442-178">Le champ objet à placer est la transformation qui est sélectionnée, comme illustré dans l’image ci-dessus, le sac à dos/réservoir de carburant associé à l’objet auquel il se connecte.</span><span class="sxs-lookup"><span data-stu-id="68442-178">The Object To Place field is the transform that is selected, as shown in the image above, the backpack/fuel tank associated with the object that it connects to.</span></span>

<span data-ttu-id="68442-179">Les paramètres distance à distance et distance déterminent la proximité des composants qui sont en place ou peuvent être libérés.</span><span class="sxs-lookup"><span data-stu-id="68442-179">The Near Distance and Far Distance settings determine the proximity to which parts snap in place or can be released.</span></span> <span data-ttu-id="68442-180">Par exemple, le réservoir de sacs/carburants doit se trouver à 0,1 unités à l’extérieur du module lunaire pour pouvoir être placé en place.</span><span class="sxs-lookup"><span data-stu-id="68442-180">For example, the backpack/fuel tank needs to be 0.1 units away from the lunar module before it will snap into place.</span></span> <span data-ttu-id="68442-181">Le paramètre distance définit l’emplacement où l’objet peut être avant de se détacher du module lunaire.</span><span class="sxs-lookup"><span data-stu-id="68442-181">The Far Distance setting sets the location where the object can be before it can detach from the lunar module.</span></span> <span data-ttu-id="68442-182">Dans ce cas, la main de l’utilisateur doit saisir le sac à dos/réservoir et le tire à une distance de 0,2 unités du module lunaire pour le retirer de l’emplacement d’insertion et le remettre en place.</span><span class="sxs-lookup"><span data-stu-id="68442-182">In this case, the user’s hand must grab the backpack/fuel tank and pull it 0.2 units away from the lunar module to remove it from snapping back into place.</span></span>

<span data-ttu-id="68442-183">L’info-bulle est l’étiquette de l’info-bulle dans la scène.</span><span class="sxs-lookup"><span data-stu-id="68442-183">The Tool Tip Object is the tool tip label in the scene.</span></span> <span data-ttu-id="68442-184">Lorsque les objets sont alignés sur place, l’étiquette est désactivée.</span><span class="sxs-lookup"><span data-stu-id="68442-184">When the objects are snapped in place, the label is disabled.</span></span>

<span data-ttu-id="68442-185">La source audio est automatiquement saisie.</span><span class="sxs-lookup"><span data-stu-id="68442-185">The Audio Source is automatically grabbed.</span></span>

## <a name="configuring-the-placement-hints-button"></a><span data-ttu-id="68442-186">Configuration du bouton indicateurs de positionnement</span><span class="sxs-lookup"><span data-stu-id="68442-186">Configuring the Placement Hints button</span></span>

<span data-ttu-id="68442-187">Dans la [leçon 2](mrlearning-base-ch2.md), vous avez appris à placer et configurer des boutons permettant d’effectuer des opérations telles que modifier la couleur d’un élément ou faire en sorte qu’il émette un signal sonore lorsqu’il est poussé.</span><span class="sxs-lookup"><span data-stu-id="68442-187">In [Lesson 2](mrlearning-base-ch2.md), you learned how to place and configure buttons to do things like change the color of an item or make it play a sound when pushed.</span></span> <span data-ttu-id="68442-188">Nous allons continuer à utiliser ces principes pour configurer nos boutons permettant d’activer et de désactiver les indicateurs de placement.</span><span class="sxs-lookup"><span data-stu-id="68442-188">We will continue to use those principles as we configure our buttons for toggling placement hints.</span></span>

<span data-ttu-id="68442-189">L’objectif est de configurer notre bouton afin que chaque fois que l’utilisateur appuie sur le bouton d’indication de placement, il active ou désactive la visibilité des indicateurs de placement translucides.</span><span class="sxs-lookup"><span data-stu-id="68442-189">The goal is to configure our button so that every time the user presses the Placement hint button, it toggles the visibility of the translucent placement hints.</span></span>

1. <span data-ttu-id="68442-190">Déplacez le module lunaire vers l’emplacement vide du runtime uniquement dans le panneau Inspecteur, tandis que l’objet indicateur de positionnement est sélectionné dans votre hiérarchie de scènes de base.</span><span class="sxs-lookup"><span data-stu-id="68442-190">Move the lunar module to the empty Runtime Only slot in the inspector panel while the Placement Hints object is selected in your base scene hierarchy.</span></span>

    ![Lesson6 Chapter3 Step1im](images/Lesson6_Chapter3_step1im.PNG)

2. <span data-ttu-id="68442-192">Cliquez sur la liste déroulante aucune fonction.</span><span class="sxs-lookup"><span data-stu-id="68442-192">Click the No Function dropdown list.</span></span> <span data-ttu-id="68442-193">Accédez à TogglePlacementHints et sélectionnez ToggleGameObjects () sous ce menu.</span><span class="sxs-lookup"><span data-stu-id="68442-193">Go down to TogglePlacementHints and select ToggleGameObjects () under that menu.</span></span> <span data-ttu-id="68442-194">ToggleGameObjects () active ou désactive les indicateurs de positionnement afin qu’ils soient visibles ou invisibles à chaque fois que le bouton est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="68442-194">ToggleGameObjects() toggles the placement hints on and off so that they are visible or invisible each time the button is pressed.</span></span>

    ![Lesson6 Chapter3 Step2im](images/Lesson6_Chapter3_step2im.PNG)

## <a name="configuring-the-reset-button"></a><span data-ttu-id="68442-196">Configuration du bouton de réinitialisation</span><span class="sxs-lookup"><span data-stu-id="68442-196">Configuring the Reset button</span></span>

<span data-ttu-id="68442-197">Il y aura des situations où l’utilisateur fait une erreur, lève accidentellement l’objet à l’écart ou souhaite simplement réinitialiser l’expérience.</span><span class="sxs-lookup"><span data-stu-id="68442-197">There will be situations where the user makes a mistake, accidentally throws the object away or just wants to reset the experience.</span></span> <span data-ttu-id="68442-198">Le bouton Réinitialiser permet de relancer l’expérience.</span><span class="sxs-lookup"><span data-stu-id="68442-198">The Reset button adds the ability to restart the experience.</span></span>

1. <span data-ttu-id="68442-199">Sélectionnez le bouton Réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="68442-199">Select the Reset button.</span></span> <span data-ttu-id="68442-200">Dans la scène de base, elle est nommée ResetRoundButton.</span><span class="sxs-lookup"><span data-stu-id="68442-200">In the base scene, it’s named ResetRoundButton.</span></span>

2. <span data-ttu-id="68442-201">Faites glisser le module lunaire de la hiérarchie de la scène de base dans l’emplacement vide sous le bouton enfoncé dans le panneau de l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="68442-201">Drag the lunar module from the base scene hierarchy into the empty slot under Button Pressed on the inspector panel.</span></span>

    ![Lesson6 Chapter4 Step2im](images/Lesson6_Chapter4_step2im.PNG)

3. <span data-ttu-id="68442-203">Sélectionnez le menu déroulant aucune fonction et pointez sur LaunchLunarModule, puis sélectionnez resetModule ().</span><span class="sxs-lookup"><span data-stu-id="68442-203">Select the No Function dropdown menu and hover over LaunchLunarModule, then select resetModule ().</span></span>

    ![Lesson6 Chapter4 Step3im](images/Lesson6_Chapter4_step3im.PNG)

    >[!NOTE]
    ><span data-ttu-id="68442-205">Notez que, par défaut, GameObject. BroadcastMessage est configuré sur ResetPlacement.</span><span class="sxs-lookup"><span data-stu-id="68442-205">Notice that by default, the GameObject.BroadcastMessage is configured to ResetPlacement.</span></span> <span data-ttu-id="68442-206">Cela diffuse un message nommé ResetPlacement pour chaque objet enfant du RocketLauncher_Tutorial.</span><span class="sxs-lookup"><span data-stu-id="68442-206">This broadcasts a message named ResetPlacement for every child object of the RocketLauncher_Tutorial.</span></span> <span data-ttu-id="68442-207">Tout objet ayant une méthode pour ResetPlacement () répond à ce message en réinitialisant sa position.</span><span class="sxs-lookup"><span data-stu-id="68442-207">Any object that has a method for ResetPlacement() responds to that message by resetting it's position.</span></span>

## <a name="configuring-the-launch-button"></a><span data-ttu-id="68442-208">Configuration du bouton de lancement</span><span class="sxs-lookup"><span data-stu-id="68442-208">Configuring the Launch button</span></span>

<span data-ttu-id="68442-209">Cette section explique comment configurer le bouton de lancement, qui permet à l’utilisateur d’appuyer sur le bouton et de lancer le module lunaire dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="68442-209">This section explains how to configure the Launch button, which permits the user to press the button and launch the lunar module into space.</span></span>

1. <span data-ttu-id="68442-210">Sélectionnez le bouton lancer.</span><span class="sxs-lookup"><span data-stu-id="68442-210">Select the Launch button.</span></span> <span data-ttu-id="68442-211">Dans la scène de base, il s’agit de LaunchRoundButton.</span><span class="sxs-lookup"><span data-stu-id="68442-211">In the base scene, it’s called LaunchRoundButton.</span></span> <span data-ttu-id="68442-212">Faites glisser le module lunaire dans l’emplacement vide sous Touch end dans le panneau de l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="68442-212">Drag the lunar module to the empty slot under Touch End in the Inspector panel.</span></span>

    ![Lesson6 Chapter5 Step1im](images/Lesson6_Chapter5_step1im.PNG)

2. <span data-ttu-id="68442-214">Sélectionnez le menu déroulant no Function et pointez sur LaunchLunarModule, puis sélectionnez StopThruster ().</span><span class="sxs-lookup"><span data-stu-id="68442-214">Select the No Function dropdown menu and hover over LaunchLunarModule, and select StopThruster ().</span></span> <span data-ttu-id="68442-215">Cela permet de contrôler le niveau de Poussée que l’utilisateur souhaite attribuer au module lunaire.</span><span class="sxs-lookup"><span data-stu-id="68442-215">This controls how much thrust the user wants to give to the lunar module.</span></span>

    ![Lesson6 Chapter5 Step2im](images/Lesson6_Chapter5_step2im.PNG)

3. <span data-ttu-id="68442-217">Faites glisser le module lunaire de la hiérarchie de la scène de base dans l’emplacement vide sous le bouton enfoncé dans le panneau de l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="68442-217">Drag the lunar module from the base scene hierarchy into the empty slot under Button Pressed in the inspector panel.</span></span>

4. <span data-ttu-id="68442-218">Cliquez sur le menu déroulant aucune fonction, puis sur LaunchLunarModule et sélectionnez StartThruster ().</span><span class="sxs-lookup"><span data-stu-id="68442-218">Click the No function dropdown menu and then on LaunchLunarModule and select StartThruster ().</span></span>

    ![Lesson6 Chapter5 Step4im](images/Lesson6_Chapter5_step4im.PNG)

5. <span data-ttu-id="68442-220">Ajoutez de la musique au module lunaire pour que la musique soit lue lorsque la fusée est désactivée.</span><span class="sxs-lookup"><span data-stu-id="68442-220">Add music to the lunar module so that music plays when the rocket takes off.</span></span> <span data-ttu-id="68442-221">Pour ce faire, faites glisser le module lunaire vers l’emplacement vide suivant sous le bouton enfoncé ().</span><span class="sxs-lookup"><span data-stu-id="68442-221">To do this, drag the lunar module to the next empty slot under Button Pressed().</span></span>

6. <span data-ttu-id="68442-222">Sélectionnez le menu déroulant aucune fonction, pointez sur AudioSource, puis sélectionnez PlayOneShot (AudioClip).</span><span class="sxs-lookup"><span data-stu-id="68442-222">Select the No Function dropdown menu, hover over AudioSource and select PlayOneShot (AudioClip).</span></span> <span data-ttu-id="68442-223">Vous pouvez explorer les différents sons fournis avec le MRTK.</span><span class="sxs-lookup"><span data-stu-id="68442-223">Feel free to explore the variety of sounds included with the MRTK.</span></span> <span data-ttu-id="68442-224">Dans cet exemple, nous allons utiliser « MRTK_Gem ».</span><span class="sxs-lookup"><span data-stu-id="68442-224">In this example, we'll use "MRTK_Gem."</span></span>

    ![Lesson6 Chapter5 Step6im](images/Lesson6_Chapter5_step6im.PNG)

## <a name="congratulations"></a><span data-ttu-id="68442-226">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="68442-226">Congratulations</span></span>

<span data-ttu-id="68442-227">Vous avez entièrement configuré cette application.</span><span class="sxs-lookup"><span data-stu-id="68442-227">You have fully configured this application.</span></span> <span data-ttu-id="68442-228">Maintenant, lorsque vous appuyez sur lire, vous pouvez assembler complètement le module lunaire, activer/désactiver les indicateurs, lancer le module lunaire et le réinitialiser pour redémarrer.</span><span class="sxs-lookup"><span data-stu-id="68442-228">Now, when you press play, you can fully assemble the lunar module, toggle hints, launch the lunar module and reset it to start again.</span></span>
