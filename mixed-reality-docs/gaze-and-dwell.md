---
title: Regards et durée d’affichage
description: Vue d’ensemble du modèle d’entrée du pointage de regard et durée d’affichage
author: liamartinez
ms.author: liamar
ms.date: 03/31/2019
ms.topic: article
keywords: Mixte réalité, regards, durée d’affichage, interaction, concevoir
ms.openlocfilehash: a50ae948a351f5152ebb98778da9be8c08090d72
ms.sourcegitcommit: 222cba2d622b47f75949bf8af80d5c62de4dceab
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2019
ms.locfileid: "64914613"
---
# <a name="gaze-and-dwell"></a><span data-ttu-id="99459-104">Regards et durée d’affichage</span><span class="sxs-lookup"><span data-stu-id="99459-104">Gaze and dwell</span></span>

<span data-ttu-id="99459-105">Lorsque mains sont occupées avec les outils et les parties, les gestes peuvent être fastidieuse, voire impossible.</span><span class="sxs-lookup"><span data-stu-id="99459-105">When hands are occupied with tools and parts, gestures can be tedious or impossible.</span></span>  <span data-ttu-id="99459-106">Les commandes vocales, comme un mouvement, peuvent être fait des circonstances fiables, par exemple dans des conditions très bruyants.</span><span class="sxs-lookup"><span data-stu-id="99459-106">Voice commands, like gesture, can be situationally unreliable, for example under excessively loud conditions.</span></span>  <span data-ttu-id="99459-107">En outre, voix à des ordinateurs de contrôle n’est pas encore une interaction de grand public, mais il est gagne à vapeur !</span><span class="sxs-lookup"><span data-stu-id="99459-107">Additionally, using voice to control computers isn't a mainstream interaction yet, but it certainly is gaining steam!</span></span>  <span data-ttu-id="99459-108">Durée d’affichage du pointage de regard offre le mécanisme plus familière et facile à master pour tête haute travail mains-libres sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="99459-108">Gaze dwell offers the most familiar and easy-to-master mechanism for working heads-up hands-free on HoloLens.</span></span>  <span data-ttu-id="99459-109">En outre, la durée d’affichage du pointage de regard est fiables à 100 % indépendantes des contraintes de bruit interférence ni de silence dans l’environnement d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="99459-109">Additionally, gaze dwell is 100% reliable independent of noise interference nor silence constraints in the operating environment.</span></span>

## <a name="goals"></a><span data-ttu-id="99459-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="99459-110">Goals</span></span>

<span data-ttu-id="99459-111">Fournissent un mécanisme pour les interactions de mains-libres, sans utiliser la voix.</span><span class="sxs-lookup"><span data-stu-id="99459-111">Provide a mechanism for full hands-free interactions, without using Voice.</span></span>

## <a name="design-principles"></a><span data-ttu-id="99459-112">Principes de conception</span><span class="sxs-lookup"><span data-stu-id="99459-112">Design principles</span></span>

1. <span data-ttu-id="99459-113">Regards n’est pas une arme</span><span class="sxs-lookup"><span data-stu-id="99459-113">Gaze is not a weapon</span></span>
    
    <span data-ttu-id="99459-114">Regards requiert des commentaires visuels pour tactiles intuitives, mais trop commentaires peuvent provoquer l’anxiété.</span><span class="sxs-lookup"><span data-stu-id="99459-114">Gaze requires visual feedback for intuitive interaction, but too much feedback can induce anxiety.</span></span> <span data-ttu-id="99459-115">Les commentaires doivent aider un utilisateur qu’ils vous ciblez, mais pas-sélection automatique par rapport à leur intention.</span><span class="sxs-lookup"><span data-stu-id="99459-115">The feedback should help a user know what they're targeting, but not auto-select against their intent.</span></span> <span data-ttu-id="99459-116">Lire le texte nécessite des précautions supplémentaires pour fournir une salle de l’utilisateur pour absorber les informations avant de sélectionner.</span><span class="sxs-lookup"><span data-stu-id="99459-116">Reading text requires extra consideration to provide a user room to absorb the info before selecting.</span></span>
    
