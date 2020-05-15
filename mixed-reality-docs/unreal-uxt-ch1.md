---
title: 1. Mise en route
description: Partie 1 d’un tutoriel pour créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in UX Tools du Mixed Reality Toolkit
author: sw5813
ms.author: suwu
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: 3ca47cfe7bb0a733932f3777cc8b531ef9df8e71
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82840128"
---
# <a name="1-getting-started"></a><span data-ttu-id="b9d7c-104">1. Mise en route</span><span class="sxs-lookup"><span data-stu-id="b9d7c-104">1. Getting started</span></span>

<span data-ttu-id="b9d7c-105">Ce tutoriel vous montre pas à pas comment créer une application de jeu d’échecs HoloLens 2 interactive en utilisant Unreal Engine 4.</span><span class="sxs-lookup"><span data-stu-id="b9d7c-105">This is a step by step tutorial that will show you how to build an interactive HoloLens 2 chess app using Unreal Engine 4.</span></span> <span data-ttu-id="b9d7c-106">Il explique également comment utiliser le plug-in UX Tools du Mixed Reality Toolkit pour Unreal afin d’accélérer le développement.</span><span class="sxs-lookup"><span data-stu-id="b9d7c-106">You will also learn how to use the UX Tools plugin from the Mixed Reality Toolkit for Unreal to speed up development.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b9d7c-107">Prérequis</span><span class="sxs-lookup"><span data-stu-id="b9d7c-107">Prerequisites</span></span>

* <span data-ttu-id="b9d7c-108">Windows 10 1809 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="b9d7c-108">Windows 10 1809 or later</span></span>
* <span data-ttu-id="b9d7c-109">SDK Windows 10 (10.0.18362.0 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="b9d7c-109">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="b9d7c-110">Unreal Engine 4.25 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="b9d7c-110">Unreal Engine 4.25 or later</span></span>
* <span data-ttu-id="b9d7c-111">Appareil Microsoft HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode) ou l’émulateur</span><span class="sxs-lookup"><span data-stu-id="b9d7c-111">Microsoft HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode) or Emulator</span></span>
* <span data-ttu-id="b9d7c-112">Visual Studio 2019 (avec les charges de travail et les composants indiqués ci-dessous)</span><span class="sxs-lookup"><span data-stu-id="b9d7c-112">Visual Studio 2019 (with below workloads and components)</span></span>

### <a name="installing-visual-studio-2019-workloads-and-components"></a><span data-ttu-id="b9d7c-113">Installation de Visual Studio 2019, et des charges de travail et composants requis</span><span class="sxs-lookup"><span data-stu-id="b9d7c-113">Installing Visual Studio 2019, workloads, and components</span></span>
1. <span data-ttu-id="b9d7c-114">Installez Visual Studio 2019 ou faites la mise à jour vers la dernière version de Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="b9d7c-114">Install or and update to the latest version of Visual Studio 2019</span></span>
* [<span data-ttu-id="b9d7c-115">Télécharger Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="b9d7c-115">Download Visual Studio 2019</span></span>](https://visualstudio.microsoft.com/downloads/)
2. <span data-ttu-id="b9d7c-116">Installez les charges de travail suivantes :</span><span class="sxs-lookup"><span data-stu-id="b9d7c-116">Install the following workloads:</span></span>
* <span data-ttu-id="b9d7c-117">Développement Desktop en C++</span><span class="sxs-lookup"><span data-stu-id="b9d7c-117">Desktop development with C++</span></span>
* <span data-ttu-id="b9d7c-118">Développement .NET Desktop</span><span class="sxs-lookup"><span data-stu-id="b9d7c-118">.NET desktop development</span></span>
* <span data-ttu-id="b9d7c-119">Développement pour la plateforme Windows universelle</span><span class="sxs-lookup"><span data-stu-id="b9d7c-119">Universal Windows Platform development</span></span>
3. <span data-ttu-id="b9d7c-120">Installez chacun des composants suivants :</span><span class="sxs-lookup"><span data-stu-id="b9d7c-120">Install the following individual components:</span></span>
* <span data-ttu-id="b9d7c-121">Compilateurs, outils de build et runtimes > MSVC v142 - VS 2019 C++ ARM64 Build Tools (dernière version)</span><span class="sxs-lookup"><span data-stu-id="b9d7c-121">Compilers, build tools, and runtimes > MSVC v142 - VS 2019 C++ ARM64 build tools (latest version)</span></span>

[<span data-ttu-id="b9d7c-122">Section suivante : 2. Initialisation de votre projet et première application</span><span class="sxs-lookup"><span data-stu-id="b9d7c-122">Next section: 2. Initializing your project and first application</span></span>](unreal-uxt-ch2.md)