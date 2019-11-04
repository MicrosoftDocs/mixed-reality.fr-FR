---
title: Mains-libres
description: Optimisation de votre application pour des mains libres
author: liamartinez
ms.author: liamar
ms.date: 04/20/2019
ms.topic: article
keywords: La réalité mixte, mains libres, point d’interposition, le regard, l’interaction et la conception
ms.openlocfilehash: b2405f5dca19838271363f53ca377c4f90ca1b36
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73435075"
---
# <a name="hands-free"></a>Mains-libres

## <a name="scenarios"></a>Scénarios

Comme indiqué dans la [vue d’ensemble du modèle d’interaction](interaction-fundamentals.md), une fois que vous avez identifié vos utilisateurs et leurs objectifs, posez-vous les questions environnementales ou de situation auxquelles ils peuvent être confrontés lorsqu’ils travaillent pour accomplir leurs tâches. Par exemple, de nombreux utilisateurs ont besoin d’utiliser leurs mains pour atteindre leurs objectifs réels, et ils auront des difficultés à interagir avec une interface basée sur les mains et les contrôleurs. 

Voici quelques scénarios spécifiques : 
* Guidée par le biais d’une tâche, tandis que les mains de l’utilisateur sont occupées
* Référencement des matériaux lorsque les mains de l’utilisateur sont occupées
* Fatigue de main
* Gants qui ne peuvent pas être suivis
* Transporter des choses en mains
* Les maladroites pour effectuer des mouvements de grande taille
* Espaces étroits


## <a name="hands-free-modalities"></a>Modalités des mains libres

### <a name="voice-inputvoice-inputmd"></a>[Entrée vocale](voice-input.md)

L’utilisation de votre voix pour la commande et le contrôle d’une interface offre un moyen pratique de faire fonctionner librement les mains et d’utiliser des raccourcis pour ignorer de manière flexible plusieurs étapes si vous le souhaitez. Avec l’entrée vocale, l’utilisateur peut simplement lire le nom du bouton à haute voix pour l’activer _(le voir, le prononcer)_ et communiquer avec un agent numérique qui peut accomplir des tâches pour vous.


### <a name="gaze-and-dwellgaze-and-dwellmd"></a>[Pointer du regard et fixer](gaze-and-dwell.md)

Dans certaines situations mains libres, l’utilisation de votre voix n’est pas idéale, voire possible. Les environnements en usine bruyants, la confidentialité ou les normes sociales peuvent être des contraintes. Le modèle de point de présence et de tête permet à l’utilisateur de naviguer dans une application sans aucune entrée supplémentaire, à part de son oeil ou de son point de vue : l’utilisateur garde simplement Gazing (avec son tête ou ses yeux) à la cible et attend un moment pour l’activer. Pour en savoir plus sur les considérations de conception individuelles pour le point de vue et le point de vue, consultez la section [œil-point](gaze-and-dwell-eyes.md) de vue et [tête](gaze-and-dwell-head.md)de regard.


## <a name="transitioning-in-and-out-of-hands-free"></a>Transition vers et à l’extérieur des mains libres

Pour ces scénarios, le fait de libérer des mains de l’interaction avec les hologrammes pour les commandes et la navigation peut aller de l’exigence absolue à l’exploitation de l’application, de bout en bout, à un confort supplémentaire que l’utilisateur peut passer dans simultanément. 

Si la spécification de l’application est qu’elle sera toujours utilisée librement, que ce soit à l’aide de son, de commandes vocales personnalisées ou de la commande vocale unique, « Select », veillez à apporter les logements appropriés dans votre interface utilisateur. 

Si votre utilisateur cible doit être en mesure de passer d’un mains à l’autre mains libres à sa discrétion, il est important de prendre en compte les principes suivants.

### <a name="assume-the-user-is-already-in-the-mode-that-they-want-to-switch-to"></a>Supposons que l’utilisateur est déjà dans le mode vers lequel il souhaite passer
Par exemple, si l’utilisateur se trouve en usine, regarde une référence vidéo sur son HoloLens et décide de sélectionner une clé pour commencer à travailler, elle commence probablement à travailler sans avoir à appuyer sur un bouton pour commencer à travailler. Elle doit être en mesure d’appeler une session vocale avec une commande vocale, son logement sur une interface utilisateur déjà visible pour commencer son logement ou le mot « Select ».

L’utilisateur doit avoir la possibilité d’effectuer les opérations suivantes : 
* Passez à l’option mains libres pendant les mains libres
* Passez aux mains avec vos mains
* Basculer vers le contrôleur à l’aide d’un contrôleur 

### <a name="create-redundant-ways-to-switch-modes"></a>Créer des méthodes redondantes pour basculer entre les modes
Tandis que le premier principe concerne l’accès, la seconde concerne la disponibilité. Il ne doit pas s’agir simplement d’un moyen unique de transition vers et à partir d’un mode. 

Voici quelques exemples : 
* Un bouton pour commencer les interactions vocales
* Commande vocale à utiliser pour la transition, en utilisant le point d’interposition

### <a name="add-a-dash-of-drama"></a>Ajouter un tiret de la fiction
Un changement de mode est un facteur important : il est important que lorsque ces transitions se produisent, il s’agit d’un commutateur explicite, même un commutateur dramatique, pour permettre à l’utilisateur de savoir ce qui s’est passé. 


## <a name="usability-checklist"></a>Liste de vérification de l’utilisation

**L’utilisateur peut-il faire tout et tout ce qui est mains libres, de bout en bout ?**
* Chaque interaction peut être accessible mains libres
* Assurez-vous qu’il existe un remplacement de tous les mouvements personnalisés, tels que le redimensionnement, le placement, les balayages, les robinets, etc.
* S’assurer que l’utilisateur a le contrôle assuré de la présence, de l’emplacement et des commentaires de l’interface utilisateur à tout moment
    * Récupération de l’interface utilisateur
    * Adressage de l’interface utilisateur en dehors de l’affichage (angle de vue)
    * Combien je vois, où, quand

**Les mécanismes de l’interaction sont-ils enseignés et armés avec le bon intuitivité ?**

L’utilisateur a-t-il compris...
* ... Dans quel mode ils se trouvent-ils ?
* ... Qu’est-ce qu’il est possible de faire dans ce mode ?
* ... Quel est l’état actuel ?
* ... Comment elles peuvent être transférées ?
    
**L’interface utilisateur est-elle optimisée pour les mains libres ?**   

* Exemple : les intuitivités de logement ne sont pas intégrés aux modèles 2D typiques
* Exemple : le ciblage vocal est mieux adapté à la mise en surbrillance des objets
* Exemple : les interactions vocales sont meilleures avec les légendes qui doivent être activées


## <a name="see-also"></a>Articles associés
* [Suivi des yeux sur HoloLens 2](eye-tracking.md)
* [Point de regard et validation](gaze-and-commit.md)
* [Pointer du regard et fixer](gaze-and-dwell.md)
* [Manipulation directe](direct-manipulation.md)
* [Mouvements pratiques](gaze-and-commit.md#composite-gestures)
* [Mains et validation](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Entrée vocale](voice-input.md)
