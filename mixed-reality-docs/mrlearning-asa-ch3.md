---
title: Didacticiels sur les ancres spatiales Azure-3. Affichage des commentaires sur l’ancrage spatial Azure
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 77d639a88d8b4c71dc5fbe1c78565c4c3f91d36c
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438414"
---
# <a name="3-displaying-azure-spatial-anchor-feedback"></a><span data-ttu-id="ae4c8-105">3. affichage des commentaires sur l’ancrage spatial Azure</span><span class="sxs-lookup"><span data-stu-id="ae4c8-105">3. Displaying Azure Spatial Anchor feedback</span></span>

<span data-ttu-id="ae4c8-106">Dans cette leçon, vous allez apprendre à fournir aux utilisateurs des commentaires sur la découverte d’ancrage, les événements et l’état lors de l’utilisation d’ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-106">In this lesson, you'll learn how to provide users with feedback about anchor discovery, events and status when using Azure Spatial Anchors.</span></span>

## <a name="objectives"></a><span data-ttu-id="ae4c8-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="ae4c8-107">Objectives</span></span>

* <span data-ttu-id="ae4c8-108">Découvrez comment configurer un panneau d’interface utilisateur qui affiche des informations importantes sur la session ASA actuelle.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-108">Learn how to set up a UI panel that displays important information about the current ASA session</span></span>

* <span data-ttu-id="ae4c8-109">Comprendre et explorer les éléments de commentaires que le kit de développement logiciel (SDK) ASA met à la disposition des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ae4c8-109">Understand and explore feedback elements that the ASA SDK makes available to users</span></span>

## <a name="instructions"></a><span data-ttu-id="ae4c8-110">Instructions</span><span class="sxs-lookup"><span data-stu-id="ae4c8-110">Instructions</span></span>

### <a name="set-up-asa-feedback-ui-panel"></a><span data-ttu-id="ae4c8-111">Panneau de l’interface utilisateur de configuration des commentaires ASA</span><span class="sxs-lookup"><span data-stu-id="ae4c8-111">Set Up ASA Feedback UI Panel</span></span>

1. <span data-ttu-id="ae4c8-112">Dans cette leçon, nous n’utilisons pas les boutons « SaveAnchorToDisk » et « ShareAnchor », donc sélectionnez les deux boutons et désactivez la case à cocher dans le panneau inspecteur (comme indiqué ci-dessous) pour masquer ces boutons.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-112">In this lesson, we are not using the "SaveAnchorToDisk" and "ShareAnchor" buttons, so select both buttons and uncheck the checkbox in the inspector panel (as shown below) to hide these buttons.</span></span>
   

![module2chapter3step1im](images/module2chapter3step1im.PNG)

2. <span data-ttu-id="ae4c8-114">Créez le panneau d’instructions.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-114">Create the instruction panel.</span></span> <span data-ttu-id="ae4c8-115">Commencez par cliquer avec le bouton droit sur le bouton « instructions », pointez sur « objet 3D », puis sélectionnez « textmeshpro-Text ».</span><span class="sxs-lookup"><span data-stu-id="ae4c8-115">Start by right-clicking the "instructions" button, hover over "3D Object" and select "textmeshpro-text."</span></span>

![module2chapter3step2im](images/module2chapter3step2im.PNG)

3. <span data-ttu-id="ae4c8-117">Ajustez l’échelle et le positionnement du texte afin qu’il corresponde aux instructions de votre scène.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-117">Adjust the scale and positioning of the text, so that it matches with the instructions in your scene.</span></span> <span data-ttu-id="ae4c8-118">En outre, assurez-vous que l’alignement de tout le texte est centré.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-118">Also, ensure the alignment for all of the text is centered.</span></span> <span data-ttu-id="ae4c8-119">Ensuite, supprimez l’exemple de texte de l’éditeur de texte, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-119">Then delete the sample text from the text editor, as shown in in the image below.</span></span>

![module2chapter3step3im](images/module2chapter3step3im.PNG)

4. <span data-ttu-id="ae4c8-121">Remplacez le nom de l’objet TextMeshPro par « FeedbackPanel ».</span><span class="sxs-lookup"><span data-stu-id="ae4c8-121">Change the name of the TextMeshPro object to "FeedbackPanel."</span></span>
   

