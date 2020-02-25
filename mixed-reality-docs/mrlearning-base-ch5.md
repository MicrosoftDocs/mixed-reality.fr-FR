---
title: Didacticiels de mise en route-6. Exploration des options d’entrée avancées
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: aaa02ce118fd051d94311e837b143affc96ff72b
ms.sourcegitcommit: bd536f4f99c71418b55c121b7ba19ecbaf6336bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "77554259"
---
# <a name="6-exploring-advanced-input-options"></a><span data-ttu-id="91fff-105">6. exploration des options d’entrée avancées</span><span class="sxs-lookup"><span data-stu-id="91fff-105">6. Exploring advanced input options</span></span>

<span data-ttu-id="91fff-106">Dans ce didacticiel, vous allez explorer quelques options d’entrée avancées pour HoloLens 2, y compris l’utilisation de commandes vocales, le mouvement panoramique et le suivi oculaire.</span><span class="sxs-lookup"><span data-stu-id="91fff-106">In this tutorial, you will explore a few advanced input options for HoloLens 2, including the use of voice commands, panning gesture, and eye tracking.</span></span>

## <a name="objectives"></a><span data-ttu-id="91fff-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="91fff-107">Objectives</span></span>

* <span data-ttu-id="91fff-108">Déclencher des événements à l’aide de commandes et de mots clés vocaux</span><span class="sxs-lookup"><span data-stu-id="91fff-108">Trigger events using voice commands and keywords</span></span>
* <span data-ttu-id="91fff-109">Utilisez des mains suivies pour faire pivoter des textures et des objets 3D avec des mains suivies</span><span class="sxs-lookup"><span data-stu-id="91fff-109">Use tracked hands to pan textures and 3D objects with tracked hands</span></span>
* <span data-ttu-id="91fff-110">Tirez parti des fonctionnalités de suivi oculaire HoloLens 2 pour sélectionner des objets</span><span class="sxs-lookup"><span data-stu-id="91fff-110">Leverage HoloLens 2 eye tracking capabilities to select objects</span></span>

## <a name="enabling-voice-commands"></a><span data-ttu-id="91fff-111">Activation des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="91fff-111">Enabling Voice Commands</span></span>
<!-- TODO: Consider changing to 'Enabling Speech Commands -->

<span data-ttu-id="91fff-112">Dans cette section, vous allez implémenter une commande vocale pour permettre à l’utilisateur de lire un son sur l’objet octa.</span><span class="sxs-lookup"><span data-stu-id="91fff-112">In this section, you will implement a speech command to let the user play a sound on the Octa object.</span></span> <span data-ttu-id="91fff-113">Pour ce faire, vous allez créer une nouvelle commande vocale, puis configurer l’événement pour qu’il déclenche l’action souhaitée lorsque le mot clé de commande vocale est parlé.</span><span class="sxs-lookup"><span data-stu-id="91fff-113">For this, you will create a new speech command and then configure the event so it triggers the desired action when the speech command keyword is spoken.</span></span>

<span data-ttu-id="91fff-114">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="91fff-114">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="91fff-115">Cloner le profil de système d’entrée par défaut</span><span class="sxs-lookup"><span data-stu-id="91fff-115">Clone the default Input System Profile</span></span>
2. <span data-ttu-id="91fff-116">Cloner le profil de commandes vocales par défaut</span><span class="sxs-lookup"><span data-stu-id="91fff-116">Clone the default Speech Commands Profile</span></span>
3. <span data-ttu-id="91fff-117">Créer une nouvelle commande vocale</span><span class="sxs-lookup"><span data-stu-id="91fff-117">Create a new speech command</span></span>
4. <span data-ttu-id="91fff-118">Ajouter et configurer le composant Gestionnaire d’entrée vocale (script)</span><span class="sxs-lookup"><span data-stu-id="91fff-118">Add and configure the Speech Input Handler (Script) component</span></span>
5. <span data-ttu-id="91fff-119">Implémenter l’événement Response pour la commande Speech</span><span class="sxs-lookup"><span data-stu-id="91fff-119">Implement the Response event for the speech command</span></span>

### <a name="1-clone-the-default-input-system-profile"></a><span data-ttu-id="91fff-120">1. cloner le profil de système d’entrée par défaut</span><span class="sxs-lookup"><span data-stu-id="91fff-120">1. Clone the default Input System Profile</span></span>

<span data-ttu-id="91fff-121">Dans la fenêtre hiérarchie, sélectionnez l’objet **MixedRealityToolkit** , puis dans la fenêtre de l’inspecteur, sélectionnez l’onglet **entrée** , puis clonez le **DefaultHoloLens2InputSystemProfile** pour le remplacer par votre **profil de système d’entrée**personnalisable :</span><span class="sxs-lookup"><span data-stu-id="91fff-121">In the Hierarchy window, select the **MixedRealityToolkit** object, then in the Inspector window, select the **Input** tab and clone the **DefaultHoloLens2InputSystemProfile** to replace it with your own customizable **Input System Profile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step1-1.png)

