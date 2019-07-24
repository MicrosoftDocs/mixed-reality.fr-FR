---
title: Son spatial dans Unity
description: Lit le son spatial qui provient d’un point 3D spécifique dans votre scène Unity.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, son spatial, HRTF, taille de la salle
ms.openlocfilehash: e2b321d7086314a14a940d57aa17e67636c758b8
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63549080"
---
# <a name="spatial-sound-in-unity"></a>Son spatial dans Unity

Cette rubrique explique comment utiliser un son spatial dans vos projets Unity. Il couvre les fichiers de plug-in requis, ainsi que les composants et les propriétés Unity qui permettent le son spatial.

## <a name="enabling-spatial-sound-in-unity"></a>Activation du son spatial dans Unity

Le son spatial, dans Unity, est activé à l’aide d’un plug-in audio Spatializer. Les fichiers de plug-in sont regroupés directement dans Unity, de sorte que l’activation du son spatial est aussi facile que la **modification > paramètres du projet > l’audio** et la modification du **plug-in Spatializer** dans l’inspecteur par le **Spatializer MS HRTF**. Étant donné que Microsoft Spatializer prend uniquement en charge 48000Hz, vous devez également définir le taux d’échantillonnage du système sur 48000 pour éviter un échec HRTF dans le cas rare où votre périphérique de sortie système n’est pas déjà défini sur 48000:

![Inspector pour AudioManager](images/audio-250px.png)<br>
*Inspector pour AudioManager*

Votre projet Unity est maintenant configuré pour utiliser un son spatial.

>[!NOTE]
>Si vous n’utilisez pas un PC Windows 10 pour le développement, vous n’obtiendrez pas de son spatial dans l’éditeur ni sur l’appareil (même si vous utilisez le kit de développement logiciel (SDK) Windows 10).

## <a name="using-spatial-sound-in-unity"></a>Utilisation du son spatial dans Unity

Le son spatial est utilisé dans votre projet Unity en ajustant trois paramètres sur vos composants sources audio. Les étapes suivantes vous permettront de configurer vos composants de source audio pour le son spatial.
* Dans le panneau **hiérarchie** , sélectionnez l’objet de jeu qui a une **source audio**attachée.
* Dans le panneau **inspecteur** , sous le composant **audio source**
    * Vérifiez l’option **spatial** .
    * Définissez **spatial Blend** sur **3D** (valeur numérique 1).
    * Pour de meilleurs résultats, développez **paramètres audio 3D** et définissez **volume Rolloff** sur **personnalisé Rolloff**.

![Panneau de l’inspecteur dans Unity présentant la source audio](images/audiosource.png)<br>
*Panneau de l’inspecteur dans Unity présentant la source audio*

Vos sons sont désormais réalistes dans l’environnement de votre projet.

Il est fortement recommandé de vous familiariser avec les [instructions de conception de son spatial](spatial-sound-design.md). Ces instructions vous aident à intégrer votre audio en toute transparence dans votre projet et à plonger vos utilisateurs dans l’expérience que vous avez créée.

## <a name="setting-spatial-sound-settings"></a>Définition des paramètres de son spatial

Le plug-in de son spatial Microsoft fournit un paramètre supplémentaire qui peut être défini, en fonction de la source audio, pour permettre un contrôle supplémentaire de la simulation audio. Ce paramètre correspond à la taille de la salle simulée.

### <a name="room-size"></a>Taille de la salle

Taille de la salle qui est simulée par son spatial. La taille approximative des salles est; petite (un bureau à une petite salle de conférence), moyen (une grande salle de conférence) et grand (un auditorium). Vous pouvez également spécifier une taille de salle nulle pour simuler un environnement extérieur. La taille de la salle par défaut est petite.

### <a name="example"></a>Exemple

Le MixedRealityToolkit pour Unity fournit une classe statique qui facilite la définition des paramètres de son spatial. Cette classe se trouve dans le [dossier MixedRealityToolkit\SpatialSound](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialSound) et peut être appelée à partir de n’importe quel script de votre projet. Il est recommandé de définir ces paramètres sur chaque composant de la source audio dans votre projet. L’exemple suivant illustre la sélection de la taille de la salle moyenne pour une source audio attachée.

```cs
AudioSource audioSource = gameObject.GetComponent<AudioSource>()

if (audioSource != null) {
    SpatialSoundSettings.SetRoomSize(audioSource, SpatialMappingRoomSizes.Medium);
}
```

### <a name="directly-accessing-parameters-from-unity"></a>Accès direct aux paramètres d’Unity

Si vous ne souhaitez pas utiliser les excellents outils audio dans le MixedRealityToolkit, voici comment modifier les paramètres HRTF. Vous pouvez le copier/coller dans un script appelé *SetHRTF.cs* que vous souhaitez attacher à chaque audiosource HRTF. Elle vous permet de modifier les paramètres importants en HRTF.

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
### <a name="spatial-sound-in-mixed-reality-toolkit"></a>Son spatial dans la réalité mixte Toolkit
- [HoloToolkit-Examples/SpatialSound/scenes/UAudioManagerTest. Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpatialSound/Scenes/UAudioManagerTest.unity)

Les exemples suivants de la boîte à outils de la réalité mixte sont des exemples d’effets audio généraux qui montrent comment rendre votre expérience plus immersive en utilisant le son.
- [HoloToolkit-Examples/SpatialSound/scenes/AudioLoFiTest. Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpatialSound/Scenes/AudioLoFiTest.unity)
- [HoloToolkit-Examples/SpatialSound/scenes/AudioOcclusionTest. Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpatialSound/Scenes/AudioOcclusionTest.unity)

## <a name="see-also"></a>Voir aussi
* [Son spatial](spatial-sound.md)
* [Conception du son spatial](spatial-sound-design.md)
