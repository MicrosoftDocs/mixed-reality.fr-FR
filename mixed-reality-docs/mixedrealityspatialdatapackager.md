---
title: Documentation du package de données spatiales de la réalité mixte
description: Documentation sur l’utilisation d’un package de données spatiales de réalité mixte
author: alfred-msft
ms.author: alreynol
ms.date: 05/16/2019
ms.topic: article
keywords: LBE, MixedRealitySpatialDataPackager. exe, MixedRealitySpatialDataPackager
ms.openlocfilehash: 331fa6dc752c64eeaa5bc2e9d1dd6b2c15049a27
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926758"
---
# <a name="mixed-reality-spatial-data-packager-documentation"></a>Documentation du package de données spatiales de la réalité mixte

>[!NOTE]
> Cet outil et son fonctionnement sont proposés tels quels. Elle est sujette à modification sans aucun préavis et peut ne pas être compatible avec les futures versions de Windows ou de Windows Mixed Reality HMD.

## <a name="download"></a>Télécharger
 Téléchargez [MixedRealitySpatialDataPackager ici](https://download.microsoft.com/download/A/1/2/A12B8A90-B3F7-4ED9-A4BB-D59DDCDAA125/MixedRealitySpatialDataPackager.zip)

## <a name="device-support"></a>Périphériques pris en charge

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Package de données spatiales de réalité mixte</td>
        <td>❌</td>
        <td>❌</td>
        <td>✔️</td>
    </tr>
</table>

## <a name="quickstart"></a>Didacticiel

L’outil mélangeur de données spatiales de réalité mixte copie les données spatiales d’une application cible d’un ordinateur vers un autre à l’aide d’un processus d’exportation et d’importation en deux étapes. L’outil doit être exécuté avec des privilèges d’administrateur et supprimer les données spatiales existantes lors de l’importation. L’exportation laisse les données spatiales existantes intactes.

Principales exigences et limitations :

1. L’outil doit être exécuté avec des privilèges d’administrateur 
2. Vous devrez peut-être redémarrer le PC si le portail de réalité mixte est instable après l’exécution de l’outil
3. L’outil ne s’exécute pas quand des incompatibilités ou des incompatibilités de version de données spatiales sont rencontrées
4. L’outil efface les données spatiales existantes lors de l’importation
5. En cas d’échec du processus d’importation, les données précédentes ne peuvent pas être restaurées, sauf si elles ont été sauvegardées en l’exportant précédemment
6. La qualité de la fonctionnalité d’importation est subordonné au mode « lecture seule » pour les données cartographiques spatiales
***

## <a name="mapping-best-practices"></a>Meilleures pratiques de mappage

1. Effacer les mappages existants dans le panneau de configuration (paramètres-> réalité mixte-> Environnement-> Effacer les données d’environnement)
2. Garantir un éclairage suffisant pour un bon suivi et si l’exécution du mode de mappage verrouillé tente de maintenir le même éclairage
3. Lorsque cela est possible, conservez la plage dynamique d’éclairage en évitant les zones d’éclairage élevé en regard des zones masquées et sombres
4. Réduire les surfaces vides et sans texture, par exemple placer une plage de différentes affiches sur des murs blancs
5. Mapper l’espace sans objets dynamiques dans la scène, tels que le déplacement de personnes
6. Verrouiller la carte lors de l’importation (disponible par le biais de la version préliminaire d’Insider)
7. Déverrouillez la carte et relancez l’analyse de l’environnement en cas de dégradation de la qualité et/ou d’évolution de l’environnement (éclairage ou modifications dans la disposition des objets).
***

## <a name="running-mixed-reality-spatial-data-packager-with-companion-script"></a>Exécution d’un package de données spatiales de réalité mixte avec un script compagnon

Nous avons fourni MRSpatialPackagerHelperScript. ps1 qui exécute les outils de mappage de package. 


Les paramètres de script sont définis ci-dessous :

```
-AppName <String>
    On export: The spatial anchors from the app of interest
    On import: The target app that spatial anchors should be imported for
    Returns a list of apps containing the input string if a unique app is not found

-UserName <String>
    Target username, will return a list of users if a unique match is not found

-Mode <String>
    import or export

-MapxPath <String>
    On export: Directory to export your mapx files
    On import: Directory where import mapx are stored

-LockMap <Int32>
    0 to unlock map
    1 to lock map
    This functionality requires an updated driver from Insider Preview Builds with the Map Locking feature

-BinPath <String>
    Path to MixedRealitySpatialDataPackager.exe, default value is current directory
```

### <a name="powershell-script-example-usage-and-output"></a>Utilisation et sortie de l’exemple de script PowerShell

.\MRSpatialPackagerHelperScript.ps1-AppName holoshell-UserName administrateur-mode Export-MapxPath D:\temp\-LockMap 0
```
Package Family Name for holoshell: HoloShell_cw5n1h2txyewy
User SID for Administrator: S-1-5-21-1279937937-3984375698-1043392598-499
Lock map value successfully set to 0

Running: C:\bin\MixedRealitySpatialDataPackager.exe export D:\temp\ HoloShell_cw5n1h2txyewy S-1-5-21-1279937937-3984375698-1043392598-499

Attempting to disable Windows MR driver
Driver disabled
Validating spatial data version information...
Device spatial data version OK
External spatial data version OK
Importing spatial anchors for user account phguan
Stopping SPECTRUM
Stopped SPECTRUM
Stopping SHAREDREALITYSVC
Stopped SHAREDREALITYSVC
Space ID is {00000000-4321-0000-0000-000000000000}
SUCCESS: Unpacked Space from D:\temp\map\het.mapx to
C:\ProgramData\WindowsHolographicDevices\SpatialStore\HoloLensSensors\{00000000-4321-0000-0000-000000000000}\
Space ID is {78FA06B5-4416-4815-BB00-B3CB5C983B7D}
SUCCESS: Unpacked Space from D:\temp\map\sa.mapx to
C:\ProgramData\Microsoft\Spectrum\PersistedSpatialAnchors\
Attempting to enable Windows MR driver
Driver enabled
Starting SHAREDREALITYSVC
Started SHAREDREALITYSVC
Starting SPECTRUM
Started SPECTRUM
IMPORT SUCCESS
```

### <a name="how-to-export-using-mixedrealitypackagerexe"></a>Procédure d’exportation à l’aide de MixedRealityPackager. exe
```
MixedRealitySpatialDataPackager.exe export <folderpath to mapx files> <source package family name>    
```

L’exportation des mappages de l’appareil génère deux fichiers MapX, obtenir. MapX et sa. MapX. Pendant le processus d’exportation, toutes les ancres spatiales sont supprimées, à l’exception de l’application spécifiée et de la limite créée par l’utilisateur (le cas échéant). Le nom de famille du package source doit correspondre à une application installée existante. sinon, le fichier exe échoue.

### <a name="how-to-import-using-mixedrealitypackagerexe"></a>Procédure d’importation à l’aide de MixedRealityPackager. exe
```
MixedRealitySpatialDataPackager.exe import <folderpath to mapx files> <target package family name> <user SID>
```
L’importation supprime les données spatiales existantes et les remplace par les données du répertoire spécifié. L’entrée nom de l’application spécifie le nom du package de l’application cible qui doit être importé pour les ancres spatiales et le SID de l’utilisateur cible spécifie l’utilisateur qui doit avoir accès aux ancres spatiales importées. Le nom de la famille de packages cible et les SID d’utilisateur doivent correspondre aux valeurs existantes sur le PC. sinon, le fichier exe échoue.


***
## <a name="error-messages"></a>Messages d'erreur
En outre, les messages d’erreur ci-dessous sont également accompagnés d’un HRESULT

### <a name="if-there-was-an-error-invalid-arguments"></a>En cas d’erreur d’arguments non valides
```
Invalid command line parameters
```

### <a name="if-the-executable-was-not-run-in-administrator-mode"></a>Si l’exécutable n’a pas été exécuté en mode administrateur
```
1. Unable to determine elevation privileges 
2. Please run with administrator privileges 
```

### <a name="if-there-was-an-error-enabling-or-disabling-the-driver"></a>Si une erreur s’est produite lors de l’activation ou de la désactivation du pilote
```
1. Could not find the specified driver with class GUID {d612553d-06b1-49ca-8938-e39ef80eb16f}
2. Could not find the device instance ID for specified driver with class GUID {d612553d-06b1-49ca-8938-e39ef80eb16f}
3. Could not find the specified driver with device instance ID <INSTANCE ID>
4. Failed to enable/disable driver
```

### <a name="if-there-was-an-error-validating-the-spatial-database-version"></a>Si une erreur s’est produite lors de la validation de la version de la base de données spatiale
```
1. Could not read database version
2. This tool is not compatible with the current driver version of Windows Mixed Reality and/or the spatial data provided to replace the existing spatial data is an invalid version.
3. No spatial data is present on the current device please connect your Mixed Reality device to initialize spatial data. If the problem persists please restart your PC.
```

### <a name="if-there-was-an-error-validating-the-package-family-name-provided-for-target-importexport-app"></a>Si une erreur s’est produite lors de la validation du nom de famille de packages fourni pour l’application d’importation/exportation cible
```
The package family name does not correspond to an installed app
```

### <a name="if-there-was-an-error-validating-the-user-sid"></a>Si une erreur s’est produite lors de la validation du SID de l’utilisateur
```
Failed to find local user for passed in user SID
```

### <a name="if-there-was-an-error-related-to-the-destination-or-source-spatial-data-files"></a>En cas d’erreur liée aux fichiers de données spatiales de destination ou source
```
1. Folder path to space store files doesn't exist 
2. het.mapx or sa.mapx file doesn't exist in <PATH> for import
3. Unable to create directory at <PATH> for export
```

### <a name="if-there-was-an-error-related-to-starting-and-stopping-spectrumsharedrealitysvc"></a>En cas d’erreur liée au démarrage et à l’arrêt du spectre/SharedRealitySvc
```
1. Unable to open service manager <SERVICE>
2. Timed out trying to start/stop <SERVICE>
```
