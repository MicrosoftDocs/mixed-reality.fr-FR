---
title: Tutoriels Azure Spatial Anchors - 3. Affichage du feedback sur les ancres spatiales Azure
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 62ce1151837a345dea1bea4a8bea275cc851b9bd
ms.sourcegitcommit: e65f1463aec3c040a1cd042e61fc2bd156a42ff8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83866899"
---
# <a name="3-displaying-azure-spatial-anchor-feedback"></a><span data-ttu-id="86f8a-105">3. Affichage du feedback sur les ancres spatiales Azure</span><span class="sxs-lookup"><span data-stu-id="86f8a-105">3. Displaying Azure Spatial Anchor feedback</span></span>

<span data-ttu-id="86f8a-106">Dans ce tutoriel, vous allez apprendre à fournir aux utilisateurs un feedback sur la découverte des ancres, leurs événements et leur état quand vous utilisez Azure Spatial Anchors (ASA).</span><span class="sxs-lookup"><span data-stu-id="86f8a-106">In this tutorial, you will learn how to provide users with feedback about anchor discovery, events, and status when using Azure Spatial Anchors (ASA).</span></span>

## <a name="objectives"></a><span data-ttu-id="86f8a-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="86f8a-107">Objectives</span></span>

* <span data-ttu-id="86f8a-108">Apprendre à configurer un panneau d’interface utilisateur qui affiche des informations importantes sur la session ASA en cours</span><span class="sxs-lookup"><span data-stu-id="86f8a-108">Learn how to set up a UI panel that displays important information about the current ASA session</span></span>
* <span data-ttu-id="86f8a-109">Comprendre et explorer les éléments de feedback que le SDK ASA met à la disposition des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="86f8a-109">Understand and explore feedback elements that the ASA SDK makes available to users</span></span>

## <a name="set-up-asa-feedback-ui-panel"></a><span data-ttu-id="86f8a-110">Configurer un panneau d’interface utilisateur pour le feedback ASA</span><span class="sxs-lookup"><span data-stu-id="86f8a-110">Set up ASA feedback UI panel</span></span>

<span data-ttu-id="86f8a-111">Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur l’objet **Instructions** > **TextContent** et sélectionnez **3D Object** > **Text - TextMeshPro** pour créer un objet texte TextMeshPro en tant qu’enfant de l’objet Instructions > TextContent et donnez-lui un nom approprié, par exemple **Feedback** :</span><span class="sxs-lookup"><span data-stu-id="86f8a-111">In the Hierarchy window, right-click on the **Instructions** > **TextContent** object and select **3D Object** > **Text - TextMeshPro** to create a TextMeshPro text object as a child of the Instructions > TextContent object and give it a suitable name, for example, **Feedback**:</span></span>

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-1.png)

> [!TIP]
> <span data-ttu-id="86f8a-113">Pour faciliter l’utilisation de votre scène, désactivez <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">Scene Visibility</a> pour l’objet ParentAnchor en cliquant sur l’icône œil à gauche de l’objet.</span><span class="sxs-lookup"><span data-stu-id="86f8a-113">To make it easier to work with your scene, set the  <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">Scene Visibility</a> for the ParentAnchor object to off by clicking the eye icon to the left of the object.</span></span> <span data-ttu-id="86f8a-114">Ceci masque l’objet dans la fenêtre Scene sans changer sa visibilité dans le jeu.</span><span class="sxs-lookup"><span data-stu-id="86f8a-114">This hides the object in the Scene window without changing their in-game visibility.</span></span>

<span data-ttu-id="86f8a-115">L’objet **Feedback** étant toujours sélectionné, dans la fenêtre Inspector, modifiez sa position et sa taille de manière à ce qu’il soit placé bien en dessous du texte d’instruction, par exemple :</span><span class="sxs-lookup"><span data-stu-id="86f8a-115">With the **Feedback** object still selected, in the Inspector window change its position and size so it is placed neatly underneath the instruction text, for example:</span></span>

* <span data-ttu-id="86f8a-116">Remplacez la valeur **Pos Y** de Rect Transform par -0,24.</span><span class="sxs-lookup"><span data-stu-id="86f8a-116">Change the Rect Transform **Pos Y** to -0.24</span></span>
* <span data-ttu-id="86f8a-117">Remplacez la valeur **Width** de Rect Transform par 0,555.</span><span class="sxs-lookup"><span data-stu-id="86f8a-117">Change the Rect Transform **Width** to 0.555</span></span>
* <span data-ttu-id="86f8a-118">Remplacez la valeur **Height** de Rect Transform par 0,1.</span><span class="sxs-lookup"><span data-stu-id="86f8a-118">Change the Rect Transform **Height** to 0.1</span></span>

<span data-ttu-id="86f8a-119">Choisissez ensuite les propriétés de police de sorte que le texte s’ajuste correctement dans la zone de texte, par exemple :</span><span class="sxs-lookup"><span data-stu-id="86f8a-119">Then choose font properties so the text fits nicely within the text area, for example:</span></span>

* <span data-ttu-id="86f8a-120">Remplacez la valeur **Font Style** de Text Mesh Pro (Script) par Bold.</span><span class="sxs-lookup"><span data-stu-id="86f8a-120">Change the Text Mesh Pro (Script) **Font Style** to Bold</span></span>
* <span data-ttu-id="86f8a-121">Remplacez la valeur **Font Size** de Text Mesh Pro (Script) par 0,17.</span><span class="sxs-lookup"><span data-stu-id="86f8a-121">Change the Text Mesh Pro (Script) **Font Size** to 0.17</span></span>
* <span data-ttu-id="86f8a-122">Remplacez la valeur **Alignment** de Text Mesh Pro (Script) par Center and Middle.</span><span class="sxs-lookup"><span data-stu-id="86f8a-122">Change the Text Mesh Pro (Script) **Alignment** to Center and Middle</span></span>

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-2.png)

<span data-ttu-id="86f8a-124">L’objet **Feedback** étant toujours sélectionné, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Anchor Feedback Script (Script)** à l’objet Feedback :</span><span class="sxs-lookup"><span data-stu-id="86f8a-124">With the **Feedback** object still selected, in the Inspector window, use the **Add Component** button to add the **Anchor Feedback Script (Script)** component to the Feedback object:</span></span>

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-3.png)

<span data-ttu-id="86f8a-126">Affectez l’objet **Feedback** lui-même au champ **Feedback Text** du composant **Anchor Feedback Script (Script)**  :</span><span class="sxs-lookup"><span data-stu-id="86f8a-126">Assign the **Feedback** object itself to the **Anchor Feedback Script (Script)** component's **Feedback Text** field:</span></span>

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-4.png)

## <a name="congratulations"></a><span data-ttu-id="86f8a-128">Félicitations</span><span class="sxs-lookup"><span data-stu-id="86f8a-128">Congratulations</span></span>

<span data-ttu-id="86f8a-129">Dans ce tutoriel, vous avez appris à créer un panneau d’interface utilisateur pour afficher l’état actuel de l’expérience Azure Spatial Anchors visant à fournir aux utilisateurs un feedback en temps réel.</span><span class="sxs-lookup"><span data-stu-id="86f8a-129">In this tutorial, you learned how to create a UI panel to display the current status of the Azure Spatial Anchor experience for providing users with real-time feedback.</span></span>

[<span data-ttu-id="86f8a-130">Leçon suivante : 4. Azure Spatial Anchors pour Android et iOS</span><span class="sxs-lookup"><span data-stu-id="86f8a-130">Next Lesson: 4. Azure Spatial Anchors for Android and iOS</span></span>](mrlearning-asa-ch4.md)
