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
# <a name="using-the-windows-namespace-with-unity-apps-for-hololens"></a><span data-ttu-id="171ab-104">Utilisation de l’espace de noms Windows avec les applications Unity pour HoloLens</span><span class="sxs-lookup"><span data-stu-id="171ab-104">Using the Windows namespace with Unity apps for HoloLens</span></span>

<span data-ttu-id="171ab-105">Cette page explique comment utiliser les API WinRT dans votre projet Unity pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="171ab-105">This page describes how to make use of WinRT APIs in your Unity project for HoloLens.</span></span>

## <a name="conditionally-include-winrt-api-calls"></a><span data-ttu-id="171ab-106">Inclure de manière conditionnelle les appels d’API WinRT</span><span class="sxs-lookup"><span data-stu-id="171ab-106">Conditionally include WinRT API calls</span></span>

<span data-ttu-id="171ab-107">Les API WinRT peuvent être exploitées pour les projets Unity conçus pour l’plateforme Windows universelle et la plateforme Xbox One. tout code que vous écrivez dans des scripts Unity qui ciblent des API WinRT doit être inclus de manière conditionnelle pour les builds uniquement.</span><span class="sxs-lookup"><span data-stu-id="171ab-107">WinRT APIs can be leveraged for Unity projects built for the Universal Windows Platform and Xbox One platform; any code that you write in Unity scripts that target WinRT APIs must be conditionally included for only those builds.</span></span> 

<span data-ttu-id="171ab-108">Pour ce faire, vous pouvez effectuer deux étapes dans Unity:</span><span class="sxs-lookup"><span data-stu-id="171ab-108">This can be done via two steps in Unity:</span></span>
1) <span data-ttu-id="171ab-109">Le niveau de compatibilité de l’API doit être défini sur **.net 4,6** ou **.NET standard 2,0** dans les paramètres du lecteur</span><span class="sxs-lookup"><span data-stu-id="171ab-109">API compatibility level must be set to **.NET 4.6** or **.NET Standard 2.0** in the player settings</span></span>
    - <span data-ttu-id="171ab-110">**Modifier** >     les paramètresduprojetniveau > de compatibilité de l’API de configuration vers .net 4,6 ou .NET standard 2,0 >  > </span><span class="sxs-lookup"><span data-stu-id="171ab-110">**Edit** > **Project Settings** > **Player** > **Configuration** > **Api Compatibility Level** to **.NET 4.6** or **.NET Standard 2.0**</span></span>
2) <span data-ttu-id="171ab-111">La directive de préprocesseur **ENABLE_WINMD_SUPPORT** doit être entourée de tout code utilisant WinRT</span><span class="sxs-lookup"><span data-stu-id="171ab-111">The preprocessor directive **ENABLE_WINMD_SUPPORT** must be wrapped around any WinRT-leveraged code</span></span>

<span data-ttu-id="171ab-112">L’extrait de code suivant provient de la page manuelle Unity pour [plateforme Windows universelle: API WinRT dans C# les](http://docs.unity3d.com/Manual/windowsstore-scripts.html)scripts.</span><span class="sxs-lookup"><span data-stu-id="171ab-112">The following code snippet is from the Unity manual page for [Universal Windows Platform: WinRT API in C# scripts](http://docs.unity3d.com/Manual/windowsstore-scripts.html).</span></span> <span data-ttu-id="171ab-113">Dans cet exemple, un ID de publicité est retourné, mais uniquement sur UWP et Xbox One builds:</span><span class="sxs-lookup"><span data-stu-id="171ab-113">In this example, an advertising ID is returned, but only on UWP and Xbox One builds:</span></span>

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

## <a name="edit-your-scripts-in-a-unity-c-project"></a><span data-ttu-id="171ab-114">Modifier vos scripts dans un projet C# Unity</span><span class="sxs-lookup"><span data-stu-id="171ab-114">Edit your scripts in a Unity C# project</span></span>

<span data-ttu-id="171ab-115">Lorsque vous double-cliquez sur un script dans l’éditeur Unity, le script est lancé par défaut dans un projet de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="171ab-115">When you double-click a script in the Unity editor, it will by default launch your script in an editor project.</span></span> <span data-ttu-id="171ab-116">Les API WinRT semblent être inconnues, car le projet Visual Studio ne fait pas référence à l’Windows Runtime.</span><span class="sxs-lookup"><span data-stu-id="171ab-116">The WinRT APIs will appear to be unknown because the Visual Studio project does not reference the Windows Runtime.</span></span> <span data-ttu-id="171ab-117">En outre, la directive **ENALBE_WINMD_SUPPORT** sera non définie et tout *#if* code encapsulé sera ignoré jusqu’à ce que vous génériez votre projet dans une solution Visual Studio UWP.</span><span class="sxs-lookup"><span data-stu-id="171ab-117">Further, the **ENALBE_WINMD_SUPPORT** directive will be undefined and any *#if* wrapped code will be ignored until you build your project into a UWP Visual Studio solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="171ab-118">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="171ab-118">See also</span></span>
* [<span data-ttu-id="171ab-119">Exportation et création de solutions Unity Visual Studio</span><span class="sxs-lookup"><span data-stu-id="171ab-119">Exporting and building a Unity Visual Studio solution</span></span>](exporting-and-building-a-unity-visual-studio-solution.md)
* [<span data-ttu-id="171ab-120">Unity support Windows Runtime</span><span class="sxs-lookup"><span data-stu-id="171ab-120">Windows Runtime Support Unity</span></span>](https://docs.unity3d.com/Manual/IL2CPP-WindowsRuntimeSupport.html)