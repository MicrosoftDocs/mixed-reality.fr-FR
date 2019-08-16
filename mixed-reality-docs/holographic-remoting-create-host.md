---
title: Écriture d’une application hôte de communication à distance holographique
description: En créant un contenu distant d’application hôte de communication à distance holographique, qui est affiché sur un ordinateur distant, peut être diffusé en continu vers HoloLens 2. Cet article explique comment procéder.
author: bethau
ms.author: bethau
ms.date: 08/01/2019
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: 95cf98504f26e2362b3c4fd38e7d9228350798f3
ms.sourcegitcommit: ca949efe0279995a376750d89e23d7123eb44846
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68718063"
---
# <a name="writing-a-holographic-remoting-host-app"></a><span data-ttu-id="6c408-105">Écriture d’une application hôte de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="6c408-105">Writing a Holographic Remoting host app</span></span>

>[!IMPORTANT]
><span data-ttu-id="6c408-106">Ce document décrit la création d’une application hôte pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="6c408-106">This document describes the creation of a host application for HoloLens 2.</span></span> <span data-ttu-id="6c408-107">L’application hôte pour **HoloLens 1** doit utiliser le package NuGet version **1. x. x**.</span><span class="sxs-lookup"><span data-stu-id="6c408-107">Host application for **HoloLens 1** must use NuGet package version **1.x.x**.</span></span> <span data-ttu-id="6c408-108">Cela implique que les applications hôtes écrites pour HoloLens 2 ne sont pas compatibles avec HoloLens 1 et vice versa.</span><span class="sxs-lookup"><span data-stu-id="6c408-108">This implies that host applications written for HoloLens 2 are not compatible with HoloLens 1 and vice versa.</span></span> <span data-ttu-id="6c408-109">La documentation de HoloLens 1 est disponible [ici](add-holographic-remoting.md).</span><span class="sxs-lookup"><span data-stu-id="6c408-109">The documentation for HoloLens 1 can be found [here](add-holographic-remoting.md).</span></span>

<span data-ttu-id="6c408-110">En créant une application hôte de communication à distance holographique, le contenu distant rendu sur une machine distante peut être transmis à HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="6c408-110">By creating a Holographic Remoting host app remote content that is rendered on a remote machine can be streamed to HoloLens 2.</span></span> <span data-ttu-id="6c408-111">Cet article explique comment procéder.</span><span class="sxs-lookup"><span data-stu-id="6c408-111">This article describes how this can be achieved.</span></span> <span data-ttu-id="6c408-112">Tout le code de cette page et des projets de travail se trouve dans le [référentiel GitHub d’exemples de communication à distance holographique](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples).</span><span class="sxs-lookup"><span data-stu-id="6c408-112">All code on this page and working projects can be found in the [Holographic Remoting samples github repository](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples).</span></span>

<span data-ttu-id="6c408-113">La communication à distance holographique permet à une application de cibler HoloLens 2 avec un contenu holographique hébergé sur un PC de bureau ou sur un appareil UWP comme la Xbox One, permettant d’accéder à davantage de ressources système et d’intégrer des [vues immersives](app-views.md) distantes dans les logiciels des PC de bureau existants.</span><span class="sxs-lookup"><span data-stu-id="6c408-113">Holographic remoting allows an app to target HoloLens 2 with holographic content hosted on a desktop PC or on a UWP device such as the Xbox One, allowing access to more system resources and making it possible to integrate remote [immersive views](app-views.md) into existing desktop PC software.</span></span> <span data-ttu-id="6c408-114">Une application hôte de communication à distance reçoit un flux de données d’entrée de HoloLens 2, restitue le contenu dans une vue immersive virtuelle et diffuse en continu des frames de contenu vers HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="6c408-114">A remoting host app receives an input data stream from HoloLens 2, renders content in a virtual immersive view, and streams content frames back to HoloLens 2.</span></span> <span data-ttu-id="6c408-115">La connexion est établie à l’aide du Wi-Fi standard.</span><span class="sxs-lookup"><span data-stu-id="6c408-115">The connection is made using standard Wi-Fi.</span></span> <span data-ttu-id="6c408-116">La communication à distance holographique est ajoutée à une application de bureau ou UWP via un paquet NuGet.</span><span class="sxs-lookup"><span data-stu-id="6c408-116">Holographic Remoting is added to a desktop or UWP app via a NuGet packet.</span></span> <span data-ttu-id="6c408-117">Du code supplémentaire est nécessaire pour gérer la connexion et le rendu dans une vue immersive.</span><span class="sxs-lookup"><span data-stu-id="6c408-117">Additional code is required which handles the connection and renders in an immersive view.</span></span>

