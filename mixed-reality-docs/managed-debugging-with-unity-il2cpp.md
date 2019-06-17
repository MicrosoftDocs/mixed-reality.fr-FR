---
title: Le débogage avec Unity IL2CPP managé
description: Cet article explique comment exécuter un débogueur managé sur votre projet Unity IL2CPP UWP.
author: keveleigh
ms.author: kurtie
ms.date: 06/13/19
ms.topic: article
keywords: Unity, il2cpp, de débogage de visual studio
ms.openlocfilehash: eb4655633384fcb5d7f27546134e21857e5c5502
ms.sourcegitcommit: 2f600e5ad00cd447b180b0f89192b4b9d86bbc7e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148854"
---
# <a name="managed-debugging-with-unity-il2cpp"></a><span data-ttu-id="24a8d-104">Le débogage avec Unity IL2CPP managé</span><span class="sxs-lookup"><span data-stu-id="24a8d-104">Managed debugging with Unity IL2CPP</span></span>

<span data-ttu-id="24a8d-105">Suivez ces étapes pour attacher un débogueur managé à votre build Unity IL2CPP UWP.</span><span class="sxs-lookup"><span data-stu-id="24a8d-105">Follow these steps to attach a managed debugger to your Unity IL2CPP UWP build.</span></span> <span data-ttu-id="24a8d-106">Ce guide a été développé pour HoloLens et HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="24a8d-106">This guide was originally developed for HoloLens and HoloLens 2.</span></span>

1. <span data-ttu-id="24a8d-107">Vérifiez que **InternetClientServer** et **PrivateNetworkClientServer** sont vérifiées dans Unity sous les fonctionnalités de paramètres de publication UWP.</span><span class="sxs-lookup"><span data-stu-id="24a8d-107">Ensure that **InternetClientServer** and **PrivateNetworkClientServer** are checked in Unity under the UWP Publishing Settings Capabilities.</span></span>

    ![UWP des fonctionnalités de paramètres de publication](images/il2cpp-debugging-capabilities.png)

1. <span data-ttu-id="24a8d-109">Configurez les paramètres de build Unity UWP :</span><span class="sxs-lookup"><span data-stu-id="24a8d-109">Configure the Unity UWP build settings:</span></span>
    - <span data-ttu-id="24a8d-110">Génération de développement</span><span class="sxs-lookup"><span data-stu-id="24a8d-110">Development Build</span></span>
    - <span data-ttu-id="24a8d-111">Débogage des scripts</span><span class="sxs-lookup"><span data-stu-id="24a8d-111">Script Debugging</span></span>
    - <span data-ttu-id="24a8d-112">Attendez le débogueur géré (facultatif)</span><span class="sxs-lookup"><span data-stu-id="24a8d-112">Wait for Managed Debugger (optional)</span></span>

    ![Paramètres de Build UWP](images/il2cpp-debugging-build.png)

1. <span data-ttu-id="24a8d-114">Build dans Unity.</span><span class="sxs-lookup"><span data-stu-id="24a8d-114">Build in Unity.</span></span>
1. <span data-ttu-id="24a8d-115">Générer et déployer à partir de la solution Visual Studio sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="24a8d-115">Build and deploy from the Visual Studio solution to your device.</span></span> <span data-ttu-id="24a8d-116">Vous devez créer avec le **déboguer** ou **version** configurations.</span><span class="sxs-lookup"><span data-stu-id="24a8d-116">You should build with the **Debug** or **Release** configurations.</span></span> <span data-ttu-id="24a8d-117">Le **Master** configuration désactive le profileur Unity et peut empêcher le débogage optimale.</span><span class="sxs-lookup"><span data-stu-id="24a8d-117">The **Master** configuration disables the Unity profiler and can prevent optimal debugging.</span></span> <span data-ttu-id="24a8d-118">Si vous le souhaitez, vérifiez **Internet (Client & serveur)** et **réseaux privés (Client & serveur)** dans la liste de fonctionnalités dans Package.appxmanifest dans la solution.</span><span class="sxs-lookup"><span data-stu-id="24a8d-118">Optionally, verify **Internet (Client & Server)** and **Private Networks (Client & Server)** in the capabilities list in Package.appxmanifest in the solution.</span></span>
1. <span data-ttu-id="24a8d-119">Démarrer l’application sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="24a8d-119">Start the app on your device.</span></span> <span data-ttu-id="24a8d-120">Assurez-vous que votre appareil est connecté au même réseau que votre PC.</span><span class="sxs-lookup"><span data-stu-id="24a8d-120">Make sure your device is connected to the same network as your PC.</span></span>
1. <span data-ttu-id="24a8d-121">Assurez-vous que l’appareil **n’est pas** connecté à votre PC via une connexion USB.</span><span class="sxs-lookup"><span data-stu-id="24a8d-121">Make sure the device **is not** connected to your PC via USB.</span></span>
1. <span data-ttu-id="24a8d-122">Accédez à la solution Visual Studio qui est créée lorsque vous double-cliquez sur un script dans Unity, où vous pouvez afficher et modifier votre C# scripts.</span><span class="sxs-lookup"><span data-stu-id="24a8d-122">Go to the Visual Studio solution that's created when you double click a script in Unity, where you can view and edit your C# scripts.</span></span>
1. <span data-ttu-id="24a8d-123">Déboguer -> attacher le débogueur Unity.</span><span class="sxs-lookup"><span data-stu-id="24a8d-123">Debug -> Attach Unity Debugger.</span></span>

    ![Attacher le débogueur Unity](images/il2cpp-debugging-attach.png)

1. <span data-ttu-id="24a8d-125">Sélectionnez votre appareil dans la liste et cliquez sur « OK » à attacher.</span><span class="sxs-lookup"><span data-stu-id="24a8d-125">Select your device in the list and click "OK" to attach.</span></span>

    ![Liste des appareils](images/il2cpp-debugging-machines.png)
