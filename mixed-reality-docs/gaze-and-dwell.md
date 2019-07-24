---
title: Suivre de la tête et stabiliser
description: Vue d’ensemble du modèle d’entrée Suivre de la tête et stabiliser
author: liamartinez
ms.author: liamar
ms.date: 05/13/2019
ms.topic: article
keywords: Mixed Reality, pointer du regard, stabiliser, interaction, concevoir
ms.openlocfilehash: d522ca3a6f36995959e8e6e87482279d05bf0aa3
ms.sourcegitcommit: b0b1b8e1182cce93929d409706cdaa99ff24fdee
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68387542"
---
# <a name="head-gaze-and-dwell"></a>Suivre de la tête et stabiliser

Quand les mains sont occupées avec des outils et des pièces, les mouvements peuvent être fastidieux, voire impossibles. Les commandes vocales, à l’image des mouvements, peuvent être incertaines dans des contextes donnés, par exemple dans des conditions très bruyantes. En outre, l’utilisation de la voix pour contrôler les ordinateurs n’est pas universellement courante, mais elle est certainement en train de s’intensifier ! Le modèle Suivre de la tête et stabiliser offre le mécanisme le plus familier et le plus facile à maîtriser pour travailler sur HoloLens tête relevée et mains libres. De plus, ce modèle est fiable à 100 % ; il n’est pas sensible aux interférences sonores et ne demande pas le silence dans l’environnement.

## <a name="scenarios"></a>Scénarios

Le modèle Suivre de la tête et stabiliser convient parfaitement dans les scénarios où les mains d’une personne sont occupées à d’autres tâches et où la voix n’est pas fiable ou disponible à 100 % en raison de contraintes environnementales ou sociales. Un bon exemple est une personne portant un appareil HoloLens pour superposer des informations de référence tout en réparant un moteur de voiture. Ses mains sont occupées par des outils ou supportent son corps quand elle se penche dans le compartiment du moteur. L’espace du garage est bruyant, les coups et bourdonnement constants des outils rendant difficile l’utilisation de commandes vocales. Le modèle Suivre de la tête et stabiliser permet à la personne immergée dans l’appareil HoloLens de parcourir en toute confiance son matériau de référence sans interrompre son workflow. 

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
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Suivre de la tête et stabiliser</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé</td>
    </tr>
</table>

## <a name="goals"></a>Objectifs

Fournir un mécanisme pour des interactions entièrement mains-libres, sans utiliser la voix.

## <a name="design-principles"></a>Principes de conception

1. Éviter le « pointage du regard comme une arme »

    Pour être intuitif, le modèle Suivre de la tête et stabiliser nécessite un retour visuel, mais trop de retour peut engendrer de l’anxiété. Le retour doit aider l’utilisateur à savoir ce qu’il cible, sans sélectionner automatiquement l’objet concerné contre son gré. L’utilisateur étant amené à lire du texte, des étiquettes et des icônes, vous devez faire en sorte qu’il dispose d’un espace suffisant pour absorber les informations avant d’effectuer une sélection.
    
2. Rechercher la vitesse idéale
    
    Les interactions avec stabilisation peuvent avoir différentes durées en fonction de l’impact de la navigation : les fonctions plus fréquemment utilisées bénéficient généralement de temps de remplissage plus rapides, tandis que les fonctions plus conséquentes peuvent bénéficier de temps de remplissage plus longs. Quand vous utilisez un effet de remplissage pour afficher ces durées, les courbes d’animation de la couleur de remplissage peuvent engendrer un sentiment positif de temps de remplissage plus rapides. Vous devez envisager de laisser à l’utilisateur la possibilité de choisir la vitesse de remplissage (rapide, moyenne, lente).
    
3. Éviter l’effet yo-yo

    L’effet yo-yo est un schéma désagréable de mouvement de la tête qui peut émerger quand la position des contrôles de contenu et de suivi de la tête et de stabilisation oblige l’utilisateur à regarder vers le haut et vers le bas de façon répétée. Par exemple, une navigation par liste avec le bouton de suivi de la tête et de stabilisation situé en bas engendre une boucle : l’utilisateur regarde vers le bas pour stabiliser, puis regarde vers le haut pour lire les résultats, puis regarde vers le bas pour stabiliser, etc. Le schéma qui en résulte est désagréable. Vous devez donc l’éviter en plaçant les contrôles de navigation dans un emplacement centralisé qui nécessite moins d’allers-retours. Le placement des boutons de stabilisation par rapport à leurs effets est important pour le confort.

## <a name="ux-guidelines-and-best-practices"></a>Recommandations et bonnes pratiques pour l’expérience utilisateur

### <a name="target-sizes"></a>Taille des cibles
  Pour être facilement accessible, une cible de suivi de la tête et de stabilisation doit être suffisamment grande pour que l’utilisateur puisse cibler et maintenir sa tête sur la cible de façon stable et confortable durant le délai imparti. Nous vous recommandons une taille de cible minimale de 2 degrés pour procurer l’expérience la plus confortable. 

### <a name="visual-feedback"></a>Retour visuel

