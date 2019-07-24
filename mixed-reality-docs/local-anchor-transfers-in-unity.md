---
title: Transferts d’ancrage locaux dans Unity
description: Transférer des ancres entre plusieurs appareils HoloLens dans une application Unity.
author: fieldsJacksonG
ms.author: jacksonf
ms.date: 03/21/2018
ms.topic: article
keywords: Partage, ancrer, WorldAnchor, m partage 250, WorldAnchorTransferBatch, SpatialPerception, transfert, transfert d’ancrage local, exportation d’ancrage, importation d’ancrage
ms.openlocfilehash: 82bcd07417fd5aa1b265ebc3c8edc939101dd783
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63516139"
---
# <a name="local-anchor-transfers-in-unity"></a><span data-ttu-id="b8021-104">Transferts d’ancrage locaux dans Unity</span><span class="sxs-lookup"><span data-stu-id="b8021-104">Local anchor transfers in Unity</span></span>

<span data-ttu-id="b8021-105">Dans les situations où vous ne pouvez pas utiliser les <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres spatiales Azure</a>, les transferts d’ancrage locaux permettent à un appareil hololens d’exporter une ancre à importer par un deuxième appareil hololens.</span><span class="sxs-lookup"><span data-stu-id="b8021-105">In situations where you cannot use <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>, local anchor transfers enable one HoloLens device to export an anchor to be imported by a second HoloLens device.</span></span>

>[!NOTE]
><span data-ttu-id="b8021-106">Les transferts d’ancrage locaux fournissent un rappel d’ancrage moins fiable que les <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres spatiales Azure</a>, et les appareils iOS et Android ne sont pas pris en charge par cette approche.</span><span class="sxs-lookup"><span data-stu-id="b8021-106">Local anchor transfers provide less robust anchor recall than <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>, and iOS and Android devices are not supported by this approach.</span></span>

### <a name="setting-the-spatialperception-capability"></a><span data-ttu-id="b8021-107">Définition de la fonctionnalité SpatialPerception</span><span class="sxs-lookup"><span data-stu-id="b8021-107">Setting the SpatialPerception capability</span></span>

<span data-ttu-id="b8021-108">Pour qu’une application puisse transférer des ancres spatiales, la capacité *SpatialPerception* doit être activée.</span><span class="sxs-lookup"><span data-stu-id="b8021-108">In order for an app to transfer spatial anchors, the *SpatialPerception* capability must be enabled.</span></span>

<span data-ttu-id="b8021-109">Comment activer la fonctionnalité *SpatialPerception* :</span><span class="sxs-lookup"><span data-stu-id="b8021-109">How to enable the *SpatialPerception* capability:</span></span>
1. <span data-ttu-id="b8021-110">Dans l’éditeur Unity, ouvrez le volet **«paramètres du lecteur»** (modifier > paramètres du projet > Player)</span><span class="sxs-lookup"><span data-stu-id="b8021-110">In the Unity Editor, open the **"Player Settings"** pane (Edit > Project Settings > Player)</span></span>
2. <span data-ttu-id="b8021-111">Cliquer sur l’onglet **«Windows Store»**</span><span class="sxs-lookup"><span data-stu-id="b8021-111">Click on the **"Windows Store"** tab</span></span>
3. <span data-ttu-id="b8021-112">Développez **«paramètres de publication»** et cochez la fonctionnalité **«SpatialPerception»** dans la liste **«fonctionnalités»** .</span><span class="sxs-lookup"><span data-stu-id="b8021-112">Expand **"Publishing Settings"** and check the **"SpatialPerception"** capability in the **"Capabilities"** list</span></span>

