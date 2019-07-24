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
# <a name="local-anchor-transfers-in-unity"></a>Transferts d’ancrage locaux dans Unity

Dans les situations où vous ne pouvez pas utiliser les <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres spatiales Azure</a>, les transferts d’ancrage locaux permettent à un appareil hololens d’exporter une ancre à importer par un deuxième appareil hololens.

>[!NOTE]
>Les transferts d’ancrage locaux fournissent un rappel d’ancrage moins fiable que les <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres spatiales Azure</a>, et les appareils iOS et Android ne sont pas pris en charge par cette approche.

### <a name="setting-the-spatialperception-capability"></a>Définition de la fonctionnalité SpatialPerception

Pour qu’une application puisse transférer des ancres spatiales, la capacité *SpatialPerception* doit être activée.

Comment activer la fonctionnalité *SpatialPerception* :
1. Dans l’éditeur Unity, ouvrez le volet **«paramètres du lecteur»** (modifier > paramètres du projet > Player)
2. Cliquer sur l’onglet **«Windows Store»**
3. Développez **«paramètres de publication»** et cochez la fonctionnalité **«SpatialPerception»** dans la liste **«fonctionnalités»** .

>[!NOTE]
>Si vous avez déjà exporté votre projet Unity vers une solution Visual Studio, vous devez l’exporter vers un nouveau dossier ou définir manuellement [cette fonctionnalité dans AppxManifest dans Visual Studio](local-anchor-transfers-in-directx.md#set-up-your-app-to-use-the-spatialperception-capability).

### <a name="anchor-transfer"></a>Transfert d’ancrage

**Espace de noms :** *UnityEngine. XR. WSA. Sharing*<br>
**Type** : *WorldAnchorTransferBatch*

Pour transférer un [WorldAnchor](coordinate-systems-in-unity.md), vous devez établir l’ancre à transférer. L’utilisateur d’un HoloLens balaie son environnement et choisit manuellement ou par programme un point dans l’espace pour être l’ancre de l’expérience partagée. Les données qui représentent ce point peuvent ensuite être sérialisées et transmises aux autres périphériques qui partagent l’expérience. Chaque appareil désérialise ensuite les données d’ancrage et tente de localiser ce point dans l’espace. Pour que le transfert d’ancrage fonctionne, chaque appareil doit avoir effectué une analyse suffisante de l’environnement, de telle sorte que le point représenté par l’ancre puisse être identifié.

### <a name="setup"></a>Installation

L’exemple de code sur cette page contient quelques champs qui devront être initialisés:
1. *Gameobject rootGameObject* est un *gameobject* dans Unity qui contient un composant *WorldAnchor* . Un utilisateur de l’expérience partagée placera ce *gameobject* et exportera les données vers les autres utilisateurs.
2. *WorldAnchor gameRootAnchor* est le *UnityEngine. XR. WSA. WorldAnchor* qui est sur *rootGameObject*.
3. *Byte [] importedData* est un tableau d’octets pour l’ancre sérialisée que chaque client reçoit sur le réseau.

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

### <a name="exporting"></a>Export

Pour exporter, nous avons juste besoin d’un *WorldAnchor* et de savoir ce que nous appelons pour l’application réceptrice. Un client de l’expérience partagée effectue les étapes suivantes pour exporter l’ancre partagée:
1. Créer un *WorldAnchorTransferBatch*
2. Ajouter le *WorldAnchors* à transférer
3. Commencer l’exportation
4. Gérer l’événement *OnExportDataAvailable* à mesure que les données deviennent disponibles
5. Gérer l’événement *OnExportComplete*

Nous créons un *WorldAnchorTransferBatch* pour encapsuler ce que nous allons transférer, puis l’exporter dans octets:

```
private void ExportGameRootAnchor()
{
    WorldAnchorTransferBatch transferBatch = new WorldAnchorTransferBatch();
    transferBatch.AddWorldAnchor("gameRoot", this.gameRootAnchor);
    WorldAnchorTransferBatch.ExportAsync(transferBatch, OnExportDataAvailable, OnExportComplete);
}
```

À mesure que les données deviennent disponibles, envoyez les octets au client ou à la mémoire tampon sous forme de segments de données disponibles et envoyés par n’importe quel moyen souhaité:

```
private void OnExportDataAvailable(byte[] data)
{
    TransferDataToClient(data);
}
```

Une fois l’exportation terminée, si nous avons transféré des données et que la sérialisation a échoué, demandez au client d’ignorer les données. Si la sérialisation a réussi, indiquez au client que toutes les données ont été transférées et que l’importation peut commencer:

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

### <a name="importing"></a>Destination

Après avoir reçu tous les octets de l’expéditeur, nous pouvons réimporter les données dans un *WorldAnchorTransferBatch* et verrouiller notre objet de jeu racine dans le même emplacement physique. Remarque: l’importation peut échouer momentanément et doit être retentée:

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

Une fois qu’un *gameobject* est verrouillé via l’appel *lockobject* , il aura un *WorldAnchor* qui le conservera dans la même position physique dans le monde, mais il peut se trouver à un emplacement différent dans l’espace de coordonnées Unity que d’autres utilisateurs.

