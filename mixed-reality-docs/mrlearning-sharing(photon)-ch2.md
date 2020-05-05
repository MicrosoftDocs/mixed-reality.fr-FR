---
title: Tutoriels sur les fonctionnalités multiutilisateurs - 3. Connexion de plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multiutilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: a597aadbddb49fefc824d8c5b5193585fa9476a5
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "81610953"
---
# <a name="2-connecting-multiple-users"></a>2. Connexion de plusieurs utilisateurs

Dans ce tutoriel, vous allez apprendre à connecter plusieurs utilisateurs dans le cadre d’une expérience partagée en direct. À la fin du tutoriel, vous pourrez exécuter l’application sur plusieurs appareils et chaque utilisateur pourra voir l’avatar d’autres utilisateurs se déplacer en temps réel.

## <a name="objectives"></a>Objectifs

* Découvrir comment connecter plusieurs utilisateurs dans un environnement partagé

## <a name="preparing-the-scene"></a>Préparation de la scène

Dans cette section, vous allez préparer la scène en ajoutant une partie des préfabriqués du tutoriel.

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs**. Tout en maintenant le bouton Ctrl enfoncé, cliquez sur **DebugWindow**, **NetworkLobby** et **SharedPlayground** pour sélectionner les trois préfabriqués :

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section1-step1-1.png)

Les trois préfabriqués étant sélectionnés, faites-les glisser dans la fenêtre Hierarchy pour les ajouter à la scène :

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section1-step1-2.png)

## <a name="creating-the-user-prefab"></a>Création du préfabriqué utilisateur

Dans cette section, vous allez créer un préfabriqué qui sera utilisé pour représenter les utilisateurs dans l’expérience partagée.

### <a name="1-create-and-configure-the-user"></a>1. Créer et configurer l’utilisateur

Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur une zone vide et sélectionnez **Create Empty** pour ajouter un objet vide à votre scène, nommez l’objet **PhotonUser**, puis configurez-le comme suit :

* Vérifiez que le paramètre **Position** de Transform a les valeurs X = 0, Y = 0, Z = 0 :

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step1-1.png)

L’objet **PhotonUser** étant toujours sélectionné, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Photon User (Script)** à l’objet PhotonUser :

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step1-2.png)

Dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Generic Net Sync (Script)** à l’objet PhotonUser et configurez-le comme suit :

* Cochez la case **Is User**.

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step1-3.png)

Dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Photon View (Script)** à l’objet PhotonUser et configurez-le comme suit :

* Affectez au champ **Observed Components** le composant Generic Net Sync (Script).

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step1-4.png)

### <a name="2-create-the-avatar"></a>2. Créer l’avatar

Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur l’objet **PhotonUser**, puis sélectionnez **3D Object** > **Sphere** pour créer un objet Sphere en tant qu’enfant de l’objet PhotonUser et configurez-le comme suit :

* Vérifiez que le paramètre **Position** de Transform a les valeurs X = 0, Y = 0, Z = 0.
* Changez le paramètre **Scale** de Transform en une taille appropriée, par exemple X = 0,15, Y = 0,15, Z = 0,15.

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step2-1.png)

### <a name="3-create-the-prefab"></a>3. Créer le préfabriqué

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources** :

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step3-1.png)

Le dossier Resources étant toujours sélectionné, **cliquez et faites glisser** l’objet **PhotonUser** de la fenêtre Hierarchy vers le dossier **Resources** pour transformer l’objet PhotonUser en préfabriqué :

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step3-2.png)

Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur l’objet **PhotonUser** et sélectionnez **Delete** pour le supprimer de la scène :

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section2-step3-3.png)

## <a name="configuring-pun-to-instantiate-the-user-prefab"></a>Configuration de PUN pour instancier le préfabriqué utilisateur

Dans cette section, vous allez configurer le projet pour qu’il utilise le préfabriqué PhotonUser créé dans la section précédente.

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Resources**.

Dans la fenêtre Hierarchy, développez l’objet **NetworkLobby** et sélectionnez l’objet enfant **NetworkRoom**. Ensuite, dans la fenêtre Inspector, localisez le composant **Photon Room (Script)** et configurez-le comme suit :

* Affectez au champ **Photon User Prefab** le préfabriqué **PhotonUser** du dossier Resources.

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section3-step1-1.png)

## <a name="trying-the-experience-with-multiple-users"></a>Essai de l’expérience avec plusieurs utilisateurs

Vous pouvez à présent générer le projet Unity et le déployer sur votre HoloLens. De retour dans Unity, si vous appuyez sur le bouton Play pour passer en mode Game pendant que l’application s’exécute sur votre HoloLens, vous voyez l’avatar de l’utilisateur HoloLens se déplacer quand vous bougez la tête (HoloLens) :

![mrlearning-sharing](images/mrlearning-sharing/tutorial2-section4-step1-1.gif)

> [!TIP]
> Pour un rappel de la façon de générer et déployer votre projet Unity sur HoloLens 2, vous pouvez vous référer aux instructions de [Générer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device).

> [!CAUTION]
> L’application a besoin de se connecter à Photon, donc vérifiez que votre ordinateur/appareil est connecté à Internet.

## <a name="congratulations"></a>Félicitations

Votre projet est désormais configuré pour permettre à plusieurs utilisateurs de se connecter à la même expérience et de voir leurs mouvements. Dans le tutoriel suivant, vous allez implémenter des fonctionnalités pour partager les mouvements d’objets avec plusieurs appareils.

[Tutoriel suivant : 2. Partage de mouvements d’objet avec plusieurs utilisateurs](mrlearning-sharing(photon)-ch3.md)
