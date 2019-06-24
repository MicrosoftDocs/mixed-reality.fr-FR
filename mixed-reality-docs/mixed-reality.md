---
title: Ce qui est une réalité mixte ?
description: Cet article définit la réalité mixte et montre où les appareils AR et VR simples, ainsi que les appareils de réalité mixte Windows tels que Microsoft HoloLens et des casques IMMERSIFS Windows Mixed Reality, se trouvent dans le spectre de réalité mixte.
author: BrandonBray
ms.author: branbray
ms.date: 03/21/2018
ms.topic: article
keywords: réalité mixte, HOLOGRAPHIQUE, ar, vr, mr, xr, réalité augmentée, réalité virtuelle, explication
ms.openlocfilehash: fbac8176b36cf28673dd9633cc059e5856a50296
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67326313"
---
# <a name="what-is-mixed-reality"></a>Ce qui est une réalité mixte ?

Réalité mixte est le résultat du mélange du monde physique avec le monde numérique. Réalité mixte est la prochaine évolution de l’interaction homme, ordinateur et l’environnement et déverrouille les possibilités qui jusqu'à présent étaient limitées à notre imaginations. Il est rendu possible par des améliorations dans la vision par ordinateur, de puissance de traitement graphique, la technologie d’affichage et les systèmes d’entrée. Le terme *une réalité mixte* a été introduite initialement dans un livre de 1994 par Paul Milgram et Fumio Kishino, «[une taxonomie de mixte affiche Visual réalité](http://etclab.mie.utoronto.ca/people/paul_dir/IEICE94/ieice.html). » Leur livre a introduit le concept de la *continuum de virtuality*et axée sur l’affichage de la catégorisation de classification appliquée à. Depuis lors, l’application de réalité mixte va au-delà d’affiche. Il inclut également l’entrée de l’environnement, son spatial et emplacement.

## <a name="environmental-input-and-perception"></a>Perception et l’entrée de l’environnement

![Diagramme de Venn montrant les interactions entre les ordinateurs, les êtres humains et les environnements](images/mixed-reality-venn-diagram-300px.png)<br> 

Dernières décennies, la relation entre l’homme et d’entrée a été bien explorée. Il a même une discipline étudiée appelée *interaction humaine ordinateur* ou HCL. Une entrée humaine se produit via une variété de moyens, notamment les claviers, souris, tactile, l’encre, voix et même le suivi de squelette Kinect.

