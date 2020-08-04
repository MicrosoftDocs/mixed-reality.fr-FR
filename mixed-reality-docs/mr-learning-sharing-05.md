---
title: Tutoriels sur les fonctionnalités multi-utilisateurs - 5. Intégration d’Azure Spatial Anchors dans une expérience partagée
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: fc8e20a9ddaa595db0a3d59975e7c785d01c0a6d
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376581"
---
# <a name="5-integrating-azure-spatial-anchors-into-a-shared-experience"></a>5. Intégration d’Azure Spatial Anchors dans une expérience partagée

Dans ce tutoriel, vous allez apprendre à intégrer Azure Spatial Anchors (ASA) à l’expérience partagée. ASA permet à plusieurs appareils d’avoir une référence commune au monde physique pour que les utilisateurs se voient à leur emplacement physique réel et voient l’expérience partagée au même endroit.

## <a name="objectives"></a>Objectifs

* Intégrer ASA à une expérience partagée pour l’alignement de plusieurs appareils
* Découvrir les principes de base du fonctionnement d’ASA dans le contexte d’une expérience partagée locale

## <a name="preparing-the-scene"></a>Préparation de la scène

Dans la fenêtre Hierarchy, développez l’objet **SharedPlayground**, puis l’objet **TableAnchor** pour exposer ses objets enfants :

![mr-learning-sharing](images/mr-learning-sharing/sharing-05-section1-step1-1.png)

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.MultiUserCapabilities** > **Prefabs**, puis faites glisser le préfabriqué **Buttons** sur l’objet enfant **TableAnchor** afin de l’ajouter à votre scène en tant qu’enfant de l’objet TableAnchor :

![mr-learning-sharing](images/mr-learning-sharing/sharing-05-section1-step1-2.png)

## <a name="configuring-the-buttons-to-operate-the-scene"></a>Configuration des boutons pour faire fonctionner la scène

Dans cette section, vous allez configurer une série d’événements de bouton qui illustrent les principes de base d’Azure Spatial Anchors pour obtenir un alignement spatial dans une expérience partagée.

Dans la fenêtre Hierarchy, développez l’objet **Button** et sélectionnez le premier bouton enfant nommé **StartAzureSession** :

![mr-learning-sharing](images/mr-learning-sharing/sharing-05-section2-step1-1.png)

Dans la fenêtre Inspector, localisez le composant **Interactable (Script)** et configurez l’événement **OnClick ()** comme suit :

* Affectez au champ **None (Object)** l’objet **TableAnchor**.
* Dans la liste déroulante **No Function**, sélectionnez la fonction **AnchorModuleScript** > **StartAzureSession ()** .

![mr-learning-sharing](images/mr-learning-sharing/sharing-05-section2-step1-2.png)

Dans la fenêtre Hierarchy, sélectionnez le deuxième objet bouton enfant nommé **CreateAzureAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Interactable (Script)** et configurez l’événement **OnClick ()** comme suit :

* Affectez au champ **None (Object)** l’objet **TableAnchor**.
* Dans la liste déroulante **No Function**, sélectionnez la fonction **AnchorModuleScript** > **CreateAzureAnchor ()** .
* Affectez au nouveau champ **None (Game Object)** qui apparaît l’objet **TableAnchor**.

![mr-learning-sharing](images/mr-learning-sharing/sharing-05-section2-step1-3.png)

Dans la fenêtre Hierarchy, sélectionnez le troisième objet bouton enfant nommé **ShareAzureAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Interactable (Script)** et configurez l’événement **OnClick ()** comme suit :

* Affectez au champ **None (Object)** l’objet **TableAnchor**.
* Dans la liste déroulante **No Function**, sélectionnez la fonction **SharingModuleScript** > **ShareAzureAnchor ()** .

![mr-learning-sharing](images/mr-learning-sharing/sharing-05-section2-step1-4.png)

Dans la fenêtre Hierarchy, sélectionnez le quatrième objet bouton enfant nommé **GetAzureAnchor**. Ensuite, dans la fenêtre Inspector, localisez le composant **Interactable (Script)** et configurez l’événement **OnClick ()** de la façon suivante :

* Affectez au champ **None (Object)** l’objet **TableAnchor**.
* Dans la liste déroulante **No Function**, sélectionnez la fonction **SharingModuleScript** > **GetAzureAnchor ()** .

![mr-learning-sharing](images/mr-learning-sharing/sharing-05-section2-step1-5.png)

## <a name="connecting-the-scene-to-the-azure-resource"></a>Connexion de la scène à la ressource Azure

Dans la fenêtre Hierarchy, développez l’objet **SharedPlayground**, puis sélectionnez l’objet **TableAnchor**.

