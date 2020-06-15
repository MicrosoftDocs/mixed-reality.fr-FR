---
title: 1. Mise en route
description: Premier tutoriel d’une série de six tutoriels, dans lequel vous apprenez à créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in UX Tools du Mixed Reality Toolkit
author: hferrone
ms.author: v-haferr
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: c16671fc8f4233378dafa646786df1f7b5ae18e1
ms.sourcegitcommit: 1b8090ba6aed9ff128e4f32d40c96fac2e6a220b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330166"
---
# <a name="1-getting-started"></a><span data-ttu-id="2679d-104">1. Mise en route</span><span class="sxs-lookup"><span data-stu-id="2679d-104">1. Getting started</span></span>

<span data-ttu-id="2679d-105">Que vous débutiez avec la réalité mixte ou que vous soyez expérimenté, ce tutoriel est parfait pour découvrir [HoloLens 2](https://docs.microsoft.com/windows/mixed-reality/) et [Unreal Engine](https://www.unrealengine.com/en-US/).</span><span class="sxs-lookup"><span data-stu-id="2679d-105">Whether you're new to mixed reality or a seasoned pro, this is the place to start your journey with [HoloLens 2](https://docs.microsoft.com/windows/mixed-reality/) and [Unreal Engine](https://www.unrealengine.com/en-US/).</span></span> <span data-ttu-id="2679d-106">Cette série de tutoriels vous guidera dans la création d’une application interactive de jeu d’échecs à l’aide du [plug-in UX Tools](https://github.com/microsoft/MixedReality-UXTools-Unreal), qui fait partie de [Mixed Reality Toolkit for Unreal](https://github.com/microsoft/MixedRealityToolkit-Unreal).</span><span class="sxs-lookup"><span data-stu-id="2679d-106">This tutorial series will give you a step by step guide on how to build an interactive chess app with the [UX Tools plugin](https://github.com/microsoft/MixedReality-UXTools-Unreal) - part of the [Mixed Reality Toolkit for Unreal](https://github.com/microsoft/MixedRealityToolkit-Unreal).</span></span> <span data-ttu-id="2679d-107">Ce plug-in vous permet d’ajouter des fonctionnalités d’expérience utilisateur courantes à vos projets à l’aide de code, de blueprints et d’exemples.</span><span class="sxs-lookup"><span data-stu-id="2679d-107">The plugin will help you add common UX features to your projects with code, blueprints, and examples.</span></span> 

![Scène finale dans la fenêtre Viewport](images/unreal-uxt/5-endscene.PNG)

<span data-ttu-id="2679d-109">À la fin de cette série, vous aurez obtenu une expérience pratique concernant :</span><span class="sxs-lookup"><span data-stu-id="2679d-109">By the end of the series you'll have hands-on experience with:</span></span>
* <span data-ttu-id="2679d-110">Création d’un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="2679d-110">Starting a new project</span></span>
* <span data-ttu-id="2679d-111">La configuration de la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="2679d-111">Setting up for mixed reality</span></span>
* <span data-ttu-id="2679d-112">L’utilisation des entrées utilisateur</span><span class="sxs-lookup"><span data-stu-id="2679d-112">Working with user input</span></span>
* <span data-ttu-id="2679d-113">L’ajout de boutons</span><span class="sxs-lookup"><span data-stu-id="2679d-113">Adding buttons</span></span>
* <span data-ttu-id="2679d-114">Le jeu sur un émulateur ou un appareil</span><span class="sxs-lookup"><span data-stu-id="2679d-114">Playing on an emulator or device</span></span>

<span data-ttu-id="2679d-115">Si vous avez des questions, consultez [Vue d’ensemble du développement Unreal](https://docs.microsoft.com/windows/mixed-reality/unreal-development-overview).</span><span class="sxs-lookup"><span data-stu-id="2679d-115">If you have any questions, check out our [Unreal development overview](https://docs.microsoft.com/windows/mixed-reality/unreal-development-overview).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2679d-116">Prérequis</span><span class="sxs-lookup"><span data-stu-id="2679d-116">Prerequisites</span></span>
<span data-ttu-id="2679d-117">Avant de commencer, vérifiez que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2679d-117">Make sure you've met the following requirements before jumping in:</span></span>
* <span data-ttu-id="2679d-118">Windows 10 1809 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="2679d-118">Windows 10 1809 or later</span></span>
* <span data-ttu-id="2679d-119">SDK Windows 10 (10.0.18362.0 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="2679d-119">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="2679d-120">[Unreal Engine](https://www.unrealengine.com/en-US/get-now) 4.25 ou ultérieur</span><span class="sxs-lookup"><span data-stu-id="2679d-120">[Unreal Engine](https://www.unrealengine.com/en-US/get-now) 4.25 or later</span></span>
* <span data-ttu-id="2679d-121">Appareil Microsoft HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode) ou l’émulateur</span><span class="sxs-lookup"><span data-stu-id="2679d-121">Microsoft HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode) or Emulator</span></span>
* <span data-ttu-id="2679d-122">Visual Studio 2019 avec les charges de travail ci-dessous</span><span class="sxs-lookup"><span data-stu-id="2679d-122">Visual Studio 2019 with the workloads below</span></span>

### <a name="installing-visual-studio-2019"></a><span data-ttu-id="2679d-123">Installation de Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="2679d-123">Installing Visual Studio 2019</span></span>
<span data-ttu-id="2679d-124">La dernière étape consiste à configurer Visual Studio de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="2679d-124">The last step is to setup Visual Studio as follows:</span></span>
1. <span data-ttu-id="2679d-125">Installez la dernière version de [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2679d-125">Install the latest version of [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/)</span></span>
2. <span data-ttu-id="2679d-126">Installez les [charges de travail](https://docs.microsoft.com/visualstudio/install/modify-visual-studio?view=vs-2019#modify-workloads) suivantes :</span><span class="sxs-lookup"><span data-stu-id="2679d-126">Install the following [workloads](https://docs.microsoft.com/visualstudio/install/modify-visual-studio?view=vs-2019#modify-workloads):</span></span>
    * <span data-ttu-id="2679d-127">Développement Desktop en C++</span><span class="sxs-lookup"><span data-stu-id="2679d-127">Desktop development with C++</span></span>
    * <span data-ttu-id="2679d-128">Développement .NET Desktop</span><span class="sxs-lookup"><span data-stu-id="2679d-128">.NET desktop development</span></span>
    * <span data-ttu-id="2679d-129">Développement pour la plateforme Windows universelle</span><span class="sxs-lookup"><span data-stu-id="2679d-129">Universal Windows Platform development</span></span>

3. <span data-ttu-id="2679d-130">Installez les [composants](https://docs.microsoft.com/visualstudio/install/modify-visual-studio?view=vs-2019#modify-individual-components) suivants :</span><span class="sxs-lookup"><span data-stu-id="2679d-130">Install the following [components](https://docs.microsoft.com/visualstudio/install/modify-visual-studio?view=vs-2019#modify-individual-components):</span></span>
    * <span data-ttu-id="2679d-131">Compilateurs, outils de build et runtimes > MSVC v142 - VS 2019 C++ ARM64 Build Tools (dernière version)</span><span class="sxs-lookup"><span data-stu-id="2679d-131">Compilers, build tools, and runtimes > MSVC v142 - VS 2019 C++ ARM64 build tools (latest version)</span></span>

<span data-ttu-id="2679d-132">C’est tout !</span><span class="sxs-lookup"><span data-stu-id="2679d-132">That's it!</span></span> <span data-ttu-id="2679d-133">Vous êtes maintenant prêt à lancer le projet d’application de jeu d’échecs.</span><span class="sxs-lookup"><span data-stu-id="2679d-133">You're all set to move on to starting the chess app project.</span></span>

[<span data-ttu-id="2679d-134">Section suivante : 2. Initialisation de votre projet et première application</span><span class="sxs-lookup"><span data-stu-id="2679d-134">Next section: 2. Initializing your project and first application</span></span>](unreal-uxt-ch2.md)