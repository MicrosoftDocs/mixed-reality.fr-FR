---
title: Curseurs
description: Un curseur, ou un indicateur de votre vecteur de ciblage, fournit des commentaires continus permettant à l’utilisateur de comprendre ce que HoloLens comprend pour ses intentions.
author: thetuvix
ms.author: alexturn, thgable
ms.date: 02/24/2019
ms.topic: article
keywords: HoloLens (1re génération), HoloLens 2, réalité mixte, curseurs, ciblage, point de regard, mouvements
ms.openlocfilehash: cdedcaffabe0f90e7956fdb19a7b85e202fcf403
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63526216"
---
# <a name="cursors"></a>Curseurs

> [!NOTE]
> Plus d’instructions spécifiques à HoloLens 2 bientôt [disponible](index.md#news-and-notes).


Un curseur, ou un indicateur de votre vecteur de ciblage actuel, fournit des commentaires continus permettant à l’utilisateur de comprendre où HoloLens pense que son focus actuel est à ce moment-là. Le curseur permet à l’utilisateur de comprendre son point de ciblage actuel et agit comme un feedback pour indiquer la zone, l’hologramme ou le point qui répondra à l’entrée. Il s’agit de la représentation numérique de l’endroit où l’appareil comprend l’attention de l’utilisateur (bien que cela puisse ne pas être le même que pour déterminer quoi que ce soit sur leurs intentions).

Les commentaires fournis par le curseur permettent aux utilisateurs d’anticiper la façon dont le système répondra, utilisez ce signal comme commentaires afin de mieux communiquer leur intention à l’appareil et, en dernier lieu, soyez plus convaincu de leurs interactions.

## <a name="hololens-1st-gen"></a>HoloLens (1ère génération)

Le ciblage du contenu sur HoloLens (1re génération) s’effectue principalement avec le vecteur point de [regard](gaze.md) (un rayon contrôlé par la position et la rotation de l’en-tête). Cela fournit une forme d’entrée directe pour l’utilisateur qui a besoin d’une petite enseigne. Toutefois, les utilisateurs ont des difficultés à utiliser un centre de regard non marqué pour un ciblage précis afin qu’un curseur permette aux utilisateurs de connaître le point qu’ils ciblent actuellement. 


## <a name="positioning"></a>Positionnement

En général, l’indicateur doit se déplacer dans un rapport d’environ 1:1 avec le mouvement de la tête. Dans certains cas, le gain (augmentation ou réduction du mouvement est notable) peut être utilisé comme mécanicien intentionnel, mais cela risque d’entraîner des problèmes pour les utilisateurs s’ils sont utilisés de façon inattendue (Notez qu’il y a un peu de «décalage» recommandé pour le curseur afin d’éviter les problèmes avec contenu verrouillé complet). Plus important encore, l’expérience doit être «honnête» dans la représentation de la position du curseur: si le lissage, le magnétisme, le gain ou d’autres effets sont inclus, le système doit toujours afficher le curseur là où la compréhension de la position du système est, avec celles effets inclus. Le curseur est la méthode du système qui permet d’indiquer à l’utilisateur ce qu’il peut ou ne peut pas interagir, et non celui de l’utilisateur.

L’indicateur doit idéalement verrouiller en profondeur les éléments que l’utilisateur peut plausibly cibler. Cela peut signifier le verrouillage de surface s’il existe un maillage de [mappage spatial](spatial-mapping.md) ou un verrouillage à la profondeur de tous les éléments d’interface utilisateur «flottants», afin d’aider l’utilisateur à comprendre à quoi il peut interagir en temps réel.

## <a name="cursor-design-principles"></a>Principes de conception de curseur

### <a name="always-present"></a>Toujours présent
* Nous recommandons que le curseur soit toujours présent.
* Si l’utilisateur ne parvient pas à trouver le curseur, ces derniers sont perdus.
* Les exceptions sont les cas où le fait d’avoir un curseur offre une expérience non optimale pour l’utilisateur. C’est le cas, par exemple, lorsqu’un utilisateur regarde une vidéo. Le curseur devient indésirable à ce stade, car il se trouve au milieu de la vidéo tout le temps. Il s’agit d’un scénario dans lequel vous pouvez envisager de rendre le curseur visible uniquement lorsque l’utilisateur a la main pour indiquer qu’il souhaite agir. Dans le cas contraire, il n’est pas visible dans la vidéo.

### <a name="cursor-scale"></a>Échelle du curseur
* Le curseur ne doit pas être plus grand que les cibles disponibles, ce qui permet aux utilisateurs d’interagir facilement avec et d’afficher le contenu.
* En fonction de l’expérience que vous créez, il est également important de mettre à l’échelle le curseur à mesure que l’utilisateur regarde. Par exemple, à mesure que l’utilisateur regarde plus loin dans votre expérience, il est possible que le curseur ne devienne pas trop petit, ce qui est perdu.
* Lors de la mise à l’échelle du curseur, envisagez de lui appliquer une animation floue, car il évolue pour lui donner un sentiment organique.
* Évitez d’obstruer le contenu. Les hologrammes sont ce qui rend l’expérience mémorable et le curseur ne doit pas être pris en charge.

### <a name="directionless-cursor"></a>Curseur bidirectionnel
* Bien qu’il n’y ait pas de forme de curseur droite, nous vous recommandons d’utiliser une forme sans direction comme un tore ou autre chose. Un curseur qui pointe dans une certaine direction (par exemple, un curseur en forme de flèche traditionnel) peut dérouter l’utilisateur pour qu’il se présente toujours de cette façon.
* Une exception est lors de l’utilisation du curseur pour communiquer des instructions d’interaction à l’utilisateur. Par exemple, lors de la mise à l’échelle d’hologrammes dans l’interpréteur de commandes Windows holographique, le curseur comprend temporairement des flèches qui permettent d’indiquer à l’utilisateur comment déplacer sa main pour mettre l’hologramme à l’échelle.

### <a name="look-and-feel"></a>Apparence
* Un curseur en forme de bouée ou de Tore fonctionne pour de nombreuses applications.
* Choisissez une couleur et une forme qui correspond le mieux à l’expérience que vous créez.
* Les curseurs sont particulièrement sujets à la [séparation des couleurs](hologram-stability.md#color-separation).
* Un petit curseur avec une opacité équilibrée conserve l’information, sans qui prennent la hiérarchie visuelle.
* Soyez Cognizant de l’utilisation des ombres ou des surbrillances derrière votre curseur, car elles peuvent entraver le contenu et distraire de l’objectif.
* Les curseurs doivent s’aligner sur les surfaces de votre application et les étreinter, ce qui donne à l’utilisateur un sentiment que le système peut voir où il regarde, mais également que le système est conscient de son environnement.
* Par exemple, dans le système d’exploitation Windows holographique, le curseur s’aligne sur les surfaces du monde de l’utilisateur, ce qui crée un sentiment de conscience du monde même lorsque l’utilisateur n’regarde pas directement sur un hologramme.
* Verrouillage magnétique du curseur sur un élément interactif lorsqu’il se trouve à proximité. Cela peut contribuer à améliorer la confiance que l’utilisateur interagit avec cet élément lorsqu’il effectue une action de sélection.

### <a name="visual-cues"></a>Signaux visuels
* Il y a beaucoup d’informations dans notre monde et avec des hologrammes, nous ajoutons des informations supplémentaires. Un curseur est un excellent moyen de communiquer à l’utilisateur ce qui est important.
* Si votre expérience est axée sur un seul hologramme, peut-être que votre curseur s’aligne et Hugs uniquement Cet hologramme et change de forme lorsque vous regardez loin de cet hologramme. Cela peut indiquer à l’utilisateur que l’hologramme est spécial et qu’il peut interagir avec lui.
* Si votre application utilise le mappage spatial, votre curseur peut s’aligner sur chaque surface visible. Ainsi, les utilisateurs peuvent voir que HoloLens et votre application peuvent voir leur espace.
* Ces éléments permettent de renforcer le fait que les hologrammes sont réels et dans notre monde. Ils permettent de combler le fossé entre les véritables et les virtuels.
* Avoir une idée de ce que le curseur doit faire lorsqu’il n’y a pas d’hologrammes ou de surfaces en vue. La placer à une distance prédéterminée devant l’utilisateur est une option.

## <a name="cursor-feedback"></a>Commentaires sur le curseur

Comme nous l’avons mentionné, il est recommandé d’avoir le curseur toujours présent, car vous pouvez utiliser le curseur pour transmettre des informations importantes.

### <a name="possible-actions"></a>Actions possibles
* Étant donné que l’utilisateur est Gazing à un hologramme et que le curseur se trouve sur cet hologramme, vous pouvez utiliser le curseur pour acheminer les actions possibles sur cet hologramme.
* Vous pouvez afficher sur le curseur une icône qui peut, par exemple, Acheter cet élément ou mettre à l’échelle Cet hologramme. Vous pouvez également utiliser des éléments aussi simples que l’hologramme.
* Ajoutez uniquement des informations supplémentaires sur le curseur si cela revient à l’utilisateur. Dans le cas contraire, les utilisateurs peuvent ne pas remarquer les modifications d’État ou être confondus par le curseur.

### <a name="input-state"></a>État d’entrée
* Nous pourrions utiliser le curseur pour afficher l’état d’entrée de l’utilisateur. Par exemple, nous pourrions afficher une icône indiquant à l’utilisateur si le système voit son état main. Cela indique à l’utilisateur que l’application sait que l’utilisateur est prêt à agir.
* Nous pourrions également utiliser le curseur pour permettre à l’utilisateur de savoir qu’une commande vocale est disponible. Ou peut-être modifier momentanément la couleur du curseur pour indiquer à l’utilisateur que la commande vocale a été entendue par le système.

Ces différents États de curseur peuvent être implémentés de différentes façons. Vous pouvez implémenter ces différents États en modélisant le curseur comme une machine à États. Exemple :
* L’état inactif est l’endroit où vous affichez le curseur par défaut.
* L’état prêt est lorsque vous avez détecté la main de l’utilisateur en position prête.
* L’état d’interaction est lorsque l’utilisateur effectue une interaction particulière.
* L’État actions possibles est lorsque vous transmettent des actions possibles qui peuvent être effectuées sur un hologramme.

Vous pouvez également implémenter ces États en fonction de l’apparence, de sorte que vous pouvez afficher différentes ressources artistiques lorsque différents États sont détectés.

## <a name="going-cursor-free"></a>Passage en «sans curseur»

La conception sans curseur est recommandée uniquement lorsque le sens de l’immersion est un composant clé d’une expérience, et les interactions qui impliquent le ciblage (via le point de regard et le mouvement) ne nécessitent pas de précision. Le système doit toujours répondre aux besoins normalement atteints par un curseur, ce qui permet aux utilisateurs d’obtenir des commentaires continus sur la compréhension du système de leur ciblage et de les aider à communiquer leurs intentions au système en toute confiance. Cela peut être réalisable par d’autres changements d’État perceptibles.

## <a name="see-also"></a>Voir aussi
* [Mouvements](gestures.md)
* [Pointage du regard](gaze-targeting.md)
