---
title: Suivre de la tête et stabiliser
description: Vue d’ensemble du modèle d’entrée Suivre de la tête et stabiliser
author: liamartinez
ms.author: liamar
ms.date: 05/13/2019
ms.topic: article
keywords: Mixed Reality, pointer du regard, stabiliser, interaction, concevoir
ms.openlocfilehash: 6d209d3cc91ceecb4b9feef2925f093288c9f8ac
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73439310"
---
# <a name="head-gaze-and-dwell"></a><span data-ttu-id="0127b-104">Suivre de la tête et stabiliser</span><span class="sxs-lookup"><span data-stu-id="0127b-104">Head-gaze and dwell</span></span>

<span data-ttu-id="0127b-105">Quand les mains sont occupées avec des outils et des pièces, les mouvements peuvent être fastidieux, voire impossibles.</span><span class="sxs-lookup"><span data-stu-id="0127b-105">When hands are occupied with tools and parts, gestures can be tedious or impossible.</span></span> <span data-ttu-id="0127b-106">Les commandes vocales, à l’image des mouvements, peuvent être incertaines dans des contextes donnés, par exemple dans des conditions très bruyantes.</span><span class="sxs-lookup"><span data-stu-id="0127b-106">Voice commands, like gestures, can be unreliable in certain contexts, for example under excessively loud conditions.</span></span> <span data-ttu-id="0127b-107">En outre, l’utilisation de la voix pour contrôler les ordinateurs n’est pas universellement courante, mais elle est certainement en train de s’intensifier !</span><span class="sxs-lookup"><span data-stu-id="0127b-107">Additionally, using voice to control computers isn't universally common, but it certainly is gaining steam!</span></span> <span data-ttu-id="0127b-108">Le modèle Suivre de la tête et stabiliser offre le mécanisme le plus familier et le plus facile à maîtriser pour travailler sur HoloLens tête relevée et mains libres.</span><span class="sxs-lookup"><span data-stu-id="0127b-108">Head-gaze and dwell offers the most familiar and easy-to-master mechanism for working heads-up and hands-free on HoloLens.</span></span> <span data-ttu-id="0127b-109">De plus, ce modèle est fiable à 100 % ; il n’est pas sensible aux interférences sonores et ne demande pas le silence dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="0127b-109">Additionally, head-gaze and dwell is 100% reliable independent of noise interference nor silence constraints in the operating environment.</span></span>

## <a name="scenarios"></a><span data-ttu-id="0127b-110">Scénarios</span><span class="sxs-lookup"><span data-stu-id="0127b-110">Scenarios</span></span>

<span data-ttu-id="0127b-111">Le point de regard et le point de vue dans les scénarios où les mains d’une personne sont occupées avec d’autres tâches, et la voix n’est pas 100% fiable ou disponible en raison de contraintes environnementales ou sociales.</span><span class="sxs-lookup"><span data-stu-id="0127b-111">Head-gaze and dwell excels in scenarios where a person's hands are busy with other tasks, and voice isn't 100% reliable or available due to environmental or social constraints.</span></span> <span data-ttu-id="0127b-112">Un bon exemple est une personne portant un appareil HoloLens pour superposer des informations de référence tout en réparant un moteur de voiture.</span><span class="sxs-lookup"><span data-stu-id="0127b-112">A good example is a person wearing a HoloLens to overlay reference information while repairing a car engine.</span></span> <span data-ttu-id="0127b-113">Ses mains sont occupées par des outils ou supportent son corps quand elle se penche dans le compartiment du moteur.</span><span class="sxs-lookup"><span data-stu-id="0127b-113">Their hands are busy with tools or supporting their body as they lean into the engine compartment.</span></span> <span data-ttu-id="0127b-114">L’espace du garage est bruyant, les coups et bourdonnement constants des outils rendant difficile l’utilisation de commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="0127b-114">The garage space is loud, with the constant banging and buzzing of tools, making voice commands difficult.</span></span> <span data-ttu-id="0127b-115">Le point de regard et l’arrière-plan permet à la personne utilisant HoloLens de parcourir en toute confiance son document de référence sans interrompre son flux de travail.</span><span class="sxs-lookup"><span data-stu-id="0127b-115">Head-gaze and dwell allows the person using the HoloLens to confidently navigate their reference material without interrupting their workflow.</span></span> 

