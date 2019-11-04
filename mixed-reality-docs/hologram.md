---
title: Qu’est-ce qu’un hologramme ?
description: HoloLens vous permet d’afficher et d’interagir avec des hologrammes à trois dimensions, des objets composés de lumière et de son qui s’affichent dans le monde autour de vous.
author: beaufolsom
ms.author: befolsom
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, HoloLens, hologrammes, conception, interaction
ms.openlocfilehash: 5fb3aff3f59d0999676356d257b72f286a8d7adf
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73435120"
---
# <a name="what-is-a-hologram"></a><span data-ttu-id="79899-104">Qu’est-ce qu’un hologramme ?</span><span class="sxs-lookup"><span data-stu-id="79899-104">What is a hologram?</span></span>

<iframe width="940" height="530" src="https://www.youtube.com/embed/MVXH5V8MVQo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


<span data-ttu-id="79899-105">HoloLens vous permet de créer des **hologrammes**, des objets composés de lumière et de son qui s’affichent partout dans le monde, comme s’il s’agissait d’objets réels.</span><span class="sxs-lookup"><span data-stu-id="79899-105">HoloLens lets you create **holograms**, objects made of light and sound that appear in the world around you, just as if they were real objects.</span></span> <span data-ttu-id="79899-106">Les hologrammes répondent à [vos](gaze-and-commit.md)commandes de pointage, de [mouvement](gaze-and-commit.md#composite-gestures) et de [voix](voice-input.md)et peuvent interagir avec des [surfaces réelles](spatial-mapping.md) autour de vous.</span><span class="sxs-lookup"><span data-stu-id="79899-106">Holograms respond to your [gaze](gaze-and-commit.md), [gestures](gaze-and-commit.md#composite-gestures) and [voice commands](voice-input.md), and can interact with [real-world surfaces](spatial-mapping.md) around you.</span></span> <span data-ttu-id="79899-107">Avec les hologrammes, vous pouvez créer des objets numériques qui font partie de votre monde.</span><span class="sxs-lookup"><span data-stu-id="79899-107">With holograms, you can create digital objects that are part of your world.</span></span>

<br>


## <a name="device-support"></a><span data-ttu-id="79899-108">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="79899-108">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="79899-109"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="79899-109"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="79899-110"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="79899-110"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="79899-111"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="79899-111"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="79899-112"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="79899-112"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="79899-113">Hologrammes</span><span class="sxs-lookup"><span data-stu-id="79899-113">Holograms</span></span></td>
        <td><span data-ttu-id="79899-114">✔️</span><span class="sxs-lookup"><span data-stu-id="79899-114">✔️</span></span></td>
        <td><span data-ttu-id="79899-115">✔️</span><span class="sxs-lookup"><span data-stu-id="79899-115">✔️</span></span></td>
        <td>❌</td>
    </tr>
</table>

<br>

---

## <a name="a-hologram-is-made-of-light-and-sound"></a><span data-ttu-id="79899-116">Un hologramme est composé de lumière et de son</span><span class="sxs-lookup"><span data-stu-id="79899-116">A hologram is made of light and sound</span></span>

<span data-ttu-id="79899-117">Les hologrammes que le [contrôle HoloLens affiche](rendering.md) dans le cadre holographique directement devant les yeux de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79899-117">The holograms that HoloLens [renders](rendering.md) appear in the holographic frame directly in front of the user's eyes.</span></span> <span data-ttu-id="79899-118">Les hologrammes ajoutent de la lumière à votre monde, ce qui signifie que vous voyez la lumière de l’écran et la lumière de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="79899-118">Holograms add light to your world, which means that you see both the light from the display and the light from your surroundings.</span></span> <span data-ttu-id="79899-119">HoloLens ne disposant pas de lumière sur vos yeux, les hologrammes ne peuvent pas être rendus avec la couleur noire.</span><span class="sxs-lookup"><span data-stu-id="79899-119">HoloLens doesn't remove light from your eyes, so holograms can't be rendered with the color black.</span></span> <span data-ttu-id="79899-120">Au lieu de cela, le contenu noir apparaît comme transparent.</span><span class="sxs-lookup"><span data-stu-id="79899-120">Instead, black content appears as transparent.</span></span>

<span data-ttu-id="79899-121">Les hologrammes peuvent avoir de nombreuses apparences et comportements différents.</span><span class="sxs-lookup"><span data-stu-id="79899-121">Holograms can have many different appearances and behaviors.</span></span> <span data-ttu-id="79899-122">Certains sont réalistes et solides, tandis que d’autres sont animés et Ethereal.</span><span class="sxs-lookup"><span data-stu-id="79899-122">Some are realistic and solid, and others are cartoonish and ethereal.</span></span> <span data-ttu-id="79899-123">Les hologrammes peuvent mettre en évidence des fonctionnalités dans votre environnement et peuvent être des éléments de l’interface utilisateur de votre application.</span><span class="sxs-lookup"><span data-stu-id="79899-123">Holograms can highlight features in your surroundings, and they can be elements in your app's user interface.</span></span>

![Mains manipulation d’un hologramme](images/hologram-hands-940px.jpg)

<span data-ttu-id="79899-125">Les hologrammes peuvent également créer des [sons](spatial-sound.md)qui semblent provenir d’un emplacement spécifique dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="79899-125">Holograms can also make [sounds](spatial-sound.md), which will appear to come from a specific place in your surroundings.</span></span> <span data-ttu-id="79899-126">Sur HoloLens, le son provient de deux enceintes situées directement au-dessus de vos oreilles, sans les couvrir.</span><span class="sxs-lookup"><span data-stu-id="79899-126">On HoloLens, sound comes from two speakers that are located directly above your ears, without covering them.</span></span> <span data-ttu-id="79899-127">Comme pour les écrans, les haut-parleurs sont additifs, ce qui introduit de nouveaux sons sans bloquer les sons de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="79899-127">Similar to the displays, the speakers are additive, introducing new sounds without blocking the sounds from your environment.</span></span>

<br>

---

## <a name="a-hologram-can-be-placed-in-the-world-or-tag-along-with-you"></a><span data-ttu-id="79899-128">Un hologramme peut être placé dans le monde entier ou dans la balise avec vous</span><span class="sxs-lookup"><span data-stu-id="79899-128">A hologram can be placed in the world or tag along with you</span></span>

<span data-ttu-id="79899-129">Si vous avez un emplacement particulier où vous souhaitez un hologramme, vous pouvez le [Placer](coordinate-systems.md) précisément dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="79899-129">When you have a particular location where you want a hologram, you can [place](coordinate-systems.md) it precisely there in the world.</span></span> <span data-ttu-id="79899-130">Au fur et à mesure que vous parcourez Cet hologramme, il apparaîtra stable par rapport au monde entier.</span><span class="sxs-lookup"><span data-stu-id="79899-130">As you walk around that hologram, it will appear stable relative to the world around you.</span></span> <span data-ttu-id="79899-131">Si vous utilisez une [ancre spatiale](coordinate-systems.md#spatial-anchors) pour épingler cet objet fermement au monde, le système peut même se souvenir de l’endroit où vous l’avez laissé lorsque vous revenez plus tard.</span><span class="sxs-lookup"><span data-stu-id="79899-131">If you use a [spatial anchor](coordinate-systems.md#spatial-anchors) to pin that object firmly to the world, the system can even remember where you left it when you come back later.</span></span>

![Deux hommes utilisant la disposition Microsoft Dynamics 365 dans un espace de vente au détail](images/HLS19_retailLayoutHologram_001-940px.jpg)

<span data-ttu-id="79899-133">Certains hologrammes suivent l’utilisateur à la place.</span><span class="sxs-lookup"><span data-stu-id="79899-133">Some holograms follow the user instead.</span></span> <span data-ttu-id="79899-134">Ces hologrammes se déplacent eux-mêmes par rapport à l’utilisateur, quel que soit l’endroit où ils parcourent.</span><span class="sxs-lookup"><span data-stu-id="79899-134">These tag-along holograms position themselves relative to the user, no matter where they walk.</span></span> <span data-ttu-id="79899-135">Vous pouvez même choisir de placer un hologramme avec vous pendant un certain temps, puis le placer sur le mur une fois que vous êtes dans une autre pièce.</span><span class="sxs-lookup"><span data-stu-id="79899-135">You may even choose to bring a hologram with you for a while and then place it on the wall once you get to another room.</span></span>

<span data-ttu-id="79899-136">**Bonnes pratiques**</span><span class="sxs-lookup"><span data-stu-id="79899-136">**Best practices**</span></span>
* <span data-ttu-id="79899-137">Certains scénarios peuvent exiger que les hologrammes restent facilement détectables ou visibles tout au long de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="79899-137">Some scenarios may demand that holograms remain easily discoverable or visible throughout the experience.</span></span> <span data-ttu-id="79899-138">Il existe deux approches de haut niveau pour ce type de positionnement.</span><span class="sxs-lookup"><span data-stu-id="79899-138">There are two high-level approaches to this kind of positioning.</span></span> <span data-ttu-id="79899-139">Appelons-les **« éléments verrouillés** » et **« verrouillés en corps »** .</span><span class="sxs-lookup"><span data-stu-id="79899-139">Let's call them **"display-locked"** and **"body-locked"**.</span></span>
   * <span data-ttu-id="79899-140">Le contenu verrouillé en affichage est positionné de façon « verrouillée » sur l’écran de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="79899-140">Display-locked content is positionally "locked" to the device display.</span></span> <span data-ttu-id="79899-141">Cela est délicat pour plusieurs raisons, notamment un sentiment de « clingyness » innaturel qui rend beaucoup d’utilisateurs frustrés et souhaitant les « secouer ».</span><span class="sxs-lookup"><span data-stu-id="79899-141">This is tricky for a number of reasons, including an unnatural feeling of "clingyness" that makes many users frustrated and wanting to "shake it off."</span></span> <span data-ttu-id="79899-142">En général, de nombreux concepteurs ont trouvé mieux qu’ils évitent le verrouillage du contenu.</span><span class="sxs-lookup"><span data-stu-id="79899-142">In general, many designers have found it better to avoid display-locking content.</span></span>
   * <span data-ttu-id="79899-143">L’approche verrouillée par le corps est beaucoup plus forgivable.</span><span class="sxs-lookup"><span data-stu-id="79899-143">The body-locked approach is far more forgivable.</span></span> <span data-ttu-id="79899-144">Le verrouillage du corps est lorsqu’un hologramme est attaché au corps ou au vecteur de pointage de l’utilisateur, mais est positionné dans l’espace 3D autour de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79899-144">Body-locking is when a hologram is tethered to the user's body or gaze vector, but is positioned in 3d space around the user.</span></span> <span data-ttu-id="79899-145">De nombreuses expériences ont adopté un comportement de verrouillage du corps où l’hologramme « suit » les utilisateurs pointant vers le regard, ce qui permet à l’utilisateur de faire pivoter son corps et de parcourir l’espace sans perdre l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="79899-145">Many experiences have adopted a body-locking behavior where the hologram "follows" the users gaze, which allows the user to rotate their body and move through space without losing the hologram.</span></span> <span data-ttu-id="79899-146">L’incorporation d’un délai permet d’obtenir un mouvement d’hologramme plus naturel.</span><span class="sxs-lookup"><span data-stu-id="79899-146">Incorporating a delay helps the hologram movement feel more natural.</span></span> <span data-ttu-id="79899-147">Par exemple, une interface utilisateur principale du système d’exploitation Windows holographique utilise une variation sur le verrouillage du corps qui suit le point d’arrêt de l’utilisateur avec un délai léger et élastique, tandis que l’utilisateur change de tête.</span><span class="sxs-lookup"><span data-stu-id="79899-147">For example, some core UI of the Windows Holographic OS uses a variation on body-locking that follows the user's gaze with a gentle, elastic-like delay while the user turns their head.</span></span>
* <span data-ttu-id="79899-148">Placez l’hologramme à une distance confortable, généralement d’environ 1-2 mètres de l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="79899-148">Place the hologram at a comfortable viewing distance typically about 1-2 meters away from the head.</span></span>
* <span data-ttu-id="79899-149">Fournissez une quantité de dérive pour les éléments qui doivent être continuellement dans le frame holographique ou envisagez d’animer votre contenu sur un côté de l’affichage lorsque l’utilisateur modifie son point de vue.</span><span class="sxs-lookup"><span data-stu-id="79899-149">Provide an amount of drift for elements that must be continually in the holographic frame, or consider animating your content to one side of the display when the user changes their point of view.</span></span>

<span data-ttu-id="79899-150">**Placer des hologrammes dans la zone optimale, entre 1,25 m et 5 m**</span><span class="sxs-lookup"><span data-stu-id="79899-150">**Place holograms in the optimal zone - between 1.25m and 5m**</span></span>

<span data-ttu-id="79899-151">Deux compteurs sont les plus optimaux, et l’expérience dégradera la plus proche d’un compteur.</span><span class="sxs-lookup"><span data-stu-id="79899-151">Two meters is the most optimal, and the experience will degrade the closer you get from one meter.</span></span> <span data-ttu-id="79899-152">À des distances près d’un mètre, les hologrammes qui se déplacent régulièrement sont plus susceptibles d’être problématiques que les hologrammes fixes.</span><span class="sxs-lookup"><span data-stu-id="79899-152">At distances nearer than one meter, holograms that regularly move in depth are more likely to be problematic than stationary holograms.</span></span> <span data-ttu-id="79899-153">Envisagez de découper ou de détourer votre contenu en douceur quand il est trop proche, ce qui ne permet pas à l’utilisateur d’être confronté à une expérience inattendue.</span><span class="sxs-lookup"><span data-stu-id="79899-153">Consider gracefully clipping or fading out your content when it gets too close so as not to jar the user into an unexpected experience.</span></span>

![Distance optimale pour le placement des hologrammes de l’utilisateur.](images/distanceguiderendering-950px.png)

<br>

---


## <a name="a-hologram-interacts-with-you-and-your-world"></a><span data-ttu-id="79899-155">Un hologramme interagit avec vous et votre monde</span><span class="sxs-lookup"><span data-stu-id="79899-155">A hologram interacts with you and your world</span></span>

<span data-ttu-id="79899-156">Les hologrammes ne sont pas uniquement à l’égard du clair et du son. ils sont également une partie active de votre monde.</span><span class="sxs-lookup"><span data-stu-id="79899-156">Holograms aren't only about light and sound; they're also an active part of your world.</span></span> <span data-ttu-id="79899-157">Pointez le regard sur un hologramme et un geste avec votre main, et un hologramme peut commencer à vous suivre.</span><span class="sxs-lookup"><span data-stu-id="79899-157">Gaze at a hologram and gesture with your hand, and a hologram can start to follow you.</span></span> <span data-ttu-id="79899-158">Donnez une commande vocale à un hologramme, qui peut répondre.</span><span class="sxs-lookup"><span data-stu-id="79899-158">Give a voice command to a hologram, and it can reply.</span></span>

![Groupe de travailleurs utilitaires gouvernementaux utilisant Microsoft HoloLens 2 pour collaborer sur un projet de développement de batterie de serveurs vent](images/HLS19_governmentUtilitiesHologram_001-940px.jpg)

<span data-ttu-id="79899-160">Les hologrammes permettent des interactions personnelles qui ne sont pas possibles ailleurs.</span><span class="sxs-lookup"><span data-stu-id="79899-160">Holograms enable personal interactions that aren't possible elsewhere.</span></span> <span data-ttu-id="79899-161">Étant donné que le HoloLens sait où il se trouve dans le monde, un caractère holographique peut vous paraître directement dans les yeux à mesure que vous parcourez la salle.</span><span class="sxs-lookup"><span data-stu-id="79899-161">Because the HoloLens knows where it is in the world, a holographic character can look you directly in the eyes as you walk around the room.</span></span>

<span data-ttu-id="79899-162">Un hologramme peut également interagir avec votre environnement.</span><span class="sxs-lookup"><span data-stu-id="79899-162">A hologram can also interact with your surroundings.</span></span> <span data-ttu-id="79899-163">Par exemple, vous pouvez placer une boule de rebond holographique au-dessus d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="79899-163">For example, you can place a holographic bouncing ball above a table.</span></span> <span data-ttu-id="79899-164">Ensuite, à l’aide d’un [robinet](gaze-and-commit.md#composite-gestures), regardez la balle rebondir et émettez un son lorsqu’il atteint le tableau.</span><span class="sxs-lookup"><span data-stu-id="79899-164">Then, with an [air tap](gaze-and-commit.md#composite-gestures), watch the ball bounce and make sound when it hits the table.</span></span>

<span data-ttu-id="79899-165">Les hologrammes peuvent également être bloqués par des objets réels.</span><span class="sxs-lookup"><span data-stu-id="79899-165">Holograms can also be occluded by real-world objects.</span></span> <span data-ttu-id="79899-166">Par exemple, un caractère holographique peut parcourir une porte et derrière un mur, en dehors de votre vue.</span><span class="sxs-lookup"><span data-stu-id="79899-166">For example, a holographic character might walk through a door and behind a wall, out of your sight.</span></span>

<span data-ttu-id="79899-167">**Conseils pour l’intégration des hologrammes et du monde réel**</span><span class="sxs-lookup"><span data-stu-id="79899-167">**Tips for integrating holograms and the real world**</span></span>
* <span data-ttu-id="79899-168">L’alignement sur les règles gravitationnelles facilite la liaison des hologrammes à et plus crédible.</span><span class="sxs-lookup"><span data-stu-id="79899-168">Aligning to gravitational rules makes holograms easier to relate to and more believable.</span></span> <span data-ttu-id="79899-169">par exemple : Placez un chien holographique sur le sol & un vase sur la table au lieu de le faire flotter dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="79899-169">eg: Place a holographic dog on the ground & a vase on the table rather than have them floating in space.</span></span>
* <span data-ttu-id="79899-170">De nombreux concepteurs ont constaté qu’ils peuvent encore plus incroyablement intégrer des hologrammes en créant une « ombre négative » sur la surface sur laquelle l’hologramme est assis.</span><span class="sxs-lookup"><span data-stu-id="79899-170">Many designers have found that they can even more believably integrate holograms by creating a "negative shadow" on the surface that the hologram is sitting on.</span></span> <span data-ttu-id="79899-171">Pour ce faire, ils créent une lueur douce sur le sol autour de l’hologramme, puis soustraient la « ombre » de la lueur.</span><span class="sxs-lookup"><span data-stu-id="79899-171">They do this by creating a soft glow on the ground around the hologram and then subtracting the "shadow" from the glow.</span></span> <span data-ttu-id="79899-172">La lueur douce s’intègre à la lumière du monde réel et l’ombre aux raisons de l’hologramme dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="79899-172">The soft glow integrates with the light from the real world and the shadow grounds the hologram in the environment.</span></span>

<br>

---

:::row:::
    :::column:::
        ## <a name="a-hologram-is-whatever-bryou-can-dream-upbr"></a><span data-ttu-id="79899-173">Un hologramme est tout ce que</span><span class="sxs-lookup"><span data-stu-id="79899-173">A hologram is whatever</span></span> <br><span data-ttu-id="79899-174">vous pouvez rêver</span><span class="sxs-lookup"><span data-stu-id="79899-174">you can dream up</span></span><br>
        <span data-ttu-id="79899-175">En tant que développeur holographique, vous avez la possibilité de scinder votre créativité en écrans 2D et dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="79899-175">As a holographic developer, you have the power to break your creativity out of 2D screens and into the world around you.</span></span><br><br>
        <span data-ttu-id="79899-176">Que allez- *vous* générer ?</span><span class="sxs-lookup"><span data-stu-id="79899-176">What will *you* build?</span></span>
    :::column-end:::
        :::column:::
        <span data-ttu-id="79899-177">espace de ![](images/spacer-20x582.png)</span><span class="sxs-lookup"><span data-stu-id="79899-177">![space](images/spacer-20x582.png)</span></span><br>
       <span data-ttu-id="79899-178">![un monde imaginaire imaginaire dans le salon](images/designoverview.jpg)</span><span class="sxs-lookup"><span data-stu-id="79899-178">![Holographic imaginary world in living room](images/designoverview.jpg)</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="see-also"></a><span data-ttu-id="79899-179">Articles associés</span><span class="sxs-lookup"><span data-stu-id="79899-179">See also</span></span>
* [<span data-ttu-id="79899-180">Développez votre processus de conception</span><span class="sxs-lookup"><span data-stu-id="79899-180">Expand your design process</span></span>](case-study-expanding-the-design-process-for-mixed-reality.md)
* [<span data-ttu-id="79899-181">Son spatial</span><span class="sxs-lookup"><span data-stu-id="79899-181">Spatial sound</span></span>](spatial-sound.md)
* [<span data-ttu-id="79899-182">Couleurs, éclairage et matériaux</span><span class="sxs-lookup"><span data-stu-id="79899-182">Color, light and materials</span></span>](color,-light-and-materials.md)
