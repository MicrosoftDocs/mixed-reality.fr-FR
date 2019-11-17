---
title: Objet interagi
description: Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait en 2D. Dans le monde de la réalité mixte en trois dimensions, nous n’avons plus à limiter le monde de l’abstraction.
author: cre8ivepark
ms.author: jennyk
ms.date: 06/06/2019
ms.topic: article
keywords: Réalité mixte, contrôles, interaction, interface utilisateur, expérience utilisateur
ms.openlocfilehash: 73c8a3ce9e01f580ecbae23f2178871642c4540e
ms.sourcegitcommit: 17427d4d8c3723d53540f1b7f5bc061bba08c1d6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2019
ms.locfileid: "74143260"
---
# <a name="interactable-object"></a><span data-ttu-id="5eaac-105">Objet interagi</span><span class="sxs-lookup"><span data-stu-id="5eaac-105">Interactable object</span></span>

![Objets Interactible](images/UX/UX_Hero_Interactable.jpg)

<span data-ttu-id="5eaac-107">Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait en 2D.</span><span class="sxs-lookup"><span data-stu-id="5eaac-107">A button has long been a metaphor used for triggering an event in the 2D abstract world.</span></span> <span data-ttu-id="5eaac-108">Dans le monde de la réalité mixte en trois dimensions, nous n’avons plus à limiter le monde de l’abstraction.</span><span class="sxs-lookup"><span data-stu-id="5eaac-108">In the three-dimensional mixed reality world, we don’t have to be confined to this world of abstraction anymore.</span></span> <span data-ttu-id="5eaac-109">Tout peut être un **objet** pouvant être utilisé qui déclenche un événement.</span><span class="sxs-lookup"><span data-stu-id="5eaac-109">Anything can be an **interactable object** that triggers an event.</span></span> <span data-ttu-id="5eaac-110">Un objet pouvant être en interaction peut être représenté sous la forme d’un objet à partir d’une tasse de café sur la table.</span><span class="sxs-lookup"><span data-stu-id="5eaac-110">An interactable object can be represented as anything from a coffee cup on the table to a balloon floating in the air.</span></span> <span data-ttu-id="5eaac-111">Nous utilisons toujours les boutons traditionnels dans certaines situations, par exemple dans l’interface utilisateur du dialogue.</span><span class="sxs-lookup"><span data-stu-id="5eaac-111">We still do make use of traditional buttons in certain situation such as in dialog UI.</span></span> <span data-ttu-id="5eaac-112">La représentation visuelle du bouton dépend du contexte.</span><span class="sxs-lookup"><span data-stu-id="5eaac-112">The visual representation of the button depends on the context.</span></span>

<br>

---


## <a name="important-properties-of-the-interactable-object"></a><span data-ttu-id="5eaac-113">Propriétés importantes de l’objet interagiable</span><span class="sxs-lookup"><span data-stu-id="5eaac-113">Important properties of the interactable object</span></span>

### <a name="visual-cues"></a><span data-ttu-id="5eaac-114">Signaux visuels</span><span class="sxs-lookup"><span data-stu-id="5eaac-114">Visual cues</span></span>

<span data-ttu-id="5eaac-115">Les signaux visuels sont des signaux sensorielles reçus par l’oeil sous forme de lumière et traités par le système visuel lors de la perception visuelle.</span><span class="sxs-lookup"><span data-stu-id="5eaac-115">Visual cues are sensory cues received by the eye in the form of light and processed by the visual system during visual perception.</span></span> <span data-ttu-id="5eaac-116">Étant donné que le système visuel est dominant dans de nombreuses espèces, en particulier les êtres humains, les signaux visuels constituent une source d’informations importante dans la manière dont le monde est perçu.</span><span class="sxs-lookup"><span data-stu-id="5eaac-116">Since the visual system is dominant in many species, especially humans, visual cues are a large source of information in how the world is perceived.</span></span>

<span data-ttu-id="5eaac-117">Étant donné que les objets holographiques sont mélangés à l’environnement réel dans la réalité mixte, il peut être difficile de comprendre les objets avec lesquels vous pouvez interagir.</span><span class="sxs-lookup"><span data-stu-id="5eaac-117">Since the holographic objects are blended with the real-world environment in mixed reality, it could be difficult to understand which objects you can interact with.</span></span> <span data-ttu-id="5eaac-118">Pour tous les objets interactifs dans votre expérience, il est important de fournir des signaux visuels différenciés pour chaque État d’entrée.</span><span class="sxs-lookup"><span data-stu-id="5eaac-118">For any interactable objects in your experience, it is important to provide differentiated visual cues for each input state.</span></span> <span data-ttu-id="5eaac-119">Cela permet à l’utilisateur de comprendre quelle partie de votre expérience est interactive et de rendre l’utilisateur confiant en utilisant une méthode d’interaction cohérente.</span><span class="sxs-lookup"><span data-stu-id="5eaac-119">This helps the user understand which part of your experience is interactable and makes the user confident by using a consistent interaction method.</span></span>

