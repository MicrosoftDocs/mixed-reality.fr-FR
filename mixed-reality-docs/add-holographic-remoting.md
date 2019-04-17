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
# <a name="add-holographic-remoting"></a>Ajouter la communication à distance HOLOGRAPHIQUE

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).

## <a name="add-holographic-remoting-to-your-desktop-or-uwp-app"></a>Ajouter HOLOGRAPHIQUE communication à distance à votre bureau ou d’une application UWP

Cette page décrit comment ajouter holographique de communication à distance à un bureau ou une application UWP.

Communication à distance HOLOGRAPHIQUE permet à votre application cibler un HoloLens avec HOLOGRAPHIQUE contenu hébergé sur un PC de bureau ou sur un appareil UWP tels que Xbox One, autorisant l’accès à davantage de ressources système et rend possible d’intégrer à distance [immersives vues](app-views.md) dans les logiciels de PC de bureau existante. Une application hôte de communication à distance reçoit un flux de données d’entrée à partir d’un HoloLens, restitue le contenu dans un affichage virtuel immersif et diffuse les images du contenu vers HoloLens. La connexion est établie à l’aide de Wi-Fi standard. Pour utiliser la communication à distance, vous utilise un package NuGet pour ajouter HOLOGRAPHIQUE communication à distance à votre bureau ou d’une application UWP et écrire du code pour gérer la connexion et s’affichent dans une vue immersive. Bibliothèques d’assistance sont inclus dans l’exemple de code qui simplifient la tâche de gestion de la connexion de l’appareil.

Une connexion de communication à distance classique aura aussi faible que la latence de 50 ms. L’application de lecteur peut signaler la latence en temps réel.

>[!NOTE]
>Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).  Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.

### <a name="get-the-remoting-nuget-packages"></a>Obtenir la communication à distance les packages NuGet

Suivez ces étapes pour obtenir le package NuGet pour la communication à distance holographique et ajoutez une référence à partir de votre projet :
1. Accédez à votre projet dans Visual Studio.
2. Avec le bouton droit sur le nœud du projet et sélectionnez **gérer les Packages NuGet...**
3. Dans le panneau qui s’affiche, cliquez sur **Parcourir** , puis recherchez « HOLOGRAPHIQUE communication à distance ».
4. Sélectionnez **Microsoft.Holographic.Remoting** et cliquez sur **installer**.
5. Si le **aperçu** boîte de dialogue s’affiche, cliquez sur **OK**.
6. La boîte de dialogue suivante qui s’affiche est le contrat de licence. Cliquez sur **J’accepte** pour accepter le contrat de licence.

### <a name="create-the-holographicstreamerhelpers"></a>Créer le HolographicStreamerHelpers

Tout d’abord, nous avons besoin d’une instance de HolographicStreamerHelpers. Ajouter à la classe qui se chargera de communication à distance.

```
#include <HolographicStreamerHelpers.h>

   private:
       Microsoft::Holographic::HolographicStreamerHelpers^ m_streamerHelpers;
```

Vous devez également suivre l’état de la connexion. Si vous souhaitez afficher l’aperçu, vous devez avoir une texture à copier. Également, vous avez besoin de quelques choses comme un verrou d’état de connexion, un moyen de stocker l’adresse IP de HoloLens et ainsi de suite.

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

### <a name="initialize-holographicstreamerhelpers-and-connect-to-hololens"></a>Initialiser HolographicStreamerHelpers et se connecter à HoloLens

Pour vous connecter à un appareil HoloLens, créez une instance de HolographicStreamerHelpers et connectez-vous à l’adresse IP cible. Vous devez définir la taille de trame vidéo pour correspondre à la largeur d’affichage HoloLens et la hauteur, étant donné que la bibliothèque de communication à distance HOLOGRAPHIQUE attend les résolutions d’encodeur et décodeur correspondre exactement.

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

La connexion de l’appareil est asynchrone. Votre application a besoin pour fournir des gestionnaires d’événements pour se connecter, vous déconnecter et envoyer des événements par frame.

L’événement OnConnected peut mettre à jour de l’interface utilisateur, démarrage du rendu et ainsi de suite. Dans notre exemple de code Windows desktop, nous mettre à jour le titre de la fenêtre avec un message « connecté ».

```
m_streamerHelpers->OnConnected += ref new ConnectedEvent(
           [this]()
           {
               UpdateWindowTitle();
           });
```

L’événement OnDisconnected peut gérer la reconnexion, mises à jour de l’interface utilisateur et ainsi de suite. Dans cet exemple, nous vous reconnecter en cas de panne temporaire.

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

