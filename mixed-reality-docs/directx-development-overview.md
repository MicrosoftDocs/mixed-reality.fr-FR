---
title: Vue d’ensemble du développement DirectX
description: Création d’un moteur de basée sur DirectX de réalité mixte à l’aide de l’API de réalité mixte Windows directement.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Rendu de DirectX, HOLOGRAPHIQUE, application native, native, WinRT, WinRT app, API de la plateforme, moteur personnalisé, intergiciel (middleware)
ms.openlocfilehash: da6beae6e256fef49481b581395e507b3f2acd04
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414382"
---
# <a name="directx-development-overview"></a>Vue d’ensemble du développement DirectX


Applications de réalité mixte Windows utilisent le [rendu HOLOGRAPHIQUE](rendering.md), [les regards](gaze.md), [mouvement](gestures.md), [contrôleur de mouvement](motion-controllers.md), [voix](voice-input.md), et [mappage spatial](spatial-mapping.md) API pour générer [une réalité mixte](mixed-reality.md) expériences pour HoloLens et des casques IMMERSIFS. Vous pouvez créer des applications de réalité mixte à l’aide d’un moteur 3D, tel que [Unity](unity-development-overview.md), ou vous pouvez écrire directement du code pour les API de réalité mixte Windows à l’aide de DirectX 11 ou DirectX 12. Si vous exploitez la plateforme directement, vous allez essentiellement peut-être générer votre propre intergiciel (middleware) ou votre infrastructure. Les API Windows prennent en charge les applications écrites dans les deux C++ et C#. Si vous choisissez d’utiliser C#, votre application peut exploiter la [SharpDX](http://sharpdx.org/) bibliothèque de logiciels open source.


Prend en charge de Windows Mixed Reality [deux types d’applications](app-views.md):
* **Mixte des applications de réalité** (UWP ou Win32) qui utilisent le [HolographicSpace API](getting-a-holographicspace.md) pour restituer un [vue immersive](app-views.md) à l’utilisateur qui remplit l’affichage de casque.
* **Applications 2D** (UWP) qui utilisent DirectX, XAML ou autres infrastructures pour restituer [vues 2D](app-views.md#2d-views) sur les tablettes multimédias dans Windows Mixed Reality domestique.


Les différences entre le développement DirectX pour [affichages 2D et immersives](app-views.md) sont principalement liés aux HOLOGRAPHIQUE rendu et entrée spatiale. Votre application UWP [IFrameworkView](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.core.iframeworkview.aspx) ou HWND de votre application Win32 sont nécessaire et restent en grande partie les mêmes, comme les WinRT APIs disponibles à votre application. Toutefois, vous devez utiliser un autre sous-ensemble de ces API pour tirer parti des fonctionnalités HOLOGRAPHIQUE. Par exemple, la chaîne de permutation est gérée par le système pour appslications HOLOGRAPHIQUE. Vous travaillez avec l’API de HolographicSpace plutôt que DXGI à [présenter des cadres](rendering-in-directx.md).

Pour commencer à développer des applications immersives :
* Pour **applications UWP**, [créer un nouveau projet UWP utilisant des modèles dans Visual Studio](creating-a-holographic-directx-project.md). Selon votre langage, **Visual C++**  ou **Visual C#** , vous pouvez trouver les modèles UWP sous **Windows universel**  >   **HOLOGRAPHIQUE**.
* Pour **applications Win32**, [démarrer à partir de la *BasicHologram* Win32, exemple](creating-a-holographic-directx-project.md#creating-a-win32-project).

Il s’agit d’un excellent moyen pour obtenir le code dont vous avez besoin pour ajouter la prise en charge du rendu holographique d’une application ou un moteur existant. Code et les concepts sont présentés dans le modèle d’une manière qui vous est familier à tout développeur de logiciels interactive en temps réel.


## <a name="getting-started"></a>Prise en main

Les rubriques suivantes décrivent les exigences de base de l’ajout de prise en charge Windows Mixed Reality à intergiciel (middleware) basée sur DirectX :

* [Création d’un projet de DirectX HOLOGRAPHIQUE](creating-a-holographic-directx-project.md): Le modèle d’application HOLOGRAPHIQUE associé à la documentation vous montre les différences entre ce que vous êtes habitué à ainsi que les exigences spéciales introduites par un appareil qui a conçu pour fonctionner tout reposant sur votre tête.
* [Obtention d’un HolographicSpace](getting-a-holographicspace.md): Vous devez tout d’abord créer un HolographicSpace qui fournira votre application de la séquence d’objets HolographicFrame qui représentent chaque position principale à partir duquel vous allez effectuer le rendu.
* [Rendu dans DirectX](rendering-in-directx.md): Dans la mesure où une chaîne de permutation HOLOGRAPHIQUE a deux cibles de rendu, vous devez apporter des modifications à la façon dont votre application s’affiche.
* [Systèmes de coordonnées dans DirectX](coordinate-systems-in-directx.md): Windows Mixed Reality apprend et sa compréhension du monde lorsque l’utilisateur autour des mises à jour. Cela fournit des systèmes de coordonnées spatiales que les applications utilisent pour raisonner sur son environnement de l’utilisateur, y compris les ancres spatiales et l’utilisateur défini phase spatiale.

## <a name="adding-mixed-reality-capabilities-and-inputs"></a>Ajout d’entrées et des fonctionnalités de réalité mixte

Pour activer la meilleure expérience possible pour les utilisateurs de votre appslication immersive, vous souhaiterez prendre en charge les blocs de construction clés suivantes :

* [Suivre de la tête et du regard dans DirectX](gaze-in-directx.md)
* [Mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md)
* [Entrée vocale dans DirectX](voice-input-in-directx.md)
* [Son spatial dans DirectX](spatial-sound-in-directx.md)
* [Mappage spatial dans DirectX](spatial-mapping-in-directx.md)


Il existe des autres fonctionnalités clés de nombreuses applications immersives souhaiterez utiliser sont également exposées à des applications DirectX :

* [Ancres spatiales partagées dans DirectX](shared-spatial-anchors-in-directx.md)
* [Appareil photo localisable dans DirectX](locatable-camera-in-directx.md)
* [Saisie à l’aide de la commande de jeu, du clavier et de la souris dans DirectX](keyboard,-mouse,-and-controller-input-in-directx.md)

## <a name="see-also"></a>Voir aussi
* [Modèle d’application](app-model.md)
* [Vues d’applications](app-views.md)
