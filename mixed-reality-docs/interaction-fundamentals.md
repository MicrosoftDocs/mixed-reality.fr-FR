---
title: Notions fondamentales d’interaction
description: Comme nous avons créé des expériences sur HoloLens (1er gen), 2 de HoloLens et des casques IMMERSIFS, nous avons commencé à écrire certaines choses que nous avons trouvé utiles pour partager.
author: rwinj
ms.author: jennyk
ms.date: 02/24/2019
ms.topic: article
keywords: Mixte réalité, interaction, concevoir
ms.openlocfilehash: d594126529b6314a4706f8b6b6af856058c3280a
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593246"
---
# <a name="interaction-fundamentals"></a>Notions fondamentales d’interaction

Comme nous avons créé des expériences sur HoloLens et des casques IMMERSIFS, nous avons commencé à écrire certaines choses que nous avons trouvé utiles pour partager. Considérez-les comme des blocs de construction fondamentaux pour la conception d’interaction de réalité mixte.

## <a name="device-support"></a>Prise en charge des appareils

Voici les articles de conception Interaction disponibles et les types ou le type d’appareil qu’ils s’appliquent à.
<br>

<table>

<th>
<tr>

<td style="width:150px;"><strong>entrée</strong></td>
<td style="width:150px; text-align: center;"><a href="hololens-hardware-details.md"><strong>HoloLens (1er gen)</strong></a></td>
<td style="width:150px; text-align: center;"><strong>HoloLens 2</strong></td>
<td style="width:150px; text-align: center;"><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
</tr>
</th>
 
<tr>
<td> <a href="gestures.md">Mains articulés</a></td><td style="text-align: center;"></td><td style="text-align: center;">✔️</td><td></td>

</tr><tr>
<td> <a href="gaze-targeting.md">Ciblage des yeux</a></td><td style="text-align: center;"></td><td style="text-align: center;">✔️</td><td style="text-align: center;"></td>
</tr><tr>
<td> <a href="gaze-targeting.md">Ciblage des regards</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> <a href="gestures.md">Mouvements</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td></td>
</tr><tr>
<td> <a href="voice-design.md">Conception de la voix</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> Boîtier de commande</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr>
<tr>
<td> <a href="motion-controllers.md">Contrôleurs de mouvement</a></td><td></td><td style="text-align: center;"></td><td style="text-align: center;">✔️</td>

</tr>
<th>
<tr>
<td style="width:150px;"><strong>Perception et des fonctionnalités spatiales</strong></td>
<td style="width:150px; text-align: center;"><a href="hololens-hardware-details.md"><strong>HoloLens (1er gen)</strong></a></td>
<td style="width:150px; text-align: center;"><strong>HoloLens 2</strong></td>
<td style="width:150px; text-align: center;"><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
</tr>
</th>
<tr>

<td> <a href="spatial-sound-design.md">Sonorisation spatiale</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> <a href="spatial-mapping-design.md">Conception de mappage spatial</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td></td>
</tr><tr>
<td> <a href="hologram.md">Hologrammes</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td></td>
</tr>

</table>

## <a name="the-user-is-the-camera"></a>L’utilisateur est l’appareil photo

![L’utilisateur est l’appareil photo](images/useriscamera-640px.jpg)

Pensez toujours conception pour votre point de vue utilisateur, lorsqu’ils circulent sur leur univers réels et virtuels.

**Certaines questions à poser**
* Est l’utilisateur assis, inclinaison, permanent ou à pied lors de l’utilisation de votre expérience ?
* Comment votre contenu n’ajuste pas à des positions différentes ?
* L’utilisateur peut ajuster il ?
* L’utilisateur sera à l’aise avec votre application ?

**Bonnes pratiques**
* L’utilisateur est l’appareil photo et qu’ils contrôlent le déplacement. Let leur lecteur.
* Si vous avez besoin transporter pratiquement de l’utilisateur, être sensible aux problèmes liés à la gêne VESTIBULAIRE.
* Utiliser des animations plus courtes
* Animer à partir du bas à gauche/droite ou apparition en fondu au lieu de Z
* Ralentir le minutage
* Autoriser l’utilisateur d’afficher le monde en arrière-plan

**Pratiques à éviter**
* Ne secouez l’appareil photo ou volontairement le verrouiller à 3DOF (uniquement l’orientation, aucune traduction), elle peut rendre les utilisateurs à l’aise.
* Aucun mouvement brusque. Si vous avez besoin fournir un contenu vers ou à partir de l’utilisateur, déplacez-le lentement et sans heurts vers eux pour un maximum de confort. Les utilisateurs réagira aux menus volumineux à eux.
* Ne pas accélérer ou désactiver la caméra de l’utilisateur. Les utilisateurs sont sensibles à l’accélération (angulaire et Translation).

