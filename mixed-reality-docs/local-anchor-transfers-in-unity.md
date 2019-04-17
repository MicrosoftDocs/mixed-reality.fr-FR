---
title: Transferts d’ancrage local dans Unity
description: Transférer des ancres entre plusieurs appareils HoloLens dans une application Unity.
author: fieldsJacksonG
ms.author: jacksonf
ms.date: 03/21/2018
ms.topic: article
keywords: Partage, d’ancrage, WorldAnchor, MR partage 250, WorldAnchorTransferBatch, SpatialPerception, transfert, transfert de local d’ancrage, exportation de point d’ancrage, importation de point d’ancrage
ms.openlocfilehash: 82bcd07417fd5aa1b265ebc3c8edc939101dd783
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597108"
---
# <a name="local-anchor-transfers-in-unity"></a><span data-ttu-id="6fe57-104">Transferts d’ancrage local dans Unity</span><span class="sxs-lookup"><span data-stu-id="6fe57-104">Local anchor transfers in Unity</span></span>

<span data-ttu-id="6fe57-105">Dans les situations où vous ne pouvez pas utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres Spatial Azure</a>, les transferts d’ancrage local activer un appareil HoloLens exporter un point d’ancrage doivent être importées par un deuxième appareil HoloLens.</span><span class="sxs-lookup"><span data-stu-id="6fe57-105">In situations where you cannot use <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>, local anchor transfers enable one HoloLens device to export an anchor to be imported by a second HoloLens device.</span></span>

>[!NOTE]
><span data-ttu-id="6fe57-106">Les transferts d’ancrage local fournissent moins fiable rappel d’ancrage que <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres Spatial Azure</a>, et les appareils iOS et Android ne sont pas pris en charge par cette approche.</span><span class="sxs-lookup"><span data-stu-id="6fe57-106">Local anchor transfers provide less robust anchor recall than <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>, and iOS and Android devices are not supported by this approach.</span></span>

### <a name="setting-the-spatialperception-capability"></a><span data-ttu-id="6fe57-107">Définition de la fonctionnalité SpatialPerception</span><span class="sxs-lookup"><span data-stu-id="6fe57-107">Setting the SpatialPerception capability</span></span>

<span data-ttu-id="6fe57-108">Dans l’ordre pour une application à transférer des ancres spatiales, le *SpatialPerception* fonctionnalité doit être activée.</span><span class="sxs-lookup"><span data-stu-id="6fe57-108">In order for an app to transfer spatial anchors, the *SpatialPerception* capability must be enabled.</span></span>

<span data-ttu-id="6fe57-109">Comment activer la *SpatialPerception* fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="6fe57-109">How to enable the *SpatialPerception* capability:</span></span>
1. <span data-ttu-id="6fe57-110">Dans l’éditeur Unity, ouvrez le **« Paramètres du lecteur »** volet (Modifier > Paramètres du projet > lecteur)</span><span class="sxs-lookup"><span data-stu-id="6fe57-110">In the Unity Editor, open the **"Player Settings"** pane (Edit > Project Settings > Player)</span></span>
2. <span data-ttu-id="6fe57-111">Cliquez sur le **« Windows Store »** onglet</span><span class="sxs-lookup"><span data-stu-id="6fe57-111">Click on the **"Windows Store"** tab</span></span>
3. <span data-ttu-id="6fe57-112">Développez **« Paramètres de publication »** et vérifiez le **« SpatialPerception »** fonctionnalité dans le **« Fonctionnalités »** liste</span><span class="sxs-lookup"><span data-stu-id="6fe57-112">Expand **"Publishing Settings"** and check the **"SpatialPerception"** capability in the **"Capabilities"** list</span></span>

