---
title: Son spatial
description: Le fait d’utiliser un son spatial dans une application de réalité mixte vous permet de placer des sons dans un espace 3D.
author: hak0n
ms.author: hakons
ms.date: 03/21/2018
ms.topic: article
keywords: son spatial, son surround, audio 3D, son 3D, son spatial
ms.openlocfilehash: 31ec8f88a060127daab9bf3afc970457ec7c90a3
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437394"
---
# <a name="spatial-sound"></a>Son spatial

Lorsque les objets sont hors de notre ligne de vue, l’un des moyens de savoir ce qui se passe nous est d’utiliser le son. Dans Windows Mixed Reality, le moteur audio fournit le composant d’acoustique de l’expérience de réalité mixte en simulant le son en 3D à l’aide de la direction, de la distance et des simulations environnementales. L’utilisation d’un son spatial dans une application permet aux développeurs de placer de manière convaincante des sons dans un espace à 3 Dimensions (sphère) autour de l’utilisateur. Ces sons semblent apparaître comme s’ils étaient issus d’objets physiques réels ou d’hologrammes de réalité mixte dans l’environnement de l’utilisateur. Étant donné que les [hologrammes](hologram.md) sont des objets en lumière et parfois des sons, le composant son permet d’obtenir des hologrammes de masse plus crédibles et de créer une expérience plus immersive.

Bien que les hologrammes ne puissent apparaître visuellement que le point de regard de l’utilisateur, le son de votre application peut provenir de toutes les directions ; au-dessus, en-dessous, en arrière-plan, etc. Vous pouvez utiliser cette fonctionnalité pour attirer l’attention sur un objet qui n’est peut-être pas actuellement dans la vue de l’utilisateur. Un utilisateur peut percevoir des sons provenant d’une source dans le monde de la réalité mixte. Par exemple, à mesure que l’utilisateur se rapproche d’un objet ou que l’objet s’y rapproche, le volume augmente. De même, lorsque les objets se déplacent sur un utilisateur, ou vice versa, les sons spatiaux donnent à l’illusion que les sons proviennent directement de l’objet.

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/PTPvx7mDon4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## <a name="device-support"></a>Périphériques pris en charge

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
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Son spatial</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️ (avec casque)</td>
    </tr>
</table>

## <a name="simulating-the-perceived-location-and-distance-of-sounds"></a>Simulation de l’emplacement et de la distance perçus des sons

En analysant la manière dont le son atteint à la fois nos oreilles, notre cerveau détermine la distance et la direction de l’objet émettant le son. Une HRTF (ou une fonction de transfert associée à l’en-tête) simule cette interaction en modélisant la réponse spectrale qui caractérise la façon dont une oreille reçoit du son à partir d’un point dans l’espace. Le moteur spatial audio utilise des HRTFs personnalisées pour étendre l’expérience de réalité mixte et simuler des sons provenant de différentes directions et distances.

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/aB3TDjYklmo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Les signaux audio gauche ou droit (azimut) proviennent de différences dans le temps que le son arrive à chaque oreille. Les signaux de début et de baisse proviennent des modifications spectrales produites par la forme de l’oreille externe (pinnae). En désignant l’origine de l’audio, le système peut simuler l’expérience du son arrivant à des moments différents de nos oreilles. Notez que sur HoloLens, alors que l’azimut Spatialization est personnalisé, la simulation d’élévation est basée sur un ensemble moyen de anthropometrics. Par conséquent, la précision de l’élévation peut être moins précise que la précision de l’azimut.

Les caractéristiques des sons changent également en fonction de l’environnement dans lequel ils se trouvent. Par exemple, si vous avez une cave, vous pouvez faire rebondir votre voix sur les murs, les planchers et les plafonds, créant ainsi un effet d’écho. Le paramètre de modèle de pièce du son spatial reproduit ces réflexions pour placer des sons dans un environnement audio particulier. Vous pouvez utiliser ce paramètre pour qu’il corresponde à l’emplacement réel de l’utilisateur pour la simulation de sons dans cet espace afin de créer une expérience audio plus immersive.

## <a name="integrating-spatial-sound"></a>Intégration du son spatial

Étant donné que le principe général de la réalité mixte consiste à utiliser des [hologrammes](hologram.md) à la terre dans le monde physique ou l’environnement virtuel de l’utilisateur, la plupart des sons des hologrammes doivent être spatiaux. Sur HoloLens, les considérations relatives au budget et à la mémoire sont naturellement prises en compte, mais vous pouvez utiliser des voix de son spatial 10-12 à cet endroit tout en utilisant moins de environ 12% de l’UC (environ 70% de l’un des quatre cœurs). L’utilisation recommandée pour les voix spatiales du son est la suivante :
* Le relief du point de vue (mise en surbrillance des objets, en particulier lorsqu’il est hors de l’affichage). Lorsqu’un hologramme a besoin de l’attention d’un utilisateur, jouez un son sur cet hologramme (par exemple, ayez un écorce de chien virtuel). Cela permet à l’utilisateur de Rechercher l’hologramme lorsqu’il n’est pas affiché.
* Haptiques audio (audio réactives pour les interactions tactiles). Par exemple, émettre un signal sonore lorsque la main ou le contrôleur de mouvement de l’utilisateur entre et quitte le cadre de mouvement. Ou émettre un signal sonore lorsque l’utilisateur sélectionne un hologramme.
* Immersion (sons ambiants entourant l’utilisateur).

Il est également important de noter que même si la fusion de sons stéréo standard avec un son spatial peut être efficace pour créer des environnements réalistes, les sons stéréo doivent être relativement calmes pour laisser de la place aux aspects subtils du son spatial, tels que les réflexions ( des signaux de distance) qui peuvent être difficiles à entendre dans un environnement bruyant.

Le moteur de sons spatiaux de Windows prend uniquement en charge un taux d’échantillonnage de 48K pour la lecture. La plupart des intergiciels (middleware), tels que Unity, convertissent automatiquement les fichiers audio dans le format pris en charge, mais lorsque vous utilisez des API audio Windows directement, vous devez faire correspondre le format du contenu au format pris en charge par l’effet.

## <a name="see-also"></a>Articles associés
* [MR spatial 220](holograms-220.md)
* [Son spatial dans Unity](spatial-sound-in-unity.md)
* [Son spatial dans DirectX](spatial-sound-in-directx.md)
* [Conception du son spatial](spatial-sound-design.md)
