---
title: Se connecter au Wi-Fi sur HoloLens
description: Obtenir des instructions sur comment se connecter à internet sans fil avec HoloLens et comment identifier l’adresse IP de l’appareil.
author: mattzmsft
ms.author: mazeller
ms.date: 09/27/2018
ms.topic: article
keywords: HoloLens, wifi, wireless, internet, ip, ip address
ms.openlocfilehash: b064514124d861c0734ca51b3878d4a68b592fab
ms.sourcegitcommit: f5c1dedb3b9e29f27f627025b9e7613931a7ce18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64670118"
---
# <a name="connecting-to-wi-fi-on-hololens"></a>Se connecter au Wi-Fi sur HoloLens

HoloLens contient un 802.11ac-compatible, 2 x 2 radio Wi-Fi. Connexion HoloLens à un réseau Wi-Fi est semblable à la connexion d’un appareil Windows 10 Desktop ou Mobile à un réseau Wi-Fi.

![Paramètres Wi-Fi de HoloLens](images/wifi-hololens-600px.jpg)

## <a name="connecting-to-a-wi-fi-network-on-hololens"></a>Connexion à un réseau Wi-Fi sur HoloLens

1. [Bloom](gestures.md#bloom) à la **Démarrer** menu.
2. Sélectionnez le **paramètres** application à partir du début ou de la **toutes les applications** liste sur la droite du menu Démarrer.
3. Le **paramètres** application seront placés devant vous automatiquement.
4. Sélectionnez **réseau & Internet**.
5. Vérifiez que le Wi-Fi est activé.
6. Sélectionnez un réseau Wi-Fi dans la liste.
7. Tapez le mot de passe réseau Wi-Fi (si nécessaire).

## <a name="disabling-wi-fi-on-hololens"></a>La désactivation de Wi-Fi sur HoloLens

### <a name="using-the-settings-app-on-hololens"></a>À l’aide de l’application paramètres sur HoloLens

1. [Bloom](gestures.md#bloom) à la **Démarrer** menu.
2. Sélectionnez le **paramètres** application à partir du début ou de la **toutes les applications** liste sur la droite du menu Démarrer.
3. Le **paramètres** application seront placés devant vous automatiquement.
4. Sélectionnez **réseau & Internet**.
5. Sélectionnez le commutateur de curseur Wi-Fi pour le déplacer vers la position « Désactivé ». Cela désactiver les composants RF de la radio Wi-Fi et désactivez toutes les fonctionnalités de Wi-Fi sur HoloLens. 

    >[!WARNING]
    >HoloLens ne sera pas en mesure de charger automatiquement votre [espaces](environment-considerations-for-hololens.md#WiFi fingerprint considerations) lorsque la case d’option Wi-Fi est désactivé.
    
6. Déplacez le commutateur de curseur vers la position « Activé » pour activer la case d’option Wi-Fi et restaurer la fonctionnalité Wi-Fi sur Microsoft HoloLens. L’état de radio Wi-Fi sélectionné (« activé » de « Désactivé ») est conservées lors des redémarrages.

## <a name="how-to-confirm-you-are-connected-to-a-wi-fi-network"></a>Comment vérifier que vous êtes connecté à un réseau Wi-Fi

1. [Bloom](gestures.md#bloom) pour faire apparaître le **Démarrer** menu.
2. Regardez en haut à gauche du menu Démarrer pour l’état de Wi-Fi. L’état de Wi-Fi et le SSID du réseau connecté seront affichera.

## <a name="identifying-the-ip-address-of-your-hololens-on-the-wi-fi-network"></a>Identification de l’adresse IP de votre HoloLens sur le réseau Wi-Fi

### <a name="using-the-settings-app"></a>À l’aide de l’application paramètres

1. [Bloom](gestures.md#bloom) à la **Démarrer** menu.
2. Sélectionnez le **paramètres** application à partir du début ou de la **toutes les applications** liste sur la droite du menu Démarrer.
3. Le **paramètres** application seront placés devant vous automatiquement.
4. Sélectionnez **réseau & Internet**.
5. Faites défiler jusqu'à sous la liste des réseaux Wi-Fi disponibles et sélectionnez **propriétés matérielles**.

    ![Propriétés de matériel dans les paramètres Wi-Fi](images/wifi-hololens-hwdetails.jpg)

L’adresse IP s’affichera à côté **adresse IPv4**.

### <a name="using-cortana"></a>À l’aide de Cortana

Par exemple *Hey Cortana, quelle est mon adresse IP ?* et Cortana s’affiche et lire votre adresse IP.

### <a name="using-windows-device-portal"></a>À l’aide de Windows Device Portal

1. Ouvrez le [portail appareils](using-the-windows-device-portal.md#networking) dans un navigateur web sur votre PC.
2. Accédez à la **mise en réseau** section.

Votre adresse IP et autres informations de réseau sont affichées ici. Cette méthode permet de facilement copier et coller de l’adresse IP sur votre PC de développement.
