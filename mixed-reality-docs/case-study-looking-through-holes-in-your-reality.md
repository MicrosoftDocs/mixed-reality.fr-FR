---
title: Étude de cas - parcourant des trous dans la réalité
description: Cette étude de cas explique comment implémenter l’effet de « fenêtre magique » sur HoloLens, permettant à l’utilisateur afficher derrière les murs, sous le plancher et dans des ouvertures virtuels au sein de leur environnement réel.
author: EricRehmeyer
ms.author: ericrehm
ms.date: 03/21/2018
ms.topic: article
keywords: Réalité mixte Windows, HoloLens, fenêtre magique, parallaxe
ms.openlocfilehash: 945a09614fbc77400825b524f4e0b591bf7b1f6b
ms.sourcegitcommit: 90ce9415889e7121dd2fd76a893dc3734672881b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64873936"
---
# <a name="case-study---looking-through-holes-in-your-reality"></a>Étude de cas - parcourant des trous dans la réalité

Lorsque nous envisageons de réalité mixte et qu’ils peuvent faire avec Microsoft HoloLens, ils se borner généralement aux questions telles que « Les objets puis-je ajouter à mon espace ? » ou « Que puis-je je couche sur mon espace ? » J’aimerais une autre zone, vous pouvez envisager de mettre en surbrillance, essentiellement un tour de magie possible, à l’aide de la même technologie pour rechercher dans ou via les objets physiques réel autour de vous.

## <a name="the-tech"></a>Les technologies

