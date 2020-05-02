---
title: Suivre du regard et valider
description: Vue d’ensemble du modèle d’entrée Suivre du regard et valider
author: sostel
ms.author: sostel
ms.date: 05/05/2019
ms.topic: article
ms.localizationpriority: high
keywords: Suivi du regard, réalité mixte, entrée, suivre du regard, suivi rétinien, suivi du mouvement des yeux, HoloLens 2, sélection basée sur le regard
ms.openlocfilehash: 89f5031635f2b67ba4c9afdf605559c2b9da4ac2
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "73437825"
---
# <a name="eye-gaze-and-commit"></a>Suivre du regard et valider
_Pointer du regard et valider_ est un cas particulier du modèle d’entrée [Pointer et valider](gaze-and-commit.md) qui implique de cibler un objet en le regardant tout simplement, puis en interagissant dessus avec une entrée de _validation_ secondaire, comme un mouvement de main, une commande vocale ou une entrée de périphérique (par exemple, avec un contrôleur de jeu). 

Dans HoloLens 2, nous pouvons utiliser le pointage du regard au lieu du suivi de la tête pour rendre les opérations de _suivi et de validation_ plus rapides et plus confortables. Nous étendons ainsi le modèle d’interaction commun [Suivre de la tête et valider](gaze-and-commit.md) : 
1. Regardez simplement une cible. 
2. Pour confirmer votre intention de sélectionner cette cible, effectuez une entrée explicite secondaire parmi celles-ci :  
   - Mouvement de la main (par exemple, un clic dans l’air)
   - Appui sur un bouton (par exemple, sur un clavier ou un dispositif de clic Bluetooth)
   - Commande vocale (par exemple, « Sélectionner »)
   - Stabilisation (par exemple, l’utilisateur continue de regarder la cible pour la sélectionner)

Cependant, le suivi du regard est différent du suivi de la tête à bien des égards et pose donc un certain nombre de défis uniques. Dans les [directives liées à la conception du suivi du regard](eye-tracking.md), nous résumons les avantages et défis généraux à prendre en compte lors de l’utilisation du suivi du regard comme entrée dans une application holographique. Dans cette section, nous nous penchons sur les considérations de conception spécifiques au modèle _Pointer du regard et valider_.
Premièrement, nos yeux bougent incroyablement vite et sont donc très efficaces pour cibler rapidement un objet dans une scène. Le pointage du regard est donc idéal pour les actions rapides de suivi et de validation, en particulier quand il est combiné à des validations rapides comme un clic dans l’air ou une pression sur un bouton.
   
Dans la section suivante, nous allons aborder les directives de conception du pointage du regard dans ce type d’interaction et discuter des différences qu’il convient de garder à l’esprit.

## <a name="design-guidelines-for-eye-gaze-and-commit"></a>Directives liées à la conception du suivi du regard et de la validation

**Ne pas afficher de curseur** : s’il est presque impossible d’interagir sans curseur dans le cadre du suivi de la tête, le curseur devient rapidement gênant quand vous utilisez le suivi du regard. Au lieu de recourir à un curseur pour indiquer à l’utilisateur si la fonction de suivi du regard fonctionne et si elle a correctement détecté la cible actuellement examinée, utilisez des surlignages visuels subtils (plus de détails ci-dessous).

**S’efforcer de fournir des retours visuels subtils et intégrés sur le pointage** : ce qui peut être un excellent retour visuel pour le suivi de la tête peut entraîner des expériences déplorables avec le suivi du regard. N’oubliez pas que vos yeux sont extrêmement rapides et qu’ils parcourent rapidement les points de votre champ de vision. Les changements soudains de surlignage (activation/désactivation) peuvent entraîner des effets de scintillement quand vous regardez autour de vous. Nous vous recommandons donc d’utiliser un surlignage qui s’intègre en douceur (et qui disparaît en fondu quand vous regardez ailleurs) pour fournir des retours visuels sur le pointage. Cela signifie que vous remarquez à peine le retour visuel quand vous commencez à regarder une cible. Après 500 à 1000 ms, le surlignage gagne en intensité. Bien que les débutants puissent continuer à regarder la cible pour vérifier qu’elle est correctement sélectionnée par le système, les utilisateurs expérimentés peuvent rapidement suivre du regard une cible et la valider sans attendre un retour visuel à pleine intensité. Nous vous recommandons également d’utiliser un fondu pour faire disparaître le retour visuel sur le pointage. Des recherches ont montré que les changements rapides de mouvement et de contraste sont très perceptibles dans votre vision périphérique (la zone de votre champ visuel où vous ne regardez pas).
La disparition en fondu n’a pas besoin d’être aussi lente que l’intégration. Ceci n’est critique que si vous avez un contraste élevé ou des changements de couleur pour votre surlignage. Si le retour visuel sur le pointage est assez subtil pour commencer, vous ne remarquerez probablement pas de différence.

**Veiller à synchroniser les signaux de pointage du regard et de validation** : la synchronisation des signaux d’entrée peut présenter un moindre défi pour les clics dans l’air et les appuis sur des boutons. Tenez-en compte au cas où vous souhaiteriez utiliser des actions de validation plus compliquées pouvant impliquer des commandes vocales longues ou des mouvements manuels complexes. Imaginons que vous regardiez une cible et que vous prononciez une commande vocale longue. Si nous tenons compte du temps qu’il faut pour parler et du temps nécessaire au système pour détecter ce que vous avez dit, votre regard est sans doute fixé depuis longtemps sur une nouvelle cible de la scène. Vous pouvez donc soit indiquer à vos utilisateurs de continuer à regarder la cible jusqu’à ce que la commande soit reconnue, soit gérer l’entrée de manière à déterminer le début de la commande et l’objet ciblé par le regard de l’utilisateur au moment de l’émission de la commande.

## <a name="see-also"></a>Voir aussi
* [Interaction basée sur le regard] (eye-gaze-interaction.md)
* [Suivi oculaire sur HoloLens 2] (eye-tracking.md)
* [Pointer et valider](gaze-and-commit.md)
* [Pointer du regard et fixer](gaze-and-dwell.md)
* [Mains : Manipulation directe](direct-manipulation.md)
* [Mains : Mouvements](gaze-and-commit.md#composite-gestures)
* [Mains : Pointer et valider](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Entrée vocale](voice-input.md)
