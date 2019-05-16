---
title: Regards de tête et de balayage
description: Vue d’ensemble du modèle d’entrée du pointage de regard head et durée d’affichage
author: liamartinez
ms.author: liamar
ms.date: 05/13/2019
ms.topic: article
ms.localizationpriority: high
keywords: Mixte réalité, regards, durée d’affichage, interaction, concevoir
ms.openlocfilehash: 9f9fa89d7730e21e89bd24ce3b483d129c8a16db
ms.sourcegitcommit: 1c0fbee8fa887525af6ed92174edc42c05b25f90
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65730777"
---
# <a name="head-gaze-and-dwell"></a>Regards de tête et de balayage

Lorsque mains sont occupées avec les outils et les parties, les gestes peuvent être fastidieuse, voire impossible. Les commandes vocales, comme les mouvements, peuvent être incertains dans certains contextes, par exemple dans des conditions très bruyants. En outre, à l’aide de la voix pour contrôler les ordinateurs ne sont pas universellement courants, mais il est gagne à vapeur ! Regards de tête et de balayage offre le mécanisme plus familière et facile à master sur l’utilisation de profondes et mains-libres sur HoloLens. En outre, head-regards et la durée d’affichage est 100 % fiables indépendamment des contraintes de bruit interférence ni de silence dans l’environnement d’exploitation.

## <a name="scenarios"></a>Scénarios

Regards de tête et de la durée d’affichage convient parfaitement dans les scénarios où les mains d’une personne sont occupées avec d’autres tâches, et voice n’est pas 100 % fiables ou disponibles en raison des contraintes de l’environnement ou de réseaux sociaux. Un bon exemple est un homme portant un HoloLens pour superposer des informations de référence pendant la réparation d’un moteur de voiture. Les mains sont occupées avec des outils ou de la prise en charge de leur corps comme ils se pencher dans le compartiment de moteur. L’espace de garage est forte, avec la constante claquement et bourdonnement d’outils, ce qui rend les commandes vocales difficile. Regards de tête et de la durée d’affichage permet à la personne dans le HoloLens pour accéder en toute confiance leurs documents de référence sans interupting leur flux de travail. 

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Modèle d’entrée</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1er gen)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
    </tr>
     <tr>
        <td>Regards de tête et de balayage</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé</td>
    </tr>
</table>

## <a name="goals"></a>Objectifs

Fournissent un mécanisme pour les interactions entièrement mains-libres, sans utiliser la voix.

## <a name="design-principles"></a>Principes de conception

1. Éviter le « Utilisation comme une arme »

    Regards de tête et de balayage nécessite une rétroaction visuelle pour être intuitive, mais trop commentaires peuvent provoquer l’anxiété. Les commentaires doivent permettent à un utilisateur de savoir qu’ils vous ciblez, mais pas de la sélection automatique il par rapport à leur intention. Lecture d’étiquettes de texte, icônes et nécessite des précautions supplémentaires pour fournir un espace de la personne pour absorber les informations avant de sélectionner.
    
2. Vitesse de boucles d’or de recherche
    
    Interactions de balayage peuvent avoir différents minuteurs en fonction de l’impact de la navigation : fonctions les plus fréquemment utilisées généralement bénéficieront de remplissage plus rapides, tandis que les fonctions plus indirects peuvent bénéficier de temps de remplissage. Lorsque vous utilisez un effet de remplissage pour afficher ces minuteurs, des courbes de l’animation de la couleur de remplissage peuvent influencer positivement un sentiment de temps de remplissage plus rapides. Considération doit être prise pour activer la décision de l’utilisateur à partir de fast/moyenne/ralentir les remplacements de vitesse de remplissage.
    
3. Par exemple no-no pour effet d’yo-yo

    L’effet yo-yo est un modèle désagréable de mouvement de la tête qui peut émerger lorsque la position des contrôles de contenu et du pointage de regard head et balayage oblige les utilisateurs à en permanence à plusieurs reprises rechercher diminué. Par exemple, une liste de navigation avec le bouton regards de tête et de la durée d’affichage en bas provoque une boucle des - rechercher vers le bas pour m’attarderai pas, examinez résultats, recherchez vers le bas à m’attarderai pas, etc. Ce modèle qui en résulte est désagréable et doit être évité en plaçant les contrôles de navigation dans un emplacement centralisé qui nécessite moins de back-et-les deux sens. L’emplacement des boutons de durée d’affichage par rapport à leurs effets devient important pour plus de confort.

## <a name="ux-guidelines-and-best-practices"></a>Les instructions de l’expérience utilisateur et les meilleures pratiques

### <a name="target-sizes"></a>Taille des cibles
  Pour être facilement accessible, head-regards m’attarderai pas cibles doivent être suffisamment grand pour comforatably cible et maintenez la touche de tête stabily sur la cible pour le délai imparti. Nous vous recommandons une taille cible minimale de 2 degrés pour atteindre l’expérience plus à l’aise. 

### <a name="visual-feedback"></a>Retour visuel

