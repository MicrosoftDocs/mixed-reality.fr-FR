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
# <a name="local-anchor-transfers-in-directx"></a><span data-ttu-id="d3473-104">Transferts d’ancrage local dans DirectX</span><span class="sxs-lookup"><span data-stu-id="d3473-104">Local anchor transfers in DirectX</span></span>

<span data-ttu-id="d3473-105">Dans les situations où vous ne pouvez pas utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres Spatial Azure</a>, les transferts d’ancrage local activer un appareil HoloLens exporter un point d’ancrage doivent être importées par un deuxième appareil HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d3473-105">In situations where you cannot use <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>, local anchor transfers enable one HoloLens device to export an anchor to be imported by a second HoloLens device.</span></span>

>[!NOTE]
><span data-ttu-id="d3473-106">Les transferts d’ancrage local fournissent moins fiable rappel d’ancrage que <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres Spatial Azure</a>, et les appareils iOS et Android ne sont pas pris en charge par cette approche.</span><span class="sxs-lookup"><span data-stu-id="d3473-106">Local anchor transfers provide less robust anchor recall than <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>, and iOS and Android devices are not supported by this approach.</span></span>

>[!NOTE]
><span data-ttu-id="d3473-107">Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="d3473-107">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="d3473-108">Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="d3473-108">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

## <a name="transferring-spatial-anchors"></a><span data-ttu-id="d3473-109">Transfert des ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="d3473-109">Transferring spatial anchors</span></span>

