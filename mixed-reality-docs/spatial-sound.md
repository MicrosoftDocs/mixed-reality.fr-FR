---
title: Audio en réalité mixte
description: L’audio en réalité mixte peut augmenter la confiance des utilisateurs dans les interactions entre les interfaces utilisateur et plonger les utilisateurs dans l’expérience.
author: kegodin
ms.author: kegodin
ms.date: 11/07/2019
ms.topic: article
keywords: son spatial, son surround, audio 3D, son 3D, son spatial
ms.openlocfilehash: b939433daf80a95a11bc0e1ac2ffd75dfe0cf299
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75181979"
---
# <a name="audio-in-mixed-reality"></a><span data-ttu-id="2eead-104">Audio en réalité mixte</span><span class="sxs-lookup"><span data-stu-id="2eead-104">Audio in mixed reality</span></span>
<span data-ttu-id="2eead-105">L’audio est un élément essentiel de la conception et de la productivité dans la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="2eead-105">Audio is an essential part of design and productivity in mixed reality.</span></span> <span data-ttu-id="2eead-106">Le son peut :</span><span class="sxs-lookup"><span data-stu-id="2eead-106">Sound can:</span></span>
* <span data-ttu-id="2eead-107">Augmentez la confiance des utilisateurs dans les interactions entre les mouvements et les voix.</span><span class="sxs-lookup"><span data-stu-id="2eead-107">Increase user confidence in gesture and voice interactions.</span></span>
* <span data-ttu-id="2eead-108">Guidez les utilisateurs vers les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="2eead-108">Guide users to next steps.</span></span>
* <span data-ttu-id="2eead-109">Associez efficacement des objets virtuels au monde réel.</span><span class="sxs-lookup"><span data-stu-id="2eead-109">Effectively combine virtual objects with the real world.</span></span>

<span data-ttu-id="2eead-110">Le suivi de la tête à faible latence des casques de réalité mixte, y compris HoloLens, prend en charge les Spatialization de haute qualité HRTF.</span><span class="sxs-lookup"><span data-stu-id="2eead-110">The low-latency head tracking of mixed reality headsets, including HoloLens, supports high-quality HRTF-based spatialization.</span></span> <span data-ttu-id="2eead-111">Vous pouvez spatialiser l’audio dans votre application pour :</span><span class="sxs-lookup"><span data-stu-id="2eead-111">You can spatialize audio in your application to:</span></span>
* <span data-ttu-id="2eead-112">Attirez l’attention sur les éléments visuels.</span><span class="sxs-lookup"><span data-stu-id="2eead-112">Call attention to visual elements.</span></span>
* <span data-ttu-id="2eead-113">Aidez les utilisateurs à prendre conscience de leur environnement réel.</span><span class="sxs-lookup"><span data-stu-id="2eead-113">Help users maintain awareness of their real-world surroundings.</span></span>

<span data-ttu-id="2eead-114">Les acoustiques connectent plus profondément les hologrammes au monde en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="2eead-114">Acoustics more deeply connect holograms to the mixed-reality world.</span></span> <span data-ttu-id="2eead-115">Il fournit des indications sur l’environnement et l’état de l’objet.</span><span class="sxs-lookup"><span data-stu-id="2eead-115">It provides cues about the environment and object state.</span></span>

<span data-ttu-id="2eead-116">Consultez [des exemples détaillés de conception qui utilise l’audio](spatial-sound-design.md).</span><span class="sxs-lookup"><span data-stu-id="2eead-116">See detailed [examples of design that uses audio](spatial-sound-design.md).</span></span>

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/PTPvx7mDon4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## <a name="device-support"></a><span data-ttu-id="2eead-117">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="2eead-117">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="2eead-118"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="2eead-118"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="2eead-119"><a href="hololens-hardware-details.md"><strong>HoloLens (première génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="2eead-119"><a href="hololens-hardware-details.md"><strong>HoloLens (first gen)</strong></a></span></span></td>
        <td><span data-ttu-id="2eead-120"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="2eead-120"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="2eead-121"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="2eead-121"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="2eead-122">Spatialisation</span><span class="sxs-lookup"><span data-stu-id="2eead-122">Spatialization</span></span></td>
        <td><span data-ttu-id="2eead-123">✔️</span><span class="sxs-lookup"><span data-stu-id="2eead-123">✔️</span></span></td>
        <td><span data-ttu-id="2eead-124">✔️</span><span class="sxs-lookup"><span data-stu-id="2eead-124">✔️</span></span></td>
        <td><span data-ttu-id="2eead-125">✔️</span><span class="sxs-lookup"><span data-stu-id="2eead-125">✔️</span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="2eead-126">Accélération matérielle Spatialization</span><span class="sxs-lookup"><span data-stu-id="2eead-126">Spatialization hardware acceleration</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="2eead-127">✔️</span><span class="sxs-lookup"><span data-stu-id="2eead-127">✔️</span></span></td>
        <td>❌</td>
    </tr>
