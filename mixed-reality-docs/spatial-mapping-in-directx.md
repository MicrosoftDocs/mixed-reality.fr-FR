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
# <a name="spatial-mapping-in-directx"></a><span data-ttu-id="1407d-105">Mappage spatial dans DirectX</span><span class="sxs-lookup"><span data-stu-id="1407d-105">Spatial mapping in DirectX</span></span>

<span data-ttu-id="1407d-106">Cette rubrique décrit comment implémenter [mappage spatial](spatial-mapping.md) dans votre application DirectX.</span><span class="sxs-lookup"><span data-stu-id="1407d-106">This topic describes how to implement [spatial mapping](spatial-mapping.md) in your DirectX app.</span></span> <span data-ttu-id="1407d-107">Cela inclut une explication détaillée de l’application de mappage spatial est incluse avec le SDK de plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="1407d-107">This includes a detailed explanation of the spatial mapping sample application that is included with the Universal Windows Platform SDK.</span></span>

<span data-ttu-id="1407d-108">Cette rubrique utilise le code à partir de la [HolographicSpatialMapping](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) exemple de code UWP.</span><span class="sxs-lookup"><span data-stu-id="1407d-108">This topic uses code from the [HolographicSpatialMapping](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) UWP code sample.</span></span>

>[!NOTE]
><span data-ttu-id="1407d-109">Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="1407d-109">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="1407d-110">Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="1407d-110">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

## <a name="directx-development-overview"></a><span data-ttu-id="1407d-111">Vue d’ensemble du développement DirectX</span><span class="sxs-lookup"><span data-stu-id="1407d-111">DirectX development overview</span></span>

<span data-ttu-id="1407d-112">Développement d’applications natives pour le mappage spatial utilise les API sous le [Windows.Perception.Spatial](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.aspx) espace de noms.</span><span class="sxs-lookup"><span data-stu-id="1407d-112">Native application development for spatial mapping uses the APIs under the [Windows.Perception.Spatial](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.aspx) namespace.</span></span> <span data-ttu-id="1407d-113">Ces API offrent un contrôle total de la fonctionnalité de mappage spatial, à la manière directement au mappage spatial API exposées par [Unity](spatial-mapping-in-unity.md).</span><span class="sxs-lookup"><span data-stu-id="1407d-113">These APIs provide full control of spatial mapping functionality, in a manner directly analogous to the spatial mapping APIs exposed by [Unity](spatial-mapping-in-unity.md).</span></span>

### <a name="perception-apis"></a><span data-ttu-id="1407d-114">API de perception</span><span class="sxs-lookup"><span data-stu-id="1407d-114">Perception APIs</span></span>

<span data-ttu-id="1407d-115">Les principaux types fournis pour le développement de mappage spatial sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="1407d-115">The primary types provided for spatial mapping development are as follows:</span></span>
* <span data-ttu-id="1407d-116">[SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) fournit des informations sur les surfaces dans des régions d’espace près de l’utilisateur, sous la forme d’objets de SpatialSurfaceInfo spécifiée par l’application.</span><span class="sxs-lookup"><span data-stu-id="1407d-116">[SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) provides information about surfaces in application-specified regions of space near the user, in the form of SpatialSurfaceInfo objects.</span></span>
* <span data-ttu-id="1407d-117">[SpatialSurfaceInfo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.aspx) décrit des spatiale surface unique, comprenant un ID unique, volume et l’heure de dernière modification de délimitation.</span><span class="sxs-lookup"><span data-stu-id="1407d-117">[SpatialSurfaceInfo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.aspx) describes a single extant spatial surface, including a unique ID, bounding volume and time of last change.</span></span> <span data-ttu-id="1407d-118">Il fournira une SpatialSurfaceMesh de façon asynchrone à la demande.</span><span class="sxs-lookup"><span data-stu-id="1407d-118">It will provide a SpatialSurfaceMesh asynchronously upon request.</span></span>
* <span data-ttu-id="1407d-119">[SpatialSurfaceMeshOptions](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemeshoptions.aspx) contient les paramètres utilisés pour personnaliser les objets SpatialSurfaceMesh demandés à partir de SpatialSurfaceInfo.</span><span class="sxs-lookup"><span data-stu-id="1407d-119">[SpatialSurfaceMeshOptions](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemeshoptions.aspx) contains parameters used to customize the SpatialSurfaceMesh objects requested from SpatialSurfaceInfo.</span></span>
* <span data-ttu-id="1407d-120">[SpatialSurfaceMesh](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.aspx) représente les données de la maille pour une seule surface spatiale.</span><span class="sxs-lookup"><span data-stu-id="1407d-120">[SpatialSurfaceMesh](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.aspx) represents the mesh data for a single spatial surface.</span></span> <span data-ttu-id="1407d-121">Les données pour les positions de vertex, les normales des sommets et des indices de triangle sont contenues dans les objets membres SpatialSurfaceMeshBuffer.</span><span class="sxs-lookup"><span data-stu-id="1407d-121">The data for vertex positions, vertex normals and triangle indices is contained in member SpatialSurfaceMeshBuffer objects.</span></span>
* <span data-ttu-id="1407d-122">[SpatialSurfaceMeshBuffer](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemeshbuffer.aspx) encapsule un seul type de données de la maille.</span><span class="sxs-lookup"><span data-stu-id="1407d-122">[SpatialSurfaceMeshBuffer](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemeshbuffer.aspx) wraps a single type of mesh data.</span></span>

