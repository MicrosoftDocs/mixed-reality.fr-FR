---
title: API WinRT avec Unity pour HoloLens
description: Explique comment utiliser les API WinRT (l’espace de noms Windows) dans votre projet Unity pour HoloLens.
author: mikeriches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, WinRT, Windows Mixed Reality, API, procédure pas à pas
ms.openlocfilehash: 80f950d7571a936e93eb08490ad83dbb34a50b3a
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81277987"
---
# <a name="winrt-apis-with-unity-for-hololens"></a><span data-ttu-id="6f046-104">API WinRT avec Unity pour HoloLens</span><span class="sxs-lookup"><span data-stu-id="6f046-104">WinRT APIs with Unity for HoloLens</span></span>

<span data-ttu-id="6f046-105">Cette page explique comment utiliser les API WinRT dans votre projet Unity pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="6f046-105">This page describes how to make use of WinRT APIs in your Unity project for HoloLens.</span></span>

## <a name="mixed-reality-apis"></a><span data-ttu-id="6f046-106">API de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="6f046-106">Mixed Reality APIs</span></span>

<span data-ttu-id="6f046-107">Un sous-ensemble axé sur la réalité mixte du SDK Windows a été mis à disposition dans une projection .NET Standard compatible 2,0, que vous pouvez utiliser dans votre projet sans les directives de préprocesseur.</span><span class="sxs-lookup"><span data-stu-id="6f046-107">A Mixed Reality focused subset of the Windows SDK has been made available in a .NET Standard 2.0 compatible projection, which you can use in your project without preprocessor directives.</span></span> <span data-ttu-id="6f046-108">Cela inclut la plupart des API dans les espaces de noms Windows. perception et Windows. UI. Input. spatial, et peut se développer pour inclure des API supplémentaires à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="6f046-108">This includes most APIs in the Windows.Perception and Windows.UI.Input.Spatial namespaces, and may expand to include additional APIs in the future.</span></span> <span data-ttu-id="6f046-109">Les API projetées peuvent être utilisées lors de l’exécution dans l’éditeur, ce qui permet l’utilisation du [mode de lecture](https://docs.microsoft.com//windows/mixed-reality/unity-play-mode).</span><span class="sxs-lookup"><span data-stu-id="6f046-109">The projected APIs can be used while running in the Editor, which enables the use of [Play Mode](https://docs.microsoft.com//windows/mixed-reality/unity-play-mode).</span></span> <span data-ttu-id="6f046-110">Pour utiliser cette projection, apportez les modifications suivantes à votre projet :</span><span class="sxs-lookup"><span data-stu-id="6f046-110">To use this projection, make the following modifications to your project:</span></span>

1) <span data-ttu-id="6f046-111">Ajoutez une référence au package NuGet [Microsoft. Windows. MixedReality. DotNetWinRT](https://www.nuget.org/packages/Microsoft.Windows.MixedReality.DotNetWinRT) à l’aide [de NuGet pour Unity](https://github.com/GlitchEnzo/NuGetForUnity).</span><span class="sxs-lookup"><span data-stu-id="6f046-111">Add a reference to the [Microsoft.Windows.MixedReality.DotNetWinRT](https://www.nuget.org/packages/Microsoft.Windows.MixedReality.DotNetWinRT) NuGet package using [NuGet for Unity](https://github.com/GlitchEnzo/NuGetForUnity).</span></span>
2) <span data-ttu-id="6f046-112">Préfixez les références à l’espace de noms `Windows` avec `Microsoft.`:</span><span class="sxs-lookup"><span data-stu-id="6f046-112">Prefix references to the `Windows` namespace with `Microsoft.`:</span></span>
```cs
using namespace Microsoft.Windows.Perception.Spatial;
```
3) <span data-ttu-id="6f046-113">Remplacez les casts de pointeur natifs par `FromNativePtr`:</span><span class="sxs-lookup"><span data-stu-id="6f046-113">Replace native pointer casts with `FromNativePtr`:</span></span>
```cs
var worldOrigin = SpatialCoordinateSystem.FromNativePtr(unityWorldOriginPtr);
```

## <a name="conditionally-include-winrt-api-calls"></a><span data-ttu-id="6f046-114">Inclure de manière conditionnelle les appels d’API WinRT</span><span class="sxs-lookup"><span data-stu-id="6f046-114">Conditionally include WinRT API calls</span></span>

