---
title: Didacticiels de mise en route-1. Vue d’ensemble et objectifs
description: Ce cours vous montre comment implémenter la reconnaissance faciale Azure dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: a311fbe377e4a2654c8905276417cf1104fc4754
ms.sourcegitcommit: 23b130d03fea46a50a712b8301fe4e5deed6cf9c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2019
ms.locfileid: "75334346"
---
# <a name="1-overview-and-objectives"></a><span data-ttu-id="ea12c-105">1. vue d’ensemble et objectifs</span><span class="sxs-lookup"><span data-stu-id="ea12c-105">1. Overview and objectives</span></span>

## <a name="device-support"></a><span data-ttu-id="ea12c-106">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="ea12c-106">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="ea12c-107"><strong>Course</strong></span><span class="sxs-lookup"><span data-stu-id="ea12c-107"><strong>Course</strong></span></span></td>
        <td><span data-ttu-id="ea12c-108"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="ea12c-108"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="ea12c-109"><a href="https://www.microsoft.com//hololens/hardware"><strong>HoloLens 2</strong></a></span><span class="sxs-lookup"><span data-stu-id="ea12c-109"><a href="https://www.microsoft.com//hololens/hardware"><strong>HoloLens 2</strong></a></span></span></td>
        <td><span data-ttu-id="ea12c-110"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="ea12c-110"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td></td>
        <td>❌</td>
        <td><span data-ttu-id="ea12c-111">✔️</span><span class="sxs-lookup"><span data-stu-id="ea12c-111">✔️</span></span></td>
        <td>❌</td>
    </tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="ea12c-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="ea12c-112">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ea12c-113">Prérequis</span><span class="sxs-lookup"><span data-stu-id="ea12c-113">Prerequisites</span></span>

* <span data-ttu-id="ea12c-114">Un PC Windows 10 configuré avec les outils corrects [installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="ea12c-114">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="ea12c-115">Windows 10 SDK 10.0.18362.0 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="ea12c-115">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="ea12c-116">Certaines fonctionnalités C# de programmation de base</span><span class="sxs-lookup"><span data-stu-id="ea12c-116">Some basic C# programming ability</span></span>
* <span data-ttu-id="ea12c-117">Un appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)</span><span class="sxs-lookup"><span data-stu-id="ea12c-117">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>

>[!IMPORTANT]
><span data-ttu-id="ea12c-118">Cette série de didacticiels requiert <a href="https://unity3d.com/get-unity/download/archive" target="_blank">unity 2019,1</a> et la version recommandée est Unity 2019.1.14.</span><span class="sxs-lookup"><span data-stu-id="ea12c-118">This tutorial series requires <a href="https://unity3d.com/get-unity/download/archive" target="_blank">Unity 2019.1</a> and the recommended version is Unity 2019.1.14.</span></span> <span data-ttu-id="ea12c-119">Cela remplace toute exigence ou recommandation de version Unity énoncées dans les conditions préalables liées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ea12c-119">This supersedes any Unity version requirements or recommendations stated in the prerequisites linked above.</span></span>

[<span data-ttu-id="ea12c-120">Leçon suivante : 2. initialisation de votre projet et de votre première application</span><span class="sxs-lookup"><span data-stu-id="ea12c-120">Next lesson: 2. Initializing your project and first application</span></span>](mrlearning-base-ch1.md)
