---
title: Étude de cas-leçons de la cuisine de Lowe
description: L’équipe HoloLens souhaite partager certaines des meilleures pratiques qui ont été dérivées du projet HoloLens de Lowe.
author: BrandonBray
ms.author: kevincol
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, Lowe, HoloLens, cuisine, étude de cas
ms.openlocfilehash: 24759f90b8b84ec19e644fb8dff44f64c3ab81d2
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63522345"
---
# <a name="case-study---lessons-from-the-lowes-kitchen"></a>Étude de cas-leçons de la cuisine de Lowe

L’équipe HoloLens souhaite partager certaines des meilleures pratiques qui ont été dérivées du projet HoloLens de Lowe. Vous trouverez ci-dessous une vidéo de l’Lowe HoloLens projeté présentée dans le discours de Satya 2016.
<br>
>[!VIDEO https://www.youtube.com/embed/gC_4JxF0e_k]

## <a name="lowes-hololens-best-practices"></a>Meilleures pratiques de Lowe HoloLens

Les deux vidéos couvrent les meilleures pratiques qui ont été dérivées du pilote HoloLens de Lowe, qui se trouvait dans deux magasins Lowe depuis avril 2016. Les principales rubriques sont les suivantes:
* Optimiser les performances d’un appareil mobile
* Créer des méthodes d’expérience utilisateur avec une image holographique complète (2e contact)
* Alignement de précision (2e contact)
* Expériences holographiques partagées (2e contact)
* Interaction avec les clients (2e Conférence)

## <a name="video-1"></a>Vidéo 1

**Optimiser les performances d’un appareil mobile** HoloLens est un appareil non attaché avec tout le traitement effectué sur l’appareil. Cela nécessite une plate-forme mobile et requiert un mentalités similaire à la création d’applications mobiles. Microsoft recommande que votre application HoloLens maintienne 60FPS pour fournir une expérience délicieuse à vos utilisateurs. Une faible FPS peut entraîner des hologrammes instables.

Voici quelques-uns des éléments les plus importants à examiner lorsque le développement sur HoloLens est l’optimisation/la décimalisation des ressources, à l’aide de nuanceurs personnalisés (disponibles gratuitement dans la [boîte à outils HoloLens](https://github.com/Microsoft/HoloToolkit-Unity)). Une autre considération importante consiste à mesurer la fréquence d’images à partir du début de votre projet. Selon le projet, l’ordre d’affichage de vos ressources peut également être un grand contributeur
<br>
>[!VIDEO https://www.youtube.com/embed/o0QIPwgiP9A]

## <a name="video-2"></a>Vidéo 2

**Créer des méthodes d’expérience utilisateur avec une image holographique complète** Il est important de comprendre le positionnement des hologrammes dans un monde physique. Avec Lowe, nous parlerons des différentes méthodes d’expérience utilisateur qui permettent aux utilisateurs d’expérimenter leurs hologrammes tout en continuant à voir l’environnement plus grand des hologrammes.

**Alignement de précision** Pour le scénario de Lowe, il était primordial d’avoir un alignement précis des hologrammes sur la cuisine physique. Nous nous penchons sur les techniques pour garantir une expérience qui convainc les utilisateurs que leur environnement physique a changé.

**Expériences holographiques partagées** Les couples sont le principal moyen de consommer l’expérience du Lowe. Une personne peut modifier le plan de plan et l’autre personne verra les modifications. Nous avons appelé «expériences partagées».

**Interaction avec les clients** Les concepteurs de Lowe n’utilisent pas un HoloLens, mais ils ont besoin de voir ce que les clients voient. Nous montrons comment capturer ce que le client voit sur une application UWP.
<br>
>[!VIDEO https://www.youtube.com/embed/LceMdyKZ4PI]
