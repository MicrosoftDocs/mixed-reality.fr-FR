---
title: Mappage spatial dans DirectX
description: Explique comment implémenter le mappage spatial dans votre application DirectX. Cela inclut une explication détaillée de l’application de mappage spatial est incluse avec le SDK de plateforme Windows universelle.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows mixte réalité, mappage spatial, environnement, interaction, directx, winrt, api, exemple de code, UWP, SDK, procédure pas à pas
ms.openlocfilehash: db3f1464158c04127e456cadd5fb633336909344
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597140"
---
# <a name="spatial-mapping-in-directx"></a>Mappage spatial dans DirectX

Cette rubrique décrit comment implémenter [mappage spatial](spatial-mapping.md) dans votre application DirectX. Cela inclut une explication détaillée de l’application de mappage spatial est incluse avec le SDK de plateforme Windows universelle.

Cette rubrique utilise le code à partir de la [HolographicSpatialMapping](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) exemple de code UWP.

>[!NOTE]
>Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).  Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.

## <a name="directx-development-overview"></a>Vue d’ensemble du développement DirectX

Développement d’applications natives pour le mappage spatial utilise les API sous le [Windows.Perception.Spatial](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.aspx) espace de noms. Ces API offrent un contrôle total de la fonctionnalité de mappage spatial, à la manière directement au mappage spatial API exposées par [Unity](spatial-mapping-in-unity.md).

### <a name="perception-apis"></a>API de perception

Les principaux types fournis pour le développement de mappage spatial sont les suivantes :
* [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) fournit des informations sur les surfaces dans des régions d’espace près de l’utilisateur, sous la forme d’objets de SpatialSurfaceInfo spécifiée par l’application.
* [SpatialSurfaceInfo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.aspx) décrit des spatiale surface unique, comprenant un ID unique, volume et l’heure de dernière modification de délimitation. Il fournira une SpatialSurfaceMesh de façon asynchrone à la demande.
* [SpatialSurfaceMeshOptions](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemeshoptions.aspx) contient les paramètres utilisés pour personnaliser les objets SpatialSurfaceMesh demandés à partir de SpatialSurfaceInfo.
* [SpatialSurfaceMesh](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.aspx) représente les données de la maille pour une seule surface spatiale. Les données pour les positions de vertex, les normales des sommets et des indices de triangle sont contenues dans les objets membres SpatialSurfaceMeshBuffer.
* [SpatialSurfaceMeshBuffer](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemeshbuffer.aspx) encapsule un seul type de données de la maille.

