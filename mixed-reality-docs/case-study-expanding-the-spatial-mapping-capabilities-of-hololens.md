---
title: Étude de cas-développement des fonctionnalités de mappage spatial de HoloLens
description: Lors de la création de nos premières applications pour Microsoft HoloLens, nous étions impatients de voir à quel moment nous pourrions pousser les limites du mappage spatial sur l’appareil.
author: jevertt
ms.author: jemccull
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, HoloLens, mappage spatial
ms.openlocfilehash: 5142cb383d4408b29eb17eb5ede84d19b2533dc4
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73436725"
---
# <a name="case-study---expanding-the-spatial-mapping-capabilities-of-hololens"></a>Étude de cas-développement des fonctionnalités de mappage spatial de HoloLens

Lors de la création de nos premières applications pour Microsoft HoloLens, nous étions impatients de voir à quel moment nous pourrions pousser les limites du mappage spatial sur l’appareil. Jeff Evertt, ingénieur logiciel chez Microsoft Studios, explique comment une nouvelle technologie a été développée afin d’avoir davantage de contrôle sur la façon dont les hologrammes sont placés dans l’environnement réel d’un utilisateur.

> [!NOTE]
> HoloLens 2 implémente un nouveau [Runtime de présentation](scene-understanding.md)de la scène, qui fournit aux développeurs de réalité mixte une représentation environnementale structurée, conçue pour rendre le développement pour les applications qui prennent en charge l’environnement de manière intuitive. 

## <a name="watch-the-video"></a>Regarder la vidéo

