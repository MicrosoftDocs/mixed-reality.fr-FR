---
title: Systèmes de coordonnées dans DirectX
description: Explique comment utiliser des localisateurs spatiaux Windows mixtes, des frames de référence, des ancres spatiales et des systèmes de coordonnées, comment utiliser le SpatialStage, comment gérer les pertes de suivi, comment enregistrer et charger des ancres et comment effectuer une stabilisation d’image.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: Réalité mixte, localisateur spatial, frame de référence spatiale, système de coordonnées spatiales, étape spatiale, exemple de code, stabilisation d’image, point d’ancrage spatial, magasin d’ancrage spatial, perte de suivi, procédure pas à pas
ms.openlocfilehash: a0bce897c1982715af24f0bf7c398cdee10f017f
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73436224"
---
# <a name="coordinate-systems-in-directx"></a>Systèmes de coordonnées dans DirectX

Les [systèmes de coordonnées](coordinate-systems.md) constituent la base de la compréhension spatiale offerte par les API Windows Mixed Reality.

Les appareils de VR ou de monolocalisation d’aujourd’hui établissent un système de coordonnées principal pour représenter leur espace suivi. Les appareils Windows Mixed Reality, tels que HoloLens, sont conçus pour être utilisés dans tous les environnements non définis, avec la découverte des appareils et l’apprentissage de son environnement à mesure que l’utilisateur parcourt. Cela permet à l’appareil de s’adapter à l’amélioration continue des connaissances sur les salles de l’utilisateur, mais il en résulte des systèmes de coordonnées qui modifieront leur relation l’un à l’autre au cours de la durée de vie de l’application. Windows Mixed Reality prend en charge un large éventail d’appareils, allant des casques immersifs intégrés à des châssis de référence universels.

>[!NOTE]
>Les extraits de code de cet article illustrent actuellement l' C++utilisation de/CX plutôt que de C++/WinRT conforme C + +17, comme utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).  Les concepts sont équivalents pour C++un projet/WinRT, bien que vous deviez traduire le code.

## <a name="spatial-coordinate-systems-in-windows"></a>Systèmes de coordonnées spatiales dans Windows

Le type de cœur utilisé pour la raison des systèmes de coordonnées réels dans Windows est le <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a>. Une instance de ce type représente un système de coordonnées arbitraire et fournit une méthode pour obtenir une matrice de transformation que vous pouvez utiliser pour transformer deux systèmes de coordonnées sans comprendre les détails de chacun d’entre eux.

Les méthodes qui retournent des informations spatiales, représentées par des points, des rayons ou des volumes dans l’environnement de l’utilisateur, acceptent un paramètre SpatialCoordinateSystem pour vous permettre de déterminer le système de coordonnées dans lequel elles sont les plus utiles pour que ces coordonnées soient retournées. Les unités de ces coordonnées seront toujours exprimées en mètres.

Un SpatialCoordinateSystem a une relation dynamique avec d’autres systèmes de coordonnées, y compris ceux qui représentent la position de l’appareil. À tout moment, l’appareil peut être en mesure de localiser certains systèmes de coordonnées et pas d’autres. Pour la plupart des systèmes de coordonnées, votre application doit être prête à gérer les périodes pendant lesquelles elles sont introuvables.

Votre application ne doit pas créer de SpatialCoordinateSystems directement, mais elle doit être utilisée via les API de perception. Il existe trois sources principales de systèmes de coordonnées dans les API de perception, chacune d’elles étant mappée à un concept décrit dans la page des [systèmes de coordonnées](coordinate-systems.md) :
* Pour obtenir une image de référence fixe, créez un <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstationaryframeofreference" target="_blank">SpatialStationaryFrameOfReference</a> ou obtenez-en un à partir du <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference" target="_blank">SpatialStageFrameOfReference</a>actuel.
* Pour obtenir une ancre spatiale, créez un <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a>.
* Pour obtenir un cadre de référence attaché, créez un <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocatorattachedframeofreference" target="_blank">SpatialLocatorAttachedFrameOfReference</a>.

