---
title: Menu de la main
description: Les menus manuels permettent aux utilisateurs d’afficher rapidement une interface utilisateur attachée à la main pour les fonctions fréquemment utilisées. Voici nos meilleures pratiques et recommandations pour les menus manuels.
author: nbarragan23
ms.author: nobarr
ms.date: 08/27/2019
ms.topic: article
keywords: main, menu, bouton, accès rapide, disposition
ms.openlocfilehash: d1d15b36bab2ca2082ca4ba91b9c64862893f80c
ms.sourcegitcommit: fef42e2908e49822f2d13b05d2f9260bf0d72158
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86061165"
---
# <a name="hand-menu"></a><span data-ttu-id="0ff8b-105">Menu de la main</span><span class="sxs-lookup"><span data-stu-id="0ff8b-105">Hand menu</span></span>

![Emplacement de la main ulnar](images/UX/UX_Hero_HandMenu.jpg)

<span data-ttu-id="0ff8b-107">Le menu de la main est l’un des modèles d’expérience utilisateur les plus uniques dans HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-107">The hand menu is one of the most unique UX patterns in HoloLens 2.</span></span> <span data-ttu-id="0ff8b-108">Elle vous permet d’accéder rapidement à une interface utilisateur jointe à la main.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-108">It allows you to quickly bring up hand-attached UI.</span></span> <span data-ttu-id="0ff8b-109">Étant donné qu’il est accessible à tout moment et peut être affiché et masqué facilement, c’est parfait pour les actions rapides.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-109">Since it's accessible anytime and can be shown and hidden easily, it's great for quick actions.</span></span>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4AJAg]

<span data-ttu-id="0ff8b-110">Vous trouverez nos meilleures pratiques recommandées pour l’utilisation des menus manuels dans la liste ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-110">You'll find our recommended best practices for working with hand menus in the list below.</span></span> <span data-ttu-id="0ff8b-111">Vous trouverez également un exemple de scène illustrant le menu manuel dans [MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_HandMenu.html).</span><span class="sxs-lookup"><span data-stu-id="0ff8b-111">You can also find an example scene demonstrating the hand menu in [MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_HandMenu.html).</span></span>

<br>


---

## <a name="best-practices"></a><span data-ttu-id="0ff8b-112">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="0ff8b-112">Best practices</span></span>
<span data-ttu-id="0ff8b-113">**Conserver le nombre de boutons petit**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-113">**Keep the number of buttons small**</span></span> 

<span data-ttu-id="0ff8b-114">En raison de la distance étroite entre un menu verrouillé et les yeux, ainsi que la tendance de l’utilisateur à se concentrer sur une zone visuelle relativement petite à tout moment (le cône de vision est à peu près 10 degrés), nous vous recommandons de laisser le nombre de boutons petit.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-114">Due to the close distance between a hand-locked menu and the eyes and also the user's tendency to focus on a relatively small visual area at any time (the attentional cone of vision is roughly 10 degrees), we recommend keeping the number of buttons small.</span></span> <span data-ttu-id="0ff8b-115">Sur la base de notre exploration, une colonne avec trois boutons fonctionne bien en conservant tout le contenu dans le champ de vision (l’angle d’accès) même lorsqu’un utilisateur passe au centre de l’angle d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-115">Based on our exploration, one column with three buttons works well by keeping all the content within the field of view (FOV) even when a user moves their hands to the center of the FOV.</span></span> 

<span data-ttu-id="0ff8b-116">**Utiliser le menu manuellement pour une action rapide**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-116">**Utilize hand menu for quick action**</span></span> 

<span data-ttu-id="0ff8b-117">L’élévation d’un bras et la maintenance de la position peuvent facilement entraîner une fatigue du bras.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-117">Raising an arm and maintaining the position could easily cause arm fatigue.</span></span> <span data-ttu-id="0ff8b-118">Utilisez une méthode verrouillée à la main pour le menu nécessitant une faible interaction.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-118">Use a hand-locked method for the menu requiring a short interaction.</span></span> <span data-ttu-id="0ff8b-119">Si votre menu est complexe et nécessite des temps d’interaction étendus, envisagez d’utiliser à la place un verrou universel ou verrouillé.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-119">If your menu is complex and requires extended interaction times, consider using world-locked or body-locked instead.</span></span> 

