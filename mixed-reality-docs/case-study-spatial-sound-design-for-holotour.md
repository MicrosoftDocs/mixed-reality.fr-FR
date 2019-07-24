---
title: Étude de cas-conception de son spatial pour HoloTour
description: Pour créer une visite virtuelle 3D véritablement immersif pour Microsoft HoloLens, les vidéos panoramiques et les scènes holographiques ne font qu’une partie de la formule.
author: JSyltebo
ms.author: jsylte
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, HoloLens, HoloTour, son spatial, étude de cas
ms.openlocfilehash: eca675534dba12dd65a20fb9d85e4df57f725288
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63522446"
---
# <a name="case-study---spatial-sound-design-for-holotour"></a>Étude de cas-conception de son spatial pour HoloTour

Pour créer une visite virtuelle 3D véritablement immersif pour Microsoft HoloLens, les vidéos panoramiques et les scènes holographiques ne font qu’une partie de la formule. Le concepteur audio Jason Syltebo discute de la façon dont le son a été capturé et traité pour vous faire croire que vous êtes en fait dans chacun des emplacements de HoloTour.

## <a name="the-tech"></a>Le Tech

La belle image et les scènes holographiques que vous voyez dans HoloTour ne sont qu’une partie de la création d’une expérience de réalité mixte incroyable. Alors que les hologrammes ne peuvent apparaître que visuellement devant un utilisateur, la fonctionnalité de [son spatial](spatial-sound.md) de HoloLens permet à l’utilisateur de sortir de toutes les directions, ce qui donne à l’utilisateur une expérience sensorielle plus complète.

Le son spatial nous permet de fournir des signaux audio pour indiquer une direction dans laquelle l’utilisateur doit s’allumer, ou pour informer l’utilisateur qu’il y a plus d’hologrammes à afficher dans son espace. Nous pouvons également joindre un son directement à un hologramme et mettre à jour continuellement la direction et la distance de l’hologramme à partir d’un utilisateur pour le faire paraître si le son provient directement de cet objet.

Avec HoloTour, nous voulions tirer parti des capacités spatiales de HoloLens pour créer un environnement ambiant à 360 degrés, synchronisé avec la vidéo afin de révéler les points importants de certains emplacements.

## <a name="behind-the-scenes"></a>En arrière-plan

Nous avons créé des expériences HoloTour de deux emplacements différents: Rome et Machu Picchu. Pour faire en sorte que ces présentations soient authentiques et attrayantes, nous souhaitons éviter d’utiliser des sons génériques et capturer des données audio directement à partir des emplacements où nous avions le film.

### <a name="capturing-the-audio"></a>Capture de l’audio

Dans notre [étude de cas sur la capture du contenu visuel pour HoloTour](case-study-capturing-and-creating-content-for-holotour.md), nous avons parlé de la conception personnalisée de notre plate-forme de caméra. Elle comprenait 14 caméras GoPro contenues dans un boîtier en 3D, conçue pour les dimensions spécifiques du trépied. Pour capturer de l’audio à partir de cette plate-forme, nous avons ajouté une baie à quatre microphones sous les caméras, qui alimentait une unité d’enregistrement à 4 canaux compacte qui se trouvait à la base du trépied. Nous avons choisi des microphones qui ne se sont pas exécutés correctement, mais qui ont un encombrement très faible, afin de ne pas occultait la vue de l’appareil photo.

![Caméra personnalisée et plate-forme de microphone](images/camera-rig-microphones-300px.png)<br>
*Caméra personnalisée et plate-forme de microphone*

Ce programme d’installation a capturé un son dans quatre directions à partir de l’emplacement précis de notre appareil photo, ce qui nous permet de recréer un panorama en 3D acoustique à l’aide d’un son spatial, que nous pourrions synchroniser ultérieurement avec la vidéo de 360 degrés.

