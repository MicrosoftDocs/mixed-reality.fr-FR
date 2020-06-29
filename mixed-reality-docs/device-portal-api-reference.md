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
# <a name="device-portal-api-reference"></a>Informations de référence sur les API du portail d’appareil

Tout ce qui se trouve dans le [portail de périphériques Windows](using-the-windows-device-portal.md) repose sur des API REST que vous pouvez utiliser pour accéder aux données et contrôler votre appareil par programme.

## <a name="app-deloyment"></a>Déploiement de l’application

**/API/App/packagemanager/package (supprimer)**

Désinstalle une application

Paramètres
* Package : nom de fichier du package à désinstaller.

**/API/App/packagemanager/package (publication)**

Installe une application

Paramètres
* Package : nom de fichier du package à installer.

Payload
* corps http en plusieurs parties, conforme

**/API/App/packagemanager/packages (récupération)**

Récupère la liste des applications installées sur le système, avec les détails

Retourner les données
* Liste des packages installés avec des détails

**/API/App/packagemanager/State (récupération)**

Obtient l’état de l’installation de l’application en cours

## <a name="dump-collection"></a>Collection de vidages

**/API/Debug/dump/usermode/CrashControl (supprimer)**

Désactive la collecte de vidages sur incident pour une application faisant

Paramètres
* packageFullname : nom du package

**/API/Debug/dump/usermode/CrashControl (récupération)**

Obtient les paramètres de la collection de vidages sur incident des applications faisant

Paramètres
* packageFullname : nom du package

**/API/Debug/dump/usermode/CrashControl (publication)**

Active et définit les paramètres de contrôle de vidage pour une application faisant

Paramètres
* packageFullname : nom du package

**/API/Debug/dump/usermode/crashdump (supprimer)**

Supprime un vidage sur incident pour une application faisant

Paramètres
* packageFullname : nom du package
* fileName : nom du fichier dump

**/API/Debug/dump/usermode/crashdump (récupération)**

Récupère un vidage sur incident pour une application faisant

Paramètres
* packageFullname : nom du package
* fileName : nom du fichier dump

Retourner les données
* Fichier dump. Inspecter avec WinDbg ou Visual Studio

**/API/Debug/dump/usermode/dumps (récupération)**

Retourne la liste de tous les vidages sur incident pour les applications faisant

Retourner les données
* Liste des vidages sur incident par application à chargement latéral

## <a name="etw"></a>ETW

**/API/ETW/Providers (récupération)**

Énumère les fournisseurs inscrits

Retourner les données
* Liste des fournisseurs, nom convivial et GUID

**/API/ETW/session/Realtime (obtient/WebSocket)**

Crée une session ETW en temps réel ; géré sur un WebSocket.

Retourner les données
* Événements ETW des fournisseurs activés

## <a name="holographic-os"></a>Système d’exploitation holographique

**/API/Holographic/OS/ETW/customproviders (récupération)**

Retourne une liste de fournisseurs ETW spécifiques à HoloLens qui ne sont pas inscrits auprès du système.

**/API/Holographic/OS/services (récupération)**

Retourne les États de tous les services en cours d’exécution.

**/API/Holographic/OS/Settings/IPD (récupération)**

Obtient la IPD stockée (distance interpupillary) en millimètres.

**/API/Holographic/OS/Settings/IPD (publication)**

Définit l’IPD

Paramètres
* IPD : nouvelle valeur IPD à définir en millimètres

**/API/Holographic/OS/webmanagement/Settings/HTTPS (récupération)**

Obtenir la spécification HTTPS pour Device Portal

**/API/Holographic/OS/webmanagement/Settings/HTTPS (publication)**

Définit les exigences HTTPs pour le portail de l’appareil

Paramètres
* obligatoire : Oui, non ou par défaut

## <a name="holographic-perception"></a>Perception holographique

**/API/Holographic/perception/client (obtient/WebSocket)**

Accepte les mises à niveau de WebSocket et exécute un client de perception qui envoie des mises à jour à 30 i/s.

Paramètres
* Clientmode : "active" force le mode de suivi visuel lorsqu’il ne peut pas être établi passivement

## <a name="holographic-thermal"></a>Thermique holographique

**/API/Holographic/thermal/stage (récupération)**