2. <span data-ttu-id="99459-117">Vitesse de boucles d’or de recherche</span><span class="sxs-lookup"><span data-stu-id="99459-117">Seek Goldilocks speed</span></span>
    
    <span data-ttu-id="99459-118">Le remplissage de balayage peut avoir différents minuteurs en fonction de l’impact de la navigation : fonctions les plus fréquemment utilisées généralement bénéficieront de remplissage plus rapides, tandis que les fonctions plus indirects peuvent bénéficier de temps de remplissage.</span><span class="sxs-lookup"><span data-stu-id="99459-118">The dwell fill can have different timers based on impact of navigation - more frequently used functions will generally benefit from faster fill times, while more consequential functions may benefit from longer fill times.</span></span> <span data-ttu-id="99459-119">Courbes de l’animation de la couleur de remplissage peuvent influencer positivement un sentiment de temps de remplissage plus rapides.</span><span class="sxs-lookup"><span data-stu-id="99459-119">Animation curves of the fill color can positively influence a feeling of faster fill times.</span></span> <span data-ttu-id="99459-120">Considération doit être prise pour activer la décision de l’utilisateur à partir de fast/moyenne/ralentir les remplacements de vitesse de remplissage.</span><span class="sxs-lookup"><span data-stu-id="99459-120">Consideration should be taken to enable user decision from fast/medium/slow fill speed overrides.</span></span>
    
3. <span data-ttu-id="99459-121">Par exemple no-no pour effet d’yo-yo</span><span class="sxs-lookup"><span data-stu-id="99459-121">Say no-no to yo-yo effect</span></span>

    <span data-ttu-id="99459-122">L’effet d’yo-yo (également appelé « nuit à le Roxbury ») est un modèle désagréable qui peut émerger à partir de certains placement du contenu et des contrôles basés sur des regards.</span><span class="sxs-lookup"><span data-stu-id="99459-122">The yo-yo effect (also known as "Night at the Roxbury") is an uncomfortable pattern that can emerge from certain  placement of content and gaze-based controls.</span></span> <span data-ttu-id="99459-123">Par exemple, une liste de navigation avec le bouton de remplissage en bas provoque une boucle des - rechercher vers le bas pour m’attarderai pas, examinez résultats, descendez à durée d’affichage, etc. Ce modèle qui en résulte est désagréable et doit être évité en plaçant les contrôles de navigation dans un emplacement centralisé qui nécessite moins de back-et-les deux sens.</span><span class="sxs-lookup"><span data-stu-id="99459-123">For example, a list nav with the fill button at the bottom induces a loop of - look down to dwell, look up at results, look down to dwell, etc. This resulting pattern is uncomfortable and should be avoided by placing navigation controls in a centralized location that requires less back-and-forth.</span></span> <span data-ttu-id="99459-124">L’emplacement des boutons de durée d’affichage par rapport à leurs effets devient important pour plus de confort.</span><span class="sxs-lookup"><span data-stu-id="99459-124">Placement of dwell buttons relative to their effects becomes important for comfort.</span></span>

## <a name="ui-patterns"></a><span data-ttu-id="99459-125">Modèles d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="99459-125">UI patterns</span></span>

### <a name="high-frequency-buttons"></a><span data-ttu-id="99459-126">Boutons de fréquence élevée</span><span class="sxs-lookup"><span data-stu-id="99459-126">High frequency buttons</span></span>
    
