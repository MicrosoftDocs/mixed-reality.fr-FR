---
title: Ciblage des regards
description: Toutes les interactions reposent sur la capacité d’un utilisateur à cibler l’élément qu'ils souhaitent interagir, quelle que soit la modalité d’entrée.
author: cre8ivepark
ms.author: jennyk
ms.date: 02/24/2019
ms.topic: article
keywords: Mixte réalité, les regards, les regards ciblant, interaction, concevoir
ms.openlocfilehash: 1ac4f06208a7574fced0a7e27e93469ec93bf6e0
ms.sourcegitcommit: 90ce9415889e7121dd2fd76a893dc3734672881b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64873926"
---
# <a name="gaze-and-dwell"></a>Regards et durée d’affichage
Il existe un grand nombre de différentes façons pour confirmer une _validation_ telles que la combinaison des regards avec _voix_ ou _main mouvements_.
Il existe plusieurs scénarios utilisateur Cependant, dans lequel les utilisateurs peuvent être occupés ou ne peut pas être suivies (par exemple, les travailleurs de fabrique avec des gants lourds volumineux). Entrée vocale également peut-être pas disponible en raison des préférences de l’utilisateur, contexte de réseaux sociaux ou environnements bruyants.
Comme une solution de secours, une autre option pour effectuer un _validation_ consiste simplement à conserver fixant un élément d’interface utilisateur que nous appelons _m’attarderai pas_.
Un _m’attarderai pas_ peuvent être effectuées avec des regards head ou yeux. L’idée est simple et peut être décomposée dans les phases suivantes : 
1. Utilisateur démarre gazing à un bouton HOLOGRAPHIQUE

2. Après un délai bref apparition (par exemple, 150 ms), une animation de rétroaction visuelle est démarrée. Le délai de début est utilisé pour éviter de surcharger l’utilisateur en affichant immédiatement des commentaires tout le temps.
    - Pour _les regards yeux_, nous vous recommandons de commentaires m’attarderai pas les éléments suivants pour la conception de l’élément visuel :
      - **Blend il**: Fondre dans les commentaires à partir d’à peine visible à tout d’abord à totalement opaque. Les commentaires est ainsi moins de détourner votre attention et overwhleming et bien s’aligne avec la certitude que le système que l’utilisateur souhaite collaborer avec ce bouton.
      - **Tirez-la**: Créer une rétroaction visuelle que diminue en taille et la déplace vers le centre de la cible, en extrayant des attention visuelle de l’utilisateur. 

3. Après une durée de la durée d’affichage prédéfinis (par exemple, 800 ms), la durée d’affichage se termine et déclenchement d’un événement associé.
    - Fournir certains finalisation auditifs ou des commentaires visuels à réellement mettre accueil que l’élément a été sélectionné maintenant.

![M’attarderai pas États](images/eyes_dwellstate_recommendation.png)


# <a name="gaze-targeting"></a>Ciblage des regards

Toutes les interactions reposent sur la capacité d’un utilisateur à cibler l’élément qu'ils souhaitent interagir, quelle que soit la modalité d’entrée. En réalité mixte Windows, cela s’effectue en général à l’aide regard de l’utilisateur.

Pour permettre aux utilisateurs de travailler avec une expérience avec succès, présentation de calculée du système de l’intention de l’utilisateur et l’intention de réelle de l’utilisateur, doit être alignées aussi près que possible. Dans la mesure que le système interprète les actions prévues de l’utilisateur correctement, la satisfaction des augmentations et les performances améliore.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Fonctionnalité</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1er gen)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> Ciblage des regards</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;">✔️ </td>
</tr><tr>
<td> Ciblage des yeux</td><td style="text-align: center;"></td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md).

## <a name="target-sizing-and-feedback"></a>Commentaires et dimensionnement de la cible

Le vecteur du pointage de regard a été démontré à plusieurs reprises pour être utilisable pour le ciblage précis, mais souvent convient le mieux brutes ciblage (lors de l’acquisition un tantinet supérieure cibles). Les tailles cible minimale de 1 à 1.5 degrés doivent autoriser les actions utilisateur réussie dans la plupart des scénarios, bien que les cibles de degrés 3 permettent souvent pour améliorer la vitesse. Notez que la taille que les cibles de l’utilisateur est effectivement une zone 2D même pour les éléments 3D--quelle que soit la projection est accessible sur les doit correspondre à la zone pouvant être ciblée. Fournissant certains cue marquants qu’un élément est « actif » (que l’utilisateur cible il) est extrêmement utile : il peut s’agir traitements tels que des effets visibles « pointage », mises en surbrillance audio ou clics, ou désactivez l’alignement d’un curseur avec un élément.