Si vous avez combattu étrangers comme ils relever vos murs dans  **[RoboRaid](https://www.youtube.com/watch?v=Hf9qkURqtbM)**, déverrouillé un mur au sein de  **[Fragments](case-study-creating-an-immersive-experience-in-fragments.md)**, ou ont été chance Pour voir le hangar à l’infini la dans le  **[expérience Halo 5 E3 en 2015](https://www.youtube.com/watch?v=QDw5QjDtFy8)**, puis vous avez vu à quoi je parle. Selon votre imagination, cette astuce visual utilisable pour placer des trous temporaires dans votre cloisons ou masquer des mondes sous plancher doté d’une faible.

![RoboRaid ajoute les canaux en trois dimensions et autres structure derrière votre murs, visibles uniquement par le biais de trous créés comme les envahisseurs de relever.](images/roboraid-640px.png)

RoboRaid ajoute les canaux en trois dimensions et autres structure derrière votre murs, visibles uniquement par le biais de trous créés comme les envahisseurs de relever.

À l’aide d’une des ces hologrammes uniques sur HoloLens, une application peut fournir l’illusion de contenu derrière votre murs ou via votre plancher de la même façon réalité présente lui-même via une fenêtre en elle-même. Déplacez vous-même gauche, et vous pouvez voir tout ce qui est situé à droite. Obtenir de plus près, et vous pouvez voir un peu plus de tout. La principale différence est que les trous réels permettent, alors que votre plancher obstinément ne vous permettre de grimper par le biais de ce contenu HOLOGRAPHIQUE magique. (Je vais ajouter une tâche à la file d’attente).

## <a name="behind-the-scenes"></a>En arrière-plan

Cette astuce est une combinaison des deux effets. Tout d’abord, HOLOGRAPHIQUE contenu est épinglé au monde à l’aide de « ancres spatiales. » À l’aide de points d’ancrage pour rendre ce contenu est « world-verrouillé » signifie que vous examinez ne visuellement dérive en dehors des objets physiques près, même si vous déplacez ou le système de mappage spatial sous-jacent met à jour son modèle 3D de votre salle de conversation.

Deuxièmement, ce contenu HOLOGRAPHIQUE soit limité visuellement à un espace très spécifique, afin de voir uniquement dans le trou dans la réalité. Ce occlusion est nécessaire de demander un examen via un trou logique, une fenêtre ou une voie d’accès, qui vend l’astuce. Sans quelque chose bloque la majeure partie de la vue, un crack dans l’espace pour une dimension jurassique secret peut ressembler simplement un dinosaure mal placé.

![Cela n’est pas une capture d’écran réelle, mais une illustration de l’aspect de l’underworld secret à partir de 101 de principes de base MR sur HoloLens. Le boîtier noir n’apparaît pas, mais vous pouvez voir le contenu par un trou virtuel. (Lors de la recherche via un périphérique réel, la valeur plancher serait semblent disparaître encore plus, car les yeux concentrer à distance supplémentaire comme si ce n’est pas encore fait.)](images/origamiholecomposited-640px.png)

Ce n’est pas une capture d’écran réelle, mais une illustration de la le secret underworld à partir de la [101 de principes de base MR](holograms-101.md) recherche sur HoloLens. Le boîtier noir n’apparaît pas, mais vous pouvez voir le contenu par un trou virtuel. (Lors de la recherche via un périphérique réel, la valeur plancher serait semblent disparaître encore plus, car les yeux concentrer à distance supplémentaire comme si ce n’est pas encore fait.)

### <a name="world-locking-holographic-content"></a>Verrouillage de monde de contenu HOLOGRAPHIQUE

Dans Unity, à l’origine du contenu HOLOGRAPHIQUE rester verrouillé de monde est aussi simple que l’ajout d’un composant WorldAnchor :

```
myObject.AddComponent<WorldAnchor>();
```

Le composant WorldAnchor s’ajuste en permanence la position et la rotation de son GameObject (et par conséquent, tout autre élément sous cet objet dans la hiérarchie) pour qu’il soit stable relatif à proximité des objets physiques. Lorsque vous créez votre contenu, créez-le de sorte que le tableau croisé dynamique de la racine de votre objet est centré à cette faille virtuel. (Si pivot de l’objet est profondément dans le mur, son légers ajustements dans la position et la rotation est beaucoup plus perceptible, et le trou ne semble pas très stable.)

### <a name="occluding-everything-but-the-virtual-hole"></a>Tout sauf le trou virtuel OCCLUSION

Il existe plusieurs façons pour bloquer l’affichage pour ce qui est masqué dans les murs de manière sélective. Le plus simple est parti du fait que HoloLens utilise un affichage additif, ce qui signifie que les objets entièrement noires apparaissent invisibles. Vous pouvez faire cela dans Unity sans effectuer n’importe quel nuanceur spéciaux ou des astuces de matériau, simplement créer un matériau noir et affectez-le à un objet que zones dans votre contenu. Si vous ne souhaitez pas vous faire de modélisation 3D, simplement utiliser un certain nombre d’objets de quatre cœurs par défaut et les faire se chevaucher légèrement. Il existe un certain nombre d’inconvénients à cette approche, mais c’est le moyen le plus rapide pour obtenir quelque chose fonctionne, et bien une fidélité faible preuve de l’utilisation de concept est très bien, même si vous pensez que vous souhaiterez peut-être refactoriser plus tard.

À l’approche de « boîte noire » ci-dessus constitue un inconvénient majeur est qu’il ne photographie bien. Pendant que votre effet peut se présenter parfait via l’affichage de HoloLens, les captures d’écran que vous prenez affichera un objet volumineux noir au lieu de ce qui reste de votre mur ou un étage. La raison à cela est que la physiques hologrammes composites matériel et des captures d’écran et la réalité différemment. Nous allons détour par un instant quelques formules mathématiques faux...

*Alerte de mathématiques faux ! Les nombres et les formules sont destinés à illustrer un point, afin de ne pas être tout type de mesure précise !*

Ce que vous voyez via HoloLens :

```
( Reality * darkening_amount ) + Holograms
```

Ce que vous voyez dans les captures d’écran et de vidéo :

```
( Reality * ( 1 - hologram_alpha ) ) + Holograms * hologram_alpha
```

En anglais : Ce que vous voyez via HoloLens est une simple combinaison de réalité sombre (tel que via lunettes de soleil) et tout ce qui hologrammes l’application souhaite afficher. Mais lorsque vous prenez une capture d’écran, les images de la caméra sont fusionnée avec hologrammes de l’application en fonction de la valeur de transparence par pixel.

Une façon de contourner ce problème consiste à modifier le matériel de « boîte noire » pour uniquement écrire dans le tampon de profondeur et trier avec tous les autres documents opaques. Pour obtenir un exemple de cela, consultez le [fichier WindowOcclusion.shader le MixedRealityToolkit sur GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Common/Shaders/WindowOcclusion.shader). Les lignes correspondantes sont copiés ici :

```
"RenderType" = "Opaque"
"Queue" = "Geometry"
ColorMask 0
```

(Notez le « décalage 50, 100 » ligne consiste à gérer les problèmes non liés, donc il serait probablement judicieux que ne pas définir.)

Implémentation d’un matériau occlusion invisible comme celle-ci sera permettent à votre application de dessiner une zone qui semble correcte dans l’affichage et des captures d’écran de réalité mixte. Pour les points de bonus, vous pouvez essayer d’améliorer les performances de cette zone encore plus loin en effectuant des opérations intelligentes pour dessiner un nombre moindre de pixels invisibles, mais qui peut vraiment obtenir dans les plantes et généralement ne sera pas nécessaire.

![Voici le secret underworld de MR bases 101 Unity dessine, sauf pour les parties externes de la zone OCCLUSION. Notez que le tableau croisé dynamique pour l’underworld est au centre de la zone, qui vous aide à conserver le trou comme stable que possible par rapport à votre plancher réelle.](images/underworld-occluded-640px.png)

Voici le secret underworld à partir de [MR bases 101](holograms-101.md) comme Unity dessine, sauf pour les parties externes de la zone OCCLUSION. Notez que le tableau croisé dynamique pour l’underworld est au centre de la zone, qui vous aide à conserver le trou comme stable que possible par rapport à votre plancher réelle.

## <a name="do-it-yourself"></a>Faites-le vous-même

Avoir un HoloLens et souhaitez tester l’effet par vous-même ? Le plus simple consiste à faire (sans codage) consiste à installer l’application de visionneuse gratuite 3D, puis charger le [télécharger le fichier the.fbx que j’ai fourni sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/CaseStudy-MagicWindow/MagicWindow) pour afficher un modèle de pot de fleur dans votre salle. Charger sur HoloLens, et vous pouvez voir l’illusion au travail. Lorsque vous êtes devant le modèle, vous pouvez uniquement afficher dans le trou petit, tout le reste est invisible. Examiner le modèle à partir de n’importe quel autre côté, il disparaît entièrement. Utilisez le déplacement, la rotation et la mise à l’échelle des contrôles de visionneuse 3D pour positionner le trou virtuel sur n’importe quelle surface verticale, que vous pouvez considérer pour générer des idées !

![Affichage de ce modèle dans votre éditeur Unity affichera une grande boîte noire autour du préfabriqué. Sur HoloLens, la zone disparaît, permet un effet magique de fenêtre.](images/magicwindowflowerpotineditor.png)

Affichage de ce modèle dans votre éditeur Unity affichera une grande boîte noire autour du préfabriqué. Sur HoloLens, la zone disparaît, permet un effet magique de fenêtre.

Si vous souhaitez créer une application qui utilise cette technique, consultez le [101 de principes de base MR didacticiel](holograms-101.md) dans le [didacticiels de réalité mixte](tutorials.md). Chapitre 7 se termine par une explosion dans votre étage que révèle un underworld masqué (comme indiqué dans l’illustration ci-dessus). Vous dites didacticiels devaient être ennuyeux ?

Voici quelques idées où vous pouvez tirer cette idée suivante :
* Imaginer des moyens de rendre le contenu à l’intérieur de la faille virtuelle interactif. Permet à vos utilisateurs ont un impact au-delà de leurs murs peut véritablement améliorer le sens d’étonnant que cette astuce peut fournir.
* Imaginer des moyens de voir, à travers des objets à des domaines connus. Par exemple, comment peut placer un trou HOLOGRAPHIQUE dans votre table de café et consultez votre plancher sous celui-ci ?

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Eric Rehmeyer" width="60" height="60" src="images/genericusertile.jpg"></td>
<td style="border-style: none"><b>Eric Rehmeyer</b><br>Ingénieur logiciel senior @Microsoft</td>
</tr>
</table>

## <a name="see-also"></a>Voir aussi
* [Réalité mixte - Principes fondamentaux - Cours 101 : Projet complet avec appareil](holograms-101.md)
* [Systèmes de coordonnées](coordinate-systems.md)
* [Ancres spatiales](spatial-anchors.md)
* [Mappage spatial](spatial-mapping.md)
