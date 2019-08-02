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
# <a name="writing-a-custom-holographic-remoting-player-app"></a>Écriture d’une application de lecteur de communication à distance holographique personnalisée

>[!IMPORTANT]
>Ce document décrit la création d’une application de lecteur personnalisée pour HoloLens 2. Les lecteurs personnalisés écrits pour HoloLens 2 ne sont pas compatibles avec les applications hôtes écrites pour HoloLens 1. Cela implique que les deux applications doivent utiliser le package NuGet version **2. x. x**.

En créant une application de lecteur de communication à distance holographique personnalisée, vous pouvez créer une application personnalisée capable d’afficher des [vues immersives](app-views.md) à partir d’un ordinateur distant sur votre HoloLens 2. Cet article explique comment procéder. Tout le code de cette page et des projets de travail se trouve dans le [référentiel GitHub d’exemples de communication à distance holographique](https://github.com/microsoft/MixedReality-HolographicRemoting-Samples).

Un lecteur de communication à distance holographique permet à votre application d’afficher le contenu holographique [rendu](rendering.md) sur un PC de bureau ou sur un appareil UWP tel que le Xbox, permettant d’accéder à davantage de ressources système. Une application de lecteur de communication à distance holographique diffuse des données d’entrée vers une application hôte de communication à distance holographique et reçoit un affichage immersif en tant que flux vidéo et audio. La connexion est établie à l’aide du Wi-Fi standard. Pour créer une application de lecteur, vous allez utiliser un package NuGet pour ajouter la communication à distance holographique à votre application UWP, puis écrire du code pour gérer la connexion et afficher une vue immersive. 

## <a name="prerequisites"></a>Prérequis

Un bon point de départ est une application UWP DirectX fonctionnelle qui cible déjà l’API Windows Mixed Reality. Pour plus d’informations, consultez [vue d’ensemble du développement DirectX](directx-development-overview.md). Si vous ne disposez pas d’une application existante et que vous souhaitez commencer à partir de zéro, le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md) est un bon point de départ.

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

>[!IMPORTANT]
><a name="idl"></a>L' ```build\native\include\HolographicAppRemoting\Microsoft.Holographic.AppRemoting.idl``` intérieur du package NuGet contient une documentation détaillée sur l’API exposée par la communication à distance holographique.

## <a name="modify-the-packageappxmanifest-of-the-application"></a>Modifier le package. appxmanifest de l’application

Pour que l’application prenne en charge le fichier Microsoft. holographique. AppRemoting. dll ajouté par le package NuGet, les étapes suivantes doivent être effectuées sur le projet:

1. Dans le Explorateur de solutions cliquez avec le bouton droit sur le fichier **Package. appxmanifest** , puis sélectionnez **Ouvrir avec...**
2. Sélectionnez **éditeur XML (texte)** , puis cliquez sur OK.
3. Ajoutez les lignes suivantes au fichier et enregistrez
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
## <a name="create-the-player-context"></a>Créer le contexte du joueur

En guise de première étape, l’application doit créer un contexte de joueur.

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
>La communication à distance holographique fonctionne en remplaçant le runtime Windows Mixed Reality qui fait partie de Windows par un Runtime spécifique à distance. Cette opération est effectuée lors de la création du contexte du joueur. Pour cette raison, tout appel sur une API de réalité mixte Windows avant de créer le contexte du joueur peut entraîner un comportement inattendu. L’approche recommandée consiste à créer le contexte du joueur le plus tôt possible avant d’interagir avec une API de réalité mixte. Ne combinez jamais des objets créés ou récupérés par le biais d’une API ```PlayerContext::Create()``` Windows Mixed Reality avant l’appel à avec des objets créés ou récupérés par la suite.

Ensuite, vous pouvez créer le HolographicSpace en appelant [HolographicSpace. CreateForCoreWindow](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicspace.createforcorewindow).

```cpp
m_holographicSpace = winrt::Windows::Graphics::Holographic::HolographicSpace::CreateForCoreWindow(window);
```

## <a name="connect-to-the-host"></a>Se connecter à l’hôte

Une fois que l’application de lecteur est prête pour le rendu du contenu, une connexion à l’hôte peut être établie.

La connexion peut être établie de l’une des manières suivantes:
1) L’application de lecteur s’exécutant sur HoloLens 2 se connecte à l’application hôte.
2) L’application hôte se connecte à l’application de lecteur s’exécutant sur HoloLens 2.

Pour vous connecter à partir de l’application du lecteur à ```Connect``` l’hôte, appelez la méthode sur le contexte du joueur spécifiant le nom d’hôte et le port. Le port par défaut est **8265**.

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
>Comme avec toute C++API ```Connect``` /WinRT peut lever une exception WinRT:: hresult_error qui doit être gérée.

L’écoute des connexions entrantes sur l’application de lecteur peut être effectuée ```Listen``` en appelant la méthode. Le port de liaison et le port de transport peuvent être spécifiés au cours de cet appel. Le port de négociation est utilisé pour le protocole de transfert initial. Les données sont ensuite envoyées sur le port de transport. Les numéros de port **8265** et **8266** sont utilisés par défaut.

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


