---
title: Compréhension des scènes
description: Présentation des fonctionnalités de présentation de la scène pour HoloLens
author: szymons
ms.author: szymons
ms.date: 07/08/2019
ms.topic: article
keywords: Compréhension des scènes, mappage spatial, Windows Mixed Reality, Unity
ms.openlocfilehash: 3d56f375c38b1dee6ab9eb97219a5e37fe698c63
ms.sourcegitcommit: 37816514b8fe20669c487774b86e80ec08edcadf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/09/2020
ms.locfileid: "81003335"
---
# <a name="scene-understanding"></a>Compréhension des scènes

La présentation des scènes fournit aux développeurs de réalité mixte une représentation d’environnement structurée et de haut niveau, conçue pour rendre le développement pour les applications compatibles avec l’environnement intuitif. Pour ce faire, nous combinons la puissance des runtimes de réalité mixte existants, tels que le [mappage spatial](spatial-mapping.md) très précis moins structuré et les nouveaux runtimes reposant sur l’intelligence artificielle. En combinant ces technologies, la compréhension des scènes génère des représentations d’environnements 3D similaires à celles que vous avez pu utiliser dans des infrastructures telles que Unity ou ARKit/ARCore. La scène comprendre le point d’entrée commence par un observateur de scène, qui est appelé par votre application pour calculer une nouvelle scène. Aujourd’hui, la technologie est capable de générer 3 catégories d’objets distinctes, mais connexes : des maillages d’environnement étanches simplifiés qui déduirent la structure de la pièce planaire sans encombrement, les régions plan pour le positionnement que nous appelons Quad et une capture instantanée du maillage de [mappage spatial](spatial-mapping.md) qui s’aligne sur les quadruples/les données étanches que nous surfaces.

![Maillage de mappage spatial, intitulé surfaces planées, maillage étanche](images/SUScenarios.png)

Ce document est destiné à fournir une vue d’ensemble du scénario et à clarifier la relation avec la compréhension des scènes et le partage spatial.

## <a name="developing-with-scene-understanding"></a>Développement avec la compréhension de la scène

Cet article sert uniquement à présenter la scène présentation du runtime et des concepts. Si vous recherchez de la documentation sur la manière de développer avec la compréhension des scènes, vous pouvez être intéressé par les éléments suivants :

[Présentation du SDK présentation de Scene](scene-understanding-SDK.md)

Vous pouvez télécharger l’exemple d’application Scene Understanding à partir de l’exemple de site GitHub :

