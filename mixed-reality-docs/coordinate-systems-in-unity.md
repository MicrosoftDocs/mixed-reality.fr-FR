---
title: Systèmes de coordonnées dans Unity
description: Apprenez à créer assis, permanent, salle à l’échelle et à l’échelle du monde mixte réalité des expériences dans Unity.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: système de coordonnées, système de coordonnées spatial, orientation, à l’échelle en place et seule permanent à l’échelle, salle à l’échelle, mise à l’échelle mondiale, assis à 360 degrés, debout, salle, monde, à l’échelle, position, orientation, Unity, ancre, spatiale d’ancrage, ancre world, world-verrouillé, verrouillage de monde, body-verrouillée, corps de verrouillage, suivi de perte, locatability, limites, recentrer
ms.openlocfilehash: 36d74488b23587e5c89b40faf97921a10be7473b
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597105"
---
# <a name="coordinate-systems-in-unity"></a>Systèmes de coordonnées dans Unity

Réalité mixte Windows prend en charge les applications sur une large gamme de [expérience échelles](coordinate-systems.md), à partir d’applications orientation uniquement et à l’échelle en place des via des applications à l’échelle de salle. Sur HoloLens, vous pouvez aller plus loin et créer des applications à l’échelle mondiale qui permettent aux utilisateurs de parcourir au-delà de 5 mètres, explorant un étage entier d’un bâtiment et au-delà.

Votre première étape dans la création d’une expérience de réalité mixte dans Unity consiste à déterminer quel [expérience mise à l’échelle](coordinate-systems.md) votre application ciblera.

## <a name="building-an-orientation-only-or-seated-scale-experience"></a>Création d’une expérience de l’orientation uniquement ou à l’échelle en place

**Namespace :** *UnityEngine.XR*<br>
**Type :** *XRDevice*

