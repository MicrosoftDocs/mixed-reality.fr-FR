---
title: Tutoriel Azure Spatial Anchors - 1. Introduction
description: Suivez ce cours pour découvrir comment implémenter Azure Spatial Anchors dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: f273c573d40b1e65e325bd31b5dd9e14c1ee66ec
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376551"
---
# <a name="1-introduction"></a>1. Introduction

## <a name="overview"></a>Vue d’ensemble

Bienvenue dans les tutoriels Azure Spatial Anchors ! Cette série de tutoriels vous apprend les notions de base d’<a href="https://azure.microsoft.com/services/spatial-anchors" target="_blank">Azure Spatial Anchors</a> (ASA) et vous explique comment ancrer une expérience de réalité mixte complète dans le monde réel. Vous verrez également comment déployer votre projet sur Android et iOS.

Tutoriels de cette série :

1. [Introduction](mr-learning-asa-01.md)
2. [Bien démarrer avec Azure Spatial Anchors](mr-learning-asa-02.md)
3. [Enregistrement, récupération et partage d’ancres spatiales Azure](mr-learning-asa-03.md)
4. [Affichage du feedback Azure Spatial Anchors](mr-learning-asa-04.md)
5. [Azure Spatial Anchors pour Android et iOS](mr-learning-asa-05.md)

## <a name="objectives"></a>Objectifs

* Apprendre à créer des ancres spatiales et à les récupérer à partir d’Azure
* Apprendre à obtenir un alignement spatial entre plusieurs sessions d’application
* Apprendre à obtenir un alignement spatial entre plusieurs appareils
* Apprendre à préparer, générer et déployer votre projet sur Android et iOS

## <a name="prerequisites"></a>Prérequis

* Ordinateur Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)
* SDK Windows 10 10.0.18362.0 ou ultérieur
* Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)
* <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.3.15 installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté
* Avoir suivi la section [Créer une ressource d’ancres spatiales](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) du tutoriel [Démarrage rapide : Créer une application HoloLens Unity qui utilise Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens).
* Avoir suivi la série de [tutoriels de démarrage](mr-learning-base-01.md) ou avoir une expérience de base avec Unity et MRTK
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
> La version Unity recommandée pour cette série de tutoriels est Unity 2019.3.15. Elle remplace toutes les versions Unity requises qui sont indiquées dans les prérequis ci-dessus.

[Tutoriel suivant : 2. Bien démarrer avec les ancres spatiales Azure](mr-learning-asa-02.md)
