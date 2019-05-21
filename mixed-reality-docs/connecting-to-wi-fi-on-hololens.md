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
# <a name="connecting-to-wi-fi-on-hololens"></a><span data-ttu-id="27373-104">Se connecter au Wi-Fi sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="27373-104">Connecting to Wi-Fi on HoloLens</span></span>

<span data-ttu-id="27373-105">HoloLens contient un 802.11ac-compatible, 2 x 2 radio Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="27373-105">HoloLens contains a 802.11ac-capable, 2x2 Wi-Fi radio.</span></span> <span data-ttu-id="27373-106">Connexion HoloLens à un réseau Wi-Fi est semblable à la connexion d’un appareil Windows 10 Desktop ou Mobile à un réseau Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="27373-106">Connecting HoloLens to a Wi-Fi network is similar to connecting a Windows 10 Desktop or Mobile device to a Wi-Fi network.</span></span>

![Paramètres Wi-Fi de HoloLens](images/wifi-hololens-600px.jpg)

## <a name="connecting-to-a-wi-fi-network-on-hololens"></a><span data-ttu-id="27373-108">Connexion à un réseau Wi-Fi sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="27373-108">Connecting to a Wi-Fi network on HoloLens</span></span>

1. <span data-ttu-id="27373-109">[Bloom](gestures.md#bloom) à la **Démarrer** menu.</span><span class="sxs-lookup"><span data-stu-id="27373-109">[Bloom](gestures.md#bloom) to the **Start** menu.</span></span>
2. <span data-ttu-id="27373-110">Sélectionnez le **paramètres** application à partir du début ou de la **toutes les applications** liste sur la droite du menu Démarrer.</span><span class="sxs-lookup"><span data-stu-id="27373-110">Select the **Settings** app from Start or from the **All Apps** list on the right of the Start menu.</span></span>
3. <span data-ttu-id="27373-111">Le **paramètres** application seront placés devant vous automatiquement.</span><span class="sxs-lookup"><span data-stu-id="27373-111">The **Settings** app will be auto-placed in front of you.</span></span>
4. <span data-ttu-id="27373-112">Sélectionnez **réseau & Internet**.</span><span class="sxs-lookup"><span data-stu-id="27373-112">Select **Network & Internet**.</span></span>
5. <span data-ttu-id="27373-113">Vérifiez que le Wi-Fi est activé.</span><span class="sxs-lookup"><span data-stu-id="27373-113">Make sure Wi-Fi is turned on.</span></span>
6. <span data-ttu-id="27373-114">Sélectionnez un réseau Wi-Fi dans la liste.</span><span class="sxs-lookup"><span data-stu-id="27373-114">Select a Wi-Fi network from the list.</span></span>
7. <span data-ttu-id="27373-115">Tapez le mot de passe réseau Wi-Fi (si nécessaire).</span><span class="sxs-lookup"><span data-stu-id="27373-115">Type in the Wi-Fi network password (if needed).</span></span>

## <a name="disabling-wi-fi-on-hololens"></a><span data-ttu-id="27373-116">La désactivation de Wi-Fi sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="27373-116">Disabling Wi-Fi on HoloLens</span></span>

### <a name="using-the-settings-app-on-hololens"></a><span data-ttu-id="27373-117">À l’aide de l’application paramètres sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="27373-117">Using the Settings app on HoloLens</span></span>

1. <span data-ttu-id="27373-118">[Bloom](gestures.md#bloom) à la **Démarrer** menu.</span><span class="sxs-lookup"><span data-stu-id="27373-118">[Bloom](gestures.md#bloom) to the **Start** menu.</span></span>
2. <span data-ttu-id="27373-119">Sélectionnez le **paramètres** application à partir du début ou de la **toutes les applications** liste sur la droite du menu Démarrer.</span><span class="sxs-lookup"><span data-stu-id="27373-119">Select the **Settings** app from Start or from the **All Apps** list on the right of the Start menu.</span></span>
3. <span data-ttu-id="27373-120">Le **paramètres** application seront placés devant vous automatiquement.</span><span class="sxs-lookup"><span data-stu-id="27373-120">The **Settings** app will be auto-placed in front of you.</span></span>
4. <span data-ttu-id="27373-121">Sélectionnez **réseau & Internet**.</span><span class="sxs-lookup"><span data-stu-id="27373-121">Select **Network & Internet**.</span></span>
5. <span data-ttu-id="27373-122">Sélectionnez le commutateur de curseur Wi-Fi pour le déplacer vers la position « Désactivé ».</span><span class="sxs-lookup"><span data-stu-id="27373-122">Select the Wi-Fi slider switch to move it to the "Off" position.</span></span> <span data-ttu-id="27373-123">Cela désactiver les composants RF de la radio Wi-Fi et désactivez toutes les fonctionnalités de Wi-Fi sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="27373-123">This will turn off the RF components of the Wi-Fi radio and disable all Wi-Fi functionality on HoloLens.</span></span> 

    >[!WARNING]
    ><span data-ttu-id="27373-124">HoloLens ne sera pas en mesure de charger automatiquement votre [espaces](environment-considerations-for-hololens.md#WiFi fingerprint considerations) lorsque la case d’option Wi-Fi est désactivé.</span><span class="sxs-lookup"><span data-stu-id="27373-124">HoloLens will not be able to automatically load your [spaces](environment-considerations-for-hololens.md#WiFi fingerprint considerations) when the Wi-Fi radio is disabled.</span></span>
    
6. <span data-ttu-id="27373-125">Déplacez le commutateur de curseur vers la position « Activé » pour activer la case d’option Wi-Fi et restaurer la fonctionnalité Wi-Fi sur Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="27373-125">Move the slider switch to the "On" position to turn on the Wi-Fi radio and restore Wi-Fi functionality on Microsoft HoloLens.</span></span> <span data-ttu-id="27373-126">L’état de radio Wi-Fi sélectionné (« activé » de « Désactivé ») est conservées lors des redémarrages.</span><span class="sxs-lookup"><span data-stu-id="27373-126">The selected Wi-Fi radio state ("On" of "Off") will persist across reboots.</span></span>

## <a name="how-to-confirm-you-are-connected-to-a-wi-fi-network"></a><span data-ttu-id="27373-127">Comment vérifier que vous êtes connecté à un réseau Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="27373-127">How to confirm you are connected to a Wi-Fi network</span></span>

1. <span data-ttu-id="27373-128">[Bloom](gestures.md#bloom) pour faire apparaître le **Démarrer** menu.</span><span class="sxs-lookup"><span data-stu-id="27373-128">[Bloom](gestures.md#bloom) to bring up the **Start** menu.</span></span>
2. <span data-ttu-id="27373-129">Regardez en haut à gauche du menu Démarrer pour l’état de Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="27373-129">Look at the top left of the Start menu for Wi-Fi status.</span></span> <span data-ttu-id="27373-130">L’état de Wi-Fi et le SSID du réseau connecté seront affichera.</span><span class="sxs-lookup"><span data-stu-id="27373-130">The state of Wi-Fi and the SSID of the connected network will be shown.</span></span>

## <a name="identifying-the-ip-address-of-your-hololens-on-the-wi-fi-network"></a><span data-ttu-id="27373-131">Identification de l’adresse IP de votre HoloLens sur le réseau Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="27373-131">Identifying the IP Address of your HoloLens on the Wi-Fi network</span></span>

### <a name="using-the-settings-app"></a><span data-ttu-id="27373-132">À l’aide de l’application paramètres</span><span class="sxs-lookup"><span data-stu-id="27373-132">Using the Settings app</span></span>

1. <span data-ttu-id="27373-133">[Bloom](gestures.md#bloom) à la **Démarrer** menu.</span><span class="sxs-lookup"><span data-stu-id="27373-133">[Bloom](gestures.md#bloom) to the **Start** menu.</span></span>
2. <span data-ttu-id="27373-134">Sélectionnez le **paramètres** application à partir du début ou de la **toutes les applications** liste sur la droite du menu Démarrer.</span><span class="sxs-lookup"><span data-stu-id="27373-134">Select the **Settings** app from Start or from the **All Apps** list on the right of the Start menu.</span></span>
3. <span data-ttu-id="27373-135">Le **paramètres** application seront placés devant vous automatiquement.</span><span class="sxs-lookup"><span data-stu-id="27373-135">The **Settings** app will be auto-placed in front of you.</span></span>
4. <span data-ttu-id="27373-136">Sélectionnez **réseau & Internet**.</span><span class="sxs-lookup"><span data-stu-id="27373-136">Select **Network & Internet**.</span></span>
5. <span data-ttu-id="27373-137">Faites défiler jusqu'à sous la liste des réseaux Wi-Fi disponibles et sélectionnez **propriétés matérielles**.</span><span class="sxs-lookup"><span data-stu-id="27373-137">Scroll down to beneath the list of available Wi-Fi networks and select **Hardware properties**.</span></span>

    ![Propriétés de matériel dans les paramètres Wi-Fi](images/wifi-hololens-hwdetails.jpg)

<span data-ttu-id="27373-139">L’adresse IP s’affichera à côté **adresse IPv4**.</span><span class="sxs-lookup"><span data-stu-id="27373-139">The IP address will be shown next to **IPv4 address**.</span></span>

### <a name="using-cortana"></a><span data-ttu-id="27373-140">À l’aide de Cortana</span><span class="sxs-lookup"><span data-stu-id="27373-140">Using Cortana</span></span>

<span data-ttu-id="27373-141">Par exemple *Hey Cortana, quelle est mon adresse IP ?*</span><span class="sxs-lookup"><span data-stu-id="27373-141">Say "*Hey Cortana, What's my IP address?*"</span></span> <span data-ttu-id="27373-142">et Cortana s’affiche et lire votre adresse IP.</span><span class="sxs-lookup"><span data-stu-id="27373-142">and Cortana will display and read out your IP address.</span></span>

### <a name="using-windows-device-portal"></a><span data-ttu-id="27373-143">À l’aide de Windows Device Portal</span><span class="sxs-lookup"><span data-stu-id="27373-143">Using Windows Device Portal</span></span>

1. <span data-ttu-id="27373-144">Ouvrez le [portail appareils](using-the-windows-device-portal.md#networking) dans un navigateur web sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="27373-144">Open the [device portal](using-the-windows-device-portal.md#networking) in a web browser on your PC.</span></span>
2. <span data-ttu-id="27373-145">Accédez à la **mise en réseau** section.</span><span class="sxs-lookup"><span data-stu-id="27373-145">Navigate to the **Networking** section.</span></span>

<span data-ttu-id="27373-146">Votre adresse IP et autres informations de réseau sont affichées ici.</span><span class="sxs-lookup"><span data-stu-id="27373-146">Your IP address and other network information will be displayed there.</span></span> <span data-ttu-id="27373-147">Cette méthode permet de facilement copier et coller de l’adresse IP sur votre PC de développement.</span><span class="sxs-lookup"><span data-stu-id="27373-147">This method allows for easy copy and paste of the IP address on your development PC.</span></span>
