---
title: Tutoriels Azure Spatial Anchors - 2. Enregistrement, récupération et partage d’ancres spatiales Azure
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 36f25229469e848a3f0612a5971cc8e9381262f5
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "80362010"
---
# <a name="2-saving-retrieving-and-sharing-azure-spatial-anchors"></a>2. Enregistrement, récupération et partage d’ancres spatiales Azure

Dans ce tutoriel, vous allez apprendre à enregistrer des ancres spatiales Azure dans plusieurs sessions d’application en enregistrant l’ID d’ancre dans le stockage de HoloLens 2. Vous allez également apprendre à partager cet ID d’ancre avec d’autres appareils à des fins d’alignement d’ancre sur plusieurs appareils.

## <a name="objectives"></a>Objectifs

* Découvrir comment enregistrer et récupérer des ID d’ancre spatiale Azure sur le disque local HoloLens 2, à des fins de persistance entre des sessions d’application
* Découvrir comment partager des ID d’ancre spatiale Azure entre des utilisateurs dans un scénario à plusieurs appareils

## <a name="preparing-the-scene"></a>Préparation de la scène

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.AzureSpatialAnchors** > **Prefabs**. Tout en maintenant la touche Ctrl enfoncée, cliquez sur **ButtonParent_SaveAnchorId** et **ButtonParent_ShareAnchorId** pour sélectionner les deux préfabriqués, puis faites-les glisser dans la fenêtre Hierarchy pour les ajouter à la scène :

![mrlearning-asa](images/mrlearning-asa/tutorial2-section1-step1-1.png)

## <a name="persist-azure-anchors-between-app-sessions---save-anchor-id-to-disk"></a>Conserver les ancres Azure entre les sessions d’application - Enregistrer l’ID d’ancre sur le disque
<!-- TODO: Consider renaming to 'Persist Azure Anchors between app sessions' -->

Dans cette section, vous allez apprendre à enregistrer et à récupérer l’ID d’ancre Azure sur le disque local HoloLens 2. Vous pouvez alors demander à Azure le même ID d’ancre entre différentes sessions d’application, ce qui permet aux hologrammes ancrés d’être positionnés au même endroit que dans la session d’application précédente.

Dans la fenêtre Hierarchy, développez l’objet **ButtonParent_SaveAnchorId** qui contient deux boutons, un pour enregistrer l’ID d’ancre Azure dans le stockage HoloLens 2 et un pour récupérer l’ID enregistré sur le disque :

![mrlearning-asa](images/mrlearning-asa/tutorial2-section2-step1-1.png)