Récupération de l’étape thermique de l’appareil (0 normal, 1 chaud, 2 critique)

## <a name="perception-simulation-control"></a>Contrôle de simulation de perception

**/API/Holographic/simulation/Control/mode (récupération)**

Obtient le mode de simulation

**/API/Holographic/simulation/Control/mode (publication)**

Définir le mode de simulation

Paramètres
* mode : mode de simulation : par défaut, simulation, distant, hérité

**/API/Holographic/simulation/Control/Stream (supprimer)**

Supprimer un flux de contrôle.

**/API/Holographic/simulation/Control/Stream (obtient/WebSocket)**

Ouvrez une connexion de socket Web pour un flux de contrôle.

**/API/Holographic/simulation/Control/Stream (publication)**

Créez un flux de contrôle (priorité obligatoire) ou publiez des données dans un flux créé (streamId requis). Les données publiées sont supposées être de type « application/octet-stream ».

**/API/Holographic/Simulation/Display/Stream (obtient/WebSocket)**

Demandez un flux vidéo de simulation contenant le contenu affiché sur le système lorsqu’il est en mode « simulation ».  Un en-tête de descripteur de format simple sera envoyé initialement, suivi des textures encodées H. 264, chacune précédée d’un en-tête indiquant l’index oculaire et la taille de la texture.

## <a name="perception-simulation-playback"></a>Lecture de simulation de perception

**/API/Holographic/simulation/playback/file (supprimer)**

Supprimer un enregistrement.

Paramètres
* enregistrement : nom de l’enregistrement à supprimer.

**/API/Holographic/simulation/playback/file (publication)**

Télécharger un enregistrement.

**/API/Holographic/simulation/playback/Files (récupération)**

Récupération de tous les enregistrements.

**/API/Holographic/simulation/playback/session (récupération)**

Obtient l’état de lecture actuel d’un enregistrement.

Paramètres
* enregistrement : nom de l’enregistrement.

**/API/Holographic/simulation/playback/session/file (supprimer)**

Décharger un enregistrement.

Paramètres
* enregistrement : nom de l’enregistrement à décharger.

**/API/Holographic/simulation/playback/session/file (publication)**

Charger un enregistrement.

Paramètres
* enregistrement : nom de l’enregistrement à charger.

**/API/Holographic/simulation/playback/session/Files (récupération)**

Récupération de tous les enregistrements chargés.

**/API/Holographic/simulation/playback/session/pause (publication)**

Suspendre un enregistrement.

Paramètres
* enregistrement : nom de l’enregistrement.

**/API/Holographic/simulation/playback/session/Play (publication)**

Lire un enregistrement.

Paramètres
* enregistrement : nom de l’enregistrement.

**/API/Holographic/simulation/playback/session/Stop (publication)**

Arrêter un enregistrement.

Paramètres
* enregistrement : nom de l’enregistrement.

**/API/Holographic/simulation/playback/session/types (récupération)**

Obtenir les types de données dans un enregistrement chargé.

Paramètres
* enregistrement : nom de l’enregistrement.

## <a name="perception-simulation-recording"></a>Enregistrement de simulation de perception

**/API/Holographic/simulation/Recording/Start (publication)**

Démarrez un enregistrement. Un seul enregistrement peut être actif à la fois. Vous devez définir l’un des principaux, mains, spatialMapping ou environnement.

Paramètres
* Head : définissez sur 1 pour enregistrer les données de tête.
* mains : définissez sur 1 pour enregistrer les données de la main.
* spatialMapping : affectez la valeur 1 pour enregistrer le mappage spatial.
* environnement : définissez sur 1 pour enregistrer les données d’environnement.
* nom : nom de l’enregistrement.
* singleSpatialMappingFrame : affectez la valeur 1 pour enregistrer uniquement un seul frame de mappage spatial.

**/API/Holographic/simulation/Recording/Status (récupération)**

Obtient l’état de l’enregistrement.

**/API/Holographic/simulation/Recording/Stop (récupération)**

Arrêter l’enregistrement en cours. L’enregistrement est retourné sous la forme d’un fichier.

## <a name="mixed-reality-capture"></a>MRC (Mixed Reality Capture)

**/API/Holographic/MRC/file (récupération)**