Lorsque le composant de communication à distance est prêt à envoyer une image, votre application est fournie une occasion de faire une copie de celle-ci dans le SendFrameEvent. Ici, nous copions le frame dans une chaîne de permutation afin que nous pouvons l’afficher dans une fenêtre d’aperçu.

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

### <a name="render-holographic-content"></a>Afficher le contenu HOLOGRAPHIQUE

Pour afficher le contenu à l’aide de la communication à distance, vous définissez un IFrameworkView virtuel au sein de votre bureau ou d’une application UWP et traiter les trames HOLOGRAPHIQUE à partir de la communication à distance. Toutes les API Windows HOLOGRAPHIQUE sont utilise que la même façon par cette vue, mais il est configurée de manière légèrement différente.

Au lieu de les créer vous-même, les composants d’espace et de reconnaissance vocale HOLOGRAPHIQUE proviennent de votre classe HolographicRemotingHelpers :

```
m_appView->Initialize(m_streamerHelpers->HolographicSpace, m_streamerHelpers->RemoteSpeech);
```

Au lieu d’utiliser une boucle de mise à jour à l’intérieur d’une méthode d’exécution, vous fournissez des mises à jour de la graduation à partir de la boucle principale de votre bureau ou d’une application UWP. Cela permet à votre bureau ou une application UWP de rester dans le contrôle du traitement du message.

```
void DesktopWindow::Tick()
   {
       auto lock = m_deviceLock.Lock();
       m_appView->Tick();

       // display preview, etc.
   }
```

Méthode de Tick() de la vue HOLOGRAPHIQUE application termine une itération de la mise à jour, le dessin, la boucle présente.

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

La mise à jour de la vue HOLOGRAPHIQUE application, le rendu et la boucle présente est exactement le même comme c’est lors de l’exécution sur HoloLens -, à ceci près que vous avez accès à une plus grande capacité de ressources système sur votre ordinateur de bureau. Vous pouvez effectuer le rendu des triangles plus nombreux, ont plusieurs passes de dessins, faire plus physique et utilisent x64 des processus de chargement du contenu qui nécessite plus de 2 Go de RAM.

### <a name="disconnect-and-end-the-remote-session"></a>Se déconnecter et fermer la session à distance

Pour déconnecter - par exemple, lorsque l’utilisateur clique sur un bouton de l’interface utilisateur pour se déconnecter - appeler Disconnect() sur le HolographicStreamerHelpers et libérer l’objet.

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

## <a name="get-the-remoting-player"></a>Obtenir le lecteur de communication à distance

Le joueur de communication à distance Windows holographique est disponible dans le magasin d’applications Windows en tant que point de terminaison pour héberger des applications de communication à distance pour se connecter à. Pour obtenir le lecteur de communication à distance Windows HOLOGRAPHIQUE, visitez le magasin d’applications Windows à partir de votre HoloLens, recherchez la communication à distance et télécharger l’application. Le lecteur de communication à distance comprend une fonctionnalité permettant d’afficher des statistiques à l’écran, ce qui peut être utile lors du débogage d’héberger des applications de communication à distance.

## <a name="notes-and-resources"></a>Notes de publication et ressources

La vue HOLOGRAPHIQUE application devez un moyen de fournir votre application avec le périphérique Direct3D, qui doit être utilisé pour initialiser l’espace HOLOGRAPHIQUE. Votre application doit utiliser ce périphérique Direct3D pour copier et afficher le frame de la version préliminaire.

```
internal:
       const std::shared_ptr<DX::DeviceResources>& GetDeviceResources()
       {
           return m_deviceResources;
       }
```

**Exemple de code :** Un exemple de code complet Remoting holographique est disponible, ce qui inclut une vue HOLOGRAPHIQUE application qui est compatible avec la communication à distance et les projets d’hôte de communication à distance pour le bureau Win32 UWP DirectX et UWP avec XAML. Pour l’obtenir, cliquez ici :
* [Exemple de Code holographique de Windows pour l’accès distant](https://github.com/Microsoft/HoloLensCompanionKit/)

**Remarque de débogage :** La bibliothèque de communication à distance HOLOGRAPHIQUE peut lever des exceptions de première chance. Ces exceptions peuvent être visibles dans les sessions de débogage, selon les paramètres d’exception de Visual Studio qui sont actives à la fois. Ces exceptions sont interceptées en interne par la bibliothèque de communication à distance holographique et peuvent être ignorées.
