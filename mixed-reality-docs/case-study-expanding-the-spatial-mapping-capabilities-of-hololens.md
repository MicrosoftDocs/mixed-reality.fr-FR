---
title: Étude de cas - développer les capacités de mappage spatial d’HoloLens
description: Lors de la création de nos premières applications pour Microsoft HoloLens, nous avons impatients de voir simplement l’amplitude, nous risquons les limites du mappage spatial sur l’appareil.
author: jevertt
ms.author: jevertt
ms.date: 03/21/2018
ms.topic: article
keywords: Mappage spatial Windows Mixed Reality, HoloLens,
ms.openlocfilehash: 602b629afa5900ff34c28b3a3a32725af06590b7
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595753"
---
# <a name="case-study---expanding-the-spatial-mapping-capabilities-of-hololens"></a>Étude de cas - développer les capacités de mappage spatial d’HoloLens

Lors de la création de nos premières applications pour Microsoft HoloLens, nous avons impatients de voir simplement l’amplitude, nous risquons les limites du mappage spatial sur l’appareil. Jeff Evertt, ingénieur logiciel chez Microsoft Studios, explique comment une nouvelle technologie a été développée en dehors de la nécessité de mieux contrôler comment les hologrammes sont placés dans un environnement d’utilisateur réel.

## <a name="watch-the-video"></a>Regardez la vidéo

