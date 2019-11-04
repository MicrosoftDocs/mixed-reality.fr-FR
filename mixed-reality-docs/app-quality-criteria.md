---
title: Critères de qualité des applications
description: Ce document décrit les principaux facteurs qui ont un impact sur la qualité des applications de réalité mixte.
author: cjdgit
ms.author: crderr
ms.date: 03/21/2018
ms.topic: article
keywords: critères de qualité des applications, réalité mixte, application de réalité mixte
ms.openlocfilehash: f98111ebe9aacc30778e86501be41e6ac5f6d165
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437050"
---
# <a name="app-quality-criteria"></a><span data-ttu-id="20992-104">Critères de qualité des applications</span><span class="sxs-lookup"><span data-stu-id="20992-104">App quality criteria</span></span>

<span data-ttu-id="20992-105">Ce document décrit les principaux facteurs qui ont un impact sur la qualité des applications de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="20992-105">This document describes the top factors impacting the quality of mixed reality apps.</span></span> <span data-ttu-id="20992-106">Pour chaque facteur, les informations suivantes sont fournies</span><span class="sxs-lookup"><span data-stu-id="20992-106">For each factor the following information is provided</span></span>
* <span data-ttu-id="20992-107">Vue d’ensemble : brève description du facteur de qualité et de la raison pour laquelle il est important.</span><span class="sxs-lookup"><span data-stu-id="20992-107">Overview – a brief description of the quality factor and why it is important.</span></span>
* <span data-ttu-id="20992-108">Impact sur l’appareil : le type de l’appareil de la réalité mixte de la fenêtre est affecté.</span><span class="sxs-lookup"><span data-stu-id="20992-108">Device impact - which type of Window Mixed Reality device is impacted.</span></span>
* <span data-ttu-id="20992-109">Critères de qualité : comment évaluer le facteur de qualité.</span><span class="sxs-lookup"><span data-stu-id="20992-109">Quality criteria – how to evaluate the quality factor.</span></span>
* <span data-ttu-id="20992-110">Comment mesurer : méthodes pour mesurer (ou expérimenter) le problème.</span><span class="sxs-lookup"><span data-stu-id="20992-110">How to measure – methods to measure (or experience) the issue.</span></span>
* <span data-ttu-id="20992-111">Recommandations : Résumé des approches pour offrir une meilleure expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-111">Recommendations – summary of approaches to provide a better user experience.</span></span>
* <span data-ttu-id="20992-112">Ressources : ressources de conception et de développement pertinentes qui sont utiles pour créer de meilleures expériences d’application.</span><span class="sxs-lookup"><span data-stu-id="20992-112">Resources – relevant developer and design resources that are useful to create better app experiences.</span></span>

## <a name="frame-rate"></a><span data-ttu-id="20992-113">Fréquence d’images</span><span class="sxs-lookup"><span data-stu-id="20992-113">Frame rate</span></span>

<span data-ttu-id="20992-114">La fréquence d’images est le premier pilier de la stabilité de l’hologramme et du confort de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-114">Frame rate is the first pillar of hologram stability and user comfort.</span></span> <span data-ttu-id="20992-115">La fréquence d’images en dessous des cibles recommandées peut provoquer l’apparition d’hologrammes, ce qui a un impact négatif sur la qualité de l’expérience et éventuellement une fatigue oculaire.</span><span class="sxs-lookup"><span data-stu-id="20992-115">Frame rate below the recommended targets can cause holograms to appear jittery, negatively impacting the believability of the experience and potentially causing eye fatigue.</span></span> <span data-ttu-id="20992-116">La fréquence d’images cible pour votre expérience sur les casques immersifs Windows Mixed Reality est 60 Hz ou 90Hz, selon les PC compatibles Windows Mixed realer que vous souhaitez prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="20992-116">The target frame rate for your experience on Windows Mixed Reality immersive headsets will be either 60Hz or 90Hz depending on which Windows Mixed Reality Compatible PCs you wish to support.</span></span> <span data-ttu-id="20992-117">Pour HoloLens, la fréquence d’images cible est 60 Hz.</span><span class="sxs-lookup"><span data-stu-id="20992-117">For HoloLens the target frame rate is 60Hz.</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-118">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-118">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-119"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-119"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-120"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-120"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-121">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-121">✔️</span></span></td>
        <td><span data-ttu-id="20992-122">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-122">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-123">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-123">Quality criteria</span></span>

|  <span data-ttu-id="20992-124">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-124">Best</span></span>  |  <span data-ttu-id="20992-125">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-125">Meets</span></span> |  <span data-ttu-id="20992-126">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-126">Fail</span></span> |
--- | --- | ---
| <span data-ttu-id="20992-127">L’application répond régulièrement à l’objectif des images par seconde (FPS) pour l’appareil cible : 60fps sur HoloLens ; 90fps sur ultra PC ; et 60fps sur les PC grand public.</span><span class="sxs-lookup"><span data-stu-id="20992-127">The app consistently meets frames per second (FPS) goal for target device: 60fps on HoloLens; 90fps on Ultra PCs; and 60fps on mainstream PCs.</span></span> | <span data-ttu-id="20992-128">L’application présente des interruptions intermittentes de la trame sans gêner l’expérience de base. ou la valeur FPS est toujours inférieure à l’objectif souhaité, mais n’empêche pas l’expérience de l’application.</span><span class="sxs-lookup"><span data-stu-id="20992-128">The app has intermittent frame drops not impeding the core experience; or FPS is consistently lower than desired goal but doesn’t impede the app experience.</span></span> | <span data-ttu-id="20992-129">L’application rencontre une baisse de la fréquence d’images en moyenne toutes les dix secondes ou moins.</span><span class="sxs-lookup"><span data-stu-id="20992-129">The app is experiencing a drop in frame rate on average every ten seconds or less.</span></span> |

### <a name="how-to-measure"></a><span data-ttu-id="20992-130">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-130">How to measure</span></span>

