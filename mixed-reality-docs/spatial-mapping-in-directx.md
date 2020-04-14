---
title: Mappage spatial dans DirectX
description: Explique comment implémenter le mappage spatial dans votre application DirectX. Cela inclut une explication détaillée de l’exemple d’application de mappage spatial qui est inclus avec le kit de développement logiciel (SDK) plateforme Windows universelle.
author: mikeriches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, mappage spatial, environnement, interaction, DirectX, WinRT, API, exemple de code, UWP, SDK, procédure pas à pas
ms.openlocfilehash: b3ef74a7e11e0e73fce47e4c7193ace42ffe7c20
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81277497"
---
# <a name="spatial-mapping-in-directx"></a><span data-ttu-id="753ee-105">Mappage spatial dans DirectX</span><span class="sxs-lookup"><span data-stu-id="753ee-105">Spatial mapping in DirectX</span></span>

<span data-ttu-id="753ee-106">Cette rubrique explique comment implémenter le [mappage spatial](spatial-mapping.md) dans votre application DirectX.</span><span class="sxs-lookup"><span data-stu-id="753ee-106">This topic describes how to implement [spatial mapping](spatial-mapping.md) in your DirectX app.</span></span> <span data-ttu-id="753ee-107">Cela inclut une explication détaillée de l’exemple d’application de mappage spatial qui est inclus avec le kit de développement logiciel (SDK) plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="753ee-107">This includes a detailed explanation of the spatial mapping sample application that is included with the Universal Windows Platform SDK.</span></span>

<span data-ttu-id="753ee-108">Cette rubrique utilise le code de l’exemple de code UWP [HolographicSpatialMapping](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) .</span><span class="sxs-lookup"><span data-stu-id="753ee-108">This topic uses code from the [HolographicSpatialMapping](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) UWP code sample.</span></span>

>[!NOTE]
><span data-ttu-id="753ee-109">Les extraits de code de cet article illustrent actuellement l' C++utilisation de/CX plutôt que de C++/WinRT conforme C + +17, comme utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="753ee-109">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="753ee-110">Les concepts sont équivalents pour C++un projet/WinRT, bien que vous deviez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="753ee-110">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

## <a name="device-support"></a><span data-ttu-id="753ee-111">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="753ee-111">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="753ee-112"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="753ee-112"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="753ee-113"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="753ee-113"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="753ee-114"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="753ee-114"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="753ee-115"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="753ee-115"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="753ee-116">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="753ee-116">Spatial mapping</span></span></td>
        <td><span data-ttu-id="753ee-117">✔️</span><span class="sxs-lookup"><span data-stu-id="753ee-117">✔️</span></span></td>
        <td><span data-ttu-id="753ee-118">✔️</span><span class="sxs-lookup"><span data-stu-id="753ee-118">✔️</span></span></td>
        <td>❌</td>
    </tr>
</table>

## <a name="directx-development-overview"></a><span data-ttu-id="753ee-119">Vue d’ensemble du développement DirectX</span><span class="sxs-lookup"><span data-stu-id="753ee-119">DirectX development overview</span></span>

<span data-ttu-id="753ee-120">Le développement d’applications natives pour le mappage spatial utilise les API sous l’espace de noms [Windows. perception. spatial](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.aspx) .</span><span class="sxs-lookup"><span data-stu-id="753ee-120">Native application development for spatial mapping uses the APIs under the [Windows.Perception.Spatial](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.aspx) namespace.</span></span> <span data-ttu-id="753ee-121">Ces API offrent un contrôle total de la fonctionnalité de mappage spatial, de manière directement analogue aux API de mappage spatial exposées par [Unity](spatial-mapping-in-unity.md).</span><span class="sxs-lookup"><span data-stu-id="753ee-121">These APIs provide full control of spatial mapping functionality, in a manner directly analogous to the spatial mapping APIs exposed by [Unity](spatial-mapping-in-unity.md).</span></span>

### <a name="perception-apis"></a><span data-ttu-id="753ee-122">API perception</span><span class="sxs-lookup"><span data-stu-id="753ee-122">Perception APIs</span></span>

<span data-ttu-id="753ee-123">Les types principaux fournis pour le développement de mappages spatiaux sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="753ee-123">The primary types provided for spatial mapping development are as follows:</span></span>
* <span data-ttu-id="753ee-124">[SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) fournit des informations sur les surfaces dans les régions d’espace spécifiées à l’application près de l’utilisateur, sous la forme d’objets SpatialSurfaceInfo.</span><span class="sxs-lookup"><span data-stu-id="753ee-124">[SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) provides information about surfaces in application-specified regions of space near the user, in the form of SpatialSurfaceInfo objects.</span></span>
* <span data-ttu-id="753ee-125">[SpatialSurfaceInfo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.aspx) décrit une seule surface spatiale, y compris un ID unique, le volume de limite et l’heure de la dernière modification.</span><span class="sxs-lookup"><span data-stu-id="753ee-125">[SpatialSurfaceInfo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.aspx) describes a single extant spatial surface, including a unique ID, bounding volume and time of last change.</span></span> <span data-ttu-id="753ee-126">Il fournira un SpatialSurfaceMesh de façon asynchrone sur demande.</span><span class="sxs-lookup"><span data-stu-id="753ee-126">It will provide a SpatialSurfaceMesh asynchronously upon request.</span></span>
* <span data-ttu-id="753ee-127">[SpatialSurfaceMeshOptions](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemeshoptions.aspx) contient les paramètres utilisés pour personnaliser les objets SpatialSurfaceMesh demandés à partir de SpatialSurfaceInfo.</span><span class="sxs-lookup"><span data-stu-id="753ee-127">[SpatialSurfaceMeshOptions](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemeshoptions.aspx) contains parameters used to customize the SpatialSurfaceMesh objects requested from SpatialSurfaceInfo.</span></span>
* <span data-ttu-id="753ee-128">[SpatialSurfaceMesh](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.aspx) représente les données de maillage pour une surface spatiale unique.</span><span class="sxs-lookup"><span data-stu-id="753ee-128">[SpatialSurfaceMesh](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.aspx) represents the mesh data for a single spatial surface.</span></span> <span data-ttu-id="753ee-129">Les données pour les positions de vertex, les normales de vertex et les index de triangle sont contenues dans les objets SpatialSurfaceMeshBuffer membres.</span><span class="sxs-lookup"><span data-stu-id="753ee-129">The data for vertex positions, vertex normals and triangle indices is contained in member SpatialSurfaceMeshBuffer objects.</span></span>
* <span data-ttu-id="753ee-130">[SpatialSurfaceMeshBuffer](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemeshbuffer.aspx) encapsule un seul type de données de maillage.</span><span class="sxs-lookup"><span data-stu-id="753ee-130">[SpatialSurfaceMeshBuffer](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemeshbuffer.aspx) wraps a single type of mesh data.</span></span>

