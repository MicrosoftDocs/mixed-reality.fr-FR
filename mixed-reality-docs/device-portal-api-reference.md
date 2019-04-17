---
title: Portail de référence de l’API des appareils
description: Référence des API pour le Windows Device Portal sur HoloLens
author: JonMLyons
ms.author: JLyons
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, Windows Device Portal, API
ms.openlocfilehash: 507ab98734adea80d0aad41d99124e3d91846f28
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596065"
---
# <a name="device-portal-api-reference"></a><span data-ttu-id="3f274-104">Portail de référence de l’API des appareils</span><span class="sxs-lookup"><span data-stu-id="3f274-104">Device portal API reference</span></span>

<span data-ttu-id="3f274-105">Tous les éléments de la [Windows Device Portal](using-the-windows-device-portal.md) se trouve au sommet de l’API REST que vous pouvez utiliser pour accéder aux données et de contrôler par programmation de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="3f274-105">Everything in the [Windows Device Portal](using-the-windows-device-portal.md) is built on top of REST API's that you can use to access the data and control your device programmatically.</span></span>

## <a name="app-deloyment"></a><span data-ttu-id="3f274-106">Application deloyment</span><span class="sxs-lookup"><span data-stu-id="3f274-106">App deloyment</span></span>

<span data-ttu-id="3f274-107">**/API/App/PackageManager/package (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="3f274-107">**/api/app/packagemanager/package (DELETE)**</span></span>

<span data-ttu-id="3f274-108">Désinstalle une application</span><span class="sxs-lookup"><span data-stu-id="3f274-108">Uninstalls an app</span></span>

<span data-ttu-id="3f274-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-109">Parameters</span></span>
* <span data-ttu-id="3f274-110">package : Nom de fichier du package doit être désinstallé.</span><span class="sxs-lookup"><span data-stu-id="3f274-110">package : File name of the package to be uninstalled.</span></span>

<span data-ttu-id="3f274-111">**/API/App/PackageManager/package (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-111">**/api/app/packagemanager/package (POST)**</span></span>

<span data-ttu-id="3f274-112">Installe une application</span><span class="sxs-lookup"><span data-stu-id="3f274-112">Installs an App</span></span>

<span data-ttu-id="3f274-113">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-113">Parameters</span></span>
* <span data-ttu-id="3f274-114">package : Nom de fichier du package doit être installé.</span><span class="sxs-lookup"><span data-stu-id="3f274-114">package : File name of the package to be installed.</span></span>

<span data-ttu-id="3f274-115">charge utile</span><span class="sxs-lookup"><span data-stu-id="3f274-115">Payload</span></span>
* <span data-ttu-id="3f274-116">corps http conforme à plusieurs parties</span><span class="sxs-lookup"><span data-stu-id="3f274-116">multi-part conforming http body</span></span>

<span data-ttu-id="3f274-117">**/API/App/PackageManager/packages (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-117">**/api/app/packagemanager/packages (GET)**</span></span>

<span data-ttu-id="3f274-118">Récupère la liste des applications installées sur le système, avec les détails</span><span class="sxs-lookup"><span data-stu-id="3f274-118">Retrieves the list of installed apps on the system, with details</span></span>

<span data-ttu-id="3f274-119">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-119">Return data</span></span>
* <span data-ttu-id="3f274-120">Liste des packages installés avec les détails</span><span class="sxs-lookup"><span data-stu-id="3f274-120">List of installed packages with details</span></span>

<span data-ttu-id="3f274-121">**/API/App/PackageManager/State (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-121">**/api/app/packagemanager/state (GET)**</span></span>

<span data-ttu-id="3f274-122">Obtient l’état de dans l’installation de l’application progression</span><span class="sxs-lookup"><span data-stu-id="3f274-122">Gets the status of in progress app installation</span></span>

## <a name="dump-collection"></a><span data-ttu-id="3f274-123">Collection de vidages</span><span class="sxs-lookup"><span data-stu-id="3f274-123">Dump collection</span></span>

<span data-ttu-id="3f274-124">**/API/Debug/dump/UserMode/CrashControl (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="3f274-124">**/api/debug/dump/usermode/crashcontrol (DELETE)**</span></span>

<span data-ttu-id="3f274-125">Désactive crash collecte des vidages pour une application chargée indépendamment</span><span class="sxs-lookup"><span data-stu-id="3f274-125">Disables crash dump collection for a sideloaded app</span></span>

<span data-ttu-id="3f274-126">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-126">Parameters</span></span>
* <span data-ttu-id="3f274-127">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="3f274-127">packageFullname : package name</span></span>

<span data-ttu-id="3f274-128">**/API/Debug/dump/UserMode/CrashControl (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-128">**/api/debug/dump/usermode/crashcontrol (GET)**</span></span>

<span data-ttu-id="3f274-129">Obtient les paramètres pour les applications de chargement de version test collecte des vidages sur incident</span><span class="sxs-lookup"><span data-stu-id="3f274-129">Gets settings for sideloaded apps crash dump collection</span></span>

<span data-ttu-id="3f274-130">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-130">Parameters</span></span>
* <span data-ttu-id="3f274-131">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="3f274-131">packageFullname : package name</span></span>

<span data-ttu-id="3f274-132">**/api/debug/dump/usermode/crashcontrol (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-132">**/api/debug/dump/usermode/crashcontrol (POST)**</span></span>

<span data-ttu-id="3f274-133">Active et configure les paramètres de contrôle d’image pour une application chargée indépendamment</span><span class="sxs-lookup"><span data-stu-id="3f274-133">Enables and sets dump control settings for a sideloaded app</span></span>

<span data-ttu-id="3f274-134">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-134">Parameters</span></span>
* <span data-ttu-id="3f274-135">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="3f274-135">packageFullname : package name</span></span>

<span data-ttu-id="3f274-136">**/API/Debug/dump/UserMode/crashdump (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="3f274-136">**/api/debug/dump/usermode/crashdump (DELETE)**</span></span>

<span data-ttu-id="3f274-137">Supprime un vidage sur incident pour une application chargée indépendamment</span><span class="sxs-lookup"><span data-stu-id="3f274-137">Deletes a crash dump for a sideloaded app</span></span>

<span data-ttu-id="3f274-138">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-138">Parameters</span></span>
* <span data-ttu-id="3f274-139">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="3f274-139">packageFullname : package name</span></span>
* <span data-ttu-id="3f274-140">nom de fichier : nom de fichier de vidage</span><span class="sxs-lookup"><span data-stu-id="3f274-140">fileName : dump file name</span></span>

<span data-ttu-id="3f274-141">**/API/Debug/dump/UserMode/crashdump (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-141">**/api/debug/dump/usermode/crashdump (GET)**</span></span>

<span data-ttu-id="3f274-142">Récupère un vidage sur incident pour une application chargée indépendamment</span><span class="sxs-lookup"><span data-stu-id="3f274-142">Retrieves a crash dump for a sideloaded app</span></span>

<span data-ttu-id="3f274-143">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-143">Parameters</span></span>
* <span data-ttu-id="3f274-144">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="3f274-144">packageFullname : package name</span></span>
* <span data-ttu-id="3f274-145">nom de fichier : nom de fichier de vidage</span><span class="sxs-lookup"><span data-stu-id="3f274-145">fileName : dump file name</span></span>

<span data-ttu-id="3f274-146">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-146">Return data</span></span>
* <span data-ttu-id="3f274-147">Fichier de vidage.</span><span class="sxs-lookup"><span data-stu-id="3f274-147">Dump file.</span></span> <span data-ttu-id="3f274-148">Inspecter avec WinDbg ou Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3f274-148">Inspect with WinDbg or Visual Studio</span></span>

<span data-ttu-id="3f274-149">**/API/Debug/dump/UserMode/dumps (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-149">**/api/debug/dump/usermode/dumps (GET)**</span></span>

<span data-ttu-id="3f274-150">Retourne la liste de tous les vidages sur incident pour les versions test d’applications</span><span class="sxs-lookup"><span data-stu-id="3f274-150">Returns list of all crash dumps for sideloaded apps</span></span>

<span data-ttu-id="3f274-151">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-151">Return data</span></span>
* <span data-ttu-id="3f274-152">Liste de blocage vidages par l’application chargée côté</span><span class="sxs-lookup"><span data-stu-id="3f274-152">List of crash dumps per side loaded app</span></span>

## <a name="etw"></a><span data-ttu-id="3f274-153">ETW</span><span class="sxs-lookup"><span data-stu-id="3f274-153">ETW</span></span>

<span data-ttu-id="3f274-154">**/api/etw/providers (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-154">**/api/etw/providers (GET)**</span></span>

<span data-ttu-id="3f274-155">Énumère les fournisseurs inscrits</span><span class="sxs-lookup"><span data-stu-id="3f274-155">Enumerates registered providers</span></span>

<span data-ttu-id="3f274-156">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-156">Return data</span></span>
* <span data-ttu-id="3f274-157">Liste des fournisseurs, nom convivial et GUID</span><span class="sxs-lookup"><span data-stu-id="3f274-157">List of providers, friendly name and GUID</span></span>

<span data-ttu-id="3f274-158">**/API/ETW/session/Realtime (GET/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="3f274-158">**/api/etw/session/realtime (GET/WebSocket)**</span></span>

<span data-ttu-id="3f274-159">Crée une session ETW en temps réel. gérés via un websocket.</span><span class="sxs-lookup"><span data-stu-id="3f274-159">Creates a realtime ETW session; managed over a websocket.</span></span>

<span data-ttu-id="3f274-160">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-160">Return data</span></span>
* <span data-ttu-id="3f274-161">Événements ETW à partir de fournisseurs activés</span><span class="sxs-lookup"><span data-stu-id="3f274-161">ETW events from the enabled providers</span></span>

## <a name="holographic-os"></a><span data-ttu-id="3f274-162">Système d’exploitation holographique</span><span class="sxs-lookup"><span data-stu-id="3f274-162">Holographic OS</span></span>

<span data-ttu-id="3f274-163">**/API/Holographic/OS/ETW/customproviders (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-163">**/api/holographic/os/etw/customproviders (GET)**</span></span>

<span data-ttu-id="3f274-164">Retourne une liste des fournisseurs ETW spécifiques HoloLens qui ne sont pas inscrits avec le système</span><span class="sxs-lookup"><span data-stu-id="3f274-164">Returns a list of HoloLens specific ETW providers that are not registered with the system</span></span>

<span data-ttu-id="3f274-165">**/API/Holographic/OS/Services (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-165">**/api/holographic/os/services (GET)**</span></span>

<span data-ttu-id="3f274-166">Retourne les États de tous les services en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="3f274-166">Returns the states of all services running.</span></span>

<span data-ttu-id="3f274-167">**/API/Holographic/OS/Settings/IPD (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-167">**/api/holographic/os/settings/ipd (GET)**</span></span>

<span data-ttu-id="3f274-168">Obtient l’IPD stockée (distance Interpupillary) en millimètres</span><span class="sxs-lookup"><span data-stu-id="3f274-168">Gets the stored IPD (Interpupillary distance) in millimeters</span></span>

<span data-ttu-id="3f274-169">**/API/Holographic/OS/Settings/IPD (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-169">**/api/holographic/os/settings/ipd (POST)**</span></span>

<span data-ttu-id="3f274-170">Définit l’IPD</span><span class="sxs-lookup"><span data-stu-id="3f274-170">Sets the IPD</span></span>

<span data-ttu-id="3f274-171">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-171">Parameters</span></span>
* <span data-ttu-id="3f274-172">IPD : Nouvelle valeur IPD à être définies en millimètres</span><span class="sxs-lookup"><span data-stu-id="3f274-172">ipd : New IPD value to be set in millimeters</span></span>

<span data-ttu-id="3f274-173">**/api/holographic/os/webmanagement/settings/https (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-173">**/api/holographic/os/webmanagement/settings/https (GET)**</span></span>

<span data-ttu-id="3f274-174">Obtenir la spécification HTTPS pour Device Portal</span><span class="sxs-lookup"><span data-stu-id="3f274-174">Get HTTPS requirements for the Device Portal</span></span>

<span data-ttu-id="3f274-175">**/api/holographic/os/webmanagement/settings/https (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-175">**/api/holographic/os/webmanagement/settings/https (POST)**</span></span>

<span data-ttu-id="3f274-176">Définit les conditions requises de HTTPS pour le portail de l’appareil</span><span class="sxs-lookup"><span data-stu-id="3f274-176">Sets HTTPS requirements for the Device Portal</span></span>

<span data-ttu-id="3f274-177">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-177">Parameters</span></span>
* <span data-ttu-id="3f274-178">requis : Oui, non ou par défaut</span><span class="sxs-lookup"><span data-stu-id="3f274-178">required : yes, no or default</span></span>

## <a name="holographic-perception"></a><span data-ttu-id="3f274-179">Perception HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="3f274-179">Holographic Perception</span></span>

<span data-ttu-id="3f274-180">**/API/Holographic/perception/client (GET/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="3f274-180">**/api/holographic/perception/client (GET/WebSocket)**</span></span>

<span data-ttu-id="3f274-181">Accepte les mises à niveau websocket et exécute un client de perception qui envoie des mises à jour à 30 i/s.</span><span class="sxs-lookup"><span data-stu-id="3f274-181">Accepts websocket upgrades and runs a perception client that sends updates at 30 fps.</span></span>

<span data-ttu-id="3f274-182">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-182">Parameters</span></span>
* <span data-ttu-id="3f274-183">clientmode : « actif » force le mode de suivi visuel quand il ne peut pas être établie passivement</span><span class="sxs-lookup"><span data-stu-id="3f274-183">clientmode: "active" forces visual tracking mode when it can't be established passively</span></span>

## <a name="holographic-thermal"></a><span data-ttu-id="3f274-184">Thermique HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="3f274-184">Holographic Thermal</span></span>

<span data-ttu-id="3f274-185">**/API/Holographic/Thermal/Stage (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-185">**/api/holographic/thermal/stage (GET)**</span></span>

<span data-ttu-id="3f274-186">Obtenir de l’étape thermique de l’appareil (normal 0, 1 à chaud, 2 critique)</span><span class="sxs-lookup"><span data-stu-id="3f274-186">Get the thermal stage of the device (0 normal, 1 warm, 2 critical)</span></span>

## <a name="perception-simulation-control"></a><span data-ttu-id="3f274-187">Contrôle de Simulation de perception</span><span class="sxs-lookup"><span data-stu-id="3f274-187">Perception Simulation Control</span></span>

<span data-ttu-id="3f274-188">**/API/Holographic/simulation/Control/mode (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-188">**/api/holographic/simulation/control/mode (GET)**</span></span>

<span data-ttu-id="3f274-189">Obtenir le mode de simulation</span><span class="sxs-lookup"><span data-stu-id="3f274-189">Get the simulation mode</span></span>

<span data-ttu-id="3f274-190">**/API/Holographic/simulation/Control/mode (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-190">**/api/holographic/simulation/control/mode (POST)**</span></span>

<span data-ttu-id="3f274-191">Définir le mode de simulation</span><span class="sxs-lookup"><span data-stu-id="3f274-191">Set the simulation mode</span></span>

<span data-ttu-id="3f274-192">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-192">Parameters</span></span>
* <span data-ttu-id="3f274-193">mode : mode de simulation : par défaut, simulation, à distance, hérité</span><span class="sxs-lookup"><span data-stu-id="3f274-193">mode : simulation mode: default, simulation, remote, legacy</span></span>

<span data-ttu-id="3f274-194">**/API/Holographic/simulation/Control/Stream (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="3f274-194">**/api/holographic/simulation/control/stream (DELETE)**</span></span>

<span data-ttu-id="3f274-195">Supprimer un flux de contrôle.</span><span class="sxs-lookup"><span data-stu-id="3f274-195">Delete a control stream.</span></span>

<span data-ttu-id="3f274-196">**/API/Holographic/simulation/Control/Stream (GET/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="3f274-196">**/api/holographic/simulation/control/stream (GET/WebSocket)**</span></span>

<span data-ttu-id="3f274-197">Ouvrir une connexion de socket web pour un flux de contrôle.</span><span class="sxs-lookup"><span data-stu-id="3f274-197">Open a web socket connection for a control stream.</span></span>

<span data-ttu-id="3f274-198">**/API/Holographic/simulation/Control/Stream (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-198">**/api/holographic/simulation/control/stream (POST)**</span></span>

<span data-ttu-id="3f274-199">Créer un flux de contrôle (la priorité est requise) ou publier des données sur un flux créé (streamId requis).</span><span class="sxs-lookup"><span data-stu-id="3f274-199">Create a control stream (priority is required) or post data to a created stream (streamId required).</span></span> <span data-ttu-id="3f274-200">Les données publiées sont censées être de type « application/octet-stream ».</span><span class="sxs-lookup"><span data-stu-id="3f274-200">Posted data is expected to be of type 'application/octet-stream'.</span></span>

## <a name="perception-simulation-playback"></a><span data-ttu-id="3f274-201">Lecture de Simulation de perception</span><span class="sxs-lookup"><span data-stu-id="3f274-201">Perception Simulation Playback</span></span>

<span data-ttu-id="3f274-202">**/API/Holographic/simulation/Playback/File (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="3f274-202">**/api/holographic/simulation/playback/file (DELETE)**</span></span>

<span data-ttu-id="3f274-203">Supprimer un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-203">Delete a recording.</span></span>

<span data-ttu-id="3f274-204">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-204">Parameters</span></span>
* <span data-ttu-id="3f274-205">enregistrement : Nom de l’enregistrement pour la supprimer.</span><span class="sxs-lookup"><span data-stu-id="3f274-205">recording : Name of recording to delete.</span></span>

<span data-ttu-id="3f274-206">**/API/Holographic/simulation/Playback/File (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-206">**/api/holographic/simulation/playback/file (POST)**</span></span>

<span data-ttu-id="3f274-207">Téléchargez un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-207">Upload a recording.</span></span>

<span data-ttu-id="3f274-208">**/API/Holographic/simulation/Playback/Files (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-208">**/api/holographic/simulation/playback/files (GET)**</span></span>

<span data-ttu-id="3f274-209">Obtenir tous les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="3f274-209">Get all recordings.</span></span>

<span data-ttu-id="3f274-210">**/API/Holographic/simulation/Playback/session (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-210">**/api/holographic/simulation/playback/session (GET)**</span></span>

<span data-ttu-id="3f274-211">Obtenir l’état actuel de la lecture de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-211">Get the current playback state of a recording.</span></span>

<span data-ttu-id="3f274-212">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-212">Parameters</span></span>
* <span data-ttu-id="3f274-213">enregistrement : Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-213">recording : Name of recording.</span></span>

<span data-ttu-id="3f274-214">**/API/Holographic/simulation/Playback/session/file (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="3f274-214">**/api/holographic/simulation/playback/session/file (DELETE)**</span></span>

<span data-ttu-id="3f274-215">Décharger un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-215">Unload a recording.</span></span>

<span data-ttu-id="3f274-216">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-216">Parameters</span></span>
* <span data-ttu-id="3f274-217">enregistrement : Nom de l’enregistrement pour décharger.</span><span class="sxs-lookup"><span data-stu-id="3f274-217">recording : Name of recording to unload.</span></span>

<span data-ttu-id="3f274-218">**/API/Holographic/simulation/Playback/session/file (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-218">**/api/holographic/simulation/playback/session/file (POST)**</span></span>

<span data-ttu-id="3f274-219">Charger un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-219">Load a recording.</span></span>

<span data-ttu-id="3f274-220">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-220">Parameters</span></span>
* <span data-ttu-id="3f274-221">enregistrement : Nom de l’enregistrement pour la charge.</span><span class="sxs-lookup"><span data-stu-id="3f274-221">recording : Name of recording to load.</span></span>

<span data-ttu-id="3f274-222">**/API/Holographic/simulation/Playback/session/files (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-222">**/api/holographic/simulation/playback/session/files (GET)**</span></span>

<span data-ttu-id="3f274-223">Obtenir des enregistrements tous chargés.</span><span class="sxs-lookup"><span data-stu-id="3f274-223">Get all loaded recordings.</span></span>

<span data-ttu-id="3f274-224">**/API/Holographic/simulation/Playback/session/pause (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-224">**/api/holographic/simulation/playback/session/pause (POST)**</span></span>

<span data-ttu-id="3f274-225">Suspendre un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-225">Pause a recording.</span></span>

<span data-ttu-id="3f274-226">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-226">Parameters</span></span>
* <span data-ttu-id="3f274-227">enregistrement : Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-227">recording : Name of recording.</span></span>

<span data-ttu-id="3f274-228">**/API/Holographic/simulation/Playback/session/Play (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-228">**/api/holographic/simulation/playback/session/play (POST)**</span></span>

<span data-ttu-id="3f274-229">Lire un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-229">Play a recording.</span></span>

<span data-ttu-id="3f274-230">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-230">Parameters</span></span>
* <span data-ttu-id="3f274-231">enregistrement : Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-231">recording : Name of recording.</span></span>

<span data-ttu-id="3f274-232">**/API/Holographic/simulation/Playback/session/Stop (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-232">**/api/holographic/simulation/playback/session/stop (POST)**</span></span>

<span data-ttu-id="3f274-233">Arrêter un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-233">Stop a recording.</span></span>

<span data-ttu-id="3f274-234">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-234">Parameters</span></span>
* <span data-ttu-id="3f274-235">enregistrement : Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-235">recording : Name of recording.</span></span>

<span data-ttu-id="3f274-236">**/API/Holographic/simulation/Playback/session/types (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-236">**/api/holographic/simulation/playback/session/types (GET)**</span></span>

<span data-ttu-id="3f274-237">Obtenir les types de données dans un enregistrement chargé.</span><span class="sxs-lookup"><span data-stu-id="3f274-237">Get the types of data in a loaded recording.</span></span>

<span data-ttu-id="3f274-238">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-238">Parameters</span></span>
* <span data-ttu-id="3f274-239">enregistrement : Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-239">recording : Name of recording.</span></span>

## <a name="perception-simulation-recording"></a><span data-ttu-id="3f274-240">Enregistrement de Simulation de perception</span><span class="sxs-lookup"><span data-stu-id="3f274-240">Perception Simulation Recording</span></span>

<span data-ttu-id="3f274-241">**/API/Holographic/simulation/Recording/Start (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-241">**/api/holographic/simulation/recording/start (POST)**</span></span>

<span data-ttu-id="3f274-242">Démarrer un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-242">Start a recording.</span></span> <span data-ttu-id="3f274-243">Un enregistrement unique peut être actif à la fois.</span><span class="sxs-lookup"><span data-stu-id="3f274-243">Only a single recording can be active at once.</span></span> <span data-ttu-id="3f274-244">Head, mains, spatialMapping ou environnement doit être définie.</span><span class="sxs-lookup"><span data-stu-id="3f274-244">One of head, hands, spatialMapping or environment must be set.</span></span>

<span data-ttu-id="3f274-245">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-245">Parameters</span></span>
* <span data-ttu-id="3f274-246">head : Définissez sur 1 pour les données de l’enregistrement principal.</span><span class="sxs-lookup"><span data-stu-id="3f274-246">head : Set to 1 to record head data.</span></span>
* <span data-ttu-id="3f274-247">mains : La valeur 1 pour enregistrer les données manuellement.</span><span class="sxs-lookup"><span data-stu-id="3f274-247">hands : Set to 1 to record hand data.</span></span>
* <span data-ttu-id="3f274-248">spatialMapping : La valeur 1 pour enregistrer le mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="3f274-248">spatialMapping : Set to 1 to record spatial mapping.</span></span>
* <span data-ttu-id="3f274-249">environnement : La valeur 1 pour enregistrer les données de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="3f274-249">environment : Set to 1 to record environment data.</span></span>
* <span data-ttu-id="3f274-250">nom : Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3f274-250">name : Name of the recording.</span></span>
* <span data-ttu-id="3f274-251">singleSpatialMappingFrame : La valeur 1 pour enregistrer uniquement une trame de mappage spatial unique.</span><span class="sxs-lookup"><span data-stu-id="3f274-251">singleSpatialMappingFrame : Set to 1 to record only a single spatial mapping frame.</span></span>

<span data-ttu-id="3f274-252">**/API/Holographic/simulation/Recording/Status (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-252">**/api/holographic/simulation/recording/status (GET)**</span></span>

<span data-ttu-id="3f274-253">Obtenir enregistrement d’état.</span><span class="sxs-lookup"><span data-stu-id="3f274-253">Get recording state.</span></span>

<span data-ttu-id="3f274-254">**/API/Holographic/simulation/Recording/Stop (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-254">**/api/holographic/simulation/recording/stop (GET)**</span></span>

<span data-ttu-id="3f274-255">Arrêter l’enregistrement actuel.</span><span class="sxs-lookup"><span data-stu-id="3f274-255">Stop the current recording.</span></span> <span data-ttu-id="3f274-256">L’enregistrement s’affichera sous forme de fichier.</span><span class="sxs-lookup"><span data-stu-id="3f274-256">Recording will be returned as a file.</span></span>

## <a name="mixed-reality-capture"></a><span data-ttu-id="3f274-257">MRC (Mixed Reality Capture)</span><span class="sxs-lookup"><span data-stu-id="3f274-257">Mixed Reality Capture</span></span>

<span data-ttu-id="3f274-258">**/API/Holographic/MRC/file (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="3f274-258">**/api/holographic/mrc/file (DELETE)**</span></span>

<span data-ttu-id="3f274-259">Supprime une réalité mixte enregistrant à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3f274-259">Deletes a mixed reality recording from the device.</span></span>

<span data-ttu-id="3f274-260">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-260">Parameters</span></span>
* <span data-ttu-id="3f274-261">nom de fichier : Nom, hex64 encodée du fichier à supprimer</span><span class="sxs-lookup"><span data-stu-id="3f274-261">filename : Name, hex64 encoded, of the file to delete</span></span>

<span data-ttu-id="3f274-262">**/API/Holographic/MRC/Settings (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-262">**/api/holographic/mrc/settings (GET)**</span></span>

<span data-ttu-id="3f274-263">Obtient la valeur par défaut une réalité mixte paramètres de capture</span><span class="sxs-lookup"><span data-stu-id="3f274-263">Gets the default mixed reality capture settings</span></span>

<span data-ttu-id="3f274-264">**/API/Holographic/MRC/file (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-264">**/api/holographic/mrc/file (GET)**</span></span>

<span data-ttu-id="3f274-265">Télécharge un fichier de réalité mixte à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3f274-265">Downloads a mixed reality file from the device.</span></span> <span data-ttu-id="3f274-266">Emploi de = le paramètre de requête de flux de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="3f274-266">Use op=stream query parameter for streaming.</span></span>

<span data-ttu-id="3f274-267">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-267">Parameters</span></span>
* <span data-ttu-id="3f274-268">nom de fichier : Nom, hex64 encodée du fichier vidéo à obtenir</span><span class="sxs-lookup"><span data-stu-id="3f274-268">filename : Name, hex64 encoded, of the video file to get</span></span>
* <span data-ttu-id="3f274-269">op : flux de données</span><span class="sxs-lookup"><span data-stu-id="3f274-269">op : stream</span></span>

<span data-ttu-id="3f274-270">**/API/Holographic/MRC/Thumbnail (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-270">**/api/holographic/mrc/thumbnail (GET)**</span></span>

<span data-ttu-id="3f274-271">Obtient l’image miniature pour le fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="3f274-271">Gets the thumbnail image for the specified file.</span></span>

<span data-ttu-id="3f274-272">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-272">Parameters</span></span>
* <span data-ttu-id="3f274-273">nom de fichier : Nom, hex64 encodée du fichier pour lequel la miniature est demandée</span><span class="sxs-lookup"><span data-stu-id="3f274-273">filename: Name, hex64 encoded, of the file for which the thumbnail is being requested</span></span>

<span data-ttu-id="3f274-274">**/API/Holographic/MRC/Status (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-274">**/api/holographic/mrc/status (GET)**</span></span>

<span data-ttu-id="3f274-275">Obtient l’état de la réalité mixte enregistrée (en cours d’exécution, arrêté)</span><span class="sxs-lookup"><span data-stu-id="3f274-275">Gets the status of the mixed reality recorded (running, stopped)</span></span>

<span data-ttu-id="3f274-276">**/API/Holographic/MRC/Files (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-276">**/api/holographic/mrc/files (GET)**</span></span>

<span data-ttu-id="3f274-277">Retourne la liste des fichiers de réalité mixte stockées sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="3f274-277">Returns the list of mixed reality files stored on the device</span></span>

<span data-ttu-id="3f274-278">**/API/Holographic/MRC/Settings (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-278">**/api/holographic/mrc/settings (POST)**</span></span>

<span data-ttu-id="3f274-279">Définit la valeur par défaut une réalité mixte paramètres de capture</span><span class="sxs-lookup"><span data-stu-id="3f274-279">Sets the default mixed reality capture settings</span></span>

<span data-ttu-id="3f274-280">**/API/Holographic/MRC/Video/Control/Start (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-280">**/api/holographic/mrc/video/control/start (POST)**</span></span>

<span data-ttu-id="3f274-281">Démarre un enregistrement de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="3f274-281">Starts a mixed reality recording</span></span>

<span data-ttu-id="3f274-282">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-282">Parameters</span></span>
* <span data-ttu-id="3f274-283">Holo : capturer hologrammes : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-283">holo : capture holograms: true or false</span></span>
* <span data-ttu-id="3f274-284">PV : capture PV caméra : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-284">pv : capture PV camera: true or false</span></span>
* <span data-ttu-id="3f274-285">MIC : capture microphone : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-285">mic : capture microphone: true or false</span></span>
* <span data-ttu-id="3f274-286">bouclage : capturer des données audio app : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-286">loopback : capture app audio: true or false</span></span>

<span data-ttu-id="3f274-287">**/API/Holographic/MRC/Video/Control/Stop (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-287">**/api/holographic/mrc/video/control/stop (POST)**</span></span>

<span data-ttu-id="3f274-288">S’arrête en cours mixte d’enregistrement de réalité</span><span class="sxs-lookup"><span data-stu-id="3f274-288">Stops the current mixed reality recording</span></span>

<span data-ttu-id="3f274-289">**/API/Holographic/MRC/photo (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-289">**/api/holographic/mrc/photo (POST)**</span></span>

<span data-ttu-id="3f274-290">Prend une photo de réalité mixte et crée un fichier sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="3f274-290">Takes a mixed reality photo and creates a file on the device</span></span>

<span data-ttu-id="3f274-291">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-291">Parameters</span></span>
* <span data-ttu-id="3f274-292">Holo : capturer hologrammes : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-292">holo : capture holograms: true or false</span></span>
* <span data-ttu-id="3f274-293">PV : capture PV caméra : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-293">pv : capture PV camera: true or false</span></span>

<span data-ttu-id="3f274-294">Réalité mixte de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="3f274-294">Mixed Reality Streaming</span></span>

<span data-ttu-id="3f274-295">**/api/holographic/stream/live.mp4 (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-295">**/api/holographic/stream/live.mp4 (GET)**</span></span>

<span data-ttu-id="3f274-296">Initie un téléchargement mémorisé en bloc d’un mp4 fragmenté</span><span class="sxs-lookup"><span data-stu-id="3f274-296">Initiates a chunked download of a fragmented mp4</span></span>

<span data-ttu-id="3f274-297">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-297">Parameters</span></span>
* <span data-ttu-id="3f274-298">Holo : capturer hologrammes : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-298">holo : capture holograms: true or false</span></span>
* <span data-ttu-id="3f274-299">PV : capture PV caméra : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-299">pv : capture PV camera: true or false</span></span>
* <span data-ttu-id="3f274-300">MIC : capture microphone : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-300">mic : capture microphone: true or false</span></span>
* <span data-ttu-id="3f274-301">bouclage : capturer des données audio app : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-301">loopback : capture app audio: true or false</span></span>

<span data-ttu-id="3f274-302">**/api/holographic/stream/live_high.mp4 (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-302">**/api/holographic/stream/live_high.mp4 (GET)**</span></span>

<span data-ttu-id="3f274-303">Initie un téléchargement mémorisé en bloc d’un mp4 fragmenté</span><span class="sxs-lookup"><span data-stu-id="3f274-303">Initiates a chunked download of a fragmented mp4</span></span>

<span data-ttu-id="3f274-304">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-304">Parameters</span></span>
* <span data-ttu-id="3f274-305">Holo : capturer hologrammes : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-305">holo : capture holograms: true or false</span></span>
* <span data-ttu-id="3f274-306">PV : capture PV caméra : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-306">pv : capture PV camera: true or false</span></span>
* <span data-ttu-id="3f274-307">MIC : capture microphone : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-307">mic : capture microphone: true or false</span></span>
* <span data-ttu-id="3f274-308">bouclage : capturer des données audio app : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-308">loopback : capture app audio: true or false</span></span>

<span data-ttu-id="3f274-309">**/api/holographic/stream/live_low.mp4 (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-309">**/api/holographic/stream/live_low.mp4 (GET)**</span></span>

<span data-ttu-id="3f274-310">Initie un téléchargement mémorisé en bloc d’un mp4 fragmenté</span><span class="sxs-lookup"><span data-stu-id="3f274-310">Initiates a chunked download of a fragmented mp4</span></span>

<span data-ttu-id="3f274-311">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-311">Parameters</span></span>
* <span data-ttu-id="3f274-312">Holo : capturer hologrammes : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-312">holo : capture holograms: true or false</span></span>
* <span data-ttu-id="3f274-313">PV : capture PV caméra : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-313">pv : capture PV camera: true or false</span></span>
* <span data-ttu-id="3f274-314">MIC : capture microphone : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-314">mic : capture microphone: true or false</span></span>
* <span data-ttu-id="3f274-315">bouclage : capturer des données audio app : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-315">loopback : capture app audio: true or false</span></span>

<span data-ttu-id="3f274-316">**/api/holographic/stream/live_med.mp4 (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-316">**/api/holographic/stream/live_med.mp4 (GET)**</span></span>

<span data-ttu-id="3f274-317">Initie un téléchargement mémorisé en bloc d’un mp4 fragmenté</span><span class="sxs-lookup"><span data-stu-id="3f274-317">Initiates a chunked download of a fragmented mp4</span></span>

<span data-ttu-id="3f274-318">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-318">Parameters</span></span>
* <span data-ttu-id="3f274-319">Holo : capturer hologrammes : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-319">holo : capture holograms: true or false</span></span>
* <span data-ttu-id="3f274-320">PV : capture PV caméra : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-320">pv : capture PV camera: true or false</span></span>
* <span data-ttu-id="3f274-321">MIC : capture microphone : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-321">mic : capture microphone: true or false</span></span>
* <span data-ttu-id="3f274-322">bouclage : capturer des données audio app : true ou false</span><span class="sxs-lookup"><span data-stu-id="3f274-322">loopback : capture app audio: true or false</span></span>

## <a name="networking"></a><span data-ttu-id="3f274-323">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="3f274-323">Networking</span></span>

<span data-ttu-id="3f274-324">**/api/networking/ipconfig (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-324">**/api/networking/ipconfig (GET)**</span></span>

<span data-ttu-id="3f274-325">Obtient la configuration ip actuelle</span><span class="sxs-lookup"><span data-stu-id="3f274-325">Gets the current ip configuration</span></span>

## <a name="os-information"></a><span data-ttu-id="3f274-326">Informations de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="3f274-326">OS Information</span></span>

<span data-ttu-id="3f274-327">**/api/os/info (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-327">**/api/os/info (GET)**</span></span>

<span data-ttu-id="3f274-328">Obtient des informations de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="3f274-328">Gets operating system information</span></span>

<span data-ttu-id="3f274-329">**/API/OS/MachineName (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-329">**/api/os/machinename (GET)**</span></span>

<span data-ttu-id="3f274-330">Obtient le nom de l’ordinateur</span><span class="sxs-lookup"><span data-stu-id="3f274-330">Gets the machine name</span></span>

<span data-ttu-id="3f274-331">**/api/os/machinename (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-331">**/api/os/machinename (POST)**</span></span>

<span data-ttu-id="3f274-332">Définit le nom de l’ordinateur</span><span class="sxs-lookup"><span data-stu-id="3f274-332">Sets the machine name</span></span>

<span data-ttu-id="3f274-333">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-333">Parameters</span></span>
* <span data-ttu-id="3f274-334">nom : Nouveau nom de l’ordinateur, hex64 encodée, pour la valeur</span><span class="sxs-lookup"><span data-stu-id="3f274-334">name : New machine name, hex64 encoded, to set to</span></span>

## <a name="performance-data"></a><span data-ttu-id="3f274-335">Données relatives aux performances</span><span class="sxs-lookup"><span data-stu-id="3f274-335">Performance data</span></span>

<span data-ttu-id="3f274-336">**/API/ResourceManager/Processes (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-336">**/api/resourcemanager/processes (GET)**</span></span>

<span data-ttu-id="3f274-337">Retourne la liste des processus en cours avec les détails</span><span class="sxs-lookup"><span data-stu-id="3f274-337">Returns the list of running processes with details</span></span>

<span data-ttu-id="3f274-338">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-338">Return data</span></span>
* <span data-ttu-id="3f274-339">JSON avec la liste des processus et les détails de chaque processus</span><span class="sxs-lookup"><span data-stu-id="3f274-339">JSON with list of processes and details for each process</span></span>

<span data-ttu-id="3f274-340">**/API/ResourceManager/systemperf (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-340">**/api/resourcemanager/systemperf (GET)**</span></span>

<span data-ttu-id="3f274-341">Retourne des statistiques de performances système (e/s en lecture/écriture, etc. statistiques de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="3f274-341">Returns system perf statistics (I/O read/write, memory stats etc.</span></span>

<span data-ttu-id="3f274-342">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-342">Return data</span></span>
* <span data-ttu-id="3f274-343">JSON avec les informations système : Processeur, processeur, mémoire, réseau, e/s</span><span class="sxs-lookup"><span data-stu-id="3f274-343">JSON with system information: CPU, GPU, Memory, Network, IO</span></span>

## <a name="power"></a><span data-ttu-id="3f274-344">Alimentation</span><span class="sxs-lookup"><span data-stu-id="3f274-344">Power</span></span>

<span data-ttu-id="3f274-345">**/api/power/battery (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-345">**/api/power/battery (GET)**</span></span>

<span data-ttu-id="3f274-346">Obtient l’état actuel de la batterie</span><span class="sxs-lookup"><span data-stu-id="3f274-346">Gets the current battery state</span></span>

<span data-ttu-id="3f274-347">**/API/Power/State (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-347">**/api/power/state (GET)**</span></span>

<span data-ttu-id="3f274-348">Vérifie si le système est dans un état de faible consommation d’énergie</span><span class="sxs-lookup"><span data-stu-id="3f274-348">Checks if the system is in a low power state</span></span>

## <a name="remote-control"></a><span data-ttu-id="3f274-349">Contrôle à distance</span><span class="sxs-lookup"><span data-stu-id="3f274-349">Remote Control</span></span>

<span data-ttu-id="3f274-350">**/api/control/restart (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-350">**/api/control/restart (POST)**</span></span>

<span data-ttu-id="3f274-351">Redémarre l’appareil cible</span><span class="sxs-lookup"><span data-stu-id="3f274-351">Restarts the target device</span></span>

<span data-ttu-id="3f274-352">**/API/Control/Shutdown (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-352">**/api/control/shutdown (POST)**</span></span>

<span data-ttu-id="3f274-353">Arrête l’appareil cible</span><span class="sxs-lookup"><span data-stu-id="3f274-353">Shuts down the target device</span></span>

## <a name="task-manager"></a><span data-ttu-id="3f274-354">Gestionnaire des tâches</span><span class="sxs-lookup"><span data-stu-id="3f274-354">Task Manager</span></span>

<span data-ttu-id="3f274-355">**/API/TaskManager/App (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="3f274-355">**/api/taskmanager/app (DELETE)**</span></span>

<span data-ttu-id="3f274-356">Arrête une application moderne</span><span class="sxs-lookup"><span data-stu-id="3f274-356">Stops a modern app</span></span>

<span data-ttu-id="3f274-357">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-357">Parameters</span></span>
* <span data-ttu-id="3f274-358">package : Nom complet du package d’application, hex64 encodé</span><span class="sxs-lookup"><span data-stu-id="3f274-358">package : Full name of the app package, hex64 encoded</span></span>
* <span data-ttu-id="3f274-359">arrêt forcé : Forcer tous les processus à arrêter (= yes)</span><span class="sxs-lookup"><span data-stu-id="3f274-359">forcestop : Force all processes to stop (=yes)</span></span>

<span data-ttu-id="3f274-360">**/api/taskmanager/app (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-360">**/api/taskmanager/app (POST)**</span></span>

<span data-ttu-id="3f274-361">Démarre une application moderne</span><span class="sxs-lookup"><span data-stu-id="3f274-361">Starts a modern app</span></span>

<span data-ttu-id="3f274-362">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-362">Parameters</span></span>
* <span data-ttu-id="3f274-363">ID d’application : PRAID d’application pour démarrer, hex64 encodé</span><span class="sxs-lookup"><span data-stu-id="3f274-363">appid : PRAID of app to start, hex64 encoded</span></span>
* <span data-ttu-id="3f274-364">package : Nom complet du package d’application, hex64 encodé</span><span class="sxs-lookup"><span data-stu-id="3f274-364">package : Full name of the app package, hex64 encoded</span></span>

## <a name="wifi-management"></a><span data-ttu-id="3f274-365">Gestion de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="3f274-365">WiFi Management</span></span>

<span data-ttu-id="3f274-366">**/api/wifi/interfaces (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-366">**/api/wifi/interfaces (GET)**</span></span>

<span data-ttu-id="3f274-367">Énumère les interfaces de réseau sans fil</span><span class="sxs-lookup"><span data-stu-id="3f274-367">Enumerates wireless network interfaces</span></span>

<span data-ttu-id="3f274-368">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-368">Return data</span></span>
* <span data-ttu-id="3f274-369">Liste des interfaces sans fil avec les détails (GUID, description, etc.).</span><span class="sxs-lookup"><span data-stu-id="3f274-369">List of wireless interfaces with details (GUID, description etc.)</span></span>

<span data-ttu-id="3f274-370">**/api/wifi/network (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="3f274-370">**/api/wifi/network (DELETE)**</span></span>

<span data-ttu-id="3f274-371">Supprime un profil associé à un réseau sur l’interface spécifiée</span><span class="sxs-lookup"><span data-stu-id="3f274-371">Deletes a profile associated with a network on a specified interface</span></span>

<span data-ttu-id="3f274-372">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-372">Parameters</span></span>
* <span data-ttu-id="3f274-373">interface : guid de l’interface de réseau</span><span class="sxs-lookup"><span data-stu-id="3f274-373">interface : network interface guid</span></span>
* <span data-ttu-id="3f274-374">profil : nom du profil</span><span class="sxs-lookup"><span data-stu-id="3f274-374">profile : profile name</span></span>

<span data-ttu-id="3f274-375">**/API/WiFi/Networks (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-375">**/api/wifi/networks (GET)**</span></span>

<span data-ttu-id="3f274-376">Énumère les réseaux sans fil sur l’interface réseau spécifiée</span><span class="sxs-lookup"><span data-stu-id="3f274-376">Enumerates wireless networks on the specified network interface</span></span>

<span data-ttu-id="3f274-377">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-377">Parameters</span></span>
* <span data-ttu-id="3f274-378">interface : guid de l’interface de réseau</span><span class="sxs-lookup"><span data-stu-id="3f274-378">interface : network interface guid</span></span>

<span data-ttu-id="3f274-379">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-379">Return data</span></span>
* <span data-ttu-id="3f274-380">Liste des réseaux sans fil trouvés sur l’interface réseau avec les détails</span><span class="sxs-lookup"><span data-stu-id="3f274-380">List of wireless networks found on the network interface with details</span></span>

<span data-ttu-id="3f274-381">**/api/wifi/network (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-381">**/api/wifi/network (POST)**</span></span>

<span data-ttu-id="3f274-382">Se connecte ou se déconnecte à un réseau sur l’interface spécifiée</span><span class="sxs-lookup"><span data-stu-id="3f274-382">Connects or disconnects to a network on the specified interface</span></span>

<span data-ttu-id="3f274-383">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-383">Parameters</span></span>
* <span data-ttu-id="3f274-384">interface : guid de l’interface de réseau</span><span class="sxs-lookup"><span data-stu-id="3f274-384">interface : network interface guid</span></span>
* <span data-ttu-id="3f274-385">SSID : ssid, hex64 codé, pour vous connecter à</span><span class="sxs-lookup"><span data-stu-id="3f274-385">ssid : ssid, hex64 encoded, to connect to</span></span>
* <span data-ttu-id="3f274-386">op : connecter ou déconnecter</span><span class="sxs-lookup"><span data-stu-id="3f274-386">op : connect or disconnect</span></span>
* <span data-ttu-id="3f274-387">CreateProfile : yes ou no</span><span class="sxs-lookup"><span data-stu-id="3f274-387">createprofile : yes or no</span></span>
* <span data-ttu-id="3f274-388">clé : partagé hex64 clé, encodé</span><span class="sxs-lookup"><span data-stu-id="3f274-388">key : shared key, hex64 encoded</span></span>

## <a name="windows-performance-recorder"></a><span data-ttu-id="3f274-389">Enregistreur de performances Windows</span><span class="sxs-lookup"><span data-stu-id="3f274-389">Windows Performance Recorder</span></span>

<span data-ttu-id="3f274-390">**/api/wpr/customtrace (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-390">**/api/wpr/customtrace (POST)**</span></span>

<span data-ttu-id="3f274-391">Télécharge un profil WPR et commence le traçage en utilisant le profil téléchargé.</span><span class="sxs-lookup"><span data-stu-id="3f274-391">Uploads a WPR profile and starts tracing using the uploaded profile.</span></span>

<span data-ttu-id="3f274-392">charge utile</span><span class="sxs-lookup"><span data-stu-id="3f274-392">Payload</span></span>
* <span data-ttu-id="3f274-393">corps http conforme à plusieurs parties</span><span class="sxs-lookup"><span data-stu-id="3f274-393">multi-part conforming http body</span></span>

<span data-ttu-id="3f274-394">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-394">Return data</span></span>
* <span data-ttu-id="3f274-395">Retourne l’état de session WPR.</span><span class="sxs-lookup"><span data-stu-id="3f274-395">Returns the WPR session status.</span></span>

<span data-ttu-id="3f274-396">**/api/wpr/status (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-396">**/api/wpr/status (GET)**</span></span>

<span data-ttu-id="3f274-397">Récupère l’état de la session WPR</span><span class="sxs-lookup"><span data-stu-id="3f274-397">Retrieves the status of the WPR session</span></span>

<span data-ttu-id="3f274-398">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-398">Return data</span></span>
* <span data-ttu-id="3f274-399">État de session WPR.</span><span class="sxs-lookup"><span data-stu-id="3f274-399">WPR session status.</span></span>

<span data-ttu-id="3f274-400">**/api/wpr/trace (GET)**</span><span class="sxs-lookup"><span data-stu-id="3f274-400">**/api/wpr/trace (GET)**</span></span>

<span data-ttu-id="3f274-401">Arrête une session de suivi WPR (performance)</span><span class="sxs-lookup"><span data-stu-id="3f274-401">Stops a WPR (performance) tracing session</span></span>

<span data-ttu-id="3f274-402">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-402">Return data</span></span>
* <span data-ttu-id="3f274-403">Retourne le fichier ETL de suivi</span><span class="sxs-lookup"><span data-stu-id="3f274-403">Returns the trace ETL file</span></span>

<span data-ttu-id="3f274-404">**/api/wpr/trace (POST)**</span><span class="sxs-lookup"><span data-stu-id="3f274-404">**/api/wpr/trace (POST)**</span></span>

<span data-ttu-id="3f274-405">Démarre un WPR (performance) suivi des sessions</span><span class="sxs-lookup"><span data-stu-id="3f274-405">Starts a WPR (performance) tracing sessions</span></span>

<span data-ttu-id="3f274-406">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3f274-406">Parameters</span></span>
* <span data-ttu-id="3f274-407">profil : Nom du profil.</span><span class="sxs-lookup"><span data-stu-id="3f274-407">profile : Profile name.</span></span> <span data-ttu-id="3f274-408">Profils disponibles sont stockés dans perfprofiles/profiles.json</span><span class="sxs-lookup"><span data-stu-id="3f274-408">Available profiles are stored in perfprofiles/profiles.json</span></span>

<span data-ttu-id="3f274-409">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="3f274-409">Return data</span></span>
* <span data-ttu-id="3f274-410">Au démarrage, retourne l’état de session WPR.</span><span class="sxs-lookup"><span data-stu-id="3f274-410">On start, returns the WPR session status.</span></span>

## <a name="see-also"></a><span data-ttu-id="3f274-411">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3f274-411">See also</span></span>
* [<span data-ttu-id="3f274-412">À l’aide de la Windows Device Portal</span><span class="sxs-lookup"><span data-stu-id="3f274-412">Using the Windows Device Portal</span></span>](using-the-windows-device-portal.md)
* [<span data-ttu-id="3f274-413">Core de portail appareil référence d’API (UWP)</span><span class="sxs-lookup"><span data-stu-id="3f274-413">Device Portal core API reference (UWP)</span></span>](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-api-core)