<span data-ttu-id="0ff8b-120">**Angle du bouton/du panneau**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-120">**Button / Panel angle**</span></span>

<span data-ttu-id="0ff8b-121">Les menus doivent s’afficher à l’épaule opposé et au milieu de la tête : cela permet à une main naturelle d’interagir avec le menu avec la main opposée et évite les positions difficiles ou inconfortables quand vous touchez des boutons.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-121">Menus should billboard towards the opposite shoulder and middle of the head: This allows a natural hand move to interact with the menu with the opposite hand and avoids any awkward or uncomfortable hand positions when touching buttons.</span></span> 

<span data-ttu-id="0ff8b-122">**Envisagez de prendre en charge une opération à la main ou mains libres**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-122">**Consider supporting one-handed or hands-free operation**</span></span>

<span data-ttu-id="0ff8b-123">Ne partez pas du principe que les deux mains de l’utilisateur sont toujours disponibles.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-123">Do not assume both of the user's hands are always available.</span></span> <span data-ttu-id="0ff8b-124">Considérez un large éventail de contextes quand l’un ou l’autre des mains n’est pas disponible, et assurez-vous que votre conception compte pour ces situations.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-124">Consider a wide range of contexts when one or both hands are not available, and make sure your design accounts for those situations.</span></span> <span data-ttu-id="0ff8b-125">Pour prendre en charge un menu contextuel à un seul mains, vous pouvez essayer de passer le positionnement du menu de façon à ce qu’il passe à l’état verrouillé à l’extérieur lorsque la main est tournée (s’affiche à l’écran).</span><span class="sxs-lookup"><span data-stu-id="0ff8b-125">To support a one-handed hand menu, you can try transitioning the menu placement from hand-locked to world-locked when the hand flips (goes palm down).</span></span> <span data-ttu-id="0ff8b-126">Pour les scénarios mains libres, envisagez d’utiliser une commande vocale pour appeler le menu de la main.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-126">For hands-free scenarios, consider using a voice command to invoke the hand menu.</span></span>

<span data-ttu-id="0ff8b-127">**Évitez d’ajouter des boutons près du poignet (bouton de démarrage du système)**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-127">**Avoid adding buttons near the wrist (system home button)**</span></span>

<span data-ttu-id="0ff8b-128">Si les boutons de menu de la main sont placés trop près du bouton d’origine, ils peuvent se déclencher accidentellement lors de l’interaction avec le menu de la main.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-128">If the hand menu buttons are placed too close to the home button, it may accidentally trigger while interacting with the hand menu.</span></span>

<br>

## <a name="hand-menu-with-large-and-complex-ui-controls"></a><span data-ttu-id="0ff8b-129">Menu manuel avec des contrôles d’interface utilisateur volumineux et complexes</span><span class="sxs-lookup"><span data-stu-id="0ff8b-129">Hand menu with large and complex UI controls</span></span>
<img src="images/UX/HandMenu_SizeExample.png" alt="HoloLens perspective of a menu system that always faces the user" width="940px">
<span data-ttu-id="0ff8b-130">Il est recommandé de limiter le nombre de boutons ou de contrôles d’interface utilisateur dans les menus attachés à la main.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-130">It's recommended to limit the number of buttons or UI controls on hand-attached menus.</span></span> <span data-ttu-id="0ff8b-131">Cela est dû au fait que l’interaction étendue avec un grand nombre d’éléments d’interface utilisateur peut entraîner une fatigue ARM.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-131">This is because extended interaction with a large number of UI elements can cause arm fatigue.</span></span> <span data-ttu-id="0ff8b-132">Si votre expérience requiert un grand menu, fournissez un moyen facile pour l’utilisateur de verrouiller le menu.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-132">If your experience requires a large menu, provide an easy way for the user to world lock the menu.</span></span> <span data-ttu-id="0ff8b-133">L’une des techniques recommandées est l’utilisation de l’option de verrouillage universel lorsque la main chute ou s’éloigne de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-133">One technique we recommend is to world-lock then menu when the hand drops or flips away from the user.</span></span> <span data-ttu-id="0ff8b-134">Une seconde technique consiste à autoriser l’utilisateur à saisir directement le menu en revanche.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-134">A second technique is to allow the user to directly grab the menu with the other hand.</span></span> <span data-ttu-id="0ff8b-135">Quand l’utilisateur relâche le menu, le menu doit être un verrou universel.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-135">When the user releases the menu, the menu should world lock.</span></span> <span data-ttu-id="0ff8b-136">De cette façon, un utilisateur peut interagir avec les différents éléments de l’interface utilisateur de manière conviviale et en toute confiance sur une période prolongée.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-136">This way, a user can interact with various UI elements comfortably and confidently over an extended period of time.</span></span> 

