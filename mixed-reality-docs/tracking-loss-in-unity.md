---
title: Suivi de la perte dans Unity
description: Gestion du suivi de la perte d’une application Unity.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, suivi de la perte, l’image de la perte de suivi
ms.openlocfilehash: eb675860d67e9cad0d1129b3a6f61343990a4179
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595716"
---
# <a name="tracking-loss-in-unity"></a>Suivi de la perte dans Unity

Lorsque l’appareil ne peut pas localiser lui-même dans le monde, l’application rencontre « perte de suivi ». Par défaut, Unity s’interrompre la boucle de mise à jour et afficher une image de démarrage à l’utilisateur. Lorsque le suivi est récupéré, l’image de démarrage disparaît et continue la boucle de mise à jour.

Comme alternative, l’utilisateur peut gérer manuellement cette transition en n’optant pas le paramètre. Tout le contenu vous sembleront pour devenir corps verrouillés pendant le suivi de la perte si rien n’est fait pour le gérer.

## <a name="default-handling"></a>La gestion par défaut

Par défaut, la boucle de mise à jour de l’application, ainsi que tous les messages et les événements s’arrête pendant la durée de suivi de la perte. À ce moment même, une image sera affichée à l’utilisateur. Vous pouvez personnaliser cette image en accédant à modifier -> Paramètres -> lecteur, en cliquant sur Image de démarrage et définition de l’image holographique suivi de la perte.

## <a name="manual-handling"></a>Gestion manuelle

Pour gérer manuellement une perte de suivi, vous devez accéder à **modifier** > **paramètres du projet** > **Player**  >   **Onglet Paramètres de plateforme de Windows Universal** > **Image de démarrage** > **Windows HOLOGRAPHIQUE** et décochez la case « sur le suivi des pertes Pause et afficher l’Image ". Après quoi, vous devez gérer le suivi des modifications avec les API spécifiées ci-dessous.

**Namespace :** *UnityEngine.XR.WSA*<br>
**Type :** *WorldManager*

* World Manager expose un événement pour détecter le suivi perdu/acquise (*WorldManager.OnPositionalLocatorStateChanged*) et une propriété pour interroger l’état actuel (*WorldManager.state*)
* Lorsque l’état de suivi n’est pas actif, l’appareil photo n’apparaîtra pas traduire dans le monde virtuel, même si l’utilisateur est traduit. Cela signifie que les objets ne sont plus correspond à n’importe quel emplacement physique et tous apparaissent corps verrouillé.

Lors du traitement de suivi des modifications sur votre propre vous devez soit pour l’interrogation de la propriété state chaque frame ou la poignée de la *OnPositionalLocatorStateChanged* événement.

### <a name="polling"></a>Interrogation

L’état plus importantes est *PositionalLocatorState.Active* ce qui signifie que le suivi est entièrement fonctionnels. N’importe quel autre état entraînent uniquement les deltas de rotation de la caméra principale. Exemple :

```cs
void Update()
{
    switch (UnityEngine.XR.WSA.WorldManager.state)
    {
        case PositionalLocatorState.Active:
            // handle active
            break;
        case PositionalLocatorState.Activating:
        case PositionalLocatorState.Inhibited:
        case PositionalLocatorState.OrientationOnly:
        case PositionalLocatorState.Unavailable:
        default:
            // only rotational information is available
            break;
    }
}
```

### <a name="handling-the-onpositionallocatorstatechanged-event"></a>Gestion de l’événement OnPositionalLocatorStateChanged

Vous pouvez également et plus facilement, vous pouvez également vous abonner à *OnPositionalLocatorStateChanged* pour gérer les transitions :

```cs
void Start()
{
    UnityEngine.XR.WSA.WorldManager.OnPositionalLocatorStateChanged += WorldManager_OnPositionalLocatorStateChanged;
}

private void WorldManager_OnPositionalLocatorStateChanged(PositionalLocatorState oldState, PositionalLocatorState newState)
{
    if (newState == PositionalLocatorState.Active)
    {
        // Handle becoming active
    }
    else
    {
        // Handle becoming rotational only
    }
}
```

## <a name="see-also"></a>Voir aussi
* [Gérer le suivi de la perte dans DirectX](coordinate-systems-in-directx.md#handling-tracking-loss)
