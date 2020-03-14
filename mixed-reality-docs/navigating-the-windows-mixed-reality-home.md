---
title: Navigation dans la page d’hébergement Windows Mixed Reality
description: Les casques HoloLens et Windows Mixed realisation partagent un paradigme pour le lancement, le placement et la manipulation des applications et des modèles 3D dans votre environnement (physique ou numérique). Découvrez comment accéder à la page d’hébergement de la réalité mixte Windows sur les deux types d’appareils.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: Shell, système d’exploitation, plateforme, maison, maison, accueil, environnement, démarrer, menu Démarrer, menu Accueil, pin, application, lancer des applications, placer des applications, téléporter, déplacer, naviguer
ms.openlocfilehash: 9de4cb44505d6cf4d0d3e4bd0fd9c5ee681063a5
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79375896"
---
# <a name="navigating-the-windows-mixed-reality-home"></a>Navigation dans la page d’hébergement Windows Mixed Reality

Tout comme l’expérience du PC Windows commence avec le bureau, Windows Mixed Reality commence par la page d’hébergement. La page d’hébergement Windows Mixed Reality utilise notre capacité innée pour comprendre et parcourir les emplacements 3D. Avec HoloLens, votre foyer est votre espace physique. Avec les casques immersifs, votre foyer est une place virtuelle.

Votre foyer est également l’emplacement où vous allez utiliser le menu Démarrer pour ouvrir et placer des applications et du contenu. Vous pouvez remplir votre foyer avec du contenu de réalité mixte et utiliser plusieurs applications en même temps. Les choses que vous placez dans votre foyer restent là, même si vous redémarrez votre appareil.

## <a name="start-menu"></a>Menu Démarrer

![Menu Démarrer sur Microsoft HoloLens](images/start-500px.png)

Le menu Démarrer se compose des éléments suivants :
* Informations système (État du réseau, pourcentage de batterie, heure actuelle et volume)
* Cortana (sur les casques immersifs, une vignette de démarrage ; sur HoloLens, en haut du début)
* Applications épinglées
* Bouton toutes les applications (signe plus)
* Boutons photo et vidéo pour la capture de la [réalité mixte](mixed-reality-capture.md)

Basculez entre les vues applications épinglées et toutes les applications en sélectionnant les boutons plus ou moins. Pour ouvrir le menu Démarrer sur HoloLens, utilisez le mouvement fleuri. Sur un casque immersif, appuyez sur le bouton Windows de votre contrôleur.

## <a name="launching-apps"></a>Lancement d’applications

Pour lancer une application, sélectionnez-la au démarrage. Le menu Démarrer disparaît et l’application s’ouvre en mode placement, sous la forme d’une fenêtre 2D ou d’un [modèle 3D](implementing-3d-app-launchers.md).

Pour exécuter l’application, vous devez la placer dans votre foyer :
1. Utilisez votre point d’interposition [ou contrôleur](gaze-and-commit.md) pour positionner l’application là où vous le souhaitez. Elle s’ajuste automatiquement (en taille et en position) pour se conformer à l’espace où vous la placez.
2. Placez l’application à l’aide d’air-TAP (HoloLens) ou du bouton de sélection (casques immersifs). Pour annuler et revenir au menu Démarrer, utilisez le geste de touche ou le bouton Windows.

les [applications 2D](building-2d-apps.md), créées pour un ordinateur de bureau, un appareil mobile ou une Xbox, peuvent être modifiées pour s’exécuter en tant qu’applications immersives de réalité mixte à l’aide de l' [API HolographicSpace](https://msdn.microsoft.com/library/windows/apps/windows.graphics.holographic.holographicspace.aspx). Une application immersive fait sortir l’utilisateur de son lieu de départ et d’une expérience immersive. Les utilisateurs peuvent retourner chez eux avec le geste (HoloLens) ou en appuyant sur le bouton Windows de leur contrôleur (casques immersifs).

Les applications peuvent également être lancées via une API app-to-App ou via Cortana.

![Applications dans la famille Windows Mixed Reality](images/mixed-reality-home-500px.png)

## <a name="moving-and-adjusting-apps"></a>Déplacement et ajustement d’applications

Sélectionnez **ajuster** dans la barre de l’application pour afficher les contrôles permettant de déplacer, de mettre à l’échelle et de faire pivoter le contenu de réalité mixte. Lorsque vous avez terminé, sélectionnez **terminé**.

![La ardoise du magasin en mode ajustement (cadre bleu). Remarque : la barre d’application (haut) a changé pour inclure les boutons « terminé » et « supprimer ».](images/adjust-500px.png)