<span data-ttu-id="1407d-123">Lorsque vous développez une application à l’aide de ces API, votre flux de programme de base sera ressembler à ceci (comme illustré dans l’exemple d’application décrit ci-dessous) :</span><span class="sxs-lookup"><span data-stu-id="1407d-123">When developing an application using these APIs, your basic program flow will look like this (as demonstrated in the sample application described below):</span></span>
- <span data-ttu-id="1407d-124">**Configurer votre SpatialSurfaceObserver**</span><span class="sxs-lookup"><span data-stu-id="1407d-124">**Set up your SpatialSurfaceObserver**</span></span>
  - <span data-ttu-id="1407d-125">Appelez [RequestAccessAsync](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.requestaccessasync.aspx)pour vous assurer que l’utilisateur a donné l’autorisation pour votre application pour utiliser les fonctionnalités de mappage spatial de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="1407d-125">Call [RequestAccessAsync](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.requestaccessasync.aspx), to ensure that the user has given permission for your application to use the device's spatial mapping capabilities.</span></span>
  - <span data-ttu-id="1407d-126">Instancie un objet SpatialSurfaceObserver.</span><span class="sxs-lookup"><span data-stu-id="1407d-126">Instantiate a SpatialSurfaceObserver object.</span></span>
  - <span data-ttu-id="1407d-127">Appelez [SetBoundingVolumes](https://msdn.microsoft.com/library/windows/apps/mt592747.aspx) pour spécifier les régions d’espace dans lequel vous souhaitez des informations sur les surfaces spatiales.</span><span class="sxs-lookup"><span data-stu-id="1407d-127">Call [SetBoundingVolumes](https://msdn.microsoft.com/library/windows/apps/mt592747.aspx) to specify the regions of space in which you want information about spatial surfaces.</span></span> <span data-ttu-id="1407d-128">Vous pouvez modifier ces régions à l’avenir en appelant simplement cette fonction à nouveau.</span><span class="sxs-lookup"><span data-stu-id="1407d-128">You may modify these regions in the future by simply calling this function again.</span></span> <span data-ttu-id="1407d-129">Chaque région est spécifiée en utilisant un [SpatialBoundingVolume](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialboundingvolume.aspx).</span><span class="sxs-lookup"><span data-stu-id="1407d-129">Each region is specified using a [SpatialBoundingVolume](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialboundingvolume.aspx).</span></span>
  - <span data-ttu-id="1407d-130">Inscrivez-vous à la [ObservedSurfacesChanged](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.observedsurfaceschanged.aspx) événement qui se déclenche chaque fois que les nouvelles informations sont disponibles sur les surfaces spatiales dans les régions d’espace que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="1407d-130">Register for the [ObservedSurfacesChanged](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.observedsurfaceschanged.aspx) event, which will fire whenever new information is available about the spatial surfaces in the regions of space you have specified.</span></span>
- <span data-ttu-id="1407d-131">**Traiter les événements ObservedSurfacesChanged**</span><span class="sxs-lookup"><span data-stu-id="1407d-131">**Process ObservedSurfacesChanged events**</span></span>
  - <span data-ttu-id="1407d-132">Dans votre gestionnaire d’événements, appelez [GetObservedSurfaces](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.getobservedsurfaces.aspx) pour recevoir un mappage d’objets de SpatialSurfaceInfo.</span><span class="sxs-lookup"><span data-stu-id="1407d-132">In your event handler, call [GetObservedSurfaces](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.getobservedsurfaces.aspx) to receive a map of SpatialSurfaceInfo objects.</span></span> <span data-ttu-id="1407d-133">À l’aide de ce mappage, vous pouvez mettre à jour vos enregistrements des surfaces spatiales [existent dans l’environnement utilisateur](spatial-mapping.md#mesh-caching).</span><span class="sxs-lookup"><span data-stu-id="1407d-133">Using this map, you can update your records of which spatial surfaces [exist in the user's environment](spatial-mapping.md#mesh-caching).</span></span>
  - <span data-ttu-id="1407d-134">Pour chaque objet SpatialSurfaceInfo, vous pouvez interroger [TryGetBounds](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.trygetbounds.aspx) pour déterminer les étendues spatiales de la surface, exprimée en un [système de coordonnées spatial](coordinate-systems.md) de votre choix.</span><span class="sxs-lookup"><span data-stu-id="1407d-134">For each SpatialSurfaceInfo object, you may query [TryGetBounds](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.trygetbounds.aspx) to determine the spatial extents of the surface, expressed in a [spatial coordinate system](coordinate-systems.md) of your choosing.</span></span>
  - <span data-ttu-id="1407d-135">Si vous décidez de demander la maille pour une surface spatiale, appelez [TryComputeLatestMeshAsync](https://msdn.microsoft.com/library/windows/apps/mt592715.aspx).</span><span class="sxs-lookup"><span data-stu-id="1407d-135">If you decide to request mesh for a spatial surface, call [TryComputeLatestMeshAsync](https://msdn.microsoft.com/library/windows/apps/mt592715.aspx).</span></span> <span data-ttu-id="1407d-136">Vous pouvez fournir des options qui spécifient la densité souhaitée de triangles et le format des données de la maille retourné.</span><span class="sxs-lookup"><span data-stu-id="1407d-136">You may provide options specifying the desired density of triangles, and the format of the returned mesh data.</span></span>
- <span data-ttu-id="1407d-137">**Recevoir et traiter de maillage**</span><span class="sxs-lookup"><span data-stu-id="1407d-137">**Receive and process mesh**</span></span>
  - <span data-ttu-id="1407d-138">Chaque appel à TryComputeLatestMeshAsync sera aysnchronously renvoyer un objet SpatialSurfaceMesh.</span><span class="sxs-lookup"><span data-stu-id="1407d-138">Each call to TryComputeLatestMeshAsync will aysnchronously return one SpatialSurfaceMesh object.</span></span>
  - <span data-ttu-id="1407d-139">À partir de cet objet vous pouvez accéder aux objets SpatialSurfaceMeshBuffer relation contenant-contenus pour accéder aux indices de triangle, les positions de vertex et (si nécessaire) les normales des sommets du maillage.</span><span class="sxs-lookup"><span data-stu-id="1407d-139">From this object you can access the contained SpatialSurfaceMeshBuffer objects in order to access the triangle indices, vertex positions and (if requested) vertex normals of the mesh.</span></span> <span data-ttu-id="1407d-140">Ces données seront dans un format directement compatible avec le [Direct3D 11 API](https://msdn.microsoft.com/library/windows/desktop/ff476501(v=vs.85).aspx) utilisés pour le rendu des mailles.</span><span class="sxs-lookup"><span data-stu-id="1407d-140">This data will be in a format directly compatible with the [Direct3D 11 APIs](https://msdn.microsoft.com/library/windows/desktop/ff476501(v=vs.85).aspx) used for rendering meshes.</span></span>
  - <span data-ttu-id="1407d-141">À ce stade votre application peut éventuellement exécuter analysis ou [traitement](spatial-mapping.md#mesh-processing) des données de la maille et utilisez-la pour [rendu](spatial-mapping.md#rendering) et de la physique [raycasting et collision](spatial-mapping.md#raycasting-and-collision).</span><span class="sxs-lookup"><span data-stu-id="1407d-141">From here your application can optionally perform analysis or [processing](spatial-mapping.md#mesh-processing) of the mesh data, and use it for [rendering](spatial-mapping.md#rendering) and physics [raycasting and collision](spatial-mapping.md#raycasting-and-collision).</span></span>
  - <span data-ttu-id="1407d-142">Un détail important à noter est que vous devez appliquer une mise à l’échelle vers les positions de vertex de maille (par exemple dans le nuanceur de sommets utilisés pour le rendu des mailles), pour les convertir des unités optimisé entier dans lequel ils sont stockés dans la mémoire tampon, de compteurs.</span><span class="sxs-lookup"><span data-stu-id="1407d-142">One important detail to note is that you must apply a scale to the mesh vertex positions (for example in the vertex shader used for rendering the meshes), to convert them from the optimized integer units in which they are stored in the buffer, to meters.</span></span> <span data-ttu-id="1407d-143">Vous pouvez récupérer cette mise à l’échelle en appelant [VertexPositionScale](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.vertexpositionscale.aspx).</span><span class="sxs-lookup"><span data-stu-id="1407d-143">You can retrieve this scale by calling [VertexPositionScale](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.vertexpositionscale.aspx).</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="1407d-144">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="1407d-144">Troubleshooting</span></span>
* <span data-ttu-id="1407d-145">N’oubliez pas de mettre à l’échelle des positions de vertex de maillage dans votre nuanceur de sommets, à l’aide de l’échelle retourné par [SpatialSurfaceMesh.VertexPositionScale](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.vertexpositionscale.aspx)</span><span class="sxs-lookup"><span data-stu-id="1407d-145">Don't forget to scale mesh vertex positions in your vertex shader, using the scale returned by [SpatialSurfaceMesh.VertexPositionScale](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.vertexpositionscale.aspx)</span></span>

## <a name="spatial-mapping-code-sample-walkthrough"></a><span data-ttu-id="1407d-146">Procédure d’exemple de code mappage spatial</span><span class="sxs-lookup"><span data-stu-id="1407d-146">Spatial Mapping code sample walkthrough</span></span>

<span data-ttu-id="1407d-147">Le [mappage Spatial HOLOGRAPHIQUE](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) exemple de code contient du code que vous pouvez utiliser pour commencer le chargement des mailles surfaces dans votre application, notamment l’infrastructure de gestion et maillages de surface de rendu.</span><span class="sxs-lookup"><span data-stu-id="1407d-147">The [Holographic Spatial Mapping](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) code sample includes code that you can use to get started loading surface meshes into your app, including infrastructure for managing and rendering surface meshes.</span></span>

<span data-ttu-id="1407d-148">À présent, voyons comment ajouter la fonctionnalité de cartographie aire de conception à votre application DirectX.</span><span class="sxs-lookup"><span data-stu-id="1407d-148">Now, we walk through how to add surface mapping capability to your DirectX app.</span></span> <span data-ttu-id="1407d-149">Vous pouvez ajouter ce code à votre [modèle d’application Windows HOLOGRAPHIQUE](creating-a-holographic-directx-project.md) projet, ou vous pouvez suivre la procédure en parcourant l’exemple de code mentionné ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="1407d-149">You can add this code to your [Windows Holographic app template](creating-a-holographic-directx-project.md) project, or you can follow along by browsing through the code sample mentioned above.</span></span> <span data-ttu-id="1407d-150">Cet exemple de code est basé sur le modèle d’application Windows HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="1407d-150">This code sample is based on the Windows Holographic app template.</span></span>

### <a name="set-up-your-app-to-use-the-spatialperception-capability"></a><span data-ttu-id="1407d-151">Configurer votre application pour utiliser la fonctionnalité spatialPerception</span><span class="sxs-lookup"><span data-stu-id="1407d-151">Set up your app to use the spatialPerception capability</span></span>

<span data-ttu-id="1407d-152">Votre application doit être en mesure d’utiliser la fonctionnalité de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="1407d-152">Your app must be able to use the spatial mapping capability.</span></span> <span data-ttu-id="1407d-153">Cela est nécessaire, car le maillage spatial est une représentation de l’environnement utilisateur, qui peut-être être considérés comme des données privées.</span><span class="sxs-lookup"><span data-stu-id="1407d-153">This is necessary because the spatial mesh is a representation of the user's environment, which may be considered private data.</span></span> <span data-ttu-id="1407d-154">Déclarez cette fonctionnalité dans le fichier package.appxmanifest pour votre application.</span><span class="sxs-lookup"><span data-stu-id="1407d-154">Declare this capability in the package.appxmanifest file for your app.</span></span> <span data-ttu-id="1407d-155">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="1407d-155">Here's an example:</span></span>

```xml
<Capabilities>
  <uap2:Capability Name="spatialPerception" />
</Capabilities>
```

<span data-ttu-id="1407d-156">La fonctionnalité provient de la **uap2** espace de noms.</span><span class="sxs-lookup"><span data-stu-id="1407d-156">The capability comes from the **uap2** namespace.</span></span> <span data-ttu-id="1407d-157">Pour accéder à cet espace de noms dans votre manifeste, inclure un *xlmns* d’attribut dans le &lt;Package > élément.</span><span class="sxs-lookup"><span data-stu-id="1407d-157">To get access to this namespace in your manifest, include it as an *xlmns* attribute in the &lt;Package> element.</span></span> <span data-ttu-id="1407d-158">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="1407d-158">Here's an example:</span></span>

```xml
<Package
    xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
    xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
    xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
    xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2"
    IgnorableNamespaces="uap uap2 mp"
    >
```

### <a name="check-for-spatial-mapping-feature-support"></a><span data-ttu-id="1407d-159">Recherchez la prise en charge des fonctionnalités de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="1407d-159">Check for spatial mapping feature support</span></span>

<span data-ttu-id="1407d-160">Réalité mixte Windows prend en charge un large éventail d’appareils, y compris les appareils qui ne prennent pas en charge le mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="1407d-160">Windows Mixed Reality supports a wide range of devices, including devices which do not support spatial mapping.</span></span> <span data-ttu-id="1407d-161">Si votre application peut utiliser mappage spatial ou devez utiliser le mappage spatial, pour fournir des fonctionnalités, elle doit vérifier pour vous assurer que le mappage spatial est pris en charge avant d’essayer de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="1407d-161">If your app can use spatial mapping, or must use spatial mapping, to provide functionality, it should check to make sure that spatial mapping is supported before trying to use it.</span></span> <span data-ttu-id="1407d-162">Par exemple, si le mappage spatial est requis par votre application de réalité mixte, il doit afficher un message à cet effet, si un utilisateur tente d’exécuter sur un appareil sans mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="1407d-162">For example, if spatial mapping is required by your mixed reality app, it should display a message to that effect if a user tries running it on a device without spatial mapping.</span></span> <span data-ttu-id="1407d-163">Ou bien, votre application peut être capable de restituer son propre environnement virtuel à la place de l’environnement utilisateur, offrant une expérience similaire à ce qui se passerait si le mappage spatial n’était pas disponible.</span><span class="sxs-lookup"><span data-stu-id="1407d-163">Or, your app may be able to render its own virtual environment in place of the user's environment, providing an experience that is similar to what would happen if spatial mapping were available.</span></span> <span data-ttu-id="1407d-164">En tout cas, cette API permet à votre application à connaître quand il pas obtenir les données de mappage spatial et répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="1407d-164">In any event, this API allows your app to be aware of when it will not get spatial mapping data and respond in the appropriate way.</span></span>

<span data-ttu-id="1407d-165">Pour vérifier l’appareil en cours pour la prise en charge du mappage spatial, d’abord vous assurer que le contrat UWP est au niveau 4 ou supérieur, puis appelez SpatialSurfaceObserver::IsSupported().</span><span class="sxs-lookup"><span data-stu-id="1407d-165">To check the current device for spatial mapping support, first make sure the UWP contract is at level 4 or greater and then call SpatialSurfaceObserver::IsSupported().</span></span> <span data-ttu-id="1407d-166">Voici comment faire dans le contexte de la [mappage Spatial HOLOGRAPHIQUE](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) exemple de code.</span><span class="sxs-lookup"><span data-stu-id="1407d-166">Here's how to do so in the context of the [Holographic Spatial Mapping](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) code sample.</span></span> <span data-ttu-id="1407d-167">Prise en charge est vérifiée juste avant la demande d’accès.</span><span class="sxs-lookup"><span data-stu-id="1407d-167">Support is checked just before requesting access.</span></span>

<span data-ttu-id="1407d-168">L’API SpatialSurfaceObserver::IsSupported() est disponible dans le SDK version 15063 de.</span><span class="sxs-lookup"><span data-stu-id="1407d-168">The SpatialSurfaceObserver::IsSupported() API is available starting in SDK version 15063.</span></span> <span data-ttu-id="1407d-169">Si nécessaire, recibler votre projet vers la version de plateforme 15063 avant d’utiliser cette API.</span><span class="sxs-lookup"><span data-stu-id="1407d-169">If necessary, retarget your project to platform version 15063 before using this API.</span></span>

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

<span data-ttu-id="1407d-170">Notez que lorsque le contrat UWP est inférieur au niveau 4, l’application doit poursuivre comme si l’appareil est capable de faire le mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="1407d-170">Note that when the UWP contract is less than level 4, the app should proceed as though the device is capable of doing spatial mapping.</span></span>

### <a name="request-access-to-spatial-mapping-data"></a><span data-ttu-id="1407d-171">Demander l’accès aux données de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="1407d-171">Request access to spatial mapping data</span></span>

<span data-ttu-id="1407d-172">Votre application doit demander l’autorisation d’accéder aux données de mappage spatial avant d’essayer de créer les observateurs d’aire de conception.</span><span class="sxs-lookup"><span data-stu-id="1407d-172">Your app needs to request permission to access spatial mapping data before trying to create any surface observers.</span></span> <span data-ttu-id="1407d-173">Voici un exemple en fonction de notre exemple de code de mappage de Surface, avec plus de détails fournis par la suite de cette page :</span><span class="sxs-lookup"><span data-stu-id="1407d-173">Here's an example based upon our Surface Mapping code sample, with more details provided later on this page:</span></span>

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

### <a name="create-a-surface-observer"></a><span data-ttu-id="1407d-174">Créer un aire de conception observateur</span><span class="sxs-lookup"><span data-stu-id="1407d-174">Create a surface observer</span></span>

<span data-ttu-id="1407d-175">Le **Windows::Perception::Spatial::Surfaces** espace de noms inclut la [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) (classe), qui observe un ou plusieurs volumes que vous spécifiez dans un [ SpatialCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.aspx).</span><span class="sxs-lookup"><span data-stu-id="1407d-175">The **Windows::Perception::Spatial::Surfaces** namespace includes the [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) class, which observes one or more volumes that you specify in a [SpatialCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.aspx).</span></span> <span data-ttu-id="1407d-176">Utilisez un [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) instance pour accéder aux données de maillage de la surface en temps réel.</span><span class="sxs-lookup"><span data-stu-id="1407d-176">Use a [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) instance to access surface mesh data in real time.</span></span>

<span data-ttu-id="1407d-177">À partir de **AppMain.h**:</span><span class="sxs-lookup"><span data-stu-id="1407d-177">From **AppMain.h**:</span></span>

```cpp
// Obtains surface mapping data from the device in real time.
Windows::Perception::Spatial::Surfaces::SpatialSurfaceObserver^     m_surfaceObserver;
Windows::Perception::Spatial::Surfaces::SpatialSurfaceMeshOptions^  m_surfaceMeshOptions;
```

<span data-ttu-id="1407d-178">Comme indiqué dans la section précédente, vous devez demander l’accès aux données de mappage spatial avant que votre application peut l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="1407d-178">As noted in the previous section, you must request access to spatial mapping data before your app can use it.</span></span> <span data-ttu-id="1407d-179">Cet accès est accordé automatiquement sur le HoloLens.</span><span class="sxs-lookup"><span data-stu-id="1407d-179">This access is granted automatically on the HoloLens.</span></span>

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

<span data-ttu-id="1407d-180">Ensuite, vous devez configurer l’aire de conception observateur pour observer un volume spécifique englobant.</span><span class="sxs-lookup"><span data-stu-id="1407d-180">Next, you need to configure the surface observer to observe a specific bounding volume.</span></span> <span data-ttu-id="1407d-181">Ici, nous observons une zone qui est de 20 x 20 x 5 mètres, centrée à l’origine du système de coordonnées.</span><span class="sxs-lookup"><span data-stu-id="1407d-181">Here, we observe a box that is 20x20x5 meters, centered at the origin of the coordinate system.</span></span>

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

<span data-ttu-id="1407d-182">Notez que vous pouvez définir plusieurs volumes englobants à la place.</span><span class="sxs-lookup"><span data-stu-id="1407d-182">Note that you can set multiple bounding volumes instead.</span></span>

<span data-ttu-id="1407d-183">*Il s’agit de pseudo-code :*</span><span class="sxs-lookup"><span data-stu-id="1407d-183">*This is pseudocode:*</span></span>

```cpp
m_surfaceObserver->SetBoundingVolumes(/* iterable collection of bounding volumes*/);
```

<span data-ttu-id="1407d-184">Il est également possible d’utiliser d’autres formes englobants - comme une frustum vue, ou à une zone englobante qui n’est pas l’axe.</span><span class="sxs-lookup"><span data-stu-id="1407d-184">It is also possible to use other bounding shapes - such as a view frustum, or a bounding box that is not axis aligned.</span></span>

<span data-ttu-id="1407d-185">*Il s’agit de pseudo-code :*</span><span class="sxs-lookup"><span data-stu-id="1407d-185">*This is pseudocode:*</span></span>

```cpp
m_surfaceObserver->SetBoundingVolume(
            SpatialBoundingVolume::FromFrustum(/*SpatialCoordinateSystem*/, /*SpatialBoundingFrustum*/)
            );
```

<span data-ttu-id="1407d-186">Si votre application a besoin de rien à faire différemment lors de la surface de mappage de données n’est pas disponible, vous pouvez écrire du code pour répondre au cas où le [SpatialPerceptionAccessStatus](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialperceptionaccessstatus.aspx) n’est pas **autorisé** , par exemple, Il ne pourrez pas sur les PC avec les appareils immersives attachés, car ces appareils n’ayant pas le matériel pour le mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="1407d-186">If your app needs to do anything differently when surface mapping data is not available, you can write code to respond to the case where the [SpatialPerceptionAccessStatus](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialperceptionaccessstatus.aspx) is not **Allowed** - for example, it will not be allowed on PCs with immersive devices attached because those devices don't have hardware for spatial mapping.</span></span> <span data-ttu-id="1407d-187">Pour ces appareils, vous fiez à la place à l’étape spatiale pour plus d’informations sur l’environnement et la configuration de l’appareil de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1407d-187">For these devices, you should instead rely on the spatial stage for information about the user's environment and device configuration.</span></span>

### <a name="initialize-and-update-the-surface-mesh-collection"></a><span data-ttu-id="1407d-188">Initialiser et mettre à jour de la collection de la maille superficielle</span><span class="sxs-lookup"><span data-stu-id="1407d-188">Initialize and update the surface mesh collection</span></span>

<span data-ttu-id="1407d-189">Si l’aire de conception observateur a été créé avec succès, nous pouvons passer à initialiser notre collection maille superficielle.</span><span class="sxs-lookup"><span data-stu-id="1407d-189">If the surface observer was successfully created, we can proceed to initialize our surface mesh collection.</span></span> <span data-ttu-id="1407d-190">Ici, nous utilisons l’API de modèle d’extraction pour obtenir l’ensemble actuel des surfaces observées immédiatement :</span><span class="sxs-lookup"><span data-stu-id="1407d-190">Here, we use the pull model API to get the current set of observed surfaces right away:</span></span>

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

<span data-ttu-id="1407d-191">Il existe également un modèle d’émission obtenir des données de la maille superficielle.</span><span class="sxs-lookup"><span data-stu-id="1407d-191">There is also a push model available to get surface mesh data.</span></span> <span data-ttu-id="1407d-192">Vous êtes libre de concevoir votre application pour utiliser le modèle d’extraction uniquement si vous choisissez, auquel cas vous allez interroger pour les données régulièrement - par exemple, une fois par frame - ou pendant une période de temps spécifique, comme lors de l’installation de jeu.</span><span class="sxs-lookup"><span data-stu-id="1407d-192">You are free to design your app to use only the pull model if you choose, in which case you'll poll for data every so often - say, once per frame - or during a specific time period, such as during game setup.</span></span> <span data-ttu-id="1407d-193">Dans ce cas, le code ci-dessus est ce dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="1407d-193">If so, the above code is what you need.</span></span>

<span data-ttu-id="1407d-194">Dans notre exemple de code, nous avons choisi illustrer l’utilisation des deux modèles à des fins pédagogiques.</span><span class="sxs-lookup"><span data-stu-id="1407d-194">In our code sample, we chose to demonstrate the use of both models for pedagogical purposes.</span></span> <span data-ttu-id="1407d-195">Ici, vous vous abonnez à un événement pour recevoir des données de la maille superficielle à jour chaque fois que le système reconnaît une modification.</span><span class="sxs-lookup"><span data-stu-id="1407d-195">Here, we subscribe to an event to receive up-to-date surface mesh data whenever the system recognizes a change.</span></span>

```cpp
m_surfaceObserver->ObservedSurfacesChanged += ref new TypedEventHandler<SpatialSurfaceObserver^, Platform::Object^>(
            bind(&HolographicDesktopAppMain::OnSurfacesChanged, this, _1, _2)
            );
```

<span data-ttu-id="1407d-196">Notre exemple de code est également configuré pour répondre à ces événements.</span><span class="sxs-lookup"><span data-stu-id="1407d-196">Our code sample is also configured to respond to these events.</span></span> <span data-ttu-id="1407d-197">Nous allons étudier comment procéder.</span><span class="sxs-lookup"><span data-stu-id="1407d-197">Let's walk through how we do this.</span></span>

<span data-ttu-id="1407d-198">**REMARQUE :** Cela peut être le moyen le plus efficace pour votre application gérer les données de la maille.</span><span class="sxs-lookup"><span data-stu-id="1407d-198">**NOTE:** This might not be the most efficient way for your app to handle mesh data.</span></span> <span data-ttu-id="1407d-199">Ce code est écrit par souci de clarté et n’est pas optimisé.</span><span class="sxs-lookup"><span data-stu-id="1407d-199">This code is written for clarity and is not optimized.</span></span>

<span data-ttu-id="1407d-200">Les données de la maille superficielle sont fournies dans un mappage en lecture seule qui stocke [SpatialSurfaceInfo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.aspx) à l’aide des objets [Platform::Guids](https://msdn.microsoft.com/library/windows/desktop/aa373931.aspx) comme valeurs de clés.</span><span class="sxs-lookup"><span data-stu-id="1407d-200">The surface mesh data is provided in a read-only map that stores [SpatialSurfaceInfo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.aspx) objects using [Platform::Guids](https://msdn.microsoft.com/library/windows/desktop/aa373931.aspx) as key values.</span></span>

```cpp
IMapView<Guid, SpatialSurfaceInfo^>^ const& surfaceCollection = sender->GetObservedSurfaces();
```

<span data-ttu-id="1407d-201">Pour traiter ces données, nous allons premier pour les valeurs de clé qui ne sont pas dans notre collection.</span><span class="sxs-lookup"><span data-stu-id="1407d-201">To process this data, we look first for key values that aren't in our collection.</span></span> <span data-ttu-id="1407d-202">Plus d’informations sur la façon dont les données sont stockées dans notre exemple d’application seront affiche plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="1407d-202">Details on how the data is stored in our sample app will be presented later in this topic.</span></span>

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

<span data-ttu-id="1407d-203">Nous devons également supprimer les mailles de surface qui se trouvent dans notre collection maille superficielle, mais qui ne sont pas dans la collection système plus.</span><span class="sxs-lookup"><span data-stu-id="1407d-203">We also have to remove surface meshes that are in our surface mesh collection, but that aren't in the system collection anymore.</span></span> <span data-ttu-id="1407d-204">Pour ce faire, nous devons faire quelque chose à l’opposé de ce que nous venons de pour l’ajout et la mise à jour des mailles ; nous répétons la boucle sur la collection de notre application et vérifiez si le **Guid** nous avons se trouve dans la collection du système.</span><span class="sxs-lookup"><span data-stu-id="1407d-204">To do so, we need to do something akin to the opposite of what we just showed for adding and updating meshes; we loop on our app's collection, and check to see if the **Guid** we have is in the system collection.</span></span> <span data-ttu-id="1407d-205">Si elle n’est pas dans la collection system, nous supprimez-le nôtres.</span><span class="sxs-lookup"><span data-stu-id="1407d-205">If it's not in the system collection, we remove it from ours.</span></span>

<span data-ttu-id="1407d-206">À partir de notre gestionnaire d’événements dans AppMain.cpp :</span><span class="sxs-lookup"><span data-stu-id="1407d-206">From our event handler in AppMain.cpp:</span></span>

```cpp
m_meshCollection->PruneMeshCollection(surfaceCollection);
```

<span data-ttu-id="1407d-207">L’implémentation de nettoyage du maillage dans RealtimeSurfaceMeshRenderer.cpp :</span><span class="sxs-lookup"><span data-stu-id="1407d-207">The implementation of mesh pruning in RealtimeSurfaceMeshRenderer.cpp:</span></span>

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

### <a name="acquire-and-use-surface-mesh-data-buffers"></a><span data-ttu-id="1407d-208">Récupérer et utiliser des mémoires tampons de données de maille superficielle</span><span class="sxs-lookup"><span data-stu-id="1407d-208">Acquire and use surface mesh data buffers</span></span>

<span data-ttu-id="1407d-209">Obtention d’informations de la maille superficielle a été aussi simple que l’extraction d’une collection de données et le traitement des mises à jour de cette collection.</span><span class="sxs-lookup"><span data-stu-id="1407d-209">Getting the surface mesh information was as easy as pulling a data collection and processing updates to that collection.</span></span> <span data-ttu-id="1407d-210">Maintenant, nous aborderons en détail sur la façon dont vous pouvez utiliser les données.</span><span class="sxs-lookup"><span data-stu-id="1407d-210">Now, we'll go into detail on how you can use the data.</span></span>

<span data-ttu-id="1407d-211">Dans notre exemple de code, nous avons choisi d’utiliser les panneaux d’aire de conception pour le rendu.</span><span class="sxs-lookup"><span data-stu-id="1407d-211">In our code example, we chose to use the surface meshes for rendering.</span></span> <span data-ttu-id="1407d-212">Il s’agit d’un scénario courant pour OCCLUSION hologrammes derrière les surfaces du monde réel.</span><span class="sxs-lookup"><span data-stu-id="1407d-212">This is a common scenario for occluding holograms behind real-world surfaces.</span></span> <span data-ttu-id="1407d-213">Vous pouvez également afficher les panneaux ou restituer traité des versions de ces, pour lui montrer les zones de la salle sont analysées avant de commencer à fournir des fonctionnalités de l’application ou votre jeu.</span><span class="sxs-lookup"><span data-stu-id="1407d-213">You can also render the meshes, or render processed versions of them, to show the user what areas of the room are scanned before you start providing app or game functionality.</span></span>

<span data-ttu-id="1407d-214">L’exemple de code démarre le processus lorsqu’il reçoit des mises à jour de la maille superficielle du Gestionnaire d’événements que nous avons décrit dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="1407d-214">The code sample starts the process when it receives surface mesh updates from the event handler that we described in the previous section.</span></span> <span data-ttu-id="1407d-215">La ligne importante de code dans cette fonction est l’appel à mettre à jour la surface *mesh*: à ce stade, nous avons déjà traité les informations de la maille, et nous sommes sur le point d’obtenir les données de vertex et d’index pour une utilisation comme bon nous semble.</span><span class="sxs-lookup"><span data-stu-id="1407d-215">The important line of code in this function is the call to update the surface *mesh*: by this time we have already processed the mesh info, and we are about to get the vertex and index data for use as we see fit.</span></span>

<span data-ttu-id="1407d-216">À partir de RealtimeSurfaceMeshRenderer.cpp :</span><span class="sxs-lookup"><span data-stu-id="1407d-216">From RealtimeSurfaceMeshRenderer.cpp:</span></span>

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

<span data-ttu-id="1407d-217">Notre exemple de code est conçu afin qu’une classe de données, **SurfaceMesh**, traite les données de maillage de traitement et le rendu.</span><span class="sxs-lookup"><span data-stu-id="1407d-217">Our sample code is designed so that a data class, **SurfaceMesh**, handles mesh data processing and rendering.</span></span> <span data-ttu-id="1407d-218">Les mailles sont ce que le **RealtimeSurfaceMeshRenderer** réellement conserve un mappage de.</span><span class="sxs-lookup"><span data-stu-id="1407d-218">These meshes are what the **RealtimeSurfaceMeshRenderer** actually keeps a map of.</span></span> <span data-ttu-id="1407d-219">Chacun d’eux a une référence à la SpatialSurfaceMesh il provient, et nous utilisez-la chaque fois que nous devons accéder les mémoires tampons de vertex ou index de maillage ou obtenir une transformation pour le maillage.</span><span class="sxs-lookup"><span data-stu-id="1407d-219">Each one has a reference to the SpatialSurfaceMesh it came from, and we use it any time that we need to access the mesh vertex or index buffers, or get a transform for the mesh.</span></span> <span data-ttu-id="1407d-220">Pour l’instant, nous indicateur la maille comme nécessitant une mise à jour.</span><span class="sxs-lookup"><span data-stu-id="1407d-220">For now, we flag the mesh as needing an update.</span></span>

<span data-ttu-id="1407d-221">À partir de SurfaceMesh.cpp :</span><span class="sxs-lookup"><span data-stu-id="1407d-221">From SurfaceMesh.cpp:</span></span>

```cpp
void SurfaceMesh::UpdateSurface(SpatialSurfaceMesh^ surfaceMesh)
{
    m_surfaceMesh = surfaceMesh;
    m_updateNeeded = true;
}
```

<span data-ttu-id="1407d-222">Prochaine fois que le maillage est invité à se dessiner lui-même, il vérifie l’indicateur tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="1407d-222">Next time the mesh is asked to draw itself, it will check the flag first.</span></span> <span data-ttu-id="1407d-223">Si une mise à jour est nécessaire, les mémoires tampons de vertex et d’index seront mis à jour sur le GPU.</span><span class="sxs-lookup"><span data-stu-id="1407d-223">If an update is needed, the vertex and index buffers will be updated on the GPU.</span></span>

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

<span data-ttu-id="1407d-224">Tout d’abord, nous avons obtenu les mémoires tampons de données brutes :</span><span class="sxs-lookup"><span data-stu-id="1407d-224">First, we acquire the raw data buffers:</span></span>

```cpp
Windows::Storage::Streams::IBuffer^ positions = m_surfaceMesh->VertexPositions->Data;
    Windows::Storage::Streams::IBuffer^ normals   = m_surfaceMesh->VertexNormals->Data;
    Windows::Storage::Streams::IBuffer^ indices   = m_surfaceMesh->TriangleIndices->Data;
```

<span data-ttu-id="1407d-225">Puis, nous créons des mémoires tampons de périphérique Direct3D avec les données de maillage fournies par le HoloLens :</span><span class="sxs-lookup"><span data-stu-id="1407d-225">Then, we create Direct3D device buffers with the mesh data provided by the HoloLens:</span></span>

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

<span data-ttu-id="1407d-226">**REMARQUE :** Pour la fonction d’assistance de CreateDirectXBuffer utilisée dans l’extrait précédent, consultez l’exemple de code de mappage de la Surface : SurfaceMesh.cpp, GetDataFromIBuffer.h.</span><span class="sxs-lookup"><span data-stu-id="1407d-226">**NOTE:** For the CreateDirectXBuffer helper function used in the previous snippet, see the Surface Mapping code sample: SurfaceMesh.cpp, GetDataFromIBuffer.h.</span></span> <span data-ttu-id="1407d-227">La création de ressources de périphérique est désormais terminée et le maillage est considéré comme pour être chargée et prête pour la mise à jour et restituer.</span><span class="sxs-lookup"><span data-stu-id="1407d-227">Now the device resource creation is complete, and the mesh is considered to be loaded and ready for update and render.</span></span>

### <a name="update-and-render-surface-meshes"></a><span data-ttu-id="1407d-228">Mettre à jour et restituer des maillages de surface</span><span class="sxs-lookup"><span data-stu-id="1407d-228">Update and render surface meshes</span></span>

<span data-ttu-id="1407d-229">Notre classe SurfaceMesh possède une fonction de mise à jour spécialisé.</span><span class="sxs-lookup"><span data-stu-id="1407d-229">Our SurfaceMesh class has a specialized update function.</span></span> <span data-ttu-id="1407d-230">Chaque [SpatialSurfaceMesh](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.aspx) a sa propre transformation, et notre exemple utilise le système de coordonnées actuel pour notre **SpatialStationaryReferenceFrame** pour acquérir la transformation.</span><span class="sxs-lookup"><span data-stu-id="1407d-230">Each [SpatialSurfaceMesh](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.aspx) has its own transform, and our sample uses the current coordinate system for our **SpatialStationaryReferenceFrame** to acquire the transform.</span></span> <span data-ttu-id="1407d-231">Puis il met à jour la mémoire tampon constante de modèle sur le GPU.</span><span class="sxs-lookup"><span data-stu-id="1407d-231">Then it updates the model constant buffer on the GPU.</span></span>

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

<span data-ttu-id="1407d-232">Lorsqu’il est temps pour restituer des mailles aire de conception, nous effectuer un travail de préparation avant le rendu de la collection.</span><span class="sxs-lookup"><span data-stu-id="1407d-232">When it's time to render surface meshes, we do some prep work before rendering the collection.</span></span> <span data-ttu-id="1407d-233">Nous configurons le pipeline de nuanceur pour la configuration de rendu actuelle, et nous configurons l’étape de l’assembleur d’entrée.</span><span class="sxs-lookup"><span data-stu-id="1407d-233">We set up the shader pipeline for the current rendering configuration, and we set up the input assembler stage.</span></span> <span data-ttu-id="1407d-234">Notez que la classe d’assistance de caméra HOLOGRAPHIQUE **CameraResources.cpp** a déjà configuré la mémoire tampon de projection de la vue constante à ce stade.</span><span class="sxs-lookup"><span data-stu-id="1407d-234">Note that the holographic camera helper class **CameraResources.cpp** already has set up the view/projection constant buffer by now.</span></span>

<span data-ttu-id="1407d-235">À partir de **RealtimeSurfaceMeshRenderer::Render**:</span><span class="sxs-lookup"><span data-stu-id="1407d-235">From **RealtimeSurfaceMeshRenderer::Render**:</span></span>

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

<span data-ttu-id="1407d-236">Après cela, nous boucle sur notre mailles et indiquer à chacun d’eux se dessiner lui-même.</span><span class="sxs-lookup"><span data-stu-id="1407d-236">Once this is done, we loop on our meshes and tell each one to draw itself.</span></span> <span data-ttu-id="1407d-237">**REMARQUE :** Cet exemple de code n’est pas optimisée pour utiliser une forme quelconque de frustum élimination face arrière, mais vous devez inclure cette fonctionnalité dans votre application.</span><span class="sxs-lookup"><span data-stu-id="1407d-237">**NOTE:** This sample code is not optimized to use any sort of frustum culling, but you should include this feature in your app.</span></span>

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

<span data-ttu-id="1407d-238">Les panneaux individuels sont responsables de configuration de la mémoire tampon de vertex et d’index, le stride et la mémoire tampon constante de transformation de modèle.</span><span class="sxs-lookup"><span data-stu-id="1407d-238">The individual meshes are responsible for setting up the vertex and index buffer, stride, and model transform constant buffer.</span></span> <span data-ttu-id="1407d-239">Comme avec le cube en rotation dans le modèle d’application Windows HOLOGRAPHIQUE, nous affichons dans les mémoires tampons STÉRÉOSCOPIQUES à l’aide de l’instanciation.</span><span class="sxs-lookup"><span data-stu-id="1407d-239">As with the spinning cube in the Windows Holographic app template, we render to stereoscopic buffers using instancing.</span></span>

<span data-ttu-id="1407d-240">À partir de **SurfaceMesh::Draw**:</span><span class="sxs-lookup"><span data-stu-id="1407d-240">From **SurfaceMesh::Draw**:</span></span>

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

### <a name="rendering-choices-with-surface-mapping"></a><span data-ttu-id="1407d-241">Choix de rendu avec Surface de mappage</span><span class="sxs-lookup"><span data-stu-id="1407d-241">Rendering choices with Surface Mapping</span></span>

<span data-ttu-id="1407d-242">L’exemple de code de mappage de Surface offre un code de rendu occlusion uniquement des données de la maille superficielle et de rendu à l’écran de données de la maille superficielle.</span><span class="sxs-lookup"><span data-stu-id="1407d-242">The Surface Mapping code sample offers code for occlusion-only rendering of surface mesh data, and for on-screen rendering of surface mesh data.</span></span> <span data-ttu-id="1407d-243">Le chemin d’accès que vous choisissez - ou les deux - dépendent de votre application.</span><span class="sxs-lookup"><span data-stu-id="1407d-243">Which path you choose - or both - depends on your application.</span></span> <span data-ttu-id="1407d-244">Nous allons étudier les deux configurations dans ce document.</span><span class="sxs-lookup"><span data-stu-id="1407d-244">We'll walk through both configurations in this document.</span></span>

<span data-ttu-id="1407d-245">**Rendu des mémoires tampons d’occlusion pour effet HOLOGRAPHIQUE**</span><span class="sxs-lookup"><span data-stu-id="1407d-245">**Rendering occlusion buffers for holographic effect**</span></span>

<span data-ttu-id="1407d-246">Démarrez en désactivant la vue de cible de rendu pour la caméra virtuelle en cours.</span><span class="sxs-lookup"><span data-stu-id="1407d-246">Start by clearing the render target view for the current virtual camera.</span></span>

<span data-ttu-id="1407d-247">À partir de AppMain.cpp :</span><span class="sxs-lookup"><span data-stu-id="1407d-247">From AppMain.cpp:</span></span>

```cpp
context->ClearRenderTargetView(pCameraResources->GetBackBufferRenderTargetView(), DirectX::Colors::Transparent);
```

<span data-ttu-id="1407d-248">Il s’agit d’une passe de « préaffichage ».</span><span class="sxs-lookup"><span data-stu-id="1407d-248">This is a "pre-rendering" pass.</span></span> <span data-ttu-id="1407d-249">Ici, nous créons une mémoire tampon d’occlusion en demandant le convertisseur de maillage pour restituer la profondeur uniquement.</span><span class="sxs-lookup"><span data-stu-id="1407d-249">Here, we create an occlusion buffer by asking the mesh renderer to render only depth.</span></span> <span data-ttu-id="1407d-250">Dans cette configuration, nous ne pas attacher une vue de cible de rendu et le convertisseur de maillage définit l’étape du nuanceur de pixels **nullptr** afin que le GPU ne cherche pas à dessiner les pixels.</span><span class="sxs-lookup"><span data-stu-id="1407d-250">In this configuration, we don't attach a render target view, and the mesh renderer sets the pixel shader stage to **nullptr** so that the GPU doesn't bother to draw pixels.</span></span> <span data-ttu-id="1407d-251">La géométrie sera rastérisé vers la mémoire tampon de profondeur, et le pipeline graphique s’y arrête.</span><span class="sxs-lookup"><span data-stu-id="1407d-251">The geometry will be rasterized to the depth buffer, and the graphics pipeline will stop there.</span></span>

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

<span data-ttu-id="1407d-252">Nous pouvons dessiner hologrammes avec un test de profondeur supplémentaire par rapport à la mémoire tampon occlusion de Surface de mappage.</span><span class="sxs-lookup"><span data-stu-id="1407d-252">We can draw holograms with an extra depth test against the Surface Mapping occlusion buffer.</span></span> <span data-ttu-id="1407d-253">Dans cet exemple de code, nous affichons pixels sur le cube une couleur différente si elles se trouvent derrière une surface.</span><span class="sxs-lookup"><span data-stu-id="1407d-253">In this code sample, we render pixels on the cube a different color if they are behind a surface.</span></span>

<span data-ttu-id="1407d-254">À partir de AppMain.cpp :</span><span class="sxs-lookup"><span data-stu-id="1407d-254">From AppMain.cpp:</span></span>

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

<span data-ttu-id="1407d-255">Basé sur le code de SpecialEffectPixelShader.hlsl :</span><span class="sxs-lookup"><span data-stu-id="1407d-255">Based on code from SpecialEffectPixelShader.hlsl:</span></span>

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

<span data-ttu-id="1407d-256">**Remarque :** Pour notre **GatherDepthLess** routine, consultez l’exemple de code de mappage de la Surface : SpecialEffectPixelShader.hlsl.</span><span class="sxs-lookup"><span data-stu-id="1407d-256">**Note:** For our **GatherDepthLess** routine, see the Surface Mapping code sample: SpecialEffectPixelShader.hlsl.</span></span>

<span data-ttu-id="1407d-257">**Données de maillage de la surface de rendu à l’affichage**</span><span class="sxs-lookup"><span data-stu-id="1407d-257">**Rendering surface mesh data to the display**</span></span>

<span data-ttu-id="1407d-258">Nous pouvons aussi simplement tirer les maillages de surface d’exposition pour les mémoires tampons d’affichage stéréo.</span><span class="sxs-lookup"><span data-stu-id="1407d-258">We can also just draw the surface meshes to the stereo display buffers.</span></span> <span data-ttu-id="1407d-259">Nous avons choisi de dessiner des visages complètes avec éclairage, mais vous êtes libre de dessiner filaire, traiter des mailles avant le rendu, appliquer un mappage de texture et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="1407d-259">We chose to draw full faces with lighting, but you're free to draw wireframe, process meshes before rendering, apply a texture map, and so on.</span></span>

<span data-ttu-id="1407d-260">Ici, notre exemple de code indique le convertisseur de maillage pour dessiner la collection.</span><span class="sxs-lookup"><span data-stu-id="1407d-260">Here, our code sample tells the mesh renderer to draw the collection.</span></span> <span data-ttu-id="1407d-261">Cette fois nous ne spécifions pas une passe de profondeur uniquement, afin de s’attacher un nuanceur de pixels et terminer le pipeline de rendu à l’aide de cibles que nous avons spécifié pour la caméra virtuelle en cours.</span><span class="sxs-lookup"><span data-stu-id="1407d-261">This time we don't specify a depth-only pass, so it will attach a pixel shader and complete the rendering pipeline using the targets that we specified for the current virtual camera.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="1407d-262">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1407d-262">See also</span></span>
* [<span data-ttu-id="1407d-263">Création d’un projet de DirectX HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="1407d-263">Creating a holographic DirectX project</span></span>](creating-a-holographic-directx-project.md)
* [<span data-ttu-id="1407d-264">Windows.Perception.Spatial API</span><span class="sxs-lookup"><span data-stu-id="1407d-264">Windows.Perception.Spatial API</span></span>](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.aspx)
