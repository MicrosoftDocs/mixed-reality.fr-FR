---
title: Informations de référence sur les API du portail d’appareil
description: Informations de référence sur l’API pour le portail de périphériques Windows sur HoloLens
author: hamalawi
ms.author: moelhama
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, portail des appareils Windows, API
ms.openlocfilehash: b9b9ada49b4f9810dc97c9da2873d4ccb60df424
ms.sourcegitcommit: 5612e8bfb9c548eac42182702cec87b160efbbfe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85441796"
---
# <a name="device-portal-api-reference"></a><span data-ttu-id="93197-104">Informations de référence sur les API du portail d’appareil</span><span class="sxs-lookup"><span data-stu-id="93197-104">Device portal API reference</span></span>

<span data-ttu-id="93197-105">Tout ce qui se trouve dans le [portail de périphériques Windows](using-the-windows-device-portal.md) repose sur des API REST que vous pouvez utiliser pour accéder aux données et contrôler votre appareil par programme.</span><span class="sxs-lookup"><span data-stu-id="93197-105">Everything in the [Windows Device Portal](using-the-windows-device-portal.md) is built on top of REST API's that you can use to access the data and control your device programmatically.</span></span>

## <a name="app-deloyment"></a><span data-ttu-id="93197-106">Déploiement de l’application</span><span class="sxs-lookup"><span data-stu-id="93197-106">App deloyment</span></span>

