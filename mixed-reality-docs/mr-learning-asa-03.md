---
title: Tutoriels Azure Spatial Anchors - 3. Enregistrement, récupération et partage d’ancres spatiales Azure
description: Suivez ce cours pour découvrir comment implémenter Azure Spatial Anchors dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 25676404a71daf41b6a5c7587fa9bed95ab813f6
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86304429"
---
# <a name="3-saving-retrieving-and-sharing-azure-spatial-anchors"></a>3. Enregistrement, récupération et partage d’ancres spatiales Azure

Dans ce tutoriel, vous allez apprendre à enregistrer des ancres spatiales Azure dans plusieurs sessions d’application en enregistrant l’ID d’ancre dans le stockage de HoloLens 2. Vous allez également apprendre à partager cet ID d’ancre avec d’autres appareils à des fins d’alignement d’ancre sur plusieurs appareils.

## <a name="objectives"></a>Objectifs

* Apprendre à obtenir un alignement spatial entre plusieurs sessions d’application
* Apprendre à obtenir un alignement spatial entre plusieurs appareils

## <a name="preparing-the-scene"></a>Préparation de la scène

Dans la fenêtre de hiérarchie, développez l’objet **ButtonParent**. Sélectionnez les **quatre derniers objets boutons enfants**. Dans la fenêtre de l’inspecteur, **cochez** la case en regard du champ de nom pour rendre tous les objets actifs.

![mr-learning-asa](images/mr-learning-asa/asa-03-section1-step1-1.png)

Dans la fenêtre de hiérarchie, sélectionnez les objets **ButtonParent**. Ensuite, dans la fenêtre de l’inspecteur, recherchez le composant **GridObjectCollection** et cliquez sur le bouton **Update Collection** pour mettre à jour la position de tous les objets enfants de l’objet **ButtonParent**.

![mr-learning-asa](images/mr-learning-asa/asa-03-section1-step1-2.png)

## <a name="persisting-azure-spatial-anchors-between-app-sessions"></a>Persistance des ancres spatiales Azure entre les sessions d’application

Dans cette section, vous allez découvrir comment enregistrer et récupérer l’ID d’ancre Azure sur le disque local HoloLens. Cela vous permettra d’interroger Azure pour obtenir le même ID d’ancre dans différentes sessions d’application. Cela permettra également de positionner les hologrammes ancrés au même emplacement que dans la session d’application précédente.

Dans la fenêtre de hiérarchie, développez l’objet **ButtonParent** et recherchez les deux boutons nommés **SaveAzureAnchorIdToDisk** et **GetAzureAnchorIdFromDisk** :

![mr-learning-asa](images/mr-learning-asa/asa-03-section2-step1-1.png)