[Exemple de compréhension de scène](https://github.com/sceneunderstanding-microsoft/unitysample)

Si vous n’avez pas de périphérique et que vous souhaitez accéder à des exemples de scènes pour essayer de comprendre les scènes, il existe des scènes dans l’exemple de dossier de ressources :

[Exemples de scènes de vision](https://github.com/sceneunderstanding-microsoft/unitysample/tree/master/Assets/Resources/SerializedScenesForPCPath)

### <a name="sdk"></a>Kit de développement logiciel

Si vous recherchez des informations spécifiques sur le développement pour la compréhension de scènes ou des détails sur le fonctionnement de scenes et sur son développement, consultez la documentation de [Présentation de Scene Understanding SDK](scene-understanding-SDK.md) .


### <a name="sample"></a>Exemple


## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Compréhension des scènes</td>
        <td>❌</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

## <a name="common-usage-scenarios"></a>Scénarios d’utilisation courants

![des illustrations de scénarios courants d’utilisation de mappages spatiaux : placement, occlusion, physique et navigation](images/sm-concepts-1000px.png)<br>
*Scénarios courants d’utilisation du mappage spatial : placement, occlusion, physique et navigation.*

<br>

La plupart des scénarios de base pour les applications prenant en charge l’environnement (placement, occlusion, physique, etc.) sont adressables à la fois par le mappage spatial et la compréhension des scènes, et cette section met en évidence ces différences. L’une des principales différences entre la compréhension des scènes et le mappage spatial est un compromis entre la précision et la latence maximales de la structure et de la simplicité. Si votre application nécessite la latence la plus faible possible et les triangles de maillage auxquels vous seul souhaitez accéder, utilisez le mappage spatial directement. Si vous effectuez un traitement de niveau supérieur, vous pouvez envisager de basculer vers le modèle de compréhension de scène, car il doit vous fournir un sur-ensemble de fonctionnalités. Notez également que, étant donné que la compréhension de la scène fournit un instantané du maillage de mappage spatial dans le cadre de sa représentation, vous aurez toujours accès aux données de mappage spatiale les plus complètes et précises possibles.

Les sections suivantes réexaminent les scénarios de mappage spatial de base dans le contexte du nouveau kit de développement logiciel (SDK).

### <a name="placement"></a>Placement

La compréhension des scènes fournit de nouvelles constructions spécifiquement conçues pour simplifier les scénarios de placement. Une scène peut calculer des primitives appelées SceneQuads qui décrivent des surfaces plates sur lesquelles des hologrammes peuvent être placés. Les SceneQuads ont été spécifiquement conçus autour du placement et décrivent une surface 2D et fournissent une API pour l’emplacement de cette surface. Auparavant, lors de l’utilisation du maillage de triangles pour effectuer un placement, vous deviez analyser toutes les zones du quadruple et effectuer le remplissage/le traitement des trous pour identifier les emplacements corrects pour le placement des objets. Cela n’est pas toujours nécessaire avec les Quad, car l’exécution de la compréhension de la scène est capable de déduire les zones du quadruple qui n’ont pas été analysées et d’invalider les zones du quadruple qui ne font pas partie de la surface.

:::row:::
    :::column:::
       ![SceneQuads avec l’inférence désactivée, capturant les zones de positionnement pour les régions numérisées.](images/SUQuads.png)<br>
       **Image #1** -SceneQuads avec l’inférence désactivée, capturant les zones de positionnement pour les régions numérisées.
    :::column-end:::
        :::column:::
       ![quatre cœurs avec l’inférence activée, le placement n’est plus limité aux zones numérisées.](images/SUWatertight.png)<br>
        **Image #2** -quads avec l’inférence activée, le placement n’est plus limité aux zones numérisées.
    :::column-end:::
:::row-end:::

<br>


Si votre application envisage de placer des hologrammes 2D ou 3D sur des structures rigides de votre environnement, la simplicité et la commodité de SceneQuads pour le placement sont préférables à la détermination de ces informations à partir du maillage de [mappage spatial](spatial-mapping.md) . Pour plus d’informations sur cette rubrique, consultez la [documentation de référence du kit de développement SDK](scene-understanding-SDK.md)

**Remarque** Pour le code de positionnement hérité qui dépend du maillage de mappage spatial, le maillage de mappage spatial peut être calculé avec SceneQuads en définissant le paramètre EnableWorldMesh. Si la compréhension de l’API de scène ne répond pas aux exigences de latence de votre application, nous vous recommandons de continuer à utiliser l' [API de mappage spatial](spatial-mapping.md#placement).

### <a name="occlusion"></a>Occlusion

L' [occlusion de mappage spatial](spatial-mapping.md#occlusion) reste le moyen le moins latent de capturer l’État en temps réel de l’environnement. Bien que cela puisse être utile pour fournir une occlusion dans des scènes très dynamiques, vous pouvez envisager une compréhension de scène pour l’occlusion pour plusieurs raisons. Si vous utilisez la maille de mappage spatial générée par la compréhension des scènes, vous pouvez demander des données à partir d’un mappage spatial qui ne serait pas stocké dans le cache local et qui, par conséquent, n’est pas disponible à partir des API de perception. L’utilisation du mappage spatial pour l’occlusion avec les mailles étanches fournira une valeur supplémentaire, en particulier l’achèvement d’une structure de salle non scannée.

Si vos exigences peuvent tolérer l’augmentation de la latence de la compréhension des scènes, les développeurs d’applications doivent envisager d’utiliser la scène avec la vue de la maille étanche, et vraisemblablement la maille de mappage spatial dans des représentations planaires. Cela fournit un scénario de « meilleur des deux mondes » dans lequel l’occlusion à l’eau simplifiée est marié avec une géométrie non planive plus fine qui offre les cartes d’occlusion les plus réalistes possibles.

### <a name="physics"></a>Physique

La compréhension des scènes génère des maillages étanches qui décomposent l’espace avec la sémantique, en particulier pour répondre à de nombreuses limitations à la physique imposées par les maillages spatiaux. Les structures étanches garantissent que les conversions de rayon physique sont toujours atteintes, et la décomposition sémantique permet une génération plus simple de maillages de navigation pour la navigation intérieure. Comme décrit dans la section sur l' [occlusion](#occlusion), la création d’une scène avec EnableSceneObjectMeshes et EnableWorldMesh produira le maillage le plus physique possible. La propriété étanche de la maille d’environnement empêche les tests de positionnement de basculer vers les surfaces atteintes et les données de maillage garantissent que la physique interagit avec tous les objets de la scène, et pas seulement la structure de la pièce.

### <a name="navigation"></a>Navigation

Les maillages planaires décomposés par la classe sémantique sont des constructions idéales pour la navigation et la planification des chemins d’accès, ce qui simplifie la plupart des problèmes décrits dans la vue d’ensemble de la navigation dans le [mappage spatial](spatial-mapping.md#navigation) . Les objets SceneMesh calculés dans la scène sont déjà décomposés de type surface, ce qui garantit que la génération du maillage de navigation est limitée aux surfaces qui peuvent être parcourues. En raison de la simplicité de la structure Floor, la génération dynamique de maillages de navigation dans les moteurs 3D tels que Unity est réalisable en fonction des exigences en temps réel.

La génération de maillages de navigation précis nécessite toujours un traitement de validation, à savoir que les applications doivent toujours projeter Occluders sur le plancher pour s’assurer que la navigation ne passe pas par un désordre/des tables, etc... La méthode la plus précise pour y parvenir consiste à projeter les données de maillage universelles qui sont fournies si la scène est calculée avec l’indicateur EnableWorldMesh.

### <a name="visualization"></a>Visualisation

Bien qu’il soit possible d’utiliser la [visualisation de mappage spatial](spatial-mapping.md#visualization) pour obtenir des commentaires en temps réel sur l’environnement, il existe de nombreux scénarios dans lesquels la simplicité des objets planaires et étanches améliore les performances ou la qualité visuelle. La projection d’ombre et les techniques de mise à la terre décrites à l’aide du mappage spatial peuvent être plus attrayantes si elles sont projetées sur les surfaces planes fournies par quads ou la maille étanche planaire. Cela est particulièrement vrai pour les environnements/scénarios où la pré-analyse complète n’est pas optimale en raison du fait que la scène est déduite, et les environnements complets et les hypothèses planaires réduisent les artefacts.

En outre, le nombre total de surfaces retournées par le mappage spatial est limité par le cache spatial interne, tandis que la version de la vue de la représentation spatiale du maillage de mappage spatial peut accéder aux données de mappage spatiale qui ne sont pas mises en cache. Pour cette raison, la compréhension de la scène est plus adaptée à la capture des représentations de maillage pour les espaces plus larges (par exemple, plus grande qu’une seule pièce) pour la visualisation ou le traitement du maillage. La maille mondiale retournée avec EnableWorldMesh aura un niveau de détail cohérent tout au long de, ce qui peut générer une visualisation plus agréable si elle est rendue sous forme filaire.

### <a name="see-also"></a>Voir aussi

* [Scène Understanding SDK](scene-understanding-SDK.md)
* [Mappage spatial](spatial-mapping.md)