<br>

---

### <a name="far-interactions"></a><span data-ttu-id="5eaac-120">Interactions lointaines</span><span class="sxs-lookup"><span data-stu-id="5eaac-120">Far interactions</span></span>

<span data-ttu-id="5eaac-121">Pour tous les objets que l’utilisateur peut interagir avec le point de vue du point de vue du regard, du rayon de la main et du contrôleur de mouvement, nous vous recommandons d’avoir un signal visuel différent pour ces trois États d’entrée :</span><span class="sxs-lookup"><span data-stu-id="5eaac-121">For any objects that user can interact with gaze, hand ray, and motion controller's ray, we recommend to have different visual cue for these three input states:</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="5eaac-122">![interactibleobject-States-](images/interactibleobject-states-default.jpg) par défaut</span><span class="sxs-lookup"><span data-stu-id="5eaac-122">![interactibleobject-states-default](images/interactibleobject-states-default.jpg)</span></span><br>
       <span data-ttu-id="5eaac-123">**État par défaut (observation)**</span><span class="sxs-lookup"><span data-stu-id="5eaac-123">**Default (Observation) state**</span></span><br>
        <span data-ttu-id="5eaac-124">État d’inactivité par défaut de l’objet.</span><span class="sxs-lookup"><span data-stu-id="5eaac-124">Default idle state of the object.</span></span>
    <span data-ttu-id="5eaac-125">Le curseur ne se trouve pas sur l’objet.</span><span class="sxs-lookup"><span data-stu-id="5eaac-125">The cursor is not on the object.</span></span> <span data-ttu-id="5eaac-126">La main n’est pas détectée.</span><span class="sxs-lookup"><span data-stu-id="5eaac-126">Hand is not detected.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="5eaac-127">![interactibleobject-États-ciblés](images/interactibleobject-states-targeted.jpg)</span><span class="sxs-lookup"><span data-stu-id="5eaac-127">![interactibleobject-states-targeted](images/interactibleobject-states-targeted.jpg)</span></span><br>
        <span data-ttu-id="5eaac-128">**État ciblé (survol)**</span><span class="sxs-lookup"><span data-stu-id="5eaac-128">**Targeted (Hover) state**</span></span><br>
        <span data-ttu-id="5eaac-129">Lorsque l’objet est ciblé avec un curseur en forme de pointage, le pointeur de proximité d’un doigt ou d’un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="5eaac-129">When the object is targeted with gaze cursor, finger proximity or motion controller's pointer.</span></span>
    <span data-ttu-id="5eaac-130">Le curseur se trouve sur l’objet.</span><span class="sxs-lookup"><span data-stu-id="5eaac-130">The cursor is on the object.</span></span> <span data-ttu-id="5eaac-131">La main est détectée, prête.</span><span class="sxs-lookup"><span data-stu-id="5eaac-131">Hand is detected, ready.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="5eaac-132">![interactibleobject-l’utilisateur a appuyé sur](images/interactibleobject-states-pressed.jpg)</span><span class="sxs-lookup"><span data-stu-id="5eaac-132">![interactibleobject-states-pressed](images/interactibleobject-states-pressed.jpg)</span></span><br>
       <span data-ttu-id="5eaac-133">**État appuyé**</span><span class="sxs-lookup"><span data-stu-id="5eaac-133">**Pressed state**</span></span><br>
        <span data-ttu-id="5eaac-134">Quand l’objet est enfoncé avec un mouvement d’appui sur l’air, appuyez sur le bouton de sélection du contrôleur de mouvement ou du doigt.</span><span class="sxs-lookup"><span data-stu-id="5eaac-134">When the object is pressed with an air tap gesture, finger press or motion controller's select button.</span></span>
    <span data-ttu-id="5eaac-135">Le curseur se trouve sur l’objet.</span><span class="sxs-lookup"><span data-stu-id="5eaac-135">The cursor is on the object.</span></span> <span data-ttu-id="5eaac-136">La main est détectée, frappée d’air.</span><span class="sxs-lookup"><span data-stu-id="5eaac-136">Hand is detected, air tapped.</span></span>
    :::column-end:::
:::row-end:::

<br>

---

<span data-ttu-id="5eaac-137">Vous pouvez utiliser des techniques telles que la mise en surbrillance ou la mise à l’échelle pour fournir des signaux visuels pour l’état d’entrée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5eaac-137">You can use techniques such as highlighting or scaling to provide visual cues for the user’s input state.</span></span> <span data-ttu-id="5eaac-138">En réalité mixte, vous trouverez les exemples de visualisation des différents États d’entrée dans le menu Démarrer et avec les boutons de la barre d’application.</span><span class="sxs-lookup"><span data-stu-id="5eaac-138">In mixed reality, you can find the examples of visualizing different input states on the Start menu and with app bar buttons.</span></span> 

