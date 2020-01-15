---
title: Manipulation directe avec les mains
description: Vue d’ensemble du modèle d’entrée de manipulation directe
author: caseymeekhof
ms.author: cmeekhof
ms.date: 04/02/2019
ms.topic: article
ms.localizationpriority: high
keywords: Réalité mixte, pointage du regard, ciblage par pointage du regard, interaction, conception, à portée de main, HoloLens
ms.openlocfilehash: 6811fe0b09ecff1ddc76d9df9ddc440f9c934ce3
ms.sourcegitcommit: 6844930427b658ae31f642c395cd8a3b3cdbf857
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75723248"
---
# <a name="direct-manipulation-with-hands"></a>Manipulation directe avec les mains

![Bouton](images/UX/UX_Hero_Manipulation.jpg)

La manipulation directe est un modèle d’entrée qui consiste à toucher les hologrammes directement avec les mains. L’idée derrière ce concept est de faire en sorte que les objets se comportent exactement comme dans le monde réel. Vous pouvez activer les boutons simplement en appuyant dessus, vous pouvez saisir les objets en les agrippant, et le contenu 2D se comporte comme un écran tactile virtuel. C’est pourquoi la manipulation directe est facile à apprendre pour les utilisateurs et amusante. Elle est considérée comme un modèle d’entrée « proche », car elle est utilisée de préférence pour interagir avec le contenu situé à portée de main.

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
     <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
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

<br>

---

## <a name="collidable-fingertip"></a>Pointe de doigt avec détection de collision

Sur HoloLens 2, les mains de l’utilisateur sont reconnues et interprétées en tant que modèles du squelette des mains gauche et droite. Pour implémenter l’idée consistant à toucher les hologrammes directement avec les mains, l’idéal serait d’attacher cinq colliders (détecteurs de collision) aux cinq pointes de doigt de chaque modèle du squelette de la main. Toutefois, en raison de l’absence de rétroaction tactile, dix bouts de doigts avec détection de collision donnent lieu à des collisions inattendues et imprévisibles avec les hologrammes. 

Nous suggérons donc de placer uniquement un collider sur chaque index. Les pointes d’index avec détection de collision peuvent toujours servir de points tactiles actifs pour les divers mouvements tactiles impliquant d’autres doigts, par exemple l’appui avec un doigt, le clic à un doigt, l’appui avec deux doigts et l’appui avec cinq doigts, comme illustré dans l’image ci-dessous.

:::row:::
    :::column:::
       ![Pointe de doigt avec détection de collision](images/Collidable-Fingertip.jpg)<br>
       **Pointe de doigt avec détection de collision**<br>
    :::column-end:::
    :::column:::
       ![Appui avec un doigt](images/Collidable-Fingertip-1-finger-press.jpg)<br>
        **Appui avec un doigt**<br>
    :::column-end:::
    :::column:::
       ![Clic à un doigt](images/Collidable-Fingertip-1-finger-tap.jpg)<br>
       **Clic à un doigt**<br>
    :::column-end:::
    :::column:::
       ![Appui avec cinq doigts](images/Collidable-Fingertip-5-finger-press.jpg)<br>
       **Appui avec cinq doigts**<br>
    :::column-end:::
:::row-end:::

<br>

---

### <a name="sphere-collider"></a>Collider sphérique

Au lieu d’utiliser une forme générique aléatoire, nous vous suggérons d’utiliser un collider de sphère. Ensuite, vous pouvez l’afficher visuellement pour fournir de meilleures indications de ciblage proche. Le diamètre de la sphère doit correspondre à l’épaisseur de l’index pour augmenter la précision tactile. Il est plus facile de récupérer la variable de l’épaisseur du doigt en appelant l’API relative à la main.

### <a name="fingertip-cursor"></a>Curseur à la pointe du doigt