## <a name="leverage-the-users-perspective"></a>Tirer parti de l’utilisateur

Les utilisateurs voient le monde de la réalité mixte via affiche sur les appareils immersives et HOLOGRAPHIQUE. Sur le HoloLens, cet affichage est appelé le [frame HOLOGRAPHIQUE](holographic-frame.md).

Dans le développement 2D, contenu fréquemment sollicitée et des paramètres peuvent être placés dans les angles d’un écran pour les rendre facilement accessibles. Toutefois, dans les applications HOLOGRAPHIQUE, contenu dans les coins de la vue peut être désagréable pour l’accès. Dans ce cas, le centre de l’image holographique est l’emplacement principal pour le contenu.

L’utilisateur peut devoir être guidé pour aider à localiser les événements importants ou objets au-delà de leur vue immédiate. Vous pouvez utiliser les flèches, pistes claires, le déplacement de la tête de caractère, bulles, pointeurs, son spatial et invites vocales de guider l’utilisateur au contenu important dans votre application.

Il est recommandé de verrou pas votre contenu à l’écran pour le confort de l’utilisateur. Si vous devez conserver le contenu dans la vue, placez-le dans le monde et que le contenu « tag-along » comme le menu Démarrer. Contenu collectée, ainsi que l’utilisateur sera sembler plus naturelle dans l’environnement.

![Le menu Démarrer suit la vue de l’utilisateur lorsqu’il atteint le bord du frame](images/tagalong-1000px.jpg)<br>
*Le menu Démarrer suit la vue de l’utilisateur lorsqu’il atteint le bord du frame*

Sur HoloLens, hologrammes sentiront réels lorsqu’elles s’inscrivent dans le cadre HOLOGRAPHIQUE dans la mesure où ils ne coupés. Les utilisateurs se déplacera afin de voir les limites d’un hologramme dans le cadre. Sur HoloLens, il est important de simplifier votre interface utilisateur pour tenir dans la vue de l’utilisateur et de conserver le focus sur l’action principale. Pour des casques IMMERSIFS, il est important de conserver l’illusion d’un monde virtuel persistant dans le champ de vision de l’appareil.

## <a name="user-comfort"></a>Confort de l’utilisateur

Pour vous assurer de maximum [confort](comfort.md) sur Afficheur tête haute, il est important pour les concepteurs et développeurs de créer et présenter du contenu d’une manière qui imite comment humains interprètent des formes 3D et la position relative des objets dans le naturel World. À partir d’un point de vue physique, il est également important de concevoir le contenu qui ne nécessite pas de mouvements fatigante du cou ou armements.

Si le développement pour HoloLens ou des casques IMMERSIFS, il est important de restituer les éléments visuels pour deux yeux. Rendu d’un affichage tête haute dans un oeil uniquement peut rendre une interface difficile à comprendre, ainsi qu’à l’origine d’uneasiness aux yeux de l’utilisateur et le cerveau.

## <a name="share-your-experience"></a>Partagez votre expérience

À l’aide de [mixte de capture de la réalité](mixed-reality-capture.md), les utilisateurs peuvent capturer une photo ou une vidéo de leur expérience à tout moment. Envisagez d’expériences dans votre application où vous voulez encourager des captures instantanées ou des vidéos.

## <a name="leverage-basic-ui-elements-of-the-windows-mixed-reality-home"></a>Tirer parti des éléments de l’interface utilisateur de base de Windows Mixed Reality domestique

Tout comme l’expérience de PC de Windows démarre avec le bureau, Windows Mixed Reality commence par la page d’accueil. Le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) tire parti de notre capacité intégrée dès le départ pour comprendre et de parcourir les emplacements 3D. Avec HoloLens, votre page d’accueil est votre espace physique. Avec des casques IMMERSIFS, votre page d’accueil est virtuel.

Votre page d’accueil est également où vous utiliserez le menu Démarrer pour ouvrir et de placer les applications et le contenu. Vous pouvez remplir votre page d’accueil avec du contenu de la réalité mixte et plusieurs tâches à l’aide de plusieurs applications en même temps. Les éléments que vous placez dans votre page d’accueil resteront, même si vous redémarrez votre appareil.

## <a name="see-also"></a>Voir aussi
* [Ciblage des regards](gaze-targeting.md)
* [Mouvements](gestures.md)
* [Conception de la voix](voice-design.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Sonorisation spatiale](spatial-sound-design.md)
* [Conception de mappage spatial](spatial-mapping-design.md)
* [Confort](comfort.md)
* [Navigation dans Windows Mixed Reality domestique](navigating-the-windows-mixed-reality-home.md)
