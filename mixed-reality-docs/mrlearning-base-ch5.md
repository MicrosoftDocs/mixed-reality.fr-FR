---
title: Tutoriels de démarrage - 6. Exploration des options d’entrée avancées
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: ec078015304e1cddc9b042fb5e94cf1904a302cb
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79376086"
---
# <a name="6-exploring-advanced-input-options"></a><span data-ttu-id="160e7-105">6. Exploration des options d’entrée avancées</span><span class="sxs-lookup"><span data-stu-id="160e7-105">6. Exploring advanced input options</span></span>

<span data-ttu-id="160e7-106">Dans ce tutoriel, vous allez examiner quelques options d’entrée avancée pour HoloLens 2, notamment l’utilisation de commandes vocales, le mouvement de panoramique et l’eye-tracking.</span><span class="sxs-lookup"><span data-stu-id="160e7-106">In this tutorial, you will explore a few advanced input options for HoloLens 2, including the use of voice commands, panning gesture, and eye tracking.</span></span>

## <a name="objectives"></a><span data-ttu-id="160e7-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="160e7-107">Objectives</span></span>

* <span data-ttu-id="160e7-108">Déclencher des événements en utilisant des commandes vocales et des mots clés</span><span class="sxs-lookup"><span data-stu-id="160e7-108">Trigger events using voice commands and keywords</span></span>
* <span data-ttu-id="160e7-109">Utiliser le suivi des mains pour faire un panoramique sur des textures et des objets 3D</span><span class="sxs-lookup"><span data-stu-id="160e7-109">Use tracked hands to pan textures and 3D objects with tracked hands</span></span>
* <span data-ttu-id="160e7-110">Tirer parti des fonctionnalités d’eye-tracking d’HoloLens 2 pour sélectionner des objets</span><span class="sxs-lookup"><span data-stu-id="160e7-110">Leverage HoloLens 2 eye tracking capabilities to select objects</span></span>

## <a name="enabling-voice-commands"></a><span data-ttu-id="160e7-111">Activation des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="160e7-111">Enabling Voice Commands</span></span>
<!-- TODO: Consider changing to 'Enabling Speech Commands -->

<span data-ttu-id="160e7-112">Dans cette section, vous allez implémenter une commande vocale pour permettre à l’utilisateur de jouer un son sur l’objet Octa.</span><span class="sxs-lookup"><span data-stu-id="160e7-112">In this section, you will implement a speech command to let the user play a sound on the Octa object.</span></span> <span data-ttu-id="160e7-113">Pour cela, vous allez créer une commande vocale, puis configurer l’événement pour qu’il déclenche l’action souhaitée quand le mot clé de la commande vocale est prononcé.</span><span class="sxs-lookup"><span data-stu-id="160e7-113">For this, you will create a new speech command and then configure the event so it triggers the desired action when the speech command keyword is spoken.</span></span>

<span data-ttu-id="160e7-114">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="160e7-114">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="160e7-115">Cloner le Input System Profile par défaut</span><span class="sxs-lookup"><span data-stu-id="160e7-115">Clone the default Input System Profile</span></span>
2. <span data-ttu-id="160e7-116">Cloner le Speech Commands Profile par défaut</span><span class="sxs-lookup"><span data-stu-id="160e7-116">Clone the default Speech Commands Profile</span></span>
3. <span data-ttu-id="160e7-117">Créer une commande vocale</span><span class="sxs-lookup"><span data-stu-id="160e7-117">Create a new speech command</span></span>
4. <span data-ttu-id="160e7-118">Ajouter et configurer le composant Speech Input Handler (Script)</span><span class="sxs-lookup"><span data-stu-id="160e7-118">Add and configure the Speech Input Handler (Script) component</span></span>
5. <span data-ttu-id="160e7-119">Implémenter l’événement Response pour la commande Speech</span><span class="sxs-lookup"><span data-stu-id="160e7-119">Implement the Response event for the speech command</span></span>

### <a name="1-clone-the-default-input-system-profile"></a><span data-ttu-id="160e7-120">1. Cloner le Input System Profile par défaut</span><span class="sxs-lookup"><span data-stu-id="160e7-120">1. Clone the default Input System Profile</span></span>

<span data-ttu-id="160e7-121">Dans la fenêtre Hierarchy, sélectionnez l’objet **MixedRealityToolkit** puis, dans la fenêtre Inspector, sélectionnez l’onglet **Input** et clonez le **DefaultHoloLens2InputSystemProfile** pour le remplacer par votre propre **Input System Profile** personnalisable :</span><span class="sxs-lookup"><span data-stu-id="160e7-121">In the Hierarchy window, select the **MixedRealityToolkit** object, then in the Inspector window, select the **Input** tab and clone the **DefaultHoloLens2InputSystemProfile** to replace it with your own customizable **Input System Profile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step1-1.png)

> [!TIP]
> <span data-ttu-id="160e7-123">Pour un rappel de la façon de cloner des profils MRTK, vous pouvez consulter les instructions du [Guide pratique pour configurer les profils du Kit de ressources de réalité mixte](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option).</span><span class="sxs-lookup"><span data-stu-id="160e7-123">For a reminder on how to clone MRTK profiles, you can refer to the [How to configure the Mixed Reality Toolkit Profiles](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) instructions.</span></span>

