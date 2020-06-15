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
# <a name="1-getting-started"></a>1. Mise en route

Que vous débutiez avec la réalité mixte ou que vous soyez expérimenté, ce tutoriel est parfait pour découvrir [HoloLens 2](https://docs.microsoft.com/windows/mixed-reality/) et [Unreal Engine](https://www.unrealengine.com/en-US/). Cette série de tutoriels vous guidera dans la création d’une application interactive de jeu d’échecs à l’aide du [plug-in UX Tools](https://github.com/microsoft/MixedReality-UXTools-Unreal), qui fait partie de [Mixed Reality Toolkit for Unreal](https://github.com/microsoft/MixedRealityToolkit-Unreal). Ce plug-in vous permet d’ajouter des fonctionnalités d’expérience utilisateur courantes à vos projets à l’aide de code, de blueprints et d’exemples. 

![Scène finale dans la fenêtre Viewport](images/unreal-uxt/5-endscene.PNG)

À la fin de cette série, vous aurez obtenu une expérience pratique concernant :
* Création d’un nouveau projet
* La configuration de la réalité mixte
* L’utilisation des entrées utilisateur
* L’ajout de boutons
* Le jeu sur un émulateur ou un appareil

Si vous avez des questions, consultez [Vue d’ensemble du développement Unreal](https://docs.microsoft.com/windows/mixed-reality/unreal-development-overview).

## <a name="prerequisites"></a>Prérequis
Avant de commencer, vérifiez que vous disposez des éléments suivants :
* Windows 10 1809 ou version ultérieure
* SDK Windows 10 (10.0.18362.0 ou version ultérieure)
* [Unreal Engine](https://www.unrealengine.com/en-US/get-now) 4.25 ou ultérieur
* Appareil Microsoft HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode) ou l’émulateur
* Visual Studio 2019 avec les charges de travail ci-dessous

### <a name="installing-visual-studio-2019"></a>Installation de Visual Studio 2019
La dernière étape consiste à configurer Visual Studio de la façon suivante :
1. Installez la dernière version de [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/).
2. Installez les [charges de travail](https://docs.microsoft.com/visualstudio/install/modify-visual-studio?view=vs-2019#modify-workloads) suivantes :
    * Développement Desktop en C++
    * Développement .NET Desktop
    * Développement pour la plateforme Windows universelle

3. Installez les [composants](https://docs.microsoft.com/visualstudio/install/modify-visual-studio?view=vs-2019#modify-individual-components) suivants :
    * Compilateurs, outils de build et runtimes > MSVC v142 - VS 2019 C++ ARM64 Build Tools (dernière version)

C’est tout ! Vous êtes maintenant prêt à lancer le projet d’application de jeu d’échecs.

[Section suivante : 2. Initialisation de votre projet et première application](unreal-uxt-ch2.md)