En plus du rendu d’une sphère avec détection de collision à la pointe de l’index, nous avons créé un curseur à la pointe du doigt pour vivre une meilleure expérience interactive de ciblage interactif proche. Il s’agit d’un curseur en forme d’anneau attaché à la pointe de l’index. En fonction de la proximité, il réagit de manière dynamique à l’orientation et à la taille d’une cible, comme indiqué ci-dessous :

* Quand un index se déplace vers un hologramme, le curseur est toujours parallèle à la surface de l’hologramme et réduit progressivement sa taille.
* Dès que le doigt touche la surface, le curseur se réduit en un point et émet un événement tactile.

Grâce à une rétroaction interactive, les utilisateurs disposent d’une haute précision pour les tâches de ciblage proche, par exemple le déclenchement d’un lien hypertexte ou la pression sur un bouton, comme illustré ci-dessous. 

:::row:::
    :::column:::
       ![Curseur à la pointe du doigt éloigné](images/Fingertip-cursor-far.jpg)<br>
       **Curseur à la pointe du doigt éloigné**<br>
    :::column-end:::
    :::column:::
       ![Curseur à la pointe du doigt proche](images/Fingertip-cursor-near.jpg)<br>
        **Curseur à la pointe du doigt proche**<br>
    :::column-end:::
    :::column:::
       ![Curseur à la pointe du doigt en contact](images/Fingertip-cursor-contact.jpg)<br>
       **Curseur à la pointe du doigt en contact**<br>
    :::column-end:::
:::row-end:::

<br>



## <a name="bounding-box-with-proximity-shader"></a>Rectangle englobant avec nuanceur de proximité

L’hologramme lui-même doit également pouvoir fournir une rétroaction visuelle et audio pour compenser le manque de rétroaction tactile. Pour cela, nous générons le concept de rectangle englobant avec un nuanceur de proximité. Un rectangle englobant est une zone volumétrique minimale qui entoure un objet 3D. Le rectangle englobant comporte un mécanisme de rendu interactif appelé nuanceur de proximité. Le nuanceur de proximité se comporte comme suit :

:::row:::
    :::column:::
       ![Pointage (éloigné) avec retour visuel](images/bounding-box-with-proximity-shader-hover-far.jpg)<br>
       **Pointage (éloigné)**<br>
       Quand l’index se trouve dans la plage appropriée, un faisceau lumineux situé à la pointe du doigt est projeté à la surface du rectangle englobant.
    :::column-end:::
    :::column:::
       ![Pointage (proche) avec retour visuel](images/bounding-box-with-proximity-shader-hover-near.jpg)<br>
        **Pointage (proche)**<br>
        Plus la pointe du doigt se rapproche de la surface, plus le faisceau lumineux projeté est réduit.
    :::column-end:::
    :::column:::
       ![Début du contact](images/bounding-box-with-proximity-shader-begin-contact.jpg)<br>
       **Début du contact**<br>
       Dès que la pointe du doigt touche la surface, tout le rectangle englobant change de couleur ou génère des effets visuels pour refléter l’état tactile.
    :::column-end:::
    :::column:::
       ![Fin du contact](images/bounding-box-with-proximity-shader-end-contact.jpg)<br>
       **Fin du contact**<br>
       Il est également possible d’activer un effet sonore pour améliorer la rétroaction tactile visuelle.
    :::column-end:::
:::row-end:::

<br>

---

## <a name="pressable-button"></a>Bouton sur lequel appuyer

Avec une pointe de doigt pourvue de la détection de collision, les utilisateurs sont désormais prêts à interagir avec un composant d’IU holographique fondamental, à savoir un bouton sur lequel appuyer. Ce type de bouton est un composant holographique conçu pour une pression directe à l’aide du doigt. Là encore, en raison du manque de rétroaction tactile, un bouton sur lequel il est possible d’appuyer associe deux mécanismes pour traiter les problèmes de rétroaction tactile.