> [!TIP]
> <span data-ttu-id="91fff-123">Pour obtenir un rappel sur la façon de cloner des profils MRTK, vous pouvez consulter les instructions de [Configuration des profils de la boîte à outils de la réalité mixte](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) .</span><span class="sxs-lookup"><span data-stu-id="91fff-123">For a reminder on how to clone MRTK profiles, you can refer to the [How to configure the Mixed Reality Toolkit Profiles](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) instructions.</span></span>

### <a name="2-clone-the-default-speech-commands-profile"></a><span data-ttu-id="91fff-124">2. cloner le profil de commandes vocales par défaut</span><span class="sxs-lookup"><span data-stu-id="91fff-124">2. Clone the default Speech Commands Profile</span></span>

<span data-ttu-id="91fff-125">Développez la section **Speech** et clonez le **DefaultMixedRealitySpeechCommandsProfile** pour le remplacer par votre propre **profil de commandes vocales**personnalisables :</span><span class="sxs-lookup"><span data-stu-id="91fff-125">Expand the **Speech** section and clone the **DefaultMixedRealitySpeechCommandsProfile** to replace it with your own customizable **Speech Commands Profile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step2-1.png)

### <a name="3-create-a-new-speech-command"></a><span data-ttu-id="91fff-127">3. créer une nouvelle commande vocale</span><span class="sxs-lookup"><span data-stu-id="91fff-127">3. Create a new speech command</span></span>

<span data-ttu-id="91fff-128">Dans la section **commandes vocales** , cliquez sur le bouton **+ Ajouter une nouvelle commande vocale** pour ajouter une nouvelle commande vocale au bas de la liste des commandes vocales existantes, puis dans le champ **mot clé** , entrez un mot ou une expression appropriée, par exemple **Lire la musique**:</span><span class="sxs-lookup"><span data-stu-id="91fff-128">In the **Speech Commands** section, click the **+ Add a New Speech Command** button to add a new speech command to the bottom of the list of existing speech commands, then in the **Keyword** field enter a suitable word or phrase, for example **Play Music**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step3-1.png)

> [!TIP]
> <span data-ttu-id="91fff-130">Si votre ordinateur ne dispose pas d’un microphone et que vous souhaitez tester la commande vocale à l’aide de la simulation dans l’éditeur, vous pouvez affecter un KeyCode à la commande vocale, ce qui vous permet de la déclencher quand vous appuyez sur la touche correspondante.</span><span class="sxs-lookup"><span data-stu-id="91fff-130">If your computer doesn't have a microphone and you would like to test the speech command using the in-editor simulation, you can assign a KeyCode to the speech command which will let you trigger it when the corresponding key is pressed.</span></span>

### <a name="4-add-and-configure-the-speech-input-handler-script-component"></a><span data-ttu-id="91fff-131">4. Ajouter et configurer le composant Gestionnaire d’entrée vocale (script)</span><span class="sxs-lookup"><span data-stu-id="91fff-131">4. Add and configure the Speech Input Handler (Script) component</span></span>

<span data-ttu-id="91fff-132">Dans la fenêtre hiérarchie, sélectionnez l’objet **octa** et ajoutez le composant **Gestionnaire d’entrée vocale (script)** à l’objet octa.</span><span class="sxs-lookup"><span data-stu-id="91fff-132">In the Hierarchy window, select the **Octa** object and add the **Speech Input Handler (Script)** component to the Octa object.</span></span> <span data-ttu-id="91fff-133">Désactivez ensuite la case à cocher **is Focus required** afin que l’utilisateur n’ait pas besoin d’examiner l’objet octa pour déclencher la commande vocale :</span><span class="sxs-lookup"><span data-stu-id="91fff-133">Then uncheck the **Is Focus Required** checkbox so the user is not required to look at the Octa object to trigger the speech command:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step4-1.png)

### <a name="5-implement-the-response-event-for-the-speech-command"></a><span data-ttu-id="91fff-135">5. implémentez l’événement Response pour la commande Speech</span><span class="sxs-lookup"><span data-stu-id="91fff-135">5. Implement the Response event for the speech command</span></span>

<span data-ttu-id="91fff-136">Sur le composant Gestionnaire d’entrée vocale (script), cliquez sur le petit bouton de **+** pour ajouter un élément de mot clé à la liste des mots clés :</span><span class="sxs-lookup"><span data-stu-id="91fff-136">On the Speech Input Handler (Script) component, click the small **+** button to add a keyword element to the list of keywords:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step5-1.png)

<span data-ttu-id="91fff-138">Cliquez sur l’élément qui vient d’être créé **0** pour le développer, puis, dans la liste déroulante **mot clé** , choisissez le mot clé **Play Music** que vous avez créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="91fff-138">Click the newly created **Element 0** to expand it, and then, from the **Keyword** dropdown, choose the **Play Music** keyword you created earlier:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step5-2.png)

> [!NOTE]
> <span data-ttu-id="91fff-140">Les mots clés dans la liste déroulante de mots clés sont renseignés en fonction des mots clés définis dans la liste commandes vocales du profil commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="91fff-140">The keywords in the Keyword dropdown are populated based on the keywords defined in the Speech Commands list in the Speech Commands Profile.</span></span>

