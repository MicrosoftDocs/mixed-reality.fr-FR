---
title: Optimisation de votre application pour mains libres
description: Optimisation de votre application pour mains libres
author: liamar
ms.author: liamar
ms.date: 04/20/2019
ms.topic: article
keywords: Une réalité mixte, mains libres, utilisation, utilisation de ciblage, interaction, conception
ms.openlocfilehash: f39a9524831161997b59be6cf89b124fa5b29c78
ms.sourcegitcommit: d6d96d552ec10cd7e6502fbbc1905432e2878325
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/10/2019
ms.locfileid: "65524327"
---
# <a name="optimizing-your-app-for-hands-free"></a><span data-ttu-id="88838-104">Optimisation de votre application pour mains libres</span><span class="sxs-lookup"><span data-stu-id="88838-104">Optimizing your app for hands-free</span></span>



## <a name="scenarios"></a><span data-ttu-id="88838-105">Scénarios</span><span class="sxs-lookup"><span data-stu-id="88838-105">Scenarios</span></span>

<span data-ttu-id="88838-106">Comme indiqué dans le [vue d’ensemble du modèle d’interaction](interaction-fundamentals.md), une fois que vous avez identifié les utilisateurs et leurs objectifs, demandez-vous quel environnementales ou connaissance défis liés peut qu’ils testent pour accomplir leurs tâches.</span><span class="sxs-lookup"><span data-stu-id="88838-106">As outlined in the [interaction model overview](interaction-fundamentals.md), once you have identified the users and their goals, ask yourself what environmental or situational challenges they might face as they work to accomplish their tasks.</span></span> <span data-ttu-id="88838-107">Par exemple, les nombreux utilisateurs ont besoin d’utiliser les mains à atteindre leurs objectifs réalistes et avoir des difficultés à interagir avec une interface en mains et contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="88838-107">For example, many users need to use their hands to accomplish their real-world goals and will have difficulty interacting with a hands-and-controllers based interface.</span></span> 

<span data-ttu-id="88838-108">Certains scénarios spécifiques peuvent être :</span><span class="sxs-lookup"><span data-stu-id="88838-108">Some specific scenarios might be:</span></span> 
* <span data-ttu-id="88838-109">Être guidés dans une tâche, tandis que les mains sont occupés</span><span class="sxs-lookup"><span data-stu-id="88838-109">Being guided through a task, while hands are busy</span></span>
* <span data-ttu-id="88838-110">Faisant référence à des documents tandis que vos mains sont occupés</span><span class="sxs-lookup"><span data-stu-id="88838-110">Referencing materials while your hands are busy</span></span>
* <span data-ttu-id="88838-111">Fatigue de main</span><span class="sxs-lookup"><span data-stu-id="88838-111">Hand fatigue</span></span>
* <span data-ttu-id="88838-112">Gants qui ne peut pas être suivis.</span><span class="sxs-lookup"><span data-stu-id="88838-112">Gloves that can't be tracked</span></span>
* <span data-ttu-id="88838-113">Exécution d’un élément</span><span class="sxs-lookup"><span data-stu-id="88838-113">Carrying something</span></span>


## <a name="hands-free-modalities"></a><span data-ttu-id="88838-114">Modalités de mains libres</span><span class="sxs-lookup"><span data-stu-id="88838-114">Hands-free modalities</span></span>

### <a name="voice-commanding"></a><span data-ttu-id="88838-115">Exécution des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="88838-115">Voice commanding</span></span>

<span data-ttu-id="88838-116">À l’aide de votre voix à la commande et de contrôle de qu'une interface peut non seulement autoriser l’utilisateur à mains libres de fonctionner, mais également ignorer plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="88838-116">Using your voice to command and control an interface can not only allow the user to operate handsfree, but also skip multiple steps.</span></span> <span data-ttu-id="88838-117">L’utilisation de cette modalité peut varier de permettre à l’utilisateur en lisant simplement les nom de n’importe quel bouton audio pour l’activer, comme dans Voir-it-say-it, à converser avec un agent qui peut effectuer des tâches pour vous.</span><span class="sxs-lookup"><span data-stu-id="88838-117">The usage of this modality can range from allowing the user to simply reading any button's name out loud to activate it, as in See-it-say-it, to conversing with an agent who can accomplish tasks for you.</span></span>

