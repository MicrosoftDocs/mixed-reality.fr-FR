---
title: Point et validation
description: Vue d’ensemble du modèle d’entrée point et de validation
author: caseymeekhof
ms.author: cmeekhof
ms.date: 04/05/2019
ms.topic: article
keywords: Mixte réalité, interaction, concevoir
ms.openlocfilehash: e0e9c97053734ac0125fce40be7ffe9afbd2dd68
ms.sourcegitcommit: f5c1dedb3b9e29f27f627025b9e7613931a7ce18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2019
ms.locfileid: "64581309"
---
# <a name="point-and-commit"></a>Point et validation
Point et validation est un modèle d’entrée permet aux utilisateurs à cibler, sélectionner et manipuler le contenu 2D et 3D objets dans une distance. Cette technique d’interaction de « Loin » est une expérience interactive le nombril étant humaine n’avions pas vraiment pendant leurs interactions quotidiennes avec le monde réel. Par exemple, dans un film super héros, magnéto est capable de contacter et de manipulation d’un objet lointain via les mains dans une distance, mais humaines ne pouvez pas le faire en réalité. Dans Microsoft HoloLens (AR) et réalité mixte de Microsoft (VR), nous doter les utilisateurs cette puissance magique, avec rupture de la contrainte physique du monde réel non seulement pour avoir une expérience optimale à vos de contenu HOLOGRAPHIQUE mais pour renforcer l’efficacité de l’interaction et efficace.

## <a name="device-support"></a>Prise en charge des appareils
<table>
    <colgroup>
    <col width="40%" />
    <col width="20%" />
    <col width="20%" />
    <col width="20%" />
    </colgroup>
    <tr>
        <td><strong>Modèle d’entrée</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1er gen)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
    </tr>
     <tr>
        <td>Point et validation (interaction lointain main)</td>
        <td>❌ Ne pas pris en charge</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé</td>
    </tr>
</table>
<br>
Point de validation a été l’un des modèles d’entrée principales sur HoloLens 2, utilisant la main articulée nouveau système de suivi. Ce modèle d’entrée est également le modèle d’entrée principal sur des casques IMMERSIFS grâce à l’utilisation de contrôleurs de mouvement. Point et validation est le modèle d’entrée que nous suggérons pour remplacer l’utilisation de tête et de validation sur HoloLens (1er gen). 

## <a name="hand-rays"></a>Rayons de main
Sur HoloLens 2, nous créons un rayon de main prise de vue à partir du centre d’un palm. Le rayon est traité comme une extension de la main. Un curseur de forme de graphique en anneau est attaché à la fin du rayon à impliquent l’emplacement où le rayon en intersection avec un objet hitted. L’objet accède le curseur reçoit les commandes de geste à partir de la main. 

La commande de geste très basique est déclenchée à l’aide de pouce et votre index pour effectuer le geste d’appui air. À l’aide de ray de main pour pointer et appuyez sur validation, les utilisateurs peuvent activer un bouton ou un lien hypertexte sur un contenu web. Les gestes composites plus, les utilisateurs sont capables de navigation du contenu web et la manipulation des objets 3D dans une distance. La conception visuelle du rayon main doit réagir également pour pointer et valider des États : <br>
* Dans l’état de pointage, le rayon est dash inline, et le curseur se trouve une forme de graphique en anneau.
* dans l’état de validation, le rayon se transforme en une ligne pleine et le curseur est réduit à un point.<br><br>
![](images/Hand-Rays-720px.jpg)<br>

## <a name="transition-between-near-and-far"></a>La transition entre près et lointain
Au lieu d’utiliser des gestes spécifiques, par ex., pointant avec votre index pour diriger le rayon, nous concevons le rayon sort à partir du centre de palm, libérer et de réserver les cinq doigts pour plusieurs manipulations de geste. Par conséquent, HoloLens 2 prend en charge exactement le même ensemble de mouvements de main pour l’interaction proche et lointain. Aucun apprentissage supplémentaire n’est nécessaire lorsque les utilisateurs de transit de trouve à proximité d’interactions lointain et vice versa. Utilisateurs peuvent utiliser le même mouvement de manipulation pour manipuler des objets à des distances différentes. L’appel des rayons est automatique et proximité en fonction : <br>
* Lorsqu’un objet est dans arm atteint distance (environ 50 cm), les rayons sont désactivées automatiquement encourageant pour l’interaction proche. 
* Lorsque l’objet est plus loin que 50 cm, les rayons sont sous tension.

Ce mécanisme effectue la transition fluide et homogène.<br>
![](images/Transition-Between-Near-And-Far-720px.jpg)<br>