* <span data-ttu-id="99459-127">Boutons suivant/précédent</span><span class="sxs-lookup"><span data-stu-id="99459-127">Next/Back buttons</span></span>
  * <span data-ttu-id="99459-128">Remplissage préalable de délai très court (tampon du scintillement passage supérieur)</span><span class="sxs-lookup"><span data-stu-id="99459-128">Very short delay pre-fill (flyover flicker buffer)</span></span>
  * <span data-ttu-id="99459-129">Boutons plus volumineux sont plus faciles à atteindre du pointage de regard</span><span class="sxs-lookup"><span data-stu-id="99459-129">Larger buttons are easier to hit with gaze</span></span>
  * <span data-ttu-id="99459-130">Bon de ne tenir compte de ces à hauteur des yeux donc aucune déformation pour interagir</span><span class="sxs-lookup"><span data-stu-id="99459-130">Nice to keep these at eye height so no strain to interact</span></span>
  * <span data-ttu-id="99459-131">Région de la durée d’affichage peut être supérieure à icône inactive pour le rendre plus facile à utiliser (arrière)</span><span class="sxs-lookup"><span data-stu-id="99459-131">Dwell region can be larger than inactive icon to make it easier to use (BACK)</span></span>

### <a name="low-frequency-buttons"></a><span data-ttu-id="99459-132">Boutons de fréquence faible</span><span class="sxs-lookup"><span data-stu-id="99459-132">Low frequency buttons</span></span>
    
* <span data-ttu-id="99459-133">Activer le menu Paramètres</span><span class="sxs-lookup"><span data-stu-id="99459-133">Activate settings menu</span></span>
  * <span data-ttu-id="99459-134">Retarder plus remplissage préalable OK (tampon du scintillement passage supérieur)</span><span class="sxs-lookup"><span data-stu-id="99459-134">Longer delay pre-fill okay (flyover flicker buffer)</span></span>
  * <span data-ttu-id="99459-135">Essaie de garder ces boutons hors de votre zone voies de curseur fréquentes</span><span class="sxs-lookup"><span data-stu-id="99459-135">Try to keep these buttons out of the way of frequent cursor pathways</span></span>

* <span data-ttu-id="99459-136">Confirmations (autrement dit, les flux d’analyse, les boîtes de dialogue)</span><span class="sxs-lookup"><span data-stu-id="99459-136">Confirmations (i.e. scan flow, dialogs)</span></span>
  * <span data-ttu-id="99459-137">Afficher la surbrillance de sélection sur le bouton principal</span><span class="sxs-lookup"><span data-stu-id="99459-137">Show selection highlight on main button</span></span>
  * <span data-ttu-id="99459-138">Révéler la cible de la durée d’affichage en même temps que la surbrillance de sélection</span><span class="sxs-lookup"><span data-stu-id="99459-138">Reveal dwell target at same time as selection highlight</span></span>
  * <span data-ttu-id="99459-139">Utilisez m’attarderai pas cible entourant l’icône pour simplifier l’interface</span><span class="sxs-lookup"><span data-stu-id="99459-139">Use dwell target surrounding icon to keep interface simple</span></span>
  * <span data-ttu-id="99459-140">Décision importante, afin de n’active la mise en surbrillance, révèle cible de la durée d’affichage pour les temps de réexamen</span><span class="sxs-lookup"><span data-stu-id="99459-140">Important decision, so highlight doesn't activate, reveals dwell target for reconsideration time</span></span>
        
### <a name="toggle-buttons"></a><span data-ttu-id="99459-141">Boutons bascule</span><span class="sxs-lookup"><span data-stu-id="99459-141">Toggle buttons</span></span>

* <span data-ttu-id="99459-142">Pin</span><span class="sxs-lookup"><span data-stu-id="99459-142">Pin</span></span>
  * <span data-ttu-id="99459-143">État visuel clair actives/inactives</span><span class="sxs-lookup"><span data-stu-id="99459-143">Clear active/inactive visual state</span></span>
  * <span data-ttu-id="99459-144">Remplissage radiale permet à utilisateur de focus et fournit la progression naturelle</span><span class="sxs-lookup"><span data-stu-id="99459-144">Radial fill helps focus user and provides natural progress</span></span> 

