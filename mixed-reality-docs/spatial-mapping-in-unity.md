---
title: Mappage spatial dans Unity
description: Rendu et se heurtant à la géométrie réelle autour de vous dans Unity.
author: davidkline-ms
ms.author: davidkl
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, mappage spatial, convertisseur, collider, maillage, l’analyse, composant
ms.openlocfilehash: 8f7bad1651ab31b2e83ad9d9c8f465547fbbdc5a
ms.sourcegitcommit: 2f600e5ad00cd447b180b0f89192b4b9d86bbc7e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148651"
---
# <a name="spatial-mapping-in-unity"></a>Mappage spatial dans Unity

Cette rubrique explique comment utiliser [mappage spatial](spatial-mapping.md) dans votre projet Unity, la récupération des maillages de triangles qui représentent les surfaces dans le monde autour d’un appareil HoloLens, pour la sélection élective, occlusion, analyse de la salle et bien plus encore.

Unity prend également en charge pour le mappage spatial, qui est exposé aux développeurs de plusieurs manières :
1. Mappage des composants disponibles dans le MixedRealityToolkit spatial, qui fournissent un chemin d’accès rapide et pratique pour bien démarrer avec mappage spatial
2. Mappage spatial de bas niveau API, qui fournissent complète contrôler et activer la personnalisation spécifique des applications plus sophistiquée

Pour utiliser le mappage spatial dans votre application, la fonctionnalité spatialPerception doit être définie dans votre AppxManifest.

## <a name="setting-the-spatialperception-capability"></a>Définition de la fonctionnalité SpatialPerception

Dans l’ordre pour une application de consommer des données de mappage spatial, la fonctionnalité SpatialPerception doit être activée.

Comment activer la fonctionnalité SpatialPerception :
1. Dans l’éditeur Unity, ouvrez le **« Paramètres du lecteur »** volet (Modifier > Paramètres du projet > lecteur)
2. Cliquez sur le **« Windows Store »** onglet
3. Développez **« Paramètres de publication »** et vérifiez le **« SpatialPerception »** fonctionnalité dans le **« Fonctionnalités »** liste

