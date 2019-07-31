---
title: Pointer et valider avec les mains
description: Vue d’ensemble du modèle d’entrée Pointer et valider
author: caseymeekhof
ms.author: cmeekhof
ms.date: 04/05/2019
ms.topic: article
ms.localizationpriority: high
keywords: Réalité mixte, interaction, conception, hololens, mains, éloigné, pointer et valider
ms.openlocfilehash: 4e19a7fd95bac42283ce3e3176a1363afda8f220
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414538"
---
# <a name="point-and-commit-with-hands"></a>Pointer et valider avec les mains
Grâce au modèle d’entrée Pointer et valider avec les mains, les utilisateurs peuvent cibler, sélectionner et manipuler du contenu 2D et des objets 3D à distance. Cette technique d’interaction « éloignée » est propre à la réalité mixte et ne constitue pas pour les humains une méthode d’interaction naturelle avec le monde réel. Par exemple, dans le film de super-héros *X-Men*, le personnage [Magnéto](https://en.wikipedia.org/wiki/Magneto_(comics)) peut atteindre et manipuler des objets éloignés avec les mains. Ce n’est pas quelque chose que les humains peuvent faire dans la réalité. Dans HoloLens (réalité augmentée) et dans la réalité mixte (MR), nous dotons les utilisateurs de ce pouvoir magique, éliminant ainsi les contraintes physiques du monde réel pour proposer une expérience amusante avec le contenu holographique et rendre les interactions des utilisateurs plus efficaces.

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
     <td>Pointer et valider avec les mains</td>
     <td>❌ Non pris en charge</td>
     <td>✔️ Recommandé</td>
     <td>✔️ Recommandé</td>
</tr>
</table>


Le modèle d’entrée Pointer et valider, aussi appelé « hands far » (mains éloignées), est l’une des fonctionnalités récemment introduites qui exploitent le nouveau système de suivi des mains articulées. Il constitue également le principal modèle d’entrée sur les casques immersifs équipés de contrôleurs de mouvement.

## <a name="hand-rays"></a>Rayon émanant de la main

Sur HoloLens 2, nous avons créé un rayon qui sort du centre de la paume de la main de l’utilisateur. Ce rayon est traité comme une extension de la main. Un curseur en forme d’anneau apparaît à l’extrémité du rayon pour indiquer à quel emplacement le rayon croise un objet cible. L’objet sur lequel le curseur atterrit peut alors recevoir des commandes gestuelles de la main.

Les commandes gestuelles de base sont déclenchées par un clic dans l’air, effectué avec le pouce et l’index. En utilisant le rayon émanant de la main pour pointer et un clic dans l’air pour valider, les utilisateurs peuvent activer un bouton ou un lien hypertexte. Des mouvements plus composites permettent aux utilisateurs de naviguer dans le contenu web et de manipuler des objets 3D à distance. La conception visuelle du rayon doit également réagir aux états de pointage et de validation décrits et illustrés ci-dessous : 

* Dans l’état de *pointage*, le rayon est une ligne en pointillés et le curseur un anneau.
* Dans l’état de *validation*, le rayon se transforme en ligne continue et le curseur est réduit à un point.

![États de pointage et de validation pour les rayons émanant de la main](images/Hand-Rays-720px.jpg)<br>
*États de pointage (à gauche) et de validation (à droite) pour les rayons émanant de la main*

## <a name="transition-between-near-and-far"></a>Transition entre le contenu proche et éloigné

Au lieu d’utiliser des mouvements spécifiques comme « pointer avec l’index » pour diriger le rayon, nous avons conçu celui-ci pour sortir du centre de la paume de la main. Nous libérons ainsi les cinq doigts qui peuvent être utilisés pour effectuer d’autres mouvements, comme pincer et saisir. Cette conception nous permet de créer un seul modèle mental prenant en charge le même ensemble de mouvements de la main pour les interactions avec du contenu proche ou éloigné. Vous pouvez utiliser le même mouvement de saisie pour manipuler des objets à différentes distances. L’appel des rayons est automatique et basé sur la proximité comme suit :

*  Quand un objet est à portée de main (environ 50 cm), les rayons sont automatiquement désactivés pour encourager l’interaction proche.
*  Si l’objet se trouve à plus de 50 cm, les rayons sont activés. La transition doit être fluide et transparente.

![Le même ensemble de mouvements de la main est utilisé pour l’interaction proche et éloigné](images/Transition-Between-Near-And-Far-720px.jpg)<br>
*Le même ensemble de mouvements de la main est utilisé pour l’interaction proche et éloignée.*

## <a name="2d-slate-interaction"></a>Interaction avec une tablette 2D

Une tablette 2D est un conteneur holographique hébergeant le contenu d’applications 2D comme un navigateur web. Le concept de l’interaction éloignée avec une ardoise 2D est le suivant : les utilisateurs se servent du rayon émanant de la main pour cibler un objet et effectuent un clic dans l’air pour le sélectionner. Après avoir ciblé un élément à l’aide du rayon, ils peuvent cliquer dans l’air pour déclencher un lien hypertexte ou un bouton. D’une main, ils peuvent « cliquer dans l’air et faire glisser » pour faire défiler le contenu de la tablette vers le haut et vers le bas. Le mouvement relatif des deux mains pour cliquer dans l’air et faire glisser permet de faire un zoom avant ou arrière sur le contenu de l’ardoise.

Le fait de cibler le rayon émanant de la main au niveau des coins et des bords permet de révéler l’affordance de manipulation la plus proche. En « saisissant et en faisant glisser » des affordances de manipulation, les utilisateurs peuvent effectuer une montée en charge uniforme (affordances de coin) et ajuster dynamiquement la tablette (affordances de bord). Saisir la barre holographique située en haut de la tablette 2D et la faire glisser permet aux utilisateurs de déplacer toute la tablette.

![Interaction avec une tablette 2D](images/2D-Slate-Interaction-Far-720px.jpg)

Pour manipuler la tablette 2D :<br>

* Les utilisateurs pointent le rayon émanant de la main au niveau des coins ou des bords pour révéler l’affordance de manipulation la plus proche. 
* En appliquant un mouvement de manipulation sur l’affordance, les utilisateurs peuvent effectuer une montée en charge uniforme (affordance de coin) et ajuster dynamiquement l’ardoise (affordance de bord). 
* En appliquant un mouvement de manipulation sur la barre holographique située en haut de la tablette 2D, les utilisateurs peuvent déplacer la tablette entière.<br>

<br>

## <a name="3d-object-manipulation"></a>Manipulation d’objet 3D

En manipulation directe, les utilisateurs ont le choix entre deux méthodes pour manipuler des objets 3D : la manipulation basée sur l’affordance et la manipulation non basée sur l’affordance. Dans le modèle Pointer et valider, les utilisateurs peuvent accomplir exactement les mêmes tâches à l’aide du rayon émanant de la main. Aucun apprentissage supplémentaire n’est nécessaire.<br>

### <a name="affordance-based-manipulation"></a>Manipulation basée sur l’affordance
Les utilisateurs utilisent le rayon émanant de la main pour pointer sur un objet et faire apparaître le cadre englobant et les affordances de manipulation. Les utilisateurs peuvent appliquer le mouvement de manipulation sur le cadre englobant pour déplacer l’objet entier, sur les affordances de bord pour faire pivoter l’objet et sur les affordances de coin pour effectuer une mise à l’échelle uniforme. <br>

![Manipulation basée sur l’affordance](images/3D-Object-Manipulation-Far-720px.jpg) <br>


### <a name="non-affordance-based-manipulation"></a>Manipulation non basée sur l’affordance
Les utilisateurs pointent sur un objet à l’aide du rayon émanant de la main pour faire apparaître le cadre englobant, puis appliquent directement des mouvements de manipulation à cet objet. Avec une main, la translation et la rotation de l’objet sont associées au mouvement et à l’orientation de la main. Avec les deux mains, les utilisateurs peuvent translater, mettre à l’échelle et faire pivoter l’objet selon les mouvements relatifs des deux mains.<br>

<br>

## <a name="instinctual-gestures"></a>Mouvements instinctifs
Le concept de mouvements instinctifs pour pointer et valider est similaire à celui de la [manipulation directe avec les mains](direct-manipulation.md). Les mouvements que les utilisateurs effectuent sur un objet 3D sont guidés par la conception des affordances de l’interface utilisateur. Par exemple, un petit point de contrôle peut inciter les utilisateurs à le pincer avec le pouce et l’index, tandis qu’un utilisateur peut souhaiter saisir un objet plus volumineux à l’aide de ses cinq doigts.

![Mouvements instinctifs](images/Instinctual-Gestures-Far-720px.jpg)<br>

## <a name="symmetric-design-between-hands-and-6-dof-controller"></a>Conception symétrique entre les mains et le contrôleur 6DoF 
Le concept Pointer et valider pour l’interaction éloignée a été initialement créé et défini pour le portail de réalité mixte (MRP), dans lequel un utilisateur porte un casque immersif et interagit avec des objets 3D à l’aide de contrôleurs de mouvement. Les contrôleurs de mouvement émettent des rayons pour pointer et manipuler des objets éloignés. Les contrôleurs sont équipés de boutons pour valider différentes actions. Nous exploitons le modèle d’interaction des rayons et les fixons aux deux mains. Grâce à cette conception symétrique, les utilisateurs qui sont familiarisés avec MRP ne sont pas contraints d’apprendre un autre modèle d’interaction pour pointer sur un objet éloigné et le manipuler quand ils utilisent HoloLens 2, et inversement.    

![Conception symétrique entre les mains et le contrôleur 6DoF](images/Symmetric-Design-For-Rays-720px.jpg)<br>


## <a name="see-also"></a>Voir également
* [Suivre de la tête et valider](gaze-and-commit.md)
* [Manipulation directe avec les mains](direct-manipulation.md)
* [Interactions instinctuelles](interaction-fundamentals.md)

