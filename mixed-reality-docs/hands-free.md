---
title: Mains-libres
description: Optimisation de votre application pour des mains libres
author: liamar
ms.author: liamar
ms.date: 04/20/2019
ms.topic: article
keywords: La réalité mixte, mains libres, point d’interposition, le regard, l’interaction et la conception
ms.openlocfilehash: 7942192f644a7133335f089cfaaccfaebdd9292e
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414395"
---
# <a name="hands-free"></a><span data-ttu-id="affd3-104">Mains-libres</span><span class="sxs-lookup"><span data-stu-id="affd3-104">Hands-free</span></span>



## <a name="scenarios"></a><span data-ttu-id="affd3-105">Scénarios</span><span class="sxs-lookup"><span data-stu-id="affd3-105">Scenarios</span></span>

<span data-ttu-id="affd3-106">Comme indiqué dans la [vue d’ensemble du modèle d’interaction](interaction-fundamentals.md), une fois que vous avez identifié les utilisateurs et leurs objectifs, posez-vous les difficultés environnementales ou de situation auxquelles ils peuvent faire face lorsqu’ils travaillent pour accomplir leurs tâches.</span><span class="sxs-lookup"><span data-stu-id="affd3-106">As outlined in the [Interaction model overview](interaction-fundamentals.md), once you have identified the users and their goals, ask yourself what environmental or situational challenges they might face as they work to accomplish their tasks.</span></span> <span data-ttu-id="affd3-107">Par exemple, de nombreux utilisateurs ont besoin d’utiliser leurs mains pour atteindre leurs objectifs réels, et auront des difficultés à interagir avec une interface basée sur les mains et les contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="affd3-107">For example, many users need to use their hands to accomplish their real-world goals, and will have difficulty interacting with a hands-and-controllers based interface.</span></span> 

<span data-ttu-id="affd3-108">Certains scénarios spécifiques peuvent être:</span><span class="sxs-lookup"><span data-stu-id="affd3-108">Some specific scenarios might be:</span></span> 
* <span data-ttu-id="affd3-109">Guidée par le biais d’une tâche, tandis que les mains sont occupées</span><span class="sxs-lookup"><span data-stu-id="affd3-109">Being guided through a task, while hands are busy</span></span>
* <span data-ttu-id="affd3-110">Référencement des matériaux lorsque vos mains sont occupées</span><span class="sxs-lookup"><span data-stu-id="affd3-110">Referencing materials while your hands are busy</span></span>
* <span data-ttu-id="affd3-111">Fatigue de main</span><span class="sxs-lookup"><span data-stu-id="affd3-111">Hand fatigue</span></span>
* <span data-ttu-id="affd3-112">Gants qui ne peuvent pas être suivis</span><span class="sxs-lookup"><span data-stu-id="affd3-112">Gloves that can't be tracked</span></span>
* <span data-ttu-id="affd3-113">Transporter un événement</span><span class="sxs-lookup"><span data-stu-id="affd3-113">Carrying something</span></span>


## <a name="hands-free-modalities"></a><span data-ttu-id="affd3-114">Modalités des mains libres</span><span class="sxs-lookup"><span data-stu-id="affd3-114">Hands-free modalities</span></span>

### <a name="voice-commandingvoice-designmd"></a>[<span data-ttu-id="affd3-115">Commander avec la voix</span><span class="sxs-lookup"><span data-stu-id="affd3-115">Voice commanding</span></span>](voice-design.md)

<span data-ttu-id="affd3-116">L’utilisation de votre voix pour commander et contrôler une interface peut non seulement permettre à l’utilisateur d’utiliser Handsfree, mais également passer plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="affd3-116">Using your voice to command and control an interface can not only allow the user to operate handsfree, but also skip multiple steps.</span></span> <span data-ttu-id="affd3-117">L’utilisation de cette modalité peut aller de permettre à l’utilisateur de simplement lire le nom du bouton à haute voix pour l’activer, comme c’est le cas dans la section Voir-le-dit-IT, pour converser avec un agent qui peut accomplir des tâches pour vous.</span><span class="sxs-lookup"><span data-stu-id="affd3-117">The usage of this modality can range from allowing the user to simply read any button's name out loud to activate it, as in See-it-say-it, to conversing with an agent who can accomplish tasks for you.</span></span>



