---
title: Point de regard
description: Le point de regard est un moyen principal pour les utilisateurs de cibler les hologrammes que votre application crée en réalité mixte.
author: thetuvix
ms.author: yoyoz
ms.date: 03/21/2018
ms.topic: article
keywords: oeil-point de regard, point de regard, Unity, hologramme, réalité mixte
ms.openlocfilehash: 43e643bac00e3c889b14000331d2ed95014fdcc5
ms.sourcegitcommit: ff330a7e36e5ff7ae0e9a08c0e99eb7f3f81361f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70122041"
---
# <a name="head-gaze-in-unity"></a>Tête-pointage dans Unity

Le point de [regard](gaze.md) est un moyen principal pour les utilisateurs de cibler les [hologrammes](hologram.md) que votre application crée en [réalité mixte](mixed-reality.md).


## <a name="implementing-head-gaze"></a>Implémentation de la tête en regard

D’un point de vue conceptuel, le regard de la [tête](gaze.md) est implémenté en projetant un rayon à partir de la tête de l’utilisateur où le casque est, dans la direction vers l’avant et en déterminant ce que ce rayon entre en conflit. Dans Unity, la position et la direction de l’en-tête de l’utilisateur sont exposées via l' [appareil photo](camera-in-unity.md)Unity principal, en particulier [UnityEngine. Camera. main](http://docs.unity3d.com/ScriptReference/Camera-main.html). [transformez. Forward](http://docs.unity3d.com/ScriptReference/Transform-forward.html) et [UnityEngine. Camera. main](http://docs.unity3d.com/ScriptReference/Camera-main.html). [transformation. position](http://docs.unity3d.com/ScriptReference/Transform-position.html).

L’appel de [physique. RayCast](http://docs.unity3d.com/ScriptReference/Physics.Raycast.html) génère une structure [RaycastHit](http://docs.unity3d.com/ScriptReference/RaycastHit.html) qui contient des informations sur la collision, y compris le point 3D dans lequel une collision s’est produite et l’autre gameobject le rayon de la tête de regard.

### <a name="example-implement-head-gaze"></a>Exemple : Implémenter l’en-tête

```cs
void Update()
{
       RaycastHit hitInfo;
       if (Physics.Raycast(
               Camera.main.transform.position,
               Camera.main.transform.forward,
               out hitInfo,
               20.0f,
               Physics.DefaultRaycastLayers))
       {
           // If the Raycast has succeeded and hit a hologram
           // hitInfo's point represents the position being gazed at
           // hitInfo's collider GameObject represents the hologram being gazed at
       }
}
```

### <a name="best-practices"></a>Bonnes pratiques

Bien que l’exemple ci-dessus montre comment effectuer un raycast unique dans une boucle de mise à jour pour trouver la cible sur laquelle pointe l’utilisateur, il est recommandé de le faire dans un seul objet gérant le point de vue de la tête au lieu de le faire dans un objet potentiellement intéressé par le obje Je suis en regard. Cela permet à votre application de sauvegarder le traitement en n’exécutant qu’une seule tête de regard raycast chaque cadre.

## <a name="visualizing-head-gaze"></a>Visualisation de l’en-tête

Tout comme sur le bureau où vous utilisez un pointeur de souris pour cibler et interagir avec le contenu, vous devez implémenter un [curseur](cursors.md) qui représente le point de regard de l’utilisateur. Cela permet à l’utilisateur de faire confiance à ce qu’il est en train d’interagir avec.

## <a name="head-gaze-in-the-mixed-reality-toolkit-v2"></a>Tête-pointage dans la réalité mixte Toolkit v2
Vous pouvez accéder au point de regard du [Gestionnaire d’entrée](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html) dans MRTK v2.

## <a name="see-also"></a>Voir aussi
* [Appareil photo](camera-in-unity.md)
* [Curseurs](cursors.md)
* [Entrée en regard](gaze.md)
* [Pointage du regard](gaze-targeting.md)
