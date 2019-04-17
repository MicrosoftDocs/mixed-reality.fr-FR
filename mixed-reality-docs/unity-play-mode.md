---
title: Mode de jeu Unity
description: Utilise le Mode de lecture dans l’éditeur Unity pour prévisualiser vos modifications sur un appareil sans déploiement d’une application.
author: JonMLyons
ms.author: jlyons
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, communication à distance, communication à distance HOLOGRAPHIQUE, lecteur de communication à distance HOLOGRAPHIQUE
ms.openlocfilehash: c118c4af61c6eb2706ef851a6654c18ff7313453
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593355"
---
# <a name="unity-play-mode"></a><span data-ttu-id="d07e2-104">Mode de jeu Unity</span><span class="sxs-lookup"><span data-stu-id="d07e2-104">Unity Play Mode</span></span>

<span data-ttu-id="d07e2-105">Un moyen rapide pour travailler sur votre projet Unity consiste à utiliser le « Mode de lecture ».</span><span class="sxs-lookup"><span data-stu-id="d07e2-105">A fast way to work on your Unity project is to use "Play Mode".</span></span> <span data-ttu-id="d07e2-106">Il s’exécute votre application localement dans l’éditeur Unity sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="d07e2-106">This runs your app locally in the Unity editor on your PC.</span></span> <span data-ttu-id="d07e2-107">Unity utilise holographique de communication à distance pour fournir un moyen rapide pour afficher un aperçu de votre contenu sur un appareil HoloLens réel.</span><span class="sxs-lookup"><span data-stu-id="d07e2-107">Unity uses Holographic Remoting to provide a fast way to preview your content on a real HoloLens device.</span></span>

## <a name="unity-play-mode-with-holographic-remoting"></a><span data-ttu-id="d07e2-108">Mode de jeu Unity avec Remoting HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="d07e2-108">Unity Play Mode with Holographic Remoting</span></span>

<span data-ttu-id="d07e2-109">Avec la communication à distance HOLOGRAPHIQUE, vous pouvez tester votre application sur le HoloLens, pendant son exécution dans l’éditeur Unity sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="d07e2-109">With Holographic Remoting, you can experience your app on the HoloLens, while it runs in the Unity editor on your PC.</span></span> <span data-ttu-id="d07e2-110">Regards, mouvement, voix et entrée de mappage spatial est envoyé à partir de votre HoloLens à votre PC.</span><span class="sxs-lookup"><span data-stu-id="d07e2-110">Gaze, gesture, voice, and spatial mapping input is sent from your HoloLens to your PC.</span></span> <span data-ttu-id="d07e2-111">Restituées sont ensuite renvoyées à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d07e2-111">Rendered frames are then sent back to your HoloLens.</span></span> <span data-ttu-id="d07e2-112">Il s’agit d’un excellent moyen de déboguer rapidement votre application sans générer et déployer un projet complet.</span><span class="sxs-lookup"><span data-stu-id="d07e2-112">This is a great way to quickly debug your app without building and deploying a full project.</span></span>
1. <span data-ttu-id="d07e2-113">Sur votre HoloLens, accédez à la **Microsoft Store** et installer le **[HOLOGRAPHIQUE Player de communication à distance](https://www.microsoft.com/store/p/holographic-remoting-player/9nblggh4sv40)** application.</span><span class="sxs-lookup"><span data-stu-id="d07e2-113">On your HoloLens, go to the **Microsoft Store** and install the **[Holographic Remoting Player](https://www.microsoft.com/store/p/holographic-remoting-player/9nblggh4sv40)** app.</span></span>
2. <span data-ttu-id="d07e2-114">Sur votre HoloLens, démarrez le **HOLOGRAPHIQUE Player de communication à distance** application.</span><span class="sxs-lookup"><span data-stu-id="d07e2-114">On your HoloLens, start the **Holographic Remoting Player** app.</span></span>
3. <span data-ttu-id="d07e2-115">Dans Unity, accédez à la **fenêtre** menu et sélectionnez **émulation HOLOGRAPHIQUE**.</span><span class="sxs-lookup"><span data-stu-id="d07e2-115">In Unity, go to the **Window** menu and select **Holographic Emulation**.</span></span>
4. <span data-ttu-id="d07e2-116">Définissez **Mode d’émulation** à **à distance au périphérique**.</span><span class="sxs-lookup"><span data-stu-id="d07e2-116">Set **Emulation Mode** to **Remote to Device**.</span></span>
5. <span data-ttu-id="d07e2-117">Pour **Machine distante**, entrez l’adresse IP de votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d07e2-117">For **Remote Machine**, enter the IP address of your HoloLens.</span></span>
6. <span data-ttu-id="d07e2-118">Cliquer sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="d07e2-118">Click **Connect**.</span></span> <span data-ttu-id="d07e2-119">Vous devriez voir **état de la connexion** modifier à **connecté** et voir l’écran vide dans le HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d07e2-119">You should see **Connection Status** change to **Connected** and see the screen go blank in the HoloLens.</span></span>
7. <span data-ttu-id="d07e2-120">Cliquez sur le **lire** bouton pour démarrer le Mode de lecture et l’expérience de l’application sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d07e2-120">Click the **Play** button to start Play Mode and experience the app on your HoloLens.</span></span>

<span data-ttu-id="d07e2-121">Remoting HOLOGRAPHIQUE requiert une connexion rapide de PC et Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="d07e2-121">Holographic Remoting requires a fast PC and Wi-Fi connection.</span></span> <span data-ttu-id="d07e2-122">Consultez [HOLOGRAPHIQUE Player de communication à distance](holographic-remoting-player.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d07e2-122">See [Holographic Remoting Player](holographic-remoting-player.md) for full details.</span></span>

<span data-ttu-id="d07e2-123">Pour de meilleurs résultats, assurez-vous que votre application définit correctement le [concentrer point](focus-point-in-unity.md).</span><span class="sxs-lookup"><span data-stu-id="d07e2-123">For best results, make sure your app properly sets the [focus point](focus-point-in-unity.md).</span></span> <span data-ttu-id="d07e2-124">Cela permet une communication à distance HOLOGRAPHIQUE pour mieux adapter votre scène à la latence de votre connexion sans fil.</span><span class="sxs-lookup"><span data-stu-id="d07e2-124">This helps Holographic Remoting to best adapt your scene to the latency of your wireless connection.</span></span>

## <a name="see-also"></a><span data-ttu-id="d07e2-125">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d07e2-125">See Also</span></span>
* [<span data-ttu-id="d07e2-126">Lecteur de communication à distance HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="d07e2-126">Holographic Remoting Player</span></span>](holographic-remoting-player.md)
