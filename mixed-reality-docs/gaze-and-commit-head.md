---
title: Suivre de la tête et valider
description: Vue d’ensemble du modèle d’entrée Suivre de la tête et valider
author: caseymeekhof
ms.author: cmeekhof
ms.date: 03/31/2019
ms.topic: article
keywords: Mixed Reality, pointage du regard, ciblage avec le regard, interaction, conception
ms.openlocfilehash: 5fef778dde6852222e098aeb1cbb41fe04e0b744
ms.sourcegitcommit: a5dc182da237f63f0487d40a2e11894027208b6c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73441094"
---
# <a name="head-gaze-and-commit"></a><span data-ttu-id="3a823-104">Suivre de la tête et valider</span><span class="sxs-lookup"><span data-stu-id="3a823-104">Head-gaze and commit</span></span>
<span data-ttu-id="3a823-105">Le point de _regard et la validation de tête_ est un cas spécial du modèle d’entrée de pointage [et de validation](gaze-and-commit.md) qui implique le ciblage d’un objet avec la direction de la tête vers l’avant (direction de l’en-tête), puis l’action avec une entrée secondaire, telle que l’air de mouvement vers la main Appuyez sur ou sur la commande vocale « Select ».</span><span class="sxs-lookup"><span data-stu-id="3a823-105">_Head-gaze and commit_ is a special case of the [gaze and commit](gaze-and-commit.md) input model that involves targeting an object with the direction of your head pointing forward (head-direction), and then acting on it with a secondary input, such as the hand gesture air tap or the voice command "Select".</span></span> 

## <a name="device-support"></a><span data-ttu-id="3a823-106">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="3a823-106">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="3a823-107"><strong>Modèle d’entrée</strong></span><span class="sxs-lookup"><span data-stu-id="3a823-107"><strong>Input model</strong></span></span></td>
        <td><span data-ttu-id="3a823-108"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="3a823-108"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="3a823-109"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="3a823-109"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="3a823-110"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="3a823-110"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="3a823-111">Suivre de la tête et valider</span><span class="sxs-lookup"><span data-stu-id="3a823-111">Head-gaze and commit</span></span></td>
        <td><span data-ttu-id="3a823-112">✔️ Recommandé</span><span class="sxs-lookup"><span data-stu-id="3a823-112">✔️ Recommended</span></span></td>
        <td><span data-ttu-id="3a823-113">✔️ Recommandé (troisième choix ; <a href="interaction-fundamentals.md">voir les autres options</a>)</span><span class="sxs-lookup"><span data-stu-id="3a823-113">✔️ Recommended (third choice - <a href="interaction-fundamentals.md">See the other options</a>)</span></span></td>
        <td><span data-ttu-id="3a823-114">➕ Autre option</span><span class="sxs-lookup"><span data-stu-id="3a823-114">➕ Alternate option</span></span></td>
    </tr>
</table>

---

## <a name="target-sizing-and-feedback"></a><span data-ttu-id="3a823-115">Dimensionnement des cibles et retour</span><span class="sxs-lookup"><span data-stu-id="3a823-115">Target sizing and feedback</span></span>
<span data-ttu-id="3a823-116">Le point de regard de l’en-tête a été affiché à plusieurs reprises pour être utilisable pour un ciblage précis, mais il fonctionne souvent mieux pour le ciblage brut, en acquérant des cibles de plus grande taille.</span><span class="sxs-lookup"><span data-stu-id="3a823-116">The head gaze vector has been shown repeatedly to be usable for fine targeting, but often works best for gross targeting--acquiring somewhat larger targets.</span></span> <span data-ttu-id="3a823-117">Les tailles de cible minimales de 1 à 1,5 degrés permettent des actions utilisateur réussies dans la plupart des scénarios, bien que les cibles de 3 degrés offrent souvent une vitesse supérieure.</span><span class="sxs-lookup"><span data-stu-id="3a823-117">Minimum target sizes of 1 to 1.5 degrees allow successful user actions in most scenarios, though targets of 3 degrees often allow for greater speed.</span></span> <span data-ttu-id="3a823-118">Notez que la taille que cible l’utilisateur est une zone 2D même pour les éléments 3D ; la projection qui lui fait face, quelle qu’elle soit, doit être la zone pouvant être ciblée.</span><span class="sxs-lookup"><span data-stu-id="3a823-118">Note that the size that the user targets is effectively a 2D area even for 3D elements--whichever projection is facing them should be the targetable area.</span></span> <span data-ttu-id="3a823-119">Fournir une indication importante indiquant qu’un élément est « actif » (que l’utilisateur cible) est extrêmement utile.</span><span class="sxs-lookup"><span data-stu-id="3a823-119">Providing some salient cue that an element is "active" (that the user is targeting it) is extremely helpful.</span></span> <span data-ttu-id="3a823-120">Cela peut inclure des traitements tels que des effets de « survol » visibles, des surbrillances audio ou des clics, ou l’alignement clair d’un curseur avec un élément.</span><span class="sxs-lookup"><span data-stu-id="3a823-120">This can include treatments like visible "hover" effects, audio highlights or clicks, or clear alignment of a cursor with an element.</span></span>

