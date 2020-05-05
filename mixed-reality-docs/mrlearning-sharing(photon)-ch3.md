---
title: Tutoriels sur les fonctionnalités multi-utilisateurs - 4. Partage de mouvements d’objet avec plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 41b62eb2d9f400d0af341c9fcce887c72af7a3aa
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "81610616"
---
# <a name="3-sharing-object-movements-with-multiple-users"></a>3. Partage de mouvements d’objet avec plusieurs utilisateurs

Dans ce tutoriel, vous allez apprendre à partager les mouvements d’objets pour que tous les participants d’une expérience partagée puissent collaborer et voir leurs interactions.

## <a name="objectives"></a>Objectifs

* Configurer votre projet pour partager les mouvements d’objets
* Apprendre à créer une application collaborative multi-utilisateur de base

## <a name="preparing-the-scene"></a>Préparation de la scène

Dans cette section, vous allez préparer la scène en ajoutant le préfabriqué du tutoriel.

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs**, puis faites glisser le préfabriqué **TableAnchor** sur l’objet **SharedPlayground** dans la fenêtre Hierarchy pour l’ajouter à votre scène en tant qu’enfant de l’objet SharedPlayground :

![mrlearning-sharing](images/mrlearning-sharing/tutorial3-section1-step1-1.png)

## <a name="configuring-pun-to-instantiate-the-objects"></a>Configuration de PUN pour instancier les objets

Dans cette section, vous allez configurer le projet pour qu’il utilise le préfabriqué RocketLauncher_Complete_Variant créé dans la section précédente et définir où il sera instancié.

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources**.

Dans la fenêtre Hierarchy, développez l’objet **NetworkLobby** et sélectionnez l’objet enfant **NetworkRoom**. Ensuite, dans la fenêtre Inspector, localisez le composant **Photon Room (Script)** et configurez-le comme suit :

* Affectez au champ **Photon User Prefab** le préfabriqué **PhotonUser** du dossier Resources.

![mrlearning-sharing](images/mrlearning-sharing/tutorial3-section2-step1-1.png)

L’objet enfant **NetworkRoom** étant toujours sélectionné, dans la fenêtre Hierarchy, développez l’objet **TableAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Photon Room (Script)** et configurez-le comme suit :

* Affectez au champ **Rocket Launcher Location** l’objet enfant **Table** à partir de la fenêtre Hierarchy.

![mrlearning-sharing](images/mrlearning-sharing/tutorial3-section2-step1-2.png)

## <a name="trying-the-experience-with-shared-object-movement"></a>Essai de l’expérience avec le mouvement d’objet partagé

Vous pouvez à présent générer le projet Unity et le déployer sur votre HoloLens. De retour dans Unity, si vous appuyez sur le bouton Play pour passer en mode Game pendant que l’application s’exécute sur votre HoloLens, vous voyez l’objet se déplacer dans Unity quand vous le déplacez dans HoloLens :

![mrlearning-sharing](images/mrlearning-sharing/tutorial3-section3-step1-1.gif)

## <a name="congratulations"></a>Félicitations

Vous venez de configurer votre projet pour synchroniser les mouvements d’objet. Les utilisateurs peuvent ainsi voir les objets se déplacer quand d’autres utilisateurs les déplacent. Dans le tutoriel suivant, vous allez implémenter des fonctionnalités pour aligner l’expérience partagée dans le monde physique, permettre aux utilisateurs de se voir à leur emplacement physique réel et faire en sorte que la position physique et la rotation des objets soient identiques pour tous les utilisateurs.

[Tutoriel suivant : 4. Intégration d’ancres spatiales Azure dans une expérience partagée](mrlearning-sharing(photon)-ch4.md)
