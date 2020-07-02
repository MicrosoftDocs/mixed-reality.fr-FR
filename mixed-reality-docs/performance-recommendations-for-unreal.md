---
title: Recommandations sur les performances pour Unreal
description: Recommandations pour des performances optimales pour les applications de réalité mixte dans Unreal
author: hferrone
ms.author: v-haferr
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, performances, optimisation, paramètres, documentation
ms.openlocfilehash: 9f128a3ef09f29fc745c21b09b7ec97f5db33605
ms.sourcegitcommit: 7f50210b71a65631fd1bc3fdb215064e0db34333
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84533121"
---
# <a name="performance-recommendations-for-unreal"></a>Recommandations sur les performances pour Unreal

## <a name="overview"></a>Vue d’ensemble

Cet article s’appuie sur les [recommandations sur les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md), mais il se concentre sur des fonctionnalités propres à Unreal Engine. Avant de continuer, nous vous encourageons à vous informer sur les goulots d’étranglement des applications, l’analyse et le profilage des applications de réalité mixte, ainsi que les correctifs des performances généraux.

## <a name="recommended-unreal-project-settings"></a>Paramètres de projet Unreal recommandés
Vous trouverez chacun des paramètres suivants dans **Edit > Project Settings**.

1. Utilisation du convertisseur VR mobile :
    * Faites défiler la page jusqu’à la section **Project**, sélectionnez **Target Hardware**, puis définissez la plateforme cible sur **Mobile/Tablet**.

![Définition de la cible mobile](images/unreal/performance-recommendations-img-01.png)

2. Désactivation de l’élimination de l’occlusion :
    * Faites défiler la page jusqu’à la section **Engine**, sélectionnez **Rendering**, développez la section **Culling**, puis décochez la case **Occlusion Culling**.
        + Si vous avez besoin d’éliminer des occlusions pour une scène précise en cours de rendu, nous vous recommandons de cocher la case **Support Software Occlusion Culling** dans **Engine > Rendering**. Ceci permet à Unreal d’effectuer le travail sur le processeur et d’éviter les requêtes d’occlusion du GPU, dont les performances sont faibles sur HoloLens 2.

![Définition de la cible mobile](images/unreal/performance-recommendations-img-02.png)

3. Mise à jour du rendu VR :
    * Faites défiler la page jusqu’à la section **Engine**, sélectionnez **Rendering**, développez la section **VR** et cochez les cases **Instanced Stereo** et **Mobile Multi-View**.
        + Il peut être nécessaire de décocher **Mobile Post-Processing** pour pouvoir cocher **Mobile Multi-View**.

![Définition de la cible mobile](images/unreal/performance-recommendations-img-03.png)
