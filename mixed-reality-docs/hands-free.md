---
title: Mains-libres
description: Optimisation de votre application pour mains libres
author: liamar
ms.author: liamar
ms.date: 04/20/2019
ms.topic: article
keywords: Une réalité mixte, mains libres, utilisation, utilisation de ciblage, interaction, conception
ms.openlocfilehash: 59a460a0c46ace7e633381019d29af54b1061695
ms.sourcegitcommit: 45676da11ebe33a2aa3dccec0e8ad7d714420853
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65629020"
---
# <a name="hands-free"></a><span data-ttu-id="e57ea-104">Mains-libres</span><span class="sxs-lookup"><span data-stu-id="e57ea-104">Hands-free</span></span>



## <a name="scenarios"></a><span data-ttu-id="e57ea-105">Scénarios</span><span class="sxs-lookup"><span data-stu-id="e57ea-105">Scenarios</span></span>

<span data-ttu-id="e57ea-106">Comme indiqué dans le [vue d’ensemble du modèle d’interaction](interaction-fundamentals.md), une fois que vous avez identifié les utilisateurs et leurs objectifs, demandez-vous quel environnementales ou connaissance défis liés peut qu’ils testent pour accomplir leurs tâches.</span><span class="sxs-lookup"><span data-stu-id="e57ea-106">As outlined in the [interaction model overview](interaction-fundamentals.md), once you have identified the users and their goals, ask yourself what environmental or situational challenges they might face as they work to accomplish their tasks.</span></span> <span data-ttu-id="e57ea-107">Par exemple, les nombreux utilisateurs ont besoin d’utiliser les mains à atteindre leurs objectifs réalistes et avoir des difficultés à interagir avec une interface en mains et contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="e57ea-107">For example, many users need to use their hands to accomplish their real-world goals and will have difficulty interacting with a hands-and-controllers based interface.</span></span> 

<span data-ttu-id="e57ea-108">Certains scénarios spécifiques peuvent être :</span><span class="sxs-lookup"><span data-stu-id="e57ea-108">Some specific scenarios might be:</span></span> 
* <span data-ttu-id="e57ea-109">Être guidés dans une tâche, tandis que les mains sont occupés</span><span class="sxs-lookup"><span data-stu-id="e57ea-109">Being guided through a task, while hands are busy</span></span>
* <span data-ttu-id="e57ea-110">Faisant référence à des documents tandis que vos mains sont occupés</span><span class="sxs-lookup"><span data-stu-id="e57ea-110">Referencing materials while your hands are busy</span></span>
* <span data-ttu-id="e57ea-111">Fatigue de main</span><span class="sxs-lookup"><span data-stu-id="e57ea-111">Hand fatigue</span></span>
* <span data-ttu-id="e57ea-112">Gants qui ne peut pas être suivis.</span><span class="sxs-lookup"><span data-stu-id="e57ea-112">Gloves that can't be tracked</span></span>
* <span data-ttu-id="e57ea-113">Exécution d’un élément</span><span class="sxs-lookup"><span data-stu-id="e57ea-113">Carrying something</span></span>


## <a name="hands-free-modalities"></a><span data-ttu-id="e57ea-114">Modalités de mains libres</span><span class="sxs-lookup"><span data-stu-id="e57ea-114">Hands-free modalities</span></span>

### <a name="voice-commandingvoice-designmd"></a>[<span data-ttu-id="e57ea-115">Exécution des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="e57ea-115">Voice commanding</span></span>](voice-design.md)

<span data-ttu-id="e57ea-116">À l’aide de votre voix à la commande et de contrôle de qu'une interface peut non seulement autoriser l’utilisateur à mains libres de fonctionner, mais également ignorer plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="e57ea-116">Using your voice to command and control an interface can not only allow the user to operate handsfree, but also skip multiple steps.</span></span> <span data-ttu-id="e57ea-117">L’utilisation de cette modalité peut varier de permettre à l’utilisateur en lisant simplement les nom de n’importe quel bouton audio pour l’activer, comme dans Voir-it-say-it, à converser avec un agent qui peut effectuer des tâches pour vous.</span><span class="sxs-lookup"><span data-stu-id="e57ea-117">The usage of this modality can range from allowing the user to simply reading any button's name out loud to activate it, as in See-it-say-it, to conversing with an agent who can accomplish tasks for you.</span></span>



