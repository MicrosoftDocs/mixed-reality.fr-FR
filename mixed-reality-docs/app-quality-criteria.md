---
title: Critères de qualité des applications
description: Ce document décrit les principaux facteurs ayant un impact sur la qualité des applications de réalité mixte.
author: cjdgit
ms.author: crderr
ms.date: 03/21/2018
ms.topic: article
keywords: critères de qualité des applications, une réalité, mixte mixte des applications en réalité
ms.openlocfilehash: 8070a434be462a636b314527c59f299ca77fb6d4
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595482"
---
# <a name="app-quality-criteria"></a><span data-ttu-id="8c34d-104">Critères de qualité des applications</span><span class="sxs-lookup"><span data-stu-id="8c34d-104">App quality criteria</span></span>

<span data-ttu-id="8c34d-105">Ce document décrit les principaux facteurs ayant un impact sur la qualité des applications de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="8c34d-105">This document describes the top factors impacting the quality of mixed reality apps.</span></span> <span data-ttu-id="8c34d-106">Pour chaque facteur les informations suivantes sont fournies</span><span class="sxs-lookup"><span data-stu-id="8c34d-106">For each factor the following information is provided</span></span>
* <span data-ttu-id="8c34d-107">Vue d’ensemble : une brève description du facteur de qualité et pourquoi il est important.</span><span class="sxs-lookup"><span data-stu-id="8c34d-107">Overview – a brief description of the quality factor and why it is important.</span></span>
* <span data-ttu-id="8c34d-108">Impact de l’appareil - type d’appareil de réalité mixte de fenêtre est affectée.</span><span class="sxs-lookup"><span data-stu-id="8c34d-108">Device impact - which type of Window Mixed Reality device is impacted.</span></span>
* <span data-ttu-id="8c34d-109">Critères de qualité – comment évaluer le facteur de qualité.</span><span class="sxs-lookup"><span data-stu-id="8c34d-109">Quality criteria – how to evaluate the quality factor.</span></span>
* <span data-ttu-id="8c34d-110">Comment mesurer : méthodes pour mesurer le problème (ou l’expérience).</span><span class="sxs-lookup"><span data-stu-id="8c34d-110">How to measure – methods to measure (or experience) the issue.</span></span>
* <span data-ttu-id="8c34d-111">Recommandations : résumées des approches pour fournir une meilleure expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-111">Recommendations – summary of approaches to provide a better user experience.</span></span>
* <span data-ttu-id="8c34d-112">Ressources – développement pertinentes et les ressources de conception qui sont utiles pour créer de meilleures expériences d’application.</span><span class="sxs-lookup"><span data-stu-id="8c34d-112">Resources – relevant developer and design resources that are useful to create better app experiences.</span></span>

## <a name="frame-rate"></a><span data-ttu-id="8c34d-113">Fréquence d’images</span><span class="sxs-lookup"><span data-stu-id="8c34d-113">Frame rate</span></span>

<span data-ttu-id="8c34d-114">Fréquence d’images est le premier pilier de confort de la stabilité et l’utilisateur hologramme.</span><span class="sxs-lookup"><span data-stu-id="8c34d-114">Frame rate is the first pillar of hologram stability and user comfort.</span></span> <span data-ttu-id="8c34d-115">Fréquence d’images ci-dessous les cibles recommandées peut provoquer hologrammes apparaisse instable, un impact négatif sur le believability de l’expérience et ce qui peut entraîner fatigue des yeux.</span><span class="sxs-lookup"><span data-stu-id="8c34d-115">Frame rate below the recommended targets can cause holograms to appear jittery, negatively impacting the believability of the experience and potentially causing eye fatigue.</span></span> <span data-ttu-id="8c34d-116">La fréquence d’images cible pour votre expérience sur des casques IMMERSIFS Windows Mixed Reality sera soit 60 ou 90Hz selon les PC compatibles Windows mixte réalité que vous souhaitez prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="8c34d-116">The target frame rate for your experience on Windows Mixed Reality immersive headsets will be either 60Hz or 90Hz depending on which Windows Mixed Reality Compatible PCs you wish to support.</span></span> <span data-ttu-id="8c34d-117">Pour HoloLens la fréquence d’images cible est de 60Hz.</span><span class="sxs-lookup"><span data-stu-id="8c34d-117">For HoloLens the target frame rate is 60Hz.</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-118">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-118">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-119"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-119"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-120"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-120"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-121">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-121">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="8c34d-122">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-122">✔️</span></span></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-123">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-123">Quality criteria</span></span>

|  <span data-ttu-id="8c34d-124">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-124">Best</span></span>  |  <span data-ttu-id="8c34d-125">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-125">Meets</span></span> |  <span data-ttu-id="8c34d-126">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-126">Fail</span></span> |
--- | --- | ---
| <span data-ttu-id="8c34d-127">L’application satisfait régulièrement les images par le deuxième objectif (i/s) pour l’appareil cible : 60 i/s sur HoloLens ; 90 i/s sur les PC Ultra ; et 60 i/s sur les PC grand public.</span><span class="sxs-lookup"><span data-stu-id="8c34d-127">The app consistently meets frames per second (FPS) goal for target device: 60fps on HoloLens; 90fps on Ultra PCs; and 60fps on mainstream PCs.</span></span> | <span data-ttu-id="8c34d-128">L’application a gouttes de frame intermittents ne pas entraver l’expérience core ; ou i/s est systématiquement inférieurs à l’objectif souhaité, mais n’entrave pas l’expérience de l’application.</span><span class="sxs-lookup"><span data-stu-id="8c34d-128">The app has intermittent frame drops not impeding the core experience; or FPS is consistently lower than desired goal but doesn’t impede the app experience.</span></span> | <span data-ttu-id="8c34d-129">L’application rencontre une chute de la fréquence d’images en moyenne de toutes les dix secondes ou moins.</span><span class="sxs-lookup"><span data-stu-id="8c34d-129">The app is experiencing a drop in frame rate on average every ten seconds or less.</span></span> |

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-130">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-130">How to measure</span></span>

