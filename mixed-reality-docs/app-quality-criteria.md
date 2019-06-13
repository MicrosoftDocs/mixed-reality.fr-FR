---
title: Critères de qualité des applications
description: Ce document décrit les principaux facteurs ayant un impact sur la qualité des applications de réalité mixte.
author: cjdgit
ms.author: crderr
ms.date: 03/21/2018
ms.topic: article
keywords: critères de qualité des applications, une réalité, mixte mixte des applications en réalité
ms.openlocfilehash: 8e635585c0981d81bf71fb5577232af28f2a0fdd
ms.sourcegitcommit: 150d258a23130026c8792da383a3993657841fb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/12/2019
ms.locfileid: "67024494"
---
# <a name="app-quality-criteria"></a><span data-ttu-id="9810d-104">Critères de qualité des applications</span><span class="sxs-lookup"><span data-stu-id="9810d-104">App quality criteria</span></span>

<span data-ttu-id="9810d-105">Ce document décrit les principaux facteurs ayant un impact sur la qualité des applications de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="9810d-105">This document describes the top factors impacting the quality of mixed reality apps.</span></span> <span data-ttu-id="9810d-106">Pour chaque facteur les informations suivantes sont fournies</span><span class="sxs-lookup"><span data-stu-id="9810d-106">For each factor the following information is provided</span></span>
* <span data-ttu-id="9810d-107">Vue d’ensemble : une brève description du facteur de qualité et pourquoi il est important.</span><span class="sxs-lookup"><span data-stu-id="9810d-107">Overview – a brief description of the quality factor and why it is important.</span></span>
* <span data-ttu-id="9810d-108">Impact de l’appareil - type d’appareil de réalité mixte de fenêtre est affectée.</span><span class="sxs-lookup"><span data-stu-id="9810d-108">Device impact - which type of Window Mixed Reality device is impacted.</span></span>
* <span data-ttu-id="9810d-109">Critères de qualité – comment évaluer le facteur de qualité.</span><span class="sxs-lookup"><span data-stu-id="9810d-109">Quality criteria – how to evaluate the quality factor.</span></span>
* <span data-ttu-id="9810d-110">Comment mesurer : méthodes pour mesurer le problème (ou l’expérience).</span><span class="sxs-lookup"><span data-stu-id="9810d-110">How to measure – methods to measure (or experience) the issue.</span></span>
* <span data-ttu-id="9810d-111">Recommandations : résumées des approches pour fournir une meilleure expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-111">Recommendations – summary of approaches to provide a better user experience.</span></span>
* <span data-ttu-id="9810d-112">Ressources – développement pertinentes et les ressources de conception qui sont utiles pour créer de meilleures expériences d’application.</span><span class="sxs-lookup"><span data-stu-id="9810d-112">Resources – relevant developer and design resources that are useful to create better app experiences.</span></span>

## <a name="frame-rate"></a><span data-ttu-id="9810d-113">Fréquence d’images</span><span class="sxs-lookup"><span data-stu-id="9810d-113">Frame rate</span></span>

<span data-ttu-id="9810d-114">Fréquence d’images est le premier pilier de confort de la stabilité et l’utilisateur hologramme.</span><span class="sxs-lookup"><span data-stu-id="9810d-114">Frame rate is the first pillar of hologram stability and user comfort.</span></span> <span data-ttu-id="9810d-115">Fréquence d’images ci-dessous les cibles recommandées peut provoquer hologrammes apparaisse instable, un impact négatif sur le believability de l’expérience et ce qui peut entraîner fatigue des yeux.</span><span class="sxs-lookup"><span data-stu-id="9810d-115">Frame rate below the recommended targets can cause holograms to appear jittery, negatively impacting the believability of the experience and potentially causing eye fatigue.</span></span> <span data-ttu-id="9810d-116">La fréquence d’images cible pour votre expérience sur des casques IMMERSIFS Windows Mixed Reality sera soit 60 ou 90Hz selon les PC compatibles Windows mixte réalité que vous souhaitez prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="9810d-116">The target frame rate for your experience on Windows Mixed Reality immersive headsets will be either 60Hz or 90Hz depending on which Windows Mixed Reality Compatible PCs you wish to support.</span></span> <span data-ttu-id="9810d-117">Pour HoloLens la fréquence d’images cible est de 60Hz.</span><span class="sxs-lookup"><span data-stu-id="9810d-117">For HoloLens the target frame rate is 60Hz.</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-118">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-118">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-119"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-119"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-120"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-120"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-121">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-121">✔️</span></span></td>
        <td><span data-ttu-id="9810d-122">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-122">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-123">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-123">Quality criteria</span></span>

|  <span data-ttu-id="9810d-124">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-124">Best</span></span>  |  <span data-ttu-id="9810d-125">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-125">Meets</span></span> |  <span data-ttu-id="9810d-126">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-126">Fail</span></span> |
--- | --- | ---
| <span data-ttu-id="9810d-127">L’application satisfait régulièrement les images par le deuxième objectif (i/s) pour l’appareil cible : 60 i/s sur HoloLens ; 90 i/s sur les PC Ultra ; et 60 i/s sur les PC grand public.</span><span class="sxs-lookup"><span data-stu-id="9810d-127">The app consistently meets frames per second (FPS) goal for target device: 60fps on HoloLens; 90fps on Ultra PCs; and 60fps on mainstream PCs.</span></span> | <span data-ttu-id="9810d-128">L’application a gouttes de frame intermittents ne pas entraver l’expérience core ; ou i/s est systématiquement inférieurs à l’objectif souhaité, mais n’entrave pas l’expérience de l’application.</span><span class="sxs-lookup"><span data-stu-id="9810d-128">The app has intermittent frame drops not impeding the core experience; or FPS is consistently lower than desired goal but doesn’t impede the app experience.</span></span> | <span data-ttu-id="9810d-129">L’application rencontre une chute de la fréquence d’images en moyenne de toutes les dix secondes ou moins.</span><span class="sxs-lookup"><span data-stu-id="9810d-129">The app is experiencing a drop in frame rate on average every ten seconds or less.</span></span> |

### <a name="how-to-measure"></a><span data-ttu-id="9810d-130">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-130">How to measure</span></span>