>[!VIDEO https://www.youtube.com/embed/iUmTi3_Ynus]

## <a name="beyond-spatial-mapping"></a>Au-delà de mappage spatial

Bien que nous travaillions sur [Fragments](https://www.microsoft.com/p/fragments/9nblggh5ggm8) et [Young pétarade](https://www.microsoft.com/p/young-conker/9nblggh5ggk1), deux des premiers jeux pour HoloLens, nous avons constaté que lorsque nous faisions placement procédurale de hologrammes dans le monde physique, nous avions besoin d’un niveau plus élevé des connaissances sur l’environnement utilisateur. Chaque jeu avait ses propres besoins placement spécifique : Dans les Fragments, par exemple, nous souhaitons pouvoir faire la distinction entre les différentes surfaces, telles que la valeur plancher ou une table, pour placer des indices dans des endroits pertinents. Nous souhaitons également être en mesure d’identifier les surfaces qui caractères HOLOGRAPHIQUE taille réelle pourraient se trouvent, par exemple un canapé ou chaise. Dans pétarade Young, nous voulions pétarade et ses adversaires pour être en mesure d’utiliser des surfaces déclenchés dans la salle d’un joueur en tant que plateformes.

[Asobo Studios](http://www.asobostudio.com/index.html), notre partenaire de développement pour ces jeux, fait face à ce problème front et créé une technologie qui étend les fonctionnalités de mappage spatial de HoloLens. À l’aide de cela, nous pouvons analyser l’espace d’un joueur et identifier les surfaces, murs, tables, chaises et étages. Nous avons reçu également la possibilité d’optimiser par rapport à un ensemble de contraintes pour déterminer le meilleur placement pour les objets HOLOGRAPHIQUE.

## <a name="the-spatial-understanding-code"></a>Le code de présentation spatial

Nous a pris le code d’origine du Asobo et créé une bibliothèque qui encapsule cette technologie. Microsoft et Asobo ont maintenant ce code open source et qu’il est disponible sur [MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialMapping) que vous pouvez utiliser dans vos propres projets. Tout le code source est inclus, ce qui vous permet de le personnaliser selon vos besoins et partager vos améliorations avec la Communauté. Le code pour le C++ Solveur a été encapsulé dans une DLL UWP et exposé à Unity avec un [préfabriqué de dernière minute contenue dans MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/SpatialUnderstanding).

Il existe de nombreuses requêtes utiles inclus dans l’exemple Unity qui vous permet de rechercher des espaces vides sur les murs, placer des objets sur le plafond ou sur les espaces de grande taille sur le sol, identifier les endroits pour les caractères dans cet état et une myriade d’autres requêtes spatiales compréhension.

Alors que la solution de mappage spatial fournie par HoloLens est conçue pour être suffisamment générique pour répondre aux besoins de toute la gamme des espaces de problème, le module de présentation spatial a été créé pour prendre en charge les besoins de deux jeux spécifiques. Par conséquent, sa solution est structurée autour d’un processus spécifique et des hypothèses :
* **Correction de taille playspace**: L’utilisateur spécifie la taille maximale playspace dans l’appel d’init.
* **Le processus d’analyse à usage unique**: Le processus nécessite un discrètes phase où l’utilisateur parcourt autour d’analyse, en définissant le playspace. Fonctions de requête ne fonctionnera pas tant qu’une fois l’analyse a été finalisé.
* **Utilisateur driven playspace « peinture »**: Pendant la phase d’analyse, l’utilisateur déplace et recherche autour de la playspace, peinture efficacement les zones qui doivent être incluses. Le maillage généré est important de fournir des commentaires des utilisateurs durant cette phase.
* **À l’intérieur le programme d’installation de votre domicile ou office**: Les fonctions de requête sont conçues autour des surfaces plats et des murs à angle droit. Il s’agit d’une limitation logicielle. Toutefois, pendant la phase d’analyse, une analyse de l’axe principal est prévue pour optimiser le pavage de maille le long de l’axe principal et secondaire.

### <a name="room-scanning-process"></a>Processus d’analyse salle

Lorsque vous chargez le module de présentation spatiales, la première chose que vous effectuerez est analyse votre espace, par conséquent, toutes les surfaces utilisables, telles que le plancher, plafond et murs, sont identifiés et étiquetés. Pendant le processus d’analyse, vous cherchez votre salle et « paint » les domaines qui doivent être inclus dans l’analyse.

Le maillage observé pendant cette phase est une composante importante de retour visuel qui permet aux utilisateurs de savoir quelles parties de la salle de conversation sont en cours d’analyse. La DLL pour le module de présentation spatial stocke en interne la playspace sous forme de grille des cubes de voxel 8cm en taille réelle. Au cours de la partie initiale d’analyse, une analyse du composant principal est terminée pour déterminer les axes de la salle. En interne, elle stocke son espace voxel alignée sur ces axes. Une maille est générée environ toutes les secondes en extrayant l’isosurface le volume voxel.

![Spatiales mappage maille en blanc et présentation playspace maillage en vert](images/spatial-mapping-500px.png)

Spatiales mappage maille en blanc et présentation playspace maillage en vert



Le fichier SpatialUnderstanding.cs inclus gère le processus phase d’analyse. Il appelle les fonctions suivantes :
* **SpatialUnderstanding_Init**: Appelée une fois au début.
* **GeneratePlayspace_InitScan**: Indique que la phase d’analyse doit commencer.
* **GeneratePlayspace_UpdateScan_DynamicScan**: Appelé pour chaque trame pour mettre à jour le processus d’analyse. La position de la caméra et l’orientation est transmise et est utilisé pour le processus de peinture playspace décrit ci-dessus.
* **GeneratePlayspace_RequestFinish**: Appelé pour finaliser le playspace. Utiliser les zones « peints » pendant la phase d’analyse pour définir et verrouiller le playspace. L’application peut interroger les statistiques pendant la phase d’analyse, ainsi qu’une requête la maille personnalisée pour fournir des commentaires des utilisateurs.
* **Import_UnderstandingMesh**: Lors de l’analyse, le **SpatialUnderstandingCustomMesh** comportement fourni par le module et placé sur le préfabriqué compréhension interroge régulièrement le maillage personnalisé généré par le processus. En outre, cela une fois de plus après que l’analyse a été finalisée.

Le flux analyse, piloté par le **SpatialUnderstanding** comportement appels **InitScan**, puis **UpdateScan** chaque frame. Lorsque la requête de statistiques signale la couverture du raisonnable, l’utilisateur peut airtap pour appeler **RequestFinish** pour indiquer la fin de la phase d’analyse. **UpdateScan** continue à être appelée jusqu'à ce qu’il s’agit de retour la valeur indique que la DLL a terminé le traitement.

## <a name="the-queries"></a>Les requêtes

Une fois que l’analyse est terminée, vous serez en mesure d’accéder aux trois différents types de requêtes dans l’interface :
* **Requêtes de topologie**: Il s’agit des requêtes rapides qui reposent sur la topologie de la salle de conversation analysé.
* **Mettre en forme des requêtes**: Ils utilisent les résultats de vos requêtes de topologie pour rechercher des surfaces horizontales qui sont une bonne correspondance avec des formes personnalisées que vous définissez.
* **Requêtes de sélection élective de l’objet**: Il s’agit des requêtes plus complexes qui trouver l’emplacement ajusté selon un ensemble de règles et des contraintes pour l’objet.

Outre les trois requêtes principales, il existe une interface raycasting qui peut être utilisée pour récupérer les types de surface avec balises et une maille de salle étanches personnalisé peut être copiée.

### <a name="topology-queries"></a>Requêtes de topologie

Dans la DLL, le Gestionnaire de topologie gère l’étiquetage de l’environnement. Comme mentionné ci-dessus, les données sont stockées dans surfels, qui sont contenus dans un volume voxel. En outre, le **PlaySpaceInfos** structure est utilisée pour stocker des informations sur le playspace, y compris l’alignement du monde (plus de détails ci-dessous), floor et au plafond.

Heuristique utilisée pour déterminer les murs floor et ceiling. Par exemple, la surface plus grande et plus basses horizontale avec plus de 1 la surface d’exposition m2 est considéré comme le plancher. Notez que le chemin d’accès de l’appareil photo pendant le processus d’analyse est également utilisé dans ce processus.

Un sous-ensemble de requêtes exposées par le Gestionnaire de la topologie sont exposés via la DLL. Les requêtes de topologie exposés sont les suivantes :
* QueryTopology_FindPositionsOnWalls
* QueryTopology_FindLargePositionsOnWalls
* QueryTopology_FindLargestWall
* QueryTopology_FindPositionsOnFloor
* QueryTopology_FindLargestPositionsOnFloor
* QueryTopology_FindPositionsSittable

Chacune des requêtes a un ensemble de paramètres, spécifiques au type de requête. Dans l’exemple suivant, l’utilisateur spécifie la hauteur minimale et la largeur du volume de votre choix, à la hauteur minimale de sélection élective au-dessus de la valeur plancher, la quantité minimale de dégagement devant le volume. Toutes les mesures sont en mètres.




```
EXTERN_C __declspec(dllexport) int QueryTopology_FindPositionsOnWalls(
          _In_ float minHeightOfWallSpace,
          _In_ float minWidthOfWallSpace,
          _In_ float minHeightAboveFloor,
          _In_ float minFacingClearance,
          _In_ int locationCount,
          _Inout_ Dll_Interface::TopologyResult* locationData)
```

Chacune de ces requêtes prend un tableau alloué au préalable de **TopologyResult** structures. Le **locationCount** paramètre spécifie la longueur du tableau passé. La valeur de retour indique le nombre d’emplacements retournés. Ce nombre n’est jamais supérieur à la passé dans **locationCount** paramètre.

Le **TopologyResult** contient la position centrale du volume retourné, la direction accessibles (par exemple, normale) et les dimensions de l’espace est trouvé.




```
struct TopologyResult
     {
          DirectX::XMFLOAT3 position;
          DirectX::XMFLOAT3 normal;
          float width;
          float length;
     };
```

Notez que dans l’exemple Unity, chacune de ces requêtes est lié à un bouton dans le panneau de l’interface utilisateur virtuel. L’exemple dur codes les paramètres pour chacune de ces requêtes à des valeurs raisonnables. Consultez *SpaceVisualizer.cs* dans l’exemple de code pour plus d’exemples.

### <a name="shape-queries"></a>Requêtes de forme

À l’intérieur de la DLL, l’Analyseur de forme (**ShapeAnalyzer_W**) utilise l’Analyseur de topologie à mettre en correspondance des formes personnalisées définies par l’utilisateur. L’exemple Unity a un ensemble prédéfini de formes qui figurent dans le menu de la requête, sous l’onglet de la forme.

Notez que l’analyse de la forme fonctionne sur les surfaces horizontales uniquement. Un canapé, par exemple, est défini par l’assise plat et haut plat de retour le canapé. La requête shape recherche deux surfaces d’une plage de taille, la hauteur et aspect spécifique, avec les deux surfaces alignée et connecté. À l’aide de la terminologie de l’API, le siège canapé et le haut de l’arrière le canapé sont shape composants et l’alignement sur les exigences sont contraintes de composant de forme.

Un exemple de requête définie dans l’exemple Unity (**ShapeDefinition.cs**), pour les objets « sittable » se présente comme suit :




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

Chaque requête shape est défini par un ensemble de composants de la forme, chacun avec un ensemble de contraintes de composant et un ensemble de contraintes de forme qui répertorie les dépendances entre les composants. Cet exemple inclut trois contraintes dans une définition de composant unique et aucune contrainte de forme entre les composants (comme il n’existe qu’un seul composant).

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

Fonctions de wrapper sont fournies dans le module Unity pour simplifier la création de définitions de formes personnalisée. Vous trouverez la liste complète des contraintes de composant et de forme dans **SpatialUnderstandingDll.cs** au sein de la **ShapeComponentConstraint** et **ShapeConstraint** structures.

![Rectangle bleu met en évidence les résultats de la requête shape chaise.](images/chair-shape-query-500px.png)

Rectangle bleu met en évidence les résultats de la requête shape chaise.



### <a name="object-placement-solver"></a>Solveur de sélection élective d’objet

Requêtes de sélection élective d’objet peuvent être utilisés pour identifier les emplacements idéale dans la salle physique pour placer vos objets. Le Solveur recherche l’emplacement ajusté, étant donné les règles de l’objet et les contraintes. En outre, les requêtes d’objet persistent jusqu'à ce que l’objet est supprimé avec **Solver_RemoveObject** ou **Solver_RemoveAllObjects** appels, ce qui contraint placement d’objets multiples.

Requêtes de sélection élective d’objet se composent de trois parties : le type d’emplacement avec les paramètres, une liste de règles et une liste de contraintes. Pour exécuter une requête, utilisez l’API suivante :




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
Cette fonction accepte un nom d’objet, définition de placement et une liste des règles et des contraintes. Le C# wrappers fournissent des fonctions d’assistance pour faciliter la construction de règle et de contrainte de construction. La définition de placement contient le type de requête, autrement dit, une des opérations suivantes :




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

Chacun des types de sélection élective a un ensemble de paramètres uniques pour le type. Le **ObjectPlacementDefinition** structure contient un ensemble de fonctions d’assistance statiques pour la création de ces définitions. Par exemple, pour rechercher un emplacement pour placer un objet sur le sol, vous pouvez utiliser la fonction suivante : 


```
public static ObjectPlacementDefinition Create_OnFloor(Vector3 halfDims)
```

Outre le type de sélection élective, vous pouvez fournir un ensemble de règles et des contraintes. Des règles ne peut pas être violées. Emplacements de positionnement possibles qui satisfont les type et les règles sont ensuite optimisés par rapport au jeu de contraintes pour sélectionner l’emplacement de placement optimal. Chacune des règles et des contraintes peut être créé par les fonctions de création statique fourni. Vous trouverez ci-dessous un exemple de fonction construction règle et de contrainte.




```
public static ObjectPlacementRule Create_AwayFromPosition(
                    Vector3 position, float minDistance)
               public static ObjectPlacementConstraint Create_NearPoint(
                    Vector3 position, float minDistance = 0.0f, float maxDistance = 0.0f)
```

La requête de sélection élective d’objet ci-dessous recherche un emplacement pour placer un cube de moitié compteur sur le bord d’une surface, autre précédemment placer des objets et près du centre de la salle.




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

En cas de réussite, une **ObjectPlacementResult** structure contenant la position de placement, de dimensions et de l’orientation est retournée. En outre, le positionnement est ajouté à la liste interne de la DLL d’objets placés. Requêtes de sélection élective ultérieures prennent cet objet en compte. Le **LevelSolver.cs** fichier dans l’exemple Unity contient plusieurs exemples de requêtes.

![Les cases bleues indiquent les résultats à partir de trois requêtes Place sur Floor avec des règles « suite à partir de la position d’une caméra ».](images/away-from-camera-position-500px.png)

Les cases bleues indiquent les résultats à partir de trois requêtes Place sur Floor avec des règles « suite à partir de la position d’une caméra ».


**Astuces :**
* Lors de la résolution pour l’emplacement du positionnement de plusieurs objets requis pour un scénario de niveau ou de l’application, tout d’abord résoudre les objets indispensables et de grande taille pour optimiser la probabilité qu’un espace peut être trouvé.
* Ordre de sélection élective est important. Si le placement de l’objet est introuvable, essayez de configurations moins limitées. Il est essentiel de prenant en charge des fonctionnalités sur de nombreuses configurations de salle de disposer d’un ensemble de configurations de secours.

### <a name="ray-casting"></a>Ray cast

Outre les trois requêtes principales, une interface de conversion de ray peut être utilisée pour récupérer des types de surface avec balises et d’une maille playspace étanches personnalisés peut être copiée out après la salle a été analysée et finalisée, étiquettes sont générés de manière interne pour les surfaces tels que le Floor, ceiling et murs. Le **PlayspaceRaycast** fonction prend un rayon et retourne si le rayon est en conflit avec une surface connue et si tel est le cas, plus d’informations sur cette surface sous la forme d’un **RaycastResult**. 


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

En interne, le raycast est calculée par rapport à la représentation sous forme de voxel calculée 8cm au cube de la playspace. Chaque voxel contient un ensemble d’éléments de surface d’exposition des données de topologie traité (également appelé surfels). Les surfels contenues dans la cellule voxel intersectées sont comparées et la meilleure correspondance est utilisée pour rechercher les informations de topologie. Les données de cette topologie contient l’étiquetage retournée sous la forme de la **SurfaceTypes** enum, ainsi que de la surface d’exposition de la surface d’intersection.

Dans l’exemple Unity, le curseur convertit un rayon chaque frame. Tout d’abord, contre colliders de d’Unity ; en second lieu, par rapport à la représentation du monde du module de présentation ; et enfin, sur les éléments d’interface utilisateur. Dans cette application, l’interface utilisateur obtient la priorité, puis le résultat de la présentation et enfin, colliders de d’Unity. Le **SurfaceType** est signalé sous forme de texte en regard du curseur.

![Résultat Raycast intersection avec la valeur plancher de création de rapports.](images/raycast-result-500px.jpg)

Résultat Raycast intersection avec la valeur plancher de création de rapports.


## <a name="get-the-code"></a>Obtenir le code

Le code open source est disponible dans [MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity). Faites-le nous savoir sur le [Forums des développeurs HoloLens](https://forums.hololens.com/) si vous utilisez le code dans un projet. Nous sommes impatients de voir ce que vous en faire !

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border:0;width:800px">
<tr>
<td style="border:0"> <img alt="Jeff Evertt, Software Engineering Lead at Microsoft" width="200" height="205" src="images/jeff-evertt-200px.jpg" /></td><td style="border:0"> <b>Jeff Evertt</b> est un prospect d’ingénierie logicielle qui a travaillé sur HoloLens depuis le début, à partir d’incubation en informatique pour expérimenter le développement. Avant de HoloLens, il a travaillé sur le Xbox Kinect et dans l’industrie de jeux sur un large éventail de plateformes et des jeux. Jeff est passionné de la robotique, des graphiques et des choses avec les voyants lumineux qui vont du signal sonore. Il aime apprendre de nouvelles choses et fonctionne sur le logiciel, matériel et en particulier dans l’espace où les deux se croisent.</td>
</tr>
</table>



## <a name="see-also"></a>Voir aussi
* [Mappage spatial](spatial-mapping.md)
* [Conception de mappage spatial](spatial-mapping-design.md)
* [Visualisation d’analyse de salle](room-scan-visualization.md)
* [MixedRealityToolkit-Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity)
* [Asobo Studio : Leçons à partir de la première ligne du développement de HoloLens](http://www.gamesindustry.biz/articles/2016-05-12-asobo-lessons-from-the-frontline-of-ar-development)
