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
# <a name="displaying-progress"></a><span data-ttu-id="96ff0-104">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="96ff0-104">Displaying progress</span></span>

<span data-ttu-id="96ff0-105">Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours.</span><span class="sxs-lookup"><span data-stu-id="96ff0-105">A progress control provides feedback to the user that a long-running operation is underway.</span></span> <span data-ttu-id="96ff0-106">Cela peut signifier que l’utilisateur ne peut pas interagir avec l’application lorsque l’indicateur de progression est visible et peut également indiquer le temps d’attente en fonction de l’indicateur utilisé.</span><span class="sxs-lookup"><span data-stu-id="96ff0-106">It can mean that the user cannot interact with the app when the progress indicator is visible, and can also indicate how long the wait time might be, depending on the indicator used.</span></span>

<span data-ttu-id="96ff0-107">![Exemple d’anneau de progression dans HoloLens](images/640px-progress-hero.jpg)</span><span class="sxs-lookup"><span data-stu-id="96ff0-107">![Progress ring example in HoloLens](images/640px-progress-hero.jpg)</span></span><br>
<span data-ttu-id="96ff0-108">*Exemple d’anneau de progression dans HoloLens*</span><span class="sxs-lookup"><span data-stu-id="96ff0-108">*Progress ring example in HoloLens*</span></span>

## <a name="types-of-progress"></a><span data-ttu-id="96ff0-109">Types de progression</span><span class="sxs-lookup"><span data-stu-id="96ff0-109">Types of progress</span></span>

<span data-ttu-id="96ff0-110">Il est important de fournir les informations utilisateur sur ce qui se passe.</span><span class="sxs-lookup"><span data-stu-id="96ff0-110">It is important to provide the user information about what is happening.</span></span> <span data-ttu-id="96ff0-111">En réalité mixte les utilisateurs peuvent être facilement distraits par environnement physique ou d’objets si votre application n’utilise pas donne une bonne visuelles.</span><span class="sxs-lookup"><span data-stu-id="96ff0-111">In mixed reality users can be easily distracted by physical environment or objects if your app does not gives good visual feedback.</span></span> <span data-ttu-id="96ff0-112">Dans les situations qui prennent quelques secondes, par exemple lors du chargement de données ou une scène est mise à jour, il est recommandé pour afficher un indicateur visuel.</span><span class="sxs-lookup"><span data-stu-id="96ff0-112">For situations that take a few seconds, such when data is loading or a scene is updating, it is good idea to show a visual indicator.</span></span> <span data-ttu-id="96ff0-113">Il existe deux options permettant à l’utilisateur qu’une opération est en cours d’exécution – un **barre de progression** ou un **boucle de progression**.</span><span class="sxs-lookup"><span data-stu-id="96ff0-113">There are two options to show the user that an operation is underway – a **Progress bar** or a **Progress ring**.</span></span>

### <a name="progress-bar"></a><span data-ttu-id="96ff0-114">Barre de progression</span><span class="sxs-lookup"><span data-stu-id="96ff0-114">Progress bar</span></span>

![Exemple de barre de progression dans HoloLens](images/640px-progressbar.jpg)

<span data-ttu-id="96ff0-116">Une barre de progression affiche le pourcentage d’achèvement d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="96ff0-116">A Progress bar shows the percentage completed of a task.</span></span> <span data-ttu-id="96ff0-117">Il doit être utilisé lors d’une opération dont la durée est connue (déterminée), mais sa progression ne doit pas bloquer l’interaction utilisateur avec l’application.</span><span class="sxs-lookup"><span data-stu-id="96ff0-117">It should be used during an operation whose duration is known (determinate), but it's progress should not block the user's interaction with the app.</span></span>

### <a name="progress-ring"></a><span data-ttu-id="96ff0-118">Anneau de progression</span><span class="sxs-lookup"><span data-stu-id="96ff0-118">Progress ring</span></span>

![Exemple d’anneau de progression dans HoloLens](images/640px-progressring.jpg)

<span data-ttu-id="96ff0-120">Une boucle de progression a un état indéterminé uniquement et doit être utilisée lors de l’interaction supplémentaire de l’utilisateur est bloquée jusqu'à ce que l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="96ff0-120">A Progress ring only has an indeterminate state, and should be used when any further user interaction is blocked until the operation has completed.</span></span>

### <a name="progress-with-a-custom-object"></a><span data-ttu-id="96ff0-121">Progression avec un objet personnalisé</span><span class="sxs-lookup"><span data-stu-id="96ff0-121">Progress with a custom object</span></span>

![Progression avec exemple de maillage personnalisé dans HoloLens](images/640px-progresscustom.jpg)

<span data-ttu-id="96ff0-123">Vous pouvez ajouter à la personnalité et une identité de marque de votre application en personnalisant le contrôle de progression avec vos propres objets 2D/3D personnalisés.</span><span class="sxs-lookup"><span data-stu-id="96ff0-123">You can add to your app's personality and brand identity by customizing the Progress control with your own custom 2D/3D objects.</span></span>

## <a name="best-practices"></a><span data-ttu-id="96ff0-124">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="96ff0-124">Best practices</span></span>
* <span data-ttu-id="96ff0-125">Coupler étroitement [le billboarding ou tag-along](billboarding-and-tag-along.md) à l’affichage de la progression dans la mesure où l’utilisateur peut facilement déplacer leur tête dans un espace vide et perdre du contexte.</span><span class="sxs-lookup"><span data-stu-id="96ff0-125">Tightly couple [billboarding or tag-along](billboarding-and-tag-along.md) to the display of Progress since the user can easily move their head into empty space and lose context.</span></span> <span data-ttu-id="96ff0-126">Votre application peut se présenter comme il s’est arrêté anormalement si l’utilisateur ne peut pas voir de quoi que ce soit.</span><span class="sxs-lookup"><span data-stu-id="96ff0-126">Your app might look like it has crashed if the user is unable to see anything.</span></span> <span data-ttu-id="96ff0-127">Billboarding et tag-along intègre le préfabriqué de progression.</span><span class="sxs-lookup"><span data-stu-id="96ff0-127">Billboarding and tag-along is built into the Progress prefab.</span></span>
* <span data-ttu-id="96ff0-128">Il est toujours judicieux de fournir des informations d’état sur ce qui se passe à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="96ff0-128">It's always good to provide status information about what is happening to the user.</span></span> <span data-ttu-id="96ff0-129">Le préfabriqué progression fournit différents styles visuels, y compris la progression de type d’anneau standard de Windows pour fournir l’état.</span><span class="sxs-lookup"><span data-stu-id="96ff0-129">The Progress prefab provides various visual styles including the Windows standard ring-type progress for providing status.</span></span> <span data-ttu-id="96ff0-130">Vous pouvez également utiliser une maille personnalisée avec une animation, si vous souhaitez que le style de votre progression pour l’aligner sur la marque de votre application.</span><span class="sxs-lookup"><span data-stu-id="96ff0-130">You can also use a custom mesh with an animation if you want the style of your progress to align to your app’s brand.</span></span>

## <a name="see-also"></a><span data-ttu-id="96ff0-131">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="96ff0-131">See also</span></span>
* [<span data-ttu-id="96ff0-132">Scripts et prefabs pour la progression sur le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="96ff0-132">Scripts and prefabs for Progress on Mixed Reality Toolkit</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/UX/Readme/README_ProgressExample.md)
* [<span data-ttu-id="96ff0-133">Objet sur</span><span class="sxs-lookup"><span data-stu-id="96ff0-133">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="96ff0-134">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="96ff0-134">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="96ff0-135">Le billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="96ff0-135">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