### <a name="head-gaze-and-dwellgaze-and-dwellmd"></a>[<span data-ttu-id="e57ea-118">Regards de tête et de balayage</span><span class="sxs-lookup"><span data-stu-id="e57ea-118">Head-gaze and dwell</span></span>](gaze-and-dwell.md)

<span data-ttu-id="e57ea-119">Dans certaines situations mains-libres, en utilisant votre voix n’est pas idéale ou même possible.</span><span class="sxs-lookup"><span data-stu-id="e57ea-119">In some hands-free situations, using your voice is not ideal or even possible.</span></span> <span data-ttu-id="e57ea-120">Environnements d’usine forte, confidentialité ou normes sociaux peuvent tous être des contraintes.</span><span class="sxs-lookup"><span data-stu-id="e57ea-120">Loud factory environments, privacy, or social norms can all be constraints.</span></span> <span data-ttu-id="e57ea-121">Utilisation de la tête + m’attarderai pas modèle permet à l’utilisateur à naviguer de l’application à l’aide de leur vecteur principal pour qu’il pointe, tout en attente, ou logement sur un bouton s’activer après un certain laps de temps (généralement environ 1 seconde ou ainsi).</span><span class="sxs-lookup"><span data-stu-id="e57ea-121">The head gaze + dwell model allows the user to navigate the app by using their head vector to point, while lingering, or dwelling on a button will activate it after a certain amount of time (typically around 1 second or so).</span></span> 


## <a name="transitioning-in-and-out-of-hands-free"></a><span data-ttu-id="e57ea-122">Transition vers et depuis mains libres</span><span class="sxs-lookup"><span data-stu-id="e57ea-122">Transitioning in and out of hands-free</span></span>

<span data-ttu-id="e57ea-123">Pour ces scénarios, la libération vos mains d’interagir avec hologrammes pour la navigation et d’exécution des commandes peut aller d’une exigence absolue jusqu'à l’exploitation de l’application,-bout, à l’utilisateur peut effectuer la transition et se déconnecte d’à tout moment d’une fonctionnalité supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="e57ea-123">For these scenarios, freeing your hands from interacting with holograms for commanding and navigation can range from being an absolute requirement to operating the app, end-to-end, to an added convenience that the user can transition in and out of at any time.</span></span> 

<span data-ttu-id="e57ea-124">Si la configuration requise de l’application est qu’il sera toujours utilisé mains-libres, en utilisant la durée d’affichage, les commandes vocales ou les commandes vocales unique, « select », puis veillez à l’hébergement approprié dans votre interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e57ea-124">If the requirement of the app is that it will always be used hands-free, whether by using dwell, voice commands, or the single voice command, "select", then make sure to make the appropriate accomodations in your UI.</span></span> 

<span data-ttu-id="e57ea-125">Si votre utilisateur cible doit être en mesure de passer de mains à mains libres à leur discrétion, il est important de tenir compte de ces principes :</span><span class="sxs-lookup"><span data-stu-id="e57ea-125">If your target user needs to be able to switch from hands to hands-free at their discretion, then it is important to take these principles into account:</span></span>

### <a name="assume-the-user-is-already-in-the-mode-that-they-want-to-switch-to"></a><span data-ttu-id="e57ea-126">Supposons que l’utilisateur est déjà dans le mode qu’ils souhaitent pour basculer vers</span><span class="sxs-lookup"><span data-stu-id="e57ea-126">Assume the user is already in the mode that they want to switch to</span></span>
<span data-ttu-id="e57ea-127">Par exemple, si votre utilisateur est en usine, regarder une vidéo référence sur son Hololens et décide de récupérer une clé pour commencer à utiliser, elle très probablement souhaite commencer à travailler dans les mains libres sans avoir à placer la clé d’appuyer sur un bouton vers le bas.</span><span class="sxs-lookup"><span data-stu-id="e57ea-127">For instance, if your user is on the factory floor, watching a video reference on her Hololens, and decides to pick up a wrench to start working, she most likely would like to begin working in handsfree without having to put down the wrench to press a button.</span></span> <span data-ttu-id="e57ea-128">Elle doit être en mesure d’appeler une session vocale avec une commande de voix, m’attarderai pas sur l’interface utilisateur déjà visible pour commencer à durée d’affichage, ou que le mot « select ».</span><span class="sxs-lookup"><span data-stu-id="e57ea-128">She should be able to invoke a voice session with a voice command, dwell on already-visible UI to begin dwell, or say the word "select".</span></span>

