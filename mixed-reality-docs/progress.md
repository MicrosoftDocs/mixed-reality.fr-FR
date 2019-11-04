---
title: Affichage de la progression
description: Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, design, Controls, UI, UX
ms.openlocfilehash: 43b4802e7c821c98c847509ace950f381da12f95
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437538"
---
# <a name="displaying-progress"></a><span data-ttu-id="83474-104">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="83474-104">Displaying progress</span></span>

<br>

<img src="images/HoloLens2_Loader.gif" alt="Progress ring example in HoloLens" width="940px">

<span data-ttu-id="83474-105">Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours.</span><span class="sxs-lookup"><span data-stu-id="83474-105">A progress control provides feedback to the user that a long-running operation is underway.</span></span> <span data-ttu-id="83474-106">Cela peut signifier que l’utilisateur ne peut pas interagir avec l’application lorsque l’indicateur de progression est visible et peut également indiquer le temps d’attente en fonction de l’indicateur utilisé.</span><span class="sxs-lookup"><span data-stu-id="83474-106">It can mean that the user cannot interact with the app when the progress indicator is visible, and can also indicate how long the wait time might be, depending on the indicator used.</span></span>

<br>

---

## <a name="types-of-progress"></a><span data-ttu-id="83474-107">Types de progression</span><span class="sxs-lookup"><span data-stu-id="83474-107">Types of progress</span></span>

<span data-ttu-id="83474-108">Il est important de fournir les informations de l’utilisateur sur ce qui se passe.</span><span class="sxs-lookup"><span data-stu-id="83474-108">It is important to provide the user information about what is happening.</span></span> <span data-ttu-id="83474-109">Dans la réalité mixte, les utilisateurs peuvent être facilement gênés par un environnement ou des objets physiques si votre application ne donne pas de bons commentaires visuels.</span><span class="sxs-lookup"><span data-stu-id="83474-109">In mixed reality users can be easily distracted by physical environment or objects if your app does not gives good visual feedback.</span></span> <span data-ttu-id="83474-110">Pour les situations qui prennent quelques secondes, telles que le chargement des données ou la mise à jour d’une scène, il est judicieux d’afficher un indicateur visuel.</span><span class="sxs-lookup"><span data-stu-id="83474-110">For situations that take a few seconds, such when data is loading or a scene is updating, it is good idea to show a visual indicator.</span></span> <span data-ttu-id="83474-111">Il existe deux options pour montrer à l’utilisateur qu’une opération est en cours d’exécution : une **barre de progression** ou un **anneau de progression**.</span><span class="sxs-lookup"><span data-stu-id="83474-111">There are two options to show the user that an operation is underway – a **Progress bar** or a **Progress ring**.</span></span>

:::row:::
    :::column:::
        ### <a name="progress-barbr"></a><span data-ttu-id="83474-112">Barre de progression</span><span class="sxs-lookup"><span data-stu-id="83474-112">Progress bar</span></span><br>
        <span data-ttu-id="83474-113">Une barre de progression indique le pourcentage d’achèvement d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="83474-113">A Progress bar shows the percentage completed of a task.</span></span> <span data-ttu-id="83474-114">Elle doit être utilisée pendant une opération dont la durée est connue (arrêt), mais la progression ne doit pas bloquer l’interaction de l’utilisateur avec l’application.</span><span class="sxs-lookup"><span data-stu-id="83474-114">It should be used during an operation whose duration is known (determinate), but it's progress should not block the user's interaction with the app.</span></span><br>
        <br>
        <span data-ttu-id="83474-115">*Image : exemple de barre de progression dans HoloLens*</span><span class="sxs-lookup"><span data-stu-id="83474-115">*Image: Progress bar example in HoloLens*</span></span>
    :::column-end:::
        :::column:::
        <span data-ttu-id="83474-116">espace de ![](images/spacer-20x582.png)</span><span class="sxs-lookup"><span data-stu-id="83474-116">![space](images/spacer-20x582.png)</span></span><br>
       <span data-ttu-id="83474-117">exemple de barre de progression ![dans HoloLens](images/640px-progressbar.jpg)</span><span class="sxs-lookup"><span data-stu-id="83474-117">![Progress bar example in HoloLens](images/640px-progressbar.jpg)</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

