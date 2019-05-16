---
title: Manipulation directe des mains
description: Vue d’ensemble du modèle d’entrée de manipulation directe
author: caseymeekhof
ms.author: cmeekhof
ms.date: 04/02/2019
ms.topic: article
ms.localizationpriority: high
keywords: Mixte réalité, les regards, les regards ciblant, interaction, concevez, mains near, HoloLens
ms.openlocfilehash: e241e13a778de0889942a3643246e087a107db86
ms.sourcegitcommit: 1c0fbee8fa887525af6ed92174edc42c05b25f90
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65730749"
---
# <a name="direct-manipulation-with-hands"></a>Manipulation directe des mains
Manipulation directe est un modèle d’entrée qui implique de toucher hologrammes directement avec vos mains. L’objectif de la manipulation directe est que les objets se comportent exactement comme dans le monde réel. Boutons peuvent être activées simplement en appuyant sur les objets peuvent être interceptés par s’emparer les et contenu 2D se comporte comme un écran tactile virtuel.  Pour cette raison, diriger manipulation est facile pour les utilisateurs pour en savoir plus, et il est passionnant trop.  Il est considéré comme un modèle d’entrée « proches », ce qui signifie qu’il est particulièrement adapté pour l’interaction avec du contenu qui est au sein des armes atteindre.

La version 2 HoloLens a un modèle d’entrée de manipulation directe qui vous permet de toucher dircly hologrammes avec vos mains. L’objectif de la manipulation directe est pour les objets se comporte exactement comme dans le monde réel. Vous pouvez activer les boutons en appuyant simplement sur eux et même prélever, saisir et déplacer des objets. Dans ces scénarios, contenu 2D se comporte comme un écran tactile virtuel.

Diriger la manipulation est facile pour les utilisateurs pour en savoir plus, et il a amusants trop. Il est considéré comme un modèle d’entrée « remet près », ce qui signifie qu’il est particulièrement adapté pour l’interaction avec du contenu qui se trouve dans une portée d’un arm.

Manipulation directe est intuitif, ce qui signifie que son convivial. Il n’y a aucune mouvements symboliques à apprendre aux utilisateurs. Toutes les interactions reposent sur un élément visuel que vous pouvez toucher ou saisir.

## <a name="device-support"></a>Prise en charge des appareils