### <a name="head-gaze-and-dwellgaze-and-dwellmd"></a>[<span data-ttu-id="affd3-118">Suivre de la tête et stabiliser</span><span class="sxs-lookup"><span data-stu-id="affd3-118">Head-gaze and dwell</span></span>](gaze-and-dwell.md)

<span data-ttu-id="affd3-119">Dans certaines situations mains libres, l’utilisation de votre voix n’est pas idéale, voire possible.</span><span class="sxs-lookup"><span data-stu-id="affd3-119">In some hands-free situations, using your voice is not ideal or even possible.</span></span> <span data-ttu-id="affd3-120">Les environnements en usine bruyants, la confidentialité ou les normes sociales peuvent être des contraintes.</span><span class="sxs-lookup"><span data-stu-id="affd3-120">Loud factory environments, privacy, or social norms can all be constraints.</span></span> <span data-ttu-id="affd3-121">Le modèle de point de vue du point de vue de la tête permet à l’utilisateur de parcourir l’application à l’aide de son vecteur d’en-tête pour pointer, tout en étant en attente ou le logement sur un bouton, l’active après un certain laps de temps, en général environ 1 seconde.</span><span class="sxs-lookup"><span data-stu-id="affd3-121">The head gaze + dwell model allows the user to navigate the app by using their head vector to point, while lingering, or dwelling on a button will activate it after a certain amount of time, typically around 1 second or so.</span></span> 


## <a name="transitioning-in-and-out-of-hands-free"></a><span data-ttu-id="affd3-122">Transition vers et à l’extérieur des mains libres</span><span class="sxs-lookup"><span data-stu-id="affd3-122">Transitioning in and out of hands-free</span></span>

<span data-ttu-id="affd3-123">Pour ces scénarios, le fait de libérer des mains de l’interaction avec les hologrammes pour les commandes et la navigation peut aller de l’exigence absolue à l’exploitation de l’application, de bout en bout, à un confort supplémentaire que l’utilisateur peut passer dans simultanément.</span><span class="sxs-lookup"><span data-stu-id="affd3-123">For these scenarios, freeing your hands from interacting with holograms for commanding and navigation can range from being an absolute requirement to operating the application, end-to-end, to an added convenience that the user can transition in and out of at any time.</span></span> 

<span data-ttu-id="affd3-124">Si la spécification de l’application est qu’elle sera toujours utilisée librement, que ce soit à l’aide de son, de commandes vocales ou de la commande vocale unique, «Select», veillez à créer les logements appropriés dans votre interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="affd3-124">If the requirement of the application is that it will always be used hands-free, whether by using dwell, voice commands, or the single voice command, "select", then make sure to make the appropriate accomodations in your UI.</span></span> 

<span data-ttu-id="affd3-125">Si votre utilisateur cible doit être en mesure de passer d’un mains à l’autre mains libres à sa discrétion, il est important de prendre en compte les principes suivants.</span><span class="sxs-lookup"><span data-stu-id="affd3-125">If your target user needs to be able to switch from hands to hands-free at their discretion, then it is important to take the following principles into account.</span></span>

### <a name="assume-the-user-is-already-in-the-mode-that-they-want-to-switch-to"></a><span data-ttu-id="affd3-126">Supposons que l’utilisateur est déjà dans le mode vers lequel il souhaite passer</span><span class="sxs-lookup"><span data-stu-id="affd3-126">Assume the user is already in the mode that they want to switch to</span></span>
<span data-ttu-id="affd3-127">Par exemple, si l’utilisateur se trouve en usine, regarde une référence vidéo sur son Hololens et décide de sélectionner une clé pour commencer à travailler, elle commence probablement à travailler dans Handsfree sans avoir à appuyer sur un bouton.</span><span class="sxs-lookup"><span data-stu-id="affd3-127">For instance, if the user is on the factory floor, watching a video reference on her Hololens, and decides to pick up a wrench to start working, she most likely would start working in handsfree without having to put down the wrench to press a button.</span></span> <span data-ttu-id="affd3-128">Elle doit être en mesure d’appeler une session vocale avec une commande vocale, son logement sur une interface utilisateur déjà visible pour commencer son logement ou le mot «Select».</span><span class="sxs-lookup"><span data-stu-id="affd3-128">She should be able to invoke a voice session with a voice command, dwell on an already-visible UI to begin dwell, or say the word "select".</span></span>