Pour générer un **orientation seule** ou **assis à l’échelle du expérience**, vous devez définir Unity à l’arrêt suivi du type d’espace. Cela définit le système de coordonnées de monde d’Unity pour suivre le [de référence stationnaire](coordinate-systems.md#spatial-coordinate-systems). Dans le mode de suivi stationnaire, contenu placé dans l’éditeur juste devant l’emplacement par défaut de l’appareil photo (-Z est vers l’avant) apparaît devant l’utilisateur quand l’application démarre.

```cs
XRDevice.SetTrackingSpaceType(TrackingSpaceType.Stationary);
```

**Namespace :** *UnityEngine.XR*<br>
**Type :** *InputTracking*

Pour une pure **orientation seule expérience** tels que l’Observateur de vidéo à 360 degrés (où les mises à jour principal positionnels seraient endommager l’illusion), vous pouvez ensuite définir [XR. InputTracking.disablePositionalTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking-disablePositionalTracking.html) sur true :

```cs
InputTracking.disablePositionalTracking = true;
```

Pour un **assis à l’échelle du expérience**, pour permettre à l’utilisateur plus tard recentrer l’origine assis, vous pouvez appeler la [XR. InputTracking.Recenter](https://docs.unity3d.com/ScriptReference/XR.InputTracking.Recenter.html) méthode :

```cs
InputTracking.Recenter();
```

## <a name="building-a-standing-scale-or-room-scale-experience"></a>Création d’une expérience permanent à l’échelle ou d’échelle de la salle

**Namespace :** *UnityEngine.XR*<br>
**Type :** *XRDevice*

Pour un **permanent à l’échelle** ou **expérience de l’échelle de la salle**, vous devez placer le contenu relatif à l’étage. Sur l’utilisateur de la raison floor, à l’aide de la  **[étape spatial](coordinate-systems.md#spatial-coordinate-systems)**, qui représente l’utilisateur défini au niveau du sol origine et les limites de salle facultatif, définissez au cours de première exécution.

Pour vous assurer que Unity fonctionne avec son système de coordonnées de monde au niveau du sol, vous pouvez définir que Unity pour le suivi du type de l’espace de RoomScale et vous assurer que le jeu réussit :

```cs
if (XRDevice.SetTrackingSpaceType(TrackingSpaceType.RoomScale))
{
    // RoomScale mode was set successfully.  App can now assume that y=0 in Unity world coordinate represents the floor.
}
else
{
    // RoomScale mode was not set successfully.  App cannot make assumptions about where the floor plane is.
}
```
* Si SetTrackingSpaceType retourne la valeur true, Unity a basculé correctement son système de coordonnées de monde pour suivre le [phase de référence](coordinate-systems.md#spatial-coordinate-systems).
* Si SetTrackingSpaceType retourne la valeur false, Unity a été impossible de passer du stade cadre de référence, probablement parce que l’utilisateur n’a pas configuré de même un étage dans leur environnement. Cela n’est pas courant, mais peut se produire si l’étape a été configurée dans une autre pièce et que l’appareil a été déplacé vers la salle sans le paramètre de l’utilisateur d’une nouvelle étape.

Une fois que votre application définit correctement le RoomScale suivi de type d’espace, contenu placé sur la y = 0 plan s’affiche sur le sol. L’origine (0, 0, 0) sera l’emplacement spécifique sur le lieu où l’utilisateur a su résister pendant l’installation de la salle, avec -Z qui représente la direction avant qu’ils ont été confrontés pendant l’installation.

**Namespace :** *UnityEngine.Experimental.XR*<br>
**Type :** *Limites*

Dans le code de script, vous pouvez, puis appelez la méthode TryGetGeometry vous êtes du genre à UnityEngine.Experimental.XR.Boundary pour obtenir un polygone de la limite, en spécifiant un type de limite de TrackedArea. Si l’utilisateur défini une limite (vous obtenez une liste de sommets), vous savez qu’il fournir un **expérience de l’échelle de la salle** à l’utilisateur, où ils peuvent la scène vous guider créer.

Notez que le système affiche automatiquement la limite lors de l’utilisateur à l’approche. Votre application n’a pas besoin d’utiliser ce polygone pour restituer la limite de lui-même. Toutefois, vous pouvez choisir de disposer de vos objets de scène à l’aide de ce polygone limite, pour vous assurer de que l’utilisateur peut atteindre physiquement ces objets sans teleporting :

```cs
var vertices = new List<Vector3>();
if (UnityEngine.Experimental.XR.Boundary.TryGetGeometry(vertices, Boundary.Type.TrackedArea))
{
    // Lay out your app's content within the boundary polygon, to ensure that users can reach it without teleporting.
}
```

## <a name="building-a-world-scale-experience"></a>Création d’une expérience à l’échelle mondiale

**Namespace :** *UnityEngine.XR.WSA*<br>
**Type :** *WorldAnchor*

Pour true **expériences à l’échelle du monde** sur HoloLens qui permettent aux utilisateurs de plate-formes au-delà de 5 mètres, vous devez disposer des nouvelles techniques au-delà de celles utilisées pour les expériences de l’échelle de la salle. Une technique clé que vous utiliserez consiste à créer un [ancre spatial](coordinate-systems.md#spatial-anchors) pour verrouiller un cluster de hologrammes précisément en place dans le monde physique, quelle que soit la distance, l’utilisateur est déplacé, puis [suite de retrouver ces hologrammes à nouveau dans sessions](coordinate-systems.md#spatial-anchor-persistence).

Dans Unity, vous créez un point d’ancrage spatiale en ajoutant le **WorldAnchor** composant Unity à un GameObject.

### <a name="adding-a-world-anchor"></a>Ajout d’un point d’ancrage du monde

Pour ajouter un point d’ancrage du monde, appelez AddComponent<WorldAnchor>() sur l’objet de jeu avec la transformation que vous souhaitez ancrer dans le monde réel.

```cs
WorldAnchor anchor = gameObject.AddComponent<WorldAnchor>();
```

C’est tout ! Cet objet de jeu sera désormais être ancré à son emplacement actuel dans le monde physique, vous pouvez voir ses coordonnées de monde Unity ajuster légèrement au fil du temps pour vous assurer qu’alignement physique. Utilisez [persistance](persistence-in-unity.md) à trouver cela ancrée emplacement dans une session de futures de l’application.

### <a name="removing-a-world-anchor"></a>Suppression d’un point d’ancrage du monde

Si n’est plus, vous souhaitez que le GameObject verrouillé sur un emplacement du monde physique et que vous ne prévoyez pas sur le déplacement de ce cadre, vous pouvez simplement appeler Destroy sur le composant de point d’ancrage du monde entier.

```cs
Destroy(gameObject.GetComponent<WorldAnchor>());
```

Si vous souhaitez déplacer le GameObject ce cadre, vous devez appeler DestroyImmediate à la place.

```cs
DestroyImmediate(gameObject.GetComponent<WorldAnchor>());
```

### <a name="moving-a-world-anchored-gameobject"></a>Déplacement d’un monde ancrée GameObject

Impossible de déplacer du GameObject pendant une ancre de World dessus. Si vous devez déplacer le GameObject ce frame, vous devez :
1. DestroyImmediate le composant de point d’ancrage du monde
2. Déplacer le GameObject
3. Ajouter un nouveau composant de point d’ancrage du monde entier pour le GameObject.

```cs
DestroyImmediate(gameObject.GetComponent<WorldAnchor>());
gameObject.transform.position = new Vector3(0, 0, 2);
WorldAnchor anchor = gameObject.AddComponent<WorldAnchor>();
```

### <a name="handling-locatability-changes"></a>Gestion des modifications de Locatability

Un WorldAnchor peut-être pas localisable dans le monde physique à un point dans le temps. Si cela se produit, Unity n'a pas mis à jour la transformation de l’objet ancré. Cela peut également changer pendant l’exécution d’une application. Gérer les modifications dans locatability provoquera l’objet s’affiche ne pas dans l’emplacement physique approprié dans le monde.

Pour être averti des modifications de locatability :
1. S’abonner à l’événement OnTrackingChanged
2. Gérer l’événement

Le **OnTrackingChanged** événement sera appelé chaque fois que le point d’ancrage spatial sous-jacent change entre un état d’être localisables et n’est pas localisable.

```cs
anchor.OnTrackingChanged += Anchor_OnTrackingChanged;
```

Puis gérer l’événement :

```cs
private void Anchor_OnTrackingChanged(WorldAnchor self, bool located)
{
    // This simply activates/deactivates this object and all children when tracking changes
    self.gameObject.SetActiveRecursively(located);
}
```

Parfois ancres se trouvent immédiatement. Dans ce cas, cette propriété isLocated de l’ancrage est fixée à true lorsque AddComponent<WorldAnchor>() retourne. Par conséquent, l’événement OnTrackingChanged ne sera pas déclenchée. Un modèle propre consisterait à appeler votre gestionnaire OnTrackingChanged avec l’état initial de IsLocated après l’attachement d’un point d’ancrage.

```cs
Anchor_OnTrackingChanged(anchor, anchor.isLocated);
```

## <a name="sharing-anchors-across-devices"></a>Partage des points d’ancrage sur des appareils

Vous pouvez utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a> pour créer un point d’ancrage cloud durable à partir d’un WorldAnchor local, lequel votre application peut ensuite localiser dans plusieurs HoloLens, appareils iOS et Android.  En partageant une ancre spatiale commune sur plusieurs appareils, chaque utilisateur peut voir le contenu restitué par rapport à ce point d’ancrage dans le même emplacement physique.  Ainsi, les expériences partagées en temps réel.

Pour commencer à créer des expériences partagées dans Unity, essayez les 5 minutes <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Démarrages rapides Azure Spatial ancres Unity</a>.

Une fois que vous êtes en cours d’exécution ancres spatiale d’Azure, vous pouvez ensuite <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">créer et localiser les points d’ancrage dans Unity</a>.

## <a name="see-also"></a>Voir aussi
* [Échelles de l’expérience](coordinate-systems.md#mixed-reality-experience-scales)
* [Étape spatial](coordinate-systems.md#stage-frame-of-reference)
* [Suivi de la perte dans Unity](tracking-loss-in-unity.md)
* [Ancres spatiales](spatial-anchors.md)
* [Persistance dans Unity](persistence-in-unity.md)
* [Expériences partagées dans Unity](shared-experiences-in-unity.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Ancres Spatial Azure</a>
* <a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Ancres Spatial Azure SDK pour Unity</a>