Dans la fenêtre Inspector, localisez le composant **Spatial Anchor Manager (Script)** et configurez la section **Credentials** avec les informations d’identification du compte Azure Spatial Anchors créé dans le cadre des [prérequis](mr-learning-sharing-01.md#prerequisites) pour cette série de tutoriels :

* Dans le champ **Spatial Anchors Account ID**, collez la valeur **Account ID** de votre compte Azure Spatial Anchors.
* Dans le champ **Spatial Anchors Account Key**, collez la valeur **Access Key** (primaire ou secondaire) de votre compte Azure Spatial Anchors.

![mr-learning-sharing](images/mr-learning-sharing/sharing-05-section3-step1-1.png)

> [!TIP]
> Au lieu de définir l’ID et la clé du compte Spatial Anchors dans la scène, vous pouvez les définir pour l’ensemble du projet, ce qui peut être avantageux si plusieurs de vos scènes utilisent Azure Spatial Anchors. Pour ce faire, dans la fenêtre Project, accédez à la ressource Assets > AzureSpatialAnchors.SDK > Resources > **SpatialAnchorConfig**, puis définissez les valeurs dans la fenêtre Inspector.

Dans la fenêtre Hierarchy, sélectionnez l’objet **TableAnchor** puis, dans la fenêtre Inspector, localisez le composant **Anchor Module (Script)** et configurez-le de la façon suivante :

* Dans le champ **Public Sharing Pin** (Code secret du partage public), modifiez quelques chiffres afin que le code secret devienne unique pour votre projet.

![mr-learning-sharing](images/mr-learning-sharing/sharing-05-section3-step1-2.png)

L’objet **TableAnchor** étant toujours sélectionné, vérifiez que tous les composants de script sont activés (**enabled**) dans la fenêtre Inspector :

* Cochez la case en regard du composant **Spatial Anchor Manager (Script)** pour l’activer.
* Cochez la case en regard du composant **Anchor Module Script (Script)** pour l’activer.
* Cochez la case en regard du composant **Sharing Module Script (Script)** pour l’activer.

![mr-learning-sharing](images/mr-learning-sharing/sharing-05-section3-step1-3.png)

## <a name="trying-the-experience-with-spatial-alignment"></a>Essai de l’expérience avec l’alignement spatial

> [!NOTE]
> Azure Spatial Anchors ne peut pas s’exécuter dans Unity. Pour tester la fonctionnalité Azure Spatial Anchors, vous devez donc déployer le projet sur au moins deux appareils.

Si vous générez et déployez le projet Unity sur deux appareils, vous pouvez obtenir un alignement spatial entre eux en partageant l’ID d’ancre Azure. Pour le tester, vous pouvez effectuer ces étapes :

1. Sur l’appareil 1 : **Démarrez l’application** (le Rover Explorer est instancié et placé dans la table).
2. Sur l’appareil 2 : **Démarrez l’application** (les deux utilisateurs voient la table avec le Rover Explorer, mais la table ne s’affiche pas au même endroit et les avatars des utilisateurs ne s’affichent pas là où se trouvent les utilisateurs).
3. Sur l’appareil 1 : Appuyez sur le bouton **Start Azure Session**.
4. Sur l’appareil 1 : Appuyez sur le bouton **Create Azure Anchor** (crée une ancre à l’emplacement de l’objet TableAnchor et stocke les informations d’ancrage dans la ressource Azure).
5. Sur l’appareil 1 : Appuyez sur le bouton **Share Azure Anchor** (partage l’ID d’ancre avec d’autres utilisateurs en temps réel).
6. Sur l’appareil 2 : Appuyez sur le bouton **Start Azure Session**.
7. Sur l’appareil 2 : Appuyez sur le bouton **Get Azure Anchor** (se connecte à la ressource Azure pour récupérer les informations d’ancrage de l’ID d’ancre partagé, puis déplace l’objet TableAnchor à l’emplacement où l’ancre a été créée avec l’appareil 1).

> [!TIP]
> Si vous n’avez pas accès à deux appareils HoloLens, suivez les instructions fournies dans [Création d’ancres spatiales Azure pour les appareils mobiles](mr-learning-asa-05.md) afin de déployer le projet sur votre appareil mobile.

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez appris à intégrer des ancres spatiales, une fonctionnalité puissante d’Azure, pour aligner des appareils dans une expérience partagée.

Ainsi se conclut cette série de tutoriels où vous avez appris à configurer un compte Photon, à créer une application PUN, à intégrer PUN dans une application Unity, à configurer des avatars d’utilisateurs et des objets partagés, et enfin à aligner plusieurs participants à l’aide d’Azure Spatial Anchors.
