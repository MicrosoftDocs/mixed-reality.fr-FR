---
title: Écriture d’un lecteur de communication à distance holographique personnalisé
description: En créant une application de lecteur de communication à distance holographique personnalisée, vous pouvez créer une application personnalisée capable d’afficher le contenu rendu sur une machine distante à votre HoloLens 2. Cet article explique comment procéder.
author: NPohl-MSFT
ms.author: nopohl
ms.date: 08/01/2019
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: fdc3d3bbd72d0812377d6a70c975f2111e1a2224
ms.sourcegitcommit: ca949efe0279995a376750d89e23d7123eb44846
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68718093"
---
# <a name="writing-a-custom-holographic-remoting-player-app"></a><span data-ttu-id="46f1c-105">Écriture d’une application de lecteur de communication à distance holographique personnalisée</span><span class="sxs-lookup"><span data-stu-id="46f1c-105">Writing a custom Holographic Remoting player app</span></span>

>[!IMPORTANT]
><span data-ttu-id="46f1c-106">Ce document décrit la création d’une application de lecteur personnalisée pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="46f1c-106">This document describes the creation of a custom player application for HoloLens 2.</span></span> <span data-ttu-id="46f1c-107">Les lecteurs personnalisés écrits pour HoloLens 2 ne sont pas compatibles avec les applications hôtes écrites pour HoloLens 1.</span><span class="sxs-lookup"><span data-stu-id="46f1c-107">Custom players written for HoloLens 2 are not compatible with host applications written for HoloLens 1.</span></span> <span data-ttu-id="46f1c-108">Cela implique que les deux applications doivent utiliser le package NuGet version **2. x. x**.</span><span class="sxs-lookup"><span data-stu-id="46f1c-108">This implies that both applications must use NuGet package version **2.x.x**.</span></span>

<span data-ttu-id="46f1c-109">En créant une application de lecteur de communication à distance holographique personnalisée, vous pouvez créer une application personnalisée capable d’afficher des [vues immersives](app-views.md) à partir d’un ordinateur distant sur votre HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="46f1c-109">By creating a custom Holographic Remoting player app you can create a custom application capable of displaying [immersive views](app-views.md) from on a remote machine on your HoloLens 2.</span></span> <span data-ttu-id="46f1c-110">Cet article explique comment procéder.</span><span class="sxs-lookup"><span data-stu-id="46f1c-110">This article describes how this can be achieved.</span></span> <span data-ttu-id="46f1c-111">Tout le code de cette page et des projets de travail se trouve dans le [référentiel GitHub d’exemples de communication à distance holographique](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples).</span><span class="sxs-lookup"><span data-stu-id="46f1c-111">All code on this page and working projects can be found in the [Holographic Remoting samples github repository](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples).</span></span>

<span data-ttu-id="46f1c-112">Un lecteur de communication à distance holographique permet à votre application d’afficher le contenu holographique [rendu](rendering.md) sur un PC de bureau ou sur un appareil UWP tel que le Xbox, permettant d’accéder à davantage de ressources système.</span><span class="sxs-lookup"><span data-stu-id="46f1c-112">A Holographic Remoting player allows your app to display holographic content [rendered](rendering.md) on a desktop PC or on a UWP device such as the Xbox One, allowing access to more system resources.</span></span> <span data-ttu-id="46f1c-113">Une application de lecteur de communication à distance holographique diffuse des données d’entrée vers une application hôte de communication à distance holographique et reçoit un affichage immersif en tant que flux vidéo et audio.</span><span class="sxs-lookup"><span data-stu-id="46f1c-113">A Holographic Remoting player app streams input data to a Holographic Remoting host application and receives back an immersive view as video and audio stream.</span></span> <span data-ttu-id="46f1c-114">La connexion est établie à l’aide du Wi-Fi standard.</span><span class="sxs-lookup"><span data-stu-id="46f1c-114">The connection is made using standard Wi-Fi.</span></span> <span data-ttu-id="46f1c-115">Pour créer une application de lecteur, vous allez utiliser un package NuGet pour ajouter la communication à distance holographique à votre application UWP, puis écrire du code pour gérer la connexion et afficher une vue immersive.</span><span class="sxs-lookup"><span data-stu-id="46f1c-115">To create a player app, you will use a NuGet package to add Holographic Remoting to your UWP app, and write code to handle the connection and to display an immersive view.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="46f1c-116">Prérequis</span><span class="sxs-lookup"><span data-stu-id="46f1c-116">Prerequisites</span></span>

