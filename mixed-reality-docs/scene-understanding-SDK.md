---
title: Scène Understanding SDK
description: Guide de programmation du SDK Scene Understanding
author: szymons
ms.author: szymons
ms.date: 07/08/2019
ms.topic: article
keywords: Compréhension des scènes, mappage spatial, Windows Mixed Reality, Unity
ms.openlocfilehash: e31c0b1c954516db2dbb025d849dba3e3203a04b
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438299"
---
# <a name="scene-understanding-sdk-overview"></a>Présentation du SDK présentation de Scene

L’objectif de la compréhension des scènes est de transformer les données de capteur d’environnement non structurées capturées par votre appareil de réalité mixte et de le convertir en une représentation puissante mais abstraite, intuitive et facile à développer pour. Le kit de développement logiciel (SDK) joue le rôle de couche de communication entre votre application et le runtime Understanding. Elle est destinée à imiter les constructions standard existantes, telles que les graphiques de scène 3D pour les représentations 3D et les rectangles/panneaux 2D pour les applications 2D. Tandis que la construction de scènes comprenant les imitations sera mappée aux frameworks concrets que vous pouvez utiliser, en général SceneUnderstanding est une infrastructure agnostique qui autorise l’interopérabilité entre des frameworks variés qui interagissent avec elle. À mesure que la compréhension de la scène évolue, le rôle du kit de développement logiciel (SDK) consiste à s’assurer que de nouvelles représentations et fonctionnalités continuent à être exposées au sein d’une infrastructure unifiée. Dans ce document, nous allons commencer par introduire des concepts de haut niveau qui vous aideront à vous familiariser avec l’environnement de développement/l’utilisation, puis à fournir une documentation plus détaillée pour des classes et des constructions spécifiques.

## <a name="where-do-i-get-the-sdk"></a>Où puis-je me procurer le kit de développement logiciel ?

Le kit de développement logiciel (SDK) SceneUnderstanding peut être téléchargé via NuGet.

