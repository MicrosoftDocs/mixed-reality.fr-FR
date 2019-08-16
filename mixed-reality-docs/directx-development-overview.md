---
title: Vue d’ensemble du développement DirectX
description: Création directe d’un moteur de réalité mixte DirectX à l’aide des API Windows Mixed Reality.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: DirectX, rendu holographique, native, application native, application WinRT, application WinRT, API de plateforme, moteur personnalisé, intergiciel
ms.openlocfilehash: 58b311038633dc325cc2c5425fd09b9a0192b161
ms.sourcegitcommit: 4ac761fed7a9570977f6d031ba4f870585d6630a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68861707"
---
# <a name="directx-development-overview"></a>Vue d’ensemble du développement DirectX


Les applications Windows Mixed Reality utilisent le [rendu holographique](rendering.md), le [point de présence](gaze.md), le [mouvement](gestures.md), le [contrôleur de mouvement](motion-controllers.md), la [voix](voice-input.md) et les API de [mappage spatial](spatial-mapping.md) pour créer des expériences de [réalité mixte](mixed-reality.md) pour HoloLens et casques immersifs. Vous pouvez créer des applications de réalité mixte à l’aide d’un moteur 3D, comme [Unity](unity-development-overview.md), ou vous pouvez coder directement vers les API Windows Mixed realing à l’aide de DirectX 11 ou DirectX 12. Si vous tirez parti de la plateforme directement, vous créerez essentiellement votre propre infrastructure ou intergiciel. Les API Windows prennent en charge les applications C++ écrites C#dans et. Si vous choisissez d’utiliser C#, votre application peut tirer parti de la bibliothèque de logiciels open source [SharpDX](http://sharpdx.org/) .


Windows Mixed Reality prend en charge [deux types d’applications](app-views.md):
* **Applications de réalité mixte** (UWP ou Win32) qui utilisent l' [API HolographicSpace](getting-a-holographicspace.md) pour restituer une [vue immersive](app-views.md) à l’utilisateur qui remplit l’affichage du casque.
* **applications 2D** (UWP) qui utilisent DirectX, XAML ou d’autres frameworks pour restituer des [vues 2D](app-views.md#2d-views) sur des ardoises dans la page d’hébergement de la réalité mixte Windows.


Les différences entre le développement DirectX pour les [vues 2D et les vues immersives](app-views.md) sont principalement liées au rendu holographique et à l’entrée spatiale. Le [IFrameworkView](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.core.iframeworkview.aspx) de votre application UWP ou le HWND de votre application Win32 sont requis et restent en grande partie les mêmes, tout comme les API WinRT disponibles pour votre application. Toutefois, vous devez utiliser un sous-ensemble différent de ces API pour tirer parti des fonctionnalités holographiques. Par exemple, la chaîne de permutation est gérée par le système pour les appslications holographiques. Vous utilisez l’API HolographicSpace plutôt que DXGI pour [présenter](rendering-in-directx.md)des frames.

Pour commencer à développer des applications immersifs:
* Pour les **applications UWP**, [créez un nouveau projet UWP à l’aide des modèles dans Visual Studio](creating-a-holographic-directx-project.md). En fonction de votre langue **, C++ visuel** ou **visuel C#** , vous trouverez les modèles UWP sous **Windows Universal** > **holographique**.
* Pour les **applications Win32**, [Démarrez à partir de l’exemple Win32 *BasicHologram* ](creating-a-holographic-directx-project.md#creating-a-win32-project).

C’est un excellent moyen d’obtenir le code dont vous avez besoin pour ajouter la prise en charge de rendu holographique à une application ou à un moteur existant. Le code et les concepts sont présentés dans le modèle d’une manière familière à tous les développeurs de logiciels interactifs en temps réel.


## <a name="getting-started"></a>Prise en main

Les rubriques suivantes décrivent les exigences de base liées à l’ajout de la prise en charge de Windows Mixed realisation à l’intergiciel (middleware) basé sur DirectX:

* [Création d’un projet de DirectX holographique](creating-a-holographic-directx-project.md): Le modèle d’application holographique associé à la documentation vous montre les différences entre ce que vous utilisez, ainsi que les exigences spéciales introduites par un appareil conçu pour fonctionner tout en restant sur votre tête.
* [Obtention d’un HolographicSpace](getting-a-holographicspace.md): Vous devez d’abord créer un HolographicSpace qui fournira à votre application la séquence d’objets HolographicFrame représentant chaque position d’en-tête à partir de laquelle vous allez effectuer le rendu.
* [Rendu dans DirectX](rendering-in-directx.md): Étant donné qu’une chaîne de permutation holographique a deux cibles de rendu, vous devez apporter certaines modifications à la façon dont votre application s’affiche.
* [Systèmes de coordonnées dans DirectX](coordinate-systems-in-directx.md): Windows Mixed Reality apprend et met à jour sa compréhension du monde au fur et à mesure que l’utilisateur parcourt. Cela fournit des systèmes de coordonnées spatiales que les applications utilisent pour la raison de l’environnement de l’utilisateur, y compris les ancres spatiales et la phase spatiale définie de l’utilisateur.

## <a name="adding-mixed-reality-capabilities-and-inputs"></a>Ajout de fonctionnalités et d’entrées de réalité mixte

Pour offrir la meilleure expérience possible aux utilisateurs de vos appslication immersifs, vous pouvez prendre en charge les principaux blocs de construction suivants:

* [Suivre de la tête et du regard dans DirectX](gaze-in-directx.md)
* [Mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md)
* [Entrée vocale dans DirectX](voice-input-in-directx.md)
* [Son spatial dans DirectX](spatial-sound-in-directx.md)
* [Mappage spatial dans DirectX](spatial-mapping-in-directx.md)


Il existe d’autres fonctionnalités clés que de nombreuses applications immersifs voudront utiliser et qui sont également exposées aux applications DirectX:

* [Ancres spatiales partagées dans DirectX](shared-spatial-anchors-in-directx.md)
* [Saisie à l’aide de la commande de jeu, du clavier et de la souris dans DirectX](keyboard,-mouse,-and-controller-input-in-directx.md)

## <a name="see-also"></a>Voir aussi
* [Modèle d’application](app-model.md)
* [Vues d’applications](app-views.md)
