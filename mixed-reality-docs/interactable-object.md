---
title: Objet sur
description: Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait 2D. Dans le monde en trois dimensions de réalité mixte, nous n’êtes pas obligé d’être limitées à ce monde d’abstraction plus.
author: cre8ivepark
ms.author: jennyk
ms.date: 02/24/2019
ms.topic: article
keywords: Réalité mixte, contrôles, interaction, l’interface utilisateur, l’expérience utilisateur
ms.openlocfilehash: f349d21707375690e00b0f7e465634c62be1537e
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594762"
---
# <a name="interactable-object"></a><span data-ttu-id="7e9c2-105">Objet sur</span><span class="sxs-lookup"><span data-stu-id="7e9c2-105">Interactable object</span></span>

<span data-ttu-id="7e9c2-106">Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait 2D.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-106">A button has long been a metaphor used for triggering an event in the 2D abstract world.</span></span> <span data-ttu-id="7e9c2-107">Dans le monde en trois dimensions de réalité mixte, nous n’êtes pas obligé d’être limitées à ce monde d’abstraction plus.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-107">In the three-dimensional mixed reality world, we don’t have to be confined to this world of abstraction anymore.</span></span> <span data-ttu-id="7e9c2-108">Quoi que ce soit peut être un **sur objet** qui déclenche un événement.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-108">Anything can be an **Interactable object** that triggers an event.</span></span> <span data-ttu-id="7e9c2-109">Un objet sur peut être représenté en tant que quoi que ce soit à partir d’une tasse de café sur la table à une info-bulle flottante en l’air.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-109">An interactable object can be represented as anything from a coffee cup on the table to a balloon floating in the air.</span></span> <span data-ttu-id="7e9c2-110">Que nous apporterons toujours l’utilisation de boutons traditionnel dans certains cas, par exemple, dans la boîte de dialogue interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-110">We still do make use of traditional buttons in certain situation such as in dialog UI.</span></span> <span data-ttu-id="7e9c2-111">La représentation visuelle du bouton dépend du contexte.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-111">The visual representation of the button depends on the context.</span></span>

![Image de héros objet interactible](images/640px-interactibleobject-hero-640px.jpg)


<span data-ttu-id="7e9c2-113">Dans le  **[Toolkit de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity)**, nous avons créé une série de scripts Unity et prefabs qui vous aideront à créer des objets sur.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-113">In the **[Mixed Reality Toolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity)**, we have created a series of Unity scripts and prefabs that will help you create Interactable objects.</span></span> <span data-ttu-id="7e9c2-114">Vous pouvez les utiliser pour créer n’importe quel type d’objet que l’utilisateur peut interagir avec, à l’aide de ces États interaction standard : observation, ciblés et enfoncé.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-114">You can use these to create any type of object that the user can interact with, using these standard interaction states: observation, targeted and pressed.</span></span> <span data-ttu-id="7e9c2-115">Vous pouvez facilement personnaliser la conception visuelle avec vos propres ressources.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-115">You can easily customize the visual design with your own assets.</span></span> <span data-ttu-id="7e9c2-116">Animations détaillées peuvent être personnalisées en créant et affectation des clips d’animation correspondant pour les États d’interaction dans le contrôleur de l’animation d’Unity ou à l’aide de décalage et mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-116">Detailed animations can be customized by either creating and assigning corresponding animation clips for the interaction states in the Unity's animation controller or using offset and scale.</span></span> 


## <a name="visual-feedback-for-the-different-input-interaction-states"></a><span data-ttu-id="7e9c2-117">Commentaires visuels pour les États de l’interaction d’entrée différents</span><span class="sxs-lookup"><span data-stu-id="7e9c2-117">Visual feedback for the different input interaction states</span></span>

<span data-ttu-id="7e9c2-118">En réalité mixte, étant donné que les objets HOLOGRAPHIQUE sont combinées avec l’environnement réel, il pourrait être difficile de comprendre quels objets sont sur.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-118">In mixed reality, since the holographic objects are mixed with the real-world environment, it could be difficult to understand which objects are interactable.</span></span> <span data-ttu-id="7e9c2-119">Pour les objets sur votre expérience, il est important de fournir des commentaires visuels différenciées pour chaque état d’entrée.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-119">For any interactable objects in your experience, it is important to provide differentiated visual feedback for each input state.</span></span> <span data-ttu-id="7e9c2-120">Cela permet à l’utilisateur de comprendre quelle partie de votre expérience est sur et fait certain de l’utilisateur avec la méthode d’interaction cohérent.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-120">This helps the user understand which part of your experience is interactable and makes the user confident with consistent interaction method.</span></span>

