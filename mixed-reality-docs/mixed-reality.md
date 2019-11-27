---
title: Qu’est-ce que la réalité mixte ?
description: Cet article définit la réalité mixte et démontre où les périphériques simples de type AR et VR, ainsi que les appareils Windows Mixed Reality, tels que Microsoft HoloLens et les casques immersifs de la réalité mixte Windows, se trouvent dans le spectre de la réalité mixte.
author: BrandonBray
ms.author: branbray
ms.date: 03/21/2018
ms.topic: article
keywords: réalité mixte, holographique, AR, VR, Mr, XR, réalité augmentée, réalité virtuelle, explication
ms.openlocfilehash: 65588902565ee0c5a1710f823311ccdecc23230e
ms.sourcegitcommit: 83698638b93c5ba77b3ffc399f1706482539f27b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74539558"
---
# <a name="what-is-mixed-reality"></a>Qu’est-ce que la réalité mixte ?

![Pointer et valider avec des mains sur HoloLens 2](images/02_MixedRealitySlashMixedReality.png)

La réalité mixte est le résultat de la fusion du monde physique avec le monde numérique. Prochaine évolution de l’interaction entre l’utilisateur, l’ordinateur et l’environnement, la réalité mixte permet de donner libre cours à nos imaginations. Elle est rendue possible grâce à l’évolution de la vision par ordinateur, de la puissance de traitement graphique, de la technologie d’affichage et des systèmes d’entrée. Le terme « *réalité mixte* » a été introduit à l’origine dans un document de 1994 par Paul Milgram et Fumio Kishino, «[une taxonomie du visuel de la réalité mixte » s’affiche](https://etclab.mie.utoronto.ca/people/paul_dir/IEICE94/ieice.html). Leur document a introduit le concept de *continuum de virtualisation*et s’est concentré sur la manière dont la catégorisation de taxonomie appliquée s’affiche. Depuis, l’application de la réalité mixte va au-delà des affichages. Il comprend également les entrées environnementales, le son spatial et l’emplacement.

![le spectre de la réalité mixte](images/MixedRealitySpectrum-worlds.jpg)<br>
*La réalité mixte est le résultat de la fusion du monde physique avec l’univers numérique.*

<br>

---

## <a name="environmental-input-and-perception"></a>Entrée et perception environnementales

Au cours des dernières décennies, la relation entre les entrées de l’homme et de l’ordinateur a été bien explorée. Il a même une discipline largement étudiée appelée *interaction des ordinateurs humains* ou HCI. L’entrée humaine s’effectue par le biais de différents moyens, y compris les claviers, les souris, les fonctions tactiles, l’encre, la voix et même le suivi squelettique Kinect.

Les avancées dans les capteurs et le traitement sont une nouvelle zone d’entrée d’ordinateur à partir d’environnements. L’interaction entre les ordinateurs et les environnements est une compréhension ou une *perception*efficace de l’environnement. Par conséquent, les noms d’API dans Windows qui révèlent des informations environnementales sont appelés des [API de perception](https://docs.microsoft.com/uwp/api/Windows.Perception). Les entrées environnementales capturent des éléments tels que la position d’une personne dans le monde (par exemple, le [suivi des têtes](coordinate-systems.md)), les surfaces et les limites (par exemple, le [mappage spatial](spatial-mapping.md) et la [compréhension des scènes](scene-understanding.md)), l’éclairage ambiant, le son ambiant, la reconnaissance d’objets, et l’emplacement.

<br>



:::row:::
    :::column:::
        À présent, la combinaison de la totalité du**traitement des ordinateurs, de l’entrée humaine et de l’environnement d’entrée**, définit la possibilité de créer de véritables expériences de réalité mixte. Le déplacement dans le monde physique peut se traduire par le mouvement dans le monde numérique. Les limites du monde physique peuvent influencer l’expérience des applications, telles que la lecture du jeu, dans le monde numérique. Sans entrée environnementale, les expériences ne peuvent pas être mélangées entre les réalités physiques et numériques.<br>
        <br>
        *Image : les interactions entre les ordinateurs, les êtres humains et les environnements.*
    :::column-end:::
        :::column:::
       ![Diagramme de Venn montrant les interactions entre les ordinateurs, les êtres humains et les environnements](images/mixed-reality-venn-diagram-300px.png)<br> 
    :::column-end:::
:::row-end:::

<br>

---


## <a name="the-mixed-reality-spectrum"></a>Le spectre de la réalité mixte

Étant donné que la réalité mixte fusionne des mondes physiques et numériques, ces deux réalités définissent les extrémités polaires d’un spectre appelé continuum de virtualisation. Pour plus de simplicité, nous faisons référence à ceci comme le spectre de la *réalité mixte*. Sur le côté gauche, nous avons une réalité physique dans laquelle nous avons des êtres humains ; sur le côté droit, nous avons la réalité numérique correspondante.

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/_xpI0JosYUk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

### <a name="augmented-vs-virtual-reality"></a>Augmentation et réalité virtuelle

La plupart des téléphones portables sur le marché n’ont pas de capacités de compréhension de l’environnement. Ainsi, les expériences qu’ils offrent ne peuvent pas se mélanger entre les réalités physiques et numériques. Les expériences qui superposent des graphiques sur les flux vidéo du monde physique sont une *réalité augmentée*. Les expériences qui occultait votre vue pour présenter une expérience numérique sont la *réalité virtuelle*. Comme vous pouvez le voir, les expériences activées entre ces deux extrêmes sont la *réalité mixte*:
* En commençant par le monde physique, en plaçant un objet numérique, tel qu’un hologramme, comme s’il était vraiment là.
* À partir de l’univers physique, une représentation numérique d’une autre personne (un avatar) indique l’emplacement où ils se trouvaient lors de la sortie des notes. En d’autres termes, les expériences qui représentent la collaboration asynchrone à différents moments.
* À partir d’un monde numérique, les limites physiques du monde physique, telles que les murs et les meubles, apparaissent numériquement dans l’expérience pour aider les utilisateurs à éviter les objets physiques.


<br>

![le spectre de la réalité mixte](images/MixedRealitySpectrum.jpg)<br>
*Le spectre de la réalité mixte*

<br>

La plupart des offres de réalité et de réalité virtuelle disponibles aujourd’hui représentent une très petite partie de ce spectre. Ils sont, toutefois, des sous-ensembles du plus grand spectre de réalité mixte. Windows 10 est conçu en tenant compte de l’ensemble du spectre et permet de fusionner des représentations numériques de personnes, de lieux et d’objets dans le monde réel.




## <a name="devices-and-experiences"></a>Appareils et expériences


Il existe deux types principaux d’appareils qui proposent des expériences Windows Mixed Reality :
1. **Appareils holographiques.** Celles-ci sont caractérisées par la capacité de l’appareil à placer du contenu numérique dans le monde réel comme s’il existait vraiment.
2. **Périphériques immersifs.** Celles-ci sont caractérisées par la capacité de l’appareil à créer un sens de « présence » : masquer le monde physique et le remplacer par une expérience numérique.

<table>
<tr>
<th width="20%"> Caractéristique</th><th width="40%"> Appareils holographiques</th><th width="40%"> Appareils immersifs</th>
</tr><tr>
<td> Exemple d’appareil</td><td> Microsoft HoloLens<br /> <img alt="Microsoft HoloLens image" width="300" height="169" src="images/mshololens-hero1-whitbg-rgb-300px.png" /></td><td> Windows Mixed Reality Development Edition<br /> <img alt="Acer Windows Mixed Reality Development Edition image" width="300" height="169" src="images/acer-windows-mixed-reality-development-edition-headset-300px.jpg" /></td>
</tr><tr>
<td> Affichage</td><td> <i>Voir affichage.</i> Permet à l’utilisateur de voir l’environnement physique tout en portant le casque.</td><td> <i>Affichage opaque.</i> Bloque l’environnement physique tout en portant le casque.</td>
</tr><tr>
<td> Trésorerie</td><td> Déplacement complet à six degrés de liberté, à la fois pour la rotation et la translation.</td><td> Déplacement complet à six degrés de liberté, à la fois pour la rotation et la translation.</td>
</tr>
</table>

Notez qu’un appareil est connecté à un PC distinct (via un câble USB ou un réseau Wi-Fi) ou qu’il est attaché à un autre ordinateur (à l’aide d’un câble USB ou Wi-Fi) qui ne reflète pas si un appareil est holographique ou immersif. En fait, les fonctionnalités qui améliorent la mobilité conduisent à de meilleures expériences, et les appareils holographiques et immersifs peuvent être attachés ou déattachés.


La progression technologique est celle qui a permis l’expérience de réalité mixte. Aucun appareil n’est actuellement capable d’exécuter des expériences sur tout le spectre. Toutefois, Windows 10 offre une plateforme de réalité mixte commune pour les fabricants de périphériques et les développeurs. Les appareils actuels peuvent prendre en charge une plage spécifique dans le spectre de la réalité mixte. Au fil du temps, de nouveaux appareils vont augmenter cette plage. À l’avenir, les appareils holographiques deviendront plus immersifs et les appareils immersifs seront plus holographiques.

<br>

![types d’appareils dans le spectre de la réalité mixte](images/MixedRealitySpectrum-devices.jpg)<br>
*Où les appareils existent sur le spectre de la réalité mixte*

Souvent, il est préférable de réfléchir au type d’expérience qu’une application ou un développeur de jeux souhaite créer. En général, l’expérience cible un point ou une partie spécifique sur le spectre. Les développeurs doivent ensuite prendre en compte les fonctionnalités des appareils qu’ils souhaitent cibler. Par exemple, les expériences qui reposent sur le monde physique s’exécuteront mieux sur HoloLens.
* **Vers la gauche (quasi-réalité physique).** Les utilisateurs restent présents dans leur environnement physique et ne pensent pas qu’ils ont quitté cet environnement.
* **Au milieu (réalité entièrement mixte).** Ces expériences fusionnent le monde réel et le monde numérique. Les utilisateurs qui ont vu le film [Jumanji](https://en.wikipedia.org/wiki/Jumanji) peuvent concilier la manière dont la structure physique de la maison où l’histoire a eu lieu a été mélangée à un environnement de jungle.
* **Vers la droite (presque Digital Reality).** Les utilisateurs bénéficient d’un environnement entièrement numérique et ignorent ce qui se passe dans l’environnement physique qui les entoure.


## <a name="see-also"></a>Articles associés

* [Qu’est-ce qu’un hologramme ?](hologram.md)
* [Comprendre les principes de base de la réalité mixte](index.md#understand-the-basics)
* [Démarrer la création et le prototypage](design.md)
* [Découvrir les outils et l’architecture](development.md)

