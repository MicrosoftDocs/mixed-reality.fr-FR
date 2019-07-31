---
title: Manipulation directe avec les mains
description: Vue d’ensemble du modèle d’entrée de manipulation directe
author: caseymeekhof
ms.author: cmeekhof
ms.date: 04/02/2019
ms.topic: article
ms.localizationpriority: high
keywords: Réalité mixte, pointage du regard, ciblage par pointage du regard, interaction, conception, à portée de main, HoloLens
ms.openlocfilehash: 8047d7549309d293b805dc43e44da99f9139e5c6
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414439"
---
# <a name="direct-manipulation-with-hands"></a>Manipulation directe avec les mains
La manipulation directe est un modèle d’entrée qui consiste à toucher les hologrammes directement avec les mains. L’idée de la manipulation directe est de faire en sorte que les objets se comportent exactement comme dans le monde réel. Vous pouvez activer les boutons simplement en appuyant dessus, vous pouvez saisir les objets en les agrippant, et le contenu 2D se comporte comme un écran tactile virtuel. C’est pourquoi la manipulation directe est facile à apprendre pour les utilisateurs et amusante. Elle est considérée comme un modèle d’entrée « proche », car elle est utilisée de préférence pour interagir avec le contenu situé à portée de main.

La manipulation directe est basée sur l’affordance, ce qui la rend conviviale. Les utilisateurs n’ont pas à apprendre de mouvements symboliques. Toutes les interactions reposent sur un élément visuel que vous pouvez toucher ou saisir.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<colgroup>
    <col width="33%" />
    <col width="22%" />
    <col width="22%" />
    <col width="22%" />
</colgroup>
<tr>
     <td><strong>Modèle d’entrée</strong></td>
     <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
     <td><strong>HoloLens 2</strong></td>
     <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
</tr>
<tr>
     <td>Manipulation directe avec les mains</td>
     <td>❌ Non pris en charge</td>
     <td>✔️ Recommandé</td>
     <td>➕ Une solution, telle que <a href="point-and-commit.md">pointer et valider avec les mains</a>, est recommandée.</td>
    
</tr>
</table>


La manipulation directe est l’un des principaux modèles d’entrée sur HoloLens 2. Elle utilise le nouveau système de suivi des mains articulé. Le modèle d’entrée est également disponible sur les casques immersifs via l’utilisation de contrôleurs de mouvement, mais il n’est pas recommandé en tant que mode principal d’interaction en dehors de la manipulation d’objets. La manipulation directe n’est pas disponible sur HoloLens (1re génération).


## <a name="collidable-fingertip"></a>Pointe de doigt avec détection de collision

Sur HoloLens 2, les mains de l’utilisateur sont reconnues et interprétées en tant que modèles du squelette des mains gauche et droite. Pour implémenter l’idée consistant à toucher les hologrammes directement avec les mains, l’idéal serait d’attacher cinq colliders (détecteurs de collision) aux cinq pointes de doigt de chaque modèle du squelette de la main. Toutefois, en raison de l’absence de rétroaction tactile, dix bouts de doigts avec détection de collision donnent lieu à des collisions inattendues et imprévisibles avec les hologrammes. 

Nous suggérons donc de placer uniquement un collider sur chaque index. Les pointes d’index avec détection de collision peuvent toujours servir de points tactiles actifs pour les divers mouvements tactiles impliquant d’autres doigts, par exemple la pression à 1 doigt, le clic à 1 doigt, la pression à 2 doigts et la pression à 5 doigts, comme illustré dans l’image ci-dessous.

![Image d’une pointe de doigt avec détection de collision](images/Collidable-Fingertip-720px.jpg)

### <a name="sphere-collider"></a>Collider sphérique