### <a name="2-clone-the-default-speech-commands-profile"></a><span data-ttu-id="160e7-124">2. Cloner le Speech Commands Profile par défaut</span><span class="sxs-lookup"><span data-stu-id="160e7-124">2. Clone the default Speech Commands Profile</span></span>

<span data-ttu-id="160e7-125">Développez la section **Speech** et clonez le profil **DefaultMixedRealitySpeechCommandsProfile** pour le remplacer par votre propre **Speech Commands Profile** personnalisable :</span><span class="sxs-lookup"><span data-stu-id="160e7-125">Expand the **Speech** section and clone the **DefaultMixedRealitySpeechCommandsProfile** to replace it with your own customizable **Speech Commands Profile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step2-1.png)

### <a name="3-create-a-new-speech-command"></a><span data-ttu-id="160e7-127">3. Créer une commande vocale</span><span class="sxs-lookup"><span data-stu-id="160e7-127">3. Create a new speech command</span></span>

<span data-ttu-id="160e7-128">Dans la section **Speech Commands**, cliquez sur le bouton **+ Add a New Speech Command** pour ajouter une nouvelle commande vocale au bas de la liste des commandes vocales existantes puis, dans le champ **Keyword**, entrez un mot ou une expression appropriée, par exemple **Play Music** :</span><span class="sxs-lookup"><span data-stu-id="160e7-128">In the **Speech Commands** section, click the **+ Add a New Speech Command** button to add a new speech command to the bottom of the list of existing speech commands, then in the **Keyword** field enter a suitable word or phrase, for example **Play Music**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step3-1.png)

> [!TIP]
> <span data-ttu-id="160e7-130">Si votre ordinateur ne dispose pas d’un microphone et que vous souhaitez tester la commande vocale avec la simulation dans l’éditeur, vous pouvez affecter un KeyCode à la commande vocale, ce qui vous permet de la déclencher quand vous appuyez sur la touche correspondante.</span><span class="sxs-lookup"><span data-stu-id="160e7-130">If your computer doesn't have a microphone and you would like to test the speech command using the in-editor simulation, you can assign a KeyCode to the speech command which will let you trigger it when the corresponding key is pressed.</span></span>

### <a name="4-add-and-configure-the-speech-input-handler-script-component"></a><span data-ttu-id="160e7-131">4. Ajouter et configurer le composant Speech Input Handler (Script)</span><span class="sxs-lookup"><span data-stu-id="160e7-131">4. Add and configure the Speech Input Handler (Script) component</span></span>

<span data-ttu-id="160e7-132">Dans la fenêtre Hierarchy, sélectionnez l’objet **Octa** et ajoutez le composant **Speech Input Handler (Script)** à l’objet Octa.</span><span class="sxs-lookup"><span data-stu-id="160e7-132">In the Hierarchy window, select the **Octa** object and add the **Speech Input Handler (Script)** component to the Octa object.</span></span> <span data-ttu-id="160e7-133">Décochez ensuite la case **Is Focus Required** pour que l’utilisateur ne soit pas obligé de regarder l’objet Octa pour déclencher la commande vocale :</span><span class="sxs-lookup"><span data-stu-id="160e7-133">Then uncheck the **Is Focus Required** checkbox so the user is not required to look at the Octa object to trigger the speech command:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step4-1.png)

### <a name="5-implement-the-response-event-for-the-speech-command"></a><span data-ttu-id="160e7-135">5. Implémenter l’événement Response pour la commande Speech</span><span class="sxs-lookup"><span data-stu-id="160e7-135">5. Implement the Response event for the speech command</span></span>

<span data-ttu-id="160e7-136">Sur le composant Speech Input Handler (Script), cliquez sur le petit bouton **+** pour ajouter un élément de mot clé à la liste des mots clés :</span><span class="sxs-lookup"><span data-stu-id="160e7-136">On the Speech Input Handler (Script) component, click the small **+** button to add a keyword element to the list of keywords:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step5-1.png)

<span data-ttu-id="160e7-138">Cliquez sur le **Element 0** que vous venez de créer pour le développer puis, dans la liste déroulante **Keyword**, choisissez le mot clé **Play Music** que vous avez créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="160e7-138">Click the newly created **Element 0** to expand it, and then, from the **Keyword** dropdown, choose the **Play Music** keyword you created earlier:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step5-2.png)

> [!NOTE]
> <span data-ttu-id="160e7-140">Les mots clés de la liste déroulante Keyword sont renseignés en fonction des mots clés définis dans la liste Speech Commands du profil de commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="160e7-140">The keywords in the Keyword dropdown are populated based on the keywords defined in the Speech Commands list in the Speech Commands Profile.</span></span>

