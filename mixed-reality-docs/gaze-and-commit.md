---
title: Suivre de la tête et valider
description: Vue d’ensemble du modèle d’entrée Suivre de la tête et valider
author: caseymeekhof
ms.author: cmeekhof
ms.date: 03/31/2019
ms.topic: article
keywords: Mixed Reality, pointage du regard, ciblage avec le regard, interaction, conception
ms.openlocfilehash: aeca5ceacf5ae350aa06cb58cc68162f885f6d78
ms.sourcegitcommit: b0b1b8e1182cce93929d409706cdaa99ff24fdee
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68387680"
---
# <a name="head-gaze-and-commit"></a>Suivre de la tête et valider
Le point de regard et la validation de la tête est un modèle d’entrée qui implique le ciblage d’un objet avec la direction de la tête vers l’avant (direction de l’en-tête), puis l’action avec une entrée secondaire, telle que le robinet à main air ou la commande vocale Select. Il est considéré comme un modèle d’entrée lointain avec manipulation indirecte, ce qui signifie qu’il est préférable d’utiliser le contenu qui se trouve au-delà des bras.

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Modèle d’entrée</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Suivre de la tête et valider</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé (troisième choix ; <a href="interaction-fundamentals.md">voir les autres options</a>)</td>
        <td>➕ Autre option</td>
    </tr>
</table>

## <a name="head-gaze"></a>Suivi de la tête
Les casques de réalité mixte utilisent la position et l’orientation de la tête de l’utilisateur pour déterminer le vecteur de direction de sa tête. Vous pouvez l’assimiler à un rayon laser qui prend son origine entre les yeux de l’utilisateur et pointe droit devant. C’est une approximation assez grossière de la zone vers laquelle se porte le regard de l’utilisateur. Votre application peut croiser ce rayon avec des objets virtuels ou réels, et dessiner un curseur à cet emplacement pour permettre à l’utilisateur de savoir ce qu’il cible actuellement.

En plus du point de vue de la tête, certains casques de réalité mixte, comme HoloLens 2, incluent des systèmes de suivi oculaire qui produisent un vecteur point-Orient. Ces dispositifs fournissent une mesure précise de la zone vers laquelle se porte le regard de l’utilisateur. Il est possible de créer des interactions de point de vue et de validation à l’aide de regard oculaire. Mais cela s’accompagne d’un ensemble très différent de contraintes de conception, qui seront couvertes séparément dans l' [article de regard](eye-tracking.md).

## <a name="commit"></a>Validation
Après avoir ciblé un objet ou un élément d’interface utilisateur, l’utilisateur peut interagir ou cliquer dessus à l’aide d’une entrée secondaire. Il s’agit de l’étape de validation du modèle. Les méthodes de validation suivantes sont prises en charge :

