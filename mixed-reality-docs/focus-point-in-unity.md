---
title: Point de focus dans Unity
description: Régler manuellement la stabilité hologramme dans Unity en définissant le point de focus
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, point de focus, plan de focus, plan de stabilisation, point de stabilisation, reprojection, LSR, mémoire tampon de profondeur
ms.openlocfilehash: 0f43c37df66ecada86dcb309fcd58d822f0f3481
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597037"
---
# <a name="focus-point-in-unity"></a>Point de focus dans Unity

**Namespace :** *UnityEngine.XR.WSA*<br>
**Type** : *HolographicSettings*

Le [concentrer point](hologram-stability.md#stabilization-plane) peut être définie sur fournir HoloLens un indicateur sur comment effectuer au mieux stabilisation sur les hologrammes actuellement en cours affiche.

Si vous souhaitez définir le Point de Focus dans Unity, il doit être définie à chaque image en utilisant le *HolographicSettings.SetFocusPointForFrame()*. Si le Point de Focus n’est pas défini pour un frame, le plan de stabilisation par défaut sera utilisé.

> [!NOTE]
> Par défaut, nouveaux projets de Unity ont l’option « Activer le partage de mémoire tampon profondeur » définie.  Avec cette option, une application Unity s’exécutant sur un casque immersif de bureau ou un HoloLens exécutant Windows 10 avril 2018 mise à jour (RS4) ou plus tard votre mémoire tampon de profondeur à Windows pour optimiser la stabilité hologramme automatiquement, sans spécifier de votre application envoie un point de focus :
> * Sur un casque bureau immersif, cela permettra reprojection en fonction de profondeur de par pixel.
> * Sur un HoloLens exécutant Windows 10 avril 2018 mettre à jour ou une version ultérieure, cette analyse le tampon de profondeur pour choisir un plan de stabilisation optimal automatiquement.
>
> Chacune de ces approches doit fournir encore meilleure qualité d’image sans travail explicite par votre application pour sélectionner un point de focus chaque frame.  Notez que si vous fournissez manuellement un point de focus, qui remplacera le comportement automatique décrit ci-dessus et permet généralement de réduire la stabilité hologramme.  En règle générale, vous devez spécifier un point de mise au point manuelle uniquement lorsque votre application s’exécute sur un HoloLens n’a pas encore été mis à jour pour les fenêtres de mettre à jour du 10 avril 2018.

### <a name="example"></a>Exemple

Il existe plusieurs façons de définir le Point de Focus, comme suggéré par les surcharges disponibles sur le *SetFocusPointForFrame* fonction statique. Présentée ci-dessous est un exemple simple de définir le plan de focus à l’objet fourni chaque frame :

```cs
public GameObject focusedObject;
void Update()
{
    // Normally the normal is best set to be the opposite of the main camera's 
    // forward vector.
    // If the content is actually all on a plane (like text), set the normal to 
    // the normal of the plane and ensure the user does not pass through the 
    // plane.
    var normal = -Camera.main.transform.forward;     
    var position = focusedObject.transform.position;
    UnityEngine.XR.WSA.HolographicSettings.SetFocusPointForFrame(position, normal);
}
```

Notez que le simple code ci-dessus peut retrouver en réduisant la stabilité hologramme si l’objet ayant le focus se retrouve derrière l’utilisateur.  C’est pourquoi vous devez généralement définir « Activer le partage de mémoire tampon de profondeur » au lieu de spécifier manuellement un point de focus.

### <a name="see-also"></a>Voir aussi
* [Plan de stabilisation](hologram-stability.md#stabilization-plane)
