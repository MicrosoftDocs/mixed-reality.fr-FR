---
title: Présentation du Module MR Learning Base
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 389a23129d4dfc5819cdc45d071b678e3792089d
ms.sourcegitcommit: cf9f8ebbca0301e9d277853771ff6e47701ba1c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67523154"
---
# <a name="1-overview-and-objectives"></a><span data-ttu-id="f0e27-104">1. Vue d’ensemble et objectifs</span><span class="sxs-lookup"><span data-stu-id="f0e27-104">1. Overview and objectives</span></span>

## <a name="device-support"></a><span data-ttu-id="f0e27-105">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="f0e27-105">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="f0e27-106"><strong>Cours</strong></span><span class="sxs-lookup"><span data-stu-id="f0e27-106"><strong>Course</strong></span></span></td>
        <td><span data-ttu-id="f0e27-107"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="f0e27-107"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="f0e27-108"><a href="https://www.microsoft.com/en-us/hololens/hardware"><strong>HoloLens 2</strong></a></span><span class="sxs-lookup"><span data-stu-id="f0e27-108"><a href="https://www.microsoft.com/en-us/hololens/hardware"><strong>HoloLens 2</strong></a></span></span></td>
        <td><span data-ttu-id="f0e27-109"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="f0e27-109"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td></td>
        <td><span data-ttu-id="f0e27-110">❌</span><span class="sxs-lookup"><span data-stu-id="f0e27-110">❌</span></span></td>
        <td><span data-ttu-id="f0e27-111">✔️</span><span class="sxs-lookup"><span data-stu-id="f0e27-111">✔️</span></span></td>
        <td><span data-ttu-id="f0e27-112">❌</span><span class="sxs-lookup"><span data-stu-id="f0e27-112">❌</span></span></td>
    </tr>
</table>

## <a name="before-you-start"></a><span data-ttu-id="f0e27-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f0e27-113">Before you start</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f0e27-114">Prérequis</span><span class="sxs-lookup"><span data-stu-id="f0e27-114">Prerequisites</span></span>

* <span data-ttu-id="f0e27-115">Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="f0e27-115">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="f0e27-116">SDK Windows 10 10.0.18362.0 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="f0e27-116">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="f0e27-117">Base C# possibilité de programmation.</span><span class="sxs-lookup"><span data-stu-id="f0e27-117">Some basic C# programming ability.</span></span>
* <span data-ttu-id="f0e27-118">Un appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).</span><span class="sxs-lookup"><span data-stu-id="f0e27-118">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode).</span></span>
