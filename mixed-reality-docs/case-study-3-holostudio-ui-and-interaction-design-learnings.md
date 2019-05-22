---
title: Étude de cas - 3 HoloStudio l’interface utilisateur et l’interaction des apprentissages de conception
description: HoloStudio UI et apprentissages de conception d’interaction
author: rwinj
ms.author: marcghal
ms.date: 03/21/2018
ms.topic: article
keywords: Windows HoloLens, HoloStudio, une réalité mixte
ms.openlocfilehash: e01e2ea888398e9982b56fd95f90ef0731ec6bc2
ms.sourcegitcommit: c20563b8195c0c374a927b96708d958b127ffc8f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974827"
---
# <a name="case-study---3-holostudio-ui-and-interaction-design-learnings"></a>Étude de cas - 3 HoloStudio l’interface utilisateur et l’interaction des apprentissages de conception

[HoloStudio](https://www.youtube.com/watch?v=BRIJG0x_We8) a été l’une des applications Microsoft premier pour HoloLens. Pour cette raison, nous avons dû créer de meilleures pratiques pour l’interface utilisateur de 3D et conception de l’interaction. Nous l’avons fait cela via un grand nombre de test de l’utilisateur, de prototypage et d’essais et d’erreurs.

Nous savons que pas tout le monde dispose des ressources à leur disposition pour effectuer ce type de recherche, donc nous avions notre concepteur HOLOGRAPHIQUE senior, Marcus Ghaly, partager des trois choses que nous avons appris lors du développement de HoloStudio sur la conception de l’interface utilisateur et d’interaction pour les applications de HoloLens.

## <a name="watch-the-video"></a>Regardez la vidéo

>[!VIDEO https://www.youtube.com/embed/sX6yKHmN1qM]

## <a name="problem-1-people-didnt-want-to-move-around-their-creations"></a>Problème #1 : Personnes ne souhaitais pas que pour vous déplacer dans leurs créations

Nous avons initialement conçu le banc d’essai dans HoloStudio comme un rectangle, beaucoup que vous trouveriez dans le monde réel. Le problème est que les personnes ont une durée de vie de l’expérience lui indiquant de rester toujours lorsqu’ils sont assis à un bureau ou utilisation devant un ordinateur, afin qu’ils n’ont pas été déplaçant le banc d’essai et Explorer leur création 3D à partir de tous les côtés.

![La conception rectangulaire du banc d’essai dans HoloStudio dissuaded les utilisateurs de déplacer et voir leurs créations à partir de tous les côtés.](images/rectangular-workbench-500px.jpg)

Nous avions l’information pour rendre le banc d’essai arrondir, afin qu’il n’a aucun « avant » ou effacer sur place qui vous devait reposer. Lorsque nous avons testé cette, personnes a commencé déplaçant dans et en explorant leurs créations sur leurs propres.

![La conception de workbench circulaire d’encourager les utilisateurs à parcourir tout autour de leurs créations.](images/circular-workbench-500px.jpg)

**Ce que nous avons appris**

Toujours être réfléchir à ce qui est à l’aise pour l’utilisateur. En tirant parti de leur espace physique est une fonction pratique de HoloLens et quelque chose que vous ne pouvez pas faire avec d’autres périphériques.

## <a name="problem-2-modal-dialogs-are-sometimes-out-of-the-holographic-frame"></a>Problème #2 : Boîtes de dialogue modales sont parfois hors du cadre HOLOGRAPHIQUE

Parfois, votre utilisateur peut rechercher dans une direction différente d’un élément nécessitant leur attention dans votre application. Sur un PC, vous pouvez simplement la fenêtre contextuelle jusqu'à une boîte de dialogue, mais si vous le faire en face d’un utilisateur dans un environnement 3D, il peut le sentiment l’obtention de la boîte de dialogue dans leur façon. Vous en avez besoin pour lire le message, mais leur instinct consiste à essayer d’obtenir depuis celle-ci. Cette réaction est très utile si vous jouez à un jeu, mais dans un outil conçu pour le travail, il est loin d’être idéal.

Après avoir essayé les différentes opérations, nous avons enfin réglée sur l’utilisation d’un système « pensé à bulles » pour nos boîtes de dialogue et ajouté des VRILLES les utilisateurs peuvent suivre pour où leur attention est nécessaire dans notre application. Nous avons apporté également l’impulsion VRILLES, cela impliquait une idée de direction afin que les utilisateurs savaient où aller.

![Le système « Bulle pensé » inclus VRILLES clignotant qui a fourni une idée de direction, permettant ainsi aux utilisateurs où leur attention était nécessaire dans l’application.](images/thought-bubble-500px.jpg)

**Ce que nous avons appris**

Il est beaucoup plus difficile en 3D pour avertir les utilisateurs à des choses qu’ils doivent faire attention aux. À l’aide de directeurs d’attention comme [son spatial](spatial-sound.md), light rayons, ou se propage de pensée, peut entraîner les utilisateurs où ils doivent être.

## <a name="problem-3-sometimes-ui-can-get-blocked-by-other-holograms"></a>Problème #3 : Parfois, l’interface utilisateur peut être bloqué par d’autres hologrammes

Il est parfois quand un utilisateur souhaite interagir avec un hologramme et ses contrôles d’interface utilisateur associés, mais ils sont bloqués à partir de la vue, car un autre hologramme est placé devant. Pendant que nous développions HoloStudio, nous avons utilisé des tâtonnements à venir pour une solution pour ce.

![Un contrôle d’interface utilisateur associé à un hologramme peut devenir bloqué s’il existe un autre hologramme entre elle et l’utilisateur a porter HoloLens.](images/ui-blocked-500px.jpg)

Nous avons essayé de déplacer le contrôle de l’interface utilisateur plus près à l’utilisateur afin qu’il n’a pas pu obtenir bloquée, mais trouvé qu’il n’a pas été à l’aise pour l’utilisateur d’examiner un contrôle qui a été proche de vous, tout en gardant simultanément un hologramme qui a été éloigné. Si, toutefois, nous avons déplacé le contrôle devant l’hologramme le plus proche à l’utilisateur, ils ont pensé comme elle a été détachée à partir de l’hologramme qu'il doit affecter.

Nous enfin retrouvés "ghosting" contrôle d’interface utilisateur et placez-le à la même distance à partir de l’utilisateur en tant que l’hologramme associé, pour que les deux Parcourir connectés. Cela permet à l’utilisateur d’interagir avec le contrôle, même si elle est été masquée.

![La solution : nous dédoublé le contrôle de l’interface utilisateur, qui à la fois autorisé l’interaction avec le contrôle et le rend l’impression connectée vers hologramme de celle-ci a été affecte.](images/ghosting-ui-500px.jpg)

**Ce que nous avons appris**

Les utilisateurs doivent être en mesure d’accéder facilement aux contrôles d’interface utilisateur même s’ils ont été bloqués, devez donc déterminer les méthodes pour vous assurer que les utilisateurs peuvent effectuer leurs tâches, où leurs hologrammes sont dans le monde réel.

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60"><img alt="Picture of Marcus Ghaly" width="60" height="60" src="images/marcus-ghaly-200px.jpg"></td>
<td style="border-style: none"><b>Marcus Ghaly</b><br>Concepteur HOLOGRAPHIQUE SR. @Microsoft</td>
</tr>
</table>

## <a name="see-also"></a>Voir aussi
* [Interactions instinctuelles](interaction-fundamentals.md)

 
