---
title: Regards et validation
description: Vue d’ensemble du modèle d’entrée du pointage de regard et validation
author: caseymeekhof
ms.author: cmeekhof
ms.date: 03/31/2019
ms.topic: article
keywords: Mixte réalité, regards, regards ciblant, interaction, concevoir
ms.openlocfilehash: 7bce18853e46d71d963574b35c393e5a5dbf2cd0
ms.sourcegitcommit: 90ce9415889e7121dd2fd76a893dc3734672881b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64873972"
---
# <a name="head-gaze-and-commit"></a>Regards de tête et de validation
Regards de tête et de validation est un modèle d’entrée qui implique de cibler un objet avec la direction de votre tête pointant vers l’avant (direction de tête) et en agissant ensuite dessus avec une base de données secondaire d’entrée tels que le mouvement de la main Air appuyez sur ou la voix de commande « Select ». Il est considéré comme un modèle « beaucoup » d’entrée avec manipulation indirecte, ce qui signifie qu’il est particulièrement adapté pour l’interaction avec du contenu qui est au-delà des armes atteindre.

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
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1er gen)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
    </tr>
     <tr>
        <td>Regards de tête et de validation</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé (troisième choix - <a href="interaction-fundamentals.md">voir les autres options</a>)</td>
        <td>Option de remplacement ➕</td>
    </tr>
</table>

## <a name="head-gaze"></a>Regards de tête
Réalité mixte casques utilisent la position et l’orientation de tête de l’utilisateur pour déterminer leur vecteur de direction principal. Vous pouvez considérer cela comme une imprimante laser qui pointe directement à l’avance de directement entre les yeux de l’utilisateur. Il s’agit d’une assez grossière approximation de recherche où l’utilisateur. Votre application peut se croisent cette ray avec des objets virtuels ou réalistes et dessiner un curseur à cet emplacement pour informer l’utilisateur qu’ils sont actuellement de ciblage.

En plus des regards principal, certains casques de réalité mixte tels que la version 2 HoloLens incluent œil des systèmes qui produisent un vecteur OCULAIRE de suivi. Cela fournit une mesure précise de recherche où l’utilisateur. Il est possible de générer des regards et valider des interactions à l’aide du pointage de regard yeux, mais il est fourni avec un ensemble très différent des contraintes de conception, qui sera abordée séparément dans le [yeux article](eye-tracking.md).

## <a name="commit"></a>Validation
Après le ciblage d’un objet ou un élément d’interface utilisateur, l’utilisateur peut interagir ou « click » à l’aide d’une entrée secondaire. Il s’agit en tant que l’étape de validation du modèle. Les méthodes de validation suivantes sont prises en charge :