Lorsque vous utilisez un remplissage radial pour représenter le minuteur de durée d’affichage, démarrez à partir du centre du bouton. Une réponse cohérente est plus claire que toutes les directions différentes sur les boutons différents. 

  * Cette règle peut être rompue, bien que pour les interactions directionnelle (par exemple, nav haut/bas/gauche/droite, etc.). Par exemple, rend les Guides Microsoft Dynamics 365 une exception sur précédente/suivante va rester remplissages de droite.
  * Envisagez d’inversion radiale remplir à partir de l’extérieur, pour des scénarios tels que l’activation/désactivation d’un bouton désactivé. Le sentiment inverse de l’envoi d’un bouton est un modèle intéressant visual pour maintenir. 

### <a name="progressive-disclosure"></a>Affichage progressif

Affichage progressif signifie uniquement affiche toutes les informations s’applique à chaque étape d’une interaction. Pour la durée d’affichage, cela signifie que la cible de la durée d’affichage est affichée sur la mise en surbrillance (par exemple, dans un contrôle de liste).

 ### <a name="oversized-targets"></a>Cibles trop volumineux
Région de la durée d’affichage peut être supérieure à icône inactive pour le rendre plus facile à utiliser, comme le bouton précédent dans les Guides Microsoft Dynamics 365.

### <a name="prevent-flickering-with-delayed-feedback"></a>Éviter le scintillement avec commentaires retardée
Utilisez un court délai avant de démarrer des commentaires visuels afin d’éviter le scintillement lorsque quelqu'un passe sur une cible de la durée d’affichage.
* Pour inteacted boutons avec fréquemment, conservez le délai très court, donc l’application semble réactive.
* Pour les boutons qui sont interagissaient avec infrequenctly un délai plus long peut être approprié afin d’éviter l’interface que vous vous sentez twitchy.

## <a name="ui-patterns"></a>Modèles d’interface utilisateur

### <a name="high-frequency-buttons"></a>Boutons de fréquence élevée
![Bouton suivant pour Microsoft Dynamics 365 Guides](images/GuideNextButton.png "bouton suivant pour Microsoft Dynamics 365 Guides") haute fréquence boutons sont couramment utilisés tout au long d’une application. Un bon exemple de ceux-ci sont les boutons suivant et précédent dans les Guides de Microsoft Dynamics 365.

* Boutons de haute fréquence doit...
  * boutons plus grande, plus facile à atteindre regards de tête
  * Restez près de hauteur des yeux afin d’éviter de surcharger ergonomique.

### <a name="low-frequency-buttons"></a>Boutons de fréquence faible
Boutons de fréquence faible sont qui ne sont pas interagi avec comme régulièrement tout au long de l’application. Un bon exemple peut être un bouton pour accéder au menu Paramètres, ou un bouton pour effacer tout le travail.

* Essayons de garder ces boutons hors de votre zone fréquentes du pointage de regard head chemins d’accès afin d’éviter toute activation accidentelle. 

### <a name="confirmations"></a>Confirmations
![Boîte de dialogue de Confirmation de Microsoft Dynamics 365 Guides](images/GuidesConfirmation.png "boîte de dialogue de Confirmation de Microsoft Dynamics 365 Guides")

Lorsqu’une action a un impact significatif, tels que money de chargement, la suppression de travail ou démarrage d’un processus long, il est utile confirmer qu’une personne destiné à sélectionner un bouton. Pour les regards de tête et de balayage interfaces utilisateur il existe quelques modèles et les considérations relatives à des boîtes de dialogue de confirmation :

  * Afficher la surbrillance de sélection sur le bouton principal.
  * Révéler la cible de la durée d’affichage en même temps que la surbrillance de sélection.
  * Pour le bouton secondaire, révéler la cible résident sur des regards de tête.
        
### <a name="toggle-buttons"></a>Boutons bascule
Boutons bascule nécessitent une logique subtils fonctionne correctement. Quand une personne dwells sur un bouton bascule et actifs il, ils doivent quitter le bouton, puis revenez pour redémarrer la logique de la durée d’affichage. Il est important que boutons pouvant ont un actif clair par rapport à l’état inactif. 

### <a name="list-views"></a>Affichages de liste
![Boîte de dialogue de Confirmation Microsoft Dynamics 365 Guides](images/GuidesListView.png "boîte de dialogue de Confirmation Microsoft Dynamics 365 Guides") les affichages en liste présentent un défi particulier pour pointage de regard head et m’attarderai pas d’entrée. Personnes doivent être en mesure d’analyser le contenu sans craindre devant tiptoe autour des cibles de la durée d’affichage. 

Quelques conseils pour la conception de vues de liste :
* avoir toute la ligne à mettre en surbrillance lorsque gazed de tête, mais ne commence pas balayage, sauf si les regards de tête se trouve sur la cible de la durée d’affichage spécifique.
* afficher uniquement la cible de la durée d’affichage lorsque la ligne est mise en surbrillance pour réduire le bruit visuel.
* être claire et cohérente avec la position des cibles de la durée d’affichage.
* Ne plus afficher que m’attarderai donc pas toutes les cibles à la fois pour éviter l’interface utilisateur répétitive
* réutiliser le même modèle aussi souvent que possible pour établir une bonne connaissance de l’expérience utilisateur
 
 ## <a name="see-also"></a>Voir aussi
* [Manipulation directe](direct-manipulation.md)
* [Pointer et valider](point-and-commit.md)
* [Fonctionnalités de base des interactions](interaction-fundamentals.md)
* [Pointer du regard vers l’avant et valider](gaze-and-commit.md)
* [Pointer du regard et parler](voice-design.md)