<span data-ttu-id="d3473-110">Vous pouvez transférer des ancres spatiales entre les appareils de réalité mixte Windows à l’aide de la [SpatialAnchorTransferManager](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchortransfermanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3473-110">You can transfer spatial anchors between Windows Mixed Reality devices by using the [SpatialAnchorTransferManager](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchortransfermanager.aspx).</span></span> <span data-ttu-id="d3473-111">Cette API vous permet de regrouper un point d’ancrage avec toutes les données de capteur de prise en charge nécessaires pour rechercher cet emplacement exact dans le monde et ensuite importer cette offre groupée sur un autre appareil.</span><span class="sxs-lookup"><span data-stu-id="d3473-111">This API lets you bundle up an anchor with all the supporting sensor data needed to find that exact place in the world, and then import that bundle on another device.</span></span> <span data-ttu-id="d3473-112">Une fois que l’application sur le deuxième a importé ce point d’ancrage, chaque application peut rendre hologrammes à l’aide qui partagé du système de coordonnées spatiales de l’ancre, qui apparaîtra au même endroit dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="d3473-112">Once the app on the second device has imported that anchor, each app can render holograms using that shared spatial anchor's coordinate system, which will then appear in the same place in the real world.</span></span>

<span data-ttu-id="d3473-113">Notez que les ancres spatiales ne sont pas en mesure de transférer entre différents types d’appareil, par exemple un point d’ancrage spatial HoloLens est peut-être pas localisable à l’aide d’un casque immersif.</span><span class="sxs-lookup"><span data-stu-id="d3473-113">Note that spatial anchors are not able to transfer between different device types, for example a HoloLens spatial anchor may not be locatable using an immersive headset.</span></span>  <span data-ttu-id="d3473-114">Également les ancres transférées ne sont pas compatibles avec les appareils iOS ou Android.</span><span class="sxs-lookup"><span data-stu-id="d3473-114">Transferred anchors are also not compatible with iOS or Android devices.</span></span>

## <a name="set-up-your-app-to-use-the-spatialperception-capability"></a><span data-ttu-id="d3473-115">Configurer votre application pour utiliser la fonctionnalité spatialPerception</span><span class="sxs-lookup"><span data-stu-id="d3473-115">Set up your app to use the spatialPerception capability</span></span>

<span data-ttu-id="d3473-116">Votre application doit être autorisée à utiliser la fonctionnalité de spatialPerception avant qu’il puisse utiliser le [SpatialAnchorTransferManager](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchortransfermanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3473-116">Your app must be granted permission to use the spatialPerception capability before it can use the [SpatialAnchorTransferManager](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchortransfermanager.aspx).</span></span> <span data-ttu-id="d3473-117">Cela est nécessaire, car transfert d’un point d’ancrage spatial concerne le partage des images de capteur collectées au fil du temps à proximité de ce point d’ancrage, ce qui peut inclure des informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="d3473-117">This is necessary because transferring a spatial anchor involves sharing sensor images gathered over time in vicinity of that anchor, which might include sensitive information.</span></span>

<span data-ttu-id="d3473-118">Déclarez cette fonctionnalité dans le fichier package.appxmanifest pour votre application.</span><span class="sxs-lookup"><span data-stu-id="d3473-118">Declare this capability in the package.appxmanifest file for your app.</span></span> <span data-ttu-id="d3473-119">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="d3473-119">Here's an example:</span></span>

```
<Capabilities>
  <uap2:Capability Name="spatialPerception" />
</Capabilities>
```

<span data-ttu-id="d3473-120">La fonctionnalité provient de la **uap2** espace de noms.</span><span class="sxs-lookup"><span data-stu-id="d3473-120">The capability comes from the **uap2** namespace.</span></span> <span data-ttu-id="d3473-121">Pour accéder à cet espace de noms dans votre manifeste, inclure un *xlmns* d’attribut dans le &lt;Package > élément.</span><span class="sxs-lookup"><span data-stu-id="d3473-121">To get access to this namespace in your manifest, include it as an *xlmns* attribute in the &lt;Package> element.</span></span> <span data-ttu-id="d3473-122">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="d3473-122">Here's an example:</span></span>

```
<Package
    xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
    xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
    xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
    xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2"
    IgnorableNamespaces="uap mp"
    >
```

<span data-ttu-id="d3473-123">**REMARQUE :** Votre application a besoin demander la fonctionnalité au runtime qu’il puisse accéder SpatialAnchor exportation/importation API.</span><span class="sxs-lookup"><span data-stu-id="d3473-123">**NOTE:** Your app will need to request the capability at runtime before it can access SpatialAnchor export/import APIs.</span></span> <span data-ttu-id="d3473-124">Consultez [RequestAccessAsync](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchortransfermanager.requestaccessasync.aspx) dans les exemples ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d3473-124">See [RequestAccessAsync](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchortransfermanager.requestaccessasync.aspx) in the examples below.</span></span>

## <a name="serialize-anchor-data-by-exporting-it-with-the-spatialanchortransfermanager"></a><span data-ttu-id="d3473-125">Sérialiser les données de point d’ancrage en les exportant avec la SpatialAnchorTransferManager</span><span class="sxs-lookup"><span data-stu-id="d3473-125">Serialize anchor data by exporting it with the SpatialAnchorTransferManager</span></span>

<span data-ttu-id="d3473-126">Une fonction d’assistance est incluse dans l’exemple de code pour exporter (sérialiser) [SpatialAnchor](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) données.</span><span class="sxs-lookup"><span data-stu-id="d3473-126">A helper function is included in the code sample to export (serialize) [SpatialAnchor](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) data.</span></span> <span data-ttu-id="d3473-127">Cette API d’exportation sérialise tous les points d’ancrage dans une collection de paires clé-valeur associant des chaînes avec des points d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="d3473-127">This export API serializes all anchors in a collection of key-value pairs associating strings with anchors.</span></span>

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

<span data-ttu-id="d3473-128">Tout d’abord, nous devons configurer le flux de données.</span><span class="sxs-lookup"><span data-stu-id="d3473-128">First, we need to set up the data stream.</span></span> <span data-ttu-id="d3473-129">Cela nous permettra à 1.) Utilisez TryExportAnchorsAsync pour placer les données dans une mémoire tampon détenue par l’application et 2). lire les données à partir du flux de mémoire tampon d’octets exporté, qui est un flux de données WinRT - dans notre propre mémoire tampon, qui est un std::vector&lt;octets >.</span><span class="sxs-lookup"><span data-stu-id="d3473-129">This will allow us to 1.) use TryExportAnchorsAsync to put the data in a buffer owned by the app, and 2.) read data from the exported byte buffer stream - which is a WinRT data stream - into our own memory buffer, which is a std::vector&lt;byte>.</span></span>

```
// Create a random access stream to process the anchor byte data.
InMemoryRandomAccessStream^ stream = ref new InMemoryRandomAccessStream();
// Get an output stream for the anchor byte stream.
IOutputStream^ outputStream = stream->GetOutputStreamAt(0);
```

<span data-ttu-id="d3473-130">Nous avons besoin de demander l’autorisation d’accéder aux données spatiales, y compris les points d’ancrage qui sont exportés par le système.</span><span class="sxs-lookup"><span data-stu-id="d3473-130">We need to ask permission to access spatial data, including anchors that are exported by the system.</span></span>

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

