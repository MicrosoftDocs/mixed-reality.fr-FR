---
title: Mouvements
description: Les mouvements de main autoriser les utilisateurs à prendre des mesures en réalité mixte.
author: rwinj
ms.author: cmeekhof
ms.date: 02/24/2019
ms.topic: article
keywords: Réalité mixte, les gestes, interaction, conception
ms.openlocfilehash: 52ba7070e2c9b5632d5978c70571fcf9cda3f499
ms.sourcegitcommit: c20563b8195c0c374a927b96708d958b127ffc8f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974885"
---
# <a name="gestures"></a>Mouvements

Les mouvements de main autoriser les utilisateurs prendre les mesures nécessaires en réalité mixte. Interaction repose sur **les regards** à la cible et **mouvement** ou **voix** sur lequel agir quelque élément a été ciblé. Les mouvements de main ne fournissent pas un emplacement précis dans l’espace, mais la simplicité de la placer sur un HoloLens et immédiatement interagir avec du contenu permet aux utilisateurs de commencer à travailler sans tous les accessoires.

<br>

>[!VIDEO https://www.youtube.com/embed/kwn9Lh0E_vU]

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Fonctionnalité</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1er gen)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> Mouvements</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
<tr>
<td> Mains articulés</td><td></td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
</table>

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).

## <a name="gaze-and-commit"></a>Gaze-and-commit

Pour prendre des mesures, remettez l’utilisation de gestes [regards principal](gaze.md) comme mécanisme de ciblage. La combinaison de **les regards** et **appui en l’Air** mouvements des résultats dans un **regards et validation** interaction. Est une alternative à regards-validation **point-validation**, activé par [contrôleurs de mouvement](motion-controllers.md). Les applications qui s’exécutent sur HoloLens suffit prendre en charge des regards et validation dans la mesure où HoloLens ne prend pas en charge les contrôleurs de mouvement. Les applications qui s’exécutent sur HoloLens et des casques IMMERSIFS doivent prendre en charge à la fois piloté par les regards pointant tournés vers et interactions, afin de donner le choix des utilisateurs dans le périphérique d’entrée qu’ils utilisent.

## <a name="the-two-core-gestures-of-hololens"></a>Les deux principaux des mouvements de HoloLens

HoloLens reconnaît actuellement deux principaux des gestes de composant - **appui en l’Air** et **Bloom**. Ces interactions à deux cœurs sont le niveau le plus bas de données spatiales d’entrée accessibles par un développeur. Ils constituent la base pour diverses actions utilisateur.

### <a name="air-tap"></a>Appui