:::row:::
    :::column:::
        ### <a name="progress-ringbr"></a><span data-ttu-id="83474-118">Anneau de progression</span><span class="sxs-lookup"><span data-stu-id="83474-118">Progress ring</span></span><br>
        <span data-ttu-id="83474-119">Un anneau de progression n’a qu’un état indéterminé et doit être utilisé quand une interaction utilisateur supplémentaire est bloquée jusqu’à ce que l’opération soit terminée.</span><span class="sxs-lookup"><span data-stu-id="83474-119">A Progress ring only has an indeterminate state, and should be used when any further user interaction is blocked until the operation has completed.</span></span><br>
        <br>
        <span data-ttu-id="83474-120">*Image : exemple de sonnerie de progression dans HoloLens*</span><span class="sxs-lookup"><span data-stu-id="83474-120">*Image: Progress ring example in HoloLens*</span></span>
    :::column-end:::
        :::column:::
        <span data-ttu-id="83474-121">espace de ![](images/spacer-20x582.png)</span><span class="sxs-lookup"><span data-stu-id="83474-121">![space](images/spacer-20x582.png)</span></span><br>
       <span data-ttu-id="83474-122">![exemple de sonnerie de progression dans HoloLens](images/640px-progressring.jpg)</span><span class="sxs-lookup"><span data-stu-id="83474-122">![Progress ring example in HoloLens](images/640px-progressring.jpg)</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

:::row:::
    :::column:::
        ### <a name="progress-with-a-custom-objectbr"></a><span data-ttu-id="83474-123">Progression avec un objet personnalisé</span><span class="sxs-lookup"><span data-stu-id="83474-123">Progress with a custom object</span></span><br>
        <span data-ttu-id="83474-124">Vous pouvez ajouter à la personnalité et à l’identité de votre application en personnalisant le contrôle de progression avec vos propres objets 2D/3D personnalisés.</span><span class="sxs-lookup"><span data-stu-id="83474-124">You can add to your app's personality and brand identity by customizing the Progress control with your own custom 2D/3D objects.</span></span><br>
        <br>
        <span data-ttu-id="83474-125">*Image : progression avec un exemple de maillage personnalisé dans HoloLens*</span><span class="sxs-lookup"><span data-stu-id="83474-125">*Image: Progress with custom mesh example in HoloLens*</span></span>
    :::column-end:::
        :::column:::
        <span data-ttu-id="83474-126">espace de ![](images/spacer-20x582.png)</span><span class="sxs-lookup"><span data-stu-id="83474-126">![space](images/spacer-20x582.png)</span></span><br>
       <span data-ttu-id="83474-127">![la progression avec l’exemple de maille personnalisé dans HoloLens](images/640px-progresscustom.jpg)</span><span class="sxs-lookup"><span data-stu-id="83474-127">![Progress with custom mesh example in HoloLens](images/640px-progresscustom.jpg)</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="best-practices"></a><span data-ttu-id="83474-128">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="83474-128">Best practices</span></span>
* <span data-ttu-id="83474-129">Couplez étroitement le [billboarding ou la balise](billboarding-and-tag-along.md) à l’affichage de la progression puisque l’utilisateur peut facilement déplacer son tête dans un espace vide et perdre le contexte.</span><span class="sxs-lookup"><span data-stu-id="83474-129">Tightly couple [billboarding or tag-along](billboarding-and-tag-along.md) to the display of Progress since the user can easily move their head into empty space and lose context.</span></span> <span data-ttu-id="83474-130">Votre application peut sembler se bloquer si l’utilisateur ne parvient pas à voir quoi que ce soit.</span><span class="sxs-lookup"><span data-stu-id="83474-130">Your app might look like it has crashed if the user is unable to see anything.</span></span> <span data-ttu-id="83474-131">Le billboarding et la balise sont intégrés au Prefab Progress.</span><span class="sxs-lookup"><span data-stu-id="83474-131">Billboarding and tag-along is built into the Progress prefab.</span></span>
* <span data-ttu-id="83474-132">Il est toujours judicieux de fournir des informations d’État sur ce qui se passe à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="83474-132">It's always good to provide status information about what is happening to the user.</span></span> <span data-ttu-id="83474-133">Le Prefab de progression fournit différents styles visuels, y compris la progression de type Ring Windows standard pour la fourniture de l’État.</span><span class="sxs-lookup"><span data-stu-id="83474-133">The Progress prefab provides various visual styles including the Windows standard ring-type progress for providing status.</span></span> <span data-ttu-id="83474-134">Vous pouvez également utiliser une maille personnalisée avec une animation si vous souhaitez que le style de la progression s’aligne sur la personnalisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="83474-134">You can also use a custom mesh with an animation if you want the style of your progress to align to your app’s brand.</span></span>

<br>

---

## <a name="see-also"></a><span data-ttu-id="83474-135">Articles associés</span><span class="sxs-lookup"><span data-stu-id="83474-135">See also</span></span>
* [<span data-ttu-id="83474-136">Scripts de progression et prefabs sur le Toolkit de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="83474-136">Progress scripts and prefabs on Mixed Reality Toolkit</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/Features/UX/Prefabs/Loader)
* [<span data-ttu-id="83474-137">Cadre englobant</span><span class="sxs-lookup"><span data-stu-id="83474-137">Bounding box</span></span>](app-bar-and-bounding-box.md)
* [<span data-ttu-id="83474-138">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="83474-138">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="83474-139">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="83474-139">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="83474-140">Billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="83474-140">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