<span data-ttu-id="affd3-129">L’utilisateur doit avoir la possibilité d’effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="affd3-129">The user should have the ability to:</span></span> 
* <span data-ttu-id="affd3-130">Passez à l’option mains libres pendant les mains libres</span><span class="sxs-lookup"><span data-stu-id="affd3-130">Switch to hands-free while hands-free</span></span>
* <span data-ttu-id="affd3-131">Passez aux mains avec vos mains</span><span class="sxs-lookup"><span data-stu-id="affd3-131">Switch to hands with your hands</span></span>
* <span data-ttu-id="affd3-132">Basculer vers le contrôleur à l’aide d’un contrôleur</span><span class="sxs-lookup"><span data-stu-id="affd3-132">Switch to the controller using a controller</span></span> 

### <a name="create-redundant-ways-to-switch-modes"></a><span data-ttu-id="affd3-133">Créer des méthodes redondantes pour basculer entre les modes</span><span class="sxs-lookup"><span data-stu-id="affd3-133">Create redundant ways to switch modes</span></span>
<span data-ttu-id="affd3-134">Tandis que le premier principe concerne l’accès, la seconde concerne la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="affd3-134">While the first principle is about access, the second one is about availability.</span></span> <span data-ttu-id="affd3-135">Il ne doit pas s’agir simplement d’un moyen unique de transition vers et à partir d’un mode.</span><span class="sxs-lookup"><span data-stu-id="affd3-135">There should not just be a single way to transition in and out of a mode.</span></span> 

<span data-ttu-id="affd3-136">Voici quelques exemples:</span><span class="sxs-lookup"><span data-stu-id="affd3-136">Some examples would be:</span></span> 
* <span data-ttu-id="affd3-137">Un bouton pour commencer les interactions vocales</span><span class="sxs-lookup"><span data-stu-id="affd3-137">A button to begin voice interactions</span></span>
* <span data-ttu-id="affd3-138">Commande vocale à utiliser pour la transition en utilisant le point de vue du regard</span><span class="sxs-lookup"><span data-stu-id="affd3-138">A voice command to transition to using gaze + dwell</span></span>

### <a name="add-a-dash-of-drama"></a><span data-ttu-id="affd3-139">Ajouter un tiret de la fiction</span><span class="sxs-lookup"><span data-stu-id="affd3-139">Add a dash of drama</span></span>
<span data-ttu-id="affd3-140">Un changement de mode est un facteur important: il est important que lorsque ces transitions se produisent, il s’agit d’un commutateur explicite, même spectaculaire, pour permettre à l’utilisateur de savoir ce qui s’est passé.</span><span class="sxs-lookup"><span data-stu-id="affd3-140">A mode switch is a big deal--it is important that when these transitions happen that they be an explicit, even dramatic switch, to let the user know what happened.</span></span> 


## <a name="usability-checklist"></a><span data-ttu-id="affd3-141">Liste de vérification de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="affd3-141">Usability checklist</span></span>

