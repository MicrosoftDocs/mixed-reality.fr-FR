---
title: Billboarding et tag-avec
description: Les objets avec des panneaux s’orientent toujours pour être confrontés à l’utilisateur.
author: radicalad
ms.author: adlinv
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, billboarding, balise
ms.openlocfilehash: 032e665d94a73b94b59f693e452874af0b45f021
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73436997"
---
# <a name="billboarding-and-tag-along"></a>Billboarding et tag-avec

<br>

<img src="images/billboarding-fragments.gif" alt="HoloLens perspective of a menu system that always faces the user" width="940px">

Le billboarding est un concept comportemental qui peut être appliqué aux objets en réalité mixte. Les objets avec des panneaux s’orientent toujours pour être confrontés à l’utilisateur. Cela s’avère particulièrement utile avec les systèmes de texte et de menu où les objets statiques placés dans l’environnement de l’utilisateur (verrouillé) seraient autrement masqués ou illisibles si un utilisateur se déplace.

Les objets avec le billboarding activé peuvent pivoter librement dans l’environnement de l’utilisateur. Ils peuvent également être limités à un seul axe en fonction des considérations de conception. Gardez à l’esprit que les objets superposés peuvent découper ou occultait eux-mêmes s’ils sont placés trop près d’autres objets, ou dans HoloLens, trop proches des surfaces numérisées. Pour éviter cela, réfléchissez à l’encombrement total qu’un objet peut produire en cas de rotation sur l’axe activé pour le billboarding.

## <a name="what-is-a-tag-along"></a>Qu’est-ce qu’une balise ?

La balise est un concept comportemental qui peut être ajouté à des hologrammes, y compris des objets de panneaux. Cette interaction est un moyen plus naturel et plus convivial d’obtenir l’effet d’un contenu verrouillé. Une balise, le long d’un objet, tente de ne jamais sortir de la vue de l’utilisateur. Cela permet à l’utilisateur d’interagir librement avec ce qui est avant, tout en continuant à voir les hologrammes en dehors de leur vue directe.

![le panneau pin HoloLens est un bon exemple de la façon dont les balises se comportent](images/tagalong-1000px.jpg)<br>
*Le menu Démarrer HoloLens est un excellent exemple de comportement avec balises*

Les objets avec balise ont des paramètres qui peuvent affiner la façon dont ils se comportent. Le contenu peut être dans ou en dehors de la ligne de vue de l’utilisateur, au fur et à mesure que l’utilisateur se déplace dans son environnement. Au fur et à mesure que l’utilisateur se déplace, le contenu tente de rester au sein de la périphérie de l’utilisateur en faisant glisser vers le bord de la vue, en fonction de la vitesse à laquelle un utilisateur se déplace, en laissant le contenu temporairement hors de l’affichage. Lorsque l’utilisateur fait un regard sur l’objet tag, il est plus complet à afficher. Imaginez que le contenu est toujours « un coup d’œil », de sorte que les utilisateurs n’oublient jamais de la direction dans laquelle ils se trouvent.

Des paramètres supplémentaires peuvent faire en sorte que l’objet de la balise soit attaché à la tête de l’utilisateur par une bande de caoutchouc. Le blocage de l’accélération ou de la décélération donne du poids à l’objet, ce qui le rend plus physiquement présent. Ce comportement de printemps est une offre qui permet à l’utilisateur de créer un modèle mental précis sur le fonctionnement de la balise. L’audio aide à fournir des intuitivité supplémentaires quand les utilisateurs disposent d’objets en mode balise. L’audio doit renforcer la vitesse de déplacement. un tour rapide doit fournir un effet sonore plus notable tout en passant à une vitesse naturelle, en cas de tout effet.

À l’instar du contenu véritablement verrouillé, les objets de balise peuvent se révéler insurmontables ou nauseating s’ils se déplacent de manière incomplète dans la vue de l’utilisateur. À mesure qu’un utilisateur regarde et s’arrête rapidement, ses sens les indiquent qu’il a cessé. Leur solde les informe que leur tête a cessé de tourner et que leur vision voit que le monde cesse de tourner. Toutefois, si tag-with continue à se déplacer lorsque l’utilisateur s’est arrêté, il peut confondre leurs sens.

## <a name="see-also"></a>Articles associés
* [Curseurs](cursors.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Confort](comfort.md)
