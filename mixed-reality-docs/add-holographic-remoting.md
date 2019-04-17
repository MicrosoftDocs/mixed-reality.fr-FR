---
title: Ajouter la communication à distance HOLOGRAPHIQUE
description: Explique comment utiliser les holographique de communication à distance pour restituer hologrammes à un HoloLens sur le réseau.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, communication à distance HOLOGRAPHIQUE, rendu à distance, réseau de rendu, HoloLens, hologrammes à distance
ms.openlocfilehash: 4726c6af43fe1b89fc8298e459a1af9dfa5fc667
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597136"
---
# <a name="add-holographic-remoting"></a><span data-ttu-id="6eb04-104">Ajouter la communication à distance HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="6eb04-104">Add holographic remoting</span></span>

> [!NOTE]
> <span data-ttu-id="6eb04-105">Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).</span><span class="sxs-lookup"><span data-stu-id="6eb04-105">More guidance specific to HoloLens 2 [coming soon](index.md#news-and-notes).</span></span>

## <a name="add-holographic-remoting-to-your-desktop-or-uwp-app"></a><span data-ttu-id="6eb04-106">Ajouter HOLOGRAPHIQUE communication à distance à votre bureau ou d’une application UWP</span><span class="sxs-lookup"><span data-stu-id="6eb04-106">Add holographic remoting to your desktop or UWP app</span></span>

<span data-ttu-id="6eb04-107">Cette page décrit comment ajouter holographique de communication à distance à un bureau ou une application UWP.</span><span class="sxs-lookup"><span data-stu-id="6eb04-107">This page describes how to add Holographic Remoting to a desktop or UWP app.</span></span>

<span data-ttu-id="6eb04-108">Communication à distance HOLOGRAPHIQUE permet à votre application cibler un HoloLens avec HOLOGRAPHIQUE contenu hébergé sur un PC de bureau ou sur un appareil UWP tels que Xbox One, autorisant l’accès à davantage de ressources système et rend possible d’intégrer à distance [immersives vues](app-views.md) dans les logiciels de PC de bureau existante.</span><span class="sxs-lookup"><span data-stu-id="6eb04-108">Holographic remoting allows your app to target a HoloLens with holographic content hosted on a desktop PC or on a UWP device such as the Xbox One, allowing access to more system resources and making it possible to integrate remote [immersive views](app-views.md) into existing desktop PC software.</span></span> <span data-ttu-id="6eb04-109">Une application hôte de communication à distance reçoit un flux de données d’entrée à partir d’un HoloLens, restitue le contenu dans un affichage virtuel immersif et diffuse les images du contenu vers HoloLens.</span><span class="sxs-lookup"><span data-stu-id="6eb04-109">A remoting host app receives an input data stream from a HoloLens, renders content in a virtual immersive view, and streams content frames back to HoloLens.</span></span> <span data-ttu-id="6eb04-110">La connexion est établie à l’aide de Wi-Fi standard.</span><span class="sxs-lookup"><span data-stu-id="6eb04-110">The connection is made using standard Wi-Fi.</span></span> <span data-ttu-id="6eb04-111">Pour utiliser la communication à distance, vous utilise un package NuGet pour ajouter HOLOGRAPHIQUE communication à distance à votre bureau ou d’une application UWP et écrire du code pour gérer la connexion et s’affichent dans une vue immersive.</span><span class="sxs-lookup"><span data-stu-id="6eb04-111">To use remoting, you will use a NuGet package to add holographic remoting to your desktop or UWP app, and write code to handle the connection and to render in an immersive view.</span></span> <span data-ttu-id="6eb04-112">Bibliothèques d’assistance sont inclus dans l’exemple de code qui simplifient la tâche de gestion de la connexion de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="6eb04-112">Helper libraries are included in the code sample that simplify the task of handling the device connection.</span></span>

<span data-ttu-id="6eb04-113">Une connexion de communication à distance classique aura aussi faible que la latence de 50 ms.</span><span class="sxs-lookup"><span data-stu-id="6eb04-113">A typical remoting connection will have as low as 50 ms of latency.</span></span> <span data-ttu-id="6eb04-114">L’application de lecteur peut signaler la latence en temps réel.</span><span class="sxs-lookup"><span data-stu-id="6eb04-114">The player app can report the latency in real-time.</span></span>

>[!NOTE]
><span data-ttu-id="6eb04-115">Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="6eb04-115">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="6eb04-116">Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="6eb04-116">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

### <a name="get-the-remoting-nuget-packages"></a><span data-ttu-id="6eb04-117">Obtenir la communication à distance les packages NuGet</span><span class="sxs-lookup"><span data-stu-id="6eb04-117">Get the remoting NuGet packages</span></span>

<span data-ttu-id="6eb04-118">Suivez ces étapes pour obtenir le package NuGet pour la communication à distance holographique et ajoutez une référence à partir de votre projet :</span><span class="sxs-lookup"><span data-stu-id="6eb04-118">Follow these steps to get the NuGet package for holographic remoting, and add a reference from your project:</span></span>
1. <span data-ttu-id="6eb04-119">Accédez à votre projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6eb04-119">Go to your project in Visual Studio.</span></span>
2. <span data-ttu-id="6eb04-120">Avec le bouton droit sur le nœud du projet et sélectionnez **gérer les Packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="6eb04-120">Right-click on the project node and select **Manage NuGet Packages...**</span></span>
3. <span data-ttu-id="6eb04-121">Dans le panneau qui s’affiche, cliquez sur **Parcourir** , puis recherchez « HOLOGRAPHIQUE communication à distance ».</span><span class="sxs-lookup"><span data-stu-id="6eb04-121">In the panel that appears, click **Browse** and then search for "Holographic Remoting".</span></span>
4. <span data-ttu-id="6eb04-122">Sélectionnez **Microsoft.Holographic.Remoting** et cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="6eb04-122">Select **Microsoft.Holographic.Remoting** and click **Install**.</span></span>
5. <span data-ttu-id="6eb04-123">Si le **aperçu** boîte de dialogue s’affiche, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6eb04-123">If the **Preview** dialog appears, click **OK**.</span></span>
6. <span data-ttu-id="6eb04-124">La boîte de dialogue suivante qui s’affiche est le contrat de licence.</span><span class="sxs-lookup"><span data-stu-id="6eb04-124">The next dialog that appears is the license agreement.</span></span> <span data-ttu-id="6eb04-125">Cliquez sur **J’accepte** pour accepter le contrat de licence.</span><span class="sxs-lookup"><span data-stu-id="6eb04-125">Click on **I Accept** to accept the license agreement.</span></span>

### <a name="create-the-holographicstreamerhelpers"></a><span data-ttu-id="6eb04-126">Créer le HolographicStreamerHelpers</span><span class="sxs-lookup"><span data-stu-id="6eb04-126">Create the HolographicStreamerHelpers</span></span>

<span data-ttu-id="6eb04-127">Tout d’abord, nous avons besoin d’une instance de HolographicStreamerHelpers.</span><span class="sxs-lookup"><span data-stu-id="6eb04-127">First, we need an instance of HolographicStreamerHelpers.</span></span> <span data-ttu-id="6eb04-128">Ajouter à la classe qui se chargera de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="6eb04-128">Add this to the class that will be handling remoting.</span></span>

```
#include <HolographicStreamerHelpers.h>

   private:
       Microsoft::Holographic::HolographicStreamerHelpers^ m_streamerHelpers;
```

<span data-ttu-id="6eb04-129">Vous devez également suivre l’état de la connexion.</span><span class="sxs-lookup"><span data-stu-id="6eb04-129">You'll also need to track connection state.</span></span> <span data-ttu-id="6eb04-130">Si vous souhaitez afficher l’aperçu, vous devez avoir une texture à copier.</span><span class="sxs-lookup"><span data-stu-id="6eb04-130">If you want to render the preview, you need to have a texture to copy it to.</span></span> <span data-ttu-id="6eb04-131">Également, vous avez besoin de quelques choses comme un verrou d’état de connexion, un moyen de stocker l’adresse IP de HoloLens et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="6eb04-131">You also need a few things like a connection state lock, some way of storing the IP address of HoloLens, and so on.</span></span>

```
private:
       Microsoft::Holographic::HolographicStreamerHelpers^ m_streamerHelpers;

       Microsoft::WRL::Wrappers::SRWLock                   m_connectionStateLock;

       RemotingHostSample::AppView^                        m_appView;
       Platform::String^                                   m_ipAddress;
       Microsoft::Holographic::HolographicStreamerHelpers^ m_streamerHelpers;

       Microsoft::WRL::Wrappers::CriticalSection           m_deviceLock;
       Microsoft::WRL::ComPtr<IDXGISwapChain1>             m_swapChain;
       Microsoft::WRL::ComPtr<ID3D11Texture2D>             m_spTexture;
```

### <a name="initialize-holographicstreamerhelpers-and-connect-to-hololens"></a><span data-ttu-id="6eb04-132">Initialiser HolographicStreamerHelpers et se connecter à HoloLens</span><span class="sxs-lookup"><span data-stu-id="6eb04-132">Initialize HolographicStreamerHelpers and connect to HoloLens</span></span>

<span data-ttu-id="6eb04-133">Pour vous connecter à un appareil HoloLens, créez une instance de HolographicStreamerHelpers et connectez-vous à l’adresse IP cible.</span><span class="sxs-lookup"><span data-stu-id="6eb04-133">To connect to a HoloLens device, create an instance of HolographicStreamerHelpers and connect to the target IP address.</span></span> <span data-ttu-id="6eb04-134">Vous devez définir la taille de trame vidéo pour correspondre à la largeur d’affichage HoloLens et la hauteur, étant donné que la bibliothèque de communication à distance HOLOGRAPHIQUE attend les résolutions d’encodeur et décodeur correspondre exactement.</span><span class="sxs-lookup"><span data-stu-id="6eb04-134">You will need to set the video frame size to match the HoloLens display width and height, because the Holographic Remoting library expects the encoder and decoder resolutions to match exactly.</span></span>

```
m_streamerHelpers = ref new HolographicStreamerHelpers();
       m_streamerHelpers->CreateStreamer(m_d3dDevice);

       // We currently need to stream at 720p because that's the resolution of our remote display.
       // There is a check in the holographic streamer that makes sure the remote and local
       // resolutions match. The default streamer resolution is 1080p.
       m_streamerHelpers->SetVideoFrameSize(1280, 720);

       try
       {
           m_streamerHelpers->Connect(m_ipAddress->Data(), 8001);
       }
       catch (Platform::Exception^ ex)
       {
           DebugLog(L"Connect failed with hr = 0x%08X", ex->HResult);
       }
```

<span data-ttu-id="6eb04-135">La connexion de l’appareil est asynchrone.</span><span class="sxs-lookup"><span data-stu-id="6eb04-135">The device connection is asynchronous.</span></span> <span data-ttu-id="6eb04-136">Votre application a besoin pour fournir des gestionnaires d’événements pour se connecter, vous déconnecter et envoyer des événements par frame.</span><span class="sxs-lookup"><span data-stu-id="6eb04-136">Your app needs to provide event handlers for connect, disconnect, and frame send events.</span></span>

<span data-ttu-id="6eb04-137">L’événement OnConnected peut mettre à jour de l’interface utilisateur, démarrage du rendu et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="6eb04-137">The OnConnected event can update the UI, start rendering, and so on.</span></span> <span data-ttu-id="6eb04-138">Dans notre exemple de code Windows desktop, nous mettre à jour le titre de la fenêtre avec un message « connecté ».</span><span class="sxs-lookup"><span data-stu-id="6eb04-138">In our desktop code sample, we update the window title with a "connected" message.</span></span>

```
m_streamerHelpers->OnConnected += ref new ConnectedEvent(
           [this]()
           {
               UpdateWindowTitle();
           });
```

<span data-ttu-id="6eb04-139">L’événement OnDisconnected peut gérer la reconnexion, mises à jour de l’interface utilisateur et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="6eb04-139">The OnDisconnected event can handle reconnection, UI updates, and so on.</span></span> <span data-ttu-id="6eb04-140">Dans cet exemple, nous vous reconnecter en cas de panne temporaire.</span><span class="sxs-lookup"><span data-stu-id="6eb04-140">In this example, we reconnect if there is a transient failure.</span></span>

```
Platform::WeakReference streamerHelpersWeakRef = Platform::WeakReference(m_streamerHelpers);
       m_streamerHelpers->OnDisconnected += ref new DisconnectedEvent(
           [this, streamerHelpersWeakRef](_In_ HolographicStreamerConnectionFailureReason failureReason)
           {
               DebugLog(L"Disconnected with reason %d", failureReason);
               UpdateWindowTitle();

               // Reconnect if this is a transient failure.
               if (failureReason == HolographicStreamerConnectionFailureReason::Unreachable ||
                   failureReason == HolographicStreamerConnectionFailureReason::ConnectionLost)
               {
                   DebugLog(L"Reconnecting...");

                   try
                   {
                       auto helpersResolved = streamerHelpersWeakRef.Resolve<HolographicStreamerHelpers>();
                       if (helpersResolved)
                       {
                           helpersResolved->Connect(m_ipAddress->Data(), 8001);
                       }
                       else
                       {
                           DebugLog(L"Failed to reconnect because a disconnect has already occurred.\n");
                       }
                   }
                   catch (Platform::Exception^ ex)
                   {
                       DebugLog(L"Connect failed with hr = 0x%08X", ex->HResult);
                   }
               }
               else
               {
                   DebugLog(L"Disconnected with unrecoverable error, not attempting to reconnect.");
               }
           });
```

<span data-ttu-id="6eb04-141">Lorsque le composant de communication à distance est prêt à envoyer une image, votre application est fournie une occasion de faire une copie de celle-ci dans le SendFrameEvent.</span><span class="sxs-lookup"><span data-stu-id="6eb04-141">When the remoting component is ready to send a frame, your app is provided an opportunity to make a copy of it in the SendFrameEvent.</span></span> <span data-ttu-id="6eb04-142">Ici, nous copions le frame dans une chaîne de permutation afin que nous pouvons l’afficher dans une fenêtre d’aperçu.</span><span class="sxs-lookup"><span data-stu-id="6eb04-142">Here, we copy the frame to a swap chain so that we can display it in a preview window.</span></span>

```
m_streamerHelpers->OnSendFrame += ref new SendFrameEvent(
           [this](_In_ const ComPtr<ID3D11Texture2D>& spTexture, _In_ FrameMetadata metadata)
           {
               if (m_showPreview)
               {
                   ComPtr<ID3D11Device1> spDevice = m_appView->GetDeviceResources()->GetD3DDevice();
                   ComPtr<ID3D11DeviceContext> spContext = m_appView->GetDeviceResources()->GetD3DDeviceContext();

                   ComPtr<ID3D11Texture2D> spBackBuffer;
                   ThrowIfFailed(m_swapChain->GetBuffer(0, IID_PPV_ARGS(&spBackBuffer)));

                   spContext->CopySubresourceRegion(
                       spBackBuffer.Get(), // dest
                       0,                  // dest subresource
                       0, 0, 0,            // dest x, y, z
                       spTexture.Get(),    // source
                       0,                  // source subresource
                       nullptr);           // source box, null means the entire resource

                   DXGI_PRESENT_PARAMETERS parameters = { 0 };
                   ThrowIfFailed(m_swapChain->Present1(1, 0, &parameters));
               }
           });
```

### <a name="render-holographic-content"></a><span data-ttu-id="6eb04-143">Afficher le contenu HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="6eb04-143">Render holographic content</span></span>

<span data-ttu-id="6eb04-144">Pour afficher le contenu à l’aide de la communication à distance, vous définissez un IFrameworkView virtuel au sein de votre bureau ou d’une application UWP et traiter les trames HOLOGRAPHIQUE à partir de la communication à distance.</span><span class="sxs-lookup"><span data-stu-id="6eb04-144">To render content using remoting, you set up a virtual IFrameworkView within your desktop or UWP app and process holographic frames from remoting.</span></span> <span data-ttu-id="6eb04-145">Toutes les API Windows HOLOGRAPHIQUE sont utilise que la même façon par cette vue, mais il est configurée de manière légèrement différente.</span><span class="sxs-lookup"><span data-stu-id="6eb04-145">All of the Windows Holographic APIs are uses the same way by this view, but it is set up slightly differently.</span></span>

<span data-ttu-id="6eb04-146">Au lieu de les créer vous-même, les composants d’espace et de reconnaissance vocale HOLOGRAPHIQUE proviennent de votre classe HolographicRemotingHelpers :</span><span class="sxs-lookup"><span data-stu-id="6eb04-146">Instead of creating them yourself, the holographic space and speech components come from your HolographicRemotingHelpers class:</span></span>

```
m_appView->Initialize(m_streamerHelpers->HolographicSpace, m_streamerHelpers->RemoteSpeech);
```

<span data-ttu-id="6eb04-147">Au lieu d’utiliser une boucle de mise à jour à l’intérieur d’une méthode d’exécution, vous fournissez des mises à jour de la graduation à partir de la boucle principale de votre bureau ou d’une application UWP.</span><span class="sxs-lookup"><span data-stu-id="6eb04-147">Instead of using an update loop inside of a Run method, you provide tick updates from the main loop of your desktop or UWP app.</span></span> <span data-ttu-id="6eb04-148">Cela permet à votre bureau ou une application UWP de rester dans le contrôle du traitement du message.</span><span class="sxs-lookup"><span data-stu-id="6eb04-148">This allows your desktop or UWP app to remain in control of message processing.</span></span>

```
void DesktopWindow::Tick()
   {
       auto lock = m_deviceLock.Lock();
       m_appView->Tick();

       // display preview, etc.
   }
```

<span data-ttu-id="6eb04-149">Méthode de Tick() de la vue HOLOGRAPHIQUE application termine une itération de la mise à jour, le dessin, la boucle présente.</span><span class="sxs-lookup"><span data-stu-id="6eb04-149">The holographic app view's Tick() method completes one iteration of the update, draw, present loop.</span></span>

```
void AppView::Tick()
   {
       if (m_main)
       {
           // When running on Windows Holographic, we can use the holographic rendering system.
           HolographicFrame^ holographicFrame = m_main->Update();

           if (holographicFrame && m_main->Render(holographicFrame))
           {
               // The holographic frame has an API that presents the swap chain for each
               // holographic camera.
               m_deviceResources->Present(holographicFrame);
           }
       }
   }
```

<span data-ttu-id="6eb04-150">La mise à jour de la vue HOLOGRAPHIQUE application, le rendu et la boucle présente est exactement le même comme c’est lors de l’exécution sur HoloLens -, à ceci près que vous avez accès à une plus grande capacité de ressources système sur votre ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="6eb04-150">The holographic app view update, render, and present loop is exactly the same as it is when running on HoloLens - except that you have access to a much greater amount of system resources on your desktop PC.</span></span> <span data-ttu-id="6eb04-151">Vous pouvez effectuer le rendu des triangles plus nombreux, ont plusieurs passes de dessins, faire plus physique et utilisent x64 des processus de chargement du contenu qui nécessite plus de 2 Go de RAM.</span><span class="sxs-lookup"><span data-stu-id="6eb04-151">You can render many more triangles, have more drawing passes, do more physics, and use x64 processes to load content that requires more than 2 GB of RAM.</span></span>

### <a name="disconnect-and-end-the-remote-session"></a><span data-ttu-id="6eb04-152">Se déconnecter et fermer la session à distance</span><span class="sxs-lookup"><span data-stu-id="6eb04-152">Disconnect and end the remote session</span></span>

<span data-ttu-id="6eb04-153">Pour déconnecter - par exemple, lorsque l’utilisateur clique sur un bouton de l’interface utilisateur pour se déconnecter - appeler Disconnect() sur le HolographicStreamerHelpers et libérer l’objet.</span><span class="sxs-lookup"><span data-stu-id="6eb04-153">To disconnect - for example, when the user clicks a UI button to disconnect - call Disconnect() on the HolographicStreamerHelpers, and then release the object.</span></span>

```
void DesktopWindow::DisconnectFromRemoteDevice()
   {
       // Disconnecting from the remote device can change the connection state.
       auto exclusiveLock = m_connectionStateLock.LockExclusive();

       if (m_streamerHelpers != nullptr)
       {
           m_streamerHelpers->Disconnect();

           // Reset state
           m_streamerHelpers = nullptr;
       }
   }
```

## <a name="get-the-remoting-player"></a><span data-ttu-id="6eb04-154">Obtenir le lecteur de communication à distance</span><span class="sxs-lookup"><span data-stu-id="6eb04-154">Get the remoting player</span></span>

<span data-ttu-id="6eb04-155">Le joueur de communication à distance Windows holographique est disponible dans le magasin d’applications Windows en tant que point de terminaison pour héberger des applications de communication à distance pour se connecter à.</span><span class="sxs-lookup"><span data-stu-id="6eb04-155">The Windows Holographic remoting player is offered in the Windows app store as an endpoint for remoting host apps to connect to.</span></span> <span data-ttu-id="6eb04-156">Pour obtenir le lecteur de communication à distance Windows HOLOGRAPHIQUE, visitez le magasin d’applications Windows à partir de votre HoloLens, recherchez la communication à distance et télécharger l’application.</span><span class="sxs-lookup"><span data-stu-id="6eb04-156">To get the Windows Holographic remoting player, visit the Windows app store from your HoloLens, search for Remoting, and download the app.</span></span> <span data-ttu-id="6eb04-157">Le lecteur de communication à distance comprend une fonctionnalité permettant d’afficher des statistiques à l’écran, ce qui peut être utile lors du débogage d’héberger des applications de communication à distance.</span><span class="sxs-lookup"><span data-stu-id="6eb04-157">The remoting player includes a feature to display statistics on-screen, which can be useful when debugging remoting host apps.</span></span>

## <a name="notes-and-resources"></a><span data-ttu-id="6eb04-158">Notes de publication et ressources</span><span class="sxs-lookup"><span data-stu-id="6eb04-158">Notes and resources</span></span>

<span data-ttu-id="6eb04-159">La vue HOLOGRAPHIQUE application devez un moyen de fournir votre application avec le périphérique Direct3D, qui doit être utilisé pour initialiser l’espace HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="6eb04-159">The holographic app view will need a way to provide your app with the Direct3D device, which must be used to initialize the holographic space.</span></span> <span data-ttu-id="6eb04-160">Votre application doit utiliser ce périphérique Direct3D pour copier et afficher le frame de la version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="6eb04-160">Your app should use this Direct3D device to copy and display the preview frame.</span></span>

```
internal:
       const std::shared_ptr<DX::DeviceResources>& GetDeviceResources()
       {
           return m_deviceResources;
       }
```

<span data-ttu-id="6eb04-161">**Exemple de code :** Un exemple de code complet Remoting holographique est disponible, ce qui inclut une vue HOLOGRAPHIQUE application qui est compatible avec la communication à distance et les projets d’hôte de communication à distance pour le bureau Win32 UWP DirectX et UWP avec XAML.</span><span class="sxs-lookup"><span data-stu-id="6eb04-161">**Code sample:** A complete Holographic Remoting code sample is available, which includes a holographic application view that is compatible with remoting and remoting host projects for desktop Win32, UWP DirectX, and UWP with XAML.</span></span> <span data-ttu-id="6eb04-162">Pour l’obtenir, cliquez ici :</span><span class="sxs-lookup"><span data-stu-id="6eb04-162">To get it, go here:</span></span>
* [<span data-ttu-id="6eb04-163">Exemple de Code holographique de Windows pour l’accès distant</span><span class="sxs-lookup"><span data-stu-id="6eb04-163">Windows Holographic Code Sample for Remoting</span></span>](https://github.com/Microsoft/HoloLensCompanionKit/)

<span data-ttu-id="6eb04-164">**Remarque de débogage :** La bibliothèque de communication à distance HOLOGRAPHIQUE peut lever des exceptions de première chance.</span><span class="sxs-lookup"><span data-stu-id="6eb04-164">**Debugging note:** The Holographic Remoting library can throw first-chance exceptions.</span></span> <span data-ttu-id="6eb04-165">Ces exceptions peuvent être visibles dans les sessions de débogage, selon les paramètres d’exception de Visual Studio qui sont actives à la fois.</span><span class="sxs-lookup"><span data-stu-id="6eb04-165">These exceptions may be visible in debugging sessions, depending on the Visual Studio exception settings that are active at the time.</span></span> <span data-ttu-id="6eb04-166">Ces exceptions sont interceptées en interne par la bibliothèque de communication à distance holographique et peuvent être ignorées.</span><span class="sxs-lookup"><span data-stu-id="6eb04-166">These exceptions are caught internally by the Holographic Remoting library and can be ignored.</span></span>