<span data-ttu-id="160e7-141">Créez un événement **Response ()** , configurez l’objet **Octa** pour recevoir l’événement, définissez **AudioSource.PlayOneShot** comme action à déclencher et affectez un clip audio approprié au champ **Audio Clip**, par exemple le clip audio MRTK_Gem :</span><span class="sxs-lookup"><span data-stu-id="160e7-141">Create a new **Response ()** event, configure the **Octa** object to receive the event, define **AudioSource.PlayOneShot** as the action to be triggered, and assign a suitable audio clip to the **Audio Clip** field, for example, the MRTK_Gem audio clip:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step5-3.png)

> [!TIP]
> <span data-ttu-id="160e7-143">Pour un rappel de la façon d’implémenter des événements et d’affecter un clip audio, vous pouvez consulter les instructions de [Implémenter un événement On Touch Started](mrlearning-base-ch4.md#4-implement-the-on-touch-started-event).</span><span class="sxs-lookup"><span data-stu-id="160e7-143">For a reminder on how to implement events and assign an audio clip, you can refer to the [Implement the On Touch Started event](mrlearning-base-ch4.md#4-implement-the-on-touch-started-event) instructions.</span></span>

## <a name="the-pan-gesture"></a><span data-ttu-id="160e7-144">Le mouvement panoramique</span><span class="sxs-lookup"><span data-stu-id="160e7-144">The Pan Gesture</span></span>

<span data-ttu-id="160e7-145">Le mouvement panoramique est utile pour le défilement en utilisant votre doigt ou votre main pour faire défiler le contenu.</span><span class="sxs-lookup"><span data-stu-id="160e7-145">The pan gesture is useful for scrolling by using your finger or hand to scroll through content.</span></span> <span data-ttu-id="160e7-146">Dans cet exemple, vous allez d’abord découvrir comment faire défiler une IU 2D, puis à développer à partir de là pour pouvoir faire défiler une collection d’objets 3D.</span><span class="sxs-lookup"><span data-stu-id="160e7-146">In this example, you will first learn how to scroll a 2D UI and then expand on that to be able to scroll through a collection of 3D objects.</span></span>

<span data-ttu-id="160e7-147">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="160e7-147">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="160e7-148">Créer un objet Quad qui peut être utilisé pour le panoramique</span><span class="sxs-lookup"><span data-stu-id="160e7-148">Create a Quad object that can be used for panning</span></span>
2. <span data-ttu-id="160e7-149">Ajouter le composant Near Interaction Touchable (Script)</span><span class="sxs-lookup"><span data-stu-id="160e7-149">Add the Near Interaction Touchable (Script) component</span></span>
3. <span data-ttu-id="160e7-150">Ajouter le composant Hand Interaction Pan Zoom (Script)</span><span class="sxs-lookup"><span data-stu-id="160e7-150">Add the Hand Interaction Pan Zoom (Script) component</span></span>
4. <span data-ttu-id="160e7-151">Ajouter du contenu 2D à faire défiler</span><span class="sxs-lookup"><span data-stu-id="160e7-151">Add 2D content to be scrolled</span></span>
5. <span data-ttu-id="160e7-152">Ajouter du contenu 3D à faire défiler</span><span class="sxs-lookup"><span data-stu-id="160e7-152">Add 3D content to be scrolled</span></span>
6. <span data-ttu-id="160e7-153">Ajouter le composant Move With Pan (Script)</span><span class="sxs-lookup"><span data-stu-id="160e7-153">Add the Move With Pan (Script) component</span></span>

> [!NOTE]
> <span data-ttu-id="160e7-154">Le composant Move With Pan (script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="160e7-154">The Move With Pan (Script) component is not part of MRTK.</span></span> <span data-ttu-id="160e7-155">Il a été fourni avec les ressources de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="160e7-155">It was provided with this tutorial's assets.</span></span>

### <a name="1-create-a-quad-object-that-can-be-used-for-panning"></a><span data-ttu-id="160e7-156">1. Créer un objet Quad qui peut être utilisé pour le panoramique</span><span class="sxs-lookup"><span data-stu-id="160e7-156">1. Create a Quad object that can be used for panning</span></span>

<span data-ttu-id="160e7-157">Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur une zone vide, puis sélectionnez **3D Object** > **Quad** pour ajouter un quad à votre scène.</span><span class="sxs-lookup"><span data-stu-id="160e7-157">In the Hierarchy window, right-click at an empty area and select **3D Object** > **Quad** to add a quad to your scene.</span></span> <span data-ttu-id="160e7-158">Donnez-lui un nom approprié, par exemple **PanGesture**, et positionnez-le à un emplacement approprié, par exemple X = 0 ; Y = -0,2 ; Z = 2.</span><span class="sxs-lookup"><span data-stu-id="160e7-158">Give it a suitable name, for example, **PanGesture**, and position it in a suitable location, for example, X = 0, Y = -0.2, Z = 2.</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step1-1.png)

> [!TIP]
> <span data-ttu-id="160e7-160">Pour un rappel de la façon d’ajouter à votre scène des primitives Unity, comme un quad 3D, vous pouvez vous reporter aux instructions de [Ajouter un cube à la scène](mrlearning-base-ch2.md#2-add-a-cube-to-the-scene).</span><span class="sxs-lookup"><span data-stu-id="160e7-160">For a reminder on how to add Unity primitives, such as a 3D quad, to your scene, you can refer to the [Add a cube to the scene](mrlearning-base-ch2.md#2-add-a-cube-to-the-scene) instructions.</span></span>

<span data-ttu-id="160e7-161">Comme pour toute autre interaction, le mouvement panoramique nécessite également un collider.</span><span class="sxs-lookup"><span data-stu-id="160e7-161">As with any other interaction, the the pan gesture also requires a collider.</span></span> <span data-ttu-id="160e7-162">Par défaut, un quad a un mesh collider.</span><span class="sxs-lookup"><span data-stu-id="160e7-162">By default, a Quad has a mesh collider.</span></span> <span data-ttu-id="160e7-163">Celui-ci n’est cependant pas idéal, car il est extrêmement fin.</span><span class="sxs-lookup"><span data-stu-id="160e7-163">However, the mesh collider is not ideal because it is extremely thin.</span></span> <span data-ttu-id="160e7-164">Pour faciliter l’interaction de l’utilisateur avec le collider, nous allons remplacer le collider de maillage par un box collider.</span><span class="sxs-lookup"><span data-stu-id="160e7-164">To make it easier for the user to interact with the collider, we will replace the mesh collider with a box collider.</span></span>

<span data-ttu-id="160e7-165">Avec l’objet PanGesture sélectionné, cliquez sur l’icône **Settings** du composant **Mesh Collider** et sélectionnez **Remove Component** pour supprimer le mesh collider :</span><span class="sxs-lookup"><span data-stu-id="160e7-165">With the PanGesture object still selected, click the **Mesh Collider** component's **Settings** icon and select **Remove Component** to remove the Mesh Collider:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step1-2.png)

<span data-ttu-id="160e7-167">Dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter un **Box Collider**, puis changez la taille (**Size**) de Z en 0,15 pour augmenter l’épaisseur du box collider :</span><span class="sxs-lookup"><span data-stu-id="160e7-167">In the Inspector window, use the **Add Component** button to add a **Box Collider**, then change the Box Collider **Size** Z to 0.15 to increase the thickness of the box collider:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step1-3.png)

### <a name="2-add-the-near-interaction-touchable-script-component"></a><span data-ttu-id="160e7-169">2. Ajouter le composant Near Interaction Touchable (Script)</span><span class="sxs-lookup"><span data-stu-id="160e7-169">2. Add the Near Interaction Touchable (Script) component</span></span>

<span data-ttu-id="160e7-170">Avec l’objet **PanGesture** toujours sélectionné, ajoutez le composant **Near Interaction Touchable (Script)** à l’objet PanGesture, puis cliquez sur les boutons **Fix Bounds** et **Fix Center** pour mettre à jour les propriétés Center et Bounds de Near Interaction Touchable (Script) pour qu’elles correspondent au BoxCollider :</span><span class="sxs-lookup"><span data-stu-id="160e7-170">With the **PanGesture** object still selected, add the **Near Interaction Touchable (Script)** component to the PanGesture object, and then click the **Fix Bounds** and **Fix Center** buttons to update the Local Center and Bounds properties of the Near Interaction Touchable (Script) to match the BoxCollider:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step2-1.png)