<span data-ttu-id="5eaac-139">Voici à quoi ressemblent ces États sur un **bouton holographique**:</span><span class="sxs-lookup"><span data-stu-id="5eaac-139">Here is what these states look like on a **holographic button**:</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="5eaac-140">![interactibleobject-States-](images/MRTK_InteractableState-default.jpg) par défaut</span><span class="sxs-lookup"><span data-stu-id="5eaac-140">![interactibleobject-states-default](images/MRTK_InteractableState-default.jpg)</span></span><br>
       <span data-ttu-id="5eaac-141">**État par défaut (observation)**</span><span class="sxs-lookup"><span data-stu-id="5eaac-141">**Default (Observation) state**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="5eaac-142">![interactibleobject-États-ciblés](images/MRTK_InteractableState-targeted.jpg)</span><span class="sxs-lookup"><span data-stu-id="5eaac-142">![interactibleobject-states-targeted](images/MRTK_InteractableState-targeted.jpg)</span></span><br>
        <span data-ttu-id="5eaac-143">**État ciblé (survol)**</span><span class="sxs-lookup"><span data-stu-id="5eaac-143">**Targeted (Hover) state**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="5eaac-144">![interactibleobject-l’utilisateur a appuyé sur](images/MRTK_InteractableState-pressed.jpg)</span><span class="sxs-lookup"><span data-stu-id="5eaac-144">![interactibleobject-states-pressed](images/MRTK_InteractableState-pressed.jpg)</span></span><br>
       <span data-ttu-id="5eaac-145">**État appuyé**</span><span class="sxs-lookup"><span data-stu-id="5eaac-145">**Pressed state**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

### <a name="near-interactions-direct"></a><span data-ttu-id="5eaac-146">Interactions proches (direct)</span><span class="sxs-lookup"><span data-stu-id="5eaac-146">Near interactions (direct)</span></span> 

<span data-ttu-id="5eaac-147">HoloLens 2 prend en charge l’entrée de suivi articulée qui vous permet d’interagir avec les objets.</span><span class="sxs-lookup"><span data-stu-id="5eaac-147">HoloLens 2 supports articulated hand tracking input which allows you to interact with objects.</span></span> <span data-ttu-id="5eaac-148">Sans commentaires haptique et perception parfaite de la profondeur, il peut parfois être difficile de savoir à quel moment votre main provient d’un objet ou si vous le touchez.</span><span class="sxs-lookup"><span data-stu-id="5eaac-148">Without haptic feedback and perfect depth perception, it can sometimes be hard to tell how far away your hand is from an object or whether you are touching it.</span></span> <span data-ttu-id="5eaac-149">Il est important de fournir suffisamment de signaux visuels pour communiquer l’état de l’objet et, en particulier, l’état de vos mains par rapport à cet objet.</span><span class="sxs-lookup"><span data-stu-id="5eaac-149">It is important to provide enough visual cues to communicate the state of the object and in particular the state of your hands in relation to that object.</span></span>

<span data-ttu-id="5eaac-150">Utilisez les commentaires visuels pour communiquer les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5eaac-150">Use visual feedback to communicate the following:</span></span>
* <span data-ttu-id="5eaac-151">**Valeur par défaut (observation)** : état inactif par défaut de l’objet.</span><span class="sxs-lookup"><span data-stu-id="5eaac-151">**Default (Observation)**: Default idle state of the object.</span></span>
* <span data-ttu-id="5eaac-152">**Survol**: quand une main est proche d’un hologramme, modifiez les éléments visuels pour indiquer que la main cible l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="5eaac-152">**Hover**: When a hand is near a hologram, change visuals to communicate that hand is targeting hologram.</span></span> 
* <span data-ttu-id="5eaac-153">**Distance et point d’interaction**: comme la main s’approche d’un hologramme, concevoir des commentaires pour communiquer le point d’interaction projeté, ainsi que la distance entre l’objet et le doigt</span><span class="sxs-lookup"><span data-stu-id="5eaac-153">**Distance and point of interaction**: As the hand approaches a hologram, design feedback to communicate the projected point of interaction, as well as how far from the object the finger is</span></span>
* <span data-ttu-id="5eaac-154">**Début du contact**: modifiez les éléments visuels (Light, Color) pour signaler qu’une pression tactile s’est produite.</span><span class="sxs-lookup"><span data-stu-id="5eaac-154">**Contact begins**: Change visuals (light, color) to communicate that a touch has occurred</span></span>
* <span data-ttu-id="5eaac-155">**Saisi**: modifier les éléments visuels (clair, couleur) quand l’objet est saisi</span><span class="sxs-lookup"><span data-stu-id="5eaac-155">**Grasped**: Change visuals (light, color) when the object is grasped</span></span>
* <span data-ttu-id="5eaac-156">**Fin du contact**: modifier les éléments visuels (Light, Color) quand Touch est terminé</span><span class="sxs-lookup"><span data-stu-id="5eaac-156">**Contact ends**: Change visuals (light, color) when touch has ended</span></span>

