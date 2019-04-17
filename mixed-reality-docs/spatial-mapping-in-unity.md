---
title: Mappage spatial dans Unity
description: Rendu et se heurtant à la géométrie réelle autour de vous dans Unity.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, mappage spatial, convertisseur, collider, maillage, l’analyse, composant
ms.openlocfilehash: f938f5921cb2c06342a9ebcd376d690c10584df9
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597148"
---
# <a name="spatial-mapping-in-unity"></a><span data-ttu-id="25d66-104">Mappage spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="25d66-104">Spatial mapping in Unity</span></span>

<span data-ttu-id="25d66-105">Cette rubrique explique comment utiliser [mappage spatial](spatial-mapping.md) dans votre projet Unity, la récupération des maillages de triangles qui représentent les surfaces dans le monde autour d’un appareil HoloLens, pour la sélection élective, occlusion, analyse de la salle et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="25d66-105">This topic describes how to use [spatial mapping](spatial-mapping.md) in your Unity project, retrieving triangle meshes that represent the surfaces in the world around a HoloLens device, for placement, occlusion, room analysis and more.</span></span>

<span data-ttu-id="25d66-106">Unity prend également en charge pour le mappage spatial, qui est exposé aux développeurs de plusieurs manières :</span><span class="sxs-lookup"><span data-stu-id="25d66-106">Unity includes full support for spatial mapping, which is exposed to developers in the following ways:</span></span>
1. <span data-ttu-id="25d66-107">Mappage des composants disponibles dans le MixedRealityToolkit spatial, qui fournissent un chemin d’accès rapide et pratique pour bien démarrer avec mappage spatial</span><span class="sxs-lookup"><span data-stu-id="25d66-107">Spatial mapping components available in the MixedRealityToolkit, which provide a convenient and rapid path for getting started with spatial mapping</span></span>
2. <span data-ttu-id="25d66-108">Mappage spatial de bas niveau API, qui fournissent complète contrôler et activer la personnalisation spécifique des applications plus sophistiquée</span><span class="sxs-lookup"><span data-stu-id="25d66-108">Lower-level spatial mapping APIs, which provide full control and enable more sophisticated application specific customization</span></span>

<span data-ttu-id="25d66-109">Pour utiliser le mappage spatial dans votre application, la fonctionnalité spatialPerception doit être définie dans votre AppxManifest.</span><span class="sxs-lookup"><span data-stu-id="25d66-109">To use spatial mapping in your app, the spatialPerception capability needs to be set in your AppxManifest.</span></span>

## <a name="setting-the-spatialperception-capability"></a><span data-ttu-id="25d66-110">Définition de la fonctionnalité SpatialPerception</span><span class="sxs-lookup"><span data-stu-id="25d66-110">Setting the SpatialPerception capability</span></span>

<span data-ttu-id="25d66-111">Dans l’ordre pour une application de consommer des données de mappage spatial, la fonctionnalité SpatialPerception doit être activée.</span><span class="sxs-lookup"><span data-stu-id="25d66-111">In order for an app to consume spatial mapping data, the SpatialPerception capability must be enabled.</span></span>

<span data-ttu-id="25d66-112">Comment activer la fonctionnalité SpatialPerception :</span><span class="sxs-lookup"><span data-stu-id="25d66-112">How to enable the SpatialPerception capability:</span></span>
1. <span data-ttu-id="25d66-113">Dans l’éditeur Unity, ouvrez le **« Paramètres du lecteur »** volet (Modifier > Paramètres du projet > lecteur)</span><span class="sxs-lookup"><span data-stu-id="25d66-113">In the Unity Editor, open the **"Player Settings"** pane (Edit > Project Settings > Player)</span></span>
2. <span data-ttu-id="25d66-114">Cliquez sur le **« Windows Store »** onglet</span><span class="sxs-lookup"><span data-stu-id="25d66-114">Click on the **"Windows Store"** tab</span></span>
3. <span data-ttu-id="25d66-115">Développez **« Paramètres de publication »** et vérifiez le **« SpatialPerception »** fonctionnalité dans le **« Fonctionnalités »** liste</span><span class="sxs-lookup"><span data-stu-id="25d66-115">Expand **"Publishing Settings"** and check the **"SpatialPerception"** capability in the **"Capabilities"** list</span></span>

