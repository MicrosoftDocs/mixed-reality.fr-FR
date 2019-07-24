---
title: Cible du visage
description: Toutes les interactions reposent sur la capacité d’un utilisateur à cibler l’élément avec lequel il souhaite interagir, quelle que soit la modalité d’entrée.
author: cre8ivepark
ms.author: jennyk
ms.date: 02/24/2019
ms.topic: article
keywords: La réalité mixte, le point de présence, le regard, l’interaction et la conception
ms.openlocfilehash: eddc832456b2ba0c6bc8955157d2c8e1a268e893
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829840"
---
# <a name="gaze-and-dwell"></a>Point de regard
Il existe de nombreuses façons de confirmer une _validation_ , par exemple la combinaison de point de présence avec des gestes de _voix_ ou de _main_.
Toutefois, il existe plusieurs scénarios utilisateur, dans lesquels les mains des utilisateurs peuvent être occupées ou ne peuvent pas être suivies (par exemple, les travailleurs de l’usine avec des gants de plus grande taille). L’entrée vocale n’est pas non plus disponible en raison des préférences de l’utilisateur, du contexte social ou des environnements bruyants.
En guise de solution de secours, une autre option pour effectuer une _validation_ consiste simplement à conserver les étoiles dans un élément d’interface utilisateur auquel nous faisons référence en tant que _logement_.
Un _logement_ peut être effectué en tête ou en regard. L’idée est simple et peut être décomposée selon les phases suivantes: 
1. L’utilisateur démarre Gazing à un bouton holographique

2. Après un bref délai d’apparition (par exemple, 150 MS), une animation de commentaires visuels est lancée. Le délai d’apparition est utilisé pour éviter de submerger l’utilisateur en affichant immédiatement des commentaires en permanence.
    - Pour les _yeux oculaires_, nous vous recommandons les éléments suivants pour la conception de commentaires sur le logement visuel:
      - **Mélanger**: Fusionnez en douceur les commentaires à partir de la première à la pleine opacité. Cela rend les commentaires moins gênants et overwhlemings et s’alignent avec la certitude que l’utilisateur veut vraiment s’associer à ce bouton.
      - **Extrayez-** la: Créez un retour visuel au-delà de la taille des sorties et évolue vers le centre de la cible, en tirant l’attention de l’utilisateur. 

3. Après une durée de remplissage prédéfinie (par exemple, 800 ms), le logement se termine et un événement associé est déclenché.
    - Fournissez des commentaires d’audit ou visuels de finalisation afin de faire en sorte que l’élément soit sélectionné maintenant.

![États du logement](images/eyes_dwellstate_recommendation.png)


# <a name="gaze-targeting"></a>Cible du visage

Toutes les interactions reposent sur la capacité d’un utilisateur à cibler l’élément avec lequel il souhaite interagir, quelle que soit la modalité d’entrée. Dans Windows Mixed Reality, cette opération fait généralement appel au pointage du regard de l’utilisateur.

Pour procurer une expérience efficace à un utilisateur, il est nécessaire que la compréhension de son intention telle que la calcule le système et son intention réelle soient alignées aussi étroitement que possible. Plus le système interprète les actions prévues de l’utilisateur correctement, plus la satisfaction augmente et les performances s’améliorent.

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Cible du visage</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
     <tr>
        <td>Ciblage oculaire</td>
        <td>❌</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

> [!NOTE]
> Plus d’instructions spécifiques à HoloLens 2 bientôt [disponible](index.md).

## <a name="target-sizing-and-feedback"></a>Dimensionnement des cibles et retour

Il a été démontré à plusieurs reprises que le vecteur du pointage du regard peut être utilisé pour le ciblage précis, mais qu’il convient souvent le mieux pour le ciblage brut (acquisition de cibles un peu plus grandes). Les tailles de cible minimales de 1 à 1,5 degré doivent permettre le bon déroulement des actions utilisateur dans la plupart des scénarios, bien que des cibles de 3 degrés puissent souvent générer un gain de vitesse. Notez que la taille que cible l’utilisateur est une zone 2D même pour les éléments 3D ; la projection qui lui fait face, quelle qu’elle soit, doit être la zone pouvant être ciblée. Il est extrêmement utile de fournir à l’utilisateur des indicateurs marquants montrant qu’un élément est « actif » (qu’il est en train de le cibler) ; il peut s’agir de traitements tels que des effets de « pointage » visibles, des mises en évidence audio, des clics ou de l’alignement clair d’un curseur avec un élément.