<span data-ttu-id="e57ea-129">L’utilisateur doit avoir la possibilité de :</span><span class="sxs-lookup"><span data-stu-id="e57ea-129">The user should have the ability to:</span></span> 
* <span data-ttu-id="e57ea-130">Basculez vers mains libres tout en mains libres</span><span class="sxs-lookup"><span data-stu-id="e57ea-130">Switch to handsfree while handsfree</span></span>
* <span data-ttu-id="e57ea-131">Basculez vers entre les mains avec vos mains</span><span class="sxs-lookup"><span data-stu-id="e57ea-131">Switch to hands with your hands</span></span>
* <span data-ttu-id="e57ea-132">Basculez vers le contrôleur à l’aide d’un contrôleur</span><span class="sxs-lookup"><span data-stu-id="e57ea-132">Switch to the controller using a controller</span></span> 

### <a name="create-redundant-ways-to-switch-modes"></a><span data-ttu-id="e57ea-133">Créer pour basculer entre les modes redondant</span><span class="sxs-lookup"><span data-stu-id="e57ea-133">Create redundant ways to switch modes</span></span>
<span data-ttu-id="e57ea-134">Bien que le premier principe soit sur l’accès, le second est sur la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e57ea-134">While the first principle is about access, the second one is about availability.</span></span> <span data-ttu-id="e57ea-135">Il ne doit pas simplement être un moyen simple pour la transition vers et depuis un mode.</span><span class="sxs-lookup"><span data-stu-id="e57ea-135">There should not just be a single way to transition in and out of a mode.</span></span> 

<span data-ttu-id="e57ea-136">Il peut s’agir :</span><span class="sxs-lookup"><span data-stu-id="e57ea-136">Some examples would be:</span></span> 
* <span data-ttu-id="e57ea-137">Un bouton pour lancer des interactions vocales</span><span class="sxs-lookup"><span data-stu-id="e57ea-137">A button to begin voice interactions</span></span>
* <span data-ttu-id="e57ea-138">Une commande de la voix pour effectuer la transition à l’utilisation du pointage de regard + durée d’affichage</span><span class="sxs-lookup"><span data-stu-id="e57ea-138">A voice command to transition to using gaze + dwell</span></span>

### <a name="add-a-dash-of-drama"></a><span data-ttu-id="e57ea-139">Ajoutez un peu de pièces de théâtre</span><span class="sxs-lookup"><span data-stu-id="e57ea-139">Add a dash of drama</span></span>
<span data-ttu-id="e57ea-140">Un commutateur de mode n’est pas anodin, il est important que lorsque ces transitions se produisent, qu’ils soient un commutateur explicit, même considérable, pour informer l’utilisateur que s’est-il passé.</span><span class="sxs-lookup"><span data-stu-id="e57ea-140">A mode switch is a big deal -- it is important that when these transitions happen, that they be an explicit, even dramatic switch, to let the user know what happened.</span></span> 


## <a name="usability-checklist"></a><span data-ttu-id="e57ea-141">Liste de vérification de facilité d’utilisation</span><span class="sxs-lookup"><span data-stu-id="e57ea-141">Usability checklist</span></span>