<span data-ttu-id="46f1c-117">Un bon point de départ est une application UWP DirectX fonctionnelle qui cible déjà l’API Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="46f1c-117">A good starting point is a working DirectX based UWP app that already targets the Windows Mixed Reality API.</span></span> <span data-ttu-id="46f1c-118">Pour plus d’informations, consultez [vue d’ensemble du développement DirectX](directx-development-overview.md).</span><span class="sxs-lookup"><span data-stu-id="46f1c-118">For details see [DirectX development overview](directx-development-overview.md).</span></span> <span data-ttu-id="46f1c-119">Si vous ne disposez pas d’une application existante et que vous souhaitez commencer à partir de zéro, le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md) est un bon point de départ.</span><span class="sxs-lookup"><span data-stu-id="46f1c-119">If you do not have an existing app and want to start from scratch the [C++ holographic project template](creating-a-holographic-directx-project.md) is a good starting point.</span></span>

>[!IMPORTANT]
><span data-ttu-id="46f1c-120">Toute application utilisant la communication à distance holographique doit être créée pour utiliser un [cloisonnement](https://docs.microsoft.com/en-us/windows/win32/com/multithreaded-apartments)multithread.</span><span class="sxs-lookup"><span data-stu-id="46f1c-120">Any app using Holographic Remoting should be authored to use a [multi-threaded apartment](https://docs.microsoft.com/en-us/windows/win32/com/multithreaded-apartments).</span></span> <span data-ttu-id="46f1c-121">L’utilisation d’un [cloisonnement à thread unique](https://docs.microsoft.com/en-us/windows/win32/com/single-threaded-apartments) est prise en charge, mais entraîne des performances non optimales et éventuellement des interruptions pendant la lecture.</span><span class="sxs-lookup"><span data-stu-id="46f1c-121">The use of a [single-threaded appartment](https://docs.microsoft.com/en-us/windows/win32/com/single-threaded-apartments) is supported but will lead to sub-optimal performance and possibly stuttering during playback.</span></span> <span data-ttu-id="46f1c-122">Lors de C++l’utilisation de/WinRT [WinRT:: init_apartment](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/get-started) , un cloisonnement multithread est la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="46f1c-122">When using C++/WinRT [winrt::init_apartment](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/get-started) a multi-threaded apartment is the default.</span></span>

## <a name="get-the-holographic-remoting-nuget-package"></a><span data-ttu-id="46f1c-123">Procurez-vous le package NuGet de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="46f1c-123">Get the Holographic Remoting NuGet package</span></span>

<span data-ttu-id="46f1c-124">Les étapes suivantes sont requises pour ajouter le package NuGet à un projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46f1c-124">The following steps are required to add the NuGet package to a project in Visual Studio.</span></span>
1. <span data-ttu-id="46f1c-125">Ouvrez le projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46f1c-125">Open the project in Visual Studio.</span></span>
2. <span data-ttu-id="46f1c-126">Cliquez avec le bouton droit sur le nœud du projet et sélectionnez **gérer les packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="46f1c-126">Right-click the project node and select **Manage NuGet Packages...**</span></span>
3. <span data-ttu-id="46f1c-127">Dans le volet qui s’affiche, cliquez sur **Parcourir** , puis recherchez «accès distant holographique».</span><span class="sxs-lookup"><span data-stu-id="46f1c-127">In the panel that appears, click **Browse** and then search for "Holographic Remoting".</span></span>
4. <span data-ttu-id="46f1c-128">Sélectionnez **Microsoft. holographique. Remoting**, assurez-vous de choisir la version la plus récente de **2. x. x** , puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="46f1c-128">Select **Microsoft.Holographic.Remoting**, ensure to pick the latest **2.x.x** version and click **Install**.</span></span>
5. <span data-ttu-id="46f1c-129">Si la boîte de dialogue **Aperçu** s’affiche, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="46f1c-129">If the **Preview** dialog appears, click **OK**.</span></span>
6. <span data-ttu-id="46f1c-130">La boîte de dialogue suivante qui s’affiche est le contrat de licence.</span><span class="sxs-lookup"><span data-stu-id="46f1c-130">The next dialog that appears is the license agreement.</span></span> <span data-ttu-id="46f1c-131">Cliquez sur **J’accepte** pour accepter le contrat de licence.</span><span class="sxs-lookup"><span data-stu-id="46f1c-131">Click on **I Accept** to accept the license agreement.</span></span>

>[!IMPORTANT]
><a name="idl"></a><span data-ttu-id="46f1c-132">L' ```build\native\include\HolographicAppRemoting\Microsoft.Holographic.AppRemoting.idl``` intérieur du package NuGet contient une documentation détaillée sur l’API exposée par la communication à distance holographique.</span><span class="sxs-lookup"><span data-stu-id="46f1c-132">The ```build\native\include\HolographicAppRemoting\Microsoft.Holographic.AppRemoting.idl``` inside the NuGet package contains detailed documentation for the API exposed by Holographic Remoting.</span></span>

## <a name="modify-the-packageappxmanifest-of-the-application"></a><span data-ttu-id="46f1c-133">Modifier le package. appxmanifest de l’application</span><span class="sxs-lookup"><span data-stu-id="46f1c-133">Modify the Package.appxmanifest of the application</span></span>

<span data-ttu-id="46f1c-134">Pour que l’application prenne en charge le fichier Microsoft. holographique. AppRemoting. dll ajouté par le package NuGet, les étapes suivantes doivent être effectuées sur le projet:</span><span class="sxs-lookup"><span data-stu-id="46f1c-134">To make the application aware of the Microsoft.Holographic.AppRemoting.dll added by the NuGet package, the following steps need to be taken on the project:</span></span>

1. <span data-ttu-id="46f1c-135">Dans le Explorateur de solutions cliquez avec le bouton droit sur le fichier **Package. appxmanifest** , puis sélectionnez **Ouvrir avec...**</span><span class="sxs-lookup"><span data-stu-id="46f1c-135">In the Solution Explorer right-click on the **Package.appxmanifest** file and select **Open With...**</span></span>
2. <span data-ttu-id="46f1c-136">Sélectionnez **éditeur XML (texte)** , puis cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="46f1c-136">Select **XML (Text) Editor** and click OK</span></span>
3. <span data-ttu-id="46f1c-137">Ajoutez les lignes suivantes au fichier et enregistrez</span><span class="sxs-lookup"><span data-stu-id="46f1c-137">Add the following lines to the file and save</span></span>
```xml
  </Capabilities>

  <!--Add lines below -->
  <Extensions>
    <Extension Category="windows.activatableClass.inProcessServer">
      <InProcessServer>
        <Path>Microsoft.Holographic.AppRemoting.dll</Path>
        <ActivatableClass ActivatableClassId="Microsoft.Holographic.AppRemoting.PlayerContext" ThreadingModel="both" />
      </InProcessServer>
    </Extension>
  </Extensions>
  <!--Add lines above -->

</Package>
```
## <a name="create-the-player-context"></a><span data-ttu-id="46f1c-138">Créer le contexte du joueur</span><span class="sxs-lookup"><span data-stu-id="46f1c-138">Create the player context</span></span>

<span data-ttu-id="46f1c-139">En guise de première étape, l’application doit créer un contexte de joueur.</span><span class="sxs-lookup"><span data-stu-id="46f1c-139">As a first step the application should create a player context.</span></span>

```cpp
// class declaration:

#include <winrt/Microsoft.Holographic.AppRemoting.h>

...

private:
// PlayerContext used to connect with a Holographic Remoting host and display remotely rendered frames
winrt::Microsoft::Holographic::AppRemoting::PlayerContext m_playerContext = nullptr;
```


```cpp
// class implementation:

// Create the player context
// IMPORTANT: This must be done before creating the HolographicSpace (or any other call to the Holographic API).
m_playerContext = winrt::Microsoft::Holographic::AppRemoting::PlayerContext::Create();

```

>[!WARNING]
><span data-ttu-id="46f1c-140">La communication à distance holographique fonctionne en remplaçant le runtime Windows Mixed Reality qui fait partie de Windows par un Runtime spécifique à distance.</span><span class="sxs-lookup"><span data-stu-id="46f1c-140">Holographic Remoting works by replacing the Windows Mixed Reality runtime which is part of Windows with a remoting specific runtime.</span></span> <span data-ttu-id="46f1c-141">Cette opération est effectuée lors de la création du contexte du joueur.</span><span class="sxs-lookup"><span data-stu-id="46f1c-141">This is done during the creation of the player context.</span></span> <span data-ttu-id="46f1c-142">Pour cette raison, tout appel sur une API de réalité mixte Windows avant de créer le contexte du joueur peut entraîner un comportement inattendu.</span><span class="sxs-lookup"><span data-stu-id="46f1c-142">For that reason any call on any Windows Mixed Reality API before creating the player context can result in unexpected behavior.</span></span> <span data-ttu-id="46f1c-143">L’approche recommandée consiste à créer le contexte du joueur le plus tôt possible avant d’interagir avec une API de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="46f1c-143">The recommended approach is to create the player context as early as possible before interaction with any Mixed Reality API.</span></span> <span data-ttu-id="46f1c-144">Ne combinez jamais des objets créés ou récupérés par le biais d’une API ```PlayerContext::Create()``` Windows Mixed Reality avant l’appel à avec des objets créés ou récupérés par la suite.</span><span class="sxs-lookup"><span data-stu-id="46f1c-144">Never mix objects created or retrieved through any Windows Mixed Reality API before the call to ```PlayerContext::Create()``` with objects created or retrieved afterwards.</span></span>

<span data-ttu-id="46f1c-145">Ensuite, vous pouvez créer le HolographicSpace en appelant [HolographicSpace. CreateForCoreWindow](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicspace.createforcorewindow).</span><span class="sxs-lookup"><span data-stu-id="46f1c-145">Next the HolographicSpace can be created, by calling [HolographicSpace.CreateForCoreWindow](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicspace.createforcorewindow).</span></span>

```cpp
m_holographicSpace = winrt::Windows::Graphics::Holographic::HolographicSpace::CreateForCoreWindow(window);
```

## <a name="connect-to-the-host"></a><span data-ttu-id="46f1c-146">Se connecter à l’hôte</span><span class="sxs-lookup"><span data-stu-id="46f1c-146">Connect to the host</span></span>

<span data-ttu-id="46f1c-147">Une fois que l’application de lecteur est prête pour le rendu du contenu, une connexion à l’hôte peut être établie.</span><span class="sxs-lookup"><span data-stu-id="46f1c-147">Once the player app is ready for rendering content a connection to the host can be established.</span></span>

<span data-ttu-id="46f1c-148">La connexion peut être établie de l’une des manières suivantes:</span><span class="sxs-lookup"><span data-stu-id="46f1c-148">The connection can be established in one of the follwing ways:</span></span>
1) <span data-ttu-id="46f1c-149">L’application de lecteur s’exécutant sur HoloLens 2 se connecte à l’application hôte.</span><span class="sxs-lookup"><span data-stu-id="46f1c-149">The player app running on HoloLens 2 connects to the host app.</span></span>
2) <span data-ttu-id="46f1c-150">L’application hôte se connecte à l’application de lecteur s’exécutant sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="46f1c-150">The host app connects to the player app running on HoloLens 2.</span></span>

