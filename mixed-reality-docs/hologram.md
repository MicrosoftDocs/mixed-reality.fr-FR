---
title: Qu’est-ce qu’un hologramme ?
description: HoloLens vous permet d’afficher et d’interagir avec des hologrammes à trois dimensions, des objets composés de lumière et de son qui s’affichent dans le monde autour de vous.
author: beaufolsom
ms.author: befolsom
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, HoloLens, hologrammes, conception, interaction
ms.openlocfilehash: 714b08db23aa641252291aebe89fa3059c209a6f
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829784"
---
# <a name="what-is-a-hologram"></a>Qu’est-ce qu’un hologramme ?

HoloLens vous permet de créer des hologrammes, des objets composés de lumière et de son qui s’affichent partout dans le monde, comme s’il s’agissait d’objets réels. Les hologrammes répondent à [vos](gaze.md)commandes de pointage, de [mouvement](gestures.md) et de [voix](voice-input.md)et peuvent interagir avec des [surfaces réelles](spatial-mapping.md) autour de vous. Avec les hologrammes, vous pouvez créer des objets numériques qui font partie de votre monde.

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
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Hologrammes</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

## <a name="a-hologram-is-made-of-light-and-sound"></a>Un hologramme est composé de lumière et de son

Les hologrammes que le [contrôle HoloLens affiche](rendering.md) dans le cadre holographique directement devant les yeux de l’utilisateur. Les hologrammes ajoutent de la lumière à votre monde, ce qui signifie que vous voyez la lumière de l’écran et la lumière de votre environnement. HoloLens ne disposant pas de lumière sur vos yeux, les hologrammes ne peuvent pas être rendus avec la couleur noire. Au lieu de cela, le contenu noir apparaît comme transparent.

Les hologrammes peuvent avoir de nombreuses apparences et comportements différents. Certains sont réalistes et solides, tandis que d’autres sont animés et Ethereal. Les hologrammes peuvent mettre en évidence des fonctionnalités dans votre environnement et peuvent être des éléments de l’interface utilisateur de votre application.

![Chien holographique marchant à l’étage](images/fang3-640px.jpg)

Les hologrammes peuvent également créer des [sons](spatial-sound.md)qui semblent provenir d’un emplacement spécifique dans votre environnement. Sur HoloLens, le son provient de deux enceintes situées directement au-dessus de vos oreilles, sans les couvrir. Comme pour les écrans, les haut-parleurs sont additifs, ce qui introduit de nouveaux sons sans bloquer les sons de votre environnement.

## <a name="a-hologram-can-be-placed-in-the-world-or-tag-along-with-you"></a>Un hologramme peut être placé dans le monde entier ou dans la balise avec vous