<br>

---

:::row:::
    :::column:::
        <span data-ttu-id="5eaac-157">![pointage (FAR)](images/640px-interactibleobject-states-near-hover.jpg)</span><span class="sxs-lookup"><span data-stu-id="5eaac-157">![Hover (Far)](images/640px-interactibleobject-states-near-hover.jpg)</span></span><br>
        <span data-ttu-id="5eaac-158">**Pointage (FAR)**</span><span class="sxs-lookup"><span data-stu-id="5eaac-158">**Hover (Far)**</span></span><br>
        <span data-ttu-id="5eaac-159">Mise en surbrillance en fonction de la proximité de la main.</span><span class="sxs-lookup"><span data-stu-id="5eaac-159">Highlighting based on the proximity of the hand.</span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="5eaac-160">Pointage de ![(Near)](images/640px-interactibleobject-states-near-hovernear.jpg)</span><span class="sxs-lookup"><span data-stu-id="5eaac-160">![Hover (Near)](images/640px-interactibleobject-states-near-hovernear.jpg)</span></span><br>
        <span data-ttu-id="5eaac-161">**Pointage (Near)**</span><span class="sxs-lookup"><span data-stu-id="5eaac-161">**Hover (Near)**</span></span><br>
        <span data-ttu-id="5eaac-162">Mettez en surbrillance les changements de taille en fonction de la distance à la main.</span><span class="sxs-lookup"><span data-stu-id="5eaac-162">Highlight size changes based on the distance to the hand.</span></span>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        <span data-ttu-id="5eaac-163">![toucher/appuyer](images/640px-interactibleobject-states-near-press.jpg)</span><span class="sxs-lookup"><span data-stu-id="5eaac-163">![Touch / press](images/640px-interactibleobject-states-near-press.jpg)</span></span><br>
        <span data-ttu-id="5eaac-164">**Toucher/appuyer**</span><span class="sxs-lookup"><span data-stu-id="5eaac-164">**Touch / press**</span></span><br>
        <span data-ttu-id="5eaac-165">Commentaires Audio Visual plus.</span><span class="sxs-lookup"><span data-stu-id="5eaac-165">Visual plus audio feedback.</span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="5eaac-166">![](images/640px-interactibleobject-states-near-grasp.jpg)</span><span class="sxs-lookup"><span data-stu-id="5eaac-166">![Grasp](images/640px-interactibleobject-states-near-grasp.jpg)</span></span><br>
        <span data-ttu-id="5eaac-167">**Maîtriser**</span><span class="sxs-lookup"><span data-stu-id="5eaac-167">**Grasp**</span></span><br>
        <span data-ttu-id="5eaac-168">Commentaires Audio Visual plus.</span><span class="sxs-lookup"><span data-stu-id="5eaac-168">Visual plus audio feedback.</span></span>
    :::column-end:::
:::row-end:::

<br>

<br>

---

<span data-ttu-id="5eaac-169">Un [bouton sur HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html) est un exemple de la façon dont les différents États d’interaction d’entrée sont visualisés :</span><span class="sxs-lookup"><span data-stu-id="5eaac-169">A [button on HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html) is an example of how the different input interaction states are visualized:</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="5eaac-170">![la](images/640px-interactibleobject-pressablebutton-default.jpg) par défaut</span><span class="sxs-lookup"><span data-stu-id="5eaac-170">![Default](images/640px-interactibleobject-pressablebutton-default.jpg)</span></span><br>
        <span data-ttu-id="5eaac-171">**Valeurs**</span><span class="sxs-lookup"><span data-stu-id="5eaac-171">**Default**</span></span><br>
    :::column-end:::
    :::column:::
        <span data-ttu-id="5eaac-172">Pointage de ![](images/640px-interactibleobject-pressablebutton-hover.jpg)</span><span class="sxs-lookup"><span data-stu-id="5eaac-172">![Hover](images/640px-interactibleobject-pressablebutton-hover.jpg)</span></span><br>
        <span data-ttu-id="5eaac-173">**Pointez**</span><span class="sxs-lookup"><span data-stu-id="5eaac-173">**Hover**</span></span><br>
        <span data-ttu-id="5eaac-174">Révélez un effet d’éclairage basé sur la proximité.</span><span class="sxs-lookup"><span data-stu-id="5eaac-174">Reveal a proximity-based lighting effect.</span></span>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        <span data-ttu-id="5eaac-175">![Interface tactile](images/640px-interactibleobject-pressablebutton-touch.jpg)</span><span class="sxs-lookup"><span data-stu-id="5eaac-175">![Touch](images/640px-interactibleobject-pressablebutton-touch.jpg)</span></span><br>
        <span data-ttu-id="5eaac-176">**Interface tactile**</span><span class="sxs-lookup"><span data-stu-id="5eaac-176">**Touch**</span></span><br>
        <span data-ttu-id="5eaac-177">Afficher l’effet de l’ondulation.</span><span class="sxs-lookup"><span data-stu-id="5eaac-177">Show ripple effect.</span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="5eaac-178">![Appuyez sur](images/640px-interactibleobject-pressablebutton-press.jpg)</span><span class="sxs-lookup"><span data-stu-id="5eaac-178">![Press](images/640px-interactibleobject-pressablebutton-press.jpg)</span></span><br>
        <span data-ttu-id="5eaac-179">**Compression**</span><span class="sxs-lookup"><span data-stu-id="5eaac-179">**Press**</span></span><br>
        <span data-ttu-id="5eaac-180">Déplacez la plaque avant.</span><span class="sxs-lookup"><span data-stu-id="5eaac-180">Move the front plate.</span></span>
    :::column-end:::