<span data-ttu-id="6c408-118">Une connexion à distance classique aura une latence aussi faible que 50 ms de latence.</span><span class="sxs-lookup"><span data-stu-id="6c408-118">A typical remoting connection will have as low as 50 ms of latency.</span></span> <span data-ttu-id="6c408-119">L’application de lecteur peut signaler la latence en temps réel.</span><span class="sxs-lookup"><span data-stu-id="6c408-119">The player app can report the latency in real-time.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c408-120">Prérequis</span><span class="sxs-lookup"><span data-stu-id="6c408-120">Prerequisites</span></span>

<span data-ttu-id="6c408-121">Un bon point de départ est un bureau DirectX opérationnel ou une application UWP qui cible l’API Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="6c408-121">A good starting point is a working DirectX based Desktop or UWP app which targets the Windows Mixed Reality API.</span></span> <span data-ttu-id="6c408-122">Pour plus d’informations, consultez [vue d’ensemble du développement DirectX](directx-development-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c408-122">For details see [DirectX development overview](directx-development-overview.md).</span></span> <span data-ttu-id="6c408-123">Le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md) est un bon point de départ.</span><span class="sxs-lookup"><span data-stu-id="6c408-123">The [C++ holographic project template](creating-a-holographic-directx-project.md) is a good starting point.</span></span>

>[!IMPORTANT]
><span data-ttu-id="6c408-124">Toute application utilisant la communication à distance holographique doit être créée pour utiliser un [cloisonnement](https://docs.microsoft.com/en-us/windows/win32/com/multithreaded-apartments)multithread.</span><span class="sxs-lookup"><span data-stu-id="6c408-124">Any app using Holographic Remoting should be authored to use a [multi-threaded apartment](https://docs.microsoft.com/en-us/windows/win32/com/multithreaded-apartments).</span></span> <span data-ttu-id="6c408-125">L’utilisation d’un [cloisonnement à thread unique](https://docs.microsoft.com/en-us/windows/win32/com/single-threaded-apartments) est prise en charge, mais entraîne des performances non optimales et éventuellement des interruptions pendant la lecture.</span><span class="sxs-lookup"><span data-stu-id="6c408-125">The use of a [single-threaded apartment](https://docs.microsoft.com/en-us/windows/win32/com/single-threaded-apartments) is supported but will lead to sub-optimal performance and possibly stuttering during playback.</span></span> <span data-ttu-id="6c408-126">Lors de C++l’utilisation de/WinRT [WinRT:: init_apartment](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/get-started) , un cloisonnement multithread est la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="6c408-126">When using C++/WinRT [winrt::init_apartment](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/get-started) a multi-threaded apartment is the default.</span></span>



## <a name="get-the-holographic-remoting-nuget-package"></a><span data-ttu-id="6c408-127">Procurez-vous le package NuGet de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="6c408-127">Get the Holographic Remoting NuGet package</span></span>

<span data-ttu-id="6c408-128">Les étapes suivantes sont requises pour ajouter le package NuGet à un projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c408-128">The following steps are required to add the NuGet package to a project in Visual Studio.</span></span>
1. <span data-ttu-id="6c408-129">Ouvrez le projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c408-129">Open the project in Visual Studio.</span></span>
2. <span data-ttu-id="6c408-130">Cliquez avec le bouton droit sur le nœud du projet et sélectionnez **gérer les packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="6c408-130">Right-click the project node and select **Manage NuGet Packages...**</span></span>
3. <span data-ttu-id="6c408-131">Dans le volet qui s’affiche, cliquez sur **Parcourir** , puis recherchez «accès distant holographique».</span><span class="sxs-lookup"><span data-stu-id="6c408-131">In the panel that appears, click **Browse** and then search for "Holographic Remoting".</span></span>
4. <span data-ttu-id="6c408-132">Sélectionnez **Microsoft. holographique. Remoting**, assurez-vous de choisir la version la plus récente de **2. x. x** , puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="6c408-132">Select **Microsoft.Holographic.Remoting**, ensure to pick the latest **2.x.x** version and click **Install**.</span></span>
5. <span data-ttu-id="6c408-133">Si la boîte de dialogue **Aperçu** s’affiche, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6c408-133">If the **Preview** dialog appears, click **OK**.</span></span>
6. <span data-ttu-id="6c408-134">La boîte de dialogue suivante qui s’affiche est le contrat de licence.</span><span class="sxs-lookup"><span data-stu-id="6c408-134">The next dialog that appears is the license agreement.</span></span> <span data-ttu-id="6c408-135">Cliquez sur **J’accepte** pour accepter le contrat de licence.</span><span class="sxs-lookup"><span data-stu-id="6c408-135">Click on **I Accept** to accept the license agreement.</span></span>

>[!NOTE]
><span data-ttu-id="6c408-136">La version **1. x. x** du package NuGet est toujours disponible pour les développeurs qui souhaitent cibler HoloLens 1.</span><span class="sxs-lookup"><span data-stu-id="6c408-136">Version **1.x.x** of the NuGet package is still available for developers who want to target HoloLens 1.</span></span> <span data-ttu-id="6c408-137">Pour plus d’informations, consultez [Ajouter une communication à distance holographique (HoloLens 1)](add-holographic-remoting.md).</span><span class="sxs-lookup"><span data-stu-id="6c408-137">For details see [Add Holographic Remoting (HoloLens 1)](add-holographic-remoting.md).</span></span>

## <a name="create-the-remote-context"></a><span data-ttu-id="6c408-138">Créer le contexte distant</span><span class="sxs-lookup"><span data-stu-id="6c408-138">Create the remote context</span></span>

<span data-ttu-id="6c408-139">En guise de première étape, l’application doit créer un contexte distant.</span><span class="sxs-lookup"><span data-stu-id="6c408-139">As a first step the application should create a remote context.</span></span>

```cpp
// class declaration
#include <winrt/Microsoft.Holographic.AppRemoting.h>

...

private:
    // RemoteContext used to connect with a Holographic Remoting player and display rendered frames
    winrt::Microsoft::Holographic::AppRemoting::RemoteContext m_remoteContext = nullptr;
```


```cpp
// class implementation
#include <HolographicAppRemoting\Streamer.h>

...

CreateRemoteContext(m_remoteContext, 20000, false, PreferredVideoCodec::Default);

```

>[!WARNING]
><span data-ttu-id="6c408-140">La communication à distance holographique fonctionne en remplaçant le runtime Windows Mixed Reality qui fait partie de Windows par un Runtime spécifique à distance.</span><span class="sxs-lookup"><span data-stu-id="6c408-140">Holographic Remoting works by replacing the Windows Mixed Reality runtime which is part of Windows with a remoting specific runtime.</span></span> <span data-ttu-id="6c408-141">Cette opération est effectuée lors de la création du contexte distant.</span><span class="sxs-lookup"><span data-stu-id="6c408-141">This is done during the creation of the remote context.</span></span> <span data-ttu-id="6c408-142">Pour cette raison, tout appel sur une API de réalité mixte Windows avant de créer le contexte distant peut entraîner un comportement inattendu.</span><span class="sxs-lookup"><span data-stu-id="6c408-142">For that reason any call on any Windows Mixed Reality API before creating the remote context can result in unexpected behavior.</span></span> <span data-ttu-id="6c408-143">L’approche recommandée consiste à créer le contexte distant le plus tôt possible avant d’interagir avec une API de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="6c408-143">The recommended approach is to create the remote context as early as possible before interaction with any Mixed Reality API.</span></span> <span data-ttu-id="6c408-144">Ne combinez jamais des objets créés ou récupérés par le biais d’une API Windows Mixed Reality avant l’appel à CreateRemoteContext avec des objets créés ou récupérés par la suite.</span><span class="sxs-lookup"><span data-stu-id="6c408-144">Never mix objects created or retrieved through any Windows Mixed Reality API before the call to CreateRemoteContext with objects created or retrieved afterwards.</span></span>

<span data-ttu-id="6c408-145">L’espace holographique doit ensuite être créé.</span><span class="sxs-lookup"><span data-stu-id="6c408-145">Next the holographic space needs to be created.</span></span> <span data-ttu-id="6c408-146">La spécification d’un CoreWindow n’est pas obligatoire.</span><span class="sxs-lookup"><span data-stu-id="6c408-146">Specifying a CoreWindow is not required.</span></span> <span data-ttu-id="6c408-147">Les applications de bureau qui n’ont pas de CoreWindow peuvent simplement ```nullptr```passer un.</span><span class="sxs-lookup"><span data-stu-id="6c408-147">Desktop apps that do not have a CoreWindow can just pass a ```nullptr```.</span></span>

```cpp
m_holographicSpace = winrt::Windows::Graphics::Holographic::HolographicSpace::CreateForCoreWindow(nullptr);
```

## <a name="connect-to-the-device"></a><span data-ttu-id="6c408-148">Se connecter à l’appareil</span><span class="sxs-lookup"><span data-stu-id="6c408-148">Connect to the device</span></span>

<span data-ttu-id="6c408-149">Une fois que l’application hôte est prête pour le rendu du contenu, une connexion à l’appareil peut être établie.</span><span class="sxs-lookup"><span data-stu-id="6c408-149">Once the host app is ready for rendering content a connection to the device can be established.</span></span>

<span data-ttu-id="6c408-150">La connexion peut être effectuée de deux manières.</span><span class="sxs-lookup"><span data-stu-id="6c408-150">Connection can be done in one of two ways.</span></span>
1) <span data-ttu-id="6c408-151">L’application hôte se connecte au lecteur qui s’exécute sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="6c408-151">The host app connects to the player running on the device.</span></span>
2) <span data-ttu-id="6c408-152">Le lecteur s’exécutant sur l’appareil se connecte à l’application hôte.</span><span class="sxs-lookup"><span data-stu-id="6c408-152">The player running on the device connects to the host app.</span></span>

