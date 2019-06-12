---
title: Suivre de la tête et valider
description: Vue d’ensemble du modèle d’entrée Suivre de la tête et valider
author: caseymeekhof
ms.author: cmeekhof
ms.date: 03/31/2019
ms.topic: article
ms.localizationpriority: high
keywords: Mixed Reality, pointage du regard, ciblage avec le regard, interaction, conception
ms.openlocfilehash: d9eae3c0cfceba7c2c31425941dfce865f3aa609
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66692303"
---
# <a name="head-gaze-and-commit"></a>Suivre de la tête et valider
Le modèle Suivre de la tête et valider est un modèle d’entrée qui implique de cibler un objet avec un mouvement de votre tête pointant vers l’avant, puis d’agir dessus avec une entrée secondaire telle qu’un clic aérien manuel ou la commande vocale « Select ». Considéré comme un modèle d’entrée « de loin » avec manipulation indirecte, il est particulièrement adapté pour l’interaction avec du contenu hors de portée de main.

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
Les casques de réalité mixte utilisent la position et l’orientation de la tête de l’utilisateur pour déterminer le vecteur de direction de sa tête. Vous pouvez l’assimiler à un rayon laser qui prend son origine entre les yeux de l’utilisateur et pointe droit devant. C’est une approximation assez grossière de la zone vers laquelle se porte le regard de l’utilisateur. Votre application peut croiser ce rayon avec des objets virtuels ou réels et dessiner un curseur à cet emplacement pour indiquer à l’utilisateur ce qu’il est en train de cibler.

En plus du suivi de la tête, certains casques de réalité mixte tels que HoloLens 2 incluent des systèmes de suivi visuel qui produisent un vecteur de suivi du regard. Ces dispositifs fournissent une mesure précise de la zone vers laquelle se porte le regard de l’utilisateur. Il est possible de générer des interactions de type pointage du regard et validation avec le suivi du regard, mais cela suppose un ensemble très différent de contraintes conceptuelles qui sera abordé séparément dans l’[article consacré au suivi visuel](eye-tracking.md).

## <a name="commit"></a>Validation
Après avoir ciblé un objet ou un élément d’interface utilisateur, l’utilisateur peut interagir avec lui ou « cliquer » dessus à l’aide d’une entrée secondaire. Il s’agit de l’étape de validation du modèle. Les méthodes de validation suivantes sont prises en charge :