<span data-ttu-id="d3473-131">Si nous obtenons bien autorisation et points d’ancrage sont exportés, nous pouvons lire le flux de données.</span><span class="sxs-lookup"><span data-stu-id="d3473-131">If we do get permission and anchors are exported, we can read the data stream.</span></span> <span data-ttu-id="d3473-132">Ici, nous montrons également comment créer le DataReader et InputStream, nous allons utiliser pour lire les données.</span><span class="sxs-lookup"><span data-stu-id="d3473-132">Here, we also show how to create the DataReader and InputStream we will use to read the data.</span></span>

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

<span data-ttu-id="d3473-133">Une fois que nous lire les octets à partir du flux, nous pouvons les enregistrer dans notre propre mémoire tampon de données comme suit.</span><span class="sxs-lookup"><span data-stu-id="d3473-133">After we read bytes from the stream, we can save them to our own data buffer like so.</span></span>

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

## <a name="deserialize-anchor-data-by-importing-it-into-the-system-using-the-spatialanchortransfermanager"></a><span data-ttu-id="d3473-134">Désérialiser des données de point d’ancrage en l’important dans le système à l’aide de la SpatialAnchorTransferManager</span><span class="sxs-lookup"><span data-stu-id="d3473-134">Deserialize anchor data by importing it into the system using the SpatialAnchorTransferManager</span></span>

<span data-ttu-id="d3473-135">Une fonction d’assistance est incluse dans l’exemple de code pour charger des données précédemment exportées.</span><span class="sxs-lookup"><span data-stu-id="d3473-135">A helper function is included in the code sample to load previously exported data.</span></span> <span data-ttu-id="d3473-136">Cette fonction de la désérialisation fournit une collection de paires clé-valeur, similaires à ce que fournit le SpatialAnchorStore -, à ceci près que nous avons ces données à partir d’une autre source, comme un socket réseau.</span><span class="sxs-lookup"><span data-stu-id="d3473-136">This deserialization function provides a collection of key-value pairs, similar to what the SpatialAnchorStore provides - except that we got this data from another source, such as a network socket.</span></span> <span data-ttu-id="d3473-137">Vous pouvez traiter et analyser ces données avant de les stocker en mémoire dans l’application en mode hors connexion, à l’aide, ou (le cas échéant) SpatialAnchorStore de votre application.</span><span class="sxs-lookup"><span data-stu-id="d3473-137">You can process and reason about this data before storing it offline, using in-app memory, or (if applicable) your app's SpatialAnchorStore.</span></span>

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

<span data-ttu-id="d3473-138">Tout d’abord, nous devons créer des objets de flux de données pour accéder aux données d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="d3473-138">First, we need to create stream objects to access the anchor data.</span></span> <span data-ttu-id="d3473-139">Nous doit écrire les données à partir de notre mémoire tampon dans une mémoire tampon du système, donc nous allons créer un DataWriter qui écrit dans un flux de données en mémoire afin d’atteindre notre objectif de l’obtention des points d’ancrage à partir d’une mémoire tampon d’octets dans le système en tant que SpatialAnchors.</span><span class="sxs-lookup"><span data-stu-id="d3473-139">We will be writing the data from our buffer to a system buffer, so we will create a DataWriter that writes to an in-memory data stream in order to accomplish our goal of getting anchors from a byte buffer into the system as SpatialAnchors.</span></span>

```
// Create a random access stream for the anchor data.
InMemoryRandomAccessStream^ stream = ref new InMemoryRandomAccessStream();
// Get an output stream for the anchor data.
IOutputStream^ outputStream = stream->GetOutputStreamAt(0);
// Create a writer, to put the bytes in the stream.
DataWriter^ writer = ref new DataWriter(outputStream);
```

<span data-ttu-id="d3473-140">Une fois encore, nous avons besoin pour vous assurer de que l’application a l’autorisation d’exporter des données spatiales d’ancrage, qui peut inclure des informations confidentielles relatives à l’environnement utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d3473-140">Once again, we need to ensure the app has permission to export spatial anchor data, which could include private information about the user's environment.</span></span>

```
// Request access to transfer spatial anchors.
return create_task(SpatialAnchorTransferManager::RequestAccessAsync()).then(
    [&anchorByteDataIn, writer](SpatialPerceptionAccessStatus status)
{
    if (status == SpatialPerceptionAccessStatus::Allowed)
    {
        // Access is allowed.
```

