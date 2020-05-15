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
# <a name="performance-recommendations-for-unreal"></a><span data-ttu-id="34ca5-104">Recommandations sur les performances pour Unreal</span><span class="sxs-lookup"><span data-stu-id="34ca5-104">Performance recommendations for Unreal</span></span>

<span data-ttu-id="34ca5-105">Cet article s’appuie sur les [recommandations sur les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md), mais il se concentre sur des informations propres à l’environnement Unreal Engine.</span><span class="sxs-lookup"><span data-stu-id="34ca5-105">This article builds on the discussion outlined in [performance recommendations for mixed reality](understanding-performance-for-mixed-reality.md) but focuses on learnings specific to the Unreal Engine environment.</span></span>

## <a name="recommended-unreal-project-settings"></a><span data-ttu-id="34ca5-106">Paramètres de projet Unreal recommandés</span><span class="sxs-lookup"><span data-stu-id="34ca5-106">Recommended Unreal project settings</span></span>

- <span data-ttu-id="34ca5-107">Utilisez le renderer de réalité virtuelle mobile - dans les paramètres de votre projet, vérifiez que votre plateforme cible est définie sur « Mobile/Tablet » sous « Project – Target Hardware ».</span><span class="sxs-lookup"><span data-stu-id="34ca5-107">Use the mobile VR renderer- in your project settings, ensure your target platform is set to "Mobile/Tablet" under "Project – Target Hardware"</span></span>
- <span data-ttu-id="34ca5-108">Désactivez l’élimination des occlusions - sous « Engine - Rendering » dans la section « Culling », décochez « Occlusion Culling »</span><span class="sxs-lookup"><span data-stu-id="34ca5-108">Disable occlusion culling- under "Engine – Rendering" in the "Culling" section, uncheck "Occlusion Culling"</span></span>
    + <span data-ttu-id="34ca5-109">Si l’élimination d’occlusion est nécessaire car une scène très détaillée doit être rendue, il est recommandé d’activer « Support Software Occlusion Culling » sous « Engine - Rendering ».</span><span class="sxs-lookup"><span data-stu-id="34ca5-109">If occlusion culling is required because a very detailed scene needs to be rendered, it is recommended that "Support Software Occlusion Culling" is enabled Under "Engine – Rendering".</span></span> <span data-ttu-id="34ca5-110">Ceci permet à Unreal d’effectuer des éliminations d’occlusion sur le processeur et d’éviter les requêtes d’occlusion du GPU, dont les performances sont faibles sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="34ca5-110">This allows Unreal to do occlusion culling on the CPU and avoid GPU occlusion queries, which perform poorly on HoloLens 2.</span></span>
- <span data-ttu-id="34ca5-111">Activez à la fois « Instanced Stereo » et « Mobile Multi-View » sous « Engine – Rendering » dans la catégorie « VR ».</span><span class="sxs-lookup"><span data-stu-id="34ca5-111">Enable both "Instanced Stereo" and "Mobile Multi-View" under "Engine – Rendering" in the "VR" category.</span></span> <span data-ttu-id="34ca5-112">Il peut être nécessaire de décocher « Mobile Post-Processing » pour pouvoir cocher « Mobile Multi-View ».</span><span class="sxs-lookup"><span data-stu-id="34ca5-112">You may need to uncheck "Mobile Post-Processing" in order to be able to check "Mobile Multi-View"</span></span>