Télécharge un fichier de réalité mixte à partir de l’appareil. Utilisez le paramètre de requête op = Stream pour la diffusion en continu.

Paramètres
* nom de fichier : nom, hex64 encodé, du fichier vidéo à récupérer
* OP : flux

**/API/Holographic/MRC/file (supprimer)**

Supprime un enregistrement de la réalité mixte de l’appareil.

Paramètres
* nom de fichier : nom, hex64 encodé, du fichier à supprimer

**/API/Holographic/MRC/Files (récupération)**

Retourne la liste des fichiers de réalité mixte stockés sur l’appareil

**/API/Holographic/MRC/photo (publication)**

Prend une photo de réalité mixte et crée un fichier sur l’appareil

Paramètres
* Holo : capturer les hologrammes : true ou false (false par défaut)
* PV : capturer l’appareil photo PV : true ou false (false par défaut)
* RenderFromCamera : (HoloLens 2 uniquement) rendu du point de vue de la caméra photo/vidéo : true ou false (true par défaut)

**/API/Holographic/MRC/Settings (récupération)**

Obtient les paramètres de capture de la réalité mixte par défaut

**/API/Holographic/MRC/Settings (publication)**

Définit les paramètres de capture de la réalité mixte par défaut.  Certains de ces paramètres sont appliqués à la photo et à la capture de vidéo MRC du système.

**/API/Holographic/MRC/Status (récupération)**

Obtient l’état de capture de la réalité mixte dans le portail de périphériques Windows.

***Réponse***

La réponse contient une propriété JSON indiquant si le portail de périphériques Windows enregistre ou non une vidéo.

``` javascript
{"IsRecording" : boolean}
```

**/API/Holographic/MRC/thumbnail (récupération)**

Obtient l’image miniature pour le fichier spécifié.

Paramètres
* nom de fichier : nom, hex64 encodé, du fichier pour lequel la miniature est demandée.

**/API/Holographic/MRC/Video/Control/Start (publication)**

Démarre un enregistrement de la réalité mixte

Paramètres
* Holo : capturer les hologrammes : true ou false (false par défaut)
* PV : capturer l’appareil photo PV : true ou false (false par défaut)
* MIC : capturer le microphone : true ou false (false par défaut)
* loopback : capturer l’audio de l’application : true ou false (false par défaut)
* RenderFromCamera : (HoloLens 2 uniquement) rendu du point de vue de la caméra photo/vidéo : true ou false (true par défaut)
* Vstab : (HoloLens 2 uniquement) activer la stabilisation vidéo : true ou false (true par défaut)
* vstabbuffer : (HoloLens 2 uniquement) latence de la mémoire tampon de stabilisation vidéo : de 0 à 30 frames (15 images par défaut)

**/API/Holographic/MRC/Video/Control/Stop (publication)**

Arrête l’enregistrement de la réalité mixte actuelle

## <a name="mixed-reality-streaming"></a>Diffusion en continu de la réalité mixte

HoloLens prend en charge l’aperçu instantané de la réalité mixte via le téléchargement segmenté d’un MP4 fragmenté.

Les flux de réalité mixte partagent le même ensemble de paramètres pour contrôler ce qui est capturé :
* Holo : capturer les hologrammes : true ou false
* PV : capturer l’appareil photo PV : true ou false
* MIC : capturer le microphone : true ou false
* loopback : capturer l’audio de l’application : true ou false

Si aucun de ces éléments n’est spécifié : les hologrammes, la caméra photo/vidéo et l’audio de l’application sont capturés<br>
Si des paramètres sont spécifiés : les paramètres non spécifiés ont par défaut la valeur false

Paramètres facultatifs (HoloLens 2 uniquement)
* RenderFromCamera : rendu du point de vue de la caméra photo/vidéo : true ou false (true par défaut)
* Vstab : activer la stabilisation vidéo : true ou false (false par défaut)
* vstabbuffer : latence de la mémoire tampon de stabilisation vidéo : de 0 à 30 frames (15 images par défaut)

**/API/Holographic/Stream/live.mp4 (récupération)**

Un flux 1280x720p 30fps 5Mbit.

**/API/Holographic/Stream/live_high.mp4 (récupération)**

Un flux 1280x720p 30fps 5Mbit.

**/API/Holographic/Stream/live_med.mp4 (récupération)**