![Taille cible optimal à distance de compteur 2](images/gazetargeting-size-1000px.jpg)<br>
*Taille cible optimal à distance de compteur 2*

![Un exemple de mise en surbrillance d’un objet ciblé du pointage de regard](images/gazetargeting-highlighting-640px.jpg)<br>
*Un exemple de mise en surbrillance d’un objet ciblé du pointage de regard*

## <a name="target-placement"></a>Placement de la cible

Utilisateurs échouent souvent rechercher des éléments d’interface utilisateur sont positionnés très élevé ou très faible dans leur champ de vision, se concentrant la majeure partie de leur attention sur des zones autour de leur vue principale (généralement à peu près yeux). Peut aider à placer la plupart des cibles dans certaines bande raisonnable autour des yeux. Étant donné la tendance pour les utilisateurs pour vous concentrer sur une zone visual relativement réduite à tout moment (cône l’attention de vision est à peu près 10 degrés), regroupement des éléments d’interface utilisateur au degré que qu’ils sont conceptuellement associés peut exploiter le chaînage l’attention des comportements à partir de élément à un autre en tant qu’utilisateur empruntant leurs regards une zone. Lorsque vous concevez l’interface utilisateur, gardez à l’esprit les grandes variations dans le champ de vision entre HoloLens et des casques IMMERSIFS potentielles.

![Un exemple d’éléments de l’interface utilisateur groupés pour des regards plus facile de ciblage dans l’Explorateur de Galaxy](images/gazetargeting-grouping-1000px.jpg)<br>
*Un exemple d’éléments de l’interface utilisateur groupés pour des regards plus facile de ciblage dans l’Explorateur de Galaxy*

## <a name="improving-targeting-behaviors"></a>Amélioration des comportements de ciblage

Si l’intention de l’utilisateur pour cibler un élément peut être déterminée (ou approximative étroitement), il peut être très utile accepter les tentatives de « near miss » à l’interaction comme s’ils ont été correctement ciblés. Il existe un certain nombre de méthodes réussites qui peuvent être incorporées dans les expériences de réalité mixte :

### <a name="gaze-stabilization-gravity-wells"></a>Utilisation de stabilisation (« wells gravité »)

Cela doit être allumé/all de la plupart du temps. Cette technique supprime le gigues du tête/cou naturel que les utilisateurs devront peut-être. Également le déplacement en raison de comportements de recherche/parler.

### <a name="closest-link-algorithms"></a>Algorithmes de lien le plus proche

Ceux-ci fonctionnent le mieux dans les zones épars contenu interactif. S’il existe une forte probabilité que vous pouvez déterminer qu’un utilisateur a tenté d’interagir avec, vous pouvez compléter leurs capacités de ciblage par simplement en supposant que certain niveau d’objectif.

### <a name="backdatingpostdating-actions"></a>Actions postdatage/postdating

Ce mécanisme est utile dans les tâches nécessitant de vitesse. Lorsqu’un utilisateur se déplace à travers une série de manœuvres/activation ciblant à la vitesse, il peut être utile pour supposent une intention et permettre *manqué étapes* pour agir sur les cibles de l’utilisateur avait le focus légèrement avant ou peu après le (appuyez sur 50 ms avant/après était en vigueur dans les premiers tests).

### <a name="smoothing"></a>Lissage

Ce mécanisme est utile pour les mouvements de chemins, en réduisant l’instabilité/OSCILLANT légère en raison des caractéristiques physiques mouvement de la tête. Lorsque le lissage sur les mouvements des chemins, smooth par taille/distance de mouvements plutôt qu’au fil du temps

### <a name="magnetism"></a>Magnétisme

Ce mécanisme peut être considéré comme une version plus générale d’algorithmes de « Lier le plus proche », un curseur vers une cible de dessin ou l’augmentation simplement hitboxes (qu’il soit visible ou non) que les utilisateurs s’approcher des objectifs probables, à l’aide de la disposition interactive à une certaine connaissance intention de l’utilisateur une meilleure approche. Cela peut être particulièrement efficace pour les petites cibles.

### <a name="focus-stickiness"></a>Le focus adhérence

Lorsque vous déterminez ce qui les plus proches des éléments interactifs pour donner le focus à, fournir un décalage à l’élément ayant le focus. Cela vous aidera à réduire le focus erratique commutation des comportements flottant à un point médian entre deux éléments avec bruit naturelle.

## <a name="see-also"></a>Voir aussi
* [Mouvements](gestures.md)
* [Conception de la voix](voice-design.md)
* [Curseurs](cursors.md)
