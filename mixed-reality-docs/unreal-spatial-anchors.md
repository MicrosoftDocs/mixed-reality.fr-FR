---
title: Ancres spatiales dans Unreal
description: Guide d’utilisation des ancres spatiales dans Unreal
author: sw5813
ms.author: jacksonf
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, ancres spatiales
ms.openlocfilehash: c35d8efc9998aac5b40de833e5acbf7f80353e6b
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82840138"
---
# <a name="spatial-anchors-in-unreal"></a>Ancres spatiales dans Unreal

Les ancres spatiales sont utilisées pour conserver les hologrammes en place dans l’espace réel entre les sessions d’application.  Elles sont exposées via Unreal sous forme d’ARPins et sont enregistrées dans le magasin d’ancres HoloLens en vue de leur chargement dans les sessions ultérieures. 

Avant d’enregistrer ou de charger des ancres, vérifiez que le magasin d’ancres est prêt.  Toute tentative d’appel d’une des fonctions d’ancrage HoloLens échouera si le magasin d’ancres n’est pas prêt.  

![Magasin d’ancres spatiales prêt](images/unreal-spatialanchors-store-ready.PNG)

## <a name="save-anchors"></a>Enregistrer des ancres

Quand l’application a un composant qui doit être relié au monde réel, ce composant peut être enregistré dans le magasin d’ancres avec la séquence suivante : 

![Enregistrer des ancres spatiales](images/unreal-spatialanchors-save.PNG)

Ici, nous générons un acteur à une position connue, nous créons un ARPin avec cette position et un nom basé sur la classe de l’acteur, nous ajoutons l’acteur à l’ARPin et nous enregistrons la broche dans le magasin d’ancres HoloLens.  Nous devons choisir un nom d’ancre unique. C’est pourquoi, dans cet exemple, nous ajoutons l’horodatage actuel.  Une fois que l’ancre a été enregistrée dans le magasin d’ancres, elle est visible dans le portail d’appareil pour HoloLens sous System > Map Manager > Anchor Files Saved On Device. 

## <a name="load-anchors"></a>Charger des ancres

Au démarrage d’une application, le Blueprint ci-dessous peut être appelé pour rétablir les composants à leurs positions d’ancrage :

![Charger des ancres spatiales](images/unreal-spatialanchors-load.PNG)

Dans cet exemple, nous faisons une itération sur toutes les ancres du magasin d’ancres, nous générons un acteur au niveau de l’identité et nous relions cet acteur à l’ARPin à partir du magasin d’ancres.  Il est important de générer l’acteur au niveau de l’identité, car comme l’ancre repositionne l’hologramme dans le monde réel en fonction de son emplacement d’enregistrement, si une transformation est ajoutée ici, un décalage sera ajouté à l’ancre. 

L’ID de l’ancre est également demandé afin que différents acteurs puissent être générés en fonction du nom enregistré de l’ancre. 

## <a name="remove-anchors"></a>Supprimer des ancres 

Lorsque vous n’avez plus besoin d’une ancre, vous pouvez supprimer tout le contenu du magasin d’ancres, ou supprimer individuellement les ancres du magasin que vous ne souhaitez pas inclure dans les sessions ultérieures : 

![Supprimer des ancres spatiales](images/unreal-spatialanchors-remove.PNG)

## <a name="see-also"></a>Voir aussi
* [Ancres spatiales](spatial-anchors.md)
* [Systèmes de coordonnées](coordinate-systems.md)