* <span data-ttu-id="99459-145">Paramètres individuels</span><span class="sxs-lookup"><span data-stu-id="99459-145">Individual settings</span></span>
  * <span data-ttu-id="99459-146">États clair actives/inactives</span><span class="sxs-lookup"><span data-stu-id="99459-146">Clear active/inactive states</span></span>
  * <span data-ttu-id="99459-147">M’attarderai pas cibles tous sur l’icône environnante gauche</span><span class="sxs-lookup"><span data-stu-id="99459-147">Dwell targets all on left surrounding icon</span></span>
  * <span data-ttu-id="99459-148">Durée d’affichage cible s’affichent uniquement quand sélection mettre en surbrillance active</span><span class="sxs-lookup"><span data-stu-id="99459-148">Dwell targets only show up when selection highlight active</span></span>
  * <span data-ttu-id="99459-149">« M’attarderai pas sur curseur « côté droit pour activé/désactivé des paramètres</span><span class="sxs-lookup"><span data-stu-id="99459-149">"Dwell on slider" on right side for on/off settings</span></span>

### <a name="list-views"></a><span data-ttu-id="99459-150">Affichages de liste</span><span class="sxs-lookup"><span data-stu-id="99459-150">List views</span></span>

* <span data-ttu-id="99459-151">Affichage de liste navigation - fichiers de guide à ouvrir</span><span class="sxs-lookup"><span data-stu-id="99459-151">Browsing list view - guide files to open</span></span>
  * <span data-ttu-id="99459-152">Points importants du curseur de ligne à partir de n’importe où sur la ligne, mais ne commence pas balayage</span><span class="sxs-lookup"><span data-stu-id="99459-152">Cursor highlights row from anywhere on row but doesn’t begin dwell</span></span>
  * <span data-ttu-id="99459-153">Lors de la ligne est mise en surbrillance par le curseur, la cible de la durée d’affichage apparaît à gauche</span><span class="sxs-lookup"><span data-stu-id="99459-153">When row is highlighted by cursor, dwell target appears on left</span></span>
  * <span data-ttu-id="99459-154">M’attarderai pas cible toujours un cercle sur le côté gauche du texte dans tous les affichages de liste</span><span class="sxs-lookup"><span data-stu-id="99459-154">Dwell target always a circle on left side of text in all list views</span></span>
  * <span data-ttu-id="99459-155">Ne plus afficher que m’attarderai donc pas toutes les cibles à la fois pour éviter l’interface utilisateur répétitive</span><span class="sxs-lookup"><span data-stu-id="99459-155">Don't show all dwell targets at once to avoid repetitive UI</span></span>
  * <span data-ttu-id="99459-156">Réutiliser le même modèle pour établir une bonne connaissance de l’expérience utilisateur</span><span class="sxs-lookup"><span data-stu-id="99459-156">Re-use the same pattern to establish UX familiarity</span></span>
        
* <span data-ttu-id="99459-157">Mode liste - hiérarchie des tâches/étapes dans un repère de navigation</span><span class="sxs-lookup"><span data-stu-id="99459-157">Browsing list view - hierarchy of tasks/steps in a guide</span></span>
  * <span data-ttu-id="99459-158">M’attarderai pas cible toujours un cercle sur le côté gauche du texte</span><span class="sxs-lookup"><span data-stu-id="99459-158">Dwell target always a circle on left side of text</span></span>
  * <span data-ttu-id="99459-159">Développer/réduire intuitif de balayage</span><span class="sxs-lookup"><span data-stu-id="99459-159">Collapse/expand dwell affordance</span></span>
        
* <span data-ttu-id="99459-160">Affichage de liste navigation - mode select</span><span class="sxs-lookup"><span data-stu-id="99459-160">Browsing list view - mode select</span></span>
  * <span data-ttu-id="99459-161">Suivez les modèles ci-dessus</span><span class="sxs-lookup"><span data-stu-id="99459-161">Follow patterns established above</span></span>

### <a name="contextual-buttons"></a><span data-ttu-id="99459-162">Boutons contextuelles</span><span class="sxs-lookup"><span data-stu-id="99459-162">Contextual buttons</span></span>

* <span data-ttu-id="99459-163">Afficher/masquer 3D - affiche des 3D le long d’attache près hologrammes</span><span class="sxs-lookup"><span data-stu-id="99459-163">Show/Hide 3D - shows up in 3D along tether near holograms</span></span> 
  * <span data-ttu-id="99459-164">État visuel clair actives/inactives</span><span class="sxs-lookup"><span data-stu-id="99459-164">Clear active/inactive visual state</span></span>