<span data-ttu-id="91fff-141">Créez un événement de **réponse ()** , configurez l’objet **octa** pour recevoir l’événement, définissez **audiosource. PlayOneShot** comme action à déclencher et affectez un clip audio approprié au champ **clip** audio, par exemple, le clip audio MRTK_Gem :</span><span class="sxs-lookup"><span data-stu-id="91fff-141">Create a new **Response ()** event, configure the **Octa** object to receive the event, define **AudioSource.PlayOneShot** as the action to be triggered, and assign a suitable audio clip to the **Audio Clip** field, for example, the MRTK_Gem audio clip:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step5-3.png)

> [!TIP]
> <span data-ttu-id="91fff-143">Pour obtenir un rappel sur la façon d’implémenter des événements et d’assigner un clip audio, vous pouvez consulter les instructions relatives à l' [implémentation de l’événement at Touch Started](mrlearning-base-ch4.md#4-implement-the-on-touch-started-event) .</span><span class="sxs-lookup"><span data-stu-id="91fff-143">For a reminder on how to implement events and assign an audio clip, you can refer to the [Implement the On Touch Started event](mrlearning-base-ch4.md#4-implement-the-on-touch-started-event) instructions.</span></span>

## <a name="the-pan-gesture"></a><span data-ttu-id="91fff-144">Le mouvement panoramique</span><span class="sxs-lookup"><span data-stu-id="91fff-144">The Pan Gesture</span></span>

<span data-ttu-id="91fff-145">Le mouvement panoramique est utile pour faire défiler le contenu à l’aide de votre doigt ou main.</span><span class="sxs-lookup"><span data-stu-id="91fff-145">The pan gesture is useful for scrolling by using your finger or hand to scroll through content.</span></span> <span data-ttu-id="91fff-146">Dans cet exemple, vous allez d’abord apprendre à faire défiler une IU 2D, puis à développer sur cela pour pouvoir faire défiler une collection d’objets 3D.</span><span class="sxs-lookup"><span data-stu-id="91fff-146">In this example, you will first learn how to scroll a 2D UI and then expand on that to be able to scroll through a collection of 3D objects.</span></span>

<span data-ttu-id="91fff-147">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="91fff-147">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="91fff-148">Créer un objet quadruple qui peut être utilisé pour le panoramique</span><span class="sxs-lookup"><span data-stu-id="91fff-148">Create a Quad object that can be used for panning</span></span>
2. <span data-ttu-id="91fff-149">Ajouter le composant touchable (script) near interaction</span><span class="sxs-lookup"><span data-stu-id="91fff-149">Add the Near Interaction Touchable (Script) component</span></span>
3. <span data-ttu-id="91fff-150">Ajouter le composant de zoom (script) d’interaction manuelle</span><span class="sxs-lookup"><span data-stu-id="91fff-150">Add the Hand Interaction Pan Zoom (Script) component</span></span>
4. <span data-ttu-id="91fff-151">Ajouter du contenu 2D à faire défiler</span><span class="sxs-lookup"><span data-stu-id="91fff-151">Add 2D content to be scrolled</span></span>
5. <span data-ttu-id="91fff-152">Ajouter du contenu 3D à faire défiler</span><span class="sxs-lookup"><span data-stu-id="91fff-152">Add 3D content to be scrolled</span></span>
6. <span data-ttu-id="91fff-153">Ajouter le composant déplacer avec le panoramique (script)</span><span class="sxs-lookup"><span data-stu-id="91fff-153">Add the Move With Pan (Script) component</span></span>

> [!NOTE]
> <span data-ttu-id="91fff-154">Le composant Move with Pan (script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="91fff-154">The Move With Pan (Script) component is not part of MRTK.</span></span> <span data-ttu-id="91fff-155">Il a été fourni avec les ressources de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="91fff-155">It was provided with this tutorial's assets.</span></span>

### <a name="1-create-a-quad-object-that-can-be-used-for-panning"></a><span data-ttu-id="91fff-156">1. créer un objet quadruple qui peut être utilisé pour le panoramique</span><span class="sxs-lookup"><span data-stu-id="91fff-156">1. Create a Quad object that can be used for panning</span></span>

<span data-ttu-id="91fff-157">Dans la fenêtre hiérarchie, cliquez avec le bouton droit sur une zone vide et sélectionnez **objet 3d** > **quadruple** pour ajouter un quadruple à votre scène.</span><span class="sxs-lookup"><span data-stu-id="91fff-157">In the Hierarchy window, right-click at an empty area and select **3D Object** > **Quad** to add a quad to your scene.</span></span> <span data-ttu-id="91fff-158">Donnez-lui un nom approprié, par exemple, **PanGesture**, et positionnez-le à un emplacement approprié, par exemple, X = 0, Y =-0,2, Z = 2.</span><span class="sxs-lookup"><span data-stu-id="91fff-158">Give it a suitable name, for example, **PanGesture**, and position it in a suitable location, for example, X = 0, Y = -0.2, Z = 2.</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step1-1.png)

