---
title: Notions fondamentales d’interaction
description: Comme nous avons créé des expériences sur HoloLens (1er gen), 2 de HoloLens et des casques IMMERSIFS, nous avons commencé à écrire certaines choses que nous avons trouvé utiles pour partager.
author: rwinj
ms.author: jennyk
ms.date: 02/24/2019
ms.topic: article
keywords: Mixte réalité, interaction, concevoir
ms.openlocfilehash: d594126529b6314a4706f8b6b6af856058c3280a
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593246"
---
# <a name="interaction-fundamentals"></a><span data-ttu-id="6b485-104">Notions fondamentales d’interaction</span><span class="sxs-lookup"><span data-stu-id="6b485-104">Interaction fundamentals</span></span>

<span data-ttu-id="6b485-105">Comme nous avons créé des expériences sur HoloLens et des casques IMMERSIFS, nous avons commencé à écrire certaines choses que nous avons trouvé utiles pour partager.</span><span class="sxs-lookup"><span data-stu-id="6b485-105">As we've built experiences across HoloLens and immersive headsets, we've started writing down some things we found useful to share.</span></span> <span data-ttu-id="6b485-106">Considérez-les comme des blocs de construction fondamentaux pour la conception d’interaction de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="6b485-106">Think of these as the fundamental building blocks for mixed reality interaction design.</span></span>

## <a name="device-support"></a><span data-ttu-id="6b485-107">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="6b485-107">Device support</span></span>

<span data-ttu-id="6b485-108">Voici les articles de conception Interaction disponibles et les types ou le type d’appareil qu’ils s’appliquent à.</span><span class="sxs-lookup"><span data-stu-id="6b485-108">Here's an outline of the available Interaction design articles and which device type or types they apply to.</span></span>
<br>

<table>

<th>
<tr>

<td style="width:150px;"><span data-ttu-id="6b485-109"><strong>entrée</strong></span><span class="sxs-lookup"><span data-stu-id="6b485-109"><strong>Input</strong></span></span></td>
<td style="width:150px; text-align: center;"><span data-ttu-id="6b485-110"><a href="hololens-hardware-details.md"><strong>HoloLens (1er gen)</strong></a></span><span class="sxs-lookup"><span data-stu-id="6b485-110"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
<td style="width:150px; text-align: center;"><span data-ttu-id="6b485-111"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="6b485-111"><strong>HoloLens 2</strong></span></span></td>
<td style="width:150px; text-align: center;"><span data-ttu-id="6b485-112"><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></span><span class="sxs-lookup"><span data-stu-id="6b485-112"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
</tr>
</th>
 
<tr>
<td> <span data-ttu-id="6b485-113"><a href="gestures.md">Mains articulés</a></span><span class="sxs-lookup"><span data-stu-id="6b485-113"><a href="gestures.md">Articulated hands</a></span></span></td><td style="text-align: center;"></td><td style="text-align: center;"><span data-ttu-id="6b485-114">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-114">✔️</span></span></td><td></td>

