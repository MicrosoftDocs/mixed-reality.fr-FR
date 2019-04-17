---
title: Étude de cas - spatiale sonorisation pour HoloTour
description: Pour créer une visite virtuelle 3D immersive réellement pour Microsoft HoloLens, les vidéos panoramiques et le décor HOLOGRAPHIQUE sont uniquement une partie de la formule.
author: JSyltebo
ms.author: jsylte
ms.date: 03/21/2018
ms.topic: article
keywords: Réalité mixte Windows, HoloLens, HoloTour, spatial étude audio, de casse
ms.openlocfilehash: eca675534dba12dd65a20fb9d85e4df57f725288
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596340"
---
# <a name="case-study---spatial-sound-design-for-holotour"></a>Étude de cas - spatiale sonorisation pour HoloTour

Pour créer une visite virtuelle 3D immersive réellement pour Microsoft HoloLens, les vidéos panoramiques et le décor HOLOGRAPHIQUE sont uniquement une partie de la formule. Concepteur audio que Jason Syltebo évoque comment son a été capturé et traité pour que vous soyez, vous avez réellement dans chacun des emplacements dans HoloTour.

## <a name="the-tech"></a>Les technologies

L’imagerie belle et des scènes HOLOGRAPHIQUE vous voyez dans HoloTour sont uniquement une partie de la création d’une expérience de réalité mixte crédibles. Tandis que hologrammes ne peuvent apparaître que visuellement devant un utilisateur, le [son spatial](spatial-sound.md) fonctionnalité de HoloLens permet audio provenir de toutes les directions, ce qui donne à l’utilisateur une expérience sensorielle plus complète.

Son spatial vous permet de nous envoyer des signaux audio pour indiquer une direction dans laquelle l’utilisateur doit activer, ou pour informer l’utilisateur sont plus hologrammes pour qu’ils puissent les voir dans leur espace. Nous pouvons également attacher un son directement à un hologramme et continuellement mise à jour de la direction et la distance que la hologramme provient d’un utilisateur pour donner l’impression que si le son provient directement de cet objet.

Avec HoloTour, nous souhaitons tirer parti des fonctionnalités spatiales audio de HoloLens pour créer un environnement ambiant à 360 degrés, synchronisé avec la vidéo pour faire apparaître les points importants sonic des emplacements spécifiques.

## <a name="behind-the-scenes"></a>En arrière-plan

Nous avons créé des expériences HoloTour de deux emplacements différents : Rome et Machu Picchu. Nous souhaitons éviter d’utiliser des sons génériques et capturer à la place des données audio directement à partir des emplacements où nous étions en train de filmer afin de rendre ces visites guidées sentir authentique et attrayantes.

### <a name="capturing-the-audio"></a>Capturer l’audio

Dans notre [étude de cas sur la capture du contenu visuel pour HoloTour](case-study-capturing-and-creating-content-for-holotour.md), nous avons parlé de la conception personnalisée de notre plate-forme d’appareil photo. Il est composé de 14 GoPro caméras contenues dans un boîtier imprimée en 3D, conçu pour les dimensions spécifiques de la trépied. Pour capturer des données audio à partir de cette plateforme de test, nous avons ajouté un tableau quad-microphone sous les caméras, une unité de compact 4 canaux d’enregistrement assis à la base de la trépied sont importées. Nous avons choisi les microphones qui non seulement effectuée correctement, mais qui avait un très faible encombrement, afin de n'occlude pas la vue de l’appareil photo.

![Plateforme de test personnalisé caméra et le microphone](images/camera-rig-microphones-300px.png)<br>
*Plateforme de test personnalisé caméra et le microphone*

Ce programme d’installation capturée son dans quatre directions à partir de l’emplacement précis de notre appareil photo, qui nous donne suffisamment d’informations pour recréer un panorama AUDITIF 3D à l’aide de son spatial, ce qui nous aurions pu synchroniser ultérieurement à la vidéo à 360 degrés.

