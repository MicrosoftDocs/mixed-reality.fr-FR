---
title: Étude de cas, qui représente des êtres humains en réalité mixte
description: Quels types d’opportunités émergent quand nous ne pouvons pas créer des éléments fantastiques, mais utiliser les captures les plus réalistes des environnements, des objets et des personnes en réalité mixte ?
author: mavitazk
ms.author: jemccull
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, humains, avatar, capture de réalité mixte, vidéo volumétrique
ms.openlocfilehash: 9826a55428c093f887531b20083c4bdc3d2bcb53
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73436538"
---
# <a name="case-study---representing-humans-in-mixed-reality"></a>Étude de cas, qui représente des êtres humains en réalité mixte

James Turrell conçoit avec la lumière. L’exécution pas à pas de son travail rend floue un sens de la profondeur et du focus. Les murs semblent à la fois proches et infinis, la luminosité donne des ombres. Perceptions non familières conçues par l’équilibrage minutieux de la couleur et de la diffusion de la lumière. [Turrell décrit ces](https://www.sculpture.org/documents/scmag02/nov02/turrell/turrell.shtml) sens comme *« sentiment avec vos yeux »* , un moyen d’étendre une compréhension de la réalité. Des mondes fantastiques, comme ceux Turrell imagine, sont des outils puissants pour exploiter nos sens, et non pas à la différence des environnements immersifs de la réalité mixte aujourd’hui.

![Grand sorti-James Turrell (1998)](images/wide-out-james-turrell.jpg)

## <a name="how-do-you-represent-complex-real-world-environments-in-mixed-reality"></a>Comment faire pour représenter des environnements réels complexes en réalité mixte ?

Le fait de représenter le travail de Turrell dans une expérience immersive est un défi attrayant. L’éclairage, la mise à l’échelle et l’audio spatial présentent des opportunités pour représenter son travail. Bien que l’environnement géométrique de l’exposition nécessiterait une modélisation 3D relativement simple, il est secondaire du point de vue de l’artiste : l’impact de la lumière sur les sens.

Le « Turrell », le « minimum Surreal », est la caractéristique de son travail, mais que se passe-t-il si nous voulions représenter une exposition avec des matériaux plus complexes en réalité mixte ?

![Bang-ai Weiwei (2013)](images/bang-ai-weiwie.jpg)

Dans 2013, The Artist ai Weiwei [a dévoilé un travail tangling d’art](https://www.designboom.com/art/ai-weiwei-bang-installation-at-venice-art-biennale-2013/) comprenant 886 antiquités sur Venice Biennale. Chaque tabouret en bois provenait d’une époque où les artisans chinoises étaient très appréciés, où ces tabourets auraient été transmis entre les générations. Les tabouret eux-mêmes (les subtilités du bois, la précision des pièces, leur positionnement prudent) sont essentiels aux commentaires de l’IA sur la culture moderne.

Les tabourets antiquités diffusent le message de l’artiste par le biais de leur authenticité. Leur représentation réaliste est essentielle à l’expérience, la création d’un défi technique : la sculpture de chacun des 886 tabourets à la main serait extrêmement exhaustive et coûteuse. Combien de temps faut-il pour modeler et positionner ? Comment assureriez-vous l’authenticité du matériel ? La recréation de ces objets à partir de zéro devient, à bien des égards, une interprétation de l’illustration elle-même. Comment pouvez-vous conserver l’intention de l’artiste ?

## <a name="methods-of-capturing-mixed-reality-assets"></a>Méthodes de capture de ressources de réalité mixte

Une alternative à la création d’un élément à partir de zéro consiste à capturer le véritable élément. Grâce à un ensemble de méthodes de capture toujours plus avancés, nous pouvons développer des représentations authentiques de chacun des types de ressources de base trouvés dans la réalité mixte (environnements, objets et personnes).

Les grandes catégories vont de la vidéo 2D bien établie aux formes les plus récentes de la vidéo volumétrique. Dans le cas de l’exposition d’AI Weiwei, l’analyse (souvent désignée par sa technique fondamentale, photogrammetry) peut être employée lors de la création de l’exposition, en balayant chacun des tabourets eux-mêmes. 360 ° la capture de photos et de vidéos est une autre méthode permettant de virtualiser l’expérience à l’aide d’une caméra omnidirectionnel de haute qualité positionnée dans l’enclos. Avec ces techniques, l’une d’entre elles commence à comprendre le sens de l’échelle, idéalement avec suffisamment de détails pour voir les artisans de chaque élément. Tout cela est possible dans un format numérique, ce qui permet d’obtenir de nouveaux Vista et de nouvelles perspectives en réalité.

![Vidéo 2D à volumétrique](images/2d-to-volumetric-video.png)

Quels types d’opportunités émergent quand nous ne pouvons pas créer des éléments fantastiques, mais utiliser les captures les plus réalistes des environnements, des objets et des personnes en réalité mixte ? L’exploration du chevauchement entre ces méthodes permet d’éclairer l’emplacement du support.

Pour les environnements et les objets, le logiciel 360 ° Imaging évolue pour inclure des éléments de Photogrammetry. Isoler les informations de profondeur des scènes, des vidéos 360 ° avancées vous aide à réduire le sentiment de blocage de votre tête dans un Fishbowl lors de la recherche d’une scène virtuelle.

Pour les personnes, de nouvelles méthodes sont émergentes, qui combinent et étendent la capture et l’analyse de mouvement : la capture de mouvement a été fondamentale pour obtenir des mouvements humains détaillés vers des effets visuels et des caractères cinématiques, tandis que l’analyse a avancé pour capturer les informations humaines des visuels tels que des visages et des mains. Avec les avancées en matière de technologie de rendu, une nouvelle méthode appelée vidéo volumétrique crée ces techniques, combinant des informations visuelles et détaillées, afin de créer la nouvelle génération de captures humaines en 3D.

## <a name="volumetric-video-and-the-pursuit-of-authentic-human-capture"></a>Vidéo volumétrique et poursuite de la capture humaine authentique

Les êtres humains sont essentiels à la narration, dans le sens le plus littéral : un parlant humain, en cours d’exécution ou en tant qu’objet de l’histoire. Certains des moments les plus immersifs et les plus oculaires des premières expériences immersifs d’aujourd’hui sont sociaux. De partager une expérience de réalité mixte dans votre salon, pour voir vos amis dans de nouveaux environnements incroyables. L’élément humain fait même la réalité la plus fantastique, une réalité.

![Mindshow en VR](images/mindshow-in-vr-640px.jpg)

Les avatars dans des expériences immersifs permettent un nouveau type de incarnation dans le récits. Les applications les plus récentes repensent le concept de propriété de corps virtuel et de configuration d’un bond générationnel dans l’élimination de la distance entre les personnes. Des entreprises telles que [Mindshow](https://mindshow.com/) développent des outils créatifs qui tirent parti des avatars, ce qui permet aux utilisateurs de prendre des personnages et des personnages entièrement nouveaux. D’autres explorent les [méthodes d’expression artistique](https://en.wikipedia.org/wiki/Uncanny_valley), une opportunité créative potentiellement illimitée pour explorer la nature (et la nécessité) des attributs de type humain. Aujourd’hui, cette absence de réalisme permet d’éviter la [vallée des ignorent humains](https://en.wikipedia.org/wiki/Uncanny_valley) , ainsi qu’un hôte de problèmes techniques pour les développeurs quotidiens. Pour ces raisons (et bien plus encore), il est très probable que les avatars non réalistes deviendront la valeur par défaut pour un avenir prévisible. Pourtant, bien que le réalisme pose un énorme défi pour la réalité mixte, *il existe des scénarios clés qui requièrent une représentation authentique des êtres humains dans l’espace 3D*.

Chez Microsoft, une petite équipe à la recherche de Microsoft Research a passé les dernières années à développer une méthode pour capturer les êtres humains via une forme de vidéo volumétrique. Aujourd’hui, le processus est similaire à la production vidéo : au lieu d’appliquer un mouvement à une ressource sculptée, il s’agit d’un enregistrement 3D complet. Les performances et l’image sont capturées en temps réel. il ne s’agit pas du travail d’un artiste, il s’agit d’une représentation authentique. Et bien que la technologie commence simplement à se développer dans des applications commerciales, les implications de la vidéo volumétrique sont essentielles à la [vision de Microsoft en matière d’informatique personnelle](https://www.youtube.com/watch?v=tcyj-_IEWt8).

![Vidéo volumétrique SIGGRAPH 2015](images/volumetric-video-siggraph-2015.gif)

La capture humaine authentique déverrouille les nouvelles catégories uniques d’expériences dans la réalité mixte. Le fait de voir quelqu’un que vous reconnaissez, qu’il s’agisse d’une célébrité, d’un collègue ou d’un autre, crée une profondeur de odeurs jamais auparavant possible dans un support numérique. Leur visage, leurs expressions, les nuances dans leurs mouvements font tous partie d’entre eux. Quelles opportunités sont déverrouillées quand nous pouvons capturer ces qualités humaines dans l’espace 3D ?

À l’heure actuelle, l’équipe pousse les limites de la vidéo volumétrique en se concentrant sur des secteurs tels que le divertissement et l’éducation : [Actiongram](https://www.microsoft.com/p/actiongram/9nblggh5ftmt) contient des caractères créatifs et [célébrités](https://www.youtube.com/watch?v=BwWueXlsOrA) pour créer des histoires de réalité mixte. [Destination : mars](https://www.jpl.nasa.gov/news/news.php?feature=6220), à présent dans le centre d’espace Kennedy de NASA, propose une vidéo volumétrique de légendaires. astronautes. L’expérience permet aux visiteurs de parcourir la surface de mars avec un bourdonnement lorsqu’il introduit la poursuite des Colonization humains sur mars.

## <a name="humans-are-fundamental-to-mixed-reality"></a>Les êtres humains sont essentiels à la réalité mixte

Concevoir des moyens de faire de ces vidéos un défi naturel pose un défi, mais l’équipe voit un potentiel énorme. Ces opportunités s’étendront à mesure que la technologie sera plus accessible et passera des enregistrements à la capture en temps réel.

[Holoportation](https://www.microsoft.com/research/project/holoportation-3/) est un effort de recherche qui repose sur la même technologie fondamentale, qui capture de manière authentique des informations visuelles et détaillées, et qui restitue le résultat en temps réel. L’équipe explore la puissance des moyens de représentation humaine réalistes pour l’avenir des conversations et des expériences partagées. Que se passe-t-il lorsqu’une capture tridimensionnelle d’une personne, depuis n’importe où dans le monde, peut être ajoutée à votre environnement ?

![Avenir de la conversation](images/girl-with-dress.jpg)

De la superposition d’un nouveau niveau d’immersion aux applications quotidiennes telles que Skype, pour remodeler radicalement le concept de réunions numériques et de voyages d’affaires, la vidéo volumétrique ouvre des scénarios uniques : un spécialiste en formation virtuelle sur un continent éloigné ou une amis assis sur les canapés et les chaises dans votre salon. L’ajout de représentations humaines authentiques à des expériences de réalité mixte reformera radicalement le concept de réunions numériques et de voyages d’affaires.

Tout comme l’art abstrait de James Turrell et le réalisme critique de l’IA Weiwei offrent leurs propres défis techniques uniques, les méthodes pour représenter les êtres humains comme des avatars créatifs et des captures réalistes. Vous ne pouvez pas l’ignorer à la lumière de l’autre et l’exploration du potentiel de chacun nous aidera à comprendre l’interaction humaine dans ce nouvel espace.

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse" padding-left="0px">
<tr>
<td style="border-style: none" width="60"><img alt="Picture of Mark Vitazko" width="60" height="60" src="images/mark-vitazko.jpg"></td>
<td style="border-style: none"><b>Marquer Vitazko</b><br>@Microsoft du concepteur UX</td>
</tr>
</table>
