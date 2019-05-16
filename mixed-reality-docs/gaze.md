---
title: Pointage du regard
description: Regards est la première forme d’entrée et un principal de ciblage dans la réalité mixte.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: Réalité mixte, regards, Interaction, concevoir
ms.openlocfilehash: 738ba9063a5d00f3bbedce989d93076d56ad1a44
ms.sourcegitcommit: 45676da11ebe33a2aa3dccec0e8ad7d714420853
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65629108"
---
# <a name="gaze"></a><span data-ttu-id="5b354-104">Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="5b354-104">Gaze</span></span>

<span data-ttu-id="5b354-105">**Utilisation** est la première forme d’entrée et un principal de ciblage dans la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="5b354-105">**Gaze** is the first form of input and is a primary form of targeting within mixed reality.</span></span> <span data-ttu-id="5b354-106">Regards vous indique où l’utilisateur recherche dans le monde et vous permet de déterminer leur intention.</span><span class="sxs-lookup"><span data-stu-id="5b354-106">Gaze tells you where the user is looking in the world and lets you determine their intent.</span></span> <span data-ttu-id="5b354-107">Dans le monde réel, vous ferez généralement à un objet que vous avez l’intention d’interagir avec.</span><span class="sxs-lookup"><span data-stu-id="5b354-107">In the real world, you'll typically look at an object that you intend to interact with.</span></span> <span data-ttu-id="5b354-108">Il s’agit même avec les regards.</span><span class="sxs-lookup"><span data-stu-id="5b354-108">This is the same with gaze.</span></span>

<span data-ttu-id="5b354-109">Casques de réalité mixte utilisent la position et l’orientation de tête de l’utilisateur pour déterminer leur vecteur regards principal.</span><span class="sxs-lookup"><span data-stu-id="5b354-109">Mixed reality headsets use the position and orientation of your user's head to determine their head gaze vector.</span></span> <span data-ttu-id="5b354-110">Vous pouvez considérer ce vecteur comme un pointeur laser directement à l’avance de directement entre les yeux de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5b354-110">You can think of this vector as a laser pointer straight ahead from directly between the user's eyes.</span></span> <span data-ttu-id="5b354-111">Comme l’utilisateur semble autour de la pièce, votre application peut se croisent ce rayon, avec son propre hologrammes et avec le [mappage spatial](spatial-mapping.md) maille pour déterminer quel objet virtuel ou réelles de votre utilisateur peut regarder.</span><span class="sxs-lookup"><span data-stu-id="5b354-111">As the user looks around the room, your application can intersect this ray, both with its own holograms and with the [spatial mapping](spatial-mapping.md) mesh to determine what virtual or real-world object your user may be looking at.</span></span>

<span data-ttu-id="5b354-112">Sur HoloLens 2, interactions peuvent être ciblées par les regards principal soit l’utilisateur par le biais de près ou présent distribuer interactions.</span><span class="sxs-lookup"><span data-stu-id="5b354-112">On HoloLens 2, interactions can be targeted by either the user's head gaze or through near or far hand interactions.</span></span>  <span data-ttu-id="5b354-113">Sur HoloLens (1er gen), les interactions doivent dériver généralement leur ciblage à partir des regards principal de l’utilisateur, au lieu d’essayer restituer ou interagir directement à l’emplacement de la part.</span><span class="sxs-lookup"><span data-stu-id="5b354-113">On HoloLens (1st gen), interactions should generally derive their targeting from the user's head gaze, rather than trying to render or interact at the hand's location directly.</span></span> <span data-ttu-id="5b354-114">Une fois démarrée, une interaction des mouvements relatifs de la main peuvent être utilisé pour contrôle le [mouvement](gestures.md), comme avec la [manipulation ou navigation](gestures.md#composite-gestures) mouvement.</span><span class="sxs-lookup"><span data-stu-id="5b354-114">Once an interaction has started, relative motions of the hand may be used to control the [gesture](gestures.md), as with the [manipulation or navigation](gestures.md#composite-gestures) gesture.</span></span> <span data-ttu-id="5b354-115">Avec des casques IMMERSIFS, vous pouvez cibler à l’aide soit du pointage de regard ou pointant compatibles [contrôleurs de mouvement](motion-controllers.md).</span><span class="sxs-lookup"><span data-stu-id="5b354-115">With immersive headsets, you can target using either gaze or pointing-capable [motion controllers](motion-controllers.md).</span></span>

<br>

