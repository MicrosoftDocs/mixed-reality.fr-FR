---
title: Curseurs
description: Un curseur, ou un indicateur de votre vecteur de ciblage, fournit des commentaires continus permettant à l’utilisateur de comprendre ce que HoloLens comprend pour ses intentions.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: HoloLens (1re génération), HoloLens 2, réalité mixte, curseurs, ciblage, point de regard, mouvements
ms.openlocfilehash: ef011d8400de1e23db3d6fb4b0f2a853d787ae86
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73435762"
---
# <a name="cursors"></a>Curseurs

Un curseur, ou un indicateur de votre vecteur de ciblage actuel, fournit à l’utilisateur des commentaires continus pour comprendre où le casque pense qu’il est actuellement actif. Le curseur permet à l’utilisateur de comprendre son point de ciblage actuel et agit comme un feedback pour indiquer la zone, l’hologramme ou le point qui répondra à l’entrée. Il s’agit de la représentation numérique de l’endroit où l’appareil comprend l’attention de l’utilisateur (bien que cela puisse ne pas être le même que pour déterminer quoi que ce soit sur leurs intentions).

Les commentaires fournis par le curseur permettent aux utilisateurs d’anticiper la façon dont le système répondra, utilisez ce signal comme commentaires afin de mieux communiquer leur intention à l’appareil et, en dernier lieu, soyez plus convaincu de leurs interactions.

Il existe 3 types de curseurs : **Finger, Ray**et **point-regard**. Ces curseurs de pointage fonctionnent avec différentes modalités d’entrée sur HoloLens, HoloLens 2 et les casques immersifs. Vous trouverez ci-dessous des conseils sur le type de curseur à utiliser pour chaque type de casque et de modèle d’interaction. Dans la boîte à outils de la réalité mixte (MRTK), nous avons créé des modules de curseurs de glisser-déplacer pour vous aider à créer l’expérience de pointage appropriée.


## <a name="device-support"></a>Périphériques pris en charge

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Curseur Finger</td>
        <td>❌</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
     <tr>
        <td>Curseur Ray</td>
        <td>❌</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td>Curseur en tête</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
</table>

## <a name="finger-cursor"></a>Curseur Finger
Le curseur Finger est disponible uniquement sur le HoloLens 2 pour améliorer le mode d’interaction «[manipulation directe avec mains](direct-manipulation.md)». Pour mieux comprendre où se trouve le doigt, nous avons attaché des anneaux aux conseils des deux doigts d’index. La taille de la sonnerie est basée sur la proximité du doigt par rapport à la surface de l’interface utilisateur (plus le doigt est proche de la petite sonnerie) et se réduit à une forme de point lorsque le doigt fait contact avec l’interface utilisateur. <br>

curseur ![Finger](images/finger-cursor.png)<br>
**Commentaires visuels États de Finger Cursor** 1 : l’anneau se réduit à un point. 2 : l’anneau s’aligne sur la surface. 3 : l’anneau est perpendiculaire au vecteur Finger. 4 : aucune sonnerie.

## <a name="ray-cursor"></a>Curseur Ray
Les curseurs de rayon sont attachés à la fin des rayons de pointage éloignés pour permettre la manipulation des objets qui ne sont pas en contact avec la main. Dans les casques immersifs, les rayons se déplacent des contrôleurs de mouvement et se terminent par des points-curseurs. Dans HoloLens 2, nous utilisons le modèle mental de ces rayons de contrôleur de mouvement et les rayons de main qui proviennent des palmiers et se terminent par les curseurs en forme d’anneau qui sont cohérents avec les curseurs Finger utilisés dans la manipulation directe. <br>
:::row:::
    :::column:::
        contrôleur de curseur ![Ray](images/ray-cursor-controller.png)<br>
        **Curseurs de rayon de contrôleurs de mouvement**<br>
    :::column-end:::
    :::column:::
        curseur ![Ray](images/ray-cursor-hand.png)<br>
        **Curseurs de Ray des mains**<br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="head-gaze-cursor"></a>Curseur en tête