<span data-ttu-id="7e9c2-121">Pour tous les objets que l’utilisateur peut interagir avec, il est recommandé d’avoir des commentaires visuels différents pour ces trois d’entrée des États :</span><span class="sxs-lookup"><span data-stu-id="7e9c2-121">For any objects that user can interact with, we recommended to have different visual feedback for these three input states:</span></span>
* <span data-ttu-id="7e9c2-122">**Observation**: État d’inactivité par défaut de l’objet.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-122">**Observation**: Default idle state of the object.</span></span>
* <span data-ttu-id="7e9c2-123">**Ciblés**: Pointeur de contrôleur proximité ou de mouvement doigt par quand l’objet est ciblé avec regards curseur.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-123">**Targeted**: When the object is targeted with gaze cursor, finger proximity or motion controller's pointer.</span></span>
* <span data-ttu-id="7e9c2-124">**Enfoncé**: Lorsque l’objet est activé avec le geste d’appui de l’air, appuyez sur le doigt ou bouton de sélection du contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-124">**Pressed**: When the object is pressed with air-tap gesture, finger press or motion controller's select button.</span></span>

<span data-ttu-id="7e9c2-125">![Bouton HOLOGRAPHIQUE](images/640px-interactibleobject-holographicbutton-650px.jpg)</span><span class="sxs-lookup"><span data-stu-id="7e9c2-125">![Holographic button](images/640px-interactibleobject-holographicbutton-650px.jpg)</span></span><br>
<span data-ttu-id="7e9c2-126">*État de l’observation, ciblées d’état et état enfoncé*</span><span class="sxs-lookup"><span data-stu-id="7e9c2-126">*Observation state, targeted state, and pressed state*</span></span>

<span data-ttu-id="7e9c2-127">Dans Windows Mixed Reality, vous pouvez trouver les exemples de visualiser les différents États d’entrée sur le menu Démarrer et des boutons de barre de l’application.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-127">In Windows Mixed Reality, you can find the examples of visualizing different input states on Start menu and App Bar buttons.</span></span> <span data-ttu-id="7e9c2-128">Vous pouvez utiliser des techniques telles que la mise en surbrillance ou de mise à l’échelle pour fournir des commentaires visuels aux États d’entrée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-128">You can use techniques such as highlighting or scaling to provide visual feedback to the user’s input states.</span></span>

<span data-ttu-id="7e9c2-129">Dans les 2 HoloLens, dans la mesure où il prend en charge entièrement articulé main suivi d’entrée, nous pouvons fournir intuitivité supplémentaires en fonction de la proximité entre les mains.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-129">In HoloLens 2, since it supports fully articulated hand tracking input, we can provide additional affordances based on the proximity to the hands.</span></span> <span data-ttu-id="7e9c2-130">Le [bouton HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html) montre cet exemple.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-130">The [Button in HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html) shows this example.</span></span>

![Bouton PRESSEE](images/640px-interactibleobject-pressablebutton-650px.jpg)<br>




## <a name="interactable-object-samples"></a><span data-ttu-id="7e9c2-132">Exemples de l’objet sur</span><span class="sxs-lookup"><span data-stu-id="7e9c2-132">Interactable object samples</span></span>

### <a name="mesh-button"></a><span data-ttu-id="7e9c2-133">Bouton de maillage</span><span class="sxs-lookup"><span data-stu-id="7e9c2-133">Mesh button</span></span>

![Bouton de maillage](images/640px-interactibleobject-meshbutton.jpg)

<span data-ttu-id="7e9c2-135">Voici des exemples à l’aide de primitives et des maillages 3D importés en tant qu’objets sur.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-135">These are examples using primitives and imported 3D meshes as Interactable objects.</span></span> <span data-ttu-id="7e9c2-136">Vous pouvez facilement attribuer différentes valeurs de couleur, le décalage et mise à l’échelle pour répondre à chaque état de l’interaction d’entrée.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-136">You can easily assign different scale, offset and color values to respond to each input interaction state.</span></span>

### <a name="toolbar"></a><span data-ttu-id="7e9c2-137">Barre d’outils</span><span class="sxs-lookup"><span data-stu-id="7e9c2-137">Toolbar</span></span>

![Barre d’outils](images/640px-interactibleobject-toolbar.jpg)

