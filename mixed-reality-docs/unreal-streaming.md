---
title: Streaming dans Unreal
description: Guide de streaming dans Unreal vers HoloLens 2
author: suwu
ms.author: suwu
ms.date: 6/8/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, streaming, PC, communication à distance d’applications holographiques, holographic remoting player, documentation
appliesto:
- HoloLens
- HoloLens 2
ms.openlocfilehash: 78a019f5b74b254c1f32ec85dc639df47648555f
ms.sourcegitcommit: ff0e89b07d0b4a945967d64c5b8845a21dc5f476
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84888910"
---
# <a name="streaming-in-unreal"></a><span data-ttu-id="afdea-104">Streaming dans Unreal</span><span class="sxs-lookup"><span data-stu-id="afdea-104">Streaming in Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="afdea-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="afdea-105">Overview</span></span>
<span data-ttu-id="afdea-106">Le streaming à partir d’un PC vers HoloLens offre deux avantages majeurs :</span><span class="sxs-lookup"><span data-stu-id="afdea-106">Streaming from a PC to HoloLens provides two major advantages:</span></span> 
* <span data-ttu-id="afdea-107">Il permet à votre application de réalité mixte de tirer parti de la puissance de calcul de vos PC.</span><span class="sxs-lookup"><span data-stu-id="afdea-107">It lets your mixed reality app take advantage of your PCs computational power.</span></span> 
* <span data-ttu-id="afdea-108">Il permet d’accélérer l’itération du développement.</span><span class="sxs-lookup"><span data-stu-id="afdea-108">It helps speed up development iteration time.</span></span> 

<span data-ttu-id="afdea-109">Pour commencer, vous devez télécharger [Holographic Remoting Player](holographic-remoting-player.md) sur votre appareil HoloLens.</span><span class="sxs-lookup"><span data-stu-id="afdea-109">To get started, you'll need to download the [Holographic Remoting Player](holographic-remoting-player.md) to your HoloLens device.</span></span> <span data-ttu-id="afdea-110">Cela permet à votre application de diffuser directement sur le lecteur de communication à distance sur votre HoloLens à partir des sources suivantes :</span><span class="sxs-lookup"><span data-stu-id="afdea-110">This allows your app to stream  directly to the remoting player on your HoloLens from the following sources:</span></span>

* <span data-ttu-id="afdea-111">L’éditeur Unreal Engine</span><span class="sxs-lookup"><span data-stu-id="afdea-111">The Unreal Engine editor</span></span>
* <span data-ttu-id="afdea-112">Un exécutable Windows empaqueté</span><span class="sxs-lookup"><span data-stu-id="afdea-112">A packaged Windows executable</span></span> 