<span data-ttu-id="93197-107">**/API/App/packagemanager/package (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="93197-107">**/api/app/packagemanager/package (DELETE)**</span></span>

<span data-ttu-id="93197-108">Désinstalle une application</span><span class="sxs-lookup"><span data-stu-id="93197-108">Uninstalls an app</span></span>

<span data-ttu-id="93197-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-109">Parameters</span></span>
* <span data-ttu-id="93197-110">Package : nom de fichier du package à désinstaller.</span><span class="sxs-lookup"><span data-stu-id="93197-110">package : File name of the package to be uninstalled.</span></span>

<span data-ttu-id="93197-111">**/API/App/packagemanager/package (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-111">**/api/app/packagemanager/package (POST)**</span></span>

<span data-ttu-id="93197-112">Installe une application</span><span class="sxs-lookup"><span data-stu-id="93197-112">Installs an App</span></span>

<span data-ttu-id="93197-113">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-113">Parameters</span></span>
* <span data-ttu-id="93197-114">Package : nom de fichier du package à installer.</span><span class="sxs-lookup"><span data-stu-id="93197-114">package : File name of the package to be installed.</span></span>

<span data-ttu-id="93197-115">Payload</span><span class="sxs-lookup"><span data-stu-id="93197-115">Payload</span></span>
* <span data-ttu-id="93197-116">corps http en plusieurs parties, conforme</span><span class="sxs-lookup"><span data-stu-id="93197-116">multi-part conforming http body</span></span>

<span data-ttu-id="93197-117">**/API/App/packagemanager/packages (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-117">**/api/app/packagemanager/packages (GET)**</span></span>

<span data-ttu-id="93197-118">Récupère la liste des applications installées sur le système, avec les détails</span><span class="sxs-lookup"><span data-stu-id="93197-118">Retrieves the list of installed apps on the system, with details</span></span>

<span data-ttu-id="93197-119">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-119">Return data</span></span>
* <span data-ttu-id="93197-120">Liste des packages installés avec des détails</span><span class="sxs-lookup"><span data-stu-id="93197-120">List of installed packages with details</span></span>

<span data-ttu-id="93197-121">**/API/App/packagemanager/State (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-121">**/api/app/packagemanager/state (GET)**</span></span>

<span data-ttu-id="93197-122">Obtient l’état de l’installation de l’application en cours</span><span class="sxs-lookup"><span data-stu-id="93197-122">Gets the status of in progress app installation</span></span>

## <a name="dump-collection"></a><span data-ttu-id="93197-123">Collection de vidages</span><span class="sxs-lookup"><span data-stu-id="93197-123">Dump collection</span></span>

<span data-ttu-id="93197-124">**/API/Debug/dump/usermode/CrashControl (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="93197-124">**/api/debug/dump/usermode/crashcontrol (DELETE)**</span></span>

<span data-ttu-id="93197-125">Désactive la collecte de vidages sur incident pour une application faisant</span><span class="sxs-lookup"><span data-stu-id="93197-125">Disables crash dump collection for a sideloaded app</span></span>

<span data-ttu-id="93197-126">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-126">Parameters</span></span>
* <span data-ttu-id="93197-127">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="93197-127">packageFullname : package name</span></span>

<span data-ttu-id="93197-128">**/API/Debug/dump/usermode/CrashControl (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-128">**/api/debug/dump/usermode/crashcontrol (GET)**</span></span>

<span data-ttu-id="93197-129">Obtient les paramètres de la collection de vidages sur incident des applications faisant</span><span class="sxs-lookup"><span data-stu-id="93197-129">Gets settings for sideloaded apps crash dump collection</span></span>

<span data-ttu-id="93197-130">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-130">Parameters</span></span>
* <span data-ttu-id="93197-131">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="93197-131">packageFullname : package name</span></span>

<span data-ttu-id="93197-132">**/API/Debug/dump/usermode/CrashControl (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-132">**/api/debug/dump/usermode/crashcontrol (POST)**</span></span>

<span data-ttu-id="93197-133">Active et définit les paramètres de contrôle de vidage pour une application faisant</span><span class="sxs-lookup"><span data-stu-id="93197-133">Enables and sets dump control settings for a sideloaded app</span></span>

<span data-ttu-id="93197-134">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-134">Parameters</span></span>
* <span data-ttu-id="93197-135">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="93197-135">packageFullname : package name</span></span>

<span data-ttu-id="93197-136">**/API/Debug/dump/usermode/crashdump (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="93197-136">**/api/debug/dump/usermode/crashdump (DELETE)**</span></span>

<span data-ttu-id="93197-137">Supprime un vidage sur incident pour une application faisant</span><span class="sxs-lookup"><span data-stu-id="93197-137">Deletes a crash dump for a sideloaded app</span></span>

<span data-ttu-id="93197-138">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-138">Parameters</span></span>
* <span data-ttu-id="93197-139">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="93197-139">packageFullname : package name</span></span>
* <span data-ttu-id="93197-140">fileName : nom du fichier dump</span><span class="sxs-lookup"><span data-stu-id="93197-140">fileName : dump file name</span></span>

<span data-ttu-id="93197-141">**/API/Debug/dump/usermode/crashdump (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-141">**/api/debug/dump/usermode/crashdump (GET)**</span></span>

<span data-ttu-id="93197-142">Récupère un vidage sur incident pour une application faisant</span><span class="sxs-lookup"><span data-stu-id="93197-142">Retrieves a crash dump for a sideloaded app</span></span>

<span data-ttu-id="93197-143">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-143">Parameters</span></span>
* <span data-ttu-id="93197-144">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="93197-144">packageFullname : package name</span></span>
* <span data-ttu-id="93197-145">fileName : nom du fichier dump</span><span class="sxs-lookup"><span data-stu-id="93197-145">fileName : dump file name</span></span>

<span data-ttu-id="93197-146">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-146">Return data</span></span>
* <span data-ttu-id="93197-147">Fichier dump.</span><span class="sxs-lookup"><span data-stu-id="93197-147">Dump file.</span></span> <span data-ttu-id="93197-148">Inspecter avec WinDbg ou Visual Studio</span><span class="sxs-lookup"><span data-stu-id="93197-148">Inspect with WinDbg or Visual Studio</span></span>

<span data-ttu-id="93197-149">**/API/Debug/dump/usermode/dumps (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-149">**/api/debug/dump/usermode/dumps (GET)**</span></span>

<span data-ttu-id="93197-150">Retourne la liste de tous les vidages sur incident pour les applications faisant</span><span class="sxs-lookup"><span data-stu-id="93197-150">Returns list of all crash dumps for sideloaded apps</span></span>

<span data-ttu-id="93197-151">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-151">Return data</span></span>
* <span data-ttu-id="93197-152">Liste des vidages sur incident par application à chargement latéral</span><span class="sxs-lookup"><span data-stu-id="93197-152">List of crash dumps per side loaded app</span></span>

## <a name="etw"></a><span data-ttu-id="93197-153">ETW</span><span class="sxs-lookup"><span data-stu-id="93197-153">ETW</span></span>

<span data-ttu-id="93197-154">**/API/ETW/Providers (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-154">**/api/etw/providers (GET)**</span></span>

<span data-ttu-id="93197-155">Énumère les fournisseurs inscrits</span><span class="sxs-lookup"><span data-stu-id="93197-155">Enumerates registered providers</span></span>

<span data-ttu-id="93197-156">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-156">Return data</span></span>
* <span data-ttu-id="93197-157">Liste des fournisseurs, nom convivial et GUID</span><span class="sxs-lookup"><span data-stu-id="93197-157">List of providers, friendly name and GUID</span></span>

<span data-ttu-id="93197-158">**/API/ETW/session/Realtime (obtient/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="93197-158">**/api/etw/session/realtime (GET/WebSocket)**</span></span>

<span data-ttu-id="93197-159">Crée une session ETW en temps réel ; géré sur un WebSocket.</span><span class="sxs-lookup"><span data-stu-id="93197-159">Creates a realtime ETW session; managed over a websocket.</span></span>

<span data-ttu-id="93197-160">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-160">Return data</span></span>
* <span data-ttu-id="93197-161">Événements ETW des fournisseurs activés</span><span class="sxs-lookup"><span data-stu-id="93197-161">ETW events from the enabled providers</span></span>

## <a name="holographic-os"></a><span data-ttu-id="93197-162">Système d’exploitation holographique</span><span class="sxs-lookup"><span data-stu-id="93197-162">Holographic OS</span></span>

<span data-ttu-id="93197-163">**/API/Holographic/OS/ETW/customproviders (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-163">**/api/holographic/os/etw/customproviders (GET)**</span></span>

<span data-ttu-id="93197-164">Retourne une liste de fournisseurs ETW spécifiques à HoloLens qui ne sont pas inscrits auprès du système.</span><span class="sxs-lookup"><span data-stu-id="93197-164">Returns a list of HoloLens specific ETW providers that are not registered with the system</span></span>

<span data-ttu-id="93197-165">**/API/Holographic/OS/services (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-165">**/api/holographic/os/services (GET)**</span></span>

<span data-ttu-id="93197-166">Retourne les États de tous les services en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="93197-166">Returns the states of all services running.</span></span>

<span data-ttu-id="93197-167">**/API/Holographic/OS/Settings/IPD (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-167">**/api/holographic/os/settings/ipd (GET)**</span></span>

<span data-ttu-id="93197-168">Obtient la IPD stockée (distance interpupillary) en millimètres.</span><span class="sxs-lookup"><span data-stu-id="93197-168">Gets the stored IPD (Interpupillary distance) in millimeters</span></span>

<span data-ttu-id="93197-169">**/API/Holographic/OS/Settings/IPD (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-169">**/api/holographic/os/settings/ipd (POST)**</span></span>

<span data-ttu-id="93197-170">Définit l’IPD</span><span class="sxs-lookup"><span data-stu-id="93197-170">Sets the IPD</span></span>

<span data-ttu-id="93197-171">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-171">Parameters</span></span>
* <span data-ttu-id="93197-172">IPD : nouvelle valeur IPD à définir en millimètres</span><span class="sxs-lookup"><span data-stu-id="93197-172">ipd : New IPD value to be set in millimeters</span></span>

<span data-ttu-id="93197-173">**/API/Holographic/OS/webmanagement/Settings/HTTPS (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-173">**/api/holographic/os/webmanagement/settings/https (GET)**</span></span>

<span data-ttu-id="93197-174">Obtenir la spécification HTTPS pour Device Portal</span><span class="sxs-lookup"><span data-stu-id="93197-174">Get HTTPS requirements for the Device Portal</span></span>

<span data-ttu-id="93197-175">**/API/Holographic/OS/webmanagement/Settings/HTTPS (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-175">**/api/holographic/os/webmanagement/settings/https (POST)**</span></span>

<span data-ttu-id="93197-176">Définit les exigences HTTPs pour le portail de l’appareil</span><span class="sxs-lookup"><span data-stu-id="93197-176">Sets HTTPS requirements for the Device Portal</span></span>

<span data-ttu-id="93197-177">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-177">Parameters</span></span>
* <span data-ttu-id="93197-178">obligatoire : Oui, non ou par défaut</span><span class="sxs-lookup"><span data-stu-id="93197-178">required : yes, no or default</span></span>

## <a name="holographic-perception"></a><span data-ttu-id="93197-179">Perception holographique</span><span class="sxs-lookup"><span data-stu-id="93197-179">Holographic Perception</span></span>

<span data-ttu-id="93197-180">**/API/Holographic/perception/client (obtient/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="93197-180">**/api/holographic/perception/client (GET/WebSocket)**</span></span>

<span data-ttu-id="93197-181">Accepte les mises à niveau de WebSocket et exécute un client de perception qui envoie des mises à jour à 30 i/s.</span><span class="sxs-lookup"><span data-stu-id="93197-181">Accepts websocket upgrades and runs a perception client that sends updates at 30 fps.</span></span>

<span data-ttu-id="93197-182">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-182">Parameters</span></span>
* <span data-ttu-id="93197-183">Clientmode : "active" force le mode de suivi visuel lorsqu’il ne peut pas être établi passivement</span><span class="sxs-lookup"><span data-stu-id="93197-183">clientmode: "active" forces visual tracking mode when it can't be established passively</span></span>

## <a name="holographic-thermal"></a><span data-ttu-id="93197-184">Thermique holographique</span><span class="sxs-lookup"><span data-stu-id="93197-184">Holographic Thermal</span></span>

<span data-ttu-id="93197-185">**/API/Holographic/thermal/stage (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-185">**/api/holographic/thermal/stage (GET)**</span></span>

<span data-ttu-id="93197-186">Récupération de l’étape thermique de l’appareil (0 normal, 1 chaud, 2 critique)</span><span class="sxs-lookup"><span data-stu-id="93197-186">Get the thermal stage of the device (0 normal, 1 warm, 2 critical)</span></span>

## <a name="perception-simulation-control"></a><span data-ttu-id="93197-187">Contrôle de simulation de perception</span><span class="sxs-lookup"><span data-stu-id="93197-187">Perception Simulation Control</span></span>

<span data-ttu-id="93197-188">**/API/Holographic/simulation/Control/mode (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-188">**/api/holographic/simulation/control/mode (GET)**</span></span>

<span data-ttu-id="93197-189">Obtient le mode de simulation</span><span class="sxs-lookup"><span data-stu-id="93197-189">Get the simulation mode</span></span>

<span data-ttu-id="93197-190">**/API/Holographic/simulation/Control/mode (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-190">**/api/holographic/simulation/control/mode (POST)**</span></span>

<span data-ttu-id="93197-191">Définir le mode de simulation</span><span class="sxs-lookup"><span data-stu-id="93197-191">Set the simulation mode</span></span>

<span data-ttu-id="93197-192">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-192">Parameters</span></span>
* <span data-ttu-id="93197-193">mode : mode de simulation : par défaut, simulation, distant, hérité</span><span class="sxs-lookup"><span data-stu-id="93197-193">mode : simulation mode: default, simulation, remote, legacy</span></span>

<span data-ttu-id="93197-194">**/API/Holographic/simulation/Control/Stream (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="93197-194">**/api/holographic/simulation/control/stream (DELETE)**</span></span>

<span data-ttu-id="93197-195">Supprimer un flux de contrôle.</span><span class="sxs-lookup"><span data-stu-id="93197-195">Delete a control stream.</span></span>

<span data-ttu-id="93197-196">**/API/Holographic/simulation/Control/Stream (obtient/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="93197-196">**/api/holographic/simulation/control/stream (GET/WebSocket)**</span></span>

<span data-ttu-id="93197-197">Ouvrez une connexion de socket Web pour un flux de contrôle.</span><span class="sxs-lookup"><span data-stu-id="93197-197">Open a web socket connection for a control stream.</span></span>

<span data-ttu-id="93197-198">**/API/Holographic/simulation/Control/Stream (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-198">**/api/holographic/simulation/control/stream (POST)**</span></span>

<span data-ttu-id="93197-199">Créez un flux de contrôle (priorité obligatoire) ou publiez des données dans un flux créé (streamId requis).</span><span class="sxs-lookup"><span data-stu-id="93197-199">Create a control stream (priority is required) or post data to a created stream (streamId required).</span></span> <span data-ttu-id="93197-200">Les données publiées sont supposées être de type « application/octet-stream ».</span><span class="sxs-lookup"><span data-stu-id="93197-200">Posted data is expected to be of type 'application/octet-stream'.</span></span>

<span data-ttu-id="93197-201">**/API/Holographic/Simulation/Display/Stream (obtient/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="93197-201">**/api/holographic/simulation/display/stream (GET/WebSocket)**</span></span>

<span data-ttu-id="93197-202">Demandez un flux vidéo de simulation contenant le contenu affiché sur le système lorsqu’il est en mode « simulation ».</span><span class="sxs-lookup"><span data-stu-id="93197-202">Request a simulation video stream containing the content rendered to the system display when in 'Simulation' mode.</span></span>  <span data-ttu-id="93197-203">Un en-tête de descripteur de format simple sera envoyé initialement, suivi des textures encodées H. 264, chacune précédée d’un en-tête indiquant l’index oculaire et la taille de la texture.</span><span class="sxs-lookup"><span data-stu-id="93197-203">A simple format descriptor header will be sent initially, followed by H.264-encoded textures, each preceded by a header indicating the eye index and texture size.</span></span>

## <a name="perception-simulation-playback"></a><span data-ttu-id="93197-204">Lecture de simulation de perception</span><span class="sxs-lookup"><span data-stu-id="93197-204">Perception Simulation Playback</span></span>

<span data-ttu-id="93197-205">**/API/Holographic/simulation/playback/file (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="93197-205">**/api/holographic/simulation/playback/file (DELETE)**</span></span>

<span data-ttu-id="93197-206">Supprimer un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-206">Delete a recording.</span></span>

<span data-ttu-id="93197-207">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-207">Parameters</span></span>
* <span data-ttu-id="93197-208">enregistrement : nom de l’enregistrement à supprimer.</span><span class="sxs-lookup"><span data-stu-id="93197-208">recording : Name of recording to delete.</span></span>

<span data-ttu-id="93197-209">**/API/Holographic/simulation/playback/file (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-209">**/api/holographic/simulation/playback/file (POST)**</span></span>

<span data-ttu-id="93197-210">Télécharger un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-210">Upload a recording.</span></span>

<span data-ttu-id="93197-211">**/API/Holographic/simulation/playback/Files (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-211">**/api/holographic/simulation/playback/files (GET)**</span></span>

<span data-ttu-id="93197-212">Récupération de tous les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="93197-212">Get all recordings.</span></span>

<span data-ttu-id="93197-213">**/API/Holographic/simulation/playback/session (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-213">**/api/holographic/simulation/playback/session (GET)**</span></span>

<span data-ttu-id="93197-214">Obtient l’état de lecture actuel d’un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-214">Get the current playback state of a recording.</span></span>

<span data-ttu-id="93197-215">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-215">Parameters</span></span>
* <span data-ttu-id="93197-216">enregistrement : nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-216">recording : Name of recording.</span></span>

<span data-ttu-id="93197-217">**/API/Holographic/simulation/playback/session/file (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="93197-217">**/api/holographic/simulation/playback/session/file (DELETE)**</span></span>

<span data-ttu-id="93197-218">Décharger un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-218">Unload a recording.</span></span>

<span data-ttu-id="93197-219">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-219">Parameters</span></span>
* <span data-ttu-id="93197-220">enregistrement : nom de l’enregistrement à décharger.</span><span class="sxs-lookup"><span data-stu-id="93197-220">recording : Name of recording to unload.</span></span>

<span data-ttu-id="93197-221">**/API/Holographic/simulation/playback/session/file (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-221">**/api/holographic/simulation/playback/session/file (POST)**</span></span>

<span data-ttu-id="93197-222">Charger un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-222">Load a recording.</span></span>

<span data-ttu-id="93197-223">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-223">Parameters</span></span>
* <span data-ttu-id="93197-224">enregistrement : nom de l’enregistrement à charger.</span><span class="sxs-lookup"><span data-stu-id="93197-224">recording : Name of recording to load.</span></span>

<span data-ttu-id="93197-225">**/API/Holographic/simulation/playback/session/Files (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-225">**/api/holographic/simulation/playback/session/files (GET)**</span></span>

<span data-ttu-id="93197-226">Récupération de tous les enregistrements chargés.</span><span class="sxs-lookup"><span data-stu-id="93197-226">Get all loaded recordings.</span></span>

<span data-ttu-id="93197-227">**/API/Holographic/simulation/playback/session/pause (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-227">**/api/holographic/simulation/playback/session/pause (POST)**</span></span>

<span data-ttu-id="93197-228">Suspendre un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-228">Pause a recording.</span></span>

<span data-ttu-id="93197-229">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-229">Parameters</span></span>
* <span data-ttu-id="93197-230">enregistrement : nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-230">recording : Name of recording.</span></span>

<span data-ttu-id="93197-231">**/API/Holographic/simulation/playback/session/Play (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-231">**/api/holographic/simulation/playback/session/play (POST)**</span></span>

<span data-ttu-id="93197-232">Lire un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-232">Play a recording.</span></span>

<span data-ttu-id="93197-233">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-233">Parameters</span></span>
* <span data-ttu-id="93197-234">enregistrement : nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-234">recording : Name of recording.</span></span>

<span data-ttu-id="93197-235">**/API/Holographic/simulation/playback/session/Stop (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-235">**/api/holographic/simulation/playback/session/stop (POST)**</span></span>

<span data-ttu-id="93197-236">Arrêter un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-236">Stop a recording.</span></span>

<span data-ttu-id="93197-237">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-237">Parameters</span></span>
* <span data-ttu-id="93197-238">enregistrement : nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-238">recording : Name of recording.</span></span>

<span data-ttu-id="93197-239">**/API/Holographic/simulation/playback/session/types (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-239">**/api/holographic/simulation/playback/session/types (GET)**</span></span>

<span data-ttu-id="93197-240">Obtenir les types de données dans un enregistrement chargé.</span><span class="sxs-lookup"><span data-stu-id="93197-240">Get the types of data in a loaded recording.</span></span>

<span data-ttu-id="93197-241">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-241">Parameters</span></span>
* <span data-ttu-id="93197-242">enregistrement : nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-242">recording : Name of recording.</span></span>

## <a name="perception-simulation-recording"></a><span data-ttu-id="93197-243">Enregistrement de simulation de perception</span><span class="sxs-lookup"><span data-stu-id="93197-243">Perception Simulation Recording</span></span>

<span data-ttu-id="93197-244">**/API/Holographic/simulation/Recording/Start (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-244">**/api/holographic/simulation/recording/start (POST)**</span></span>

<span data-ttu-id="93197-245">Démarrez un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-245">Start a recording.</span></span> <span data-ttu-id="93197-246">Un seul enregistrement peut être actif à la fois.</span><span class="sxs-lookup"><span data-stu-id="93197-246">Only a single recording can be active at once.</span></span> <span data-ttu-id="93197-247">Vous devez définir l’un des principaux, mains, spatialMapping ou environnement.</span><span class="sxs-lookup"><span data-stu-id="93197-247">One of head, hands, spatialMapping or environment must be set.</span></span>

<span data-ttu-id="93197-248">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-248">Parameters</span></span>
* <span data-ttu-id="93197-249">Head : définissez sur 1 pour enregistrer les données de tête.</span><span class="sxs-lookup"><span data-stu-id="93197-249">head : Set to 1 to record head data.</span></span>
* <span data-ttu-id="93197-250">mains : définissez sur 1 pour enregistrer les données de la main.</span><span class="sxs-lookup"><span data-stu-id="93197-250">hands : Set to 1 to record hand data.</span></span>
* <span data-ttu-id="93197-251">spatialMapping : affectez la valeur 1 pour enregistrer le mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="93197-251">spatialMapping : Set to 1 to record spatial mapping.</span></span>
* <span data-ttu-id="93197-252">environnement : définissez sur 1 pour enregistrer les données d’environnement.</span><span class="sxs-lookup"><span data-stu-id="93197-252">environment : Set to 1 to record environment data.</span></span>
* <span data-ttu-id="93197-253">nom : nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-253">name : Name of the recording.</span></span>
* <span data-ttu-id="93197-254">singleSpatialMappingFrame : affectez la valeur 1 pour enregistrer uniquement un seul frame de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="93197-254">singleSpatialMappingFrame : Set to 1 to record only a single spatial mapping frame.</span></span>

<span data-ttu-id="93197-255">**/API/Holographic/simulation/Recording/Status (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-255">**/api/holographic/simulation/recording/status (GET)**</span></span>

<span data-ttu-id="93197-256">Obtient l’état de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93197-256">Get recording state.</span></span>

<span data-ttu-id="93197-257">**/API/Holographic/simulation/Recording/Stop (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-257">**/api/holographic/simulation/recording/stop (GET)**</span></span>

<span data-ttu-id="93197-258">Arrêter l’enregistrement en cours.</span><span class="sxs-lookup"><span data-stu-id="93197-258">Stop the current recording.</span></span> <span data-ttu-id="93197-259">L’enregistrement est retourné sous la forme d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="93197-259">Recording will be returned as a file.</span></span>

## <a name="mixed-reality-capture"></a><span data-ttu-id="93197-260">MRC (Mixed Reality Capture)</span><span class="sxs-lookup"><span data-stu-id="93197-260">Mixed Reality Capture</span></span>

<span data-ttu-id="93197-261">**/API/Holographic/MRC/file (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-261">**/api/holographic/mrc/file (GET)**</span></span>

<span data-ttu-id="93197-262">Télécharge un fichier de réalité mixte à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="93197-262">Downloads a mixed reality file from the device.</span></span> <span data-ttu-id="93197-263">Utilisez le paramètre de requête op = Stream pour la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="93197-263">Use op=stream query parameter for streaming.</span></span>

<span data-ttu-id="93197-264">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-264">Parameters</span></span>
* <span data-ttu-id="93197-265">nom de fichier : nom, hex64 encodé, du fichier vidéo à récupérer</span><span class="sxs-lookup"><span data-stu-id="93197-265">filename : Name, hex64 encoded, of the video file to get</span></span>
* <span data-ttu-id="93197-266">OP : flux</span><span class="sxs-lookup"><span data-stu-id="93197-266">op : stream</span></span>

<span data-ttu-id="93197-267">**/API/Holographic/MRC/file (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="93197-267">**/api/holographic/mrc/file (DELETE)**</span></span>

<span data-ttu-id="93197-268">Supprime un enregistrement de la réalité mixte de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="93197-268">Deletes a mixed reality recording from the device.</span></span>

<span data-ttu-id="93197-269">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-269">Parameters</span></span>
* <span data-ttu-id="93197-270">nom de fichier : nom, hex64 encodé, du fichier à supprimer</span><span class="sxs-lookup"><span data-stu-id="93197-270">filename : Name, hex64 encoded, of the file to delete</span></span>

<span data-ttu-id="93197-271">**/API/Holographic/MRC/Files (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-271">**/api/holographic/mrc/files (GET)**</span></span>

<span data-ttu-id="93197-272">Retourne la liste des fichiers de réalité mixte stockés sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="93197-272">Returns the list of mixed reality files stored on the device</span></span>

<span data-ttu-id="93197-273">**/API/Holographic/MRC/photo (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-273">**/api/holographic/mrc/photo (POST)**</span></span>

<span data-ttu-id="93197-274">Prend une photo de réalité mixte et crée un fichier sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="93197-274">Takes a mixed reality photo and creates a file on the device</span></span>

<span data-ttu-id="93197-275">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-275">Parameters</span></span>
* <span data-ttu-id="93197-276">Holo : capturer les hologrammes : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-276">holo : capture holograms: true or false (defaults to false)</span></span>
* <span data-ttu-id="93197-277">PV : capturer l’appareil photo PV : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-277">pv : capture PV camera: true or false (defaults to false)</span></span>
* <span data-ttu-id="93197-278">RenderFromCamera : (HoloLens 2 uniquement) rendu du point de vue de la caméra photo/vidéo : true ou false (true par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-278">RenderFromCamera : (HoloLens 2 only) render from perspective of photo/video camera: true or false (defaults to true)</span></span>

<span data-ttu-id="93197-279">**/API/Holographic/MRC/Settings (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-279">**/api/holographic/mrc/settings (GET)**</span></span>

<span data-ttu-id="93197-280">Obtient les paramètres de capture de la réalité mixte par défaut</span><span class="sxs-lookup"><span data-stu-id="93197-280">Gets the default mixed reality capture settings</span></span>

<span data-ttu-id="93197-281">**/API/Holographic/MRC/Settings (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-281">**/api/holographic/mrc/settings (POST)**</span></span>

<span data-ttu-id="93197-282">Définit les paramètres de capture de la réalité mixte par défaut.</span><span class="sxs-lookup"><span data-stu-id="93197-282">Sets the default mixed reality capture settings.</span></span>  <span data-ttu-id="93197-283">Certains de ces paramètres sont appliqués à la photo et à la capture de vidéo MRC du système.</span><span class="sxs-lookup"><span data-stu-id="93197-283">Some of these settings are applied to the system's MRC photo and video capture.</span></span>

<span data-ttu-id="93197-284">**/API/Holographic/MRC/Status (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-284">**/api/holographic/mrc/status (GET)**</span></span>

<span data-ttu-id="93197-285">Obtient l’état de capture de la réalité mixte dans le portail de périphériques Windows.</span><span class="sxs-lookup"><span data-stu-id="93197-285">Gets the state of mixed reality capture within the Windows Device Portal.</span></span>

<span data-ttu-id="93197-286">***Réponse***</span><span class="sxs-lookup"><span data-stu-id="93197-286">***Response***</span></span>

<span data-ttu-id="93197-287">La réponse contient une propriété JSON indiquant si le portail de périphériques Windows enregistre ou non une vidéo.</span><span class="sxs-lookup"><span data-stu-id="93197-287">The response contains a JSON property indicating if Windows Device Portal is recording video or not.</span></span>

``` javascript
{"IsRecording" : boolean}
```

<span data-ttu-id="93197-288">**/API/Holographic/MRC/thumbnail (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-288">**/api/holographic/mrc/thumbnail (GET)**</span></span>

<span data-ttu-id="93197-289">Obtient l’image miniature pour le fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="93197-289">Gets the thumbnail image for the specified file.</span></span>

<span data-ttu-id="93197-290">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-290">Parameters</span></span>
* <span data-ttu-id="93197-291">nom de fichier : nom, hex64 encodé, du fichier pour lequel la miniature est demandée.</span><span class="sxs-lookup"><span data-stu-id="93197-291">filename: Name, hex64 encoded, of the file for which the thumbnail is being requested</span></span>

<span data-ttu-id="93197-292">**/API/Holographic/MRC/Video/Control/Start (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-292">**/api/holographic/mrc/video/control/start (POST)**</span></span>

<span data-ttu-id="93197-293">Démarre un enregistrement de la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="93197-293">Starts a mixed reality recording</span></span>

<span data-ttu-id="93197-294">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-294">Parameters</span></span>
* <span data-ttu-id="93197-295">Holo : capturer les hologrammes : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-295">holo : capture holograms: true or false (defaults to false)</span></span>
* <span data-ttu-id="93197-296">PV : capturer l’appareil photo PV : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-296">pv : capture PV camera: true or false (defaults to false)</span></span>
* <span data-ttu-id="93197-297">MIC : capturer le microphone : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-297">mic : capture microphone: true or false (defaults to false)</span></span>
* <span data-ttu-id="93197-298">loopback : capturer l’audio de l’application : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-298">loopback : capture app audio: true or false (defaults to false)</span></span>
* <span data-ttu-id="93197-299">RenderFromCamera : (HoloLens 2 uniquement) rendu du point de vue de la caméra photo/vidéo : true ou false (true par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-299">RenderFromCamera : (HoloLens 2 only) render from perspective of photo/video camera: true or false (defaults to true)</span></span>
* <span data-ttu-id="93197-300">Vstab : (HoloLens 2 uniquement) activer la stabilisation vidéo : true ou false (true par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-300">vstab : (HoloLens 2 only) enable video stabilization: true or false (defaults to true)</span></span>
* <span data-ttu-id="93197-301">vstabbuffer : (HoloLens 2 uniquement) latence de la mémoire tampon de stabilisation vidéo : de 0 à 30 frames (15 images par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-301">vstabbuffer: (HoloLens 2 only) video stabilization buffer latency: 0 to 30 frames (defaults to 15 frames)</span></span>

<span data-ttu-id="93197-302">**/API/Holographic/MRC/Video/Control/Stop (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-302">**/api/holographic/mrc/video/control/stop (POST)**</span></span>

<span data-ttu-id="93197-303">Arrête l’enregistrement de la réalité mixte actuelle</span><span class="sxs-lookup"><span data-stu-id="93197-303">Stops the current mixed reality recording</span></span>

## <a name="mixed-reality-streaming"></a><span data-ttu-id="93197-304">Diffusion en continu de la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="93197-304">Mixed Reality Streaming</span></span>

<span data-ttu-id="93197-305">HoloLens prend en charge l’aperçu instantané de la réalité mixte via le téléchargement segmenté d’un MP4 fragmenté.</span><span class="sxs-lookup"><span data-stu-id="93197-305">HoloLens supports live preview of mixed reality via chunked download of a fragmented mp4.</span></span>

<span data-ttu-id="93197-306">Les flux de réalité mixte partagent le même ensemble de paramètres pour contrôler ce qui est capturé :</span><span class="sxs-lookup"><span data-stu-id="93197-306">Mixed reality streams share the same set of parameters to control what is captured:</span></span>
* <span data-ttu-id="93197-307">Holo : capturer les hologrammes : true ou false</span><span class="sxs-lookup"><span data-stu-id="93197-307">holo : capture holograms: true or false</span></span>
* <span data-ttu-id="93197-308">PV : capturer l’appareil photo PV : true ou false</span><span class="sxs-lookup"><span data-stu-id="93197-308">pv : capture PV camera: true or false</span></span>
* <span data-ttu-id="93197-309">MIC : capturer le microphone : true ou false</span><span class="sxs-lookup"><span data-stu-id="93197-309">mic : capture microphone: true or false</span></span>
* <span data-ttu-id="93197-310">loopback : capturer l’audio de l’application : true ou false</span><span class="sxs-lookup"><span data-stu-id="93197-310">loopback : capture app audio: true or false</span></span>

<span data-ttu-id="93197-311">Si aucun de ces éléments n’est spécifié : les hologrammes, la caméra photo/vidéo et l’audio de l’application sont capturés</span><span class="sxs-lookup"><span data-stu-id="93197-311">If none of these are specified: holograms, photo/video camera, and app audio will be captured</span></span><br>
<span data-ttu-id="93197-312">Si des paramètres sont spécifiés : les paramètres non spécifiés ont par défaut la valeur false</span><span class="sxs-lookup"><span data-stu-id="93197-312">If any are specified: the unspecified parameters will default to false</span></span>

<span data-ttu-id="93197-313">Paramètres facultatifs (HoloLens 2 uniquement)</span><span class="sxs-lookup"><span data-stu-id="93197-313">Optional parameters (HoloLens 2 only)</span></span>
* <span data-ttu-id="93197-314">RenderFromCamera : rendu du point de vue de la caméra photo/vidéo : true ou false (true par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-314">RenderFromCamera : render from perspective of photo/video camera: true or false (defaults to true)</span></span>
* <span data-ttu-id="93197-315">Vstab : activer la stabilisation vidéo : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-315">vstab : enable video stabilization: true or false (defaults to false)</span></span>
* <span data-ttu-id="93197-316">vstabbuffer : latence de la mémoire tampon de stabilisation vidéo : de 0 à 30 frames (15 images par défaut)</span><span class="sxs-lookup"><span data-stu-id="93197-316">vstabbuffer: video stabilization buffer latency: 0 to 30 frames (defaults to 15 frames)</span></span>

<span data-ttu-id="93197-317">**/API/Holographic/Stream/live.mp4 (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-317">**/api/holographic/stream/live.mp4 (GET)**</span></span>

<span data-ttu-id="93197-318">Un flux 1280x720p 30fps 5Mbit.</span><span class="sxs-lookup"><span data-stu-id="93197-318">A 1280x720p 30fps 5Mbit stream.</span></span>

<span data-ttu-id="93197-319">**/API/Holographic/Stream/live_high.mp4 (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-319">**/api/holographic/stream/live_high.mp4 (GET)**</span></span>

<span data-ttu-id="93197-320">Un flux 1280x720p 30fps 5Mbit.</span><span class="sxs-lookup"><span data-stu-id="93197-320">A 1280x720p 30fps 5Mbit stream.</span></span>

<span data-ttu-id="93197-321">**/API/Holographic/Stream/live_med.mp4 (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-321">**/api/holographic/stream/live_med.mp4 (GET)**</span></span>

<span data-ttu-id="93197-322">Flux 854x480p 30fps 2,5 Mbits.</span><span class="sxs-lookup"><span data-stu-id="93197-322">A 854x480p 30fps 2.5Mbit stream.</span></span>

<span data-ttu-id="93197-323">**/API/Holographic/Stream/live_low.mp4 (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-323">**/api/holographic/stream/live_low.mp4 (GET)**</span></span>

<span data-ttu-id="93197-324">Flux 428x240p 15fps 0,6 Mbit.</span><span class="sxs-lookup"><span data-stu-id="93197-324">A 428x240p 15fps 0.6Mbit stream.</span></span>

## <a name="networking"></a><span data-ttu-id="93197-325">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="93197-325">Networking</span></span>

<span data-ttu-id="93197-326">**/API/Networking/ipconfig (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-326">**/api/networking/ipconfig (GET)**</span></span>

<span data-ttu-id="93197-327">Obtient la configuration IP actuelle</span><span class="sxs-lookup"><span data-stu-id="93197-327">Gets the current ip configuration</span></span>

## <a name="os-information"></a><span data-ttu-id="93197-328">Informations sur le système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="93197-328">OS Information</span></span>

<span data-ttu-id="93197-329">**/API/OS/info (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-329">**/api/os/info (GET)**</span></span>

<span data-ttu-id="93197-330">Obtient des informations sur le système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="93197-330">Gets operating system information</span></span>

<span data-ttu-id="93197-331">**/API/OS/MachineName (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-331">**/api/os/machinename (GET)**</span></span>

<span data-ttu-id="93197-332">Obtient le nom de l’ordinateur</span><span class="sxs-lookup"><span data-stu-id="93197-332">Gets the machine name</span></span>

<span data-ttu-id="93197-333">**/API/OS/MachineName (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-333">**/api/os/machinename (POST)**</span></span>

<span data-ttu-id="93197-334">Définit le nom de l’ordinateur</span><span class="sxs-lookup"><span data-stu-id="93197-334">Sets the machine name</span></span>

<span data-ttu-id="93197-335">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-335">Parameters</span></span>
* <span data-ttu-id="93197-336">nom : nouveau nom de l’ordinateur, hex64 encodé, à affecter à</span><span class="sxs-lookup"><span data-stu-id="93197-336">name : New machine name, hex64 encoded, to set to</span></span>

## <a name="performance-data"></a><span data-ttu-id="93197-337">Données de performances</span><span class="sxs-lookup"><span data-stu-id="93197-337">Performance data</span></span>

<span data-ttu-id="93197-338">**/API/ResourceManager/Processes (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-338">**/api/resourcemanager/processes (GET)**</span></span>

<span data-ttu-id="93197-339">Retourne la liste des processus en cours d’exécution avec les détails</span><span class="sxs-lookup"><span data-stu-id="93197-339">Returns the list of running processes with details</span></span>

<span data-ttu-id="93197-340">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-340">Return data</span></span>
* <span data-ttu-id="93197-341">JSON avec liste de processus et détails pour chaque processus</span><span class="sxs-lookup"><span data-stu-id="93197-341">JSON with list of processes and details for each process</span></span>

<span data-ttu-id="93197-342">**/API/ResourceManager/systemperf (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-342">**/api/resourcemanager/systemperf (GET)**</span></span>

<span data-ttu-id="93197-343">Retourne les statistiques de performances système (lecture/écriture d’e/s, statistiques de mémoire, etc.).</span><span class="sxs-lookup"><span data-stu-id="93197-343">Returns system perf statistics (I/O read/write, memory stats etc.</span></span>

<span data-ttu-id="93197-344">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-344">Return data</span></span>
* <span data-ttu-id="93197-345">JSON avec informations système : processeur, GPU, mémoire, réseau, e/s</span><span class="sxs-lookup"><span data-stu-id="93197-345">JSON with system information: CPU, GPU, Memory, Network, IO</span></span>

## <a name="power"></a><span data-ttu-id="93197-346">Avancé</span><span class="sxs-lookup"><span data-stu-id="93197-346">Power</span></span>

<span data-ttu-id="93197-347">**/API/Power/Battery (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-347">**/api/power/battery (GET)**</span></span>

<span data-ttu-id="93197-348">Obtient l’état actuel de la batterie</span><span class="sxs-lookup"><span data-stu-id="93197-348">Gets the current battery state</span></span>

<span data-ttu-id="93197-349">**/API/Power/State (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-349">**/api/power/state (GET)**</span></span>

<span data-ttu-id="93197-350">Vérifie si le système est dans un état de faible consommation d’énergie.</span><span class="sxs-lookup"><span data-stu-id="93197-350">Checks if the system is in a low power state</span></span>

## <a name="remote-control"></a><span data-ttu-id="93197-351">Contrôle à distance</span><span class="sxs-lookup"><span data-stu-id="93197-351">Remote Control</span></span>

<span data-ttu-id="93197-352">**/API/Control/Restart (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-352">**/api/control/restart (POST)**</span></span>

<span data-ttu-id="93197-353">Redémarre l’appareil cible</span><span class="sxs-lookup"><span data-stu-id="93197-353">Restarts the target device</span></span>

<span data-ttu-id="93197-354">**/API/Control/Shutdown (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-354">**/api/control/shutdown (POST)**</span></span>

<span data-ttu-id="93197-355">Arrête l’appareil cible</span><span class="sxs-lookup"><span data-stu-id="93197-355">Shuts down the target device</span></span>

## <a name="task-manager"></a><span data-ttu-id="93197-356">Gestionnaire des tâches</span><span class="sxs-lookup"><span data-stu-id="93197-356">Task Manager</span></span>

<span data-ttu-id="93197-357">**/API/taskmanager/App (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="93197-357">**/api/taskmanager/app (DELETE)**</span></span>

<span data-ttu-id="93197-358">Arrête une application moderne</span><span class="sxs-lookup"><span data-stu-id="93197-358">Stops a modern app</span></span>

<span data-ttu-id="93197-359">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-359">Parameters</span></span>
* <span data-ttu-id="93197-360">Package : nom complet du package d’application, hex64 encodé</span><span class="sxs-lookup"><span data-stu-id="93197-360">package : Full name of the app package, hex64 encoded</span></span>
* <span data-ttu-id="93197-361">forceStop : force l’arrêt de tous les processus (= oui)</span><span class="sxs-lookup"><span data-stu-id="93197-361">forcestop : Force all processes to stop (=yes)</span></span>

<span data-ttu-id="93197-362">**/API/taskmanager/App (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-362">**/api/taskmanager/app (POST)**</span></span>

<span data-ttu-id="93197-363">Démarre une application moderne</span><span class="sxs-lookup"><span data-stu-id="93197-363">Starts a modern app</span></span>

<span data-ttu-id="93197-364">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-364">Parameters</span></span>
* <span data-ttu-id="93197-365">AppID : PRAID de l’application à démarrer, hex64 encodé</span><span class="sxs-lookup"><span data-stu-id="93197-365">appid : PRAID of app to start, hex64 encoded</span></span>
* <span data-ttu-id="93197-366">Package : nom complet du package d’application, hex64 encodé</span><span class="sxs-lookup"><span data-stu-id="93197-366">package : Full name of the app package, hex64 encoded</span></span>

## <a name="wifi-management"></a><span data-ttu-id="93197-367">Gestion WiFi</span><span class="sxs-lookup"><span data-stu-id="93197-367">WiFi Management</span></span>

<span data-ttu-id="93197-368">**/API/WiFi/interfaces (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-368">**/api/wifi/interfaces (GET)**</span></span>

<span data-ttu-id="93197-369">Énumère les interfaces de réseau sans fil</span><span class="sxs-lookup"><span data-stu-id="93197-369">Enumerates wireless network interfaces</span></span>

<span data-ttu-id="93197-370">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-370">Return data</span></span>
* <span data-ttu-id="93197-371">Liste des interfaces sans fil avec des détails (GUID, description, etc.)</span><span class="sxs-lookup"><span data-stu-id="93197-371">List of wireless interfaces with details (GUID, description etc.)</span></span>

<span data-ttu-id="93197-372">**/API/WiFi/Network (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="93197-372">**/api/wifi/network (DELETE)**</span></span>

<span data-ttu-id="93197-373">Supprime un profil associé à un réseau sur une interface spécifiée</span><span class="sxs-lookup"><span data-stu-id="93197-373">Deletes a profile associated with a network on a specified interface</span></span>

<span data-ttu-id="93197-374">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-374">Parameters</span></span>
* <span data-ttu-id="93197-375">Interface : GUID de l’interface réseau</span><span class="sxs-lookup"><span data-stu-id="93197-375">interface : network interface guid</span></span>
* <span data-ttu-id="93197-376">Profil : nom du profil</span><span class="sxs-lookup"><span data-stu-id="93197-376">profile : profile name</span></span>

<span data-ttu-id="93197-377">**/API/WiFi/Networks (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-377">**/api/wifi/networks (GET)**</span></span>

<span data-ttu-id="93197-378">Énumère les réseaux sans fil sur l’interface réseau spécifiée.</span><span class="sxs-lookup"><span data-stu-id="93197-378">Enumerates wireless networks on the specified network interface</span></span>

<span data-ttu-id="93197-379">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-379">Parameters</span></span>
* <span data-ttu-id="93197-380">Interface : GUID de l’interface réseau</span><span class="sxs-lookup"><span data-stu-id="93197-380">interface : network interface guid</span></span>

<span data-ttu-id="93197-381">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-381">Return data</span></span>
* <span data-ttu-id="93197-382">Liste des réseaux sans fil détectés sur l’interface réseau avec les détails</span><span class="sxs-lookup"><span data-stu-id="93197-382">List of wireless networks found on the network interface with details</span></span>

<span data-ttu-id="93197-383">**/API/WiFi/Network (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-383">**/api/wifi/network (POST)**</span></span>

<span data-ttu-id="93197-384">Se connecte ou se déconnecte à un réseau sur l’interface spécifiée</span><span class="sxs-lookup"><span data-stu-id="93197-384">Connects or disconnects to a network on the specified interface</span></span>

<span data-ttu-id="93197-385">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-385">Parameters</span></span>
* <span data-ttu-id="93197-386">Interface : GUID de l’interface réseau</span><span class="sxs-lookup"><span data-stu-id="93197-386">interface : network interface guid</span></span>
* <span data-ttu-id="93197-387">SSID : SSID, hex64 encodé, pour se connecter à</span><span class="sxs-lookup"><span data-stu-id="93197-387">ssid : ssid, hex64 encoded, to connect to</span></span>
* <span data-ttu-id="93197-388">opération : se connecter ou se déconnecter</span><span class="sxs-lookup"><span data-stu-id="93197-388">op : connect or disconnect</span></span>
* <span data-ttu-id="93197-389">CreateProfile : oui ou non</span><span class="sxs-lookup"><span data-stu-id="93197-389">createprofile : yes or no</span></span>
* <span data-ttu-id="93197-390">clé : clé partagée, encodée en hex64</span><span class="sxs-lookup"><span data-stu-id="93197-390">key : shared key, hex64 encoded</span></span>

## <a name="windows-performance-recorder"></a><span data-ttu-id="93197-391">Enregistreur de performances Windows</span><span class="sxs-lookup"><span data-stu-id="93197-391">Windows Performance Recorder</span></span>

<span data-ttu-id="93197-392">**/API/WPR/customtrace (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-392">**/api/wpr/customtrace (POST)**</span></span>

<span data-ttu-id="93197-393">Charge un profil WPR et démarre le suivi à l’aide du profil chargé.</span><span class="sxs-lookup"><span data-stu-id="93197-393">Uploads a WPR profile and starts tracing using the uploaded profile.</span></span>

<span data-ttu-id="93197-394">Payload</span><span class="sxs-lookup"><span data-stu-id="93197-394">Payload</span></span>
* <span data-ttu-id="93197-395">corps http en plusieurs parties, conforme</span><span class="sxs-lookup"><span data-stu-id="93197-395">multi-part conforming http body</span></span>

<span data-ttu-id="93197-396">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-396">Return data</span></span>
* <span data-ttu-id="93197-397">Retourne l’état de la session WPR.</span><span class="sxs-lookup"><span data-stu-id="93197-397">Returns the WPR session status.</span></span>

<span data-ttu-id="93197-398">**/API/WPR/Status (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-398">**/api/wpr/status (GET)**</span></span>

<span data-ttu-id="93197-399">Récupère l’état de la session WPR</span><span class="sxs-lookup"><span data-stu-id="93197-399">Retrieves the status of the WPR session</span></span>

<span data-ttu-id="93197-400">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-400">Return data</span></span>
* <span data-ttu-id="93197-401">État de session WPR.</span><span class="sxs-lookup"><span data-stu-id="93197-401">WPR session status.</span></span>

<span data-ttu-id="93197-402">**/API/WPR/trace (récupération)**</span><span class="sxs-lookup"><span data-stu-id="93197-402">**/api/wpr/trace (GET)**</span></span>

<span data-ttu-id="93197-403">Arrête une session de suivi WPR (performance)</span><span class="sxs-lookup"><span data-stu-id="93197-403">Stops a WPR (performance) tracing session</span></span>

<span data-ttu-id="93197-404">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-404">Return data</span></span>
* <span data-ttu-id="93197-405">Retourne le fichier ETL de trace</span><span class="sxs-lookup"><span data-stu-id="93197-405">Returns the trace ETL file</span></span>

<span data-ttu-id="93197-406">**/API/WPR/trace (publication)**</span><span class="sxs-lookup"><span data-stu-id="93197-406">**/api/wpr/trace (POST)**</span></span>

<span data-ttu-id="93197-407">Démarre une session de suivi WPR (performance)</span><span class="sxs-lookup"><span data-stu-id="93197-407">Starts a WPR (performance) tracing sessions</span></span>

<span data-ttu-id="93197-408">Paramètres</span><span class="sxs-lookup"><span data-stu-id="93197-408">Parameters</span></span>
* <span data-ttu-id="93197-409">Profil : nom du profil.</span><span class="sxs-lookup"><span data-stu-id="93197-409">profile : Profile name.</span></span> <span data-ttu-id="93197-410">Les profils disponibles sont stockés dans perfprofiles/profiles.jssur</span><span class="sxs-lookup"><span data-stu-id="93197-410">Available profiles are stored in perfprofiles/profiles.json</span></span>

<span data-ttu-id="93197-411">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="93197-411">Return data</span></span>
* <span data-ttu-id="93197-412">Dans Démarrer, retourne l’état de la session WPR.</span><span class="sxs-lookup"><span data-stu-id="93197-412">On start, returns the WPR session status.</span></span>

## <a name="see-also"></a><span data-ttu-id="93197-413">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="93197-413">See also</span></span>
* [<span data-ttu-id="93197-414">Utilisation du portail d’appareil Windows</span><span class="sxs-lookup"><span data-stu-id="93197-414">Using the Windows Device Portal</span></span>](using-the-windows-device-portal.md)
* [<span data-ttu-id="93197-415">Informations de référence sur l’API principale du portail des appareils (UWP)</span><span class="sxs-lookup"><span data-stu-id="93197-415">Device Portal core API reference (UWP)</span></span>](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-api-core)
