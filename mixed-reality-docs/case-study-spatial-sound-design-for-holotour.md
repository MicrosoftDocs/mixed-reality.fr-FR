---
title: Étude de cas-conception de son spatial pour HoloTour
description: Pour créer une visite virtuelle 3D véritablement immersif pour Microsoft HoloLens, les vidéos panoramiques et les scènes holographiques ne font qu’une partie de la formule.
author: JSyltebo
ms.author: jsylte
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, HoloLens, HoloTour, son spatial, étude de cas
ms.openlocfilehash: f2dd704089d9c76b7ba175a4a1ad5cebf9ec6c68
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75181924"
---
# <a name="case-study-spatial-sound-design-for-holotour"></a>Étude de cas : conception de son spatial pour HoloTour

Les vidéos panoramiques et les paysages holographiques ne font qu’une partie de la formule pour une visite virtuelle Microsoft HoloLens véritablement immersif. Cet article décrit comment le son a été utilisé pour vous faire croire que vous êtes en fait à chaque emplacement HoloTour.

## <a name="the-tech"></a>Le Tech

La belle image et les scènes holographiques que vous voyez dans HoloTour ne sont qu’une partie d’une expérience de réalité mixte incroyable. Bien que les hologrammes ne puissent apparaître visuellement qu’à l’avant d’un utilisateur, le [son spatial](spatial-sound.md) fourni par HoloLens dans toutes les directions fournit une expérience sensorielle plus complète.

Le son spatial fournit des signaux pour indiquer une direction que l’utilisateur doit activer ou pour informer l’utilisateur qu’il y a plus d’hologrammes à afficher dans son espace. Nous pouvons également joindre un son directement à un hologramme et mettre à jour continuellement la direction et la distance de l’hologramme de l’utilisateur. Cette technique semble si le son provient directement de cet objet.

Pour HoloTour, nous souhaitons tirer parti des capacités spatiales de HoloLens pour créer un environnement ambiant à 360 degrés qui est synchronisé avec la vidéo afin de révéler les points forts de certains emplacements.

## <a name="behind-the-scenes"></a>En arrière-plan

Nous avons créé des expériences HoloTour de deux emplacements différents : Rome et Machu Picchu. Pour faire en sorte que ces présentations soient authentiques et attrayantes, nous souhaitons capturer le son à partir des emplacements où nous avons fait des films au lieu d’utiliser des sons génériques.

### <a name="capture-the-audio"></a>Capturer l’audio

Dans notre [étude de cas sur la capture du contenu visuel pour HoloTour](case-study-capturing-and-creating-content-for-holotour.md), nous parlerons de la conception de notre plate-forme de caméra. Il a été constitué de 14 caméras GoPro dans un logement en 3D qui a été conçu pour s’adapter au trépied. Pour capturer de l’audio, nous avons ajouté un tableau à quatre microphones sous les caméras. Le son a été alimenté dans une unité d’enregistrement à quatre canaux compacte à la base du trépied. Nous avons choisi des microphones qui s’exécutaient bien, mais suffisamment petits pour éviter toute interférence avec les caméras.

![une caméra personnalisée et un microphone](images/camera-rig-microphones-300px.png)<br>
*Caméra personnalisée et plate-forme de microphone*

Ce programme d’installation capture le son dans quatre directions. Nous avons enregistré suffisamment d’informations pour recréer un panoramique acoustique 3D de son spatial, que nous pourrions synchroniser ultérieurement avec la vidéo de 360 degrés.

L’un des défis de l’audio de la baie de caméra est que vous êtes à la merci des sons de l’appareil photo, tels que les Sirens, les avions ou les vents élevés. Pour vous assurer que nous avions tous les éléments sonores nécessaires, nous avons également utilisé des enregistreurs mobiles stéréo et mono pour capturer des sons ambiants asynchrones à des points d’intérêt spécifiques à chaque emplacement. Ces enregistrements fournissent le contenu propre au concepteur de sons pour ajouter de l’intérêt et améliorer la direction dans la suite de la production.

Chaque jour de capture génère de nombreux fichiers. Il était donc important de développer un système pour effectuer le suivi des fichiers qui correspondent à un emplacement ou à une capture d’appareil photo spécifique. Notre unité d’enregistrement a été configurée pour nommer automatiquement les fichiers par date et « Take ». Nous avons sauvegardé des fichiers sur des lecteurs externes à la fin de chaque jour. Nous avons également découvert qu’il était important d’ajouter oralement le début des enregistrements audio. Cette précaution permet d’identifier facilement le contenu en cas de problème de nom de fichier. Il était également important de visualiser visuellement la capture de la caméra, car la vidéo et l’audio ont été enregistrés comme des supports distincts et devaient être synchronisés au cours de la publication.

### <a name="edit-the-audio"></a>Modifier l’audio

En retour au Studio après le trajet, la première étape de l’assemblage d’une expérience de l’entrée auditive directionnelle et immersive consiste à passer en revue tous les éléments audio capturés pour un emplacement. Nous choisissons la meilleure prise et identifiez les mises en évidence qui peuvent être appliquées au cours de l’intégration. L’audio est ensuite modifié et nettoyé. Par exemple, un signal d’explosion de voiture qui dure une seconde ou, et se répète plusieurs fois, peut être remplacé par un son ambiant plus calme de la même session de capture.