- Geste d’appui en l’air
- Énoncer les commandes vocales « Select » ou l’une des commandes vocales ciblé
- Appuyez sur le bouton unique un [HoloLens Clicker](hardware-accessories.md#hololens-clicker)
- Appuyez sur le bouton « A » sur un Xbox Gamepad
- Appuyez sur le bouton « A » sur un contrôleur Adaptive Xbox

### <a name="gaze-and-air-tap-gesture"></a>Mouvement d’appui regards et air
Appui en l’air est un mouvement en appuyant sur avec la main droite. Pour effectuer un appui, déclencher votre doigt de l’index à la position de prête, puis pincement avec votre curseur et déclencher votre doigt index sauvegarder à libérer. Sur 1 HoloLens, appui en l’Air est l’entrée secondaire courante.

![Doigt dans la position de prête, puis un mouvement cliquez ou appuyez sur](images/readyandpress.jpg)<br>

Appui en l’air est également disponible sur HoloLens 2, et il a été levée à partir de la version d’origine. Presque tous les types de pinches sont désormais pris en charge, tant que la main est vertical et exploitation toujours. Cela rend beaucoup plus facile pour les utilisateurs à apprendre et effectuez le geste.  Ce nouvel appui remplace l’ancien via l’API de même, pour les applications existantes obtiennent le nouveau comportement automatiquement après recompilation pour HoloLens 2.

### <a name="gaze-and-select-voice-command"></a>Utilisation et voice command « sélectionner »
Exécution des commandes vocales sont une des méthodes d’interaction principal sur la réalité mixte. Il fournit un mécanisme de « Mains libre » très puissant pour contrôler le système. Il existe autre types de modèles d’interaction vocale :

- La commande générique « Select » qui permet d’effectuer une activation de « clic » ou la validation comme une entrée secondaire.
- Commandes d’objet comme « Fermer » ou « Agrandissez-le » qui permettent de réaliser et valider dans une action en tant qu’une entrée secondaire.
- Commnads globaux tels que « Accédez à démarrer » qui ne nécessitent pas une cible.
- Interfaces utilisateur de conversation ou des entités comme Cortana qui disposent d’une capacité d’intelligence artificielle en langage naturel.
- Commnads personnalisé

Pour trouver plus d’informations et une liste de comprenhesive des commandes disponibles et l’utilisation, consultez notre [vocal conception](voice-design.md) des conseils.


### <a name="gaze-and-hololens-clicker"></a>Regards et HoloLens Clicker
Le HoloLens Clicker est le premier périphérique spécialement conçu pour HoloLens et est inclus avec l’édition de développement HoloLens 1. Le HoloLens Clicker permet à un utilisateur de cliquer avec le mouvement de la main minimal et valider en tant qu’une entrée secondaire. Le clicker HoloLens se connecte à la HoloLens 1 ou 2 à l’aide de Bluetooth faible énergie (BTLE).

![](images/hololens-clicker-500px.jpg)<br>
HoloLens Clicker

Plus d’informations et obtenir des instructions pour coupler l’appareil, vous pouvez trouver [ici](hardware-accessories.md#pairing-bluetooth-accessories)




### <a name="gaze-and-xbox-wireless-controller"></a>Regards et contrôleur sans fil Xbox
Le contrôleur sans fil Xbox permet pour exécuter une commande « clic » comme une base de données secondaire d’entrée à l’aide du bouton A. L’appareil est mappé à un ensemble par défaut des actions qui aident à naviguer et contrôler le système. Si vous souhaitez personnaliser le contrôleur, utilisez le Xbox Accesories application pour configurer votre contrôleur de sans fil Xbox.

![](images/xboxcontroller.jpg)<br>
Contrôleur sans fil Xbox

[Association d’une manette Xbox avec votre PC](hardware-accessories.md#pairing-bluetooth-accessories)


### <a name="gaze-and-xbox-adaptive-controller"></a>Contrôleur Adaptive regards et Xbox
Conçu principalement pour répondre aux besoins de joueurs à mobilité réduite, le contrôleur Adaptive Xbox est un hub unifié pour les appareils qui permet de rendre la réalité mixte plus accessible.

Le contrôleur Adaptive Xbox permet d’exécuter une commande « clic » comme une base de données secondaire d’entrée à l’aide du bouton A. L’appareil est mappé à un ensemble par défaut des actions qui aident à naviguer et contrôler le système. Si vous souhaitez personnaliser le contrôleur, utilisez le Xbox Accesories application pour configurer votre contrôleur Adaptive Xbox.

![](images/xbox-adaptive-controller-devices.jpg)<br>
Contrôleur Adaptive Xbox

Connecter des appareils externes tels que des commutateurs, des boutons, des montages et manettes de jeu pour créer une expérience personnalisée contrôleurs qui identifie de façon unique vous appartient. Les entrées de bouton, Stick analogique et déclencheur sont contrôlées avec des périphériques d’assistance connectés via les prises de 3,5 mm et ports USB.

![](images/xbox-adaptive-controller-ports.jpg)<br>
Ports de contrôleur Adaptive Xbox

[Instructions pour coupler l’appareil](hardware-accessories.md#pairing-bluetooth-accessories)

<a href=https://www.xbox.com/en-US/xbox-one/accessories/controllers/xbox-adaptive-controller>Plus d’informations sur le site Xbox</a>


# <a name="device-support"></a>Prise en charge des appareils
Utilisation de tête et validation est disponible sur tous les casques de réalité mixte. Est le modèle d’entrée principal sur HoloLens v1. En règle générale, autres casques incluent un mécanisme de pointage sur à la main, tels que les contrôleurs de mouvement ou articulée main suivi. Sur ces appareils, applications privilégier [point-validation](point-and-commit.md) pour les interactions lointain lorsque cela est possible.

Les regards yeux et de la validation est disponible sur HoloLens 2, mais n’est pas le modèle d’entrée principal. Accède à la section « Instructions de conception du pointage de regard yeux » pour une discussion sur lorsque cela peut être utile pour votre application.

# <a name="head-gaze-design-guidelines"></a>Head utilisation des règles de conception
> [!NOTE]
> Obtenir des instructions spécifiques à l’utilisation de conception [bientôt](index.md).

## <a name="gaze-targeting"></a>Ciblage des regards
Toutes les interactions reposent sur la capacité d’un utilisateur à cibler l’élément qu'ils souhaitent interagir, quelle que soit la modalité d’entrée. En réalité mixte Windows, cela s’effectue en général à l’aide regard de l’utilisateur.
Pour permettre aux utilisateurs de travailler avec une expérience avec succès, présentation de calculée du système de l’intention de l’utilisateur et l’intention de réelle de l’utilisateur, doit être alignées aussi près que possible. Dans la mesure que le système interprète les actions prévues de l’utilisateur correctement, la satisfaction des augmentations et les performances améliore.


## <a name="target-sizing-and-feedback"></a>Commentaires et dimensionnement de la cible
Le vecteur du pointage de regard a été démontré à plusieurs reprises pour être utilisable pour le ciblage précis, mais souvent convient le mieux brutes ciblage (lors de l’acquisition un tantinet supérieure cibles). Les tailles cible minimale de 1 à 1.5 degrés doivent autoriser les actions utilisateur réussie dans la plupart des scénarios, bien que les cibles de degrés 3 permettent souvent pour améliorer la vitesse. Notez que la taille que les cibles de l’utilisateur est effectivement une zone 2D même pour les éléments 3D--quelle que soit la projection est accessible sur les doit correspondre à la zone pouvant être ciblée. Fournissant certains cue marquants qu’un élément est « actif » (que l’utilisateur cible il) est extrêmement utile : il peut s’agir traitements tels que des effets visibles « pointage », mises en surbrillance audio ou clics, ou désactivez l’alignement d’un curseur avec un élément.

![Taille cible optimal à distance de compteur 2](images/gazetargeting-size-1000px.jpg)<br>
*Taille cible optimal à distance de compteur 2*

![Un exemple de mise en surbrillance d’un objet ciblé du pointage de regard](images/gazetargeting-highlighting-640px.jpg)<br>
*Un exemple de mise en surbrillance d’un objet ciblé du pointage de regard*

## <a name="target-placement"></a>Placement de la cible
Utilisateurs échouent souvent rechercher des éléments d’interface utilisateur sont positionnés très élevé ou très faible dans leur champ de vision, se concentrant la majeure partie de leur attention sur des zones autour de leur vue principale (généralement à peu près yeux). Peut aider à placer la plupart des cibles dans certaines bande raisonnable autour des yeux. Étant donné la tendance pour les utilisateurs pour vous concentrer sur une zone visual relativement réduite à tout moment (cône l’attention de vision est à peu près 10 degrés), regroupement des éléments d’interface utilisateur au degré que qu’ils sont conceptuellement associés peut exploiter le chaînage l’attention des comportements à partir de élément à un autre en tant qu’utilisateur empruntant leurs regards une zone. Lorsque vous concevez l’interface utilisateur, gardez à l’esprit les grandes variations dans le champ de vision entre HoloLens et des casques IMMERSIFS potentielles.

![Un exemple d’éléments de l’interface utilisateur groupés pour des regards plus facile de ciblage dans l’Explorateur de Galaxy](images/gazetargeting-grouping-1000px.jpg)<br>
*Un exemple d’éléments de l’interface utilisateur groupés pour des regards plus facile de ciblage dans l’Explorateur de Galaxy*

## <a name="improving-targeting-behaviors"></a>Amélioration des comportements de ciblage
Si l’intention de l’utilisateur pour cibler un élément peut être déterminée (ou approximative étroitement), il peut être très utile accepter les tentatives de « near miss » à l’interaction comme s’ils ont été correctement ciblés. Il existe un certain nombre de méthodes réussites qui peuvent être incorporées dans les expériences de réalité mixte :

### <a name="gaze-stabilization-gravity-wells"></a>Utilisation de stabilisation (« wells gravité »)
Cela doit être allumé/all de la plupart du temps. Cette technique supprime le gigues du tête/cou naturel que les utilisateurs devront peut-être. Également le déplacement en raison de comportements de recherche/parler.

### <a name="closest-link-algorithms"></a>Algorithmes de lien le plus proche
Ceux-ci fonctionnent le mieux dans les zones épars contenu interactif. S’il existe une forte probabilité que vous pouvez déterminer qu’un utilisateur a tenté d’interagir avec, vous pouvez compléter leurs capacités de ciblage par simplement en supposant que certain niveau d’objectif.

### <a name="backdatingpostdating-actions"></a>Actions postdatage/postdating
Ce mécanisme est utile dans les tâches nécessitant de vitesse. Lors du déplace d’un utilisateur via une série de manœuvres/activation ciblant à la vitesse, il peut être utile pour supposent une intention et permettre les étapes manquantes agir sur les cibles de l’utilisateur avait le focus légèrement avant ou après un appui (50 ms avant/après était en vigueur dans légèrement au début de test).

### <a name="smoothing"></a>Lissage
Ce mécanisme est utile pour les mouvements de chemins, en réduisant l’instabilité/OSCILLANT légère en raison des caractéristiques physiques mouvement de la tête. Lorsque le lissage sur les mouvements des chemins, smooth par taille/distance de mouvements plutôt qu’au fil du temps

### <a name="magnetism"></a>Magnétisme
Ce mécanisme peut être considéré comme une version plus générale d’algorithmes de « Lier le plus proche », un curseur vers une cible de dessin ou l’augmentation simplement hitboxes (qu’il soit visible ou non) que les utilisateurs s’approcher des objectifs probables, à l’aide de la disposition interactive à une certaine connaissance intention de l’utilisateur une meilleure approche. Cela peut être particulièrement efficace pour les petites cibles.

### <a name="focus-stickiness"></a>Le focus adhérence
Lorsque vous déterminez ce qui les plus proches des éléments interactifs pour donner le focus à, fournir un décalage à l’élément ayant le focus. Cela vous aidera à réduire le focus erratique commutation des comportements flottant à un point médian entre deux éléments avec bruit naturelle.


## <a name="composite-gestures"></a>Mouvements composite
Applications peuvent reconnaître plusieurs seulement les clics. En combinant tap, maintenez et mise en production avec le mouvement de la main, des gestes composites plus complexes peuvent être effectuées. Ces mouvements composites ou de haut niveau générer sur le plus bas niveau d’entrée des données spatiales (à partir d’appui en l’Air Bloom) que les développeurs ont accès à.

### <a name="air-tap"></a>Appui
Le geste d’appui Air (ainsi que les autres gestes ci-dessous) réagit uniquement à un drainage spécifique. Pour détecter les autres robinets, tels que Menu ou comprendre, votre application doit utiliser directement les interactions de bas niveau décrites dans la section de mouvements de deux composants clé ci-dessus.

### <a name="tap-and-hold"></a>Cliquez et maintenez
Blocage consiste simplement à maintenir la position du doigt vers le bas de l’appui en l’air. La combinaison d’appui en l’air et hold autorise une grande variété de « cliquez et faites glisser » des interactions plus complexes lorsqu’elles sont combinées avec déplacement arm telles que la sélection d’un objet au lieu d’activer ou de « mousedown » des interactions secondaire par exemple affichage d’un menu contextuel.
Attention doit être utilisée lors de la conception pour ce mouvement Toutefois, en tant qu’utilisateurs peut être sujette à assouplissement leurs postures disponible au cours de tout mouvement étendu.

### <a name="manipulation"></a>Manipulation
Les mouvements de manipulation peuvent servir à déplacer, redimensionner ou faire pivoter un hologramme lorsque vous souhaitez que l’hologramme pour réagir 1:1 pour les mouvements de main de l’utilisateur. Une utilisation de ces mouvements 1:1 consiste à laisser l’utilisateur dessiner ou peindre dans le monde.
Le ciblage initiale pour un mouvement de manipulation doit être effectué en regards ou pointant vers. Une fois que le démarrage de maintenir, toute manipulation de l’objet est ensuite gérée manuellement mouvements, libération de l’utilisateur à rechercher pendant qu’elles manipulent.

### <a name="navigation"></a>Navigation
Les mouvements de navigation fonctionnent comme une manette de jeu virtuel et peuvent être utilisées pour naviguer de widgets d’interface utilisateur, tels que des menus radiales. Vous maintenez sur pour démarrer le mouvement, puis déplacez votre main dans un cube 3D normalisé, centré autour de la presse initiale. Vous pouvez déplacer votre main sur l’axe des X, Y ou Z à partir de la valeur -1 à 1, 0 étant le point de départ.
Navigation peut servir à générer basé sur la vitesse de défilement continu ou gestes de zoom, similaires à une interface utilisateur 2D de défilement en cliquant sur le bouton central de la souris puis diminué en déplaçant la souris.

Navigation avec rails désigne la capacité de reconnaissance de mouvements dans un certain axe jusqu'à ce que certain seuil est atteint sur cet axe. Cela est utile, uniquement lorsque le déplacement dans plus d’un axe est activé dans une application par le développeur, par exemple, si une application est configurée pour reconnaître des gestes de navigation entre axe des X, Y, mais également spécifiée X axe avec rails. Dans ce cas système reconnaît des mouvements de main sur axe des X tant qu’ils restent au sein d’un rails imaginaire (guide) sur l’axe, X si l’axe des Y produit également des mouvements de main.

Dans les applications 2D, les utilisateurs peuvent utiliser des gestes de navigation verticale pour faire défiler, effectuer un zoom avant ou faites glisser à l’intérieur de l’application. Cela injecte finales doigt virtuel à l’application pour simuler des entrées tactiles multipoints du même type. Les utilisateurs peuvent sélectionner ces actions ont lieu en basculant entre les outils sur la barre située au-dessus de l’application, en sélectionnant le bouton ou en indiquant que '< défilement, faites glisser/Zoom > outil'.

[Plus d’informations sur les mouvements composites](gestures.md#composite-gestures)

## <a name="gesture-recognizers"></a>Modules de reconnaissance de mouvement

L’un des avantages de l’utilisation de reconnaissance de mouvement sont que vous pouvez configurer un module de reconnaissance de mouvement uniquement pour les gestes que l’hologramme actuellement ciblée peut accepter. La plateforme effectue uniquement la levée d’ambiguïté nécessaire de distinguer ces mouvements pris en charge particuliers. De cette façon, un hologramme qui prend en charge uniquement appui peut accepter une durée prolongée entre press et de mise en production, tout en un hologramme que prend en charge à la fois tap et hold peut promouvoir le tap à une suspension après le seuil de temps d’attente.

## <a name="hand-recognition"></a>Reconnaissance de main
HoloLens reconnaît des mouvements de main en effectuant le suivi de la position d’un ou deux mains qui sont visibles à l’appareil. HoloLens voit mains lorsqu’ils sont dans l’état prêt (arrière de l’aiguille de face vous avec votre index) ou l’état enfoncé (arrière main face à vous avec l’index vers le bas). Lorsque mains se trouvent dans les autres pose, le HoloLens les ignorer.
Pour chaque aiguille ce HoloLens détecte, vous pouvez accéder à sa position (sans orientation) et son état enfoncé. Lorsque le bord de l’image de mouvement arrive à la main, vous êtes également fourni avec un vecteur de direction, vous pouvez afficher à l’utilisateur afin qu’ils connaissent le déplacement de la main pour l’obtenir précédent où HoloLens peut la voir.

## <a name="gesture-frame"></a>Frame de mouvement
Pour les mouvements sur HoloLens, la main doit être dans un « mouvement cadre », dans une plage que les caméras de détection de mouvement peuvent voir correctement (très à peu près de nez de taille et entre les épaules). Les utilisateurs doivent être formés sur cette zone de la reconnaissance pour la réussite d’action et pour leur propres confort (nombre d’utilisateurs initialement supposera que le frame de mouvement doit être au sein de leur vue via HoloLens et retardez pas leurs bras uncomfortably pour interagir). Lorsque vous utilisez le HoloLens Clicker, vos mains n’avez pas besoin de se trouver dans le cadre de mouvement.

Dans le cas des gestes continues existe en particulier, des risques d’utilisateurs en déplacement ne commencent à utiliser en dehors de l’image de mouvement en mouvement intermédiaire (pendant le déplacement d’un objet HOLOGRAPHIQUE, par exemple) et la perte de leur résultat prévu.

Voici trois choses que vous devez prendre en compte :

- Éducation des utilisateurs sur le frame de mouvement existence et limites approximatifs (enseigné pendant l’installation de HoloLens).

- Avertissement aux utilisateurs lorsque leurs mouvements sont arrivent à/avec rupture les limites du cadre de mouvement dans une application, au même niveau qu’un mouvement perdu aboutira à des résultats indésirables. Des études ont montré les qualités principales d’un tel système de notification et l’interpréteur de commandes HoloLens fournit un bon exemple de ce type de notification (visuel sur le curseur central, qui indique le sens dans les limites traversée est en cours).

- Conséquences de rompre les limites de frame de mouvement doivent être réduites. En règle générale, cela signifie que le résultat d’un mouvement doit être arrêté à la limite, mais pas inversé. Par exemple, si un utilisateur déplace un objet HOLOGRAPHIQUE dans une même pièce, le déplacement doit s’arrêter lorsque le frame de mouvement est dépassé, mais ne pas être retourné au point de départ. L’utilisateur peut rencontrer certains frustration puis, mais peut comprendre plus rapidement les limites et pas obligé de redémarrer leurs actions prévues sont complète chaque fois.


## <a name="see-also"></a>Voir aussi
* [Manipulation directe](direct-manipulation.md)
* [Point et validation](point-and-commit.md)
* [Fonctionnalités de base des interactions](interaction-fundamentals.md)
* [Regards et durée d’affichage](gaze-targeting.md)
* [Regards et vocal](voice-design.md)





