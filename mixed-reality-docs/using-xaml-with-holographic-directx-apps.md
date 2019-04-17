---
title: À l’aide de XAML avec les applications DirectX HOLOGRAPHIQUE
description: Explique l’impact du changement entre les affichages XAML 2D et immersives dans votre application DirectX et comment utiliser efficacement des modes un XAML et immersives.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: afficher les applications en réalité mixte, UWP, Windows management, xaml, clavier, procédure pas à pas, DirectX
ms.openlocfilehash: 32b2feea0cb6b8aba972c1772451ca7b5b9946d5
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593699"
---
# <a name="using-xaml-with-holographic-directx-apps"></a>À l’aide de XAML avec les applications DirectX HOLOGRAPHIQUE

Cette rubrique explique l’impact du changement entre [2D vues XAML et immersives](app-views.md) dans votre application DirectX et comment utiliser efficacement des modes un XAML et immersives.

## <a name="xaml-view-switching-overview"></a>Changement de vue d’ensemble de la vue XAML

Sur HoloLens, une application générale immersive qui peut afficher ultérieurement une vue XAML 2D doit initialiser cette vue XAML tout d’abord et passer immédiatement à une vue immersif à partir de là. Cela signifie que le XAML doit charger avant que votre application peut faire quoi que ce soit. Par conséquent, il y aura une légère augmentation de votre temps de démarrage et XAML continue d’occuper l’espace de mémoire dans le processus de votre application pendant qu’il est dans l’arrière-plan. la quantité de mémoire utilisation dépend de ce que votre application fait avec XAML avant de passer au mode natif et de délai de démarrage. Si vous ne faites rien dans votre code dans un premier temps, à ceci près démarrer votre vue immersive de démarrage XAML, l’impact devrait être mineur. En outre, étant donné que votre rendu holographique est effectuée directement à la vue immersive, vous permet d’éviter des restrictions liées à XAML sur ce rendu.

Notez que le compte de l’utilisation de la mémoire pour l’UC et GPU. Direct3D 11 est en mesure d’échange de mémoire virtuelle graphique, mais il peut ne pas pouvoir remplacer tout ou partie des ressources XAML GPU et il peut y avoir une baisse des performances notable. Dans les deux cas, ne pas le chargement des fonctionnalités XAML, vous ne devez laisser plus de place pour votre application et fournir une meilleure expérience.

## <a name="xaml-view-switching-workflow"></a>Changement de flux de travail de la vue XAML

Le flux de travail pour une application qui accède directement à partir de XAML au mode immersif est comme suit :
* Démarrage de l’application dans la vue XAML 2D.
* Séquence de démarrage de l’application XAML détecte si le système actuel prend en charge le rendu HOLOGRAPHIQUE :
* Dans ce cas, l’application crée la vue immersive et rend immédiatement au premier plan. Le chargement XAML est ignoré pour tout élément n’est pas nécessaire sur les appareils Windows Mixed Reality, y compris les classes de rendu et de la ressource lors du chargement dans la vue XAML. Si l’application est à l’aide de XAML pour l’entrée au clavier, cette page d’entrée doit toujours être créée.
* Si ce n’est pas le cas, la vue XAML peut poursuivre d’entreprise comme d’habitude.

## <a name="tip-for-rendering-graphics-across-both-views"></a>Conseil pour restituer des graphiques sur les deux affichages

Si votre application doit implémenter une certaine quantité de rendu dans DirectX pour la vue XAML en réalité mixte Windows, la meilleure solution consiste à créer un convertisseur qui peut fonctionner avec les deux vues. Le convertisseur doit être une instance qui est accessible à partir de ces deux vues, et il doit être en mesure de basculer entre le rendu 2D et HOLOGRAPHIQUE. De cette façon, les ressources GPU sont chargés uniquement une fois - cela réduit temps de chargement, impact sur la mémoire et la quantité de ressources à échanger en changeant d’affichage.
