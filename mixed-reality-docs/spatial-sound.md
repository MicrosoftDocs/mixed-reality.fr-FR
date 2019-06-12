---
title: Son spatial
description: À l’aide de son spatial dans une application de réalité mixte vous permet de placer convaincante des sons dans un espace 3D.
author: hak0n
ms.author: hakons
ms.date: 03/21/2018
ms.topic: article
keywords: spatial son son à effet surround, audio 3d, audio audio, spatial 3d
ms.openlocfilehash: a30a484c4e47593556fbd1786158262551e11d22
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829923"
---
# <a name="spatial-sound"></a>Son spatial

Lorsque les objets sont en dehors de notre ligne de vue, une des façons dont nous pouvons percevoir que se passe-t-il autour de nous est via son. En réalité mixte de Windows, le moteur audio fournit le composant auditif de l’expérience de réalité mixte en simulant les sons 3D à l’aide de la direction, la distance et les simulations de l’environnement. À l’aide de son spatial dans une application permet aux développeurs de placer convaincante des sons dans un espace tridimensionnel 3 (sphère) autour de l’utilisateur. Ces sons paraîtra comme si elles provenaient d’objets physiques réel ou les hologrammes de réalité mixte dans son environnement de l’utilisateur. Étant donné que [hologrammes](hologram.md) sont les objets de lumière et parfois audio, le composant audio permet de bout en bout hologrammes ce qui les rend plus crédibles et la création d’une expérience plus riche.

Bien que hologrammes ne peuvent apparaître visuellement où le regard de l’utilisateur pointe, les sons de votre application peuvent provenir de toutes les directions ; ci-dessus, ci-dessous, retard, sur le côté, etc. Vous pouvez utiliser cette fonctionnalité pour attirer l’attention sur un objet qui ne peut pas être actuellement dans la vue de l’utilisateur. Un utilisateur peut percevoir sons pour être émanant d’une source dans le monde de réalité mixte. Par exemple, lorsque l’utilisateur se rapproche un objet ou l’objet se rapproche les, le volume augmente. De même, comme objets déplacent autour d’un utilisateur, ou vice versa, sons spatiales donnent l’illusion que sons proviennent directement l’objet.

<br>

>[!VIDEO https://www.youtube.com/embed/PTPvx7mDon4]

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
        <td>Son spatial</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️ (avec un casque)</td>
    </tr>
</table>

## <a name="simulating-the-perceived-location-and-distance-of-sounds"></a>Simulation de l’emplacement perçue et la distance de sons

En analysant la façon dont le son atteint nos deux oreilles, notre cerveau détermine la distance et la direction de l’objet émettant le son. Un HRTF (ou une fonction de transfert Related Head) simule cette interaction en la réponse spectre qui caractérise la façon dont une oreille reçoit son à partir d’un point dans l’espace de modélisation. Le moteur audio spatial utilise des fonctions HRTF personnalisées pour développer l’expérience de réalité mixte, simuler les sons provenant de différentes instructions et des distances.

<br>

>[!VIDEO https://www.youtube.com/embed/aB3TDjYklmo]

Les signaux audio de gauche ou droit (AZIMUT) issus de différences dans le temps que son arrive à chaque oreille. Haut et bas de signaux issus de modifications spectrales produites par la forme d’une oreille externe (pinnae). En désignant où provenant de l’audio, le système peut simuler l’expérience du son qui arrivent à différents moments dans nos oreilles. Notez que HoloLens, tandis que les spatialisation AZIMUT sont personnalisée, la simulation d’élévation est basée sur un ensemble moyenne d’anthropometrics. Par conséquent, la précision d’élévation peut être moins précise que la précision de l’azimut.

Les caractéristiques de sons changent également en fonction de l’environnement dans lequel ils existent. Par exemple, trouver dans une caverne entraîne votre voix rebondit sur les murs, étages et des plafonds, création d’un effet d’écho. Le paramètre de modèle de salle de son spatial reproduit ces reflets pour placer des sons dans un environnement audio particulier. Vous pouvez utiliser ce paramètre pour faire correspondre l’emplacement l’utilisateur réel pour la simulation des sons dans cet espace pour créer une expérience audio plus riche.

## <a name="integrating-spatial-sound"></a>L’intégration de son spatial

Étant donné que le principe général de réalité mixte est au sol [hologrammes](hologram.md) dans le monde physique ou l’environnement virtuel de l’utilisateur, la plupart des sons à partir de hologrammes doivent être spatialized. Sur HoloLens, il sont naturellement processeur et mémoire considérations relatives aux budgets, mais vous pouvez utiliser 10-12 spatial audio voix il lors de l’utilisation inférieure à ~ 12 % de l’UC (environ 70 % d’un des quatre cœurs). Voix audio spatial conseillé d’utiliser sont les suivantes :
* Utilisation de mixage (objets, en particulier lorsque la vue de mise en surbrillance). Quand un hologramme a besoin d’attention de l’utilisateur, un signal sonore sur ce hologramme (par exemple, avoir un écorce chien virtuel). Cela permet à l’utilisateur de trouver l’hologramme lorsqu’il n’est pas dans la vue.
* HAPTIQUES audio (audio réactif pour les interactions sans contact). Par exemple, un signal sonore lorsque le contrôleur main ou de mouvement de l’utilisateur saisit et quitte l’image de mouvement. Ou un signal sonore lorsque l’utilisateur sélectionne un hologramme.
* Immersion (sons ambiantes autour de l’utilisateur).

Il est également important de noter que bien que les sons stéréo standards avec son spatial de fusion peut être efficace dans la création d’environnements réalistes, les sons stéréo doivent être relativement calme d’espace pour les aspects subtiles de son spatiaux, tels que des réflexions ( distance de signaux) qui peuvent être difficiles à entendre dans un environnement bruyant.

Moteur audio spatial des Windows prend uniquement en charge un taux d’échantillonnage 48 Ko pour la lecture. La plupart des intergiciels (middleware), par exemple, Unity, est automatiquement convertir les fichiers audio au format pris en charge, mais lorsque vous utilisez Windows Audio API directement mettez en correspondance le format du contenu au format pris en charge par l’effet.

## <a name="see-also"></a>Voir aussi
* [MR 220 Spatial](holograms-220.md)
* [Son spatial dans Unity](spatial-sound-in-unity.md)
* [Son spatial dans DirectX](spatial-sound-in-directx.md)
* [Conception du son spatial](spatial-sound-design.md)