Un des défis de l’audio de tableau de caméra est que vous êtes à la merci de ce qui est enregistré au moment de la capture. Même si la capture vidéo est correcte, la capture audio peut devenir problématique, car les sons de désactiver la caméra comme sirène, constructeur aéronautique ou vents haute. Afin de garantir que nous avions tous les éléments que nous avons besoin, nous avons utilisé une série d’unités de l’enregistrement des mobiles stéréo et mono pour obtenir des éléments asynchrones, ambiantes à des moments particuliers d’intérêt dans chaque emplacement. Cette capture est importante car elle permet le Concepteur de son contenu propre et réutilisable qui peut être utilisé de post-production pour élaborer des intérêts et augmenter la direction de recherche.

N’importe quel jour de capture donnée générerait un grand nombre de fichiers. Il était important développer un système pour suivre les fichiers qui correspondent à un emplacement particulier ou une caméra capture de. Notre unité d’enregistrement a été autorisé à des fichiers d’un nom automatique par date et take nombre et nous serait sauvegarder à la fin de la journée aux lecteurs externes. Au minimum, verbalement slating le début des enregistrements audio était important car cela permet de faciliter l’identification du contenu contextuelle doivent les noms de fichiers deviennent un problème. C’était également important pour nous d’ardoise visuellement la capture de plateforme d’appareil photo comme audio et vidéo ont été enregistrés en tant que média distinct et nécessaires pour être synchronisés pendant l’opération post.

### <a name="editing-the-audio"></a>Modification de l’audio

Au studio après le voyage de capture, la première étape de l’assemblage d’une expérience AUDITIF directionnelle et immersive consiste à examiner tous les de la capture audio pour un emplacement, la meilleure permet de repérer et identifier les points importants qui peut être appliquées de manière créative pendant intégration. L’audio est ensuite modifié et nettoyée. Par exemple, un horn voiture bruyant une durée d’une seconde ou presque et répéter plusieurs fois, peut être remplacé et assembler avec les sections de quiet, ambiante audio à partir de la même capture.

Une fois que le montage vidéo pour un emplacement a été établie, que le concepteur audio peut synchroniser l’audio correspondant. À ce stade, nous avons collaboré avec la capture de plateforme d’appareil photo et de capture mobile pour décider quels éléments ou une combinaison de celles-ci, fonctionnera pour créer une scène audio immersive. Une technique que nous avons trouvé utiles consistait à ajouter tous les éléments audio dans un audio éditeur et la génération rapide linéaire fictifs onduleur à faire des essais avec des idées de combinaison différente. Cela nous a donné mieux les idées formées lorsqu’il était temps de générer les coulisses HoloTour réels.

### <a name="assembling-the-scene"></a>Assemblage de la scène

La première étape pour générer une scène 3D ambiante consiste à créer un lit des informations générales ambiante bouclage sons qui prendra en charge autres fonctionnalités et les éléments audio interactifs dans une scène. Ce faisant, nous avons choisi une approche holistique de techniques d’implémentation différentes selon les besoins spécifiques et les critères de conception de toutes les scènes particulier. Certaines séquences peuvent indexer dans l’utilisation de la capture de la caméra synchronisés, tandis que d’autres peuvent nécessiter une approche plus organisée utilise plus discrètement placé les sons, les éléments interactifs musique et des effets sonores pour les moments plus cinématiques dans HoloTour.

Lors de l’indexation sur l’utilisation de l’audio de capture photo, nous avons placé spatiales son activé ambiantes audio émetteurs correspondant aux coordonnées directionnelles de l’orientation de l’appareil photo, tels que la vue de la caméra du Nord joue audio du microphone du Nord et de la même manière pour les autres instructions cardinales. Ces émetteurs sont verrouillés de monde, ce qui signifie que l’utilisateur peut activer librement leur tête par rapport à ces émetteurs et le son changera en conséquence, modélisation efficacement le son de capacité à cet emplacement. Pour obtenir des exemples de scènes utilisent une bonne combinaison d’audio de l’appareil photo capturée, écoutez déployé Navona ou le Pantheon.