Si vous avez un emplacement particulier où vous souhaitez un hologramme, vous pouvez le [Placer](coordinate-systems.md) précisément dans le monde entier. Au fur et à mesure que vous parcourez Cet hologramme, il apparaîtra stable par rapport au monde entier. Si vous utilisez une [ancre spatiale](coordinate-systems.md#spatial-anchors) pour épingler cet objet fermement au monde, le système peut même se souvenir de l’endroit où vous l’avez laissé lorsque vous revenez plus tard.

![Construction holographique maquette assis sur une table](images/image5-640px.png)

Certains hologrammes suivent l’utilisateur à la place. Ces hologrammes se déplacent eux-mêmes par rapport à l’utilisateur, quel que soit l’endroit où ils parcourent. Vous pouvez même choisir de placer un hologramme avec vous pendant un certain temps, puis le placer sur le mur une fois que vous êtes dans une autre pièce.

**Bonnes pratiques**
* Certains scénarios peuvent exiger que les hologrammes restent facilement détectables ou visibles tout au long de l’expérience. Il existe deux approches de haut niveau pour ce type de positionnement. Appelons-les **«** éléments verrouillés» et **«verrouillés en corps»** .
   * Le contenu verrouillé en affichage est positionné de façon «verrouillée» sur l’écran de l’appareil. Cela est délicat pour plusieurs raisons, notamment un sentiment de «clingyness» innaturel qui rend beaucoup d’utilisateurs frustrés et souhaitant les «secouer». En général, de nombreux concepteurs ont trouvé mieux qu’ils évitent le verrouillage du contenu.
   * L’approche verrouillée par le corps est beaucoup plus forgivable. Le verrouillage du corps est lorsqu’un hologramme est attaché au corps ou au vecteur de pointage de l’utilisateur, mais est positionné dans l’espace 3D autour de l’utilisateur. De nombreuses expériences ont adopté un comportement de verrouillage du corps où l’hologramme «suit» les utilisateurs pointant vers le regard, ce qui permet à l’utilisateur de faire pivoter son corps et de parcourir l’espace sans perdre l’hologramme. L’incorporation d’un délai permet d’obtenir un mouvement d’hologramme plus naturel. Par exemple, une interface utilisateur principale du système d’exploitation Windows holographique utilise une variation sur le verrouillage du corps qui suit le point d’arrêt de l’utilisateur avec un délai léger et élastique, tandis que l’utilisateur change de tête.
* Placez l’hologramme à une distance confortable, généralement d’environ 1-2 mètres de l’en-tête.
* Fournissez une quantité de dérive pour les éléments qui doivent être continuellement dans le frame holographique ou envisagez d’animer votre contenu sur un côté de l’affichage lorsque l’utilisateur modifie son point de vue.

**Placer des hologrammes dans la zone optimale, entre 1,25 m et 5 m**

Deux compteurs sont les plus optimaux, et l’expérience dégradera la plus proche d’un compteur. À des distances près d’un mètre, les hologrammes qui se déplacent régulièrement sont plus susceptibles d’être problématiques que les hologrammes fixes. Envisagez de découper ou de détourer votre contenu en douceur quand il est trop proche, ce qui ne permet pas à l’utilisateur d’être confronté à une expérience inattendue.

![Distance optimale pour le placement des hologrammes de l’utilisateur.](images/distanceguiderendering-640px.png)

## <a name="a-hologram-interacts-with-you-and-your-world"></a>Un hologramme interagit avec vous et votre monde

Les hologrammes ne sont pas uniquement à l’égard du clair et du son. ils sont également une partie active de votre monde. Pointez le regard sur un hologramme et un geste avec votre main, et un hologramme peut commencer à vous suivre. Donnez une commande vocale à un hologramme, qui peut répondre.

![Conception de motocyclettes holographiques placée sur un véhicule de motocyclette](images/image8-640px.png)

Les hologrammes permettent des interactions personnelles qui ne sont pas possibles ailleurs. Étant donné que le HoloLens sait où il se trouve dans le monde, un caractère holographique peut vous paraître directement dans les yeux à mesure que vous parcourez la salle.

Un hologramme peut également interagir avec votre environnement. Par exemple, vous pouvez placer une boule de rebond holographique au-dessus d’un tableau. Ensuite, à l’aide d’un [robinet](gestures.md#air-tap), regardez la balle rebondir et émettez un son lorsqu’il atteint le tableau.

Les hologrammes peuvent également être bloqués par des objets réels. Par exemple, un caractère holographique peut parcourir une porte et derrière un mur, en dehors de votre vue.

**Conseils pour l’intégration des hologrammes et du monde réel**
* L’alignement sur les règles gravitationnelles facilite la liaison des hologrammes à et plus crédible. par exemple Placez un chien holographique sur le sol & un vase sur la table plutôt que de les faire flotter dans l’espace.
* De nombreux concepteurs ont constaté qu’ils peuvent encore plus incroyablement intégrer des hologrammes en créant une «ombre négative» sur la surface sur laquelle l’hologramme est assis. Pour ce faire, ils créent une lueur douce sur le sol autour de l’hologramme, puis soustraient la «ombre» de la lueur. La lueur douce s’intègre à la lumière du monde réel et l’ombre aux raisons de l’hologramme dans l’environnement.

## <a name="a-hologram-is-whatever-you-dream-up"></a>Un hologramme est tout ce que vous rêvez

En tant que développeur holographique, vous avez la possibilité de scinder votre créativité en écrans 2D et dans le monde entier. Que allez- *vous* générer?

![Monde imaginaire imaginaire dans le salon](images/designoverview.jpg)

## <a name="see-also"></a>Voir aussi
* [Son spatial](spatial-sound.md)
* [Couleurs, éclairage et matériaux](color,-light-and-materials.md)
