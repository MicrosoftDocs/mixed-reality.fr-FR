---
title: Audio en réalité mixte
description: L’audio en réalité mixte peut augmenter la confiance des utilisateurs dans les interactions entre les interfaces utilisateur et plonger les utilisateurs dans l’expérience.
author: kegodin
ms.author: kegodin
ms.date: 11/07/2019
ms.topic: article
keywords: son spatial, son surround, audio 3D, son 3D, son spatial
ms.openlocfilehash: b939433daf80a95a11bc0e1ac2ffd75dfe0cf299
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75181979"
---
# <a name="audio-in-mixed-reality"></a>Audio en réalité mixte
L’audio est un élément essentiel de la conception et de la productivité dans la réalité mixte. Le son peut :
* Augmentez la confiance des utilisateurs dans les interactions entre les mouvements et les voix.
* Guidez les utilisateurs vers les étapes suivantes.
* Associez efficacement des objets virtuels au monde réel.

Le suivi de la tête à faible latence des casques de réalité mixte, y compris HoloLens, prend en charge les Spatialization de haute qualité HRTF. Vous pouvez spatialiser l’audio dans votre application pour :
* Attirez l’attention sur les éléments visuels.
* Aidez les utilisateurs à prendre conscience de leur environnement réel.

Les acoustiques connectent plus profondément les hologrammes au monde en réalité mixte. Il fournit des indications sur l’environnement et l’état de l’objet.

Consultez [des exemples détaillés de conception qui utilise l’audio](spatial-sound-design.md).

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
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (première génération)</strong></a></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Spatialisation</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
     <tr>
        <td>Accélération matérielle Spatialization</td>
        <td>❌</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

## <a name="use-of-sounds-in-mixed-reality"></a>Utilisation de sons dans une réalité mixte
[L’utilisation de sons dans une réalité mixte](spatial-sound-design.md) requiert une approche différente de celle des applications tactiles et du clavier et de la souris. Les décisions relatives à la conception de sons clés incluent les sons à spatialiser et les interactions à sonify. Ces décisions affectent fortement la confiance des utilisateurs, la productivité et la courbe d’apprentissage.

### <a name="case-studies"></a>Études de cas
HoloTour prend pratiquement les utilisateurs sur des sites touristiques et historiques dans le monde entier. Consultez l’étude [de cas Sound Design for HoloTour](case-study-spatial-sound-design-for-holotour.md) . Un microphone spécial et une configuration de rendu ont été utilisés pour capturer les espaces de sujet.

RoboRaid est un tir à haute énergie pour HoloLens. L’étude [de cas de conception audio pour RoboRaid](case-study-using-spatial-sound-in-roboraid.md) décrit les choix de conception qui ont été effectués pour garantir que l’audio spatial était utilisé à l’effet le plus spectaculaire.

## <a name="spatialization"></a>Spatialisation
Spatialization est le composant directionnel du son spatial. Pour une configuration 7,1 Home cinéma, Spatialization est aussi simple que le panoramique entre les haut-parleurs. Mais pour le casque en réalité mixte, il est essentiel d’utiliser une technologie HRTF pour la précision et le confort. Windows propose des Spatialization basés sur HRTF, et cette prise en charge est accélérée par le matériel sur HoloLens 2.

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/aB3TDjYklmo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### <a name="should-i-spatialize"></a>Dois-je spatialiser ?
Spatialization peut améliorer de nombreux sons dans des applications en réalité mixte. Spatialization utilise un son en dehors de la tête de l’écouteur et le place dans le monde. Pour obtenir des suggestions sur l’utilisation effective de Spatialization dans votre application, consultez [conception de son spatial](spatial-sound-design.md).

### <a name="spatializer-personalization"></a>Personnalisation de Spatializer
Les HRTFs manipulent les différences de niveau et de phase entre les oreilles à travers le spectre de fréquences. Ils sont basés sur des modèles physiques et des mesures de la tête humaine, du tors et des formes d’oreille (pinnae). Notre cerveau répond à ces différences pour fournir un sens sonore.

Chaque individu a une forme auriculaire, une taille de tête et une position Ear uniques. Le meilleur HRTFs est donc conforme à vos exigences. Pour augmenter la précision de la Spatialization, HoloLens utilise votre distance inter-pupille (IPD) à partir du casque pour ajuster la HRTFs de la taille de la tête.

### <a name="spatializer-platform-support"></a>Prise en charge de la plateforme Spatializer
Windows offre Spatialization, y compris HRTFs, via l' [API ISpatialAudioClient](https://docs.microsoft.com/windows/win32/coreaudio/spatial-sound). Cette API expose l’accélération matérielle HoloLens 2 HRTF aux applications.

### <a name="spatializer-middleware-support"></a>Prise en charge de l’intergiciel Spatializer
La prise en charge de Windows HRTFs est disponible pour les moteurs audio tiers suivants.
* Un [plug-in de moteur audio Unity](spatial-sound-in-unity.md)
* Un [plug-in de moteur audio Wwise](https://www.audiokinetic.com/products/plug-ins/msspatial/)

## <a name="acoustics"></a>Acoustiques
Le son spatial est plus que la direction. Les autres dimensions incluent l’occlusion, l’obstruction, la réverbération, le portail et la modélisation source. Ces dimensions sont collectivement appelées « *acoustiques*». Sans acoustiques, les sons spatiaux n’ont pas de distance perçue.

Les traitements acoustiques vont du plus simple au plus complexe. Vous pouvez utiliser un verbe simple qui est pris en charge par n’importe quel moteur audio pour envoyer des sons spatiales dans l’environnement de l’écouteur. Les systèmes acoustiques, tels que les [acoustiques de projet](https://aka.ms/acoustics) , offrent un traitement des acoustiques plus riche et plus attrayant. Les acoustiques de projet peuvent modéliser l’effet des murs, des portes et d’autres géométries de scène sur un son. C’est une option efficace pour les cas où la géométrie de scène appropriée est connue au moment du développement.

## <a name="next-steps"></a>Étapes suivantes
- [Son spatial dans Unity](spatial-sound-in-unity.md)
- [Comment utiliser le son dans des applications en réalité mixte](spatial-sound-design.md)
