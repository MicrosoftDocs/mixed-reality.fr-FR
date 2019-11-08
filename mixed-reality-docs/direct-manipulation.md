---
title: Manipulation directe avec les mains
description: Vue d’ensemble du modèle d’entrée de manipulation directe
author: caseymeekhof
ms.author: cmeekhof
ms.date: 04/02/2019
ms.topic: article
ms.localizationpriority: high
keywords: Réalité mixte, pointage du regard, ciblage par pointage du regard, interaction, conception, à portée de main, HoloLens
ms.openlocfilehash: ed3b25fe9a7dd404d07073b578b8da13e1984cab
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73435942"
---
# <a name="direct-manipulation-with-hands"></a><span data-ttu-id="eb37e-104">Manipulation directe avec les mains</span><span class="sxs-lookup"><span data-stu-id="eb37e-104">Direct manipulation with hands</span></span>
<span data-ttu-id="eb37e-105">La manipulation directe est un modèle d’entrée qui consiste à toucher les hologrammes directement avec les mains.</span><span class="sxs-lookup"><span data-stu-id="eb37e-105">Direct manipulation is an input model that involves touching holograms directly with your hands.</span></span> <span data-ttu-id="eb37e-106">L’idée derrière ce concept est de faire en sorte que les objets se comportent exactement comme dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="eb37e-106">The idea behind this concept is that objects behave just as they would in the real world.</span></span> <span data-ttu-id="eb37e-107">Vous pouvez activer les boutons simplement en appuyant dessus, vous pouvez saisir les objets en les agrippant, et le contenu 2D se comporte comme un écran tactile virtuel.</span><span class="sxs-lookup"><span data-stu-id="eb37e-107">Buttons can be activated simply by pressing them, objects can be picked up by grabbing them, and 2D content behaves like a virtual touchscreen.</span></span> <span data-ttu-id="eb37e-108">C’est pourquoi la manipulation directe est facile à apprendre pour les utilisateurs et amusante.</span><span class="sxs-lookup"><span data-stu-id="eb37e-108">This makes direct manipulation easy for users to learn, and fun.</span></span> <span data-ttu-id="eb37e-109">Elle est considérée comme un modèle d’entrée « proche », car elle est utilisée de préférence pour interagir avec le contenu situé à portée de main.</span><span class="sxs-lookup"><span data-stu-id="eb37e-109">It's considered a "near" input model in that it's best used for interacting with content within arms reach.</span></span>

<span data-ttu-id="eb37e-110">La manipulation directe est basée sur l’affordance, ce qui la rend conviviale.</span><span class="sxs-lookup"><span data-stu-id="eb37e-110">Direct manipulation is affordance-based, meaning it's user friendly.</span></span> <span data-ttu-id="eb37e-111">Les utilisateurs n’ont pas à apprendre de mouvements symboliques.</span><span class="sxs-lookup"><span data-stu-id="eb37e-111">There are no symbolic gestures to teach users.</span></span> <span data-ttu-id="eb37e-112">Toutes les interactions reposent sur un élément visuel que vous pouvez toucher ou saisir.</span><span class="sxs-lookup"><span data-stu-id="eb37e-112">All interactions are built around a visual element that you can touch or grab.</span></span>

## <a name="device-support"></a><span data-ttu-id="eb37e-113">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="eb37e-113">Device support</span></span>

<table>
<colgroup>
    <col width="33%" />
    <col width="22%" />
    <col width="22%" />
    <col width="22%" />
</colgroup>
<tr>
     <td><span data-ttu-id="eb37e-114"><strong>Modèle d’entrée</strong></span><span class="sxs-lookup"><span data-stu-id="eb37e-114"><strong>Input model</strong></span></span></td>
     <td><span data-ttu-id="eb37e-115"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="eb37e-115"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
     <td><span data-ttu-id="eb37e-116"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="eb37e-116"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
     <td><span data-ttu-id="eb37e-117"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="eb37e-117"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
</tr>
<tr>
     <td><span data-ttu-id="eb37e-118">Manipulation directe avec les mains</span><span class="sxs-lookup"><span data-stu-id="eb37e-118">Direct manipulation with hands</span></span></td>
     <td><span data-ttu-id="eb37e-119">❌ Non pris en charge</span><span class="sxs-lookup"><span data-stu-id="eb37e-119">❌ Not supported</span></span></td>
     <td><span data-ttu-id="eb37e-120">✔️ Recommandé</span><span class="sxs-lookup"><span data-stu-id="eb37e-120">✔️ Recommended</span></span></td>
     <td><span data-ttu-id="eb37e-121">➕ Une solution, telle que <a href="point-and-commit.md">pointer et valider avec les mains</a>, est recommandée.</span><span class="sxs-lookup"><span data-stu-id="eb37e-121">➕ An alternative, <a href="point-and-commit.md">point and commit with hands</a> is recommended.</span></span></td>
    
</tr>
</table>


<span data-ttu-id="eb37e-122">La manipulation directe est l’un des principaux modèles d’entrée sur HoloLens 2. Elle utilise le nouveau système de suivi des mains articulé.</span><span class="sxs-lookup"><span data-stu-id="eb37e-122">Direct manipulation is a primary input model on HoloLens 2, which uses the new articulated hand-tracking system.</span></span> <span data-ttu-id="eb37e-123">Le modèle d’entrée est également disponible sur les casques immersifs via l’utilisation de contrôleurs de mouvement, mais il n’est pas recommandé en tant que mode principal d’interaction en dehors de la manipulation d’objets.</span><span class="sxs-lookup"><span data-stu-id="eb37e-123">The input model is also available on immersive headsets through the use of motion controllers, but is not recommended as a primary means of interaction outside of object manipulation.</span></span> <span data-ttu-id="eb37e-124">La manipulation directe n’est pas disponible sur HoloLens (1re génération).</span><span class="sxs-lookup"><span data-stu-id="eb37e-124">Direct manipulation is not available on HoloLens (1st gen).</span></span>

<br>

---

