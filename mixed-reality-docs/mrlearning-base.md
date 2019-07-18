---
title: Présentation du module de base de l’apprentissage de MR
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 3c779d731d7cf139ebcbe305c94754970e937b57
ms.sourcegitcommit: 611af6ff7a2412abad80c0c7d4decfc0c3a0e8c8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/17/2019
ms.locfileid: "68293612"
---
# <a name="1-overview-and-objectives"></a><span data-ttu-id="a03cd-104">1. Vue d’ensemble et objectifs</span><span class="sxs-lookup"><span data-stu-id="a03cd-104">1. Overview and objectives</span></span>

## <a name="device-support"></a><span data-ttu-id="a03cd-105">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="a03cd-105">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="a03cd-106"><strong>Course</strong></span><span class="sxs-lookup"><span data-stu-id="a03cd-106"><strong>Course</strong></span></span></td>
        <td><span data-ttu-id="a03cd-107"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="a03cd-107"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="a03cd-108"><a href="https://www.microsoft.com/en-us/hololens/hardware"><strong>HoloLens 2</strong></a></span><span class="sxs-lookup"><span data-stu-id="a03cd-108"><a href="https://www.microsoft.com/en-us/hololens/hardware"><strong>HoloLens 2</strong></a></span></span></td>
        <td><span data-ttu-id="a03cd-109"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="a03cd-109"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td></td>
        <td><span data-ttu-id="a03cd-110">❌</span><span class="sxs-lookup"><span data-stu-id="a03cd-110">❌</span></span></td>
        <td><span data-ttu-id="a03cd-111">✔️</span><span class="sxs-lookup"><span data-stu-id="a03cd-111">✔️</span></span></td>
        <td><span data-ttu-id="a03cd-112">❌</span><span class="sxs-lookup"><span data-stu-id="a03cd-112">❌</span></span></td>
    </tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="a03cd-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a03cd-113">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a03cd-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="a03cd-114">Prerequisites</span></span>

* <span data-ttu-id="a03cd-115">Un PC Windows 10 configuré avec les outils corrects [installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="a03cd-115">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="a03cd-116">Windows 10 SDK 10.0.18362.0 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="a03cd-116">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="a03cd-117">Certaines fonctionnalités C# de programmation de base.</span><span class="sxs-lookup"><span data-stu-id="a03cd-117">Some basic C# programming ability.</span></span>
* <span data-ttu-id="a03cd-118">Un appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="a03cd-118">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>

[<span data-ttu-id="a03cd-119">Leçon suivante : Initialisation de votre projet et première application</span><span class="sxs-lookup"><span data-stu-id="a03cd-119">Next Lesson: Initializing your project and first application</span></span>](mrlearning-base-ch1.md)