</tr><tr>
<td> <span data-ttu-id="6b485-115"><a href="gaze-targeting.md">Ciblage des yeux</a></span><span class="sxs-lookup"><span data-stu-id="6b485-115"><a href="gaze-targeting.md">Eye targeting</a></span></span></td><td style="text-align: center;"></td><td style="text-align: center;"><span data-ttu-id="6b485-116">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-116">✔️</span></span></td><td style="text-align: center;"></td>
</tr><tr>
<td> <span data-ttu-id="6b485-117"><a href="gaze-targeting.md">Ciblage des regards</a></span><span class="sxs-lookup"><span data-stu-id="6b485-117"><a href="gaze-targeting.md">Gaze targeting</a></span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-118">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-118">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-119">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-119">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-120">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-120">✔️</span></span></td>
</tr><tr>
<td> <span data-ttu-id="6b485-121"><a href="gestures.md">Mouvements</a></span><span class="sxs-lookup"><span data-stu-id="6b485-121"><a href="gestures.md">Gestures</a></span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-122">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-122">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-123">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-123">✔️</span></span></td><td></td>
</tr><tr>
<td> <span data-ttu-id="6b485-124"><a href="voice-design.md">Conception de la voix</a></span><span class="sxs-lookup"><span data-stu-id="6b485-124"><a href="voice-design.md">Voice design</a></span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-125">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-125">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-126">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-126">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-127">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-127">✔️</span></span></td>
</tr><tr>
<td> <span data-ttu-id="6b485-128">Boîtier de commande</span><span class="sxs-lookup"><span data-stu-id="6b485-128">Gamepad</span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-129">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-129">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-130">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-130">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-131">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-131">✔️</span></span></td>
</tr>
<tr>
<td> <span data-ttu-id="6b485-132"><a href="motion-controllers.md">Contrôleurs de mouvement</a></span><span class="sxs-lookup"><span data-stu-id="6b485-132"><a href="motion-controllers.md">Motion controllers</a></span></span></td><td></td><td style="text-align: center;"></td><td style="text-align: center;"><span data-ttu-id="6b485-133">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-133">✔️</span></span></td>

</tr>
<th>
<tr>
<td style="width:150px;"><span data-ttu-id="6b485-134"><strong>Perception et des fonctionnalités spatiales</strong></span><span class="sxs-lookup"><span data-stu-id="6b485-134"><strong>Perception and spatial features</strong></span></span></td>
<td style="width:150px; text-align: center;"><span data-ttu-id="6b485-135"><a href="hololens-hardware-details.md"><strong>HoloLens (1er gen)</strong></a></span><span class="sxs-lookup"><span data-stu-id="6b485-135"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
<td style="width:150px; text-align: center;"><span data-ttu-id="6b485-136"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="6b485-136"><strong>HoloLens 2</strong></span></span></td>
<td style="width:150px; text-align: center;"><span data-ttu-id="6b485-137"><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></span><span class="sxs-lookup"><span data-stu-id="6b485-137"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
</tr>
</th>
<tr>

<td> <span data-ttu-id="6b485-138"><a href="spatial-sound-design.md">Sonorisation spatiale</a></span><span class="sxs-lookup"><span data-stu-id="6b485-138"><a href="spatial-sound-design.md">Spatial sound design</a></span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-139">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-139">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-140">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-140">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-141">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-141">✔️</span></span></td>
</tr><tr>
<td> <span data-ttu-id="6b485-142"><a href="spatial-mapping-design.md">Conception de mappage spatial</a></span><span class="sxs-lookup"><span data-stu-id="6b485-142"><a href="spatial-mapping-design.md">Spatial mapping design</a></span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-143">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-143">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-144">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-144">✔️</span></span></td><td></td>
</tr><tr>
<td> <span data-ttu-id="6b485-145"><a href="hologram.md">Hologrammes</a></span><span class="sxs-lookup"><span data-stu-id="6b485-145"><a href="hologram.md">Holograms</a></span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-146">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-146">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="6b485-147">✔️</span><span class="sxs-lookup"><span data-stu-id="6b485-147">✔️</span></span></td><td></td>
</tr>

</table>

## <a name="the-user-is-the-camera"></a><span data-ttu-id="6b485-148">L’utilisateur est l’appareil photo</span><span class="sxs-lookup"><span data-stu-id="6b485-148">The user is the camera</span></span>

![L’utilisateur est l’appareil photo](images/useriscamera-640px.jpg)

<span data-ttu-id="6b485-150">Pensez toujours conception pour votre point de vue utilisateur, lorsqu’ils circulent sur leur univers réels et virtuels.</span><span class="sxs-lookup"><span data-stu-id="6b485-150">Always think about design for your user's point of view as they move about their real and virtual worlds.</span></span>

