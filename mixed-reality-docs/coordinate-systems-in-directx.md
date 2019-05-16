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
# <a name="coordinate-systems-in-directx"></a>Systèmes de coordonnées dans DirectX

[Systèmes de coordonnées](coordinate-systems.md) constituent la base pour comprendre spatial proposée par les API de réalité mixte Windows.

Aujourd'hui assis VR ou appareils de salle d’unique de VR établissent un système de coordonnées principal pour représenter leur espace suivie. Les appareils Windows Mixed Reality comme HoloLens sont conçues pour être utilisées dans les environnements de grande taille non définis, avec l’appareil de découvrir et apprendre à connaître son environnement en tant que l’utilisateur parcourt autour. Cela permet à l’appareil pour s’adapter à améliorer continuellement connaissance des salles de l’utilisateur, mais les résultats dans les systèmes de coordonnées qui va changer leur relation un à l’autre pendant la durée de vie de l’application. Réalité mixte Windows prend en charge un large éventail d’appareils, allant des casques IMMERSIFS assis via des trames de référence connecté au monde.

>[!NOTE]
>Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).  Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.

## <a name="spatial-coordinate-systems-in-windows"></a>Systèmes de coordonnées spatiales dans Windows

Le type de base permet de raisonner sur les systèmes de coordonnées de monde réel dans Windows est le <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a>. Une instance de ce type représente un système de coordonnées arbitraire et fournit une méthode pour obtenir une matrice de transformation que vous pouvez utiliser pour transformer entre deux systèmes de coordonnées sans avoir à comprendre les détails de chacun d’eux.

Les méthodes qui retournent des informations spatiales, représentées en tant que points, les rayons ou les volumes dans son environnement de l’utilisateur, accepte un paramètre SpatialCoordinateSystem pour vous permettre de décider le système de coordonnées dans lequel il est très utile pour ces coordonnées à retourner. Les unités pour ces coordonnées sera toujours en mètres.

Un SpatialCoordinateSystem a une relation dynamique avec d’autres systèmes de coordonnées, y compris ceux qui représentent la position de l’appareil. À tout moment dans le temps, l’appareil peut être en mesure de localiser des systèmes de coordonnées et d’autres non. Pour la plupart des systèmes de coordonnées, votre application doit être prête à gérer les périodes de temps pendant laquelle ils ne peut pas être localisés.

Votre application ne doit pas créer directement SpatialCoordinateSystems - plutôt qu’ils doivent être utilisées via les API de Perception. Il existe trois sources principales de systèmes de coordonnées dans les API de Perception, chacun d'entre eux mappe à un concept décrit sur le [systèmes de coordonnées](coordinate-systems.md) page :
* Pour obtenir un système de référence stationnaire, créez un <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstationaryframeofreference" target="_blank">SpatialStationaryFrameOfReference</a> ou obtenir un auprès d’actuel <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference" target="_blank">SpatialStageFrameOfReference</a>.
* Pour obtenir un point d’ancrage spatial, créez un <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a>.
* Pour obtenir un cadre de référence jointe, créez un <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocatorattachedframeofreference" target="_blank">SpatialLocatorAttachedFrameOfReference</a>.

