---
title: Écriture d’une application hôte de communication à distance holographique
description: En créant un contenu distant d’application hôte de communication à distance holographique, qui est affiché sur un ordinateur distant, peut être diffusé en continu vers HoloLens 2. Cet article explique comment procéder.
author: bethau
ms.author: bethau
ms.date: 08/01/2019
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: 6b0f92fce1099ec98d87100e015de9442bff6bd2
ms.sourcegitcommit: ff330a7e36e5ff7ae0e9a08c0e99eb7f3f81361f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70122022"
---
# <a name="writing-a-holographic-remoting-host-app"></a>Écriture d’une application hôte de communication à distance holographique

>[!IMPORTANT]
>Ce document décrit la création d’une application hôte pour HoloLens 2. L’application hôte pour **HoloLens (1re génération)** doit utiliser le package NuGet version **1. x. x**. Cela implique que les applications hôtes écrites pour HoloLens 2 ne sont pas compatibles avec HoloLens 1 et vice versa. La documentation de HoloLens 1 est disponible [ici](add-holographic-remoting.md).

En créant une application hôte de communication à distance holographique, le contenu distant rendu sur une machine distante peut être transmis à HoloLens 2. Cet article explique comment procéder. Tout le code de cette page et des projets de travail se trouve dans le [référentiel GitHub d’exemples de communication à distance holographique](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples).

La communication à distance holographique permet à une application de cibler HoloLens 2 avec un contenu holographique hébergé sur un PC de bureau ou sur un appareil UWP comme la Xbox One, permettant d’accéder à davantage de ressources système et d’intégrer des [vues immersives](app-views.md) distantes dans les logiciels des PC de bureau existants. Une application hôte de communication à distance reçoit un flux de données d’entrée de HoloLens 2, restitue le contenu dans une vue immersive virtuelle et diffuse en continu des frames de contenu vers HoloLens 2. La connexion est établie à l’aide du Wi-Fi standard. La communication à distance holographique est ajoutée à une application de bureau ou UWP via un paquet NuGet. Du code supplémentaire est nécessaire pour gérer la connexion et le rendu dans une vue immersive.

Une connexion à distance classique aura une latence aussi faible que 50 ms de latence. L’application de lecteur peut signaler la latence en temps réel.

## <a name="prerequisites"></a>Prérequis

Un bon point de départ est un bureau DirectX opérationnel ou une application UWP qui cible l’API Windows Mixed Reality. Pour plus d’informations, consultez [vue d’ensemble du développement DirectX](directx-development-overview.md). Le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md) est un bon point de départ.