<span data-ttu-id="d3473-141">Si l’accès est autorisé, nous pouvons écrire des octets à partir de la mémoire tampon dans un flux de données système.</span><span class="sxs-lookup"><span data-stu-id="d3473-141">If access is allowed, we can write bytes from the buffer to a system data stream.</span></span>

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

<span data-ttu-id="d3473-142">Si nous avons réussies à stocker des octets dans le flux de données, nous pouvons essayer d’importer ces données à l’aide de la SpatialAnchorTransferManager.</span><span class="sxs-lookup"><span data-stu-id="d3473-142">If we were successful in storing bytes in the data stream, we can try to import that data using the SpatialAnchorTransferManager.</span></span>

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

<span data-ttu-id="d3473-143">Si les données peuvent être importés, nous obtenons une vue cartographique de paires clé-valeur associant des chaînes avec des points d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="d3473-143">If the data is able to be imported, we get a map view of key-value pairs associating strings with anchors.</span></span> <span data-ttu-id="d3473-144">Nous pouvons charger cela dans notre propre collection de données en mémoire et utiliser cette collection pour rechercher des points d’ancrage qui nous intéressent.</span><span class="sxs-lookup"><span data-stu-id="d3473-144">We can load this into our own in-memory data collection, and use that collection to look for anchors that we are interested in using.</span></span>

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

<span data-ttu-id="d3473-145">**REMARQUE :** Parce que vous pouvez importer une ancre, ne signifie pas nécessairement que vous pouvez l’utiliser immédiatement.</span><span class="sxs-lookup"><span data-stu-id="d3473-145">**NOTE:** Just because you can import an anchor, doesn't necessarily mean that you can use it right away.</span></span> <span data-ttu-id="d3473-146">Le point d’ancrage est peut-être dans un espace différent ou à un autre emplacement physique entièrement ; le point d’ancrage n’est pas localisable jusqu'à ce que l’appareil ayant reçue a suffisamment d’informations sur l’environnement que le point d’ancrage a été créé, pour restaurer la position de l’ancre par rapport à l’environnement actuel connu visual.</span><span class="sxs-lookup"><span data-stu-id="d3473-146">The anchor might be in a different room, or another physical location entirely; the anchor won't be locatable until the device that received it has enough visual information about the environment the anchor was created in, to restore the anchor's position relative to the known current environment.</span></span> <span data-ttu-id="d3473-147">L’implémentation du client doit essayer de localiser le point d’ancrage par rapport à votre système de coordonnées local ou d’un cadre de référence avant de continuer sur tente d’utiliser pour le contenu en direct.</span><span class="sxs-lookup"><span data-stu-id="d3473-147">The client implementation should try locating the anchor relative to your local coordinate system or reference frame before continuing on to try to use it for live content.</span></span> <span data-ttu-id="d3473-148">Par exemple, essayez de localiser le point d’ancrage par rapport à un système de coordonnées actuel régulièrement jusqu'à ce que le point d’ancrage commence à être localisable.</span><span class="sxs-lookup"><span data-stu-id="d3473-148">For example, try locating the anchor relative to a current coordinate system periodically until the anchor begins to be locatable.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="d3473-149">Considérations spéciales</span><span class="sxs-lookup"><span data-stu-id="d3473-149">Special Considerations</span></span>

