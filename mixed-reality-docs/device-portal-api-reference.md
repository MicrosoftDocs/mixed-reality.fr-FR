---
title: Informations de référence sur l’API du portail d’appareils
description: Informations de référence sur l’API pour le portail de périphériques Windows sur HoloLens
author: JonMLyons
ms.author: JLyons
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, portail des appareils Windows, API
ms.openlocfilehash: 4b5b48c13b1b7ec8bfdf447f42097a8448b6a0e6
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694432"
---
# <a name="device-portal-api-reference"></a><span data-ttu-id="39a9e-104">Informations de référence sur l’API du portail d’appareils</span><span class="sxs-lookup"><span data-stu-id="39a9e-104">Device portal API reference</span></span>

<span data-ttu-id="39a9e-105">Tout ce qui se trouve dans le [portail de périphériques Windows](using-the-windows-device-portal.md) repose sur des API REST que vous pouvez utiliser pour accéder aux données et contrôler votre appareil par programme.</span><span class="sxs-lookup"><span data-stu-id="39a9e-105">Everything in the [Windows Device Portal](using-the-windows-device-portal.md) is built on top of REST API's that you can use to access the data and control your device programmatically.</span></span>

## <a name="app-deloyment"></a><span data-ttu-id="39a9e-106">Déploiement de l’application</span><span class="sxs-lookup"><span data-stu-id="39a9e-106">App deloyment</span></span>

