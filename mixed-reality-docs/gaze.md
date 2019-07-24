---
title: Pointage du regard
description: Le point de présence est la première forme d’entrée et est une forme principale de ciblage au sein de la réalité mixte.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: Réalité mixte, point de regard, interaction, conception
ms.openlocfilehash: 7e65d26d3e9edabbd01d35a887ffc8622a3c6337
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414369"
---
# <a name="gaze"></a><span data-ttu-id="22d41-104">Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="22d41-104">Gaze</span></span>

<span data-ttu-id="22d41-105">Le point de **présence est la** première forme d’entrée et est une forme principale de ciblage au sein de la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="22d41-105">**Gaze** is the first form of input and is a primary form of targeting within mixed reality.</span></span> <span data-ttu-id="22d41-106">Le point de regard indique où l’utilisateur regarde dans le monde et vous permet de déterminer son intention.</span><span class="sxs-lookup"><span data-stu-id="22d41-106">Gaze tells you where the user is looking in the world and lets you determine their intent.</span></span> <span data-ttu-id="22d41-107">Dans le monde réel, vous examinez généralement un objet avec lequel vous souhaitez interagir.</span><span class="sxs-lookup"><span data-stu-id="22d41-107">In the real world, you'll typically look at an object that you intend to interact with.</span></span> <span data-ttu-id="22d41-108">C’est le même avec le point de regard.</span><span class="sxs-lookup"><span data-stu-id="22d41-108">This is the same with gaze.</span></span>

<span data-ttu-id="22d41-109">Les casques de réalité mixte utilisent la position et l’orientation de la tête de l’utilisateur pour déterminer le vecteur de regard de son en-tête.</span><span class="sxs-lookup"><span data-stu-id="22d41-109">Mixed reality headsets use the position and orientation of your user's head to determine their head gaze vector.</span></span> <span data-ttu-id="22d41-110">Vous pouvez considérer ce vecteur comme un pointeur laser directement entre les yeux de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="22d41-110">You can think of this vector as a laser pointer straight ahead from directly between the user's eyes.</span></span> <span data-ttu-id="22d41-111">À mesure que l’utilisateur regarde dans la pièce, votre application peut croiser ce rayon, à la fois avec ses propres hologrammes et avec le maillage de [mappage spatial](spatial-mapping.md) pour déterminer l’objet virtuel ou réel que votre utilisateur peut consulter.</span><span class="sxs-lookup"><span data-stu-id="22d41-111">As the user looks around the room, your application can intersect this ray, both with its own holograms and with the [spatial mapping](spatial-mapping.md) mesh to determine what virtual or real-world object your user may be looking at.</span></span>

