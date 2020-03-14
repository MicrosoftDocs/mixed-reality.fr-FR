---
title: Mappage spatial dans DirectX
description: Explique comment implémenter le mappage spatial dans votre application DirectX. Cela inclut une explication détaillée de l’exemple d’application de mappage spatial qui est inclus avec le kit de développement logiciel (SDK) plateforme Windows universelle.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, mappage spatial, environnement, interaction, DirectX, WinRT, API, exemple de code, UWP, SDK, procédure pas à pas
ms.openlocfilehash: 456fcf1c00e23a287a741673e94b3f8d2d2d346c
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79375816"
---
# <a name="spatial-mapping-in-directx"></a>Mappage spatial dans DirectX

Cette rubrique explique comment implémenter le [mappage spatial](spatial-mapping.md) dans votre application DirectX. Cela inclut une explication détaillée de l’exemple d’application de mappage spatial qui est inclus avec le kit de développement logiciel (SDK) plateforme Windows universelle.

Cette rubrique utilise le code de l’exemple de code UWP [HolographicSpatialMapping](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) .

>[!NOTE]
>Les extraits de code de cet article illustrent actuellement l' C++utilisation de/CX plutôt que de C++/WinRT conforme C + +17, comme utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).  Les concepts sont équivalents pour C++un projet/WinRT, bien que vous deviez traduire le code.

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Mappage spatial</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

## <a name="directx-development-overview"></a>Vue d’ensemble du développement DirectX

Le développement d’applications natives pour le mappage spatial utilise les API sous l’espace de noms [Windows. perception. spatial](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.aspx) . Ces API offrent un contrôle total de la fonctionnalité de mappage spatial, de manière directement analogue aux API de mappage spatial exposées par [Unity](spatial-mapping-in-unity.md).

### <a name="perception-apis"></a>API perception

Les types principaux fournis pour le développement de mappages spatiaux sont les suivants :
* [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) fournit des informations sur les surfaces dans les régions d’espace spécifiées à l’application près de l’utilisateur, sous la forme d’objets SpatialSurfaceInfo.
* [SpatialSurfaceInfo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.aspx) décrit une seule surface spatiale, y compris un ID unique, le volume de limite et l’heure de la dernière modification. Il fournira un SpatialSurfaceMesh de façon asynchrone sur demande.
* [SpatialSurfaceMeshOptions](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemeshoptions.aspx) contient les paramètres utilisés pour personnaliser les objets SpatialSurfaceMesh demandés à partir de SpatialSurfaceInfo.
* [SpatialSurfaceMesh](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.aspx) représente les données de maillage pour une surface spatiale unique. Les données pour les positions de vertex, les normales de vertex et les index de triangle sont contenues dans les objets SpatialSurfaceMeshBuffer membres.
* [SpatialSurfaceMeshBuffer](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemeshbuffer.aspx) encapsule un seul type de données de maillage.