Au lieu d’utiliser une forme générique aléatoire, nous vous suggérons d’utiliser un collider de sphère. Ensuite, affichez-le visuellement pour fournir de meilleures indications de ciblage proche. Le diamètre de la sphère doit correspondre à l’épaisseur de l’index pour augmenter la précision tactile. Il est plus facile de récupérer la variable de l’épaisseur du doigt en appelant l’API relative à la main.

### <a name="fingertip-cursor"></a>Curseur à la pointe du doigt

En plus du rendu d’une sphère avec détection de collision à la pointe de l’index, nous avons créé un curseur à la pointe du doigt pour vivre une meilleure expérience interactive de ciblage interactif proche. Il s’agit d’un curseur en forme d’anneau attaché à la pointe de l’index. En fonction de la proximité, il réagit de manière dynamique à l’orientation et à la taille d’une cible, comme indiqué ci-dessous :

* Quand un index se déplace vers un hologramme, le curseur est toujours parallèle à la surface de l’hologramme et réduit progressivement sa taille.
* Dès que le doigt touche la surface, le curseur se réduit en un point et émet un événement tactile.

Grâce à une rétroaction interactive, les utilisateurs disposent d’une haute précision pour les tâches de ciblage proche, par exemple le déclenchement d’un lien hypertexte ou la pression sur un bouton, comme illustré ci-dessous. 

![Image de curseur à la pointe du doigt](images/Fingertip-Cursor-720px.jpg)

## <a name="bounding-box-with-proximity-shader"></a>Rectangle englobant avec nuanceur de proximité

L’hologramme lui-même doit également pouvoir fournir une rétroaction visuelle et audio pour compenser le manque de rétroaction tactile. Pour cela, nous générons le concept de rectangle englobant avec un nuanceur de proximité. Un rectangle englobant est une zone volumétrique minimale qui entoure un objet 3D. Le rectangle englobant comporte un mécanisme de rendu interactif appelé nuanceur de proximité. Le nuanceur de proximité se comporte comme suit :

* Quand l’index se trouve dans la plage appropriée, un faisceau lumineux situé à la pointe du doigt est projeté à la surface du rectangle englobant.
* Plus la pointe du doigt se rapproche de la surface, plus le faisceau lumineux projeté est réduit.
* Dès que la pointe du doigt touche la surface, tout le rectangle englobant change de couleur ou génère des effets visuels pour refléter l’état tactile.
* Il est également possible d’activer un effet sonore pour améliorer la rétroaction tactile visuelle.

![Image de rectangle englobant avec nuanceur de proximité](images/Bounding-Box-With-Proximity-Shader-720px.jpg)

## <a name="pressable-button"></a>Bouton sur lequel appuyer

Avec une pointe de doigt pourvue de la détection de collision, les utilisateurs sont désormais prêts à interagir avec le composants d’IU holographique fondamental, à savoir un bouton sur lequel appuyer. Ce type de bouton est un composant holographique conçu pour une pression directe à l’aide du doigt. Là encore, en raison du manque de rétroaction tactile, un bouton sur lequel il est possible d’appuyer associe deux mécanismes pour traiter les problèmes de rétroaction tactile.

* Le premier mécanisme est un rectangle englobant avec nuanceur de proximité, détaillé dans la section précédente. Il offre aux utilisateurs une meilleure sensation de proximité lors de l’approche et du contact avec un bouton.
* Le second mécanisme est une dépression. La dépression crée une sensation de pression lorsque le doigt entre en contact avec un bouton. Grâce à ce mécanisme, le bouton se déplace étroitement avec la pointe du doigt dans l’axe de profondeur. Le bouton peut se déclencher quand il atteint une profondeur déterminée (l’utilisateur appuie sur le bouton) ou quand il quitte cette profondeur (l’utilisateur relâche le bouton).
* Il est possible d’ajouter un effet sonore pour améliorer la rétroaction quand le bouton se déclenche.

![Image d’un bouton sur lequel appuyer](images/Pressable-Button-720px.jpg)

## <a name="2d-slate-interaction"></a>Interaction avec une tablette 2D

