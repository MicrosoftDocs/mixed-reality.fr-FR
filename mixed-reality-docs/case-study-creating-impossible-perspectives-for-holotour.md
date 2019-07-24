---
title: Étude de cas-création de perspectives impossibles pour HoloTour
description: Nous souhaitons que vos expériences dans HoloTour pour Microsoft HoloLens soient Unforgettable. En plus des arrêts traditionnels du tourisme, nous avons prévu des «perspectives impossibles».
author: DannyAskew
ms.author: daaske
ms.date: 03/21/2018
ms.topic: article
keywords: HoloTour, HoloLens, Windows Mixed Reality
ms.openlocfilehash: be00df73543aa295e1e0dbe1462a888d6bb24954
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63523593"
---
# <a name="case-study---creating-impossible-perspectives-for-holotour"></a>Étude de cas-création de perspectives impossibles pour HoloTour

Nous souhaitons que vos expériences dans HoloTour pour Microsoft HoloLens soient Unforgettable. En plus des arrêts traditionnels du tourisme, nous avons prévu des «perspectives impossibles», qui seraient impossibles à expérimenter sur une visite guidée, mais qui, grâce à la technologie de HoloLens, nous pourrions apporter directement votre salon. La création du contenu pour ces expériences nécessitait des techniques différentes par rapport à notre processus de capture standard.

## <a name="the-content-challenge"></a>Défi du contenu

Il y a certaines scènes dans l’expérience HoloTour, telles que la bulle d’air chaud, sur une fête moderne et la lutte gladiatorial au Colosseum à l’ancien Rome, qui fournissent des vues uniques que vous ne voyez nulle part ailleurs. Ces moments sont censés exciter et amAze vous, ce qui vous permet de vous faire passer des HoloTour plus qu’une simple expérience pédagogique. C’est le moment que nous souhaitons vous souvenir et que vous êtes heureux d’en informer d’autres personnes. Étant donné que nous n’avons pas pu faire passer notre caméra dans le ciel et que nous n’avons pas (encore) de temps, chacun de ces «perspectives impossibles» est appelé pour une approche spéciale de la création de contenu.

## <a name="behind-the-scenes"></a>En arrière-plan

La création de ces moments et perspectives uniques nécessitait plus que la simple pelliculeisation et la modification. Il a fallu beaucoup de temps, des personnes ayant de nombreuses compétences différentes et un peu de magie Hollywood.

### <a name="viewing-rome-from-a-hot-air-balloon"></a>Affichage de Rome à partir d’une bulle d’air chaud

Depuis nos premiers jours de planification, nous savions que nous souhaitions faire des vues aériennes dans HoloTour. La consultation de Rome à partir du ciel vous donne un point de vue que la plupart des gens ne voient jamais et un sens de la localisation spatiale des points de repère populaires. Nous n’avons pas eu à nous faire part de notre caméra existante et de notre plate-forme de microphone.

Tout d’abord, il est important d’expliquer que tous les emplacements que vous visitez dans HoloTour y sont déplacés. Notre objectif était de vous faire savoir que vous êtes vraiment là et, étant donné que vous êtes entouré d’un mouvement où que vous soyez en temps réel, nos destinations virtuelles devaient également transmettre des mouvements ambiants. Par exemple, lorsque vous visitez le Pantheon à votre voyage, vous verrez que les gens s’importent dans le Plaza et congregating sur les étapes. Le mouvement d’arrière-plan vous aide à vous sentir à l’aise avec l’emplacement, plutôt que dans un environnement statique intermédiaire.

Pour créer les vues aériennes pour l’info-bulle, nous avons travaillé avec d’autres équipes chez Microsoft pour obtenir l’accès à l’image panoramique aérienne de Rome. La qualité de ces images était excellente et la vue était remarquable, mais quand nous les avions utilisés dans les coulisses sans modification, elles ont pensé Lifeless par rapport aux autres parties de la visite guidée et l’absence de mouvement s’est dérangée. 


![Le panier d’air chaud, flottant à Rome.](images/hotairballoon1-300px.png)<br>
*Le panier d’air chaud, flottant à Rome*