## <a name="device-support"></a><span data-ttu-id="0127b-116">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="0127b-116">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="0127b-117"><strong>Modèle d’entrée</strong></span><span class="sxs-lookup"><span data-stu-id="0127b-117"><strong>Input model</strong></span></span></td>
        <td><span data-ttu-id="0127b-118"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="0127b-118"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="0127b-119"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="0127b-119"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="0127b-120"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="0127b-120"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="0127b-121">Suivre de la tête et stabiliser</span><span class="sxs-lookup"><span data-stu-id="0127b-121">Head-gaze and dwell</span></span></td>
        <td><span data-ttu-id="0127b-122">✔️ Recommandé</span><span class="sxs-lookup"><span data-stu-id="0127b-122">✔️ Recommended</span></span></td>
        <td><span data-ttu-id="0127b-123">✔️ Recommandé</span><span class="sxs-lookup"><span data-stu-id="0127b-123">✔️ Recommended</span></span></td>
        <td><span data-ttu-id="0127b-124">✔️ Recommandé</span><span class="sxs-lookup"><span data-stu-id="0127b-124">✔️ Recommended</span></span></td>
    </tr>
</table>


## <a name="design-principles"></a><span data-ttu-id="0127b-125">Principes de conception</span><span class="sxs-lookup"><span data-stu-id="0127b-125">Design principles</span></span>

<span data-ttu-id="0127b-126">**Évitez le « regard d’arme »**</span><span class="sxs-lookup"><span data-stu-id="0127b-126">**Avoid "Gaze as a weapon"**</span></span>

<span data-ttu-id="0127b-127">Pour être intuitif, le modèle Suivre de la tête et stabiliser nécessite un retour visuel, mais trop de retour peut engendrer de l’anxiété.</span><span class="sxs-lookup"><span data-stu-id="0127b-127">Head-gaze and dwell requires visual feedback to be intuitive, but too much feedback can induce anxiety.</span></span> <span data-ttu-id="0127b-128">Le retour doit aider l’utilisateur à savoir ce qu’il cible, sans sélectionner automatiquement l’objet concerné contre son gré.</span><span class="sxs-lookup"><span data-stu-id="0127b-128">The feedback should help a user know what they're targeting, but not auto-select it against their intent.</span></span> <span data-ttu-id="0127b-129">L’utilisateur étant amené à lire du texte, des étiquettes et des icônes, vous devez faire en sorte qu’il dispose d’un espace suffisant pour absorber les informations avant d’effectuer une sélection.</span><span class="sxs-lookup"><span data-stu-id="0127b-129">Reading text, icons, and labels requires extra consideration to provide a person room to absorb the information before selecting.</span></span>
    
<span data-ttu-id="0127b-130">**Rechercher la vitesse histoire**</span><span class="sxs-lookup"><span data-stu-id="0127b-130">**Seek Goldilocks speed**</span></span>
    
<span data-ttu-id="0127b-131">Les interactions avec stabilisation peuvent avoir différentes durées en fonction de l’impact de la navigation : les fonctions plus fréquemment utilisées bénéficient généralement de temps de remplissage plus rapides, tandis que les fonctions plus conséquentes peuvent bénéficier de temps de remplissage plus longs.</span><span class="sxs-lookup"><span data-stu-id="0127b-131">Dwell interactions can have different timers based on impact of navigation - more frequently used functions will generally benefit from faster fill times, while more consequential functions may benefit from longer fill times.</span></span> <span data-ttu-id="0127b-132">Quand vous utilisez un effet de remplissage pour afficher ces durées, les courbes d’animation de la couleur de remplissage peuvent engendrer un sentiment positif de temps de remplissage plus rapides.</span><span class="sxs-lookup"><span data-stu-id="0127b-132">When using a fill-effect to show these timers, animation curves of the fill color can positively influence a feeling of faster fill times.</span></span> <span data-ttu-id="0127b-133">Vous devez envisager de laisser à l’utilisateur la possibilité de choisir la vitesse de remplissage (rapide, moyenne, lente).</span><span class="sxs-lookup"><span data-stu-id="0127b-133">Consideration should be taken to enable user decision from fast/medium/slow fill speed overrides.</span></span>
    
<span data-ttu-id="0127b-134">**Dites non-non à Yo-Yo Effect**</span><span class="sxs-lookup"><span data-stu-id="0127b-134">**Say no-no to yo-yo effect**</span></span>