### <a name="3-add-the-hand-interaction-pan-zoom-script-component"></a><span data-ttu-id="160e7-172">3. Ajouter le composant Hand Interaction Pan Zoom (Script)</span><span class="sxs-lookup"><span data-stu-id="160e7-172">3. Add the Hand Interaction Pan Zoom (Script) component</span></span>

<span data-ttu-id="160e7-173">Avec l’objet **PanGesture** sélectionné, ajoutez le composant **Hand Interaction Pan Zoom (Script)** à l’objet PanGesture, puis cochez la case **Lock Horizontal** pour autoriser seulement le défilement vertical :</span><span class="sxs-lookup"><span data-stu-id="160e7-173">With the **PanGesture** object still selected, add the **Hand Interaction Pan Zoom (Script)** component to the PanGesture object, and then check the **Lock Horizontal** checkbox to allow vertical scrolling only:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step3-1.png)

### <a name="4-add-2d-content-to-be-scrolled"></a><span data-ttu-id="160e7-175">4. Ajouter du contenu 2D à faire défiler</span><span class="sxs-lookup"><span data-stu-id="160e7-175">4. Add 2D content to be scrolled</span></span>

<span data-ttu-id="160e7-176">Dans le panneau Project, recherchez le matériau **PanContent**, puis cliquez sur celui-ci et faites-le glisser vers la propriété Mesh Renderer **Material** Element 0 de l’objet **PanGesture** :</span><span class="sxs-lookup"><span data-stu-id="160e7-176">In the Project panel, search for the **PanContent** material and then click-and-drag it on to the **PanGesture** object's Mesh Renderer **Material** Element 0 property:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step4-1.png)

