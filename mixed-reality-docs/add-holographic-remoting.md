---
title: Ajouter la communication à distance holographique
description: Explique comment utiliser la communication à distance holographique pour afficher des hologrammes sur le réseau.
author: MikeRiches
ms.author: mriches
ms.date: 05/24/2019
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, accès distant holographique, rendu à distance, rendu réseau, HoloLens, hologrammes distants
ms.openlocfilehash: 71a763b0660867bf910c0dcecb5fba921f19d068
ms.sourcegitcommit: ca949efe0279995a376750d89e23d7123eb44846
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68712429"
---
# <a name="add-holographic-remoting-hololens-1"></a>Ajouter la communication à distance holographique (HoloLens 1)

>[!IMPORTANT]
>Ce document décrit la création d’une application hôte pour HoloLens 1. L’application hôte pour **HoloLens 1** doit utiliser le package NuGet version **1. x. x**. Cela implique que les applications hôtes écrites pour HoloLens 1 ne sont pas compatibles avec HoloLens 2 et vice versa.

## <a name="hololens-2"></a>HoloLens 2

Les développeurs HoloLens qui utilisent la communication à distance holographique doivent mettre à jour leurs applications pour les rendre compatibles avec HoloLens 2. Cela nécessite une nouvelle version du package NuGet de communication à distance holographique. Si une application qui utilise le package NuGet de communication à distance holographique avec un numéro de version inférieur à 2.0.0.0 tente de se connecter au lecteur de communication à distance holographique sur HoloLens 2, la connexion échoue.

>[!NOTE]
>Vous trouverez des conseils spécifiques à HoloLens 2 [ici](holographic-remoting-create-host.md).


## <a name="add-holographic-remoting-to-your-desktop-or-uwp-app"></a>Ajout de la communication à distance holographique à votre application de bureau ou UWP

Cette page explique comment ajouter la communication à distance holographique à une application de bureau ou UWP.

La communication à distance holographique permet à votre application de cibler un HoloLens avec un contenu holographique hébergé sur un ordinateur de bureau ou sur un appareil UWP tel que le Xbox, permettant d’accéder à davantage de ressources système et d’intégrer des [vues immersives](app-views.md) distantes dans logiciel de PC de bureau existant. Une application hôte de communication à distance reçoit un flux de données d’entrée d’un HoloLens, restitue le contenu dans une vue immersive virtuelle et diffuse en continu des frames de contenu vers HoloLens. La connexion est établie à l’aide du Wi-Fi standard. Pour utiliser la communication à distance, vous allez utiliser un package NuGet pour ajouter la communication à distance holographique à votre application de bureau ou UWP, et écrire du code pour gérer la connexion et effectuer un rendu dans une vue immersive. Les bibliothèques d’assistance sont incluses dans l’exemple de code qui simplifie la tâche de gestion de la connexion de l’appareil.

Une connexion à distance classique aura une latence aussi faible que 50 ms de latence. L’application de lecteur peut signaler la latence en temps réel.

>[!NOTE]
>Les extraits de code de cet article illustrent actuellement l' C++utilisation de/CX plutôt que de C++/WinRT conforme C + +17, comme utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).  Les concepts sont équivalents pour C++un projet/WinRT, bien que vous deviez traduire le code.

### <a name="get-the-remoting-nuget-packages"></a>Récupération des packages NuGet de communication à distance

Procédez comme suit pour obtenir le package NuGet pour la communication à distance holographique et ajouter une référence à partir de votre projet:
1. Accédez à votre projet dans Visual Studio.
2. Cliquez avec le bouton droit sur le nœud du projet et sélectionnez **gérer les packages NuGet...**
3. Dans le volet qui s’affiche, cliquez sur **Parcourir** , puis recherchez «accès distant holographique».
4. Sélectionnez **Microsoft. holographique. Remoting** , puis cliquez sur **installer**.
5. Si la boîte de dialogue **Aperçu** s’affiche, cliquez sur **OK**.
6. La boîte de dialogue suivante qui s’affiche est le contrat de licence. Cliquez sur **J’accepte** pour accepter le contrat de licence.

### <a name="create-the-holographicstreamerhelpers"></a>Créer le HolographicStreamerHelpers

Tout d’abord, nous avons besoin d’une instance de HolographicStreamerHelpers. Ajoutez ceci à la classe qui gérera la communication à distance.

```cpp
#include <HolographicStreamerHelpers.h>

   private:
       Microsoft::Holographic::HolographicStreamerHelpers^ m_streamerHelpers;
```

Vous devez également suivre l’état de la connexion. Si vous souhaitez afficher l’aperçu, vous devez avoir une texture sur laquelle la copier. Vous avez également besoin de quelques éléments comme un verrou d’état de connexion, un moyen de stocker l’adresse IP de HoloLens, et ainsi de suite.

```cpp
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

### <a name="initialize-holographicstreamerhelpers-and-connect-to-hololens"></a>Initialiser HolographicStreamerHelpers et se connecter à HoloLens

Pour vous connecter à un appareil HoloLens, créez une instance de HolographicStreamerHelpers et connectez-vous à l’adresse IP cible. Vous devrez définir la taille de l’image vidéo pour qu’elle corresponde à la largeur et à la hauteur de l’affichage HoloLens, car la bibliothèque de communication à distance holographique s’attend à ce que les résolutions d’encodeur et de décodeur correspondent exactement.

```cpp
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