<span data-ttu-id="46f1c-151">Pour vous connecter à partir de l’application du lecteur à ```Connect``` l’hôte, appelez la méthode sur le contexte du joueur spécifiant le nom d’hôte et le port.</span><span class="sxs-lookup"><span data-stu-id="46f1c-151">To connect from the player app to the host call the ```Connect``` method on the player context specifying the hostname and port.</span></span> <span data-ttu-id="46f1c-152">Le port par défaut est **8265**.</span><span class="sxs-lookup"><span data-stu-id="46f1c-152">The default port is **8265**.</span></span>

```cpp
try
{
    m_playerContext.Connect(m_hostname, m_port);
}
catch(winrt::hresult_error& e)
{
    // Failed to connect. Get an error details via e.code() and e.message()
}
```

>[!IMPORTANT]
><span data-ttu-id="46f1c-153">Comme avec toute C++API ```Connect``` /WinRT peut lever une exception WinRT:: hresult_error qui doit être gérée.</span><span class="sxs-lookup"><span data-stu-id="46f1c-153">As with any C++/WinRT API ```Connect``` might throw an winrt::hresult_error which needs to be handled.</span></span>

<span data-ttu-id="46f1c-154">L’écoute des connexions entrantes sur l’application de lecteur peut être effectuée ```Listen``` en appelant la méthode.</span><span class="sxs-lookup"><span data-stu-id="46f1c-154">Listening for incoming connections on the player app can be done by calling the ```Listen``` method.</span></span> <span data-ttu-id="46f1c-155">Le port de liaison et le port de transport peuvent être spécifiés au cours de cet appel.</span><span class="sxs-lookup"><span data-stu-id="46f1c-155">Both the handshake port and transport port can be specified during this call.</span></span> <span data-ttu-id="46f1c-156">Le port de négociation est utilisé pour le protocole de transfert initial.</span><span class="sxs-lookup"><span data-stu-id="46f1c-156">The handshake port is used for the initial handshake.</span></span> <span data-ttu-id="46f1c-157">Les données sont ensuite envoyées sur le port de transport.</span><span class="sxs-lookup"><span data-stu-id="46f1c-157">The data is then send over the transport port.</span></span> <span data-ttu-id="46f1c-158">Les numéros de port **8265** et **8266** sont utilisés par défaut.</span><span class="sxs-lookup"><span data-stu-id="46f1c-158">By default port number **8265** and **8266** are used.</span></span>

