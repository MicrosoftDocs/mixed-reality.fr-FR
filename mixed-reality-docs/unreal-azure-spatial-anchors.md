---
title: Azure Spatial Anchors dans Unreal
description: Vue d’ensemble de la création d’ancres spatiales Azure dans un moteur Unreal.
author: hferrone
services: azure-spatial-anchors
ms.author: v-haferr
ms.date: 07/01/2020
ms.topic: tutorial
ms.service: azure-spatial-anchors
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens 2, azure, développement Azure, ancres spatiales, réalité mixte, développement, fonctionnalités, nouveau projet, émulateur, documentation, guides, hologrammes, développement de jeux
ms.openlocfilehash: c7189407bea4b38e7305f0dda7637b82d3325704
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87377282"
---
# <a name="azure-spatial-anchors-in-unreal"></a>Azure Spatial Anchors dans Unreal

## <a name="overview"></a>Vue d’ensemble

Azure Spatial Anchors est un service de Réalité mixte Microsoft qui permet aux appareils de réalité augmentée de découvrir, de partager et de conserver des points d’ancrage dans le monde physique. La documentation ci-dessous fournit des instructions pour l’intégration du service Azure Spatial Anchors à un projet Unreal. Si vous souhaitez obtenir plus d’informations, consultez la documentation sur le [service Azure Spatial Anchors](https://azure.microsoft.com/services/spatial-anchors/).

> [!IMPORTANT]
> Les ancres locales sont stockées sur l’appareil, alors que les ancres spatiales Azure sont stockées dans le cloud. Si vous envisagez de stocker vos ancres localement sur un appareil, nous mettons à votre disposition un document sur les [ancres spatiales locales](unreal-spatial-anchors.md) qui peut vous guider tout au long du processus. Notez que vous pouvez avoir des ancres locales et Azure dans le même projet sans conflit.

## <a name="prerequisites"></a>Prérequis

Pour suivre ce guide, vous devez avoir :

- Installé [Unreal version 4.25](https://www.unrealengine.com/get-now) ou version ultérieure.
- Un projet [HoloLens 2](unreal-uxt-ch1.md) configuré dans Unreal. 
- Lu la [vue d’ensemble d’Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/overview).
- Une connaissance de base de C++ et Unreal.

## <a name="getting-azure-spatial-anchors-account-info"></a>Obtention d’informations sur le compte Azure Spatial Anchors

Avant d’utiliser Azure Spatial Anchors dans votre projet, vous devez :
* [Créer une ressource d’ancres spatiales](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens#create-a-spatial-anchors-resource) et copier les champs de compte listés ci-dessous. Ces valeurs sont utilisées pour authentifier les utilisateurs auprès du compte de votre application :
    * **ID de compte**
    * **Clé de compte**

Pour plus d’informations, consultez la documentation sur l’[authentification Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/concepts/authentication?tabs=csharp).

> [!NOTE]
> Azure Spatial Anchors dans Unreal 4.25 ne prend pas en charge les jetons d’authentification Azure AD, mais la prise en charge de cette fonctionnalité sera disponible dans une version ultérieure.

## <a name="adding-azure-spatial-anchors-plugins"></a>Ajout des plug-ins Azure Spatial Anchors

Activez les plug-ins Azure Spatial Anchors dans l’éditeur Unreal en effectuant les étapes suivantes :
1. Cliquez sur **Edit > Plugins** et recherchez **AzureSpatialAnchors** et **AzureSpatialAnchorsForWMR**.
2. Cochez la case **Enabled** dans les deux plug-ins pour autoriser l’accès aux bibliothèques de blueprints Azure Spatial Anchors dans votre application.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-01.png)

Une fois cette opération terminée, redémarrez l’éditeur Unreal pour que les modifications apportées aux plug-ins prennent effet. Le projet est maintenant prêt à utiliser Azure Spatial Anchors.

## <a name="starting-a-spatial-anchors-session"></a>Démarrage d’une session Spatial Anchors
Une session Azure Spatial Anchors permet aux applications clientes de communiquer avec le service Azure Spatial Anchors. Vous devez créer et démarrer une session Azure Spatial Anchors pour créer, conserver et partager des ancres spatiales Azure :

1. Ouvrez le blueprint du Pawn que vous utilisez dans l’application.
2. Ajoutez deux variables de chaîne pour l’**ID de compte** et la **clé de compte**, puis affectez les valeurs correspondantes à partir de votre compte Azure Spatial Anchors pour authentifier la session.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-02.png)

Démarrez une session Azure Spatial Anchors en effectuant les étapes suivantes :
1. Vérifiez qu’une **session RA** est en cours d’exécution dans l’application HoloLens, car la session Azure Spatial Anchors ne peut pas démarrer tant qu’une session RA n’est pas en cours d’exécution. Si vous n’en avez pas configuré, [créez une ressource de session RA](https://docs.microsoft.com/windows/mixed-reality/unreal-uxt-ch3#adding-the-session-asset).
2. Ajoutez l’événement personnalisé **Démarrer une session Azure Spatial Anchors** et configurez-le comme indiqué dans la capture d’écran ci-dessous.
    * La création d’une session ne provoque pas son démarrage par défaut, ce qui permet au développeur de configurer la session pour l’authentification auprès du service Azure Spatial Anchors.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-03.png)

3. Configurez la session Azure Spatial Anchors pour fournir l’**ID de compte** et la **clé de compte**.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-04.png)

