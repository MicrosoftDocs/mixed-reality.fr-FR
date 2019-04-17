---
title: Les regards dans Unity
description: Regards est un moyen principal pour les utilisateurs à cibler les hologrammes que votre application crée en réalité mixte.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: regards, unity, HOLOGRAMME, réalité mixte
ms.openlocfilehash: 09915479a9eef95c5ce4533371e113ab6191a331
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597005"
---
# <a name="gaze-in-unity"></a>Les regards dans Unity

[Utilisation](gaze.md) est un moyen principal pour les utilisateurs à cibler le [vntana](hologram.md) votre application crée dans [une réalité mixte](mixed-reality.md).

## <a name="implementing-gaze"></a>Implémentation du pointage de regard

Conceptuellement, [les regards](gaze.md) est implémentée en projetant un rayon à partir de la tête de l’utilisateur où le casque est, dans la direction avant qu’ils sont accessibles et déterminer ce que ray est en conflit avec. Dans Unity, position principal de l’utilisateur et la direction sont exposées via les principaux Unity [caméra](camera-in-unity.md), plus précisément [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[ Transform.Forward](http://docs.unity3d.com/ScriptReference/Transform-forward.html) et [UnityEngine.Camera.main](http://docs.unity3d.com/ScriptReference/Camera-main.html).[ Transform.position](http://docs.unity3d.com/ScriptReference/Transform-position.html).

Appel [Physics.RayCast](http://docs.unity3d.com/ScriptReference/Physics.Raycast.html) entraîne une [RaycastHit](http://docs.unity3d.com/ScriptReference/RaycastHit.html) structure qui contient des informations sur la collision, y compris le point 3D où collision s’est produite et autres GameObject le rayon du pointage de regard entrent en conflit avec.

### <a name="example-implement-gaze"></a>Exemple : Implémentez regards

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

## <a name="gaze-in-mixed-reality-toolkit"></a>Utilisation dans le Kit de ressources de réalité mixte
Lorsque vous importez [MRTK publie des packages de Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases) ou cloner le projet à partir de la [référentiel GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity), vous vous apprêtez à trouver un nouveau menu « Toolkit de réalité mixte » dans Unity. Sous le menu « Configurer », vous verrez le menu « Application des paramètres de scène réalité mixte ». Lorsque vous cliquez dessus, il supprime l’appareil photo par défaut et ajoute les composants fondamentaux - [InputManager](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/InputManager.prefab), [MixedRealityCameraParent](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/MixedRealityCameraParent.prefab), et [DefaultCursor](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor/DefaultCursor.prefab).

![Menu MRTK pour le programme d’installation de scène](images/MRTK_Input_Menu.png)<br>
*Menu MRTK pour le programme d’installation de scène*

![Programme d’installation automatique de scène dans MRTK](images/MRTK_HowTo_Input1.png)<br>
*Programme d’installation automatique de scène dans MRTK*

### <a name="gaze-related-scripts-in-mixed-reality-toolkit"></a>Utilisation des scripts associés dans le Kit de ressources de réalité mixte
Mixte réalité la boîte à outils inclut des InputManager prefab [GazeManager.cs](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Gaze/GazeManager.cs) et [les regards de stabilisation](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Gaze/GazeStabilizer.cs). Sous [SimpleSinglePointerSelector](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Focus/SimpleSinglePointerSelector.cs), vous pouvez assigner votre curseur personnalisé. Par défaut, animée [DefaultCursor](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor/DefaultCursor.prefab) est affecté.

[Cursor.prefab](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor) et [CursorWithFeedback.prefab](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor) vous montre comment visualiser votre regard sur l’utilisation de curseurs.

## <a name="see-also"></a>Voir aussi
* [Appareil photo](camera-in-unity.md)
* [Gaze](gaze.md)
* [Curseurs](cursors.md)
* [Ciblage des regards](gaze-targeting.md)
