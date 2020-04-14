---
title: Étude de cas-examen des failles dans votre réalité
description: Cette étude de cas explique comment implémenter l’effet « fenêtre magique » sur HoloLens, ce qui permet à l’utilisateur de voir derrière les murs, le plancher et les ouvertures virtuelles au sein de leur environnement réel.
author: ericrehmeyer
ms.author: bestruku
ms.date: 10/18/2019
ms.topic: article
keywords: Windows Mixed Reality, HoloLens, Magic Window, parallaxe
ms.openlocfilehash: c829656c98b7c87f8b969dbbd16115f6a0bbaf27
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81278147"
---
# <a name="case-study---looking-through-holes-in-your-reality"></a>Étude de cas-examen des failles dans votre réalité

Lorsque les gens pensent à la réalité mixte et à ce qu’ils peuvent faire avec Microsoft HoloLens, ils sont généralement confrontés à des questions comme « quels objets puis-je ajouter à ma salle ? ». ou « que puis-je couche en plus de mon espace ? » J’aimerais mettre en évidence une autre zone que vous pouvez prendre en compte, essentiellement une astuce magique, en utilisant la même technologie pour examiner ou parcourir des objets physiques réels autour de vous.

## <a name="the-tech"></a>Le Tech

Si vous avez lutté des étrangers lorsqu’ils sont confrontés à des murs dans **[RoboRaid](https://www.youtube.com/watch?v=Hf9qkURqtbM)** , déverrouillé un mur protégé en **[fragments](case-study-creating-an-immersive-experience-in-fragments.md)** ou si vous étiez suffisamment heureux pour voir le UNSC infini hangar dans l' **[expérience de Halo 5 à E3 dans 2015](https://www.youtube.com/watch?v=QDw5QjDtFy8)** , vous avez vu ce que je parle. En fonction de votre imagination, cette astuce visuelle peut être utilisée pour placer des trous temporaires dans votre cloison ou pour masquer des mondes sous un plancher faible.

![RoboRaid ajoute des canaux à trois dimensions et d’autres structures derrière vos murs, visibles uniquement par des trous créés en tant que saut de envahisseurs.](images/roboraid-640px.png)

RoboRaid ajoute des canaux à trois dimensions et d’autres structures derrière vos murs, visibles uniquement par des trous créés en tant que saut de envahisseurs.

À l’aide de l’un de ces hologrammes uniques sur HoloLens, une application peut fournir l’illusion de contenu derrière vos murs ou à travers votre étage de la même façon que la réalité s’affiche dans une fenêtre réelle. Déplacez-vous vers la gauche et vous pouvez voir tout ce qui se trouve sur le côté droit. Plus près, vous pouvez voir un peu plus de tout. La principale différence réside dans le fait que les véritables failles vous permettent, tandis que votre obstinément ne vous permet pas de passer à ce contenu holographique magique. (J’ajoute une tâche au Backlog.)

## <a name="behind-the-scenes"></a>En arrière-plan

Cette astuce est une combinaison de deux effets. Tout d’abord, le contenu holographique est épinglé au monde en utilisant des « ancres spatiales ». En utilisant des ancres pour que ce contenu soit « verrouillé par le monde », cela signifie que ce que vous regardez ne dérive pas visuellement des objets physiques près de lui, même lorsque vous déplacez ou le système de mappage spatial sous-jacent met à jour son modèle 3D de votre salle.

Deuxièmement, ce contenu holographique est visuellement limité à un espace très spécifique, de sorte que vous ne pouvez voir que dans le trou de votre réalité. Cette occlusion est nécessaire pour que vous ayez besoin d’un trou logique, d’une fenêtre ou d’une porte, qui vend le pli. Sans bloquer la majeure partie de la vue, une fissure dans l’espace d’une dimension Jurassique secrète peut simplement ressembler à un dinosaure mal placé.

![Il ne s’agit pas d’une capture d’écran réelle, mais une illustration de la façon dont le sous-monde secret de la base de connaissances de m. 101 examine HoloLens. Le boîtier noir n’apparaît pas, mais vous pouvez voir le contenu via un trou virtuel. (Lorsque vous examinez un appareil réel, le plancher semble disparaître encore davantage, car vos yeux se focalisent sur une autre distance comme s’il n’y est pas encore.)](images/origamiholecomposited-640px.png)

Il ne s’agit pas d’une capture d’écran réelle, mais une illustration de la façon dont le sous-monde secret de la [base de connaissances de m. 101](holograms-101.md) se penche sur HoloLens. Le boîtier noir n’apparaît pas, mais vous pouvez voir le contenu via un trou virtuel. (Lorsque vous examinez un appareil réel, le plancher semble disparaître encore davantage, car vos yeux se focalisent sur une autre distance comme s’il n’y est pas encore.)

### <a name="world-locking-holographic-content"></a>Contenu holographique de verrouillage universel

Dans Unity, il est aussi facile de faire en sorte que le contenu holographique reste verrouillé en ajoutant un composant WorldAnchor :

```
myObject.AddComponent<WorldAnchor>();
```

Le composant WorldAnchor ajuste en permanence la position et la rotation de son GameObject (et donc de tout autre élément sous cet objet dans la hiérarchie) pour le maintenir stable par rapport aux objets physiques voisins. Lors de la création de votre contenu, créez-le de façon à ce que le pivot racine de votre objet soit centré sur ce trou virtuel. (Si le tableau croisé dynamique de votre objet est profond au mur, ses légères modifications de position et de rotation seront beaucoup plus perceptibles, et le trou peut ne pas sembler très stable.)

### <a name="occluding-everything-but-the-virtual-hole"></a>Boucher tout sauf le trou virtuel

Il existe plusieurs façons de bloquer de manière sélective la vue sur ce qui est masqué dans vos murs. La plus simple tire parti du fait que HoloLens utilise un affichage additif, ce qui signifie que les objets noirs sont invisibles. Vous pouvez effectuer cette opération dans Unity sans avoir à utiliser de nuanceur spécial ou d’astuces matérielles. il vous suffit de créer un matériau noir et de l’affecter à un objet qui contient des zones de votre contenu. Si vous ne vous inquiétez pas de la modélisation 3D, utilisez simplement quelques objets Quad par défaut et faites-les légèrement chevaucher. Cette approche présente un certain nombre d’inconvénients, mais il s’agit de la méthode la plus rapide pour travailler, et l’obtention d’une preuve de concept de faible fidélité est très intéressante, même si vous pensez que vous voudrez peut-être la Refactoriser ultérieurement.

L’une des inconvénients majeurs de l’approche « Black Box » ci-dessus est qu’elle n’est pas bien photographie. Si votre effet peut sembler parfait par le biais de l’affichage de HoloLens, les captures d’écran que vous prenez affichent un gros objet noir au lieu de ce qui reste de votre mur ou de votre plancher. Cela est dû au fait que le matériel physique et les captures d’écran composites sont différents des hologrammes et de la réalité. Nous allons nous pencher sur un moment dans quelques fausses maths...

*Alerte mathématique factice ! Ces chiffres et formules sont destinés à illustrer un point, et non une mesure exacte.*

Ce que vous voyez via HoloLens :

```
( Reality * darkening_amount ) + Holograms
```

Ce que vous voyez dans les captures d’écran et les vidéos :

```
( Reality * ( 1 - hologram_alpha ) ) + Holograms * hologram_alpha
```

En anglais : ce que vous voyez par le biais de HoloLens est une combinaison simple de réalité obscurcie (par exemple, à travers les soleil) et les hologrammes que l’application souhaite afficher. Toutefois, lorsque vous prenez une capture d’écran, l’image de l’appareil photo est fusionnée avec les hologrammes de l’application en fonction de la valeur de transparence par pixel.

Pour contourner ce cas, vous pouvez modifier le matériel « boîte noire » pour écrire uniquement dans le tampon de profondeur et effectuer un tri avec tous les autres matériaux opaques. Pour obtenir un exemple, consultez le [fichier WindowOcclusion. Shader dans le MixedRealityToolkit sur GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Common/Shaders/WindowOcclusion.shader). Les lignes correspondantes sont copiées ici :

```
"RenderType" = "Opaque"
"Queue" = "Geometry"
ColorMask 0
```

(Notez que la ligne « offset 50, 100 » est de traiter les problèmes non liés, c’est pourquoi il est probablement judicieux de le faire.)

L’implémentation d’un matériau d’occlusion invisible comme cela permet à votre application de dessiner une zone qui semble correcte dans l’affichage et dans des captures d’écran de réalité mixte. Pour les points de bonus, vous pouvez essayer d’améliorer encore davantage les performances de cette boîte en faisant des choses astucieuses pour dessiner encore moins de pixels invisibles, mais cela peut s’avérer très utile et ne pas être nécessaire.

![Voici le sous-monde secret de la base de connaissances de m. 101, car Unity les dessine, à l’exception des parties externes de la zone d’occlusion. Notez que le pivot du sous-monde se trouve au centre de la zone, ce qui permet de maintenir le trou aussi stable que possible par rapport à votre étage réel.](images/underworld-occluded-640px.png)

Voici le sous-monde secret de la [base de connaissances de m. 101](holograms-101.md) , car Unity les dessine, à l’exception des parties externes de la zone d’occlusion. Notez que le pivot du sous-monde se trouve au centre de la zone, ce qui permet de maintenir le trou aussi stable que possible par rapport à votre étage réel.

## <a name="do-it-yourself"></a>Faites-le vous-même

Vous avez un HoloLens et souhaitez essayer l’effet pour vous-même ? La méthode la plus simple que vous puissiez faire (aucun codage requis) consiste à installer l’application Free 3D Viewer, puis à charger le [fichier. FBX que j’ai fourni sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/CaseStudy-MagicWindow/MagicWindow) pour afficher un modèle de pot de fleurs dans votre salle. Chargez-la sur HoloLens et vous pouvez voir l’illusion au travail. Lorsque vous êtes devant le modèle, vous ne pouvez voir que dans le petit trou : tout le reste est invisible. Examinez le modèle de tout autre côté et il disparaît entièrement. Utilisez les commandes de mouvement, de rotation et de mise à l’échelle de la visionneuse 3D pour positionner le trou virtuel sur n’importe quelle surface verticale que vous pouvez considérer pour générer des idées.

![L’affichage de ce modèle dans l’éditeur Unity affiche une grande zone noire autour du Flowerpot. Sur HoloLens, la zone disparaît, en donnant un effet à une fenêtre magique.](images/magicwindowflowerpotineditor.png)

L’affichage de ce modèle dans l’éditeur Unity affiche une grande zone noire autour du Flowerpot. Sur HoloLens, la zone disparaît, en donnant un effet à une fenêtre magique.

Si vous souhaitez créer une application qui utilise cette technique, consultez le [didacticiel 101 de base](holograms-101.md) de l’utilisation de la version d’essai de la réalité de la [réalité](tutorials.md). Le chapitre 7 se termine par une explosion de votre étage qui révèle un sous-monde masqué (comme illustré ci-dessus). Qui a dit que les didacticiels devaient être ennuyeuses ?

Voici quelques idées pour vous permettre de suivre cette idée suivante :
* Pensez aux moyens de rendre le contenu à l’intérieur de la fenêtre interactive de trous virtuels. Le fait de permettre à vos utilisateurs d’avoir un impact supérieur à leurs murs peut véritablement améliorer le sens que ce piège peut offrir.
* Pensez aux différentes façons d’afficher les objets dans des zones connues. Par exemple, comment pouvez-vous placer un trou holographique dans votre table café pour voir votre étage sous celui-ci ?

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Eric Rehmeyer" width="60" height="60" src="images/genericusertile.jpg"></td>
<td style="border-style: none"><b>Eric Rehmeyer</b><br>Ingénieur logiciel Senior @Microsoft</td>
</tr>
</table>

## <a name="see-also"></a>Voir aussi
* [MR Basics 101 : finaliser le projet avec l’appareil](holograms-101.md)
* [Systèmes de coordonnées](coordinate-systems.md)
* [Ancres spatiales](spatial-anchors.md)
* [Mappage spatial](spatial-mapping.md)