<span data-ttu-id="6c408-153">Pour établir une connexion à partir de l’application hôte à HoloLens 2 ```Connect``` , appelez la méthode sur le contexte distant en spécifiant le nom d’hôte et le port.</span><span class="sxs-lookup"><span data-stu-id="6c408-153">To establish a connection from the host app to HoloLens 2 call the ```Connect``` method on the remote context specifying the hostname and port.</span></span> <span data-ttu-id="6c408-154">Le port utilisé par le lecteur de communication à distance holographique est **8265**.</span><span class="sxs-lookup"><span data-stu-id="6c408-154">The port used by the Holographic Remoting Player is **8265**.</span></span>

```cpp
try
{
    m_remoteContext.Connect(m_hostname, m_port);
}
catch(winrt::hresult_error& e)
{
    DebugLog(L"Connect failed with hr = 0x%08X", e.code());
}
```

>[!IMPORTANT]
><span data-ttu-id="6c408-155">Comme avec toute C++API ```Connect``` /WinRT peut lever une exception WinRT:: hresult_error qui doit être gérée.</span><span class="sxs-lookup"><span data-stu-id="6c408-155">As with any C++/WinRT API ```Connect``` might throw an winrt::hresult_error which needs to be handled.</span></span>

>[!TIP]
><span data-ttu-id="6c408-156">Pour éviter d' [ C++](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/) utiliser la projection du langage ```build\native\include\<windows sdk version>\abi\Microsoft.Holographic.AppRemoting.h``` /WinRT, le fichier situé dans le package NuGet de communication à distance holographique peut être inclus.</span><span class="sxs-lookup"><span data-stu-id="6c408-156">To avoid using [C++/WinRT](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/) language projection the file ```build\native\include\<windows sdk version>\abi\Microsoft.Holographic.AppRemoting.h``` located inside the Holographic Remoting NuGet package can be included.</span></span> <span data-ttu-id="6c408-157">Il contient les déclarations des interfaces COM sous-jacentes.</span><span class="sxs-lookup"><span data-stu-id="6c408-157">It contains declarations of the underlying COM interfaces.</span></span> <span data-ttu-id="6c408-158">L’utilisation de C++/WinRT est toutefois recommandée.</span><span class="sxs-lookup"><span data-stu-id="6c408-158">The use of C++/WinRT is recommended though.</span></span>

