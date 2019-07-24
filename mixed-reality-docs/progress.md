---
title: Affichage de la progression
description: Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, design, Controls, UI, UX
ms.openlocfilehash: 84853a23a73bbece30c1f96b83e586642f3ab762
ms.sourcegitcommit: cf9f8ebbca0301e9d277853771ff6e47701ba1c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67523251"
---
# <a name="displaying-progress"></a>Affichage de la progression

Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours. Cela peut signifier que l’utilisateur ne peut pas interagir avec l’application lorsque l’indicateur de progression est visible et peut également indiquer le temps d’attente en fonction de l’indicateur utilisé.

![Exemple de sonnerie de progression dans HoloLens](images/HoloLens2_Loader.gif)<br>
*Exemple de sonnerie de progression dans HoloLens*

## <a name="types-of-progress"></a>Types de progression

Il est important de fournir les informations de l’utilisateur sur ce qui se passe. Dans la réalité mixte, les utilisateurs peuvent être facilement gênés par un environnement ou des objets physiques si votre application ne donne pas de bons commentaires visuels. Pour les situations qui prennent quelques secondes, telles que le chargement des données ou la mise à jour d’une scène, il est judicieux d’afficher un indicateur visuel. Il existe deux options pour montrer à l’utilisateur qu’une opération est en cours d’exécution: une **barre de progression** ou un **anneau de progression**.

### <a name="progress-bar"></a>Barre de progression

![Exemple de barre de progression dans HoloLens](images/640px-progressbar.jpg)

Une barre de progression indique le pourcentage d’achèvement d’une tâche. Elle doit être utilisée pendant une opération dont la durée est connue (arrêt), mais la progression ne doit pas bloquer l’interaction de l’utilisateur avec l’application.

### <a name="progress-ring"></a>Anneau de progression

![Exemple de sonnerie de progression dans HoloLens](images/640px-progressring.jpg)

Un anneau de progression n’a qu’un état indéterminé et doit être utilisé quand une interaction utilisateur supplémentaire est bloquée jusqu’à ce que l’opération soit terminée.

### <a name="progress-with-a-custom-object"></a>Progression avec un objet personnalisé

![Progression avec l’exemple de maille personnalisé dans HoloLens](images/640px-progresscustom.jpg)

Vous pouvez ajouter à la personnalité et à l’identité de votre application en personnalisant le contrôle de progression avec vos propres objets 2D/3D personnalisés.

## <a name="best-practices"></a>Bonnes pratiques
* Couplez étroitement le [billboarding ou](billboarding-and-tag-along.md) la balise à l’affichage de la progression puisque l’utilisateur peut facilement déplacer son tête dans un espace vide et perdre le contexte. Votre application peut sembler se bloquer si l’utilisateur ne parvient pas à voir quoi que ce soit. Le billboarding et la balise sont intégrés au Prefab Progress.
* Il est toujours judicieux de fournir des informations d’État sur ce qui se passe à l’utilisateur. Le Prefab de progression fournit différents styles visuels, y compris la progression de type Ring Windows standard pour la fourniture de l’État. Vous pouvez également utiliser une maille personnalisée avec une animation si vous souhaitez que le style de la progression s’aligne sur la personnalisation de votre application.

## <a name="see-also"></a>Voir aussi
* [Scripts de progression et prefabs sur le Toolkit de réalité mixte](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/Features/UX/Prefabs/Loader)
* [Cadre englobant](app-bar-and-bounding-box.md)
* [Objet avec interaction possible](interactable-object.md)
* [Collection d’objets](object-collection.md)
* [Billboarding et tag-along](billboarding-and-tag-along.md)