<span data-ttu-id="25d66-116">Notez que si vous avez déjà exporté votre projet Unity à une solution Visual Studio, vous devrez soit exporter vers un nouveau dossier ou manuellement [définir cette fonctionnalité dans le fichier AppxManifest dans Visual Studio](spatial-mapping-in-directx.md#set-up-your-app-to-use-the-spatialperception-capability).</span><span class="sxs-lookup"><span data-stu-id="25d66-116">Note that if you have already exported your Unity project to a Visual Studio solution, you will need to either export to a new folder or manually [set this capability in the AppxManifest in Visual Studio](spatial-mapping-in-directx.md#set-up-your-app-to-use-the-spatialperception-capability).</span></span>

<span data-ttu-id="25d66-117">Mappage spatial requiert également un MaxVersionTested de 10.0.10586.0 au moins :</span><span class="sxs-lookup"><span data-stu-id="25d66-117">Spatial mapping also requires a MaxVersionTested of at least 10.0.10586.0:</span></span>
1. <span data-ttu-id="25d66-118">Dans Visual Studio, avec le bouton droit, cliquez sur **Package.appxmanifest** dans l’Explorateur de solutions, puis sélectionnez **afficher le Code**</span><span class="sxs-lookup"><span data-stu-id="25d66-118">In Visual Studio, right click on **Package.appxmanifest** in the Solution Explorer and select **View Code**</span></span>
2. <span data-ttu-id="25d66-119">Recherchez la ligne spécifiant **TargetDeviceFamily** et modifiez **MaxVersionTested = « 10.0.10240.0 »** à **MaxVersionTested = « 10.0.10586.0 »**</span><span class="sxs-lookup"><span data-stu-id="25d66-119">Find the line specifying **TargetDeviceFamily** and change **MaxVersionTested="10.0.10240.0"** to **MaxVersionTested="10.0.10586.0"**</span></span>
3. <span data-ttu-id="25d66-120">**Enregistrer** le Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="25d66-120">**Save** the Package.appxmanifest.</span></span>

## <a name="getting-started-with-unitys-built-in-spatial-mapping-components"></a><span data-ttu-id="25d66-121">Mise en route avec les composants de mappage spatial intégrés d’Unity</span><span class="sxs-lookup"><span data-stu-id="25d66-121">Getting started with Unity's built-in spatial mapping components</span></span>

<span data-ttu-id="25d66-122">Unity propose 2 composants permettant d’ajouter facilement mappage spatial à votre application, **convertisseur de mappage Spatial** et **Collider de mappage Spatial**.</span><span class="sxs-lookup"><span data-stu-id="25d66-122">Unity offers 2 components for easily adding spatial mapping to your app, **Spatial Mapping Renderer** and **Spatial Mapping Collider**.</span></span>

### <a name="spatial-mapping-renderer"></a><span data-ttu-id="25d66-123">Convertisseur de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="25d66-123">Spatial Mapping Renderer</span></span>

<span data-ttu-id="25d66-124">Le convertisseur de mappage Spatial permet la visualisation de la maille de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="25d66-124">The Spatial Mapping Renderer allows for visualization of the spatial mapping mesh.</span></span>

![Convertisseur de mappage spatial dans Unity](images/spatialmappingrenderer.png)

### <a name="spatial-mapping-collider"></a><span data-ttu-id="25d66-126">Mappage spatial Collider</span><span class="sxs-lookup"><span data-stu-id="25d66-126">Spatial Mapping Collider</span></span>

<span data-ttu-id="25d66-127">Permet du Collider mappage Spatial pour le contenu HOLOGRAPHIQUE (ou caractère) interaction, telles que physique, avec le maillage de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="25d66-127">The Spatial Mapping Collider allows for holographic content (or character) interaction, such as physics, with the spatial mapping mesh.</span></span>

![Collider mappage spatial dans Unity](images/spatialmappingcollider.png)

### <a name="using-the-built-in-spatial-mapping-components"></a><span data-ttu-id="25d66-129">L’utilisation des composants intégrés mappage spatial</span><span class="sxs-lookup"><span data-stu-id="25d66-129">Using the built-in spatial mapping components</span></span>

<span data-ttu-id="25d66-130">Si vous souhaitez les visualiser et interagir avec des surfaces physiques, vous pouvez ajouter les deux composants à votre application.</span><span class="sxs-lookup"><span data-stu-id="25d66-130">You may add both components to your app if you'd like to both visualize and interact with physical surfaces.</span></span>

<span data-ttu-id="25d66-131">Pour utiliser ces deux composants dans votre application Unity :</span><span class="sxs-lookup"><span data-stu-id="25d66-131">To use these two components in your Unity app:</span></span>
1. <span data-ttu-id="25d66-132">Sélectionnez un GameObject au centre de la zone dans laquelle vous souhaitez détecter les mailles de surface spatiales.</span><span class="sxs-lookup"><span data-stu-id="25d66-132">Select a GameObject at the center of the area in which you'd like to detect spatial surface meshes.</span></span>
2. <span data-ttu-id="25d66-133">Dans la fenêtre d’inspecteur, **ajouter un composant** > **XR** > **Collider de mappage Spatial** ou **Spatial Convertisseur de mappage**.</span><span class="sxs-lookup"><span data-stu-id="25d66-133">In the Inspector window, **Add Component** > **XR** > **Spatial Mapping Collider** or **Spatial Mapping Renderer**.</span></span>

<span data-ttu-id="25d66-134">Vous trouverez plus d’informations sur l’utilisation de ces composants à la <a href="https://docs.unity3d.com/Manual/SpatialMappingComponents.html" target="_blank">site de documentation Unity</a>.</span><span class="sxs-lookup"><span data-stu-id="25d66-134">You can find more details on how to use these components at the <a href="https://docs.unity3d.com/Manual/SpatialMappingComponents.html" target="_blank">Unity documentation site</a>.</span></span>

### <a name="going-beyond-the-built-in-spatial-mapping-components"></a><span data-ttu-id="25d66-135">Au-delà des composants intégrés mappage spatial</span><span class="sxs-lookup"><span data-stu-id="25d66-135">Going beyond the built-in spatial mapping components</span></span>

<span data-ttu-id="25d66-136">Ces composants rendent glisser-déplacer faciles pour bien démarrer avec le mappage Spatial.</span><span class="sxs-lookup"><span data-stu-id="25d66-136">These components make it drag-and-drop easy to get started with Spatial Mapping.</span></span> <span data-ttu-id="25d66-137"> Lorsque vous souhaitez aller plus loin, il existe deux chemins d’accès principales pour Explorer :</span><span class="sxs-lookup"><span data-stu-id="25d66-137"> When you want to go further, there are two main paths to explore:</span></span>
* <span data-ttu-id="25d66-138">Pour faire votre propre traitement de maillage de niveau inférieur, consultez la section ci-dessous sur le script mappage Spatial API de bas niveau.</span><span class="sxs-lookup"><span data-stu-id="25d66-138">To do your own lower-level mesh processing, see the section below about the low-level Spatial Mapping script API.</span></span>
* <span data-ttu-id="25d66-139">Pour effectuer des analyses de maillage de niveau supérieur, consultez la section ci-dessous sur la bibliothèque SpatialUnderstanding dans <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialUnderstanding" target="_blank">MixedRealityToolkit</a>.</span><span class="sxs-lookup"><span data-stu-id="25d66-139">To do higher-level mesh analysis, see the section below about the SpatialUnderstanding library in <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialUnderstanding" target="_blank">MixedRealityToolkit</a>.</span></span>

## <a name="using-the-low-level-unity-spatial-mapping-api"></a><span data-ttu-id="25d66-140">À l’aide de l’API de mappage Spatial Unity bas niveau</span><span class="sxs-lookup"><span data-stu-id="25d66-140">Using the low-level Unity Spatial Mapping API</span></span>

<span data-ttu-id="25d66-141">Si vous avez besoin de plus de contrôle que vous obtenez à partir des composants de convertisseur de mappage spatiales et spatiales Collider de mappage, vous pouvez utiliser le script de bas niveau mappage Spatial API.</span><span class="sxs-lookup"><span data-stu-id="25d66-141">If you need more control than you get from the Spatial Mapping Renderer and Spatial Mapping Collider components, you can use the low-level Spatial Mapping script APIs.</span></span>

<span data-ttu-id="25d66-142">**Namespace :** *UnityEngine.XR.WSA*</span><span class="sxs-lookup"><span data-stu-id="25d66-142">**Namespace:** *UnityEngine.XR.WSA*</span></span><br>
<span data-ttu-id="25d66-143">**Types**: *SurfaceObserver*, *SurfaceChange*, *SurfaceData*, *SurfaceId*</span><span class="sxs-lookup"><span data-stu-id="25d66-143">**Types**: *SurfaceObserver*, *SurfaceChange*, *SurfaceData*, *SurfaceId*</span></span>

<span data-ttu-id="25d66-144">Voici un plan du flux suggéré pour une application qui utilise l’API de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="25d66-144">The following is an outline of the suggested flow for an application that uses the spatial mapping APIs.</span></span>

### <a name="set-up-the-surfaceobservers"></a><span data-ttu-id="25d66-145">Configurer le SurfaceObserver(s)</span><span class="sxs-lookup"><span data-stu-id="25d66-145">Set up the SurfaceObserver(s)</span></span>

<span data-ttu-id="25d66-146">Instanciez un objet SurfaceObserver pour chaque région définie par l’application de l’espace dont vous avez besoin des données de mappage spatial pour.</span><span class="sxs-lookup"><span data-stu-id="25d66-146">Instantiate one SurfaceObserver object for each application-defined region of space that you need spatial mapping data for.</span></span>

```cs
SurfaceObserver surfaceObserver;

 void Start () {
     surfaceObserver = new SurfaceObserver();
 }
```

<span data-ttu-id="25d66-147">Spécifier la région d’espace que chaque objet SurfaceObserver fournira les données pour en appelant SetVolumeAsSphere, SetVolumeAsAxisAlignedBox, SetVolumeAsOrientedBox ou SetVolumeAsFrustum.</span><span class="sxs-lookup"><span data-stu-id="25d66-147">Specify the region of space that each SurfaceObserver object will provide data for by calling either SetVolumeAsSphere, SetVolumeAsAxisAlignedBox, SetVolumeAsOrientedBox, or SetVolumeAsFrustum.</span></span> <span data-ttu-id="25d66-148">Vous pouvez redéfinir la région d’espace à l’avenir en appelant simplement une de ces méthodes à nouveau.</span><span class="sxs-lookup"><span data-stu-id="25d66-148">You can redefine the region of space in the future by simply calling one of these methods again.</span></span>

```cs
void Start () {
    ...
     surfaceObserver.SetVolumeAsAxisAlignedBox(Vector3.zero, new Vector3(3, 3, 3));
}
```

<span data-ttu-id="25d66-149">Lorsque vous appelez SurfaceObserver.Update(), vous devez fournir un gestionnaire pour chaque surface spatiale dans la région de la SurfaceObserver d’espace au système de mappage spatial a de nouvelles informations pour.</span><span class="sxs-lookup"><span data-stu-id="25d66-149">When you call SurfaceObserver.Update(), you must provide a handler for each spatial surface in the SurfaceObserver's region of space that the spatial mapping system has new information for.</span></span> <span data-ttu-id="25d66-150">Le gestionnaire reçoit, pour une surface spatiale :</span><span class="sxs-lookup"><span data-stu-id="25d66-150">The handler receives, for one spatial surface:</span></span>

```cs
private void OnSurfaceChanged(SurfaceId surfaceId, SurfaceChange changeType, Bounds bounds, System.DateTime updateTime)
 {
    //see Handling Surface Changes
 }
```

### <a name="handling-surface-changes"></a><span data-ttu-id="25d66-151">Gestion des modifications de l’aire de conception</span><span class="sxs-lookup"><span data-stu-id="25d66-151">Handling Surface Changes</span></span>

<span data-ttu-id="25d66-152">Il existe plusieurs cas principales à gérer.</span><span class="sxs-lookup"><span data-stu-id="25d66-152">There are several main cases to handle.</span></span> <span data-ttu-id="25d66-153">Ajouter & code de mise à jour qui peut utiliser le même chemin d’accès et suppression.</span><span class="sxs-lookup"><span data-stu-id="25d66-153">Added & Updated which can use the same code path and Removed.</span></span>
* <span data-ttu-id="25d66-154">Dans les cas Added & mis à jour dans l’exemple, nous ajouter ou à obtenir le GameObject représentant ce maillage à partir du dictionnaire, créez un struct SurfaceData avec les composants nécessaires, puis appeler RequestMeshDataAsync pour remplir le GameObject avec les données de maillage et position dans la scène.</span><span class="sxs-lookup"><span data-stu-id="25d66-154">In the Added & Updated cases in the example, we add or get the GameObject representing this mesh from the dictionary, create a SurfaceData struct with the necessary components, then call RequestMeshDataAsync to populate the GameObject with the mesh data and position in the scene.</span></span>
* <span data-ttu-id="25d66-155">Dans le cas de suppression, nous supprimer le GameObject représentant ce maillage à partir du dictionnaire et détruire.</span><span class="sxs-lookup"><span data-stu-id="25d66-155">In the Removed case, we remove the GameObject representing this mesh from the dictionary and destroy it.</span></span>

```cs
System.Collections.Generic.Dictionary<SurfaceId, GameObject> spatialMeshObjects = 
    new System.Collections.Generic.Dictionary<SurfaceId, GameObject>();

   private void OnSurfaceChanged(SurfaceId surfaceId, SurfaceChange changeType, Bounds bounds, System.DateTime updateTime)
   {
       switch (changeType)
       {
           case SurfaceChange.Added:
           case SurfaceChange.Updated:
               if (!spatialMeshObjects.ContainsKey(surfaceId))
               {
                   spatialMeshObjects[surfaceId] = new GameObject("spatial-mapping-" + surfaceId);
                   spatialMeshObjects[surfaceId].transform.parent = this.transform;
                   spatialMeshObjects[surfaceId].AddComponent<MeshRenderer>();
               }
               GameObject target = spatialMeshObjects[surfaceId];
               SurfaceData sd = new SurfaceData(
                   //the surface id returned from the system
                   surfaceId,
                   //the mesh filter that is populated with the spatial mapping data for this mesh
                   target.GetComponent<MeshFilter>() ?? target.AddComponent<MeshFilter>(),
                   //the world anchor used to position the spatial mapping mesh in the world
                   target.GetComponent<WorldAnchor>() ?? target.AddComponent<WorldAnchor>(),
                   //the mesh collider that is populated with collider data for this mesh, if true is passed to bakeMeshes below
                   target.GetComponent<MeshCollider>() ?? target.AddComponent<MeshCollider>(),
                   //triangles per cubic meter requested for this mesh
                   1000,
                   //bakeMeshes - if true, the mesh collider is populated, if false, the mesh collider is empty.
                   true
                   );

               SurfaceObserver.RequestMeshAsync(sd, OnDataReady);
               break;
           case SurfaceChange.Removed:
               var obj = spatialMeshObjects[surfaceId];
               spatialMeshObjects.Remove(surfaceId);
               if (obj != null)
               {
                   GameObject.Destroy(obj);
               }
               break;
           default:
               break;
       }
   }
```

### <a name="handling-data-ready"></a><span data-ttu-id="25d66-156">Gestion des données prêtes</span><span class="sxs-lookup"><span data-stu-id="25d66-156">Handling Data Ready</span></span>

<span data-ttu-id="25d66-157">Le Gestionnaire de OnDataReady reçoit un objet SurfaceData.</span><span class="sxs-lookup"><span data-stu-id="25d66-157">The OnDataReady handler receives a SurfaceData object.</span></span> <span data-ttu-id="25d66-158">Le WorldAnchor, MeshFilter et (éventuellement les objets MeshCollider qu’il contient) reflètent l’état de la surface spatiale associé.</span><span class="sxs-lookup"><span data-stu-id="25d66-158">The WorldAnchor, MeshFilter and (optionally) MeshCollider objects it contains reflect the latest state of the associated spatial surface.</span></span> <span data-ttu-id="25d66-159">Si vous le souhaitez effectuer une analyse et/ou [traitement](spatial-mapping.md#mesh-processing) des données par l’accès au membre de maillage de l’objet MeshFilter maille.</span><span class="sxs-lookup"><span data-stu-id="25d66-159">Optionally perform analysis and/or [processing](spatial-mapping.md#mesh-processing) of the mesh data by accessing the Mesh member of the MeshFilter object.</span></span> <span data-ttu-id="25d66-160">Restituer la surface spatiale auprès de la maille la plus récente et (éventuellement) de l’utiliser pour les collisions de physique et raycasts.</span><span class="sxs-lookup"><span data-stu-id="25d66-160">Render the spatial surface with the latest mesh and (optionally) use it for physics collisions and raycasts.</span></span> <span data-ttu-id="25d66-161">Il est important de confirmer que le contenu de la SurfaceData n’est pas null.</span><span class="sxs-lookup"><span data-stu-id="25d66-161">It's important to confirm that the contents of the SurfaceData are not null.</span></span>

### <a name="start-processing-on-updates"></a><span data-ttu-id="25d66-162">Commencer le traitement des mises à jour</span><span class="sxs-lookup"><span data-stu-id="25d66-162">Start processing on updates</span></span>

<span data-ttu-id="25d66-163">SurfaceObserver.Update() doit être appelée sur un délai, pas chaque trame.</span><span class="sxs-lookup"><span data-stu-id="25d66-163">SurfaceObserver.Update() should be called on a delay, not every frame.</span></span>

```cs
void Start () {
    ...
     StartCoroutine(UpdateLoop());
}

 IEnumerator UpdateLoop()
    {
        var wait = new WaitForSeconds(2.5f);
        while(true)
        {
            surfaceObserver.Update(OnSurfaceChanged);
            yield return wait;
        }
    }
```

## <a name="higher-level-mesh-analysis-spatialunderstanding"></a><span data-ttu-id="25d66-164">Analyse de maillage de niveau supérieur : SpatialUnderstanding</span><span class="sxs-lookup"><span data-stu-id="25d66-164">Higher-level mesh analysis: SpatialUnderstanding</span></span>

<span data-ttu-id="25d66-165">Le <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">MixedRealityToolkit</a> est une collection de code d’utilitaire utile pour le développement holographique basé sur les API Unity HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="25d66-165">The <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">MixedRealityToolkit</a> is a collection of helpful utility code for holographic development built upon the holographic Unity APIs.</span></span>

### <a name="spatial-understanding"></a><span data-ttu-id="25d66-166">Présentation spatiale</span><span class="sxs-lookup"><span data-stu-id="25d66-166">Spatial Understanding</span></span>

<span data-ttu-id="25d66-167">Lorsque vous placez des hologrammes dans le monde physique, il est souvent souhaitable d’aller au-delà du mappage spatial de maillage et plans de surface.</span><span class="sxs-lookup"><span data-stu-id="25d66-167">When placing holograms in the physical world it is often desirable to go beyond spatial mapping’s mesh and surface planes.</span></span> <span data-ttu-id="25d66-168">Lors de la sélection élective est effectuée de façon procédurale, un niveau plus élevé de compréhension de l’environnement est souhaitable.</span><span class="sxs-lookup"><span data-stu-id="25d66-168">When placement is done procedurally, a higher level of environmental understanding is desirable.</span></span> <span data-ttu-id="25d66-169">Vous devez prendre des décisions sur les nouveautés, floor, ceiling et murs.</span><span class="sxs-lookup"><span data-stu-id="25d66-169">This usually requires making decisions about what is floor, ceiling, and walls.</span></span> <span data-ttu-id="25d66-170">En outre, la capacité d’optimiser par rapport à un ensemble de contraintes de placement à la détermination des emplacements physiques plus souhaitables pour les objets HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="25d66-170">In addition, the ability to optimize against a set of placement constraints to determining the most desirable physical locations for holographic objects.</span></span>

<span data-ttu-id="25d66-171">Pendant le développement de Young pétarade et de Fragments, Asobo Studios confrontés head de ce problème sur, le développement d’un solveur salle à cet effet.</span><span class="sxs-lookup"><span data-stu-id="25d66-171">During the development of Young Conker and Fragments, Asobo Studios faced this problem head on, developing a room solver for this purpose.</span></span> <span data-ttu-id="25d66-172">Chacun de ces jeux avait jeu besoins spécifiques, mais qu’ils partageaient core spatial fonctionnement de la technologie.</span><span class="sxs-lookup"><span data-stu-id="25d66-172">Each of these games had game specific needs, but they shared core spatial understanding technology.</span></span> <span data-ttu-id="25d66-173">HoloToolkit.SpatialUnderstanding bibliothèque encapsule cette technologie, ce qui que vous permettent de rechercher rapidement les espaces vides sur les murs, les objets sur place au plafond, identifiez placés par caractère asseoir et une myriade d’autres requêtes spatiales compréhension.</span><span class="sxs-lookup"><span data-stu-id="25d66-173">The HoloToolkit.SpatialUnderstanding library encapsulates this technology, allowing you to quickly find empty spaces on the walls, place objects on the ceiling, identify placed for character to sit, and a myriad of other spatial understanding queries.</span></span>

<span data-ttu-id="25d66-174">Tout le code source est inclus, ce qui vous permet de le personnaliser selon vos besoins et partager vos améliorations avec la Communauté.</span><span class="sxs-lookup"><span data-stu-id="25d66-174">All of the source code is included, allowing you to customize it to your needs and share your improvements with the community.</span></span> <span data-ttu-id="25d66-175">Le code pour le C++ Solveur a été encapsulé dans une dll UWP et exposé à Unity avec une baisse de préfabriqué contenu dans le MixedRealityToolkit.</span><span class="sxs-lookup"><span data-stu-id="25d66-175">The code for the C++ solver has been wrapped into a UWP dll and exposed to Unity with a drop in prefab contained within the MixedRealityToolkit.</span></span>

### <a name="understanding-modules"></a><span data-ttu-id="25d66-176">Modules de présentation</span><span class="sxs-lookup"><span data-stu-id="25d66-176">Understanding Modules</span></span>

<span data-ttu-id="25d66-177">Il existe trois interfaces principales exposées par le module : topologie pour surface simple et les requêtes spatiales, la forme pour la détection de l’objet et le solveur de sélection élective d’objet pour la sélection élective de contrainte en fonction de jeux d’objets.</span><span class="sxs-lookup"><span data-stu-id="25d66-177">There are three primary interfaces exposed by the module: topology for simple surface and spatial queries, shape for object detection, and the object placement solver for constraint based placement of object sets.</span></span> <span data-ttu-id="25d66-178">Chacune d'entre elles est décrite ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="25d66-178">Each of these is described below.</span></span> <span data-ttu-id="25d66-179">En plus des trois interfaces de module principal, une interface de casting ray peut être utilisée pour récupérer des types de surface avec balises et une maille playspace étanches personnalisé peut être copiée.</span><span class="sxs-lookup"><span data-stu-id="25d66-179">In addition to the three primary module interfaces, a ray casting interface can be used to retrieve tagged surface types and a custom watertight playspace mesh can be copied out.</span></span>

### <a name="ray-casting"></a><span data-ttu-id="25d66-180">Ray cast</span><span class="sxs-lookup"><span data-stu-id="25d66-180">Ray Casting</span></span>

<span data-ttu-id="25d66-181">Une fois que la pièce a été analysée et finalisée, étiquettes sont générés de manière interne pour les surfaces comme floor, ceiling, les murs.</span><span class="sxs-lookup"><span data-stu-id="25d66-181">After the room has been scanned and finalized, labels are internally generated for surfaces like the floor, ceiling, and walls.</span></span> <span data-ttu-id="25d66-182">Le « PlayspaceRaycast » prend un rayon de fonction et retourne si le rayon est en conflit avec une surface connue et le cas échéant, des informations sur cette surface sous la forme d’un « RaycastResult ».</span><span class="sxs-lookup"><span data-stu-id="25d66-182">The “PlayspaceRaycast” function takes a ray and returns if the ray collides with a known surface and if so, information about that surface in the form of a “RaycastResult”.</span></span>

```cpp
struct RaycastResult
{
    enum SurfaceTypes
    {
        Invalid,    // No intersection
        Other,
        Floor,
        FloorLike,  // Not part of the floor topology, 
                    //  but close to the floor and looks like the floor
        Platform,   // Horizontal platform between the ground and 
                    //  the ceiling
        Ceiling,
        WallExternal,
        WallLike,   // Not part of the external wall surface, 
                    //  but vertical surface that looks like a 
                    //  wall structure
    };
    SurfaceTypes SurfaceType;
    float SurfaceArea;  // Zero if unknown 
                        //  (i.e. if not part of the topology analysis)
    DirectX::XMFLOAT3 IntersectPoint;
    DirectX::XMFLOAT3 IntersectNormal;
};
```

<span data-ttu-id="25d66-183">En interne, le raycast est calculée par rapport à la représentation sous forme de voxel calculée 8cm au cube de la playspace.</span><span class="sxs-lookup"><span data-stu-id="25d66-183">Internally, the raycast is computed against the computed 8cm cubed voxel representation of the playspace.</span></span> <span data-ttu-id="25d66-184">Chaque voxel contient un ensemble d’éléments de surface d’exposition des données de topologie traité (également appelé surfels).</span><span class="sxs-lookup"><span data-stu-id="25d66-184">Each voxel contains a set of surface elements with processed topology data (aka surfels).</span></span> <span data-ttu-id="25d66-185">Les surfels contenues dans la cellule voxel intersectées sont comparées et la meilleure correspondance est utilisée pour rechercher les informations de topologie.</span><span class="sxs-lookup"><span data-stu-id="25d66-185">The surfels contained within the intersected voxel cell are compared and the best match used to look up the topology information.</span></span> <span data-ttu-id="25d66-186">Les données de cette topologie contient l’étiquetage retournées dans le formulaire de l’enum « SurfaceTypes », ainsi que la surface d’exposition de la surface d’intersection.</span><span class="sxs-lookup"><span data-stu-id="25d66-186">This topology data contains the labeling returned in the form of the “SurfaceTypes” enum, as well as the surface area of the intersected surface.</span></span>

<span data-ttu-id="25d66-187">Dans l’exemple Unity, le curseur convertit un rayon chaque frame.</span><span class="sxs-lookup"><span data-stu-id="25d66-187">In the Unity sample, the cursor casts a ray each frame.</span></span> <span data-ttu-id="25d66-188">Tout d’abord, contre colliders de d’Unity.</span><span class="sxs-lookup"><span data-stu-id="25d66-188">First, against Unity’s colliders.</span></span> <span data-ttu-id="25d66-189">En second lieu, par rapport à la représentation sous forme de monde du module de présentation.</span><span class="sxs-lookup"><span data-stu-id="25d66-189">Second, against the understanding module’s world representation.</span></span> <span data-ttu-id="25d66-190">Et enfin, à nouveau éléments d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="25d66-190">And finally, again UI elements.</span></span> <span data-ttu-id="25d66-191">Dans cette application, l’interface utilisateur obtient ensuite la priorité, le résultat de la présentation et enfin, les colliders d’Unity.</span><span class="sxs-lookup"><span data-stu-id="25d66-191">In this application, UI gets priority, next the understanding result, and lastly, Unity’s colliders.</span></span> <span data-ttu-id="25d66-192">Le SurfaceType est signalée en tant que texte en regard du curseur.</span><span class="sxs-lookup"><span data-stu-id="25d66-192">The SurfaceType is reported as text next to the cursor.</span></span>

<span data-ttu-id="25d66-193">![Type de l’aire de conception est étiqueté situé à proximité du curseur](images/su-raycastresults-300px.jpg)</span><span class="sxs-lookup"><span data-stu-id="25d66-193">![Surface type is labeled next to the cursor](images/su-raycastresults-300px.jpg)</span></span><br>
<span data-ttu-id="25d66-194">*Type de l’aire de conception est étiqueté situé à proximité du curseur*</span><span class="sxs-lookup"><span data-stu-id="25d66-194">*Surface type is labeled next to the cursor*</span></span>

### <a name="topology-queries"></a><span data-ttu-id="25d66-195">Requêtes de topologie</span><span class="sxs-lookup"><span data-stu-id="25d66-195">Topology Queries</span></span>

<span data-ttu-id="25d66-196">Dans la DLL, le Gestionnaire de topologie gère l’étiquetage de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="25d66-196">Within the DLL, the topology manager handles labeling of the environment.</span></span> <span data-ttu-id="25d66-197">Comme mentionné ci-dessus, les données sont stockées dans surfels, contenus dans un volume voxel.</span><span class="sxs-lookup"><span data-stu-id="25d66-197">As mentioned above, much of the data is stored within surfels, contained within a voxel volume.</span></span> <span data-ttu-id="25d66-198">En outre, la structure « PlaySpaceInfos » est utilisée pour stocker des informations sur le playspace, y compris l’alignement du monde (plus de détails ci-dessous), floor et au plafond.</span><span class="sxs-lookup"><span data-stu-id="25d66-198">In addition, the “PlaySpaceInfos” structure is used to store information about the playspace, including the world alignment (more details on this below), floor, and ceiling height.</span></span> <span data-ttu-id="25d66-199">Heuristique utilisée pour déterminer les murs floor et ceiling.</span><span class="sxs-lookup"><span data-stu-id="25d66-199">Heuristics are used for determining floor, ceiling, and walls.</span></span> <span data-ttu-id="25d66-200">Par exemple, la surface plus grande et plus basses horizontale avec plus de 1 la surface d’exposition m2 est considéré comme le plancher.</span><span class="sxs-lookup"><span data-stu-id="25d66-200">For example, the largest and lowest horizontal surface with greater than 1 m2 surface area is considered the floor.</span></span> <span data-ttu-id="25d66-201">Notez que le chemin d’accès de l’appareil photo pendant le processus d’analyse est également utilisé dans ce processus.</span><span class="sxs-lookup"><span data-stu-id="25d66-201">Note that the camera path during the scanning process is also used in this process.</span></span>

<span data-ttu-id="25d66-202">Un sous-ensemble de requêtes exposées par le Gestionnaire de la topologie sont exposés via la dll.</span><span class="sxs-lookup"><span data-stu-id="25d66-202">A subset of the queries exposed by the Topology manager are exposed out through the dll.</span></span> <span data-ttu-id="25d66-203">Les requêtes de topologie exposés sont comme suit.</span><span class="sxs-lookup"><span data-stu-id="25d66-203">The exposed topology queries are as follows.</span></span>

```cpp
QueryTopology_FindPositionsOnWalls
QueryTopology_FindLargePositionsOnWalls
QueryTopology_FindLargestWall
QueryTopology_FindPositionsOnFloor
QueryTopology_FindLargestPositionsOnFloor
QueryTopology_FindPositionsSittable
```

<span data-ttu-id="25d66-204">Chacune des requêtes a un ensemble de paramètres, spécifiques au type de requête.</span><span class="sxs-lookup"><span data-stu-id="25d66-204">Each of the queries has a set of parameters, specific to the query type.</span></span> <span data-ttu-id="25d66-205">Dans l’exemple suivant, l’utilisateur spécifie la hauteur minimale et la largeur du volume de votre choix, à la hauteur minimale de sélection élective au-dessus de la valeur plancher, la quantité minimale de dégagement devant le volume.</span><span class="sxs-lookup"><span data-stu-id="25d66-205">In the following example, the user specifies the minimum height & width of the desired volume, minimum placement height above the floor, and the minimum amount of clearance in front of the volume.</span></span> <span data-ttu-id="25d66-206">Toutes les mesures sont en mètres.</span><span class="sxs-lookup"><span data-stu-id="25d66-206">All measurements are in meters.</span></span>

```cpp
EXTERN_C __declspec(dllexport) int QueryTopology_FindPositionsOnWalls(
    _In_ float minHeightOfWallSpace,
    _In_ float minWidthOfWallSpace,
    _In_ float minHeightAboveFloor,
    _In_ float minFacingClearance,
    _In_ int locationCount,
    _Inout_ Dll_Interface::TopologyResult* locationData)
```

<span data-ttu-id="25d66-207">Chacune de ces requêtes prend un tableau alloué au préalable de structures de « TopologyResult ».</span><span class="sxs-lookup"><span data-stu-id="25d66-207">Each of these queries takes a pre-allocated array of “TopologyResult” structures.</span></span> <span data-ttu-id="25d66-208">Le paramètre « locationCount » spécifie la longueur du tableau transmis.</span><span class="sxs-lookup"><span data-stu-id="25d66-208">The “locationCount” parameter specifies the length of the passed in array.</span></span> <span data-ttu-id="25d66-209">La valeur de retour indique le nombre d’emplacements retournés.</span><span class="sxs-lookup"><span data-stu-id="25d66-209">The return value reports the number of returned locations.</span></span> <span data-ttu-id="25d66-210">Ce nombre n’est jamais supérieur à passé dans le paramètre de « locationCount ».</span><span class="sxs-lookup"><span data-stu-id="25d66-210">This number is never greater than the passed in “locationCount” parameter.</span></span>

<span data-ttu-id="25d66-211">Le « TopologyResult » contient la position centrale du volume retourné, la direction accessibles (par exemple, normale) et les dimensions de l’espace est trouvé.</span><span class="sxs-lookup"><span data-stu-id="25d66-211">The “TopologyResult” contains the center position of the returned volume, the facing direction (i.e. normal), and the dimensions of the found space.</span></span>

```cpp
struct TopologyResult 
{ 
    DirectX::XMFLOAT3 position; 
    DirectX::XMFLOAT3 normal; 
    float width; 
    float length;
};
```

<span data-ttu-id="25d66-212">Notez que dans l’exemple Unity, chacune de ces requêtes est lié à un bouton dans le panneau de l’interface utilisateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="25d66-212">Note that in the Unity sample, each of these queries is linked up to a button in the virtual UI panel.</span></span> <span data-ttu-id="25d66-213">L’exemple dur codes les paramètres pour chacune de ces requêtes à des valeurs raisonnables.</span><span class="sxs-lookup"><span data-stu-id="25d66-213">The sample hard codes the parameters for each of these queries to reasonable values.</span></span> <span data-ttu-id="25d66-214">Dans l’exemple de code pour plus d’exemples, consultez SpaceVisualizer.cs.</span><span class="sxs-lookup"><span data-stu-id="25d66-214">See SpaceVisualizer.cs in the sample code for more examples.</span></span>

### <a name="shape-queries"></a><span data-ttu-id="25d66-215">Requêtes de forme</span><span class="sxs-lookup"><span data-stu-id="25d66-215">Shape Queries</span></span>

<span data-ttu-id="25d66-216">À l’intérieur de la dll, l’Analyseur de forme (« ShapeAnalyzer_W ») utilise l’Analyseur de topologie à mettre en correspondance des formes personnalisées définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="25d66-216">Inside of the dll, the shape analyzer (“ShapeAnalyzer_W”) uses the topology analyzer to match against custom shapes defined by the user.</span></span> <span data-ttu-id="25d66-217">L’exemple Unity définit un ensemble de formes et expose les résultats vers l’extérieur via le menu de la requête de dans l’application, dans l’onglet de la forme. L’intention est que l’utilisateur peut définir leurs propres requêtes de forme d’objet et rendre utiliser d'entre eux, selon les besoins de leur application.</span><span class="sxs-lookup"><span data-stu-id="25d66-217">The Unity sample defines a set of shapes and exposes the results out through the in-app query menu, within the shape tab. The intention is that the user can define their own object shape queries and make use of those, as needed by their application.</span></span>

<span data-ttu-id="25d66-218">Notez que l’analyse de la forme fonctionne sur les surfaces horizontales uniquement.</span><span class="sxs-lookup"><span data-stu-id="25d66-218">Note that the shape analysis works on horizontal surfaces only.</span></span> <span data-ttu-id="25d66-219">Un canapé, par exemple, est défini par l’assise plat et haut plat de retour le canapé.</span><span class="sxs-lookup"><span data-stu-id="25d66-219">A couch, for example, is defined by the flat seat surface and the flat top of the couch back.</span></span> <span data-ttu-id="25d66-220">La requête shape recherche deux surfaces d’une plage de taille, la hauteur et aspect spécifique, avec les deux surfaces alignée et connecté.</span><span class="sxs-lookup"><span data-stu-id="25d66-220">The shape query looks for two surfaces of a specific size, height, and aspect range, with the two surfaces aligned and connected.</span></span> <span data-ttu-id="25d66-221">À l’aide de la terminologie de l’API, le siège de canapé et le haut précédent sont des composants de la forme et les exigences d’alignement sont des contraintes de composant de forme.</span><span class="sxs-lookup"><span data-stu-id="25d66-221">Using the APIs terminology, the couch seat and back top are shape components and the alignment requirements are shape component constraints.</span></span>

<span data-ttu-id="25d66-222">Voici un exemple de requête définie dans l’exemple de Unity (ShapeDefinition.cs), pour les objets « sittable ».</span><span class="sxs-lookup"><span data-stu-id="25d66-222">An example query defined in the Unity sample (ShapeDefinition.cs), for “sittable” objects is as follows.</span></span>

```cs
shapeComponents = new List<ShapeComponent>()
{
    new ShapeComponent(
        new List<ShapeComponentConstraint>()
        {
            ShapeComponentConstraint.Create_SurfaceHeight_Between(0.2f, 0.6f),
            ShapeComponentConstraint.Create_SurfaceCount_Min(1),
            ShapeComponentConstraint.Create_SurfaceArea_Min(0.035f),
        }
    ),
};
AddShape("Sittable", shapeComponents);
```

<span data-ttu-id="25d66-223">Chaque requête shape est défini par un ensemble de composants de forme, chacun avec un ensemble de contraintes de composant et un ensemble de contraintes de forme qui établissement des dépendances entre les composants.</span><span class="sxs-lookup"><span data-stu-id="25d66-223">Each shape query is defined by a set of shape components, each with a set of component constraints and a set of shape constraints which listing dependencies between the components.</span></span> <span data-ttu-id="25d66-224">Cet exemple inclut trois contraintes dans une définition de composant unique et aucune contrainte de forme entre les composants (comme il n’existe qu’un seul composant).</span><span class="sxs-lookup"><span data-stu-id="25d66-224">This example includes three constraints in a single component definition and no shape constraints between components (as there is only one component).</span></span>

<span data-ttu-id="25d66-225">En revanche, la forme de canapé a deux composants de forme et quatre contraintes de forme.</span><span class="sxs-lookup"><span data-stu-id="25d66-225">In contrast, the couch shape has two shape components and four shape constraints.</span></span> <span data-ttu-id="25d66-226">Notez que les composants sont identifiés par leur index dans la liste des composants de l’utilisateur (0 et 1 dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="25d66-226">Note that components are identified by their index in the user’s component list (0 and 1 in this example).</span></span>

```cs
shapeConstraints = new List<ShapeConstraint>()
{
    ShapeConstraint.Create_RectanglesSameLength(0, 1, 0.6f),
    ShapeConstraint.Create_RectanglesParallel(0, 1),
    ShapeConstraint.Create_RectanglesAligned(0, 1, 0.3f),
    ShapeConstraint.Create_AtBackOf(1, 0),
};
```

<span data-ttu-id="25d66-227">Fonctions de wrapper sont fournies dans le module Unity pour simplifier la création de définitions de formes personnalisée.</span><span class="sxs-lookup"><span data-stu-id="25d66-227">Wrapper functions are provided in the Unity module for easy creation of custom shape definitions.</span></span> <span data-ttu-id="25d66-228">Vous trouverez la liste complète des contraintes de composant et de forme dans « SpatialUnderstandingDll.cs » dans le « ShapeComponentConstraint » et les structures de « ShapeConstraint ».</span><span class="sxs-lookup"><span data-stu-id="25d66-228">The full list of component and shape constraints can be found in “SpatialUnderstandingDll.cs” within the “ShapeComponentConstraint” and the “ShapeConstraint” structures.</span></span>

<span data-ttu-id="25d66-229">![Forme de rectangle se trouve sur cette surface](images/su-shapequery-300px.jpg)</span><span class="sxs-lookup"><span data-stu-id="25d66-229">![Rectangle shape is found on this surface](images/su-shapequery-300px.jpg)</span></span><br>
<span data-ttu-id="25d66-230">*Forme de rectangle se trouve sur cette surface*</span><span class="sxs-lookup"><span data-stu-id="25d66-230">*Rectangle shape is found on this surface*</span></span>

### <a name="object-placement-solver"></a><span data-ttu-id="25d66-231">Solveur de sélection élective d’objet</span><span class="sxs-lookup"><span data-stu-id="25d66-231">Object Placement Solver</span></span>

<span data-ttu-id="25d66-232">Le solveur de sélection élective d’objet peut être utilisé pour identifier les emplacements idéale dans la salle physique pour placer vos objets.</span><span class="sxs-lookup"><span data-stu-id="25d66-232">The object placement solver can be used to identify ideal locations in the physical room to place your objects.</span></span> <span data-ttu-id="25d66-233">Le Solveur trouve le conviennent le mieux à l’emplacement donné les règles de l’objet et les contraintes.</span><span class="sxs-lookup"><span data-stu-id="25d66-233">The solver will find the best fit location given the object rules and constraints.</span></span> <span data-ttu-id="25d66-234">En outre, les requêtes d’objet persistent jusqu'à ce que l’objet est supprimé avec « Solver_RemoveObject » ou d’appels « Solver_RemoveAllObjects », ce qui contraint placement d’objets multiples.</span><span class="sxs-lookup"><span data-stu-id="25d66-234">In addition, object queries persist until the object is removed with “Solver_RemoveObject” or “Solver_RemoveAllObjects” calls, allowing constrained multi-object placement.</span></span> <span data-ttu-id="25d66-235">Requêtes de sélection élective d’objets se composent de trois parties : le type d’emplacement avec les paramètres, une liste de règles et une liste de contraintes.</span><span class="sxs-lookup"><span data-stu-id="25d66-235">Objects placement queries consist of three parts: placement type with parameters, a list of rules, and a list of constraints.</span></span> <span data-ttu-id="25d66-236">Pour exécuter une requête, utilisez l’API suivante.</span><span class="sxs-lookup"><span data-stu-id="25d66-236">To run a query, use the following API.</span></span>

```cpp
public static int Solver_PlaceObject(
            [In] string objectName,
            [In] IntPtr placementDefinition,        // ObjectPlacementDefinition
            [In] int placementRuleCount,
            [In] IntPtr placementRules,             // ObjectPlacementRule
            [In] int constraintCount,
            [In] IntPtr placementConstraints,       // ObjectPlacementConstraint
            [Out] IntPtr placementResult)
```

<span data-ttu-id="25d66-237">Cette fonction accepte un nom d’objet, définition de placement et une liste des règles et des contraintes.</span><span class="sxs-lookup"><span data-stu-id="25d66-237">This function takes an object name, placement definition, and a list of rules and constraints.</span></span> <span data-ttu-id="25d66-238">Le C# wrappers fournit des fonctions d’assistance pour faciliter la construction de règle et de contrainte de construction.</span><span class="sxs-lookup"><span data-stu-id="25d66-238">The C# wrappers provides construction helper functions to make rule and constraint construction easy.</span></span> <span data-ttu-id="25d66-239">La définition de placement contient le type de requête : autrement dit, une des opérations suivantes.</span><span class="sxs-lookup"><span data-stu-id="25d66-239">The placement definition contains the query type – that is, one of the following.</span></span>

```cpp
public enum PlacementType
            {
                Place_OnFloor,
                Place_OnWall,
                Place_OnCeiling,
                Place_OnShape,
                Place_OnEdge,
                Place_OnFloorAndCeiling,
                Place_RandomInAir,
                Place_InMidAir,
                Place_UnderFurnitureEdge,
            };
```

<span data-ttu-id="25d66-240">Chacun des types de sélection élective a un ensemble de paramètres uniques pour le type.</span><span class="sxs-lookup"><span data-stu-id="25d66-240">Each of the placement types has a set of parameters unique to the type.</span></span> <span data-ttu-id="25d66-241">La structure « ObjectPlacementDefinition » contient un ensemble de fonctions d’assistance statiques pour la création de ces définitions.</span><span class="sxs-lookup"><span data-stu-id="25d66-241">The “ObjectPlacementDefinition” structure contains a set of static helper functions for creating these definitions.</span></span> <span data-ttu-id="25d66-242">Par exemple, pour rechercher un emplacement pour placer un objet sur le sol, vous pouvez utiliser la fonction suivante.</span><span class="sxs-lookup"><span data-stu-id="25d66-242">For example, to find a place to put an object on the floor, you can use the following function.</span></span> <span data-ttu-id="25d66-243">publique statique ObjectPlacementDefinition Create_OnFloor(Vector3 halfDims) en plus du type de placement, vous pouvez fournir un ensemble de règles et des contraintes.</span><span class="sxs-lookup"><span data-stu-id="25d66-243">public static ObjectPlacementDefinition Create_OnFloor(Vector3 halfDims) In addition to the placement type, you can provide a set of rules and constraints.</span></span> <span data-ttu-id="25d66-244">Des règles ne peut pas être violées.</span><span class="sxs-lookup"><span data-stu-id="25d66-244">Rules cannot be violated.</span></span> <span data-ttu-id="25d66-245">Emplacements de positionnement possibles qui satisfont les type et les règles sont ensuite optimisés par rapport au jeu de contraintes afin de sélectionner l’emplacement de placement optimal.</span><span class="sxs-lookup"><span data-stu-id="25d66-245">Possible placement locations that satisfy the type and rules are then optimized against the set of constraints in order to select the optimal placement location.</span></span> <span data-ttu-id="25d66-246">Chacune des règles et des contraintes peut être créé par les fonctions de création statique fourni.</span><span class="sxs-lookup"><span data-stu-id="25d66-246">Each of the rules and constraints can be created by the provided static creation functions.</span></span> <span data-ttu-id="25d66-247">Vous trouverez ci-dessous un exemple de fonction construction règle et de contrainte.</span><span class="sxs-lookup"><span data-stu-id="25d66-247">An example rule and constraint construction function is provided below.</span></span>

```cs
public static ObjectPlacementRule Create_AwayFromPosition(
    Vector3 position, float minDistance)
public static ObjectPlacementConstraint Create_NearPoint(
    Vector3 position, float minDistance = 0.0f, float maxDistance = 0.0f)
```

<span data-ttu-id="25d66-248">La recherche se trouve sous objet requête de sélection élective pour un emplacement pour placer un cube de moitié compteur sur le bord d’une surface, autre précédemment placer des objets et près du centre de la salle.</span><span class="sxs-lookup"><span data-stu-id="25d66-248">The below object placement query is looking for a place to put a half meter cube on the edge of a surface, away from other previously place objects and near the center of the room.</span></span>

```cs
List<ObjectPlacementRule> rules = 
    new List<ObjectPlacementRule>() {
        ObjectPlacementRule.Create_AwayFromOtherObjects(1.0f),
    };

List<ObjectPlacementConstraint> constraints = 
    new List<ObjectPlacementConstraint> {
        ObjectPlacementConstraint.Create_NearCenter(),
    };

Solver_PlaceObject(
    “MyCustomObject”,
    new ObjectPlacementDefinition.Create_OnEdge(
        new Vector3(0.25f, 0.25f, 0.25f), 
        new Vector3(0.25f, 0.25f, 0.25f)),
    rules.Count,
    UnderstandingDLL.PinObject(rules.ToArray()),
    constraints.Count,
    UnderstandingDLL.PinObject(constraints.ToArray()),
    UnderstandingDLL.GetStaticObjectPlacementResultPtr());
```

<span data-ttu-id="25d66-249">En cas de réussite, une structure « ObjectPlacementResult » contenant la position de la sélection élective, dimensions et l’orientation est retournée.</span><span class="sxs-lookup"><span data-stu-id="25d66-249">If successful, a “ObjectPlacementResult” structure containing the placement position, dimensions and orientation is returned.</span></span> <span data-ttu-id="25d66-250">En outre, le positionnement est ajouté à la liste interne de la dll d’objets placés.</span><span class="sxs-lookup"><span data-stu-id="25d66-250">In addition, the placement is added to the dll’s internal list of placed objects.</span></span> <span data-ttu-id="25d66-251">Requêtes de sélection élective ultérieures prennent cet objet en compte.</span><span class="sxs-lookup"><span data-stu-id="25d66-251">Subsequent placement queries will take this object into account.</span></span> <span data-ttu-id="25d66-252">Le fichier « LevelSolver.cs » dans l’exemple Unity contient plusieurs exemples de requêtes.</span><span class="sxs-lookup"><span data-stu-id="25d66-252">The “LevelSolver.cs” file in the Unity sample contains more example queries.</span></span>

<span data-ttu-id="25d66-253">![Résultats du placement des objets](images/su-objectplacement-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="25d66-253">![Results of object placement](images/su-objectplacement-1000px.jpg)</span></span><br>
<span data-ttu-id="25d66-254">*Figure 3 : Le bleu boîtes de fonctionnement des requêtes avec le résultat à partir de trois endroits sur sol en dehors des règles de position de la caméra*</span><span class="sxs-lookup"><span data-stu-id="25d66-254">*Figure 3: The blue boxes how the result from three place on floor queries with away from camera position rules*</span></span>

<span data-ttu-id="25d66-255">Lors de la résolution pour l’emplacement du positionnement de plusieurs objets requis pour un scénario de niveau ou de l’application, tout d’abord résoudre indispensables et de grande taille des objets dans l’ordre à l’optimisation de la probabilité qu’un espace peut être trouvé.</span><span class="sxs-lookup"><span data-stu-id="25d66-255">When solving for placement location of multiple objects required for a level or application scenario, first solve indispensable and large objects in order to maximizing the probability that a space can be found.</span></span> <span data-ttu-id="25d66-256">Ordre de sélection élective est important.</span><span class="sxs-lookup"><span data-stu-id="25d66-256">Placement order is important.</span></span> <span data-ttu-id="25d66-257">Si le placement de l’objet est introuvable, essayez de configurations moins limitées.</span><span class="sxs-lookup"><span data-stu-id="25d66-257">If object placements cannot be found, try less constrained configurations.</span></span> <span data-ttu-id="25d66-258">Il est essentiel de prenant en charge des fonctionnalités sur de nombreuses configurations de salle de disposer d’un ensemble de configurations de secours.</span><span class="sxs-lookup"><span data-stu-id="25d66-258">Having a set of fallback configurations is critical to supporting functionality across many room configurations.</span></span>

### <a name="room-scanning-process"></a><span data-ttu-id="25d66-259">Processus d’analyse salle</span><span class="sxs-lookup"><span data-stu-id="25d66-259">Room Scanning Process</span></span>

<span data-ttu-id="25d66-260">Alors que la solution de mappage spatial fournie par le HoloLens est conçue pour être suffisamment générique pour répondre aux besoins de toute la gamme des espaces de problème, le module de présentation spatial a été créé pour prendre en charge les besoins de deux jeux spécifiques.</span><span class="sxs-lookup"><span data-stu-id="25d66-260">While the spatial mapping solution provided by the HoloLens is designed to be generic enough to meet the needs of the entire gamut of problem spaces, the spatial understanding module was built to support the needs of two specific games.</span></span> <span data-ttu-id="25d66-261">Sa solution est structurée autour d’un processus spécifique et des hypothèses, résumées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="25d66-261">Its solution is structured around a specific process and set of assumptions, summarized below.</span></span>

```
Fixed size playspace – The user specifies the maximum playspace size in the init call.

One-time scan process – 
    The process requires a discrete scanning phase where the user walks around,
    defining the playspace. 
    Query functions will not function until after the scan has been finalized.
```

<span data-ttu-id="25d66-262">Par playspace « peinture » – pendant la phase d’analyse, l’utilisateur, l’utilisateur déplace et recherche autour de la lecture du son propre rythme, peinture efficacement les zones qui doivent être incluses.</span><span class="sxs-lookup"><span data-stu-id="25d66-262">User driven playspace “painting” – During the scanning phase, the user moves and looks around the plays pace, effectively painting the areas which should be included.</span></span> <span data-ttu-id="25d66-263">Le maillage généré est important de fournir des commentaires des utilisateurs durant cette phase.</span><span class="sxs-lookup"><span data-stu-id="25d66-263">The generated mesh is important to provide user feedback during this phase.</span></span> <span data-ttu-id="25d66-264">À l’intérieur d’accueil ou d’installation office : la requête de fonctions sont conçues autour des surfaces plats et des murs à angle droit.</span><span class="sxs-lookup"><span data-stu-id="25d66-264">Indoors home or office setup – The query functions are designed around flat surfaces and walls at right angles.</span></span> <span data-ttu-id="25d66-265">Il s’agit d’une limitation logicielle.</span><span class="sxs-lookup"><span data-stu-id="25d66-265">This is a soft limitation.</span></span> <span data-ttu-id="25d66-266">Toutefois, pendant la phase d’analyse, une analyse de l’axe principal est prévue pour optimiser le pavage de maille le long de l’axe principal et secondaire.</span><span class="sxs-lookup"><span data-stu-id="25d66-266">However, during the scanning phase, a primary axis analysis is completed to optimize the mesh tessellation along major and minor axis.</span></span> <span data-ttu-id="25d66-267">Le fichier SpatialUnderstanding.cs inclus gère le processus phase d’analyse.</span><span class="sxs-lookup"><span data-stu-id="25d66-267">The included SpatialUnderstanding.cs file manages the scanning phase process.</span></span> <span data-ttu-id="25d66-268">Il appelle les fonctions suivantes.</span><span class="sxs-lookup"><span data-stu-id="25d66-268">It calls the following functions.</span></span>

```
SpatialUnderstanding_Init – Called once at the start.

GeneratePlayspace_InitScan – Indicates that the scan phase should begin.

GeneratePlayspace_UpdateScan_DynamicScan – 
    Called each frame to update the scanning process. The camera position and 
    orientation is passed in and is used for the playspace painting process, 
    described above.

GeneratePlayspace_RequestFinish – 
    Called to finalize the playspace. This will use the areas “painted” during 
    the scan phase to define and lock the playspace. The application can query 
    statistics during the scanning phase as well as query the custom mesh for 
    providing user feedback.

Import_UnderstandingMesh – 
    During scanning, the “SpatialUnderstandingCustomMesh” behavior provided by 
    the module and placed on the understanding prefab will periodically query the 
    custom mesh generated by the process. In addition, this is done once more 
    after scanning has been finalized.
```

<span data-ttu-id="25d66-269">Le flux analyse, piloté par le comportement de « SpatialUnderstanding » appelle InitScan, puis UpdateScan chaque frame.</span><span class="sxs-lookup"><span data-stu-id="25d66-269">The scanning flow, driven by the “SpatialUnderstanding” behavior calls InitScan, then UpdateScan each frame.</span></span> <span data-ttu-id="25d66-270">Lorsque la requête de statistiques signale la couverture du raisonnable, l’utilisateur est autorisé à airtap pour appeler RequestFinish pour indiquer la fin de la phase d’analyse.</span><span class="sxs-lookup"><span data-stu-id="25d66-270">When the statistics query reports reasonable coverage, the user is allowed to airtap to call RequestFinish to indicate the end of the scanning phase.</span></span> <span data-ttu-id="25d66-271">UpdateScan continue à être appelée jusqu'à ce qu’il s’agit de retour la valeur indique que la dll a terminé le traitement.</span><span class="sxs-lookup"><span data-stu-id="25d66-271">UpdateScan continues to be called until it’s return value indicates that the dll has completed processing.</span></span>

### <a name="understanding-mesh"></a><span data-ttu-id="25d66-272">Maillage de présentation</span><span class="sxs-lookup"><span data-stu-id="25d66-272">Understanding Mesh</span></span>

<span data-ttu-id="25d66-273">La dll de présentation stocke en interne la playspace sous forme de grille des cubes de voxel 8cm en taille réelle.</span><span class="sxs-lookup"><span data-stu-id="25d66-273">The understanding dll internally stores the playspace as a grid of 8cm sized voxel cubes.</span></span> <span data-ttu-id="25d66-274">Au cours de la partie initiale d’analyse, une analyse du composant principal est terminée pour déterminer les axes de la salle.</span><span class="sxs-lookup"><span data-stu-id="25d66-274">During the initial part of scanning, a primary component analysis is completed to determine the axes of the room.</span></span> <span data-ttu-id="25d66-275">En interne, elle stocke son espace voxel alignée sur ces axes.</span><span class="sxs-lookup"><span data-stu-id="25d66-275">Internally, it stores its voxel space aligned to these axes.</span></span> <span data-ttu-id="25d66-276">Une maille est générée environ toutes les secondes en extrayant l’isosurface le volume voxel.</span><span class="sxs-lookup"><span data-stu-id="25d66-276">A mesh is generated approximately every second by extracting the isosurface from the voxel volume.</span></span> 

<span data-ttu-id="25d66-277">![Panneau généré produites à partir du volume voxel](images/su-custommesh.jpg)</span><span class="sxs-lookup"><span data-stu-id="25d66-277">![Generated mesh produced from the voxel volume](images/su-custommesh.jpg)</span></span><br>
<span data-ttu-id="25d66-278">*Panneau généré produites à partir du volume voxel*</span><span class="sxs-lookup"><span data-stu-id="25d66-278">*Generated mesh produced from the voxel volume*</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="25d66-279">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="25d66-279">Troubleshooting</span></span>
* <span data-ttu-id="25d66-280">Assurez-vous que vous avez défini le [SpatialPerception](#setting-the-spatialperception-capability) fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="25d66-280">Ensure you have set the [SpatialPerception](#setting-the-spatialperception-capability) capability</span></span>
* <span data-ttu-id="25d66-281">En cas de perte de suivi, l’événement OnSurfaceChanged suivant supprime toutes les mailles.</span><span class="sxs-lookup"><span data-stu-id="25d66-281">When tracking is lost, the next OnSurfaceChanged event will remove all meshes.</span></span>

## <a name="spatial-mapping-in-mixed-reality-toolkit"></a><span data-ttu-id="25d66-282">Mappage spatial dans le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="25d66-282">Spatial Mapping in Mixed Reality Toolkit</span></span>
<span data-ttu-id="25d66-283">Pour plus d’informations sur l’utilisation de mappage Spatial avec v2 Toolkit de réalité mixte, consultez le <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/SpatialAwareness/SpatialAwarenessGettingStarted.html" target="_blank">section de la reconnaissance spatiale</a> des documents MRTK.</span><span class="sxs-lookup"><span data-stu-id="25d66-283">For more information on using Spatial Mapping with Mixed Reality Toolkit v2, see the <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/SpatialAwareness/SpatialAwarenessGettingStarted.html" target="_blank">Spatial Awareness section</a> of the MRTK docs.</span></span>

## <a name="see-also"></a><span data-ttu-id="25d66-284">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="25d66-284">See also</span></span>
* [<span data-ttu-id="25d66-285">MR 230 spatiale : Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="25d66-285">MR Spatial 230: Spatial mapping</span></span>](holograms-230.md)
* [<span data-ttu-id="25d66-286">Systèmes de coordonnées</span><span class="sxs-lookup"><span data-stu-id="25d66-286">Coordinate systems</span></span>](coordinate-systems.md)
* [<span data-ttu-id="25d66-287">Systèmes de coordonnées dans Unity</span><span class="sxs-lookup"><span data-stu-id="25d66-287">Coordinate systems in Unity</span></span>](coordinate-systems-in-unity.md)
* <span data-ttu-id="25d66-288"><a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">MixedRealityToolkit</a></span><span class="sxs-lookup"><span data-stu-id="25d66-288"><a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">MixedRealityToolkit</a></span></span>
* <span data-ttu-id="25d66-289"><a href="http://docs.unity3d.com/ScriptReference/MeshFilter.html" target="_blank">UnityEngine.MeshFilter</a></span><span class="sxs-lookup"><span data-stu-id="25d66-289"><a href="http://docs.unity3d.com/ScriptReference/MeshFilter.html" target="_blank">UnityEngine.MeshFilter</a></span></span>
* <span data-ttu-id="25d66-290"><a href="http://docs.unity3d.com/ScriptReference/MeshCollider.html" target="_blank">UnityEngine.MeshCollider</a></span><span class="sxs-lookup"><span data-stu-id="25d66-290"><a href="http://docs.unity3d.com/ScriptReference/MeshCollider.html" target="_blank">UnityEngine.MeshCollider</a></span></span>
* <span data-ttu-id="25d66-291"><a href="http://docs.unity3d.com/ScriptReference/Bounds.html" target="_blank">UnityEngine.Bounds</a></span><span class="sxs-lookup"><span data-stu-id="25d66-291"><a href="http://docs.unity3d.com/ScriptReference/Bounds.html" target="_blank">UnityEngine.Bounds</a></span></span>