Différentes applications peuvent avoir des options supplémentaires dans la barre des applications. Par exemple, Microsoft Edge possède des options de *défilement*, de *glisser-déplacer*et de *Zoom* . 

![Barre d’application pour les applications 2D s’exécutant sur HoloLens](images/holobar-500px.png)

Le bouton **précédent** permet de revenir aux écrans affichés précédemment dans l’application. Il s’arrête lorsque vous atteignez le début des expériences qui ont été affichées dans l’application et n’accède pas à d’autres applications.

## <a name="getting-around-your-home"></a>L’approche de votre foyer

Avec **HoloLens**, vous vous déplacez dans l’espace physique pour vous déplacer dans votre foyer.

Avec les **casques immersifs**, vous pouvez également vous familiariser avec vos PlaySpace pour vous déplacer dans une zone similaire dans le monde virtuel. Pour vous déplacer sur des distances plus longues, vous pouvez utiliser le stick analogique sur votre contrôleur pour « parcourir » virtuellement, ou vous pouvez utiliser la *téléportage* pour passer immédiatement plus de distances.

![Téléporting dans la page d’hébergement Windows Mixed Reality](images/teleportation-500px.png)

**Pour vous téléporter :**
1. Affichez le réticule de téléportation.
   * À l’aide de [contrôleurs de mouvement](motion-controllers.md): Appuyez sur le stick analogique et maintenez-le à cette position.
   * À l’aide d’un contrôleur Xbox : Appuyez sur le stick analogique gauche vers l’avant et maintenez-le à cette position.
   * À l’aide de la souris, cliquez avec le bouton droit sur le bouton de la souris (et utilisez la roulette de défilement pour faire pivoter la direction de votre choix lorsque vous vous reportez).
2. Placez le réticule là où vous souhaitez vous téléporter.
   * À l’aide de [contrôleurs de mouvement](motion-controllers.md): Inclinez le contrôleur (sur lequel vous conservez le stick analogique) pour déplacer le réticule.
   * À l’aide d’un contrôleur Xbox : utilisez votre point de [regard](gaze-and-commit.md) pour déplacer le réticule.
   * À l’aide d’une souris : déplacez votre souris pour déplacer le réticule.
3. Relâchez le bouton pour vous téléporter où le réticule a été placé.

**Pour « parcourir » virtuellement :**
* À l’aide de [contrôleurs de mouvement](motion-controllers.md): cliquez sur le stick analogique et maintenez-le enfoncé, puis déplacez le stick analogique dans le sens où vous souhaitez « parcourir ».
* À l’aide d’un contrôleur Xbox : cliquez sur le stick analogique gauche et maintenez-le enfoncé, puis déplacez le stick analogique dans le sens où vous souhaitez « parcourir ».

## <a name="immersive-headset-input-support"></a>Prise en charge des entrées du casque immersif

Les [casques immersifs Windows Mixed Reality](immersive-headset-hardware-details.md) prennent en charge plusieurs types d’entrée pour naviguer dans la page d’hébergement de la réalité mixte Windows. HoloLens ne prend pas en charge les entrées d’accessoire pour la navigation, car vous vous familiarisez physiquement avec votre environnement. Toutefois, HoloLens [prend en charge les entrées](hardware-accessories.md) pour l’interaction avec les applications.

### <a name="motion-controllers"></a>Contrôleurs de mouvement

La meilleure expérience Windows Mixed Reality sera avec les [contrôleurs de mouvement](motion-controllers.md) Windows Mixed Real qui prennent en charge le suivi de 6 degrés de liberté en utilisant uniquement les capteurs de votre casque-aucun appareil photo ou marqueur externe n’est nécessaire.

Commandes de navigation bientôt disponibles.

