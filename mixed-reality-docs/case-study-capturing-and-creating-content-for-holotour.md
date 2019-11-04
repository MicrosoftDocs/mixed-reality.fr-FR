---
title: Étude de cas-HoloTour
description: HoloTour pour Microsoft HoloLens fournit des présentations personnelles en 3D immersifs d’emplacements sous forme à travers le monde. Cette étude de cas vous guidera tout au long du processus de capture et de création du contenu utilisé pour HoloTour.
author: DannyAskew
ms.author: daaske
ms.date: 03/21/2018
ms.topic: article
keywords: HoloTour, HoloLens, Windows Mixed Reality
ms.openlocfilehash: 035bec9b0d46a31978bc91f23bfb3a5ee47d6247
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73436926"
---
# <a name="case-study---holotour"></a>Étude de cas-HoloTour

HoloTour pour Microsoft HoloLens fournit des présentations personnelles en 3D immersifs d’emplacements sous forme à travers le monde. À mesure que les concepteurs, les artistes, les producteurs, les concepteurs audio et les développeurs qui travaillent sur ce projet, la création d’un rendu 3D convaincant d’un emplacement bien connu prend une fusion unique des encadrement créatives et technologiques. Cette étude de cas vous guidera tout au long du processus de capture et de création du contenu utilisé pour HoloTour.

## <a name="the-tech"></a>Le Tech

