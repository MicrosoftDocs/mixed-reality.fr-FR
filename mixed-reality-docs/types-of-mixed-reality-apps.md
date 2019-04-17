---
title: Types d’applications de réalité mixte
description: Un des avantages du développement d’applications pour Windows Mixed Reality est qu’il existe une gamme d’expériences de la plateforme pouvant prendre en charge à partir des environnements virtuels totalement immersives, superposition clair d’informations sur environmentl actuel d’un utilisateur.
author: rwinj
ms.author: willyang
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, les modèles d’application
ms.openlocfilehash: 97f8039dcd9bbf8ee3d6c7be926db16b60a76b97
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593707"
---
# <a name="types-of-mixed-reality-apps"></a>Types d’applications de réalité mixte

Un des avantages du développement d’applications pour Windows Mixed Reality est qu’il existe une gamme d’expériences de la plateforme pouvant prendre en charge. À partir d’environnements totalement immersives et virtuels, aux informations claires superposition sur un environnement d’utilisateur actuel, Windows Mixed Reality fournit un ensemble robust d’outils pour introduire tout sur la durée de vie. Il est important pour un créateur de l’application comprendre au début de leur processus de développement concernant où leur expérience se trouve le long de ce spectre. Cette décision a une incidence sur la composition de conception d’application et le chemin d’accès technologique pour le développement.

## <a name="enhanced-environment-apps-hololens-only"></a>Applications de l’environnement amélioré (HoloLens uniquement)

Une des manières plus efficaces que réalité mixte peut apporter de valeur aux utilisateurs est en facilitant le positionnement des informations numériques ou des contenus dans un environnement d’utilisateur actuel. Il s’agit d’une application d’environnement améliorée. Cette approche est souvent utilisée pour les applications où l’emplacement contextuel de contenu numérique dans le monde réel est primordiale et/ou en conservant l’environnement l’utilisateur réel « present » lors de leur expérience est de clé. Cette approche permet également aux utilisateurs facilement déplacer des tâches du monde réel aux tâches numériques et sauvegarder facilement, encore plus de crédibilité pour promise que les applications de réalité mixte que l’utilisateur voit font réellement une partie de leur environnement de prêt.

![Applications de l’environnement améliorée](images/enhancedenvironmentapps-640px.jpg)<br>
*Applications de l’environnement améliorée*

**Exemple utilise**
* Une application de style de bloc-notes de réalité mixte qui permet aux utilisateurs de créer et placer des notes autour de leur environnement
* Une application de télévision de réalité mixte placée dans une zone à l’aise pour l’affichage
* Une réalité mixte cuisine application placé au-dessus de l’îlot de cuisine pour aider à une tâche de préparation
* Une application de réalité mixte qui permet aux utilisateurs le sentiment de « vision rayons x » (autrement dit, un hologramme placé en haut d’et simule un objet du monde réel, tout en autorisant l’utilisateur de voir sous forme HOLOGRAPHIQUE « à l’intérieur »)
* Annotations de réalité mixte de placement dans une fabrique pour donner des informations nécessaires du travail
* ORIENTATION PARTICULIERE réalité mixte dans un espace de bureau
* Expériences munie de réalité mixte (c'est-à-dire rencontre de style de jeu de plateau)
* Les applications de communication de réalité mixte tels que Skype

## <a name="blended-environment-apps"></a>Applications de l’environnement mixte

Possibilité de réalité mixte Windows reconnaît et mapper l’environnement utilisateur, il est capable de créer une couche numérique qui peut être complètement à superposer sur l’espace de l’utilisateur. Couche mince respecte la forme et les limites de l’environnement utilisateur, mais l’application peut choisir pour transformer certains éléments idéal pour découvrir les prochaines l’utilisateur dans l’application. Il s’agit d’une application d’environnement mixte. Contrairement à une application d’environnement améliorée, applications de l’environnement mixte ne peuvent être soins suffisamment sur l’environnement pour mieux utiliser sa composition pour encourager comportement utilisateur spécifique (par exemple, le déplacement ou l’exploration encourageante) ou en remplaçant les éléments avec des modifications (une cuisine compteur est pratiquement dépouillée pour afficher un modèle de mosaïque différent). Ce type d’expérience peut même transformer un élément dans un objet entièrement différent, tout en conservant les dimensions approximatives de l’objet en tant que sa base (un îlot de cuisine est transformé en un benne pour un jeu de policier crime).

![Applications de l’environnement mixte](images/blendedenvironmentapps-640px.jpg)<br>
*Applications de l’environnement mixte*

**Exemple utilise**
* Une application de conception de l’intérieur de réalité mixte qui peut se peindre murs, countertops ou étages dans différentes couleurs et des modèles
* Une application de réalité mixte qui permet à un concepteur automobile d’itérations de conception nouvelle couche pour une actualisation de la voiture à venir sur une voiture existante
* Un lit est « couvert » et remplacé par un support de fruits de réalité mixte dans le jeu d’enfants
* Un support est « couvert » et remplacé par une réalité mixte benne dans un jeu de policier crime
* Un lanterne négatif est « couvert » et remplacé par poteau indicateur à l’aide à peu près la même forme et dimension
* Une application qui permet aux utilisateurs de trous de souffle dans leurs murs de monde réel ou immersives qui révèlent un monde magique

## <a name="immersive-environment-apps"></a>Applications immersives environnement

Les applications immersives environnement sont centrées sur un environnement qui modifie complètement monde de l’utilisateur et les placer dans une autre heure et un espace. Ces environnements peuvent se sentent bien réelles, créer des expériences immersives et mémorables sont uniquement limités par l’imagination du créateur de l’application. Contrairement aux applications de l’environnement mixte, une fois que Windows Mixed Reality identifie l’espace de l’utilisateur, une application d’environnement immersif peut totalement ignorer l’environnement l’utilisateur actuel et remplacez-le stock ensemble avec l’un de ses propres. Ces expériences peuvent eux aussi complètement séparer temps et espace, ce qui signifie qu’un utilisateur peut parcourir les rues de Rome dans une expérience d’immersion, tout en restant relativement toujours dans leur espace de monde réel. Contexte de l’environnement du monde réel n’est peut-être pas important pour une application d’environnement immersif.

![Applications immersives environnement](images/windows-mixed-reality-640px.jpg)<br>
*Applications immersives environnement*

**Exemple utilise**
* Une application immersive qui permet aux utilisateurs de parcourir un espace totalement distinct de leurs propres (par exemple, parcourir un célèbre construction, le musée, la ville)
* Une application immersive qui gère un événement ou un scénario autour de l’utilisateur (par exemple, une bataille ou performances)

## <a name="see-also"></a>Voir aussi
* [Vue d’ensemble du développement](development-overview.md)
* [Modèle d’application](app-model.md)
* [Vues de l’application](app-views.md)
