---
title: API WinRT avec Unity pour HoloLens
description: Explique comment utiliser les API WinRT (l’espace de noms Windows) dans votre projet Unity pour HoloLens.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, WinRT, Windows Mixed Reality, API, procédure pas à pas
ms.openlocfilehash: 73764d191813f6dcae750e74ce3181af987c9e0e
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437233"
---
# <a name="winrt-apis-with-unity-for-hololens"></a>API WinRT avec Unity pour HoloLens

Cette page explique comment utiliser les API WinRT dans votre projet Unity pour HoloLens.

## <a name="mixed-reality-apis"></a>API de réalité mixte

Un sous-ensemble axé sur la réalité mixte du SDK Windows a été mis à disposition dans une projection .NET Standard compatible 2,0, que vous pouvez utiliser dans votre projet sans les directives de préprocesseur. Cela inclut la plupart des API dans les espaces de noms Windows. perception et Windows. UI. Input. spatial, et peut se développer pour inclure des API supplémentaires à l’avenir. Les API projetées peuvent être utilisées lors de l’exécution dans l’éditeur, ce qui permet l’utilisation du [mode de lecture](https://docs.microsoft.com//windows/mixed-reality/unity-play-mode). Pour utiliser cette projection, apportez les modifications suivantes à votre projet :

1) Ajoutez une référence au package NuGet [Microsoft. Windows. MixedReality. DotNetWinRT](https://www.nuget.org/packages/Microsoft.Windows.MixedReality.DotNetWinRT) à l’aide [de NuGet pour Unity](https://github.com/GlitchEnzo/NuGetForUnity).
2) Préfixez les références à l’espace de noms `Windows` avec `Microsoft.`:
```cs
using namespace Microsoft.Windows.Perception.Spatial;
```
3) Remplacez les casts de pointeur natifs par `FromNativePtr`:
```cs
var worldOrigin = SpatialCoordinateSystem.FromNativePtr(unityWorldOriginPtr);
```

## <a name="conditionally-include-winrt-api-calls"></a>Inclure de manière conditionnelle les appels d’API WinRT

Vous pouvez également tirer parti des API WinRT pour les projets Unity conçus pour le plateforme Windows universelle et la plateforme Xbox One à l’aide de directives de préprocesseur. tout code que vous écrivez dans des scripts Unity qui ciblent des API WinRT doit être inclus de manière conditionnelle pour les builds uniquement. 

Pour ce faire, vous pouvez effectuer deux étapes dans Unity :
1) Le niveau de compatibilité de l’API doit être défini sur **.net 4,6** ou **.NET standard 2,0** dans les paramètres du lecteur
    - **Modifier** > **paramètres du projet** > **Player** > **configuration** > niveau de compatibilité de l' **API** sur **.net 4,6** ou **.NET standard 2,0**
2) La directive de préprocesseur **ENABLE_WINMD_SUPPORT** doit être entourée de tout code utilisant WinRT

L’extrait de code suivant provient de la page manuelle Unity pour [plateforme Windows universelle : API C# WinRT dans les scripts](https://docs.unity3d.com/Manual/windowsstore-scripts.html). Dans cet exemple, un ID de publicité est retourné, mais uniquement sur UWP et Xbox One builds :

```
using UnityEngine;
public class WinRTAPI : MonoBehaviour {
    void Update() {
        auto adId = GetAdvertisingId();
        // ...
    }

    string GetAdvertisingId() {
        #if ENABLE_WINMD_SUPPORT
            return Windows.System.UserProfile.AdvertisingManager.AdvertisingId;
        #else
            return "";
        #endif
    }
}
```

## <a name="edit-your-scripts-in-a-unity-c-project"></a>Modifier vos scripts dans un projet C# Unity

Lorsque vous double-cliquez sur un script dans l’éditeur Unity, le script est lancé par défaut dans un projet de l’éditeur. Les API WinRT semblent être inconnues, car le projet Visual Studio ne fait pas référence à l’Windows Runtime. En outre, la directive **ENABLE_WINMD_SUPPORT** sera non définie et tout *#if* code encapsulé sera ignoré jusqu’à ce que vous génériez votre projet dans une solution Visual Studio UWP.

## <a name="see-also"></a>Articles associés
* [Exportation et création de solutions Unity Visual Studio](exporting-and-building-a-unity-visual-studio-solution.md)
* [Unity support Windows Runtime](https://docs.unity3d.com/Manual/IL2CPP-WindowsRuntimeSupport.html)