<span data-ttu-id="0127b-135">L’effet yo-yo est un schéma désagréable de mouvement de la tête qui peut émerger quand la position des contrôles de contenu et de suivi de la tête et de stabilisation oblige l’utilisateur à regarder vers le haut et vers le bas de façon répétée.</span><span class="sxs-lookup"><span data-stu-id="0127b-135">The yo-yo effect is an uncomfortable pattern of head movement that can emerge when the placement of content and head-gaze and dwell controls forces people to constantly look up and down repeatedly.</span></span> <span data-ttu-id="0127b-136">Par exemple, une liste de navigation avec le bouton en tête et le point d’interposition en bas de la liste donne une boucle de-regarde vers le bas, recherche les résultats, regarde jusqu’à son logement, etc. Ce modèle résultant est peu pratique et doit être évité en plaçant les contrôles de navigation dans un emplacement centralisé qui nécessite moins de sauvegarde et d’arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="0127b-136">For example, a list nav with the head-gaze and dwell button at the bottom induces a loop of - look down to dwell, look up at results, look down to dwell, etc. This resulting pattern is uncomfortable and should be avoided by placing navigation controls in a centralized location that requires less back-and-forth.</span></span> <span data-ttu-id="0127b-137">Le placement des boutons de stabilisation par rapport à leurs effets est important pour le confort.</span><span class="sxs-lookup"><span data-stu-id="0127b-137">Placement of dwell buttons relative to their effects becomes important for comfort.</span></span>

<br>

---


## <a name="ux-guidelines-and-best-practices"></a><span data-ttu-id="0127b-138">Recommandations et bonnes pratiques pour l’expérience utilisateur</span><span class="sxs-lookup"><span data-stu-id="0127b-138">UX Guidelines and best practices</span></span>

### <a name="target-sizes"></a><span data-ttu-id="0127b-139">Taille des cibles</span><span class="sxs-lookup"><span data-stu-id="0127b-139">Target sizes</span></span>
  <span data-ttu-id="0127b-140">Pour être facilement accessibles, les cibles du point de vue et du regard doivent être suffisamment grandes pour regarder confortablement et maintenir une tête stable sur la cible pour le temps imparti.</span><span class="sxs-lookup"><span data-stu-id="0127b-140">To be easily accessible, head-gaze and dwell targets need to be large enough to comfortably look at, and hold one's head stable on the target for the prescribed time.</span></span> <span data-ttu-id="0127b-141">Nous vous recommandons une taille de cible minimale de 2 degrés pour obtenir l’expérience la plus confortable.</span><span class="sxs-lookup"><span data-stu-id="0127b-141">We recommend a minimum target size of 2 degrees to achieve the most comfortable experience.</span></span> 

### <a name="visual-feedback"></a><span data-ttu-id="0127b-142">Retour visuel</span><span class="sxs-lookup"><span data-stu-id="0127b-142">Visual feedback</span></span>

<span data-ttu-id="0127b-143">Quand vous utilisez un remplissage radial pour représenter la durée de stabilisation, démarrez à partir du centre du bouton.</span><span class="sxs-lookup"><span data-stu-id="0127b-143">When using a radial fill to represent the dwell timer, start from the center of button.</span></span> <span data-ttu-id="0127b-144">Une réponse cohérente est plus claire que toutes les directions différentes sur les différents boutons.</span><span class="sxs-lookup"><span data-stu-id="0127b-144">A consistent response is less confusing than all different directions on different buttons.</span></span> 

  * <span data-ttu-id="0127b-145">Cette règle peut cependant être enfreinte pour les interactions directionnelles (par exemple, navigation vers le haut/bas/gauche/droite, etc.).</span><span class="sxs-lookup"><span data-stu-id="0127b-145">This rule can be broken though for directional interactions (e.g., nav up/down/left/right, etc.).</span></span> <span data-ttu-id="0127b-146">Par exemple, Microsoft Dynamics 365 Guides fait une exception pour SUIVANT/PRECEDENT qui correspond aux remplissages gauche et droite.</span><span class="sxs-lookup"><span data-stu-id="0127b-146">For example, Microsoft Dynamics 365 Guides makes an exception on NEXT/BACK being left right fills.</span></span>
  * <span data-ttu-id="0127b-147">Envisagez d’inverser le remplissage radial à partir de l’extérieur pour les scénarios tels que la désactivation d’un bouton.</span><span class="sxs-lookup"><span data-stu-id="0127b-147">Consider inverting radial fill from outside, for scenarios like toggling a button off.</span></span> <span data-ttu-id="0127b-148">Le sentiment inverse d’appui sur un bouton est un schéma visuel agréable à conserver.</span><span class="sxs-lookup"><span data-stu-id="0127b-148">The inverse feeling of pushing a button is a nice visual pattern to maintain.</span></span> 

