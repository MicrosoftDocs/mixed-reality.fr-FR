---
title: Accessoires matériels
description: Décrit les types d’accessoires disponibles à utiliser avec HoloLens et Windows Mixed Reality et comment les configurer.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: Guide pratique, accessoires, Bluetooth, BT, contrôleur, boîtier de commande, cliquez sur Xbox
ms.openlocfilehash: 566d4217fb674057e1dc3d9791b247185bf61d32
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73435147"
---
# <a name="hardware-accessories"></a>Accessoires matériels

Les appareils Windows Mixed Reality prennent en charge les accessoires. Vous allez associer les accessoires pris en charge à HoloLens à l’aide de Bluetooth, tandis que vous pouvez utiliser Bluetooth ou USB pour coupler les accessoires pris en charge à un casque immersif via le PC auquel il est connecté.

Deux scénarios courants d’utilisation des accessoires avec HoloLens sont les substituts du mouvement d’appui à l’air et du clavier virtuel. Pour ce faire, les deux accessoires les plus courants sont les claviers **HoloLens** et **Bluetooth**. Microsoft HoloLens comprend une radio Bluetooth 4,1 et prend en charge les profils [HID Bluetooth](https://en.wikipedia.org/wiki/List_of_Bluetooth_profiles#Human_Interface_Device_Profile_.28HID.29) et [Bluetooth GATT](https://en.wikipedia.org/wiki/List_of_Bluetooth_profiles#Generic_Attribute_Profile_.28GATT.29) .

Les casques immersifs Windows Mixed Reality requièrent des accessoires pour l’entrée au-delà du [point de vue](gaze-and-commit.md) et de la [voix](voice-input.md). Les accessoires pris en charge incluent le **clavier et la souris**, le **boîtier de soumanette**et les **[contrôleurs de mouvement](motion-controllers.md)** .

## <a name="pairing-bluetooth-accessories"></a>Association des accessoires Bluetooth

Le couplage d’un périphérique Bluetooth avec Microsoft HoloLens est semblable au couplage d’un périphérique Bluetooth à un ordinateur de bureau ou un appareil mobile Windows 10 :
1. Dans le menu Démarrer, ouvrez l’application **paramètres** .
2. Accéder aux **appareils**
3. Activer la radio Bluetooth si elle est désactivée à l’aide du commutateur Slider
4. Mettez votre appareil Bluetooth en mode d’appariement. Cela varie d’un appareil à l’appareil. Sur la plupart des appareils Bluetooth, cette opération s’effectue en appuyant sur un ou plusieurs boutons.
5. Attendez que le nom de l’appareil apparaisse dans la liste des périphériques Bluetooth. Dans ce cas, sélectionnez l’appareil, puis sélectionnez le bouton de **paire** . Si vous avez de nombreux périphériques Bluetooth à proximité, vous devrez peut-être faire défiler vers le bas de la liste des appareils Bluetooth pour voir l’appareil que vous essayez de coupler.
6. Lorsque vous associez des périphériques Bluetooth à une capacité d’entrée (par exemple, des claviers Bluetooth), un code pin à 6 ou 8 chiffres peut s’afficher. Veillez à taper ce code PIN sur le périphérique, puis appuyez sur entrée pour terminer le jumelage avec Microsoft HoloLens.

## <a name="motion-controllers"></a>Contrôleurs de mouvement

Les [contrôleurs de mouvement](motion-controllers.md) Windows Mixed Reality sont pris en charge par les casques immersifs, mais pas HoloLens. Ces contrôleurs offrent un suivi précis et réactif des mouvements dans votre champ de vue à l’aide des capteurs du casque immersif, ce qui signifie qu’il n’est pas nécessaire d’installer le matériel sur les murs de votre espace. Chaque contrôleur est doté de plusieurs méthodes d’entrée.

![Contrôleurs de mouvement Windows Mixed Reality](images/winmr-ck-1080x1080-350px.jpg)

## <a name="hololens-clicker"></a>Clicker de HoloLens

L’interutilisateur HoloLens est le premier périphérique périphérique créé spécifiquement pour HoloLens et est inclus dans l’édition de développement HoloLens. L’utilisateur de l’un des clickers HoloLens permet à un utilisateur de cliquer et de faire défiler avec un déplacement minimal pour remplacer le mouvement d’appui sur l’air. Ce n’est pas un remplacement pour tous les [mouvements](gaze-and-commit.md#composite-gestures). Par exemple, les gestes de [floraison](system-gesture.md#bloom) et de [redimensionnement ou de déplacement](gaze-and-commit.md#composite-gestures) utilisent des mouvements manuels. L’interclic HoloLens est un dispositif de capteur d’orientation avec un bouton simple. Il se connecte à HoloLens à l’aide de la BTLE (Bluetooth Low Energy).

![Clicker du HoloLens](images/hololens-clicker-500px.jpg)

Pour sélectionner un [hologramme](hologram.md), pointez dessus, puis cliquez sur. L’orientation du clic n’a pas d’importance pour cette opération. Pour faire défiler ou panoramiquer, cliquez et maintenez le bouton enfoncé, puis faites pivoter l’utilisateur vers le haut ou vers le haut ou vers la gauche/droite. Lors du défilement, vous atteignez la vitesse la plus rapide avec un minimum de +/-15 ° de rotation du poignet. Le déplacement d’autres ne permet pas de faire défiler plus rapidement.

Il y a deux voyants à l’intérieur du clic :
* La DEL blanche indique si l’appareil est couplé (clignotement) ou en charge (plein)
* Le voyant orange indique que la batterie de l’appareil est faible (clignotement) ou a subi une défaillance (pleine)

Vous pouvez vous attendre à une utilisation régulière de 2 semaines ou plus sur un coût total (par exemple, 2-3 heures sur un chargeur mural). Lorsque la batterie est faible, la LED orange clignote 10 fois sur une période de 5 secondes si vous appuyez sur le bouton ou l’éveil du mode veille. Le voyant orange clignote plus rapidement sur une période de 5 secondes si votre interclic est en mode de batterie faible critique.

## <a name="bluetooth-keyboards"></a>Claviers Bluetooth

Les claviers Bluetooth de l’anglais QWERTY peuvent être couplés et utilisés partout où vous pouvez utiliser le clavier holographique. L’obtention d’un clavier de qualité fait une différence. nous vous recommandons donc d’utiliser le [clavier pliable universel Microsoft](https://www.microsoft.com/accessories/products/keyboards/universal-foldable-keyboard/gu5-00001) ou le [Bureau Bluetooth Microsoft designer](https://www.microsoft.com/accessories/products/keyboards/designer-bluetooth-desktop/7n9-00001).

## <a name="bluetooth-gamepads"></a>Boîtiers de manette Bluetooth

Vous pouvez utiliser un contrôleur avec des applications et des jeux qui activent spécifiquement la prise en charge du boîtier de commande. Les boîtiers de commande ne peuvent pas être utilisés pour contrôler l’interface utilisateur HoloLens.

Les contrôleurs Xbox Wireless livrés avec la Xbox One ou vendus comme accessoires pour la Xbox One S disposent d’une connectivité Bluetooth qui leur permet d’être utilisés avec HoloLens et des casques immersifs. Le contrôleur sans fil Xbox [doit être mis à jour](https://support.xbox.com/xbox-one/accessories/update-controller-for-stereo-headset-adapter) avant de pouvoir être utilisé avec HoloLens.

D’autres marques de manette Bluetooth peuvent fonctionner avec des appareils Windows Mixed Reality, mais la prise en charge varie selon l’application.

## <a name="other-bluetooth-accessories"></a>Autres accessoires Bluetooth

Tant que le périphérique prend en charge les profils HID Bluetooth ou GATT, il sera en mesure de s’associer à HoloLens. Les autres périphériques HID et du GATT Bluetooth, en plus du clavier, de la souris et du module de clic de l’appareil HoloLens, peuvent nécessiter une application complémentaire sur Microsoft HoloLens pour être entièrement fonctionnelle.

Les périphériques non pris en charge sont les suivants :
* Les périphériques dans les profils audio Bluetooth ne sont pas pris en charge.
* Les périphériques audio Bluetooth, tels que les haut-parleurs et les casques, peuvent apparaître comme étant disponibles dans l’application paramètres, mais ne sont pas pris en charge pour être utilisés avec Microsoft HoloLens comme point de terminaison audio.
* Les téléphones et les PC compatibles Bluetooth ne sont pas pris en charge pour le transfert de fichiers.

## <a name="unpairing-a-bluetooth-peripheral"></a>Découplage d’un périphérique Bluetooth
1. Dans le menu Démarrer, ouvrez l’application **paramètres** .
2. Accéder aux **appareils**
3. Activer la radio Bluetooth si elle est désactivée
4. Rechercher votre appareil dans la liste des appareils Bluetooth disponibles
5. Sélectionnez votre appareil dans la liste, puis cliquez sur le bouton **supprimer** .

## <a name="disabling-bluetooth-on-microsoft-hololens"></a>Désactivation de Bluetooth sur Microsoft HoloLens

Cela va entraîner la désactivation des composants RF de la radio Bluetooth et la désactivation de toutes les fonctionnalités Bluetooth sur Microsoft HoloLens.
1. Dans le menu Démarrer, ouvrez l’application **paramètres** .
2. Accéder aux **appareils**
3. Déplacer le commutateur de curseur pour Bluetooth en position hors tension
