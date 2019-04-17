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
# <a name="device-portal-api-reference"></a>Portail de référence de l’API des appareils

Tous les éléments de la [Windows Device Portal](using-the-windows-device-portal.md) se trouve au sommet de l’API REST que vous pouvez utiliser pour accéder aux données et de contrôler par programmation de votre appareil.

## <a name="app-deloyment"></a>Application deloyment

**/API/App/PackageManager/package (DELETE)**

Désinstalle une application

Paramètres
* package : Nom de fichier du package doit être désinstallé.

**/API/App/PackageManager/package (POST)**

Installe une application

Paramètres
* package : Nom de fichier du package doit être installé.

charge utile
* corps http conforme à plusieurs parties

**/API/App/PackageManager/packages (GET)**

Récupère la liste des applications installées sur le système, avec les détails

Retourner des données
* Liste des packages installés avec les détails

**/API/App/PackageManager/State (GET)**

Obtient l’état de dans l’installation de l’application progression

## <a name="dump-collection"></a>Collection de vidages

**/API/Debug/dump/UserMode/CrashControl (DELETE)**

Désactive crash collecte des vidages pour une application chargée indépendamment

Paramètres
* packageFullname : nom du package

**/API/Debug/dump/UserMode/CrashControl (GET)**

Obtient les paramètres pour les applications de chargement de version test collecte des vidages sur incident

Paramètres
* packageFullname : nom du package

**/api/debug/dump/usermode/crashcontrol (POST)**

Active et configure les paramètres de contrôle d’image pour une application chargée indépendamment

Paramètres
* packageFullname : nom du package

**/API/Debug/dump/UserMode/crashdump (DELETE)**

Supprime un vidage sur incident pour une application chargée indépendamment

Paramètres
* packageFullname : nom du package
* nom de fichier : nom de fichier de vidage

**/API/Debug/dump/UserMode/crashdump (GET)**

Récupère un vidage sur incident pour une application chargée indépendamment

Paramètres
* packageFullname : nom du package
* nom de fichier : nom de fichier de vidage

Retourner des données
* Fichier de vidage. Inspecter avec WinDbg ou Visual Studio

**/API/Debug/dump/UserMode/dumps (GET)**

Retourne la liste de tous les vidages sur incident pour les versions test d’applications

Retourner des données
* Liste de blocage vidages par l’application chargée côté

## <a name="etw"></a>ETW

**/api/etw/providers (GET)**

Énumère les fournisseurs inscrits

Retourner des données
* Liste des fournisseurs, nom convivial et GUID

**/API/ETW/session/Realtime (GET/WebSocket)**

Crée une session ETW en temps réel. gérés via un websocket.

Retourner des données
* Événements ETW à partir de fournisseurs activés

## <a name="holographic-os"></a>Système d’exploitation holographique

**/API/Holographic/OS/ETW/customproviders (GET)**

Retourne une liste des fournisseurs ETW spécifiques HoloLens qui ne sont pas inscrits avec le système

**/API/Holographic/OS/Services (GET)**

Retourne les États de tous les services en cours d’exécution.

**/API/Holographic/OS/Settings/IPD (GET)**

Obtient l’IPD stockée (distance Interpupillary) en millimètres

**/API/Holographic/OS/Settings/IPD (POST)**

Définit l’IPD

Paramètres
* IPD : Nouvelle valeur IPD à être définies en millimètres

**/api/holographic/os/webmanagement/settings/https (GET)**

Obtenir la spécification HTTPS pour Device Portal

**/api/holographic/os/webmanagement/settings/https (POST)**

Définit les conditions requises de HTTPS pour le portail de l’appareil

Paramètres
* requis : Oui, non ou par défaut

## <a name="holographic-perception"></a>Perception HOLOGRAPHIQUE

**/API/Holographic/perception/client (GET/WebSocket)**

Accepte les mises à niveau websocket et exécute un client de perception qui envoie des mises à jour à 30 i/s.

Paramètres
* clientmode : « actif » force le mode de suivi visuel quand il ne peut pas être établie passivement

## <a name="holographic-thermal"></a>Thermique HOLOGRAPHIQUE

**/API/Holographic/Thermal/Stage (GET)**

Obtenir de l’étape thermique de l’appareil (normal 0, 1 à chaud, 2 critique)

## <a name="perception-simulation-control"></a>Contrôle de Simulation de perception

**/API/Holographic/simulation/Control/mode (GET)**

Obtenir le mode de simulation

**/API/Holographic/simulation/Control/mode (POST)**

Définir le mode de simulation

Paramètres
* mode : mode de simulation : par défaut, simulation, à distance, hérité

**/API/Holographic/simulation/Control/Stream (DELETE)**

Supprimer un flux de contrôle.

**/API/Holographic/simulation/Control/Stream (GET/WebSocket)**

Ouvrir une connexion de socket web pour un flux de contrôle.

**/API/Holographic/simulation/Control/Stream (POST)**

Créer un flux de contrôle (la priorité est requise) ou publier des données sur un flux créé (streamId requis). Les données publiées sont censées être de type « application/octet-stream ».