```cpp
try
{
    m_playerContext.Listen(L"0.0.0.0", m_port, m_port + 1);
}
catch(winrt::hresult_error& e)
{
    // Failed to listen. Get an error details via e.code() and e.message()
}
```


## <a name="handling-connection-related-events"></a><span data-ttu-id="46f1c-159">Gestion des événements liés à la connexion</span><span class="sxs-lookup"><span data-stu-id="46f1c-159">Handling connection related events</span></span>

<span data-ttu-id="46f1c-160">Le ```PlayerContext``` expose trois événements pour surveiller l’état de la connexion.</span><span class="sxs-lookup"><span data-stu-id="46f1c-160">The ```PlayerContext``` exposes three events to monitor the state of the connection</span></span>
1) <span data-ttu-id="46f1c-161">OnConnected: Déclenché lorsqu’une connexion à l’hôte a été établie avec succès.</span><span class="sxs-lookup"><span data-stu-id="46f1c-161">OnConnected: Triggered when a connection to the host has been successfully established.</span></span>
```cpp
m_onConnectedEventToken = m_playerContext.OnConnected([]() 
{
    // Handle connection successfully established
});
```
2) <span data-ttu-id="46f1c-162">OnDisconnected: Déclenché si une connexion établie est terminée ou si une connexion n’a pas pu être établie.</span><span class="sxs-lookup"><span data-stu-id="46f1c-162">OnDisconnected: Triggered if an established connection is terminated or a connection could not be established.</span></span>
```cpp
m_onDisconnectedEventToken = m_playerContext.OnDisconnected([](ConnectionFailureReason failureReason)
{
    switch (failureReason)
    {
        // Handle connection failed or terminated.
        // See ConnectionFailureReason for possible reasons.
    }
}
```
>[!NOTE]
><span data-ttu-id="46f1c-163">Les ```ConnectionFailureReason``` valeurs possibles sont documentées ```Microsoft.Holographic.AppRemoting.idl``` dans le [fichier](#idl).</span><span class="sxs-lookup"><span data-stu-id="46f1c-163">Possible ```ConnectionFailureReason``` values are documented in the ```Microsoft.Holographic.AppRemoting.idl``` [file](#idl).</span></span>

3) <span data-ttu-id="46f1c-164">OnListening: Lors du démarrage de l’écoute des connexions entrantes.</span><span class="sxs-lookup"><span data-stu-id="46f1c-164">OnListening: When listening for incoming connections starts.</span></span>
```cpp
m_onListeningEventToken = m_playerContext.OnListening([]()
{
    // Handle start listening for incoming connections
});
```

