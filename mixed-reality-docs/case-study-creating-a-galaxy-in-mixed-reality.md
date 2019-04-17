---
title: Étude de cas - création d’une galaxie en réalité mixte
description: Avant que Microsoft HoloLens expédié, nous avons demandé notre communauté de développeurs quel type d’application il souhaite voir une équipe interne expérimentée à générer pour le nouvel appareil. Plus de 5 000 idées ont été partagées, et après une interrogation de Twitter 24 heures, le gagnant était une idée appelée « Explorer Galaxy. »
author: KarimLUCCIN
ms.author: kaluccin
ms.date: 03/21/2018
ms.topic: article
keywords: Explorateur de Galaxy, HoloLens, réalité mixte Windows, partager vos idées, étude de cas
ms.openlocfilehash: a478eaa35144a8ee0fbeaeb43cec4b9f901890ab
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597017"
---
# <a name="case-study---creating-a-galaxy-in-mixed-reality"></a>Étude de cas - création d’une galaxie en réalité mixte

Avant que Microsoft HoloLens expédié, nous avons demandé notre communauté de développeurs quel type d’application il souhaite voir une équipe interne expérimentée à générer pour le nouvel appareil. Plus de 5 000 idées ont été partagées, et après une interrogation de Twitter 24 heures, le gagnant était une idée appelée [Galaxy Explorer](galaxy-explorer.md).

Andy Zibits, le responsable de la bibliothèque sur le projet et Karim Luccin, ingénieur de graphiques de l’équipe, parler de l’effort de collaboration entre art et d’ingénierie qui ont conduit à la création d’une représentation précise et interactive du galaxy lactée dans l’Explorateur de Galaxy.

## <a name="the-tech"></a>Les technologies