## <a name="perception-simulation-playback"></a>Lecture de Simulation de perception

**/API/Holographic/simulation/Playback/File (DELETE)**

Supprimer un enregistrement.

Paramètres
* enregistrement : Nom de l’enregistrement pour la supprimer.

**/API/Holographic/simulation/Playback/File (POST)**

Téléchargez un enregistrement.

**/API/Holographic/simulation/Playback/Files (GET)**

Obtenir tous les enregistrements.

**/API/Holographic/simulation/Playback/session (GET)**

Obtenir l’état actuel de la lecture de l’enregistrement.

Paramètres
* enregistrement : Nom de l’enregistrement.

**/API/Holographic/simulation/Playback/session/file (DELETE)**

Décharger un enregistrement.

Paramètres
* enregistrement : Nom de l’enregistrement pour décharger.

**/API/Holographic/simulation/Playback/session/file (POST)**

Charger un enregistrement.

Paramètres
* enregistrement : Nom de l’enregistrement pour la charge.

**/API/Holographic/simulation/Playback/session/files (GET)**

Obtenir des enregistrements tous chargés.

**/API/Holographic/simulation/Playback/session/pause (POST)**

Suspendre un enregistrement.

Paramètres
* enregistrement : Nom de l’enregistrement.

**/API/Holographic/simulation/Playback/session/Play (POST)**

Lire un enregistrement.

Paramètres
* enregistrement : Nom de l’enregistrement.

**/API/Holographic/simulation/Playback/session/Stop (POST)**

Arrêter un enregistrement.

Paramètres
* enregistrement : Nom de l’enregistrement.

**/API/Holographic/simulation/Playback/session/types (GET)**

Obtenir les types de données dans un enregistrement chargé.

Paramètres
* enregistrement : Nom de l’enregistrement.

## <a name="perception-simulation-recording"></a>Enregistrement de Simulation de perception

**/API/Holographic/simulation/Recording/Start (POST)**

Démarrer un enregistrement. Un enregistrement unique peut être actif à la fois. Head, mains, spatialMapping ou environnement doit être définie.

Paramètres
* head : Définissez sur 1 pour les données de l’enregistrement principal.
* mains : La valeur 1 pour enregistrer les données manuellement.
* spatialMapping : La valeur 1 pour enregistrer le mappage spatial.
* environnement : La valeur 1 pour enregistrer les données de l’environnement.
* nom : Nom de l’enregistrement.
* singleSpatialMappingFrame : La valeur 1 pour enregistrer uniquement une trame de mappage spatial unique.

**/API/Holographic/simulation/Recording/Status (GET)**

Obtenir enregistrement d’état.

**/API/Holographic/simulation/Recording/Stop (GET)**

Arrêter l’enregistrement actuel. L’enregistrement s’affichera sous forme de fichier.

## <a name="mixed-reality-capture"></a>MRC (Mixed Reality Capture)

**/API/Holographic/MRC/file (DELETE)**

Supprime une réalité mixte enregistrant à partir de l’appareil.

Paramètres
* nom de fichier : Nom, hex64 encodée du fichier à supprimer

**/API/Holographic/MRC/Settings (GET)**

Obtient la valeur par défaut une réalité mixte paramètres de capture

**/API/Holographic/MRC/file (GET)**

Télécharge un fichier de réalité mixte à partir de l’appareil. Emploi de = le paramètre de requête de flux de diffusion en continu.

Paramètres
* nom de fichier : Nom, hex64 encodée du fichier vidéo à obtenir
* op : flux de données

**/API/Holographic/MRC/Thumbnail (GET)**

Obtient l’image miniature pour le fichier spécifié.

Paramètres
* nom de fichier : Nom, hex64 encodée du fichier pour lequel la miniature est demandée

**/API/Holographic/MRC/Status (GET)**

Obtient l’état de la réalité mixte enregistrée (en cours d’exécution, arrêté)

**/API/Holographic/MRC/Files (GET)**

Retourne la liste des fichiers de réalité mixte stockées sur l’appareil

**/API/Holographic/MRC/Settings (POST)**

Définit la valeur par défaut une réalité mixte paramètres de capture

**/API/Holographic/MRC/Video/Control/Start (POST)**

Démarre un enregistrement de réalité mixte

Paramètres
* Holo : capturer hologrammes : true ou false
* PV : capture PV caméra : true ou false
* MIC : capture microphone : true ou false
* bouclage : capturer des données audio app : true ou false

**/API/Holographic/MRC/Video/Control/Stop (POST)**

S’arrête en cours mixte d’enregistrement de réalité

**/API/Holographic/MRC/photo (POST)**

Prend une photo de réalité mixte et crée un fichier sur l’appareil

Paramètres
* Holo : capturer hologrammes : true ou false
* PV : capture PV caméra : true ou false

Réalité mixte de diffusion en continu

**/api/holographic/stream/live.mp4 (GET)**

Initie un téléchargement mémorisé en bloc d’un mp4 fragmenté

Paramètres
* Holo : capturer hologrammes : true ou false
* PV : capture PV caméra : true ou false
* MIC : capture microphone : true ou false
* bouclage : capturer des données audio app : true ou false

