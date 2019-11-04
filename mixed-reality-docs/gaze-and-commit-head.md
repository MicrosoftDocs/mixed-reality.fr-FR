---
title: Suivre de la tête et valider
description: Vue d’ensemble du modèle d’entrée Suivre de la tête et valider
author: caseymeekhof
ms.author: cmeekhof
ms.date: 03/31/2019
ms.topic: article
keywords: Mixed Reality, pointage du regard, ciblage avec le regard, interaction, conception
ms.openlocfilehash: 5fef778dde6852222e098aeb1cbb41fe04e0b744
ms.sourcegitcommit: a5dc182da237f63f0487d40a2e11894027208b6c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73441094"
---
# <a name="head-gaze-and-commit"></a>Suivre de la tête et valider
Le point de _regard et la validation de tête_ est un cas spécial du modèle d’entrée de pointage [et de validation](gaze-and-commit.md) qui implique le ciblage d’un objet avec la direction de la tête vers l’avant (direction de l’en-tête), puis l’action avec une entrée secondaire, telle que l’air de mouvement vers la main Appuyez sur ou sur la commande vocale « Select ». 

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
        <td>Suivre de la tête et valider</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé (troisième choix ; <a href="interaction-fundamentals.md">voir les autres options</a>)</td>
        <td>➕ Autre option</td>
    </tr>
</table>

---

## <a name="target-sizing-and-feedback"></a>Dimensionnement des cibles et retour
Le point de regard de l’en-tête a été affiché à plusieurs reprises pour être utilisable pour un ciblage précis, mais il fonctionne souvent mieux pour le ciblage brut, en acquérant des cibles de plus grande taille. Les tailles de cible minimales de 1 à 1,5 degrés permettent des actions utilisateur réussies dans la plupart des scénarios, bien que les cibles de 3 degrés offrent souvent une vitesse supérieure. Notez que la taille que cible l’utilisateur est une zone 2D même pour les éléments 3D ; la projection qui lui fait face, quelle qu’elle soit, doit être la zone pouvant être ciblée. Fournir une indication importante indiquant qu’un élément est « actif » (que l’utilisateur cible) est extrêmement utile. Cela peut inclure des traitements tels que des effets de « survol » visibles, des surbrillances audio ou des clics, ou l’alignement clair d’un curseur avec un élément.

![Taille optimale de la cible à une distance de 2 mètres](images/gazetargeting-size-1000px.jpg)<br>
*Taille optimale de la cible à une distance de 2 mètres*

<br>

![Exemple de mise en surbrillance d’un objet ciblé avec le regard](images/gazetargeting-highlighting-940px.jpg)<br>
*Exemple de mise en surbrillance d’un objet ciblé avec le regard*

## <a name="target-placement"></a>Placement de la cible
Souvent, les utilisateurs ne parviennent pas à trouver des éléments d’interface utilisateur qui sont positionnés très haut ou très bas dans leur champ de vision, en mettant l’accent sur les zones autour de leur objectif principal, ce qui est à peu près oculaire. Le fait de placer la plupart des cibles dans une bande raisonnable autour des yeux peut s’avérer utile. Etant donné que les utilisateurs ont tendance à se concentrer sur un champ visuel relativement étroit (le cône de vision lié à l’attention est à peu près de 10 degrés), ils sont davantage susceptibles de passer d’un élément à l’autre à mesure qu’ils déplacent leur regard si les éléments d’interface utilisateur d’un même concept sont regroupés dans ce champ de vision. Quand vous concevez l’interface utilisateur, gardez à l’esprit les grandes variations potentielles du champ de vision entre les casques immersifs et HoloLens.

![Exemple d’éléments d’interface utilisateur groupés pour faciliter le ciblage avec le regard dans Galaxy Explorer](images/gazetargeting-grouping-1000px.jpg)<br>
*Exemple d’éléments d’interface utilisateur groupés pour faciliter le ciblage avec le regard dans Galaxy Explorer*

## <a name="improving-targeting-behaviors"></a>Amélioration des comportements de ciblage
Si l’intention de l’utilisateur de cibler un événement peut être déterminée (ou approchée), il peut être très utile d’accepter des tentatives presque manquées à l’interaction comme si elles étaient ciblées correctement. Voici quelques-unes des méthodes qui peuvent être incorporées dans les expériences de réalité mixte :

### <a name="head-gaze-stabilization-gravity-wells"></a>Stabilisation avec suivi de la tête (« stabilisation de la gravité »)
Cette fonction doit être activée le plus ou la totalité du temps. Cette technique supprime les instabilités de tête et de cou naturelles que les utilisateurs peuvent avoir en mouvement en raison des comportements de recherche et de conversation.

### <a name="closest-link-algorithms"></a>Algorithmes du lien le plus proche
Ces derniers fonctionnent le mieux dans les zones dont le contenu interactif est clairsemé. S’il existe une forte probabilité que vous puissiez déterminer ce à quoi un utilisateur tente d’interagir, vous pouvez compléter ses capacités de ciblage en supposant un certain niveau d’intention.

### <a name="backdating-and-postdating-actions"></a>Actions d’postdating et de mise à jour
Ce mécanisme est utile dans les tâches nécessitant de la vitesse. Lorsqu’un utilisateur parcourt une série de manoeuvres de ciblage et d’activation à la vitesse, il est utile de prendre des mesures et d’autoriser les étapes manquées à agir sur les cibles que l’utilisateur a placées plus légèrement avant ou légèrement après le TAP (50 ms avant/après). test RLY).

### <a name="smoothing"></a>Adoucissage
Ce mécanisme est utile pour le tracé des mouvements, en réduisant les légères gigues et les tremblements dus aux caractéristiques naturelles de mouvement de la tête. En cas de lissage sur les mouvements de tracés, lisse par la taille et la distance des mouvements plutôt qu’au fil du temps.

### <a name="magnetism"></a>Magnétisme
Ce mécanisme peut être considéré comme une version plus générale des algorithmes de lien les plus proches : le fait de dessiner un curseur vers une cible ou d’augmenter simplement hitboxes, visuellement ou non, à mesure que les utilisateurs approchent les cibles probables en utilisant une connaissance de la disposition interactive pour mieux approche de l’intention de l’utilisateur. Il peut être particulièrement efficace pour les petites cibles.

### <a name="focus-stickiness"></a>Adhérence du focus
Lorsque vous déterminez les éléments interactifs proches auxquels donner le focus, l’adhérence au focus fournit un décalage à l’élément qui est actuellement concentré. Cela permet de réduire les comportements de changement de focus erratiques lorsqu’ils flottent à un point médian entre deux éléments avec un bruit naturel.


## <a name="see-also"></a>Articles associés
* [Interaction basée sur les yeux](eye-gaze-interaction.md)
* [Pointer du regard et fixer](gaze-and-dwell.md)
* [Manipulation directe](direct-manipulation.md)
* [Mouvements pratiques](gaze-and-commit.md#composite-gestures)
* [Mains et validation](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Entrée vocale](voice-input.md)



