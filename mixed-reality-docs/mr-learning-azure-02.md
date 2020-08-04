---
title: Tutoriels sur le cloud Azure - 2. Intégration du stockage Azure
description: Suivez ce cours pour apprendre à implémenter Stockage Table Azure et Stockage Blob Azure dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens, hololens 2, stockage azure
ms.localizationpriority: high
ms.openlocfilehash: a8d91bc55b3ce73d6e1fb46e5d696d853adcf871
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376471"
---
# <a name="2-integrating-azure-storage"></a>2. Intégration du stockage Azure

Dans ce tutoriel, vous allez apprendre à enregistrer des données d’entités dans le stockage Table Azure et des images miniatures dans le stockage Blob Azure. Cette fonctionnalité nous permettra de stocker et de récupérer des *objets suivis* avec des données telles que l’ID, le nom, l’image miniature, et ainsi de suite, entre les sessions et les appareils dans le cloud.

## <a name="objectives"></a>Objectifs

* Apprendre les bases du stockage Azure
* Apprendre à stocker, modifier et récupérer des données à partir du stockage Table
* Apprendre à stocker et supprimer des images à partir du stockage Blob

## <a name="understanding-azure-storage"></a>Présentation du stockage Azure

**Stockage Azure** est une solution de stockage Microsoft sur le cloud qui peut couvrir de nombreux scénarios et besoins. Elle est hautement scalable et aisément accessible aux développeurs. Tous les services peuvent être consommés dans le cadre d’un **compte de stockage Azure**. Pour notre cas d’usage, nous allons utiliser le *stockage Table* et le *stockage Blob*.

Apprenez-en davantage sur les [services de stockage Azure](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-overview).

### <a name="azure-table-storage"></a>Stockage Table Azure

Ce service nous permet de stocker des données de manière semblable à NoSQL. Dans ce projet, nous l’utiliserons pour stocker des informations sur l’*objet suivi*, telles que nom, description, ID d’ancre spatiale et ainsi de suite.

Dans le contexte de l’application de démonstration, vous avez besoin de deux tables : une pour stocker des informations sur le projet, avec des informations relatives à l’état des modèles entraînés (nous y reviendrons dans le tutoriel [Intégration d’Azure Custom Vision](mr-learning-azure-03.md)), et une autre pour stocker des informations sur les *objets suivis*.

