---
title: Documentation du package de données spatiales de la réalité mixte
description: Documentation sur l’utilisation d’un package de données spatiales de réalité mixte
author: alfred-msft
ms.author: yuripek
ms.date: 05/16/2019
ms.topic: article
keywords: LBE, MixedRealitySpatialDataPackager.exe, MixedRealitySpatialDataPackager
ms.openlocfilehash: 4a285cbd7423d7cacaf52370e6e19acf42672289
ms.sourcegitcommit: cfca6cb016d8683fa2c611a97d493a4947935dbb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86402738"
---
# <a name="mixed-reality-spatial-data-packager-documentation"></a><span data-ttu-id="2f52a-104">Documentation du package de données spatiales de la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="2f52a-104">Mixed Reality Spatial Data Packager Documentation</span></span>

>[!NOTE]
> <span data-ttu-id="2f52a-105">Cet outil et son fonctionnement sont proposés tels quels.</span><span class="sxs-lookup"><span data-stu-id="2f52a-105">This tool and its operation are offered as-is.</span></span> <span data-ttu-id="2f52a-106">Elle est sujette à modification sans aucun préavis et peut ne pas être compatible avec les futures versions de Windows ou de Windows Mixed Reality HMD.</span><span class="sxs-lookup"><span data-stu-id="2f52a-106">It is subject to change without any notice and may not be compatible with future Windows or Windows Mixed Reality HMD releases.</span></span>

