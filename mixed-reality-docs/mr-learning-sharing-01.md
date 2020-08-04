---
title: Tutoriels sur les fonctionnalités multiutilisateurs - 1. Introduction
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: ebdef9818aace28b32e91384cd9d3278da2733b4
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376341"
---
# <a name="1-introduction"></a>1. Introduction

## <a name="overview"></a>Vue d’ensemble

Bienvenue dans les tutoriels sur les fonctionnalités multiutilisateurs ! Dans cette série de tutoriels, vous allez apprendre les bases de la création d’une expérience multiutilisateur à l’aide de <a href="https://www.photonengine.com/PUN" target="_blank">Photon Unity Networking</a> (PUN). PUN est l’une des nombreuses options de réseau que peuvent utiliser les développeurs de réalité mixte pour créer des expériences partagées.

Tutoriels de cette série :

* [Configuration de Photon Unity Networking](mr-learning-sharing-02.md)
* [Connexion de plusieurs utilisateurs](mr-learning-sharing-03.md)
* [Partage de mouvements d’objet avec plusieurs utilisateurs](mr-learning-sharing-04.md)
* [Intégration d’Azure Spatial Anchors dans une expérience partagée](mr-learning-sharing-05.md)

## <a name="objectives"></a>Objectifs

* Apprendre à créer une application PUN et y connecter votre projet Unity
* Apprendre à connecter plusieurs utilisateurs dans un environnement partagé
* Apprendre à partager les mouvements d’objets avec d’autres utilisateurs
* Apprendre à obtenir un alignement spatial entre plusieurs appareils

## <a name="prerequisites"></a>Prérequis

* Ordinateur Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)
* SDK Windows 10 (10.0.18362.0 ou version ultérieure)
* Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)
* <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.3.15 installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté
* Avoir suivi la section [Créer une ressource d’ancres spatiales](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) du tutoriel [Démarrage rapide : Créer une application HoloLens Unity qui utilise Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens).
* Avoir suivi la série de [tutoriels de démarrage](mr-learning-base-01.md) ou connaître les fondamentaux d’Unity et de MRTK
* Avoir suivi la série de [tutoriels sur Azure Spatial Anchors](mr-learning-asa-01.md) ou avoir déjà créé des comptes Azure Spatial Anchors
* Si vous envisagez d’effectuer un déploiement à la fois sur Android et sur HoloLens :
  * Appareil Android <a href="https://developer.android.com/studio/debug/dev-options" target="_blank">en mode développeur</a> et <a href="https://developers.google.com/ar/discover/supported-devices" target="_blank">compatible avec ARCore</a> disposant d’une connexion USB à votre ordinateur Windows ou macOS
  * <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.3.15 installé et le module Android Build Support ajouté
* Si vous envisagez d’effectuer un déploiement à la fois sur iOS et sur HoloLens :
  * Ordinateur macOS avec les dernières versions de <a href="https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12" target="_blank">Xcode</a> et de <a href="https://cocoapods.org" target="_blank">CocoaPods</a> installées
  * Appareil iOS <a href="https://developer.apple.com/documentation/arkit/verifying_device_support_and_user_permission" target="_blank">compatible avec ARKit</a> disposant d’une connexion USB à votre ordinateur macOS
  * <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.3.15 installé et le module iOS Build Support ajouté

> [!CAUTION]
> La version de Mixed Reality Toolkit qui est recommandée pour cette série de tutoriels est MRTK 2.4.0.

> [!CAUTION]
> La version Unity recommandée pour cette série de tutoriels est Unity 2019.3.15. Cela remplace toutes les exigences de version Unity énoncées dans les prérequis indiqués ci-dessus.

[Tutoriel suivant : 2. Configuration du réseau Photon Unity](mr-learning-sharing-02.md)