Apprenez-en davantage sur le [stockage Table Azure](https://docs.microsoft.com/azure/storage/tables/table-storage-overview).

### <a name="azure-blob-storage"></a>Stockage Blob Azure

Ce service permet de stocker des fichiers binaires volumineux. Vous l’utiliserez pour stocker des photos des *objets suivis* sous forme de miniatures.
Pour l’application de démonstration, vous avez besoin d’un conteneur d’objets blob pour stocker les images.

Apprenez-en davantage sur le [stockage Blob Azure](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction).

## <a name="preparing-azure-storage"></a>Préparation du stockage Azure

Pour consommer les services de stockage Azure, vous avez besoin d’un compte Stockage Azure. Pour créer un compte de stockage, consultez [Créer un compte de stockage](https://docs.microsoft.com/azure/storage/common/storage-account-create?tabs=azure-portal). Pour en savoir plus sur les comptes de stockage, consultez [Vue d’ensemble du compte de stockage](https://docs.microsoft.com/azure/storage/common/storage-account-overview).

Une fois que vous avez un compte de stockage, vous pouvez récupérer la chaîne de connexion à partir du **portail Azure**. Vous en aurez besoin dans la section suivante de cette leçon.

### <a name="optional-azure-storage-explorer"></a>Explorateur Stockage Azure (facultatif)

Même si vous pouvez voir et vérifier toutes les modifications apportées aux données à partir de l’interface utilisateur dans l’application, nous vous recommandons d’installer l’[Explorateur Stockage Azure](https://azure.microsoft.com/features/storage-explorer/). Cet outil vous permet de visualiser les données dans le stockage Azure, et offre une aide précieuse lors du débogage et de l’apprentissage.

> [!TIP]
> Pour les tests à partir de l’éditeur Unity, vous pouvez utiliser un émulateur local :

> * Sur Windows 10, vous pouvez utiliser l’[émulateur de stockage Azure](https://docs.microsoft.com/azure/storage/common/storage-use-emulator)
> * Sur MacOS/Linux, vous pouvez utiliser l’[image Docker Azurite](https://hub.docker.com/_/microsoft-azure-storage-azurite) pour Docker

## <a name="preparing-the-scene"></a>Préparation de la scène

Dans la fenêtre de hiérarchie, recherchez l’objet **DataManager** et sélectionnez-le.

![mr-learning-azure](images/mr-learning-azure/tutorial2-section4-step1-1.png)

Dans la fenêtre de l’inspecteur, vous verrez que le composant **DataManager (script)** est l’endroit où sont conservés tous les paramètres liés au **stockage Azure**. Tous les paramètres pertinents sont déjà définis. Il vous suffit de remplacer le champ *Connection String* (Chaîne de connexion) par celle que vous pouvez récupérer à partir du portail Azure. Si vous utilisez une solution d’émulateur de stockage Azure locale, vous pouvez conserver la *chaîne de connexion* déjà fournie.

Le composant **DataManager (script)** est responsable de la communication avec le **stockage Table** et le **stockage Blob** qui est consommé par d’autres scripts de contrôleur sur les composants d’interface utilisateur.

## <a name="writing-and-reading-data-from-azure-table-storage"></a>Écriture et lecture de données à partir du stockage Table Azure

Maintenant que tout est prêt, vous pouvez créer un *objet suivi*.

Ouvrez l’application sur votre HoloLens et cliquez sur **Set Object** (Définir un objet). Vous verrez que l’objet *EnterObjectName* devient actif dans la hiérarchie. Dans ce menu, cliquez sur la *barre de recherche* et tapez le nom que vous voulez donner à l’*objet suivi*. Après cela, cliquez sur le bouton **Set object**. Cela crée l’*objet suivi* dans le stockage Table Azure, et vous verrez maintenant la **fiche d’objet**.

Cette **fiche d’objet** est une représentation sous forme d’interface utilisateur de l’*objet suivi*. Elle aura un rôle important à plusieurs reprises dans cette série de tutoriels.

Cliquez maintenant sur la *zone de texte* de description et tapez « Car ». Après cela, cliquez sur le bouton **Enregistrer** pour enregistrer les modifications. Arrêtez l’application et réexécutez-la.

Cette fois-ci, cliquez sur **Search Object** et tapez dans la *barre de recherche* le nom utilisé lors de la création de l’*objet suivi*. Vous constaterez que la **fiche d’objet** avec toutes les données est récupérée à partir du **stockage Table Azure**.

N’hésitez pas à fermer la **fiche d’objet** et à créer de nouveaux *objets suivis* et modifier leurs données.

> [!TIP]
> Si vous avez installé l’[Explorateur Stockage Azure](https://azure.microsoft.com/features/storage-explorer/), accédez au tableau d’*objets*. Vous verrez que l’*objet suivi* créé y figure.

## <a name="uploading-and-download-image-from-azure-blob-storage"></a>Chargement et téléchargement d’images à partir du stockage Blob Azure

Dans cette section, vous allez utiliser le stockage Blob Azure pour charger et télécharger des images qui seront utilisées comme miniatures pour les *objets suivis*.

> [!NOTE]
> Dans ce tutoriel, l’application va prendre des photos pour charger des images dans le stockage Blob. Si vous l’exécutez localement à partir de l’éditeur Unity, vérifiez qu’une webcam est connectée à votre ordinateur.

Ouvrez l’application sur votre HoloLens, cliquez sur **Set Object** et tapez le nom « Car » dans la *barre de recherche*. Vous devez maintenant voir la **fiche d’objet**. Cliquez sur le bouton **Camera** et vous serez invité à effectuer un clic aérien pour prendre une photo. Une fois la photo prise, un message vous informe du chargement. Après quelques instants, l’image doit apparaître à la place de l’espace réservé.

Réexécutez l’application et recherchez l’*objet suivi*. L’image chargée doit apparaître sous forme de miniature.

## <a name="deleting-image-from-azure-blob-storage"></a>Suppression d’une image du stockage Blob Azure

Dans la section précédente, vous avez chargé de nouvelles images dans le stockage Blob Azure. Dans cette section, vous allez supprimer une image miniature pour des *objets suivis*.

Ouvrez l’application sur votre HoloLens, cliquez sur **Set Object** et tapez le nom « Car » dans la *barre de recherche*. Vous devez maintenant voir la **fiche d’objet** avec l’image miniature. Cliquez sur le bouton **Delete**. Vous remarquerez que l’image miniature est remplacée par l’image d’espace réservé.

À présent, réexécutez l’application et recherchez l’*objet suivi* de la miniature que vous venez de supprimer. Vous ne devriez voir que l’image d’espace réservé.

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez appris à utiliser les services de stockage Azure pour conserver des données non structurées (comme dans notre cas des **objets suivis**) et des binaires sous forme d’images miniatures pour l’application de démonstration **HoloLens 2** sur le cloud.

Dans le tutoriel suivant, vous allez voir comment utiliser Azure Custom Vision pour détecter les images associées à un *objet suivi*.

[Tutoriel suivant : 3. Intégration d’Azure Custom Vision](mr-learning-azure-03.md)
