---
title: Tutoriels sur le cloud Azure - 4. Intégration d’Azure Spatial Anchors
description: Suivez ce cours pour découvrir comment implémenter Azure Spatial Anchors dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens, hololens 2, ancres spatiales Azure
ms.localizationpriority: high
ms.openlocfilehash: 4eac2b96519abeebc277a53ad83d1b6dec8d61fd
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86304420"
---
# <a name="4-integrating-azure-spatial-anchors"></a>4. Intégration d’Azure Spatial Anchors

Dans ce tutoriel, vous allez découvrir comment utiliser **Azure Spatial Anchors**. Vous allez stocker l’emplacement d’un **objet suivi** en tant qu’ancre spatiale Azure. Ensuite, vous interrogerez et présenterez à l’utilisateur une flèche de guidage pointant vers l’emplacement.

## <a name="objectives"></a>Objectifs

* Apprendre les bases d’Azure Spatial Anchors
* Apprendre à configurer la scène pour utiliser Azure Spatial Anchors dans ce projet
* Apprendre à intégrer le stockage et la recherche des emplacements

## <a name="understanding-azure-spatial-anchors"></a>Présentation d’Azure Spatial Anchors

 **Azure Spatial Anchors** fait partie de la famille Azure Cloud Services. Sa fonction est d’enregistrer les emplacements d’ancrage. Les emplacements d’ancrage enregistrés peuvent être récupérés à partir du cloud d’après l’*ID d’ancre*. Ces emplacements d’ancrage peuvent être partagés et sollicités par des appareils multiplateformes tels que des appareils HoloLens, iOS et Android.

Apprenez-en davantage sur [Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/overview).

## <a name="preparing-azure-spatial-anchors"></a>Préparation d’Azure Spatial Anchors

Avant de commencer, vous devez créer une ressource Spatial Anchors dans le portail Azure.
Découvrez comment créer une [ressource Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens#create-a-spatial-anchors-resource).

## <a name="preparing-the-scene"></a>Préparation de la scène

Dans cette section, vous allez découvrir comment configurer la scène et apporter les modifications nécessaires.

Dans la fenêtre Project, accédez à **Assets > MRTK.Tutorials.AzureCloudServices > Prefabs > Manager**.

![mr-learning-azure](images/mr-learning-azure/tutorial4-section1-step1-1.png)

Dans le dossier **Manager**, glissez-déposez le préfabriqué **Anchor Manager** vers la hiérarchie de la scène.

Sélectionnez **Anchor Manager** GameObject dans la hiérarchie et, dans la section Inspector, vous trouverez **Spatial Anchor Manager** (Script). Recherchez l’ID de compte et le champ de clé, puis ajoutez les informations d’identification que vous avez créées dans la section Prérequis à l’étape précédente.

![mr-learning-azure](images/mr-learning-azure/tutorial4-section1-step2-1.png)

À présent, recherchez l’objet **Scene Controller** dans la hiérarchie de votre scène et sélectionnez-le. Vous verrez l’inspecteur **Scene Controller**.

![mr-learning-azure](images/mr-learning-azure/tutorial4-section1-step3-1.png)

Vous remarquerez que le champ **Anchor Manager** du composant **Scene Controller** est vide. Glissez-déposez l’**Anchor Manager** de la hiérarchie de la scène vers ce champ et enregistrez la scène.

## <a name="build-and-deploy-the-app-to-your-hololens-2"></a>Générer et déployer l’application sur votre HoloLens 2

Azure Spatial Anchors ne peut pas s’exécuter dans Unity : pour tester la fonctionnalité Azure Spatial Anchors, vous devez déployer le projet sur votre appareil.

> [!TIP]
> Pour un rappel de la façon de générer et déployer votre projet Unity sur HoloLens 2, vous pouvez vous référer aux instructions de [Générer votre application sur votre appareil](mr-learning-base-ch1.md#build-your-application-to-your-device).

## <a name="run-the-app-on-your-hololens-2-and-follow-the-in-app-instructions"></a>Exécuter l’application sur votre HoloLens 2 et suivre les instructions dans l’application

### <a name="create-an-anchor-to-store-a-location"></a>Créer une ancre où stocker un emplacement

Dans cette section, vous allez découvrir comment enregistrer l’emplacement d’un objet.

Exécutez l’application et cliquez sur **Set Object** (Définir un objet) dans le menu principal de l’expérience.

Indiquez le **nom** de l’objet que vous souhaitez enregistrer, puis cliquez sur **Set Object** pour continuer. Pour ajouter des informations supplémentaires sur l’objet, sélectionnez l’**image** et décrivez l’objet.

Pour enregistrer l’emplacement, cliquez sur **Save Location**.

Vous verrez un **pointeur d’ancrage** que vous pouvez déplacer et positionner à l’emplacement que vous souhaitez enregistrer. Après cela, une fenêtre contextuelle de confirmation s’affiche. Si vous souhaitez confirmer et enregistrer l’emplacement, cliquez sur **Yes** ; dans le cas contraire, vous pouvez changer l’emplacement en cliquant sur **No** et en sélectionnant à nouveau l’emplacement.

Une fois que vous avez confirmé l’emplacement en cliquant sur **Yes**, l’emplacement et l’ID d’ancre sont enregistrés dans le stockage cloud Azure. Après cela, vous verrez l’**étiquette d’objet** dans l’ancre, avec le nom de l’objet.

L’emplacement de l’objet est maintenant enregistré.

### <a name="query-for-finding-an-anchor-location"></a>Recherche d’un emplacement d’ancrage

Une fois que vous avez enregistré correctement l’emplacement d’ancrage, vous pouvez le rechercher en sélectionnant **Search Object** dans le menu principal.

Quand vous cliquez sur **Search Object**, une nouvelle fenêtre s’affiche, dans laquelle vous devez indiquer le nom de l’objet à rechercher.

Entrez le nom de l’objet et cliquez sur **Search Object**. Si l’objet a été enregistré précédemment et se trouve dans la base de données, vous obtiendrez la fiche de l’objet avec tous les détails de l’objet que vous avez enregistré.

Vous pouvez maintenant cliquer sur **Show Location** (Afficher l’emplacement) pour rechercher l’objet. Quand vous cliquez sur **Show Location**, le système interroge le stockage cloud afin de connaître l’adresse de l’objet.

Une fois l’emplacement récupéré, une **flèche** vous dirige vers l’emplacement de l’objet. Suivez la flèche jusqu’à ce que vous trouviez l’emplacement de l’objet.

Une fois que vous avez trouvé l’objet, son nom s’affiche en haut et la flèche disparaît. Vous pouvez maintenant cliquer sur l’**étiquette d’objet** pour voir les détails de l’objet.

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez vu comment Azure Spatial Anchors pouvait enregistrer et récupérer l’emplacement d’un objet sur HoloLense 2.

Dans le dernier tutoriel, vous allez découvrir comment utiliser **Azure Bot Service** pour ajouter le langage naturel comme nouvelle méthode d’interaction pour notre application.

[Tutoriel suivant : 5. Intégration d’Azure Bot Service avec LUIS](mr-learning-azure-05.md)
