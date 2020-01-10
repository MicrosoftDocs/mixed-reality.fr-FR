---
title: Menu de la main
description: Les menus manuels permettent aux utilisateurs d’afficher rapidement une interface utilisateur attachée à la main pour les fonctions fréquemment utilisées. Voici nos meilleures pratiques et recommandations pour les menus manuels.
author: nbarragan23
ms.author: nobarr
ms.date: 08/27/2019
ms.topic: article
keywords: main, menu, bouton, accès rapide, disposition
ms.openlocfilehash: c0e1800be69a15706e17f40b1601fc79d05e5d75
ms.sourcegitcommit: 6844930427b658ae31f642c395cd8a3b3cdbf857
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75723258"
---
# <a name="hand-menu"></a><span data-ttu-id="ac13d-105">Menu de la main</span><span class="sxs-lookup"><span data-stu-id="ac13d-105">Hand menu</span></span>

![Emplacement de la main ulnar](images/UX/UX_Hero_HandMenu.jpg)

<span data-ttu-id="ac13d-107">Les menus manuels permettent aux utilisateurs d’afficher rapidement une interface utilisateur attachée à la main pour les fonctions fréquemment utilisées.</span><span class="sxs-lookup"><span data-stu-id="ac13d-107">Hand menus allow users to quickly bring up hand-attached UI for frequently used functions.</span></span> 

