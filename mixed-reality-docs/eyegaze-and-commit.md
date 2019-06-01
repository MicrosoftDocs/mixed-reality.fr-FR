---
title: Oculaire et validation
description: Vue d’ensemble du modèle d’entrée oculaire et validation
author: sostel
ms.author: sostel
ms.date: 05/05/2019
ms.topic: article
ms.localizationpriority: high
keywords: Suivi des yeux, mixte réalité, entrée, du pointage de regard yeux, ciblant des yeux, HoloLens 2, sélection basée sur les yeux
ms.openlocfilehash: 9cc27f24e1275223f33becd1ff0ec6bdf5b43a57
ms.sourcegitcommit: 60060386305eabfac2758a2c861a43c36286b151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66455085"
---
# <a name="eye-gaze-and-commit"></a>Oculaire et validation
Avec 2 HoloLens, nous avons l’occasion idéale pour améliorer les regards & validation plus rapide et plus à l’aise en utilisant des regards de œil au lieu de regards principal. Cela permet d’étendre le commun [regards de tête et de validation](gaze-and-commit.md) modèle d’interaction : 
1. Consulter simplement une cible et 
2. Pour confirmer votre intention de sélectionner la cible, effectuez une base de données secondaire explicite d’entrée tels que r :  
   - Mouvements de main (par exemple, un Air appuyez sur)
   - Appuyez sur le bouton (par exemple, sur un clavier ou un clicker)
   - Commande vocale (par exemple, « Select »)
   - Logement (par exemple, l’utilisateur conserve Examinez simplement la cible pour sélectionner)

Toutefois, les regards yeux se comportement différemment de regards principal d’une certaine façon et, par conséquent, est fourni avec un nombre de défis uniques. Dans le [yeux utilisation des règles de conception](eye-tracking.md), nous résumons les avantages généraux et les défis à prendre en compte lors de l’utilisation des yeux suivi en tant qu’entrée dans votre application HOLOGRAPHIQUE. Dans cette section, nous nous concentrons sur les considérations de conception spécifiques pour OCULAIRE & validation.
Tout d’abord, nos yeux extrêmement vite et est donc idéales au ciblage rapidement sur la vue. Cela, yeux les regards parfaits pour des actions du pointage de regard-validation rapides en particulier lorsqu’elles sont combinées avec des validations rapides comme un appui en l’air ou bouton press.
   
Dans l’exemple suivant, nous étudierons les instructions de conception lorsque vous utilisez des yeux d’utilisation de ce type d’interaction et de sera présentent les différences entre la tête et yeux du pointage de regard que vous devez prendre en compte.

## <a name="design-guidelines-for-eye-gaze-and-commit"></a>Instructions pour oculaire et validation de conception

**Ne pas afficher un curseur**: S’il est presque impossible d’interagir sans un curseur lors de l’utilisation de tête les regards, le curseur se transforme rapidement parasites et agaçante lors de l’utilisation du pointage de regard yeux. Au lieu d’utiliser un curseur pour informer l’utilisateur si le suivi de le œil fonctionne et a correctement détecté actuellement consultés sur la cible, visual subtiles utilisation met en évidence (plus de détails ci-dessous).

**Pour envoyer des commentaires de pointage combinées subtile vous efforcer**: Ce qui paraît excellent retour visuel pour les regards principal peut entraîner une terrible, écrasant expériences à l’aide du pointage de regard yeux. N’oubliez pas que les yeux sont extrêmement rapides, darting rapidement entre les points de votre champ de vision. Commentaires flickery peuvent entraîner des modifications de mise en surbrillance soudaine rapide (activé/désactivé) lors de la recherche. Par conséquent, lorsque vous fournissez des commentaires de pointage, nous vous recommandons d’utiliser une mise en surbrillance correctement fusionnés dans (et fusionnée à la sortie lors de la recherche de suite). Cela signifie que dans un premier temps vous à peine remarquerait les commentaires lorsque vous examinez une cible. Au cours de 500 à 1000 ms, la mise en surbrillance augmenterait en intensité. Tandis que les utilisateurs novices peuvent continuer à chercher à la cible pour vous assurer que le système a déterminé correctement la cible ayant le focus, les utilisateurs expérimentés pourraient rapidement les regards & sont validées sans attendre que les commentaires sont à son intensité complète. En outre, nous vous recommandons également d’à l’aide de blend montée lorsque atténuant progressivement les commentaires de pointage. Research a montré que les modifications rapides de mouvement et contraste sont très visibles dans votre vision périphérique (par conséquent, la zone de votre champ visuel où vous cherchez pas). Le fondu ne doit pas être lentes en tant que blend dans. Cela est essentiel uniquement lorsque vous avez un contraste élevé ou des modifications de couleur pour votre mise en surbrillance. Si les commentaires de pointage étaient assez subtile pour commencer, vous ne constaterez certainement une différence.

**Rechercher des signaux regards et validation de synchronisation**: La synchronisation des signaux d’entrée est peut-être moins difficile pour les regards simple & validation, par conséquent, ne vous inquiétez pas ! Il est quelque chose à prendre en compte au cas où vous souhaitez utiliser des actions de validation plus complexes que qui peut impliquer des commandes vocales long ou mouvements de main compliqué. Imaginez que vous examinez cible et prononcez une commande longue vocale. Prise en compte l’heure à laquelle vous avez besoin de parler et l’heure à laquelle le système nécessaires pour détecter ce que vous l’avez dit, votre regard yeux est généralement long passé à une nouvelle cible dans la scène. Par conséquent, apportez vos utilisateurs qu’ils peuvent pas besoin de continuer à chercher à une cible jusqu'à ce que la commande a été reconnue ou gérer l’entrée de manière à déterminer le début de la commande et ce que l’utilisateur avait été regardez à l’époque.

## <a name="see-also"></a>Voir aussi
* [Suivre de la tête et valider](gaze-and-commit.md)
* [Mouvements de main](gestures.md)
* [Entrée vocale](voice-design.md)
* [Contrôleurs de mouvement](motion-controllers.md)