>[!VIDEO https://www.youtube.com/embed/iUmTi3_Ynus]

## <a name="beyond-spatial-mapping"></a>Au-delà du mappage spatial

Pendant que nous travaillions sur des [fragments](https://www.microsoft.com/p/fragments/9nblggh5ggm8) et des [jeunes Conkers](https://www.microsoft.com/p/young-conker/9nblggh5ggk1), deux des premiers jeux pour HoloLens, nous avons constaté que lorsque nous avions utilisé des hologrammes dans le monde physique, nous avions besoin d’un niveau de compréhension plus élevé de l’utilisateur environnement. Chaque jeu avait ses propres besoins spécifiques en matière de placement : en fragments, par exemple, nous souhaitons pouvoir faire la distinction entre les différentes surfaces, telles que le plancher ou une table, pour placer des indices dans des emplacements pertinents. Nous souhaitons également pouvoir identifier les surfaces sur lesquelles les caractères holographiques de taille vie peuvent se trouver, tels qu’un canapé ou une chaise. Dans jeune Conker, nous souhaitons que Conker et ses adversaires soient en mesure d’utiliser des surfaces en relief dans la salle d’un joueur en tant que plateformes.

[Asobo Studios](https://www.asobostudio.com/index.html), notre partenaire de développement de ces jeux, est confronté à ce problème et a créé une technologie qui étend les fonctionnalités de mappage spatial de HoloLens. À l’aide de cela, nous pourrions analyser la salle d’un joueur et identifier des surfaces telles que des murs, des tables, des chaises et des sols. Elle nous a également donné la possibilité d’optimiser par rapport à un ensemble de contraintes pour déterminer le meilleur placement pour les objets holographiques.

## <a name="the-spatial-understanding-code"></a>Code de la compréhension spatiale

Nous avons pris le code d’origine de Asobo et créé une bibliothèque qui encapsule cette technologie. Microsoft et Asobo ont à présent ouvert ce code en open source et le rend disponible sur [MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialMapping) pour que vous l’utilisiez dans vos propres projets. Tout le code source est inclus, ce qui vous permet de le personnaliser en fonction de vos besoins et de partager vos améliorations avec la communauté. Le code du C++ solveur a été encapsulé dans une dll UWP et exposé à Unity avec une [Prefab de dépôt contenue dans MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/SpatialUnderstanding).

L’exemple Unity contient de nombreuses requêtes utiles qui vous permettent de rechercher des espaces vides sur les murs, de placer des objets sur le plafond ou sur des grands espaces sur le plancher, d’identifier des emplacements pour les caractères à asseoir et une multitude d’autres requêtes de compréhension spatiale.

Bien que la solution de mappage spatial fournie par HoloLens soit conçue pour être suffisamment générique pour répondre aux besoins de la gamme complète des espaces à problème, le module de compréhension spatiale a été conçu pour prendre en charge les besoins de deux jeux spécifiques. Par conséquent, sa solution est structurée autour d’un processus et d’un ensemble d’hypothèses spécifiques :
* **PlaySpace de taille fixe**: l’utilisateur spécifie la taille de PlaySpace maximale dans l’appel init.
* **Processus d’analyse à usage unique**: le processus nécessite une phase d’analyse discrète dans laquelle l’utilisateur se contourne et définit le PlaySpace. Les fonctions de requête ne fonctionneront pas tant que l’analyse n’aura pas été finalisée.
* **« Peinture » PlaySpace pilotée par l’utilisateur**: au cours de la phase d’analyse, l’utilisateur se déplace et explore le PlaySpace, ce qui a pour effet de peindre les zones qui doivent être incluses. La maille générée est importante pour fournir des commentaires de l’utilisateur au cours de cette phase.
* **Configuration de la page d’hébergement ou**de l’entreprise : les fonctions de requête sont conçues autour des surfaces plates et des parois à des angles droits. Il s’agit d’une limitation souple. Toutefois, pendant la phase d’analyse, une analyse de l’axe principal est effectuée pour optimiser la facettisation du maillage le long de l’axe principal et de l’axe secondaire.

### <a name="room-scanning-process"></a>Processus d’analyse de la salle

Lorsque vous chargez le module de compréhension spatiale, la première chose à faire est d’analyser votre espace. par conséquent, toutes les surfaces utilisables (telles que le plancher, le plafond et les murs) sont identifiées et étiquetées. Pendant le processus d’analyse, vous examinez votre espace et « peignez » les zones qui doivent être incluses dans l’analyse.

Le maillage vu pendant cette phase est un élément important de retour visuel qui permet aux utilisateurs de savoir quelles parties de la salle sont analysées. La DLL du module de compréhension spatiale stocke en interne le PlaySpace sous la forme d’une grille de cubes voxel de 8cm dimensionnés. Au cours de la phase initiale d’analyse, une analyse de composant principale est effectuée pour déterminer les axes de la salle. En interne, elle stocke son espace voxel aligné sur ces axes. Une maille est générée environ chaque seconde en extrayant le isosurface du volume voxel.

![Mappage spatial maillage en blanc et compréhension du maillage PlaySpace en vert](images/spatial-mapping-500px.png)

Mappage spatial maillage en blanc et compréhension du maillage PlaySpace en vert



Le fichier SpatialUnderstanding.cs inclus gère le processus de phase d’analyse. Il appelle les fonctions suivantes :
* **SpatialUnderstanding_Init**: appelée une fois au début.
* **GeneratePlayspace_InitScan**: indique que la phase d’analyse doit commencer.
* **GeneratePlayspace_UpdateScan_DynamicScan**: appelé chaque frame pour mettre à jour le processus d’analyse. La position et l’orientation de la caméra sont transmises et sont utilisées pour le processus de peinture PlaySpace décrit ci-dessus.
* **GeneratePlayspace_RequestFinish**: appelé pour finaliser le PlaySpace. Cela utilisera les zones « peintes » pendant la phase d’analyse pour définir et verrouiller le PlaySpace. L’application peut interroger des statistiques pendant la phase d’analyse et interroger la maille personnalisée pour fournir des commentaires utilisateur.
* **Import_UnderstandingMesh**: lors de l’analyse, le comportement de **SpatialUnderstandingCustomMesh** fourni par le module et placé sur le Prefab de compréhension interroge régulièrement le maillage personnalisé généré par le processus. En outre, cette opération est effectuée une fois de plus après la finalisation de l’analyse.

Le workflow de numérisation, piloté par le comportement **SpatialUnderstanding** appelle **InitScan**, puis **UpdateScan** chaque frame. Lorsque la requête de statistiques signale une couverture raisonnable, l’utilisateur peut airtap d’appeler **RequestFinish** pour indiquer la fin de la phase d’analyse. **UpdateScan** continue à être appelé jusqu’à ce qu’il retourne la valeur indiquant que la dll a terminé le traitement.

## <a name="the-queries"></a>Les requêtes

Une fois l’analyse terminée, vous pouvez accéder à trois types de requêtes différents dans l’interface :
* **Requêtes de topologie**: il s’agit de requêtes rapides basées sur la topologie de la salle analysée.
* **Requêtes de forme**: celles-ci utilisent les résultats de vos requêtes de topologie pour rechercher des surfaces horizontales qui correspondent parfaitement aux formes personnalisées que vous définissez.
* **Requêtes de placement d’objets**: il s’agit de requêtes plus complexes qui recherchent l’emplacement le mieux adapté en fonction d’un ensemble de règles et de contraintes pour l’objet.

Outre les trois requêtes principales, il existe une interface Raycasting qui peut être utilisée pour récupérer des types de surfaces avec balises et un maillage de salle étanche personnalisé peut être copié.

### <a name="topology-queries"></a>Requêtes de topologie

Dans la DLL, le gestionnaire de topologie gère l’étiquetage de l’environnement. Comme indiqué ci-dessus, la plupart des données sont stockées dans surfels, qui sont contenues dans un volume voxel. En outre, la structure **PlaySpaceInfos** est utilisée pour stocker des informations sur le PlaySpace, y compris l’alignement universel (plus de détails à ce niveau ci-dessous), le plancher et la hauteur du plafond.

Les heuristiques sont utilisées pour déterminer l’étage, le plafond et les murs. Par exemple, la surface horizontale la plus grande et la plus basse avec une surface d’exposition supérieure à 1 m2 est considérée comme le plancher. Notez que le chemin d’accès de l’appareil photo pendant le processus d’analyse est également utilisé dans ce processus.

Un sous-ensemble des requêtes exposées par le gestionnaire de topologie est exposé via la DLL. Les requêtes de topologie exposées sont les suivantes :
* QueryTopology_FindPositionsOnWalls
* QueryTopology_FindLargePositionsOnWalls
* QueryTopology_FindLargestWall
* QueryTopology_FindPositionsOnFloor
* QueryTopology_FindLargestPositionsOnFloor
* QueryTopology_FindPositionsSittable

Chacune des requêtes a un ensemble de paramètres, spécifique au type de requête. Dans l’exemple suivant, l’utilisateur spécifie la hauteur minimale & largeur du volume souhaité, la hauteur minimale de placement au-dessus du plancher et la quantité minimale d’autorisation devant le volume. Toutes les mesures sont en mètres.




```
EXTERN_C __declspec(dllexport) int QueryTopology_FindPositionsOnWalls(
          _In_ float minHeightOfWallSpace,
          _In_ float minWidthOfWallSpace,
          _In_ float minHeightAboveFloor,
          _In_ float minFacingClearance,
          _In_ int locationCount,
          _Inout_ Dll_Interface::TopologyResult* locationData)
```

Chacune de ces requêtes utilise un tableau pré-alloué de structures **TopologyResult** . Le paramètre **locationCount** spécifie la longueur du tableau transmis. La valeur de retour indique le nombre d’emplacements retournés. Ce nombre n’est jamais supérieur au paramètre **locationCount** passé.

Le **TopologyResult** contient la position centrale du volume retourné, le sens de face (c’est-à-dire normal) et les dimensions de l’espace trouvé.




```
struct TopologyResult
     {
          DirectX::XMFLOAT3 position;
          DirectX::XMFLOAT3 normal;
          float width;
          float length;
     };
```

Notez que dans l’exemple Unity, chacune de ces requêtes est liée à un bouton dans le panneau de l’interface utilisateur virtuelle. L’exemple code en dur les paramètres de chacune de ces requêtes à des valeurs raisonnables. Pour plus d’exemples, consultez *SpaceVisualizer.cs* dans l’exemple de code.

### <a name="shape-queries"></a>Requêtes de forme

À l’intérieur de la DLL, l’analyseur de forme (**ShapeAnalyzer_W**) utilise l’analyseur de topologie pour faire correspondre les formes personnalisées définies par l’utilisateur. L’exemple Unity a un ensemble prédéfini de formes qui s’affichent dans le menu requête, sous l’onglet forme.

Notez que l’analyse des formes fonctionne uniquement sur des surfaces horizontales. Un canapé, par exemple, est défini par la surface du siège plat et le haut à l’arrière de la canapé. La requête Shape recherche deux surfaces d’une taille, d’une hauteur et d’une plage d’aspect spécifiques, les deux surfaces étant alignées et connectées. À l’aide de la terminologie des API, le siège de la canapé et le haut de l’arrière du canapé sont des composants de forme et les exigences d’alignement sont des contraintes de composant de forme.

Voici un exemple de requête défini dans l’exemple Unity (**ShapeDefinition.cs**) pour les objets « sittable » :




```
shapeComponents = new List<ShapeComponent>()
     {
          new ShapeComponent(
               new List<ShapeComponentConstraint>()
               {
                    ShapeComponentConstraint.Create_SurfaceHeight_Between(0.2f, 0.6f),
                    ShapeComponentConstraint.Create_SurfaceCount_Min(1),
                    ShapeComponentConstraint.Create_SurfaceArea_Min(0.035f),
               }),
     };
     AddShape("Sittable", shapeComponents);
```

Chaque requête de forme est définie par un ensemble de composants de forme, chacun avec un ensemble de contraintes de composant et un ensemble de contraintes de forme qui répertorie les dépendances entre les composants. Cet exemple inclut trois contraintes dans une définition de composant unique et aucune contrainte de forme entre les composants (étant donné qu’il n’y a qu’un seul composant).

En revanche, la forme de canapé a deux composants de forme et quatre contraintes de forme. Notez que les composants sont identifiés par leur index dans la liste des composants de l’utilisateur (0 et 1 dans cet exemple).




```
shapeConstraints = new List<ShapeConstraint>()
        {
              ShapeConstraint.Create_RectanglesSameLength(0, 1, 0.6f),
              ShapeConstraint.Create_RectanglesParallel(0, 1),
              ShapeConstraint.Create_RectanglesAligned(0, 1, 0.3f),
              ShapeConstraint.Create_AtBackOf(1, 0),
        };
```

Les fonctions wrapper sont fournies dans le module Unity pour faciliter la création de définitions de formes personnalisées. La liste complète des contraintes de composant et de forme se trouve dans **SpatialUnderstandingDll.cs** dans les structures **ShapeComponentConstraint** et **ShapeConstraint** .

![Le rectangle bleu met en surbrillance les résultats de la requête de forme de chaise.](images/chair-shape-query-500px.png)

Le rectangle bleu met en surbrillance les résultats de la requête de forme de chaise.



### <a name="object-placement-solver"></a>Solveur de positionnement des objets

Les requêtes de placement d’objet peuvent être utilisées pour identifier les emplacements idéaux dans la salle physique pour placer vos objets. Le solveur trouvera l’emplacement le mieux adapté en fonction des contraintes et règles d’objet. En outre, les requêtes d’objet sont conservées jusqu’à ce que l’objet soit supprimé avec des appels **Solver_RemoveObject** ou **Solver_RemoveAllObjects** , ce qui permet le placement de plusieurs objets avec restriction.

Les requêtes de placement d’objet se composent de trois parties : le type de placement avec des paramètres, une liste de règles et une liste de contraintes. Pour exécuter une requête, utilisez l’API suivante :




```
public static int Solver_PlaceObject(
                [In] string objectName,
                [In] IntPtr placementDefinition,    // ObjectPlacementDefinition
                [In] int placementRuleCount,
                [In] IntPtr placementRules,         // ObjectPlacementRule
                [In] int constraintCount,
                [In] IntPtr placementConstraints,   // ObjectPlacementConstraint
                [Out] IntPtr placementResult)
```
Cette fonction accepte un nom d’objet, une définition de placement et une liste de règles et de contraintes. Les C# wrappers fournissent des fonctions d’assistance de construction pour faciliter la création de règles et de contraintes. La définition de placement contient le type de requête, à savoir l’un des éléments suivants :




```
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

Chacun des types de placement a un ensemble de paramètres propre au type. La structure **ObjectPlacementDefinition** contient un jeu de fonctions d’assistance statiques pour la création de ces définitions. Par exemple, pour trouver un endroit où placer un objet sur l’étage, vous pouvez utiliser la fonction suivante : 


```
public static ObjectPlacementDefinition Create_OnFloor(Vector3 halfDims)
```

Outre le type de placement, vous pouvez fournir un ensemble de règles et de contraintes. Les règles ne peuvent pas être violées. Les emplacements d’emplacement possibles qui satisfont au type et aux règles sont ensuite optimisés par rapport au jeu de contraintes pour sélectionner l’emplacement de positionnement optimal. Chacune des règles et contraintes peut être créée par les fonctions de création statique fournies. Vous trouverez ci-dessous un exemple de fonction de construction de règle et de contrainte.




```
public static ObjectPlacementRule Create_AwayFromPosition(
                    Vector3 position, float minDistance)
               public static ObjectPlacementConstraint Create_NearPoint(
                    Vector3 position, float minDistance = 0.0f, float maxDistance = 0.0f)
```

La requête de placement d’objet ci-dessous recherche un endroit où placer un cube demi-mètre sur le bord d’une surface, à l’écart des autres objets placés précédemment et près du centre de la pièce.




```
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

En cas de réussite, une structure **ObjectPlacementResult** contenant la position, les dimensions et l’orientation de placement est retournée. En outre, le placement est ajouté à la liste interne des objets placés de la DLL. Les requêtes d’emplacement suivantes prennent en compte cet objet. Le fichier **LevelSolver.cs** dans l’exemple Unity contient plus d’exemples de requêtes.

![Les zones bleues affichent le résultat de trois emplacements sur les requêtes d’étage avec les règles « éloigner de la position de la caméra ».](images/away-from-camera-position-500px.png)

Les zones bleues affichent le résultat de trois emplacements sur les requêtes d’étage avec les règles « éloigner de la position de la caméra ».


**Conseil**
* Lors de la résolution de l’emplacement de positionnement de plusieurs objets requis pour un scénario de niveau ou d’application, résolvez tout d’abord les objets indispensables et volumineux pour maximiser la probabilité qu’un espace soit trouvé.
* L’ordre de placement est important. Si vous ne trouvez pas de placement d’objet, essayez des configurations moins restreintes. Avoir un ensemble de configurations de secours est essentiel à la prise en charge des fonctionnalités dans de nombreuses configurations de salles.

### <a name="ray-casting"></a>Conversion de rayon

En plus des trois requêtes principales, une interface de type Ray peut être utilisée pour récupérer des types de surfaces avec balises et un maillage PlaySpace étanche personnalisé peut être copié après la numérisation et la finalisation de la salle, et les étiquettes sont générées en interne pour les surfaces comme plancher, plafond et murs. La fonction **PlayspaceRaycast** prend un rayon et retourne si le rayon entre en conflit avec une surface connue et, le cas échéant, des informations sur cette surface sous la forme d’un **RaycastResult**. 


```
struct RaycastResult
     {
          enum SurfaceTypes
          {
               Invalid, // No intersection
               Other,
               Floor,
               FloorLike,         // Not part of the floor topology, 
                                  //     but close to the floor and looks like the floor
               Platform,          // Horizontal platform between the ground and 
                                  //     the ceiling
               Ceiling,
               WallExternal,
               WallLike,          // Not part of the external wall surface, 
                                  //     but vertical surface that looks like a 
                                  //    wall structure
               };
               SurfaceTypes SurfaceType;
               float SurfaceArea;   // Zero if unknown 
                                        //  (i.e. if not part of the topology analysis)
               DirectX::XMFLOAT3 IntersectPoint;
               DirectX::XMFLOAT3 IntersectNormal;
     };
```

En interne, raycast est calculé par rapport à la représentation voxel 8cm cube calculée du PlaySpace. Chaque voxel contient un ensemble d’éléments surface avec des données de topologie traitées (également appelées surfels). Le surfels contenu dans la cellule voxel intersectée est comparé et la meilleure correspondance est utilisée pour rechercher les informations de topologie. Ces données de topologie contiennent l’étiquetage renvoyé sous la forme de l’énumération **SurfaceTypes** , ainsi que la surface d’exposition de la surface intersectée.

Dans l’exemple Unity, le curseur convertit chaque image de rayon. Tout d’abord, contre les conflits avec Unity ; Deuxièmement, par rapport à la représentation mondiale du module de présentation ; Enfin, sur les éléments d’interface utilisateur. Dans cette application, l’interface utilisateur est prioritaire, puis le résultat de la compréhension et enfin, les conflits avec Unity. Le **SurfaceType** est signalé en tant que texte en regard du curseur.

![Raycast intersection de rapports de résultats avec le plancher.](images/raycast-result-500px.jpg)

Raycast intersection de rapports de résultats avec le plancher.


## <a name="get-the-code"></a>Obtenir le code

Le code open source est disponible dans [MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity). Faites-le nous savoir sur les [forums de développement HoloLens](https://forums.hololens.com/) si vous utilisez le code dans un projet. Nous ne pouvons pas attendre pour voir ce que vous faites avec !

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border:0;width:800px">
<tr>
<td style="border:0"> <img alt="Jeff Evertt, Software Engineering Lead at Microsoft" width="200" height="205" src="images/jeff-evertt-200px.jpg" /></td><td style="border:0"> <b>Jeff Evertt</b> est responsable de l’ingénierie logicielle qui a travaillé sur HoloLens depuis les premiers jours, depuis l’incubation jusqu’au développement de l’expérience. Avant HoloLens, il travaillait sur la Xbox Kinect et dans le secteur des jeux sur un large éventail de plates-formes et de jeux. Jeff est passionné par la robotique, les graphiques et les choses avec des lumières éclairées. Il aime découvrir de nouveaux éléments et travailler sur des logiciels, du matériel, et en particulier dans l’espace où les deux se croisent.</td>
</tr>
</table>



## <a name="see-also"></a>Articles associés
* [Mappage spatial](spatial-mapping.md)
* [Compréhension des scènes](scene-understanding.md)
* [Visualisation du balayage d’une pièce](room-scan-visualization.md)
* [MixedRealityToolkit-Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity)
* [Asobo Studio : leçons de la Frontline du développement HoloLens](https://www.gamesindustry.biz/articles/2016-05-12-asobo-lessons-from-the-frontline-of-ar-development)
