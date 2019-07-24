---
title: Mouvements
description: Les gestes manuels permettent aux utilisateurs d’agir en réalité mixte.
author: rwinj
ms.author: cmeekhof
ms.date: 02/24/2019
ms.topic: article
keywords: Réalité mixte, gestes, interaction, conception
ms.openlocfilehash: 8094caaf8a5d805606e9dac11ece56bc50122e5d
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829771"
---
# <a name="gestures"></a>Mouvements

Les gestes manuels permettent aux utilisateurs de prendre des mesures en réalité mixte. L’interaction repose sur **le point** d’arrêt et le point de vue cible et le **mouvement** ou la **voix** pour agir sur tout élément ciblé. Les gestes manuels ne fournissent pas un emplacement précis dans l’espace, mais la simplicité de mise en place d’un HoloLens et l’interaction immédiate avec le contenu permet aux utilisateurs de travailler sans aucun autre accessoire.

<br>

>[!VIDEO https://www.youtube.com/embed/kwn9Lh0E_vU]

## <a name="device-support"></a>Prise en charge des appareils

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
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Mouvements</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
     <tr>
        <td>Mains articulées</td>
        <td>❌</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

> [!NOTE]
> Plus d’instructions spécifiques à HoloLens 2 bientôt [disponible](index.md#news-and-notes).

## <a name="gaze-and-commit"></a>Point de dépointment et validation

Pour prendre des mesures, les gestes manuels utilisent le point de vue de la [tête](gaze.md) en tant que mécanisme de ciblage. La combinaison du mouvement de pointage **et du** robinet d’air entraîne une interaction de point de **suspension** **et de validation** . Une alternative au point de contrôle et à la validation est la possibilité de **pointer et de valider**, activée par les contrôleurs de [mouvement](motion-controllers.md). Les applications qui s’exécutent sur HoloLens doivent uniquement prendre en charge le point de recherche et la validation puisque HoloLens ne prend pas en charge les contrôleurs de mouvement. Les applications qui s’exécutent à la fois sur HoloLens et sur des casques immersifs doivent prendre en charge les interactions pilotées par le pointage et le pointage, afin de permettre aux utilisateurs de choisir le périphérique d’entrée qu’ils utilisent.

## <a name="the-two-core-gestures-of-hololens"></a>Les deux principaux mouvements de HoloLens

HoloLens reconnaît actuellement deux gestes de composants principaux: le robinet et **le**toucher de l' **air** . Ces deux interactions de base sont le niveau le plus bas des données d’entrée spatiale auxquelles un développeur peut accéder. Elles constituent la base d’une série d’actions utilisateur possibles.

### <a name="air-tap"></a>Clic aérien

Le robinet d’air est un geste de taraudage qui se trouve à la main, à l’instar d’un clic de souris ou d’une sélection. Cela est utilisé dans la plupart des expériences HoloLens pour l’équivalent d’un «clic» sur un élément d’interface utilisateur après avoir été ciblé avec le point de [regard](gaze.md). Il s’agit d’une action universelle que vous apprenez une fois, puis appliquez-la à toutes vos applications. Pour effectuer une sélection, vous pouvez d’autres manières d’appuyer sur le bouton unique d’un [clic](hardware-accessories.md#hololens-clicker) de l’un des clickers ou de parler de la commande vocale «Select».

![État prêt pour les gestes manuels sur HoloLens](images/image9.png)<br>
*État prêt pour le TAP Air sur HoloLens.*

Le robinet air est un geste discret. Une sélection est terminée ou n’a pas la valeur, une action est ou n’est pas prise dans une expérience. Il est toutefois possible, bien qu’il ne soit pas recommandé, de créer d’autres gestes discrets à partir de combinaisons de composants principaux (par exemple, un geste de double-clic pour signifier quelque chose d’autre qu’un simple robinet).

![Doigt à la position de prêt, puis à appuyer ou cliquer sur un mouvement](images/readyandpress.jpg)<br>
*Comment effectuer un robinet d’air: Augmentez le doigt de votre index à la position prête, appuyez sur le doigt pour appuyer ou sélectionner, puis sur effectuer la sauvegarde.*

### <a name="bloom"></a>Fleuri

Fleuri est le geste «à l’appui» et est réservé à ce seul. Il s’agit d’une action système spéciale qui est utilisée pour revenir au menu Démarrer. Cela équivaut à appuyer sur la touche Windows d’un clavier ou sur le bouton Xbox sur un contrôleur Xbox. L’utilisateur peut utiliser l’une ou l’autre main.

![Mouvement de fleurs sur HoloLens](images/image10-640px.png)

Pour effectuer le mouvement de floraison sur HoloLens, tenez-vous à la main, à l’œil, avec vos doigts ensemble. Ouvrez ensuite votre main. Notez que vous pouvez toujours revenir au début en disant «Hey Cortana, Go Accueil». Les applications ne peuvent pas réagir spécifiquement à une action d’habitation, car elles sont gérées par le système.

![Mouvement de fleurs](images/bloom-giphy.gif)<br>
*Comment effectuer le mouvement de floraison sur HoloLens.*

## <a name="composite-gestures"></a>Mouvements composites

Les applications peuvent reconnaître d’autres choses que de simples appuis. La combinaison des actions d’appui, d’appui prolongé et de libération avec le mouvement de la main permet d’effectuer des mouvements composites plus complexes. Ces mouvements composites ou de haut niveau s’appuient sur les données d’entrée spatiales de bas niveau (allant du clic aérien à l’écartement des doigts paume vers le haut) auxquelles les développeurs ont accès.

<table>
<tr>
<th> Mouvement composite</th><th> Procédure d’application</th>
</tr><tr>
<td>Clic aérien</td><td>Le clic aérien (ainsi que les autres mouvements ci-dessous) réagit uniquement à un appui spécifique. Pour détecter les autres appuis, tels que l’ouverture d’un menu ou la saisie d’un objet, votre application doit utiliser directement les interactions de bas niveau décrites plus haut dans la section consacrée aux mouvements à deux composants clés.</td>
</tr><tr>
<td>Appui de longue durée</td><td><p>L’appui prolongé consiste simplement à maintenir la position du doigt vers le bas pendant le clic aérien. La combinaison du robinet et du maintien de l’air permet d’obtenir une &quot;série d’interactions&quot; plus complexes de clics et de glissements lorsqu’il est combiné avec un mouvement ARM, par &quot;exemple&quot; en sélectionnant un objet au lieu de l’activer ou MouseDown les interactions secondaires, telles que l’émission d’un menu contextuel.</p><p>Toutefois, vous devez faire preuve de vigilance lors de la conception de ce mouvement, car l’utilisateur peut être sujet à relâcher ses postures de la main pendant un mouvement étendu.</p></td>
</tr><tr>
<td>Manipulation</td><td><p>Les mouvements de manipulation peuvent être utilisés pour déplacer, redimensionner ou faire pivoter un hologramme lorsque vous souhaitez que l’hologramme réagisse 1:1 aux mouvements de la main des utilisateurs&#39;. La possibilité pour l’utilisateur de dessiner ou de peindre dans le monde illustre l’utilisation de ce type de mouvement.</p><p>Le ciblage initial pour un mouvement de manipulation doit être effectué au moyen d’un pointage du regard ou d’un pointage. Dès que l’appui de longue durée commence, toute manipulation de l’objet est gérée par les mouvements de la main, l’utilisateur pouvant alors déplacer son regard pendant qu’il effectue ses manipulations.</p></td>
</tr><tr>
<td>Navigation</td><td><p>Les mouvements de navigation fonctionnent comme une manette de jeu virtuelle et peuvent être utilisés pour parcourir des widgets d’interface utilisateur, tels que des menus circulaires. Vous appuyez longuement pour démarrer le mouvement, puis déplacez votre main dans un cube 3D normalisé, centré sur l’appui initial. Vous pouvez déplacer votre main sur l’axe des X, Y ou Z à partir d’une valeur comprise entre -1 et 1, 0 étant le point de départ.</p><p>La navigation peut servir à générer des mouvements de zoom ou de défilement continus basés sur la vitesse, à l’image du défilement d’une interface utilisateur 2D que vous pouvez obtenir en cliquant sur le bouton central de la souris, puis en déplaçant le pointeur de la souris vers le haut ou le bas.</p><p>La navigation avec rails désigne la possibilité de reconnaître les mouvements dans un certain axe jusqu’à ce qu’un seuil donné soit atteint sur cet axe. Cela n’est utile que si le développeur d’une application active le déplacement dans plus d’un axe ; c’est, par exemple, le cas si l’application est configurée pour reconnaître des mouvements de navigation sur l’axe des X et Y, mais qu’elle spécifie également l’axe X avec des rails. Dans ce cas, le système reconnaît les mouvements de la main sur l’axe des X tant qu’ils restent à l’intérieur de rails imaginaires (guide) sur l’axe des X, si un mouvement de la main se produit également sur l’axe des Y.</p><p>Dans les applications 2D, l’utilisateur peut se servir de mouvements de navigation verticaux pour faire défiler l’écran, effectuer un zoom ou faire glisser un élément à l’intérieur de l’application. Des interactions tactiles virtuelles sont ainsi injectées dans l’application pour simuler des mouvements tactiles du même type. Les utilisateurs peuvent sélectionner les actions qui ont lieu en basculant entre les outils de la barre au-dessus de l’application, soit en sélectionnant le &#39; &lt;bouton, soit en disant&gt; l'&#39;outil défilement/glisser-déplacer/zoom.</p></td>
</tr>
</table>



### <a name="gesture-recognizers"></a>Modules de reconnaissance des mouvements

L’un des avantages de l’utilisation de la reconnaissance des mouvements est que vous pouvez configurer un module de reconnaissance des mouvements uniquement pour les mouvements que l’hologramme actuellement ciblé peut accepter. La plateforme n’effectue que la levée d’ambiguïté nécessaire pour distinguer les mouvements pris en charge concernés. De cette façon, un hologramme qui prend en charge uniquement le clic aérien peut accepter n’importe quelle durée entre l’appui et la libération, tandis qu’un hologramme qui prend en charge l’appui de longue durée peut promouvoir l’appui en appui prolongé une fois écoulée la durée d’appui définie.

## <a name="hand-recognition"></a>Reconnaissance des mouvements de la main

HoloLens reconnaît les mouvements de la main en effectuant le suivi de la position de la main, ou des mains, que l’appareil peut voir. HoloLens voit les mains lorsqu’ils sont dans l' **état prêt** (arrière-plan de la main avec un doigt d’index) ou l' **état enfoncé** (arrière de la main avec l’index). Quand les mains sont dans d’autres poses, HoloLens les ignore.

Pour chaque main que HoloLens détecte, vous pouvez accéder à sa position (sans orientation) et à son état « enfoncé ». Quand la main s’approche du bord du cadre de mouvement, vous disposez également d’un vecteur de direction, que vous pouvez présenter à l’utilisateur afin qu’il sache comment déplacer sa main de manière à ce que HoloLens puisse la voir.

## <a name="gesture-frame"></a>Cadre de mouvement

Pour les mouvements sur HoloLens, la main doit être dans un « cadre de mouvement », dans une plage de visibilité appropriée pour les caméras de détection de mouvement (à peu près du nez à la taille et entre les épaules). Les utilisateurs doivent être formés sur cette zone de reconnaissance, à la fois pour la réussite de leurs actions et pour leur propre confort (nombre d’utilisateurs, qui supposent initialement que le cadre de mouvement doit se trouver dans la vue que leur procure HoloLens, maintiennent leurs bras levés de manière inconfortable pour effectuer les opérations d’interaction). Quand vous utilisez le dispositif de clic HoloLens, vos mains n’ont pas besoin de se trouver dans le cadre de mouvement.

Dans le cas des mouvements continus notamment, l’utilisateur risque de déplacer ses mains hors du cadre de mouvement au milieu du geste (pendant qu’il déplace un objet holographique, par exemple) et de perdre le résultat prévu.

Voici trois choses que vous devez envisager :
* Former les utilisateurs à l’existence du cadre de mouvement et aux limites approximatives (cette formation est dispensée pendant la configuration de HoloLens).
* Avertir les utilisateurs quand leurs mouvements s’approchent des limites du cadre de mouvement dans une application, ou les franchissent, au point qu’une perte de mouvement peut engendrer des résultats indésirables. Des études ont montré les qualités principales d’un tel système de notification, auquel répond le shell HoloLens avec une notification visuelle sur le curseur central, indiquant le sens dans lequel la limite est franchie.
* Réduire au minimum les conséquences d’un franchissement des limites du cadre de mouvement. En règle générale, le résultat d’un mouvement doit être arrêté à la limite, mais pas inversé. Par exemple, si un utilisateur déplace un objet holographique dans une salle, le mouvement doit s’arrêter lorsque le cadre de mouvement est violé, mais **ne peut pas** être retourné au point de départ. L’utilisateur peut alors ressentir une certaine frustration, mais peut comprendre plus rapidement les limites sans être systématiquement obligé de redémarrer les actions souhaitées dans leur intégralité.

## <a name="see-also"></a>Voir aussi
* [Suivre de la tête et stabiliser](gaze-and-dwell.md)
* [Conception de la voix](voice-design.md)
* [Réalité mixte - Entrées - Cours 211 : Mouvement](holograms-211.md)
* [Mouvements et contrôleurs de mouvement dans Unity](gestures-and-motion-controllers-in-unity.md)
* [Mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md)
* [Contrôleurs de mouvement](motion-controllers.md)
