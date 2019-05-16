---
title: Systèmes de coordonnées dans DirectX
description: Explique comment utiliser les localisateurs spatiales Windows Mixed Reality, trames de référence, ancres spatiales et systèmes de coordonnées, comment utiliser le SpatialStage, comment gérer la perte de suivi, comment enregistrer et charger les ancres et comment réaliser des opérations d’image stabilisation.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: Mixte réalité, le localisateur spatiale, cadre de référence spatiale, système de coordonnées spatial, étape spatiale, exemple de code, stabilisation de l’image, spatiale d’ancrage, Boutique spatiale, perte de suivi, procédure pas à pas
ms.openlocfilehash: 5a48e0a829ba8647718e28ec20760d8a764b13fe
ms.sourcegitcommit: 45676da11ebe33a2aa3dccec0e8ad7d714420853
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65628974"
---
# <a name="coordinate-systems-in-directx"></a><span data-ttu-id="dd136-104">Systèmes de coordonnées dans DirectX</span><span class="sxs-lookup"><span data-stu-id="dd136-104">Coordinate systems in DirectX</span></span>

<span data-ttu-id="dd136-105">[Systèmes de coordonnées](coordinate-systems.md) constituent la base pour comprendre spatial proposée par les API de réalité mixte Windows.</span><span class="sxs-lookup"><span data-stu-id="dd136-105">[Coordinate systems](coordinate-systems.md) form the basis for spatial understanding offered by Windows Mixed Reality APIs.</span></span>

<span data-ttu-id="dd136-106">Aujourd'hui assis VR ou appareils de salle d’unique de VR établissent un système de coordonnées principal pour représenter leur espace suivie.</span><span class="sxs-lookup"><span data-stu-id="dd136-106">Today's seated VR or single-room VR devices establish one primary coordinate system to represent their tracked space.</span></span> <span data-ttu-id="dd136-107">Les appareils Windows Mixed Reality comme HoloLens sont conçues pour être utilisées dans les environnements de grande taille non définis, avec l’appareil de découvrir et apprendre à connaître son environnement en tant que l’utilisateur parcourt autour.</span><span class="sxs-lookup"><span data-stu-id="dd136-107">Windows Mixed Reality devices such as HoloLens are designed to be used throughout large undefined environments, with the device discovering and learning about its surroundings as the user walks around.</span></span> <span data-ttu-id="dd136-108">Cela permet à l’appareil pour s’adapter à améliorer continuellement connaissance des salles de l’utilisateur, mais les résultats dans les systèmes de coordonnées qui va changer leur relation un à l’autre pendant la durée de vie de l’application.</span><span class="sxs-lookup"><span data-stu-id="dd136-108">This allows the device to adapt to continually-improving knowledge about the user's rooms, but results in coordinate systems that will change their relationship to one another through the lifetime of the app.</span></span> <span data-ttu-id="dd136-109">Réalité mixte Windows prend en charge un large éventail d’appareils, allant des casques IMMERSIFS assis via des trames de référence connecté au monde.</span><span class="sxs-lookup"><span data-stu-id="dd136-109">Windows Mixed Reality supports a wide spectrum of devices, ranging from seated immersive headsets through world-attached reference frames.</span></span>

>[!NOTE]
><span data-ttu-id="dd136-110">Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="dd136-110">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="dd136-111">Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="dd136-111">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

## <a name="spatial-coordinate-systems-in-windows"></a><span data-ttu-id="dd136-112">Systèmes de coordonnées spatiales dans Windows</span><span class="sxs-lookup"><span data-stu-id="dd136-112">Spatial coordinate systems in Windows</span></span>

<span data-ttu-id="dd136-113">Le type de base permet de raisonner sur les systèmes de coordonnées de monde réel dans Windows est le <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a>.</span><span class="sxs-lookup"><span data-stu-id="dd136-113">The core type used to reason about real-world coordinate systems in Windows is the <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a>.</span></span> <span data-ttu-id="dd136-114">Une instance de ce type représente un système de coordonnées arbitraire et fournit une méthode pour obtenir une matrice de transformation que vous pouvez utiliser pour transformer entre deux systèmes de coordonnées sans avoir à comprendre les détails de chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="dd136-114">An instance of this type represents an arbitrary coordinate system and provides a method to get a transformation matrix that you can use to transform between two coordinate systems without understanding the details of each.</span></span>

<span data-ttu-id="dd136-115">Les méthodes qui retournent des informations spatiales, représentées en tant que points, les rayons ou les volumes dans son environnement de l’utilisateur, accepte un paramètre SpatialCoordinateSystem pour vous permettre de décider le système de coordonnées dans lequel il est très utile pour ces coordonnées à retourner.</span><span class="sxs-lookup"><span data-stu-id="dd136-115">Methods that return spatial information, represented as points, rays, or volumes in the user's surroundings, will accept a SpatialCoordinateSystem parameter to let you decide the coordinate system in which it's most useful for those coordinates to be returned.</span></span> <span data-ttu-id="dd136-116">Les unités pour ces coordonnées sera toujours en mètres.</span><span class="sxs-lookup"><span data-stu-id="dd136-116">The units for these coordinates will always be in meters.</span></span>

<span data-ttu-id="dd136-117">Un SpatialCoordinateSystem a une relation dynamique avec d’autres systèmes de coordonnées, y compris ceux qui représentent la position de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="dd136-117">A SpatialCoordinateSystem has a dynamic relationship with other coordinate systems, including those that represent the device's position.</span></span> <span data-ttu-id="dd136-118">À tout moment dans le temps, l’appareil peut être en mesure de localiser des systèmes de coordonnées et d’autres non.</span><span class="sxs-lookup"><span data-stu-id="dd136-118">At any point in time, the device may be able to locate some coordinate systems and not others.</span></span> <span data-ttu-id="dd136-119">Pour la plupart des systèmes de coordonnées, votre application doit être prête à gérer les périodes de temps pendant laquelle ils ne peut pas être localisés.</span><span class="sxs-lookup"><span data-stu-id="dd136-119">For most coordinate systems, your app must be ready to handle periods of time during which they cannot be located.</span></span>

<span data-ttu-id="dd136-120">Votre application ne doit pas créer directement SpatialCoordinateSystems - plutôt qu’ils doivent être utilisées via les API de Perception.</span><span class="sxs-lookup"><span data-stu-id="dd136-120">Your application should not create SpatialCoordinateSystems directly - rather they should be consumed via the Perception APIs.</span></span> <span data-ttu-id="dd136-121">Il existe trois sources principales de systèmes de coordonnées dans les API de Perception, chacun d'entre eux mappe à un concept décrit sur le [systèmes de coordonnées](coordinate-systems.md) page :</span><span class="sxs-lookup"><span data-stu-id="dd136-121">There are three primary sources of coordinate systems in the Perception APIs, each of which map to a concept described on the [Coordinate systems](coordinate-systems.md) page:</span></span>
* <span data-ttu-id="dd136-122">Pour obtenir un système de référence stationnaire, créez un <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstationaryframeofreference" target="_blank">SpatialStationaryFrameOfReference</a> ou obtenir un auprès d’actuel <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference" target="_blank">SpatialStageFrameOfReference</a>.</span><span class="sxs-lookup"><span data-stu-id="dd136-122">To get a stationary frame of reference, create a <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstationaryframeofreference" target="_blank">SpatialStationaryFrameOfReference</a> or obtain one from the current <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference" target="_blank">SpatialStageFrameOfReference</a>.</span></span>
* <span data-ttu-id="dd136-123">Pour obtenir un point d’ancrage spatial, créez un <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a>.</span><span class="sxs-lookup"><span data-stu-id="dd136-123">To get a spatial anchor, create a <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a>.</span></span>
* <span data-ttu-id="dd136-124">Pour obtenir un cadre de référence jointe, créez un <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocatorattachedframeofreference" target="_blank">SpatialLocatorAttachedFrameOfReference</a>.</span><span class="sxs-lookup"><span data-stu-id="dd136-124">To get an attached frame of reference, create a <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocatorattachedframeofreference" target="_blank">SpatialLocatorAttachedFrameOfReference</a>.</span></span>