![module2chapter3step4im](images/module2chapter3step4im.PNG)

5. <span data-ttu-id="ae4c8-123">Dans le panneau projet, sélectionnez « ressources », cliquez avec le bouton droit, puis sélectionnez « Afficher dans l’Explorateur ».</span><span class="sxs-lookup"><span data-stu-id="ae4c8-123">In the project panel, select "assets" and right click, then select "show in explorer."</span></span>
   

![module2chapter3step4im](images/module2chapter3step5im.PNG)

<span data-ttu-id="ae4c8-125">Cliquez [ici](https://onedrive.live.com/?authkey=%21ABXEC8PvyQu8Qd8&id=5B7335C4342BCB0E%21395636&cid=5B7335C4342BCB0E) pour télécharger les fichiers nécessaires dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-125">Click [here](https://onedrive.live.com/?authkey=%21ABXEC8PvyQu8Qd8&id=5B7335C4342BCB0E%21395636&cid=5B7335C4342BCB0E) to download the files needed in the next few steps.</span></span>

6. <span data-ttu-id="ae4c8-126">Une fois que l’Explorateur s’ouvre, sélectionnez le dossier ressources, puis le dossier « ASAmodulesAssets » et copiez le script de commentaires d’ancrage et les fichiers de script du module d’ancrage dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-126">Once Explorer opens, select the Assets folder, then the "ASAmodulesAssets" folder and copy the anchor feedback script and the anchor module script files into the folder.</span></span> 

![module2chapter3step5im](images/module2chapter3step6im.PNG)

> <span data-ttu-id="ae4c8-128">Remarque : Si vous recevez un message contextuel vous demandant si vous souhaitez remplacer l’ancien ou conserver l’ancien, sélectionnez remplacer.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-128">note: if you get a pop-up message asking if you to overwrite the old or keep the old, select overwrite.</span></span>

7. <span data-ttu-id="ae4c8-129">Revenez au dossier Assets.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-129">Return to the Assets folder.</span></span> <span data-ttu-id="ae4c8-130">Ensuite, accédez au dossier « AzureSpatialAnchorsPlugin », suivi du dossier exemples et enfin du dossier scripts.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-130">Then, go into the "AzureSpatialAnchorsPlugin" folder, followed by the Examples folder and finally the Scripts folder.</span></span> <span data-ttu-id="ae4c8-131">Copiez ensuite le wrapper de démonstration des ancres spatiales Azure dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-131">Then copy the Azure Spatial Anchors demo wrapper into that folder.</span></span> 

![module2chapter3step8im](images/module2chapter3step7im.PNG)

8. <span data-ttu-id="ae4c8-133">Maintenant que les fichiers sont téléchargés, assurez-vous que le texte « feedbackpanel » est sélectionné dans la hiérarchie ASA_feedback, cliquez sur « Ajouter un composant » et ajoutez le script d’ancrage de commentaires en le recherchant et en le sélectionnant une fois qu’il apparaît.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-133">Now that the files are uploaded, ensure that the "feedbackpanel" text is selected in the ASA_feedback hierarchy, click "add component" and add the anchor feedback script by searching for it and selecting it once it appears.</span></span> 

![module2chapter3step8im](images/module2chapter3step8im.PNG)

9. <span data-ttu-id="ae4c8-135">Faites glisser l’objet de texte « feedbackPanel » de la hiérarchie ASA_Feedback vers l’emplacement vide sous le script, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-135">Drag the "feedbackPanel" text object from the ASA_Feedback hierarchy into the empty slot beneath the script as seen in the picture below.</span></span> 

![module2chapter3step9im](images/module2chapter3step9im.PNG)

## <a name="congratulations"></a><span data-ttu-id="ae4c8-137">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="ae4c8-137">Congratulations</span></span>

<span data-ttu-id="ae4c8-138">Dans cette leçon, nous avons appris à créer un panneau d’interface utilisateur pour afficher l’état actuel de l’expérience d’ancrage spatial Azure pour fournir aux utilisateurs des commentaires en temps réel.</span><span class="sxs-lookup"><span data-stu-id="ae4c8-138">In this lesson, we learned how to create a UI panel to display the current status of the Azure Spatial Anchor experience for providing users with real-time feedback.</span></span>


