---
title: Optimisation de votre application pour mains libres
description: Optimisation de votre application pour mains libres
author: liamar
ms.author: liamar
ms.date: 04/20/2019
ms.topic: article
keywords: Une réalité mixte, mains libres, utilisation, utilisation de ciblage, interaction, conception
ms.openlocfilehash: b64dec802d8ed2886021a54f302ba4a948c4f5b9
ms.sourcegitcommit: f5c1dedb3b9e29f27f627025b9e7613931a7ce18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2019
ms.locfileid: "64581029"
---
# <a name="optimizing-your-app-for-hands-free"></a>Optimisation de votre application pour mains libres



## <a name="scenarios"></a>Scénarios

Comme indiqué dans le [vue d’ensemble du modèle d’interaction](interaction-fundamentals.md), une fois que vous avez identifié les utilisateurs et leurs objectifs, demandez-vous quel environnementales ou connaissance défis liés peut qu’ils testent pour accomplir leurs tâches. Par exemple, les nombreux utilisateurs ont besoin d’utiliser les mains à atteindre leurs objectifs réalistes et avoir des difficultés à interagir avec une interface en mains et contrôleurs. 

Certains scénarios spécifiques peuvent être : 
* Être guidés dans une tâche, tandis que les mains sont occupés
* Faisant référence à des documents tandis que vos mains sont occupés
* Fatigue de main
* Gants qui ne peut pas être suivis.
* Exécution d’un élément


## <a name="hands-free-modalities"></a>Modalités de mains libres

### <a name="voice-commanding"></a>Exécution des commandes vocales

À l’aide de votre voix à la commande et de contrôle de qu'une interface peut non seulement autoriser l’utilisateur à mains libres de fonctionner, mais également ignorer plusieurs étapes. L’utilisation de cette modalité peut varier de permettre à l’utilisateur en lisant simplement les nom de n’importe quel bouton audio pour l’activer, comme dans Voir-it-say-it, à converser avec un agent qui peut effectuer des tâches pour vous.

* [Conception de la voix](voice-design.md)


### <a name="head-gaze-and-dwell"></a>Regards de tête et de balayage

Dans certaines situations mains-libres, en utilisant votre voix n’est pas idéale ou même possible. Environnements d’usine forte, confidentialité ou normes sociaux peuvent tous être des contraintes. Utilisation de la tête + m’attarderai pas modèle permet à l’utilisateur à naviguer de l’application à l’aide de leur vecteur principal pour qu’il pointe, tout en attente, ou logement sur un bouton s’activer après un certain laps de temps (généralement environ 1 seconde ou ainsi). 

* [Regards et durée d’affichage](gaze-and-dwell.md)

## <a name="transitioning-in-and-out-of-hands-free"></a>Transition vers et depuis mains libres

Pour ces scénarios, la libération vos mains d’interagir avec hologrammes pour la navigation et d’exécution des commandes peut aller d’une exigence absolue jusqu'à l’exploitation de l’application,-bout, à l’utilisateur peut effectuer la transition et se déconnecte d’à tout moment d’une fonctionnalité supplémentaire. 

Si la configuration requise de l’application est qu’il sera toujours utilisé mains-libres, en utilisant la durée d’affichage, les commandes vocales ou les commandes vocales unique, « select », puis veillez à l’hébergement approprié dans votre interface utilisateur. 

Si votre utilisateur cible doit être en mesure de passer de mains à mains libres à leur discrétion, il est important de tenir compte de ces principes :

### <a name="assume-the-user-is-already-in-the-mode-that-they-want-to-switch-to"></a>Supposons que l’utilisateur est déjà dans le mode qu’ils souhaitent pour basculer vers
Par exemple, si votre utilisateur est en usine, regarder une vidéo référence sur son Hololens et décide de récupérer une clé pour commencer à utiliser, elle très probablement souhaite commencer à travailler dans les mains libres sans avoir à placer la clé d’appuyer sur un bouton vers le bas. Elle doit être en mesure d’appeler une session vocale avec une commande de voix, m’attarderai pas sur l’interface utilisateur déjà visible pour commencer à durée d’affichage, ou que le mot « select ».

L’utilisateur doit avoir la possibilité de : 
* Basculez vers mains libres tout en mains libres
* Basculez vers entre les mains avec vos mains
* Basculez vers le contrôleur à l’aide d’un contrôleur 

### <a name="create-redundant-ways-to-switch-modes"></a>Créer pour basculer entre les modes redondant
Bien que le premier principe soit sur l’accès, le second est sur la disponibilité. Il ne doit pas simplement être un moyen simple pour la transition vers et depuis un mode. 

Il peut s’agir : 
* Un bouton pour lancer des interactions vocales
* Une commande de la voix pour effectuer la transition à l’utilisation du pointage de regard + durée d’affichage

### <a name="add-a-dash-of-drama"></a>Ajoutez un peu de pièces de théâtre
Un commutateur de mode n’est pas anodin, il est important que lorsque ces transitions se produisent, qu’ils soient un commutateur explicit, même considérable, pour informer l’utilisateur que s’est-il passé. 


## <a name="usability-checklist"></a>Liste de vérification de facilité d’utilisation

**L’utilisateur peut faire de tout et rien mains-libres, end-to-end ?**
* Chaque interactible doivent être accessibles mains libres
* Vérifiez qu’il existe un remplacement pour tous les mouvements personnalisés, tels que redimensionnement, de placement, où les balayages, robinets, etc.
* Assurez-vous que l’utilisateur dispose du contrôle de certitude de la présence de l’interface utilisateur, de placement, de niveau de détail en permanence
    * Obtention de l’interface utilisateur disparaître
    * Adressage de l’interface utilisateur qui est en dehors du champ de vision (angle d’ouverture)
    * Combien je vois, où, quand

**Sont les mécanismes de l’interaction en cours dispensés et renforcés avec l’intuitivité droit ?**

L’utilisateur comprend...
* ... Quel mode ils compte-t-elle ?
* ... Ce qu’ils peuvent faire dans ce mode ?
* ... Quel est l’état actuel ?
* ... Comment ils peuvent transition sortante ?
    
**L’interface utilisateur optimisée pour mains libres ?**   

* Exemple : Balayage intuitivité n’est pas intégrées aux modèles 2D standard
* Exemple : Ciblage de la voix est préférable avec mise en surbrillance de l’objet
* Exemple : Interactions vocales sont meilleures avec des légendes qui doivent être mis sous tension


## <a name="see-also"></a>Voir aussi
* [Regards et validation](gaze-and-commit.md)
* [Manipulation directe](direct-manipulation.md)
* [Point et validation](point-and-commit.md)
