---
title: L’utilisation du simulateur Windows Mixed Reality
description: Le simulateur Windows Mixed Reality vous permet de tester des applications de réalité mixte sur votre PC sans un casque immersif Windows Mixed Reality.
author: JonMLyons
ms.author: jlyons
ms.date: 03/21/2018
ms.topic: article
keywords: Windows mixte réalité, le simulateur, test
ms.openlocfilehash: 782cab85f163edd2afc4251210b7596c73dcc8b8
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596335"
---
# <a name="using-the-windows-mixed-reality-simulator"></a>L’utilisation du simulateur Windows Mixed Reality

Le simulateur Windows Mixed Reality vous permet de tester des applications de réalité mixte sur votre PC sans un casque immersif Windows Mixed Reality. Il est disponible à compter de Windows 10 Creators Update. Le simulateur est similaire à la [HoloLens émulateur](using-the-hololens-emulator.md), bien que le simulateur n’utilise pas d’une machine virtuelle. Applications qui s’exécutent dans le simulateur s’exécuter dans votre session d’utilisateur du bureau Windows 10, tout comme il le ferait si vous utilisiez un casque immersif. L’entrée humaine et l’environnement qui serait généralement être lues par les capteurs sur un casque immersif sont simulés à la place à l’aide de votre clavier, souris ou manette Xbox. Les applications ne doivent être modifiés pour s’exécuter dans le simulateur et ne sais pas qu’ils ne sont pas en cours d’exécution sur un casque immersif.

## <a name="enabling-the-windows-mixed-reality-simulator"></a>Activer le simulateur Windows Mixed Reality

1. **Activer le mode développeur** à partir des paramètres -> mise à jour et de sécurité -> pour les développeurs
2. Lancer le **Portal de réalité mixte** à partir du bureau
3. S’il s’agit de lancer le portail pour la première fois, vous devez passer par l’expérience d’installation
   1. Cliquez sur **prise en main**
   2. Cliquez sur **J’accepte** d’accepter le contrat
   3. Cliquez sur **défini pour la simulation (pour les développeurs)** poursuivre le programme d’installation sans un appareil physique
   4. Cliquez sur **configurer** pour confirmer votre choix
4. Cliquez sur le **pour les développeurs** bouton sur le côté gauche du portail de réalité mixte
5. Activer le bouton bascule Simulation **sur**
   * Cela nécessite des autorisations d’administrateur et vous devez accepter la boîte de dialogue contrôle de compte d’utilisateur qui s’affiche

Vous devez maintenant exécuter avec simulation !

## <a name="deploying-apps-to-the-mixed-reality-simulator"></a>Déploiement d’applications sur le simulateur de réalité mixte

Étant donné que le simulateur s’exécute sur votre ordinateur local sans une Machine virtuelle, vous pouvez simplement déployer vos applications Windows universelles à le **ordinateur Local** lors du débogage.

## <a name="basic-simulator-input"></a>Entrée de simulateur de base

Contrôle le simulateur est très similaire à de nombreux de jeux vidéo 3D courants et la [HoloLens émulateur](using-the-hololens-emulator.md). Options d’entrée sont disponibles à l’aide du clavier, souris ou manette Xbox.

Vous contrôlez le simulateur en dirigeant les actions d’un utilisateur simulé a porter un casque immersif. Vos actions passer l’utilisateur simulé, entraînant des interactions avec les applications qui réagissent comme ils le feraient sur un casque immersif.
* **Remonter vers l’avant, arrière, gauche et avec le bouton droit** -utiliser le W, A, S et D clés sur votre clavier ou la clé gauche sur une manette Xbox.
* **Rechercher, vers le bas, gauche et avec le bouton droit** -cliquez et faites glisser la souris, utilisez les touches de direction sur votre clavier ou la clé droite sur une manette Xbox.
* **Appuyez sur le bouton action sur le contrôleur** - avec le bouton droit de la souris, appuyez sur la touche entrée de votre clavier ou utilisez le bouton A sur un contrôleur Xbox.
* **Appuyez sur le bouton sur le contrôleur d’accueil** : appuyez sur la clé de Windows ou la touche F2 du clavier, ou appuyez sur le bouton B sur une manette Xbox.
* **Déplacement de contrôleur pour le défilement** : maintenez la touche Alt enfoncée, maintenez le bouton droit de la souris et faites glisser la souris haut / bas, ou dans une manette Xbox maintenez le déclencheur de droite et un bouton et la clé droite haut et bas.

## <a name="tracked-controllers"></a>Contrôleurs de suivis

Le simulateur de réalité mixte permet de simuler jusqu'à deux contrôleurs de mouvement suivies à main. Activer l’utilisation des commutateurs bascule dans le portail de réalité mixte. Chaque contrôleur simulé a :
* Position dans l’espace
* Bouton Accueil
* Bouton Menu
* Bouton de la poignée
* Pavé tactile

## <a name="see-also"></a>Voir aussi
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Avancées d’entrée de simulateur de réalité mixte](advanced-hololens-emulator-and-mixed-reality-simulator-input.md)
* [Mappage spatial dans Unity](spatial-mapping-in-unity.md)
* [Mappage spatial dans DirectX](spatial-mapping-in-directx.md)
