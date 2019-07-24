---
title: Étude de cas-3 interface utilisateur HoloStudio et apprentissage de la conception d’interaction
description: Apprentissage de la conception de l’interface utilisateur et des interactions HoloStudio
author: rwinj
ms.author: marcghal
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, HoloStudio, Windows Mixed Reality
ms.openlocfilehash: e01e2ea888398e9982b56fd95f90ef0731ec6bc2
ms.sourcegitcommit: c20563b8195c0c374a927b96708d958b127ffc8f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974827"
---
# <a name="case-study---3-holostudio-ui-and-interaction-design-learnings"></a><span data-ttu-id="9eb60-104">Étude de cas-3 interface utilisateur HoloStudio et apprentissage de la conception d’interaction</span><span class="sxs-lookup"><span data-stu-id="9eb60-104">Case study - 3 HoloStudio UI and interaction design learnings</span></span>

<span data-ttu-id="9eb60-105">[HoloStudio](https://www.youtube.com/watch?v=BRIJG0x_We8) était l’une des premières applications Microsoft pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9eb60-105">[HoloStudio](https://www.youtube.com/watch?v=BRIJG0x_We8) was one of the first Microsoft apps for HoloLens.</span></span> <span data-ttu-id="9eb60-106">Pour cette raison, nous avons dû créer de nouvelles pratiques pour l’interface utilisateur 3D et la conception d’interaction.</span><span class="sxs-lookup"><span data-stu-id="9eb60-106">Because of this, we had to create new best practices for 3D UI and interaction design.</span></span> <span data-ttu-id="9eb60-107">Nous l’avons fait à travers un grand nombre de tests utilisateur, de prototypages, d’essais et d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="9eb60-107">We did this through a lot of user testing, prototyping, and trial and error.</span></span>

<span data-ttu-id="9eb60-108">Nous savons que tous les utilisateurs n’ont pas les ressources nécessaires pour effectuer ce type de recherche. nous avions donc notre concepteur SR. holographique, Marcus Ghaly, à partager trois choses que nous avons appris pendant le développement de HoloStudio sur l’interface utilisateur et la conception d’interaction pour les applications HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9eb60-108">We know that not everyone has the resources at their disposal to do this type of research, so we had our Sr. Holographic Designer, Marcus Ghaly, share three things we learned during the development of HoloStudio about UI and interaction design for HoloLens apps.</span></span>

## <a name="watch-the-video"></a><span data-ttu-id="9eb60-109">Regarder la vidéo</span><span class="sxs-lookup"><span data-stu-id="9eb60-109">Watch the video</span></span>

>[!VIDEO https://www.youtube.com/embed/sX6yKHmN1qM]

## <a name="problem-1-people-didnt-want-to-move-around-their-creations"></a><span data-ttu-id="9eb60-110">#1 du problème: Les gens ne veulent pas se déplacer dans leurs créations</span><span class="sxs-lookup"><span data-stu-id="9eb60-110">Problem #1: People didn't want to move around their creations</span></span>

<span data-ttu-id="9eb60-111">Nous avons initialement conçu le Workbench dans HoloStudio comme un rectangle, comme vous le feriez dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="9eb60-111">We originally designed the workbench in HoloStudio as a rectangle, much like you'd find in the real world.</span></span> <span data-ttu-id="9eb60-112">Le problème est que les gens ont une durée de vie qui leur demande de rester quand ils sont assis sur un bureau ou qu’ils travaillent devant un ordinateur, de sorte qu’ils ne se déplacent pas dans l’atelier et explorent leur création en 3D de tous les côtés.</span><span class="sxs-lookup"><span data-stu-id="9eb60-112">The problem is that people have a lifetime of experience that tells them to stay still when they're sitting at a desk or working in front of a computer, so they weren't moving around the workbench and exploring their 3D creation from all sides.</span></span>

![La conception rectangulaire du Workbench dans HoloStudio dissuaded les utilisateurs de se déplacer et de voir leurs créations de tous les côtés.](images/rectangular-workbench-500px.jpg)

<span data-ttu-id="9eb60-114">Nous avons eu l’idée de faire en sorte que le banc d’essai fasse l’aller de l’avant, ce qui signifie qu’il n’y avait pas de «front» ou d’endroit évident que vous étiez supposé reposer.</span><span class="sxs-lookup"><span data-stu-id="9eb60-114">We had the insight to make the workbench round, so that there was no "front" or clear place that you were supposed to stand.</span></span> <span data-ttu-id="9eb60-115">Lorsque nous avons testé cette solution, soudain, les utilisateurs ont commencé à se déplacer et à explorer leurs créations eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="9eb60-115">When we tested this, suddenly people started moving around and exploring their creations on their own.</span></span>

![La conception circulaire Workbench encourage les utilisateurs à se familiariser avec leurs créations.](images/circular-workbench-500px.jpg)

<span data-ttu-id="9eb60-117">**Ce que nous avons appris**</span><span class="sxs-lookup"><span data-stu-id="9eb60-117">**What we learned**</span></span>

<span data-ttu-id="9eb60-118">Réfléchissez toujours à ce qui est confortable pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9eb60-118">Always be thinking about what's comfortable for the user.</span></span> <span data-ttu-id="9eb60-119">Tirer parti de leur espace physique est une fonctionnalité utile de HoloLens et un élément que vous ne pouvez pas faire avec d’autres appareils.</span><span class="sxs-lookup"><span data-stu-id="9eb60-119">Taking advantage of their physical space is a cool feature of HoloLens and something you can't do with other devices.</span></span>

## <a name="problem-2-modal-dialogs-are-sometimes-out-of-the-holographic-frame"></a><span data-ttu-id="9eb60-120">#2 du problème: Les boîtes de dialogue modales sont parfois hors du frame holographique</span><span class="sxs-lookup"><span data-stu-id="9eb60-120">Problem #2: Modal dialogs are sometimes out of the holographic frame</span></span>

<span data-ttu-id="9eb60-121">Parfois, il se peut que votre utilisateur regarde dans une autre direction que celle qui nécessite une attention particulière dans votre application.</span><span class="sxs-lookup"><span data-stu-id="9eb60-121">Sometimes, your user may be looking in a different direction from something that needs their attention in your app.</span></span> <span data-ttu-id="9eb60-122">Sur un PC, vous pouvez simplement afficher une boîte de dialogue, mais si vous effectuez cette opération dans un environnement 3D, il peut sembler que la boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9eb60-122">On a PC, you can just pop up a dialog, but if you do this in someone's face in a 3D environment, it can feel like the dialog is getting in their way.</span></span> <span data-ttu-id="9eb60-123">Vous en avez besoin pour lire le message, mais leur instinct est de tenter de s’en éloigner.</span><span class="sxs-lookup"><span data-stu-id="9eb60-123">You need them to read the message, but their instinct is to try to get away from it.</span></span> <span data-ttu-id="9eb60-124">Cette réaction est intéressante si vous jouez à un jeu, mais dans un outil conçu pour le travail, il est moins que parfait.</span><span class="sxs-lookup"><span data-stu-id="9eb60-124">This reaction is great if you're playing a game, but in a tool designed for work, it's less than ideal.</span></span>

<span data-ttu-id="9eb60-125">Après avoir essayé plusieurs choses, nous avons finalement décidé d’utiliser un système de «bulles de pensée» pour nos boîtes de dialogue et d’ajouter des tendrils que les utilisateurs peuvent suivre à l’endroit où leur attention est nécessaire dans notre application.</span><span class="sxs-lookup"><span data-stu-id="9eb60-125">After trying a few different things, we finally settled on using a "thought bubble" system for our dialogs and added tendrils that users can follow to where their attention is needed in our application.</span></span> <span data-ttu-id="9eb60-126">Nous avons également rendu l’impulsion tendrils, qui impliquait un sens de la direction afin que les utilisateurs connaissaient l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="9eb60-126">We also made the tendrils pulse, which implied a sense of directionality so that users knew where to go.</span></span>

![Le système «bulle de pensée» comprenait des tendrilss d’impulsions qui offraient un sens de direction, les utilisateurs de premier plan à l’endroit où leur attention était nécessaire dans l’application.](images/thought-bubble-500px.jpg)

<span data-ttu-id="9eb60-128">**Ce que nous avons appris**</span><span class="sxs-lookup"><span data-stu-id="9eb60-128">**What we learned**</span></span>

<span data-ttu-id="9eb60-129">En 3D, il est beaucoup plus difficile d’alerter les utilisateurs en fonction de leurs besoins.</span><span class="sxs-lookup"><span data-stu-id="9eb60-129">It's much harder in 3D to alert users to things they need to pay attention to.</span></span> <span data-ttu-id="9eb60-130">L’utilisation de directeurs d’attention tels que le [son spatial](spatial-sound.md), les rayons de lumière ou les bulles de pensée peut amener les utilisateurs à l’endroit où ils doivent être.</span><span class="sxs-lookup"><span data-stu-id="9eb60-130">Using attention directors such as [spatial sound](spatial-sound.md), light rays, or thought bubbles, can lead users to where they need to be.</span></span>

## <a name="problem-3-sometimes-ui-can-get-blocked-by-other-holograms"></a><span data-ttu-id="9eb60-131">#3 du problème: Parfois, l’interface utilisateur peut être bloquée par d’autres hologrammes</span><span class="sxs-lookup"><span data-stu-id="9eb60-131">Problem #3: Sometimes UI can get blocked by other holograms</span></span>

<span data-ttu-id="9eb60-132">Il peut arriver qu’un utilisateur souhaite interagir avec un hologramme et ses contrôles d’interface utilisateur associés, mais qu’il ne peut pas être affiché parce qu’un autre hologramme est devant eux.</span><span class="sxs-lookup"><span data-stu-id="9eb60-132">There are times when a user wants to interact with a hologram and its associated UI controls, but they are blocked from view because another hologram is in front of them.</span></span> <span data-ttu-id="9eb60-133">Pendant que nous développons HoloStudio, nous avons utilisé une version d’évaluation et une erreur pour résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="9eb60-133">While we were developing HoloStudio, we used trial and error to come to a solution for this.</span></span>

![Un contrôle d’interface utilisateur associé à un hologramme peut être bloqué s’il y a un autre hologramme entre celui-ci et l’utilisateur qui a le port HoloLens.](images/ui-blocked-500px.jpg)

<span data-ttu-id="9eb60-135">Nous avons essayé de rapprocher le contrôle d’interface utilisateur de l’utilisateur afin qu’il n’ait pas pu être bloqué, mais il a été découvert qu’il n’était pas facile pour l’utilisateur d’examiner un contrôle qui était proche de vous en regardant simultanément un hologramme éloigné.</span><span class="sxs-lookup"><span data-stu-id="9eb60-135">We tried moving the UI control closer to the user so it couldn't get blocked, but found that it wasn't comfortable for the user to look at a control that was near to you while simultaneously looking at a hologram that was far away.</span></span> <span data-ttu-id="9eb60-136">Toutefois, si nous avons déplacé le contrôle devant l’hologramme le plus proche de l’utilisateur, il a pensé qu’il a été détaché de l’hologramme qu’il devrait affecter.</span><span class="sxs-lookup"><span data-stu-id="9eb60-136">If, however, we moved the control in front of the closest hologram to the user, they felt like it was detached from the hologram it should be affecting.</span></span>

<span data-ttu-id="9eb60-137">Nous avons finalement fini de dupliquer le contrôle de l’interface utilisateur et le placer à la même distance de l’utilisateur que l’hologramme auquel il est associé, de sorte qu’ils se sentent tous deux connectés.</span><span class="sxs-lookup"><span data-stu-id="9eb60-137">We finally ended up ghosting the UI control, and put it at the same distance from the user as the hologram it's associated with, so they both feel connected.</span></span> <span data-ttu-id="9eb60-138">Cela permet à l’utilisateur d’interagir avec le contrôle même s’il est masqué.</span><span class="sxs-lookup"><span data-stu-id="9eb60-138">This allows the user to interact with the control even though it's been obscured.</span></span>

![La solution: nous avons dupliqué le contrôle de l’interface utilisateur, qui permettait l’interaction avec le contrôle et a fait en sorte qu’il soit connecté à l’hologramme qu’il affectait.](images/ghosting-ui-500px.jpg)

<span data-ttu-id="9eb60-140">**Ce que nous avons appris**</span><span class="sxs-lookup"><span data-stu-id="9eb60-140">**What we learned**</span></span>

<span data-ttu-id="9eb60-141">Les utilisateurs doivent être en mesure d’accéder facilement aux contrôles d’interface utilisateur même s’ils ont été bloqués. par conséquent, déterminez les méthodes permettant de s’assurer que les utilisateurs peuvent effectuer leurs tâches, quel que soit l’endroit où leurs hologrammes se trouvent dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="9eb60-141">Users need to be able to easily access UI controls even if they've been blocked, so figure out methods to ensure that users can complete their tasks no matter where their holograms are in the real world.</span></span>

## <a name="about-the-author"></a><span data-ttu-id="9eb60-142">À propos de l’auteur</span><span class="sxs-lookup"><span data-stu-id="9eb60-142">About the author</span></span>

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60"><img alt="Picture of Marcus Ghaly" width="60" height="60" src="images/marcus-ghaly-200px.jpg"></td>
<td style="border-style: none"><span data-ttu-id="9eb60-143"><b>Marcus Ghaly</b></span><span class="sxs-lookup"><span data-stu-id="9eb60-143"><b>Marcus Ghaly</b></span></span><br><span data-ttu-id="9eb60-144">Concepteur de SR. holographique@Microsoft</span><span class="sxs-lookup"><span data-stu-id="9eb60-144">Sr. Holographic Designer @Microsoft</span></span></td>
</tr>
</table>

## <a name="see-also"></a><span data-ttu-id="9eb60-145">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9eb60-145">See also</span></span>
* [<span data-ttu-id="9eb60-146">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="9eb60-146">Instinctual interactions</span></span>](interaction-fundamentals.md)

 
