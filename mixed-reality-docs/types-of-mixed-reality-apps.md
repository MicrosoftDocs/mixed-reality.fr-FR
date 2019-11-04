---
title: Types d’applications de réalité mixte
description: L’un des avantages du développement d’applications pour Windows Mixed Reality est qu’il existe un éventail d’expériences que la plateforme peut prendre en charge à partir d’environnements virtuels et entièrement immersifs, en passant par la couche d’informations légère sur l’environnement actuel d’un utilisateur.
author: rwinj
ms.author: willyang
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, modèles d’application
ms.openlocfilehash: 62a0b76ba7853262a46b34466a6d3b0567bc137d
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438260"
---
# <a name="types-of-mixed-reality-apps"></a>Types d’applications de réalité mixte

L’un des avantages du développement d’applications pour Windows Mixed Reality est qu’il existe un éventail d’expériences que la plateforme peut prendre en charge. Des environnements virtuels entièrement immersifs à la couche d’informations légère sur l’environnement actuel d’un utilisateur, Windows Mixed Reality fournit un ensemble d’outils robustes pour donner vie à toute expérience. Il est important pour un concepteur d’applications de comprendre au plus tôt son processus de développement quant à la position de son expérience sur ce spectre. Cette décision aura un impact sur la conception de la conception d’application et le chemin d’accès technologique pour le développement.

## <a name="enhanced-environment-apps-hololens-only"></a>Applications d’environnement améliorées (HoloLens uniquement)

L’un des moyens les plus puissants dont la réalité mixte peut apporter la valeur aux utilisateurs consiste à faciliter l’emplacement des informations numériques ou du contenu dans l’environnement actuel d’un utilisateur. Il s’agit d’une application d’environnement améliorée. Cette approche est populaire pour les applications où le positionnement contextuel du contenu numérique dans le monde réel est primordial et/ou que l’environnement réel de l’utilisateur « présent » est essentiel. Cette approche permet également aux utilisateurs de passer facilement de tâches réelles à des tâches numériques et de les rendre plus facilement, en prêtant encore plus de certaine crédibilité pour garantir que les applications de réalité mixte que l’utilisateur voit font véritablement partie de leur environnement.

![des applications d’environnement améliorées](images/enhancedenvironmentapps-640px.jpg)<br>
*Applications d’environnement améliorées*

**Exemples d’utilisation**
* Application de style Notepad de réalité mixte qui permet aux utilisateurs de créer et de placer des notes dans leur environnement
* Une application de télévision de réalité mixte placée dans un endroit confortable pour l’affichage
* Application de cuisson de réalité mixte placée au-dessus de l’île de cuisine pour faciliter la tâche de cuisson
* Application de réalité mixte qui donne aux utilisateurs le sentiment de « x-ray vision » (par exemple, un hologramme placé en haut et imite un objet réel, tout en permettant à l’utilisateur de voir « dedans » de façon holographique)
* Annotations de réalité mixte placées dans une fabrique pour fournir les informations nécessaires pour le travail
* Wayfinding de la réalité mixte dans un espace de travail
* Expériences de bureau de la réalité mixte (c’est-à-dire des expériences de style de jeu)
* Applications de communication de réalité mixte comme Skype

## <a name="blended-environment-apps"></a>Applications d’environnement fusionné

En raison de la capacité de Windows Mixed Reality à reconnaître et à mapper l’environnement de l’utilisateur, il est capable de créer une couche numérique qui peut être entièrement superposée à l’espace de l’utilisateur. La couche mince respecte la forme et les limites de l’environnement de l’utilisateur, mais l’application peut choisir de transformer certains éléments qui conviennent le mieux pour plonger l’utilisateur dans l’application. C’est ce que l’on appelle une application d’environnement fusionné. Contrairement à une application d’environnement améliorée, les applications de l’environnement fusionné peuvent uniquement s’occuper de l’environnement pour mieux utiliser son composition pour encourager un comportement spécifique de l’utilisateur (par exemple, encourager le déplacement ou l’exploration) ou remplacer des éléments par des modifications (une cuisine le compteur est virtuellement dépouillé pour afficher un modèle de mosaïque différent). Ce type d’expérience peut même transformer un élément en un objet complètement différent, tout en conservant les dimensions approximatives de l’objet en tant que base (un îlot de cuisine est transformé en benne pour un jeu de criminalité plus excitant).

![les applications de l’environnement fusionné](images/blendedenvironmentapps-640px.jpg)<br>
*Applications d’environnement fusionné*

**Exemples d’utilisation**
* Une application de conception intérieure de réalité mixte qui peut peindre des murs, des plans de plan ou des planchers dans des couleurs et des modèles différents
* Application de réalité mixte permettant à un concepteur automobile de coucher de nouvelles itérations de conception pour une prochaine actualisation de la voiture sur une voiture existante
* Une vitre est « couverte » et remplacée par un peuplement de réalité mixte dans le jeu des enfants
* Un bureau est « couvert » et remplacé par une benne de réalité mixte dans un jeu plus excitant du crime
* Une lanterne en suspens est « couverte » et remplacée par un poteau à l’aide de la même forme et de la même dimension
* Application qui permet aux utilisateurs d’éclater des trous dans leurs murs réels ou immersifs, qui révèlent un monde magique

## <a name="immersive-environment-apps"></a>Applications d’environnement immersif

Les applications d’environnement immersif sont centrées autour d’un environnement qui modifie complètement le monde de l’utilisateur et peut les placer dans un autre temps et dans un autre espace. Ces environnements peuvent sembler très réels, créant des expériences immersifs et excitantes qui ne sont limitées que par l’imagination de l’auteur de l’application. Contrairement aux applications d’environnement fusionné, une fois que Windows Mixed Reality identifie l’espace de l’utilisateur, une application d’environnement immersif peut ignorer totalement l’environnement actuel de l’utilisateur et la remplacer par l’un de ses propres actions. Ces expériences peuvent également complètement séparer le temps et l’espace, ce qui signifie qu’un utilisateur peut parcourir les rues de Rome dans une expérience immersive, tout en restant relativement toujours dans son espace réaliste. Le contexte de l’environnement réel peut ne pas être important pour une application d’environnement immersif.

![des applications d’environnement immersif](images/windows-mixed-reality-640px.jpg)<br>
*Applications d’environnement immersif*

**Exemples d’utilisation**
* Une application immersif qui permet à un utilisateur de parcourir un espace complètement distinct de son propre utilisateur (par exemple, en passant par une construction célèbre, un musée, une ville populaire)
* Application immersif qui orchestre un événement ou un scénario autour de l’utilisateur (par exemple, une bataille ou une performance)

## <a name="see-also"></a>Articles associés
* [Vue d’ensemble du développement](development.md)
* [Modèle d’application](app-model.md)
* [Vues d’applications](app-views.md)
