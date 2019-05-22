---
title: Le billboarding et tag-along
description: Objets avec le billboarding intérimaires toujours pour faire face à l’utilisateur.
author: radicalad
ms.author: adlinv
ms.date: 03/21/2018
ms.topic: article
keywords: Réalité mixte de Windows, le billboarding, tag-along
ms.openlocfilehash: e33ab0121398742b2e48553c9cbf2c1debdc6abf
ms.sourcegitcommit: c20563b8195c0c374a927b96708d958b127ffc8f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974786"
---
# <a name="billboarding-and-tag-along"></a>Le billboarding et tag-along

Le billboarding est un concept de comportement qui peut être appliqué aux objets dans la réalité mixte. Objets avec le billboarding intérimaires toujours pour faire face à l’utilisateur. Ceci est particulièrement utile avec le texte et les systèmes de rentrer où les objets statiques sont placés dans l’environnement utilisateur (verrouillé au monde) serait sinon masquées ou illisibles si un utilisateur à déplacer.

![HoloLens de point de vue d’un système de menus qui toujours est confronté l’utilisateur](images/billboarding-fragments.gif)<br>
*HoloLens de point de vue d’un système de menus qui toujours est confronté l’utilisateur*

Objets avec le billboarding activée peuvent faire pivoter librement dans l’environnement utilisateur. Ils peuvent également être limités à un seul axe en fonction des considérations de conception. N’oubliez pas, les objets billboarded peuvent découper ou occlude eux-mêmes s’ils sont placés trop près d’autres objets, ou dans HoloLens, trop près analysés surfaces. Pour éviter ce problème, pensez à l’encombrement total à qu'un objet peut produire lors de rotation sur l’axe est activé pour le billboarding.

## <a name="what-is-a-tag-along"></a>Qu’est un tag-along ?

Tag-Along est un concept de comportement qui peut être ajouté à hologrammes, y compris les objets billboarded. Cette interaction est un moyen plus naturel et convivial de la réalisation de l’effet du contenu de tête verrouillée. Un objet tag-along tente ne quittent jamais vue de l’utilisateur. Cela permet à l’utilisateur d’interagir librement avec ce qui est avant tout profitant toujours également les hologrammes en dehors de leur vue directe.

![Le panneau de codes confidentiels HoloLens constitue un excellent exemple de comment se comporte tag-along](images/tagalong-1000px.jpg)<br>
*Le menu Démarrer de HoloLens constitue un excellent exemple de comportement de tag-along*

Les objets Tag-Along ont des paramètres qui peuvent ajuster le comportement. Contenu peut être dans ou hors d’une visibilité de l’utilisateur comme vous le souhaitez, tandis que l’utilisateur se déplace sur leur environnement. Lorsque l’utilisateur se trouve, le contenu va tenter de rester au sein de la périphérie de l’utilisateur en faisant glisser vers le bord de la vue, selon la vitesse à laquelle un utilisateur déplace peut laisser le contenu temporairement hors de la vue. Lorsque l’utilisateur son rapprocher de l’objet tag-along, il s’agit plus en détail dans la vue. Réfléchir contenu toujours en cours « un coup de œil absent » pour les utilisateurs oublient jamais quel sens leur contenu est dans.

Paramètres supplémentaires peuvent rendre l’objet tag-along se sentent attaché au début de l’utilisateur par un élastique. Blocage de l’accélération ou la décélération donne de poids à l’objet environnement plus physiquement présent. Ce comportement spring est un intuitif qui permet à l’utilisateur de créer un modèle mental précis du fonctionnement de tag-along. Audio contribue à supplémentaires permettant de lorsque les utilisateurs disposent des objets en mode de tag-along. Audio doit renforcer la vitesse du mouvement ; un tour rapide principal doit fournir un effet audio plus notable tandis que parcours à une vitesse naturelle doivent présenter des effets audio dans le cas échéant minimaux du tout.

Comme contenu véritablement tête verrouillée, les objets tag-along peuvent s’avérer surcharger ou nauseating s’ils connaissent un formidable de déplacer ou printemps trop en vue de l’utilisateur. Comme un utilisateur recherche et puis rapidement stop, leurs sens en leur indiquant qu’ils ont arrêté. Leur solde les informe que leur tête a cessé de tournage, ainsi que leurs voit vision l’arrêt du monde activation. Toutefois, si tag-along à déplacer dans lorsque l’utilisateur s’est arrêté, il risque de perturber leurs sens.

## <a name="see-also"></a>Voir aussi
* [Curseurs](cursors.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Confort](comfort.md)
