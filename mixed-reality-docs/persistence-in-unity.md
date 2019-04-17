---
title: Persistance dans Unity
description: Persistance permet aux utilisateurs d’épingler hologrammes individuels ou un espace de travail, où qu’ils veulent et puis recherchez il où qu’elles attendent de plusieurs utilise de votre application.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: HoloLens, persistance, Unity
ms.openlocfilehash: b6a67e52b3a5ce724a90eb1a479c5eda74b0c4cb
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597116"
---
# <a name="persistence-in-unity"></a>Persistance dans Unity

**Namespace :** *UnityEngine.XR.WSA.Persistence*<br>
**Classe :** *WorldAnchorStore*

Le WorldAnchorStore est essentiel à la création d’expériences HOLOGRAPHIQUE où hologrammes restent dans les positions du monde réel spécifique entre les instances de l’application. Vous pouvez ainsi vos utilisateurs épinglent hologrammes individuels ou un espace de travail, où qu’ils le souhaitent il et ensuite les retrouver ultérieurement où qu’elles attendent sur nombreuses utilisations de votre application.

## <a name="how-to-persist-holograms-across-sessions"></a>Comment conserver hologrammes entre les sessions

Le WorldAnchorStore permettent de conserver l’emplacement de WorldAnchor entre les sessions. Pour conserver réellement hologrammes entre les sessions, vous devrez effectuer séparément le suivi de votre GameObjects qui utilisent un point d’ancrage du monde particulier. Il est souvent judicieux pour créer une racine GameObject avec un point d’ancrage du monde et avoir des enfants hologrammes ancrée par celui-ci avec un décalage de position local.

Pour charger hologrammes provenant des sessions précédentes :
1. Obtenir le WorldAnchorStore
2. Charger des données d’application sur le point d’ancrage du monde qui vous donne l’id de l’ancrage du monde
3. Charger un point d’ancrage du monde entier à partir de son id

Pour enregistrer les hologrammes pour les sessions ultérieures :
1. Obtenir le WorldAnchorStore
2. Enregistrer un point d’ancrage du monde spécifiant un id
3. Enregistrer les données relatives à l’ancrage du monde avec un id d’application

### <a name="getting-the-worldanchorstore"></a>Obtention de la WorldAnchorStore

Nous souhaitons conserver une référence à la WorldAnchorStore autour donc nous savons que nous sommes prêts à exécuter une fois que nous souhaitons effectuer une opération. S’agissant d’un appel asynchrone, potentiellement dès le début, nous voulons appeler

```
WorldAnchorStore.GetAsync(StoreLoaded);
```

Dans ce cas, StoreLoaded est notre gestionnaire pour lorsque le WorldAnchorStore le chargement est terminé :

```
private void StoreLoaded(WorldAnchorStore store)
{
       this.store = store;
}
```

Nous disposons désormais d’une référence à la WorldAnchorStore que nous utiliserons pour enregistrer et charger les ancres monde spécifique.

### <a name="saving-a-worldanchor"></a>L’enregistrement d’un WorldAnchor

Pour enregistrer, nous devons simplement nommer nous enregistrez et transmettez-le dans le WorldAnchor soulevées avant lorsque vous souhaitez enregistrer. Remarque : la tentative d’enregistrement de deux points d’ancrage à la même chaîne échoue (magasin. Enregistrer retournera la valeur false). Vous devez supprimer l’enregistrement précédent avant d’enregistrer une nouvelle :

```
private void SaveGame()
{
       // Save data about holograms positioned by this world anchor
       if (!this.savedRoot) // Only Save the root once
       {
              this.savedRoot = this.store.Save("rootGameObject", anchor);
              Assert(this.savedRoot);
       }
}
```

### <a name="loading-a-worldanchor"></a>Le chargement d’un WorldAnchor

Et à charger :

```
private void LoadGame()
{
       // Save data about holograms positioned by this world anchor
       this.savedRoot = this.store.Load("rootGameObject", rootGameObject);
       if (!this.savedRoot)
       {
              // We didn't actually have the game root saved! We have to re-place our objects or start over
       }
}
```

Nous pouvons en outre utiliser le magasin. Delete() pour supprimer un point d’ancrage que nous avons précédemment enregistré et store. Clear() supprimer toutes les données précédemment enregistrées.

### <a name="enumerating-existing-anchors"></a>Énumération des ancres existants

Pour découvrir les ancres précédemment stockés, appelez GetAllIds.

```
string[] ids = this.store.GetAllIds();
for (int index = 0; index < ids.Length; index++)
{
        Debug.Log(ids[index]);
}
```

## <a name="persisting-holograms-for-multiple-devices"></a>Hologrammes persistantes pour plusieurs appareils

Vous pouvez utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a> pour créer un point d’ancrage cloud durable à partir d’un WorldAnchor local, lequel votre application peut ensuite localiser dans plusieurs HoloLens, appareils iOS et Android, même si ces appareils ne sont pas présents dans le même heure.  Étant donné que les ancres cloud sont persistants, plusieurs périphériques au fil du temps peuvent chacun voir le contenu restitué par rapport à ce point d’ancrage dans le même emplacement physique.

Pour commencer à créer des expériences partagées dans Unity, essayez les 5 minutes <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Démarrages rapides Azure Spatial ancres Unity</a>.

Une fois que vous êtes en cours d’exécution ancres spatiale d’Azure, vous pouvez ensuite <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">créer et localiser les points d’ancrage dans Unity</a>.

## <a name="see-also"></a>Voir aussi
* [Persistance de l’ancre spatial](coordinate-systems.md#spatial-anchor-persistence)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Ancres Spatial Azure</a>
* <a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Ancres Spatial Azure SDK pour Unity</a>