<span data-ttu-id="0ff8b-137">Lorsque le menu est verrouillé dans le monde entier, veillez à fournir un moyen de déplacer le menu, puis fermez le menu lorsqu’il n’est plus nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-137">When the menu is world-locked, make sure to provide a way to move the menu, and close the menu when it's no longer needed.</span></span> <span data-ttu-id="0ff8b-138">Rendez le menu déplaçable en fournissant des poignées sur les côtés ou en haut du menu.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-138">Make the menu movable by providing handles on the sides or top of menu.</span></span> <span data-ttu-id="0ff8b-139">Ajoutez un bouton Fermer pour permettre au menu de se fermer.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-139">Add a close button to allow the menu to close.</span></span> <span data-ttu-id="0ff8b-140">Autoriser le menu à se rattacher à la main lorsque l’utilisateur est confronté à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-140">Allow for the menu to re-attach to the hand when the user hand faces the user.</span></span> <span data-ttu-id="0ff8b-141">Nous vous recommandons également de demander à ce que les utilisateurs pointent à la main pour empêcher les fausses activations (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="0ff8b-141">We also recommend requiring that the users gazes at their hand to prevent false activations (see below).</span></span>

<span data-ttu-id="0ff8b-142">**Grand menu présentant un problème d’utilisation**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-142">**Large menu that shows a usability issue**</span></span>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4AOPx]

<span data-ttu-id="0ff8b-143">**Menu déroulant à la main**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-143">**World-locked menu on hand drop**</span></span>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4AGZi]

<span data-ttu-id="0ff8b-144">**Récupération manuelle & de l’extraction dans le monde entier-verrouiller le menu**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-144">**Manual grab & pull to world-lock the menu**</span></span>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4AJAf]


## <a name="how-to-prevent-false-activation"></a><span data-ttu-id="0ff8b-145">Comment empêcher une fausse activation</span><span class="sxs-lookup"><span data-stu-id="0ff8b-145">How to prevent false activation</span></span>

<span data-ttu-id="0ff8b-146">Si vous utilisez simplement Palm-up comme événement pour déclencher le menu de la main, il peut s’afficher accidentellement quand vous n’en avez pas besoin (faux positif), car les gens déplacent leurs mains intentionnellement (pour la communication et la manipulation d’objets) et involontairement.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-146">If you use just palm-up as an event to trigger the hand menu, it may accidentally appear when you don't need it (false-positive), because people move their hands both intentionally (for communication and object manipulation) and unintentionally.</span></span> <span data-ttu-id="0ff8b-147">Pour réduire les fausses activations, ajoutez une étape supplémentaire en plus de l’événement Palm-up pour appeler le menu de la main (par exemple, des doigts entièrement ouverts ou l’utilisateur intentionnellement Gazing à la main).</span><span class="sxs-lookup"><span data-stu-id="0ff8b-147">To reduce false activations, add an additional step besides the palm-up event to invoke the hand menu (such as fully opened fingers, or the user intentionally gazing at their hand).</span></span>

<span data-ttu-id="0ff8b-148">**Exiger un Palm plat**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-148">**Require Flat Palm**</span></span>

<span data-ttu-id="0ff8b-149">En exigeant une main ouverte, vous pouvez empêcher une fausse activation qui peut se produire lorsque l’utilisateur manipule des objets ou des gestes tout en communiquant au sein d’un environnement.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-149">By requiring a flat open hand, you can prevent false activation that might occur as the user manipulates objects or gestures while communicating within an environment.</span></span> 

<span data-ttu-id="0ff8b-150">**Exiger le point de regard**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-150">**Require Gaze**</span></span>

<span data-ttu-id="0ff8b-151">En demandant à l’utilisateur de pointer à sa main (avec un regard ou un point de présence oculaire), il empêche les fausses activations, car l’utilisateur doit intentionnellement attirer son attention sur la main en tant qu’étape d’activation secondaire (avec un seuil de distance réglable utilisé pour permettre le confort de l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="0ff8b-151">By requiring the user to gaze at their hand (either with eye gaze or head gaze), it prevents false activations due to the user having to intentionally direct their attention to the hand as a secondary activation step (with a tunable distance threshold used to allow for user comfort).</span></span>  

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4Asn4]

---

## <a name="hand-menu-placement-best-practices"></a><span data-ttu-id="0ff8b-152">Meilleures pratiques relatives à l’emplacement des menus manuels</span><span class="sxs-lookup"><span data-stu-id="0ff8b-152">Hand menu placement best practices</span></span>

<span data-ttu-id="0ff8b-153">Dans l’anatomie humaine, le nerf ulnar est un nerf qui s’exécute près du segment ulna.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-153">In human anatomy, the ulnar nerve is a nerve that runs near the ulna bone.</span></span> <span data-ttu-id="0ff8b-154">Le ulna est un long segment trouvé dans le bras qui s’étend du coud au doigt le plus petit.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-154">The ulna is a long bone found in the forearm that stretches from the elbow to the smallest finger.</span></span>

<span data-ttu-id="0ff8b-155">Vous trouverez ci-dessous deux placements recommandés en fonction de nos explorations :</span><span class="sxs-lookup"><span data-stu-id="0ff8b-155">Below are 2 recommended placements based on our explorations:</span></span>


:::row:::
    :::column:::
        <span data-ttu-id="0ff8b-156">![Emplacement de la main ulnar](images/UlnarSideHandMenu.gif)</span><span class="sxs-lookup"><span data-stu-id="0ff8b-156">![Ulnar side hand location](images/UlnarSideHandMenu.gif)</span></span><br>
        <span data-ttu-id="0ff8b-157">**A. ulnar dans Palm**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-157">**A. Ulnar inside palm**</span></span><br>
        <span data-ttu-id="0ff8b-158">Cette position est fiable, car les mains ne se chevauchent pas mutuellement.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-158">This position is reliable because the hands do not overlap each other.</span></span> <span data-ttu-id="0ff8b-159">Cela est essentiel pour une détection et un suivi précis des mains.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-159">This is critical for accurate hand detection and tracking.</span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="0ff8b-160">![Emplacement de la main ulnar](images/UlnarAboveHandMenu.gif)</span><span class="sxs-lookup"><span data-stu-id="0ff8b-160">![Ulnar side hand location](images/UlnarAboveHandMenu.gif)</span></span><br>
        <span data-ttu-id="0ff8b-161">**B. ulnar au-dessus de la main**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-161">**B. Ulnar above hand**</span></span><br>
        <span data-ttu-id="0ff8b-162">Cet emplacement est à l’aise pour les utilisateurs, car ils n’ont pas besoin d’augmenter trop le bras pour interagir avec le menu de la main.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-162">This location is comfortable for users because they don't need to raise their arm too much to interact with the hand menu.</span></span> <span data-ttu-id="0ff8b-163">Nous vous recommandons de placer les menus **13cm** au-dessus de la paume et d’aligner les boutons à l’intérieur de la paume ulnar.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-163">We recommend placing menus **13cm** above the palm and align the buttons inside the ulnar palm.</span></span> [<span data-ttu-id="0ff8b-164">En savoir plus sur la taille optimale du bouton</span><span class="sxs-lookup"><span data-stu-id="0ff8b-164">Read more about the optimal button size</span></span>](interactable-object.md)<br>
        <br>
        <span data-ttu-id="0ff8b-165">Pour des raisons techniques, nous recommandons cet emplacement avec une mise en œuvre obligatoire : le développeur doit geler le menu une fois que la main opposée de l’utilisateur est proche de son interaction.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-165">For technical reasons we recommend this location with one required implementation: the developer will need to freeze the menu once the user's opposite hand gets close to interacting with it.</span></span> <span data-ttu-id="0ff8b-166">Cela évite à jitteriness de se chevaucher les mains et permet également de cibler plus rapidement les boutons.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-166">This will avoid jitteriness from overlapping hands and also allows for a faster targeting of the buttons.</span></span><br>
        <br>
        <span data-ttu-id="0ff8b-167">Les caméras HoloLens 2 identifient les mains avec précision lorsqu’elles sont séparées les unes des autres.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-167">HoloLens 2 cameras identify hands accurately when they are separate from each other.</span></span> <span data-ttu-id="0ff8b-168">Les mains qui se chevauchent peuvent entraîner un déplacement des menus manuels hors de l’emplacement d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-168">Any overlapping hands can cause hand menus move away from the anchor location.</span></span><br>
    :::column-end:::
:::row-end:::



<br>

---

## <a name="menu-positions-that-are-not-recommended"></a><span data-ttu-id="0ff8b-169">Positions de menu non recommandées</span><span class="sxs-lookup"><span data-stu-id="0ff8b-169">Menu positions that are not recommended</span></span>
<span data-ttu-id="0ff8b-170">Nous avons fait des recherches utilisateur avec différents emplacements et dispositions de menus, les emplacements de menu suivants ne sont **pas recommandés**, recherchez les inconvénients de chaque étude ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0ff8b-170">We have done user research with different menus layouts and locations, the following menu locations are **NOT recommended**, find the cons of each study below:</span></span>


:::row:::
    :::column:::
        <span data-ttu-id="0ff8b-171">![Au-dessus du bras](images/AboveArm.gif)</span><span class="sxs-lookup"><span data-stu-id="0ff8b-171">![Above arm](images/AboveArm.gif)</span></span><br>
        <span data-ttu-id="0ff8b-172">**Au-dessus du bras**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-172">**Above the arm**</span></span><br>
        <span data-ttu-id="0ff8b-173">1-difficulté à entretenir un bon suivi des mains</span><span class="sxs-lookup"><span data-stu-id="0ff8b-173">1 - Difficult to maintain good hand tracking</span></span><br>
        <span data-ttu-id="0ff8b-174">2-provoque la fatigue de l’utilisateur en raison d’une position non naturelle</span><span class="sxs-lookup"><span data-stu-id="0ff8b-174">2 - Causes user fatigue due to unnatural position</span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="0ff8b-175">![Les doigts ci-dessus](images/AboveFingers.gif)</span><span class="sxs-lookup"><span data-stu-id="0ff8b-175">![Above fingers](images/AboveFingers.gif)</span></span><br>
        <span data-ttu-id="0ff8b-176">**Les doigts ci-dessus**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-176">**Above fingers**</span></span><br>
        <span data-ttu-id="0ff8b-177">fatigue à 1 main en raison de la main pendant une longue période</span><span class="sxs-lookup"><span data-stu-id="0ff8b-177">1 - Hand fatigue due to holding out hand for a long time</span></span><br>
        <span data-ttu-id="0ff8b-178">2 problèmes de suivi sur l’index et les doigts centraux</span><span class="sxs-lookup"><span data-stu-id="0ff8b-178">2 - Hand tracking issues on index and middle fingers</span></span>
    :::column-end:::
:::row-end:::

<br>

:::row:::
    :::column:::
        <span data-ttu-id="0ff8b-179">![Au-dessus de Center Palm](images/handCenter.gif)</span><span class="sxs-lookup"><span data-stu-id="0ff8b-179">![Above center palm](images/handCenter.gif)</span></span><br>
        <span data-ttu-id="0ff8b-180">**Au-dessus-Centre Palm**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-180">**Above-center palm**</span></span><br>
        <span data-ttu-id="0ff8b-181">problèmes de suivi de 1 main en raison du chevauchement des mains</span><span class="sxs-lookup"><span data-stu-id="0ff8b-181">1 - Hand tracking issues due to overlapping hands</span></span><br>
        <span data-ttu-id="0ff8b-182">fatigue à deux mains, en raison de la maintenance de longue durée pour interagir avec les menus</span><span class="sxs-lookup"><span data-stu-id="0ff8b-182">2 - Hand fatigue due to holding hands for long time in order to interact with menus</span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="0ff8b-183">![Le haut ](images/TopFingerTip.gif) de **la main**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-183">![Top Fingertip](images/TopFingerTip.gif) **Top fingertip**</span></span><br>
        <span data-ttu-id="0ff8b-184">1-problèmes de suivi de la main</span><span class="sxs-lookup"><span data-stu-id="0ff8b-184">1 - Hand tracking issues</span></span><br>
        <span data-ttu-id="0ff8b-185">2-la fatigue de la main au-dessus de la position normale</span><span class="sxs-lookup"><span data-stu-id="0ff8b-185">2 - Hand fatigue from holding hand above normal posture</span></span><br>
        <span data-ttu-id="0ff8b-186">3-problèmes de pression sur les boutons avec d’autres doigts par accident en raison d’un espace limité entre les doigts</span><span class="sxs-lookup"><span data-stu-id="0ff8b-186">3 - Issues pressing buttons with other fingers by accident due to limited space between fingers</span></span>
    :::column-end:::
:::row-end:::

<br>

:::row:::
    :::column:::
        <span data-ttu-id="0ff8b-187">![Arrière du bras](images/BackOfTheArm.gif)</span><span class="sxs-lookup"><span data-stu-id="0ff8b-187">![Back of the Arm](images/BackOfTheArm.gif)</span></span><br>
        <span data-ttu-id="0ff8b-188">**Arrière du bras**</span><span class="sxs-lookup"><span data-stu-id="0ff8b-188">**Back of the arm**</span></span><br>
        <span data-ttu-id="0ff8b-189">1-peut déclencher le bouton d’origine par accident</span><span class="sxs-lookup"><span data-stu-id="0ff8b-189">1 - Can trigger home button by accident</span></span><br>
        <span data-ttu-id="0ff8b-190">2-n’est pas une position naturelle ou confortable</span><span class="sxs-lookup"><span data-stu-id="0ff8b-190">2 - Not a natural or comfortable position</span></span>
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

<br>

---

## <a name="hand-menu-in-mrtk-mixed-reality-toolkit-for-unity"></a><span data-ttu-id="0ff8b-191">Menu de la main dans MRTK (ensemble d’outils de réalité mixte) pour Unity</span><span class="sxs-lookup"><span data-stu-id="0ff8b-191">Hand menu in MRTK (Mixed Reality Toolkit) for Unity</span></span>
<span data-ttu-id="0ff8b-192">**[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)** fournit des scripts et des exemples de scènes pour le menu de la main.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-192">**[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)** provides scripts and example scenes for the hand menu.</span></span> <span data-ttu-id="0ff8b-193">Le script du solveur HandConstraintPalmUp vous permet de joindre des objets aux mains avec différentes options configurables.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-193">The HandConstraintPalmUp solver script allows you to attach any objects to the hands with various configurable options.</span></span> <span data-ttu-id="0ff8b-194">Les exemples de menu manuel de MRTK incluent des options utiles, telles que le Palm plat et le point de vue du regard pour empêcher l’activation erronée.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-194">MRTK's hand menu examples include useful options such as flat palm and gaze requirement for preventing false activation.</span></span>

* [<span data-ttu-id="0ff8b-195">Documentation des menus contextuels</span><span class="sxs-lookup"><span data-stu-id="0ff8b-195">Hand Menu Documentations</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_HandMenu.html)
* [<span data-ttu-id="0ff8b-196">Exemple de scène de menu manuel</span><span class="sxs-lookup"><span data-stu-id="0ff8b-196">Hand Menu Example Scene</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_development/Assets/MRTK/Examples/Demos/HandTracking/Scenes/HandMenuExamples.unity)

<span data-ttu-id="0ff8b-197">Vous pouvez essayer des exemples de menu manuel dans HoloLens 2 avec l’application MRTK d’exemples de Hub.</span><span class="sxs-lookup"><span data-stu-id="0ff8b-197">You can try hand menu examples in HoloLens 2 with MRTK Examples Hub app.</span></span> 
* [<span data-ttu-id="0ff8b-198">Scène du menu manuel dans MRTK exemples Hub</span><span class="sxs-lookup"><span data-stu-id="0ff8b-198">Hand Menu Scene in MRTK Examples Hub</span></span>](https://www.microsoft.com/en-us/p/mrtk-examples-hub/9mv8c39l2sj4?activetab=pivot:overviewtab)

<br>

---


## <a name="see-also"></a><span data-ttu-id="0ff8b-199">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="0ff8b-199">See also</span></span>

* [<span data-ttu-id="0ff8b-200">Curseurs</span><span class="sxs-lookup"><span data-stu-id="0ff8b-200">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="0ff8b-201">Rayon émanant de la main</span><span class="sxs-lookup"><span data-stu-id="0ff8b-201">Hand ray</span></span>](point-and-commit.md)
* [<span data-ttu-id="0ff8b-202">Button</span><span class="sxs-lookup"><span data-stu-id="0ff8b-202">Button</span></span>](button.md)
* [<span data-ttu-id="0ff8b-203">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="0ff8b-203">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="0ff8b-204">Rectangle englobant et barre de l’application</span><span class="sxs-lookup"><span data-stu-id="0ff8b-204">Bounding box and App bar</span></span>](app-bar-and-bounding-box.md)
* [<span data-ttu-id="0ff8b-205">Manipulation</span><span class="sxs-lookup"><span data-stu-id="0ff8b-205">Manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="0ff8b-206">Menu de la main</span><span class="sxs-lookup"><span data-stu-id="0ff8b-206">Hand menu</span></span>](hand-menu.md)
* [<span data-ttu-id="0ff8b-207">Menu proche</span><span class="sxs-lookup"><span data-stu-id="0ff8b-207">Near menu</span></span>](near-menu.md)
* [<span data-ttu-id="0ff8b-208">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="0ff8b-208">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="0ff8b-209">Commande vocale</span><span class="sxs-lookup"><span data-stu-id="0ff8b-209">Voice command</span></span>](voice-input.md)
* [<span data-ttu-id="0ff8b-210">Clavier</span><span class="sxs-lookup"><span data-stu-id="0ff8b-210">Keyboard</span></span>](keyboard.md)
* [<span data-ttu-id="0ff8b-211">Info-bulle</span><span class="sxs-lookup"><span data-stu-id="0ff8b-211">Tooltip</span></span>](tooltip.md)
* [<span data-ttu-id="0ff8b-212">Tablette</span><span class="sxs-lookup"><span data-stu-id="0ff8b-212">Slate</span></span>](slate.md)
* [<span data-ttu-id="0ff8b-213">Curseur</span><span class="sxs-lookup"><span data-stu-id="0ff8b-213">Slider</span></span>](slider.md)
* [<span data-ttu-id="0ff8b-214">Nuanceur</span><span class="sxs-lookup"><span data-stu-id="0ff8b-214">Shader</span></span>](shader.md)
* [<span data-ttu-id="0ff8b-215">Billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="0ff8b-215">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
* [<span data-ttu-id="0ff8b-216">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="0ff8b-216">Displaying progress</span></span>](progress.md)
* [<span data-ttu-id="0ff8b-217">Aimantation de surface</span><span class="sxs-lookup"><span data-stu-id="0ff8b-217">Surface magnetism</span></span>](surface-magnetism.md)