<span data-ttu-id="6f046-115">Vous pouvez également tirer parti des API WinRT pour les projets Unity conçus pour le plateforme Windows universelle et la plateforme Xbox One à l’aide de directives de préprocesseur. tout code que vous écrivez dans des scripts Unity qui ciblent des API WinRT doit être inclus de manière conditionnelle pour les builds uniquement.</span><span class="sxs-lookup"><span data-stu-id="6f046-115">Alternatively, WinRT APIs can be leveraged for Unity projects built for the Universal Windows Platform and Xbox One platform by using preprocessor directives; any code that you write in Unity scripts that target WinRT APIs must be conditionally included for only those builds.</span></span> 

<span data-ttu-id="6f046-116">Pour ce faire, vous pouvez effectuer deux étapes dans Unity :</span><span class="sxs-lookup"><span data-stu-id="6f046-116">This can be done via two steps in Unity:</span></span>
1) <span data-ttu-id="6f046-117">Le niveau de compatibilité de l’API doit être défini sur **.net 4,6** ou **.NET standard 2,0** dans les paramètres du lecteur</span><span class="sxs-lookup"><span data-stu-id="6f046-117">API compatibility level must be set to **.NET 4.6** or **.NET Standard 2.0** in the player settings</span></span>
    - <span data-ttu-id="6f046-118">**Modifier** > **paramètres du projet** > **Player** > **configuration** > niveau de compatibilité de l' **API** sur **.net 4,6** ou **.NET standard 2,0**</span><span class="sxs-lookup"><span data-stu-id="6f046-118">**Edit** > **Project Settings** > **Player** > **Configuration** > **Api Compatibility Level** to **.NET 4.6** or **.NET Standard 2.0**</span></span>
2) <span data-ttu-id="6f046-119">La directive de préprocesseur **ENABLE_WINMD_SUPPORT** doit être entourée de tout code utilisant WinRT</span><span class="sxs-lookup"><span data-stu-id="6f046-119">The preprocessor directive **ENABLE_WINMD_SUPPORT** must be wrapped around any WinRT-leveraged code</span></span>

<span data-ttu-id="6f046-120">L’extrait de code suivant provient de la page manuelle Unity pour [plateforme Windows universelle : API C# WinRT dans les scripts](https://docs.unity3d.com/Manual/windowsstore-scripts.html).</span><span class="sxs-lookup"><span data-stu-id="6f046-120">The following code snippet is from the Unity manual page for [Universal Windows Platform: WinRT API in C# scripts](https://docs.unity3d.com/Manual/windowsstore-scripts.html).</span></span> <span data-ttu-id="6f046-121">Dans cet exemple, un ID de publicité est retourné, mais uniquement sur UWP et Xbox One builds :</span><span class="sxs-lookup"><span data-stu-id="6f046-121">In this example, an advertising ID is returned, but only on UWP and Xbox One builds:</span></span>

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

## <a name="edit-your-scripts-in-a-unity-c-project"></a><span data-ttu-id="6f046-122">Modifier vos scripts dans un projet C# Unity</span><span class="sxs-lookup"><span data-stu-id="6f046-122">Edit your scripts in a Unity C# project</span></span>

<span data-ttu-id="6f046-123">Lorsque vous double-cliquez sur un script dans l’éditeur Unity, le script est lancé par défaut dans un projet de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="6f046-123">When you double-click a script in the Unity editor, it will by default launch your script in an editor project.</span></span> <span data-ttu-id="6f046-124">Les API WinRT semblent être inconnues, car le projet Visual Studio ne fait pas référence à l’Windows Runtime.</span><span class="sxs-lookup"><span data-stu-id="6f046-124">The WinRT APIs will appear to be unknown because the Visual Studio project does not reference the Windows Runtime.</span></span> <span data-ttu-id="6f046-125">En outre, la directive **ENABLE_WINMD_SUPPORT** sera non définie et tout code encapsulé *#if* sera ignoré jusqu’à ce que vous génériez votre projet dans une solution Visual Studio UWP.</span><span class="sxs-lookup"><span data-stu-id="6f046-125">Further, the **ENABLE_WINMD_SUPPORT** directive will be undefined and any *#if* wrapped code will be ignored until you build your project into a UWP Visual Studio solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="6f046-126">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6f046-126">See also</span></span>
* [<span data-ttu-id="6f046-127">Exportation et création de solutions Unity Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f046-127">Exporting and building a Unity Visual Studio solution</span></span>](exporting-and-building-a-unity-visual-studio-solution.md)
* [<span data-ttu-id="6f046-128">Unity support Windows Runtime</span><span class="sxs-lookup"><span data-stu-id="6f046-128">Windows Runtime Support Unity</span></span>](https://docs.unity3d.com/Manual/IL2CPP-WindowsRuntimeSupport.html)
