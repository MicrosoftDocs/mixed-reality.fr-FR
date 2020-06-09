---
title: Entrée en pointage en regard
description: Didacticiel sur la configuration de l’entrée de regard pour HoloLens et le moteur inréel
author: hferrone
ms.author: v-haferr
ms.date: 04/08/2020
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, HoloLens 2, suivi oculaire, entrée de regard, affichage monté en tête, moteur non réel
ms.openlocfilehash: 0bc8b83a2e840b066eb5e30665584e1c68f7b021
ms.sourcegitcommit: 7f50210b71a65631fd1bc3fdb215064e0db34333
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84551805"
---
# <a name="gaze-input"></a><span data-ttu-id="f727f-104">Entrée en regard</span><span class="sxs-lookup"><span data-stu-id="f727f-104">Gaze Input</span></span>

## <a name="overview"></a><span data-ttu-id="f727f-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="f727f-105">Overview</span></span>

<span data-ttu-id="f727f-106">Le [plug-in Windows Mixed Reality](https://docs.unrealengine.com/Platforms/VR/WMR/index.html) ne fournit pas de fonctions intégrées pour l’entrée en regard, mais HoloLens 2 prend en charge le suivi oculaire.</span><span class="sxs-lookup"><span data-stu-id="f727f-106">The [Windows Mixed Reality plugin](https://docs.unrealengine.com/Platforms/VR/WMR/index.html) doesn’t provide any built-in functions for gaze input, but HoloLens 2 does support eye tracking.</span></span> <span data-ttu-id="f727f-107">Les fonctionnalités de suivi réelles sont fournies par les API d' **affichage** et de **suivi oculaire** non réelles et incluent :</span><span class="sxs-lookup"><span data-stu-id="f727f-107">The actual tracking features are provided by Unreal's **Head Mounted Display** and **Eye Tracking** APIs and include:</span></span>

- <span data-ttu-id="f727f-108">Informations sur l'appareil</span><span class="sxs-lookup"><span data-stu-id="f727f-108">Device information</span></span>
- <span data-ttu-id="f727f-109">Capteurs de suivi</span><span class="sxs-lookup"><span data-stu-id="f727f-109">Tracking sensors</span></span>
- <span data-ttu-id="f727f-110">Orientation et position</span><span class="sxs-lookup"><span data-stu-id="f727f-110">Orientation and position</span></span>
- <span data-ttu-id="f727f-111">Volets de découpage</span><span class="sxs-lookup"><span data-stu-id="f727f-111">Clipping panes</span></span>
- <span data-ttu-id="f727f-112">Données de regard et informations de suivi</span><span class="sxs-lookup"><span data-stu-id="f727f-112">Gaze data and tracking information</span></span>

<span data-ttu-id="f727f-113">Vous trouverez la liste complète des fonctionnalités dans la documentation sur l' [affichage](https://docs.unrealengine.com/BlueprintAPI/Input/HeadMountedDisplay/index.html) et le [suivi des yeux](https://docs.unrealengine.com/BlueprintAPI/EyeTracking/index.html) de l’inréel.</span><span class="sxs-lookup"><span data-stu-id="f727f-113">You can find the full list of features in Unreal's [Head Mounted Display](https://docs.unrealengine.com/BlueprintAPI/Input/HeadMountedDisplay/index.html) and [Eye Tracking](https://docs.unrealengine.com/BlueprintAPI/EyeTracking/index.html) documentation.</span></span>

<span data-ttu-id="f727f-114">En plus des API inréelless, consultez la documentation sur l' [interaction](eye-gaze-interaction.md) avec le regard sur les yeux pour hololens 2 et découvrez comment fonctionne le [suivi oculaire sur hololens 2](https://docs.microsoft.com/windows/mixed-reality/eye-tracking) .</span><span class="sxs-lookup"><span data-stu-id="f727f-114">In addition to the Unreal APIs, check out the documentation on [eye-gaze-based interaction](eye-gaze-interaction.md) for HoloLens 2 and read up on how [eye tracking on HoloLens 2](https://docs.microsoft.com/windows/mixed-reality/eye-tracking) works.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f727f-115">Le suivi oculaire est pris en charge uniquement sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="f727f-115">Eye tracking is only supported on HoloLens 2.</span></span>

## <a name="enabling-eye-tracking"></a><span data-ttu-id="f727f-116">Activation du suivi oculaire</span><span class="sxs-lookup"><span data-stu-id="f727f-116">Enabling eye tracking</span></span>
<span data-ttu-id="f727f-117">L’entrée en regard doit être activée dans les paramètres du projet HoloLens avant que vous puissiez utiliser l’une des API inréelles.</span><span class="sxs-lookup"><span data-stu-id="f727f-117">Gaze input needs to be enabled in the HoloLens project settings before you can use any of Unreal's APIs.</span></span> <span data-ttu-id="f727f-118">Lorsque l’application démarre, une invite de consentement s’affiche dans la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f727f-118">When the application starts you'll see a consent prompt shown in the screenshot below.</span></span>

- <span data-ttu-id="f727f-119">Sélectionnez **Oui** pour définir l’autorisation et accéder à l’entrée en regard.</span><span class="sxs-lookup"><span data-stu-id="f727f-119">Select **Yes** to set the permission and get access to gaze input.</span></span> <span data-ttu-id="f727f-120">Si vous avez besoin de modifier ce paramètre à tout moment, il se trouve dans l’application **paramètres** .</span><span class="sxs-lookup"><span data-stu-id="f727f-120">If you need to change this setting at any time, it can be found in the **Settings** app.</span></span>

![Autorisations d’entrée oculaire](images/unreal/eye-input-permissions.png)

> [!NOTE] 
> <span data-ttu-id="f727f-122">Le suivi oculaire HoloLens en non réel a un seul rayon de regard pour les yeux au lieu des deux rayons nécessaires pour le suivi STEREOSCOPIQUE, ce qui n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f727f-122">HoloLens eye tracking in Unreal only has a single gaze ray for both eyes instead of the two rays needed for stereoscopic tracking, which is not supported.</span></span>

<span data-ttu-id="f727f-123">C’est tout ce dont vous avez besoin pour commencer à ajouter des entrées de regard à vos applications HoloLens 2 en toute réalité.</span><span class="sxs-lookup"><span data-stu-id="f727f-123">That's all the setup you'll need to start adding gaze input to your HoloLens 2 apps in Unreal.</span></span> <span data-ttu-id="f727f-124">Pour plus d’informations sur l’entrée en regard et la façon dont elle affecte les utilisateurs en réalité mixte, consultez les liens ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f727f-124">More information on gaze input and how it affects users in mixed reality can be found at the links below.</span></span> <span data-ttu-id="f727f-125">Pensez à les utiliser lors de la création de vos expériences interactives.</span><span class="sxs-lookup"><span data-stu-id="f727f-125">Be sure to think about these when building your interactive experiences.</span></span>

## <a name="see-also"></a><span data-ttu-id="f727f-126">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f727f-126">See also</span></span>
* [<span data-ttu-id="f727f-127">Étalonnage</span><span class="sxs-lookup"><span data-stu-id="f727f-127">Calibration</span></span>](calibration.md)
* [<span data-ttu-id="f727f-128">Confort</span><span class="sxs-lookup"><span data-stu-id="f727f-128">Comfort</span></span>](comfort.md)
* [<span data-ttu-id="f727f-129">Pointer et valider</span><span class="sxs-lookup"><span data-stu-id="f727f-129">Gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="f727f-130">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="f727f-130">Voice input</span></span>](voice-design.md)