:::row-end:::

<br>

---

:::row:::
    :::column:::
        ### <a name="the-ring-visual-cue-on-hololens-2br"></a><span data-ttu-id="5eaac-181">Le signal visuel « Ring » sur HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="5eaac-181">The "ring" visual cue on HoloLens 2</span></span><br>
        <span data-ttu-id="5eaac-182">Sur HoloLens 2, il existe un signal visuel supplémentaire qui peut aider la perception de l’utilisateur en profondeur.</span><span class="sxs-lookup"><span data-stu-id="5eaac-182">On HoloLens 2, there is an additional visual cue which can help the user's perception of depth.</span></span> <span data-ttu-id="5eaac-183">Un anneau proche de son doigt s’affiche et s’adapte à mesure que l’approche est plus proche de l’objet.</span><span class="sxs-lookup"><span data-stu-id="5eaac-183">A ring near their fingertip shows up and scales down as the fingertip gets closer to the object.</span></span> <span data-ttu-id="5eaac-184">L’anneau se convergera en un point lorsque l’état appuyé est atteint.</span><span class="sxs-lookup"><span data-stu-id="5eaac-184">The ring eventually converges into a dot when the pressed state is reached.</span></span> <span data-ttu-id="5eaac-185">Cet accord visuel aide l’utilisateur à comprendre à quel moment il s’agit de l’objet.</span><span class="sxs-lookup"><span data-stu-id="5eaac-185">This visual affordance helps the user understand how far they are from the object.</span></span><br>
        <br>
        <span data-ttu-id="5eaac-186">*Boucle vidéo : exemple de retour visuel basé sur la proximité d’un cadre englobant*</span><span class="sxs-lookup"><span data-stu-id="5eaac-186">*Video loop: Example of visual feedback based on proximity to a bounding box*</span></span>
    :::column-end:::
        :::column:::
        <span data-ttu-id="5eaac-187">espace de ![](images/spacer-20x582.png)</span><span class="sxs-lookup"><span data-stu-id="5eaac-187">![space](images/spacer-20x582.png)</span></span><br>
       <span data-ttu-id="5eaac-188">![des commentaires visuels à proximité](images/HoloLens2_Proximity.gif)</span><span class="sxs-lookup"><span data-stu-id="5eaac-188">![Visual feedback on hand proximity](images/HoloLens2_Proximity.gif)</span></span><br>
    :::column-end:::
:::row-end:::


<br>

---


### <a name="audio-cues"></a><span data-ttu-id="5eaac-189">Signaux audio</span><span class="sxs-lookup"><span data-stu-id="5eaac-189">Audio cues</span></span>

<span data-ttu-id="5eaac-190">Pour les interactions directes, les retours audio corrects peuvent améliorer considérablement l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5eaac-190">For direct hand interactions, proper audio feedback can dramatically improve the user experience.</span></span> <span data-ttu-id="5eaac-191">Utilisez les commentaires audio pour communiquer les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5eaac-191">Use audio feedback to communicate the following:</span></span>
* <span data-ttu-id="5eaac-192">**Début du contact**: émettre un signal sonore à la début de la saisie tactile</span><span class="sxs-lookup"><span data-stu-id="5eaac-192">**Contact begins**: Play sound when touch begins</span></span>
* <span data-ttu-id="5eaac-193">Fin du **contact**: émettre un signal sonore à l’extrémité tactile</span><span class="sxs-lookup"><span data-stu-id="5eaac-193">**Contact ends**: Play sound on touch end</span></span>
* <span data-ttu-id="5eaac-194">**Début**de la manipulation : émettre un signal sonore lors du démarrage de la manipulation</span><span class="sxs-lookup"><span data-stu-id="5eaac-194">**Grab begins**: Play sound when grab starts</span></span>
* <span data-ttu-id="5eaac-195">Opérations de **manipulation**: émettre un signal sonore lorsque la sélection est terminée</span><span class="sxs-lookup"><span data-stu-id="5eaac-195">**Grab ends**: Play sound when grab ends</span></span>