- Clic aérien
- Énoncer la commande vocale « Select » ou l’une des commandes vocales ciblées
- Appuyer sur le bouton unique d’un [dispositif de clic HoloLens](hardware-accessories.md#hololens-clicker)
- Appuyer sur le bouton « A » d’une manette Xbox
- Appuyer sur le bouton « A » d’une manette Xbox Adaptive Controller

### <a name="head-gaze-and-air-tap-gesture"></a>Suivi de la tête et clic aérien
Le clic aérien est une action d’appui avec la main levée. Pour effectuer un clic aérien, relevez l’index jusqu’à la position « prêt », effectuez un pincement avec votre pouce, puis relevez l’index pour libérer l’objet. Sur HoloLens 1, le clic aérien est l’entrée secondaire la plus courante.

![Doigt en position « prêt », puis mouvement de clic ou d’appui](images/readyandpress.jpg)<br>

Le clic aérien est également disponible sur HoloLens 2, et il a été assoupli par rapport à la version d’origine. Presque tous les types de pincements sont désormais pris en charge, sous réserve que la main soit verticale et immobile. Ainsi, les utilisateurs peuvent apprendre et effectuer le mouvement beaucoup plus facilement.  Comme ce nouveau clic aérien remplace l’ancien par le biais de la même API, les applications existantes bénéficient automatiquement du nouveau comportement une fois recompilées pour HoloLens 2.

### <a name="head-gaze-and-select-voice-command"></a>Suivi de la tête et commande vocale « Select »
La méthode Commander avec la voix est l’une des méthodes d’interaction principales sur Mixed Reality. Elle fournit un mécanisme « mains-libres » très puissant pour contrôler le système. Il existe différents types de modèles d’interaction vocale :

- La commande générique « Select » qui permet d’effectuer une action ou une validation avec un clic en guise d’entrée secondaire.
- Les commandes d’objet comme « Close » ou « Make it bigger » qui permettent d’effectuer et de valider une action en tant qu’entrée secondaire.
- Les commandes globales telles que « Go to start » qui ne nécessitent pas de cible.
- Les entités ou interfaces utilisateur de conversation comme Cortana qui disposent d’une fonctionnalité de langage naturel faisant appel à l’intelligence artificielle.
- Commandes personnalisées

Pour obtenir des informations supplémentaires ainsi qu’une liste complète des commandes disponibles et une description de leur utilisation, consultez notre guide sur la [méthode Commander avec la voix](voice-design.md).


### <a name="head-gaze-and-hololens-clicker"></a>Suivi de la tête et dispositif de clic HoloLens
Le dispositif de clic HoloLens est le premier périphérique spécialement conçu pour HoloLens et est inclus avec l’édition de développement HoloLens 1. Le dispositif de clic HoloLens permet à un utilisateur de cliquer avec un mouvement de la main minimal et d’effectuer une validation en tant qu’entrée secondaire. Le dispositif de clic HoloLens se connecte à HoloLens 1 ou 2 à l’aide de la technologie Bluetooth basse énergie.

![Dispositif de clic HoloLens](images/hololens-clicker-500px.jpg)<br>
*Dispositif de clic HoloLens*

Vous trouverez [ici](hardware-accessories.md#pairing-bluetooth-accessories) plus d’informations et des instructions sur le couplage de l’appareil.




### <a name="head-gaze-and-xbox-wireless-controller"></a>Suivi de la tête et manette Xbox Wireless Controller
La manette Xbox Wireless Controller permet d’effectuer une action avec un clic en tant qu’entrée secondaire à l’aide du bouton A. L’appareil est mappé à un ensemble par défaut d’actions qui aident à parcourir et à contrôler le système. Si vous souhaitez personnaliser votre manette Xbox Wireless Controller, vous pouvez la configurer à l’aide de l’application Accessoires Xbox.

![Manette Xbox Wireless Controller](images/xboxcontroller.jpg)<br>
*Manette Xbox Wireless Controller*

[Couplage d’une manette Xbox avec votre PC](hardware-accessories.md#pairing-bluetooth-accessories)


### <a name="head-gaze-and-xbox-adaptive-controller"></a>Suivi de la tête et manette Xbox Adaptive Controller
Conçu principalement pour répondre aux besoins des joueurs à mobilité réduite, la manette Xbox Adaptive Controller est un hub unifié pour les appareils qui aide à rendre Mixed Reality plus accessible.

La manette Xbox Adaptive Controller permet d’effectuer une action avec un clic en tant qu’entrée secondaire à l’aide du bouton A. L’appareil est mappé à un ensemble par défaut d’actions qui aident à parcourir et à contrôler le système. Si vous souhaitez personnaliser le contrôleur, utilisez l’application Accessoires Xbox pour configurer votre contrôleur adaptatif Xbox.

![Manette Xbox Adaptive Controller](images/xbox-adaptive-controller-devices.jpg)<br>
*Manette Xbox Adaptive Controller*

Connectez des appareils externes tels que des commutateurs, des boutons, des montages et des manettes de jeu pour créer une expérience de contrôleurs personnalisée unique. Les entrées de bouton, de joystick et de déclencheur sont contrôlées avec des appareils d’assistance connectés par le biais de prises 3,5 mm et de ports USB.

![Ports de la manette Xbox Adaptive Controller](images/xbox-adaptive-controller-ports.jpg)<br>
*Ports de la manette Xbox Adaptive Controller*

[Instructions pour coupler l’appareil](hardware-accessories.md#pairing-bluetooth-accessories)

<a href=https://www.xbox.com/en-US/xbox-one/accessories/controllers/xbox-adaptive-controller>Plus d’informations sur le site Xbox</a>


## <a name="design-guidelines"></a>Recommandations en matière de conception
> [!NOTE]
> Des conseils spécifiques à la conception de fonctionnalités de pointage du regard seront [bientôt](index.md) disponibles.

## <a name="head-gaze-targeting"></a>Ciblage avec la tête
Toutes les interactions reposent sur la capacité d’un utilisateur à cibler l’élément avec lequel il souhaite interagir, quelle que soit la modalité d’entrée. Dans Windows Mixed Reality, cette opération fait généralement appel au pointage du regard de l’utilisateur.
Pour procurer une expérience efficace à un utilisateur, il est nécessaire que la compréhension de son intention telle que la calcule le système et son intention réelle soient alignées aussi étroitement que possible. Plus le système interprète les actions prévues de l’utilisateur correctement, plus la satisfaction augmente et les performances s’améliorent.


## <a name="target-sizing-and-feedback"></a>Dimensionnement des cibles et retour
Il a été démontré à plusieurs reprises que le vecteur du pointage du regard peut être utilisé pour le ciblage précis, mais qu’il convient souvent le mieux pour le ciblage brut (acquisition de cibles un peu plus grandes). Les tailles de cible minimales de 1 à 1,5 degré doivent permettre le bon déroulement des actions utilisateur dans la plupart des scénarios, bien que des cibles de 3 degrés puissent souvent générer un gain de vitesse. Notez que la taille que cible l’utilisateur est une zone 2D même pour les éléments 3D ; la projection qui lui fait face, quelle qu’elle soit, doit être la zone pouvant être ciblée. Il est extrêmement utile de fournir à l’utilisateur des indicateurs marquants montrant qu’un élément est « actif » (qu’il est en train de le cibler) ; il peut s’agir de traitements tels que des effets de « pointage » visibles, des mises en évidence audio, des clics ou de l’alignement clair d’un curseur avec un élément.

![Taille de cible optimale à une distance de 2 mètres](images/gazetargeting-size-1000px.jpg)<br>
*Taille de cible optimale à une distance de 2 mètres*

![Exemple de mise en surbrillance d’un objet ciblé avec le regard](images/gazetargeting-highlighting-640px.jpg)<br>
*Exemple de mise en surbrillance d’un objet ciblé avec le regard*

## <a name="target-placement"></a>Placement de la cible
Les utilisateurs ne parviennent pas souvent à trouver les éléments d’interface utilisateur qui sont positionnés très haut ou très bas dans leur champ de vision, concentrant la majeure partie de leur attention sur des zones autour de leur vue principale (généralement au niveau des yeux). Le fait de placer la plupart des cibles dans une bande raisonnable autour des yeux peut s’avérer utile. Etant donné que les utilisateurs ont tendance à se concentrer sur un champ visuel relativement étroit (le cône de vision lié à l’attention est à peu près de 10 degrés), ils sont davantage susceptibles de passer d’un élément à l’autre à mesure qu’ils déplacent leur regard si les éléments d’interface utilisateur d’un même concept sont regroupés dans ce champ de vision. Quand vous concevez l’interface utilisateur, gardez à l’esprit les grandes variations potentielles du champ de vision entre les casques immersifs et HoloLens.

![Exemple d’éléments d’interface utilisateur groupés pour faciliter le ciblage avec le regard dans Galaxy Explorer](images/gazetargeting-grouping-1000px.jpg)<br>
*Exemple d’éléments d’interface utilisateur groupés pour faciliter le ciblage avec le regard dans Galaxy Explorer*

## <a name="improving-targeting-behaviors"></a>Amélioration des comportements de ciblage
Si l’intention de l’utilisateur de cibler un élément peut être déterminée (ou approchée étroitement), il peut être très utile d’accepter comme correctes les tentatives d’interaction échouant de peu. Il existe un certain nombre de méthodes utiles pouvant être incorporées dans les expériences de réalité mixte :

### <a name="head-gaze-stabilization-gravity-wells"></a>Stabilisation avec suivi de la tête (« stabilisation de la gravité »)
Cette technique doit être activée tout le temps ou la plupart du temps. Elle supprime les petits mouvements naturels de la tête ou du cou que l’utilisateur peut faire. Il en va de même des comportements liés à l’observation et à l’élocution.

### <a name="closest-link-algorithms"></a>Algorithmes du lien le plus proche
Ces derniers fonctionnent le mieux dans les zones dont le contenu interactif est clairsemé. S’il existe une forte probabilité que vous puissiez déterminer ce avec quoi un utilisateur a tenté d’interagir, vous pouvez compléter ses capacités de ciblage simplement en supposant un certain niveau d’intention.

### <a name="backdatingpostdating-actions"></a>Actions d’antidatage et de postdatage
Ce mécanisme est utile dans les tâches nécessitant de la vitesse. Quand un utilisateur effectue rapidement une série de manœuvres d’activation ou de ciblage, il peut être utile de supposer ses intentions et de l’autoriser à manquer des étapes pour lui permettre d’agir sur les cibles qu’il avait dans son champ de vision légèrement avant ou après l’appui (un écart de 50 ms avant/après s’est avéré efficace au cours des premiers tests).

### <a name="smoothing"></a>Adoucissage
Ce mécanisme est utile pour les mouvements de déplacement, réduisant les petits mouvements et les tremblements naturels de la tête. Quand vous adoucissez les mouvements de déplacement, agissez sur la taille/distance des mouvements plutôt que sur leur durée.

### <a name="magnetism"></a>Magnétisme
Ce mécanisme peut être considéré comme une version plus générale des algorithmes du « lien le plus proche » ; il consiste à déplacer un curseur vers une cible ou simplement à agrandir les zones de ciblage (visibles ou non) à mesure que l’utilisateur s’approche de cibles probables, en s’appuyant sur la disposition interactive pour mieux interpréter l’intention de l’utilisateur. Il peut être particulièrement efficace pour les petites cibles.

### <a name="focus-stickiness"></a>Adhérence du focus
Quand vous déterminez à quels éléments interactifs proches donner le focus, déportez-vous de l’élément qui a actuellement le focus. Cette approche aide à réduire les comportements erratiques liés aux changements de focus quand l’utilisateur se trouve entre deux éléments avec un bruit normal.


## <a name="composite-gestures"></a>Mouvements composites
Les applications peuvent reconnaître d’autres choses que de simples appuis. La combinaison des actions d’appui, d’appui prolongé et de libération avec le mouvement de la main permet d’effectuer des mouvements composites plus complexes. Ces mouvements composites ou de haut niveau s’appuient sur les données d’entrée spatiales de bas niveau (allant du clic aérien à l’écartement des doigts paume vers le haut) auxquelles les développeurs ont accès.

### <a name="air-tap"></a>Clic aérien
Le clic aérien (ainsi que les autres mouvements ci-dessous) réagit uniquement à un appui spécifique. Pour détecter les autres appuis, tels que l’ouverture d’un menu ou la saisie d’un objet, votre application doit utiliser directement les interactions de bas niveau décrites plus haut dans la section consacrée aux mouvements à deux composants clés.

### <a name="tap-and-hold"></a>Appui de longue durée
L’appui prolongé consiste simplement à maintenir la position du doigt vers le bas pendant le clic aérien. La combinaison du clic aérien et de l’appui prolongé autorise une grande variété d’interactions de type « clic et glissement » plus complexes quand elles sont combinées avec un déplacement du bras, telles que la sélection d’un objet au lieu de son activation, ou d’interactions secondaires de type « clic de bouton de la souris », telles que l’affichage d’un menu contextuel.
Toutefois, vous devez faire preuve de vigilance lors de la conception de ce mouvement, car l’utilisateur peut être sujet à relâcher ses postures de la main pendant un mouvement étendu.

### <a name="manipulation"></a>Manipulation
Les mouvements de manipulation peuvent servir à déplacer, redimensionner ou faire pivoter un hologramme quand vous voulez qu’il obéisse exactement aux mouvements de la main de l’utilisateur. La possibilité pour l’utilisateur de dessiner ou de peindre dans le monde illustre l’utilisation de ce type de mouvement.
Le ciblage initial pour un mouvement de manipulation doit être effectué au moyen d’un pointage du regard ou d’un pointage. Dès que l’appui de longue durée commence, toute manipulation de l’objet est gérée par les mouvements de la main, l’utilisateur pouvant alors déplacer son regard pendant qu’il effectue ses manipulations.

### <a name="navigation"></a>Navigation
Les mouvements de navigation fonctionnent comme une manette de jeu virtuelle et peuvent être utilisés pour parcourir des widgets d’interface utilisateur, tels que des menus circulaires. Vous appuyez longuement pour démarrer le mouvement, puis déplacez votre main dans un cube 3D normalisé, centré sur l’appui initial. Vous pouvez déplacer votre main sur l’axe des X, Y ou Z à partir d’une valeur comprise entre -1 et 1, 0 étant le point de départ.
La navigation peut servir à générer des mouvements de zoom ou de défilement continus basés sur la vitesse, à l’image du défilement d’une interface utilisateur 2D que vous pouvez obtenir en cliquant sur le bouton central de la souris, puis en déplaçant le pointeur de la souris vers le haut ou le bas.

La navigation avec rails désigne la possibilité de reconnaître les mouvements dans un certain axe jusqu’à ce qu’un seuil donné soit atteint sur cet axe. Cela n’est utile que si le développeur d’une application active le déplacement dans plus d’un axe ; c’est, par exemple, le cas si l’application est configurée pour reconnaître des mouvements de navigation sur l’axe des X et Y, mais qu’elle spécifie également l’axe X avec des rails. Dans ce cas, le système reconnaît les mouvements de la main sur l’axe des X tant qu’ils restent à l’intérieur de rails imaginaires (guide) sur l’axe des X, si un mouvement de la main se produit également sur l’axe des Y.

Dans les applications 2D, l’utilisateur peut se servir de mouvements de navigation verticaux pour faire défiler l’écran, effectuer un zoom ou faire glisser un élément à l’intérieur de l’application. Des interactions tactiles virtuelles sont ainsi injectées dans l’application pour simuler des mouvements tactiles du même type. L’utilisateur peut sélectionner l’action à effectuer en basculant d’un outil à l’autre dans la barre située au-dessus de l’application, en sélectionnant le bouton adéquat ou en disant «<Scroll/Drag/Zoom> Tool ».

[Plus d’informations sur les mouvements composites](gestures.md#composite-gestures)

## <a name="gesture-recognizers"></a>Modules de reconnaissance des mouvements

L’un des avantages de l’utilisation de la reconnaissance des mouvements est que vous pouvez configurer un module de reconnaissance des mouvements uniquement pour les mouvements que l’hologramme actuellement ciblé peut accepter. La plateforme n’effectue que la levée d’ambiguïté nécessaire pour distinguer les mouvements pris en charge concernés. De cette façon, un hologramme qui prend en charge uniquement le clic aérien peut accepter n’importe quelle durée entre l’appui et la libération, tandis qu’un hologramme qui prend en charge l’appui de longue durée peut promouvoir l’appui en appui prolongé une fois écoulée la durée d’appui définie.

## <a name="hand-recognition"></a>Reconnaissance des mouvements de la main
HoloLens reconnaît les mouvements de la main en effectuant le suivi de la position de la main, ou des mains, que l’appareil peut voir. HoloLens voit les mains quand elles sont dans l’état « prêt » (dos de la main face à vous, index dressé) ou « enfoncé » (dos de la main face à vous, index abaissé). Quand les mains sont dans d’autres poses, HoloLens les ignore.
Pour chaque main que HoloLens détecte, vous pouvez accéder à sa position (sans orientation) et à son état « enfoncé ». Quand la main s’approche du bord du cadre de mouvement, vous disposez également d’un vecteur de direction, que vous pouvez présenter à l’utilisateur afin qu’il sache comment déplacer sa main de manière à ce que HoloLens puisse la voir.

## <a name="gesture-frame"></a>Cadre de mouvement
Pour les mouvements sur HoloLens, la main doit être dans un « cadre de mouvement », dans une plage de visibilité appropriée pour les caméras de détection de mouvement (à peu près du nez à la taille et entre les épaules). Les utilisateurs doivent être formés sur cette zone de reconnaissance, à la fois pour la réussite de leurs actions et pour leur propre confort (nombre d’utilisateurs, qui supposent initialement que le cadre de mouvement doit se trouver dans la vue que leur procure HoloLens, maintiennent leurs bras levés de manière inconfortable pour effectuer les opérations d’interaction). Quand vous utilisez le dispositif de clic HoloLens, vos mains n’ont pas besoin de se trouver dans le cadre de mouvement.

Dans le cas des mouvements continus notamment, l’utilisateur risque de déplacer ses mains hors du cadre de mouvement au milieu du geste (pendant qu’il déplace un objet holographique, par exemple) et de perdre le résultat prévu.

Voici trois choses que vous devez envisager :

- Former les utilisateurs à l’existence du cadre de mouvement et aux limites approximatives (cette formation est dispensée pendant la configuration de HoloLens).

- Avertir les utilisateurs quand leurs mouvements s’approchent des limites du cadre de mouvement dans une application, ou les franchissent, au point qu’une perte de mouvement peut engendrer des résultats indésirables. Des études ont montré les qualités principales d’un tel système de notification, auquel répond le shell HoloLens avec une notification visuelle sur le curseur central, indiquant le sens dans lequel la limite est franchie.

- Réduire au minimum les conséquences d’un franchissement des limites du cadre de mouvement. En règle générale, le résultat d’un mouvement doit être arrêté à la limite, mais pas inversé. Par exemple, si un utilisateur déplace un objet holographique dans une pièce, le déplacement doit s’arrêter quand le cadre de mouvement est dépassé, mais il ne doit pas être retourné au point de départ. L’utilisateur peut alors ressentir une certaine frustration, mais peut comprendre plus rapidement les limites sans être systématiquement obligé de redémarrer les actions souhaitées dans leur intégralité.


## <a name="see-also"></a>Voir également
* [Manipulation directe avec les mains](direct-manipulation.md)
* [Pointer et valider avec les mains](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Suivre de la tête et stabiliser](gaze-and-dwell.md)
* [Commander avec la voix](voice-design.md)





