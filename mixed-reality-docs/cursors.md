---
title: Curseurs
description: Un curseur, ou indiquer votre vecteur de ciblage, fournit des commentaires en continu pour l’utilisateur à comprendre ce que comprend HoloLens sur leurs intentions.
author: thetuvix
ms.author: alexturn, thgable
ms.date: 02/24/2019
ms.topic: article
keywords: HoloLens (1er gen), 2 de HoloLens, réalité mixte, les curseurs, ciblage, regards, les mouvements
ms.openlocfilehash: cdedcaffabe0f90e7956fdb19a7b85e202fcf403
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596948"
---
# <a name="cursors"></a>Curseurs

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).


Un curseur, ou indiquer votre vecteur actuel de ciblage, fournit des commentaires en continu pour l’utilisateur à comprendre où HoloLens estime que leur focus actuel sont à ce moment-là. Le curseur permet de pointer l’utilisateur à comprendre leur ciblant actuel et agit en tant que commentaires pour indiquer quelle zone, hologramme ou point répondra à entrer. Il s’agit de la numérique représentation où l’appareil comprend l’attention des utilisateurs (même si qui ne peut pas être identique à la détermination de quoi que ce soit sur leurs intentions).

Les commentaires formulés par le curseur offre aux utilisateurs la possibilité d’anticiper la façon dont le système répond, utiliser ce signal en tant que commentaires pour mieux communiquer leur intention de l’appareil et finalement être plus confiants sur leurs interactions.

## <a name="hololens-1st-gen"></a>HoloLens (1er gen)

Ciblage du contenu sur HoloLens (1er gen) s’effectue principalement avec la [les regards](gaze.md) vecteur (un rayon contrôlé par la position et la rotation de la tête). Cela fournit un formulaire d’entrée directe pour l’utilisateur qui a besoin de peu d’enseignement. Toutefois, les utilisateurs ont des difficultés à utiliser un centre de regards de non marqué pour le ciblage précis pour un curseur garantit que les utilisateurs connaissent le point qu'actuellement cibler. 


## <a name="positioning"></a>Positionnement

En règle générale, l’indicateur doit déplacer environ un ratio de 1:1 avec un mouvement de la tête. Il existe certains cas où gain (augmentation ou une diminution des mouvements sensiblement) peut être utilisée comme un garagiste intentionnel, mais elle entraîne des problèmes pour les utilisateurs si utilisé de façon inattendue (Notez qu’il existe une petite quantité de 'lag' recommandé pour le curseur afin d’éviter des problèmes avec contenu entièrement verrouillé en affichage). Plus important encore, expériences doivent être « honnêtes » dans la représentation sous forme de position du curseur - si le lissage, magnétisme, gain, ou autres effets sont inclus, le système doit continue d’afficher le curseur partout où compréhension du système de position est avec ceux effets inclus. Le curseur est moyen du système d’indiquer à l’utilisateur qu’ils peuvent ou ne peuvent pas interagir, pas les moyen de l’utilisateur d’indiquer le système.

L’indicateur doit idéalement verrouiller en profondeur pour les éléments de l’utilisateur peut cibler plausibly. Cela peut signifier l’aire de verrouillage s’il existe certaines [mappage Spatial](spatial-mapping.md) maillage ou à la profondeur de n’importe quel éléments d’interface utilisateur « flottants », le verrouillage pour aider l’utilisateur à comprendre ce qu’ils peuvent interagir avec en temps réel.

## <a name="cursor-design-principles"></a>Principes de conception de curseur

### <a name="always-present"></a>Toujours présent
* Nous recommandons que le curseur est toujours présent.
* Si l’utilisateur ne peut pas trouver le curseur, elles sont perdues.
* Exceptions sont des instances où l’ayant un curseur fournit une expérience non optimal pour l’utilisateur. Voici un exemple : un utilisateur est chargé d’observer une vidéo. Le curseur devient indésirable à ce stade, car elle est en cours de la vidéo de tout le temps. Il s’agit d’un scénario où vous pouvez envisager de rendre le curseur visible uniquement lorsque l’utilisateur a la main indiquant un désir de prendre des mesures. Sinon, il n’est pas visible dans la vidéo.

### <a name="cursor-scale"></a>Mise à l’échelle de curseur
* Le curseur doit être ne dépassant pas les cibles disponibles, permettant aux utilisateurs d’interagir facilement avec et afficher le contenu.
* En fonction de l’expérience que vous créez, mise à l’échelle le curseur que l’utilisateur recherche est également un facteur important. Par exemple, comme l’utilisateur cherche plus loin absent dans votre expérience peut-être le curseur ne doit pas devenir trop petit telles que son perdues.
* Le curseur de l’échelle, envisagez de lui appliquer une animation de manière réversible comme il s’adapte en lui attribuant un sentiment organique.
* Évitez l’obstruction de contenu. Hologrammes sont permettent à l’expérience facile à mémoriser et le curseur ne doit pas suivre en dehors de leur.

### <a name="directionless-cursor"></a>Curseur sombre
* Bien qu’il n’y a pas une forme de curseur approprié, nous vous recommandons d’utiliser une forme sombre comme un anneau ou quelque chose d’autre. Un curseur qui pointe dans une direction (ex : un curseur en flèche traditionnel) peut induire en erreur l’utilisateur de rechercher toujours de cette façon.
* Une exception à cette règle est lorsque vous utilisez le curseur pour communiquer des instructions d’interaction à l’utilisateur. Par exemple, lors de la mise à l’échelle hologrammes dans l’interpréteur de commandes Windows HOLOGRAPHIQUE, le curseur inclut temporairement les flèches qui aident à demander à l’utilisateur comment déplacer la main à l’échelle l’hologramme.