<span data-ttu-id="160e7-178">Dans la fenêtre Inspector, développez le composant de matériau **PanContent** nouvellement ajouté, puis changez sa valeur Y de **Tiling** en 0,5 afin qu’elle corresponde à la valeur X et que les vignettes apparaissent sous forme de carré :</span><span class="sxs-lookup"><span data-stu-id="160e7-178">In the Inspector window, expand the newly added **PanContent** material component, and then change it's **Tiling** Y value to 0.5 so it matches the X value and the tiles appear square:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step4-2.png)

<span data-ttu-id="160e7-180">Si vous passez maintenant en mode Game, vous pouvez tester le défilement de contenu 2D avec le mouvement panoramique de la simulation dans l’éditeur :</span><span class="sxs-lookup"><span data-stu-id="160e7-180">If you now enter Game mode, you can test scrolling the 2D content using the pan gesture in the in-editor simulation:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step4-3.png)

### <a name="5-add-3d-content-to-be-scrolled"></a><span data-ttu-id="160e7-182">5. Ajouter du contenu 3D à faire défiler</span><span class="sxs-lookup"><span data-stu-id="160e7-182">5. Add 3D content to be scrolled</span></span>

<span data-ttu-id="160e7-183">Dans la fenêtre Hierarchy, **créez quatre cubes** en tant qu’objets enfants de l’objet **PanGesture** et définissez la valeur **Scale** de leur transformation sur X = 0,15 ; Y = 0,15 ; Z = 0,15 :</span><span class="sxs-lookup"><span data-stu-id="160e7-183">In the Hierarchy window, **create four cubes** as a child objects of the **PanGesture** object and set their Transform **Scale** to X = 0.15, Y = 0.15, Z = 0.15:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step5-1.png)

<span data-ttu-id="160e7-185">Pour espacer uniformément les cubes et gagner du temps, ajoutez le composant **Grid Object Collection (Script)** à l’objet parent des cubes, c’est-à-dire à l’objet **PanGesture**, et configurez Grid Object Collection (Script) comme suit :</span><span class="sxs-lookup"><span data-stu-id="160e7-185">To space the cubes out evenly, and save some time, add the **Grid Object Collection (Script)** component, to the cubes' parent object, i.e. the **PanGesture** object, and configure the Grid Object Collection (Script) as follows:</span></span>

* <span data-ttu-id="160e7-186">Changez **Num Rows** en 1 pour que tous les cubes soient alignés sur une même ligne</span><span class="sxs-lookup"><span data-stu-id="160e7-186">Change **Num Rows** to 1 to have all the cubes aligned on one single row</span></span>
* <span data-ttu-id="160e7-187">Changez **Cell Width** en 0,25 pour espacer les cubes dans la ligne</span><span class="sxs-lookup"><span data-stu-id="160e7-187">Change **Cell Width** to 0.25 to space out the cubes within the row</span></span>

<span data-ttu-id="160e7-188">Cliquez ensuite sur le bouton **Update Collection** pour appliquer la nouvelle configuration :</span><span class="sxs-lookup"><span data-stu-id="160e7-188">Then click the **Update Collection** button to apply the new configuration:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step5-2.png)

### <a name="6-add-the-move-with-pan-script-component"></a><span data-ttu-id="160e7-190">6. Ajouter le composant Move With Pan (Script)</span><span class="sxs-lookup"><span data-stu-id="160e7-190">6. Add the Move With Pan (Script) component</span></span>

<span data-ttu-id="160e7-191">Dans la fenêtre Hierarchy, sélectionnez tous les **objets enfants du cube** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Move With Pan (Script)** à tous les cubes :</span><span class="sxs-lookup"><span data-stu-id="160e7-191">In the Hierarchy window, select all the **Cube child objects**, then in the Inspector window, use the **Add Component** button to add the **Move With Pan (Script)** component to all the cubes:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-1.png)

> [!TIP]
> <span data-ttu-id="160e7-193">Pour un rappel de la façon de sélectionner plusieurs objets dans la fenêtre Hierarchy, vous pouvez vous référer aux instructions de [Ajouter le composant Manipulation Handler (Script) à tous les objets](mrlearning-base-ch4.md#1-add-the-manipulation-handler-script-component-to-all-the-objects).</span><span class="sxs-lookup"><span data-stu-id="160e7-193">For a reminder on how to select multiple objects in the Hierarchy window, tou can refer to the [Add the Manipulation Handler (Script) component to all the objects](mrlearning-base-ch4.md#1-add-the-manipulation-handler-script-component-to-all-the-objects) instructions.</span></span>

<span data-ttu-id="160e7-194">Avec tous les cubes sélectionnés, cliquez et faites glisser l’objet **PanGesture** vers le champ**Pan Input Source** :</span><span class="sxs-lookup"><span data-stu-id="160e7-194">With all the cubes still selected, click-and-drag the **PanGesture** object to the **Pan Input Source** field:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-2.png)

> [!TIP]
> <span data-ttu-id="160e7-196">Le composant Move with Pan (Script) sur chaque cube est à l’écoute de l’événement Pan Updated envoyé par le composant HandInteractionPanZoom (Script) sur l’objet PanGesture, que vous avez affecté comme Pan Input Source à l’étape ci-dessus, et il met à jour la position de chaque cube en conséquence.</span><span class="sxs-lookup"><span data-stu-id="160e7-196">The Move With Pan (Script) component on each cube listens for the Pan Updated event sent by the HandInteractionPanZoom (Script) component on the PanGesture object, which you assigned as the Pan Input Source in the step above, and updates each cube's position accordingly.</span></span>