* <span data-ttu-id="20992-131">Un graphique de fréquence d’images en temps réel est fourni par le biais du [portail d’appareils Windows](using-the-windows-device-portal.md#system-performance) sous « performances système ».</span><span class="sxs-lookup"><span data-stu-id="20992-131">A real-time frame rate graph is provided through by the [Windows Device Portal](using-the-windows-device-portal.md#system-performance) under "System Performance".</span></span>
* <span data-ttu-id="20992-132">Pour le débogage de développement, ajoutez un compteur de diagnostic de fréquence d’images dans l’application.</span><span class="sxs-lookup"><span data-stu-id="20992-132">For development debugging, add a frame rate diagnostic counter into the app.</span></span> <span data-ttu-id="20992-133">Consultez ressources pour obtenir un exemple de compteur.</span><span class="sxs-lookup"><span data-stu-id="20992-133">See Resources for a sample counter.</span></span>
* <span data-ttu-id="20992-134">Les chutes de fréquence d’images peuvent être rencontrées dans l’appareil pendant que l’application est en cours d’exécution en déplaçant votre tête d’un côté à l’autre.</span><span class="sxs-lookup"><span data-stu-id="20992-134">Frame rate drops can be experienced in device while the app is running by moving your head from side to side.</span></span> <span data-ttu-id="20992-135">Si l’hologramme présente un mouvement instable inattendue, la fréquence d’images faible ou le plan de stabilité est probablement la cause.</span><span class="sxs-lookup"><span data-stu-id="20992-135">If the hologram shows unexpected jittery movement, then low frame rate or the stability plane is likely the cause.</span></span>

### <a name="recommendations"></a><span data-ttu-id="20992-136">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-136">Recommendations</span></span>

* <span data-ttu-id="20992-137">Ajoutez un compteur de fréquence d’images au début du travail de développement.</span><span class="sxs-lookup"><span data-stu-id="20992-137">Add a frame rate counter at the beginning of the development work.</span></span>
* <span data-ttu-id="20992-138">Les modifications qui entraînent une chute de la fréquence d’images doivent être évaluées et résolues de manière appropriée en tant que bogue de performance.</span><span class="sxs-lookup"><span data-stu-id="20992-138">Changes that incur a drop in frame rate should be evaluated and appropriately resolved as a performance bug.</span></span>

### <a name="resources"></a><span data-ttu-id="20992-139">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-139">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="20992-140">Documentation</span><span class="sxs-lookup"><span data-stu-id="20992-140">Documentation</span></span>

* [<span data-ttu-id="20992-141">Comprendre les performances de la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="20992-141">Understanding Performance for Mixed Reality</span></span>](understanding-performance-for-mixed-reality.md)
* [<span data-ttu-id="20992-142">Stabilité et fréquence d’hologramme</span><span class="sxs-lookup"><span data-stu-id="20992-142">Hologram stability and framerate</span></span>](hologram-stability.md#frame-rate)
* [<span data-ttu-id="20992-143">Budget des performances des actifs</span><span class="sxs-lookup"><span data-stu-id="20992-143">Asset performance budget</span></span>](asset-creation-process.md)
* [<span data-ttu-id="20992-144">Recommandations de performances pour Unity</span><span class="sxs-lookup"><span data-stu-id="20992-144">Performance recommendations for Unity</span></span>](performance-recommendations-for-unity.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="20992-145">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="20992-145">Tools and tutorials</span></span>

* [<span data-ttu-id="20992-146">MRToolkit, affichage du compteur FPS</span><span class="sxs-lookup"><span data-stu-id="20992-146">MRToolkit, FPS counter display</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Utilities/README.md)
* [<span data-ttu-id="20992-147">MRToolkit, nuanceurs</span><span class="sxs-lookup"><span data-stu-id="20992-147">MRToolkit, Shaders</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Utilities/Shaders)

#### <a name="external-references"></a><span data-ttu-id="20992-148">Références externes</span><span class="sxs-lookup"><span data-stu-id="20992-148">External references</span></span>

* [<span data-ttu-id="20992-149">Unity, optimisation des applications mobiles</span><span class="sxs-lookup"><span data-stu-id="20992-149">Unity, Optimizing mobile applications</span></span>](https://www.youtube.com/watch?v=j4YAY36xjwE)

## <a name="hologram-stability"></a><span data-ttu-id="20992-150">Stabilité de l’hologramme</span><span class="sxs-lookup"><span data-stu-id="20992-150">Hologram stability</span></span>

<span data-ttu-id="20992-151">Les hologrammes stables augmenteront la convivialité et l’incroyableté de votre application et créeront une expérience d’affichage plus confortable pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-151">Stable holograms will increase the usability and believability of your app, and create a more comfortable viewing experience for the user.</span></span> <span data-ttu-id="20992-152">La qualité de la stabilité des hologrammes résulte d’un développement d’applications correct et de la capacité de l’appareil à comprendre (suivre) son environnement.</span><span class="sxs-lookup"><span data-stu-id="20992-152">The quality of hologram stability is a result of good app development and the device's ability to understand (track) its environment.</span></span> <span data-ttu-id="20992-153">Alors que la fréquence d’images est le premier pilier de la stabilité, d’autres facteurs peuvent avoir un impact sur la stabilité, notamment :</span><span class="sxs-lookup"><span data-stu-id="20992-153">While frame rate is the first pillar of stability, other factors can impact stability including:</span></span>

* <span data-ttu-id="20992-154">Utilisation du plan de stabilisation</span><span class="sxs-lookup"><span data-stu-id="20992-154">Use of the stabilization plane</span></span>
* <span data-ttu-id="20992-155">Distance aux ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="20992-155">Distance to spatial anchors</span></span>
* <span data-ttu-id="20992-156">Suivre</span><span class="sxs-lookup"><span data-stu-id="20992-156">Tracking</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-157">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-157">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-158"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-158"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-159"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-159"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-160">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-160">✔️</span></span></td>
        <td>❌</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-161">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-161">Quality criteria</span></span>

|  <span data-ttu-id="20992-162">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-162">Best</span></span>  |  <span data-ttu-id="20992-163">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-163">Meets</span></span> |  <span data-ttu-id="20992-164">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-164">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="20992-165">Les hologrammes semblent constamment stables.</span><span class="sxs-lookup"><span data-stu-id="20992-165">Holograms consistently appear stable.</span></span> | <span data-ttu-id="20992-166">Le contenu secondaire présente un mouvement inattendu ; ou un mouvement inattendu ne fait pas obstacle à l’expérience globale de l’application.</span><span class="sxs-lookup"><span data-stu-id="20992-166">Secondary content exhibits unexpected movement; or unexpected movement does not impede overall app experience.</span></span> | <span data-ttu-id="20992-167">Le contenu principal du cadre présente un mouvement inattendu.</span><span class="sxs-lookup"><span data-stu-id="20992-167">Primary content in frame exhibits unexpected movement.</span></span> |

### <a name="how-to-measure"></a><span data-ttu-id="20992-168">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-168">How to measure</span></span>

<span data-ttu-id="20992-169">Lors de l’usure de l’appareil et de l’affichage de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="20992-169">While wearing the device and viewing the experience:</span></span>

* <span data-ttu-id="20992-170">Déplacez votre tête d’un côté à l’autre, si les hologrammes affichent un mouvement inattendu, alors une fréquence d’images faible ou un alignement incorrect du plan de stabilité sur le plan focal est la cause probable.</span><span class="sxs-lookup"><span data-stu-id="20992-170">Move your head from side to side, if the holograms show unexpected movement then low frame rate or improper alignment of the stability plane to the focal plane is the likely cause.</span></span>
* <span data-ttu-id="20992-171">Déplacez-vous autour des hologrammes et de l’environnement, recherchez des comportements tels que natation et jumpiness.</span><span class="sxs-lookup"><span data-stu-id="20992-171">Move around the holograms and environment, look for behaviors such as swim and jumpiness.</span></span> <span data-ttu-id="20992-172">Ce type de mouvement est probablement dû au fait que l’appareil n’effectue pas le suivi de l’environnement ou à la distance vers l’ancrage spatial.</span><span class="sxs-lookup"><span data-stu-id="20992-172">This type of motion is likely caused by the device not tracking the environment, or the distance to the spatial anchor.</span></span>
* <span data-ttu-id="20992-173">Si un grand nombre ou plusieurs hologrammes se trouvent dans le cadre, observez le comportement de l’hologramme à différentes profondes tout en déplaçant la position de votre tête d’un côté à l’autre, si shakiness apparaît que cela est probablement dû au plan de stabilisation.</span><span class="sxs-lookup"><span data-stu-id="20992-173">If large or multiple holograms are in the frame, observe hologram behavior at various depths while moving your head position from side to side, if shakiness appears this is likely caused by the stabilization plane.</span></span>

### <a name="recomendations"></a><span data-ttu-id="20992-174">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-174">Recomendations</span></span>

* <span data-ttu-id="20992-175">Ajoutez un compteur de fréquence d’images au début du travail de développement.</span><span class="sxs-lookup"><span data-stu-id="20992-175">Add an frame rate counter at the beginning of the development work.</span></span>
* <span data-ttu-id="20992-176">Utilisez le plan de stabilisation.</span><span class="sxs-lookup"><span data-stu-id="20992-176">Use the stabilization plane.</span></span>
* <span data-ttu-id="20992-177">Affichez toujours les hologrammes ancrés dans les 3 mètres de leur ancrage.</span><span class="sxs-lookup"><span data-stu-id="20992-177">Always render anchored holograms within 3 meters of their anchor.</span></span>
* <span data-ttu-id="20992-178">Assurez-vous que votre environnement est configuré pour un suivi correct.</span><span class="sxs-lookup"><span data-stu-id="20992-178">Make sure your environment is setup for proper tracking.</span></span>
* <span data-ttu-id="20992-179">Concevez votre expérience afin d’éviter les hologrammes à différents niveaux de profondeur focale dans le cadre.</span><span class="sxs-lookup"><span data-stu-id="20992-179">Design your experience to avoid holograms at various focal depth levels within the frame.</span></span>

### <a name="resources"></a><span data-ttu-id="20992-180">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-180">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="20992-181">Documentation</span><span class="sxs-lookup"><span data-stu-id="20992-181">Documentation</span></span>

* [<span data-ttu-id="20992-182">Stabilité et fréquence d’hologramme</span><span class="sxs-lookup"><span data-stu-id="20992-182">Hologram stability and framerate</span></span>](hologram-stability.md#frame-rate)
* [<span data-ttu-id="20992-183">Étude de cas, à l’aide du plan de stabilisation</span><span class="sxs-lookup"><span data-stu-id="20992-183">Case study, Using the stabilization plane</span></span>](case-study-using-the-stabilization-plane-to-reduce-holographic-turbulence.md)
* [<span data-ttu-id="20992-184">Comprendre les performances de la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="20992-184">Understanding Performance for Mixed Reality</span></span>](understanding-performance-for-mixed-reality.md)
* [<span data-ttu-id="20992-185">Recommandations de performances pour Unity</span><span class="sxs-lookup"><span data-stu-id="20992-185">Performance recommendations for Unity</span></span>](performance-recommendations-for-unity.md)
* [<span data-ttu-id="20992-186">Ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="20992-186">Spatial anchors</span></span>](spatial-anchors.md)
* [<span data-ttu-id="20992-187">Gestion des erreurs de suivi</span><span class="sxs-lookup"><span data-stu-id="20992-187">Handling tracking errors</span></span>](coordinate-systems.md#handling-tracking-errors)
* [<span data-ttu-id="20992-188">Cadre de référence stationnaire</span><span class="sxs-lookup"><span data-stu-id="20992-188">Stationary frame of reference</span></span>](coordinate-systems.md#stationary-frame-of-reference)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="20992-189">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="20992-189">Tools and tutorials</span></span>

* [<span data-ttu-id="20992-190">Kit de complément MR, IPD Kinect</span><span class="sxs-lookup"><span data-stu-id="20992-190">MR Companion Kit, Kinect IPD</span></span>](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/KinectIPD)

## <a name="holograms-position-on-real-surfaces"></a><span data-ttu-id="20992-191">Position des hologrammes sur les surfaces réelles</span><span class="sxs-lookup"><span data-stu-id="20992-191">Holograms position on real surfaces</span></span>

<span data-ttu-id="20992-192">Un mauvais alignement des hologrammes avec des objets physiques (s’ils sont destinés à être placés les uns par rapport aux autres) est une indication claire de l’absence d’Union des hologrammes et du monde réel.</span><span class="sxs-lookup"><span data-stu-id="20992-192">Misalignments of holograms with physical objects (if intended to be placed in relation to one another) is a clear indication of the non-union of holograms and real-world.</span></span> <span data-ttu-id="20992-193">La précision de la position doit être relative aux besoins du scénario ; par exemple, le positionnement de surface général peut utiliser la carte spatiale, mais un positionnement plus précis nécessitera l’utilisation de marqueurs et d’étalonnage.</span><span class="sxs-lookup"><span data-stu-id="20992-193">Accuracy of the placement should be relative to the needs of the scenario; for example, general surface placement can use the spatial map, but more accurate placement will require some use of markers and calibration.</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-194">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-194">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-195"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-195"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-196"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-196"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-197">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-197">✔️</span></span></td>
        <td>❌</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-198">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-198">Quality criteria</span></span>

|  <span data-ttu-id="20992-199">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-199">Best</span></span>  |  <span data-ttu-id="20992-200">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-200">Meets</span></span> |  <span data-ttu-id="20992-201">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-201">Fail</span></span> |
--- | --- | ---
| <span data-ttu-id="20992-202">Les hologrammes s’alignent sur la surface généralement dans la plage de centimètres en pouces.</span><span class="sxs-lookup"><span data-stu-id="20992-202">Holograms align to the surface typically in the centimeters to inches range.</span></span> <span data-ttu-id="20992-203">Si une plus grande précision est requise, l’application doit fournir un moyen efficace de collaboration au sein de la spécification de l’application souhaitée.</span><span class="sxs-lookup"><span data-stu-id="20992-203">If more accuracy is required, the app should provide an efficient means for collaboration within the desired app spec.</span></span> | <span data-ttu-id="20992-204">N/A</span><span class="sxs-lookup"><span data-stu-id="20992-204">NA</span></span> | <span data-ttu-id="20992-205">Les hologrammes apparaissent non alignés avec l’objet cible physique en rompant le plan de surface ou en s’éloignant de l’aire.</span><span class="sxs-lookup"><span data-stu-id="20992-205">The holograms appear unaligned with the physical target object by either breaking the surface plane or appearing to float away from the surface.</span></span> <span data-ttu-id="20992-206">Si la précision est requise, les hologrammes doivent répondre aux spécifications de proximité du scénario.</span><span class="sxs-lookup"><span data-stu-id="20992-206">If accuracy is required, Holograms should meet the proximity spec of the scenario.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="20992-207">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-207">How to measure</span></span>

* <span data-ttu-id="20992-208">Les hologrammes placés sur la carte spatiale ne doivent pas sembler très flotter au-dessus ou en dessous de la surface.</span><span class="sxs-lookup"><span data-stu-id="20992-208">Holograms that are placed on spatial map should not appear to dramatically float above or below the surface.</span></span>
* <span data-ttu-id="20992-209">Les hologrammes qui nécessitent un placement précis doivent avoir une forme de système de marqueur et de système d’étalonnage qui est précis à l’exigence du scénario.</span><span class="sxs-lookup"><span data-stu-id="20992-209">Holograms that require accurate placement should have some form of marker and calibration system that is accurate to the scenario's requirement.</span></span>

### <a name="recommendations"></a><span data-ttu-id="20992-210">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-210">Recommendations</span></span>

* <span data-ttu-id="20992-211">La carte spatiale est utile pour placer des objets sur des surfaces lorsque la précision n’est pas requise.</span><span class="sxs-lookup"><span data-stu-id="20992-211">Spatial map is useful for placing objects on surfaces when precision isn’t required.</span></span>
* <span data-ttu-id="20992-212">Pour une meilleure précision, utilisez des marqueurs ou des affiches pour définir les hologrammes et un contrôleur Xbox (ou un mécanisme d’alignement manuel) pour l’étalonnage final.</span><span class="sxs-lookup"><span data-stu-id="20992-212">For the best precision, use markers or posters to set the holograms and an Xbox controller (or some manual alignment mechanism) for final calibration.</span></span>
* <span data-ttu-id="20992-213">Envisagez de casser des hologrammes très grands en parties logiques et en alignant chaque partie sur l’aire de conception.</span><span class="sxs-lookup"><span data-stu-id="20992-213">Consider breaking extra-large holograms into logical parts and aligning each part to the surface.</span></span>
* <span data-ttu-id="20992-214">Une distance incorrecte (IPD) peut également affecter l’alignement de l’hologramme.</span><span class="sxs-lookup"><span data-stu-id="20992-214">Improperly set interpupilary distance (IPD) can also effect hologram alignment.</span></span> <span data-ttu-id="20992-215">Configurez toujours HoloLens sur l’IPD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-215">Always configure HoloLens to the user's IPD.</span></span>

### <a name="resources"></a><span data-ttu-id="20992-216">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-216">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="20992-217">Documentation</span><span class="sxs-lookup"><span data-stu-id="20992-217">Documentation</span></span>

* [<span data-ttu-id="20992-218">Positionnement du mappage spatial</span><span class="sxs-lookup"><span data-stu-id="20992-218">Spatial mapping placement</span></span>](spatial-mapping.md#placement)
* [<span data-ttu-id="20992-219">Processus d’analyse de la salle</span><span class="sxs-lookup"><span data-stu-id="20992-219">Room scanning process</span></span>](case-study-expanding-the-spatial-mapping-capabilities-of-hololens.md)
* [<span data-ttu-id="20992-220">Meilleures pratiques pour les ancrages spatiaux</span><span class="sxs-lookup"><span data-stu-id="20992-220">Spatial anchors best practices</span></span>](spatial-anchors.md#best-practices)
* [<span data-ttu-id="20992-221">Gestion des erreurs de suivi</span><span class="sxs-lookup"><span data-stu-id="20992-221">Handling tracking errors</span></span>](coordinate-systems.md#handling-tracking-errors)
* [<span data-ttu-id="20992-222">Mappage spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="20992-222">Spatial mapping in Unity</span></span>](spatial-mapping-in-unity.md)
* [<span data-ttu-id="20992-223">Présentation du développement Vuforia</span><span class="sxs-lookup"><span data-stu-id="20992-223">Vuforia development overview</span></span>](vuforia-development-overview.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="20992-224">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="20992-224">Tools and tutorials</span></span>

* [<span data-ttu-id="20992-225">MR spatial 230 : mappage spatial</span><span class="sxs-lookup"><span data-stu-id="20992-225">MR Spatial 230: Spatial mapping</span></span>](holograms-230.md)
* [<span data-ttu-id="20992-226">Boîte à outils MR, bibliothèques de mappage spatiale</span><span class="sxs-lookup"><span data-stu-id="20992-226">MR Toolkit, Spatial Mapping Libraries</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/SpatialMapping/README.md)
* [<span data-ttu-id="20992-227">Kit de complément MR, exemple d’étalonnage d’affiches</span><span class="sxs-lookup"><span data-stu-id="20992-227">MR Companion Kit, Poster Calibration Sample</span></span>](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/PosterCalibrationSample)
* [<span data-ttu-id="20992-228">Kit de complément MR, IPD Kinect</span><span class="sxs-lookup"><span data-stu-id="20992-228">MR Companion Kit, Kinect IPD</span></span>](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/KinectIPD)

#### <a name="external-references"></a><span data-ttu-id="20992-229">Références externes</span><span class="sxs-lookup"><span data-stu-id="20992-229">External references</span></span>

* [<span data-ttu-id="20992-230">Étude de cas Lowes, alignement de précision</span><span class="sxs-lookup"><span data-stu-id="20992-230">Lowes Case Study, Precision alignment</span></span>](https://www.youtube.com/watch?v=LceMdyKZ4PI)

## <a name="viewing-zone-of-comfort"></a><span data-ttu-id="20992-231">Affichage de la zone de confort</span><span class="sxs-lookup"><span data-stu-id="20992-231">Viewing zone of comfort</span></span>

<span data-ttu-id="20992-232">Les développeurs d’applications contrôlent l’emplacement des yeux des utilisateurs en plaçant le contenu et les hologrammes à différents niveaux.</span><span class="sxs-lookup"><span data-stu-id="20992-232">App developers control where users' eyes converge by placing content and holograms at various depths.</span></span> <span data-ttu-id="20992-233">Les utilisateurs qui ont le port HoloLens s’intègrent toujours à la version 2.0 m pour maintenir une image claire, car les affichages HoloLens sont fixés à une distance optique d’environ 2,0 mètres de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-233">Users wearing HoloLens will always accommodate to 2.0m to maintain a clear image because HoloLens displays are fixed at an optical distance approximately 2.0m away from the user.</span></span> <span data-ttu-id="20992-234">Une profondeur de contenu incorrecte peut entraîner une gêne visuelle ou une fatigue.</span><span class="sxs-lookup"><span data-stu-id="20992-234">Improper content depth can lead to visual discomfort or fatigue.</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-235">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-235">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-236"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-236"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-237"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-237"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-238">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-238">✔️</span></span></td>
        <td>❌</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-239">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-239">Quality criteria</span></span>

<table>
<tr>
<td> <span data-ttu-id="20992-240">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-240">Best</span></span> </td><td><ul>
<li><span data-ttu-id="20992-241">Placez le contenu à 2 m.</span><span class="sxs-lookup"><span data-stu-id="20992-241">Place content at 2m.</span></span></li><li><span data-ttu-id="20992-242">Quand les hologrammes ne peuvent pas être placés à 2 ou 2 millions de conflits entre la convergence et l’hébergement, la zone optimale pour le placement de l’hologramme est comprise entre 1,25 m et 5 m.</span><span class="sxs-lookup"><span data-stu-id="20992-242">When holograms cannot be placed at 2m and conflicts between convergence and accommodation cannot be avoided, the optimal zone for hologram placement is between 1.25m and 5m.</span></span></li><li><span data-ttu-id="20992-243">Dans tous les cas, les concepteurs doivent structurer le contenu pour encourager les utilisateurs à interagir à distance de 1 + m (par exemple, ajuster la taille du contenu et les paramètres de positionnement par défaut).</span><span class="sxs-lookup"><span data-stu-id="20992-243">In every case, designers should structure content to encourage users to interact 1+ m away (e.g. adjust content size and default placement parameters).</span></span></li><li><span data-ttu-id="20992-244">À moins qu’il ne soit spécifiquement pas requis par le scénario, un plan de découpage doit être implémenté avec fadeout à partir de 1 million.</span><span class="sxs-lookup"><span data-stu-id="20992-244">Unless specifically not required by the scenario, a clipping plane should be implement with fadeout starting at 1m.</span></span></li><li><span data-ttu-id="20992-245">Dans les cas où une observation plus proche d’un hologramme motionless est requise, le contenu ne doit pas être plus proche que 50cm.</span><span class="sxs-lookup"><span data-stu-id="20992-245">In cases where closer observation of a motionless hologram is required, the content should not be closer than 50cm.</span></span></li>
</ul></td>
</tr><tr>
<td> <span data-ttu-id="20992-246">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-246">Meets</span></span></td><td> <span data-ttu-id="20992-247">Le contenu se trouve dans le Guide d’affichage et de mouvement, mais il n’utilise pas ou n’utilise pas le plan de découpage.</span><span class="sxs-lookup"><span data-stu-id="20992-247">Content is within the viewing and motion guidance, but improper use or no use of the clipping plane.</span></span></td>
</tr><tr>
<td> <span data-ttu-id="20992-248">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-248">Fail</span></span> </td><td> <span data-ttu-id="20992-249">Le contenu est présenté trop près (généralement &lt;1,25 m, ou &lt;50cm pour les hologrammes fixes nécessitant une observation plus proche.)</span><span class="sxs-lookup"><span data-stu-id="20992-249">Content is presented too close (typically &lt;1.25m, or &lt;50cm for stationary holograms requiring closer observation.)</span></span></td>
</tr>
</table>

### <a name="how-to-measure"></a><span data-ttu-id="20992-250">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-250">How to measure</span></span>

* <span data-ttu-id="20992-251">Le contenu doit généralement être en 2 millions de dollars, mais pas plus près de 1,25 ou plus que 5 m.</span><span class="sxs-lookup"><span data-stu-id="20992-251">Content should typically be 2m away, but no closer than 1.25 or further than 5m.</span></span>
* <span data-ttu-id="20992-252">À quelques exceptions près, la distance de rendu du découpage HoloLens doit être définie sur. 85CM avec fadeout de contenu à partir de 1 million.</span><span class="sxs-lookup"><span data-stu-id="20992-252">With few exceptions, the HoloLens clipping render distance should be set to .85CM with fadeout of content starting at 1m.</span></span> <span data-ttu-id="20992-253">Approchez le contenu et notez l’effet plan de découpage.</span><span class="sxs-lookup"><span data-stu-id="20992-253">Approach the content and note the clipping plane effect.</span></span>
* <span data-ttu-id="20992-254">Le contenu fixe ne doit pas être plus proche de 50cm.</span><span class="sxs-lookup"><span data-stu-id="20992-254">Stationary content should not be closer than 50cm away.</span></span>

### <a name="recommendations"></a><span data-ttu-id="20992-255">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-255">Recommendations</span></span>

* <span data-ttu-id="20992-256">Concevez du contenu pour une distance d’affichage optimale de 2 m.</span><span class="sxs-lookup"><span data-stu-id="20992-256">Design content for the optimal viewing distance of 2m.</span></span>
* <span data-ttu-id="20992-257">Définissez la distance de rendu du découpage sur 85cm avec fadeout de contenu à partir de 1M.</span><span class="sxs-lookup"><span data-stu-id="20992-257">Set the clipping render distance to 85cm with fadeout of content starting at 1m.</span></span>
* <span data-ttu-id="20992-258">Pour les hologrammes fixes qui nécessitent un affichage plus étroit, le plan de découpage ne doit pas être plus proche de 30cm et fadeout doit démarrer au moins 10cm à partir du plan de découpage.</span><span class="sxs-lookup"><span data-stu-id="20992-258">For stationary holograms that need closer viewing, the clipping plane should be no closer than 30cm and fadeout should start at least 10cm away from the clipping plane.</span></span>

### <a name="resources"></a><span data-ttu-id="20992-259">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-259">Resources</span></span>

* [<span data-ttu-id="20992-260">Distance de rendu</span><span class="sxs-lookup"><span data-stu-id="20992-260">Render distance</span></span>](hologram-stability.md#hologram-render-distances)
* [<span data-ttu-id="20992-261">Point de focus dans Unity</span><span class="sxs-lookup"><span data-stu-id="20992-261">Focus point in Unity</span></span>](focus-point-in-unity.md)
* [<span data-ttu-id="20992-262">Expérimentation avec l’échelle</span><span class="sxs-lookup"><span data-stu-id="20992-262">Experimenting with scale</span></span>](scale.md#experimenting-with-scale)
* [<span data-ttu-id="20992-263">Texte, taille de police recommandée</span><span class="sxs-lookup"><span data-stu-id="20992-263">Text, Recommended font size</span></span>](typography.md#recommended-font-size)

## <a name="depth-switching"></a><span data-ttu-id="20992-264">Basculement de profondeur</span><span class="sxs-lookup"><span data-stu-id="20992-264">Depth switching</span></span>

<span data-ttu-id="20992-265">Indépendamment de l’affichage des problèmes liés à la zone de confort, les demandes pour l’utilisateur de basculer fréquemment ou rapidement entre des objets de niveau proche et lointain (y compris des hologrammes et du contenu réel) peuvent entraîner une fatigue oculomotor et une gêne générale.</span><span class="sxs-lookup"><span data-stu-id="20992-265">Regardless of viewing zone of comfort issues, demands for the user to switch frequently or quickly between near and far focal objects (including holograms and real-world content) can lead to oculomotor fatigue, and general discomfort.</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-266">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-266">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-267"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-267"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-268"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-268"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-269">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-269">✔️</span></span></td>
        <td><span data-ttu-id="20992-270">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-270">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-271">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-271">Quality criteria</span></span>

|  <span data-ttu-id="20992-272">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-272">Best</span></span>  |  <span data-ttu-id="20992-273">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-273">Meets</span></span> |  <span data-ttu-id="20992-274">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-274">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="20992-275">Basculement de profondeur limitée ou naturelle qui ne permet pas à l’utilisateur de se concentrer de manière non naturelle.</span><span class="sxs-lookup"><span data-stu-id="20992-275">Limited or natural depth switching that doesn’t cause the user to unnaturally refocus.</span></span> | <span data-ttu-id="20992-276">Commutateur à profondeur brusque : il s’agit du noyau et est conçu pour l’expérience de l’application, ou le commutateur de profondeur brusque provoqué par un contenu réel inattendu.</span><span class="sxs-lookup"><span data-stu-id="20992-276">Abrupt depth switch this is core and designed into the app experience, or abrupt depth switch that is caused by unexpected real-world content.</span></span> | <span data-ttu-id="20992-277">Commutateur de profondeur cohérent ou basculement de profondeur brusque qui n’est pas nécessaire ou essentiel à l’expérience de l’application.</span><span class="sxs-lookup"><span data-stu-id="20992-277">Consistent depth switch, or abrupt depth switching that isn’t necessary or core to the app experience.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="20992-278">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-278">How to measure</span></span>

* <span data-ttu-id="20992-279">Si l’application exige que l’utilisateur change de manière cohérente et/ou brusquement le focus de profondeur, il y a un problème de changement de profondeur.</span><span class="sxs-lookup"><span data-stu-id="20992-279">If the app requires the user to consistently and/or abruptly change depth focus, there is depth switching problem.</span></span>

### <a name="recommendations"></a><span data-ttu-id="20992-280">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-280">Recommendations</span></span>

* <span data-ttu-id="20992-281">Conservez le contenu principal dans un plan focal cohérent et assurez-vous que le plan de stabilisation correspond au plan focal.</span><span class="sxs-lookup"><span data-stu-id="20992-281">Keep primary content at a consistent focal plane and make sure the stabilization plane matches the focal plane.</span></span> <span data-ttu-id="20992-282">Cela permet d’atténuer la fatigue oculomotor et le mouvement d’hologramme inattendu.</span><span class="sxs-lookup"><span data-stu-id="20992-282">This will alleviate oculomotor fatigue and unexpected hologram movement.</span></span>

### <a name="resources"></a><span data-ttu-id="20992-283">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-283">Resources</span></span>

* [<span data-ttu-id="20992-284">Distance de rendu</span><span class="sxs-lookup"><span data-stu-id="20992-284">Render distance</span></span>](hologram-stability.md#hologram-render-distances)
* [<span data-ttu-id="20992-285">Point de focus dans Unity</span><span class="sxs-lookup"><span data-stu-id="20992-285">Focus point in Unity</span></span>](focus-point-in-unity.md)

## <a name="use-of-spatial-sound"></a><span data-ttu-id="20992-286">Utilisation du son spatial</span><span class="sxs-lookup"><span data-stu-id="20992-286">Use of spatial sound</span></span>

<span data-ttu-id="20992-287">Dans Windows Mixed Reality, le moteur audio fournit le composant d’acoustique de l’expérience de la réalité mixte en simulant le son en 3D à l’aide de la direction, de la distance et des simulations environnementales.</span><span class="sxs-lookup"><span data-stu-id="20992-287">In Windows Mixed Reality, the audio engine provides the aural component of the mixed reality experience by simulating 3D sound using direction, distance, and environmental simulations.</span></span> <span data-ttu-id="20992-288">L’utilisation d’un son spatial dans une application permet aux développeurs de placer de manière convaincante des sons dans un espace à 3 Dimensions (sphère) autour de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-288">Using spatial sound in an application allows developers to convincingly place sounds in a 3 dimensional space (sphere) all around the user.</span></span> <span data-ttu-id="20992-289">Ces sons semblent apparaître comme s’ils étaient issus d’objets physiques réels ou d’hologrammes de réalité mixte dans l’environnement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-289">Those sounds will then seem as if they were coming from real physical objects or the mixed reality holograms in the user's surroundings.</span></span> <span data-ttu-id="20992-290">Le son spatial est un outil puissant pour la conception de l’immersion, de l’accessibilité et de l’expérience utilisateur dans les applications de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="20992-290">Spatial sound is a powerful tool for immersion, accessibility, and UX design in mixed reality applications.</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-291">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-291">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-292"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-292"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-293"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-293"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-294">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-294">✔️</span></span></td>
        <td><span data-ttu-id="20992-295">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-295">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-296">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-296">Quality criteria</span></span>

|  <span data-ttu-id="20992-297">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-297">Best</span></span>  |  <span data-ttu-id="20992-298">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-298">Meets</span></span> |  <span data-ttu-id="20992-299">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-299">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="20992-300">Le son est logiquement spatial, et l’expérience utilisateur utilise le son de manière appropriée pour faciliter la détection d’objets et les commentaires des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="20992-300">Sound is logically spatialized, and the UX appropriately uses sound to assist with object discovery and user feedback.</span></span> <span data-ttu-id="20992-301">Les sons sont naturels et pertinents pour les objets et normalisés dans le scénario.</span><span class="sxs-lookup"><span data-stu-id="20992-301">Sound is natural and relevant to objects and normalized across the scenario.</span></span> | <span data-ttu-id="20992-302">L’audio spatial est utilisé de façon appropriée pour la récupération, mais il est manquant comme moyen d’aider aux commentaires des utilisateurs et à la découverte.</span><span class="sxs-lookup"><span data-stu-id="20992-302">Spatial audio is used appropriately for believability but missing as means to help with user feedback and discoverability.</span></span> | <span data-ttu-id="20992-303">Le son n’est pas spatial comme prévu, et/ou manque de son pour aider l’utilisateur au sein de l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-303">Sound is not spatialized as expected, and/or lack of sound to assist user within the UX.</span></span> <span data-ttu-id="20992-304">Ou l’audio spatial n’a pas été pris en compte ou utilisé dans la conception du scénario.</span><span class="sxs-lookup"><span data-stu-id="20992-304">Or spatial audio was not considered or used in the design of the scenario.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="20992-305">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-305">How to measure</span></span>

* <span data-ttu-id="20992-306">En général, les sons pertinents doivent émettre des hologrammes cibles (par exemple, des sons d’écorce provenant du chien holographique).</span><span class="sxs-lookup"><span data-stu-id="20992-306">In general, relevant sounds should emit from target holograms (eg., bark sound coming from holographic dog.)</span></span>
* <span data-ttu-id="20992-307">Des signaux sonores doivent être utilisés tout au long de l’expérience utilisateur pour aider l’utilisateur à faire part de ses commentaires ou à connaître des actions en dehors du cadre holographique.</span><span class="sxs-lookup"><span data-stu-id="20992-307">Sound cues should be used throughout the UX to assist the user with feedback or awareness of actions outside the holographic frame.</span></span>

### <a name="recommendations"></a><span data-ttu-id="20992-308">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-308">Recommendations</span></span>

* <span data-ttu-id="20992-309">Utilisez l’audio spatial pour faciliter la détection d’objets et les interfaces utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-309">Use spatial audio to assist with object discovery and user interfaces.</span></span>
* <span data-ttu-id="20992-310">Les sons réels fonctionnent mieux que la synthèse ou le son non naturel.</span><span class="sxs-lookup"><span data-stu-id="20992-310">Real sounds work better than synthesize or unnatural sound.</span></span>
* <span data-ttu-id="20992-311">La plupart des sons doivent être spatiaux.</span><span class="sxs-lookup"><span data-stu-id="20992-311">Most sounds should be spatialized.</span></span>
* <span data-ttu-id="20992-312">Évitez les émetteurs invisibles.</span><span class="sxs-lookup"><span data-stu-id="20992-312">Avoid invisible emitters.</span></span>
* <span data-ttu-id="20992-313">Évitez le masquage spatial.</span><span class="sxs-lookup"><span data-stu-id="20992-313">Avoid spatial masking.</span></span>
* <span data-ttu-id="20992-314">Normaliser tous les sons.</span><span class="sxs-lookup"><span data-stu-id="20992-314">Normalize all sounds.</span></span>

### <a name="resources"></a><span data-ttu-id="20992-315">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-315">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="20992-316">Documentation</span><span class="sxs-lookup"><span data-stu-id="20992-316">Documentation</span></span>

* [<span data-ttu-id="20992-317">Son spatial</span><span class="sxs-lookup"><span data-stu-id="20992-317">Spatial sound</span></span>](spatial-sound.md)
* [<span data-ttu-id="20992-318">Conception du son spatial</span><span class="sxs-lookup"><span data-stu-id="20992-318">Spatial sound design</span></span>](spatial-sound-design.md)
* [<span data-ttu-id="20992-319">Son spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="20992-319">Spatial sound in Unity</span></span>](spatial-sound-in-unity.md)
* [<span data-ttu-id="20992-320">Étude de cas, son spatial pour HoloTour</span><span class="sxs-lookup"><span data-stu-id="20992-320">Case study, Spatial sound for HoloTour</span></span>](case-study-spatial-sound-design-for-holotour.md)
* [<span data-ttu-id="20992-321">Étude de cas utilisant le son spatial dans RoboRaid</span><span class="sxs-lookup"><span data-stu-id="20992-321">Case study, Using spatial sound in RoboRaid</span></span>](case-study-using-spatial-sound-in-roboraid.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="20992-322">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="20992-322">Tools and tutorials</span></span>

* [<span data-ttu-id="20992-323">MR spatial 220 : son spatial</span><span class="sxs-lookup"><span data-stu-id="20992-323">MR Spatial 220: Spatial sound</span></span>](holograms-220.md)
* [<span data-ttu-id="20992-324">MRToolkit, audio spatial</span><span class="sxs-lookup"><span data-stu-id="20992-324">MRToolkit, Spatial Audio</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/SpatialSound/README.md)

## <a name="focus-on-holographic-frame-fov-boundaries"></a><span data-ttu-id="20992-325">Focalisation sur les limites du cadre holographique</span><span class="sxs-lookup"><span data-stu-id="20992-325">Focus on holographic frame (FOV) boundaries</span></span>

<span data-ttu-id="20992-326">Les expériences utilisateur bien conçues peuvent créer et gérer le contexte utile de l’environnement virtuel qui s’étend autour des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="20992-326">Well-designed user experiences can create and maintain useful context of the virtual environment that extends around the users.</span></span> <span data-ttu-id="20992-327">L’atténuation de l’effet des limites de l’aide implique une conception réfléchie de l’échelle et du contexte du contenu, l’utilisation de l’audio spatial, les systèmes d’aide et la position de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-327">Mitigating the effect of the FOV boundaries involves a thoughtful design of content scale and context, use of spatial audio, guidance systems, and the user's position.</span></span> <span data-ttu-id="20992-328">Si vous avez terminé, l’utilisateur se sentira moins affecté par les limites de l’aide, tout en disposant d’une expérience d’application confortable.</span><span class="sxs-lookup"><span data-stu-id="20992-328">If done right, the user will feel less impaired by the FOV boundaries while having a comfortable app experience.</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-329">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-329">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-330"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-330"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-331"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-331"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-332">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-332">✔️</span></span></td>
        <td>❌</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-333">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-333">Quality criteria</span></span>

|  <span data-ttu-id="20992-334">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-334">Best</span></span>  |  <span data-ttu-id="20992-335">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-335">Meets</span></span> |  <span data-ttu-id="20992-336">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-336">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="20992-337">L’utilisateur ne perd jamais de contexte et l’affichage est à l’aise.</span><span class="sxs-lookup"><span data-stu-id="20992-337">User never loses context and viewing is comfortable.</span></span> <span data-ttu-id="20992-338">L’assistance contextuelle est fournie pour les objets volumineux.</span><span class="sxs-lookup"><span data-stu-id="20992-338">Context assistance is provided for large objects.</span></span> <span data-ttu-id="20992-339">Les informations de découverte et d’affichage sont fournies pour les objets en dehors du frame.</span><span class="sxs-lookup"><span data-stu-id="20992-339">Discoverability and viewing guidance is provided for objects outside the frame.</span></span> <span data-ttu-id="20992-340">En général, la conception de mouvement et l’échelle des hologrammes sont appropriées pour une expérience d’affichage confortable.</span><span class="sxs-lookup"><span data-stu-id="20992-340">In general, motion design and scale of the holograms are appropriate for a comfortable viewing experience.</span></span> | <span data-ttu-id="20992-341">L’utilisateur ne perd jamais de contexte, mais un mouvement de cou supplémentaire peut être nécessaire dans des situations limitées.</span><span class="sxs-lookup"><span data-stu-id="20992-341">User never loses context, but extra neck motion may be required in limited situations.</span></span> <span data-ttu-id="20992-342">Dans le cas d’une mise à l’échelle limitée, les hologrammes rompent le cadre vertical ou horizontal provoquant un mouvement du cou pour afficher les hologrammes.</span><span class="sxs-lookup"><span data-stu-id="20992-342">In limited situations scale causes holograms to break either the vertical or horizontal frame causing some neck motion to view holograms.</span></span> | <span data-ttu-id="20992-343">L’utilisateur risque de perdre du contexte et/ou un mouvement de cou cohérent est nécessaire pour afficher les hologrammes.</span><span class="sxs-lookup"><span data-stu-id="20992-343">User likely to lose context and/or consistent neck motion is required to view holograms.</span></span> <span data-ttu-id="20992-344">Aucun guide de contexte pour les grands objets holographiques, déplacement d’objets facile à perdre en dehors du cadre sans guide de détectabilité, ou hologrammes de haut, nécessite un mouvement de cou normal.</span><span class="sxs-lookup"><span data-stu-id="20992-344">No context guidance for large holographic objects, moving objects easy to lose outside the frame with no discoverability guidance, or tall holograms requires regular neck motion to view.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="20992-345">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-345">How to measure</span></span>

* <span data-ttu-id="20992-346">Le contexte d’un (grand) hologramme est perdu ou n’est pas compris en raison d’un découpage aux limites.</span><span class="sxs-lookup"><span data-stu-id="20992-346">Context for a (large) hologram is lost or not understood due to being clipped at the boundaries.</span></span>
* <span data-ttu-id="20992-347">L’emplacement des hologrammes est difficile à trouver en raison du manque d’administrateurs ou de contenus qui se déplacent rapidement dans le cadre holographique.</span><span class="sxs-lookup"><span data-stu-id="20992-347">Location of holograms are hard to find due to the lack of attention directors or content that rapidly moves in and out of the holographic frame.</span></span>
* <span data-ttu-id="20992-348">Le scénario nécessite un mouvement de tête normal et répétitif pour voir entièrement un hologramme entraînant une fatigue du cou.</span><span class="sxs-lookup"><span data-stu-id="20992-348">Scenario requires regular and repetitive up and down head motion to fully see a hologram resulting in neck fatigue.</span></span>

### <a name="recommendations"></a><span data-ttu-id="20992-349">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-349">Recommendations</span></span>

* <span data-ttu-id="20992-350">Démarrez l’expérience avec les petits objets qui correspondent à l’angle d’ouverture, puis faites la transition avec des signaux visuels vers des versions plus grandes.</span><span class="sxs-lookup"><span data-stu-id="20992-350">Start the experience with small objects that fit the FOV, then transition with visual cues to larger versions.</span></span>
* <span data-ttu-id="20992-351">Utilisez des directeurs audio et d’avertissement pour aider l’utilisateur à trouver du contenu en dehors de l’aide.</span><span class="sxs-lookup"><span data-stu-id="20992-351">Use spatial audio and attention directors to help the user find content that is outside the FOV.</span></span>
* <span data-ttu-id="20992-352">Évitez autant que possible les hologrammes qui découpent verticalement l’angle de la verticale.</span><span class="sxs-lookup"><span data-stu-id="20992-352">As much as possible, avoid holograms that vertically clip the FOV.</span></span>
* <span data-ttu-id="20992-353">Fournissez à l’utilisateur des conseils dans l’application pour un meilleur affichage de l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="20992-353">Provide the user with in-app guidance for best viewing location.</span></span>

### <a name="resources"></a><span data-ttu-id="20992-354">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-354">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="20992-355">Documentation</span><span class="sxs-lookup"><span data-stu-id="20992-355">Documentation</span></span>

* [<span data-ttu-id="20992-356">Image holographique</span><span class="sxs-lookup"><span data-stu-id="20992-356">Holographic frame</span></span>](holographic-frame.md)
* [<span data-ttu-id="20992-357">Étude de cas, interface utilisateur HoloStudio et apprentissages de conception d’interaction</span><span class="sxs-lookup"><span data-stu-id="20992-357">Case Study, HoloStudio UI and interaction design learnings</span></span>](case-study-3-holostudio-ui-and-interaction-design-learnings.md?#problem-2-modal-dialogs-are-sometimes-out-of-the-holographic-frame)
* [<span data-ttu-id="20992-358">Échelle des objets et des environnements</span><span class="sxs-lookup"><span data-stu-id="20992-358">Scale of objects and environments</span></span>](scale.md)
* [<span data-ttu-id="20992-359">Curseurs, signaux visuels</span><span class="sxs-lookup"><span data-stu-id="20992-359">Cursors, Visual cues</span></span>](cursors.md#visual-cues)

#### <a name="external-references"></a><span data-ttu-id="20992-360">Références externes</span><span class="sxs-lookup"><span data-stu-id="20992-360">External references</span></span>

* [<span data-ttu-id="20992-361">Bien d’ADO sur l’angle d’été</span><span class="sxs-lookup"><span data-stu-id="20992-361">Much ado about the FOV</span></span>](https://www.linkedin.com/pulse/hololens-much-ado-field-of-view-michael-hoffman?lipi=urn%3Ali%3Apage%3Ad_flagship3_feed%3B6iQ%2FbTevLDU93w3I2ewLJw%3D%3D)

## <a name="content-reacts-to-user-position"></a><span data-ttu-id="20992-362">Le contenu réagit à la position de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="20992-362">Content reacts to user position</span></span>

<span data-ttu-id="20992-363">Les hologrammes doivent réagir à la position de l’utilisateur à peu près de la même façon que les objets « réels ».</span><span class="sxs-lookup"><span data-stu-id="20992-363">Holograms should react to the user position in roughly the same ways that "real" objects do.</span></span> <span data-ttu-id="20992-364">L’un des éléments d’interface utilisateur qui ne peuvent pas nécessairement supposer que la position d’un utilisateur est stationnaire et s’adapte au mouvement de l’utilisateur est une considération notable.</span><span class="sxs-lookup"><span data-stu-id="20992-364">A notable design consideration is UI elements that can't necessarily assume a user's position is stationary and adapt to the user's motion.</span></span> <span data-ttu-id="20992-365">La conception d’une application qui s’adapte correctement à la position de l’utilisateur crée une expérience plus crédible et la rend plus facile à utiliser.</span><span class="sxs-lookup"><span data-stu-id="20992-365">Designing an app that correctly adapts to user position will create a more believable experience and make it easier to use.</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-366">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-366">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-367"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-367"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-368"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-368"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-369">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-369">✔️</span></span></td>
        <td><span data-ttu-id="20992-370">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-370">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-371">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-371">Quality criteria</span></span>

<table>
<tr>
<td> <span data-ttu-id="20992-372">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-372">Best</span></span> </td><td> <span data-ttu-id="20992-373">Le contenu et l’interface utilisateur s’adaptent aux postes des utilisateurs, ce qui permet à l’utilisateur d’interagir naturellement avec le contenu dans le cadre du déplacement d’utilisateur attendu.</span><span class="sxs-lookup"><span data-stu-id="20992-373">Content and UI adapt to user positions allowing user to naturally interact with content within the scope of expected user movement.</span></span></td>
</tr><tr>
<td> <span data-ttu-id="20992-374">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-374">Meets</span></span> </td><td> <span data-ttu-id="20992-375">L’interface utilisateur s’adapte à la position de l’utilisateur, mais peut empêcher l’affichage du contenu de la clé qui oblige l’utilisateur à ajuster sa position.</span><span class="sxs-lookup"><span data-stu-id="20992-375">UI adapts to the user position, but may impede the view of key content requiring the user to adjust their position.</span></span></td>
</tr><tr>
<td> <span data-ttu-id="20992-376">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-376">Fail</span></span> </td><td><ol>
<li><span data-ttu-id="20992-377">Les éléments d’interface utilisateur sont perdus ou verrouillés au cours du mouvement, provoquant ainsi un retour à (ou une recherche) anormal des contrôles.</span><span class="sxs-lookup"><span data-stu-id="20992-377">UI elements are lost or locked during movement causing user to unnaturally return to (or find) controls.</span></span></li><li><span data-ttu-id="20992-378">Les éléments d’interface utilisateur limitent l’affichage du contenu principal.</span><span class="sxs-lookup"><span data-stu-id="20992-378">UI elements limit the view of primary content.</span></span></li><li><span data-ttu-id="20992-379">Le déplacement de l’interface utilisateur n’est pas optimisé pour l’affichage de la distance et de l’inertie, en particulier avec les éléments de <a href="billboarding-and-tag-along.md">balisage</a> .</span><span class="sxs-lookup"><span data-stu-id="20992-379">UI movement is not optimized for viewing distance and momentum particularly with <a href="billboarding-and-tag-along.md">tag-along</a> UI elements.</span></span></li>
</ol></td>
</tr>
</table>

### <a name="how-to-measure"></a><span data-ttu-id="20992-380">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-380">How to measure</span></span>

* <span data-ttu-id="20992-381">Toutes les mesures doivent être effectuées dans une étendue raisonnable du scénario.</span><span class="sxs-lookup"><span data-stu-id="20992-381">All measurements should be done within a reasonable scope of the scenario.</span></span> <span data-ttu-id="20992-382">Si le déplacement des utilisateurs varie, n’essayez pas de tromper l’application avec un déplacement extrême de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-382">While user movement will vary, don’t try to trick the app with extreme user movement.</span></span>
* <span data-ttu-id="20992-383">Pour les éléments d’interface utilisateur, les contrôles pertinents doivent être disponibles quel que soit le déplacement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-383">For UI elements, relevant controls should be available regardless of user movement.</span></span> <span data-ttu-id="20992-384">Par exemple, si l’utilisateur consulte et parcourt une carte 3D avec zoom, le contrôle de zoom doit être immédiatement accessible à l’utilisateur, quel que soit son emplacement.</span><span class="sxs-lookup"><span data-stu-id="20992-384">For example, if the user is viewing and walking around a 3D map with zoom, the zoom control should be readily available to the user regardless of location.</span></span>

### <a name="recommendations"></a><span data-ttu-id="20992-385">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-385">Recommendations</span></span>

* <span data-ttu-id="20992-386">L’utilisateur est l’appareil photo et il contrôle le mouvement.</span><span class="sxs-lookup"><span data-stu-id="20992-386">The user is the camera and they control the movement.</span></span> <span data-ttu-id="20992-387">Laissez-les sur le lecteur.</span><span class="sxs-lookup"><span data-stu-id="20992-387">Let them drive.</span></span>
* <span data-ttu-id="20992-388">Envisagez l’utilisation de panneaux pour le texte et les systèmes de menus qui, autrement, seraient universellement verrouillés ou obscurcis si un utilisateur devait se déplacer.</span><span class="sxs-lookup"><span data-stu-id="20992-388">Consider billboarding for text and menuing systems that would otherwise be world-locked or obscured if a user were to move around.</span></span>
* <span data-ttu-id="20992-389">Utilisez tag-avec pour le contenu qui doit suivre l’utilisateur tout en permettant à l’utilisateur de voir ce qui est devant eux.</span><span class="sxs-lookup"><span data-stu-id="20992-389">Use tag-along for content that needs to follow the user while still allowing the user to see what is in front of them.</span></span>

### <a name="resources"></a><span data-ttu-id="20992-390">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-390">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="20992-391">Documentation</span><span class="sxs-lookup"><span data-stu-id="20992-391">Documentation</span></span>

* [<span data-ttu-id="20992-392">Conception d’interaction</span><span class="sxs-lookup"><span data-stu-id="20992-392">Interaction design</span></span>](hologram.md)
* [<span data-ttu-id="20992-393">Couleur, lumière et matériau</span><span class="sxs-lookup"><span data-stu-id="20992-393">Color, light, and material</span></span>](color,-light-and-materials.md)
* [<span data-ttu-id="20992-394">Billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="20992-394">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
* [<span data-ttu-id="20992-395">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="20992-395">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="20992-396">Automotion et utilisateur locomotion</span><span class="sxs-lookup"><span data-stu-id="20992-396">Self-motion and user locomotion</span></span>](comfort.md#self-motion-and-user-locomotion)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="20992-397">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="20992-397">Tools and tutorials</span></span>

* [<span data-ttu-id="20992-398">Monsieur-entrée 210 : point de regard</span><span class="sxs-lookup"><span data-stu-id="20992-398">MR Input 210: Gaze</span></span>](holograms-210.md)

## <a name="input-interaction-clarity"></a><span data-ttu-id="20992-399">Clarté d’interaction d’entrée</span><span class="sxs-lookup"><span data-stu-id="20992-399">Input interaction clarity</span></span>

<span data-ttu-id="20992-400">La clarté de l’interaction d’entrée est essentielle à l’utilisation d’une application et comprend la cohérence des entrées, l’approche, la détectabilité des méthodes d’interaction.</span><span class="sxs-lookup"><span data-stu-id="20992-400">Input interaction clarity is critical to an app's usability and includes input consistency, approachability, discoverability of interaction methods.</span></span> <span data-ttu-id="20992-401">L’utilisateur doit être en mesure d’utiliser des interactions communes à l’ensemble de la plateforme sans réapprendre.</span><span class="sxs-lookup"><span data-stu-id="20992-401">User should be able to use platform-wide common interactions without relearning.</span></span> <span data-ttu-id="20992-402">Si l’application dispose d’une entrée personnalisée, elle doit être clairement communiquée et démontrée.</span><span class="sxs-lookup"><span data-stu-id="20992-402">If the app has custom input, it should be clearly communicated and demonstrated.</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-403">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-403">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-404"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-404"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-405"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-405"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-406">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-406">✔️</span></span></td>
        <td><span data-ttu-id="20992-407">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-407">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-408">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-408">Quality criteria</span></span>

|  <span data-ttu-id="20992-409">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-409">Best</span></span>  |  <span data-ttu-id="20992-410">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-410">Meets</span></span> |  <span data-ttu-id="20992-411">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-411">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="20992-412">Les méthodes d’interaction d’entrée sont cohérentes avec les [recommandations](interaction-fundamentals.md)fournies par Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="20992-412">Input interaction methods are consistent with Windows Mixed Reality provided [guidance](interaction-fundamentals.md).</span></span> <span data-ttu-id="20992-413">Toute entrée personnalisée ne doit pas être redondante avec une entrée standard (plutôt que d’utiliser l’interaction standard) et doit être clairement communiquée et présentée à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-413">Any custom input should not be redundant with standard input (rather use standard interaction) and must be clearly communicated and demonstrated to the user.</span></span> | <span data-ttu-id="20992-414">Semblable au meilleur, mais les entrées personnalisées sont redondantes avec des méthodes d’entrée standard.</span><span class="sxs-lookup"><span data-stu-id="20992-414">Similar to best, but custom inputs are redundant with standard input methods.</span></span> <span data-ttu-id="20992-415">L’utilisateur peut toujours atteindre l’objectif et progresser dans l’expérience de l’application.</span><span class="sxs-lookup"><span data-stu-id="20992-415">User can still achieve the goal and progress through the app experience.</span></span> | <span data-ttu-id="20992-416">Il est difficile de comprendre la méthode d’entrée ou le mappage de bouton.</span><span class="sxs-lookup"><span data-stu-id="20992-416">Difficult to understand input method or button mapping.</span></span> <span data-ttu-id="20992-417">L’entrée est fortement personnalisée, ne prend pas en charge les entrées standard, aucune instruction, ou risque de provoquer des problèmes de fatigue et de confort.</span><span class="sxs-lookup"><span data-stu-id="20992-417">Input is heavily customized, does not support standard input, no instructions, or likely to cause fatigue and comfort issues.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="20992-418">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-418">How to measure</span></span>

* <span data-ttu-id="20992-419">L’application utilise des [méthodes d’entrée standard](interaction-fundamentals.md) cohérentes.</span><span class="sxs-lookup"><span data-stu-id="20992-419">The app uses consistent [standard input methods.](interaction-fundamentals.md)</span></span>
* <span data-ttu-id="20992-420">Si l’application a des entrées personnalisées, elle est clairement communiquée à :</span><span class="sxs-lookup"><span data-stu-id="20992-420">If the app has custome input, it is clearly communicated through:</span></span>
* <span data-ttu-id="20992-421">Expérience de première exécution</span><span class="sxs-lookup"><span data-stu-id="20992-421">First-run experience</span></span>
* <span data-ttu-id="20992-422">Écrans d’introduction</span><span class="sxs-lookup"><span data-stu-id="20992-422">Introductory screens</span></span>
* <span data-ttu-id="20992-423">Info-bulles</span><span class="sxs-lookup"><span data-stu-id="20992-423">Tooltips</span></span>
* <span data-ttu-id="20992-424">Autocar à main</span><span class="sxs-lookup"><span data-stu-id="20992-424">Hand coach</span></span>
* <span data-ttu-id="20992-425">Section d’aide</span><span class="sxs-lookup"><span data-stu-id="20992-425">Help section</span></span>
* <span data-ttu-id="20992-426">Voix sur</span><span class="sxs-lookup"><span data-stu-id="20992-426">Voice over</span></span>

### <a name="recommendations"></a><span data-ttu-id="20992-427">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-427">Recommendations</span></span>

* <span data-ttu-id="20992-428">Utilisez des méthodes d’entrée standard dans la mesure du possible.</span><span class="sxs-lookup"><span data-stu-id="20992-428">Use standard input methods whenever possible.</span></span>
* <span data-ttu-id="20992-429">Fournissez des démonstrations, des didacticiels et des info-bulles pour les méthodes d’entrée non standard.</span><span class="sxs-lookup"><span data-stu-id="20992-429">Provide demonstrations, tutorials, and tooltips for non-standard input methods.</span></span>
* <span data-ttu-id="20992-430">Utilisez un modèle d’interaction cohérent dans l’ensemble de l’application.</span><span class="sxs-lookup"><span data-stu-id="20992-430">Use a consistent interaction model throughout the app.</span></span>

### <a name="resources"></a><span data-ttu-id="20992-431">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-431">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="20992-432">Documentation</span><span class="sxs-lookup"><span data-stu-id="20992-432">Documentation</span></span>

* [<span data-ttu-id="20992-433">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="20992-433">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="20992-434">Objets interactifs</span><span class="sxs-lookup"><span data-stu-id="20992-434">Interactable objects</span></span>](interactable-object.md)
* [<span data-ttu-id="20992-435">Suivre de la tête et stabiliser</span><span class="sxs-lookup"><span data-stu-id="20992-435">Head-gaze and dwell</span></span>](gaze-and-dwell.md)
* [<span data-ttu-id="20992-436">Curseurs</span><span class="sxs-lookup"><span data-stu-id="20992-436">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="20992-437">Confort et point de regard</span><span class="sxs-lookup"><span data-stu-id="20992-437">Comfort and gaze</span></span>](comfort.md#gaze-direction)
* [<span data-ttu-id="20992-438">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="20992-438">Voice input</span></span>](voice-input.md)
* [<span data-ttu-id="20992-439">Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="20992-439">Motion controllers</span></span>](motion-controllers.md)
* [<span data-ttu-id="20992-440">Guide de portage des entrées pour Unity</span><span class="sxs-lookup"><span data-stu-id="20992-440">Input porting guide for Unity</span></span>](input-porting-guide-for-unity.md)
* [<span data-ttu-id="20992-441">Saisie au clavier dans Unity</span><span class="sxs-lookup"><span data-stu-id="20992-441">Keyboard input in Unity</span></span>](keyboard-input-in-unity.md)
* [<span data-ttu-id="20992-442">Pointage du regard dans Unity</span><span class="sxs-lookup"><span data-stu-id="20992-442">Gaze in Unity</span></span>](gaze-in-unity.md)
* [<span data-ttu-id="20992-443">Mouvements et contrôleurs de mouvement dans Unity</span><span class="sxs-lookup"><span data-stu-id="20992-443">Gestures and motion controllers in Unity</span></span>](gestures-and-motion-controllers-in-unity.md)
* [<span data-ttu-id="20992-444">Entrée vocale dans Unity</span><span class="sxs-lookup"><span data-stu-id="20992-444">Voice input in Unity</span></span>](voice-input-in-unity.md)
* [<span data-ttu-id="20992-445">Saisie à l’aide de la commande de jeu, du clavier et de la souris dans DirectX</span><span class="sxs-lookup"><span data-stu-id="20992-445">Keyboard, mouse, and controller input in DirectX</span></span>](keyboard,-mouse,-and-controller-input-in-directx.md)
* [<span data-ttu-id="20992-446">Suivre de la tête et du regard dans DirectX</span><span class="sxs-lookup"><span data-stu-id="20992-446">Head and eye gaze in DirectX</span></span>](gaze-in-directx.md)
* [<span data-ttu-id="20992-447">Mains et contrôleurs de mouvement dans DirectX</span><span class="sxs-lookup"><span data-stu-id="20992-447">Hands and motion controllers in DirectX</span></span>](hands-and-motion-controllers-in-directx.md)
* [<span data-ttu-id="20992-448">Entrée vocale dans DirectX</span><span class="sxs-lookup"><span data-stu-id="20992-448">Voice input in DirectX</span></span>](voice-input-in-directx.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="20992-449">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="20992-449">Tools and tutorials</span></span>

* [<span data-ttu-id="20992-450">Étude de cas : la poursuite de l’informatique plus personnelle</span><span class="sxs-lookup"><span data-stu-id="20992-450">Case study: The pursuit of more personal computing</span></span>](case-study-the-pursuit-of-more-personal-computing.md#less-interface-in-your-face)
* [<span data-ttu-id="20992-451">Étude de Cast : interface utilisateur HoloStudio et apprentissages de conception d’interaction</span><span class="sxs-lookup"><span data-stu-id="20992-451">Cast study: HoloStudio UI and interaction design learnings</span></span>](case-study-3-holostudio-ui-and-interaction-design-learnings.md)
* [<span data-ttu-id="20992-452">Exemple d’application : table périodique des éléments</span><span class="sxs-lookup"><span data-stu-id="20992-452">Sample app: Periodic table of the elements</span></span>](periodic-table-of-the-elements.md)
* [<span data-ttu-id="20992-453">Exemple d’application : module lunaire</span><span class="sxs-lookup"><span data-stu-id="20992-453">Sample app: Lunar module</span></span>](lunar-module.md)
* [<span data-ttu-id="20992-454">Monsieur-entrée 210 : point de regard</span><span class="sxs-lookup"><span data-stu-id="20992-454">MR Input 210: Gaze</span></span>](holograms-210.md)
* [<span data-ttu-id="20992-455">Entrée MR 211 : gestes</span><span class="sxs-lookup"><span data-stu-id="20992-455">MR Input 211: Gestures</span></span>](holograms-211.md)
* [<span data-ttu-id="20992-456">Entrée MR 212 : voix</span><span class="sxs-lookup"><span data-stu-id="20992-456">MR Input 212: Voice</span></span>](holograms-212.md)

## <a name="interactable-objects"></a><span data-ttu-id="20992-457">Objets interactifs</span><span class="sxs-lookup"><span data-stu-id="20992-457">Interactable objects</span></span>

<span data-ttu-id="20992-458">Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait en 2D.</span><span class="sxs-lookup"><span data-stu-id="20992-458">A button has long been a metaphor used for triggering an event in the 2D abstract world.</span></span> <span data-ttu-id="20992-459">Dans le monde de la réalité mixte en trois dimensions, nous n’avons plus à limiter le monde de l’abstraction.</span><span class="sxs-lookup"><span data-stu-id="20992-459">In the three-dimensional mixed reality world, we don’t have to be confined to this world of abstraction anymore.</span></span> <span data-ttu-id="20992-460">Tout peut être un objet pouvant être utilisé qui déclenche un événement.</span><span class="sxs-lookup"><span data-stu-id="20992-460">Anything can be an Interactable object that triggers an event.</span></span> <span data-ttu-id="20992-461">Un objet pouvant être en interaction peut être représenté sous la forme d’un objet à partir d’une tasse de café sur la table.</span><span class="sxs-lookup"><span data-stu-id="20992-461">An interactable object can be represented as anything from a coffee cup on the table to a balloon floating in the air.</span></span> <span data-ttu-id="20992-462">Quelle que soit la forme, les objets interactifs doivent être clairement reconnus par l’utilisateur via des signaux visuels et audio.</span><span class="sxs-lookup"><span data-stu-id="20992-462">Regardless of the form, interactable objects should be clearly recognizable by the user through visual and audio cues.</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-463">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-463">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-464"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-464"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-465"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-465"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-466">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-466">✔️</span></span></td>
        <td><span data-ttu-id="20992-467">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-467">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-468">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-468">Quality criteria</span></span>

|  <span data-ttu-id="20992-469">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-469">Best</span></span>  |  <span data-ttu-id="20992-470">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-470">Meets</span></span> |  <span data-ttu-id="20992-471">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-471">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="20992-472">Quelle que soit la forme, les objets interactifs sont reconnaissables par des signaux audio et visuels dans les trois États : inactif, ciblé et sélectionné.</span><span class="sxs-lookup"><span data-stu-id="20992-472">Regardless of form, interactable objects are recognizable through visual and audio cues across three states: idle, targeted, and selected.</span></span> <span data-ttu-id="20992-473">« Regardez-le, dites-le » est clair et constamment utilisé tout au long de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="20992-473">"See it, say it" is clear and consistently used throughout the experience.</span></span> <span data-ttu-id="20992-474">Les objets sont mis à l’échelle et distribués pour permettre le ciblage gratuit des erreurs.</span><span class="sxs-lookup"><span data-stu-id="20992-474">Objects are scaled and distributed to allow for error free targeting.</span></span> | <span data-ttu-id="20992-475">L’utilisateur peut reconnaître un objet comme étant en interaction avec des retours audio ou visuels, et peut cibler et activer l’objet.</span><span class="sxs-lookup"><span data-stu-id="20992-475">User can recognize object as interactable through audio or visual feedback, and can target and activate the object.</span></span> | <span data-ttu-id="20992-476">En l’absence de signaux visuels ou audio, l’utilisateur ne peut pas reconnaître un objet pouvant être en interaction.</span><span class="sxs-lookup"><span data-stu-id="20992-476">Given no visual or audio cues, user cannot recognize an interactable object.</span></span> <span data-ttu-id="20992-477">Les interactions sont sujettes aux erreurs en raison de l’échelle de l’objet ou de la distance entre les objets.</span><span class="sxs-lookup"><span data-stu-id="20992-477">Interactions are error prone due to object scale or distance between objects.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="20992-478">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-478">How to measure</span></span>

* <span data-ttu-id="20992-479">Les objets interactifs sont reconnaissables comme « interactifs »; y compris les boutons, les menus et le contenu spécifique à l’application.</span><span class="sxs-lookup"><span data-stu-id="20992-479">Interactable objects are recognizable as 'interactable'; including buttons, menus, and app specific content.</span></span> <span data-ttu-id="20992-480">En règle générale, il doit exister un signal visuel et audio pour cibler les objets interactifs.</span><span class="sxs-lookup"><span data-stu-id="20992-480">As a rule of thumb there should be a visual and audio cue when targeting interactable objects.</span></span>

### <a name="recommendations"></a><span data-ttu-id="20992-481">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-481">Recommendations</span></span>

* <span data-ttu-id="20992-482">Utilisez des commentaires visuels et audio pour les interactions.</span><span class="sxs-lookup"><span data-stu-id="20992-482">Use visual and audio feedback for interactions.</span></span>
* <span data-ttu-id="20992-483">Les commentaires visuels doivent être différenciés pour chaque État d’entrée (inactif, ciblé, sélectionné)</span><span class="sxs-lookup"><span data-stu-id="20992-483">Visual feedback should be differentiated for each input state (idle, targeted, selected)</span></span>
* <span data-ttu-id="20992-484">Les objets interactifs doivent être mis à l’échelle et placés en vue d’une erreur de ciblage libre.</span><span class="sxs-lookup"><span data-stu-id="20992-484">Interactable objects should be scaled and placed for error free targeting.</span></span>
* <span data-ttu-id="20992-485">Les objets interactifs groupés (tels qu’une barre de menus ou une liste) doivent avoir un espacement correct pour le ciblage.</span><span class="sxs-lookup"><span data-stu-id="20992-485">Grouped interactable objects (such as a menu bar or list) should have proper spacing for targeting.</span></span>
* <span data-ttu-id="20992-486">Les boutons et les menus qui prennent en charge les commandes vocales doivent fournir des étiquettes de texte pour le mot clé de commande (« consultez-le », dites-le «»)</span><span class="sxs-lookup"><span data-stu-id="20992-486">Buttons and menus that support voice command should provide text labels for the command keyword ("See it, say it")</span></span>

### <a name="resources"></a><span data-ttu-id="20992-487">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-487">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="20992-488">Documentation</span><span class="sxs-lookup"><span data-stu-id="20992-488">Documentation</span></span>

* [<span data-ttu-id="20992-489">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="20992-489">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="20992-490">Texte dans Unity</span><span class="sxs-lookup"><span data-stu-id="20992-490">Text in Unity</span></span>](text-in-unity.md)
* [<span data-ttu-id="20992-491">Rectangle englobant et barre de l’application</span><span class="sxs-lookup"><span data-stu-id="20992-491">Bounding box and App bar</span></span>](app-bar-and-bounding-box.md)
* [<span data-ttu-id="20992-492">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="20992-492">Voice input</span></span>](voice-input.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="20992-493">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="20992-493">Tools and tutorials</span></span>

* [<span data-ttu-id="20992-494">Kit de pratiques de réalité mixte-UX</span><span class="sxs-lookup"><span data-stu-id="20992-494">Mixed Reality Toolkit - UX</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/UX)

## <a name="room-scanning"></a><span data-ttu-id="20992-495">Analyse de la salle</span><span class="sxs-lookup"><span data-stu-id="20992-495">Room scanning</span></span>

<span data-ttu-id="20992-496">Les applications qui requièrent des données de mappage spatiale s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions lorsque l’utilisateur explore son environnement avec l’appareil actif.</span><span class="sxs-lookup"><span data-stu-id="20992-496">Apps that require spatial mapping data rely on the device to automatically collect this data over time and across sessions as the user explores their environment with the device active.</span></span> <span data-ttu-id="20992-497">L’exhaustivité et la qualité de ces données dépendent d’un certain nombre de facteurs, notamment la quantité d’exploration effectuée par l’utilisateur, le temps écoulé depuis l’exploration et si les objets tels que les meubles et les portes ont été déplacés depuis que l’appareil a analysé la zone.</span><span class="sxs-lookup"><span data-stu-id="20992-497">The completeness and quality of this data depends on a number of factors including the amount of exploration the user has done, how much time has passed since the exploration and whether objects such as furniture and doors have moved since the device scanned the area.</span></span> <span data-ttu-id="20992-498">De nombreuses applications analysent les données de mappage spatiale au début de l’expérience afin de déterminer si l’utilisateur doit effectuer des étapes supplémentaires pour améliorer l’exhaustivité et la qualité de la carte spatiale.</span><span class="sxs-lookup"><span data-stu-id="20992-498">Many apps will analyze the spatial mapping data at the start of the experience to judge whether the user should perform additional steps to improve the completeness and quality of the spatial map.</span></span> <span data-ttu-id="20992-499">Si l’utilisateur est invité à analyser l’environnement, vous devez fournir des instructions claires au cours de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="20992-499">If the user is required to scan the environment, clear guidance should be provided during the scanning experience.</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-500">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-500">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-501"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-501"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-502"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-502"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-503">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-503">✔️</span></span></td>
        <td>❌</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-504">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-504">Quality criteria</span></span>

|  <span data-ttu-id="20992-505">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-505">Best</span></span>  |  <span data-ttu-id="20992-506">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-506">Meets</span></span> |  <span data-ttu-id="20992-507">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-507">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="20992-508">La visualisation de la maille spatiale indique aux utilisateurs que l’analyse est en cours.</span><span class="sxs-lookup"><span data-stu-id="20992-508">Visualization of the spatial mesh tell users scanning is in progress.</span></span> <span data-ttu-id="20992-509">L’utilisateur sait clairement ce qu’il doit faire et quand l’analyse démarre et s’arrête.</span><span class="sxs-lookup"><span data-stu-id="20992-509">User clearly knows what to do and when the scan starts and stops.</span></span> | <span data-ttu-id="20992-510">La visualisation du maillage spatial est fournie, mais l’utilisateur peut ne pas savoir clairement ce qu’il faut faire et aucune information de progression n’est fournie.</span><span class="sxs-lookup"><span data-stu-id="20992-510">Visualization of the spatial mesh is provided, but the user may not clearly know what to do and no progress information is provided.</span></span> | <span data-ttu-id="20992-511">Aucune visualisation de la maille.</span><span class="sxs-lookup"><span data-stu-id="20992-511">No visualization of mesh.</span></span> <span data-ttu-id="20992-512">Aucune information n’est fournie à l’utilisateur quant à son emplacement ou au démarrage ou à l’arrêt de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="20992-512">No guidance information provided to the user regarding where to look, or when the scan starts/stops.</span></span> |

### <a name="how-to-measure"></a><span data-ttu-id="20992-513">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-513">How to measure</span></span>

* <span data-ttu-id="20992-514">Au cours d’une analyse de la salle requise, des conseils visuels et audio sont fournis pour indiquer l’emplacement et le moment du démarrage et de l’arrêt de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="20992-514">During a required room scan, visual and audio guidance is provided indicating where to look, and when to start and stop scanning.</span></span>

### <a name="recommendations"></a><span data-ttu-id="20992-515">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-515">Recommendations</span></span>

* <span data-ttu-id="20992-516">Indiquez la quantité de volume total des utilisateurs avoisinants qui doit faire partie de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="20992-516">Indicate how much of the total volume in the users vicinity needs to be part of the experience.</span></span>
* <span data-ttu-id="20992-517">Communiquer quand l’analyse démarre et s’arrête, comme un indicateur de progression.</span><span class="sxs-lookup"><span data-stu-id="20992-517">Communicate when the scan starts and stops such as a progress indicator.</span></span>
* <span data-ttu-id="20992-518">Utilisez une visualisation de la maille pendant l’analyse.</span><span class="sxs-lookup"><span data-stu-id="20992-518">Use a visualization of the mesh during the scan.</span></span>
* <span data-ttu-id="20992-519">Fournissez des signaux visuels et audio pour encourager l’utilisateur à regarder et à se déplacer dans la pièce.</span><span class="sxs-lookup"><span data-stu-id="20992-519">Provide visual and audio cues to encourage the user to look and move around the room.</span></span>
* <span data-ttu-id="20992-520">Informez l’utilisateur où accéder à pour améliorer les données.</span><span class="sxs-lookup"><span data-stu-id="20992-520">Inform the user where to go to improve the data.</span></span> <span data-ttu-id="20992-521">Dans de nombreux cas, il peut être préférable de dire à l’utilisateur ce qu’il doit faire (par exemple, regarder le plafond, regarder derrière le mobilier), afin d’obtenir la qualité d’analyse nécessaire.</span><span class="sxs-lookup"><span data-stu-id="20992-521">In many cases, it may be best to tell the user what they need to do (e.g. look at the ceiling, look behind furniture), in order to get the necessary scan quality.</span></span>

### <a name="resources"></a><span data-ttu-id="20992-522">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-522">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="20992-523">Documentation</span><span class="sxs-lookup"><span data-stu-id="20992-523">Documentation</span></span>

* [<span data-ttu-id="20992-524">Visualisation du balayage d’une pièce</span><span class="sxs-lookup"><span data-stu-id="20992-524">Room scan visualization</span></span>](room-scan-visualization.md)
* [<span data-ttu-id="20992-525">Étude de cas : développement des fonctionnalités de mappage spatial de HoloLens</span><span class="sxs-lookup"><span data-stu-id="20992-525">Case study: Expanding the spatial mapping capabilities of HoloLens</span></span>](case-study-expanding-the-spatial-mapping-capabilities-of-hololens.md)
* [<span data-ttu-id="20992-526">Étude de cas : conception de son spatial pour HoloTour</span><span class="sxs-lookup"><span data-stu-id="20992-526">Case study: Spatial sound design for HoloTour</span></span>](case-study-spatial-sound-design-for-holotour.md)
* [<span data-ttu-id="20992-527">Étude de cas : création d’une expérience immersive dans des fragments</span><span class="sxs-lookup"><span data-stu-id="20992-527">Case study: Creating an immersive experience in Fragments</span></span>](case-study-creating-an-immersive-experience-in-fragments.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="20992-528">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="20992-528">Tools and tutorials</span></span>

* [<span data-ttu-id="20992-529">Kit de pratiques de réalité mixte-UX</span><span class="sxs-lookup"><span data-stu-id="20992-529">Mixed Reality Toolkit - UX</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/UX)

## <a name="directional-indicators"></a><span data-ttu-id="20992-530">Indicateurs directionnels</span><span class="sxs-lookup"><span data-stu-id="20992-530">Directional indicators</span></span>

<span data-ttu-id="20992-531">Dans une application de réalité mixte, le contenu peut être en dehors du champ de vue ou bloqués par des objets réels.</span><span class="sxs-lookup"><span data-stu-id="20992-531">In a mixed reality app, content may be outside the field of view or occluded by real-world objects.</span></span> <span data-ttu-id="20992-532">Une application bien conçue permettra à l’utilisateur de trouver plus facilement du contenu non visible.</span><span class="sxs-lookup"><span data-stu-id="20992-532">A well designed app will make it easier for the user to find non-visible content.</span></span> <span data-ttu-id="20992-533">Les indicateurs directionnels signalent à un utilisateur un contenu important et fournissent des conseils sur le contenu relatif à la position de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-533">Directional indicators alert a user to important content and provide guidance to the content relative to the user's position.</span></span> <span data-ttu-id="20992-534">Les instructions relatives au contenu non visible peuvent prendre la forme d’émetteurs de sons, de flèches directionnelles ou de signaux visuels directs.</span><span class="sxs-lookup"><span data-stu-id="20992-534">Guidance to non-visible content can take the form of sound emitters, directional arrows, or direct visual cues.</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-535">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-535">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-536"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-536"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-537"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-537"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-538">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-538">✔️</span></span></td>
        <td><span data-ttu-id="20992-539">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-539">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-540">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-540">Quality criteria</span></span>

|  <span data-ttu-id="20992-541">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-541">Best</span></span>  |  <span data-ttu-id="20992-542">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-542">Meets</span></span> |  <span data-ttu-id="20992-543">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-543">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="20992-544">Les signaux audio et visuel guident directement l’utilisateur vers du contenu pertinent en dehors du champ de vue.</span><span class="sxs-lookup"><span data-stu-id="20992-544">Visual and audio cues directly guide the user to relevant content outside the field of view.</span></span> | <span data-ttu-id="20992-545">Une flèche ou un indicateur qui dirige l’utilisateur dans la direction générale du contenu.</span><span class="sxs-lookup"><span data-stu-id="20992-545">An arrow or some indicator that points the user in the general direction of the content.</span></span> | <span data-ttu-id="20992-546">Le contenu pertinent est en dehors du champ de la vue, et de mauvaises instructions de localisation sont fournies à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="20992-546">Relevant content is outside of the field of view, and poor or no location guidance is provided to the user.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="20992-547">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-547">How to measure</span></span>

* <span data-ttu-id="20992-548">Le contenu pertinent en dehors du champ utilisateur de la vue est détectable via des signaux visuels et/ou audio.</span><span class="sxs-lookup"><span data-stu-id="20992-548">Relevant content outside of the user field of view is discoverable through visual and/or audio cues.</span></span>

### <a name="recommendations"></a><span data-ttu-id="20992-549">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-549">Recommendations</span></span>

* <span data-ttu-id="20992-550">Quand le contenu pertinent est en dehors du champ de vue de l’utilisateur, utilisez des indicateurs directionnels et des signaux audio pour guider l’utilisateur vers le contenu.</span><span class="sxs-lookup"><span data-stu-id="20992-550">When relevant content is outside the user's field of view, use directional indicators and audio cues to guide the user to the content.</span></span> <span data-ttu-id="20992-551">Dans de nombreux cas, un guide visuel direct est préférable sur les flèches directionnelles.</span><span class="sxs-lookup"><span data-stu-id="20992-551">In many cases, a direct visual guide is preferred over directional arrows.</span></span>
* <span data-ttu-id="20992-552">Les indicateurs directionnels ne doivent pas être intégrés au curseur.</span><span class="sxs-lookup"><span data-stu-id="20992-552">Directional indicators should not be built into the cursor.</span></span>

### <a name="resources"></a><span data-ttu-id="20992-553">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-553">Resources</span></span>

* [<span data-ttu-id="20992-554">Image holographique</span><span class="sxs-lookup"><span data-stu-id="20992-554">Holographic frame</span></span>](holographic-frame.md)

## <a name="data-loading"></a><span data-ttu-id="20992-555">Chargement de données</span><span class="sxs-lookup"><span data-stu-id="20992-555">Data loading</span></span>

<span data-ttu-id="20992-556">Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours.</span><span class="sxs-lookup"><span data-stu-id="20992-556">A progress control provides feedback to the user that a long-running operation is underway.</span></span> <span data-ttu-id="20992-557">Cela peut signifier que l’utilisateur ne peut pas interagir avec l’application lorsque l’indicateur de progression est visible et peut également indiquer la durée du délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="20992-557">It can mean that the user cannot interact with the app when the progress indicator is visible and can also indicate how long the wait time might be.</span></span>

### <a name="device-impact"></a><span data-ttu-id="20992-558">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="20992-558">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="20992-559"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-559"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="20992-560"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="20992-560"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="20992-561">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-561">✔️</span></span></td>
        <td><span data-ttu-id="20992-562">✔️</span><span class="sxs-lookup"><span data-stu-id="20992-562">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="20992-563">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="20992-563">Quality criteria</span></span>

|  <span data-ttu-id="20992-564">Meilleures</span><span class="sxs-lookup"><span data-stu-id="20992-564">Best</span></span>  |  <span data-ttu-id="20992-565">Présente</span><span class="sxs-lookup"><span data-stu-id="20992-565">Meets</span></span> |  <span data-ttu-id="20992-566">Incident</span><span class="sxs-lookup"><span data-stu-id="20992-566">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="20992-567">Indicateur visuel animé, sous la forme d’une barre de progression ou d’un anneau, indiquant la progression pendant le chargement ou le traitement des données.</span><span class="sxs-lookup"><span data-stu-id="20992-567">Animated visual indicator, in the form of a progress bar or ring, showing progress during any data loading or processing.</span></span> <span data-ttu-id="20992-568">L’indicateur visuel fournit des indications sur la durée de l’attente.</span><span class="sxs-lookup"><span data-stu-id="20992-568">The visual indicator provides guidance on how long the wait could be.</span></span> | <span data-ttu-id="20992-569">L’utilisateur est informé que le chargement des données est en cours, mais il n’existe aucune indication sur la durée de l’attente.</span><span class="sxs-lookup"><span data-stu-id="20992-569">User is informed that data loading is in progress, but there is no indication of how long the wait could be.</span></span> | <span data-ttu-id="20992-570">Aucun chargement de données ou indicateur de processus pour la tâche ne dure plus de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="20992-570">No data loading or process indicators for task taking longer than 5 seconds.</span></span> |

### <a name="how-to-measure"></a><span data-ttu-id="20992-571">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="20992-571">How to measure</span></span>

* <span data-ttu-id="20992-572">Pendant le chargement des données, vérifiez qu’il n’y a pas d’état vide pendant plus de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="20992-572">During data loading verify there is no blank state for more than 5 seconds.</span></span>

### <a name="recommendations"></a><span data-ttu-id="20992-573">Recommandations</span><span class="sxs-lookup"><span data-stu-id="20992-573">Recommendations</span></span>

* <span data-ttu-id="20992-574">Fournissez un animateur de chargement des données qui indique la progression dans toutes les situations où l’utilisateur peut percevoir cette application comme étant bloquée ou bloquée.</span><span class="sxs-lookup"><span data-stu-id="20992-574">Provide a data loading animator showing progress in any situation when the user may perceive this app to have stalled or crashed.</span></span> <span data-ttu-id="20992-575">Une règle raisonnable est toute activité de « chargement » qui peut prendre plus de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="20992-575">A reasonable rule of thumb is any 'loading' activity that could take more than 5 seconds.</span></span>

### <a name="resources"></a><span data-ttu-id="20992-576">Ressources</span><span class="sxs-lookup"><span data-stu-id="20992-576">Resources</span></span>

* [<span data-ttu-id="20992-577">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="20992-577">Displaying progress</span></span>](progress.md)
