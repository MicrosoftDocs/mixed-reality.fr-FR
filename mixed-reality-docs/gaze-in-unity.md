---
title: Les regards dans Unity
description: Regards est un moyen principal pour les utilisateurs à cibler les hologrammes que votre application crée en réalité mixte.
author: thetuvix
ms.author: yoyoz
ms.date: 03/21/2018
ms.topic: article
keywords: regards, unity, HOLOGRAMME, réalité mixte
ms.openlocfilehash: b2cc86db156a1e97b013e4cd6debe3abe5ffb6dd
ms.sourcegitcommit: 60060386305eabfac2758a2c861a43c36286b151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453721"
---
# <a name="head-gaze-in-unity"></a>Head regards dans Unity

[Utilisation](gaze.md) est un moyen principal pour les utilisateurs à cibler le [vntana](hologram.md) votre application crée dans [réalité mixte](mixed-reality.md).


## <a name="implementing-head-gaze"></a>Implémentation des regards principal

Conceptuellement, [les regards](gaze.md) est implémentée en projetant un rayon à partir de la tête de l’utilisateur où le casque est, dans la direction avant qu’ils sont accessibles et déterminer ce que ray est en conflit avec. Dans Unity, position principal de l’utilisateur et la direction sont exposées via les principaux Unity [caméra](camera-in-unity.md), plus précisément [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[ Transform.Forward](http://docs.unity3d.com/ScriptReference/Transform-forward.html) et [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[ Transform.position](http://docs.unity3d.com/ScriptReference/Transform-position.html).

Appel [Physics.RayCast](http://docs.unity3d.com/ScriptReference/Physics.Raycast.html) entraîne une [RaycastHit](http://docs.unity3d.com/ScriptReference/RaycastHit.html) structure qui contient des informations sur la collision, y compris le point 3D où collision s’est produite et autres GameObject le rayon du pointage de regard entrent en conflit avec.

### <a name="example-implement-head-gaze"></a>Exemple : Implémentez des regards principal

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

### <a name="best-practices"></a>Meilleures pratiques

Tandis que l’exemple ci-dessus montre comment effectuer un raycast unique dans une boucle de mise à jour pour rechercher la cible du pointage de regard, il est recommandé d’effectuer cette opération dans un seul objet de la gestion des regards au lieu de cela dans n’importe quel objet qui est potentiellement intéressé par l’objet en cours gazed à. Cela permet à votre application d’enregistrer le traitement en procédant comme seul regards raycast chaque frame.

## <a name="visualizing-gaze"></a>Visualisation du pointage de regard

Tout comme sur le bureau où vous utilisez un pointeur de la souris pour cibler et interagir avec du contenu, vous devez implémenter un [curseur](cursors.md) qui représente le regard de l’utilisateur. Cela donne la confiance des utilisateurs dans ce que sur le point d’interagir avec elles.

## <a name="gaze-in-mixed-reality-toolkit-v2"></a>Utilisation en réalité mixte Toolkit v2
Vous pouvez accéder à des regards à partir de la [d’entrée Manager](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html) dans MRTK v2.

## <a name="see-also"></a>Voir aussi
* [Appareil photo](camera-in-unity.md)
* [Entrée des regards](gaze.md)
* [Curseurs](cursors.md)
* [Pointage du regard](gaze-targeting.md)
