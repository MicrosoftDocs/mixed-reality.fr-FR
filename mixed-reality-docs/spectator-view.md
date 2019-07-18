---
title: Vue spectateur
description: Visualisez des hologrammes à partir d’un appareil externe pour illustrer une expérience de réalité mixte sur un affichage externe ou une vidéo d’enregistrement d’une expérience de réalité mixte.
author: chrisfromwork
ms.author: chriba
ms.date: 02/11/2019
ms.topic: article
keywords: Vue spectateur, iPhone, iOS, iPad, OpenCV, Camera, ARKit, HoloLens, realer, MixedRealityToolkit, Demo, record
ms.openlocfilehash: 02088d7b218a25c72f2eb98ae24c85a90e6e5b86
ms.sourcegitcommit: 611af6ff7a2412abad80c0c7d4decfc0c3a0e8c8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/17/2019
ms.locfileid: "68293607"
---
# <a name="spectator-view-for-hololens-and-hololens-2"></a>Vue spectateur pour HoloLens et HoloLens 2

![Marker](images/SpecViewPhoneHero.jpg)

## <a name="overview"></a>Vue d'ensemble

Lors de l’ajout d’un HoloLens, nous oublions souvent qu’une personne qui ne l’a pas n’est pas en mesure de découvrir les merveilles que nous pouvons. La vue spectateur permet à d’autres utilisateurs de voir sur un écran 2D ce qu’un utilisateur HoloLens voit dans son monde.
La vue spectateur offre une approche rapide et abordable pour l’enregistrement d’hologrammes en HD avec des appareils mobiles. Il offre également un enregistrement de qualité professionnelle des hologrammes avec les caméras DSLR.

## <a name="key-resources"></a>Ressources clés

* [**Vue spectateur sur GitHub**](https://github.com/microsoft/MixedReality-SpectatorView)
* [**SOA**](https://github.com/microsoft/MixedReality-SpectatorView/blob/master/doc/SpectatorView.Architecture.md)
* [**Extraits**](https://github.com/microsoft/MixedReality-SpectatorView/tree/master/samples)
* [**Instructions d’installation de mobile**](https://github.com/microsoft/MixedReality-SpectatorView/blob/master/doc/SpectatorView.Setup.md)
* [**Instructions d’installation de DSLR**](https://github.com/microsoft/MixedReality-SpectatorView/blob/master/doc/SpectatorView.Setup.DSLR.md)

## <a name="use-cases"></a>Cas d’usage
* Vous pouvez enregistrer une expérience de réalité mixte à l’aide d’un appareil iPhone ou Android. Enregistrez en HD entièrement et appliquez l’anticrénelage aux hologrammes et même aux ombres. Il s’agit d’un moyen économique et rapide de capturer la vidéo des hologrammes.
* Diffusez des expériences de réalité mixte en direct sur un téléviseur Apple directement à partir de votre iPhone ou iPad, sans tarder!
* Partagez l’expérience avec les invités: Laissez les utilisateurs non-HoloLens expérimenter des hologrammes directement à partir de leurs téléphones ou tablettes.

## <a name="current-features"></a>Fonctionnalités actuelles

* La synchronisation spatiale des hologrammes, afin de permettre à tout le monde de voir les hologrammes exactement dans le même emplacement.
* prise en charge d’iOS (appareils compatibles ARKit) et des appareils Android (ARCore).
Plusieurs invités iOS.
Enregistrement de vidéos + hologrammes + son ambiant + son d’hologramme.
Partager la feuille pour pouvoir enregistrer la vidéo, la envoyer par courrier électronique ou partager avec d’autres applications de prise en charge.

![Marqueur de marqueur](images/SpecViewPhoneDemo.jpg)
![](images/hololensspectatorview-500px.jpg) ![](images/spectatorview-300px.png)

Le tableau suivant présente différentes fonctionnalités de vue de spectateur et leurs fonctionnalités. Choisissez l’option qui correspond le mieux à vos besoins d’enregistrement vidéo:

|                                      | Mobile                  |                    Appareil photo DSLR              |
|--------------------------------------|:-----------------------:|:-------------------------------------------:|
| Qualité HD                           |         Full HD         |        Filming de qualité professionnelle (tel que déterminé par DSLR)      |
| Mouvement facile de l’appareil photo                 |            ✔            |                      ✔                      |
| Vue de la troisième personne                    |            ✔            |                      ✔                      |
| Peut être diffusé en continu vers des écrans           |            ✔            |                      ✔                      |
| Portatif                             |            ✔            |                                             |
| Sans fil                             |            ✔            |                                             |
| Matériel supplémentaire requis         |     Téléphone Android, iPhone    | HoloLens + plate-forme + trépied + DSLR + PC + Unity |
| Investissement matériel                  |           Faible            |                     Élevé                    |
| Système multiplateforme                       |           Android, iOS   |                                             |
| Contenu synchronisé                 |            ✔            |                      ✔                      |
| Durée d’installation du Runtime               |         Messagerie          |                     Lent                    |
## <a name="see-also"></a>Voir aussi

* [Capture de Réalité Mixte](mixed-reality-capture.md) 
* [Capture de Réalité Mixte pour les développeurs](mixed-reality-capture-for-developers.md)
* [Expériences partagées dans Mixed Reality](shared-experiences-in-mixed-reality.md)
