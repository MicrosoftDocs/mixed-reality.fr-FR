---
title: Cadre englobant et barre de l’application
description: La barre de l’application est un menu de niveau objet qui contient une série de boutons qui s’affichent sur le bord inférieur des limites d’un hologramme.
author: radicalad
ms.author: adlinv
ms.date: 06/07/2019
ms.topic: article
keywords: Windows Mixed Reality, barre d’application, cadre englobant
ms.openlocfilehash: f09187bc2a3969a8f844711052e15433f5449d6d
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437056"
---
# <a name="bounding-box-and-app-bar"></a>Cadre englobant et barre de l’application
![La délimitation est l’interface standard pour la manipulation d’objets en réalité mixte.](images/640px-boundingbox-hero.jpg)<br>

<br>

---

## <a name="what-is-the-bounding-box"></a>Qu’est-ce que le cadre englobant ?

La délimitation est l’interface standard pour la manipulation d’objets en réalité mixte. Il permet à l’utilisateur de s’assurer que l’objet est actuellement réglable. Sur HoloLens 2, le cadre englobant fonctionne avec la manipulation directe de la main et répond à la proximité de l’utilisateur finger’s. Il affiche des commentaires visuels pour aider l’utilisateur à percevoir la distance par rapport à l’objet.

:::row:::
    :::column:::
        ### <a name="scaling-an-objectbr"></a>Mise à l’échelle d’un objet<br>
        Les angles du rectangle englobant indiquent à l’utilisateur que l’objet peut être mis à l’échelle. Les poignées suivent un modèle largement compréhensible pour ajuster l’échelle. Ce visuel offre aux utilisateurs la zone totale de l’objet, même s’ils ne sont pas visibles en dehors d’un mode de réglage. Ceci est particulièrement important, car s’il n’y figure pas, un objet accroché à un autre objet ou surface peut sembler se comporter comme s’il existait un espace qui ne devrait pas y figurer.<br>
        <br>
        *Boucle vidéo : mise à l’échelle d’un objet via un cadre englobant*
    :::column-end:::
        :::column:::
        espace de ![](images/spacer-20x582.png)<br>
       ![point de vue HoloLens de la mise à l’échelle d’un objet via un cadre englobant](images/HoloLens2_BoundingBox.gif)<br>
    :::column-end:::
:::row-end:::

<br>

:::row:::
    :::column:::
        ### <a name="rotating-an-objectbr"></a>Rotation d’un objet<br>
        Les intuitivité rectangulaires verticaux sur les bords du cadre englobant sont des indicateurs de rotation. Cela permet à l’utilisateur d’effectuer des ajustements plus précis sur les hologrammes placés. Ils peuvent non seulement les ajuster et les mettre à l’échelle, mais également faire pivoter.<br>
        <br>
        *Boucle vidéo : rotation d’un objet à l’aide du cadre englobant*
    :::column-end:::
        :::column:::
        espace de ![](images/spacer-20x582.png)<br>
       ![point de vue HoloLens de la rotation d’un objet à l’aide d’un cadre englobant](images/HoloLens2_BoundingBox_Rotate.gif)<br>
    :::column-end:::
:::row-end:::

<br>

:::row:::
    :::column:::
        ### <a name="visual-feedback-on-hand-proximity-on-hololens-2br"></a>Commentaires visuels sur la proximité de HoloLens 2<br>
        Sur HoloLens 2, il existe un signal visuel supplémentaire qui peut aider la perception de l’utilisateur en profondeur. Un anneau proche de son doigt s’affiche et s’adapte à mesure que l’approche est plus proche de l’objet. L’anneau se convergera en un point lorsque l’état appuyé est atteint. Cet accord visuel aide l’utilisateur à comprendre à quel moment il s’agit de l’objet.<br>
        <br>
        *Boucle vidéo : exemple de retour visuel basé sur la proximité d’un cadre englobant*
    :::column-end:::
        :::column:::
        espace de ![](images/spacer-20x582.png)<br>
       ![des commentaires visuels à proximité](images/HoloLens2_Proximity.gif)<br>
    :::column-end:::
:::row-end:::

<br>

**Pour le développement d’applications Unity, consultez [cadre englobant dans le Toolkit de réalité mixte-Unity.](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)**

<br>

---

## <a name="what-is-the-app-bar"></a>Qu’est-ce que la barre d’application ?

La barre de l’application est un menu de niveau objet qui contient une série de boutons qui s’affichent sur le bord inférieur des limites d’un hologramme. Ce modèle est couramment utilisé pour permettre aux utilisateurs de supprimer et d’ajuster des hologrammes. La barre de l’application a été conçue principalement comme un moyen de gérer les objets placés dans l’environnement d’un utilisateur. Couplée avec le cadre englobant, un utilisateur dispose d’un contrôle total sur l’emplacement et la manière dont les objets sont orientés en réalité mixte.

:::row:::
    :::column:::
        ### <a name="the-app-bar-follows-the-userbr"></a>La barre de l’application suit l’utilisateur<br>
        Étant donné que ce modèle est utilisé avec les objets qui sont verrouillés au monde, lorsqu’un utilisateur se déplace autour de l’objet, la barre de l’application s’affichera toujours sur le côté objets le plus proche de l’utilisateur. Même si ce n’est pas le cas, il obtient le même résultat. empêcher la position d’un utilisateur pour occultait ou bloquer les fonctionnalités qui seraient autrement disponibles à partir d’un autre emplacement dans son environnement. <br>
        <br>
        *Boucle vidéo : à travers un hologramme, la barre de l’application suit*
    :::column-end:::
        :::column:::
        espace de ![](images/spacer-20x582.png)<br>
       ![la marche autour d’un hologramme. La barre de l’application suit.](images/HoloLens2_AppBarFollowing.gif)<br>
    :::column-end:::
:::row-end:::

<br>



**Pour le développement d’applications Unity, consultez [la barre des applications dans le Toolkit de réalité mixte-Unity.](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_AppBar.html)**

<br>

---

## <a name="see-also"></a>Articles associés
* [Objet avec interaction possible](interactable-object.md)
* [Texte dans Unity](text-in-unity.md)
* [Collection d’objets](object-collection.md)
* [Affichage de la progression](progress.md)
