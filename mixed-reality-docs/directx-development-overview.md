---
title: Vue d’ensemble du développement natif
description: Créez un moteur de réalité mixte DirectX en utilisant directement les API Windows Mixed Reality.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: DirectX, rendu holographique, native, application native, application WinRT, application WinRT, API de plateforme, moteur personnalisé, intergiciel
ms.openlocfilehash: 5c61739ea6c90b4547c5c9927cf2129304650926
ms.sourcegitcommit: 9de2cb11321e6517db69e8c93459a205900a2174
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80159994"
---
# <a name="native-development-overview"></a>Vue d’ensemble du développement natif

Les applications Windows Mixed Reality utilisent les API suivantes pour créer des expériences de [réalité mixte](mixed-reality.md) pour HoloLens et d’autres casques immersifs :

 - [Rendu holographique](rendering.md)
 - [Pointage du regard](gaze-and-commit.md)
 - [Mouvement](gaze-and-commit.md#composite-gestures)
 - [Contrôleur de mouvement](motion-controllers.md)
 - [Voix](voice-input.md)
 - [Mappage spatial](spatial-mapping.md)

Vous pouvez créer des applications de réalité mixte à l’aide d’un moteur 3D, comme [Unity](unity-development-overview.md). Vous pouvez ou directement coder les API Windows Mixed Reality à l’aide de DirectX 11 ou DirectX 12. Si vous tirez parti de la plateforme directement, vous créez essentiellement votre propre infrastructure ou intergiciel (middleware). Les API Windows prennent en charge les applications écrites à C++ la C#fois dans et. Si vous utilisez C#, votre application peut tirer parti de la bibliothèque de logiciels open source [SharpDX](https://sharpdx.org/) .

Windows Mixed Reality prend en charge [deux types d’applications](app-views.md):
* **Applications en réalité mixte** (UWP ou Win32) qui utilisent l’API [HOLOGRAPHICSPACE](getting-a-holographicspace.md) ou l' [API OpenXR](openxr.md) pour restituer une [vue immersive](app-views.md) à l’utilisateur qui remplit l’affichage du casque
* **applications 2D** (UWP) qui utilisent DirectX, XAML ou une autre infrastructure pour restituer des [vues 2D](app-views.md#2d-views) sur des ardoises dans la page d’hébergement de Windows Mixed Reality

Les différences entre le développement DirectX pour les [vues 2D et les vues immersives](app-views.md) concernent principalement le rendu holographique et l’entrée spatiale. Le [IFrameworkView](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.core.iframeworkview.aspx) de votre application UWP ou le HWND de votre application Win32 sont requis et restent en grande partie les mêmes. Il en va de même pour les API WinRT qui sont disponibles pour votre application. Toutefois, vous devez utiliser un sous-ensemble différent de ces API pour tirer parti des fonctionnalités holographiques. Par exemple, le utilise permutation et le frame présent sont gérés par le système pour les applications holographiques afin d’activer une boucle de frame de prédiction de pose.

## <a name="get-started-with-openxr"></a>Prise en main de OpenXR

Vous pouvez développer à l’aide de OpenXR sur un casque de l’architecture HoloLens 2 ou Windows Mixed Reality sur le bureau.  Si vous n’avez pas accès à un casque, vous pouvez utiliser l’émulateur HoloLens 2 ou Windows Mixed Reality Simulator à la place.

Pour commencer à développer des applications OpenXR pour les casques HoloLens 2 ou Windows Mixed Reality, consultez [la page prise en main du développement OpenXR](openxr-getting-started.md).

## <a name="get-started-with-winrt"></a>Prise en main de WinRT

Pour commencer à développer des applications immersifs :
* Pour les **applications UWP**, [Utilisez les modèles de Visual Studio pour créer un projet UWP](creating-a-holographic-directx-project.md). En fonction de votre langage, C++ visuel ou C#visuel, recherchez les modèles UWP sous **Windows Universal** > **holographique**.
* Pour les **applications Win32**, [Démarrez à partir de l’exemple Win32 *BasicHologram* ](creating-a-holographic-directx-project.md#creating-a-win32-project).

Cette étape est un excellent moyen d’obtenir le code dont vous avez besoin pour ajouter la prise en charge de rendu holographique à une application ou à un moteur existant. Le code et les concepts sont présentés dans le modèle d’une manière familière à tous les développeurs de logiciels interactifs en temps réel.

Les rubriques suivantes décrivent les exigences de base lorsque vous ajoutez la prise en charge de Windows Mixed Reality à l’intergiciel (middleware) basé sur DirectX.

* [Créer un projet holographique DirectX](creating-a-holographic-directx-project.md): le modèle d’application holographique associé à la documentation montre les différences par rapport à ce que vous utilisez. Il décrit également les exigences spéciales pour un appareil conçu pour fonctionner tout en restant sur votre tête.
* [Obtenez un HolographicSpace](getting-a-holographicspace.md): vous devez d’abord créer un HolographicSpace qui donne à votre application la séquence d’objets HolographicFrame qui représentent chaque position d’en-tête à partir de laquelle vous allez effectuer le rendu.
* [Rendu dans DirectX](rendering-in-directx.md): étant donné qu’un utilise permutation holographique a deux cibles de rendu, vous devez apporter certaines modifications à la façon dont votre application s’affiche.
* [Systèmes de coordonnées dans DirectX](coordinate-systems-in-directx.md): Windows Mixed Reality apprend et met à jour sa compréhension du monde à mesure que l’utilisateur parcourt. Cela fournit des systèmes de coordonnées spatiales que les applications utilisent pour la raison de l’environnement de l’utilisateur, y compris les ancres spatiales et la phase spatiale définie de l’utilisateur.

## <a name="add-mixed-reality-capabilities-and-inputs"></a>Ajouter des fonctionnalités et des entrées de réalité mixte

Pour offrir la meilleure expérience possible aux utilisateurs de votre application immersif, vous devez prendre en charge les principaux blocs de construction suivants :

* [Suivre de la tête et du regard dans DirectX](gaze-in-directx.md)
* [Mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md)
* [Entrée vocale dans DirectX](voice-input-in-directx.md)
* [Son spatial](https://docs.microsoft.com/windows/win32/coreaudio/spatial-sound)
* [Mappage spatial dans DirectX](spatial-mapping-in-directx.md)

Il s’agit d’autres fonctionnalités clés utilisées par de nombreuses applications immersifs qui sont également exposées aux applications DirectX :

* [Ancres spatiales partagées dans DirectX](shared-spatial-anchors-in-directx.md)
* [Saisie à l’aide de la commande de jeu, du clavier et de la souris dans DirectX](keyboard-mouse-and-controller-input-in-directx.md)

## <a name="see-also"></a>Voir aussi
* [Modèle d’application](app-model.md)
* [Vues d’applications](app-views.md)