## <a name="2d-slate-interaction"></a>Interaction ardoise 2D
Une ardoise 2D est un conteneur HOLOGRAPHIQUE hébergement de contenu application 2D, comme navigateur web. Le concept de conception pour présent interagir avec une ardoise 2D consiste à utiliser des rayons de main pour pointer et appuyez sur Valider.<br>

Pour interagir avec l’obtention de surfaces ardoise :<br>

* Les utilisateurs peuvent pointer vers un lien hypertexte ou un bouton, puis appui en l’air pour l’activer. 
* Utilisateurs peuvent utiliser une seule main pour effectuer un mouvement de navigation pour défiler un contenu ardoise. 
* Utilisateurs peuvent utiliser deux mains pour effectuer des mouvements de navigation pour effectuer un zoom et de sortie le contenu ardoise.<br><br>

![](images/2D-Slate-Interaction-Far-720px.jpg)<br>

Pour la manipulation 2D d’ardoise lui-même :<br>

* Les utilisateurs pointent le rayon de la main à angles ou sur les bords pour révéler le plus proche intuitif de manipulation. 
* En appliquant un mouvement de manipulation sur l’intuitif, les utilisateurs peuvent effectuer une mise à l’échelle uniforme via intuitif de l’angle et peuvent ajuster dynamiquement l’ardoise via l’intuitif edge. 
* En appliquant un mouvement de manipulation sur la holobar en haut de l’ardoise 2D, les utilisateurs peuvent déplacer l’ardoise entière.<br>

<br>

## <a name="3d-object-manipulation"></a>Manipulation des objets 3D
Dans manipulation directe, il existe deux façons pour les utilisateurs de manipuler l’objet 3D, intuitif basé Manipulation et Manipulation en fonction de Non-affordnace. Dans le modèle de point et de validation, les utilisateurs sont capables d’atteindre exactement les mêmes tâches par le biais des rayons de main. Aucun apprentissage supplémentaire n’est nécessaire.<br>

### <a name="affordance-based-manipulation"></a>Manipulation d’intuitif basé
Les utilisateurs utiliser rayons de main pour pointer et faire apparaître la zone englobante et l’intuitivité de manipulation. Les utilisateurs peuvent appliquer le mouvement de manipulation sur la zone englobante pour déplacer l’objet entier, l’intuitivité edge pour faire pivoter et sur le coner permettant à l’échelle de manière uniforme. <br>

![](images/3D-Object-Manipulation-Far-720px.jpg) <br>


### <a name="non-affordance-based-manipulation"></a>Le caractère non-intuitif en fonction de manipulation
Les utilisateurs point avec des rayons de main pour faire apparaître la zone englobante, puis appliquer directement des mouvements de manipulation sur celui-ci. Une part, la traduction et la rotation de l’objet sont associées au mouvement et l’orientation de la main. Avec deux mains, les utilisateurs peuvent traduire, mettre à l’échelle et faire pivoter en fonction des mouvements relatifs de deux mains.<br>

<br>

## <a name="instinctual-gesturers"></a>Gesturers instinctual
Le concept de mouvements instinctual de point et de validation est synchronisé avec qui pour la manipulation directe. Ce que les utilisateurs de mouvements censés pour effectuer sur un objet 3D sont guidés par la conception du intuitivité de l’interface utilisateur. Un point de contrôle de petites serait motiver aux utilisateurs de pincement avec thumb et votre index, alors qu’un objet volumineux apporte aux utilisateurs de récupérer avec 5 doigt.

![](images/Instinctual-Gestures-Far-720px.jpg)<br>

## <a name="symmetric-design-between-hands-and-6-dof-controller"></a>Conception symétrique entre les mains et 6 contrôleur DDL 
Le concept de modèle de point et de validation pour l’interaction lointain est tout d’abord créé et défini pour le mixte réalité Portal (MRP), où les utilisateurs porter un casque immersif et interagissent avec l’objet 3d par le biais de contrôleurs de mouvement. Les contrôleurs de mouvement dépanner les rayons pour pointant et la manipulation des objets lointain. Il existe des boutons sur les contrôleurs de validation supplémentaire de différentes fonctionnalités. Nous exploiter le modèle d’interaction des rayons et définissez-les sur deux mains. Grâce à cette conception symétrique, les utilisateurs familiarisés avec MRP ne devront pas apprendre un autre modèle d’interaction pour pointant présent et la manipulation lors de la première fois à l’aide de HoloLen 2 et vice versa.    

![](images/Symmetric-Design-For-Rays-720px.jpg)<br>


## <a name="see-also"></a>Voir aussi
* [Regards et validation](gaze-and-commit.md)
* [Manipulation directe](direct-manipulation.md)
* [Fonctionnalités de base des interactions](interaction-fundamentals.md)
