---
title: Pointer et valider avec les mains
description: Vue d’ensemble du modèle d’entrée Pointer et valider
author: caseymeekhof
ms.author: cmeekhof
ms.date: 04/05/2019
ms.topic: article
ms.localizationpriority: high
keywords: Réalité mixte, interaction, conception, HoloLens, mains, éloigné, pointer et valider
ms.openlocfilehash: 77c596f5250240d436529e879434a8f508b06732
ms.sourcegitcommit: 781e47db2ca2f2c792c95e76ac309b44b3535555
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/15/2019
ms.locfileid: "74105988"
---
# <a name="point-and-commit-with-hands"></a>Pointer et valider avec les mains

![Curseurs](images/UX/UX_Hero_HandRay.jpg)

Grâce au modèle d’entrée Pointer et valider avec les mains, les utilisateurs peuvent cibler, sélectionner et manipuler du contenu 2D et des objets 3D hors de portée. Cette technique d’interaction « éloignée » est propre à la réalité mixte et ne constitue pas pour les humains une méthode d’interaction naturelle avec le monde réel. Par exemple, dans le film de super-héros *X-Men*, le personnage [Magnéto](https://en.wikipedia.org/wiki/Magneto_(comics)) peut atteindre et manipuler des objets éloignés avec les mains. Ce n’est pas quelque chose que les humains peuvent faire dans la réalité. Dans HoloLens (réalité augmentée) et dans la réalité mixte, nous dotons les utilisateurs de ce pouvoir magique, éliminant ainsi les contraintes physiques du monde réel pour proposer une expérience amusante avec le contenu holographique et rendre les interactions des utilisateurs plus efficaces.

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
     <td>Pointer et valider avec les mains</td>
     <td>❌ Non pris en charge</td>
     <td>✔️ Recommandé</td>
     <td>✔️ Recommandé</td>
</tr>
</table>


Le modèle d’entrée _« Pointer et valider »_ est l’une des fonctionnalités récemment introduites qui exploitent le nouveau système de suivi des mains articulées. Il constitue également le principal modèle d’entrée sur les casques immersifs équipés de contrôleurs de mouvement.

<br>

---

## <a name="hand-rays"></a>Rayon émanant de la main

Sur HoloLens 2, nous avons créé un rayon qui sort du centre de la paume de la main de l’utilisateur. Ce rayon est traité comme une extension de la main. Un curseur en forme d’anneau apparaît à l’extrémité du rayon pour indiquer à quel emplacement le rayon croise un objet cible. L’objet sur lequel le curseur atterrit peut alors recevoir des commandes gestuelles de la main.

Les commandes gestuelles de base sont déclenchées par un clic dans l’air, effectué avec le pouce et l’index. En utilisant le rayon émanant de la main pour pointer et un clic dans l’air pour valider, les utilisateurs peuvent activer un bouton ou un lien hypertexte. Des mouvements plus composites permettent aux utilisateurs de naviguer dans le contenu web et de manipuler des objets 3D à distance. La conception visuelle du rayon doit également réagir aux états de pointage et de validation décrits et illustrés ci-dessous : 

:::row:::
    :::column:::
        ![rayons émanant de la main en pointage](images/hand-rays-pointing.jpg)<br>
        **État de pointage**<br>
        Dans l’état de *pointage*, le rayon est une ligne en pointillés et le curseur un anneau.
    :::column-end:::
    :::column:::
        ![rayons émanant de la main en validation](images/hand-rays-commit.jpg)<br>
        **État de validation**<br>
        Dans l’état de *validation*, le rayon se transforme en ligne continue et le curseur est réduit à un point.
    :::column-end:::
:::row-end:::

<br>

---


## <a name="transition-between-near-and-far"></a>Transition entre le contenu proche et éloigné

Au lieu d’utiliser des mouvements spécifiques comme « pointer avec l’index » pour diriger le rayon, nous avons conçu celui-ci pour sortir du centre de la paume de la main. Nous libérons ainsi les cinq doigts qui peuvent être utilisés pour effectuer d’autres mouvements, comme pincer et saisir. Cette conception nous permet de créer un seul modèle mental. Le même ensemble de mouvements de la main est utilisé pour les interactions avec du contenu proche ou éloigné. Vous pouvez utiliser le même mouvement de saisie pour manipuler des objets à différentes distances. L’appel des rayons est automatique et basé sur la proximité comme suit :

:::row:::
    :::column:::
        ![Manipulation proche](images/transition-near-manipulation.jpg)<br>
        **Manipulation proche**<br>
        Quand un objet est à portée de main (environ 50 cm), les rayons sont automatiquement désactivés pour encourager l’interaction proche.
    :::column-end:::
    :::column:::
        ![Manipulation éloignée](images/transition-far-manipulation.jpg)<br>
        **Manipulation éloignée**<br>
        Si l’objet se trouve à plus de 50 cm, les rayons sont activés. La transition doit être fluide et transparente.
    :::column-end:::
:::row-end:::

<br>

---

## <a name="2d-slate-interaction"></a>Interaction avec une tablette 2D

Une tablette 2D est un conteneur holographique hébergeant le contenu d’applications 2D comme un navigateur web. Le concept de l’interaction éloignée avec une ardoise 2D est le suivant : les utilisateurs se servent du rayon émanant de la main pour cibler un objet et effectuent un clic dans l’air pour le sélectionner. Après avoir ciblé un élément à l’aide du rayon, ils peuvent cliquer dans l’air pour déclencher un lien hypertexte ou un bouton. D’une main, ils peuvent « cliquer dans l’air et faire glisser » pour faire défiler le contenu de la tablette vers le haut et vers le bas. Le mouvement relatif des deux mains pour cliquer dans l’air et faire glisser permet de faire un zoom avant ou arrière sur le contenu de l’ardoise.

Le fait de cibler le rayon émanant de la main au niveau des coins et des bords permet de révéler l’affordance de manipulation la plus proche. En « saisissant et en faisant glisser » des affordances de manipulation, les utilisateurs peuvent effectuer une montée en charge uniforme (affordances de coin) et ajuster dynamiquement la tablette (affordances de bord). Saisir la barre holographique située en haut de la tablette 2D et la faire glisser permet aux utilisateurs de déplacer toute la tablette.

:::row:::
    :::column:::
       ![Clic d’interaction avec une tablette 2D](images/2d-slate-interaction-click.jpg)<br>
       **Clic**<br>
    :::column-end:::
    :::column:::
       ![Défilement d’interaction avec une tablette 2D](images/2d-slate-interaction-scroll.jpg)<br>
        **Faire défiler**<br>
    :::column-end:::
    :::column:::
       ![Zoom d’interaction avec une tablette 2D](images/2d-slate-interaction-zoom.jpg)<br>
       **Zoom**<br>
    :::column-end:::
:::row-end:::

<br>

**Pour manipuler la tablette 2D**<br>

* Les utilisateurs pointent le rayon émanant de la main au niveau des coins ou des bords pour révéler l’affordance de manipulation la plus proche. 
* En appliquant un mouvement de manipulation sur l’affordance, les utilisateurs peuvent effectuer une montée en charge uniforme (affordance de coin) et ajuster dynamiquement l’ardoise (affordance de bord). 
* En appliquant un mouvement de manipulation sur la barre holographique située en haut de la tablette 2D, les utilisateurs peuvent déplacer la tablette entière.<br>


<br>

---

## <a name="3d-object-manipulation"></a>Manipulation d’objet 3D

En manipulation directe, les utilisateurs ont le choix entre deux méthodes pour manipuler des objets 3D : la manipulation basée sur l’affordance et la manipulation non basée sur l’affordance. Dans le modèle Pointer et valider, les utilisateurs peuvent accomplir exactement les mêmes tâches à l’aide du rayon émanant de la main. Aucun apprentissage supplémentaire n’est nécessaire.<br>

### <a name="affordance-based-manipulation"></a>Manipulation basée sur l’affordance
Les utilisateurs utilisent le rayon émanant de la main pour pointer sur un objet et faire apparaître le cadre englobant et les affordances de manipulation. Les utilisateurs peuvent appliquer le mouvement de manipulation sur le cadre englobant pour déplacer l’objet entier, sur les affordances de bord pour faire pivoter l’objet et sur les affordances de coin pour effectuer une mise à l’échelle uniforme. <br>

:::row:::
    :::column:::
       ![Déplacement éloigné lors d’une manipulation d’objet 3D](images/3d-object-manipulation-far-move.jpg)<br>
       **Déplacer**<br>
    :::column-end:::
    :::column:::
       ![Rotation éloignée lors d’une manipulation d’objet 3D](images/3d-object-manipulation-far-rotate.jpg)<br>
        **Faire pivoter**<br>
    :::column-end:::
    :::column:::
       ![Mise à l’échelle éloignée lors d’une manipulation d’objet 3D](images/3d-object-manipulation-far-scale.jpg)<br>
       **Mettre à l’échelle**<br>
    :::column-end:::
:::row-end:::


### <a name="non-affordance-based-manipulation"></a>Manipulation non basée sur l’affordance
Les utilisateurs pointent sur un objet à l’aide du rayon émanant de la main pour faire apparaître le cadre englobant, puis appliquent directement des mouvements de manipulation à cet objet. Avec une main, la translation et la rotation de l’objet sont associées au mouvement et à l’orientation de la main. Avec les deux mains, les utilisateurs peuvent translater, mettre à l’échelle et faire pivoter l’objet selon les mouvements relatifs des deux mains.<br>

<br>

---

## <a name="instinctual-gestures"></a>Mouvements instinctifs
Le concept de mouvements instinctifs pour pointer et valider est similaire à celui de la [manipulation directe avec les mains](direct-manipulation.md). Les mouvements que les utilisateurs effectuent sur un objet 3D sont guidés par la conception des affordances de l’interface utilisateur. Par exemple, un petit point de contrôle peut inciter les utilisateurs à le pincer avec le pouce et l’index, tandis qu’un utilisateur peut souhaiter saisir un objet plus volumineux à l’aide de ses cinq doigts.

:::row:::
    :::column:::
       ![Mouvements instinctifs sur objet éloigné de petite taille](images/instinctual-gestures-far-smallobject.jpg)<br>
       **Petit objet**<br>
    :::column-end:::
    :::column:::
       ![Mouvements instinctifs sur objet éloigné de taille moyenne](images/instinctual-gestures-far-mediumobject.jpg)<br>
        **Objet de taille moyenne**<br>
    :::column-end:::
    :::column:::
       ![Mouvements instinctifs sur objet éloigné volumineux](images/instinctual-gestures-far-largeobject.jpg)<br>
       **Objet volumineux**<br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="symmetric-design-between-hands-and-6-dof-controller"></a>Conception symétrique entre les mains et le contrôleur 6DoF 

Le concept Pointer et valider pour l’interaction éloignée a été initialement créé et défini pour le portail de réalité mixte (MRP), dans lequel un utilisateur porte un casque immersif et interagit avec des objets 3D à l’aide de contrôleurs de mouvement. Les contrôleurs de mouvement émettent des rayons pour pointer et manipuler des objets éloignés. Les contrôleurs sont équipés de boutons pour valider différentes actions. Nous exploitons le modèle d’interaction des rayons et les fixons aux deux mains. Grâce à cette conception symétrique, les utilisateurs qui sont familiarisés avec MRP ne sont pas contraints d’apprendre un autre modèle d’interaction pour pointer sur un objet éloigné et le manipuler quand ils utilisent HoloLens 2, et inversement.    

:::row:::
    :::column:::
        ![Conception symétrique pour les rayons avec des contrôleurs](images/symmetric-design-for-rays-controllers.jpg)<br>
        **Rayons de contrôleur**<br>
    :::column-end:::
    :::column:::
        ![Conception symétrique pour les rayons avec les mains](images/symmetric-design-for-rays-hands.jpg)<br>
        **Rayons émanant de la main**<br>
    :::column-end:::
:::row-end:::

<br>


---

## <a name="hand-ray-in-mrtkmixed-reality-toolkit-for-unity"></a>Rayon émanant de la main dans MRTK (Mixed Reality Toolkit) pour Unity
Par défaut, MRTK fournit un préfabriqué de rayon émanant de la main ([DefaultControllerPointer.prefab](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.SDK/Features/UX/Prefabs/Pointers)) qui a le même état visuel que le rayon système du shell. Il est assigné dans le profil d’entrée de MRTK, sous Pointers. Dans le casque immersif Windows Mixed Reality, les mêmes rayons sont aussi utilisés pour les contrôleurs de mouvement.

* [MRTK - Profil de pointeur](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html#pointer-configuration)
* [MRTK - Système d’entrée](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html)
* [MRTK - Pointeurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Pointers.html)


---

## <a name="see-also"></a>Voir également
* [Manipulation directe avec les mains](direct-manipulation.md)
* [Pointer et valider](gaze-and-commit.md)
* [Mains : Manipulation directe](direct-manipulation.md)
* [Mains : Mouvements](gaze-and-commit.md#composite-gestures)
* [Interactions instinctuelles](interaction-fundamentals.md)