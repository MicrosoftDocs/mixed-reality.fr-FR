---
title: Suivre de la tête et stabiliser
description: Vue d’ensemble du modèle d’entrée Suivre de la tête et stabiliser
author: liamartinez
ms.author: liamar
ms.date: 05/13/2019
ms.topic: article
keywords: Mixed Reality, pointer du regard, stabiliser, interaction, concevoir
ms.openlocfilehash: 6d209d3cc91ceecb4b9feef2925f093288c9f8ac
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73439310"
---
# <a name="head-gaze-and-dwell"></a>Suivre de la tête et stabiliser

Quand les mains sont occupées avec des outils et des pièces, les mouvements peuvent être fastidieux, voire impossibles. Les commandes vocales, à l’image des mouvements, peuvent être incertaines dans des contextes donnés, par exemple dans des conditions très bruyantes. En outre, l’utilisation de la voix pour contrôler les ordinateurs n’est pas universellement courante, mais elle est certainement en train de s’intensifier ! Le modèle Suivre de la tête et stabiliser offre le mécanisme le plus familier et le plus facile à maîtriser pour travailler sur HoloLens tête relevée et mains libres. De plus, ce modèle est fiable à 100 % ; il n’est pas sensible aux interférences sonores et ne demande pas le silence dans l’environnement.

## <a name="scenarios"></a>Scénarios

Le point de regard et le point de vue dans les scénarios où les mains d’une personne sont occupées avec d’autres tâches, et la voix n’est pas 100% fiable ou disponible en raison de contraintes environnementales ou sociales. Un bon exemple est une personne portant un appareil HoloLens pour superposer des informations de référence tout en réparant un moteur de voiture. Ses mains sont occupées par des outils ou supportent son corps quand elle se penche dans le compartiment du moteur. L’espace du garage est bruyant, les coups et bourdonnement constants des outils rendant difficile l’utilisation de commandes vocales. Le point de regard et l’arrière-plan permet à la personne utilisant HoloLens de parcourir en toute confiance son document de référence sans interrompre son flux de travail. 

## <a name="device-support"></a>Périphériques pris en charge

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
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Suivre de la tête et stabiliser</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé</td>
    </tr>
</table>


## <a name="design-principles"></a>Principes de conception

**Évitez le « regard d’arme »**

Pour être intuitif, le modèle Suivre de la tête et stabiliser nécessite un retour visuel, mais trop de retour peut engendrer de l’anxiété. Le retour doit aider l’utilisateur à savoir ce qu’il cible, sans sélectionner automatiquement l’objet concerné contre son gré. L’utilisateur étant amené à lire du texte, des étiquettes et des icônes, vous devez faire en sorte qu’il dispose d’un espace suffisant pour absorber les informations avant d’effectuer une sélection.
    
**Rechercher la vitesse histoire**
    
Les interactions avec stabilisation peuvent avoir différentes durées en fonction de l’impact de la navigation : les fonctions plus fréquemment utilisées bénéficient généralement de temps de remplissage plus rapides, tandis que les fonctions plus conséquentes peuvent bénéficier de temps de remplissage plus longs. Quand vous utilisez un effet de remplissage pour afficher ces durées, les courbes d’animation de la couleur de remplissage peuvent engendrer un sentiment positif de temps de remplissage plus rapides. Vous devez envisager de laisser à l’utilisateur la possibilité de choisir la vitesse de remplissage (rapide, moyenne, lente).
    
**Dites non-non à Yo-Yo Effect**

L’effet yo-yo est un schéma désagréable de mouvement de la tête qui peut émerger quand la position des contrôles de contenu et de suivi de la tête et de stabilisation oblige l’utilisateur à regarder vers le haut et vers le bas de façon répétée. Par exemple, une liste de navigation avec le bouton en tête et le point d’interposition en bas de la liste donne une boucle de-regarde vers le bas, recherche les résultats, regarde jusqu’à son logement, etc. Ce modèle résultant est peu pratique et doit être évité en plaçant les contrôles de navigation dans un emplacement centralisé qui nécessite moins de sauvegarde et d’arrière-plan. Le placement des boutons de stabilisation par rapport à leurs effets est important pour le confort.

<br>

---


## <a name="ux-guidelines-and-best-practices"></a>Recommandations et bonnes pratiques pour l’expérience utilisateur

