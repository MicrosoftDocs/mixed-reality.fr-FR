---
title: Transferts d’ancrage local dans DirectX
description: Explique comment synchroniser deux appareils HoloLens en transférant les ancres spatiales.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, synchroniser, ancre spatiale, transfert, mode multijoueur, afficher, scénario, procédure pas à pas, exemple de code, transfert, transfert de local d’ancrage, exportation de point d’ancrage, importation de point d’ancrage
ms.openlocfilehash: 5d03f4bfa764b9948ec4718bce86127cfcc3e303
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597112"
---
# <a name="local-anchor-transfers-in-directx"></a>Transferts d’ancrage local dans DirectX

Dans les situations où vous ne pouvez pas utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres Spatial Azure</a>, les transferts d’ancrage local activer un appareil HoloLens exporter un point d’ancrage doivent être importées par un deuxième appareil HoloLens.

>[!NOTE]
>Les transferts d’ancrage local fournissent moins fiable rappel d’ancrage que <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres Spatial Azure</a>, et les appareils iOS et Android ne sont pas pris en charge par cette approche.

>[!NOTE]
>Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).  Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.

## <a name="transferring-spatial-anchors"></a>Transfert des ancres spatiales

Vous pouvez transférer des ancres spatiales entre les appareils de réalité mixte Windows à l’aide de la [SpatialAnchorTransferManager](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchortransfermanager.aspx). Cette API vous permet de regrouper un point d’ancrage avec toutes les données de capteur de prise en charge nécessaires pour rechercher cet emplacement exact dans le monde et ensuite importer cette offre groupée sur un autre appareil. Une fois que l’application sur le deuxième a importé ce point d’ancrage, chaque application peut rendre hologrammes à l’aide qui partagé du système de coordonnées spatiales de l’ancre, qui apparaîtra au même endroit dans le monde réel.

Notez que les ancres spatiales ne sont pas en mesure de transférer entre différents types d’appareil, par exemple un point d’ancrage spatial HoloLens est peut-être pas localisable à l’aide d’un casque immersif.  Également les ancres transférées ne sont pas compatibles avec les appareils iOS ou Android.

## <a name="set-up-your-app-to-use-the-spatialperception-capability"></a>Configurer votre application pour utiliser la fonctionnalité spatialPerception

Votre application doit être autorisée à utiliser la fonctionnalité de spatialPerception avant qu’il puisse utiliser le [SpatialAnchorTransferManager](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchortransfermanager.aspx). Cela est nécessaire, car transfert d’un point d’ancrage spatial concerne le partage des images de capteur collectées au fil du temps à proximité de ce point d’ancrage, ce qui peut inclure des informations sensibles.

Déclarez cette fonctionnalité dans le fichier package.appxmanifest pour votre application. Voici un exemple :

```
<Capabilities>
  <uap2:Capability Name="spatialPerception" />
</Capabilities>
```

La fonctionnalité provient de la **uap2** espace de noms. Pour accéder à cet espace de noms dans votre manifeste, inclure un *xlmns* d’attribut dans le &lt;Package > élément. Voici un exemple :

```
<Package
    xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
    xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
    xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
    xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2"
    IgnorableNamespaces="uap mp"
    >
```

**REMARQUE :** Votre application a besoin demander la fonctionnalité au runtime qu’il puisse accéder SpatialAnchor exportation/importation API. Consultez [RequestAccessAsync](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchortransfermanager.requestaccessasync.aspx) dans les exemples ci-dessous.

## <a name="serialize-anchor-data-by-exporting-it-with-the-spatialanchortransfermanager"></a>Sérialiser les données de point d’ancrage en les exportant avec la SpatialAnchorTransferManager

Une fonction d’assistance est incluse dans l’exemple de code pour exporter (sérialiser) [SpatialAnchor](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) données. Cette API d’exportation sérialise tous les points d’ancrage dans une collection de paires clé-valeur associant des chaînes avec des points d’ancrage.

```
// ExportAnchorDataAsync: Exports a byte buffer containing all of the anchors in the given collection.
//
// This function will place data in a buffer using a std::vector<byte>. The ata buffer contains one or more
// Anchors if one or more Anchors were successfully imported; otherwise, it is ot modified.
//
task<bool> SpatialAnchorImportExportHelper::ExportAnchorDataAsync(
    vector<byte>* anchorByteDataOut,
    IMap<String^, SpatialAnchor^>^ anchorsToExport
    )
{
```