Une approche différente impliqués jouant un bouclage ambiance stéréo conjointement avec des émetteurs de sons spatiales placés autour de la scène de lecture de sons uniques qui sont aléatoires en termes de fréquence de volume, de tangage et de déclencheur. Cette opération crée une ambiance avec renforce le sentiment de direction. Dans Aguas Calientes, par exemple, vous pouvez écouter comment chaque quadrant du panorama a émetteurs spécifiques qui intentionnellement mettent en évidence des zones spécifiques de la géographie, mais fonctionnent ensemble pour créer une ambiance globale immersive.

## <a name="tips-and-tricks"></a>Conseils et astuces

Lorsque vous la placez ensemble audio pour une scène, il existe des méthodes supplémentaires vous permettent plus mettre en surbrillance une direction et immersion, tirant pleinement parti des fonctionnalités spatiales audio de HoloLens. Nous vous avons fourni une liste de certaines ci-dessous, écouter attentivement la prochaine fois que vous essayez de HoloTour.
* **Rechercher les cibles**: Il s’agit des sons qui déclenchent uniquement lorsque vous examinez un objet spécifique ou d’une zone du frame HOLOGRAPHIQUE. Par exemple, vous recherchez dans la direction de la rue côté café dans déployé Navona de Rome légèrement déclenche les sons d’un restaurant occupé.
* **Vision locale**: Le parcours que HoloTour contient certaines beats où votre visite guidée guide, facilité par hologrammes, explorerai une rubrique détaillée. Par exemple, comme la façade de le Pantheon fondus pour révéler l’oculus, audio bel placé comme un émetteur 3D à partir de l’intérieur de la Pantheon encourage l’utilisateur pour Explorer le modèle intérieur.
* **Amélioré une direction**: Au sein de nombreuses d’arrière-plan, nous avons placé les sons de différentes manières pour ajouter à la direction. Dans la scène Pantheon, par exemple, le son de la Fontaine a été placé comme un émetteur distinct suffisamment proches pour l’utilisateur afin qu’ils pourraient avoir une idée de « parallaxe sonic » comme ils parcourue autour de l’espace de lecture. Dans la scène de Salinas de Maras du Pérou, la perspective individuelle de certains flux peu a été placée en tant que distincts émetteurs pour créer un environnement ambiant plus riche, autour de l’utilisateur avec les sons authentiques de cet emplacement.
* **Émetteur de spline**: Cet émetteur son spatial spéciaux se déplace dans l’espace 3D par rapport à la position visuelle de l’objet, à qu'il est attaché. Un exemple de ceci a été le train dans Machu Picchu, où nous avons utilisé un émetteur de spline pour donner une idée distincte de direction et le déplacement.
* **Musique et dans SFX**: Certains aspects de HoloTour qui représentent une approche plus stylisée ou cinématique utilisent musique et des effets sonores en vue d’accroître l’impact émotionnel. Dans la bataille gladiator à la fin de la visite guidée de Rome, des effets spéciaux tels que whooshes ou stingers ont été utilisées pour vous aider à renforcer l’effet des étiquettes qui apparaissent dans les scènes.

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Jason Syltebo" width="60" height="60" src="images/syltebo.png"></td>
<td style="border-style: none"><b>Jason Syltebo</b><br>Concepteur audio @Microsoft</td>
</tr>
</table>

## <a name="see-also"></a>Voir aussi
* [Son spatial](spatial-sound.md)
* [Sonorisation spatiale](spatial-sound-design.md)
* [Son spatial dans Unity](spatial-sound-in-unity.md)
* [MR 220 Spatial](holograms-220.md)
* [Vidéo : Microsoft HoloLens : HoloTour](https://www.youtube.com/watch?v=pLd9WPlaMpY)

 
