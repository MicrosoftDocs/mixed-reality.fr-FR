---
title: Mode de lecture Unity
description: Utilisation du mode lecture dans l’éditeur Unity pour afficher un aperçu de vos modifications sur un appareil sans déployer une application.
author: JonMLyons
ms.author: jlyons
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, communication à distance, communication à distance holographique, lecteur de communication à distance holographique
ms.openlocfilehash: c118c4af61c6eb2706ef851a6654c18ff7313453
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63548730"
---
# <a name="unity-play-mode"></a><span data-ttu-id="6144d-104">Mode de lecture Unity</span><span class="sxs-lookup"><span data-stu-id="6144d-104">Unity Play Mode</span></span>

<span data-ttu-id="6144d-105">Un moyen rapide de travailler sur votre projet Unity consiste à utiliser le «mode lecture».</span><span class="sxs-lookup"><span data-stu-id="6144d-105">A fast way to work on your Unity project is to use "Play Mode".</span></span> <span data-ttu-id="6144d-106">Cela exécute votre application localement dans l’éditeur Unity sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="6144d-106">This runs your app locally in the Unity editor on your PC.</span></span> <span data-ttu-id="6144d-107">Unity utilise la communication à distance holographique pour offrir un moyen rapide d’afficher un aperçu de votre contenu sur un appareil HoloLens réel.</span><span class="sxs-lookup"><span data-stu-id="6144d-107">Unity uses Holographic Remoting to provide a fast way to preview your content on a real HoloLens device.</span></span>

## <a name="unity-play-mode-with-holographic-remoting"></a><span data-ttu-id="6144d-108">Mode de lecture Unity avec accès distant holographique</span><span class="sxs-lookup"><span data-stu-id="6144d-108">Unity Play Mode with Holographic Remoting</span></span>

<span data-ttu-id="6144d-109">Avec la communication à distance holographique, vous pouvez expérimenter votre application sur le HoloLens, pendant qu’elle s’exécute dans l’éditeur Unity sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="6144d-109">With Holographic Remoting, you can experience your app on the HoloLens, while it runs in the Unity editor on your PC.</span></span> <span data-ttu-id="6144d-110">L’entrée de pointage, de mouvement, de voix et de mappage spatial est envoyée de votre HoloLens à votre PC.</span><span class="sxs-lookup"><span data-stu-id="6144d-110">Gaze, gesture, voice, and spatial mapping input is sent from your HoloLens to your PC.</span></span> <span data-ttu-id="6144d-111">Les frames rendus sont ensuite renvoyés à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="6144d-111">Rendered frames are then sent back to your HoloLens.</span></span> <span data-ttu-id="6144d-112">C’est un excellent moyen de déboguer rapidement votre application sans générer et déployer un projet complet.</span><span class="sxs-lookup"><span data-stu-id="6144d-112">This is a great way to quickly debug your app without building and deploying a full project.</span></span>
1. <span data-ttu-id="6144d-113">Sur votre HoloLens, accédez à la **Microsoft Store** et installez l’application de **[lecteur de communication à distance holographique](https://www.microsoft.com/store/p/holographic-remoting-player/9nblggh4sv40)** .</span><span class="sxs-lookup"><span data-stu-id="6144d-113">On your HoloLens, go to the **Microsoft Store** and install the **[Holographic Remoting Player](https://www.microsoft.com/store/p/holographic-remoting-player/9nblggh4sv40)** app.</span></span>
2. <span data-ttu-id="6144d-114">Sur votre HoloLens, démarrez l’application de **lecteur de communication à distance holographique** .</span><span class="sxs-lookup"><span data-stu-id="6144d-114">On your HoloLens, start the **Holographic Remoting Player** app.</span></span>
3. <span data-ttu-id="6144d-115">Dans Unity, accédez au menu **fenêtre** et sélectionnez **émulation holographique**.</span><span class="sxs-lookup"><span data-stu-id="6144d-115">In Unity, go to the **Window** menu and select **Holographic Emulation**.</span></span>
4. <span data-ttu-id="6144d-116">Définissez le **mode d’émulation** à **distant sur appareil**.</span><span class="sxs-lookup"><span data-stu-id="6144d-116">Set **Emulation Mode** to **Remote to Device**.</span></span>
5. <span data-ttu-id="6144d-117">Pour **ordinateur distant**, entrez l’adresse IP de votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="6144d-117">For **Remote Machine**, enter the IP address of your HoloLens.</span></span>
6. <span data-ttu-id="6144d-118">Cliquer sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="6144d-118">Click **Connect**.</span></span> <span data-ttu-id="6144d-119">Le changement d' **État** de la connexion doit être défini sur **connecté** et l’écran s’affichera vide dans HoloLens.</span><span class="sxs-lookup"><span data-stu-id="6144d-119">You should see **Connection Status** change to **Connected** and see the screen go blank in the HoloLens.</span></span>
7. <span data-ttu-id="6144d-120">Cliquez sur le bouton **lecture** pour démarrer le mode lecture et tester l’application sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="6144d-120">Click the **Play** button to start Play Mode and experience the app on your HoloLens.</span></span>

<span data-ttu-id="6144d-121">La communication à distance holographique requiert une connexion rapide PC et Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="6144d-121">Holographic Remoting requires a fast PC and Wi-Fi connection.</span></span> <span data-ttu-id="6144d-122">Pour plus d’informations, consultez [lecteur de communication à distance holographique](holographic-remoting-player.md) .</span><span class="sxs-lookup"><span data-stu-id="6144d-122">See [Holographic Remoting Player](holographic-remoting-player.md) for full details.</span></span>

<span data-ttu-id="6144d-123">Pour de meilleurs résultats, assurez-vous que votre application définit correctement le [point de focus](focus-point-in-unity.md).</span><span class="sxs-lookup"><span data-stu-id="6144d-123">For best results, make sure your app properly sets the [focus point](focus-point-in-unity.md).</span></span> <span data-ttu-id="6144d-124">Cela permet à la communication à distance holographique d’adapter au mieux votre scène à la latence de votre connexion sans fil.</span><span class="sxs-lookup"><span data-stu-id="6144d-124">This helps Holographic Remoting to best adapt your scene to the latency of your wireless connection.</span></span>

## <a name="see-also"></a><span data-ttu-id="6144d-125">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6144d-125">See Also</span></span>
* [<span data-ttu-id="6144d-126">Holographic Remoting Player</span><span class="sxs-lookup"><span data-stu-id="6144d-126">Holographic Remoting Player</span></span>](holographic-remoting-player.md)