Quand vous utilisez un remplissage radial pour représenter la durée de stabilisation, démarrez à partir du centre du bouton. Une réponse cohérente est plus claire que toutes les directions différentes sur les différents boutons. 

  * Cette règle peut cependant être enfreinte pour les interactions directionnelles (par exemple, navigation vers le haut/bas/gauche/droite, etc.). Par exemple, Microsoft Dynamics 365 Guides fait une exception pour SUIVANT/PRECEDENT qui correspond aux remplissages gauche et droite.
  * Envisagez d’inverser le remplissage radial à partir de l’extérieur pour les scénarios tels que la désactivation d’un bouton. Le sentiment inverse d’appui sur un bouton est un schéma visuel agréable à conserver. 

### <a name="progressive-disclosure"></a>Affichage progressif

L’affichage progressif consiste à n’afficher que les informations pertinentes à chaque étape d’une interaction. Pour la stabilisation, cela signifie que la cible de stabilisation est affichée au moment de la mise en surbrillance (par exemple, dans un contrôle de liste).

 ### <a name="oversized-targets"></a>Cibles trop grandes
La région de stabilisation peut être plus grande que l’icône à l’état inactif pour faciliter son utilisation, comme le bouton Précédent dans Microsoft Dynamics 365 Guides.

### <a name="prevent-flickering-with-delayed-feedback"></a>Éviter le scintillement avec un retour décalé
Utilisez un court délai avant de démarrer le retour visuel afin d’éviter le scintillement quand l’utilisateur passe au-dessus d’une cible de stabilisation.
* Pour les boutons avec lesquels l’utilisateur interagit fréquemment, conservez un délai très court afin que l’application semble réactive.
* Pour les boutons avec lesquels l’utilisateur interagit peu fréquemment, un délai plus long peut être approprié afin que l’interface conserve sa fluidité.

## <a name="ui-patterns"></a>Schémas de l’interface utilisateur

### <a name="high-frequency-buttons"></a>Boutons à haute fréquence
![Bouton suivant de Microsoft Dynamics 365 guides](images/GuideNextButton.png "Bouton suivant de Microsoft Dynamics 365 guides")<br>
*Les boutons à fréquence élevée sont des boutons utilisés couramment dans une application. Les boutons suivant et précédent dans les guides Microsoft Dynamics 365 sont un bon exemple.*

Les boutons à haute fréquence doivent :
* Être des boutons plus grands et plus faciles à atteindre avec un suivi de la tête
* Demeurer à hauteur des yeux afin d’éviter une surcharge ergonomique

### <a name="low-frequency-buttons"></a>Boutons à fréquence faible
Les boutons à fréquence faible sont les boutons avec lesquels l’utilisateur n’interagit pas aussi régulièrement tout au long de l’application. À titre d’exemple, citons un bouton permettant d’accéder à un menu de paramètres ou d’effacer la totalité du travail.

* Dans la mesure du possible, maintenez ces boutons hors du chemin emprunté par les suivis de la tête afin d’éviter une activation accidentelle. 

### <a name="confirmations"></a>Confirmations
![Boîte de dialogue de confirmation dans Microsoft Dynamics 365 Guides](images/GuidesConfirmation.png "Boîte de dialogue de confirmation dans Microsoft Dynamics 365 Guides")

Quand une action a un impact significatif, telle que le prélèvement d’une somme d’argent, la suppression d’un travail ou le démarrage d’un long processus, il est utile de vérifier que l’utilisateur a effectivement souhaité sélectionner le bouton lié à cette action. Pour les interfaces utilisateur avec suivi de la tête et stabilisation, il existe quelques schémas et considérations relatifs aux boîtes de dialogue de confirmation :

  * Afficher la surbrillance de la sélection sur le bouton principal
  * Révéler la cible de stabilisation en même temps que la surbrillance de la sélection
  * Pour le bouton secondaire, révéler la cible de stabilisation en fonction du suivi de la tête
        
### <a name="toggle-buttons"></a>Boutons bascule
Les boutons bascule nécessitent une logique nuancée pour fonctionner correctement. Quand l’utilisateur reste sur un bouton bascule et l’active, il doit quitter le bouton, puis revenir pour redémarrer la logique de stabilisation. Il est important que l’utilisateur puisse clairement identifier si un bouton bascule est à l’état actif ou inactif. 

### <a name="list-views"></a>Affichages de liste
![Boîte de dialogue de confirmation dans Microsoft Dynamics 365 Guides](images/GuidesListView.png "Boîte de dialogue de confirmation dans Microsoft Dynamics 365 Guides")<br>
*Les affichages de liste présentent un défi particulier pour les entrées de point de vue et de point d’entrée. Les utilisateurs doivent être en mesure d’analyser le contenu sans avoir à se sentir Tiptoe autour des cibles du logement.*

Quelques conseils pour la conception des vues de liste :
* Mettre en surbrillance toute la ligne quand elle est suivie de la tête, mais ne commencer la stabilisation que si le suivi de la tête se trouve sur la cible de stabilisation souhaitée
* N’afficher la cible de stabilisation que quand la ligne est mise en surbrillance pour réduire le bruit visuel
* Être clair et cohérent avec la position des cibles de stabilisation
* Ne pas afficher toutes les cibles de stabilisation à la fois pour éviter que l’interface utilisateur ait un caractère répétitif
* Réutiliser le même schéma aussi souvent que possible pour procurer une expérience utilisateur familière
 
 ## <a name="see-also"></a>Voir aussi
* [Manipulation directe avec les mains](direct-manipulation.md)
* [Pointer et valider avec les mains](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Suivre de la tête et valider](gaze-and-commit.md)
* [Commander avec la voix](voice-design.md)
