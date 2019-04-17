---
title: Affichage de la progression
description: Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, contrôles, l’interface utilisateur, l’expérience utilisateur
ms.openlocfilehash: 9edddc7800f0d7334d1ceba97b9a06fd6d4580ac
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596017"
---
# <a name="displaying-progress"></a>Affichage de la progression

Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours. Cela peut signifier que l’utilisateur ne peut pas interagir avec l’application lorsque l’indicateur de progression est visible et peut également indiquer le temps d’attente en fonction de l’indicateur utilisé.

![Exemple d’anneau de progression dans HoloLens](images/640px-progress-hero.jpg)<br>
*Exemple d’anneau de progression dans HoloLens*

## <a name="types-of-progress"></a>Types de progression

Il est important de fournir les informations utilisateur sur ce qui se passe. En réalité mixte les utilisateurs peuvent être facilement distraits par environnement physique ou d’objets si votre application n’utilise pas donne une bonne visuelles. Dans les situations qui prennent quelques secondes, par exemple lors du chargement de données ou une scène est mise à jour, il est recommandé pour afficher un indicateur visuel. Il existe deux options permettant à l’utilisateur qu’une opération est en cours d’exécution – un **barre de progression** ou un **boucle de progression**.

### <a name="progress-bar"></a>Barre de progression

![Exemple de barre de progression dans HoloLens](images/640px-progressbar.jpg)

Une barre de progression affiche le pourcentage d’achèvement d’une tâche. Il doit être utilisé lors d’une opération dont la durée est connue (déterminée), mais sa progression ne doit pas bloquer l’interaction utilisateur avec l’application.

### <a name="progress-ring"></a>Anneau de progression

![Exemple d’anneau de progression dans HoloLens](images/640px-progressring.jpg)

Une boucle de progression a un état indéterminé uniquement et doit être utilisée lors de l’interaction supplémentaire de l’utilisateur est bloquée jusqu'à ce que l’opération est terminée.

### <a name="progress-with-a-custom-object"></a>Progression avec un objet personnalisé

![Progression avec exemple de maillage personnalisé dans HoloLens](images/640px-progresscustom.jpg)

Vous pouvez ajouter à la personnalité et une identité de marque de votre application en personnalisant le contrôle de progression avec vos propres objets 2D/3D personnalisés.

## <a name="best-practices"></a>Meilleures pratiques
* Coupler étroitement [le billboarding ou tag-along](billboarding-and-tag-along.md) à l’affichage de la progression dans la mesure où l’utilisateur peut facilement déplacer leur tête dans un espace vide et perdre du contexte. Votre application peut se présenter comme il s’est arrêté anormalement si l’utilisateur ne peut pas voir de quoi que ce soit. Billboarding et tag-along intègre le préfabriqué de progression.
* Il est toujours judicieux de fournir des informations d’état sur ce qui se passe à l’utilisateur. Le préfabriqué progression fournit différents styles visuels, y compris la progression de type d’anneau standard de Windows pour fournir l’état. Vous pouvez également utiliser une maille personnalisée avec une animation, si vous souhaitez que le style de votre progression pour l’aligner sur la marque de votre application.

## <a name="see-also"></a>Voir aussi
* [Scripts et prefabs pour la progression sur le Kit de ressources de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/UX/Readme/README_ProgressExample.md)
* [Objet sur](interactable-object.md)
* [Collection d’objets](object-collection.md)
* [Le billboarding et tag-along](billboarding-and-tag-along.md)
