---
title: Affichage de la progression
description: Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, contrôles, l’interface utilisateur, l’expérience utilisateur
ms.openlocfilehash: 84853a23a73bbece30c1f96b83e586642f3ab762
ms.sourcegitcommit: cf9f8ebbca0301e9d277853771ff6e47701ba1c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67523251"
---
# <a name="displaying-progress"></a>Affichage de la progression

Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours. Cela peut signifier que l’utilisateur ne peut pas interagir avec l’application lorsque l’indicateur de progression est visible et peut également indiquer le temps d’attente en fonction de l’indicateur utilisé.

![Exemple d’anneau de progression dans HoloLens](images/HoloLens2_Loader.gif)<br>
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
* [Scripts de progression et prefabs sur le Kit de ressources de réalité mixte](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/Features/UX/Prefabs/Loader)
* [zone englobante](app-bar-and-bounding-box.md)
* [Objet avec interaction possible](interactable-object.md)
* [Collection d’objets](object-collection.md)
* [Billboarding et tag-along](billboarding-and-tag-along.md)
