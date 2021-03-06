---
title: Point de focus dans Unity
description: Réglage manuel de la stabilité des hologrammes dans Unity en définissant le point de focus
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, point de focalisation, plan de focalisation, plan de stabilisation, point de stabilisation, reprojection, LSR, tampon de profondeur
ms.openlocfilehash: 9a7f30b552242b24a9a7b260b6574690a27d2c1d
ms.sourcegitcommit: 7e8b9de561cbc8483e84511f3e9cbd779f3a999f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/27/2019
ms.locfileid: "75502620"
---
# <a name="focus-point-in-unity"></a>Point de focus dans Unity

**Espace de noms :** *UnityEngine. XR. WSA*<br>
**Type**: *HolographicSettings*

Le [point de focus](hologram-stability.md#reprojection) peut être défini pour fournir à HoloLens une indication sur la façon d’effectuer la meilleure stabilisation sur les hologrammes actuellement affichés.

Si vous souhaitez définir le point de focus dans Unity, vous devez définir chaque frame à l’aide de *HolographicSettings. SetFocusPointForFrame ()* . Si le point de focus n’est pas défini pour un frame, le plan de stabilisation par défaut est utilisé.

> [!NOTE]
> Par défaut, l’option « Activer le partage de tampon de profondeur » est définie pour les nouveaux projets Unity.  Avec cette option, une application Unity s’exécutant sur un casque de bureau immersif ou sur un HoloLens exécutant la mise à jour 2018 d’avril de Windows 10 (RS4) ou une version ultérieure envoie votre tampon de profondeur à Windows pour optimiser la stabilité de l’hologramme automatiquement, sans que votre application spécifie un point de Focus :
> * Sur un casque d’un bureau immersif, cela permet une reprojection basée sur la profondeur par pixel.
> * Sur un HoloLens exécutant la mise à jour 2018 de Windows 10 avril ou une version ultérieure, le tampon de profondeur est analysé afin de choisir un plan de stabilisation optimal automatiquement.
>
> L’une ou l’autre approche devrait offrir une meilleure qualité d’image sans travail explicite de votre application pour sélectionner un point de focus pour chaque frame.  Notez que si vous fournissez un point de focalisation manuellement, cela remplacera le comportement automatique décrit ci-dessus et réduira généralement la stabilité de l’hologramme.  En règle générale, vous devez uniquement spécifier un point de focus manuel lorsque votre application s’exécute sur un HoloLens qui n’a pas encore été mis à jour vers la mise à jour 2018 d’avril de Windows 10.

### <a name="example"></a>Exemple

Il existe de nombreuses façons de définir le point de focus, comme suggéré par les surcharges disponibles sur la fonction statique *SetFocusPointForFrame* . Vous trouverez ci-dessous un exemple simple pour définir le plan de focus sur l’objet fourni pour chaque frame :

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

Notez que le code simple ci-dessus peut finir par réduire la stabilité des hologrammes si l’objet ayant le focus se termine derrière l’utilisateur.  C’est la raison pour laquelle vous devez généralement définir « activer le partage de mémoire tampon de profondeur » au lieu de spécifier manuellement un point de focus.

### <a name="see-also"></a>Articles associés
* [Plan de stabilisation](hologram-stability.md#reprojection)
