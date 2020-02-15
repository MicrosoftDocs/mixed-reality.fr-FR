---
title: Didacticiels sur les ancres spatiales Azure-2. Enregistrement, récupération et partage d’ancres spatiales Azure
description: Suivez ce cours pour découvrir comment implémenter Reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 7b19233a9634e2568200476c9483464bbf9dd3c8
ms.sourcegitcommit: a580166a19294f835b8e09c780f663f228dd5de0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2020
ms.locfileid: "77250733"
---
# <a name="2-saving-retrieving-and-sharing-azure-spatial-anchors"></a>2. enregistrement, récupération et partage d’ancres spatiales Azure

Dans ce didacticiel, vous allez apprendre à enregistrer des ancres spatiales Azure sur plusieurs sessions d’application en enregistrant l’ID d’ancrage dans le stockage de HoloLens 2. Vous allez également apprendre à partager cet ID d’ancrage avec d’autres appareils pour un alignement d’ancrage sur plusieurs appareils.

## <a name="objectives"></a>Objectifs

* Découvrez comment enregistrer et récupérer des ID d’ancrage spatial Azure vers et à partir du disque local HoloLens 2, pour la persistance entre les sessions d’application
* Découvrez comment partager des ID d’ancrage spatial Azure entre les utilisateurs dans un scénario multi-appareil

## <a name="preparing-the-scene"></a>Préparation de la scène

Dans la fenêtre projet, accédez à **ressources** > **MRTK. Tutoriels. AzureSpatialAnchors** > dossier **Prefabs** . Tout en maintenant enfoncé le bouton CTRL, cliquez sur **ButtonParent_SaveAnchorId** et **ButtonParent_ShareAnchorId** pour sélectionner les deux prefabs, puis faites-les glisser dans la fenêtre hiérarchie pour les ajouter à la scène :

![mrlearning-ASA](images/mrlearning-asa/tutorial2-section1-step1-1.png)

## <a name="persist-azure-anchors-between-app-sessions---save-anchor-id-to-disk"></a>Conserver les ancres Azure entre les sessions d’application-enregistrer l’ID d’ancrage sur le disque
<!-- TODO: Consider renaming to 'Persist Azure Anchors between app sessions' -->

Dans cette section, vous allez apprendre à enregistrer et à récupérer l’ID d’ancre Azure vers et à partir du disque local HoloLens 2. Cela vous permet d’interroger Azure pour obtenir le même ID d’ancrage entre différentes sessions d’application, ce qui permet aux hologrammes ancrés d’être positionnés au même emplacement que dans la session d’application précédente.

Dans la fenêtre hiérarchie, développez l’objet **ButtonParent_SaveAnchorId** qui contient deux boutons, un bouton permettant d’enregistrer l’ID d’ancrage Azure dans le stockage HoloLens 2 et un autre pour récupérer l’ID enregistré à partir du disque :

![mrlearning-ASA](images/mrlearning-asa/tutorial2-section2-step1-1.png)

