---
title: Navigation dans Windows Mixed Reality domestique
description: HoloLens et Windows Mixed Reality casques partagent un paradigme de lancement, la plaçant et la manipulation des applications et des modèles 3D dans votre environnement (qu’il soit physique ou numérique). Découvrez comment naviguer dans la réalité mixte Windows accueil sur les deux types d’appareils.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: interpréteur de commandes, du système d’exploitation, plate-forme, maison cliff, maison, accueil, environnement, Démarrer, menu Démarrer, menu Accueil, codes confidentiels, application, applications de lancement, placer des applications, teleport, déplacer, accédez
ms.openlocfilehash: 1ca6dd66506a64ad2e1c21870fee2725ddf20bd8
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597044"
---
# <a name="navigating-the-windows-mixed-reality-home"></a>Navigation dans Windows Mixed Reality domestique

Tout comme l’expérience de PC de Windows démarre avec le bureau, Windows Mixed Reality commence par la page d’accueil. Windows Mixed Reality accueil tire parti de notre capacité intégrée dès le départ pour comprendre et de parcourir les emplacements 3D. Avec HoloLens, votre page d’accueil est votre espace physique. Avec des casques IMMERSIFS, votre page d’accueil est virtuel.

Votre page d’accueil est également où vous utiliserez le menu Démarrer pour ouvrir et de placer les applications et le contenu. Vous pouvez remplir votre page d’accueil avec du contenu de la réalité mixte et plusieurs tâches à l’aide de plusieurs applications en même temps. Les éléments que vous placez dans votre page d’accueil resteront, même si vous redémarrez votre appareil.

## <a name="start-menu"></a>Menu Démarrer

![Menu Démarrer sur Microsoft HoloLens](images/start-500px.png)

Le menu Démarrer se compose de :
* Informations système (état du réseau, pourcentage de la batterie, heure actuelle et volume)
* Cortana (sur des casques IMMERSIFS, une vignette de début ; sur HoloLens, en haut du début)
* Applications épinglées
* Le bouton d’applications tout (signe plus)
* Boutons de photo et vidéo pour [mixte de capture de la réalité](mixed-reality-capture.md)

Basculez entre les applications épinglées et toutes les applications en sélectionnant le signe plus ou moins de boutons. Pour ouvrir le menu Démarrer sur HoloLens, utilisez le mouvement de bloom. Sur un casque immersif, appuyez sur le bouton Windows sur votre contrôleur.

## <a name="launching-apps"></a>Lancement des applications

Pour lancer une application, sélectionnez-le sur Démarrer. Le menu Démarrer disparaît, et l’application s’ouvre en mode de sélection élective, sous forme de fenêtre 2D ou un [modèle 3D](implementing-3d-app-launchers.md).

Pour exécuter l’application, vous devrez puis les placer dans votre page d’accueil :
1. Utilisez votre [les regards](gaze.md) ou contrôleur pour positionner l’application où vous le souhaitez. Elle s’ajuste automatiquement (en taille et position) pour se conformer à l’espace où vous le placez.
2. Placez l’application à l’aide d’appui (HoloLens) ou le bouton de sélection (des casques IMMERSIFS). Pour annuler et rétablir le menu Démarrer, utilisez le mouvement de bloom ou sur le bouton Windows.