* Le premier mécanisme est un rectangle englobant avec nuanceur de proximité, détaillé dans la section précédente. Il offre aux utilisateurs une meilleure sensation de proximité lors de l’approche et du contact avec un bouton.
* Le second mécanisme est une dépression. La dépression crée une sensation de pression lorsque le doigt entre en contact avec un bouton. Ce mécanisme permet de veiller à ce que le bouton se déplace étroitement avec la pointe du doigt dans l’axe de profondeur. Le bouton peut se déclencher quand il atteint une profondeur déterminée (l’utilisateur appuie sur le bouton) ou quand il quitte cette profondeur (l’utilisateur relâche le bouton).
* Il est possible d’ajouter un effet sonore pour améliorer la rétroaction quand le bouton se déclenche.

:::row:::
    :::column:::
       ![Bouton sur lequel appuyer éloigné](images/pressable-button-far.jpg)<br>
       **Doigt éloigné**<br>
    :::column-end:::
    :::column:::
       ![Bouton sur lequel appuyer proche](images/pressable-button-approach.jpg)<br>
        **Doigt en approche**<br>
    :::column-end:::
    :::column:::
       ![Début du contact avec le bouton sur lequel appuyer](images/pressable-button-contact.jpg)<br>
       **Début du contact**<br>
    :::column-end:::
    :::column:::
       ![Appui sur le bouton sur lequel appuyer](images/pressable-button-press.jpg)<br>
       **Appui**<br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="2d-slate-interaction"></a>Interaction avec une tablette 2D

Une [tablette](slate.md) 2D est un conteneur holographique utilisé pour héberger le contenu d’applications 2D comme un navigateur web. L’interaction avec une tablette 2D par manipulation directe consiste à exploiter le modèle mental de l’interaction avec un écran tactile physique.

### <a name="to-interact-with-the-slate-contact"></a>Pour interagir avec la tablette par contact

:::row:::
    :::column:::
       ![Interface tactile](images/2d-slate-interaction-touch.jpg)<br>
       **Interface tactile**<br>
       Utilisez l’index pour appuyer sur un lien hypertexte ou un bouton.
    :::column-end:::
    :::column:::
       ![Faire défiler](images/2d-slate-interaction-scroll2.jpg)<br>
        **Faire défiler**<br>
        Utilisez l’index pour faire défiler le contenu de la tablette vers le haut et vers le bas.
    :::column-end:::
    :::column:::
       ![Zoom](images/2d-slate-interaction-zoom2.jpg)<br>
       **Zoom**<br>
       Les deux index de l’utilisateur sont utilisés pour effectuer un zoom avant ou arrière sur le contenu de la tablette en fonction du mouvement relatif des doigts.
    :::column-end:::
:::row-end:::


### <a name="for-manipulating-the-2d-slate-itself"></a>Pour manipuler la tablette 2D

:::row:::
    :::column:::
       ![Déplacer](images/manipulate-2d-slate-move.jpg)<br>
       **Déplacer**<br>
       Déplacez vos mains vers les coins et les bords pour faire apparaître les affordances de manipulation les plus proches. Saisissez la barre holographique en haut de la tablette 2D pour pouvoir déplacer la tablette entière.
    :::column-end:::
    :::column:::
       ![Mettre à l’échelle](images/manipulate-2d-slate-scale.jpg)<br>
        **Mettre à l’échelle**<br>
        Saisissez les affordances de manipulation, puis effectuez une mise à l’échelle uniforme par le biais des affordances d’angle.
    :::column-end:::
    :::column:::
       ![Ajuster dynamiquement](images/manipulate-2d-slate-reflow.jpg)<br>
       **Ajuster dynamiquement**<br>
       Saisissez les affordances de manipulation, puis effectuez un ajustement dynamique par le biais des affordances de bord.
    :::column-end:::
:::row-end:::

<br>

---


## <a name="3d-object-manipulation"></a>Manipulation d’objet 3D

