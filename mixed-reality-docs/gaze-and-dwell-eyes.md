---
title: Pointer du regard et fixer
description: Vue d’ensemble du modèle d’entrée Pointer du regard et fixer
author: sostel
ms.author: sostel
ms.date: 10/29/2019
ms.topic: article
ms.localizationpriority: high
keywords: Suivi du regard, réalité mixte, entrée, suivre du regard, suivi rétinien, suivi du mouvement des yeux, HoloLens 2, sélection basée sur le regard, fixer
ms.openlocfilehash: 0ec5d5e3b7f56038c7be9930a4468d286b388a65
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926605"
---
# <a name="eye-gaze-and-dwell"></a>Pointer du regard et fixer

Le modèle d’interaction _« Pointer du regard et fixer »_ est un cas particulier du modèle d’interaction [Pointer du regard et valider](gaze-and-commit.md) :
1. Regardez simplement une cible. 
2. Pour confirmer votre intention de sélectionner cette cible, effectuez une entrée explicite secondaire : _Continuez simplement de regarder la cible que vous voulez sélectionner_.

## <a name="advantages-of-the-eye-gaze-and-dwell-interaction-model"></a>Avantages du modèle d’interaction « Pointer du regard et fixer » 
Lorsque vos mains sont déjà occupées par une tâche ou chargées d’outils, vous ne pouvez probablement pas les utiliser pour interagir avec des hologrammes.
Une alternative d’interaction sans les mains pour sélectionner des hologrammes consiste à « pointer du regard et fixer », autrement dit, à _« regarder et maintenir son regard »_ . L’avantage de cette approche est que même les utilisateurs soumis à de fortes contraintes, dans l’incapacité de tourner complètement la tête ou le corps, peuvent interagir avec des hologrammes (par exemple, dans un environnement de travail très confiné).
L’utilisateur continue simplement de regarder la cible qu’il souhaite sélectionner et une rétroaction différente s’affiche pour indiquer le processus.


## <a name="challenges-of-the-eye-gaze-and-dwell-interaction-model"></a>Défis du modèle d’interaction « Pointer du regard et fixer »
En règle générale, nous vous recommandons de n’utiliser les activations par fixation du regard qu’en dernier recours si aucune entrée vocale ou manuelle n’est disponible. En effet, le choix de la durée de fixation du regard s’avère assez délicat. Alors que les utilisateurs débutants acceptent de fixer leur regard plus longtemps, les utilisateurs experts préfèrent un parcours rapide et efficace de leurs expériences. Cette différence rend difficile la manière d’ajuster la durée du regard selon les besoins spécifiques de l’utilisateur.
Si la durée de fixation du regard est trop courte : L’utilisateur peut finir par se sentir accablé par tous les hologrammes constamment à sa portée. Si la durée de fixation du regard est trop longue : L’expérience peut sembler trop lente et hachée, car l’utilisateur doit fixer les cibles pendant trop longtemps.

## <a name="design-recommendations"></a>Recommandations de conception
Nous vous recommandons d’utiliser une approche avec deux états pour la rétroaction d’un regard fixe :
1. *Délai initial* : Quand l’utilisateur commence à fixer une cible, rien ne doit se produire immédiatement, sans quoi l’expérience utilisateur risque de devenir désagréable et pesante. Nous préférons lancer un minuteur pour détecter si l’utilisateur fixe délibérément son regard sur la cible ou s’il ne le pose que machinalement.
2. *Lancement de la rétroaction du regard fixe :* Après vérification que l’utilisateur regarde délibérément la cible, nous commençons à faire apparaître la rétroaction du regard fixe pour informer l’utilisateur que l’activation par fixation du regard est lancée. Nous recommandons un délai initial compris entre 150 et 250 ms dans une proximité donnée (ce qui signifie que l’utilisateur pointe son regard et fixe précisément, plutôt qu’il ne regarde vaguement une cible plus large).  
3. *Rétroaction en continu :* Pendant que l’utilisateur regarde toujours la cible, faites apparaître un indicateur de progression pour que l’utilisateur sache qu’il doit continuer à fixer la cible. En particulier pour les entrées par pointage du regard, nous vous recommandons d’_attirer l’attention visuelle de l’utilisateur_ en commençant avec un cercle ou une sphère volumineuse qui rétrécit progressivement. L’utilisation d’un indicateur pour l’état final (petit cercle) vous aide à communiquer à l’utilisateur à quel moment la rétroaction est terminée. Vous trouverez ci-dessous un exemple d’illustration. 
4. *Fin :* Si l’utilisateur a continué de fixer la cible (pendant 650 à 850 ms supplémentaires), effectuez l’activation de la rétroaction et sélectionnez la cible fixée.

![États de rétroaction](images/eyes_dwellstate_recommendation.png)<br>

## <a name="see-also"></a>Voir également
* [Eye-tracking](eye-tracking.md)
* [Pointer du regard et valider](gaze-and-commit-eyes.md)
* [Pointer et valider](gaze-and-commit.md)
* [Pointer du regard et fixer](gaze-and-dwell.md)
* [Entrée vocale](voice-design.md)
