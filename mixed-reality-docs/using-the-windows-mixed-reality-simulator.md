---
title: Utilisation du simulateur Windows Mixed Reality
description: Le simulateur Windows Mixed Reality vous permet de tester des applications de réalité mixte sur votre ordinateur sans un casque Windows Mixed realisation immersif.
author: pbarnettms
ms.author: pbarnett
ms.date: 04/25/2019
ms.topic: article
keywords: Windows Mixed Reality, simulateur, test
ms.openlocfilehash: a7cbd5b5ca1c0ed0e4f81715d337d5eec68117f0
ms.sourcegitcommit: f5c1dedb3b9e29f27f627025b9e7613931a7ce18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64580700"
---
# <a name="using-the-windows-mixed-reality-simulator"></a>Utilisation du simulateur Windows Mixed Reality

Le simulateur Windows Mixed Reality vous permet de tester des applications de réalité mixte sur votre ordinateur sans un casque Windows Mixed realisation immersif. Il est disponible à partir de la mise à jour Windows 10 Creators Update. Le simulateur est semblable à l' [émulateur HoloLens](using-the-hololens-emulator.md), bien que le simulateur n’utilise pas de machine virtuelle. Les applications qui s’exécutent dans le simulateur s’exécutent dans votre session utilisateur Windows 10 Desktop, comme si vous utilisiez un casque immersif. Les entrées humaines et environnementales qui seraient généralement lues par les capteurs sur un casque immersif sont à la place simulées à l’aide de votre clavier, de votre souris ou de votre contrôleur Xbox. Les applications n’ont pas besoin d’être modifiées pour s’exécuter dans le simulateur, et elles ne savent pas qu’elles ne s’exécutent pas sur un casque immersif.

## <a name="enabling-the-windows-mixed-reality-simulator"></a>Activation du simulateur Windows Mixed Reality

1. **Activer le mode développeur** à partir des paramètres-mise à jour > et sécurité-> pour les développeurs
2. Lancer le **portail de réalité mixte** à partir du Bureau
3. S’il s’agit de la première fois que vous lancez le portail, vous devez suivre le processus d’installation
   1. Cliquez sur **prise en main**
   2. Cliquez sur **J’accepte** pour accepter le contrat
   3. Cliquez sur **configurer pour la simulation (pour les développeurs)** pour procéder à l’installation sans appareil physique
   4. Cliquez sur **configurer** pour confirmer votre choix
4. Cliquez sur le bouton **pour les développeurs** sur le côté gauche du portail de réalité mixte
5. Activer le basculement de la simulation **sur activé**
   * L’activation de la simulation installe et active le contrôleur 6-DDL simulé à gauche par défaut.  Avant la mise à jour de Windows 10 mai 2019, l’installation d’un contrôleur 6-DDL simulé nécessite des autorisations d’administrateur.  Vous devez accepter la boîte de dialogue contrôle de compte d’utilisateur si elle s’affiche.

Vous devez maintenant être en cours d’exécution avec la simulation!

## <a name="deploying-apps-to-the-mixed-reality-simulator"></a>Déploiement d’applications dans le simulateur de réalité mixte

Étant donné que le simulateur s’exécute sur votre ordinateur local sans ordinateur virtuel, vous pouvez simplement déployer vos applications Windows universelles sur l' **ordinateur local** lors du débogage.

## <a name="basic-simulator-input"></a>Entrée du simulateur de base

Le contrôle du simulateur est très similaire à de nombreux jeux vidéo en 3D courants et à l' [émulateur HoloLens](using-the-hololens-emulator.md). Les options d’entrée sont disponibles par le biais du clavier, de la souris ou d’une manette Xbox.

Vous contrôlez le simulateur en dirigeant les actions d’un utilisateur simulé qui porte un casque immersif. Vos actions déplacent l’utilisateur simulé et entraînent des interactions avec les applications qui répondent comme elles le feraient sur un casque immersif.
* **Marcher vers l’avant, l’arrière, la gauche et la droite** : utilisez les touches W, A, S et D du clavier, ou le stick gauche d’une manette Xbox.
* **Regarder vers le haut, le bas, la gauche et la droite** : cliquez et faites glisser la souris, utilisez les touches de direction du clavier ou utilisez le stick droit d’une manette Xbox.
* **Bouton d’action Appuyez** sur le contrôleur-cliquez avec le bouton droit sur la souris, appuyez sur la touche entrée de votre clavier ou utilisez le bouton A sur un contrôleur Xbox.
* **Appuyez sur le bouton de démarrage du contrôleur** -Appuyez sur la touche Windows ou F2 de votre clavier, ou appuyez sur le bouton B sur un contrôleur Xbox.
* **Déplacement du contrôleur pour le défilement** : maintenez la touche Alt enfoncée, maintenez le bouton droit de la souris enfoncé, faites glisser la souris vers le haut ou vers le haut, ou dans un contrôleur Xbox, maintenez le déclencheur droit et un bouton enfoncé et déplacez le levier droit vers le haut et le haut.

## <a name="tracked-controllers"></a>Contrôleurs suivis

Le simulateur de réalité mixte peut simuler jusqu’à deux contrôleurs de mouvement suivis. Activez-les à l’aide des commutateurs bascule dans le portail de la réalité mixte. Chaque contrôleur simulé a:
* Position et orientation dans l’espace
* Bouton Accueil
* Bouton Menu
* Bouton de poignée
* Pavé tactile
* Stick
* Niveau de la batterie

## <a name="see-also"></a>Voir aussi
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Entrée de simulateur de réalité mixte avancée](advanced-hololens-emulator-and-mixed-reality-simulator-input.md)
* [Mappage spatial dans Unity](spatial-mapping-in-unity.md)
* [Mappage spatial dans DirectX](spatial-mapping-in-directx.md)