| Modèle d’entrée | [HoloLens (1er Gen)](https://review.docs.microsoft.com/en-us/windows/mixed-reality/hololens-hardware-details?branch=master) | HoloLens 2 |[Casques IMMERSIFS](https://review.docs.microsoft.com/en-us/windows/mixed-reality/immersive-headset-hardware-details?branch=master)|
|:-------- | :-------| :--------| :------------|
| Manipulation directe | ❌ Ne pas pris en charge | ✔️ Recommandé | ➕ alternative [pointez et validez](https://review.docs.microsoft.com/en-us/windows/mixed-reality/point-and-commit?branch=master) est recommandé.

Manipulation directe est un modèle d’entrée principal sur HoloLens 2 et utilise le nouveau système de suivi de la main bras. Le modèle d’entrée est également disponible sur des casques IMMERSIFS grâce à l’utilisation de contrôleurs de mouvement, mais n’est pas recommandé comme moyen principal d’interaction en dehors de la manipulation des objets.  Diriger manipluation n’est pas disponible sur HoloLens (1er gen).


## <a name="collidable-fingertip"></a>Bout des doigts collidable

Sur HoloLens 2, mains réel de l’utilisateur sont reconnus et interprétés en tant que modèles squelettes gauche et droite. Pour implémenter l’idée de toucher hologrammes directement des mains, dans l’idéal, 5 colliders ne sont attachés à portée de 5 main de chaque modèle de squelette de main. Cependant, en pratique, en raison du manque de rétroaction tactile, portée de main collidable 10 dû collisions inattendues et imprévisibles avec hologrammes. 

Par conséquent, nous vous suggérons pour ne placer un collider sur chaque doigt de l’index. La portée de main collidable index peut toujours servir de tactile actif points pour diverses entrées tactiles multipoints impliquant autre doigt, tels qu’appuyez sur 1-doigt, appuyez sur 1-doigt, appuyez sur 2-doigt et appuyez sur 5-doigt, comme illustré dans l’image ci-dessous.

![Image de collidable par un doigt](images/Collidable-Fingertip-720px.jpg)

### <a name="sphere-collider"></a>Sphère collider

Au lieu d’utiliser une forme générique aléatoire, nous vous suggérons d’utiliser un collider sphère et rendre visuellement pour fournir une meilleure signaux pour le ciblage de quasiment. Diamètre de la sphère doit correspondre à l’épaisseur du doigt index pour augmenter la précision de tactile. Il sera facile de récupérer la variable d’épaisseur du doigt en appelant l’aiguille de l’API.

### <a name="fingertip-cursor"></a>Curseur du bout des doigts

Outre le rendu d’une sphère collidable sur le bout des doigts index, nous avons créé une solution avancée, le curseur par un doigt, pour obtenir une meilleure expérience près de multi-ciblage interactivement. Il est un curseur en forme de graphique en anneau attaché sur le bout des doigts index. En fonction de la proximité, il réagit dynamiquement à une cible en termes d’orientation et la taille comme indiqué ci-dessous :

* Lorsque votre index se déplace vers un hologramme, le curseur est toujours parallèle à surface de l’hologramme et progressivement diminue sa taille en conséquence.
* Dès que le doigt touche la surface, le curseur est réduit à un point et émet un événement tactile.

Avec les commentaires interactive, les utilisateurs peuvent obtenir une haute précision près de ciblage des tâches, telles que le déclenchement d’un lien hypertexte sur le contenu web ou en appuyant sur un bouton, comme indiqué ci-dessous. 

![Image de curseur par un doigt](images/Fingertip-Cursor-720px.jpg)

## <a name="bounding-box-with-proximity-shader"></a>Zone englobante avec le nuanceur de proximité

L’hologramme lui-même nécessite également la possibilité de fournir des commentaires visuels et audio pour compenser l’absence de rétroaction tactile. Pour ce faire, nous générons le concept d’un rectangle englobant avec le nuanceur de proximité. Un rectangle englobant est une zone de volumétrique minimale qui comprend un objet 3D. La zone englobante a un mécanisme interactive de rendu appelé nuanceur de proximité. Le nuanceur de proximité se comporte :

* Lorsque le doigt de l’index se trouve dans une plage, un coup de projecteur par un doigt est converti sur l’aire du cadre englobant.
* Lorsque le bout des doigts se rapproche la surface, actualités condense en conséquence.
* Dès que le bout des doigts toucher la surface, la totalité de zone englobante modifie la couleur ou générer un effet visuel pour refléter l’état tactile.
* Pendant ce temps, un effet audio peut être activé pour améliorer le feedback de saisie visual.

![Zone englobante avec l’image de nuanceur de proximité](images/Bounding-Box-With-Proximity-Shader-720px.jpg)

## <a name="pressable-button"></a>Bouton PRESSEE

Avec un par un doigt collidable, les utilisateurs sont maintenant prêtes à interagir avec le composant interface utilisateur de HOLOGRAPHIQUE très fondamental, bouton PRESSEE. Un bouton PRESSEE est un bouton HOLOGRAPHIQUE adapté pour press du doigt direct. Là encore, en raison du manque de rétroaction tactile, un bouton PRESSEE doter les deux mécanismes pour aborder des problèmes liés à la rétroaction tactiles.

* Le premier mécanisme est un cadre englobant avec le nuanceur de proximité, détaillé dans la section précédente. Il sert à fournir une meilleure idée de proximité permettant aux utilisateurs de l’approche et assurez-vous contact avec un bouton.
* Le second est DÉPRESSION. Il crée le sens de presse, après qu’un par un doigt contacte le bouton. Le mécanisme est que le bouton se déplace étroitement avec le bout des doigts sur l’axe de profondeur. Le bouton peut être déclenché lorsqu’il atteint une profondeur désignée (sur press) ou le quitte la profondeur (sur la mise en production) après la transmission par son intermédiaire.
* L’effet audio doit être ajouté pour améliorer les commentaires, lorsque le bouton est déclenché.

![Image du bouton PRESSEE](images/Pressable-Button-720px.jpg)

## <a name="2d-slate-interaction"></a>Interaction ardoise 2D

Une ardoise 2D est un conteneur HOLOGRAPHIQUE hébergement de contenu application 2D, comme navigateur web. Le concept de conception permettant d’interagir avec une ardoise 2D via la manipulation directe consiste à tirer parti du modèle mental de l’interaction avec un écran tactile physique.

Pour interagir avec le contact ardoise :

* Utilisez votre index à appuyer sur un bouton ou un lien hypertexte.
* Utilisez votre index pour faire défiler un contenu ardoise diminué.
* Les utilisateurs utiliser deux doigts de l’index pour effectuer un zoom et de sortie au contenu ardoise selon un mouvement relatif des doigts.

![Image d’ardoise 2D](images/2D-Slate-Interaction-720px.jpg)

Pour la manipulation 2D d’ardoise lui-même :

* Approche vos mains vers des angles et des bords pour révéler l’intuitivité de manipulation le plus proche.
* Saisissez l’intuitivité de manipulation et effectuer la mise à l’échelle uniforme via l’intuitivité de coin et redistribution via l’intuitivité edge.
* Saisissez le holobar en haut de l’ardoise 2D, ce qui vous permet de déplacer l’ardoise entière.

![Image d’ardoise manipulation](images/Manipulate-2d-slate-720px.jpg)

## <a name="3d-object-manipulation"></a>Manipulation des objets 3D

HoloLens 2 permet des utilisateurs ne commencent à utiliser diriger permet de manipuler les objets 3D hologramphic en appliquant un cadre englobant à chaque objet 3D. La zone englobante fournit une meilleure perception de profondeur via son nuanceur de proximité. Avec la zone englobante, il existe deux approches de conception pour la manipulation de l’objet 3D.

### <a name="affordance-based-manipulation"></a>En fonction du intuitif de manipulation

Cela vous permet de manipuler l’objet 3D via une zone englobante et l’intuitivité de manipulation autour d’elle. Dès que la part de l’utilisateur est proche d’un objet 3D, la zone englobante et la plus proche intuitif sont dévoilées. Les utilisateurs peuvent saisir la zone englobante pour déplacer l’objet entier, l’intuitivité edge pour faire pivoter et l’intuitivité supérieur à l’échelle de manière uniforme.

![Image de manipulation d’objet 3D](images/3D-Object-Manipulation-720px.jpg)

### <a name="non-affordance-based-manipulation"></a>Le caractère non-intuitif en fonction de manipulation

Dans ce mécanisme, aucun intuitif n’est attaché à la zone englobante. Les utilisateurs peuvent uniquement afficher la zone englobante, puis interagir directement avec lui. Si la zone englobante est saisie avec une main, la traduction et la rotation de l’objet sont associés au mouvement et l’orientation de la main. Lorsque l’objet est saisi avec deux mains, les utilisateurs peuvent traduire, mettre à l’échelle et faire pivoter en fonction des mouvements relatifs de deux mains.

Manipulation spécifique requiert la précision, nous vous recommandons d’utiliser **basée sur le caractère intuitif de manipulation**, car il fournit un haut niveau de granularité. Pour une manipulation flexible, nous vous recommandons utilise **non intuitif manipulation** est car elle permet à l’approche instantanée et amusant.

## <a name="instinctual-gestures"></a>Mouvements instinctual

Avec HoloLens (1er gen), nous avons dispensés utilisateurs quelques gestes prédéfinis, tels que Bloom et Air appuyez sur. Pour HoloLens 2, nous ne me demander aux utilisateurs de mémoriser les mouvements symboliques. Tous les mouvements de l’utilisateur requis, les utilisateurs doivent interagir avec hologrammes et de contenu, sont instinctual. Pour réaliser le mouvement instinctual consiste à guider les utilisateurs pour effectuer des mouvements de la conception d’intuitivité de l’interface utilisateur.

Par exemple, si nous vous encourageons à la capture d’un objet ou un point de contrôle avec pincement de deux doigts, l’objet ou le point de contrôle doit être petit. Si nous voulons vous permettent d’effectuer cinq manipulation doigt, l’objet ou le point de contrôle doit être relativement important. Comme pour les boutons, un petit bouton limiterait les utilisateurs pour appuyer sur avec un seul doigt, tandis qu’un bouton énorme encourage les utilisateurs à appuyer sur avec leurs paumes.

![](images/Instinctual-Gestures-720px.jpg)

## <a name="symmetric-design-between-hands-and-6-dof-controllers"></a>Conception symétrique entre les mains et 6 contrôleurs DDL

Vous avez peut-être remarqué qu’il existe désormais parallels interaction que nous pouvons dessiner entre les mains dans les contrôleurs AR et mouvement dans VR. Les deux entrées peuvent servir à déclencher les manipulations directes dans leurs environnements respectifs. Dans les 2 HoloLens, faisant des mains au fonctionnement de la distance fermer une grande partie de la même façon que le bouton de manipulation glisser effectuent sur les contrôleurs de mouvement dans WMR. Cela permet aux utilisateurs d’une bonne connaissance de l’interaction entre les deux plateformes et peut s’avérer utile devez jamais vous décidez de migrer votre application à partir d’un à l’autre.

## <a name="optimize-with-eye-tracking"></a>Optimiser les yeux

Manipulation directe peut se sentent magique si elle fonctionne comme prévu, mais peut également rapidement devenir frustrante si vous ne pouvez pas déplacer n’importe où votre main plus sans par inadvertance déclencher un hologramme.
Suivi de le œil peut potentiellement utile dans une meilleure identification des éléments intention de l’utilisateur.

* **Lorsque**: Réduire faussement déclencher une réponse de manipulation. Suivi de le œil permet de mieux comprendre qu’un utilisateur actuellement engagé avec.
Par exemple, imaginez la que lecture dans un texte (démonstration) HOLOGRAPHIQUE lorsque vous atteignez plus vous attraper l’outil de travail réel.

En procédant ainsi, vous déplacer accidentellement votre main sur certains boutons HOLOGRAPHIQUE interactifs qui vous auriez pas remarqué même avant (par exemple, qu'il était même en dehors de champ de vision l’utilisateur (angle d’ouverture)).

  Pour faire court : Si l’utilisateur n’a pas examiné un hologramme pendant un certain temps, mais un événement tactile ou comprendre a été détecté pour celle-ci, il est probable que l’utilisateur n’a pas été réellement qui a l’intention d’interagir avec ce hologramme.

* **Celui**:  À part l’adressage false activations positif, un autre exemple comprend mieux identifier les hologrammes pour saisir ou examiner le point d’intersection précise ne peut pas être clair à partir de votre point de vue en particulier si plusieurs hologrammes sont positionnés proximité les uns autres.

  Alors que suivi d’yeux sur HoloLens 2 a une certaine limite sur la façon de précisément, elle peut déterminer vous regards des yeux, elle peut être très utile pour près interactions en raison d’une disparité de profondeur lors de l’interaction avec la main d’entrée.  Cela signifie qu’il est parfois difficile de déterminer si votre main est derrière ou devant un hologramme précisément Attrapez par exemple un widget de manipulation.

* **Où**: Utiliser les informations sur ce qu’un utilisateur consulte les rapide - levant gestes. Saisissez un hologramme et à peu près jeter celui-ci vers votre destination prévue.  

    Alors que cela peut être parfois fonctionne parfaitement, rapidement effectuer des mouvements de main peut entraîner des destinations hautement inexactes. Il s’agit où yeux peut aider à appuyer la main levée vecteur précédent de votre position prévue.

## <a name="see-also"></a>Voir aussi

* [Pointer du regard vers l’avant et valider](gaze-and-commit.md)
* [Pointer et valider](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)