[Notre équipe](galaxy-explorer.md#meet-the-team) - constitués de deux concepteurs de trois développeurs, quatre artistes, un producteur et un testeur — avait six semaines pour générer une application entièrement fonctionnelle qui permettrait aux utilisateurs d’en savoir plus sur et explorez les vastness et la beauté de notre Galaxy lactée.

Nous souhaitons tirer pleinement parti de la possibilité d’effectuer le rendu des objets 3D directement dans votre espace de vie, donc nous avons décidé de créer un aspect réaliste galaxy où les personnes serait en mesure de zoomer fermer et voir les étoiles individuels, chacun sur leurs propres trajectoires de HoloLens .

Dans la première semaine du développement, nous avons élaboré quelques objectifs pour notre le Galaxy lactée représentation : Il est nécessaire d’avoir une profondeur, de déplacement et la convivialité volumétrique — intégral d’étoiles qui permet de créer la forme du galaxy.

Le problème avec la création d’un galaxy animée qui avait des milliards d’étoiles était que le nombre d’éléments uniques nécessitant la mise à jour serait trop volumineux par trame pour HoloLens animer à l’aide de l’UC. Notre solution impliquait un mélange complexe de l’art et de science.

## <a name="behind-the-scenes"></a>En arrière-plan

Pour permettre aux utilisateurs d’Explorer les étoiles individuels, notre première étape a été de déterminer combien de particules nous aurions pu effectuer le rendu à la fois.

### <a name="rendering-particles"></a>Particules de rendu

UC actuelles est très utiles pour le traitement des tâches en série et jusqu'à quelques tâches parallèles en une seule fois (en fonction du nombre de cœurs sont-ils), mais les GPU sont beaucoup plus efficaces pour traiter des milliers d’opérations en parallèle. Toutefois, car ils ne partagent généralement la même mémoire que l’UC, échange de données entre les UC <> GPU peut rapidement devenir un goulot d’étranglement. Notre solution était de rendre une galaxie sur le GPU, et il devait live complètement sur le GPU.

Nous avons commencé à des tests de contrainte avec des milliers de particules de point dans différents modèles. Cela nous a permis d’obtenir le galaxy sur HoloLens pour voir ce qui a fonctionné et ce qui n’a pas.

### <a name="creating-the-position-of-the-stars"></a>Création de la position des étoiles

Un membre de notre équipe avait déjà écrit le C# code susceptible de générer étoiles à leur position initiale. Les étoiles se trouvent sur une ellipse et leur position pouvant être décrits par (**curveOffset**, **ellipseSize**, **élévation**) où **curveOffset**est l’angle de l’étoile le long de l’ellipse, **ellipseSize** est la dimension de l’ellipse le long de X et Z et l’élévation l’élévation appropriée de l’étoile dans le galaxy. Par conséquent, nous pouvons créer une mémoire tampon ([ComputeBuffer d’Unity](http://docs.unity3d.com/ScriptReference/ComputeBuffer.html)) qui serait initialisée avec chaque attribut en étoile et les envoyer sur le GPU où il serait live pour le reste de l’expérience. Pour dessiner cette mémoire tampon, nous utilisons [DrawProcedural d’Unity](http://docs.unity3d.com/ScriptReference/Graphics.DrawProcedural.html) qui permet d’exécuter un shader (code sur un GPU) sur un ensemble arbitraire de points sans avoir une maille réelle qui représente le galaxy :

**PROCESSEUR :**




```
GraphicsDrawProcedural(MeshTopology.Points, starCount, 1);
```

**GPU :**




```
v2g vert (uint index : SV_VertexID)
{

 // _Stars is the buffer we created that contains the initial state of the system
 StarDescriptor star = _Stars[index];
 …

}
```

Nous avons commencé avec des modèles circulaires brutes avec des milliers de particules. Cela nous a donné la preuve que nous devions nous aurions pu gérer plusieurs particules et l’exécuter à des vitesses de performante, mais nous n’avons pas satisfaits de la forme générale de la galaxy. Pour améliorer la forme, nous avons essayé de différents modèles et les systèmes de particules avec une rotation. Celles-ci étaient initialement prometteurs, car le nombre de particules et performances restée cohérent, mais la forme est tombé en panne près du centre et les étoiles émettait vers l’extérieur qui n’était pas réaliste. Nous avions besoin d’une émission qui nous permettrait de manipuler les temps et que les particules à déplacer dans la pratique, une boucle sans cesse plus étroite au centre du galaxy.

![Nous avons essayé de différents modèles et les systèmes de particules de faire pivoter, comme celles-ci.](images/galaxy-patterns-500px.png)

Nous avons essayé de différents modèles et les systèmes de particules de faire pivoter, comme celles-ci.

Notre équipe a fait des recherches sur la fonction de galaxies moyen et nous avons apporté un système de particules personnalisée spécifiquement pour le galaxy afin que nous pourrions passer les particules basés sur des points de suspension «[théorie sur les ondes de densité](https://en.wikipedia.org/wiki/Density_wave_theory), » qui theorizes qui les branches d’un Galaxy sont des zones de densité plus élevée, mais dans un flux constant, comme un embouteillage. Il semble stable et solide, mais les étoiles bougent vers et depuis les bras lorsqu’ils passent le long de leurs points de suspension respectifs. Dans notre système, les particules existent jamais sur le processeur — nous générer les cartes et les orienter tous sur le GPU, par conséquent, l’ensemble du système est simplement initialState + temps nécessaire. Il s’est déroulée comme suit :

![Progression de système de particules avec le rendu du GPU](images/spiral-galaxy-arms-500px.jpg)

Progression de système de particules avec le rendu du GPU


Une fois que suffisamment points de suspension sont ajoutés et sont définies pour faire pivoter, les galaxies ont commencé au formulaire « armes » où le déplacement des étoiles converger. L’espacement des étoiles sur chaque tracé elliptique ont été fournie à un caractère aléatoire, et chaque étoile a obtenu un peu de caractère aléatoire positionnel ajouté. Cela créé une distribution qui recherchent beaucoup plus naturelle de la forme de mouvement et arm en étoile. Enfin, nous avons ajouté la possibilité de couleur de lecteur en fonction de distance à partir du centre.

### <a name="creating-the-motion-of-the-stars"></a>Création le mouvement des étoiles

Pour animer le mouvement en étoile général, nous avions besoin pour ajouter un angle constant pour chaque trame et pour obtenir des étoiles déplacer le long de leurs points de suspension à une vitesse constante radiale. C’est la raison principale pour l’utilisation de **curveOffset**. Ce n’est pas techniquement correct, comme les étoiles déplacera plus rapidement sur les côtés long des ellipses, mais le mouvement général senti bon.

![Étoiles accélère la migration de l’arc long, plus lent sur les bords.](images/ellipse-movement.jpg)

Étoiles accélère la migration de l’arc long, plus lent sur les bords.


Avec cela, chaque étoile est entièrement décrite par (**curveOffset**, **ellipseSize**, **élévation**, **âge**) où **âge** est une accumulation du temps total écoulé depuis la scène a été chargée.




```
float3 ComputeStarPosition(StarDescriptor star)
{

  float curveOffset = star.curveOffset + Age;
  
  // this will be coded as a “sincos” on the hardware which will compute both sides
  float x = cos(curveOffset) * star.xRadii;
  float z = sin(curveOffset) * star.zRadii;
   
  return float3(x, star.elevation, z);
  
}
```

Cela a permis de générer des dizaines de milliers d’étoiles qu’une seule fois au début de l’application, puis nous animée un ensemble simples d’étoiles sur les courbes établis. Dans la mesure où tout est sur le GPU, le système peut animer tous les étoiles en parallèle sans coût à l’UC.

![Voici à quoi elle ressemble lorsque dessin quadrilatères blancs.](images/drawing-white-quads-300px.jpg)

Voici à quoi elle ressemble lorsque dessin quadrilatères blancs.



Pour rendre chaque face quad l’appareil photo, nous avons utilisé un nuanceur de géométrie pour transformer chaque position en étoile à un rectangle 2D de l’écran qui contient notre texture en étoile.

![Diamants au lieu de quadrilatères.](images/drawing-white-quads-300px.jpg)

Diamants au lieu de quadrilatères.


Étant donné que nous souhaitons limiter les superpositions (nombre de fois où un pixel est traité) autant que possible, nous paysage notre quadrilatères afin qu’ils auraient pas moins se chevauchent.

### <a name="adding-clouds"></a>Ajout de clouds

Il existe de nombreuses façons d’obtenir un sentiment volumétrique avec particules — à partir de ray marching à l’intérieur d’un volume au dessin de particules autant que possible pour simuler un cloud. Ray en temps réel marching allait être trop coûteux et difficile d’auteur, donc nous avons tout d’abord tenté de création d’un système imposteur à l’aide d’une méthode pour les forêts de rendu dans les jeux, avec un grand nombre d’images 2D d’arbres accessible sur l’appareil photo. Lorsque nous le faire dans un jeu, nous pouvons avoir les textures de rendu à partir d’un appareil photo qui pivote autour, enregistrez toutes ces images et lors de l’exécution pour chaque carte billboard des arborescences, sélectionnez l’image qui correspond à la direction de la vue. Cela ne fonctionne pas aussi bien lorsque les images sont hologrammes. La différence entre l’oeil gauche et de l’oeil droit faire en sorte que nous avons besoin d’une plus grande résolution, sans quoi il recherche simplement à plat, un alias, ou répétitives.

Lors de notre deuxième tentative, nous avons essayé d’avoir des particules autant que possible. Les meilleurs visuels ont été obtenus lorsque nous avons dessiné de particules feu et que vous les floue avant de les ajouter à la scène. Les problèmes classiques de cette approche ont été liés à combien de particules nous pouvons dessiner en une seule fois et écran combien ils superficie tout en conservant 60 i/s. Flou de l’image obtenue pour obtenir ce cloud que vous vous sentez était généralement une opération très coûteuse.

![Sans la texture, c’est quoi ressemblerait les clouds avec une opacité de 2 %.](images/clouds-without-texture-300px.jpg)

Sans la texture, c’est quoi ressemblerait les clouds avec une opacité de 2 %.



Additif en cours et avoir un grand nombre d'entre eux signifie que nous devrions plusieurs quadrilatères au-dessus des autres, ombrage à plusieurs reprises le même pixel. Dans le centre du galaxy, le même pixel a des centaines de quadrilatères superposées et cela a un coût considérable lorsque effectué plein écran.

Effectuant des clouds de plein écran et essayez de les flou aurait été une mauvaise idée, par conséquent, au lieu de cela que nous avons décidé de laisser le matériel de faire le travail pour nous.

### <a name="a-bit-of-context-first"></a>Un bit du contexte tout d’abord

Lors de l’utilisation des textures dans un jeu de la taille de texture rarement correspond à la zone que nous souhaitons utiliser dans, mais nous pouvons utiliser différents types de filtrage pour obtenir la carte graphique pour interpoler la couleur que nous voulons des pixels de la texture de texture ([defiltragedeTexture<C3/>). Le filtrage qui nous intéresse est [Filtrage bilinéaire](https://msdn.microsoft.com/library/windows/desktop/bb172357.aspx) qui calcule la valeur d’un pixel à l’aide de la 4 voisins les plus proches.

![Original avant le filtrage](images/texture-1.png)

![Résultat après le filtrage](images/texture-2.png)

À l’aide de cette propriété, nous voyons que chaque fois que nous essayons de dessiner une texture dans une zone à deux reprises en tant que big, brouiller le résultat.

Au lieu de rendu au mode plein écran et perdre ces millisecondes précieux, que nous pourrions passer sur autre chose, nous affichons vers une version minuscule de l’écran. Ensuite, en copiant cette texture et en étirant selon un facteur de 2 plusieurs fois, nous obtenons en plein écran tout en atténuant le contenu dans le processus.

![x3 haut de gamme à pleine résolution.](images/galaxy-resolutions-300px.png)

x3 haut de gamme à pleine résolution.



Cela a permis de récupérer la partie cloud avec uniquement une fraction du coût d’origine. Au lieu d’ajouter des clouds sur la résolution maximale, nous uniquement paint 1/64 pixels et simplement étirer la texture à pleine résolution.

![Gauche, avec un haut de gamme parlent de 1/8 en pleine résolution ; et bien, avec 3 haut de gamme à l’aide de la puissance de 2.](images/stars-upscaled-300px.jpg)

Gauche, avec un haut de gamme parlent de 1/8 en pleine résolution ; et bien, avec 3 haut de gamme à l’aide de la puissance de 2.


Notez que de l’accès à partir de 1/64, la taille pour la version complète la taille d’un coup ressemblerait complètement différente, comme la carte graphique utiliseriez toujours 4 pixels à ombrer une zone plus grande dans notre programme d’installation et d’artefacts commencent à apparaître.

Ensuite, si nous ajoutons les étoiles pleine résolution avec cartes plus petites, nous obtenons le galaxy complète :

![Près de résultat final du rendu galaxy en utilisant les étoiles pleine résolution](images/full-galaxy-500px.png)

Une fois que nous avons sur la bonne voie avec la forme, nous avons ajouté une couche de clouds, permutée les points temporaires avec ceux que nous peints dans Photoshop et ajouté des couleurs supplémentaires. Il en résultait une galaxie lactée notre art et ingénieurs les deux senti bons pour qu’il atteint ses objectifs en matière de profondeur, de volume et de mouvement, tout cela sans imposer de l’UC.

![Notre Galaxy lactée finale en 3D.](images/final-galaxy-500px.jpg)

Notre Galaxy lactée finale en 3D.


### <a name="more-to-explore"></a>Autres points à Explorer

Nous avons le code de l’application Explorateur de Galaxy open source et qu’il est disponible sur [GitHub](https://github.com/Microsoft/GalaxyExplorer) aux développeurs de créer.

Vous souhaitez trouver plus d’informations sur le processus de développement pour Explorer de Galaxy ? Découvrez toutes nos cours projet mises à jour sur le [chaîne YouTube de Microsoft HoloLens](https://www.youtube.com/playlist?list=PLZCHH_4VqpRj0Nl46J0LNRkMyBNU4knbL).

## <a name="about-the-authors"></a>À propos des auteurs

<table style="border:0">
<tr>
<td style="border:0" width="60px"> <img alt="Picture of Karim Luccin at his desk" width="60" height="60" src="images/karim-thumb.jpg" /></td>
<td style="border:0"><b>Karim Luccin</b> est un ingénieur logiciel et un passionné de fantaisie visuels. Il a été l’ingénieur de graphiques pour Explorer de Galaxy.</td>
</tr>
<tr>
<td style="border:0" width="60px"> <img alt="Photo of art lead Andy Zibits" width="60" height="60" src="images/andy-avatar.png" /></td>
<td style="border:0"><b>Andy Zibits</b> est un Art Lead et espace passionné gérés de l’équipe de modélisation 3D pour Explorer de Galaxy et lutté pour encore plus de particules.</td>
</tr>
</table>


## <a name="see-also"></a>Voir aussi
* [Explorer Galaxy sur GitHub](https://github.com/Microsoft/GalaxyExplorer)
* [Mises à jour de projet Galaxy Explorer sur YouTube](https://www.youtube.com/playlist?list=PLZCHH_4VqpRj0Nl46J0LNRkMyBNU4knbL)