<span data-ttu-id="3a823-121">![Taille optimale de la cible à une distance de 2 mètres](images/gazetargeting-size-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="3a823-121">![Optimal target size at 2 meter distance](images/gazetargeting-size-1000px.jpg)</span></span><br>
<span data-ttu-id="3a823-122">*Taille optimale de la cible à une distance de 2 mètres*</span><span class="sxs-lookup"><span data-stu-id="3a823-122">*Optimal target size at 2 meter distance*</span></span>

<br>

<span data-ttu-id="3a823-123">![Exemple de mise en surbrillance d’un objet ciblé avec le regard](images/gazetargeting-highlighting-940px.jpg)</span><span class="sxs-lookup"><span data-stu-id="3a823-123">![An example of highlighting a gaze targeted object](images/gazetargeting-highlighting-940px.jpg)</span></span><br>
<span data-ttu-id="3a823-124">*Exemple de mise en surbrillance d’un objet ciblé avec le regard*</span><span class="sxs-lookup"><span data-stu-id="3a823-124">*An example of highlighting a gaze targeted object*</span></span>

## <a name="target-placement"></a><span data-ttu-id="3a823-125">Placement de la cible</span><span class="sxs-lookup"><span data-stu-id="3a823-125">Target placement</span></span>
<span data-ttu-id="3a823-126">Souvent, les utilisateurs ne parviennent pas à trouver des éléments d’interface utilisateur qui sont positionnés très haut ou très bas dans leur champ de vision, en mettant l’accent sur les zones autour de leur objectif principal, ce qui est à peu près oculaire.</span><span class="sxs-lookup"><span data-stu-id="3a823-126">Users often fail to find UI elements that are positioned very high or very low in their field of view, focusing most of their attention on areas around their main focus, which is approximately at eye level.</span></span> <span data-ttu-id="3a823-127">Le fait de placer la plupart des cibles dans une bande raisonnable autour des yeux peut s’avérer utile.</span><span class="sxs-lookup"><span data-stu-id="3a823-127">Placing most targets in some reasonable band around eye level can help.</span></span> <span data-ttu-id="3a823-128">Etant donné que les utilisateurs ont tendance à se concentrer sur un champ visuel relativement étroit (le cône de vision lié à l’attention est à peu près de 10 degrés), ils sont davantage susceptibles de passer d’un élément à l’autre à mesure qu’ils déplacent leur regard si les éléments d’interface utilisateur d’un même concept sont regroupés dans ce champ de vision.</span><span class="sxs-lookup"><span data-stu-id="3a823-128">Given the tendency for users to focus on a relatively small visual area at any time (the attentional cone of vision is roughly 10 degrees), grouping UI elements together to the degree that they're related conceptually can leverage attention-chaining behaviors from item to item as a user moves their gaze through an area.</span></span> <span data-ttu-id="3a823-129">Quand vous concevez l’interface utilisateur, gardez à l’esprit les grandes variations potentielles du champ de vision entre les casques immersifs et HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3a823-129">When designing UI, keep in mind the potential large variation in field of view between HoloLens and immersive headsets.</span></span>

<span data-ttu-id="3a823-130">![Exemple d’éléments d’interface utilisateur groupés pour faciliter le ciblage avec le regard dans Galaxy Explorer](images/gazetargeting-grouping-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="3a823-130">![An example of grouped UI elements for easier gaze targeting in Galaxy Explorer](images/gazetargeting-grouping-1000px.jpg)</span></span><br>
<span data-ttu-id="3a823-131">*Exemple d’éléments d’interface utilisateur groupés pour faciliter le ciblage avec le regard dans Galaxy Explorer*</span><span class="sxs-lookup"><span data-stu-id="3a823-131">*An example of grouped UI elements for easier gaze targeting in Galaxy Explorer*</span></span>

## <a name="improving-targeting-behaviors"></a><span data-ttu-id="3a823-132">Amélioration des comportements de ciblage</span><span class="sxs-lookup"><span data-stu-id="3a823-132">Improving targeting behaviors</span></span>
<span data-ttu-id="3a823-133">Si l’intention de l’utilisateur de cibler un événement peut être déterminée (ou approchée), il peut être très utile d’accepter des tentatives presque manquées à l’interaction comme si elles étaient ciblées correctement.</span><span class="sxs-lookup"><span data-stu-id="3a823-133">If user intent to target something can be determined (or approximated closely), it can be very helpful to accept near miss attempts at interaction as though they were targeted correctly.</span></span> <span data-ttu-id="3a823-134">Voici quelques-unes des méthodes qui peuvent être incorporées dans les expériences de réalité mixte :</span><span class="sxs-lookup"><span data-stu-id="3a823-134">Here are a handful of successful methods that can be incorporated in mixed reality experiences:</span></span>

### <a name="head-gaze-stabilization-gravity-wells"></a><span data-ttu-id="3a823-135">Stabilisation avec suivi de la tête (« stabilisation de la gravité »)</span><span class="sxs-lookup"><span data-stu-id="3a823-135">Head-gaze stabilization ("gravity wells")</span></span>
<span data-ttu-id="3a823-136">Cette fonction doit être activée le plus ou la totalité du temps.</span><span class="sxs-lookup"><span data-stu-id="3a823-136">This should be turned on most or all of the time.</span></span> <span data-ttu-id="3a823-137">Cette technique supprime les instabilités de tête et de cou naturelles que les utilisateurs peuvent avoir en mouvement en raison des comportements de recherche et de conversation.</span><span class="sxs-lookup"><span data-stu-id="3a823-137">This technique removes the natural head and neck jitters that users might have as well movement due to looking and speaking behaviors.</span></span>

### <a name="closest-link-algorithms"></a><span data-ttu-id="3a823-138">Algorithmes du lien le plus proche</span><span class="sxs-lookup"><span data-stu-id="3a823-138">Closest link algorithms</span></span>
<span data-ttu-id="3a823-139">Ces derniers fonctionnent le mieux dans les zones dont le contenu interactif est clairsemé.</span><span class="sxs-lookup"><span data-stu-id="3a823-139">These work best in areas with sparse interactive content.</span></span> <span data-ttu-id="3a823-140">S’il existe une forte probabilité que vous puissiez déterminer ce à quoi un utilisateur tente d’interagir, vous pouvez compléter ses capacités de ciblage en supposant un certain niveau d’intention.</span><span class="sxs-lookup"><span data-stu-id="3a823-140">If there is a high probability that you can determine what a user was attempting to interact with, you can supplement their targeting abilities by assuming some level of intent.</span></span>

### <a name="backdating-and-postdating-actions"></a><span data-ttu-id="3a823-141">Actions d’postdating et de mise à jour</span><span class="sxs-lookup"><span data-stu-id="3a823-141">Backdating and postdating actions</span></span>
<span data-ttu-id="3a823-142">Ce mécanisme est utile dans les tâches nécessitant de la vitesse.</span><span class="sxs-lookup"><span data-stu-id="3a823-142">This mechanism is useful in tasks requiring speed.</span></span> <span data-ttu-id="3a823-143">Lorsqu’un utilisateur parcourt une série de manoeuvres de ciblage et d’activation à la vitesse, il est utile de prendre des mesures et d’autoriser les étapes manquées à agir sur les cibles que l’utilisateur a placées plus légèrement avant ou légèrement après le TAP (50 ms avant/après). test RLY).</span><span class="sxs-lookup"><span data-stu-id="3a823-143">When a user is moving through a series of targeting and activation maneuvers at speed, it is useful to assume some intent, and allow missed steps to act upon targets that the user had in focus slightly before or slightly after the tap (50 ms before/after was effective in early testing).</span></span>

### <a name="smoothing"></a><span data-ttu-id="3a823-144">Adoucissage</span><span class="sxs-lookup"><span data-stu-id="3a823-144">Smoothing</span></span>
<span data-ttu-id="3a823-145">Ce mécanisme est utile pour le tracé des mouvements, en réduisant les légères gigues et les tremblements dus aux caractéristiques naturelles de mouvement de la tête.</span><span class="sxs-lookup"><span data-stu-id="3a823-145">This mechanism is useful for pathing movements, reducing the slight jitter and wobble due to natural head movement characteristics.</span></span> <span data-ttu-id="3a823-146">En cas de lissage sur les mouvements de tracés, lisse par la taille et la distance des mouvements plutôt qu’au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="3a823-146">When smoothing over pathing motions, smooth by the size and distance of movements rather than over time.</span></span>

### <a name="magnetism"></a><span data-ttu-id="3a823-147">Magnétisme</span><span class="sxs-lookup"><span data-stu-id="3a823-147">Magnetism</span></span>
<span data-ttu-id="3a823-148">Ce mécanisme peut être considéré comme une version plus générale des algorithmes de lien les plus proches : le fait de dessiner un curseur vers une cible ou d’augmenter simplement hitboxes, visuellement ou non, à mesure que les utilisateurs approchent les cibles probables en utilisant une connaissance de la disposition interactive pour mieux approche de l’intention de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3a823-148">This mechanism can be thought of as a more general version of closest link algorithms--drawing a cursor toward a target or simply increasing hitboxes, whether visibly or not, as users approach likely targets by using some knowledge of the interactive layout to better approach user intent.</span></span> <span data-ttu-id="3a823-149">Il peut être particulièrement efficace pour les petites cibles.</span><span class="sxs-lookup"><span data-stu-id="3a823-149">This can be particularly powerful for small targets.</span></span>

### <a name="focus-stickiness"></a><span data-ttu-id="3a823-150">Adhérence du focus</span><span class="sxs-lookup"><span data-stu-id="3a823-150">Focus stickiness</span></span>
<span data-ttu-id="3a823-151">Lorsque vous déterminez les éléments interactifs proches auxquels donner le focus, l’adhérence au focus fournit un décalage à l’élément qui est actuellement concentré.</span><span class="sxs-lookup"><span data-stu-id="3a823-151">When determining which nearby interactive elements to give focus to, focus stickiness provides a bias to the element that is currently focused.</span></span> <span data-ttu-id="3a823-152">Cela permet de réduire les comportements de changement de focus erratiques lorsqu’ils flottent à un point médian entre deux éléments avec un bruit naturel.</span><span class="sxs-lookup"><span data-stu-id="3a823-152">This helps reduce erratic focus switching behaviors when floating at a midpoint between two elements with natural noise.</span></span>


## <a name="see-also"></a><span data-ttu-id="3a823-153">Articles associés</span><span class="sxs-lookup"><span data-stu-id="3a823-153">See also</span></span>
* [<span data-ttu-id="3a823-154">Interaction basée sur les yeux</span><span class="sxs-lookup"><span data-stu-id="3a823-154">Eye-based interaction</span></span>](eye-gaze-interaction.md)
* [<span data-ttu-id="3a823-155">Pointer du regard et fixer</span><span class="sxs-lookup"><span data-stu-id="3a823-155">Gaze and dwell</span></span>](gaze-and-dwell.md)
* [<span data-ttu-id="3a823-156">Manipulation directe</span><span class="sxs-lookup"><span data-stu-id="3a823-156">Hands - Direct manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="3a823-157">Mouvements pratiques</span><span class="sxs-lookup"><span data-stu-id="3a823-157">Hands - Gestures</span></span>](gaze-and-commit.md#composite-gestures)
* [<span data-ttu-id="3a823-158">Mains et validation</span><span class="sxs-lookup"><span data-stu-id="3a823-158">Hands - Point and commit</span></span>](point-and-commit.md)
* [<span data-ttu-id="3a823-159">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="3a823-159">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="3a823-160">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="3a823-160">Voice input</span></span>](voice-input.md)



