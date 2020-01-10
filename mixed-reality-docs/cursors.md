---
title: Curseurs
description: Un curseur, ou un indicateur de votre vecteur de ciblage, fournit des commentaires continus permettant à l’utilisateur de comprendre ce que HoloLens comprend pour ses intentions.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: HoloLens (1re génération), HoloLens 2, réalité mixte, curseurs, ciblage, point de regard, mouvements
ms.openlocfilehash: 969906cb09e100dbdd289d78baba722a4bd32537
ms.sourcegitcommit: 6844930427b658ae31f642c395cd8a3b3cdbf857
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75723238"
---
# <a name="cursors"></a><span data-ttu-id="afb6f-104">Curseurs</span><span class="sxs-lookup"><span data-stu-id="afb6f-104">Cursors</span></span>

![Curseurs](images/UX/UX_Hero_Cursor.jpg)

<span data-ttu-id="afb6f-106">Un curseur, ou un indicateur de votre vecteur de ciblage actuel, fournit à l’utilisateur des commentaires continus pour comprendre où le casque pense qu’il est actuellement actif.</span><span class="sxs-lookup"><span data-stu-id="afb6f-106">A cursor, or indicator of your current targeting vector, provides continuous feedback for the user to understand where the headset believes their current focus is at that time.</span></span> <span data-ttu-id="afb6f-107">Le curseur permet à l’utilisateur de comprendre son point de ciblage actuel et agit comme un feedback pour indiquer la zone, l’hologramme ou le point qui répondra à l’entrée.</span><span class="sxs-lookup"><span data-stu-id="afb6f-107">The cursor allows the user to understand their current targeting point and acts as feedback to indicate what area, hologram, or point will respond to input.</span></span> <span data-ttu-id="afb6f-108">Il s’agit de la représentation numérique de l’endroit où l’appareil comprend l’attention de l’utilisateur (bien que cela puisse ne pas être le même que pour déterminer quoi que ce soit sur leurs intentions).</span><span class="sxs-lookup"><span data-stu-id="afb6f-108">It is the digital representation of where the device understands the user's attention to be (though that may not be the same as determining anything about their intentions).</span></span>

<span data-ttu-id="afb6f-109">Les commentaires fournis par le curseur permettent aux utilisateurs d’anticiper la façon dont le système répondra, utilisez ce signal comme commentaires afin de mieux communiquer leur intention à l’appareil et, en dernier lieu, soyez plus convaincu de leurs interactions.</span><span class="sxs-lookup"><span data-stu-id="afb6f-109">The feedback provided by the cursor offers users the ability to anticipate how the system will respond, use that signal as feedback to better communicate their intention to the device, and ultimately be more confident about their interactions.</span></span>

<span data-ttu-id="afb6f-110">Il existe 3 types de curseurs : **Finger, Ray**et **point-regard**.</span><span class="sxs-lookup"><span data-stu-id="afb6f-110">There are 3 kinds of cursors: **finger, ray**, and **head-gaze**.</span></span> <span data-ttu-id="afb6f-111">Ces curseurs de pointage fonctionnent avec différentes modalités d’entrée sur HoloLens, HoloLens 2 et les casques immersifs.</span><span class="sxs-lookup"><span data-stu-id="afb6f-111">These pointing cursors work with different input modalities on HoloLens, HoloLens 2, and immersive headsets.</span></span> <span data-ttu-id="afb6f-112">Vous trouverez ci-dessous des conseils sur le type de curseur à utiliser pour chaque type de casque et de modèle d’interaction.</span><span class="sxs-lookup"><span data-stu-id="afb6f-112">Below is guidance on which type of cursor to use for each type of headset and interaction model.</span></span> <span data-ttu-id="afb6f-113">Dans la boîte à outils de la réalité mixte (MRTK), nous avons créé des modules de curseurs de glisser-déplacer pour vous aider à créer l’expérience de pointage appropriée.</span><span class="sxs-lookup"><span data-stu-id="afb6f-113">In the Mixed Reality Toolkit (MRTK), we've created drag-and-drop cursors modules to help you build the right pointing experience.</span></span>


