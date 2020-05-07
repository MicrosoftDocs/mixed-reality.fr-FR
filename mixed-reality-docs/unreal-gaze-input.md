---
title: Entrée en pointage en regard
description: Explique comment utiliser l’entrée en regard dans le temps
author: AndreyChistyakov
ms.author: anchisty
ms.date: 04/08/2020
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, HoloLens, suivi oculaire
ms.openlocfilehash: 7387bb3f25cdbdfac32f508c173fbd098f844e84
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82835621"
---
# <a name="gaze-input"></a><span data-ttu-id="2583c-104">Entrée en regard</span><span class="sxs-lookup"><span data-stu-id="2583c-104">Gaze Input</span></span>

<span data-ttu-id="2583c-105">Le plug-in Windows Mixed Reality ne fournit pas de fonctions spéciales pour l’entrée en regard.</span><span class="sxs-lookup"><span data-stu-id="2583c-105">The Windows Mixed Reality plugin doesn’t provide any special functions for the gaze input.</span></span> <span data-ttu-id="2583c-106">Tout fonctionne par le biais de l’API inréelles standard.</span><span class="sxs-lookup"><span data-stu-id="2583c-106">Everything works though the standard Unreal API.</span></span>

[<span data-ttu-id="2583c-107">API de pointage de tête</span><span class="sxs-lookup"><span data-stu-id="2583c-107">Head gaze API</span></span>](https://docs.unrealengine.com/en-US/BlueprintAPI/Input/HeadMountedDisplay/index.html)

## <a name="eye-tracking"></a><span data-ttu-id="2583c-108">Eye-tracking</span><span class="sxs-lookup"><span data-stu-id="2583c-108">Eye tracking</span></span>

<span data-ttu-id="2583c-109">Pour utiliser l’API de suivi oculaire, les développeurs doivent activer la fonctionnalité « entrée de regard » dans leurs paramètres de projet HoloLens.</span><span class="sxs-lookup"><span data-stu-id="2583c-109">To use the eye tracking API, developers should enable the “Gaze Input” capability in their HoloLens project settings.</span></span> <span data-ttu-id="2583c-110">Lorsque l’application démarre, l’utilisateur voit l’invite de consentement suivante</span><span class="sxs-lookup"><span data-stu-id="2583c-110">When the application starts, user will see the following consent prompt</span></span>

![Autorisations d’entrée oculaire](images/unreal/eye-input-permissions.png)
 
<span data-ttu-id="2583c-112">Si l’utilisateur donne son autorisation, l’application obtient une entrée en regard de l’œil.</span><span class="sxs-lookup"><span data-stu-id="2583c-112">If the user gives their permission, the application will get eye gaze input.</span></span> 

<span data-ttu-id="2583c-113">L’API de suivi des yeux inréel est documentée [ici](https://docs.unrealengine.com/en-US/BlueprintAPI/EyeTracking/index.html)</span><span class="sxs-lookup"><span data-stu-id="2583c-113">Unreal’s eye tracking API is documented is [here](https://docs.unrealengine.com/en-US/BlueprintAPI/EyeTracking/index.html)</span></span>

<span data-ttu-id="2583c-114">Les détails techniques du suivi oculaire sont [ici](eye-tracking.md)</span><span class="sxs-lookup"><span data-stu-id="2583c-114">The technical details of eye tracking are [here](eye-tracking.md)</span></span>

<span data-ttu-id="2583c-115">Notez que, spécifiquement pour le suivi des yeux HoloLens non réels, a un seul rayon de regard pour les deux yeux.</span><span class="sxs-lookup"><span data-stu-id="2583c-115">Note that specifically for Unreal, HoloLens eye tracking has a single gaze ray for both eyes.</span></span> <span data-ttu-id="2583c-116">HoloLens ne fournit pas de suivi oculaire stéréoscopique.</span><span class="sxs-lookup"><span data-stu-id="2583c-116">HoloLens doesn’t provide stereoscopic eye tracking.</span></span>