### <a name="progressive-disclosure"></a><span data-ttu-id="0127b-149">Affichage progressif</span><span class="sxs-lookup"><span data-stu-id="0127b-149">Progressive disclosure</span></span>

<span data-ttu-id="0127b-150">L’affichage progressif consiste à n’afficher que les informations pertinentes à chaque étape d’une interaction.</span><span class="sxs-lookup"><span data-stu-id="0127b-150">Progressive disclosure means only showing as much detail as is relevant at each stage of an interaction.</span></span> <span data-ttu-id="0127b-151">Pour la stabilisation, cela signifie que la cible de stabilisation est affichée au moment de la mise en surbrillance (par exemple, dans un contrôle de liste).</span><span class="sxs-lookup"><span data-stu-id="0127b-151">For dwell, that means the dwell target is revealed on highlight (e.g., in a list control).</span></span>

 ### <a name="oversized-targets"></a><span data-ttu-id="0127b-152">Cibles trop grandes</span><span class="sxs-lookup"><span data-stu-id="0127b-152">Oversized targets</span></span>
<span data-ttu-id="0127b-153">La région de stabilisation peut être plus grande que l’icône à l’état inactif pour faciliter son utilisation, comme le bouton Précédent dans Microsoft Dynamics 365 Guides.</span><span class="sxs-lookup"><span data-stu-id="0127b-153">Dwell region can be larger than inactive icon to make it easier to use, like the Back button in Microsoft Dynamics 365 Guides.</span></span>

### <a name="prevent-flickering-with-delayed-feedback"></a><span data-ttu-id="0127b-154">Éviter le scintillement avec un retour décalé</span><span class="sxs-lookup"><span data-stu-id="0127b-154">Prevent flickering with delayed feedback</span></span>
<span data-ttu-id="0127b-155">Utilisez un court délai avant de démarrer le retour visuel afin d’éviter le scintillement quand l’utilisateur passe au-dessus d’une cible de stabilisation.</span><span class="sxs-lookup"><span data-stu-id="0127b-155">Use a short delay before starting visual feedback to avoid flickering when someone passes over a dwell target.</span></span>
* <span data-ttu-id="0127b-156">Pour les boutons qui sont interactifs fréquemment, laissez le délai très bref pour que l’application soit réactive.</span><span class="sxs-lookup"><span data-stu-id="0127b-156">For buttons interacted with frequently, keep the delay very short so the application feels reactive.</span></span>
* <span data-ttu-id="0127b-157">Pour les boutons qui sont interactifs rarement, un délai plus long peut être approprié pour éviter que l’interface twitchy.</span><span class="sxs-lookup"><span data-stu-id="0127b-157">For buttons that are interacted with infrequently, a longer delay can be appropriate to avoid the interface feeling twitchy.</span></span>


<br>

---

## <a name="ui-patterns"></a><span data-ttu-id="0127b-158">Schémas de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="0127b-158">UI patterns</span></span>

### <a name="high-frequency-buttons"></a><span data-ttu-id="0127b-159">Boutons à haute fréquence</span><span class="sxs-lookup"><span data-stu-id="0127b-159">High frequency buttons</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="0127b-160">Les boutons à fréquence élevée sont des boutons utilisés couramment dans une application.</span><span class="sxs-lookup"><span data-stu-id="0127b-160">High frequency buttons are buttons that are used commonly throughout an application.</span></span> <span data-ttu-id="0127b-161">Les boutons Suivant et Précédent dans Microsoft Dynamics 365 Guides constituent un bon exemple.</span><span class="sxs-lookup"><span data-stu-id="0127b-161">A good example of these are the next and back buttons in Microsoft Dynamics 365 Guides.</span></span><br>
        <br>
        <span data-ttu-id="0127b-162">**Relatives**</span><span class="sxs-lookup"><span data-stu-id="0127b-162">**Recommendations**</span></span><br>
  * <span data-ttu-id="0127b-163">Les boutons à fréquence élevée doivent être volumineux, plus faciles à toucher avec le regard</span><span class="sxs-lookup"><span data-stu-id="0127b-163">High frequency buttons should be large, easier to hit with head-gaze</span></span>
  * <span data-ttu-id="0127b-164">Restez près de la hauteur pour éviter les tensions ergonomiques.</span><span class="sxs-lookup"><span data-stu-id="0127b-164">Stay near eye height to avoid ergonomic straining.</span></span><br>
        <br>
