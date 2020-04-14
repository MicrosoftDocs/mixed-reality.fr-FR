---
title: Écriture d’un lecteur de communication à distance holographique personnalisé
description: En créant une application de lecteur de communication à distance holographique personnalisée, vous pouvez créer une application personnalisée capable d’afficher le contenu rendu sur une machine distante à votre HoloLens 2. Cet article explique comment procéder.
author: florianbagarmicrosoft
ms.author: flbagar
ms.date: 03/11/2020
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: b276558e43fc545be9e5c0be6feded229904ee97
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81278217"
---
# <a name="writing-a-custom-holographic-remoting-player-app"></a><span data-ttu-id="da266-105">Écriture d’une application de lecteur de communication à distance holographique personnalisée</span><span class="sxs-lookup"><span data-stu-id="da266-105">Writing a custom Holographic Remoting player app</span></span>

>[!IMPORTANT]
><span data-ttu-id="da266-106">Ce document décrit la création d’une application de lecteur personnalisée pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="da266-106">This document describes the creation of a custom player application for HoloLens 2.</span></span> <span data-ttu-id="da266-107">Les lecteurs personnalisés écrits pour HoloLens 2 ne sont pas compatibles avec les applications distantes écrites pour HoloLens 1.</span><span class="sxs-lookup"><span data-stu-id="da266-107">Custom players written for HoloLens 2 are not compatible with remote applications written for HoloLens 1.</span></span> <span data-ttu-id="da266-108">Cela implique que les deux applications doivent utiliser le package NuGet version **2. x. x**.</span><span class="sxs-lookup"><span data-stu-id="da266-108">This implies that both applications must use NuGet package version **2.x.x**.</span></span>

<span data-ttu-id="da266-109">En créant une application de lecteur de communication à distance holographique personnalisée, vous pouvez créer une application personnalisée capable d’afficher des [vues immersives](app-views.md) à partir d’un ordinateur distant sur votre HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="da266-109">By creating a custom Holographic Remoting player app you can create a custom application capable of displaying [immersive views](app-views.md) from on a remote machine on your HoloLens 2.</span></span> <span data-ttu-id="da266-110">Cet article explique comment procéder.</span><span class="sxs-lookup"><span data-stu-id="da266-110">This article describes how this can be achieved.</span></span> <span data-ttu-id="da266-111">Tout le code de cette page et des projets de travail se trouve dans le [référentiel GitHub d’exemples de communication à distance holographique](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples).</span><span class="sxs-lookup"><span data-stu-id="da266-111">All code on this page and working projects can be found in the [Holographic Remoting samples github repository](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples).</span></span>

<span data-ttu-id="da266-112">Un lecteur de communication à distance holographique permet à votre application d’afficher le contenu holographique [rendu](rendering.md) sur un PC de bureau ou sur un appareil UWP tel que le Xbox, permettant d’accéder à davantage de ressources système.</span><span class="sxs-lookup"><span data-stu-id="da266-112">A Holographic Remoting player allows your app to display holographic content [rendered](rendering.md) on a desktop PC or on a UWP device such as the Xbox One, allowing access to more system resources.</span></span> <span data-ttu-id="da266-113">Une application de lecteur de communication à distance holographique diffuse des données d’entrée vers une application distante de communication à distance holographique et reçoit un affichage immersif en tant que flux vidéo et audio.</span><span class="sxs-lookup"><span data-stu-id="da266-113">A Holographic Remoting player app streams input data to a Holographic Remoting remote application and receives back an immersive view as video and audio stream.</span></span> <span data-ttu-id="da266-114">La connexion est établie à l’aide du Wi-Fi standard.</span><span class="sxs-lookup"><span data-stu-id="da266-114">The connection is made using standard Wi-Fi.</span></span> <span data-ttu-id="da266-115">Pour créer une application de lecteur, vous allez utiliser un package NuGet pour ajouter la communication à distance holographique à votre application UWP, puis écrire du code pour gérer la connexion et afficher une vue immersive.</span><span class="sxs-lookup"><span data-stu-id="da266-115">To create a player app, you will use a NuGet package to add Holographic Remoting to your UWP app, and write code to handle the connection and to display an immersive view.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="da266-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="da266-116">Prerequisites</span></span>

<span data-ttu-id="da266-117">Un bon point de départ est une application UWP DirectX fonctionnelle qui cible déjà l’API Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="da266-117">A good starting point is a working DirectX based UWP app that already targets the Windows Mixed Reality API.</span></span> <span data-ttu-id="da266-118">Pour plus d’informations, consultez [vue d’ensemble du développement DirectX](directx-development-overview.md).</span><span class="sxs-lookup"><span data-stu-id="da266-118">For details see [DirectX development overview](directx-development-overview.md).</span></span> <span data-ttu-id="da266-119">Si vous ne disposez pas d’une application existante et que vous souhaitez commencer à partir de zéro, le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md) est un bon point de départ.</span><span class="sxs-lookup"><span data-stu-id="da266-119">If you do not have an existing app and want to start from scratch the [C++ holographic project template](creating-a-holographic-directx-project.md) is a good starting point.</span></span>