La connexion de l’appareil est asynchrone. Votre application doit fournir des gestionnaires d’événements pour les événements de connexion, de déconnexion et d’envoi de frame.

L’événement OnConnected peut mettre à jour l’interface utilisateur, démarrer le rendu, et ainsi de suite. Dans notre exemple de code de bureau, nous mettons à jour le titre de la fenêtre avec un message «connecté».

```cpp
m_streamerHelpers->OnConnected += ref new ConnectedEvent(
           [this]()
           {
               UpdateWindowTitle();
           });
```

L’événement OnDisconnected peut gérer la reconnexion, les mises à jour de l’interface utilisateur, etc. Dans cet exemple, nous nous reconnectons en cas de défaillance temporaire.

```cpp
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

Lorsque le composant de communication à distance est prêt à envoyer un frame, votre application vous offre la possibilité d’en faire une copie dans le SendFrameEvent. Ici, nous copions le frame dans une chaîne de permutation afin que nous puissions l’afficher dans une fenêtre d’aperçu.

```cpp
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

### <a name="render-holographic-content"></a>Afficher le contenu holographique

Pour afficher le contenu à l’aide de la communication à distance, vous devez configurer un IFrameworkView virtuel dans votre application de bureau ou UWP et traiter des frames holographiques à partir de la communication à distance. Toutes les API Windows holographiques sont utilisées de la même façon par cette vue, mais elles sont configurées légèrement différemment.

Au lieu de les créer vous-même, les composants d’espace et de parole holographiques proviennent de votre classe HolographicRemotingHelpers:

```cpp
m_appView->Initialize(m_streamerHelpers->HolographicSpace, m_streamerHelpers->RemoteSpeech);
```

Au lieu d’utiliser une boucle de mise à jour à l’intérieur d’une méthode Run, vous fournissez des mises à jour de graduations à partir de la boucle principale de votre application de bureau ou UWP. Cela permet à votre application de bureau ou UWP de rester dans le contrôle du traitement des messages.

```cpp
void DesktopWindow::Tick()
   {
       auto lock = m_deviceLock.Lock();
       m_appView->Tick();

       // display preview, etc.
   }
```

La méthode Tick () de la vue de l’application holographique termine une itération de la boucle Update, Draw et present.

```cpp
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

La vue de mise à jour, le rendu et la boucle d’affichage des applications holographiques sont exactement les mêmes que lorsqu’elles s’exécutent sur HoloLens, sauf que vous avez accès à une quantité beaucoup plus importante de ressources système sur votre ordinateur de bureau. Vous pouvez restituer beaucoup plus de triangles, avoir plus de passes de dessin, faire plus de physique et utiliser des processus x64 pour charger le contenu qui nécessite plus de 2 Go de RAM.

### <a name="disconnect-and-end-the-remote-session"></a>Déconnecter et mettre fin à la session à distance

Pour se déconnecter: par exemple, quand l’utilisateur clique sur un bouton de l’interface utilisateur pour déconnecter-appeler Disconnect () sur HolographicStreamerHelpers, puis libérer l’objet.

```cpp
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

## <a name="get-the-remoting-player"></a>Procurez-vous le lecteur de communication à distance

Le lecteur Windows holographique Remoting est proposé dans le magasin d’applications Windows sous la forme d’un point de terminaison pour la connexion des applications hôtes à distance. Pour obtenir le lecteur Windows holographique Remoting, visitez le Windows App Store à partir de votre HoloLens, recherchez la communication à distance et téléchargez l’application. Le lecteur de communication à distance comprend une fonctionnalité permettant d’afficher les statistiques à l’écran, ce qui peut être utile lors du débogage des applications hôtes de communication à distance.

## <a name="notes-and-resources"></a>Remarques et ressources

La vue de l’application holographique a besoin d’un moyen de fournir à votre application l’appareil Direct3D, qui doit être utilisé pour initialiser l’espace holographique. Votre application doit utiliser ce périphérique Direct3D pour copier et afficher le frame d’aperçu.

```cpp
internal:
       const std::shared_ptr<DX::DeviceResources>& GetDeviceResources()
       {
           return m_deviceResources;
       }
```

**Exemple de code:** Un exemple complet de code de communication à distance holographique est disponible, qui comprend une vue d’application holographique compatible avec la communication à distance et les projets hôtes de communication à distance pour les ordinateurs de bureau Win32, UWP DirectX et UWP avec XAML. Pour l’utiliser, cliquez ici:
* [Exemple de code Windows holographique pour la communication à distance](https://github.com/Microsoft/HoloLensCompanionKit/)

**Remarque sur le débogage:** La bibliothèque de communication à distance holographique peut lever des exceptions de première chance. Ces exceptions peuvent être visibles dans les sessions de débogage, en fonction des paramètres d’exception de Visual Studio qui sont actifs à ce moment-là. Ces exceptions sont interceptées en interne par la bibliothèque de communication à distance holographique et peuvent être ignorées.
