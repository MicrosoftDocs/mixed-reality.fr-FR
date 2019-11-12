---
title: Didacticiels sur les ancres spatiales Azure-3. Affichage des commentaires sur l’ancrage spatial Azure
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 9f57cb9874aade2d6b19d0c061fd83eb04b9ef11
ms.sourcegitcommit: b6b76275fad90df6d9645dd2bc074b7b2168c7c8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/11/2019
ms.locfileid: "73914380"
---
# <a name="3-displaying-azure-spatial-anchor-feedback"></a><span data-ttu-id="8c8f3-105">3. affichage des commentaires sur l’ancrage spatial Azure</span><span class="sxs-lookup"><span data-stu-id="8c8f3-105">3. Displaying Azure Spatial Anchor feedback</span></span>

<span data-ttu-id="8c8f3-106">Dans cette leçon, vous allez apprendre à fournir aux utilisateurs des commentaires sur la découverte d’ancrage, les événements et l’état lors de l’utilisation d’ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="8c8f3-106">In this lesson, you'll learn how to provide users with feedback about anchor discovery, events and status when using Azure Spatial Anchors.</span></span>

## <a name="objectives"></a><span data-ttu-id="8c8f3-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="8c8f3-107">Objectives</span></span>

* <span data-ttu-id="8c8f3-108">Découvrez comment configurer un panneau d’interface utilisateur qui affiche des informations importantes sur la session ASA actuelle.</span><span class="sxs-lookup"><span data-stu-id="8c8f3-108">Learn how to set up a UI panel that displays important information about the current ASA session</span></span>

* <span data-ttu-id="8c8f3-109">Comprendre et explorer les éléments de commentaires que le kit de développement logiciel (SDK) ASA met à la disposition des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8c8f3-109">Understand and explore feedback elements that the ASA SDK makes available to users</span></span>

## <a name="instructions"></a><span data-ttu-id="8c8f3-110">Instructions</span><span class="sxs-lookup"><span data-stu-id="8c8f3-110">Instructions</span></span>

### <a name="set-up-asa-feedback-ui-panel"></a><span data-ttu-id="8c8f3-111">Panneau de l’interface utilisateur de configuration des commentaires ASA</span><span class="sxs-lookup"><span data-stu-id="8c8f3-111">Set Up ASA Feedback UI Panel</span></span>

1. <span data-ttu-id="8c8f3-112">Dans cette leçon, nous n’utilisons pas les boutons « SaveAnchorToDisk » et « ShareAnchor », donc sélectionnez les deux boutons et désactivez la case à cocher dans le panneau inspecteur (comme indiqué ci-dessous) pour masquer ces boutons.</span><span class="sxs-lookup"><span data-stu-id="8c8f3-112">In this lesson, we are not using the "SaveAnchorToDisk" and "ShareAnchor" buttons, so select both buttons and uncheck the checkbox in the inspector panel (as shown below) to hide these buttons.</span></span>
   

![module2chapter3step1im](images/module2chapter3step1im.PNG)

2. <span data-ttu-id="8c8f3-114">Créez le panneau d’instructions.</span><span class="sxs-lookup"><span data-stu-id="8c8f3-114">Create the instruction panel.</span></span> <span data-ttu-id="8c8f3-115">Commencez par cliquer avec le bouton droit sur le bouton « instructions », pointez sur « objet 3D », puis sélectionnez « textmeshpro-Text ».</span><span class="sxs-lookup"><span data-stu-id="8c8f3-115">Start by right-clicking the "instructions" button, hover over "3D Object" and select "textmeshpro-text."</span></span>

![module2chapter3step2im](images/module2chapter3step2im.PNG)

3. <span data-ttu-id="8c8f3-117">Ajustez l’échelle et le positionnement du texte afin qu’il corresponde aux instructions de votre scène.</span><span class="sxs-lookup"><span data-stu-id="8c8f3-117">Adjust the scale and positioning of the text, so that it matches with the instructions in your scene.</span></span> <span data-ttu-id="8c8f3-118">En outre, assurez-vous que l’alignement de tout le texte est centré.</span><span class="sxs-lookup"><span data-stu-id="8c8f3-118">Also, ensure the alignment for all of the text is centered.</span></span> <span data-ttu-id="8c8f3-119">Ensuite, supprimez l’exemple de texte de l’éditeur de texte, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8c8f3-119">Then delete the sample text from the text editor, as shown in in the image below.</span></span>

![module2chapter3step3im](images/module2chapter3step3im.PNG)

4. <span data-ttu-id="8c8f3-121">Remplacez le nom de l’objet TextMeshPro par « FeedbackPanel ».</span><span class="sxs-lookup"><span data-stu-id="8c8f3-121">Change the name of the TextMeshPro object to "FeedbackPanel."</span></span>
   

![module2chapter3step4im](images/module2chapter3step4im.PNG)

5. <span data-ttu-id="8c8f3-123">Assurez-vous que le texte « feedbackpanel » est sélectionné dans la hiérarchie ASA_feedback, cliquez sur « Ajouter un composant » et ajoutez le script d’ancrage de commentaires en le recherchant et en le sélectionnant une fois qu’il apparaît.</span><span class="sxs-lookup"><span data-stu-id="8c8f3-123">Ensure that the "feedbackpanel" text is selected in the ASA_feedback hierarchy, click "add component" and add the anchor feedback script by searching for it and selecting it once it appears.</span></span> 

![module2chapter3step8im](images/module2chapter3step8im.PNG)

6. <span data-ttu-id="8c8f3-125">Faites glisser l’objet de texte « feedbackPanel » de la hiérarchie ASA_Feedback vers l’emplacement vide sous le script, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8c8f3-125">Drag the "feedbackPanel" text object from the ASA_Feedback hierarchy into the empty slot beneath the script as seen in the picture below.</span></span> 

![module2chapter3step9im](images/module2chapter3step9im.PNG)

## <a name="congratulations"></a><span data-ttu-id="8c8f3-127">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="8c8f3-127">Congratulations</span></span>

<span data-ttu-id="8c8f3-128">Dans cette leçon, nous avons appris à créer un panneau d’interface utilisateur pour afficher l’état actuel de l’expérience d’ancrage spatial Azure pour fournir aux utilisateurs des commentaires en temps réel.</span><span class="sxs-lookup"><span data-stu-id="8c8f3-128">In this lesson, we learned how to create a UI panel to display the current status of the Azure Spatial Anchor experience for providing users with real-time feedback.</span></span>