HoloLens 2 permet aux utilisateurs de diriger et manipuler des objets holographiques 3D en appliquant un rectangle englobant à chaque objet 3D. La rectangle englobant offre une meilleure perception de la profondeur grâce à son nuanceur de proximité. Avec le rectangle englobant, il existe deux approches de conception pour la manipulation d’objets 3D.

### <a name="affordance-based-manipulation"></a>Manipulation basée sur l’affordance

La manipulation basée sur l’affordance vous permet de manipuler l’objet 3D via un rectangle englobant avec les affordances de manipulation qui l’entourent. 

:::row:::
    :::column:::
       ![Déplacer](images/3d-object-manipulation-move.jpg)<br>
       **Déplacer**<br>
       Dès que la main d’un utilisateur est proche d’un objet 3D, le rectangle englobant et l’affordance la plus proche apparaissent. Les utilisateurs peuvent saisir le rectangle englobant pour déplacer l’objet entier.
    :::column-end:::
    :::column:::
       ![Faire pivoter](images/3d-object-manipulation-rotate.jpg)<br>
        **Faire pivoter**<br>
        Les utilisateurs peuvent saisir les affordances de bord pour effectuer une rotation.
    :::column-end:::
    :::column:::
       ![Mettre à l’échelle](images/3d-object-manipulation-scale.jpg)<br>
       **Mettre à l’échelle**<br>
       Les utilisateurs peuvent saisir les affordances d’angle pour effectuer une mise à l’échelle uniforme.
    :::column-end:::
:::row-end:::

<br>


### <a name="non-affordance-based-manipulation"></a>Manipulation non basée sur l’affordance

La manipulation sans affordance n’attache pas l’affordance au cadre englobant. Les utilisateurs peuvent uniquement faire apparaître le rectangle englobant, puis interagir directement avec celui-ci. Si les utilisateurs se saisissent du rectangle englobant à une seule main, la translation et la rotation de l’objet sont associées au mouvement et à l’orientation de la main. Quand les utilisateurs se saisissent de l’objet à deux mains, ils peuvent le translater, le mettre à l’échelle et le faire pivoter en fonction des mouvements relatifs des deux mains.

Une manipulation spécifique nécessite de la précision. Nous vous recommandons d’utiliser la **manipulation basée sur l’affordance**, car elle offre un haut niveau de granularité. Pour une manipulation flexible, nous vous recommandons d’utiliser la **manipulation sans affordance**, car elle offre une approche instantanée et ludique.

<br>

---


## <a name="instinctual-gestures"></a>Mouvements instinctifs

Avec HoloLens (1re génération), nous avons montré aux utilisateurs quelques mouvements prédéfinis, tels qu’écarter les doigts paume vers le haut et cliquer dans l’air. Avec HoloLens 2, nous ne demandons pas aux utilisateurs de mémoriser des mouvements symboliques. Tous les mouvements nécessaires à l’utilisateur qui lui permettent d’interagir avec les hologrammes et le contenu sont instinctifs. Les mouvements instinctifs doivent aider les utilisateurs à effectuer des mouvements via les affordances d’IU conçues à cet effet.

Par exemple, si nous encourageons l’utilisateur à saisir un objet ou un point de contrôle en le pinçant avec deux doigts, l’objet ou le point de contrôle doit être petit. Si nous souhaitons que l’utilisateur le saisisse avec cinq doigts, l’objet ou le point de contrôle doit être relativement grand. Si nous prenons l’exemple des boutons, un tout petit bouton oblige les utilisateurs à appuyer dessus avec un seul doigt ; un gros bouton incite les utilisateurs à appuyer dessus avec la paume de la main.


:::row:::
    :::column:::
       ![Déplacer](images/instinctual-gestures-smallobject.jpg)<br>
       **Petit objet**<br>
    :::column-end:::
    :::column:::
       ![Faire pivoter](images/instinctual-gestures-mediumobject.jpg)<br>
        **Objet de taille moyenne**<br>
    :::column-end:::
    :::column:::
       ![Mettre à l’échelle](images/instinctual-gestures-largeobject.jpg)<br>
       **Objet volumineux**<br>
    :::column-end:::