<span data-ttu-id="46f1c-165">En outre, l’état de la connexion peut être interrogé ```ConnectionState``` à l’aide de la propriété du contexte du lecteur.</span><span class="sxs-lookup"><span data-stu-id="46f1c-165">Additionally the connection state can be queried using the ```ConnectionState``` property on the player context.</span></span>
```cpp
winrt::Microsoft::Holographic::AppRemoting::ConnectionState state = m_playerContext.ConnectionState();
```

## <a name="display-the-remotely-rendered-frame"></a><span data-ttu-id="46f1c-166">Afficher le frame rendu à distance</span><span class="sxs-lookup"><span data-stu-id="46f1c-166">Display the remotely rendered frame</span></span>

<span data-ttu-id="46f1c-167">Pour afficher le contenu rendu à distance, appelez ```PlayerContext::BlitRemoteFrame()``` lors du rendu d’un [HolographicFrame](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe).</span><span class="sxs-lookup"><span data-stu-id="46f1c-167">To display the remotely rendered content, call ```PlayerContext::BlitRemoteFrame()``` while rendering a [HolographicFrame](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe).</span></span> 

<span data-ttu-id="46f1c-168">```BlitRemoteFrame()```requiert que la mémoire tampon d’arrière-plan pour le HolographicFrame actuel soit liée en tant que cible de rendu.</span><span class="sxs-lookup"><span data-stu-id="46f1c-168">```BlitRemoteFrame()``` requires that the back buffer for the current HolographicFrame is bound as render target.</span></span> <span data-ttu-id="46f1c-169">La mémoire tampon d’arrière-plan peut être reçue à partir du [HolographicCameraRenderingParameters](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe.getrenderingparameters) via la propriété [Direct3D11BackBuffer](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.direct3d11backbuffer) .</span><span class="sxs-lookup"><span data-stu-id="46f1c-169">The back buffer can be received from the [HolographicCameraRenderingParameters](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe.getrenderingparameters) via the [Direct3D11BackBuffer](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.direct3d11backbuffer) property.</span></span>