Avec HoloTour, nous souhaitons permettre aux utilisateurs de visiter certaines des destinations les plus étonnantes du monde, comme les [Ruins de Machu Picchu](https://en.wikipedia.org/wiki/Machu_Picchu) au Pérou ou la journée moderne [Piazza Navona](https://en.wikipedia.org/wiki/Piazza_Navona) en Italie, directement à partir de leurs propres salles vivantes. Notre équipe a fait de l’esprit l’objectif de la HoloTour « vous sentir comme vous le faites. » L’expérience était plus qu’une simple image ou une vidéo. En tirant parti de l’affichage unique, du suivi et de la technologie audio de HoloLens, nous avons pensé que nous avions pratiquement pu vous transporter vers un autre emplacement. Nous aurions besoin de capturer les paysages, les sons et la géométrie à trois dimensions de chaque emplacement visité, puis de le recréer dans notre application.

Pour ce faire, nous avons besoin d’une caméra de 360 ° pour la capture audio directionnelle. Elle devait être capturée à une résolution extrêmement élevée, afin que le pied de page apparaisse plus clair lorsqu’il est lu sur un HoloLens et que les caméras doivent être positionnées de manière étroite pour réduire les artefacts d’assemblage. Nous voulions une couverture sphérique complète, pas seulement le long de l’horizon, mais au-dessus et au-dessous. La plate-forme devait également être portable pour que nous puissions l’emporter dans le monde entier. Nous avons évalué les options prêtes à l’emploi et réalisé qu’elles n’étaient tout simplement pas suffisantes pour réaliser notre vision, en raison de la résolution, du coût ou de la taille. Si nous n’avons pas trouvé de plate-forme de caméra qui répond à nos besoins, nous devrions en créer une nous.

### <a name="building-the-rig"></a>Génération de la plate-forme de test

La première version, créée à partir de carton, Velcro, bande de conduit et 14 caméras GoPro, était un MacGyver qui aurait été fier. Après avoir examiné tous les aspects des solutions de bas de gamme aux plates-formes personnalisées, les caméras GoPro étaient finalement la meilleure option pour nous car elles étaient petites, abordables et avaient un stockage en mémoire facile à utiliser. Le facteur de forme réduite était particulièrement important, car il nous permettait de placer des caméras relativement proches, plus la distance entre les caméras est petite, plus les artefacts de combinaison seront petits. Notre agencement unique de l’appareil photo nous permettait de bénéficier d’une couverture complète de toutes les sphères, *plus* suffisamment de repiquages pour aligner intelligemment les caméras et lisser certains artefacts pendant le processus de combinaison.

Tirer parti des capacités [spatiales du son](spatial-sound.md) sur HoloLens est essentiel à la création d’une expérience immersive convaincante. Nous avons utilisé un tableau à quatre microphones situé sous les caméras sur le trépied, qui capture le son à partir de l’emplacement de notre caméra dans quatre directions, ce qui nous donne suffisamment d’informations pour créer des sons spatiaux dans nos scènes.

![Notre plateforme de 360 ° caméra configurée pour la vidéo en dehors du Pantheon.](images/camera-pantheon-200px.png)

Notre plateforme de 360 ° caméra configurée pour la vidéo en dehors du Pantheon. 


Nous avons testé notre plate-forme organiser en la mettant à Rattlesnake en relief près de Seattle, en capturant le décor en haut du randonnée. Le résultat, bien qu’il soit beaucoup moins poli que les emplacements que vous voyez dans HoloTour aujourd’hui, nous a donné la certitude que notre conception de la plate-forme était suffisamment bonne pour vous faire penser que vous en êtes vraiment là.

Nous avons mis à niveau notre plate-forme à partir de Velcro et de carton vers un logement d’appareil photo en 3D et acheté des packs de batterie externes pour les caméras GoPro afin de simplifier la gestion des batteries. Nous avons ensuite effectué un test plus complet, qui est en déplacement vers San Francisco pour créer une visite miniature de la côte de la ville et du pont sous forme Golden Gate. Cette plate-forme d’appareil photo correspond à ce que nous avons utilisé pour la plupart de nos captures des emplacements que vous visitez dans HoloTour.

![La vidéo de 360 la plate-forme de Machu Picchu.](images/camera-machu-pichu-500px.png)

La vidéo de 360 la plate-forme de Machu Picchu. 

## <a name="behind-the-scenes"></a>En arrière-plan

Avant de filmer, nous devions déterminer les emplacements que nous souhaitons inclure dans notre visite virtuelle. Rome était le premier emplacement que nous avons prévu d’expédier et nous voulions le faire juste, donc nous avons décidé de faire un voyage à l’avance. Nous avons envoyé une équipe de six personnes, y compris des artistes, des concepteurs et des producteurs, pour une visite en personne aux sites que nous envisageons. Le trajet a duré environ 9 jours – 2,5 pour voyages, le reste pour la filmation. (Pour Machu Picchu, nous avons choisi de ne pas faire un voyage Scout, de rechercher à l’avance et de réserver quelques jours de mémoire tampon pour la pellicule.)

À Rome, l’équipe a pris des photos de chaque zone et noté des faits intéressants, ainsi que des considérations pratiques, telles que le déplacement à chaque place et la difficulté à filmer en raison de la foule ou des restrictions. Cela peut sembler une vacances, mais c’est beaucoup de travail. Les journées commencent tôt le matin et seraient ininterrompues jusqu’au soir. Chaque nuit, le métrage a été chargé pour l’équipe à Seattle pour réviser. 

![Notre équipe de capture à Rome.](images/holotour-filming-crew-rome-500px.jpg) 

Notre équipe de capture à Rome. 


Une fois le voyage Scout terminé, un plan final a été créé pour la filmation réelle. Cela nécessitait une liste détaillée de l’endroit où nous allions filmer, le jour et l’heure. Tous les jours à l’étranger étant coûteux, ces voyages devaient être efficaces. Nous avons enregistré des guides et des gestionnaires à Rome pour nous aider à utiliser tous les jours avant le soleil à après le coucher du soleil. Nous devons obtenir le meilleur métrage possible pour vous faire penser à ce que vous êtes vraiment là.

### <a name="capturing-the-video"></a>Capture de la vidéo

Le fait d’effectuer quelques opérations simples au cours de la capture peut simplifier considérablement le traitement. Par exemple, chaque fois que vous assemblez des images à partir de plusieurs caméras, vous obtenez des artefacts visuels, car chaque caméra a une vue légèrement différente. Plus les objets sont proches de l’appareil photo, plus la différence entre les vues est grande, et plus les artefacts de combinaison sont volumineux. Voici un moyen simple de visualiser le problème : maintenez votre pouce devant votre visage et examinez-le avec un seul œil. Basculez maintenant les yeux. Vous verrez que votre curseur semble se déplacer par rapport à l’arrière-plan. Si vous vous éloignez encore de votre visage et que vous répétez l’expérience, votre curseur s’affiche pour vous déplacer moins. Ce mouvement apparent est semblable au problème de combinaison que nous avons rencontré : vos yeux, comme nos appareils photo, ne voient pas exactement la même image, car ils sont séparés par une petite distance.

Étant donné qu’il est beaucoup plus facile d’éviter les pires artefacts tout en filmant plutôt que de les corriger dans le traitement, nous avons essayé de garder les gens et les choses loin de l’appareil photo dans l’espoir que nous pourrions éliminer le besoin d’agrafer des objets de plus en plus étroits. La maintenance d’un grand effacement autour de notre appareil photo était probablement l’un des plus grands défis que nous avions au cours de la prise de vue et nous devions nous rendre créatif pour le faire fonctionner. L’utilisation de guides locaux était une aide importante pour la gestion des foules, mais nous avons également découvert que l’utilisation de signes (et parfois de petits cônes ou sacs de haricot) pour marquer notre espace de film était raisonnablement efficace, surtout puisque nous avons uniquement besoin d’obtenir une petite quantité de métrage à chaque emplacement. Souvent, la meilleure façon d’obtenir une bonne capture consistait à arriver très tôt le matin, avant la plupart des gens.

Certaines autres techniques de capture utiles proviennent directement des pratiques de film traditionnelles. Par exemple, nous avons utilisé une carte de correction des couleurs sur toutes nos caméras et des photos de référence capturées des textures et des objets dont nous pourrions avoir besoin ultérieurement. 

![Une coupe approximative du Picchu Machu avec la carte de correction des couleurs.](images/rough-cut-machu-picchu-500px.png)

Une coupe approximative du métrage de Pantheon avant la combinaison.

### <a name="processing-the-video"></a>Traitement de la vidéo

La capture du contenu de 360 ° n’est que la première étape : un traitement important est nécessaire pour convertir le métrage de la caméra brute que nous avons capturé dans les ressources finales que vous voyez dans HoloTour. Une fois que nous étions à nouveau à l’usage, nous avions besoin de prendre la vidéo de 14 flux de caméra différents et de les convertir en une vidéo continue unique avec des artefacts minimaux. Notre équipe technique a utilisé un certain nombre d’outils pour combiner et peaufiner le métrage capturé et nous avons développé un pipeline pour optimiser le traitement le plus possible. Le métrage devait être combiné, corrigé de la couleur, puis composite pour supprimer les éléments et les artefacts gênants, ou pour ajouter des poches supplémentaires de vie et de mouvement, le tout avec l’objectif d’améliorer ce sentiment d’être réellement présent.

![Une coupe approximative du métrage de Pantheon avant la combinaison.](images/rough-cut-pantheon-500px.png)

Une coupe approximative du métrage de Pantheon avant la combinaison. 


Pour combiner les vidéos, nous avons utilisé un outil appelé [PTGui](https://www.ptgui.com/) et nous l’avons intégré dans notre pipeline de traitement. Dans le cadre du traitement après le traitement, nous avons extrait les images de nos vidéos et avons trouvé un modèle d’assemblage qui était parfait pour l’un de ces cadres. Nous avons ensuite appliqué ce modèle à un plug-in personnalisé que nous avons écrit, ce qui permettait à nos artistes d’effectuer des réglages et d’ajuster le modèle d’assemblage directement lors de la composition dans After Effects. 

![Capture d’écran de PTGui montrant le métrage Pantheon.](images/stitching-tool-pantheon-500px.png)

Capture d’écran de PTGui montrant le métrage Pantheon. 


### <a name="video-playback"></a>Lecture vidéo

Une fois le métrage terminé, nous disposons d’une vidéo transparente, mais elle est très importante, avec une résolution de 8 Ko environ. Le décodage de la vidéo est onéreux et il y a très peu d’ordinateurs capables de gérer une vidéo de 8 Ko. par conséquent, le prochain défi consistait à trouver un moyen de relire cette vidéo sur HoloLens. Nous avons développé un certain nombre de stratégies pour éviter le coût du décodage tout en faisant en sorte que l’utilisateur ait l’impression d’afficher l’intégralité de la vidéo.

L’optimisation la plus simple consiste à éviter de décoder des parties de la vidéo qui ne changent pas. Nous avons écrit un outil pour identifier les zones de chaque scène qui n’ont que peu ou pas de mouvement. Pour ces régions, nous affichons une image statique au lieu de décoder une vidéo pour chaque image. Pour que cela soit possible, nous avons divisé la vidéo massive en plus petits segments.

Nous avons également fait en sorte que tous les pixels décodés ont été utilisés le plus efficacement. Nous avons expérimenté les techniques de compression pour réduire la taille de la vidéo. nous séparons les régions vidéo en fonction des polygones de la géométrie sur laquelle elles seraient projetées. Nous avons ajusté UVs et recompressé les vidéos en fonction de la quantité de détails que les polygones comprenaient. Le résultat de ce travail est que ce qui a démarré comme une vidéo de 8 Ko a été retournée dans de nombreux segments qui semblent presque incompréhensibles jusqu’à ce qu’ils soient réprojetés correctement dans la scène. Pour un développeur de jeux qui comprend le mappage de texture et la compression UV, cela vous semblera probablement familier. 

![Vue complète du Pantheon avant les optimisations.](images/pantheon-before-optimization-500px.png) 

Vue complète du Pantheon avant les optimisations. 


![La moitié droite du Pantheon, traitée pour la lecture vidéo.](images/pantheon-process-video-playback-500px.png) 

La moitié droite du Pantheon, traitée pour la lecture vidéo. 


![Exemple d’une région vidéo unique après l’optimisation et la compression.](images/single-video-region-after-optimization-500px.png) 

Exemple d’une région vidéo unique après l’optimisation et la compression. 


Une autre astuce utilisée consistait à éviter de décoder la vidéo que vous ne Visualisez pas activement. Dans HoloTour, vous ne pouvez voir qu’une partie de la scène complète à un moment donné. Nous décoderons uniquement les vidéos dans ou sous peu en dehors de votre champ de vision (angle de vue). À mesure que vous faites pivoter votre tête, nous commençons à écouter les régions de la vidéo qui se trouvent maintenant dans votre angle d’ouverture et à arrêter celles qui ne se trouvent plus dans celle-ci. La plupart des gens ne remarqueront pas que cela se produit, mais si vous l’éteignez rapidement, vous verrez que la vidéo prend une seconde pour démarrer. dans le même temps, vous verrez une image statique qui s’affiche ensuite en fondu avec la vidéo une fois qu’elle est prête.

Pour que cette stratégie fonctionne, nous avons développé un système de lecture vidéo étendu. Nous avons optimisé le code de lecture de bas niveau afin de rendre le basculement vidéo extrêmement efficace. En outre, nous avons dû Encoder nos vidéos d’une façon spéciale pour pouvoir basculer rapidement vers une vidéo à tout moment. Ce pipeline de lecture prenait beaucoup de temps de développement, nous l’avons mis en œuvre par étapes. Nous avons commencé avec un système plus simple qui était moins efficace, mais qui permettaient aux concepteurs et aux artistes de travailler sur l’expérience et de les améliorer lentement dans un système de lecture plus robuste qui nous permettait d’être expédiés à la barre de qualité finale. Ce système final comportait des outils personnalisés que nous avons créés dans Unity pour configurer la vidéo dans la scène et surveiller le moteur de lecture.

### <a name="recreating-near-space-objects-in-3d"></a>Recréation d’objets proches de l’espace en 3D

Les vidéos constituent la plupart des éléments que vous voyez dans HoloTour, mais il existe un certain nombre d’objets en 3D qui s’affichent à proximité, tels que la peinture dans Piazza Navona, la fontaine à l’extérieur du Pantheon ou la bulle d’air chaud dans laquelle vous vous trouvez pour les scènes aériennes. Ces objets 3D sont importants, car la perception de la profondeur humaine est très bonne, mais pas très bonne loin. Nous pouvons sortir de la vidéo dans la distance, mais pour permettre aux utilisateurs de parcourir leur espace et sembler comme étant vraiment là, les objets les plus proches ont besoin de profondeur. Cette technique est similaire à la nature de ce que vous pouvez voir dans un musée de l’historique naturel, à savoir un diorama qui a des plans d’aménagement d’animaux physiques, des plantes et des spécimens animaux au premier plan, mais qui est remplacé par un dessin de Matt masqué de manière intelligente en arrière-plan.

Certains objets sont simplement des ressources 3D que nous avons créées et ajoutées à la scène pour améliorer l’expérience. La peinture et la bulle d’air chaud rentrent dans cette catégorie, car elles n’étaient pas présentes lors de la pellicule. Comme pour les ressources de jeu, elles ont été créées par un artiste en 3D de notre équipe et texturées de manière appropriée. Nous allons les placer dans nos coulisses près de l’endroit où vous vous posez, et le moteur de jeu peut les afficher dans les deux affichages HoloLens pour qu’ils apparaissent sous la forme d’un objet 3D.

D’autres ressources, comme la fontaine en dehors du Pantheon, sont des objets réels qui existent aux emplacements où nous filmons la vidéo, mais pour mettre ces objets hors de la vidéo et en 3D, nous devons effectuer un certain nombre de choses.

Tout d’abord, nous avons besoin d’informations supplémentaires sur chaque objet. Bien qu’à l’emplacement de la vidéo, notre équipe a capturé un grand nombre de références de ces objets afin que nous ayons suffisamment d’images détaillées pour recréer avec précision les textures. L’équipe a également effectué une analyse [Photogrammetry](https://en.wikipedia.org/wiki/Photogrammetry) , qui construit un modèle 3D à partir de dizaines d’images 2D, ce qui nous donne un modèle approximatif de l’objet à l’échelle parfaite.

Pendant le traitement de notre métrage, les objets qui seront remplacés ultérieurement par une représentation 3D sont supprimés de la vidéo. La ressource 3D est basée sur le modèle Photogrammetry, mais elle est nettoyée et simplifiée par nos artistes. Pour certains objets, nous pouvons utiliser des parties de la vidéo, telles que la texture eau sur la fontaine, mais la plus grande partie de la fontaine est maintenant un objet 3D, qui permet aux utilisateurs de percevoir la profondeur et de la détailler dans un espace limité dans l’expérience. Le fait d’avoir des objets quasi-Spaces comme celui-ci augmente le réalisme et permet de replacer les utilisateurs dans l’emplacement virtuel. 

![Pantheon le métrage avec la fontaine supprimée. Elle sera remplacée par une ressource 3D.](images/object-removal-pantheon-500px.png)

Pantheon le métrage avec la fontaine supprimée. Elle sera remplacée par une ressource 3D.


## <a name="final-thoughts"></a>Réflexions finales

Évidemment, il y avait plus de création de ce contenu que ce que nous avons abordé ici. Il y a quelques scènes : nous aimerions les appeler « perspectives inactives », y compris la bulle de l’air chaud et la lutte contre la Gladiator dans le Colosseum, qui prenait une approche plus créative. Nous les traiterons dans une prochaine étude de cas.

Nous espérons que les solutions de partage à certains des plus grands défis que nous avions en production sont utiles aux autres développeurs et que vous êtes inspiré de l’utilisation de certaines de ces techniques pour créer vos propres expériences immersifs pour HoloLens. (Et si vous le faites, assurez-vous de le partager avec nous sur le [Forum de développement d’applications HoloLens](https://forums.hololens.com/)!)

## <a name="about-the-authors"></a>À propos des auteurs

<table style="border:0">
<tr>
<td style="border:0" width="60px"> <img alt="David Haley" width="60" height="60" src="images/haley.png" /></td>
<td style="border:0" width="408"> <b>David Haley</b> est un développeur senior qui a appris plus sur les plates-formes de caméra et la lecture vidéo que de travailler sur HoloTour.</td>
<td style="border:0" width="60px"> <img alt="Danny Askew" width="60" height="60" src="images/askew.png" /></td>
<td style="border:0" width="408"> <b>Danny Askew</b> est un artiste qui a fait en sorte que votre parcours de Rome était aussi irréprochable que possible.</td>
</tr>
<tr>
<td style="border:0" width="60px"> <img alt="Jason Syltebo" width="60" height="60" src="images/syltebo.png" /></td>
<td style="border:0" width="408"> <b>Jason Syltebo</b> est un concepteur audio qui a fait en sorte que vous pouviez expérimenter les Soundscape de chaque destination que vous visitez, même lorsque vous revenez dans le temps.</td>
<td style="border:0" width="60px"> <img alt="Travis Steiner" width="60" height="60" src="images/steiner.png" /></td>
<td style="border:0" width="408"> <b>Travis Steiner</b> est un directeur de la conception, qui a fait ses recherches, a créé des plans de voyage et des films dirigés sur le site.</td>
</tr>
</table>



## <a name="see-also"></a>Articles associés
* [Vidéo : Microsoft HoloLens : HoloTour](https://www.youtube.com/watch?v=pLd9WPlaMpY)
