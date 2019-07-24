---
title: Achats dans l'application
description: Les achats dans l’application sont pris en charge dans les applications de réalité mixte, mais il existe un certain travail pour les configurer.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: achats dans l’application, hololens
ms.openlocfilehash: bc96893d1777e94295285736982fd9a7167240a4
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63515294"
---
# <a name="in-app-purchases"></a>Achats dans l'application

Les achats dans l’application sont pris en charge dans HoloLens, mais il existe un certain travail pour les configurer.

Pour tirer parti de la fonctionnalité d’achat d’applications, vous devez:
* Créer une [vue 2D](app-views.md) XAML pour qu’elle apparaisse en tant que ardoise
* Basculez vers celui-ci pour activer le placement, ce qui laisse la vue immersive
* Appeler l’API: await [CurrentApp. RequestProductPurchaseAsync ("DurableItemIAPName");](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp#Windows_ApplicationModel_Store_CurrentApp_RequestProductPurchaseAsync_System_String_)

Cette API affiche la fenêtre contextuelle du système d’exploitation Windows qui affiche le nom, la description et le prix de l’achat dans l’application. L’utilisateur peut ensuite choisir des options d’achat. Une fois l’action terminée, l’application doit présenter une interface utilisateur qui permet à l’utilisateur de revenir à sa [vue immersive](app-views.md).

Pour les applications ciblant des casques immersifs de la réalité Windows mixte basés sur le bureau, il n’est pas nécessaire de basculer manuellement vers une vue XAML avant d’appeler l’API RequestProductPurchaseAsync.