<span data-ttu-id="afdea-113">Lors du streaming, vous avez accès à presque toutes les mêmes fonctionnalités HoloLens que lors de l’exécution d’une application sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="afdea-113">When streaming, you have access to almost all of the same HoloLens capabilities as you would when running an application on a device.</span></span> <span data-ttu-id="afdea-114">Cela comprend notamment le [suivi de la main](unreal-hand-tracking.md) (si vous êtes sur un HoloLens 2), le [mappage spatial](unreal-spatial-mapping.md) et les [ancres spatiales](unreal-spatial-anchors.md), mais pas les fonctionnalités mentionnées dans cette [liste de limitations](holographic-remoting-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="afdea-114">This includes [hand joint tracking](unreal-hand-tracking.md) (if you're on a HoloLens 2), [spatial mapping](unreal-spatial-mapping.md), and [spatial anchors](unreal-spatial-anchors.md), but leaves out the features on this [list of limitations](holographic-remoting-troubleshooting.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="afdea-115">La qualité de streaming dépend fortement de la puissance de votre réseau Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="afdea-115">Streaming quality is highly dependent on the strength of your wifi network.</span></span>

## <a name="device-support"></a><span data-ttu-id="afdea-116">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="afdea-116">Device support</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="afdea-117"><strong>Source</strong></span><span class="sxs-lookup"><span data-stu-id="afdea-117"><strong>Source</strong></span></span></td>
        <td><span data-ttu-id="afdea-118"><a href="https://docs.microsoft.com/hololens/hololens1-hardware"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="afdea-118"><a href="https://docs.microsoft.com/hololens/hololens1-hardware"><strong>HoloLens 1st Gen</strong></a></span></span></td>
        <td><span data-ttu-id="afdea-119"><a href="https://www.microsoft.com/hololens/hardware"><strong>HoloLens 2</strong></a></span><span class="sxs-lookup"><span data-stu-id="afdea-119"><a href="https://www.microsoft.com/hololens/hardware"><strong>HoloLens 2</strong></a></span></span></td>
        <td><span data-ttu-id="afdea-120"><strong>Casques immersifs</strong></span><span class="sxs-lookup"><span data-stu-id="afdea-120"><strong>Immersive Headsets</strong></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="afdea-121">Éditeur Unreal</span><span class="sxs-lookup"><span data-stu-id="afdea-121">Unreal editor</span></span></td>
        <td><span data-ttu-id="afdea-122">✔</span><span class="sxs-lookup"><span data-stu-id="afdea-122">✔</span></span></td>
        <td><span data-ttu-id="afdea-123">✔️</span><span class="sxs-lookup"><span data-stu-id="afdea-123">✔️</span></span></td>
        <td>❌</td>
    </tr>
    <tr>
        <td><span data-ttu-id="afdea-124">Package Windows</span><span class="sxs-lookup"><span data-stu-id="afdea-124">Windows package</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="afdea-125">✔️</span><span class="sxs-lookup"><span data-stu-id="afdea-125">✔️</span></span></td>
        <td>❌</td>
    </tr>

</table>

## <a name="streaming-from-the-unreal-editor"></a><span data-ttu-id="afdea-126">Streaming à partir de l’éditeur Unreal</span><span class="sxs-lookup"><span data-stu-id="afdea-126">Streaming from the Unreal editor</span></span>

<span data-ttu-id="afdea-127">En tant que développeur, vous constaterez que le streaming de l’éditeur Unreal vers votre appareil HoloLens offre de gros avantages lors des tests ; en effet, vous n’avez plus besoin d’attendre que votre application soit générée et déployée avant d’essayer vos mises à jour.</span><span class="sxs-lookup"><span data-stu-id="afdea-127">As a developer, you'll find that streaming from the Unreal editor to your HoloLens device provides big benefits when testing, namely that you no longer have to wait for your app to build and deploy before trying out your updates.</span></span>

<span data-ttu-id="afdea-128">Vous trouverez des instructions détaillées sur le [streaming à partir de l’éditeur Unreal](unreal-uxt-ch6.md#device-only-streaming) dans la dernière section de la séries de tutoriels Bien démarrer avec Unreal.</span><span class="sxs-lookup"><span data-stu-id="afdea-128">You can find detailed instructions on [streaming from the Unreal editor](unreal-uxt-ch6.md#device-only-streaming) in the last section of the Getting Started with Unreal tutorial series.</span></span>

## <a name="streaming-from-a-packaged-windows-executable"></a><span data-ttu-id="afdea-129">Streaming à partir d’un exécutable Windows empaqueté</span><span class="sxs-lookup"><span data-stu-id="afdea-129">Streaming from a packaged Windows executable</span></span>

<span data-ttu-id="afdea-130">À partir d’Unreal 4.25.1, vous pouvez diffuser votre application sur un appareil HoloLens 2 à partir d’un exécutable Windows empaqueté en effectuant les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="afdea-130">As of Unreal 4.25.1, you can stream your app to a HoloLens 2 device from a packaged Windows executable by following the steps below:</span></span> 

1. <span data-ttu-id="afdea-131">Accédez à **File > Package Project > Windows** dans le menu de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="afdea-131">Go to **File > Package Project > Windows** in the editor menu.</span></span> 
    * <span data-ttu-id="afdea-132">Choisissez un emplacement où enregistrer votre package, puis cliquez sur **Select Folder** (Sélectionner un dossier).</span><span class="sxs-lookup"><span data-stu-id="afdea-132">Choose a location to save your package and click **Select Folder**.</span></span>

2. <span data-ttu-id="afdea-133">Une fois la génération du package terminée, ouvrez **Holographic Remoting Player** sur votre HoloLens 2 et prenez note de l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="afdea-133">Once the package has finished building, open the **Holographic Remoting Player** on your HoloLens 2 and make note of the IP Address.</span></span> 
3. <span data-ttu-id="afdea-134">Laissez **Holographic Remoting Player** ouvert et utilisez l’invite de ligne de commande pour :</span><span class="sxs-lookup"><span data-stu-id="afdea-134">Leave the **Holographic Remoting Player** open and use the command line prompt to:</span></span> 
    * <span data-ttu-id="afdea-135">Basculer vers le répertoire local où vous avez enregistré votre package.</span><span class="sxs-lookup"><span data-stu-id="afdea-135">cd into the local directory where you saved your package.</span></span>
    * <span data-ttu-id="afdea-136">Entrer la commande suivante : ```<App Name>.exe -vr -HoloLensRemoting=<IP Address>```</span><span class="sxs-lookup"><span data-stu-id="afdea-136">Enter the following command: ```<App Name>.exe -vr -HoloLensRemoting=<IP Address>```</span></span>

> [!NOTE]
> <span data-ttu-id="afdea-137">Le nom de l’application dans les paramètres de votre projet doit être utilisé automatiquement pour créer le package Windows.</span><span class="sxs-lookup"><span data-stu-id="afdea-137">The application name in your project settings should be automatically used to create the Windows package.</span></span> <span data-ttu-id="afdea-138">Si les noms diffèrent pour une raison ou une autre, utilisez le nom de l’exécutable Windows à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="afdea-138">If these are different for some reason, use the Windows executable name in the command prompt.</span></span>

<span data-ttu-id="afdea-139">Appuyez sur Entrée ; le streaming de votre application commence.</span><span class="sxs-lookup"><span data-stu-id="afdea-139">Hit enter and watch your application start streaming!</span></span>

## <a name="see-also"></a><span data-ttu-id="afdea-140">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="afdea-140">See also</span></span>
* [<span data-ttu-id="afdea-141">Historique des versions de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="afdea-141">Holographic remoting version history</span></span>](holographic-remoting-version-history.md)
* [<span data-ttu-id="afdea-142">Écriture d’une application de lecteur de communication à distance holographique personnalisée</span><span class="sxs-lookup"><span data-stu-id="afdea-142">Writing a custom Holographic Remoting player app</span></span>](holographic-remoting-create-player.md)
* [<span data-ttu-id="afdea-143">Établissement d’une connexion sécurisée avec la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="afdea-143">Establishing a secure connection with Holographic Remoting</span></span>](holographic-remoting-secure-connection.md)
