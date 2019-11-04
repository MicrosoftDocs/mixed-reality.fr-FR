---
title: Transferts d’ancrage locaux dans DirectX
description: Explique comment synchroniser deux appareils HoloLens en transférant des ancres spatiales.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, synchroniser, ancrage spatial, transfert, multijoueur, vue, scénario, procédure pas à pas, exemple de code, transfert, transfert d’ancrage local, exportation d’ancrage, importation d’ancrage
ms.openlocfilehash: f961862c3c49872484683e264fb9c62b5d0b60ee
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437956"
---
# <a name="local-anchor-transfers-in-directx"></a>Transferts d’ancrage locaux dans DirectX

Dans les situations où vous ne pouvez pas utiliser les <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres spatiales Azure</a>, les transferts d’ancrage locaux permettent à un appareil hololens d’exporter une ancre à importer par un deuxième appareil hololens.

>[!NOTE]
>Les transferts d’ancrage locaux fournissent un rappel d’ancrage moins fiable que les <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres spatiales Azure</a>, et les appareils iOS et Android ne sont pas pris en charge par cette approche.

>[!NOTE]
>Les extraits de code de cet article illustrent actuellement l' C++utilisation de/CX plutôt que de C++/WinRT conforme C + +17, comme utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).  Les concepts sont équivalents pour C++un projet/WinRT, bien que vous deviez traduire le code.

## <a name="transferring-spatial-anchors"></a>Transfert des ancres spatiales

Vous pouvez transférer des ancres spatiales entre des appareils Windows Mixed Reality à l’aide de [SpatialAnchorTransferManager](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchortransfermanager.aspx). Cette API vous permet de regrouper une ancre avec toutes les données de capteur de prise en charge nécessaires pour trouver cet emplacement exact dans le monde, puis d’importer cette offre groupée sur un autre appareil. Une fois que l’application sur le deuxième appareil a importé cette ancre, chaque application peut restituer des hologrammes à l’aide du système de coordonnées de cette ancre spatiale partagée, qui apparaît alors au même endroit dans le monde réel.

Notez que les ancres spatiales ne peuvent pas être transférées entre différents types d’appareils, par exemple une ancre spatiale HoloLens peut ne pas être localisable à l’aide d’un casque immersif.  Les ancres transférées ne sont pas non plus compatibles avec les appareils iOS ou Android.

## <a name="set-up-your-app-to-use-the-spatialperception-capability"></a>Configurer votre application pour utiliser la fonctionnalité spatialPerception

Pour pouvoir utiliser le [SpatialAnchorTransferManager](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchortransfermanager.aspx), votre application doit avoir l’autorisation d’utiliser la fonctionnalité spatialPerception. Cela est nécessaire, car le transfert d’une ancre spatiale implique le partage d’images de capteur collectées au fil du temps à proximité de cette ancre, qui peut inclure des informations sensibles.

Déclarez cette fonctionnalité dans le fichier Package. appxmanifest pour votre application. Voici un exemple :

```
<Capabilities>
  <uap2:Capability Name="spatialPerception" />
</Capabilities>
```

La fonctionnalité provient de l’espace de noms **UAP2** . Pour accéder à cet espace de noms dans votre manifeste, incluez-le en tant qu’attribut *xlmns* dans l’élément &lt;> Package. Voici un exemple :

```
<Package
    xmlns="https://schemas.microsoft.com/appx/manifest/foundation/windows10"
    xmlns:mp="https://schemas.microsoft.com/appx/2014/phone/manifest"
    xmlns:uap="https://schemas.microsoft.com/appx/manifest/uap/windows10"
    xmlns:uap2="https://schemas.microsoft.com/appx/manifest/uap/windows10/2"
    IgnorableNamespaces="uap mp"
    >
```

**Remarque :** Votre application devra demander la fonctionnalité au moment de l’exécution avant de pouvoir accéder aux API d’exportation/importation SpatialAnchor. Consultez [RequestAccessAsync](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchortransfermanager.requestaccessasync.aspx) dans les exemples ci-dessous.

## <a name="serialize-anchor-data-by-exporting-it-with-the-spatialanchortransfermanager"></a>Sérialisez les données d’ancrage en les exportant avec SpatialAnchorTransferManager