<span data-ttu-id="6b485-151">**Certaines questions à poser**</span><span class="sxs-lookup"><span data-stu-id="6b485-151">**Some questions to ask**</span></span>
* <span data-ttu-id="6b485-152">Est l’utilisateur assis, inclinaison, permanent ou à pied lors de l’utilisation de votre expérience ?</span><span class="sxs-lookup"><span data-stu-id="6b485-152">Is the user sitting, reclining, standing, or walking while using your experience?</span></span>
* <span data-ttu-id="6b485-153">Comment votre contenu n’ajuste pas à des positions différentes ?</span><span class="sxs-lookup"><span data-stu-id="6b485-153">How does your content adjust to different positions?</span></span>
* <span data-ttu-id="6b485-154">L’utilisateur peut ajuster il ?</span><span class="sxs-lookup"><span data-stu-id="6b485-154">Can the user adjust it?</span></span>
* <span data-ttu-id="6b485-155">L’utilisateur sera à l’aise avec votre application ?</span><span class="sxs-lookup"><span data-stu-id="6b485-155">Will the user be comfortable using your app?</span></span>

<span data-ttu-id="6b485-156">**Bonnes pratiques**</span><span class="sxs-lookup"><span data-stu-id="6b485-156">**Best practices**</span></span>
* <span data-ttu-id="6b485-157">L’utilisateur est l’appareil photo et qu’ils contrôlent le déplacement.</span><span class="sxs-lookup"><span data-stu-id="6b485-157">The user is the camera and they control the movement.</span></span> <span data-ttu-id="6b485-158">Let leur lecteur.</span><span class="sxs-lookup"><span data-stu-id="6b485-158">Let them drive.</span></span>
* <span data-ttu-id="6b485-159">Si vous avez besoin transporter pratiquement de l’utilisateur, être sensible aux problèmes liés à la gêne VESTIBULAIRE.</span><span class="sxs-lookup"><span data-stu-id="6b485-159">If you need to virtually transport the user, be sensitive to issues around vestibular discomfort.</span></span>
* <span data-ttu-id="6b485-160">Utiliser des animations plus courtes</span><span class="sxs-lookup"><span data-stu-id="6b485-160">Use shorter animations</span></span>
* <span data-ttu-id="6b485-161">Animer à partir du bas à gauche/droite ou apparition en fondu au lieu de Z</span><span class="sxs-lookup"><span data-stu-id="6b485-161">Animate from down/left/right or fade in instead of Z</span></span>
* <span data-ttu-id="6b485-162">Ralentir le minutage</span><span class="sxs-lookup"><span data-stu-id="6b485-162">Slow down timing</span></span>
* <span data-ttu-id="6b485-163">Autoriser l’utilisateur d’afficher le monde en arrière-plan</span><span class="sxs-lookup"><span data-stu-id="6b485-163">Allow user to see the world in the background</span></span>

<span data-ttu-id="6b485-164">**Pratiques à éviter**</span><span class="sxs-lookup"><span data-stu-id="6b485-164">**What to avoid**</span></span>
* <span data-ttu-id="6b485-165">Ne secouez l’appareil photo ou volontairement le verrouiller à 3DOF (uniquement l’orientation, aucune traduction), elle peut rendre les utilisateurs à l’aise.</span><span class="sxs-lookup"><span data-stu-id="6b485-165">Don't shake the camera or purposely lock it to 3DOF (only orientation, no translation), it can make users feel uncomfortable.</span></span>
* <span data-ttu-id="6b485-166">Aucun mouvement brusque.</span><span class="sxs-lookup"><span data-stu-id="6b485-166">No abrupt movement.</span></span> <span data-ttu-id="6b485-167">Si vous avez besoin fournir un contenu vers ou à partir de l’utilisateur, déplacez-le lentement et sans heurts vers eux pour un maximum de confort.</span><span class="sxs-lookup"><span data-stu-id="6b485-167">If you need to bring content to or from the user, move it slowly and smoothly toward them for maximum comfort.</span></span> <span data-ttu-id="6b485-168">Les utilisateurs réagira aux menus volumineux à eux.</span><span class="sxs-lookup"><span data-stu-id="6b485-168">Users will react to large menus coming at them.</span></span>
* <span data-ttu-id="6b485-169">Ne pas accélérer ou désactiver la caméra de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6b485-169">Don't accelerate or turn the user's camera.</span></span> <span data-ttu-id="6b485-170">Les utilisateurs sont sensibles à l’accélération (angulaire et Translation).</span><span class="sxs-lookup"><span data-stu-id="6b485-170">Users are sensitive to acceleration (both angular and translational).</span></span>