>[!NOTE]
><span data-ttu-id="6fe57-113">Si vous avez déjà exporté votre projet Unity à une solution Visual Studio, vous devrez soit exporter vers un nouveau dossier ou manuellement [définir cette fonctionnalité dans le fichier AppxManifest dans Visual Studio](local-anchor-transfers-in-directx.md#set-up-your-app-to-use-the-spatialperception-capability).</span><span class="sxs-lookup"><span data-stu-id="6fe57-113">If you have already exported your Unity project to a Visual Studio solution, you will need to either export to a new folder or manually [set this capability in the AppxManifest in Visual Studio](local-anchor-transfers-in-directx.md#set-up-your-app-to-use-the-spatialperception-capability).</span></span>

### <a name="anchor-transfer"></a><span data-ttu-id="6fe57-114">Transfert de point d’ancrage</span><span class="sxs-lookup"><span data-stu-id="6fe57-114">Anchor Transfer</span></span>

<span data-ttu-id="6fe57-115">**Namespace :** *UnityEngine.XR.WSA.Sharing*</span><span class="sxs-lookup"><span data-stu-id="6fe57-115">**Namespace:** *UnityEngine.XR.WSA.Sharing*</span></span><br>
<span data-ttu-id="6fe57-116">**Type** : *WorldAnchorTransferBatch*</span><span class="sxs-lookup"><span data-stu-id="6fe57-116">**Type**: *WorldAnchorTransferBatch*</span></span>

<span data-ttu-id="6fe57-117">Pour transférer un [WorldAnchor](coordinate-systems-in-unity.md), un doit établir le point d’ancrage à transférer.</span><span class="sxs-lookup"><span data-stu-id="6fe57-117">To transfer a [WorldAnchor](coordinate-systems-in-unity.md), one must establish the anchor to be transferred.</span></span> <span data-ttu-id="6fe57-118">L’utilisateur d’une HoloLens analyse de leur environnement et manuellement ou par programmation choisit un point dans l’espace pour être le point d’ancrage pour l’expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="6fe57-118">The user of one HoloLens scans their environment and either manually or programmatically chooses a point in space to be the Anchor for the shared experience.</span></span> <span data-ttu-id="6fe57-119">Les données qui représente ce point puis pouvant être sérialisées et transmises aux autres appareils qui sont dans l’expérience de partage.</span><span class="sxs-lookup"><span data-stu-id="6fe57-119">The data that represents this point can then be serialized and transmitted to the other devices that are sharing in the experience.</span></span> <span data-ttu-id="6fe57-120">Chaque appareil puis désérialise les données d’ancrage et tente de localiser ce point dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="6fe57-120">Each device then de-serializes the anchor data and attempts to locate that point in space.</span></span> <span data-ttu-id="6fe57-121">Dans l’ordre pour le transfert de point d’ancrage travailler, chaque appareil doit ont analysés suffisamment de l’environnement telles que le point représenté par le point d’ancrage peut être identifié.</span><span class="sxs-lookup"><span data-stu-id="6fe57-121">In order for Anchor Transfer to work, each device must have scanned in enough of the environment such that the point represented by the anchor can be identified.</span></span>

### <a name="setup"></a><span data-ttu-id="6fe57-122">Installation</span><span class="sxs-lookup"><span data-stu-id="6fe57-122">Setup</span></span>

<span data-ttu-id="6fe57-123">L’exemple de code sur cette page présente quelques champs qui devront être initialisé :</span><span class="sxs-lookup"><span data-stu-id="6fe57-123">The sample code on this page has a few fields that will need to be initialized:</span></span>
1. <span data-ttu-id="6fe57-124">*GameObject rootGameObject* est un *GameObject* dans Unity a un *WorldAnchor* composant dessus.</span><span class="sxs-lookup"><span data-stu-id="6fe57-124">*GameObject rootGameObject* is a *GameObject* in Unity that has a *WorldAnchor* Component on it.</span></span> <span data-ttu-id="6fe57-125">Un seul utilisateur dans l’expérience partagée placera cela *GameObject* et exporter les données vers les autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6fe57-125">One user in the shared experience will place this *GameObject* and export the data to the other users.</span></span>
2. <span data-ttu-id="6fe57-126">*WorldAnchor gameRootAnchor* est la *UnityEngine.XR.WSA.WorldAnchor* qui se trouve sur *rootGameObject*.</span><span class="sxs-lookup"><span data-stu-id="6fe57-126">*WorldAnchor gameRootAnchor* is the *UnityEngine.XR.WSA.WorldAnchor* that is on *rootGameObject*.</span></span>
3. <span data-ttu-id="6fe57-127">*Byte [] importedData* est un tableau d’octets pour le point d’ancrage sérialisée chaque client reçoit via le réseau.</span><span class="sxs-lookup"><span data-stu-id="6fe57-127">*byte[] importedData* is a byte array for the serialized anchor each client is receiving over the network.</span></span>

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

### <a name="exporting"></a><span data-ttu-id="6fe57-128">Exportation</span><span class="sxs-lookup"><span data-stu-id="6fe57-128">Exporting</span></span>

<span data-ttu-id="6fe57-129">Pour exporter, il nous reste un *WorldAnchor* et savoir ce que nous appellerons tel qu’il est judicieux pour l’application de réception.</span><span class="sxs-lookup"><span data-stu-id="6fe57-129">To export, we just need a *WorldAnchor* and to know what we will call it such that it makes sense for the receiving app.</span></span> <span data-ttu-id="6fe57-130">Un client dans l’expérience partagée va effectuer ces étapes pour exporter le point d’ancrage partagé :</span><span class="sxs-lookup"><span data-stu-id="6fe57-130">One client in the shared experience will perform these steps to export the shared anchor:</span></span>
1. <span data-ttu-id="6fe57-131">Créer un *WorldAnchorTransferBatch*</span><span class="sxs-lookup"><span data-stu-id="6fe57-131">Create a *WorldAnchorTransferBatch*</span></span>
2. <span data-ttu-id="6fe57-132">Ajouter le *WorldAnchors* à transférer</span><span class="sxs-lookup"><span data-stu-id="6fe57-132">Add the *WorldAnchors* to transfer</span></span>
3. <span data-ttu-id="6fe57-133">Commencer l’exportation</span><span class="sxs-lookup"><span data-stu-id="6fe57-133">Begin the export</span></span>
4. <span data-ttu-id="6fe57-134">Gérer le *OnExportDataAvailable* événement sous forme de données devient disponible</span><span class="sxs-lookup"><span data-stu-id="6fe57-134">Handle the *OnExportDataAvailable* event as data becomes available</span></span>
5. <span data-ttu-id="6fe57-135">Gérer le *OnExportComplete* événement</span><span class="sxs-lookup"><span data-stu-id="6fe57-135">Handle the *OnExportComplete* event</span></span>

<span data-ttu-id="6fe57-136">Nous créons un *WorldAnchorTransferBatch* pour encapsuler ce que nous seront transfert et puis de l’exporter en octets :</span><span class="sxs-lookup"><span data-stu-id="6fe57-136">We create a *WorldAnchorTransferBatch* to encapsulate what we will be transferring and then export that into bytes:</span></span>

```
private void ExportGameRootAnchor()
{
    WorldAnchorTransferBatch transferBatch = new WorldAnchorTransferBatch();
    transferBatch.AddWorldAnchor("gameRoot", this.gameRootAnchor);
    WorldAnchorTransferBatch.ExportAsync(transferBatch, OnExportDataAvailable, OnExportComplete);
}
```

<span data-ttu-id="6fe57-137">Comme les données deviennent disponibles, les octets d’envoi au client ou de la mémoire tampon comme segments de données est disponible et envoyer par quelque moyen que vous le souhaitez :</span><span class="sxs-lookup"><span data-stu-id="6fe57-137">As data becomes available, send the bytes to the client or buffer as segments of data is available and send through whatever means desired:</span></span>

```
private void OnExportDataAvailable(byte[] data)
{
    TransferDataToClient(data);
}
```

<span data-ttu-id="6fe57-138">Une fois l’exportation terminée, si nous avons été transfert de données et la sérialisation a échoué, indiquent au client d’ignorer les données.</span><span class="sxs-lookup"><span data-stu-id="6fe57-138">Once the export is complete, if we have been transferring data and serialization failed, tell the client to discard the data.</span></span> <span data-ttu-id="6fe57-139">Si la sérialisation a réussi, indiquent au client que toutes les données ont été transférées et l’importation peut commencer :</span><span class="sxs-lookup"><span data-stu-id="6fe57-139">If the serialization succeeded, tell the client that all data has been transferred and importing can start:</span></span>

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

### <a name="importing"></a><span data-ttu-id="6fe57-140">L’importation</span><span class="sxs-lookup"><span data-stu-id="6fe57-140">Importing</span></span>

<span data-ttu-id="6fe57-141">Après avoir reçu tous les octets à partir de l’expéditeur, nous pouvons importer les données dans un *WorldAnchorTransferBatch* et verrouiller notre objet de jeu de racine dans le même emplacement physique.</span><span class="sxs-lookup"><span data-stu-id="6fe57-141">After receiving all of the bytes from the sender, we can import the data back into a *WorldAnchorTransferBatch* and lock our root game object into the same physical location.</span></span> <span data-ttu-id="6fe57-142">Remarque : l’importation échoue parfois de manière transitoire et doit être retentée :</span><span class="sxs-lookup"><span data-stu-id="6fe57-142">Note: import will sometimes transiently fail and needs to be retried:</span></span>

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

<span data-ttu-id="6fe57-143">Après un *GameObject* est verrouillé par le biais de la *LockObject* appel, il aura un *WorldAnchor* qui sera le conserver dans la même position physique dans le monde, mais il peut être à un autre emplacement dans Unity coordonner d’espace que d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6fe57-143">After a *GameObject* is locked via the *LockObject* call, it will have a *WorldAnchor* which will keep it in the same physical position in the world, but it may be at a different location in the Unity coordinate space than other users.</span></span>

