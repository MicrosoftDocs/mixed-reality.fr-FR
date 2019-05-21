---
title: Documentation de Packager les données spatiales de réalité mixte
description: Documentation sur l’utilisation mixte Packager de données spatiales réalité
author: alfred-msft
ms.author: alreynol
ms.date: 05/16/2019
ms.topic: article
keywords: lbe, MixedRealitySpatialDataPackager.exe, MixedRealitySpatialDataPackager
ms.openlocfilehash: 7ad1159af9eecd3ca3622dd25cc1f49fb0b1700a
ms.sourcegitcommit: d565a69a9320e736304372b3f010af1a4d286a62
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65942105"
---
# <a name="mixed-reality-spatial-data-packager-documentation"></a>Documentation de Packager les données spatiales de réalité mixte

>[!NOTE]
> Cet outil et son fonctionnement sont proposés en tant que-est. Il est susceptible de changer sans préavis et ne seront ne peut-être pas compatible avec Windows futures ou libère HMD de réalité mixte Windows.

## <a name="download"></a>Télécharger
 Télécharger [MixedRealitySpatialDataPackager ici](http://download.microsoft.com/download/A/1/2/A12B8A90-B3F7-4ED9-A4BB-D59DDCDAA125/MixedRealitySpatialDataPackager.zip)

## <a name="quickstart"></a>Guide de démarrage rapide

L’outil mixte Packager de données spatiales réalité copie les données spatiales d’une application cible à partir d’un PC à un autre via une étape deux exporter et importer des processus. L’outil doit être exécuté avec des privilèges d’administrateur et supprime les données spatiales existantes lors de l’importation. Exportation laisse les données spatiales existantes intacts.

Conditions de clé et limitations :

1. Outil doit être exécuté avec des privilèges d’administrateur 
2. Vous devrez peut-être redémarrer le PC si le portail de réalité mixte est instable après l’exécution de l’outil
3. Outil ne s’exécutera pas si vous rencontrez des incompatibilités de version des données spatiales ou des incompatibilités
4. Outil effacera les données spatiales existantes lors de l’importation
5. Si le processus d’importation échoue précédentes données ne peut pas être restaurées, sauf si elle a été sauvegardée en exportant précédemment
6. Qualité de la fonctionnalité d’importation éventuels sur le mode « Lecture seule » pour les données de mappage spatial
***

## <a name="mapping-best-practices"></a>Mappage des meilleures pratiques

1. Effacer les mappages existants à partir du panneau (Paramètres -> Mixed Reality -> environnement -> environnement effacer les données)
2. Assurez-vous d’éclairage suffisant pour le suivi des bons et si le mode mappage verrouillé en cours d’exécution tenter de maintenir l’éclairage même
3. Lorsque cela est possible limiter la plage dynamique d’éclairage en évitant les zones d’éclairage élevé en regard des zones masquées foncées
4. Réduit vide, les surfaces textureless placent par exemple, une plage de posters différentes sur les murs blancs
5. Mapper l’espace sans objets dynamiques dans la scène tels que le déplacement des personnes
6. Verrouiller la carte lors de l’importation (disponible via Insider Preview)
7. Déverrouiller la carte et relancer l’analyse de l’environnement lorsque le suivi de la qualité dégrade et/ou des modifications dans l’environnement (éclairage ou modifications apportées à la disposition des objets)
***

## <a name="running-mixed-reality-spatial-data-packager-with-companion-script"></a>En cours d’exécution Packager les données spatiales de réalité mixte avec Script d’accompagnement

Nous vous proposons MRSpatialPackagerHelperScript.ps1 qui exécute le Gestionnaire de package de carte les outils. 


Les paramètres de script sont définies ci-dessous :

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

### <a name="powershell-script-example-usage-and-output"></a>Exemple d’utilisation du Script Powershell et de sortie

.\MRSpatialPackagerHelperScript.ps1 - AppName holoshell - UserName administrateur-Mode exporter - MapxPath D:\temp\ LockMap - 0
```
Package Family Name for holoshell: HoloShell_cw5n1h2txyewy
User SID for Administrator: S-1-5-21-1279937937-3984375698-1043392598-499
Lock map value succesfully set to 0

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

### <a name="how-to-export-using-mixedrealitypackagerexe"></a>L’exportation à l’aide de MixedRealityPackager.exe
```
MixedRealitySpatialDataPackager.exe export <folderpath to mapx files> <source package family name>    
```

Exportation des mappages à l’appareil hors tension génère deux fichiers mapx, het.mapx et sa.mapx. Pendant le processus d’exportation tous les points d’ancrage spatiales sont supprimées à l’exception de l’application spécifiée et la limite créée par l’utilisateur (si elle existe). Le nom de famille du package source doit correspondre à une application installée existante ou l’exécutable échoue.

### <a name="how-to-import-using-mixedrealitypackagerexe"></a>Comment importer à l’aide de MixedRealityPackager.exe
```
MixedRealitySpatialDataPackager.exe import <folderpath to mapx files> <target package family name> <user SID>
```
Importation supprime les données spatiales existantes et le remplace par les données à partir du répertoire spécifié. L’entrée de nom d’application spécifie le nom du package de l’application cible que que les ancres spatiales doit être importé pour et le SID de l’utilisateur cible spécifie l’utilisateur qui doit avoir accès aux ancres spatiales importés. Le nom de famille de packages cible et le SID d’utilisateur doivent correspondre à des valeurs existantes sur le PC ou l’exécutable échoue.


***
## <a name="error-messages"></a>Messages d'erreur
En outre les messages d’erreur ci-dessous défaillances seront également associés avec un HRESULT

### <a name="if-there-was-an-error-invalid-arguments"></a>Si une erreur s’est produite arguments non valides
```
Invalid command line parameters
```

### <a name="if-the-executable-was-not-run-in-administrator-mode"></a>Si le fichier exécutable n’a pas été exécuté en mode administrateur
```
1. Unable to determine elevation privileges 
2. Please run with administrator privileges 
```

### <a name="if-there-was-an-error-enabling-or-disabling-the-driver"></a>Si une erreur est l’activation ou désactivation du pilote
```
1. Could not find the specified driver with class GUID {d612553d-06b1-49ca-8938-e39ef80eb16f}
2. Could not find the device instance ID for specified driver with class GUID {d612553d-06b1-49ca-8938-e39ef80eb16f}
3. Could not find the specified driver with device instance ID <INSTANCE ID>
4. Failed to enable/disable driver
```

### <a name="if-there-was-an-error-validating-the-spatial-database-version"></a>Si une erreur de validation de la version de base de données spatiales
```
1. Could not read database version
2. This tool is not compatible with the current driver version of Windows Mixed Reality and/or the spatial data provided to replace the existing spatial data is an invalid version.
3. No spatial data is present on the current device please connect your Mixed Reality device to initialize spatial data. If the problem persists please restart your PC.
```

### <a name="if-there-was-an-error-validating-the-package-family-name-provided-for-target-importexport-app"></a>Si une erreur de contrôle est le nom de famille de packages fourni pour l’application d’importation/exportation de cible
```
The package family name does not correspond to an installed app
```

### <a name="if-there-was-an-error-validating-the-user-sid"></a>Si une erreur de contrôle est le SID d’utilisateur
```
Failed to find local user for passed in user SID
```

### <a name="if-there-was-an-error-related-to-the-destination-or-source-spatial-data-files"></a>S’il y avait une erreur liée à la destination ou la source de données spatiales fichiers
```
1. Folder path to space store files doesn't exist 
2. het.mapx or sa.mapx file doesn't exist in <PATH> for import
3. Unable to create directory at <PATH> for export
```

### <a name="if-there-was-an-error-related-to-starting-and-stoping-spectrumsharedrealitysvc"></a>Si une erreur s’est produite relatifs au démarrage et arrêt du spectre/SharedRealitySvc
```
1. Unable to open service manager <SERVICE>
2. Timed out trying to start/stop <SERVICE>
```
