---
title: Audio en réalité mixte
description: L’audio en réalité mixte peut augmenter la confiance des utilisateurs dans les interactions entre les interfaces utilisateur et plonger les utilisateurs dans l’expérience.
author: kegodin
ms.author: kegodin
ms.date: 11/07/2019
ms.topic: article
keywords: son spatial, son surround, audio 3D, son 3D, son spatial
ms.openlocfilehash: 1930017903439aee3ac53b6c4be344fdc44c356f
ms.sourcegitcommit: 2e54d0aff91dc31aa0020c865dada3ae57ae0ffc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73641114"
---
# <a name="audio-in-mixed-reality"></a><span data-ttu-id="eaf1d-104">Audio en réalité mixte</span><span class="sxs-lookup"><span data-stu-id="eaf1d-104">Audio in Mixed Reality</span></span>
<span data-ttu-id="eaf1d-105">L’audio est un élément essentiel de la conception et de la productivité en réalité mixte, et peut :</span><span class="sxs-lookup"><span data-stu-id="eaf1d-105">Audio is an essential part of design and productivity in mixed reality, and can:</span></span>
* <span data-ttu-id="eaf1d-106">Augmentez la confiance des utilisateurs dans les interactions basées sur les gestes et les voix</span><span class="sxs-lookup"><span data-stu-id="eaf1d-106">Increase user confidence in gesture- and voice-based interactions</span></span>
* <span data-ttu-id="eaf1d-107">Guider les utilisateurs vers les étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eaf1d-107">Guide users to next steps</span></span>
* <span data-ttu-id="eaf1d-108">Combiner efficacement des objets virtuels avec le monde réel</span><span class="sxs-lookup"><span data-stu-id="eaf1d-108">Effectively combine virtual objects with the real world</span></span>

<span data-ttu-id="eaf1d-109">Le suivi de la tête à faible latence des casques de réalité mixte, y compris HoloLens, permet l’utilisation de Spatialization HRTF de haute qualité.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-109">The low-latency head tracking of mixed reality headsets, including HoloLens, enables the use of high quality HRTF-based spatialization.</span></span> <span data-ttu-id="eaf1d-110">L’aménagement de l’audio dans votre application peut :</span><span class="sxs-lookup"><span data-stu-id="eaf1d-110">Spatializing audio in your application can:</span></span>
* <span data-ttu-id="eaf1d-111">Attirer l’attention sur les éléments visuels</span><span class="sxs-lookup"><span data-stu-id="eaf1d-111">Call attention to visual elements</span></span>
* <span data-ttu-id="eaf1d-112">Aider les utilisateurs à prendre conscience de leur environnement réel</span><span class="sxs-lookup"><span data-stu-id="eaf1d-112">Help users maintain awareness of their real-world surroundings</span></span>

<span data-ttu-id="eaf1d-113">L’ajout de acoustiques connecte plus profondément les hologrammes au monde mixte et peut fournir des indications sur l’environnement et l’état de l’objet.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-113">Adding acoustics more deeply connects holograms to the mixed world, and can provide cues about the environment and object state.</span></span>

<span data-ttu-id="eaf1d-114">Pour obtenir des exemples plus détaillés de la conception à l’aide de l’audio, consultez [conception audio](spatial-sound-design.md).</span><span class="sxs-lookup"><span data-stu-id="eaf1d-114">For more detailed examples of design using audio, see [sound design](spatial-sound-design.md).</span></span>

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/PTPvx7mDon4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## <a name="device-support"></a><span data-ttu-id="eaf1d-115">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="eaf1d-115">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="eaf1d-116"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="eaf1d-116"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="eaf1d-117"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="eaf1d-117"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="eaf1d-118"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="eaf1d-118"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="eaf1d-119"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="eaf1d-119"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="eaf1d-120">Spatialization</span><span class="sxs-lookup"><span data-stu-id="eaf1d-120">Spatialization</span></span></td>
        <td><span data-ttu-id="eaf1d-121">✔️</span><span class="sxs-lookup"><span data-stu-id="eaf1d-121">✔️</span></span></td>
        <td><span data-ttu-id="eaf1d-122">✔️</span><span class="sxs-lookup"><span data-stu-id="eaf1d-122">✔️</span></span></td>
        <td><span data-ttu-id="eaf1d-123">✔️</span><span class="sxs-lookup"><span data-stu-id="eaf1d-123">✔️</span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="eaf1d-124">Accélération matérielle Spatialization</span><span class="sxs-lookup"><span data-stu-id="eaf1d-124">Spatialization hardware acceleration</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="eaf1d-125">✔️</span><span class="sxs-lookup"><span data-stu-id="eaf1d-125">✔️</span></span></td>
        <td>❌</td>
    </tr>
