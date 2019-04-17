---
title: Étude de cas - à l’aide de son spatial dans RoboRaid
description: Son spatial est une des fonctionnalités plus intéressantes de Microsoft HoloLens, offrant ainsi un moyen permettant aux utilisateurs de percevoir que se passe-t-il autour d’elles lorsque les objets sont en dehors de la ligne de vue.
author: mattzmsft
ms.author: hakons
ms.date: 03/21/2018
ms.topic: article
keywords: Réalité mixte Windows, HoloLens, RoboRaid, son spatial
ms.openlocfilehash: 4bb050b4a4051c121c488ea38e150a8973bd7c04
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594538"
---
# <a name="case-study---using-spatial-sound-in-roboraid"></a>Étude de cas - à l’aide de son spatial dans RoboRaid

Charles Sinex, audio responsable de l’équipe Microsoft HoloLens expérience parle des défis uniques qu’il a rencontré lors de la création audio pour [RoboRaid](https://www.microsoft.com/en-us/p/roboraid/9nblggh5fv3j), un tir de réalité mixte.

## <a name="the-tech"></a>Les technologies

[Son spatial](spatial-sound.md) est une des fonctionnalités plus intéressantes de Microsoft HoloLens, offrant ainsi un moyen permettant aux utilisateurs de percevoir que se passe-t-il autour d’elles lorsque les objets sont en dehors de la ligne de vue.

Dans RoboRaid, l’utilisation la plus évidente et efficace de son spatial est à l’alerte au lecteur de quelque chose qui se produisent en dehors de la vision périphérique de l’utilisateur. Par exemple, entrez le Breacher des murs analysés dans la salle, mais si vous n'êtes pas confronté à l’emplacement où elle est entrée, vous risquez de manquer il. Pour vous prévenir ce invasion, que vous entendrez un peu distinct de contenu audio d’où le Breacher est entré, ce qui vous permet de savoir que vous avez besoin d’agir rapidement pour l’arrêter.

## <a name="behind-the-scenes"></a>En arrière-plan

Le processus de création d’un son spatial pour les applications de HoloLens est par conséquent, nouveaux et uniques et un grand nombre de tête gratter lorsque vous rencontrez un problème peut entraîner l’absence de projets antérieurs à utiliser pour référence. J’espère que ces exemples des défis audio nous avons été confrontés pendant que la fabrication RoboRaid vous aidera à mesure que vous créez audio pour vos propres applications.

### <a name="be-mindful-of-taxing-the-cpu"></a>N’oubliez pas de l’UC de taxation

Son spatiaux peut être importantes sur l’UC. Pour une expérience d’utilisation RoboRaid occupé, il était crucial de conserver les instances de son spatial sous huit à un moment donné. La plupart du temps, il a été aussi simple que la définition de la limite d’instances de différents événements audio afin que toutes les instances qui se produisent une fois que la limite est atteinte sont alors supprimés. Par exemple, lors de drones spawn, leur s ' écrie est limité à trois instances à un moment donné. Étant donné que seulement quatre drones peuvent générer à la fois, trois s ' écrie manquent dans la mesure où il n’existe aucun moyen de votre cerveau garder une trace de que de nombreux événements audio à consonance similaire. Cela libérer des ressources pour les autres événements sonores spatiaux, tels qu’explosions ennemies ou ennemis préparation à dépanner.

### <a name="rewarding-a-successful-dodge"></a>Récompenser une densité réussie

Le garagiste dodging est un des aspects les plus importants de jeu dans RoboRaid et quelque chose que nous avons pensé a été réellement unique à l’expérience de HoloLens. Par conséquent, nous voulions qu’illumine réussie très enrichissant à l’acteur. Nous avons le Doppler « whizz-by » pour paraître intéressante assez tôt dans le développement. Au départ, j’avais prévu d’utiliser une boucle et de les manipuler en temps réel à l’aide de volume, de hauteur et de filtre. L’implémentation de ce point d’être très élaboré, avant de valider les ressources pour créer effectivement cela nous avons donc créé un prototype bon marché à l’aide d’un élément multimédia avec l’effet Doppler intégrées juste pour voir comment il a estimé *. Notre développement embarqué fait afin que cette ressource whizz par lirait des exactement 0,7 secondes avant des projectiles sera dépassée par l’oreille du joueur et les résultats senti extraordinaire ! Inutile de dire que nous abandonne la solution plus complexe et implémenté le prototype.

** (Si vous souhaitez plus d’informations sur la création d’une ressource audio avec l’effet de Doppler intégrée, consultez un article par son concepteur appelé Charles Deenan [100 Whooshes en 2 Minutes](http://designingsound.org/2010/02/charles-deenen-special-100-whooshes-in-2-minutes/).) *
<br>
![Éclaircissement correctement les projectiles un ennemi récompense le lecteur avec un son en whizz satisfaisante.](images/successful-dodge-roboraid-500px.jpg)

### <a name="ditching-ineffective-sounds"></a>Ditching sons inefficaces

À l’origine, nous avions voulu lire une explosion son derrière le lecteur une fois qu’ils ont estompée correctement les projectiles ennemis, mais nous avons décidé d’abandonner ce pour plusieurs raisons. Tout d’abord, elle a décidé aussi efficace que le SFX par whizz, nous avons utilisé pour la densité. Au moment où que les projectiles atteint un mur derrière vous, quelque chose d’autre serait se sont déroulées dans le jeu qui serait presque quantité masque son. Deuxièmement, nous n’avions pas collision sur le sol, donc nous n’avons pas pu obtenir l’explosion de jouer lorsque les projectiles atteint la valeur plancher au lieu des murs. Et enfin, le coût de l’UC de son spatial. L’ennemi Elite Scorpion (celui qui peut analyser à l’intérieur du mur) a une attaque spéciale qui enverra des projectiles environ huit. Non seulement n’avez effectué une énorme pagaille dans la combinaison, il a également introduit awful crépitement, car il a été atteint l’UC trop difficile.

### <a name="communicating-a-hit"></a>Communication d’atteinte

Un problème intéressant que s’est produite, qui nous avons pensé était unique à l’expérience de HoloLens, était la difficulté d’une communication efficace aux joueurs qu’ils ont été atteintes. Ce qui rend une réalité mixte expérience réussie est le sentiment que l’histoire qui se passe pour vous. Cela signifie que vous avez à croire que vous luttez de façon une intrusion robot étranger dans votre propre salon.

Lecteurs évidemment ne sentent quoi que ce soit lorsqu’ils atteint, donc il nous fallait trouver un moyen vraiment convaincre le lecteur que quelque chose de mauvais avaient happed leur. Dans les jeux classiques, vous pouvez voir une animation qui vous permet de savoir votre caractère a pris une baisse, ou l’écran est rouge et votre caractère peut-être un peu grunt. Étant donné que ces types de signaux ne fonctionnent pas dans une expérience de réalité mixte, nous avons décidé de combiner l’indication visuelle avec un signal sonore vraiment exagéré indiquant que vous avez pris les dommages. J’ai créé un son grand et que vous effectuées dans la combinaison il ducked tous les éléments vers le bas. Ensuite, pour faire ressortir même plus, nous avons ajouté un alarme sonore court comme si la réception d’un sub nucléaire. 
<br>
![Lorsqu’un lecteur est atteint dans RoboRaid, ils voir un indice visuel, mais également obtenir un signal audio exagéré lui indiquant qu’ils avez pris les dommages.](images/player-hit-roboraid-500px.jpg)

### <a name="getting-big-sound-from-small-speakers"></a>Obtention de son grand à partir de petits haut-parleurs

HoloLens haut-parleurs sont petits et clair en fonction des besoins de l’appareil, donc vous ne pouvez pas vous attendre à entendre trop bas de gamme. Similaire au développement de Smartphones ou les périphériques de jeu portables, les concepteurs audio et les compositeurs ont être conscient que le contenu de la fréquence de leur audio. J’ai toujours concevoir des sons ou écrire musique avec la plage de fréquences complet, car un casque de port est une option pour les utilisateurs. Toutefois, pour garantir la compatibilité avec les intervenants HoloLens, exécuter un test occasionnellement en plaçant un EQ dans le maître de n’importe quel Dupont, j’ai se produire à travailler dans. Le paramètre EQ se compose d’un filtre passe-haut (pas trop forte pente) à environ 600 à 700 Hz et passe-bas filtrer à environ 10 K (très forte). Qui devrait vous donner une idée approximatif de la façon dont votre sons seront la lecture sur l’appareil.

Si vous comptez sur les basses pour donner au sens de la pression simultanée de la modification dans votre musique, vous trouverez peut-être que votre musique perd complètement le sens de la racine lorsque vous appliquez ce paramètre EQ. Pour résoudre ce problème, j’ai ajouté une autre couche à basses qui sont une octave plus élevée (avec certains papillotement riche) et mixte pour obtenir le sens du dossier racine. Parfois, à l’aide de distorsion à Améliorez encore le papillotement donnera suffisamment contenu fréquence dans la plage supérieure pour rendre nos cerveau croire qu’il y a quelque chose en dessous. Cela vaut pour SFX comme impacts, explosions ou de sons à des instants spéciales, telles que les attaques super d’un responsable. Vraiment vous ne pouvez pas compter sur l’entrée de gamme pour donner le joueur une idée d’impact ou de poids. Comme avec la musique, à l’aide de distorsion pour donner un peu de faites vos sans aucun doute a permis à.

### <a name="making-your-audio-cues-stand-out"></a>Rendre votre signaux audio ressortir

Naturellement, tous les membres de l’équipe souhaitait bombastic musique, des canons à forts et des explosions folles ; mais ils voulaient également entendre voiceover ou toutes autres signaux audio stratégiques sur le jeu.

Sur un jeu de console avec une gamme complète de fréquence, vous avez plusieurs options pour diviser les fréquences selon l’importance du son. Toutefois, pour RoboRaid, j’ai limité dans le nombre de plages de fréquences que je pourrais courbe des sons. Par exemple, si vous utilisez le filtre passe-bas et courbe out trop de ressources à partir de l’extrémité supérieure de la gamme, vous n’aurez rien restant sur le son, car il n’est pas très bas de gamme.

Afin de rendre RoboRaid son aussi grand que possible sur l’appareil, nous avons dû abaisser la plage dynamique de l’intégralité de l’expérience et ai beaucoup utilisé pour laisser en créant une hiérarchie claire d’importance pour différents types de sons. J’ai défini la laisser de -2 à dB-6 selon l’importance. Je ne personnellement aime laisser évidente dans les jeux, donc j’ai passé beaucoup de temps de paramétrage le fondu dans/hors synchronisation et la quantité d’atténuation de volume. Nous configurer bus distincts pour son spatial, son non spatiales, VO et bus dry sans réverbération pour la musique, puis créé bus critiques et non critiques de priorité très élevée. Les ressources ont été ensuite configurer pour accéder à leurs bus appropriés.

J’espère que les professionnels de l’audio quasi-certitude aura autant amusant et l’enthousiasme travailler sur leurs propres applications, comme je l’ai fait de travailler sur RoboRaid. J’ai hâte de voir (et écoutez !) ce que les gens talentueux en dehors de Microsoft seront allumera avec pour HoloLens.

## <a name="do-it-yourself"></a>Faites-le vous-même

Une astuce que j’ai découvert pour rendre certains événements (tels que des explosions) son « supérieure », comme ils remplissent l’espace — consistait à créer un élément mono pour le son spatial et combinez avec une ressource de stéréo 2D, pour être lu en 3D. Prend quelques réglages, étant donné qu’avoir trop d’informations dans le contenu stéréo permettront de réduire la direction des actifs mono. Toutefois, bien l’équilibre approprié entraîne des sons énormes qui obtient les joueurs permettent de convertir leurs têtes de la bonne direction.

Vous pouvez essayer vous-même en utilisant les ressources audio ci-dessous :

**Scénario 1**
1. Télécharger [roboraid_enemy_explo_mono.wav](images/roboraid-enemy-explo-mono.wav) et configurée pour la lecture via son spatial et affectez-le à un événement.
2. Télécharger [roboraid_enemy_explo_stereo.wav](images/roboraid-enemy-explo-stereo.wav) et configurée pour la lecture en 2D stéréo et affecter à l’événement même comme indiqué ci-dessus. Étant donné que ces ressources sont normalisées à Unity, atténuer le volume de ces deux ressources afin qu’il ne découpe pas.
3. Les deux sons ensemble. Déplacer votre tête environ se sentir de comment spatial son nom l’indique.

**Scénario 2**
1. Télécharger [roboraid_enemy_explo_summed.wav](images/roboraid-enemy-explo-summed.wav) et configurée pour la lecture via son spatial et affecter à un événement.
2. Lire cette ressource en lui-même, puis comparer à l’événement du scénario 1.
3. Essayez différents compromis entre les fichiers stéréo et mono.

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Charles Sinex" width="60" height="60" src="images/genericusertile.jpg"></td>
<td style="border-style: none"><b>Charles Sinex</b><br>Ingénieur audio @Microsoft</td>
</tr>
</table>

## <a name="see-also"></a>Voir aussi
* [Son spatial](spatial-sound.md)
* [RoboRaid pour Microsoft HoloLens](https://www.microsoft.com/en-us/p/roboraid/9nblggh5fv3j)