<span data-ttu-id="753ee-131">Lors du développement d’une application à l’aide de ces API, le déroulement de votre programme de base ressemblera à ce qui suit (comme illustré dans l’exemple d’application décrit ci-dessous) :</span><span class="sxs-lookup"><span data-stu-id="753ee-131">When developing an application using these APIs, your basic program flow will look like this (as demonstrated in the sample application described below):</span></span>
- <span data-ttu-id="753ee-132">**Configurer votre SpatialSurfaceObserver**</span><span class="sxs-lookup"><span data-stu-id="753ee-132">**Set up your SpatialSurfaceObserver**</span></span>
  - <span data-ttu-id="753ee-133">Appelez [RequestAccessAsync](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.requestaccessasync.aspx)pour vous assurer que l’utilisateur a l’autorisation nécessaire pour que votre application utilise les fonctionnalités de mappage spatiale de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="753ee-133">Call [RequestAccessAsync](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.requestaccessasync.aspx), to ensure that the user has given permission for your application to use the device's spatial mapping capabilities.</span></span>
  - <span data-ttu-id="753ee-134">Instanciez un objet SpatialSurfaceObserver.</span><span class="sxs-lookup"><span data-stu-id="753ee-134">Instantiate a SpatialSurfaceObserver object.</span></span>
  - <span data-ttu-id="753ee-135">Appelez [SetBoundingVolumes](https://msdn.microsoft.com/library/windows/apps/mt592747.aspx) pour spécifier les régions d’espace dans lesquelles vous souhaitez obtenir des informations sur les surfaces spatiales.</span><span class="sxs-lookup"><span data-stu-id="753ee-135">Call [SetBoundingVolumes](https://msdn.microsoft.com/library/windows/apps/mt592747.aspx) to specify the regions of space in which you want information about spatial surfaces.</span></span> <span data-ttu-id="753ee-136">Vous pouvez modifier ces régions à l’avenir en appelant à nouveau cette fonction.</span><span class="sxs-lookup"><span data-stu-id="753ee-136">You may modify these regions in the future by simply calling this function again.</span></span> <span data-ttu-id="753ee-137">Chaque région est spécifiée à l’aide d’un [SpatialBoundingVolume](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialboundingvolume.aspx).</span><span class="sxs-lookup"><span data-stu-id="753ee-137">Each region is specified using a [SpatialBoundingVolume](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialboundingvolume.aspx).</span></span>
  - <span data-ttu-id="753ee-138">Inscrivez-vous à l’événement [ObservedSurfacesChanged](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.observedsurfaceschanged.aspx) , qui se déclenche chaque fois que de nouvelles informations sont disponibles sur les surfaces spatiales dans les régions d’espace que vous avez spécifiées.</span><span class="sxs-lookup"><span data-stu-id="753ee-138">Register for the [ObservedSurfacesChanged](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.observedsurfaceschanged.aspx) event, which will fire whenever new information is available about the spatial surfaces in the regions of space you have specified.</span></span>
- <span data-ttu-id="753ee-139">**Traiter les événements ObservedSurfacesChanged**</span><span class="sxs-lookup"><span data-stu-id="753ee-139">**Process ObservedSurfacesChanged events**</span></span>
  - <span data-ttu-id="753ee-140">Dans votre gestionnaire d’événements, appelez [GetObservedSurfaces](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.getobservedsurfaces.aspx) pour recevoir un mappage d’objets SpatialSurfaceInfo.</span><span class="sxs-lookup"><span data-stu-id="753ee-140">In your event handler, call [GetObservedSurfaces](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.getobservedsurfaces.aspx) to receive a map of SpatialSurfaceInfo objects.</span></span> <span data-ttu-id="753ee-141">À l’aide de cette carte, vous pouvez mettre à jour vos enregistrements dont les surfaces spatiales [existent dans l’environnement de l’utilisateur](spatial-mapping.md#mesh-caching).</span><span class="sxs-lookup"><span data-stu-id="753ee-141">Using this map, you can update your records of which spatial surfaces [exist in the user's environment](spatial-mapping.md#mesh-caching).</span></span>
  - <span data-ttu-id="753ee-142">Pour chaque objet SpatialSurfaceInfo, vous pouvez interroger [TryGetBounds](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.trygetbounds.aspx) pour déterminer les étendues spatiales de la surface, exprimées dans un [système de coordonnées spatiales](coordinate-systems.md) de votre choix.</span><span class="sxs-lookup"><span data-stu-id="753ee-142">For each SpatialSurfaceInfo object, you may query [TryGetBounds](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.trygetbounds.aspx) to determine the spatial extents of the surface, expressed in a [spatial coordinate system](coordinate-systems.md) of your choosing.</span></span>
  - <span data-ttu-id="753ee-143">Si vous décidez de demander un maillage pour une surface spatiale, appelez [TryComputeLatestMeshAsync](https://msdn.microsoft.com/library/windows/apps/mt592715.aspx).</span><span class="sxs-lookup"><span data-stu-id="753ee-143">If you decide to request mesh for a spatial surface, call [TryComputeLatestMeshAsync](https://msdn.microsoft.com/library/windows/apps/mt592715.aspx).</span></span> <span data-ttu-id="753ee-144">Vous pouvez fournir des options spécifiant la densité souhaitée des triangles et le format des données de maillage retournées.</span><span class="sxs-lookup"><span data-stu-id="753ee-144">You may provide options specifying the desired density of triangles, and the format of the returned mesh data.</span></span>
- <span data-ttu-id="753ee-145">**Recevoir et traiter le maillage**</span><span class="sxs-lookup"><span data-stu-id="753ee-145">**Receive and process mesh**</span></span>
  - <span data-ttu-id="753ee-146">Chaque appel à TryComputeLatestMeshAsync va aysnchronously retourner un objet SpatialSurfaceMesh.</span><span class="sxs-lookup"><span data-stu-id="753ee-146">Each call to TryComputeLatestMeshAsync will aysnchronously return one SpatialSurfaceMesh object.</span></span>
  - <span data-ttu-id="753ee-147">À partir de cet objet, vous pouvez accéder aux objets SpatialSurfaceMeshBuffer contenus pour accéder aux index de triangle, aux positions de vertex et (le cas échéant) aux normales des sommets de la maille.</span><span class="sxs-lookup"><span data-stu-id="753ee-147">From this object you can access the contained SpatialSurfaceMeshBuffer objects in order to access the triangle indices, vertex positions and (if requested) vertex normals of the mesh.</span></span> <span data-ttu-id="753ee-148">Ces données seront dans un format directement compatible avec les [API Direct3D 11](https://msdn.microsoft.com/library/windows/desktop/ff476501(v=vs.85).aspx) utilisées pour le rendu des maillages.</span><span class="sxs-lookup"><span data-stu-id="753ee-148">This data will be in a format directly compatible with the [Direct3D 11 APIs](https://msdn.microsoft.com/library/windows/desktop/ff476501(v=vs.85).aspx) used for rendering meshes.</span></span>
  - <span data-ttu-id="753ee-149">À partir de là, votre application peut éventuellement effectuer l’analyse ou le [traitement](spatial-mapping.md#mesh-processing) des données de maillage, et les utiliser pour le [rendu](spatial-mapping.md#rendering) et la [Raycasting physique et les collisions](spatial-mapping.md#raycasting-and-collision).</span><span class="sxs-lookup"><span data-stu-id="753ee-149">From here your application can optionally perform analysis or [processing](spatial-mapping.md#mesh-processing) of the mesh data, and use it for [rendering](spatial-mapping.md#rendering) and physics [raycasting and collision](spatial-mapping.md#raycasting-and-collision).</span></span>
  - <span data-ttu-id="753ee-150">Un détail important à noter est que vous devez appliquer une mise à l’échelle aux positions de vertex de maillage (par exemple, dans le nuanceur de sommets utilisé pour le rendu des maillages), pour les convertir des unités entières optimisées dans lesquelles elles sont stockées dans la mémoire tampon, en mètres.</span><span class="sxs-lookup"><span data-stu-id="753ee-150">One important detail to note is that you must apply a scale to the mesh vertex positions (for example in the vertex shader used for rendering the meshes), to convert them from the optimized integer units in which they are stored in the buffer, to meters.</span></span> <span data-ttu-id="753ee-151">Vous pouvez récupérer cette échelle en appelant [VertexPositionScale](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.vertexpositionscale.aspx).</span><span class="sxs-lookup"><span data-stu-id="753ee-151">You can retrieve this scale by calling [VertexPositionScale](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.vertexpositionscale.aspx).</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="753ee-152">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="753ee-152">Troubleshooting</span></span>
* <span data-ttu-id="753ee-153">N’oubliez pas de mettre à l’échelle les positions de vertex de maillage dans votre nuanceur de sommets, à l’aide de l’échelle retournée par [SpatialSurfaceMesh. VertexPositionScale](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.vertexpositionscale.aspx)</span><span class="sxs-lookup"><span data-stu-id="753ee-153">Don't forget to scale mesh vertex positions in your vertex shader, using the scale returned by [SpatialSurfaceMesh.VertexPositionScale](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.vertexpositionscale.aspx)</span></span>

## <a name="spatial-mapping-code-sample-walkthrough"></a><span data-ttu-id="753ee-154">Exemple de code de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="753ee-154">Spatial Mapping code sample walkthrough</span></span>

<span data-ttu-id="753ee-155">L’exemple de code de [mappage spatial holographique](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) inclut du code que vous pouvez utiliser pour commencer à charger des maillages superficiels dans votre application, y compris l’infrastructure de gestion et de rendu des maillages d’aire.</span><span class="sxs-lookup"><span data-stu-id="753ee-155">The [Holographic Spatial Mapping](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) code sample includes code that you can use to get started loading surface meshes into your app, including infrastructure for managing and rendering surface meshes.</span></span>

<span data-ttu-id="753ee-156">À présent, nous allons vous montrer comment ajouter la fonctionnalité de mappage de surface à votre application DirectX.</span><span class="sxs-lookup"><span data-stu-id="753ee-156">Now, we walk through how to add surface mapping capability to your DirectX app.</span></span> <span data-ttu-id="753ee-157">Vous pouvez ajouter ce code à votre projet de [modèle d’application holographique Windows](creating-a-holographic-directx-project.md) , ou vous pouvez suivre la procédure en parcourant l’exemple de code mentionné ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="753ee-157">You can add this code to your [Windows Holographic app template](creating-a-holographic-directx-project.md) project, or you can follow along by browsing through the code sample mentioned above.</span></span> <span data-ttu-id="753ee-158">Cet exemple de code est basé sur le modèle d’application holographique Windows.</span><span class="sxs-lookup"><span data-stu-id="753ee-158">This code sample is based on the Windows Holographic app template.</span></span>

### <a name="set-up-your-app-to-use-the-spatialperception-capability"></a><span data-ttu-id="753ee-159">Configurer votre application pour utiliser la fonctionnalité spatialPerception</span><span class="sxs-lookup"><span data-stu-id="753ee-159">Set up your app to use the spatialPerception capability</span></span>

<span data-ttu-id="753ee-160">Votre application doit être en mesure d’utiliser la fonctionnalité de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="753ee-160">Your app must be able to use the spatial mapping capability.</span></span> <span data-ttu-id="753ee-161">Cela est nécessaire, car le maillage spatial est une représentation de l’environnement de l’utilisateur, qui peut être considérée comme des données privées.</span><span class="sxs-lookup"><span data-stu-id="753ee-161">This is necessary because the spatial mesh is a representation of the user's environment, which may be considered private data.</span></span> <span data-ttu-id="753ee-162">Déclarez cette fonctionnalité dans le fichier Package. appxmanifest pour votre application.</span><span class="sxs-lookup"><span data-stu-id="753ee-162">Declare this capability in the package.appxmanifest file for your app.</span></span> <span data-ttu-id="753ee-163">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="753ee-163">Here's an example:</span></span>

```xml
<Capabilities>
  <uap2:Capability Name="spatialPerception" />
</Capabilities>
```

<span data-ttu-id="753ee-164">La fonctionnalité provient de l’espace de noms **UAP2** .</span><span class="sxs-lookup"><span data-stu-id="753ee-164">The capability comes from the **uap2** namespace.</span></span> <span data-ttu-id="753ee-165">Pour accéder à cet espace de noms dans votre manifeste, incluez-le en tant qu’attribut *xlmns* dans l’élément &lt;> Package.</span><span class="sxs-lookup"><span data-stu-id="753ee-165">To get access to this namespace in your manifest, include it as an *xlmns* attribute in the &lt;Package> element.</span></span> <span data-ttu-id="753ee-166">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="753ee-166">Here's an example:</span></span>

```xml
<Package
    xmlns="https://schemas.microsoft.com/appx/manifest/foundation/windows10"
    xmlns:mp="https://schemas.microsoft.com/appx/2014/phone/manifest"
    xmlns:uap="https://schemas.microsoft.com/appx/manifest/uap/windows10"
    xmlns:uap2="https://schemas.microsoft.com/appx/manifest/uap/windows10/2"
    IgnorableNamespaces="uap uap2 mp"
    >
```

### <a name="check-for-spatial-mapping-feature-support"></a><span data-ttu-id="753ee-167">Vérifier la prise en charge de la fonctionnalité de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="753ee-167">Check for spatial mapping feature support</span></span>

<span data-ttu-id="753ee-168">Windows Mixed Reality prend en charge un large éventail d’appareils, notamment les appareils qui ne prennent pas en charge le mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="753ee-168">Windows Mixed Reality supports a wide range of devices, including devices which do not support spatial mapping.</span></span> <span data-ttu-id="753ee-169">Si votre application peut utiliser le mappage spatial, ou si elle doit utiliser le mappage spatial, pour fournir des fonctionnalités, elle doit s’assurer que le mappage spatial est pris en charge avant d’essayer de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="753ee-169">If your app can use spatial mapping, or must use spatial mapping, to provide functionality, it should check to make sure that spatial mapping is supported before trying to use it.</span></span> <span data-ttu-id="753ee-170">Par exemple, si le mappage spatial est requis par votre application de réalité mixte, elle doit afficher un message à cet effet si un utilisateur tente de l’exécuter sur un appareil sans mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="753ee-170">For example, if spatial mapping is required by your mixed reality app, it should display a message to that effect if a user tries running it on a device without spatial mapping.</span></span> <span data-ttu-id="753ee-171">Ou bien, votre application peut être en mesure d’effectuer le rendu de son propre environnement virtuel à la place de l’environnement de l’utilisateur, en fournissant une expérience similaire à ce qui se passerait si le mappage spatial était disponible.</span><span class="sxs-lookup"><span data-stu-id="753ee-171">Or, your app may be able to render its own virtual environment in place of the user's environment, providing an experience that is similar to what would happen if spatial mapping were available.</span></span> <span data-ttu-id="753ee-172">Dans tous les cas, cette API permet à votre application de savoir quand elle n’obtiendra pas de données de mappage spatiales et de répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="753ee-172">In any event, this API allows your app to be aware of when it will not get spatial mapping data and respond in the appropriate way.</span></span>

<span data-ttu-id="753ee-173">Pour vérifier la prise en charge du mappage spatial sur l’appareil actuel, assurez-vous d’abord que le contrat UWP est au niveau 4 ou supérieur, puis appelez SpatialSurfaceObserver :: IsSupported ().</span><span class="sxs-lookup"><span data-stu-id="753ee-173">To check the current device for spatial mapping support, first make sure the UWP contract is at level 4 or greater and then call SpatialSurfaceObserver::IsSupported().</span></span> <span data-ttu-id="753ee-174">Voici comment procéder dans le contexte de l’exemple de code de [mappage spatial holographique](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) .</span><span class="sxs-lookup"><span data-stu-id="753ee-174">Here's how to do so in the context of the [Holographic Spatial Mapping](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicSpatialMapping) code sample.</span></span> <span data-ttu-id="753ee-175">La prise en charge est vérifiée juste avant de demander l’accès.</span><span class="sxs-lookup"><span data-stu-id="753ee-175">Support is checked just before requesting access.</span></span>

<span data-ttu-id="753ee-176">L’API SpatialSurfaceObserver :: IsSupported () est disponible à partir de la version 15063 du kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="753ee-176">The SpatialSurfaceObserver::IsSupported() API is available starting in SDK version 15063.</span></span> <span data-ttu-id="753ee-177">Si nécessaire, reciblez votre projet vers la version 15063 de la plateforme avant d’utiliser cette API.</span><span class="sxs-lookup"><span data-stu-id="753ee-177">If necessary, retarget your project to platform version 15063 before using this API.</span></span>

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

<span data-ttu-id="753ee-178">Notez que lorsque le contrat UWP est inférieur au niveau 4, l’application doit s’exécuter comme si l’appareil est capable d’effectuer un mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="753ee-178">Note that when the UWP contract is less than level 4, the app should proceed as though the device is capable of doing spatial mapping.</span></span>

### <a name="request-access-to-spatial-mapping-data"></a><span data-ttu-id="753ee-179">Demander l’accès aux données de mappage spatiale</span><span class="sxs-lookup"><span data-stu-id="753ee-179">Request access to spatial mapping data</span></span>

<span data-ttu-id="753ee-180">Votre application doit demander l’autorisation d’accéder aux données de mappage spatiale avant d’essayer de créer des observateurs de surface.</span><span class="sxs-lookup"><span data-stu-id="753ee-180">Your app needs to request permission to access spatial mapping data before trying to create any surface observers.</span></span> <span data-ttu-id="753ee-181">Voici un exemple basé sur notre exemple de code de mappage de surface, avec plus de détails fournis plus loin dans cette page :</span><span class="sxs-lookup"><span data-stu-id="753ee-181">Here's an example based upon our Surface Mapping code sample, with more details provided later on this page:</span></span>

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

### <a name="create-a-surface-observer"></a><span data-ttu-id="753ee-182">Créer un observateur de surface</span><span class="sxs-lookup"><span data-stu-id="753ee-182">Create a surface observer</span></span>

<span data-ttu-id="753ee-183">L’espace de noms **Windows ::P erception :: spatial :: surfaces** comprend la classe [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) , qui observe un ou plusieurs volumes que vous spécifiez dans un [SpatialCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.aspx).</span><span class="sxs-lookup"><span data-stu-id="753ee-183">The **Windows::Perception::Spatial::Surfaces** namespace includes the [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) class, which observes one or more volumes that you specify in a [SpatialCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.aspx).</span></span> <span data-ttu-id="753ee-184">Utilisez une instance [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) pour accéder aux données de maillage des surfaces en temps réel.</span><span class="sxs-lookup"><span data-stu-id="753ee-184">Use a [SpatialSurfaceObserver](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceobserver.aspx) instance to access surface mesh data in real time.</span></span>

<span data-ttu-id="753ee-185">À partir de **AppMain. h**:</span><span class="sxs-lookup"><span data-stu-id="753ee-185">From **AppMain.h**:</span></span>

```cpp
// Obtains surface mapping data from the device in real time.
Windows::Perception::Spatial::Surfaces::SpatialSurfaceObserver^     m_surfaceObserver;
Windows::Perception::Spatial::Surfaces::SpatialSurfaceMeshOptions^  m_surfaceMeshOptions;
```

<span data-ttu-id="753ee-186">Comme indiqué dans la section précédente, vous devez demander l’accès aux données de mappage spatiale pour que votre application puisse l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="753ee-186">As noted in the previous section, you must request access to spatial mapping data before your app can use it.</span></span> <span data-ttu-id="753ee-187">Cet accès est accordé automatiquement sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="753ee-187">This access is granted automatically on the HoloLens.</span></span>

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

<span data-ttu-id="753ee-188">Ensuite, vous devez configurer l’observateur de surface pour observer un volume de limite spécifique.</span><span class="sxs-lookup"><span data-stu-id="753ee-188">Next, you need to configure the surface observer to observe a specific bounding volume.</span></span> <span data-ttu-id="753ee-189">Ici, nous observons une boîte qui est 20x20x5 mètres, centrée sur l’origine du système de coordonnées.</span><span class="sxs-lookup"><span data-stu-id="753ee-189">Here, we observe a box that is 20x20x5 meters, centered at the origin of the coordinate system.</span></span>

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

<span data-ttu-id="753ee-190">Notez que vous pouvez définir plusieurs volumes englobants à la place.</span><span class="sxs-lookup"><span data-stu-id="753ee-190">Note that you can set multiple bounding volumes instead.</span></span>

<span data-ttu-id="753ee-191">*Il s’agit du pseudo-code :*</span><span class="sxs-lookup"><span data-stu-id="753ee-191">*This is pseudocode:*</span></span>

```cpp
m_surfaceObserver->SetBoundingVolumes(/* iterable collection of bounding volumes*/);
```

<span data-ttu-id="753ee-192">Il est également possible d’utiliser d’autres formes englobantes, telles qu’une vue frustum, ou un rectangle englobant qui n’est pas aligné sur l’axe.</span><span class="sxs-lookup"><span data-stu-id="753ee-192">It is also possible to use other bounding shapes - such as a view frustum, or a bounding box that is not axis aligned.</span></span>

<span data-ttu-id="753ee-193">*Il s’agit du pseudo-code :*</span><span class="sxs-lookup"><span data-stu-id="753ee-193">*This is pseudocode:*</span></span>

```cpp
m_surfaceObserver->SetBoundingVolume(
            SpatialBoundingVolume::FromFrustum(/*SpatialCoordinateSystem*/, /*SpatialBoundingFrustum*/)
            );
```

<span data-ttu-id="753ee-194">Si votre application doit effectuer une opération différente quand les données de mappage des surfaces ne sont pas disponibles, vous pouvez écrire du code pour répondre au cas où le [SpatialPerceptionAccessStatus](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialperceptionaccessstatus.aspx) n’est pas **autorisé** . par exemple, il ne sera pas autorisé sur les PC avec des appareils immersifs connectés, car ces appareils n’ont pas de matériel pour le mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="753ee-194">If your app needs to do anything differently when surface mapping data is not available, you can write code to respond to the case where the [SpatialPerceptionAccessStatus](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialperceptionaccessstatus.aspx) is not **Allowed** - for example, it will not be allowed on PCs with immersive devices attached because those devices don't have hardware for spatial mapping.</span></span> <span data-ttu-id="753ee-195">Pour ces appareils, vous devez plutôt compter sur la phase spatiale pour obtenir des informations sur l’environnement et la configuration de l’appareil de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="753ee-195">For these devices, you should instead rely on the spatial stage for information about the user's environment and device configuration.</span></span>

### <a name="initialize-and-update-the-surface-mesh-collection"></a><span data-ttu-id="753ee-196">Initialiser et mettre à jour la collection de maillages d’aire</span><span class="sxs-lookup"><span data-stu-id="753ee-196">Initialize and update the surface mesh collection</span></span>

<span data-ttu-id="753ee-197">Si l’observateur de surface a été créé avec succès, nous pouvons commencer à initialiser notre collection de maillages de surface.</span><span class="sxs-lookup"><span data-stu-id="753ee-197">If the surface observer was successfully created, we can proceed to initialize our surface mesh collection.</span></span> <span data-ttu-id="753ee-198">Ici, nous utilisons l’API du modèle pull pour obtenir immédiatement l’ensemble actuel des surfaces observées :</span><span class="sxs-lookup"><span data-stu-id="753ee-198">Here, we use the pull model API to get the current set of observed surfaces right away:</span></span>

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

<span data-ttu-id="753ee-199">Un modèle d’émission est également disponible pour obtenir des données de maillage de surface.</span><span class="sxs-lookup"><span data-stu-id="753ee-199">There is also a push model available to get surface mesh data.</span></span> <span data-ttu-id="753ee-200">Vous êtes libre de concevoir votre application pour qu’elle utilise uniquement le modèle d’extraction si vous le souhaitez, auquel cas vous interrogez les données chaque fois, par exemple, une fois par cadre, ou pendant une période spécifique, par exemple lors de la configuration du jeu.</span><span class="sxs-lookup"><span data-stu-id="753ee-200">You are free to design your app to use only the pull model if you choose, in which case you'll poll for data every so often - say, once per frame - or during a specific time period, such as during game setup.</span></span> <span data-ttu-id="753ee-201">Si c’est le cas, le code ci-dessus est ce dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="753ee-201">If so, the above code is what you need.</span></span>

<span data-ttu-id="753ee-202">Dans notre exemple de code, nous avons choisi d’illustrer l’utilisation des deux modèles à des fins pédagogiques.</span><span class="sxs-lookup"><span data-stu-id="753ee-202">In our code sample, we chose to demonstrate the use of both models for pedagogical purposes.</span></span> <span data-ttu-id="753ee-203">Ici, nous nous abonnons à un événement pour recevoir des données de maillage de surface à jour chaque fois que le système reconnaît une modification.</span><span class="sxs-lookup"><span data-stu-id="753ee-203">Here, we subscribe to an event to receive up-to-date surface mesh data whenever the system recognizes a change.</span></span>

```cpp
m_surfaceObserver->ObservedSurfacesChanged += ref new TypedEventHandler<SpatialSurfaceObserver^, Platform::Object^>(
            bind(&HolographicDesktopAppMain::OnSurfacesChanged, this, _1, _2)
            );
```

<span data-ttu-id="753ee-204">Notre exemple de code est également configuré pour répondre à ces événements.</span><span class="sxs-lookup"><span data-stu-id="753ee-204">Our code sample is also configured to respond to these events.</span></span> <span data-ttu-id="753ee-205">Passons en revue la procédure à suivre.</span><span class="sxs-lookup"><span data-stu-id="753ee-205">Let's walk through how we do this.</span></span>

<span data-ttu-id="753ee-206">**Remarque :** Cela peut ne pas être le moyen le plus efficace pour votre application de gérer les données de maillage.</span><span class="sxs-lookup"><span data-stu-id="753ee-206">**NOTE:** This might not be the most efficient way for your app to handle mesh data.</span></span> <span data-ttu-id="753ee-207">Ce code est écrit par souci de clarté et n’est pas optimisé.</span><span class="sxs-lookup"><span data-stu-id="753ee-207">This code is written for clarity and is not optimized.</span></span>

<span data-ttu-id="753ee-208">Les données de maillage des surfaces sont fournies dans un mappage en lecture seule qui stocke les objets [SpatialSurfaceInfo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.aspx) en utilisant [Platform :: GUID](https://msdn.microsoft.com/library/windows/desktop/aa373931.aspx) comme valeurs de clés.</span><span class="sxs-lookup"><span data-stu-id="753ee-208">The surface mesh data is provided in a read-only map that stores [SpatialSurfaceInfo](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfaceinfo.aspx) objects using [Platform::Guids](https://msdn.microsoft.com/library/windows/desktop/aa373931.aspx) as key values.</span></span>

```cpp
IMapView<Guid, SpatialSurfaceInfo^>^ const& surfaceCollection = sender->GetObservedSurfaces();
```

<span data-ttu-id="753ee-209">Pour traiter ces données, nous examinons d’abord les valeurs de clés qui ne se trouvent pas dans notre collection.</span><span class="sxs-lookup"><span data-stu-id="753ee-209">To process this data, we look first for key values that aren't in our collection.</span></span> <span data-ttu-id="753ee-210">Des informations détaillées sur la façon dont les données sont stockées dans notre exemple d’application seront présentées plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="753ee-210">Details on how the data is stored in our sample app will be presented later in this topic.</span></span>

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

<span data-ttu-id="753ee-211">Nous devons également supprimer les maillages des surfaces qui se trouvent dans notre collection de maillages de surface, mais qui ne se trouvent plus dans la collection système.</span><span class="sxs-lookup"><span data-stu-id="753ee-211">We also have to remove surface meshes that are in our surface mesh collection, but that aren't in the system collection anymore.</span></span> <span data-ttu-id="753ee-212">Pour ce faire, nous devons effectuer une opération similaire à l’inverse de ce que nous venons de montrer pour ajouter et mettre à jour des mailles. Nous effectuons une boucle sur la collection de votre application et vérifions si le **GUID** est présent dans la collection système.</span><span class="sxs-lookup"><span data-stu-id="753ee-212">To do so, we need to do something akin to the opposite of what we just showed for adding and updating meshes; we loop on our app's collection, and check to see if the **Guid** we have is in the system collection.</span></span> <span data-ttu-id="753ee-213">Si elle ne se trouve pas dans le regroupement système, nous la supprimons de la nôtre.</span><span class="sxs-lookup"><span data-stu-id="753ee-213">If it's not in the system collection, we remove it from ours.</span></span>

<span data-ttu-id="753ee-214">À partir de notre gestionnaire d’événements dans AppMain. cpp :</span><span class="sxs-lookup"><span data-stu-id="753ee-214">From our event handler in AppMain.cpp:</span></span>

```cpp
m_meshCollection->PruneMeshCollection(surfaceCollection);
```

<span data-ttu-id="753ee-215">Implémentation du nettoyage de maillage dans RealtimeSurfaceMeshRenderer. cpp :</span><span class="sxs-lookup"><span data-stu-id="753ee-215">The implementation of mesh pruning in RealtimeSurfaceMeshRenderer.cpp:</span></span>

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

### <a name="acquire-and-use-surface-mesh-data-buffers"></a><span data-ttu-id="753ee-216">Acquérir et utiliser des tampons de données de maillage des surfaces</span><span class="sxs-lookup"><span data-stu-id="753ee-216">Acquire and use surface mesh data buffers</span></span>

<span data-ttu-id="753ee-217">L’obtention des informations de maillage des surfaces était aussi simple que l’extraction d’une collection de données et le traitement des mises à jour de cette collection.</span><span class="sxs-lookup"><span data-stu-id="753ee-217">Getting the surface mesh information was as easy as pulling a data collection and processing updates to that collection.</span></span> <span data-ttu-id="753ee-218">Maintenant, nous aborderons en détail la façon dont vous pouvez utiliser les données.</span><span class="sxs-lookup"><span data-stu-id="753ee-218">Now, we'll go into detail on how you can use the data.</span></span>

<span data-ttu-id="753ee-219">Dans notre exemple de code, nous avons choisi d’utiliser les maillages des surfaces pour le rendu.</span><span class="sxs-lookup"><span data-stu-id="753ee-219">In our code example, we chose to use the surface meshes for rendering.</span></span> <span data-ttu-id="753ee-220">Il s’agit d’un scénario courant pour boucher des hologrammes derrière des surfaces réelles.</span><span class="sxs-lookup"><span data-stu-id="753ee-220">This is a common scenario for occluding holograms behind real-world surfaces.</span></span> <span data-ttu-id="753ee-221">Vous pouvez également effectuer le rendu des panneaux ou afficher les versions traitées de ceux-ci pour montrer à l’utilisateur quelles zones de la salle sont analysées avant de commencer à fournir des fonctionnalités d’application ou de jeu.</span><span class="sxs-lookup"><span data-stu-id="753ee-221">You can also render the meshes, or render processed versions of them, to show the user what areas of the room are scanned before you start providing app or game functionality.</span></span>

<span data-ttu-id="753ee-222">L’exemple de code démarre le processus lorsqu’il reçoit des mises à jour de la maille des surfaces du gestionnaire d’événements que nous avons décrit dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="753ee-222">The code sample starts the process when it receives surface mesh updates from the event handler that we described in the previous section.</span></span> <span data-ttu-id="753ee-223">La ligne de code importante dans cette fonction est l’appel permettant de mettre à jour le *maillage*des surfaces : à ce stade, nous avons déjà traité les informations de maillage, et nous sommes sur le point d’obtenir les données de vertex et d’index pour une utilisation comme nous le voyons.</span><span class="sxs-lookup"><span data-stu-id="753ee-223">The important line of code in this function is the call to update the surface *mesh*: by this time we have already processed the mesh info, and we are about to get the vertex and index data for use as we see fit.</span></span>

<span data-ttu-id="753ee-224">À partir de RealtimeSurfaceMeshRenderer. cpp :</span><span class="sxs-lookup"><span data-stu-id="753ee-224">From RealtimeSurfaceMeshRenderer.cpp:</span></span>

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

<span data-ttu-id="753ee-225">Notre exemple de code est conçu de sorte qu’une classe de données, **SurfaceMesh**, gère le traitement et le rendu des données de maillage.</span><span class="sxs-lookup"><span data-stu-id="753ee-225">Our sample code is designed so that a data class, **SurfaceMesh**, handles mesh data processing and rendering.</span></span> <span data-ttu-id="753ee-226">Il s’agit de ce que le **RealtimeSurfaceMeshRenderer** conserve en fait une carte.</span><span class="sxs-lookup"><span data-stu-id="753ee-226">These meshes are what the **RealtimeSurfaceMeshRenderer** actually keeps a map of.</span></span> <span data-ttu-id="753ee-227">Chacune d’elles a une référence à l’SpatialSurfaceMesh d’origine, et nous l’utilisons tout le temps nécessaire pour accéder au vertex de maillage ou aux tampons d’index, ou obtenir une transformation pour la maille.</span><span class="sxs-lookup"><span data-stu-id="753ee-227">Each one has a reference to the SpatialSurfaceMesh it came from, and we use it any time that we need to access the mesh vertex or index buffers, or get a transform for the mesh.</span></span> <span data-ttu-id="753ee-228">Pour le moment, nous signalons le maillage comme nécessitant une mise à jour.</span><span class="sxs-lookup"><span data-stu-id="753ee-228">For now, we flag the mesh as needing an update.</span></span>

<span data-ttu-id="753ee-229">À partir de SurfaceMesh. cpp :</span><span class="sxs-lookup"><span data-stu-id="753ee-229">From SurfaceMesh.cpp:</span></span>

```cpp
void SurfaceMesh::UpdateSurface(SpatialSurfaceMesh^ surfaceMesh)
{
    m_surfaceMesh = surfaceMesh;
    m_updateNeeded = true;
}
```

<span data-ttu-id="753ee-230">La prochaine fois que la maille sera invitée à se dessiner lui-même, elle vérifiera d’abord l’indicateur.</span><span class="sxs-lookup"><span data-stu-id="753ee-230">Next time the mesh is asked to draw itself, it will check the flag first.</span></span> <span data-ttu-id="753ee-231">Si une mise à jour est nécessaire, les mémoires tampons de vertex et d’index seront mises à jour sur le GPU.</span><span class="sxs-lookup"><span data-stu-id="753ee-231">If an update is needed, the vertex and index buffers will be updated on the GPU.</span></span>

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

<span data-ttu-id="753ee-232">Tout d’abord, nous acquérant les tampons de données brutes :</span><span class="sxs-lookup"><span data-stu-id="753ee-232">First, we acquire the raw data buffers:</span></span>

```cpp
Windows::Storage::Streams::IBuffer^ positions = m_surfaceMesh->VertexPositions->Data;
    Windows::Storage::Streams::IBuffer^ normals   = m_surfaceMesh->VertexNormals->Data;
    Windows::Storage::Streams::IBuffer^ indices   = m_surfaceMesh->TriangleIndices->Data;
```

<span data-ttu-id="753ee-233">Ensuite, nous créons des tampons de périphérique Direct3D avec les données de maillage fournies par le HoloLens :</span><span class="sxs-lookup"><span data-stu-id="753ee-233">Then, we create Direct3D device buffers with the mesh data provided by the HoloLens:</span></span>

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

<span data-ttu-id="753ee-234">**Remarque :** Pour la fonction d’assistance CreateDirectXBuffer utilisée dans l’extrait de code précédent, consultez l’exemple de code de mappage des surfaces : SurfaceMesh. cpp, GetDataFromIBuffer. h.</span><span class="sxs-lookup"><span data-stu-id="753ee-234">**NOTE:** For the CreateDirectXBuffer helper function used in the previous snippet, see the Surface Mapping code sample: SurfaceMesh.cpp, GetDataFromIBuffer.h.</span></span> <span data-ttu-id="753ee-235">À présent, la création de la ressource d’appareil est terminée et le maillage est considéré comme étant chargé et prêt pour la mise à jour et le rendu.</span><span class="sxs-lookup"><span data-stu-id="753ee-235">Now the device resource creation is complete, and the mesh is considered to be loaded and ready for update and render.</span></span>

### <a name="update-and-render-surface-meshes"></a><span data-ttu-id="753ee-236">Maillages des surfaces de mise à jour et de rendu</span><span class="sxs-lookup"><span data-stu-id="753ee-236">Update and render surface meshes</span></span>

<span data-ttu-id="753ee-237">Notre classe SurfaceMesh possède une fonction de mise à jour spécialisée.</span><span class="sxs-lookup"><span data-stu-id="753ee-237">Our SurfaceMesh class has a specialized update function.</span></span> <span data-ttu-id="753ee-238">Chaque [SpatialSurfaceMesh](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.aspx) possède sa propre transformation, et notre exemple utilise le système de coordonnées actuel pour notre **SpatialStationaryReferenceFrame** pour acquérir la transformation.</span><span class="sxs-lookup"><span data-stu-id="753ee-238">Each [SpatialSurfaceMesh](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.surfaces.spatialsurfacemesh.aspx) has its own transform, and our sample uses the current coordinate system for our **SpatialStationaryReferenceFrame** to acquire the transform.</span></span> <span data-ttu-id="753ee-239">Ensuite, il met à jour le tampon de constante de modèle sur le GPU.</span><span class="sxs-lookup"><span data-stu-id="753ee-239">Then it updates the model constant buffer on the GPU.</span></span>

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

<span data-ttu-id="753ee-240">Lorsqu’il est temps de restituer des maillages d’aire, nous procédons à un travail de préparation avant de restituer la collection.</span><span class="sxs-lookup"><span data-stu-id="753ee-240">When it's time to render surface meshes, we do some prep work before rendering the collection.</span></span> <span data-ttu-id="753ee-241">Nous avons configuré le pipeline du nuanceur pour la configuration de rendu actuelle et nous avons configuré l’étape assembleur d’entrée.</span><span class="sxs-lookup"><span data-stu-id="753ee-241">We set up the shader pipeline for the current rendering configuration, and we set up the input assembler stage.</span></span> <span data-ttu-id="753ee-242">Notez que la classe d’assistance d’appareil photo holographique **CameraResources. cpp** a déjà configuré la mémoire tampon de la vue/projection à présent.</span><span class="sxs-lookup"><span data-stu-id="753ee-242">Note that the holographic camera helper class **CameraResources.cpp** already has set up the view/projection constant buffer by now.</span></span>

<span data-ttu-id="753ee-243">À partir de **RealtimeSurfaceMeshRenderer :: Render**:</span><span class="sxs-lookup"><span data-stu-id="753ee-243">From **RealtimeSurfaceMeshRenderer::Render**:</span></span>

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

<span data-ttu-id="753ee-244">Une fois cette opération effectuée, nous effectuons une boucle sur nos mailles et indiquons à chacun de se dessiner lui-même.</span><span class="sxs-lookup"><span data-stu-id="753ee-244">Once this is done, we loop on our meshes and tell each one to draw itself.</span></span> <span data-ttu-id="753ee-245">**Remarque :** Cet exemple de code n’est pas optimisé pour utiliser n’importe quel type d’élimination de frustum, mais vous devez inclure cette fonctionnalité dans votre application.</span><span class="sxs-lookup"><span data-stu-id="753ee-245">**NOTE:** This sample code is not optimized to use any sort of frustum culling, but you should include this feature in your app.</span></span>

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

<span data-ttu-id="753ee-246">Les maillages individuels sont responsables de la configuration des tampons de mémoire tampon de vertex et d’index, de Stride et de la transformation de modèle.</span><span class="sxs-lookup"><span data-stu-id="753ee-246">The individual meshes are responsible for setting up the vertex and index buffer, stride, and model transform constant buffer.</span></span> <span data-ttu-id="753ee-247">Comme pour le cube en rotation dans le modèle d’application holographique Windows, nous rendons les tampons stéréoscopiques à l’aide de l’instanciation.</span><span class="sxs-lookup"><span data-stu-id="753ee-247">As with the spinning cube in the Windows Holographic app template, we render to stereoscopic buffers using instancing.</span></span>

<span data-ttu-id="753ee-248">À partir de **SurfaceMesh ::D RAW**:</span><span class="sxs-lookup"><span data-stu-id="753ee-248">From **SurfaceMesh::Draw**:</span></span>

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

### <a name="rendering-choices-with-surface-mapping"></a><span data-ttu-id="753ee-249">Choix du rendu avec le mappage des surfaces</span><span class="sxs-lookup"><span data-stu-id="753ee-249">Rendering choices with Surface Mapping</span></span>

<span data-ttu-id="753ee-250">L’exemple de code de mappage des surfaces offre du code pour le rendu d’occlusion uniquement des données de maillage des surfaces et pour le rendu à l’écran des données de maillage des surfaces.</span><span class="sxs-lookup"><span data-stu-id="753ee-250">The Surface Mapping code sample offers code for occlusion-only rendering of surface mesh data, and for on-screen rendering of surface mesh data.</span></span> <span data-ttu-id="753ee-251">Le chemin que vous choisissez, ou les deux, dépend de votre application.</span><span class="sxs-lookup"><span data-stu-id="753ee-251">Which path you choose - or both - depends on your application.</span></span> <span data-ttu-id="753ee-252">Nous allons examiner les deux configurations dans ce document.</span><span class="sxs-lookup"><span data-stu-id="753ee-252">We'll walk through both configurations in this document.</span></span>

<span data-ttu-id="753ee-253">**Rendu des mémoires tampons d’occlusion pour l’effet holographique**</span><span class="sxs-lookup"><span data-stu-id="753ee-253">**Rendering occlusion buffers for holographic effect**</span></span>

<span data-ttu-id="753ee-254">Commencez par effacer la vue de la cible de rendu pour la caméra virtuelle actuelle.</span><span class="sxs-lookup"><span data-stu-id="753ee-254">Start by clearing the render target view for the current virtual camera.</span></span>

<span data-ttu-id="753ee-255">À partir de AppMain. cpp :</span><span class="sxs-lookup"><span data-stu-id="753ee-255">From AppMain.cpp:</span></span>

```cpp
context->ClearRenderTargetView(pCameraResources->GetBackBufferRenderTargetView(), DirectX::Colors::Transparent);
```

<span data-ttu-id="753ee-256">Il s’agit d’une passe de « pré-rendu ».</span><span class="sxs-lookup"><span data-stu-id="753ee-256">This is a "pre-rendering" pass.</span></span> <span data-ttu-id="753ee-257">Ici, nous créons une mémoire tampon d’occlusion en demandant au convertisseur de maille d’afficher uniquement la profondeur.</span><span class="sxs-lookup"><span data-stu-id="753ee-257">Here, we create an occlusion buffer by asking the mesh renderer to render only depth.</span></span> <span data-ttu-id="753ee-258">Dans cette configuration, nous n’attachons pas de vue de cible de rendu et le convertisseur de maillage définit l’étape de nuanceur de pixels sur **nullptr** afin que le GPU ne s’arrête pas à dessiner des pixels.</span><span class="sxs-lookup"><span data-stu-id="753ee-258">In this configuration, we don't attach a render target view, and the mesh renderer sets the pixel shader stage to **nullptr** so that the GPU doesn't bother to draw pixels.</span></span> <span data-ttu-id="753ee-259">La géométrie est pixellisée dans le tampon de profondeur et le pipeline graphique s’arrête.</span><span class="sxs-lookup"><span data-stu-id="753ee-259">The geometry will be rasterized to the depth buffer, and the graphics pipeline will stop there.</span></span>

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

<span data-ttu-id="753ee-260">Nous pouvons dessiner des hologrammes avec un test de profondeur supplémentaire sur la mémoire tampon d’occlusion de mappage de surface.</span><span class="sxs-lookup"><span data-stu-id="753ee-260">We can draw holograms with an extra depth test against the Surface Mapping occlusion buffer.</span></span> <span data-ttu-id="753ee-261">Dans cet exemple de code, nous avons rendu les pixels sur le cube d’une couleur différente s’ils se trouvent derrière une surface.</span><span class="sxs-lookup"><span data-stu-id="753ee-261">In this code sample, we render pixels on the cube a different color if they are behind a surface.</span></span>

<span data-ttu-id="753ee-262">À partir de AppMain. cpp :</span><span class="sxs-lookup"><span data-stu-id="753ee-262">From AppMain.cpp:</span></span>

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

<span data-ttu-id="753ee-263">Basé sur le code de SpecialEffectPixelShader. HLSL :</span><span class="sxs-lookup"><span data-stu-id="753ee-263">Based on code from SpecialEffectPixelShader.hlsl:</span></span>

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

<span data-ttu-id="753ee-264">**Remarque :** Pour notre routine **GatherDepthLess** , consultez l’exemple de code de mappage des surfaces : SpecialEffectPixelShader. HLSL.</span><span class="sxs-lookup"><span data-stu-id="753ee-264">**Note:** For our **GatherDepthLess** routine, see the Surface Mapping code sample: SpecialEffectPixelShader.hlsl.</span></span>

<span data-ttu-id="753ee-265">**Rendu des données de maillage des surfaces à l’affichage**</span><span class="sxs-lookup"><span data-stu-id="753ee-265">**Rendering surface mesh data to the display**</span></span>

<span data-ttu-id="753ee-266">Nous pouvons également simplement dessiner les maillages des surfaces dans les tampons d’affichage stéréo.</span><span class="sxs-lookup"><span data-stu-id="753ee-266">We can also just draw the surface meshes to the stereo display buffers.</span></span> <span data-ttu-id="753ee-267">Nous avons choisi de dessiner des visages complets avec de l’éclairage, mais vous êtes libre de dessiner du filaire, de traiter les maillages avant le rendu, d’appliquer une carte de texture, etc.</span><span class="sxs-lookup"><span data-stu-id="753ee-267">We chose to draw full faces with lighting, but you're free to draw wireframe, process meshes before rendering, apply a texture map, and so on.</span></span>

<span data-ttu-id="753ee-268">Ici, notre exemple de code indique au convertisseur de maille de dessiner la collection.</span><span class="sxs-lookup"><span data-stu-id="753ee-268">Here, our code sample tells the mesh renderer to draw the collection.</span></span> <span data-ttu-id="753ee-269">Cette fois, nous ne spécifions pas de passage à profondeur uniquement. il attachera donc un nuanceur de pixels et terminera le pipeline de rendu à l’aide des cibles que nous avons spécifiées pour la caméra virtuelle actuelle.</span><span class="sxs-lookup"><span data-stu-id="753ee-269">This time we don't specify a depth-only pass, so it will attach a pixel shader and complete the rendering pipeline using the targets that we specified for the current virtual camera.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="753ee-270">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="753ee-270">See also</span></span>
* [<span data-ttu-id="753ee-271">Création d’un projet DirectX holographique</span><span class="sxs-lookup"><span data-stu-id="753ee-271">Creating a holographic DirectX project</span></span>](creating-a-holographic-directx-project.md)
* [<span data-ttu-id="753ee-272">API Windows. perception. spatial</span><span class="sxs-lookup"><span data-stu-id="753ee-272">Windows.Perception.Spatial API</span></span>](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.aspx)