Suivez les mêmes étapes que celles indiquées dans [Configuration des boutons pour faire fonctionner la scène](mrlearning-asa-ch1.md#configuring-the-buttons-to-operate-the-scene) dans le tutoriel précédent pour configurer le composant **Pressable Button Holo Lens 2 (Script)** et le composant **Interactable (Script)** sur chacun des deux boutons :

* Pour l’objet **SaveAzureAnchorIdToDisk**, affectez la fonction AnchorModuleScript > **SaveAzureAnchorIdToDisk ()** .
* Pour l’objet **GetAzureAnchorIdFromDisk**, affectez la fonction AnchorModuleScript > **GetAzureAnchorIdFromDisk ()** .

Si vous générez l’application mise à jour dans votre HoloLens, vous pouvez à présent conserver les ancres spatiales Azure entre les sessions d’application en enregistrant l’ID d’ancre Azure. Pour le tester, vous pouvez effectuer ces étapes :

1. Déplacez l’expérience Rocket Launcher à l’endroit souhaité.
2. Démarrez la session Azure.
3. Créez une ancre Azure (cela crée des ancres à l’emplacement de l’expérience Rocket Launcher).
4. Enregistrez l’ID d’ancre Azure sur le disque.
5. Redémarrez l’application.
6. Obtenez l’ancre Azure à partir du disque (cela charge l’ID d’ancre que vous venez d’enregistrer).
7. Démarrez la session Azure.
8. Recherchez l’ancre Azure (cela positionne l’expérience Rocket Launcher à l’emplacement de l’étape 3).

> [!NOTE]
> Pour redémarrer complètement l’application après avoir quitté la vue d’application immersive, fermez la fenêtre de l’application dans l’accueil réalité mixte avant de relancer l’application à partir du menu Démarrer. Pour plus d’informations, consultez la documentation [Utilisation d’applications sur HoloLens](https://docs.microsoft.com/hololens/holographic-home#using-apps-on-hololens).

## <a name="share-azure-anchors-between-multiple-devices"></a>Partager des ancres Azure entre plusieurs appareils

Dans cette section, vous allez apprendre à partager l’ID d’ancre Azure entre plusieurs appareils. Ainsi, plusieurs appareils peuvent demander à Azure le même ID d’ancre, ce qui permet d’aligner dans l’espace des hologrammes ancrés. L’alignement spatial, c’est-à-dire le fait de voir les mêmes hologrammes au même emplacement physique entre plusieurs appareils, est primordial pour les expériences partagées locales dans le HoloLens 2.

Il existe de nombreuses façons de transférer des ID d’ancre Azure entre des appareils, notamment les méthodes décrites dans la série de [tutoriels sur les fonctionnalités multi-utilisateurs](mrlearning-sharing(photon)-ch1.md). Dans cet exemple, vous allez utiliser un service web simple pour charger et télécharger des ID d’ancre entre des appareils.

Dans la fenêtre Hierarchy, développez l’objet **ButtonParent_ShareAnchorId** qui contient deux boutons, un bouton pour charger l’ID d’ancre Azure sur le serveur web et un autre pour télécharger l’ID à partir du serveur web :

![mrlearning-asa](images/mrlearning-asa/tutorial2-section3-step1-1.png)

Suivez les mêmes étapes que celles indiquées dans [Configuration des boutons pour faire fonctionner la scène](mrlearning-asa-ch1.md#configuring-the-buttons-to-operate-the-scene) dans le tutoriel précédent pour configurer le composant **Pressable Button Holo Lens 2 (Script)** et le composant **Interactable (Script)** sur chacun des deux boutons :

* Pour l’objet **ShareAzureAnchorIdToNetwork**, affectez la fonction AnchorModuleScript > **ShareAzureAnchorIdToNetwork ()** .
* Pour l’objet **GetAzureAnchorIdFromNetwork**, affectez la fonction AnchorModuleScript > **GetAzureAnchorIdFromNetwork ()** .

Si vous générez l’application mise à jour sur deux appareils HoloLens, vous pouvez à présent obtenir un alignement spatial entre eux en partageant l’ID d’ancre Azure. Pour le tester, vous pouvez effectuer ces étapes :

1. Sur l’appareil HoloLens 1 : Déplacez l’expérience Rocket Launcher à l’endroit souhaité.
2. Sur l’appareil HoloLens 1 : Démarrez la session Azure.
3. Sur l’appareil HoloLens 1 : Créez une ancre Azure (cela crée des ancres à l’emplacement de l’expérience Rocket Launcher).
4. Sur l’appareil HoloLens 1 : Partagez l’ID d’ancre Azure sur le réseau.
5. Sur l’appareil HoloLens 2 : Démarrez l’application.
6. Sur l’appareil HoloLens 2 : Obtenez l’ID d’ancre partagé à partir du réseau (cela extrait l’ID d’ancre qui vient d’être partagé de l’appareil HoloLens 1).
7. Sur l’appareil HoloLens 2 : Démarrez la session Azure.
8. Sur l’appareil HoloLens 2 : Recherchez l’ancre Azure (cela positionne l’expérience Rocket Launcher à l’emplacement de l’étape 3).

> [!TIP]
> Si vous ne disposez que d’un HoloLens, vous pouvez quand même tester la fonctionnalité en redémarrant l’application au lieu d’utiliser un second appareil HoloLens.

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez appris à conserver des ancres spatiales Azure entre les sessions d’application et les redémarrages d’application en enregistrant l’ID d’ancre spatiale Azure sur le disque local sur HoloLens. Vous avez également appris à partager des ancres spatiales Azure entre plusieurs appareils pour une expérience partagée d’hologramme statique multi-utilisateur de base.

Dans le tutoriel suivant, vous allez apprendre à offrir aux utilisateurs un retour en temps réel. Ce retour inclut des informations sur la création d’ancres, la compréhension de qualité de l’environnement et l’état de la session Azure. Sans retour, les utilisateurs risquent de ne pas savoir si une ancre a été correctement chargée sur Azure, si la qualité de l’environnement est suffisante pour créer une ancre ou pour l’état actuel.

[Leçon suivante : 3. Affichage des commentaires sur les ancres spatiales Azure](mrlearning-asa-ch3.md)
