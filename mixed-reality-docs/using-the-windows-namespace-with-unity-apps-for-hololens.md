---
title: À l’aide de l’espace de noms Windows avec les applications Unity pour HoloLens
description: Explique comment utiliser les APIs WinRT dans votre projet Unity pour HoloLens.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Procédure pas à pas de Unity, WinRT, windows réalité mixte, API,
ms.openlocfilehash: ed65b5995d74c54057a49b878c1206d0f06394ca
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594174"
---
# <a name="using-the-windows-namespace-with-unity-apps-for-hololens"></a>À l’aide de l’espace de noms Windows avec les applications Unity pour HoloLens

Cette page explique comment utiliser les APIs WinRT dans votre projet Unity pour HoloLens.

## <a name="conditionally-include-winrt-api-calls"></a>Inclure les appels d’API de WinRT de façon conditionnelle

WinRT APIs servira uniquement dans les générations de projet Unity qui ciblent Windows 8, Windows 8.1 ou la plateforme Windows universelle ; tout code que vous écrivez dans les scripts Unity qui cible WinRT APIs doit être inclus pour uniquement ces builds de manière conditionnelle. Cette opération est effectuée à l’aide de définitions de préprocesseur NETFX_CORE ou WINDOWS_UWP. Cette règle s’applique à l’aide des instructions, ainsi que tout autre code.

L’extrait de code suivant provient de la page du manuel Unity pour [plateforme Windows universelle : Les API WinRT dans C# scripts](http://docs.unity3d.com/Manual/windowsstore-scripts.html). Dans cet exemple, un ID de publicité est retourné, mais uniquement sur Windows 8.0 ou supérieur cible builds :

```
using UnityEngine;
public class WinRTAPI : MonoBehaviour {
    void Update() {
        auto adId = GetAdvertisingId();
        // ...
    }

    string GetAdvertisingId() {
        #if NETFX_CORE
            return Windows.System.UserProfile.AdvertisingManager.AdvertisingId;
        #else
            return "";
        #endif
    }
}
```

## <a name="edit-your-scripts-in-a-unity-c-project"></a>Modifier vos scripts dans un Unity C# projet

Lorsque vous double-cliquez sur un script dans l’éditeur Unity, il sera par défaut lancer votre script dans un projet de l’éditeur. Les APIs WinRT semblent être inconnu pour deux raisons : NETFX_CORE n’est pas défini dans cet environnement, et le projet ne référence pas l’exécution de Windows. Si vous utilisez le [recommandé d’exportation et créé des paramètres](exporting-and-building-a-unity-visual-studio-solution.md)et modifier les scripts dans le projet au lieu de cela, il sera définir NETFX_CORE et également inclure une référence à l’exécution de Windows ; avec cette configuration en place, WinRT APIs seront disponibles pour IntelliSense.

Notez que votre Unity C# projet peut également servir à déboguer dans vos scripts en utilisant F5 dans Visual Studio de débogage à distance. Si vous ne voyez pas IntelliSense fonctionne de la première fois que vous ouvrez votre Unity C# de projet, fermez le projet et rouvrez-le. IntelliSense doit commencer à fonctionner.

## <a name="see-also"></a>Voir aussi
* [Exportation et création d’une solution de Unity Visual Studio](exporting-and-building-a-unity-visual-studio-solution.md)
