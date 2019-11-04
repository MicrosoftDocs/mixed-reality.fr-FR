---
title: Vues d’applications
description: Les deux types d’affichages dans les applications Windows Mixed Reality sont des vues immersives et des vues 2D.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: vue immersive, vue 2D, ardoise, application
ms.openlocfilehash: a5b50df5be31d66a866e691d9e059bcf38672064
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437036"
---
# <a name="app-views"></a>Vues d’applications

Les applications Windows peuvent contenir deux types d’affichages, des vues **immersives** et des **vues 2D**. Les applications peuvent basculer entre les différents affichages immersifs et les vues 2D, en présentant leurs vues 2D sur une analyse sous la forme d’une fenêtre ou dans un casque comme un ardoise. Les applications qui ont au moins une vue immersive sont classées en tant qu' **applications de réalité mixte**. Les applications qui n’ont jamais une vue immersive sont des **applications 2D**.

## <a name="immersive-views"></a>Vues immersives

Une vue immersive donne à votre application la possibilité de créer des hologrammes dans le monde autour de vous ou de plonger l’utilisateur dans un environnement virtuel. Quand une application dessine dans l’affichage immersif, aucune autre application n’est dessinée en même temps&mdash;les hologrammes de plusieurs applications ne sont pas composites ensemble. En ajustant continuellement la perspective à partir de laquelle votre [application affiche](rendering.md) sa scène pour correspondre aux mouvements de l’utilisateur, votre application peut afficher des hologrammes [universels](coordinate-systems.md) qui restent à un point fixe dans le monde réel, ou elle peut afficher un monde virtuel qui contient sa position lorsqu’un utilisateur se déplace dans celui-ci.

![dans une vue immersive, les hologrammes peuvent être placés dans le monde entier autour de vous.](images/designoverview-940px.jpg)<br>
*Dans une vue immersive, les hologrammes peuvent être placés dans le monde entier*

Sur [HoloLens](hololens-hardware-details.md), votre application affiche ses hologrammes en plus de l’environnement réel de l’utilisateur. Sur un [casque d’immersion immersif Windows Mixed Reality](immersive-headset-hardware-details.md), l’utilisateur ne peut pas voir le monde réel et, par conséquent, votre application doit rendre tout ce que l’utilisateur verra.

La [page d’accueil de la réalité mixte Windows](navigating-the-windows-mixed-reality-home.md) (y compris le menu Démarrer et les hologrammes que vous avez placés autour de l’environnement) ne s’affiche pas non plus dans un affichage immersif. Sur HoloLens, les notifications système qui se produisent lorsqu’une vue immersive est affichée sont relayées de façon audible par Cortana et l’utilisateur peut répondre avec une entrée vocale.

En mode immersif, votre application est également responsable de la gestion de toutes les entrées. L’entrée dans Windows Mixed Reality est composée [de points](gaze-and-commit.md)de contrôle de point de présence, de [mouvement](gaze-and-commit.md#composite-gestures) (HoloLens uniquement), de [contrôleurs](motion-controllers.md) [vocaux](voice-input.md) et de mouvements (casques immersifs uniquement).

## <a name="2d-views"></a>vues 2D

![plusieurs vues 2D disposées dans la page d’hébergement Windows Mixed Reality](images/teleportation-940px.png)<br>
*Plusieurs applications avec une vue 2D placée dans la page d’hébergement de Windows Mixed Reality*

Une application dotée d’une vue 2D apparaît dans la [page d’hébergement de Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md) (parfois appelée « Shell ») en tant que pièce virtuelle, rendue avec les lanceurs d’applications et autres hologrammes que l’utilisateur a placés dans son monde. L’utilisateur peut ajuster cette ardoise pour la déplacer et la mettre à l’échelle, même si elle reste à une résolution fixe, quelle que soit sa taille. Si le premier affichage de votre application est une vue 2D, votre contenu 2D remplit la même ardoise que celle utilisée pour lancer l’application.

Sur un casque de bureau, vous pouvez exécuter toutes les applications de plateforme Windows universelle (UWP) qui s’exécutent sur votre moniteur de bureau dès aujourd’hui. Ces applications affichent déjà des vues 2D aujourd’hui et leur contenu apparaît automatiquement dans un ardoise dans le monde de l’utilisateur lors de son lancement. les applications UWP 2D peuvent cibler la famille d’appareils **Windows. Universal** pour qu’elle s’exécute sur les casques de bureau et sur HoloLens en tant que tablettes.

L’une des principales utilisation des vues 2D consiste à afficher un formulaire de saisie de texte qui peut utiliser le clavier du système. Étant donné que l’interpréteur de commandes ne peut pas être rendu sur une vue immersive, l’application doit basculer vers une vue 2D pour afficher le clavier système. Les applications qui souhaitent accepter la saisie de texte peuvent basculer vers une vue 2D avec une zone de texte. Alors que cette zone de texte a le focus, le système affiche le clavier du système, ce qui permet à l’utilisateur d’entrer du texte.

Notez que sur un PC de bureau, une application peut avoir des vues 2D à la fois sur le moniteur de bureau et dans un casque attaché. Par exemple, vous pouvez parcourir Edge sur votre moniteur de bureau à l’aide de sa vue principale 2D pour trouver une vidéo de 360 degrés. Quand vous jouez cette vidéo, Edge lance une vue immersive secondaire à l’intérieur du casque pour afficher le contenu vidéo immersif.

## <a name="see-also"></a>Articles associés

* [Modèle d’application](app-model.md)
* [Mise à jour des applications UWP 2D pour la réalité mixte](building-2d-apps.md)
* [Obtention d’un HolographicSpace](getting-a-holographicspace.md)
* [Exploration de la page d’accueil Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md)
* [Types d’applications de réalité mixte](types-of-mixed-reality-apps.md)