<span data-ttu-id="e57ea-142">**L’utilisateur peut faire de tout et rien mains-libres, end-to-end ?**</span><span class="sxs-lookup"><span data-stu-id="e57ea-142">**Can the user do everything and anything hands-free, end-to-end?**</span></span>
* <span data-ttu-id="e57ea-143">Chaque interactible doivent être accessibles mains libres</span><span class="sxs-lookup"><span data-stu-id="e57ea-143">Every interactible should be accessible hands-free</span></span>
* <span data-ttu-id="e57ea-144">Vérifiez qu’il existe un remplacement pour tous les mouvements personnalisés, tels que redimensionnement, de placement, où les balayages, robinets, etc.</span><span class="sxs-lookup"><span data-stu-id="e57ea-144">Ensure that there is a replacement for all custom gestures, such as resizing, placing, swipes, taps, etc.</span></span>
* <span data-ttu-id="e57ea-145">Assurez-vous que l’utilisateur dispose du contrôle de certitude de la présence de l’interface utilisateur, de placement, de niveau de détail en permanence</span><span class="sxs-lookup"><span data-stu-id="e57ea-145">Ensure that the user has confident control of UI presence, placement, verbosity at all times</span></span>
    * <span data-ttu-id="e57ea-146">Obtention de l’interface utilisateur disparaître</span><span class="sxs-lookup"><span data-stu-id="e57ea-146">Getting UI out of the way</span></span>
    * <span data-ttu-id="e57ea-147">Adressage de l’interface utilisateur qui est en dehors du champ de vision (angle d’ouverture)</span><span class="sxs-lookup"><span data-stu-id="e57ea-147">Addressing UI that is out of field of view (FOV)</span></span>
    * <span data-ttu-id="e57ea-148">Combien je vois, où, quand</span><span class="sxs-lookup"><span data-stu-id="e57ea-148">How much I see, where, when</span></span>

<span data-ttu-id="e57ea-149">**Sont les mécanismes de l’interaction en cours dispensés et renforcés avec l’intuitivité droit ?**</span><span class="sxs-lookup"><span data-stu-id="e57ea-149">**Are the mechanics of the interaction being taught and reinforced with the right affordances?**</span></span>

<span data-ttu-id="e57ea-150">L’utilisateur comprend...</span><span class="sxs-lookup"><span data-stu-id="e57ea-150">Does the user understand ...</span></span>
* <span data-ttu-id="e57ea-151">... Quel mode ils compte-t-elle ?</span><span class="sxs-lookup"><span data-stu-id="e57ea-151">... What mode they are in?</span></span>
* <span data-ttu-id="e57ea-152">... Ce qu’ils peuvent faire dans ce mode ?</span><span class="sxs-lookup"><span data-stu-id="e57ea-152">... What they can do in this mode?</span></span>
* <span data-ttu-id="e57ea-153">... Quel est l’état actuel ?</span><span class="sxs-lookup"><span data-stu-id="e57ea-153">... What is the current state?</span></span>
* <span data-ttu-id="e57ea-154">... Comment ils peuvent transition sortante ?</span><span class="sxs-lookup"><span data-stu-id="e57ea-154">... How they can transition out?</span></span>
    
<span data-ttu-id="e57ea-155">**L’interface utilisateur optimisée pour mains libres ?**</span><span class="sxs-lookup"><span data-stu-id="e57ea-155">**Is the UI optimized for hands-free?**</span></span>   

* <span data-ttu-id="e57ea-156">Exemple :</span><span class="sxs-lookup"><span data-stu-id="e57ea-156">Ex.</span></span> <span data-ttu-id="e57ea-157">Balayage intuitivité n’est pas intégrées aux modèles 2D standard</span><span class="sxs-lookup"><span data-stu-id="e57ea-157">Dwell affordances are not built-in to typical 2D patterns</span></span>
* <span data-ttu-id="e57ea-158">Exemple :</span><span class="sxs-lookup"><span data-stu-id="e57ea-158">Ex.</span></span> <span data-ttu-id="e57ea-159">Ciblage de la voix est préférable avec mise en surbrillance de l’objet</span><span class="sxs-lookup"><span data-stu-id="e57ea-159">Voice targeting is better with object highlighting</span></span>
* <span data-ttu-id="e57ea-160">Exemple :</span><span class="sxs-lookup"><span data-stu-id="e57ea-160">Ex.</span></span> <span data-ttu-id="e57ea-161">Interactions vocales sont meilleures avec des légendes qui doivent être mis sous tension</span><span class="sxs-lookup"><span data-stu-id="e57ea-161">Voice interactions are better with captions that have to be turned on</span></span>


## <a name="see-also"></a><span data-ttu-id="e57ea-162">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e57ea-162">See also</span></span>
* [<span data-ttu-id="e57ea-163">Pointer du regard vers l’avant et valider</span><span class="sxs-lookup"><span data-stu-id="e57ea-163">Head-gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="e57ea-164">Manipulation directe</span><span class="sxs-lookup"><span data-stu-id="e57ea-164">Direct manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="e57ea-165">Pointer et valider</span><span class="sxs-lookup"><span data-stu-id="e57ea-165">Point and commit</span></span>](point-and-commit.md)