### <a name="pivots"></a><span data-ttu-id="99459-165">Pivots</span><span class="sxs-lookup"><span data-stu-id="99459-165">Pivots</span></span>

* <span data-ttu-id="99459-166">Liste de récents/tous les repères</span><span class="sxs-lookup"><span data-stu-id="99459-166">Recent/All guides list</span></span>
  * <span data-ttu-id="99459-167">Remplir l’intuitif de l’interface utilisateur reste pour indiquer quel onglet est actif</span><span class="sxs-lookup"><span data-stu-id="99459-167">Fill the UI affordance that remains to indicate which tab is active</span></span>
  * <span data-ttu-id="99459-168">Pour les tableaux croisés dynamiques court terme unique, nous avons choisi de renoncer au modèle cible de balayage</span><span class="sxs-lookup"><span data-stu-id="99459-168">For short single word pivots, we elected to forego the dwell target pattern</span></span>
  * <span data-ttu-id="99459-169">Nous favorisé l’interface simplifiée par rapport à un autre cibles cercle 2 et une interface utilisateur plus large</span><span class="sxs-lookup"><span data-stu-id="99459-169">We favored the simplified interface over another 2 circle targets and a wider UI</span></span>
  * <span data-ttu-id="99459-170">Dans notre cas, les mots sont suffisamment courts pour qu’un délai fournit suffisamment confort avant leur remplissage</span><span class="sxs-lookup"><span data-stu-id="99459-170">In our case, the words are short enough that a delay provides enough comfort before filling</span></span>


## <a name="ux-guidelines-and-best-practices"></a><span data-ttu-id="99459-171">Les instructions de l’expérience utilisateur et les meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="99459-171">UX Guidelines and best practices</span></span>

### <a name="target-sizes"></a><span data-ttu-id="99459-172">Taille des cibles</span><span class="sxs-lookup"><span data-stu-id="99459-172">Target sizes</span></span>

  * <span data-ttu-id="99459-173">Taille minimale de l’icône PIN : 6cm dans l’espace universel dans Unity, 30 derniers éléments utilisés (30cm @ 2m)</span><span class="sxs-lookup"><span data-stu-id="99459-173">Pin icon minimum size: 6cm in world space in Unity, 30 MRUs ( 30cm @ 2m)</span></span>
  * <span data-ttu-id="99459-174">Sont les cibles de « elle était aimantées » ou « permanent » du tout ?</span><span class="sxs-lookup"><span data-stu-id="99459-174">Are the targets "magnetized" or "sticky" at all?</span></span> <span data-ttu-id="99459-175">(autrement dit, les regards lissage du curseur)</span><span class="sxs-lookup"><span data-stu-id="99459-175">(i.e. gaze cursor smoothing)</span></span>

### <a name="animation"></a><span data-ttu-id="99459-176">Animation</span><span class="sxs-lookup"><span data-stu-id="99459-176">Animation</span></span>

  * <span data-ttu-id="99459-177">Délai d’attente avant la durée d’affichage des déclencheurs visual .5sec</span><span class="sxs-lookup"><span data-stu-id="99459-177">Delay before dwell visual triggers .5sec</span></span>
  * <span data-ttu-id="99459-178">Durée de balayage visuel 1,2 s</span><span class="sxs-lookup"><span data-stu-id="99459-178">Duration of dwell visual 1.2sec</span></span>
  * <span data-ttu-id="99459-179">Animation de courbe ?</span><span class="sxs-lookup"><span data-stu-id="99459-179">Curve on animation?</span></span>