Tous les systèmes de coordonnées retournés par ces objets sont droitiers, avec + y vers le haut, + x vers la droite et + z vers l’arrière. Vous pouvez vous souvenir de la direction vers laquelle pointe l’axe z positif en pointant les doigts de votre gauche ou de droite dans la direction x positive et en les plaçant dans la direction y positive. La direction vers laquelle pointe votre pouce (vers vous ou à l'opposé) correspond à la direction dans laquelle pointe l’axe z positif pour ce système de coordonnées. L’illustration suivante décrit ces deux systèmes de coordonnées.

![systèmes de coordonnées à gauche et à droite](images/left-hand-right-hand.gif)<br>
*Systèmes de coordonnées à gauche et à droite*

Pour démarrer dans un SpatialCoordinateSystem en fonction de la position d’un HoloLens, utilisez la classe <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a> pour créer une image de référence attachée ou stationnaire, comme décrit dans les sections ci-dessous.

## <a name="place-holograms-in-the-world-using-a-spatial-stage"></a>Placer des hologrammes dans le monde à l’aide d’une étape spatiale

Le système de coordonnées pour les casques immersifs immersifs de la réalité Windows mixed est accessible à l’aide de la propriété statique <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialstageframeofreference.current" target="_blank">SpatialStageFrameOfReference :: Current</a> . Cette API fournit un système de coordonnées, des informations indiquant si le joueur est assis ou mobile, la limite d’une zone sûre pour se déplacer si le joueur est mobile, et indique si le casque est directionnel. Il existe également un gestionnaire d’événements pour les mises à jour de la phase spatiale.

Tout d’abord, nous obtenons la phase spatiale et m’abonnons aux mises à jour : 

Code pour **l’initialisation de la phase spatiale**

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

Dans la méthode OnCurrentChanged, votre application doit inspecter la phase spatiale et mettre à jour l’expérience du joueur en conséquence. Dans cet exemple, nous fournissons une visualisation de la limite de la phase, ainsi que la position de départ spécifiée par l’utilisateur, ainsi que la plage d’affichage et la plage des propriétés de déplacement de l’étape. Nous revenons également à notre propre système de coordonnées stationnaires, lorsqu’une étape ne peut pas être fournie.


Code pour la **mise à jour de la phase spatiale**

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

L’ensemble des vertex qui définissent les limites de l’étape sont fournis dans l’ordre des aiguilles d’une montre. Le shell Windows Mixed Reality dessine une clôture à la limite lorsque l’utilisateur l’approche ; vous souhaiterez peut-être triangulaire la zone à votre convenance. L’algorithme suivant peut être utilisé pour triangulairer la phase.


Code pour **triangulaire de la phase spatiale**

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

## <a name="place-holograms-in-the-world-using-a-stationary-frame-of-reference"></a>Placez des hologrammes dans le monde à l’aide d’un cadre stationnaire de référence

La classe [SpatialStationaryFrameOfReference](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialstationaryframeofreference.aspx) représente une image de référence qui [reste stationnaire](coordinate-systems.md#stationary-frame-of-reference) par rapport à l’environnement de l’utilisateur au fur et à mesure que l’utilisateur se déplace. Ce cadre de référence établit une priorité pour maintenir les coordonnées stables près de l’appareil. L’une des principales utilisation d’un SpatialStationaryFrameOfReference consiste à agir comme système de coordonnées universelles sous-jacent dans un moteur de rendu lors du rendu d’hologrammes.

Pour obtenir un SpatialStationaryFrameOfReference, utilisez la classe [SpatialLocator](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatiallocator.aspx) et appelez [CreateStationaryFrameOfReferenceAtCurrentLocation](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatiallocator.createstationaryframeofreferenceatcurrentlocation.aspx).

À partir du code du modèle d’application holographique Windows :

```
           // The simplest way to render world-locked holograms is to create a stationary reference frame
           // when the app is launched. This is roughly analogous to creating a "world" coordinate system
           // with the origin placed at the device's position as the app is launched.
           referenceFrame = locator.CreateStationaryFrameOfReferenceAtCurrentLocation();
```
* Les frames de référence stationnaires sont conçus pour fournir une position la mieux adaptée par rapport à l’espace global. Les positions individuelles dans ce frame de référence sont autorisées à dériver légèrement. Cela est normal, car l’appareil en apprend davantage sur l’environnement.
* Lorsque le positionnement précis des hologrammes individuels est requis, un SpatialAnchor doit être utilisé pour ancrer l’hologramme individuel à une position dans le monde réel (par exemple, un point que l’utilisateur indique d’avoir un intérêt particulier). Les positions d’ancrage ne dérivent pas, mais peuvent être corrigées ; le point d’ancrage utilise la position corrigée à partir de l’image suivante, une fois la correction effectuée.

## <a name="place-holograms-in-the-world-using-spatial-anchors"></a>Placer des hologrammes dans le monde à l’aide d’ancres spatiales

Les [ancres spatiales](coordinate-systems.md#spatial-anchors) sont un excellent moyen de placer des hologrammes à un endroit précis dans le monde réel, le système garantissant que l’ancre reste en place au fil du temps. Cette rubrique explique comment créer et utiliser une ancre, et comment utiliser les données d’ancrage.

Vous pouvez créer un SpatialAnchor à n’importe quelle position et orientation dans le SpatialCoordinateSystem de votre choix. L’appareil doit être en mesure de localiser ce système de coordonnées pour le moment et le système ne doit pas avoir atteint sa limite d’ancrages spatiaux.

Une fois défini, le système de coordonnées d’un SpatialAnchor s’ajuste continuellement pour conserver la position et l’orientation précises de son emplacement initial. Vous pouvez ensuite utiliser ce SpatialAnchor pour afficher des hologrammes qui seront corrigés dans l’environnement de l’utilisateur à cet emplacement exact.

Les effets des ajustements qui maintiennent l’ancre sont agrandis à mesure que la distance entre l’ancrage augmente. Par conséquent, vous devez éviter de rendre le contenu relatif à une ancre supérieure à environ 3 mètres de l’origine de cette ancre.

La propriété [CoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.coordinatesystem.aspx) obtient un système de coordonnées qui vous permet de placer du contenu par rapport à l’ancre, avec une accélération appliquée lorsque l’appareil ajuste l’emplacement précis de l’ancre.

Utilisez la propriété [RawCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.rawcoordinatesystem.aspx) et l’événement [RawCoordinateSystemAdjusted](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted.aspx) correspondant pour gérer ces réglages vous-même.

### <a name="persist-and-share-spatial-anchors"></a>Conserver et partager des ancres spatiales

Vous pouvez conserver un SpatialAnchor localement à l’aide de la classe [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx) , puis le récupérer dans une session d’application future sur le même appareil HoloLens.

En utilisant des <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres spatiales Azure</a>, vous pouvez créer une ancre Cloud durable à partir d’un SpatialAnchor local, que votre application peut ensuite localiser sur plusieurs appareils HoloLens, iOS et Android.  En partageant une ancre spatiale commune sur plusieurs appareils, chaque utilisateur peut voir le contenu affiché par rapport à cette ancre dans le même emplacement physique.  Cette technique autorise les expériences partagées en temps réel.

Vous pouvez également utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a> pour la persistance asynchrone des hologrammes sur les appareils HoloLens, iOS et Android.  En partageant une ancre spatiale cloud durable, plusieurs appareils peuvent observer le même hologramme conservé au fil du temps, même si ces appareils ne sont pas présents ensemble en même temps.

Pour commencer à créer des expériences partagées dans votre application HoloLens, essayez le démarrage rapide de 5 minutes d' <a href="https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens" target="_blank">ancrage spatial Azure HoloLens</a>.

Une fois que vous êtes opérationnel avec les ancres spatiales Azure, vous pouvez <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-cpp-winrt" target="_blank">créer et localiser des ancres sur HoloLens</a>.  Les procédures pas à pas sont également disponibles pour <a href="https://docs.microsoft.com/azure/spatial-anchors/create-locate-anchors-overview" target="_blank">Android et iOS</a> , ce qui vous permet de partager les mêmes ancres sur tous les appareils.

### <a name="create-spatialanchors-for-holographic-content"></a>Créer des SpatialAnchors pour le contenu holographique

Pour cet exemple de code, nous avons modifié le modèle d’application holographique Windows pour créer des ancres lorsque le geste **appuyé** est détecté. Le cube est ensuite placé au point d’ancrage pendant la passe de rendu.

Étant donné que plusieurs points d’ancrage sont pris en charge par la classe d’assistance, nous pouvons placer autant de cubes que vous le souhaitez à l’aide de cet exemple de code !

Notez que les ID des ancres sont des éléments que vous contrôlez dans votre application. Dans cet exemple, nous avons créé un modèle d’affectation de noms qui est séquentiel en fonction du nombre d’ancres actuellement stockées dans la collection d’ancres de l’application.

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

### <a name="asynchronously-load-and-cache-the-spatialanchorstore"></a>Charger et mettre en cache de façon asynchrone SpatialAnchorStore

Voyons comment écrire une classe SampleSpatialAnchorHelper qui permet de gérer cette persistance, notamment :
* Stockage d’une collection d’ancres en mémoire, indexées par une clé Platform :: String.
* Chargement des ancres à partir du SpatialAnchorStore du système, qui est conservé distinct de la collection en mémoire locale.
* Enregistrement de la collection en mémoire locale des ancres dans le SpatialAnchorStore quand l’application choisit de le faire.

Voici comment enregistrer des objets [SpatialAnchor](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) dans [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx).

Lorsque la classe démarre, nous recherchons le SpatialAnchorStore de manière asynchrone. Cela implique des e/s système, car l’API charge le magasin d’ancrage, et cette API est rendue asynchrone afin que les e/s soient non bloquantes.

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

Vous aurez un SpatialAnchorStore que vous pouvez utiliser pour enregistrer les ancres. Il s’agit d’un IMapView qui associe des valeurs de clés qui sont des chaînes, avec des valeurs de données qui sont SpatialAnchors. Dans notre exemple de code, nous le stockons dans une variable membre de classe privée qui est accessible par le biais d’une fonction publique de notre classe d’assistance.

```
   SampleSpatialAnchorHelper::SampleSpatialAnchorHelper(SpatialAnchorStore^ anchorStore)
   {
       m_anchorStore = anchorStore;
       m_anchorMap = ref new Platform::Collections::Map<String^, SpatialAnchor^>();
   }
```

>[!NOTE]
>N’oubliez pas de raccorder les événements de suspension/reprise pour enregistrer et charger le magasin d’ancrage.

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

Lorsque le système interrompt votre application, vous devez enregistrer vos ancres spatiales dans le magasin d’ancrage. Vous pouvez également choisir d’enregistrer les ancres dans le magasin d’ancrage à d’autres moments, car vous en aurez besoin pour l’implémentation de votre application.

Lorsque vous êtes prêt à essayer d’enregistrer les ancres en mémoire dans le SpatialAnchorStore, vous pouvez parcourir votre collection et essayer d’enregistrer chacune d’elles.

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

Lorsque votre application reprend, ou à tout moment nécessaire pour le implementaiton de votre application, vous pouvez restaurer les ancres précédemment enregistrées dans le AnchorStore en les transférant du IMapView de la boutique d’ancrage à votre propre base de données en mémoire de SpatialAnchors.

Pour restaurer les ancres à partir du SpatialAnchorStore, restaurez chacune d’elles qui vous intéresse à votre propre collection en mémoire.

Vous avez besoin de votre propre base de données en mémoire de SpatialAnchors ; un moyen d’associer des chaînes à l’SpatialAnchors que vous créez. Dans notre exemple de code, nous choisissons d’utiliser un Windows :: Foundation :: Collections :: IMap pour stocker les ancres, ce qui facilite l’utilisation de la même clé et de la même valeur de données pour SpatialAnchorStore.

```
   // This is an in-memory anchor list that is separate from the anchor store.
   // These anchors may be used, reasoned about, and so on before committing the collection to the store.
   Windows::Foundation::Collections::IMap<Platform::String^, Windows::Perception::Spatial::SpatialAnchor^>^ m_anchorMap;
```

>[!NOTE]
>Une ancre qui est restaurée peut ne pas être localisable immédiatement. Par exemple, il peut s’agir d’une ancre dans une salle distincte ou dans une construction différente. Les ancres récupérées à partir du AnchorStore doivent être testées en vue de leur localisation avant de les utiliser.

<br>

>[!NOTE]
>Dans cet exemple de code, nous récupérons toutes les ancres du AnchorStore. Ce n’est pas une condition requise. votre application peut tout aussi bien sélectionner et choisir un certain sous-ensemble d’ancres à l’aide de valeurs de clés de chaîne qui sont significatives pour votre implémentation.

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

Parfois, vous devez effacer l’état de l’application et écrire de nouvelles données. Voici comment procéder avec [SpatialAnchorStore](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchorstore.aspx).

À l’aide de la classe d’assistance, il est presque inutile d’encapsuler la fonction Clear. Nous choisissons cette opération dans notre exemple d’implémentation, car la responsabilité de la propriétaire de l’instance SpatialAnchorStore est attribuée à notre classe d’assistance.

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

### <a name="example-relating-anchor-coordinate-systems-to-stationary-reference-frame-coordinate-systems"></a>Exemple : Association de systèmes de coordonnées d’ancrage à des systèmes de coordonnées de cadre de référence stationnaire

Supposons que vous disposiez d’une ancre et que vous vouliez associer un nom du système de coordonnées de votre ancre à l’SpatialStationaryReferenceFrame que vous utilisez déjà pour la plupart de votre autre contenu. Vous pouvez utiliser [TryGetTransformTo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.trygettransformto.aspx) pour obtenir une transformation du système de coordonnées de l’ancre à celle du cadre de référence fixe :

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

Ce processus est utile de deux manières :
1. Elle vous indique si les deux frames de référence peuvent être compris entre eux, et ;
2. Si c’est le cas, il vous fournit une transformation pour passer directement d’un système de coordonnées à l’autre.

Avec ces informations, vous comprenez la relation spatiale entre les objets entre les deux frames de référence.

Pour le rendu, vous pouvez souvent obtenir de meilleurs résultats en regroupant des objets en fonction de leur frame de référence ou de leur ancre d’origine. Effectuez une passe de dessin distincte pour chaque groupe. Les matrices de vue sont plus précises pour les objets avec des transformations de modèle créées initialement à l’aide du même système de coordonnées.

## <a name="create-holograms-using-a-device-attached-frame-of-reference"></a>Créer des hologrammes à l’aide d’une image de référence associée à un appareil

Il peut arriver que vous souhaitiez afficher un hologramme qui [reste attaché](coordinate-systems.md#attached-frame-of-reference) à l’emplacement de l’appareil, par exemple un panneau avec des informations de débogage ou un message d’information lorsque l’appareil est uniquement en mesure de déterminer son orientation et non sa position dans espace. Pour ce faire, nous utilisons un cadre de référence attaché.

La classe SpatialLocatorAttachedFrameOfReference définit des systèmes de coordonnées relatifs à l’appareil plutôt qu’au monde réel. Ce cadre a un titre fixe par rapport à l’environnement de l’utilisateur qui pointe dans la direction vers laquelle l’utilisateur était confronté lorsque le frame de référence a été créé. À partir de là, toutes les orientations dans ce frame de référence sont relatives à cet en-tête fixe, même lorsque l’utilisateur fait pivoter l’appareil.

Pour HoloLens, l’origine du système de coordonnées de ce frame se trouve au centre de rotation de la tête de l’utilisateur, de sorte que sa position n’est pas affectée par la rotation de la tête. Votre application peut spécifier un décalage par rapport à ce point pour positionner les hologrammes devant l’utilisateur.

Pour obtenir un SpatialLocatorAttachedFrameOfReference, utilisez la classe SpatialLocator et appelez CreateAttachedFrameOfReferenceAtCurrentHeading.

Notez que cela s’applique à toute la plage d’appareils Windows Mixed Reality.

### <a name="use-a-reference-frame-attached-to-the-device"></a>Utiliser un cadre de référence attaché à l’appareil

Ces sections décrivent ce que nous avons modifié dans le modèle d’application holographique Windows pour activer un cadre de référence associé à un appareil à l’aide de cette API. Notez que cet hologramme « attaché » fonctionne avec les hologrammes fixes ou ancrés, et peut également être utilisé lorsque l’appareil est momentanément incapable de trouver sa position dans le monde.

Tout d’abord, nous avons modifié le modèle pour stocker un SpatialLocatorAttachedFrameOfReference au lieu d’un SpatialStationaryFrameOfReference :

À partir de **HolographicTagAlongSampleMain. h**:

```
   // A reference frame attached to the holographic camera.
   Windows::Perception::Spatial::SpatialLocatorAttachedFrameOfReference^   m_referenceFrame;
```

À partir de **HolographicTagAlongSampleMain. cpp**:

```
   // In this example, we create a reference frame attached to the device.
   m_referenceFrame = m_locator->CreateAttachedFrameOfReferenceAtCurrentHeading();
```

Au cours de la mise à jour, nous obtenons désormais le système de coordonnées à l’horodatage obtenu à l’aide de la prédiction de cadre.

```
   // Next, we get a coordinate system from the attached frame of reference that is
   // associated with the current frame. Later, this coordinate system is used for
   // for creating the stereo view matrices when rendering the sample content.
   SpatialCoordinateSystem^ currentCoordinateSystem =
       m_referenceFrame->GetStationaryCoordinateSystemAtTimestamp(prediction->Timestamp);
```

### <a name="get-a-spatial-pointer-pose-and-follow-the-users-gaze"></a>Obtenir une pose de pointeur spatial et suivre le point de regard de l’utilisateur

Nous souhaitons que notre exemple d’hologramme suive le [regard](gaze-and-commit.md)de l’utilisateur, de la même façon que le shell holographique peut suivre le regard de l’utilisateur. Pour cela, nous devons obtenir le SpatialPointerPose à partir du même horodatage.

```
SpatialPointerPose^ pose = SpatialPointerPose::TryGetAtTimestamp(currentCoordinateSystem, prediction->Timestamp);
```

Ce SpatialPointerPose contient les informations nécessaires pour positionner l’hologramme en fonction de l' [en-tête actuel de l’utilisateur](gaze-in-directx.md).

Pour des raisons de confort de l’utilisateur, nous utilisons l’interpolation linéaire (« Lerp ») pour lisser la modification de position de sorte qu’elle se produise sur une période donnée. L’utilisateur est plus à l’aise avec le verrouillage de l’hologramme. Lerping la position de la balise, le long de l’hologramme, nous permet également de stabiliser l’hologramme en amortissant le mouvement. Si ce n’est pas le cas, l’utilisateur voit l’instabilité de l’hologramme en raison de ce qui est normalement considéré comme des mouvements imperceptibles de la tête de l’utilisateur.

À partir de **StationaryQuadRenderer ::P ositionhologram**:

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
>Dans le cas d’un panneau de débogage, vous pouvez choisir de repositionner l’hologramme sur le côté afin qu’il n’obstrue pas votre vue. Voici un exemple de ce que vous pouvez faire.

Pour **StationaryQuadRenderer ::P ositionhologram**:

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

Il n’est pas suffisant de positionner simplement l’hologramme, qui dans ce cas est un quadruple. Nous devons également faire pivoter l’objet pour faire face à l’utilisateur. Notez que cette rotation se produit dans l’espace universel, car ce type de billboarding permet à l’hologramme de conserver une partie de l’environnement de l’utilisateur. L’affichage de l’espacement d’affichage n’est pas aussi agréable, car l’hologramme est verrouillé à l’orientation d’affichage. dans ce cas, vous devez également interpoler entre les matrices de vue de gauche et de droite afin d’acquérir une transformation d’affichage de l’espace d’affichage qui n’interrompt pas le rendu stéréo. Ici, nous allons faire pivoter sur les axes X et Z pour faire face à l’utilisateur.

À partir de **StationaryQuadRenderer :: Update**:

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

### <a name="render-the-attached-hologram"></a>Rendre l’hologramme attaché

Pour cet exemple, nous choisissons également d’afficher l’hologramme dans le système de coordonnées du SpatialLocatorAttachedReferenceFrame, où nous avons positionné l’hologramme. (Si nous avions décidé d’effectuer le rendu à l’aide d’un autre système de coordonnées, nous aurions besoin d’acquérir une transformation du système de coordonnées de l’appareil de référence associé à l’appareil vers ce système de coordonnées.)

À partir de **HolographicTagAlongSampleMain :: Render**:

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

C’est tout ! L’hologramme va à présent « débusquer » une position qui est de 2 mètres devant la direction du regard de l’utilisateur.

>[!NOTE]
>Cet exemple charge également du contenu supplémentaire. consultez StationaryQuadRenderer. cpp.

## <a name="handling-tracking-loss"></a>Gestion des pertes de suivi

Lorsque l’appareil ne peut pas se trouver dans le monde entier, l’application rencontre une « perte de suivi ». Les applications Windows Mixed Reality doivent être en mesure de gérer ces interruptions du système de suivi positionnel. Ces interruptions peuvent être observées et les réponses créées à l’aide de l’événement LocatabilityChanged sur le SpatialLocator par défaut.

À partir de **AppMain :: SetHolographicSpace :**

```
   // Be able to respond to changes in the positional tracking state.
   m_locatabilityChangedToken =
       m_locator->LocatabilityChanged +=
           ref new Windows::Foundation::TypedEventHandler<SpatialLocator^, Object^>(
               std::bind(&HolographicApp1Main::OnLocatabilityChanged, this, _1, _2)
               );
```

Lorsque votre application reçoit un événement LocatabilityChanged, elle peut modifier le comportement en fonction des besoins. Par exemple, dans l’État PositionalTrackingInhibited, votre application peut suspendre une opération normale et afficher un message d’avertissement [sur l’hologramme](coordinate-systems-in-directx.md#create-holograms-using-a-device-attached-frame-of-reference) qui affiche un message d’avertissement.

Le modèle d’application holographique Windows est fourni avec un gestionnaire LocatabilityChanged déjà créé pour vous. Par défaut, il affiche un avertissement dans la console de débogage lorsque le suivi positionnel n’est pas disponible. Vous pouvez ajouter du code à ce gestionnaire pour fournir une réponse en fonction des besoins de votre application.

À partir de **AppMain. cpp :**

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

Les API de [mappage spatial](spatial-mapping-in-directx.md) utilisent des systèmes de coordonnées pour obtenir des transformations de modèle pour les maillages de surface.

## <a name="see-also"></a>Articles associés
* [Systèmes de coordonnées](coordinate-systems.md)
* [Ancres spatiales](spatial-anchors.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>
* [Suivre de la tête et du regard dans DirectX](gaze-in-directx.md)
* [Mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md)
* [Mappage spatial dans DirectX](spatial-mapping-in-directx.md)
