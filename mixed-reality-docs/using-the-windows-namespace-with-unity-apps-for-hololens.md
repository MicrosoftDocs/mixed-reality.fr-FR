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
# <a name="using-the-windows-namespace-with-unity-apps-for-hololens"></a><span data-ttu-id="1c2e2-104">À l’aide de l’espace de noms Windows avec les applications Unity pour HoloLens</span><span class="sxs-lookup"><span data-stu-id="1c2e2-104">Using the Windows namespace with Unity apps for HoloLens</span></span>

<span data-ttu-id="1c2e2-105">Cette page explique comment utiliser les APIs WinRT dans votre projet Unity pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="1c2e2-105">This page describes how to make use of WinRT APIs in your Unity project for HoloLens.</span></span>

## <a name="conditionally-include-winrt-api-calls"></a><span data-ttu-id="1c2e2-106">Inclure les appels d’API de WinRT de façon conditionnelle</span><span class="sxs-lookup"><span data-stu-id="1c2e2-106">Conditionally include WinRT API calls</span></span>

<span data-ttu-id="1c2e2-107">WinRT APIs servira uniquement dans les générations de projet Unity qui ciblent Windows 8, Windows 8.1 ou la plateforme Windows universelle ; tout code que vous écrivez dans les scripts Unity qui cible WinRT APIs doit être inclus pour uniquement ces builds de manière conditionnelle.</span><span class="sxs-lookup"><span data-stu-id="1c2e2-107">WinRT APIs will only be used in Unity project builds that target Windows 8, Windows 8.1, or the Universal Windows Platform; any code that you write in Unity scripts that targets WinRT APIs must be conditionally included for only those builds.</span></span> <span data-ttu-id="1c2e2-108">Cette opération est effectuée à l’aide de définitions de préprocesseur NETFX_CORE ou WINDOWS_UWP.</span><span class="sxs-lookup"><span data-stu-id="1c2e2-108">This is done using the NETFX_CORE or WINDOWS_UWP preprocessor definitions.</span></span> <span data-ttu-id="1c2e2-109">Cette règle s’applique à l’aide des instructions, ainsi que tout autre code.</span><span class="sxs-lookup"><span data-stu-id="1c2e2-109">This rule applies to using statements, as well as other code.</span></span>

<span data-ttu-id="1c2e2-110">L’extrait de code suivant provient de la page du manuel Unity pour [plateforme Windows universelle : Les API WinRT dans C# scripts](http://docs.unity3d.com/Manual/windowsstore-scripts.html).</span><span class="sxs-lookup"><span data-stu-id="1c2e2-110">The following code snippet is from the Unity manual page for [Universal Windows Platform: WinRT API in C# scripts](http://docs.unity3d.com/Manual/windowsstore-scripts.html).</span></span> <span data-ttu-id="1c2e2-111">Dans cet exemple, un ID de publicité est retourné, mais uniquement sur Windows 8.0 ou supérieur cible builds :</span><span class="sxs-lookup"><span data-stu-id="1c2e2-111">In this example, an advertising ID is returned, but only on Windows 8.0 or higher target builds:</span></span>

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

## <a name="edit-your-scripts-in-a-unity-c-project"></a><span data-ttu-id="1c2e2-112">Modifier vos scripts dans un Unity C# projet</span><span class="sxs-lookup"><span data-stu-id="1c2e2-112">Edit your scripts in a Unity C# project</span></span>

<span data-ttu-id="1c2e2-113">Lorsque vous double-cliquez sur un script dans l’éditeur Unity, il sera par défaut lancer votre script dans un projet de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="1c2e2-113">When you double-click a script in the Unity editor, it will by default launch your script in an editor project.</span></span> <span data-ttu-id="1c2e2-114">Les APIs WinRT semblent être inconnu pour deux raisons : NETFX_CORE n’est pas défini dans cet environnement, et le projet ne référence pas l’exécution de Windows.</span><span class="sxs-lookup"><span data-stu-id="1c2e2-114">The WinRT APIs will appear to be unknown for two reasons: NETFX_CORE is not defined in this environment, and the project does not reference the Windows Runtime.</span></span> <span data-ttu-id="1c2e2-115">Si vous utilisez le [recommandé d’exportation et créé des paramètres](exporting-and-building-a-unity-visual-studio-solution.md)et modifier les scripts dans le projet au lieu de cela, il sera définir NETFX_CORE et également inclure une référence à l’exécution de Windows ; avec cette configuration en place, WinRT APIs seront disponibles pour IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="1c2e2-115">If you use the [recommended export and built settings](exporting-and-building-a-unity-visual-studio-solution.md), and edit the scripts in that project instead, it will define NETFX_CORE and also include a reference to the Windows Runtime; with this configuration in place, WinRT APIs will be available for IntelliSense.</span></span>

<span data-ttu-id="1c2e2-116">Notez que votre Unity C# projet peut également servir à déboguer dans vos scripts en utilisant F5 dans Visual Studio de débogage à distance.</span><span class="sxs-lookup"><span data-stu-id="1c2e2-116">Note that your Unity C# project can also be used to debug through your scripts using F5 remote debugging in Visual Studio.</span></span> <span data-ttu-id="1c2e2-117">Si vous ne voyez pas IntelliSense fonctionne de la première fois que vous ouvrez votre Unity C# de projet, fermez le projet et rouvrez-le.</span><span class="sxs-lookup"><span data-stu-id="1c2e2-117">If you do not see IntelliSense working the first time that you open your Unity C# project, close the project and re-open it.</span></span> <span data-ttu-id="1c2e2-118">IntelliSense doit commencer à fonctionner.</span><span class="sxs-lookup"><span data-stu-id="1c2e2-118">IntelliSense should start working.</span></span>

## <a name="see-also"></a><span data-ttu-id="1c2e2-119">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1c2e2-119">See also</span></span>
* [<span data-ttu-id="1c2e2-120">Exportation et création d’une solution de Unity Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1c2e2-120">Exporting and building a Unity Visual Studio solution</span></span>](exporting-and-building-a-unity-visual-studio-solution.md)
