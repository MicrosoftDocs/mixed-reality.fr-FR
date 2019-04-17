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
# <a name="in-app-purchases"></a><span data-ttu-id="d462e-104">Achats dans l'application</span><span class="sxs-lookup"><span data-stu-id="d462e-104">In-app purchases</span></span>

<span data-ttu-id="d462e-105">Achats dans l’application sont prises en charge dans HoloLens, mais certaines tâches pour les configurer.</span><span class="sxs-lookup"><span data-stu-id="d462e-105">In-app purchases are supported in HoloLens, but there is some work to set them up.</span></span>

<span data-ttu-id="d462e-106">Afin de tirer parti de l’achat d’application en fonctionnalités, vous devez :</span><span class="sxs-lookup"><span data-stu-id="d462e-106">In order to leverage the in app-purchase functionality, you must:</span></span>
* <span data-ttu-id="d462e-107">Créer un XAML [vue en 2D](app-views.md) apparaisse comme une ardoise</span><span class="sxs-lookup"><span data-stu-id="d462e-107">Create a XAML [2D view](app-views.md) to appear as a slate</span></span>
* <span data-ttu-id="d462e-108">Basculez vers celui-ci pour activer la sélection élective, ce qui laisse la vue immersive</span><span class="sxs-lookup"><span data-stu-id="d462e-108">Switch to it to activate placement, which leaves the immersive view</span></span>
* <span data-ttu-id="d462e-109">Appeler l’API : await [CurrentApp.RequestProductPurchaseAsync("DurableItemIAPName") ;](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp#Windows_ApplicationModel_Store_CurrentApp_RequestProductPurchaseAsync_System_String_)</span><span class="sxs-lookup"><span data-stu-id="d462e-109">Call the API: await [CurrentApp.RequestProductPurchaseAsync("DurableItemIAPName");](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store.currentapp#Windows_ApplicationModel_Store_CurrentApp_RequestProductPurchaseAsync_System_String_)</span></span>

<span data-ttu-id="d462e-110">Cette API fait apparaître la fenêtre contextuelle du système d’exploitation Windows stockée qui affiche le nom de l’achat dans l’application, la description et le prix.</span><span class="sxs-lookup"><span data-stu-id="d462e-110">This API will bring up the stock Windows OS popup that shows the in-app purchase name, description, and price.</span></span> <span data-ttu-id="d462e-111">L’utilisateur peut alors choisir les options d’achat.</span><span class="sxs-lookup"><span data-stu-id="d462e-111">The user can then choose purchase options.</span></span> <span data-ttu-id="d462e-112">Une fois que l’action est terminée, l’application doit présenter l’interface utilisateur qui permet à l’utilisateur revenir à son [vue immersive](app-views.md).</span><span class="sxs-lookup"><span data-stu-id="d462e-112">Once the action is completed, the app will need to present UI which allows the user to switch back to its [immersive view](app-views.md).</span></span>

<span data-ttu-id="d462e-113">Pour les applications ciblant des casques IMMERSIFS de réalité mixte Windows sur le bureau, il n’est pas nécessaire de basculer manuellement vers une vue XAML avant d’appeler l’API RequestProductPurchaseAsync.</span><span class="sxs-lookup"><span data-stu-id="d462e-113">For apps targeting desktop-based Windows Mixed Reality immersive headsets, it is not required to manually switch to a XAML view before calling the RequestProductPurchaseAsync API.</span></span>