</table>

## <a name="using-sounds-in-mixed-reality"></a><span data-ttu-id="eaf1d-126">Utilisation de sons dans une réalité mixte</span><span class="sxs-lookup"><span data-stu-id="eaf1d-126">Using sounds in mixed reality</span></span>
<span data-ttu-id="eaf1d-127">[L’utilisation de sons en réalité mixte](spatial-sound-design.md) peut nécessiter une approche différente de celle des applications tactiles et du clavier et de la souris.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-127">[Using sounds in mixed reality](spatial-sound-design.md) can require a different approach than in touch and keyboard-and-mouse applications.</span></span> <span data-ttu-id="eaf1d-128">Les décisions relatives à la conception de sons clés incluent les sons à spatialiser et les interactions à sonify.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-128">Key sound design decisions include which sounds to spatialize and which interactions to sonify.</span></span> <span data-ttu-id="eaf1d-129">Ces décisions peuvent avoir un impact important sur la confiance des utilisateurs, la productivité et la courbe d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-129">These decisions can have a strong effect on user confidence, productivity, and learning curve.</span></span>

### <a name="case-studies"></a><span data-ttu-id="eaf1d-130">Études de cas</span><span class="sxs-lookup"><span data-stu-id="eaf1d-130">Case studies</span></span>
<span data-ttu-id="eaf1d-131">HoloTour prend pratiquement les utilisateurs sur des sites touristiques et historiques dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-131">HoloTour virtually takes users to tourist and historical sites around the world.</span></span> <span data-ttu-id="eaf1d-132">L’étude de cas suivante décrit la conception saine de HoloTour : [Sound Design pour HoloTour](case-study-spatial-sound-design-for-holotour.md).</span><span class="sxs-lookup"><span data-stu-id="eaf1d-132">The following case study describes the sound design for HoloTour: [Sound design for HoloTour](case-study-spatial-sound-design-for-holotour.md).</span></span> <span data-ttu-id="eaf1d-133">Un microphone spécial et une configuration de rendu ont été utilisés pour capturer les espaces de sujet.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-133">A special microphone and rendering setup were used to capture the subject spaces.</span></span>

<span data-ttu-id="eaf1d-134">RoboRaid est un tir à haute énergie pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-134">RoboRaid is a high-energy shooter for HoloLens.</span></span> <span data-ttu-id="eaf1d-135">L’étude de cas suivante décrit les choix de conception effectués pour garantir que l’audio spatial a été utilisé pour atteindre un effet spectaculaire : la [conception de sons pour RoboRaid](case-study-using-spatial-sound-in-roboraid.md).</span><span class="sxs-lookup"><span data-stu-id="eaf1d-135">The following case study describes the design choices made to ensure spatial audio was used to fullest dramatic effect: [Sound design for RoboRaid](case-study-using-spatial-sound-in-roboraid.md).</span></span>