>[!IMPORTANT]
><span data-ttu-id="da266-120">Toute application utilisant la communication à distance holographique doit être créée pour utiliser un [cloisonnement](https://docs.microsoft.com//windows/win32/com/multithreaded-apartments)multithread.</span><span class="sxs-lookup"><span data-stu-id="da266-120">Any app using Holographic Remoting should be authored to use a [multi-threaded apartment](https://docs.microsoft.com//windows/win32/com/multithreaded-apartments).</span></span> <span data-ttu-id="da266-121">L’utilisation d’un [cloisonnement à thread unique](https://docs.microsoft.com//windows/win32/com/single-threaded-apartments) est prise en charge, mais entraîne des performances non optimales et éventuellement des interruptions pendant la lecture.</span><span class="sxs-lookup"><span data-stu-id="da266-121">The use of a [single-threaded appartment](https://docs.microsoft.com//windows/win32/com/single-threaded-apartments) is supported but will lead to sub-optimal performance and possibly stuttering during playback.</span></span> <span data-ttu-id="da266-122">Lors de C++l’utilisation de/WinRT [WinRT :: init_apartment](https://docs.microsoft.com//windows/uwp/cpp-and-winrt-apis/get-started) un cloisonnement multithread est la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="da266-122">When using C++/WinRT [winrt::init_apartment](https://docs.microsoft.com//windows/uwp/cpp-and-winrt-apis/get-started) a multi-threaded apartment is the default.</span></span>

## <a name="get-the-holographic-remoting-nuget-package"></a><span data-ttu-id="da266-123">Procurez-vous le package NuGet de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="da266-123">Get the Holographic Remoting NuGet package</span></span>

<span data-ttu-id="da266-124">Les étapes suivantes sont requises pour ajouter le package NuGet à un projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="da266-124">The following steps are required to add the NuGet package to a project in Visual Studio.</span></span>
1. <span data-ttu-id="da266-125">Ouvrez le projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="da266-125">Open the project in Visual Studio.</span></span>
2. <span data-ttu-id="da266-126">Cliquez avec le bouton droit sur le nœud du projet et sélectionnez **gérer les packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="da266-126">Right-click the project node and select **Manage NuGet Packages...**</span></span>
3. <span data-ttu-id="da266-127">Dans le volet qui s’affiche, cliquez sur **Parcourir** , puis recherchez « accès distant holographique ».</span><span class="sxs-lookup"><span data-stu-id="da266-127">In the panel that appears, click **Browse** and then search for "Holographic Remoting".</span></span>
4. <span data-ttu-id="da266-128">Sélectionnez **Microsoft. holographique. Remoting**, assurez-vous de choisir la version la plus récente de **2. x. x** , puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="da266-128">Select **Microsoft.Holographic.Remoting**, ensure to pick the latest **2.x.x** version and click **Install**.</span></span>
5. <span data-ttu-id="da266-129">Si la boîte de dialogue **Aperçu** s’affiche, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="da266-129">If the **Preview** dialog appears, click **OK**.</span></span>
6. <span data-ttu-id="da266-130">La boîte de dialogue suivante qui s’affiche est le contrat de licence.</span><span class="sxs-lookup"><span data-stu-id="da266-130">The next dialog that appears is the license agreement.</span></span> <span data-ttu-id="da266-131">Cliquez sur **J’accepte** pour accepter le contrat de licence.</span><span class="sxs-lookup"><span data-stu-id="da266-131">Click on **I Accept** to accept the license agreement.</span></span>

>[!IMPORTANT]
><a name="idl"></a><span data-ttu-id="da266-132">Le ```build\native\include\HolographicAppRemoting\Microsoft.Holographic.AppRemoting.idl``` à l’intérieur du package NuGet contient une documentation détaillée sur l’API exposée par la communication à distance holographique.</span><span class="sxs-lookup"><span data-stu-id="da266-132">The ```build\native\include\HolographicAppRemoting\Microsoft.Holographic.AppRemoting.idl``` inside the NuGet package contains detailed documentation for the API exposed by Holographic Remoting.</span></span>

## <a name="modify-the-packageappxmanifest-of-the-application"></a><span data-ttu-id="da266-133">Modifier le package. appxmanifest de l’application</span><span class="sxs-lookup"><span data-stu-id="da266-133">Modify the Package.appxmanifest of the application</span></span>

<span data-ttu-id="da266-134">Pour que l’application prenne en charge le fichier Microsoft. holographique. AppRemoting. dll ajouté par le package NuGet, les étapes suivantes doivent être effectuées sur le projet :</span><span class="sxs-lookup"><span data-stu-id="da266-134">To make the application aware of the Microsoft.Holographic.AppRemoting.dll added by the NuGet package, the following steps need to be taken on the project:</span></span>

1. <span data-ttu-id="da266-135">Dans le Explorateur de solutions cliquez avec le bouton droit sur le fichier **Package. appxmanifest** , puis sélectionnez **Ouvrir avec...**</span><span class="sxs-lookup"><span data-stu-id="da266-135">In the Solution Explorer right-click on the **Package.appxmanifest** file and select **Open With...**</span></span>
2. <span data-ttu-id="da266-136">Sélectionnez **éditeur XML (texte)** , puis cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="da266-136">Select **XML (Text) Editor** and click OK</span></span>
3. <span data-ttu-id="da266-137">Ajoutez les lignes suivantes au fichier et enregistrez</span><span class="sxs-lookup"><span data-stu-id="da266-137">Add the following lines to the file and save</span></span>
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
## <a name="create-the-player-context"></a><span data-ttu-id="da266-138">Créer le contexte du joueur</span><span class="sxs-lookup"><span data-stu-id="da266-138">Create the player context</span></span>

<span data-ttu-id="da266-139">En guise de première étape, l’application doit créer un contexte de joueur.</span><span class="sxs-lookup"><span data-stu-id="da266-139">As a first step the application should create a player context.</span></span>

```cpp
// class declaration:

#include <winrt/Microsoft.Holographic.AppRemoting.h>

...

private:
// PlayerContext used to connect with a Holographic Remoting remote app and display remotely rendered frames
winrt::Microsoft::Holographic::AppRemoting::PlayerContext m_playerContext = nullptr;
```


```cpp
// class implementation:

// Create the player context
// IMPORTANT: This must be done before creating the HolographicSpace (or any other call to the Holographic API).
m_playerContext = winrt::Microsoft::Holographic::AppRemoting::PlayerContext::Create();

```

>[!WARNING]
><span data-ttu-id="da266-140">La communication à distance holographique fonctionne en remplaçant le runtime Windows Mixed Reality qui fait partie de Windows par un Runtime spécifique à distance.</span><span class="sxs-lookup"><span data-stu-id="da266-140">Holographic Remoting works by replacing the Windows Mixed Reality runtime which is part of Windows with a remoting specific runtime.</span></span> <span data-ttu-id="da266-141">Cette opération est effectuée lors de la création du contexte du joueur.</span><span class="sxs-lookup"><span data-stu-id="da266-141">This is done during the creation of the player context.</span></span> <span data-ttu-id="da266-142">Pour cette raison, tout appel sur une API de réalité mixte Windows avant de créer le contexte du joueur peut entraîner un comportement inattendu.</span><span class="sxs-lookup"><span data-stu-id="da266-142">For that reason any call on any Windows Mixed Reality API before creating the player context can result in unexpected behavior.</span></span> <span data-ttu-id="da266-143">L’approche recommandée consiste à créer le contexte du joueur le plus tôt possible avant d’interagir avec une API de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="da266-143">The recommended approach is to create the player context as early as possible before interaction with any Mixed Reality API.</span></span> <span data-ttu-id="da266-144">Ne combinez jamais des objets créés ou récupérés par le biais d’une API Windows Mixed Reality avant l’appel à ```PlayerContext::Create``` avec des objets créés ou récupérés par la suite.</span><span class="sxs-lookup"><span data-stu-id="da266-144">Never mix objects created or retrieved through any Windows Mixed Reality API before the call to ```PlayerContext::Create``` with objects created or retrieved afterwards.</span></span>

<span data-ttu-id="da266-145">Ensuite, vous pouvez créer le HolographicSpace en appelant [HolographicSpace. CreateForCoreWindow](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographicspace.createforcorewindow).</span><span class="sxs-lookup"><span data-stu-id="da266-145">Next the HolographicSpace can be created, by calling [HolographicSpace.CreateForCoreWindow](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographicspace.createforcorewindow).</span></span>

```cpp
m_holographicSpace = winrt::Windows::Graphics::Holographic::HolographicSpace::CreateForCoreWindow(window);
```

## <a name="connect-to-the-remote-app"></a><span data-ttu-id="da266-146">Se connecter à l’application distante</span><span class="sxs-lookup"><span data-stu-id="da266-146">Connect to the remote app</span></span>

<span data-ttu-id="da266-147">Une fois que l’application de lecteur est prête pour le rendu du contenu, une connexion à l’application distante peut être établie.</span><span class="sxs-lookup"><span data-stu-id="da266-147">Once the player app is ready for rendering content a connection to the remote app can be established.</span></span>

<span data-ttu-id="da266-148">La connexion peut être établie de l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="da266-148">The connection can be established in one of the following ways:</span></span>
1) <span data-ttu-id="da266-149">L’application de lecteur s’exécutant sur HoloLens 2 se connecte à l’application distante.</span><span class="sxs-lookup"><span data-stu-id="da266-149">The player app running on HoloLens 2 connects to the remote app.</span></span>
2) <span data-ttu-id="da266-150">L’application distante se connecte à l’application de lecteur s’exécutant sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="da266-150">The remote app connects to the player app running on HoloLens 2.</span></span>