>[!IMPORTANT]
>Toute application utilisant la communication à distance holographique doit être créée pour utiliser un [cloisonnement](https://docs.microsoft.com/en-us/windows/win32/com/multithreaded-apartments)multithread. L’utilisation d’un [cloisonnement à thread unique](https://docs.microsoft.com/en-us/windows/win32/com/single-threaded-apartments) est prise en charge, mais entraîne des performances non optimales et éventuellement des interruptions pendant la lecture. Lors de C++l’utilisation de/WinRT [WinRT:: init_apartment](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/get-started) , un cloisonnement multithread est la valeur par défaut.



## <a name="get-the-holographic-remoting-nuget-package"></a>Procurez-vous le package NuGet de communication à distance holographique

Les étapes suivantes sont requises pour ajouter le package NuGet à un projet dans Visual Studio.
1. Ouvrez le projet dans Visual Studio.
2. Cliquez avec le bouton droit sur le nœud du projet et sélectionnez **gérer les packages NuGet...**
3. Dans le volet qui s’affiche, cliquez sur **Parcourir** , puis recherchez «accès distant holographique».
4. Sélectionnez **Microsoft. holographique. Remoting**, assurez-vous de choisir la version la plus récente de **2. x. x** , puis cliquez sur **installer**.
5. Si la boîte de dialogue **Aperçu** s’affiche, cliquez sur **OK**.
6. La boîte de dialogue suivante qui s’affiche est le contrat de licence. Cliquez sur **J’accepte** pour accepter le contrat de licence.

>[!NOTE]
>La version **1. x. x** du package NuGet est toujours disponible pour les développeurs qui souhaitent cibler HoloLens 1. Pour plus d’informations [, consultez Ajouter une communication à distance holographique (HoloLens (1re génération))](add-holographic-remoting.md).

## <a name="create-the-remote-context"></a>Créer le contexte distant

En guise de première étape, l’application doit créer un contexte distant.

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
>La communication à distance holographique fonctionne en remplaçant le runtime Windows Mixed Reality qui fait partie de Windows par un Runtime spécifique à distance. Cette opération est effectuée lors de la création du contexte distant. Pour cette raison, tout appel sur une API de réalité mixte Windows avant de créer le contexte distant peut entraîner un comportement inattendu. L’approche recommandée consiste à créer le contexte distant le plus tôt possible avant d’interagir avec une API de réalité mixte. Ne combinez jamais des objets créés ou récupérés par le biais d’une API Windows Mixed Reality avant l’appel à CreateRemoteContext avec des objets créés ou récupérés par la suite.

L’espace holographique doit ensuite être créé. La spécification d’un CoreWindow n’est pas obligatoire. Les applications de bureau qui n’ont pas de CoreWindow peuvent simplement ```nullptr```passer un.

```cpp
m_holographicSpace = winrt::Windows::Graphics::Holographic::HolographicSpace::CreateForCoreWindow(nullptr);
```

## <a name="connect-to-the-device"></a>Se connecter à l’appareil

Une fois que l’application hôte est prête pour le rendu du contenu, une connexion à l’appareil peut être établie.

La connexion peut être effectuée de deux manières.
1) L’application hôte se connecte au lecteur qui s’exécute sur l’appareil.
2) Le lecteur s’exécutant sur l’appareil se connecte à l’application hôte.

Pour établir une connexion à partir de l’application hôte à HoloLens 2 ```Connect``` , appelez la méthode sur le contexte distant en spécifiant le nom d’hôte et le port. Le port utilisé par le lecteur de communication à distance holographique est **8265**.

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
>Comme avec toute C++API ```Connect``` /WinRT peut lever une exception WinRT:: hresult_error qui doit être gérée.

>[!TIP]
>Pour éviter d' [ C++](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/) utiliser la projection du langage ```build\native\include\<windows sdk version>\abi\Microsoft.Holographic.AppRemoting.h``` /WinRT, le fichier situé dans le package NuGet de communication à distance holographique peut être inclus. Il contient les déclarations des interfaces COM sous-jacentes. L’utilisation de C++/WinRT est toutefois recommandée.

L’écoute des connexions entrantes sur l’application hôte peut être effectuée en ```Listen``` appelant la méthode. Le port de liaison et le port de transport peuvent être spécifiés au cours de cet appel. Le port de négociation est utilisé pour le protocole de transfert initial. Les données sont ensuite envoyées sur le port de transport. Par défaut, **8265** et **8266** sont utilisés.

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
>L' ```build\native\include\HolographicAppRemoting\Microsoft.Holographic.AppRemoting.idl``` intérieur du package NuGet contient une documentation détaillée sur l’API exposée par la communication à distance holographique.

## <a name="handling-remoting-specific-events"></a>Gestion des événements de communication à distance spécifiques

Le contexte distant expose trois événements qui sont importants pour surveiller l’état d’une connexion.
1) OnConnected: Déclenché lorsqu’une connexion à l’appareil a été établie avec succès.
```cpp
winrt::weak_ref<winrt::Microsoft::Holographic::AppRemoting::IRemoteContext> remoteContextWeakRef = m_remoteContext;

m_onConnectedEventRevoker = m_remoteContext.OnConnected(winrt::auto_revoke, [this, remoteContextWeakRef]() {
    if (auto remoteContext = remoteContextWeakRef.get())
    {
        // Update UI state
    }
});
```
2) OnDisconnected: Déclenché si une connexion établie est fermée ou si une connexion n’a pas pu être établie.
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
3) OnListening: Lors du démarrage de l’écoute des connexions entrantes.
```cpp
m_onListeningEventRevoker = m_remoteContext.OnListening(winrt::auto_revoke, [this, remoteContextWeakRef]() {
    if (auto remoteContext = remoteContextWeakRef.get())
    {
        // Update UI state
    }
});
```

