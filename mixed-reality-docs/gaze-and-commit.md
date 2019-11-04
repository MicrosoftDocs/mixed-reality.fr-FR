---
title: Point de regard et validation
description: Vue d’ensemble générale du modèle d’entrée « point d’entrée et de validation », à l’aide d’une entrée d’œil ou de tête.
author: sostel
ms.author: sostel
ms.date: 10/31/2019
ms.topic: article
keywords: La réalité mixte, le point de présence, le regard, l’interaction, la conception, le suivi des yeux, le suivi des têtes
ms.openlocfilehash: df152f6a3a6e4ae2d6c32a0c56fbb615bcfa7aa8
ms.sourcegitcommit: a5dc182da237f63f0487d40a2e11894027208b6c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73441124"
---
# <a name="gaze-and-commit"></a>Point de regard et validation

Le point de _regard et la validation_ est un modèle d’entrée fondamental étroitement lié à la façon dont nous interagissons avec nos ordinateurs à l’aide de la souris : _point & cliquez_.
Sur cette page, nous présentons deux types d’entrées de regard (pointer et Eye-regard) et différents types d’actions de validation. 
Le point de _regard et la validation_ sont considérés comme un modèle d’entrée lointain avec manipulation indirecte.
Cela signifie qu’il est préférable d’utiliser le contenu holographique qui est hors de portée.

Les casques de réalité mixte peuvent utiliser la position et l’orientation de la tête de l’utilisateur pour déterminer le vecteur de direction de l’en-tête. Vous pouvez l’assimiler à un rayon laser qui prend son origine entre les yeux de l’utilisateur et pointe droit devant. C’est une approximation assez grossière de la zone vers laquelle se porte le regard de l’utilisateur. Votre application peut croiser ce rayon avec des objets virtuels ou réels, et dessiner un curseur à cet emplacement pour permettre à l’utilisateur de savoir ce qu’il cible actuellement.

En plus de la tête de regard, certains casques de réalité mixte, tels que HoloLens 2, incluent des systèmes de suivi oculaire qui produisent un vecteur point-Orient. Ces dispositifs fournissent une mesure précise de la zone vers laquelle se porte le regard de l’utilisateur. Dans les deux cas, le point de regard représente un signal important pour l’intention de l’utilisateur. Mieux le système peut interpréter et prédire les actions prévues de l’utilisateur, l’augmentation de la satisfaction des utilisateurs et l’amélioration des performances.

Voici quelques exemples de la façon dont vous êtes un développeur de réalité mixte qui peut tirer parti de la tête ou du regard :
* Votre application peut faire une intersection avec le regard des hologrammes dans votre scène pour déterminer où l’attention de l’utilisateur est (plus précise avec le regard de l’oeil).
* Votre application peut canaliser les gestes et les presses des contrôleurs en fonction du point de regard de l’utilisateur, ce qui permet à l’utilisateur de sélectionner, d’activer, de saisir, de faire défiler ou d’interagir de manière transparente avec ses hologrammes.
* Votre application peut permettre à l’utilisateur de placer des hologrammes sur des surfaces réelles en croisant leur rayon de regard avec le maillage de mappage spatial.
* Votre application peut savoir quand l’utilisateur *ne cherche pas* dans la direction d’un objet important, ce qui peut amener votre application à donner des signaux visuels et audio pour tourner vers cet objet.

<br>


## <a name="device-support"></a>Périphériques pris en charge

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
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Suivre de la tête et valider</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé (troisième choix ; <a href="interaction-fundamentals.md">voir les autres options</a>)</td>
        <td>➕ Autre option</td>
    </tr>
         <tr>
        <td>Suivre du regard et valider</td>
        <td>❌ non disponible</td>
        <td>✔️ Recommandé (troisième choix ; <a href="interaction-fundamentals.md">voir les autres options</a>)</td>
        <td>❌ non disponible</td>
    </tr>
</table>


## <a name="gaze"></a>Pointage du regard

