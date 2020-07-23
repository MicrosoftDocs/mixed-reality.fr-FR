---
title: Streaming dans Unreal
description: Guide de streaming dans Unreal vers HoloLens 2
author: sw5813
ms.author: suwu
ms.date: 7/10/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, streaming, PC, communication à distance d’applications holographiques, holographic remoting player, documentation
appliesto:
- HoloLens
- HoloLens 2
ms.openlocfilehash: d25efbcf83e45749cc4eb8b99581b71105c59c9d
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86303530"
---
# <a name="streaming-in-unreal"></a><span data-ttu-id="e7844-104">Streaming dans Unreal</span><span class="sxs-lookup"><span data-stu-id="e7844-104">Streaming in Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="e7844-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="e7844-105">Overview</span></span>
<span data-ttu-id="e7844-106">Le streaming à partir d’un PC vers HoloLens offre deux avantages majeurs :</span><span class="sxs-lookup"><span data-stu-id="e7844-106">Streaming from a PC to HoloLens provides two major advantages:</span></span> 
* <span data-ttu-id="e7844-107">Il permet à votre application de réalité mixte de tirer parti de la puissance de calcul de vos PC.</span><span class="sxs-lookup"><span data-stu-id="e7844-107">It lets your mixed reality app take advantage of your PCs computational power.</span></span> 
* <span data-ttu-id="e7844-108">Il permet d’accélérer l’itération du développement.</span><span class="sxs-lookup"><span data-stu-id="e7844-108">It helps speed up development iteration time.</span></span> 

<span data-ttu-id="e7844-109">Pour commencer, vous devez télécharger [Holographic Remoting Player](holographic-remoting-player.md) sur votre appareil HoloLens.</span><span class="sxs-lookup"><span data-stu-id="e7844-109">To get started, you'll need to download the [Holographic Remoting Player](holographic-remoting-player.md) to your HoloLens device.</span></span> <span data-ttu-id="e7844-110">Cela permet à votre application de diffuser directement sur le lecteur de communication à distance sur votre HoloLens à partir des sources suivantes :</span><span class="sxs-lookup"><span data-stu-id="e7844-110">This allows your app to stream  directly to the remoting player on your HoloLens from the following sources:</span></span>

* <span data-ttu-id="e7844-111">L’éditeur Unreal Engine</span><span class="sxs-lookup"><span data-stu-id="e7844-111">The Unreal Engine editor</span></span>
* <span data-ttu-id="e7844-112">Un exécutable Windows empaqueté</span><span class="sxs-lookup"><span data-stu-id="e7844-112">A packaged Windows executable</span></span> 