En outre, l’état de la connexion peut être interrogé ```ConnectionState``` à l’aide de la propriété sur le contexte distant.
```cpp
auto connectionState = m_remoteContext.ConnectionState();
```

## <a name="handling-speech-events"></a>Gestion des événements vocaux

À l’aide de l’interface de reconnaissance vocale à distance, il est possible d’inscrire les déclencheurs vocaux avec HoloLens 2 et de les faire distants à l’application hôte.

Ce membre supplémentaire est requis pour effectuer le suivi de l’état de la voix à distance.

```cpp
winrt::Microsoft::Holographic::AppRemoting::IRemoteSpeech::OnRecognizedSpeech_revoker m_onRecognizedSpeechRevoker;

```

Tout d’abord, l’interface de reconnaissance vocale à distance doit être récupérée.

```cpp
if (auto remoteSpeech = m_remoteContext.GetRemoteSpeech())
{
    InitializeSpeechAsync(remoteSpeech, m_onRecognizedSpeechRevoker, weak_from_this());
}
```

À l’aide d’une méthode d’assistance asynchrone, vous pouvez initialiser la reconnaissance vocale à distance. Cette opération doit être effectuée de façon asynchrone, car l’initialisation peut prendre beaucoup de temps. [Opérations d’accès concurrentiel C++et asynchrones avec/WinRT](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/concurrency) explique comment créer des fonctions asynchrones avec/WinRT. C++

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

Il existe deux façons de spécifier des expressions à reconnaître.
1) Spécification à l’intérieur d’un fichier XML de grammaire vocale. Pour plus d’informations, consultez [comment créer une grammaire XML de base](https://docs.microsoft.com/en-us/previous-versions/office/developer/speech-technologies/hh361658(v=office.14)) .
2) Spécifiez en les passant dans le vecteur du ```ApplyParameters```dictionnaire à.

Dans le rappel OnRecognizedSpeech, les événements vocaux peuvent ensuite être traités:

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

## <a name="preview-streamed-content-locally"></a>Afficher un aperçu du contenu diffusé en continu localement

Pour afficher le même contenu dans l’application hôte qui est envoyé à l’appareil, ```OnSendFrame``` l’événement du contexte distant peut être utilisé. L' ```OnSendFrame``` événement est déclenché chaque fois que la bibliothèque de communication à distance holographique envoie le frame actuel au périphérique distant. C’est le moment idéal pour prendre le contenu et le configurer dans la fenêtre du bureau ou UWP.

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

## <a name="optional-custom-data-channels"></a>Facultatif : Canaux de données personnalisés

Les canaux de données personnalisés peuvent être utilisés pour envoyer des données utilisateur sur la connexion de communication à distance déjà établie. Pour plus d’informations, consultez [canaux de données personnalisés](holographic-remoting-custom-data-channels.md) .

## <a name="see-also"></a>Voir aussi
* [Écriture d’une application de lecteur de communication à distance holographique personnalisée](holographic-remoting-create-player.md)
* [Canaux de données de communication à distance holographique personnalisés](holographic-remoting-custom-data-channels.md)
* [Établissement d’une connexion sécurisée à l’aide de la communication à distance holographique](holographic-remoting-secure-connection.md)
* [Résolution des problèmes et limitations de la communication à distance holographique](holographic-remoting-troubleshooting.md)
* [Termes du contrat de licence de la communication à distance holographique](https://docs.microsoft.com/en-us/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [Déclaration de confidentialité Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