<span data-ttu-id="da266-151">Pour vous connecter à partir de l’application du lecteur à l’application distante, appelez la méthode ```Connect``` sur le contexte du lecteur en spécifiant le nom d’hôte et le port.</span><span class="sxs-lookup"><span data-stu-id="da266-151">To connect from the player app to the remote app call the ```Connect``` method on the player context specifying the hostname and port.</span></span> <span data-ttu-id="da266-152">Le port par défaut est **8265**.</span><span class="sxs-lookup"><span data-stu-id="da266-152">The default port is **8265**.</span></span>

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
><span data-ttu-id="da266-153">Comme pour toute C++API/WinRT ```Connect``` peut lever une exception WinRT :: hresult_error qui doit être gérée.</span><span class="sxs-lookup"><span data-stu-id="da266-153">As with any C++/WinRT API ```Connect``` might throw an winrt::hresult_error which needs to be handled.</span></span>

<span data-ttu-id="da266-154">L’écoute des connexions entrantes sur l’application du lecteur peut être effectuée en appelant la méthode ```Listen```.</span><span class="sxs-lookup"><span data-stu-id="da266-154">Listening for incoming connections on the player app can be done by calling the ```Listen``` method.</span></span> <span data-ttu-id="da266-155">Le port de liaison et le port de transport peuvent être spécifiés au cours de cet appel.</span><span class="sxs-lookup"><span data-stu-id="da266-155">Both the handshake port and transport port can be specified during this call.</span></span> <span data-ttu-id="da266-156">Le port de négociation est utilisé pour le protocole de transfert initial.</span><span class="sxs-lookup"><span data-stu-id="da266-156">The handshake port is used for the initial handshake.</span></span> <span data-ttu-id="da266-157">Les données sont ensuite envoyées sur le port de transport.</span><span class="sxs-lookup"><span data-stu-id="da266-157">The data is then send over the transport port.</span></span> <span data-ttu-id="da266-158">Les numéros de port **8265** et **8266** sont utilisés par défaut.</span><span class="sxs-lookup"><span data-stu-id="da266-158">By default port number **8265** and **8266** are used.</span></span>

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