Le curseur en tête est un point qui s’attache à la fin d’un vecteur de pointage de tête invisible qui utilise la position et la rotation de l’en-tête. Pour exécuter des actions, ce curseur de pointage est associé à diverses entrées de validation telles que le TAP-Air, les commandes vocales, le son et l’enfoncement de bouton. Dans HoloLens 2, le point de regard est le mieux associé à toute entrée de validation qui n’est pas de pression pneumatique, car il y aura un conflit d’interaction entre les rayons d’appui et de loin. <br>
:::row:::
    :::column:::
        ![la main du point d’insertion de la tête](images/head-gaze-cursor-hand.png)<br>
        **Curseur en tête avec mouvement vers la main**<br>
    :::column-end:::
    :::column:::
        ](images/head-gaze-cursor-voice.png) de la voix du curseur en tête ![<br>
        **Curseur en tête avec commande vocale**<br>
    :::column-end:::
:::row-end:::

<br>

---


## <a name="cursor-customization-recommendations"></a>Recommandations sur la personnalisation des curseurs
Si vous souhaitez personnaliser les comportements et les apparences de commentaires des curseurs, voici quelques recommandations en matière de conception :

### <a name="cursor-scale"></a>Échelle du curseur
* Le curseur ne doit pas être plus grand que les cibles disponibles, ce qui permet aux utilisateurs d’interagir facilement avec et d’afficher le contenu.
* En fonction de l’expérience que vous créez, il est également important de mettre à l’échelle le curseur à mesure que l’utilisateur regarde. Par exemple, à mesure que l’utilisateur regarde plus loin dans votre expérience, le curseur ne doit pas être trop petit pour être perdu.
* Lors de la mise à l’échelle du curseur, envisagez d’appliquer une animation douce à celle-ci lorsqu’il est mis à l’échelle pour lui attribuer une sensation organique.
* Évitez d’obstruer le contenu. Les hologrammes sont ce qui rend l’expérience mémorable et le curseur ne doit pas être pris en charge.

### <a name="directionless-cursor-shape"></a>Forme de curseur dédirectionnelle
* Bien qu’il n’y ait pas de forme de curseur droite, nous vous recommandons d’utiliser une forme sans direction comme un tore. Un curseur qui pointe dans une certaine direction (par exemple, un curseur en forme de flèche traditionnel) peut dérouter l’utilisateur pour qu’il se présente toujours de cette façon.
* Une exception est lors de l’utilisation du curseur pour communiquer des instructions d’interaction à l’utilisateur. Par exemple, lors de la mise à l’échelle d’hologrammes dans le système d’exploitation de réalité mixte, le curseur comprend temporairement des flèches qui indiquent à l’utilisateur comment déplacer sa main pour mettre l’hologramme à l’échelle.

### <a name="look-and-feel"></a>Apparence
* Un curseur en forme de bouée ou de Tore fonctionne pour de nombreuses applications.
* Choisissez une couleur et une forme qui correspond le mieux à l’expérience que vous créez.
* Les curseurs sont particulièrement sujets à la [séparation des couleurs](hologram-stability.md#color-separation).
* Un petit curseur avec une opacité équilibrée conserve l’information, sans qui prennent la hiérarchie visuelle.
* Soyez Cognizant de l’utilisation des ombres ou des surbrillances derrière votre curseur, car elles peuvent entraver le contenu et nuire à la tâche en cours.
* Les curseurs doivent s’aligner sur les surfaces de votre application et les étreinter, ce qui donne à l’utilisateur un sentiment que le système peut voir où il regarde, mais également que le système est conscient de son environnement. Par exemple, dans le système d’exploitation de la réalité mixte, le curseur s’aligne sur les surfaces du monde de l’utilisateur, ce qui crée un sentiment de conscience du monde même lorsque l’utilisateur n’est pas directement à l’hologramme.
* Le verrouillage magnétique du curseur sur un élément interactif lorsque celui-ci est proche de proximité peut contribuer à améliorer la confiance que l’utilisateur interagit avec cet élément lorsqu’il effectue une action de sélection.

### <a name="visual-cues"></a>Signaux visuels
* Si votre expérience est axée sur un seul hologramme, votre curseur doit s’aligner sur cet hologramme et changer de forme lorsque vous examinez l’hologramme. Cela peut indiquer à l’utilisateur que l’hologramme est actionnable et qu’il peut interagir avec lui.
* Si votre application utilise le mappage spatial, votre curseur peut s’aligner sur chaque surface visible. Ainsi, les utilisateurs peuvent voir que HoloLens et votre application peuvent voir leur espace. Cela renforce le fait que les hologrammes sont réels et dans notre monde et permet de combler le fossé entre les véritables et les virtuels.
* Avoir une idée de ce que le curseur doit faire lorsqu’il n’y a pas d’hologrammes ou de surfaces en vue. La placer à une distance prédéterminée devant l’utilisateur est une option.

### <a name="possible-actions"></a>Actions possibles
* Le curseur peut être représenté par différentes icônes pour indiquer les actions possibles qu’un hologramme peut effectuer, par exemple la mise à l’échelle ou la rotation.
* Ajoutez uniquement des informations supplémentaires sur le curseur si cela revient à l’utilisateur. Dans le cas contraire, les utilisateurs peuvent ne pas remarquer les modifications d’État ou être confondus par le curseur.

### <a name="input-state"></a>État d’entrée
* Nous pourrions utiliser le curseur pour afficher l’état d’entrée ou l’intention de l’utilisateur. Par exemple, nous pourrions afficher une icône indiquant à l’utilisateur que le système voit son état main et que l’application sait qu’il est prêt à agir.
* Nous pourrions également utiliser le curseur pour montrer aux utilisateurs que les commandes vocales ont été entendues par le système par le biais d’une couleur momentanée modifiable.

* Les États de curseur suivants peuvent être implémentés de différentes façons. Vous pouvez implémenter ces différents États en modélisant le curseur comme une machine à États. Exemple :
    * L’état inactif est l’endroit où vous affichez le curseur par défaut.
    * L’état prêt est lorsque vous avez détecté la main de l’utilisateur en position prête.
    * L’état d’interaction est lorsque l’utilisateur effectue une interaction particulière.
    * L’état des actions possibles ou l’état de survol est lorsque vous transmettent des actions possibles qui peuvent être effectuées sur un hologramme.

Vous pouvez également implémenter ces États en fonction de l’apparence, de sorte que vous pouvez afficher différentes ressources artistiques lorsque différents États sont détectés.

<br>

---


## <a name="going-cursor-free"></a>Passage en « sans curseur »
La conception sans curseur est recommandée lorsque le sens de l’immersion est un composant clé d’une expérience et lorsque les interactions de pointage (via le point de regard et le mouvement) ne nécessitent pas de précision. Le système doit toujours répondre aux besoins normalement atteints par un curseur en fournissant aux utilisateurs des commentaires continus sur la compréhension du système de leur pointage et en aidant les utilisateurs à communiquer en toute confiance leurs intentions au système. Cela peut être réalisable par d’autres changements d’État perceptibles.

<br>

---


## <a name="see-also"></a>Articles associés
* [Mouvements](gaze-and-commit.md#composite-gestures)
* [Pointer du regard vers l’avant et valider](gaze-and-commit.md)