L’un des défis liés à l’audio de la baie de caméra est que vous êtes à la merci de ce qui est enregistré au moment de la capture. Même si la capture vidéo est correcte, la capture de sons peut devenir problématique en raison de sons d’appareil photo tels que Sirens, les avions ou les vents élevés. Pour nous assurer que nous avions tous les éléments dont nous avons besoin, nous avons utilisé une série d’unités d’enregistrement mono et stéréo pour obtenir des éléments ambiants asynchrones à des points d’intérêt spécifiques à chaque emplacement. Cette capture est importante, car elle offre au concepteur de sons la possibilité de rechercher du contenu propre et utilisable qui peut être utilisé dans le cadre de la publication en production pour créer un intérêt et ajouter de la direction.

Tout jour de capture donné génère un grand nombre de fichiers. Il était important de développer un système pour assurer le suivi des fichiers qui correspondent à un emplacement particulier ou à une capture d’appareil photo. Notre unité d’enregistrement a été configurée de manière à ce qu’elle renomme automatiquement les fichiers par date et prenne le nombre et nous y revenons à la fin de la journée sur les lecteurs externes. Au moins, il est important de faire une SLAT verbale du début des enregistrements audio, car cela permet d’identifier facilement le contenu et de faire en sorte que les noms de fichiers deviennent un problème. Nous avons également important pour nous de vous présenter visuellement la capture de la plateforme de la caméra, car la vidéo et l’audio ont été enregistrés comme des médias distincts et devaient être synchronisés pendant la publication.

### <a name="editing-the-audio"></a>Modification de l’audio

En retour au Studio après le trajet, la première étape de l’assemblage d’une expérience de l’État oral et immersif consiste à passer en revue l’ensemble de la capture audio pour un emplacement, à choisir les meilleures prises et à identifier les surbrillances qui pourraient être appliquées de façon créative pendant intégration. L’audio est ensuite modifié et nettoyé. Par exemple, un avertisseur bruyant qui dure une seconde ou donc, et se répète plusieurs fois, peut être remplacée par des sections de l’audio ambiant en mode silencieux de la même capture.

Une fois que la modification vidéo d’un emplacement a été établie, le concepteur de sons peut synchroniser l’audio correspondant. À ce stade, nous avons travaillé avec la capture d’appareil photo et la capture mobile pour décider quels éléments, ou la combinaison de ces éléments, travailleront pour créer une scène audio immersive. Nous avons trouvé une technique utile pour ajouter tous les éléments de son dans un éditeur audio et créer des maquettes linéaires rapides pour expérimenter différentes idées de combinaison. Cela nous a permis de mieux former des idées lorsqu’il était temps de créer les scènes HoloTour réelles.

### <a name="assembling-the-scene"></a>Assemblage de la scène

La première étape de la création d’une scène ambiante 3D consiste à créer un lit de sons généraux de bouclage ambiant qui prendront en charge d’autres fonctions et éléments de son interactifs dans une scène. Dans ce cas, nous avons adopté une approche holistique pour les différentes techniques d’implémentation déterminées par les besoins spécifiques et les critères de conception d’une scène particulière. Certaines scènes peuvent être indexées à l’aide de la capture de la caméra synchronisée, tandis que d’autres peuvent nécessiter une approche plus organisée qui utilise des sons, des éléments interactifs et des effets sonores et de musique plus cinématographiques pour des moments plus cinématiques dans HoloTour.

Lors de l’indexation sur l’utilisation de l’audio de capture de l’appareil photo, nous avons placé des signaux audio ambiants compatibles avec le son spatial correspondant aux coordonnées directionnelles de l’orientation de l’appareil photo, de telle sorte que la vue de la caméra Nord lise l’audio du microphone Nord et de la même manière pour les autres directions cardinales. Ces émetteurs sont verrouillés dans le monde entier, ce qui signifie que l’utilisateur peut librement changer sa tête par rapport à ces émetteurs et que le son change en conséquence, en modélisant efficacement le son de la position debout à cet emplacement. Écoutez Piazza Navona ou Pantheon pour obtenir des exemples de scènes qui utilisent une bonne combinaison de l’audio capturé par l’appareil photo.

