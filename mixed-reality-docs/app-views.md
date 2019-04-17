---
title: Vues d’applications
description: Les deux types de vues dans les applications de réalité mixte Windows sont des vues immersives et 2D.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: vue immersive, application de la vue en 2D, ardoise,
ms.openlocfilehash: 2cf65941616ac6906d40e4b4616311317ac705d3
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596977"
---
# <a name="app-views"></a>Vues d’applications

Les applications Windows peuvent contenir deux types de vues, **vues immersives** et **vues 2D**. Applications peuvent basculer entre leurs différents immersives de vues et 2D montrant leurs vues 2D soit sur une analyse sous la forme d’une fenêtre ou dans un casque comme une ardoise. Les applications qui ont au moins une vue immersif sont classées comme **applications de réalité mixte**. Les applications qui n’ont jamais une vue immersif sont **applications 2D**.

## <a name="immersive-views"></a>Vues immersives

Une vue immersive offre la possibilité de créer hologrammes dans le monde ou découvrir les prochaines l’utilisateur dans un environnement virtuel à votre application. Lorsqu’une application dessine dans la vue immersive, aucune autre application ne dessine en même temps&mdash;hologrammes à partir de plusieurs applications ne sont pas combinés ensemble. En ajustant en permanence la perspective à partir de laquelle votre [application rendus](rendering.md) son scène pour faire correspondre les mouvements de la tête de l’utilisateur, votre application peut rendre [verrouillé de monde](coordinate-systems.md) hologrammes qui restent à un point fixe dans la réalité monde, ou il peut rendre un monde virtuel qui conserve sa position quand un utilisateur se déplace dans celui-ci.

![Dans une vue immersives, hologrammes peuvent être placés dans le monde.](images/designoverview.jpg)<br>
*Dans une vue immersives, hologrammes peuvent être placés dans le monde*

Sur [HoloLens](hololens-hardware-details.md), votre application restitue son hologrammes sur son environnement réel de l’utilisateur. Sur un [casque immersif Windows Mixed Reality](immersive-headset-hardware-details.md), l’utilisateur ne peut pas voir le monde réel, et donc de votre application doit rendre tout ce que l’utilisateur verra.

Le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) (y compris le menu Démarrer et hologrammes que vous avez placé autour de l’environnement) ne rend pas alors que dans un immersives soit afficher. Sur HoloLens, toutes les notifications système qui se produisent quand vous présente une vue immersive seront relayées audible par Cortana, et l’utilisateur peut répondre avec une entrée de la voix.

Dans un affichage immersif, votre application est également chargée de gérer toutes les entrées. Entrée dans la réalité mixte Windows se compose de [les regards](gaze.md), [mouvement](gestures.md) (HoloLens uniquement), [voix](voice-input.md) et [contrôleurs de mouvement](motion-controllers.md) (immersives casques uniquement).

## <a name="2d-views"></a>Vues 2D

![Plusieurs vues 2D disposé autour de Windows Mixed Reality domestique](images/teleportation-640px.png)<br>
*Plusieurs applications avec une vue en 2D affichée autour de Windows Mixed Reality domestique*

Une application avec une vue en 2D apparaît dans le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) (parfois appelé le « shell ») comme une ardoise virtuelle, rendu en même temps que les lanceurs d’applications et autres hologrammes placée par l’utilisateur dans leur environnement. L’utilisateur peut ajuster cette ardoise pour déplacer et mettre à l’échelle, même si elle reste à une résolution fixe, quel que soit sa taille. Si votre application premier est une vue en 2D, votre contenu 2D remplira l’ardoise même utilisé pour lancer l’application.

Dans un casque de bureau, vous pouvez exécuter toutes les applications Universal Windows Platform (UWP) qui s’exécutent sur votre moniteur du bureau dès aujourd'hui. Ces applications sont déjà rendu des vues 2D aujourd'hui, et leur contenu s’affichent automatiquement dans une séquence dans le monde de l’utilisateur au lancement. Les applications UWP 2D peuvent cibler le **Windows.Universal** famille de périphériques pour s’exécuter sur les deux casques de bureau et sur HoloLens comme les tablettes multimédias.

Une des principales utilisations de vues 2D consiste à afficher un formulaire de saisie de texte qui vous utiliser le clavier du système. Étant donné que l’interpréteur de commandes ne peut pas restituer sur une vue immersive, l’application doit passer à une vue 2D à afficher le clavier système. Applications désireuses d’accepter l’entrée de texte peuvent passer à une vue 2D avec une zone de texte. Bien que cette zone de texte a le focus, le système affiche le clavier système, permettant à l’utilisateur d’entrer du texte.

Notez que sur un PC de bureau, une application peut avoir des vues 2D sur les deux le moniteur de bureau et dans un casque attaché. Par exemple, vous pouvez parcourir Edge sur votre moniteur du Bureau à l’aide de sa vue 2D principale pour rechercher une vidéo à 360 degrés. Lorsque vous regardez cette vidéo, Edge lancera une vue secondaire immersif à l’intérieur le casque pour afficher le contenu vidéo immersif.

## <a name="see-also"></a>Voir aussi

* [Modèle d’application](app-model.md)
* [La mise à jour des applications UWP 2D pour la réalité mixte](building-2d-apps.md)
* [Obtention d’un HolographicSpace](getting-a-holographicspace.md)
* [Navigation dans Windows Mixed Reality domestique](navigating-the-windows-mixed-reality-home.md)
* [Types d’applications de réalité mixte](types-of-mixed-reality-apps.md)