<span data-ttu-id="6c408-159">L’écoute des connexions entrantes sur l’application hôte peut être effectuée en ```Listen``` appelant la méthode.</span><span class="sxs-lookup"><span data-stu-id="6c408-159">Listening for incoming connections on the host app can be done by calling the ```Listen``` method.</span></span> <span data-ttu-id="6c408-160">Le port de liaison et le port de transport peuvent être spécifiés au cours de cet appel.</span><span class="sxs-lookup"><span data-stu-id="6c408-160">Both the handshake port and transport port can be specified during this call.</span></span> <span data-ttu-id="6c408-161">Le port de négociation est utilisé pour le protocole de transfert initial.</span><span class="sxs-lookup"><span data-stu-id="6c408-161">The handshake port is used for the initial handshake.</span></span> <span data-ttu-id="6c408-162">Les données sont ensuite envoyées sur le port de transport.</span><span class="sxs-lookup"><span data-stu-id="6c408-162">The data is then send over the transport port.</span></span> <span data-ttu-id="6c408-163">Par défaut, **8265** et **8266** sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="6c408-163">By default **8265** and **8266** are used.</span></span>

```cpp
try
{
    m_remoteContext.Listen(L"0.0.0.0", m_port, m_port + 1);
}
catch(winrt::hresult_error& e)
{
    DebugLog(L"Listen failed with hr = 0x%08X", e.code());
}
```