:::row-end:::


<br>

---

<br>

## <a name="symmetric-design-between-hands-and-6-dof-controllers"></a>Conception symétrique entre les mains et les contrôleurs 6DoF

Vous avez peut-être remarqué que nous pouvons établir des parallèles au niveau de l’interaction entre les mains en environnement AR (réalité augmentée) et les contrôleurs de mouvement en environnement VR (réalité virtuelle). Les deux entrées peuvent être utilisées pour déclencher des manipulations directes dans leurs environnements respectifs. Avec HoloLens 2, la saisie et le déplacement à l’aide des mains à courte distance fonctionnent de la même manière que le bouton de saisie des contrôleurs de mouvement WMR. Cela permet aux utilisateurs d’accéder à des interactions familières sur les deux plateformes. De plus, cela peut s’avérer utile si vous décidez de porter votre application d’une plateforme à l’autre.

<br>

---

## <a name="optimize-with-eye-tracking"></a>Optimiser avec l’eye-tracking

La manipulation directe peut paraître magique si elle fonctionne comme prévu. Mais elle peut également devenir frustrante si vous ne pouvez pas bouger votre main sans déclencher involontairement un hologramme. Le suivi oculaire peut vous aider à mieux identifier l’intention de l’utilisateur.

* **Quand** : Réduisez le déclenchements par inadvertance d’une réponse à une manipulation. L’eye-tracking permet de mieux comprendre l’engagement de l’utilisateur.
Par exemple, supposons que vous lisiez un texte holographique (instructions) quand vous tendez la main pour saisir votre outil de travail réel.

En procédant ainsi, vous passez accidentellement votre main sur des boutons holographiques interactifs que vous n’aviez même pas remarqués auparavant (par exemple, situés en dehors du champ de vision de l’utilisateur (FoV)).

  Pour faire court : Si l’utilisateur n’a pas regardé un hologramme depuis un certain temps et si un événement tactile ou de saisie a été détecté, il est probable que l’utilisateur n’avait pas réellement l’intention d’interagir avec cet hologramme.

* **Lequel** :  En plus du traitement des activations correspondant à des faux positifs, il est également possible d’améliorer l’identification des hologrammes à saisir ou à pousser, car le point d’intersection n’est pas forcément clair selon votre perspective, surtout si plusieurs hologrammes sont proches les uns des autres.

  Bien que le suivi oculaire sur HoloLens 2 soit parfois limité au niveau de la précision avec laquelle il évalue votre regard, il peut être très utile pour les interactions rapprochées en raison de la disparité de la profondeur quand vous interagissez avec la saisie manuelle. Cela signifie qu’il est parfois difficile de déterminer si votre main est placée derrière ou devant un hologramme pour saisir avec précision un widget de manipulation, par exemple.

* **Où** : Utilisez les informations relatives à ce qu’un utilisateur regarde avec des mouvements rapides. Saisissez un hologramme et lancez-le à peu près vers l’emplacement souhaité.  

    Bien que cela fonctionne parfois, les mouvements rapides de la main peuvent cibler des emplacements très imprécis. Toutefois, le suivi oculaire peut améliorer la précision du mouvement.

<br>

---

## <a name="manipulation-in-mrtk-mixed-reality-toolkit-for-unity"></a>Manipulation dans MRTK (Mixed Reality Toolkit) pour Unity
Avec **[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)** , vous pouvez facilement obtenir un comportement de manipulation courant à l’aide du script **ManipulationHandler**. Avec ManipulationHandler, vous pouvez saisir et déplacer les objets directement avec les mains ou avec un rayon émanant de la main. Il prend également en charge les manipulations à deux mains pour la mise à l’échelle et la rotation des objets.

* [MRTK - Manipulation](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html)


---

## <a name="see-also"></a>Voir aussi

* [Suivre de la tête et valider](gaze-and-commit.md)
* [Pointer et valider avec les mains](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
