---
title: Visualisation de maillage spatial
author: cre8ivepark
ms.author: dongpark
ms.date: 06/19/2020
ms.topic: article
keywords: Réalité mixte, HoloLens, contrôles d’interface utilisateur, interaction, interface utilisateur, expérience utilisateur, conception UX, interface utilisateur spatiale, interaction spatiale, interface utilisateur 3D, expérience utilisateur 3D
ms.openlocfilehash: 17a799dcaba5caf4dd7018f8289cad02b40f1277
ms.sourcegitcommit: 7ca383ef1c5dc895ca2a289435f2e9d4c1ee6e65
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85346112"
---
# <a name="spatial-mesh"></a><span data-ttu-id="784f2-103">Maillage spatial</span><span class="sxs-lookup"><span data-stu-id="784f2-103">Spatial mesh</span></span>

![Maillage spatial](images/UX/MRTK_PulseShader_SpatialMesh.gif)

<span data-ttu-id="784f2-105">Grâce à la visualisation de maillage spatial, l’utilisateur peut apprendre comment un appareil perçoit et comprend l’environnement physique.</span><span class="sxs-lookup"><span data-stu-id="784f2-105">Through the spatial mesh visualization, the user can learn how a device perceives and understands the physical environment.</span></span> <span data-ttu-id="784f2-106">En plus de fournir un contexte spatial, la visualisation de maillage spatial appropriée peut créer une expérience délicieuse et magique.</span><span class="sxs-lookup"><span data-stu-id="784f2-106">In addition to providing spatial context, proper spatial mesh visualization can create a delightful and magical experience.</span></span>  

## <a name="design-guideline"></a><span data-ttu-id="784f2-107">Directives de conception</span><span class="sxs-lookup"><span data-stu-id="784f2-107">Design guideline</span></span>
<span data-ttu-id="784f2-108">Étant donné qu’il est important d’autoriser l’utilisateur à se concentrer et à interagir avec le contenu, la visualisation continue et répétée du maillage spatial en arrière-plan peut être gênante.</span><span class="sxs-lookup"><span data-stu-id="784f2-108">Since it's important to allow the user to focus and interact with content, continuous and repeated visualization of the spatial mesh in the background could be distracting.</span></span> <span data-ttu-id="784f2-109">Il est recommandé de visualiser l’environnement avec modération, qu’une seule fois au lancement initial ou lorsque l’utilisateur montre clairement l’intention de voir la maille environnementale en ciblant et en appuyant sur de l’air.</span><span class="sxs-lookup"><span data-stu-id="784f2-109">It is recommended to visualize the environment sparingly, either only once in the initial launch or when the user shows clear intention to see the environmental mesh by targeting and air-tapping space.</span></span> <span data-ttu-id="784f2-110">Vous pouvez observer ce comportement dans l’interpréteur de commandes HoloLens.</span><span class="sxs-lookup"><span data-stu-id="784f2-110">You can observe this behavior in the HoloLens shell.</span></span>
<br>


## <a name="spatial-mesh-visualization-in-mrtk-mixed-reality-toolkit-for-unity"></a><span data-ttu-id="784f2-111">Visualisation de maillage spatial dans MRTK (ensemble d’outils de réalité mixte) pour Unity</span><span class="sxs-lookup"><span data-stu-id="784f2-111">Spatial mesh visualization in MRTK (Mixed Reality Toolkit) for Unity</span></span>
<span data-ttu-id="784f2-112">MRTK fournit plusieurs documents pour la visualisation de maillage spatial.</span><span class="sxs-lookup"><span data-stu-id="784f2-112">MRTK provides several materials for the spatial mesh visualization.</span></span>

- <span data-ttu-id="784f2-113">**MRTK_Wireframe. mat, MRTK_Wireframe. mat**: matériau de maillage spatial statique par défaut qui affiche les contours de maillage sans animation.</span><span class="sxs-lookup"><span data-stu-id="784f2-113">**MRTK_Wireframe.mat, MRTK_Wireframe.mat**: Default static spatial mesh material which shows the mesh outlines without animation.</span></span> <span data-ttu-id="784f2-114">Ce document est utile à des fins de débogage, car il affiche les géométries entières du maillage spatial.</span><span class="sxs-lookup"><span data-stu-id="784f2-114">This material is useful for debugging purposes since it shows the entire spatial mesh geometries.</span></span> <span data-ttu-id="784f2-115">Toutefois, il n’est pas recommandé pour la production.</span><span class="sxs-lookup"><span data-stu-id="784f2-115">However, it is not recommended for production.</span></span>
<br>
<img src="images/SurfaceReconstruction.jpg" alt="Wireframe spatial mesh visualization" width="640px">