>[!IMPORTANT]
><span data-ttu-id="6c408-164">L' ```build\native\include\HolographicAppRemoting\Microsoft.Holographic.AppRemoting.idl``` intérieur du package NuGet contient une documentation détaillée sur l’API exposée par la communication à distance holographique.</span><span class="sxs-lookup"><span data-stu-id="6c408-164">The ```build\native\include\HolographicAppRemoting\Microsoft.Holographic.AppRemoting.idl``` inside the NuGet package contains detailed documentation for the API exposed by Holographic Remoting.</span></span>

## <a name="handling-remoting-specific-events"></a><span data-ttu-id="6c408-165">Gestion des événements de communication à distance spécifiques</span><span class="sxs-lookup"><span data-stu-id="6c408-165">Handling Remoting specific events</span></span>

<span data-ttu-id="6c408-166">Le contexte distant expose trois événements qui sont importants pour surveiller l’état d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="6c408-166">The remote context exposes three events which are important to monitor the state of a connection.</span></span>
1) <span data-ttu-id="6c408-167">OnConnected: Déclenché lorsqu’une connexion à l’appareil a été établie avec succès.</span><span class="sxs-lookup"><span data-stu-id="6c408-167">OnConnected: Triggered when a connection to the device has been successfully established.</span></span>
```cpp
winrt::weak_ref<winrt::Microsoft::Holographic::AppRemoting::IRemoteContext> remoteContextWeakRef = m_remoteContext;

m_onConnectedEventRevoker = m_remoteContext.OnConnected(winrt::auto_revoke, [this, remoteContextWeakRef]() {
    if (auto remoteContext = remoteContextWeakRef.get())
    {
        // Update UI state
    }
});
```
2) <span data-ttu-id="6c408-168">OnDisconnected: Déclenché si une connexion établie est fermée ou si une connexion n’a pas pu être établie.</span><span class="sxs-lookup"><span data-stu-id="6c408-168">OnDisconnected: Triggered if an established connection is closed or a connection could not be established.</span></span>
```cpp
m_onDisconnectedEventRevoker =
    m_remoteContext.OnDisconnected(winrt::auto_revoke, [this, remoteContextWeakRef](ConnectionFailureReason failureReason) {
        if (auto remoteContext = remoteContextWeakRef.get())
        {
            DebugLog(L"Disconnected with reason %d", failureReason);
            // Update UI

            // Reconnect if this is a transient failure.
            if (failureReason == ConnectionFailureReason::HandshakeUnreachable ||
                failureReason == ConnectionFailureReason::TransportUnreachable ||
                failureReason == ConnectionFailureReason::ConnectionLost)
            {
                DebugLog(L"Reconnecting...");

                ConnectOrListen();
            }
            // Failure reason None indicates a normal disconnect.
            else if (failureReason != ConnectionFailureReason::None)
            {
                DebugLog(L"Disconnected with unrecoverable error, not attempting to reconnect.");
            }
        }
    });
```
3) <span data-ttu-id="6c408-169">OnListening: Lors du démarrage de l’écoute des connexions entrantes.</span><span class="sxs-lookup"><span data-stu-id="6c408-169">OnListening: When listening for incoming connections starts.</span></span>
```cpp
m_onListeningEventRevoker = m_remoteContext.OnListening(winrt::auto_revoke, [this, remoteContextWeakRef]() {
    if (auto remoteContext = remoteContextWeakRef.get())
    {
        // Update UI state
    }
});
```

