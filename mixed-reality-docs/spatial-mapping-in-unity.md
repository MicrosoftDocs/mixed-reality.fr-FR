---
title: Mappage spatial dans Unity
description: Rendu et collision avec la géométrie réelle autour de vous dans Unity.
author: davidkline-ms
ms.author: davidkl
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, mappage spatial, convertisseur, conflit, maillage, numérisation, composant
ms.openlocfilehash: 8f7bad1651ab31b2e83ad9d9c8f465547fbbdc5a
ms.sourcegitcommit: 2f600e5ad00cd447b180b0f89192b4b9d86bbc7e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148651"
---
# <a name="spatial-mapping-in-unity"></a>Mappage spatial dans Unity

Cette rubrique explique comment utiliser le [mappage spatial](spatial-mapping.md) dans votre projet Unity, en récupérant les maillages de triangles qui représentent les surfaces dans le monde autour d’un appareil HoloLens, pour le placement, l’occlusion, l’analyse de la salle, et bien plus encore.

Unity comprend la prise en charge complète du mappage spatial, qui est exposé aux développeurs des manières suivantes:
1. Composants de mappage spatial disponibles dans MixedRealityToolkit, qui fournissent un chemin d’accès pratique et rapide pour la prise en main du mappage spatial
2. API de mappage spatial de niveau inférieur, qui fournissent un contrôle total et permettent une personnalisation plus sophistiquée des applications

Pour utiliser le mappage spatial dans votre application, vous devez définir la capacité spatialPerception dans votre AppxManifest.

## <a name="setting-the-spatialperception-capability"></a>Définition de la fonctionnalité SpatialPerception

Pour qu’une application consomme des données de mappage spatiales, la capacité SpatialPerception doit être activée.

Comment activer la fonctionnalité SpatialPerception:
1. Dans l’éditeur Unity, ouvrez le volet **«paramètres du lecteur»** (modifier > paramètres du projet > Player)
2. Cliquer sur l’onglet **«Windows Store»**
3. Développez **«paramètres de publication»** et cochez la fonctionnalité **«SpatialPerception»** dans la liste **«fonctionnalités»** .

