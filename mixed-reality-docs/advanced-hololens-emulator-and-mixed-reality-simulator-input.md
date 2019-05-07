---
title: Entrée avancée d’émulateur de HoloLens et simulateur de réalité mixte
description: Obtenir des instructions détaillées pour l’utilisation du clavier, la souris et la manette Xbox pour simuler l’entrée pour le simulateur de l’émulateur de HoloLens et Windows Mixed Reality.
author: pbarnettms
ms.author: pbarnett
ms.date: 04/26/2019
ms.topic: article
keywords: HoloLens, émulateur, Simulation, Windows Mixed Reality
ms.openlocfilehash: 6ea493d8c1269ff0bea1d4102b9e224e30d06aef
ms.sourcegitcommit: f5c1dedb3b9e29f27f627025b9e7613931a7ce18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64580590"
---
# <a name="advanced-hololens-emulator-and-mixed-reality-simulator-input"></a>Entrée avancée d’émulateur de HoloLens et simulateur de réalité mixte

La plupart des utilisateurs de l’émulateur devrez utiliser les contrôles d’entrée de base pour le [HoloLens émulateur](using-the-hololens-emulator.md#basic-emulator-input) ou [simulateur de réalité mixte Windows](using-the-windows-mixed-reality-simulator.md#basic-simulator-input). Les détails ci-dessous sont pour les utilisateurs expérimentés qui ont trouvé un besoin pour simuler des types plus complexes d’entrée.


## <a name="concepts"></a>Concepts

Pour commencer à contrôler les entrées virtuelle pour le simulateur de l’émulateur de HoloLens et Windows Mixed Reality, vous devez d’abord comprendre quelques concepts.

Mouvement fait référence au contrôle et la modification de la position et l’orientation d’un élément dans la scène. Pour un objet contrôlable ciblé, le mouvement est contrôlé avec une rotation et de translation (déplacement) le long des trois axes.
* **Lacet**: Activez la gauche ou vers la droite.
* **Pitch**: Activer le haut ou vers le bas.
* **ROULEAU**: Déploiement côte à côte.
* **X**: Déplacer à gauche ou droite.
* **Y**: Faire monter ou Descendre.
* **Z**: Déplacer vers l’avant ou vers l’arrière.

[Mouvement](gestures.md) et de l’entrée de contrôleur de mouvement sont mappées étroitement à la manière dont ils périphériques physiques :
* **Action**: Cela simule l’action d’en appuyant sur l’index pour le curseur ou en les extrayant le bouton d’action sur un contrôleur. Par exemple, l’entrée d’Action peut être utilisée pour simuler le mouvement d’appui en l’air, pour faire défiler le contenu et à appuyer et maintenir.
* **[Bloom](gestures.md#bloom)mouvement de /System ou accueil**: Le mouvement de bloom/système HoloLens ou un bouton d’accueil d’un contrôleur est utilisé pour retourner à l’environnement et pour effectuer des actions du système.

Mains ont une riche reprresentation dans HoloLens 2.  En plus d’être suivies/non et non suivies utilisables pour les mouvements de conduite, mains sont maintenant un modèle squelette articulé ajuster à leur et exposée au développeur.  Cela introduit 26 points suivies sur chaque aiguille.  
* **Mixte**: L’une des vingt positions suivies pour chaque cas suivies. Cela aura un point est associé un espace 3d.
* **Poser**: Une collection complète de tous les articulations dans une main suivie. À ce stade, il s’agit d’une collection de 26 Joints. 

À ce stade, nous n’exposent pas un contrôle direct de chaque position commune individuellement via l’interface utilisateur de l’émulateur, bien que vous pouvez les définir via l’API de simulation. Au lieu de cela, nous avons un ensemble d’utile risque de poser représentatif l’émulateur vous permet de basculer entre.

Vous pouvez également contrôler l’état de l’entrée de capteur simulées :
* **Réinitialiser**: Ceci renverra tous les capteurs simulés à leurs valeurs par défaut.  À partir de l’émulateur de 2 HoloLens, une réinitialisation peut être limitée à un ou deux mains en effectuant le hand(s) souhaité à l’aide de l’ou les clés de modificateur appropriée ou l’ou les boutons (gauche et/ou Alt de droite ou gauche et/ou droit pare-chocs du boîtier de commande).
* **Suivi des**: Parcourt les modes de suivi positionnels. Cela comprend les éléments suivants :
  * **Par défaut** : Le système d’exploitation choisit le mode de suivi des meilleures basé sur les demandes du système.
   * **Orientation**: Force l’Orientation uniquement le suivi, quel que soit les demandes du système.
   * **Positionnels**: Force positionnels le suivi, quelle que soit les demandes du système.

## <a name="types-of-input"></a>Types d’entrées

Le tableau suivant montre comment chaque type de d’entrée est mappé au clavier, de la souris et de la manette Xbox. Chaque type a un mappage différent selon le mode de contrôle d’entrée ; plus d’informations sur les modes de contrôle d’entrée sont fournies plus loin dans ce document.

|  |  Clavier |  Souris |  Contrôleur Xbox | 
|----------|----------|----------|----------|
|  Lacet |  Flèches gauche / droite |  Faites glisser gauche / droite |  Stick analogique droit gauche / droite | 
|  Inclinaison |  Haut / bas flèches |  Faites glisser le haut / bas |  Stick analogique droit haut / bas | 
|  Annuler |  Q / E |  |  DPad gauche / droite | 
|  X |  A / D |  |  Stick analogique gauche gauche / droite | 
|  Y |  Page vers le haut / bas de page |  |  DPad haut / bas | 
|  Z |  W / S |  |  Stick analogique gauche, haut / bas | 
|  Action |  Entrez ou espace |  Bouton de droite |  Un bouton ou un déclencheur | 
|  Bloom/système |  Touche F2 ou Windows |  |  Bouton B | 
|  Bouton de poignée de contrôleur |  G  |  |  | 
|  Bouton de menu de contrôleur |  M  |  |  | 
|  Touch pavé tactile de contrôleur |  U  |  |  | 
|  Appuyez sur le pavé tactile contrôleur |  P  |  |  | 
|  Appuyez sur le stick analogique contrôleur |  K  |  |  | 
|  Suivi de l’état de contrôleur de gauche |  F9 |  |  | 
|  Suivi de l’état de contrôleur de droite |  F10 |  |  | 
|  Pose « Fermer » de main | 7 |  |  |
|  Remettez Pose « Open » (valeur par défaut) | 8 |  |  |
|  Main 'Point' Pose | 9 |  |  |
|  Pose de « Pincement » disponible | 0 |  |  |
|  Réinitialiser |  Touche ÉCHAP |  |  bouton Démarrer | 
|  Suivi |  T ou F3 |  |  Bouton X | 


Remarque: Les boutons de contrôleur peuvent être adressé à une seule main/contrôleur ou l’autre à l’aide de l’aiguille de ciblage des modificateurs.

## <a name="targeting"></a>Ciblage 

Certains des concepts d’entrée ci-dessus, mettez au point leurs propres.  Action, de Bloom/système, de réinitialisation et de suivi sont des concepts complètes n’est pas nécessaire et ne sont pas affectés par n’importe quel modificateur supplémentaires pour le ciblage.  Toutefois, les concepts restants peuvent être appliquées à une de plusieurs cibles. Nous avons introduit les méthodes vous permettent de spécifier qui cible à que votre commande doit être appliqué.  Dans tous les cas, il est possible de spécifier via l’interface utilisateur ou via les appuis de clavier, objet targtet.  Dans certains cas, il est également possible de spécifier directement avec le contrôleur de la xbox. 

Le tableau suivant décrivent les options de ciblage et la façon d’activer chacun d’eux.

| Objet | Touche de modification | Modificateur de contrôleur | Modificateur de l’interface utilisateur d’émulateur |
|----------|----------|----------|----------|
| Corps | (par défaut) | (par défaut) | (par défaut) |
| head | Blocage H | (Non disponible) | (Non disponible) |
| Main gauche/contrôleur | Maintenez le bouton de Alt gauche | Maintenez le bouton de l’épaule gauche | Gauche punaise | 
| Droite/contrôleur | Maintenez la touche Alt de droite | Maintenez le bouton de droite épaule | Droite punaise |
| Yeux | Attente Y | (Non disponible) | Yeux punaise |
  
Le tableau suivant montre comment chaque modificateur cible est mappé à chacun des mouvements d’entrée certains concepts fondamentaux

|  | Par défaut (corps) |  Main/contrôleur (maintenez la touche Alt, bouton de blocage gamepad épaule ou activer/désactiver l’interface utilisateur punaise) |  Head (maintenez H)  |  Yeux (punaise Y contenir ou activer/désactiver l’interface utilisateur) |
|----------|----------|----------|----------|
|  Lacet |  Corps de la main gauche / droite |  Déplacer la main gauche / droite |  Activer la tête gauche / droite | Les regards yeux recherche gauche/droite |
|  Inclinaison |  Activer la tête haut / bas |  Main haut / bas |  Activer la tête haut / bas | Les regards yeux recherche haut/bas | 
|  Annuler |  Rouleau de tête gauche / droite |  |  Rouleau de tête gauche / droite | (Aucune action) |
|  X |  Corps de la diapositive gauche / droite |  Déplacer/contrôleur de la main gauche / droite |  Activer la tête gauche / droite | (Aucune Action) |
|  Y |  Déplacer des corps haut / bas |  Déplacer la main/contrôleur haut / bas |  Activer la tête haut / bas | (Aucune Action) |
|  Z |  Déplacer vers l’avant / arrière de corps |  Déplacer vers l’avant / arrière main/de contrôleur. |  Activer la tête haut / bas | (Aucune Action) |
 
 
## <a name="controlling-an-app"></a>Contrôle d’une application

L’ensemble de contrôles suivant est suggéré pour une utilisation quotidienne :

|  Opération |  Clavier et souris |  Contrôleur | 
|----------|----------|----------|
|  Corps X |  A / D |  Stick analogique gauche gauche / droite | 
|  Corps Y |  Page vers le haut / bas de page |  DPad haut / bas | 
|  Corps Z |  W / S |  Stick analogique gauche, haut / bas | 
|  Corps lacet |  Faites glisser la souris gauche / droite |  Stick analogique droit gauche / droite | 
|  Head lacet |  H + faire glisser la souris gauche / droite |  H (sur le clavier) + stick analogique droit gauche / droite | 
|  Hauteur de la tête |  Faites glisser la souris haut / bas |  Stick analogique droit haut / bas | 
|  Rouleau de tête |  Q / E |  DPad gauche / droite | 
|  Main/contrôleur X |  ALT + A / D |  Épaule + stick analogique gauche gauche / droite | 
|  Main/contrôleur Y |  ALT + PG. préc / Pg |  Épaule + DPad haut / bas | 
|  Main/contrôleur Z |  ALT + W / S |  Épaule + stick analogique gauche, haut / bas | 
|  Main/contrôleur lacet |  Alt + faire glisser la souris gauche / droite |  Épaule + stick analogique droit gauche / droite | 
|  Main/contrôleur tangage |  Alt + faire glisser la souris haut / bas |  Épaule + stick analogique droit haut / bas | 
|  Rouleau de main/contrôleur |  ALT + Q / E |  Épaule + DPad gauche / droite | 
|  Action |  Bouton droit de la souris |  déclencheur | 
|  Bloom / système / Home |  Touche F2 ou Windows |  Bouton B | 
|  Réinitialiser |  Échappement |  bouton Démarrer | 
|  Suivi |  T |  Bouton X | 
|  Défilement |  ALT + flèche droite bouton de souris + faire glisser la souris haut / bas |  Épaule + déclencheur + stick analogique droit haut / bas | 
|  Déplacement/faire tourner plus rapidement | Touche MAJ de gauche ou droite | Maintenez la touche et le stick analogique droit |
|  Déplacement/faire pivoter lente | Touche Ctrl de gauche ou droite | Maintenez la touche et le stick analogique gauche |

## <a name="perception-simulation-control-panel-keyboard-shortcuts"></a>Raccourcis de clavier perception Simulation le panneau de configuration

Les raccourcis clavier suivants sont disponibles pour accéder au panneau Perception Simulation et l’activation ou désactivation périphériques d’entrée de PC pour les utilisent avec simulation.

| Opération | Raccourci | Description/Remarques |
|-----------|----------|-------------|
| Activer/désactiver « Utiliser le clavier pour la simulation » | F4 | Mise hors tension, l’entrée de clavier va à l’application HoloLens ou Windows Mixed Reality. |
| Activer/désactiver « Utiliser la souris pour la simulation » | F5 | Mise hors tension, l’entrée de la souris va à l’environnement de réalité mixte (Windows Mixed Reality uniquement) |
| Activer/désactiver « Utiliser gamepad de simulation » | F6 | Mise hors tension, gamepad entrée est ignorée par simulation |
| Afficher ou masquer le panneau de configuration | F7 | |
| Définir le focus clavier au panneau de commande | F8 | Si le panneau n’est pas actuellement visible il est affiché en premier. |
| Attacher ou détacher le panneau vers/à partir de l’émulateur ou de la fenêtre du portail de réalité mixte | F9 | Si la fenêtre est fermée lorsque flottant, il est ancré et masqué. |

## <a name="see-also"></a>Voir aussi
* [Installer les outils](install-the-tools.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Utilisation du simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md)
