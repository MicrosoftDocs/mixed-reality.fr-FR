---
title: Créer des modèles 3D pour une utilisation dans la page d’accueil
description: Configuration requise d’Asset et création des conseils pour les modèles 3D à utiliser dans la réalité mixte Windows accueil sur HoloLens et des casques IMMERSIFS (VR).
author: thmignon
ms.author: thmignon
ms.date: 03/21/2018
ms.topic: article
keywords: Limite de modélisation 3D, conseils, configuration requise d’asset, directives, Lanceur, Lanceur 3D, texture, le matériel, la complexité, triangles, maillage, polygones, polycount, de création de modélisation
ms.openlocfilehash: 73af40cf2915742cab612625c8243a36ee74d748
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66692283"
---
# <a name="create-3d-models-for-use-in-the-home"></a>Créer des modèles 3D pour une utilisation dans la page d’accueil

Le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs arrivent avant de lancer des applications. Vous pouvez concevoir votre application pour les casques de réalité mixte Windows tirer parti un [modèle 3D en tant qu’un lanceur d’applications](implementing-3d-app-launchers.md) et autoriser [des liens ciblés 3D doit être placé en Windows Mixed Reality accueil](implementing-3d-app-launchers.md#3d-deep-links-secondarytiles) à partir d’au sein de votre application. Cet article décrit les instructions pour créer des modèles 3D compatible avec Windows Mixed Reality domestique.

## <a name="asset-requirements-overview"></a>Vue d’ensemble des exigences de ressource
Lors de la création de modèles 3D pour la réalité mixte Windows, il existe certaines exigences que toutes les ressources doivent respecter : 
1. [Exportation](#exporting-models) -ressources doivent être remis dans le format de fichier .glb (glTF binaire)
2. [Modélisation](#modeling-guidelines) -ressources doit être inférieure à 10 triangles k, avoir pas plus de 64 nœuds et 32 submeshes par LOD
3. [Matières](#material-guidelines) - Textures ne peut pas être supérieure à 4096 x 4096 et le mappage mip plus petit doit pas être supérieur à 4 sur une dimension
4. [Animation](#animation-guidelines) -Animations ne peut pas comporter plus de 20 minutes à 30 i/s (36 000 images clés) et doit contenir < = 8192 vertex de cible de morph
5. [Optimisation](#optimizations) -ressources doivent être optimisés à l’aide de la [WindowsMRAssetConverter](https://github.com/Microsoft/glTF-Toolkit/releases). Il s’agit de **requis sur les Versions de système d’exploitation Windows < = 1709** et recommandé sur les versions de système d’exploitation Windows > = 1803

Le reste de cet article inclut une présentation détaillée de ces exigences, ainsi que des instructions supplémentaires pour s’assurer que vos modèles fonctionnent bien avec Windows Mixed Reality domestique. 

## <a name="detailed-guidance"></a>Obtenir des instructions détaillées

### <a name="exporting-models"></a>Exportation de modèles

Windows Mixed Reality accueil attend des composants 3D pour être remis à l’aide du format de fichier .glb avec des images incorporées et les données binaires. GLB est la version binaire du format glTF qui est une redevance gratuit norme ouverte pour la remise de ressources 3D gérée par le groupe Khronos. Comme glTF évolue en tant qu’industrie standard pour le contenu 3D interopérable ce sera également le support technique de Microsoft pour le format entre les applications Windows et des expériences. Si vous n’avez pas créé une ressource glTF avant que vous pouvez trouver un [liste des convertisseurs et des exportateurs pris en charge](https://github.com/KhronosGroup/glTF/blob/master/README.md#converters-and-exporters) sur la page de github du groupe de travail glTF.  

### <a name="modeling-guidelines"></a>Instructions de modélisation

Windows attend des ressources pour être généré en utilisant les instructions de modélisation suivantes pour assurer la compatibilité avec l’expérience d’accueil de réalité mixte. Lors de la modélisation dans votre programme de votre choix n’oubliez pas les recommandations et limitations suivantes :
1. L’axe à distance doit être définie à « Y ».
2. L’élément multimédia doit faire face « forward » vers l’axe Z positif.
3. Toutes les ressources doivent être générées sur le plan de masse à l’origine de la scène (0,0,0)
4. Unités de travaille doivent être définies sur les compteurs et des ressources afin que les ressources peuvent être créées à l’échelle mondiale
5. Toutes les mailles n’êtes pas obligé d’être combinés, mais il est recommandé si vous ciblez des appareils avec contraintes de ressources
6. Toutes les mailles doivent partager des documents de 1, avec seulement 1 texture définir utilisé pour la ressource entière
7. UVs doivent être disposés dans une disposition carrée dans 0-1 espace. Évitez les textures de mosaïque même si elles sont autorisées.
8. Multi-UVs ne sont pas pris en charge.
9. Matériaux verso double n’est pas pris en charge.

### <a name="triangle-counts-and-levels-of-detail-lods"></a>Nombres de triangle et niveaux de détail (degrés)

Windows Mixed Reality domestique ne prend pas en charge les modèles avec plus de 10 000 triangles. Il est recommandé d’effectuer une triangulation sur votre mailles avant l’exportation pour vous assurer qu’ils ne dépassent pas ce nombre. MR de Windows prend également en charge les niveaux de géométrie facultatif de détail (degrés) afin de garantir un performante et une expérience de qualité. [Le WindowsMRAssetConverter](https://github.com/Microsoft/glTF-Toolkit/releases) vous permettra de combiner les 3 versions de votre modèle dans un modèle .glb unique. Windows détermine quels LOD à afficher en fonction de la quantité d’espace d’écran qu'occupe le modèle. Uniquement 3 niveaux LOD sont pris en charge par le code suivant recommandé triangle nombres :
<br>

|  Niveau de texture  |  Nombre de Triangle recommandée  |  Nombre maximal de Triangle | 
|------|------|------|
|  LOD 0 |  10,000 |  10,000 | 
|  LOD 1 |  5,000  |  10,000 | 
|  LOD 2 |  2,500  |  10,000 | 

### <a name="node-counts-and-submesh-limits"></a>Nombre de nœuds et les limites de sous-maillage
Windows Mixed Reality domestique ne prend pas en charge les modèles avec plus de 64 nœuds ou 32 submeshes par LOD. Les nœuds sont un concept dans le [glTF spécification](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#nodes-and-hierarchy) qui définissent les objets dans la scène. Submeshes sont définis dans le tableau de [primitives](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#meshes) sur la maille dans l’objet. 

|  Fonctionnalité |  Description  |  Nombre maximal pris en charge | Documentation |
|------|------|------|------|
|  Nœuds |  Objets dans la scène glTF |  64 par LOD | [Ici](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#nodes-and-hierarchy)|
|  Submeshes |  Somme des primitives sur toutes les mailles |  32 par LOD | [Ici](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#meshes)|

## <a name="material-guidelines"></a>Recommandations matérielles

Textures doivent être préparés à l’aide d’un flux de travail PBR irrégularité complète. Commencez par créer un ensemble complet de textures notamment Albedo Normal, Occlusion, métalliques et irrégularité. Réalité mixte Windows prend en charge textures avec des résolutions jusqu'à 4096 x 4096 mais son recommandé auteur à 512 x 512. En outre, les textures doivent être conçus aux résolutions par multiples de 4 car il s’agit d’une exigence pour le format de compression appliqué à des textures dans les étapes d’exportation décrites ci-dessous. Enfin, lorsque les mipmaps gerating ou une texture le mip le plus bas doit être un maximum de 4 x 4.
<br>

|  Taille de Texture recommandée  |  Taille de Texture de max | Mip le plus bas
|----|----|----|
|  512x512  |  4096x4096 | 4 x 4 max|

### <a name="albedo-base-color-map"></a>Mappage de albedo (couleur de base)

Couleurs brutes sans aucune information d’éclairage. Ce mappage contient également la réflexion et diffuse des nus (blanc dans le mappage métallique) et les surfaces isolant (noir dans le mappage métallique) respectivement.

### <a name="normal"></a>Normal

Carte de normale de l’espace tangent

### <a name="roughness-map"></a>Mappage de la cassure

Décrit le microsurface de l’objet. Blanc 1.0 est approximative noir 0.0 est lisse. Ce mappage donne la ressource le plus de caractères car il décrit véritablement la surface par exemple, fait qu’effleurer empreintes digitales, tâches, grime etc.

### <a name="ambient-occlusion-map"></a>Mappage de l’occlusion ambiante

Mappage de mise à l’échelle de valeurs représentant des zones de la lumière un vaisseau qui bloque des réflexions

### <a name="metallic-map"></a>Carte métallique

Indique le nuanceur si quelque chose de métal ou non. Métal brutes = 1.0 complète Non blanc = 0,0 noir. Il peut y avoir des valeurs de gris transitoires qui indiqueront couvrant le métal brutes telles que saletés, mais en général ce mappage doit être noir et blanc uniquement.

## <a name="optimizations"></a>optimisations

Windows Mixed Reality accueil propose une série d’optimisations par-dessus les spécifications principales de glTF définis à l’aide des extensions personnalisées. Ces optimisations sont requises sur les versions de Windows < = 1709 et recommandés sur les versions plus récentes de Windows. Vous pouvez optimiser facilement n’importe quel modèle glTF 2.0 à l’aide du [mixte réalité Asset convertisseur Windows disponible sur GitHub](https://github.com/Microsoft/glTF-Toolkit/releases). Cet outil effectue la compression de texture correcte et les optimisations comme indiqué ci-dessous. Pour une utilisation générale, nous recommandons l’utilisation de la WindowsMRAssetConverter, mais si vous avez besoin de davantage de contrôle sur l’expérience et que vous souhaitez créer votre propre pipeline de l’optimisation puis vous pouvez faire référence à la spécification détaillée ci-dessous.  

### <a name="materials"></a>Matériaux

Pour améliorer les temps dans les environnements de réalité mixte Windows MR de chargement de ressource prend en charge le rendu des textures compressées DDS emballés en fonction de la texture empaquetage d’un modèle défini dans cette section. Les textures DDS sont référencés à l’aide de la [MSFT_texture_dds extension](https://github.com/sbtron/glTF/tree/MSFT_lod/extensions/Vendor/MSFT_texture_dds). La compression des textures est fortement recommandée. 

#### <a name="hololens"></a>HoloLens

Basée sur HoloLens de réalité mixte expériences attendent des textures pour être compressé à l’aide d’une installation de texture de 2 à l’aide de la spécification de compression suivantes :
<br>

|  glTF, propriété  |  Texture  |  Schéma de compression | 
|----------|----------|----------|
|  pbrMetallicRoughness  |  baseColorTexture  |  Rouge (R), vert (G), bleu (B) | 
|  [MSFT_packing_normalRoughnessMetallic](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_normalRoughnessMetallic/README.md)  |  normalRoughnessMetallicTexture  |  Normal (RG), irrégularité (B), métallique (A) | 


Lors de la compression les textures DDS la compression suivante est attendue sur chaque carte :
<br>

|  Texture  |  Compression attendue | 
|------|------|
|  baseColorTexture, normalRoughnessMetallicTexture |  BC7 | 

#### <a name="immersive-vr-headsets"></a>Casques IMMERSIFS (VR)

Basé sur les PC Windows Mixed Reality expériences utilisateur pour des casques IMMERSIFS (VR) attendre des textures pour être compressé à l’aide d’une installation de texture de 3 à l’aide de la spécification de compression suivantes :

##### <a name="windows-os--1803"></a>Windows OS >= 1803

<br>

|  glTF, propriété  |  Texture  |  Schéma de compression | 
|----------|----------|----------|
|  pbrMetallicRoughness  |  baseColorTexture  |  Rouge (R), vert (G), bleu (B) | 
|  [MSFT_packing_occlusionRoughnessMetallic](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_occlusionRoughnessMetallic/README.md)  |  occlusionRoughnessMetallicTexture  |  OCCLUSION (R), irrégularité (G), métallique (B) | 
|  [MSFT_packing_occlusionRoughnessMetallic](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_occlusionRoughnessMetallic/README.md)  |  normalTexture  |  Normal (RG) | 

Lors de la compression les textures DDS la compression suivante est attendue sur chaque carte :
<br>

|  Texture  |  Compression attendue | 
|------|------|
|  normalTexture  |  BC5 | 
|  baseColorTexture, occlusionRoughnessMetallicTexture  |  BC7 | 

##### <a name="windows-os--1709"></a>Windows OS <= 1709
<br>

|  glTF, propriété  |  Texture  |  Schéma de compression | 
|----------|----------|----------|
|  pbrMetallicRoughness  |  baseColorTexture  |  Rouge (R), vert (G), bleu (B) | 
|  [MSFT_packing_occlusionRoughnessMetallic](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_occlusionRoughnessMetallic/README.md)  |  roughnessMetallicOcclusionTexture  |  Roughness (R), Metallic (G), Occlusion (B) | 
|  [MSFT_packing_occlusionRoughnessMetallic](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_occlusionRoughnessMetallic/README.md)  |  normalTexture  |  Normal (RG) | 

Lors de la compression les textures DDS la compression suivante est attendue sur chaque carte :
<br>

|  Texture  |  Compression attendue | 
|------|------|
|  normalTexture  |  BC5 | 
|  baseColorTexture, roughnessMetallicOcclusionTexture | BC7 |

### <a name="adding-mesh-lods"></a>Ajout de maille degrés

Windows MR utilise nœud geometry degrés pour restituer les modèles 3D dans différents niveaux de détail en fonction de l’écran. Bien que cette fonctionnalité n’est pas techniquement nécessaire, il est fortement recommandé pour toutes les ressources. Windows prend en charge 3 niveaux de détail. La valeur par défaut LOD est 0, ce qui représente la qualité la plus élevée. Autres degrés sont numérotées de manière séquentielle, par exemple, 1, 2 et get progressivement plus bas dans la qualité. Le [convertisseur de ressource de réalité mixte Windows](https://github.com/Microsoft/glTF-Toolkit/releases) prend en charge la génération de ressources qui répondent à cette spécification LOD en acceptant plusieurs modèles glTF et de les fusionner en un seul élément multimédia avec des niveaux LOD valides. Le tableau suivant présente les objectifs de classement et de triangle LOD attendus :
<br>

|  Niveau de texture  |  Nombre de Triangle recommandée  |  Nombre maximal de Triangle | 
|-------|-------|-------|
|  LOD 0 |  10,000 |  10,000 | 
|  LOD 1 |  5,000  |  10,000 | 
|  LOD 2 |  2,500  |  10,000 | 

Lorsque vous utilisez toujours des degrés spécifier 3 niveaux LOD. Manquant degrés entraîne le modèle s’affichait ne pas inopinément en tant que les commutateurs de système LOD au niveau LOD manquant. glTF 2.0 ne prend pas en charge degrés dans le cadre de la spécification de base. Degrés doivent par conséquent être définis à l’aide de la [extension MSFT_LOD](https://github.com/sbtron/glTF/tree/MSFT_lod/extensions/Vendor/MSFT_lod).

### <a name="screen-coverage"></a>Couverture de l’écran

Degrés sont affichés dans la réalité mixte Windows basé sur un système piloté par la valeur de la couverture d’écran définie sur chaque LOD. Objets qui utilisent actuellement une plus grande partie de l’espace d’écran sont affichés à un niveau supérieur de la texture. Couverture de l’écran ne fait pas partie de la spécification de glTF 2.0 core et doit être spécifiée à l’aide de MSFT_ScreenCoverage dans la section « extras » de la [MSFT_lod extension](https://github.com/sbtron/glTF/tree/MSFT_lod/extensions/Vendor/MSFT_lod).
<br>

|  Niveau de texture  |  Intervalle recommandé  |  Plage par défaut | 
|-------|-------|-------|
|  LOD 0  |  100% - 50% |  .5 | 
|  LOD 1 |  Sous 50 % à 20 %  |  .2 | 
|  LOD 2 |  Sous 20 % à 1 %  |  .01 | 
|  LOD 4  |  Moins de 1 %  |  - | 

## <a name="animation-guidelines"></a>Instructions d’animation

> [!NOTE]
> Cette fonctionnalité a été ajoutée dans le cadre de [mettre à jour du 10 avril 2018 Windows](release-notes-april-2018.md). Dans les versions antérieures de Windows, ces animations ne seront pas lue, toutefois, ils seront chargera si créés selon les instructions de cet article.  

L’accueil de réalité mixte prend en charge les objets animés glTF HoloLens et des casques IMMERSIFS (VR). Si vous souhaitez déclencher des animations sur votre modèle, vous devez utiliser l’extension de carte de l’Animation sur le format glTF. Cette extension vous permet de déclencher des animations dans le modèle glTF basée sur la présence d’utilisateurs dans le monde, par exemple déclencher une animation lorsque l’utilisateur est proche de l’objet ou lors d’une consultation à elle. Si l’objet glTF vous dispose d’animations, mais ne définit pas les déclencheurs les animations ne seront pas lues. La section ci-dessous décrit un flux de travail pour l’ajout de ces déclencheurs à n’importe quel objet glTF animée.

### <a name="tools"></a>Outils
Tout d’abord, téléchargez les outils suivants si vous ne les avez pas déjà. Ces outils faciliteront ouvrir n’importe quel modèle glTF, en afficher un aperçu, modifier et enregistrer arrière en tant que glTF ou .glb :
1. [Visual Studio Code](https://code.visualstudio.com/)
2. [glTF Code Tools pour Visual Studio](https://marketplace.visualstudio.com/items?itemName=cesium.gltf-vscode)


### <a name="opening-and-previewing-the-model"></a>Ouverture et de l’aperçu du modèle
Commencez par ouvrir le modèle glTF dans VSCode en faisant glisser le fichier .glTF dans la fenêtre d’éditeur. Notez que si vous avez un .glb au lieu d’un fichier .glTF vous pouvez l’importer dans VSCode à l’aide du complément Outils glTF que vous avez téléchargé. Accédez à « Affichage -> Palette de commandes », puis commencez à taper « glTF » dans la palette de commandes et sélectionnez « glTF : Importer à partir de glb » qui s’affiche pour vous permettre d’importer un .glb avec un sélecteur de fichiers. 

Après avoir ouvert votre modèle glTF, vous devez voir le JSON dans la fenêtre d’éditeur. Notez que vous pouvez également afficher un aperçu du modèle dans une visualisation 3D en direct à l’aide de l’en cliquant avec le bouton avec le bouton droit sur le nom de fichier et en sélectionnant le « glTF : Afficher un aperçu du modèle 3D » le raccourci de commande à partir du menu contextuel. 

### <a name="adding-the-triggers"></a>L’ajout de déclencheurs
Les déclencheurs d’animations sont ajoutées au modèle de glTF JSON à l’aide de l’extension de carte de l’Animation. L’extension de carte d’animation est décrite publiquement [ici sur GitHub](https://github.com/msfeldstein/glTF/blob/04f7005206257cf97b215df5e3f469d7838c1fee/extensions/Vendor/FB_animation_map/README.md) (Remarque : IL S’AGIT UNE EXTENSION DE PROJET). Pour ajouter l’extension parchemin votre modèle simplement à la fin du fichier glTF dans l’éditeur et ajoutez le bloc « extensionsUsed » et « extensions » à votre fichier s’ils n’existent pas déjà. Dans la section « extensionsUsed », vous allez ajouter une référence à l’extension « EXT_animation_map » et dans le bloc « extensions », vous ajouterez vos mappages pour les animations dans le modèle.

Comme indiqué [dans les spécifications de](https://github.com/msfeldstein/glTF/blob/04f7005206257cf97b215df5e3f469d7838c1fee/extensions/Vendor/FB_animation_map/README.md) vous définissez ce qui déclenche l’animation à l’aide de la chaîne « sémantique » sur la liste des « animations » qui est un tableau d’index de l’animation. Dans l’exemple ci-dessous, nous avons défini l’animation pendant que l’utilisateur est gazing à l’objet :

```json
  "extensionsUsed": [
    "EXT_animation_map"
  ],
  "extensions" : {
      "EXT_animation_map" : {
            "bindings": [
                {
                    "semantic": "GAZE",
                    "animations": [0]
                }
            ]
      }
  }
```
La sémantique de déclencheurs d’animation suivants est pris en charge par Windows Mixed Reality domestique.  
* « TOUJOURS » : Boucle en permanence une animation
* "HELD": Un objet en boucle pendant toute la durée est saisi.
* « UTILISATION » : En boucle pendant que l’objet est examiné
* « PROXIMITÉ » : En boucle pendant une visionneuse se trouve à proximité un objet
* « POINTANT » : En boucle pendant que l’utilisateur pointe vers un objet

### <a name="saving-and-exporting"></a>Enregistrement et exportation
Une fois que vous avez apporté les modifications à votre modèle glTF vous pouvez l’enregistrer directement en tant que glTF ou avec le bouton droit sur le nom du fichier dans l’éditeur, puis sélectionnez « glTF : Exporter vers GLB (fichier binaire) » à la place exporter un .glb. 

### <a name="restrictions"></a>Restrictions
Animations ne peut pas comporter plues de 20 minutes et ne peut pas contenir plus de 36 000 images clés (20 minutes à 30 i/s). En outre lors de l’utilisation de cible de morph en animations ne dépassent pas vertex de cible morph 8192 ou moins. Dépassement ces être évités sera de nombre de la ressource animée afin d’être prises en charge dans la page d’accueil Windows Mixed Reality. 

|Fonctionnalité|Durée maximum|
|-----|-----|
|Durée|20 minutes|
|Images clés|36,000| 
|Morph cible vertex|8 192|

## <a name="gltf-implementation-notes"></a>Remarques sur l’implémentation glTF
MR de Windows ne prend pas en charge retournement geometry à l’aide des échelles négatif. Géométrie avec échelles négatif provoquera probablement artefacts visuels.

L’élément multimédia glTF doit pointer vers la scène par défaut à l’aide de l’attribut de scène doit être restitué par Windows MR. En outre le chargeur Windows RM glTF antérieures à la [mettre à jour du 10 avril 2018 Windows](release-notes-april-2018.md) **requiert** accesseurs :
* Doit avoir les valeurs minimale et maximale.
* Type scalaire doit être componentType UNSIGNED_SHORT (5123) ou UNSIGNED_INT (5125).
* Type VEC2 et VEC3 doivent être componentType FLOAT (5126).

Les propriétés matérielles suivantes sont utilisées à partir de spécifications principales de glTF 2.0, mais pas obligatoires :
* baseColorFactor, metallicFactor, roughnessFactor
* baseColorTexture : Doit pointer vers une texture stockée dans dds.
* emissiveTexture : Doit pointer vers une texture stockée dans dds.
* emissiveFactor
* alphaMode

Les propriétés de matériau suivantes sont ignorées à partir de spécifications principales :
* Tous les Multi-UVs
* metalRoughnessTexture : Doit utiliser à la place de compression de texture Microsoft optimisé définie ci-dessous
* normalTexture : Doit utiliser à la place de compression de texture Microsoft optimisé définie ci-dessous
* normalScale
* occlusionTexture : Doit utiliser à la place de compression de texture Microsoft optimisé définie ci-dessous
* occlusionStrength

MR de Windows ne prend pas en charge les points et les lignes mode primitif. 

Qu’un seul attribut de vertex de UV est pris en charge.

## <a name="additional-resources"></a>Ressources supplémentaires
* [glTF exportateurs et des convertisseurs](https://github.com/KhronosGroup/glTF#converters-and-exporters)
* [glTF Toolkit](https://github.com/Microsoft/glTF-Toolkit)
* [glTF 2.0 spécification](https://github.com/KhronosGroup/glTF/blob/master/README.md)
* [Microsoft glTF LOD spécification d’Extension](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_lod/README.md)
* [PC mixte réalité la spécification d’Extensions de l’emballage Texture](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_occlusionRoughnessMetallic/README.md)
* [HoloLens mixte réalité la spécification d’Extensions de l’emballage Texture](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_normalRoughnessMetallic/README.md)
* [Spécification des extensions Microsoft DDS Textures glTF](https://github.com/KhronosGroup/glTF/tree/master/extensions/2.0/Vendor/MSFT_texture_dds)

## <a name="see-also"></a>Voir aussi

* [Implémenter des lanceurs d’applications 3D (applications UWP)](implementing-3d-app-launchers.md)
* [Implémenter des lanceurs d’applications 3D (applications Win32)](implementing-3d-app-launchers-win32.md)
* [Exploration de la page d’accueil Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md)