### <a name="gamepad"></a>Boîtier de commande
* **Stick analogique gauche :**
  * Appuyez sur le stick analogique gauche et maintenez-le enfoncé pour faire apparaître le réticule de [téléportation](navigating-the-windows-mixed-reality-home.md#getting-around-your-home) .
  * Appuyez sur le stick analogique à gauche, à droite ou à gauche pour déplacer les petits incréments vers la gauche, vers la droite ou vers l’arrière.
  * Cliquez sur le stick analogique gauche et maintenez-le enfoncé, puis déplacez le stick analogique dans le sens où vous souhaitez [virtuellement « parcourir ».](navigating-the-windows-mixed-reality-home.md#getting-around-your-home)
* Appuyez sur le **Stick à droite** vers la gauche ou vers la droite pour faire pivoter la direction que vous avez dirigée de 45 degrés.
* Le fait d’appuyer sur le bouton **a** effectue une opération SELECT et agit comme le mouvement [air TAP](gaze-and-commit.md#composite-gestures) .
* Le fait d’appuyer sur le bouton du **repère** permet d’ouvrir le [menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu) et agit comme [le geste.](system-gesture.md#bloom)
* Le fait d’appuyer sur les **déclencheurs de gauche et de droite** vous permet d’effectuer un zoom avant et arrière sur une application de bureau 2D avec laquelle vous interagissez à l’origine.

### <a name="keyboard-and-mouse"></a>Clavier et souris

**Remarque :** Utilisez la **touche Windows + Y** pour faire basculer la souris entre le Bureau de votre PC et la page d’hébergement Windows Mixed Reality.

Dans la page d’hébergement de Windows Mixed Reality :
* Le fait d’appuyer sur le bouton **gauche** de la souris permet d’effectuer une sélection et agit comme le mouvement d’appui sur l' [air](gaze-and-commit.md#composite-gestures) .
* En maintenant le bouton droit de la souris **, vous** Affichez le réticule de [téléportation](navigating-the-windows-mixed-reality-home.md#getting-around-your-home) .
* Le fait d’appuyer sur la touche **Windows** du clavier affiche le [menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu) et agit comme [le geste.](system-gesture.md#bloom)
* Quand vous [Gazing](gaze-and-commit.md) dans une application de bureau 2D, vous pouvez **Cliquer** avec le bouton droit pour sélectionner, **cliquer avec le bouton droit** pour afficher les menus contextuels et utiliser la **roulette de défilement** pour faire défiler (comme sur le Bureau de votre PC).

## <a name="cortana"></a>Cortana

[Cortana](voice-input.md#hey-cortana) est votre assistant personnel dans Windows Mixed Reality, tout comme sur les PC et les téléphones. HoloLens possède un microphone intégré, mais les casques immersifs peuvent nécessiter du matériel supplémentaire. Utilisez Cortana pour ouvrir des applications, redémarrer votre appareil, Rechercher des éléments en ligne et bien plus encore. Les développeurs peuvent également choisir d' [intégrer Cortana](https://dev.windows.com/cortana) dans leurs expériences.

Vous pouvez également utiliser des commandes vocales pour vous familiariser avec votre foyer. Par exemple, pointez sur un bouton (en utilisant du [regard](gaze-and-commit.md) ou un contrôleur, en fonction de l’appareil) et dites « sélectionner ». D’autres commandes vocales incluent « Go, », « large », « Small », « Close » et « me suis ».

## <a name="store-settings-and-system-apps"></a>Stocker, paramètres et applications système

Windows Mixed Reality possède un certain nombre d’applications intégrées, telles que :
* **Microsoft Store** pour accéder aux applications et aux Jeux
* **Hub de commentaires** pour envoyer des commentaires sur les applications système et système
* **Paramètres** pour configurer les paramètres système ([y compris la mise en réseau](connecting-to-wi-fi-on-hololens.md) et les mises à jour système)
* **Microsoft Edge** pour parcourir les sites Web
* **Photos** pour afficher et partager des photos et des vidéos
* **Étalonnage** (hololens uniquement) pour l’adaptation de l’expérience HoloLens à l’utilisateur actuel
* **Apprenez les gestes** (HoloLens) ou **Découvrez la réalité mixte** (casques immersifs) pour en savoir plus sur l’utilisation de votre appareil
* **visionneuse 3D** pour décorer votre monde avec du contenu de réalité mixte
* **Portail de réalité mixte** (Desktop) pour la configuration et la gestion de votre casque immersif et la diffusion en continu d’un aperçu instantané de votre vue dans le casque pour que d’autres utilisateurs puissent les voir.
* **Films et TV** pour visionner des vidéos 360 et les derniers films et émissions TV
* **Cortana** pour tous les besoins de votre assistant virtuel
* **Bureau** (casques immersifs) pour afficher votre moniteur de bureau dans un casque immersif
* **Explorateur de fichiers** Accéder aux fichiers et aux dossiers situés sur votre appareil

## <a name="see-also"></a>Voir aussi
* [Vues d’applications](app-views.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Accessoires matériels](hardware-accessories.md)
* [Considérations relatives à l’environnement pour HoloLens](environment-considerations-for-hololens.md)
* [Implémentation des lanceurs d’applications 3D](implementing-3d-app-launchers.md)
* [Création de modèles 3D à utiliser dans la page d’hébergement Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