* <span data-ttu-id="8c34d-131">Un graphique de taux de frame en temps réel est fourni par le biais par la [Windows Device Portal](using-the-windows-device-portal.md#system-performance) sous « Performances du système ».</span><span class="sxs-lookup"><span data-stu-id="8c34d-131">A real-time frame rate graph is provided through by the [Windows Device Portal](using-the-windows-device-portal.md#system-performance) under "System Performance".</span></span>
* <span data-ttu-id="8c34d-132">Pour le débogage de développement, ajoutez un compteur de diagnostic de taux de trames dans l’application.</span><span class="sxs-lookup"><span data-stu-id="8c34d-132">For development debugging, add a frame rate diagnostic counter into the app.</span></span> <span data-ttu-id="8c34d-133">Consultez les ressources pour un exemple de compteur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-133">See Resources for a sample counter.</span></span>
* <span data-ttu-id="8c34d-134">Supprime des taux de cadre peut être testées dans l’appareil pendant l’exécution de l’application en déplaçant votre tête de gauche à droite.</span><span class="sxs-lookup"><span data-stu-id="8c34d-134">Frame rate drops can be experienced in device while the app is running by moving your head from side to side.</span></span> <span data-ttu-id="8c34d-135">Si l’hologramme indique un mouvement instable inattendu, basse fréquence d’images ou le plan de la stabilité est probablement la cause.</span><span class="sxs-lookup"><span data-stu-id="8c34d-135">If the hologram shows unexpected jittery movement, then low frame rate or the stability plane is likely the cause.</span></span>

### <a name="recommendations"></a><span data-ttu-id="8c34d-136">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-136">Recommendations</span></span>

* <span data-ttu-id="8c34d-137">Ajouter un compteur de taux de trames au début du travail de développement.</span><span class="sxs-lookup"><span data-stu-id="8c34d-137">Add a frame rate counter at the beginning of the development work.</span></span>
* <span data-ttu-id="8c34d-138">Les modifications qui peuvent entraîner une baisse de la fréquence d’images doivent être évaluées et correctement résolues comme un bogue de performances.</span><span class="sxs-lookup"><span data-stu-id="8c34d-138">Changes that incur a drop in frame rate should be evaluated and appropriately resolved as a performance bug.</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-139">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-139">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="8c34d-140">Documentation</span><span class="sxs-lookup"><span data-stu-id="8c34d-140">Documentation</span></span>

* [<span data-ttu-id="8c34d-141">Comprendre les performances pour la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="8c34d-141">Understanding Performance for Mixed Reality</span></span>](understanding-performance-for-mixed-reality.md)
* [<span data-ttu-id="8c34d-142">Fréquence d’images et la stabilité HOLOGRAMME</span><span class="sxs-lookup"><span data-stu-id="8c34d-142">Hologram stability and framerate</span></span>](hologram-stability.md#frame-rate)
* [<span data-ttu-id="8c34d-143">Budget de performances Asset</span><span class="sxs-lookup"><span data-stu-id="8c34d-143">Asset performance budget</span></span>](asset-creation-process.md)
* [<span data-ttu-id="8c34d-144">Recommandations relatives aux performances pour Unity</span><span class="sxs-lookup"><span data-stu-id="8c34d-144">Performance recommendations for Unity</span></span>](performance-recommendations-for-unity.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="8c34d-145">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="8c34d-145">Tools and tutorials</span></span>

* [<span data-ttu-id="8c34d-146">Affichage du compteur MRToolkit, i/s</span><span class="sxs-lookup"><span data-stu-id="8c34d-146">MRToolkit, FPS counter display</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Utilities/README.md)
* [<span data-ttu-id="8c34d-147">MRToolkit, Shaders</span><span class="sxs-lookup"><span data-stu-id="8c34d-147">MRToolkit, Shaders</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Utilities/Shaders)

#### <a name="external-references"></a><span data-ttu-id="8c34d-148">Références externes</span><span class="sxs-lookup"><span data-stu-id="8c34d-148">External references</span></span>

* [<span data-ttu-id="8c34d-149">Unity, optimisation des applications mobiles</span><span class="sxs-lookup"><span data-stu-id="8c34d-149">Unity, Optimizing mobile applications</span></span>](https://www.youtube.com/watch?v=j4YAY36xjwE)

## <a name="hologram-stability"></a><span data-ttu-id="8c34d-150">Stabilité HOLOGRAMME</span><span class="sxs-lookup"><span data-stu-id="8c34d-150">Hologram stability</span></span>

<span data-ttu-id="8c34d-151">Hologrammes stables augmentera l’utilisation et believability de votre application et créer une expérience d’affichage plus à l’aise pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-151">Stable holograms will increase the usability and believability of your app, and create a more comfortable viewing experience for the user.</span></span> <span data-ttu-id="8c34d-152">La qualité de la stabilité hologramme est un résultat de développement de la bonne application et la capacité du périphérique (track) de comprendre son environnement.</span><span class="sxs-lookup"><span data-stu-id="8c34d-152">The quality of hologram stability is a result of good app development and the device's ability to understand (track) its environment.</span></span> <span data-ttu-id="8c34d-153">Tandis que la fréquence d’images est le premier pilier de la stabilité, d’autres facteurs peuvent avoir un impact sur la stabilité, y compris :</span><span class="sxs-lookup"><span data-stu-id="8c34d-153">While frame rate is the first pillar of stability, other factors can impact stability including:</span></span>

* <span data-ttu-id="8c34d-154">Utilisation du plan de stabilisation</span><span class="sxs-lookup"><span data-stu-id="8c34d-154">Use of the stabilization plane</span></span>
* <span data-ttu-id="8c34d-155">Distance et ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="8c34d-155">Distance to spatial anchors</span></span>
* <span data-ttu-id="8c34d-156">Suivi</span><span class="sxs-lookup"><span data-stu-id="8c34d-156">Tracking</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-157">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-157">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-158"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-158"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-159"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-159"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-160">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-160">✔️</span></span></td><td style="text-align: center;"></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-161">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-161">Quality criteria</span></span>

|  <span data-ttu-id="8c34d-162">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-162">Best</span></span>  |  <span data-ttu-id="8c34d-163">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-163">Meets</span></span> |  <span data-ttu-id="8c34d-164">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-164">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="8c34d-165">Hologrammes s’affichent régulièrement stables.</span><span class="sxs-lookup"><span data-stu-id="8c34d-165">Holograms consistently appear stable.</span></span> | <span data-ttu-id="8c34d-166">Contenu secondaire présente un mouvement inattendu ; ou un mouvement inattendu n’entrave pas l’expérience de l’application globale.</span><span class="sxs-lookup"><span data-stu-id="8c34d-166">Secondary content exhibits unexpected movement; or unexpected movement does not impede overall app experience.</span></span> | <span data-ttu-id="8c34d-167">Contenu principal dans le frame présente un mouvement inattendu.</span><span class="sxs-lookup"><span data-stu-id="8c34d-167">Primary content in frame exhibits unexpected movement.</span></span> |

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-168">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-168">How to measure</span></span>

<span data-ttu-id="8c34d-169">Tandis que le port de l’appareil et l’expérience d’affichage :</span><span class="sxs-lookup"><span data-stu-id="8c34d-169">While wearing the device and viewing the experience:</span></span>

* <span data-ttu-id="8c34d-170">Déplacer votre tête de gauche à droite, si les hologrammes affichent un mouvement inattendu basse fréquence d’images ou un alignement incorrect du plan de stabilité pour le plan focal est la cause probable.</span><span class="sxs-lookup"><span data-stu-id="8c34d-170">Move your head from side to side, if the holograms show unexpected movement then low frame rate or improper alignment of the stability plane to the focal plane is the likely cause.</span></span>
* <span data-ttu-id="8c34d-171">Déplacer l’environnement et hologrammes, rechercher des comportements tels que natation et jumpiness.</span><span class="sxs-lookup"><span data-stu-id="8c34d-171">Move around the holograms and environment, look for behaviors such as swim and jumpiness.</span></span> <span data-ttu-id="8c34d-172">Ce type de déplacement est probablement due à l’analyse de périphérique ne pas l’environnement, ou la distance à l’ancre spatial.</span><span class="sxs-lookup"><span data-stu-id="8c34d-172">This type of motion is likely caused by the device not tracking the environment, or the distance to the spatial anchor.</span></span>
* <span data-ttu-id="8c34d-173">Si de grands ou hologrammes plusieurs se trouvent dans le frame, observer le comportement de hologramme à différentes profondeurs tandis que le déplacement de votre position principale de gauche à droite, si tremblement apparaît cela est probablement causé par le plan de stabilisation.</span><span class="sxs-lookup"><span data-stu-id="8c34d-173">If large or multiple holograms are in the frame, observe hologram behavior at various depths while moving your head position from side to side, if shakiness appears this is likely caused by the stabilization plane.</span></span>

### <a name="recomendations"></a><span data-ttu-id="8c34d-174">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-174">Recomendations</span></span>

* <span data-ttu-id="8c34d-175">Ajouter un compteur de taux de trames au début du travail de développement.</span><span class="sxs-lookup"><span data-stu-id="8c34d-175">Add an frame rate counter at the beginning of the development work.</span></span>
* <span data-ttu-id="8c34d-176">Utilisez le plan de stabilisation.</span><span class="sxs-lookup"><span data-stu-id="8c34d-176">Use the stabilization plane.</span></span>
* <span data-ttu-id="8c34d-177">Toujours afficher hologrammes ancrés dans 3 mètres de leur point d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="8c34d-177">Always render anchored holograms within 3 meters of their anchor.</span></span>
* <span data-ttu-id="8c34d-178">Assurez-vous que votre environnement est configuré pour le suivi approprié.</span><span class="sxs-lookup"><span data-stu-id="8c34d-178">Make sure your environment is setup for proper tracking.</span></span>
* <span data-ttu-id="8c34d-179">Votre expérience afin d’éviter les hologrammes à différents niveaux de profondeur focal dans le cadre de la conception.</span><span class="sxs-lookup"><span data-stu-id="8c34d-179">Design your experience to avoid holograms at various focal depth levels within the frame.</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-180">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-180">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="8c34d-181">Documentation</span><span class="sxs-lookup"><span data-stu-id="8c34d-181">Documentation</span></span>

* [<span data-ttu-id="8c34d-182">Fréquence d’images et la stabilité HOLOGRAMME</span><span class="sxs-lookup"><span data-stu-id="8c34d-182">Hologram stability and framerate</span></span>](hologram-stability.md#frame-rate)
* [<span data-ttu-id="8c34d-183">Étude de cas, à l’aide du plan de stabilisation</span><span class="sxs-lookup"><span data-stu-id="8c34d-183">Case study, Using the stabilization plane</span></span>](case-study-using-the-stabilization-plane-to-reduce-holographic-turbulence.md)
* [<span data-ttu-id="8c34d-184">Comprendre les performances pour la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="8c34d-184">Understanding Performance for Mixed Reality</span></span>](understanding-performance-for-mixed-reality.md)
* [<span data-ttu-id="8c34d-185">Recommandations relatives aux performances pour Unity</span><span class="sxs-lookup"><span data-stu-id="8c34d-185">Performance recommendations for Unity</span></span>](performance-recommendations-for-unity.md)
* [<span data-ttu-id="8c34d-186">Ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="8c34d-186">Spatial anchors</span></span>](spatial-anchors.md)
* [<span data-ttu-id="8c34d-187">Gestion des erreurs de suivi</span><span class="sxs-lookup"><span data-stu-id="8c34d-187">Handling tracking errors</span></span>](coordinate-systems.md#handling-tracking-errors)
* [<span data-ttu-id="8c34d-188">Système de référence stationnaire</span><span class="sxs-lookup"><span data-stu-id="8c34d-188">Stationary frame of reference</span></span>](coordinate-systems.md#stationary-frame-of-reference)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="8c34d-189">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="8c34d-189">Tools and tutorials</span></span>

* [<span data-ttu-id="8c34d-190">Kit d’accompagnement MR, Kinect IPD</span><span class="sxs-lookup"><span data-stu-id="8c34d-190">MR Companion Kit, Kinect IPD</span></span>](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/KinectIPD)

## <a name="holograms-position-on-real-surfaces"></a><span data-ttu-id="8c34d-191">Position hologrammes sur des surfaces réels</span><span class="sxs-lookup"><span data-stu-id="8c34d-191">Holograms position on real surfaces</span></span>

<span data-ttu-id="8c34d-192">Distorsions de hologrammes avec des objets physiques (si destinés à être mis en relation avec eux) est une indication claire de l’union de hologrammes et réalistes.</span><span class="sxs-lookup"><span data-stu-id="8c34d-192">Misalignments of holograms with physical objects (if intended to be placed in relation to one another) is a clear indication of the non-union of holograms and real-world.</span></span> <span data-ttu-id="8c34d-193">Précision de l’emplacement doit être par rapport aux besoins du scénario ; par exemple, placement surface général peut utiliser le mappage spatial, mais plus précise placement nécessitera certains utilisation de marqueurs et d’étalonnage.</span><span class="sxs-lookup"><span data-stu-id="8c34d-193">Accuracy of the placement should be relative to the needs of the scenario; for example, general surface placement can use the spatial map, but more accurate placement will require some use of markers and calibration.</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-194">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-194">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-195"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-195"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-196"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-196"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-197">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-197">✔️</span></span></td><td style="text-align: center;"></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-198">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-198">Quality criteria</span></span>

|  <span data-ttu-id="8c34d-199">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-199">Best</span></span>  |  <span data-ttu-id="8c34d-200">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-200">Meets</span></span> |  <span data-ttu-id="8c34d-201">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-201">Fail</span></span> |
--- | --- | ---
| <span data-ttu-id="8c34d-202">Hologrammes alignent sur la surface en général dans les centimètres à pouces plage.</span><span class="sxs-lookup"><span data-stu-id="8c34d-202">Holograms align to the surface typically in the centimeters to inches range.</span></span> <span data-ttu-id="8c34d-203">Si plus de précision est requise, l’application doit fournir un moyen efficace pour la collaboration au sein de la spécification de l’application souhaitée.</span><span class="sxs-lookup"><span data-stu-id="8c34d-203">If more accuracy is required, the app should provide an efficient means for collaboration within the desired app spec.</span></span> | <span data-ttu-id="8c34d-204">N/A</span><span class="sxs-lookup"><span data-stu-id="8c34d-204">NA</span></span> | <span data-ttu-id="8c34d-205">Les hologrammes apparaissent non alignés avec l’objet cible physique par rompre le plan de surface ou qui apparaissent pour les faire flotter en dehors de la surface.</span><span class="sxs-lookup"><span data-stu-id="8c34d-205">The holograms appear unaligned with the physical target object by either breaking the surface plane or appearing to float away from the surface.</span></span> <span data-ttu-id="8c34d-206">Si l’exactitude est requis, hologrammes doivent répondre à la spécification de la proximité du scénario.</span><span class="sxs-lookup"><span data-stu-id="8c34d-206">If accuracy is required, Holograms should meet the proximity spec of the scenario.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-207">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-207">How to measure</span></span>

* <span data-ttu-id="8c34d-208">Hologrammes sont placés sur la carte spatial ne doivent pas apparaître considérablement flotter au-dessus ou au-dessous de la surface.</span><span class="sxs-lookup"><span data-stu-id="8c34d-208">Holograms that are placed on spatial map should not appear to dramatically float above or below the surface.</span></span>
* <span data-ttu-id="8c34d-209">Hologrammes qui nécessitent le positionnement précis doivent avoir une forme de marqueur et système d’étalonnage adaptée aux besoins du scénario le.</span><span class="sxs-lookup"><span data-stu-id="8c34d-209">Holograms that require accurate placement should have some form of marker and calibration system that is accurate to the scenario's requirement.</span></span>

### <a name="recommendations"></a><span data-ttu-id="8c34d-210">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-210">Recommendations</span></span>

* <span data-ttu-id="8c34d-211">Mappage spatial est utile pour placer des objets sur des surfaces lors de la précision n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8c34d-211">Spatial map is useful for placing objects on surfaces when precision isn’t required.</span></span>
* <span data-ttu-id="8c34d-212">La meilleure précision, utiliser marqueurs ou des affiches pour déterminer les hologrammes et une manette Xbox (ou un mécanisme d’alignement manuel) d’étalonnage finale.</span><span class="sxs-lookup"><span data-stu-id="8c34d-212">For the best precision, use markers or posters to set the holograms and an Xbox controller (or some manual alignment mechanism) for final calibration.</span></span>
* <span data-ttu-id="8c34d-213">Envisagez de diviser hologrammes de très grande taille en parties logiques et d’alignement de chaque partie vers l’aire.</span><span class="sxs-lookup"><span data-stu-id="8c34d-213">Consider breaking extra-large holograms into logical parts and aligning each part to the surface.</span></span>
* <span data-ttu-id="8c34d-214">Mal ensemble interpupilary distance (IPD) peut également un effet sur les alignement hologramme.</span><span class="sxs-lookup"><span data-stu-id="8c34d-214">Improperly set interpupilary distance (IPD) can also effect hologram alignment.</span></span> <span data-ttu-id="8c34d-215">Configurez toujours HoloLens à IPD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-215">Always configure HoloLens to the user's IPD.</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-216">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-216">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="8c34d-217">Documentation</span><span class="sxs-lookup"><span data-stu-id="8c34d-217">Documentation</span></span>

* [<span data-ttu-id="8c34d-218">Placement de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="8c34d-218">Spatial mapping placement</span></span>](spatial-mapping.md#placement)
* [<span data-ttu-id="8c34d-219">Espace de processus d’analyse</span><span class="sxs-lookup"><span data-stu-id="8c34d-219">Room scanning process</span></span>](case-study-expanding-the-spatial-mapping-capabilities-of-hololens.md)
* [<span data-ttu-id="8c34d-220">Meilleures pratiques d’ancres spatial</span><span class="sxs-lookup"><span data-stu-id="8c34d-220">Spatial anchors best practices</span></span>](spatial-anchors.md#best-practices)
* [<span data-ttu-id="8c34d-221">Gestion des erreurs de suivi</span><span class="sxs-lookup"><span data-stu-id="8c34d-221">Handling tracking errors</span></span>](coordinate-systems.md#handling-tracking-errors)
* [<span data-ttu-id="8c34d-222">Mappage spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="8c34d-222">Spatial mapping in Unity</span></span>](spatial-mapping-in-unity.md)
* [<span data-ttu-id="8c34d-223">Vue d’ensemble du développement Vuforia</span><span class="sxs-lookup"><span data-stu-id="8c34d-223">Vuforia development overview</span></span>](vuforia-development-overview.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="8c34d-224">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="8c34d-224">Tools and tutorials</span></span>

* [<span data-ttu-id="8c34d-225">MR 230 spatiale : Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="8c34d-225">MR Spatial 230: Spatial mapping</span></span>](holograms-230.md)
* [<span data-ttu-id="8c34d-226">MR boîte à outils, bibliothèques de mappage Spatial</span><span class="sxs-lookup"><span data-stu-id="8c34d-226">MR Toolkit, Spatial Mapping Libraries</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/SpatialMapping/README.md)
* [<span data-ttu-id="8c34d-227">Kit de Compagnon MR, exemple d’étalonnage de Poster</span><span class="sxs-lookup"><span data-stu-id="8c34d-227">MR Companion Kit, Poster Calibration Sample</span></span>](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/PosterCalibrationSample)
* [<span data-ttu-id="8c34d-228">Kit d’accompagnement MR, Kinect IPD</span><span class="sxs-lookup"><span data-stu-id="8c34d-228">MR Companion Kit, Kinect IPD</span></span>](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/KinectIPD)

#### <a name="external-references"></a><span data-ttu-id="8c34d-229">Références externes</span><span class="sxs-lookup"><span data-stu-id="8c34d-229">External references</span></span>

* [<span data-ttu-id="8c34d-230">Étude de cas Lowes, alignement de précision</span><span class="sxs-lookup"><span data-stu-id="8c34d-230">Lowes Case Study, Precision alignment</span></span>](https://www.youtube.com/watch?v=LceMdyKZ4PI)

## <a name="viewing-zone-of-comfort"></a><span data-ttu-id="8c34d-231">Zone d’affichage de confort</span><span class="sxs-lookup"><span data-stu-id="8c34d-231">Viewing zone of comfort</span></span>

<span data-ttu-id="8c34d-232">Contrôle les développeurs d’applications où les yeux des utilisateurs convergent en plaçant le contenu et hologrammes à des profondeurs différents.</span><span class="sxs-lookup"><span data-stu-id="8c34d-232">App developers control where users' eyes converge by placing content and holograms at various depths.</span></span> <span data-ttu-id="8c34d-233">Les utilisateurs qui HoloLens inclura toujours à m 2.0 pour maintenir une image claire, car HoloLens affiche sont fixés à une distance optique environ 2.0m éloignée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-233">Users wearing HoloLens will always accommodate to 2.0m to maintain a clear image because HoloLens displays are fixed at an optical distance approximately 2.0m away from the user.</span></span> <span data-ttu-id="8c34d-234">Profondeur de contenu incorrecte peut entraîner une gêne visual ou fatigue.</span><span class="sxs-lookup"><span data-stu-id="8c34d-234">Improper content depth can lead to visual discomfort or fatigue.</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-235">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-235">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-236"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-236"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-237"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-237"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-238">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-238">✔️</span></span></td><td style="text-align: center;"></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-239">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-239">Quality criteria</span></span>

<table>
<tr>
<td> <span data-ttu-id="8c34d-240">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-240">Best</span></span> </td><td><ul>
<li><span data-ttu-id="8c34d-241">Placer le contenu à 2m.</span><span class="sxs-lookup"><span data-stu-id="8c34d-241">Place content at 2m.</span></span></li><li><span data-ttu-id="8c34d-242">Lorsque hologrammes ne peut pas être placés au 2m et les conflits entre convergence et d’hébergement ne peut pas être évitées, la zone optimale pour la sélection élective hologramme est entre 1,25 m et 5m.</span><span class="sxs-lookup"><span data-stu-id="8c34d-242">When holograms cannot be placed at 2m and conflicts between convergence and accommodation cannot be avoided, the optimal zone for hologram placement is between 1.25m and 5m.</span></span></li><li><span data-ttu-id="8c34d-243">Dans tous les cas, les concepteurs doivent structurer le contenu à encourager les utilisateurs à interagir 1 + m (par exemple, ajuster la taille du contenu et les paramètres de sélection élective par défaut).</span><span class="sxs-lookup"><span data-stu-id="8c34d-243">In every case, designers should structure content to encourage users to interact 1+ m away (e.g. adjust content size and default placement parameters).</span></span></li><li><span data-ttu-id="8c34d-244">Sauf si spécifiquement ne pas requis par le scénario, un plan de découpage doit être implémentez avec fadeout en commençant à 1 million.</span><span class="sxs-lookup"><span data-stu-id="8c34d-244">Unless specifically not required by the scenario, a clipping plane should be implement with fadeout starting at 1m.</span></span></li><li><span data-ttu-id="8c34d-245">Dans les cas où une observation plus proche d’un hologramme immobile est requise, le contenu ne doit pas être à moins de 50cm.</span><span class="sxs-lookup"><span data-stu-id="8c34d-245">In cases where closer observation of a motionless hologram is required, the content should not be closer than 50cm.</span></span></li>
</ul></td>
</tr><tr>
<td> <span data-ttu-id="8c34d-246">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-246">Meets</span></span></td><td> <span data-ttu-id="8c34d-247">Contenu se trouve dans le Guide de visualisation et de mouvement, mais une utilisation incorrecte ou aucune utilisation du plan de découpage.</span><span class="sxs-lookup"><span data-stu-id="8c34d-247">Content is within the viewing and motion guidance, but improper use or no use of the clipping plane.</span></span></td>
</tr><tr>
<td> <span data-ttu-id="8c34d-248">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-248">Fail</span></span> </td><td> <span data-ttu-id="8c34d-249">Le contenu est présenté trop près (généralement &lt;1,25 m, ou &lt;50 cm pour hologrammes STATIONNAIRES nécessitant une observation plus proche.)</span><span class="sxs-lookup"><span data-stu-id="8c34d-249">Content is presented too close (typically &lt;1.25m, or &lt;50cm for stationary holograms requiring closer observation.)</span></span></td>
</tr>
</table>

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-250">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-250">How to measure</span></span>

* <span data-ttu-id="8c34d-251">Contenu doivent être généralement 2m absent, mais ne plus proche que 1,25 ou plus : optez 5m.</span><span class="sxs-lookup"><span data-stu-id="8c34d-251">Content should typically be 2m away, but no closer than 1.25 or further than 5m.</span></span>
* <span data-ttu-id="8c34d-252">À quelques exceptions près, la distance de rendu de découpage HoloLens doit être définie à .85CM avec fadeout du contenu, en commençant à 1 million.</span><span class="sxs-lookup"><span data-stu-id="8c34d-252">With few exceptions, the HoloLens clipping render distance should be set to .85CM with fadeout of content starting at 1m.</span></span> <span data-ttu-id="8c34d-253">Approche le contenu et notez l’effet de plan de découpage.</span><span class="sxs-lookup"><span data-stu-id="8c34d-253">Approach the content and note the clipping plane effect.</span></span>
* <span data-ttu-id="8c34d-254">Contenu stationnaire ne doit pas être à moins de 50cm de suite.</span><span class="sxs-lookup"><span data-stu-id="8c34d-254">Stationary content should not be closer than 50cm away.</span></span>

### <a name="recommendations"></a><span data-ttu-id="8c34d-255">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-255">Recommendations</span></span>

* <span data-ttu-id="8c34d-256">Concevoir le contenu de la distance d’optimiser l’affichage de 2m.</span><span class="sxs-lookup"><span data-stu-id="8c34d-256">Design content for the optimal viewing distance of 2m.</span></span>
* <span data-ttu-id="8c34d-257">Définit la distance de rendu de découpage à 85cm avec fadeout du contenu, en commençant à 1 million.</span><span class="sxs-lookup"><span data-stu-id="8c34d-257">Set the clipping render distance to 85cm with fadeout of content starting at 1m.</span></span>
* <span data-ttu-id="8c34d-258">Pour hologrammes STATIONNAIRES nécessitant l’affichage de plus près, le plan de découpage doit être non moins de 30 centimètres et fadeout doit commencer au moins 10cm en dehors du plan de découpage.</span><span class="sxs-lookup"><span data-stu-id="8c34d-258">For stationary holograms that need closer viewing, the clipping plane should be no closer than 30cm and fadeout should start at least 10cm away from the clipping plane.</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-259">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-259">Resources</span></span>

* [<span data-ttu-id="8c34d-260">Restituer la distance</span><span class="sxs-lookup"><span data-stu-id="8c34d-260">Render distance</span></span>](hologram-stability.md#hologram-render-distances)
* [<span data-ttu-id="8c34d-261">Point de focus dans Unity</span><span class="sxs-lookup"><span data-stu-id="8c34d-261">Focus point in Unity</span></span>](focus-point-in-unity.md)
* [<span data-ttu-id="8c34d-262">Expérimenter la mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="8c34d-262">Experimenting with scale</span></span>](scale.md#experimenting-with-scale)
* [<span data-ttu-id="8c34d-263">Texte, la taille de police recommandée</span><span class="sxs-lookup"><span data-stu-id="8c34d-263">Text, Recommended font size</span></span>](typography.md#recommended-font-size)

## <a name="depth-switching"></a><span data-ttu-id="8c34d-264">Profondeur de commutation</span><span class="sxs-lookup"><span data-stu-id="8c34d-264">Depth switching</span></span>

<span data-ttu-id="8c34d-265">Quelle que soit la zone d’affichage des problèmes de confort, les demandes de l’utilisateur de basculer rapidement ou fréquemment entre près et présent focal objets (y compris les hologrammes et contenu du monde réel) peuvent entraîner la fatigue oculomotor et de gêne générale.</span><span class="sxs-lookup"><span data-stu-id="8c34d-265">Regardless of viewing zone of comfort issues, demands for the user to switch frequently or quickly between near and far focal objects (including holograms and real-world content) can lead to oculomotor fatigue, and general discomfort.</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-266">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-266">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-267"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-267"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-268"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-268"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-269">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-269">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="8c34d-270">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-270">✔️</span></span></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-271">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-271">Quality criteria</span></span>

|  <span data-ttu-id="8c34d-272">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-272">Best</span></span>  |  <span data-ttu-id="8c34d-273">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-273">Meets</span></span> |  <span data-ttu-id="8c34d-274">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-274">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="8c34d-275">Profondeur limitée ou naturelle de commutation qui n’entraîne pas l’utilisateur peut se concentrer Queues.</span><span class="sxs-lookup"><span data-stu-id="8c34d-275">Limited or natural depth switching that doesn’t cause the user to unnaturally refocus.</span></span> | <span data-ttu-id="8c34d-276">Profondeur brusque commutateur core et conçu dans l’expérience de l’application, ou profondeur brusque qui est provoquée par le contenu réel inattendu.</span><span class="sxs-lookup"><span data-stu-id="8c34d-276">Abrupt depth switch this is core and designed into the app experience, or abrupt depth switch that is caused by unexpected real-world content.</span></span> | <span data-ttu-id="8c34d-277">Commutateur de profondeur cohérent, ou profondeur brusque changement qui n’est pas nécessaire ou core à l’expérience de l’application.</span><span class="sxs-lookup"><span data-stu-id="8c34d-277">Consistent depth switch, or abrupt depth switching that isn’t necessary or core to the app experience.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-278">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-278">How to measure</span></span>

* <span data-ttu-id="8c34d-279">Si l’application requiert l’utilisateur de manière cohérente et/ou brusquement définir le focus de profondeur, profondeur est problème de commutation.</span><span class="sxs-lookup"><span data-stu-id="8c34d-279">If the app requires the user to consistently and/or abruptly change depth focus, there is depth switching problem.</span></span>

### <a name="recommendations"></a><span data-ttu-id="8c34d-280">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-280">Recommendations</span></span>

* <span data-ttu-id="8c34d-281">Conserver le contenu principal à un plan focal cohérent et assurez-vous que le plan de stabilisation correspond à la focale.</span><span class="sxs-lookup"><span data-stu-id="8c34d-281">Keep primary content at a consistent focal plane and make sure the stabilization plane matches the focal plane.</span></span> <span data-ttu-id="8c34d-282">Cela résoudra oculomotor fatigue et déplacement des hologramme inattendue.</span><span class="sxs-lookup"><span data-stu-id="8c34d-282">This will alleviate oculomotor fatigue and unexpected hologram movement.</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-283">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-283">Resources</span></span>

* [<span data-ttu-id="8c34d-284">Restituer la distance</span><span class="sxs-lookup"><span data-stu-id="8c34d-284">Render distance</span></span>](hologram-stability.md#hologram-render-distances)
* [<span data-ttu-id="8c34d-285">Point de focus dans Unity</span><span class="sxs-lookup"><span data-stu-id="8c34d-285">Focus point in Unity</span></span>](focus-point-in-unity.md)

## <a name="use-of-spatial-sound"></a><span data-ttu-id="8c34d-286">Utilisation de son spatial</span><span class="sxs-lookup"><span data-stu-id="8c34d-286">Use of spatial sound</span></span>

<span data-ttu-id="8c34d-287">En réalité mixte de Windows, le moteur audio fournit le composant auditif de l’expérience de réalité mixte en simulant 3D audio à l’aide de la direction, la distance et les simulations de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="8c34d-287">In Windows Mixed Reality, the audio engine provides the aural component of the mixed reality experience by simulating 3D sound using direction, distance, and environmental simulations.</span></span> <span data-ttu-id="8c34d-288">À l’aide de son spatial dans une application permet aux développeurs de placer convaincante des sons dans un espace tridimensionnel 3 (sphère) autour de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-288">Using spatial sound in an application allows developers to convincingly place sounds in a 3 dimensional space (sphere) all around the user.</span></span> <span data-ttu-id="8c34d-289">Ces sons paraîtra comme si elles provenaient d’objets physiques réel ou les hologrammes de réalité mixte dans son environnement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-289">Those sounds will then seem as if they were coming from real physical objects or the mixed reality holograms in the user's surroundings.</span></span> <span data-ttu-id="8c34d-290">Son spatial est un outil puissant pour immersion, d’accessibilité et la conception de l’expérience utilisateur dans les applications de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="8c34d-290">Spatial sound is a powerful tool for immersion, accessibility, and UX design in mixed reality applications.</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-291">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-291">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-292"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-292"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-293"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-293"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-294">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-294">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="8c34d-295">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-295">✔️</span></span></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-296">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-296">Quality criteria</span></span>

|  <span data-ttu-id="8c34d-297">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-297">Best</span></span>  |  <span data-ttu-id="8c34d-298">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-298">Meets</span></span> |  <span data-ttu-id="8c34d-299">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-299">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="8c34d-300">Son est logiquement spatialized, et l’expérience utilisateur utilise correctement son afin de faciliter objet découverte et commentaires des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8c34d-300">Sound is logically spatialized, and the UX appropriately uses sound to assist with object discovery and user feedback.</span></span> <span data-ttu-id="8c34d-301">Son est naturel et pertinents aux objets et normalisée entre le scénario.</span><span class="sxs-lookup"><span data-stu-id="8c34d-301">Sound is natural and relevant to objects and normalized across the scenario.</span></span> | <span data-ttu-id="8c34d-302">Audio spatial est utilisé convenablement pour believability mais manquant comme moyen de faciliter la détectabilité et les commentaires des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8c34d-302">Spatial audio is used appropriately for believability but missing as means to help with user feedback and discoverability.</span></span> | <span data-ttu-id="8c34d-303">Son n’est pas spatialized comme prévu, et/ou manque de son pour aider l’utilisateur au sein de l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-303">Sound is not spatialized as expected, and/or lack of sound to assist user within the UX.</span></span> <span data-ttu-id="8c34d-304">Ou spatial audio a été pas considéré comme utilisé dans la conception du scénario.</span><span class="sxs-lookup"><span data-stu-id="8c34d-304">Or spatial audio was not considered or used in the design of the scenario.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-305">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-305">How to measure</span></span>

* <span data-ttu-id="8c34d-306">En règle générale, d’émettre des sons pertinentes à partir de hologrammes de cible (par ex., son écorce provenant HOLOGRAPHIQUE dog.)</span><span class="sxs-lookup"><span data-stu-id="8c34d-306">In general, relevant sounds should emit from target holograms (eg., bark sound coming from holographic dog.)</span></span>
* <span data-ttu-id="8c34d-307">Signaux audio doivent être utilisées dans l’expérience utilisateur pour aider l’utilisateur avec des commentaires ou une connaissance des actions en dehors du cadre HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="8c34d-307">Sound cues should be used throughout the UX to assist the user with feedback or awareness of actions outside the holographic frame.</span></span>

### <a name="recommendations"></a><span data-ttu-id="8c34d-308">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-308">Recommendations</span></span>

* <span data-ttu-id="8c34d-309">Utilisez audio spatial afin de faciliter les interfaces utilisateur et de découverte de l’objet.</span><span class="sxs-lookup"><span data-stu-id="8c34d-309">Use spatial audio to assist with object discovery and user interfaces.</span></span>
* <span data-ttu-id="8c34d-310">Sons réels fonctionnent mieux que son non naturelle ou de synthèse.</span><span class="sxs-lookup"><span data-stu-id="8c34d-310">Real sounds work better than synthesize or unnatural sound.</span></span>
* <span data-ttu-id="8c34d-311">La plupart des sons doivent être spatialized.</span><span class="sxs-lookup"><span data-stu-id="8c34d-311">Most sounds should be spatialized.</span></span>
* <span data-ttu-id="8c34d-312">Évitez d’émetteurs invisibles.</span><span class="sxs-lookup"><span data-stu-id="8c34d-312">Avoid invisible emitters.</span></span>
* <span data-ttu-id="8c34d-313">Évitez les masques spatiale.</span><span class="sxs-lookup"><span data-stu-id="8c34d-313">Avoid spatial masking.</span></span>
* <span data-ttu-id="8c34d-314">Normaliser toutes les sons.</span><span class="sxs-lookup"><span data-stu-id="8c34d-314">Normalize all sounds.</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-315">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-315">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="8c34d-316">Documentation</span><span class="sxs-lookup"><span data-stu-id="8c34d-316">Documentation</span></span>

* [<span data-ttu-id="8c34d-317">Son spatial</span><span class="sxs-lookup"><span data-stu-id="8c34d-317">Spatial sound</span></span>](spatial-sound.md)
* [<span data-ttu-id="8c34d-318">Sonorisation spatiale</span><span class="sxs-lookup"><span data-stu-id="8c34d-318">Spatial sound design</span></span>](spatial-sound-design.md)
* [<span data-ttu-id="8c34d-319">Son spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="8c34d-319">Spatial sound in Unity</span></span>](spatial-sound-in-unity.md)
* [<span data-ttu-id="8c34d-320">Étude de cas, Spatial audio pour HoloTour</span><span class="sxs-lookup"><span data-stu-id="8c34d-320">Case study, Spatial sound for HoloTour</span></span>](case-study-spatial-sound-design-for-holotour.md)
* [<span data-ttu-id="8c34d-321">Étude de cas, à l’aide de son spatial dans RoboRaid</span><span class="sxs-lookup"><span data-stu-id="8c34d-321">Case study, Using spatial sound in RoboRaid</span></span>](case-study-using-spatial-sound-in-roboraid.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="8c34d-322">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="8c34d-322">Tools and tutorials</span></span>

* [<span data-ttu-id="8c34d-323">MR 220 spatiale : Son spatial</span><span class="sxs-lookup"><span data-stu-id="8c34d-323">MR Spatial 220: Spatial sound</span></span>](holograms-220.md)
* [<span data-ttu-id="8c34d-324">MRToolkit, Audio Spatial</span><span class="sxs-lookup"><span data-stu-id="8c34d-324">MRToolkit, Spatial Audio</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/SpatialSound/README.md)

## <a name="focus-on-holographic-frame-fov-boundaries"></a><span data-ttu-id="8c34d-325">Vous concentrer sur les limites du cadre HOLOGRAPHIQUE (angle d’ouverture)</span><span class="sxs-lookup"><span data-stu-id="8c34d-325">Focus on holographic frame (FOV) boundaries</span></span>

<span data-ttu-id="8c34d-326">Expériences utilisateur bien conçue peuvent créer et gérer un contexte utile de l’environnement virtuel qui s’étend sur les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8c34d-326">Well-designed user experiences can create and maintain useful context of the virtual environment that extends around the users.</span></span> <span data-ttu-id="8c34d-327">Atténuer l’effet des limites d’angle d’ouverture implique une conception réfléchie de contenu à l’échelle et le contexte, utilisez de signal audio spatial, les systèmes de conseils et position de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-327">Mitigating the effect of the FOV boundaries involves a thoughtful design of content scale and context, use of spatial audio, guidance systems, and the user's position.</span></span> <span data-ttu-id="8c34d-328">Si est correctement effectuée, l’utilisateur semblera étrange qu'inférieur altérée par les limites de l’angle d’ouverture, tout en ayant une expérience d’application à l’aise.</span><span class="sxs-lookup"><span data-stu-id="8c34d-328">If done right, the user will feel less impaired by the FOV boundaries while having a comfortable app experience.</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-329">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-329">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-330"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-330"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-331"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-331"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-332">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-332">✔️</span></span></td><td style="text-align: center;"></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-333">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-333">Quality criteria</span></span>

|  <span data-ttu-id="8c34d-334">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-334">Best</span></span>  |  <span data-ttu-id="8c34d-335">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-335">Meets</span></span> |  <span data-ttu-id="8c34d-336">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-336">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="8c34d-337">Utilisateur perd jamais le contexte et l’affichage est à l’aise.</span><span class="sxs-lookup"><span data-stu-id="8c34d-337">User never loses context and viewing is comfortable.</span></span> <span data-ttu-id="8c34d-338">L’assistance de contexte est fourni pour les objets volumineux.</span><span class="sxs-lookup"><span data-stu-id="8c34d-338">Context assistance is provided for large objects.</span></span> <span data-ttu-id="8c34d-339">Détectabilité et l’affichage des instructions est fournie pour les objets en dehors du cadre.</span><span class="sxs-lookup"><span data-stu-id="8c34d-339">Discoverability and viewing guidance is provided for objects outside the frame.</span></span> <span data-ttu-id="8c34d-340">En règle générale, conception de mouvement et de mise à l’échelle des hologrammes conviennent pour une expérience d’affichage à l’aise.</span><span class="sxs-lookup"><span data-stu-id="8c34d-340">In general, motion design and scale of the holograms are appropriate for a comfortable viewing experience.</span></span> | <span data-ttu-id="8c34d-341">Utilisateur perd jamais le contexte, mais le mouvement de cou supplémentaire peut être nécessaire dans des situations bien définies.</span><span class="sxs-lookup"><span data-stu-id="8c34d-341">User never loses context, but extra neck motion may be required in limited situations.</span></span> <span data-ttu-id="8c34d-342">Dans des situations bien définies à l’échelle provoque hologrammes arrêter l’exécution soit le frame vertical ou horizontal à l’origine de certains mouvements cou afficher les hologrammes.</span><span class="sxs-lookup"><span data-stu-id="8c34d-342">In limited situations scale causes holograms to break either the vertical or horizontal frame causing some neck motion to view holograms.</span></span> | <span data-ttu-id="8c34d-343">Utilisateur risque de perdre le contexte et/ou de mouvement de cou cohérent est requis pour afficher les hologrammes.</span><span class="sxs-lookup"><span data-stu-id="8c34d-343">User likely to lose context and/or consistent neck motion is required to view holograms.</span></span> <span data-ttu-id="8c34d-344">Aucune indication de contexte pour les objets volumineux HOLOGRAPHIQUE, déplacement d’objets facile de perdre en dehors du cadre sans les conseils de détectabilité, ni en hauteur hologrammes ne requiert cou régulière à afficher.</span><span class="sxs-lookup"><span data-stu-id="8c34d-344">No context guidance for large holographic objects, moving objects easy to lose outside the frame with no discoverability guidance, or tall holograms requires regular neck motion to view.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-345">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-345">How to measure</span></span>

* <span data-ttu-id="8c34d-346">Contexte pour un hologramme (grand) est perdu ou pas comprise en raison d’être détourée aux limites de le.</span><span class="sxs-lookup"><span data-stu-id="8c34d-346">Context for a (large) hologram is lost or not understood due to being clipped at the boundaries.</span></span>
* <span data-ttu-id="8c34d-347">Emplacement de hologrammes sont difficiles à détecter en raison du manque de directeurs d’attention ou du contenu qui déplace rapidement vers et depuis le frame HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="8c34d-347">Location of holograms are hard to find due to the lack of attention directors or content that rapidly moves in and out of the holographic frame.</span></span>
* <span data-ttu-id="8c34d-348">Scénario nécessite régulière et répétitives haut et bas de mouvement principal pour afficher entièrement un hologramme résultant de fatigue de col.</span><span class="sxs-lookup"><span data-stu-id="8c34d-348">Scenario requires regular and repetitive up and down head motion to fully see a hologram resulting in neck fatigue.</span></span>

### <a name="recommendations"></a><span data-ttu-id="8c34d-349">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-349">Recommendations</span></span>

* <span data-ttu-id="8c34d-350">Démarrez l’expérience avec les petits objets ajuster l’angle d’ouverture, puis effectuer la transition des aides visuelles aux versions plus grande.</span><span class="sxs-lookup"><span data-stu-id="8c34d-350">Start the experience with small objects that fit the FOV, then transition with visual cues to larger versions.</span></span>
* <span data-ttu-id="8c34d-351">Utilisez spatiales directeurs audio et d’attention pour la recherche de contenu utilisateur qui est en dehors de l’angle d’ouverture.</span><span class="sxs-lookup"><span data-stu-id="8c34d-351">Use spatial audio and attention directors to help the user find content that is outside the FOV.</span></span>
* <span data-ttu-id="8c34d-352">Autant que possible, évitez hologrammes qui découper verticalement l’angle d’ouverture.</span><span class="sxs-lookup"><span data-stu-id="8c34d-352">As much as possible, avoid holograms that vertically clip the FOV.</span></span>
* <span data-ttu-id="8c34d-353">Fournir à l’utilisateur dans l’application des conseils pour optimiser l’affichage d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="8c34d-353">Provide the user with in-app guidance for best viewing location.</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-354">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-354">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="8c34d-355">Documentation</span><span class="sxs-lookup"><span data-stu-id="8c34d-355">Documentation</span></span>

* [<span data-ttu-id="8c34d-356">Frame HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="8c34d-356">Holographic frame</span></span>](holographic-frame.md)
* [<span data-ttu-id="8c34d-357">Étude de cas, HoloStudio UI et apprentissages de conception d’interaction</span><span class="sxs-lookup"><span data-stu-id="8c34d-357">Case Study, HoloStudio UI and interaction design learnings</span></span>](case-study-3-holostudio-ui-and-interaction-design-learnings.md?#problem-2-modal-dialogs-are-sometimes-out-of-the-holographic-frame)
* [<span data-ttu-id="8c34d-358">Mise à l’échelle des objets et des environnements</span><span class="sxs-lookup"><span data-stu-id="8c34d-358">Scale of objects and environments</span></span>](scale.md)
* [<span data-ttu-id="8c34d-359">Curseurs, les signaux visuels</span><span class="sxs-lookup"><span data-stu-id="8c34d-359">Cursors, Visual cues</span></span>](cursors.md#visual-cues)

#### <a name="external-references"></a><span data-ttu-id="8c34d-360">Références externes</span><span class="sxs-lookup"><span data-stu-id="8c34d-360">External references</span></span>

* [<span data-ttu-id="8c34d-361">Fait beaucoup de bruit sur l’angle d’ouverture</span><span class="sxs-lookup"><span data-stu-id="8c34d-361">Much ado about the FOV</span></span>](https://www.linkedin.com/pulse/hololens-much-ado-field-of-view-michael-hoffman?lipi=urn%3Ali%3Apage%3Ad_flagship3_feed%3B6iQ%2FbTevLDU93w3I2ewLJw%3D%3D)

## <a name="content-reacts-to-user-position"></a><span data-ttu-id="8c34d-362">Contenu réagit à la position de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="8c34d-362">Content reacts to user position</span></span>

<span data-ttu-id="8c34d-363">Hologrammes doivent réagir à la position de l’utilisateur dans à peu près la même façon que les objets de « vraies ».</span><span class="sxs-lookup"><span data-stu-id="8c34d-363">Holograms should react to the user position in roughly the same ways that "real" objects do.</span></span> <span data-ttu-id="8c34d-364">Une considération de conception importants est éléments d’interface utilisateur qui ne peut pas supposer nécessairement la position de l’utilisateur est à l’arrêt et s’adapter aux mouvements de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-364">A notable design consideration is UI elements that can't necessarily assume a user's position is stationary and adapt to the user's motion.</span></span> <span data-ttu-id="8c34d-365">Conception d’une application qui s’adapte correctement à la position de l’utilisateur pour créer une expérience plus crédible et rendre plus facile à utiliser.</span><span class="sxs-lookup"><span data-stu-id="8c34d-365">Designing an app that correctly adapts to user position will create a more believable experience and make it easier to use.</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-366">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-366">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-367"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-367"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-368"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-368"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-369">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-369">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="8c34d-370">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-370">✔️</span></span></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-371">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-371">Quality criteria</span></span>

<table>
<tr>
<td> <span data-ttu-id="8c34d-372">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-372">Best</span></span> </td><td> <span data-ttu-id="8c34d-373">Contenu et l’interface utilisateur de s’adapter aux positions d’utilisateur qui permet à utilisateur d’interagir naturellement avec le contenu dans l’étendue du mouvement de l’utilisateur attendu.</span><span class="sxs-lookup"><span data-stu-id="8c34d-373">Content and UI adapt to user positions allowing user to naturally interact with content within the scope of expected user movement.</span></span></td>
</tr><tr>
<td> <span data-ttu-id="8c34d-374">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-374">Meets</span></span> </td><td> <span data-ttu-id="8c34d-375">L’interface utilisateur s’adapte à la position de l’utilisateur, mais susceptible de compromettre l’affichage de contenu de clé nécessitant l’utilisateur d’ajuster leur position.</span><span class="sxs-lookup"><span data-stu-id="8c34d-375">UI adapts to the user position, but may impede the view of key content requiring the user to adjust their position.</span></span></td>
</tr><tr>
<td> <span data-ttu-id="8c34d-376">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-376">Fail</span></span> </td><td><ol>
<li><span data-ttu-id="8c34d-377">Éléments d’interface utilisateur sont perdus ou verrouillés au cours de l’utilisateur entraînant le déplacement des queues revenir à (ou rechercher) des contrôles.</span><span class="sxs-lookup"><span data-stu-id="8c34d-377">UI elements are lost or locked during movement causing user to unnaturally return to (or find) controls.</span></span></li><li><span data-ttu-id="8c34d-378">Éléments d’interface utilisateur restreindre l’affichage du contenu principal.</span><span class="sxs-lookup"><span data-stu-id="8c34d-378">UI elements limit the view of primary content.</span></span></li><li><span data-ttu-id="8c34d-379">Déplacement de l’interface utilisateur n’est pas optimisé pour la distance d’affichage et l’inertie en particulier avec <a href="billboarding-and-tag-along.md">tag-along</a> éléments d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-379">UI movement is not optimized for viewing distance and momentum particularly with <a href="billboarding-and-tag-along.md">tag-along</a> UI elements.</span></span></li>
</ol></td>
</tr>
</table>

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-380">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-380">How to measure</span></span>

* <span data-ttu-id="8c34d-381">Toutes les mesures doivent être effectuées dans une étendue raisonnable du scénario.</span><span class="sxs-lookup"><span data-stu-id="8c34d-381">All measurements should be done within a reasonable scope of the scenario.</span></span> <span data-ttu-id="8c34d-382">Tandis que le déplacement de l’utilisateur peut varier, n’essayez pas de tromper l’application avec le déplacement des utilisateur extrêmes.</span><span class="sxs-lookup"><span data-stu-id="8c34d-382">While user movement will vary, don’t try to trick the app with extreme user movement.</span></span>
* <span data-ttu-id="8c34d-383">Pour les éléments d’interface utilisateur, les contrôles appropriés doivent être disponibles quel que soit le mouvement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-383">For UI elements, relevant controls should be available regardless of user movement.</span></span> <span data-ttu-id="8c34d-384">Par exemple, si l’utilisateur est Affichez et vous épargne une carte 3D avec zoom, le contrôle de zoom doit être prête à l’utilisateur, quel que soit l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="8c34d-384">For example, if the user is viewing and walking around a 3D map with zoom, the zoom control should be readily available to the user regardless of location.</span></span>

### <a name="recommendations"></a><span data-ttu-id="8c34d-385">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-385">Recommendations</span></span>

* <span data-ttu-id="8c34d-386">L’utilisateur est l’appareil photo et qu’ils contrôlent le déplacement.</span><span class="sxs-lookup"><span data-stu-id="8c34d-386">The user is the camera and they control the movement.</span></span> <span data-ttu-id="8c34d-387">Let leur lecteur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-387">Let them drive.</span></span>
* <span data-ttu-id="8c34d-388">Prendre en compte le billboarding pour le texte et pour vous déplacer dans les systèmes de rentrer qui seraient sinon être world-verrouillé ou masquées si un utilisateur étaient.</span><span class="sxs-lookup"><span data-stu-id="8c34d-388">Consider billboarding for text and menuing systems that would otherwise be world-locked or obscured if a user were to move around.</span></span>
* <span data-ttu-id="8c34d-389">Utiliser tag-along pour le contenu qui doit suivre l’utilisateur tout en permettant à l’utilisateur de voir ce qui est placé devant.</span><span class="sxs-lookup"><span data-stu-id="8c34d-389">Use tag-along for content that needs to follow the user while still allowing the user to see what is in front of them.</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-390">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-390">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="8c34d-391">Documentation</span><span class="sxs-lookup"><span data-stu-id="8c34d-391">Documentation</span></span>

* [<span data-ttu-id="8c34d-392">Conception de l’interaction</span><span class="sxs-lookup"><span data-stu-id="8c34d-392">Interaction design</span></span>](hologram.md)
* [<span data-ttu-id="8c34d-393">Couleur, clair et matériel</span><span class="sxs-lookup"><span data-stu-id="8c34d-393">Color, light, and material</span></span>](color,-light-and-materials.md)
* [<span data-ttu-id="8c34d-394">Le billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="8c34d-394">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
* [<span data-ttu-id="8c34d-395">Notions fondamentales d’interaction</span><span class="sxs-lookup"><span data-stu-id="8c34d-395">Interaction fundamentals</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="8c34d-396">Automatique de mouvement et locomotion de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="8c34d-396">Self-motion and user locomotion</span></span>](comfort.md#self-motion-and-user-locomotion)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="8c34d-397">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="8c34d-397">Tools and tutorials</span></span>

* [<span data-ttu-id="8c34d-398">Entrée M. 210 : Gaze</span><span class="sxs-lookup"><span data-stu-id="8c34d-398">MR Input 210: Gaze</span></span>](holograms-210.md)

## <a name="input-interaction-clarity"></a><span data-ttu-id="8c34d-399">Clarté de l’interaction d’entrée</span><span class="sxs-lookup"><span data-stu-id="8c34d-399">Input interaction clarity</span></span>

<span data-ttu-id="8c34d-400">Clarté de l’interaction d’entrée est essentielle à la facilité d’utilisation d’une application et inclut la cohérence d’entrée, de commodité, de détectabilité des méthodes d’interaction.</span><span class="sxs-lookup"><span data-stu-id="8c34d-400">Input interaction clarity is critical to an app's usability and includes input consistency, approachability, discoverability of interaction methods.</span></span> <span data-ttu-id="8c34d-401">Utilisateur doit être en mesure d’utiliser des interactions courantes à l’échelle de la plateforme sans efforts d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="8c34d-401">User should be able to use platform-wide common interactions without relearning.</span></span> <span data-ttu-id="8c34d-402">Si l’application a entrée personnalisée, il doit être clairement communiqué et démontré.</span><span class="sxs-lookup"><span data-stu-id="8c34d-402">If the app has custom input, it should be clearly communicated and demonstrated.</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-403">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-403">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-404"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-404"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-405"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-405"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-406">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-406">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="8c34d-407">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-407">✔️</span></span></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-408">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-408">Quality criteria</span></span>

|  <span data-ttu-id="8c34d-409">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-409">Best</span></span>  |  <span data-ttu-id="8c34d-410">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-410">Meets</span></span> |  <span data-ttu-id="8c34d-411">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-411">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="8c34d-412">Méthodes d’interaction d’entrée sont cohérents avec la réalité mixte Windows fourni [conseils](interaction-fundamentals.md).</span><span class="sxs-lookup"><span data-stu-id="8c34d-412">Input interaction methods are consistent with Windows Mixed Reality provided [guidance](interaction-fundamentals.md).</span></span> <span data-ttu-id="8c34d-413">Toute entrée personnalisée ne doit pas être redondante avec l’entrée standard (plutôt utiliser l’interaction standard) et doit être clairement communiquée et démontrée à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-413">Any custom input should not be redundant with standard input (rather use standard interaction) and must be clearly communicated and demonstrated to the user.</span></span> | <span data-ttu-id="8c34d-414">Similaire aux entrées meilleures, mais personnalisées sont redondantes avec les méthodes d’entrée standards.</span><span class="sxs-lookup"><span data-stu-id="8c34d-414">Similar to best, but custom inputs are redundant with standard input methods.</span></span> <span data-ttu-id="8c34d-415">Utilisateur peut toujours atteindre l’objectif et la progression via l’expérience de l’application.</span><span class="sxs-lookup"><span data-stu-id="8c34d-415">User can still achieve the goal and progress through the app experience.</span></span> | <span data-ttu-id="8c34d-416">Il est difficile de comprendre le mappage de bouton ou de la méthode d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8c34d-416">Difficult to understand input method or button mapping.</span></span> <span data-ttu-id="8c34d-417">Entrée est fortement personnalisée, ne prend pas en charge l’entrée standard, aucune instruction, ou susceptibles de provoquer des problèmes de fatigue et de confort.</span><span class="sxs-lookup"><span data-stu-id="8c34d-417">Input is heavily customized, does not support standard input, no instructions, or likely to cause fatigue and comfort issues.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-418">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-418">How to measure</span></span>

* <span data-ttu-id="8c34d-419">L’application utilise cohérente [standard d’entrée des méthodes.](interaction-fundamentals.md)</span><span class="sxs-lookup"><span data-stu-id="8c34d-419">The app uses consistent [standard input methods.](interaction-fundamentals.md)</span></span>
* <span data-ttu-id="8c34d-420">Si l’application a d’entrée personnalisés, il est clairement communiqué via :</span><span class="sxs-lookup"><span data-stu-id="8c34d-420">If the app has custome input, it is clearly communicated through:</span></span>
* <span data-ttu-id="8c34d-421">Expérience de première exécution</span><span class="sxs-lookup"><span data-stu-id="8c34d-421">First-run experience</span></span>
* <span data-ttu-id="8c34d-422">Écrans d’introduction</span><span class="sxs-lookup"><span data-stu-id="8c34d-422">Introductory screens</span></span>
* <span data-ttu-id="8c34d-423">Info-bulles</span><span class="sxs-lookup"><span data-stu-id="8c34d-423">Tooltips</span></span>
* <span data-ttu-id="8c34d-424">Coach de main</span><span class="sxs-lookup"><span data-stu-id="8c34d-424">Hand coach</span></span>
* <span data-ttu-id="8c34d-425">Section aide</span><span class="sxs-lookup"><span data-stu-id="8c34d-425">Help section</span></span>
* <span data-ttu-id="8c34d-426">VoiceOver</span><span class="sxs-lookup"><span data-stu-id="8c34d-426">Voice over</span></span>

### <a name="recommendations"></a><span data-ttu-id="8c34d-427">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-427">Recommendations</span></span>

* <span data-ttu-id="8c34d-428">Utilisez les méthodes d’entrée standards chaque fois que possible.</span><span class="sxs-lookup"><span data-stu-id="8c34d-428">Use standard input methods whenever possible.</span></span>
* <span data-ttu-id="8c34d-429">Fournir des démonstrations, des didacticiels et des info-bulles pour les méthodes d’entrée non standards.</span><span class="sxs-lookup"><span data-stu-id="8c34d-429">Provide demonstrations, tutorials, and tooltips for non-standard input methods.</span></span>
* <span data-ttu-id="8c34d-430">Utiliser un modèle d’interaction cohérente dans toute l’application.</span><span class="sxs-lookup"><span data-stu-id="8c34d-430">Use a consistent interaction model throughout the app.</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-431">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-431">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="8c34d-432">Documentation</span><span class="sxs-lookup"><span data-stu-id="8c34d-432">Documentation</span></span>

* [<span data-ttu-id="8c34d-433">Principes de base Windows MR interaction</span><span class="sxs-lookup"><span data-stu-id="8c34d-433">Windows MR interaction fundamentals</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="8c34d-434">Objets sur</span><span class="sxs-lookup"><span data-stu-id="8c34d-434">Interactable objects</span></span>](interactable-object.md)
* [<span data-ttu-id="8c34d-435">Ciblage des regards</span><span class="sxs-lookup"><span data-stu-id="8c34d-435">Gaze targeting</span></span>](gaze-targeting.md)
* [<span data-ttu-id="8c34d-436">Curseurs</span><span class="sxs-lookup"><span data-stu-id="8c34d-436">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="8c34d-437">Confort et regards</span><span class="sxs-lookup"><span data-stu-id="8c34d-437">Comfort and gaze</span></span>](comfort.md#gaze-direction)
* [<span data-ttu-id="8c34d-438">Mouvements</span><span class="sxs-lookup"><span data-stu-id="8c34d-438">Gestures</span></span>](gestures.md)
* [<span data-ttu-id="8c34d-439">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="8c34d-439">Voice input</span></span>](voice-input.md)
* [<span data-ttu-id="8c34d-440">Conception de la voix</span><span class="sxs-lookup"><span data-stu-id="8c34d-440">Voice design</span></span>](voice-design.md)
* [<span data-ttu-id="8c34d-441">Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="8c34d-441">Motion controllers</span></span>](motion-controllers.md)
* [<span data-ttu-id="8c34d-442">Entrée portage guide pour Unity</span><span class="sxs-lookup"><span data-stu-id="8c34d-442">Input porting guide for Unity</span></span>](input-porting-guide-for-unity.md)
* [<span data-ttu-id="8c34d-443">Entrée au clavier dans Unity</span><span class="sxs-lookup"><span data-stu-id="8c34d-443">Keyboard input in Unity</span></span>](keyboard-input-in-unity.md)
* [<span data-ttu-id="8c34d-444">Les regards dans Unity</span><span class="sxs-lookup"><span data-stu-id="8c34d-444">Gaze in Unity</span></span>](gaze-in-unity.md)
* [<span data-ttu-id="8c34d-445">Mouvements et les contrôleurs de mouvement dans Unity</span><span class="sxs-lookup"><span data-stu-id="8c34d-445">Gestures and motion controllers in Unity</span></span>](gestures-and-motion-controllers-in-unity.md)
* [<span data-ttu-id="8c34d-446">Entrée vocale dans Unity</span><span class="sxs-lookup"><span data-stu-id="8c34d-446">Voice input in Unity</span></span>](voice-input-in-unity.md)
* [<span data-ttu-id="8c34d-447">Entrée d’un contrôleur dans DirectX, clavier et souris</span><span class="sxs-lookup"><span data-stu-id="8c34d-447">Keyboard, mouse, and controller input in DirectX</span></span>](keyboard,-mouse,-and-controller-input-in-directx.md)
* [<span data-ttu-id="8c34d-448">Regards, les mouvements et les contrôleurs de mouvement dans DirectX</span><span class="sxs-lookup"><span data-stu-id="8c34d-448">Gaze, gesture, and motion controllers in DirectX</span></span>](gaze,-gestures,-and-motion-controllers-in-directx.md)
* [<span data-ttu-id="8c34d-449">Entrée vocale dans DirectX</span><span class="sxs-lookup"><span data-stu-id="8c34d-449">Voice input in DirectX</span></span>](voice-input-in-directx.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="8c34d-450">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="8c34d-450">Tools and tutorials</span></span>

* [<span data-ttu-id="8c34d-451">Étude de cas : La poursuite de l’informatique plus personnelle</span><span class="sxs-lookup"><span data-stu-id="8c34d-451">Case study: The pursuit of more personal computing</span></span>](case-study-the-pursuit-of-more-personal-computing.md#less-interface-in-your-face)
* [<span data-ttu-id="8c34d-452">Étude de cast : HoloStudio UI et apprentissages de conception d’interaction</span><span class="sxs-lookup"><span data-stu-id="8c34d-452">Cast study: HoloStudio UI and interaction design learnings</span></span>](case-study-3-holostudio-ui-and-interaction-design-learnings.md)
* [<span data-ttu-id="8c34d-453">Exemple d’application : Tableau périodique des éléments</span><span class="sxs-lookup"><span data-stu-id="8c34d-453">Sample app: Periodic table of the elements</span></span>](periodic-table-of-the-elements.md)
* [<span data-ttu-id="8c34d-454">Exemple d’application : Module de lunaire</span><span class="sxs-lookup"><span data-stu-id="8c34d-454">Sample app: Lunar module</span></span>](lunar-module.md)
* [<span data-ttu-id="8c34d-455">Entrée M. 210 : Gaze</span><span class="sxs-lookup"><span data-stu-id="8c34d-455">MR Input 210: Gaze</span></span>](holograms-210.md)
* [<span data-ttu-id="8c34d-456">Entrée M. 211 : Mouvements</span><span class="sxs-lookup"><span data-stu-id="8c34d-456">MR Input 211: Gestures</span></span>](holograms-211.md)
* [<span data-ttu-id="8c34d-457">Entrée M. 212 : Voix</span><span class="sxs-lookup"><span data-stu-id="8c34d-457">MR Input 212: Voice</span></span>](holograms-212.md)

## <a name="interactable-objects"></a><span data-ttu-id="8c34d-458">Objets sur</span><span class="sxs-lookup"><span data-stu-id="8c34d-458">Interactable objects</span></span>

<span data-ttu-id="8c34d-459">Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait 2D.</span><span class="sxs-lookup"><span data-stu-id="8c34d-459">A button has long been a metaphor used for triggering an event in the 2D abstract world.</span></span> <span data-ttu-id="8c34d-460">Dans le monde en trois dimensions de réalité mixte, nous n’êtes pas obligé d’être limitées à ce monde d’abstraction plus.</span><span class="sxs-lookup"><span data-stu-id="8c34d-460">In the three-dimensional mixed reality world, we don’t have to be confined to this world of abstraction anymore.</span></span> <span data-ttu-id="8c34d-461">Quoi que ce soit peut être un objet sur qui déclenche un événement.</span><span class="sxs-lookup"><span data-stu-id="8c34d-461">Anything can be an Interactable object that triggers an event.</span></span> <span data-ttu-id="8c34d-462">Un objet sur peut être représenté en tant que quoi que ce soit à partir d’une tasse de café sur la table à une info-bulle flottante en l’air.</span><span class="sxs-lookup"><span data-stu-id="8c34d-462">An interactable object can be represented as anything from a coffee cup on the table to a balloon floating in the air.</span></span> <span data-ttu-id="8c34d-463">Quel que soit le formulaire, les objets sur doivent être clairement reconnaissables par l’utilisateur via des signaux visuels et audio.</span><span class="sxs-lookup"><span data-stu-id="8c34d-463">Regardless of the form, interactable objects should be clearly recognizable by the user through visual and audio cues.</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-464">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-464">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-465"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-465"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-466"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-466"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-467">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-467">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="8c34d-468">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-468">✔️</span></span></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-469">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-469">Quality criteria</span></span>

|  <span data-ttu-id="8c34d-470">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-470">Best</span></span>  |  <span data-ttu-id="8c34d-471">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-471">Meets</span></span> |  <span data-ttu-id="8c34d-472">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-472">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="8c34d-473">Quel que soit le formulaire, des objets sur sont reconnaissables par le biais des signaux visuels et audio sur trois états : inactif, ciblées et sélectionné.</span><span class="sxs-lookup"><span data-stu-id="8c34d-473">Regardless of form, interactable objects are recognizable through visual and audio cues across three states: idle, targeted, and selected.</span></span> <span data-ttu-id="8c34d-474">« Consultez, dites » effacer et de manière cohérente sert tout au long de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="8c34d-474">"See it, say it" is clear and consistently used throughout the experience.</span></span> <span data-ttu-id="8c34d-475">Les objets sont mis à l’échelle et distribués pour autoriser l’erreur gratuit de ciblage.</span><span class="sxs-lookup"><span data-stu-id="8c34d-475">Objects are scaled and distributed to allow for error free targeting.</span></span> | <span data-ttu-id="8c34d-476">Utilisateur peut reconnaître l’objet en tant que sur via des commentaires audio et visuels et cibler et activer l’objet.</span><span class="sxs-lookup"><span data-stu-id="8c34d-476">User can recognize object as interactable through audio or visual feedback, and can target and activate the object.</span></span> | <span data-ttu-id="8c34d-477">Étant donné aucun signaux visual ou audio, utilisateur ne peut pas reconnaître un objet sur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-477">Given no visual or audio cues, user cannot recognize an interactable object.</span></span> <span data-ttu-id="8c34d-478">Interactions sont sujettes en raison de l’échelle de l’objet ou la distance entre les objets.</span><span class="sxs-lookup"><span data-stu-id="8c34d-478">Interactions are error prone due to object scale or distance between objects.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-479">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-479">How to measure</span></span>

* <span data-ttu-id="8c34d-480">Objets sur sont reconnus comme 'sur' ; y compris les boutons, menus et application de contenu spécifique.</span><span class="sxs-lookup"><span data-stu-id="8c34d-480">Interactable objects are recognizable as 'interactable'; including buttons, menus, and app specific content.</span></span> <span data-ttu-id="8c34d-481">En règle générale il doit être un indice visuel et audio lors du ciblage des objets sur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-481">As a rule of thumb there should be a visual and audio cue when targeting interactable objects.</span></span>

### <a name="recommendations"></a><span data-ttu-id="8c34d-482">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-482">Recommendations</span></span>

* <span data-ttu-id="8c34d-483">Utiliser des commentaires visuels et audio pour les interactions.</span><span class="sxs-lookup"><span data-stu-id="8c34d-483">Use visual and audio feedback for interactions.</span></span>
* <span data-ttu-id="8c34d-484">Des commentaires visuels doivent être différenciées pour chaque d’entrée d’état (inactif, ciblé, sélectionné)</span><span class="sxs-lookup"><span data-stu-id="8c34d-484">Visual feedback should be differentiated for each input state (idle, targeted, selected)</span></span>
* <span data-ttu-id="8c34d-485">Objets sur doivent être mis à l’échelle et placés par erreur gratuit de ciblage.</span><span class="sxs-lookup"><span data-stu-id="8c34d-485">Interactable objects should be scaled and placed for error free targeting.</span></span>
* <span data-ttu-id="8c34d-486">Les objets groupés sur (par exemple, une barre de menus ou de la liste) doivent avoir espacement approprié pour le ciblage.</span><span class="sxs-lookup"><span data-stu-id="8c34d-486">Grouped interactable objects (such as a menu bar or list) should have proper spacing for targeting.</span></span>
* <span data-ttu-id="8c34d-487">Boutons et des menus qui prennent en charge de la commande vocale doivent fournir des étiquettes de texte pour le mot clé de commande (« voir, dites-le »)</span><span class="sxs-lookup"><span data-stu-id="8c34d-487">Buttons and menus that support voice command should provide text labels for the command keyword ("See it, say it")</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-488">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-488">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="8c34d-489">Documentation</span><span class="sxs-lookup"><span data-stu-id="8c34d-489">Documentation</span></span>

* [<span data-ttu-id="8c34d-490">Objet sur</span><span class="sxs-lookup"><span data-stu-id="8c34d-490">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="8c34d-491">Texte dans Unity</span><span class="sxs-lookup"><span data-stu-id="8c34d-491">Text in Unity</span></span>](text-in-unity.md)
* [<span data-ttu-id="8c34d-492">Barre de l’application et de la zone englobante</span><span class="sxs-lookup"><span data-stu-id="8c34d-492">App bar and bounding box</span></span>](app-bar-and-bounding-box.md)
* [<span data-ttu-id="8c34d-493">Conception de la voix</span><span class="sxs-lookup"><span data-stu-id="8c34d-493">Voice design</span></span>](voice-design.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="8c34d-494">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="8c34d-494">Tools and tutorials</span></span>

* [<span data-ttu-id="8c34d-495">Réalité mixte Toolkit - UX</span><span class="sxs-lookup"><span data-stu-id="8c34d-495">Mixed Reality Toolkit - UX</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/UX)

## <a name="room-scanning"></a><span data-ttu-id="8c34d-496">Espace d’analyse</span><span class="sxs-lookup"><span data-stu-id="8c34d-496">Room scanning</span></span>

<span data-ttu-id="8c34d-497">Les applications qui requièrent des données de mappage spatial s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions en tant que l’utilisateur explore leur environnement avec l’appareil actif.</span><span class="sxs-lookup"><span data-stu-id="8c34d-497">Apps that require spatial mapping data rely on the device to automatically collect this data over time and across sessions as the user explores their environment with the device active.</span></span> <span data-ttu-id="8c34d-498">Le souci d’exhaustivité et la qualité de ces données dépend de plusieurs facteurs, notamment la quantité d’exploration de l’utilisateur a effectué, combien de temps écoulé depuis l’exploration et indique si les objets tels que des portes et meubles ont déplacés depuis le périphérique analyse la zone.</span><span class="sxs-lookup"><span data-stu-id="8c34d-498">The completeness and quality of this data depends on a number of factors including the amount of exploration the user has done, how much time has passed since the exploration and whether objects such as furniture and doors have moved since the device scanned the area.</span></span> <span data-ttu-id="8c34d-499">De nombreuses applications analysera les données de mappage spatial au début de l’expérience pour déterminer si l’utilisateur doit effectuer des étapes supplémentaires pour améliorer l’exhaustivité et la qualité de la carte spatiale à.</span><span class="sxs-lookup"><span data-stu-id="8c34d-499">Many apps will analyze the spatial mapping data at the start of the experience to judge whether the user should perform additional steps to improve the completeness and quality of the spatial map.</span></span> <span data-ttu-id="8c34d-500">Si l’utilisateur est requis pour l’analyse de l’environnement, effacer des conseils doivent être fournis lors de l’expérience d’analyse.</span><span class="sxs-lookup"><span data-stu-id="8c34d-500">If the user is required to scan the environment, clear guidance should be provided during the scanning experience.</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-501">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-501">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-502"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-502"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-503"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-503"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-504">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-504">✔️</span></span></td><td style="text-align: center;"></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-505">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-505">Quality criteria</span></span>

|  <span data-ttu-id="8c34d-506">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-506">Best</span></span>  |  <span data-ttu-id="8c34d-507">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-507">Meets</span></span> |  <span data-ttu-id="8c34d-508">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-508">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="8c34d-509">Visualisation de la maille spatiale indiquent aux utilisateurs de l’analyse sont en cours.</span><span class="sxs-lookup"><span data-stu-id="8c34d-509">Visualization of the spatial mesh tell users scanning is in progress.</span></span> <span data-ttu-id="8c34d-510">Utilisateur clairement sait quoi faire lorsque l’analyse démarre et s’arrête.</span><span class="sxs-lookup"><span data-stu-id="8c34d-510">User clearly knows what to do and when the scan starts and stops.</span></span> | <span data-ttu-id="8c34d-511">Visualisation de la maille spatiale est fournie, mais l’utilisateur ne peut pas clairement savoir comment procéder et aucune information de progression est fournie.</span><span class="sxs-lookup"><span data-stu-id="8c34d-511">Visualization of the spatial mesh is provided, but the user may not clearly know what to do and no progress information is provided.</span></span> | <span data-ttu-id="8c34d-512">Aucune visualisation de la maille.</span><span class="sxs-lookup"><span data-stu-id="8c34d-512">No visualization of mesh.</span></span> <span data-ttu-id="8c34d-513">Aucune information de conseils fournie à l’utilisateur concernant où rechercher, ou lorsque l’analyse démarre/arrête.</span><span class="sxs-lookup"><span data-stu-id="8c34d-513">No guidance information provided to the user regarding where to look, or when the scan starts/stops.</span></span> |

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-514">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-514">How to measure</span></span>

* <span data-ttu-id="8c34d-515">Lors d’une analyse de l’espace requis, des conseils visuels et audio sont fourni qui indique où rechercher et quand commencer et l’arrêter l’analyse.</span><span class="sxs-lookup"><span data-stu-id="8c34d-515">During a required room scan, visual and audio guidance is provided indicating where to look, and when to start and stop scanning.</span></span>

### <a name="recommendations"></a><span data-ttu-id="8c34d-516">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-516">Recommendations</span></span>

* <span data-ttu-id="8c34d-517">Indique la quantité du volume total à proximité des utilisateurs doit faire partie de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="8c34d-517">Indicate how much of the total volume in the users vicinity needs to be part of the experience.</span></span>
* <span data-ttu-id="8c34d-518">Communiquer lors de l’analyse démarre et s’arrête comme un indicateur de progression.</span><span class="sxs-lookup"><span data-stu-id="8c34d-518">Communicate when the scan starts and stops such as a progress indicator.</span></span>
* <span data-ttu-id="8c34d-519">Utiliser une visualisation de la maille lors de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="8c34d-519">Use a visualization of the mesh during the scan.</span></span>
* <span data-ttu-id="8c34d-520">Fournir des signaux visuels et audio pour inciter l’utilisateur à rechercher et vous déplacer dans la salle.</span><span class="sxs-lookup"><span data-stu-id="8c34d-520">Provide visual and audio cues to encourage the user to look and move around the room.</span></span>
* <span data-ttu-id="8c34d-521">Informer l’utilisateur où aller pour améliorer les données.</span><span class="sxs-lookup"><span data-stu-id="8c34d-521">Inform the user where to go to improve the data.</span></span> <span data-ttu-id="8c34d-522">Dans de nombreux cas, il peut être préférable d’indiquer à l’utilisateur de ce qu’ils doivent (par exemple, examinez le plafond, recherchez derrière meubles), afin d’obtenir la qualité d’analyse nécessaires.</span><span class="sxs-lookup"><span data-stu-id="8c34d-522">In many cases, it may be best to tell the user what they need to do (e.g. look at the ceiling, look behind furniture), in order to get the necessary scan quality.</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-523">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-523">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="8c34d-524">Documentation</span><span class="sxs-lookup"><span data-stu-id="8c34d-524">Documentation</span></span>

* [<span data-ttu-id="8c34d-525">Visualisation d’analyse de salle</span><span class="sxs-lookup"><span data-stu-id="8c34d-525">Room scan visualization</span></span>](room-scan-visualization.md)
* [<span data-ttu-id="8c34d-526">Étude de cas : Développer les capacités de mappage spatial d’HoloLens</span><span class="sxs-lookup"><span data-stu-id="8c34d-526">Case study: Expanding the spatial mapping capabilities of HoloLens</span></span>](case-study-expanding-the-spatial-mapping-capabilities-of-hololens.md)
* [<span data-ttu-id="8c34d-527">Étude de cas : Spatiale sonorisation pour HoloTour</span><span class="sxs-lookup"><span data-stu-id="8c34d-527">Case study: Spatial sound design for HoloTour</span></span>](case-study-spatial-sound-design-for-holotour.md)
* [<span data-ttu-id="8c34d-528">Étude de cas : Création d’une expérience d’immersion dans les Fragments</span><span class="sxs-lookup"><span data-stu-id="8c34d-528">Case study: Creating an immersive experience in Fragments</span></span>](case-study-creating-an-immersive-experience-in-fragments.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="8c34d-529">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="8c34d-529">Tools and tutorials</span></span>

* [<span data-ttu-id="8c34d-530">Réalité mixte Toolkit - UX</span><span class="sxs-lookup"><span data-stu-id="8c34d-530">Mixed Reality Toolkit - UX</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/UX)

## <a name="directional-indicators"></a><span data-ttu-id="8c34d-531">Indicateurs directionnels</span><span class="sxs-lookup"><span data-stu-id="8c34d-531">Directional indicators</span></span>

<span data-ttu-id="8c34d-532">Dans une application de réalité mixte, le contenu peut être à l’extérieur du champ de vue ou bloqués par les objets du monde réel.</span><span class="sxs-lookup"><span data-stu-id="8c34d-532">In a mixed reality app, content may be outside the field of view or occluded by real-world objects.</span></span> <span data-ttu-id="8c34d-533">Une application bien conçue rend plus facile pour l’utilisateur rechercher du contenu non visibles.</span><span class="sxs-lookup"><span data-stu-id="8c34d-533">A well designed app will make it easier for the user to find non-visible content.</span></span> <span data-ttu-id="8c34d-534">Indicateurs directionnels alerter un utilisateur au contenu important et fournissent des conseils pour le contenu par rapport à la position de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-534">Directional indicators alert a user to important content and provide guidance to the content relative to the user's position.</span></span> <span data-ttu-id="8c34d-535">Conseils pour le contenu non visible peuvent prendre la forme d’émetteurs audio, flèches de direction ou des signaux visuels directs.</span><span class="sxs-lookup"><span data-stu-id="8c34d-535">Guidance to non-visible content can take the form of sound emitters, directional arrows, or direct visual cues.</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-536">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-536">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-537"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-537"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-538"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-538"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-539">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-539">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="8c34d-540">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-540">✔️</span></span></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-541">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-541">Quality criteria</span></span>

|  <span data-ttu-id="8c34d-542">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-542">Best</span></span>  |  <span data-ttu-id="8c34d-543">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-543">Meets</span></span> |  <span data-ttu-id="8c34d-544">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-544">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="8c34d-545">Les signaux visuels et audio guident directement vers le contenu approprié à l’extérieur du champ de vue.</span><span class="sxs-lookup"><span data-stu-id="8c34d-545">Visual and audio cues directly guide the user to relevant content outside the field of view.</span></span> | <span data-ttu-id="8c34d-546">Une flèche ou un indicateur qui pointe vers l’utilisateur de la direction générale du contenu.</span><span class="sxs-lookup"><span data-stu-id="8c34d-546">An arrow or some indicator that points the user in the general direction of the content.</span></span> | <span data-ttu-id="8c34d-547">Le contenu approprié est en dehors du champ de vue et une mauvaise ou aucun guide de l’emplacement n’est fourni à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-547">Relevant content is outside of the field of view, and poor or no location guidance is provided to the user.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-548">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-548">How to measure</span></span>

* <span data-ttu-id="8c34d-549">Le contenu approprié en dehors de l’utilisateur champ de vision est détectable par le biais des signaux visual et/ou audio.</span><span class="sxs-lookup"><span data-stu-id="8c34d-549">Relevant content outside of the user field of view is discoverable through visual and/or audio cues.</span></span>

### <a name="recommendations"></a><span data-ttu-id="8c34d-550">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-550">Recommendations</span></span>

* <span data-ttu-id="8c34d-551">Lorsque le contenu approprié est en dehors du champ de vision de l’utilisateur, utiliser des indicateurs directionnels et signaux audio pour guider l’utilisateur au contenu.</span><span class="sxs-lookup"><span data-stu-id="8c34d-551">When relevant content is outside the user's field of view, use directional indicators and audio cues to guide the user to the content.</span></span> <span data-ttu-id="8c34d-552">Dans de nombreux cas, un guide visuel direct est préféré sur les flèches de direction.</span><span class="sxs-lookup"><span data-stu-id="8c34d-552">In many cases, a direct visual guide is preferred over directional arrows.</span></span>
* <span data-ttu-id="8c34d-553">Les indicateurs de directionnelles ne doivent pas être créés dans le curseur.</span><span class="sxs-lookup"><span data-stu-id="8c34d-553">Directional indicators should not be built into the cursor.</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-554">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-554">Resources</span></span>

* [<span data-ttu-id="8c34d-555">Frame HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="8c34d-555">Holographic frame</span></span>](holographic-frame.md)

## <a name="data-loading"></a><span data-ttu-id="8c34d-556">Chargement des données</span><span class="sxs-lookup"><span data-stu-id="8c34d-556">Data loading</span></span>

<span data-ttu-id="8c34d-557">Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours.</span><span class="sxs-lookup"><span data-stu-id="8c34d-557">A progress control provides feedback to the user that a long-running operation is underway.</span></span> <span data-ttu-id="8c34d-558">Cela peut signifier que l’utilisateur ne peut pas interagir avec l’application lorsque l’indicateur de progression est visible et peut également indiquer la durée pendant laquelle le délai d’attente peut être.</span><span class="sxs-lookup"><span data-stu-id="8c34d-558">It can mean that the user cannot interact with the app when the progress indicator is visible and can also indicate how long the wait time might be.</span></span>

### <a name="device-impact"></a><span data-ttu-id="8c34d-559">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="8c34d-559">Device impact</span></span>

<table>
<tr>
<th style="width:150px"> <span data-ttu-id="8c34d-560"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-560"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8c34d-561"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8c34d-561"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td style="text-align: center;"> <span data-ttu-id="8c34d-562">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-562">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="8c34d-563">✔️</span><span class="sxs-lookup"><span data-stu-id="8c34d-563">✔️</span></span></td>
</tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="8c34d-564">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="8c34d-564">Quality criteria</span></span>

|  <span data-ttu-id="8c34d-565">Meilleur</span><span class="sxs-lookup"><span data-stu-id="8c34d-565">Best</span></span>  |  <span data-ttu-id="8c34d-566">Répond à</span><span class="sxs-lookup"><span data-stu-id="8c34d-566">Meets</span></span> |  <span data-ttu-id="8c34d-567">Échec</span><span class="sxs-lookup"><span data-stu-id="8c34d-567">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="8c34d-568">Indicateur visuel animée, sous la forme d’une barre de progression ou un anneau, affichant la progression au cours de toutes les données du chargement ou de traitement.</span><span class="sxs-lookup"><span data-stu-id="8c34d-568">Animated visual indicator, in the form of a progress bar or ring, showing progress during any data loading or processing.</span></span> <span data-ttu-id="8c34d-569">L’indicateur visuel fournit des conseils sur la durée pendant laquelle l’attente pourrait être.</span><span class="sxs-lookup"><span data-stu-id="8c34d-569">The visual indicator provides guidance on how long the wait could be.</span></span> | <span data-ttu-id="8c34d-570">L’utilisateur est informé que le chargement des données est en cours d’exécution, mais il n’existe aucune indication de la durée pendant laquelle l’attente peut être.</span><span class="sxs-lookup"><span data-stu-id="8c34d-570">User is informed that data loading is in progress, but there is no indication of how long the wait could be.</span></span> | <span data-ttu-id="8c34d-571">Aucun lors du chargement de données ou les indicateurs de processus pour la tâche prend plus de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="8c34d-571">No data loading or process indicators for task taking longer than 5 seconds.</span></span> |

### <a name="how-to-measure"></a><span data-ttu-id="8c34d-572">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="8c34d-572">How to measure</span></span>

* <span data-ttu-id="8c34d-573">Pendant le chargement de données vérifier le que état n’est pas vide pendant plus de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="8c34d-573">During data loading verify there is no blank state for more than 5 seconds.</span></span>

### <a name="recommendations"></a><span data-ttu-id="8c34d-574">Recommandations</span><span class="sxs-lookup"><span data-stu-id="8c34d-574">Recommendations</span></span>

* <span data-ttu-id="8c34d-575">Fournir une d’animation de chargement de données affichant la progression dans n’importe quelle situation lorsque l’utilisateur peut-être percevoir cette application est bloqué ou est tombé en panne.</span><span class="sxs-lookup"><span data-stu-id="8c34d-575">Provide a data loading animator showing progress in any situation when the user may perceive this app to have stalled or crashed.</span></span> <span data-ttu-id="8c34d-576">Une règle empirique raisonnable est toute activité « chargement » qui peut prendre plus de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="8c34d-576">A reasonable rule of thumb is any 'loading' activity that could take more than 5 seconds.</span></span>

### <a name="resources"></a><span data-ttu-id="8c34d-577">Ressources</span><span class="sxs-lookup"><span data-stu-id="8c34d-577">Resources</span></span>

* [<span data-ttu-id="8c34d-578">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="8c34d-578">Displaying progress</span></span>](progress.md)
