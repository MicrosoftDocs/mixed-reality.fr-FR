---
title: Qu’est-ce qu’un hologramme ?
description: HoloLens vous permet de consultez et interagissez avec hologrammes en trois dimensions, les objets rendus de lumière et son qui apparaissent dans le monde.
author: beaufolsom
ms.author: befolsom
ms.date: 03/21/2018
ms.topic: article
keywords: Réalité mixte Windows, HoloLens, hologrammes, conception, interaction
ms.openlocfilehash: 714b08db23aa641252291aebe89fa3059c209a6f
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829784"
---
# <a name="what-is-a-hologram"></a>Qu’est-ce qu’un hologramme ?

HoloLens vous permet de créer **hologrammes**, objets effectuée de la lumière et son qui apparaissent dans le monde, simplement comme si elles étaient des objets réels. Hologrammes répondent à votre [les regards](gaze.md), [mouvements](gestures.md) et [commandes vocales](voice-input.md)et interagir avec elles [réalistes surfaces](spatial-mapping.md) autour de vous. Avec hologrammes, vous pouvez créer des objets numériques qui font partie de votre monde.

<br>

>[!VIDEO https://www.youtube.com/embed/MVXH5V8MVQo]

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1er gen)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
    </tr>
     <tr>
        <td>Hologrammes</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

## <a name="a-hologram-is-made-of-light-and-sound"></a>Un hologramme est constitué de lumière et son

Les hologrammes ce HoloLens [restitue](rendering.md) apparaissent dans le frame HOLOGRAPHIQUE directement devant les yeux de l’utilisateur. Hologrammes ajouter lumière à votre monde, ce qui signifie que vous voyez la lumière à partir de l’affichage et la lumière à partir de votre environnement. HoloLens ne supprime pas clair à partir de vos yeux, donc vntana ne peut pas être restitué avec la couleur noir. Au lieu de cela, contenu noir apparaît comme étant transparent.

Hologrammes peuvent avoir de nombreux différentes apparences et des comportements. Certains sont réalistes et solide, et d’autres regorge et ethereal. Hologrammes peuvent mettre en évidence les fonctionnalités dans votre environnement, et ils peuvent être des éléments dans l’interface utilisateur de votre application.

![Chien HOLOGRAPHIQUE parcours sur le sol](images/fang3-640px.jpg)

Hologrammes peuvent également rendre [sons](spatial-sound.md), qui apparaissent proviennent d’un emplacement spécifique dans votre environnement. Sur HoloLens, sembler provient de deux intervenants qui sont trouvent directement au-dessus de vos oreilles, sans les aborder. Comme pour les affichages, les haut-parleurs sont additifs, introduire de nouveaux sons sans bloquer les sons de votre environnement.

## <a name="a-hologram-can-be-placed-in-the-world-or-tag-along-with-you"></a>Un hologramme peut être placé dans le monde ou la balise avec vous