<span data-ttu-id="39a9e-107">**/API/App/packagemanager/package (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-107">**/api/app/packagemanager/package (DELETE)**</span></span>

<span data-ttu-id="39a9e-108">Désinstalle une application</span><span class="sxs-lookup"><span data-stu-id="39a9e-108">Uninstalls an app</span></span>

<span data-ttu-id="39a9e-109">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-109">Parameters</span></span>
* <span data-ttu-id="39a9e-110">Packages Nom de fichier du package à désinstaller.</span><span class="sxs-lookup"><span data-stu-id="39a9e-110">package : File name of the package to be uninstalled.</span></span>

<span data-ttu-id="39a9e-111">**/API/App/packagemanager/package (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-111">**/api/app/packagemanager/package (POST)**</span></span>

<span data-ttu-id="39a9e-112">Installe une application</span><span class="sxs-lookup"><span data-stu-id="39a9e-112">Installs an App</span></span>

<span data-ttu-id="39a9e-113">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-113">Parameters</span></span>
* <span data-ttu-id="39a9e-114">Packages Nom de fichier du package à installer.</span><span class="sxs-lookup"><span data-stu-id="39a9e-114">package : File name of the package to be installed.</span></span>

<span data-ttu-id="39a9e-115">Transport</span><span class="sxs-lookup"><span data-stu-id="39a9e-115">Payload</span></span>
* <span data-ttu-id="39a9e-116">corps http en plusieurs parties, conforme</span><span class="sxs-lookup"><span data-stu-id="39a9e-116">multi-part conforming http body</span></span>

<span data-ttu-id="39a9e-117">**/API/App/packagemanager/packages (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-117">**/api/app/packagemanager/packages (GET)**</span></span>

<span data-ttu-id="39a9e-118">Récupère la liste des applications installées sur le système, avec les détails</span><span class="sxs-lookup"><span data-stu-id="39a9e-118">Retrieves the list of installed apps on the system, with details</span></span>

<span data-ttu-id="39a9e-119">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-119">Return data</span></span>
* <span data-ttu-id="39a9e-120">Liste des packages installés avec des détails</span><span class="sxs-lookup"><span data-stu-id="39a9e-120">List of installed packages with details</span></span>

<span data-ttu-id="39a9e-121">**/API/App/packagemanager/State (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-121">**/api/app/packagemanager/state (GET)**</span></span>

<span data-ttu-id="39a9e-122">Obtient l’état de l’installation de l’application en cours</span><span class="sxs-lookup"><span data-stu-id="39a9e-122">Gets the status of in progress app installation</span></span>

## <a name="dump-collection"></a><span data-ttu-id="39a9e-123">Collection de vidages</span><span class="sxs-lookup"><span data-stu-id="39a9e-123">Dump collection</span></span>

<span data-ttu-id="39a9e-124">**/API/Debug/dump/usermode/CrashControl (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-124">**/api/debug/dump/usermode/crashcontrol (DELETE)**</span></span>

<span data-ttu-id="39a9e-125">Désactive la collecte de vidages sur incident pour une application faisant</span><span class="sxs-lookup"><span data-stu-id="39a9e-125">Disables crash dump collection for a sideloaded app</span></span>

<span data-ttu-id="39a9e-126">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-126">Parameters</span></span>
* <span data-ttu-id="39a9e-127">packageFullname: nom du package</span><span class="sxs-lookup"><span data-stu-id="39a9e-127">packageFullname : package name</span></span>

<span data-ttu-id="39a9e-128">**/API/Debug/dump/usermode/CrashControl (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-128">**/api/debug/dump/usermode/crashcontrol (GET)**</span></span>

<span data-ttu-id="39a9e-129">Obtient les paramètres de la collection de vidages sur incident des applications faisant</span><span class="sxs-lookup"><span data-stu-id="39a9e-129">Gets settings for sideloaded apps crash dump collection</span></span>

<span data-ttu-id="39a9e-130">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-130">Parameters</span></span>
* <span data-ttu-id="39a9e-131">packageFullname: nom du package</span><span class="sxs-lookup"><span data-stu-id="39a9e-131">packageFullname : package name</span></span>

<span data-ttu-id="39a9e-132">**/API/Debug/dump/usermode/CrashControl (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-132">**/api/debug/dump/usermode/crashcontrol (POST)**</span></span>

<span data-ttu-id="39a9e-133">Active et définit les paramètres de contrôle de vidage pour une application faisant</span><span class="sxs-lookup"><span data-stu-id="39a9e-133">Enables and sets dump control settings for a sideloaded app</span></span>

<span data-ttu-id="39a9e-134">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-134">Parameters</span></span>
* <span data-ttu-id="39a9e-135">packageFullname: nom du package</span><span class="sxs-lookup"><span data-stu-id="39a9e-135">packageFullname : package name</span></span>

<span data-ttu-id="39a9e-136">**/API/Debug/dump/usermode/crashdump (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-136">**/api/debug/dump/usermode/crashdump (DELETE)**</span></span>

<span data-ttu-id="39a9e-137">Supprime un vidage sur incident pour une application faisant</span><span class="sxs-lookup"><span data-stu-id="39a9e-137">Deletes a crash dump for a sideloaded app</span></span>

<span data-ttu-id="39a9e-138">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-138">Parameters</span></span>
* <span data-ttu-id="39a9e-139">packageFullname: nom du package</span><span class="sxs-lookup"><span data-stu-id="39a9e-139">packageFullname : package name</span></span>
* <span data-ttu-id="39a9e-140">fileName: nom du fichier dump</span><span class="sxs-lookup"><span data-stu-id="39a9e-140">fileName : dump file name</span></span>

<span data-ttu-id="39a9e-141">**/API/Debug/dump/usermode/crashdump (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-141">**/api/debug/dump/usermode/crashdump (GET)**</span></span>

<span data-ttu-id="39a9e-142">Récupère un vidage sur incident pour une application faisant</span><span class="sxs-lookup"><span data-stu-id="39a9e-142">Retrieves a crash dump for a sideloaded app</span></span>

<span data-ttu-id="39a9e-143">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-143">Parameters</span></span>
* <span data-ttu-id="39a9e-144">packageFullname: nom du package</span><span class="sxs-lookup"><span data-stu-id="39a9e-144">packageFullname : package name</span></span>
* <span data-ttu-id="39a9e-145">fileName: nom du fichier dump</span><span class="sxs-lookup"><span data-stu-id="39a9e-145">fileName : dump file name</span></span>

<span data-ttu-id="39a9e-146">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-146">Return data</span></span>
* <span data-ttu-id="39a9e-147">Fichier dump.</span><span class="sxs-lookup"><span data-stu-id="39a9e-147">Dump file.</span></span> <span data-ttu-id="39a9e-148">Inspecter avec WinDbg ou Visual Studio</span><span class="sxs-lookup"><span data-stu-id="39a9e-148">Inspect with WinDbg or Visual Studio</span></span>

<span data-ttu-id="39a9e-149">**/API/Debug/dump/usermode/dumps (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-149">**/api/debug/dump/usermode/dumps (GET)**</span></span>

<span data-ttu-id="39a9e-150">Retourne la liste de tous les vidages sur incident pour les applications faisant</span><span class="sxs-lookup"><span data-stu-id="39a9e-150">Returns list of all crash dumps for sideloaded apps</span></span>

<span data-ttu-id="39a9e-151">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-151">Return data</span></span>
* <span data-ttu-id="39a9e-152">Liste des vidages sur incident par application à chargement latéral</span><span class="sxs-lookup"><span data-stu-id="39a9e-152">List of crash dumps per side loaded app</span></span>

## <a name="etw"></a><span data-ttu-id="39a9e-153">ETW</span><span class="sxs-lookup"><span data-stu-id="39a9e-153">ETW</span></span>

<span data-ttu-id="39a9e-154">**/API/ETW/Providers (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-154">**/api/etw/providers (GET)**</span></span>

<span data-ttu-id="39a9e-155">Énumère les fournisseurs inscrits</span><span class="sxs-lookup"><span data-stu-id="39a9e-155">Enumerates registered providers</span></span>

<span data-ttu-id="39a9e-156">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-156">Return data</span></span>
* <span data-ttu-id="39a9e-157">Liste des fournisseurs, nom convivial et GUID</span><span class="sxs-lookup"><span data-stu-id="39a9e-157">List of providers, friendly name and GUID</span></span>

<span data-ttu-id="39a9e-158">**/API/ETW/session/Realtime (obtient/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-158">**/api/etw/session/realtime (GET/WebSocket)**</span></span>

<span data-ttu-id="39a9e-159">Crée une session ETW en temps réel; géré sur un WebSocket.</span><span class="sxs-lookup"><span data-stu-id="39a9e-159">Creates a realtime ETW session; managed over a websocket.</span></span>

<span data-ttu-id="39a9e-160">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-160">Return data</span></span>
* <span data-ttu-id="39a9e-161">Événements ETW des fournisseurs activés</span><span class="sxs-lookup"><span data-stu-id="39a9e-161">ETW events from the enabled providers</span></span>

## <a name="holographic-os"></a><span data-ttu-id="39a9e-162">Système d’exploitation holographique</span><span class="sxs-lookup"><span data-stu-id="39a9e-162">Holographic OS</span></span>

<span data-ttu-id="39a9e-163">**/API/Holographic/OS/ETW/customproviders (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-163">**/api/holographic/os/etw/customproviders (GET)**</span></span>

<span data-ttu-id="39a9e-164">Retourne une liste de fournisseurs ETW spécifiques à HoloLens qui ne sont pas inscrits auprès du système.</span><span class="sxs-lookup"><span data-stu-id="39a9e-164">Returns a list of HoloLens specific ETW providers that are not registered with the system</span></span>

<span data-ttu-id="39a9e-165">**/API/Holographic/OS/services (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-165">**/api/holographic/os/services (GET)**</span></span>

<span data-ttu-id="39a9e-166">Retourne les États de tous les services en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="39a9e-166">Returns the states of all services running.</span></span>

<span data-ttu-id="39a9e-167">**/API/Holographic/OS/Settings/IPD (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-167">**/api/holographic/os/settings/ipd (GET)**</span></span>

<span data-ttu-id="39a9e-168">Obtient la IPD stockée (distance interpupillary) en millimètres.</span><span class="sxs-lookup"><span data-stu-id="39a9e-168">Gets the stored IPD (Interpupillary distance) in millimeters</span></span>

<span data-ttu-id="39a9e-169">**/API/Holographic/OS/Settings/IPD (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-169">**/api/holographic/os/settings/ipd (POST)**</span></span>

<span data-ttu-id="39a9e-170">Définit l’IPD</span><span class="sxs-lookup"><span data-stu-id="39a9e-170">Sets the IPD</span></span>

<span data-ttu-id="39a9e-171">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-171">Parameters</span></span>
* <span data-ttu-id="39a9e-172">IPD Nouvelle valeur IPD à définir en millimètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-172">ipd : New IPD value to be set in millimeters</span></span>

<span data-ttu-id="39a9e-173">**/API/Holographic/OS/webmanagement/Settings/HTTPS (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-173">**/api/holographic/os/webmanagement/settings/https (GET)**</span></span>

<span data-ttu-id="39a9e-174">Obtenir la spécification HTTPS pour Device Portal</span><span class="sxs-lookup"><span data-stu-id="39a9e-174">Get HTTPS requirements for the Device Portal</span></span>

<span data-ttu-id="39a9e-175">**/API/Holographic/OS/webmanagement/Settings/HTTPS (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-175">**/api/holographic/os/webmanagement/settings/https (POST)**</span></span>

<span data-ttu-id="39a9e-176">Définit les exigences HTTPs pour le portail de l’appareil</span><span class="sxs-lookup"><span data-stu-id="39a9e-176">Sets HTTPS requirements for the Device Portal</span></span>

<span data-ttu-id="39a9e-177">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-177">Parameters</span></span>
* <span data-ttu-id="39a9e-178">obligatoire: Oui, non ou par défaut</span><span class="sxs-lookup"><span data-stu-id="39a9e-178">required : yes, no or default</span></span>

## <a name="holographic-perception"></a><span data-ttu-id="39a9e-179">Perception holographique</span><span class="sxs-lookup"><span data-stu-id="39a9e-179">Holographic Perception</span></span>

<span data-ttu-id="39a9e-180">**/API/Holographic/perception/client (obtient/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-180">**/api/holographic/perception/client (GET/WebSocket)**</span></span>

<span data-ttu-id="39a9e-181">Accepte les mises à niveau de WebSocket et exécute un client de perception qui envoie des mises à jour à 30 i/s.</span><span class="sxs-lookup"><span data-stu-id="39a9e-181">Accepts websocket upgrades and runs a perception client that sends updates at 30 fps.</span></span>

<span data-ttu-id="39a9e-182">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-182">Parameters</span></span>
* <span data-ttu-id="39a9e-183">Clientmode: "active" force le mode de suivi visuel lorsqu’il ne peut pas être établi passivement</span><span class="sxs-lookup"><span data-stu-id="39a9e-183">clientmode: "active" forces visual tracking mode when it can't be established passively</span></span>

## <a name="holographic-thermal"></a><span data-ttu-id="39a9e-184">Thermique holographique</span><span class="sxs-lookup"><span data-stu-id="39a9e-184">Holographic Thermal</span></span>

<span data-ttu-id="39a9e-185">**/API/Holographic/thermal/stage (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-185">**/api/holographic/thermal/stage (GET)**</span></span>

<span data-ttu-id="39a9e-186">Récupération de l’étape thermique de l’appareil (0 normal, 1 chaud, 2 critique)</span><span class="sxs-lookup"><span data-stu-id="39a9e-186">Get the thermal stage of the device (0 normal, 1 warm, 2 critical)</span></span>

## <a name="perception-simulation-control"></a><span data-ttu-id="39a9e-187">Contrôle de simulation de perception</span><span class="sxs-lookup"><span data-stu-id="39a9e-187">Perception Simulation Control</span></span>

<span data-ttu-id="39a9e-188">**/API/Holographic/simulation/Control/mode (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-188">**/api/holographic/simulation/control/mode (GET)**</span></span>

<span data-ttu-id="39a9e-189">Obtient le mode de simulation</span><span class="sxs-lookup"><span data-stu-id="39a9e-189">Get the simulation mode</span></span>

<span data-ttu-id="39a9e-190">**/API/Holographic/simulation/Control/mode (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-190">**/api/holographic/simulation/control/mode (POST)**</span></span>

<span data-ttu-id="39a9e-191">Définir le mode de simulation</span><span class="sxs-lookup"><span data-stu-id="39a9e-191">Set the simulation mode</span></span>

<span data-ttu-id="39a9e-192">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-192">Parameters</span></span>
* <span data-ttu-id="39a9e-193">mode: mode de simulation: par défaut, simulation, distant, hérité</span><span class="sxs-lookup"><span data-stu-id="39a9e-193">mode : simulation mode: default, simulation, remote, legacy</span></span>

<span data-ttu-id="39a9e-194">**/API/Holographic/simulation/Control/Stream (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-194">**/api/holographic/simulation/control/stream (DELETE)**</span></span>

<span data-ttu-id="39a9e-195">Supprimer un flux de contrôle.</span><span class="sxs-lookup"><span data-stu-id="39a9e-195">Delete a control stream.</span></span>

<span data-ttu-id="39a9e-196">**/API/Holographic/simulation/Control/Stream (obtient/WebSocket)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-196">**/api/holographic/simulation/control/stream (GET/WebSocket)**</span></span>

<span data-ttu-id="39a9e-197">Ouvrez une connexion de socket Web pour un flux de contrôle.</span><span class="sxs-lookup"><span data-stu-id="39a9e-197">Open a web socket connection for a control stream.</span></span>

<span data-ttu-id="39a9e-198">**/API/Holographic/simulation/Control/Stream (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-198">**/api/holographic/simulation/control/stream (POST)**</span></span>

<span data-ttu-id="39a9e-199">Créez un flux de contrôle (priorité obligatoire) ou publiez des données dans un flux créé (streamId requis).</span><span class="sxs-lookup"><span data-stu-id="39a9e-199">Create a control stream (priority is required) or post data to a created stream (streamId required).</span></span> <span data-ttu-id="39a9e-200">Les données publiées sont supposées être de type «application/octet-stream».</span><span class="sxs-lookup"><span data-stu-id="39a9e-200">Posted data is expected to be of type 'application/octet-stream'.</span></span>

## <a name="perception-simulation-playback"></a><span data-ttu-id="39a9e-201">Lecture de simulation de perception</span><span class="sxs-lookup"><span data-stu-id="39a9e-201">Perception Simulation Playback</span></span>

<span data-ttu-id="39a9e-202">**/API/Holographic/simulation/playback/file (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-202">**/api/holographic/simulation/playback/file (DELETE)**</span></span>

<span data-ttu-id="39a9e-203">Supprimer un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-203">Delete a recording.</span></span>

<span data-ttu-id="39a9e-204">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-204">Parameters</span></span>
* <span data-ttu-id="39a9e-205">d' Nom de l’enregistrement à supprimer.</span><span class="sxs-lookup"><span data-stu-id="39a9e-205">recording : Name of recording to delete.</span></span>

<span data-ttu-id="39a9e-206">**/API/Holographic/simulation/playback/file (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-206">**/api/holographic/simulation/playback/file (POST)**</span></span>

<span data-ttu-id="39a9e-207">Télécharger un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-207">Upload a recording.</span></span>

<span data-ttu-id="39a9e-208">**/API/Holographic/simulation/playback/Files (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-208">**/api/holographic/simulation/playback/files (GET)**</span></span>

<span data-ttu-id="39a9e-209">Récupération de tous les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="39a9e-209">Get all recordings.</span></span>

<span data-ttu-id="39a9e-210">**/API/Holographic/simulation/playback/session (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-210">**/api/holographic/simulation/playback/session (GET)**</span></span>

<span data-ttu-id="39a9e-211">Obtient l’état de lecture actuel d’un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-211">Get the current playback state of a recording.</span></span>

<span data-ttu-id="39a9e-212">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-212">Parameters</span></span>
* <span data-ttu-id="39a9e-213">d' Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-213">recording : Name of recording.</span></span>

<span data-ttu-id="39a9e-214">**/API/Holographic/simulation/playback/session/file (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-214">**/api/holographic/simulation/playback/session/file (DELETE)**</span></span>

<span data-ttu-id="39a9e-215">Décharger un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-215">Unload a recording.</span></span>

<span data-ttu-id="39a9e-216">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-216">Parameters</span></span>
* <span data-ttu-id="39a9e-217">d' Nom de l’enregistrement à décharger.</span><span class="sxs-lookup"><span data-stu-id="39a9e-217">recording : Name of recording to unload.</span></span>

<span data-ttu-id="39a9e-218">**/API/Holographic/simulation/playback/session/file (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-218">**/api/holographic/simulation/playback/session/file (POST)**</span></span>

<span data-ttu-id="39a9e-219">Charger un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-219">Load a recording.</span></span>

<span data-ttu-id="39a9e-220">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-220">Parameters</span></span>
* <span data-ttu-id="39a9e-221">d' Nom de l’enregistrement à charger.</span><span class="sxs-lookup"><span data-stu-id="39a9e-221">recording : Name of recording to load.</span></span>

<span data-ttu-id="39a9e-222">**/API/Holographic/simulation/playback/session/Files (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-222">**/api/holographic/simulation/playback/session/files (GET)**</span></span>

<span data-ttu-id="39a9e-223">Récupération de tous les enregistrements chargés.</span><span class="sxs-lookup"><span data-stu-id="39a9e-223">Get all loaded recordings.</span></span>

<span data-ttu-id="39a9e-224">**/API/Holographic/simulation/playback/session/pause (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-224">**/api/holographic/simulation/playback/session/pause (POST)**</span></span>

<span data-ttu-id="39a9e-225">Suspendre un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-225">Pause a recording.</span></span>

<span data-ttu-id="39a9e-226">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-226">Parameters</span></span>
* <span data-ttu-id="39a9e-227">d' Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-227">recording : Name of recording.</span></span>

<span data-ttu-id="39a9e-228">**/API/Holographic/simulation/playback/session/Play (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-228">**/api/holographic/simulation/playback/session/play (POST)**</span></span>

<span data-ttu-id="39a9e-229">Lire un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-229">Play a recording.</span></span>

<span data-ttu-id="39a9e-230">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-230">Parameters</span></span>
* <span data-ttu-id="39a9e-231">d' Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-231">recording : Name of recording.</span></span>

<span data-ttu-id="39a9e-232">**/API/Holographic/simulation/playback/session/Stop (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-232">**/api/holographic/simulation/playback/session/stop (POST)**</span></span>

<span data-ttu-id="39a9e-233">Arrêter un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-233">Stop a recording.</span></span>

<span data-ttu-id="39a9e-234">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-234">Parameters</span></span>
* <span data-ttu-id="39a9e-235">d' Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-235">recording : Name of recording.</span></span>

<span data-ttu-id="39a9e-236">**/API/Holographic/simulation/playback/session/types (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-236">**/api/holographic/simulation/playback/session/types (GET)**</span></span>

<span data-ttu-id="39a9e-237">Obtenir les types de données dans un enregistrement chargé.</span><span class="sxs-lookup"><span data-stu-id="39a9e-237">Get the types of data in a loaded recording.</span></span>

<span data-ttu-id="39a9e-238">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-238">Parameters</span></span>
* <span data-ttu-id="39a9e-239">d' Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-239">recording : Name of recording.</span></span>

## <a name="perception-simulation-recording"></a><span data-ttu-id="39a9e-240">Enregistrement de simulation de perception</span><span class="sxs-lookup"><span data-stu-id="39a9e-240">Perception Simulation Recording</span></span>

<span data-ttu-id="39a9e-241">**/API/Holographic/simulation/Recording/Start (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-241">**/api/holographic/simulation/recording/start (POST)**</span></span>

<span data-ttu-id="39a9e-242">Démarrez un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-242">Start a recording.</span></span> <span data-ttu-id="39a9e-243">Un seul enregistrement peut être actif à la fois.</span><span class="sxs-lookup"><span data-stu-id="39a9e-243">Only a single recording can be active at once.</span></span> <span data-ttu-id="39a9e-244">Vous devez définir l’un des principaux, mains, spatialMapping ou environnement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-244">One of head, hands, spatialMapping or environment must be set.</span></span>

<span data-ttu-id="39a9e-245">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-245">Parameters</span></span>
* <span data-ttu-id="39a9e-246">siège Affectez la valeur 1 pour enregistrer les données de tête.</span><span class="sxs-lookup"><span data-stu-id="39a9e-246">head : Set to 1 to record head data.</span></span>
* <span data-ttu-id="39a9e-247">leçon Définissez la valeur 1 pour enregistrer les données de la main.</span><span class="sxs-lookup"><span data-stu-id="39a9e-247">hands : Set to 1 to record hand data.</span></span>
* <span data-ttu-id="39a9e-248">spatialMapping : Affectez la valeur 1 pour enregistrer le mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="39a9e-248">spatialMapping : Set to 1 to record spatial mapping.</span></span>
* <span data-ttu-id="39a9e-249">environnement Affectez la valeur 1 pour enregistrer les données d’environnement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-249">environment : Set to 1 to record environment data.</span></span>
* <span data-ttu-id="39a9e-250">nomme Nom de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-250">name : Name of the recording.</span></span>
* <span data-ttu-id="39a9e-251">singleSpatialMappingFrame : Affectez la valeur 1 pour enregistrer uniquement un seul frame de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="39a9e-251">singleSpatialMappingFrame : Set to 1 to record only a single spatial mapping frame.</span></span>

<span data-ttu-id="39a9e-252">**/API/Holographic/simulation/Recording/Status (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-252">**/api/holographic/simulation/recording/status (GET)**</span></span>

<span data-ttu-id="39a9e-253">Obtient l’état de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="39a9e-253">Get recording state.</span></span>

<span data-ttu-id="39a9e-254">**/API/Holographic/simulation/Recording/Stop (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-254">**/api/holographic/simulation/recording/stop (GET)**</span></span>

<span data-ttu-id="39a9e-255">Arrêter l’enregistrement en cours.</span><span class="sxs-lookup"><span data-stu-id="39a9e-255">Stop the current recording.</span></span> <span data-ttu-id="39a9e-256">L’enregistrement est retourné sous la forme d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="39a9e-256">Recording will be returned as a file.</span></span>

## <a name="mixed-reality-capture"></a><span data-ttu-id="39a9e-257">MRC (Mixed Reality Capture)</span><span class="sxs-lookup"><span data-stu-id="39a9e-257">Mixed Reality Capture</span></span>

<span data-ttu-id="39a9e-258">**/API/Holographic/MRC/file (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-258">**/api/holographic/mrc/file (GET)**</span></span>

<span data-ttu-id="39a9e-259">Télécharge un fichier de réalité mixte à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="39a9e-259">Downloads a mixed reality file from the device.</span></span> <span data-ttu-id="39a9e-260">Utilisez le paramètre de requête op = Stream pour la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="39a9e-260">Use op=stream query parameter for streaming.</span></span>

<span data-ttu-id="39a9e-261">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-261">Parameters</span></span>
* <span data-ttu-id="39a9e-262">extension Nom, hex64 encodé, du fichier vidéo à récupérer</span><span class="sxs-lookup"><span data-stu-id="39a9e-262">filename : Name, hex64 encoded, of the video file to get</span></span>
* <span data-ttu-id="39a9e-263">OP: flux</span><span class="sxs-lookup"><span data-stu-id="39a9e-263">op : stream</span></span>

<span data-ttu-id="39a9e-264">**/API/Holographic/MRC/file (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-264">**/api/holographic/mrc/file (DELETE)**</span></span>

<span data-ttu-id="39a9e-265">Supprime un enregistrement de la réalité mixte de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="39a9e-265">Deletes a mixed reality recording from the device.</span></span>

<span data-ttu-id="39a9e-266">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-266">Parameters</span></span>
* <span data-ttu-id="39a9e-267">extension Nom, hex64 encodé, du fichier à supprimer</span><span class="sxs-lookup"><span data-stu-id="39a9e-267">filename : Name, hex64 encoded, of the file to delete</span></span>

<span data-ttu-id="39a9e-268">**/API/Holographic/MRC/Files (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-268">**/api/holographic/mrc/files (GET)**</span></span>

<span data-ttu-id="39a9e-269">Retourne la liste des fichiers de réalité mixte stockés sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="39a9e-269">Returns the list of mixed reality files stored on the device</span></span>

<span data-ttu-id="39a9e-270">**/API/Holographic/MRC/photo (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-270">**/api/holographic/mrc/photo (POST)**</span></span>

<span data-ttu-id="39a9e-271">Prend une photo de réalité mixte et crée un fichier sur l’appareil</span><span class="sxs-lookup"><span data-stu-id="39a9e-271">Takes a mixed reality photo and creates a file on the device</span></span>

<span data-ttu-id="39a9e-272">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-272">Parameters</span></span>
* <span data-ttu-id="39a9e-273">Holo: capturer les hologrammes: true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-273">holo : capture holograms: true or false (defaults to false)</span></span>
* <span data-ttu-id="39a9e-274">PV: capturer l’appareil photo PV: true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-274">pv : capture PV camera: true or false (defaults to false)</span></span>
* <span data-ttu-id="39a9e-275">RenderFromCamera : (HoloLens 2 uniquement) rendu du point de vue de la caméra photo/vidéo: true ou false (true par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-275">RenderFromCamera : (HoloLens 2 only) render from perspective of photo/video camera: true or false (defaults to true)</span></span>

<span data-ttu-id="39a9e-276">**/API/Holographic/MRC/Settings (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-276">**/api/holographic/mrc/settings (GET)**</span></span>

<span data-ttu-id="39a9e-277">Obtient les paramètres de capture de la réalité mixte par défaut</span><span class="sxs-lookup"><span data-stu-id="39a9e-277">Gets the default mixed reality capture settings</span></span>

<span data-ttu-id="39a9e-278">**/API/Holographic/MRC/Settings (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-278">**/api/holographic/mrc/settings (POST)**</span></span>

<span data-ttu-id="39a9e-279">Définit les paramètres de capture de la réalité mixte par défaut.</span><span class="sxs-lookup"><span data-stu-id="39a9e-279">Sets the default mixed reality capture settings.</span></span>  <span data-ttu-id="39a9e-280">Certains de ces paramètres sont appliqués à la photo et à la capture de vidéo MRC du système.</span><span class="sxs-lookup"><span data-stu-id="39a9e-280">Some of these settings are applied to the system's MRC photo and video capture.</span></span>

<span data-ttu-id="39a9e-281">**/API/Holographic/MRC/Status (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-281">**/api/holographic/mrc/status (GET)**</span></span>

<span data-ttu-id="39a9e-282">Obtient l’état de la réalité mixte enregistrée (en cours d’exécution, arrêtée).</span><span class="sxs-lookup"><span data-stu-id="39a9e-282">Gets the status of the mixed reality recorded (running, stopped)</span></span>

<span data-ttu-id="39a9e-283">**/API/Holographic/MRC/thumbnail (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-283">**/api/holographic/mrc/thumbnail (GET)**</span></span>

<span data-ttu-id="39a9e-284">Obtient l’image miniature pour le fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="39a9e-284">Gets the thumbnail image for the specified file.</span></span>

<span data-ttu-id="39a9e-285">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-285">Parameters</span></span>
* <span data-ttu-id="39a9e-286">extension Nom, hex64 encodé, du fichier pour lequel la miniature est demandée</span><span class="sxs-lookup"><span data-stu-id="39a9e-286">filename: Name, hex64 encoded, of the file for which the thumbnail is being requested</span></span>

<span data-ttu-id="39a9e-287">**/API/Holographic/MRC/Video/Control/Start (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-287">**/api/holographic/mrc/video/control/start (POST)**</span></span>

<span data-ttu-id="39a9e-288">Démarre un enregistrement de la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="39a9e-288">Starts a mixed reality recording</span></span>

<span data-ttu-id="39a9e-289">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-289">Parameters</span></span>
* <span data-ttu-id="39a9e-290">Holo: capturer les hologrammes: true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-290">holo : capture holograms: true or false (defaults to false)</span></span>
* <span data-ttu-id="39a9e-291">PV: capturer l’appareil photo PV: true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-291">pv : capture PV camera: true or false (defaults to false)</span></span>
* <span data-ttu-id="39a9e-292">MIC: capturer le microphone: true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-292">mic : capture microphone: true or false (defaults to false)</span></span>
* <span data-ttu-id="39a9e-293">loopback: capturer l’audio de l’application: true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-293">loopback : capture app audio: true or false (defaults to false)</span></span>
* <span data-ttu-id="39a9e-294">RenderFromCamera : (HoloLens 2 uniquement) rendu du point de vue de la caméra photo/vidéo: true ou false (true par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-294">RenderFromCamera : (HoloLens 2 only) render from perspective of photo/video camera: true or false (defaults to true)</span></span>
* <span data-ttu-id="39a9e-295">vstab : (HoloLens 2 uniquement) activer la stabilisation vidéo: true ou false (true par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-295">vstab : (HoloLens 2 only) enable video stabilization: true or false (defaults to true)</span></span>
* <span data-ttu-id="39a9e-296">vstabbuffer: (HoloLens 2 uniquement) latence de la mémoire tampon de stabilisation vidéo: 0 à 30 frames (15 images par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-296">vstabbuffer: (HoloLens 2 only) video stabilization buffer latency: 0 to 30 frames (defaults to 15 frames)</span></span>

<span data-ttu-id="39a9e-297">**/API/Holographic/MRC/Video/Control/Stop (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-297">**/api/holographic/mrc/video/control/stop (POST)**</span></span>

<span data-ttu-id="39a9e-298">Arrête l’enregistrement de la réalité mixte actuelle</span><span class="sxs-lookup"><span data-stu-id="39a9e-298">Stops the current mixed reality recording</span></span>

## <a name="mixed-reality-streaming"></a><span data-ttu-id="39a9e-299">Diffusion en continu de la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="39a9e-299">Mixed Reality Streaming</span></span>

<span data-ttu-id="39a9e-300">HoloLens prend en charge l’aperçu instantané de la réalité mixte via le téléchargement segmenté d’un MP4 fragmenté.</span><span class="sxs-lookup"><span data-stu-id="39a9e-300">HoloLens supports live preview of mixed reality via chunked download of a fragmented mp4.</span></span>

<span data-ttu-id="39a9e-301">Les flux de réalité mixte partagent le même ensemble de paramètres pour contrôler ce qui est capturé:</span><span class="sxs-lookup"><span data-stu-id="39a9e-301">Mixed reality streams share the same set of parameters to control what is captured:</span></span>
* <span data-ttu-id="39a9e-302">Holo: capturer les hologrammes: true ou false</span><span class="sxs-lookup"><span data-stu-id="39a9e-302">holo : capture holograms: true or false</span></span>
* <span data-ttu-id="39a9e-303">PV: capturer l’appareil photo PV: true ou false</span><span class="sxs-lookup"><span data-stu-id="39a9e-303">pv : capture PV camera: true or false</span></span>
* <span data-ttu-id="39a9e-304">MIC: capturer le microphone: true ou false</span><span class="sxs-lookup"><span data-stu-id="39a9e-304">mic : capture microphone: true or false</span></span>
* <span data-ttu-id="39a9e-305">loopback: capturer l’audio de l’application: true ou false</span><span class="sxs-lookup"><span data-stu-id="39a9e-305">loopback : capture app audio: true or false</span></span>

<span data-ttu-id="39a9e-306">Si aucun de ces éléments n’est spécifié: les hologrammes, la caméra photo/vidéo et l’audio de l’application sont capturés</span><span class="sxs-lookup"><span data-stu-id="39a9e-306">If none of these are specified: holograms, photo/video camera, and app audio will be captured</span></span><br>
<span data-ttu-id="39a9e-307">Si des paramètres sont spécifiés: les paramètres non spécifiés ont par défaut la valeur false</span><span class="sxs-lookup"><span data-stu-id="39a9e-307">If any are specified: the unspecified parameters will default to false</span></span>

<span data-ttu-id="39a9e-308">Paramètres facultatifs (HoloLens 2 uniquement)</span><span class="sxs-lookup"><span data-stu-id="39a9e-308">Optional parameters (HoloLens 2 only)</span></span>
* <span data-ttu-id="39a9e-309">RenderFromCamera: rendu du point de vue de la caméra photo/vidéo: true ou false (true par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-309">RenderFromCamera : render from perspective of photo/video camera: true or false (defaults to true)</span></span>
* <span data-ttu-id="39a9e-310">Vstab: activer la stabilisation vidéo: true ou false (false par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-310">vstab : enable video stabilization: true or false (defaults to false)</span></span>
* <span data-ttu-id="39a9e-311">vstabbuffer: latence de la mémoire tampon de stabilisation vidéo: 0 à 30 frames (15 images par défaut)</span><span class="sxs-lookup"><span data-stu-id="39a9e-311">vstabbuffer: video stabilization buffer latency: 0 to 30 frames (defaults to 15 frames)</span></span>

<span data-ttu-id="39a9e-312">**/API/Holographic/Stream/Live.MP4 (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-312">**/api/holographic/stream/live.mp4 (GET)**</span></span>

<span data-ttu-id="39a9e-313">Un flux 1280x720p 30fps 5Mbit.</span><span class="sxs-lookup"><span data-stu-id="39a9e-313">A 1280x720p 30fps 5Mbit stream.</span></span>

<span data-ttu-id="39a9e-314">**/API/Holographic/Stream/live_high.MP4 (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-314">**/api/holographic/stream/live_high.mp4 (GET)**</span></span>

<span data-ttu-id="39a9e-315">Un flux 1280x720p 30fps 5Mbit.</span><span class="sxs-lookup"><span data-stu-id="39a9e-315">A 1280x720p 30fps 5Mbit stream.</span></span>

<span data-ttu-id="39a9e-316">**/API/Holographic/Stream/live_med.MP4 (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-316">**/api/holographic/stream/live_med.mp4 (GET)**</span></span>

<span data-ttu-id="39a9e-317">Flux 854x480p 30fps 2,5 Mbits.</span><span class="sxs-lookup"><span data-stu-id="39a9e-317">A 854x480p 30fps 2.5Mbit stream.</span></span>

<span data-ttu-id="39a9e-318">**/API/Holographic/Stream/live_low.MP4 (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-318">**/api/holographic/stream/live_low.mp4 (GET)**</span></span>

<span data-ttu-id="39a9e-319">Flux 428x240p 15fps 0,6 Mbit.</span><span class="sxs-lookup"><span data-stu-id="39a9e-319">A 428x240p 15fps 0.6Mbit stream.</span></span>

## <a name="networking"></a><span data-ttu-id="39a9e-320">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="39a9e-320">Networking</span></span>

<span data-ttu-id="39a9e-321">**/API/Networking/ipconfig (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-321">**/api/networking/ipconfig (GET)**</span></span>

<span data-ttu-id="39a9e-322">Obtient la configuration IP actuelle</span><span class="sxs-lookup"><span data-stu-id="39a9e-322">Gets the current ip configuration</span></span>

## <a name="os-information"></a><span data-ttu-id="39a9e-323">Informations sur le système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="39a9e-323">OS Information</span></span>

<span data-ttu-id="39a9e-324">**/API/OS/info (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-324">**/api/os/info (GET)**</span></span>

<span data-ttu-id="39a9e-325">Obtient des informations sur le système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="39a9e-325">Gets operating system information</span></span>

<span data-ttu-id="39a9e-326">**/API/OS/MachineName (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-326">**/api/os/machinename (GET)**</span></span>

<span data-ttu-id="39a9e-327">Obtient le nom de l’ordinateur</span><span class="sxs-lookup"><span data-stu-id="39a9e-327">Gets the machine name</span></span>

<span data-ttu-id="39a9e-328">**/API/OS/MachineName (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-328">**/api/os/machinename (POST)**</span></span>

<span data-ttu-id="39a9e-329">Définit le nom de l’ordinateur</span><span class="sxs-lookup"><span data-stu-id="39a9e-329">Sets the machine name</span></span>

<span data-ttu-id="39a9e-330">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-330">Parameters</span></span>
* <span data-ttu-id="39a9e-331">nomme Nouveau nom de l’ordinateur, hex64 encodé, à définir sur</span><span class="sxs-lookup"><span data-stu-id="39a9e-331">name : New machine name, hex64 encoded, to set to</span></span>

## <a name="performance-data"></a><span data-ttu-id="39a9e-332">Données relatives aux performances</span><span class="sxs-lookup"><span data-stu-id="39a9e-332">Performance data</span></span>

<span data-ttu-id="39a9e-333">**/API/ResourceManager/Processes (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-333">**/api/resourcemanager/processes (GET)**</span></span>

<span data-ttu-id="39a9e-334">Retourne la liste des processus en cours d’exécution avec les détails</span><span class="sxs-lookup"><span data-stu-id="39a9e-334">Returns the list of running processes with details</span></span>

<span data-ttu-id="39a9e-335">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-335">Return data</span></span>
* <span data-ttu-id="39a9e-336">JSON avec liste de processus et détails pour chaque processus</span><span class="sxs-lookup"><span data-stu-id="39a9e-336">JSON with list of processes and details for each process</span></span>

<span data-ttu-id="39a9e-337">**/API/ResourceManager/systemperf (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-337">**/api/resourcemanager/systemperf (GET)**</span></span>

<span data-ttu-id="39a9e-338">Retourne les statistiques de performances système (lecture/écriture d’e/s, statistiques de mémoire, etc.).</span><span class="sxs-lookup"><span data-stu-id="39a9e-338">Returns system perf statistics (I/O read/write, memory stats etc.</span></span>

<span data-ttu-id="39a9e-339">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-339">Return data</span></span>
* <span data-ttu-id="39a9e-340">JSON avec informations système: PROCESSEUR, GPU, mémoire, réseau, e/s</span><span class="sxs-lookup"><span data-stu-id="39a9e-340">JSON with system information: CPU, GPU, Memory, Network, IO</span></span>

## <a name="power"></a><span data-ttu-id="39a9e-341">Alimentation</span><span class="sxs-lookup"><span data-stu-id="39a9e-341">Power</span></span>

<span data-ttu-id="39a9e-342">**/API/Power/Battery (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-342">**/api/power/battery (GET)**</span></span>

<span data-ttu-id="39a9e-343">Obtient l’état actuel de la batterie</span><span class="sxs-lookup"><span data-stu-id="39a9e-343">Gets the current battery state</span></span>

<span data-ttu-id="39a9e-344">**/API/Power/State (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-344">**/api/power/state (GET)**</span></span>

<span data-ttu-id="39a9e-345">Vérifie si le système est dans un état de faible consommation d’énergie.</span><span class="sxs-lookup"><span data-stu-id="39a9e-345">Checks if the system is in a low power state</span></span>

## <a name="remote-control"></a><span data-ttu-id="39a9e-346">Contrôle à distance</span><span class="sxs-lookup"><span data-stu-id="39a9e-346">Remote Control</span></span>

<span data-ttu-id="39a9e-347">**/API/Control/Restart (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-347">**/api/control/restart (POST)**</span></span>

<span data-ttu-id="39a9e-348">Redémarre l’appareil cible</span><span class="sxs-lookup"><span data-stu-id="39a9e-348">Restarts the target device</span></span>

<span data-ttu-id="39a9e-349">**/API/Control/Shutdown (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-349">**/api/control/shutdown (POST)**</span></span>

<span data-ttu-id="39a9e-350">Arrête l’appareil cible</span><span class="sxs-lookup"><span data-stu-id="39a9e-350">Shuts down the target device</span></span>

## <a name="task-manager"></a><span data-ttu-id="39a9e-351">Gestionnaire des tâches</span><span class="sxs-lookup"><span data-stu-id="39a9e-351">Task Manager</span></span>

<span data-ttu-id="39a9e-352">**/API/taskmanager/App (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-352">**/api/taskmanager/app (DELETE)**</span></span>

<span data-ttu-id="39a9e-353">Arrête une application moderne</span><span class="sxs-lookup"><span data-stu-id="39a9e-353">Stops a modern app</span></span>

<span data-ttu-id="39a9e-354">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-354">Parameters</span></span>
* <span data-ttu-id="39a9e-355">Packages Nom complet du package d’application, hex64 encodé</span><span class="sxs-lookup"><span data-stu-id="39a9e-355">package : Full name of the app package, hex64 encoded</span></span>
* <span data-ttu-id="39a9e-356">forcestop : Forcer l’arrêt de tous les processus (= oui)</span><span class="sxs-lookup"><span data-stu-id="39a9e-356">forcestop : Force all processes to stop (=yes)</span></span>

<span data-ttu-id="39a9e-357">**/API/taskmanager/App (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-357">**/api/taskmanager/app (POST)**</span></span>

<span data-ttu-id="39a9e-358">Démarre une application moderne</span><span class="sxs-lookup"><span data-stu-id="39a9e-358">Starts a modern app</span></span>

<span data-ttu-id="39a9e-359">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-359">Parameters</span></span>
* <span data-ttu-id="39a9e-360">AppID PRAID de l’application à démarrer, encodée hex64</span><span class="sxs-lookup"><span data-stu-id="39a9e-360">appid : PRAID of app to start, hex64 encoded</span></span>
* <span data-ttu-id="39a9e-361">Packages Nom complet du package d’application, hex64 encodé</span><span class="sxs-lookup"><span data-stu-id="39a9e-361">package : Full name of the app package, hex64 encoded</span></span>

## <a name="wifi-management"></a><span data-ttu-id="39a9e-362">Gestion WiFi</span><span class="sxs-lookup"><span data-stu-id="39a9e-362">WiFi Management</span></span>

<span data-ttu-id="39a9e-363">**/API/WiFi/interfaces (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-363">**/api/wifi/interfaces (GET)**</span></span>

<span data-ttu-id="39a9e-364">Énumère les interfaces de réseau sans fil</span><span class="sxs-lookup"><span data-stu-id="39a9e-364">Enumerates wireless network interfaces</span></span>

<span data-ttu-id="39a9e-365">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-365">Return data</span></span>
* <span data-ttu-id="39a9e-366">Liste des interfaces sans fil avec des détails (GUID, description, etc.)</span><span class="sxs-lookup"><span data-stu-id="39a9e-366">List of wireless interfaces with details (GUID, description etc.)</span></span>

<span data-ttu-id="39a9e-367">**/API/WiFi/Network (supprimer)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-367">**/api/wifi/network (DELETE)**</span></span>

<span data-ttu-id="39a9e-368">Supprime un profil associé à un réseau sur une interface spécifiée</span><span class="sxs-lookup"><span data-stu-id="39a9e-368">Deletes a profile associated with a network on a specified interface</span></span>

<span data-ttu-id="39a9e-369">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-369">Parameters</span></span>
* <span data-ttu-id="39a9e-370">Interface: GUID de l’interface réseau</span><span class="sxs-lookup"><span data-stu-id="39a9e-370">interface : network interface guid</span></span>
* <span data-ttu-id="39a9e-371">Profil: nom du profil</span><span class="sxs-lookup"><span data-stu-id="39a9e-371">profile : profile name</span></span>

<span data-ttu-id="39a9e-372">**/API/WiFi/Networks (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-372">**/api/wifi/networks (GET)**</span></span>

<span data-ttu-id="39a9e-373">Énumère les réseaux sans fil sur l’interface réseau spécifiée.</span><span class="sxs-lookup"><span data-stu-id="39a9e-373">Enumerates wireless networks on the specified network interface</span></span>

<span data-ttu-id="39a9e-374">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-374">Parameters</span></span>
* <span data-ttu-id="39a9e-375">Interface: GUID de l’interface réseau</span><span class="sxs-lookup"><span data-stu-id="39a9e-375">interface : network interface guid</span></span>

<span data-ttu-id="39a9e-376">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-376">Return data</span></span>
* <span data-ttu-id="39a9e-377">Liste des réseaux sans fil détectés sur l’interface réseau avec les détails</span><span class="sxs-lookup"><span data-stu-id="39a9e-377">List of wireless networks found on the network interface with details</span></span>

<span data-ttu-id="39a9e-378">**/API/WiFi/Network (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-378">**/api/wifi/network (POST)**</span></span>

<span data-ttu-id="39a9e-379">Se connecte ou se déconnecte à un réseau sur l’interface spécifiée</span><span class="sxs-lookup"><span data-stu-id="39a9e-379">Connects or disconnects to a network on the specified interface</span></span>

<span data-ttu-id="39a9e-380">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-380">Parameters</span></span>
* <span data-ttu-id="39a9e-381">Interface: GUID de l’interface réseau</span><span class="sxs-lookup"><span data-stu-id="39a9e-381">interface : network interface guid</span></span>
* <span data-ttu-id="39a9e-382">SSID: SSID, hex64 encodé, pour se connecter à</span><span class="sxs-lookup"><span data-stu-id="39a9e-382">ssid : ssid, hex64 encoded, to connect to</span></span>
* <span data-ttu-id="39a9e-383">opération: se connecter ou se déconnecter</span><span class="sxs-lookup"><span data-stu-id="39a9e-383">op : connect or disconnect</span></span>
* <span data-ttu-id="39a9e-384">CreateProfile: oui ou non</span><span class="sxs-lookup"><span data-stu-id="39a9e-384">createprofile : yes or no</span></span>
* <span data-ttu-id="39a9e-385">clé: clé partagée, encodée en hex64</span><span class="sxs-lookup"><span data-stu-id="39a9e-385">key : shared key, hex64 encoded</span></span>

## <a name="windows-performance-recorder"></a><span data-ttu-id="39a9e-386">Enregistreur de performances Windows</span><span class="sxs-lookup"><span data-stu-id="39a9e-386">Windows Performance Recorder</span></span>

<span data-ttu-id="39a9e-387">**/API/WPR/customtrace (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-387">**/api/wpr/customtrace (POST)**</span></span>

<span data-ttu-id="39a9e-388">Charge un profil WPR et démarre le suivi à l’aide du profil chargé.</span><span class="sxs-lookup"><span data-stu-id="39a9e-388">Uploads a WPR profile and starts tracing using the uploaded profile.</span></span>

<span data-ttu-id="39a9e-389">Transport</span><span class="sxs-lookup"><span data-stu-id="39a9e-389">Payload</span></span>
* <span data-ttu-id="39a9e-390">corps http en plusieurs parties, conforme</span><span class="sxs-lookup"><span data-stu-id="39a9e-390">multi-part conforming http body</span></span>

<span data-ttu-id="39a9e-391">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-391">Return data</span></span>
* <span data-ttu-id="39a9e-392">Retourne l’état de la session WPR.</span><span class="sxs-lookup"><span data-stu-id="39a9e-392">Returns the WPR session status.</span></span>

<span data-ttu-id="39a9e-393">**/API/WPR/Status (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-393">**/api/wpr/status (GET)**</span></span>

<span data-ttu-id="39a9e-394">Récupère l’état de la session WPR</span><span class="sxs-lookup"><span data-stu-id="39a9e-394">Retrieves the status of the WPR session</span></span>

<span data-ttu-id="39a9e-395">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-395">Return data</span></span>
* <span data-ttu-id="39a9e-396">État de session WPR.</span><span class="sxs-lookup"><span data-stu-id="39a9e-396">WPR session status.</span></span>

<span data-ttu-id="39a9e-397">**/API/WPR/trace (récupération)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-397">**/api/wpr/trace (GET)**</span></span>

<span data-ttu-id="39a9e-398">Arrête une session de suivi WPR (performance)</span><span class="sxs-lookup"><span data-stu-id="39a9e-398">Stops a WPR (performance) tracing session</span></span>

<span data-ttu-id="39a9e-399">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-399">Return data</span></span>
* <span data-ttu-id="39a9e-400">Retourne le fichier ETL de trace</span><span class="sxs-lookup"><span data-stu-id="39a9e-400">Returns the trace ETL file</span></span>

<span data-ttu-id="39a9e-401">**/API/WPR/trace (publication)**</span><span class="sxs-lookup"><span data-stu-id="39a9e-401">**/api/wpr/trace (POST)**</span></span>

<span data-ttu-id="39a9e-402">Démarre une session de suivi WPR (performance)</span><span class="sxs-lookup"><span data-stu-id="39a9e-402">Starts a WPR (performance) tracing sessions</span></span>

<span data-ttu-id="39a9e-403">Paramètres</span><span class="sxs-lookup"><span data-stu-id="39a9e-403">Parameters</span></span>
* <span data-ttu-id="39a9e-404">Profil Nom du profil.</span><span class="sxs-lookup"><span data-stu-id="39a9e-404">profile : Profile name.</span></span> <span data-ttu-id="39a9e-405">Les profils disponibles sont stockés dans perfprofiles/profiles. JSON</span><span class="sxs-lookup"><span data-stu-id="39a9e-405">Available profiles are stored in perfprofiles/profiles.json</span></span>

<span data-ttu-id="39a9e-406">Retourner les données</span><span class="sxs-lookup"><span data-stu-id="39a9e-406">Return data</span></span>
* <span data-ttu-id="39a9e-407">Dans Démarrer, retourne l’état de la session WPR.</span><span class="sxs-lookup"><span data-stu-id="39a9e-407">On start, returns the WPR session status.</span></span>

## <a name="see-also"></a><span data-ttu-id="39a9e-408">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="39a9e-408">See also</span></span>
* [<span data-ttu-id="39a9e-409">Utilisation du portail d’appareil Windows</span><span class="sxs-lookup"><span data-stu-id="39a9e-409">Using the Windows Device Portal</span></span>](using-the-windows-device-portal.md)
* [<span data-ttu-id="39a9e-410">Informations de référence sur l’API principale du portail des appareils (UWP)</span><span class="sxs-lookup"><span data-stu-id="39a9e-410">Device Portal core API reference (UWP)</span></span>](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-api-core)