## <a name="collidable-fingertip"></a><span data-ttu-id="eb37e-125">Pointe de doigt avec détection de collision</span><span class="sxs-lookup"><span data-stu-id="eb37e-125">Collidable fingertip</span></span>

<span data-ttu-id="eb37e-126">Sur HoloLens 2, les mains de l’utilisateur sont reconnues et interprétées en tant que modèles du squelette des mains gauche et droite.</span><span class="sxs-lookup"><span data-stu-id="eb37e-126">On HoloLens 2, the user's hands are recognized and interpreted as left and right hand skeletal models.</span></span> <span data-ttu-id="eb37e-127">Pour implémenter l’idée consistant à toucher les hologrammes directement avec les mains, l’idéal serait d’attacher cinq colliders (détecteurs de collision) aux cinq pointes de doigt de chaque modèle du squelette de la main.</span><span class="sxs-lookup"><span data-stu-id="eb37e-127">To implement the idea of touching holograms directly with hands, ideally, five colliders could be attached to the five fingertips of each hand skeletal model.</span></span> <span data-ttu-id="eb37e-128">Toutefois, en raison de l’absence de rétroaction tactile, dix bouts de doigts avec détection de collision donnent lieu à des collisions inattendues et imprévisibles avec les hologrammes.</span><span class="sxs-lookup"><span data-stu-id="eb37e-128">However, due to the lack of tactile feedback, ten collidable fingertips can cause unexpected and unpredictable collisions with holograms.</span></span> 

