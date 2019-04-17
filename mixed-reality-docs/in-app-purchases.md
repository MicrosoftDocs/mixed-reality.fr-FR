---
title: Achats dans l'application
description: Achats dans l’application sont prises en charge dans les applications de réalité mixte, mais certaines tâches pour les configurer.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: achats dans l’application, hololens
ms.openlocfilehash: bc96893d1777e94295285736982fd9a7167240a4
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595782"
---
# <a name="in-app-purchases"></a>Achats dans l'application

Achats dans l’application sont prises en charge dans HoloLens, mais certaines tâches pour les configurer.

Afin de tirer parti de l’achat d’application en fonctionnalités, vous devez :
* Créer un XAML [vue en 2D](app-views.md) apparaisse comme une ardoise
* Basculez vers celui-ci pour activer la sélection élective, ce qui laisse la vue immersive
* Appeler l’API : await [CurrentApp.RequestProductPurchaseAsync("DurableItemIAPName") ;](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp#Windows_ApplicationModel_Store_CurrentApp_RequestProductPurchaseAsync_System_String_)

Cette API fait apparaître la fenêtre contextuelle du système d’exploitation Windows stockée qui affiche le nom de l’achat dans l’application, la description et le prix. L’utilisateur peut alors choisir les options d’achat. Une fois que l’action est terminée, l’application doit présenter l’interface utilisateur qui permet à l’utilisateur revenir à son [vue immersive](app-views.md).

Pour les applications ciblant des casques IMMERSIFS de réalité mixte Windows sur le bureau, il n’est pas nécessaire de basculer manuellement vers une vue XAML avant d’appeler l’API RequestProductPurchaseAsync.