### <a name="eye--or-head-gaze"></a>Le regard de l’œil ou de la tête ?
Il y a plusieurs points à prendre en compte lorsque vous êtes confronté à la question de savoir si vous devez utiliser le modèle d’entrée « Eye-regard and Commit » ou « Head-Pointing and commit ». Si vous développez pour un casque immersif ou pour HoloLens (1re génération), le choix est simple : début et validation. Si vous développez pour HoloLens 2, le choix devient un peu plus difficile, c’est pourquoi il est important de comprendre les avantages et les défis inhérents à chacun d’eux.
Nous avons compilé un grand nombre de professionnels et de conversions dans le tableau ci-dessous pour contraster en tête et en regard. Ceci est loin d’être terminé et nous vous suggérons d’en apprendre davantage sur le ciblage des regards dans la réalité mixte ici :
* [Suivi oculaire sur hololens 2](eye-tracking.md): présentation générale de notre nouvelle fonctionnalité de suivi oculaire sur hololens 2, avec quelques conseils pour les développeurs. 
* [Œil-regard](eye-gaze-interaction.md): considérations de conception et recommandations lors de la planification de l’utilisation du suivi oculaire comme entrée.

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
   <tr>
        <td><strong>Regard sur les yeux</strong></td>
        <td><strong>Cible du regard</strong></td>
    </tr>
    <tr>
        <td>Expédition!</td>
        <td>Élevé</td>
    </tr>
    <tr>
        <td>Faible effort (à peine les mouvements de corps nécessaires)</td>
        <td>Peut être fatiguing-une gêne possible (par exemple, une fatigue du cou)</td>
    </tr>
    <tr>
        <td>Ne nécessite pas de curseur, mais les commentaires subtils sont recommandés</td>
        <td>Requiert l’affichage d’un curseur</td>
    </tr>
    <tr>
        <td>Aucun mouvement d’œil lisse, par exemple, non adapté au dessin</td>
        <td>Plus contrôlé et plus explicite</td>
    </tr>
    <tr>
        <td>Difficile pour les très petites cibles (par exemple, des boutons minuscules ou des liens weblink)</td>
        <td>Fidèles! Parfait !</td>
    </tr>
    <tr>
        <td>...</td>
        <td>...</td>
    </tr>
</table>

Que vous utilisiez le point de regard ou le regard de votre modèle d’entrée de point de présence et de validation, il est fourni avec différents jeux de contraintes de conception, qui seront couverts séparément dans [les Articles de](gaze-and-commit-head.md) [regard et](gaze-and-commit-eyes.md) de validation.

<br>

---

### <a name="cursor"></a>Curseur

:::row:::
    :::column:::
        Pour le point de vue de la tête, la plupart des applications doivent utiliser un [curseur](cursors.md) (ou une autre indication d’audit/visuel) pour donner à l’utilisateur la certitude de ce qu’ils sont sur le point d’interagir. En règle générale, vous positionnez ce curseur dans le monde où le rayon de regard de son en-tête croise d’abord un objet, qui peut être un hologramme ou une surface réaliste.<br>
        <br>
        Pour les yeux oculaires, nous vous recommandons généralement de *ne pas* afficher de curseur, car cela peut rapidement devenir gênant et ennuyeux pour l’utilisateur. À la place, mettez en surbrillance les cibles visuelles ou utilisez un curseur très pâle pour faire confiance à ce que l’utilisateur est sur le point d’interagir. Pour plus d’informations, consultez notre [Guide de conception pour une entrée basée](eye-tracking.md) sur l’œil sur HoloLens 2.
    :::column-end:::
        :::column:::
       ![un exemple de curseur visuel pour afficher le regard](images/cursor.jpg)<br>
       *Image : un exemple de curseur visuel pour afficher le regard*
    :::column-end:::
:::row-end:::

<br>

---

## <a name="commit"></a>Validation
Après avoir parlé des différentes façons de pointer vers une cible, nous _allons en parler_ plus sur la partie _validation_ dans le point de vue _et la validation_.
Après avoir ciblé un objet ou un élément d’interface utilisateur, l’utilisateur peut interagir ou cliquer dessus à l’aide d’une entrée secondaire. C’est ce que l’on appelle l’étape de validation du modèle d’entrée. 

