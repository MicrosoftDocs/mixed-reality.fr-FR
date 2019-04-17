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
# <a name="local-anchor-transfers-in-unity"></a>Transferts d’ancrage local dans Unity

Dans les situations où vous ne pouvez pas utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres Spatial Azure</a>, les transferts d’ancrage local activer un appareil HoloLens exporter un point d’ancrage doivent être importées par un deuxième appareil HoloLens.

>[!NOTE]
>Les transferts d’ancrage local fournissent moins fiable rappel d’ancrage que <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres Spatial Azure</a>, et les appareils iOS et Android ne sont pas pris en charge par cette approche.

### <a name="setting-the-spatialperception-capability"></a>Définition de la fonctionnalité SpatialPerception

Dans l’ordre pour une application à transférer des ancres spatiales, le *SpatialPerception* fonctionnalité doit être activée.

Comment activer la *SpatialPerception* fonctionnalité :
1. Dans l’éditeur Unity, ouvrez le **« Paramètres du lecteur »** volet (Modifier > Paramètres du projet > lecteur)
2. Cliquez sur le **« Windows Store »** onglet
3. Développez **« Paramètres de publication »** et vérifiez le **« SpatialPerception »** fonctionnalité dans le **« Fonctionnalités »** liste

>[!NOTE]
>Si vous avez déjà exporté votre projet Unity à une solution Visual Studio, vous devrez soit exporter vers un nouveau dossier ou manuellement [définir cette fonctionnalité dans le fichier AppxManifest dans Visual Studio](local-anchor-transfers-in-directx.md#set-up-your-app-to-use-the-spatialperception-capability).

### <a name="anchor-transfer"></a>Transfert de point d’ancrage

**Namespace :** *UnityEngine.XR.WSA.Sharing*<br>
**Type** : *WorldAnchorTransferBatch*

Pour transférer un [WorldAnchor](coordinate-systems-in-unity.md), un doit établir le point d’ancrage à transférer. L’utilisateur d’une HoloLens analyse de leur environnement et manuellement ou par programmation choisit un point dans l’espace pour être le point d’ancrage pour l’expérience partagée. Les données qui représente ce point puis pouvant être sérialisées et transmises aux autres appareils qui sont dans l’expérience de partage. Chaque appareil puis désérialise les données d’ancrage et tente de localiser ce point dans l’espace. Dans l’ordre pour le transfert de point d’ancrage travailler, chaque appareil doit ont analysés suffisamment de l’environnement telles que le point représenté par le point d’ancrage peut être identifié.

### <a name="setup"></a>Installation

L’exemple de code sur cette page présente quelques champs qui devront être initialisé :
1. *GameObject rootGameObject* est un *GameObject* dans Unity a un *WorldAnchor* composant dessus. Un seul utilisateur dans l’expérience partagée placera cela *GameObject* et exporter les données vers les autres utilisateurs.
2. *WorldAnchor gameRootAnchor* est la *UnityEngine.XR.WSA.WorldAnchor* qui se trouve sur *rootGameObject*.
3. *Byte [] importedData* est un tableau d’octets pour le point d’ancrage sérialisée chaque client reçoit via le réseau.

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

### <a name="exporting"></a>Exportation

Pour exporter, il nous reste un *WorldAnchor* et savoir ce que nous appellerons tel qu’il est judicieux pour l’application de réception. Un client dans l’expérience partagée va effectuer ces étapes pour exporter le point d’ancrage partagé :
1. Créer un *WorldAnchorTransferBatch*
2. Ajouter le *WorldAnchors* à transférer
3. Commencer l’exportation
4. Gérer le *OnExportDataAvailable* événement sous forme de données devient disponible
5. Gérer le *OnExportComplete* événement

Nous créons un *WorldAnchorTransferBatch* pour encapsuler ce que nous seront transfert et puis de l’exporter en octets :

```
private void ExportGameRootAnchor()
{
    WorldAnchorTransferBatch transferBatch = new WorldAnchorTransferBatch();
    transferBatch.AddWorldAnchor("gameRoot", this.gameRootAnchor);
    WorldAnchorTransferBatch.ExportAsync(transferBatch, OnExportDataAvailable, OnExportComplete);
}
```

Comme les données deviennent disponibles, les octets d’envoi au client ou de la mémoire tampon comme segments de données est disponible et envoyer par quelque moyen que vous le souhaitez :

```
private void OnExportDataAvailable(byte[] data)
{
    TransferDataToClient(data);
}
```

Une fois l’exportation terminée, si nous avons été transfert de données et la sérialisation a échoué, indiquent au client d’ignorer les données. Si la sérialisation a réussi, indiquent au client que toutes les données ont été transférées et l’importation peut commencer :

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

### <a name="importing"></a>L’importation

Après avoir reçu tous les octets à partir de l’expéditeur, nous pouvons importer les données dans un *WorldAnchorTransferBatch* et verrouiller notre objet de jeu de racine dans le même emplacement physique. Remarque : l’importation échoue parfois de manière transitoire et doit être retentée :

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

Après un *GameObject* est verrouillé par le biais de la *LockObject* appel, il aura un *WorldAnchor* qui sera le conserver dans la même position physique dans le monde, mais il peut être à un autre emplacement dans Unity coordonner d’espace que d’autres utilisateurs.

