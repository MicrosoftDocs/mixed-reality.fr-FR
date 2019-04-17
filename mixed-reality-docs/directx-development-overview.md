---
title: Vue d’ensemble du développement DirectX
description: Création d’un moteur de basée sur DirectX de réalité mixte à l’aide de l’API de réalité mixte Windows directement.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Rendu de DirectX, HOLOGRAPHIQUE, application native, native, WinRT, WinRT app, API de la plateforme, moteur personnalisé, intergiciel (middleware)
ms.openlocfilehash: 047144cb8fcf158f74375e9ec69dca92a2a1cf01
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593678"
---
# <a name="directx-development-overview"></a>Vue d’ensemble du développement DirectX

Utilisation des applications Windows Mixed Reality le [rendu HOLOGRAPHIQUE](rendering.md), [les regards](gaze.md), [mouvement](gestures.md), [contrôleur de mouvement](motion-controllers.md), [vocal ](voice-input.md) et [mappage spatial](spatial-mapping.md) API pour générer [une réalité mixte](mixed-reality.md) expériences pour HoloLens et des casques IMMERSIFS. Vous pouvez créer des applications de réalité mixte à l’aide d’un moteur 3D, tel que [Unity](unity-development-overview.md), ou vous pouvez utiliser les API de réalité mixte Windows avec DirectX 11. Veuillez noter que DirectX 12 n’est pas compatible. Si vous exploitez la plateforme directement, vous allez essentiellement peut-être générer votre propre intergiciel (middleware) ou votre infrastructure. L’API de Windows prennent en charge les applications écrites dans les deux C++ et C#. Si vous souhaitez utiliser C#, votre application peut exploiter la [SharpDX](http://sharpdx.org/) bibliothèque de logiciels open source.

Prend en charge de Windows Mixed Reality [deux types d’applications](app-views.md):
* **Applications de réalité mixte** (UWP ou Win32), qui utilisent le [HolographicSpace API](getting-a-holographicspace.md) pour restituer un [vue immersive](app-views.md) à l’utilisateur qui remplit l’affichage de casque.
* **Applications 2D** (UWP), qui utilisent DirectX, XAML ou autres infrastructures pour effectuer le rendu [vues 2D](app-views.md#2d-views) sur les tablettes multimédias dans Windows Mixed Reality domestique.

Les différences entre le développement DirectX pour [affichages 2D et immersives](app-views.md) sont principalement liés aux HOLOGRAPHIQUE rendu et entrée spatiale. Votre application UWP [IFrameworkView](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.core.iframeworkview.aspx) ou HWND de votre application Win32 sont toujours nécessaire et restent en grande partie identiques, comme les WinRT APIs disponibles à votre application. Toutefois, vous utilisez un autre sous-ensemble de ces API pour tirer parti des fonctionnalités HOLOGRAPHIQUE. Par exemple, la chaîne de permutation est gérée par le système pour les applications holographique et que vous travaillez avec l’API de HolographicSpace plutôt que DXGI à [présenter des cadres](rendering-in-directx.md).

Pour commencer à développer des applications immersives :
* Pour **applications UWP**, [créer un nouveau projet UWP utilisant des modèles dans Visual Studio](creating-a-holographic-directx-project.md). Selon votre langage, **Visual C++**  ou **Visual C#** , vous trouverez les modèles UWP sous **Windows universel**  >   **HOLOGRAPHIQUE**.
* Pour **applications Win32**, [créer un nouveau projet de bureau Win32](creating-a-holographic-directx-project.md#creating-a-win32-project) puis suivez les instructions de Win32 le [bien un HolographicSpace](getting-a-holographicspace.md) page pour obtenir un HolographicSpace.

Il s’agit d’un excellent moyen pour obtenir le code que vous devez ajouter la prise en charge du rendu HOLOGRAPHIQUE vers une application ou un moteur existant. Code et les concepts sont présentés dans le modèle d’une manière qui vous est familier à tout développeur de logiciels interactive en temps réel.

## <a name="getting-started"></a>Prise en main

Les rubriques suivantes décrivent les exigences de base de l’ajout de prise en charge Windows Mixed Reality à intergiciel (middleware) basée sur DirectX :
* [Création d’un projet de DirectX HOLOGRAPHIQUE](creating-a-holographic-directx-project.md): Le modèle d’application HOLOGRAPHIQUE associé à la documentation vous montre les différences entre ce que vous êtes habitué et les exigences spéciales introduites par un appareil qui a conçu pour fonctionner tout reposant sur votre tête.
* [Obtention d’un HolographicSpace](getting-a-holographicspace.md): Vous devez tout d’abord créer un HolographicSpace, qui fournit votre application la séquence d’objets HolographicFrame qui représentent chaque position principale à partir duquel vous allez effectuer le rendu.
* [Rendu dans DirectX](rendering-in-directx.md): Dans la mesure où une chaîne de permutation HOLOGRAPHIQUE a deux cibles de rendu, vous devrez probablement apporter des modifications à la façon dont votre application s’affiche.
* [Systèmes de coordonnées dans DirectX](coordinate-systems-in-directx.md): Windows Mixed Reality apprend et met à jour de sa compréhension du monde en tant que les parcours utilisateur, en fournissant des systèmes de coordonnées spatiales qui utilisent des applications de raisonner sur son environnement de l’utilisateur, y compris les ancres spatiales et stade spatiale de l’utilisateur défini.

## <a name="adding-mixed-reality-capabilities-and-inputs"></a>Ajout d’entrées et des fonctionnalités de réalité mixte

Pour activer la meilleure expérience possible pour les utilisateurs de vos applications immersives, vous souhaiterez prendre en charge les blocs de construction clés suivantes :
* [Regards, les mouvements et les contrôleurs de mouvement dans DirectX](gaze,-gestures,-and-motion-controllers-in-directx.md)
* [Entrée vocale dans DirectX](voice-input-in-directx.md)
* [Son spatial dans DirectX](spatial-sound-in-directx.md)
* [Mappage spatial dans DirectX](spatial-mapping-in-directx.md)

Il existe d’autres fonctionnalités clées que de nombreuses applications immersives souhaitez utiliser, qui sont également exposées à des applications DirectX :
* [Partagé spatiales ancres dans DirectX](shared-spatial-anchors-in-directx.md)
* [Caméra localisable dans DirectX](locatable-camera-in-directx.md)
* [Entrée d’un contrôleur dans DirectX, clavier et souris](keyboard,-mouse,-and-controller-input-in-directx.md)

## <a name="see-also"></a>Voir aussi
* [Modèle d’application](app-model.md)
* [Vues de l’application](app-views.md)
