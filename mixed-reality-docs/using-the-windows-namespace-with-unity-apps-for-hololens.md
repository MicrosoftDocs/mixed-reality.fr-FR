---
title: Utilisation de l’espace de noms Windows avec les applications Unity pour HoloLens
description: Explique comment utiliser les API WinRT dans votre projet Unity pour HoloLens.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, WinRT, Windows Mixed Reality, API, procédure pas à pas
ms.openlocfilehash: fd25548de8eeb3c8157a3f9de283dc5004ed1180
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63548739"
---
# <a name="using-the-windows-namespace-with-unity-apps-for-hololens"></a>Utilisation de l’espace de noms Windows avec les applications Unity pour HoloLens

Cette page explique comment utiliser les API WinRT dans votre projet Unity pour HoloLens.

## <a name="conditionally-include-winrt-api-calls"></a>Inclure de manière conditionnelle les appels d’API WinRT

Les API WinRT peuvent être exploitées pour les projets Unity conçus pour l’plateforme Windows universelle et la plateforme Xbox One. tout code que vous écrivez dans des scripts Unity qui ciblent des API WinRT doit être inclus de manière conditionnelle pour les builds uniquement. 

Pour ce faire, vous pouvez effectuer deux étapes dans Unity:
1) Le niveau de compatibilité de l’API doit être défini sur **.net 4,6** ou **.NET standard 2,0** dans les paramètres du lecteur
    - **Modifier** >     les paramètresduprojetniveau > de compatibilité de l’API de configuration vers .net 4,6 ou .NET standard 2,0 >  > 
2) La directive de préprocesseur **ENABLE_WINMD_SUPPORT** doit être entourée de tout code utilisant WinRT

L’extrait de code suivant provient de la page manuelle Unity pour [plateforme Windows universelle: API WinRT dans C# les](http://docs.unity3d.com/Manual/windowsstore-scripts.html)scripts. Dans cet exemple, un ID de publicité est retourné, mais uniquement sur UWP et Xbox One builds:

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

Lorsque vous double-cliquez sur un script dans l’éditeur Unity, le script est lancé par défaut dans un projet de l’éditeur. Les API WinRT semblent être inconnues, car le projet Visual Studio ne fait pas référence à l’Windows Runtime. En outre, la directive **ENALBE_WINMD_SUPPORT** sera non définie et tout *#if* code encapsulé sera ignoré jusqu’à ce que vous génériez votre projet dans une solution Visual Studio UWP.

## <a name="see-also"></a>Voir aussi
* [Exportation et création de solutions Unity Visual Studio](exporting-and-building-a-unity-visual-studio-solution.md)
* [Unity support Windows Runtime](https://docs.unity3d.com/Manual/IL2CPP-WindowsRuntimeSupport.html)