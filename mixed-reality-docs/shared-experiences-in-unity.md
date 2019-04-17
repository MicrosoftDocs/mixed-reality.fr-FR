---
title: Expériences partagées dans Unity
description: Partager les mêmes hologrammes entre plusieurs utilisateurs dans une application Unity.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: Partage de point d’ancrage, WorldAnchor, MR partage 250, WorldAnchorTransferBatch, SpatialPerception, Azure, Azure ancres spatiales, ASA
ms.openlocfilehash: fe755c15d942660b1e16b2335db28d3d7ce72816
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597113"
---
# <a name="shared-experiences-in-unity"></a>Expériences partagées dans Unity

Une expérience partagée est un où plusieurs utilisateurs, chacun avec leur propre HoloLens, appareil iOS ou Android, afficher et interagir avec le même hologramme qui est positionné sur un point fixe dans l’espace de collectivement. Pour cela via le partage de point d’ancrage spatiale.

## <a name="azure-spatial-anchors"></a>Azure Spatial Anchors

Vous pouvez utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a> de créer des durables spatiales ancres reposant sur le cloud, dont votre application peut ensuite localiser dans plusieurs HoloLens, appareils iOS et Android.  En partageant une ancre spatiale commune sur plusieurs appareils, chaque utilisateur peut voir le contenu restitué par rapport à ce point d’ancrage dans le même emplacement physique.  Ainsi, les expériences partagées en temps réel.

Vous pouvez également utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a> pour la persistance hologramme asynchrone sur HoloLens, appareils iOS et Android.  En partageant une ancre spatial cloud durable, plusieurs périphériques peuvent observer l’hologramme persistante même au fil du temps, même si ces appareils ne sont pas présents ensemble en même temps.

Pour commencer à créer des expériences partagées dans Unity, essayez les 5 minutes <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Démarrages rapides Azure Spatial ancres Unity</a>.

Une fois que vous êtes en cours d’exécution ancres spatiale d’Azure, vous pouvez ensuite <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">créer et localiser les points d’ancrage dans Unity</a>.

## <a name="local-anchor-transfers"></a>Transferts d’ancrage local

Dans les situations où vous ne pouvez pas utiliser les ancres spatiale d’Azure, [local d’ancrage transferts](local-anchor-transfers-in-unity.md) activer un appareil HoloLens exporter un point d’ancrage doivent être importées par un deuxième appareil HoloLens.  Notez que cette approche fournit moins fiable rappel d’ancrage qu’ancres spatiale d’Azure, et appareils iOS et Android ne sont pas pris en charge par cette approche.

## <a name="see-also"></a>Voir aussi
* [Partage des expériences en réalité mixte](shared-experiences-in-mixed-reality.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Ancres Spatial Azure</a>
* <a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Ancres Spatial Azure SDK pour Unity</a>