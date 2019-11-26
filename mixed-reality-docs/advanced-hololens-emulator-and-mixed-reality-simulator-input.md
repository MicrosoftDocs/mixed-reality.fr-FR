---
title: Entrée de l’émulateur HoloLens avancé et du simulateur de réalité mixte
description: Instructions détaillées pour l’utilisation du clavier, de la souris et du contrôleur Xbox pour simuler l’entrée pour l’émulateur HoloLens et le simulateur Windows Mixed Reality.
author: pbarnettms
ms.author: pbarnett
ms.date: 04/26/2019
ms.topic: article
keywords: HoloLens, émulateur, simulation, Windows Mixed Reality
ms.openlocfilehash: c5601ae2caf235cb22248ce7c6bf7e29225ade2c
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926596"
---
# <a name="advanced-hololens-emulator-and-mixed-reality-simulator-input"></a>Entrée de l’émulateur HoloLens avancé et du simulateur de réalité mixte

La plupart des utilisateurs de l’émulateur auront uniquement besoin d’utiliser les contrôles d’entrée de base pour l' [émulateur HoloLens](using-the-hololens-emulator.md#basic-emulator-input) ou le [simulateur de réalité mixte Windows](using-the-windows-mixed-reality-simulator.md#basic-simulator-input). Les informations ci-dessous sont destinées aux utilisateurs expérimentés qui ont trouvé besoin de simuler des types d’entrée plus complexes.


## <a name="concepts"></a>Concepts

Pour commencer à contrôler l’entrée virtuelle dans l’émulateur HoloLens et le simulateur Windows Mixed Reality, vous devez d’abord comprendre quelques concepts.

Motion fait référence au contrôle et à la modification de la position et de l’orientation d’un événement dans la scène. Pour un objet contrôlable ciblé, motion est contrôlé avec la rotation et la translation (mouvement) sur trois axes.
* **Lacet**: tournez à gauche ou à droite.
* Pas de **hauteur**: activer ou désactiver.
* **Roll**: Roll-to-Side.
* **X**: déplacer vers la gauche ou vers la droite.
* **Y**: monter ou descendre.
* **Z**: déplacer vers l’avant ou vers l’arrière.