## <a name="device-support"></a><span data-ttu-id="afb6f-114">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="afb6f-114">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="afb6f-115"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="afb6f-115"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="afb6f-116"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="afb6f-116"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="afb6f-117"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="afb6f-117"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="afb6f-118"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="afb6f-118"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="afb6f-119">Curseur Finger</span><span class="sxs-lookup"><span data-stu-id="afb6f-119">Finger cursor</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="afb6f-120">✔️</span><span class="sxs-lookup"><span data-stu-id="afb6f-120">✔️</span></span></td>
        <td>❌</td>
    </tr>
     <tr>
        <td><span data-ttu-id="afb6f-121">Curseur Ray</span><span class="sxs-lookup"><span data-stu-id="afb6f-121">Ray cursor</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="afb6f-122">✔️</span><span class="sxs-lookup"><span data-stu-id="afb6f-122">✔️</span></span></td>
        <td><span data-ttu-id="afb6f-123">✔️</span><span class="sxs-lookup"><span data-stu-id="afb6f-123">✔️</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="afb6f-124">Curseur en tête</span><span class="sxs-lookup"><span data-stu-id="afb6f-124">Head-gaze cursor</span></span></td>
        <td><span data-ttu-id="afb6f-125">✔️</span><span class="sxs-lookup"><span data-stu-id="afb6f-125">✔️</span></span></td>
        <td><span data-ttu-id="afb6f-126">✔️</span><span class="sxs-lookup"><span data-stu-id="afb6f-126">✔️</span></span></td>
        <td><span data-ttu-id="afb6f-127">✔️</span><span class="sxs-lookup"><span data-stu-id="afb6f-127">✔️</span></span></td>
    </tr>
</table>

## <a name="finger-cursor"></a><span data-ttu-id="afb6f-128">Curseur Finger</span><span class="sxs-lookup"><span data-stu-id="afb6f-128">Finger cursor</span></span>
<span data-ttu-id="afb6f-129">Le curseur Finger est disponible uniquement sur le HoloLens 2 pour améliorer le mode d’interaction «[manipulation directe avec mains](direct-manipulation.md)».</span><span class="sxs-lookup"><span data-stu-id="afb6f-129">The finger cursor is available only on the HoloLens 2 to enhance the "[direct manipulation with hands](direct-manipulation.md)" interaction mode.</span></span> <span data-ttu-id="afb6f-130">Pour mieux comprendre où se trouve le doigt, nous avons attaché des anneaux aux conseils des deux doigts d’index.</span><span class="sxs-lookup"><span data-stu-id="afb6f-130">To better understand where the finger is pointing, we have attached rings to the tips of both index fingers.</span></span> <span data-ttu-id="afb6f-131">La taille de la sonnerie est basée sur la proximité du doigt par rapport à la surface de l’interface utilisateur (plus le doigt est proche de la petite sonnerie) et se réduit à une forme de point lorsque le doigt fait contact avec l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="afb6f-131">The ring size is based on the proximity of the finger to the UI surface (the closer the finger, the smaller the ring) and will shrink to a dot shape when the finger makes contact with the UI.</span></span> <br>

<span data-ttu-id="afb6f-132">curseur ![Finger](images/finger-cursor.png)</span><span class="sxs-lookup"><span data-stu-id="afb6f-132">![finger cursor](images/finger-cursor.png)</span></span><br>
<span data-ttu-id="afb6f-133">**Commentaires visuels États de Finger Cursor** 1 : l’anneau se réduit à un point.</span><span class="sxs-lookup"><span data-stu-id="afb6f-133">**Visual feedback states of finger cursor** 1: The ring shrinks to a dot.</span></span> <span data-ttu-id="afb6f-134">2 : l’anneau s’aligne sur la surface.</span><span class="sxs-lookup"><span data-stu-id="afb6f-134">2: The ring aligns with surface.</span></span> <span data-ttu-id="afb6f-135">3 : l’anneau est perpendiculaire au vecteur Finger.</span><span class="sxs-lookup"><span data-stu-id="afb6f-135">3: The ring is perpendicular to finger vector.</span></span> <span data-ttu-id="afb6f-136">4 : aucune sonnerie.</span><span class="sxs-lookup"><span data-stu-id="afb6f-136">4: No ring.</span></span>

