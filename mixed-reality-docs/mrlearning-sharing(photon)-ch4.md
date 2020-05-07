---
title: Tutoriels sur les fonctionnalités multi-utilisateurs - 5. Intégration d’Azure Spatial Anchors dans une expérience partagée
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: c27ed7327cfe0a61f2b63e309348bdea1a535ea1
ms.sourcegitcommit: 92ff5478a5c55b4e2c5cc2f44f1588702f4ec5d1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82604970"
---
# <a name="4-integrating-azure-spatial-anchors-into-a-shared-experience"></a>4. Intégration d’Azure Spatial Anchors dans une expérience partagée

Dans ce tutoriel, vous allez apprendre à intégrer Azure Spatial Anchors (ASA) à l’expérience partagée. ASA permet à plusieurs appareils d’avoir une référence commune au monde physique pour que les utilisateurs se voient à leur emplacement physique réel et voient l’expérience partagée au même endroit.

## <a name="objectives"></a>Objectifs

* Intégrer ASA à une expérience partagée pour l’alignement de plusieurs appareils
* Découvrir les principes de base du fonctionnement d’ASA dans le contexte d’une expérience partagée locale

## <a name="preparing-the-scene"></a>Préparation de la scène

Dans la fenêtre Hierarchy, développez l’objet **SharedPlayground**, puis l’objet **TableAnchor** pour exposer ses objets enfants :

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section1-step1-1.png)

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs**, puis faites glisser le préfabriqué **Buttons** sur l’objet **TableAnchor** dans la fenêtre Hierarchy pour l’ajouter à votre scène en tant qu’enfant de l’objet TableAnchor :

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section1-step1-2.png)

## <a name="configuring-the-buttons-to-operate-the-scene"></a>Configuration des boutons pour faire fonctionner la scène

Dans cette section, vous allez configurer une série d’événements de bouton qui illustrent les principes de base d’Azure Spatial Anchors pour obtenir un alignement spatial dans une expérience partagée.

Dans la fenêtre Hierarchy, développez l’objet **Button** et sélectionnez le premier bouton enfant nommé **StartAzureSession** :

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section2-step1-1.png)

Dans la fenêtre Inspector, localisez le composant **Interactable (Script)** et configurez l’événement **OnClick ()** comme suit :

* Affectez à **None (Object)** l’objet **TableAnchor**.
* Dans la liste déroulante **No Function**, sélectionnez la fonction **AnchorModuleScript** > **StartAzureSession ()** .

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section2-step1-2.png)

Dans la fenêtre Hierarchy, sélectionnez le deuxième objet bouton enfant nommé **CreateAzureAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Interactable (Script)** et configurez l’événement **OnClick ()** comme suit :

* Affectez au champ **None (Object)** l’objet **TableAnchor**.
* Dans la liste déroulante **No Function**, sélectionnez la fonction **AnchorModuleScript** > **CreateAzureAnchor ()** .
* Affectez au nouveau champ **None (Game Object)** qui apparaît l’objet **TableAnchor**.

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section2-step1-3.png)

Dans la fenêtre Hierarchy, sélectionnez le troisième objet bouton enfant nommé **ShareAzureAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Interactable (Script)** et configurez l’événement **OnClick ()** comme suit :

* Affectez au champ **None (Object)** l’objet **TableAnchor**.
* Dans la liste déroulante **No Function**, sélectionnez la fonction **SharingModuleScript** > **ShareAzureAnchor ()** .

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section2-step1-4.png)

Dans la fenêtre Hierarchy, sélectionnez le quatrième objet bouton enfant nommé **GetAzureAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Interactable (Script)** et configurez l’événement **OnClick ()** comme suit :

* Affectez au champ **None (Object)** l’objet **TableAnchor**.
* Dans la liste déroulante **No Function**, sélectionnez la fonction **SharingModuleScript** > **GetAzureAnchor ()** .

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section2-step1-5.png)

## <a name="connecting-the-scene-to-the-azure-resource"></a>Connexion de la scène à la ressource Azure

Dans la fenêtre Hierarchy, développez l’objet **SharedPlayground**, puis sélectionnez l’objet **TableAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Spatial Anchor Manager (Script)** et configurez la section **Credentials** avec les informations d’identification du compte Azure Spatial Anchors créé dans le cadre des [prérequis](mrlearning-sharing(photon)-ch1.md#prerequisites) pour cette série de tutoriels :

* Dans le champ **Spatial Anchors Account ID**, collez la valeur **Account ID** de votre compte Azure Spatial Anchors.
* Dans le champ **Spatial Anchors Account Key**, collez la valeur **Access Key** (primaire ou secondaire) de votre compte Azure Spatial Anchors.

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section3-step1-1.png)

L’objet **TableAnchor** étant toujours sélectionné, vérifiez que tous les composants de script sont activés dans la fenêtre Inspector :

* Cochez la case en regard du composant **Spatial Anchor Manager (Script)** pour l’activer.
* Cochez la case en regard du composant **Anchor Module Script (Script)** pour l’activer.
* Cochez la case en regard du composant **Sharing Module Script (Script)** pour l’activer.

![mrlearning-sharing](images/mrlearning-sharing/tutorial4-section3-step1-2.png)

## <a name="trying-the-experience-with-spatial-alignment"></a>Essai de l’expérience avec l’alignement spatial

> [!NOTE]
> Azure Spatial Anchors ne peut pas s’exécuter dans Unity. Pour tester la fonctionnalité Azure Spatial Anchors, vous devez donc déployer le projet sur au moins deux appareils HoloLens.

Si vous générez et déployez le projet Unity sur deux appareils HoloLens, vous pouvez obtenir un alignement spatial entre eux en partageant l’ID d’ancre Azure. Pour le tester, vous pouvez effectuer ces étapes :

1. Sur l’appareil HoloLens 1 : **Démarrez l’application** (le Rocket Launcher est instancié et placé sur la table).
2. Sur l’appareil HoloLens 2 : **Démarrez l’application** (les deux utilisateurs voient la table avec le Rocket Launcher, mais la table n’apparaît pas au même endroit et les avatars des utilisateurs n’apparaissent pas là où se trouvent les utilisateurs).
3. Sur l’appareil HoloLens 1 : Appuyez sur le bouton **Start Azure Session**.
4. Sur l’appareil HoloLens 1 : Appuyez sur le bouton **Create Azure Anchor** (crée une ancre à l’emplacement de l’objet TableAnchor et stocke les informations d’ancrage dans la ressource Azure).
5. Sur l’appareil HoloLens 1 : Appuyez sur le bouton **Share Azure Anchor** (partage l’ID d’ancre avec d’autres utilisateurs en temps réel).
6. Sur l’appareil HoloLens 2 : Appuyez sur le bouton **Start Azure Session**.
7. Sur l’appareil HoloLens 2 : Appuyez sur le bouton **Get Azure Anchor** (se connecte à la ressource Azure pour récupérer les informations d’ancrage de l’ID d’ancre partagé, puis déplace l’objet TableAnchor à l’emplacement où l’ancre a été créée avec l’appareil HoloLens 1)

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez appris à intégrer des ancres spatiales, une fonctionnalité puissante d’Azure, pour aligner des appareils dans une expérience partagée. Ainsi se conclut cette série de tutoriels où vous avez appris à configurer un compte et une application Photon, à intégrer Photon et PUN dans une application Unity, à configurer des avatars d’utilisateurs et des objets partagés, et enfin à aligner plusieurs participants à l’aide d’ASA.