<span data-ttu-id="ac13d-108">Voici les meilleures pratiques que nous avons trouvées pour les menus manuels.</span><span class="sxs-lookup"><span data-stu-id="ac13d-108">Below are the best practices we have found for hand menus.</span></span> <span data-ttu-id="ac13d-109">Vous trouverez également un exemple de scène illustrant le menu manuel dans [MRTK](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_Solver.md#hand-menu-with-handconstraint-and-handconstraintpalmup).</span><span class="sxs-lookup"><span data-stu-id="ac13d-109">You can also find an example scene demonstrating the hand menu in [MRTK](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_Solver.md#hand-menu-with-handconstraint-and-handconstraintpalmup).</span></span>

<br>

---

## <a name="behavior-best-practices"></a><span data-ttu-id="ac13d-110">Meilleures pratiques relatives au comportement</span><span class="sxs-lookup"><span data-stu-id="ac13d-110">Behavior best practices</span></span>
<span data-ttu-id="ac13d-111">**A. conserver le nombre de boutons petit :** en raison de la distance étroite entre un menu verrouillé et les yeux, et également la tendance de l’utilisateur à se concentrer sur une zone visuelle relativement petite à tout moment (le cône d’acuité visuelle est approximativement de 10 degrés), nous vous recommandons de réduire le nombre de boutons.</span><span class="sxs-lookup"><span data-stu-id="ac13d-111">**A. Keep the number of buttons small:** Due to the close distance between a hand-locked menu and the eyes and also the user's tendency to focus on a relatively small visual area at any time (the attentional cone of vision is roughly 10 degrees), we recommend keeping the number of buttons small.</span></span> <span data-ttu-id="ac13d-112">En fonction de notre exploration, une colonne avec trois boutons fonctionne bien en conservant tout le contenu dans le champ de vision (l’angle de vue) même lorsque les utilisateurs passent leur mains au centre de l’aide.</span><span class="sxs-lookup"><span data-stu-id="ac13d-112">Based on our exploration, one column with three buttons work well by keeping all the content within the field of view (FOV) even when users move their hands to the center of the FOV.</span></span> 

<span data-ttu-id="ac13d-113">**B. utilisation du menu pour une action rapide :** l’élévation d’un bras et la maintenance de la position peuvent facilement entraîner une fatigue du bras.</span><span class="sxs-lookup"><span data-stu-id="ac13d-113">**B. Utilize hand menu for quick action:** Raising an arm and maintaining the position could easily cause arm fatigue.</span></span> <span data-ttu-id="ac13d-114">Utilisez une méthode verrouillée à la main pour le menu nécessitant une faible interaction.</span><span class="sxs-lookup"><span data-stu-id="ac13d-114">Use a hand-locked method for the menu requiring a short interaction.</span></span> <span data-ttu-id="ac13d-115">Si votre menu est complexe et nécessite des temps d’interaction étendus, envisagez d’utiliser à la place un verrou universel ou verrouillé.</span><span class="sxs-lookup"><span data-stu-id="ac13d-115">If your menu is complex and requires extended interaction times, consider using world-locked or body-locked instead.</span></span> 

<span data-ttu-id="ac13d-116">**C. angle du bouton/du panneau :** les menus doivent s’afficher à l’épaule opposé et au milieu de la tête : cela permet à une main naturelle d’interagir avec le menu avec la main opposée et évite les positions difficiles ou inconfortables quand vous touchez des boutons.</span><span class="sxs-lookup"><span data-stu-id="ac13d-116">**C. Button / Panel angle:** Menus should billboard towards the opposite shoulder and middle of the head: This allows a natural hand move to interact with the menu with the opposite hand and avoids any awkward or uncomfortable hand positions when touching buttons.</span></span> 

<span data-ttu-id="ac13d-117">**D. envisagez de prendre en charge une opération unidirectionnelle ou mains libres :** ne partez pas du principe que les deux mains de l’utilisateur sont toujours disponibles.</span><span class="sxs-lookup"><span data-stu-id="ac13d-117">**D. Consider supporting one-handed or hands-free operation:** Do not assume both of the user's hands are always available.</span></span> <span data-ttu-id="ac13d-118">Considérez un large éventail de contextes quand l’un ou l’autre des mains n’est pas disponible, et assurez-vous que votre conception compte pour ces situations.</span><span class="sxs-lookup"><span data-stu-id="ac13d-118">Consider a wide range of contexts when one or both hands are not available, and make sure your design accounts for those situations.</span></span> <span data-ttu-id="ac13d-119">Pour prendre en charge un menu contextuel à un seul mains, vous pouvez essayer de passer le positionnement du menu de façon à ce qu’il passe à l’état verrouillé à l’extérieur lorsque la main est tournée (s’affiche à l’écran).</span><span class="sxs-lookup"><span data-stu-id="ac13d-119">To support a one-handed hand menu, you can try transitioning the menu placement from hand-locked to world-locked when the hand flips (goes palm down).</span></span> <span data-ttu-id="ac13d-120">Pour les scénarios mains libres, envisagez d’utiliser une commande vocale pour appeler les boutons de menu de la main.</span><span class="sxs-lookup"><span data-stu-id="ac13d-120">For hands-free scenarios, consider using a voice command to invoke the hand menu buttons.</span></span>

<span data-ttu-id="ac13d-121">**E. appel en deux étapes :** si vous utilisez simplement Palm-up comme événement pour déclencher le menu de la main, il peut s’afficher accidentellement quand vous n’en avez pas besoin (faux positif), car les gens déplacent leurs mains de manière intentionnelle (pour la communication et la manipulation d’objets) et involontairement.</span><span class="sxs-lookup"><span data-stu-id="ac13d-121">**E. Two-step invocation:** If you use just palm-up as an event to trigger the hand menu, it may accidentally appear when you don't need it (false-positive), because people move their hands a lot both intentionally (for communication and object manipulation) and unintentionally.</span></span> <span data-ttu-id="ac13d-122">Si vous rencontrez des faux positifs dans votre application, envisagez d’ajouter une étape supplémentaire en plus de l’événement Palm-up pour appeler le menu de la main, par exemple les doigts entièrement ouverts.</span><span class="sxs-lookup"><span data-stu-id="ac13d-122">If you experience false-positives in your app, consider adding an additional step besides the palm-up event to invoke the hand menu such as fully opened fingers.</span></span>

<span data-ttu-id="ac13d-123">**F. Évitez d’ajouter des boutons à proximité du poignet (bouton de démarrage du système) :** si les boutons de menu de la main sont placés trop près du bouton d’origine, ils peuvent être déclenchés par inadvertance lors de l’interaction avec le menu de la main.</span><span class="sxs-lookup"><span data-stu-id="ac13d-123">**F. Avoid adding buttons near the wrist (system home button):** If the hand menu buttons are placed too close to the home button, it may get accidentally triggered while interacting with the hand menu.</span></span>

<span data-ttu-id="ac13d-124">**G. test, test, test :** les personnes ont des corps différents, avec des seuils différents pour le confort et la gêne, etc. Veillez à tester votre conception et à obtenir des commentaires d’un grand nombre de personnes.</span><span class="sxs-lookup"><span data-stu-id="ac13d-124">**G. Test, test, test:** People have different bodies, with different thresholds for comfort and discomfort, etc. Be sure to test out your design on and get feedback from a variety of people.</span></span>

<br>

---

## <a name="hand-menu-placement-best-practices"></a><span data-ttu-id="ac13d-125">Meilleures pratiques relatives à l’emplacement des menus manuels</span><span class="sxs-lookup"><span data-stu-id="ac13d-125">Hand menu placement best practices</span></span>

<span data-ttu-id="ac13d-126">Dans l’anatomie humaine, le nerf ulnar est un nerf qui s’exécute près du segment ulna.</span><span class="sxs-lookup"><span data-stu-id="ac13d-126">In human anatomy, the ulnar nerve is a nerve that runs near the ulna bone.</span></span> <span data-ttu-id="ac13d-127">Le ulna est un long segment trouvé dans le bras qui s’étend du coud au doigt le plus petit.</span><span class="sxs-lookup"><span data-stu-id="ac13d-127">The ulna is a long bone found in the forearm that stretches from the elbow to the smallest finger.</span></span>

<span data-ttu-id="ac13d-128">Vous trouverez ci-dessous deux placements recommandés en fonction de nos explorations :</span><span class="sxs-lookup"><span data-stu-id="ac13d-128">Below are 2 recommended placements based on our explorations:</span></span>


:::row:::
    :::column:::
        <span data-ttu-id="ac13d-129">![emplacement ulnar](images/UlnarSideHandMenu.gif)</span><span class="sxs-lookup"><span data-stu-id="ac13d-129">![Ulnar side hand location](images/UlnarSideHandMenu.gif)</span></span><br>
        <span data-ttu-id="ac13d-130">**A. ulnar dans Palm**</span><span class="sxs-lookup"><span data-stu-id="ac13d-130">**A. Ulnar inside palm**</span></span><br>
        <span data-ttu-id="ac13d-131">Cette position est fiable, car les mains ne se chevauchent pas mutuellement.</span><span class="sxs-lookup"><span data-stu-id="ac13d-131">This position is reliable because the hands do not overlap each other.</span></span> <span data-ttu-id="ac13d-132">Cela est essentiel pour une détection et un suivi précis des mains.</span><span class="sxs-lookup"><span data-stu-id="ac13d-132">This is critical for accurate hand detection and tracking.</span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="ac13d-133">![emplacement ulnar](images/UlnarAboveHandMenu.gif)</span><span class="sxs-lookup"><span data-stu-id="ac13d-133">![Ulnar side hand location](images/UlnarAboveHandMenu.gif)</span></span><br>
        <span data-ttu-id="ac13d-134">**B. ulnar au-dessus de la main**</span><span class="sxs-lookup"><span data-stu-id="ac13d-134">**B. Ulnar above hand**</span></span><br>
        <span data-ttu-id="ac13d-135">Cet emplacement est à l’aise pour les utilisateurs, car ils n’ont pas besoin d’augmenter trop le bras pour interagir avec le menu de la main.</span><span class="sxs-lookup"><span data-stu-id="ac13d-135">This location is comfortable for users because they don't need to raise their arm too much to interact with the hand menu.</span></span> <span data-ttu-id="ac13d-136">Nous vous recommandons de placer les menus **13cm** au-dessus de la paume et d’aligner les boutons à l’intérieur de la paume ulnar.</span><span class="sxs-lookup"><span data-stu-id="ac13d-136">We recommend placing menus **13cm** above the palm and align the buttons inside the ulnar palm.</span></span> [<span data-ttu-id="ac13d-137">En savoir plus sur la taille optimale du bouton</span><span class="sxs-lookup"><span data-stu-id="ac13d-137">Read more about the optimal button size</span></span>](interactable-object.md)<br>
        <br>
        <span data-ttu-id="ac13d-138">Pour des raisons techniques, nous recommandons cet emplacement avec une mise en œuvre obligatoire : le développeur doit geler le menu une fois que la main opposée de l’utilisateur est proche de son interaction.</span><span class="sxs-lookup"><span data-stu-id="ac13d-138">For technical reasons we recommend this location with one required implementation: the developer will need to freeze the menu once the user's opposite hand gets close to interacting with it.</span></span> <span data-ttu-id="ac13d-139">Cela évite à jitteriness de se chevaucher les mains et permet également de cibler plus rapidement les boutons.</span><span class="sxs-lookup"><span data-stu-id="ac13d-139">This will avoid jitteriness from overlapping hands and also allows for a faster targeting of the buttons.</span></span><br>
        <br>
        <span data-ttu-id="ac13d-140">Les caméras HoloLens 2 identifient les mains avec précision lorsqu’elles sont séparées les unes des autres.</span><span class="sxs-lookup"><span data-stu-id="ac13d-140">HoloLens 2 cameras identify hands accurately when they are separate from each other.</span></span> <span data-ttu-id="ac13d-141">Les mains qui se chevauchent peuvent entraîner un déplacement des menus manuels hors de l’emplacement d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="ac13d-141">Any overlapping hands can cause hand menus move away from the anchor location.</span></span><br>
    :::column-end:::
:::row-end:::



<br>

---

## <a name="menu-positions-that-are-not-recommended"></a><span data-ttu-id="ac13d-142">Positions de menu non recommandées</span><span class="sxs-lookup"><span data-stu-id="ac13d-142">Menu positions that are not recommended</span></span>
<span data-ttu-id="ac13d-143">Nous avons fait des recherches utilisateur avec différents emplacements et dispositions de menus, les emplacements de menu suivants ne sont **pas recommandés**, recherchez les inconvénients de chaque étude ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ac13d-143">We have done user research with different menus layouts and locations, the following menu locations are **NOT recommended**, find the cons of each study below:</span></span>


:::row:::
    :::column:::
        <span data-ttu-id="ac13d-144">![](images/AboveArm.gif) ARM</span><span class="sxs-lookup"><span data-stu-id="ac13d-144">![Above arm](images/AboveArm.gif)</span></span><br>
        <span data-ttu-id="ac13d-145">**Au-dessus du bras**</span><span class="sxs-lookup"><span data-stu-id="ac13d-145">**Above the arm**</span></span><br>
        <span data-ttu-id="ac13d-146">1-difficulté à entretenir un bon suivi des mains</span><span class="sxs-lookup"><span data-stu-id="ac13d-146">1 - Difficult to maintain good hand tracking</span></span><br>
        <span data-ttu-id="ac13d-147">2-provoque la fatigue de l’utilisateur en raison d’une position non naturelle</span><span class="sxs-lookup"><span data-stu-id="ac13d-147">2 - Causes user fatigue due to unnatural position</span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="ac13d-148">![les doigts ci-dessus](images/AboveFingers.gif)</span><span class="sxs-lookup"><span data-stu-id="ac13d-148">![Above fingers](images/AboveFingers.gif)</span></span><br>
        <span data-ttu-id="ac13d-149">**Les doigts ci-dessus**</span><span class="sxs-lookup"><span data-stu-id="ac13d-149">**Above fingers**</span></span><br>
        <span data-ttu-id="ac13d-150">fatigue de la main en raison de la main à long terme</span><span class="sxs-lookup"><span data-stu-id="ac13d-150">1 - Hand fatigue due to holding hand for long time</span></span><br>
        <span data-ttu-id="ac13d-151">2 problèmes de suivi sur l’index et le doigt central</span><span class="sxs-lookup"><span data-stu-id="ac13d-151">2 - Hand tracking issues on index and middle finger</span></span>
    :::column-end:::
:::row-end:::

<br>

:::row:::
    :::column:::
        <span data-ttu-id="ac13d-152">![au-dessus de la](images/handCenter.gif) Center Palm</span><span class="sxs-lookup"><span data-stu-id="ac13d-152">![Above center palm](images/handCenter.gif)</span></span><br>
        <span data-ttu-id="ac13d-153">**Au-dessus-Centre Palm**</span><span class="sxs-lookup"><span data-stu-id="ac13d-153">**Above-center palm**</span></span><br>
        <span data-ttu-id="ac13d-154">problèmes de suivi de 1 main en raison du chevauchement des mains</span><span class="sxs-lookup"><span data-stu-id="ac13d-154">1 - Hand tracking issues due to overlapping hands</span></span><br>
        <span data-ttu-id="ac13d-155">fatigue à deux mains, en raison de la maintenance de longue durée pour interagir avec les menus</span><span class="sxs-lookup"><span data-stu-id="ac13d-155">2 - Hand fatigue due to holding hands for long time in order to interact with menus</span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="ac13d-156">![**le haut de la main](images/TopFingerTip.gif)\*\*</span><span class="sxs-lookup"><span data-stu-id="ac13d-156">![Top Fingertip](images/TopFingerTip.gif) **Top fingertip**</span></span><br>
        <span data-ttu-id="ac13d-157">1-problèmes de suivi de la main</span><span class="sxs-lookup"><span data-stu-id="ac13d-157">1 - Hand tracking issues</span></span><br>
        <span data-ttu-id="ac13d-158">fatigue à deux mains, en tenant au-dessus de la position normale</span><span class="sxs-lookup"><span data-stu-id="ac13d-158">2 - Hand fatigue holding hand above normal posture</span></span><br>
        <span data-ttu-id="ac13d-159">3-problèmes de pression sur les boutons avec d’autres doigts par accident en raison d’un espace limité entre les doigts</span><span class="sxs-lookup"><span data-stu-id="ac13d-159">3 - Issues pressing buttons with other fingers by accident due to limited space between fingers</span></span>
    :::column-end:::
:::row-end:::

<br>

:::row:::
    :::column:::
        <span data-ttu-id="ac13d-160">![arrière du](images/BackOfTheArm.gif) ARM</span><span class="sxs-lookup"><span data-stu-id="ac13d-160">![Back of the Arm](images/BackOfTheArm.gif)</span></span><br>
        <span data-ttu-id="ac13d-161">**Arrière du bras**</span><span class="sxs-lookup"><span data-stu-id="ac13d-161">**Back of the arm**</span></span><br>
        <span data-ttu-id="ac13d-162">1-peut déclencher le bouton d’origine par accident</span><span class="sxs-lookup"><span data-stu-id="ac13d-162">1 - Can trigger home button by accident</span></span><br>
        <span data-ttu-id="ac13d-163">2-pas de position naturelle ou confortable pour les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ac13d-163">2 - Not a natural or comfortable position for users</span></span>
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

<br>

---

## <a name="hand-menu-in-mrtk-mixed-reality-toolkit-for-unity"></a><span data-ttu-id="ac13d-164">Menu de la main dans MRTK (ensemble d’outils de réalité mixte) pour Unity</span><span class="sxs-lookup"><span data-stu-id="ac13d-164">Hand menu in MRTK (Mixed Reality Toolkit) for Unity</span></span>
<span data-ttu-id="ac13d-165">**[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)** fournit des scripts et des exemples de scènes pour le menu de la main.</span><span class="sxs-lookup"><span data-stu-id="ac13d-165">**[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)** provides scripts and example scenes for the hand menu.</span></span> <span data-ttu-id="ac13d-166">Le script HandConstraintPalmUp Solver vous permet de joindre facilement des objets aux mains avec différentes options configurables.</span><span class="sxs-lookup"><span data-stu-id="ac13d-166">HandConstraintPalmUp solver script allows you easily attach any objects to the hands with various configurable options.</span></span>

* [<span data-ttu-id="ac13d-167">Menu MRTK avec HandConstraint et HandConstraintPalmUp</span><span class="sxs-lookup"><span data-stu-id="ac13d-167">MRTK - Hand Menu with HandConstraint and HandConstraintPalmUp </span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_Solver.md#hand-menu-with-handconstraint-and-handconstraintpalmup)


<br>

---


## <a name="see-also"></a><span data-ttu-id="ac13d-168">Articles associés</span><span class="sxs-lookup"><span data-stu-id="ac13d-168">See also</span></span>

* [<span data-ttu-id="ac13d-169">Curseurs</span><span class="sxs-lookup"><span data-stu-id="ac13d-169">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="ac13d-170">Rayon émanant de la main</span><span class="sxs-lookup"><span data-stu-id="ac13d-170">Hand ray</span></span>](point-and-commit.md)
* [<span data-ttu-id="ac13d-171">Button</span><span class="sxs-lookup"><span data-stu-id="ac13d-171">Button</span></span>](button.md)
* [<span data-ttu-id="ac13d-172">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="ac13d-172">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="ac13d-173">Rectangle englobant et barre de l’application</span><span class="sxs-lookup"><span data-stu-id="ac13d-173">Bounding box and App bar</span></span>](app-bar-and-bounding-box.md)
* [<span data-ttu-id="ac13d-174">Manipulation</span><span class="sxs-lookup"><span data-stu-id="ac13d-174">Manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="ac13d-175">Menu de la main</span><span class="sxs-lookup"><span data-stu-id="ac13d-175">Hand menu</span></span>](hand-menu.md)
* [<span data-ttu-id="ac13d-176">Menu proche</span><span class="sxs-lookup"><span data-stu-id="ac13d-176">Near menu</span></span>](near-menu.md)
* [<span data-ttu-id="ac13d-177">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="ac13d-177">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="ac13d-178">Commande vocale</span><span class="sxs-lookup"><span data-stu-id="ac13d-178">Voice command</span></span>](voice-input.md)
* [<span data-ttu-id="ac13d-179">Clavier</span><span class="sxs-lookup"><span data-stu-id="ac13d-179">Keyboard</span></span>](keyboard.md)
* [<span data-ttu-id="ac13d-180">Info-bulle</span><span class="sxs-lookup"><span data-stu-id="ac13d-180">Tooltip</span></span>](tooltip.md)
* [<span data-ttu-id="ac13d-181">Tablette</span><span class="sxs-lookup"><span data-stu-id="ac13d-181">Slate</span></span>](slate.md)
* [<span data-ttu-id="ac13d-182">Curseur</span><span class="sxs-lookup"><span data-stu-id="ac13d-182">Slider</span></span>](slider.md)
* [<span data-ttu-id="ac13d-183">Nuanceur</span><span class="sxs-lookup"><span data-stu-id="ac13d-183">Shader</span></span>](shader.md)
* [<span data-ttu-id="ac13d-184">Billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="ac13d-184">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
* [<span data-ttu-id="ac13d-185">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="ac13d-185">Displaying progress</span></span>](progress.md)
* [<span data-ttu-id="ac13d-186">Aimantation de surface</span><span class="sxs-lookup"><span data-stu-id="ac13d-186">Surface magnetism</span></span>](surface-magnetism.md)
