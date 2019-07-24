---
title: Cadre englobant et barre de l’application
description: La barre de l’application est un menu de niveau objet qui contient une série de boutons qui s’affichent sur le bord inférieur des limites d’un hologramme.
author: radicalad
ms.author: adlinv
ms.date: 06/07/2019
ms.topic: article
keywords: Windows Mixed Reality, barre d’application, cadre englobant
ms.openlocfilehash: d289be31129324c6ff419b69dbce52bd8f62eb64
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829684"
---
# <a name="bounding-box-and-app-bar"></a>Cadre englobant et barre de l’application
![La délimitation est l’interface standard pour la manipulation d’objets en réalité mixte.](images/640px-boundingbox-hero.jpg)<br>

## <a name="what-is-the-bounding-box"></a>Qu’est-ce que le cadre englobant?

La délimitation est l’interface standard pour la manipulation d’objets en réalité mixte. Il permet à l’utilisateur de s’assurer que l’objet est actuellement réglable. Les angles indiquent à l’utilisateur que l’objet peut également être mis à l’échelle. Ce visuel offre aux utilisateurs la zone totale de l’objet, même s’ils ne sont pas visibles en dehors d’un mode de réglage. Ceci est particulièrement important, car s’il n’y figure pas, un objet accroché à un autre objet ou surface peut sembler se comporter comme s’il existait un espace qui ne devrait pas y figurer. Sur HoloLens 2, le cadre englobant fonctionne avec la manipulation directe de la main et répond à la proximité de l’utilisateur finger’s. Il affiche des commentaires visuels pour aider l’utilisateur à percevoir la distance par rapport à l’objet. 

![HoloLens point de vue de la mise à l’échelle d’un objet à l’aide du cadre englobant](images/HoloLens2_BoundingBox.gif)<br>
*Mise à l’échelle d’un objet à l’aide du cadre englobant*

Les poignées situées aux angles du rectangle englobant suivent un modèle largement compréhensible pour ajuster l’échelle. 

![HoloLens point de vue de la rotation d’un objet par le biais du cadre englobant](images/HoloLens2_BoundingBox_Rotate.gif)<br>
*Rotation d’un objet à l’aide du cadre englobant*


![Commentaires visuels à proximité](images/HoloLens2_Proximity.gif)<br>
*Commentaires visuels en fonction de la proximité*

Les intuitivité rectangulaires verticaux sur les bords du cadre englobant sont des indicateurs de rotation. Cela permet à l’utilisateur d’effectuer des ajustements plus précis sur les hologrammes placés. Ils peuvent non seulement les ajuster et les mettre à l’échelle, mais également faire pivoter.

* Pour le développement d’applications Unity, consultez cadre [englobant sur la réalité mixte Toolkit-Unity](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)



## <a name="what-is-the-app-bar"></a>Qu’est-ce que la barre d’application?

La barre de l’application est un menu de niveau objet qui contient une série de boutons qui s’affichent sur le bord inférieur des limites d’un hologramme. Ce modèle est couramment utilisé pour permettre aux utilisateurs de supprimer et d’ajuster des hologrammes.

Étant donné que ce modèle est utilisé avec les objets qui sont verrouillés au monde, lorsqu’un utilisateur se déplace autour de l’objet, la barre de l’application s’affichera toujours sur le côté objets le plus proche de l’utilisateur. Même si ce n’est pas le cas, il obtient le même résultat. empêcher la position d’un utilisateur pour occultait ou bloquer les fonctionnalités qui seraient autrement disponibles à partir d’un autre emplacement dans son environnement.

![Parcours d’un hologramme. La barre de l’application suit.](images/HoloLens2_AppBarFollowing.gif)<br>
*Si vous vous déplacez autour d’un hologramme, la barre de l’application suit*

La barre de l’application a été conçue principalement comme un moyen de gérer les objets placés dans l’environnement d’un utilisateur. Couplée avec le cadre englobant, un utilisateur dispose d’un contrôle total sur l’emplacement et la manière dont les objets sont orientés en réalité mixte.

* Pour le développement d’applications Unity, consultez la [barre d’application sur la réalité mixte Toolkit-Unity](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html)

## <a name="see-also"></a>Voir aussi
* [Objet avec interaction possible](interactable-object.md)
* [Texte dans Unity](text-in-unity.md)
* [Collection d’objets](object-collection.md)
* [Affichage de la progression](progress.md)
