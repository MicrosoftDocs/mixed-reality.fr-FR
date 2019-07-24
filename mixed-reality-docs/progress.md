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
# <a name="displaying-progress"></a><span data-ttu-id="120b5-104">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="120b5-104">Displaying progress</span></span>

<span data-ttu-id="120b5-105">Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours.</span><span class="sxs-lookup"><span data-stu-id="120b5-105">A progress control provides feedback to the user that a long-running operation is underway.</span></span> <span data-ttu-id="120b5-106">Cela peut signifier que l’utilisateur ne peut pas interagir avec l’application lorsque l’indicateur de progression est visible et peut également indiquer le temps d’attente en fonction de l’indicateur utilisé.</span><span class="sxs-lookup"><span data-stu-id="120b5-106">It can mean that the user cannot interact with the app when the progress indicator is visible, and can also indicate how long the wait time might be, depending on the indicator used.</span></span>

<span data-ttu-id="120b5-107">![Exemple de sonnerie de progression dans HoloLens](images/HoloLens2_Loader.gif)</span><span class="sxs-lookup"><span data-stu-id="120b5-107">![Progress ring example in HoloLens](images/HoloLens2_Loader.gif)</span></span><br>
<span data-ttu-id="120b5-108">*Exemple de sonnerie de progression dans HoloLens*</span><span class="sxs-lookup"><span data-stu-id="120b5-108">*Progress ring example in HoloLens*</span></span>

## <a name="types-of-progress"></a><span data-ttu-id="120b5-109">Types de progression</span><span class="sxs-lookup"><span data-stu-id="120b5-109">Types of progress</span></span>

<span data-ttu-id="120b5-110">Il est important de fournir les informations de l’utilisateur sur ce qui se passe.</span><span class="sxs-lookup"><span data-stu-id="120b5-110">It is important to provide the user information about what is happening.</span></span> <span data-ttu-id="120b5-111">Dans la réalité mixte, les utilisateurs peuvent être facilement gênés par un environnement ou des objets physiques si votre application ne donne pas de bons commentaires visuels.</span><span class="sxs-lookup"><span data-stu-id="120b5-111">In mixed reality users can be easily distracted by physical environment or objects if your app does not gives good visual feedback.</span></span> <span data-ttu-id="120b5-112">Pour les situations qui prennent quelques secondes, telles que le chargement des données ou la mise à jour d’une scène, il est judicieux d’afficher un indicateur visuel.</span><span class="sxs-lookup"><span data-stu-id="120b5-112">For situations that take a few seconds, such when data is loading or a scene is updating, it is good idea to show a visual indicator.</span></span> <span data-ttu-id="120b5-113">Il existe deux options pour montrer à l’utilisateur qu’une opération est en cours d’exécution: une **barre de progression** ou un **anneau de progression**.</span><span class="sxs-lookup"><span data-stu-id="120b5-113">There are two options to show the user that an operation is underway – a **Progress bar** or a **Progress ring**.</span></span>

### <a name="progress-bar"></a><span data-ttu-id="120b5-114">Barre de progression</span><span class="sxs-lookup"><span data-stu-id="120b5-114">Progress bar</span></span>

![Exemple de barre de progression dans HoloLens](images/640px-progressbar.jpg)

<span data-ttu-id="120b5-116">Une barre de progression indique le pourcentage d’achèvement d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="120b5-116">A Progress bar shows the percentage completed of a task.</span></span> <span data-ttu-id="120b5-117">Elle doit être utilisée pendant une opération dont la durée est connue (arrêt), mais la progression ne doit pas bloquer l’interaction de l’utilisateur avec l’application.</span><span class="sxs-lookup"><span data-stu-id="120b5-117">It should be used during an operation whose duration is known (determinate), but it's progress should not block the user's interaction with the app.</span></span>

### <a name="progress-ring"></a><span data-ttu-id="120b5-118">Anneau de progression</span><span class="sxs-lookup"><span data-stu-id="120b5-118">Progress ring</span></span>