Flux 854x480p 30fps 2,5 Mbits.

**/API/Holographic/Stream/live_low.mp4 (récupération)**

Flux 428x240p 15fps 0,6 Mbit.

## <a name="networking"></a>Mise en réseau

**/API/Networking/ipconfig (récupération)**

Obtient la configuration IP actuelle

## <a name="os-information"></a>Informations sur le système d’exploitation

**/API/OS/info (récupération)**

Obtient des informations sur le système d’exploitation

**/API/OS/MachineName (récupération)**

Obtient le nom de l’ordinateur

**/API/OS/MachineName (publication)**

Définit le nom de l’ordinateur

Paramètres
* nom : nouveau nom de l’ordinateur, hex64 encodé, à affecter à

## <a name="performance-data"></a>Données de performances

**/API/ResourceManager/Processes (récupération)**

Retourne la liste des processus en cours d’exécution avec les détails

Retourner les données
* JSON avec liste de processus et détails pour chaque processus

**/API/ResourceManager/systemperf (récupération)**

Retourne les statistiques de performances système (lecture/écriture d’e/s, statistiques de mémoire, etc.).

Retourner les données
* JSON avec informations système : processeur, GPU, mémoire, réseau, e/s

## <a name="power"></a>Avancé

**/API/Power/Battery (récupération)**

Obtient l’état actuel de la batterie

**/API/Power/State (récupération)**

Vérifie si le système est dans un état de faible consommation d’énergie.

## <a name="remote-control"></a>Contrôle à distance

**/API/Control/Restart (publication)**

Redémarre l’appareil cible

**/API/Control/Shutdown (publication)**

Arrête l’appareil cible

## <a name="task-manager"></a>Gestionnaire des tâches

**/API/taskmanager/App (supprimer)**

Arrête une application moderne

Paramètres
* Package : nom complet du package d’application, hex64 encodé
* forceStop : force l’arrêt de tous les processus (= oui)

**/API/taskmanager/App (publication)**

Démarre une application moderne

Paramètres
* AppID : PRAID de l’application à démarrer, hex64 encodé
* Package : nom complet du package d’application, hex64 encodé

## <a name="wifi-management"></a>Gestion WiFi

**/API/WiFi/interfaces (récupération)**

Énumère les interfaces de réseau sans fil

Retourner les données
* Liste des interfaces sans fil avec des détails (GUID, description, etc.)

**/API/WiFi/Network (supprimer)**

Supprime un profil associé à un réseau sur une interface spécifiée

Paramètres
* Interface : GUID de l’interface réseau
* Profil : nom du profil

**/API/WiFi/Networks (récupération)**

Énumère les réseaux sans fil sur l’interface réseau spécifiée.

Paramètres
* Interface : GUID de l’interface réseau

Retourner les données
* Liste des réseaux sans fil détectés sur l’interface réseau avec les détails

**/API/WiFi/Network (publication)**

Se connecte ou se déconnecte à un réseau sur l’interface spécifiée

Paramètres
* Interface : GUID de l’interface réseau
* SSID : SSID, hex64 encodé, pour se connecter à
* opération : se connecter ou se déconnecter
* CreateProfile : oui ou non
* clé : clé partagée, encodée en hex64

## <a name="windows-performance-recorder"></a>Enregistreur de performances Windows

**/API/WPR/customtrace (publication)**

Charge un profil WPR et démarre le suivi à l’aide du profil chargé.

Payload
* corps http en plusieurs parties, conforme

Retourner les données
* Retourne l’état de la session WPR.

**/API/WPR/Status (récupération)**

Récupère l’état de la session WPR

Retourner les données
* État de session WPR.

**/API/WPR/trace (récupération)**

Arrête une session de suivi WPR (performance)

Retourner les données
* Retourne le fichier ETL de trace

**/API/WPR/trace (publication)**

Démarre une session de suivi WPR (performance)

Paramètres
* Profil : nom du profil. Les profils disponibles sont stockés dans perfprofiles/profiles.jssur

Retourner les données
* Dans Démarrer, retourne l’état de la session WPR.

## <a name="see-also"></a>Voir aussi
* [Utilisation du portail d’appareil Windows](using-the-windows-device-portal.md)
* [Informations de référence sur l’API principale du portail des appareils (UWP)](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-api-core)