</table>

## <a name="use-of-sounds-in-mixed-reality"></a><span data-ttu-id="2eead-128">Utilisation de sons dans une réalité mixte</span><span class="sxs-lookup"><span data-stu-id="2eead-128">Use of sounds in mixed reality</span></span>
<span data-ttu-id="2eead-129">[L’utilisation de sons dans une réalité mixte](spatial-sound-design.md) requiert une approche différente de celle des applications tactiles et du clavier et de la souris.</span><span class="sxs-lookup"><span data-stu-id="2eead-129">[Use of sounds in mixed reality](spatial-sound-design.md) requires a different approach than in touch and keyboard-and-mouse applications.</span></span> <span data-ttu-id="2eead-130">Les décisions relatives à la conception de sons clés incluent les sons à spatialiser et les interactions à sonify.</span><span class="sxs-lookup"><span data-stu-id="2eead-130">Key sound design decisions include which sounds to spatialize and which interactions to sonify.</span></span> <span data-ttu-id="2eead-131">Ces décisions affectent fortement la confiance des utilisateurs, la productivité et la courbe d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="2eead-131">These decisions strongly effect user confidence, productivity, and learning curve.</span></span>

### <a name="case-studies"></a><span data-ttu-id="2eead-132">Études de cas</span><span class="sxs-lookup"><span data-stu-id="2eead-132">Case studies</span></span>
<span data-ttu-id="2eead-133">HoloTour prend pratiquement les utilisateurs sur des sites touristiques et historiques dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="2eead-133">HoloTour virtually takes users to tourist and historical sites around the world.</span></span> <span data-ttu-id="2eead-134">Consultez l’étude [de cas Sound Design for HoloTour](case-study-spatial-sound-design-for-holotour.md) .</span><span class="sxs-lookup"><span data-stu-id="2eead-134">See the [Sound design for HoloTour](case-study-spatial-sound-design-for-holotour.md) case study.</span></span> <span data-ttu-id="2eead-135">Un microphone spécial et une configuration de rendu ont été utilisés pour capturer les espaces de sujet.</span><span class="sxs-lookup"><span data-stu-id="2eead-135">A special microphone and rendering setup were used to capture the subject spaces.</span></span>

<span data-ttu-id="2eead-136">RoboRaid est un tir à haute énergie pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="2eead-136">RoboRaid is a high-energy shooter for HoloLens.</span></span> <span data-ttu-id="2eead-137">L’étude [de cas de conception audio pour RoboRaid](case-study-using-spatial-sound-in-roboraid.md) décrit les choix de conception qui ont été effectués pour garantir que l’audio spatial était utilisé à l’effet le plus spectaculaire.</span><span class="sxs-lookup"><span data-stu-id="2eead-137">The [Sound design for RoboRaid](case-study-using-spatial-sound-in-roboraid.md) case study describes the design choices that were made to ensure spatial audio was used to the fullest dramatic effect.</span></span>