>[!VIDEO https://www.youtube.com/embed/zCPiZlWdVws]

## <a name="device-support"></a><span data-ttu-id="5b354-116">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="5b354-116">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="5b354-117">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="5b354-117">Feature</span></span></th><th style="width:150px"> <span data-ttu-id="5b354-118"><a href="hololens-hardware-details.md">HoloLens (1er gen)</a></span><span class="sxs-lookup"><span data-stu-id="5b354-118"><a href="hololens-hardware-details.md">HoloLens (1st gen)</a></span></span></th><th style="width:150px"><span data-ttu-id="5b354-119">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="5b354-119">HoloLens 2</span></span></th><th style="width:150px"> <span data-ttu-id="5b354-120"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="5b354-120"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="5b354-121">Utilisation de la tête</span><span class="sxs-lookup"><span data-stu-id="5b354-121">Head gaze</span></span></td><td style="text-align: center;"> <span data-ttu-id="5b354-122">✔️</span><span class="sxs-lookup"><span data-stu-id="5b354-122">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="5b354-123">✔️</span><span class="sxs-lookup"><span data-stu-id="5b354-123">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="5b354-124">✔️</span><span class="sxs-lookup"><span data-stu-id="5b354-124">✔️</span></span></td>
</tr><tr>
<td> <span data-ttu-id="5b354-125">Regard de œil</span><span class="sxs-lookup"><span data-stu-id="5b354-125">Eye gaze</span></span></td><td></td><td style="text-align: center;"><span data-ttu-id="5b354-126">✔️</span><span class="sxs-lookup"><span data-stu-id="5b354-126">✔️</span></span></td><td></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="5b354-127">Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).</span><span class="sxs-lookup"><span data-stu-id="5b354-127">More guidance specific to HoloLens 2 [coming soon](index.md#news-and-notes).</span></span>


## <a name="uses-of-gaze"></a><span data-ttu-id="5b354-128">Utilisations des regards</span><span class="sxs-lookup"><span data-stu-id="5b354-128">Uses of gaze</span></span>

<span data-ttu-id="5b354-129">Un développeur de réalité mixte, vous pouvez faire beaucoup avec pointage de regard :</span><span class="sxs-lookup"><span data-stu-id="5b354-129">As a mixed reality developer, you can do a lot with gaze:</span></span>
* <span data-ttu-id="5b354-130">Votre application peut se croisent regards avec les hologrammes dans votre scène pour déterminer où se trouve l’attention des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5b354-130">Your app can intersect gaze with the holograms in your scene to determine where the user's attention is.</span></span>
* <span data-ttu-id="5b354-131">Votre application peut cibler des mouvements et appuie sur le contrôleur en fonction du pointage de regard de l’utilisateur, vous sélectionnez, activer, récupérer, faites défiler ou sinon interagir avec leurs hologrammes permettant de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5b354-131">Your app can target gestures and controller presses based on the user's gaze, letting the user select, activate, grab, scroll, or otherwise interact with their holograms.</span></span>
* <span data-ttu-id="5b354-132">Votre application peut permettre à l’utilisateur de placer des hologrammes sur les surfaces du monde réel, par l’intersection de leur ray regards auprès de la maille de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="5b354-132">Your app can let the user place holograms on real-world surfaces, by intersecting their gaze ray with the spatial mapping mesh.</span></span>
* <span data-ttu-id="5b354-133">Votre application peut savoir quand l’utilisateur est *pas* recherche dans la direction d’un objet important, ce qui peut conduire à votre application afin de donner des signaux visuels et audio pour activer vers cet objet.</span><span class="sxs-lookup"><span data-stu-id="5b354-133">Your app can know when the user is *not* looking in the direction of an important object, which can lead your app to give visual and audio cues to turn towards that object.</span></span>

## <a name="cursor"></a><span data-ttu-id="5b354-134">Curseur</span><span class="sxs-lookup"><span data-stu-id="5b354-134">Cursor</span></span>

<span data-ttu-id="5b354-135">La plupart des applications doivent utiliser un [curseur](cursors.md) (ou autre indication AUDITIVE/visual) à attribuer à la confiance des utilisateurs de ce que, ils sont sur le point d’interagir avec.</span><span class="sxs-lookup"><span data-stu-id="5b354-135">Most apps should use a [cursor](cursors.md) (or other auditory/visual indication) to give the user confidence in what they're about to interact with.</span></span> <span data-ttu-id="5b354-136">En général, vous positionnez ce curseur dans le monde où leur ray regards interagit tout d’abord un objet qui peut être un hologramme ou une surface du monde réel.</span><span class="sxs-lookup"><span data-stu-id="5b354-136">You typically position this cursor in the world where their gaze ray first interacts an object, which may be a hologram or a real-world surface.</span></span>

<span data-ttu-id="5b354-137">![Un exemple visuel du curseur pour afficher les regards](images/cursor.jpg)</span><span class="sxs-lookup"><span data-stu-id="5b354-137">![An example visual cursor to show gaze](images/cursor.jpg)</span></span><br>
<span data-ttu-id="5b354-138">*Un exemple visuel du curseur pour afficher les regards*</span><span class="sxs-lookup"><span data-stu-id="5b354-138">*An example visual cursor to show gaze*</span></span>

## <a name="giving-action-to-the-users-gaze"></a><span data-ttu-id="5b354-139">Donnant action au regard de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="5b354-139">Giving action to the user's gaze</span></span>

<span data-ttu-id="5b354-140">Une fois que l’utilisateur a ciblé un hologramme ou un objet réel à l’aide de leurs regards, leur étape suivante consiste à prendre des mesures sur cet objet.</span><span class="sxs-lookup"><span data-stu-id="5b354-140">Once the user has targeted a hologram or real-world object using their gaze, their next step is to take action on that object.</span></span> <span data-ttu-id="5b354-141">Les méthodes principales pour un utilisateur de prendre des mesures sont effectuent via [mouvements](gestures.md), [contrôleurs de mouvement](motion-controllers.md) et [voix](voice-input.md).</span><span class="sxs-lookup"><span data-stu-id="5b354-141">The primary ways for a user to take action are through [gestures](gestures.md), [motion controllers](motion-controllers.md) and [voice](voice-input.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5b354-142">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5b354-142">See also</span></span>
* [<span data-ttu-id="5b354-143">Réalité mixte - Entrées - Cours 210 : Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="5b354-143">MR Input 210: Gaze</span></span>](holograms-210.md)
* [<span data-ttu-id="5b354-144">HEAD et surveillez les regards dans DirectX</span><span class="sxs-lookup"><span data-stu-id="5b354-144">Head and eye gaze in DirectX</span></span>](gaze-in-directx.md)
* [<span data-ttu-id="5b354-145">Pointage du regard dans Unity</span><span class="sxs-lookup"><span data-stu-id="5b354-145">Gaze in Unity</span></span>](gaze-in-unity.md)