<span data-ttu-id="affd3-142">**L’utilisateur peut-il faire tout et tout ce qui est mains libres, de bout en bout?**</span><span class="sxs-lookup"><span data-stu-id="affd3-142">**Can the user do everything and anything hands-free, end-to-end?**</span></span>
* <span data-ttu-id="affd3-143">Chaque interactible doit être accessible mains libres</span><span class="sxs-lookup"><span data-stu-id="affd3-143">Every interactible should be accessible hands-free</span></span>
* <span data-ttu-id="affd3-144">Assurez-vous qu’il existe un remplacement de tous les mouvements personnalisés, tels que le redimensionnement, le placement, les balayages, les robinets, etc.</span><span class="sxs-lookup"><span data-stu-id="affd3-144">Ensure that there is a replacement for all custom gestures, such as resizing, placing, swipes, taps, etc.</span></span>
* <span data-ttu-id="affd3-145">S’assurer que l’utilisateur a le contrôle assuré de la présence, de l’emplacement et des commentaires de l’interface utilisateur à tout moment</span><span class="sxs-lookup"><span data-stu-id="affd3-145">Ensure that the user has confident control of UI presence, placement, and verbosity at all times</span></span>
    * <span data-ttu-id="affd3-146">Récupération de l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="affd3-146">Getting UI out of the way</span></span>
    * <span data-ttu-id="affd3-147">Adressage de l’interface utilisateur en dehors de l’affichage (angle de vue)</span><span class="sxs-lookup"><span data-stu-id="affd3-147">Addressing UI that is out of field of view (FOV)</span></span>
    * <span data-ttu-id="affd3-148">Combien je vois, où, quand</span><span class="sxs-lookup"><span data-stu-id="affd3-148">How much I see, where, when</span></span>

<span data-ttu-id="affd3-149">**Les mécanismes de l’interaction sont-ils enseignés et armés avec le bon intuitivité?**</span><span class="sxs-lookup"><span data-stu-id="affd3-149">**Are the mechanics of the interaction being taught and reinforced with the right affordances?**</span></span>

<span data-ttu-id="affd3-150">L’utilisateur a-t-il compris...</span><span class="sxs-lookup"><span data-stu-id="affd3-150">Does the user understand ...</span></span>
* <span data-ttu-id="affd3-151">... Dans quel mode ils se trouvent-ils?</span><span class="sxs-lookup"><span data-stu-id="affd3-151">... What mode they are in?</span></span>
* <span data-ttu-id="affd3-152">... Qu’est-ce qu’il est possible de faire dans ce mode?</span><span class="sxs-lookup"><span data-stu-id="affd3-152">... What they can do in this mode?</span></span>
* <span data-ttu-id="affd3-153">... Quel est l’état actuel?</span><span class="sxs-lookup"><span data-stu-id="affd3-153">... What is the current state?</span></span>
* <span data-ttu-id="affd3-154">... Comment elles peuvent être transférées?</span><span class="sxs-lookup"><span data-stu-id="affd3-154">... How they can transition out?</span></span>
    
<span data-ttu-id="affd3-155">**L’interface utilisateur est-elle optimisée pour les mains libres?**</span><span class="sxs-lookup"><span data-stu-id="affd3-155">**Is the UI optimized for hands-free?**</span></span>   

* <span data-ttu-id="affd3-156">Exemple : Les intuitivités de logement ne sont pas intégrés aux modèles 2D typiques</span><span class="sxs-lookup"><span data-stu-id="affd3-156">Example: Dwell affordances are not built-in to typical 2D patterns</span></span>
* <span data-ttu-id="affd3-157">Exemple : Le ciblage vocal est mieux adapté à la mise en surbrillance des objets</span><span class="sxs-lookup"><span data-stu-id="affd3-157">Example: Voice targeting is better with object highlighting</span></span>
* <span data-ttu-id="affd3-158">Exemple : Les interactions vocales sont mieux adaptées aux légendes qui doivent être activées</span><span class="sxs-lookup"><span data-stu-id="affd3-158">Example: Voice interactions are better with captions that have to be turned on</span></span>


## <a name="see-also"></a><span data-ttu-id="affd3-159">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="affd3-159">See also</span></span>
* [<span data-ttu-id="affd3-160">Suivre de la tête et valider</span><span class="sxs-lookup"><span data-stu-id="affd3-160">Head-gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="affd3-161">Manipulation directe avec les mains</span><span class="sxs-lookup"><span data-stu-id="affd3-161">Direct manipulation with hands</span></span>](direct-manipulation.md)
* [<span data-ttu-id="affd3-162">Pointer et valider avec les mains</span><span class="sxs-lookup"><span data-stu-id="affd3-162">Point and commit with hands</span></span>](point-and-commit.md)