> [!TIP]
> <span data-ttu-id="91fff-160">Pour obtenir un rappel sur la façon d’ajouter des primitives Unity, telles qu’un quadruple 3D, à votre scène, vous pouvez consulter les instructions [Ajouter un cube aux scènes](mrlearning-base-ch2.md#2-add-a-cube-to-the-scene) .</span><span class="sxs-lookup"><span data-stu-id="91fff-160">For a reminder on how to add Unity primitives, such as a 3D quad, to your scene, you can refer to the [Add a cube to the scene](mrlearning-base-ch2.md#2-add-a-cube-to-the-scene) instructions.</span></span>

<span data-ttu-id="91fff-161">Comme pour toute autre interaction, le geste panoramique requiert également un conflit.</span><span class="sxs-lookup"><span data-stu-id="91fff-161">As with any other interaction, the the pan gesture also requires a collider.</span></span> <span data-ttu-id="91fff-162">Par défaut, un quadruple a un conflit de maille.</span><span class="sxs-lookup"><span data-stu-id="91fff-162">By default, a Quad has a mesh collider.</span></span> <span data-ttu-id="91fff-163">Toutefois, le conflit de maille n’est pas idéal, car il est extrêmement léger.</span><span class="sxs-lookup"><span data-stu-id="91fff-163">However, the mesh collider is not ideal because it is extremely thin.</span></span> <span data-ttu-id="91fff-164">Pour faciliter l’interaction de l’utilisateur avec le conflit, nous allons remplacer le conflit de maille par un conflit de Box.</span><span class="sxs-lookup"><span data-stu-id="91fff-164">To make it easier for the user to interact with the collider, we will replace the mesh collider with a box collider.</span></span>

<span data-ttu-id="91fff-165">Avec l’objet PanGesture toujours sélectionné, cliquez sur l’icône des **paramètres** du composant de **conflit de maillage** et sélectionnez **supprimer le composant** pour supprimer le conflit de maille :</span><span class="sxs-lookup"><span data-stu-id="91fff-165">With the PanGesture object still selected, click the **Mesh Collider** component's **Settings** icon and select **Remove Component** to remove the Mesh Collider:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step1-2.png)

<span data-ttu-id="91fff-167">Dans la fenêtre de l’inspecteur, utilisez le bouton **Ajouter un composant** pour ajouter un **conflit de cases**, puis modifiez la **taille** de la zone de conflit Z à 0,15 pour augmenter l’épaisseur du conflit de boîte :</span><span class="sxs-lookup"><span data-stu-id="91fff-167">In the Inspector window, use the **Add Component** button to add a **Box Collider**, then change the Box Collider **Size** Z to 0.15 to increase the thickness of the box collider:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step1-3.png)

### <a name="2-add-the-near-interaction-touchable-script-component"></a><span data-ttu-id="91fff-169">2. ajouter le composant touchable (script) near interaction</span><span class="sxs-lookup"><span data-stu-id="91fff-169">2. Add the Near Interaction Touchable (Script) component</span></span>

<span data-ttu-id="91fff-170">L’objet **PanGesture** étant toujours sélectionné, ajoutez le composant **touchable (script) near-interaction** à l’objet PanGesture, puis cliquez sur les boutons **corriger les limites** et le centre de **Correction** pour mettre à jour les propriétés du centre local et des limites du touchable d’interaction Near (script) pour qu’elles correspondent à la BoxCollider :</span><span class="sxs-lookup"><span data-stu-id="91fff-170">With the **PanGesture** object still selected, add the **Near Interaction Touchable (Script)** component to the PanGesture object, and then click the **Fix Bounds** and **Fix Center** buttons to update the Local Center and Bounds properties of the Near Interaction Touchable (Script) to match the BoxCollider:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step2-1.png)

### <a name="3-add-the-hand-interaction-pan-zoom-script-component"></a><span data-ttu-id="91fff-172">3. Ajoutez le composant zoom (script) d’interaction manuelle</span><span class="sxs-lookup"><span data-stu-id="91fff-172">3. Add the Hand Interaction Pan Zoom (Script) component</span></span>

<span data-ttu-id="91fff-173">Lorsque l’objet **PanGesture** est toujours sélectionné, ajoutez le composant **Zoom (script) d’interaction manuelle** à l’objet PanGesture, puis activez la case à cocher **Verrouiller horizontal** pour autoriser le défilement vertical uniquement :</span><span class="sxs-lookup"><span data-stu-id="91fff-173">With the **PanGesture** object still selected, add the **Hand Interaction Pan Zoom (Script)** component to the PanGesture object, and then check the **Lock Horizontal** checkbox to allow vertical scrolling only:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step3-1.png)

### <a name="4-add-2d-content-to-be-scrolled"></a><span data-ttu-id="91fff-175">4. ajouter le contenu 2D à faire défiler</span><span class="sxs-lookup"><span data-stu-id="91fff-175">4. Add 2D content to be scrolled</span></span>

<span data-ttu-id="91fff-176">Dans le panneau projet, recherchez la documentation **PanContent** , puis cliquez dessus et faites-la glisser vers la propriété élément 0 de la **matière** du convertisseur de maillage de l’objet **PanGesture** :</span><span class="sxs-lookup"><span data-stu-id="91fff-176">In the Project panel, search for the **PanContent** material and then click-and-drag it on to the **PanGesture** object's Mesh Renderer **Material** Element 0 property:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step4-1.png)