<span data-ttu-id="6c408-170">En outre, l’état de la connexion peut être interrogé ```ConnectionState``` à l’aide de la propriété sur le contexte distant.</span><span class="sxs-lookup"><span data-stu-id="6c408-170">Additionally the connection state can be queried using the ```ConnectionState``` property on the remote context.</span></span>
```cpp
auto connectionState = m_remoteContext.ConnectionState();
```

## <a name="handling-speech-events"></a><span data-ttu-id="6c408-171">Gestion des événements vocaux</span><span class="sxs-lookup"><span data-stu-id="6c408-171">Handling speech events</span></span>

<span data-ttu-id="6c408-172">À l’aide de l’interface de reconnaissance vocale à distance, il est possible d’inscrire les déclencheurs vocaux avec HoloLens 2 et de les faire distants à l’application hôte.</span><span class="sxs-lookup"><span data-stu-id="6c408-172">Using the remote speech interface it is possible to register speech triggers with HoloLens 2 and have them remoted to the host application.</span></span>

<span data-ttu-id="6c408-173">Ce membre supplémentaire est requis pour effectuer le suivi de l’état de la voix à distance.</span><span class="sxs-lookup"><span data-stu-id="6c408-173">This additional member is required to track the state of the remote speech.</span></span>

```cpp
winrt::Microsoft::Holographic::AppRemoting::IRemoteSpeech::OnRecognizedSpeech_revoker m_onRecognizedSpeechRevoker;

```

<span data-ttu-id="6c408-174">Tout d’abord, l’interface de reconnaissance vocale à distance doit être récupérée.</span><span class="sxs-lookup"><span data-stu-id="6c408-174">First the remote speech interface needs to be retrieved.</span></span>

```cpp
if (auto remoteSpeech = m_remoteContext.GetRemoteSpeech())
{
    InitializeSpeechAsync(remoteSpeech, m_onRecognizedSpeechRevoker, weak_from_this());
}
```

<span data-ttu-id="6c408-175">À l’aide d’une méthode d’assistance asynchrone, vous pouvez initialiser la reconnaissance vocale à distance.</span><span class="sxs-lookup"><span data-stu-id="6c408-175">Using an asynchronous helper method you can then initialize the remote speech.</span></span> <span data-ttu-id="6c408-176">Cette opération doit être effectuée de façon asynchrone, car l’initialisation peut prendre beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="6c408-176">This should be done asynchronously as initializing might take a considerable amount of time.</span></span> <span data-ttu-id="6c408-177">[Opérations d’accès concurrentiel C++et asynchrones avec/WinRT](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/concurrency) explique comment créer des fonctions asynchrones avec/WinRT. C++</span><span class="sxs-lookup"><span data-stu-id="6c408-177">[Concurrency and asynchronous operations with C++/WinRT](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/concurrency) explains how to author asynchronous functions with C++/WinRT.</span></span>

