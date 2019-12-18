---
title: Son spatial dans Unity
description: Lire le son spatial à partir d’un point 3D spécifique dans votre scène Unity.
author: kegodin
ms.author: kegodin
ms.date: 11/07/2019
ms.topic: article
keywords: Unity, son spatial, HRTF, taille de la salle
ms.openlocfilehash: 3e7d0ea231545d5112d182dffbc02f217ca4a4a7
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75181989"
---
# <a name="spatial-sound-in-unity"></a>Son spatial dans Unity

Cette page contient des liens vers des ressources pour le son spatial dans Unity.

## <a name="spatializer-options"></a>Options de Spatializer
Les options Spatializer pour les applications de réalité mixte sont les suivantes :
* *Spatializer MS HRTF*. Unity fournit cela dans le cadre du package facultatif *Windows Mixed Reality* .
  * Cela s’exécute sur le processeur dans une architecture à source unique à coût plus élevé.
  * Elle est fournie à des fins de compatibilité descendante avec les applications HoloLens d’origine.
* *Microsoft Spatializer*. Celui-ci est disponible à partir du [dépôt github Microsoft Spatializer](https://github.com/microsoft/spatialaudio-unity).
  * Cela utilise une architecture à plusieurs sources moins onéreuse.
  * Sur HoloLens 2, cette valeur est déchargée sur un accélérateur matériel.

Pour les nouvelles applications, nous vous recommandons *Microsoft Spatializer*.

## <a name="enable-spatialization"></a>Activer Spatialization

Utilisez [NuGet pour Unity](https://github.com/GlitchEnzo/NuGetForUnity/releases/latest) pour installer _Microsoft. SpatialAudio. Spatializer. Unity_ et choisissez **Microsoft Spatializer** dans les paramètres audio de votre projet. Alors :
* Attacher une **source audio** à un objet dans la hiérarchie
* Cochez la case **Enable Spatialization**
* Déplacez le curseur de **lissage spatial** sur « 1 »

Pour plus de détails, voir:
* [Dépôt GitHub Microsoft Spatializer](https://github.com/microsoft/spatialaudio-unity)
* [Didacticiel Spatializer de Microsoft](unity-spatial-audio-ch1.md)
* [Documentation de la source audio de Unity](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html)
* [Documentation Spatializer de Unity](https://docs.unity3d.com/Manual/VRAudioSpatializer.html)

## <a name="distance-based-attenuation"></a>Atténuation basée sur la distance
La dégradation basée sur les distances par défaut d’Unity a une distance minimale de 1 mètre et une distance maximale de 500 mètres, avec un Rolloff logarithmique. Ces paramètres peuvent fonctionner pour votre scénario, ou vous pouvez constater que les sources s’atténuent trop rapidement ou trop lentement. Pour plus de détails, voir:
* [Conception audio en réalité mixte](spatial-sound-design.md) pour les paramètres recommandés.
* [Documentation de la source audio de Unity](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html) pour obtenir des instructions sur la définition de ces courbes.

## <a name="reverb"></a>Réverbération
Le _Spatializer Microsoft_ désactive les effets postérieurs à Spatializer par défaut. Pour activer la réverbération et d’autres effets pour les sources spatiales :
* Attacher le composant de niveau d’envoi de l' **effet de salle** à chaque source
* Ajustez la courbe de niveau d’envoi pour chaque source, afin de contrôler le gain sur le son renvoyé au graphique pour le traitement des effets

Pour plus d’informations, consultez [le chapitre 5 du didacticiel Spatializer](unity-spatial-audio-ch5.md) .

## <a name="unity-spatial-sound-examples"></a>Exemples de sons spatiaux Unity
Pour obtenir des exemples de son spatial dans Unity, consultez :
* [Démonstrations MRTK](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.Examples/Demos/Audio)
* [Exemple de projet Microsoft Spatializer](https://github.com/microsoft/spatialaudio-unity/tree/master/Samples/MicrosoftSpatializerSample)

## <a name="next-steps"></a>Étapes suivantes
* [Conception audio en réalité mixte](spatial-sound-design.md)
* [Didacticiel Spatializer de Microsoft](unity-spatial-audio-ch1.md)