<span data-ttu-id="e7844-113">Lors du streaming, vous avez accès à presque toutes les mêmes fonctionnalités HoloLens que lors de l’exécution d’une application sur un appareil.</span><span class="sxs-lookup"><span data-stu-id="e7844-113">When streaming, you have access to almost all of the same HoloLens capabilities as you would when running an application on a device.</span></span> <span data-ttu-id="e7844-114">Cela comprend notamment le [suivi de la main](unreal-hand-tracking.md) (si vous êtes sur un HoloLens 2), le [mappage spatial](unreal-spatial-mapping.md) et les [ancres spatiales](unreal-spatial-anchors.md), mais pas les fonctionnalités mentionnées dans cette [liste de limitations](holographic-remoting-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e7844-114">This includes [hand joint tracking](unreal-hand-tracking.md) (if you're on a HoloLens 2), [spatial mapping](unreal-spatial-mapping.md), and [spatial anchors](unreal-spatial-anchors.md), but leaves out the features on this [list of limitations](holographic-remoting-troubleshooting.md).</span></span> 

> [!NOTE]
> * <span data-ttu-id="e7844-115">La qualité de streaming dépend fortement de la puissance de votre réseau Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="e7844-115">Streaming quality is highly dependent on the strength of your wifi network.</span></span>
> * <span data-ttu-id="e7844-116">Toutes les fonctionnalités sont automatiquement activées pour le lecteur de communication à distance holographique.</span><span class="sxs-lookup"><span data-stu-id="e7844-116">All capabilities are automatically enabled for the holographic remoting player.</span></span> <span data-ttu-id="e7844-117">Si vous trouvez une fonctionnalité qui nécessite l’autorisation de l’utilisateur (par exemple le suivi oculaire) à utiliser sur le streaming mais pas lors de l’exécution sur l’appareil, vérifiez que vous avez activé les fonctionnalités appropriées dans les paramètres de votre projet.</span><span class="sxs-lookup"><span data-stu-id="e7844-117">If you find a capability that requires user permission (ex: eye tracking) to be working over streaming but not when running on device, check to ensure you've enabled the proper capabilities under your project settings.</span></span>

## <a name="device-support"></a><span data-ttu-id="e7844-118">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="e7844-118">Device support</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="e7844-119"><strong>Source</strong></span><span class="sxs-lookup"><span data-stu-id="e7844-119"><strong>Source</strong></span></span></td>
        <td><span data-ttu-id="e7844-120"><a href="https://docs.microsoft.com/hololens/hololens1-hardware"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="e7844-120"><a href="https://docs.microsoft.com/hololens/hololens1-hardware"><strong>HoloLens 1st Gen</strong></a></span></span></td>
        <td><span data-ttu-id="e7844-121"><a href="https://www.microsoft.com/hololens/hardware"><strong>HoloLens 2</strong></a></span><span class="sxs-lookup"><span data-stu-id="e7844-121"><a href="https://www.microsoft.com/hololens/hardware"><strong>HoloLens 2</strong></a></span></span></td>
        <td><span data-ttu-id="e7844-122"><strong>Casques immersifs</strong></span><span class="sxs-lookup"><span data-stu-id="e7844-122"><strong>Immersive Headsets</strong></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="e7844-123">Éditeur Unreal</span><span class="sxs-lookup"><span data-stu-id="e7844-123">Unreal editor</span></span></td>
        <td><span data-ttu-id="e7844-124">✔️</span><span class="sxs-lookup"><span data-stu-id="e7844-124">✔️</span></span></td>
        <td><span data-ttu-id="e7844-125">✔️</span><span class="sxs-lookup"><span data-stu-id="e7844-125">✔️</span></span></td>
        <td>❌</td>
    </tr>
    <tr>
        <td><span data-ttu-id="e7844-126">Package Windows</span><span class="sxs-lookup"><span data-stu-id="e7844-126">Windows package</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="e7844-127">✔️</span><span class="sxs-lookup"><span data-stu-id="e7844-127">✔️</span></span></td>
        <td>❌</td>
    </tr>

</table>

## <a name="streaming-from-the-unreal-editor"></a><span data-ttu-id="e7844-128">Streaming à partir de l’éditeur Unreal</span><span class="sxs-lookup"><span data-stu-id="e7844-128">Streaming from the Unreal editor</span></span>

<span data-ttu-id="e7844-129">En tant que développeur, vous constaterez que le streaming de l’éditeur Unreal vers votre appareil HoloLens offre de gros avantages lors des tests ; en effet, vous n’avez plus besoin d’attendre que votre application soit générée et déployée avant d’essayer vos mises à jour.</span><span class="sxs-lookup"><span data-stu-id="e7844-129">As a developer, you'll find that streaming from the Unreal editor to your HoloLens device provides big benefits when testing, namely that you no longer have to wait for your app to build and deploy before trying out your updates.</span></span>

<span data-ttu-id="e7844-130">Vous trouverez des instructions détaillées sur le [streaming à partir de l’éditeur Unreal](unreal-uxt-ch6.md#device-only-streaming) dans la dernière section de la séries de tutoriels Bien démarrer avec Unreal.</span><span class="sxs-lookup"><span data-stu-id="e7844-130">You can find detailed instructions on [streaming from the Unreal editor](unreal-uxt-ch6.md#device-only-streaming) in the last section of the Getting Started with Unreal tutorial series.</span></span>

## <a name="streaming-from-a-packaged-windows-executable"></a><span data-ttu-id="e7844-131">Streaming à partir d’un exécutable Windows empaqueté</span><span class="sxs-lookup"><span data-stu-id="e7844-131">Streaming from a packaged Windows executable</span></span>

<span data-ttu-id="e7844-132">À partir d’Unreal 4.25.1, vous pouvez diffuser votre application sur un appareil HoloLens 2 à partir d’un exécutable Windows empaqueté en effectuant les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="e7844-132">As of Unreal 4.25.1, you can stream your app to a HoloLens 2 device from a packaged Windows executable by following the steps below:</span></span> 

1. <span data-ttu-id="e7844-133">Accédez à **File > Package Project > Windows** dans le menu de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="e7844-133">Go to **File > Package Project > Windows** in the editor menu.</span></span> 
    * <span data-ttu-id="e7844-134">Choisissez un emplacement où enregistrer votre package, puis cliquez sur **Select Folder** (Sélectionner un dossier).</span><span class="sxs-lookup"><span data-stu-id="e7844-134">Choose a location to save your package and click **Select Folder**.</span></span>

2. <span data-ttu-id="e7844-135">Une fois la génération du package terminée, ouvrez **Holographic Remoting Player** sur votre HoloLens 2 et prenez note de l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="e7844-135">Once the package has finished building, open the **Holographic Remoting Player** on your HoloLens 2 and make note of the IP Address.</span></span> 
3. <span data-ttu-id="e7844-136">Laissez **Holographic Remoting Player** ouvert et utilisez l’invite de ligne de commande pour :</span><span class="sxs-lookup"><span data-stu-id="e7844-136">Leave the **Holographic Remoting Player** open and use the command line prompt to:</span></span> 
    * <span data-ttu-id="e7844-137">Basculer vers le répertoire local où vous avez enregistré votre package.</span><span class="sxs-lookup"><span data-stu-id="e7844-137">cd into the local directory where you saved your package.</span></span>
    * <span data-ttu-id="e7844-138">Entrez la commande suivante : ```<App Name>.exe -vr -HoloLensRemoting=<IP Address>```</span><span class="sxs-lookup"><span data-stu-id="e7844-138">Enter the following command: ```<App Name>.exe -vr -HoloLensRemoting=<IP Address>```</span></span>

> [!NOTE]
> <span data-ttu-id="e7844-139">Le nom de l’application dans les paramètres de votre projet doit être utilisé automatiquement pour créer le package Windows.</span><span class="sxs-lookup"><span data-stu-id="e7844-139">The application name in your project settings should be automatically used to create the Windows package.</span></span> <span data-ttu-id="e7844-140">Si les noms diffèrent pour une raison ou une autre, utilisez le nom de l’exécutable Windows à l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="e7844-140">If these are different for some reason, use the Windows executable name in the command prompt.</span></span>

<span data-ttu-id="e7844-141">Appuyez sur Entrée ; le streaming de votre application commence.</span><span class="sxs-lookup"><span data-stu-id="e7844-141">Hit enter and watch your application start streaming!</span></span>

## <a name="see-also"></a><span data-ttu-id="e7844-142">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e7844-142">See also</span></span>
* [<span data-ttu-id="e7844-143">Historique des versions de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="e7844-143">Holographic remoting version history</span></span>](holographic-remoting-version-history.md)
* [<span data-ttu-id="e7844-144">Écriture d’une application de lecteur de communication à distance holographique personnalisée</span><span class="sxs-lookup"><span data-stu-id="e7844-144">Writing a custom Holographic Remoting player app</span></span>](holographic-remoting-create-player.md)
* [<span data-ttu-id="e7844-145">Établissement d’une connexion sécurisée avec la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="e7844-145">Establishing a secure connection with Holographic Remoting</span></span>](holographic-remoting-secure-connection.md)