```cpp
winrt::Windows::Foundation::IAsyncOperation<winrt::Windows::Storage::StorageFile> LoadGrammarFileAsync()
{
    const wchar_t* speechGrammarFile = L"SpeechGrammar.xml";
    auto rootFolder = winrt::Windows::ApplicationModel::Package::Current().InstalledLocation();
    return rootFolder.GetFileAsync(speechGrammarFile);
}

winrt::fire_and_forget InitializeSpeechAsync(
    winrt::Microsoft::Holographic::AppRemoting::IRemoteSpeech remoteSpeech,
    winrt::Microsoft::Holographic::AppRemoting::IRemoteSpeech::OnRecognizedSpeech_revoker& onRecognizedSpeechRevoker,
    std::weak_ptr<SampleHostMain> sampleHostMainWeak)
{
    onRecognizedSpeechRevoker = remoteSpeech.OnRecognizedSpeech(
        winrt::auto_revoke, [sampleHostMainWeak](const winrt::Microsoft::Holographic::AppRemoting::RecognizedSpeech& recognizedSpeech) {
            if (auto sampleHostMain = sampleHostMainWeak.lock())
            {
                sampleHostMain->OnRecognizedSpeech(recognizedSpeech.RecognizedText);
            }
        });

    auto grammarFile = co_await LoadGrammarFileAsync();

    std::vector<winrt::hstring> dictionary;
    dictionary.push_back(L"Red");
    dictionary.push_back(L"Blue");
    dictionary.push_back(L"Green");
    dictionary.push_back(L"Default");
    dictionary.push_back(L"Aquamarine");

    remoteSpeech.ApplyParameters(L"en-US", grammarFile, dictionary);
}
```

<span data-ttu-id="6c408-178">Il existe deux façons de spécifier des expressions à reconnaître.</span><span class="sxs-lookup"><span data-stu-id="6c408-178">There are two ways of specifying phrases to be recognized.</span></span>
1) <span data-ttu-id="6c408-179">Spécification à l’intérieur d’un fichier XML de grammaire vocale.</span><span class="sxs-lookup"><span data-stu-id="6c408-179">Specification inside a speech grammar xml file.</span></span> <span data-ttu-id="6c408-180">Pour plus d’informations, consultez [comment créer une grammaire XML de base](https://docs.microsoft.com/en-us/previous-versions/office/developer/speech-technologies/hh361658(v=office.14)) .</span><span class="sxs-lookup"><span data-stu-id="6c408-180">See [How to create a basic XML Grammar](https://docs.microsoft.com/en-us/previous-versions/office/developer/speech-technologies/hh361658(v=office.14)) for details.</span></span>
2) <span data-ttu-id="6c408-181">Spécifiez en les passant dans le vecteur du ```ApplyParameters```dictionnaire à.</span><span class="sxs-lookup"><span data-stu-id="6c408-181">Specify by passing them inside the dictionary vector to ```ApplyParameters```.</span></span>

<span data-ttu-id="6c408-182">Dans le rappel OnRecognizedSpeech, les événements vocaux peuvent ensuite être traités:</span><span class="sxs-lookup"><span data-stu-id="6c408-182">Inside the OnRecognizedSpeech callback the speech events can then be processed:</span></span>

```cpp
void SampleHostMain::OnRecognizedSpeech(const winrt::hstring& recognizedText)
{
    bool changedColor = false;
    DirectX::XMFLOAT4 color = {1, 1, 1, 1};

    if (recognizedText == L"Red")
    {
        color = {1, 0, 0, 1};
        changedColor = true;
    }
    else if (recognizedText == L"Blue")
    {
        color = {0, 0, 1, 1};
        changedColor = true;
    }
    else if (recognizedText == L"Green")
    {
        ...
    }

    ...
}
```

## <a name="preview-streamed-content-locally"></a><span data-ttu-id="6c408-183">Afficher un aperçu du contenu diffusé en continu localement</span><span class="sxs-lookup"><span data-stu-id="6c408-183">Preview streamed content locally</span></span>