4. Démarrez la session Azure Spatial Anchors afin de permettre à l’application de créer et de localiser les ancres spatiales Azure.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-05.png)

Nous vous recommandons de nettoyer les ressources Azure Spatial Anchors dans votre blueprint de graphe d’événements lorsque vous n’utilisez plus le service :

1. Arrêtez la session Azure Spatial Anchors. La session ne sera plus en cours d’exécution, mais ses ressources associées existeront toujours dans le plug-in Azure Spatial Anchors.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-06.png)

2. Détruisez la session Azure Spatial Anchors pour nettoyer toutes les ressources de session Azure Spatial Anchors, toujours connues du plug-in Azure Spatial Anchors.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-07.png)

Votre blueprint de graphe d’événements doit ressembler à la capture d’écran ci-dessous :

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-08.png)


## <a name="creating-an-anchor"></a>Création d’une ancre
Une ancre spatiale Azure représente un environnement physique dans l’espace de l’application de réalité augmentée, qui verrouille le contenu de réalité augmentée à des emplacements du monde physique. Les ancres spatiales Azure peuvent également être partagées par différents utilisateurs. Ce partage permet de placer du contenu de réalité augmenté sur différents appareils au même emplacement dans le monde physique. 

Pour créer une ancre spatiale Azure
1. Vérifiez qu’une session Azure Spatial Anchors est en cours d’exécution. L’application ne peut pas créer ou conserver une ancre spatiale Azure quand aucune session Azure Spatial Anchors n’est en cours d’exécution.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-09.png)