<br>

---

:::row:::
    :::column:::
        ### <a name="voice-commandingbr"></a><span data-ttu-id="5eaac-196">Commander avec la voix</span><span class="sxs-lookup"><span data-stu-id="5eaac-196">Voice commanding</span></span><br>
        <span data-ttu-id="5eaac-197">Pour tous les objets interactifs, il est important de prendre en charge d’autres options d’interaction.</span><span class="sxs-lookup"><span data-stu-id="5eaac-197">For any interactable objects, it is important to support alternative interaction options.</span></span> <span data-ttu-id="5eaac-198">Par défaut, nous vous recommandons de prendre en charge les [commandes vocales](voice-design.md) pour tous les objets qui sont interactifs.</span><span class="sxs-lookup"><span data-stu-id="5eaac-198">By default, we recommend that [voice commanding](voice-design.md) be supported for any objects that are interactable.</span></span> <span data-ttu-id="5eaac-199">Pour améliorer la détectabilité, vous pouvez également fournir une info-bulle pendant l’état de survol.</span><span class="sxs-lookup"><span data-stu-id="5eaac-199">To improve discoverability, you can also provide a tooltip during the hover state.</span></span><br>
        <br>
        <span data-ttu-id="5eaac-200">*Image : info-bulle pour la commande vocale*</span><span class="sxs-lookup"><span data-stu-id="5eaac-200">*Image: Tooltip for the voice command*</span></span>
    :::column-end:::
        :::column:::
       ![commandes vocales](images/640px-interactibleobject-voicecommand.png)<br>
    :::column-end:::
:::row-end:::


<br>

---


## <a name="sizing-recommendations"></a><span data-ttu-id="5eaac-202">Recommandations de dimensionnement</span><span class="sxs-lookup"><span data-stu-id="5eaac-202">Sizing recommendations</span></span> 

<span data-ttu-id="5eaac-203">Pour vous assurer que tous les objets interactifs peuvent facilement être manipulés par les utilisateurs, nous vous recommandons de vous assurer que l’interagissant est conforme à une taille minimale (l’angle visuel souvent mesuré en degrés d’arc visuel) en fonction de la distance qu’il est placée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5eaac-203">To ensure that all interactable objects can easily be touched by users, we recommend that you make sure the interactable meets a minimum size (the visual angle often measured in degrees of visual arc) based on the distance it is placed from the user.</span></span> <span data-ttu-id="5eaac-204">L’angle visuel est basé sur la distance entre les yeux de l’utilisateur et l’objet et reste constant, tandis que la taille physique de la cible peut changer en fonction de la distance entre les modifications de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5eaac-204">Visual angle is based on the distance between the user's eyes and the object and stays constant, while the physical size of the target may change as the distance from the user changes.</span></span> <span data-ttu-id="5eaac-205">Pour déterminer la taille physique nécessaire d’un objet en fonction de la distance de l’utilisateur, essayez d’utiliser une calculatrice d’angle visuel telle que celle- [ci](https://elvers.us/perception/visualAngle/).</span><span class="sxs-lookup"><span data-stu-id="5eaac-205">To determine the necessary physical size of an object based on the distance from the user, try using a visual angle calculator such as [this one](https://elvers.us/perception/visualAngle/).</span></span>

<span data-ttu-id="5eaac-206">Vous trouverez ci-dessous les recommandations relatives aux tailles minimales de contenu exploitable.</span><span class="sxs-lookup"><span data-stu-id="5eaac-206">Below are the recommendations for minimum sizes of interactable content.</span></span>


### <a name="target-size-for-direct-hand-interaction"></a><span data-ttu-id="5eaac-207">Taille cible pour l’interaction directe</span><span class="sxs-lookup"><span data-stu-id="5eaac-207">Target size for direct hand interaction</span></span>

| <span data-ttu-id="5eaac-208">Distance</span><span class="sxs-lookup"><span data-stu-id="5eaac-208">Distance</span></span> | <span data-ttu-id="5eaac-209">Angle d’affichage</span><span class="sxs-lookup"><span data-stu-id="5eaac-209">Viewing angle</span></span> | <span data-ttu-id="5eaac-210">Size</span><span class="sxs-lookup"><span data-stu-id="5eaac-210">Size</span></span> |
|---------|---------|---------|
| <span data-ttu-id="5eaac-211">45cm</span><span class="sxs-lookup"><span data-stu-id="5eaac-211">45cm</span></span>  | <span data-ttu-id="5eaac-212">non inférieur à 2 °</span><span class="sxs-lookup"><span data-stu-id="5eaac-212">no smaller than 2°</span></span> | <span data-ttu-id="5eaac-213">1,6 x 1,6 cm</span><span class="sxs-lookup"><span data-stu-id="5eaac-213">1.6 x 1.6 cm</span></span> |