### <a name="target-sizes"></a>Taille des cibles
  Pour être facilement accessibles, les cibles du point de vue et du regard doivent être suffisamment grandes pour regarder confortablement et maintenir une tête stable sur la cible pour le temps imparti. Nous vous recommandons une taille de cible minimale de 2 degrés pour obtenir l’expérience la plus confortable. 

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
* Pour les boutons qui sont interactifs fréquemment, laissez le délai très bref pour que l’application soit réactive.
* Pour les boutons qui sont interactifs rarement, un délai plus long peut être approprié pour éviter que l’interface twitchy.


<br>

---

## <a name="ui-patterns"></a>Schémas de l’interface utilisateur

### <a name="high-frequency-buttons"></a>Boutons à haute fréquence

:::row:::
    :::column:::
        Les boutons à fréquence élevée sont des boutons utilisés couramment dans une application. Les boutons Suivant et Précédent dans Microsoft Dynamics 365 Guides constituent un bon exemple.<br>
        <br>
        **Relatives**<br>
  * Les boutons à fréquence élevée doivent être volumineux, plus faciles à toucher avec le regard
  * Restez près de la hauteur pour éviter les tensions ergonomiques.<br>
        <br>
*Image : Microsoft Dynamics 365 guides Next Button*
    :::column-end:::
        :::column:::
       ![Bouton suivant de Microsoft Dynamics 365 guides](images/GuideNextButton.png)<br>
    :::column-end:::
:::row-end:::

<br>

---


### <a name="low-frequency-buttons"></a>Boutons à fréquence faible
Les boutons à fréquence faible sont les boutons avec lesquels l’utilisateur n’interagit pas aussi régulièrement tout au long de l’application. À titre d’exemple, citons un bouton permettant d’accéder à un menu de paramètres ou d’effacer la totalité du travail.

* Dans la mesure du possible, maintenez ces boutons hors du chemin emprunté par les suivis de la tête afin d’éviter une activation accidentelle. 

<br>

---

### <a name="confirmations"></a>Confirmations

:::row:::
    :::column:::
        Quand une action a un impact significatif, telle que le prélèvement d’une somme d’argent, la suppression d’un travail ou le démarrage d’un long processus, il est utile de vérifier que l’utilisateur a effectivement souhaité sélectionner le bouton lié à cette action.<br>
        <br>
        **Relatives**<br>
  * Afficher la surbrillance de la sélection sur le bouton principal
  * Révéler la cible de stabilisation en même temps que la surbrillance de la sélection
  * Pour le bouton secondaire, révéler la cible de stabilisation en fonction du suivi de la tête<br>
        <br>
*Image : boîte de dialogue de confirmation des guides Microsoft Dynamics 365*
    :::column-end:::
        :::column:::
       ![Boîte de dialogue de confirmation des guides Microsoft Dynamics 365](images/GuidesConfirmation.png)<br>
    :::column-end:::
:::row-end:::
        
<br>

---

### <a name="toggle-buttons"></a>Boutons bascule
Les boutons bascule nécessitent une logique nuancée pour fonctionner correctement. Quand l’utilisateur reste sur un bouton bascule et l’active, il doit quitter le bouton, puis revenir pour redémarrer la logique de stabilisation. Il est important que l’utilisateur puisse clairement identifier si un bouton bascule est à l’état actif ou inactif. 

<br>

---

### <a name="list-views"></a>Affichages Liste

:::row:::
    :::column:::
        Les affichages de liste présentent un défi particulier pour les entrées de point de vue et de point d’entrée. L’utilisateur doit être en mesure de balayer le contenu sans avoir le sentiment de devoir tâtonner autour des cibles de stabilisation.<br>
        <br>
**Relatives**<br>
  * Faites en sorte que la totalité de la ligne surbrille quand la tête est en regard, mais ne commence pas, sauf si le point de regard se trouve sur la cible d’un logement spécifique.
  * Affichez uniquement la cible d’un logement lorsque la ligne est mise en surbrillance pour réduire le bruit visuel.
  * Soyez clair et cohérent avec la position des cibles du logement.
  * N’affichez pas toutes les cibles de logement à la fois pour éviter l’interface utilisateur répétitive.
  * Réutilisez le même modèle aussi souvent que possible pour établir une familiarité avec l’expérience utilisateur.<br>
        <br>
*Image : liste des guides Microsoft Dynamics 365*
    :::column-end:::
        :::column:::
       ![Liste des guides Microsoft Dynamics 365](images/GuidesListView.png)<br>
    :::column-end:::
:::row-end:::

<br>

---
 
 ## <a name="see-also"></a>Articles associés
* [Point de regard et validation](gaze-and-commit.md)
* [Manipulation directe](direct-manipulation.md)
* [Mouvements pratiques](gaze-and-commit.md#composite-gestures)
* [Mains et validation](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Entrée vocale](voice-input.md)