## <a name="handling-connection-related-events"></a><span data-ttu-id="da266-159">Gestion des événements liés à la connexion</span><span class="sxs-lookup"><span data-stu-id="da266-159">Handling connection related events</span></span>

<span data-ttu-id="da266-160">Le ```PlayerContext``` expose trois événements pour surveiller l’état de la connexion.</span><span class="sxs-lookup"><span data-stu-id="da266-160">The ```PlayerContext``` exposes three events to monitor the state of the connection</span></span>
1) <span data-ttu-id="da266-161">OnConnected : déclenché lorsqu’une connexion à l’application distante a été établie avec succès.</span><span class="sxs-lookup"><span data-stu-id="da266-161">OnConnected: Triggered when a connection to the remote app has been successfully established.</span></span>
```cpp
m_onConnectedEventToken = m_playerContext.OnConnected([]() 
{
    // Handle connection successfully established
});
```
2) <span data-ttu-id="da266-162">OnDisconnected : déclenché si une connexion établie est terminée ou si une connexion n’a pas pu être établie.</span><span class="sxs-lookup"><span data-stu-id="da266-162">OnDisconnected: Triggered if an established connection is terminated or a connection could not be established.</span></span>
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
><span data-ttu-id="da266-163">Les valeurs ```ConnectionFailureReason``` possibles sont documentées dans le [fichier](#idl)```Microsoft.Holographic.AppRemoting.idl```.</span><span class="sxs-lookup"><span data-stu-id="da266-163">Possible ```ConnectionFailureReason``` values are documented in the ```Microsoft.Holographic.AppRemoting.idl``` [file](#idl).</span></span>

3) <span data-ttu-id="da266-164">OnListening : lors du démarrage de l’écoute des connexions entrantes.</span><span class="sxs-lookup"><span data-stu-id="da266-164">OnListening: When listening for incoming connections starts.</span></span>
```cpp
m_onListeningEventToken = m_playerContext.OnListening([]()
{
    // Handle start listening for incoming connections
});
```

<span data-ttu-id="da266-165">En outre, l’état de la connexion peut être interrogé à l’aide de la propriété ```ConnectionState``` du contexte du lecteur.</span><span class="sxs-lookup"><span data-stu-id="da266-165">Additionally the connection state can be queried using the ```ConnectionState``` property on the player context.</span></span>
```cpp
winrt::Microsoft::Holographic::AppRemoting::ConnectionState state = m_playerContext.ConnectionState();
```

## <a name="display-the-remotely-rendered-frame"></a><span data-ttu-id="da266-166">Afficher le frame rendu à distance</span><span class="sxs-lookup"><span data-stu-id="da266-166">Display the remotely rendered frame</span></span>