Une fois que la modification vidéo d’un emplacement est définie, le concepteur de sons peut synchroniser l’audio correspondant. À ce stade, nous évaluons à la fois les captures de la caméra et des sons mobiles pour décider quels éléments fonctionnent pour créer une scène audio immersive. Nous avons découvert qu’il était utile de placer tous les éléments sonores dans un éditeur audio et de créer des maquettes linéaires rapides pour expérimenter différentes idées de combinaison. Cette étape nous a permis d’obtenir des idées améliorées pour le moment où il était temps de créer les scènes HoloTour réelles.

### <a name="assemble-the-scene"></a>Assembler la scène

La première étape de la création d’une scène ambiante 3D consiste à créer un lit de sons généraux de bouclage ambiant qui prendront en charge d’autres fonctions et éléments de son interactifs dans une scène. Nous prenons une approche holistique de l’implémentation, telle que déterminée par les critères de conception d’une scène particulière. Certaines scènes peuvent être indexées vers à l’aide de la capture d’appareil photo synchronisée. Davantage de moments « cinématiques » peuvent nécessiter une approche organisée qui repose sur des sons, des éléments interactifs et de la musique disposés discrètement.

Lorsque nous avons indexé l’audio de capture d’appareil photo, nous avons placé des émetteurs audio spatiaux compatibles avec le son spatial qui correspondaient à l’orientation directionnelle des caméras. La vue de la caméra Nord lit les données audio du microphone Nord, et de la même façon pour les autres directions cardinales. Ces émetteurs sont verrouillés dans le monde, ce qui signifie que lorsque l’utilisateur change sa tête par rapport à ces émetteurs, le son change. Cette technique modélise efficacement le son de la position debout à cet emplacement. Écoutez Piazza Navona ou Pantheon pour obtenir des exemples de scènes qui utilisent un bon mélange de données audio capturées par une caméra.

Dans une approche différente, nous affichons parfois l’ambiance stéréo en boucle conjointement avec les émetteurs de sons spatiaux placés autour de la scène. Ces émetteurs émettent des sons uniques d’une fréquence de déclenchement et de volume aléatoires. Cette technique crée une ambiance qui a un sens amélioré de la direction. Dans Aguas alienates, par exemple, vous pouvez savoir comment chaque quadrant du panorama a des émetteurs spécifiques qui mettent en évidence des zones spécifiques de la géographie, mais qui travaillent ensemble pour créer une ambiance immersive globale.

## <a name="tips-and-tricks"></a>Conseils et astuces

Il existe d’autres façons de mettre en évidence la direction et d’améliorer l’immersion pour tirer pleinement parti des fonctionnalités de son spatial de HoloLens. Nous avons fourni une liste ici. Écoutez ces effets la prochaine fois que vous essaierez HoloTour.
* **Rechercher les cibles :** Ces sons sont déclenchés lorsque vous examinez un objet ou une zone spécifique du cadre holographique. Par exemple, regardez sur le café de Rome dans Piazza Navona pour déclencher discrètement des sons occupés-restaurants.
* **Vision locale :** Bien que HoloTour contienne certains « temps » dans lesquels votre guide de visite guidée, assisté par des hologrammes, explore un sujet en profondeur. Par exemple, à mesure que la façade du Pantheon se résout pour révéler le Oculus, le son reverberating qui a été placé en tant qu’émetteur en 3D à partir de l’Pantheon encourage l’utilisateur à explorer l’intérieur.
* **Orientation améliorée :** Dans de nombreuses scènes, nous avons placé des sons de différentes façons pour les ajouter à la direction. Dans la scène Pantheon, par exemple, le son de la Fontaine a été placé comme un émetteur distinct suffisamment proche de l’utilisateur pour qu’il puisse obtenir un sens « Sonic parallaxe » lorsqu’ils parcourent l’espace de lecture. Dans la scène Salinas de Maras du Pérou, les sons des petits flux individuels ont été placés en tant qu’émetteurs distincts pour créer un environnement ambiant plus immersif, mettant l’utilisateur avec les sons authentiques de cet emplacement.
* **Émetteur de spline :** Ces émetteurs se déplacent dans l’espace 3D par rapport à la position visuelle de l’objet auquel ils sont attachés. Un exemple est le train dans Machu Picchu, où nous avons utilisé un émetteur de spline pour donner un sens distinct de la direction et du mouvement.
* **Musique et SFX :** Certains aspects des HoloTour qui représentent une approche plus stylisée ou cinématographique utilisent des effets sonores et musicaux pour renforcer l’impact émotionnelle. Dans la bataille Gladiator à la fin de la visite de Rome, par exemple, des effets spéciaux comme les whooshes et les batteurs aident à renforcer l’effet des étiquettes qui s’affichent en arrière-plan.

## <a name="see-also"></a>Articles associés
* [Son spatial](spatial-sound.md)
* [Conception du son spatial](spatial-sound-design.md)
* [Son spatial dans Unity](spatial-sound-in-unity.md)
* [Vidéo : Microsoft HoloLens : HoloTour](https://www.youtube.com/watch?v=pLd9WPlaMpY)