Les entrées de contrôleur de mouvement et de mouvement sont mappées de près à la façon dont elles sont les appareils physiques :
* **Action**: cela simule l’action d’appuyer sur le index sur le curseur ou d’extraire le bouton d’action d’un contrôleur. Par exemple, l’entrée d’action peut être utilisée pour simuler le mouvement d’appui sur l’air, pour faire défiler le contenu et pour appuyer et maintenir.
* **[](system-gesture.md#bloom)Geste ou page d’habitation/** : le geste de système et de réseau HoloLens ou le bouton d’hébergement d’un contrôleur est utilisé pour retourner à l’interpréteur de commandes et effectuer des actions système.

Les mains ont une représentation riche dans HoloLens 2.  En plus de faire l’objet d’un suivi/non suivi, et d’être utilisable pour la conduite de mouvements, les mains disposent désormais d’un modèle de squelette articulé qui leur est adapté et exposé au développeur.  Cela présente 26 points suivis sur chaque main.  
* **Joint**: l’un des vingt positions suivies pour une main donnée. Un point est alors associé à l’espace 3D.
* **Pose**: collection complète de tous les joints dans une main. À ce stade, il s’agit d’une collection de 26 jointures. 

À ce stade, nous n’exposent pas le contrôle direct de chaque position conjointe individuellement par le biais de l’interface utilisateur de l’émulateur, même si vous pouvez les définir via l’API de simulation. Au lieu de cela, nous disposons d’un ensemble de jeux représentatifs utiles que l’émulateur vous permet de basculer entre.

Vous pouvez également contrôler l’état de l’entrée de capteur simulé :
* **Réinitialisation**: tous les capteurs simulés sont retournés à leurs valeurs par défaut.  À partir de l’émulateur HoloLens 2, une réinitialisation peut être étendue à l’un ou aux deux mains en faisant passer la ou les mains souhaitées à l’aide de la ou des touches de modification appropriées ou des boutons (gauche et/ou droit Alt, ou de gauche et/ou de droite sur le boîtier de sélection).
* **Suivi**: parcourt les modes de suivi positionnel. Cela comprend les éléments suivants :
  * **Valeur par défaut**: le système d’exploitation choisit le mode de suivi le plus approprié en fonction des demandes effectuées sur le système.
   * **Orientation**: force le suivi de l’orientation uniquement, quelles que soient les demandes effectuées sur le système.
   * **Positional**: force le suivi positionnel, quelles que soient les demandes effectuées sur le système.

## <a name="types-of-input"></a>Types d’entrée

Le tableau suivant montre comment chaque type d’entrée est mappé au clavier, à la souris et au contrôleur Xbox. Chaque type a un mappage différent selon le mode de contrôle d’entrée. plus d’informations sur les modes de contrôle d’entrée sont fournies plus loin dans ce document.

|  |  Clavier |  Souris |  Contrôleur Xbox | 
|----------|----------|----------|----------|
|  Lacet |  Flèches gauche/droite |  Faire glisser vers la gauche/droite |  Stick à droite gauche/droite | 
|  Inclinaison |  Flèches haut/bas |  Faire glisser vers le haut/vers le haut |  Joystick droit vers le haut/vers le haut | 
|  Annuler |  Q/E |  |  DPad gauche/droite | 
|  X |  A/D |  |  Stick analogique gauche vers la gauche/droite | 
|  Y |  PG. suiv/PG. suiv |  |  DPad vers le haut/vers le haut | 
|  Z |  W/S |  |  Joystick gauche vers le haut/vers le haut | 
|  Action |  Entrée ou espace |  Bouton droit |  Un bouton ou un déclencheur | 
|  Fleuri/système |  F2 ou touche Windows |  |  Bouton B | 
|  Bouton de poignée du contrôleur |  G  |  |  | 
|  Bouton de menu contrôleur |  M  |  |  | 
|  Pavé tactile du contrôleur |  GOUDJARATI  |  |  | 
|  Appuyez sur le contrôleur Touchpad |  P  |  |  | 
|  Pression du joystick du contrôleur |  K  |  |  | 
|  État du suivi du contrôleur de gauche |  F9 |  |  | 
|  État du suivi du contrôleur approprié |  F10 |  |  | 
|  Poser la main | 7 |  |  |
|  Main « Open » (valeur par défaut) | 8 |  |  |
|  Pose de la main | 9 |  |  |
|  Main « pincer » | 0 |  |  |
|  Réinitialiser |  Touche Échap |  |  bouton Démarrer | 
|  Suivre |  T ou F3 |  |  Bouton X | 


Remarque : les boutons de contrôleur peuvent être ciblés sur une main ou un contrôleur, ou sur l’autre à l’aide des modificateurs de ciblage de la main.

## <a name="targeting"></a>Ciblage 

Certains des concepts d’entrée ci-dessus sont autonomes.  Les concepts action, fleuri/System, Reset et Tracking sont complets, n’ont pas besoin et ne sont pas affectés par, tout modificateur supplémentaire pour le ciblage.  Toutefois, les autres concepts peuvent être appliqués à une ou plusieurs cibles. Nous avons introduit des moyens de spécifier la cible à laquelle votre commande doit être appliquée.  Dans tous les cas, il est possible de spécifier par le biais de l’interface utilisateur ou par le biais de l’appui sur le clavier, l’objet à cibler.  Dans certains cas, il est également possible de spécifier directement avec le contrôleur Xbox. 

Le tableau suivant décrit les options de ciblage et la manière d’activer chacune d’elles.

| Objet | Modificateur de clavier | Modificateur de contrôleur | Modificateur de l’interface utilisateur de l’émulateur |
|----------|----------|----------|----------|
| Corps de message | (par défaut) | (par défaut) | (par défaut) |
| Siège | Contenir H | (Non disponible) | (Non disponible) |
| Main gauche/contrôleur | Maintenir le bouton gauche ALT | Bouton conserver l’épaule gauche | Punaise gauche | 
| Main droite/contrôleur | Maintenir le bouton droit Alt | Bouton de maintien de l’épaule de droite | Clic droit |
| Yeux | Conserver Y | (Non disponible) | Punaise yeux |
  
Le tableau suivant montre comment chaque modificateur cible mappe chacun des concepts d’entrée de déplacement de base

|  | Valeur par défaut (corps) |  Main/contrôleur (maintenez la touche Alt enfoncée, maintenez le bouton d’épauler du boîtier ou la punaise de l’interface utilisateur) |  En-tête (Hold H)  |  Yeux (maintenir Y ou basculer l’UI punaise) |
|----------|----------|----------|----------|
|  Lacet |  Transformer le corps vers la gauche/droite |  Déplacer la main vers la gauche/droite |  Activer l’en-tête gauche/droite | Yeux oculaires gauche/droite |
|  Inclinaison |  Activer/désactiver la tête |  Monter/descendre |  Activer/désactiver la tête | Point de regard des yeux | 
|  Annuler |  Tête de roulement gauche/droite |  |  Tête de roulement gauche/droite | (Aucune action) |
|  X |  Corps de la diapositive vers la gauche/droite |  Déplacer la main/le contrôleur vers la gauche/droite |  Activer l’en-tête gauche/droite | (Aucune action) |
|  Y |  Déplacer le corps vers le haut/vers le haut |  Monter/descendre dans la main/le contrôleur |  Activer/désactiver la tête | (Aucune action) |
|  Z |  Déplacer le corps vers l’avant/vers l’arrière |  Déplacer vers l’avant/à l’arrière du contrôleur |  Activer/désactiver la tête | (Aucune action) |
 
 
## <a name="controlling-an-app"></a>Contrôle d’une application

L’ensemble de contrôles suivant est suggéré pour une utilisation quotidienne :

|  Opération |  Clavier et souris |  Controller | 
|----------|----------|----------|
|  Corps X |  A/D |  Stick analogique gauche vers la gauche/droite | 
|  Corps Y |  PG. suiv/PG. suiv |  DPad vers le haut/vers le haut | 
|  Corps Z |  W/S |  Joystick gauche vers le haut/vers le haut | 
|  Lacet de corps |  Faire glisser la souris vers la gauche/droite |  Stick à droite gauche/droite | 
|  Lacet tête |  H + faire glisser la souris vers la gauche/droite |  H (on Keyboard) + Joystick droit gauche/droite | 
|  Hauteur des têtes |  Faire glisser la souris vers le haut/vers le haut |  Joystick droit vers le haut/vers le haut | 
|  Rouleau de tête |  Q/E |  DPad gauche/droite | 
|  Main/contrôleur X |  Alt + A/D |  Épaule + Stick à gauche gauche/droite | 
|  Main/contrôleur Y |  Alt + Pg. suiv/PG. suiv |  Épaule + DPad haut/PG. | 
|  Main/contrôleur Z |  Alt + W/S |  Épauler + joystick gauche vers le haut/vers le haut | 
|  Lacet main/Controller |  Alt + faire glisser la souris vers la gauche/droite |  Épaule + joystick droit gauche/droite | 
|  Hauteur de la main/du contrôleur |  Alt + faire glisser la souris vers le haut/vers le haut |  Haut/bouton de l’épaule + droite | 
|  Rouleau de main/contrôleur |  Alt + Q/E |  Épaule + DPad gauche/droite | 
|  Action |  Bouton droit de la souris |  Déclencheur | 
|  Fleuri/système/page d’hébergement |  F2 ou touche Windows |  Bouton B | 
|  Réinitialiser |  Échappement |  bouton Démarrer | 
|  Suivre |  T |  Bouton X | 
|  Défilement |  Alt + bouton droit de la souris + faire glisser la souris vers le haut/vers le haut |  Épaule + déclencheur + joystick droit vers le haut/vers le haut | 
|  Déplacer/faire pivoter plus rapidement | Touche Maj de gauche ou de droite | Appuyez sur le joystick droit et maintenez-le enfoncé |
|  Déplacer/faire pivoter lentement | Touche CTRL de gauche ou de droite | Appuyez sur le stick analogique gauche et maintenez-le enfoncé |

## <a name="perception-simulation-control-panel-keyboard-shortcuts"></a>Raccourcis clavier du panneau de configuration de la perception

Les raccourcis clavier suivants sont disponibles pour accéder au panneau de configuration de la simulation de perception et à l’activation ou la désactivation de périphériques d’entrée de PC pour une utilisation avec la simulation.

| Opération | Raccourci | Description/remarques |
|-----------|----------|-------------|
| Activer/désactiver le clavier pour la simulation | F4 | Lorsqu’elle est désactivée, l’entrée au clavier est envoyée à l’application HoloLens ou Windows Mixed Reality. |
| Activer l’utilisation de la souris pour la simulation | F5 | Lorsqu’elle est désactivée, l’entrée de la souris est envoyée à l’environnement de réalité mixte (Windows Mixed Reality uniquement) |
| Activer/désactiver le boîtier d’activation pour la simulation | F6 | Lorsqu’elle est désactivée, l’entrée du boîtier est ignorée par la simulation |
| Afficher ou masquer le panneau de configuration | F7 | |
| Définir le focus clavier sur le panneau de configuration | F8 | Si le panneau n’est pas visible actuellement, il s’affiche en premier. |
| Ancrer ou détacher le panneau vers/depuis la fenêtre du portail de l’émulateur ou de la réalité mixte | F9 | Si la fenêtre est fermée lorsqu’elle est désancrée, elle est ancrée et masquée. |

## <a name="see-also"></a>Voir également
* [Installer les outils](install-the-tools.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Utilisation du simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md)