<span data-ttu-id="da266-167">Pour afficher le contenu rendu à distance, appelez ```PlayerContext::BlitRemoteFrame``` lors du rendu d’un [HolographicFrame](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographicframe).</span><span class="sxs-lookup"><span data-stu-id="da266-167">To display the remotely rendered content, call ```PlayerContext::BlitRemoteFrame``` while rendering a [HolographicFrame](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographicframe).</span></span> 

<span data-ttu-id="da266-168">```BlitRemoteFrame``` requiert que la mémoire tampon d’arrière-plan pour le HolographicFrame actuel soit liée en tant que cible de rendu.</span><span class="sxs-lookup"><span data-stu-id="da266-168">```BlitRemoteFrame``` requires that the back buffer for the current HolographicFrame is bound as render target.</span></span> <span data-ttu-id="da266-169">La mémoire tampon d’arrière-plan peut être reçue à partir du [HolographicCameraRenderingParameters](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographicframe.getrenderingparameters) via la propriété [Direct3D11BackBuffer](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.direct3d11backbuffer) .</span><span class="sxs-lookup"><span data-stu-id="da266-169">The back buffer can be received from the [HolographicCameraRenderingParameters](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographicframe.getrenderingparameters) via the [Direct3D11BackBuffer](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.direct3d11backbuffer) property.</span></span>

<span data-ttu-id="da266-170">Quand elle est appelée, ```BlitRemoteFrame``` copie la dernière trame reçue de l’application distante dans la mémoire tampon de l’HolographicFrame.</span><span class="sxs-lookup"><span data-stu-id="da266-170">When called, ```BlitRemoteFrame``` copies the latest received frame from the remote application into the BackBuffer of the HolographicFrame.</span></span> <span data-ttu-id="da266-171">En outre, l’ensemble de points de focalisation est défini, si l’application distante a spécifié un point de focus pendant le rendu du frame distant.</span><span class="sxs-lookup"><span data-stu-id="da266-171">Additionally the focus point set is set, if the remote application has specified a focus point during the rendering of the remote frame.</span></span>

```cpp
// Blit the remote frame into the backbuffer for the HolographicFrame.
winrt::Microsoft::Holographic::AppRemoting::BlitResult result = m_playerContext.BlitRemoteFrame();
```

>[!NOTE]
><span data-ttu-id="da266-172">```PlayerContext::BlitRemoteFrame``` remplace potentiellement le point de focus du frame actuel.</span><span class="sxs-lookup"><span data-stu-id="da266-172">```PlayerContext::BlitRemoteFrame``` potentially overwrites the focus point for the current frame.</span></span> 
>- <span data-ttu-id="da266-173">Pour spécifier un point de focus de secours, appelez [HolographicCameraRenderingParameters :: SetFocusPoint](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.setfocuspoint) avant ```PlayerContext::BlitRemoteFrame```.</span><span class="sxs-lookup"><span data-stu-id="da266-173">To specify a fallback focus point, call [HolographicCameraRenderingParameters::SetFocusPoint](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.setfocuspoint) before ```PlayerContext::BlitRemoteFrame```.</span></span> 
>- <span data-ttu-id="da266-174">Pour remplacer le point de focus distant, appelez [HolographicCameraRenderingParameters :: SetFocusPoint](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.setfocuspoint) après ```PlayerContext::BlitRemoteFrame```.</span><span class="sxs-lookup"><span data-stu-id="da266-174">To overwrite the remote focus point, call [HolographicCameraRenderingParameters::SetFocusPoint](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.setfocuspoint)  after ```PlayerContext::BlitRemoteFrame```.</span></span>

<span data-ttu-id="da266-175">En cas de réussite, ```BlitRemoteFrame``` retourne ```BlitResult::Success_Color```.</span><span class="sxs-lookup"><span data-stu-id="da266-175">On success, ```BlitRemoteFrame``` returns ```BlitResult::Success_Color```.</span></span> <span data-ttu-id="da266-176">Dans le cas contraire, elle retourne la raison de l’échec :</span><span class="sxs-lookup"><span data-stu-id="da266-176">Otherwise it returns the failure reason:</span></span>
- <span data-ttu-id="da266-177">```BlitResult::Failed_NoRemoteFrameAvailable```: échec, car aucun frame distant n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="da266-177">```BlitResult::Failed_NoRemoteFrameAvailable```: Failed because no remote frame is available.</span></span>
- <span data-ttu-id="da266-178">```BlitResult::Failed_NoCamera```: échec, car aucun appareil photo n’est présent.</span><span class="sxs-lookup"><span data-stu-id="da266-178">```BlitResult::Failed_NoCamera```: Failed because no camera present.</span></span>
- <span data-ttu-id="da266-179">```BlitResult::Failed_RemoteFrameTooOld```: échec, car le frame distant est trop ancien (consultez la propriété PlayerContext :: BlitRemoteFrameTimeout).</span><span class="sxs-lookup"><span data-stu-id="da266-179">```BlitResult::Failed_RemoteFrameTooOld```: Failed because remote frame is too old (see PlayerContext::BlitRemoteFrameTimeout property).</span></span>