Notez que si vous avez déjà exporté votre projet Unity à une solution Visual Studio, vous devrez soit exporter vers un nouveau dossier ou manuellement [définir cette fonctionnalité dans le fichier AppxManifest dans Visual Studio](spatial-mapping-in-directx.md#set-up-your-app-to-use-the-spatialperception-capability).

Mappage spatial requiert également un MaxVersionTested de 10.0.10586.0 au moins :
1. Dans Visual Studio, avec le bouton droit, cliquez sur **Package.appxmanifest** dans l’Explorateur de solutions, puis sélectionnez **afficher le Code**
2. Recherchez la ligne spécifiant **TargetDeviceFamily** et modifiez **MaxVersionTested = « 10.0.10240.0 »** à **MaxVersionTested = « 10.0.10586.0 »**
3. **Enregistrer** le Package.appxmanifest.

## <a name="getting-started-with-unitys-built-in-spatial-mapping-components"></a>Mise en route avec les composants de mappage spatial intégrés d’Unity

Unity propose 2 composants permettant d’ajouter facilement mappage spatial à votre application, **convertisseur de mappage Spatial** et **Collider de mappage Spatial**.

### <a name="spatial-mapping-renderer"></a>Convertisseur de mappage spatial

Le convertisseur de mappage Spatial permet la visualisation de la maille de mappage spatial.

![Convertisseur de mappage spatial dans Unity](images/spatialmappingrenderer.png)

### <a name="spatial-mapping-collider"></a>Mappage spatial Collider

Permet du Collider mappage Spatial pour le contenu HOLOGRAPHIQUE (ou caractère) interaction, telles que physique, avec le maillage de mappage spatial.

![Collider mappage spatial dans Unity](images/spatialmappingcollider.png)

### <a name="using-the-built-in-spatial-mapping-components"></a>L’utilisation des composants intégrés mappage spatial

Si vous souhaitez les visualiser et interagir avec des surfaces physiques, vous pouvez ajouter les deux composants à votre application.

Pour utiliser ces deux composants dans votre application Unity :
1. Sélectionnez un GameObject au centre de la zone dans laquelle vous souhaitez détecter les mailles de surface spatiales.
2. Dans la fenêtre d’inspecteur, **ajouter un composant** > **XR** > **Collider de mappage Spatial** ou **Spatial Convertisseur de mappage**.

Vous trouverez plus d’informations sur l’utilisation de ces composants à la <a href="https://docs.unity3d.com/Manual/SpatialMappingComponents.html" target="_blank">site de documentation Unity</a>.

### <a name="going-beyond-the-built-in-spatial-mapping-components"></a>Au-delà des composants intégrés mappage spatial

Ces composants rendent glisser-déplacer faciles pour bien démarrer avec le mappage Spatial.  Lorsque vous souhaitez aller plus loin, il existe deux chemins d’accès principales pour Explorer :
* Pour faire votre propre traitement de maillage de niveau inférieur, consultez la section ci-dessous sur le script mappage Spatial API de bas niveau.
* Pour effectuer des analyses de maillage de niveau supérieur, consultez la section ci-dessous sur la bibliothèque SpatialUnderstanding dans <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialUnderstanding" target="_blank">MixedRealityToolkit</a>.

## <a name="using-the-low-level-unity-spatial-mapping-api"></a>À l’aide de l’API de mappage Spatial Unity bas niveau

Si vous avez besoin de plus de contrôle que vous obtenez à partir des composants de convertisseur de mappage spatiales et spatiales Collider de mappage, vous pouvez utiliser le script de bas niveau mappage Spatial API.

**Namespace :** *UnityEngine.XR.WSA*<br>
**Types**: *SurfaceObserver*, *SurfaceChange*, *SurfaceData*, *SurfaceId*

Voici un plan du flux suggéré pour une application qui utilise l’API de mappage spatial.

### <a name="set-up-the-surfaceobservers"></a>Configurer le SurfaceObserver(s)

Instanciez un objet SurfaceObserver pour chaque région définie par l’application de l’espace dont vous avez besoin des données de mappage spatial pour.

```cs
SurfaceObserver surfaceObserver;

 void Start () {
     surfaceObserver = new SurfaceObserver();
 }
```

Spécifier la région d’espace que chaque objet SurfaceObserver fournira les données pour en appelant SetVolumeAsSphere, SetVolumeAsAxisAlignedBox, SetVolumeAsOrientedBox ou SetVolumeAsFrustum. Vous pouvez redéfinir la région d’espace à l’avenir en appelant simplement une de ces méthodes à nouveau.

```cs
void Start () {
    ...
     surfaceObserver.SetVolumeAsAxisAlignedBox(Vector3.zero, new Vector3(3, 3, 3));
}
```

Lorsque vous appelez SurfaceObserver.Update(), vous devez fournir un gestionnaire pour chaque surface spatiale dans la région de la SurfaceObserver d’espace au système de mappage spatial a de nouvelles informations pour. Le gestionnaire reçoit, pour une surface spatiale :

```cs
private void OnSurfaceChanged(SurfaceId surfaceId, SurfaceChange changeType, Bounds bounds, System.DateTime updateTime)
 {
    //see Handling Surface Changes
 }
```

### <a name="handling-surface-changes"></a>Gestion des modifications de l’aire de conception

Il existe plusieurs cas principales à gérer. Ajouter & code de mise à jour qui peut utiliser le même chemin d’accès et suppression.
* Dans les cas Added & mis à jour dans l’exemple, nous ajouter ou à obtenir le GameObject représentant ce maillage à partir du dictionnaire, créez un struct SurfaceData avec les composants nécessaires, puis appeler RequestMeshDataAsync pour remplir le GameObject avec les données de maillage et position dans la scène.
* Dans le cas de suppression, nous supprimer le GameObject représentant ce maillage à partir du dictionnaire et détruire.

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

### <a name="handling-data-ready"></a>Gestion des données prêtes

Le Gestionnaire de OnDataReady reçoit un objet SurfaceData. Le WorldAnchor, MeshFilter et (éventuellement les objets MeshCollider qu’il contient) reflètent l’état de la surface spatiale associé. Si vous le souhaitez effectuer une analyse et/ou [traitement](spatial-mapping.md#mesh-processing) des données par l’accès au membre de maillage de l’objet MeshFilter maille. Restituer la surface spatiale auprès de la maille la plus récente et (éventuellement) de l’utiliser pour les collisions de physique et raycasts. Il est important de confirmer que le contenu de la SurfaceData n’est pas null.

### <a name="start-processing-on-updates"></a>Commencer le traitement des mises à jour

SurfaceObserver.Update() doit être appelée sur un délai, pas chaque trame.

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

## <a name="higher-level-mesh-analysis-spatialunderstanding"></a>Analyse de maillage de niveau supérieur : SpatialUnderstanding

Le <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">MixedRealityToolkit</a> est une collection de code d’utilitaire utile pour le développement holographique basé sur les API Unity HOLOGRAPHIQUE.

### <a name="spatial-understanding"></a>Présentation spatiale

Lorsque vous placez des hologrammes dans le monde physique, il est souvent souhaitable d’aller au-delà du mappage spatial de maillage et plans de surface. Lors de la sélection élective est effectuée de façon procédurale, un niveau plus élevé de compréhension de l’environnement est souhaitable. Vous devez prendre des décisions sur les nouveautés, floor, ceiling et murs. En outre, la capacité d’optimiser par rapport à un ensemble de contraintes de placement à la détermination des emplacements physiques plus souhaitables pour les objets HOLOGRAPHIQUE.

Pendant le développement de Young pétarade et de Fragments, Asobo Studios confrontés head de ce problème sur, le développement d’un solveur salle à cet effet. Chacun de ces jeux avait jeu besoins spécifiques, mais qu’ils partageaient core spatial fonctionnement de la technologie. HoloToolkit.SpatialUnderstanding bibliothèque encapsule cette technologie, ce qui que vous permettent de rechercher rapidement les espaces vides sur les murs, les objets sur place au plafond, identifiez placés par caractère asseoir et une myriade d’autres requêtes spatiales compréhension.

Tout le code source est inclus, ce qui vous permet de le personnaliser selon vos besoins et partager vos améliorations avec la Communauté. Le code pour le C++ Solveur a été encapsulé dans une dll UWP et exposé à Unity avec une baisse de préfabriqué contenu dans le MixedRealityToolkit.

### <a name="understanding-modules"></a>Modules de présentation

Il existe trois interfaces principales exposées par le module : topologie pour surface simple et les requêtes spatiales, la forme pour la détection de l’objet et le solveur de sélection élective d’objet pour la sélection élective de contrainte en fonction de jeux d’objets. Chacune d'entre elles est décrite ci-dessous. En plus des trois interfaces de module principal, une interface de casting ray peut être utilisée pour récupérer des types de surface avec balises et une maille playspace étanches personnalisé peut être copiée.

### <a name="ray-casting"></a>Ray cast

Une fois que la pièce a été analysée et finalisée, étiquettes sont générés de manière interne pour les surfaces comme floor, ceiling, les murs. Le « PlayspaceRaycast » prend un rayon de fonction et retourne si le rayon est en conflit avec une surface connue et le cas échéant, des informations sur cette surface sous la forme d’un « RaycastResult ».

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

En interne, le raycast est calculée par rapport à la représentation sous forme de voxel calculée 8cm au cube de la playspace. Chaque voxel contient un ensemble d’éléments de surface d’exposition des données de topologie traité (également appelé surfels). Les surfels contenues dans la cellule voxel intersectées sont comparées et la meilleure correspondance est utilisée pour rechercher les informations de topologie. Les données de cette topologie contient l’étiquetage retournées dans le formulaire de l’enum « SurfaceTypes », ainsi que la surface d’exposition de la surface d’intersection.

Dans l’exemple Unity, le curseur convertit un rayon chaque frame. Tout d’abord, contre colliders de d’Unity. En second lieu, par rapport à la représentation sous forme de monde du module de présentation. Et enfin, à nouveau éléments d’interface utilisateur. Dans cette application, l’interface utilisateur obtient ensuite la priorité, le résultat de la présentation et enfin, les colliders d’Unity. Le SurfaceType est signalée en tant que texte en regard du curseur.

![Type de l’aire de conception est étiqueté situé à proximité du curseur](images/su-raycastresults-300px.jpg)<br>
*Type de l’aire de conception est étiqueté situé à proximité du curseur*

### <a name="topology-queries"></a>Requêtes de topologie

Dans la DLL, le Gestionnaire de topologie gère l’étiquetage de l’environnement. Comme mentionné ci-dessus, les données sont stockées dans surfels, contenus dans un volume voxel. En outre, la structure « PlaySpaceInfos » est utilisée pour stocker des informations sur le playspace, y compris l’alignement du monde (plus de détails ci-dessous), floor et au plafond. Heuristique utilisée pour déterminer les murs floor et ceiling. Par exemple, la surface plus grande et plus basses horizontale avec plus de 1 la surface d’exposition m2 est considéré comme le plancher. Notez que le chemin d’accès de l’appareil photo pendant le processus d’analyse est également utilisé dans ce processus.

Un sous-ensemble de requêtes exposées par le Gestionnaire de la topologie sont exposés via la dll. Les requêtes de topologie exposés sont comme suit.

```cpp
QueryTopology_FindPositionsOnWalls
QueryTopology_FindLargePositionsOnWalls
QueryTopology_FindLargestWall
QueryTopology_FindPositionsOnFloor
QueryTopology_FindLargestPositionsOnFloor
QueryTopology_FindPositionsSittable
```

Chacune des requêtes a un ensemble de paramètres, spécifiques au type de requête. Dans l’exemple suivant, l’utilisateur spécifie la hauteur minimale et la largeur du volume de votre choix, à la hauteur minimale de sélection élective au-dessus de la valeur plancher, la quantité minimale de dégagement devant le volume. Toutes les mesures sont en mètres.

```cpp
EXTERN_C __declspec(dllexport) int QueryTopology_FindPositionsOnWalls(
    _In_ float minHeightOfWallSpace,
    _In_ float minWidthOfWallSpace,
    _In_ float minHeightAboveFloor,
    _In_ float minFacingClearance,
    _In_ int locationCount,
    _Inout_ Dll_Interface::TopologyResult* locationData)
```

Chacune de ces requêtes prend un tableau alloué au préalable de structures de « TopologyResult ». Le paramètre « locationCount » spécifie la longueur du tableau transmis. La valeur de retour indique le nombre d’emplacements retournés. Ce nombre n’est jamais supérieur à passé dans le paramètre de « locationCount ».

Le « TopologyResult » contient la position centrale du volume retourné, la direction accessibles (par exemple, normale) et les dimensions de l’espace est trouvé.

```cpp
struct TopologyResult 
{ 
    DirectX::XMFLOAT3 position; 
    DirectX::XMFLOAT3 normal; 
    float width; 
    float length;
};
```

Notez que dans l’exemple Unity, chacune de ces requêtes est lié à un bouton dans le panneau de l’interface utilisateur virtuel. L’exemple dur codes les paramètres pour chacune de ces requêtes à des valeurs raisonnables. Dans l’exemple de code pour plus d’exemples, consultez SpaceVisualizer.cs.

### <a name="shape-queries"></a>Requêtes de forme

À l’intérieur de la dll, l’Analyseur de forme (« ShapeAnalyzer_W ») utilise l’Analyseur de topologie à mettre en correspondance des formes personnalisées définies par l’utilisateur. L’exemple Unity définit un ensemble de formes et expose les résultats vers l’extérieur via le menu de la requête de dans l’application, dans l’onglet de la forme. L’intention est que l’utilisateur peut définir leurs propres requêtes de forme d’objet et rendre utiliser d'entre eux, selon les besoins de leur application.

Notez que l’analyse de la forme fonctionne sur les surfaces horizontales uniquement. Un canapé, par exemple, est défini par l’assise plat et haut plat de retour le canapé. La requête shape recherche deux surfaces d’une plage de taille, la hauteur et aspect spécifique, avec les deux surfaces alignée et connecté. À l’aide de la terminologie de l’API, le siège de canapé et le haut précédent sont des composants de la forme et les exigences d’alignement sont des contraintes de composant de forme.

Voici un exemple de requête définie dans l’exemple de Unity (ShapeDefinition.cs), pour les objets « sittable ».

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

Chaque requête shape est défini par un ensemble de composants de forme, chacun avec un ensemble de contraintes de composant et un ensemble de contraintes de forme qui établissement des dépendances entre les composants. Cet exemple inclut trois contraintes dans une définition de composant unique et aucune contrainte de forme entre les composants (comme il n’existe qu’un seul composant).

En revanche, la forme de canapé a deux composants de forme et quatre contraintes de forme. Notez que les composants sont identifiés par leur index dans la liste des composants de l’utilisateur (0 et 1 dans cet exemple).

```cs
shapeConstraints = new List<ShapeConstraint>()
{
    ShapeConstraint.Create_RectanglesSameLength(0, 1, 0.6f),
    ShapeConstraint.Create_RectanglesParallel(0, 1),
    ShapeConstraint.Create_RectanglesAligned(0, 1, 0.3f),
    ShapeConstraint.Create_AtBackOf(1, 0),
};
```

Fonctions de wrapper sont fournies dans le module Unity pour simplifier la création de définitions de formes personnalisée. Vous trouverez la liste complète des contraintes de composant et de forme dans « SpatialUnderstandingDll.cs » dans le « ShapeComponentConstraint » et les structures de « ShapeConstraint ».

![Forme de rectangle se trouve sur cette surface](images/su-shapequery-300px.jpg)<br>
*Forme de rectangle se trouve sur cette surface*

### <a name="object-placement-solver"></a>Solveur de sélection élective d’objet

Le solveur de sélection élective d’objet peut être utilisé pour identifier les emplacements idéale dans la salle physique pour placer vos objets. Le Solveur trouve le conviennent le mieux à l’emplacement donné les règles de l’objet et les contraintes. En outre, les requêtes d’objet persistent jusqu'à ce que l’objet est supprimé avec « Solver_RemoveObject » ou d’appels « Solver_RemoveAllObjects », ce qui contraint placement d’objets multiples. Requêtes de sélection élective d’objets se composent de trois parties : le type d’emplacement avec les paramètres, une liste de règles et une liste de contraintes. Pour exécuter une requête, utilisez l’API suivante.

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

Cette fonction accepte un nom d’objet, définition de placement et une liste des règles et des contraintes. Le C# wrappers fournit des fonctions d’assistance pour faciliter la construction de règle et de contrainte de construction. La définition de placement contient le type de requête : autrement dit, une des opérations suivantes.

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

Chacun des types de sélection élective a un ensemble de paramètres uniques pour le type. La structure « ObjectPlacementDefinition » contient un ensemble de fonctions d’assistance statiques pour la création de ces définitions. Par exemple, pour rechercher un emplacement pour placer un objet sur le sol, vous pouvez utiliser la fonction suivante. publique statique ObjectPlacementDefinition Create_OnFloor(Vector3 halfDims) en plus du type de placement, vous pouvez fournir un ensemble de règles et des contraintes. Des règles ne peut pas être violées. Emplacements de positionnement possibles qui satisfont les type et les règles sont ensuite optimisés par rapport au jeu de contraintes afin de sélectionner l’emplacement de placement optimal. Chacune des règles et des contraintes peut être créé par les fonctions de création statique fourni. Vous trouverez ci-dessous un exemple de fonction construction règle et de contrainte.

```cs
public static ObjectPlacementRule Create_AwayFromPosition(
    Vector3 position, float minDistance)
public static ObjectPlacementConstraint Create_NearPoint(
    Vector3 position, float minDistance = 0.0f, float maxDistance = 0.0f)
```

La recherche se trouve sous objet requête de sélection élective pour un emplacement pour placer un cube de moitié compteur sur le bord d’une surface, autre précédemment placer des objets et près du centre de la salle.

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

En cas de réussite, une structure « ObjectPlacementResult » contenant la position de la sélection élective, dimensions et l’orientation est retournée. En outre, le positionnement est ajouté à la liste interne de la dll d’objets placés. Requêtes de sélection élective ultérieures prennent cet objet en compte. Le fichier « LevelSolver.cs » dans l’exemple Unity contient plusieurs exemples de requêtes.

![Résultats du placement des objets](images/su-objectplacement-1000px.jpg)<br>
*Figure 3 : Le bleu boîtes de fonctionnement des requêtes avec le résultat à partir de trois endroits sur sol en dehors des règles de position de la caméra*

Lors de la résolution pour l’emplacement du positionnement de plusieurs objets requis pour un scénario de niveau ou de l’application, tout d’abord résoudre indispensables et de grande taille des objets dans l’ordre à l’optimisation de la probabilité qu’un espace peut être trouvé. Ordre de sélection élective est important. Si le placement de l’objet est introuvable, essayez de configurations moins limitées. Il est essentiel de prenant en charge des fonctionnalités sur de nombreuses configurations de salle de disposer d’un ensemble de configurations de secours.

### <a name="room-scanning-process"></a>Processus d’analyse salle

Alors que la solution de mappage spatial fournie par le HoloLens est conçue pour être suffisamment générique pour répondre aux besoins de toute la gamme des espaces de problème, le module de présentation spatial a été créé pour prendre en charge les besoins de deux jeux spécifiques. Sa solution est structurée autour d’un processus spécifique et des hypothèses, résumées ci-dessous.

```
Fixed size playspace – The user specifies the maximum playspace size in the init call.

One-time scan process – 
    The process requires a discrete scanning phase where the user walks around,
    defining the playspace. 
    Query functions will not function until after the scan has been finalized.
```

Par playspace « peinture » – pendant la phase d’analyse, l’utilisateur, l’utilisateur déplace et recherche autour de la lecture du son propre rythme, peinture efficacement les zones qui doivent être incluses. Le maillage généré est important de fournir des commentaires des utilisateurs durant cette phase. À l’intérieur d’accueil ou d’installation office : la requête de fonctions sont conçues autour des surfaces plats et des murs à angle droit. Il s’agit d’une limitation logicielle. Toutefois, pendant la phase d’analyse, une analyse de l’axe principal est prévue pour optimiser le pavage de maille le long de l’axe principal et secondaire. Le fichier SpatialUnderstanding.cs inclus gère le processus phase d’analyse. Il appelle les fonctions suivantes.

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

Le flux analyse, piloté par le comportement de « SpatialUnderstanding » appelle InitScan, puis UpdateScan chaque frame. Lorsque la requête de statistiques signale la couverture du raisonnable, l’utilisateur est autorisé à airtap pour appeler RequestFinish pour indiquer la fin de la phase d’analyse. UpdateScan continue à être appelée jusqu'à ce qu’il s’agit de retour la valeur indique que la dll a terminé le traitement.

### <a name="understanding-mesh"></a>Maillage de présentation

La dll de présentation stocke en interne la playspace sous forme de grille des cubes de voxel 8cm en taille réelle. Au cours de la partie initiale d’analyse, une analyse du composant principal est terminée pour déterminer les axes de la salle. En interne, elle stocke son espace voxel alignée sur ces axes. Une maille est générée environ toutes les secondes en extrayant l’isosurface le volume voxel. 

![Panneau généré produites à partir du volume voxel](images/su-custommesh.jpg)<br>
*Panneau généré produites à partir du volume voxel*

## <a name="troubleshooting"></a>Résolution des problèmes
* Assurez-vous que vous avez défini le [SpatialPerception](#setting-the-spatialperception-capability) fonctionnalité
* En cas de perte de suivi, l’événement OnSurfaceChanged suivant supprime toutes les mailles.

## <a name="spatial-mapping-in-mixed-reality-toolkit"></a>Mappage spatial dans le Kit de ressources de réalité mixte
Pour plus d’informations sur l’utilisation de mappage Spatial avec v2 Toolkit de réalité mixte, consultez le <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/SpatialAwareness/SpatialAwarenessGettingStarted.html" target="_blank">section de la reconnaissance spatiale</a> des documents MRTK.

## <a name="see-also"></a>Voir aussi
* [Réalité mixte - Fonctionnalités spatiales - Cours 230 : Mappage spatial](holograms-230.md)
* [Systèmes de coordonnées](coordinate-systems.md)
* [Systèmes de coordonnées dans Unity](coordinate-systems-in-unity.md)
* <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">MixedRealityToolkit</a>
* <a href="http://docs.unity3d.com/ScriptReference/MeshFilter.html" target="_blank">UnityEngine.MeshFilter</a>
* <a href="http://docs.unity3d.com/ScriptReference/MeshCollider.html" target="_blank">UnityEngine.MeshCollider</a>
* <a href="http://docs.unity3d.com/ScriptReference/Bounds.html" target="_blank">UnityEngine.Bounds</a>