Tout d’abord, nous devons configurer le flux de données. Cela nous permettra à 1.) Utilisez TryExportAnchorsAsync pour placer les données dans une mémoire tampon détenue par l’application et 2). lire les données à partir du flux de mémoire tampon d’octets exporté, qui est un flux de données WinRT - dans notre propre mémoire tampon, qui est un std::vector&lt;octets >.

```
// Create a random access stream to process the anchor byte data.
InMemoryRandomAccessStream^ stream = ref new InMemoryRandomAccessStream();
// Get an output stream for the anchor byte stream.
IOutputStream^ outputStream = stream->GetOutputStreamAt(0);
```

Nous avons besoin de demander l’autorisation d’accéder aux données spatiales, y compris les points d’ancrage qui sont exportés par le système.

```
// Request access to spatial data.
auto accessRequestedTask = create_taskSpatialAnchorTransferManager::RequestAccessAsync()).then([anchorsToExport, utputStream](SpatialPerceptionAccessStatus status)
{
    if (status == SpatialPerceptionAccessStatus::Allowed)
    {
        // Access is allowed.
        // Export the indicated set of anchors.
        return create_task(SpatialAnchorTransferManager::TryExportAnchorsAsync(
            anchorsToExport,
            outputStream
            ));
    }
    else
    {
        // Access is denied.
        return task_from_result<bool>(false);
    }
});
```

Si nous obtenons bien autorisation et points d’ancrage sont exportés, nous pouvons lire le flux de données. Ici, nous montrons également comment créer le DataReader et InputStream, nous allons utiliser pour lire les données.

```
// Get the input stream for the anchor byte stream.
IInputStream^ inputStream = stream->GetInputStreamAt(0);
// Create a DataReader, to get bytes from the anchor byte stream.
DataReader^ reader = ref new DataReader(inputStream);
return accessRequestedTask.then([anchorByteDataOut, stream, reader](bool nchorsExported)
{
    if (anchorsExported)
    {
        // Get the size of the exported anchor byte stream.
        size_t bufferSize = static_cast<size_t>(stream->Size);
        // Resize the output buffer to accept the data from the stream.
        anchorByteDataOut->reserve(bufferSize);
        anchorByteDataOut->resize(bufferSize);
        // Read the exported anchor store into the stream.
        return create_task(reader->LoadAsync(bufferSize));
    }
    else
    {
        return task_from_result<size_t>(0);
    }
```

Une fois que nous lire les octets à partir du flux, nous pouvons les enregistrer dans notre propre mémoire tampon de données comme suit.

```
}).then([anchorByteDataOut, reader](size_t bytesRead)
{
    if (bytesRead > 0)
    {
        // Read the bytes from the stream, into our data output buffer.
        reader->ReadBytes(Platform::ArrayReference<byte>(&(*anchorByteDataOut)[0], bytesRead));
        return true;
    }
    else
    {
        return false;
    }
});
};
```

## <a name="deserialize-anchor-data-by-importing-it-into-the-system-using-the-spatialanchortransfermanager"></a>Désérialiser des données de point d’ancrage en l’important dans le système à l’aide de la SpatialAnchorTransferManager

Une fonction d’assistance est incluse dans l’exemple de code pour charger des données précédemment exportées. Cette fonction de la désérialisation fournit une collection de paires clé-valeur, similaires à ce que fournit le SpatialAnchorStore -, à ceci près que nous avons ces données à partir d’une autre source, comme un socket réseau. Vous pouvez traiter et analyser ces données avant de les stocker en mémoire dans l’application en mode hors connexion, à l’aide, ou (le cas échéant) SpatialAnchorStore de votre application.

```
// ImportAnchorDataAsync: Imports anchors from a byte buffer that was previously exported.
//
// This function will import all anchors from a data buffer into an in-memory ollection of key, value
// pairs that maps String objects to SpatialAnchor objects. The Spatial nchorStore is not affected by
// this function unless you provide it as the target collection for import.
//
task<bool> SpatialAnchorImportExportHelper::ImportAnchorDataAsync(
    std::vector<byte>& anchorByteDataIn,
    IMap<String^, SpatialAnchor^>^ anchorMapOut
    )
{
```