Pour vous assurer que les emplacements aériens remplissent la même barre de qualité que les autres destinations, nous avons décidé de transformer les photographies statiques en scènes vivantes et en déplacement. La première étape consistait à modifier l’image et le mouvement composite. Nous avons contracté un artiste des effets visuels pour nous aider. La modification a été apportée pour montrer des clouds dérivent lentement, des oiseaux volants de et un plan occasionnel ou un hélicoptère traversant l’horizon. Au fond, un certain nombre de voitures ont été prises pour conduire les rues. Si vous êtes dans la visite guidée de Rome dans HoloTour, il est peu probable que vous ayez explicitement conscience de l’un de ces mouvements. C’est vraiment parfait! Le mouvement subtil n’est pas destiné à attirer l’attention, mais sans ces petites touches, les gens ont remarqué immédiatement qu’il s’agissait d’une image statique dans la scène.

La deuxième chose que nous avons fait vous donne un point de bourré à partir duquel vous pouvez afficher la scène. Vous n’avez pas l’impression que vous y êtes vraiment, s’il semble que vous soyez simplement flottant dans Midair, nous avons donc créé un modèle 3D d’une bulle et vous l’avez placé dans celui-ci. Cela vous permet de vous familiariser avec l’info-bulle et d’examiner le bord pour obtenir un meilleur point de vue. Nous avons trouvé qu’il s’agit d’une façon naturelle et amusante d’expérimenter l’image aérienne.

L’expérience de l’air chaud a présenté des défis uniques pour notre équipe audio, car la logistique nous a empêché d’avoir des microphones qui pointent vers des milliers de mètres sur Rome. Heureusement, nous avions un grand nombre de captures audio ambiantes à travers la ville que nous avons pu utiliser pendant la publication. Nous avons placé les émetteurs audio à leur emplacement relatif à partir duquel ils ont été capturés à partir du sol. L’audio a ensuite été filtré pour le son à distance, comme si vous l’écoutiez du point de vue d’une personne dans la bulle d’air chaud, en fournissant un Soundscape authentique et directionnel pour la scène.

### <a name="time-traveling-to-ancient-rome"></a>Temps de voyage à l’ancien Rome

Les restes de monuments et de bâtiments tout à Rome sont impressionnants même 2000 ans après leur construction, mais nous savions que nous avions une occasion unique de vous montrer ce qu’il serait possible de revenir en arrière et de voir ces structures telles qu’elles apparaissaient à l’ancien Rome.

Naturellement, il n’y a pas de métrage vidéo ou d’image statique du Colosseum tel qu’il apparaissait au moment de sa création. nous avons donc dû créer notre propre image. Nous avons dû faire un grand nombre de recherches pour en savoir plus sur la structure. la compréhension des documents, la consultation des diagrammes architecturaux et la lecture des descriptions historiques pour obtenir suffisamment d’informations pour pouvoir créer une recréation virtuelle. 

![La journée moderne Ruins du Colosseum avec une superposition présentant le plancher de la porte, telle qu’elle aurait été recherchée à l’ancien Rome.](images/rome-colosseum-overlay-500px.png)<br>
*La journée moderne Ruins du Colosseum avec une superposition qui indique le plancher comme il aurait été regardé à l’ancien Rome*

La première chose que nous souhaitions faire était d’améliorer les visites traditionnelles avec des superpositions de formation. Dans HoloTour, lorsque vous visitez le Ruins du Colosseum tel qu’il est aujourd’hui, le plancher est transformé pour vous montrer comment il s’est trouvé en cours d’utilisation, y compris les zones de préproduction souterraines élaborées. Dans une visite guidée normale, vous pouvez avoir ces informations qui vous sont décrites et vous pouvez essayer de l’imaginer, mais dans HoloTour, vous pouvez le voir.

Pour une superposition comme celle-ci, nous avions nos artistes qui correspondent au point de vue de notre métrage de capture et à créer l’image de superposition à la main. La perspective doit correspondre afin que lorsque nous remplaçons la vidéo avec notre image, les deux s’alignent correctement.

### <a name="staging-the-gladiator-fight"></a>Mise en œuvre de la lutte contre la Gladiator

Alors que les superpositions sont un moyen attrayant d’enseigner à l’histoire, ce que nous étions le plus enthousiaste pour le transport de retour dans le temps. La superposition était juste une image d’un point de vue particulier, mais l’heure à laquelle la création de l’ensemble de Colosseum devait être modelée, et, comme nous l’avons vu plus haut, nous avions besoin d’un mouvement dans la scène pour l’amener à l’aise. La réalisation d’un effort considérable a été nécessaire.