<span data-ttu-id="eb37e-129">Nous suggérons donc de placer uniquement un collider sur chaque index.</span><span class="sxs-lookup"><span data-stu-id="eb37e-129">Hence, we suggest only putting a collider on each index finger.</span></span> <span data-ttu-id="eb37e-130">Les pointes d’index avec détection de collision peuvent toujours servir de points tactiles actifs pour les divers mouvements tactiles impliquant d’autres doigts, par exemple l’appui avec un doigt, le clic à un doigt, l’appui avec deux doigts et l’appui avec cinq doigts, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="eb37e-130">The collidable index fingertips can still serve as active touch points for diverse touch gestures involving other fingers, such as One-finger press, One-finger tap, Two-finger press and Five-finger press, as shown in the image below.</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="eb37e-131">![Pointe de doigt avec détection de collision](images/Collidable-Fingertip.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-131">![collidable fingertip](images/Collidable-Fingertip.jpg)</span></span><br>
       <span data-ttu-id="eb37e-132">**Pointe de doigt avec détection de collision**</span><span class="sxs-lookup"><span data-stu-id="eb37e-132">**Collidable fingertip**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-133">![Appui avec un doigt](images/Collidable-Fingertip-1-finger-press.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-133">![One-finger press](images/Collidable-Fingertip-1-finger-press.jpg)</span></span><br>
        <span data-ttu-id="eb37e-134">**Appui avec un doigt**</span><span class="sxs-lookup"><span data-stu-id="eb37e-134">**One-finger press**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-135">![Clic à un doigt](images/Collidable-Fingertip-1-finger-tap.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-135">![One-finger tap](images/Collidable-Fingertip-1-finger-tap.jpg)</span></span><br>
       <span data-ttu-id="eb37e-136">**Clic à un doigt**</span><span class="sxs-lookup"><span data-stu-id="eb37e-136">**One-finger tap**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-137">![Appui avec cinq doigts](images/Collidable-Fingertip-5-finger-press.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-137">![Five-finger press](images/Collidable-Fingertip-5-finger-press.jpg)</span></span><br>
       <span data-ttu-id="eb37e-138">**Appui avec cinq doigts**</span><span class="sxs-lookup"><span data-stu-id="eb37e-138">**Five-finger press**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

### <a name="sphere-collider"></a><span data-ttu-id="eb37e-139">Collider sphérique</span><span class="sxs-lookup"><span data-stu-id="eb37e-139">Sphere collider</span></span>

<span data-ttu-id="eb37e-140">Au lieu d’utiliser une forme générique aléatoire, nous vous suggérons d’utiliser un collider de sphère.</span><span class="sxs-lookup"><span data-stu-id="eb37e-140">Instead of using a random generic shape, we suggest you use a sphere collider.</span></span> <span data-ttu-id="eb37e-141">Ensuite, vous pouvez l’afficher visuellement pour fournir de meilleures indications de ciblage proche.</span><span class="sxs-lookup"><span data-stu-id="eb37e-141">Then you can visually render it to provide better cues for near targeting.</span></span> <span data-ttu-id="eb37e-142">Le diamètre de la sphère doit correspondre à l’épaisseur de l’index pour augmenter la précision tactile.</span><span class="sxs-lookup"><span data-stu-id="eb37e-142">The sphere's diameter should match the thickness of the index finger to increase touch accuracy.</span></span> <span data-ttu-id="eb37e-143">Il est plus facile de récupérer la variable de l’épaisseur du doigt en appelant l’API relative à la main.</span><span class="sxs-lookup"><span data-stu-id="eb37e-143">It's easier to retrieve the variable of finger thickness by calling the hand API.</span></span>

### <a name="fingertip-cursor"></a><span data-ttu-id="eb37e-144">Curseur à la pointe du doigt</span><span class="sxs-lookup"><span data-stu-id="eb37e-144">Fingertip cursor</span></span>

<span data-ttu-id="eb37e-145">En plus du rendu d’une sphère avec détection de collision à la pointe de l’index, nous avons créé un curseur à la pointe du doigt pour vivre une meilleure expérience interactive de ciblage interactif proche.</span><span class="sxs-lookup"><span data-stu-id="eb37e-145">In addition to rendering a collidable sphere on the index fingertip, we've created an advanced fingertip cursor to interactively achieve a better near-targeting experience.</span></span> <span data-ttu-id="eb37e-146">Il s’agit d’un curseur en forme d’anneau attaché à la pointe de l’index.</span><span class="sxs-lookup"><span data-stu-id="eb37e-146">It is a donut-shaped cursor attached to the index fingertip.</span></span> <span data-ttu-id="eb37e-147">En fonction de la proximité, il réagit de manière dynamique à l’orientation et à la taille d’une cible, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="eb37e-147">According to proximity, it dynamically reacts to a target in terms of orientation and size as detailed below:</span></span>

* <span data-ttu-id="eb37e-148">Quand un index se déplace vers un hologramme, le curseur est toujours parallèle à la surface de l’hologramme et réduit progressivement sa taille.</span><span class="sxs-lookup"><span data-stu-id="eb37e-148">When an index finger moves toward a hologram, the cursor is always parallel to the hologram's surface and gradually shrinks its size accordingly.</span></span>
* <span data-ttu-id="eb37e-149">Dès que le doigt touche la surface, le curseur se réduit en un point et émet un événement tactile.</span><span class="sxs-lookup"><span data-stu-id="eb37e-149">As soon as the finger touches the surface, the cursor shrinks into a dot and emits a touch event.</span></span>

<span data-ttu-id="eb37e-150">Grâce à une rétroaction interactive, les utilisateurs disposent d’une haute précision pour les tâches de ciblage proche, par exemple le déclenchement d’un lien hypertexte ou la pression sur un bouton, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="eb37e-150">With interactive feedback, users can achieve high precision near-targeting tasks, such as triggering a hyperlink or pressing a button as shown below.</span></span> 

:::row:::
    :::column:::
       <span data-ttu-id="eb37e-151">![Curseur à la pointe du doigt éloigné](images/Fingertip-cursor-far.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-151">![Fingertip cursor far](images/Fingertip-cursor-far.jpg)</span></span><br>
       <span data-ttu-id="eb37e-152">**Curseur à la pointe du doigt éloigné**</span><span class="sxs-lookup"><span data-stu-id="eb37e-152">**Fingertip cursor far**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-153">![Curseur à la pointe du doigt proche](images/Fingertip-cursor-near.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-153">![Fingertip cursor near](images/Fingertip-cursor-near.jpg)</span></span><br>
        <span data-ttu-id="eb37e-154">**Curseur à la pointe du doigt proche**</span><span class="sxs-lookup"><span data-stu-id="eb37e-154">**Fingertip cursor near**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-155">![Curseur à la pointe du doigt en contact](images/Fingertip-cursor-contact.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-155">![Fingertip cursor contact](images/Fingertip-cursor-contact.jpg)</span></span><br>
       <span data-ttu-id="eb37e-156">**Curseur à la pointe du doigt en contact**</span><span class="sxs-lookup"><span data-stu-id="eb37e-156">**Fingertip cursor contact**</span></span><br>
    :::column-end:::
:::row-end:::

<br>



## <a name="bounding-box-with-proximity-shader"></a><span data-ttu-id="eb37e-157">Rectangle englobant avec nuanceur de proximité</span><span class="sxs-lookup"><span data-stu-id="eb37e-157">Bounding box with proximity shader</span></span>

<span data-ttu-id="eb37e-158">L’hologramme lui-même doit également pouvoir fournir une rétroaction visuelle et audio pour compenser le manque de rétroaction tactile.</span><span class="sxs-lookup"><span data-stu-id="eb37e-158">The hologram itself also requires the ability to provide both visual and audio feedback to compensate the lack of tactile feedback.</span></span> <span data-ttu-id="eb37e-159">Pour cela, nous générons le concept de rectangle englobant avec un nuanceur de proximité.</span><span class="sxs-lookup"><span data-stu-id="eb37e-159">For that, we generate the concept of a bounding box with a proximity shader.</span></span> <span data-ttu-id="eb37e-160">Un rectangle englobant est une zone volumétrique minimale qui entoure un objet 3D.</span><span class="sxs-lookup"><span data-stu-id="eb37e-160">A bounding box is a minimum volumetric area that encloses a 3D object.</span></span> <span data-ttu-id="eb37e-161">Le rectangle englobant comporte un mécanisme de rendu interactif appelé nuanceur de proximité.</span><span class="sxs-lookup"><span data-stu-id="eb37e-161">The bounding box has an interactive rendering mechanism called a proximity shader.</span></span> <span data-ttu-id="eb37e-162">Le nuanceur de proximité se comporte comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb37e-162">The proximity shader behaves:</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="eb37e-163">![Pointage (éloigné) avec retour visuel](images/bounding-box-with-proximity-shader-hover-far.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-163">![Hover (far) with visual feedback](images/bounding-box-with-proximity-shader-hover-far.jpg)</span></span><br>
       <span data-ttu-id="eb37e-164">**Pointage (éloigné)**</span><span class="sxs-lookup"><span data-stu-id="eb37e-164">**Hover (far)**</span></span><br>
       <span data-ttu-id="eb37e-165">Quand l’index se trouve dans la plage appropriée, un faisceau lumineux situé à la pointe du doigt est projeté à la surface du rectangle englobant.</span><span class="sxs-lookup"><span data-stu-id="eb37e-165">When the index finger is within a range, a fingertip spotlight is cast on the surface of the bounding box.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-166">![Pointage (proche) avec retour visuel](images/bounding-box-with-proximity-shader-hover-near.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-166">![Hover (near) with visual feedback](images/bounding-box-with-proximity-shader-hover-near.jpg)</span></span><br>
        <span data-ttu-id="eb37e-167">**Pointage (proche)**</span><span class="sxs-lookup"><span data-stu-id="eb37e-167">**Hover (near)**</span></span><br>
        <span data-ttu-id="eb37e-168">Plus la pointe du doigt se rapproche de la surface, plus le faisceau lumineux projeté est réduit.</span><span class="sxs-lookup"><span data-stu-id="eb37e-168">When the fingertip gets closer to the surface, the spotlight shrinks accordingly.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-169">![Début du contact](images/bounding-box-with-proximity-shader-begin-contact.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-169">![Contact begins](images/bounding-box-with-proximity-shader-begin-contact.jpg)</span></span><br>
       <span data-ttu-id="eb37e-170">**Début du contact**</span><span class="sxs-lookup"><span data-stu-id="eb37e-170">**Contact begins**</span></span><br>
       <span data-ttu-id="eb37e-171">Dès que la pointe du doigt touche la surface, tout le rectangle englobant change de couleur ou génère des effets visuels pour refléter l’état tactile.</span><span class="sxs-lookup"><span data-stu-id="eb37e-171">As soon as the fingertip touches the surface, the entire bounding box changes color or generates visual effects to reflect the touch state.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-172">![Fin du contact](images/bounding-box-with-proximity-shader-end-contact.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-172">![Contact ends](images/bounding-box-with-proximity-shader-end-contact.jpg)</span></span><br>
       <span data-ttu-id="eb37e-173">**Fin du contact**</span><span class="sxs-lookup"><span data-stu-id="eb37e-173">**Contact ends**</span></span><br>
       <span data-ttu-id="eb37e-174">Il est également possible d’activer un effet sonore pour améliorer la rétroaction tactile visuelle.</span><span class="sxs-lookup"><span data-stu-id="eb37e-174">A sound effect can also be activated to enhance the visual touch feedback.</span></span>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="pressable-button"></a><span data-ttu-id="eb37e-175">Bouton sur lequel appuyer</span><span class="sxs-lookup"><span data-stu-id="eb37e-175">Pressable button</span></span>

<span data-ttu-id="eb37e-176">Avec une pointe de doigt pourvue de la détection de collision, les utilisateurs sont désormais prêts à interagir avec un composant d’IU holographique fondamental, à savoir un bouton sur lequel appuyer.</span><span class="sxs-lookup"><span data-stu-id="eb37e-176">With a collidable fingertip, users are now ready to interact with a fundamental holographic UI component, such as a pressable button.</span></span> <span data-ttu-id="eb37e-177">Ce type de bouton est un composant holographique conçu pour une pression directe à l’aide du doigt.</span><span class="sxs-lookup"><span data-stu-id="eb37e-177">A pressable button is a holographic button tailored for a direct finger press.</span></span> <span data-ttu-id="eb37e-178">Là encore, en raison du manque de rétroaction tactile, un bouton sur lequel il est possible d’appuyer associe deux mécanismes pour traiter les problèmes de rétroaction tactile.</span><span class="sxs-lookup"><span data-stu-id="eb37e-178">Again, due to the lack of tactile feedback, a pressable button equips a couple mechanisms to tackle tactile feedback-related issues.</span></span>

* <span data-ttu-id="eb37e-179">Le premier mécanisme est un rectangle englobant avec nuanceur de proximité, détaillé dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="eb37e-179">The first mechanism is a bounding box with a proximity shader, which is detailed in the previous section.</span></span> <span data-ttu-id="eb37e-180">Il offre aux utilisateurs une meilleure sensation de proximité lors de l’approche et du contact avec un bouton.</span><span class="sxs-lookup"><span data-stu-id="eb37e-180">It gives users a better sense of proximity when they approach and make contact with a button.</span></span>
* <span data-ttu-id="eb37e-181">Le second mécanisme est une dépression.</span><span class="sxs-lookup"><span data-stu-id="eb37e-181">The second mechanism is depression.</span></span> <span data-ttu-id="eb37e-182">La dépression crée une sensation de pression lorsque le doigt entre en contact avec un bouton.</span><span class="sxs-lookup"><span data-stu-id="eb37e-182">Depression creates a sense of pressing down after a fingertip contacts a button.</span></span> <span data-ttu-id="eb37e-183">Ce mécanisme permet de veiller à ce que le bouton se déplace étroitement avec la pointe du doigt dans l’axe de profondeur.</span><span class="sxs-lookup"><span data-stu-id="eb37e-183">The mechanism ensures that the button tightly moves with the fingertip along the depth axis.</span></span> <span data-ttu-id="eb37e-184">Le bouton peut se déclencher quand il atteint une profondeur déterminée (l’utilisateur appuie sur le bouton) ou quand il quitte cette profondeur (l’utilisateur relâche le bouton).</span><span class="sxs-lookup"><span data-stu-id="eb37e-184">The button can be triggered when it reaches a designated depth (on press) or leaves the depth (on release) after passing through it.</span></span>
* <span data-ttu-id="eb37e-185">Il est possible d’ajouter un effet sonore pour améliorer la rétroaction quand le bouton se déclenche.</span><span class="sxs-lookup"><span data-stu-id="eb37e-185">The sound effect should be added to enhance feedback when the button is triggered.</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="eb37e-186">![Bouton sur lequel appuyer éloigné](images/pressable-button-far.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-186">![pressable button far](images/pressable-button-far.jpg)</span></span><br>
       <span data-ttu-id="eb37e-187">**Doigt éloigné**</span><span class="sxs-lookup"><span data-stu-id="eb37e-187">**Finger is far away**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-188">![Bouton sur lequel appuyer proche](images/pressable-button-approach.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-188">![pressable button near](images/pressable-button-approach.jpg)</span></span><br>
        <span data-ttu-id="eb37e-189">**Doigt en approche**</span><span class="sxs-lookup"><span data-stu-id="eb37e-189">**Finger approaches**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-190">![Début du contact avec le bouton sur lequel appuyer](images/pressable-button-contact.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-190">![pressable button contact begins](images/pressable-button-contact.jpg)</span></span><br>
       <span data-ttu-id="eb37e-191">**Début du contact**</span><span class="sxs-lookup"><span data-stu-id="eb37e-191">**Contact begins**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-192">![Appui sur le bouton sur lequel appuyer](images/pressable-button-press.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-192">![pressable button press](images/pressable-button-press.jpg)</span></span><br>
       <span data-ttu-id="eb37e-193">**Appui**</span><span class="sxs-lookup"><span data-stu-id="eb37e-193">**Press down**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="2d-slate-interaction"></a><span data-ttu-id="eb37e-194">Interaction avec une tablette 2D</span><span class="sxs-lookup"><span data-stu-id="eb37e-194">2D slate interaction</span></span>

<span data-ttu-id="eb37e-195">Une tablette 2D est un conteneur holographique hébergeant le contenu d’applications 2D comme un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="eb37e-195">A 2D slate is a holographic container hosting 2D app contents, such as a web browser.</span></span> <span data-ttu-id="eb37e-196">L’interaction avec une tablette 2D par manipulation directe consiste à exploiter le modèle mental de l’interaction avec un écran tactile physique.</span><span class="sxs-lookup"><span data-stu-id="eb37e-196">The design concept for interacting with a 2D slate via direct manipulation is to leverage the mental model of interacting with a physical touch screen.</span></span>

### <a name="to-interact-with-the-slate-contact"></a><span data-ttu-id="eb37e-197">Pour interagir avec la tablette par contact</span><span class="sxs-lookup"><span data-stu-id="eb37e-197">To interact with the slate contact</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="eb37e-198">![Interface tactile](images/2d-slate-interaction-touch.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-198">![Touch](images/2d-slate-interaction-touch.jpg)</span></span><br>
       <span data-ttu-id="eb37e-199">**Interface tactile**</span><span class="sxs-lookup"><span data-stu-id="eb37e-199">**Touch**</span></span><br>
       <span data-ttu-id="eb37e-200">Utilisez l’index pour appuyer sur un lien hypertexte ou un bouton.</span><span class="sxs-lookup"><span data-stu-id="eb37e-200">Use an index finger to press a hyperlink or a button.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-201">![Faire défiler](images/2d-slate-interaction-scroll2.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-201">![Scroll](images/2d-slate-interaction-scroll2.jpg)</span></span><br>
        <span data-ttu-id="eb37e-202">**Faire défiler**</span><span class="sxs-lookup"><span data-stu-id="eb37e-202">**Scroll**</span></span><br>
        <span data-ttu-id="eb37e-203">Utilisez l’index pour faire défiler le contenu de la tablette vers le haut et vers le bas.</span><span class="sxs-lookup"><span data-stu-id="eb37e-203">Use an index finger to scroll a slate content up and down.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-204">![Zoom](images/2d-slate-interaction-zoom2.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-204">![Zoom](images/2d-slate-interaction-zoom2.jpg)</span></span><br>
       <span data-ttu-id="eb37e-205">**Zoom**</span><span class="sxs-lookup"><span data-stu-id="eb37e-205">**Zoom**</span></span><br>
       <span data-ttu-id="eb37e-206">Les deux index de l’utilisateur sont utilisés pour effectuer un zoom avant ou arrière sur le contenu de la tablette en fonction du mouvement relatif des doigts.</span><span class="sxs-lookup"><span data-stu-id="eb37e-206">The user's two index fingers are used to zoom in and out of the slate content, according to the relative motion of the fingers.</span></span>
    :::column-end:::
:::row-end:::


### <a name="for-manipulating-the-2d-slate-itself"></a><span data-ttu-id="eb37e-207">Pour manipuler la tablette 2D</span><span class="sxs-lookup"><span data-stu-id="eb37e-207">For manipulating the 2D slate itself</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="eb37e-208">![Déplacer](images/manipulate-2d-slate-move.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-208">![Move](images/manipulate-2d-slate-move.jpg)</span></span><br>
       <span data-ttu-id="eb37e-209">**Déplacer**</span><span class="sxs-lookup"><span data-stu-id="eb37e-209">**Move**</span></span><br>
       <span data-ttu-id="eb37e-210">Déplacez vos mains vers les coins et les bords pour faire apparaître les affordances de manipulation les plus proches.</span><span class="sxs-lookup"><span data-stu-id="eb37e-210">Move your hands toward corners and edges to reveal the closest manipulation affordances.</span></span> <span data-ttu-id="eb37e-211">Saisissez la barre holographique en haut de la tablette 2D pour pouvoir déplacer la tablette entière.</span><span class="sxs-lookup"><span data-stu-id="eb37e-211">Grab the Holobar at the top of the 2D slate, which lets you move the whole slate.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-212">![Mettre à l’échelle](images/manipulate-2d-slate-scale.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-212">![Scale](images/manipulate-2d-slate-scale.jpg)</span></span><br>
        <span data-ttu-id="eb37e-213">**Mettre à l’échelle**</span><span class="sxs-lookup"><span data-stu-id="eb37e-213">**Scale**</span></span><br>
        <span data-ttu-id="eb37e-214">Saisissez les affordances de manipulation, puis effectuez une mise à l’échelle uniforme par le biais des affordances d’angle.</span><span class="sxs-lookup"><span data-stu-id="eb37e-214">Grab the manipulation affordances and perform uniform scaling through the corner affordances.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-215">![Ajuster dynamiquement](images/manipulate-2d-slate-reflow.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-215">![Reflow](images/manipulate-2d-slate-reflow.jpg)</span></span><br>
       <span data-ttu-id="eb37e-216">**Ajuster dynamiquement**</span><span class="sxs-lookup"><span data-stu-id="eb37e-216">**Reflow**</span></span><br>
       <span data-ttu-id="eb37e-217">Saisissez les affordances de manipulation, puis effectuez un ajustement dynamique par le biais des affordances de bord.</span><span class="sxs-lookup"><span data-stu-id="eb37e-217">Grab the manipulation affordances and perform reflow via the edge affordances.</span></span>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="3d-object-manipulation"></a><span data-ttu-id="eb37e-218">Manipulation d’objet 3D</span><span class="sxs-lookup"><span data-stu-id="eb37e-218">3D object manipulation</span></span>

<span data-ttu-id="eb37e-219">HoloLens 2 permet aux utilisateurs de diriger et manipuler des objets holographiques 3D en appliquant un rectangle englobant à chaque objet 3D.</span><span class="sxs-lookup"><span data-stu-id="eb37e-219">HoloLens 2 lets users enable their hands to direct and manipulate 3D holographic objects by applying a bounding box to each 3D object.</span></span> <span data-ttu-id="eb37e-220">La rectangle englobant offre une meilleure perception de la profondeur grâce à son nuanceur de proximité.</span><span class="sxs-lookup"><span data-stu-id="eb37e-220">The bounding box provides better depth perception through its proximity shader.</span></span> <span data-ttu-id="eb37e-221">Avec le rectangle englobant, il existe deux approches de conception pour la manipulation d’objets 3D.</span><span class="sxs-lookup"><span data-stu-id="eb37e-221">With the bounding box, there are two design approaches for 3D object manipulation.</span></span>

### <a name="affordance-based-manipulation"></a><span data-ttu-id="eb37e-222">Manipulation basée sur l’affordance</span><span class="sxs-lookup"><span data-stu-id="eb37e-222">Affordance-based manipulation</span></span>

<span data-ttu-id="eb37e-223">La manipulation basée sur l’affordance vous permet de manipuler l’objet 3D via un rectangle englobant avec les affordances de manipulation qui l’entourent.</span><span class="sxs-lookup"><span data-stu-id="eb37e-223">Affordance-base manipulation lets you manipulate the 3D object through a bounding box along with the manipulation affordances around it.</span></span> 

:::row:::
    :::column:::
       <span data-ttu-id="eb37e-224">![Déplacer](images/3d-object-manipulation-move.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-224">![Move](images/3d-object-manipulation-move.jpg)</span></span><br>
       <span data-ttu-id="eb37e-225">**Déplacer**</span><span class="sxs-lookup"><span data-stu-id="eb37e-225">**Move**</span></span><br>
       <span data-ttu-id="eb37e-226">Dès que la main d’un utilisateur est proche d’un objet 3D, le rectangle englobant et l’affordance la plus proche apparaissent.</span><span class="sxs-lookup"><span data-stu-id="eb37e-226">As soon as a user's hand is close to a 3D object, the bounding box and the nearest affordance are revealed.</span></span> <span data-ttu-id="eb37e-227">Les utilisateurs peuvent saisir le rectangle englobant pour déplacer l’objet entier.</span><span class="sxs-lookup"><span data-stu-id="eb37e-227">Users can grab the bounding box to move the whole object.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-228">![Faire pivoter](images/3d-object-manipulation-rotate.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-228">![Rotate](images/3d-object-manipulation-rotate.jpg)</span></span><br>
        <span data-ttu-id="eb37e-229">**Faire pivoter**</span><span class="sxs-lookup"><span data-stu-id="eb37e-229">**Rotate**</span></span><br>
        <span data-ttu-id="eb37e-230">Les utilisateurs peuvent saisir les affordances de bord pour effectuer une rotation.</span><span class="sxs-lookup"><span data-stu-id="eb37e-230">Users can grab the edge affordances to rotate.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-231">![Mettre à l’échelle](images/3d-object-manipulation-scale.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-231">![Scale](images/3d-object-manipulation-scale.jpg)</span></span><br>
       <span data-ttu-id="eb37e-232">**Mettre à l’échelle**</span><span class="sxs-lookup"><span data-stu-id="eb37e-232">**Scale**</span></span><br>
       <span data-ttu-id="eb37e-233">Les utilisateurs peuvent saisir les affordances d’angle pour effectuer une mise à l’échelle uniforme.</span><span class="sxs-lookup"><span data-stu-id="eb37e-233">Users can grab the corner affordances to scale uniformly.</span></span>
    :::column-end:::
:::row-end:::

<br>


### <a name="non-affordance-based-manipulation"></a><span data-ttu-id="eb37e-234">Manipulation non basée sur l’affordance</span><span class="sxs-lookup"><span data-stu-id="eb37e-234">Non-affordance based manipulation</span></span>

<span data-ttu-id="eb37e-235">La manipulation sans affordance n’attache pas l’affordance au cadre englobant.</span><span class="sxs-lookup"><span data-stu-id="eb37e-235">Non-affordance-based manipulation does not attach affordance to the bounding box.</span></span> <span data-ttu-id="eb37e-236">Les utilisateurs peuvent uniquement faire apparaître le rectangle englobant, puis interagir directement avec celui-ci.</span><span class="sxs-lookup"><span data-stu-id="eb37e-236">Users can only reveal the bounding box, then directly interact with it.</span></span> <span data-ttu-id="eb37e-237">Si les utilisateurs se saisissent du rectangle englobant à une seule main, la translation et la rotation de l’objet sont associées au mouvement et à l’orientation de la main.</span><span class="sxs-lookup"><span data-stu-id="eb37e-237">If the bounding box is grabbed with one hand, the translation and rotation of the object are associated to motion and orientation of the hand.</span></span> <span data-ttu-id="eb37e-238">Quand les utilisateurs se saisissent de l’objet à deux mains, ils peuvent le translater, le mettre à l’échelle et le faire pivoter en fonction des mouvements relatifs des deux mains.</span><span class="sxs-lookup"><span data-stu-id="eb37e-238">When the object is grabbed with two hands, users can translate, scale, and rotate it according to relative motions of two hands.</span></span>

<span data-ttu-id="eb37e-239">Une manipulation spécifique nécessite de la précision.</span><span class="sxs-lookup"><span data-stu-id="eb37e-239">Specific manipulation requires precision.</span></span> <span data-ttu-id="eb37e-240">Nous vous recommandons d’utiliser la **manipulation basée sur l’affordance**, car elle offre un haut niveau de granularité.</span><span class="sxs-lookup"><span data-stu-id="eb37e-240">We recommend that you use **affordance-based manipulation** because it provides a high level of granularity.</span></span> <span data-ttu-id="eb37e-241">Pour une manipulation flexible, nous vous recommandons d’utiliser la **manipulation sans affordance**, car elle offre une approche instantanée et ludique.</span><span class="sxs-lookup"><span data-stu-id="eb37e-241">For flexible manipulation, we recommend you use **non-affordance manipulation** as it allows for instant and playful experiences.</span></span>

<br>

---


## <a name="instinctual-gestures"></a><span data-ttu-id="eb37e-242">Mouvements instinctifs</span><span class="sxs-lookup"><span data-stu-id="eb37e-242">Instinctual gestures</span></span>

<span data-ttu-id="eb37e-243">Avec HoloLens (1re génération), nous avons montré aux utilisateurs quelques mouvements prédéfinis, tels qu’écarter les doigts paume vers le haut et cliquer dans l’air.</span><span class="sxs-lookup"><span data-stu-id="eb37e-243">With HoloLens (1st gen), we taught users a couple of predefined gestures, such as bloom and air tap.</span></span> <span data-ttu-id="eb37e-244">Avec HoloLens 2, nous ne demandons pas aux utilisateurs de mémoriser des mouvements symboliques.</span><span class="sxs-lookup"><span data-stu-id="eb37e-244">For HoloLens 2, we don't ask users to memorize any symbolic gestures.</span></span> <span data-ttu-id="eb37e-245">Tous les mouvements nécessaires à l’utilisateur qui lui permettent d’interagir avec les hologrammes et le contenu sont instinctifs.</span><span class="sxs-lookup"><span data-stu-id="eb37e-245">All required user gestures, where users need to interact with holograms and content, are instinctual.</span></span> <span data-ttu-id="eb37e-246">Les mouvements instinctifs doivent aider les utilisateurs à effectuer des mouvements via les affordances d’IU conçues à cet effet.</span><span class="sxs-lookup"><span data-stu-id="eb37e-246">The way to achieve instinctual gestures is to help users perform gestures through the design of UI affordances.</span></span>

<span data-ttu-id="eb37e-247">Par exemple, si nous encourageons l’utilisateur à saisir un objet ou un point de contrôle en le pinçant avec deux doigts, l’objet ou le point de contrôle doit être petit.</span><span class="sxs-lookup"><span data-stu-id="eb37e-247">For example, if we encourage the user to grab an object or a control point with a two finger pinch, the object or the control point should be small.</span></span> <span data-ttu-id="eb37e-248">Si nous souhaitons que l’utilisateur le saisisse avec cinq doigts, l’objet ou le point de contrôle doit être relativement grand.</span><span class="sxs-lookup"><span data-stu-id="eb37e-248">If we want the user to perform five finger grab, the object or the control point should be relatively large.</span></span> <span data-ttu-id="eb37e-249">Si nous prenons l’exemple des boutons, un tout petit bouton oblige les utilisateurs à appuyer dessus avec un seul doigt ; un gros bouton incite les utilisateurs à appuyer dessus avec la paume de la main.</span><span class="sxs-lookup"><span data-stu-id="eb37e-249">Similar to buttons, a tiny button would limit users to press it with a single finger; a large button would encourage users to press it with their palms.</span></span>


:::row:::
    :::column:::
       <span data-ttu-id="eb37e-250">![Déplacer](images/instinctual-gestures-smallobject.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-250">![Move](images/instinctual-gestures-smallobject.jpg)</span></span><br>
       <span data-ttu-id="eb37e-251">**Petit objet**</span><span class="sxs-lookup"><span data-stu-id="eb37e-251">**Small object**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-252">![Faire pivoter](images/instinctual-gestures-mediumobject.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-252">![Rotate](images/instinctual-gestures-mediumobject.jpg)</span></span><br>
        <span data-ttu-id="eb37e-253">**Objet de taille moyenne**</span><span class="sxs-lookup"><span data-stu-id="eb37e-253">**Medium object**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="eb37e-254">![Mettre à l’échelle](images/instinctual-gestures-largeobject.jpg)</span><span class="sxs-lookup"><span data-stu-id="eb37e-254">![Scale](images/instinctual-gestures-largeobject.jpg)</span></span><br>
       <span data-ttu-id="eb37e-255">**Objet volumineux**</span><span class="sxs-lookup"><span data-stu-id="eb37e-255">**Large object**</span></span><br>
    :::column-end:::
:::row-end:::


<br>

---

<br>

## <a name="symmetric-design-between-hands-and-6-dof-controllers"></a><span data-ttu-id="eb37e-256">Conception symétrique entre les mains et les contrôleurs 6DoF</span><span class="sxs-lookup"><span data-stu-id="eb37e-256">Symmetric design between hands and 6 DoF controllers</span></span>

<span data-ttu-id="eb37e-257">Vous avez peut-être remarqué que nous pouvons établir des parallèles au niveau de l’interaction entre les mains en environnement AR (réalité augmentée) et les contrôleurs de mouvement en environnement VR (réalité virtuelle).</span><span class="sxs-lookup"><span data-stu-id="eb37e-257">You may have noticed that there are interaction parallels we can draw between hands in AR and motion controllers in VR.</span></span> <span data-ttu-id="eb37e-258">Les deux entrées peuvent être utilisées pour déclencher des manipulations directes dans leurs environnements respectifs.</span><span class="sxs-lookup"><span data-stu-id="eb37e-258">Both inputs can be used to trigger direct manipulations in their respective environments.</span></span> <span data-ttu-id="eb37e-259">Avec HoloLens 2, la saisie et le déplacement à l’aide des mains à courte distance fonctionnent de la même manière que le bouton de saisie des contrôleurs de mouvement WMR.</span><span class="sxs-lookup"><span data-stu-id="eb37e-259">In HoloLens 2, grabbing and dragging with hands at a close distance works much the same way as the grab button does on WMR motion controllers.</span></span> <span data-ttu-id="eb37e-260">Cela permet aux utilisateurs d’accéder à des interactions familières sur les deux plateformes. De plus, cela peut s’avérer utile si vous décidez de porter votre application d’une plateforme à l’autre.</span><span class="sxs-lookup"><span data-stu-id="eb37e-260">This provides users with interaction familiarity between the two platforms, which might prove useful if you ever decide to port your application from one to the other.</span></span>


<br>

---


<br>

---

## <a name="optimize-with-eye-tracking"></a><span data-ttu-id="eb37e-261">Optimiser avec l’eye-tracking</span><span class="sxs-lookup"><span data-stu-id="eb37e-261">Optimize with eye tracking</span></span>

<span data-ttu-id="eb37e-262">La manipulation directe peut paraître magique si elle fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="eb37e-262">Direct manipulation can feel magical if it works as intended.</span></span> <span data-ttu-id="eb37e-263">Mais elle peut également devenir frustrante si vous ne pouvez pas bouger votre main sans déclencher involontairement un hologramme.</span><span class="sxs-lookup"><span data-stu-id="eb37e-263">But it can also become frustrating if you can’t move your hand anywhere without unintentionally triggering a hologram.</span></span> <span data-ttu-id="eb37e-264">Le suivi oculaire peut vous aider à mieux identifier l’intention de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="eb37e-264">Eye tracking potentially helps to better identify what the user’s intent is.</span></span>

* <span data-ttu-id="eb37e-265">**Quand** : Réduisez le déclenchements par inadvertance d’une réponse à une manipulation.</span><span class="sxs-lookup"><span data-stu-id="eb37e-265">**When**: Reduce unintentionally triggering a manipulation response.</span></span> <span data-ttu-id="eb37e-266">L’eye-tracking permet de mieux comprendre l’engagement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="eb37e-266">Eye tracking allows for better understanding what a user is currently engaged with.</span></span>
<span data-ttu-id="eb37e-267">Par exemple, supposons que vous lisiez un texte holographique (instructions) quand vous tendez la main pour saisir votre outil de travail réel.</span><span class="sxs-lookup"><span data-stu-id="eb37e-267">For example, imagine you are reading through a holographic (instructional) text when reaching over to grab you real-world work tool.</span></span>

<span data-ttu-id="eb37e-268">En procédant ainsi, vous passez accidentellement votre main sur des boutons holographiques interactifs que vous n’aviez même pas remarqués auparavant (par exemple, situés en dehors du champ de vision de l’utilisateur (FoV)).</span><span class="sxs-lookup"><span data-stu-id="eb37e-268">By doing so, you accidentally move your hand across some interactive holographic buttons that you hadn't even noticed before (e.g. it  may be outside the user's field-of-view (FoV)).</span></span>

  <span data-ttu-id="eb37e-269">Pour faire court : Si l’utilisateur n’a pas regardé un hologramme depuis un certain temps et si un événement tactile ou de saisie a été détecté, il est probable que l’utilisateur n’avait pas réellement l’intention d’interagir avec cet hologramme.</span><span class="sxs-lookup"><span data-stu-id="eb37e-269">Long story short: If the user hasn't looked at a hologram for a while, yet a touch or grasp event has been detected for it, it is likely that the user wasn't actually intending to interact with that hologram.</span></span>

* <span data-ttu-id="eb37e-270">**Lequel** :  En plus du traitement des activations correspondant à des faux positifs, il est également possible d’améliorer l’identification des hologrammes à saisir ou à pousser, car le point d’intersection n’est pas forcément clair selon votre perspective, surtout si plusieurs hologrammes sont proches les uns des autres.</span><span class="sxs-lookup"><span data-stu-id="eb37e-270">**Which one**:  Aside from addressing false positive activations, another example includes better identifying which holograms to grab or poke as the precise intersection point may not be clear from your perspective, especially if several holograms are positioned close to each other.</span></span>

  <span data-ttu-id="eb37e-271">Bien que le suivi oculaire sur HoloLens 2 soit parfois limité au niveau de la précision avec laquelle il évalue votre regard, il peut être très utile pour les interactions rapprochées en raison de la disparité de la profondeur quand vous interagissez avec la saisie manuelle.</span><span class="sxs-lookup"><span data-stu-id="eb37e-271">While eye tracking on HoloLens 2 has limitations based on how accurately it can determine your eye gaze, this can still be very helpful for near interactions due to depth disparity when interacting with hand input.</span></span> <span data-ttu-id="eb37e-272">Cela signifie qu’il est parfois difficile de déterminer si votre main est placée derrière ou devant un hologramme pour saisir avec précision un widget de manipulation, par exemple.</span><span class="sxs-lookup"><span data-stu-id="eb37e-272">This means that it is sometimes difficult to determine whether your hand is behind or in front of a hologram to precisely grab a manipulation widget, for example.</span></span>

* <span data-ttu-id="eb37e-273">**Où** : Utilisez les informations relatives à ce qu’un utilisateur regarde avec des mouvements rapides.</span><span class="sxs-lookup"><span data-stu-id="eb37e-273">**Where to**: Use information about what a user is looking at with quick-throwing gestures.</span></span> <span data-ttu-id="eb37e-274">Saisissez un hologramme et lancez-le à peu près vers l’emplacement souhaité.</span><span class="sxs-lookup"><span data-stu-id="eb37e-274">Grab a hologram and roughly toss it toward your intended destination.</span></span>  

    <span data-ttu-id="eb37e-275">Bien que cela fonctionne parfois, les mouvements rapides de la main peuvent cibler des emplacements très imprécis.</span><span class="sxs-lookup"><span data-stu-id="eb37e-275">While this sometimes works, quickly performing hand gestures may result in highly inaccurate destinations.</span></span> <span data-ttu-id="eb37e-276">Toutefois, le suivi oculaire peut améliorer la précision du mouvement.</span><span class="sxs-lookup"><span data-stu-id="eb37e-276">However, eye tracking could improve the accuracy of the gesture.</span></span>

## <a name="see-also"></a><span data-ttu-id="eb37e-277">Voir également</span><span class="sxs-lookup"><span data-stu-id="eb37e-277">See also</span></span>

* [<span data-ttu-id="eb37e-278">Suivre de la tête et valider</span><span class="sxs-lookup"><span data-stu-id="eb37e-278">Head-gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="eb37e-279">Pointer et valider avec les mains</span><span class="sxs-lookup"><span data-stu-id="eb37e-279">Point and commit with hands</span></span>](point-and-commit.md)
* [<span data-ttu-id="eb37e-280">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="eb37e-280">Instinctual interactions</span></span>](interaction-fundamentals.md)