<span data-ttu-id="7e9c2-139">Une barre d’outils est un modèle largement utilisé dans les expériences de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-139">A toolbar is a widely used pattern in mixed reality experiences.</span></span> <span data-ttu-id="7e9c2-140">Il est une simple collection de boutons avec des comportements supplémentaires telles que [Billboarding et tag-along](billboarding-and-tag-along.md).</span><span class="sxs-lookup"><span data-stu-id="7e9c2-140">It is a simple collection of buttons with additional behaviors such as [Billboarding and tag-along](billboarding-and-tag-along.md).</span></span> <span data-ttu-id="7e9c2-141">Cet exemple utilise un script Billboarding et tag-along à partir de la MixedRealityToolkit.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-141">This example uses a Billboarding and tag-along script from the MixedRealityToolkit.</span></span> <span data-ttu-id="7e9c2-142">Vous pouvez contrôler les comportements détaillées, y compris la distance, déplacer des valeurs de vitesse et de seuil.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-142">You can control detailed behaviors including distance, moving speed and threshold values.</span></span>

### <a name="traditional-button"></a><span data-ttu-id="7e9c2-143">Bouton classique</span><span class="sxs-lookup"><span data-stu-id="7e9c2-143">Traditional button</span></span>

![Bouton classique](images/640px-interactibleobject-traditionalbutton.jpg)

<span data-ttu-id="7e9c2-145">Cet exemple montre un bouton de style 2D traditionnel.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-145">This example shows a traditional 2D style button.</span></span> <span data-ttu-id="7e9c2-146">Chaque état d’entrée a une profondeur légèrement différente et la propriété d’animation.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-146">Each input state has a slightly different depth and animation property.</span></span>

### <a name="other-examples"></a><span data-ttu-id="7e9c2-147">Autres exemples</span><span class="sxs-lookup"><span data-stu-id="7e9c2-147">Other examples</span></span>

<span data-ttu-id="7e9c2-148">![Bouton de commande](images/640px-interactibleobject-pushbutton.jpg)</span><span class="sxs-lookup"><span data-stu-id="7e9c2-148">![Push button](images/640px-interactibleobject-pushbutton.jpg)</span></span><br>
<span data-ttu-id="7e9c2-149">*Bouton de commande*</span><span class="sxs-lookup"><span data-stu-id="7e9c2-149">*Push button*</span></span>
<br>
<span data-ttu-id="7e9c2-150">![Objet de durée de vie réel](images/640px-interactibleobject-reallifeobject.jpg)</span><span class="sxs-lookup"><span data-stu-id="7e9c2-150">![Real Life object](images/640px-interactibleobject-reallifeobject.jpg)</span></span><br>
<span data-ttu-id="7e9c2-151">*Objet de la vie réelle*</span><span class="sxs-lookup"><span data-stu-id="7e9c2-151">*Real life object*</span></span>

<span data-ttu-id="7e9c2-152">Avec HoloLens, vous pouvez tirer parti d’espace physique.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-152">With HoloLens, you can leverage physical space.</span></span> <span data-ttu-id="7e9c2-153">Imaginez un bouton de commande HOLOGRAPHIQUE sur un mur physique.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-153">Imagine a holographic push button on a physical wall.</span></span> <span data-ttu-id="7e9c2-154">Ou est-il une tasse de café sur une table réelle ?</span><span class="sxs-lookup"><span data-stu-id="7e9c2-154">Or how about a coffee cup on a real table?</span></span> <span data-ttu-id="7e9c2-155">À l’aide des modèles 3D importés de modéliser le logiciel, nous pouvons créer un objet sur qui ressemble à des objets de la vie réelle.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-155">Using 3D models imported from modeling software, we can create an Interactable object that resembles real life object.</span></span> <span data-ttu-id="7e9c2-156">Dans la mesure où il s’agit d’un objet numérique, nous pouvons ajouter des interactions magiques à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="7e9c2-156">Since it's a digital object, we can add magical interactions to it.</span></span>

## <a name="interactable-object-in-mixed-reality-toolkit"></a><span data-ttu-id="7e9c2-157">Objet sur dans la boîte à outils de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="7e9c2-157">Interactable object in Mixed Reality Toolkit</span></span>
<span data-ttu-id="7e9c2-158">Vous pouvez trouver le [exemples de Interactable de l’objet dans la boîte à outils de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html)</span><span class="sxs-lookup"><span data-stu-id="7e9c2-158">You can find the [examples of Interactable object in Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html)</span></span>


## <a name="see-also"></a><span data-ttu-id="7e9c2-159">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7e9c2-159">See also</span></span>
* [<span data-ttu-id="7e9c2-160">Bouton PRESSEE de réalité mixte Toolkit-Unity</span><span class="sxs-lookup"><span data-stu-id="7e9c2-160">Pressable Button on Mixed Reality Toolkit-Unity</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html)
* [<span data-ttu-id="7e9c2-161">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="7e9c2-161">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="7e9c2-162">Le billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="7e9c2-162">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