Cette entreprise était trop grande pour que notre équipe soit en mesure de la faire, donc notre équipe de dessin a travaillé avec Whiskytree, une société d’effets externes qui travaille généralement sur des effets visuels pour les films d’Hollywood. Whiskytree nous a aidé à recréer le Colosseum dans son Heyday, ce qui nous permet de vous enseigner sur la structure tout en étant debout sur le plancher et de créer une vue d’un combat Gladiator à partir de la boîte de l’empereur. Les retards et les bannières d’ambiance ajoutent le mouvement subtil nécessaire pour que ces derniers soient des emplacements réels et pas seulement des images.

![Colosseum recréé comme vu à partir du plancher. En cas d’affichage dans HoloTour, les bannières sont flottantes dans le Breeze, ce qui donne un sentiment de mouvement.](images/recreated-colosseum-holotour-500px.png)<br>
*Colosseum recréé comme vu à partir du plancher. En cas d’affichage dans HoloTour, les bannières sont flottantes dans le Breeze, ce qui donne un sentiment de mouvement.*

La visite guidée de Rome culmine avec la lutte Gladiator. Whiskytree nous a fourni une vidéo et des simulations de foule en 3D, mais nous avions besoin d’ajouter des Gladiators sur le plancher. Cette partie de notre processus ressemble davantage à une production vidéo d’Hollywood qu’à un projet d’un studio de jeu d’incubation. Les membres de notre équipe ont mis en correspondance une séquence de combat approximative, puis l’ont affiné avec un Choreographer. Nous avons recruté des acteurs pour organiser notre bataille factice et acheté le blindage afin qu’ils recherchent la partie. Enfin, nous avons filmé l’ensemble de la scène sur un écran vert.

![Notre Gladiators, en obtenant des instructions entre les différentes procédures.](images/green-screen-gladiators-holotour-500px.jpg)<br>
*Notre gladiatiors, obtenir des instructions entre les différentes*

Cette scène vous place dans le cadre de l’empereur, ce qui signifiait que tout le métrage devait provenir de cette perspective. Si nous sommes à l’origine de la lutte contre la Gladiators à l’étage, nous n’aurions pas pu correctement répartir la séquence de lutter par la suite. nous avons donc placé notre opérateur d’appareil photo dans une belle levée à la verticale, en observant la séquence de lutte pour la pellicule.

![Obtention de la bonne perspective: filmer à partir d’une levée de ciseaux.](images/scissor-lift-holotour-500px.jpg)<br>
*Obtention de la bonne perspective: filmer à partir d’une levée de ciseaux*

Dans la suite de la production, les Gladiators ont été composites dans le plancher et la perspective était correcte, mais un problème est resté: les ombres du Gladiators sur l’écran vert ont été supprimées dans le cadre du processus de composition. Sans Shadows, les Gladiators étaient flottantes à l’air. Heureusement, Whiskytree est parfait pour résoudre ce type de problème et il a utilisé un peu de encadrement technique pour rajouter des ombres à notre scène. Le résultat est ce que vous voyez dans la visite du jour.

## <a name="about-the-authors"></a>À propos des auteurs

<table style="border:0">
<tr>
<td style="border:0" width="60px"> <img alt="David Haley" width="60" height="60" src="images/haley.png" /></td>
<td style="border:0" width="408"> <b>David Haley</b> est un développeur senior qui a appris plus sur les plates-formes de caméra et la lecture vidéo que de travailler sur HoloTour.</td>

<td style="border:0" width="60px"> <img alt="Jason Syltebo" width="60" height="60" src="images/syltebo.png" /></td>
<td style="border:0" width="408"> <b>Jason Syltebo</b> est un concepteur audio qui a fait en sorte que vous pouviez expérimenter les Soundscape de chaque destination que vous visitez, même lorsque vous revenez dans le temps.</td>
</tr>
<tr>
<td style="border:0" width="60px"> <img alt="Danny Askew" width="60" height="60" src="images/askew.png" /></td>
<td style="border:0" width="408"> <b>Danny Askew</b> est un artiste qui a fait en sorte que votre parcours de Rome était aussi irréprochable que possible.</td>

<td style="border:0" width="60px"></td>
<td style="border:0" width="408"></td>
</tr>
</table>


## <a name="see-also"></a>Voir aussi
* [Vidéo : Microsoft HoloLens : HoloTour](https://www.youtube.com/watch?v=pLd9WPlaMpY)