<span data-ttu-id="46f1c-170">En cas d' ```BlitRemoteFrame()``` appel, copie la dernière trame reçue à partir de l’application hôte dans la mémoire tampon de l’HolographicFrame.</span><span class="sxs-lookup"><span data-stu-id="46f1c-170">When called, ```BlitRemoteFrame()``` copies the latest received frame from the host application into the BackBuffer of the HolographicFrame.</span></span> <span data-ttu-id="46f1c-171">En outre, l’ensemble de points de focalisation est défini, si l’application distante a spécifié un point de focus pendant le rendu du frame distant.</span><span class="sxs-lookup"><span data-stu-id="46f1c-171">Additionally the focus point set is set, if the remote application has specified a focus point during the rendering of the remote frame.</span></span>

```cpp
// Blit the remote frame into the backbuffer for the HolographicFrame.
winrt::Microsoft::Holographic::AppRemoting::BlitResult result = m_playerContext.BlitRemoteFrame();
```

>[!NOTE]
><span data-ttu-id="46f1c-172">```PlayerContext::BlitRemoteFrame()```remplace potentiellement le point de focus du frame actuel.</span><span class="sxs-lookup"><span data-stu-id="46f1c-172">```PlayerContext::BlitRemoteFrame()``` potentially overwrites the focus point for the current frame.</span></span> 
>- <span data-ttu-id="46f1c-173">Pour spécifier un point de focus de secours, appelez [HolographicCameraRenderingParameters:: SetFocusPoint](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.setfocuspoint) avant ```PlayerContext::BlitRemoteFrame()```.</span><span class="sxs-lookup"><span data-stu-id="46f1c-173">To specifiy a fallback focus point, call [HolographicCameraRenderingParameters::SetFocusPoint](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.setfocuspoint) before ```PlayerContext::BlitRemoteFrame()```.</span></span> 
>- <span data-ttu-id="46f1c-174">Pour overrwrite le point de focus distant, appelez [HolographicCameraRenderingParameters:: SetFocusPoint](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.setfocuspoint) après ```PlayerContext::BlitRemoteFrame()```.</span><span class="sxs-lookup"><span data-stu-id="46f1c-174">To overrwrite the remote focus point, call [HolographicCameraRenderingParameters::SetFocusPoint](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.setfocuspoint)  after ```PlayerContext::BlitRemoteFrame()```.</span></span>

<span data-ttu-id="46f1c-175">En cas de ```BlitRemoteFrame()``` réussite ```BlitResult::Success_Color```, retourne.</span><span class="sxs-lookup"><span data-stu-id="46f1c-175">On success, ```BlitRemoteFrame()``` returns ```BlitResult::Success_Color```.</span></span> <span data-ttu-id="46f1c-176">Dans le cas contraire, elle retourne la raison de l’échec:</span><span class="sxs-lookup"><span data-stu-id="46f1c-176">Otherwise it returns the failure reason:</span></span>
- <span data-ttu-id="46f1c-177">```BlitResult::Failed_NoRemoteFrameAvailable```: Échec, car aucun frame distant n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="46f1c-177">```BlitResult::Failed_NoRemoteFrameAvailable```: Failed because no remote frame is available.</span></span>
- <span data-ttu-id="46f1c-178">```BlitResult::Failed_NoCamera```: A échoué, car aucun appareil photo n’est présent.</span><span class="sxs-lookup"><span data-stu-id="46f1c-178">```BlitResult::Failed_NoCamera```: Failed because no camera present.</span></span>