[SDK SceneUnderstanding](https://www.nuget.org/packages/Microsoft.MixedReality.SceneUnderstanding/)

**Remarque :** la version la plus récente dépend de la version préliminaire de exploitation et vous devez activer les packages de préversions pour les afficher.

Depuis la version 0.5.2022-RC, Scene Understanding prend en charge les C# projections de langage pour et C++ permettant aux applications de développer des applications pour les plateformes Win32 ou UWP. À compter de cette version, SceneUnderstanding prend en charge Unity dans le cadre de la prise en charge de l’éditeur, avec la SceneObserver qui est utilisée uniquement pour communiquer avec HoloLens2. 

SceneUnderstanding requiert SDK Windows version 18362 ou ultérieure. 

Si vous utilisez le kit de développement logiciel (SDK) dans un projet Unity, utilisez [NuGet pour Unity](https://github.com/GlitchEnzo/NuGetForUnity) pour installer le package dans votre projet.

## <a name="conceptual-overview"></a>Vue d’ensemble conceptuelle

### <a name="the-scene"></a>La scène

Votre appareil de réalité mixte intègre constamment des informations sur ce qu’il voit dans votre environnement. La compréhension de la scène entonnoir toutes ces sources de données et produit une seule abstraction cohésive. La compréhension des scènes génère des scènes qui constituent une composition de [SceneObjects](scene-understanding-SDK.md#sceneobjects) représentant une instance d’une seule chose (par exemple, un mur/un plafond/étage). Les objets de scène sont eux-mêmes une composition de [SceneComponents](scene-understanding-SDK.md#scenecomponents) qui représentent des éléments plus granulaires qui composent ce SceneObject. Les exemples de composants sont les Quad et les maillages, mais à l’avenir, ils peuvent représenter des zones englobantes, des mehses de collision, des métadonnées, etc.

Le processus de conversion des données de capteur brutes en scène est une opération potentiellement coûteuse qui peut prendre des secondes pour les espaces moyens (~ 10x10m) à minutes pour les espaces de très grande taille (~ 50x50m). par conséquent, il ne s’agit pas d’un objet qui est calculé par l’appareil sans demande de l’application. Au lieu de cela, la génération de scènes est déclenchée par votre application à la demande. La classe SceneObserver a des méthodes statiques qui peuvent calculer ou désérialiser une scène, que vous pouvez ensuite énumérer/interagir avec. L’action « Compute » est exécutée à la demande et s’exécute sur l’UC, mais dans un processus séparé (le pilote de réalité mixte). Toutefois, pendant que nous effectuons le calcul dans un autre processus, les données de scène obtenues sont stockées et conservées dans votre application dans l’objet de scène. 

Vous trouverez ci-dessous un diagramme qui illustre ce processus et montre des exemples de deux applications interagissant avec le runtime de la vision de la scène. 

![Diagramme de processus](images/SU-ProcessFlow.png)

La partie gauche est un diagramme du runtime de réalité mixte qui est toujours actif et s’exécute dans son propre processus. Ce Runtime est chargé d’effectuer le suivi des appareils, le mappage spatial et d’autres opérations que la présentation de Scene utilise pour comprendre et expliquer le monde autour de vous. Sur le côté droit du diagramme, nous présentons deux applications théoriques qui utilisent la compréhension des scènes. La première application interface avec MRTK, qui utilise le kit de développement logiciel (SDK) de scène en interne, la deuxième application calcule et utilise deux instances de scène sepereate. Les trois scènes dans ce diagramme génèrent des instances distinctes des scènes, le pilote ne suit pas l’état global qui est partagé entre les applications et les objets de scène dans une scène ne sont pas trouvés dans un autre. La compréhension de la scène fournit un mécanisme de suivi au fil du temps, mais cette opération s’effectue à l’aide du kit de développement logiciel (SDK) et du code, le code qui effectue ce suivi s’exécute dans le kit de développement logiciel (SDK) du processus de votre application

Étant donné que chaque scène stocke ses données dans l’espace mémoire de votre application, vous pouvez supposer que toutes les fonctions de l’objet de la scène ou de ses données internes sont toujours exécutées dans le processus de votre application.

### <a name="layout"></a>Mise en page

Pour travailler avec la compréhension des scènes, il peut être utile de savoir et de comprendre comment le runtime représente des composants logiquement et physiquement. La scène représente des données avec une disposition spécifique qui a été choisie comme simple tout en conservant une structure sous-jacente qui est pliable pour répondre aux exigences futures sans avoir besoin de révisions majeures. Pour ce faire, la scène stocke tous les composants (blocs de construction pour tous les objets de scène) dans une liste plate et définit la hiérarchie et la composition par le biais de références où des composants spécifiques référencent d’autres.

Ci-dessous, nous présentons un exemple de structure dans sa forme plate et logique.

<table>
<tr><th>Disposition logique</th><th>Disposition physique</th></tr>
<tr>
<td>
<ul>
  Écran
  <ul>
  <li>SceneObject_1
    <ul>
      <li>SceneMesh_1</li>
      <li>SceneQuad_1</li>
      <li>SceneQuad_2</li>
    </ul>
  </li>
  <li>SceneObject_2
    <ul>
      <li>SceneQuad_1</li>
      <li>SceneQuad_3</li>
      </li></ul>
  </li>
  <li>SceneObject_3
    <ul>
      <li>SceneMesh_3</li>
    </ul>
  </ul>
</ul>
</td>
<td>
<ul>
  <li>SceneObject_1</li>
  <li>SceneObject_2</li>
  <li>SceneObject_3</li>
  <li>SceneQuad_1</li>
  <li>SceneQuad_2</li>
  <li>SceneQuad_3</li>
  <li>SceneMesh_1</li>
  <li>SceneMesh_2</li>
</ul>
</td>
</tr>
</table>

Cette illustration met en évidence la différence entre la disposition physique et logique de la scène. À droite, nous voyons la disposition hiérarchique des données que votre application voit lors de l’énumération de la scène. À gauche, nous voyons que la scène est en fait composée de 12 composants distincts qui sont accessibles individuellement si nécessaire. Lors du traitement d’une nouvelle scène, nous pensons que les applications parcourent cette hiérarchie logiquement, toutefois, lors du suivi entre les mises à jour de la scène, certaines applications peuvent uniquement être intéressées à cibler des composants spécifiques qui sont partagés entre deux scènes.

## <a name="api-overview"></a>Vue d’ensemble des API

La section suivante fournit une vue d’ensemble des constructions de la présentation des scènes. La lecture de cette section vous donne une idée de la façon dont les scènes sont représentées, ainsi que de l’utilisation des différents composants. La section suivante fournit des exemples de code concrets et des détails supplémentaires qui sont brillants dans cette vue d’ensemble.

Tous les types décrits ci-dessous résident dans l’espace de noms `Microsoft.MixedReality.SceneUnderstanding`.

### <a name="scenecomponents"></a>SceneComponents

Maintenant que vous comprenez la disposition logique des scènes, nous pouvons maintenant présenter le concept de SceneComponents et la façon dont ils sont utilisés pour composer la hiérarchie. SceneComponents sont les décompositions les plus granulaires de SceneUnderstanding qui représentent une seule base, par exemple une maille ou un quadruple-Box ou un cadre englobant. Les SceneComponents sont des éléments qui peuvent être mis à jour de manière indépendante et peuvent être référencés par d’autres SceneComponents, de sorte qu’ils disposent d’un ID unique de propriété globale unique, qui autorise ce type de mécanisme de suivi/référencement. Les ID sont utilisés pour la composition logique de la hiérarchie des scènes, ainsi que pour la persistance des objets (opération consistant à mettre à jour une scène par rapport à une autre.) 

Si vous traitez toutes les scènes nouvellement calculées comme étant distinctes et que vous énumérez simplement toutes les données qu’elle contient, les ID sont en grande partie transparents pour vous. Toutefois, si vous envisagez de suivre des composants sur plusieurs mises à jour, vous allez utiliser les ID pour indexer et Rechercher des SceneComponents entre les objets de scène.

### <a name="sceneobjects"></a>SceneObjects

Un SceneObject est un SceneComponent qui représente une instance d’un « élément », par exemple un mur, un étage, un plafond, etc. exprimé par leur propriété Kind. Les SceneObjects sont géométriques et, par conséquent, ont des fonctions et des propriétés qui représentent leur emplacement dans l’espace, mais elles ne contiennent pas de structure géométrique ou logique. Au lieu de cela, SceneObjects référence d’autres SceneComponents, en particulier SceneQuads et SceneMeshes, qui fournissent les représentations variées prises en charge par le système. Quand une nouvelle scène est calculée, votre application va probablement énumérer le SceneObjects de la scène pour traiter ce qui l’intéresse.

SceneObjects peut avoir l’un des éléments suivants :

<table>
<tr>
<th>SceneObjectKind</th> <th>Description</th>
</tr>
<tr><td>Arrière-plan</td><td>Le SceneObject est connu pour <b>ne pas</b> être l’un des autres types d’objets de scène reconnus. Cette classe ne doit pas être confondue avec Unknown, où l’arrière-plan est connu comme étant un mur/plancher/plafond, etc... alors que inconnu n’est pas encore catégorisé.</b></td></tr>
<tr><td>Encastre</td><td>Un mur physique. Les murs sont supposés être des structures environnementales immobilières.</td></tr>
<tr><td>Floor</td><td>Les étages sont des surfaces sur lesquelles il est possible de parcourir. Remarque : les escaliers ne sont pas des étages. Notez également que les étages supposent une surface pouvant être guidée et qu’il n’y a donc pas d’hypothèse explicite d’un étage singulier. Structures à plusieurs niveaux, rampes, etc... doit tous être classifiés en tant que plancher.</td></tr>
<tr><td>plafond</td><td>Surface supérieure d’une salle.</td></tr>
<tr><td>Plateforme</td><td>Grande surface plate sur laquelle vous pouvez placer des hologrammes. Elles ont tendance à représenter des tables, des plans de plan et d’autres grandes surfaces horizontales.</td></tr>
<tr><td>World</td><td>Étiquette réservée pour les données géométriques indépendantes de l’étiquetage. La maille générée par la définition de l’indicateur de mise à jour EnableWorldMesh est classée comme monde.</td></tr>
<tr><td>Inconnu</td><td>Cet objet de scène n’a pas encore été classé et affecté un genre. Cela ne doit pas être confondu avec l’arrière-plan, car cet objet peut être n’importe quoi, le système n’a pas encore pu trouver une classification suffisamment importante pour l’informatique.</td></tr>
</tr>
</table>

### <a name="scenemesh"></a>SceneMesh

Un SceneMesh est un SceneComponent qui se rapproche de la géométrie des objets géométriques arbitraires à l’aide d’une liste de triangles. Les SceneMeshes sont utilisés dans plusieurs contextes différents, ils peuvent représenter des composants de la structure de cellules étanches ou en tant que WorldMesh qui représente le maillage de mappage spatial non lié à la scène. Les données d’index et de vertex fournies avec chaque maille utilisent la même disposition familière que les [mémoires tampons de vertex et d’index](https://msdn.microsoft.com/library/windows/desktop/bb147325%28v=vs.85%29.aspx) utilisées pour le rendu des maillages de triangle dans toutes les API de rendu modernes. Notez que, dans la compréhension de la scène, les maillages utilisent des index 32 bits et peuvent avoir besoin d’être décomposés en segments pour certains moteurs de rendu.

### <a name="scenequad"></a>SceneQuad

Un SceneQuad est un SceneComponent qui représente des surfaces 2D qui occupent le monde 3D. SceneQuads peut être utilisé de la même façon que les plans ARKit ARPlaneAnchor ou ARCore, mais ils offrent des fonctionnalités de haut niveau comme des canevas 2D à utiliser par les applications plates, ou une expérience utilisateur améliorée. des API spécifiques 2D sont fournies pour les quatre cœurs qui facilitent l’utilisation de l’emplacement et de la disposition, et le développement (à l’exception du rendu) avec quatre cœurs doit avoir un sens plus semblable à l’utilisation de canevas 2D que les maillages 3D.

## <a name="scene-understanding-sdk-details-and-reference"></a>Description et informations de référence du SDK

La section suivante vous aidera à vous familiariser avec les principes fondamentaux de SceneUnderstanding. Cette section doit vous fournir les principes de base, à partir desquels vous devez disposer d’un contexte suffisant pour parcourir les exemples d’applications et voir comment SceneUnderstanding est utilisé de manière holistique.

### <a name="initialization"></a>Initialisation

La première étape de l’utilisation de SceneUnderstanding est de permettre à votre application d’obtenir une référence à un objet de scène. Cette opération peut être effectuée de deux manières : une scène peut être calculée par le pilote, ou une scène existante qui a été calculée dans le passé peut être désérialisée. Ce dernier est particulièrement utile pour travailler avec SceneUnderstanding pendant le développement, où les applications et les expériences peuvent être rapidement prototypées sans appareil de réalité mixte.

Les scènes sont calculées à l’aide d’un SceneObserver. Avant de créer une scène, votre application doit interroger votre appareil pour s’assurer qu’il prend en charge SceneUnderstanding, ainsi que pour demander l’accès utilisateur aux informations dont SceneUnderstanding a besoin.

```cs
if (SceneObserver.IsSupported())
{
    // Handle the error
}

// This call should grant the access we need.
await SceneObserver.RequestAccessAsync();
```

Si RequestAccessAsync () n’est pas appelé, le calcul d’une nouvelle scène échoue. Ensuite, nous allons calculer une nouvelle scène enracinée autour du casque de la réalité mixte et ayant un rayon de 10 mètres.

```cs
// Create Query settings for the scene update
SceneQuerySettings querySettings;

querySettings.EnableSceneObjectQuads = true;                                       // Requests that the scene updates quads.
querySettings.EnableSceneObjectMeshes = true;                                      // Requests that the scene updates watertight mesh data.
querySettings.EnableOnlyObservedSceneObjects = false;                              // Do not explicitly turn off quad inference.
querySettings.EnableWorldMesh = true;                                              // Requests a static version of the spatial mapping mesh.
querySettings.RequestedMeshLevelOfDetail = SceneMeshLevelOfDetail.Fine;            // Requests the finest LOD of the static spatial mapping mesh.

// Initialize a new Scene
Scene myScene = SceneObserver.ComputeAsync(querySettings, 10.0f).GetAwaiter().GetResult();
```

### <a name="initialization-from-data-aka-the-pc-path"></a>Initialisation à partir des données (alias. le chemin d’accès du PC)

Si les scènes peuvent être calculées pour une consommation directe, elles peuvent également être calculées sous forme sérialisée pour une utilisation ultérieure. Cela s’est avéré très utile pour le développement, car il permet aux développeurs de travailler dans et de tester la compréhension des scènes sans avoir besoin d’un appareil. L’acte de sérialisation d’une scène est quasiment identique à son calcul, les données sont retournées à votre application au lieu d’être désérialisées localement par le kit de développement logiciel (SDK). Vous pouvez ensuite le désérialiser vous-même ou l’enregistrer pour une utilisation ultérieure.

```cs
// Create Query settings for the scene update
SceneQuerySettings querySettings;

// Compute a scene but serialized as a byte array
SceneBuffer newSceneBuffer = SceneObserver.ComputeSerializedAsync(querySettings, 10.0f).GetAwaiter().GetResult();

// If we want to use it immediately we can de-serialize the scene ourselves
byte[] newSceneData = new byte[newSceneBuffer.Size];
newSceneBuffer.GetData(newSceneData);
Scene mySceneDeSerialized = Scene.Deserialize(newSceneData);

// Save newSceneBlob for later
```

### <a name="sceneobject-enumeration"></a>Énumération SceneObject

Maintenant que votre application a une scène, votre application va regarder et interagir avec SceneObjects. Pour ce faire, accédez à la propriété **SceneObjects** :

```cs
SceneObject firstFloor = null;

// Find the first floor object
foreach (var sceneObject in myScene.SceneObjects)
{
    if (sceneObject.Kind == SceneObjectKind.Floor)
    {
        firstFloor = sceneObject;
        break;
    }
}
```

### <a name="component-update-and-re-finding-components"></a>Mise à jour des composants et rerecherche de composants

Une autre fonction récupère les composants de la scène appelée ***FindComponent***. Cette fonction est utile lors de la mise à jour des objets de suivi et de leur recherche dans des scènes ultérieures. Le code suivant calcule une nouvelle scène par rapport à une scène précédente, puis trouve le plancher dans la nouvelle scène.

```cs
// Compute a new scene, and tell the system that we want to compute relative to the previous scene
Scene myNextScene = SceneObserver.ComputeAsync(querySettings, 10.0f, myScene).GetAwaiter().GetResult();

// Use the Id for the floor we found last time, and find it again
firstFloor = (SceneObject)myNextScene.FindComponent(firstFloor.Id);

if (firstFloor != null)
{
    // We found it again, we can now update the transforms of all objects we attatched to this floor transform
}
```

## <a name="accessing-meshes-and-quads-from-scene-objects"></a>Accès aux maillages et aux quads à partir d’objets de scène

Une fois les SceneObjects trouvés, votre application souhaitera probablement accéder aux données contenues dans les quadruples/les maillages dont elle est composée. Ces données sont accessibles avec les propriétés ***quads*** et ***meshes*** . Le code suivant énumère tous les Quad et les maillages de notre objet Floor.

```cs

// Get the transform for the SceneObject
System.Numerics.Matrix4x4 objectToSceneOrigin = firstFloor.GetLocationAsMatrix();

// Enumerate quads
foreach (var quad in firstFloor.Quads)
{
    // Process quads
}

// Enumerate meshes
foreach (var mesh in firstFloor.Meshes)
{
    // Process meshes
}
```

Notez qu’il s’agit du SceneObject qui a la transformation par rapport à l’origine de la scène. Cela est dû au fait que SceneObject représente une instance d’un « élément » et qu’il est localisable dans l’espace, les Quad et les maillages représentent une géométrie transformée par rapport à leur parent. Il est possible pour des SceneObjects distincts de référencer le même SceneComponewnts SceneMesh/SceneQuad, et il est également possible qu’un SceneObject ait plus d’un SceneMesh/SceneQuad.

### <a name="dealing-with-transforms"></a>Traitement des transformations

La compréhension des scènes a fait une tentative délibérée d’alignement avec les représentations de scène 3D traditionnelles lors du traitement des transformations. Chaque scène est donc confinée à un système de coordonnées unique, à l’instar des représentations environnementales 3D les plus courantes. Les SceneObjects fournissent chacun leur emplacement sous la forme d’une position et d’une orientation au sein de ce système de coordonnées. Si votre application traite des scènes qui étendent la limite de ce qu’une origine unique fournit peut ancrer SceneObjects à SpatialAnchors, ou générer plusieurs scènes et les fusionner, mais pour des raisons de simplicité, nous supposons que des scènes étanches existent dans leur propre origine localisée par un NodeId défini par Scene. OriginSpatialGraphNodeId.

Le code Unity suivant, par exemple, montre comment utiliser la perception de Windows et les API Unity pour aligner les systèmes de coordonnées ensemble. Pour plus d’informations sur les API de perception Windows et sur les [objets natifs de réalité mixte en Unity](https://docs.microsoft.com//windows/mixed-reality/unity-xrdevice-advanced) pour plus d’informations sur l’obtention d’un SpatialCoordinateSystem qui correspond à Unity, consultez [SpatialCoordinateSystem](https://docs.microsoft.com//uwp/api/windows.perception.spatial.spatialcoordinatesystem) et [SpatialGraphInteropPreview](https://docs.microsoft.com//uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview) . environnement d’origine, ainsi que la méthode d’extension `.ToUnity()` pour la conversion entre `System.Numerics.Matrix4x4` et `UnityEngine.Matrix4x4`.

```cs
public class SceneRootComponent : MonoBehavior
{
    public SpatialCoordinateSystem worldOrigin;
    public Scene scene;
    SpatialCoordinateSystem sceneOrigin;
    
    void Start()
    {
        // Initialize a SpatialCoordinateSystem for the scene's node in the system's Spatial Graph.
        scene.origin = SpatialGraphInteropPreview.CreateCoordinateSystemForNode(scene.OriginSpatialGraphNodeId);
    }
    
    void Update()
    {
        // Try to get the current transform of the scene's spatial graph node.
        // This may not be available, e.g. when tracking has been lost.
        var sceneToWorld = sceneOrigin.TryGetTransformTo(worldOrigin);
        if (sceneToWorld.HasValue)
        {
            // Convert the transform to Unity numerics and update the game object.
            var sceneToWorldUnity = sceneToWorld.Value.ToUnity();
            this.gameObject.transform.SetPositionAndRotation(sceneToWorldUnity.GetColumn(3), sceneToWorldUnity.rotation);
        }
    }
}
```

Chaque `SceneObject` a une propriété `Position` et `Orientation` qui peut être utilisée pour positionner le contenu correspondant par rapport à l’origine du `Scene`contenant. Par exemple, l’exemple suivantes suppose que le jeu est un enfant de la racine de la scène et affecte sa position et sa rotation locales pour qu’il s’aligne sur un `SceneObject`donné :

```cs
void SetLocalTransformFromSceneObject(GameObject gameObject, SceneObject sceneObject)
{
    gameObject.transform.localPosition = sceneObject.Position.ToUnity();
    gameObject.transform.localRotation = sceneObject.Orientation.ToUnity());
}
```

### <a name="quad"></a>Quadruple

Les Quad sont conçus pour faciliter les scénarios de positionnement 2D et doivent être considérés comme des extensions aux éléments d’expérience utilisateur 2D Canvas. Alors que les Quad sont des composants de SceneObjects et peuvent être rendus en 3D, les API Quad elles-mêmes partent du principe que les quatre cœurs sont des structures 2D. Elles offrent des informations telles que l’étendue, la forme et fournissent des API pour le positionnement.

Les Quad présentent des étendues rectangulaires, mais elles représentent des surfaces 2D de forme arbitraire. Pour activer la position sur ces surfaces 2D qui interagissent avec les utilitaires de l’environnement 3D quads, vous pouvez faire en sorte que cette interaction soit possible. Actuellement, la compréhension des scènes fournit deux fonctions telles que **FindCentermostPlacement** et **GetOcclusionMask**. FindCentermostPlacement est une API de haut niveau qui localise une position sur le quadruple dans laquelle un objet peut être placé et tente de trouver le meilleur emplacement pour votre objet, garantissant que le cadre englobant que vous fournissez se trouvera sur la surface sous-jacente.

L’exemple suivant montre comment Rechercher l’emplacement positionnable centermost et ancrer un hologramme au quadruple.

```cs
// This code assumes you already have a "Root" object that attaches the Scene's Origin.

// Find the first quad
foreach (var sceneObject in myScene.SceneObjects)
{
    // Find a wall
    if (sceneObject.Kind == SceneObjectKind.Wall)
    {
        // Get the quad
        var quads = sceneObject.Quads;
        if (quads.Count > 0)
        {
            // Find a good location for a 1mx1m object  
            System.Numerics.Vector2 location;
            if (quads[0].FindCentermostPlacement(new System.Numerics.Vector2(1.0f, 1.0f), out location))
            {
                // We found one, anchor something to the transform
                // Step 1: Create a new game object for the quad itself as a child of the scene root
                // Step 2: Set the local transform from quads[0].Position and quads[0].Orientation
                // Step 3: Create your hologram and set it as a child of the quad's game object
                // Step 4: Set the hologram's local tranform to a translation (location.x, location.y, 0)
            }
        }
    }
}
```

Les étapes 1-4 sont fortement dépendantes de votre infrastructure/implémentation particulière, mais les thèmes doivent être similaires. Il est important de noter que le quad représente simplement un plan 2D limité qui est localisé dans l’espace. En faisant savoir à votre moteur/infrastructure où se trouve le quad et la racine de vos objets par rapport au Quad, vos hologrammes se trouveront correctement avec repect dans le monde réel. Pour obtenir des informations plus détaillées, consultez nos exemples sur les quatre cœurs qui présentent des implémentations spécifiques.

### <a name="mesh"></a>Déjà

Les maillages représentent les représentations géométriques des objets ou des environnements. À l’instar du [mappage spatial](spatial-mapping.md), les données de vertex et d’index de maillage fournies avec chaque maillage de surface spatiale utilisent la même disposition familière que les mémoires tampons de vertex et d’index utilisées pour le rendu des maillages de triangle dans toutes les API de rendu modernes. Les positions de vertex sont fournies dans le système de coordonnées du `Scene`. Les API spécifiques utilisées pour référencer ces données sont les suivantes :

```cs
void GetTriangleIndices(int[] indices);
void GetVertices(System.Numerics.Vector3[] vertices);
```

Le code suivant fournit un exemple de génération d’une liste de triangles à partir de la structure de maillage :

```cs
uint[] indices = new uint[mesh.TriangleIndexCount];
System.Numerics.Vector3[] positions = new System.Numerics.Vector3[mesh.VertexCount];

mesh.GetTriangleIndices(indices);
mesh.GetVertexPositions(positions);
```

Les mémoires tampons d’index/vertex doivent être > = nombre d’index/vertex, mais peuvent être de taille arbitraire, ce qui permet une réutilisation efficace de la mémoire.

## <a name="developing-with-scene-understandings"></a>Développement avec présentation des scènes

À ce stade, vous devez comprendre les principaux blocs de construction de la scène présentation du runtime et du kit de développement logiciel (SDK). La majeure partie de la puissance et de la complexité se trouve dans les modèles d’accès, l’interaction avec les frameworks 3D et les outils qui peuvent être écrits sur ces API pour effectuer des tâches plus avancées telles que la planification spatiale, l’analyse de la salle, la navigation, la physique, etc. Nous espérons capturer ces exemples dans des exemples qui devraient vous guider dans la bonne direction pour que vos scénarios brillent. S’il existe des exemples ou des scénarios que nous n’adressons pas, faites-le nous savoir et nous essaierons de documenter/prototyper ce dont vous avez besoin.

## <a name="see-also"></a>Articles associés

* [Mappage spatial](spatial-mapping.md)
* [Compréhension des scènes](scene-understanding.md)