<span data-ttu-id="91fff-178">Dans la fenêtre de l’inspecteur, développez le composant de matériau **PanContent** que vous venez d’ajouter, puis remplacez la valeur Y de la **mosaïque** par 0,5 afin qu’il corresponde à la valeur X et que les vignettes apparaissent carré :</span><span class="sxs-lookup"><span data-stu-id="91fff-178">In the Inspector window, expand the newly added **PanContent** material component, and then change it's **Tiling** Y value to 0.5 so it matches the X value and the tiles appear square:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step4-2.png)

<span data-ttu-id="91fff-180">Si vous passez maintenant en mode jeu, vous pouvez tester le contenu 2D à l’aide du mouvement panoramique de la simulation dans l’éditeur :</span><span class="sxs-lookup"><span data-stu-id="91fff-180">If you now enter Game mode, you can test scrolling the 2D content using the pan gesture in the in-editor simulation:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step4-3.png)

### <a name="5-add-3d-content-to-be-scrolled"></a><span data-ttu-id="91fff-182">5. ajouter du contenu 3D à faire défiler</span><span class="sxs-lookup"><span data-stu-id="91fff-182">5. Add 3D content to be scrolled</span></span>

<span data-ttu-id="91fff-183">Dans la fenêtre hiérarchie, **créez quatre cubes** en tant qu’objets enfants de l’objet **PanGesture** et définissez leur **échelle** de transformation sur X = 0,15, Y = 0,15, Z = 0,15 :</span><span class="sxs-lookup"><span data-stu-id="91fff-183">In the Hierarchy window, **create four cubes** as a child objects of the **PanGesture** object and set their Transform **Scale** to X = 0.15, Y = 0.15, Z = 0.15:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step5-1.png)

<span data-ttu-id="91fff-185">Pour espacer uniformément les cubes et gagner du temps, ajoutez le composant de **collection d’objets Grid (script)** à l’objet parent des cubes, c’est-à-dire l’objet **PanGesture** , puis configurez la collection d’objets Grid (script) comme suit :</span><span class="sxs-lookup"><span data-stu-id="91fff-185">To space the cubes out evenly, and save some time, add the **Grid Object Collection (Script)** component, to the cubes' parent object, i.e. the **PanGesture** object, and configure the Grid Object Collection (Script) as follows:</span></span>

* <span data-ttu-id="91fff-186">Remplacez le **nombre de lignes** par 1 pour que tous les cubes soient alignés sur une seule ligne</span><span class="sxs-lookup"><span data-stu-id="91fff-186">Change **Num Rows** to 1 to have all the cubes aligned on one single row</span></span>
* <span data-ttu-id="91fff-187">Modifier la **largeur de cellule** à 0,25 pour espacer les cubes dans la ligne</span><span class="sxs-lookup"><span data-stu-id="91fff-187">Change **Cell Width** to 0.25 to space out the cubes within the row</span></span>

<span data-ttu-id="91fff-188">Cliquez ensuite sur le bouton **mettre à jour la collection** pour appliquer la nouvelle configuration :</span><span class="sxs-lookup"><span data-stu-id="91fff-188">Then click the **Update Collection** button to apply the new configuration:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step5-2.png)

### <a name="6-add-the-move-with-pan-script-component"></a><span data-ttu-id="91fff-190">6. ajouter le composant déplacer avec le panoramique (script)</span><span class="sxs-lookup"><span data-stu-id="91fff-190">6. Add the Move With Pan (Script) component</span></span>

<span data-ttu-id="91fff-191">Dans la fenêtre hiérarchie, sélectionnez tous les **objets enfants du cube**, puis dans la fenêtre de l’inspecteur, utilisez le bouton **Ajouter un composant** pour ajouter le composant **déplacer avec le panoramique (script)** à tous les cubes :</span><span class="sxs-lookup"><span data-stu-id="91fff-191">In the Hierarchy window, select all the **Cube child objects**, then in the Inspector window, use the **Add Component** button to add the **Move With Pan (Script)** component to all the cubes:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-1.png)

> [!TIP]
> <span data-ttu-id="91fff-193">Pour obtenir un rappel sur la sélection de plusieurs objets dans la fenêtre hiérarchie, les conditions d’utilisation peuvent faire référence au [composant Ajouter le gestionnaire de manipulation (script) à toutes les instructions d’objets](mrlearning-base-ch4.md#1-add-the-manipulation-handler-script-component-to-all-the-objects) .</span><span class="sxs-lookup"><span data-stu-id="91fff-193">For a reminder on how to select multiple objects in the Hierarchy window, tou can refer to the [Add the Manipulation Handler (Script) component to all the objects](mrlearning-base-ch4.md#1-add-the-manipulation-handler-script-component-to-all-the-objects) instructions.</span></span>

<span data-ttu-id="91fff-194">Avec tous les cubes toujours sélectionnés, cliquez sur l’objet **PanGesture** et faites-le glisser vers le champ **source d’entrée de panoramique** :</span><span class="sxs-lookup"><span data-stu-id="91fff-194">With all the cubes still selected, click-and-drag the **PanGesture** object to the **Pan Input Source** field:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-2.png)

