---
title: Cadre englobant de la zone et la barre de l’application
description: La barre des applications est un menu de niveau de l’objet qui contient une série de boutons qui s’affiche sur le bord inférieur des limites d’un hologramme.
author: radicalad
ms.author: adlinv
ms.date: 06/07/2019
ms.topic: article
keywords: Windows Mixed Reality, barre, zone englobante de l’application
ms.openlocfilehash: d289be31129324c6ff419b69dbce52bd8f62eb64
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829684"
---
# <a name="bounding-box-and-app-bar"></a>Cadre englobant de la zone et la barre de l’application
![La délimitation est l’interface standard pour la manipulation des objets dans la réalité mixte.](images/640px-boundingbox-hero.jpg)<br>

## <a name="what-is-the-bounding-box"></a>Quelle est la zone englobante ?

La délimitation est l’interface standard pour la manipulation des objets dans la réalité mixte. Il fournit à l’utilisateur un intuitif que l’objet est actuellement réglable. Les angles indiquent à l’utilisateur que l’objet peut également mettre à l’échelle. Ce visuel intuitif affiche les utilisateurs la zone totale de l’objet : même s’il n’est pas visible en dehors d’un mode d’ajustement. Cela est particulièrement important, car si elle n’était pas il, un objet aligné sur un autre objet ou la surface semble se comporte comme si l’espace autour d’elle et qui ne doivent pas être présents. Sur HoloLens 2, la zone englobante fonctionne avec la manipulation de direct disponible et répond à proximité du doigt de l’utilisateur. Il montre une rétroaction visuelle pour aider l’utilisateur à percevoir la distance à partir de l’objet. 

![HoloLens de point de vue de la mise à l’échelle un objet par le biais de zone englobante](images/HoloLens2_BoundingBox.gif)<br>
*Mise à l’échelle un objet par le biais de zone englobante*

Les descripteurs dans les angles du rectangle englobant suivent un modèle très largement compris pour ajuster l’échelle. 

![HoloLens de point de vue de faire pivoter un objet par le biais de zone englobante](images/HoloLens2_BoundingBox_Rotate.gif)<br>
*Rotation d’un objet par le biais de zone englobante*


![Commentaires visuels sur la proximité de main](images/HoloLens2_Proximity.gif)<br>
*Commentaires visuels en fonction de la proximité*

L’intuitivité rectangulaire verticale sur les bords du rectangle englobant est des indicateurs de rotation. Ainsi, l’utilisateur plus un réglage sur leurs hologrammes placés. Non seulement peuvent ils ajuster et mettre à l’échelle, mais maintenant, faites tourner également.

* Pour le développement d’applications Unity, consultez [englobant sur des Toolkit-Unity de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)



## <a name="what-is-the-app-bar"></a>Quelle est la barre des applications ?

La barre des applications est un menu de niveau de l’objet qui contient une série de boutons qui s’affiche sur le bord inférieur des limites d’un hologramme. Ce modèle est généralement utilisé pour permettre aux utilisateurs la possibilité de supprimer et ajuster hologrammes.

Dans la mesure où ce modèle est utilisé avec des objets qui sont world verrouillé, comme un utilisateur se déplace l’objet de que la barre de l’application affiche toujours sur le côté de l’objet le plus proche de l’utilisateur. Bien que cela n’est pas le billboarding, elle efficacement permet d’obtenir le même résultat ; empêche la position d’occlude d’un utilisateur ou une fonctionnalité de bloc qui serait disponible à partir d’un autre emplacement dans leur environnement.

![Vous épargne un hologramme. La barre des applications suit.](images/HoloLens2_AppBarFollowing.gif)<br>
*Vous épargne un hologramme, suit de la barre des applications*

La barre de l’application a été conçue principalement comme un moyen de gérer les objets placés dans un environnement d’utilisateur. Associé à la zone englobante, un utilisateur a un contrôle total sur où et comment les objets sont orientées en réalité mixte.

* Pour le développement d’applications Unity, consultez [barre de l’application sur des Toolkit-Unity de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html)

## <a name="see-also"></a>Voir aussi
* [Objet avec interaction possible](interactable-object.md)
* [Texte dans Unity](text-in-unity.md)
* [Collection d’objets](object-collection.md)
* [Affichage de la progression](progress.md)