* [<span data-ttu-id="88838-118">Conception de la voix</span><span class="sxs-lookup"><span data-stu-id="88838-118">Voice design</span></span>](voice-design.md)


### <a name="head-gaze-and-dwell"></a><span data-ttu-id="88838-119">Regards de tête et de balayage</span><span class="sxs-lookup"><span data-stu-id="88838-119">Head gaze and dwell</span></span>

<span data-ttu-id="88838-120">Dans certaines situations mains-libres, en utilisant votre voix n’est pas idéale ou même possible.</span><span class="sxs-lookup"><span data-stu-id="88838-120">In some hands-free situations, using your voice is not ideal or even possible.</span></span> <span data-ttu-id="88838-121">Environnements d’usine forte, confidentialité ou normes sociaux peuvent tous être des contraintes.</span><span class="sxs-lookup"><span data-stu-id="88838-121">Loud factory environments, privacy, or social norms can all be constraints.</span></span> <span data-ttu-id="88838-122">Utilisation de la tête + m’attarderai pas modèle permet à l’utilisateur à naviguer de l’application à l’aide de leur vecteur principal pour qu’il pointe, tout en attente, ou logement sur un bouton s’activer après un certain laps de temps (généralement environ 1 seconde ou ainsi).</span><span class="sxs-lookup"><span data-stu-id="88838-122">The head gaze + dwell model allows the user to navigate the app by using their head vector to point, while lingering, or dwelling on a button will activate it after a certain amount of time (typically around 1 second or so).</span></span> 

* [<span data-ttu-id="88838-123">Pointer du regard et fixer</span><span class="sxs-lookup"><span data-stu-id="88838-123">Gaze and dwell</span></span>](gaze-and-dwell.md)

## <a name="transitioning-in-and-out-of-hands-free"></a><span data-ttu-id="88838-124">Transition vers et depuis mains libres</span><span class="sxs-lookup"><span data-stu-id="88838-124">Transitioning in and out of hands-free</span></span>

<span data-ttu-id="88838-125">Pour ces scénarios, la libération vos mains d’interagir avec hologrammes pour la navigation et d’exécution des commandes peut aller d’une exigence absolue jusqu'à l’exploitation de l’application,-bout, à l’utilisateur peut effectuer la transition et se déconnecte d’à tout moment d’une fonctionnalité supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="88838-125">For these scenarios, freeing your hands from interacting with holograms for commanding and navigation can range from being an absolute requirement to operating the app, end-to-end, to an added convenience that the user can transition in and out of at any time.</span></span> 

<span data-ttu-id="88838-126">Si la configuration requise de l’application est qu’il sera toujours utilisé mains-libres, en utilisant la durée d’affichage, les commandes vocales ou les commandes vocales unique, « select », puis veillez à l’hébergement approprié dans votre interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="88838-126">If the requirement of the app is that it will always be used hands-free, whether by using dwell, voice commands, or the single voice command, "select", then make sure to make the appropriate accomodations in your UI.</span></span> 

<span data-ttu-id="88838-127">Si votre utilisateur cible doit être en mesure de passer de mains à mains libres à leur discrétion, il est important de tenir compte de ces principes :</span><span class="sxs-lookup"><span data-stu-id="88838-127">If your target user needs to be able to switch from hands to hands-free at their discretion, then it is important to take these principles into account:</span></span>

### <a name="assume-the-user-is-already-in-the-mode-that-they-want-to-switch-to"></a><span data-ttu-id="88838-128">Supposons que l’utilisateur est déjà dans le mode qu’ils souhaitent pour basculer vers</span><span class="sxs-lookup"><span data-stu-id="88838-128">Assume the user is already in the mode that they want to switch to</span></span>
<span data-ttu-id="88838-129">Par exemple, si votre utilisateur est en usine, regarder une vidéo référence sur son Hololens et décide de récupérer une clé pour commencer à utiliser, elle très probablement souhaite commencer à travailler dans les mains libres sans avoir à placer la clé d’appuyer sur un bouton vers le bas.</span><span class="sxs-lookup"><span data-stu-id="88838-129">For instance, if your user is on the factory floor, watching a video reference on her Hololens, and decides to pick up a wrench to start working, she most likely would like to begin working in handsfree without having to put down the wrench to press a button.</span></span> <span data-ttu-id="88838-130">Elle doit être en mesure d’appeler une session vocale avec une commande de voix, m’attarderai pas sur l’interface utilisateur déjà visible pour commencer à durée d’affichage, ou que le mot « select ».</span><span class="sxs-lookup"><span data-stu-id="88838-130">She should be able to invoke a voice session with a voice command, dwell on already-visible UI to begin dwell, or say the word "select".</span></span>