<span data-ttu-id="0127b-165">*Image : Microsoft Dynamics 365 guides Next Button*</span><span class="sxs-lookup"><span data-stu-id="0127b-165">*Image: Microsoft Dynamics 365 Guides next button*</span></span>
    :::column-end:::
        :::column:::
       ![Bouton suivant de Microsoft Dynamics 365 guides](images/GuideNextButton.png)<br>
    :::column-end:::
:::row-end:::

<br>

---


### <a name="low-frequency-buttons"></a><span data-ttu-id="0127b-167">Boutons à fréquence faible</span><span class="sxs-lookup"><span data-stu-id="0127b-167">Low frequency buttons</span></span>
<span data-ttu-id="0127b-168">Les boutons à fréquence faible sont les boutons avec lesquels l’utilisateur n’interagit pas aussi régulièrement tout au long de l’application.</span><span class="sxs-lookup"><span data-stu-id="0127b-168">Low frequency buttons are buttons that are not interacted with as regularly throughout the application.</span></span> <span data-ttu-id="0127b-169">À titre d’exemple, citons un bouton permettant d’accéder à un menu de paramètres ou d’effacer la totalité du travail.</span><span class="sxs-lookup"><span data-stu-id="0127b-169">A good example might be a button to access the settings menu, or a button to clear all work.</span></span>

* <span data-ttu-id="0127b-170">Dans la mesure du possible, maintenez ces boutons hors du chemin emprunté par les suivis de la tête afin d’éviter une activation accidentelle.</span><span class="sxs-lookup"><span data-stu-id="0127b-170">Try to keep these buttons out of the way of frequent head-gaze paths to avoid accidental activation.</span></span> 

<br>

---

### <a name="confirmations"></a><span data-ttu-id="0127b-171">Confirmations</span><span class="sxs-lookup"><span data-stu-id="0127b-171">Confirmations</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="0127b-172">Quand une action a un impact significatif, telle que le prélèvement d’une somme d’argent, la suppression d’un travail ou le démarrage d’un long processus, il est utile de vérifier que l’utilisateur a effectivement souhaité sélectionner le bouton lié à cette action.</span><span class="sxs-lookup"><span data-stu-id="0127b-172">When an action has significant impact, like charging money, deleting work, or starting a long process, it is useful to confirm that a person meant to select a button.</span></span><br>
        <br>
        <span data-ttu-id="0127b-173">**Relatives**</span><span class="sxs-lookup"><span data-stu-id="0127b-173">**Recommendations**</span></span><br>
  * <span data-ttu-id="0127b-174">Afficher la surbrillance de la sélection sur le bouton principal</span><span class="sxs-lookup"><span data-stu-id="0127b-174">Show selection highlight on main button.</span></span>
  * <span data-ttu-id="0127b-175">Révéler la cible de stabilisation en même temps que la surbrillance de la sélection</span><span class="sxs-lookup"><span data-stu-id="0127b-175">Reveal dwell target at same time as selection highlight.</span></span>
  * <span data-ttu-id="0127b-176">Pour le bouton secondaire, révéler la cible de stabilisation en fonction du suivi de la tête</span><span class="sxs-lookup"><span data-stu-id="0127b-176">For the secondary button, reveal the dwell target on head-gaze.</span></span><br>
        <br>
<span data-ttu-id="0127b-177">*Image : boîte de dialogue de confirmation des guides Microsoft Dynamics 365*</span><span class="sxs-lookup"><span data-stu-id="0127b-177">*Image: Microsoft Dynamics 365 Guides confirmation dialog*</span></span>
    :::column-end:::
        :::column:::
       ![Boîte de dialogue de confirmation des guides Microsoft Dynamics 365](images/GuidesConfirmation.png)<br>
    :::column-end:::
:::row-end:::
        
<br>

---

