---
title: Systèmes de coordonnées dans Unity
description: Découvrez comment créer des expériences de réalité mixte assiste, debout, à l’échelle de la place et à l’échelle mondiale dans Unity.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: système de coordonnées, système de coordonnées spatiales, orientation uniquement, à l’échelle assise, à l’échelle debout, à l’échelle de la pièce, à l’échelle mondiale, 360 de degrés, assis, debout, salle, monde, échelle, position, orientation, Unity, ancrage, ancrage spatial, ancrage universel, verrouillé, verrouillage universel, verrouillage du corps, verrouillage du corps, perte de suivi, localisation, limites, recentrer
ms.openlocfilehash: 36d74488b23587e5c89b40faf97921a10be7473b
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79375766"
---
# <a name="coordinate-systems-in-unity"></a>Systèmes de coordonnées dans Unity

Windows Mixed Reality prend en charge les applications à travers une large gamme d' [expériences](coordinate-systems.md), des applications en orientation seule et à l’échelle à l’échelle jusqu’à des applications à l’échelle de la place. Sur HoloLens, vous pouvez aller plus loin et créer des applications à l’échelle mondiale qui permettent aux utilisateurs d’aller au-delà de 5 mètres, en explorant un étage entier d’un immeuble et au-delà.

La première étape de la création d’une expérience de réalité mixte dans Unity consiste à déterminer la mise à l' [échelle](coordinate-systems.md) ciblée par votre application.

## <a name="building-an-orientation-only-or-seated-scale-experience"></a>Création d’une expérience d’orientation seule ou de mise à l’échelle installée

**Espace de noms :** *UnityEngine. XR*<br>
**Type :** *XRDevice*