2. Créez ou obtenez un **[composant de scène](https://docs.unrealengine.com/API/Runtime/Engine/Components/USceneComponent/index.html)** Unreal dont l’emplacement doit être conservé. 
    * Dans l’image ci-dessous, le composant **Scene Component Needing Anchor** est utilisé comme variable. Un composant de scène Unreal est nécessaire pour établir une transformation universelle d’application pour une [épingle RA](https://docs.unrealengine.com/BlueprintAPI/HoloLensAR/ARPin/index.html) et une ancre spatiale Azure.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-10.png)

Pour construire et enregistrer une ancre spatiale Azure pour un composant de scène Unreal
1. Appelez le [composant d’épingle](https://docs.unrealengine.com/BlueprintAPI/ARAugmentedReality/Pin/PinComponent/index.html) pour le composant de scène Unreal et spécifiez la **transformation universelle** du composant de scène comme transformation universelle utilisée pour l’épingle RA.
    * Unreal effectue le suivi des points RA dans l’espace de l’application à l’aide d’épingles RA, qui sont utilisées pour créer une ancre spatiale Azure. Dans Unreal, une épingle RA est analogue à un SpatialAnchor sur HoloLens.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-11.png)

2. Appelez **Create Cloud Anchor** à l’aide de l’épingle RA que vous venez de créer.
    * Create Cloud Anchor crée une ancre spatiale Azure localement mais pas dans le service Azure Spatial Anchors. Les paramètres de l’ancre spatiale Azure, tels que la date d’expiration, peuvent être définis avant de créer l’ancre spatiale Azure avec le service.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-12.png)

3. Définissez l’expiration de l’ancre spatiale Azure. Le paramètre Durée de vie de cette fonction permet au développeur de spécifier, en secondes, la durée pendant laquelle l’ancre doit être tenue à jour par le service.
    * Par exemple, un délai d’expiration d’une semaine prendrait une valeur de 60 secondes x 60 minutes x 24 heures x 7 jours = 604 800 secondes.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-13.png)

Après avoir défini les paramètres de l’ancre, déclarez-la comme prête à être enregistrée. Dans l’exemple ci-dessous, la nouvelle ancre spatiale Azure est ajoutée à un ensemble d’ancres spatiales Azure nécessitant un enregistrement. Cet ensemble est déclaré en tant que variable pour le blueprint de Pawn.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-14.png)

## <a name="saving-an-anchor"></a>Enregistrement d’une ancre

Après avoir configuré l’ancre spatiale Azure avec vos paramètres, appelez **Save Cloud Anchor**. Save Cloud Anchor déclare l’ancre auprès du service Azure Spatial Anchors. Lorsque l’appel à Save Cloud Anchor s’effectue correctement, l’ancre spatiale Azure est disponible pour les autres utilisateurs du service Azure Spatial Anchors.  

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-15.png)

> [!NOTE]
> Save Cloud Anchor est une fonction asynchrone qui peut être appelée uniquement sur un événement de thread de jeu, par exemple **EventTick**. Save Cloud Anchor peut ne pas apparaître en tant que fonction de blueprint disponible dans les fonctions de blueprint personnalisées. Toutefois, elle devrait être disponible dans l’éditeur de blueprint de graphe d’événements de Pawn.

Dans l’exemple ci-dessous, l’ancre spatiale Azure est stockée dans un ensemble pendant un rappel d’événement d’entrée. Elle est ensuite enregistrée sur l’EventTick. L’enregistrement d’une ancre spatiale Azure peut nécessiter plusieurs tentatives, en fonction de la quantité de données spatiales créées par votre session Azure Spatial Anchors. Il est donc préférable de vérifier si l’appel d’enregistrement a réussi.

Si l’ancre n’est pas enregistrée, rajoutez-la à l’ensemble d’ancres à enregistrer. Les EventTicks ultérieurs essaieront d’enregistrer l’ancre jusqu’à ce qu’elle soit correctement stockée dans le service Azure Spatial Anchors.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-16.png)

Une fois l’ancre enregistrée, vous pouvez utiliser la transformation d’épingles RA en tant que transformation de référence pour placer du contenu dans l’application. D’autres utilisateurs peuvent détecter cette ancre et aligner du contenu RA pour différents appareils dans le monde physique.

## <a name="deleting-an-anchor"></a>Suppression d’une ancre

Vous pouvez supprimer des ancres du service Azure Spatial Anchors en appelant **Delete Cloud Anchor**.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-17.png)

> [!NOTE]
> Delete Cloud Anchor est une fonction latente qui peut être appelée uniquement sur un événement de thread de jeu, tel qu’EventTick. Delete Cloud Anchor peut ne pas apparaître en tant que fonction de blueprint disponible dans les fonctions de blueprint personnalisées. Elle devrait toutefois être disponible dans l’éditeur de blueprint de graphe d’événements de Pawn.

