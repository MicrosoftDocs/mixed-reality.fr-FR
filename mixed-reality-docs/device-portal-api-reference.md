---
title: Portail de référence de l’API des appareils
description: Référence des API pour le Windows Device Portal sur HoloLens
author: JonMLyons
ms.author: JLyons
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, Windows Device Portal, API
ms.openlocfilehash: 4b5b48c13b1b7ec8bfdf447f42097a8448b6a0e6
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694432"
---
# <a name="device-portal-api-reference"></a><span data-ttu-id="853f5-104">Portail de référence de l’API des appareils</span><span class="sxs-lookup"><span data-stu-id="853f5-104">Device portal API reference</span></span>

<span data-ttu-id="853f5-105">Tous les éléments de la [Windows Device Portal](using-the-windows-device-portal.md) se trouve au sommet de l’API REST que vous pouvez utiliser pour accéder aux données et de contrôler par programmation de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="853f5-105">Everything in the [Windows Device Portal](using-the-windows-device-portal.md) is built on top of REST API's that you can use to access the data and control your device programmatically.</span></span>

## <a name="app-deloyment"></a><span data-ttu-id="853f5-106">Application deloyment</span><span class="sxs-lookup"><span data-stu-id="853f5-106">App deloyment</span></span>

<span data-ttu-id="853f5-107">**/API/App/PackageManager/package (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="853f5-107">**/api/app/packagemanager/package (DELETE)**</span></span>

<span data-ttu-id="853f5-108">Désinstalle une application</span><span class="sxs-lookup"><span data-stu-id="853f5-108">Uninstalls an app</span></span>

<span data-ttu-id="853f5-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-109">Parameters</span></span>
* <span data-ttu-id="853f5-110">package : Nom de fichier du package doit être désinstallé.</span><span class="sxs-lookup"><span data-stu-id="853f5-110">package : File name of the package to be uninstalled.</span></span>

<span data-ttu-id="853f5-111">**/API/App/PackageManager/package (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-111">**/api/app/packagemanager/package (POST)**</span></span>

<span data-ttu-id="853f5-112">Installe une application</span><span class="sxs-lookup"><span data-stu-id="853f5-112">Installs an App</span></span>

<span data-ttu-id="853f5-113">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-113">Parameters</span></span>
* <span data-ttu-id="853f5-114">package : Nom de fichier du package doit être installé.</span><span class="sxs-lookup"><span data-stu-id="853f5-114">package : File name of the package to be installed.</span></span>

<span data-ttu-id="853f5-115">charge utile</span><span class="sxs-lookup"><span data-stu-id="853f5-115">Payload</span></span>
* <span data-ttu-id="853f5-116">corps http conforme à plusieurs parties</span><span class="sxs-lookup"><span data-stu-id="853f5-116">multi-part conforming http body</span></span>

<span data-ttu-id="853f5-117">**/API/App/PackageManager/packages (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-117">**/api/app/packagemanager/packages (GET)**</span></span>

<span data-ttu-id="853f5-118">Récupère la liste des applications installées sur le système, avec les détails</span><span class="sxs-lookup"><span data-stu-id="853f5-118">Retrieves the list of installed apps on the system, with details</span></span>

<span data-ttu-id="853f5-119">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-119">Return data</span></span>
* <span data-ttu-id="853f5-120">Liste des packages installés avec les détails</span><span class="sxs-lookup"><span data-stu-id="853f5-120">List of installed packages with details</span></span>

<span data-ttu-id="853f5-121">**/API/App/PackageManager/State (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-121">**/api/app/packagemanager/state (GET)**</span></span>

<span data-ttu-id="853f5-122">Obtient l’état de dans l’installation de l’application progression</span><span class="sxs-lookup"><span data-stu-id="853f5-122">Gets the status of in progress app installation</span></span>

## <a name="dump-collection"></a><span data-ttu-id="853f5-123">Collection de vidages</span><span class="sxs-lookup"><span data-stu-id="853f5-123">Dump collection</span></span>

<span data-ttu-id="853f5-124">**/API/Debug/dump/UserMode/CrashControl (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="853f5-124">**/api/debug/dump/usermode/crashcontrol (DELETE)**</span></span>

<span data-ttu-id="853f5-125">Désactive crash collecte des vidages pour une application chargée indépendamment</span><span class="sxs-lookup"><span data-stu-id="853f5-125">Disables crash dump collection for a sideloaded app</span></span>

<span data-ttu-id="853f5-126">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-126">Parameters</span></span>
* <span data-ttu-id="853f5-127">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="853f5-127">packageFullname : package name</span></span>

<span data-ttu-id="853f5-128">**/API/Debug/dump/UserMode/CrashControl (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-128">**/api/debug/dump/usermode/crashcontrol (GET)**</span></span>

<span data-ttu-id="853f5-129">Obtient les paramètres pour les applications de chargement de version test collecte des vidages sur incident</span><span class="sxs-lookup"><span data-stu-id="853f5-129">Gets settings for sideloaded apps crash dump collection</span></span>

<span data-ttu-id="853f5-130">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-130">Parameters</span></span>
* <span data-ttu-id="853f5-131">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="853f5-131">packageFullname : package name</span></span>

<span data-ttu-id="853f5-132">**/api/debug/dump/usermode/crashcontrol (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-132">**/api/debug/dump/usermode/crashcontrol (POST)**</span></span>

<span data-ttu-id="853f5-133">Active et configure les paramètres de contrôle d’image pour une application chargée indépendamment</span><span class="sxs-lookup"><span data-stu-id="853f5-133">Enables and sets dump control settings for a sideloaded app</span></span>

<span data-ttu-id="853f5-134">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-134">Parameters</span></span>
* <span data-ttu-id="853f5-135">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="853f5-135">packageFullname : package name</span></span>

<span data-ttu-id="853f5-136">**/API/Debug/dump/UserMode/crashdump (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="853f5-136">**/api/debug/dump/usermode/crashdump (DELETE)**</span></span>

<span data-ttu-id="853f5-137">Supprime un vidage sur incident pour une application chargée indépendamment</span><span class="sxs-lookup"><span data-stu-id="853f5-137">Deletes a crash dump for a sideloaded app</span></span>

<span data-ttu-id="853f5-138">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-138">Parameters</span></span>
* <span data-ttu-id="853f5-139">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="853f5-139">packageFullname : package name</span></span>
* <span data-ttu-id="853f5-140">nom de fichier : nom de fichier de vidage</span><span class="sxs-lookup"><span data-stu-id="853f5-140">fileName : dump file name</span></span>

<span data-ttu-id="853f5-141">**/API/Debug/dump/UserMode/crashdump (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-141">**/api/debug/dump/usermode/crashdump (GET)**</span></span>

<span data-ttu-id="853f5-142">Récupère un vidage sur incident pour une application chargée indépendamment</span><span class="sxs-lookup"><span data-stu-id="853f5-142">Retrieves a crash dump for a sideloaded app</span></span>

<span data-ttu-id="853f5-143">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-143">Parameters</span></span>
* <span data-ttu-id="853f5-144">packageFullname : nom du package</span><span class="sxs-lookup"><span data-stu-id="853f5-144">packageFullname : package name</span></span>
* <span data-ttu-id="853f5-145">nom de fichier : nom de fichier de vidage</span><span class="sxs-lookup"><span data-stu-id="853f5-145">fileName : dump file name</span></span>

<span data-ttu-id="853f5-146">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-146">Return data</span></span>
* <span data-ttu-id="853f5-147">Fichier de vidage.</span><span class="sxs-lookup"><span data-stu-id="853f5-147">Dump file.</span></span> <span data-ttu-id="853f5-148">Inspecter avec WinDbg ou Visual Studio</span><span class="sxs-lookup"><span data-stu-id="853f5-148">Inspect with WinDbg or Visual Studio</span></span>

<span data-ttu-id="853f5-149">**/API/Debug/dump/UserMode/dumps (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-149">**/api/debug/dump/usermode/dumps (GET)**</span></span>

<span data-ttu-id="853f5-150">Retourne la liste de tous les vidages sur incident pour les versions test d’applications</span><span class="sxs-lookup"><span data-stu-id="853f5-150">Returns list of all crash dumps for sideloaded apps</span></span>

<span data-ttu-id="853f5-151">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-151">Return data</span></span>
* <span data-ttu-id="853f5-152">Liste de blocage vidages par l’application chargée côté</span><span class="sxs-lookup"><span data-stu-id="853f5-152">List of crash dumps per side loaded app</span></span>

## <a name="etw"></a><span data-ttu-id="853f5-153">ETW</span><span class="sxs-lookup"><span data-stu-id="853f5-153">ETW</span></span>

<span data-ttu-id="853f5-154">**/api/etw/providers (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-154">**/api/etw/providers (GET)**</span></span>

<span data-ttu-id="853f5-155">Énumère les fournisseurs inscrits</span><span class="sxs-lookup"><span data-stu-id="853f5-155">Enumerates registered providers</span></span>

<span data-ttu-id="853f5-156">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-156">Return data</span></span>
* <span data-ttu-id="853f5-157">Liste des fournisseurs, nom convivial et GUID</span><span class="sxs-lookup"><span data-stu-id="853f5-157">List of providers, friendly name and GUID</span></span>

<span data-ttu-id="853f5-158">**/API/ETW/session/Realtime (GET/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="853f5-158">**/api/etw/session/realtime (GET/WebSocket)**</span></span>

<span data-ttu-id="853f5-159">Crée une session ETW en temps réel. gérés via un websocket.</span><span class="sxs-lookup"><span data-stu-id="853f5-159">Creates a realtime ETW session; managed over a websocket.</span></span>

<span data-ttu-id="853f5-160">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-160">Return data</span></span>
* <span data-ttu-id="853f5-161">Événements ETW à partir de fournisseurs activés</span><span class="sxs-lookup"><span data-stu-id="853f5-161">ETW events from the enabled providers</span></span>

## <a name="holographic-os"></a><span data-ttu-id="853f5-162">Système d’exploitation holographique</span><span class="sxs-lookup"><span data-stu-id="853f5-162">Holographic OS</span></span>

<span data-ttu-id="853f5-163">**/API/Holographic/OS/ETW/customproviders (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-163">**/api/holographic/os/etw/customproviders (GET)**</span></span>

<span data-ttu-id="853f5-164">Retourne une liste des fournisseurs ETW spécifiques HoloLens qui ne sont pas inscrits avec le système</span><span class="sxs-lookup"><span data-stu-id="853f5-164">Returns a list of HoloLens specific ETW providers that are not registered with the system</span></span>

<span data-ttu-id="853f5-165">**/API/Holographic/OS/Services (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-165">**/api/holographic/os/services (GET)**</span></span>

<span data-ttu-id="853f5-166">Retourne les États de tous les services en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="853f5-166">Returns the states of all services running.</span></span>

<span data-ttu-id="853f5-167">**/API/Holographic/OS/Settings/IPD (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-167">**/api/holographic/os/settings/ipd (GET)**</span></span>

<span data-ttu-id="853f5-168">Obtient l’IPD stockée (distance Interpupillary) en millimètres</span><span class="sxs-lookup"><span data-stu-id="853f5-168">Gets the stored IPD (Interpupillary distance) in millimeters</span></span>

<span data-ttu-id="853f5-169">**/API/Holographic/OS/Settings/IPD (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-169">**/api/holographic/os/settings/ipd (POST)**</span></span>

<span data-ttu-id="853f5-170">Définit l’IPD</span><span class="sxs-lookup"><span data-stu-id="853f5-170">Sets the IPD</span></span>

<span data-ttu-id="853f5-171">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-171">Parameters</span></span>
* <span data-ttu-id="853f5-172">IPD : Nouvelle valeur IPD à être définies en millimètres</span><span class="sxs-lookup"><span data-stu-id="853f5-172">ipd : New IPD value to be set in millimeters</span></span>

<span data-ttu-id="853f5-173">**/api/holographic/os/webmanagement/settings/https (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-173">**/api/holographic/os/webmanagement/settings/https (GET)**</span></span>

<span data-ttu-id="853f5-174">Obtenir la spécification HTTPS pour Device Portal</span><span class="sxs-lookup"><span data-stu-id="853f5-174">Get HTTPS requirements for the Device Portal</span></span>

<span data-ttu-id="853f5-175">**/api/holographic/os/webmanagement/settings/https (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-175">**/api/holographic/os/webmanagement/settings/https (POST)**</span></span>

<span data-ttu-id="853f5-176">Définit les conditions requises de HTTPS pour le portail de l’appareil</span><span class="sxs-lookup"><span data-stu-id="853f5-176">Sets HTTPS requirements for the Device Portal</span></span>

<span data-ttu-id="853f5-177">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-177">Parameters</span></span>
* <span data-ttu-id="853f5-178">requis : Oui, non ou par défaut</span><span class="sxs-lookup"><span data-stu-id="853f5-178">required : yes, no or default</span></span>

## <a name="holographic-perception"></a><span data-ttu-id="853f5-179">Perception HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="853f5-179">Holographic Perception</span></span>

<span data-ttu-id="853f5-180">**/API/Holographic/perception/client (GET/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="853f5-180">**/api/holographic/perception/client (GET/WebSocket)**</span></span>

<span data-ttu-id="853f5-181">Accepte les mises à niveau websocket et exécute un client de perception qui envoie des mises à jour à 30 i/s.</span><span class="sxs-lookup"><span data-stu-id="853f5-181">Accepts websocket upgrades and runs a perception client that sends updates at 30 fps.</span></span>

<span data-ttu-id="853f5-182">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-182">Parameters</span></span>
* <span data-ttu-id="853f5-183">clientmode : « actif » force le mode de suivi visuel quand il ne peut pas être établie passivement</span><span class="sxs-lookup"><span data-stu-id="853f5-183">clientmode: "active" forces visual tracking mode when it can't be established passively</span></span>

## <a name="holographic-thermal"></a><span data-ttu-id="853f5-184">Thermique HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="853f5-184">Holographic Thermal</span></span>

<span data-ttu-id="853f5-185">**/API/Holographic/Thermal/Stage (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-185">**/api/holographic/thermal/stage (GET)**</span></span>

<span data-ttu-id="853f5-186">Obtenir de l’étape thermique de l’appareil (normal 0, 1 à chaud, 2 critique)</span><span class="sxs-lookup"><span data-stu-id="853f5-186">Get the thermal stage of the device (0 normal, 1 warm, 2 critical)</span></span>

## <a name="perception-simulation-control"></a><span data-ttu-id="853f5-187">Contrôle de Simulation de perception</span><span class="sxs-lookup"><span data-stu-id="853f5-187">Perception Simulation Control</span></span>

<span data-ttu-id="853f5-188">**/API/Holographic/simulation/Control/mode (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-188">**/api/holographic/simulation/control/mode (GET)**</span></span>

<span data-ttu-id="853f5-189">Obtenir le mode de simulation</span><span class="sxs-lookup"><span data-stu-id="853f5-189">Get the simulation mode</span></span>

<span data-ttu-id="853f5-190">**/API/Holographic/simulation/Control/mode (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-190">**/api/holographic/simulation/control/mode (POST)**</span></span>

<span data-ttu-id="853f5-191">Définir le mode de simulation</span><span class="sxs-lookup"><span data-stu-id="853f5-191">Set the simulation mode</span></span>

<span data-ttu-id="853f5-192">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-192">Parameters</span></span>
* <span data-ttu-id="853f5-193">mode : mode de simulation : par défaut, simulation, à distance, hérité</span><span class="sxs-lookup"><span data-stu-id="853f5-193">mode : simulation mode: default, simulation, remote, legacy</span></span>

<span data-ttu-id="853f5-194">**/API/Holographic/simulation/Control/Stream (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="853f5-194">**/api/holographic/simulation/control/stream (DELETE)**</span></span>

<span data-ttu-id="853f5-195">Supprimer un flux de contrôle.</span><span class="sxs-lookup"><span data-stu-id="853f5-195">Delete a control stream.</span></span>

<span data-ttu-id="853f5-196">**/API/Holographic/simulation/Control/Stream (GET/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="853f5-196">**/api/holographic/simulation/control/stream (GET/WebSocket)**</span></span>

<span data-ttu-id="853f5-197">Ouvrir une connexion de socket web pour un flux de contrôle.</span><span class="sxs-lookup"><span data-stu-id="853f5-197">Open a web socket connection for a control stream.</span></span>

<span data-ttu-id="853f5-198">**/API/Holographic/simulation/Control/Stream (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-198">**/api/holographic/simulation/control/stream (POST)**</span></span>

<span data-ttu-id="853f5-199">Créer un flux de contrôle (la priorité est requise) ou publier des données sur un flux créé (streamId requis).</span><span class="sxs-lookup"><span data-stu-id="853f5-199">Create a control stream (priority is required) or post data to a created stream (streamId required).</span></span> <span data-ttu-id="853f5-200">Les données publiées sont censées être de type « application/octet-stream ».</span><span class="sxs-lookup"><span data-stu-id="853f5-200">Posted data is expected to be of type 'application/octet-stream'.</span></span>

## <a name="perception-simulation-playback"></a><span data-ttu-id="853f5-201">Lecture de Simulation de perception</span><span class="sxs-lookup"><span data-stu-id="853f5-201">Perception Simulation Playback</span></span>

<span data-ttu-id="853f5-202">**/API/Holographic/simulation/Playback/File (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="853f5-202">**/api/holographic/simulation/playback/file (DELETE)**</span></span>

<span data-ttu-id="853f5-203">Supprimer un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-203">Delete a recording.</span></span>

<span data-ttu-id="853f5-204">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-204">Parameters</span></span>
* <span data-ttu-id="853f5-205">enregistrement : Nom de l’enregistrement pour la supprimer.</span><span class="sxs-lookup"><span data-stu-id="853f5-205">recording : Name of recording to delete.</span></span>

<span data-ttu-id="853f5-206">**/API/Holographic/simulation/Playback/File (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-206">**/api/holographic/simulation/playback/file (POST)**</span></span>

<span data-ttu-id="853f5-207">Téléchargez un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-207">Upload a recording.</span></span>

<span data-ttu-id="853f5-208">**/API/Holographic/simulation/Playback/Files (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-208">**/api/holographic/simulation/playback/files (GET)**</span></span>

<span data-ttu-id="853f5-209">Obtenir tous les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="853f5-209">Get all recordings.</span></span>

<span data-ttu-id="853f5-210">**/API/Holographic/simulation/Playback/session (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-210">**/api/holographic/simulation/playback/session (GET)**</span></span>

<span data-ttu-id="853f5-211">Obtenir l’état actuel de la lecture de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-211">Get the current playback state of a recording.</span></span>

<span data-ttu-id="853f5-212">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-212">Parameters</span></span>
* <span data-ttu-id="853f5-213">enregistrement : Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-213">recording : Name of recording.</span></span>

<span data-ttu-id="853f5-214">**/API/Holographic/simulation/Playback/session/file (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="853f5-214">**/api/holographic/simulation/playback/session/file (DELETE)**</span></span>

<span data-ttu-id="853f5-215">Décharger un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-215">Unload a recording.</span></span>

<span data-ttu-id="853f5-216">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-216">Parameters</span></span>
* <span data-ttu-id="853f5-217">enregistrement : Nom de l’enregistrement pour décharger.</span><span class="sxs-lookup"><span data-stu-id="853f5-217">recording : Name of recording to unload.</span></span>

<span data-ttu-id="853f5-218">**/API/Holographic/simulation/Playback/session/file (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-218">**/api/holographic/simulation/playback/session/file (POST)**</span></span>

<span data-ttu-id="853f5-219">Charger un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-219">Load a recording.</span></span>

<span data-ttu-id="853f5-220">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-220">Parameters</span></span>
* <span data-ttu-id="853f5-221">enregistrement : Nom de l’enregistrement pour la charge.</span><span class="sxs-lookup"><span data-stu-id="853f5-221">recording : Name of recording to load.</span></span>

<span data-ttu-id="853f5-222">**/API/Holographic/simulation/Playback/session/files (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-222">**/api/holographic/simulation/playback/session/files (GET)**</span></span>

<span data-ttu-id="853f5-223">Obtenir des enregistrements tous chargés.</span><span class="sxs-lookup"><span data-stu-id="853f5-223">Get all loaded recordings.</span></span>

<span data-ttu-id="853f5-224">**/API/Holographic/simulation/Playback/session/pause (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-224">**/api/holographic/simulation/playback/session/pause (POST)**</span></span>

<span data-ttu-id="853f5-225">Suspendre un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-225">Pause a recording.</span></span>

<span data-ttu-id="853f5-226">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-226">Parameters</span></span>
* <span data-ttu-id="853f5-227">enregistrement : Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-227">recording : Name of recording.</span></span>

<span data-ttu-id="853f5-228">**/API/Holographic/simulation/Playback/session/Play (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-228">**/api/holographic/simulation/playback/session/play (POST)**</span></span>

<span data-ttu-id="853f5-229">Lire un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-229">Play a recording.</span></span>

<span data-ttu-id="853f5-230">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-230">Parameters</span></span>
* <span data-ttu-id="853f5-231">enregistrement : Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-231">recording : Name of recording.</span></span>

<span data-ttu-id="853f5-232">**/API/Holographic/simulation/Playback/session/Stop (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-232">**/api/holographic/simulation/playback/session/stop (POST)**</span></span>

<span data-ttu-id="853f5-233">Arrêter un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-233">Stop a recording.</span></span>

<span data-ttu-id="853f5-234">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-234">Parameters</span></span>
* <span data-ttu-id="853f5-235">enregistrement : Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-235">recording : Name of recording.</span></span>

<span data-ttu-id="853f5-236">**/API/Holographic/simulation/Playback/session/types (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-236">**/api/holographic/simulation/playback/session/types (GET)**</span></span>

<span data-ttu-id="853f5-237">Obtenir les types de données dans un enregistrement chargé.</span><span class="sxs-lookup"><span data-stu-id="853f5-237">Get the types of data in a loaded recording.</span></span>

<span data-ttu-id="853f5-238">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-238">Parameters</span></span>
* <span data-ttu-id="853f5-239">enregistrement : Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-239">recording : Name of recording.</span></span>

## <a name="perception-simulation-recording"></a><span data-ttu-id="853f5-240">Enregistrement de Simulation de perception</span><span class="sxs-lookup"><span data-stu-id="853f5-240">Perception Simulation Recording</span></span>

<span data-ttu-id="853f5-241">**/API/Holographic/simulation/Recording/Start (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-241">**/api/holographic/simulation/recording/start (POST)**</span></span>

<span data-ttu-id="853f5-242">Démarrer un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-242">Start a recording.</span></span> <span data-ttu-id="853f5-243">Un enregistrement unique peut être actif à la fois.</span><span class="sxs-lookup"><span data-stu-id="853f5-243">Only a single recording can be active at once.</span></span> <span data-ttu-id="853f5-244">Head, mains, spatialMapping ou environnement doit être définie.</span><span class="sxs-lookup"><span data-stu-id="853f5-244">One of head, hands, spatialMapping or environment must be set.</span></span>

<span data-ttu-id="853f5-245">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-245">Parameters</span></span>
* <span data-ttu-id="853f5-246">head : Définissez sur 1 pour les données de l’enregistrement principal.</span><span class="sxs-lookup"><span data-stu-id="853f5-246">head : Set to 1 to record head data.</span></span>
* <span data-ttu-id="853f5-247">mains : La valeur 1 pour enregistrer les données manuellement.</span><span class="sxs-lookup"><span data-stu-id="853f5-247">hands : Set to 1 to record hand data.</span></span>
* <span data-ttu-id="853f5-248">spatialMapping : La valeur 1 pour enregistrer le mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="853f5-248">spatialMapping : Set to 1 to record spatial mapping.</span></span>
* <span data-ttu-id="853f5-249">environnement : La valeur 1 pour enregistrer les données de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="853f5-249">environment : Set to 1 to record environment data.</span></span>
* <span data-ttu-id="853f5-250">nom : Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="853f5-250">name : Name of the recording.</span></span>
* <span data-ttu-id="853f5-251">singleSpatialMappingFrame : La valeur 1 pour enregistrer uniquement une trame de mappage spatial unique.</span><span class="sxs-lookup"><span data-stu-id="853f5-251">singleSpatialMappingFrame : Set to 1 to record only a single spatial mapping frame.</span></span>

<span data-ttu-id="853f5-252">**/API/Holographic/simulation/Recording/Status (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-252">**/api/holographic/simulation/recording/status (GET)**</span></span>

<span data-ttu-id="853f5-253">Obtenir enregistrement d’état.</span><span class="sxs-lookup"><span data-stu-id="853f5-253">Get recording state.</span></span>

<span data-ttu-id="853f5-254">**/API/Holographic/simulation/Recording/Stop (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-254">**/api/holographic/simulation/recording/stop (GET)**</span></span>

<span data-ttu-id="853f5-255">Arrêter l’enregistrement actuel.</span><span class="sxs-lookup"><span data-stu-id="853f5-255">Stop the current recording.</span></span> <span data-ttu-id="853f5-256">L’enregistrement s’affichera sous forme de fichier.</span><span class="sxs-lookup"><span data-stu-id="853f5-256">Recording will be returned as a file.</span></span>

## <a name="mixed-reality-capture"></a><span data-ttu-id="853f5-257">MRC (Mixed Reality Capture)</span><span class="sxs-lookup"><span data-stu-id="853f5-257">Mixed Reality Capture</span></span>

<span data-ttu-id="853f5-258">**/API/Holographic/MRC/file (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-258">**/api/holographic/mrc/file (GET)**</span></span>

<span data-ttu-id="853f5-259">Télécharge un fichier de réalité mixte à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="853f5-259">Downloads a mixed reality file from the device.</span></span> <span data-ttu-id="853f5-260">Emploi de = le paramètre de requête de flux de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="853f5-260">Use op=stream query parameter for streaming.</span></span>

<span data-ttu-id="853f5-261">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-261">Parameters</span></span>
* <span data-ttu-id="853f5-262">nom de fichier : Nom, hex64 encodée du fichier vidéo à obtenir</span><span class="sxs-lookup"><span data-stu-id="853f5-262">filename : Name, hex64 encoded, of the video file to get</span></span>
* <span data-ttu-id="853f5-263">op : flux de données</span><span class="sxs-lookup"><span data-stu-id="853f5-263">op : stream</span></span>

<span data-ttu-id="853f5-264">**/API/Holographic/MRC/file (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="853f5-264">**/api/holographic/mrc/file (DELETE)**</span></span>

<span data-ttu-id="853f5-265">Supprime une réalité mixte enregistrant à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="853f5-265">Deletes a mixed reality recording from the device.</span></span>

<span data-ttu-id="853f5-266">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-266">Parameters</span></span>
* <span data-ttu-id="853f5-267">nom de fichier : Nom, hex64 encodée du fichier à supprimer</span><span class="sxs-lookup"><span data-stu-id="853f5-267">filename : Name, hex64 encoded, of the file to delete</span></span>

<span data-ttu-id="853f5-268">**/API/Holographic/MRC/Files (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-268">**/api/holographic/mrc/files (GET)**</span></span>

<span data-ttu-id="853f5-269">Retourne la liste des fichiers de réalité mixte stockées sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="853f5-269">Returns the list of mixed reality files stored on the device</span></span>

<span data-ttu-id="853f5-270">**/API/Holographic/MRC/photo (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-270">**/api/holographic/mrc/photo (POST)**</span></span>

<span data-ttu-id="853f5-271">Prend une photo de réalité mixte et crée un fichier sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="853f5-271">Takes a mixed reality photo and creates a file on the device</span></span>

<span data-ttu-id="853f5-272">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-272">Parameters</span></span>
* <span data-ttu-id="853f5-273">Holo : capturer hologrammes : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-273">holo : capture holograms: true or false (defaults to false)</span></span>
* <span data-ttu-id="853f5-274">PV : capture PV caméra : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-274">pv : capture PV camera: true or false (defaults to false)</span></span>
* <span data-ttu-id="853f5-275">RenderFromCamera : Rendu (HoloLens 2 seulement) du point de vue de la caméra vidéo/photo : true ou false (true par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-275">RenderFromCamera : (HoloLens 2 only) render from perspective of photo/video camera: true or false (defaults to true)</span></span>

<span data-ttu-id="853f5-276">**/API/Holographic/MRC/Settings (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-276">**/api/holographic/mrc/settings (GET)**</span></span>

<span data-ttu-id="853f5-277">Obtient la valeur par défaut une réalité mixte paramètres de capture</span><span class="sxs-lookup"><span data-stu-id="853f5-277">Gets the default mixed reality capture settings</span></span>

<span data-ttu-id="853f5-278">**/API/Holographic/MRC/Settings (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-278">**/api/holographic/mrc/settings (POST)**</span></span>

<span data-ttu-id="853f5-279">Définit la valeur par défaut une réalité mixte paramètres de capture.</span><span class="sxs-lookup"><span data-stu-id="853f5-279">Sets the default mixed reality capture settings.</span></span>  <span data-ttu-id="853f5-280">Certains de ces paramètres sont appliqués à la photo de cette option et la capture vidéo du système.</span><span class="sxs-lookup"><span data-stu-id="853f5-280">Some of these settings are applied to the system's MRC photo and video capture.</span></span>

<span data-ttu-id="853f5-281">**/API/Holographic/MRC/Status (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-281">**/api/holographic/mrc/status (GET)**</span></span>

<span data-ttu-id="853f5-282">Obtient l’état de la réalité mixte enregistrée (en cours d’exécution, arrêté)</span><span class="sxs-lookup"><span data-stu-id="853f5-282">Gets the status of the mixed reality recorded (running, stopped)</span></span>

<span data-ttu-id="853f5-283">**/API/Holographic/MRC/Thumbnail (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-283">**/api/holographic/mrc/thumbnail (GET)**</span></span>

<span data-ttu-id="853f5-284">Obtient l’image miniature pour le fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="853f5-284">Gets the thumbnail image for the specified file.</span></span>

<span data-ttu-id="853f5-285">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-285">Parameters</span></span>
* <span data-ttu-id="853f5-286">nom de fichier : Nom, hex64 encodée du fichier pour lequel la miniature est demandée</span><span class="sxs-lookup"><span data-stu-id="853f5-286">filename: Name, hex64 encoded, of the file for which the thumbnail is being requested</span></span>

<span data-ttu-id="853f5-287">**/API/Holographic/MRC/Video/Control/Start (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-287">**/api/holographic/mrc/video/control/start (POST)**</span></span>

<span data-ttu-id="853f5-288">Démarre un enregistrement de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="853f5-288">Starts a mixed reality recording</span></span>

<span data-ttu-id="853f5-289">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-289">Parameters</span></span>
* <span data-ttu-id="853f5-290">Holo : capturer hologrammes : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-290">holo : capture holograms: true or false (defaults to false)</span></span>
* <span data-ttu-id="853f5-291">PV : capture PV caméra : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-291">pv : capture PV camera: true or false (defaults to false)</span></span>
* <span data-ttu-id="853f5-292">MIC : capture microphone : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-292">mic : capture microphone: true or false (defaults to false)</span></span>
* <span data-ttu-id="853f5-293">bouclage : capturer des données audio app : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-293">loopback : capture app audio: true or false (defaults to false)</span></span>
* <span data-ttu-id="853f5-294">RenderFromCamera : Rendu (HoloLens 2 seulement) du point de vue de la caméra vidéo/photo : true ou false (true par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-294">RenderFromCamera : (HoloLens 2 only) render from perspective of photo/video camera: true or false (defaults to true)</span></span>
* <span data-ttu-id="853f5-295">Vstab : Activer (HoloLens 2 seulement) une stabilisation vidéo : true ou false (true par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-295">vstab : (HoloLens 2 only) enable video stabilization: true or false (defaults to true)</span></span>
* <span data-ttu-id="853f5-296">vstabbuffer : Latence de mémoire tampon de stabilisation vidéo (2 HoloLens uniquement) : 0 et 30 frames (15 images par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-296">vstabbuffer: (HoloLens 2 only) video stabilization buffer latency: 0 to 30 frames (defaults to 15 frames)</span></span>

<span data-ttu-id="853f5-297">**/API/Holographic/MRC/Video/Control/Stop (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-297">**/api/holographic/mrc/video/control/stop (POST)**</span></span>

<span data-ttu-id="853f5-298">S’arrête en cours mixte d’enregistrement de réalité</span><span class="sxs-lookup"><span data-stu-id="853f5-298">Stops the current mixed reality recording</span></span>

## <a name="mixed-reality-streaming"></a><span data-ttu-id="853f5-299">Réalité mixte de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="853f5-299">Mixed Reality Streaming</span></span>

<span data-ttu-id="853f5-300">HoloLens prend en charge l’aperçu instantané de réalité mixte par téléchargement mémorisé en bloc d’un fichier mp4 fragmenté.</span><span class="sxs-lookup"><span data-stu-id="853f5-300">HoloLens supports live preview of mixed reality via chunked download of a fragmented mp4.</span></span>

<span data-ttu-id="853f5-301">Flux de réalité mixte partagent le même jeu de paramètres pour contrôler ce qui est capturé :</span><span class="sxs-lookup"><span data-stu-id="853f5-301">Mixed reality streams share the same set of parameters to control what is captured:</span></span>
* <span data-ttu-id="853f5-302">Holo : capturer hologrammes : true ou false</span><span class="sxs-lookup"><span data-stu-id="853f5-302">holo : capture holograms: true or false</span></span>
* <span data-ttu-id="853f5-303">PV : capture PV caméra : true ou false</span><span class="sxs-lookup"><span data-stu-id="853f5-303">pv : capture PV camera: true or false</span></span>
* <span data-ttu-id="853f5-304">MIC : capture microphone : true ou false</span><span class="sxs-lookup"><span data-stu-id="853f5-304">mic : capture microphone: true or false</span></span>
* <span data-ttu-id="853f5-305">bouclage : capturer des données audio app : true ou false</span><span class="sxs-lookup"><span data-stu-id="853f5-305">loopback : capture app audio: true or false</span></span>

<span data-ttu-id="853f5-306">Si aucune d'entre elles sont spécifiées : hologrammes, caméra photo/vidéo et audio de l’application seront capturées</span><span class="sxs-lookup"><span data-stu-id="853f5-306">If none of these are specified: holograms, photo/video camera, and app audio will be captured</span></span><br>
<span data-ttu-id="853f5-307">Si une est spécifiée : false par défaut les paramètres non spécifiés</span><span class="sxs-lookup"><span data-stu-id="853f5-307">If any are specified: the unspecified parameters will default to false</span></span>

<span data-ttu-id="853f5-308">Paramètres facultatifs (HoloLens 2 uniquement)</span><span class="sxs-lookup"><span data-stu-id="853f5-308">Optional parameters (HoloLens 2 only)</span></span>
* <span data-ttu-id="853f5-309">RenderFromCamera : effectuer le rendu du point de vue de la caméra vidéo/photo : true ou false (true par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-309">RenderFromCamera : render from perspective of photo/video camera: true or false (defaults to true)</span></span>
* <span data-ttu-id="853f5-310">Vstab : activer une stabilisation vidéo : true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-310">vstab : enable video stabilization: true or false (defaults to false)</span></span>
* <span data-ttu-id="853f5-311">vstabbuffer : latence de mémoire tampon de stabilisation vidéo : 0 et 30 frames (15 images par défaut)</span><span class="sxs-lookup"><span data-stu-id="853f5-311">vstabbuffer: video stabilization buffer latency: 0 to 30 frames (defaults to 15 frames)</span></span>

<span data-ttu-id="853f5-312">**/api/holographic/stream/live.mp4 (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-312">**/api/holographic/stream/live.mp4 (GET)**</span></span>

<span data-ttu-id="853f5-313">Un flux de 5Mbit 1280x720p 30 i/s.</span><span class="sxs-lookup"><span data-stu-id="853f5-313">A 1280x720p 30fps 5Mbit stream.</span></span>

<span data-ttu-id="853f5-314">**/api/holographic/stream/live_high.mp4 (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-314">**/api/holographic/stream/live_high.mp4 (GET)**</span></span>

<span data-ttu-id="853f5-315">Un flux de 5Mbit 1280x720p 30 i/s.</span><span class="sxs-lookup"><span data-stu-id="853f5-315">A 1280x720p 30fps 5Mbit stream.</span></span>

<span data-ttu-id="853f5-316">**/api/holographic/stream/live_med.mp4 (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-316">**/api/holographic/stream/live_med.mp4 (GET)**</span></span>

<span data-ttu-id="853f5-317">Un flux de 30 i/s 2.5Mbit 854x480p.</span><span class="sxs-lookup"><span data-stu-id="853f5-317">A 854x480p 30fps 2.5Mbit stream.</span></span>

<span data-ttu-id="853f5-318">**/api/holographic/stream/live_low.mp4 (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-318">**/api/holographic/stream/live_low.mp4 (GET)**</span></span>

<span data-ttu-id="853f5-319">Un flux de 15 i/s 0.6Mbit 428x240p.</span><span class="sxs-lookup"><span data-stu-id="853f5-319">A 428x240p 15fps 0.6Mbit stream.</span></span>

## <a name="networking"></a><span data-ttu-id="853f5-320">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="853f5-320">Networking</span></span>

<span data-ttu-id="853f5-321">**/api/networking/ipconfig (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-321">**/api/networking/ipconfig (GET)**</span></span>

<span data-ttu-id="853f5-322">Obtient la configuration ip actuelle</span><span class="sxs-lookup"><span data-stu-id="853f5-322">Gets the current ip configuration</span></span>

## <a name="os-information"></a><span data-ttu-id="853f5-323">Informations de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="853f5-323">OS Information</span></span>

<span data-ttu-id="853f5-324">**/api/os/info (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-324">**/api/os/info (GET)**</span></span>

<span data-ttu-id="853f5-325">Obtient des informations de système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="853f5-325">Gets operating system information</span></span>

<span data-ttu-id="853f5-326">**/API/OS/MachineName (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-326">**/api/os/machinename (GET)**</span></span>

<span data-ttu-id="853f5-327">Obtient le nom de l’ordinateur</span><span class="sxs-lookup"><span data-stu-id="853f5-327">Gets the machine name</span></span>

<span data-ttu-id="853f5-328">**/api/os/machinename (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-328">**/api/os/machinename (POST)**</span></span>

<span data-ttu-id="853f5-329">Définit le nom de l’ordinateur</span><span class="sxs-lookup"><span data-stu-id="853f5-329">Sets the machine name</span></span>

<span data-ttu-id="853f5-330">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-330">Parameters</span></span>
* <span data-ttu-id="853f5-331">nom : Nouveau nom de l’ordinateur, hex64 encodée, pour la valeur</span><span class="sxs-lookup"><span data-stu-id="853f5-331">name : New machine name, hex64 encoded, to set to</span></span>

## <a name="performance-data"></a><span data-ttu-id="853f5-332">Données relatives aux performances</span><span class="sxs-lookup"><span data-stu-id="853f5-332">Performance data</span></span>

<span data-ttu-id="853f5-333">**/API/ResourceManager/Processes (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-333">**/api/resourcemanager/processes (GET)**</span></span>

<span data-ttu-id="853f5-334">Retourne la liste des processus en cours avec les détails</span><span class="sxs-lookup"><span data-stu-id="853f5-334">Returns the list of running processes with details</span></span>

<span data-ttu-id="853f5-335">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-335">Return data</span></span>
* <span data-ttu-id="853f5-336">JSON avec la liste des processus et les détails de chaque processus</span><span class="sxs-lookup"><span data-stu-id="853f5-336">JSON with list of processes and details for each process</span></span>

<span data-ttu-id="853f5-337">**/API/ResourceManager/systemperf (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-337">**/api/resourcemanager/systemperf (GET)**</span></span>

<span data-ttu-id="853f5-338">Retourne des statistiques de performances système (e/s en lecture/écriture, etc. statistiques de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="853f5-338">Returns system perf statistics (I/O read/write, memory stats etc.</span></span>

<span data-ttu-id="853f5-339">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-339">Return data</span></span>
* <span data-ttu-id="853f5-340">JSON avec les informations système : Processeur, processeur, mémoire, réseau, e/s</span><span class="sxs-lookup"><span data-stu-id="853f5-340">JSON with system information: CPU, GPU, Memory, Network, IO</span></span>

## <a name="power"></a><span data-ttu-id="853f5-341">Marche/Arrêt</span><span class="sxs-lookup"><span data-stu-id="853f5-341">Power</span></span>

<span data-ttu-id="853f5-342">**/api/power/battery (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-342">**/api/power/battery (GET)**</span></span>

<span data-ttu-id="853f5-343">Obtient l’état actuel de la batterie</span><span class="sxs-lookup"><span data-stu-id="853f5-343">Gets the current battery state</span></span>

<span data-ttu-id="853f5-344">**/API/Power/State (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-344">**/api/power/state (GET)**</span></span>

<span data-ttu-id="853f5-345">Vérifie si le système est dans un état de faible consommation d’énergie</span><span class="sxs-lookup"><span data-stu-id="853f5-345">Checks if the system is in a low power state</span></span>

## <a name="remote-control"></a><span data-ttu-id="853f5-346">Contrôle à distance</span><span class="sxs-lookup"><span data-stu-id="853f5-346">Remote Control</span></span>

<span data-ttu-id="853f5-347">**/api/control/restart (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-347">**/api/control/restart (POST)**</span></span>

<span data-ttu-id="853f5-348">Redémarre l’appareil cible</span><span class="sxs-lookup"><span data-stu-id="853f5-348">Restarts the target device</span></span>

<span data-ttu-id="853f5-349">**/API/Control/Shutdown (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-349">**/api/control/shutdown (POST)**</span></span>

<span data-ttu-id="853f5-350">Arrête l’appareil cible</span><span class="sxs-lookup"><span data-stu-id="853f5-350">Shuts down the target device</span></span>

## <a name="task-manager"></a><span data-ttu-id="853f5-351">Gestionnaire des tâches</span><span class="sxs-lookup"><span data-stu-id="853f5-351">Task Manager</span></span>

<span data-ttu-id="853f5-352">**/API/TaskManager/App (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="853f5-352">**/api/taskmanager/app (DELETE)**</span></span>

<span data-ttu-id="853f5-353">Arrête une application moderne</span><span class="sxs-lookup"><span data-stu-id="853f5-353">Stops a modern app</span></span>

<span data-ttu-id="853f5-354">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-354">Parameters</span></span>
* <span data-ttu-id="853f5-355">package : Nom complet du package d’application, hex64 encodé</span><span class="sxs-lookup"><span data-stu-id="853f5-355">package : Full name of the app package, hex64 encoded</span></span>
* <span data-ttu-id="853f5-356">arrêt forcé : Forcer tous les processus à arrêter (= yes)</span><span class="sxs-lookup"><span data-stu-id="853f5-356">forcestop : Force all processes to stop (=yes)</span></span>

<span data-ttu-id="853f5-357">**/api/taskmanager/app (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-357">**/api/taskmanager/app (POST)**</span></span>

<span data-ttu-id="853f5-358">Démarre une application moderne</span><span class="sxs-lookup"><span data-stu-id="853f5-358">Starts a modern app</span></span>

<span data-ttu-id="853f5-359">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-359">Parameters</span></span>
* <span data-ttu-id="853f5-360">ID d’application : PRAID d’application pour démarrer, hex64 encodé</span><span class="sxs-lookup"><span data-stu-id="853f5-360">appid : PRAID of app to start, hex64 encoded</span></span>
* <span data-ttu-id="853f5-361">package : Nom complet du package d’application, hex64 encodé</span><span class="sxs-lookup"><span data-stu-id="853f5-361">package : Full name of the app package, hex64 encoded</span></span>

## <a name="wifi-management"></a><span data-ttu-id="853f5-362">Gestion de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="853f5-362">WiFi Management</span></span>

<span data-ttu-id="853f5-363">**/api/wifi/interfaces (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-363">**/api/wifi/interfaces (GET)**</span></span>

<span data-ttu-id="853f5-364">Énumère les interfaces de réseau sans fil</span><span class="sxs-lookup"><span data-stu-id="853f5-364">Enumerates wireless network interfaces</span></span>

<span data-ttu-id="853f5-365">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-365">Return data</span></span>
* <span data-ttu-id="853f5-366">Liste des interfaces sans fil avec les détails (GUID, description, etc.).</span><span class="sxs-lookup"><span data-stu-id="853f5-366">List of wireless interfaces with details (GUID, description etc.)</span></span>

<span data-ttu-id="853f5-367">**/api/wifi/network (DELETE)**</span><span class="sxs-lookup"><span data-stu-id="853f5-367">**/api/wifi/network (DELETE)**</span></span>

<span data-ttu-id="853f5-368">Supprime un profil associé à un réseau sur l’interface spécifiée</span><span class="sxs-lookup"><span data-stu-id="853f5-368">Deletes a profile associated with a network on a specified interface</span></span>

<span data-ttu-id="853f5-369">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-369">Parameters</span></span>
* <span data-ttu-id="853f5-370">interface : guid de l’interface de réseau</span><span class="sxs-lookup"><span data-stu-id="853f5-370">interface : network interface guid</span></span>
* <span data-ttu-id="853f5-371">profil : nom du profil</span><span class="sxs-lookup"><span data-stu-id="853f5-371">profile : profile name</span></span>

<span data-ttu-id="853f5-372">**/API/WiFi/Networks (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-372">**/api/wifi/networks (GET)**</span></span>

<span data-ttu-id="853f5-373">Énumère les réseaux sans fil sur l’interface réseau spécifiée</span><span class="sxs-lookup"><span data-stu-id="853f5-373">Enumerates wireless networks on the specified network interface</span></span>

<span data-ttu-id="853f5-374">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-374">Parameters</span></span>
* <span data-ttu-id="853f5-375">interface : guid de l’interface de réseau</span><span class="sxs-lookup"><span data-stu-id="853f5-375">interface : network interface guid</span></span>

<span data-ttu-id="853f5-376">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-376">Return data</span></span>
* <span data-ttu-id="853f5-377">Liste des réseaux sans fil trouvés sur l’interface réseau avec les détails</span><span class="sxs-lookup"><span data-stu-id="853f5-377">List of wireless networks found on the network interface with details</span></span>

<span data-ttu-id="853f5-378">**/api/wifi/network (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-378">**/api/wifi/network (POST)**</span></span>

<span data-ttu-id="853f5-379">Se connecte ou se déconnecte à un réseau sur l’interface spécifiée</span><span class="sxs-lookup"><span data-stu-id="853f5-379">Connects or disconnects to a network on the specified interface</span></span>

<span data-ttu-id="853f5-380">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-380">Parameters</span></span>
* <span data-ttu-id="853f5-381">interface : guid de l’interface de réseau</span><span class="sxs-lookup"><span data-stu-id="853f5-381">interface : network interface guid</span></span>
* <span data-ttu-id="853f5-382">SSID : ssid, hex64 codé, pour vous connecter à</span><span class="sxs-lookup"><span data-stu-id="853f5-382">ssid : ssid, hex64 encoded, to connect to</span></span>
* <span data-ttu-id="853f5-383">op : connecter ou déconnecter</span><span class="sxs-lookup"><span data-stu-id="853f5-383">op : connect or disconnect</span></span>
* <span data-ttu-id="853f5-384">CreateProfile : yes ou no</span><span class="sxs-lookup"><span data-stu-id="853f5-384">createprofile : yes or no</span></span>
* <span data-ttu-id="853f5-385">clé : partagé hex64 clé, encodé</span><span class="sxs-lookup"><span data-stu-id="853f5-385">key : shared key, hex64 encoded</span></span>

## <a name="windows-performance-recorder"></a><span data-ttu-id="853f5-386">Enregistreur de performances Windows</span><span class="sxs-lookup"><span data-stu-id="853f5-386">Windows Performance Recorder</span></span>

<span data-ttu-id="853f5-387">**/api/wpr/customtrace (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-387">**/api/wpr/customtrace (POST)**</span></span>

<span data-ttu-id="853f5-388">Télécharge un profil WPR et commence le traçage en utilisant le profil téléchargé.</span><span class="sxs-lookup"><span data-stu-id="853f5-388">Uploads a WPR profile and starts tracing using the uploaded profile.</span></span>

<span data-ttu-id="853f5-389">charge utile</span><span class="sxs-lookup"><span data-stu-id="853f5-389">Payload</span></span>
* <span data-ttu-id="853f5-390">corps http conforme à plusieurs parties</span><span class="sxs-lookup"><span data-stu-id="853f5-390">multi-part conforming http body</span></span>

<span data-ttu-id="853f5-391">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-391">Return data</span></span>
* <span data-ttu-id="853f5-392">Retourne l’état de session WPR.</span><span class="sxs-lookup"><span data-stu-id="853f5-392">Returns the WPR session status.</span></span>

<span data-ttu-id="853f5-393">**/api/wpr/status (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-393">**/api/wpr/status (GET)**</span></span>

<span data-ttu-id="853f5-394">Récupère l’état de la session WPR</span><span class="sxs-lookup"><span data-stu-id="853f5-394">Retrieves the status of the WPR session</span></span>

<span data-ttu-id="853f5-395">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-395">Return data</span></span>
* <span data-ttu-id="853f5-396">État de session WPR.</span><span class="sxs-lookup"><span data-stu-id="853f5-396">WPR session status.</span></span>

<span data-ttu-id="853f5-397">**/api/wpr/trace (GET)**</span><span class="sxs-lookup"><span data-stu-id="853f5-397">**/api/wpr/trace (GET)**</span></span>

<span data-ttu-id="853f5-398">Arrête une session de suivi WPR (performance)</span><span class="sxs-lookup"><span data-stu-id="853f5-398">Stops a WPR (performance) tracing session</span></span>

<span data-ttu-id="853f5-399">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-399">Return data</span></span>
* <span data-ttu-id="853f5-400">Retourne le fichier ETL de suivi</span><span class="sxs-lookup"><span data-stu-id="853f5-400">Returns the trace ETL file</span></span>

<span data-ttu-id="853f5-401">**/api/wpr/trace (POST)**</span><span class="sxs-lookup"><span data-stu-id="853f5-401">**/api/wpr/trace (POST)**</span></span>

<span data-ttu-id="853f5-402">Démarre un WPR (performance) suivi des sessions</span><span class="sxs-lookup"><span data-stu-id="853f5-402">Starts a WPR (performance) tracing sessions</span></span>

<span data-ttu-id="853f5-403">Paramètres</span><span class="sxs-lookup"><span data-stu-id="853f5-403">Parameters</span></span>
* <span data-ttu-id="853f5-404">profil : Nom du profil.</span><span class="sxs-lookup"><span data-stu-id="853f5-404">profile : Profile name.</span></span> <span data-ttu-id="853f5-405">Profils disponibles sont stockés dans perfprofiles/profiles.json</span><span class="sxs-lookup"><span data-stu-id="853f5-405">Available profiles are stored in perfprofiles/profiles.json</span></span>

<span data-ttu-id="853f5-406">Retourner des données</span><span class="sxs-lookup"><span data-stu-id="853f5-406">Return data</span></span>
* <span data-ttu-id="853f5-407">Au démarrage, retourne l’état de session WPR.</span><span class="sxs-lookup"><span data-stu-id="853f5-407">On start, returns the WPR session status.</span></span>

## <a name="see-also"></a><span data-ttu-id="853f5-408">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="853f5-408">See also</span></span>
* [<span data-ttu-id="853f5-409">Utilisation du portail d’appareil Windows</span><span class="sxs-lookup"><span data-stu-id="853f5-409">Using the Windows Device Portal</span></span>](using-the-windows-device-portal.md)
* [<span data-ttu-id="853f5-410">Core de portail appareil référence d’API (UWP)</span><span class="sxs-lookup"><span data-stu-id="853f5-410">Device Portal core API reference (UWP)</span></span>](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-api-core)