## <a name="leverage-the-users-perspective"></a><span data-ttu-id="6b485-171">Tirer parti de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="6b485-171">Leverage the user's perspective</span></span>

<span data-ttu-id="6b485-172">Les utilisateurs voient le monde de la réalité mixte via affiche sur les appareils immersives et HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="6b485-172">Users see the world of mixed reality through displays on immersive and holographic devices.</span></span> <span data-ttu-id="6b485-173">Sur le HoloLens, cet affichage est appelé le [frame HOLOGRAPHIQUE](holographic-frame.md).</span><span class="sxs-lookup"><span data-stu-id="6b485-173">On the HoloLens, this display is called the [holographic frame](holographic-frame.md).</span></span>

<span data-ttu-id="6b485-174">Dans le développement 2D, contenu fréquemment sollicitée et des paramètres peuvent être placés dans les angles d’un écran pour les rendre facilement accessibles.</span><span class="sxs-lookup"><span data-stu-id="6b485-174">In 2D development, frequently accessed content and settings may be placed in the corners of a screen to make them easily accessible.</span></span> <span data-ttu-id="6b485-175">Toutefois, dans les applications HOLOGRAPHIQUE, contenu dans les coins de la vue peut être désagréable pour l’accès.</span><span class="sxs-lookup"><span data-stu-id="6b485-175">However, in holographic apps, content in the corners of the user's view may be uncomfortable to access.</span></span> <span data-ttu-id="6b485-176">Dans ce cas, le centre de l’image holographique est l’emplacement principal pour le contenu.</span><span class="sxs-lookup"><span data-stu-id="6b485-176">In this case, the center of the holographic frame is the prime location for content.</span></span>

<span data-ttu-id="6b485-177">L’utilisateur peut devoir être guidé pour aider à localiser les événements importants ou objets au-delà de leur vue immédiate.</span><span class="sxs-lookup"><span data-stu-id="6b485-177">The user may need to be guided to help locate important events or objects beyond their immediate view.</span></span> <span data-ttu-id="6b485-178">Vous pouvez utiliser les flèches, pistes claires, le déplacement de la tête de caractère, bulles, pointeurs, son spatial et invites vocales de guider l’utilisateur au contenu important dans votre application.</span><span class="sxs-lookup"><span data-stu-id="6b485-178">You can use arrows, light trails, character head movement, thought bubbles, pointers, spatial sound, and voice prompts to help guide the user to important content in your app.</span></span>

<span data-ttu-id="6b485-179">Il est recommandé de verrou pas votre contenu à l’écran pour le confort de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6b485-179">It is recommended to not lock content to the screen for the user's comfort.</span></span> <span data-ttu-id="6b485-180">Si vous devez conserver le contenu dans la vue, placez-le dans le monde et que le contenu « tag-along » comme le menu Démarrer.</span><span class="sxs-lookup"><span data-stu-id="6b485-180">If you need to keep content in view, place it in the world and make the content "tag-along" like the Start menu.</span></span> <span data-ttu-id="6b485-181">Contenu collectée, ainsi que l’utilisateur sera sembler plus naturelle dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="6b485-181">Content that gets pulled along with the user's perspective will feel more natural in the environment.</span></span>

