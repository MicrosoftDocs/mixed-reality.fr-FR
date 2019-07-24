---
title: Expériences partagées dans Unity
description: Partager les mêmes hologrammes entre plusieurs utilisateurs dans une application Unity.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: Partage, ancrer, WorldAnchor, MR partageant 250, WorldAnchorTransferBatch, SpatialPerception, Azure, ancres spatiales Azure, ASA
ms.openlocfilehash: fe755c15d942660b1e16b2335db28d3d7ce72816
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63516792"
---
# <a name="shared-experiences-in-unity"></a>Expériences partagées dans Unity

Une expérience partagée est celle où plusieurs utilisateurs, chacun disposant de leurs propres appareils HoloLens, iOS ou Android, affichent et interagissent collectivement avec le même hologramme, qui est positionné à un point fixe dans l’espace. Pour ce faire, vous devez utiliser le partage d’ancrage spatial.

## <a name="azure-spatial-anchors"></a>Azure Spatial Anchors

Vous pouvez utiliser des <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres spatiales Azure</a> pour créer des ancres spatiales durables dans le Cloud, que votre application peut ensuite localiser sur plusieurs appareils HoloLens, iOS et Android.  En partageant une ancre spatiale commune sur plusieurs appareils, chaque utilisateur peut voir le contenu affiché par rapport à cette ancre dans le même emplacement physique.  Cette technique autorise les expériences partagées en temps réel.

Vous pouvez également utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a> pour la persistance asynchrone des hologrammes sur les appareils HoloLens, iOS et Android.  En partageant une ancre spatiale cloud durable, plusieurs appareils peuvent observer le même hologramme conservé au fil du temps, même si ces appareils ne sont pas présents ensemble en même temps.

Pour commencer à créer des expériences partagées dans Unity, essayez les Démarrages rapides de 5 minutes d' <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Unity spatiales Azure Unity</a>.

Une fois que vous êtes opérationnel avec les ancres spatiales Azure, vous pouvez <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">créer et localiser des ancres dans Unity</a>.

## <a name="local-anchor-transfers"></a>Transferts d’ancrage locaux

Dans les situations où vous ne pouvez pas utiliser les ancres spatiales Azure, les [transferts d’ancrage locaux](local-anchor-transfers-in-unity.md) permettent à un appareil hololens d’exporter une ancre à importer par un deuxième appareil hololens.  Notez que cette approche offre un rappel d’ancrage moins fiable que les ancres spatiales Azure, et les appareils iOS et Android ne sont pas pris en charge par cette approche.

## <a name="see-also"></a>Voir aussi
* [Expériences partagées dans Mixed Reality](shared-experiences-in-mixed-reality.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>
* <a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Kit de développement logiciel (SDK) d’ancre spatiale Azure pour Unity</a>