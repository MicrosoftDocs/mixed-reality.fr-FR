---
title: Entrée avancée d’émulateur de HoloLens et simulateur de réalité mixte
description: Obtenir des instructions détaillées pour l’utilisation du clavier, souris et le contrôleur de X-Box pour simuler l’entrée pour l’émulateur de HoloLens et d’un simulateur de réalité mixte de Windows.
author: ChimeraScorn
ms.author: cwhite
ms.date: 02/24/2018
ms.topic: article
keywords: HoloLens, émulateur, Simulation, Windows Mixed Reality
ms.openlocfilehash: 59bea340a2ecdd2d65481c9ace4ab3f0bf15bc6f
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593366"
---
# <a name="advanced-hololens-emulator-and-mixed-reality-simulator-input"></a>Entrée avancée d’émulateur de HoloLens et simulateur de réalité mixte

La plupart des utilisateurs de l’émulateur devrez utiliser les contrôles d’entrée de base pour le [HoloLens émulateur](using-the-hololens-emulator.md#basic-emulator-input) ou [simulateur de réalité mixte Windows](using-the-windows-mixed-reality-simulator.md#basic-simulator-input). Les détails ci-dessous sont pour les utilisateurs expérimentés qui ont trouvé un besoin pour simuler des types plus complexes d’entrée.

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).

## <a name="concepts"></a>Concepts

Pour commencer à contrôler les entrées virtuelle à l’émulateur de HoloLens et d’un simulateur de réalité mixte Windows, vous devez d’abord comprendre quelques concepts.

Mouvement fait référence au contrôle et la modification de la position et l’orientation d’un élément dans la scène. Pour un objet contrôlable ciblé, le mouvement est contrôlé avec une rotation et de translation (déplacement) le long des trois axes.
* **Lacet**: Activez la gauche ou vers la droite.
* **Pitch**: Activer le haut ou vers le bas.
* **ROULEAU**: Déploiement côte à côte.
* **X**: Déplacer à gauche ou droite.
* **Y**: Faire monter ou Descendre.
* **Z**: Déplacer vers l’avant ou vers l’arrière.