Une approche différente impliquait la lecture d’une ambiance stéréo en boucle avec les émetteurs de sons spatiaux placés autour de la scène en lisant des sons uniques qui sont aléatoires en termes de fréquence de volume, de tangage et de déclenchement. Cela crée une ambiance avec un sens amélioré de la direction. Dans Aguas Calientes, par exemple, vous pouvez écouter comment chaque quadrant du panorama a des émetteurs spécifiques qui mettent intentionnellement en évidence des zones spécifiques de la géographie, mais fonctionnent ensemble pour créer une ambiance immersive globale.

## <a name="tips-and-tricks"></a>Trucs et astuces

Lorsque vous regroupez des données audio pour une scène, vous pouvez utiliser d’autres méthodes pour mettre en évidence la direction et l’immersion, en utilisant pleinement les capacités spatiales du son de HoloLens. Nous avons fourni une liste d’éléments ci-dessous, à écouter la prochaine fois que vous essayez HoloTour.
* **Rechercher les cibles**: Il s’agit de sons qui se déclenchent uniquement lorsque vous examinez un objet ou une zone spécifique du cadre holographique. Par exemple, si vous recherchez dans la direction du café situé à la rue dans Piazza Navona de Rome, vous déclenchez légèrement les sons d’un restaurant occupé.
* **Vision locale**: Bien que HoloTour contient certains temps où votre guide de visite guidée, assisté par des hologrammes, explorera un sujet en détail. Par exemple, à mesure que la façade du Pantheon se résout pour révéler le Oculus, le son reverberating placé en tant qu’émetteur 3D à partir de l’intérieur de la Pantheon encourage l’utilisateur à explorer le modèle intérieur.
* **Orientation améliorée**: Dans de nombreuses scènes, nous avons placé des sons de différentes façons pour les ajouter à la direction. Dans la scène Pantheon, par exemple, le son de la Fontaine a été placé comme un émetteur distinct suffisamment proche de l’utilisateur afin qu’il puisse obtenir un sens de «Sonic parallaxe» lorsqu’il parcourt l’espace de lecture. Dans la scène Salinas de Maras, le point de vue individuel de certains des petits flux a été placé en tant qu’émetteurs distincts pour créer un environnement ambiant plus immersif, mettant l’utilisateur en place avec les sons authentiques de cet emplacement.
* **Émetteur de spline**: Cet émetteur de son spatial spécial déplace dans l’espace 3D par rapport à la position visuelle de l’objet auquel il est attaché. Par exemple, l’apprentissage dans Machu Picchu, où nous avons utilisé un émetteur de spline pour donner un sens distinct de la direction et du mouvement.
* **Musique et SFX**: Certains aspects des HoloTour qui représentent une approche plus stylisée ou cinématographique utilisent la musique et les effets sonores pour renforcer l’impact émotionnelle. Dans la bataille Gladiator à la fin de la visite de Rome, des effets spéciaux tels que whooshes ou des s ont été utilisés pour aider à renforcer l’effet des étiquettes apparaissant en scène.

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Jason Syltebo" width="60" height="60" src="images/syltebo.png"></td>
<td style="border-style: none"><b>Jason Syltebo</b><br>Concepteur audio@Microsoft</td>
</tr>
</table>

## <a name="see-also"></a>Voir aussi
* [Son spatial](spatial-sound.md)
* [Conception du son spatial](spatial-sound-design.md)
* [Son spatial dans Unity](spatial-sound-in-unity.md)
* [MR spatial 220](holograms-220.md)
* [Vidéo : Microsoft HoloLens : HoloTour](https://www.youtube.com/watch?v=pLd9WPlaMpY)

 