<span data-ttu-id="160e7-197">Dans la fenêtre Hierarchy, sélectionnez l’objet **PanGesture** puis, dans l’inspecteur, **décochez** la case **Mesh Renderer** pour désactiver le composant Mesh Renderer :</span><span class="sxs-lookup"><span data-stu-id="160e7-197">In the Hierarchy window, select the **PanGesture** object, then in the inspector **un-check** the **Mesh Renderer** checkbox to disable the Mesh Renderer component:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-3.png)

<span data-ttu-id="160e7-199">Si vous passez maintenant en mode Game, vous pouvez tester le défilement de contenu 3D avec le mouvement panoramique de la simulation dans l’éditeur :</span><span class="sxs-lookup"><span data-stu-id="160e7-199">If you now enter Game mode, you can test scrolling the 3D content using the pan gesture in the in-editor simulation:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-4.png)

## <a name="eye-tracking"></a><span data-ttu-id="160e7-201">Eye-tracking</span><span class="sxs-lookup"><span data-stu-id="160e7-201">Eye Tracking</span></span>

<span data-ttu-id="160e7-202">Dans cette section, nous allons examiner comment activer l’eye-tracking dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="160e7-202">In this section, you will explore how to enable eye tracking in your project.</span></span> <span data-ttu-id="160e7-203">Pour cet exemple, vous allez implémenter une fonctionnalité permettant de faire en sorte que chaque objet de la 3DObjectCollection tourne lentement tout en faisant l’objet d’un pointage du regard de l’utilisateur, ainsi que de déclencher un effet de spot quand l’objet regardé est sélectionné par un toucher en l’air ou une commande vocale.</span><span class="sxs-lookup"><span data-stu-id="160e7-203">For this example, you will implement functionality to make each object in the 3DObjectCollection spin slowly while being looked at by the user's eye gaze, as well as, trigger a blip effect when the object being looked at is selected by air-tap or speech command.</span></span>

<span data-ttu-id="160e7-204">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="160e7-204">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="160e7-205">Ajouter le composant Eye Tracking Target (Script) à tous les objets cibles.</span><span class="sxs-lookup"><span data-stu-id="160e7-205">Add the Eye Tracking Target (Script) component to all target objects</span></span>
2. <span data-ttu-id="160e7-206">Ajouter le composant Eye Tracking Tutorial Demo (Script) à tous les objets cibles</span><span class="sxs-lookup"><span data-stu-id="160e7-206">Add the Eye Tracking Tutorial Demo (Script) component  to all target objects</span></span>
3. <span data-ttu-id="160e7-207">Implémenter l’événement While Looking At Target</span><span class="sxs-lookup"><span data-stu-id="160e7-207">Implement the While Looking At Target event</span></span>
4. <span data-ttu-id="160e7-208">Implémenter l’événement On Selected</span><span class="sxs-lookup"><span data-stu-id="160e7-208">Implement the On Selected event</span></span>
5. <span data-ttu-id="160e7-209">Activer l’eye-tracking simulé pour les simulations dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="160e7-209">Enable simulated eye tracking for in-editor simulations</span></span>
6. <span data-ttu-id="160e7-210">Activer l’entrée par pointage du regard dans les fonctionnalités de l’application du projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="160e7-210">Enable Gaze Input in the Visual Studio project's app capabilities</span></span>

### <a name="1-add-the-eye-tracking-target-script-component-to-all-target-objects"></a><span data-ttu-id="160e7-211">1. Ajouter le composant Eye Tracking Target (Script) à tous les objets cibles.</span><span class="sxs-lookup"><span data-stu-id="160e7-211">1. Add the Eye Tracking Target (Script) component to all target objects</span></span>

<span data-ttu-id="160e7-212">Dans la fenêtre Hierarchy, développez l’objet **3DObjectCollection** et sélectionnez tous les **objets enfants** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Eye Tracking Target (Script)** à tous les objets enfants :</span><span class="sxs-lookup"><span data-stu-id="160e7-212">In the Hierarchy window, expand the **3DObjectCollection** object and select all the **child objects**, then in the Inspector window, use the **Add Component** button to add the **Eye Tracking Target (Script)** component to all the child objects:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step1-1.png)

<span data-ttu-id="160e7-214">Avec tous les **objets enfants** sélectionnés, configurez le composant **Eye Tracking Target (Script)** comme suit :</span><span class="sxs-lookup"><span data-stu-id="160e7-214">With all the **child objects** still selected, configure the **Eye Tracking Target (Script)** component as follows:</span></span>

