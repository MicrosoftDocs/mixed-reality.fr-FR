---
title: Audio en réalité mixte
description: L’audio en réalité mixte peut augmenter la confiance des utilisateurs dans les interactions entre les interfaces utilisateur et plonger les utilisateurs dans l’expérience.
author: kegodin
ms.author: kegodin
ms.date: 11/07/2019
ms.topic: article
keywords: son spatial, son surround, audio 3D, son 3D, son spatial
ms.openlocfilehash: 1930017903439aee3ac53b6c4be344fdc44c356f
ms.sourcegitcommit: 2e54d0aff91dc31aa0020c865dada3ae57ae0ffc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73641114"
---
# <a name="audio-in-mixed-reality"></a>Audio en réalité mixte
L’audio est un élément essentiel de la conception et de la productivité en réalité mixte, et peut :
* Augmentez la confiance des utilisateurs dans les interactions basées sur les gestes et les voix
* Guider les utilisateurs vers les étapes suivantes
* Combiner efficacement des objets virtuels avec le monde réel

Le suivi de la tête à faible latence des casques de réalité mixte, y compris HoloLens, permet l’utilisation de Spatialization HRTF de haute qualité. L’aménagement de l’audio dans votre application peut :
* Attirer l’attention sur les éléments visuels
* Aider les utilisateurs à prendre conscience de leur environnement réel

L’ajout de acoustiques connecte plus profondément les hologrammes au monde mixte et peut fournir des indications sur l’environnement et l’état de l’objet.

Pour obtenir des exemples plus détaillés de la conception à l’aide de l’audio, consultez [conception audio](spatial-sound-design.md).

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
        <td>Spatialization</td>
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

## <a name="using-sounds-in-mixed-reality"></a>Utilisation de sons dans une réalité mixte
[L’utilisation de sons en réalité mixte](spatial-sound-design.md) peut nécessiter une approche différente de celle des applications tactiles et du clavier et de la souris. Les décisions relatives à la conception de sons clés incluent les sons à spatialiser et les interactions à sonify. Ces décisions peuvent avoir un impact important sur la confiance des utilisateurs, la productivité et la courbe d’apprentissage.

### <a name="case-studies"></a>Études de cas
HoloTour prend pratiquement les utilisateurs sur des sites touristiques et historiques dans le monde entier. L’étude de cas suivante décrit la conception saine de HoloTour : [Sound Design pour HoloTour](case-study-spatial-sound-design-for-holotour.md). Un microphone spécial et une configuration de rendu ont été utilisés pour capturer les espaces de sujet.

RoboRaid est un tir à haute énergie pour HoloLens. L’étude de cas suivante décrit les choix de conception effectués pour garantir que l’audio spatial a été utilisé pour atteindre un effet spectaculaire : la [conception de sons pour RoboRaid](case-study-using-spatial-sound-in-roboraid.md).

## <a name="spatialization"></a>Spatialization
Spatialization est le composant directionnel du son spatial. Lors de l’utilisation d’une configuration Home cinéma 7,1, Spatialization est aussi simple que le panoramique entre les haut-parleurs forts. Mais avec un casque en réalité mixte, il est essentiel d’utiliser une technologie HRTF pour la précision et le confort. Windows propose des Spatialization basés sur HRTF, et cette prise en charge est accélérée par le matériel sur HoloLens 2.

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/aB3TDjYklmo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### <a name="should-i-spatialize"></a>Dois-je spatialiser ?
De nombreux sons dans les applications de réalité mixte tirent parti de Spatialization, qui tire un son de la tête de l’écouteur et le place dans le monde. Reportez-vous à la [conception de son spatial](spatial-sound-design.md) pour obtenir des suggestions sur les utilisations les plus efficaces de Spatialization dans votre application.

### <a name="spatializer-personalization"></a>Personnalisation de Spatializer
Les HRTFs manipulent les différences de niveau et de phase entre les oreilles à travers le spectre de fréquences. Ils sont basés sur des modèles physiques et des mesures de la tête humaine, du tors et des formes d’oreille (pinnae). Notre cerveau répond à ces différences pour donner une idée de la direction du son. 

Chaque individu a une forme d’oreille, une taille de tête et une position Ear uniques, donc les meilleurs HRTFs sont ceux qui se conforment à vous. HoloLens augmente la précision de la Spatialization en utilisant votre distance inter-pupille (IPD) à partir du casque pour ajuster la HRTFs pour la taille de la tête.

### <a name="spatializer-platform-support"></a>Prise en charge de la plateforme Spatializer
Windows offre Spatialization, y compris HRTFs, via l' [API ISpatialAudioClient](https://docs.microsoft.com/windows/win32/coreaudio/spatial-sound). Cette API expose l’accélération matérielle HoloLens 2 HRTF aux applications.

### <a name="spatializer-middleware-support"></a>Prise en charge de l’intergiciel Spatializer
La prise en charge de Windows HRTFs est disponible pour certains moteurs audio tiers :
* Un plug-in de [moteur audio Unity](spatial-sound-in-unity.md) appelle le XAPO HRTF
* Un [plug-in de moteur audio Wwise](https://www.audiokinetic.com/products/plug-ins/msspatial/) appelle l’API ISpatialAudioClient

## <a name="acoustics"></a>Acoustiques
L’audio spatial peut être plus ou moins que la direction. Les autres dimensions, y compris l’occlusion, l’obstruction, la réverbération, le portail et la modélisation source, sont collectivement appelées « acoustiques ». Sans acoustiques, les sons spatiaux n’ont pas une distance perçue.

Le traitement des acoustiques peut aller du simple au très complexe. En utilisant un verbe simple, tel que celui pris en charge par n’importe quel moteur audio, vous pouvez envoyer des sons spatiaux dans l’environnement qui entoure l’écouteur. Le traitement des acoustiques plus riches et plus attrayant est disponible à partir de systèmes acoustiques tels que les [acoustiques de projet](https://aka.ms/acoustics). Les acoustiques de projet peuvent modéliser l’effet des murs, des portes et d’autres géométries de scène sur un son, et est une option efficace pour les cas où la géométrie de scène appropriée est connue au moment du développement.