- <span data-ttu-id="784f2-116">**MRTK_SurfaceReconstruction. mat**: ce matériau vous donne un effet d’impulsion animée sur le maillage spatial.</span><span class="sxs-lookup"><span data-stu-id="784f2-116">**MRTK_SurfaceReconstruction.mat**: This material gives you an animated pulse effect on the spatial mesh.</span></span> <span data-ttu-id="784f2-117">Vous pouvez utiliser ce document pour visualiser l’environnement à un moment précis de votre expérience ou sur l’entrée d’air de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="784f2-117">You can use this material to visualize the environment at a specific moment of your experience or on the user's air-tap input.</span></span> <span data-ttu-id="784f2-118">Consultez la scène **PulseShaderExamples. Unity** pour obtenir des exemples.</span><span class="sxs-lookup"><span data-stu-id="784f2-118">See **PulseShaderExamples.unity** scene for the examples.</span></span>
<br>
<img src="images/UX/MRTK_SRMesh_Pulse.jpg" alt="Pulse spatial mesh visualization" width="640px">
* <span data-ttu-id="784f2-119">Pour plus d’informations, consultez [MRTK-spatial awarenes](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/SpatialAwareness/SpatialAwarenessGettingStarted.html) et [MRTK-Pulse Shader](https://microsoft.github.io/MixedRealityToolkit-Unity/Assets/MRTK/SDK/Experimental/PulseShader/README.html) .</span><span class="sxs-lookup"><span data-stu-id="784f2-119">Please see [MRTK - Spatial Awareness](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/SpatialAwareness/SpatialAwarenessGettingStarted.html) and [MRTK - Pulse Shader](https://microsoft.github.io/MixedRealityToolkit-Unity/Assets/MRTK/SDK/Experimental/PulseShader/README.html) for more details.</span></span>

<br>

---

## <a name="see-also"></a><span data-ttu-id="784f2-120">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="784f2-120">See also</span></span>

* [<span data-ttu-id="784f2-121">Curseurs</span><span class="sxs-lookup"><span data-stu-id="784f2-121">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="784f2-122">Rayon émanant de la main</span><span class="sxs-lookup"><span data-stu-id="784f2-122">Hand ray</span></span>](point-and-commit.md)
* [<span data-ttu-id="784f2-123">Button</span><span class="sxs-lookup"><span data-stu-id="784f2-123">Button</span></span>](button.md)
* [<span data-ttu-id="784f2-124">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="784f2-124">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="784f2-125">Rectangle englobant et barre de l’application</span><span class="sxs-lookup"><span data-stu-id="784f2-125">Bounding box and App bar</span></span>](app-bar-and-bounding-box.md)
* [<span data-ttu-id="784f2-126">Manipulation</span><span class="sxs-lookup"><span data-stu-id="784f2-126">Manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="784f2-127">Menu de la main</span><span class="sxs-lookup"><span data-stu-id="784f2-127">Hand menu</span></span>](hand-menu.md)
* [<span data-ttu-id="784f2-128">Menu proche</span><span class="sxs-lookup"><span data-stu-id="784f2-128">Near menu</span></span>](near-menu.md)
* [<span data-ttu-id="784f2-129">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="784f2-129">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="784f2-130">Commande vocale</span><span class="sxs-lookup"><span data-stu-id="784f2-130">Voice command</span></span>](voice-input.md)
* [<span data-ttu-id="784f2-131">Clavier</span><span class="sxs-lookup"><span data-stu-id="784f2-131">Keyboard</span></span>](keyboard.md)
* [<span data-ttu-id="784f2-132">Info-bulle</span><span class="sxs-lookup"><span data-stu-id="784f2-132">Tooltip</span></span>](tooltip.md)
* [<span data-ttu-id="784f2-133">Tablette</span><span class="sxs-lookup"><span data-stu-id="784f2-133">Slate</span></span>](slate.md)
* [<span data-ttu-id="784f2-134">Curseur</span><span class="sxs-lookup"><span data-stu-id="784f2-134">Slider</span></span>](slider.md)
* [<span data-ttu-id="784f2-135">Nuanceur</span><span class="sxs-lookup"><span data-stu-id="784f2-135">Shader</span></span>](shader.md)
* [<span data-ttu-id="784f2-136">Billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="784f2-136">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
* [<span data-ttu-id="784f2-137">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="784f2-137">Displaying progress</span></span>](progress.md)
* [<span data-ttu-id="784f2-138">Aimantation de surface</span><span class="sxs-lookup"><span data-stu-id="784f2-138">Surface magnetism</span></span>](surface-magnetism.md)