* <span data-ttu-id="160e7-215">Changez **Select Action** en **Select** pour définir l’action de toucher en l’air pour cet objet comme étant Select</span><span class="sxs-lookup"><span data-stu-id="160e7-215">Change **Select Action** to **Select**, to define the air-tap action for this object as Select</span></span>
* <span data-ttu-id="160e7-216">Développez **Voice Select** et définissez la taille (**Size**) de la liste des commandes vocales sur 1 puis, dans la nouvelle liste d’éléments qui apparaît, changez **Element 0** en **Select** pour définir l’action de commande vocale pour cet objet comme étant Select</span><span class="sxs-lookup"><span data-stu-id="160e7-216">Expand **Voice Select** and set the voice command list **Size** to 1, and then, in the new element list that appear, change **Element 0** to **Select**, to define the speech command action for this object as Select</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step1-2.png)

### <a name="2-add-the-eye-tracking-tutorial-demo-script-component--to-all-target-objects"></a><span data-ttu-id="160e7-218">2. Ajouter le composant Eye Tracking Tutorial Demo (Script) à tous les objets cibles</span><span class="sxs-lookup"><span data-stu-id="160e7-218">2. Add the Eye Tracking Tutorial Demo (Script) component  to all target objects</span></span>

<span data-ttu-id="160e7-219">Avec tous les **objets enfants** sélectionnés, utilisez le bouton **Add Component** pour ajouter le composant **Eye Tracking Tutorial Demo (Script)** à tous les objets enfants :</span><span class="sxs-lookup"><span data-stu-id="160e7-219">With all the **child objects** still selected, use the **Add Component** button to add the **Eye Tracking Tutorial Demo (Script)** component to all the child objects:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step2-1.png)

> [!NOTE]
> <span data-ttu-id="160e7-221">Le composant Eye Tracking Target (Script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="160e7-221">The Eye Tracking Target (Script) component is not part of MRTK.</span></span> <span data-ttu-id="160e7-222">Il a été fourni avec les ressources de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="160e7-222">It was provided with this tutorial's assets.</span></span>

### <a name="3-implement-the-while-looking-at-target-event"></a><span data-ttu-id="160e7-223">3. Implémenter l’événement While Looking At Target</span><span class="sxs-lookup"><span data-stu-id="160e7-223">3. Implement the While Looking At Target event</span></span>

<span data-ttu-id="160e7-224">Dans la fenêtre Hierarchy, sélectionnez l’objet **Cheese**, puis créez un événement **While Looking At Target ()** , configurez l’objet **Cheese** pour recevoir l’événement et définissez **EyeTrackingTutorialDemo.RotateTarget** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="160e7-224">In the Hierarchy window, select the **Cheese** object, then create a new **While Looking At Target ()** event, configure the **Cheese** object to receive the event, and define **EyeTrackingTutorialDemo.RotateTarget** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step3-1.png)

<span data-ttu-id="160e7-226">**Répétez** pour chacun des objets enfants dans la 3DObjectCollection.</span><span class="sxs-lookup"><span data-stu-id="160e7-226">**Repeat** for each of the child objects in the 3DObjectCollection.</span></span>

> [!TIP]
> <span data-ttu-id="160e7-227">Pour un rappel de la façon d’implémenter des événements, vous pouvez vous référer aux instructions de [Gestes de suivi de la main et boutons d’interaction](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons).</span><span class="sxs-lookup"><span data-stu-id="160e7-227">For a reminder on how to implement events, you can refer to the [Hand tracking gestures and interactable buttons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) instructions.</span></span>

### <a name="4-implement-the-on-selected-event"></a><span data-ttu-id="160e7-228">4. Implémenter l’événement On Selected</span><span class="sxs-lookup"><span data-stu-id="160e7-228">4. Implement the On Selected event</span></span>

<span data-ttu-id="160e7-229">Dans la fenêtre Hierarchy, sélectionnez l’objet **Cheese**, puis créez un événement **On Selected ()** , configurez l’objet **Cheese** pour recevoir l’événement et définissez **EyeTrackingTutorialDemo.BlipTarget** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="160e7-229">In the Hierarchy window, select the **Cheese** object, then create a new **On Selected ()** event, configure the **Cheese** object to receive the event, and define **EyeTrackingTutorialDemo.BlipTarget** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step4-1.png)

<span data-ttu-id="160e7-231">**Répétez** pour chacun des objets enfants dans la 3DObjectCollection.</span><span class="sxs-lookup"><span data-stu-id="160e7-231">**Repeat** for each of the child objects in the 3DObjectCollection.</span></span>

### <a name="5-enable-simulated-eye-tracking-for-in-editor-simulations"></a><span data-ttu-id="160e7-232">5. Activer l’eye-tracking simulé pour les simulations dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="160e7-232">5. Enable simulated eye tracking for in-editor simulations</span></span>

<span data-ttu-id="160e7-233">Dans la fenêtre Hierarchy, sélectionnez l’objet **MixedRealityToolkit** puis, dans la fenêtre Inspector, sélectionnez l’onglet **Input**, développez la section **Input Data Providers**, puis la section **Input Simulation Service**, puis clonez le **DefaultMixedRealityInputSimulationProfile** pour le remplacer par votre **Input Simulation Profile** personnalisable :</span><span class="sxs-lookup"><span data-stu-id="160e7-233">In the Hierarchy window, select the **MixedRealityToolkit** object, then in the Inspector window, select the **Input** tab, expand the **Input Data Providers** section and then the **Input Simulation Service** section, and clone the **DefaultMixedRealityInputSimulationProfile** to replace it with your own customizable **Input Simulation Profile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step5-1.png)