Dans l’exemple ci-dessous, l’ancre est marquée pour suppression sur un événement d’entrée personnalisé. La suppression est ensuite tentée sur l’EventTick. En cas d’échec de la suppression de l’ancre spatiale Azure, ajoutez-la à l’ensemble d’ancres marquées pour suppression. La suppression sera retentée lors des EventTicks ultérieurs.

Votre blueprint de graphe d’événements doit maintenant ressembler à la capture d’écran ci-dessous :

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-18.png)


## <a name="locating-pre-existing-anchors"></a>Recherche d’ancres préexistantes

En plus de créer des ancres spatiales Azure, vous pouvez détecter les ancres créées par des homologues avec le service Azure Spatial Anchors :

1. Obtenez un identificateur Azure Spatial Anchors pour l’ancre que vous souhaitez détecter.
    * Un identificateur d’ancre peut être obtenu pour une ancre créée par le même appareil lors d’une session Azure Spatial Anchors précédente. Il peut également être créé et partagé par des appareils homologues qui interagissent avec le service Azure Spatial Anchors.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-24.png)

2. Ajoutez un composant **AzureSpatialAnchorsEvent** à votre blueprint de Pawn.
    * Ce composant vous permet de vous abonner à différents événements Azure Spatial Anchors, tels que des événements appelés quand des ancres spatiales Azure sont localisées.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-19.png)

3. Abonnez-vous à l’**ASAAnchor Located Delegate** pour le composant **AzureSpatialAnchorsEvent**.
    * Le délégué permet à l’application de savoir quand de nouvelles ancres associées au compte Azure Spatial Anchors ont été localisées.
    * Avec le rappel d’événement, les ancres spatiales Azure créées par les homologues à l’aide de la session Azure Spatial Anchors n’auront pas d’épingles RA créées par défaut. Pour créer une épingle RA pour l’ancre spatiale Azure détectée, les développeurs peuvent appeler **Create ARPin Around Azure Cloud Spatial Anchor**.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-20.png)

Pour localiser les ancres spatiales Azure créées par des homologues à l’aide du service Azure Spatial Anchors, l’application doit créer un **observateur Azure Spatial Anchors** :
1. Vérifiez qu’une session Azure Spatial Anchors est en cours d’exécution.
2. Créez un **AzureSpatialAnchorsLocateCriteria**.
    * Vous pouvez spécifier différents paramètres d’emplacement tels que la distance par rapport à l’utilisateur ou la distance par rapport à une autre ancre.
3. Déclarez l’identificateur Azure Spatial Anchors souhaité dans l’**AzureSpatialAnchorsLocateCritieria**.
4. Appelez **Create Watcher**.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-21.png)

L’application commence maintenant à rechercher les ancres spatiales Azure connues du service Azure Spatial Anchors, ce qui signifie que les utilisateurs peuvent localiser les ancres spatiales Azure créées par leurs homologues.

Après avoir localisé l’ancre spatiale Azure, appelez **Stop Watcher** pour arrêter l’observateur Azure Spatial Anchors et nettoyer ses ressources.

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-22.png)

Votre blueprint de graphe d’événements final doit maintenant ressembler à la capture d’écran ci-dessous :

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-23.png)


## <a name="next-steps"></a>Étapes suivantes
* [Ancres spatiales locales](unreal-spatial-anchors.md)
* [Documentation sur les ancres spatiales](https://docs.microsoft.com/azure/spatial-anchors/)
* [Fonctionnalités des ancres spatiales](https://azure.microsoft.com/services/spatial-anchors/#features)
* [Recommandations pour une expérience d’ancrage efficace](https://docs.microsoft.com/azure/spatial-anchors/concepts/guidelines-effective-anchor-experiences)