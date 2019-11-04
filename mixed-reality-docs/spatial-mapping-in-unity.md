---
title: Mappage spatial dans Unity
description: Rendu et collision avec la géométrie réelle autour de vous dans Unity.
author: davidkline-ms
ms.author: davidkl
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, mappage spatial, convertisseur, conflit, maillage, numérisation, composant
ms.openlocfilehash: 452e629a877df585ffbc0a6466ffeb2588b66ecf
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438034"
---
# <a name="spatial-mapping-in-unity"></a><span data-ttu-id="61079-104">Mappage spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="61079-104">Spatial mapping in Unity</span></span>

<span data-ttu-id="61079-105">Cette rubrique explique comment utiliser le [mappage spatial](spatial-mapping.md) dans votre projet Unity, en récupérant les maillages de triangles qui représentent les surfaces dans le monde autour d’un appareil HoloLens, pour le placement, l’occlusion, l’analyse de la salle, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="61079-105">This topic describes how to use [spatial mapping](spatial-mapping.md) in your Unity project, retrieving triangle meshes that represent the surfaces in the world around a HoloLens device, for placement, occlusion, room analysis and more.</span></span>

<span data-ttu-id="61079-106">Unity comprend la prise en charge complète du mappage spatial, qui est exposé aux développeurs des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="61079-106">Unity includes full support for spatial mapping, which is exposed to developers in the following ways:</span></span>
1. <span data-ttu-id="61079-107">Composants de mappage spatial disponibles dans MixedRealityToolkit, qui fournissent un chemin d’accès pratique et rapide pour la prise en main du mappage spatial</span><span class="sxs-lookup"><span data-stu-id="61079-107">Spatial mapping components available in the MixedRealityToolkit, which provide a convenient and rapid path for getting started with spatial mapping</span></span>
2. <span data-ttu-id="61079-108">API de mappage spatial de niveau inférieur, qui fournissent un contrôle total et permettent une personnalisation plus sophistiquée des applications</span><span class="sxs-lookup"><span data-stu-id="61079-108">Lower-level spatial mapping APIs, which provide full control and enable more sophisticated application specific customization</span></span>

<span data-ttu-id="61079-109">Pour utiliser le mappage spatial dans votre application, vous devez définir la capacité spatialPerception dans votre AppxManifest.</span><span class="sxs-lookup"><span data-stu-id="61079-109">To use spatial mapping in your app, the spatialPerception capability needs to be set in your AppxManifest.</span></span>

## <a name="device-support"></a><span data-ttu-id="61079-110">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="61079-110">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="61079-111"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="61079-111"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="61079-112"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="61079-112"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="61079-113"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="61079-113"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="61079-114"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="61079-114"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="61079-115">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="61079-115">Spatial mapping</span></span></td>
        <td><span data-ttu-id="61079-116">✔️</span><span class="sxs-lookup"><span data-stu-id="61079-116">✔️</span></span></td>
        <td><span data-ttu-id="61079-117">✔️</span><span class="sxs-lookup"><span data-stu-id="61079-117">✔️</span></span></td>
        <td>❌</td>
    </tr>
</table>

## <a name="setting-the-spatialperception-capability"></a><span data-ttu-id="61079-118">Définition de la fonctionnalité SpatialPerception</span><span class="sxs-lookup"><span data-stu-id="61079-118">Setting the SpatialPerception capability</span></span>

<span data-ttu-id="61079-119">Pour qu’une application consomme des données de mappage spatiales, la capacité SpatialPerception doit être activée.</span><span class="sxs-lookup"><span data-stu-id="61079-119">In order for an app to consume spatial mapping data, the SpatialPerception capability must be enabled.</span></span>

<span data-ttu-id="61079-120">Comment activer la fonctionnalité SpatialPerception :</span><span class="sxs-lookup"><span data-stu-id="61079-120">How to enable the SpatialPerception capability:</span></span>
1. <span data-ttu-id="61079-121">Dans l’éditeur Unity, ouvrez le volet **« paramètres du lecteur »** (modifier > paramètres du projet > Player)</span><span class="sxs-lookup"><span data-stu-id="61079-121">In the Unity Editor, open the **"Player Settings"** pane (Edit > Project Settings > Player)</span></span>
2. <span data-ttu-id="61079-122">Cliquer sur l’onglet **« Windows Store »**</span><span class="sxs-lookup"><span data-stu-id="61079-122">Click on the **"Windows Store"** tab</span></span>
3. <span data-ttu-id="61079-123">Développez **« paramètres de publication »** et cochez la fonctionnalité **« SpatialPerception »** dans la liste **« fonctionnalités »** .</span><span class="sxs-lookup"><span data-stu-id="61079-123">Expand **"Publishing Settings"** and check the **"SpatialPerception"** capability in the **"Capabilities"** list</span></span>

