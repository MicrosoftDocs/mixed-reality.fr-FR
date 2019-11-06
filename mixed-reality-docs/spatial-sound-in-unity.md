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
# <a name="spatial-sound-in-unity"></a><span data-ttu-id="f1e84-104">Son spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="f1e84-104">Spatial Sound in Unity</span></span>

<span data-ttu-id="f1e84-105">Cette page contient des liens vers des ressources qui vous aideront à utiliser et à concevoir avec Microsoft HRTF Spatializer dans vos projets de réalité mixte Unity.</span><span class="sxs-lookup"><span data-stu-id="f1e84-105">This page links to resources to help you use and design with the Microsoft HRTF spatializer in your Unity mixed reality projects.</span></span>

## <a name="enable-spatialization"></a><span data-ttu-id="f1e84-106">Activer Spatialization</span><span class="sxs-lookup"><span data-stu-id="f1e84-106">Enable spatialization</span></span>

<span data-ttu-id="f1e84-107">Activez le **Spatializer MS HRTF** dans les paramètres audio de votre projet.</span><span class="sxs-lookup"><span data-stu-id="f1e84-107">Enable the **MS HRTF Spatializer** in your project's audio settings.</span></span> <span data-ttu-id="f1e84-108">Pour plus d’informations, consultez la [documentation Spatializer de Unity](https://docs.unity3d.com/Manual/VRAudioSpatializer.html).</span><span class="sxs-lookup"><span data-stu-id="f1e84-108">For more details, see [Unity's spatializer documentation](https://docs.unity3d.com/Manual/VRAudioSpatializer.html).</span></span> 

<span data-ttu-id="f1e84-109">Attachez une **source audio** à un objet de la hiérarchie et activez Spatialization en activant la case à cocher **activer Spatialization** et en déplaçant le curseur de **lissage spatial** sur « 1 ».</span><span class="sxs-lookup"><span data-stu-id="f1e84-109">Attach an **Audio Source** to an object in the hierarchy, and enable spatialization by checking the **Enable spatialization** checkbox and moving the **Spatial Blend** slider to '1'.</span></span> <span data-ttu-id="f1e84-110">Pour plus d’informations, consultez [la documentation sur la source audio de Unity](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html).</span><span class="sxs-lookup"><span data-stu-id="f1e84-110">For more details, see [Unity's audio source documentation](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html).</span></span> 

## <a name="design-with-spatialization"></a><span data-ttu-id="f1e84-111">Conception avec Spatialization</span><span class="sxs-lookup"><span data-stu-id="f1e84-111">Design with spatialization</span></span>

### <a name="distance-based-attenuation"></a><span data-ttu-id="f1e84-112">Atténuation basée sur la distance</span><span class="sxs-lookup"><span data-stu-id="f1e84-112">Distance-based attenuation</span></span>
<span data-ttu-id="f1e84-113">La dégradation basée sur les distances par défaut d’Unity a une distance minimale de 1 mètre et une distance maximale de 500 mètres, avec un Rolloff logarithmique.</span><span class="sxs-lookup"><span data-stu-id="f1e84-113">Unity's default distance-based decay has a minimum distance of 1 meter and a maximum distance of 500 meters, with a logarithmic rolloff.</span></span> <span data-ttu-id="f1e84-114">Cela peut fonctionner pour votre scénario, ou vous pouvez constater que les sources s’atténuent trop rapidement ou trop lentement.</span><span class="sxs-lookup"><span data-stu-id="f1e84-114">This may work for your scenario, or you may find sources attenuate too quickly or too slowly.</span></span> <span data-ttu-id="f1e84-115">Pour plus d’informations sur [la](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html) définition de ces courbes dans Unity, consultez [conception de sons en réalité mixte](spatial-sound-design.md) pour obtenir les paramètres recommandés pour les courbes de dégradation des distances.</span><span class="sxs-lookup"><span data-stu-id="f1e84-115">See [sound design in mixed reality](spatial-sound-design.md) for recommended settings for distance decay curves, and see [Unity's audio source documentation](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html) for information on setting these curves in Unity.</span></span>

### <a name="environment"></a><span data-ttu-id="f1e84-116">Environment</span><span class="sxs-lookup"><span data-stu-id="f1e84-116">Environment</span></span>
<span data-ttu-id="f1e84-117">Le **Spatializer MS HRTF** comprend un composant de réverbération de salle avec [quatre paramètres de réverbération](https://docs.microsoft.com/windows/win32/api/hrtfapoapi/ne-hrtfapoapi-hrtfenvironment) et un « petit » comme valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="f1e84-117">The **MS HRTF Spatializer** includes a room reverb component with [four reverb settings](https://docs.microsoft.com/windows/win32/api/hrtfapoapi/ne-hrtfapoapi-hrtfenvironment) and a default of 'small'.</span></span> <span data-ttu-id="f1e84-118">Le paramètre de la salle peut être modifié par programmation pour chaque source audio en joignant le script C# suivant à chaque objet dans Unity qui a une source audio spatiale :</span><span class="sxs-lookup"><span data-stu-id="f1e84-118">The room setting can be changed programmatically for each audio source by attaching the following C# script to each object in Unity that has a spatialized Audio Source:</span></span>

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

## <a name="unity-spatial-sound-examples"></a><span data-ttu-id="f1e84-119">Exemples de sons spatiaux Unity</span><span class="sxs-lookup"><span data-stu-id="f1e84-119">Unity spatial sound examples</span></span>
<span data-ttu-id="f1e84-120">La boîte à outils de réalité mixte (MRTK) comprend des exemples de façons d’appliquer des effets audio en réalité mixte : les [démonstrations MRTK](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.Examples/Demos/Audio).</span><span class="sxs-lookup"><span data-stu-id="f1e84-120">The Mixed Reality Toolkit (MRTK) includes examples of ways to apply audio effects in mixed reality: [MRTK demos](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.Examples/Demos/Audio).</span></span>