## <a name="optional-get-statistics-about-the-last-remote-frame"></a><span data-ttu-id="46f1c-179">Facultatif : Obtenir des statistiques sur le dernier frame distant</span><span class="sxs-lookup"><span data-stu-id="46f1c-179">Optional: Get statistics about the last remote frame</span></span>

<span data-ttu-id="46f1c-180">Pour diagnostiquer les problèmes de performances ou de réseau, les statistiques relatives au dernier frame distant peuvent ```PlayerContext::LastFrameStatistics``` être récupérées via la propriété.</span><span class="sxs-lookup"><span data-stu-id="46f1c-180">To diagnose performance or network issues, statistics about the last remote frame can be retrieved via the ```PlayerContext::LastFrameStatistics``` property.</span></span> <span data-ttu-id="46f1c-181">Les statistiques sont mises à jour lors de l’appel à [HolographicFrame::P resentusingcurrentprediction](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe.presentusingcurrentprediction).</span><span class="sxs-lookup"><span data-stu-id="46f1c-181">Statistics are updated during the call to [HolographicFrame::PresentUsingCurrentPrediction](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe.presentusingcurrentprediction).</span></span>

```cpp
// Get statistics for the last presented frame.
winrt::Microsoft::Holographic::AppRemoting::PlayerFrameStatistics statistics = m_playerContext.LastFrameStatistics();
```

<span data-ttu-id="46f1c-182">Pour plus d’informations, consultez ```PlayerFrameStatistics``` la documentation ```Microsoft.Holographic.AppRemoting.idl``` du [fichier](#idl).</span><span class="sxs-lookup"><span data-stu-id="46f1c-182">For more details, see the ```PlayerFrameStatistics``` documentation in the ```Microsoft.Holographic.AppRemoting.idl``` [file](#idl).</span></span>

## <a name="optional-custom-data-channels"></a><span data-ttu-id="46f1c-183">Facultatif : Canaux de données personnalisés</span><span class="sxs-lookup"><span data-stu-id="46f1c-183">Optional: Custom data channels</span></span>

<span data-ttu-id="46f1c-184">Les canaux de données personnalisés peuvent être utilisés pour envoyer des données utilisateur sur la connexion de communication à distance déjà établie.</span><span class="sxs-lookup"><span data-stu-id="46f1c-184">Custom data channels can be used to send user data over the already established remoting connection.</span></span> <span data-ttu-id="46f1c-185">Pour plus d’informations, consultez [canaux de données personnalisés](holographic-remoting-custom-data-channels.md) .</span><span class="sxs-lookup"><span data-stu-id="46f1c-185">See [custom data channels](holographic-remoting-custom-data-channels.md) for more information.</span></span>

## <a name="see-also"></a><span data-ttu-id="46f1c-186">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="46f1c-186">See Also</span></span>
* [<span data-ttu-id="46f1c-187">Écriture d’une application hôte de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="46f1c-187">Writing a Holographic Remoting host app</span></span>](holographic-remoting-create-host.md)
* [<span data-ttu-id="46f1c-188">Canaux de données de communication à distance holographiques personnalisés</span><span class="sxs-lookup"><span data-stu-id="46f1c-188">Custom Holographic Remoting data channels</span></span>](holographic-remoting-custom-data-channels.md)
* [<span data-ttu-id="46f1c-189">Établissement d’une connexion sécurisée à l’aide de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="46f1c-189">Establishing a secure connection with Holographic Remoting</span></span>](holographic-remoting-secure-connection.md)
* [<span data-ttu-id="46f1c-190">Résolution des problèmes et limitations de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="46f1c-190">Holographic Remoting troubleshooting and limitations</span></span>](holographic-remoting-troubleshooting.md)
* [<span data-ttu-id="46f1c-191">Termes du contrat de licence du logiciel de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="46f1c-191">Holographic Remoting software license terms</span></span>](https://docs.microsoft.com/en-us/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [<span data-ttu-id="46f1c-192">Déclaration de confidentialité Microsoft</span><span class="sxs-lookup"><span data-stu-id="46f1c-192">Microsoft Privacy Statement</span></span>](https://go.microsoft.com/fwlink/?LinkId=521839)