>[!IMPORTANT]
> <span data-ttu-id="da266-180">À partir de la version [2.1.0](holographic-remoting-version-history.md#v2.1.0) , un joueur personnalisé peut utiliser la reprojection de profondeur via la communication à distance holographique.</span><span class="sxs-lookup"><span data-stu-id="da266-180">Starting with version [2.1.0](holographic-remoting-version-history.md#v2.1.0) it is possible with a custom player to use depth reprojection via Holographic Remoting.</span></span>

<span data-ttu-id="da266-181">```BlitResult``` pouvez également retourner des ```BlitResult::Success_Color_Depth``` dans les conditions suivantes :</span><span class="sxs-lookup"><span data-stu-id="da266-181">```BlitResult``` can also return ```BlitResult::Success_Color_Depth``` under the following conditions:</span></span>

- <span data-ttu-id="da266-182">L’application distante a validé un tampon de profondeur par le biais de [HolographicCameraRenderingParameters. CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_).</span><span class="sxs-lookup"><span data-stu-id="da266-182">The remote app has committed a depth buffer via [HolographicCameraRenderingParameters.CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_).</span></span>
- <span data-ttu-id="da266-183">L’application de joueur personnalisée a lié une mémoire tampon de profondeur valide avant d’appeler ```BlitRemoteFrame```.</span><span class="sxs-lookup"><span data-stu-id="da266-183">The custom player app has bound a valid depth buffer before calling ```BlitRemoteFrame```.</span></span>

<span data-ttu-id="da266-184">Si ces conditions sont remplies ```BlitRemoteFrame``` confondra la profondeur à distance dans la mémoire tampon de profondeur locale actuellement liée.</span><span class="sxs-lookup"><span data-stu-id="da266-184">If these conditions are met ```BlitRemoteFrame``` will blit the remote depth into the currently bound local depth buffer.</span></span> <span data-ttu-id="da266-185">Vous pouvez ensuite afficher du contenu local supplémentaire qui aura une intersection de profondeur avec le contenu rendu distant.</span><span class="sxs-lookup"><span data-stu-id="da266-185">You can then render additional local content which will have depth intersection with the remote rendered content.</span></span> <span data-ttu-id="da266-186">En outre, vous pouvez valider le tampon de profondeur local à l’aide de [HolographicCameraRenderingParameters. CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_) dans votre lecteur personnalisé pour effectuer une reprojection de profondeur pour le contenu rendu local et distant.</span><span class="sxs-lookup"><span data-stu-id="da266-186">Additionally you can commit the local depth buffer via [HolographicCameraRenderingParameters.CommitDirect3D11DepthBuffer](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer#Windows_Graphics_Holographic_HolographicCameraRenderingParameters_CommitDirect3D11DepthBuffer_Windows_Graphics_DirectX_Direct3D11_IDirect3DSurface_) in your custom player to have depth reprojection for remote and local rendered content.</span></span> <span data-ttu-id="da266-187">Pour plus d’informations, consultez [reprojection de profondeur](hologram-stability.md#reprojection) .</span><span class="sxs-lookup"><span data-stu-id="da266-187">See [Depth Reprojection](hologram-stability.md#reprojection) for details.</span></span>

### <a name="projection-transform-mode"></a><span data-ttu-id="da266-188">Mode de transformation de projection</span><span class="sxs-lookup"><span data-stu-id="da266-188">Projection Transform Mode</span></span>

<span data-ttu-id="da266-189">L’un des problèmes qui se pose lorsque vous utilisez la reprojection de profondeur via la communication à distance holographique est que le contenu distant peut être rendu avec une transformation de projection différente de celle du contenu local affiché directement par votre application de lecteur personnalisée.</span><span class="sxs-lookup"><span data-stu-id="da266-189">One problem which surfaces when using depth reprojection via Holographic Remoting is that the remote content can be rendered with a different projection transform than local content directly rendered by your custom player app.</span></span> <span data-ttu-id="da266-190">Un cas d’usage courant consiste à spécifier des valeurs différentes pour le plan near et Far (via [HolographicCamera :: SetNearPlaneDistance](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera.setnearplanedistance) et [HolographicCamera :: SetFarPlaneDistance](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera.setfarplanedistance)) du côté joueur et du côté distant.</span><span class="sxs-lookup"><span data-stu-id="da266-190">A common use-case is to specify different values for near and far plane (via [HolographicCamera::SetNearPlaneDistance](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera.setnearplanedistance) and [HolographicCamera::SetFarPlaneDistance](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera.setfarplanedistance)) on the player side and the remote side.</span></span> <span data-ttu-id="da266-191">Dans ce cas, il n’est pas évident que la transformation de projection côté joueur doit refléter les distances à distance de plan proche/lointain ou celles locales.</span><span class="sxs-lookup"><span data-stu-id="da266-191">In this case it's not clear if the projection transform on the player side should reflect the remote near/far plane distances or the local ones.</span></span>

<span data-ttu-id="da266-192">À partir de la version [2.1.0](holographic-remoting-version-history.md#v2.1.0) , vous pouvez contrôler le mode de transformation de projection via ```PlayerContext::ProjectionTransformConfig```.</span><span class="sxs-lookup"><span data-stu-id="da266-192">Starting with version [2.1.0](holographic-remoting-version-history.md#v2.1.0) you can control the projection transform mode via ```PlayerContext::ProjectionTransformConfig```.</span></span> <span data-ttu-id="da266-193">Les valeurs prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="da266-193">Supported values are:</span></span>

- <span data-ttu-id="da266-194">```Local``` - [HolographicCameraPose ::P rojectiontransform](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerapose.projectiontransform) retourne une transformation de projection qui reflète les distances de plan proche/lointain définies par votre application de lecteur personnalisée sur le HolographicCamera.</span><span class="sxs-lookup"><span data-stu-id="da266-194">```Local``` - [HolographicCameraPose::ProjectionTransform](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerapose.projectiontransform) returns a projection transform which reflects the near/far plane distances set by your custom player app on the HolographicCamera.</span></span>
- <span data-ttu-id="da266-195">```Remote``` transformation de projection reflète les distances de plan proche/éloignées spécifiées par l’application distante.</span><span class="sxs-lookup"><span data-stu-id="da266-195">```Remote``` - Projection transform reflects the near/far plane distances specified by the remote app.</span></span>
- <span data-ttu-id="da266-196">```Merged``` les distances proches/lointaines de votre application distante et votre application de lecteur personnalisé sont fusionnées.</span><span class="sxs-lookup"><span data-stu-id="da266-196">```Merged``` - Near/Far plane distances from your remote app and your custom player app are merged.</span></span> <span data-ttu-id="da266-197">Par défaut, cette opération s’effectue en tenant au minimum les distances proches du plan et le maximum des distances du plan lointain.</span><span class="sxs-lookup"><span data-stu-id="da266-197">By default this is done by taking the minimum of the near plane distances and the maximum of the far plane distances.</span></span> <span data-ttu-id="da266-198">Si le côté distant ou local est inversé, disons < près, les distances à proximité du plan distant sont retournées.</span><span class="sxs-lookup"><span data-stu-id="da266-198">In case either the remote or local side are inverted, say far < near, the remote near/far plane distances are flipped.</span></span>

## <a name="optional-set-blitremoteframetimeout"></a><span data-ttu-id="da266-199">Facultatif : Set BlitRemoteFrameTimeout<a name="BlitRemoteFrameTimeout"></a></span><span class="sxs-lookup"><span data-stu-id="da266-199">Optional: Set BlitRemoteFrameTimeout <a name="BlitRemoteFrameTimeout"></a></span></span>
>[!IMPORTANT]
> <span data-ttu-id="da266-200">```PlayerContext::BlitRemoteFrameTimeout``` est pris en charge à partir de la version [2.0.9](holographic-remoting-version-history.md#v2.0.9).</span><span class="sxs-lookup"><span data-stu-id="da266-200">```PlayerContext::BlitRemoteFrameTimeout``` is supported starting with version [2.0.9](holographic-remoting-version-history.md#v2.0.9).</span></span> 

<span data-ttu-id="da266-201">La propriété ```PlayerContext::BlitRemoteFrameTimeout``` spécifie la durée pendant laquelle un frame distant est réutilisé si aucune nouvelle trame distante n’est reçue.</span><span class="sxs-lookup"><span data-stu-id="da266-201">The ```PlayerContext::BlitRemoteFrameTimeout``` property specifies the amount of time a remote frame is reused if no new remote frame is received.</span></span> 

<span data-ttu-id="da266-202">Un cas d’usage courant consiste à permettre au délai d’attente de BlitRemoteFrame d’afficher un écran vide si aucun nouveau Frame n’est reçu pendant un certain laps de temps.</span><span class="sxs-lookup"><span data-stu-id="da266-202">A common use-case is to enable the BlitRemoteFrame timeout to display a blank screen if no new frames are received for a certain amount of time.</span></span> <span data-ttu-id="da266-203">Quand cette option est activée, le type de retour de la méthode ```BlitRemoteFrame``` peut également être utilisé pour basculer vers un contenu de secours rendu localement.</span><span class="sxs-lookup"><span data-stu-id="da266-203">When enabled the return type of the ```BlitRemoteFrame``` method can also be used to switch to a locally rendered fallback content.</span></span> 

<span data-ttu-id="da266-204">Pour activer le délai d’expiration, définissez la valeur de la propriété sur une durée égale ou supérieure à 100 ms.</span><span class="sxs-lookup"><span data-stu-id="da266-204">To enable the timeout, set the property value to a duration equal or greater than 100ms.</span></span> <span data-ttu-id="da266-205">Pour désactiver le délai d’attente, affectez la valeur zéro à la propriété.</span><span class="sxs-lookup"><span data-stu-id="da266-205">To disable the timeout, set the property to zero duration.</span></span> <span data-ttu-id="da266-206">Si le délai d’expiration est activé et qu’aucun frame distant n’est reçu pour la durée définie, BlitRemoteFrame échoue et retourne ```Failed_RemoteFrameTooOld``` jusqu’à la réception d’un nouveau Frame distant.</span><span class="sxs-lookup"><span data-stu-id="da266-206">If the timeout is enabled and no remote frame is received for the set duration, BlitRemoteFrame will fail and return ```Failed_RemoteFrameTooOld``` until a new remote frame is received.</span></span>

```cpp
using namespace std::chrono_literals;

// Set the BlitRemoteFrame timeout to 0.5s
m_playerContext.BlitRemoteFrameTimeout(500ms);
```

## <a name="optional-get-statistics-about-the-last-remote-frame"></a><span data-ttu-id="da266-207">Facultatif : obtenir des statistiques sur le dernier frame distant</span><span class="sxs-lookup"><span data-stu-id="da266-207">Optional: Get statistics about the last remote frame</span></span>

<span data-ttu-id="da266-208">Pour diagnostiquer les problèmes de performances ou de réseau, les statistiques relatives au dernier frame distant peuvent être récupérées via la propriété ```PlayerContext::LastFrameStatistics```.</span><span class="sxs-lookup"><span data-stu-id="da266-208">To diagnose performance or network issues, statistics about the last remote frame can be retrieved via the ```PlayerContext::LastFrameStatistics``` property.</span></span> <span data-ttu-id="da266-209">Les statistiques sont mises à jour lors de l’appel à [HolographicFrame ::P resentusingcurrentprediction](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographicframe.presentusingcurrentprediction).</span><span class="sxs-lookup"><span data-stu-id="da266-209">Statistics are updated during the call to [HolographicFrame::PresentUsingCurrentPrediction](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographicframe.presentusingcurrentprediction).</span></span>

```cpp
// Get statistics for the last presented frame.
winrt::Microsoft::Holographic::AppRemoting::PlayerFrameStatistics statistics = m_playerContext.LastFrameStatistics();
```

<span data-ttu-id="da266-210">Pour plus d’informations, consultez la documentation ```PlayerFrameStatistics``` dans le [fichier](#idl)```Microsoft.Holographic.AppRemoting.idl```.</span><span class="sxs-lookup"><span data-stu-id="da266-210">For more details, see the ```PlayerFrameStatistics``` documentation in the ```Microsoft.Holographic.AppRemoting.idl``` [file](#idl).</span></span>

## <a name="optional-custom-data-channels"></a><span data-ttu-id="da266-211">Facultatif : canaux de données personnalisés</span><span class="sxs-lookup"><span data-stu-id="da266-211">Optional: Custom data channels</span></span>

<span data-ttu-id="da266-212">Les canaux de données personnalisés peuvent être utilisés pour envoyer des données utilisateur sur la connexion de communication à distance déjà établie.</span><span class="sxs-lookup"><span data-stu-id="da266-212">Custom data channels can be used to send user data over the already established remoting connection.</span></span> <span data-ttu-id="da266-213">Pour plus d’informations, consultez [canaux de données personnalisés](holographic-remoting-custom-data-channels.md) .</span><span class="sxs-lookup"><span data-stu-id="da266-213">See [custom data channels](holographic-remoting-custom-data-channels.md) for more information.</span></span>

## <a name="see-also"></a><span data-ttu-id="da266-214">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="da266-214">See Also</span></span>
* [<span data-ttu-id="da266-215">Écriture d’une application distante de communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="da266-215">Writing a Holographic Remoting remote app</span></span>](holographic-remoting-create-host.md)
* [<span data-ttu-id="da266-216">Canaux de données de communication à distance holographique personnalisés</span><span class="sxs-lookup"><span data-stu-id="da266-216">Custom Holographic Remoting data channels</span></span>](holographic-remoting-custom-data-channels.md)
* [<span data-ttu-id="da266-217">Établissement d’une connexion sécurisée à l’aide de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="da266-217">Establishing a secure connection with Holographic Remoting</span></span>](holographic-remoting-secure-connection.md)
* [<span data-ttu-id="da266-218">Résolution des problèmes et limitations de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="da266-218">Holographic Remoting troubleshooting and limitations</span></span>](holographic-remoting-troubleshooting.md)
* [<span data-ttu-id="da266-219">Termes du contrat de licence de la communication à distance holographique</span><span class="sxs-lookup"><span data-stu-id="da266-219">Holographic Remoting software license terms</span></span>](https://docs.microsoft.com//legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [<span data-ttu-id="da266-220">Déclaration de confidentialité Microsoft</span><span class="sxs-lookup"><span data-stu-id="da266-220">Microsoft Privacy Statement</span></span>](https://go.microsoft.com/fwlink/?LinkId=521839)