> [!TIP]
> <span data-ttu-id="160e7-235">Pour un rappel de la façon de cloner des profils MRTK, vous pouvez consulter les instructions du [Guide pratique pour configurer les profils du Kit de ressources de réalité mixte](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option).</span><span class="sxs-lookup"><span data-stu-id="160e7-235">For a reminder on how to clone MRTK profiles, you can refer to the [How to configure the Mixed Reality Toolkit Profiles](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) instructions.</span></span>

<span data-ttu-id="160e7-236">Dans la section **Eye Simulation**, cochez la case **Simulate Eye Position** pour activer la simulation de l’eye-tracking :</span><span class="sxs-lookup"><span data-stu-id="160e7-236">In the **Eye Simulation** section, check the **Simulate Eye Position** checkbox to enable eye tracking simulation:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step5-2.png)

<span data-ttu-id="160e7-238">Si vous entrez maintenant dans le mode Game, vous pouvez tester les effets de rotation et de spot que vous avez implémentés en ajustant la vue afin que le curseur atteigne l’un des objets, et en utilisant une interaction manuelle ou une commande vocale pour sélectionner l’objet :</span><span class="sxs-lookup"><span data-stu-id="160e7-238">If you now enter Game mode, you can test the spin and blip effects you implemented by adjusting the view so the cursor hits one of the objects and using hand interaction or speech command to select the object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step5-3.png)

> [!NOTE]
> <span data-ttu-id="160e7-240">Si vous n’avez pas utilisé le DefaultHoloLens2ConfigurationProfile pour cloner votre profil de configuration MRTK personnalisable, comme indiqué dans les instructions de [Configurer le Kit de ressources de réalité mixte](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit), l’eye-tracking peut ne pas être activé dans votre projet et vous devrez l’activer.</span><span class="sxs-lookup"><span data-stu-id="160e7-240">If you did not use the DefaultHoloLens2ConfigurationProfile to clone your customizable MRTK configuration profile, as instructed in the [Configure the Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) instructions, eye tracking may not be enable in your project and will need to be enabled.</span></span> <span data-ttu-id="160e7-241">Pour cela, vous pouvez vous reporter aux instructions de [Bien démarrer avec l’eye-tracking dans MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html).</span><span class="sxs-lookup"><span data-stu-id="160e7-241">For that, you can refer to the [Getting started with eye tracking in MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html) instructions.</span></span>

### <a name="6-enable-gaze-input-in-the-visual-studio-projects-app-capabilities"></a><span data-ttu-id="160e7-242">6. Activer l’entrée par pointage du regard dans les fonctionnalités de l’application du projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="160e7-242">6. Enable Gaze Input in the Visual Studio project's app capabilities</span></span>

<span data-ttu-id="160e7-243">Avant de générer et de déployer votre application à partir de Visual Studio sur votre appareil, l’entrée par pointage du regard doit être activée dans les fonctionnalités de l’application du projet.</span><span class="sxs-lookup"><span data-stu-id="160e7-243">Before building and deploying your app from Visual Studio to your device, Gaze Input has to been enabled in the project's app capabilities.</span></span> <span data-ttu-id="160e7-244">Pour cela, vous pouvez suivre les instructions de [Test de votre application Unity sur HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#testing-your-unity-app-on-a-hololens-2).</span><span class="sxs-lookup"><span data-stu-id="160e7-244">For this, you can follow the [Testing your Unity app on a HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#testing-your-unity-app-on-a-hololens-2) instructions.</span></span>

## <a name="congratulations"></a><span data-ttu-id="160e7-245">Félicitations</span><span class="sxs-lookup"><span data-stu-id="160e7-245">Congratulations</span></span>

<span data-ttu-id="160e7-246">Vous avez réussi à ajouter des fonctionnalités d’eye-tracking de base à votre application.</span><span class="sxs-lookup"><span data-stu-id="160e7-246">You have successfully added basic eye tracking capabilities to your application.</span></span> <span data-ttu-id="160e7-247">Ces premiers pas vous ouvrent la voie vers tout un monde de possibilités avec l’eye-tracking.</span><span class="sxs-lookup"><span data-stu-id="160e7-247">These actions are only the beginning of a world of possibilities with eye tracking.</span></span> <span data-ttu-id="160e7-248">Dans ce tutoriel, vous avez également découvert d’autres fonctionnalités d’entrée avancées, comme les commandes vocales et les mouvements de panoramique.</span><span class="sxs-lookup"><span data-stu-id="160e7-248">In this tutorial, you also learned about other advanced input features, such as voice commands and panning gestures.</span></span>

[<span data-ttu-id="160e7-249">Leçon suivante : 7. Création d’un exemple d’application Module lunaire</span><span class="sxs-lookup"><span data-stu-id="160e7-249">Next Lesson: 7. Creating a Lunar Module sample application</span></span>](mrlearning-base-ch6.md)