<span data-ttu-id="dd136-125">Tous les systèmes de coordonnées retournées par ces objets sont droitiers avec + y haut + x à droite et + z vers l’arrière.</span><span class="sxs-lookup"><span data-stu-id="dd136-125">All of the coordinate systems returned by these objects are right-handed, with +y up, +x to the right and +z backwards.</span></span> <span data-ttu-id="dd136-126">Vous pouvez mémoriser le sens dans lequel les points de l’axe z positif en pointant vers les doigts de votre gauche ou droite dans le sens positif x et les utiliser curl dans l’axe y positif.</span><span class="sxs-lookup"><span data-stu-id="dd136-126">You can remember which direction the positive z-axis points by pointing the fingers of either your left or right hand in the positive x direction and curling them into the positive y direction.</span></span> <span data-ttu-id="dd136-127">La direction vers laquelle pointe votre pouce (vers vous ou à l'opposé) correspond à la direction dans laquelle pointe l’axe z positif pour ce système de coordonnées.</span><span class="sxs-lookup"><span data-stu-id="dd136-127">The direction your thumb points, either toward or away from you, is the direction that the positive z-axis points for that coordinate system.</span></span> <span data-ttu-id="dd136-128">L’illustration suivante décrit ces deux systèmes de coordonnées.</span><span class="sxs-lookup"><span data-stu-id="dd136-128">The following illustration shows these two coordinate systems.</span></span>

<span data-ttu-id="dd136-129">![Systèmes de coordonnées de gauche et droite](images/left-hand-right-hand.gif)</span><span class="sxs-lookup"><span data-stu-id="dd136-129">![Left-hand and right-hand coordinate systems](images/left-hand-right-hand.gif)</span></span><br>
<span data-ttu-id="dd136-130">*Systèmes de coordonnées de gauche et droite*</span><span class="sxs-lookup"><span data-stu-id="dd136-130">*Left-hand and right-hand coordinate systems*</span></span>

<span data-ttu-id="dd136-131">Pour l’amorçage dans un SpatialCoordinateSystem selon la position d’un HoloLens, utilisez le <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a> classe pour créer soit une jointe ou stationnaire de référence, comme décrit dans les sections ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="dd136-131">To bootstrap into a SpatialCoordinateSystem based on the position of a HoloLens, use the <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a> class to create either an attached or stationary frame of reference, as described in the sections below.</span></span>

## <a name="place-holograms-in-the-world-using-a-spatial-stage"></a><span data-ttu-id="dd136-132">Hologrammes place dans le monde à l’aide d’une phase spatiale</span><span class="sxs-lookup"><span data-stu-id="dd136-132">Place holograms in the world using a spatial stage</span></span>

<span data-ttu-id="dd136-133">Le système de coordonnées pour des casques IMMERSIFS Windows Mixed Reality opaques est accessible à l’aide de la méthode statique <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference.current" target="_blank">SpatialStageFrameOfReference::Current</a> propriété.</span><span class="sxs-lookup"><span data-stu-id="dd136-133">The coordinate system for opaque Windows Mixed Reality immersive headsets is accessed using the static <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference.current" target="_blank">SpatialStageFrameOfReference::Current</a> property.</span></span> <span data-ttu-id="dd136-134">Cette API fournit un système de coordonnées, les informations sur indique si le lecteur est inséré ou mobiles, la limite d’une zone de sécurité pour vous épargne si le lecteur est mobile, et indique s’il faut ou non le casque est directionnel.</span><span class="sxs-lookup"><span data-stu-id="dd136-134">This API provides a coordinate system, information about whether the player is seated or mobile, the boundary of a safe area for walking around if the player is mobile, and an indication of whether or not the headset is directional.</span></span> <span data-ttu-id="dd136-135">Il existe également un gestionnaire d’événements pour les mises à jour à l’étape spatiale.</span><span class="sxs-lookup"><span data-stu-id="dd136-135">There is also an event handler for updates to the spatial stage.</span></span>

<span data-ttu-id="dd136-136">Tout d’abord, nous avons obtenir la scène spatiale et s’abonner pour les mises à jour correspondantes :</span><span class="sxs-lookup"><span data-stu-id="dd136-136">First, we get the spatial stage and subscribe for updates to it:</span></span> 

<span data-ttu-id="dd136-137">Code pour **l’initialisation de phase spatiale**</span><span class="sxs-lookup"><span data-stu-id="dd136-137">Code for **Spatial stage initialization**</span></span>

```
SpatialStageManager::SpatialStageManager(
    const std::shared_ptr<DX::DeviceResources>& deviceResources, 
    const std::shared_ptr<SceneController>& sceneController)
    : m_deviceResources(deviceResources), m_sceneController(sceneController)
{
    // Get notified when the stage is updated.
    m_spatialStageChangedEventToken = SpatialStageFrameOfReference::CurrentChanged +=
        ref new EventHandler<Object^>(std::bind(&SpatialStageManager::OnCurrentChanged, this, _1));

    // Make sure to get the current spatial stage.
    OnCurrentChanged(nullptr);
}
```

<span data-ttu-id="dd136-138">Dans la méthode OnCurrentChanged, votre application doit inspecter la scène spatiale et mettre à jour l’expérience de joueur en conséquence.</span><span class="sxs-lookup"><span data-stu-id="dd136-138">In the OnCurrentChanged method, your app should inspect the spatial stage and update the player experience accordingly.</span></span> <span data-ttu-id="dd136-139">Dans cet exemple, nous fournissons une visualisation de la limite de la scène, ainsi que la position de début spécifiée par l’utilisateur et de la plage de la phase de vue et de la gamme de déplacement des propriétés.</span><span class="sxs-lookup"><span data-stu-id="dd136-139">In this example, we provide a visualization of the stage boundary, as well as the start position specified by the user and the stage's range of view and range of movement properties.</span></span> <span data-ttu-id="dd136-140">Nous avons également revenir à notre propre système de coordonnées stationnaire, lorsqu’une étape ne peut pas être fournie.</span><span class="sxs-lookup"><span data-stu-id="dd136-140">We also fall back to our own stationary coordinate system, when a stage cannot be provided.</span></span>


<span data-ttu-id="dd136-141">Code pour **mise à jour de la phase spatiale**</span><span class="sxs-lookup"><span data-stu-id="dd136-141">Code for **Spatial stage update**</span></span>

```
void SpatialStageManager::OnCurrentChanged(Object^ /*o*/)
{
    // The event notifies us that a new stage is available.
    // Get the current stage.
    m_currentStage = SpatialStageFrameOfReference::Current;

    // Clear previous content.
    m_sceneController->ClearSceneObjects();

    if (m_currentStage != nullptr)
    {
        // Obtain stage geometry.
        auto stageCoordinateSystem = m_currentStage->CoordinateSystem;
        auto boundsVertexArray = m_currentStage->TryGetMovementBounds(stageCoordinateSystem);

        // Visualize the area where the user can move around.
        std::vector<float3> boundsVertices;
        boundsVertices.resize(boundsVertexArray->Length);
        memcpy(boundsVertices.data(), boundsVertexArray->Data, boundsVertexArray->Length * sizeof(float3));
        std::vector<unsigned short> indices = TriangulatePoints(boundsVertices);
        m_stageBoundsShape =
            std::make_shared<SceneObject>(
                    m_deviceResources,
                    reinterpret_cast<std::vector<XMFLOAT3>&>(boundsVertices),
                    indices,
                    XMFLOAT3(DirectX::Colors::SeaGreen),
                    stageCoordinateSystem);
        m_sceneController->AddSceneObject(m_stageBoundsShape);

        // In this sample, we draw a visual indicator for some spatial stage properties.
        // If the view is forward-only, the indicator is a half circle pointing forward - otherwise, it
        // is a full circle.
        // If the user can walk around, the indicator is blue. If the user is seated, it is red.

        // The indicator is rendered at the origin - which is where the user declared the center of the
        // stage to be during setup - above the plane of the stage bounds object.
        float3 visibleAreaCenter = float3(0.f, 0.001f, 0.f);

        // Its shape depends on the look direction range.
        std::vector<float3> visibleAreaIndicatorVertices;
        if (m_currentStage->LookDirectionRange == SpatialLookDirectionRange::ForwardOnly)
        {
            // Half circle for forward-only look direction range.
            visibleAreaIndicatorVertices = CreateCircle(visibleAreaCenter, 0.25f, 9, XM_PI);
        }
        else
        {
            // Full circle for omnidirectional look direction range.
            visibleAreaIndicatorVertices = CreateCircle(visibleAreaCenter, 0.25f, 16, XM_2PI);
        }

        // Its color depends on the movement range.
        XMFLOAT3 visibleAreaColor;
        if (m_currentStage->MovementRange == SpatialMovementRange::NoMovement)
        {
            visibleAreaColor = XMFLOAT3(DirectX::Colors::OrangeRed);
        }
        else
        {
            visibleAreaColor = XMFLOAT3(DirectX::Colors::Aqua);
        }

        std::vector<unsigned short> visibleAreaIndicatorIndices = TriangulatePoints(visibleAreaIndicatorVertices);

        // Visualize the look direction range.
        m_stageVisibleAreaIndicatorShape =
            std::make_shared<SceneObject>(
                    m_deviceResources,
                    reinterpret_cast<std::vector<XMFLOAT3>&>(visibleAreaIndicatorVertices),
                    visibleAreaIndicatorIndices,
                    visibleAreaColor,
                    stageCoordinateSystem);
        m_sceneController->AddSceneObject(m_stageVisibleAreaIndicatorShape);
    }
    else
    {
        // No spatial stage was found.
        // Fall back to a stationary coordinate system.
        auto locator = SpatialLocator::GetDefault();
        if (locator)
        {
            m_stationaryFrameOfReference = locator->CreateStationaryFrameOfReferenceAtCurrentLocation();

            // Render an indicator, so that we know we fell back to a mode without a stage.
            std::vector<float3> visibleAreaIndicatorVertices;
            float3 visibleAreaCenter = float3(0.f, -2.0f, 0.f);
            visibleAreaIndicatorVertices = CreateCircle(visibleAreaCenter, 0.125f, 16, XM_2PI);
            std::vector<unsigned short> visibleAreaIndicatorIndices = TriangulatePoints(visibleAreaIndicatorVertices);
            m_stageVisibleAreaIndicatorShape =
                std::make_shared<SceneObject>(
                    m_deviceResources,
                    reinterpret_cast<std::vector<XMFLOAT3>&>(visibleAreaIndicatorVertices),
                    visibleAreaIndicatorIndices,
                    XMFLOAT3(DirectX::Colors::LightSlateGray),
                    m_stationaryFrameOfReference->CoordinateSystem);
            m_sceneController->AddSceneObject(m_stageVisibleAreaIndicatorShape);
        }
    }
}
```

<span data-ttu-id="dd136-142">L’ensemble de sommets qui définissent la limite étape sont fournies dans le sens horaire.</span><span class="sxs-lookup"><span data-stu-id="dd136-142">The set of vertices that define the stage boundary are provided in clockwise order.</span></span> <span data-ttu-id="dd136-143">L’interpréteur de commandes Windows Mixed Reality Dessine une frontière de sécurité à la limite lors de l’utilisateur à l’approche ; Vous pouvez souhaiter triangularize la zone opérationnel pour vos propres besoins.</span><span class="sxs-lookup"><span data-stu-id="dd136-143">The Windows Mixed Reality shell draws a fence at the boundary when the user approaches it; you may wish to triangularize the walkable area for your own purposes.</span></span> <span data-ttu-id="dd136-144">L’algorithme suivant peut être utilisé pour triangularize la scène.</span><span class="sxs-lookup"><span data-stu-id="dd136-144">The following algorithm can be used to triangularize the stage.</span></span>


<span data-ttu-id="dd136-145">Code pour **triangularization de phase spatiale**</span><span class="sxs-lookup"><span data-stu-id="dd136-145">Code for **Spatial stage triangularization**</span></span>

```
std::vector<unsigned short> SpatialStageManager::TriangulatePoints(std::vector<float3> const& vertices)
{
    size_t const& vertexCount = vertices.size();

    // Segments of the shape are removed as they are triangularized.
    std::vector<bool> vertexRemoved;
    vertexRemoved.resize(vertexCount, false);
    unsigned int vertexRemovedCount = 0;

    // Indices are used to define triangles.
    std::vector<unsigned short> indices;

    // Decompose into convex segments.
    unsigned short currentVertex = 0;
    while (vertexRemovedCount < (vertexCount - 2))
    {
        // Get next triangle:
        // Start with the current vertex.
        unsigned short index1 = currentVertex;

        // Get the next available vertex.
        unsigned short index2 = index1 + 1;

        // This cycles to the next available index.
        auto CycleIndex = [=](unsigned short indexToCycle, unsigned short stopIndex)
        {
            // Make sure the index does not exceed bounds.
            if (indexToCycle >= unsigned short(vertexCount))
            {
                indexToCycle -= unsigned short(vertexCount);
            }

            while (vertexRemoved[indexToCycle])
            {
                // If the vertex is removed, go to the next available one.
                ++indexToCycle;

                // Make sure the index does not exceed bounds.
                if (indexToCycle >= unsigned short(vertexCount))
                {
                    indexToCycle -= unsigned short(vertexCount);
                }

                // Prevent cycling all the way around.
                // Should not be needed, as we limit with the vertex count.
                if (indexToCycle == stopIndex)
                {
                    break;
                }
            }

            return indexToCycle;
        };
        index2 = CycleIndex(index2, index1);

        // Get the next available vertex after that.
        unsigned short index3 = index2 + 1;
        index3 = CycleIndex(index3, index1);

        // Vertices that may define a triangle inside the 2D shape.
        auto& v1 = vertices[index1];
        auto& v2 = vertices[index2];
        auto& v3 = vertices[index3];

        // If the projection of the first segment (in clockwise order) onto the second segment is 
        // positive, we know that the clockwise angle is less than 180 degrees, which tells us 
        // that the triangle formed by the two segments is contained within the bounding shape.
        auto v2ToV1 = v1 - v2;
        auto v2ToV3 = v3 - v2;
        float3 normalToV2ToV3 = { -v2ToV3.z, 0.f, v2ToV3.x };
        float projectionOntoNormal = dot(v2ToV1, normalToV2ToV3);
        if (projectionOntoNormal >= 0)
        {
            // Triangle is contained within the 2D shape.

            // Remove peak vertex from the list.
            vertexRemoved[index2] = true;
            ++vertexRemovedCount;

            // Create the triangle.
            indices.push_back(index1);
            indices.push_back(index2);
            indices.push_back(index3);

            // Continue on to the next outer triangle.
            currentVertex = index3;
        }
        else
        {
            // Triangle is a cavity in the 2D shape.
            // The next triangle starts at the inside corner.
            currentVertex = index2;
        }
    }

    indices.shrink_to_fit();
    return indices;
}
```

## <a name="place-holograms-in-the-world-using-a-stationary-frame-of-reference"></a><span data-ttu-id="dd136-146">Hologrammes place dans le monde à l’aide d’un système de référence stationnaire</span><span class="sxs-lookup"><span data-stu-id="dd136-146">Place holograms in the world using a stationary frame of reference</span></span>

<span data-ttu-id="dd136-147">Le [SpatialStationaryFrameOfReference](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialstationaryframeofreference.aspx) classe représente une image de référence qui [reste stationnaire](coordinate-systems.md#stationary-frame-of-reference) par rapport aux environs de l’utilisateur en tant que l’utilisateur se déplace.</span><span class="sxs-lookup"><span data-stu-id="dd136-147">The [SpatialStationaryFrameOfReference](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialstationaryframeofreference.aspx) class represents a frame of reference that [remains stationary](coordinate-systems.md#stationary-frame-of-reference) relative to the user's surroundings as the user moves around.</span></span> <span data-ttu-id="dd136-148">Ce cadre de référence hiérarchise les coordonnées de conservation stable près de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="dd136-148">This frame of reference prioritizes keeping coordinates stable near the device.</span></span> <span data-ttu-id="dd136-149">Une des principales utilisations d’un SpatialStationaryFrameOfReference consiste à agir en tant que le système de coordonnées de monde sous-jacent au sein d’un moteur de rendu lors du rendu hologrammes.</span><span class="sxs-lookup"><span data-stu-id="dd136-149">One key use of a SpatialStationaryFrameOfReference is to act as the underlying world coordinate system within a rendering engine when rendering holograms.</span></span>

<span data-ttu-id="dd136-150">Pour obtenir un SpatialStationaryFrameOfReference, utilisez le [SpatialLocator](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatiallocator.aspx) classe et appelez [CreateStationaryFrameOfReferenceAtCurrentLocation](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatiallocator.createstationaryframeofreferenceatcurrentlocation.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd136-150">To get a SpatialStationaryFrameOfReference, use the [SpatialLocator](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatiallocator.aspx) class and call [CreateStationaryFrameOfReferenceAtCurrentLocation](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatiallocator.createstationaryframeofreferenceatcurrentlocation.aspx).</span></span>

<span data-ttu-id="dd136-151">À partir du code du modèle application Windows HOLOGRAPHIQUE :</span><span class="sxs-lookup"><span data-stu-id="dd136-151">From the Windows Holographic app template code:</span></span>

```
           // The simplest way to render world-locked holograms is to create a stationary reference frame
           // when the app is launched. This is roughly analogous to creating a "world" coordinate system
           // with the origin placed at the device's position as the app is launched.
           referenceFrame = locator.CreateStationaryFrameOfReferenceAtCurrentLocation();
```
* <span data-ttu-id="dd136-152">Trames de référence stationnaire sont conçus pour fournir une position ajustée par rapport à l’espace global.</span><span class="sxs-lookup"><span data-stu-id="dd136-152">Stationary reference frames are designed to provide a best-fit position relative to the overall space.</span></span> <span data-ttu-id="dd136-153">Postes individuels dans ce cadre de référence sont autorisés à dérives légèrement.</span><span class="sxs-lookup"><span data-stu-id="dd136-153">Individual positions within that reference frame are allowed to drift slightly.</span></span> <span data-ttu-id="dd136-154">Ceci est normal que l’appareil en apprend plus sur l’environnement.</span><span class="sxs-lookup"><span data-stu-id="dd136-154">This is normal as the device learns more about the environment.</span></span>
* <span data-ttu-id="dd136-155">Lorsque le positionnement précis des hologrammes individuels est requis, un SpatialAnchor doit être utilisé pour ancrer l’hologramme individuel vers une position dans le monde réel : par exemple, un point de l’utilisateur indique le pour intéresser.</span><span class="sxs-lookup"><span data-stu-id="dd136-155">When precise placement of individual holograms is required, a SpatialAnchor should be used to anchor the individual hologram to a position in the real world - for example, a point the user indicates to be of special interest.</span></span> <span data-ttu-id="dd136-156">Les positions d’ancrage ne pas dérive, mais peuvent être corrigées ; le point d’ancrage utilise la position corrigée à partir de l’image suivante après la correction.</span><span class="sxs-lookup"><span data-stu-id="dd136-156">Anchor positions do not drift, but can be corrected; the anchor will use the corrected position starting in the next frame after the correction has occurred.</span></span>

## <a name="place-holograms-in-the-world-using-spatial-anchors"></a><span data-ttu-id="dd136-157">Hologrammes place dans le monde à l’aide de points d’ancrage spatiales</span><span class="sxs-lookup"><span data-stu-id="dd136-157">Place holograms in the world using spatial anchors</span></span>

<span data-ttu-id="dd136-158">[Ancres spatiales](coordinate-systems.md#spatial-anchors) sont un excellent moyen pour placer hologrammes à un emplacement spécifique dans le monde réel, avec le système en garantissant le point d’ancrage reste en place au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="dd136-158">[Spatial anchors](coordinate-systems.md#spatial-anchors) are a great way to place holograms at a specific place in the real world, with the system ensuring the anchor stays in place over time.</span></span> <span data-ttu-id="dd136-159">Cette rubrique explique comment créer et utiliser un point d’ancrage et l’utilisation des données de point d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="dd136-159">This topic explains how to create and use an anchor, and how to work with anchor data.</span></span>

<span data-ttu-id="dd136-160">Vous pouvez créer un SpatialAnchor à toute position et l’orientation dans le SpatialCoordinateSystem de votre choix.</span><span class="sxs-lookup"><span data-stu-id="dd136-160">You can create a SpatialAnchor at any position and orientation within the SpatialCoordinateSystem of your choosing.</span></span> <span data-ttu-id="dd136-161">L’appareil doit être en mesure de localiser ce système de coordonnées pour le moment, et le système ne doit pas avoir atteint sa limite ancres spatiales.</span><span class="sxs-lookup"><span data-stu-id="dd136-161">The device must be able to locate that coordinate system at the moment, and the system must not have reached its limit of spatial anchors.</span></span>

<span data-ttu-id="dd136-162">Une fois défini, le système de coordonnées d’un SpatialAnchor s’ajuste en permanence pour conserver la position précise et l’orientation de son emplacement initial.</span><span class="sxs-lookup"><span data-stu-id="dd136-162">Once defined, the coordinate system of a SpatialAnchor adjusts continually to retain the precise position and orientation of its initial location.</span></span> <span data-ttu-id="dd136-163">Vous pouvez ensuite utiliser cette SpatialAnchor pour restituer hologrammes apparaîtront fixes dans l’environnement de l’utilisateur à l’emplacement spécifié.</span><span class="sxs-lookup"><span data-stu-id="dd136-163">You can then use this SpatialAnchor to render holograms that will appear fixed in the user's surroundings at that exact location.</span></span>

<span data-ttu-id="dd136-164">Les effets des ajustements qui empêchent le point d’ancrage en place sont amplifient encore comme la distance à partir de l’augmentation d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="dd136-164">The effects of the adjustments that keep the anchor in place are magnified as distance from the anchor increases.</span></span> <span data-ttu-id="dd136-165">Par conséquent, vous devez éviter de restituer le contenu par rapport à un point d’ancrage est supérieure à 3 mètres à partir de l’origine de ce point d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="dd136-165">Therefore, you should avoid rendering content relative to an anchor that is more than about 3 meters from that anchor's origin.</span></span>

<span data-ttu-id="dd136-166">Le [CoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.coordinatesystem.aspx) propriété obtient un système de coordonnées qui vous permet de placer le contenu par rapport à l’ancre, avec accélération appliquée lorsque l’appareil s’ajuste l’emplacement précis de l’ancre.</span><span class="sxs-lookup"><span data-stu-id="dd136-166">The [CoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.coordinatesystem.aspx) property gets a coordinate system that lets you place content relative to the anchor, with easing applied when the device adjusts the anchor's precise location.</span></span>

<span data-ttu-id="dd136-167">Utilisez le [RawCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.rawcoordinatesystem.aspx) propriété et le correspondantes [RawCoordinateSystemAdjusted](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted.aspx) événement à gérer ces ajustements vous-même.</span><span class="sxs-lookup"><span data-stu-id="dd136-167">Use the [RawCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.rawcoordinatesystem.aspx) property and the corresponding [RawCoordinateSystemAdjusted](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted.aspx) event to manage these adjustments yourself.</span></span>

### <a name="persist-and-share-spatial-anchors"></a><span data-ttu-id="dd136-168">Conserver et partager des ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="dd136-168">Persist and share spatial anchors</span></span>

<span data-ttu-id="dd136-169">Vous pouvez conserver un SpatialAnchor localement à l’aide de la [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx) classe et de retour dans une session de futures de l’application sur le même appareil HoloLens.</span><span class="sxs-lookup"><span data-stu-id="dd136-169">You can persist a SpatialAnchor locally using the [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx) class and then get it back in a future app session on the same HoloLens device.</span></span>

<span data-ttu-id="dd136-170">À l’aide de <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a>, vous pouvez créer un point d’ancrage cloud durable à partir d’un SpatialAnchor local, lequel votre application peut ensuite localiser dans plusieurs HoloLens, appareils iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="dd136-170">By using <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a>, you can create a durable cloud anchor from a local SpatialAnchor, which your app can then locate across multiple HoloLens, iOS and Android devices.</span></span>  <span data-ttu-id="dd136-171">En partageant une ancre spatiale commune sur plusieurs appareils, chaque utilisateur peut voir le contenu restitué par rapport à ce point d’ancrage dans le même emplacement physique.</span><span class="sxs-lookup"><span data-stu-id="dd136-171">By sharing a common spatial anchor across multiple devices, each user can see content rendered relative to that anchor in the same physical location.</span></span>  <span data-ttu-id="dd136-172">Ainsi, les expériences partagées en temps réel.</span><span class="sxs-lookup"><span data-stu-id="dd136-172">This allows for real-time shared experiences.</span></span>

<span data-ttu-id="dd136-173">Vous pouvez également utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a> pour la persistance hologramme asynchrone sur HoloLens, appareils iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="dd136-173">You can also use <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a> for asynchronous hologram persistence across HoloLens, iOS and Android devices.</span></span>  <span data-ttu-id="dd136-174">En partageant une ancre spatial cloud durable, plusieurs périphériques peuvent observer l’hologramme persistante même au fil du temps, même si ces appareils ne sont pas présents ensemble en même temps.</span><span class="sxs-lookup"><span data-stu-id="dd136-174">By sharing a durable cloud spatial anchor, multiple devices can observe the same persisted hologram over time, even if those devices are not present together at the same time.</span></span>

<span data-ttu-id="dd136-175">Pour commencer à créer des expériences partagées dans votre application HoloLens, essayez les 5 minutes <a href="https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens" target="_blank">Guide de démarrage rapide Azure Spatial ancres HoloLens</a>.</span><span class="sxs-lookup"><span data-stu-id="dd136-175">To get started building shared experiences in your HoloLens app, try out the 5-minute <a href="https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens" target="_blank">Azure Spatial Anchors HoloLens quickstart</a>.</span></span>

<span data-ttu-id="dd136-176">Une fois que vous êtes en cours d’exécution ancres spatiale d’Azure, vous pouvez ensuite <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-cpp-winrt" target="_blank">créer et localiser les points d’ancrage sur HoloLens</a>.</span><span class="sxs-lookup"><span data-stu-id="dd136-176">Once you're up and running with Azure Spatial Anchors, you can then <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-cpp-winrt" target="_blank">create and locate anchors on HoloLens</a>.</span></span>  <span data-ttu-id="dd136-177">Procédures pas à pas sont disponibles pour <a href="https://docs.microsoft.com/azure/spatial-anchors/create-locate-anchors-overview" target="_blank">Android et iOS</a> également, ce qui vous permet de partager les ancres mêmes sur tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="dd136-177">Walkthroughs are available for <a href="https://docs.microsoft.com/azure/spatial-anchors/create-locate-anchors-overview" target="_blank">Android and iOS</a> as well, enabling you to share the same anchors on all devices.</span></span>

### <a name="create-spatialanchors-for-holographic-content"></a><span data-ttu-id="dd136-178">Créer SpatialAnchors pour le contenu HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="dd136-178">Create SpatialAnchors for holographic content</span></span>

<span data-ttu-id="dd136-179">Pour cet exemple de code, nous avons modifié Windows HOLOGRAPHIQUE ancre de modèle d’application à créer lorsque le **Pressed** mouvement est détecté.</span><span class="sxs-lookup"><span data-stu-id="dd136-179">For this code sample, we modified the Windows Holographic app template to create anchors when the **Pressed** gesture is detected.</span></span> <span data-ttu-id="dd136-180">Le cube est ensuite placé dans le point d’ancrage pendant la passe de rendu.</span><span class="sxs-lookup"><span data-stu-id="dd136-180">The cube is then placed at the anchor during the render pass.</span></span>

<span data-ttu-id="dd136-181">Dans la mesure où plusieurs points d’ancrage sont pris en charge par la classe d’assistance, nous pouvons placer autant de cubes que nous voulons à l’aide de cet exemple de code !</span><span class="sxs-lookup"><span data-stu-id="dd136-181">Since multiple anchors are supported by the helper class, we can place as many cubes as we want using this code sample!</span></span>

<span data-ttu-id="dd136-182">Notez que les ID d’ancrage sont quelque chose que vous contrôler dans votre application.</span><span class="sxs-lookup"><span data-stu-id="dd136-182">Note that the IDs for anchors are something you control in your app.</span></span> <span data-ttu-id="dd136-183">Dans cet exemple, nous avons créé un schéma d’affectation de noms est séquentiel, en fonction du nombre d’ancres actuellement stockés dans la collection de l’application de points d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="dd136-183">In this example, we have created a naming scheme that is sequential based on the number of anchors currently stored in the app's collection of anchors.</span></span>

```
   // Check for new input state since the last frame.
   SpatialInteractionSourceState^ pointerState = m_spatialInputHandler->CheckForInput();
   if (pointerState != nullptr)
   {
       // Try to get the pointer pose relative to the SpatialStationaryReferenceFrame.
       SpatialPointerPose^ pointerPose = pointerState->TryGetPointerPose(currentCoordinateSystem);
       if (pointerPose != nullptr)
       {
           // When a Pressed gesture is detected, the anchor will be created two meters in front of the user.

           // Get the gaze direction relative to the given coordinate system.
           const float3 headPosition = pointerPose->Head->Position;
           const float3 headDirection = pointerPose->Head->ForwardDirection;

           // The anchor position in the StationaryReferenceFrame.
           static const float distanceFromUser = 2.0f; // meters
           const float3 gazeAtTwoMeters = headPosition + (distanceFromUser * headDirection);

           // Create the anchor at position.
           SpatialAnchor^ anchor = SpatialAnchor::TryCreateRelativeTo(currentCoordinateSystem, gazeAtTwoMeters);

           if ((anchor != nullptr) && (m_spatialAnchorHelper != nullptr))
           {
               // In this example, we store the anchor in an IMap.
               auto anchorMap = m_spatialAnchorHelper->GetAnchorMap();

               // Create an identifier for the anchor.
               String^ id = ref new String(L"HolographicSpatialAnchorStoreSample_Anchor") + anchorMap->Size;

               anchorMap->Insert(id->ToString(), anchor);
           }
       }
   }
```

### <a name="asynchronously-load-and-cache-the-spatialanchorstore"></a><span data-ttu-id="dd136-184">En mode asynchrone charger et mettre en cache, le SpatialAnchorStore</span><span class="sxs-lookup"><span data-stu-id="dd136-184">Asynchronously load, and cache, the SpatialAnchorStore</span></span>

<span data-ttu-id="dd136-185">Nous allons voir comment écrire une classe SampleSpatialAnchorHelper qui permet de gérer cette persistance, y compris :</span><span class="sxs-lookup"><span data-stu-id="dd136-185">Let's see how to write a SampleSpatialAnchorHelper class that helps handle this persistence, including:</span></span>
* <span data-ttu-id="dd136-186">Stocker une collection de points d’ancrage en mémoire, indexées par une clé de Platform::String.</span><span class="sxs-lookup"><span data-stu-id="dd136-186">Storing a collection of in-memory anchors, indexed by a Platform::String key.</span></span>
* <span data-ttu-id="dd136-187">Chargement des points d’ancrage à partir SpatialAnchorStore du système, qui sont maintenu séparé à partir de la collection en mémoire locale.</span><span class="sxs-lookup"><span data-stu-id="dd136-187">Loading anchors from the system's SpatialAnchorStore, which is kept separate from the local in-memory collection.</span></span>
* <span data-ttu-id="dd136-188">L’enregistrement de la collection en mémoire locale des ancres d’à la SpatialAnchorStore lorsque l’application choisit à le faire.</span><span class="sxs-lookup"><span data-stu-id="dd136-188">Saving the local in-memory collection of anchors to the SpatialAnchorStore when the app chooses to do so.</span></span>

<span data-ttu-id="dd136-189">Voici comment enregistrer [SpatialAnchor](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) des objets dans le [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd136-189">Here's how to save [SpatialAnchor](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) objects in the [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx).</span></span>

<span data-ttu-id="dd136-190">Au démarrage de la classe, nous demandons la SpatialAnchorStore de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="dd136-190">When the class starts up, we request the SpatialAnchorStore asynchronously.</span></span> <span data-ttu-id="dd136-191">Cela implique d’e/s de système comme l’API charge le magasin d’ancrage, et cette API est effectuée asynchrone afin que les e/s est non bloquant.</span><span class="sxs-lookup"><span data-stu-id="dd136-191">This involves system I/O as the API loads the anchor store, and this API is made asynchronous so that the I/O is non-blocking.</span></span>

```
   // Request the spatial anchor store, which is the WinRT object that will accept the imported anchor data.
   return create_task(SpatialAnchorManager::RequestStoreAsync())
       .then([](task<SpatialAnchorStore^> previousTask)
   {
       std::shared_ptr<SampleSpatialAnchorHelper> newHelper = nullptr;

       try
       {
           SpatialAnchorStore^ anchorStore = previousTask.get();

           // Once the SpatialAnchorStore has been loaded by the system, we can create our helper class.

           // Using "new" to access private constructor
           newHelper = std::shared_ptr<SampleSpatialAnchorHelper>(new SampleSpatialAnchorHelper(anchorStore));

           // Now we can load anchors from the store.
           newHelper->LoadFromAnchorStore();
       }
       catch (Exception^ exception)
       {
           PrintWstringToDebugConsole(
               std::wstring(L"Exception while loading the anchor store: ") +
               exception->Message->Data() +
               L"\n"
               );
       }

       // Return the initialized class instance.
       return newHelper;
   });
```

<span data-ttu-id="dd136-192">Nous vous fournirons un SpatialAnchorStore que vous pouvez utiliser pour enregistrer les ancres.</span><span class="sxs-lookup"><span data-stu-id="dd136-192">You will be given a SpatialAnchorStore that you can use to save the anchors.</span></span> <span data-ttu-id="dd136-193">Il s’agit d’un IMapView qui associe les valeurs de clés qui sont des chaînes, avec les valeurs de données qui sont SpatialAnchors.</span><span class="sxs-lookup"><span data-stu-id="dd136-193">This is an IMapView that associates key values that are Strings, with data values that are SpatialAnchors.</span></span> <span data-ttu-id="dd136-194">Dans notre exemple de code, nous stockez-le dans une variable de membre de classe privée qui est accessible via une fonction publique de notre classe d’assistance.</span><span class="sxs-lookup"><span data-stu-id="dd136-194">In our sample code, we store this in a private class member variable that is accessible through a public function of our helper class.</span></span>

```
   SampleSpatialAnchorHelper::SampleSpatialAnchorHelper(SpatialAnchorStore^ anchorStore)
   {
       m_anchorStore = anchorStore;
       m_anchorMap = ref new Platform::Collections::Map<String^, SpatialAnchor^>();
   }
```

>[!NOTE]
><span data-ttu-id="dd136-195">N’oubliez pas de raccorder les événements suspend/resume pour enregistrer et charger le magasin d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="dd136-195">Don't forget to hook up the suspend/resume events to save and load the anchor store.</span></span>

```
   void HolographicSpatialAnchorStoreSampleMain::SaveAppState()
   {
       // For example, store information in the SpatialAnchorStore.
       if (m_spatialAnchorHelper != nullptr)
       {
           m_spatialAnchorHelper->TrySaveToAnchorStore();
       }
   }
```

```
   void HolographicSpatialAnchorStoreSampleMain::LoadAppState()
   {
       // For example, load information from the SpatialAnchorStore.
       LoadAnchorStore();
   }
```

### <a name="save-content-to-the-anchor-store"></a><span data-ttu-id="dd136-196">Enregistrer le contenu dans le magasin d’ancrage</span><span class="sxs-lookup"><span data-stu-id="dd136-196">Save content to the anchor store</span></span>

<span data-ttu-id="dd136-197">Lorsque le système interrompt votre application, vous devez enregistrer les points d’ancrage spatiales dans le magasin de point d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="dd136-197">When the system suspends your app, you need to save your spatial anchors to the anchor store.</span></span> <span data-ttu-id="dd136-198">Vous pouvez également choisir d’enregistrer des ancres dans le magasin d’ancrage à d’autres moments, que vous avez trouvé comme étant nécessaires pour la mise en œuvre de votre application.</span><span class="sxs-lookup"><span data-stu-id="dd136-198">You may also choose to save anchors to the anchor store at other times, as you find to be necessary for your app's implementation.</span></span>

<span data-ttu-id="dd136-199">Lorsque vous êtes prêt pour enregistrer les points d’ancrage en mémoire pour le SpatialAnchorStore, vous pouvez parcourir votre collection et essayez d’enregistrer chacune d’elles.</span><span class="sxs-lookup"><span data-stu-id="dd136-199">When you're ready to try saving the in-memory anchors to the SpatialAnchorStore, you can loop through your collection and try to save each one.</span></span>

```
   // TrySaveToAnchorStore: Stores all anchors from memory into the app's anchor store.
   //
   // For each anchor in memory, this function tries to store it in the app's AnchorStore. The operation will fail if
   // the anchor store already has an anchor by that name.
   //
   bool SampleSpatialAnchorHelper::TrySaveToAnchorStore()
   {
       // This function returns true if all the anchors in the in-memory collection are saved to the anchor
       // store. If zero anchors are in the in-memory collection, we will still return true because the
       // condition has been met.
       bool success = true;

       // If access is denied, 'anchorStore' will not be obtained.
       if (m_anchorStore != nullptr)
       {
           for each (auto& pair in m_anchorMap)
           {
               auto const& id = pair->Key;
               auto const& anchor = pair->Value;

               // Try to save the anchors.
               if (!m_anchorStore->TrySave(id, anchor))
               {
                   // This may indicate the anchor ID is taken, or the anchor limit is reached for the app.
                   success=false;
               }
           }
       }

       return success;
   }
```

### <a name="load-content-from-the-anchor-store-when-the-app-resumes"></a><span data-ttu-id="dd136-200">Charger le contenu à partir du magasin d’ancrage lorsque l’application reprend</span><span class="sxs-lookup"><span data-stu-id="dd136-200">Load content from the anchor store when the app resumes</span></span>

<span data-ttu-id="dd136-201">Lorsque votre application se poursuit, ou à tout moment nécessaire pour les implementaiton de votre application, vous pouvez restaurer les points d’ancrage qui ont été précédemment enregistrées pour le AnchorStore par les transférer à partir IMapView du magasin d’ancrage à votre propre base de données en mémoire de SpatialAnchors.</span><span class="sxs-lookup"><span data-stu-id="dd136-201">When your app resumes, or at any other time necessary for your app's implementaiton, you can restore anchors that were previously saved to the AnchorStore by transferring them from the anchor store's IMapView to your own in-memory database of SpatialAnchors.</span></span>

<span data-ttu-id="dd136-202">Pour restaurer les points d’ancrage à partir de la SpatialAnchorStore, restaurer Chacun d’eux qui vous intéresse à votre propre collection en mémoire.</span><span class="sxs-lookup"><span data-stu-id="dd136-202">To restore anchors from the SpatialAnchorStore, restore each one that you are interested in to your own in-memory collection.</span></span>

<span data-ttu-id="dd136-203">Vous avez besoin de votre propre base de données en mémoire de SpatialAnchors ; un moyen d’associer des chaînes avec SpatialAnchors que vous créez.</span><span class="sxs-lookup"><span data-stu-id="dd136-203">You need your own in-memory database of SpatialAnchors; some way to associate Strings with the SpatialAnchors that you create.</span></span> <span data-ttu-id="dd136-204">Dans notre exemple de code, nous choisissons d’utiliser un Windows::Foundation::Collections::IMap pour stocker les ancres, ce qui la rend facile à utiliser la même valeur de clé et les données pour le SpatialAnchorStore.</span><span class="sxs-lookup"><span data-stu-id="dd136-204">In our sample code, we choose to use a Windows::Foundation::Collections::IMap to store the anchors, which makes it easy to use the same key and data value for the SpatialAnchorStore.</span></span>

```
   // This is an in-memory anchor list that is separate from the anchor store.
   // These anchors may be used, reasoned about, and so on before committing the collection to the store.
   Windows::Foundation::Collections::IMap<Platform::String^, Windows::Perception::Spatial::SpatialAnchor^>^ m_anchorMap;
```

>[!NOTE]
><span data-ttu-id="dd136-205">Une ancre qui est restaurée n’est pas immédiatement toujours localisable.</span><span class="sxs-lookup"><span data-stu-id="dd136-205">An anchor that is restored might not be locatable right away.</span></span> <span data-ttu-id="dd136-206">Par exemple, il peut être un point d’ancrage dans une salle distincte ou dans une autre génération complètement.</span><span class="sxs-lookup"><span data-stu-id="dd136-206">For example, it might be an anchor in a separate room or in a different building altogether.</span></span> <span data-ttu-id="dd136-207">Ancres récupérées à partir de la AnchorStore doivent être testés pour locatability avant de les utiliser.</span><span class="sxs-lookup"><span data-stu-id="dd136-207">Anchors retrieved from the AnchorStore should be tested for locatability before using them.</span></span>

<br>

>[!NOTE]
><span data-ttu-id="dd136-208">Dans cet exemple de code, nous récupérons tous les points d’ancrage à partir de la AnchorStore.</span><span class="sxs-lookup"><span data-stu-id="dd136-208">In this example code, we retrieve all anchors from the AnchorStore.</span></span> <span data-ttu-id="dd136-209">Cela n’est pas obligatoire ; votre application pourrait tout aussi bien choisir un sous-ensemble spécifique de points d’ancrage à l’aide des valeurs de clés de chaîne qui sont significatives pour votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="dd136-209">This is not a requirement; your app could just as well pick and choose a certain subset of anchors by using String key values that are meaningful to your implementation.</span></span>

```
   // LoadFromAnchorStore: Loads all anchors from the app's anchor store into memory.
   //
   // The anchors are stored in memory using an IMap, which stores anchors using a string identifier. Any string can be used as
   // the identifier; it can have meaning to the app, such as "Game_Leve1_CouchAnchor," or it can be a GUID that is generated
   // by the app.
   //
   void SampleSpatialAnchorHelper::LoadFromAnchorStore()
   {
       // If access is denied, 'anchorStore' will not be obtained.
       if (m_anchorStore != nullptr)
       {
           // Get all saved anchors.
           auto anchorMapView = m_anchorStore->GetAllSavedAnchors();
           for each (auto const& pair in anchorMapView)
           {
               auto const& id = pair->Key;
               auto const& anchor = pair->Value;
               m_anchorMap->Insert(id, anchor);
           }
       }
   }
```

### <a name="clear-the-anchor-store-when-needed"></a><span data-ttu-id="dd136-210">Effacer le magasin d’ancrage, si nécessaire</span><span class="sxs-lookup"><span data-stu-id="dd136-210">Clear the anchor store, when needed</span></span>

<span data-ttu-id="dd136-211">Parfois, vous devez effacer l’état de l’application et d’écriture de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="dd136-211">Sometimes, you need to clear app state and write new data.</span></span> <span data-ttu-id="dd136-212">Voici comment procéder avec le [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd136-212">Here's how you do that with the [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx).</span></span>

<span data-ttu-id="dd136-213">À l’aide de notre classe d’assistance, il est presque pas nécessaire d’inclure dans un wrapper la fonction Clear.</span><span class="sxs-lookup"><span data-stu-id="dd136-213">Using our helper class, it's almost unnecessary to wrap the Clear function.</span></span> <span data-ttu-id="dd136-214">Nous choisissons à le faire dans notre exemple d’implémentation, étant donné que notre classe d’assistance porte la responsabilité du propriétaire de l’instance SpatialAnchorStore.</span><span class="sxs-lookup"><span data-stu-id="dd136-214">We choose to do so in our sample implementation, because our helper class is given the responsibility of owning the SpatialAnchorStore instance.</span></span>

```
   // ClearAnchorStore: Clears the AnchorStore for the app.
   //
   // This function clears the AnchorStore. It has no effect on the anchors stored in memory.
   //
   void SampleSpatialAnchorHelper::ClearAnchorStore()
   {
       // If access is denied, 'anchorStore' will not be obtained.
       if (m_anchorStore != nullptr)
       {
           // Clear all anchors from the store.
           m_anchorStore->Clear();
       }
   }
```

### <a name="example-relating-anchor-coordinate-systems-to-stationary-reference-frame-coordinate-systems"></a><span data-ttu-id="dd136-215">Exemple : Systèmes de coordonnées de cadre de référence stationnaire concernant les systèmes de coordonnées de point d’ancrage</span><span class="sxs-lookup"><span data-stu-id="dd136-215">Example: Relating anchor coordinate systems to stationary reference frame coordinate systems</span></span>

<span data-ttu-id="dd136-216">Supposons que vous avez un point d’ancrage, et que vous souhaitez quelque chose dans le système de coordonnées de votre point d’ancrage se rapportent à SpatialStationaryReferenceFrame que vous utilisez déjà pour la plupart des autres votre contenu.</span><span class="sxs-lookup"><span data-stu-id="dd136-216">Let's say that you have an anchor, and you want to relate something in your anchor's coordinate system to the SpatialStationaryReferenceFrame that you’re already using for most of your other content.</span></span> <span data-ttu-id="dd136-217">Vous pouvez utiliser [TryGetTransformTo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.trygettransformto.aspx) pour obtenir une transformation à partir du système de coordonnées de l’ancre à celle de l’image de référence stationnaire :</span><span class="sxs-lookup"><span data-stu-id="dd136-217">You can use [TryGetTransformTo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.trygettransformto.aspx) to obtain a transform from the anchor’s coordinate system to that of the stationary reference frame:</span></span>

```
   // In this code snippet, someAnchor is a SpatialAnchor^ that has been initialized and is valid in the current environment.
   float4x4 anchorSpaceToCurrentCoordinateSystem;
   SpatialCoordinateSystem^ anchorSpace = someAnchor->CoordinateSystem;
   const auto tryTransform = anchorSpace->TryGetTransformTo(currentCoordinateSystem);
   if (tryTransform != nullptr)
   {
       anchorSpaceToCurrentCoordinateSystem = tryTransform->Value;
   }
```

<span data-ttu-id="dd136-218">Ce processus est utile pour vous de deux manières :</span><span class="sxs-lookup"><span data-stu-id="dd136-218">This process is useful to you in two ways:</span></span>
1. <span data-ttu-id="dd136-219">Elle indique si les deux images de référence peuvent être reconnus par rapport aux autres, et ;</span><span class="sxs-lookup"><span data-stu-id="dd136-219">It tells you if the two reference frames can be understood relative to one another, and;</span></span>
2. <span data-ttu-id="dd136-220">Dans ce cas, il vous fournit une transformation pour accéder directement à partir d’un système de coordonnées à l’autre.</span><span class="sxs-lookup"><span data-stu-id="dd136-220">If so, it provides you a transform to go directly from one coordinate system to the other.</span></span>

<span data-ttu-id="dd136-221">Avec ces informations, vous avez une connaissance de la relation spatiale entre les objets entre les deux images de référence.</span><span class="sxs-lookup"><span data-stu-id="dd136-221">With this information, you have an understanding of the spatial relation between objects between the two reference frames.</span></span>

<span data-ttu-id="dd136-222">Pour le rendu, vous pouvez souvent obtenir de meilleurs résultats en regroupant les objets en fonction de leur image de référence d’origine ou d’un point d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="dd136-222">For rendering, you can often obtain better results by grouping objects according to their original reference frame or anchor.</span></span> <span data-ttu-id="dd136-223">Effectuer une étape de dessin distincte pour chaque groupe.</span><span class="sxs-lookup"><span data-stu-id="dd136-223">Perform a separate drawing pass for each group.</span></span> <span data-ttu-id="dd136-224">Les matrices de vue sont plus précises pour les objets avec des transformations de modèle qui sont créées initialement à l’aide du même système de coordonnées.</span><span class="sxs-lookup"><span data-stu-id="dd136-224">The view matrices are more accurate for objects with model transforms that are created initially using the same coordinate system.</span></span>

## <a name="create-holograms-using-a-device-attached-frame-of-reference"></a><span data-ttu-id="dd136-225">Créer hologrammes à l’aide d’un périphérique connecté de référence</span><span class="sxs-lookup"><span data-stu-id="dd136-225">Create holograms using a device-attached frame of reference</span></span>

<span data-ttu-id="dd136-226">Parfois, lorsque vous souhaitez restituer un hologramme qui [reste attachée](coordinate-systems.md#attached-frame-of-reference) à l’emplacement de l’appareil, par exemple un panneau avec les informations ou un message d’information de débogage quand l’appareil est uniquement en mesure de déterminer son orientation et pas sa position dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="dd136-226">There are times when you want to render a hologram that [remains attached](coordinate-systems.md#attached-frame-of-reference) to the device's location, for example a panel with debugging information or an informational message when the device is only able to determine its orientation and not its position in space.</span></span> <span data-ttu-id="dd136-227">Pour ce faire, nous utilisons un cadre de référence jointe.</span><span class="sxs-lookup"><span data-stu-id="dd136-227">To accomplish this, we use an attached frame of reference.</span></span>

<span data-ttu-id="dd136-228">La classe SpatialLocatorAttachedFrameOfReference définit des systèmes de coordonnées qui sont par rapport à l’appareil, plutôt que dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="dd136-228">The SpatialLocatorAttachedFrameOfReference class defines coordinate systems which are relative to the device rather than to the real-world.</span></span> <span data-ttu-id="dd136-229">Cette image a un titre fixe par rapport aux environs de l’utilisateur qui pointe dans la direction de l’utilisateur a été confronté lors de la création de l’image de référence.</span><span class="sxs-lookup"><span data-stu-id="dd136-229">This frame has a fixed heading relative to the user's surroundings that points in the direction the user was facing when the reference frame was created.</span></span> <span data-ttu-id="dd136-230">Dès lors, toutes les orientations dans ce cadre de référence sont par rapport à ce titre fixe, même lorsque l’utilisateur fait pivoter l’appareil.</span><span class="sxs-lookup"><span data-stu-id="dd136-230">From then on, all orientations in this frame of reference are relative to that fixed heading, even as the user rotates the device.</span></span>

<span data-ttu-id="dd136-231">Pour HoloLens, l’origine de cette image système de coordonnées se trouve au centre de rotation de tête de l’utilisateur, afin que sa position n’est pas affectée par rotation principale.</span><span class="sxs-lookup"><span data-stu-id="dd136-231">For HoloLens, the origin of this frame's coordinate system is located at the center of rotation of the user's head, so that its position is not affected by head rotation.</span></span> <span data-ttu-id="dd136-232">Votre application peut spécifier un décalage par rapport à ce point pour positionner hologrammes devant l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd136-232">Your app can specify an offset relative to this point to position holograms in front of the user.</span></span>

<span data-ttu-id="dd136-233">Pour obtenir un SpatialLocatorAttachedFrameOfReference, utilisez la classe SpatialLocator et appeler CreateAttachedFrameOfReferenceAtCurrentHeading.</span><span class="sxs-lookup"><span data-stu-id="dd136-233">To get a SpatialLocatorAttachedFrameOfReference, use the SpatialLocator class and call CreateAttachedFrameOfReferenceAtCurrentHeading.</span></span>

<span data-ttu-id="dd136-234">Notez que cela s’applique aux appareils toute plage de Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="dd136-234">Note that this applies to the entire range of Windows Mixed Reality devices.</span></span>

### <a name="use-a-reference-frame-attached-to-the-device"></a><span data-ttu-id="dd136-235">Utiliser une image de référence associée à l’appareil</span><span class="sxs-lookup"><span data-stu-id="dd136-235">Use a reference frame attached to the device</span></span>

<span data-ttu-id="dd136-236">Ces sections parler de ce que nous avons modifié dans le modèle d’application Windows HOLOGRAPHIQUE pour activer une périphérique connecté de référence à l’aide de cette API.</span><span class="sxs-lookup"><span data-stu-id="dd136-236">These sections talk about what we changed in the Windows Holographic app template to enable a device-attached frame of reference using this API.</span></span> <span data-ttu-id="dd136-237">Notez que cette hologramme « joint » est exécutés en parallèle hologrammes ancrés ou STATIONNAIRES et peut également être utilisé quand l’appareil est temporairement Impossible de trouver sa position dans le monde.</span><span class="sxs-lookup"><span data-stu-id="dd136-237">Note that this "attached" hologram will work alongside stationary or anchored holograms, and may also be used when the device is temporarily unable to find its position in the world.</span></span>

<span data-ttu-id="dd136-238">Tout d’abord, nous avons modifié le modèle pour stocker un SpatialLocatorAttachedFrameOfReference au lieu d’un SpatialStationaryFrameOfReference :</span><span class="sxs-lookup"><span data-stu-id="dd136-238">First, we changed the template to store a SpatialLocatorAttachedFrameOfReference instead of a SpatialStationaryFrameOfReference:</span></span>

<span data-ttu-id="dd136-239">À partir de **HolographicTagAlongSampleMain.h**:</span><span class="sxs-lookup"><span data-stu-id="dd136-239">From **HolographicTagAlongSampleMain.h**:</span></span>

```
   // A reference frame attached to the holographic camera.
   Windows::Perception::Spatial::SpatialLocatorAttachedFrameOfReference^   m_referenceFrame;
```

<span data-ttu-id="dd136-240">À partir de **HolographicTagAlongSampleMain.cpp**:</span><span class="sxs-lookup"><span data-stu-id="dd136-240">From **HolographicTagAlongSampleMain.cpp**:</span></span>

```
   // In this example, we create a reference frame attached to the device.
   m_referenceFrame = m_locator->CreateAttachedFrameOfReferenceAtCurrentHeading();
```

<span data-ttu-id="dd136-241">Pendant la mise à jour, nous obtenons maintenant le système de coordonnées à l’horodatage obtenue à partir d’avec la prédiction de frame.</span><span class="sxs-lookup"><span data-stu-id="dd136-241">During the update, we now obtain the coordinate system at the time stamp obtained from with the frame prediction.</span></span>

```
   // Next, we get a coordinate system from the attached frame of reference that is
   // associated with the current frame. Later, this coordinate system is used for
   // for creating the stereo view matrices when rendering the sample content.
   SpatialCoordinateSystem^ currentCoordinateSystem =
       m_referenceFrame->GetStationaryCoordinateSystemAtTimestamp(prediction->Timestamp);
```

### <a name="get-a-spatial-pointer-pose-and-follow-the-users-gaze"></a><span data-ttu-id="dd136-242">Obtenir une pose de pointeur spatiale et suivez les regards de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="dd136-242">Get a spatial pointer pose, and follow the user's Gaze</span></span>

<span data-ttu-id="dd136-243">Nous voulons que notre hologramme d’exemple à suivre l’utilisateur [les regards](gaze.md), similaire à comment l’interpréteur de commandes HOLOGRAPHIQUE peut suivre des regards de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd136-243">We want our example hologram to follow the user's [gaze](gaze.md), similar to how the holographic shell can follow the user's gaze.</span></span> <span data-ttu-id="dd136-244">Pour ce faire, nous devons obtenir le SpatialPointerPose à partir de la même horodatage.</span><span class="sxs-lookup"><span data-stu-id="dd136-244">For this, we need to get the SpatialPointerPose from the same time stamp.</span></span>

```
SpatialPointerPose^ pose = SpatialPointerPose::TryGetAtTimestamp(currentCoordinateSystem, prediction->Timestamp);
```

<span data-ttu-id="dd136-245">Cette SpatialPointerPose a les informations nécessaires pour positionner l’hologramme conformément à la [titre actuel de l’utilisateur](gaze-in-directx.md).</span><span class="sxs-lookup"><span data-stu-id="dd136-245">This SpatialPointerPose has the information needed to position the hologram according to the [user's current heading](gaze-in-directx.md).</span></span>

<span data-ttu-id="dd136-246">Pour des raisons de confort de l’utilisateur, nous utilisons une interpolation linéaire (« lerp ») pour lisser la modification de la position où il se produit sur une période de temps.</span><span class="sxs-lookup"><span data-stu-id="dd136-246">For reasons of user comfort, we use linear interpolation ("lerp") to smooth the change in position such that it occurs over a period of time.</span></span> <span data-ttu-id="dd136-247">Il s’agit plus à l’aise pour l’utilisateur que l’hologramme à leur regards de verrouillage.</span><span class="sxs-lookup"><span data-stu-id="dd136-247">This is more comfortable for the user than locking the hologram to their gaze.</span></span> <span data-ttu-id="dd136-248">Lerping que position de l’hologramme tag-along permet également de stabiliser le hologramme par atténuation pour le déplacement ; Si nous n’avez pas ce blocage, l’utilisateur verrait l’hologramme instabilité en raison de ce qui sont normalement considéré comme imperceptibles mouvements de tête de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd136-248">Lerping the tag-along hologram's position also allows us to stabilize the hologram by dampening the movement; if we did not do this dampening, the user would see the hologram jitter because of what are normally considered to be imperceptible movements of the user's head.</span></span>

<span data-ttu-id="dd136-249">From **StationaryQuadRenderer::PositionHologram**:</span><span class="sxs-lookup"><span data-stu-id="dd136-249">From **StationaryQuadRenderer::PositionHologram**:</span></span>

```
   const float& dtime = static_cast<float>(timer.GetElapsedSeconds());

   if (pointerPose != nullptr)
   {
       // Get the gaze direction relative to the given coordinate system.
       const float3 headPosition  = pointerPose->Head->Position;
       const float3 headDirection = pointerPose->Head->ForwardDirection;

       // The tag-along hologram follows a point 2.0m in front of the user's gaze direction.
       static const float distanceFromUser = 2.0f; // meters
       const float3 gazeAtTwoMeters = headPosition + (distanceFromUser * headDirection);

       // Lerp the position, to keep the hologram comfortably stable.
       auto lerpedPosition = lerp(m_position, gazeAtTwoMeters, dtime * c_lerpRate);

       // This will be used as the translation component of the hologram's
       // model transform.
       SetPosition(lerpedPosition);
   }
```

>[!NOTE]
><span data-ttu-id="dd136-250">Dans le cas d’un panneau de débogage, vous pouvez choisir repositionner un peu l’hologramme désactivé pour le côté afin qu’elle ne gêne pas votre affichage.</span><span class="sxs-lookup"><span data-stu-id="dd136-250">In the case of a debugging panel, you might choose to reposition the hologram off to the side a little so that it does not obstruct your view.</span></span> <span data-ttu-id="dd136-251">Voici un exemple de comment vous pouvez le faire.</span><span class="sxs-lookup"><span data-stu-id="dd136-251">Here's an example of how you might do that.</span></span>

<span data-ttu-id="dd136-252">Pour **StationaryQuadRenderer::PositionHologram**:</span><span class="sxs-lookup"><span data-stu-id="dd136-252">For **StationaryQuadRenderer::PositionHologram**:</span></span>

```
       // If you're making a debug view, you might not want the tag-along to be directly in the
       // center of your field of view. Use this code to position the hologram to the right of
       // the user's gaze direction.
       /*
       const float3 offset = float3(0.13f, 0.0f, 0.f);
       static const float distanceFromUser = 2.2f; // meters
       const float3 gazeAtTwoMeters = headPosition + (distanceFromUser * (headDirection + offset));
       */
```

### <a name="rotate-the-hologram-to-face-the-camera"></a><span data-ttu-id="dd136-253">Faire pivoter l’hologramme pour faire face à l’appareil photo</span><span class="sxs-lookup"><span data-stu-id="dd136-253">Rotate the hologram to face the camera</span></span>

<span data-ttu-id="dd136-254">Il n’est pas suffisant de simplement positionner HOLOGRAMME, qui est dans ce cas un quadruple ; Nous devons également faire pivoter l’objet pour faire face à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd136-254">It is not enough to simply position the hologram, which in this case is a quad; we must also rotate the object to face the user.</span></span> <span data-ttu-id="dd136-255">Notez que cette rotation s’effectue dans l’espace universel, car ce type de le billboarding permet l’hologramme reste une partie de l’environnement utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd136-255">Note that this rotation occurs in world space, because this type of billboarding allows the hologram to remain a part of the user's environment.</span></span> <span data-ttu-id="dd136-256">Espace d’affichage le billboarding n’est pas à l’aise, car l’hologramme est verrouillé à l’orientation de l’affichage ; Dans ce cas, vous devrez également interpoler entre les matrices de vue de gauche et droite afin d’acquérir une transformation de tableau blanc espace d’affichage qui n’interrompt pas rendu stéréo.</span><span class="sxs-lookup"><span data-stu-id="dd136-256">View-space billboarding is not as comfortable because the hologram becomes locked to the display orientation; in that case, you would also have to interpolate between the left and right view matrices in order to acquire a view-space billboard transform that does not disrupt stereo rendering.</span></span> <span data-ttu-id="dd136-257">Ici, nous faire pivoter sur les axes X et Z pour faire face à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd136-257">Here, we rotate on the X and Z axes to face the user.</span></span>

<span data-ttu-id="dd136-258">À partir de **StationaryQuadRenderer::Update**:</span><span class="sxs-lookup"><span data-stu-id="dd136-258">From **StationaryQuadRenderer::Update**:</span></span>

```
   // Seconds elapsed since previous frame.
   const float& dTime = static_cast<float>(timer.GetElapsedSeconds());

   // Create a direction normal from the hologram's position to the origin of person space.
   // This is the z-axis rotation.
   XMVECTOR facingNormal = XMVector3Normalize(-XMLoadFloat3(&m_position));

   // Rotate the x-axis around the y-axis.
   // This is a 90-degree angle from the normal, in the xz-plane.
   // This is the x-axis rotation.
   XMVECTOR xAxisRotation = XMVector3Normalize(XMVectorSet(XMVectorGetZ(facingNormal), 0.f, -XMVectorGetX(facingNormal), 0.f));

   // Create a third normal to satisfy the conditions of a rotation matrix.
   // The cross product  of the other two normals is at a 90-degree angle to
   // both normals. (Normalize the cross product to avoid floating-point math
   // errors.)
   // Note how the cross product will never be a zero-matrix because the two normals
   // are always at a 90-degree angle from one another.
   XMVECTOR yAxisRotation = XMVector3Normalize(XMVector3Cross(facingNormal, xAxisRotation));

   // Construct the 4x4 rotation matrix.

   // Rotate the quad to face the user.
   XMMATRIX rotationMatrix = XMMATRIX(
       xAxisRotation,
       yAxisRotation,
       facingNormal,
       XMVectorSet(0.f, 0.f, 0.f, 1.f)
       );

   // Position the quad.
   const XMMATRIX modelTranslation = XMMatrixTranslationFromVector(XMLoadFloat3(&m_position));

   // The view and projection matrices are provided by the system; they are associated
   // with holographic cameras, and updated on a per-camera basis.
   // Here, we provide the model transform for the sample hologram. The model transform
   // matrix is transposed to prepare it for the shader.
   XMStoreFloat4x4(&m_modelConstantBufferData.model, XMMatrixTranspose(rotationMatrix * modelTranslation));
```

### <a name="render-the-attached-hologram"></a><span data-ttu-id="dd136-259">Restituer la hologramme attaché</span><span class="sxs-lookup"><span data-stu-id="dd136-259">Render the attached hologram</span></span>

<span data-ttu-id="dd136-260">Pour cet exemple, nous avons également choisir restituer l’hologramme dans le système de coordonnées de la SpatialLocatorAttachedReferenceFrame, c'est-à-dire où nous avons positionné la hologramme.</span><span class="sxs-lookup"><span data-stu-id="dd136-260">For this example, we also choose to render the hologram in the coordinate system of the SpatialLocatorAttachedReferenceFrame, which is where we positioned the hologram.</span></span> <span data-ttu-id="dd136-261">(Si nous avions décidé d’effectuer le rendu à l’aide d’un autre système de coordonnées, nous devons acquérir une transformation à partir du système de coordonnées du cadre de référence de périphérique connecté à ce système de coordonnées.)</span><span class="sxs-lookup"><span data-stu-id="dd136-261">(If we had decided to render using another coordinate system, we would need to acquire a transform from the device-attached reference frame's coordinate system to that coordinate system.)</span></span>

<span data-ttu-id="dd136-262">From **HolographicTagAlongSampleMain::Render**:</span><span class="sxs-lookup"><span data-stu-id="dd136-262">From **HolographicTagAlongSampleMain::Render**:</span></span>

```
   // The view and projection matrices for each holographic camera will change
   // every frame. This function refreshes the data in the constant buffer for
   // the holographic camera indicated by cameraPose.
   pCameraResources->UpdateViewProjectionBuffer(
       m_deviceResources,
       cameraPose,
       m_referenceFrame->GetStationaryCoordinateSystemAtTimestamp(prediction->Timestamp)
       );
```

<span data-ttu-id="dd136-263">C’est tout !</span><span class="sxs-lookup"><span data-stu-id="dd136-263">That's it!</span></span> <span data-ttu-id="dd136-264">L’hologramme sera désormais « repère » une position qui est de 2 mètres devant la direction du regard de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd136-264">The hologram will now "chase" a position that is 2 meters in front of the user's gaze direction.</span></span>

>[!NOTE]
><span data-ttu-id="dd136-265">Cet exemple charge également le contenu supplémentaire, consultez StationaryQuadRenderer.cpp.</span><span class="sxs-lookup"><span data-stu-id="dd136-265">This example also loads additional content - see StationaryQuadRenderer.cpp.</span></span>

## <a name="handling-tracking-loss"></a><span data-ttu-id="dd136-266">Suivi de la perte de la gestion des</span><span class="sxs-lookup"><span data-stu-id="dd136-266">Handling tracking loss</span></span>

<span data-ttu-id="dd136-267">Lorsque l’appareil ne peut pas localiser lui-même dans le monde, l’application rencontre « perte de suivi ».</span><span class="sxs-lookup"><span data-stu-id="dd136-267">When the device cannot locate itself in the world, the app experiences "tracking loss".</span></span> <span data-ttu-id="dd136-268">Applications de réalité mixte Windows doivent être en mesure de gérer les perturbations pour le système de suivi positionnels.</span><span class="sxs-lookup"><span data-stu-id="dd136-268">Windows Mixed Reality apps should be able to handle such disruptions to the positional tracking system.</span></span> <span data-ttu-id="dd136-269">Ces interruptions peuvent être observées et la création de réponses à l’aide de l’événement LocatabilityChanged sur la valeur par défaut SpatialLocator.</span><span class="sxs-lookup"><span data-stu-id="dd136-269">These disruptions can be observed, and responses created, by using the LocatabilityChanged event on the default SpatialLocator.</span></span>

<span data-ttu-id="dd136-270">À partir de **AppMain::SetHolographicSpace :**</span><span class="sxs-lookup"><span data-stu-id="dd136-270">From **AppMain::SetHolographicSpace:**</span></span>

```
   // Be able to respond to changes in the positional tracking state.
   m_locatabilityChangedToken =
       m_locator->LocatabilityChanged +=
           ref new Windows::Foundation::TypedEventHandler<SpatialLocator^, Object^>(
               std::bind(&HolographicApp1Main::OnLocatabilityChanged, this, _1, _2)
               );
```

<span data-ttu-id="dd136-271">Lorsque votre application reçoit un événement LocatabilityChanged, il peut modifier le comportement en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="dd136-271">When your app receives a LocatabilityChanged event, it can change behavior as needed.</span></span> <span data-ttu-id="dd136-272">Par exemple, dans l’état PositionalTrackingInhibited, votre application peut interrompre le fonctionnement normal et restituer un [hologramme de tag-along](coordinate-systems-in-directx.md#create-holograms-using-a-device-attached-frame-of-reference) qui affiche un message d’avertissement.</span><span class="sxs-lookup"><span data-stu-id="dd136-272">For example, in the PositionalTrackingInhibited state, your app can pause normal operation and render a [tag-along hologram](coordinate-systems-in-directx.md#create-holograms-using-a-device-attached-frame-of-reference) that displays a warning message.</span></span>

<span data-ttu-id="dd136-273">Le modèle d’application Windows holographique est fourni avec un gestionnaire LocatabilityChanged déjà créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="dd136-273">The Windows Holographic app template comes with a LocatabilityChanged handler already created for you.</span></span> <span data-ttu-id="dd136-274">Par défaut, il affiche un avertissement dans la console de débogage lorsque le suivi de position n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="dd136-274">By default, it displays a warning in the debug console when positional tracking is unavailable.</span></span> <span data-ttu-id="dd136-275">Vous pouvez ajouter du code à ce gestionnaire pour fournir une réponse en fonction des besoins de votre application.</span><span class="sxs-lookup"><span data-stu-id="dd136-275">You can add code to this handler to provide a response as needed from your app.</span></span>

<span data-ttu-id="dd136-276">À partir de **AppMain.cpp :**</span><span class="sxs-lookup"><span data-stu-id="dd136-276">From **AppMain.cpp:**</span></span>

```
   void HolographicApp1Main::OnLocatabilityChanged(SpatialLocator^ sender, Object^ args)
   {
       switch (sender->Locatability)
       {
       case SpatialLocatability::Unavailable:
           // Holograms cannot be rendered.
           {
               String^ message = L"Warning! Positional tracking is " +
                                           sender->Locatability.ToString() + L".\n";
               OutputDebugStringW(message->Data());
           }
           break;

       // In the following three cases, it is still possible to place holograms using a
       // SpatialLocatorAttachedFrameOfReference.
       case SpatialLocatability::PositionalTrackingActivating:
           // The system is preparing to use positional tracking.

       case SpatialLocatability::OrientationOnly:
           // Positional tracking has not been activated.

       case SpatialLocatability::PositionalTrackingInhibited:
           // Positional tracking is temporarily inhibited. User action may be required
           // in order to restore positional tracking.
           break;

       case SpatialLocatability::PositionalTrackingActive:
           // Positional tracking is active. World-locked content can be rendered.
           break;
       }
   }
```

## <a name="spatial-mapping"></a><span data-ttu-id="dd136-277">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="dd136-277">Spatial mapping</span></span>

<span data-ttu-id="dd136-278">Le [mappage spatial](spatial-mapping-in-directx.md) API permettent l’utilisation de systèmes de coordonnées pour obtenir des transformations de modèle pour les maillages de surface.</span><span class="sxs-lookup"><span data-stu-id="dd136-278">The [spatial mapping](spatial-mapping-in-directx.md) APIs make use of coordinate systems to get model transforms for surface meshes.</span></span>

## <a name="see-also"></a><span data-ttu-id="dd136-279">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="dd136-279">See also</span></span>
* [<span data-ttu-id="dd136-280">Systèmes de coordonnées</span><span class="sxs-lookup"><span data-stu-id="dd136-280">Coordinate systems</span></span>](coordinate-systems.md)
* [<span data-ttu-id="dd136-281">Ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="dd136-281">Spatial anchors</span></span>](spatial-anchors.md)
* <span data-ttu-id="dd136-282"><a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a></span><span class="sxs-lookup"><span data-stu-id="dd136-282"><a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a></span></span>
* [<span data-ttu-id="dd136-283">HEAD et surveillez les regards dans DirectX</span><span class="sxs-lookup"><span data-stu-id="dd136-283">Head and eye gaze in DirectX</span></span>](gaze-in-directx.md)
* [<span data-ttu-id="dd136-284">Mains et contrôleurs de mouvement dans DirectX</span><span class="sxs-lookup"><span data-stu-id="dd136-284">Hands and motion controllers in DirectX</span></span>](hands-and-motion-controllers-in-directx.md)
* [<span data-ttu-id="dd136-285">Mappage spatial dans DirectX</span><span class="sxs-lookup"><span data-stu-id="dd136-285">Spatial mapping in DirectX</span></span>](spatial-mapping-in-directx.md)