Une tablette 2D est un conteneur holographique hébergeant le contenu d’applications 2D, par exemple un navigateur web. L’interaction avec une tablette 2D par manipulation directe consiste à exploiter le modèle mental de l’interaction avec un écran tactile physique.

Pour interagir avec la tablette par contact :

* Utilisez l’index pour appuyer sur un lien hypertexte ou un bouton.
* Utilisez l’index pour faire défiler le contenu de la tablette vers le haut et vers le bas.
* Les deux index de l’utilisateur sont utilisés pour effectuer un zoom avant ou arrière sur le contenu de la tablette en fonction du mouvement relatif des doigts.

![Image de tablette 2D](images/2D-Slate-Interaction-720px.jpg)

Pour manipuler la tablette 2D elle-même :

* Approchez vos mains des coins et des bords pour faire apparaître les affordances de manipulation les plus proches.
* Saisissez les affordances de manipulation, puis effectuez une montée en charge uniforme via les affordances d’angle et effectuez un ajustage dynamique via les affordances de bord.
* Saisissez l’holobar en haut de la tablette 2D pour pouvoir déplacer la tablette entière.

![Image de la manipulation de la tablette](images/Manipulate-2d-slate-720px.jpg)

## <a name="3d-object-manipulation"></a>Manipulation d’objet 3D

HoloLens 2 permet aux utilisateurs de manipuler directement des objets holographiques 3D en appliquant un rectangle englobant à chaque objet 3D. La rectangle englobant offre une meilleure perception de la profondeur grâce à son nuanceur de proximité. Avec le rectangle englobant, il existe deux approches de conception pour la manipulation d’objets 3D.

### <a name="affordance-based-manipulation"></a>Manipulation basée sur l’affordance

La manipulation basée sur l’affordance vous permet de manipuler l’objet 3D via un rectangle englobant avec les affordances de manipulation qui l’entourent. Dès que la main d’un utilisateur est proche d’un objet 3D, le rectangle englobant et l’affordance la plus proche apparaissent. Les utilisateurs peuvent se saisir du rectangle englobant pour déplacer l’objet entier, des affordances de bord pour le faire pivoter et des affordances d’angle pour le mettre à l’échelle de manière uniforme.

![Image de manipulation d’objet 3D](images/3D-Object-Manipulation-720px.jpg)

### <a name="non-affordance-based-manipulation"></a>Manipulation non basée sur l’affordance

La manipulation sans affordance n’attache pas l’affordance au cadre englobant. Les utilisateurs peuvent uniquement faire apparaître le rectangle englobant, puis interagir directement avec celui-ci. Si les utilisateurs se saisissent du rectangle englobant à une seule main, la translation et la rotation de l’objet sont associées au mouvement et à l’orientation de la main. Quand les utilisateurs se saisissent de l’objet à deux mains, ils peuvent le translater, le mettre à l’échelle et le faire pivoter en fonction des mouvements relatifs des deux mains.

Une manipulation spécifique nécessite de la précision. Nous vous recommandons d’utiliser la **manipulation basée sur l’affordance**, car elle offre un haut niveau de granularité. Pour une manipulation flexible, nous vous recommandons d’utiliser la **manipulation sans affordance**, car elle offre une approche instantanée et ludique.

## <a name="instinctual-gestures"></a>Mouvements instinctifs

Avec HoloLens (1ère génération), nous avons montré aux utilisateurs quelques mouvements prédéfinis, tels qu’écarter les doigts paume vers le haut et cliquer dans l'air. Avec HoloLens 2, nous ne demandons pas aux utilisateurs de mémoriser des mouvements symboliques. Tous les mouvements nécessaires de l’utilisateur qui lui permettent d’interagir avec les hologrammes et le contenu sont instinctifs. Les mouvements instinctifs doivent aider les utilisateurs à effectuer des mouvements via les affordances d’IU conçues à cet effet.