Des améliorations dans les capteurs et de traitement sont donnant lieu à une nouvelle zone d’entrée de l’ordinateur à partir d’environnements. L’interaction entre les environnements et les ordinateurs est compréhension efficacement l’environnement ou *perception*. Par conséquent, les noms d’API dans Windows qui révèlent des informations de l’environnement sont appelés les [perception API](https://docs.microsoft.com/uwp/api/Windows.Perception). Entrée environnementale capture des éléments tels que de la position d’une personne dans le monde (par exemple, [suivi principal](coordinate-systems.md)), des limites et des surfaces (par exemple, [mappage spatial](spatial-mapping.md) et [compréhension spatiale](case-study-expanding-the-spatial-mapping-capabilities-of-hololens.md)), d’éclairage ambiant, son environnement, reconnaissance d’objet et l’emplacement.

À présent, la combinaison de tous les ordinateurs de trois--traitement, une entrée humaine et l’environnement entrée--définit la possibilité de créer des expériences de réalité mixte true. Mouvement à travers le monde physique peut se traduire pour le déplacement dans le monde numérique. Limites dans le monde physique peuvent influencer les expériences d’applications, telles que la partie, le monde numérique. Sans intervention de l’environnement, les expériences ne peut pas blend entre réalités physiques et numériques.

## <a name="the-mixed-reality-spectrum"></a>Le spectre de réalité mixte

Étant donné que la réalité mixte fusionne les mondes physique et numérique, ces deux réalités définissent les terminaisons polaires spectre appelé le continuum virtuality. Par souci de simplicité, nous faisons référence à ce que le *spectre de réalité mixte*. Sur le côté gauche, nous avons réalité physique dans lequel nous, humains, existe ; dans la partie droite, nous avons la réalité numérique correspondante.

<br>

>[!VIDEO https://www.youtube.com/embed/_xpI0JosYUk]

Aujourd'hui, la plupart des téléphones mobiles sur le marché n’ont peu à aucuns possibilités de présentation de l’environnement. Par conséquent, les expériences que proposent-ils Impossible de mélanger entre réalités physiques et numériques. Les expériences superposer des graphiques sur les flux vidéo du monde physique sont *une réalité augmentée*. Les expériences occlude votre vue pour présenter une expérience numérique sont *réalité virtuelle*. Comme vous pouvez le voir, les expériences activées entre ces deux extrêmes est *une réalité mixte*:
* En commençant par le monde physique, placer un objet numérique, comme un hologramme, comme si elle est vraiment là.
* En commençant par le monde physique, une représentation numérique d’une autre personne--un avatar--indique l’emplacement où ils ont été permanent en quittant les notes de publication. En d’autres termes, les expériences qui représentent une collaboration asynchrone à différents moments dans le temps.
* Les limites physiques du monde physique, tels que des murs et meubles, en commençant avec un monde numérique, apparaissent numériquement au sein de l’expérience pour aider les utilisateurs à éviter des objets physiques.

![Le spectre de réalité mixte](images/mixed-reality-spectrum-550px.png)

Plus la réalité augmentée et offres de réalité virtuelle disponibles aujourd'hui représentent une très petite partie de cette gamme. Ils sont, toutefois, des sous-ensembles de la plus grande gamme de réalité mixte. Windows 10 est généré avec la gamme complète à l’esprit et permet la fusion des représentations numériques des personnes, des lieux et des objets avec le monde réel.

![Types d’appareils dans le spectre de réalité mixte](images/mixed-reality-spectrum-device-types-550px.png)

Il existe deux principaux types d’appareils qui délivrent des expériences Windows Mixed Reality :
1. **Appareils HOLOGRAPHIQUE.** Ceux-ci sont caractérisés par la capacité du périphérique pour placer le contenu numérique dans le monde réel comme s’il s’agissait vraiment il.
2. **Appareils immersives.** Ceux-ci sont caractérisés par la capacité du périphérique pour créer une idée de la « présence »--masquage du monde physique et en la remplaçant par une expérience numérique.

<table>
<tr>
<th width="20%"> Caractéristique</th><th width="40%"> Appareils HOLOGRAPHIQUE</th><th width="40%"> Appareils immersives</th>
</tr><tr>
<td> Appareil de l’exemple</td><td> Microsoft HoloLens<br /> <img alt="Microsoft HoloLens image" width="300" height="169" src="images/mshololens-hero1-whitbg-rgb-300px.png" /></td><td> Windows Acer mixte réalité Development Edition<br /> <img alt="Acer Windows Mixed Reality Development Edition image" width="300" height="169" src="images/acer-windows-mixed-reality-development-edition-headset-300px.jpg" /></td>
</tr><tr>
<td> Écran</td><td> <i>Affichage transparente.</i> Permet à l’utilisateur afficher l’environnement physique tout en portant le casque.</td><td> <i>Affichage opaque.</i> Blocs de l’environnement physique tout en portant le casque.</td>
</tr><tr>
<td> Déplacement</td><td> Complète le déplacement des six degrés de liberté, rotation et traduction.</td><td> Complète le déplacement des six degrés de liberté, rotation et traduction.</td>
</tr>
</table>

Notez que, si un appareil est connecté à ou attaché à un PC distinct (via un câble USB ou Wi-Fi), soit il autonome ne (illimité) ne reflète pas si un appareil est HOLOGRAPHIQUE ou immersives. Certainement, responsable des fonctionnalités qui améliorent la mobilité pour une meilleure expérience et HOLOGRAPHIQUES et immersives appareils peut être attachés ou disposerez.

## <a name="devices-and-experiences"></a>Appareils et expériences

Progrès technologique est ce qui a activé les expériences de réalité mixte. Il n’existe aucun appareil aujourd'hui qui permettre exécuter des expériences dans tout le spectre entier. Toutefois, Windows 10 fournit une plateforme commune de réalité mixte pour les développeurs et les fabricants d’appareils. Appareils aujourd'hui peuvent prendre en charge une plage spécifique dans le spectre de réalité mixte. Au fil du temps, les nouveaux appareils seront développe cette plage. À l’avenir, HOLOGRAPHIQUE appareils sera plus riche, et appareils immersives deviendront plus HOLOGRAPHIQUES.

![Où les périphériques de disposer de la gamme de réalité mixte](images/mixed-reality-spectrum-device-placement-550px.png)

Souvent, il est préférable d’envisager le type d’expérience d’une application ou développeur de jeux souhaite créer. Les expériences ciblera généralement un point spécifique ou une partie de la gamme. Ensuite, les développeurs doivent envisager les capacités des appareils, qu'ils souhaitent cibler. Par exemple, les expériences qui s’appuient sur le monde physique exécutera meilleures sur HoloLens.
* **Vers la gauche (en réalité physique).** Les utilisateurs sont toujours présents dans leur environnement physique et ne sont jamais effectués de croire qu’ils ont quitté cet environnement.
* **L’intercepteur (réalité mixte entièrement).** Ces expériences blend le monde réel et le monde numérique. Les personnes ont vu le film [Jumanji](https://en.wikipedia.org/wiki/Jumanji) peuvent également rapprocher la façon dont la structure physique de la maison où l’histoire a eu lieu a été fusionnée avec un environnement de jungle.
* **Vers la droite (en réalité numérique).** Les utilisateurs rencontrer un environnement totalement au numérique et n’ont pas conscience de ce qui se produit dans l’environnement physique autour d’elles.


## <a name="see-also"></a>Voir aussi
* [Référence de l’API : Windows.Perception](https://docs.microsoft.com/uwp/api/Windows.Perception)
* [Référence de l’API : Windows.Perception.Spatial](https://docs.microsoft.com/uwp/api/Windows.Perception.Spatial)
* [Référence de l’API : Windows.Perception.Spatial.Surfaces](https://docs.microsoft.com/uwp/api/Windows.Perception.Spatial.Surfaces)
