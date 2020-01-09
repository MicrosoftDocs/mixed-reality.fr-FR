---
title: Nuance
description: Le nuanceur standard MRTK fournit différents types d’effets visuels qui peuvent être utilisés avec des hologrammes.
author: cre8ivepark
ms.author: dongpark
ms.date: 11/01/2019
ms.topic: article
keywords: Réalité mixte, contrôles, interaction, interface utilisateur, expérience utilisateur
ms.openlocfilehash: 4d95e335b3f7020766beae916423d0588ee66572
ms.sourcegitcommit: 270ca09ec61e1153a83cf44942d7ba3783ef1805
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75694163"
---
# <a name="shader"></a><span data-ttu-id="61e98-104">Nuance</span><span class="sxs-lookup"><span data-stu-id="61e98-104">Shader</span></span>

![Nuance](images/UX/UX_Hero_StandardShader.jpg)

<span data-ttu-id="61e98-106">Étant donné que les objets holographiques sont mélangés avec les éléments physiques dans l’environnement, il est important de fournir des signaux visuels en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="61e98-106">Since holographic objects are mixed with the physical ones in the environment, it's important to provide visual cues in mixed reality.</span></span> <span data-ttu-id="61e98-107">Le nuanceur standard MRTK fournit différents types d’effets visuels qui peuvent être utilisés avec des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="61e98-107">The MRTK Standard shader provides various types of visual effects that can be used with holograms.</span></span> <span data-ttu-id="61e98-108">Le système d’ombrage standard MRTK utilise un nuanceur unique et flexible qui permet d’obtenir des éléments visuels similaires au nuanceur standard de Unity, d’implémenter des [principes de système de conception Fluent](https://www.microsoft.com/design/fluent/#/)et de rester performant sur des appareils de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="61e98-108">The MRTK Standard shading system utilizes a single, flexible shader that can achieve visuals similar to Unity's Standard Shader, implements [Fluent Design System principles](https://www.microsoft.com/design/fluent/#/), and remain performant on mixed reality devices.</span></span>
<br>

## <a name="examples-of-visual-effects-using-mrtk-standard-shader"></a><span data-ttu-id="61e98-109">Exemples d’effets visuels utilisant le nuanceur standard MRTK</span><span class="sxs-lookup"><span data-stu-id="61e98-109">Examples of visual effects using MRTK Standard shader</span></span> 
:::row:::
    :::column:::
       <span data-ttu-id="61e98-110">![Déplacer](images/UX/UX_Button_Affordance_ProximityLight.jpg)</span><span class="sxs-lookup"><span data-stu-id="61e98-110">![Move](images/UX/UX_Button_Affordance_ProximityLight.jpg)</span></span><br>
       <span data-ttu-id="61e98-111">**Lumière de proximité**</span><span class="sxs-lookup"><span data-stu-id="61e98-111">**Proximity light**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="61e98-112">![Faire pivoter](images/UX/UX_Button_Affordance_FocusHighlight.jpg)</span><span class="sxs-lookup"><span data-stu-id="61e98-112">![Rotate](images/UX/UX_Button_Affordance_FocusHighlight.jpg)</span></span><br>
        <span data-ttu-id="61e98-113">**Bordure claire**</span><span class="sxs-lookup"><span data-stu-id="61e98-113">**Border light**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="mrtk-standard-shader-in-mrtk-mixed-reality-toolkit-for-unity"></a><span data-ttu-id="61e98-114">Nuanceur standard MRTK dans MRTK (Mixed Reality Toolkit) pour Unity</span><span class="sxs-lookup"><span data-stu-id="61e98-114">MRTK Standard shader in MRTK (Mixed Reality Toolkit) for Unity</span></span>

* [<span data-ttu-id="61e98-115">MRTK-nuanceur standard</span><span class="sxs-lookup"><span data-stu-id="61e98-115">MRTK - Standard shader</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_MRTKStandardShader.html)


<br>

---

## <a name="see-also"></a><span data-ttu-id="61e98-116">Articles associés</span><span class="sxs-lookup"><span data-stu-id="61e98-116">See also</span></span>

* [<span data-ttu-id="61e98-117">Curseurs</span><span class="sxs-lookup"><span data-stu-id="61e98-117">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="61e98-118">Rayon émanant de la main</span><span class="sxs-lookup"><span data-stu-id="61e98-118">Hand ray</span></span>](point-and-commit.md)
* [<span data-ttu-id="61e98-119">Button</span><span class="sxs-lookup"><span data-stu-id="61e98-119">Button</span></span>](button.md)
* [<span data-ttu-id="61e98-120">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="61e98-120">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="61e98-121">Rectangle englobant et barre de l’application</span><span class="sxs-lookup"><span data-stu-id="61e98-121">Bounding box and App bar</span></span>](app-bar-and-bounding-box.md)
* [<span data-ttu-id="61e98-122">Manipulation</span><span class="sxs-lookup"><span data-stu-id="61e98-122">Manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="61e98-123">Menu de la main</span><span class="sxs-lookup"><span data-stu-id="61e98-123">Hand menu</span></span>](hand-menu.md)
* [<span data-ttu-id="61e98-124">Menu proche</span><span class="sxs-lookup"><span data-stu-id="61e98-124">Near menu</span></span>](near-menu.md)
* [<span data-ttu-id="61e98-125">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="61e98-125">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="61e98-126">Commande vocale</span><span class="sxs-lookup"><span data-stu-id="61e98-126">Voice command</span></span>](voice-input.md)
* [<span data-ttu-id="61e98-127">Clavier</span><span class="sxs-lookup"><span data-stu-id="61e98-127">Keyboard</span></span>](keyboard.md)
* [<span data-ttu-id="61e98-128">Info-bulle</span><span class="sxs-lookup"><span data-stu-id="61e98-128">Tooltip</span></span>](tooltip.md)
* [<span data-ttu-id="61e98-129">Tablette</span><span class="sxs-lookup"><span data-stu-id="61e98-129">Slate</span></span>](slate.md)
* [<span data-ttu-id="61e98-130">Curseur</span><span class="sxs-lookup"><span data-stu-id="61e98-130">Slider</span></span>](slider.md)
* [<span data-ttu-id="61e98-131">Billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="61e98-131">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
* [<span data-ttu-id="61e98-132">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="61e98-132">Displaying progress</span></span>](progress.md)
* [<span data-ttu-id="61e98-133">Aimantation de surface</span><span class="sxs-lookup"><span data-stu-id="61e98-133">Surface magnetism</span></span>](surface-magnetism.md)