Lors du développement d’une application à l’aide de ces API, le déroulement de votre programme de base ressemblera à ce qui suit (comme illustré dans l’exemple d’application décrit ci-dessous) :
- **Configurer votre SpatialSurfaceObserver**
  - Appelez [RequestAccessAsync](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.requestaccessasync.aspx)pour vous assurer que l’utilisateur a l’autorisation nécessaire pour que votre application utilise les fonctionnalités de mappage spatiale de l’appareil.
  - Instanciez un objet SpatialSurfaceObserver.
  - Appelez [SetBoundingVolumes](https://msdn.microsoft.com/library/windows/apps/mt592747.aspx) pour spécifier les régions d’espace dans lesquelles vous souhaitez obtenir des informations sur les surfaces spatiales. Vous pouvez modifier ces régions à l’avenir en appelant à nouveau cette fonction. Chaque région est spécifiée à l’aide d’un [SpatialBoundingVolume](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialboundingvolume.aspx).
  - Inscrivez-vous à l’événement [ObservedSurfacesChanged](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.observedsurfaceschanged.aspx) , qui se déclenche chaque fois que de nouvelles informations sont disponibles sur les surfaces spatiales dans les régions d’espace que vous avez spécifiées.
- **Traiter les événements ObservedSurfacesChanged**
  - Dans votre gestionnaire d’événements, appelez [GetObservedSurfaces](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.getobservedsurfaces.aspx) pour recevoir un mappage d’objets SpatialSurfaceInfo. À l’aide de cette carte, vous pouvez mettre à jour vos enregistrements dont les surfaces spatiales [existent dans l’environnement de l’utilisateur](spatial-mapping.md#mesh-caching).
  - Pour chaque objet SpatialSurfaceInfo, vous pouvez interroger [TryGetBounds](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.trygetbounds.aspx) pour déterminer les étendues spatiales de la surface, exprimées dans un [système de coordonnées spatiales](coordinate-systems.md) de votre choix.
  - Si vous décidez de demander un maillage pour une surface spatiale, appelez [TryComputeLatestMeshAsync](https://msdn.microsoft.com/library/windows/apps/mt592715.aspx). Vous pouvez fournir des options spécifiant la densité souhaitée des triangles et le format des données de maillage retournées.
- **Recevoir et traiter le maillage**
  - Chaque appel à TryComputeLatestMeshAsync va aysnchronously retourner un objet SpatialSurfaceMesh.
  - À partir de cet objet, vous pouvez accéder aux objets SpatialSurfaceMeshBuffer contenus pour accéder aux index de triangle, aux positions de vertex et (le cas échéant) aux normales des sommets de la maille. Ces données seront dans un format directement compatible avec les [API Direct3D 11](https://msdn.microsoft.com/library/windows/desktop/ff476501(v=vs.85).aspx) utilisées pour le rendu des maillages.
  - À partir de là, votre application peut éventuellement effectuer l’analyse ou le [traitement](spatial-mapping.md#mesh-processing) des données de maillage, et les utiliser pour le [rendu](spatial-mapping.md#rendering) et la [Raycasting physique et les collisions](spatial-mapping.md#raycasting-and-collision).
  - Un détail important à noter est que vous devez appliquer une mise à l’échelle aux positions de vertex de maillage (par exemple, dans le nuanceur de sommets utilisé pour le rendu des maillages), pour les convertir des unités entières optimisées dans lesquelles elles sont stockées dans la mémoire tampon, en mètres. Vous pouvez récupérer cette échelle en appelant [VertexPositionScale](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.vertexpositionscale.aspx).

### <a name="troubleshooting"></a>Résolution des problèmes
* N’oubliez pas de mettre à l’échelle les positions de vertex de maillage dans votre nuanceur de sommets, à l’aide de l’échelle retournée par [SpatialSurfaceMesh. VertexPositionScale](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.vertexpositionscale.aspx)

## <a name="spatial-mapping-code-sample-walkthrough"></a>Exemple de code de mappage spatial

L’exemple de code de [mappage spatial holographique](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) inclut du code que vous pouvez utiliser pour commencer à charger des maillages superficiels dans votre application, y compris l’infrastructure de gestion et de rendu des maillages d’aire.

À présent, nous allons vous montrer comment ajouter la fonctionnalité de mappage de surface à votre application DirectX. Vous pouvez ajouter ce code à votre projet de [modèle d’application holographique Windows](creating-a-holographic-directx-project.md) , ou vous pouvez suivre la procédure en parcourant l’exemple de code mentionné ci-dessus. Cet exemple de code est basé sur le modèle d’application holographique Windows.

### <a name="set-up-your-app-to-use-the-spatialperception-capability"></a>Configurer votre application pour utiliser la fonctionnalité spatialPerception

Votre application doit être en mesure d’utiliser la fonctionnalité de mappage spatial. Cela est nécessaire, car le maillage spatial est une représentation de l’environnement de l’utilisateur, qui peut être considérée comme des données privées. Déclarez cette fonctionnalité dans le fichier Package. appxmanifest pour votre application. Voici un exemple :

```xml
<Capabilities>
  <uap2:Capability Name="spatialPerception" />
</Capabilities>
```

La fonctionnalité provient de l’espace de noms **UAP2** . Pour accéder à cet espace de noms dans votre manifeste, incluez-le en tant qu’attribut *xlmns* dans l’élément &lt;> Package. Voici un exemple :

```xml
<Package
    xmlns="https://schemas.microsoft.com/appx/manifest/foundation/windows10"
    xmlns:mp="https://schemas.microsoft.com/appx/2014/phone/manifest"
    xmlns:uap="https://schemas.microsoft.com/appx/manifest/uap/windows10"
    xmlns:uap2="https://schemas.microsoft.com/appx/manifest/uap/windows10/2"
    IgnorableNamespaces="uap uap2 mp"
    >
```

### <a name="check-for-spatial-mapping-feature-support"></a>Vérifier la prise en charge de la fonctionnalité de mappage spatial

Windows Mixed Reality prend en charge un large éventail d’appareils, notamment les appareils qui ne prennent pas en charge le mappage spatial. Si votre application peut utiliser le mappage spatial, ou si elle doit utiliser le mappage spatial, pour fournir des fonctionnalités, elle doit s’assurer que le mappage spatial est pris en charge avant d’essayer de l’utiliser. Par exemple, si le mappage spatial est requis par votre application de réalité mixte, elle doit afficher un message à cet effet si un utilisateur tente de l’exécuter sur un appareil sans mappage spatial. Ou bien, votre application peut être en mesure d’effectuer le rendu de son propre environnement virtuel à la place de l’environnement de l’utilisateur, en fournissant une expérience similaire à ce qui se passerait si le mappage spatial était disponible. Dans tous les cas, cette API permet à votre application de savoir quand elle n’obtiendra pas de données de mappage spatiales et de répondre de manière appropriée.

Pour vérifier la prise en charge du mappage spatial sur l’appareil actuel, assurez-vous d’abord que le contrat UWP est au niveau 4 ou supérieur, puis appelez SpatialSurfaceObserver :: IsSupported (). Voici comment procéder dans le contexte de l’exemple de code de [mappage spatial holographique](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) . La prise en charge est vérifiée juste avant de demander l’accès.

L’API SpatialSurfaceObserver :: IsSupported () est disponible à partir de la version 15063 du kit de développement logiciel (SDK). Si nécessaire, reciblez votre projet vers la version 15063 de la plateforme avant d’utiliser cette API.

```cpp
if (m_surfaceObserver == nullptr)
   {
       using namespace Windows::Foundation::Metadata;
       if (ApiInformation::IsApiContractPresent(L"Windows.Foundation.UniversalApiContract", 4))
       {
           if (!SpatialSurfaceObserver::IsSupported())
           {
               // The current system does not have spatial mapping capability.
               // Turn off spatial mapping.
               m_spatialPerceptionAccessRequested = true;
               m_surfaceAccessAllowed = false;
           }
       }

       if (!m_spatialPerceptionAccessRequested)
       {
           /// etc ...
```

Notez que lorsque le contrat UWP est inférieur au niveau 4, l’application doit s’exécuter comme si l’appareil est capable d’effectuer un mappage spatial.

### <a name="request-access-to-spatial-mapping-data"></a>Demander l’accès aux données de mappage spatiale

Votre application doit demander l’autorisation d’accéder aux données de mappage spatiale avant d’essayer de créer des observateurs de surface. Voici un exemple basé sur notre exemple de code de mappage de surface, avec plus de détails fournis plus loin dans cette page :

```cpp
auto initSurfaceObserverTask = create_task(SpatialSurfaceObserver::RequestAccessAsync());
initSurfaceObserverTask.then([this, coordinateSystem](Windows::Perception::Spatial::SpatialPerceptionAccessStatus status)
{
    if (status == SpatialPerceptionAccessStatus::Allowed)
    {
        // Create a surface observer.
    }
    else
    {
        // Handle spatial mapping unavailable.
    }
}
```

### <a name="create-a-surface-observer"></a>Créer un observateur de surface

L’espace de noms **Windows ::P erception :: spatial :: surfaces** comprend la classe [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) , qui observe un ou plusieurs volumes que vous spécifiez dans un [SpatialCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.aspx). Utilisez une instance [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) pour accéder aux données de maillage des surfaces en temps réel.

À partir de **AppMain. h**:

```cpp
// Obtains surface mapping data from the device in real time.
Windows::Perception::Spatial::Surfaces::SpatialSurfaceObserver^     m_surfaceObserver;
Windows::Perception::Spatial::Surfaces::SpatialSurfaceMeshOptions^  m_surfaceMeshOptions;
```

Comme indiqué dans la section précédente, vous devez demander l’accès aux données de mappage spatiale pour que votre application puisse l’utiliser. Cet accès est accordé automatiquement sur HoloLens.

```cpp
// The surface mapping API reads information about the user's environment. The user must
// grant permission to the app to use this capability of the Windows Mixed Reality device.
auto initSurfaceObserverTask = create_task(SpatialSurfaceObserver::RequestAccessAsync());
initSurfaceObserverTask.then([this, coordinateSystem](Windows::Perception::Spatial::SpatialPerceptionAccessStatus status)
{
    if (status == SpatialPerceptionAccessStatus::Allowed)
    {
        // If status is allowed, we can create the surface observer.
        m_surfaceObserver = ref new SpatialSurfaceObserver();
```

Ensuite, vous devez configurer l’observateur de surface pour observer un volume de limite spécifique. Ici, nous observons une boîte qui est 20x20x5 mètres, centrée sur l’origine du système de coordonnées.

```cpp
// The surface observer can now be configured as needed.

        // In this example, we specify one area to be observed using an axis-aligned
        // bounding box 20 meters in width and 5 meters in height and centered at the
        // origin.
        SpatialBoundingBox aabb =
        {
            { 0.f,  0.f, 0.f },
            {20.f, 20.f, 5.f },
        };

        SpatialBoundingVolume^ bounds = SpatialBoundingVolume::FromBox(coordinateSystem, aabb);
        m_surfaceObserver->SetBoundingVolume(bounds);
```

Notez que vous pouvez définir plusieurs volumes englobants à la place.

*Il s’agit du pseudo-code :*

```cpp
m_surfaceObserver->SetBoundingVolumes(/* iterable collection of bounding volumes*/);
```

Il est également possible d’utiliser d’autres formes englobantes, telles qu’une vue frustum, ou un rectangle englobant qui n’est pas aligné sur l’axe.

*Il s’agit du pseudo-code :*

```cpp
m_surfaceObserver->SetBoundingVolume(
            SpatialBoundingVolume::FromFrustum(/*SpatialCoordinateSystem*/, /*SpatialBoundingFrustum*/)
            );
```

Si votre application doit effectuer une opération différente quand les données de mappage des surfaces ne sont pas disponibles, vous pouvez écrire du code pour répondre au cas où le [SpatialPerceptionAccessStatus](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialperceptionaccessstatus.aspx) n’est pas **autorisé** . par exemple, il ne sera pas autorisé sur les PC avec des appareils immersifs connectés, car ces appareils n’ont pas de matériel pour le mappage spatial. Pour ces appareils, vous devez plutôt compter sur la phase spatiale pour obtenir des informations sur l’environnement et la configuration de l’appareil de l’utilisateur.

### <a name="initialize-and-update-the-surface-mesh-collection"></a>Initialiser et mettre à jour la collection de maillages d’aire

Si l’observateur de surface a été créé avec succès, nous pouvons commencer à initialiser notre collection de maillages de surface. Ici, nous utilisons l’API du modèle pull pour obtenir immédiatement l’ensemble actuel des surfaces observées :

```cpp
auto mapContainingSurfaceCollection = m_surfaceObserver->GetObservedSurfaces();
        for (auto& pair : mapContainingSurfaceCollection)
        {
            // Store the ID and metadata for each surface.
            auto const& id = pair->Key;
            auto const& surfaceInfo = pair->Value;
            m_meshCollection->AddOrUpdateSurface(id, surfaceInfo);
        }
```

Un modèle d’émission est également disponible pour obtenir des données de maillage de surface. Vous êtes libre de concevoir votre application pour qu’elle utilise uniquement le modèle d’extraction si vous le souhaitez, auquel cas vous interrogez les données chaque fois, par exemple, une fois par cadre, ou pendant une période spécifique, par exemple lors de la configuration du jeu. Si c’est le cas, le code ci-dessus est ce dont vous avez besoin.

Dans notre exemple de code, nous avons choisi d’illustrer l’utilisation des deux modèles à des fins pédagogiques. Ici, nous nous abonnons à un événement pour recevoir des données de maillage de surface à jour chaque fois que le système reconnaît une modification.

```cpp
m_surfaceObserver->ObservedSurfacesChanged += ref new TypedEventHandler<SpatialSurfaceObserver^, Platform::Object^>(
            bind(&HolographicDesktopAppMain::OnSurfacesChanged, this, _1, _2)
            );
```

Notre exemple de code est également configuré pour répondre à ces événements. Passons en revue la procédure à suivre.

**Remarque :** Cela peut ne pas être le moyen le plus efficace pour votre application de gérer les données de maillage. Ce code est écrit par souci de clarté et n’est pas optimisé.

Les données de maillage des surfaces sont fournies dans un mappage en lecture seule qui stocke les objets [SpatialSurfaceInfo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.aspx) en utilisant [Platform :: GUID](https://msdn.microsoft.com/library/windows/desktop/aa373931.aspx) comme valeurs de clés.

```cpp
IMapView<Guid, SpatialSurfaceInfo^>^ const& surfaceCollection = sender->GetObservedSurfaces();
```

Pour traiter ces données, nous examinons d’abord les valeurs de clés qui ne se trouvent pas dans notre collection. Des informations détaillées sur la façon dont les données sont stockées dans notre exemple d’application seront présentées plus loin dans cette rubrique.

```cpp
// Process surface adds and updates.
for (const auto& pair : surfaceCollection)
{
    auto id = pair->Key;
    auto surfaceInfo = pair->Value;

    if (m_meshCollection->HasSurface(id))
    {
        // Update existing surface.
        m_meshCollection->AddOrUpdateSurface(id, surfaceInfo);
    }
    else
    {
        // New surface.
        m_meshCollection->AddOrUpdateSurface(id, surfaceInfo);
    }
}
```

Nous devons également supprimer les maillages des surfaces qui se trouvent dans notre collection de maillages de surface, mais qui ne se trouvent plus dans la collection système. Pour ce faire, nous devons effectuer une opération similaire à l’inverse de ce que nous venons de montrer pour ajouter et mettre à jour des mailles. Nous effectuons une boucle sur la collection de votre application et vérifions si le **GUID** est présent dans la collection système. Si elle ne se trouve pas dans le regroupement système, nous la supprimons de la nôtre.

À partir de notre gestionnaire d’événements dans AppMain. cpp :

```cpp
m_meshCollection->PruneMeshCollection(surfaceCollection);
```

Implémentation du nettoyage de maillage dans RealtimeSurfaceMeshRenderer. cpp :

```cpp
void RealtimeSurfaceMeshRenderer::PruneMeshCollection(IMapView<Guid, SpatialSurfaceInfo^>^ const& surfaceCollection)
{
    std::lock_guard<std::mutex> guard(m_meshCollectionLock);
    std::vector<Guid> idsToRemove;

    // Remove surfaces that moved out of the culling frustum or no longer exist.
    for (const auto& pair : m_meshCollection)
    {
        const auto& id = pair.first;
        if (!surfaceCollection->HasKey(id))
        {
            idsToRemove.push_back(id);
        }
    }

    for (const auto& id : idsToRemove)
    {
        m_meshCollection.erase(id);
    }
}
```

### <a name="acquire-and-use-surface-mesh-data-buffers"></a>Acquérir et utiliser des tampons de données de maillage des surfaces

L’obtention des informations de maillage des surfaces était aussi simple que l’extraction d’une collection de données et le traitement des mises à jour de cette collection. Maintenant, nous aborderons en détail la façon dont vous pouvez utiliser les données.

Dans notre exemple de code, nous avons choisi d’utiliser les maillages des surfaces pour le rendu. Il s’agit d’un scénario courant pour boucher des hologrammes derrière des surfaces réelles. Vous pouvez également effectuer le rendu des panneaux ou afficher les versions traitées de ceux-ci pour montrer à l’utilisateur quelles zones de la salle sont analysées avant de commencer à fournir des fonctionnalités d’application ou de jeu.

L’exemple de code démarre le processus lorsqu’il reçoit des mises à jour de la maille des surfaces du gestionnaire d’événements que nous avons décrit dans la section précédente. La ligne de code importante dans cette fonction est l’appel permettant de mettre à jour le *maillage*des surfaces : à ce stade, nous avons déjà traité les informations de maillage, et nous sommes sur le point d’obtenir les données de vertex et d’index pour une utilisation comme nous le voyons.

À partir de RealtimeSurfaceMeshRenderer. cpp :

```cpp
void RealtimeSurfaceMeshRenderer::AddOrUpdateSurface(Guid id, SpatialSurfaceInfo^ newSurface)
{
    auto options = ref new SpatialSurfaceMeshOptions();
    options->IncludeVertexNormals = true;

    auto createMeshTask = create_task(newSurface->TryComputeLatestMeshAsync(1000, options));
    createMeshTask.then([this, id](SpatialSurfaceMesh^ mesh)
    {
        if (mesh != nullptr)
        {
            std::lock_guard<std::mutex> guard(m_meshCollectionLock);
            '''m_meshCollection[id].UpdateSurface(mesh);'''
        }
    }, task_continuation_context::use_current());
}
```

Notre exemple de code est conçu de sorte qu’une classe de données, **SurfaceMesh**, gère le traitement et le rendu des données de maillage. Il s’agit de ce que le **RealtimeSurfaceMeshRenderer** conserve en fait une carte. Chacune d’elles a une référence à l’SpatialSurfaceMesh d’origine, et nous l’utilisons tout le temps nécessaire pour accéder au vertex de maillage ou aux tampons d’index, ou obtenir une transformation pour la maille. Pour le moment, nous signalons le maillage comme nécessitant une mise à jour.

À partir de SurfaceMesh. cpp :

```cpp
void SurfaceMesh::UpdateSurface(SpatialSurfaceMesh^ surfaceMesh)
{
    m_surfaceMesh = surfaceMesh;
    m_updateNeeded = true;
}
```

La prochaine fois que la maille sera invitée à se dessiner lui-même, elle vérifiera d’abord l’indicateur. Si une mise à jour est nécessaire, les mémoires tampons de vertex et d’index seront mises à jour sur le GPU.

```cpp
void SurfaceMesh::CreateDeviceDependentResources(ID3D11Device* device)
{
    m_indexCount = m_surfaceMesh->TriangleIndices->ElementCount;
    if (m_indexCount < 3)
    {
        // Not enough indices to draw a triangle.
        return;
    }
```

Tout d’abord, nous acquérant les tampons de données brutes :

```cpp
Windows::Storage::Streams::IBuffer^ positions = m_surfaceMesh->VertexPositions->Data;
    Windows::Storage::Streams::IBuffer^ normals   = m_surfaceMesh->VertexNormals->Data;
    Windows::Storage::Streams::IBuffer^ indices   = m_surfaceMesh->TriangleIndices->Data;
```

Ensuite, nous créons des tampons de périphérique Direct3D avec les données de maillage fournies par le HoloLens :

```cpp
CreateDirectXBuffer(device, D3D11_BIND_VERTEX_BUFFER, positions, m_vertexPositions.GetAddressOf());
    CreateDirectXBuffer(device, D3D11_BIND_VERTEX_BUFFER, normals,   m_vertexNormals.GetAddressOf());
    CreateDirectXBuffer(device, D3D11_BIND_INDEX_BUFFER,  indices,   m_triangleIndices.GetAddressOf());

    // Create a constant buffer to control mesh position.
    CD3D11_BUFFER_DESC constantBufferDesc(sizeof(SurfaceTransforms), D3D11_BIND_CONSTANT_BUFFER);
    DX::ThrowIfFailed(
        device->CreateBuffer(
            &constantBufferDesc,
            nullptr,
            &m_modelTransformBuffer
            )
        );

    m_loadingComplete = true;
}
```

**Remarque :** Pour la fonction d’assistance CreateDirectXBuffer utilisée dans l’extrait de code précédent, consultez l’exemple de code de mappage des surfaces : SurfaceMesh. cpp, GetDataFromIBuffer. h. À présent, la création de la ressource d’appareil est terminée et le maillage est considéré comme étant chargé et prêt pour la mise à jour et le rendu.

### <a name="update-and-render-surface-meshes"></a>Maillages des surfaces de mise à jour et de rendu

Notre classe SurfaceMesh possède une fonction de mise à jour spécialisée. Chaque [SpatialSurfaceMesh](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.aspx) possède sa propre transformation, et notre exemple utilise le système de coordonnées actuel pour notre **SpatialStationaryReferenceFrame** pour acquérir la transformation. Ensuite, il met à jour le tampon de constante de modèle sur le GPU.

```cpp
void SurfaceMesh::UpdateTransform(
    ID3D11DeviceContext* context,
    SpatialCoordinateSystem^ baseCoordinateSystem
    )
{
    if (m_indexCount < 3)
    {
        // Not enough indices to draw a triangle.
        return;
    }

    XMMATRIX transform = XMMatrixIdentity();

    auto tryTransform = m_surfaceMesh->CoordinateSystem->TryGetTransformTo(baseCoordinateSystem);
    if (tryTransform != nullptr)
    {
        transform = XMLoadFloat4x4(&tryTransform->Value);
    }

    XMMATRIX scaleTransform = XMMatrixScalingFromVector(XMLoadFloat3(&m_surfaceMesh->VertexPositionScale));

    XMStoreFloat4x4(
        &m_constantBufferData.vertexWorldTransform,
        XMMatrixTranspose(
            scaleTransform * transform
            )
        );

    // Normals don't need to be translated.
    XMMATRIX normalTransform = transform;
    normalTransform.r[3] = XMVectorSet(0.f, 0.f, 0.f, XMVectorGetW(normalTransform.r[3]));
    XMStoreFloat4x4(
        &m_constantBufferData.normalWorldTransform,
        XMMatrixTranspose(
            normalTransform
        )
        );

    if (!m_loadingComplete)
    {
        return;
    }

    context->UpdateSubresource(
        m_modelTransformBuffer.Get(),
        0,
        NULL,
        &m_constantBufferData,
        0,
        0
        );
}
```

Lorsqu’il est temps de restituer des maillages d’aire, nous procédons à un travail de préparation avant de restituer la collection. Nous avons configuré le pipeline du nuanceur pour la configuration de rendu actuelle et nous avons configuré l’étape assembleur d’entrée. Notez que la classe d’assistance d’appareil photo holographique **CameraResources. cpp** a déjà configuré la mémoire tampon de la vue/projection à présent.

À partir de **RealtimeSurfaceMeshRenderer :: Render**:

```cpp
auto context = m_deviceResources->GetD3DDeviceContext();

context->IASetPrimitiveTopology(D3D11_PRIMITIVE_TOPOLOGY_TRIANGLELIST);
context->IASetInputLayout(m_inputLayout.Get());

// Attach our vertex shader.
context->VSSetShader(
    m_vertexShader.Get(),
    nullptr,
    0
    );

// The constant buffer is per-mesh, and will be set as such.

if (depthOnly)
{
    // Explicitly detach the later shader stages.
    context->GSSetShader(nullptr, nullptr, 0);
    context->PSSetShader(nullptr, nullptr, 0);
}
else
{
    if (!m_usingVprtShaders)
    {
        // Attach the passthrough geometry shader.
        context->GSSetShader(
            m_geometryShader.Get(),
            nullptr,
            0
            );
    }

    // Attach our pixel shader.
    context->PSSetShader(
        m_pixelShader.Get(),
        nullptr,
        0
        );
}
```

Une fois cette opération effectuée, nous effectuons une boucle sur nos mailles et indiquons à chacun de se dessiner lui-même. **Remarque :** Cet exemple de code n’est pas optimisé pour utiliser n’importe quel type d’élimination de frustum, mais vous devez inclure cette fonctionnalité dans votre application.

```cpp
std::lock_guard<std::mutex> guard(m_meshCollectionLock);

auto device = m_deviceResources->GetD3DDevice();

// Draw the meshes.
for (auto& pair : m_meshCollection)
{
    auto& id = pair.first;
    auto& surfaceMesh = pair.second;

    surfaceMesh.Draw(device, context, m_usingVprtShaders, isStereo);
}
```

Les maillages individuels sont responsables de la configuration des tampons de mémoire tampon de vertex et d’index, de Stride et de la transformation de modèle. Comme pour le cube en rotation dans le modèle d’application holographique Windows, nous rendons les tampons stéréoscopiques à l’aide de l’instanciation.

À partir de **SurfaceMesh ::D RAW**:

```cpp
// The vertices are provided in {vertex, normal} format

const auto& vertexStride = m_surfaceMesh->VertexPositions->Stride;
const auto& normalStride = m_surfaceMesh->VertexNormals->Stride;

UINT strides [] = { vertexStride, normalStride };
UINT offsets [] = { 0, 0 };
ID3D11Buffer* buffers [] = { m_vertexPositions.Get(), m_vertexNormals.Get() };

context->IASetVertexBuffers(
    0,
    ARRAYSIZE(buffers),
    buffers,
    strides,
    offsets
    );

const auto& indexFormat = static_cast<DXGI_FORMAT>(m_surfaceMesh->TriangleIndices->Format);

context->IASetIndexBuffer(
    m_triangleIndices.Get(),
    indexFormat,
    0
    );

context->VSSetConstantBuffers(
    0,
    1,
    m_modelTransformBuffer.GetAddressOf()
    );

if (!usingVprtShaders)
{
    context->GSSetConstantBuffers(
        0,
        1,
        m_modelTransformBuffer.GetAddressOf()
        );
}

context->PSSetConstantBuffers(
    0,
    1,
    m_modelTransformBuffer.GetAddressOf()
    );

context->DrawIndexedInstanced(
    m_indexCount,       // Index count per instance.
    isStereo ? 2 : 1,   // Instance count.
    0,                  // Start index location.
    0,                  // Base vertex location.
    0                   // Start instance location.
    );
```

### <a name="rendering-choices-with-surface-mapping"></a>Choix du rendu avec le mappage des surfaces

L’exemple de code de mappage des surfaces offre du code pour le rendu d’occlusion uniquement des données de maillage des surfaces et pour le rendu à l’écran des données de maillage des surfaces. Le chemin que vous choisissez, ou les deux, dépend de votre application. Nous allons examiner les deux configurations dans ce document.

**Rendu des mémoires tampons d’occlusion pour l’effet holographique**

Commencez par effacer la vue de la cible de rendu pour la caméra virtuelle actuelle.

À partir de AppMain. cpp :

```cpp
context->ClearRenderTargetView(pCameraResources->GetBackBufferRenderTargetView(), DirectX::Colors::Transparent);
```

Il s’agit d’une passe de « pré-rendu ». Ici, nous créons une mémoire tampon d’occlusion en demandant au convertisseur de maille d’afficher uniquement la profondeur. Dans cette configuration, nous n’attachons pas de vue de cible de rendu et le convertisseur de maillage définit l’étape de nuanceur de pixels sur **nullptr** afin que le GPU ne s’arrête pas à dessiner des pixels. La géométrie est pixellisée dans le tampon de profondeur et le pipeline graphique s’arrête.

```cpp
// Pre-pass rendering: Create occlusion buffer from Surface Mapping data.
context->ClearDepthStencilView(pCameraResources->GetSurfaceDepthStencilView(), D3D11_CLEAR_DEPTH | D3D11_CLEAR_STENCIL, 1.0f, 0);

// Set the render target to null, and set the depth target occlusion buffer.
// We will use this same buffer as a shader resource when drawing holograms.
context->OMSetRenderTargets(0, nullptr, pCameraResources->GetSurfaceOcclusionDepthStencilView());

// The first pass is a depth-only pass that generates an occlusion buffer we can use to know which
// hologram pixels are hidden behind surfaces in the environment.
m_meshCollection->Render(pCameraResources->IsRenderingStereoscopic(), true);
```

Nous pouvons dessiner des hologrammes avec un test de profondeur supplémentaire sur la mémoire tampon d’occlusion de mappage de surface. Dans cet exemple de code, nous avons rendu les pixels sur le cube d’une couleur différente s’ils se trouvent derrière une surface.

À partir de AppMain. cpp :

```cpp
// Hologram rendering pass: Draw holographic content.
context->ClearDepthStencilView(pCameraResources->GetHologramDepthStencilView(), D3D11_CLEAR_DEPTH | D3D11_CLEAR_STENCIL, 1.0f, 0);

// Set the render target, and set the depth target drawing buffer.
ID3D11RenderTargetView *const targets[1] = { pCameraResources->GetBackBufferRenderTargetView() };
context->OMSetRenderTargets(1, targets, pCameraResources->GetHologramDepthStencilView());

// Render the scene objects.
// In this example, we draw a special effect that uses the occlusion buffer we generated in the
// Pre-Pass step to render holograms using X-Ray Vision when they are behind physical objects.
m_xrayCubeRenderer->Render(
    pCameraResources->IsRenderingStereoscopic(),
    pCameraResources->GetSurfaceOcclusionShaderResourceView(),
    pCameraResources->GetHologramOcclusionShaderResourceView(),
    pCameraResources->GetDepthTextureSamplerState()
    );
```

Basé sur le code de SpecialEffectPixelShader. HLSL :

```cpp
// Draw boundaries
min16int surfaceSum = GatherDepthLess(envDepthTex, uniSamp, input.pos.xy, pixelDepth, input.idx.x);

if (surfaceSum <= -maxSum)
{
    // The pixel and its neighbors are behind the surface.
    // Return the occluded 'X-ray' color.
    return min16float4(0.67f, 0.f, 0.f, 1.0f);
}
else if (surfaceSum < maxSum)
{
    // The pixel and its neighbors are a mix of in front of and behind the surface.
    // Return the silhouette edge color.
    return min16float4(1.f, 1.f, 1.f, 1.0f);
}
else
{
    // The pixel and its neighbors are all in front of the surface.
    // Return the color of the hologram.
    return min16float4(input.color, 1.0f);
}
```

**Remarque :** Pour notre routine **GatherDepthLess** , consultez l’exemple de code de mappage des surfaces : SpecialEffectPixelShader. HLSL.

**Rendu des données de maillage des surfaces à l’affichage**

Nous pouvons également simplement dessiner les maillages des surfaces dans les tampons d’affichage stéréo. Nous avons choisi de dessiner des visages complets avec de l’éclairage, mais vous êtes libre de dessiner du filaire, de traiter les maillages avant le rendu, d’appliquer une carte de texture, etc.

Ici, notre exemple de code indique au convertisseur de maille de dessiner la collection. Cette fois, nous ne spécifions pas de passage à profondeur uniquement. il attachera donc un nuanceur de pixels et terminera le pipeline de rendu à l’aide des cibles que nous avons spécifiées pour la caméra virtuelle actuelle.

```cpp
// Spatial Mapping mesh rendering pass: Draw Spatial Mapping mesh over the world.
context->ClearDepthStencilView(pCameraResources->GetSurfaceOcclusionDepthStencilView(), D3D11_CLEAR_DEPTH | D3D11_CLEAR_STENCIL, 1.0f, 0);

// Set the render target to the current holographic camera's back buffer, and set the depth buffer.
ID3D11RenderTargetView *const targets[1] = { pCameraResources->GetBackBufferRenderTargetView() };
context->OMSetRenderTargets(1, targets, pCameraResources->GetSurfaceDepthStencilView());

// This drawing pass renders the surface meshes to the stereoscopic display. The user will be
// able to see them while wearing the device.
m_meshCollection->Render(pCameraResources->IsRenderingStereoscopic(), false);
```

## <a name="see-also"></a>Voir aussi
* [Création d’un projet DirectX holographique](creating-a-holographic-directx-project.md)
* [API Windows. perception. spatial](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.aspx)