<span data-ttu-id="22d41-112">Sur HoloLens 2, les interactions peuvent être ciblées par les intersections du point de regard de l’utilisateur, du regard ou des interactions près ou Far.</span><span class="sxs-lookup"><span data-stu-id="22d41-112">On HoloLens 2, interactions can be targeted by either the user's head gaze, eye gaze or through near or far hand interactions.</span></span>
<span data-ttu-id="22d41-113">Sur HoloLens (1ère génération), les interactions doivent généralement dériver leur ciblage du point de vue de l’utilisateur, au lieu d’essayer d’effectuer un rendu ou une interaction directement à l’emplacement de la main.</span><span class="sxs-lookup"><span data-stu-id="22d41-113">On HoloLens (1st gen), interactions should generally derive their targeting from the user's head gaze, rather than trying to render or interact at the hand's location directly.</span></span> <span data-ttu-id="22d41-114">Une fois qu’une interaction a démarré, les mouvements relatifs de la main peuvent être utilisés pour contrôler le [mouvement](gestures.md), comme avec la [manipulation ou](gestures.md#composite-gestures) le mouvement de navigation.</span><span class="sxs-lookup"><span data-stu-id="22d41-114">Once an interaction has started, relative motions of the hand may be used to control the [gesture](gestures.md), as with the [manipulation or navigation](gestures.md#composite-gestures) gesture.</span></span> <span data-ttu-id="22d41-115">Avec les casques immersifs, vous pouvez cibler à l’aide de contrôleurs de [mouvement](motion-controllers.md)de pointage de tête ou de pointage.</span><span class="sxs-lookup"><span data-stu-id="22d41-115">With immersive headsets, you can target using either head gaze or pointing-capable [motion controllers](motion-controllers.md).</span></span>

<br>

>[!VIDEO https://www.youtube.com/embed/zCPiZlWdVws]

## <a name="device-support"></a><span data-ttu-id="22d41-116">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="22d41-116">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="22d41-117"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="22d41-117"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="22d41-118"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="22d41-118"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="22d41-119"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="22d41-119"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="22d41-120"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="22d41-120"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="22d41-121">Point de tête</span><span class="sxs-lookup"><span data-stu-id="22d41-121">Head gaze</span></span></td>
        <td><span data-ttu-id="22d41-122">✔️</span><span class="sxs-lookup"><span data-stu-id="22d41-122">✔️</span></span></td>
        <td><span data-ttu-id="22d41-123">✔️</span><span class="sxs-lookup"><span data-stu-id="22d41-123">✔️</span></span></td>
        <td><span data-ttu-id="22d41-124">✔️</span><span class="sxs-lookup"><span data-stu-id="22d41-124">✔️</span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="22d41-125">Point de regard</span><span class="sxs-lookup"><span data-stu-id="22d41-125">Eye gaze</span></span></td>
        <td><span data-ttu-id="22d41-126">❌</span><span class="sxs-lookup"><span data-stu-id="22d41-126">❌</span></span></td>
        <td><span data-ttu-id="22d41-127">✔️</span><span class="sxs-lookup"><span data-stu-id="22d41-127">✔️</span></span></td>
        <td><span data-ttu-id="22d41-128">❌</span><span class="sxs-lookup"><span data-stu-id="22d41-128">❌</span></span></td>
    </tr>
</table>

> [!NOTE]
> <span data-ttu-id="22d41-129">Plus d’instructions spécifiques à HoloLens 2 bientôt [disponible](index.md#news-and-notes).</span><span class="sxs-lookup"><span data-stu-id="22d41-129">More guidance specific to HoloLens 2 [coming soon](index.md#news-and-notes).</span></span>


## <a name="uses-of-gaze"></a><span data-ttu-id="22d41-130">Utilisations du point de regard</span><span class="sxs-lookup"><span data-stu-id="22d41-130">Uses of gaze</span></span>

<span data-ttu-id="22d41-131">En tant que développeur de réalité mixte, vous pouvez faire beaucoup de regard en tête ou en œil:</span><span class="sxs-lookup"><span data-stu-id="22d41-131">As a mixed reality developer, you can do a lot with head or eye gaze:</span></span>
* <span data-ttu-id="22d41-132">Votre application peut faire une intersection avec le regard des hologrammes dans votre scène pour déterminer où se trouve l’attention de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="22d41-132">Your app can intersect gaze with the holograms in your scene to determine where the user's attention is.</span></span>
* <span data-ttu-id="22d41-133">Votre application peut cibler les gestes et les presses du contrôleur en fonction du point de regard de l’utilisateur, ce qui permet à l’utilisateur de sélectionner, d’activer, de saisir, de faire défiler ou d’interagir de manière interactive avec ses hologrammes.</span><span class="sxs-lookup"><span data-stu-id="22d41-133">Your app can target gestures and controller presses based on the user's gaze, letting the user select, activate, grab, scroll, or otherwise interact with their holograms.</span></span>
* <span data-ttu-id="22d41-134">Votre application peut permettre à l’utilisateur de placer des hologrammes sur des surfaces réelles, en croisant leur rayon de regard avec le maillage de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="22d41-134">Your app can let the user place holograms on real-world surfaces, by intersecting their gaze ray with the spatial mapping mesh.</span></span>
* <span data-ttu-id="22d41-135">Votre application peut savoir quand l’utilisateur *ne cherche pas* dans la direction d’un objet important, ce qui peut amener votre application à donner des signaux visuels et audio pour tourner vers cet objet.</span><span class="sxs-lookup"><span data-stu-id="22d41-135">Your app can know when the user is *not* looking in the direction of an important object, which can lead your app to give visual and audio cues to turn towards that object.</span></span>

## <a name="cursor"></a><span data-ttu-id="22d41-136">Curseur</span><span class="sxs-lookup"><span data-stu-id="22d41-136">Cursor</span></span>

<span data-ttu-id="22d41-137">Pour le point de vue de la tête, la plupart des applications doivent utiliser un [curseur](cursors.md) (ou une autre indication d’audit/visuel) pour donner à l’utilisateur la certitude de ce qu’ils sont sur le point d’interagir.</span><span class="sxs-lookup"><span data-stu-id="22d41-137">For head gaze, most apps should use a [cursor](cursors.md) (or other auditory/visual indication) to give the user confidence in what they're about to interact with.</span></span> <span data-ttu-id="22d41-138">En règle générale, vous positionnez ce curseur dans le monde où le rayon de regard de son en-tête croise d’abord un objet, qui peut être un hologramme ou une surface réaliste.</span><span class="sxs-lookup"><span data-stu-id="22d41-138">You typically position this cursor in the world where their head gaze ray first intersects an object, which may be a hologram or a real-world surface.</span></span>

<span data-ttu-id="22d41-139">![Exemple de curseur visuel pour afficher le regard](images/cursor.jpg)</span><span class="sxs-lookup"><span data-stu-id="22d41-139">![An example visual cursor to show gaze](images/cursor.jpg)</span></span><br>
<span data-ttu-id="22d41-140">*Exemple de curseur visuel pour afficher le regard*</span><span class="sxs-lookup"><span data-stu-id="22d41-140">*An example visual cursor to show gaze*</span></span>

<span data-ttu-id="22d41-141">Pour les yeux oculaires, nous vous recommandons généralement de *ne pas* afficher de curseur, car cela peut rapidement devenir gênant et ennuyeux pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="22d41-141">For eye gaze, we generally recommend *not* to show a cursor, as this can quickly become distracting and annoying for the user.</span></span> <span data-ttu-id="22d41-142">À la place, mettez en surbrillance les cibles visuelles ou utilisez un curseur très pâle pour faire confiance à ce que l’utilisateur est sur le point d’interagir.</span><span class="sxs-lookup"><span data-stu-id="22d41-142">Instead subtly highlight visual targets or use a very faint eye cursor to provide confidence about what the user is about to interact with.</span></span> <span data-ttu-id="22d41-143">Pour plus d’informations, consultez notre [Guide de conception pour une entrée basée](eye-tracking.md) sur l’œil sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="22d41-143">For more information, please check out our [design guidance for eye-based input](eye-tracking.md) on HoloLens 2.</span></span>

## <a name="giving-action-to-the-users-gaze"></a><span data-ttu-id="22d41-144">Donner une action au point de vue de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="22d41-144">Giving action to the user's gaze</span></span>

<span data-ttu-id="22d41-145">Une fois que l’utilisateur a ciblé un hologramme ou un objet réel à l’aide de son regard, l’étape suivante consiste à agir sur cet objet.</span><span class="sxs-lookup"><span data-stu-id="22d41-145">Once the user has targeted a hologram or real-world object using their gaze, their next step is to take action on that object.</span></span> <span data-ttu-id="22d41-146">Les principales méthodes permettant à un utilisateur de prendre des mesures sont les [gestes](gestures.md), les contrôleurs de [mouvement](motion-controllers.md) et la [voix](voice-input.md).</span><span class="sxs-lookup"><span data-stu-id="22d41-146">The primary ways for a user to take action are through [gestures](gestures.md), [motion controllers](motion-controllers.md) and [voice](voice-input.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="22d41-147">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="22d41-147">See also</span></span>
* [<span data-ttu-id="22d41-148">Réalité mixte - Entrées - Cours 210 : Point de tête</span><span class="sxs-lookup"><span data-stu-id="22d41-148">MR Input 210: Head gaze</span></span>](holograms-210.md)
* [<span data-ttu-id="22d41-149">Suivre de la tête et du regard dans DirectX</span><span class="sxs-lookup"><span data-stu-id="22d41-149">Head and eye gaze in DirectX</span></span>](gaze-in-directx.md)
* [<span data-ttu-id="22d41-150">Point de regard de l’en-tête dans Unity</span><span class="sxs-lookup"><span data-stu-id="22d41-150">Head gaze in Unity</span></span>](gaze-in-unity.md)
* [<span data-ttu-id="22d41-151">Eye-point de regard sur HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="22d41-151">Eye-gaze on HoloLens 2</span></span>](eye-tracking.md)
* [<span data-ttu-id="22d41-152">Point de regard sur Unity avec la réalité mixte Toolkit</span><span class="sxs-lookup"><span data-stu-id="22d41-152">Eye gaze in Unity using Mixed Reality Toolkit</span></span>](https://aka.ms/mrtk-eyes)