## <a name="spatialization"></a><span data-ttu-id="eaf1d-136">Spatialization</span><span class="sxs-lookup"><span data-stu-id="eaf1d-136">Spatialization</span></span>
<span data-ttu-id="eaf1d-137">Spatialization est le composant directionnel du son spatial.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-137">Spatialization is the directional component of spatial audio.</span></span> <span data-ttu-id="eaf1d-138">Lors de l’utilisation d’une configuration Home cinéma 7,1, Spatialization est aussi simple que le panoramique entre les haut-parleurs forts.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-138">When using a 7.1 home theater setup, spatialization is as simple as panning between loud speakers.</span></span> <span data-ttu-id="eaf1d-139">Mais avec un casque en réalité mixte, il est essentiel d’utiliser une technologie HRTF pour la précision et le confort.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-139">But with headphones in mixed reality it's essential to use an HRTF-based technology for accuracy and comfort.</span></span> <span data-ttu-id="eaf1d-140">Windows propose des Spatialization basés sur HRTF, et cette prise en charge est accélérée par le matériel sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-140">Windows offers HRTF-based spatialization, and this support is hardware-accelerated on HoloLens 2.</span></span>

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/aB3TDjYklmo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### <a name="should-i-spatialize"></a><span data-ttu-id="eaf1d-141">Dois-je spatialiser ?</span><span class="sxs-lookup"><span data-stu-id="eaf1d-141">Should I spatialize?</span></span>
<span data-ttu-id="eaf1d-142">De nombreux sons dans les applications de réalité mixte tirent parti de Spatialization, qui tire un son de la tête de l’écouteur et le place dans le monde.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-142">Many sounds in mixed reality applications benefit from spatialization, which takes a sound out of the listener's head and places it in the world.</span></span> <span data-ttu-id="eaf1d-143">Reportez-vous à la [conception de son spatial](spatial-sound-design.md) pour obtenir des suggestions sur les utilisations les plus efficaces de Spatialization dans votre application.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-143">Refer to [Spatial Sound Design](spatial-sound-design.md) for suggestions on the most effective uses of spatialization in your application.</span></span>

### <a name="spatializer-personalization"></a><span data-ttu-id="eaf1d-144">Personnalisation de Spatializer</span><span class="sxs-lookup"><span data-stu-id="eaf1d-144">Spatializer personalization</span></span>
<span data-ttu-id="eaf1d-145">Les HRTFs manipulent les différences de niveau et de phase entre les oreilles à travers le spectre de fréquences.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-145">HRTFs manipulate the level and phase differences between ears across the frequency spectrum.</span></span> <span data-ttu-id="eaf1d-146">Ils sont basés sur des modèles physiques et des mesures de la tête humaine, du tors et des formes d’oreille (pinnae).</span><span class="sxs-lookup"><span data-stu-id="eaf1d-146">They're based on physical models and measurements of human head, torso, and ear shapes (pinnae).</span></span> <span data-ttu-id="eaf1d-147">Notre cerveau répond à ces différences pour donner une idée de la direction du son.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-147">Our brains respond to these differences to give rise to a perception of direction in sound.</span></span> 

<span data-ttu-id="eaf1d-148">Chaque individu a une forme d’oreille, une taille de tête et une position Ear uniques, donc les meilleurs HRTFs sont ceux qui se conforment à vous.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-148">Every individual has a unique ear shape, head size, and ear position, so the best HRTFs are those that conform to you.</span></span> <span data-ttu-id="eaf1d-149">HoloLens augmente la précision de la Spatialization en utilisant votre distance inter-pupille (IPD) à partir du casque pour ajuster la HRTFs pour la taille de la tête.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-149">HoloLens increases spatialization accuracy by using your inter-pupilary distance (IPD) from the headset displays to adjust the HRTFs for your head size.</span></span>

### <a name="spatializer-platform-support"></a><span data-ttu-id="eaf1d-150">Prise en charge de la plateforme Spatializer</span><span class="sxs-lookup"><span data-stu-id="eaf1d-150">Spatializer platform support</span></span>
<span data-ttu-id="eaf1d-151">Windows offre Spatialization, y compris HRTFs, via l' [API ISpatialAudioClient](https://docs.microsoft.com/windows/win32/coreaudio/spatial-sound).</span><span class="sxs-lookup"><span data-stu-id="eaf1d-151">Windows offers spatialization, including HRTFs, via the [ISpatialAudioClient API](https://docs.microsoft.com/windows/win32/coreaudio/spatial-sound).</span></span> <span data-ttu-id="eaf1d-152">Cette API expose l’accélération matérielle HoloLens 2 HRTF aux applications.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-152">This API exposes the HoloLens 2 HRTF hardware acceleration to applications.</span></span>