[Mouvement](gestures.md) et de l’entrée de contrôleur de mouvement sont mappées étroitement à la manière dont ils périphériques physiques :
* **Action**: Cela simule l’action d’en appuyant sur l’index pour le curseur ou en les extrayant le bouton d’action sur un contrôleur. Par exemple, l’entrée d’Action peut être utilisée pour simuler le mouvement d’appui en l’air, pour faire défiler le contenu et à appuyer et maintenir.
* **[Bloom](gestures.md#bloom) ou accueil**: Les HoloLens fleurir mouvement ou bouton d’accueil d’un contrôleur est utilisé pour retourner à l’environnement et pour effectuer des actions du système.

Mains ont une riche reprresentation dans HoloLens V2.  En plus d’être suivies/non et non suivies utilisables pour les mouvements de conduite, mains sont maintenant un modèle squelette articulé ajuster à leur et exposée au développeur.  Cela introduit 20 points de suivi sur chaque aiguille.  
* **Mixte**: L’une des vingt positions suivies pour chaque cas suivies. Cela aura un point est associé un espace 3d.
* **Poser**: Une collection complète de tous les articulations dans une main suivie. À ce stade, il s’agit d’une collection de 20 Joints. 

À ce stade, nous n’exposent pas un contrôle direct de chaque position commune individuellement via l’interface utilisateur de l’émulateur. Bien que vous pouvez les définir via l’API de simulation. Au lieu de cela, nous avons un ensemble d’utile risque de poser représentatif l’émulateur vous permet de basculer entre.

Vous pouvez également contrôler l’état de l’entrée de capteur simulées :
* **Réinitialiser**: Ceci renverra tous les capteurs simulés à leurs valeurs par défaut.
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
|  Bloom |  Touche F2 ou Windows (clé de Windows ne fonctionne qu’avec l’émulateur de HoloLens) |  |  Bouton B | 
|  Bouton de poignée de contrôleur |  G (Windows Mixed Reality simulateur uniquement) |  |  | 
|  Bouton de menu de contrôleur |  M (Windows Mixed Reality simulateur uniquement) |  |  | 
|  Touch pavé tactile de contrôleur |  U (Windows Mixed Reality simulateur uniquement) |  |  | 
|  Appuyez sur le pavé tactile contrôleur |  P (Windows Mixed Reality simulateur uniquement) |  |  | 
|  Définir la Pose de main | 7, 8, 9 ou 0 |  |  |
|  Réinitialiser |  Touche ÉCHAP |  |  bouton Démarrer | 
|  Suivi |  T ou F3 |  |  Bouton X | 


Remarque: Dans le simulateur de réalité mixte Windows, les boutons de contrôleur peuvent être adressé à un côté ou de l’autre à l’aide de l’aiguille de ciblage des modificateurs.

## <a name="targeting"></a>Ciblage 

Certains des concepts d’entrée ci-dessus, mettez au point leurs propres.  Action, de Bloom, de réinitialisation et de suivi sont des concepts complètes n’est pas nécessaire et ne sont pas affectés par n’importe quel modificateur supplémentaires pour le ciblage.  Toutefois, les concepts restants peuvent être appliquées à une de plusieurs cibles. Nous avons introduit les méthodes vous permettent de spécifier qui cible à que votre commande doit être appliqué.  Dans tous les cas, il est possible de spécifier via l’interface utilisateur ou via les appuis de clavier, objet targtet.  Dans certains cas, il est également possible de spécifier directement avec le contrôleur de la xbox. 

Le tableau suivant décrivent les options de ciblage et la façon d’activer chacun d’eux.

| Objet | Touche de modification | Modificateur de contrôleur | Modificateur de l’interface utilisateur d’émulateur |
|----------|----------|----------|----------|
| Corps | <default> | <default> | <default> |
| head | Blocage H | <None available> | Punaise HEAD dans l’interface utilisateur |
| Main gauche/contrôleur | Bouton de Alt gauche | Bouton de l’épaule gauche | Gauche punaise | 
| Droite/contrôleur | Bouton Alt droite | Bouton de droite épaule | Droite punaise |
| Yeux | Attente Y | <No contoller modifier available> | Punaise des yeux |
  
Le tableau suivant montre comment chaque modificateur cible est mappé à chacun des mouvements d’entrée certains concepts fondamentaux

|  Par défaut (corps) |  Main/contrôleur (maintenez la touche alt / épaule) |  Head (maintenez H)  |  Yeux (maintenez Y) |
|----------|----------|----------|----------|
|  Lacet |  Corps de la main gauche / droite |  Déplacer la main gauche / droite |  Activer la tête gauche / droite | Les regards yeux recherche gauche/droite |
|  Inclinaison |  Activer la tête haut / bas |  Main haut / bas |  Activer la tête haut / bas | Les regards yeux recherche haut/bas | 
|  Annuler |  Rouleau de tête gauche / droite |  |  Rouleau de tête gauche / droite | (Aucune action) |
|  X |  Corps de la diapositive gauche / droite |  Déplacer/contrôleur de la main gauche / droite |  Activer la tête gauche / droite | (Aucune Action) |
|  Y |  Déplacer des corps haut / bas |  Déplacer la main/contrôleur haut / bas |  Activer la tête haut / bas | (Aucune Action) |
|  Z |  Déplacer vers l’avant / arrière de corps |  Déplacer vers l’avant / arrière main/de contrôleur. |  Activer la tête haut / bas | (Aucune Action) |
 
Remarque: Dans le simulateur de réalité mixte Windows, les boutons de contrôleur peuvent être adressé à un côté ou de l’autre à l’aide de l’aiguille de ciblage des modificateurs. De même, dans l’émulateur de HoloLens, la pose articulés main peut être adressé à un côté ou de l’autre à l’aide des modificateurs de la main. 
 
## <a name="controlling-an-app"></a>Contrôle d’une application

Cet article a décrit l’ensemble complet des types d’entrée et les modes d’entrée qui sont disponibles dans l’émulateur de HoloLens et d’un simulateur de réalité mixte Windows. L’ensemble de contrôles suivant est suggéré pour une utilisation quotidienne :

|  Opération |  Clavier et souris |  Contrôleur | 
|----------|----------|----------|
|  Corps X |  A / D |  Stick analogique gauche gauche / droite | 
|  Corps Y |  Page vers le haut / bas de page |  DPad haut / bas | 
|  Corps Z |  W / S |  Stick analogique gauche, haut / bas | 
|  Corps lacet |  Faites glisser la souris gauche / droite |  Stick analogique droit gauche / droite | 
|  Head lacet |  H + faire glisser la souris gauche / droite |  H (sur le clavier) + stick analogique droit gauche / droite | 
|  Hauteur de la tête |  Faites glisser la souris haut / bas |  Stick analogique droit haut / bas | 
|  Rouleau de tête |  Q / E |  DPad gauche / droite | 
|  Main X |  Alt + faire glisser la souris gauche / droite |  Épaule + stick analogique droit gauche / droite | 
|  Main Y |  Alt + faire glisser la souris haut / bas |  Épaule + stick analogique droit haut / bas | 
|  Main Z |  ALT + W / S |  Épaule + stick analogique gauche, haut / bas | 
|  Action |  Bouton droit de la souris |  déclencheur | 
|  Fleurir / Home |  Touche F2 ou Windows (clé de Windows est uniquement pour l’émulateur de HoloLens) |  Bouton B | 
|  Réinitialiser |  Échappement |  bouton Démarrer | 
|  Suivi |  T |  Bouton X | 
|  Défilement |  ALT + flèche droite bouton de souris + faire glisser la souris haut / bas |  Épaule + déclencheur + stick analogique droit haut / bas | 

## <a name="see-also"></a>Voir aussi
* [Installer les outils](install-the-tools.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [L’utilisation du simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md)
