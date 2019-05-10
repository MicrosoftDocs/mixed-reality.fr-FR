---
title: Regards et durée d’affichage
description: Vue d’ensemble du modèle d’entrée du pointage de regard et durée d’affichage
author: liamartinez
ms.author: liamar
ms.date: 03/31/2019
ms.topic: article
keywords: Mixte réalité, regards, durée d’affichage, interaction, concevoir
ms.openlocfilehash: d99180b6eb278eb6d7bf322c01a1c7cceb7fad1f
ms.sourcegitcommit: a4a53e6772805d89a47588857e3e8fb1fd8d9710
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65469065"
---
# <a name="gaze-and-dwell"></a>Regards et durée d’affichage

Lorsque mains sont occupées avec les outils et les parties, les gestes peuvent être fastidieuse, voire impossible.  Les commandes vocales, comme un mouvement, peuvent être fait des circonstances fiables, par exemple dans des conditions très bruyants.  En outre, voix à des ordinateurs de contrôle n’est pas encore une interaction de grand public, mais il est gagne à vapeur !  Durée d’affichage du pointage de regard offre le mécanisme plus familière et facile à master pour tête haute travail mains-libres sur HoloLens.  En outre, la durée d’affichage du pointage de regard est fiables à 100 % indépendantes des contraintes de bruit interférence ni de silence dans l’environnement d’exploitation.

## <a name="goals"></a>Objectifs

Fournissent un mécanisme pour les interactions de mains-libres, sans utiliser la voix.

## <a name="design-principles"></a>Principes de conception

1. Regards n’est pas une arme
    
    Regards requiert des commentaires visuels pour tactiles intuitives, mais trop commentaires peuvent provoquer l’anxiété. Les commentaires doivent aider un utilisateur qu’ils vous ciblez, mais pas-sélection automatique par rapport à leur intention. Lire le texte nécessite des précautions supplémentaires pour fournir une salle de l’utilisateur pour absorber les informations avant de sélectionner.
    
2. Vitesse de boucles d’or de recherche
    
    Le remplissage de balayage peut avoir différents minuteurs en fonction de l’impact de la navigation : fonctions les plus fréquemment utilisées généralement bénéficieront de remplissage plus rapides, tandis que les fonctions plus indirects peuvent bénéficier de temps de remplissage. Courbes de l’animation de la couleur de remplissage peuvent influencer positivement un sentiment de temps de remplissage plus rapides. Considération doit être prise pour activer la décision de l’utilisateur à partir de fast/moyenne/ralentir les remplacements de vitesse de remplissage.
    
3. Par exemple no-no pour effet d’yo-yo

    L’effet d’yo-yo (également appelé « nuit à le Roxbury ») est un modèle désagréable qui peut émerger à partir de certains placement du contenu et des contrôles basés sur des regards. Par exemple, une liste de navigation avec le bouton de remplissage en bas provoque une boucle des - rechercher vers le bas pour m’attarderai pas, examinez résultats, descendez à durée d’affichage, etc. Ce modèle qui en résulte est désagréable et doit être évité en plaçant les contrôles de navigation dans un emplacement centralisé qui nécessite moins de back-et-les deux sens. L’emplacement des boutons de durée d’affichage par rapport à leurs effets devient important pour plus de confort.

## <a name="ui-patterns"></a>Modèles d’interface utilisateur

### <a name="high-frequency-buttons"></a>Boutons de fréquence élevée
    
* Boutons suivant/précédent
  * Remplissage préalable de délai très court (tampon du scintillement passage supérieur)
  * Boutons plus volumineux sont plus faciles à atteindre du pointage de regard
  * Bon de ne tenir compte de ces à hauteur des yeux donc aucune déformation pour interagir
  * Région de la durée d’affichage peut être supérieure à icône inactive pour le rendre plus facile à utiliser (arrière)

### <a name="low-frequency-buttons"></a>Boutons de fréquence faible
    
* Activer le menu Paramètres
  * Retarder plus remplissage préalable OK (tampon du scintillement passage supérieur)
  * Essaie de garder ces boutons hors de votre zone voies de curseur fréquentes

* Confirmations (autrement dit, les flux d’analyse, les boîtes de dialogue)
  * Afficher la surbrillance de sélection sur le bouton principal
  * Révéler la cible de la durée d’affichage en même temps que la surbrillance de sélection
  * Utilisez m’attarderai pas cible entourant l’icône pour simplifier l’interface
  * Décision importante, afin de n’active la mise en surbrillance, révèle cible de la durée d’affichage pour les temps de réexamen
        