## <a name="ray-cursor"></a><span data-ttu-id="afb6f-137">Curseur Ray</span><span class="sxs-lookup"><span data-stu-id="afb6f-137">Ray cursor</span></span>
<span data-ttu-id="afb6f-138">Les curseurs de rayon sont attachés à la fin des rayons de pointage éloignés pour permettre la manipulation des objets qui ne sont pas en contact avec la main.</span><span class="sxs-lookup"><span data-stu-id="afb6f-138">Ray cursors attach to the end of far pointing rays to allow manipulation of objects that are out of hands-reach.</span></span> <span data-ttu-id="afb6f-139">Dans les casques immersifs, les rayons se déplacent des contrôleurs de mouvement et se terminent par des points-curseurs.</span><span class="sxs-lookup"><span data-stu-id="afb6f-139">In immersive headsets, the rays shoot out from motion controllers and end in dot cursors.</span></span> <span data-ttu-id="afb6f-140">Dans HoloLens 2, nous utilisons le modèle mental de ces rayons de contrôleur de mouvement et les rayons de main qui proviennent des palmiers et se terminent par les curseurs en forme d’anneau qui sont cohérents avec les curseurs Finger utilisés dans la manipulation directe.</span><span class="sxs-lookup"><span data-stu-id="afb6f-140">In HoloLens 2, we leverage the mental model of these motion controller rays and designed hand rays that originate from the palms and end in ring-shaped cursors that are consistent with finger cursors used in direct manipulation.</span></span> <br>
:::row:::
    :::column:::
        <span data-ttu-id="afb6f-141">contrôleur de curseur ![Ray](images/ray-cursor-controller.png)</span><span class="sxs-lookup"><span data-stu-id="afb6f-141">![Ray cursor controller](images/ray-cursor-controller.png)</span></span><br>
        <span data-ttu-id="afb6f-142">**Curseurs de rayon de contrôleurs de mouvement**</span><span class="sxs-lookup"><span data-stu-id="afb6f-142">**Ray cursors of motion controllers**</span></span><br>
    :::column-end:::
    :::column:::
        <span data-ttu-id="afb6f-143">curseur ![Ray](images/ray-cursor-hand.png)</span><span class="sxs-lookup"><span data-stu-id="afb6f-143">![Ray cursor hand](images/ray-cursor-hand.png)</span></span><br>
        <span data-ttu-id="afb6f-144">**Curseurs de Ray des mains**</span><span class="sxs-lookup"><span data-stu-id="afb6f-144">**Ray cursors of hands**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="head-gaze-cursor"></a><span data-ttu-id="afb6f-145">Curseur en tête</span><span class="sxs-lookup"><span data-stu-id="afb6f-145">Head-gaze cursor</span></span>