![Exemple de sonnerie de progression dans HoloLens](images/640px-progressring.jpg)

<span data-ttu-id="120b5-120">Un anneau de progression n’a qu’un état indéterminé et doit être utilisé quand une interaction utilisateur supplémentaire est bloquée jusqu’à ce que l’opération soit terminée.</span><span class="sxs-lookup"><span data-stu-id="120b5-120">A Progress ring only has an indeterminate state, and should be used when any further user interaction is blocked until the operation has completed.</span></span>

### <a name="progress-with-a-custom-object"></a><span data-ttu-id="120b5-121">Progression avec un objet personnalisé</span><span class="sxs-lookup"><span data-stu-id="120b5-121">Progress with a custom object</span></span>

![Progression avec l’exemple de maille personnalisé dans HoloLens](images/640px-progresscustom.jpg)

<span data-ttu-id="120b5-123">Vous pouvez ajouter à la personnalité et à l’identité de votre application en personnalisant le contrôle de progression avec vos propres objets 2D/3D personnalisés.</span><span class="sxs-lookup"><span data-stu-id="120b5-123">You can add to your app's personality and brand identity by customizing the Progress control with your own custom 2D/3D objects.</span></span>

## <a name="best-practices"></a><span data-ttu-id="120b5-124">Bonnes pratiques</span><span class="sxs-lookup"><span data-stu-id="120b5-124">Best practices</span></span>
* <span data-ttu-id="120b5-125">Couplez étroitement le [billboarding ou](billboarding-and-tag-along.md) la balise à l’affichage de la progression puisque l’utilisateur peut facilement déplacer son tête dans un espace vide et perdre le contexte.</span><span class="sxs-lookup"><span data-stu-id="120b5-125">Tightly couple [billboarding or tag-along](billboarding-and-tag-along.md) to the display of Progress since the user can easily move their head into empty space and lose context.</span></span> <span data-ttu-id="120b5-126">Votre application peut sembler se bloquer si l’utilisateur ne parvient pas à voir quoi que ce soit.</span><span class="sxs-lookup"><span data-stu-id="120b5-126">Your app might look like it has crashed if the user is unable to see anything.</span></span> <span data-ttu-id="120b5-127">Le billboarding et la balise sont intégrés au Prefab Progress.</span><span class="sxs-lookup"><span data-stu-id="120b5-127">Billboarding and tag-along is built into the Progress prefab.</span></span>
* <span data-ttu-id="120b5-128">Il est toujours judicieux de fournir des informations d’État sur ce qui se passe à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="120b5-128">It's always good to provide status information about what is happening to the user.</span></span> <span data-ttu-id="120b5-129">Le Prefab de progression fournit différents styles visuels, y compris la progression de type Ring Windows standard pour la fourniture de l’État.</span><span class="sxs-lookup"><span data-stu-id="120b5-129">The Progress prefab provides various visual styles including the Windows standard ring-type progress for providing status.</span></span> <span data-ttu-id="120b5-130">Vous pouvez également utiliser une maille personnalisée avec une animation si vous souhaitez que le style de la progression s’aligne sur la personnalisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="120b5-130">You can also use a custom mesh with an animation if you want the style of your progress to align to your app’s brand.</span></span>

## <a name="see-also"></a><span data-ttu-id="120b5-131">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="120b5-131">See also</span></span>
* [<span data-ttu-id="120b5-132">Scripts de progression et prefabs sur le Toolkit de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="120b5-132">Progress scripts and prefabs on Mixed Reality Toolkit</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/Features/UX/Prefabs/Loader)
* [<span data-ttu-id="120b5-133">Cadre englobant</span><span class="sxs-lookup"><span data-stu-id="120b5-133">Bounding box</span></span>](app-bar-and-bounding-box.md)
* [<span data-ttu-id="120b5-134">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="120b5-134">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="120b5-135">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="120b5-135">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="120b5-136">Billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="120b5-136">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
