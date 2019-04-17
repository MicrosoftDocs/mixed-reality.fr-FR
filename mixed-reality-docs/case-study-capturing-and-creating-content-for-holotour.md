---
title: Étude de cas - capture et création de contenu à HoloTour
description: HoloTour pour Microsoft HoloLens fournit des visites personnelles 3D IMMERSIFS des emplacements sous forme d’icône dans le monde entier.
author: DannyAskew
ms.author: daaske
ms.date: 03/21/2018
ms.topic: article
keywords: Windows HoloTour, HoloLens, une réalité mixte
ms.openlocfilehash: 6c9e5f44c439310883c8b0271187a7b2263b0854
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593279"
---
# <a name="case-study---capturing-and-creating-content-for-holotour"></a>Étude de cas - capture et création de contenu à HoloTour

HoloTour pour Microsoft HoloLens fournit des visites personnelles 3D IMMERSIFS des emplacements sous forme d’icône dans le monde entier. En tant que les concepteurs, les artistes, producteurs, concepteurs audio et les développeurs qui travaillent sur ce projet a découvert, la création d’un rendu 3D convaincante réelle d’un emplacement connu prend un ensemble unique de savez-vous exactement créatif et technologique.

## <a name="the-tech"></a>Les technologies

Avec HoloTour, nous voulions que possible pour les personnes à consulter certaines des destinations plus importante au monde, comme le [ruins de Machu Picchu](https://en.wikipedia.org/wiki/Machu_Picchu) dans Pérou ou le jour modern [déployé Navona](https://en.wikipedia.org/wiki/Piazza_Navona) en Italie, directement à partir de leurs propres salons. Notre équipe rendait l’objectif de HoloTour pour « faire vous estimez que vous y êtes vraiment. » L’expérience nécessaire pour être plus que des images ou des vidéos. En tirant parti de l’affichage unique, le suivi et la technologie audio de HoloLens nous croire que nous avons pratiquement vous transport vers un autre emplacement. Il nous faudrait capturer les paysages, sons et la géométrie 3D de chaque emplacement nous visité et puis recréez qui au sein de notre application.

Pour ce faire, nous avions besoin d’une caméra à 360 ° rayon avec la capture audio directionnelle. Il est nécessaire pour capturer à très haute résolution, afin que le tournage ressemblerait clair lors de la lecture sur un HoloLens et les caméras devait être positionné proches afin de réduire les artefacts de liaison. Nous voulions complète sphérique couverture, pas seulement le long de l’horizon, mais au-dessus et au-dessous de vous aussi. La plateforme est également nécessaire pour être portable afin que nous pourrions mettez-le dans le monde entier. Nous évaluée options prêtes à l’emploi disponibles et me suis rendu compte qu’ils simplement n’ont pas été suffisamment efficace pour concrétiser notre vision : soit en raison de la résolution, de coût ou de taille. Si nous n’avons pas pu trouver une plate-forme d’appareil photo qui satisfait nos besoins, nous devrions générer un nous-mêmes.

### <a name="building-the-rig"></a>Création de la plate-forme de test

La première version, effectuées à partir de carton, Velcro, ruban adhésif sur bande et les caméras GoPro 14 — était quelque chose que MacGyver aurait été fier. Après avoir examiné tous les éléments à partir de solutions bas de gamme aux plates-formes fabriqués personnalisés, des caméras de GoPro ont été finalement la meilleure option pour nous, car elles ont été petit, abordable et facile à utiliser la mémoire stockage. Le facteur de forme petit a été particulièrement important, car il a permis de placer des caméras relativement proches, plus la distance entre les caméras est petite, plus les artefacts liaison seront. Notre accord de caméra unique nous a permis à obtenir une couverture complète sphère *plus* suffisamment chevauchement aligner des caméras et aplanir certains artefacts pendant le processus de liaison.

En tirant parti de la [son spatial](spatial-sound.md) fonctionnalités sur HoloLens est essentielle à la création d’une expérience immersive convaincante réel. Nous avons utilisé un tableau de quatre-microphone situé sous les caméras sur trépied, ce qui serait capturer du son à partir de l’emplacement de notre appareil photo dans quatre directions, qui nous donne suffisamment d’informations pour créer des sons spatiales dans notre scènes.

![Notre plateforme d’appareil photo de 360° configurée pour filmer en dehors de la Pantheon.](images/camera-pantheon-200px.png)

Notre plateforme d’appareil photo de 360° configurée pour filmer en dehors de la Pantheon. 


Nous avons testé out notre plate-forme garderez le souvenir en la migrant jusqu'à Ridge Rattlesnake près de Seattle, capture la scène en haut de la randonnée. Le résultat, même si beaucoup moins finalisée que les emplacements que vous consultez dans HoloTour aujourd'hui, nous a donné confiance notre conception de la plateforme de test a été suffisamment efficace pour que vous soyez, vous avez vraiment il.

Nous mis à niveau notre plate-forme Velcro et carton vers un logement de caméra imprimée en 3D et a acheté des packs de batterie externe pour les caméras GoPro simplifier la gestion de la batterie. Ensuite, nous avons un test plus complet, en déplacement à San Francisco pour créer une visite de la miniature de la ville côte d’et le pont de Golden Gate sous forme d’icône. Cette plateforme d’appareil photo est ce que nous avons utilisé pour la plupart de nos captures des emplacements que vous visitez dans HoloTour.

![La plate-forme de caméra à 360° filmer dans Machu Picchu.](images/camera-machu-pichu-500px.png)

La plate-forme de caméra à 360° filmer dans Machu Picchu. 


## <a name="behind-the-scenes"></a>En arrière-plan

Avant de filmer, nous devions figure out quels emplacements nous souhaitons inclure sur notre visite virtuelle. Rome a été le premier emplacement à que nous destinés et nous souhaitions faire correctement, nous avons donc décidé à faire un trajet en utilisant à l’avance. Nous avons envoyé une équipe de six personnes, y compris les artistes, les concepteurs et les producteurs — pour une visite en personne aux sites nous étions en train de proposer. Le voyage a duré environ 9 jours – 2.5 pour les déplacements, le reste pour filmer. (Pour Machu Picchu nous choisi de ne pas pour faire un trajet scout, effectuer des recherches à l’avance et de réservation de quelques jours de la mémoire tampon pour filmer.)

Tandis que dans Rome, l’équipe a pris des photos de chaque zone et noter les faits intéressants, ainsi que des considérations pratiques, comme il est difficile à transiter vers chaque place et la difficulté qu’il serait un film en raison de la foule ou restrictions. Cela peut paraître un congé, mais il y a beaucoup de travail. Jours a commencé tôt le matin et irait sans interruption jusqu'à ce que le soir. Chaque nuit, métrage était chargé pour l’équipe à Seattle pour passer en revue. 

![Notre groupe de capture à Rome.](images/holotour-filming-crew-rome-500px.jpg) 

Notre groupe de capture à Rome. 


Une fois le voyage scout a été terminé, un plan final a été effectué pour filmer réelle. Cette opération nécessaire une liste détaillée des où nous allions film, le jour et à quel moment. Tous les jours à l’étranger sont coûteuse, donc ces allers-retours être efficace. Nous guides et des gestionnaires dans Rome pour nous aider à une réservation et entièrement utilisé tous les jours à partir d’avant de lever du soleil quotidiennes pour après coucher de soleil. Nous devons obtenir le meilleur tournage possible afin que vous soyez, vous avez vraiment il.

### <a name="capturing-the-video"></a>Capture de la vidéo

Faire quelques mesures simples que durant la capture peut faciliter le post-traitement. Par exemple, chaque fois que vous combiner les images à partir de plusieurs appareils photo, vous vous retrouvez avec artefacts visuels, car chaque caméra a une vue légèrement différente. Les objets plus en détail sont à l’appareil photo, la plus grande, la différence entre les vues, et seront plus les artefacts de liaison. Voici un moyen facile de visualiser le problème : prendre en charge votre curseur jusqu'à vos yeux et l’examinez avec uniquement un oeil. Passez maintenant les yeux. Vous verrez que votre curseur s’affiche pour déplacer par rapport à l’arrière-plan. Si vous maintenez votre curseur davantage en dehors de votre visage et répétez l’expérience, votre curseur s’affiche pour déplacer inférieur. Apparent de ce mouvement est similaire au problème de liaison nous devions faire face : Les yeux, comme notre caméras, ne voyez pas la même image exacte, car ils sont séparés par une petite distance.

Car il est beaucoup plus facile empêcher les artefacts pires alors qu’il consiste à les corriger de post-traitement, nous avons essayé de conserver les personnes et les objets éloignés à partir de l’appareil photo dans l’espoir que nous pouvons éliminer la nécessité de relier les gros objets. Maintenance d’un grand effacement autour de notre caméra était probablement un des plus grands défis que nous avons dû au cours de la résolution et nous avons dû être créatif pour qu’il fonctionne. Utilisation des guides locales était une aide non négligeable dans la gestion de fois, mais nous avons également découvert dans qu’à l’aide de signe et parfois petits cônes ou sacs de bean — pour marquer notre espace défavorables n’était raisonnablement efficace, en particulier parce que nous avons simplement dû obtenir un court laps de métrage à chaque emplacement. Souvent la meilleure façon d’obtenir une bonne capture était juste pour arriver très tôt dans la matinée, avant la plupart des gens s’est présenté.

Certaines autres techniques utiles capture proviennent directement des pratiques de film traditionnel. Par exemple, nous avons utilisé une carte de correction des couleurs sur tous nos caméras et photos de référence capturée des textures et des objets, nous aurons besoin plus tard. 

![Ébauche de Picchu Machu affichant la carte de correction des couleurs.](images/rough-cut-machu-picchu-500px.png)

Une ébauche de séquences vidéo Pantheon avant d’assemblage.

### <a name="processing-the-video"></a>Traitement de la vidéo

Capturer du contenu de 360° n'est que la première étape, un grand nombre de traitement est nécessaire pour convertir le tournage caméra brutes nous capturées dans les ressources finales que vous voyez dans HoloTour. Une fois que nous avons retour accueil que nous devions prendre la vidéo à partir de l’appareil photo différents 14 flux et le transformer en une vidéo continue unique avec des artefacts minimales. Notre équipe d’art utilisé un certain nombre d’outils pour combiner et de peaufiner le tournage capturé et nous avons développé un pipeline afin d’optimiser le traitement autant que possible. Le tournage devait être assemblée couleur ensemble, corrigé et ensuite composée pour supprimer des éléments perturbant et des artefacts ou pour ajouter des poches supplémentaires de la vie et de mouvement, tous dans le but d’améliorer ce sentiment d’être réellement il.

![Une ébauche de séquences vidéo Pantheon avant d’assemblage.](images/rough-cut-pantheon-500px.png)

Une ébauche de séquences vidéo Pantheon avant d’assemblage. 


Pour assembler les vidéos, nous avons utilisé un outil appelé [PTGui](http://www.ptgui.com/) et intégrés à notre pipeline de traitement. Dans le cadre de post-traitement nous extraites toujours frames nos vidéos et de trouver un modèle de liaison sans recherche bon pour l’une de ces images. Ensuite, nous avons appliqué ce modèle pour un plug-in personnalisé, que nous avons rédigé qui autorisé notre vidéo artistes pour affiner et ajuster le modèle de liaison directement lors de la composition dans After Effects. 

![PTGui capture d’écran de montrant le tournage Pantheon assemblée.](images/stitching-tool-pantheon-500px.png)

PTGui capture d’écran de montrant le tournage Pantheon assemblée. 


### <a name="video-playback"></a>Lecture vidéo

Une fois le traitement de la séquence est terminé, nous avons une vidéo transparente mais il est extrêmement volumineux, environ 8 K résolution. Décodage de vidéo est coûteux et il existe très peu d’ordinateurs qui peut gérer une vidéo de 8 Ko pour le défi suivant a été recherche un moyen de lire cette vidéo sur HoloLens. Nous avons développé un certain nombre de stratégies pour éviter le coût de décodage tout en rendant la convivialité de l’utilisateur comme ils ont été affichant l’intégralité de vidéo.

L’optimisation de la plus simple consiste à éviter les parties de la vidéo qui ne changent pas beaucoup de décodage. Nous avons écrit un outil pour identifier des zones dans chaque scène qui ont peu ou pas de mouvement. Pour ces régions nous affichons une image statique au lieu d’une vidéo de décodage chaque frame. Pour ce faire, nous avons divisé la vidéo volumineux en petits segments.

Nous avons également veillé à ce que chaque pixel que nous décodés a utilisé plus efficacement. Nous avons expérimenté avec les techniques de compression pour réduire la taille de la vidéo ; Nous séparons les régions vidéo selon les polygones de la géométrie, qu'il serait être projeté sur ; Nous ajustée UVs et réempaquetage les vidéos en fonction de la quantité polygones différent de détail inclus. Le résultat de ce travail est que ce qui a été lancé sous un seul 8k vidéo activé en plusieurs segments qui ressemblent presque inintelligibles jusqu'à ce qu’ils soient correctement ré-projetés dans la scène. Pour un développeur de jeux qui comprend le mappage de texture et de livraison de UV, cela sera probablement familier. 

![Une vue complète de la Pantheon avant les optimisations.](images/pantheon-before-optimization-500px.png) 

Une vue complète de la Pantheon avant les optimisations. 


![La partie droite de la Pantheon, traité pour la lecture vidéo.](images/pantheon-process-video-playback-500px.png) 

La partie droite de la Pantheon, traité pour la lecture vidéo. 


![Exemple d’une seule région vidéo après l’optimisation et de livraison.](images/single-video-region-after-optimization-500px.png) 

Exemple d’une seule région vidéo après l’optimisation et de livraison. 


Une autre astuce que nous avons utilisé a été afin d’éviter le décodage de vidéo que vous n’affichez pas activement. Tandis que dans HoloTour, vous voyez uniquement la partie de la scène complète à un moment donné. Nous décoder uniquement des vidéos dans ou peu de temps en dehors de votre champ de vision (angle d’ouverture). Lorsque vous tournez votre tête, nous commençons à jouer les régions de la vidéo qui se trouvent maintenant dans votre angle d’ouverture et d’arrêtent la lecture de celles qui ne sont plus qu’il contient. La plupart des gens ne remarquerez même pas cela se produit, mais si vous activez rapidement, vous verrez la vidéo prend une seconde pour démarrer, en attendant, vous verrez une image statique les atténuations puis au vidéo une fois qu’il est prêt.

Pour que cette stratégie fonctionne nous avons développé un système complet de la lecture vidéo. Nous avons optimisé le code de lecture de niveau bas afin de rendre la vidéo de commutation extrêmement efficace. En outre, nous avons dû coder nos vidéos d’une manière spéciale pour le rendre possible de basculer rapidement vers n’importe quel vidéo à tout moment. Ce pipeline de la lecture a pris beaucoup de temps de développement afin de nous l’avons implémenté par étapes. Nous avons commencé avec un système plus simple qui était moins efficace, mais les concepteurs autorisées et artistes pour travailler sur l’expérience et lentement l’amélioré à un système de lecture plus robuste qui nous a permis à expédier dans la barre de qualité finale. Ce système final avait des outils personnalisés, que nous avons créé dans Unity pour configurer la vidéo dans la scène et le moniteur le moteur de lecture.

### <a name="recreating-near-space-objects-in-3d"></a>Recréer des objets de près de l’espace 3D

Vidéos constituent la majeure partie de ce que vous voyez dans HoloTour, mais il existe un nombre d’objets 3D qui s’affichent proche de vous, telles que la peinture dans Navona déployé, cette Fontaine en dehors de la Pantheon, ou de la bulle d’air chaud que vous en êtes les scènes aériens. Ces objets 3D sont importantes, car la perception de profondeur humaine est très bonne communiquez, mais pas très bons loin. Nous pouvons vous en sortir avec la vidéo dans la distance, mais pour permettre aux utilisateurs de porter leur espace et de l’apparence, comme elles sont vraiment là, les objets situés à proximité doivent profondeur. Cette technique est similaire au genre de chose que vous pouvez voir dans un musée naturel historique — un diorama aménagement paysager physiques, des plantes et spécimens animales au premier plan, mais s’atténuera dans un dessin cache intelligemment masqué en arrière-plan d’image.

Certains objets sont des composants 3D simplement nous avons créé et ajouté à la scène pour améliorer l’expérience. La peinture et l’info-bulle de l’air chaud appartiennent à cette catégorie, car elles n’étaient pas présents lorsque nous filmé. Comme pour les ressources de jeu, ils ont été créés par un artiste 3D de notre équipe et une texture de façon appropriée. Nous placer dans notre scènes près de votre situation, et le moteur de jeu permettre les afficher pour les deux affichages HoloLens afin qu’ils apparaissent en tant qu’objet 3D.

Autres ressources, comme la Fontaine en dehors de la Pantheon, sont des objets réels qui existent dans les emplacements où nous allons résolution vidéo, mais pour afficher ces objets en dehors de la vidéo et en 3D, nous devons effectuer un certain nombre de choses.

Tout d’abord, nous avons besoin des informations supplémentaires sur chaque objet. Tandis que sur l’emplacement pour filmer, notre équipe capturé un grand nombre de séquences vidéo de référence de ces objets afin que nous devrions suffisamment détaillées des images pour recréer précisément les textures. L’équipe a également un [PHOTOGRAMMÉTRIE](https://en.wikipedia.org/wiki/Photogrammetry) scan, qui construit un modèle parmi des dizaines d’images 2D, 3D qui nous donne un modèle approximatif de l’objet à l’échelle parfait.

Comme nous avons notre métrage de processus, les objets qui seront remplacés ultérieurement avec une représentation 3D sont supprimés de la vidéo. L’élément multimédia 3D est basé sur le modèle PHOTOGRAMMÉTRIE mais nettoyée et simplifié par notre artistes. Pour certains objets, nous pouvons utiliser des parties de la vidéo, telles que la texture de l’eau sur cette Fontaine, mais la plupart de la fontaine est désormais un objet 3D, ce qui permet aux utilisateurs de percevoir de profondeur et remonter autour d’elle dans un espace limité dans l’expérience. Lorsque les objets de près de l’espace ainsi considérablement ajoute à la plus de réalisme et permet à la pour terre des utilisateurs dans l’emplacement virtuel. 

![Métrage pantheon avec cette Fontaine supprimé. Il est remplacé par un élément 3D.](images/object-removal-pantheon-500px.png)

Métrage pantheon avec cette Fontaine supprimé. Il est remplacé par un élément 3D.


## <a name="final-thoughts"></a>Réflexions finales

Évidemment, il a été plus à la création de ce contenu à ce que nous avons abordées ici. Il existe quelques scènes — nous souhaitons les appeler « perspectives impossibles » — y compris la conduite de bulle d’air chaud et le gladiator combattre dans Colosseum, ce qui a pris une approche plus créative. Nous allons y remédier dans une étude de cas futures.

Nous espérons que le partage des solutions à certains des défis plus volumineuses que nous avions lors de la production est utile à d’autres développeurs et que vous êtes inspiré à utiliser certaines de ces techniques pour créer votre propre expérience immersive pour HoloLens. (Et si vous fassiez, vérifiez que partager avec nous sur le [forum de HoloLens Application Development](https://forums.hololens.com/)!)

## <a name="about-the-authors"></a>À propos des auteurs

<table style="border:0">
<tr>
<td style="border:0" width="60px"> <img alt="David Haley" width="60" height="60" src="images/haley.png" /></td>
<td style="border:0" width="408"> <b>David Haley</b> est développeur Senior qui ont appris le plus d’informations sur les plateformes d’appareil photo et de lecture vidéo qu’il pensait possible de travailler sur HoloTour.</td>
<td style="border:0" width="60px"> <img alt="Danny Askew" width="60" height="60" src="images/askew.png" /></td>
<td style="border:0" width="408"> <b>Danny Askew</b> est un artiste de vidéo qui a fait en sorte que votre parcours dans Rome a été comme exempt de failles que possible.</td>
</tr>
<tr>
<td style="border:0" width="60px"> <img alt="Jason Syltebo" width="60" height="60" src="images/syltebo.png" /></td>
<td style="border:0" width="408"> <b>Jason Syltebo</b> est un concepteur Audio qui fait en sorte que vous pouvez constater la soundscape de chaque destination que vous visitez, même lorsque vous revenez en arrière dans le temps.</td>
<td style="border:0" width="60px"> <img alt="Travis Steiner" width="60" height="60" src="images/steiner.png" /></td>
<td style="border:0" width="408"> <b>Travis Steiner</b> est directeur de conception qui examinées scouted emplacements, créé des plans de voyage et dirigé filmer sur site.</td>
</tr>
</table>



## <a name="see-also"></a>Voir aussi
* [Vidéo : Microsoft HoloLens : HoloTour](https://www.youtube.com/watch?v=pLd9WPlaMpY)
