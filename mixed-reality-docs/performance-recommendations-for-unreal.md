---
title: Recommandations sur les performances pour Unreal
description: Recommandations pour des performances optimales pour les applications de réalité mixte dans Unreal
author: hferrone
ms.author: v-haferr
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, performances, optimisation, paramètres, documentation
ms.openlocfilehash: 3c65eb519b57457e6c9e9747af0ad75e6a5e1b4d
ms.sourcegitcommit: 1b8090ba6aed9ff128e4f32d40c96fac2e6a220b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330185"
---
# <a name="performance-recommendations-for-unreal"></a><span data-ttu-id="6dda0-104">Recommandations sur les performances pour Unreal</span><span class="sxs-lookup"><span data-stu-id="6dda0-104">Performance recommendations for Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="6dda0-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="6dda0-105">Overview</span></span>

<span data-ttu-id="6dda0-106">Cet article s’appuie sur les [recommandations sur les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md), mais il se concentre sur des fonctionnalités propres à Unreal Engine.</span><span class="sxs-lookup"><span data-stu-id="6dda0-106">This article builds on the discussion outlined in [performance recommendations for mixed reality](understanding-performance-for-mixed-reality.md), but focuses on features specific to Unreal Engine.</span></span> <span data-ttu-id="6dda0-107">Avant de continuer, nous vous encourageons à vous informer sur les goulots d’étranglement des applications, l’analyse et le profilage des applications de réalité mixte, ainsi que les correctifs des performances généraux.</span><span class="sxs-lookup"><span data-stu-id="6dda0-107">You're encouraged to read up on application bottlenecks, analyzing and profiling mixed reality apps, and general performance fixes before continuing.</span></span>

## <a name="recommended-unreal-project-settings"></a><span data-ttu-id="6dda0-108">Paramètres de projet Unreal recommandés</span><span class="sxs-lookup"><span data-stu-id="6dda0-108">Recommended Unreal project settings</span></span>
<span data-ttu-id="6dda0-109">Vous trouverez chacun des paramètres suivants dans **Edit > Project Settings**.</span><span class="sxs-lookup"><span data-stu-id="6dda0-109">You can find each of the following settings in **Edit > Project Settings**.</span></span>

1. <span data-ttu-id="6dda0-110">Utilisation du convertisseur VR mobile :</span><span class="sxs-lookup"><span data-stu-id="6dda0-110">Using the mobile VR renderer:</span></span>
    * <span data-ttu-id="6dda0-111">Faites défiler la page jusqu’à la section **Project**, sélectionnez **Target Hardware**, puis définissez la plateforme cible sur **Mobile/Tablet**.</span><span class="sxs-lookup"><span data-stu-id="6dda0-111">Scroll to the **Project** section, select **Target Hardware**, and set the target platform to **Mobile/Tablet**</span></span>

![Définition de la cible mobile](images/unreal/performance-recommendations-img-01.png)

2. <span data-ttu-id="6dda0-113">Désactivation de l’élimination de l’occlusion :</span><span class="sxs-lookup"><span data-stu-id="6dda0-113">Disabling occlusion culling:</span></span>
    * <span data-ttu-id="6dda0-114">Faites défiler la page jusqu’à la section **Engine**, sélectionnez **Rendering**, développez la section **Culling**, puis décochez la case **Occlusion Culling**.</span><span class="sxs-lookup"><span data-stu-id="6dda0-114">Scroll to the **Engine** section, select **Rendering**, expand the **Culling** section, and uncheck **Occlusion Culling**.</span></span>
        + <span data-ttu-id="6dda0-115">Si vous avez besoin d’éliminer des occlusions pour une scène précise en cours de rendu, il est recommandé de cocher la case **Support Software Occlusion Culling** dans **Engine > Rendering**.</span><span class="sxs-lookup"><span data-stu-id="6dda0-115">If you need occlusion culling for a detailed scene being rendered, it's recommended that you enable **Support Software Occlusion Cullin** in **Engine > Rendering**.</span></span> <span data-ttu-id="6dda0-116">Ceci permet à Unreal d’effectuer le travail sur le processeur et d’éviter les requêtes d’occlusion du GPU, dont les performances sont faibles sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="6dda0-116">This lets Unreal to do the work on the CPU and avoid GPU occlusion queries, which perform poorly on HoloLens 2.</span></span>

![Définition de la cible mobile](images/unreal/performance-recommendations-img-02.png)

3. <span data-ttu-id="6dda0-118">Mise à jour du rendu VR :</span><span class="sxs-lookup"><span data-stu-id="6dda0-118">Updating VR rendering:</span></span>
    * <span data-ttu-id="6dda0-119">Faites défiler la page jusqu’à la section **Engine**, sélectionnez **Rendering**, développez la section **VR** et cochez les cases **Instanced Stereo** et **Mobile Multi-View**.</span><span class="sxs-lookup"><span data-stu-id="6dda0-119">Scroll to the **Engine** section, select **Rendering**, expand the **VR** section, and enable both **Instanced Stereo** and **Mobile Multi-View**.</span></span>
        + <span data-ttu-id="6dda0-120">Il peut être nécessaire de décocher **Mobile Post-Processing** pour pouvoir cocher **Mobile Multi-View**.</span><span class="sxs-lookup"><span data-stu-id="6dda0-120">You may need to uncheck **Mobile Post-Processing** in order to be able to check **Mobile Multi-View**</span></span>

![Définition de la cible mobile](images/unreal/performance-recommendations-img-03.png)
