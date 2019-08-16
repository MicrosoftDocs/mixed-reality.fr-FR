---
title: Présentation du développement
description: Cet article décrit les blocs de construction de base du développement d’une application Windows Mixed Reality.
author: mattzmsft
ms.author: grbury
ms.date: 02/10/2019
ms.topic: article
keywords: prise en main, principes de base, HoloLens, HoloLens 2, casque immersif, Unity, Visual Studio
ms.openlocfilehash: 23bd173f89a468b4403d44236534bfe811a968dd
ms.sourcegitcommit: 90ce9415889e7121dd2fd76a893dc3734672881b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64873973"
---
# <a name="development-overview"></a>Présentation du développement

Les applications de réalité mixte peuvent être développées à l’aide de diverses technologies de développement.  HoloLens exécute des applications qui sont générées avec l' [plateforme Windows universelle](https://dev.windows.com/getstarted).  Les casques immersifs exécutent des applications plateforme Windows universelle, ainsi que des applications Win32.
En vous familiarisant avec les outils middleware tels que Unity, vous pouvez commencer à créer des expériences de réalité mixte dès aujourd’hui.  Tirez parti de la [boîte à outils de réalité mixte](install-the-tools.md) Open source pour commencer rapidement.
Les <a href="https://azure.microsoft.com/topic/mixed-reality" target="_blank">services de réalité mixte</a>, tels que les <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres spatiales Azure</a>, possèdent également des kits de développement logiciel (SDK) qui peuvent s’intégrer à différentes technologies de développement multiplateforme.

>[!VIDEO https://www.youtube.com/embed/A784OdX8xzI]

## <a name="basics-of-mixed-reality-development"></a>Principes de base du développement de réalité mixte

Les expériences de [réalité mixte](mixed-reality.md) sont rendues possibles grâce à de nouvelles fonctionnalités Windows qui facilitent la compréhension de l’environnement. Les développeurs peuvent ainsi placer un [hologramme](hologram.md) dans le monde réel et permettre aux utilisateurs d’explorer littéralement des mondes numériques. 

Voici les fonctionnalités principales du développement de réalité mixte :

<table>
<tr>
<th>Entrée</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1ère génération)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> <a href="gaze.md">Suivi de la tête</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> <a href="gaze.md">Suivre du regard</a></td><td></td><td style="text-align: center;">✔️</td><td></td>
</tr><tr>
<td> Mains/ <a href="gestures.md">mouvements</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td></td>
</tr><tr>
<td> <a href="voice-input.md">Voix</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> <a href="hardware-accessories.md">Boîtier de commande</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> <a href="motion-controllers.md">Contrôleurs de mouvement</a></td><td></td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<th> Perception et fonctionnalités spatiales</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1ère génération)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> <a href="coordinate-systems.md">Coordonnées universelles</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> <a href="spatial-sound.md">Son spatial</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> <a href="spatial-mapping.md">Mappage spatial</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td></td>
</tr>
</table>



Le modèle d’interaction de base pour [HoloLens](hololens-hardware-details.md) est [pointage du regard](gaze.md), [mouvement](gestures.md) et [voix](voice-input.md), parfois appelé *GGV* (Gaze, Gesture et Voice). Les [casques immersifs Windows Mixed Reality](immersive-headset-hardware-details.md) utilisent également le pointage du regard et la voix, mais échangent les [contrôleurs de mouvement](motion-controllers.md) pour les mouvements.


Tous les appareils Windows de réalité mixte tirent parti de l’écosystème d’entrée disponible pour Windows, y compris la souris, le clavier, les boîtiers de manette, et bien plus encore. Dans le cas de HoloLens, les [accessoires matériels](hardware-accessories.md) sont connectés via Bluetooth. Dans le cas des casques immersifs, les accessoires se connectent à l’ordinateur hôte via Bluetooth, un port USB et autres protocoles pris en charge.

Les fonctionnalités de compréhension de l’environnement, telles que les [coordonnées](coordinate-systems.md), le [son spatial](spatial-sound.md) et le [mappage spatial](spatial-mapping.md), fournissent les fonctionnalités nécessaires pour obtenir une réalité mixte. Propre à HoloLens, le mappage spatial permet aux hologrammes d’interagir avec l’utilisateur et le monde physique qui l’entoure. Avec les systèmes de coordonnées, le déplacement de l’utilisateur peut affecter le déplacement dans le monde numérique.

Les [hologrammes](hologram.md) sont faits de son et de lumière, lesquels sont basés sur le [rendu holographique](rendering.md). Pour vous familiariser avec l’expérience utilisateur, rien de tel que de comprendre l’expérience du placement et de la persistance, comme l’illustre la [page d’accueil Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md) (parfois appelée « shell »).

## <a name="tools-for-developing-for-mixed-reality"></a>Outils de développement pour la réalité mixte

Les outils employés dépendent du [style d’application](app-views.md) à générer.
* Les [applications dotées d’une vue en 2D](building-2d-apps.md) tirent parti des outils de génération d’applications UWP adaptés aux environnements comme Windows Phone, les PC et les tablettes. Ces applications prennent la forme de projections 2D dans la page d’accueil Windows Mixed Reality et peuvent fonctionner sur différents types d’appareils (notamment téléphones et PC).
* Les applications immersives et holographiques nécessitent des outils conçus pour bénéficier des API Windows Mixed Reality. Nous vous [recommandons d’utiliser Unity](unity-development-overview.md) pour générer des applications de réalité mixte. Les développeurs désireux de générer leu propre moteur peuvent [utiliser DirectX et d’autres API Windows](directx-development-overview.md).

Quel que soit le type d’application que vous générez, les outils ci-après facilitent votre expérience de développement d’application :
* [Visual Studio et le SDK Windows](using-visual-studio.md)
* [Portail d’appareil Windows](using-the-windows-device-portal.md)
* [Émulateur HoloLens](using-the-hololens-emulator.md) (Émulateur HoloLens 2 bientôt disponible)
* [Simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md)
* [Critères de qualité des applications](app-quality-criteria.md)

## <a name="see-also"></a>Voir aussi
* [Installer les outils](install-the-tools.md)
* <a href="https://azure.microsoft.com/topic/mixed-reality" target="_blank">Services de réalité mixte</a>
* [Didacticiels de réalité mixte](tutorials.md)
* [Projets open source](open-source-projects.md)
* [Réalité mixte - Principes fondamentaux - Cours 100 : Bien démarrer avec Unity](holograms-100.md)
* [Instructions de compatibilité matérielle PC minimale pour Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines)
* [Envoi d’une application au Windows Store](submitting-an-app-to-the-microsoft-store.md)