![Taille de cible optimale à une distance de 2 mètres](images/gazetargeting-size-1000px.jpg)<br>
*Taille de cible optimale à une distance de 2 mètres*

![Exemple de mise en surbrillance d’un objet ciblé avec le regard](images/gazetargeting-highlighting-640px.jpg)<br>
*Exemple de mise en surbrillance d’un objet ciblé avec le regard*

## <a name="target-placement"></a>Placement de la cible

Les utilisateurs ne parviennent pas souvent à trouver les éléments d’interface utilisateur qui sont positionnés très haut ou très bas dans leur champ de vision, concentrant la majeure partie de leur attention sur des zones autour de leur vue principale (généralement au niveau des yeux). Le fait de placer la plupart des cibles dans une bande raisonnable autour des yeux peut s’avérer utile. Etant donné que les utilisateurs ont tendance à se concentrer sur un champ visuel relativement étroit (le cône de vision lié à l’attention est à peu près de 10 degrés), ils sont davantage susceptibles de passer d’un élément à l’autre à mesure qu’ils déplacent leur regard si les éléments d’interface utilisateur d’un même concept sont regroupés dans ce champ de vision. Quand vous concevez l’interface utilisateur, gardez à l’esprit les grandes variations potentielles du champ de vision entre les casques immersifs et HoloLens.

![Exemple d’éléments d’interface utilisateur groupés pour faciliter le ciblage avec le regard dans Galaxy Explorer](images/gazetargeting-grouping-1000px.jpg)<br>
*Exemple d’éléments d’interface utilisateur groupés pour faciliter le ciblage avec le regard dans Galaxy Explorer*

## <a name="improving-targeting-behaviors"></a>Amélioration des comportements de ciblage

Si l’intention de l’utilisateur de cibler un élément peut être déterminée (ou approchée étroitement), il peut être très utile d’accepter comme correctes les tentatives d’interaction échouant de peu. Il existe un certain nombre de méthodes utiles pouvant être incorporées dans les expériences de réalité mixte :

### <a name="gaze-stabilization-gravity-wells"></a>Stabilisation du regard («puits de gravité»)

Cette technique doit être activée tout le temps ou la plupart du temps. Elle supprime les petits mouvements naturels de la tête ou du cou que l’utilisateur peut faire. Il en va de même des comportements liés à l’observation et à l’élocution.

### <a name="closest-link-algorithms"></a>Algorithmes du lien le plus proche

Ces derniers fonctionnent le mieux dans les zones dont le contenu interactif est clairsemé. S’il existe une forte probabilité que vous puissiez déterminer ce avec quoi un utilisateur a tenté d’interagir, vous pouvez compléter ses capacités de ciblage simplement en supposant un certain niveau d’intention.

### <a name="backdatingpostdating-actions"></a>Actions d’antidatage et de postdatage

Ce mécanisme est utile dans les tâches nécessitant de la vitesse. Lorsqu’un utilisateur parcourt une série de manoeuvres de ciblage/activation à la vitesse, il peut être utile d’avoir un intérêt et d’autoriser les *étapes manquées* à agir sur les cibles que l’utilisateur a placées plus légèrement avant ou légèrement après le TAP (50 ms avant/après). efficace dans les premiers tests).

### <a name="smoothing"></a>Adoucissage

Ce mécanisme est utile pour les mouvements de déplacement, réduisant les petits mouvements et les tremblements naturels de la tête. Quand vous adoucissez les mouvements de déplacement, agissez sur la taille/distance des mouvements plutôt que sur leur durée.

### <a name="magnetism"></a>Magnétisme

Ce mécanisme peut être considéré comme une version plus générale des algorithmes du « lien le plus proche » ; il consiste à déplacer un curseur vers une cible ou simplement à agrandir les zones de ciblage (visibles ou non) à mesure que l’utilisateur s’approche de cibles probables, en s’appuyant sur la disposition interactive pour mieux interpréter l’intention de l’utilisateur. Il peut être particulièrement efficace pour les petites cibles.

### <a name="focus-stickiness"></a>Adhérence du focus

Quand vous déterminez à quels éléments interactifs proches donner le focus, déportez-vous de l’élément qui a actuellement le focus. Cette approche aide à réduire les comportements erratiques liés aux changements de focus quand l’utilisateur se trouve entre deux éléments avec un bruit normal.

## <a name="see-also"></a>Voir aussi
* [Mouvements](gestures.md)
* [Commander avec la voix](voice-design.md)
* [Curseurs](cursors.md)