**/api/holographic/stream/live_high.mp4 (GET)**

Initie un téléchargement mémorisé en bloc d’un mp4 fragmenté

Paramètres
* Holo : capturer hologrammes : true ou false
* PV : capture PV caméra : true ou false
* MIC : capture microphone : true ou false
* bouclage : capturer des données audio app : true ou false

**/api/holographic/stream/live_low.mp4 (GET)**

Initie un téléchargement mémorisé en bloc d’un mp4 fragmenté

Paramètres
* Holo : capturer hologrammes : true ou false
* PV : capture PV caméra : true ou false
* MIC : capture microphone : true ou false
* bouclage : capturer des données audio app : true ou false

**/api/holographic/stream/live_med.mp4 (GET)**

Initie un téléchargement mémorisé en bloc d’un mp4 fragmenté

Paramètres
* Holo : capturer hologrammes : true ou false
* PV : capture PV caméra : true ou false
* MIC : capture microphone : true ou false
* bouclage : capturer des données audio app : true ou false

## <a name="networking"></a>Mise en réseau

**/api/networking/ipconfig (GET)**

Obtient la configuration ip actuelle

## <a name="os-information"></a>Informations de système d’exploitation

**/api/os/info (GET)**

Obtient des informations de système d’exploitation

**/API/OS/MachineName (GET)**

Obtient le nom de l’ordinateur

**/api/os/machinename (POST)**

Définit le nom de l’ordinateur

Paramètres
* nom : Nouveau nom de l’ordinateur, hex64 encodée, pour la valeur

## <a name="performance-data"></a>Données relatives aux performances

**/API/ResourceManager/Processes (GET)**

Retourne la liste des processus en cours avec les détails

Retourner des données
* JSON avec la liste des processus et les détails de chaque processus

**/API/ResourceManager/systemperf (GET)**

Retourne des statistiques de performances système (e/s en lecture/écriture, etc. statistiques de la mémoire.

Retourner des données
* JSON avec les informations système : Processeur, processeur, mémoire, réseau, e/s

## <a name="power"></a>Alimentation

**/api/power/battery (GET)**

Obtient l’état actuel de la batterie

**/API/Power/State (GET)**

Vérifie si le système est dans un état de faible consommation d’énergie

## <a name="remote-control"></a>Contrôle à distance

**/api/control/restart (POST)**

Redémarre l’appareil cible

**/API/Control/Shutdown (POST)**

Arrête l’appareil cible

## <a name="task-manager"></a>Gestionnaire des tâches

**/API/TaskManager/App (DELETE)**

Arrête une application moderne

Paramètres
* package : Nom complet du package d’application, hex64 encodé
* arrêt forcé : Forcer tous les processus à arrêter (= yes)

**/api/taskmanager/app (POST)**

Démarre une application moderne

Paramètres
* ID d’application : PRAID d’application pour démarrer, hex64 encodé
* package : Nom complet du package d’application, hex64 encodé

## <a name="wifi-management"></a>Gestion de Wi-Fi

**/api/wifi/interfaces (GET)**

Énumère les interfaces de réseau sans fil

Retourner des données
* Liste des interfaces sans fil avec les détails (GUID, description, etc.).

**/api/wifi/network (DELETE)**

Supprime un profil associé à un réseau sur l’interface spécifiée

Paramètres
* interface : guid de l’interface de réseau
* profil : nom du profil

**/API/WiFi/Networks (GET)**

Énumère les réseaux sans fil sur l’interface réseau spécifiée

Paramètres
* interface : guid de l’interface de réseau

Retourner des données
* Liste des réseaux sans fil trouvés sur l’interface réseau avec les détails

**/api/wifi/network (POST)**

Se connecte ou se déconnecte à un réseau sur l’interface spécifiée

Paramètres
* interface : guid de l’interface de réseau
* SSID : ssid, hex64 codé, pour vous connecter à
* op : connecter ou déconnecter
* CreateProfile : yes ou no
* clé : partagé hex64 clé, encodé

## <a name="windows-performance-recorder"></a>Enregistreur de performances Windows

**/api/wpr/customtrace (POST)**

Télécharge un profil WPR et commence le traçage en utilisant le profil téléchargé.

charge utile
* corps http conforme à plusieurs parties

Retourner des données
* Retourne l’état de session WPR.

**/api/wpr/status (GET)**

Récupère l’état de la session WPR

Retourner des données
* État de session WPR.

**/api/wpr/trace (GET)**

Arrête une session de suivi WPR (performance)

Retourner des données
* Retourne le fichier ETL de suivi

**/api/wpr/trace (POST)**

Démarre un WPR (performance) suivi des sessions

Paramètres
* profil : Nom du profil. Profils disponibles sont stockés dans perfprofiles/profiles.json

Retourner des données
* Au démarrage, retourne l’état de session WPR.

## <a name="see-also"></a>Voir aussi
* [À l’aide de la Windows Device Portal](using-the-windows-device-portal.md)
* [Core de portail appareil référence d’API (UWP)](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-api-core)