<span data-ttu-id="5eaac-214">![taille cible pour l’interaction directe](images/TargetSizingNear.jpg)</span><span class="sxs-lookup"><span data-stu-id="5eaac-214">![Target size for direct hand interaction](images/TargetSizingNear.jpg)</span></span><br>
<span data-ttu-id="5eaac-215">*Taille cible pour l’interaction directe*</span><span class="sxs-lookup"><span data-stu-id="5eaac-215">*Target size for direct hand interaction*</span></span>

<br>

### <a name="target-size-for-buttons"></a><span data-ttu-id="5eaac-216">Taille cible pour les boutons</span><span class="sxs-lookup"><span data-stu-id="5eaac-216">Target size for buttons</span></span>

<span data-ttu-id="5eaac-217">Lorsque vous créez des boutons pour une interaction directe, nous vous recommandons une taille minimale supérieure de 3,2 x 3,2 cm pour garantir qu’il y a suffisamment d’espace pour contenir une icône et éventuellement du texte.</span><span class="sxs-lookup"><span data-stu-id="5eaac-217">When creating buttons for direct interaction, we recommend a larger minimum size of 3.2 x 3.2 cm to ensure that there is enough space to contain an icon and potentially some text.</span></span>

| <span data-ttu-id="5eaac-218">Distance</span><span class="sxs-lookup"><span data-stu-id="5eaac-218">Distance</span></span> | <span data-ttu-id="5eaac-219">Taille minimale</span><span class="sxs-lookup"><span data-stu-id="5eaac-219">Minimum size</span></span> |
|---------|---------|
| <span data-ttu-id="5eaac-220">45cm</span><span class="sxs-lookup"><span data-stu-id="5eaac-220">45cm</span></span>  | <span data-ttu-id="5eaac-221">3,2 x 3,2 cm</span><span class="sxs-lookup"><span data-stu-id="5eaac-221">3.2 x 3.2 cm</span></span> |

<span data-ttu-id="5eaac-222">![taille cible pour les boutons](images/TargetSizingButtons.png)</span><span class="sxs-lookup"><span data-stu-id="5eaac-222">![Target size for the buttons](images/TargetSizingButtons.png)</span></span><br>
<span data-ttu-id="5eaac-223">*Taille cible pour les boutons*</span><span class="sxs-lookup"><span data-stu-id="5eaac-223">*Target size for the buttons*</span></span>

<br>

### <a name="target-size-for-hand-ray-or-gaze-interaction"></a><span data-ttu-id="5eaac-224">Taille cible pour un rayon de la main ou une interaction du regard</span><span class="sxs-lookup"><span data-stu-id="5eaac-224">Target size for hand ray or gaze interaction</span></span>
| <span data-ttu-id="5eaac-225">Distance</span><span class="sxs-lookup"><span data-stu-id="5eaac-225">Distance</span></span> | <span data-ttu-id="5eaac-226">Angle d’affichage</span><span class="sxs-lookup"><span data-stu-id="5eaac-226">Viewing angle</span></span> | <span data-ttu-id="5eaac-227">Size</span><span class="sxs-lookup"><span data-stu-id="5eaac-227">Size</span></span> |
|---------|---------|---------|
| <span data-ttu-id="5eaac-228">dollars</span><span class="sxs-lookup"><span data-stu-id="5eaac-228">2m</span></span>  | <span data-ttu-id="5eaac-229">inférieur à 1 °</span><span class="sxs-lookup"><span data-stu-id="5eaac-229">no smaller than 1°</span></span> | <span data-ttu-id="5eaac-230">3,5 x 3,5 cm</span><span class="sxs-lookup"><span data-stu-id="5eaac-230">3.5 x 3.5 cm</span></span> |

<span data-ttu-id="5eaac-231">![taille cible pour les](images/TargetSizingFar.jpg) de rayon ou d’interaction de regard</span><span class="sxs-lookup"><span data-stu-id="5eaac-231">![Target size for hand ray or gaze interaction](images/TargetSizingFar.jpg)</span></span><br>
<span data-ttu-id="5eaac-232">*Taille cible pour un rayon de la main ou une interaction du regard*</span><span class="sxs-lookup"><span data-stu-id="5eaac-232">*Target size for hand ray or gaze interaction*</span></span>


<br>

---


## <a name="interactable-object-in-mrtkmixed-reality-toolkit-for-unit"></a><span data-ttu-id="5eaac-233">Objet interactif dans MRTK (ensemble d’outils de réalité mixte) pour l’unité</span><span class="sxs-lookup"><span data-stu-id="5eaac-233">Interactable object in MRTK(Mixed Reality Toolkit) for Unit</span></span>

