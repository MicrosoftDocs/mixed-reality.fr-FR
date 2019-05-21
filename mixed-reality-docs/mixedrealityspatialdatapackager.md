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
# <a name="mixed-reality-spatial-data-packager-documentation"></a><span data-ttu-id="b3f9f-104">Documentation de Packager les données spatiales de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="b3f9f-104">Mixed Reality Spatial Data Packager Documentation</span></span>

>[!NOTE]
> <span data-ttu-id="b3f9f-105">Cet outil et son fonctionnement sont proposés en tant que-est.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-105">This tool and its operation are offered as-is.</span></span> <span data-ttu-id="b3f9f-106">Il est susceptible de changer sans préavis et ne seront ne peut-être pas compatible avec Windows futures ou libère HMD de réalité mixte Windows.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-106">It is subject to change without any notice and may not be compatible with future Windows or Windows Mixed Reality HMD releases.</span></span>

## <a name="download"></a><span data-ttu-id="b3f9f-107">Télécharger</span><span class="sxs-lookup"><span data-stu-id="b3f9f-107">Download</span></span>
 <span data-ttu-id="b3f9f-108">Télécharger [MixedRealitySpatialDataPackager ici](http://download.microsoft.com/download/A/1/2/A12B8A90-B3F7-4ED9-A4BB-D59DDCDAA125/MixedRealitySpatialDataPackager.zip)</span><span class="sxs-lookup"><span data-stu-id="b3f9f-108">Download [MixedRealitySpatialDataPackager here](http://download.microsoft.com/download/A/1/2/A12B8A90-B3F7-4ED9-A4BB-D59DDCDAA125/MixedRealitySpatialDataPackager.zip)</span></span>

## <a name="quickstart"></a><span data-ttu-id="b3f9f-109">Guide de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="b3f9f-109">Quickstart</span></span>

<span data-ttu-id="b3f9f-110">L’outil mixte Packager de données spatiales réalité copie les données spatiales d’une application cible à partir d’un PC à un autre via une étape deux exporter et importer des processus.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-110">The Mixed Reality Spatial Data Packager tool copies the spatial data of a target app from one PC to another through a two step export and import process.</span></span> <span data-ttu-id="b3f9f-111">L’outil doit être exécuté avec des privilèges d’administrateur et supprime les données spatiales existantes lors de l’importation.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-111">The tool must be run with administrator privileges and deletes the existing spatial data on import.</span></span> <span data-ttu-id="b3f9f-112">Exportation laisse les données spatiales existantes intacts.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-112">Export leaves the existing spatial data intact.</span></span>

<span data-ttu-id="b3f9f-113">Conditions de clé et limitations :</span><span class="sxs-lookup"><span data-stu-id="b3f9f-113">Key requirements and limitations:</span></span>

1. <span data-ttu-id="b3f9f-114">Outil doit être exécuté avec des privilèges d’administrateur</span><span class="sxs-lookup"><span data-stu-id="b3f9f-114">Tool must be run with administrator privileges</span></span> 
2. <span data-ttu-id="b3f9f-115">Vous devrez peut-être redémarrer le PC si le portail de réalité mixte est instable après l’exécution de l’outil</span><span class="sxs-lookup"><span data-stu-id="b3f9f-115">You may have to restart PC if Mixed Reality Portal is unstable after running the tool</span></span>
3. <span data-ttu-id="b3f9f-116">Outil ne s’exécutera pas si vous rencontrez des incompatibilités de version des données spatiales ou des incompatibilités</span><span class="sxs-lookup"><span data-stu-id="b3f9f-116">Tool will not run when encountering spatial data version mismatches or incompatibilities</span></span>
4. <span data-ttu-id="b3f9f-117">Outil effacera les données spatiales existantes lors de l’importation</span><span class="sxs-lookup"><span data-stu-id="b3f9f-117">Tool will erase existing spatial data on import</span></span>
5. <span data-ttu-id="b3f9f-118">Si le processus d’importation échoue précédentes données ne peut pas être restaurées, sauf si elle a été sauvegardée en exportant précédemment</span><span class="sxs-lookup"><span data-stu-id="b3f9f-118">If import process fails previous data cannot be restored unless it has been backed up by exporting previously</span></span>
6. <span data-ttu-id="b3f9f-119">Qualité de la fonctionnalité d’importation éventuels sur le mode « Lecture seule » pour les données de mappage spatial</span><span class="sxs-lookup"><span data-stu-id="b3f9f-119">Quality of import functionality contingent on “Read-Only” mode for spatial map data</span></span>
***

## <a name="mapping-best-practices"></a><span data-ttu-id="b3f9f-120">Mappage des meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="b3f9f-120">Mapping Best Practices</span></span>

1. <span data-ttu-id="b3f9f-121">Effacer les mappages existants à partir du panneau (Paramètres -> Mixed Reality -> environnement -> environnement effacer les données)</span><span class="sxs-lookup"><span data-stu-id="b3f9f-121">Clear existing maps from the Control Panel (Settings -> Mixed Reality -> Environment -> Clear environment data)</span></span>
2. <span data-ttu-id="b3f9f-122">Assurez-vous d’éclairage suffisant pour le suivi des bons et si le mode mappage verrouillé en cours d’exécution tenter de maintenir l’éclairage même</span><span class="sxs-lookup"><span data-stu-id="b3f9f-122">Ensure sufficient lighting for good tracking and if running locked map mode try to maintain the same lighting</span></span>
3. <span data-ttu-id="b3f9f-123">Lorsque cela est possible limiter la plage dynamique d’éclairage en évitant les zones d’éclairage élevé en regard des zones masquées foncées</span><span class="sxs-lookup"><span data-stu-id="b3f9f-123">When possible keep the lighting dynamic range low by avoiding areas of high illumination next to dark, shadowed areas</span></span>
4. <span data-ttu-id="b3f9f-124">Réduit vide, les surfaces textureless placent par exemple, une plage de posters différentes sur les murs blancs</span><span class="sxs-lookup"><span data-stu-id="b3f9f-124">Minimize blank, textureless surfaces e.g. place a range of different posters on white walls</span></span>
5. <span data-ttu-id="b3f9f-125">Mapper l’espace sans objets dynamiques dans la scène tels que le déplacement des personnes</span><span class="sxs-lookup"><span data-stu-id="b3f9f-125">Map the space without dynamic objects in the scene such as moving people</span></span>
6. <span data-ttu-id="b3f9f-126">Verrouiller la carte lors de l’importation (disponible via Insider Preview)</span><span class="sxs-lookup"><span data-stu-id="b3f9f-126">Lock the map on import (available via Insider Preview)</span></span>
7. <span data-ttu-id="b3f9f-127">Déverrouiller la carte et relancer l’analyse de l’environnement lorsque le suivi de la qualité dégrade et/ou des modifications dans l’environnement (éclairage ou modifications apportées à la disposition des objets)</span><span class="sxs-lookup"><span data-stu-id="b3f9f-127">Unlock the map and rescan the enviornment when tracking quality degrades and/or there are changes in the environment (lighting or changes in object layout)</span></span>
***

## <a name="running-mixed-reality-spatial-data-packager-with-companion-script"></a><span data-ttu-id="b3f9f-128">En cours d’exécution Packager les données spatiales de réalité mixte avec Script d’accompagnement</span><span class="sxs-lookup"><span data-stu-id="b3f9f-128">Running Mixed Reality Spatial Data Packager with Companion Script</span></span>

<span data-ttu-id="b3f9f-129">Nous vous proposons MRSpatialPackagerHelperScript.ps1 qui exécute le Gestionnaire de package de carte les outils.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-129">We have provided MRSpatialPackagerHelperScript.ps1 that runs the map packager the tools.</span></span> 


<span data-ttu-id="b3f9f-130">Les paramètres de script sont définies ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b3f9f-130">The script parameters are defined below:</span></span>

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

### <a name="powershell-script-example-usage-and-output"></a><span data-ttu-id="b3f9f-131">Exemple d’utilisation du Script Powershell et de sortie</span><span class="sxs-lookup"><span data-stu-id="b3f9f-131">Powershell Script Example Usage and Output</span></span>

<span data-ttu-id="b3f9f-132">.\MRSpatialPackagerHelperScript.ps1 - AppName holoshell - UserName administrateur-Mode exporter - MapxPath D:\temp\ LockMap - 0</span><span class="sxs-lookup"><span data-stu-id="b3f9f-132">.\MRSpatialPackagerHelperScript.ps1 -AppName holoshell -UserName Administrator -Mode export -MapxPath D:\temp\ -LockMap 0</span></span>
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

### <a name="how-to-export-using-mixedrealitypackagerexe"></a><span data-ttu-id="b3f9f-133">L’exportation à l’aide de MixedRealityPackager.exe</span><span class="sxs-lookup"><span data-stu-id="b3f9f-133">How to Export using MixedRealityPackager.exe</span></span>
```
MixedRealitySpatialDataPackager.exe export <folderpath to mapx files> <source package family name>    
```

<span data-ttu-id="b3f9f-134">Exportation des mappages à l’appareil hors tension génère deux fichiers mapx, het.mapx et sa.mapx.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-134">Exporting maps off device generates two mapx files, het.mapx and sa.mapx.</span></span> <span data-ttu-id="b3f9f-135">Pendant le processus d’exportation tous les points d’ancrage spatiales sont supprimées à l’exception de l’application spécifiée et la limite créée par l’utilisateur (si elle existe).</span><span class="sxs-lookup"><span data-stu-id="b3f9f-135">During the export process all spatial anchors are removed except for the specified app and the user-created boundary (if it exists).</span></span> <span data-ttu-id="b3f9f-136">Le nom de famille du package source doit correspondre à une application installée existante ou l’exécutable échoue.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-136">The source package family name must match an existing installed app or the exe will fail.</span></span>

### <a name="how-to-import-using-mixedrealitypackagerexe"></a><span data-ttu-id="b3f9f-137">Comment importer à l’aide de MixedRealityPackager.exe</span><span class="sxs-lookup"><span data-stu-id="b3f9f-137">How to Import using MixedRealityPackager.exe</span></span>
```
MixedRealitySpatialDataPackager.exe import <folderpath to mapx files> <target package family name> <user SID>
```
<span data-ttu-id="b3f9f-138">Importation supprime les données spatiales existantes et le remplace par les données à partir du répertoire spécifié.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-138">Import deletes the existing spatial data and replaces it with the data from the specified directory.</span></span> <span data-ttu-id="b3f9f-139">L’entrée de nom d’application spécifie le nom du package de l’application cible que que les ancres spatiales doit être importé pour et le SID de l’utilisateur cible spécifie l’utilisateur qui doit avoir accès aux ancres spatiales importés.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-139">The app name input specifies the package name of the target app that like the spatial anchors should be imported for and the target user SID specifies the user that should have access to the imported spatial anchors.</span></span> <span data-ttu-id="b3f9f-140">Le nom de famille de packages cible et le SID d’utilisateur doivent correspondre à des valeurs existantes sur le PC ou l’exécutable échoue.</span><span class="sxs-lookup"><span data-stu-id="b3f9f-140">The target package family name and user SIDs must match existing values on the PC or the exe will fail.</span></span>


***
## <a name="error-messages"></a><span data-ttu-id="b3f9f-141">Messages d'erreur</span><span class="sxs-lookup"><span data-stu-id="b3f9f-141">Error Messages</span></span>
<span data-ttu-id="b3f9f-142">En outre les messages d’erreur ci-dessous défaillances seront également associés avec un HRESULT</span><span class="sxs-lookup"><span data-stu-id="b3f9f-142">In addition the error messages below failures will also be accompanied with an HRESULT</span></span>

### <a name="if-there-was-an-error-invalid-arguments"></a><span data-ttu-id="b3f9f-143">Si une erreur s’est produite arguments non valides</span><span class="sxs-lookup"><span data-stu-id="b3f9f-143">If there was an error invalid arguments</span></span>
```
Invalid command line parameters
```

### <a name="if-the-executable-was-not-run-in-administrator-mode"></a><span data-ttu-id="b3f9f-144">Si le fichier exécutable n’a pas été exécuté en mode administrateur</span><span class="sxs-lookup"><span data-stu-id="b3f9f-144">If the executable was not run in administrator mode</span></span>
```
1. Unable to determine elevation privileges 
2. Please run with administrator privileges 
```

### <a name="if-there-was-an-error-enabling-or-disabling-the-driver"></a><span data-ttu-id="b3f9f-145">Si une erreur est l’activation ou désactivation du pilote</span><span class="sxs-lookup"><span data-stu-id="b3f9f-145">If there was an error enabling or disabling the driver</span></span>
```
1. Could not find the specified driver with class GUID {d612553d-06b1-49ca-8938-e39ef80eb16f}
2. Could not find the device instance ID for specified driver with class GUID {d612553d-06b1-49ca-8938-e39ef80eb16f}
3. Could not find the specified driver with device instance ID <INSTANCE ID>
4. Failed to enable/disable driver
```

### <a name="if-there-was-an-error-validating-the-spatial-database-version"></a><span data-ttu-id="b3f9f-146">Si une erreur de validation de la version de base de données spatiales</span><span class="sxs-lookup"><span data-stu-id="b3f9f-146">If there was an error validating the spatial database version</span></span>
```
1. Could not read database version
2. This tool is not compatible with the current driver version of Windows Mixed Reality and/or the spatial data provided to replace the existing spatial data is an invalid version.
3. No spatial data is present on the current device please connect your Mixed Reality device to initialize spatial data. If the problem persists please restart your PC.
```

### <a name="if-there-was-an-error-validating-the-package-family-name-provided-for-target-importexport-app"></a><span data-ttu-id="b3f9f-147">Si une erreur de contrôle est le nom de famille de packages fourni pour l’application d’importation/exportation de cible</span><span class="sxs-lookup"><span data-stu-id="b3f9f-147">If there was an error validating the package family name provided for target import/export app</span></span>
```
The package family name does not correspond to an installed app
```

### <a name="if-there-was-an-error-validating-the-user-sid"></a><span data-ttu-id="b3f9f-148">Si une erreur de contrôle est le SID d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="b3f9f-148">If there was an error validating the user SID</span></span>
```
Failed to find local user for passed in user SID
```

### <a name="if-there-was-an-error-related-to-the-destination-or-source-spatial-data-files"></a><span data-ttu-id="b3f9f-149">S’il y avait une erreur liée à la destination ou la source de données spatiales fichiers</span><span class="sxs-lookup"><span data-stu-id="b3f9f-149">If there was an error related to the destination or source spatial data files</span></span>
```
1. Folder path to space store files doesn't exist 
2. het.mapx or sa.mapx file doesn't exist in <PATH> for import
3. Unable to create directory at <PATH> for export
```

### <a name="if-there-was-an-error-related-to-starting-and-stoping-spectrumsharedrealitysvc"></a><span data-ttu-id="b3f9f-150">Si une erreur s’est produite relatifs au démarrage et arrêt du spectre/SharedRealitySvc</span><span class="sxs-lookup"><span data-stu-id="b3f9f-150">If there was an error related to starting and stoping Spectrum/SharedRealitySvc</span></span>
```
1. Unable to open service manager <SERVICE>
2. Timed out trying to start/stop <SERVICE>
```