<span data-ttu-id="6b485-182">![Le menu Démarrer suit la vue de l’utilisateur lorsqu’il atteint le bord du frame](images/tagalong-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="6b485-182">![The start menu follows the user's view when it reaches the edge of the frame](images/tagalong-1000px.jpg)</span></span><br>
<span data-ttu-id="6b485-183">*Le menu Démarrer suit la vue de l’utilisateur lorsqu’il atteint le bord du frame*</span><span class="sxs-lookup"><span data-stu-id="6b485-183">*The Start menu follows the user's view when it reaches the edge of the frame*</span></span>

<span data-ttu-id="6b485-184">Sur HoloLens, hologrammes sentiront réels lorsqu’elles s’inscrivent dans le cadre HOLOGRAPHIQUE dans la mesure où ils ne coupés.</span><span class="sxs-lookup"><span data-stu-id="6b485-184">On HoloLens, holograms feel real when they fit within the holographic frame since they don't get cut off.</span></span> <span data-ttu-id="6b485-185">Les utilisateurs se déplacera afin de voir les limites d’un hologramme dans le cadre.</span><span class="sxs-lookup"><span data-stu-id="6b485-185">Users will move in order to see the bounds of a hologram within the frame.</span></span> <span data-ttu-id="6b485-186">Sur HoloLens, il est important de simplifier votre interface utilisateur pour tenir dans la vue de l’utilisateur et de conserver le focus sur l’action principale.</span><span class="sxs-lookup"><span data-stu-id="6b485-186">On HoloLens, it's important to simplify your UI to fit within the user's view and keep your focus on the main action.</span></span> <span data-ttu-id="6b485-187">Pour des casques IMMERSIFS, il est important de conserver l’illusion d’un monde virtuel persistant dans le champ de vision de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="6b485-187">For immersive headsets, it's important to maintain the illusion of a persistent virtual world within the device's field of view.</span></span>

## <a name="user-comfort"></a><span data-ttu-id="6b485-188">Confort de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="6b485-188">User comfort</span></span>

<span data-ttu-id="6b485-189">Pour vous assurer de maximum [confort](comfort.md) sur Afficheur tête haute, il est important pour les concepteurs et développeurs de créer et présenter du contenu d’une manière qui imite comment humains interprètent des formes 3D et la position relative des objets dans le naturel World.</span><span class="sxs-lookup"><span data-stu-id="6b485-189">To ensure maximum [comfort](comfort.md) on head-mounted displays, it’s important for designers and developers to create and present content in a way that mimics how humans interpret 3D shapes and the relative position of objects in the natural world.</span></span> <span data-ttu-id="6b485-190">À partir d’un point de vue physique, il est également important de concevoir le contenu qui ne nécessite pas de mouvements fatigante du cou ou armements.</span><span class="sxs-lookup"><span data-stu-id="6b485-190">From a physical perspective, it is also important to design content that does not require fatiguing motions of the neck or arms.</span></span>

<span data-ttu-id="6b485-191">Si le développement pour HoloLens ou des casques IMMERSIFS, il est important de restituer les éléments visuels pour deux yeux.</span><span class="sxs-lookup"><span data-stu-id="6b485-191">Whether developing for HoloLens or immersive headsets, it is important to render visuals for both eyes.</span></span> <span data-ttu-id="6b485-192">Rendu d’un affichage tête haute dans un oeil uniquement peut rendre une interface difficile à comprendre, ainsi qu’à l’origine d’uneasiness aux yeux de l’utilisateur et le cerveau.</span><span class="sxs-lookup"><span data-stu-id="6b485-192">Rendering a heads-up display in one eye only can make an interface hard to understand, as well as causing uneasiness to the user's eye and brain.</span></span>

## <a name="share-your-experience"></a><span data-ttu-id="6b485-193">Partagez votre expérience</span><span class="sxs-lookup"><span data-stu-id="6b485-193">Share your experience</span></span>

<span data-ttu-id="6b485-194">À l’aide de [mixte de capture de la réalité](mixed-reality-capture.md), les utilisateurs peuvent capturer une photo ou une vidéo de leur expérience à tout moment.</span><span class="sxs-lookup"><span data-stu-id="6b485-194">Using [mixed reality capture](mixed-reality-capture.md), users can capture a photo or video of their experience at any time.</span></span> <span data-ttu-id="6b485-195">Envisagez d’expériences dans votre application où vous voulez encourager des captures instantanées ou des vidéos.</span><span class="sxs-lookup"><span data-stu-id="6b485-195">Consider experiences in your app where you may want to encourage snapshots or videos.</span></span>

## <a name="leverage-basic-ui-elements-of-the-windows-mixed-reality-home"></a><span data-ttu-id="6b485-196">Tirer parti des éléments de l’interface utilisateur de base de Windows Mixed Reality domestique</span><span class="sxs-lookup"><span data-stu-id="6b485-196">Leverage basic UI elements of the Windows Mixed Reality home</span></span>

<span data-ttu-id="6b485-197">Tout comme l’expérience de PC de Windows démarre avec le bureau, Windows Mixed Reality commence par la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="6b485-197">Just like the Windows PC experience starts with the desktop, Windows Mixed Reality starts with the home.</span></span> <span data-ttu-id="6b485-198">Le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) tire parti de notre capacité intégrée dès le départ pour comprendre et de parcourir les emplacements 3D.</span><span class="sxs-lookup"><span data-stu-id="6b485-198">The [Windows Mixed Reality home](navigating-the-windows-mixed-reality-home.md) leverages our innate ability to understand and navigate 3D places.</span></span> <span data-ttu-id="6b485-199">Avec HoloLens, votre page d’accueil est votre espace physique.</span><span class="sxs-lookup"><span data-stu-id="6b485-199">With HoloLens, your home is your physical space.</span></span> <span data-ttu-id="6b485-200">Avec des casques IMMERSIFS, votre page d’accueil est virtuel.</span><span class="sxs-lookup"><span data-stu-id="6b485-200">With immersive headsets, your home is a virtual place.</span></span>

<span data-ttu-id="6b485-201">Votre page d’accueil est également où vous utiliserez le menu Démarrer pour ouvrir et de placer les applications et le contenu.</span><span class="sxs-lookup"><span data-stu-id="6b485-201">Your home is also where you’ll use the Start menu to open and place apps and content.</span></span> <span data-ttu-id="6b485-202">Vous pouvez remplir votre page d’accueil avec du contenu de la réalité mixte et plusieurs tâches à l’aide de plusieurs applications en même temps.</span><span class="sxs-lookup"><span data-stu-id="6b485-202">You can fill your home with mixed reality content and multitask by using multiple apps at the same time.</span></span> <span data-ttu-id="6b485-203">Les éléments que vous placez dans votre page d’accueil resteront, même si vous redémarrez votre appareil.</span><span class="sxs-lookup"><span data-stu-id="6b485-203">The things you place in your home stay there, even if you restart your device.</span></span>

## <a name="see-also"></a><span data-ttu-id="6b485-204">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6b485-204">See also</span></span>
* [<span data-ttu-id="6b485-205">Ciblage des regards</span><span class="sxs-lookup"><span data-stu-id="6b485-205">Gaze targeting</span></span>](gaze-targeting.md)
* [<span data-ttu-id="6b485-206">Mouvements</span><span class="sxs-lookup"><span data-stu-id="6b485-206">Gestures</span></span>](gestures.md)
* [<span data-ttu-id="6b485-207">Conception de la voix</span><span class="sxs-lookup"><span data-stu-id="6b485-207">Voice design</span></span>](voice-design.md)
* [<span data-ttu-id="6b485-208">Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="6b485-208">Motion controllers</span></span>](motion-controllers.md)
* [<span data-ttu-id="6b485-209">Sonorisation spatiale</span><span class="sxs-lookup"><span data-stu-id="6b485-209">Spatial sound design</span></span>](spatial-sound-design.md)
* [<span data-ttu-id="6b485-210">Conception de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="6b485-210">Spatial mapping design</span></span>](spatial-mapping-design.md)
* [<span data-ttu-id="6b485-211">Confort</span><span class="sxs-lookup"><span data-stu-id="6b485-211">Comfort</span></span>](comfort.md)
* [<span data-ttu-id="6b485-212">Navigation dans Windows Mixed Reality domestique</span><span class="sxs-lookup"><span data-stu-id="6b485-212">Navigating the Windows Mixed Reality home</span></span>](navigating-the-windows-mixed-reality-home.md)