<span data-ttu-id="d3473-150">Le [TryExportAnchorsAsync](https://msdn.microsoft.com/library/windows/apps/mt592763.aspx) API permet plusieurs [SpatialAnchors](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) pour être exportés dans le même objet binaire blob opaque.</span><span class="sxs-lookup"><span data-stu-id="d3473-150">The [TryExportAnchorsAsync](https://msdn.microsoft.com/library/windows/apps/mt592763.aspx) API allows multiple [SpatialAnchors](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialanchor.aspx) to be exported into the same opaque binary blob.</span></span> <span data-ttu-id="d3473-151">Toutefois, il est une différence subtile dans les données qui inclut l’objet blob, en fonction de si un SpatialAnchor unique ou plusieurs SpatialAnchors sont exportés dans un seul appel.</span><span class="sxs-lookup"><span data-stu-id="d3473-151">However, there is a subtle difference in what data the blob will include, depending on whether a single SpatialAnchor or multiple SpatialAnchors are exported in a single call.</span></span>

### <a name="export-of-a-single-spatialanchor"></a><span data-ttu-id="d3473-152">Exportation d’un seul SpatialAnchor</span><span class="sxs-lookup"><span data-stu-id="d3473-152">Export of a single SpatialAnchor</span></span>

<span data-ttu-id="d3473-153">L’objet blob contient une représentation de l’environnement à proximité de la SpatialAnchor afin que l’environnement peut être reconnu sur l’appareil qui importe le SpatialAnchor.</span><span class="sxs-lookup"><span data-stu-id="d3473-153">The blob contains a representation of the environment in the vicinity of the SpatialAnchor so that the environment can be recognized on the device that imports the SpatialAnchor.</span></span> <span data-ttu-id="d3473-154">Une fois l’importation terminée, le nouveau SpatialAnchor seront disponible sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="d3473-154">After the import completes, the new SpatialAnchor will be available to the device.</span></span> <span data-ttu-id="d3473-155">En supposant que l’utilisateur a été récemment à proximité de l’ancre, il sera localisable et hologrammes attachés à la SpatialAnchor peuvent être rendus.</span><span class="sxs-lookup"><span data-stu-id="d3473-155">Assuming the user has recently been in vicinity of the anchor, it will be locatable and holograms attached to the SpatialAnchor can be rendered.</span></span> <span data-ttu-id="d3473-156">Ces hologrammes seront affichera dans le même emplacement physique sur l’appareil d’origine qui a exporté le SpatialAnchor c’était le cas.</span><span class="sxs-lookup"><span data-stu-id="d3473-156">These holograms will show up in the same physical location that they did on the original device which exported the SpatialAnchor.</span></span>

![Exportation d’un seul SpatialAnchor](images/singleanchor.png)

### <a name="export-of-multiple-spatialanchors"></a><span data-ttu-id="d3473-158">Exportation de plusieurs SpatialAnchors</span><span class="sxs-lookup"><span data-stu-id="d3473-158">Export of multiple SpatialAnchors</span></span>

<span data-ttu-id="d3473-159">Comme l’exportation d’un SpatialAnchor unique, l’objet blob contient une représentation de l’environnement à proximité de tous les SpatialAnchors spécifiés.</span><span class="sxs-lookup"><span data-stu-id="d3473-159">Like the export of a single SpatialAnchor, the blob contains a representation of the environment in the vicinity of all the specified SpatialAnchors.</span></span> <span data-ttu-id="d3473-160">En outre, l’objet blob contient des informations sur les connexions entre le SpatialAnchors inclus, s’ils sont situés dans le même espace physique.</span><span class="sxs-lookup"><span data-stu-id="d3473-160">In addition, the blob contains information about the connections between the included SpatialAnchors, if they are located in the same physical space.</span></span> <span data-ttu-id="d3473-161">Cela signifie que si deux SpatialAnchors à proximité sont importés, puis un hologramme attaché à la *deuxième* SpatialAnchor serait localisable même si le périphérique reconnaît uniquement l’environnement autour de la *premier* Étant donné que suffisamment de données pour calculer transformation entre les deux SpatialAnchors SpatialAnchor, a été inclus dans l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="d3473-161">This means that if two nearby SpatialAnchors are imported, then a hologram attached to the *second* SpatialAnchor would be locatable even if the device only recognizes the environment around the *first* SpatialAnchor, because enough data to compute transform between the two SpatialAnchors was included in the blob.</span></span> <span data-ttu-id="d3473-162">Si les deux SpatialAnchors ont été exportés individuellement (deux des appels distincts à TryExportSpatialAnchors) il peut ne pas être suffisamment de données inclus dans l’objet blob pour hologrammes attaché à la deuxième SpatialAnchor à localisables quand le premier d'entre eux se trouve.</span><span class="sxs-lookup"><span data-stu-id="d3473-162">If the two SpatialAnchors were exported individually (two separate calls to TryExportSpatialAnchors) then there may not be enough data included in the blob for holograms attached to the second SpatialAnchor to be locatable when the first one is located.</span></span>

![Plusieurs points d’ancrage exportés à l’aide d’un seul appel TryExportAnchorsAsync](images/multipleanchors.png) ![Plusieurs points d’ancrage exportés à l’aide d’un appel TryExportAnchorsAsync distinct pour chaque point d’ancrage](images/separateanchors.png)

## <a name="example-send-anchor-data-using-a-windowsnetworkingstreamsocket"></a><span data-ttu-id="d3473-165">Exemple : Envoyer des données de point d’ancrage à l’aide d’un Windows::Networking::StreamSocket</span><span class="sxs-lookup"><span data-stu-id="d3473-165">Example: Send anchor data using a Windows::Networking::StreamSocket</span></span>

<span data-ttu-id="d3473-166">Ici, nous fournissons un exemple montrant comment utiliser les données exportées d’ancrage en lui envoyant un réseau TCP.</span><span class="sxs-lookup"><span data-stu-id="d3473-166">Here, we provide an example of how to use exported anchor data by sending it across a TCP network.</span></span> <span data-ttu-id="d3473-167">Il s’agit de la HolographicSpatialAnchorTransferSample.</span><span class="sxs-lookup"><span data-stu-id="d3473-167">This is from the HolographicSpatialAnchorTransferSample.</span></span>

<span data-ttu-id="d3473-168">La classe StreamSocket de WinRT utilise la bibliothèque de tâches PPL.</span><span class="sxs-lookup"><span data-stu-id="d3473-168">The WinRT StreamSocket class uses the PPL task library.</span></span> <span data-ttu-id="d3473-169">Dans le cas d’erreurs réseau, l’erreur est retournée à la tâche suivante dans la chaîne à l’aide d’une exception est levée de nouveau.</span><span class="sxs-lookup"><span data-stu-id="d3473-169">In the case of network errors, the error is returned to the next task in the chain using an exception that is re-thrown.</span></span> <span data-ttu-id="d3473-170">L’exception contient une valeur HRESULT indiquant l’état d’erreur.</span><span class="sxs-lookup"><span data-stu-id="d3473-170">The exception contains an HRESULT indicating the error status.</span></span>

### <a name="use-a-windowsnetworkingstreamsocketlistener-with-tcp-to-send-exported-anchor-data"></a><span data-ttu-id="d3473-171">Utiliser un Windows::Networking::StreamSocketListener avec TCP pour envoyer des données de point d’ancrage exporté</span><span class="sxs-lookup"><span data-stu-id="d3473-171">Use a Windows::Networking::StreamSocketListener with TCP to send exported anchor data</span></span>

<span data-ttu-id="d3473-172">Créer une instance de serveur qui écoute pour une connexion.</span><span class="sxs-lookup"><span data-stu-id="d3473-172">Create a server instance that listens for a connection.</span></span>

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

<span data-ttu-id="d3473-173">Lors de la réception d’une connexion, utilisez la connexion de socket client pour envoyer des données de point d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="d3473-173">When a connection is received, use the client socket connection to send anchor data.</span></span>

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

<span data-ttu-id="d3473-174">Maintenant, nous pouvons commencer à envoyer un flux de données qui contient les données exportées d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="d3473-174">Now, we can begin to send a data stream that contains the exported anchor data.</span></span>

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

<span data-ttu-id="d3473-175">Avant que nous pouvons envoyer le flux de données lui-même, nous devons tout d’abord envoyer un paquet d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="d3473-175">Before we can send the stream itself, we must first send a header packet.</span></span> <span data-ttu-id="d3473-176">Ce paquet d’en-tête doit être de longueur fixe, et il doit également indiquer la longueur de la variable tableau d’octets qui est le flux de données d’ancrage ; dans le cas de cet exemple, nous ne disposons d’aucune autre donnée d’en-tête à envoyer, par conséquent, notre en-tête de 4 octets et contient un entier non signé 32 bits.</span><span class="sxs-lookup"><span data-stu-id="d3473-176">This header packet must be of fixed length, and it must also indicate the length of the variable array of bytes that is the anchor data stream; in the case of this example we have no other header data to send, so our header is 4 bytes long and contains a 32-bit unsigned integer.</span></span>

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

<span data-ttu-id="d3473-177">Une fois que la longueur du flux, en octets, a été envoyée au client, nous pouvons passer à écrire le flux de données lui-même dans le flux de socket.</span><span class="sxs-lookup"><span data-stu-id="d3473-177">Once the stream length, in bytes, has been sent to the client, we can proceed to write the data stream itself to the socket stream.</span></span> <span data-ttu-id="d3473-178">Cela entraîne les octets de la Boutique à soient envoyées au client.</span><span class="sxs-lookup"><span data-stu-id="d3473-178">This will cause the anchor store bytes to get sent to the client.</span></span>

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

<span data-ttu-id="d3473-179">Comme indiqué plus haut dans cette rubrique, nous devons être préparés à gérer les exceptions contenant des messages d’état erreur réseau.</span><span class="sxs-lookup"><span data-stu-id="d3473-179">As noted earlier in this topic, we must be prepared to handle exceptions containing network error status messages.</span></span> <span data-ttu-id="d3473-180">Pour les erreurs qui ne sont pas attendues, nous pouvons écrire les informations d’exception à la console de débogage comme suit.</span><span class="sxs-lookup"><span data-stu-id="d3473-180">For errors that are not expected, we can write the exception info to the debug console like so.</span></span> <span data-ttu-id="d3473-181">Cela nous donnera un doute sur ce qui est arrivé si notre exemple de code ne peut pas terminer la connexion, ou s’il est impossible de terminer l’envoi des données d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="d3473-181">This will give us a clue as to what happened if our code sample is unable to complete the connection, or if it is unable to finish sending the anchor data.</span></span>

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

### <a name="use-a-windowsnetworkingstreamsocket-with-tcp-to-receive-exported-anchor-data"></a><span data-ttu-id="d3473-182">Utiliser un Windows::Networking::StreamSocket avec TCP pour recevoir les données exportées d’ancrage</span><span class="sxs-lookup"><span data-stu-id="d3473-182">Use a Windows::Networking::StreamSocket with TCP to receive exported anchor data</span></span>

<span data-ttu-id="d3473-183">Nous devons tout d’abord, connectez-vous au serveur.</span><span class="sxs-lookup"><span data-stu-id="d3473-183">First, we have to connect to the server.</span></span> <span data-ttu-id="d3473-184">Cet exemple de code montre comment créer et configurer un StreamSocket et créer un objet DataReader que vous pouvez utiliser pour acquérir les données de réseau à l’aide de la connexion de socket.</span><span class="sxs-lookup"><span data-stu-id="d3473-184">This code sample shows how to create and configure a StreamSocket, and create a DataReader that you can use to acquire network data using the socket connection.</span></span>

<span data-ttu-id="d3473-185">**REMARQUE :** Si vous exécutez cet exemple de code, assurez-vous que vous allez configurer et lancer le serveur avant de démarrer le client.</span><span class="sxs-lookup"><span data-stu-id="d3473-185">**NOTE:** If you run this sample code, ensure that you configure and launch the server before starting the client.</span></span>

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

<span data-ttu-id="d3473-186">Une fois que nous disposons d’une connexion, nous pouvons attend le serveur envoyer des données.</span><span class="sxs-lookup"><span data-stu-id="d3473-186">Once we have a connection, we can wait for the server to send data.</span></span> <span data-ttu-id="d3473-187">Pour cela, nous appelant LoadAsync sur le lecteur de flux de données.</span><span class="sxs-lookup"><span data-stu-id="d3473-187">We do this by calling LoadAsync on the stream data reader.</span></span>

<span data-ttu-id="d3473-188">Le premier jeu d’octets que nous recevons doit toujours être le paquet d’en-tête, ce qui indique le point d’ancrage data stream longueur d’octet comme décrit dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="d3473-188">The first set of bytes we receive should always be the header packet, which indicates the anchor data stream byte length as described in the previous section.</span></span>

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

<span data-ttu-id="d3473-189">...</span><span class="sxs-lookup"><span data-stu-id="d3473-189">...</span></span>

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

<span data-ttu-id="d3473-190">Une fois que nous avons bien reçu le paquet d’en-tête, nous savons combien d’octets de données de point d’ancrage nous devons nous attendre.</span><span class="sxs-lookup"><span data-stu-id="d3473-190">After we have received the header packet, we know how many bytes of anchor data we should expect.</span></span> <span data-ttu-id="d3473-191">Nous pouvons passer à lire ces octets dans le flux.</span><span class="sxs-lookup"><span data-stu-id="d3473-191">We can proceed to read those bytes from the stream.</span></span>

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

<span data-ttu-id="d3473-192">Voici notre code pour la réception du flux de données de point d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="d3473-192">Here's our code for receiving the anchor data stream.</span></span> <span data-ttu-id="d3473-193">Là encore, nous chargera tout d’abord les octets à partir du flux ; Cette opération peut prendre un certain temps pour terminer, comme le StreamSocket attend de recevoir cette quantité en octets à partir du réseau.</span><span class="sxs-lookup"><span data-stu-id="d3473-193">Again, we will first load the bytes from the stream; this operation may take some time to complete as the StreamSocket waits to receive that amount of bytes from the network.</span></span>

<span data-ttu-id="d3473-194">Lorsque l’opération de chargement est terminée, nous pouvons lire ce nombre d’octets.</span><span class="sxs-lookup"><span data-stu-id="d3473-194">When the loading operation is complete, we can read that number of bytes.</span></span> <span data-ttu-id="d3473-195">Si nous avons reçu le nombre d’octets qui nous pensons que pour le flux de données de point d’ancrage, nous pouvons continuer et importer les données d’ancrage ; Si ce n’est pas le cas, il doit vous avoir été une sorte d’erreur.</span><span class="sxs-lookup"><span data-stu-id="d3473-195">If we received the number of bytes that we expect for the anchor data stream, we can go ahead and import the anchor data; if not, there must have been some sort of error.</span></span> <span data-ttu-id="d3473-196">Par exemple, cela peut se produire lorsque l’instance de serveur se termine avant de pouvoir terminer envoyant le flux de données ou le réseau tombe en panne avant que le flux de données entier peut être reçu par le client.</span><span class="sxs-lookup"><span data-stu-id="d3473-196">For example, this can happen when the server instance terminates before it can finish sending the data stream, or the network goes down before the entire data stream can be received by the client.</span></span>

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

<span data-ttu-id="d3473-197">Là encore, nous devons être préparés à gérer les erreurs de réseau inconnue.</span><span class="sxs-lookup"><span data-stu-id="d3473-197">Again, we must be prepared to handle unknown network errors.</span></span>

```
void SampleAnchorTcpClient::HandleException(Exception^ exception)
{
    std::wstring error = L"Connection error: ";
    error += exception->ToString()->Data();
    error += L"\n";
    OutputDebugString(error.c_str());
}
```

<span data-ttu-id="d3473-198">C’est tout !</span><span class="sxs-lookup"><span data-stu-id="d3473-198">That's it!</span></span> <span data-ttu-id="d3473-199">Maintenant, vous devez disposer de suffisamment d’informations pour essayer de rapprocher les ancres reçus sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="d3473-199">Now, you should have enough information to try locating the anchors received over the network.</span></span> <span data-ttu-id="d3473-200">Là encore, notez que le client doit avoir suffisamment de données suivi visuel de l’espace à trouver le point d’ancrage ; Si elle ne fonctionne pas immédiatement, essayez de vous épargne pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="d3473-200">Again, note that the client must have enough visual tracking data for the space to successfully locate the anchor; if it doesn't work right away, try walking around for a while.</span></span> <span data-ttu-id="d3473-201">Si cela ne fonctionne toujours pas, que le serveur envoyer plusieurs points d’ancrage et utiliser des communications réseau se pour accorder sur une solution qui fonctionne pour le client.</span><span class="sxs-lookup"><span data-stu-id="d3473-201">If it still doesn't work, have the server send more anchors, and use network communications to agree on one that works for the client.</span></span> <span data-ttu-id="d3473-202">Vous pouvez tester cela en téléchargeant le HolographicSpatialAnchorTransferSample, configuration de votre client et les adresses IP de serveur et déployez-le sur des appareils HoloLens client et serveur.</span><span class="sxs-lookup"><span data-stu-id="d3473-202">You can try this out by downloading the HolographicSpatialAnchorTransferSample, configuring your client and server IPs, and deploying it to client and server HoloLens devices.</span></span>

## <a name="see-also"></a><span data-ttu-id="d3473-203">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d3473-203">See also</span></span>
* [<span data-ttu-id="d3473-204">Bibliothèque de modèles parallèles (PPL)</span><span class="sxs-lookup"><span data-stu-id="d3473-204">Parallel Patterns Library (PPL)</span></span>](https://msdn.microsoft.com/library/dd492418.aspx)
* [<span data-ttu-id="d3473-205">Windows.Networking.StreamSocket</span><span class="sxs-lookup"><span data-stu-id="d3473-205">Windows.Networking.StreamSocket</span></span>](https://msdn.microsoft.com/library/windows/apps/windows.networking.sockets.streamsocket.aspx)
* [<span data-ttu-id="d3473-206">Windows.Networking.StreamSocketListener</span><span class="sxs-lookup"><span data-stu-id="d3473-206">Windows.Networking.StreamSocketListener</span></span>](https://msdn.microsoft.com/library/windows/apps/windows.networking.sockets.streamsocketlistener.aspx)
