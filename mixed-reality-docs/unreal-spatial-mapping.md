---
title: Mappage spatial dans Unreal
description: Guide d’utilisation du mappage spatial dans Unreal
author: sw5813
ms.author: jacksonf
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, mappage spatial
ms.openlocfilehash: 32f8247010745b23bf73c5161c378bc1284169ef
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82840078"
---
# <a name="spatial-mapping-in-unreal"></a>Mappage spatial dans Unreal

Pour activer le mappage spatial sur HoloLens, vérifiez que la fonctionnalité « Spatial Perception » est cochée dans l’éditeur Unreal sous Project Settings > Platform > HoloLens > Capabilities.  

Pour activer l’utilisation du mappage spatial dans un jeu HoloLens, activez « Generate Mesh Data from Tracked Geometry » dans ARSessionConfig.  Le plug-in HoloLens pourra alors obtenir de manière asynchrone les données de mappage spatial et les exposer à Unreal par le biais du composant MRMesh. 

![Magasin d’ancres spatiales prêt](images/unreal-spatialmapping-arsettings.PNG)

Pour avoir une visualisation de débogage du maillage de mappage spatial, cochez « Render Mesh Data in Wireframe » dans ARSessionConfig. Vous verrez ainsi une maquette (ou wireframe) blanche autour de chaque triangle dans le composant MRMesh. 

Dans Project Settings > Platform > HoloLens > Spatial Mapping, les paramètres suivants peuvent être modifiés pour changer le comportement d’exécution du mappage spatial : 

![Paramètres projet des ancres spatiales](images/unreal-spatialmapping-projectsettings.PNG)

Le paramètre « Max Triangles Per Cubic Meter » modifie la densité des triangles dans le maillage de mappage spatial.  Le paramètre « Spatial Meshing Volume Size » définit la taille du cube autour du joueur utilisé pour le rendu et la mise à jour des données de mappage spatial.  Si l’environnement d’exécution de l’application est supposé être grand, cette zone devra être suffisamment grande pour s’adapter à l’espace réel.  À l’inverse, si l’application doit uniquement placer des hologrammes sur des surfaces proches de l’utilisateur, cette zone pourra être plus petite.  Le volume de mappage spatial bougera en même temps que l’utilisateur se déplacera dans le monde. 

Pour pouvoir accéder au composant MRMesh pendant l’exécution, ajoutez d’abord un composant ARTrackableNotify à un acteur Blueprint : 

![Composant ARTrackableNotify pour les ancres spatiales](images/unreal-spatialmapping-artrackablenotify.PNG)

Ensuite, accédez aux détails du composant et cliquez sur le bouton « + » vert dans les événements à surveiller. 

![Événements d’ancres spatiales](images/unreal-spatialmapping-events.PNG)

Ici, nous surveillons l’événement On Add Tracked Geometry pour rechercher des maillages universels valides qui correspondent aux données de mappage spatial, puis nous changeons le matériau du maillage : 

![Exemple d’ancres spatiales](images/unreal-spatialmapping-example.PNG)

Dans C++, nous pouvons nous abonner au délégué OnTrackableAdded pour obtenir ARTrackedGeometry dès qu’il est disponible.  Il existe des délégués similaires pour les événements de mise à jour et de suppression : AddOnTrackableUpdatedDelegate_Handle et AddOnTrackableRemovedDelegate_Handle. 

![Exemple de code C++ pour les ancres spatiales](images/unreal-spatialmapping-examplecode.PNG)

Dans le fichier build.cs du projet, « AugmentedReality » doit figurer dans la liste PublicDependencyModuleNames pour inclure « ARBlueprintLibrary.h » et « MRMesh » afin d’inspecter le composant MRMesh du UARTrackedGeometry. 

Le mappage spatial n’est pas le seul type de données exposées à travers ARTrackedGeometries. Nous devons donc vérifier que EARObjectClassification est défini sur World, ce qui indique qu’il s’agit d’une géométrie de mappage spatial. 

## <a name="see-also"></a>Voir aussi
* [Mappage spatial](spatial-mapping.md)