### <a name="visual-feedback"></a><span data-ttu-id="99459-180">Retour visuel</span><span class="sxs-lookup"><span data-stu-id="99459-180">Visual feedback</span></span>

  * <span data-ttu-id="99459-181">Remplir à partir de l’emplacement de début du curseur regards de radiale</span><span class="sxs-lookup"><span data-stu-id="99459-181">Radial fill from gaze cursor start location</span></span>
  * <span data-ttu-id="99459-182">Remplissage toujours radiale à partir du centre du bouton.</span><span class="sxs-lookup"><span data-stu-id="99459-182">Always radial fill from center of button.</span></span> <span data-ttu-id="99459-183">Une réponse cohérente est plus claire que toutes les directions différentes sur les boutons différents.</span><span class="sxs-lookup"><span data-stu-id="99459-183">A consistent response is less confusing than all different directions on different buttons.</span></span> 
    * <span data-ttu-id="99459-184">Cette règle peut être rompue, bien que pour les interactions directionnelle (par exemple, nav haut/bas/gauche/droite, etc.).</span><span class="sxs-lookup"><span data-stu-id="99459-184">This rule can be broken though for directional interactions (e.g., nav up/down/left/right, etc.).</span></span> <span data-ttu-id="99459-185">Par exemple, rend Guides une exception sur précédente/suivante va rester avec le bouton droit de remplissage.</span><span class="sxs-lookup"><span data-stu-id="99459-185">For example, Guides makes an exception on NEXT/BACK being left right fills.</span></span>
    * <span data-ttu-id="99459-186">Envisagez d’inversion radiale remplir à partir d’à l’extérieur (si l’activation/désactivation).</span><span class="sxs-lookup"><span data-stu-id="99459-186">Consider inverting radial fill from outside (if toggling off).</span></span> <span data-ttu-id="99459-187">Le sentiment inverse de l’envoi d’un bouton est un modèle intéressant visual pour maintenir.</span><span class="sxs-lookup"><span data-stu-id="99459-187">THe inverse feeling of pushing a button is a nice visual pattern to maintain.</span></span> 

### <a name="progressive-disclosure"></a><span data-ttu-id="99459-188">Affichage progressif</span><span class="sxs-lookup"><span data-stu-id="99459-188">Progressive Disclosure</span></span>

 * <span data-ttu-id="99459-189">Affichage progressif signifie que la cible de la durée d’affichage est affichée sur la mise en surbrillance (par exemple, dans un contrôle de liste)</span><span class="sxs-lookup"><span data-stu-id="99459-189">Progressive disclosure means that the dwell target is revealed on highlight (e.g., in a list control)</span></span>
 * <span data-ttu-id="99459-190">Points importants de barre de texte avec spotlight révèlent sur regards n’importe où sur le texte</span><span class="sxs-lookup"><span data-stu-id="99459-190">Text bar highlights with spotlight reveal on gaze anywhere on text</span></span>
 * <span data-ttu-id="99459-191">Cible de remplissage du pointage de regard apparaît toujours sur la gauche, mais uniquement pour l’élément de liste qui est mis en surbrillance</span><span class="sxs-lookup"><span data-stu-id="99459-191">Gaze fill target appears always on left, but only for the list item which is highlighted</span></span>
 * <span data-ttu-id="99459-192">Essayez d’éviter d’avoir toutes les cibles de balayage sur à tout moment en raison de l’aspect répétitif de cercles empilées</span><span class="sxs-lookup"><span data-stu-id="99459-192">Try to avoid having all dwell targets on at all times due to repetitive look of stacked circles</span></span>
 
 ## <a name="see-also"></a><span data-ttu-id="99459-193">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="99459-193">See also</span></span>
* [<span data-ttu-id="99459-194">Manipulation directe</span><span class="sxs-lookup"><span data-stu-id="99459-194">Direct manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="99459-195">Point et validation</span><span class="sxs-lookup"><span data-stu-id="99459-195">Point and commit</span></span>](point-and-commit.md)
* [<span data-ttu-id="99459-196">Fonctionnalités de base des interactions</span><span class="sxs-lookup"><span data-stu-id="99459-196">Interaction fundamentals</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="99459-197">Regards de tête et de validation</span><span class="sxs-lookup"><span data-stu-id="99459-197">Head-gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="99459-198">Regards et vocal</span><span class="sxs-lookup"><span data-stu-id="99459-198">Gaze and voice</span></span>](voice-design.md)