Lorsque vous développez une application à l’aide de ces API, votre flux de programme de base sera ressembler à ceci (comme illustré dans l’exemple d’application décrit ci-dessous) :
- **Configurer votre SpatialSurfaceObserver**
  - Appelez [RequestAccessAsync](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.requestaccessasync.aspx)pour vous assurer que l’utilisateur a donné l’autorisation pour votre application pour utiliser les fonctionnalités de mappage spatial de l’appareil.
  - Instancie un objet SpatialSurfaceObserver.
  - Appelez [SetBoundingVolumes](https://msdn.microsoft.com/library/windows/apps/mt592747.aspx) pour spécifier les régions d’espace dans lequel vous souhaitez des informations sur les surfaces spatiales. Vous pouvez modifier ces régions à l’avenir en appelant simplement cette fonction à nouveau. Chaque région est spécifiée en utilisant un [SpatialBoundingVolume](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialboundingvolume.aspx).
  - Inscrivez-vous à la [ObservedSurfacesChanged](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.observedsurfaceschanged.aspx) événement qui se déclenche chaque fois que les nouvelles informations sont disponibles sur les surfaces spatiales dans les régions d’espace que vous avez spécifié.
- **Traiter les événements ObservedSurfacesChanged**
  - Dans votre gestionnaire d’événements, appelez [GetObservedSurfaces](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.getobservedsurfaces.aspx) pour recevoir un mappage d’objets de SpatialSurfaceInfo. À l’aide de ce mappage, vous pouvez mettre à jour vos enregistrements des surfaces spatiales [existent dans l’environnement utilisateur](spatial-mapping.md#mesh-caching).
  - Pour chaque objet SpatialSurfaceInfo, vous pouvez interroger [TryGetBounds](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.trygetbounds.aspx) pour déterminer les étendues spatiales de la surface, exprimée en un [système de coordonnées spatial](coordinate-systems.md) de votre choix.
  - Si vous décidez de demander la maille pour une surface spatiale, appelez [TryComputeLatestMeshAsync](https://msdn.microsoft.com/library/windows/apps/mt592715.aspx). Vous pouvez fournir des options qui spécifient la densité souhaitée de triangles et le format des données de la maille retourné.
- **Recevoir et traiter de maillage**
  - Chaque appel à TryComputeLatestMeshAsync sera aysnchronously renvoyer un objet SpatialSurfaceMesh.
  - À partir de cet objet vous pouvez accéder aux objets SpatialSurfaceMeshBuffer relation contenant-contenus pour accéder aux indices de triangle, les positions de vertex et (si nécessaire) les normales des sommets du maillage. Ces données seront dans un format directement compatible avec le [Direct3D 11 API](https://msdn.microsoft.com/library/windows/desktop/ff476501(v=vs.85).aspx) utilisés pour le rendu des mailles.
  - À ce stade votre application peut éventuellement exécuter analysis ou [traitement](spatial-mapping.md#mesh-processing) des données de la maille et utilisez-la pour [rendu](spatial-mapping.md#rendering) et de la physique [raycasting et collision](spatial-mapping.md#raycasting-and-collision).
  - Un détail important à noter est que vous devez appliquer une mise à l’échelle vers les positions de vertex de maille (par exemple dans le nuanceur de sommets utilisés pour le rendu des mailles), pour les convertir des unités optimisé entier dans lequel ils sont stockés dans la mémoire tampon, de compteurs. Vous pouvez récupérer cette mise à l’échelle en appelant [VertexPositionScale](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.vertexpositionscale.aspx).

### <a name="troubleshooting"></a>Résolution des problèmes
* N’oubliez pas de mettre à l’échelle des positions de vertex de maillage dans votre nuanceur de sommets, à l’aide de l’échelle retourné par [SpatialSurfaceMesh.VertexPositionScale](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.vertexpositionscale.aspx)

## <a name="spatial-mapping-code-sample-walkthrough"></a>Procédure d’exemple de code mappage spatial

Le [mappage Spatial HOLOGRAPHIQUE](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) exemple de code contient du code que vous pouvez utiliser pour commencer le chargement des mailles surfaces dans votre application, notamment l’infrastructure de gestion et maillages de surface de rendu.

À présent, voyons comment ajouter la fonctionnalité de cartographie aire de conception à votre application DirectX. Vous pouvez ajouter ce code à votre [modèle d’application Windows HOLOGRAPHIQUE](creating-a-holographic-directx-project.md) projet, ou vous pouvez suivre la procédure en parcourant l’exemple de code mentionné ci-dessus. Cet exemple de code est basé sur le modèle d’application Windows HOLOGRAPHIQUE.

### <a name="set-up-your-app-to-use-the-spatialperception-capability"></a>Configurer votre application pour utiliser la fonctionnalité spatialPerception

Votre application doit être en mesure d’utiliser la fonctionnalité de mappage spatial. Cela est nécessaire, car le maillage spatial est une représentation de l’environnement utilisateur, qui peut-être être considérés comme des données privées. Déclarez cette fonctionnalité dans le fichier package.appxmanifest pour votre application. Voici un exemple :

```xml
<Capabilities>
  <uap2:Capability Name="spatialPerception" />
</Capabilities>
```

La fonctionnalité provient de la **uap2** espace de noms. Pour accéder à cet espace de noms dans votre manifeste, inclure un *xlmns* d’attribut dans le &lt;Package > élément. Voici un exemple :

```xml
<Package
    xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
    xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
    xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
    xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2"
    IgnorableNamespaces="uap uap2 mp"
    >
```

### <a name="check-for-spatial-mapping-feature-support"></a>Recherchez la prise en charge des fonctionnalités de mappage spatial

Réalité mixte Windows prend en charge un large éventail d’appareils, y compris les appareils qui ne prennent pas en charge le mappage spatial. Si votre application peut utiliser mappage spatial ou devez utiliser le mappage spatial, pour fournir des fonctionnalités, elle doit vérifier pour vous assurer que le mappage spatial est pris en charge avant d’essayer de l’utiliser. Par exemple, si le mappage spatial est requis par votre application de réalité mixte, il doit afficher un message à cet effet, si un utilisateur tente d’exécuter sur un appareil sans mappage spatial. Ou bien, votre application peut être capable de restituer son propre environnement virtuel à la place de l’environnement utilisateur, offrant une expérience similaire à ce qui se passerait si le mappage spatial n’était pas disponible. En tout cas, cette API permet à votre application à connaître quand il pas obtenir les données de mappage spatial et répondre de manière appropriée.

Pour vérifier l’appareil en cours pour la prise en charge du mappage spatial, d’abord vous assurer que le contrat UWP est au niveau 4 ou supérieur, puis appelez SpatialSurfaceObserver::IsSupported(). Voici comment faire dans le contexte de la [mappage Spatial HOLOGRAPHIQUE](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) exemple de code. Prise en charge est vérifiée juste avant la demande d’accès.

L’API SpatialSurfaceObserver::IsSupported() est disponible dans le SDK version 15063 de. Si nécessaire, recibler votre projet vers la version de plateforme 15063 avant d’utiliser cette API.

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

Notez que lorsque le contrat UWP est inférieur au niveau 4, l’application doit poursuivre comme si l’appareil est capable de faire le mappage spatial.

### <a name="request-access-to-spatial-mapping-data"></a>Demander l’accès aux données de mappage spatial

Votre application doit demander l’autorisation d’accéder aux données de mappage spatial avant d’essayer de créer les observateurs d’aire de conception. Voici un exemple en fonction de notre exemple de code de mappage de Surface, avec plus de détails fournis par la suite de cette page :

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

### <a name="create-a-surface-observer"></a>Créer un aire de conception observateur

Le **Windows::Perception::Spatial::Surfaces** espace de noms inclut la [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) (classe), qui observe un ou plusieurs volumes que vous spécifiez dans un [ SpatialCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.aspx). Utilisez un [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) instance pour accéder aux données de maillage de la surface en temps réel.

À partir de **AppMain.h**:

```cpp
// Obtains surface mapping data from the device in real time.
Windows::Perception::Spatial::Surfaces::SpatialSurfaceObserver^     m_surfaceObserver;
Windows::Perception::Spatial::Surfaces::SpatialSurfaceMeshOptions^  m_surfaceMeshOptions;
```

Comme indiqué dans la section précédente, vous devez demander l’accès aux données de mappage spatial avant que votre application peut l’utiliser. Cet accès est accordé automatiquement sur le HoloLens.

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

Ensuite, vous devez configurer l’aire de conception observateur pour observer un volume spécifique englobant. Ici, nous observons une zone qui est de 20 x 20 x 5 mètres, centrée à l’origine du système de coordonnées.

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

*Il s’agit de pseudo-code :*

```cpp
m_surfaceObserver->SetBoundingVolumes(/* iterable collection of bounding volumes*/);
```

Il est également possible d’utiliser d’autres formes englobants - comme une frustum vue, ou à une zone englobante qui n’est pas l’axe.

*Il s’agit de pseudo-code :*

```cpp
m_surfaceObserver->SetBoundingVolume(
            SpatialBoundingVolume::FromFrustum(/*SpatialCoordinateSystem*/, /*SpatialBoundingFrustum*/)
            );
```

Si votre application a besoin de rien à faire différemment lors de la surface de mappage de données n’est pas disponible, vous pouvez écrire du code pour répondre au cas où le [SpatialPerceptionAccessStatus](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialperceptionaccessstatus.aspx) n’est pas **autorisé** , par exemple, Il ne pourrez pas sur les PC avec les appareils immersives attachés, car ces appareils n’ayant pas le matériel pour le mappage spatial. Pour ces appareils, vous fiez à la place à l’étape spatiale pour plus d’informations sur l’environnement et la configuration de l’appareil de l’utilisateur.

### <a name="initialize-and-update-the-surface-mesh-collection"></a>Initialiser et mettre à jour de la collection de la maille superficielle

Si l’aire de conception observateur a été créé avec succès, nous pouvons passer à initialiser notre collection maille superficielle. Ici, nous utilisons l’API de modèle d’extraction pour obtenir l’ensemble actuel des surfaces observées immédiatement :

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

Il existe également un modèle d’émission obtenir des données de la maille superficielle. Vous êtes libre de concevoir votre application pour utiliser le modèle d’extraction uniquement si vous choisissez, auquel cas vous allez interroger pour les données régulièrement - par exemple, une fois par frame - ou pendant une période de temps spécifique, comme lors de l’installation de jeu. Dans ce cas, le code ci-dessus est ce dont vous avez besoin.

Dans notre exemple de code, nous avons choisi illustrer l’utilisation des deux modèles à des fins pédagogiques. Ici, vous vous abonnez à un événement pour recevoir des données de la maille superficielle à jour chaque fois que le système reconnaît une modification.

```cpp
m_surfaceObserver->ObservedSurfacesChanged += ref new TypedEventHandler<SpatialSurfaceObserver^, Platform::Object^>(
            bind(&HolographicDesktopAppMain::OnSurfacesChanged, this, _1, _2)
            );
```

Notre exemple de code est également configuré pour répondre à ces événements. Nous allons étudier comment procéder.

**REMARQUE :** Cela peut être le moyen le plus efficace pour votre application gérer les données de la maille. Ce code est écrit par souci de clarté et n’est pas optimisé.

Les données de la maille superficielle sont fournies dans un mappage en lecture seule qui stocke [SpatialSurfaceInfo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.aspx) à l’aide des objets [Platform::Guids](https://msdn.microsoft.com/library/windows/desktop/aa373931.aspx) comme valeurs de clés.

```cpp
IMapView<Guid, SpatialSurfaceInfo^>^ const& surfaceCollection = sender->GetObservedSurfaces();
```

Pour traiter ces données, nous allons premier pour les valeurs de clé qui ne sont pas dans notre collection. Plus d’informations sur la façon dont les données sont stockées dans notre exemple d’application seront affiche plus loin dans cette rubrique.

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

Nous devons également supprimer les mailles de surface qui se trouvent dans notre collection maille superficielle, mais qui ne sont pas dans la collection système plus. Pour ce faire, nous devons faire quelque chose à l’opposé de ce que nous venons de pour l’ajout et la mise à jour des mailles ; nous répétons la boucle sur la collection de notre application et vérifiez si le **Guid** nous avons se trouve dans la collection du système. Si elle n’est pas dans la collection system, nous supprimez-le nôtres.

À partir de notre gestionnaire d’événements dans AppMain.cpp :

```cpp
m_meshCollection->PruneMeshCollection(surfaceCollection);
```

L’implémentation de nettoyage du maillage dans RealtimeSurfaceMeshRenderer.cpp :

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

### <a name="acquire-and-use-surface-mesh-data-buffers"></a>Récupérer et utiliser des mémoires tampons de données de maille superficielle

Obtention d’informations de la maille superficielle a été aussi simple que l’extraction d’une collection de données et le traitement des mises à jour de cette collection. Maintenant, nous aborderons en détail sur la façon dont vous pouvez utiliser les données.

Dans notre exemple de code, nous avons choisi d’utiliser les panneaux d’aire de conception pour le rendu. Il s’agit d’un scénario courant pour OCCLUSION hologrammes derrière les surfaces du monde réel. Vous pouvez également afficher les panneaux ou restituer traité des versions de ces, pour lui montrer les zones de la salle sont analysées avant de commencer à fournir des fonctionnalités de l’application ou votre jeu.

L’exemple de code démarre le processus lorsqu’il reçoit des mises à jour de la maille superficielle du Gestionnaire d’événements que nous avons décrit dans la section précédente. La ligne importante de code dans cette fonction est l’appel à mettre à jour la surface *mesh*: à ce stade, nous avons déjà traité les informations de la maille, et nous sommes sur le point d’obtenir les données de vertex et d’index pour une utilisation comme bon nous semble.

À partir de RealtimeSurfaceMeshRenderer.cpp :

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

Notre exemple de code est conçu afin qu’une classe de données, **SurfaceMesh**, traite les données de maillage de traitement et le rendu. Les mailles sont ce que le **RealtimeSurfaceMeshRenderer** réellement conserve un mappage de. Chacun d’eux a une référence à la SpatialSurfaceMesh il provient, et nous utilisez-la chaque fois que nous devons accéder les mémoires tampons de vertex ou index de maillage ou obtenir une transformation pour le maillage. Pour l’instant, nous indicateur la maille comme nécessitant une mise à jour.

À partir de SurfaceMesh.cpp :

```cpp
void SurfaceMesh::UpdateSurface(SpatialSurfaceMesh^ surfaceMesh)
{
    m_surfaceMesh = surfaceMesh;
    m_updateNeeded = true;
}
```

Prochaine fois que le maillage est invité à se dessiner lui-même, il vérifie l’indicateur tout d’abord. Si une mise à jour est nécessaire, les mémoires tampons de vertex et d’index seront mis à jour sur le GPU.

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

Tout d’abord, nous avons obtenu les mémoires tampons de données brutes :

```cpp
Windows::Storage::Streams::IBuffer^ positions = m_surfaceMesh->VertexPositions->Data;
    Windows::Storage::Streams::IBuffer^ normals   = m_surfaceMesh->VertexNormals->Data;
    Windows::Storage::Streams::IBuffer^ indices   = m_surfaceMesh->TriangleIndices->Data;
```

Puis, nous créons des mémoires tampons de périphérique Direct3D avec les données de maillage fournies par le HoloLens :

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

**REMARQUE :** Pour la fonction d’assistance de CreateDirectXBuffer utilisée dans l’extrait précédent, consultez l’exemple de code de mappage de la Surface : SurfaceMesh.cpp, GetDataFromIBuffer.h. La création de ressources de périphérique est désormais terminée et le maillage est considéré comme pour être chargée et prête pour la mise à jour et restituer.

### <a name="update-and-render-surface-meshes"></a>Mettre à jour et restituer des maillages de surface

Notre classe SurfaceMesh possède une fonction de mise à jour spécialisé. Chaque [SpatialSurfaceMesh](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.aspx) a sa propre transformation, et notre exemple utilise le système de coordonnées actuel pour notre **SpatialStationaryReferenceFrame** pour acquérir la transformation. Puis il met à jour la mémoire tampon constante de modèle sur le GPU.

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

Lorsqu’il est temps pour restituer des mailles aire de conception, nous effectuer un travail de préparation avant le rendu de la collection. Nous configurons le pipeline de nuanceur pour la configuration de rendu actuelle, et nous configurons l’étape de l’assembleur d’entrée. Notez que la classe d’assistance de caméra HOLOGRAPHIQUE **CameraResources.cpp** a déjà configuré la mémoire tampon de projection de la vue constante à ce stade.

À partir de **RealtimeSurfaceMeshRenderer::Render**:

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

Après cela, nous boucle sur notre mailles et indiquer à chacun d’eux se dessiner lui-même. **REMARQUE :** Cet exemple de code n’est pas optimisée pour utiliser une forme quelconque de frustum élimination face arrière, mais vous devez inclure cette fonctionnalité dans votre application.

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

Les panneaux individuels sont responsables de configuration de la mémoire tampon de vertex et d’index, le stride et la mémoire tampon constante de transformation de modèle. Comme avec le cube en rotation dans le modèle d’application Windows HOLOGRAPHIQUE, nous affichons dans les mémoires tampons STÉRÉOSCOPIQUES à l’aide de l’instanciation.

À partir de **SurfaceMesh::Draw**:

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

### <a name="rendering-choices-with-surface-mapping"></a>Choix de rendu avec Surface de mappage

L’exemple de code de mappage de Surface offre un code de rendu occlusion uniquement des données de la maille superficielle et de rendu à l’écran de données de la maille superficielle. Le chemin d’accès que vous choisissez - ou les deux - dépendent de votre application. Nous allons étudier les deux configurations dans ce document.

**Rendu des mémoires tampons d’occlusion pour effet HOLOGRAPHIQUE**

Démarrez en désactivant la vue de cible de rendu pour la caméra virtuelle en cours.

À partir de AppMain.cpp :

```cpp
context->ClearRenderTargetView(pCameraResources->GetBackBufferRenderTargetView(), DirectX::Colors::Transparent);
```

Il s’agit d’une passe de « préaffichage ». Ici, nous créons une mémoire tampon d’occlusion en demandant le convertisseur de maillage pour restituer la profondeur uniquement. Dans cette configuration, nous ne pas attacher une vue de cible de rendu et le convertisseur de maillage définit l’étape du nuanceur de pixels **nullptr** afin que le GPU ne cherche pas à dessiner les pixels. La géométrie sera rastérisé vers la mémoire tampon de profondeur, et le pipeline graphique s’y arrête.

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

Nous pouvons dessiner hologrammes avec un test de profondeur supplémentaire par rapport à la mémoire tampon occlusion de Surface de mappage. Dans cet exemple de code, nous affichons pixels sur le cube une couleur différente si elles se trouvent derrière une surface.

À partir de AppMain.cpp :

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

Basé sur le code de SpecialEffectPixelShader.hlsl :

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

**Remarque :** Pour notre **GatherDepthLess** routine, consultez l’exemple de code de mappage de la Surface : SpecialEffectPixelShader.hlsl.

**Données de maillage de la surface de rendu à l’affichage**

Nous pouvons aussi simplement tirer les maillages de surface d’exposition pour les mémoires tampons d’affichage stéréo. Nous avons choisi de dessiner des visages complètes avec éclairage, mais vous êtes libre de dessiner filaire, traiter des mailles avant le rendu, appliquer un mappage de texture et ainsi de suite.

Ici, notre exemple de code indique le convertisseur de maillage pour dessiner la collection. Cette fois nous ne spécifions pas une passe de profondeur uniquement, afin de s’attacher un nuanceur de pixels et terminer le pipeline de rendu à l’aide de cibles que nous avons spécifié pour la caméra virtuelle en cours.

```cpp
// SR mesh rendering pass: Draw SR mesh over the world.
context->ClearDepthStencilView(pCameraResources->GetSurfaceOcclusionDepthStencilView(), D3D11_CLEAR_DEPTH | D3D11_CLEAR_STENCIL, 1.0f, 0);

// Set the render target to the current holographic camera's back buffer, and set the depth buffer.
ID3D11RenderTargetView *const targets[1] = { pCameraResources->GetBackBufferRenderTargetView() };
context->OMSetRenderTargets(1, targets, pCameraResources->GetSurfaceDepthStencilView());

// This drawing pass renders the surface meshes to the stereoscopic display. The user will be
// able to see them while wearing the device.
m_meshCollection->Render(pCameraResources->IsRenderingStereoscopic(), false);
```

## <a name="see-also"></a>Voir aussi
* [Création d’un projet de DirectX HOLOGRAPHIQUE](creating-a-holographic-directx-project.md)
* [Windows.Perception.Spatial API](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.aspx)