<span data-ttu-id="6c408-184">Pour afficher le même contenu dans l’application hôte qui est envoyé à l’appareil, ```OnSendFrame``` l’événement du contexte distant peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="6c408-184">To display the same content in the host app that is send to the device the ```OnSendFrame``` event of the remote context can be used.</span></span> <span data-ttu-id="6c408-185">L' ```OnSendFrame``` événement est déclenché chaque fois que la bibliothèque de communication à distance holographique envoie le frame actuel au périphérique distant.</span><span class="sxs-lookup"><span data-stu-id="6c408-185">The ```OnSendFrame``` event is triggered every time the Holographic Remoting library sends the current frame to the remote device.</span></span> <span data-ttu-id="6c408-186">C’est le moment idéal pour prendre le contenu et le configurer dans la fenêtre du bureau ou UWP.</span><span class="sxs-lookup"><span data-stu-id="6c408-186">This is the ideal time to take the content and also blit it into the desktop or UWP window.</span></span>

```cpp
#include <windows.graphics.directx.direct3d11.interop.h>

...

m_onSendFrameEventRevoker = m_remoteContext.OnSendFrame(
    winrt::auto_revoke, [this](const winrt::Windows::Graphics::DirectX::Direct3D11::IDirect3DSurface& texture) {
        winrt::com_ptr<ID3D11Texture2D> texturePtr;
        {
            winrt::com_ptr<ID3D11Resource> resource;
            winrt::com_ptr<::IInspectable> inspectable = texture.as<::IInspectable>();
            winrt::com_ptr<Windows::Graphics::DirectX::Direct3D11::IDirect3DDxgiInterfaceAccess> dxgiInterfaceAccess;
            winrt::check_hresult(inspectable->QueryInterface(__uuidof(dxgiInterfaceAccess), dxgiInterfaceAccess.put_void()));
            winrt::check_hresult(dxgiInterfaceAccess->GetInterface(__uuidof(resource), resource.put_void()));
            resource.as(texturePtr);
        }

        // Copy / blit texturePtr into the back buffer here.
    });
```

## <a name="optional-custom-data-channels"></a><span data-ttu-id="6c408-187">Facultatif : Canaux de données personnalisés</span><span class="sxs-lookup"><span data-stu-id="6c408-187">Optional: Custom data channels</span></span>

<span data-ttu-id="6c408-188">Les canaux de données personnalisés peuvent être utilisés pour envoyer des données utilisateur sur la connexion de communication à distance déjà établie.</span><span class="sxs-lookup"><span data-stu-id="6c408-188">Custom data channels can be used to send user data over the already established remoting connection.</span></span> <span data-ttu-id="6c408-189">Pour plus d’informations, consultez [canaux de données personnalisés](holographic-remoting-custom-data-channels.md) .</span><span class="sxs-lookup"><span data-stu-id="6c408-189">See [custom data channels](holographic-remoting-custom-data-channels.md) for more information.</span></span>

## <a name="see-also"></a><span data-ttu-id="6c408-190">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6c408-190">See Also</span></span>
* [<span data-ttu-id="6c408-191">Écriture d’une application de lecteur de communication à distance holographique personnalisée</span><span class="sxs-lookup"><span data-stu-id="6c408-191">Writing a custom Holographic Remoting player app</span></span>](holographic-remoting-create-player.md)
* [<span data-ttu-id="6c408-192">Canaux de données de communication à distance holographiques personnalisés</span><span class="sxs-lookup"><span data-stu-id="6c408-192">Custom Holographic Remoting data channels</span></span>](holographic-remoting-custom-data-channels.md)
* [<span data-ttu-id="6c408-193">Établissement d’une connexion sécurisée à l’aide de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="6c408-193">Establishing a secure connection with Holographic Remoting</span></span>](holographic-remoting-secure-connection.md)
* [<span data-ttu-id="6c408-194">Résolution des problèmes et limitations de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="6c408-194">Holographic Remoting troubleshooting and limitations</span></span>](holographic-remoting-troubleshooting.md)
* [<span data-ttu-id="6c408-195">Termes du contrat de licence du logiciel de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="6c408-195">Holographic Remoting software license terms</span></span>](https://docs.microsoft.com/en-us/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [<span data-ttu-id="6c408-196">Déclaration de confidentialité Microsoft</span><span class="sxs-lookup"><span data-stu-id="6c408-196">Microsoft Privacy Statement</span></span>](https://go.microsoft.com/fwlink/?LinkId=521839)