### <a name="toggle-buttons"></a>Boutons bascule

* Pin
  * État visuel clair actives/inactives
  * Remplissage radiale permet à utilisateur de focus et fournit la progression naturelle 

* Paramètres individuels
  * États clair actives/inactives
  * M’attarderai pas cibles tous sur l’icône environnante gauche
  * Durée d’affichage cible s’affichent uniquement quand sélection mettre en surbrillance active
  * « M’attarderai pas sur curseur « côté droit pour activé/désactivé des paramètres

### <a name="list-views"></a>Affichages de liste

* Affichage de liste navigation - fichiers de guide à ouvrir
  * Points importants du curseur de ligne à partir de n’importe où sur la ligne, mais ne commence pas balayage
  * Lors de la ligne est mise en surbrillance par le curseur, la cible de la durée d’affichage apparaît à gauche
  * M’attarderai pas cible toujours un cercle sur le côté gauche du texte dans tous les affichages de liste
  * Ne plus afficher que m’attarderai donc pas toutes les cibles à la fois pour éviter l’interface utilisateur répétitive
  * Réutiliser le même modèle pour établir une bonne connaissance de l’expérience utilisateur
        
* Mode liste - hiérarchie des tâches/étapes dans un repère de navigation
  * M’attarderai pas cible toujours un cercle sur le côté gauche du texte
  * Développer/réduire intuitif de balayage
        
* Affichage de liste navigation - mode select
  * Suivez les modèles ci-dessus

### <a name="contextual-buttons"></a>Boutons contextuelles

* Afficher/masquer 3D - affiche des 3D le long d’attache près hologrammes 
  * État visuel clair actives/inactives

### <a name="pivots"></a>Pivots

* Liste de récents/tous les repères
  * Remplir l’intuitif de l’interface utilisateur reste pour indiquer quel onglet est actif
  * Pour les tableaux croisés dynamiques court terme unique, nous avons choisi de renoncer au modèle cible de balayage
  * Nous favorisé l’interface simplifiée par rapport à un autre cibles cercle 2 et une interface utilisateur plus large
  * Dans notre cas, les mots sont suffisamment courts pour qu’un délai fournit suffisamment confort avant leur remplissage


## <a name="ux-guidelines-and-best-practices"></a>Les instructions de l’expérience utilisateur et les meilleures pratiques

### <a name="target-sizes"></a>Taille des cibles

  * Taille minimale de l’icône PIN : 6cm dans l’espace universel dans Unity, 30 derniers éléments utilisés (30cm @ 2m)
  * Sont les cibles de « elle était aimantées » ou « permanent » du tout ? (autrement dit, les regards lissage du curseur)

### <a name="animation"></a>Animation

  * Délai d’attente avant la durée d’affichage des déclencheurs visual .5sec
  * Durée de balayage visuel 1,2 s
  * Animation de courbe ?

### <a name="visual-feedback"></a>Retour visuel

  * Remplir à partir de l’emplacement de début du curseur regards de radiale
  * Remplissage toujours radiale à partir du centre du bouton. Une réponse cohérente est plus claire que toutes les directions différentes sur les boutons différents. 
    * Cette règle peut être rompue, bien que pour les interactions directionnelle (par exemple, nav haut/bas/gauche/droite, etc.). Par exemple, rend Guides une exception sur précédente/suivante va rester avec le bouton droit de remplissage.
    * Envisagez d’inversion radiale remplir à partir d’à l’extérieur (si l’activation/désactivation). Le sentiment inverse de l’envoi d’un bouton est un modèle intéressant visual pour maintenir. 

### <a name="progressive-disclosure"></a>Affichage progressif

 * Affichage progressif signifie que la cible de la durée d’affichage est affichée sur la mise en surbrillance (par exemple, dans un contrôle de liste)
 * Points importants de barre de texte avec spotlight révèlent sur regards n’importe où sur le texte
 * Cible de remplissage du pointage de regard apparaît toujours sur la gauche, mais uniquement pour l’élément de liste qui est mis en surbrillance
 * Essayez d’éviter d’avoir toutes les cibles de balayage sur à tout moment en raison de l’aspect répétitif de cercles empilées
 
 ## <a name="see-also"></a>Voir aussi
* [Manipulation directe](direct-manipulation.md)
* [Pointer et valider](point-and-commit.md)
* [Fonctionnalités de base des interactions](interaction-fundamentals.md)
* [Pointer du regard vers l’avant et valider](gaze-and-commit.md)
* [Pointer du regard et parler](voice-design.md)