### <a name="toggle-buttons"></a><span data-ttu-id="0127b-179">Boutons bascule</span><span class="sxs-lookup"><span data-stu-id="0127b-179">Toggle buttons</span></span>
<span data-ttu-id="0127b-180">Les boutons bascule nécessitent une logique nuancée pour fonctionner correctement.</span><span class="sxs-lookup"><span data-stu-id="0127b-180">Toggle buttons require some nuanced logic to work properly.</span></span> <span data-ttu-id="0127b-181">Quand l’utilisateur reste sur un bouton bascule et l’active, il doit quitter le bouton, puis revenir pour redémarrer la logique de stabilisation.</span><span class="sxs-lookup"><span data-stu-id="0127b-181">When a person dwells on a toggle button and actives it, they need to exit the button and then return to restart the dwell logic.</span></span> <span data-ttu-id="0127b-182">Il est important que l’utilisateur puisse clairement identifier si un bouton bascule est à l’état actif ou inactif.</span><span class="sxs-lookup"><span data-stu-id="0127b-182">It is important that togglable buttons have a clear active versus inactive state.</span></span> 

<br>

---

### <a name="list-views"></a><span data-ttu-id="0127b-183">Affichages Liste</span><span class="sxs-lookup"><span data-stu-id="0127b-183">List views</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="0127b-184">Les affichages de liste présentent un défi particulier pour les entrées de point de vue et de point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="0127b-184">List views present a particular challenge for head-gaze and dwell input.</span></span> <span data-ttu-id="0127b-185">L’utilisateur doit être en mesure de balayer le contenu sans avoir le sentiment de devoir tâtonner autour des cibles de stabilisation.</span><span class="sxs-lookup"><span data-stu-id="0127b-185">People need to be able to scan the content without feeling like that have to tiptoe around the dwell targets.</span></span><br>
        <br>
<span data-ttu-id="0127b-186">**Relatives**</span><span class="sxs-lookup"><span data-stu-id="0127b-186">**Recommendations**</span></span><br>
  * <span data-ttu-id="0127b-187">Faites en sorte que la totalité de la ligne surbrille quand la tête est en regard, mais ne commence pas, sauf si le point de regard se trouve sur la cible d’un logement spécifique.</span><span class="sxs-lookup"><span data-stu-id="0127b-187">Have the entire row highlight when head-gazed but doesn’t begin dwell unless head-gaze is on the specific dwell target.</span></span>
  * <span data-ttu-id="0127b-188">Affichez uniquement la cible d’un logement lorsque la ligne est mise en surbrillance pour réduire le bruit visuel.</span><span class="sxs-lookup"><span data-stu-id="0127b-188">Only show the dwell target when the row is highlighted to cut down on visual noise.</span></span>
  * <span data-ttu-id="0127b-189">Soyez clair et cohérent avec la position des cibles du logement.</span><span class="sxs-lookup"><span data-stu-id="0127b-189">Be clear and consistent with the position of dwell targets.</span></span>
  * <span data-ttu-id="0127b-190">N’affichez pas toutes les cibles de logement à la fois pour éviter l’interface utilisateur répétitive.</span><span class="sxs-lookup"><span data-stu-id="0127b-190">Don't show all dwell targets at once to avoid repetitive UI.</span></span>
  * <span data-ttu-id="0127b-191">Réutilisez le même modèle aussi souvent que possible pour établir une familiarité avec l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0127b-191">Re-use the same pattern as often as possible to establish UX familiarity.</span></span><br>
        <br>
<span data-ttu-id="0127b-192">*Image : liste des guides Microsoft Dynamics 365*</span><span class="sxs-lookup"><span data-stu-id="0127b-192">*Image: Microsoft Dynamics 365 Guides list*</span></span>
    :::column-end:::
        :::column:::
       ![Liste des guides Microsoft Dynamics 365](images/GuidesListView.png)<br>
    :::column-end:::
:::row-end:::

<br>

---
 
 ## <a name="see-also"></a><span data-ttu-id="0127b-194">Articles associés</span><span class="sxs-lookup"><span data-stu-id="0127b-194">See also</span></span>
* [<span data-ttu-id="0127b-195">Point de regard et validation</span><span class="sxs-lookup"><span data-stu-id="0127b-195">Gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="0127b-196">Manipulation directe</span><span class="sxs-lookup"><span data-stu-id="0127b-196">Hands - Direct manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="0127b-197">Mouvements pratiques</span><span class="sxs-lookup"><span data-stu-id="0127b-197">Hands - Gestures</span></span>](gaze-and-commit.md#composite-gestures)
* [<span data-ttu-id="0127b-198">Mains et validation</span><span class="sxs-lookup"><span data-stu-id="0127b-198">Hands - Point and commit</span></span>](point-and-commit.md)
* [<span data-ttu-id="0127b-199">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="0127b-199">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="0127b-200">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="0127b-200">Voice input</span></span>](voice-input.md)