<span data-ttu-id="afb6f-146">Le curseur en tête est un point qui s’attache à la fin d’un vecteur de pointage de tête invisible qui utilise la position et la rotation de l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="afb6f-146">The head-gaze cursor is a dot that attaches to the end of an invisible head-gaze vector that uses the position and rotation of the head to point.</span></span> <span data-ttu-id="afb6f-147">Pour exécuter des actions, ce curseur de pointage est associé à diverses entrées de validation telles que le TAP-Air, les commandes vocales, le son et l’enfoncement de bouton.</span><span class="sxs-lookup"><span data-stu-id="afb6f-147">To execute actions, this pointing cursor is paired with various commit inputs such as air tap, voice commands, dwell, and button press.</span></span> <span data-ttu-id="afb6f-148">Dans HoloLens 2, le point de regard est le mieux associé à toute entrée de validation qui n’est pas de pression pneumatique, car il y aura un conflit d’interaction entre les rayons d’appui et de loin.</span><span class="sxs-lookup"><span data-stu-id="afb6f-148">In HoloLens 2, head-gaze is best paired with any commit input that is not air tap, as there will be interaction conflict between air tap and far hand rays.</span></span> <br>
:::row:::
    :::column:::
        <span data-ttu-id="afb6f-149">![la main du point d’insertion de la tête](images/head-gaze-cursor-hand.png)</span><span class="sxs-lookup"><span data-stu-id="afb6f-149">![Head gaze cursor hand](images/head-gaze-cursor-hand.png)</span></span><br>
        <span data-ttu-id="afb6f-150">**Curseur en tête avec mouvement vers la main**</span><span class="sxs-lookup"><span data-stu-id="afb6f-150">**Head-gaze cursor with hand gesture**</span></span><br>
    :::column-end:::
    :::column:::
        <span data-ttu-id="afb6f-151">](images/head-gaze-cursor-voice.png) de la voix du curseur en tête ![</span><span class="sxs-lookup"><span data-stu-id="afb6f-151">![Head gaze cursor voice](images/head-gaze-cursor-voice.png)</span></span><br>
        <span data-ttu-id="afb6f-152">**Curseur en tête avec commande vocale**</span><span class="sxs-lookup"><span data-stu-id="afb6f-152">**Head-gaze cursor with voice command**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="cursor-customization-recommendations"></a><span data-ttu-id="afb6f-153">Recommandations sur la personnalisation des curseurs</span><span class="sxs-lookup"><span data-stu-id="afb6f-153">Cursor customization recommendations</span></span>
<span data-ttu-id="afb6f-154">Si vous souhaitez personnaliser les comportements et les apparences de commentaires des curseurs, voici quelques recommandations en matière de conception :</span><span class="sxs-lookup"><span data-stu-id="afb6f-154">If you would like to customize the cursor feedback behaviors and appearances, here are some design recommendations:</span></span>

### <a name="cursor-scale"></a><span data-ttu-id="afb6f-155">Échelle du curseur</span><span class="sxs-lookup"><span data-stu-id="afb6f-155">Cursor scale</span></span>
* <span data-ttu-id="afb6f-156">Le curseur ne doit pas être plus grand que les cibles disponibles, ce qui permet aux utilisateurs d’interagir facilement avec et d’afficher le contenu.</span><span class="sxs-lookup"><span data-stu-id="afb6f-156">The cursor should be no larger than the available targets, allowing users to easily interact with and view the content.</span></span>
* <span data-ttu-id="afb6f-157">En fonction de l’expérience que vous créez, il est également important de mettre à l’échelle le curseur à mesure que l’utilisateur regarde.</span><span class="sxs-lookup"><span data-stu-id="afb6f-157">Depending on the experience you create, scaling the cursor as the user looks around is also an important consideration.</span></span> <span data-ttu-id="afb6f-158">Par exemple, à mesure que l’utilisateur regarde plus loin dans votre expérience, le curseur ne doit pas être trop petit pour être perdu.</span><span class="sxs-lookup"><span data-stu-id="afb6f-158">For example, as the user looks further away in your experience, the cursor should not become too small such that it's lost.</span></span>
* <span data-ttu-id="afb6f-159">Lors de la mise à l’échelle du curseur, envisagez d’appliquer une animation douce à celle-ci lorsqu’il est mis à l’échelle pour lui attribuer une sensation organique.</span><span class="sxs-lookup"><span data-stu-id="afb6f-159">When scaling the cursor, consider applying a soft animation to it as it scales to give it an organic feeling.</span></span>
* <span data-ttu-id="afb6f-160">Évitez d’obstruer le contenu.</span><span class="sxs-lookup"><span data-stu-id="afb6f-160">Avoid obstructing content.</span></span> <span data-ttu-id="afb6f-161">Les hologrammes sont ce qui rend l’expérience mémorable et le curseur ne doit pas être pris en charge.</span><span class="sxs-lookup"><span data-stu-id="afb6f-161">Holograms are what make the experience memorable and the cursor should not be taking away from them.</span></span>

### <a name="directionless-cursor-shape"></a><span data-ttu-id="afb6f-162">Forme de curseur dédirectionnelle</span><span class="sxs-lookup"><span data-stu-id="afb6f-162">Directionless cursor shape</span></span>
* <span data-ttu-id="afb6f-163">Bien qu’il n’y ait pas de forme de curseur droite, nous vous recommandons d’utiliser une forme sans direction comme un tore.</span><span class="sxs-lookup"><span data-stu-id="afb6f-163">Although there is no one right cursor shape, we recommend that you use a directionless shape like a torus.</span></span> <span data-ttu-id="afb6f-164">Un curseur qui pointe dans une certaine direction (par exemple, un curseur en forme de flèche traditionnel) peut dérouter l’utilisateur pour qu’il se présente toujours de cette façon.</span><span class="sxs-lookup"><span data-stu-id="afb6f-164">A cursor that points in some direction (For example, a traditional arrow cursor) might confuse the user to always look that way.</span></span>
* <span data-ttu-id="afb6f-165">Une exception est lors de l’utilisation du curseur pour communiquer des instructions d’interaction à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="afb6f-165">An exception to this is when using the cursor to communicate interaction instruction to the user.</span></span> <span data-ttu-id="afb6f-166">Par exemple, lors de la mise à l’échelle d’hologrammes dans le système d’exploitation de réalité mixte, le curseur comprend temporairement des flèches qui indiquent à l’utilisateur comment déplacer sa main pour mettre l’hologramme à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="afb6f-166">For example, when scaling holograms in the Mixed Reality OS, the cursor temporarily includes arrows that instructs the user on how to move their hand to scale the hologram.</span></span>

### <a name="look-and-feel"></a><span data-ttu-id="afb6f-167">Apparence</span><span class="sxs-lookup"><span data-stu-id="afb6f-167">Look and feel</span></span>
* <span data-ttu-id="afb6f-168">Un curseur en forme de bouée ou de Tore fonctionne pour de nombreuses applications.</span><span class="sxs-lookup"><span data-stu-id="afb6f-168">A donut or torus shaped cursor works for a lot of applications.</span></span>
* <span data-ttu-id="afb6f-169">Choisissez une couleur et une forme qui correspond le mieux à l’expérience que vous créez.</span><span class="sxs-lookup"><span data-stu-id="afb6f-169">Pick a color and shape that best represents the experience you are creating.</span></span>
* <span data-ttu-id="afb6f-170">Les curseurs sont particulièrement sujets à la [séparation des couleurs](hologram-stability.md#color-separation).</span><span class="sxs-lookup"><span data-stu-id="afb6f-170">Cursors are especially prone to [color separation](hologram-stability.md#color-separation).</span></span>
* <span data-ttu-id="afb6f-171">Un petit curseur avec une opacité équilibrée conserve l’information, sans qui prennent la hiérarchie visuelle.</span><span class="sxs-lookup"><span data-stu-id="afb6f-171">A small cursor with balanced opacity keeps it informative without dominating the visual hierarchy.</span></span>
* <span data-ttu-id="afb6f-172">Soyez Cognizant de l’utilisation des ombres ou des surbrillances derrière votre curseur, car elles peuvent entraver le contenu et nuire à la tâche en cours.</span><span class="sxs-lookup"><span data-stu-id="afb6f-172">Be cognizant of using shadows or highlights behind your cursor as they might obstruct content and distract from the task at hand.</span></span>
* <span data-ttu-id="afb6f-173">Les curseurs doivent s’aligner sur les surfaces de votre application et les étreinter, ce qui donne à l’utilisateur un sentiment que le système peut voir où il regarde, mais également que le système est conscient de son environnement.</span><span class="sxs-lookup"><span data-stu-id="afb6f-173">Cursors should align to and hug the surfaces in your app, this will give the user a feeling that the system can see where they are looking, but also that the system is aware of their surroundings.</span></span> <span data-ttu-id="afb6f-174">Par exemple, dans le système d’exploitation de la réalité mixte, le curseur s’aligne sur les surfaces du monde de l’utilisateur, ce qui crée un sentiment de conscience du monde même lorsque l’utilisateur n’est pas directement à l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="afb6f-174">For example, in the Mixed Reality OS, the cursor aligns to the surfaces of the user's world, creating a feeling of awareness of the world even when the user isn't looking directly at a hologram.</span></span>
* <span data-ttu-id="afb6f-175">Le verrouillage magnétique du curseur sur un élément interactif lorsque celui-ci est proche de proximité peut contribuer à améliorer la confiance que l’utilisateur interagit avec cet élément lorsqu’il effectue une action de sélection.</span><span class="sxs-lookup"><span data-stu-id="afb6f-175">Magnetically locking the cursor to an interactive element when it is within close proximity can help improve confidence that user will interact with that element when they perform a selection action.</span></span>

### <a name="visual-cues"></a><span data-ttu-id="afb6f-176">Signaux visuels</span><span class="sxs-lookup"><span data-stu-id="afb6f-176">Visual cues</span></span>
* <span data-ttu-id="afb6f-177">Si votre expérience est axée sur un seul hologramme, votre curseur doit s’aligner sur cet hologramme et changer de forme lorsque vous examinez l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="afb6f-177">If your experience is focused on a single hologram, your cursor should align and hug only that hologram and change shape when you look away from that hologram.</span></span> <span data-ttu-id="afb6f-178">Cela peut indiquer à l’utilisateur que l’hologramme est actionnable et qu’il peut interagir avec lui.</span><span class="sxs-lookup"><span data-stu-id="afb6f-178">This can convey to the user that the hologram is actionable and they can interact with it.</span></span>
* <span data-ttu-id="afb6f-179">Si votre application utilise le mappage spatial, votre curseur peut s’aligner sur chaque surface visible.</span><span class="sxs-lookup"><span data-stu-id="afb6f-179">If your application uses spatial mapping, then your cursor could align and hug every surface it sees.</span></span> <span data-ttu-id="afb6f-180">Ainsi, les utilisateurs peuvent voir que HoloLens et votre application peuvent voir leur espace.</span><span class="sxs-lookup"><span data-stu-id="afb6f-180">This gives feedback to the users that HoloLens and your application can see their space.</span></span> <span data-ttu-id="afb6f-181">Cela renforce le fait que les hologrammes sont réels et dans notre monde et permet de combler le fossé entre les véritables et les virtuels.</span><span class="sxs-lookup"><span data-stu-id="afb6f-181">This reinforces the fact that holograms are real and in our world and helps bridge the gap between real and virtual.</span></span>
* <span data-ttu-id="afb6f-182">Avoir une idée de ce que le curseur doit faire lorsqu’il n’y a pas d’hologrammes ou de surfaces en vue.</span><span class="sxs-lookup"><span data-stu-id="afb6f-182">Have an idea of what the cursor should do when there are no holograms or surfaces in view.</span></span> <span data-ttu-id="afb6f-183">La placer à une distance prédéterminée devant l’utilisateur est une option.</span><span class="sxs-lookup"><span data-stu-id="afb6f-183">Placing it at a predetermined distance in front of the user is one option.</span></span>

### <a name="possible-actions"></a><span data-ttu-id="afb6f-184">Actions possibles</span><span class="sxs-lookup"><span data-stu-id="afb6f-184">Possible actions</span></span>
* <span data-ttu-id="afb6f-185">Le curseur peut être représenté par différentes icônes pour indiquer les actions possibles qu’un hologramme peut effectuer, par exemple la mise à l’échelle ou la rotation.</span><span class="sxs-lookup"><span data-stu-id="afb6f-185">The cursor can be represented by different icons to convey possible actions a hologram can perform, such as scaling or rotation.</span></span>
* <span data-ttu-id="afb6f-186">Ajoutez uniquement des informations supplémentaires sur le curseur si cela revient à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="afb6f-186">Only add extra information on the cursor if it means something to the user.</span></span> <span data-ttu-id="afb6f-187">Dans le cas contraire, les utilisateurs peuvent ne pas remarquer les modifications d’État ou être confondus par le curseur.</span><span class="sxs-lookup"><span data-stu-id="afb6f-187">Otherwise, users might either not notice the state changes or get confused by the cursor.</span></span>

### <a name="input-state"></a><span data-ttu-id="afb6f-188">État d’entrée</span><span class="sxs-lookup"><span data-stu-id="afb6f-188">Input state</span></span>
* <span data-ttu-id="afb6f-189">Nous pourrions utiliser le curseur pour afficher l’état d’entrée ou l’intention de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="afb6f-189">We could use the cursor to display the user's input state or intent.</span></span> <span data-ttu-id="afb6f-190">Par exemple, nous pourrions afficher une icône indiquant à l’utilisateur que le système voit son état main et que l’application sait qu’il est prêt à agir.</span><span class="sxs-lookup"><span data-stu-id="afb6f-190">For example, we could display an icon telling the user the system sees their hand state and that the application knows they are ready to take action.</span></span>
* <span data-ttu-id="afb6f-191">Nous pourrions également utiliser le curseur pour montrer aux utilisateurs que les commandes vocales ont été entendues par le système par le biais d’une couleur momentanée modifiable.</span><span class="sxs-lookup"><span data-stu-id="afb6f-191">We could also use the cursor to show users that voice commands have been heard by the system via a momentary color chang</span></span>

* <span data-ttu-id="afb6f-192">Les États de curseur suivants peuvent être implémentés de différentes façons.</span><span class="sxs-lookup"><span data-stu-id="afb6f-192">The following cursor states can be implemented in different ways.</span></span> <span data-ttu-id="afb6f-193">Vous pouvez implémenter ces différents États en modélisant le curseur comme une machine à États.</span><span class="sxs-lookup"><span data-stu-id="afb6f-193">You might implement these different states by modeling the cursor like a state machine.</span></span> <span data-ttu-id="afb6f-194">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="afb6f-194">For example:</span></span>
    * <span data-ttu-id="afb6f-195">L’état inactif est l’endroit où vous affichez le curseur par défaut.</span><span class="sxs-lookup"><span data-stu-id="afb6f-195">Idle state is where you show the default cursor.</span></span>
    * <span data-ttu-id="afb6f-196">L’état prêt est lorsque vous avez détecté la main de l’utilisateur en position prête.</span><span class="sxs-lookup"><span data-stu-id="afb6f-196">Ready state is when you have detected the user's hand in the ready position.</span></span>
    * <span data-ttu-id="afb6f-197">L’état d’interaction est lorsque l’utilisateur effectue une interaction particulière.</span><span class="sxs-lookup"><span data-stu-id="afb6f-197">Interaction state is when the user is performing a particular interaction.</span></span>
    * <span data-ttu-id="afb6f-198">L’état des actions possibles ou l’état de survol est lorsque vous transmettent des actions possibles qui peuvent être effectuées sur un hologramme.</span><span class="sxs-lookup"><span data-stu-id="afb6f-198">Possible Actions state or hover state is when you convey possible actions that can be performed on a hologram.</span></span>

<span data-ttu-id="afb6f-199">Vous pouvez également implémenter ces États en fonction de l’apparence, de sorte que vous pouvez afficher différentes ressources artistiques lorsque différents États sont détectés.</span><span class="sxs-lookup"><span data-stu-id="afb6f-199">You could also implement these states in a skin-able manner such that you can display different art assets when different states are detected.</span></span>

<br>

---


## <a name="going-cursor-free"></a><span data-ttu-id="afb6f-200">Passage en « sans curseur »</span><span class="sxs-lookup"><span data-stu-id="afb6f-200">Going "cursor-free"</span></span>
<span data-ttu-id="afb6f-201">La conception sans curseur est recommandée lorsque le sens de l’immersion est un composant clé d’une expérience et lorsque les interactions de pointage (via le point de regard et le mouvement) ne nécessitent pas de précision.</span><span class="sxs-lookup"><span data-stu-id="afb6f-201">Designing without a cursor is recommended when the sense of immersion is a key component of an experience and when pointing interactions (through gaze and gesture) do not require great precision.</span></span> <span data-ttu-id="afb6f-202">Le système doit toujours répondre aux besoins normalement atteints par un curseur en fournissant aux utilisateurs des commentaires continus sur la compréhension du système de leur pointage et en aidant les utilisateurs à communiquer en toute confiance leurs intentions au système.</span><span class="sxs-lookup"><span data-stu-id="afb6f-202">The system must still meet the needs that are normally met by a cursor by providing users with continuous feedback on the system's understanding of their pointing and helping them to confidently communicate their intentions to the system.</span></span> <span data-ttu-id="afb6f-203">Cela peut être réalisable par d’autres changements d’État perceptibles.</span><span class="sxs-lookup"><span data-stu-id="afb6f-203">This may be achievable through other noticeable state changes.</span></span>

<br>

---

## <a name="cursor-in-mrtk-mixed-reality-toolkit-for-unity"></a><span data-ttu-id="afb6f-204">Curseur dans MRTK (ensemble d’outils de réalité mixte) pour Unity</span><span class="sxs-lookup"><span data-stu-id="afb6f-204">Cursor in MRTK (Mixed Reality Toolkit) for Unity</span></span>
<span data-ttu-id="afb6f-205">Par défaut, [MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity) fournit un Prefab de curseur ([DefaultCursor. Prefab](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.SDK/Features/UX/Prefabs/Cursors)) qui a le même état visuel que le curseur système de l’interpréteur de commandes.</span><span class="sxs-lookup"><span data-stu-id="afb6f-205">By default, [MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity) provides a cursor prefab([DefaultCursor.prefab](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.SDK/Features/UX/Prefabs/Cursors)) which has the same visual state as the shell's system cursor.</span></span> <span data-ttu-id="afb6f-206">Il est assigné dans le profil d’entrée de MRTK, sous Pointers.</span><span class="sxs-lookup"><span data-stu-id="afb6f-206">It is assigned in MRTK's Input profile, under Pointers.</span></span> <span data-ttu-id="afb6f-207">Vous pouvez remplacer/personnaliser ce curseur pour votre expérience.</span><span class="sxs-lookup"><span data-stu-id="afb6f-207">You can replace/customize this cursor for your experience.</span></span> <span data-ttu-id="afb6f-208">Pour l’expérience avec l’entrée de suivi oculaire, MRTK fournit également EyeGazeCursor qui a un visuel subtil pour réduire la distraction.</span><span class="sxs-lookup"><span data-stu-id="afb6f-208">For the experience with eye-tracking input, MRTK also provides EyeGazeCursor which has subtle visual to minimize the distraction.</span></span>

* [<span data-ttu-id="afb6f-209">MRTK - Profil de pointeur</span><span class="sxs-lookup"><span data-stu-id="afb6f-209">MRTK - Pointer profile</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html#pointer-configuration)
* [<span data-ttu-id="afb6f-210">MRTK - Système d’entrée</span><span class="sxs-lookup"><span data-stu-id="afb6f-210">MRTK - Input system</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html)
* [<span data-ttu-id="afb6f-211">MRTK - Pointeurs</span><span class="sxs-lookup"><span data-stu-id="afb6f-211">MRTK - Pointers</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Pointers.html)


---

## <a name="see-also"></a><span data-ttu-id="afb6f-212">Articles associés</span><span class="sxs-lookup"><span data-stu-id="afb6f-212">See also</span></span>
* [<span data-ttu-id="afb6f-213">Mouvements</span><span class="sxs-lookup"><span data-stu-id="afb6f-213">Gestures</span></span>](gaze-and-commit.md#composite-gestures)
* [<span data-ttu-id="afb6f-214">Pointer du regard vers l’avant et valider</span><span class="sxs-lookup"><span data-stu-id="afb6f-214">Head-gaze and commit</span></span>](gaze-and-commit.md)