Une fonction d’assistance est incluse dans l’exemple de code pour exporter (sérialiser) des données [SpatialAnchor](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) . Cette API d’exportation sérialise toutes les ancres dans une collection de paires clé-valeur associant des chaînes à des points d’ancrage.

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

Tout d’abord, nous devons configurer le flux de données. Cela nous permettra de 1.) Utilisez TryExportAnchorsAsync pour placer les données dans une mémoire tampon appartenant à l’application, et 2.) lire les données du flux de mémoire tampon d’octets exporté, qui est un flux de données WinRT-dans notre propre mémoire tampon, qui est un > d’octets std :: Vector&lt;.

```
// Create a random access stream to process the anchor byte data.
InMemoryRandomAccessStream^ stream = ref new InMemoryRandomAccessStream();
// Get an output stream for the anchor byte stream.
IOutputStream^ outputStream = stream->GetOutputStreamAt(0);
```

Nous devons demander l’autorisation d’accéder aux données spatiales, y compris les ancres exportées par le système.

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

Si nous obtenons l’autorisation et que les ancres sont exportées, nous pouvons lire le flux de données. Ici, nous vous montrons également comment créer le DataReader et le InputStream que nous utiliserons pour lire les données.

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

Une fois que nous avons lu octets à partir du flux, nous pouvons les enregistrer dans notre propre mémoire tampon de données, comme c’est le cas.

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

## <a name="deserialize-anchor-data-by-importing-it-into-the-system-using-the-spatialanchortransfermanager"></a>Désérialiser les données d’ancrage en les important dans le système à l’aide de SpatialAnchorTransferManager

Une fonction d’assistance est incluse dans l’exemple de code pour charger des données précédemment exportées. Cette fonction de désérialisation fournit une collection de paires clé-valeur, similaire à ce que le SpatialAnchorStore fournit, sauf que nous obtenons ces données à partir d’une autre source, telle qu’un socket réseau. Vous pouvez traiter et motifr ces données avant de les stocker hors connexion, à l’aide de la mémoire dans l’application ou (le cas échéant) de l’SpatialAnchorStore de votre application.

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

Tout d’abord, nous devons créer des objets de flux pour accéder aux données d’ancrage. Nous allons écrire les données de notre tampon dans une mémoire tampon système. nous allons donc créer une DataWriter qui écrit dans un flux de données en mémoire afin d’atteindre notre objectif d’obtenir des ancres à partir d’une mémoire tampon d’octets dans le système en tant que SpatialAnchors.

```
// Create a random access stream for the anchor data.
InMemoryRandomAccessStream^ stream = ref new InMemoryRandomAccessStream();
// Get an output stream for the anchor data.
IOutputStream^ outputStream = stream->GetOutputStreamAt(0);
// Create a writer, to put the bytes in the stream.
DataWriter^ writer = ref new DataWriter(outputStream);
```

Là encore, nous devons nous assurer que l’application a l’autorisation d’exporter les données d’ancrage spatiale, ce qui peut inclure des informations privées sur l’environnement de l’utilisateur.

```
// Request access to transfer spatial anchors.
return create_task(SpatialAnchorTransferManager::RequestAccessAsync()).then(
    [&anchorByteDataIn, writer](SpatialPerceptionAccessStatus status)
{
    if (status == SpatialPerceptionAccessStatus::Allowed)
    {
        // Access is allowed.
```

Si l’accès est autorisé, nous pouvons écrire des octets de la mémoire tampon dans un flux de données système.

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

Si nous avons réussi à stocker les octets dans le flux de données, nous pouvons essayer d’importer ces données à l’aide de SpatialAnchorTransferManager.

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

Si les données peuvent être importées, nous obtenons une vue cartographique des paires clé-valeur associant des chaînes à des points d’ancrage. Nous pouvons charger cela dans notre propre collecte de données en mémoire et utiliser cette collection pour rechercher les ancres que nous souhaitons utiliser.

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

**Remarque :** La seule raison pour laquelle vous pouvez importer une ancre ne signifie pas nécessairement que vous pouvez l’utiliser immédiatement. Le point d’ancrage peut se trouver dans une salle différente, ou dans un autre emplacement physique. le point d’ancrage ne peut pas être localisé tant que l’appareil qui l’a reçu n’a pas suffisamment d’informations visuelles sur l’environnement dans lequel l’ancre a été créée, afin de restaurer la position de l’ancre par rapport à l’environnement actuel connu. L’implémentation du client doit essayer de localiser le point d’ancrage par rapport au système de coordonnées local ou au frame de référence avant de continuer à essayer de l’utiliser pour du contenu dynamique. Par exemple, essayez de localiser l’ancre par rapport à un système de coordonnées actif régulièrement jusqu’à ce que le point d’ancrage commence à être localisable.