>[!NOTE]
><span data-ttu-id="b8021-113">Si vous avez déjà exporté votre projet Unity vers une solution Visual Studio, vous devez l’exporter vers un nouveau dossier ou définir manuellement [cette fonctionnalité dans AppxManifest dans Visual Studio](local-anchor-transfers-in-directx.md#set-up-your-app-to-use-the-spatialperception-capability).</span><span class="sxs-lookup"><span data-stu-id="b8021-113">If you have already exported your Unity project to a Visual Studio solution, you will need to either export to a new folder or manually [set this capability in the AppxManifest in Visual Studio](local-anchor-transfers-in-directx.md#set-up-your-app-to-use-the-spatialperception-capability).</span></span>

### <a name="anchor-transfer"></a><span data-ttu-id="b8021-114">Transfert d’ancrage</span><span class="sxs-lookup"><span data-stu-id="b8021-114">Anchor Transfer</span></span>

<span data-ttu-id="b8021-115">**Espace de noms :** *UnityEngine. XR. WSA. Sharing*</span><span class="sxs-lookup"><span data-stu-id="b8021-115">**Namespace:** *UnityEngine.XR.WSA.Sharing*</span></span><br>
<span data-ttu-id="b8021-116">**Type** : *WorldAnchorTransferBatch*</span><span class="sxs-lookup"><span data-stu-id="b8021-116">**Type**: *WorldAnchorTransferBatch*</span></span>

<span data-ttu-id="b8021-117">Pour transférer un [WorldAnchor](coordinate-systems-in-unity.md), vous devez établir l’ancre à transférer.</span><span class="sxs-lookup"><span data-stu-id="b8021-117">To transfer a [WorldAnchor](coordinate-systems-in-unity.md), one must establish the anchor to be transferred.</span></span> <span data-ttu-id="b8021-118">L’utilisateur d’un HoloLens balaie son environnement et choisit manuellement ou par programme un point dans l’espace pour être l’ancre de l’expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="b8021-118">The user of one HoloLens scans their environment and either manually or programmatically chooses a point in space to be the Anchor for the shared experience.</span></span> <span data-ttu-id="b8021-119">Les données qui représentent ce point peuvent ensuite être sérialisées et transmises aux autres périphériques qui partagent l’expérience.</span><span class="sxs-lookup"><span data-stu-id="b8021-119">The data that represents this point can then be serialized and transmitted to the other devices that are sharing in the experience.</span></span> <span data-ttu-id="b8021-120">Chaque appareil désérialise ensuite les données d’ancrage et tente de localiser ce point dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="b8021-120">Each device then de-serializes the anchor data and attempts to locate that point in space.</span></span> <span data-ttu-id="b8021-121">Pour que le transfert d’ancrage fonctionne, chaque appareil doit avoir effectué une analyse suffisante de l’environnement, de telle sorte que le point représenté par l’ancre puisse être identifié.</span><span class="sxs-lookup"><span data-stu-id="b8021-121">In order for Anchor Transfer to work, each device must have scanned in enough of the environment such that the point represented by the anchor can be identified.</span></span>

### <a name="setup"></a><span data-ttu-id="b8021-122">Installation</span><span class="sxs-lookup"><span data-stu-id="b8021-122">Setup</span></span>

<span data-ttu-id="b8021-123">L’exemple de code sur cette page contient quelques champs qui devront être initialisés:</span><span class="sxs-lookup"><span data-stu-id="b8021-123">The sample code on this page has a few fields that will need to be initialized:</span></span>
1. <span data-ttu-id="b8021-124">*Gameobject rootGameObject* est un *gameobject* dans Unity qui contient un composant *WorldAnchor* .</span><span class="sxs-lookup"><span data-stu-id="b8021-124">*GameObject rootGameObject* is a *GameObject* in Unity that has a *WorldAnchor* Component on it.</span></span> <span data-ttu-id="b8021-125">Un utilisateur de l’expérience partagée placera ce *gameobject* et exportera les données vers les autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b8021-125">One user in the shared experience will place this *GameObject* and export the data to the other users.</span></span>
2. <span data-ttu-id="b8021-126">*WorldAnchor gameRootAnchor* est le *UnityEngine. XR. WSA. WorldAnchor* qui est sur *rootGameObject*.</span><span class="sxs-lookup"><span data-stu-id="b8021-126">*WorldAnchor gameRootAnchor* is the *UnityEngine.XR.WSA.WorldAnchor* that is on *rootGameObject*.</span></span>
3. <span data-ttu-id="b8021-127">*Byte [] importedData* est un tableau d’octets pour l’ancre sérialisée que chaque client reçoit sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="b8021-127">*byte[] importedData* is a byte array for the serialized anchor each client is receiving over the network.</span></span>

```
public GameObject rootGameObject;
private UnityEngine.XR.WSA.WorldAnchor gameRootAnchor;

void Start ()
{
    gameRootAnchor = rootGameObject.GetComponent<UnityEngine.XR.WSA.WorldAnchor>();

    if (gameRootAnchor == null)
    {
        gameRootAnchor = rootGameObject.AddComponent<UnityEngine.XR.WSA.WorldAnchor>();
    }
}
```

### <a name="exporting"></a><span data-ttu-id="b8021-128">Export</span><span class="sxs-lookup"><span data-stu-id="b8021-128">Exporting</span></span>

<span data-ttu-id="b8021-129">Pour exporter, nous avons juste besoin d’un *WorldAnchor* et de savoir ce que nous appelons pour l’application réceptrice.</span><span class="sxs-lookup"><span data-stu-id="b8021-129">To export, we just need a *WorldAnchor* and to know what we will call it such that it makes sense for the receiving app.</span></span> <span data-ttu-id="b8021-130">Un client de l’expérience partagée effectue les étapes suivantes pour exporter l’ancre partagée:</span><span class="sxs-lookup"><span data-stu-id="b8021-130">One client in the shared experience will perform these steps to export the shared anchor:</span></span>
1. <span data-ttu-id="b8021-131">Créer un *WorldAnchorTransferBatch*</span><span class="sxs-lookup"><span data-stu-id="b8021-131">Create a *WorldAnchorTransferBatch*</span></span>
2. <span data-ttu-id="b8021-132">Ajouter le *WorldAnchors* à transférer</span><span class="sxs-lookup"><span data-stu-id="b8021-132">Add the *WorldAnchors* to transfer</span></span>
3. <span data-ttu-id="b8021-133">Commencer l’exportation</span><span class="sxs-lookup"><span data-stu-id="b8021-133">Begin the export</span></span>
4. <span data-ttu-id="b8021-134">Gérer l’événement *OnExportDataAvailable* à mesure que les données deviennent disponibles</span><span class="sxs-lookup"><span data-stu-id="b8021-134">Handle the *OnExportDataAvailable* event as data becomes available</span></span>
5. <span data-ttu-id="b8021-135">Gérer l’événement *OnExportComplete*</span><span class="sxs-lookup"><span data-stu-id="b8021-135">Handle the *OnExportComplete* event</span></span>

<span data-ttu-id="b8021-136">Nous créons un *WorldAnchorTransferBatch* pour encapsuler ce que nous allons transférer, puis l’exporter dans octets:</span><span class="sxs-lookup"><span data-stu-id="b8021-136">We create a *WorldAnchorTransferBatch* to encapsulate what we will be transferring and then export that into bytes:</span></span>

```
private void ExportGameRootAnchor()
{
    WorldAnchorTransferBatch transferBatch = new WorldAnchorTransferBatch();
    transferBatch.AddWorldAnchor("gameRoot", this.gameRootAnchor);
    WorldAnchorTransferBatch.ExportAsync(transferBatch, OnExportDataAvailable, OnExportComplete);
}
```

<span data-ttu-id="b8021-137">À mesure que les données deviennent disponibles, envoyez les octets au client ou à la mémoire tampon sous forme de segments de données disponibles et envoyés par n’importe quel moyen souhaité:</span><span class="sxs-lookup"><span data-stu-id="b8021-137">As data becomes available, send the bytes to the client or buffer as segments of data is available and send through whatever means desired:</span></span>

```
private void OnExportDataAvailable(byte[] data)
{
    TransferDataToClient(data);
}
```

<span data-ttu-id="b8021-138">Une fois l’exportation terminée, si nous avons transféré des données et que la sérialisation a échoué, demandez au client d’ignorer les données.</span><span class="sxs-lookup"><span data-stu-id="b8021-138">Once the export is complete, if we have been transferring data and serialization failed, tell the client to discard the data.</span></span> <span data-ttu-id="b8021-139">Si la sérialisation a réussi, indiquez au client que toutes les données ont été transférées et que l’importation peut commencer:</span><span class="sxs-lookup"><span data-stu-id="b8021-139">If the serialization succeeded, tell the client that all data has been transferred and importing can start:</span></span>

```
private void OnExportComplete(SerializationCompletionReason completionReason)
{
    if (completionReason != SerializationCompletionReason.Succeeded)
    {
        SendExportFailedToClient();
    }
    else
    {
        SendExportSucceededToClient();
    }
}
```

### <a name="importing"></a><span data-ttu-id="b8021-140">Destination</span><span class="sxs-lookup"><span data-stu-id="b8021-140">Importing</span></span>

<span data-ttu-id="b8021-141">Après avoir reçu tous les octets de l’expéditeur, nous pouvons réimporter les données dans un *WorldAnchorTransferBatch* et verrouiller notre objet de jeu racine dans le même emplacement physique.</span><span class="sxs-lookup"><span data-stu-id="b8021-141">After receiving all of the bytes from the sender, we can import the data back into a *WorldAnchorTransferBatch* and lock our root game object into the same physical location.</span></span> <span data-ttu-id="b8021-142">Remarque: l’importation peut échouer momentanément et doit être retentée:</span><span class="sxs-lookup"><span data-stu-id="b8021-142">Note: import will sometimes transiently fail and needs to be retried:</span></span>

```
// This byte array should have been updated over the network from TransferDataToClient
private byte[] importedData;
private int retryCount = 3;

private void ImportRootGameObject()
{
    WorldAnchorTransferBatch.ImportAsync(importedData, OnImportComplete);
}

private void OnImportComplete(SerializationCompletionReason completionReason, WorldAnchorTransferBatch deserializedTransferBatch)
{
    if (completionReason != SerializationCompletionReason.Succeeded)
    {
        Debug.Log("Failed to import: " + completionReason.ToString());
        if (retryCount > 0)
        {
            retryCount--;
            WorldAnchorTransferBatch.ImportAsync(importedData, OnImportComplete);
        }
        return;
    }

    this.gameRootAnchor = deserializedTransferBatch.LockObject("gameRoot", this.rootGameObject);
}
```

<span data-ttu-id="b8021-143">Une fois qu’un *gameobject* est verrouillé via l’appel *lockobject* , il aura un *WorldAnchor* qui le conservera dans la même position physique dans le monde, mais il peut se trouver à un emplacement différent dans l’espace de coordonnées Unity que d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b8021-143">After a *GameObject* is locked via the *LockObject* call, it will have a *WorldAnchor* which will keep it in the same physical position in the world, but it may be at a different location in the Unity coordinate space than other users.</span></span>

