---
title: Mappage spatial dans Unreal
description: Guide d’utilisation du mappage spatial dans Unreal
author: hferrone
ms.author: v-haferr
ms.date: 06/10/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, mappage spatial
ms.openlocfilehash: ffa57749cd96e240ac4812f950f4e13a6dbc68bd
ms.sourcegitcommit: 45da0a056fa42088ff81ccdd11232830fbe8430f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84720405"
---
# <a name="spatial-mapping-in-unreal"></a>Mappage spatial dans Unreal

## <a name="overview"></a>Vue d’ensemble
Le mappage spatial permet de placer des objets sur des surfaces du monde physique en montrant l’environnement autour d’HoloLens, ce qui fait paraître les hologrammes encore plus réels à l’utilisateur. Le mappage spatial ancre également les objets dans le monde de l’utilisateur en tirant parti des indications de profondeur du monde réel. De cette façon, l’utilisateur a réellement l’impression que ces hologrammes se trouvent autour de lui. Les hologrammes qui flottent dans les airs ou qui se déplacent en même temps que l’utilisateur ne sembleront pas aussi réels. Il est conseillé d’ajouter des éléments à des fins de confort dès que cela vous est possible.

Vous trouverez plus d’informations sur la qualité du mappage spatial, le positionnement, l’occlusion, le rendu et plus encore, dans le document [Mappage spatial](spatial-mapping.md).

## <a name="enabling-spatial-mapping"></a>Activation du mappage spatial

Pour activer le mappage spatial sur HoloLens :
- Ouvrez **Edit > Project Settings** , puis faites défiler jusqu’à la section **Platforms**.    
    + Sélectionnez **HoloLens**, puis cochez **Spatial Perception**.

Pour choisir le mappage spatial et déboguer **MRMesh** dans un jeu HoloLens :
1. Ouvrez **ARSessionConfig**, puis développez la section **ARSettings > World Mapping**. 

2. Cochez **Generate Mesh Data from Tracked Geometry** (Générer les données de maillage à partir de la géométrie suivie), ce qui indique au plug-in HoloLens qu’il doit démarrer de manière asynchrone la récupération des données de mappage spatial et les afficher dans Unreal via **MRMesh**. 
3. Cochez **Render Mesh Data in Wireframe** (Afficher les données de maillage dans un contour filaire) pour afficher un contour filaire blanc autour de chaque triangle dans **MRMesh**. 

![Magasin d’ancres spatiales prêt](images/unreal-spatialmapping-arsettings.PNG)


## <a name="spatial-mapping-at-runtime"></a>Mappage spatial au moment de l’exécution
Vous pouvez modifier les paramètres suivants pour mettre à jour le comportement du runtime de mappage spatial :

- Ouvrez **Edit > Project Settings**, faites défiler jusqu’à la section **Platforms**, puis sélectionnez **HoloLens > Spatial Mapping** : 

![Paramètres projet des ancres spatiales](images/unreal-spatialmapping-projectsettings.PNG)

- Le paramètre **Max Triangles Per Cubic Meter** (Nombre maximal de triangles par mètre cube) modifie la densité des triangles dans le maillage de mappage spatial.  
- Le paramètre **Spatial Meshing Volume Size** (Volume du maillage spatial) définit la taille du cube autour du joueur utilisé pour le rendu et la mise à jour des données de mappage spatial.  
    + Si l’environnement d’exécution de l’application est supposé être grand, cette valeur devra être suffisamment grande pour s’adapter à l’espace réel.  À l’inverse, si l’application doit uniquement placer des hologrammes sur des surfaces proches de l’utilisateur, cette valeur pourra être plus petite. Le volume de mappage spatial bougera en même temps que l’utilisateur se déplacera dans le monde. 

## <a name="working-with-mrmesh"></a>Utilisation de MRMesh
Pour accéder à **MRMesh** au moment de l’exécution :
1. Ajoutez un composant **ARTrackableNotify** à l’acteur Blueprint. 

![Composant ARTrackableNotify pour les ancres spatiales](images/unreal-spatialmapping-artrackablenotify.PNG)

2. Sélectionnez le composant **ARTrackableNotify**, puis développez la section **Events** (Événements) dans le panneau **Details**. 
    - Cliquez sur le bouton **+** pour les événements que vous souhaitez superviser. 

![Événements d’ancres spatiales](images/unreal-spatialmapping-events.PNG)

Dans ce cas, l’événement **On Add Tracked Geometry** (Lors de l’ajout d’une géométrie suivie) est supervisé. Celui-ci recherche les maillages valides de l’environnement qui correspondent aux données de mappage spatial. Vous trouverez la liste complète des événements dans l’API du composant [UARTrackableNotify](https://docs.unrealengine.com/API/Runtime/AugmentedReality/UARTrackableNotifyComponent/index.html). 

Vous pouvez changer le matériau du maillage dans le graphe d’événements Blueprint ou dans le code C++. La capture d’écran ci-dessous montre la route du blueprint : 

![Exemple d’ancres spatiales](images/unreal-spatialmapping-example.PNG)

Dans le code C++, vous pouvez vous abonner au délégué `OnTrackableAdded` pour récupérer `ARTrackedGeometry` dès qu’il est disponible, comme indiqué dans le code ci-dessous. 

> [!IMPORTANT]
> Le fichier build.cs du projet **DOIT INCLURE** **AugmentedReality** dans la liste **PublicDependencyModuleNames**.
> - Cela inclut **ARBlueprintLibrary.h** et **MRMeshComponent.h**, ce qui vous permet d’examiner le composant **MRMesh** de **UARTrackedGeometry**. 

![Exemple de code C++ pour les ancres spatiales](images/unreal-spatialmapping-examplecode.PNG)

Le mappage spatial n’est pas le seul type de données qui est affiché à travers **ARTrackedGeometries**. Vous pouvez vérifier que `EARObjectClassification` est `World`, ce qui signifie qu’il s’agit d’une géométrie de mappage spatial. 

Il existe des délégués similaires pour les événements de mise à jour et de suppression : 
- `AddOnTrackableUpdatedDelegate_Handle` 
- `AddOnTrackableRemovedDelegate_Handle`. 

Vous trouverez la liste complète des événements dans l’API [UARTrackedGeometry](https://docs.unrealengine.com/API/Runtime/AugmentedReality/UARTrackedGeometry/index.html).

## <a name="see-also"></a>Voir aussi
* [Mappage spatial](spatial-mapping.md)