### <a name="look-and-feel"></a>Apparence
* La forme d’un graphique en anneau ou un anneau works de curseur pour un grand nombre d’applications.
* Choisissez une couleur et une forme qui correspond le mieux à l’expérience que vous créez.
* Les curseurs sont particulièrement sujettes à [séparation des couleurs](hologram-stability.md#color-separation).
* Un petit curseur avec une opacité à charge équilibrée met constamment informatives sans domine la hiérarchie d’objets visuel.
* Être informé de l’utilisation des ombres ou les grands titres derrière votre curseur car elles peuvent entraver le contenu et l’objectif d’un point.
* Les curseurs doivent aligner sur et étreinte les surfaces dans votre application, vous obtiendrez l’utilisateur un sentiment que le système peut voir où dont ils ont besoin, mais également que le système est informé de leur environnement.
* Par exemple, dans le système d’exploitation holographique de Windows, le curseur s’aligne sur les surfaces du monde de l’utilisateur, création d’un sentiment de la connaissance du monde de même lorsque l’utilisateur n’est pas examinant directement un hologramme...
* Verrouillage magnétique le curseur sur un élément interactif lorsqu’il est au sein de proximité. Cela peut aider à améliorer la confiance que l’utilisateur interagit avec cet élément lorsqu’ils effectuent une action de sélection.

### <a name="visual-cues"></a>Signaux visuels
* Il y a beaucoup d’informations dans notre monde et nous ajoutons avec hologrammes de plus d’informations. Un curseur est un excellent moyen de communiquer à l’utilisateur, ce qui est important.
* Si votre expérience se concentre sur un hologramme unique, puis peut-être votre curseur aligne et bloquée uniquement de hologramme et modifications de la forme lorsque vous consultez en dehors de ce hologramme. Cela peut transmettre à l’utilisateur que l’hologramme est spéciale et ils peuvent interagir avec lui.
* Si votre application utilise le mappage spatial, votre curseur peut aligner et étreinte chaque surface qu'il voit. Cela donne des commentaires aux utilisateurs ce HoloLens et votre application peut voir leur espace.
* Ces éléments vous aider à renforcer le fait que hologrammes sont réel et dans notre monde. Ils permettent de combler le fossé entre réels et virtuels.
* Vous avez une idée de ce que le curseur doit faire lorsqu’il n’y aucun hologrammes ou surfaces dans la vue. En le plaçant à une distance prédéterminée devant l’utilisateur est une option.

## <a name="cursor-feedback"></a>Commentaire du curseur

Comme nous l’avons mentionné qu’il est conseillé pour que le curseur soit toujours présente, comme vous pouvez utiliser le curseur pour transmettre des bits importants d’informations.

### <a name="possible-actions"></a>Actions possibles
* Lorsque l’utilisateur est gazing à un hologramme et le curseur se trouve sur ce HOLOGRAMME, vous pouvez utiliser le curseur pour transmettre les actions possibles sur ce hologramme.
* Vous pouvez afficher une icône sur le curseur que l’utilisateur peut par exemple acheter élément ou peut-être que hologramme mises à l’échelle. Ou même quelque chose d’aussi simple que l’hologramme peut être activé par un clic sur.
* Ajouter uniquement des informations supplémentaires sur le curseur, si cela signifie que quelque chose à l’utilisateur. Sinon, les utilisateurs n’avez peut-être soit remarqué les modifications d’état ou perturbés par le curseur.

### <a name="input-state"></a>État d’entrée
* Nous pourrions utiliser le curseur pour afficher l’état d’entrée de l’utilisateur. Par exemple, nous pouvons afficher une icône indiquant si le système détecte leur état disponible à l’utilisateur. Cela indique à l’utilisateur que l’application sait que l’utilisateur est prêt à prendre des mesures.
* Nous pourrions également utiliser le curseur pour qu’un utilisateur prenant en charge qu’une commande vocale est disponible. Ou peut-être modifier la couleur du curseur momentanément à indiquer à l’utilisateur que la commande voix a été émises par le système.

Ces États de curseur différent peuvent être implémentés de différentes façons. Vous pouvez implémenter ces différents États en modélisant le curseur comme une machine à états. Exemple :
* État d’inactivité est où vous affichez le curseur par défaut.
* L’état prêt est lorsque vous avez détecté main de l’utilisateur dans la position de prête.
* État d’interaction est quand l’utilisateur effectue une interaction particulière.
* État des Actions possibles est lorsque vous indiquez des actions possibles qui peuvent être effectuées sur un hologramme.

Vous pouvez aussi implémenter ces États de manière en mesure de l’apparence de telle sorte que vous pouvez afficher les composants graphiques différents lors de la détection des différents états.

## <a name="going-cursor-free"></a>Va « curseur-libre »

Conception sans un curseur est recommandée uniquement lorsque le sens d’immersion est un composant clé d’une expérience, et les interactions qui impliquent le ciblage (par le biais du pointage de regard et mouvement) ne nécessitent pas une grande précision. Le système doit tout en respectant les exigences qui sont normalement satisfaites par un curseur cependant - offrant aux utilisateurs des commentaires en continu de compréhension du système de leurs ciblant les aidant ainsi à communiquer en toute confiance leurs intentions dans le système. Cela peut être réalisable via d’autres modifications notables d’état.

## <a name="see-also"></a>Voir aussi
* [Mouvements](gestures.md)
* [Ciblage des regards](gaze-targeting.md)