Par exemple, si nous encourageons l’utilisateur à saisir un objet ou un point de contrôle en le pinçant avec deux doigts, l’objet ou le point de contrôle doit être petit. Si nous souhaitons que l’utilisateur le saisisse avec cinq doigts, l’objet ou le point de contrôle doit être relativement grand. Si nous prenons l’exemple des boutons, un tout petit bouton oblige les utilisateurs à appuyer dessus avec un seul doigt ; un gros bouton incite les utilisateurs à appuyer dessus avec la paume de la main.

![](images/Instinctual-Gestures-720px.jpg)

## <a name="symmetric-design-between-hands-and-6-dof-controllers"></a>Conception symétrique entre les mains et les contrôleurs 6DoF

Vous avez peut-être remarqué que nous pouvons établir des parallèles au niveau de l’interaction entre les mains en environnement AR (réalité augmentée) et les contrôleurs de mouvement en environnement VR (réalité virtuelle). Les deux entrées peuvent être utilisées pour déclencher des manipulations directes dans leurs environnements respectifs. Avec HoloLens 2, la saisie et le déplacement à l’aide des mains à courte distance fonctionnent de la même manière que le bouton de saisie des contrôleurs de mouvement WMR. Cela permet aux utilisateurs d’accéder à des interactions familières sur les deux plateformes. De plus, cela peut s’avérer utile si vous décidez de porter votre application d’une plateforme à l’autre.

## <a name="optimize-with-eye-tracking"></a>Optimiser avec l’eye-tracking

La manipulation directe peut paraître magique si elle fonctionne comme prévu. Mais elle peut également devenir rapidement frustrante si vous ne pouvez pas bouger votre main sans déclencher involontairement un hologramme. L’eye-tracking peut éventuellement aider à mieux identifier l’intention de l’utilisateur.

* **Quand** : Réduisez le déclenchements par inadvertance d’une réponse à une manipulation. L’eye-tracking permet de mieux comprendre l’engagement de l’utilisateur.
Par exemple, supposons que vous lisiez un texte holographique (instructions) quand vous tendez la main pour saisir votre outil de travail réel.

En procédant ainsi, vous passez accidentellement votre main sur des boutons holographiques interactifs que vous n’aviez même pas remarqués auparavant (peut-être même situés en dehors du champ de vision de l’utilisateur (FoV)).

  Pour faire court : Si l’utilisateur n’a pas regardé un hologramme depuis un certain temps et si un événement tactile ou de saisie a été détecté, il est probable que l’utilisateur n’avait pas réellement l’intention d’interagir avec cet hologramme.

* **Lequel** :  En plus du traitement des activations correspondant à des faux positifs, il est également possible d’améliorer l’identification des hologrammes à saisir ou à pousser, car le point d’intersection n’est pas forcément clair selon votre perspective, surtout si plusieurs hologrammes sont proches les uns des autres.

  Bien que l’eye-tracking sur HoloLens 2 soit parfois limité au niveau de la précision avec laquelle il évalue votre suivi du regard, il peut être très utile pour les interactions rapprochées en raison de la disparité de la profondeur quand vous interagissez avec la saisie manuelle. Cela signifie qu’il est parfois difficile de déterminer si votre main est placée derrière ou devant un hologramme pour saisir avec précision un widget de manipulation, par exemple.

* **Où** : Utilisez les informations relatives à ce qu’un utilisateur regarde avec des mouvements rapides. Saisissez un hologramme et lancez-le à peu près vers l’emplacement souhaité.  

    Bien que cela fonctionne parfois, les mouvements rapides de la main peuvent cibler des emplacements très imprécis. Dans ce scénario, le suivi oculaire peut améliorer la précision du mouvement.

## <a name="see-also"></a>Voir également

* [Suivre de la tête et valider](gaze-and-commit.md)
* [Pointer et valider avec les mains](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)

