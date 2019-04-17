---
title: Son spatial dans Unity
description: Lecture d’un son spatial provient d’un point en 3D spécifique au sein de votre scène Unity.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, son spatial, HRTF, taille de la pièce
ms.openlocfilehash: e2b321d7086314a14a940d57aa17e67636c758b8
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593231"
---
# <a name="spatial-sound-in-unity"></a>Son spatial dans Unity

Cette rubrique décrit comment utiliser le son de Spatial dans vos projets Unity. Il couvre les fichiers de plug-in requis ainsi que les composants de Unity et les propriétés qui permettent son de Spatial.

## <a name="enabling-spatial-sound-in-unity"></a>L’activation de son Spatial dans Unity

Spatial son, dans Unity, est activé à l’aide d’un plug-in spatial audio. Les fichiers de plug-in sont regroupées directement dans Unity, par conséquent, l’activation de son spatial est aussi simple que va **Modifier > Paramètres du projet > Audio** et en modifiant le **plug-in spatial** dans l’inspecteur pour les  **MS HRTF spatial**. Dans la mesure où le spatial Microsoft uniquement Hz 48000 prend actuellement en charge, vous devez également définir votre taux d’échantillonnage système à 48000 afin d’éviter un échec HRTF dans les rares cas que votre périphérique de sortie du système n’est pas déjà définie sur 48000 :

![Inspecteur pour AudioManager](images/audio-250px.png)<br>
*Inspecteur pour AudioManager*

Votre projet Unity est maintenant configuré pour utiliser le son de Spatial.

>[!NOTE]
>Si vous n’utilisez pas un PC Windows 10 pour le développement, vous n’obtiendrez Spatial son dans l’éditeur, ni sur l’appareil (même si vous utilisez le SDK Windows 10).

## <a name="using-spatial-sound-in-unity"></a>À l’aide de son Spatial dans Unity

Spatial son est utilisé dans votre projet Unity en ajustant les trois paramètres sur vos composants de la Source de données Audio. Les étapes suivantes va configurer les composants de votre Source de données Audio Spatial audio.
* Dans le **hiérarchie** du panneau, sélectionnez l’objet de jeu qui a un attaché **Audio Source**.
* Dans le **inspecteur** panneau, sous la **Audio Source** composant
    * Vérifier le **Spatialize** option.
    * Définissez **Blend Spatial** à **3D** (valeur numérique 1).
    * Pour de meilleurs résultats, développez **les paramètres audio 3D** et définissez **Volume écrêtage** à **personnalisé écrêtage**.

![Panneau Inspecteur dans Unity affichant la Source Audio](images/audiosource.png)<br>
*Panneau Inspecteur dans Unity affichant la Source Audio*

Votre sons réaliste existent maintenant dans l’environnement de votre projet !

Il est fortement recommandé de vous familiariser avec la [les instructions de conception Spatial son](spatial-sound-design.md). Ces instructions permettent d’intégrer votre audio en toute transparence dans votre projet et à plonger davantage vos utilisateurs dans l’expérience que vous avez créé.

## <a name="setting-spatial-sound-settings"></a>Définition des paramètres de son Spatial

Le plug-in Microsoft Spatial Sound fournit un paramètre supplémentaire qui peut être défini, dans une application par Source Audio, pour permettre un contrôle supplémentaire de la simulation audio. Ce paramètre est la taille de la salle simulée.

### <a name="room-size"></a>Taille de la pièce

La taille de salle de conversation est simulée par Spatial son. La taille approximative des salles est ; petite (un bureau à une salle de conférence petit), moyenne (une grande salle de conférence) et de grande taille (un auditorium). Vous pouvez également spécifier une taille de la pièce None pour simuler un environnement extérieur. La taille de la valeur par défaut est petite.

### <a name="example"></a>Exemple

Le MixedRealityToolkit pour Unity fournit une classe statique qui rend la configuration des paramètres Spatial son facile. Cette classe peut être trouvée dans le [MixedRealityToolkit\SpatialSound dossier](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialSound) et peut être appelée à partir de n’importe quel script dans votre projet. Il est recommandé de définir ces paramètres sur chaque composant de Source de données Audio dans votre projet. L’exemple suivant montre la sélection de la taille de la moyenne pour une Source Audio liée.

```cs
AudioSource audioSource = gameObject.GetComponent<AudioSource>()

if (audioSource != null) {
    SpatialSoundSettings.SetRoomSize(audioSource, SpatialMappingRoomSizes.Medium);
}
```

### <a name="directly-accessing-parameters-from-unity"></a>En accédant directement aux paramètres à partir d’Unity

Si vous ne souhaitez pas utiliser les outils de l’Audio excellents dans la MixedRealityToolkit, voici comment vous pouvez modifier les paramètres de HRTF. Vous pouvez copier/coller cela dans un script appelé *SetHRTF.cs* que vous souhaitez attacher à chaque AudioSource HRTF. Il vous permet de modifier des paramètres importants pour HRTF.

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
### <a name="spatial-sound-in-mixed-reality-toolkit"></a>Son spatial dans le Kit de ressources de réalité mixte
- [HoloToolkit-Examples/SpatialSound/Scenes/UAudioManagerTest.unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpatialSound/Scenes/UAudioManagerTest.unity)

Les exemples suivants à partir de la boîte à outils de réalité mixte sont des exemples généraux effet audio qui illustrent des façons de rendre votre expérience plus riche à l’aide de son.
- [HoloToolkit-Examples/SpatialSound/Scenes/AudioLoFiTest.unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpatialSound/Scenes/AudioLoFiTest.unity)
- [HoloToolkit-Examples/SpatialSound/Scenes/AudioOcclusionTest.unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpatialSound/Scenes/AudioOcclusionTest.unity)

## <a name="see-also"></a>Voir aussi
* [Son spatial](spatial-sound.md)
* [Sonorisation spatiale](spatial-sound-design.md)