[Applications 2D](building-2d-apps.md), créé pour le bureau, mobile, ou Xbox peut être modifié pour exécuter en tant qu’applications immersives de réalité mixte à l’aide de la [HolographicSpace API](https://msdn.microsoft.com/library/windows/apps/windows.graphics.holographic.holographicspace.aspx). Une application captivante dirige l’utilisateur en dehors de la page d’accueil et dans une expérience d’immersion. Les utilisateurs peuvent retourner d’accueil avec le mouvement de bloom (HoloLens) ou en appuyant sur le bouton Windows sur leur contrôleur (des casques IMMERSIFS).

Applications peuvent également être lancées via une API d’application vers ou via Cortana.

![Applications dans Windows Mixed Reality domestique](images/mixed-reality-home-500px.png)

## <a name="moving-and-adjusting-apps"></a>Déplacement et le réglage des applications

Sélectionnez **Adjust** sur l’application les contrôles de barre pour afficher ce déplacement, mise à l’échelle, et faire pivoter réalité un contenu mixte. Lorsque vous avez terminé, sélectionnez **fait**.

![La magasin de la séquence en Mode d’ajustement (frame bleu). Notez la barre d’application (du haut) a été modifié pour inclure 'Terminé' et 'Remove' boutons.](images/adjust-500px.png)

Différentes applications peuvent avoir des options supplémentaires dans la barre des applications. Par exemple, Microsoft Edge a *défilement*, *glisser*, et *Zoom* choix. 

![Barre de l’application pour les applications 2D en cours d’exécution sur HoloLens](images/holobar-500px.png)

Le **retour** bouton revient à écrans précédemment affichées dans l’application. Il s’arrête lorsque vous atteignez le début des expériences qui ont été affichés dans l’application et ne sera pas naviguer vers d’autres applications.

## <a name="getting-around-your-home"></a>Obtention de votre maison

Avec **HoloLens**, vous déplacez dans un espace physique pour vous déplacer dans votre page d’accueil.

Avec **des casques IMMERSIFS**, vous pouvez même être opérationnel et Parcourir dans votre playspace pour se déplacer dans une zone similaire dans le monde virtuel. Pour vous déplacer sur les longues distances, vous pouvez utiliser le stick analogique sur votre contrôleur pour pratiquement « Parcourir », ou vous pouvez utiliser *teleportation* pour accéder immédiatement les longues distances.

![Téléportation dans Windows Mixed Reality domestique](images/teleportation-500px.png)

**Pour teleport :**
1. Afficher la réticule téléportation.
   * À l’aide de [contrôleurs de mouvement](motion-controllers.md): appuyez sur le stick analogique avant celle-ci et maintenez-la enfoncée dans cette position.
   * À l’aide d’une manette Xbox : appuyez sur le stick analogique gauche avant celle-ci et maintenez-la enfoncée dans cette position.
   * À l’aide de la souris : maintenez le bouton de la souris avec le bouton droit (et utiliser la roulette de défilement pour faire pivoter la direction que vous souhaitez faire face lorsque vous teleport).
2. Placer la réticule dans lequel vous souhaitez teleport.
   * À l’aide de [contrôleurs de mouvement](motion-controllers.md): pivoter vers le contrôleur (sur lequel vous êtes maintenant le stick analogique vers l’avant) pour déplacer la réticule.
   * À l’aide d’une manette Xbox : utiliser votre [les regards](gaze.md) pour déplacer la réticule.
   * À l’aide de la souris : déplacez votre souris pour déplacer la réticule.
3. Relâchez le bouton pour teleport où la réticule a été placée.

**Pour pratiquement « remonter : »**
* À l’aide de [contrôleurs de mouvement](motion-controllers.md): cliquez sur le stick analogique et maintenir, puis déplacez le stick analogique dans la direction que vous souhaitez « remonter ».
* À l’aide d’une manette Xbox : cliquez sur le stick analogique gauche et le blocage, puis déplacez le stick analogique dans la direction que vous souhaitez « remonter ».

## <a name="immersive-headset-input-support"></a>Prise en charge d’entrée de casque immersives

[Des casques IMMERSIFS Windows Mixed Reality](immersive-headset-hardware-details.md) prennent en charge plusieurs types d’entrée pour naviguer dans la réalité mixte Windows domestique. HoloLens ne prend pas en charge les entrées accessoires pour la navigation, car vous partez physiquement et que vous consultez votre environnement. Cependant, n’est HoloLens [prennent en charge les entrées](hardware-accessories.md) permettant d’interagir avec les applications.

### <a name="motion-controllers"></a>Contrôleurs de mouvement

La meilleure expérience de réalité mixte Windows sera avec Windows Mixed Reality [contrôleurs de mouvement](motion-controllers.md) ce suivi de 6 degrés de liberté de prise en charge à l’aide de simplement les capteurs dans votre casque - aucun caméras externes ou marqueurs de requis !

Commandes de navigation sera bientôt disponible.

### <a name="gamepad"></a>Boîtier de commande
* **Stick analogique gauche :**
  * Maintenez le stick analogique gauche vers l’avant pour faire apparaître le [teleportation](navigating-the-windows-mixed-reality-home.md#getting-around-your-home) réticule.
  * Appuyez sur le stick analogique gauche, droite, sauvegarder à déplacer vers la gauche, droite ou sauvegarder par petits incréments.
  * Cliquez sur le stick analogique gauche et le blocage, puis déplacez le stick analogique dans la direction que vous souhaitez [pratiquement « Parcourir ».](navigating-the-windows-mixed-reality-home.md#getting-around-your-home)
* Appuyez sur la **stick analogique droit** gauche ou droite pour faire pivoter la direction que vous rencontrez de 45 degrés.
* En appuyant sur la **A** bouton exécute une instruction select et agit comme le [appui en l’air](gestures.md#air-tap) mouvement.
* En appuyant sur la **Guide** bouton permet d’afficher le [menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu) et agit comme le [bloom](gestures.md#bloom) mouvement.
* En appuyant sur la **gauche et droit des déclencheurs** permet d’effectuer un zoom avant vers et depuis une application de bureau 2D, vous interagissez avec dans la page d’accueil.

### <a name="keyboard-and-mouse"></a>Clavier et souris

**Remarque :** Utilisez **les touche Windows + Y** pour basculer de la souris entre le contrôle de bureau de votre PC et Windows Mixed Reality domestique.

Dans le Windows Mixed Reality domestique :
* En appuyant sur la **clic gauche** bouton de la souris effectue une opération select et agit comme le [appui en l’air](gestures.md#air-tap) mouvement.
* Contenant le **avec le bouton droit** bouton de la souris fait apparaître le [teleportation](navigating-the-windows-mixed-reality-home.md#getting-around-your-home) réticule.
* En appuyant sur la **Windows** touche du clavier fait apparaître la [Menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu) et agit comme le [bloom](gestures.md#bloom) mouvement.
* Lorsque [gazing](gaze.md) à une application de bureau 2D, vous pouvez **clic gauche** pour sélectionner, **avec le bouton droit** pour faire apparaître les menus contextuels, utilisez le **roulette de défilement** Scroll (comme sur le bureau de votre PC).

## <a name="cortana"></a>Cortana

[Cortana](voice-input.md#hey-cortana) est votre assistant personnel en réalité mixte Windows, tout comme sur l’ordinateur et téléphone. HoloLens a un microphone intégré, mais des casques IMMERSIFS peuvent nécessiter du matériel supplémentaire. Utiliser Cortana pour ouvrir des applications, de redémarrer votre appareil, de rechercher les éléments en ligne et bien plus encore. Les développeurs peuvent également choisir de [intégrer Cortana](https://dev.windows.com/cortana) dans leurs expériences.

Vous pouvez également utiliser les commandes vocales pour obtenir votre maison. Par exemple, pointer sur un bouton (à l’aide de [les regards](gaze.md) ou un contrôleur, en fonction de l’appareil) et dire « Select ». Autres commandes vocales incluent « Go home, » « Supérieure », « plus petits, » « Fermer » et « Doivent faire Face me. »

## <a name="store-settings-and-system-apps"></a>Applications de Store, les paramètres et système

Réalité mixte Windows possède un nombre d’applications intégrées, telles que :
* **Microsoft Store** pour obtenir des applications et des jeux
* **Hub de commentaires** pour envoyer vos commentaires sur le système et les applications du système
* **Paramètres** pour configurer les paramètres système ([y compris les réseaux](connecting-to-wi-fi-on-hololens.md) et mises à jour du système)
* **Microsoft Edge** pour parcourir des sites Web
* **Photos** pour afficher et partager des photos et vidéos
* **Étalonnage** (HoloLens uniquement) pour ajuster l’expérience de HoloLens à l’utilisateur actuel
* **Découvrez les mouvements** (HoloLens) ou **Découvrez la réalité mixte** (des casques IMMERSIFS) pour en savoir plus sur l’utilisation de votre appareil
* **Visionneuse 3D** pour décorer votre monde avec le contenu de la réalité mixte
* **Mixte réalité portail** (bureau) pour la configuration et la gestion de votre casque immersive et diffusion en continu d’un aperçu instantané de l’affichage dans le casque pour d’autres utilisateurs peuvent voir.
* **Vidéos et TV** pour l’affichage des 360 vidéos et dernières vidéos et tv montre
* **Cortana** pour l’ensemble de votre assistant virtuel a besoin
* **Bureau** (des casques IMMERSIFS) pour l’affichage de votre moniteur du bureau dans un casque immersif
* **Explorateur de fichiers** accéder aux fichiers et dossiers situés sur votre appareil

## <a name="see-also"></a>Voir aussi
* [Vues de l’application](app-views.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Accessoires de matériel](hardware-accessories.md)
* [Considérations sur l’environnement pour HoloLens](environment-considerations-for-hololens.md)
* [Implémentation des lanceurs d’applications 3D.](implementing-3d-app-launchers.md)
* [Création de modèles 3D pour une utilisation dans la page d’accueil Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