Tous les systèmes de coordonnées retournées par ces objets sont droitiers avec + y haut + x à droite et + z vers l’arrière. Vous pouvez mémoriser le sens dans lequel les points de l’axe z positif en pointant vers les doigts de votre gauche ou droite dans le sens positif x et les utiliser curl dans l’axe y positif. La direction vers laquelle pointe votre pouce (vers vous ou à l'opposé) correspond à la direction dans laquelle pointe l’axe z positif pour ce système de coordonnées. L’illustration suivante décrit ces deux systèmes de coordonnées.

![Systèmes de coordonnées de gauche et droite](images/left-hand-right-hand.gif)<br>
*Systèmes de coordonnées de gauche et droite*

Pour l’amorçage dans un SpatialCoordinateSystem selon la position d’un HoloLens, utilisez le <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a> classe pour créer soit une jointe ou stationnaire de référence, comme décrit dans les sections ci-dessous.

## <a name="place-holograms-in-the-world-using-a-spatial-stage"></a>Hologrammes place dans le monde à l’aide d’une phase spatiale

Le système de coordonnées pour des casques IMMERSIFS Windows Mixed Reality opaques est accessible à l’aide de la méthode statique <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference.current" target="_blank">SpatialStageFrameOfReference::Current</a> propriété. Cette API fournit un système de coordonnées, les informations sur indique si le lecteur est inséré ou mobiles, la limite d’une zone de sécurité pour vous épargne si le lecteur est mobile, et indique s’il faut ou non le casque est directionnel. Il existe également un gestionnaire d’événements pour les mises à jour à l’étape spatiale.

Tout d’abord, nous avons obtenir la scène spatiale et s’abonner pour les mises à jour correspondantes : 

Code pour **l’initialisation de phase spatiale**

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

Dans la méthode OnCurrentChanged, votre application doit inspecter la scène spatiale et mettre à jour l’expérience de joueur en conséquence. Dans cet exemple, nous fournissons une visualisation de la limite de la scène, ainsi que la position de début spécifiée par l’utilisateur et de la plage de la phase de vue et de la gamme de déplacement des propriétés. Nous avons également revenir à notre propre système de coordonnées stationnaire, lorsqu’une étape ne peut pas être fournie.


Code pour **mise à jour de la phase spatiale**

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

L’ensemble de sommets qui définissent la limite étape sont fournies dans le sens horaire. L’interpréteur de commandes Windows Mixed Reality Dessine une frontière de sécurité à la limite lors de l’utilisateur à l’approche ; Vous pouvez souhaiter triangularize la zone opérationnel pour vos propres besoins. L’algorithme suivant peut être utilisé pour triangularize la scène.


Code pour **triangularization de phase spatiale**

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

## <a name="place-holograms-in-the-world-using-a-stationary-frame-of-reference"></a>Hologrammes place dans le monde à l’aide d’un système de référence stationnaire

Le [SpatialStationaryFrameOfReference](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialstationaryframeofreference.aspx) classe représente une image de référence qui [reste stationnaire](coordinate-systems.md#stationary-frame-of-reference) par rapport aux environs de l’utilisateur en tant que l’utilisateur se déplace. Ce cadre de référence hiérarchise les coordonnées de conservation stable près de l’appareil. Une des principales utilisations d’un SpatialStationaryFrameOfReference consiste à agir en tant que le système de coordonnées de monde sous-jacent au sein d’un moteur de rendu lors du rendu hologrammes.

Pour obtenir un SpatialStationaryFrameOfReference, utilisez le [SpatialLocator](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatiallocator.aspx) classe et appelez [CreateStationaryFrameOfReferenceAtCurrentLocation](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatiallocator.createstationaryframeofreferenceatcurrentlocation.aspx).

À partir du code du modèle application Windows HOLOGRAPHIQUE :

```
           // The simplest way to render world-locked holograms is to create a stationary reference frame
           // when the app is launched. This is roughly analogous to creating a "world" coordinate system
           // with the origin placed at the device's position as the app is launched.
           referenceFrame = locator.CreateStationaryFrameOfReferenceAtCurrentLocation();
```
* Trames de référence stationnaire sont conçus pour fournir une position ajustée par rapport à l’espace global. Postes individuels dans ce cadre de référence sont autorisés à dérives légèrement. Ceci est normal que l’appareil en apprend plus sur l’environnement.
* Lorsque le positionnement précis des hologrammes individuels est requis, un SpatialAnchor doit être utilisé pour ancrer l’hologramme individuel vers une position dans le monde réel : par exemple, un point de l’utilisateur indique le pour intéresser. Les positions d’ancrage ne pas dérive, mais peuvent être corrigées ; le point d’ancrage utilise la position corrigée à partir de l’image suivante après la correction.

## <a name="place-holograms-in-the-world-using-spatial-anchors"></a>Hologrammes place dans le monde à l’aide de points d’ancrage spatiales

[Ancres spatiales](coordinate-systems.md#spatial-anchors) sont un excellent moyen pour placer hologrammes à un emplacement spécifique dans le monde réel, avec le système en garantissant le point d’ancrage reste en place au fil du temps. Cette rubrique explique comment créer et utiliser un point d’ancrage et l’utilisation des données de point d’ancrage.

Vous pouvez créer un SpatialAnchor à toute position et l’orientation dans le SpatialCoordinateSystem de votre choix. L’appareil doit être en mesure de localiser ce système de coordonnées pour le moment, et le système ne doit pas avoir atteint sa limite ancres spatiales.

Une fois défini, le système de coordonnées d’un SpatialAnchor s’ajuste en permanence pour conserver la position précise et l’orientation de son emplacement initial. Vous pouvez ensuite utiliser cette SpatialAnchor pour restituer hologrammes apparaîtront fixes dans l’environnement de l’utilisateur à l’emplacement spécifié.

Les effets des ajustements qui empêchent le point d’ancrage en place sont amplifient encore comme la distance à partir de l’augmentation d’ancrage. Par conséquent, vous devez éviter de restituer le contenu par rapport à un point d’ancrage est supérieure à 3 mètres à partir de l’origine de ce point d’ancrage.

Le [CoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.coordinatesystem.aspx) propriété obtient un système de coordonnées qui vous permet de placer le contenu par rapport à l’ancre, avec accélération appliquée lorsque l’appareil s’ajuste l’emplacement précis de l’ancre.

Utilisez le [RawCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.rawcoordinatesystem.aspx) propriété et le correspondantes [RawCoordinateSystemAdjusted](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted.aspx) événement à gérer ces ajustements vous-même.

### <a name="persist-and-share-spatial-anchors"></a>Conserver et partager des ancres spatiales

Vous pouvez conserver un SpatialAnchor localement à l’aide de la [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx) classe et de retour dans une session de futures de l’application sur le même appareil HoloLens.

À l’aide de <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a>, vous pouvez créer un point d’ancrage cloud durable à partir d’un SpatialAnchor local, lequel votre application peut ensuite localiser dans plusieurs HoloLens, appareils iOS et Android.  En partageant une ancre spatiale commune sur plusieurs appareils, chaque utilisateur peut voir le contenu restitué par rapport à ce point d’ancrage dans le même emplacement physique.  Ainsi, les expériences partagées en temps réel.

Vous pouvez également utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a> pour la persistance hologramme asynchrone sur HoloLens, appareils iOS et Android.  En partageant une ancre spatial cloud durable, plusieurs périphériques peuvent observer l’hologramme persistante même au fil du temps, même si ces appareils ne sont pas présents ensemble en même temps.

Pour commencer à créer des expériences partagées dans votre application HoloLens, essayez les 5 minutes <a href="https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens" target="_blank">Guide de démarrage rapide Azure Spatial ancres HoloLens</a>.

Une fois que vous êtes en cours d’exécution ancres spatiale d’Azure, vous pouvez ensuite <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-cpp-winrt" target="_blank">créer et localiser les points d’ancrage sur HoloLens</a>.  Procédures pas à pas sont disponibles pour <a href="https://docs.microsoft.com/azure/spatial-anchors/create-locate-anchors-overview" target="_blank">Android et iOS</a> également, ce qui vous permet de partager les ancres mêmes sur tous les appareils.

### <a name="create-spatialanchors-for-holographic-content"></a>Créer SpatialAnchors pour le contenu HOLOGRAPHIQUE

Pour cet exemple de code, nous avons modifié Windows HOLOGRAPHIQUE ancre de modèle d’application à créer lorsque le **Pressed** mouvement est détecté. Le cube est ensuite placé dans le point d’ancrage pendant la passe de rendu.

Dans la mesure où plusieurs points d’ancrage sont pris en charge par la classe d’assistance, nous pouvons placer autant de cubes que nous voulons à l’aide de cet exemple de code !

Notez que les ID d’ancrage sont quelque chose que vous contrôler dans votre application. Dans cet exemple, nous avons créé un schéma d’affectation de noms est séquentiel, en fonction du nombre d’ancres actuellement stockés dans la collection de l’application de points d’ancrage.

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

### <a name="asynchronously-load-and-cache-the-spatialanchorstore"></a>En mode asynchrone charger et mettre en cache, le SpatialAnchorStore

Nous allons voir comment écrire une classe SampleSpatialAnchorHelper qui permet de gérer cette persistance, y compris :
* Stocker une collection de points d’ancrage en mémoire, indexées par une clé de Platform::String.
* Chargement des points d’ancrage à partir SpatialAnchorStore du système, qui sont maintenu séparé à partir de la collection en mémoire locale.
* L’enregistrement de la collection en mémoire locale des ancres d’à la SpatialAnchorStore lorsque l’application choisit à le faire.

Voici comment enregistrer [SpatialAnchor](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) des objets dans le [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx).

Au démarrage de la classe, nous demandons la SpatialAnchorStore de façon asynchrone. Cela implique d’e/s de système comme l’API charge le magasin d’ancrage, et cette API est effectuée asynchrone afin que les e/s est non bloquant.

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

Nous vous fournirons un SpatialAnchorStore que vous pouvez utiliser pour enregistrer les ancres. Il s’agit d’un IMapView qui associe les valeurs de clés qui sont des chaînes, avec les valeurs de données qui sont SpatialAnchors. Dans notre exemple de code, nous stockez-le dans une variable de membre de classe privée qui est accessible via une fonction publique de notre classe d’assistance.

```
   SampleSpatialAnchorHelper::SampleSpatialAnchorHelper(SpatialAnchorStore^ anchorStore)
   {
       m_anchorStore = anchorStore;
       m_anchorMap = ref new Platform::Collections::Map<String^, SpatialAnchor^>();
   }
```

>[!NOTE]
>N’oubliez pas de raccorder les événements suspend/resume pour enregistrer et charger le magasin d’ancrage.

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

### <a name="save-content-to-the-anchor-store"></a>Enregistrer le contenu dans le magasin d’ancrage

Lorsque le système interrompt votre application, vous devez enregistrer les points d’ancrage spatiales dans le magasin de point d’ancrage. Vous pouvez également choisir d’enregistrer des ancres dans le magasin d’ancrage à d’autres moments, que vous avez trouvé comme étant nécessaires pour la mise en œuvre de votre application.

Lorsque vous êtes prêt pour enregistrer les points d’ancrage en mémoire pour le SpatialAnchorStore, vous pouvez parcourir votre collection et essayez d’enregistrer chacune d’elles.

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

### <a name="load-content-from-the-anchor-store-when-the-app-resumes"></a>Charger le contenu à partir du magasin d’ancrage lorsque l’application reprend

Lorsque votre application se poursuit, ou à tout moment nécessaire pour les implementaiton de votre application, vous pouvez restaurer les points d’ancrage qui ont été précédemment enregistrées pour le AnchorStore par les transférer à partir IMapView du magasin d’ancrage à votre propre base de données en mémoire de SpatialAnchors.

Pour restaurer les points d’ancrage à partir de la SpatialAnchorStore, restaurer Chacun d’eux qui vous intéresse à votre propre collection en mémoire.

Vous avez besoin de votre propre base de données en mémoire de SpatialAnchors ; un moyen d’associer des chaînes avec SpatialAnchors que vous créez. Dans notre exemple de code, nous choisissons d’utiliser un Windows::Foundation::Collections::IMap pour stocker les ancres, ce qui la rend facile à utiliser la même valeur de clé et les données pour le SpatialAnchorStore.

```
   // This is an in-memory anchor list that is separate from the anchor store.
   // These anchors may be used, reasoned about, and so on before committing the collection to the store.
   Windows::Foundation::Collections::IMap<Platform::String^, Windows::Perception::Spatial::SpatialAnchor^>^ m_anchorMap;
```

>[!NOTE]
>Une ancre qui est restaurée n’est pas immédiatement toujours localisable. Par exemple, il peut être un point d’ancrage dans une salle distincte ou dans une autre génération complètement. Ancres récupérées à partir de la AnchorStore doivent être testés pour locatability avant de les utiliser.

<br>

>[!NOTE]
>Dans cet exemple de code, nous récupérons tous les points d’ancrage à partir de la AnchorStore. Cela n’est pas obligatoire ; votre application pourrait tout aussi bien choisir un sous-ensemble spécifique de points d’ancrage à l’aide des valeurs de clés de chaîne qui sont significatives pour votre implémentation.

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

### <a name="clear-the-anchor-store-when-needed"></a>Effacer le magasin d’ancrage, si nécessaire

Parfois, vous devez effacer l’état de l’application et d’écriture de nouvelles données. Voici comment procéder avec le [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx).

À l’aide de notre classe d’assistance, il est presque pas nécessaire d’inclure dans un wrapper la fonction Clear. Nous choisissons à le faire dans notre exemple d’implémentation, étant donné que notre classe d’assistance porte la responsabilité du propriétaire de l’instance SpatialAnchorStore.

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

### <a name="example-relating-anchor-coordinate-systems-to-stationary-reference-frame-coordinate-systems"></a>Exemple : Systèmes de coordonnées de cadre de référence stationnaire concernant les systèmes de coordonnées de point d’ancrage

Supposons que vous avez un point d’ancrage, et que vous souhaitez quelque chose dans le système de coordonnées de votre point d’ancrage se rapportent à SpatialStationaryReferenceFrame que vous utilisez déjà pour la plupart des autres votre contenu. Vous pouvez utiliser [TryGetTransformTo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.trygettransformto.aspx) pour obtenir une transformation à partir du système de coordonnées de l’ancre à celle de l’image de référence stationnaire :

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

Ce processus est utile pour vous de deux manières :
1. Elle indique si les deux images de référence peuvent être reconnus par rapport aux autres, et ;
2. Dans ce cas, il vous fournit une transformation pour accéder directement à partir d’un système de coordonnées à l’autre.

Avec ces informations, vous avez une connaissance de la relation spatiale entre les objets entre les deux images de référence.

Pour le rendu, vous pouvez souvent obtenir de meilleurs résultats en regroupant les objets en fonction de leur image de référence d’origine ou d’un point d’ancrage. Effectuer une étape de dessin distincte pour chaque groupe. Les matrices de vue sont plus précises pour les objets avec des transformations de modèle qui sont créées initialement à l’aide du même système de coordonnées.

## <a name="create-holograms-using-a-device-attached-frame-of-reference"></a>Créer hologrammes à l’aide d’un périphérique connecté de référence

Parfois, lorsque vous souhaitez restituer un hologramme qui [reste attachée](coordinate-systems.md#attached-frame-of-reference) à l’emplacement de l’appareil, par exemple un panneau avec les informations ou un message d’information de débogage quand l’appareil est uniquement en mesure de déterminer son orientation et pas sa position dans l’espace. Pour ce faire, nous utilisons un cadre de référence jointe.

La classe SpatialLocatorAttachedFrameOfReference définit des systèmes de coordonnées qui sont par rapport à l’appareil, plutôt que dans le monde réel. Cette image a un titre fixe par rapport aux environs de l’utilisateur qui pointe dans la direction de l’utilisateur a été confronté lors de la création de l’image de référence. Dès lors, toutes les orientations dans ce cadre de référence sont par rapport à ce titre fixe, même lorsque l’utilisateur fait pivoter l’appareil.

Pour HoloLens, l’origine de cette image système de coordonnées se trouve au centre de rotation de tête de l’utilisateur, afin que sa position n’est pas affectée par rotation principale. Votre application peut spécifier un décalage par rapport à ce point pour positionner hologrammes devant l’utilisateur.

Pour obtenir un SpatialLocatorAttachedFrameOfReference, utilisez la classe SpatialLocator et appeler CreateAttachedFrameOfReferenceAtCurrentHeading.

Notez que cela s’applique aux appareils toute plage de Windows Mixed Reality.

### <a name="use-a-reference-frame-attached-to-the-device"></a>Utiliser une image de référence associée à l’appareil

Ces sections parler de ce que nous avons modifié dans le modèle d’application Windows HOLOGRAPHIQUE pour activer une périphérique connecté de référence à l’aide de cette API. Notez que cette hologramme « joint » est exécutés en parallèle hologrammes ancrés ou STATIONNAIRES et peut également être utilisé quand l’appareil est temporairement Impossible de trouver sa position dans le monde.

Tout d’abord, nous avons modifié le modèle pour stocker un SpatialLocatorAttachedFrameOfReference au lieu d’un SpatialStationaryFrameOfReference :

À partir de **HolographicTagAlongSampleMain.h**:

```
   // A reference frame attached to the holographic camera.
   Windows::Perception::Spatial::SpatialLocatorAttachedFrameOfReference^   m_referenceFrame;
```

À partir de **HolographicTagAlongSampleMain.cpp**:

```
   // In this example, we create a reference frame attached to the device.
   m_referenceFrame = m_locator->CreateAttachedFrameOfReferenceAtCurrentHeading();
```

Pendant la mise à jour, nous obtenons maintenant le système de coordonnées à l’horodatage obtenue à partir d’avec la prédiction de frame.

```
   // Next, we get a coordinate system from the attached frame of reference that is
   // associated with the current frame. Later, this coordinate system is used for
   // for creating the stereo view matrices when rendering the sample content.
   SpatialCoordinateSystem^ currentCoordinateSystem =
       m_referenceFrame->GetStationaryCoordinateSystemAtTimestamp(prediction->Timestamp);
```

### <a name="get-a-spatial-pointer-pose-and-follow-the-users-gaze"></a>Obtenir une pose de pointeur spatiale et suivez les regards de l’utilisateur

Nous voulons que notre hologramme d’exemple à suivre l’utilisateur [les regards](gaze.md), similaire à comment l’interpréteur de commandes HOLOGRAPHIQUE peut suivre des regards de l’utilisateur. Pour ce faire, nous devons obtenir le SpatialPointerPose à partir de la même horodatage.

```
SpatialPointerPose^ pose = SpatialPointerPose::TryGetAtTimestamp(currentCoordinateSystem, prediction->Timestamp);
```

Cette SpatialPointerPose a les informations nécessaires pour positionner l’hologramme conformément à la [titre actuel de l’utilisateur](gaze-in-directx.md).

Pour des raisons de confort de l’utilisateur, nous utilisons une interpolation linéaire (« lerp ») pour lisser la modification de la position où il se produit sur une période de temps. Il s’agit plus à l’aise pour l’utilisateur que l’hologramme à leur regards de verrouillage. Lerping que position de l’hologramme tag-along permet également de stabiliser le hologramme par atténuation pour le déplacement ; Si nous n’avez pas ce blocage, l’utilisateur verrait l’hologramme instabilité en raison de ce qui sont normalement considéré comme imperceptibles mouvements de tête de l’utilisateur.

From **StationaryQuadRenderer::PositionHologram**:

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
>Dans le cas d’un panneau de débogage, vous pouvez choisir repositionner un peu l’hologramme désactivé pour le côté afin qu’elle ne gêne pas votre affichage. Voici un exemple de comment vous pouvez le faire.

Pour **StationaryQuadRenderer::PositionHologram**:

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

### <a name="rotate-the-hologram-to-face-the-camera"></a>Faire pivoter l’hologramme pour faire face à l’appareil photo

Il n’est pas suffisant de simplement positionner HOLOGRAMME, qui est dans ce cas un quadruple ; Nous devons également faire pivoter l’objet pour faire face à l’utilisateur. Notez que cette rotation s’effectue dans l’espace universel, car ce type de le billboarding permet l’hologramme reste une partie de l’environnement utilisateur. Espace d’affichage le billboarding n’est pas à l’aise, car l’hologramme est verrouillé à l’orientation de l’affichage ; Dans ce cas, vous devrez également interpoler entre les matrices de vue de gauche et droite afin d’acquérir une transformation de tableau blanc espace d’affichage qui n’interrompt pas rendu stéréo. Ici, nous faire pivoter sur les axes X et Z pour faire face à l’utilisateur.

À partir de **StationaryQuadRenderer::Update**:

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

### <a name="render-the-attached-hologram"></a>Restituer la hologramme attaché

Pour cet exemple, nous avons également choisir restituer l’hologramme dans le système de coordonnées de la SpatialLocatorAttachedReferenceFrame, c'est-à-dire où nous avons positionné la hologramme. (Si nous avions décidé d’effectuer le rendu à l’aide d’un autre système de coordonnées, nous devons acquérir une transformation à partir du système de coordonnées du cadre de référence de périphérique connecté à ce système de coordonnées.)

From **HolographicTagAlongSampleMain::Render**:

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

C’est tout ! L’hologramme sera désormais « repère » une position qui est de 2 mètres devant la direction du regard de l’utilisateur.

>[!NOTE]
>Cet exemple charge également le contenu supplémentaire, consultez StationaryQuadRenderer.cpp.

## <a name="handling-tracking-loss"></a>Suivi de la perte de la gestion des

Lorsque l’appareil ne peut pas localiser lui-même dans le monde, l’application rencontre « perte de suivi ». Applications de réalité mixte Windows doivent être en mesure de gérer les perturbations pour le système de suivi positionnels. Ces interruptions peuvent être observées et la création de réponses à l’aide de l’événement LocatabilityChanged sur la valeur par défaut SpatialLocator.

À partir de **AppMain::SetHolographicSpace :**

```
   // Be able to respond to changes in the positional tracking state.
   m_locatabilityChangedToken =
       m_locator->LocatabilityChanged +=
           ref new Windows::Foundation::TypedEventHandler<SpatialLocator^, Object^>(
               std::bind(&HolographicApp1Main::OnLocatabilityChanged, this, _1, _2)
               );
```

Lorsque votre application reçoit un événement LocatabilityChanged, il peut modifier le comportement en fonction des besoins. Par exemple, dans l’état PositionalTrackingInhibited, votre application peut interrompre le fonctionnement normal et restituer un [hologramme de tag-along](coordinate-systems-in-directx.md#create-holograms-using-a-device-attached-frame-of-reference) qui affiche un message d’avertissement.

Le modèle d’application Windows holographique est fourni avec un gestionnaire LocatabilityChanged déjà créé pour vous. Par défaut, il affiche un avertissement dans la console de débogage lorsque le suivi de position n’est pas disponible. Vous pouvez ajouter du code à ce gestionnaire pour fournir une réponse en fonction des besoins de votre application.

À partir de **AppMain.cpp :**

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

## <a name="spatial-mapping"></a>Mappage spatial

Le [mappage spatial](spatial-mapping-in-directx.md) API permettent l’utilisation de systèmes de coordonnées pour obtenir des transformations de modèle pour les maillages de surface.

## <a name="see-also"></a>Voir aussi
* [Systèmes de coordonnées](coordinate-systems.md)
* [Ancres spatiales](spatial-anchors.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>
* [HEAD et surveillez les regards dans DirectX](gaze-in-directx.md)
* [Mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md)
* [Mappage spatial dans DirectX](spatial-mapping-in-directx.md)