Pour créer une expérience d' **orientation uniquement** ou de mise à l' **échelle assise**, vous devez définir Unity sur le type d’espace de suivi fixe. Définit le système de coordonnées universelles de Unity pour suivre le [cadre stationnaire de référence](coordinate-systems.md#spatial-coordinate-systems). Dans le mode de suivi fixe, le contenu placé dans l’éditeur juste devant l’emplacement par défaut de l’appareil photo (Forward is-Z) s’affiche devant l’utilisateur au lancement de l’application.

```cs
XRDevice.SetTrackingSpaceType(TrackingSpaceType.Stationary);
```

**Espace de noms :** *UnityEngine. XR*<br>
**Type :** *InputTracking*

Pour une expérience purement en **orientation uniquement** telle qu’une visionneuse vidéo de 360 degrés (où les mises à jour de la tête de position dépasseraient l’illusion), vous pouvez définir [XR. InputTracking. disablePositionalTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking-disablePositionalTracking.html) sur true :

```cs
InputTracking.disablePositionalTracking = true;
```

Pour une expérience de mise à l' **échelle assiste**, pour permettre à l’utilisateur de recentrer plus tard l’origine assise, vous pouvez appeler [XR. Méthode InputTracking. recenter](https://docs.unity3d.com/ScriptReference/XR.InputTracking.Recenter.html) :

```cs
InputTracking.Recenter();
```

## <a name="building-a-standing-scale-or-room-scale-experience"></a>Création d’une expérience de mise à l’échelle permanente ou à l’échelle de l’espace

**Espace de noms :** *UnityEngine. XR*<br>
**Type :** *XRDevice*

Pour une expérience à l’échelle **permanente** ou à l’échelle de l' **espace**, vous devez placer du contenu par rapport à l’étage. Vous avez raison de l’étage de l’utilisateur à l’aide de la **[Phase spatiale](coordinate-systems.md#spatial-coordinate-systems)** , qui représente l’origine de l’utilisateur et la limite facultative de l’espace, configurées lors de la première exécution.

Pour vous assurer que Unity fonctionne avec son système de coordonnées universel à l’étage, vous pouvez définir Unity sur le type d’espace de suivi RoomScale et vérifier que le jeu est correctement effectué :

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
* Si SetTrackingSpaceType retourne la valeur true, Unity a correctement basculé son système de coordonnées universel pour suivre le [cadre de la phase de référence](coordinate-systems.md#spatial-coordinate-systems).
* Si SetTrackingSpaceType retourne la valeur false, Unity n’a pas pu basculer vers le cadre de la phase de référence, ce qui est probablement dû au fait que l’utilisateur n’a pas configuré un étage dans son environnement. Ce n’est pas courant, mais cela peut se produire si l’étape a été configurée dans une autre salle et que l’appareil a été déplacé dans la salle active sans que l’utilisateur n’ait configuré une nouvelle phase.

Une fois que votre application a correctement défini le type d’espace de suivi RoomScale, le contenu placé sur le plan y = 0 s’affiche sur le plancher. L’origine à (0, 0, 0) sera l’emplacement spécifique sur le plancher où l’utilisateur a pris la main pendant la configuration de la salle, avec-Z représentant la direction vers l’avant au cours de l’installation.

**Espace de noms :** *UnityEngine. expérimentale. XR*<br>
**Type :** *limite*

Dans le code de script, vous pouvez ensuite appeler la méthode TryGetGeometry sur vous êtes le type UnityEngine. expérimental. XR. Boundary pour obtenir un polygone de limite, en spécifiant un type de limite de TrackedArea. Si l’utilisateur a défini une limite (vous récupérez une liste de vertex), vous savez qu’il est possible de fournir une expérience de mise à l’échelle de l' **espace** à l’utilisateur, où il peut se déplacer dans la scène que vous créez.

Notez que le système affiche automatiquement la limite lorsque l’utilisateur l’approche. Votre application n’a pas besoin d’utiliser ce polygone pour restituer la limite elle-même. Toutefois, vous pouvez choisir de disposer vos objets de scène à l’aide de ce polygone limite pour vous assurer que l’utilisateur peut atteindre physiquement ces objets sans téléportage :

```cs
var vertices = new List<Vector3>();
if (UnityEngine.Experimental.XR.Boundary.TryGetGeometry(vertices, Boundary.Type.TrackedArea))
{
    // Lay out your app's content within the boundary polygon, to ensure that users can reach it without teleporting.
}
```

## <a name="building-a-world-scale-experience"></a>Création d’une expérience à l’échelle mondiale

**Espace de noms :** *UnityEngine. XR. WSA*<br>
**Type :** *WorldAnchor*

Pour les expériences réelles à l' **échelle mondiale** sur HoloLens qui permettent aux utilisateurs d’aller au-delà de 5 mètres, vous aurez besoin de nouvelles techniques au-delà de celles utilisées pour les expériences à l’échelle de la place. Une technique clé que vous allez utiliser consiste à créer une [ancre spatiale](coordinate-systems.md#spatial-anchors) pour verrouiller un cluster d’hologrammes précisément en place dans le monde physique, quelle que soit la durée d’itinérance de l’utilisateur, puis [retrouvez ces hologrammes dans les sessions ultérieures](coordinate-systems.md#spatial-anchor-persistence).

Dans Unity, vous créez une ancre spatiale en ajoutant le composant **WorldAnchor** Unity à un GameObject.

### <a name="adding-a-world-anchor"></a>Ajout d’une ancre mondiale

Pour ajouter une ancre universelle, appelez AddComponent<WorldAnchor>() sur l’objet de jeu avec la transformation que vous souhaitez ancrer dans le monde réel.

```cs
WorldAnchor anchor = gameObject.AddComponent<WorldAnchor>();
```

C’est tout ! Cet objet de jeu sera désormais ancré à son emplacement actuel dans le monde physique : vous pouvez constater que ses coordonnées universelles s’ajustent légèrement au fil du temps pour garantir l’alignement physique. Utilisez la [persistance](persistence-in-unity.md) pour rechercher à nouveau cet emplacement d’ancrage dans une session d’application future.

### <a name="removing-a-world-anchor"></a>Suppression d’une ancre mondiale

Si vous ne souhaitez plus que les GameObject soient verrouillés sur un emplacement géographique physique et que vous n’envisagez pas de déplacer ce cadre, vous pouvez simplement appeler Destroy sur le composant d’ancrage du monde.

```cs
Destroy(gameObject.GetComponent<WorldAnchor>());
```

Si vous souhaitez déplacer le GameObject ce frame, vous devez appeler DestroyImmediate à la place.

```cs
DestroyImmediate(gameObject.GetComponent<WorldAnchor>());
```

### <a name="moving-a-world-anchored-gameobject"></a>Déplacement d’un GameObject ancré dans le monde

Les GameObject ne peuvent pas être déplacées pendant qu’une ancre mondiale y est. Si vous devez déplacer le GameObject ce frame, vous devez :
1. DestroyImmediate le composant d’ancrage universel
2. Déplacer le GameObject
3. Ajoutez un nouveau composant d’ancrage du monde au GameObject.

```cs
DestroyImmediate(gameObject.GetComponent<WorldAnchor>());
gameObject.transform.position = new Vector3(0, 0, 2);
WorldAnchor anchor = gameObject.AddComponent<WorldAnchor>();
```

### <a name="handling-locatability-changes"></a>Gestion des modifications de localisabilité

Un WorldAnchor peut ne pas être localisable dans le monde physique à un moment donné. Si cela se produit, Unity ne met pas à jour la transformation de l’objet ancré. Cela peut également changer pendant l’exécution d’une application. Si la modification de la localisation n’est pas prise en charge, l’objet n’apparaîtra pas à l’emplacement physique approprié dans le monde.

Pour être informé des changements de localisation :
1. S’abonner à l’événement OnTrackingChanged
2. Gérer l’événement

L’événement **OnTrackingChanged** est appelé chaque fois que l’ancrage spatial sous-jacent change entre un État localisable et n’est pas localisable.

```cs
anchor.OnTrackingChanged += Anchor_OnTrackingChanged;
```

Ensuite, gérez l’événement :

```cs
private void Anchor_OnTrackingChanged(WorldAnchor self, bool located)
{
    // This simply activates/deactivates this object and all children when tracking changes
    self.gameObject.SetActiveRecursively(located);
}
```

Parfois, les ancres se trouvent immédiatement. Dans ce cas, cette propriété isLocated de l’ancre sera définie sur true lorsque AddComponent<WorldAnchor>() retourne. Par conséquent, l’événement OnTrackingChanged n’est pas déclenché. Un modèle propre serait d’appeler votre gestionnaire OnTrackingChanged avec l’état initial de IsLocated après avoir attaché une ancre.

```cs
Anchor_OnTrackingChanged(anchor, anchor.isLocated);
```

## <a name="sharing-anchors-across-devices"></a>Partage d’ancres sur plusieurs appareils

Vous pouvez utiliser des <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres spatiales Azure</a> pour créer une ancre Cloud durable à partir d’un WorldAnchor local, que votre application peut ensuite localiser sur plusieurs appareils HoloLens, iOS et Android.  En partageant une ancre spatiale commune sur plusieurs appareils, chaque utilisateur peut voir le contenu affiché par rapport à cette ancre dans le même emplacement physique.  Cette technique autorise les expériences partagées en temps réel.

Pour commencer à créer des expériences partagées dans Unity, essayez les Démarrages rapides de 5 minutes d' <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Unity spatiales Azure Unity</a>.

Une fois que vous êtes opérationnel avec les ancres spatiales Azure, vous pouvez <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">créer et localiser des ancres dans Unity</a>.

## <a name="see-also"></a>Voir aussi
* [Échelle de l’expérience](coordinate-systems.md#mixed-reality-experience-scales)
* [Étape spatiale](coordinate-systems.md#stage-frame-of-reference)
* [Suivi des pertes dans Unity](tracking-loss-in-unity.md)
* [Ancres spatiales](spatial-anchors.md)
* [Persistance dans Unity](persistence-in-unity.md)
* [Expériences partagées dans Unity](shared-experiences-in-unity.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>
* <a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Kit de développement logiciel (SDK) d’ancre spatiale Azure pour Unity</a>