* <span data-ttu-id="9810d-131">Un graphique de taux de frame en temps réel est fourni par le biais par la [Windows Device Portal](using-the-windows-device-portal.md#system-performance) sous « Performances du système ».</span><span class="sxs-lookup"><span data-stu-id="9810d-131">A real-time frame rate graph is provided through by the [Windows Device Portal](using-the-windows-device-portal.md#system-performance) under "System Performance".</span></span>
* <span data-ttu-id="9810d-132">Pour le débogage de développement, ajoutez un compteur de diagnostic de taux de trames dans l’application.</span><span class="sxs-lookup"><span data-stu-id="9810d-132">For development debugging, add a frame rate diagnostic counter into the app.</span></span> <span data-ttu-id="9810d-133">Consultez les ressources pour un exemple de compteur.</span><span class="sxs-lookup"><span data-stu-id="9810d-133">See Resources for a sample counter.</span></span>
* <span data-ttu-id="9810d-134">Supprime des taux de cadre peut être testées dans l’appareil pendant l’exécution de l’application en déplaçant votre tête de gauche à droite.</span><span class="sxs-lookup"><span data-stu-id="9810d-134">Frame rate drops can be experienced in device while the app is running by moving your head from side to side.</span></span> <span data-ttu-id="9810d-135">Si l’hologramme indique un mouvement instable inattendu, basse fréquence d’images ou le plan de la stabilité est probablement la cause.</span><span class="sxs-lookup"><span data-stu-id="9810d-135">If the hologram shows unexpected jittery movement, then low frame rate or the stability plane is likely the cause.</span></span>

### <a name="recommendations"></a><span data-ttu-id="9810d-136">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-136">Recommendations</span></span>

* <span data-ttu-id="9810d-137">Ajouter un compteur de taux de trames au début du travail de développement.</span><span class="sxs-lookup"><span data-stu-id="9810d-137">Add a frame rate counter at the beginning of the development work.</span></span>
* <span data-ttu-id="9810d-138">Les modifications qui peuvent entraîner une baisse de la fréquence d’images doivent être évaluées et correctement résolues comme un bogue de performances.</span><span class="sxs-lookup"><span data-stu-id="9810d-138">Changes that incur a drop in frame rate should be evaluated and appropriately resolved as a performance bug.</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-139">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-139">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="9810d-140">Documentation</span><span class="sxs-lookup"><span data-stu-id="9810d-140">Documentation</span></span>

* [<span data-ttu-id="9810d-141">Comprendre les performances pour la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="9810d-141">Understanding Performance for Mixed Reality</span></span>](understanding-performance-for-mixed-reality.md)
* [<span data-ttu-id="9810d-142">Fréquence d’images et la stabilité HOLOGRAMME</span><span class="sxs-lookup"><span data-stu-id="9810d-142">Hologram stability and framerate</span></span>](hologram-stability.md#frame-rate)
* [<span data-ttu-id="9810d-143">Budget de performances Asset</span><span class="sxs-lookup"><span data-stu-id="9810d-143">Asset performance budget</span></span>](asset-creation-process.md)
* [<span data-ttu-id="9810d-144">Recommandations de performances pour Unity</span><span class="sxs-lookup"><span data-stu-id="9810d-144">Performance recommendations for Unity</span></span>](performance-recommendations-for-unity.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="9810d-145">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="9810d-145">Tools and tutorials</span></span>

* [<span data-ttu-id="9810d-146">Affichage du compteur MRToolkit, i/s</span><span class="sxs-lookup"><span data-stu-id="9810d-146">MRToolkit, FPS counter display</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Utilities/README.md)
* [<span data-ttu-id="9810d-147">MRToolkit, Shaders</span><span class="sxs-lookup"><span data-stu-id="9810d-147">MRToolkit, Shaders</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Utilities/Shaders)

#### <a name="external-references"></a><span data-ttu-id="9810d-148">Références externes</span><span class="sxs-lookup"><span data-stu-id="9810d-148">External references</span></span>

* [<span data-ttu-id="9810d-149">Unity, optimisation des applications mobiles</span><span class="sxs-lookup"><span data-stu-id="9810d-149">Unity, Optimizing mobile applications</span></span>](https://www.youtube.com/watch?v=j4YAY36xjwE)

## <a name="hologram-stability"></a><span data-ttu-id="9810d-150">Stabilité HOLOGRAMME</span><span class="sxs-lookup"><span data-stu-id="9810d-150">Hologram stability</span></span>

<span data-ttu-id="9810d-151">Hologrammes stables augmentera l’utilisation et believability de votre application et créer une expérience d’affichage plus à l’aise pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-151">Stable holograms will increase the usability and believability of your app, and create a more comfortable viewing experience for the user.</span></span> <span data-ttu-id="9810d-152">La qualité de la stabilité hologramme est un résultat de développement de la bonne application et la capacité du périphérique (track) de comprendre son environnement.</span><span class="sxs-lookup"><span data-stu-id="9810d-152">The quality of hologram stability is a result of good app development and the device's ability to understand (track) its environment.</span></span> <span data-ttu-id="9810d-153">Tandis que la fréquence d’images est le premier pilier de la stabilité, d’autres facteurs peuvent avoir un impact sur la stabilité, y compris :</span><span class="sxs-lookup"><span data-stu-id="9810d-153">While frame rate is the first pillar of stability, other factors can impact stability including:</span></span>

* <span data-ttu-id="9810d-154">Utilisation du plan de stabilisation</span><span class="sxs-lookup"><span data-stu-id="9810d-154">Use of the stabilization plane</span></span>
* <span data-ttu-id="9810d-155">Distance et ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="9810d-155">Distance to spatial anchors</span></span>
* <span data-ttu-id="9810d-156">Suivi</span><span class="sxs-lookup"><span data-stu-id="9810d-156">Tracking</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-157">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-157">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-158"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-158"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-159"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-159"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-160">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-160">✔️</span></span></td>
        <td><span data-ttu-id="9810d-161">❌</span><span class="sxs-lookup"><span data-stu-id="9810d-161">❌</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-162">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-162">Quality criteria</span></span>

|  <span data-ttu-id="9810d-163">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-163">Best</span></span>  |  <span data-ttu-id="9810d-164">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-164">Meets</span></span> |  <span data-ttu-id="9810d-165">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-165">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="9810d-166">Hologrammes s’affichent régulièrement stables.</span><span class="sxs-lookup"><span data-stu-id="9810d-166">Holograms consistently appear stable.</span></span> | <span data-ttu-id="9810d-167">Contenu secondaire présente un mouvement inattendu ; ou un mouvement inattendu n’entrave pas l’expérience de l’application globale.</span><span class="sxs-lookup"><span data-stu-id="9810d-167">Secondary content exhibits unexpected movement; or unexpected movement does not impede overall app experience.</span></span> | <span data-ttu-id="9810d-168">Contenu principal dans le frame présente un mouvement inattendu.</span><span class="sxs-lookup"><span data-stu-id="9810d-168">Primary content in frame exhibits unexpected movement.</span></span> |

### <a name="how-to-measure"></a><span data-ttu-id="9810d-169">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-169">How to measure</span></span>

<span data-ttu-id="9810d-170">Tandis que le port de l’appareil et l’expérience d’affichage :</span><span class="sxs-lookup"><span data-stu-id="9810d-170">While wearing the device and viewing the experience:</span></span>

* <span data-ttu-id="9810d-171">Déplacer votre tête de gauche à droite, si les hologrammes affichent un mouvement inattendu basse fréquence d’images ou un alignement incorrect du plan de stabilité pour le plan focal est la cause probable.</span><span class="sxs-lookup"><span data-stu-id="9810d-171">Move your head from side to side, if the holograms show unexpected movement then low frame rate or improper alignment of the stability plane to the focal plane is the likely cause.</span></span>
* <span data-ttu-id="9810d-172">Déplacer l’environnement et hologrammes, rechercher des comportements tels que natation et jumpiness.</span><span class="sxs-lookup"><span data-stu-id="9810d-172">Move around the holograms and environment, look for behaviors such as swim and jumpiness.</span></span> <span data-ttu-id="9810d-173">Ce type de déplacement est probablement due à l’analyse de périphérique ne pas l’environnement, ou la distance à l’ancre spatial.</span><span class="sxs-lookup"><span data-stu-id="9810d-173">This type of motion is likely caused by the device not tracking the environment, or the distance to the spatial anchor.</span></span>
* <span data-ttu-id="9810d-174">Si de grands ou hologrammes plusieurs se trouvent dans le frame, observer le comportement de hologramme à différentes profondeurs tandis que le déplacement de votre position principale de gauche à droite, si tremblement apparaît cela est probablement causé par le plan de stabilisation.</span><span class="sxs-lookup"><span data-stu-id="9810d-174">If large or multiple holograms are in the frame, observe hologram behavior at various depths while moving your head position from side to side, if shakiness appears this is likely caused by the stabilization plane.</span></span>

### <a name="recomendations"></a><span data-ttu-id="9810d-175">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-175">Recomendations</span></span>

* <span data-ttu-id="9810d-176">Ajouter un compteur de taux de trames au début du travail de développement.</span><span class="sxs-lookup"><span data-stu-id="9810d-176">Add an frame rate counter at the beginning of the development work.</span></span>
* <span data-ttu-id="9810d-177">Utilisez le plan de stabilisation.</span><span class="sxs-lookup"><span data-stu-id="9810d-177">Use the stabilization plane.</span></span>
* <span data-ttu-id="9810d-178">Toujours afficher hologrammes ancrés dans 3 mètres de leur point d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="9810d-178">Always render anchored holograms within 3 meters of their anchor.</span></span>
* <span data-ttu-id="9810d-179">Assurez-vous que votre environnement est configuré pour le suivi approprié.</span><span class="sxs-lookup"><span data-stu-id="9810d-179">Make sure your environment is setup for proper tracking.</span></span>
* <span data-ttu-id="9810d-180">Votre expérience afin d’éviter les hologrammes à différents niveaux de profondeur focal dans le cadre de la conception.</span><span class="sxs-lookup"><span data-stu-id="9810d-180">Design your experience to avoid holograms at various focal depth levels within the frame.</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-181">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-181">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="9810d-182">Documentation</span><span class="sxs-lookup"><span data-stu-id="9810d-182">Documentation</span></span>

* [<span data-ttu-id="9810d-183">Fréquence d’images et la stabilité HOLOGRAMME</span><span class="sxs-lookup"><span data-stu-id="9810d-183">Hologram stability and framerate</span></span>](hologram-stability.md#frame-rate)
* [<span data-ttu-id="9810d-184">Étude de cas, à l’aide du plan de stabilisation</span><span class="sxs-lookup"><span data-stu-id="9810d-184">Case study, Using the stabilization plane</span></span>](case-study-using-the-stabilization-plane-to-reduce-holographic-turbulence.md)
* [<span data-ttu-id="9810d-185">Comprendre les performances pour la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="9810d-185">Understanding Performance for Mixed Reality</span></span>](understanding-performance-for-mixed-reality.md)
* [<span data-ttu-id="9810d-186">Recommandations de performances pour Unity</span><span class="sxs-lookup"><span data-stu-id="9810d-186">Performance recommendations for Unity</span></span>](performance-recommendations-for-unity.md)
* [<span data-ttu-id="9810d-187">Ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="9810d-187">Spatial anchors</span></span>](spatial-anchors.md)
* [<span data-ttu-id="9810d-188">Gestion des erreurs de suivi</span><span class="sxs-lookup"><span data-stu-id="9810d-188">Handling tracking errors</span></span>](coordinate-systems.md#handling-tracking-errors)
* [<span data-ttu-id="9810d-189">Système de référence stationnaire</span><span class="sxs-lookup"><span data-stu-id="9810d-189">Stationary frame of reference</span></span>](coordinate-systems.md#stationary-frame-of-reference)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="9810d-190">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="9810d-190">Tools and tutorials</span></span>

* [<span data-ttu-id="9810d-191">Kit d’accompagnement MR, Kinect IPD</span><span class="sxs-lookup"><span data-stu-id="9810d-191">MR Companion Kit, Kinect IPD</span></span>](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/KinectIPD)

## <a name="holograms-position-on-real-surfaces"></a><span data-ttu-id="9810d-192">Position hologrammes sur des surfaces réels</span><span class="sxs-lookup"><span data-stu-id="9810d-192">Holograms position on real surfaces</span></span>

<span data-ttu-id="9810d-193">Distorsions de hologrammes avec des objets physiques (si destinés à être mis en relation avec eux) est une indication claire de l’union de hologrammes et réalistes.</span><span class="sxs-lookup"><span data-stu-id="9810d-193">Misalignments of holograms with physical objects (if intended to be placed in relation to one another) is a clear indication of the non-union of holograms and real-world.</span></span> <span data-ttu-id="9810d-194">Précision de l’emplacement doit être par rapport aux besoins du scénario ; par exemple, placement surface général peut utiliser le mappage spatial, mais plus précise placement nécessitera certains utilisation de marqueurs et d’étalonnage.</span><span class="sxs-lookup"><span data-stu-id="9810d-194">Accuracy of the placement should be relative to the needs of the scenario; for example, general surface placement can use the spatial map, but more accurate placement will require some use of markers and calibration.</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-195">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-195">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-196"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-196"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-197"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-197"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-198">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-198">✔️</span></span></td>
        <td><span data-ttu-id="9810d-199">❌</span><span class="sxs-lookup"><span data-stu-id="9810d-199">❌</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-200">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-200">Quality criteria</span></span>

|  <span data-ttu-id="9810d-201">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-201">Best</span></span>  |  <span data-ttu-id="9810d-202">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-202">Meets</span></span> |  <span data-ttu-id="9810d-203">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-203">Fail</span></span> |
--- | --- | ---
| <span data-ttu-id="9810d-204">Hologrammes alignent sur la surface en général dans les centimètres à pouces plage.</span><span class="sxs-lookup"><span data-stu-id="9810d-204">Holograms align to the surface typically in the centimeters to inches range.</span></span> <span data-ttu-id="9810d-205">Si plus de précision est requise, l’application doit fournir un moyen efficace pour la collaboration au sein de la spécification de l’application souhaitée.</span><span class="sxs-lookup"><span data-stu-id="9810d-205">If more accuracy is required, the app should provide an efficient means for collaboration within the desired app spec.</span></span> | <span data-ttu-id="9810d-206">N/A</span><span class="sxs-lookup"><span data-stu-id="9810d-206">NA</span></span> | <span data-ttu-id="9810d-207">Les hologrammes apparaissent non alignés avec l’objet cible physique par rompre le plan de surface ou qui apparaissent pour les faire flotter en dehors de la surface.</span><span class="sxs-lookup"><span data-stu-id="9810d-207">The holograms appear unaligned with the physical target object by either breaking the surface plane or appearing to float away from the surface.</span></span> <span data-ttu-id="9810d-208">Si l’exactitude est requis, hologrammes doivent répondre à la spécification de la proximité du scénario.</span><span class="sxs-lookup"><span data-stu-id="9810d-208">If accuracy is required, Holograms should meet the proximity spec of the scenario.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="9810d-209">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-209">How to measure</span></span>

* <span data-ttu-id="9810d-210">Hologrammes sont placés sur la carte spatial ne doivent pas apparaître considérablement flotter au-dessus ou au-dessous de la surface.</span><span class="sxs-lookup"><span data-stu-id="9810d-210">Holograms that are placed on spatial map should not appear to dramatically float above or below the surface.</span></span>
* <span data-ttu-id="9810d-211">Hologrammes qui nécessitent le positionnement précis doivent avoir une forme de marqueur et système d’étalonnage adaptée aux besoins du scénario le.</span><span class="sxs-lookup"><span data-stu-id="9810d-211">Holograms that require accurate placement should have some form of marker and calibration system that is accurate to the scenario's requirement.</span></span>

### <a name="recommendations"></a><span data-ttu-id="9810d-212">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-212">Recommendations</span></span>

* <span data-ttu-id="9810d-213">Mappage spatial est utile pour placer des objets sur des surfaces lors de la précision n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9810d-213">Spatial map is useful for placing objects on surfaces when precision isn’t required.</span></span>
* <span data-ttu-id="9810d-214">La meilleure précision, utiliser marqueurs ou des affiches pour déterminer les hologrammes et une manette Xbox (ou un mécanisme d’alignement manuel) d’étalonnage finale.</span><span class="sxs-lookup"><span data-stu-id="9810d-214">For the best precision, use markers or posters to set the holograms and an Xbox controller (or some manual alignment mechanism) for final calibration.</span></span>
* <span data-ttu-id="9810d-215">Envisagez de diviser hologrammes de très grande taille en parties logiques et d’alignement de chaque partie vers l’aire.</span><span class="sxs-lookup"><span data-stu-id="9810d-215">Consider breaking extra-large holograms into logical parts and aligning each part to the surface.</span></span>
* <span data-ttu-id="9810d-216">Mal ensemble interpupilary distance (IPD) peut également un effet sur les alignement hologramme.</span><span class="sxs-lookup"><span data-stu-id="9810d-216">Improperly set interpupilary distance (IPD) can also effect hologram alignment.</span></span> <span data-ttu-id="9810d-217">Configurez toujours HoloLens à IPD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-217">Always configure HoloLens to the user's IPD.</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-218">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-218">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="9810d-219">Documentation</span><span class="sxs-lookup"><span data-stu-id="9810d-219">Documentation</span></span>

* [<span data-ttu-id="9810d-220">Placement de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="9810d-220">Spatial mapping placement</span></span>](spatial-mapping.md#placement)
* [<span data-ttu-id="9810d-221">Espace de processus d’analyse</span><span class="sxs-lookup"><span data-stu-id="9810d-221">Room scanning process</span></span>](case-study-expanding-the-spatial-mapping-capabilities-of-hololens.md)
* [<span data-ttu-id="9810d-222">Meilleures pratiques d’ancres spatial</span><span class="sxs-lookup"><span data-stu-id="9810d-222">Spatial anchors best practices</span></span>](spatial-anchors.md#best-practices)
* [<span data-ttu-id="9810d-223">Gestion des erreurs de suivi</span><span class="sxs-lookup"><span data-stu-id="9810d-223">Handling tracking errors</span></span>](coordinate-systems.md#handling-tracking-errors)
* [<span data-ttu-id="9810d-224">Mappage spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="9810d-224">Spatial mapping in Unity</span></span>](spatial-mapping-in-unity.md)
* [<span data-ttu-id="9810d-225">Vue d’ensemble du développement Vuforia</span><span class="sxs-lookup"><span data-stu-id="9810d-225">Vuforia development overview</span></span>](vuforia-development-overview.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="9810d-226">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="9810d-226">Tools and tutorials</span></span>

* [<span data-ttu-id="9810d-227">Réalité mixte - Fonctionnalités spatiales - Cours 230 : Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="9810d-227">MR Spatial 230: Spatial mapping</span></span>](holograms-230.md)
* [<span data-ttu-id="9810d-228">MR boîte à outils, bibliothèques de mappage Spatial</span><span class="sxs-lookup"><span data-stu-id="9810d-228">MR Toolkit, Spatial Mapping Libraries</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/SpatialMapping/README.md)
* [<span data-ttu-id="9810d-229">Kit de Compagnon MR, exemple d’étalonnage de Poster</span><span class="sxs-lookup"><span data-stu-id="9810d-229">MR Companion Kit, Poster Calibration Sample</span></span>](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/PosterCalibrationSample)
* [<span data-ttu-id="9810d-230">Kit d’accompagnement MR, Kinect IPD</span><span class="sxs-lookup"><span data-stu-id="9810d-230">MR Companion Kit, Kinect IPD</span></span>](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/KinectIPD)

#### <a name="external-references"></a><span data-ttu-id="9810d-231">Références externes</span><span class="sxs-lookup"><span data-stu-id="9810d-231">External references</span></span>

* [<span data-ttu-id="9810d-232">Étude de cas Lowes, alignement de précision</span><span class="sxs-lookup"><span data-stu-id="9810d-232">Lowes Case Study, Precision alignment</span></span>](https://www.youtube.com/watch?v=LceMdyKZ4PI)

## <a name="viewing-zone-of-comfort"></a><span data-ttu-id="9810d-233">Zone d’affichage de confort</span><span class="sxs-lookup"><span data-stu-id="9810d-233">Viewing zone of comfort</span></span>

<span data-ttu-id="9810d-234">Contrôle les développeurs d’applications où les yeux des utilisateurs convergent en plaçant le contenu et hologrammes à des profondeurs différents.</span><span class="sxs-lookup"><span data-stu-id="9810d-234">App developers control where users' eyes converge by placing content and holograms at various depths.</span></span> <span data-ttu-id="9810d-235">Les utilisateurs qui HoloLens inclura toujours à m 2.0 pour maintenir une image claire, car HoloLens affiche sont fixés à une distance optique environ 2.0m éloignée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-235">Users wearing HoloLens will always accommodate to 2.0m to maintain a clear image because HoloLens displays are fixed at an optical distance approximately 2.0m away from the user.</span></span> <span data-ttu-id="9810d-236">Profondeur de contenu incorrecte peut entraîner une gêne visual ou fatigue.</span><span class="sxs-lookup"><span data-stu-id="9810d-236">Improper content depth can lead to visual discomfort or fatigue.</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-237">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-237">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-238"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-238"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-239"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-239"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-240">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-240">✔️</span></span></td>
        <td><span data-ttu-id="9810d-241">❌</span><span class="sxs-lookup"><span data-stu-id="9810d-241">❌</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-242">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-242">Quality criteria</span></span>

<table>
<tr>
<td> <span data-ttu-id="9810d-243">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-243">Best</span></span> </td><td><ul>
<li><span data-ttu-id="9810d-244">Placer le contenu à 2m.</span><span class="sxs-lookup"><span data-stu-id="9810d-244">Place content at 2m.</span></span></li><li><span data-ttu-id="9810d-245">Lorsque hologrammes ne peut pas être placés au 2m et les conflits entre convergence et d’hébergement ne peut pas être évitées, la zone optimale pour la sélection élective hologramme est entre 1,25 m et 5m.</span><span class="sxs-lookup"><span data-stu-id="9810d-245">When holograms cannot be placed at 2m and conflicts between convergence and accommodation cannot be avoided, the optimal zone for hologram placement is between 1.25m and 5m.</span></span></li><li><span data-ttu-id="9810d-246">Dans tous les cas, les concepteurs doivent structurer le contenu à encourager les utilisateurs à interagir 1 + m (par exemple, ajuster la taille du contenu et les paramètres de sélection élective par défaut).</span><span class="sxs-lookup"><span data-stu-id="9810d-246">In every case, designers should structure content to encourage users to interact 1+ m away (e.g. adjust content size and default placement parameters).</span></span></li><li><span data-ttu-id="9810d-247">Sauf si spécifiquement ne pas requis par le scénario, un plan de découpage doit être implémentez avec fadeout en commençant à 1 million.</span><span class="sxs-lookup"><span data-stu-id="9810d-247">Unless specifically not required by the scenario, a clipping plane should be implement with fadeout starting at 1m.</span></span></li><li><span data-ttu-id="9810d-248">Dans les cas où une observation plus proche d’un hologramme immobile est requise, le contenu ne doit pas être à moins de 50cm.</span><span class="sxs-lookup"><span data-stu-id="9810d-248">In cases where closer observation of a motionless hologram is required, the content should not be closer than 50cm.</span></span></li>
</ul></td>
</tr><tr>
<td> <span data-ttu-id="9810d-249">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-249">Meets</span></span></td><td> <span data-ttu-id="9810d-250">Contenu se trouve dans le Guide de visualisation et de mouvement, mais une utilisation incorrecte ou aucune utilisation du plan de découpage.</span><span class="sxs-lookup"><span data-stu-id="9810d-250">Content is within the viewing and motion guidance, but improper use or no use of the clipping plane.</span></span></td>
</tr><tr>
<td> <span data-ttu-id="9810d-251">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-251">Fail</span></span> </td><td> <span data-ttu-id="9810d-252">Le contenu est présenté trop près (généralement &lt;1,25 m, ou &lt;50 cm pour hologrammes STATIONNAIRES nécessitant une observation plus proche.)</span><span class="sxs-lookup"><span data-stu-id="9810d-252">Content is presented too close (typically &lt;1.25m, or &lt;50cm for stationary holograms requiring closer observation.)</span></span></td>
</tr>
</table>

### <a name="how-to-measure"></a><span data-ttu-id="9810d-253">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-253">How to measure</span></span>

* <span data-ttu-id="9810d-254">Contenu doivent être généralement 2m absent, mais ne plus proche que 1,25 ou plus : optez 5m.</span><span class="sxs-lookup"><span data-stu-id="9810d-254">Content should typically be 2m away, but no closer than 1.25 or further than 5m.</span></span>
* <span data-ttu-id="9810d-255">À quelques exceptions près, la distance de rendu de découpage HoloLens doit être définie à .85CM avec fadeout du contenu, en commençant à 1 million.</span><span class="sxs-lookup"><span data-stu-id="9810d-255">With few exceptions, the HoloLens clipping render distance should be set to .85CM with fadeout of content starting at 1m.</span></span> <span data-ttu-id="9810d-256">Approche le contenu et notez l’effet de plan de découpage.</span><span class="sxs-lookup"><span data-stu-id="9810d-256">Approach the content and note the clipping plane effect.</span></span>
* <span data-ttu-id="9810d-257">Contenu stationnaire ne doit pas être à moins de 50cm de suite.</span><span class="sxs-lookup"><span data-stu-id="9810d-257">Stationary content should not be closer than 50cm away.</span></span>

### <a name="recommendations"></a><span data-ttu-id="9810d-258">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-258">Recommendations</span></span>

* <span data-ttu-id="9810d-259">Concevoir le contenu de la distance d’optimiser l’affichage de 2m.</span><span class="sxs-lookup"><span data-stu-id="9810d-259">Design content for the optimal viewing distance of 2m.</span></span>
* <span data-ttu-id="9810d-260">Définit la distance de rendu de découpage à 85cm avec fadeout du contenu, en commençant à 1 million.</span><span class="sxs-lookup"><span data-stu-id="9810d-260">Set the clipping render distance to 85cm with fadeout of content starting at 1m.</span></span>
* <span data-ttu-id="9810d-261">Pour hologrammes STATIONNAIRES nécessitant l’affichage de plus près, le plan de découpage doit être non moins de 30 centimètres et fadeout doit commencer au moins 10cm en dehors du plan de découpage.</span><span class="sxs-lookup"><span data-stu-id="9810d-261">For stationary holograms that need closer viewing, the clipping plane should be no closer than 30cm and fadeout should start at least 10cm away from the clipping plane.</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-262">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-262">Resources</span></span>

* [<span data-ttu-id="9810d-263">Restituer la distance</span><span class="sxs-lookup"><span data-stu-id="9810d-263">Render distance</span></span>](hologram-stability.md#hologram-render-distances)
* [<span data-ttu-id="9810d-264">Point de focus dans Unity</span><span class="sxs-lookup"><span data-stu-id="9810d-264">Focus point in Unity</span></span>](focus-point-in-unity.md)
* [<span data-ttu-id="9810d-265">Expérimenter la mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="9810d-265">Experimenting with scale</span></span>](scale.md#experimenting-with-scale)
* [<span data-ttu-id="9810d-266">Texte, la taille de police recommandée</span><span class="sxs-lookup"><span data-stu-id="9810d-266">Text, Recommended font size</span></span>](typography.md#recommended-font-size)

## <a name="depth-switching"></a><span data-ttu-id="9810d-267">Profondeur de commutation</span><span class="sxs-lookup"><span data-stu-id="9810d-267">Depth switching</span></span>

<span data-ttu-id="9810d-268">Quelle que soit la zone d’affichage des problèmes de confort, les demandes de l’utilisateur de basculer rapidement ou fréquemment entre près et présent focal objets (y compris les hologrammes et contenu du monde réel) peuvent entraîner la fatigue oculomotor et de gêne générale.</span><span class="sxs-lookup"><span data-stu-id="9810d-268">Regardless of viewing zone of comfort issues, demands for the user to switch frequently or quickly between near and far focal objects (including holograms and real-world content) can lead to oculomotor fatigue, and general discomfort.</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-269">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-269">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-270"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-270"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-271"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-271"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-272">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-272">✔️</span></span></td>
        <td><span data-ttu-id="9810d-273">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-273">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-274">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-274">Quality criteria</span></span>

|  <span data-ttu-id="9810d-275">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-275">Best</span></span>  |  <span data-ttu-id="9810d-276">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-276">Meets</span></span> |  <span data-ttu-id="9810d-277">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-277">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="9810d-278">Profondeur limitée ou naturelle de commutation qui n’entraîne pas l’utilisateur peut se concentrer Queues.</span><span class="sxs-lookup"><span data-stu-id="9810d-278">Limited or natural depth switching that doesn’t cause the user to unnaturally refocus.</span></span> | <span data-ttu-id="9810d-279">Profondeur brusque commutateur core et conçu dans l’expérience de l’application, ou profondeur brusque qui est provoquée par le contenu réel inattendu.</span><span class="sxs-lookup"><span data-stu-id="9810d-279">Abrupt depth switch this is core and designed into the app experience, or abrupt depth switch that is caused by unexpected real-world content.</span></span> | <span data-ttu-id="9810d-280">Commutateur de profondeur cohérent, ou profondeur brusque changement qui n’est pas nécessaire ou core à l’expérience de l’application.</span><span class="sxs-lookup"><span data-stu-id="9810d-280">Consistent depth switch, or abrupt depth switching that isn’t necessary or core to the app experience.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="9810d-281">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-281">How to measure</span></span>

* <span data-ttu-id="9810d-282">Si l’application requiert l’utilisateur de manière cohérente et/ou brusquement définir le focus de profondeur, profondeur est problème de commutation.</span><span class="sxs-lookup"><span data-stu-id="9810d-282">If the app requires the user to consistently and/or abruptly change depth focus, there is depth switching problem.</span></span>

### <a name="recommendations"></a><span data-ttu-id="9810d-283">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-283">Recommendations</span></span>

* <span data-ttu-id="9810d-284">Conserver le contenu principal à un plan focal cohérent et assurez-vous que le plan de stabilisation correspond à la focale.</span><span class="sxs-lookup"><span data-stu-id="9810d-284">Keep primary content at a consistent focal plane and make sure the stabilization plane matches the focal plane.</span></span> <span data-ttu-id="9810d-285">Cela résoudra oculomotor fatigue et déplacement des hologramme inattendue.</span><span class="sxs-lookup"><span data-stu-id="9810d-285">This will alleviate oculomotor fatigue and unexpected hologram movement.</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-286">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-286">Resources</span></span>

* [<span data-ttu-id="9810d-287">Restituer la distance</span><span class="sxs-lookup"><span data-stu-id="9810d-287">Render distance</span></span>](hologram-stability.md#hologram-render-distances)
* [<span data-ttu-id="9810d-288">Point de focus dans Unity</span><span class="sxs-lookup"><span data-stu-id="9810d-288">Focus point in Unity</span></span>](focus-point-in-unity.md)

## <a name="use-of-spatial-sound"></a><span data-ttu-id="9810d-289">Utilisation de son spatial</span><span class="sxs-lookup"><span data-stu-id="9810d-289">Use of spatial sound</span></span>

<span data-ttu-id="9810d-290">En réalité mixte de Windows, le moteur audio fournit le composant auditif de l’expérience de réalité mixte en simulant 3D audio à l’aide de la direction, la distance et les simulations de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="9810d-290">In Windows Mixed Reality, the audio engine provides the aural component of the mixed reality experience by simulating 3D sound using direction, distance, and environmental simulations.</span></span> <span data-ttu-id="9810d-291">À l’aide de son spatial dans une application permet aux développeurs de placer convaincante des sons dans un espace tridimensionnel 3 (sphère) autour de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-291">Using spatial sound in an application allows developers to convincingly place sounds in a 3 dimensional space (sphere) all around the user.</span></span> <span data-ttu-id="9810d-292">Ces sons paraîtra comme si elles provenaient d’objets physiques réel ou les hologrammes de réalité mixte dans son environnement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-292">Those sounds will then seem as if they were coming from real physical objects or the mixed reality holograms in the user's surroundings.</span></span> <span data-ttu-id="9810d-293">Son spatial est un outil puissant pour immersion, d’accessibilité et la conception de l’expérience utilisateur dans les applications de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="9810d-293">Spatial sound is a powerful tool for immersion, accessibility, and UX design in mixed reality applications.</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-294">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-294">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-295"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-295"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-296"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-296"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-297">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-297">✔️</span></span></td>
        <td><span data-ttu-id="9810d-298">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-298">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-299">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-299">Quality criteria</span></span>

|  <span data-ttu-id="9810d-300">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-300">Best</span></span>  |  <span data-ttu-id="9810d-301">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-301">Meets</span></span> |  <span data-ttu-id="9810d-302">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-302">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="9810d-303">Son est logiquement spatialized, et l’expérience utilisateur utilise correctement son afin de faciliter objet découverte et commentaires des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9810d-303">Sound is logically spatialized, and the UX appropriately uses sound to assist with object discovery and user feedback.</span></span> <span data-ttu-id="9810d-304">Son est naturel et pertinents aux objets et normalisée entre le scénario.</span><span class="sxs-lookup"><span data-stu-id="9810d-304">Sound is natural and relevant to objects and normalized across the scenario.</span></span> | <span data-ttu-id="9810d-305">Audio spatial est utilisé convenablement pour believability mais manquant comme moyen de faciliter la détectabilité et les commentaires des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9810d-305">Spatial audio is used appropriately for believability but missing as means to help with user feedback and discoverability.</span></span> | <span data-ttu-id="9810d-306">Son n’est pas spatialized comme prévu, et/ou manque de son pour aider l’utilisateur au sein de l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-306">Sound is not spatialized as expected, and/or lack of sound to assist user within the UX.</span></span> <span data-ttu-id="9810d-307">Ou spatial audio a été pas considéré comme utilisé dans la conception du scénario.</span><span class="sxs-lookup"><span data-stu-id="9810d-307">Or spatial audio was not considered or used in the design of the scenario.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="9810d-308">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-308">How to measure</span></span>

* <span data-ttu-id="9810d-309">En règle générale, d’émettre des sons pertinentes à partir de hologrammes de cible (par ex., son écorce provenant HOLOGRAPHIQUE dog.)</span><span class="sxs-lookup"><span data-stu-id="9810d-309">In general, relevant sounds should emit from target holograms (eg., bark sound coming from holographic dog.)</span></span>
* <span data-ttu-id="9810d-310">Signaux audio doivent être utilisées dans l’expérience utilisateur pour aider l’utilisateur avec des commentaires ou une connaissance des actions en dehors du cadre HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="9810d-310">Sound cues should be used throughout the UX to assist the user with feedback or awareness of actions outside the holographic frame.</span></span>

### <a name="recommendations"></a><span data-ttu-id="9810d-311">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-311">Recommendations</span></span>

* <span data-ttu-id="9810d-312">Utilisez audio spatial afin de faciliter les interfaces utilisateur et de découverte de l’objet.</span><span class="sxs-lookup"><span data-stu-id="9810d-312">Use spatial audio to assist with object discovery and user interfaces.</span></span>
* <span data-ttu-id="9810d-313">Sons réels fonctionnent mieux que son non naturelle ou de synthèse.</span><span class="sxs-lookup"><span data-stu-id="9810d-313">Real sounds work better than synthesize or unnatural sound.</span></span>
* <span data-ttu-id="9810d-314">La plupart des sons doivent être spatialized.</span><span class="sxs-lookup"><span data-stu-id="9810d-314">Most sounds should be spatialized.</span></span>
* <span data-ttu-id="9810d-315">Évitez d’émetteurs invisibles.</span><span class="sxs-lookup"><span data-stu-id="9810d-315">Avoid invisible emitters.</span></span>
* <span data-ttu-id="9810d-316">Évitez les masques spatiale.</span><span class="sxs-lookup"><span data-stu-id="9810d-316">Avoid spatial masking.</span></span>
* <span data-ttu-id="9810d-317">Normaliser toutes les sons.</span><span class="sxs-lookup"><span data-stu-id="9810d-317">Normalize all sounds.</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-318">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-318">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="9810d-319">Documentation</span><span class="sxs-lookup"><span data-stu-id="9810d-319">Documentation</span></span>

* [<span data-ttu-id="9810d-320">Son spatial</span><span class="sxs-lookup"><span data-stu-id="9810d-320">Spatial sound</span></span>](spatial-sound.md)
* [<span data-ttu-id="9810d-321">Conception du son spatial</span><span class="sxs-lookup"><span data-stu-id="9810d-321">Spatial sound design</span></span>](spatial-sound-design.md)
* [<span data-ttu-id="9810d-322">Son spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="9810d-322">Spatial sound in Unity</span></span>](spatial-sound-in-unity.md)
* [<span data-ttu-id="9810d-323">Étude de cas, Spatial audio pour HoloTour</span><span class="sxs-lookup"><span data-stu-id="9810d-323">Case study, Spatial sound for HoloTour</span></span>](case-study-spatial-sound-design-for-holotour.md)
* [<span data-ttu-id="9810d-324">Étude de cas, à l’aide de son spatial dans RoboRaid</span><span class="sxs-lookup"><span data-stu-id="9810d-324">Case study, Using spatial sound in RoboRaid</span></span>](case-study-using-spatial-sound-in-roboraid.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="9810d-325">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="9810d-325">Tools and tutorials</span></span>

* [<span data-ttu-id="9810d-326">Réalité mixte - Fonctionnalités spatiales - Cours 220 : Son spatial</span><span class="sxs-lookup"><span data-stu-id="9810d-326">MR Spatial 220: Spatial sound</span></span>](holograms-220.md)
* [<span data-ttu-id="9810d-327">MRToolkit, Audio Spatial</span><span class="sxs-lookup"><span data-stu-id="9810d-327">MRToolkit, Spatial Audio</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/SpatialSound/README.md)

## <a name="focus-on-holographic-frame-fov-boundaries"></a><span data-ttu-id="9810d-328">Vous concentrer sur les limites du cadre HOLOGRAPHIQUE (angle d’ouverture)</span><span class="sxs-lookup"><span data-stu-id="9810d-328">Focus on holographic frame (FOV) boundaries</span></span>

<span data-ttu-id="9810d-329">Expériences utilisateur bien conçue peuvent créer et gérer un contexte utile de l’environnement virtuel qui s’étend sur les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9810d-329">Well-designed user experiences can create and maintain useful context of the virtual environment that extends around the users.</span></span> <span data-ttu-id="9810d-330">Atténuer l’effet des limites d’angle d’ouverture implique une conception réfléchie de contenu à l’échelle et le contexte, utilisez de signal audio spatial, les systèmes de conseils et position de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-330">Mitigating the effect of the FOV boundaries involves a thoughtful design of content scale and context, use of spatial audio, guidance systems, and the user's position.</span></span> <span data-ttu-id="9810d-331">Si est correctement effectuée, l’utilisateur semblera étrange qu'inférieur altérée par les limites de l’angle d’ouverture, tout en ayant une expérience d’application à l’aise.</span><span class="sxs-lookup"><span data-stu-id="9810d-331">If done right, the user will feel less impaired by the FOV boundaries while having a comfortable app experience.</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-332">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-332">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-333"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-333"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-334"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-334"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-335">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-335">✔️</span></span></td>
        <td><span data-ttu-id="9810d-336">❌</span><span class="sxs-lookup"><span data-stu-id="9810d-336">❌</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-337">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-337">Quality criteria</span></span>

|  <span data-ttu-id="9810d-338">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-338">Best</span></span>  |  <span data-ttu-id="9810d-339">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-339">Meets</span></span> |  <span data-ttu-id="9810d-340">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-340">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="9810d-341">Utilisateur perd jamais le contexte et l’affichage est à l’aise.</span><span class="sxs-lookup"><span data-stu-id="9810d-341">User never loses context and viewing is comfortable.</span></span> <span data-ttu-id="9810d-342">L’assistance de contexte est fourni pour les objets volumineux.</span><span class="sxs-lookup"><span data-stu-id="9810d-342">Context assistance is provided for large objects.</span></span> <span data-ttu-id="9810d-343">Détectabilité et l’affichage des instructions est fournie pour les objets en dehors du cadre.</span><span class="sxs-lookup"><span data-stu-id="9810d-343">Discoverability and viewing guidance is provided for objects outside the frame.</span></span> <span data-ttu-id="9810d-344">En règle générale, conception de mouvement et de mise à l’échelle des hologrammes conviennent pour une expérience d’affichage à l’aise.</span><span class="sxs-lookup"><span data-stu-id="9810d-344">In general, motion design and scale of the holograms are appropriate for a comfortable viewing experience.</span></span> | <span data-ttu-id="9810d-345">Utilisateur perd jamais le contexte, mais le mouvement de cou supplémentaire peut être nécessaire dans des situations bien définies.</span><span class="sxs-lookup"><span data-stu-id="9810d-345">User never loses context, but extra neck motion may be required in limited situations.</span></span> <span data-ttu-id="9810d-346">Dans des situations bien définies à l’échelle provoque hologrammes arrêter l’exécution soit le frame vertical ou horizontal à l’origine de certains mouvements cou afficher les hologrammes.</span><span class="sxs-lookup"><span data-stu-id="9810d-346">In limited situations scale causes holograms to break either the vertical or horizontal frame causing some neck motion to view holograms.</span></span> | <span data-ttu-id="9810d-347">Utilisateur risque de perdre le contexte et/ou de mouvement de cou cohérent est requis pour afficher les hologrammes.</span><span class="sxs-lookup"><span data-stu-id="9810d-347">User likely to lose context and/or consistent neck motion is required to view holograms.</span></span> <span data-ttu-id="9810d-348">Aucune indication de contexte pour les objets volumineux HOLOGRAPHIQUE, déplacement d’objets facile de perdre en dehors du cadre sans les conseils de détectabilité, ni en hauteur hologrammes ne requiert cou régulière à afficher.</span><span class="sxs-lookup"><span data-stu-id="9810d-348">No context guidance for large holographic objects, moving objects easy to lose outside the frame with no discoverability guidance, or tall holograms requires regular neck motion to view.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="9810d-349">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-349">How to measure</span></span>

* <span data-ttu-id="9810d-350">Contexte pour un hologramme (grand) est perdu ou pas comprise en raison d’être détourée aux limites de le.</span><span class="sxs-lookup"><span data-stu-id="9810d-350">Context for a (large) hologram is lost or not understood due to being clipped at the boundaries.</span></span>
* <span data-ttu-id="9810d-351">Emplacement de hologrammes sont difficiles à détecter en raison du manque de directeurs d’attention ou du contenu qui déplace rapidement vers et depuis le frame HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="9810d-351">Location of holograms are hard to find due to the lack of attention directors or content that rapidly moves in and out of the holographic frame.</span></span>
* <span data-ttu-id="9810d-352">Scénario nécessite régulière et répétitives haut et bas de mouvement principal pour afficher entièrement un hologramme résultant de fatigue de col.</span><span class="sxs-lookup"><span data-stu-id="9810d-352">Scenario requires regular and repetitive up and down head motion to fully see a hologram resulting in neck fatigue.</span></span>

### <a name="recommendations"></a><span data-ttu-id="9810d-353">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-353">Recommendations</span></span>

* <span data-ttu-id="9810d-354">Démarrez l’expérience avec les petits objets ajuster l’angle d’ouverture, puis effectuer la transition des aides visuelles aux versions plus grande.</span><span class="sxs-lookup"><span data-stu-id="9810d-354">Start the experience with small objects that fit the FOV, then transition with visual cues to larger versions.</span></span>
* <span data-ttu-id="9810d-355">Utilisez spatiales directeurs audio et d’attention pour la recherche de contenu utilisateur qui est en dehors de l’angle d’ouverture.</span><span class="sxs-lookup"><span data-stu-id="9810d-355">Use spatial audio and attention directors to help the user find content that is outside the FOV.</span></span>
* <span data-ttu-id="9810d-356">Autant que possible, évitez hologrammes qui découper verticalement l’angle d’ouverture.</span><span class="sxs-lookup"><span data-stu-id="9810d-356">As much as possible, avoid holograms that vertically clip the FOV.</span></span>
* <span data-ttu-id="9810d-357">Fournir à l’utilisateur dans l’application des conseils pour optimiser l’affichage d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="9810d-357">Provide the user with in-app guidance for best viewing location.</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-358">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-358">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="9810d-359">Documentation</span><span class="sxs-lookup"><span data-stu-id="9810d-359">Documentation</span></span>

* [<span data-ttu-id="9810d-360">Image holographique</span><span class="sxs-lookup"><span data-stu-id="9810d-360">Holographic frame</span></span>](holographic-frame.md)
* [<span data-ttu-id="9810d-361">Étude de cas, HoloStudio UI et apprentissages de conception d’interaction</span><span class="sxs-lookup"><span data-stu-id="9810d-361">Case Study, HoloStudio UI and interaction design learnings</span></span>](case-study-3-holostudio-ui-and-interaction-design-learnings.md?#problem-2-modal-dialogs-are-sometimes-out-of-the-holographic-frame)
* [<span data-ttu-id="9810d-362">Mise à l’échelle des objets et des environnements</span><span class="sxs-lookup"><span data-stu-id="9810d-362">Scale of objects and environments</span></span>](scale.md)
* [<span data-ttu-id="9810d-363">Curseurs, les signaux visuels</span><span class="sxs-lookup"><span data-stu-id="9810d-363">Cursors, Visual cues</span></span>](cursors.md#visual-cues)

#### <a name="external-references"></a><span data-ttu-id="9810d-364">Références externes</span><span class="sxs-lookup"><span data-stu-id="9810d-364">External references</span></span>

* [<span data-ttu-id="9810d-365">Fait beaucoup de bruit sur l’angle d’ouverture</span><span class="sxs-lookup"><span data-stu-id="9810d-365">Much ado about the FOV</span></span>](https://www.linkedin.com/pulse/hololens-much-ado-field-of-view-michael-hoffman?lipi=urn%3Ali%3Apage%3Ad_flagship3_feed%3B6iQ%2FbTevLDU93w3I2ewLJw%3D%3D)

## <a name="content-reacts-to-user-position"></a><span data-ttu-id="9810d-366">Contenu réagit à la position de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="9810d-366">Content reacts to user position</span></span>

<span data-ttu-id="9810d-367">Hologrammes doivent réagir à la position de l’utilisateur dans à peu près la même façon que les objets de « vraies ».</span><span class="sxs-lookup"><span data-stu-id="9810d-367">Holograms should react to the user position in roughly the same ways that "real" objects do.</span></span> <span data-ttu-id="9810d-368">Une considération de conception importants est éléments d’interface utilisateur qui ne peut pas supposer nécessairement la position de l’utilisateur est à l’arrêt et s’adapter aux mouvements de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-368">A notable design consideration is UI elements that can't necessarily assume a user's position is stationary and adapt to the user's motion.</span></span> <span data-ttu-id="9810d-369">Conception d’une application qui s’adapte correctement à la position de l’utilisateur pour créer une expérience plus crédible et rendre plus facile à utiliser.</span><span class="sxs-lookup"><span data-stu-id="9810d-369">Designing an app that correctly adapts to user position will create a more believable experience and make it easier to use.</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-370">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-370">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-371"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-371"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-372"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-372"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-373">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-373">✔️</span></span></td>
        <td><span data-ttu-id="9810d-374">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-374">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-375">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-375">Quality criteria</span></span>

<table>
<tr>
<td> <span data-ttu-id="9810d-376">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-376">Best</span></span> </td><td> <span data-ttu-id="9810d-377">Contenu et l’interface utilisateur de s’adapter aux positions d’utilisateur qui permet à utilisateur d’interagir naturellement avec le contenu dans l’étendue du mouvement de l’utilisateur attendu.</span><span class="sxs-lookup"><span data-stu-id="9810d-377">Content and UI adapt to user positions allowing user to naturally interact with content within the scope of expected user movement.</span></span></td>
</tr><tr>
<td> <span data-ttu-id="9810d-378">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-378">Meets</span></span> </td><td> <span data-ttu-id="9810d-379">L’interface utilisateur s’adapte à la position de l’utilisateur, mais susceptible de compromettre l’affichage de contenu de clé nécessitant l’utilisateur d’ajuster leur position.</span><span class="sxs-lookup"><span data-stu-id="9810d-379">UI adapts to the user position, but may impede the view of key content requiring the user to adjust their position.</span></span></td>
</tr><tr>
<td> <span data-ttu-id="9810d-380">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-380">Fail</span></span> </td><td><ol>
<li><span data-ttu-id="9810d-381">Éléments d’interface utilisateur sont perdus ou verrouillés au cours de l’utilisateur entraînant le déplacement des queues revenir à (ou rechercher) des contrôles.</span><span class="sxs-lookup"><span data-stu-id="9810d-381">UI elements are lost or locked during movement causing user to unnaturally return to (or find) controls.</span></span></li><li><span data-ttu-id="9810d-382">Éléments d’interface utilisateur restreindre l’affichage du contenu principal.</span><span class="sxs-lookup"><span data-stu-id="9810d-382">UI elements limit the view of primary content.</span></span></li><li><span data-ttu-id="9810d-383">Déplacement de l’interface utilisateur n’est pas optimisé pour la distance d’affichage et l’inertie en particulier avec <a href="billboarding-and-tag-along.md">tag-along</a> éléments d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-383">UI movement is not optimized for viewing distance and momentum particularly with <a href="billboarding-and-tag-along.md">tag-along</a> UI elements.</span></span></li>
</ol></td>
</tr>
</table>

### <a name="how-to-measure"></a><span data-ttu-id="9810d-384">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-384">How to measure</span></span>

* <span data-ttu-id="9810d-385">Toutes les mesures doivent être effectuées dans une étendue raisonnable du scénario.</span><span class="sxs-lookup"><span data-stu-id="9810d-385">All measurements should be done within a reasonable scope of the scenario.</span></span> <span data-ttu-id="9810d-386">Tandis que le déplacement de l’utilisateur peut varier, n’essayez pas de tromper l’application avec le déplacement des utilisateur extrêmes.</span><span class="sxs-lookup"><span data-stu-id="9810d-386">While user movement will vary, don’t try to trick the app with extreme user movement.</span></span>
* <span data-ttu-id="9810d-387">Pour les éléments d’interface utilisateur, les contrôles appropriés doivent être disponibles quel que soit le mouvement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-387">For UI elements, relevant controls should be available regardless of user movement.</span></span> <span data-ttu-id="9810d-388">Par exemple, si l’utilisateur est Affichez et vous épargne une carte 3D avec zoom, le contrôle de zoom doit être prête à l’utilisateur, quel que soit l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="9810d-388">For example, if the user is viewing and walking around a 3D map with zoom, the zoom control should be readily available to the user regardless of location.</span></span>

### <a name="recommendations"></a><span data-ttu-id="9810d-389">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-389">Recommendations</span></span>

* <span data-ttu-id="9810d-390">L’utilisateur est l’appareil photo et qu’ils contrôlent le déplacement.</span><span class="sxs-lookup"><span data-stu-id="9810d-390">The user is the camera and they control the movement.</span></span> <span data-ttu-id="9810d-391">Let leur lecteur.</span><span class="sxs-lookup"><span data-stu-id="9810d-391">Let them drive.</span></span>
* <span data-ttu-id="9810d-392">Prendre en compte le billboarding pour le texte et pour vous déplacer dans les systèmes de rentrer qui seraient sinon être world-verrouillé ou masquées si un utilisateur étaient.</span><span class="sxs-lookup"><span data-stu-id="9810d-392">Consider billboarding for text and menuing systems that would otherwise be world-locked or obscured if a user were to move around.</span></span>
* <span data-ttu-id="9810d-393">Utiliser tag-along pour le contenu qui doit suivre l’utilisateur tout en permettant à l’utilisateur de voir ce qui est placé devant.</span><span class="sxs-lookup"><span data-stu-id="9810d-393">Use tag-along for content that needs to follow the user while still allowing the user to see what is in front of them.</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-394">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-394">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="9810d-395">Documentation</span><span class="sxs-lookup"><span data-stu-id="9810d-395">Documentation</span></span>

* [<span data-ttu-id="9810d-396">Conception de l’interaction</span><span class="sxs-lookup"><span data-stu-id="9810d-396">Interaction design</span></span>](hologram.md)
* [<span data-ttu-id="9810d-397">Couleur, clair et matériel</span><span class="sxs-lookup"><span data-stu-id="9810d-397">Color, light, and material</span></span>](color,-light-and-materials.md)
* [<span data-ttu-id="9810d-398">Billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="9810d-398">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
* [<span data-ttu-id="9810d-399">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="9810d-399">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="9810d-400">Automatique de mouvement et locomotion de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="9810d-400">Self-motion and user locomotion</span></span>](comfort.md#self-motion-and-user-locomotion)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="9810d-401">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="9810d-401">Tools and tutorials</span></span>

* [<span data-ttu-id="9810d-402">Réalité mixte - Entrées - Cours 210 : Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="9810d-402">MR Input 210: Gaze</span></span>](holograms-210.md)

## <a name="input-interaction-clarity"></a><span data-ttu-id="9810d-403">Clarté de l’interaction d’entrée</span><span class="sxs-lookup"><span data-stu-id="9810d-403">Input interaction clarity</span></span>

<span data-ttu-id="9810d-404">Clarté de l’interaction d’entrée est essentielle à la facilité d’utilisation d’une application et inclut la cohérence d’entrée, de commodité, de détectabilité des méthodes d’interaction.</span><span class="sxs-lookup"><span data-stu-id="9810d-404">Input interaction clarity is critical to an app's usability and includes input consistency, approachability, discoverability of interaction methods.</span></span> <span data-ttu-id="9810d-405">Utilisateur doit être en mesure d’utiliser des interactions courantes à l’échelle de la plateforme sans efforts d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="9810d-405">User should be able to use platform-wide common interactions without relearning.</span></span> <span data-ttu-id="9810d-406">Si l’application a entrée personnalisée, il doit être clairement communiqué et démontré.</span><span class="sxs-lookup"><span data-stu-id="9810d-406">If the app has custom input, it should be clearly communicated and demonstrated.</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-407">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-407">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-408"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-408"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-409"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-409"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-410">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-410">✔️</span></span></td>
        <td><span data-ttu-id="9810d-411">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-411">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-412">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-412">Quality criteria</span></span>

|  <span data-ttu-id="9810d-413">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-413">Best</span></span>  |  <span data-ttu-id="9810d-414">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-414">Meets</span></span> |  <span data-ttu-id="9810d-415">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-415">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="9810d-416">Méthodes d’interaction d’entrée sont cohérents avec la réalité mixte Windows fourni [conseils](interaction-fundamentals.md).</span><span class="sxs-lookup"><span data-stu-id="9810d-416">Input interaction methods are consistent with Windows Mixed Reality provided [guidance](interaction-fundamentals.md).</span></span> <span data-ttu-id="9810d-417">Toute entrée personnalisée ne doit pas être redondante avec l’entrée standard (plutôt utiliser l’interaction standard) et doit être clairement communiquée et démontrée à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-417">Any custom input should not be redundant with standard input (rather use standard interaction) and must be clearly communicated and demonstrated to the user.</span></span> | <span data-ttu-id="9810d-418">Similaire aux entrées meilleures, mais personnalisées sont redondantes avec les méthodes d’entrée standards.</span><span class="sxs-lookup"><span data-stu-id="9810d-418">Similar to best, but custom inputs are redundant with standard input methods.</span></span> <span data-ttu-id="9810d-419">Utilisateur peut toujours atteindre l’objectif et la progression via l’expérience de l’application.</span><span class="sxs-lookup"><span data-stu-id="9810d-419">User can still achieve the goal and progress through the app experience.</span></span> | <span data-ttu-id="9810d-420">Il est difficile de comprendre le mappage de bouton ou de la méthode d’entrée.</span><span class="sxs-lookup"><span data-stu-id="9810d-420">Difficult to understand input method or button mapping.</span></span> <span data-ttu-id="9810d-421">Entrée est fortement personnalisée, ne prend pas en charge l’entrée standard, aucune instruction, ou susceptibles de provoquer des problèmes de fatigue et de confort.</span><span class="sxs-lookup"><span data-stu-id="9810d-421">Input is heavily customized, does not support standard input, no instructions, or likely to cause fatigue and comfort issues.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="9810d-422">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-422">How to measure</span></span>

* <span data-ttu-id="9810d-423">L’application utilise cohérente [standard d’entrée des méthodes.](interaction-fundamentals.md)</span><span class="sxs-lookup"><span data-stu-id="9810d-423">The app uses consistent [standard input methods.](interaction-fundamentals.md)</span></span>
* <span data-ttu-id="9810d-424">Si l’application a d’entrée personnalisés, il est clairement communiqué via :</span><span class="sxs-lookup"><span data-stu-id="9810d-424">If the app has custome input, it is clearly communicated through:</span></span>
* <span data-ttu-id="9810d-425">Expérience de première exécution</span><span class="sxs-lookup"><span data-stu-id="9810d-425">First-run experience</span></span>
* <span data-ttu-id="9810d-426">Écrans d’introduction</span><span class="sxs-lookup"><span data-stu-id="9810d-426">Introductory screens</span></span>
* <span data-ttu-id="9810d-427">Info-bulles</span><span class="sxs-lookup"><span data-stu-id="9810d-427">Tooltips</span></span>
* <span data-ttu-id="9810d-428">Coach de main</span><span class="sxs-lookup"><span data-stu-id="9810d-428">Hand coach</span></span>
* <span data-ttu-id="9810d-429">Section aide</span><span class="sxs-lookup"><span data-stu-id="9810d-429">Help section</span></span>
* <span data-ttu-id="9810d-430">VoiceOver</span><span class="sxs-lookup"><span data-stu-id="9810d-430">Voice over</span></span>

### <a name="recommendations"></a><span data-ttu-id="9810d-431">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-431">Recommendations</span></span>

* <span data-ttu-id="9810d-432">Utilisez les méthodes d’entrée standards chaque fois que possible.</span><span class="sxs-lookup"><span data-stu-id="9810d-432">Use standard input methods whenever possible.</span></span>
* <span data-ttu-id="9810d-433">Fournir des démonstrations, des didacticiels et des info-bulles pour les méthodes d’entrée non standards.</span><span class="sxs-lookup"><span data-stu-id="9810d-433">Provide demonstrations, tutorials, and tooltips for non-standard input methods.</span></span>
* <span data-ttu-id="9810d-434">Utiliser un modèle d’interaction cohérente dans toute l’application.</span><span class="sxs-lookup"><span data-stu-id="9810d-434">Use a consistent interaction model throughout the app.</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-435">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-435">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="9810d-436">Documentation</span><span class="sxs-lookup"><span data-stu-id="9810d-436">Documentation</span></span>

* [<span data-ttu-id="9810d-437">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="9810d-437">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="9810d-438">Objets sur</span><span class="sxs-lookup"><span data-stu-id="9810d-438">Interactable objects</span></span>](interactable-object.md)
* [<span data-ttu-id="9810d-439">Suivre de la tête et stabiliser</span><span class="sxs-lookup"><span data-stu-id="9810d-439">Head-gaze and dwell</span></span>](gaze-and-dwell.md)
* [<span data-ttu-id="9810d-440">Curseurs</span><span class="sxs-lookup"><span data-stu-id="9810d-440">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="9810d-441">Confort et regards</span><span class="sxs-lookup"><span data-stu-id="9810d-441">Comfort and gaze</span></span>](comfort.md#gaze-direction)
* [<span data-ttu-id="9810d-442">Mouvements</span><span class="sxs-lookup"><span data-stu-id="9810d-442">Gestures</span></span>](gestures.md)
* [<span data-ttu-id="9810d-443">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="9810d-443">Voice input</span></span>](voice-input.md)
* [<span data-ttu-id="9810d-444">Commander avec la voix</span><span class="sxs-lookup"><span data-stu-id="9810d-444">Voice commanding</span></span>](voice-design.md)
* [<span data-ttu-id="9810d-445">Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="9810d-445">Motion controllers</span></span>](motion-controllers.md)
* [<span data-ttu-id="9810d-446">Guide de portage des entrées pour Unity</span><span class="sxs-lookup"><span data-stu-id="9810d-446">Input porting guide for Unity</span></span>](input-porting-guide-for-unity.md)
* [<span data-ttu-id="9810d-447">Saisie au clavier dans Unity</span><span class="sxs-lookup"><span data-stu-id="9810d-447">Keyboard input in Unity</span></span>](keyboard-input-in-unity.md)
* [<span data-ttu-id="9810d-448">Pointage du regard dans Unity</span><span class="sxs-lookup"><span data-stu-id="9810d-448">Gaze in Unity</span></span>](gaze-in-unity.md)
* [<span data-ttu-id="9810d-449">Mouvements et contrôleurs de mouvement dans Unity</span><span class="sxs-lookup"><span data-stu-id="9810d-449">Gestures and motion controllers in Unity</span></span>](gestures-and-motion-controllers-in-unity.md)
* [<span data-ttu-id="9810d-450">Entrée vocale dans Unity</span><span class="sxs-lookup"><span data-stu-id="9810d-450">Voice input in Unity</span></span>](voice-input-in-unity.md)
* [<span data-ttu-id="9810d-451">Saisie à l’aide de la commande de jeu, du clavier et de la souris dans DirectX</span><span class="sxs-lookup"><span data-stu-id="9810d-451">Keyboard, mouse, and controller input in DirectX</span></span>](keyboard,-mouse,-and-controller-input-in-directx.md)
* [<span data-ttu-id="9810d-452">Suivre de la tête et du regard dans DirectX</span><span class="sxs-lookup"><span data-stu-id="9810d-452">Head and eye gaze in DirectX</span></span>](gaze-in-directx.md)
* [<span data-ttu-id="9810d-453">Mains et contrôleurs de mouvement dans DirectX</span><span class="sxs-lookup"><span data-stu-id="9810d-453">Hands and motion controllers in DirectX</span></span>](hands-and-motion-controllers-in-directx.md)
* [<span data-ttu-id="9810d-454">Entrée vocale dans DirectX</span><span class="sxs-lookup"><span data-stu-id="9810d-454">Voice input in DirectX</span></span>](voice-input-in-directx.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="9810d-455">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="9810d-455">Tools and tutorials</span></span>

* [<span data-ttu-id="9810d-456">Étude de cas : La poursuite de l’informatique plus personnelle</span><span class="sxs-lookup"><span data-stu-id="9810d-456">Case study: The pursuit of more personal computing</span></span>](case-study-the-pursuit-of-more-personal-computing.md#less-interface-in-your-face)
* [<span data-ttu-id="9810d-457">Étude de cast : HoloStudio UI et apprentissages de conception d’interaction</span><span class="sxs-lookup"><span data-stu-id="9810d-457">Cast study: HoloStudio UI and interaction design learnings</span></span>](case-study-3-holostudio-ui-and-interaction-design-learnings.md)
* [<span data-ttu-id="9810d-458">Exemple d’application : Tableau périodique des éléments</span><span class="sxs-lookup"><span data-stu-id="9810d-458">Sample app: Periodic table of the elements</span></span>](periodic-table-of-the-elements.md)
* [<span data-ttu-id="9810d-459">Exemple d’application : Module de lunaire</span><span class="sxs-lookup"><span data-stu-id="9810d-459">Sample app: Lunar module</span></span>](lunar-module.md)
* [<span data-ttu-id="9810d-460">Réalité mixte - Entrées - Cours 210 : Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="9810d-460">MR Input 210: Gaze</span></span>](holograms-210.md)
* [<span data-ttu-id="9810d-461">Réalité mixte - Entrées - Cours 211 : Mouvements</span><span class="sxs-lookup"><span data-stu-id="9810d-461">MR Input 211: Gestures</span></span>](holograms-211.md)
* [<span data-ttu-id="9810d-462">Réalité mixte - Entrées - Cours 212 : Voix</span><span class="sxs-lookup"><span data-stu-id="9810d-462">MR Input 212: Voice</span></span>](holograms-212.md)

## <a name="interactable-objects"></a><span data-ttu-id="9810d-463">Objets sur</span><span class="sxs-lookup"><span data-stu-id="9810d-463">Interactable objects</span></span>

<span data-ttu-id="9810d-464">Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait 2D.</span><span class="sxs-lookup"><span data-stu-id="9810d-464">A button has long been a metaphor used for triggering an event in the 2D abstract world.</span></span> <span data-ttu-id="9810d-465">Dans le monde en trois dimensions de réalité mixte, nous n’êtes pas obligé d’être limitées à ce monde d’abstraction plus.</span><span class="sxs-lookup"><span data-stu-id="9810d-465">In the three-dimensional mixed reality world, we don’t have to be confined to this world of abstraction anymore.</span></span> <span data-ttu-id="9810d-466">Quoi que ce soit peut être un objet sur qui déclenche un événement.</span><span class="sxs-lookup"><span data-stu-id="9810d-466">Anything can be an Interactable object that triggers an event.</span></span> <span data-ttu-id="9810d-467">Un objet sur peut être représenté en tant que quoi que ce soit à partir d’une tasse de café sur la table à une info-bulle flottante en l’air.</span><span class="sxs-lookup"><span data-stu-id="9810d-467">An interactable object can be represented as anything from a coffee cup on the table to a balloon floating in the air.</span></span> <span data-ttu-id="9810d-468">Quel que soit le formulaire, les objets sur doivent être clairement reconnaissables par l’utilisateur via des signaux visuels et audio.</span><span class="sxs-lookup"><span data-stu-id="9810d-468">Regardless of the form, interactable objects should be clearly recognizable by the user through visual and audio cues.</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-469">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-469">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-470"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-470"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-471"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-471"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-472">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-472">✔️</span></span></td>
        <td><span data-ttu-id="9810d-473">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-473">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-474">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-474">Quality criteria</span></span>

|  <span data-ttu-id="9810d-475">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-475">Best</span></span>  |  <span data-ttu-id="9810d-476">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-476">Meets</span></span> |  <span data-ttu-id="9810d-477">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-477">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="9810d-478">Quel que soit le formulaire, des objets sur sont reconnaissables par le biais des signaux visuels et audio sur trois états : inactif, ciblées et sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9810d-478">Regardless of form, interactable objects are recognizable through visual and audio cues across three states: idle, targeted, and selected.</span></span> <span data-ttu-id="9810d-479">« Consultez, dites » effacer et de manière cohérente sert tout au long de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="9810d-479">"See it, say it" is clear and consistently used throughout the experience.</span></span> <span data-ttu-id="9810d-480">Les objets sont mis à l’échelle et distribués pour autoriser l’erreur gratuit de ciblage.</span><span class="sxs-lookup"><span data-stu-id="9810d-480">Objects are scaled and distributed to allow for error free targeting.</span></span> | <span data-ttu-id="9810d-481">Utilisateur peut reconnaître l’objet en tant que sur via des commentaires audio et visuels et cibler et activer l’objet.</span><span class="sxs-lookup"><span data-stu-id="9810d-481">User can recognize object as interactable through audio or visual feedback, and can target and activate the object.</span></span> | <span data-ttu-id="9810d-482">Étant donné aucun signaux visual ou audio, utilisateur ne peut pas reconnaître un objet sur.</span><span class="sxs-lookup"><span data-stu-id="9810d-482">Given no visual or audio cues, user cannot recognize an interactable object.</span></span> <span data-ttu-id="9810d-483">Interactions sont sujettes en raison de l’échelle de l’objet ou la distance entre les objets.</span><span class="sxs-lookup"><span data-stu-id="9810d-483">Interactions are error prone due to object scale or distance between objects.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="9810d-484">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-484">How to measure</span></span>

* <span data-ttu-id="9810d-485">Objets sur sont reconnus comme 'sur' ; y compris les boutons, menus et application de contenu spécifique.</span><span class="sxs-lookup"><span data-stu-id="9810d-485">Interactable objects are recognizable as 'interactable'; including buttons, menus, and app specific content.</span></span> <span data-ttu-id="9810d-486">En règle générale il doit être un indice visuel et audio lors du ciblage des objets sur.</span><span class="sxs-lookup"><span data-stu-id="9810d-486">As a rule of thumb there should be a visual and audio cue when targeting interactable objects.</span></span>

### <a name="recommendations"></a><span data-ttu-id="9810d-487">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-487">Recommendations</span></span>

* <span data-ttu-id="9810d-488">Utiliser des commentaires visuels et audio pour les interactions.</span><span class="sxs-lookup"><span data-stu-id="9810d-488">Use visual and audio feedback for interactions.</span></span>
* <span data-ttu-id="9810d-489">Des commentaires visuels doivent être différenciées pour chaque d’entrée d’état (inactif, ciblé, sélectionné)</span><span class="sxs-lookup"><span data-stu-id="9810d-489">Visual feedback should be differentiated for each input state (idle, targeted, selected)</span></span>
* <span data-ttu-id="9810d-490">Objets sur doivent être mis à l’échelle et placés par erreur gratuit de ciblage.</span><span class="sxs-lookup"><span data-stu-id="9810d-490">Interactable objects should be scaled and placed for error free targeting.</span></span>
* <span data-ttu-id="9810d-491">Les objets groupés sur (par exemple, une barre de menus ou de la liste) doivent avoir espacement approprié pour le ciblage.</span><span class="sxs-lookup"><span data-stu-id="9810d-491">Grouped interactable objects (such as a menu bar or list) should have proper spacing for targeting.</span></span>
* <span data-ttu-id="9810d-492">Boutons et des menus qui prennent en charge de la commande vocale doivent fournir des étiquettes de texte pour le mot clé de commande (« voir, dites-le »)</span><span class="sxs-lookup"><span data-stu-id="9810d-492">Buttons and menus that support voice command should provide text labels for the command keyword ("See it, say it")</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-493">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-493">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="9810d-494">Documentation</span><span class="sxs-lookup"><span data-stu-id="9810d-494">Documentation</span></span>

* [<span data-ttu-id="9810d-495">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="9810d-495">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="9810d-496">Texte dans Unity</span><span class="sxs-lookup"><span data-stu-id="9810d-496">Text in Unity</span></span>](text-in-unity.md)
* [<span data-ttu-id="9810d-497">Rectangle englobant et barre de l’application</span><span class="sxs-lookup"><span data-stu-id="9810d-497">Bounding box and App bar</span></span>](app-bar-and-bounding-box.md)
* [<span data-ttu-id="9810d-498">Commander avec la voix</span><span class="sxs-lookup"><span data-stu-id="9810d-498">Voice commanding</span></span>](voice-design.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="9810d-499">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="9810d-499">Tools and tutorials</span></span>

* [<span data-ttu-id="9810d-500">Réalité mixte Toolkit - UX</span><span class="sxs-lookup"><span data-stu-id="9810d-500">Mixed Reality Toolkit - UX</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/UX)

## <a name="room-scanning"></a><span data-ttu-id="9810d-501">Espace d’analyse</span><span class="sxs-lookup"><span data-stu-id="9810d-501">Room scanning</span></span>

<span data-ttu-id="9810d-502">Les applications qui requièrent des données de mappage spatial s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions en tant que l’utilisateur explore leur environnement avec l’appareil actif.</span><span class="sxs-lookup"><span data-stu-id="9810d-502">Apps that require spatial mapping data rely on the device to automatically collect this data over time and across sessions as the user explores their environment with the device active.</span></span> <span data-ttu-id="9810d-503">Le souci d’exhaustivité et la qualité de ces données dépend de plusieurs facteurs, notamment la quantité d’exploration de l’utilisateur a effectué, combien de temps écoulé depuis l’exploration et indique si les objets tels que des portes et meubles ont déplacés depuis le périphérique analyse la zone.</span><span class="sxs-lookup"><span data-stu-id="9810d-503">The completeness and quality of this data depends on a number of factors including the amount of exploration the user has done, how much time has passed since the exploration and whether objects such as furniture and doors have moved since the device scanned the area.</span></span> <span data-ttu-id="9810d-504">De nombreuses applications analysera les données de mappage spatial au début de l’expérience pour déterminer si l’utilisateur doit effectuer des étapes supplémentaires pour améliorer l’exhaustivité et la qualité de la carte spatiale à.</span><span class="sxs-lookup"><span data-stu-id="9810d-504">Many apps will analyze the spatial mapping data at the start of the experience to judge whether the user should perform additional steps to improve the completeness and quality of the spatial map.</span></span> <span data-ttu-id="9810d-505">Si l’utilisateur est requis pour l’analyse de l’environnement, effacer des conseils doivent être fournis lors de l’expérience d’analyse.</span><span class="sxs-lookup"><span data-stu-id="9810d-505">If the user is required to scan the environment, clear guidance should be provided during the scanning experience.</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-506">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-506">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-507"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-507"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-508"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-508"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-509">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-509">✔️</span></span></td>
        <td><span data-ttu-id="9810d-510">❌</span><span class="sxs-lookup"><span data-stu-id="9810d-510">❌</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-511">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-511">Quality criteria</span></span>

|  <span data-ttu-id="9810d-512">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-512">Best</span></span>  |  <span data-ttu-id="9810d-513">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-513">Meets</span></span> |  <span data-ttu-id="9810d-514">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-514">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="9810d-515">Visualisation de la maille spatiale indiquent aux utilisateurs de l’analyse sont en cours.</span><span class="sxs-lookup"><span data-stu-id="9810d-515">Visualization of the spatial mesh tell users scanning is in progress.</span></span> <span data-ttu-id="9810d-516">Utilisateur clairement sait quoi faire lorsque l’analyse démarre et s’arrête.</span><span class="sxs-lookup"><span data-stu-id="9810d-516">User clearly knows what to do and when the scan starts and stops.</span></span> | <span data-ttu-id="9810d-517">Visualisation de la maille spatiale est fournie, mais l’utilisateur ne peut pas clairement savoir comment procéder et aucune information de progression est fournie.</span><span class="sxs-lookup"><span data-stu-id="9810d-517">Visualization of the spatial mesh is provided, but the user may not clearly know what to do and no progress information is provided.</span></span> | <span data-ttu-id="9810d-518">Aucune visualisation de la maille.</span><span class="sxs-lookup"><span data-stu-id="9810d-518">No visualization of mesh.</span></span> <span data-ttu-id="9810d-519">Aucune information de conseils fournie à l’utilisateur concernant où rechercher, ou lorsque l’analyse démarre/arrête.</span><span class="sxs-lookup"><span data-stu-id="9810d-519">No guidance information provided to the user regarding where to look, or when the scan starts/stops.</span></span> |

### <a name="how-to-measure"></a><span data-ttu-id="9810d-520">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-520">How to measure</span></span>

* <span data-ttu-id="9810d-521">Lors d’une analyse de l’espace requis, des conseils visuels et audio sont fourni qui indique où rechercher et quand commencer et l’arrêter l’analyse.</span><span class="sxs-lookup"><span data-stu-id="9810d-521">During a required room scan, visual and audio guidance is provided indicating where to look, and when to start and stop scanning.</span></span>

### <a name="recommendations"></a><span data-ttu-id="9810d-522">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-522">Recommendations</span></span>

* <span data-ttu-id="9810d-523">Indique la quantité du volume total à proximité des utilisateurs doit faire partie de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="9810d-523">Indicate how much of the total volume in the users vicinity needs to be part of the experience.</span></span>
* <span data-ttu-id="9810d-524">Communiquer lors de l’analyse démarre et s’arrête comme un indicateur de progression.</span><span class="sxs-lookup"><span data-stu-id="9810d-524">Communicate when the scan starts and stops such as a progress indicator.</span></span>
* <span data-ttu-id="9810d-525">Utiliser une visualisation de la maille lors de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="9810d-525">Use a visualization of the mesh during the scan.</span></span>
* <span data-ttu-id="9810d-526">Fournir des signaux visuels et audio pour inciter l’utilisateur à rechercher et vous déplacer dans la salle.</span><span class="sxs-lookup"><span data-stu-id="9810d-526">Provide visual and audio cues to encourage the user to look and move around the room.</span></span>
* <span data-ttu-id="9810d-527">Informer l’utilisateur où aller pour améliorer les données.</span><span class="sxs-lookup"><span data-stu-id="9810d-527">Inform the user where to go to improve the data.</span></span> <span data-ttu-id="9810d-528">Dans de nombreux cas, il peut être préférable d’indiquer à l’utilisateur de ce qu’ils doivent (par exemple, examinez le plafond, recherchez derrière meubles), afin d’obtenir la qualité d’analyse nécessaires.</span><span class="sxs-lookup"><span data-stu-id="9810d-528">In many cases, it may be best to tell the user what they need to do (e.g. look at the ceiling, look behind furniture), in order to get the necessary scan quality.</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-529">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-529">Resources</span></span>

#### <a name="documentation"></a><span data-ttu-id="9810d-530">Documentation</span><span class="sxs-lookup"><span data-stu-id="9810d-530">Documentation</span></span>

* [<span data-ttu-id="9810d-531">Visualisation du balayage d’une pièce</span><span class="sxs-lookup"><span data-stu-id="9810d-531">Room scan visualization</span></span>](room-scan-visualization.md)
* [<span data-ttu-id="9810d-532">Étude de cas : Développer les capacités de mappage spatial d’HoloLens</span><span class="sxs-lookup"><span data-stu-id="9810d-532">Case study: Expanding the spatial mapping capabilities of HoloLens</span></span>](case-study-expanding-the-spatial-mapping-capabilities-of-hololens.md)
* [<span data-ttu-id="9810d-533">Étude de cas : Spatiale sonorisation pour HoloTour</span><span class="sxs-lookup"><span data-stu-id="9810d-533">Case study: Spatial sound design for HoloTour</span></span>](case-study-spatial-sound-design-for-holotour.md)
* [<span data-ttu-id="9810d-534">Étude de cas : Création d’une expérience d’immersion dans les Fragments</span><span class="sxs-lookup"><span data-stu-id="9810d-534">Case study: Creating an immersive experience in Fragments</span></span>](case-study-creating-an-immersive-experience-in-fragments.md)

#### <a name="tools-and-tutorials"></a><span data-ttu-id="9810d-535">Outils et didacticiels</span><span class="sxs-lookup"><span data-stu-id="9810d-535">Tools and tutorials</span></span>

* [<span data-ttu-id="9810d-536">Réalité mixte Toolkit - UX</span><span class="sxs-lookup"><span data-stu-id="9810d-536">Mixed Reality Toolkit - UX</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/UX)

## <a name="directional-indicators"></a><span data-ttu-id="9810d-537">Indicateurs directionnels</span><span class="sxs-lookup"><span data-stu-id="9810d-537">Directional indicators</span></span>

<span data-ttu-id="9810d-538">Dans une application de réalité mixte, le contenu peut être à l’extérieur du champ de vue ou bloqués par les objets du monde réel.</span><span class="sxs-lookup"><span data-stu-id="9810d-538">In a mixed reality app, content may be outside the field of view or occluded by real-world objects.</span></span> <span data-ttu-id="9810d-539">Une application bien conçue rend plus facile pour l’utilisateur rechercher du contenu non visibles.</span><span class="sxs-lookup"><span data-stu-id="9810d-539">A well designed app will make it easier for the user to find non-visible content.</span></span> <span data-ttu-id="9810d-540">Indicateurs directionnels alerter un utilisateur au contenu important et fournissent des conseils pour le contenu par rapport à la position de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-540">Directional indicators alert a user to important content and provide guidance to the content relative to the user's position.</span></span> <span data-ttu-id="9810d-541">Conseils pour le contenu non visible peuvent prendre la forme d’émetteurs audio, flèches de direction ou des signaux visuels directs.</span><span class="sxs-lookup"><span data-stu-id="9810d-541">Guidance to non-visible content can take the form of sound emitters, directional arrows, or direct visual cues.</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-542">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-542">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-543"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-543"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-544"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-544"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-545">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-545">✔️</span></span></td>
        <td><span data-ttu-id="9810d-546">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-546">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-547">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-547">Quality criteria</span></span>

|  <span data-ttu-id="9810d-548">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-548">Best</span></span>  |  <span data-ttu-id="9810d-549">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-549">Meets</span></span> |  <span data-ttu-id="9810d-550">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-550">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="9810d-551">Les signaux visuels et audio guident directement vers le contenu approprié à l’extérieur du champ de vue.</span><span class="sxs-lookup"><span data-stu-id="9810d-551">Visual and audio cues directly guide the user to relevant content outside the field of view.</span></span> | <span data-ttu-id="9810d-552">Une flèche ou un indicateur qui pointe vers l’utilisateur de la direction générale du contenu.</span><span class="sxs-lookup"><span data-stu-id="9810d-552">An arrow or some indicator that points the user in the general direction of the content.</span></span> | <span data-ttu-id="9810d-553">Le contenu approprié est en dehors du champ de vue et une mauvaise ou aucun guide de l’emplacement n’est fourni à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9810d-553">Relevant content is outside of the field of view, and poor or no location guidance is provided to the user.</span></span> | 

### <a name="how-to-measure"></a><span data-ttu-id="9810d-554">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-554">How to measure</span></span>

* <span data-ttu-id="9810d-555">Le contenu approprié en dehors de l’utilisateur champ de vision est détectable par le biais des signaux visual et/ou audio.</span><span class="sxs-lookup"><span data-stu-id="9810d-555">Relevant content outside of the user field of view is discoverable through visual and/or audio cues.</span></span>

### <a name="recommendations"></a><span data-ttu-id="9810d-556">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-556">Recommendations</span></span>

* <span data-ttu-id="9810d-557">Lorsque le contenu approprié est en dehors du champ de vision de l’utilisateur, utiliser des indicateurs directionnels et signaux audio pour guider l’utilisateur au contenu.</span><span class="sxs-lookup"><span data-stu-id="9810d-557">When relevant content is outside the user's field of view, use directional indicators and audio cues to guide the user to the content.</span></span> <span data-ttu-id="9810d-558">Dans de nombreux cas, un guide visuel direct est préféré sur les flèches de direction.</span><span class="sxs-lookup"><span data-stu-id="9810d-558">In many cases, a direct visual guide is preferred over directional arrows.</span></span>
* <span data-ttu-id="9810d-559">Les indicateurs de directionnelles ne doivent pas être créés dans le curseur.</span><span class="sxs-lookup"><span data-stu-id="9810d-559">Directional indicators should not be built into the cursor.</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-560">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-560">Resources</span></span>

* [<span data-ttu-id="9810d-561">Image holographique</span><span class="sxs-lookup"><span data-stu-id="9810d-561">Holographic frame</span></span>](holographic-frame.md)

## <a name="data-loading"></a><span data-ttu-id="9810d-562">Chargement des données</span><span class="sxs-lookup"><span data-stu-id="9810d-562">Data loading</span></span>

<span data-ttu-id="9810d-563">Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours.</span><span class="sxs-lookup"><span data-stu-id="9810d-563">A progress control provides feedback to the user that a long-running operation is underway.</span></span> <span data-ttu-id="9810d-564">Cela peut signifier que l’utilisateur ne peut pas interagir avec l’application lorsque l’indicateur de progression est visible et peut également indiquer la durée pendant laquelle le délai d’attente peut être.</span><span class="sxs-lookup"><span data-stu-id="9810d-564">It can mean that the user cannot interact with the app when the progress indicator is visible and can also indicate how long the wait time might be.</span></span>

### <a name="device-impact"></a><span data-ttu-id="9810d-565">Impact de l’appareil</span><span class="sxs-lookup"><span data-stu-id="9810d-565">Device impact</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="9810d-566"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-566"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="9810d-567"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="9810d-567"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
        <td></td>
    </tr>
     <tr>
        <td><span data-ttu-id="9810d-568">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-568">✔️</span></span></td>
        <td><span data-ttu-id="9810d-569">✔️</span><span class="sxs-lookup"><span data-stu-id="9810d-569">✔️</span></span></td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a><span data-ttu-id="9810d-570">Critères de qualité</span><span class="sxs-lookup"><span data-stu-id="9810d-570">Quality criteria</span></span>

|  <span data-ttu-id="9810d-571">Meilleur</span><span class="sxs-lookup"><span data-stu-id="9810d-571">Best</span></span>  |  <span data-ttu-id="9810d-572">Répond à</span><span class="sxs-lookup"><span data-stu-id="9810d-572">Meets</span></span> |  <span data-ttu-id="9810d-573">Échec</span><span class="sxs-lookup"><span data-stu-id="9810d-573">Fail</span></span> |
--- | --- | ---
|  <span data-ttu-id="9810d-574">Indicateur visuel animée, sous la forme d’une barre de progression ou un anneau, affichant la progression au cours de toutes les données du chargement ou de traitement.</span><span class="sxs-lookup"><span data-stu-id="9810d-574">Animated visual indicator, in the form of a progress bar or ring, showing progress during any data loading or processing.</span></span> <span data-ttu-id="9810d-575">L’indicateur visuel fournit des conseils sur la durée pendant laquelle l’attente pourrait être.</span><span class="sxs-lookup"><span data-stu-id="9810d-575">The visual indicator provides guidance on how long the wait could be.</span></span> | <span data-ttu-id="9810d-576">L’utilisateur est informé que le chargement des données est en cours d’exécution, mais il n’existe aucune indication de la durée pendant laquelle l’attente peut être.</span><span class="sxs-lookup"><span data-stu-id="9810d-576">User is informed that data loading is in progress, but there is no indication of how long the wait could be.</span></span> | <span data-ttu-id="9810d-577">Aucun lors du chargement de données ou les indicateurs de processus pour la tâche prend plus de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="9810d-577">No data loading or process indicators for task taking longer than 5 seconds.</span></span> |

### <a name="how-to-measure"></a><span data-ttu-id="9810d-578">Comment mesurer</span><span class="sxs-lookup"><span data-stu-id="9810d-578">How to measure</span></span>

* <span data-ttu-id="9810d-579">Pendant le chargement de données vérifier le que état n’est pas vide pendant plus de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="9810d-579">During data loading verify there is no blank state for more than 5 seconds.</span></span>

### <a name="recommendations"></a><span data-ttu-id="9810d-580">Recommandations</span><span class="sxs-lookup"><span data-stu-id="9810d-580">Recommendations</span></span>

* <span data-ttu-id="9810d-581">Fournir une d’animation de chargement de données affichant la progression dans n’importe quelle situation lorsque l’utilisateur peut-être percevoir cette application est bloqué ou est tombé en panne.</span><span class="sxs-lookup"><span data-stu-id="9810d-581">Provide a data loading animator showing progress in any situation when the user may perceive this app to have stalled or crashed.</span></span> <span data-ttu-id="9810d-582">Une règle empirique raisonnable est toute activité « chargement » qui peut prendre plus de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="9810d-582">A reasonable rule of thumb is any 'loading' activity that could take more than 5 seconds.</span></span>

### <a name="resources"></a><span data-ttu-id="9810d-583">Ressources</span><span class="sxs-lookup"><span data-stu-id="9810d-583">Resources</span></span>

* [<span data-ttu-id="9810d-584">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="9810d-584">Displaying progress</span></span>](progress.md)