Suivez les mêmes étapes que celles indiquées dans [Configuration des boutons pour faire fonctionner la scène](mr-learning-asa-02.md#configuring-the-buttons-to-operate-the-scene) dans le tutoriel précédent afin de configurer le composant **Interactable (Script)** sur chacun des deux boutons :

* Pour l’objet de bouton **SaveAzureAnchorIdToDisk**, affectez la fonction AnchorModuleScript > **SaveAzureAnchorIdToDisk ()** .
* Pour l’objet de bouton **GetAzureAnchorIdFromDisk**, affectez la fonction AnchorModuleScript > **GetAzureAnchorIdFromDisk ()** .

Si vous générez l’application mise à jour dans votre HoloLens, vous pouvez à présent conserver les ancres spatiales Azure entre les sessions d’application en enregistrant l’ID d’ancre Azure. Pour le tester, vous pouvez effectuer ces étapes :

1. Déplacer le Rover Explorer à l’emplacement souhaité
2. Démarrer la session Azure
3. Créer une ancre Azure (cela crée des ancres à l’emplacement du Rover Explorer)
4. Enregistrer l’ID d’ancre Azure sur le disque
5. Redémarrer l’application
6. Obtenir l’ancre Azure à partir du disque (cela charge l’ID d’ancre que vous venez d’enregistrer)
7. Démarrer la session Azure
8. Rechercher l’ancre Azure (cela positionne le Rover Explorer à l’emplacement de l’étape 3)

> [!NOTE]
> Pour redémarrer complètement l’application après avoir quitté la vue d’application immersive, fermez la fenêtre de l’application dans l’accueil réalité mixte avant de la relancer à partir du menu Démarrer. Pour plus d’informations, consultez la documentation [Utilisation d’applications sur HoloLens](https://docs.microsoft.com/hololens/holographic-home#using-apps-on-hololens).

## <a name="sharing-azure-spatial-anchors-between-devices"></a>Partage d’ancres spatiales Azure entre des appareils

Dans cette section, vous allez apprendre à partager l’ID d’ancre Azure entre plusieurs appareils. Ainsi, plusieurs appareils peuvent demander à Azure le même ID d’ancre, ce qui permet d’aligner dans l’espace des hologrammes ancrés. L’alignement spatial, c’est-à-dire le fait de voir les mêmes hologrammes au même emplacement physique entre plusieurs appareils, est primordial pour les expériences partagées locales dans HoloLens 2.

Il existe de nombreuses façons de transférer des ID d’ancre Azure entre des appareils, notamment les méthodes décrites dans la série de [tutoriels sur les fonctionnalités multiutilisateurs](mr-learning-sharing-02.md). Dans cet exemple, vous allez utiliser un service web simple pour charger et télécharger des ID d’ancre entre des appareils.

Dans la fenêtre de hiérarchie, développez l’objet **ButtonParent**.   Recherchez les deux boutons nommés **ShareAzureAnchorIdToNetwork** et **GetAzureAnchorIdFromNetwork** :

![mr-learning-asa](images/mr-learning-asa/asa-03-section3-step1-1.png)

Suivez les mêmes étapes que celles indiquées dans [Configuration des boutons pour faire fonctionner la scène](mr-learning-asa-02.md#configuring-the-buttons-to-operate-the-scene) dans le tutoriel précédent afin de configurer le composant **Interactable (Script)** sur chacun des deux boutons :

* Pour l’objet **ShareAzureAnchorIdToNetwork**, affectez la fonction AnchorModuleScript > **ShareAzureAnchorIdToNetwork ()** .
* Pour l’objet **GetAzureAnchorIdFromNetwork**, affectez la fonction AnchorModuleScript > **GetAzureAnchorIdFromNetwork ()** .

Si vous générez l’application mise à jour sur deux appareils HoloLens, vous pouvez à présent obtenir un alignement spatial en partageant l’ID d’ancre Azure. Pour le tester, vous pouvez effectuer ces étapes :

1. Sur l’appareil HoloLens 1 : Déplacez le Rover Explorer à l’emplacement souhaité.
2. Sur l’appareil HoloLens 1 : Démarrez la session Azure.
3. Sur l’appareil HoloLens 1 : Créez une ancre Azure (cela crée des ancres à l’emplacement du Rover Explorer).
4. Sur l’appareil HoloLens 1 : Partagez l’ID d’ancre Azure sur le réseau.
5. Sur l’appareil HoloLens 2 : Démarrez l’application.
6. Sur l’appareil HoloLens 2 : Obtenez l’ID d’ancre partagé à partir du réseau (cela extrait l’ID d’ancre qui vient d’être partagé de l’appareil HoloLens 1).
7. Sur l’appareil HoloLens 2 : Démarrez la session Azure.
8. Sur l’appareil HoloLens 2 : Recherchez l’ancre Azure (cela positionne le Rover Explorer à l’emplacement de l’étape 3).

> [!TIP]
> Si vous ne disposez que d’un appareil HoloLens, vous pouvez quand même tester la fonctionnalité en redémarrant l’application au lieu d’utiliser un second appareil HoloLens.

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez découvert comment conserver des ancres spatiales Azure entre les sessions d’application et les redémarrages d’application en enregistrant l’ID d’ancre spatiale Azure sur le disque local sur HoloLens. Vous avez également appris à partager des ancres spatiales Azure entre plusieurs appareils pour une expérience partagée d’hologramme statique multi-utilisateur de base.

Dans le tutoriel suivant, vous allez apprendre à offrir aux utilisateurs un retour en temps réel. Ce retour inclut des informations sur la création d’ancres, la compréhension de qualité de l’environnement, et l’état de la session Azure. Sans retour, les utilisateurs risquent de ne pas savoir si une ancre a été correctement chargée sur Azure, si la qualité de l’environnement est suffisante pour créer une ancre ou pour l’état actuel.

[Tutoriel suivant : 4. Affichage des commentaires sur les ancres spatiales Azure](mr-learning-asa-04.md)
