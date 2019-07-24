---
title: Connexion à Wi-Fi sur HoloLens
description: Instructions sur la façon de se connecter à Wireless Internet avec HoloLens et comment identifier l’adresse IP de l’appareil.
author: mattzmsft
ms.author: mazeller
ms.date: 09/27/2018
ms.topic: article
keywords: HoloLens, WiFi, sans fil, Internet, IP, adresse IP
ms.openlocfilehash: b064514124d861c0734ca51b3878d4a68b592fab
ms.sourcegitcommit: f5c1dedb3b9e29f27f627025b9e7613931a7ce18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64670118"
---
# <a name="connecting-to-wi-fi-on-hololens"></a>Connexion à Wi-Fi sur HoloLens

HoloLens contient une radio Wi-Fi de norme 802.11 2x2. La connexion de HoloLens à un réseau Wi-Fi est semblable à la connexion d’un appareil mobile ou de bureau Windows 10 à un réseau Wi-Fi.

![Paramètres Wi-Fi HoloLens](images/wifi-hololens-600px.jpg)

## <a name="connecting-to-a-wi-fi-network-on-hololens"></a>Connexion à un réseau Wi-Fi sur HoloLens

1. [Dans le](gestures.md#bloom) menu **Démarrer** .
2. Sélectionnez l’application **paramètres** dans Démarrer ou dans la liste **toutes les applications** à droite du menu Démarrer.
3. L’application **paramètres** sera placée automatiquement devant vous.
4. Sélectionnez **réseau & Internet**.
5. Vérifiez que le Wi-Fi est activé.
6. Sélectionnez un réseau Wi-Fi dans la liste.
7. Tapez le mot de passe du réseau Wi-Fi (si nécessaire).

## <a name="disabling-wi-fi-on-hololens"></a>Désactivation de Wi-Fi sur HoloLens

### <a name="using-the-settings-app-on-hololens"></a>Utilisation de l’application paramètres sur HoloLens

1. [Dans le](gestures.md#bloom) menu **Démarrer** .
2. Sélectionnez l’application **paramètres** dans Démarrer ou dans la liste **toutes les applications** à droite du menu Démarrer.
3. L’application **paramètres** sera placée automatiquement devant vous.
4. Sélectionnez **réseau & Internet**.
5. Sélectionnez le commutateur de curseur Wi-Fi pour le déplacer à la position «désactivé». Cela va entraîner la désactivation des composants RF de la radio Wi-Fi et la désactivation de toutes les fonctionnalités Wi-Fi sur HoloLens. 

    >[!WARNING]
    >HoloLens ne peut pas charger automatiquement vos [espaces](environment-considerations-for-hololens.md#WiFi fingerprint considerations) lorsque la radio Wi-Fi est désactivée.
    
6. Déplacez le curseur sur la position «on» pour activer la radio Wi-Fi et restaurer la fonctionnalité Wi-Fi sur Microsoft HoloLens. L’état de radio Wi-Fi sélectionné («activé» de «désactivé») sera conservé au cours des redémarrages.

## <a name="how-to-confirm-you-are-connected-to-a-wi-fi-network"></a>Comment vérifier que vous êtes connecté à un réseau Wi-Fi

1. [Pour afficher](gestures.md#bloom) le menu **Démarrer** .
2. Regardez en haut à gauche du menu Démarrer pour l’État Wi-Fi. L’état de Wi-Fi et le SSID du réseau connecté s’affichent.

## <a name="identifying-the-ip-address-of-your-hololens-on-the-wi-fi-network"></a>Identification de l’adresse IP de votre HoloLens sur le réseau Wi-Fi

### <a name="using-the-settings-app"></a>Utilisation de l’application paramètres

1. [Dans le](gestures.md#bloom) menu **Démarrer** .
2. Sélectionnez l’application **paramètres** dans Démarrer ou dans la liste **toutes les applications** à droite du menu Démarrer.
3. L’application **paramètres** sera placée automatiquement devant vous.
4. Sélectionnez **réseau & Internet**.
5. Faites défiler vers le bas la liste des réseaux Wi-Fi disponibles et sélectionnez **propriétés matérielles**.

    ![Propriétés matérielles dans les paramètres Wi-Fi](images/wifi-hololens-hwdetails.jpg)

L’adresse IP s’affichera en regard de **adresse IPv4**.

### <a name="using-cortana"></a>Utilisation de Cortana

Par exemple *Hey Cortana, quelle est mon adresse IP ?* et Cortana affichent et lisent votre adresse IP.

### <a name="using-windows-device-portal"></a>Utilisation du portail d’appareils Windows

1. Ouvrez le [portail](using-the-windows-device-portal.md#networking) de l’appareil dans un navigateur Web sur votre PC.
2. Accédez à la section **mise en réseau** .

Votre adresse IP et d’autres informations réseau seront affichées ici. Cette méthode permet de copier et coller facilement l’adresse IP sur votre PC de développement.
