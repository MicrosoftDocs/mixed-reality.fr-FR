---
title: Vue d’ensemble du développement
description: Cet article décrit les composants de base du développement d’une application Windows Mixed Reality.
author: mattzmsft
ms.author: grbury
ms.date: 02/10/2019
ms.topic: article
keywords: mise en route prise en main, principes de base, HoloLens, HoloLens, 2, casque immersif, unity, visual studio
ms.openlocfilehash: 1d23e458477cc23252ccd4c44f67c400aa356965
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597129"
---
# <a name="development-overview"></a>Vue d’ensemble du développement

Applications de réalité mixte peuvent être développées à l’aide de diverses technologies de développeur.  HoloLens exécute des applications qui sont générées avec le [plateforme Windows universelle](https://dev.windows.com/getstarted).  Casques IMMERSIFS exécuter des applications de plateforme Windows universelle, ainsi que les applications Win32.
En obtenant familiarisé avec les outils d’intergiciel (middleware) tels que Unity, vous pouvez commencer aujourd'hui des expériences de réalité mixte.  Tirer parti de l’open source [Toolkit de réalité mixte](install-the-tools.md) pour démarrer rapidement.
<a href="https://azure.microsoft.com/topic/mixed-reality" target="_blank">Mixte des services de réalité</a>, tel que <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres Spatial Azure</a>, ont des kits de développement logiciel qui peuvent d’intégrer dans diverses technologies de développement interplateforme ainsi.

>[!VIDEO https://www.youtube.com/embed/A784OdX8xzI]

## <a name="basics-of-mixed-reality-development"></a>Principes fondamentaux du développement de réalité mixte

[Une réalité mixte](mixed-reality.md) expériences sont activées par les nouvelles fonctionnalités de Windows pour comprendre l’environnement. Ces outils permettent aux développeurs de placer un [hologramme](hologram.md) dans le monde réel, et permettre aux utilisateurs de parcourir les mondes numériques en parcourant littéralement sur. 

Il s’agit des principaux blocs de construction pour le développement de réalité mixte :

<table>
<tr>
<th>Entrée</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1er gen)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> <a href="gaze.md">Utilisation de la tête</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> <a href="gaze.md">Regard de œil</a></td><td></td><td style="text-align: center;">✔️</td><td></td>
</tr><tr>
<td> Mains / <a href="gestures.md">mouvements</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td></td>
</tr><tr>
<td> <a href="voice-input.md">Voice</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> <a href="hardware-accessories.md">Gamepad</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> <a href="motion-controllers.md">Contrôleurs de mouvement</a></td><td></td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<th> Perception et des fonctionnalités spatiales</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1er gen)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> <a href="coordinate-systems.md">Coordonnées universelles</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> <a href="spatial-sound.md">Son spatial</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td> <a href="spatial-mapping.md">Mappage spatial</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td></td>
</tr>
</table>



Le modèle d’interaction de base pour [HoloLens](hololens-hardware-details.md) est [les regards](gaze.md), [mouvement](gestures.md), et [voix](voice-input.md), parfois appelé *GGV* . [Des casques IMMERSIFS Windows Mixed Reality](immersive-headset-hardware-details.md) également utilisez regards et vocale, mais échange [contrôleurs de mouvement](motion-controllers.md) pour les gestes.


Tous les appareils basée sur Windows la réalité mixte bénéficient de l’écosystème d’entrée disponible pour Windows, y compris la souris, clavier, boîtiers de commande et bien plus encore. Avec HoloLens, [Accessoires matériels](hardware-accessories.md) sont connectés via Bluetooth. Avec des casques IMMERSIFS accessoires vous connecter à l’ordinateur hôte via Bluetooth, USB et autres protocoles pris en charge.

Les fonctionnalités de présentation de l’environnement, telles que [coordonnées](coordinate-systems.md), [son spatial](spatial-sound.md), et [mappage spatial](spatial-mapping.md) fournissent les fonctionnalités nécessaires pour le mélange de réalité. Mappage spatial est unique pour HoloLens et permet des hologrammes interagir avec l’utilisateur et le monde physique autour d’elles. Systèmes de coordonnées autoriser le déplacement de l’utilisateur à affecter le déplacement dans le monde numérique.

[Hologrammes](hologram.md) sont constitués de lumière et son, qui s’appuient sur [rendu HOLOGRAPHIQUE](rendering.md). Comprendre l’expérience de placement et la persistance, comme illustré dans le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) (parfois appelé le « shell ») est une excellente façon raccordez-vous dans l’expérience utilisateur.

## <a name="tools-for-developing-for-mixed-reality"></a>Outils de développement pour la réalité mixte

Les outils que vous utilisez varie selon le [style d’application](app-views.md) vous souhaitez générer.
* [Applications avec une vue en 2D](building-2d-apps.md) tirer parti des outils pour la création d’applications de plateforme Windows universelle adapté aux environnements comme Windows Phone, PC et les tablettes. Ces applications sont familiarisées comme projections 2D placées dans la réalité mixte Windows domestique et peuvent travailler dans différents types de périphériques multiples (y compris phone et PC).
* Les applications immersives et HOLOGRAPHIQUES nécessitent des outils conçus pour tirer parti des API de réalité mixte Windows. Nous [vous recommandons d’utiliser Unity](unity-development-overview.md) pour créer des applications de réalité mixte. Les développeurs désireux de bâtir leur propres moteur peuvent [utiliser DirectX et les autres API Windows](directx-development-overview.md).

Quel que soit le type d’application que vous créez, ces outils faciliteront votre expérience de développement d’application :
* [Visual Studio et le Kit de développement logiciel Windows](using-visual-studio.md)
* [Portail d’appareil Windows](using-the-windows-device-portal.md)
* [Émulateur de HoloLens](using-the-hololens-emulator.md) (émulateur HoloLens 2 bientôt disponible)
* [Simulateur de réalité mixte Windows](using-the-windows-mixed-reality-simulator.md)
* [Critères de qualité des applications](app-quality-criteria.md)

## <a name="see-also"></a>Voir aussi
* [Installer les outils](install-the-tools.md)
* <a href="https://azure.microsoft.com/topic/mixed-reality" target="_blank">Services de réalité mixte</a>
* [Didacticiels de réalité mixtes](academy.md)
* [Projets Open source](open-source-projects.md)
* [Principes de base MR 100 : Mise en route avec Unity](holograms-100.md)
* [Recommandations de compatibilité Windows Mixed Reality minimale PC matérielles](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines)
* [Soumission d’une application pour le Windows Store](submitting-an-app-to-the-microsoft-store.md)
