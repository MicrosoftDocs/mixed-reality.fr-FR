---
title: Tutoriels de démarrage - 1. Vue d’ensemble et objectifs
description: Ce cours vous montre comment implémenter la reconnaissance faciale Azure dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 36c12d82759b8ac2ba24aa9af37a096e0faf5fb5
ms.sourcegitcommit: ee8c7e821cb337cbccd8af64b13ee5f50109a776
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80082048"
---
# <a name="1-overview-and-objectives"></a><span data-ttu-id="b1b54-105">1. Vue d’ensemble et objectifs</span><span class="sxs-lookup"><span data-stu-id="b1b54-105">1. Overview and objectives</span></span>

## <a name="device-support"></a><span data-ttu-id="b1b54-106">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="b1b54-106">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="b1b54-107"><strong>Cours</strong></span><span class="sxs-lookup"><span data-stu-id="b1b54-107"><strong>Course</strong></span></span></td>
        <td><span data-ttu-id="b1b54-108"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="b1b54-108"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="b1b54-109"><a href="https://www.microsoft.com//hololens/hardware"><strong>HoloLens 2</strong></a></span><span class="sxs-lookup"><span data-stu-id="b1b54-109"><a href="https://www.microsoft.com//hololens/hardware"><strong>HoloLens 2</strong></a></span></span></td>
        <td><span data-ttu-id="b1b54-110"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="b1b54-110"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td></td>
        <td>❌</td>
        <td><span data-ttu-id="b1b54-111">✔️</span><span class="sxs-lookup"><span data-stu-id="b1b54-111">✔️</span></span></td>
        <td>❌</td>
    </tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="b1b54-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="b1b54-112">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b1b54-113">Prérequis</span><span class="sxs-lookup"><span data-stu-id="b1b54-113">Prerequisites</span></span>

* <span data-ttu-id="b1b54-114">PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="b1b54-114">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="b1b54-115">SDK Windows 10 (10.0.18362.0 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="b1b54-115">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="b1b54-116">Capacité de programmation C# de base</span><span class="sxs-lookup"><span data-stu-id="b1b54-116">Some basic C# programming ability</span></span>
* <span data-ttu-id="b1b54-117">Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)</span><span class="sxs-lookup"><span data-stu-id="b1b54-117">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>
* <span data-ttu-id="b1b54-118"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté</span><span class="sxs-lookup"><span data-stu-id="b1b54-118"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.2.X installed and the Universal Windows Platform Build Support module added</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1b54-119">La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X.</span><span class="sxs-lookup"><span data-stu-id="b1b54-119">The recommended Unity version for this tutorial series is Unity 2019.2.X.</span></span> <span data-ttu-id="b1b54-120">Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b1b54-120">This supersedes any Unity version requirements or recommendations stated in the prerequisites linked above.</span></span>

[<span data-ttu-id="b1b54-121">Leçon suivante : 2. Initialisation de votre projet et première application</span><span class="sxs-lookup"><span data-stu-id="b1b54-121">Next lesson: 2. Initializing your project and first application</span></span>](mrlearning-base-ch1.md)
