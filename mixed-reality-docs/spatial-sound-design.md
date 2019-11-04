---
title: Conception de son spatial
description: Le son spatial est un outil puissant pour la conception de l’immersion, de l’accessibilité et de l’expérience utilisateur dans les applications de réalité mixte.
author: joekellyms
ms.author: joekelly
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, son spatial, design, style
ms.openlocfilehash: acc568eeb08d2a27574dcfbc9f132519e1e31843
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438291"
---
# <a name="spatial-sound-design"></a>Conception de son spatial

Le son spatial est un outil puissant pour la conception de l’immersion, de l’accessibilité et de l’expérience utilisateur dans les applications de réalité mixte.

Si vous avez déjà joué à [Marco Polo](https://en.wikipedia.org/wiki/Marco_Polo_(game))ou si quelqu’un a appelé votre téléphone pour vous aider à le localiser, vous êtes déjà familiarisé avec l’importance du son spatial. Nous utilisons des signaux sonores dans nos vies quotidiennes pour localiser des objets, attirer l’attention d’une personne ou obtenir une meilleure compréhension de notre environnement. Plus le son de votre application se comporte de la même façon que dans le monde réel, plus votre monde virtuel est convaincant et attrayant.

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/aB3TDjYklmo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## <a name="device-support"></a>Périphériques pris en charge

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Conception de son spatial</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
</table>


## <a name="four-key-things-spatial-sound-does-for-mixed-reality-development"></a>Quatre points clés pour le développement de la réalité spatiale

Par défaut, les sons sont lus en stéréo. Cela signifie que le son est lu sans position spatiale, de sorte que l’utilisateur ne sait pas où provient le son. Le son spatial fait quatre choses clés pour le développement de réalité mixte :

**Terre**

Sans son, les objets virtuels cessent d’exister quand nous éloigneons notre tête. Tout comme les objets réels, vous souhaitez être en mesure d’entendre ces objets même si vous ne les voyez pas et que vous souhaitez être en mesure de les localiser partout. Tout comme les objets virtuels doivent être visuellement mis en terre pour être mélangés à votre monde réel, ils doivent également être mis en terre de manière audible. Le son spatial fusionne en toute transparence votre environnement audio réel avec l’environnement audio numérique.

**Attention de l’utilisateur**

Dans les expériences de réalité mixte, vous ne pouvez pas supposer où votre utilisateur regarde et s’attendre à ce que vous puissiez voir un aspect que vous placez dans le monde visuellement. Toutefois, les utilisateurs peuvent toujours entendre un son audible même lorsque l’objet qui lit le son est derrière. Les gens sont utilisés pour attirer l’attention du son. nous instinctuallyons à un objet que nous entendons nous. Lorsque vous souhaitez diriger le regard de votre utilisateur vers un endroit particulier, plutôt que d’utiliser une flèche pour les pointer visuellement, le fait de placer un son dans cet emplacement est un moyen très naturel et rapide de les guider.

**Immersion**

Lorsque des objets sont déplacés ou en conflit, nous entendons généralement ces interactions entre les matériaux. Ainsi, lorsque vos objets n’ont pas le même son qu’ils le ferait dans le monde réel, un niveau d’immersion est perdu, en regardant un film effrayant avec le volume tout le temps. Tous les sons du monde réel proviennent d’un point particulier dans l’espace, lorsque nous transmettons nos têtes, nous entendons la modification de l’emplacement des sons par rapport à nos oreilles, et nous pouvons suivre l’emplacement de tout son de cette façon. Les sons spatiaux constituent la « sensation » d’un point au-delà de ce que nous pouvons voir.

**Conception d’interaction**

Dans la plupart des expériences interactives traditionnelles, les sons d’interaction sont lus en mono ou stéréo standard. Toutefois, étant donné que tout en réalité mixte existe dans l’espace 3D, y compris l’interface utilisateur, ces objets tirent parti des sons spatiaux. Quand vous appuyez sur un bouton dans le monde réel, le son que nous entendons provient de ce bouton. En spatialeant les sons d’interaction, nous fournissons encore une expérience utilisateur plus naturelle et plus réaliste.

## <a name="best-practices-when-using-spatial-sound"></a>Meilleures pratiques lors de l’utilisation d’un son spatial

**Des sons réels fonctionnent mieux que des sons synthétisés ou non naturels**

Plus votre utilisateur est familiarisé avec un type de son, plus il semblera réaliste et plus il sera facile de le localiser dans son environnement. Une voix humaine, par exemple, est un type de son très courant, et vos utilisateurs la trouveront aussi rapidement qu’une personne réelle dans la salle.

**Simulation des atouts de l’attente**

Si vous êtes utilisé comme un son provenant d’une direction particulière, votre attention sera guidée dans cette direction, indépendamment des indications spatiales. Par exemple, la plupart du temps, nous entendons les oiseaux au-dessus des États-Unis. Le fait de toucher le son d’un oiseau entraînera très probablement la recherche de l’utilisateur, même si vous placez le son en dessous. Ce processus est généralement confus et il est recommandé de travailler avec des attentes comme celles-ci plutôt que de vous en rendre compte pour une expérience plus naturelle.

**La plupart des sons doivent être spatiaux**

Comme indiqué ci-dessus, il existe des sons en réalité dans la réalité mixte. Même la musique peut parfois tirer parti de Spatialization, en particulier lorsqu’elle est liée à un menu ou à une autre interface utilisateur.

**Éviter les émetteurs invisibles**

Étant donné que nous avons eu l’air d’examiner les sons que nous avons appris, il peut s’agir d’une expérience inégalée et même unnerving pour localiser un son sans présence visuelle. Les sons dans le monde réel ne proviennent pas d’un espace vide. Assurez-vous que si un émetteur audio est placé dans l’environnement immédiat de l’utilisateur, il peut également être consulté.

**Éviter le masquage spatial**

Le son spatial repose sur des signaux acoustiques très subtiles qui peuvent être suralimentés par d’autres sons. Si vous avez de la musique stéréo ou des sons ambiants, assurez-vous qu’ils sont suffisamment faibles dans la combinaison pour libérer de l’espace pour les détails de vos sons spatiaux qui permettront à vos utilisateurs de les localiser facilement et de les maintenir réalistes et naturels.

## <a name="general-concepts-to-keep-in-mind-when-using-spatial-sound"></a>Concepts généraux à prendre en compte lors de l’utilisation d’un son spatial

**Le son spatial est une simulation**

L’utilisation la plus fréquente du son spatial fait apparaître un son comme s’il s’agissait d’un objet réel ou virtuel dans le monde. Par conséquent, les sons spatiaux peuvent prendre le plus de sens en provenance de tels objets.

Notez que la précision perçue du son spatial signifie qu’un son ne doit pas nécessairement émettre à partir du centre d’un objet, car la différence sera perceptible en fonction de la taille de l’objet et de la distance de l’utilisateur. Avec les petits objets, le point central de l’objet est généralement suffisant. Pour les objets plus grands, vous pouvez souhaiter un émetteur de sons ou plusieurs émetteurs à l’emplacement spécifique au sein de l’objet qui est supposé produire le son.

**Normaliser tous les sons**

L’atténuation de la distance se produit rapidement dans le premier compteur de l’utilisateur, comme il le fait dans le monde réel. Tous les fichiers audio doivent être normalisés pour garantir une atténuation physique exacte des distances et garantir qu’un signal sonore peut être entendu quand plusieurs mètres sont éloignés (le cas échéant). Le moteur audio spatial gère l’atténuation nécessaire pour qu’un son ressemble à une distance donnée (avec une combinaison d’atténuation et de « signaux de distance ») et en appliquant une atténuation en plus de cela peut réduire l’effet. En dehors de la simulation d’un objet réel, l’atténuation de la distance initiale des sons *spatiaux* sera probablement plus que suffisante pour une combinaison correcte de votre audio.

**Détection d’objets et interfaces utilisateur**

Lorsque vous utilisez des signaux audio pour attirer l’attention de l’utilisateur au-delà de la vue actuelle, le son doit être audible et apparent dans la combinaison, bien au-dessus de tout son stéréo et tout autre son spatial qui peut gêner le signal audio directionnel. Pour les sons et la musique associés à un élément de l’interface utilisateur (par exemple, un menu), l’émetteur audio doit être attaché à cet objet. Le stéréo et autre lecture audio non positionnel peut rendre les éléments spatiaux difficiles à localiser pour les utilisateurs (voir ci-dessus : Évitez le masquage spatial).

**Utiliser le son spatial sur le son 3D standard le plus possible**

En réalité mixte, pour une expérience utilisateur optimale, les données audio 3D doivent être obtenues à l’aide de sons spatiaux plutôt que de technologies audio 3D héritées. En général, le Spatialization amélioré mérite le faible coût de l’UC par rapport au son 3D standard. L’audio 3D standard peut être utilisé pour les sons de faible priorité, les sons qui sont spatiaux mais pas nécessairement liés à un objet physique ou virtuel, et les objets que l’utilisateur n’a jamais besoin de localiser pour interagir avec l’application.

## <a name="see-also"></a>Articles associés
* [Son spatial](spatial-sound.md)
* [Mappage spatial](spatial-mapping.md)
