---
title: Son spatial dans Unity
description: Lit le son spatial qui provient d’un point 3D spécifique dans votre scène Unity.
author: kegodin
ms.author: kegodin
ms.date: 11/07/2019
ms.topic: article
keywords: Unity, son spatial, HRTF, taille de la salle
ms.openlocfilehash: c96717d9df9b89fbb09f0b4466ee3a9bf5c8a149
ms.sourcegitcommit: 2e54d0aff91dc31aa0020c865dada3ae57ae0ffc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73641077"
---
# <a name="spatial-sound-in-unity"></a>Son spatial dans Unity

Cette page contient des liens vers des ressources qui vous aideront à utiliser et à concevoir avec Microsoft HRTF Spatializer dans vos projets de réalité mixte Unity.

## <a name="enable-spatialization"></a>Activer Spatialization

Activez le **Spatializer MS HRTF** dans les paramètres audio de votre projet. Pour plus d’informations, consultez la [documentation Spatializer de Unity](https://docs.unity3d.com/Manual/VRAudioSpatializer.html). 

Attachez une **source audio** à un objet de la hiérarchie et activez Spatialization en activant la case à cocher **activer Spatialization** et en déplaçant le curseur de **lissage spatial** sur « 1 ». Pour plus d’informations, consultez [la documentation sur la source audio de Unity](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html). 

## <a name="design-with-spatialization"></a>Conception avec Spatialization

### <a name="distance-based-attenuation"></a>Atténuation basée sur la distance
La dégradation basée sur les distances par défaut d’Unity a une distance minimale de 1 mètre et une distance maximale de 500 mètres, avec un Rolloff logarithmique. Cela peut fonctionner pour votre scénario, ou vous pouvez constater que les sources s’atténuent trop rapidement ou trop lentement. Pour plus d’informations sur [la](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html) définition de ces courbes dans Unity, consultez [conception de sons en réalité mixte](spatial-sound-design.md) pour obtenir les paramètres recommandés pour les courbes de dégradation des distances.

### <a name="environment"></a>Environment
Le **Spatializer MS HRTF** comprend un composant de réverbération de salle avec [quatre paramètres de réverbération](https://docs.microsoft.com/windows/win32/api/hrtfapoapi/ne-hrtfapoapi-hrtfenvironment) et un « petit » comme valeur par défaut. Le paramètre de la salle peut être modifié par programmation pour chaque source audio en joignant le script C# suivant à chaque objet dans Unity qui a une source audio spatiale :

```cs
using UnityEngine;
   using System.Collections;
   public class SetHRTF : MonoBehaviour    {
       public enum ROOMSIZE { Small, Medium, Large, None };
       public ROOMSIZE room = ROOMSIZE.Small;  // Small is regarded as the "most average"
       // defaults and docs from MSDN
       // https://msdn.microsoft.com/library/windows/desktop/mt186602(v=vs.85).aspx
       AudioSource audiosource;
       void Awake()
       {
           audiosource = this.gameObject.GetComponent<AudioSource>();
           if (audiosource == null)
           {
               print("SetHRTFParams needs an audio source to do anything.");
               return;
           }
           audiosource.spatialize = 1; // we DO want spatialized audio
           audiosource.spread = 0; // we dont want to reduce our angle of hearing
           audiosource.spatialBlend = 1;   // we do want to hear spatialized audio
           audiosource.SetSpatializerFloat(1, (float)room);    // 1 is the roomsize param
       }
   }
```

## <a name="unity-spatial-sound-examples"></a>Exemples de sons spatiaux Unity
La boîte à outils de réalité mixte (MRTK) comprend des exemples de façons d’appliquer des effets audio en réalité mixte : les [démonstrations MRTK](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.Examples/Demos/Audio).