## <a name="handling-connection-related-events"></a>Gestion des événements liés à la connexion

Le ```PlayerContext``` expose trois événements pour surveiller l’état de la connexion.
1) OnConnected: Déclenché lorsqu’une connexion à l’hôte a été établie avec succès.
```cpp
m_onConnectedEventToken = m_playerContext.OnConnected([]() 
{
    // Handle connection successfully established
});
```
2) OnDisconnected: Déclenché si une connexion établie est terminée ou si une connexion n’a pas pu être établie.
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
>Les ```ConnectionFailureReason``` valeurs possibles sont documentées ```Microsoft.Holographic.AppRemoting.idl``` dans le [fichier](#idl).

3) OnListening: Lors du démarrage de l’écoute des connexions entrantes.
```cpp
m_onListeningEventToken = m_playerContext.OnListening([]()
{
    // Handle start listening for incoming connections
});
```

En outre, l’état de la connexion peut être interrogé ```ConnectionState``` à l’aide de la propriété du contexte du lecteur.
```cpp
winrt::Microsoft::Holographic::AppRemoting::ConnectionState state = m_playerContext.ConnectionState();
```

## <a name="display-the-remotely-rendered-frame"></a>Afficher le frame rendu à distance

Pour afficher le contenu rendu à distance, appelez ```PlayerContext::BlitRemoteFrame()``` lors du rendu d’un [HolographicFrame](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe). 

```BlitRemoteFrame()```requiert que la mémoire tampon d’arrière-plan pour le HolographicFrame actuel soit liée en tant que cible de rendu. La mémoire tampon d’arrière-plan peut être reçue à partir du [HolographicCameraRenderingParameters](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe.getrenderingparameters) via la propriété [Direct3D11BackBuffer](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.direct3d11backbuffer) .

En cas d' ```BlitRemoteFrame()``` appel, copie la dernière trame reçue à partir de l’application hôte dans la mémoire tampon de l’HolographicFrame. En outre, l’ensemble de points de focalisation est défini, si l’application distante a spécifié un point de focus pendant le rendu du frame distant.

```cpp
// Blit the remote frame into the backbuffer for the HolographicFrame.
winrt::Microsoft::Holographic::AppRemoting::BlitResult result = m_playerContext.BlitRemoteFrame();
```

>[!NOTE]
>```PlayerContext::BlitRemoteFrame()```remplace potentiellement le point de focus du frame actuel. 
>- Pour spécifier un point de focus de secours, appelez [HolographicCameraRenderingParameters:: SetFocusPoint](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.setfocuspoint) avant ```PlayerContext::BlitRemoteFrame()```. 
>- Pour overrwrite le point de focus distant, appelez [HolographicCameraRenderingParameters:: SetFocusPoint](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.setfocuspoint) après ```PlayerContext::BlitRemoteFrame()```.

En cas de ```BlitRemoteFrame()``` réussite ```BlitResult::Success_Color```, retourne. Dans le cas contraire, elle retourne la raison de l’échec:
- ```BlitResult::Failed_NoRemoteFrameAvailable```: Échec, car aucun frame distant n’est disponible.
- ```BlitResult::Failed_NoCamera```: A échoué, car aucun appareil photo n’est présent.

## <a name="optional-get-statistics-about-the-last-remote-frame"></a>Facultatif : Obtenir des statistiques sur le dernier frame distant

Pour diagnostiquer les problèmes de performances ou de réseau, les statistiques relatives au dernier frame distant peuvent ```PlayerContext::LastFrameStatistics``` être récupérées via la propriété. Les statistiques sont mises à jour lors de l’appel à [HolographicFrame::P resentusingcurrentprediction](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe.presentusingcurrentprediction).

```cpp
// Get statistics for the last presented frame.
winrt::Microsoft::Holographic::AppRemoting::PlayerFrameStatistics statistics = m_playerContext.LastFrameStatistics();
```

Pour plus d’informations, consultez ```PlayerFrameStatistics``` la documentation ```Microsoft.Holographic.AppRemoting.idl``` du [fichier](#idl).

## <a name="optional-custom-data-channels"></a>Facultatif : Canaux de données personnalisés

Les canaux de données personnalisés peuvent être utilisés pour envoyer des données utilisateur sur la connexion de communication à distance déjà établie. Pour plus d’informations, consultez [canaux de données personnalisés](holographic-remoting-custom-data-channels.md) .

## <a name="see-also"></a>Voir aussi
* [Écriture d’une application hôte de communication à distance holographique](holographic-remoting-create-host.md)
* [Canaux de données de communication à distance holographiques personnalisés](holographic-remoting-custom-data-channels.md)
* [Établissement d’une connexion sécurisée à l’aide de la communication à distance holographique](holographic-remoting-secure-connection.md)
* [Résolution des problèmes et limitations de la communication à distance holographique](holographic-remoting-troubleshooting.md)
* [Termes du contrat de licence du logiciel de communication à distance holographique](https://docs.microsoft.com/en-us/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [Déclaration de confidentialité Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)