- Mouvement d’appui sur l’air
- Parlez la commande vocale, sélectionnez, ou l’une des commandes vocales ciblées.
- Appuyer sur un bouton unique sur un [Clicker HoloLens](hardware-accessories.md#hololens-clicker)
- Appuyez sur le bouton «A» sur un boîtier de manette Xbox
- Appuyez sur le bouton «A» sur un contrôleur d’adaptateur Xbox

### <a name="head-gaze-and-air-tap-gesture"></a>Suivi de la tête et clic aérien
Le clic aérien est une action d’appui avec la main levée. Pour effectuer un TAP Air, soulevez le doigt de votre index jusqu’à la position prête, puis pincez-le avec votre curseur et augmentez la sauvegarde du doigt de l’index jusqu’à la version finale. Sur HoloLens (1ère génération), le robinet air est l’entrée secondaire la plus courante.

![Doigt en position « prêt », puis mouvement de clic ou d’appui](images/readyandpress.jpg)<br>

Le TAP Air est également disponible sur HoloLens 2. Elle a été allégée de la version d’origine. Presque tous les types de pincements sont maintenant pris en charge tant que la main est debout et qu’elles sont conservées. Ainsi, les utilisateurs peuvent apprendre et effectuer le mouvement beaucoup plus facilement. Ce nouveau robinet d’air remplace l’ancien par la même API. par conséquent, les applications existantes auront le nouveau comportement automatiquement après la recompilation pour HoloLens 2.

### <a name="head-gaze-and-select-voice-command"></a>Suivi de la tête et commande vocale « Select »
Les commandes vocales sont l’une des principales méthodes d’interaction dans la réalité mixte. Il fournit un mécanisme pratique et gratuit pour contrôler le système. Il existe différents types de modèles d’interaction vocale :

- Commande générique SELECT qui effectue une activation de clic ou une validation en tant qu’entrée secondaire.
- Les commandes d’objet telles que Close ou le rendent plus grand s’exécutent et sont validées à une action comme une entrée secondaire.
- Les commnads globaux tels que Go to Start ne nécessitent pas de cible.
- Les interfaces utilisateur ou les entités de conversation comme Cortana disposent d’une fonctionnalité de langage naturel AI.
- Commandes personnalisées

Pour obtenir plus d’informations, ainsi qu’une liste comprenhesive des commandes disponibles et comment les utiliser, consultez notre guide de [commande vocale](voice-design.md) .


### <a name="head-gaze-and-hololens-clicker"></a>Suivi de la tête et dispositif de clic HoloLens
L’interutilisateur HoloLens est le premier périphérique périphérique créé spécifiquement pour HoloLens. Elle est incluse dans la version développement de HoloLens (1re génération). L’utilisateur de l’un des clickers HoloLens permet à un utilisateur de cliquer avec un mouvement de main minimal et de valider comme entrée secondaire. L’utilisateur de l’un des clickers HoloLens se connecte à HoloLens (1re génération) ou à HoloLens 2 à l’aide de la BTLE (Bluetooth Low Energy).

![Dispositif de clic HoloLens](images/hololens-clicker-500px.jpg)<br>
*Dispositif de clic HoloLens*

Vous trouverez [ici](hardware-accessories.md#pairing-bluetooth-accessories) plus d’informations et des instructions sur le couplage de l’appareil.




### <a name="head-gaze-and-xbox-wireless-controller"></a>Suivi de la tête et manette Xbox Wireless Controller
Le contrôleur Xbox Wireless effectue une activation de clic comme entrée secondaire à l’aide du bouton «A». L’appareil est mappé à un ensemble par défaut d’actions qui aident à parcourir et à contrôler le système. Si vous souhaitez personnaliser le contrôleur, utilisez l’application Xbox accesories pour configurer votre contrôleur Xbox Wireless.

![Manette Xbox Wireless Controller](images/xboxcontroller.jpg)<br>
*Manette Xbox Wireless Controller*

[Couplage d’une manette Xbox avec votre PC](hardware-accessories.md#pairing-bluetooth-accessories)


### <a name="head-gaze-and-xbox-adaptive-controller"></a>Suivi de la tête et manette Xbox Adaptive Controller
Conçu principalement pour répondre aux besoins des joueurs avec une mobilité limitée, le contrôleur d’adaptateur Xbox est un concentrateur unifié pour les appareils qui permet de rendre la réalité mixte plus accessible.

Le contrôleur d’adaptateur Xbox effectue une action de clic comme entrée secondaire à l’aide du bouton «A». L’appareil est mappé à un ensemble d’actions par défaut qui facilitent la navigation et le contrôle du système. Si vous souhaitez personnaliser le contrôleur, utilisez l’application Xbox accesories pour configurer votre contrôleur d’adaptateur Xbox.

![Manette Xbox Adaptive Controller](images/xbox-adaptive-controller-devices.jpg)<br>
*Manette Xbox Adaptive Controller*

Connectez des appareils externes, tels que des commutateurs, des boutons, des montages et des joysticks, afin de créer une expérience de contrôleur personnalisée unique. Les entrées de bouton, de Stick et de déclencheur sont contrôlées à l’aide d’appareils d’assistance connectés par des connecteurs 3,5 mm et des ports USB.

![Ports de la manette Xbox Adaptive Controller](images/xbox-adaptive-controller-ports.jpg)<br>
*Ports de la manette Xbox Adaptive Controller*

[Instructions pour coupler l’appareil](hardware-accessories.md#pairing-bluetooth-accessories)

<a href=https://www.xbox.com/en-US/xbox-one/accessories/controllers/xbox-adaptive-controller>Plus d’informations sur le site Xbox</a>


## <a name="design-guidelines"></a>Recommandations en matière de conception
> [!NOTE]
> Des conseils spécifiques à la conception de fonctionnalités de pointage du regard seront [bientôt](index.md) disponibles.

## <a name="head-gaze-targeting"></a>Ciblage avec la tête
Toutes les interactions reposent sur la capacité d’un utilisateur à cibler l’élément avec lequel il souhaite interagir, quelle que soit la modalité d’entrée. Dans Windows Mixed Reality, cette opération fait généralement appel au pointage du regard de l’utilisateur.
Pour permettre à un utilisateur de travailler avec succès, la compréhension calculée du système de l’intention d’un utilisateur et l’intention réelle de l’utilisateur doivent s’aligner le plus fidèlement possible. Plus le système interprète les actions prévues de l’utilisateur correctement, plus la satisfaction augmente et les performances s’améliorent.


## <a name="target-sizing-and-feedback"></a>Dimensionnement des cibles et retour
Le point de regard a été affiché à plusieurs reprises pour être utilisable pour un ciblage précis, mais il fonctionne souvent mieux pour le ciblage brut, en acquérant des cibles de plus grande taille. Les tailles de cible minimales de 1 à 1,5 degrés permettent des actions utilisateur réussies dans la plupart des scénarios, bien que les cibles de 3 degrés autorisent souvent une plus grande vitesse. Notez que la taille que cible l’utilisateur est une zone 2D même pour les éléments 3D ; la projection qui lui fait face, quelle qu’elle soit, doit être la zone pouvant être ciblée. Fournir une indication importante indiquant qu’un élément est «actif» (que l’utilisateur cible) est extrêmement utile. Cela peut inclure des traitements tels que des effets de «survol» visibles, des surbrillances audio ou des clics, ou l’alignement clair d’un curseur avec un élément.

![Taille optimale de la cible à une distance de 2 mètres](images/gazetargeting-size-1000px.jpg)<br>
*Taille de cible optimale à une distance de 2 mètres*

![Exemple de mise en surbrillance d’un objet ciblé avec le regard](images/gazetargeting-highlighting-640px.jpg)<br>
*Exemple de mise en surbrillance d’un objet ciblé avec le regard*

## <a name="target-placement"></a>Placement de la cible
Souvent, les utilisateurs ne parviennent pas à trouver des éléments d’interface utilisateur qui sont positionnés très haut ou très bas dans leur champ de vision, en mettant l’accent sur les zones autour de leur objectif principal, ce qui est à peu près oculaire. Le fait de placer la plupart des cibles dans une bande raisonnable autour des yeux peut s’avérer utile. Etant donné que les utilisateurs ont tendance à se concentrer sur un champ visuel relativement étroit (le cône de vision lié à l’attention est à peu près de 10 degrés), ils sont davantage susceptibles de passer d’un élément à l’autre à mesure qu’ils déplacent leur regard si les éléments d’interface utilisateur d’un même concept sont regroupés dans ce champ de vision. Quand vous concevez l’interface utilisateur, gardez à l’esprit les grandes variations potentielles du champ de vision entre les casques immersifs et HoloLens.

![Exemple d’éléments d’interface utilisateur groupés pour faciliter le ciblage avec le regard dans Galaxy Explorer](images/gazetargeting-grouping-1000px.jpg)<br>
*Exemple d’éléments d’interface utilisateur groupés pour faciliter le ciblage avec le regard dans Galaxy Explorer*

## <a name="improving-targeting-behaviors"></a>Amélioration des comportements de ciblage
Si l’intention de l’utilisateur de cibler un événement peut être déterminée (ou approchée), il peut être très utile d’accepter des tentatives presque manquées à l’interaction comme si elles étaient ciblées correctement. Voici quelques-unes des méthodes qui peuvent être incorporées dans les expériences de réalité mixte:

### <a name="head-gaze-stabilization-gravity-wells"></a>Stabilisation avec suivi de la tête (« stabilisation de la gravité »)
Cette fonction doit être activée le plus ou la totalité du temps. Cette technique supprime les instabilités de tête et de cou naturelles que les utilisateurs peuvent avoir en mouvement en raison des comportements de recherche et de conversation.

### <a name="closest-link-algorithms"></a>Algorithmes du lien le plus proche
Ces derniers fonctionnent le mieux dans les zones dont le contenu interactif est clairsemé. S’il existe une forte probabilité que vous puissiez déterminer ce à quoi un utilisateur tente d’interagir, vous pouvez compléter ses capacités de ciblage en supposant un certain niveau d’intention.

### <a name="backdating-and-postdating-actions"></a>Actions d’postdating et de mise à jour
Ce mécanisme est utile dans les tâches nécessitant de la vitesse. Lorsqu’un utilisateur parcourt une série de manoeuvres de ciblage et d’activation à la vitesse, il est utile de prendre des mesures et d’autoriser les étapes manquées à agir sur les cibles que l’utilisateur a placées plus légèrement avant ou légèrement après le TAP (50 ms avant/après). test RLY).

### <a name="smoothing"></a>Adoucissage
Ce mécanisme est utile pour le tracé des mouvements, en réduisant les légères gigues et les tremblements dus aux caractéristiques naturelles de mouvement de la tête. En cas de lissage sur les mouvements de tracés, lisse par la taille et la distance des mouvements plutôt qu’au fil du temps.

### <a name="magnetism"></a>Magnétisme
Ce mécanisme peut être considéré comme une version plus générale des algorithmes de lien les plus proches: le fait de dessiner un curseur vers une cible ou d’augmenter simplement hitboxes, visuellement ou non, à mesure que les utilisateurs approchent les cibles probables en utilisant une connaissance de la disposition interactive pour mieux approche de l’intention de l’utilisateur. Il peut être particulièrement efficace pour les petites cibles.

### <a name="focus-stickiness"></a>Adhérence du focus
Lorsque vous déterminez les éléments interactifs proches auxquels donner le focus, l’adhérence au focus fournit un décalage à l’élément qui est actuellement concentré. Cela permet de réduire les comportements de changement de focus erratiques lorsqu’ils flottent à un point médian entre deux éléments avec un bruit naturel.


## <a name="composite-gestures"></a>Mouvements composites

### <a name="air-tap"></a>Clic aérien
Le mouvement d’appui sur l’air (ainsi que les autres mouvements ci-dessous) réagit uniquement à un TAP spécifique. Pour détecter d’autres pressions, telles que menu ou saisis, votre application doit utiliser directement les interactions de niveau inférieur décrites dans la section relative aux mouvements de composants clés ci-dessus.

### <a name="tap-and-hold"></a>Appui de longue durée
L’appui prolongé consiste simplement à maintenir la position du doigt vers le bas pendant le clic aérien. La combinaison du robinet et du maintien de l’air permet d’obtenir une série d’interactions plus complexes de type «glisser-déplacer» lorsqu’elles sont combinées à des mouvements ARM tels que la sélection d’un objet au lieu de l’activer ou des interactions secondaires MouseDown, telles que l’émission d’un menu contextuel.
Toutefois, vous devez faire preuve de vigilance lors de la conception de ce mouvement, car l’utilisateur peut être sujet à relâcher ses postures de la main pendant un mouvement étendu.

### <a name="manipulation"></a>Manipulation
Les mouvements de manipulation peuvent être utilisés pour déplacer, redimensionner ou faire pivoter un hologramme lorsque vous souhaitez que l’hologramme réagisse 1:1 aux mouvements manuels de l’utilisateur. La possibilité pour l’utilisateur de dessiner ou de peindre dans le monde illustre l’utilisation de ce type de mouvement.
Le ciblage initial pour un mouvement de manipulation doit être effectué au moyen d’un pointage du regard ou d’un pointage. Une fois le TAP et le Hold démarré, toute manipulation de l’objet est gérée par des mouvements manuels, ce qui permet à l’utilisateur d’effectuer des recherches lors de la manipulation.

### <a name="navigation"></a>Navigation
Les mouvements de navigation fonctionnent comme une manette de jeu virtuelle et peuvent être utilisés pour parcourir des widgets d’interface utilisateur, tels que des menus circulaires. Vous appuyez longuement pour démarrer le mouvement, puis déplacez votre main dans un cube 3D normalisé, centré sur l’appui initial. Vous pouvez déplacer votre main sur l’axe des X, Y ou Z à partir d’une valeur comprise entre -1 et 1, 0 étant le point de départ.
La navigation peut servir à générer des mouvements de zoom ou de défilement continus basés sur la vitesse, à l’image du défilement d’une interface utilisateur 2D que vous pouvez obtenir en cliquant sur le bouton central de la souris, puis en déplaçant le pointeur de la souris vers le haut ou le bas.

La navigation avec rails fait référence à la possibilité de reconnaître des mouvements dans certains axes jusqu’à ce qu’un certain seuil soit atteint sur cet axe. Cela est utile uniquement lorsque le déplacement dans plus d’un axe est activé dans une application par le développeur, par exemple si une application est configurée pour reconnaître les gestes de navigation sur l’axe des X, Y, mais également dans l’axe des X avec rails. Dans ce cas, le système reconnaît les mouvements de main sur l’axe des X tant qu’ils restent dans des rails imaginaires (repère) sur l’axe des X, si le mouvement des mains se produit également sur l’axe des Y.

Dans les applications 2D, l’utilisateur peut se servir de mouvements de navigation verticaux pour faire défiler l’écran, effectuer un zoom ou faire glisser un élément à l’intérieur de l’application. Des interactions tactiles virtuelles sont ainsi injectées dans l’application pour simuler des mouvements tactiles du même type. Les utilisateurs peuvent sélectionner les actions à effectuer en basculant entre les outils de la barre au-dessus de l’application, soit en sélectionnant le bouton, soit en disant «< défilement/glissement/Zoom > outil».

[Plus d’informations sur les mouvements composites](gestures.md#composite-gestures)

## <a name="gesture-recognizers"></a>Modules de reconnaissance des mouvements

L’un des avantages de l’utilisation de la reconnaissance des mouvements est que vous pouvez configurer un module de reconnaissance de mouvement uniquement pour les mouvements que l’hologramme actuellement ciblé peut accepter. La plateforme ne fait que lever l’ambiguïté nécessaire pour distinguer les gestes pris en charge. De cette façon, un hologramme qui prend uniquement en charge le TAP-Air peut accepter n’importe quel laps de temps entre une pression et une mise en route, tandis qu’un hologramme qui prend en charge les deux robinets peut promouvoir le robinet en attente après le seuil de temps de maintien.

## <a name="hand-recognition"></a>Reconnaissance des mouvements de la main
HoloLens reconnaît les mouvements de la main en effectuant le suivi de la position de la main, ou des mains, que l’appareil peut voir. HoloLens voit les mains quand elles sont dans l’état « prêt » (dos de la main face à vous, index dressé) ou « enfoncé » (dos de la main face à vous, index abaissé). Quand les mains sont dans d’autres poses, HoloLens ignore Themz.
Pour chaque main détectée par HoloLens, vous pouvez accéder à sa position sans orientation et à son état appuyé. Quand la main s’approche du bord du cadre de mouvement, vous disposez également d’un vecteur de direction, que vous pouvez présenter à l’utilisateur afin qu’il sache comment déplacer sa main de manière à ce que HoloLens puisse la voir.

## <a name="gesture-frame"></a>Cadre de mouvement
Pour les gestes sur HoloLens, la main doit se trouver dans un cadre de mouvement, dans une plage que les caméras de détection de mouvement peuvent voir de manière appropriée, d’un nez à l’autre et entre les épaules. Les utilisateurs doivent être formés dans ce domaine de reconnaissance pour la réussite de l’action et pour leur propre confort. Un grand nombre d’utilisateurs partent initialement du principe que le cadre de mouvement doit se trouver dans leur vue par le biais de HoloLens et que leurs bras ne sont pas plus confortables pour interagir. Lorsque vous utilisez le clicker HoloLens, il n’est pas nécessaire que les mains soient dans le cadre de mouvement.

En particulier, dans le cas de mouvements continus, il existe un risque que les utilisateurs se déplacent en dehors du cadre du geste pendant le déplacement d’un objet holographique, par exemple, et perdent leur résultat prévu.

Voici trois choses que vous devez envisager :

- Éducation de l’utilisateur sur l’existence du cadre de mouvement et les limites approximatives. Ce processus est enseigné au cours de la configuration de HoloLens.

- Notifier les utilisateurs lorsque leurs gestes approchent ou rompent les limites du cadre de mouvement au sein d’une application jusqu’à ce qu’un geste perdu aboutisse à des résultats indésirables. La recherche a montré les qualités clés d’un tel système de notification. L’interpréteur de commandes HoloLens fournit un bon exemple de ce type de notification, visuel, sur le curseur central, indiquant la direction dans laquelle le franchissement des limites est effectué.

- Réduire au minimum les conséquences d’un franchissement des limites du cadre de mouvement. En général, cela signifie que le résultat d’un mouvement doit être arrêté à la limite et non inversé. Par exemple, si un utilisateur déplace un objet holographique dans une salle, le mouvement doit s’arrêter lorsque le cadre de mouvement est violé, et n’est pas retourné au point de départ. L’utilisateur peut faire des frustrations, mais il peut comprendre plus rapidement les limites et ne pas avoir à redémarrer ses actions complètes à chaque fois.


## <a name="see-also"></a>Voir aussi
* [Manipulation directe avec les mains](direct-manipulation.md)
* [Pointer et valider avec les mains](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Suivre de la tête et stabiliser](gaze-and-dwell.md)
* [Commander avec la voix](voice-design.md)