## <a name="special-considerations"></a>Considérations spéciales

L’API [TryExportAnchorsAsync](https://msdn.microsoft.com/library/windows/apps/mt592763.aspx) permet d’exporter plusieurs [SpatialAnchors](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) dans le même objet blob binaire opaque. Toutefois, il existe une différence subtile entre les données que l’objet BLOB doit inclure, selon qu’un seul SpatialAnchor ou plusieurs SpatialAnchors sont exportés dans un seul appel.

### <a name="export-of-a-single-spatialanchor"></a>Exportation d’un SpatialAnchor unique

L’objet BLOB contient une représentation de l’environnement à proximité du SpatialAnchor afin que l’environnement puisse être reconnu sur l’appareil qui importe le SpatialAnchor. Une fois l’importation terminée, la nouvelle SpatialAnchor sera disponible pour l’appareil. En supposant que l’utilisateur a récemment été à proximité de l’ancre, il sera localisable et les hologrammes attachés au SpatialAnchor peuvent être rendus. Ces hologrammes s’affichent dans l’emplacement physique où ils se trouvaient sur l’appareil d’origine, ce qui a exporté le SpatialAnchor.

![Exportation d’un SpatialAnchor unique](images/singleanchor.png)

### <a name="export-of-multiple-spatialanchors"></a>Exportation de plusieurs SpatialAnchors

À l’instar de l’exportation d’un seul SpatialAnchor, l’objet BLOB contient une représentation de l’environnement à proximité de tous les SpatialAnchors spécifiés. En outre, l’objet BLOB contient des informations sur les connexions entre les SpatialAnchors inclus, s’ils se trouvent dans le même espace physique. Cela signifie que si deux SpatialAnchors à proximité sont importés, un hologramme attaché au *second* SpatialAnchor serait localisable même si l’appareil reconnaît uniquement l’environnement autour du *premier* SpatialAnchor, car il y a suffisamment de données pour la transformation de calcul entre les deux SpatialAnchors a été incluse dans l’objet BLOB. Si les deux SpatialAnchors ont été exportés individuellement (deux appels distincts à TryExportSpatialAnchors), il se peut que le nombre de données incluses dans l’objet BLOB soit insuffisant pour les hologrammes attachés au deuxième SpatialAnchor à localiser lorsque le premier est localisé.

![Plusieurs ancres exportées à l’aide d’un seul appel TryExportAnchorsAsync](images/multipleanchors.png) ![Plusieurs ancres exportées à l’aide d’un appel TryExportAnchorsAsync distinct pour chaque ancre](images/separateanchors.png)

## <a name="example-send-anchor-data-using-a-windowsnetworkingstreamsocket"></a>Exemple : envoyer des données d’ancrage à l’aide d’un Windows :: Networking :: StreamSocket

Ici, nous fournissons un exemple d’utilisation des données d’ancrage exportées en les envoyant à travers un réseau TCP. C’est à partir du HolographicSpatialAnchorTransferSample.

La classe StreamSocket WinRT utilise la bibliothèque de tâches PPL. Dans le cas d’erreurs réseau, l’erreur est retournée à la tâche suivante dans la chaîne à l’aide d’une exception qui est levée à nouveau. L’exception contient un HRESULT indiquant l’état de l’erreur.

### <a name="use-a-windowsnetworkingstreamsocketlistener-with-tcp-to-send-exported-anchor-data"></a>Utiliser un Windows :: Networking :: StreamSocketListener avec TCP pour envoyer des données d’ancrage exportées

Créez une instance de serveur qui écoute une connexion.

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

Quand une connexion est reçue, utilisez la connexion de socket client pour envoyer des données d’ancrage.

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

À présent, nous pouvons commencer à envoyer un flux de données qui contient les données d’ancrage exportées.

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

Avant de pouvoir envoyer le flux lui-même, nous devons d’abord envoyer un paquet d’en-tête. Ce paquet d’en-tête doit avoir une longueur fixe et doit également indiquer la longueur du tableau de variables d’octets qui est le flux de données d’ancrage ; dans le cas de cet exemple, nous n’avons pas d’autres données d’en-tête à envoyer. par conséquent, notre en-tête a une longueur de 4 octets et contient un entier non signé 32 bits.

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

Une fois que la longueur du flux, en octets, a été envoyée au client, nous pouvons continuer à écrire le flux de données lui-même dans le flux de Socket. Les octets du magasin d’ancrage sont alors envoyés au client.

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

Comme indiqué précédemment dans cette rubrique, nous devons être prêts à gérer les exceptions contenant les messages d’état d’erreur réseau. Pour les erreurs qui ne sont pas attendues, nous pouvons écrire les informations sur l’exception dans la console de débogage, comme c’est le cas. Cela nous donne un indice sur ce qui s’est produit si notre exemple de code ne parvient pas à terminer la connexion, ou s’il ne parvient pas à terminer l’envoi des données d’ancrage.

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

### <a name="use-a-windowsnetworkingstreamsocket-with-tcp-to-receive-exported-anchor-data"></a>Utiliser un Windows :: Networking :: StreamSocket avec TCP pour recevoir les données d’ancrage exportées

Tout d’abord, nous devons nous connecter au serveur. Cet exemple de code montre comment créer et configurer un StreamSocket et créer un DataReader que vous pouvez utiliser pour acquérir des données réseau à l’aide de la connexion de Socket.

**Remarque :** Si vous exécutez cet exemple de code, assurez-vous de configurer et de lancer le serveur avant de démarrer le client.

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

Une fois que nous disposons d’une connexion, nous pouvons attendre que le serveur envoie des données. Pour ce faire, nous appelons LoadAsync sur le lecteur de données de flux.

Le premier jeu d’octets que nous recevons doit toujours être le paquet d’en-tête, qui indique la longueur en octets du flux de données d’ancrage comme décrit dans la section précédente.

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

Une fois que nous avons reçu le paquet d’en-tête, nous savons combien d’octets de données d’ancrage devraient s’attendre. Nous pouvons continuer à lire ces octets dans le flux.

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

Voici notre code pour recevoir le flux de données d’ancrage. Là encore, nous allons d’abord charger les octets à partir du flux. l’exécution de cette opération peut prendre un certain temps, car le StreamSocket attend de recevoir ce nombre d’octets à partir du réseau.

Lorsque l’opération de chargement est terminée, nous pouvons lire ce nombre d’octets. Si nous avons reçu le nombre d’octets attendu pour le flux de données d’ancrage, nous pouvons importer les données d’ancrage. Si ce n’est pas le cas, il doit y avoir une erreur. Par exemple, cela peut se produire lorsque l’instance de serveur se termine avant de terminer l’envoi du flux de données, ou que le réseau tombe en panne avant que le client ne puisse recevoir la totalité du flux de données.

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

Là encore, vous devez être prêt à gérer les erreurs réseau inconnues.

```
void SampleAnchorTcpClient::HandleException(Exception^ exception)
{
    std::wstring error = L"Connection error: ";
    error += exception->ToString()->Data();
    error += L"\n";
    OutputDebugString(error.c_str());
}
```

C’est tout ! Maintenant, vous devez disposer de suffisamment d’informations pour essayer de localiser les ancres reçues sur le réseau. Là encore, Notez que le client doit disposer d’un nombre suffisant de données de suivi visuel pour l’espace pour la localisation de l’ancre. Si cela ne fonctionne pas immédiatement, essayez de vous lancer pendant un certain temps. Si cela ne fonctionne toujours pas, faites en sorte que le serveur envoie davantage d’ancres et qu’il utilise des communications réseau pour s’en contenter. Vous pouvez essayer cela en téléchargeant le HolographicSpatialAnchorTransferSample, en configurant les adresses IP du client et du serveur, et en le déployant sur des appareils HoloLens client et serveur.

## <a name="see-also"></a>Articles associés
* [Bibliothèque de modèles parallèles (PPL)](https://msdn.microsoft.com/library/dd492418.aspx)
* [Windows. Networking. StreamSocket](https://msdn.microsoft.com/library/windows/apps/windows.networking.sockets.streamsocket.aspx)
* [Windows. Networking. StreamSocketListener](https://msdn.microsoft.com/library/windows/apps/windows.networking.sockets.streamsocketlistener.aspx)