> [!TIP]
> <span data-ttu-id="91fff-196">Le composant Move with Pan (script) sur chaque cube écoute l’événement Pan updated envoyé par le composant HandInteractionPanZoom (script) sur l’objet PanGesture, que vous avez affecté comme source d’entrée Pan à l’étape ci-dessus et met à jour la position de chaque cube en conséquence.</span><span class="sxs-lookup"><span data-stu-id="91fff-196">The Move With Pan (Script) component on each cube listens for the Pan Updated event sent by the HandInteractionPanZoom (Script) component on the PanGesture object, which you assigned as the Pan Input Source in the step above, and updates each cube's position accordingly.</span></span>

<span data-ttu-id="91fff-197">Dans la fenêtre hiérarchie, sélectionnez l’objet **PanGesture** , puis dans l’inspecteur désactivez la case à **cocher** **convertisseur de maillage** pour désactiver le composant de rendu de maille :</span><span class="sxs-lookup"><span data-stu-id="91fff-197">In the Hierarchy window, select the **PanGesture** object, then in the inspector **un-check** the **Mesh Renderer** checkbox to disable the Mesh Renderer component:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-3.png)

<span data-ttu-id="91fff-199">Si vous passez maintenant en mode jeu, vous pouvez tester le défilement du contenu 3D à l’aide du mouvement panoramique de la simulation dans l’éditeur :</span><span class="sxs-lookup"><span data-stu-id="91fff-199">If you now enter Game mode, you can test scrolling the 3D content using the pan gesture in the in-editor simulation:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-4.png)

## <a name="eye-tracking"></a><span data-ttu-id="91fff-201">Eye-tracking</span><span class="sxs-lookup"><span data-stu-id="91fff-201">Eye Tracking</span></span>

<span data-ttu-id="91fff-202">Dans cette section, vous allez découvrir comment activer le suivi visuel dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="91fff-202">In this section, you will explore how to enable eye tracking in your project.</span></span> <span data-ttu-id="91fff-203">Pour cet exemple, vous allez implémenter une fonctionnalité permettant de faire en sorte que chaque objet de la 3DObjectCollection tourne lentement tout en étant examiné par le point de vue des yeux de l’utilisateur, ainsi que de déclencher un effet de spot lorsque l’objet examiné est sélectionné par un TAP ou une commande vocale.</span><span class="sxs-lookup"><span data-stu-id="91fff-203">For this example, you will implement functionality to make each object in the 3DObjectCollection spin slowly while being looked at by the user's eye gaze, as well as, trigger a blip effect when the object being looked at is selected by air-tap or speech command.</span></span>

<span data-ttu-id="91fff-204">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="91fff-204">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="91fff-205">Ajouter le composant de cible de suivi oculaire (script) à tous les objets cibles</span><span class="sxs-lookup"><span data-stu-id="91fff-205">Add the Eye Tracking Target (Script) component to all target objects</span></span>
2. <span data-ttu-id="91fff-206">Ajouter le composant de démonstration du didacticiel de suivi oculaire (script) à tous les objets cibles</span><span class="sxs-lookup"><span data-stu-id="91fff-206">Add the Eye Tracking Tutorial Demo (Script) component  to all target objects</span></span>
3. <span data-ttu-id="91fff-207">Implémenter le tout en examinant l’événement cible</span><span class="sxs-lookup"><span data-stu-id="91fff-207">Implement the While Looking At Target event</span></span>
4. <span data-ttu-id="91fff-208">Implémenter l’événement sur sélectionné</span><span class="sxs-lookup"><span data-stu-id="91fff-208">Implement the On Selected event</span></span>
5. <span data-ttu-id="91fff-209">Activer le suivi oculaire simulé pour les simulations dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="91fff-209">Enable simulated eye tracking for in-editor simulations</span></span>
6. <span data-ttu-id="91fff-210">Activer l’entrée de regard dans les fonctionnalités de l’application du projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="91fff-210">Enable Gaze Input in the Visual Studio project's app capabilities</span></span>

### <a name="1-add-the-eye-tracking-target-script-component-to-all-target-objects"></a><span data-ttu-id="91fff-211">1. ajouter le composant cible de suivi des yeux (script) à tous les objets cibles</span><span class="sxs-lookup"><span data-stu-id="91fff-211">1. Add the Eye Tracking Target (Script) component to all target objects</span></span>

<span data-ttu-id="91fff-212">Dans la fenêtre hiérarchie, développez l’objet **3DObjectCollection** et sélectionnez tous les **objets enfants**, puis dans la fenêtre de l’inspecteur, utilisez le bouton **Ajouter un composant** pour ajouter le composant de cible de **suivi oculaire (script)** à tous les objets enfants :</span><span class="sxs-lookup"><span data-stu-id="91fff-212">In the Hierarchy window, expand the **3DObjectCollection** object and select all the **child objects**, then in the Inspector window, use the **Add Component** button to add the **Eye Tracking Target (Script)** component to all the child objects:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step1-1.png)

<span data-ttu-id="91fff-214">Lorsque tous les **objets enfants** sont toujours sélectionnés, configurez le composant **cible de suivi oculaire (script)** comme suit :</span><span class="sxs-lookup"><span data-stu-id="91fff-214">With all the **child objects** still selected, configure the **Eye Tracking Target (Script)** component as follows:</span></span>

