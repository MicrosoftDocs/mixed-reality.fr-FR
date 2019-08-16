---
title: Créer des modèles 3D à utiliser dans la page d’hébergement
description: Exigences relatives aux ressources et aide à la création de modèles 3D à utiliser dans la famille Windows Mixed Reality sur les casques HoloLens et immersif (VR).
author: thmignon
ms.author: thmignon
ms.date: 03/21/2018
ms.topic: article
keywords: 3D, modélisation, Guide de modélisation, besoins en ressources, instructions de création, lanceur, lanceur 3D, texture, matériaux, complexité, triangles, maillage, polygones, polynombre, limites
ms.openlocfilehash: 73af40cf2915742cab612625c8243a36ee74d748
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66692283"
---
# <a name="create-3d-models-for-use-in-the-home"></a>Créer des modèles 3D à utiliser dans la page d’hébergement

La [base de la réalité Windows Mixed](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs se trouvent avant de lancer des applications. Vous pouvez concevoir votre application pour les écouteurs Windows Mixed Reality pour tirer parti d’un [modèle 3D en tant que lanceur d’applications](implementing-3d-app-launchers.md) et permettre [la mise en place de liens en profondeur en 3D dans le Windows Mixed Reality à l'](implementing-3d-app-launchers.md#3d-deep-links-secondarytiles) intérieur de votre application. Cet article décrit les instructions de création de modèles 3D compatibles avec la page d’hébergement de la réalité mixte Windows.

## <a name="asset-requirements-overview"></a>Présentation des exigences relatives aux ressources
Lorsque vous créez des modèles 3D pour Windows Mixed Reality, toutes les ressources doivent respecter les conditions suivantes: 
1. L' [exportation](#exporting-models) des ressources doit être fournie au format de fichier. GLB (binaire glTF)
2. La [modélisation](#modeling-guidelines) des ressources doit être inférieure à 10 Ko, ne pas comporter plus de 64 nœuds et des sous-maillages 32 par LOD
3. [Matériaux](#material-guidelines) -les textures ne peuvent pas être supérieures à 4096 x 4096 et la plus petite carte MIP ne doit pas être supérieure à 4 sur l’une ou l’autre des dimensions
4. [Animation](#animation-guidelines) -les animations ne peuvent pas dépasser 20 minutes à 30 i/s (images clés 36 000) et doivent contenir < = 8192 sommets cibles Morph
5. [Optimisation](#optimizations) -les ressources doivent être optimisées à l’aide de [WindowsMRAssetConverter](https://github.com/Microsoft/glTF-Toolkit/releases). Cela est **requis sur les versions de système d’exploitation windows < = 1709** et recommandé sur les versions de système d’exploitation Windows > = 1803

Le reste de cet article comprend une présentation détaillée de ces exigences, ainsi que des instructions supplémentaires pour garantir que vos modèles fonctionnent bien avec la page d’hébergement Windows Mixed Reality. 

## <a name="detailed-guidance"></a>Conseils détaillés

### <a name="exporting-models"></a>Exportation de modèles

Windows Mixed Reality s’attend à ce que les ressources 3D soient remises à l’aide du format de fichier. GLB avec des images incorporées et des données binaires. GLB est la version binaire du format glTF, qui est une norme ouverte libre Royalty pour la remise de ressources 3D gérée par le groupe Khronos. Comme glTF évolue comme une norme industrielle pour le contenu 3D interopérable, Microsoft prend en charge le format sur les applications et les expériences Windows. Si vous n’avez pas créé de ressource glTF avant de pouvoir trouver la [liste des exportateurs et convertisseurs pris en charge](https://github.com/KhronosGroup/glTF/blob/master/README.md#converters-and-exporters) sur la page GitHub glTF Working Group.  

### <a name="modeling-guidelines"></a>Instructions de modélisation

Windows s’attend à ce que les ressources soient générées à l’aide des recommandations de modélisation suivantes pour garantir la compatibilité avec l’expérience d’origine de la réalité mixte. Lorsque vous modélisez dans votre programme de votre choix, gardez à l’esprit les recommandations et limitations suivantes:
1. L’axe vers le haut doit être défini sur «Y».
2. L’élément multimédia doit être orienté vers l’avant vers l’axe Z positif.
3. Toutes les ressources doivent être construites sur le plan de sol à l’origine de la scène (0, 0, 0)
4. Les unités de travail doivent être définies sur des compteurs et des ressources afin que les ressources puissent être créées à l’échelle mondiale
5. Il n’est pas nécessaire de combiner tous les maillages, mais il est recommandé si vous ciblez des appareils à ressources restreintes.
6. Tous les maillages doivent partager 1 matériau, avec seulement 1 jeu de textures utilisé pour l’ensemble de l’élément multimédia
7. UVs doit être disposé dans une disposition carrée de l’espace 0-1. Évitez les textures en mosaïque bien qu’elles soient autorisées.
8. Les UVs multiples ne sont pas pris en charge
9. Les matériaux à double face ne sont pas pris en charge

### <a name="triangle-counts-and-levels-of-detail-lods"></a>Nombres et niveaux de détails des triangles (LODs)

La page d’hébergement Windows Mixed Reality ne prend pas en charge les modèles avec plus de 10 000 triangles. Il est recommandé de facettiser vos mailles avant de les exporter pour vous assurer qu’elles ne dépassent pas ce nombre. Windows MR prend également en charge les niveaux de détail Geometry facultatifs (LODs) pour garantir une expérience performante et de haute qualité. [Le WindowsMRAssetConverter](https://github.com/Microsoft/glTF-Toolkit/releases) vous permet de combiner 3 versions de votre modèle en un seul modèle. glb. Windows détermine le LOD à afficher en fonction de la quantité d’écran occupée par le modèle. Seuls 3 niveaux de LOD sont pris en charge avec les nombres de triangles recommandés suivants:
<br>

|  Niveau LOD  |  Nombre de triangles recommandé  |  Nombre maximal de triangles | 
|------|------|------|
|  LOD 0 |  10 000 |  10 000 | 
|  LOD 1 |  5 000  |  10 000 | 
|  LOD 2 |  2 500  |  10 000 | 

### <a name="node-counts-and-submesh-limits"></a>Nombres de nœuds et limites de sous-maillage
La page d’hébergement de la réalité mixte Windows ne prend pas en charge les modèles avec plus de 64 nœuds ou de sous-maillages 32 par LOD. Les nœuds sont un concept de la [spécification glTF](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#nodes-and-hierarchy) qui définit les objets de la scène. Les sous-maillages sont définis dans le tableau de [primitives](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#meshes) sur le maillage de l’objet. 

|  Fonctionnalité |  Description  |  Max pris en charge | Documentation |
|------|------|------|------|
|  Nœuds |  Objets dans la scène glTF |  64 par LOD | [Cette](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#nodes-and-hierarchy)|
|  Sous-maillages |  Somme des primitives sur tous les maillages |  32 par LOD | [Cette](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#meshes)|

## <a name="material-guidelines"></a>Instructions relatives aux matériaux

Les textures doivent être préparées à l’aide d’un flux de travail d’irrégularité du métal PBR. Commencez par créer un ensemble complet de textures, notamment Albedo, normal, occlusion, métallique et rugueuse. Windows Mixed Reality prend en charge les textures avec des résolutions allant jusqu’à 4096x4096, mais il est recommandé de créer chez 512 x 512. En outre, les textures doivent être créées à des résolutions par multiples de 4, car il s’agit d’une condition requise pour le format de compression appliqué aux textures dans les étapes d’exportation décrites ci-dessous. Enfin, lorsque gerating MIP mappe ou une texture, le MIP le plus bas doit être un maximum de 4 x 4.
<br>

|  Taille de texture recommandée  |  Taille maximale de la texture | MIP le plus bas
|----|----|----|
|  512 x 512  |  4096x4096 | 4x4 max.|

### <a name="albedo-base-color-map"></a>Carte Albedo (couleur de base)

Couleur brute sans informations d’éclairage. Cette carte contient également les informations de réflectivité et de diffusion pour le métal (blanc dans les cartes métalliques) et l’isolateur (noir dans les surfaces métalliques) respectivement.

### <a name="normal"></a>Normale

Carte normale d’espace tangente

### <a name="roughness-map"></a>Carte d’irrégularité

Décrit le microsurface de l’objet. Le blanc 1,0 est un espace blanc grossier de 0,0. Cette carte donne à l’élément multimédia le plus grand nombre de caractères, par exemple les éraflures, les empreintes digitales, les traînées, les Grime, etc.

### <a name="ambient-occlusion-map"></a>Carte d’occlusion ambiante

Carte de mise à l’échelle des valeurs montrant les zones de bloqués Light qui bloquent les réflexions

### <a name="metallic-map"></a>Carte métallique

Indique au nuanceur s’il s’agit d’un métal ou non. RAW Metal = 1,0 blanc non Metal = 0,0 noir. Il peut y avoir des valeurs de gris transitoires qui indiquent un sujet couvrant le métal brut tel que le saleté, mais en général, cette carte doit être en noir et blanc uniquement.

## <a name="optimizations"></a>Optimisations

La page d’hébergement Windows Mixed Reality offre une série d’optimisations par-dessus les spécifications glTF principales définies à l’aide d’extensions personnalisées. Ces optimisations sont requises sur les versions de Windows < = 1709 et recommandées sur les versions plus récentes de Windows. Vous pouvez facilement optimiser n’importe quel modèle glTF 2,0 à l’aide de [Windows Mixed Reality Converter disponible sur GitHub](https://github.com/Microsoft/glTF-Toolkit/releases). Cet outil effectuera les optimisations de l’empaquetage et des optimisations de texture, comme indiqué ci-dessous. Pour une utilisation générale, nous vous recommandons d’utiliser WindowsMRAssetConverter, mais si vous avez besoin de davantage de contrôle sur l’expérience et que vous souhaitez créer votre propre pipeline optmization, vous pouvez vous référer à la spécification détaillée ci-dessous.  

### <a name="materials"></a>Destinés

Pour améliorer le temps de chargement des ressources dans les environnements de réalité mixte, Windows MR prend en charge le rendu des textures DDS compressées compressées en fonction du schéma de distribution de texture défini dans cette section. Les textures DDS sont référencées à l’aide de l' [extension MSFT_texture_dds](https://github.com/sbtron/glTF/tree/MSFT_lod/extensions/Vendor/MSFT_texture_dds). La compression des textures est fortement recommandée. 

#### <a name="hololens"></a>HoloLens

Les expériences de réalité mixte basées sur HoloLens s’attendent à ce que les textures soient emballées à l’aide d’une configuration à 2 textures à l’aide des spécifications suivantes:
<br>

|  Propriété glTF  |  Motif  |  Schéma d’emballage | 
|----------|----------|----------|
|  pbrMetallicRoughness  |  baseColorTexture  |  Rouge (R), vert (G), bleu (B) | 
|  [MSFT_packing_normalRoughnessMetallic](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_normalRoughnessMetallic/README.md)  |  normalRoughnessMetallicTexture  |  Normal (RG), rugosité (B), métal (A) | 


Lorsque vous compressez les textures DDS, la compression suivante est attendue sur chaque carte:
<br>

|  Motif  |  Compression attendue | 
|------|------|
|  baseColorTexture, normalRoughnessMetallicTexture |  BC7 | 

#### <a name="immersive-vr-headsets"></a>Casques immersifs (VR)

Les expériences Windows Mixed Reality basées sur PC pour les casques immersifs s’attendent à ce que les textures soient emballées à l’aide d’une configuration à 3 textures à l’aide de la spécification de compression suivante:

##### <a name="windows-os--1803"></a>> Du système d’exploitation Windows = 1803

<br>

|  Propriété glTF  |  Motif  |  Schéma d’emballage | 
|----------|----------|----------|
|  pbrMetallicRoughness  |  baseColorTexture  |  Rouge (R), vert (G), bleu (B) | 
|  [MSFT_packing_occlusionRoughnessMetallic](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_occlusionRoughnessMetallic/README.md)  |  occlusionRoughnessMetallicTexture  |  Occlusion (R), ébauche (G), métal (B) | 
|  [MSFT_packing_occlusionRoughnessMetallic](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_occlusionRoughnessMetallic/README.md)  |  normalTexture  |  Normal (RG) | 

Lorsque vous compressez les textures DDS, la compression suivante est attendue sur chaque carte:
<br>

|  Motif  |  Compression attendue | 
|------|------|
|  normalTexture  |  BC5 | 
|  baseColorTexture, occlusionRoughnessMetallicTexture  |  BC7 | 

##### <a name="windows-os--1709"></a>< Du système d’exploitation Windows = 1709
<br>

|  Propriété glTF  |  Motif  |  Schéma d’emballage | 
|----------|----------|----------|
|  pbrMetallicRoughness  |  baseColorTexture  |  Rouge (R), vert (G), bleu (B) | 
|  [MSFT_packing_occlusionRoughnessMetallic](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_occlusionRoughnessMetallic/README.md)  |  roughnessMetallicOcclusionTexture  |  Rugosité (R), métal (G), occlusion (B) | 
|  [MSFT_packing_occlusionRoughnessMetallic](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_occlusionRoughnessMetallic/README.md)  |  normalTexture  |  Normal (RG) | 

Lorsque vous compressez les textures DDS, la compression suivante est attendue sur chaque carte:
<br>

|  Motif  |  Compression attendue | 
|------|------|
|  normalTexture  |  BC5 | 
|  baseColorTexture, roughnessMetallicOcclusionTexture | BC7 |

### <a name="adding-mesh-lods"></a>Ajout de Mesh LODs

Windows MR utilise un nœud Geometry LODs pour restituer des modèles 3D à différents niveaux de détail en fonction de la couverture de l’écran. Bien que cette fonctionnalité ne soit techniquement pas nécessaire, elle est fortement recommandée pour tous les éléments multimédias. Actuellement, Windows prend en charge 3 niveaux de détail. Le LOD par défaut est 0, ce qui représente la meilleure qualité. Les autres LODs sont numérotés séquentiellement, par exemple 1, 2 et sont progressivement plus bas en qualité. Le [convertisseur Windows Mixed Reality Asset](https://github.com/Microsoft/glTF-Toolkit/releases) prend en charge la génération de ressources qui répondent à cette spécification LOD en acceptant plusieurs modèles glTF et en les fusionnant dans une seule ressource avec des niveaux de LOD valides. Le tableau suivant présente le classement LOD attendu et les cibles de triangle:
<br>

|  Niveau LOD  |  Nombre de triangles recommandé  |  Nombre maximal de triangles | 
|-------|-------|-------|
|  LOD 0 |  10 000 |  10 000 | 
|  LOD 1 |  5 000  |  10 000 | 
|  LOD 2 |  2 500  |  10 000 | 

Lorsque vous utilisez LODs, spécifiez toujours 3 niveaux de LOD. Un LODs manquant entraîne le non-rendu du modèle de manière inattendue, car le système LOD passe au niveau de LOD manquant. glTF 2,0 ne prend pas actuellement en charge LODs dans le cadre de la spécification de base. LODs doit donc être défini à l’aide de l' [extension MSFT_LOD](https://github.com/sbtron/glTF/tree/MSFT_lod/extensions/Vendor/MSFT_lod).

### <a name="screen-coverage"></a>Couverture de l’écran

Les LODs sont affichés dans Windows Mixed Reality en fonction d’un système piloté par la valeur de la couverture d’écran définie sur chaque LOD. Les objets qui consomment actuellement une plus grande partie de l’espace d’écran sont affichés à un niveau plus élevé de LOD. La couverture d’écran ne fait pas partie de la spécification Core glTF 2,0 et doit être spécifiée à l’aide de MSFT_ScreenCoverage dans la section «Extras» de l' [extension MSFT_lod](https://github.com/sbtron/glTF/tree/MSFT_lod/extensions/Vendor/MSFT_lod).
<br>

|  Niveau LOD  |  Plage recommandée  |  Plage par défaut | 
|-------|-------|-------|
|  LOD 0  |  100%-50% |  .5 | 
|  LOD 1 |  Moins de 50%-20%  |  cède | 
|  LOD 2 |  Moins de 20%-1%  |  0,01 | 
|  LOD 4  |  Moins de 1%  |  - | 

## <a name="animation-guidelines"></a>Instructions d’animation

> [!NOTE]
> Cette fonctionnalité a été ajoutée dans le cadre de la [mise à jour 2018 d’avril de Windows 10](release-notes-april-2018.md). Dans les versions antérieures de Windows, ces animations ne seront pas lues, mais elles continueront à être chargées si elles sont créées conformément aux instructions de cet article.  

La page d’hébergement de la réalité mixte prend en charge les objets glTF animés sur les casques HoloLens et immersif (VR). Si vous souhaitez déclencher des animations sur votre modèle, vous devez utiliser l’extension de la carte d’animation au format glTF. Cette extension vous permet de déclencher des animations dans le modèle glTF en fonction de la présence des utilisateurs dans le monde, par exemple déclencher une animation lorsque l’utilisateur est proche de l’objet ou qu’il l’examine. Si vous glTF objet contient des animations, mais ne définit pas les déclencheurs, les animations ne sont pas lues. La section ci-dessous décrit un flux de travail pour l’ajout de ces déclencheurs à n’importe quel objet glTF animé.

### <a name="tools"></a>Outils
Tout d’abord, téléchargez les outils suivants si vous ne les avez pas déjà. Ces outils facilitent l’ouverture de tout modèle glTF, la préversion, la modification et l’enregistrement d’une sauvegarde en tant que glTF ou. glb:
1. [Visual Studio Code](https://code.visualstudio.com/)
2. [Outils glTF pour Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=cesium.gltf-vscode)


### <a name="opening-and-previewing-the-model"></a>Ouverture et aperçu du modèle
Commencez par ouvrir le modèle glTF dans VSCode en faisant glisser le fichier. glTF dans la fenêtre de l’éditeur. Notez que si vous avez un fichier. GLB au lieu d’un fichier. glTF, vous pouvez l’importer dans VSCode à l’aide du complément outils glTF que vous avez téléchargé. Accédez à «View-> Command palette», puis commencez à taper «glTF» dans la palette de commandes et sélectionnez «glTF: Importez à partir de GLB» qui contiendra un sélecteur de fichier pour que vous importiez un. GLB avec. 

Une fois que vous avez ouvert votre modèle glTF, le code JSON doit s’afficher dans la fenêtre de l’éditeur. Notez que vous pouvez également afficher un aperçu du modèle dans une visionneuse 3D en direct à l’aide du en cliquant avec le bouton droit sur le nom du fichier et en sélectionnant l’option «glTF: Aperçu du modèle 3D» dans le menu contextuel. 

### <a name="adding-the-triggers"></a>Ajout des déclencheurs
Les déclencheurs d’animation sont ajoutés au modèle JSON glTF à l’aide de l’extension de mappage d’animation. L’extension de mappage d’animation est documentée publiquement [ici sur GitHub](https://github.com/msfeldstein/glTF/blob/04f7005206257cf97b215df5e3f469d7838c1fee/extensions/Vendor/FB_animation_map/README.md) (Remarque: IL S’AGIT D’UNE EXTENSION DE BROUILLON). Pour ajouter l’extension à votre modèle, faites défiler jusqu’à la fin du fichier glTF dans l’éditeur et ajoutez le bloc «extensionsUsed» et «extensions» à votre fichier s’ils n’existent pas déjà. Dans la section «extensionsUsed», vous allez ajouter une référence à l’extension «EXT_animation_map» et dans le bloc «extensions», vous ajouterez vos mappages aux animations dans le modèle.

Comme indiqué [dans la spécification](https://github.com/msfeldstein/glTF/blob/04f7005206257cf97b215df5e3f469d7838c1fee/extensions/Vendor/FB_animation_map/README.md) , vous définissez ce qui déclenche l’animation à l’aide de la chaîne «sémantique» sur une liste d' «animations», qui est un tableau d’index d’animation. Dans l’exemple ci-dessous, nous avons spécifié l’animation à lire lorsque l’utilisateur est Gazing au niveau de l’objet:

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
L’animation suivante déclenche la sémantique est prise en charge par la page d’hébergement Windows Mixed Reality.  
* «ALWAYS»: Boucler constamment une animation
* «DÉTENU»: En boucle pendant toute la durée d’un objet.
* «POINT DE REGARD»: En boucle lors de la recherche d’un objet
* «PROXIMITÉ»: En boucle lorsqu’une visionneuse est proche d’un objet
* «POINTAGE»: En boucle lorsqu’un utilisateur pointe sur un objet

### <a name="saving-and-exporting"></a>Enregistrement et exportation
Une fois que vous avez apporté les modifications à votre modèle glTF, vous pouvez l’enregistrer directement en tant que glTF, ou vous pouvez cliquer avec le bouton droit sur le nom du fichier dans l’éditeur et sélectionner «glTF: Exporter vers GLB (fichier binaire)» pour exporter un. glb. 

### <a name="restrictions"></a>Restrictions
Les animations ne peuvent pas dépasser 20 minutes et ne peuvent pas contenir plus de 36 000 images clés (20 minutes à 30 i/s). En outre, lorsque vous utilisez des animations basées sur des cibles morphes, vous ne dépassez pas 8192 sommets de cible morphe ou moins. Si vous dépassez ce nombre, la ressource animée sera entraînere non prise en charge dans la page d’hébergement Windows Mixed Reality. 

|Fonctionnalité|Maximale|
|-----|-----|
|Duration|20 minutes|
|Images clés|36,000| 
|Vertex cible Morph|8 192|

## <a name="gltf-implementation-notes"></a>Remarques sur l’implémentation de glTF
Windows MR ne prend pas en charge le retournement de géométrie à l’aide d’échelles négatives. La géométrie avec des échelles négatives entraîne probablement des artefacts visuels.

La ressource glTF doit pointer vers la scène par défaut à l’aide de l’attribut Scene qui doit être rendu par Windows MR. En outre, le chargeur glTF de Windows RM antérieur à la [mise à jour 2018 de Windows 10 avril](release-notes-april-2018.md) **requiert** des accesseurs:
* Doit avoir des valeurs min et max.
* Le type scalaire doit être componentType UNSIGNED_SHORT (5123) ou UNSIGNED_INT (5125).
* Le type VEC2 et VEC3 doit être componentType FLOAT (5126).

Les propriétés de matériau suivantes sont utilisées à partir de Core glTF 2,0 Spec, mais pas obligatoire:
* baseColorFactor, metallicFactor, roughnessFactor
* baseColorTexture: Doit pointer vers une texture stockée dans DDS.
* emissiveTexture: Doit pointer vers une texture stockée dans DDS.
* emissiveFactor
* alphaMode

Les propriétés de matériau suivantes sont ignorées à partir des spécifications principales:
* Tous les UVs
* metalRoughnessTexture: Doit utiliser à la place la distribution de texture optimisée Microsoft définie ci-dessous
* normalTexture: Doit utiliser à la place la distribution de texture optimisée Microsoft définie ci-dessous
* normalScale
* occlusionTexture: Doit utiliser à la place la distribution de texture optimisée Microsoft définie ci-dessous
* occlusionStrength

Windows MR ne prend pas en charge les lignes et les points en mode primitif. 

Un seul attribut de vertex UV est pris en charge.

## <a name="additional-resources"></a>Ressources supplémentaires
* [exportateurs et convertisseurs glTF](https://github.com/KhronosGroup/glTF#converters-and-exporters)
* [Boîte à outils glTF](https://github.com/Microsoft/glTF-Toolkit)
* [Spécification glTF 2,0](https://github.com/KhronosGroup/glTF/blob/master/README.md)
* [Spécification de l’extension Microsoft glTF LOD](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_lod/README.md)
* [Spécification des extensions de la compression de texture PC Mixed Real](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_occlusionRoughnessMetallic/README.md)
* [Spécification des extensions de compression de texture de réalité mixte HoloLens](https://github.com/KhronosGroup/glTF/blob/master/extensions/2.0/Vendor/MSFT_packing_normalRoughnessMetallic/README.md)
* [Spécification des extensions glTF textures Microsoft DDS](https://github.com/KhronosGroup/glTF/tree/master/extensions/2.0/Vendor/MSFT_texture_dds)

## <a name="see-also"></a>Voir aussi

* [Implémenter des lanceurs d’applications 3D (applications UWP)](implementing-3d-app-launchers.md)
* [Implémenter des lanceurs d’applications 3D (applications Win32)](implementing-3d-app-launchers-win32.md)
* [Exploration de la page d’accueil Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md)
