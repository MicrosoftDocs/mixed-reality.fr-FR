---
title: Sonorisation spatiale
description: Son spatial est un outil puissant pour immersion, d’accessibilité et la conception de l’expérience utilisateur dans les applications de réalité mixte.
author: joekellyms
ms.author: joekelly
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, son spatial, de conception, de style
ms.openlocfilehash: c8f5268faf5eef779401c046947c3137d177cb89
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593270"
---
# <a name="spatial-sound-design"></a>Sonorisation spatiale

Son spatial est un outil puissant pour immersion, d’accessibilité et la conception de l’expérience utilisateur dans les applications de réalité mixte.

Si vous avez déjà lu [Marco Polo](https://en.wikipedia.org/wiki/Marco_Polo_(game)), ou quelqu'un avait à appeler votre téléphone pour vous aider à vous la localiser, vous êtes déjà familiarisé avec l’importance de son spatial. Nous utilisons des signaux audio dans nos vies quotidiennes pour rechercher des objets, l’attention d’une personne ou obtenir une meilleure compréhension de notre environnement. Plus étroitement les sons de votre application se comportement comme il le fait dans le monde réel, les plus convaincantes et attrayantes que votre monde virtuel sera.

<br>

> [!VIDEO https://www.youtube.com/embed/aB3TDjYklmo]

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Fonctionnalité</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> Son spatial</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="four-key-things-spatial-sound-does-for-mixed-reality-development"></a>Quatre éléments clés son spatial fait pour le développement de la réalité mixte

Par défaut, les sons sont lus en stéréo. Cela signifie que le son est lu avec aucune position spatiale, afin de l’utilisateur ne sait pas d'où provenance le son. Son spatial effectue quatre points clés pour le développement de réalité mixte :

**Mise à la terre**

Sans le son, des objets virtuels efficacement cessent d’exister lorsque nous activons les notre tête. Comme des objets réels, que vous souhaitez être en mesure d’écouter ces objets, même lorsque vous ne pouvez pas les voir, et que vous souhaitez être en mesure de les localiser n’importe où autour de vous. Tout comme les objets virtuels doivent être mis à la terre visuellement pour fusionner avec votre monde réel, ils doivent également être ancrée de façon audible. Son spatial fusionne en toute transparence votre environnement audio du monde réel avec l’environnement audio numérique.

**Attention de l’utilisateur**

Dans les expériences de réalité mixte, vous ne peut pas supposer où votre utilisateur recherche et s’attendre à les voir quelque chose que vous placez dans le monde visuellement. Mais les utilisateurs peuvent toujours entendez une lire même lorsque l’objet qui joue le son est derrière eux. Gens sont habitués à avoir leur attention dessinée par son, nous allons instinctually vers un objet que nous entendons qui nous entoure. Lorsque vous souhaitez diriger regards de vos utilisateurs à une place particulière, plutôt qu’à l’aide d’une flèche pour pointer les visuellement, placez un son dans la mesure où emplacement est un moyen très naturels et rapide pour guider les.

**Immersion**

Lorsque des objets déplacent ou sont en conflit, nous entendons généralement ces interactions entre les documents. Par conséquent, lorsque vos objets n’effectuez pas le même son qu'elles le feraient dans le monde réel, un niveau d’immersion est perdu, à regarder un film effrayant avec le volume vers le bas. Tous les sons dans le monde réel proviennent d’un point particulier dans l’espace - lorsque nous activons nos têtes, nous entendons la modification de ces sons provenance par rapport à nos oreilles, et nous pouvons suivre l’emplacement de son de cette façon. Sons spatialized composent le « impression » d’un emplacement au-delà de ce que nous pouvons voir.

**Conception de l’interaction**

Dans la plupart des expériences interactives, les sons interaction tels que les effets de son interface utilisateur sont lus dans standard mono ou stéréo. Mais étant donné que tous les éléments de réalité mixte existe dans l’espace 3D, y compris l’interface utilisateur - ces objets tirer parti des sons spatialized. Lorsque vous appuyez sur un bouton dans le monde réel, le son, que nous entendons provient de ce bouton. Par spatializing sons d’interaction, nous fournissons à nouveau une expérience utilisateur plus naturelle et réaliste.

## <a name="best-practices-when-using-spatial-sound"></a>Meilleures pratiques lors de l’utilisation de son spatial

**Sons réels fonctionnent mieux que les sons de synthèse ou non naturelles**

Votre utilisateur est plus familiers avec un type de son, le vrai plus sembleront, et plus facilement qu’ils pourront rechercher dans leur environnement. Une voix humaine, par exemple, est un type très courant du son et vos utilisateurs seront localiser aussi rapidement comme une personne réelle dans la salle leur parler.

**Attente prévaut sur la simulation**

Si vous êtes habitué à un son provenant d’une orientation particulière, vous serez guidée votre attention dans cette direction, quel que soit les signaux spatiales. Par exemple, la plupart du temps que nous entendons oiseaux, ils sont au-dessus de nous. Lecture du son d’un oiseau provoquera très probablement votre utilisateur à rechercher, même si vous placez le son au-dessous. Il s’agit généralement de confusion, et il est recommandé que vous travailliez avec les attentes comme ceux-ci, sans devoir contre eux pour une expérience plus naturelle.

**La plupart des sons doivent être spatialized**

Comme mentionné ci-dessus, tous les éléments de réalité mixte existe dans l’espace 3D - votre sons doivent également. Même de la musique peut parfois profiter de spatialisation, en particulier lorsque celle-ci est liée à un menu ou une autre interface utilisateur.

**Éviter les émetteurs invisibles**

Étant donné que nous avons été conditionnées à examiner les sons que nous entendons autour de nous, il peut être une expérience non naturelle et même énervant pour localiser un son qui n’a aucune présence visuelle. Sons dans le monde réel ne proviennent pas d’espace vide, par conséquent, vérifiez que si un émetteur audio est placé dans un environnement immédiat de l’utilisateur qu’il est également visible.

**Éviter les masques spatial**

Son spatial s’appuie sur des signaux acoustiques très subtiles qui peuvent être overpowered par d’autres sons. Si vous n’avez pas son stéréo ou sons ambiantes, assurez-vous qu’ils sont suffisamment faibles dans la combinaison de donner à la place pour les détails de votre sons spatialized qui permettre aux utilisateurs de les localiser facilement, laissez-les sonne réaliste et naturelle.

## <a name="general-concepts-to-keep-in-mind-when-using-spatial-sound"></a>Concepts généraux à prendre en compte lors de l’utilisation de son spatial

**Son spatial est une simulation**

L’utilisation la plus fréquente de son spatial fait un bruit croire qu’émanant d’un objet réel ou virtuel dans le monde. Par conséquent, les sons spatialized peuvent les plus pertinentes provenant de ces objets.

Notez que la précision perçue de moyens spatiales qui ne doivent pas nécessairement émettent d’un son à partir du centre d’un objet, comme la différence est notable selon la taille de l’objet et la distance à partir de l’utilisateur. Avec petits objets, le point central de l’objet est généralement suffisant. Pour des objets plus volumineux, vous souhaiterez peut-être un émetteur audio ou plusieurs émetteurs à l’emplacement spécifique dans l’objet qui est supposé pour être produire le son.

**Normaliser toutes les sons**

Atténuation de la distance se produit rapidement dans le premier compteur à partir de l’utilisateur, comme il le fait dans le monde réel. Tous les fichiers audio doivent être normalisées pour garantir une atténuation distance physiquement précis et vous assurer qu’un entendre lorsque plusieurs mètres (le cas échéant). Le moteur audio spatial gérera la nécessaire pour un son à « sentir » comme il se trouve à une certaine distance (avec une combinaison d’atténuation et des « signaux à distance »), et appliquer toute atténuation en cela peut réduire l’effet d’atténuation. En dehors de la simulation d’un objet réel, initial de DÉSINTÉGRATION de distance *son spatial* sons seront sans doute plus que suffisant pour une une bonne combinaison du son.

**Objet découverte et des interfaces utilisateur**

Lorsque vous utilisez des signaux audio pour diriger l’attention des utilisateurs au-delà de leur vue actuelle, le son doit être audible et mis en évidence dans la combinaison, bien au-dessus des sons stéréo, tous les autres sons spatialized qui peuvent vous détournera pas de la pile audio directionnelle. Pour les sons et la musique qui sont associés à un élément de l’interface utilisateur (par exemple, un menu), l’émetteur audio doit être attaché à cet objet. Stéréo et autres lecture audio non positionnels peuvent compliquer les éléments spatialized permettant aux utilisateurs de localiser (voir ci-dessus : Évitez de masquage spatial).

**Utiliser le son spatial sur son 3D standard autant que possible**

En réalité mixte, pour une expérience utilisateur optimale, audio 3D doit être obtenue à l’aide de son spatial plutôt que des technologies audio 3D héritées. En général, l’amélioration spatialisation dépasse vaut-elle le coût UC small 3D standard audio. Audio 3D standard peut être utilisé pour les sons de faible priorité, les sons spatialized mais pas nécessairement liés à un objet physique ou virtuel et les objets que l’utilisateur devez localiser jamais pour interagir avec l’application.

## <a name="see-also"></a>Voir aussi
* [Son spatial](spatial-sound.md)
* [Mappage spatial](spatial-mapping.md)