* <span data-ttu-id="91fff-215">Modifiez **Sélectionner l’action** à **Sélectionner**pour définir l’action d’appui à l’air pour cet objet comme SELECT</span><span class="sxs-lookup"><span data-stu-id="91fff-215">Change **Select Action** to **Select**, to define the air-tap action for this object as Select</span></span>
* <span data-ttu-id="91fff-216">Développez **Voice Select** et définissez la **taille** de la liste de commandes vocale sur 1, puis, dans la nouvelle liste d’éléments qui s’affiche, remplacez l' **élément 0** par **Select**, afin de définir l’action de commande vocale pour cet objet comme SELECT</span><span class="sxs-lookup"><span data-stu-id="91fff-216">Expand **Voice Select** and set the voice command list **Size** to 1, and then, in the new element list that appear, change **Element 0** to **Select**, to define the speech command action for this object as Select</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step1-2.png)

### <a name="2-add-the-eye-tracking-tutorial-demo-script-component--to-all-target-objects"></a><span data-ttu-id="91fff-218">2. ajouter le composant de démonstration du didacticiel de suivi oculaire (script) à tous les objets cibles</span><span class="sxs-lookup"><span data-stu-id="91fff-218">2. Add the Eye Tracking Tutorial Demo (Script) component  to all target objects</span></span>

<span data-ttu-id="91fff-219">Lorsque tous les **objets enfants** sont toujours sélectionnés, utilisez le bouton **Ajouter un composant** pour ajouter le composant démonstration du **didacticiel de suivi oculaire (script)** à tous les objets enfants :</span><span class="sxs-lookup"><span data-stu-id="91fff-219">With all the **child objects** still selected, use the **Add Component** button to add the **Eye Tracking Tutorial Demo (Script)** component to all the child objects:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step2-1.png)

> [!NOTE]
> <span data-ttu-id="91fff-221">Le composant cible de suivi oculaire (script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="91fff-221">The Eye Tracking Target (Script) component is not part of MRTK.</span></span> <span data-ttu-id="91fff-222">Il a été fourni avec les ressources de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="91fff-222">It was provided with this tutorial's assets.</span></span>

### <a name="3-implement-the-while-looking-at-target-event"></a><span data-ttu-id="91fff-223">3. implémentez le tout en examinant l’événement cible</span><span class="sxs-lookup"><span data-stu-id="91fff-223">3. Implement the While Looking At Target event</span></span>

<span data-ttu-id="91fff-224">Dans la fenêtre hiérarchie, sélectionnez l’objet **fromage** , puis créez un événement **tout en regardant à la cible ()** , configurez l’objet **fromage** pour recevoir l’événement et définissez **EyeTrackingTutorialDemo. RotateTarget** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="91fff-224">In the Hierarchy window, select the **Cheese** object, then create a new **While Looking At Target ()** event, configure the **Cheese** object to receive the event, and define **EyeTrackingTutorialDemo.RotateTarget** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step3-1.png)

<span data-ttu-id="91fff-226">**Répétez cette opération** pour chacun des objets enfants du 3DObjectCollection.</span><span class="sxs-lookup"><span data-stu-id="91fff-226">**Repeat** for each of the child objects in the 3DObjectCollection.</span></span>

> [!TIP]
> <span data-ttu-id="91fff-227">Pour obtenir un rappel sur la façon d’implémenter des événements, vous pouvez consulter les instructions de suivi de la [main et les boutons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) interactifs.</span><span class="sxs-lookup"><span data-stu-id="91fff-227">For a reminder on how to implement events, you can refer to the [Hand tracking gestures and interactable buttons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) instructions.</span></span>

### <a name="4-implement-the-on-selected-event"></a><span data-ttu-id="91fff-228">4. implémentez l’événement sur sélectionné</span><span class="sxs-lookup"><span data-stu-id="91fff-228">4. Implement the On Selected event</span></span>

<span data-ttu-id="91fff-229">Dans la fenêtre hiérarchie, sélectionnez l’objet **fromage** , puis créer un événement **sur sélectionné ()** , configurez l’objet **fromage** pour recevoir l’événement et définissez **EyeTrackingTutorialDemo. BlipTarget** comme action à déclencher :</span><span class="sxs-lookup"><span data-stu-id="91fff-229">In the Hierarchy window, select the **Cheese** object, then create a new **On Selected ()** event, configure the **Cheese** object to receive the event, and define **EyeTrackingTutorialDemo.BlipTarget** as the action to be triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step4-1.png)

<span data-ttu-id="91fff-231">**Répétez cette opération** pour chacun des objets enfants du 3DObjectCollection.</span><span class="sxs-lookup"><span data-stu-id="91fff-231">**Repeat** for each of the child objects in the 3DObjectCollection.</span></span>

### <a name="5-enable-simulated-eye-tracking-for-in-editor-simulations"></a><span data-ttu-id="91fff-232">5. activer le suivi oculaire simulé pour les simulations dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="91fff-232">5. Enable simulated eye tracking for in-editor simulations</span></span>