Appui en l’air est un mouvement appuyant avec portatifs debout, similaire à un clic de souris, ou sélectionnez. Il est utilisé dans la plupart des expériences de HoloLens pour l’équivalent d’un « clic » sur un élément d’interface utilisateur après ciblage avec [les regards](gaze.md). Il est une action universelle que vous découvrez qu’une seule fois et que vous appliquerez toutes vos applications. Autres façons d’exécuter select sont en appuyant sur le bouton unique un [HoloLens Clicker](hardware-accessories.md#hololens-clicker) ou en parlant de la voix de commande « Select ».

![État prêt pour les mouvements de main sur HoloLens](images/image9.png)<br>
*État prêt pour l’appui sur HoloLens.*

Appui en l’air est un mouvement discrète. Une sélection soit terminée ou il n’est pas, une action est ou n’est pas effectuée au sein d’une expérience. Il est possible, bien que non recommandé sans un but spécifique, pour créer des autres gestes discrètes à partir de combinaisons des principaux composants (par exemple, un mouvement de double-clic pour désigner autre chose qu’un simple clic).

![Doigt dans la position de prête, puis un mouvement cliquez ou appuyez sur](images/readyandpress.jpg)<br>
*Comment effectuer un appui : Déclencher votre doigt de l’index à la position de prête, appuyez votre doigt sur tap ou sélectionnez et sauvegarder à libérer.*

### <a name="bloom"></a>Bloom

Bloom est le mouvement « home » et est réservée pour ce seul. Il est une action système spécial qui permet de revenir en arrière dans le Menu Démarrer. Il est équivalent à la touche Windows sur un clavier ou le bouton Xbox sur une manette Xbox. L’utilisateur peut utiliser soit disponible.

![Mouvement de Bloom sur HoloLens](images/image10-640px.png)

Pour faire le mouvement de bloom sur HoloLens, maintenez la touche de votre main, palm, conjointement avec la portée de main. Ouvrez ensuite votre main. Notez que vous pouvez également toujours revenir à démarrer en disant « Hey Cortana, Go Home ». Les applications ne peut pas réagir spécifiquement pour une action de base, car celles-ci sont gérées par le système.

![Mouvement de Bloom](images/bloom-giphy.gif)<br>
*Comment effectuer le mouvement de bloom sur HoloLens.*

## <a name="composite-gestures"></a>Mouvements composite

Applications peuvent reconnaître plusieurs seulement les clics. En combinant tap, maintenez et mise en production avec le mouvement de la main, des gestes composites plus complexes peuvent être effectuées. Ces mouvements composites ou de haut niveau générer sur le plus bas niveau d’entrée des données spatiales (à partir d’appui en l’Air Bloom) que les développeurs ont accès à.

<table>
<tr>
<th> Mouvement composite</th><th> L’application</th>
</tr><tr>
<td>Appui</td><td>Le geste d’appui Air (ainsi que les autres gestes ci-dessous) réagit uniquement à un drainage spécifique. Pour détecter les autres robinets, tels que Menu ou comprendre, votre application doit utiliser directement les interactions de bas niveau décrites dans la section de mouvements de deux composants clé ci-dessus.</td>
</tr><tr>
<td>Cliquez et maintenez</td><td><p>Blocage consiste simplement à maintenir la position du doigt vers le bas de l’appui en l’air. La combinaison d’appui en l’air et hold autorise une grande variété de plus complexe &quot;cliquez et faites glisser&quot; interactions lorsqu’elles sont combinées avec arm mouvement telles que la sélection d’un objet au lieu de son activation ou &quot;mousedown&quot; interactions secondaire par exemple affichage d’un menu contextuel.</p><p>Attention doit être utilisée lors de la conception pour ce mouvement Toutefois, en tant qu’utilisateurs peut être sujette à assouplissement leurs postures disponible au cours de tout mouvement étendu.</p></td>
</tr><tr>
<td>Manipulation</td><td><p>Les mouvements de manipulation peuvent être utilisées pour déplacer, redimensionner ou faire pivoter un hologramme lorsque vous souhaitez que l’hologramme pour réagir 1:1 à l’utilisateur&#39;mouvements de main s. Une utilisation de ces mouvements 1:1 consiste à laisser l’utilisateur dessiner ou peindre dans le monde.</p><p>Le ciblage initiale pour un mouvement de manipulation doit être effectué en regards ou pointant vers. Une fois que le démarrage de maintenir, toute manipulation de l’objet est ensuite gérée manuellement mouvements, libération de l’utilisateur à rechercher pendant qu’elles manipulent.</p></td>
</tr><tr>
<td>Navigation</td><td><p>Les mouvements de navigation fonctionnent comme une manette de jeu virtuel et peuvent être utilisées pour naviguer de widgets d’interface utilisateur, tels que des menus radiales. Vous maintenez sur pour démarrer le mouvement, puis déplacez votre main dans un cube 3D normalisé, centré autour de la presse initiale. Vous pouvez déplacer votre main sur l’axe des X, Y ou Z à partir de la valeur -1 à 1, 0 étant le point de départ.</p><p>Navigation peut servir à générer basé sur la vitesse de défilement continu ou gestes de zoom, similaires à une interface utilisateur 2D de défilement en cliquant sur le bouton central de la souris puis diminué en déplaçant la souris.</p><p>Navigation avec rails désigne la capacité de reconnaissance de mouvements dans un certain axe jusqu'à ce que certain seuil est atteint sur cet axe. Cela est utile, uniquement lorsque le déplacement dans plus d’un axe est activé dans une application par le développeur, par exemple, si une application est configurée pour reconnaître des gestes de navigation entre axe des X, Y, mais également spécifiée X axe avec rails. Dans ce cas système reconnaît des mouvements de main sur axe des X tant qu’ils restent au sein d’un rails imaginaire (guide) sur l’axe, X si l’axe des Y produit également des mouvements de main.</p><p>Dans les applications 2D, les utilisateurs peuvent utiliser des gestes de navigation verticale pour faire défiler, effectuer un zoom avant ou faites glisser à l’intérieur de l’application. Cela injecte finales doigt virtuel à l’application pour simuler des entrées tactiles multipoints du même type. Les utilisateurs peuvent sélectionner ces actions ont lieu en basculant entre les outils sur la barre située au-dessus de l’application, en sélectionnant le bouton ou en indiquant que &#39; &lt;glisser/défilement/Zoom&gt; outil&#39;.</p></td>
</tr>
</table>



### <a name="gesture-recognizers"></a>Modules de reconnaissance de mouvement

L’un des avantages de l’utilisation de reconnaissance de mouvement sont que vous pouvez configurer un module de reconnaissance de mouvement uniquement pour les gestes que l’hologramme actuellement ciblée peut accepter. La plateforme effectue uniquement la levée d’ambiguïté nécessaire de distinguer ces mouvements pris en charge particuliers. De cette façon, un hologramme qui prend en charge uniquement appui peut accepter une durée prolongée entre press et de mise en production, tout en un hologramme que prend en charge à la fois tap et hold peut promouvoir le tap à une suspension après le seuil de temps d’attente.

## <a name="hand-recognition"></a>Reconnaissance de main

HoloLens reconnaît des mouvements de main en effectuant le suivi de la position d’un ou deux mains qui sont visibles à l’appareil. HoloLens voit mains lorsqu’ils sont dans un le **prêt état** (arrière de l’aiguille de face vous avec votre index) ou le **état enfoncé** (arrière main face à vous avec l’index vers le bas). Lorsque mains se trouvent dans les autres pose, le HoloLens les ignorer.

Pour chaque aiguille ce HoloLens détecte, vous pouvez accéder à sa position (sans orientation) et son état enfoncé. Lorsque le bord de l’image de mouvement arrive à la main, vous êtes également fourni avec un vecteur de direction, vous pouvez afficher à l’utilisateur afin qu’ils connaissent le déplacement de la main pour l’obtenir précédent où HoloLens peut la voir.

## <a name="gesture-frame"></a>Frame de mouvement

Pour les mouvements sur HoloLens, la main doit être dans un « mouvement cadre », dans une plage que les caméras de détection de mouvement peuvent voir correctement (très à peu près de nez de taille et entre les épaules). Les utilisateurs doivent être formés sur cette zone de la reconnaissance pour la réussite d’action et pour leur propres confort (nombre d’utilisateurs initialement supposera que le frame de mouvement doit être au sein de leur vue via HoloLens et retardez pas leurs bras uncomfortably pour interagir). Lorsque vous utilisez le HoloLens Clicker, vos mains n’avez pas besoin de se trouver dans le cadre de mouvement.

Dans le cas des gestes continues existe en particulier, des risques d’utilisateurs en déplacement ne commencent à utiliser en dehors de l’image de mouvement en mouvement intermédiaire (pendant le déplacement d’un objet HOLOGRAPHIQUE, par exemple) et la perte de leur résultat prévu.

Voici trois choses que vous devez prendre en compte :
* Éducation des utilisateurs sur le frame de mouvement existence et limites approximatifs (enseigné pendant l’installation de HoloLens).
* Avertissement aux utilisateurs lorsque leurs mouvements sont arrivent à/avec rupture les limites du cadre de mouvement dans une application, au même niveau qu’un mouvement perdu aboutira à des résultats indésirables. Des études ont montré les qualités principales d’un tel système de notification et l’interpréteur de commandes HoloLens fournit un bon exemple de ce type de notification (visuel sur le curseur central, qui indique le sens dans les limites traversée est en cours).
* Conséquences de rompre les limites de frame de mouvement doivent être réduites. En règle générale, cela signifie que le résultat d’un mouvement doit être arrêté à la limite, mais pas inversé. Par exemple, si un utilisateur déplace un objet HOLOGRAPHIQUE dans une même pièce, le déplacement doit s’arrêter lorsque le frame de mouvement est dépassé, mais **pas** affichera à nouveau le point de départ. L’utilisateur peut rencontrer certains frustration puis, mais peut comprendre plus rapidement les limites et pas obligé de redémarrer leurs actions prévues sont complète chaque fois.

## <a name="see-also"></a>Voir aussi
* [Suivre de la tête et stabiliser](gaze-and-dwell.md)
* [Conception de la voix](voice-design.md)
* [Réalité mixte - Entrées - Cours 211 : Mouvement](holograms-211.md)
* [Mouvements et contrôleurs de mouvement dans Unity](gestures-and-motion-controllers-in-unity.md)
* [Mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md)
* [Contrôleurs de mouvement](motion-controllers.md)