Tout d’abord, nous devons créer des objets de flux de données pour accéder aux données d’ancrage. Nous doit écrire les données à partir de notre mémoire tampon dans une mémoire tampon du système, donc nous allons créer un DataWriter qui écrit dans un flux de données en mémoire afin d’atteindre notre objectif de l’obtention des points d’ancrage à partir d’une mémoire tampon d’octets dans le système en tant que SpatialAnchors.

```
// Create a random access stream for the anchor data.
InMemoryRandomAccessStream^ stream = ref new InMemoryRandomAccessStream();
// Get an output stream for the anchor data.
IOutputStream^ outputStream = stream->GetOutputStreamAt(0);
// Create a writer, to put the bytes in the stream.
DataWriter^ writer = ref new DataWriter(outputStream);
```

Une fois encore, nous avons besoin pour vous assurer de que l’application a l’autorisation d’exporter des données spatiales d’ancrage, qui peut inclure des informations confidentielles relatives à l’environnement utilisateur.

```
// Request access to transfer spatial anchors.
return create_task(SpatialAnchorTransferManager::RequestAccessAsync()).then(
    [&anchorByteDataIn, writer](SpatialPerceptionAccessStatus status)
{
    if (status == SpatialPerceptionAccessStatus::Allowed)
    {
        // Access is allowed.
```

Si l’accès est autorisé, nous pouvons écrire des octets à partir de la mémoire tampon dans un flux de données système.

```
// Write the bytes to the stream.
        byte* anchorDataFirst = &anchorByteDataIn[0];
        size_t anchorDataSize = anchorByteDataIn.size();
        writer->WriteBytes(Platform::ArrayReference<byte>(anchorDataFirst, anchorDataSize));
        // Store the stream.
        return create_task(writer->StoreAsync());
    }
    else
    {
        // Access is denied.
        return task_from_result<size_t>(0);
    }
```

Si nous avons réussies à stocker des octets dans le flux de données, nous pouvons essayer d’importer ces données à l’aide de la SpatialAnchorTransferManager.

```
}).then([writer, stream](unsigned int bytesWritten)
{
    if (bytesWritten > 0)
    {
        // Try to import anchors from the byte stream.
        return create_task(writer->FlushAsync())
            .then([stream](bool dataWasFlushed)
        {
            if (dataWasFlushed)
            {
                // Get the input stream for the anchor data.
                IInputStream^ inputStream = stream->GetInputStreamAt(0);
                return create_task(SpatialAnchorTransferManager::TryImportAnchorsAsync(inputStream));
            }
            else
            {
                return task_from_result<IMapView<String^, SpatialAnchor^>^>(nullptr);
            }
        });
    }
    else
    {
        return task_from_result<IMapView<String^, SpatialAnchor^>^>(nullptr);
    }
```

Si les données peuvent être importés, nous obtenons une vue cartographique de paires clé-valeur associant des chaînes avec des points d’ancrage. Nous pouvons charger cela dans notre propre collection de données en mémoire et utiliser cette collection pour rechercher des points d’ancrage qui nous intéressent.

```
}).then([anchorMapOut](task<Windows::Foundation::Collections::IMapView<String^, SpatialAnchor^>^>  previousTask)
{
    try
    {
        auto importedAnchorsMap = previousTask.get();
        // If the operation was successful, we get a set of imported anchors.
        if (importedAnchorsMap != nullptr)
        {
            for each (auto& pair in importedAnchorsMap)
            {
                // Note that you could look for specific anchors here, if you know their key values.
                auto const& id = pair->Key;
                auto const& anchor = pair->Value;
                // Append "Remote" to the end of the anchor name for disambiguation.
                std::wstring idRemote(id->Data());
                idRemote += L"Remote";
                String^ idRemoteConst = ref new String (idRemote.c_str());
                // Store the anchor in the current in-memory anchor map.
                anchorMapOut->Insert(idRemoteConst, anchor);
            }
            return true;
        }
    }
    catch (Exception^ exception)
    {
        OutputDebugString(L"Error: Unable to import the anchor data buffer bytes into the in-memory anchor collection.\n");
    }
    return false;
});
}
```