<span data-ttu-id="88838-131">L’utilisateur doit avoir la possibilité de :</span><span class="sxs-lookup"><span data-stu-id="88838-131">The user should have the ability to:</span></span> 
* <span data-ttu-id="88838-132">Basculez vers mains libres tout en mains libres</span><span class="sxs-lookup"><span data-stu-id="88838-132">Switch to handsfree while handsfree</span></span>
* <span data-ttu-id="88838-133">Basculez vers entre les mains avec vos mains</span><span class="sxs-lookup"><span data-stu-id="88838-133">Switch to hands with your hands</span></span>
* <span data-ttu-id="88838-134">Basculez vers le contrôleur à l’aide d’un contrôleur</span><span class="sxs-lookup"><span data-stu-id="88838-134">Switch to the controller using a controller</span></span> 

### <a name="create-redundant-ways-to-switch-modes"></a><span data-ttu-id="88838-135">Créer pour basculer entre les modes redondant</span><span class="sxs-lookup"><span data-stu-id="88838-135">Create redundant ways to switch modes</span></span>
<span data-ttu-id="88838-136">Bien que le premier principe soit sur l’accès, le second est sur la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="88838-136">While the first principle is about access, the second one is about availability.</span></span> <span data-ttu-id="88838-137">Il ne doit pas simplement être un moyen simple pour la transition vers et depuis un mode.</span><span class="sxs-lookup"><span data-stu-id="88838-137">There should not just be a single way to transition in and out of a mode.</span></span> 

<span data-ttu-id="88838-138">Il peut s’agir :</span><span class="sxs-lookup"><span data-stu-id="88838-138">Some examples would be:</span></span> 
* <span data-ttu-id="88838-139">Un bouton pour lancer des interactions vocales</span><span class="sxs-lookup"><span data-stu-id="88838-139">A button to begin voice interactions</span></span>
* <span data-ttu-id="88838-140">Une commande de la voix pour effectuer la transition à l’utilisation du pointage de regard + durée d’affichage</span><span class="sxs-lookup"><span data-stu-id="88838-140">A voice command to transition to using gaze + dwell</span></span>

### <a name="add-a-dash-of-drama"></a><span data-ttu-id="88838-141">Ajoutez un peu de pièces de théâtre</span><span class="sxs-lookup"><span data-stu-id="88838-141">Add a dash of drama</span></span>
<span data-ttu-id="88838-142">Un commutateur de mode n’est pas anodin, il est important que lorsque ces transitions se produisent, qu’ils soient un commutateur explicit, même considérable, pour informer l’utilisateur que s’est-il passé.</span><span class="sxs-lookup"><span data-stu-id="88838-142">A mode switch is a big deal -- it is important that when these transitions happen, that they be an explicit, even dramatic switch, to let the user know what happened.</span></span> 


## <a name="usability-checklist"></a><span data-ttu-id="88838-143">Liste de vérification de facilité d’utilisation</span><span class="sxs-lookup"><span data-stu-id="88838-143">Usability checklist</span></span>