Quand vous avez un emplacement particulier dans lequel vous souhaitez un hologramme, vous pouvez [placer](coordinate-systems.md) celui-ci précisément dans le monde. Comme vous guider autour de ce HOLOGRAMME, celle-ci apparaîtra stable par rapport au monde. Si vous utilisez un [ancre spatial](coordinate-systems.md#spatial-anchors) pour épingler cet objet fermement au monde, le système peut même pas se souvenir où vous vous étiez lorsque vous y revenir plus tard.

![Maquette de construction HOLOGRAPHIQUE assis sur une table](images/image5-640px.png)

Certains hologrammes suivent l’utilisateur à la place. Ces hologrammes tag-along se positionnement par rapport à l’utilisateur, peu importe où ils remonter. Vous pouvez même choisir mettre un hologramme avec vous pour un certain temps et les placer sur le mur une fois que vous obtenez une autre salle.

**Bonnes pratiques**
* Certains scénarios peuvent exiger que hologrammes restent visibles tout au long de l’expérience ou facilement détectables. Il existe deux approches générales pour ce type de positionnement. Appelons-les **« affichage-verrouillé »** et **« corps-verrouillé »** .
   * Verrouillé en affichage de contenu est par position « verrouillé » pour l’affichage du périphérique. C’est difficile pour de nombreuses raisons, y compris un sentiment non naturelle de « clingyness », ce qui rend les nombreux utilisateurs frustrés et que vous souhaitiez « renoncer il. » En règle générale, plusieurs concepteurs ont trouvé préférable d’éviter le verrouillage d’écran de contenu.
   * L’approche de verrouillage de corps est beaucoup plus non remboursable sous conditions. Le verrouillage de corps est quand un hologramme est attaché au corps de l’utilisateur ou du pointage de regard vecteur, mais il est positionné dans l’espace 3d autour de l’utilisateur. Nombreuses expériences ont adopté un comportement de verrouillage de corps dans lequel l’hologramme « suit « l’utilisateurs du pointage de regard, ce qui permet à l’utilisateur faire pivoter de leur corps et déplacer dans l’espace sans perdre l’hologramme. Incorporer un délai vous aide à la circulation hologramme sembler plus naturelle. Par exemple, certains core l’interface utilisateur du système d’exploitation Windows HOLOGRAPHIQUE utilise une variante sur le verrouillage par un organisme qui suit le regard de l’utilisateur avec un délai gentiment et élastique de type tandis que l’utilisateur Active leur tête.
* Placez l’hologramme à distance à l’aise affichage généralement environ 1 à 2 mètres de la tête.
* Fournir un montant de dérive des éléments ou qui doivent être en permanence dans le frame HOLOGRAPHIQUE, envisagez d’animation de votre contenu à un côté de l’affichage lorsque l’utilisateur modifie son point de vue.

**Placez hologrammes dans la zone optimale - entre 1,25 m et 5m**

Deux compteurs est le plus optimal et l’expérience dégradera vous approchez d’un compteur. À des distances proche à un mètre, hologrammes déplacement régulièrement en profondeur sont plus susceptibles d’être problématique que hologrammes STATIONNAIRES. Envisagez normalement découpage ou fondu votre contenu lorsqu’il atteint trop étroite pour autant jar de l’utilisateur dans une expérience inattendue.

![Distance optimale pour placer hologrammes à partir de l’utilisateur.](images/distanceguiderendering-640px.png)

## <a name="a-hologram-interacts-with-you-and-your-world"></a>Un hologramme interagit avec vous et votre monde

Hologrammes ne sont pas uniquement sur la lumière et son ; elles sont également une partie de votre monde active. Regard sur un hologramme et le mouvement de votre part, et un hologramme peut commencer à vous suivre. Donnez une commande de voix à un hologramme et il peut répondre.

![Conception de moto HOLOGRAPHIQUE munie d’un corps de la vie réelle motorcycle](images/image8-640px.png)

Hologrammes autoriser des interactions personnelles qui ne sont pas possibles ailleurs. Étant donné que le HoloLens sache où c’est dans le monde, un caractère HOLOGRAPHIQUE peut vous trouver directement dans les yeux au cours d’autour de la pièce.

Un hologramme peut également interagir avec votre environnement. Par exemple, vous pouvez placer une balle en mouvement HOLOGRAPHIQUE au-dessus d’une table. Ensuite, avec un [appui en l’air](gestures.md#air-tap), regardez la boule de rebond et de rendre son lorsqu’il atteint la table.

Hologrammes peuvent également être bloqués par des objets du monde réel. Par exemple, un caractère HOLOGRAPHIQUE peut remonter via une porte et derrière un mur, hors de votre vue.

**Conseils pour l’intégration hologrammes et le monde réel**
* Alignement des règles gravitationnelle facilite hologrammes à se rapportent à et plus crédibles. Par exemple : Placer un chien HOLOGRAPHIQUE sur le sol & un vase sur la table plutôt que des flottant dans l’espace.
* Nombreux concepteurs ont constaté qu’ils peuvent être encore plus believably intégrés hologrammes en créant un « négatif fantôme » sur l’aire du hologramme s’appuie sur. Pour cela, ils devez création d’un éclat de manière réversible sur le sol autour de l’hologramme, puis en soustrayant le « fantôme » à partir de l’éclat. L’éclat de manière réversible s’intègre à la lumière dans le monde réel et les clichés instantanés pour des motifs l’hologramme dans l’environnement.

## <a name="a-hologram-is-whatever-you-dream-up"></a>Un hologramme est tout ce qui vous procure

En tant que HOLOGRAPHIQUE développeur, vous avez la possibilité d’arrêter votre créativité en dehors d’écrans 2D et dans le monde. Types de données *vous* créer ?

![HOLOGRAPHIQUE world imaginaire dans salon](images/designoverview.jpg)

## <a name="see-also"></a>Voir aussi
* [Son spatial](spatial-sound.md)
* [Couleurs, éclairage et matériaux](color,-light-and-materials.md)