<span data-ttu-id="61079-124">Notez que si vous avez déjà exporté votre projet Unity vers une solution Visual Studio, vous devez soit exporter vers un nouveau dossier, soit [définir manuellement cette fonctionnalité dans AppxManifest dans Visual Studio](spatial-mapping-in-directx.md#set-up-your-app-to-use-the-spatialperception-capability).</span><span class="sxs-lookup"><span data-stu-id="61079-124">Note that if you have already exported your Unity project to a Visual Studio solution, you will need to either export to a new folder or manually [set this capability in the AppxManifest in Visual Studio](spatial-mapping-in-directx.md#set-up-your-app-to-use-the-spatialperception-capability).</span></span>

<span data-ttu-id="61079-125">Le mappage spatial nécessite également un MaxVersionTested d’au moins 10.0.10586.0 :</span><span class="sxs-lookup"><span data-stu-id="61079-125">Spatial mapping also requires a MaxVersionTested of at least 10.0.10586.0:</span></span>
1. <span data-ttu-id="61079-126">Dans Visual Studio, cliquez avec le bouton droit sur **Package. appxmanifest** dans le Explorateur de solutions puis sélectionnez **afficher le code** .</span><span class="sxs-lookup"><span data-stu-id="61079-126">In Visual Studio, right click on **Package.appxmanifest** in the Solution Explorer and select **View Code**</span></span>
2. <span data-ttu-id="61079-127">Recherchez la ligne qui spécifie **TargetDeviceFamily** et remplacez **MaxVersionTested = "10.0.10240.0"** par **MaxVersionTested = "10.0.10586.0"**</span><span class="sxs-lookup"><span data-stu-id="61079-127">Find the line specifying **TargetDeviceFamily** and change **MaxVersionTested="10.0.10240.0"** to **MaxVersionTested="10.0.10586.0"**</span></span>
3. <span data-ttu-id="61079-128">**Enregistrez** le package. appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="61079-128">**Save** the Package.appxmanifest.</span></span>

## <a name="getting-started-with-unitys-built-in-spatial-mapping-components"></a><span data-ttu-id="61079-129">Prise en main des composants de mappage spatial intégrés à Unity</span><span class="sxs-lookup"><span data-stu-id="61079-129">Getting started with Unity's built-in spatial mapping components</span></span>

<span data-ttu-id="61079-130">Unity offre 2 composants pour ajouter facilement le mappage spatial à votre application, le **convertisseur de mappage spatial** et le **conflit de mappage spatial**.</span><span class="sxs-lookup"><span data-stu-id="61079-130">Unity offers 2 components for easily adding spatial mapping to your app, **Spatial Mapping Renderer** and **Spatial Mapping Collider**.</span></span>

### <a name="spatial-mapping-renderer"></a><span data-ttu-id="61079-131">Convertisseur de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="61079-131">Spatial Mapping Renderer</span></span>

<span data-ttu-id="61079-132">Le convertisseur de mappage spatial permet la visualisation du maillage de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="61079-132">The Spatial Mapping Renderer allows for visualization of the spatial mapping mesh.</span></span>

![Convertisseur de mappage spatial dans Unity](images/spatialmappingrenderer.png)

### <a name="spatial-mapping-collider"></a><span data-ttu-id="61079-134">Conflit de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="61079-134">Spatial Mapping Collider</span></span>

<span data-ttu-id="61079-135">Le conflit de mappage spatial permet l’interaction entre le contenu holographique (ou le caractère), tel que la physique, avec le maillage de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="61079-135">The Spatial Mapping Collider allows for holographic content (or character) interaction, such as physics, with the spatial mapping mesh.</span></span>

![Conflit de mappage spatial dans Unity](images/spatialmappingcollider.png)

### <a name="using-the-built-in-spatial-mapping-components"></a><span data-ttu-id="61079-137">Utilisation des composants de mappage spatial intégrés</span><span class="sxs-lookup"><span data-stu-id="61079-137">Using the built-in spatial mapping components</span></span>

<span data-ttu-id="61079-138">Vous pouvez ajouter les deux composants à votre application si vous souhaitez visualiser et interagir avec les surfaces physiques.</span><span class="sxs-lookup"><span data-stu-id="61079-138">You may add both components to your app if you'd like to both visualize and interact with physical surfaces.</span></span>

<span data-ttu-id="61079-139">Pour utiliser ces deux composants dans votre application Unity :</span><span class="sxs-lookup"><span data-stu-id="61079-139">To use these two components in your Unity app:</span></span>
1. <span data-ttu-id="61079-140">Sélectionnez un GameObject au centre de la zone dans laquelle vous souhaitez détecter les maillages de surface spatiale.</span><span class="sxs-lookup"><span data-stu-id="61079-140">Select a GameObject at the center of the area in which you'd like to detect spatial surface meshes.</span></span>
2. <span data-ttu-id="61079-141">Dans la fenêtre de l’inspecteur, **Ajoutez le composant** >  > **XR** de **mappage spatial** ou le **convertisseur de mappage spatial**.</span><span class="sxs-lookup"><span data-stu-id="61079-141">In the Inspector window, **Add Component** > **XR** > **Spatial Mapping Collider** or **Spatial Mapping Renderer**.</span></span>

<span data-ttu-id="61079-142">Vous trouverez plus d’informations sur l’utilisation de ces composants sur le <a href="https://docs.unity3d.com/Manual/SpatialMappingComponents.html" target="_blank">site de documentation Unity</a>.</span><span class="sxs-lookup"><span data-stu-id="61079-142">You can find more details on how to use these components at the <a href="https://docs.unity3d.com/Manual/SpatialMappingComponents.html" target="_blank">Unity documentation site</a>.</span></span>

### <a name="going-beyond-the-built-in-spatial-mapping-components"></a><span data-ttu-id="61079-143">Aller au-delà des composants de mappage spatial intégrés</span><span class="sxs-lookup"><span data-stu-id="61079-143">Going beyond the built-in spatial mapping components</span></span>

<span data-ttu-id="61079-144">Ces composants facilitent le glisser-déplacer pour la prise en main du mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="61079-144">These components make it drag-and-drop easy to get started with Spatial Mapping.</span></span> <span data-ttu-id="61079-145"> Lorsque vous souhaitez aller plus loin, il existe deux chemins principaux à explorer :</span><span class="sxs-lookup"><span data-stu-id="61079-145"> When you want to go further, there are two main paths to explore:</span></span>
* <span data-ttu-id="61079-146">Pour effectuer votre propre traitement de maillage de niveau inférieur, consultez la section ci-dessous sur l’API de script de mappage spatial de bas niveau.</span><span class="sxs-lookup"><span data-stu-id="61079-146">To do your own lower-level mesh processing, see the section below about the low-level Spatial Mapping script API.</span></span>
* <span data-ttu-id="61079-147">Pour effectuer une analyse de maillage de niveau supérieur, consultez la section ci-dessous sur la bibliothèque SpatialUnderstanding dans <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialUnderstanding" target="_blank">MixedRealityToolkit</a>.</span><span class="sxs-lookup"><span data-stu-id="61079-147">To do higher-level mesh analysis, see the section below about the SpatialUnderstanding library in <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialUnderstanding" target="_blank">MixedRealityToolkit</a>.</span></span>

## <a name="using-the-low-level-unity-spatial-mapping-api"></a><span data-ttu-id="61079-148">Utilisation de l’API de mappage spatial de bas niveau</span><span class="sxs-lookup"><span data-stu-id="61079-148">Using the low-level Unity Spatial Mapping API</span></span>

<span data-ttu-id="61079-149">Si vous avez besoin d’un contrôle plus élevé que celui obtenu à partir du convertisseur de mappage spatial et des composants de conflit de mappage spatial, vous pouvez utiliser les API de script de mappage spatial de bas niveau.</span><span class="sxs-lookup"><span data-stu-id="61079-149">If you need more control than you get from the Spatial Mapping Renderer and Spatial Mapping Collider components, you can use the low-level Spatial Mapping script APIs.</span></span>

<span data-ttu-id="61079-150">**Espace de noms :** *UnityEngine. XR. WSA*</span><span class="sxs-lookup"><span data-stu-id="61079-150">**Namespace:** *UnityEngine.XR.WSA*</span></span><br>
<span data-ttu-id="61079-151">**Types**: *SurfaceObserver*, *SurfaceChange*, *SurfaceData*, *SurfaceId*</span><span class="sxs-lookup"><span data-stu-id="61079-151">**Types**: *SurfaceObserver*, *SurfaceChange*, *SurfaceData*, *SurfaceId*</span></span>

<span data-ttu-id="61079-152">Voici un aperçu du déroulement suggéré pour une application qui utilise les API de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="61079-152">The following is an outline of the suggested flow for an application that uses the spatial mapping APIs.</span></span>

### <a name="set-up-the-surfaceobservers"></a><span data-ttu-id="61079-153">Configurer le (s) SurfaceObserver (s)</span><span class="sxs-lookup"><span data-stu-id="61079-153">Set up the SurfaceObserver(s)</span></span>

<span data-ttu-id="61079-154">Instanciez un objet SurfaceObserver pour chaque région d’espace définie par l’application dont vous avez besoin pour les données de mappage spatiale.</span><span class="sxs-lookup"><span data-stu-id="61079-154">Instantiate one SurfaceObserver object for each application-defined region of space that you need spatial mapping data for.</span></span>

```cs
SurfaceObserver surfaceObserver;

 void Start () {
     surfaceObserver = new SurfaceObserver();
 }
```

<span data-ttu-id="61079-155">Spécifiez la région d’espace pour laquelle chaque objet SurfaceObserver fournira des données en appelant SetVolumeAsSphere, SetVolumeAsAxisAlignedBox, SetVolumeAsOrientedBox ou SetVolumeAsFrustum.</span><span class="sxs-lookup"><span data-stu-id="61079-155">Specify the region of space that each SurfaceObserver object will provide data for by calling either SetVolumeAsSphere, SetVolumeAsAxisAlignedBox, SetVolumeAsOrientedBox, or SetVolumeAsFrustum.</span></span> <span data-ttu-id="61079-156">Vous pouvez redéfinir la région de l’espace à l’avenir en appelant une nouvelle fois l’une de ces méthodes.</span><span class="sxs-lookup"><span data-stu-id="61079-156">You can redefine the region of space in the future by simply calling one of these methods again.</span></span>

```cs
void Start () {
    ...
     surfaceObserver.SetVolumeAsAxisAlignedBox(Vector3.zero, new Vector3(3, 3, 3));
}
```

<span data-ttu-id="61079-157">Quand vous appelez SurfaceObserver. Update (), vous devez fournir un gestionnaire pour chaque surface spatiale de la région du SurfaceObserver d’espace pour lequel le système de mappage spatial a de nouvelles informations.</span><span class="sxs-lookup"><span data-stu-id="61079-157">When you call SurfaceObserver.Update(), you must provide a handler for each spatial surface in the SurfaceObserver's region of space that the spatial mapping system has new information for.</span></span> <span data-ttu-id="61079-158">Le gestionnaire reçoit, pour une surface spatiale :</span><span class="sxs-lookup"><span data-stu-id="61079-158">The handler receives, for one spatial surface:</span></span>

```cs
private void OnSurfaceChanged(SurfaceId surfaceId, SurfaceChange changeType, Bounds bounds, System.DateTime updateTime)
 {
    //see Handling Surface Changes
 }
```

### <a name="handling-surface-changes"></a><span data-ttu-id="61079-159">Gestion des modifications de surface</span><span class="sxs-lookup"><span data-stu-id="61079-159">Handling Surface Changes</span></span>

<span data-ttu-id="61079-160">Il existe plusieurs cas principaux à gérer.</span><span class="sxs-lookup"><span data-stu-id="61079-160">There are several main cases to handle.</span></span> <span data-ttu-id="61079-161">Ajout de & mis à jour qui peut utiliser le même chemin de code et supprimé.</span><span class="sxs-lookup"><span data-stu-id="61079-161">Added & Updated which can use the same code path and Removed.</span></span>
* <span data-ttu-id="61079-162">Dans la & ajoutée cas mis à jour dans l’exemple, nous ajoutons ou obtenons le GameObject représentant ce maillage du dictionnaire, nous créons un struct SurfaceData avec les composants nécessaires, puis appelons RequestMeshDataAsync pour remplir le GameObject avec les données de maillage et position dans la scène.</span><span class="sxs-lookup"><span data-stu-id="61079-162">In the Added & Updated cases in the example, we add or get the GameObject representing this mesh from the dictionary, create a SurfaceData struct with the necessary components, then call RequestMeshDataAsync to populate the GameObject with the mesh data and position in the scene.</span></span>
* <span data-ttu-id="61079-163">Dans le cas supprimé, nous supprimons le GameObject représentant ce maillage du dictionnaire et le détruisons.</span><span class="sxs-lookup"><span data-stu-id="61079-163">In the Removed case, we remove the GameObject representing this mesh from the dictionary and destroy it.</span></span>

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

### <a name="handling-data-ready"></a><span data-ttu-id="61079-164">Gestion des données prêtes</span><span class="sxs-lookup"><span data-stu-id="61079-164">Handling Data Ready</span></span>

<span data-ttu-id="61079-165">Le gestionnaire OnDataReady reçoit un objet SurfaceData.</span><span class="sxs-lookup"><span data-stu-id="61079-165">The OnDataReady handler receives a SurfaceData object.</span></span> <span data-ttu-id="61079-166">Les objets WorldAnchor, MeshFilter et (facultatif) MeshCollider qu’il contient reflètent l’état le plus récent de la surface spatiale associée.</span><span class="sxs-lookup"><span data-stu-id="61079-166">The WorldAnchor, MeshFilter and (optionally) MeshCollider objects it contains reflect the latest state of the associated spatial surface.</span></span> <span data-ttu-id="61079-167">Effectuez éventuellement une analyse et/ou un [traitement](spatial-mapping.md#mesh-processing) des données de maillage en accédant au membre de maillage de l’objet MeshFilter.</span><span class="sxs-lookup"><span data-stu-id="61079-167">Optionally perform analysis and/or [processing](spatial-mapping.md#mesh-processing) of the mesh data by accessing the Mesh member of the MeshFilter object.</span></span> <span data-ttu-id="61079-168">Affichez la surface spatiale avec la dernière maille et (éventuellement) utilisez-la pour les collisions physiques et les raycasts.</span><span class="sxs-lookup"><span data-stu-id="61079-168">Render the spatial surface with the latest mesh and (optionally) use it for physics collisions and raycasts.</span></span> <span data-ttu-id="61079-169">Il est important de vérifier que le contenu du SurfaceData n’est pas null.</span><span class="sxs-lookup"><span data-stu-id="61079-169">It's important to confirm that the contents of the SurfaceData are not null.</span></span>

### <a name="start-processing-on-updates"></a><span data-ttu-id="61079-170">Démarrer le traitement des mises à jour</span><span class="sxs-lookup"><span data-stu-id="61079-170">Start processing on updates</span></span>

<span data-ttu-id="61079-171">SurfaceObserver. Update () doit être appelé sur un délai, et non sur tous les frames.</span><span class="sxs-lookup"><span data-stu-id="61079-171">SurfaceObserver.Update() should be called on a delay, not every frame.</span></span>

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

## <a name="higher-level-mesh-analysis-spatialunderstanding"></a><span data-ttu-id="61079-172">Analyse de maillage de niveau supérieur : SpatialUnderstanding</span><span class="sxs-lookup"><span data-stu-id="61079-172">Higher-level mesh analysis: SpatialUnderstanding</span></span>

<span data-ttu-id="61079-173">Le <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">MixedRealityToolkit</a> est une collection de code d’utilitaire utile pour le développement holographique reposant sur les API d’Unity holographique.</span><span class="sxs-lookup"><span data-stu-id="61079-173">The <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">MixedRealityToolkit</a> is a collection of helpful utility code for holographic development built upon the holographic Unity APIs.</span></span>

### <a name="spatial-understanding"></a><span data-ttu-id="61079-174">Compréhension spatiale</span><span class="sxs-lookup"><span data-stu-id="61079-174">Spatial Understanding</span></span>

<span data-ttu-id="61079-175">Quand vous placez des hologrammes dans le monde physique, il est souvent préférable d’aller au-delà des plans de maillage et de surface du mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="61079-175">When placing holograms in the physical world it is often desirable to go beyond spatial mapping’s mesh and surface planes.</span></span> <span data-ttu-id="61079-176">Une fois le placement effectué, il est souhaitable d’avoir un niveau de compréhension environnemental plus élevé.</span><span class="sxs-lookup"><span data-stu-id="61079-176">When placement is done procedurally, a higher level of environmental understanding is desirable.</span></span> <span data-ttu-id="61079-177">Il est généralement nécessaire de prendre des décisions sur le plancher, le plafond et les murs.</span><span class="sxs-lookup"><span data-stu-id="61079-177">This usually requires making decisions about what is floor, ceiling, and walls.</span></span> <span data-ttu-id="61079-178">En outre, il est possible d’optimiser par rapport à un ensemble de contraintes de placement pour déterminer les emplacements physiques les plus intéressants pour les objets holographiques.</span><span class="sxs-lookup"><span data-stu-id="61079-178">In addition, the ability to optimize against a set of placement constraints to determining the most desirable physical locations for holographic objects.</span></span>

<span data-ttu-id="61079-179">Pendant le développement de jeunes Conkers et fragments, Asobo Studios a rencontré ce problème en développant un solveur de salle à cet effet.</span><span class="sxs-lookup"><span data-stu-id="61079-179">During the development of Young Conker and Fragments, Asobo Studios faced this problem head on, developing a room solver for this purpose.</span></span> <span data-ttu-id="61079-180">Chacun de ces jeux avait des besoins spécifiques aux jeux, mais ils partageaient la technologie de compréhension spatiale principale.</span><span class="sxs-lookup"><span data-stu-id="61079-180">Each of these games had game specific needs, but they shared core spatial understanding technology.</span></span> <span data-ttu-id="61079-181">La bibliothèque HoloToolkit. SpatialUnderstanding encapsule cette technologie, ce qui vous permet de trouver rapidement des espaces vides sur les murs, de placer des objets sur le plafond, d’identifier le positionnement d’un personnage et une multitude d’autres requêtes de compréhension spatiale.</span><span class="sxs-lookup"><span data-stu-id="61079-181">The HoloToolkit.SpatialUnderstanding library encapsulates this technology, allowing you to quickly find empty spaces on the walls, place objects on the ceiling, identify placed for character to sit, and a myriad of other spatial understanding queries.</span></span>

<span data-ttu-id="61079-182">Tout le code source est inclus, ce qui vous permet de le personnaliser en fonction de vos besoins et de partager vos améliorations avec la communauté.</span><span class="sxs-lookup"><span data-stu-id="61079-182">All of the source code is included, allowing you to customize it to your needs and share your improvements with the community.</span></span> <span data-ttu-id="61079-183">Le code du C++ solveur a été encapsulé dans une dll UWP et exposé à Unity avec une chute de Prefab contenue dans le MixedRealityToolkit.</span><span class="sxs-lookup"><span data-stu-id="61079-183">The code for the C++ solver has been wrapped into a UWP dll and exposed to Unity with a drop in prefab contained within the MixedRealityToolkit.</span></span>

### <a name="understanding-modules"></a><span data-ttu-id="61079-184">Fonctionnement des modules</span><span class="sxs-lookup"><span data-stu-id="61079-184">Understanding Modules</span></span>

<span data-ttu-id="61079-185">Il existe trois interfaces principales exposées par le module : la topologie pour les requêtes spatiales et spatiales simples, la forme pour la détection d’objets et le solveur de positionnement des objets pour le positionnement basé sur les contraintes des jeux d’objets.</span><span class="sxs-lookup"><span data-stu-id="61079-185">There are three primary interfaces exposed by the module: topology for simple surface and spatial queries, shape for object detection, and the object placement solver for constraint based placement of object sets.</span></span> <span data-ttu-id="61079-186">Chacun d’eux est décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="61079-186">Each of these is described below.</span></span> <span data-ttu-id="61079-187">En plus des trois interfaces de module principales, une interface de type Ray peut être utilisée pour récupérer des types de surfaces avec balises et un maillage PlaySpace à l’eau personnalisé peut être copié.</span><span class="sxs-lookup"><span data-stu-id="61079-187">In addition to the three primary module interfaces, a ray casting interface can be used to retrieve tagged surface types and a custom watertight playspace mesh can be copied out.</span></span>

### <a name="ray-casting"></a><span data-ttu-id="61079-188">Conversion de rayon</span><span class="sxs-lookup"><span data-stu-id="61079-188">Ray Casting</span></span>

<span data-ttu-id="61079-189">Une fois la salle analysée et finalisée, les étiquettes sont générées en interne pour les surfaces comme le plancher, le plafond et les murs.</span><span class="sxs-lookup"><span data-stu-id="61079-189">After the room has been scanned and finalized, labels are internally generated for surfaces like the floor, ceiling, and walls.</span></span> <span data-ttu-id="61079-190">La fonction « PlayspaceRaycast » prend un rayon et retourne si le rayon entre en conflit avec une surface connue et, le cas échéant, des informations sur cette surface sous la forme d’un « RaycastResult ».</span><span class="sxs-lookup"><span data-stu-id="61079-190">The “PlayspaceRaycast” function takes a ray and returns if the ray collides with a known surface and if so, information about that surface in the form of a “RaycastResult”.</span></span>

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

<span data-ttu-id="61079-191">En interne, raycast est calculé par rapport à la représentation voxel 8cm cube calculée du PlaySpace.</span><span class="sxs-lookup"><span data-stu-id="61079-191">Internally, the raycast is computed against the computed 8cm cubed voxel representation of the playspace.</span></span> <span data-ttu-id="61079-192">Chaque voxel contient un ensemble d’éléments surface avec des données de topologie traitées (surfels).</span><span class="sxs-lookup"><span data-stu-id="61079-192">Each voxel contains a set of surface elements with processed topology data (aka surfels).</span></span> <span data-ttu-id="61079-193">Le surfels contenu dans la cellule voxel intersectée est comparé et la meilleure correspondance est utilisée pour rechercher les informations de topologie.</span><span class="sxs-lookup"><span data-stu-id="61079-193">The surfels contained within the intersected voxel cell are compared and the best match used to look up the topology information.</span></span> <span data-ttu-id="61079-194">Ces données de topologie contiennent l’étiquetage renvoyé sous la forme de l’énumération « SurfaceTypes », ainsi que la surface d’exposition de la surface intersectée.</span><span class="sxs-lookup"><span data-stu-id="61079-194">This topology data contains the labeling returned in the form of the “SurfaceTypes” enum, as well as the surface area of the intersected surface.</span></span>

<span data-ttu-id="61079-195">Dans l’exemple Unity, le curseur convertit chaque image de rayon.</span><span class="sxs-lookup"><span data-stu-id="61079-195">In the Unity sample, the cursor casts a ray each frame.</span></span> <span data-ttu-id="61079-196">Tout d’abord, contre les conflits avec Unity.</span><span class="sxs-lookup"><span data-stu-id="61079-196">First, against Unity’s colliders.</span></span> <span data-ttu-id="61079-197">Deuxièmement, par rapport à la représentation universelle du module de présentation.</span><span class="sxs-lookup"><span data-stu-id="61079-197">Second, against the understanding module’s world representation.</span></span> <span data-ttu-id="61079-198">Enfin, les éléments d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="61079-198">And finally, again UI elements.</span></span> <span data-ttu-id="61079-199">Dans cette application, l’interface utilisateur est prioritaire, puis le résultat de la compréhension et enfin, les conflits avec Unity.</span><span class="sxs-lookup"><span data-stu-id="61079-199">In this application, UI gets priority, next the understanding result, and lastly, Unity’s colliders.</span></span> <span data-ttu-id="61079-200">Le SurfaceType est signalé en tant que texte en regard du curseur.</span><span class="sxs-lookup"><span data-stu-id="61079-200">The SurfaceType is reported as text next to the cursor.</span></span>

<span data-ttu-id="61079-201">![type de surface est étiqueté en regard du curseur](images/su-raycastresults-300px.jpg)</span><span class="sxs-lookup"><span data-stu-id="61079-201">![Surface type is labeled next to the cursor](images/su-raycastresults-300px.jpg)</span></span><br>
<span data-ttu-id="61079-202">*Le type de surface est étiqueté en regard du curseur*</span><span class="sxs-lookup"><span data-stu-id="61079-202">*Surface type is labeled next to the cursor*</span></span>

### <a name="topology-queries"></a><span data-ttu-id="61079-203">Requêtes de topologie</span><span class="sxs-lookup"><span data-stu-id="61079-203">Topology Queries</span></span>

<span data-ttu-id="61079-204">Dans la DLL, le gestionnaire de topologie gère l’étiquetage de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="61079-204">Within the DLL, the topology manager handles labeling of the environment.</span></span> <span data-ttu-id="61079-205">Comme indiqué ci-dessus, la plupart des données sont stockées dans surfels, contenues dans un volume voxel.</span><span class="sxs-lookup"><span data-stu-id="61079-205">As mentioned above, much of the data is stored within surfels, contained within a voxel volume.</span></span> <span data-ttu-id="61079-206">En outre, la structure « PlaySpaceInfos » est utilisée pour stocker des informations sur le PlaySpace, y compris l’alignement universel (plus de détails à ce niveau ci-dessous), le plancher et la hauteur du plafond.</span><span class="sxs-lookup"><span data-stu-id="61079-206">In addition, the “PlaySpaceInfos” structure is used to store information about the playspace, including the world alignment (more details on this below), floor, and ceiling height.</span></span> <span data-ttu-id="61079-207">Les heuristiques sont utilisées pour déterminer l’étage, le plafond et les murs.</span><span class="sxs-lookup"><span data-stu-id="61079-207">Heuristics are used for determining floor, ceiling, and walls.</span></span> <span data-ttu-id="61079-208">Par exemple, la surface horizontale la plus grande et la plus basse avec une surface d’exposition supérieure à 1 m2 est considérée comme le plancher.</span><span class="sxs-lookup"><span data-stu-id="61079-208">For example, the largest and lowest horizontal surface with greater than 1 m2 surface area is considered the floor.</span></span> <span data-ttu-id="61079-209">Notez que le chemin d’accès de l’appareil photo pendant le processus d’analyse est également utilisé dans ce processus.</span><span class="sxs-lookup"><span data-stu-id="61079-209">Note that the camera path during the scanning process is also used in this process.</span></span>

<span data-ttu-id="61079-210">Un sous-ensemble des requêtes exposées par le gestionnaire de topologie est exposé via la dll.</span><span class="sxs-lookup"><span data-stu-id="61079-210">A subset of the queries exposed by the Topology manager are exposed out through the dll.</span></span> <span data-ttu-id="61079-211">Les requêtes de topologie exposées sont les suivantes.</span><span class="sxs-lookup"><span data-stu-id="61079-211">The exposed topology queries are as follows.</span></span>

```cpp
QueryTopology_FindPositionsOnWalls
QueryTopology_FindLargePositionsOnWalls
QueryTopology_FindLargestWall
QueryTopology_FindPositionsOnFloor
QueryTopology_FindLargestPositionsOnFloor
QueryTopology_FindPositionsSittable
```

<span data-ttu-id="61079-212">Chacune des requêtes a un ensemble de paramètres, spécifique au type de requête.</span><span class="sxs-lookup"><span data-stu-id="61079-212">Each of the queries has a set of parameters, specific to the query type.</span></span> <span data-ttu-id="61079-213">Dans l’exemple suivant, l’utilisateur spécifie la hauteur minimale & largeur du volume souhaité, la hauteur minimale de placement au-dessus du plancher et la quantité minimale d’autorisation devant le volume.</span><span class="sxs-lookup"><span data-stu-id="61079-213">In the following example, the user specifies the minimum height & width of the desired volume, minimum placement height above the floor, and the minimum amount of clearance in front of the volume.</span></span> <span data-ttu-id="61079-214">Toutes les mesures sont en mètres.</span><span class="sxs-lookup"><span data-stu-id="61079-214">All measurements are in meters.</span></span>

```cpp
EXTERN_C __declspec(dllexport) int QueryTopology_FindPositionsOnWalls(
    _In_ float minHeightOfWallSpace,
    _In_ float minWidthOfWallSpace,
    _In_ float minHeightAboveFloor,
    _In_ float minFacingClearance,
    _In_ int locationCount,
    _Inout_ Dll_Interface::TopologyResult* locationData)
```

<span data-ttu-id="61079-215">Chacune de ces requêtes utilise un tableau pré-alloué de structures « TopologyResult ».</span><span class="sxs-lookup"><span data-stu-id="61079-215">Each of these queries takes a pre-allocated array of “TopologyResult” structures.</span></span> <span data-ttu-id="61079-216">Le paramètre « locationCount » spécifie la longueur du tableau transmis.</span><span class="sxs-lookup"><span data-stu-id="61079-216">The “locationCount” parameter specifies the length of the passed in array.</span></span> <span data-ttu-id="61079-217">La valeur de retour indique le nombre d’emplacements retournés.</span><span class="sxs-lookup"><span data-stu-id="61079-217">The return value reports the number of returned locations.</span></span> <span data-ttu-id="61079-218">Ce nombre n’est jamais supérieur au paramètre « locationCount » passé.</span><span class="sxs-lookup"><span data-stu-id="61079-218">This number is never greater than the passed in “locationCount” parameter.</span></span>

<span data-ttu-id="61079-219">« TopologyResult » contient la position centrale du volume retourné, le sens de face (c’est-à-dire normal) et les dimensions de l’espace trouvé.</span><span class="sxs-lookup"><span data-stu-id="61079-219">The “TopologyResult” contains the center position of the returned volume, the facing direction (i.e. normal), and the dimensions of the found space.</span></span>

```cpp
struct TopologyResult 
{ 
    DirectX::XMFLOAT3 position; 
    DirectX::XMFLOAT3 normal; 
    float width; 
    float length;
};
```

<span data-ttu-id="61079-220">Notez que dans l’exemple Unity, chacune de ces requêtes est liée à un bouton dans le panneau de l’interface utilisateur virtuelle.</span><span class="sxs-lookup"><span data-stu-id="61079-220">Note that in the Unity sample, each of these queries is linked up to a button in the virtual UI panel.</span></span> <span data-ttu-id="61079-221">L’exemple code en dur les paramètres de chacune de ces requêtes à des valeurs raisonnables.</span><span class="sxs-lookup"><span data-stu-id="61079-221">The sample hard codes the parameters for each of these queries to reasonable values.</span></span> <span data-ttu-id="61079-222">Pour plus d’exemples, consultez SpaceVisualizer.cs dans l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="61079-222">See SpaceVisualizer.cs in the sample code for more examples.</span></span>

### <a name="shape-queries"></a><span data-ttu-id="61079-223">Requêtes de forme</span><span class="sxs-lookup"><span data-stu-id="61079-223">Shape Queries</span></span>

<span data-ttu-id="61079-224">À l’intérieur de la dll, l’analyseur de forme (« ShapeAnalyzer_W ») utilise l’analyseur de topologie pour faire correspondre les formes personnalisées définies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="61079-224">Inside of the dll, the shape analyzer (“ShapeAnalyzer_W”) uses the topology analyzer to match against custom shapes defined by the user.</span></span> <span data-ttu-id="61079-225">L’exemple Unity définit un ensemble de formes et expose les résultats par le biais du menu requête dans l’application, dans l’onglet forme. L’objectif est que l’utilisateur peut définir ses propres requêtes de forme d’objet et les utiliser, selon les besoins de leur application.</span><span class="sxs-lookup"><span data-stu-id="61079-225">The Unity sample defines a set of shapes and exposes the results out through the in-app query menu, within the shape tab. The intention is that the user can define their own object shape queries and make use of those, as needed by their application.</span></span>

<span data-ttu-id="61079-226">Notez que l’analyse des formes fonctionne uniquement sur des surfaces horizontales.</span><span class="sxs-lookup"><span data-stu-id="61079-226">Note that the shape analysis works on horizontal surfaces only.</span></span> <span data-ttu-id="61079-227">Un canapé, par exemple, est défini par la surface du siège plat et le haut à l’arrière de la canapé.</span><span class="sxs-lookup"><span data-stu-id="61079-227">A couch, for example, is defined by the flat seat surface and the flat top of the couch back.</span></span> <span data-ttu-id="61079-228">La requête Shape recherche deux surfaces d’une taille, d’une hauteur et d’une plage d’aspect spécifiques, les deux surfaces étant alignées et connectées.</span><span class="sxs-lookup"><span data-stu-id="61079-228">The shape query looks for two surfaces of a specific size, height, and aspect range, with the two surfaces aligned and connected.</span></span> <span data-ttu-id="61079-229">En utilisant la terminologie des API, le siège de la canapé et l’arrière-plan sont des composants de forme et les exigences d’alignement sont des contraintes de composant de forme.</span><span class="sxs-lookup"><span data-stu-id="61079-229">Using the APIs terminology, the couch seat and back top are shape components and the alignment requirements are shape component constraints.</span></span>

<span data-ttu-id="61079-230">Voici un exemple de requête défini dans l’exemple Unity (ShapeDefinition.cs) pour les objets « sittable ».</span><span class="sxs-lookup"><span data-stu-id="61079-230">An example query defined in the Unity sample (ShapeDefinition.cs), for “sittable” objects is as follows.</span></span>

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

<span data-ttu-id="61079-231">Chaque requête de forme est définie par un ensemble de composants de forme, chacun avec un ensemble de contraintes de composant et un ensemble de contraintes de forme qui répertorient les dépendances entre les composants.</span><span class="sxs-lookup"><span data-stu-id="61079-231">Each shape query is defined by a set of shape components, each with a set of component constraints and a set of shape constraints which listing dependencies between the components.</span></span> <span data-ttu-id="61079-232">Cet exemple inclut trois contraintes dans une définition de composant unique et aucune contrainte de forme entre les composants (étant donné qu’il n’y a qu’un seul composant).</span><span class="sxs-lookup"><span data-stu-id="61079-232">This example includes three constraints in a single component definition and no shape constraints between components (as there is only one component).</span></span>

<span data-ttu-id="61079-233">En revanche, la forme de canapé a deux composants de forme et quatre contraintes de forme.</span><span class="sxs-lookup"><span data-stu-id="61079-233">In contrast, the couch shape has two shape components and four shape constraints.</span></span> <span data-ttu-id="61079-234">Notez que les composants sont identifiés par leur index dans la liste des composants de l’utilisateur (0 et 1 dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="61079-234">Note that components are identified by their index in the user’s component list (0 and 1 in this example).</span></span>

```cs
shapeConstraints = new List<ShapeConstraint>()
{
    ShapeConstraint.Create_RectanglesSameLength(0, 1, 0.6f),
    ShapeConstraint.Create_RectanglesParallel(0, 1),
    ShapeConstraint.Create_RectanglesAligned(0, 1, 0.3f),
    ShapeConstraint.Create_AtBackOf(1, 0),
};
```

<span data-ttu-id="61079-235">Les fonctions wrapper sont fournies dans le module Unity pour faciliter la création de définitions de formes personnalisées.</span><span class="sxs-lookup"><span data-stu-id="61079-235">Wrapper functions are provided in the Unity module for easy creation of custom shape definitions.</span></span> <span data-ttu-id="61079-236">La liste complète des contraintes de composant et de forme se trouve dans « SpatialUnderstandingDll.cs » dans les structures « ShapeComponentConstraint » et « ShapeConstraint ».</span><span class="sxs-lookup"><span data-stu-id="61079-236">The full list of component and shape constraints can be found in “SpatialUnderstandingDll.cs” within the “ShapeComponentConstraint” and the “ShapeConstraint” structures.</span></span>

<span data-ttu-id="61079-237">![forme de rectangle se trouve sur cette surface](images/su-shapequery-300px.jpg)</span><span class="sxs-lookup"><span data-stu-id="61079-237">![Rectangle shape is found on this surface](images/su-shapequery-300px.jpg)</span></span><br>
<span data-ttu-id="61079-238">*Forme de rectangle trouvée sur cette surface*</span><span class="sxs-lookup"><span data-stu-id="61079-238">*Rectangle shape is found on this surface*</span></span>

### <a name="object-placement-solver"></a><span data-ttu-id="61079-239">Solveur de positionnement des objets</span><span class="sxs-lookup"><span data-stu-id="61079-239">Object Placement Solver</span></span>

<span data-ttu-id="61079-240">Le solveur de placement d’objet peut être utilisé pour identifier les emplacements idéaux dans la salle physique pour placer vos objets.</span><span class="sxs-lookup"><span data-stu-id="61079-240">The object placement solver can be used to identify ideal locations in the physical room to place your objects.</span></span> <span data-ttu-id="61079-241">Le solveur trouvera l’emplacement le mieux adapté en fonction des contraintes et règles d’objet.</span><span class="sxs-lookup"><span data-stu-id="61079-241">The solver will find the best fit location given the object rules and constraints.</span></span> <span data-ttu-id="61079-242">En outre, les requêtes d’objet sont conservées jusqu’à ce que l’objet soit supprimé avec les appels « Solver_RemoveObject » ou « Solver_RemoveAllObjects », ce qui permet le placement de plusieurs objets avec restriction.</span><span class="sxs-lookup"><span data-stu-id="61079-242">In addition, object queries persist until the object is removed with “Solver_RemoveObject” or “Solver_RemoveAllObjects” calls, allowing constrained multi-object placement.</span></span> <span data-ttu-id="61079-243">Les requêtes de placement d’objets se composent de trois parties : le type de placement avec des paramètres, une liste de règles et une liste de contraintes.</span><span class="sxs-lookup"><span data-stu-id="61079-243">Objects placement queries consist of three parts: placement type with parameters, a list of rules, and a list of constraints.</span></span> <span data-ttu-id="61079-244">Pour exécuter une requête, utilisez l’API suivante.</span><span class="sxs-lookup"><span data-stu-id="61079-244">To run a query, use the following API.</span></span>

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

<span data-ttu-id="61079-245">Cette fonction accepte un nom d’objet, une définition de placement et une liste de règles et de contraintes.</span><span class="sxs-lookup"><span data-stu-id="61079-245">This function takes an object name, placement definition, and a list of rules and constraints.</span></span> <span data-ttu-id="61079-246">Les C# wrappers fournissent des fonctions d’assistance de construction pour faciliter la création de règles et de contraintes.</span><span class="sxs-lookup"><span data-stu-id="61079-246">The C# wrappers provides construction helper functions to make rule and constraint construction easy.</span></span> <span data-ttu-id="61079-247">La définition de placement contient le type de requête, c’est-à-dire l’un des éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="61079-247">The placement definition contains the query type – that is, one of the following.</span></span>

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

<span data-ttu-id="61079-248">Chacun des types de placement a un ensemble de paramètres propre au type.</span><span class="sxs-lookup"><span data-stu-id="61079-248">Each of the placement types has a set of parameters unique to the type.</span></span> <span data-ttu-id="61079-249">La structure « ObjectPlacementDefinition » contient un ensemble de fonctions d’assistance statiques pour la création de ces définitions.</span><span class="sxs-lookup"><span data-stu-id="61079-249">The “ObjectPlacementDefinition” structure contains a set of static helper functions for creating these definitions.</span></span> <span data-ttu-id="61079-250">Par exemple, pour trouver un endroit où placer un objet sur l’étage, vous pouvez utiliser la fonction suivante.</span><span class="sxs-lookup"><span data-stu-id="61079-250">For example, to find a place to put an object on the floor, you can use the following function.</span></span> <span data-ttu-id="61079-251">public static ObjectPlacementDefinition Create_OnFloor (Vector3 halfDims) en plus du type de placement, vous pouvez fournir un ensemble de règles et de contraintes.</span><span class="sxs-lookup"><span data-stu-id="61079-251">public static ObjectPlacementDefinition Create_OnFloor(Vector3 halfDims) In addition to the placement type, you can provide a set of rules and constraints.</span></span> <span data-ttu-id="61079-252">Les règles ne peuvent pas être violées.</span><span class="sxs-lookup"><span data-stu-id="61079-252">Rules cannot be violated.</span></span> <span data-ttu-id="61079-253">Les emplacements d’emplacement possibles qui satisfont au type et aux règles sont ensuite optimisés par rapport au jeu de contraintes afin de sélectionner l’emplacement de placement optimal.</span><span class="sxs-lookup"><span data-stu-id="61079-253">Possible placement locations that satisfy the type and rules are then optimized against the set of constraints in order to select the optimal placement location.</span></span> <span data-ttu-id="61079-254">Chacune des règles et contraintes peut être créée par les fonctions de création statique fournies.</span><span class="sxs-lookup"><span data-stu-id="61079-254">Each of the rules and constraints can be created by the provided static creation functions.</span></span> <span data-ttu-id="61079-255">Vous trouverez ci-dessous un exemple de fonction de construction de règle et de contrainte.</span><span class="sxs-lookup"><span data-stu-id="61079-255">An example rule and constraint construction function is provided below.</span></span>

```cs
public static ObjectPlacementRule Create_AwayFromPosition(
    Vector3 position, float minDistance)
public static ObjectPlacementConstraint Create_NearPoint(
    Vector3 position, float minDistance = 0.0f, float maxDistance = 0.0f)
```

<span data-ttu-id="61079-256">La requête de placement d’objet ci-dessous recherche un endroit où placer un cube demi-mètre sur le bord d’une surface, à l’écart des autres objets placés précédemment et près du centre de la pièce.</span><span class="sxs-lookup"><span data-stu-id="61079-256">The below object placement query is looking for a place to put a half meter cube on the edge of a surface, away from other previously place objects and near the center of the room.</span></span>

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

<span data-ttu-id="61079-257">En cas de réussite, une structure « ObjectPlacementResult » contenant la position, les dimensions et l’orientation de placement est retournée.</span><span class="sxs-lookup"><span data-stu-id="61079-257">If successful, a “ObjectPlacementResult” structure containing the placement position, dimensions and orientation is returned.</span></span> <span data-ttu-id="61079-258">En outre, le placement est ajouté à la liste interne des objets placés de la dll.</span><span class="sxs-lookup"><span data-stu-id="61079-258">In addition, the placement is added to the dll’s internal list of placed objects.</span></span> <span data-ttu-id="61079-259">Les requêtes d’emplacement suivantes prennent en compte cet objet.</span><span class="sxs-lookup"><span data-stu-id="61079-259">Subsequent placement queries will take this object into account.</span></span> <span data-ttu-id="61079-260">Le fichier « LevelSolver.cs » dans l’exemple Unity contient plus d’exemples de requêtes.</span><span class="sxs-lookup"><span data-stu-id="61079-260">The “LevelSolver.cs” file in the Unity sample contains more example queries.</span></span>

<span data-ttu-id="61079-261">![résultats de l’emplacement des objets](images/su-objectplacement-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="61079-261">![Results of object placement](images/su-objectplacement-1000px.jpg)</span></span><br>
<span data-ttu-id="61079-262">*Figure 3 : zone bleue comment le résultat de trois emplacements sur les requêtes d’étage à l’extérieur des règles de position de l’appareil photo*</span><span class="sxs-lookup"><span data-stu-id="61079-262">*Figure 3: The blue boxes how the result from three place on floor queries with away from camera position rules*</span></span>

<span data-ttu-id="61079-263">Lors de la résolution de l’emplacement de positionnement de plusieurs objets requis pour un scénario de niveau ou d’application, commencez par résoudre les objets indispensables et volumineux afin d’optimiser la probabilité qu’un espace soit trouvé.</span><span class="sxs-lookup"><span data-stu-id="61079-263">When solving for placement location of multiple objects required for a level or application scenario, first solve indispensable and large objects in order to maximizing the probability that a space can be found.</span></span> <span data-ttu-id="61079-264">L’ordre de placement est important.</span><span class="sxs-lookup"><span data-stu-id="61079-264">Placement order is important.</span></span> <span data-ttu-id="61079-265">Si vous ne trouvez pas de placement d’objet, essayez des configurations moins restreintes.</span><span class="sxs-lookup"><span data-stu-id="61079-265">If object placements cannot be found, try less constrained configurations.</span></span> <span data-ttu-id="61079-266">Avoir un ensemble de configurations de secours est essentiel à la prise en charge des fonctionnalités dans de nombreuses configurations de salles.</span><span class="sxs-lookup"><span data-stu-id="61079-266">Having a set of fallback configurations is critical to supporting functionality across many room configurations.</span></span>

### <a name="room-scanning-process"></a><span data-ttu-id="61079-267">Processus d’analyse de la salle</span><span class="sxs-lookup"><span data-stu-id="61079-267">Room Scanning Process</span></span>

<span data-ttu-id="61079-268">Bien que la solution de mappage spatial fournie par le HoloLens soit conçue pour être suffisamment générique pour répondre aux besoins de la gamme complète des espaces à problème, le module de compréhension spatiale a été conçu pour prendre en charge les besoins de deux jeux spécifiques.</span><span class="sxs-lookup"><span data-stu-id="61079-268">While the spatial mapping solution provided by the HoloLens is designed to be generic enough to meet the needs of the entire gamut of problem spaces, the spatial understanding module was built to support the needs of two specific games.</span></span> <span data-ttu-id="61079-269">Sa solution est structurée autour d’un processus et d’un ensemble d’hypothèses spécifiques, résumés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="61079-269">Its solution is structured around a specific process and set of assumptions, summarized below.</span></span>

```
Fixed size playspace – The user specifies the maximum playspace size in the init call.

One-time scan process – 
    The process requires a discrete scanning phase where the user walks around,
    defining the playspace. 
    Query functions will not function until after the scan has been finalized.
```

<span data-ttu-id="61079-270">« Peinture » PlaySpace pilotée par l’utilisateur : au cours de la phase d’analyse, l’utilisateur se déplace et regarde le rythme des lectures, en peignant efficacement les zones qui doivent être incluses.</span><span class="sxs-lookup"><span data-stu-id="61079-270">User driven playspace “painting” – During the scanning phase, the user moves and looks around the plays pace, effectively painting the areas which should be included.</span></span> <span data-ttu-id="61079-271">La maille générée est importante pour fournir des commentaires de l’utilisateur au cours de cette phase.</span><span class="sxs-lookup"><span data-stu-id="61079-271">The generated mesh is important to provide user feedback during this phase.</span></span> <span data-ttu-id="61079-272">Installation à la page d’hébergement ou d’Office : les fonctions de requête sont conçues autour des surfaces plates et des parois à des angles droits.</span><span class="sxs-lookup"><span data-stu-id="61079-272">Indoors home or office setup – The query functions are designed around flat surfaces and walls at right angles.</span></span> <span data-ttu-id="61079-273">Il s’agit d’une limitation souple.</span><span class="sxs-lookup"><span data-stu-id="61079-273">This is a soft limitation.</span></span> <span data-ttu-id="61079-274">Toutefois, pendant la phase d’analyse, une analyse de l’axe principal est effectuée pour optimiser la facettisation du maillage le long de l’axe principal et de l’axe secondaire.</span><span class="sxs-lookup"><span data-stu-id="61079-274">However, during the scanning phase, a primary axis analysis is completed to optimize the mesh tessellation along major and minor axis.</span></span> <span data-ttu-id="61079-275">Le fichier SpatialUnderstanding.cs inclus gère le processus de phase d’analyse.</span><span class="sxs-lookup"><span data-stu-id="61079-275">The included SpatialUnderstanding.cs file manages the scanning phase process.</span></span> <span data-ttu-id="61079-276">Il appelle les fonctions suivantes.</span><span class="sxs-lookup"><span data-stu-id="61079-276">It calls the following functions.</span></span>

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

<span data-ttu-id="61079-277">Le workflow d’analyse, piloté par le comportement « SpatialUnderstanding », appelle InitScan, puis UpdateScan chaque frame.</span><span class="sxs-lookup"><span data-stu-id="61079-277">The scanning flow, driven by the “SpatialUnderstanding” behavior calls InitScan, then UpdateScan each frame.</span></span> <span data-ttu-id="61079-278">Lorsque la requête de statistiques signale une couverture raisonnable, l’utilisateur est autorisé à airtap d’appeler RequestFinish pour indiquer la fin de la phase d’analyse.</span><span class="sxs-lookup"><span data-stu-id="61079-278">When the statistics query reports reasonable coverage, the user is allowed to airtap to call RequestFinish to indicate the end of the scanning phase.</span></span> <span data-ttu-id="61079-279">UpdateScan continue à être appelé jusqu’à ce qu’il retourne la valeur indiquant que la dll a terminé le traitement.</span><span class="sxs-lookup"><span data-stu-id="61079-279">UpdateScan continues to be called until it’s return value indicates that the dll has completed processing.</span></span>

### <a name="understanding-mesh"></a><span data-ttu-id="61079-280">Fonctionnement de la maille</span><span class="sxs-lookup"><span data-stu-id="61079-280">Understanding Mesh</span></span>

<span data-ttu-id="61079-281">La dll de compréhension stocke en interne le PlaySpace sous la forme d’une grille de cubes voxel 8cm dimensionnés.</span><span class="sxs-lookup"><span data-stu-id="61079-281">The understanding dll internally stores the playspace as a grid of 8cm sized voxel cubes.</span></span> <span data-ttu-id="61079-282">Au cours de la phase initiale d’analyse, une analyse de composant principale est effectuée pour déterminer les axes de la salle.</span><span class="sxs-lookup"><span data-stu-id="61079-282">During the initial part of scanning, a primary component analysis is completed to determine the axes of the room.</span></span> <span data-ttu-id="61079-283">En interne, elle stocke son espace voxel aligné sur ces axes.</span><span class="sxs-lookup"><span data-stu-id="61079-283">Internally, it stores its voxel space aligned to these axes.</span></span> <span data-ttu-id="61079-284">Une maille est générée environ chaque seconde en extrayant le isosurface du volume voxel.</span><span class="sxs-lookup"><span data-stu-id="61079-284">A mesh is generated approximately every second by extracting the isosurface from the voxel volume.</span></span> 

<span data-ttu-id="61079-285">![maille générée produite à partir du volume voxel](images/su-custommesh.jpg)</span><span class="sxs-lookup"><span data-stu-id="61079-285">![Generated mesh produced from the voxel volume](images/su-custommesh.jpg)</span></span><br>
<span data-ttu-id="61079-286">*Maille générée produite à partir du volume voxel*</span><span class="sxs-lookup"><span data-stu-id="61079-286">*Generated mesh produced from the voxel volume*</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="61079-287">Dépannage</span><span class="sxs-lookup"><span data-stu-id="61079-287">Troubleshooting</span></span>
* <span data-ttu-id="61079-288">Vérifiez que vous avez défini la fonctionnalité [SpatialPerception](#setting-the-spatialperception-capability)</span><span class="sxs-lookup"><span data-stu-id="61079-288">Ensure you have set the [SpatialPerception](#setting-the-spatialperception-capability) capability</span></span>
* <span data-ttu-id="61079-289">Lorsque le suivi est perdu, l’événement OnSurfaceChanged suivant supprime tous les maillages.</span><span class="sxs-lookup"><span data-stu-id="61079-289">When tracking is lost, the next OnSurfaceChanged event will remove all meshes.</span></span>

## <a name="spatial-mapping-in-mixed-reality-toolkit"></a><span data-ttu-id="61079-290">Mappage spatial dans le Toolkit de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="61079-290">Spatial Mapping in Mixed Reality Toolkit</span></span>
<span data-ttu-id="61079-291">Pour plus d’informations sur l’utilisation du mappage spatial avec Mixed Reality Toolkit v2, consultez la <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/SpatialAwareness/SpatialAwarenessGettingStarted.html" target="_blank">section relative à la sensibilisation spatiale</a> des documents MRTK.</span><span class="sxs-lookup"><span data-stu-id="61079-291">For more information on using Spatial Mapping with Mixed Reality Toolkit v2, see the <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/SpatialAwareness/SpatialAwarenessGettingStarted.html" target="_blank">Spatial Awareness section</a> of the MRTK docs.</span></span>

## <a name="see-also"></a><span data-ttu-id="61079-292">Articles associés</span><span class="sxs-lookup"><span data-stu-id="61079-292">See also</span></span>
* [<span data-ttu-id="61079-293">MR spatial 230 : mappage spatial</span><span class="sxs-lookup"><span data-stu-id="61079-293">MR Spatial 230: Spatial mapping</span></span>](holograms-230.md)
* [<span data-ttu-id="61079-294">Systèmes de coordonnées</span><span class="sxs-lookup"><span data-stu-id="61079-294">Coordinate systems</span></span>](coordinate-systems.md)
* [<span data-ttu-id="61079-295">Systèmes de coordonnées dans Unity</span><span class="sxs-lookup"><span data-stu-id="61079-295">Coordinate systems in Unity</span></span>](coordinate-systems-in-unity.md)
* <span data-ttu-id="61079-296"><a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">MixedRealityToolkit</a></span><span class="sxs-lookup"><span data-stu-id="61079-296"><a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">MixedRealityToolkit</a></span></span>
* <span data-ttu-id="61079-297"><a href="https://docs.unity3d.com/ScriptReference/MeshFilter.html" target="_blank">UnityEngine. MeshFilter</a></span><span class="sxs-lookup"><span data-stu-id="61079-297"><a href="https://docs.unity3d.com/ScriptReference/MeshFilter.html" target="_blank">UnityEngine.MeshFilter</a></span></span>
* <span data-ttu-id="61079-298"><a href="https://docs.unity3d.com/ScriptReference/MeshCollider.html" target="_blank">UnityEngine. MeshCollider</a></span><span class="sxs-lookup"><span data-stu-id="61079-298"><a href="https://docs.unity3d.com/ScriptReference/MeshCollider.html" target="_blank">UnityEngine.MeshCollider</a></span></span>
* <span data-ttu-id="61079-299"><a href="https://docs.unity3d.com/ScriptReference/Bounds.html" target="_blank">Limites de UnityEngine.</a></span><span class="sxs-lookup"><span data-stu-id="61079-299"><a href="https://docs.unity3d.com/ScriptReference/Bounds.html" target="_blank">UnityEngine.Bounds</a></span></span>
