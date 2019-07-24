---
title: Mains-libres
description: Optimisation de votre application pour des mains libres
author: liamar
ms.author: liamar
ms.date: 04/20/2019
ms.topic: article
keywords: La réalité mixte, mains libres, point d’interposition, le regard, l’interaction et la conception
ms.openlocfilehash: 7942192f644a7133335f089cfaaccfaebdd9292e
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414395"
---
# <a name="hands-free"></a>Mains-libres



## <a name="scenarios"></a>Scénarios

Comme indiqué dans la [vue d’ensemble du modèle d’interaction](interaction-fundamentals.md), une fois que vous avez identifié les utilisateurs et leurs objectifs, posez-vous les difficultés environnementales ou de situation auxquelles ils peuvent faire face lorsqu’ils travaillent pour accomplir leurs tâches. Par exemple, de nombreux utilisateurs ont besoin d’utiliser leurs mains pour atteindre leurs objectifs réels, et auront des difficultés à interagir avec une interface basée sur les mains et les contrôleurs. 

Certains scénarios spécifiques peuvent être: 
* Guidée par le biais d’une tâche, tandis que les mains sont occupées
* Référencement des matériaux lorsque vos mains sont occupées
* Fatigue de main
* Gants qui ne peuvent pas être suivis
* Transporter un événement


## <a name="hands-free-modalities"></a>Modalités des mains libres

### <a name="voice-commandingvoice-designmd"></a>[Commander avec la voix](voice-design.md)

L’utilisation de votre voix pour commander et contrôler une interface peut non seulement permettre à l’utilisateur d’utiliser Handsfree, mais également passer plusieurs étapes. L’utilisation de cette modalité peut aller de permettre à l’utilisateur de simplement lire le nom du bouton à haute voix pour l’activer, comme c’est le cas dans la section Voir-le-dit-IT, pour converser avec un agent qui peut accomplir des tâches pour vous.



### <a name="head-gaze-and-dwellgaze-and-dwellmd"></a>[Suivre de la tête et stabiliser](gaze-and-dwell.md)

Dans certaines situations mains libres, l’utilisation de votre voix n’est pas idéale, voire possible. Les environnements en usine bruyants, la confidentialité ou les normes sociales peuvent être des contraintes. Le modèle de point de vue du point de vue de la tête permet à l’utilisateur de parcourir l’application à l’aide de son vecteur d’en-tête pour pointer, tout en étant en attente ou le logement sur un bouton, l’active après un certain laps de temps, en général environ 1 seconde. 


## <a name="transitioning-in-and-out-of-hands-free"></a>Transition vers et à l’extérieur des mains libres

Pour ces scénarios, le fait de libérer des mains de l’interaction avec les hologrammes pour les commandes et la navigation peut aller de l’exigence absolue à l’exploitation de l’application, de bout en bout, à un confort supplémentaire que l’utilisateur peut passer dans simultanément. 

Si la spécification de l’application est qu’elle sera toujours utilisée librement, que ce soit à l’aide de son, de commandes vocales ou de la commande vocale unique, «Select», veillez à créer les logements appropriés dans votre interface utilisateur. 

Si votre utilisateur cible doit être en mesure de passer d’un mains à l’autre mains libres à sa discrétion, il est important de prendre en compte les principes suivants.

### <a name="assume-the-user-is-already-in-the-mode-that-they-want-to-switch-to"></a>Supposons que l’utilisateur est déjà dans le mode vers lequel il souhaite passer
Par exemple, si l’utilisateur se trouve en usine, regarde une référence vidéo sur son Hololens et décide de sélectionner une clé pour commencer à travailler, elle commence probablement à travailler dans Handsfree sans avoir à appuyer sur un bouton. Elle doit être en mesure d’appeler une session vocale avec une commande vocale, son logement sur une interface utilisateur déjà visible pour commencer son logement ou le mot «Select».

L’utilisateur doit avoir la possibilité d’effectuer les opérations suivantes: 
* Passez à l’option mains libres pendant les mains libres
* Passez aux mains avec vos mains
* Basculer vers le contrôleur à l’aide d’un contrôleur 

### <a name="create-redundant-ways-to-switch-modes"></a>Créer des méthodes redondantes pour basculer entre les modes
Tandis que le premier principe concerne l’accès, la seconde concerne la disponibilité. Il ne doit pas s’agir simplement d’un moyen unique de transition vers et à partir d’un mode. 

Voici quelques exemples: 
* Un bouton pour commencer les interactions vocales
* Commande vocale à utiliser pour la transition en utilisant le point de vue du regard

### <a name="add-a-dash-of-drama"></a>Ajouter un tiret de la fiction
Un changement de mode est un facteur important: il est important que lorsque ces transitions se produisent, il s’agit d’un commutateur explicite, même spectaculaire, pour permettre à l’utilisateur de savoir ce qui s’est passé. 


## <a name="usability-checklist"></a>Liste de vérification de l’utilisation

**L’utilisateur peut-il faire tout et tout ce qui est mains libres, de bout en bout?**
* Chaque interactible doit être accessible mains libres
* Assurez-vous qu’il existe un remplacement de tous les mouvements personnalisés, tels que le redimensionnement, le placement, les balayages, les robinets, etc.
* S’assurer que l’utilisateur a le contrôle assuré de la présence, de l’emplacement et des commentaires de l’interface utilisateur à tout moment
    * Récupération de l’interface utilisateur
    * Adressage de l’interface utilisateur en dehors de l’affichage (angle de vue)
    * Combien je vois, où, quand

**Les mécanismes de l’interaction sont-ils enseignés et armés avec le bon intuitivité?**

L’utilisateur a-t-il compris...
* ... Dans quel mode ils se trouvent-ils?
* ... Qu’est-ce qu’il est possible de faire dans ce mode?
* ... Quel est l’état actuel?
* ... Comment elles peuvent être transférées?
    
**L’interface utilisateur est-elle optimisée pour les mains libres?**   

* Exemple : Les intuitivités de logement ne sont pas intégrés aux modèles 2D typiques
* Exemple : Le ciblage vocal est mieux adapté à la mise en surbrillance des objets
* Exemple : Les interactions vocales sont mieux adaptées aux légendes qui doivent être activées


## <a name="see-also"></a>Voir aussi
* [Suivre de la tête et valider](gaze-and-commit.md)
* [Manipulation directe avec les mains](direct-manipulation.md)
* [Pointer et valider avec les mains](point-and-commit.md)