Suivez les mêmes étapes que dans les instructions de [Configuration des boutons pour exécuter les](mrlearning-asa-ch1.md#configuring-the-buttons-to-operate-the-scene) instructions de la scène du didacticiel précédent afin de configurer le composant **Holo Lens 2 (script) du bouton enfoncé** et le composant **(script)** pouvant être interagi sur chacun des deux boutons :

* Pour l’objet **SaveAzureAnchorIdToDisk** , assignez la fonction AnchorModuleScript > **SaveAzureAnchorIdToDisk ()** .
* Pour l’objet **GetAzureAnchorIdFromDisk** , assignez la fonction AnchorModuleScript > **GetAzureAnchorIdFromDisk ()** .

Si vous générez l’application mise à jour dans votre HoloLens, vous pouvez désormais conserver les ancres spatiales Azure entre les sessions d’application en enregistrant l’ID d’ancrage Azure. Pour le tester, procédez comme suit :

1. Déplacez l’expérience du lanceur Rocket vers l’emplacement souhaité.
2. Démarrez la session Azure.
3. Créer un point d’ancrage Azure (crée des ancres à l’emplacement de l’expérience du lanceur Rocket).
4. Enregistrez l’ID d’ancrage Azure sur le disque.
5. Redémarrez l’application.
6. Procurez-vous Azure Anchor à partir du disque (charge l’ID d’ancrage que vous venez d’enregistrer).
7. Démarrez la session Azure.
8. Recherchez Azure Anchor (positionne l’expérience du lanceur Rocket à l’emplacement de l’étape 3).

## <a name="share-azure-anchors-between-multiple-devices"></a>Partager des ancres Azure entre plusieurs appareils

Dans cette section, vous allez apprendre à partager l’ID d’ancre Azure entre plusieurs appareils. Cela permet à plusieurs appareils d’interroger Azure pour obtenir le même ID d’ancrage, ce qui permet l’alignement spatial des hologrammes ancrés. L’alignement spatial, c’est-à-dire le fait de voir les mêmes hologrammes dans le même emplacement physique entre plusieurs appareils, est essentiel pour les expériences partagées locales dans le HoloLens 2.

Il existe de nombreuses façons de transférer des ID d’ancrage Azure entre les appareils, notamment les méthodes décrites dans la série de [didacticiels sur les fonctionnalités multi-utilisateur](mrlearning-sharing(photon)-ch1.md) . Dans cet exemple, vous allez utiliser un service Web simple pour charger et télécharger des ID d’ancrage entre les appareils.

Dans la fenêtre hiérarchie, développez l’objet **ButtonParent_ShareAnchorId** qui contient deux boutons. un bouton pour télécharger l’ID d’ancre Azure sur le serveur Web et un autre pour télécharger l’ID à partir du serveur Web :

![mrlearning-ASA](images/mrlearning-asa/tutorial2-section3-step1-1.png)

Suivez les mêmes étapes que dans les instructions de [Configuration des boutons pour exécuter les](mrlearning-asa-ch1.md#configuring-the-buttons-to-operate-the-scene) instructions de la scène du didacticiel précédent afin de configurer le composant **Holo Lens 2 (script) du bouton enfoncé** et le composant **(script)** pouvant être interagi sur chacun des deux boutons :

* Pour l’objet **ShareAzureAnchorIdToNetwork** , assignez la fonction AnchorModuleScript > **ShareAzureAnchorIdToNetwork ()** .
* Pour l’objet **GetAzureAnchorIdFromNetwork** , assignez la fonction AnchorModuleScript > **GetAzureAnchorIdFromNetwork ()** .

Si vous générez l’application mise à jour sur deux appareils HoloLens, vous pouvez désormais obtenir un alignement spatial entre eux en partageant l’ID d’ancrage Azure. Pour le tester, procédez comme suit :

1. Sur l’appareil HoloLens 1 : déplacez l’expérience du lanceur Rocket vers l’emplacement souhaité.
2. Sur l’appareil HoloLens 1 : démarrez la session Azure.
3. Sur HoloLens Device 1 : Create Azure Anchor (crée des ancres à l’emplacement de l’expérience du lanceur Rocket).
4. Sur l’appareil HoloLens 1 : partager l’ID d’ancrage Azure sur le réseau.
5. Sur l’appareil HoloLens 2 : redémarrez l’application.
6. Sur l’appareil HoloLens 2 : obtenir l’ID d’ancrage partagé à partir du réseau (récupère l’ID d’ancrage qui vient d’être partagé à partir de l’appareil HoloLens 1).
7. Sur l’appareil HoloLens 2 : démarrez la session Azure.
8. Sur l’appareil HoloLens 2 : recherchez Azure Anchor (positionne l’expérience du lanceur Rocket à l’emplacement de l’étape 3).

> [!TIP]
> Si vous ne disposez que d’un HoloLens, vous pouvez toujours tester la fonctionnalité en redémarrant l’application au lieu d’utiliser un deuxième appareil HoloLens.

## <a name="congratulations"></a>Félicitations !

Dans ce didacticiel, vous avez appris à conserver les ancres spatiales Azure entre les sessions d’application et les redémarrages d’application en enregistrant l’ID d’ancrage spatial Azure sur le disque local sur HoloLens. Vous avez également appris comment partager des ancres spatiales Azure entre plusieurs appareils pour une expérience de base multi-utilisateur et une expérience partagée d’hologramme statique.

Dans le didacticiel suivant, vous allez apprendre à fournir aux utilisateurs des commentaires en temps réel. Ces commentaires incluent des informations sur la création d’ancres, la qualité de la compréhension de l’environnement et l’état de la session Azure. Sans commentaires, les utilisateurs peuvent ne pas savoir si un point d’ancrage a été chargé avec succès sur Azure, que la qualité de l’environnement soit suffisante pour la création de l’ancre ou pour l’état actuel.

[Leçon suivante : 3. affichage des commentaires sur l’ancrage spatial Azure](mrlearning-asa-ch3.md)