### <a name="spatializer-middleware-support"></a><span data-ttu-id="eaf1d-153">Prise en charge de l’intergiciel Spatializer</span><span class="sxs-lookup"><span data-stu-id="eaf1d-153">Spatializer middleware support</span></span>
<span data-ttu-id="eaf1d-154">La prise en charge de Windows HRTFs est disponible pour certains moteurs audio tiers :</span><span class="sxs-lookup"><span data-stu-id="eaf1d-154">Support for Windows' HRTFs is available for some 3rd-party audio engines:</span></span>
* <span data-ttu-id="eaf1d-155">Un plug-in de [moteur audio Unity](spatial-sound-in-unity.md) appelle le XAPO HRTF</span><span class="sxs-lookup"><span data-stu-id="eaf1d-155">A [Unity audio engine](spatial-sound-in-unity.md) plugin calls the HRTF XAPO</span></span>
* <span data-ttu-id="eaf1d-156">Un [plug-in de moteur audio Wwise](https://www.audiokinetic.com/products/plug-ins/msspatial/) appelle l’API ISpatialAudioClient</span><span class="sxs-lookup"><span data-stu-id="eaf1d-156">A [Wwise audio engine plugin](https://www.audiokinetic.com/products/plug-ins/msspatial/) calls the ISpatialAudioClient API</span></span>

## <a name="acoustics"></a><span data-ttu-id="eaf1d-157">Acoustiques</span><span class="sxs-lookup"><span data-stu-id="eaf1d-157">Acoustics</span></span>
<span data-ttu-id="eaf1d-158">L’audio spatial peut être plus ou moins que la direction.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-158">Spatial audio can be about more than direction.</span></span> <span data-ttu-id="eaf1d-159">Les autres dimensions, y compris l’occlusion, l’obstruction, la réverbération, le portail et la modélisation source, sont collectivement appelées « acoustiques ».</span><span class="sxs-lookup"><span data-stu-id="eaf1d-159">Other dimensions, including occlusion, obstruction, reverb, portalling, and source modelling, are collectively referred to as 'acoustics'.</span></span> <span data-ttu-id="eaf1d-160">Sans acoustiques, les sons spatiaux n’ont pas une distance perçue.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-160">Without acoustics, spatialized sounds lack a perceived distance.</span></span>

<span data-ttu-id="eaf1d-161">Le traitement des acoustiques peut aller du simple au très complexe.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-161">Acoustics treatment can range from simple to very complex.</span></span> <span data-ttu-id="eaf1d-162">En utilisant un verbe simple, tel que celui pris en charge par n’importe quel moteur audio, vous pouvez envoyer des sons spatiaux dans l’environnement qui entoure l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-162">By using a simple reverb, such as that supported by any audio engine, you can push spatialized sounds out into the environment surrounding the listener.</span></span> <span data-ttu-id="eaf1d-163">Le traitement des acoustiques plus riches et plus attrayant est disponible à partir de systèmes acoustiques tels que les [acoustiques de projet](https://aka.ms/acoustics).</span><span class="sxs-lookup"><span data-stu-id="eaf1d-163">Richer and more compelling acoustics treatment is available from acoustics systems such as [Project Acoustics](https://aka.ms/acoustics).</span></span> <span data-ttu-id="eaf1d-164">Les acoustiques de projet peuvent modéliser l’effet des murs, des portes et d’autres géométries de scène sur un son, et est une option efficace pour les cas où la géométrie de scène appropriée est connue au moment du développement.</span><span class="sxs-lookup"><span data-stu-id="eaf1d-164">Project Acoustics can model the effect of walls, doors, and other scene geometry on a sound, and is an effective option for cases where the relevant scene geometry is known at development time.</span></span>

