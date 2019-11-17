---
title: Billboarding et tag-avec
description: Les objets avec des panneaux s’orientent toujours pour être confrontés à l’utilisateur.
author: radicalad
ms.author: adlinv
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, billboarding, balise
ms.openlocfilehash: ff2b1ce20174b1b9aecbb90b1d1dc3e8896b3761
ms.sourcegitcommit: 17427d4d8c3723d53540f1b7f5bc061bba08c1d6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2019
ms.locfileid: "74143130"
---
# <a name="billboarding-and-tag-along"></a>Billboarding et tag-avec

<br>

<img src="images/UX/MRTK_TagAlong.gif" alt="HoloLens perspective of a menu system that always faces the user" width="940px">
<br>

## <a name="what-is-billboarding"></a>Qu’est-ce que le billboarding ?

Le billboarding est un concept comportemental qui peut être appliqué aux objets en réalité mixte. Les objets avec des panneaux s’orientent toujours pour être confrontés à l’utilisateur. Cela s’avère particulièrement utile avec les systèmes de texte et de menu où les objets statiques placés dans l’environnement de l’utilisateur (verrouillé) seraient autrement masqués ou illisibles si un utilisateur se déplace.

Les objets avec le billboarding activé peuvent pivoter librement dans l’environnement de l’utilisateur. Ils peuvent également être limités à un seul axe en fonction des considérations de conception. Gardez à l’esprit que les objets superposés peuvent découper ou occultait eux-mêmes s’ils sont placés trop près d’autres objets, ou dans HoloLens, trop proches des surfaces numérisées. Pour éviter cela, réfléchissez à l’encombrement total qu’un objet peut produire en cas de rotation sur l’axe activé pour le billboarding.

<br>

---
## <a name="what-is-a-tag-along"></a>Qu’est-ce qu’une balise ?

La balise est un concept comportemental qui peut être ajouté à des hologrammes. Une balise associée à un objet tente de rester dans une plage qui permet à l’utilisateur d’interagir confortablement.

![le panneau pin HoloLens est un bon exemple de la façon dont les balises se comportent](images/tagalong-1000px.jpg)<br>
*Le menu Démarrer HoloLens est un excellent exemple de comportement avec balises*

Les objets avec balise ont des paramètres qui peuvent affiner la façon dont ils se comportent. Le contenu peut être dans ou en dehors de la ligne de vue de l’utilisateur, au fur et à mesure que l’utilisateur se déplace dans son environnement. Au fur et à mesure que l’utilisateur se déplace, le contenu tente de rester au sein de la périphérie de l’utilisateur en faisant glisser vers le bord de la vue, en fonction de la vitesse à laquelle un utilisateur se déplace, en laissant le contenu temporairement hors de l’affichage. Lorsque l’utilisateur fait un regard sur l’objet tag, il est plus complet à afficher. Imaginez que le contenu est toujours « un coup d’œil », de sorte que les utilisateurs n’oublient jamais de la direction dans laquelle ils se trouvent.

Des paramètres supplémentaires peuvent faire en sorte que l’objet de la balise soit attaché à la tête de l’utilisateur par une bande de caoutchouc. Le blocage de l’accélération ou de la décélération donne du poids à l’objet, ce qui le rend plus physiquement présent. Ce comportement de printemps est une offre qui permet à l’utilisateur de créer un modèle mental précis sur le fonctionnement de la balise. L’audio aide à fournir des intuitivité supplémentaires quand les utilisateurs disposent d’objets en mode balise. L’audio doit renforcer la vitesse de déplacement. un tour rapide doit fournir un effet sonore plus notable tout en passant à une vitesse naturelle, en cas de tout effet.

À l’instar du contenu véritablement verrouillé, les objets de balise peuvent se révéler insurmontables ou nauseating s’ils se déplacent de manière incomplète dans la vue de l’utilisateur. À mesure qu’un utilisateur regarde et s’arrête rapidement, ses sens les indiquent qu’il a cessé. Leur solde les informe que leur tête a cessé de tourner et que leur vision voit que le monde cesse de tourner. Toutefois, si tag-with continue à se déplacer lorsque l’utilisateur s’est arrêté, il peut confondre leurs sens.

<br>

---

## <a name="billboarding-and-tag-along-in-mrtkmixed-reality-toolkit-for-unity"></a>Superpointage et balise dans MRTK (kit de temps de réalité mixte) pour Unity
**[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)** fournit des scripts pour le comportement de l’analyseur et de la balise. Affectez simplement le script Billboard.cs à n’importe quel objet pour ajouter un comportement d’emboutment et faire en sorte que l’objet soit toujours le même. Pour ajouter un comportement avec balise, utilisez le script RadialView.cs. Vous pouvez ajuster diverses options, telles que le temps de lerping, la distance et le degré.

* [MRTK : solveur de vue radiale](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html#radialview)
* [Script MRTK-Billboard](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Assets/MixedRealityToolkit.SDK/Features/UX/Scripts/Utilities/Billboard.cs)


<br>

---

## <a name="see-also"></a>Articles associés

* [Curseurs](cursors.md)
* [Rayon de la main](point-and-commit.md)
* [Button](button.md)
* [Objet avec interaction possible](interactable-object.md)
* [Rectangle englobant et barre de l’application](app-bar-and-bounding-box.md)
* [Manoeuvr](direct-manipulation.md)
* [Menu de la main](hand-menu.md)
* [Menu proche](near-menu.md)
* [Collection d’objets](object-collection.md)
* [Commande vocale](voice-input.md)
* [Clavier](keyboard.md)
* [Bulle](tooltip.md)
* [Médias](slate.md)
* [Curseur](slider.md)
* [Nuance](shader.md)
* [Billboarding et tag-along](billboarding-and-tag-along.md)
* [Affichage de la progression](progress.md)
* [Aimantation de surface](surface-magnetism.md)
