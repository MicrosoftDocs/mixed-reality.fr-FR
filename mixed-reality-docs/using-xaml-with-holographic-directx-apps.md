---
title: Utilisation de XAML avec des applications DirectX holographiques
description: Explique l’impact du basculement entre les vues XAML 2D et les vues immersives dans votre application DirectX, et comment utiliser efficacement un mode XAML et un affichage immersif.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, UWP, gestion des affichages des applications, XAML, clavier, procédure pas à pas, DirectX
ms.openlocfilehash: 32b2feea0cb6b8aba972c1772451ca7b5b9946d5
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63548703"
---
# <a name="using-xaml-with-holographic-directx-apps"></a>Utilisation de XAML avec des applications DirectX holographiques

Cette rubrique explique l’impact du basculement entre les [vues XAML 2D et les vues immersives](app-views.md) dans votre application DirectX, et comment utiliser efficacement un affichage XAML et une vue immersive.

## <a name="xaml-view-switching-overview"></a>Vue d’ensemble du basculement de vue XAML

Sur HoloLens, une application généralement immersive qui peut afficher ultérieurement un affichage XAML 2D doit initialiser d’abord cette vue XAML et basculer immédiatement vers une vue immersive. Cela signifie que XAML se chargera avant que votre application puisse faire quoi que ce soit. Par conséquent, il y aura une légère augmentation du temps de démarrage, et XAML continuera à occuper de l’espace mémoire dans le processus de votre application pendant qu’il se trouve en arrière-plan. le délai de démarrage et l’utilisation de la mémoire dépendent de ce que fait votre application avec XAML avant de basculer vers la vue native. Si vous ne faites rien dans votre code de démarrage XAML dans un premier temps, sauf démarrer votre vue immersif, l’impact doit être mineur. En outre, étant donné que votre rendu holographique est effectué directement vers la vue immersive, vous évitez les restrictions XAML relatives à ce rendu.

Notez que le compte d’utilisation de la mémoire pour le processeur et le GPU. Direct3D 11 est en mesure d’échanger la mémoire graphique virtuelle, mais il est possible qu’il ne soit pas en mesure de permuter une partie ou la totalité des ressources du GPU XAML, et il peut y avoir un impact notable sur les performances. Dans les deux cas, ne pas charger les fonctionnalités XAML dont vous n’avez pas besoin offre davantage de place pour votre application et offre une meilleure expérience.

## <a name="xaml-view-switching-workflow"></a>Flux de travail de basculement de vue XAML

Le flux de travail d’une application qui va directement du XAML au mode immersif est le suivant:
* L’application démarre en mode XAML 2D.
* La séquence de démarrage XAML de l’application détecte si le système actuel prend en charge le rendu holographique:
* Si c’est le cas, l’application crée l’affichage immersif et le met immédiatement au premier plan. Le chargement XAML est ignoré pour tout élément qui n’est pas nécessaire sur les appareils Windows Mixed Reality, y compris les classes de rendu et le chargement des ressources dans la vue XAML. Si l’application utilise du code XAML pour l’entrée au clavier, cette page d’entrée doit encore être créée.
* Si ce n’est pas le cas, la vue XAML peut poursuivre l’entreprise comme d’habitude.

## <a name="tip-for-rendering-graphics-across-both-views"></a>Conseil pour le rendu des graphiques sur les deux vues

Si votre application doit implémenter une certaine quantité de rendu dans DirectX pour la vue XAML dans Windows Mixed Reality, il est préférable de créer un convertisseur capable de fonctionner avec les deux vues. Le convertisseur doit être une instance qui est accessible à partir des deux vues, et il doit pouvoir basculer entre le rendu 2D et le rendu holographique. Ainsi, les ressources GPU ne sont chargées qu’une seule fois. cela réduit le temps de chargement, l’impact sur la mémoire et la quantité de ressources à échanger lors du basculement des vues.