Notez que si vous avez déjà exporté votre projet Unity vers une solution Visual Studio, vous devez soit exporter vers un nouveau dossier, soit [définir manuellement cette fonctionnalité dans AppxManifest dans Visual Studio](spatial-mapping-in-directx.md#set-up-your-app-to-use-the-spatialperception-capability).

Le mappage spatial nécessite également un MaxVersionTested d’au moins 10.0.10586.0:
1. Dans Visual Studio, cliquez avec le bouton droit sur **Package. appxmanifest** dans le Explorateur de solutions puis sélectionnez **afficher le code** .
2. Recherchez la ligne qui spécifie **TargetDeviceFamily** et remplacez **MaxVersionTested = "10.0.10240.0"** par **MaxVersionTested = "10.0.10586.0"**
3. **Enregistrez** le package. appxmanifest.

## <a name="getting-started-with-unitys-built-in-spatial-mapping-components"></a>Prise en main des composants de mappage spatial intégrés à Unity

Unity offre 2 composants pour ajouter facilement le mappage spatial à votre application, le **convertisseur de mappage spatial** et le **conflit de mappage spatial**.

### <a name="spatial-mapping-renderer"></a>Convertisseur de mappage spatial

Le convertisseur de mappage spatial permet la visualisation du maillage de mappage spatial.

![Convertisseur de mappage spatial dans Unity](images/spatialmappingrenderer.png)

### <a name="spatial-mapping-collider"></a>Conflit de mappage spatial

Le conflit de mappage spatial permet l’interaction entre le contenu holographique (ou le caractère), tel que la physique, avec le maillage de mappage spatial.

![Conflit de mappage spatial dans Unity](images/spatialmappingcollider.png)

### <a name="using-the-built-in-spatial-mapping-components"></a>Utilisation des composants de mappage spatial intégrés

Vous pouvez ajouter les deux composants à votre application si vous souhaitez visualiser et interagir avec les surfaces physiques.

Pour utiliser ces deux composants dans votre application Unity:
1. Sélectionnez un GameObject au centre de la zone dans laquelle vous souhaitez détecter les maillages de surface spatiale.
2. Dans la fenêtre de l’inspecteur, **Ajoutez le composant** >  >  XR**mappage spatial de conflit**ou le convertisseur de **mappage spatial**.

Vous trouverez plus d’informations sur l’utilisation de ces composants sur le <a href="https://docs.unity3d.com/Manual/SpatialMappingComponents.html" target="_blank">site de documentation Unity</a>.

### <a name="going-beyond-the-built-in-spatial-mapping-components"></a>Aller au-delà des composants de mappage spatial intégrés

Ces composants facilitent le glisser-déplacer pour la prise en main du mappage spatial.  Lorsque vous souhaitez aller plus loin, il existe deux chemins principaux à explorer:
* Pour effectuer votre propre traitement de maillage de niveau inférieur, consultez la section ci-dessous sur l’API de script de mappage spatial de bas niveau.
* Pour effectuer une analyse de maillage de niveau supérieur, consultez la section ci-dessous sur la bibliothèque SpatialUnderstanding dans <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialUnderstanding" target="_blank">MixedRealityToolkit</a>.

## <a name="using-the-low-level-unity-spatial-mapping-api"></a>Utilisation de l’API de mappage spatial de bas niveau

Si vous avez besoin d’un contrôle plus élevé que celui obtenu à partir du convertisseur de mappage spatial et des composants de conflit de mappage spatial, vous pouvez utiliser les API de script de mappage spatial de bas niveau.

**Espace de noms :** *UnityEngine. XR. WSA*<br>
**Types**: *SurfaceObserver*, *SurfaceChange*, *SurfaceData*, *SurfaceId*

Voici un aperçu du déroulement suggéré pour une application qui utilise les API de mappage spatial.

### <a name="set-up-the-surfaceobservers"></a>Configurer le (s) SurfaceObserver (s)

Instanciez un objet SurfaceObserver pour chaque région d’espace définie par l’application dont vous avez besoin pour les données de mappage spatiale.

```cs
SurfaceObserver surfaceObserver;

 void Start () {
     surfaceObserver = new SurfaceObserver();
 }
```

Spécifiez la région d’espace pour laquelle chaque objet SurfaceObserver fournira des données en appelant SetVolumeAsSphere, SetVolumeAsAxisAlignedBox, SetVolumeAsOrientedBox ou SetVolumeAsFrustum. Vous pouvez redéfinir la région de l’espace à l’avenir en appelant une nouvelle fois l’une de ces méthodes.

```cs
void Start () {
    ...
     surfaceObserver.SetVolumeAsAxisAlignedBox(Vector3.zero, new Vector3(3, 3, 3));
}
```

Quand vous appelez SurfaceObserver. Update (), vous devez fournir un gestionnaire pour chaque surface spatiale de la région du SurfaceObserver d’espace pour lequel le système de mappage spatial a de nouvelles informations. Le gestionnaire reçoit, pour une surface spatiale:

```cs
private void OnSurfaceChanged(SurfaceId surfaceId, SurfaceChange changeType, Bounds bounds, System.DateTime updateTime)
 {
    //see Handling Surface Changes
 }
```

### <a name="handling-surface-changes"></a>Gestion des modifications de surface

Il existe plusieurs cas principaux à gérer. Ajout de & mis à jour qui peut utiliser le même chemin de code et supprimé.
* Dans la & ajoutée cas mis à jour dans l’exemple, nous ajoutons ou obtenons le GameObject représentant ce maillage du dictionnaire, nous créons un struct SurfaceData avec les composants nécessaires, puis appelons RequestMeshDataAsync pour remplir le GameObject avec les données de maillage et position dans la scène.
* Dans le cas supprimé, nous supprimons le GameObject représentant ce maillage du dictionnaire et le détruisons.

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

Le gestionnaire OnDataReady reçoit un objet SurfaceData. Les objets WorldAnchor, MeshFilter et (facultatif) MeshCollider qu’il contient reflètent l’état le plus récent de la surface spatiale associée. Effectuez éventuellement une analyse et/ou un [traitement](spatial-mapping.md#mesh-processing) des données de maillage en accédant au membre de maillage de l’objet MeshFilter. Affichez la surface spatiale avec la dernière maille et (éventuellement) utilisez-la pour les collisions physiques et les raycasts. Il est important de vérifier que le contenu du SurfaceData n’est pas null.

### <a name="start-processing-on-updates"></a>Démarrer le traitement des mises à jour

SurfaceObserver. Update () doit être appelé sur un délai, et non sur tous les frames.

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

## <a name="higher-level-mesh-analysis-spatialunderstanding"></a>Analyse de maillage de niveau supérieur: SpatialUnderstanding

Le <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">MixedRealityToolkit</a> est une collection de code d’utilitaire utile pour le développement holographique reposant sur les API d’Unity holographique.

### <a name="spatial-understanding"></a>Compréhension spatiale

Quand vous placez des hologrammes dans le monde physique, il est souvent préférable d’aller au-delà des plans de maillage et de surface du mappage spatial. Une fois le placement effectué, il est souhaitable d’avoir un niveau de compréhension environnemental plus élevé. Il est généralement nécessaire de prendre des décisions sur le plancher, le plafond et les murs. En outre, il est possible d’optimiser par rapport à un ensemble de contraintes de placement pour déterminer les emplacements physiques les plus intéressants pour les objets holographiques.

Pendant le développement de jeunes Conkers et fragments, Asobo Studios a rencontré ce problème en développant un solveur de salle à cet effet. Chacun de ces jeux avait des besoins spécifiques aux jeux, mais ils partageaient la technologie de compréhension spatiale principale. La bibliothèque HoloToolkit. SpatialUnderstanding encapsule cette technologie, ce qui vous permet de trouver rapidement des espaces vides sur les murs, de placer des objets sur le plafond, d’identifier le positionnement d’un personnage et une multitude d’autres requêtes de compréhension spatiale.

Tout le code source est inclus, ce qui vous permet de le personnaliser en fonction de vos besoins et de partager vos améliorations avec la communauté. Le code du C++ solveur a été encapsulé dans une dll UWP et exposé à Unity avec une chute de Prefab contenue dans le MixedRealityToolkit.

### <a name="understanding-modules"></a>Fonctionnement des modules

Il existe trois interfaces principales exposées par le module: la topologie pour les requêtes spatiales et spatiales simples, la forme pour la détection d’objets et le solveur de positionnement des objets pour le positionnement basé sur les contraintes des jeux d’objets. Chacun d’eux est décrit ci-dessous. En plus des trois interfaces de module principales, une interface de type Ray peut être utilisée pour récupérer des types de surfaces avec balises et un maillage PlaySpace à l’eau personnalisé peut être copié.

### <a name="ray-casting"></a>Conversion de rayon

Une fois la salle analysée et finalisée, les étiquettes sont générées en interne pour les surfaces comme le plancher, le plafond et les murs. La fonction «PlayspaceRaycast» prend un rayon et retourne si le rayon entre en conflit avec une surface connue et, le cas échéant, des informations sur cette surface sous la forme d’un «RaycastResult».

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

En interne, raycast est calculé par rapport à la représentation voxel 8cm cube calculée du PlaySpace. Chaque voxel contient un ensemble d’éléments surface avec des données de topologie traitées (surfels). Le surfels contenu dans la cellule voxel intersectée est comparé et la meilleure correspondance est utilisée pour rechercher les informations de topologie. Ces données de topologie contiennent l’étiquetage renvoyé sous la forme de l’énumération «SurfaceTypes», ainsi que la surface d’exposition de la surface intersectée.

Dans l’exemple Unity, le curseur convertit chaque image de rayon. Tout d’abord, contre les conflits avec Unity. Deuxièmement, par rapport à la représentation universelle du module de présentation. Enfin, les éléments d’interface utilisateur. Dans cette application, l’interface utilisateur est prioritaire, puis le résultat de la compréhension et enfin, les conflits avec Unity. Le SurfaceType est signalé en tant que texte en regard du curseur.

![Le type de surface est étiqueté en regard du curseur](images/su-raycastresults-300px.jpg)<br>
*Le type de surface est étiqueté en regard du curseur*

### <a name="topology-queries"></a>Requêtes de topologie

Dans la DLL, le gestionnaire de topologie gère l’étiquetage de l’environnement. Comme indiqué ci-dessus, la plupart des données sont stockées dans surfels, contenues dans un volume voxel. En outre, la structure «PlaySpaceInfos» est utilisée pour stocker des informations sur le PlaySpace, y compris l’alignement universel (plus de détails à ce niveau ci-dessous), le plancher et la hauteur du plafond. Les heuristiques sont utilisées pour déterminer l’étage, le plafond et les murs. Par exemple, la surface horizontale la plus grande et la plus basse avec une surface d’exposition supérieure à 1 m2 est considérée comme le plancher. Notez que le chemin d’accès de l’appareil photo pendant le processus d’analyse est également utilisé dans ce processus.

Un sous-ensemble des requêtes exposées par le gestionnaire de topologie est exposé via la dll. Les requêtes de topologie exposées sont les suivantes.

```cpp
QueryTopology_FindPositionsOnWalls
QueryTopology_FindLargePositionsOnWalls
QueryTopology_FindLargestWall
QueryTopology_FindPositionsOnFloor
QueryTopology_FindLargestPositionsOnFloor
QueryTopology_FindPositionsSittable
```

Chacune des requêtes a un ensemble de paramètres, spécifique au type de requête. Dans l’exemple suivant, l’utilisateur spécifie la hauteur minimale & largeur du volume souhaité, la hauteur minimale de placement au-dessus du plancher et la quantité minimale d’autorisation devant le volume. Toutes les mesures sont en mètres.

```cpp
EXTERN_C __declspec(dllexport) int QueryTopology_FindPositionsOnWalls(
    _In_ float minHeightOfWallSpace,
    _In_ float minWidthOfWallSpace,
    _In_ float minHeightAboveFloor,
    _In_ float minFacingClearance,
    _In_ int locationCount,
    _Inout_ Dll_Interface::TopologyResult* locationData)
```

Chacune de ces requêtes utilise un tableau pré-alloué de structures «TopologyResult». Le paramètre «locationCount» spécifie la longueur du tableau transmis. La valeur de retour indique le nombre d’emplacements retournés. Ce nombre n’est jamais supérieur au paramètre «locationCount» passé.

«TopologyResult» contient la position centrale du volume retourné, le sens de face (c’est-à-dire normal) et les dimensions de l’espace trouvé.

```cpp
struct TopologyResult 
{ 
    DirectX::XMFLOAT3 position; 
    DirectX::XMFLOAT3 normal; 
    float width; 
    float length;
};
```

Notez que dans l’exemple Unity, chacune de ces requêtes est liée à un bouton dans le panneau de l’interface utilisateur virtuelle. L’exemple code en dur les paramètres de chacune de ces requêtes à des valeurs raisonnables. Pour plus d’exemples, consultez SpaceVisualizer.cs dans l’exemple de code.

### <a name="shape-queries"></a>Requêtes de forme

À l’intérieur de la dll, l’analyseur de forme («ShapeAnalyzer_W») utilise l’analyseur de topologie pour faire correspondre les formes personnalisées définies par l’utilisateur. L’exemple Unity définit un ensemble de formes et expose les résultats par le biais du menu requête dans l’application, dans l’onglet forme. L’objectif est que l’utilisateur peut définir ses propres requêtes de forme d’objet et les utiliser, selon les besoins de leur application.

Notez que l’analyse des formes fonctionne uniquement sur des surfaces horizontales. Un canapé, par exemple, est défini par la surface du siège plat et le haut à l’arrière de la canapé. La requête Shape recherche deux surfaces d’une taille, d’une hauteur et d’une plage d’aspect spécifiques, les deux surfaces étant alignées et connectées. En utilisant la terminologie des API, le siège de la canapé et l’arrière-plan sont des composants de forme et les exigences d’alignement sont des contraintes de composant de forme.

Voici un exemple de requête défini dans l’exemple Unity (ShapeDefinition.cs) pour les objets «sittable».

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

Chaque requête de forme est définie par un ensemble de composants de forme, chacun avec un ensemble de contraintes de composant et un ensemble de contraintes de forme qui répertorient les dépendances entre les composants. Cet exemple inclut trois contraintes dans une définition de composant unique et aucune contrainte de forme entre les composants (étant donné qu’il n’y a qu’un seul composant).

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

Les fonctions wrapper sont fournies dans le module Unity pour faciliter la création de définitions de formes personnalisées. La liste complète des contraintes de composant et de forme se trouve dans «SpatialUnderstandingDll.cs» dans les structures «ShapeComponentConstraint» et «ShapeConstraint».

![Forme de rectangle trouvée sur cette surface](images/su-shapequery-300px.jpg)<br>
*Forme de rectangle trouvée sur cette surface*

### <a name="object-placement-solver"></a>Solveur de positionnement des objets

Le solveur de placement d’objet peut être utilisé pour identifier les emplacements idéaux dans la salle physique pour placer vos objets. Le solveur trouvera l’emplacement le mieux adapté en fonction des contraintes et règles d’objet. En outre, les requêtes d’objet sont conservées jusqu’à ce que l’objet soit supprimé avec les appels «Solver_RemoveObject» ou «Solver_RemoveAllObjects», ce qui permet le placement de plusieurs objets avec restriction. Les requêtes de placement d’objets se composent de trois parties: le type de placement avec des paramètres, une liste de règles et une liste de contraintes. Pour exécuter une requête, utilisez l’API suivante.

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

Cette fonction accepte un nom d’objet, une définition de placement et une liste de règles et de contraintes. Les C# wrappers fournissent des fonctions d’assistance de construction pour faciliter la création de règles et de contraintes. La définition de placement contient le type de requête, c’est-à-dire l’un des éléments suivants.

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

Chacun des types de placement a un ensemble de paramètres propre au type. La structure «ObjectPlacementDefinition» contient un ensemble de fonctions d’assistance statiques pour la création de ces définitions. Par exemple, pour trouver un endroit où placer un objet sur l’étage, vous pouvez utiliser la fonction suivante. public static ObjectPlacementDefinition Create_OnFloor (Vector3 halfDims) en plus du type de placement, vous pouvez fournir un ensemble de règles et de contraintes. Les règles ne peuvent pas être violées. Les emplacements d’emplacement possibles qui satisfont au type et aux règles sont ensuite optimisés par rapport au jeu de contraintes afin de sélectionner l’emplacement de placement optimal. Chacune des règles et contraintes peut être créée par les fonctions de création statique fournies. Vous trouverez ci-dessous un exemple de fonction de construction de règle et de contrainte.

```cs
public static ObjectPlacementRule Create_AwayFromPosition(
    Vector3 position, float minDistance)
public static ObjectPlacementConstraint Create_NearPoint(
    Vector3 position, float minDistance = 0.0f, float maxDistance = 0.0f)
```

La requête de placement d’objet ci-dessous recherche un endroit où placer un cube demi-mètre sur le bord d’une surface, à l’écart des autres objets placés précédemment et près du centre de la pièce.

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

En cas de réussite, une structure «ObjectPlacementResult» contenant la position, les dimensions et l’orientation de placement est retournée. En outre, le placement est ajouté à la liste interne des objets placés de la dll. Les requêtes d’emplacement suivantes prennent en compte cet objet. Le fichier «LevelSolver.cs» dans l’exemple Unity contient plus d’exemples de requêtes.

![Résultats de l’emplacement des objets](images/su-objectplacement-1000px.jpg)<br>
*Figure 3: La zone bleue comment le résultat de trois positions sur les requêtes Floor est en dehors des règles de position de l’appareil photo*

Lors de la résolution de l’emplacement de positionnement de plusieurs objets requis pour un scénario de niveau ou d’application, commencez par résoudre les objets indispensables et volumineux afin d’optimiser la probabilité qu’un espace soit trouvé. L’ordre de placement est important. Si vous ne trouvez pas de placement d’objet, essayez des configurations moins restreintes. Avoir un ensemble de configurations de secours est essentiel à la prise en charge des fonctionnalités dans de nombreuses configurations de salles.

### <a name="room-scanning-process"></a>Processus d’analyse de la salle

Bien que la solution de mappage spatial fournie par le HoloLens soit conçue pour être suffisamment générique pour répondre aux besoins de la gamme complète des espaces à problème, le module de compréhension spatiale a été conçu pour prendre en charge les besoins de deux jeux spécifiques. Sa solution est structurée autour d’un processus et d’un ensemble d’hypothèses spécifiques, résumés ci-dessous.

```
Fixed size playspace – The user specifies the maximum playspace size in the init call.

One-time scan process – 
    The process requires a discrete scanning phase where the user walks around,
    defining the playspace. 
    Query functions will not function until after the scan has been finalized.
```

«Peinture» PlaySpace pilotée par l’utilisateur: au cours de la phase d’analyse, l’utilisateur se déplace et regarde le rythme des lectures, en peignant efficacement les zones qui doivent être incluses. La maille générée est importante pour fournir des commentaires de l’utilisateur au cours de cette phase. Installation à la page d’hébergement ou d’Office: les fonctions de requête sont conçues autour des surfaces plates et des parois à des angles droits. Il s’agit d’une limitation souple. Toutefois, pendant la phase d’analyse, une analyse de l’axe principal est effectuée pour optimiser la facettisation du maillage le long de l’axe principal et de l’axe secondaire. Le fichier SpatialUnderstanding.cs inclus gère le processus de phase d’analyse. Il appelle les fonctions suivantes.

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

Le workflow d’analyse, piloté par le comportement «SpatialUnderstanding», appelle InitScan, puis UpdateScan chaque frame. Lorsque la requête de statistiques signale une couverture raisonnable, l’utilisateur est autorisé à airtap d’appeler RequestFinish pour indiquer la fin de la phase d’analyse. UpdateScan continue à être appelé jusqu’à ce qu’il retourne la valeur indiquant que la dll a terminé le traitement.

### <a name="understanding-mesh"></a>Fonctionnement de la maille

La dll de compréhension stocke en interne le PlaySpace sous la forme d’une grille de cubes voxel 8cm dimensionnés. Au cours de la phase initiale d’analyse, une analyse de composant principale est effectuée pour déterminer les axes de la salle. En interne, elle stocke son espace voxel aligné sur ces axes. Une maille est générée environ chaque seconde en extrayant le isosurface du volume voxel. 

![Maille générée produite à partir du volume voxel](images/su-custommesh.jpg)<br>
*Maille générée produite à partir du volume voxel*

## <a name="troubleshooting"></a>Résolution des problèmes
* Vérifiez que vous avez défini la fonctionnalité [SpatialPerception](#setting-the-spatialperception-capability)
* Lorsque le suivi est perdu, l’événement OnSurfaceChanged suivant supprime tous les maillages.

## <a name="spatial-mapping-in-mixed-reality-toolkit"></a>Mappage spatial dans le Toolkit de réalité mixte
Pour plus d’informations sur l’utilisation du mappage spatial avec Mixed Reality Toolkit v2, consultez la <a href="https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/SpatialAwareness/SpatialAwarenessGettingStarted.html" target="_blank">section relative à la sensibilisation spatiale</a> des documents MRTK.

## <a name="see-also"></a>Voir aussi
* [Réalité mixte - Fonctionnalités spatiales - Cours 230 : Mappage spatial](holograms-230.md)
* [Systèmes de coordonnées](coordinate-systems.md)
* [Systèmes de coordonnées dans Unity](coordinate-systems-in-unity.md)
* <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">MixedRealityToolkit</a>
* <a href="http://docs.unity3d.com/ScriptReference/MeshFilter.html" target="_blank">UnityEngine. MeshFilter</a>
* <a href="http://docs.unity3d.com/ScriptReference/MeshCollider.html" target="_blank">UnityEngine. MeshCollider</a>
* <a href="http://docs.unity3d.com/ScriptReference/Bounds.html" target="_blank">Limites de UnityEngine.</a>
