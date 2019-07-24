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
# <a name="in-app-purchases"></a><span data-ttu-id="af303-104">Achats dans l'application</span><span class="sxs-lookup"><span data-stu-id="af303-104">In-app purchases</span></span>

<span data-ttu-id="af303-105">Les achats dans l’application sont pris en charge dans HoloLens, mais il existe un certain travail pour les configurer.</span><span class="sxs-lookup"><span data-stu-id="af303-105">In-app purchases are supported in HoloLens, but there is some work to set them up.</span></span>

<span data-ttu-id="af303-106">Pour tirer parti de la fonctionnalité d’achat d’applications, vous devez:</span><span class="sxs-lookup"><span data-stu-id="af303-106">In order to leverage the in app-purchase functionality, you must:</span></span>
* <span data-ttu-id="af303-107">Créer une [vue 2D](app-views.md) XAML pour qu’elle apparaisse en tant que ardoise</span><span class="sxs-lookup"><span data-stu-id="af303-107">Create a XAML [2D view](app-views.md) to appear as a slate</span></span>
* <span data-ttu-id="af303-108">Basculez vers celui-ci pour activer le placement, ce qui laisse la vue immersive</span><span class="sxs-lookup"><span data-stu-id="af303-108">Switch to it to activate placement, which leaves the immersive view</span></span>
* <span data-ttu-id="af303-109">Appeler l’API: await [CurrentApp. RequestProductPurchaseAsync ("DurableItemIAPName");](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp#Windows_ApplicationModel_Store_CurrentApp_RequestProductPurchaseAsync_System_String_)</span><span class="sxs-lookup"><span data-stu-id="af303-109">Call the API: await [CurrentApp.RequestProductPurchaseAsync("DurableItemIAPName");](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp#Windows_ApplicationModel_Store_CurrentApp_RequestProductPurchaseAsync_System_String_)</span></span>

<span data-ttu-id="af303-110">Cette API affiche la fenêtre contextuelle du système d’exploitation Windows qui affiche le nom, la description et le prix de l’achat dans l’application.</span><span class="sxs-lookup"><span data-stu-id="af303-110">This API will bring up the stock Windows OS popup that shows the in-app purchase name, description, and price.</span></span> <span data-ttu-id="af303-111">L’utilisateur peut ensuite choisir des options d’achat.</span><span class="sxs-lookup"><span data-stu-id="af303-111">The user can then choose purchase options.</span></span> <span data-ttu-id="af303-112">Une fois l’action terminée, l’application doit présenter une interface utilisateur qui permet à l’utilisateur de revenir à sa [vue immersive](app-views.md).</span><span class="sxs-lookup"><span data-stu-id="af303-112">Once the action is completed, the app will need to present UI which allows the user to switch back to its [immersive view](app-views.md).</span></span>

<span data-ttu-id="af303-113">Pour les applications ciblant des casques immersifs de la réalité Windows mixte basés sur le bureau, il n’est pas nécessaire de basculer manuellement vers une vue XAML avant d’appeler l’API RequestProductPurchaseAsync.</span><span class="sxs-lookup"><span data-stu-id="af303-113">For apps targeting desktop-based Windows Mixed Reality immersive headsets, it is not required to manually switch to a XAML view before calling the RequestProductPurchaseAsync API.</span></span>