## <a name="spatialization"></a><span data-ttu-id="2eead-138">Spatialisation</span><span class="sxs-lookup"><span data-stu-id="2eead-138">Spatialization</span></span>
<span data-ttu-id="2eead-139">Spatialization est le composant directionnel du son spatial.</span><span class="sxs-lookup"><span data-stu-id="2eead-139">Spatialization is the directional component of spatial audio.</span></span> <span data-ttu-id="2eead-140">Pour une configuration 7,1 Home cinéma, Spatialization est aussi simple que le panoramique entre les haut-parleurs.</span><span class="sxs-lookup"><span data-stu-id="2eead-140">For a 7.1 home theater setup, spatialization is as simple as panning between loudspeakers.</span></span> <span data-ttu-id="2eead-141">Mais pour le casque en réalité mixte, il est essentiel d’utiliser une technologie HRTF pour la précision et le confort.</span><span class="sxs-lookup"><span data-stu-id="2eead-141">But for headphones in mixed reality, it's essential to use an HRTF-based technology for accuracy and comfort.</span></span> <span data-ttu-id="2eead-142">Windows propose des Spatialization basés sur HRTF, et cette prise en charge est accélérée par le matériel sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="2eead-142">Windows offers HRTF-based spatialization, and this support is hardware-accelerated on HoloLens 2.</span></span>

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/aB3TDjYklmo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### <a name="should-i-spatialize"></a><span data-ttu-id="2eead-143">Dois-je spatialiser ?</span><span class="sxs-lookup"><span data-stu-id="2eead-143">Should I spatialize?</span></span>
<span data-ttu-id="2eead-144">Spatialization peut améliorer de nombreux sons dans des applications en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="2eead-144">Spatialization can improve many sounds in mixed-reality applications.</span></span> <span data-ttu-id="2eead-145">Spatialization utilise un son en dehors de la tête de l’écouteur et le place dans le monde.</span><span class="sxs-lookup"><span data-stu-id="2eead-145">Spatialization takes a sound out of the listener's head and places it in the world.</span></span> <span data-ttu-id="2eead-146">Pour obtenir des suggestions sur l’utilisation effective de Spatialization dans votre application, consultez [conception de son spatial](spatial-sound-design.md).</span><span class="sxs-lookup"><span data-stu-id="2eead-146">For suggestions on effective use of spatialization in your application, see [Spatial sound design](spatial-sound-design.md).</span></span>

### <a name="spatializer-personalization"></a><span data-ttu-id="2eead-147">Personnalisation de Spatializer</span><span class="sxs-lookup"><span data-stu-id="2eead-147">Spatializer personalization</span></span>
<span data-ttu-id="2eead-148">Les HRTFs manipulent les différences de niveau et de phase entre les oreilles à travers le spectre de fréquences.</span><span class="sxs-lookup"><span data-stu-id="2eead-148">HRTFs manipulate the level and phase differences between ears across the frequency spectrum.</span></span> <span data-ttu-id="2eead-149">Ils sont basés sur des modèles physiques et des mesures de la tête humaine, du tors et des formes d’oreille (pinnae).</span><span class="sxs-lookup"><span data-stu-id="2eead-149">They're based on physical models and measurements of human head, torso, and ear shapes (pinnae).</span></span> <span data-ttu-id="2eead-150">Notre cerveau répond à ces différences pour fournir un sens sonore.</span><span class="sxs-lookup"><span data-stu-id="2eead-150">Our brains respond to these differences to provide perceived direction in sound.</span></span>

<span data-ttu-id="2eead-151">Chaque individu a une forme auriculaire, une taille de tête et une position Ear uniques.</span><span class="sxs-lookup"><span data-stu-id="2eead-151">Every individual has a unique ear shape, head size, and ear position.</span></span> <span data-ttu-id="2eead-152">Le meilleur HRTFs est donc conforme à vos exigences.</span><span class="sxs-lookup"><span data-stu-id="2eead-152">So the best HRTFs conform to you.</span></span> <span data-ttu-id="2eead-153">Pour augmenter la précision de la Spatialization, HoloLens utilise votre distance inter-pupille (IPD) à partir du casque pour ajuster la HRTFs de la taille de la tête.</span><span class="sxs-lookup"><span data-stu-id="2eead-153">To increase spatialization accuracy, HoloLens uses your inter-pupilary distance (IPD) from the headset displays to adjust the HRTFs for your head size.</span></span>

### <a name="spatializer-platform-support"></a><span data-ttu-id="2eead-154">Prise en charge de la plateforme Spatializer</span><span class="sxs-lookup"><span data-stu-id="2eead-154">Spatializer platform support</span></span>
<span data-ttu-id="2eead-155">Windows offre Spatialization, y compris HRTFs, via l' [API ISpatialAudioClient](https://docs.microsoft.com/windows/win32/coreaudio/spatial-sound).</span><span class="sxs-lookup"><span data-stu-id="2eead-155">Windows offers spatialization, including HRTFs, via the [ISpatialAudioClient API](https://docs.microsoft.com/windows/win32/coreaudio/spatial-sound).</span></span> <span data-ttu-id="2eead-156">Cette API expose l’accélération matérielle HoloLens 2 HRTF aux applications.</span><span class="sxs-lookup"><span data-stu-id="2eead-156">This API exposes the HoloLens 2 HRTF hardware acceleration to applications.</span></span>