## <a name="download"></a><span data-ttu-id="2f52a-107">Téléchargement</span><span class="sxs-lookup"><span data-stu-id="2f52a-107">Download</span></span>
 <span data-ttu-id="2f52a-108">Téléchargez [MixedRealitySpatialDataPackager ici](https://download.microsoft.com/download/A/1/2/A12B8A90-B3F7-4ED9-A4BB-D59DDCDAA125/MixedRealitySpatialDataPackager.zip)</span><span class="sxs-lookup"><span data-stu-id="2f52a-108">Download [MixedRealitySpatialDataPackager here](https://download.microsoft.com/download/A/1/2/A12B8A90-B3F7-4ED9-A4BB-D59DDCDAA125/MixedRealitySpatialDataPackager.zip)</span></span>

## <a name="device-support"></a><span data-ttu-id="2f52a-109">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="2f52a-109">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="2f52a-110"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="2f52a-110"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="2f52a-111"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="2f52a-111"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="2f52a-112"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="2f52a-112"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="2f52a-113"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="2f52a-113"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="2f52a-114">Package de données spatiales de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="2f52a-114">Mixed Reality Spatial Data Packager</span></span></td>
        <td>❌</td>
        <td>❌</td>
        <td><span data-ttu-id="2f52a-115">✔️</span><span class="sxs-lookup"><span data-stu-id="2f52a-115">✔️</span></span></td>
    </tr>
</table>

## <a name="quickstart"></a><span data-ttu-id="2f52a-116">Démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="2f52a-116">Quickstart</span></span>

<span data-ttu-id="2f52a-117">L’outil mélangeur de données spatiales de réalité mixte copie les données spatiales d’une application cible d’un ordinateur vers un autre à l’aide d’un processus d’exportation et d’importation en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="2f52a-117">The Mixed Reality Spatial Data Packager tool copies the spatial data of a target app from one PC to another through a two step export and import process.</span></span> <span data-ttu-id="2f52a-118">L’outil doit être exécuté avec des privilèges d’administrateur et supprimer les données spatiales existantes lors de l’importation.</span><span class="sxs-lookup"><span data-stu-id="2f52a-118">The tool must be run with administrator privileges and deletes the existing spatial data on import.</span></span> <span data-ttu-id="2f52a-119">L’exportation laisse les données spatiales existantes intactes.</span><span class="sxs-lookup"><span data-stu-id="2f52a-119">Export leaves the existing spatial data intact.</span></span>

<span data-ttu-id="2f52a-120">Principales exigences et limitations :</span><span class="sxs-lookup"><span data-stu-id="2f52a-120">Key requirements and limitations:</span></span>

1. <span data-ttu-id="2f52a-121">L’outil doit être exécuté avec des privilèges d’administrateur</span><span class="sxs-lookup"><span data-stu-id="2f52a-121">Tool must be run with administrator privileges</span></span> 
2. <span data-ttu-id="2f52a-122">Vous devrez peut-être redémarrer le PC si le portail de réalité mixte est instable après l’exécution de l’outil</span><span class="sxs-lookup"><span data-stu-id="2f52a-122">You may have to restart PC if Mixed Reality Portal is unstable after running the tool</span></span>
3. <span data-ttu-id="2f52a-123">L’outil ne s’exécute pas quand des incompatibilités ou des incompatibilités de version de données spatiales sont rencontrées</span><span class="sxs-lookup"><span data-stu-id="2f52a-123">Tool will not run when encountering spatial data version mismatches or incompatibilities</span></span>
4. <span data-ttu-id="2f52a-124">L’outil efface les données spatiales existantes lors de l’importation</span><span class="sxs-lookup"><span data-stu-id="2f52a-124">Tool will erase existing spatial data on import</span></span>
5. <span data-ttu-id="2f52a-125">En cas d’échec du processus d’importation, les données précédentes ne peuvent pas être restaurées, sauf si elles ont été sauvegardées en l’exportant précédemment</span><span class="sxs-lookup"><span data-stu-id="2f52a-125">If import process fails previous data cannot be restored unless it has been backed up by exporting previously</span></span>
6. <span data-ttu-id="2f52a-126">La qualité de la fonctionnalité d’importation est subordonné au mode « lecture seule » pour les données cartographiques spatiales</span><span class="sxs-lookup"><span data-stu-id="2f52a-126">Quality of import functionality contingent on “Read-Only” mode for spatial map data</span></span>
***

## <a name="mapping-best-practices"></a><span data-ttu-id="2f52a-127">Meilleures pratiques de mappage</span><span class="sxs-lookup"><span data-stu-id="2f52a-127">Mapping Best Practices</span></span>

1. <span data-ttu-id="2f52a-128">Effacer les mappages existants dans le panneau de configuration (paramètres-> réalité mixte-> environnement-> effacer les données d’environnement)</span><span class="sxs-lookup"><span data-stu-id="2f52a-128">Clear existing maps from the Control Panel (Settings -> Mixed Reality -> Environment -> Clear environment data)</span></span>
2. <span data-ttu-id="2f52a-129">Garantir un éclairage suffisant pour un bon suivi et si l’exécution du mode de mappage verrouillé tente de maintenir le même éclairage</span><span class="sxs-lookup"><span data-stu-id="2f52a-129">Ensure sufficient lighting for good tracking and if running locked map mode try to maintain the same lighting</span></span>
3. <span data-ttu-id="2f52a-130">Lorsque cela est possible, conservez la plage dynamique d’éclairage en évitant les zones d’éclairage élevé en regard des zones masquées et sombres</span><span class="sxs-lookup"><span data-stu-id="2f52a-130">When possible keep the lighting dynamic range low by avoiding areas of high illumination next to dark, shadowed areas</span></span>
4. <span data-ttu-id="2f52a-131">Réduire les surfaces vides et sans texture, par exemple placer une plage de différentes affiches sur des murs blancs</span><span class="sxs-lookup"><span data-stu-id="2f52a-131">Minimize blank, textureless surfaces e.g. place a range of different posters on white walls</span></span>
5. <span data-ttu-id="2f52a-132">Mapper l’espace sans objets dynamiques dans la scène, tels que le déplacement de personnes</span><span class="sxs-lookup"><span data-stu-id="2f52a-132">Map the space without dynamic objects in the scene such as moving people</span></span>
6. <span data-ttu-id="2f52a-133">Verrouiller la carte lors de l’importation (disponible par le biais de la version préliminaire d’Insider)</span><span class="sxs-lookup"><span data-stu-id="2f52a-133">Lock the map on import (available via Insider Preview)</span></span>
7. <span data-ttu-id="2f52a-134">Déverrouillez la carte et relancez l’analyse de l’environnement en cas de dégradation de la qualité et/ou d’évolution de l’environnement (éclairage ou modifications dans la disposition des objets).</span><span class="sxs-lookup"><span data-stu-id="2f52a-134">Unlock the map and rescan the environment when tracking quality degrades and/or there are changes in the environment (lighting or changes in object layout)</span></span>
***

## <a name="running-mixed-reality-spatial-data-packager-with-companion-script"></a><span data-ttu-id="2f52a-135">Exécution d’un package de données spatiales de réalité mixte avec un script compagnon</span><span class="sxs-lookup"><span data-stu-id="2f52a-135">Running Mixed Reality Spatial Data Packager with Companion Script</span></span>

<span data-ttu-id="2f52a-136">Nous avons fourni MRSpatialPackagerHelperScript.ps1 qui exécute les outils de mappage de package.</span><span class="sxs-lookup"><span data-stu-id="2f52a-136">We have provided MRSpatialPackagerHelperScript.ps1 that runs the map packager the tools.</span></span> 


<span data-ttu-id="2f52a-137">Les paramètres de script sont définis ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2f52a-137">The script parameters are defined below:</span></span>

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

-BinPath <String>
    Path to MixedRealitySpatialDataPackager.exe, default value is current directory
```

### <a name="powershell-script-example-usage-and-output"></a><span data-ttu-id="2f52a-138">Utilisation et sortie de l’exemple de script PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f52a-138">Powershell Script Example Usage and Output</span></span>

<span data-ttu-id="2f52a-139">.\MRSpatialPackagerHelperScript.ps1-AppName holoshell-nom_utilisateur mode administrateur Export-MapxPath D:\temp\-LockMap 0</span><span class="sxs-lookup"><span data-stu-id="2f52a-139">.\MRSpatialPackagerHelperScript.ps1 -AppName holoshell -UserName Administrator -Mode export -MapxPath D:\temp\ -LockMap 0</span></span>
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

### <a name="how-to-export-using-mixedrealityspatialdatapackagerexe"></a><span data-ttu-id="2f52a-140">Procédure d’exportation à l’aide de MixedRealitySpatialDataPackager.exe</span><span class="sxs-lookup"><span data-stu-id="2f52a-140">How to Export using MixedRealitySpatialDataPackager.exe</span></span>
```
MixedRealitySpatialDataPackager.exe export <folderpath to mapx files> <source package family name>    
```

<span data-ttu-id="2f52a-141">L’exportation des mappages de l’appareil génère deux fichiers MapX, obtenir. MapX et sa. MapX.</span><span class="sxs-lookup"><span data-stu-id="2f52a-141">Exporting maps off device generates two mapx files, het.mapx and sa.mapx.</span></span> <span data-ttu-id="2f52a-142">Pendant le processus d’exportation, toutes les ancres spatiales sont supprimées, à l’exception de l’application spécifiée et de la limite créée par l’utilisateur (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="2f52a-142">During the export process all spatial anchors are removed except for the specified app and the user-created boundary (if it exists).</span></span> <span data-ttu-id="2f52a-143">Le nom de famille du package source doit correspondre à une application installée existante. sinon, le fichier exe échoue.</span><span class="sxs-lookup"><span data-stu-id="2f52a-143">The source package family name must match an existing installed app or the exe will fail.</span></span>

### <a name="how-to-import-using-mixedrealityspatialdatapackagerexe"></a><span data-ttu-id="2f52a-144">Procédure d’importation à l’aide de MixedRealitySpatialDataPackager.exe</span><span class="sxs-lookup"><span data-stu-id="2f52a-144">How to Import using MixedRealitySpatialDataPackager.exe</span></span>
```
MixedRealitySpatialDataPackager.exe import <folderpath to mapx files> <target package family name> <user SID>
```
<span data-ttu-id="2f52a-145">L’importation supprime les données spatiales existantes et les remplace par les données du répertoire spécifié.</span><span class="sxs-lookup"><span data-stu-id="2f52a-145">Import deletes the existing spatial data and replaces it with the data from the specified directory.</span></span> <span data-ttu-id="2f52a-146">L’entrée nom de l’application spécifie le nom du package de l’application cible qui doit être importé pour les ancres spatiales et le SID de l’utilisateur cible spécifie l’utilisateur qui doit avoir accès aux ancres spatiales importées.</span><span class="sxs-lookup"><span data-stu-id="2f52a-146">The app name input specifies the package name of the target app that like the spatial anchors should be imported for and the target user SID specifies the user that should have access to the imported spatial anchors.</span></span> <span data-ttu-id="2f52a-147">Le nom de la famille de packages cible et les SID d’utilisateur doivent correspondre aux valeurs existantes sur le PC. sinon, le fichier exe échoue.</span><span class="sxs-lookup"><span data-stu-id="2f52a-147">The target package family name and user SIDs must match existing values on the PC or the exe will fail.</span></span>


***
## <a name="error-messages"></a><span data-ttu-id="2f52a-148">Messages d'erreur</span><span class="sxs-lookup"><span data-stu-id="2f52a-148">Error Messages</span></span>
<span data-ttu-id="2f52a-149">En outre, les messages d’erreur ci-dessous sont également accompagnés d’un HRESULT</span><span class="sxs-lookup"><span data-stu-id="2f52a-149">In addition the error messages below failures will also be accompanied with an HRESULT</span></span>

### <a name="if-there-was-an-error-invalid-arguments"></a><span data-ttu-id="2f52a-150">En cas d’erreur d’arguments non valides</span><span class="sxs-lookup"><span data-stu-id="2f52a-150">If there was an error invalid arguments</span></span>
```
Invalid command line parameters
```

### <a name="if-the-executable-was-not-run-in-administrator-mode"></a><span data-ttu-id="2f52a-151">Si l’exécutable n’a pas été exécuté en mode administrateur</span><span class="sxs-lookup"><span data-stu-id="2f52a-151">If the executable was not run in administrator mode</span></span>
```
1. Unable to determine elevation privileges 
2. Please run with administrator privileges 
```

### <a name="if-there-was-an-error-enabling-or-disabling-the-driver"></a><span data-ttu-id="2f52a-152">Si une erreur s’est produite lors de l’activation ou de la désactivation du pilote</span><span class="sxs-lookup"><span data-stu-id="2f52a-152">If there was an error enabling or disabling the driver</span></span>
```
1. Could not find the specified driver with class GUID {d612553d-06b1-49ca-8938-e39ef80eb16f}
2. Could not find the device instance ID for specified driver with class GUID {d612553d-06b1-49ca-8938-e39ef80eb16f}
3. Could not find the specified driver with device instance ID <INSTANCE ID>
4. Failed to enable/disable driver
```

### <a name="if-there-was-an-error-validating-the-spatial-database-version"></a><span data-ttu-id="2f52a-153">Si une erreur s’est produite lors de la validation de la version de la base de données spatiale</span><span class="sxs-lookup"><span data-stu-id="2f52a-153">If there was an error validating the spatial database version</span></span>
```
1. Could not read database version
2. This tool is not compatible with the current driver version of Windows Mixed Reality and/or the spatial data provided to replace the existing spatial data is an invalid version.
3. No spatial data is present on the current device please connect your Mixed Reality device to initialize spatial data. If the problem persists please restart your PC.
```

### <a name="if-there-was-an-error-validating-the-package-family-name-provided-for-target-importexport-app"></a><span data-ttu-id="2f52a-154">Si une erreur s’est produite lors de la validation du nom de famille de packages fourni pour l’application d’importation/exportation cible</span><span class="sxs-lookup"><span data-stu-id="2f52a-154">If there was an error validating the package family name provided for target import/export app</span></span>
```
The package family name does not correspond to an installed app
```

### <a name="if-there-was-an-error-validating-the-user-sid"></a><span data-ttu-id="2f52a-155">Si une erreur s’est produite lors de la validation du SID de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2f52a-155">If there was an error validating the user SID</span></span>
```
Failed to find local user for passed in user SID
```

### <a name="if-there-was-an-error-related-to-the-destination-or-source-spatial-data-files"></a><span data-ttu-id="2f52a-156">En cas d’erreur liée aux fichiers de données spatiales de destination ou source</span><span class="sxs-lookup"><span data-stu-id="2f52a-156">If there was an error related to the destination or source spatial data files</span></span>
```
1. Folder path to space store files doesn't exist 
2. het.mapx or sa.mapx file doesn't exist in <PATH> for import
3. Unable to create directory at <PATH> for export
```

### <a name="if-there-was-an-error-related-to-starting-and-stopping-spectrumsharedrealitysvc"></a><span data-ttu-id="2f52a-157">En cas d’erreur liée au démarrage et à l’arrêt du spectre/SharedRealitySvc</span><span class="sxs-lookup"><span data-stu-id="2f52a-157">If there was an error related to starting and stopping Spectrum/SharedRealitySvc</span></span>
```
1. Unable to open service manager <SERVICE>
2. Timed out trying to start/stop <SERVICE>
```
