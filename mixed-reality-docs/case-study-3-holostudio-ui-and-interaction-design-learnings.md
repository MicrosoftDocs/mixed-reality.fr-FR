---
title: Étude de cas - 3 HoloStudio l’interface utilisateur et l’interaction des apprentissages de conception
description: HoloStudio UI et apprentissages de conception d’interaction
author: rwinj
ms.author: marcghal
ms.date: 03/21/2018
ms.topic: article
keywords: Windows HoloLens, HoloStudio, une réalité mixte
ms.openlocfilehash: 217c489fed3c0588dae1c2753db6ba15da3522c8
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596016"
---
# <a name="case-study---3-holostudio-ui-and-interaction-design-learnings"></a><span data-ttu-id="67507-104">Étude de cas - 3 HoloStudio l’interface utilisateur et l’interaction des apprentissages de conception</span><span class="sxs-lookup"><span data-stu-id="67507-104">Case study - 3 HoloStudio UI and interaction design learnings</span></span>

<span data-ttu-id="67507-105">[HoloStudio](https://www.youtube.com/watch?v=BRIJG0x_We8) a été l’une des applications Microsoft premier pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="67507-105">[HoloStudio](https://www.youtube.com/watch?v=BRIJG0x_We8) was one of the first Microsoft apps for HoloLens.</span></span> <span data-ttu-id="67507-106">Pour cette raison, nous avons dû créer de meilleures pratiques pour l’interface utilisateur de 3D et conception de l’interaction.</span><span class="sxs-lookup"><span data-stu-id="67507-106">Because of this, we had to create new best practices for 3D UI and interaction design.</span></span> <span data-ttu-id="67507-107">Nous l’avons fait cela via un grand nombre de test de l’utilisateur, de prototypage et d’essais et d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="67507-107">We did this through a lot of user testing, prototyping, and trial and error.</span></span>

<span data-ttu-id="67507-108">Nous savons que pas tout le monde dispose des ressources à leur disposition pour effectuer ce type de recherche, donc nous avions notre concepteur HOLOGRAPHIQUE senior, Marcus Ghaly, partager des trois choses que nous avons appris lors du développement de HoloStudio sur la conception de l’interface utilisateur et d’interaction pour les applications de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="67507-108">We know that not everyone has the resources at their disposal to do this type of research, so we had our Sr. Holographic Designer, Marcus Ghaly, share three things we learned during the development of HoloStudio about UI and interaction design for HoloLens apps.</span></span>

## <a name="watch-the-video"></a><span data-ttu-id="67507-109">Regardez la vidéo</span><span class="sxs-lookup"><span data-stu-id="67507-109">Watch the video</span></span>

>[!VIDEO https://www.youtube.com/embed/sX6yKHmN1qM]

## <a name="problem-1-people-didnt-want-to-move-around-their-creations"></a><span data-ttu-id="67507-110">Problème #1 : Personnes ne souhaitais pas que pour vous déplacer dans leurs créations</span><span class="sxs-lookup"><span data-stu-id="67507-110">Problem #1: People didn't want to move around their creations</span></span>

<span data-ttu-id="67507-111">Nous avons initialement conçu le banc d’essai dans HoloStudio comme un rectangle, beaucoup que vous trouveriez dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="67507-111">We originally designed the workbench in HoloStudio as a rectangle, much like you'd find in the real world.</span></span> <span data-ttu-id="67507-112">Le problème est que les personnes ont une durée de vie de l’expérience lui indiquant de rester toujours lorsqu’ils sont assis à un bureau ou utilisation devant un ordinateur, afin qu’ils n’ont pas été déplaçant le banc d’essai et Explorer leur création 3D à partir de tous les côtés.</span><span class="sxs-lookup"><span data-stu-id="67507-112">The problem is that people have a lifetime of experience that tells them to stay still when they're sitting at a desk or working in front of a computer, so they weren't moving around the workbench and exploring their 3D creation from all sides.</span></span>

![La conception rectangulaire du banc d’essai dans HoloStudio dissuaded les utilisateurs de déplacer et voir leurs créations à partir de tous les côtés.](images/rectangular-workbench-500px.jpg)

<span data-ttu-id="67507-114">Nous avions l’information pour rendre le banc d’essai arrondir, afin qu’il n’a aucun « avant » ou effacer sur place qui vous devait reposer.</span><span class="sxs-lookup"><span data-stu-id="67507-114">We had the insight to make the workbench round, so that there was no "front" or clear place that you were supposed to stand.</span></span> <span data-ttu-id="67507-115">Lorsque nous avons testé cette, personnes a commencé déplaçant dans et en explorant leurs créations sur leurs propres.</span><span class="sxs-lookup"><span data-stu-id="67507-115">When we tested this, suddenly people started moving around and exploring their creations on their own.</span></span>

![La conception de workbench circulaire d’encourager les utilisateurs à parcourir tout autour de leurs créations.](images/circular-workbench-500px.jpg)

<span data-ttu-id="67507-117">**Ce que nous avons appris**</span><span class="sxs-lookup"><span data-stu-id="67507-117">**What we learned**</span></span>

<span data-ttu-id="67507-118">Toujours être réfléchir à ce qui est à l’aise pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="67507-118">Always be thinking about what's comfortable for the user.</span></span> <span data-ttu-id="67507-119">En tirant parti de leur espace physique est une fonction pratique de HoloLens et quelque chose que vous ne pouvez pas faire avec d’autres périphériques.</span><span class="sxs-lookup"><span data-stu-id="67507-119">Taking advantage of their physical space is a cool feature of HoloLens and something you can't do with other devices.</span></span>

## <a name="problem-2-modal-dialogs-are-sometimes-out-of-the-holographic-frame"></a><span data-ttu-id="67507-120">Problème #2 : Boîtes de dialogue modales sont parfois hors du cadre HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="67507-120">Problem #2: Modal dialogs are sometimes out of the holographic frame</span></span>

<span data-ttu-id="67507-121">Parfois, votre utilisateur peut rechercher dans une direction différente d’un élément nécessitant leur attention dans votre application.</span><span class="sxs-lookup"><span data-stu-id="67507-121">Sometimes, your user may be looking in a different direction from something that needs their attention in your app.</span></span> <span data-ttu-id="67507-122">Sur un PC, vous pouvez simplement la fenêtre contextuelle jusqu'à une boîte de dialogue, mais si vous le faire en face d’un utilisateur dans un environnement 3D, il peut le sentiment l’obtention de la boîte de dialogue dans leur façon.</span><span class="sxs-lookup"><span data-stu-id="67507-122">On a PC, you can just pop up a dialog, but if you do this in someone's face in a 3D environment, it can feel like the dialog is getting in their way.</span></span> <span data-ttu-id="67507-123">Vous en avez besoin pour lire le message, mais leur instinct consiste à essayer d’obtenir depuis celle-ci.</span><span class="sxs-lookup"><span data-stu-id="67507-123">You need them to read the message, but their instinct is to try to get away from it.</span></span> <span data-ttu-id="67507-124">Cette réaction est très utile si vous jouez à un jeu, mais dans un outil conçu pour le travail, il est loin d’être idéal.</span><span class="sxs-lookup"><span data-stu-id="67507-124">This reaction is great if you're playing a game, but in a tool designed for work, it's less than ideal.</span></span>

<span data-ttu-id="67507-125">Après avoir essayé les différentes opérations, nous avons enfin réglée sur l’utilisation d’un système « pensé à bulles » pour nos boîtes de dialogue et ajouté des VRILLES les utilisateurs peuvent suivre pour où leur attention est nécessaire dans notre application.</span><span class="sxs-lookup"><span data-stu-id="67507-125">After trying a few different things, we finally settled on using a "thought bubble" system for our dialogs and added tendrils that users can follow to where their attention is needed in our application.</span></span> <span data-ttu-id="67507-126">Nous avons apporté également l’impulsion VRILLES, cela impliquait une idée de direction afin que les utilisateurs savaient où aller.</span><span class="sxs-lookup"><span data-stu-id="67507-126">We also made the tendrils pulse, which implied a sense of directionality so that users knew where to go.</span></span>

![Le système « Bulle pensé » inclus VRILLES clignotant qui a fourni une idée de direction, permettant ainsi aux utilisateurs où leur attention était nécessaire dans l’application.](images/thought-bubble-500px.jpg)

<span data-ttu-id="67507-128">**Ce que nous avons appris**</span><span class="sxs-lookup"><span data-stu-id="67507-128">**What we learned**</span></span>

<span data-ttu-id="67507-129">Il est beaucoup plus difficile en 3D pour avertir les utilisateurs à des choses qu’ils doivent faire attention aux.</span><span class="sxs-lookup"><span data-stu-id="67507-129">It's much harder in 3D to alert users to things they need to pay attention to.</span></span> <span data-ttu-id="67507-130">À l’aide de directeurs d’attention comme [son spatial](spatial-sound.md), light rayons, ou se propage de pensée, peut entraîner les utilisateurs où ils doivent être.</span><span class="sxs-lookup"><span data-stu-id="67507-130">Using attention directors such as [spatial sound](spatial-sound.md), light rays, or thought bubbles, can lead users to where they need to be.</span></span>

## <a name="problem-3-sometimes-ui-can-get-blocked-by-other-holograms"></a><span data-ttu-id="67507-131">Problème #3 : Parfois, l’interface utilisateur peut être bloqué par d’autres hologrammes</span><span class="sxs-lookup"><span data-stu-id="67507-131">Problem #3: Sometimes UI can get blocked by other holograms</span></span>

<span data-ttu-id="67507-132">Il est parfois quand un utilisateur souhaite interagir avec un hologramme et ses contrôles d’interface utilisateur associés, mais ils sont bloqués à partir de la vue, car un autre hologramme est placé devant.</span><span class="sxs-lookup"><span data-stu-id="67507-132">There are times when a user wants to interact with a hologram and its associated UI controls, but they are blocked from view because another hologram is in front of them.</span></span> <span data-ttu-id="67507-133">Pendant que nous développions HoloStudio, nous avons utilisé des tâtonnements à venir pour une solution pour ce.</span><span class="sxs-lookup"><span data-stu-id="67507-133">While we were developing HoloStudio, we used trial and error to come to a solution for this.</span></span>

![Un contrôle d’interface utilisateur associé à un hologramme peut devenir bloqué s’il existe un autre hologramme entre elle et l’utilisateur a porter HoloLens.](images/ui-blocked-500px.jpg)

<span data-ttu-id="67507-135">Nous avons essayé de déplacer le contrôle de l’interface utilisateur plus près à l’utilisateur afin qu’il n’a pas pu obtenir bloquée, mais trouvé qu’il n’a pas été à l’aise pour l’utilisateur d’examiner un contrôle qui a été proche de vous, tout en gardant simultanément un hologramme qui a été éloigné.</span><span class="sxs-lookup"><span data-stu-id="67507-135">We tried moving the UI control closer to the user so it couldn't get blocked, but found that it wasn't comfortable for the user to look at a control that was near to you while simultaneously looking at a hologram that was far away.</span></span> <span data-ttu-id="67507-136">Si, toutefois, nous avons déplacé le contrôle devant l’hologramme le plus proche à l’utilisateur, ils ont pensé comme elle a été détachée à partir de l’hologramme qu'il doit affecter.</span><span class="sxs-lookup"><span data-stu-id="67507-136">If, however, we moved the control in front of the closest hologram to the user, they felt like it was detached from the hologram it should be affecting.</span></span>

<span data-ttu-id="67507-137">Nous enfin retrouvés "ghosting" contrôle d’interface utilisateur et placez-le à la même distance à partir de l’utilisateur en tant que l’hologramme associé, pour que les deux Parcourir connectés.</span><span class="sxs-lookup"><span data-stu-id="67507-137">We finally ended up ghosting the UI control, and put it at the same distance from the user as the hologram it's associated with, so they both feel connected.</span></span> <span data-ttu-id="67507-138">Cela permet à l’utilisateur d’interagir avec le contrôle, même si elle est été masquée.</span><span class="sxs-lookup"><span data-stu-id="67507-138">This allows the user to interact with the control even though it's been obscured.</span></span>

![La solution : nous dédoublé le contrôle de l’interface utilisateur, qui à la fois autorisé l’interaction avec le contrôle et le rend l’impression connectée vers hologramme de celle-ci a été affecte.](images/ghosting-ui-500px.jpg)

<span data-ttu-id="67507-140">**Ce que nous avons appris**</span><span class="sxs-lookup"><span data-stu-id="67507-140">**What we learned**</span></span>

<span data-ttu-id="67507-141">Les utilisateurs doivent être en mesure d’accéder facilement aux contrôles d’interface utilisateur même s’ils ont été bloqués, devez donc déterminer les méthodes pour vous assurer que les utilisateurs peuvent effectuer leurs tâches, où leurs hologrammes sont dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="67507-141">Users need to be able to easily access UI controls even if they've been blocked, so figure out methods to ensure that users can complete their tasks no matter where their holograms are in the real world.</span></span>

## <a name="about-the-author"></a><span data-ttu-id="67507-142">À propos de l’auteur</span><span class="sxs-lookup"><span data-stu-id="67507-142">About the author</span></span>

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60"><img alt="Picture of Marcus Ghaly" width="60" height="60" src="images/marcus-ghaly-200px.jpg"></td>
<td style="border-style: none"><span data-ttu-id="67507-143"><b>Marcus Ghaly</b></span><span class="sxs-lookup"><span data-stu-id="67507-143"><b>Marcus Ghaly</b></span></span><br><span data-ttu-id="67507-144">Concepteur HOLOGRAPHIQUE SR. @Microsoft</span><span class="sxs-lookup"><span data-stu-id="67507-144">Sr. Holographic Designer @Microsoft</span></span></td>
</tr>
</table>

## <a name="see-also"></a><span data-ttu-id="67507-145">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="67507-145">See also</span></span>
* [<span data-ttu-id="67507-146">Notions fondamentales d’interaction</span><span class="sxs-lookup"><span data-stu-id="67507-146">Interaction fundamentals</span></span>](interaction-fundamentals.md)

 