### <a name="spatializer-middleware-support"></a><span data-ttu-id="2eead-157">Prise en charge de l’intergiciel Spatializer</span><span class="sxs-lookup"><span data-stu-id="2eead-157">Spatializer middleware support</span></span>
<span data-ttu-id="2eead-158">La prise en charge de Windows HRTFs est disponible pour les moteurs audio tiers suivants.</span><span class="sxs-lookup"><span data-stu-id="2eead-158">Support for Windows' HRTFs is available for the following third-party audio engines.</span></span>
* <span data-ttu-id="2eead-159">Un [plug-in de moteur audio Unity](spatial-sound-in-unity.md)</span><span class="sxs-lookup"><span data-stu-id="2eead-159">A [Unity audio engine plugin](spatial-sound-in-unity.md)</span></span>
* <span data-ttu-id="2eead-160">Un [plug-in de moteur audio Wwise](https://www.audiokinetic.com/products/plug-ins/msspatial/)</span><span class="sxs-lookup"><span data-stu-id="2eead-160">A [Wwise audio engine plugin](https://www.audiokinetic.com/products/plug-ins/msspatial/)</span></span>

## <a name="acoustics"></a><span data-ttu-id="2eead-161">Acoustiques</span><span class="sxs-lookup"><span data-stu-id="2eead-161">Acoustics</span></span>
<span data-ttu-id="2eead-162">Le son spatial est plus que la direction.</span><span class="sxs-lookup"><span data-stu-id="2eead-162">Spatial audio is about more than direction.</span></span> <span data-ttu-id="2eead-163">Les autres dimensions incluent l’occlusion, l’obstruction, la réverbération, le portail et la modélisation source.</span><span class="sxs-lookup"><span data-stu-id="2eead-163">Other dimensions include occlusion, obstruction, reverb, portalling, and source modeling.</span></span> <span data-ttu-id="2eead-164">Ces dimensions sont collectivement appelées « *acoustiques*».</span><span class="sxs-lookup"><span data-stu-id="2eead-164">Collectively these dimensions are referred to as *acoustics*.</span></span> <span data-ttu-id="2eead-165">Sans acoustiques, les sons spatiaux n’ont pas de distance perçue.</span><span class="sxs-lookup"><span data-stu-id="2eead-165">Without acoustics, spatialized sounds lack perceived distance.</span></span>

<span data-ttu-id="2eead-166">Les traitements acoustiques vont du plus simple au plus complexe.</span><span class="sxs-lookup"><span data-stu-id="2eead-166">Acoustics treatments range from simple to very complex.</span></span> <span data-ttu-id="2eead-167">Vous pouvez utiliser un verbe simple qui est pris en charge par n’importe quel moteur audio pour envoyer des sons spatiales dans l’environnement de l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="2eead-167">You can use a simple reverb that's supported by any audio engine to push spatialized sounds into the environment of the listener.</span></span> <span data-ttu-id="2eead-168">Les systèmes acoustiques, tels que les [acoustiques de projet](https://aka.ms/acoustics) , offrent un traitement des acoustiques plus riche et plus attrayant.</span><span class="sxs-lookup"><span data-stu-id="2eead-168">Acoustics systems such as [Project Acoustics](https://aka.ms/acoustics)  provide richer and more compelling acoustics treatment.</span></span> <span data-ttu-id="2eead-169">Les acoustiques de projet peuvent modéliser l’effet des murs, des portes et d’autres géométries de scène sur un son.</span><span class="sxs-lookup"><span data-stu-id="2eead-169">Project Acoustics can model the effect of walls, doors, and other scene geometry on a sound.</span></span> <span data-ttu-id="2eead-170">C’est une option efficace pour les cas où la géométrie de scène appropriée est connue au moment du développement.</span><span class="sxs-lookup"><span data-stu-id="2eead-170">It's an effective option for cases where the relevant scene geometry is known at development time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2eead-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2eead-171">Next steps</span></span>
- [<span data-ttu-id="2eead-172">Son spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="2eead-172">Spatial sound in Unity</span></span>](spatial-sound-in-unity.md)
- [<span data-ttu-id="2eead-173">Comment utiliser le son dans des applications en réalité mixte</span><span class="sxs-lookup"><span data-stu-id="2eead-173">How to use sound in mixed-reality applications</span></span>](spatial-sound-design.md)
