---
title: Accessoires de matériel
description: Décrit les types d’accessoires disponibles à utiliser avec HoloLens et Windows Mixed Reality et comment les configurer.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: savoir-faire, Accessoires, bluetooth, bt, contrôleur, gamepad, clicker, xbox
ms.openlocfilehash: c25f849cbf05a78ba2fe7118dbe160d05e0f5e3f
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596980"
---
# <a name="hardware-accessories"></a>Accessoires de matériel

Appareils de réalité mixte Windows prennent en charge les accessoires. Vous allez associer des accessoires pris en charge pour HoloLens à l’aide de Bluetooth, tandis que vous pouvez utiliser Bluetooth ou USB à paire pris en charge des accessoires pour un casque immersif via le PC auquel il est connecté.

Deux scénarios courants pour l’utilisation des accessoires avec HoloLens sont comme substituts pour l’air appuyez sur le clavier virtuel et mouvement. Pour ce faire, les deux accessoires courants sont le **HoloLens Clicker** et **claviers**. Microsoft HoloLens inclut une case d’option Bluetooth 4.1 et prend en charge [HID Bluetooth](https://en.wikipedia.org/wiki/List_of_Bluetooth_profiles#Human_Interface_Device_Profile_.28HID.29) et [Bluetooth GATT](https://en.wikipedia.org/wiki/List_of_Bluetooth_profiles#Generic_Attribute_Profile_.28GATT.29) profils.

Des casques IMMERSIFS Windows Mixed Reality requièrent des accessoires pour l’entrée au-delà [les regards](gaze.md) et [voix](voice-input.md). Accessoires pris en charge incluent **clavier et souris**, **gamepad**, et  **[contrôleurs de mouvement](motion-controllers.md)**.

## <a name="pairing-bluetooth-accessories"></a>Appariement accessoires Bluetooth

Appariement d’un périphérique Bluetooth périphérique avec Microsoft HoloLens est similaire à l’appariement d’un périphérique Bluetooth périphérique avec Windows 10 desktop ou un appareil mobile :
1. Dans le Menu Démarrer, ouvrez le **paramètres** application
2. Accédez à **appareils**
3. Activez la case d’option Bluetooth si elle est désactivée à l’aide du commutateur de curseur
4. Placez votre périphérique Bluetooth en mode de jumelage. Cela varie d’un périphérique à l’autre. Sur la plupart des périphériques Bluetooth cela en appuyant sur un ou plusieurs boutons.
5. Attendez que le nom de l’appareil s’affichent dans la liste des appareils Bluetooth. Quand il, sélectionnez l’appareil, sélectionnez le **paire** bouton. Si vous avez de nombreux périphériques Bluetooth proches vous devrez peut-être faire défiler vers le bas de la liste des appareils Bluetooth pour voir l’appareil que vous voulez associer.
6. Lorsque appariement des périphériques Bluetooth avec l'entrée fonctionnalité (par exemple : Claviers), un chiffre de 6 ou un code confidentiel à 8 chiffres peut-être s’afficher. Veillez à taper ce code pin sur le périphérique et appuyez sur ENTRÉE pour un appariement complète avec Microsoft HoloLens.

## <a name="motion-controllers"></a>Contrôleurs de mouvement

Windows Mixed Reality [contrôleurs de mouvement](motion-controllers.md) sont pris en charge par des casques IMMERSIFS, mais pas HoloLens. Ces contrôleurs offrent précis et réactif suivi du mouvement dans votre champ de vue à l’aide des capteurs dans le casque immersif, ce qui signifie qu’il est inutile d’installer le matériel sur les murs dans votre espace. Chaque contrôleur propose plusieurs méthodes d’entrée.

![Contrôleurs de mouvement Windows Mixed Reality](images/winmr-ck-1080x1080-350px.jpg)

## <a name="hololens-clicker"></a>HoloLens Clicker

Le HoloLens Clicker est le premier périphérique spécialement conçu pour HoloLens et est inclus avec l’édition de développement HoloLens. Le HoloLens Clicker permet à un utilisateur de cliquer sur et défilement des animations minimale disponible en tant qu’un remplacement pour le mouvement d’appui en l’air. Il n’est pas un remplacement pour tous les [mouvements](gestures.md). Par exemple, [bloom](gestures.md#bloom) et [redimensionner ou déplacer](gestures.md#composite-gestures) mouvements utilisent les mouvements de main. Le clicker HoloLens est un dispositif de capteur d’orientation d’un simple. Il se connecte à la HoloLens à l’aide de Bluetooth faible énergie (BTLE).

![Le HoloLens Clicker](images/hololens-clicker-500px.jpg)

Pour sélectionner un [hologramme](hologram.md), fixez du il regard, puis cliquez sur. Orientation de la clicker n’a pas d’importance pour cette opération. Pour faire défiler ou effectuer un panoramique, cliquez sur et maintenez-la enfoncée, puis faites tourner la Clicker haut/bas ou gauche/droite. Pendant le défilement, vous pouvez d’obtenir la vitesse plus rapide avec aussi peu que +/-15 degrés de rotation de poignet. Ajouter d’autres pas défilera les plus rapidement.

Il existe deux LED à l’intérieur de la Clicker :
* La LED blanche indique si l’appareil est jumelage (clignoter) ou de facturation (fixe)
* L’orange indique que l’appareil a batterie faible (clignoter) ou a subi un échec (fixe)

Vous pouvez vous attendre au moins 2 semaines d’utilisation régulière avec une charge maximale (par exemple, 2 à 3 heures sur un chargeur de mur). Lorsque la batterie est faible, l’orange qu'et clignote 10 fois sur une période de 5 secondes si vous appuyez sur le bouton ou sortir du mode veille. L’orange que voyant clignote plus rapidement sur une période de 5 secondes si votre Clicker est en mode batterie dangereusement faible.

## <a name="bluetooth-keyboards"></a>Claviers Bluetooth

Claviers Qwerty en langue anglaise peuvent être jumelés et utilisée partout où que vous pouvez utiliser le clavier HOLOGRAPHIQUE. L’obtention d’un clavier de qualité apporte une différence, nous recommandons donc du [clavier pliable universel Microsoft](https://www.microsoft.com/accessories/products/keyboards/universal-foldable-keyboard/gu5-00001) ou le [Microsoft concepteur Bluetooth Desktop](https://www.microsoft.com/accessories/products/keyboards/designer-bluetooth-desktop/7n9-00001).

## <a name="bluetooth-gamepads"></a>Les boîtiers de commande Bluetooth

Vous pouvez utiliser un contrôleur avec les applications et des jeux qui spécifiquement activent la prise en charge de gamepad. Boîtiers de commande ne peut pas être utilisé pour contrôler l’interface utilisateur de HoloLens.

Contrôleurs de sans fil Xbox fournis avec le S une Xbox ou vendus en tant que des accessoires pour la fonctionnalité S une Xbox la connectivité Bluetooth leur permettant d’être utilisé avec HoloLens et des casques IMMERSIFS. Le contrôleur sans fil Xbox [doit être mis à jour](https://support.xbox.com/xbox-one/accessories/update-controller-for-stereo-headset-adapter) avant de pouvoir être utilisé avec HoloLens.

Autres marques de boîtiers de commande Bluetooth peuvent fonctionner avec les appareils Windows Mixed Reality, mais la prise en charge varie par application.

## <a name="other-bluetooth-accessories"></a>Autres accessoires Bluetooth

Tant que le périphérique prend en charge les profils Bluetooth HID ou GATT, il sera en mesure de coupler avec HoloLens. Autres appareils Bluetooth HID et GATT outre clavier, souris et le HoloLens Clicker peuvent nécessiter une application Compagnon sur Microsoft HoloLens soit pleinement opérationnelle.

Les périphériques non pris en charge sont les suivantes :
* Périphériques dans les profils audio Bluetooth ne sont pas pris en charge.
* Périphériques audio Bluetooth tels que les intervenants, les écouteurs peuvent apparaître comme étant disponibles dans l’application paramètres, mais ne sont pas pris en charge pour être utilisé avec Microsoft HoloLens comme point de terminaison audio.
* Avec des téléphones et des PC ne sont pas pris en charge pour être couplé et utilisés pour le transfert de fichier.

## <a name="unpairing-a-bluetooth-peripheral"></a>Découplage d’un périphérique de Bluetooth
1. Dans le Menu Démarrer, ouvrez le **paramètres** application
2. Accédez à **appareils**
3. Activez la case d’option Bluetooth si elle est désactivée
4. Recherchez votre appareil dans la liste des appareils Bluetooth disponibles
5. Sélectionnez votre appareil dans la liste, puis sélectionnez le **supprimer** bouton

## <a name="disabling-bluetooth-on-microsoft-hololens"></a>La désactivation de Bluetooth sur Microsoft HoloLens

Cela désactiver les composants RF de la radio Bluetooth et désactivez toutes les fonctionnalités de Bluetooth sur Microsoft HoloLens.
1. Dans le Menu Démarrer, ouvrez le **paramètres** application
2. Accédez à **appareils**
3. Déplacer le commutateur de curseur pour Bluetooth à la position d’arrêt