<span data-ttu-id="91fff-233">Dans la fenêtre hiérarchie, sélectionnez l’objet **MixedRealityToolkit** , puis dans la fenêtre de l’inspecteur, sélectionnez l’onglet **entrée** , développez la section **fournisseurs de données d’entrée** , puis la section **service de simulation d’entrée** , puis clonez le **DefaultMixedRealityInputSimulationProfile** pour le remplacer par votre **profil de simulation d’entrée**personnalisable :</span><span class="sxs-lookup"><span data-stu-id="91fff-233">In the Hierarchy window, select the **MixedRealityToolkit** object, then in the Inspector window, select the **Input** tab, expand the **Input Data Providers** section and then the **Input Simulation Service** section, and clone the **DefaultMixedRealityInputSimulationProfile** to replace it with your own customizable **Input Simulation Profile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step5-1.png)

> [!TIP]
> <span data-ttu-id="91fff-235">Pour obtenir un rappel sur la façon de cloner des profils MRTK, vous pouvez consulter les instructions de [Configuration des profils de la boîte à outils de la réalité mixte](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) .</span><span class="sxs-lookup"><span data-stu-id="91fff-235">For a reminder on how to clone MRTK profiles, you can refer to the [How to configure the Mixed Reality Toolkit Profiles](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) instructions.</span></span>

<span data-ttu-id="91fff-236">Dans la section **simulation oculaire** , activez la case à cocher **simuler la position des yeux** pour activer la simulation du suivi oculaire :</span><span class="sxs-lookup"><span data-stu-id="91fff-236">In the **Eye Simulation** section, check the **Simulate Eye Position** checkbox to enable eye tracking simulation:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step5-2.png)

<span data-ttu-id="91fff-238">Si vous entrez maintenant le mode jeu, vous pouvez tester les effets de spin et de spot que vous avez implémentés en ajustant la vue afin que le curseur atteigne l’un des objets et en utilisant une interaction manuelle ou une commande vocale pour sélectionner l’objet :</span><span class="sxs-lookup"><span data-stu-id="91fff-238">If you now enter Game mode, you can test the spin and blip effects you implemented by adjusting the view so the cursor hits one of the objects and using hand interaction or speech command to select the object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step5-3.png)

> [!NOTE]
> <span data-ttu-id="91fff-240">Si vous n’avez pas utilisé DefaultHoloLens2ConfigurationProfile pour cloner votre profil de configuration MRTK personnalisable, comme indiqué dans les instructions [configurer les outils de réalité mixte](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) , le suivi des yeux peut ne pas être activé dans votre projet et doit être activé.</span><span class="sxs-lookup"><span data-stu-id="91fff-240">If you did not use the DefaultHoloLens2ConfigurationProfile to clone your customizable MRTK configuration profile, as instructed in the [Configure the Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) instructions, eye tracking may not be enable in your project and will need to be enabled.</span></span> <span data-ttu-id="91fff-241">Pour cela, vous pouvez vous reporter au [Guide de prise en main du suivi oculaire dans MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html) .</span><span class="sxs-lookup"><span data-stu-id="91fff-241">For that, you can refer to the [Getting started with eye tracking in MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html) instructions.</span></span>

### <a name="6-enable-gaze-input-in-the-visual-studio-projects-app-capabilities"></a><span data-ttu-id="91fff-242">6. activer l’entrée de regard dans les fonctionnalités de l’application du projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="91fff-242">6. Enable Gaze Input in the Visual Studio project's app capabilities</span></span>

<span data-ttu-id="91fff-243">Avant de générer et de déployer votre application à partir de Visual Studio sur votre appareil, le point d’entrée de regard doit être activé dans les fonctionnalités de l’application du projet.</span><span class="sxs-lookup"><span data-stu-id="91fff-243">Before building and deploying your app from Visual Studio to your device, Gaze Input has to been enabled in the project's app capabilities.</span></span> <span data-ttu-id="91fff-244">Pour ce faire, vous pouvez suivre le [test de votre application Unity sur les instructions HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#testing-your-unity-app-on-a-hololens-2) .</span><span class="sxs-lookup"><span data-stu-id="91fff-244">For this, you can follow the [Testing your Unity app on a HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#testing-your-unity-app-on-a-hololens-2) instructions.</span></span>

## <a name="congratulations"></a><span data-ttu-id="91fff-245">Félicitations</span><span class="sxs-lookup"><span data-stu-id="91fff-245">Congratulations</span></span>

<span data-ttu-id="91fff-246">Vous avez ajouté avec succès des fonctionnalités de suivi des yeux de base à votre application.</span><span class="sxs-lookup"><span data-stu-id="91fff-246">You have successfully added basic eye tracking capabilities to your application.</span></span> <span data-ttu-id="91fff-247">Ces premiers pas vous ouvrent la voie vers tout un monde de possibilités avec l’eye-tracking.</span><span class="sxs-lookup"><span data-stu-id="91fff-247">These actions are only the beginning of a world of possibilities with eye tracking.</span></span> <span data-ttu-id="91fff-248">Dans ce didacticiel, vous avez également appris les autres fonctionnalités d’entrée avancées, telles que les commandes vocales et les gestes de panoramique.</span><span class="sxs-lookup"><span data-stu-id="91fff-248">In this tutorial, you also learned about other advanced input features, such as voice commands and panning gestures.</span></span>

[<span data-ttu-id="91fff-249">Leçon suivante : 7. création d’un exemple d’application de module lunaire</span><span class="sxs-lookup"><span data-stu-id="91fff-249">Next Lesson: 7. Creating a Lunar Module sample application</span></span>](mrlearning-base-ch6.md)