**REMARQUE :** Parce que vous pouvez importer une ancre, ne signifie pas nécessairement que vous pouvez l’utiliser immédiatement. Le point d’ancrage est peut-être dans un espace différent ou à un autre emplacement physique entièrement ; le point d’ancrage n’est pas localisable jusqu'à ce que l’appareil ayant reçue a suffisamment d’informations sur l’environnement que le point d’ancrage a été créé, pour restaurer la position de l’ancre par rapport à l’environnement actuel connu visual. L’implémentation du client doit essayer de localiser le point d’ancrage par rapport à votre système de coordonnées local ou d’un cadre de référence avant de continuer sur tente d’utiliser pour le contenu en direct. Par exemple, essayez de localiser le point d’ancrage par rapport à un système de coordonnées actuel régulièrement jusqu'à ce que le point d’ancrage commence à être localisable.

## <a name="special-considerations"></a>Considérations spéciales

Le [TryExportAnchorsAsync](https://msdn.microsoft.com/library/windows/apps/mt592763.aspx) API permet plusieurs [SpatialAnchors](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) pour être exportés dans le même objet binaire blob opaque. Toutefois, il est une différence subtile dans les données qui inclut l’objet blob, en fonction de si un SpatialAnchor unique ou plusieurs SpatialAnchors sont exportés dans un seul appel.

### <a name="export-of-a-single-spatialanchor"></a>Exportation d’un seul SpatialAnchor

L’objet blob contient une représentation de l’environnement à proximité de la SpatialAnchor afin que l’environnement peut être reconnu sur l’appareil qui importe le SpatialAnchor. Une fois l’importation terminée, le nouveau SpatialAnchor seront disponible sur l’appareil. En supposant que l’utilisateur a été récemment à proximité de l’ancre, il sera localisable et hologrammes attachés à la SpatialAnchor peuvent être rendus. Ces hologrammes seront affichera dans le même emplacement physique sur l’appareil d’origine qui a exporté le SpatialAnchor c’était le cas.

![Exportation d’un seul SpatialAnchor](images/singleanchor.png)

### <a name="export-of-multiple-spatialanchors"></a>Exportation de plusieurs SpatialAnchors

Comme l’exportation d’un SpatialAnchor unique, l’objet blob contient une représentation de l’environnement à proximité de tous les SpatialAnchors spécifiés. En outre, l’objet blob contient des informations sur les connexions entre le SpatialAnchors inclus, s’ils sont situés dans le même espace physique. Cela signifie que si deux SpatialAnchors à proximité sont importés, puis un hologramme attaché à la *deuxième* SpatialAnchor serait localisable même si le périphérique reconnaît uniquement l’environnement autour de la *premier* Étant donné que suffisamment de données pour calculer transformation entre les deux SpatialAnchors SpatialAnchor, a été inclus dans l’objet blob. Si les deux SpatialAnchors ont été exportés individuellement (deux des appels distincts à TryExportSpatialAnchors) il peut ne pas être suffisamment de données inclus dans l’objet blob pour hologrammes attaché à la deuxième SpatialAnchor à localisables quand le premier d'entre eux se trouve.

![Plusieurs points d’ancrage exportés à l’aide d’un seul appel TryExportAnchorsAsync](images/multipleanchors.png) ![Plusieurs points d’ancrage exportés à l’aide d’un appel TryExportAnchorsAsync distinct pour chaque point d’ancrage](images/separateanchors.png)

## <a name="example-send-anchor-data-using-a-windowsnetworkingstreamsocket"></a>Exemple : Envoyer des données de point d’ancrage à l’aide d’un Windows::Networking::StreamSocket

Ici, nous fournissons un exemple montrant comment utiliser les données exportées d’ancrage en lui envoyant un réseau TCP. Il s’agit de la HolographicSpatialAnchorTransferSample.

La classe StreamSocket de WinRT utilise la bibliothèque de tâches PPL. Dans le cas d’erreurs réseau, l’erreur est retournée à la tâche suivante dans la chaîne à l’aide d’une exception est levée de nouveau. L’exception contient une valeur HRESULT indiquant l’état d’erreur.

### <a name="use-a-windowsnetworkingstreamsocketlistener-with-tcp-to-send-exported-anchor-data"></a>Utiliser un Windows::Networking::StreamSocketListener avec TCP pour envoyer des données de point d’ancrage exporté

Créer une instance de serveur qui écoute pour une connexion.

```
void SampleAnchorTcpServer::ListenForConnection()
{
    // Make a local copy to avoid races with Closed events.
    StreamSocketListener^ streamSocketListener = m_socketServer;
    if (streamSocketListener == nullptr)
    {
        OutputDebugString(L"Server listening for client.\n");
        // Create the web socket connection.
        streamSocketListener = ref new StreamSocketListener();
        streamSocketListener->Control->KeepAlive = true;
        streamSocketListener->BindEndpointAsync(
            SampleAnchorTcpCommon::m_serverHost,
            SampleAnchorTcpCommon::m_tcpPort
            );
        streamSocketListener->ConnectionReceived +=
            ref new Windows::Foundation::TypedEventHandler<StreamSocketListener^, StreamSocketListenerConnectionReceivedEventArgs^>(
                std::bind(&SampleAnchorTcpServer::OnConnectionReceived, this, _1, _2)
                );
        m_socketServer = streamSocketListener;
    }
    else
    {
        OutputDebugString(L"Error: Stream socket listener not created.\n");
    }
}
```

Lors de la réception d’une connexion, utilisez la connexion de socket client pour envoyer des données de point d’ancrage.

```
void SampleAnchorTcpServer::OnConnectionReceived(StreamSocketListener^ listener, StreamSocketListenerConnectionReceivedEventArgs^ args)
{
    m_socketForClient = args->Socket;
    if (m_socketForClient != nullptr)
    {
        // In this example, when the client first connects, we catch it up to the current state of our anchor set.
        OutputToClientSocket(m_spatialAnchorHelper->GetAnchorMap());
    }
}
```

Maintenant, nous pouvons commencer à envoyer un flux de données qui contient les données exportées d’ancrage.

```
void SampleAnchorTcpServer::OutputToClientSocket(IMap<String^, SpatialAnchor^>^ anchorsToSend)
{
    m_anchorTcpSocketStreamWriter = ref new DataWriter(m_socketForClient->OutputStream);
    OutputDebugString(L"Sending stream to client.\n");
    SendAnchorDataStream(anchorsToSend).then([this](task<bool> previousTask)
    {
        try
        {
            bool success = previousTask.get();
            if (success)
            {
                OutputDebugString(L"Anchor data sent!\n");
            }
            else
            {
                OutputDebugString(L"Error: Anchor data not sent.\n");
            }
        }
        catch (Exception^ exception)
        {
            HandleException(exception);
            OutputDebugString(L"Error: Anchor data was not sent.\n");
        }
    });
}
```

Avant que nous pouvons envoyer le flux de données lui-même, nous devons tout d’abord envoyer un paquet d’en-tête. Ce paquet d’en-tête doit être de longueur fixe, et il doit également indiquer la longueur de la variable tableau d’octets qui est le flux de données d’ancrage ; dans le cas de cet exemple, nous ne disposons d’aucune autre donnée d’en-tête à envoyer, par conséquent, notre en-tête de 4 octets et contient un entier non signé 32 bits.

```
Concurrency::task<bool> SampleAnchorTcpServer::SendAnchorDataLengthMessage(size_t dataStreamLength)
{
    unsigned int arrayLength = dataStreamLength;
    byte* data = reinterpret_cast<byte*>(&arrayLength);
    m_anchorTcpSocketStreamWriter->WriteBytes(Platform::ArrayReference<byte>(data, SampleAnchorTcpCommon::c_streamHeaderByteArrayLength));
    return create_task(m_anchorTcpSocketStreamWriter->StoreAsync()).then([this](unsigned int bytesStored)
    {
        if (bytesStored > 0)
        {
            OutputDebugString(L"Anchor data length stored in stream; Flushing stream.\n");
            return create_task(m_anchorTcpSocketStreamWriter->FlushAsync());
        }
        else
        {
            OutputDebugString(L"Error: Anchor data length not stored in stream.\n");
            return task_from_result<bool>(false);
        }
    });
}
Concurrency::task<bool> SampleAnchorTcpServer::SendAnchorDataStreamIMap<String^, SpatialAnchor^>^ anchorsToSend)
{
    return SpatialAnchorImportExportHelper::ExportAnchorDataAsync(
        &m_exportedAnchorStoreBytes,
        anchorsToSend
        ).then([this](bool anchorDataExported)
    {
        if (anchorDataExported)
        {
            const size_t arrayLength = m_exportedAnchorStoreBytes.size();
            if (arrayLength > 0)
            {
                OutputDebugString(L"Anchor data was exported; sending data stream length message.\n");
                return SendAnchorDataLengthMessage(arrayLength);
            }
        }
        OutputDebugString(L"Error: Anchor data was not exported.\n");
        // No data to send.
        return task_from_result<bool>(false);
```

Une fois que la longueur du flux, en octets, a été envoyée au client, nous pouvons passer à écrire le flux de données lui-même dans le flux de socket. Cela entraîne les octets de la Boutique à soient envoyées au client.

```
}).then([this](bool dataLengthSent)
    {
        if (dataLengthSent)
        {
            OutputDebugString(L"Data stream length message sent; writing exported anchor store bytes to stream.\n");
            m_anchorTcpSocketStreamWriter->WriteBytes(Platform::ArrayReference<byte>(&m_exportedAnchorStoreBytes[0], m_exportedAnchorStoreBytes.size()));
            return create_task(m_anchorTcpSocketStreamWriter->StoreAsync());
        }
        else
        {
            OutputDebugString(L"Error: Data stream length message not sent.\n");
            return task_from_result<size_t>(0);
        }
    }).then([this](unsigned int bytesStored)
    {
        if (bytesStored > 0)
        {
            PrintWstringToDebugConsole(
                std::to_wstring(bytesStored) +
                L" bytes of anchor data written and stored to stream; flushing stream.\n"
                );
        }
        else
        {
            OutputDebugString(L"Error: No anchor data bytes were written to the stream.\n");
        }
        return task_from_result<bool>(false);
    });
}
```

Comme indiqué plus haut dans cette rubrique, nous devons être préparés à gérer les exceptions contenant des messages d’état erreur réseau. Pour les erreurs qui ne sont pas attendues, nous pouvons écrire les informations d’exception à la console de débogage comme suit. Cela nous donnera un doute sur ce qui est arrivé si notre exemple de code ne peut pas terminer la connexion, ou s’il est impossible de terminer l’envoi des données d’ancrage.

```
void SampleAnchorTcpServer::HandleException(Exception^ exception)
{
    PrintWstringToDebugConsole(
        std::wstring(L"Connection error: ") +
        exception->ToString()->Data() +
        L"\n"
        );
}
```

### <a name="use-a-windowsnetworkingstreamsocket-with-tcp-to-receive-exported-anchor-data"></a>Utiliser un Windows::Networking::StreamSocket avec TCP pour recevoir les données exportées d’ancrage

Nous devons tout d’abord, connectez-vous au serveur. Cet exemple de code montre comment créer et configurer un StreamSocket et créer un objet DataReader que vous pouvez utiliser pour acquérir les données de réseau à l’aide de la connexion de socket.

**REMARQUE :** Si vous exécutez cet exemple de code, assurez-vous que vous allez configurer et lancer le serveur avant de démarrer le client.

```
task<bool> SampleAnchorTcpClient::ConnectToServer()
{
    // Make a local copy to avoid races with Closed events.
    StreamSocket^ streamSocket = m_socketClient;
    // Have we connected yet?
    if (m_socketClient == nullptr)
    {
        OutputDebugString(L"Client is attempting to connect to server.\n");
        EndpointPair^ endpointPair = ref new EndpointPair(
            SampleAnchorTcpCommon::m_clientHost,
            SampleAnchorTcpCommon::m_tcpPort,
            SampleAnchorTcpCommon::m_serverHost,
            SampleAnchorTcpCommon::m_tcpPort
            );
        // Create the web socket connection.
        m_socketClient = ref new StreamSocket();
        // The client connects to the server.
        return create_task(m_socketClient->ConnectAsync(endpointPair, SocketProtectionLevel::PlainSocket)).then([this](task<void> previousTask)
        {
            try
            {
                // Try getting all exceptions from the continuation chain above this point.
                previousTask.get();
                m_anchorTcpSocketStreamReader = ref new DataReader(m_socketClient->InputStream);
                OutputDebugString(L"Client connected!\n");
                m_anchorTcpSocketStreamReader->InputStreamOptions = InputStreamOptions::ReadAhead;
                WaitForAnchorDataStream();
                return true;
            }
            catch (Exception^ exception)
            {
                if (exception->HResult == 0x80072741)
                {
                    // This code sample includes a very simple implementation of client/server
                    // endpoint detection: if the current instance tries to connect to itself,
                    // it is determined to be the server.
                    OutputDebugString(L"Starting up the server instance.\n");
                    // When we return false, we'll start up the server instead.
                    return false;
                }
                else if ((exception->HResult == 0x8007274c) || // connection timed out
                    (exception->HResult == 0x80072740)) // connection maxed at server end
                {
                    // If the connection timed out, try again.
                    ConnectToServer();
                }
                else if (exception->HResult == 0x80072741)
                {
                    // No connection is possible.
                }
                HandleException(exception);
                return true;
            }
        });
    }
    else
    {
        OutputDebugString(L"A StreamSocket connection to a server already exists.\n");
        return task_from_result<bool>(true);
    }
}
```

Une fois que nous disposons d’une connexion, nous pouvons attend le serveur envoyer des données. Pour cela, nous appelant LoadAsync sur le lecteur de flux de données.

Le premier jeu d’octets que nous recevons doit toujours être le paquet d’en-tête, ce qui indique le point d’ancrage data stream longueur d’octet comme décrit dans la section précédente.

```
void SampleAnchorTcpClient::WaitForAnchorDataStream()
{
    if (m_anchorTcpSocketStreamReader == nullptr)
    {
        // We have not connected yet.
        return;
    }
    OutputDebugString(L"Waiting for server message.\n");
    // Wait for the first message, which specifies the byte length of the string data.
    create_task(m_anchorTcpSocketStreamReader->LoadAsync(SampleAnchorTcpCommon::c_streamHeaderByteArrayLength)).then([this](unsigned int numberOfBytes)
    {
        if (numberOfBytes > 0)
        {
            OutputDebugString(L"Server message incoming.\n");
            return ReceiveAnchorDataLengthMessage();
        }
        else
        {
            OutputDebugString(L"0-byte async task received, awaiting server message again.\n");
            WaitForAnchorDataStream();
            return task_from_result<size_t>(0);
        }
```

...

```
task<size_t> SampleAnchorTcpClient::ReceiveAnchorDataLengthMessage()
{
    byte data[4];
    m_anchorTcpSocketStreamReader->ReadBytes(Platform::ArrayReference<byte>(data, SampleAnchorTcpCommon::c_streamHeaderByteArrayLength));
    unsigned int lengthMessageSize = *reinterpret_cast<unsigned int*>(data);
    if (lengthMessageSize > 0)
    {
        OutputDebugString(L"One or more anchors to be received.\n");
        return task_from_result<size_t>(lengthMessageSize);
    }
    else
    {
        OutputDebugString(L"No anchors to be received.\n");
        ConnectToServer();
    }
    return task_from_result<size_t>(0);
}
```

Une fois que nous avons bien reçu le paquet d’en-tête, nous savons combien d’octets de données de point d’ancrage nous devons nous attendre. Nous pouvons passer à lire ces octets dans le flux.

```
}).then([this](size_t dataStreamLength)
    {
        if (dataStreamLength > 0)
        {
            std::wstring debugMessage = std::to_wstring(dataStreamLength);
            debugMessage += L" bytes of anchor data incoming.\n";
            OutputDebugString(debugMessage.c_str());
            // Prepare to receive the data stream in one or more pieces.
            m_anchorStreamLength = dataStreamLength;
            m_exportedAnchorStoreBytes.clear();
            m_exportedAnchorStoreBytes.resize(m_anchorStreamLength);
            OutputDebugString(L"Loading byte stream.\n");
            return ReceiveAnchorDataStream();
        }
        else
        {
            OutputDebugString(L"Error: Anchor data size not received.\n");
            ConnectToServer();
            return task_from_result<bool>(false);
        }
    });
}
```

Voici notre code pour la réception du flux de données de point d’ancrage. Là encore, nous chargera tout d’abord les octets à partir du flux ; Cette opération peut prendre un certain temps pour terminer, comme le StreamSocket attend de recevoir cette quantité en octets à partir du réseau.

Lorsque l’opération de chargement est terminée, nous pouvons lire ce nombre d’octets. Si nous avons reçu le nombre d’octets qui nous pensons que pour le flux de données de point d’ancrage, nous pouvons continuer et importer les données d’ancrage ; Si ce n’est pas le cas, il doit vous avoir été une sorte d’erreur. Par exemple, cela peut se produire lorsque l’instance de serveur se termine avant de pouvoir terminer envoyant le flux de données ou le réseau tombe en panne avant que le flux de données entier peut être reçu par le client.

```
task<bool> SampleAnchorTcpClient::ReceiveAnchorDataStream()
{
    if (m_anchorStreamLength > 0)
    {
        // First, we load the bytes from the network socket.
        return create_task(m_anchorTcpSocketStreamReader->LoadAsync(m_anchorStreamLength)).then([this](size_t bytesLoadedByStreamReader)
        {
            if (bytesLoadedByStreamReader > 0)
            {
                // Once the bytes are loaded, we can read them from the stream.
                m_anchorTcpSocketStreamReader->ReadBytes(Platform::ArrayReference<byte>(&m_exportedAnchorStoreBytes[0],
                    bytesLoadedByStreamReader));
                // Check status.
                if (bytesLoadedByStreamReader == m_anchorStreamLength)
                {
                    // The whole stream has arrived. We can process the data.
                    // Informational message of progress complete.
                    std::wstring infoMessage = std::to_wstring(bytesLoadedByStreamReader);
                    infoMessage += L" bytes read out of ";
                    infoMessage += std::to_wstring(m_anchorStreamLength);
                    infoMessage += L" total bytes; importing the data.\n";
                    OutputDebugStringW(infoMessage.c_str());
                    // Kick off a thread to wait for a new message indicating another incoming anchor data stream.
                    WaitForAnchorDataStream();
                    // Process the data for the stream we just received.
                    return SpatialAnchorImportExportHelper::ImportAnchorDataAsync(m_exportedAnchorStoreBytes, m_spatialAnchorHelper->GetAnchorMap());
                }
                else
                {
                    OutputDebugString(L"Error: Fewer than expected anchor data bytes were received.\n");
                }
            }
            else
            {
                OutputDebugString(L"Error: No anchor bytes were received.\n");
            }
            return task_from_result<bool>(false);
        });
    }
    else
    {
        OutputDebugString(L"Warning: A zero-length data buffer was sent.\n");
        return task_from_result<bool>(false);
    }
}
```

Là encore, nous devons être préparés à gérer les erreurs de réseau inconnue.

```
void SampleAnchorTcpClient::HandleException(Exception^ exception)
{
    std::wstring error = L"Connection error: ";
    error += exception->ToString()->Data();
    error += L"\n";
    OutputDebugString(error.c_str());
}
```

C’est tout ! Maintenant, vous devez disposer de suffisamment d’informations pour essayer de rapprocher les ancres reçus sur le réseau. Là encore, notez que le client doit avoir suffisamment de données suivi visuel de l’espace à trouver le point d’ancrage ; Si elle ne fonctionne pas immédiatement, essayez de vous épargne pendant un certain temps. Si cela ne fonctionne toujours pas, que le serveur envoyer plusieurs points d’ancrage et utiliser des communications réseau se pour accorder sur une solution qui fonctionne pour le client. Vous pouvez tester cela en téléchargeant le HolographicSpatialAnchorTransferSample, configuration de votre client et les adresses IP de serveur et déployez-le sur des appareils HoloLens client et serveur.

## <a name="see-also"></a>Voir aussi
* [Bibliothèque de modèles parallèles (PPL)](https://msdn.microsoft.com/library/dd492418.aspx)
* [Windows.Networking.StreamSocket](https://msdn.microsoft.com/library/windows/apps/windows.networking.sockets.streamsocket.aspx)
* [Windows.Networking.StreamSocketListener](https://msdn.microsoft.com/library/windows/apps/windows.networking.sockets.streamsocketlistener.aspx)