<span data-ttu-id="5eaac-234">Dans **[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)** , vous pouvez utiliser le script en [**interaction**](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.SDK/Features/UX/Interactable/Scripts) pour faire en sorte que les objets répondent à différents types d’États d’interaction d’entrée.</span><span class="sxs-lookup"><span data-stu-id="5eaac-234">In **[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)**, you can use the script [**Interactable**](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.SDK/Features/UX/Interactable/Scripts) to make objects respond to various types of input interaction states.</span></span> <span data-ttu-id="5eaac-235">Il prend en charge différents types de thèmes qui vous permettent de définir des États visuels en contrôlant des propriétés d’objet telles que la couleur, la taille, le matériau et le nuanceur.</span><span class="sxs-lookup"><span data-stu-id="5eaac-235">It supports various types of themes that allows you define visual states by controlling object properties such as color, size, material, and shader.</span></span>

* [<span data-ttu-id="5eaac-236">Sur</span><span class="sxs-lookup"><span data-stu-id="5eaac-236">Interactable</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html)
* [<span data-ttu-id="5eaac-237">Button</span><span class="sxs-lookup"><span data-stu-id="5eaac-237">Button</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html)
* [<span data-ttu-id="5eaac-238">Scène d’exemples d’interaction manuelle</span><span class="sxs-lookup"><span data-stu-id="5eaac-238">Hand interaction examples scene</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_HandInteractionExamples.md)

<span data-ttu-id="5eaac-239">Le nuanceur standard de MixedRealityToolkit fournit diverses options telles que la **lumière de proximité** qui vous aide à créer des signaux visuels et audio.</span><span class="sxs-lookup"><span data-stu-id="5eaac-239">MixedRealityToolkit's Standard shader provides various options such as **proximity light** that helps you create visual and audio cues.</span></span>
* [<span data-ttu-id="5eaac-240">Nuanceur standard MRTK</span><span class="sxs-lookup"><span data-stu-id="5eaac-240">MRTK Standard Shader</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Documentation/README_MRTKStandardShader.md)


<br>

---


## <a name="see-also"></a><span data-ttu-id="5eaac-241">Articles associés</span><span class="sxs-lookup"><span data-stu-id="5eaac-241">See also</span></span>

* [<span data-ttu-id="5eaac-242">Curseurs</span><span class="sxs-lookup"><span data-stu-id="5eaac-242">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="5eaac-243">Rayon de la main</span><span class="sxs-lookup"><span data-stu-id="5eaac-243">Hand ray</span></span>](point-and-commit.md)
* [<span data-ttu-id="5eaac-244">Button</span><span class="sxs-lookup"><span data-stu-id="5eaac-244">Button</span></span>](button.md)
* [<span data-ttu-id="5eaac-245">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="5eaac-245">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="5eaac-246">Rectangle englobant et barre de l’application</span><span class="sxs-lookup"><span data-stu-id="5eaac-246">Bounding box and App bar</span></span>](app-bar-and-bounding-box.md)
* [<span data-ttu-id="5eaac-247">Manoeuvr</span><span class="sxs-lookup"><span data-stu-id="5eaac-247">Manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="5eaac-248">Menu de la main</span><span class="sxs-lookup"><span data-stu-id="5eaac-248">Hand menu</span></span>](hand-menu.md)
* [<span data-ttu-id="5eaac-249">Menu proche</span><span class="sxs-lookup"><span data-stu-id="5eaac-249">Near menu</span></span>](near-menu.md)
* [<span data-ttu-id="5eaac-250">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="5eaac-250">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="5eaac-251">Commande vocale</span><span class="sxs-lookup"><span data-stu-id="5eaac-251">Voice command</span></span>](voice-input.md)
* [<span data-ttu-id="5eaac-252">Clavier</span><span class="sxs-lookup"><span data-stu-id="5eaac-252">Keyboard</span></span>](keyboard.md)
* [<span data-ttu-id="5eaac-253">Bulle</span><span class="sxs-lookup"><span data-stu-id="5eaac-253">Tooltip</span></span>](tooltip.md)
* [<span data-ttu-id="5eaac-254">Médias</span><span class="sxs-lookup"><span data-stu-id="5eaac-254">Slate</span></span>](slate.md)
* [<span data-ttu-id="5eaac-255">Curseur</span><span class="sxs-lookup"><span data-stu-id="5eaac-255">Slider</span></span>](slider.md)
* [<span data-ttu-id="5eaac-256">Nuance</span><span class="sxs-lookup"><span data-stu-id="5eaac-256">Shader</span></span>](shader.md)
* [<span data-ttu-id="5eaac-257">Billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="5eaac-257">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
* [<span data-ttu-id="5eaac-258">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="5eaac-258">Displaying progress</span></span>](progress.md)
* [<span data-ttu-id="5eaac-259">Aimantation de surface</span><span class="sxs-lookup"><span data-stu-id="5eaac-259">Surface magnetism</span></span>](surface-magnetism.md)
