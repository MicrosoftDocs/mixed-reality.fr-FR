---
title: Utiliser HoloLens dans de nouveaux espaces
description: HoloLens apprend à quoi ressemble un espace dans le temps. Les utilisateurs peuvent faciliter ce processus en déplaçant le HoloLens de certaines façons à travers l’espace.
author: dorreneb
ms.author: dobrown
ms.date: 08/16/2019
ms.topic: article
keywords: Windows Mixed Reality, conception, mappage spatial, HoloLens, reconstruction des surfaces, maillage, suivi des têtes, mappage
ms.openlocfilehash: a6a83dfc2c883723e4cd79c0dc46a9cd78f1f604
ms.sourcegitcommit: 60f73ca23023c17c1da833c83d2a02f4dcc4d17b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2019
ms.locfileid: "69566018"
---
# <a name="use-hololens-in-new-spaces"></a>Utiliser HoloLens dans de nouveaux espaces

HoloLens *mappe*, ou apprend sur, son environnement lorsque l’utilisateur se déplace autour d’un espace. Au fil du temps, le HoloLens crée une *carte spatiale* de toutes les parties de l’environnement qui ont été observées. HoloLens met à jour la carte au fur et à mesure que des modifications sont observées dans l’environnement. Cette analyse est automatiquement conservée entre les lancements de l’application.

HoloLens crée et met à jour les mappages tant que l’appareil est sous tension et qu’un utilisateur est connecté. Si vous tenez l’appareil avec les caméras pointant sur un espace, celui-ci essaie de mapper la zone. Alors que le HoloLens apprend un espace naturellement dans le temps, il existe des conseils et des astuces pour mettre l’espace plus rapidement et plus efficacement. 

Si votre HoloLens ne peut pas mapper votre espace ou n’est pas à l’étalonnage, vous pouvez entrer en mode limité. En mode limité, vous ne pourrez pas placer des hologrammes dans votre environnement.

## <a name="tips-and-tricks-for-mapping-spaces"></a>Trucs et astuces pour le mappage des espaces

### <a name="make-sure-the-space-is-set-up-for-mixed-reality"></a>Assurez-vous que l’espace est configuré pour la réalité mixte

Dans un environnement, les fonctionnalités peuvent compliquer l’interprétation d’un espace par le HoloLens. Les niveaux d’éclairage, les matériaux dans l’espace, la disposition des objets et plus peuvent tous affecter la manière dont HoloLens mappe une zone.

Vous trouverez des conseils sur la configuration de votre espace pour HoloLens et d’autres appareils de réalité mixte dans [considérations environnementales pour hololens](environment-considerations-for-hololens.md).

### <a name="understand-the-scenarios-for-the-area"></a>Comprendre les scénarios de la zone

Il est important de consacrer le plus de temps à l’utilisation du HoloLens afin que la carte soit pertinente et complète. 

Par exemple, si un scénario utilisateur pour HoloLens implique de passer du point A au point B, parcourez ce chemin deux à trois fois, en regardant toutes les directions à mesure que vous déplacez. 

### <a name="walk-slowly-around-the-space"></a>Parcourez lentement l’espace

Si vous parcourez trop rapidement dans la zone, il est probable que le HoloLens ne manquera pas de zones de mappage. Parcourez lentement l’espace, en arrêtant tous les 9 à 5-8 de votre environnement.

Les mouvements lisses aident également la carte HoloLens plus efficacement.

### <a name="look-in-all-directions"></a>Rechercher dans toutes les directions

Si vous recherchez à mesure que vous mappez l’espace, vous obtenez des données supplémentaires sur les emplacements où les points sont relatifs les uns par rapport aux autres. 

Si vous ne parvenez pas à rechercher, par exemple, le HoloLens peut ne pas savoir où se trouve le plafond dans une pièce. 

N’oubliez pas de regarder au sol au fur et à mesure que vous mappez l’espace.

### <a name="cover-key-areas-multiple-times"></a>Couvrir plusieurs fois les domaines clés

Le déplacement de plusieurs fois dans une zone vous aidera à sélectionner les fonctionnalités que vous n’avez peut-être pas manquées lors de la première procédure pas à pas. Essayez de parcourir une zone deux à trois fois pour créer une carte idéale.

Si possible, lors de la répétition de ces mouvements, consacrez du temps à parcourir une zone dans un sens, puis à vous déplacer et à revenir en arrière.

### <a name="take-your-time-mapping-the-area"></a>Prendre votre temps à mapper la zone

Le schéma HoloLens peut prendre de 15 à 20 minutes pour être entièrement mappé et ajusté à son environnement. Si vous avez un espace dans lequel vous envisagez d’utiliser un HoloLens fréquemment, prendre ce temps en amont pour mapper l’espace peut empêcher des problèmes plus tard. 

## <a name="possible-errors-in-the-spatial-map"></a>Erreurs possibles dans la carte spatiale

Les erreurs dans les données de mappage spatiale sont classées dans l’une des trois catégories suivantes:

* *Trous*: Les surfaces réelles sont absentes des données de mappage spatiale.
* *Hallucinations*: Des surfaces existent dans les données de mappage spatiale qui n’existent pas dans le monde réel.
* Repères: L’élément HoloLens «perd» la partie de la carte spatiale en pensant qu’il se trouve dans une autre partie de la carte qu’il ne l’est réellement.
* *Biais*: Les surfaces dans les données de mappage spatiale sont alignées de façon imparfaite avec les surfaces réelles, push dans ou extraites.

La plupart de ces erreurs peuvent être atténuées en [supprimant vos hologrammes](environment-considerations-for-hololens.md) et en remappant l’espace.