Les méthodes de validation suivantes sont prises en charge :
- Mouvement d’appui sur la main (par exemple, augmentez votre main en avant et regroupez le doigt et le curseur de votre index)
- Dites _« Sélectionner »_ ou l’une des commandes vocales ciblées
- Appuyer sur un bouton unique sur un [Clicker HoloLens](hardware-accessories.md#hololens-clicker)
- Appuyez sur le bouton « A » sur un boîtier de manette Xbox
- Appuyez sur le bouton « A » sur un contrôleur d’adaptateur Xbox

### <a name="gaze-and-air-tap-gesture"></a>Mouvement du toucher et de l’air
Le clic aérien est une action d’appui avec la main levée. Pour effectuer un TAP Air, soulevez le doigt de votre index jusqu’à la position prête, puis pincez-le avec votre curseur et augmentez la sauvegarde du doigt de l’index jusqu’à la version finale. Sur HoloLens (1ère génération), le robinet air est l’entrée secondaire la plus courante.


:::row:::
    :::column:::
       ![doigt en position prête](images/readyandpress-ready.jpg)<br>
       **Doigt en position prête**<br>
    :::column-end:::
    :::column:::
       ![Appuyez sur le doigt pour appuyer ou sur](images/readyandpress-press.jpg)<br>
        **Appuyez sur le doigt pour appuyer ou sur**<br>
    :::column-end:::
:::row-end:::


Le TAP Air est également disponible sur HoloLens 2. Elle a été allégée de la version d’origine. Presque tous les types de pincements sont maintenant pris en charge tant que la main est debout et qu’elles sont conservées. Ainsi, les utilisateurs peuvent apprendre et effectuer le mouvement beaucoup plus facilement. Ce nouveau robinet d’air remplace l’ancien par la même API. par conséquent, les applications existantes auront le nouveau comportement automatiquement après la recompilation pour HoloLens 2.

<br>

---

### <a name="gaze-and-select-voice-command"></a>Commande vocale en regard de « sélectionner »
Les commandes vocales sont l’une des principales méthodes d’interaction dans la réalité mixte. Il fournit un mécanisme pratique et gratuit pour contrôler le système. Il existe différents types de modèles d’interactions vocales :

- Commande « SELECT » générique qui effectue une activation de clic ou une validation en tant qu’entrée secondaire.
- Les commandes d’objet (par exemple, « fermer » ou « agrandir ») effectuent et valident une action en tant qu’entrée secondaire.
- Les commandes globales (par exemple, « atteindre le début ») ne nécessitent pas de cible.
- Les interfaces utilisateur ou les entités de conversation comme Cortana disposent d’une fonctionnalité de langage naturel AI.
- Commandes vocales personnalisées

Pour obtenir plus de détails, ainsi qu’une liste complète des commandes vocales disponibles et comment les utiliser, consultez notre guide de [commande vocale](voice-design.md) .

<br>

---


### <a name="gaze-and-hololens-clicker"></a>Clic de la même façon

:::row:::
    :::column:::
        L’interutilisateur HoloLens est le premier périphérique périphérique créé spécifiquement pour HoloLens. Elle est incluse dans la version développement de HoloLens (1re génération). L’utilisateur de l’un des clickers HoloLens permet à un utilisateur de cliquer avec un mouvement de main minimal et de valider comme entrée secondaire. L’utilisateur de l’un des clickers HoloLens se connecte à HoloLens (1re génération) ou à HoloLens 2 à l’aide de la BTLE (Bluetooth Low Energy).<br>
        <br>
        [Plus d’informations et d’instructions pour coupler l’appareil](hardware-accessories.md#pairing-bluetooth-accessories)<br>
        <br>
        *Image : Clicker de HoloLens*
    :::column-end:::
        :::column:::
       ![Clicker de HoloLens](images/hololens-clicker-500px.jpg)<br>
    :::column-end:::
:::row-end:::

<br>

---


### <a name="gaze-and-xbox-wireless-controller"></a>Contrôleur de réseau sans fil en regard

:::row:::
    :::column:::
        Le contrôleur Xbox Wireless effectue une activation de clic comme entrée secondaire à l’aide du bouton « A ». L’appareil est mappé à un ensemble d’actions par défaut qui facilitent la navigation et le contrôle du système. Si vous souhaitez personnaliser le contrôleur, utilisez l’application Accessoires Xbox pour configurer votre contrôleur Xbox Wireless.<br>
        <br>
        [Comment associer un contrôleur Xbox à votre PC](hardware-accessories.md#pairing-bluetooth-accessories)<br>
        <br>
        *Image : contrôleur sans fil Xbox*
    :::column-end:::
        :::column:::
       ![Contrôleur Xbox Wireless](images/xboxcontroller.jpg)<br>
    :::column-end:::
:::row-end:::



<br>

---


### <a name="gaze-and-xbox-adaptive-controller"></a>Contrôleur adaptatif du point de regard et de Xbox
Conçu principalement pour répondre aux besoins des joueurs avec une mobilité limitée, le contrôleur d’adaptateur Xbox est un concentrateur unifié pour les appareils qui permet de rendre la réalité mixte plus accessible.

Le contrôleur d’adaptateur Xbox effectue une action de clic comme entrée secondaire à l’aide du bouton « A ». L’appareil est mappé à un ensemble d’actions par défaut qui facilitent la navigation et le contrôle du système. Si vous souhaitez personnaliser le contrôleur, utilisez l’application Accessoires Xbox pour configurer votre contrôleur d’adaptateur Xbox.

![Manette Xbox Adaptive Controller](images/xbox-adaptive-controller-devices.jpg)<br>
*Manette Xbox Adaptive Controller*

Connectez des appareils externes, tels que des commutateurs, des boutons, des montages et des joysticks, afin de créer une expérience de contrôleur personnalisée unique. Les entrées de bouton, de Stick et de déclencheur sont contrôlées à l’aide d’appareils d’assistance connectés par des connecteurs 3,5 mm et des ports USB.

![Ports de la manette Xbox Adaptive Controller](images/xbox-adaptive-controller-ports.jpg)<br>
*Ports de la manette Xbox Adaptive Controller*

[Instructions pour coupler l’appareil](hardware-accessories.md#pairing-bluetooth-accessories)

<a href=https://www.xbox.com/xbox-one/accessories/controllers/xbox-adaptive-controller>Plus d’informations sur le site Xbox</a>

<br>

---

## <a name="composite-gestures"></a>Mouvements composites

### <a name="air-tap"></a>Clic aérien
Le mouvement d’appui sur l’air (ainsi que les autres mouvements ci-dessous) réagit uniquement à un TAP spécifique. Pour détecter d’autres pressions, telles que menu ou saisis, votre application doit utiliser directement les interactions de niveau inférieur décrites dans la section relative aux mouvements de composants clés ci-dessus.

### <a name="tap-and-hold"></a>Appui de longue durée
L’appui prolongé consiste simplement à maintenir la position du doigt vers le bas pendant le clic aérien. La combinaison du robinet et du maintien de l’air permet d’obtenir une série d’interactions plus complexes de type « glisser-déplacer » lorsqu’elles sont combinées à des mouvements ARM tels que la sélection d’un objet au lieu de l’activer ou des interactions secondaires MouseDown, telles que l’émission d’un menu contextuel.
Toutefois, vous devez faire preuve de vigilance lors de la conception de ce mouvement, car l’utilisateur peut être sujet à relâcher ses postures de la main pendant un mouvement étendu.

### <a name="manipulation"></a>Manipulation
Les mouvements de manipulation peuvent être utilisés pour déplacer, redimensionner ou faire pivoter un hologramme lorsque vous souhaitez que l’hologramme réagisse 1:1 aux mouvements manuels de l’utilisateur. La possibilité pour l’utilisateur de dessiner ou de peindre dans le monde illustre l’utilisation de ce type de mouvement.
Le ciblage initial pour un mouvement de manipulation doit être effectué au moyen d’un pointage du regard ou d’un pointage. Une fois le TAP et le Hold démarré, toute manipulation de l’objet est gérée par des mouvements manuels, ce qui permet à l’utilisateur d’effectuer des recherches lors de la manipulation.

### <a name="navigation"></a>Navigation
Les mouvements de navigation fonctionnent comme une manette de jeu virtuelle et peuvent être utilisés pour parcourir des widgets d’interface utilisateur, tels que des menus circulaires. Vous appuyez longuement pour démarrer le mouvement, puis déplacez votre main dans un cube 3D normalisé, centré sur l’appui initial. Vous pouvez déplacer votre main sur l’axe des X, Y ou Z à partir d’une valeur comprise entre -1 et 1, 0 étant le point de départ.
La navigation peut servir à générer des mouvements de zoom ou de défilement continus basés sur la vitesse, à l’image du défilement d’une interface utilisateur 2D que vous pouvez obtenir en cliquant sur le bouton central de la souris, puis en déplaçant le pointeur de la souris vers le haut ou le bas.

La navigation avec rails fait référence à la possibilité de reconnaître des mouvements dans certains axes jusqu’à ce qu’un certain seuil soit atteint sur cet axe. Cela est utile uniquement lorsque le déplacement dans plus d’un axe est activé dans une application par le développeur, par exemple si une application est configurée pour reconnaître les gestes de navigation sur l’axe des X, Y, mais également dans l’axe des X avec rails. Dans ce cas, le système reconnaît les mouvements de main sur l’axe des X tant qu’ils restent dans des rails imaginaires (repère) sur l’axe des X, si le mouvement des mains se produit également sur l’axe des Y.

Dans les applications 2D, l’utilisateur peut se servir de mouvements de navigation verticaux pour faire défiler l’écran, effectuer un zoom ou faire glisser un élément à l’intérieur de l’application. Des interactions tactiles virtuelles sont ainsi injectées dans l’application pour simuler des mouvements tactiles du même type. Les utilisateurs peuvent sélectionner les actions à effectuer en basculant entre les outils de la barre au-dessus de l’application, soit en sélectionnant le bouton, soit en disant « < défilement/glissement/Zoom > outil ».

[Plus d’informations sur les mouvements composites](gaze-and-commit.md#composite-gestures)

## <a name="gesture-recognizers"></a>Modules de reconnaissance des mouvements

L’un des avantages de l’utilisation de la reconnaissance des mouvements est que vous pouvez configurer un module de reconnaissance de mouvement uniquement pour les mouvements que l’hologramme actuellement ciblé peut accepter. La plateforme ne fait que lever l’ambiguïté nécessaire pour distinguer les gestes pris en charge. De cette façon, un hologramme qui prend uniquement en charge le TAP-Air peut accepter n’importe quel laps de temps entre une pression et une mise en route, tandis qu’un hologramme qui prend en charge les deux robinets peut promouvoir le robinet en attente après le seuil de temps de maintien.

## <a name="hand-recognition"></a>Reconnaissance des mouvements de la main
HoloLens reconnaît les mouvements de la main en effectuant le suivi de la position de la main, ou des mains, que l’appareil peut voir. HoloLens voit les mains quand elles sont dans l’état « prêt » (dos de la main face à vous, index dressé) ou « enfoncé » (dos de la main face à vous, index abaissé). Lorsque les mains sont dans d’autres poses, HoloLens les ignore.
Pour chaque main détectée par HoloLens, vous pouvez accéder à sa position sans orientation et à son état appuyé. Quand la main s’approche du bord du cadre de mouvement, vous disposez également d’un vecteur de direction, que vous pouvez présenter à l’utilisateur afin qu’il sache comment déplacer sa main de manière à ce que HoloLens puisse la voir.

## <a name="gesture-frame"></a>Cadre de mouvement
Pour les gestes sur HoloLens, la main doit se trouver dans un cadre de mouvement, dans une plage que les caméras de détection de mouvement peuvent voir de manière appropriée, d’un nez à l’autre et entre les épaules. Les utilisateurs doivent être formés dans ce domaine de reconnaissance pour la réussite de l’action et pour leur propre confort. Un grand nombre d’utilisateurs partent initialement du principe que le cadre de mouvement doit se trouver dans leur vue par le biais de HoloLens et que leurs bras ne sont pas plus confortables pour interagir. Lorsque vous utilisez le clicker HoloLens, il n’est pas nécessaire que les mains soient dans le cadre de mouvement.

En particulier, dans le cas de mouvements continus, il existe un risque que les utilisateurs se déplacent en dehors du cadre du geste pendant le déplacement d’un objet holographique, par exemple, et perdent leur résultat prévu.

Voici trois choses que vous devez envisager :

- Éducation de l’utilisateur sur l’existence du cadre de mouvement et les limites approximatives. Ce processus est enseigné au cours de la configuration de HoloLens.

- Notifier les utilisateurs lorsque leurs gestes approchent ou rompent les limites du cadre de mouvement au sein d’une application jusqu’à ce qu’un geste perdu aboutisse à des résultats indésirables. La recherche a montré les qualités clés d’un tel système de notification. L’interpréteur de commandes HoloLens fournit un bon exemple de ce type de notification, visuel, sur le curseur central, indiquant la direction dans laquelle le franchissement des limites est effectué.

- Réduire au minimum les conséquences d’un franchissement des limites du cadre de mouvement. En général, cela signifie que le résultat d’un mouvement doit être arrêté à la limite et non inversé. Par exemple, si un utilisateur déplace un objet holographique dans une salle, le mouvement doit s’arrêter lorsque le cadre de mouvement est violé, et n’est pas retourné au point de départ. L’utilisateur peut faire des frustrations, mais il peut comprendre plus rapidement les limites et ne pas avoir à redémarrer ses actions complètes à chaque fois.



## <a name="see-also"></a>Articles associés
* [Interaction basée sur les yeux](eye-gaze-interaction.md)
* [Suivi des yeux sur HoloLens 2](eye-tracking.md)
* [Pointer du regard et fixer](gaze-and-dwell.md)
* [Manipulation directe](direct-manipulation.md)
* [Mouvements pratiques](gaze-and-commit.md#composite-gestures)
* [Mains et validation](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Entrée vocale](voice-input.md)

