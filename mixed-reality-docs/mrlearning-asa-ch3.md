---
title: Didacticiels sur les ancres spatiales Azure-3. Affichage des commentaires sur l’ancrage spatial Azure
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 3d762950ea8e211fd5a8e4cf8af717674d3fe7e1
ms.sourcegitcommit: bd536f4f99c71418b55c121b7ba19ecbaf6336bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "77553929"
---
# <a name="3-displaying-azure-spatial-anchor-feedback"></a><span data-ttu-id="7429e-105">3. affichage des commentaires sur l’ancrage spatial Azure</span><span class="sxs-lookup"><span data-stu-id="7429e-105">3. Displaying Azure Spatial Anchor feedback</span></span>

<span data-ttu-id="7429e-106">Dans ce didacticiel, vous allez apprendre à fournir aux utilisateurs des commentaires sur la découverte d’ancrage, les événements et l’état lors de l’utilisation d’ancres spatiales Azure (ASA).</span><span class="sxs-lookup"><span data-stu-id="7429e-106">In this tutorial, you will learn how to provide users with feedback about anchor discovery, events, and status when using Azure Spatial Anchors (ASA).</span></span>

## <a name="objectives"></a><span data-ttu-id="7429e-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="7429e-107">Objectives</span></span>

* <span data-ttu-id="7429e-108">Découvrez comment configurer un panneau d’interface utilisateur qui affiche des informations importantes sur la session ASA actuelle.</span><span class="sxs-lookup"><span data-stu-id="7429e-108">Learn how to set up a UI panel that displays important information about the current ASA session</span></span>
* <span data-ttu-id="7429e-109">Comprendre et explorer les éléments de commentaires que le kit de développement logiciel (SDK) ASA met à la disposition des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="7429e-109">Understand and explore feedback elements that the ASA SDK makes available to users</span></span>

## <a name="set-up-asa-feedback-ui-panel"></a><span data-ttu-id="7429e-110">Panneau de l’interface utilisateur de configuration des commentaires ASA</span><span class="sxs-lookup"><span data-stu-id="7429e-110">Set up ASA feedback UI panel</span></span>

<span data-ttu-id="7429e-111">Dans la fenêtre hiérarchie, cliquez avec le bouton droit sur les **instructions** > objet **TextContent** et sélectionnez **objet 3D** > **texte-TextMeshPro** pour créer un objet de texte TextMeshPro en tant qu’enfant des instructions > objet TextContent et donnez-lui un nom approprié, par exemple, **Commentaires**:</span><span class="sxs-lookup"><span data-stu-id="7429e-111">In the Hierarchy window, right-click on the **Instructions** > **TextContent** object and select **3D Object** > **Text - TextMeshPro** to create a TextMeshPro text object as a child of the Instructions > TextContent object and give it a suitable name, for example, **Feedback**:</span></span>

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-1.png)

> [!TIP]
> <span data-ttu-id="7429e-113">Pour faciliter l’utilisation de votre scène, définissez l’option visibilité de la <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">scène</a> de l’objet ParentAnchor sur désactivé en cliquant sur l’icône représentant un œil à gauche de l’objet.</span><span class="sxs-lookup"><span data-stu-id="7429e-113">To make it easier to work with your scene, set the  <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">Scene Visibility</a> for the ParentAnchor object to off by clicking the eye icon to the left of the object.</span></span> <span data-ttu-id="7429e-114">Cela masque l’objet dans la fenêtre de scène sans modifier sa visibilité dans le jeu.</span><span class="sxs-lookup"><span data-stu-id="7429e-114">This hides the object in the Scene window without changing their in-game visibility.</span></span>

<span data-ttu-id="7429e-115">Lorsque l’objet de **Commentaires** est toujours sélectionné, dans la fenêtre de l’inspecteur, modifiez sa position et sa taille de manière à ce qu’il soit placé soigneusement sous le texte d’instruction, par exemple :</span><span class="sxs-lookup"><span data-stu-id="7429e-115">With the **Feedback** object still selected, in the Inspector window change its position and size so it is placed neatly underneath the instruction text, for example:</span></span>

* <span data-ttu-id="7429e-116">Remplacez le POS transformation Rect **Y** par-0,24</span><span class="sxs-lookup"><span data-stu-id="7429e-116">Change the Rect Transform **Pos Y** to -0.24</span></span>
* <span data-ttu-id="7429e-117">Modifiez la **largeur** de la transformation Rect en 0,555</span><span class="sxs-lookup"><span data-stu-id="7429e-117">Change the Rect Transform **Width** to 0.555</span></span>
* <span data-ttu-id="7429e-118">Modifier la **hauteur** de la transformation Rect en 0,1</span><span class="sxs-lookup"><span data-stu-id="7429e-118">Change the Rect Transform **Height** to 0.1</span></span>

<span data-ttu-id="7429e-119">Choisissez ensuite propriétés de police pour que le texte s’ajuste correctement dans la zone de texte, par exemple :</span><span class="sxs-lookup"><span data-stu-id="7429e-119">Then choose font properties so the text fits nicely within the text area, for example:</span></span>

* <span data-ttu-id="7429e-120">Modifier le **style de police** du texte de maillage Pro (script) en gras</span><span class="sxs-lookup"><span data-stu-id="7429e-120">Change the Text Mesh Pro (Script) **Font Style** to Bold</span></span>
* <span data-ttu-id="7429e-121">Modifier la **taille de police** du texte de maille Pro (script) à 0,17</span><span class="sxs-lookup"><span data-stu-id="7429e-121">Change the Text Mesh Pro (Script) **Font Size** to 0.17</span></span>
* <span data-ttu-id="7429e-122">Modifiez l' **alignement** du texte de maille Pro (script) en centre et au milieu</span><span class="sxs-lookup"><span data-stu-id="7429e-122">Change the Text Mesh Pro (Script) **Alignment** to Center and Middle</span></span>

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-2.png)

<span data-ttu-id="7429e-124">Lorsque l’objet de **Commentaires** est toujours sélectionné, dans la fenêtre de l’inspecteur, utilisez le bouton **Ajouter un composant** pour ajouter le composant script d' **ancrage de commentaires (script)** à l’objet de commentaires :</span><span class="sxs-lookup"><span data-stu-id="7429e-124">With the **Feedback** object still selected, in the Inspector window, use the **Add Component** button to add the **Anchor Feedback Script (Script)** component to the Feedback object:</span></span>

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-3.png)

<span data-ttu-id="7429e-126">Assignez l’objet de **Commentaires** lui-même au champ de texte de **Commentaire** du composant de **script d’ancrage de commentaires (script)** :</span><span class="sxs-lookup"><span data-stu-id="7429e-126">Assign the **Feedback** object itself to the **Anchor Feedback Script (Script)** component's **Feedback Text** field:</span></span>

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-4.png)

## <a name="congratulations"></a><span data-ttu-id="7429e-128">Félicitations</span><span class="sxs-lookup"><span data-stu-id="7429e-128">Congratulations</span></span>

<span data-ttu-id="7429e-129">Dans ce didacticiel, vous avez appris à créer un panneau d’interface utilisateur pour afficher l’état actuel de l’expérience d’ancrage spatial Azure pour fournir aux utilisateurs des commentaires en temps réel.</span><span class="sxs-lookup"><span data-stu-id="7429e-129">In this tutorial, you learned how to create a UI panel to display the current status of the Azure Spatial Anchor experience for providing users with real-time feedback.</span></span>