<span data-ttu-id="88838-144">**L’utilisateur peut faire de tout et rien mains-libres, end-to-end ?**</span><span class="sxs-lookup"><span data-stu-id="88838-144">**Can the user do everything and anything hands-free, end-to-end?**</span></span>
* <span data-ttu-id="88838-145">Chaque interactible doivent être accessibles mains libres</span><span class="sxs-lookup"><span data-stu-id="88838-145">Every interactible should be accessible hands-free</span></span>
* <span data-ttu-id="88838-146">Vérifiez qu’il existe un remplacement pour tous les mouvements personnalisés, tels que redimensionnement, de placement, où les balayages, robinets, etc.</span><span class="sxs-lookup"><span data-stu-id="88838-146">Ensure that there is a replacement for all custom gestures, such as resizing, placing, swipes, taps, etc.</span></span>
* <span data-ttu-id="88838-147">Assurez-vous que l’utilisateur dispose du contrôle de certitude de la présence de l’interface utilisateur, de placement, de niveau de détail en permanence</span><span class="sxs-lookup"><span data-stu-id="88838-147">Ensure that the user has confident control of UI presence, placement, verbosity at all times</span></span>
    * <span data-ttu-id="88838-148">Obtention de l’interface utilisateur disparaître</span><span class="sxs-lookup"><span data-stu-id="88838-148">Getting UI out of the way</span></span>
    * <span data-ttu-id="88838-149">Adressage de l’interface utilisateur qui est en dehors du champ de vision (angle d’ouverture)</span><span class="sxs-lookup"><span data-stu-id="88838-149">Addressing UI that is out of field of view (FOV)</span></span>
    * <span data-ttu-id="88838-150">Combien je vois, où, quand</span><span class="sxs-lookup"><span data-stu-id="88838-150">How much I see, where, when</span></span>

<span data-ttu-id="88838-151">**Sont les mécanismes de l’interaction en cours dispensés et renforcés avec l’intuitivité droit ?**</span><span class="sxs-lookup"><span data-stu-id="88838-151">**Are the mechanics of the interaction being taught and reinforced with the right affordances?**</span></span>

<span data-ttu-id="88838-152">L’utilisateur comprend...</span><span class="sxs-lookup"><span data-stu-id="88838-152">Does the user understand ...</span></span>
* <span data-ttu-id="88838-153">... Quel mode ils compte-t-elle ?</span><span class="sxs-lookup"><span data-stu-id="88838-153">... What mode they are in?</span></span>
* <span data-ttu-id="88838-154">... Ce qu’ils peuvent faire dans ce mode ?</span><span class="sxs-lookup"><span data-stu-id="88838-154">... What they can do in this mode?</span></span>
* <span data-ttu-id="88838-155">... Quel est l’état actuel ?</span><span class="sxs-lookup"><span data-stu-id="88838-155">... What is the current state?</span></span>
* <span data-ttu-id="88838-156">... Comment ils peuvent transition sortante ?</span><span class="sxs-lookup"><span data-stu-id="88838-156">... How they can transition out?</span></span>
    
<span data-ttu-id="88838-157">**L’interface utilisateur optimisée pour mains libres ?**</span><span class="sxs-lookup"><span data-stu-id="88838-157">**Is the UI optimized for hands-free?**</span></span>   

* <span data-ttu-id="88838-158">Exemple :</span><span class="sxs-lookup"><span data-stu-id="88838-158">Ex.</span></span> <span data-ttu-id="88838-159">Balayage intuitivité n’est pas intégrées aux modèles 2D standard</span><span class="sxs-lookup"><span data-stu-id="88838-159">Dwell affordances are not built-in to typical 2D patterns</span></span>
* <span data-ttu-id="88838-160">Exemple :</span><span class="sxs-lookup"><span data-stu-id="88838-160">Ex.</span></span> <span data-ttu-id="88838-161">Ciblage de la voix est préférable avec mise en surbrillance de l’objet</span><span class="sxs-lookup"><span data-stu-id="88838-161">Voice targeting is better with object highlighting</span></span>
* <span data-ttu-id="88838-162">Exemple :</span><span class="sxs-lookup"><span data-stu-id="88838-162">Ex.</span></span> <span data-ttu-id="88838-163">Interactions vocales sont meilleures avec des légendes qui doivent être mis sous tension</span><span class="sxs-lookup"><span data-stu-id="88838-163">Voice interactions are better with captions that have to be turned on</span></span>


## <a name="see-also"></a><span data-ttu-id="88838-164">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="88838-164">See also</span></span>
* [<span data-ttu-id="88838-165">Pointer du regard vers l’avant et valider</span><span class="sxs-lookup"><span data-stu-id="88838-165">Head-gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="88838-166">Manipulation directe</span><span class="sxs-lookup"><span data-stu-id="88838-166">Direct manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="88838-167">Pointer et valider</span><span class="sxs-lookup"><span data-stu-id="88838-167">Point and commit</span></span>](point-and-commit.md)
