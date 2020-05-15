---
title: Recommandations sur les performances pour Unreal
description: Recommandations pour des performances optimales pour les applications de réalité mixte dans Unreal
author: sw5813
ms.author: suwu
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, performances, optimisation, paramètres, documentation
ms.openlocfilehash: 1fab2f714628f61a518d89795cf644e90130200a
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82840198"
---
# <a name="performance-recommendations-for-unreal"></a>Recommandations sur les performances pour Unreal

Cet article s’appuie sur les [recommandations sur les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md), mais il se concentre sur des informations propres à l’environnement Unreal Engine.

## <a name="recommended-unreal-project-settings"></a>Paramètres de projet Unreal recommandés

- Utilisez le renderer de réalité virtuelle mobile - dans les paramètres de votre projet, vérifiez que votre plateforme cible est définie sur « Mobile/Tablet » sous « Project – Target Hardware ».
- Désactivez l’élimination des occlusions - sous « Engine - Rendering » dans la section « Culling », décochez « Occlusion Culling »
    + Si l’élimination d’occlusion est nécessaire car une scène très détaillée doit être rendue, il est recommandé d’activer « Support Software Occlusion Culling » sous « Engine - Rendering ». Ceci permet à Unreal d’effectuer des éliminations d’occlusion sur le processeur et d’éviter les requêtes d’occlusion du GPU, dont les performances sont faibles sur HoloLens 2.
- Activez à la fois « Instanced Stereo » et « Mobile Multi-View » sous « Engine – Rendering » dans la catégorie « VR ». Il peut être nécessaire de décocher « Mobile Post-Processing » pour pouvoir cocher « Mobile Multi-View ».
