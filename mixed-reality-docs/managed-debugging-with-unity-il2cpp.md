---
title: Débogage managé avec Unity IL2CPP
description: Cet article explique comment exécuter un débogueur géré sur votre projet UWP IL2CPP Unity.
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: Unity, Visual Studio, débogage, il2cpp
ms.openlocfilehash: fd09c3ca1bd410c56e46eb8e8815742f87482d08
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73439630"
---
# <a name="managed-debugging-with-unity-il2cpp"></a><span data-ttu-id="08b50-104">Débogage managé avec Unity IL2CPP</span><span class="sxs-lookup"><span data-stu-id="08b50-104">Managed debugging with Unity IL2CPP</span></span>

<span data-ttu-id="08b50-105">Procédez comme suit pour attacher un débogueur géré à votre Build IL2CPP Unity.</span><span class="sxs-lookup"><span data-stu-id="08b50-105">Follow these steps to attach a managed debugger to your Unity IL2CPP UWP build.</span></span> <span data-ttu-id="08b50-106">Ce guide a été développé à l’origine pour HoloLens et HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="08b50-106">This guide was originally developed for HoloLens and HoloLens 2.</span></span>

1. <span data-ttu-id="08b50-107">Vous devez disposer d’un réseau qui prend en charge la [multidiffusion](https://en.wikipedia.org/wiki/Multicast).</span><span class="sxs-lookup"><span data-stu-id="08b50-107">You will need to be on a network that supports [multicast](https://en.wikipedia.org/wiki/Multicast).</span></span>
1. <span data-ttu-id="08b50-108">Assurez-vous que **InternetClientServer** et **PrivateNetworkClientServer** sont archivés dans Unity sous les fonctionnalités des paramètres de publication UWP.</span><span class="sxs-lookup"><span data-stu-id="08b50-108">Ensure that **InternetClientServer** and **PrivateNetworkClientServer** are checked in Unity under the UWP Publishing Settings Capabilities.</span></span>

    ![Fonctionnalités des paramètres de publication UWP](images/il2cpp-debugging-capabilities.png)

1. <span data-ttu-id="08b50-110">Configurer les paramètres de build UWP Unity :</span><span class="sxs-lookup"><span data-stu-id="08b50-110">Configure the Unity UWP build settings:</span></span>
    - <span data-ttu-id="08b50-111">Build de développement</span><span class="sxs-lookup"><span data-stu-id="08b50-111">Development Build</span></span>
    - <span data-ttu-id="08b50-112">Débogage des scripts</span><span class="sxs-lookup"><span data-stu-id="08b50-112">Script Debugging</span></span>
    - <span data-ttu-id="08b50-113">Attendre le débogueur managé (facultatif)</span><span class="sxs-lookup"><span data-stu-id="08b50-113">Wait for Managed Debugger (optional)</span></span>

    ![Paramètres de build UWP](images/il2cpp-debugging-build.png)

1. <span data-ttu-id="08b50-115">Créez dans Unity.</span><span class="sxs-lookup"><span data-stu-id="08b50-115">Build in Unity.</span></span>
1. <span data-ttu-id="08b50-116">Générez et déployez à partir de la solution Visual Studio sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="08b50-116">Build and deploy from the Visual Studio solution to your device.</span></span> <span data-ttu-id="08b50-117">Vous devez générer avec les configurations **Debug** ou **Release** .</span><span class="sxs-lookup"><span data-stu-id="08b50-117">You should build with the **Debug** or **Release** configurations.</span></span> <span data-ttu-id="08b50-118">La configuration **principale** désactive le profileur Unity et peut empêcher le débogage optimal.</span><span class="sxs-lookup"><span data-stu-id="08b50-118">The **Master** configuration disables the Unity profiler and can prevent optimal debugging.</span></span> <span data-ttu-id="08b50-119">Si vous le souhaitez, vérifiez **Internet (client & Server)** et les **réseaux privés (client & Server)** dans la liste des fonctionnalités dans package. appxmanifest dans la solution.</span><span class="sxs-lookup"><span data-stu-id="08b50-119">Optionally, verify **Internet (Client & Server)** and **Private Networks (Client & Server)** in the capabilities list in Package.appxmanifest in the solution.</span></span>
1. <span data-ttu-id="08b50-120">Démarrez l’application sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="08b50-120">Start the app on your device.</span></span> <span data-ttu-id="08b50-121">Assurez-vous que votre appareil est connecté au même réseau que votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="08b50-121">Make sure your device is connected to the same network as your PC.</span></span>
1. <span data-ttu-id="08b50-122">Assurez-vous que l’appareil **n’est pas** connecté à votre ordinateur via USB.</span><span class="sxs-lookup"><span data-stu-id="08b50-122">Make sure the device **is not** connected to your PC via USB.</span></span>
1. <span data-ttu-id="08b50-123">Accédez à la solution Visual Studio qui est créée lorsque vous double-cliquez sur un script dans Unity, où vous pouvez afficher C# et modifier vos scripts.</span><span class="sxs-lookup"><span data-stu-id="08b50-123">Go to the Visual Studio solution that's created when you double click a script in Unity, where you can view and edit your C# scripts.</span></span>
1. <span data-ttu-id="08b50-124">Debug-> attacher le débogueur Unity.</span><span class="sxs-lookup"><span data-stu-id="08b50-124">Debug -> Attach Unity Debugger.</span></span>

    ![Attacher le débogueur Unity](images/il2cpp-debugging-attach.png)

1. <span data-ttu-id="08b50-126">Sélectionnez votre appareil dans la liste et cliquez sur OK pour l’attacher.</span><span class="sxs-lookup"><span data-stu-id="08b50-126">Select your device in the list and click "OK" to attach.</span></span>

    ![Liste des appareils](images/il2cpp-debugging-machines.png)
