---
title: Module ASA d’apprentissage de la fonction d’ancrage spatial Azure sur HoloLens 2
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: c6e902710eebe205b9e944b1bf95a9ddd3bd9044
ms.sourcegitcommit: 611af6ff7a2412abad80c0c7d4decfc0c3a0e8c8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/17/2019
ms.locfileid: "68293808"
---
# <a name="displaying-azure-spatial-anchor-feedback"></a><span data-ttu-id="5db5e-104">Affichage des commentaires sur l’ancrage spatial Azure</span><span class="sxs-lookup"><span data-stu-id="5db5e-104">Displaying Azure Spatial Anchor Feedback</span></span>

<span data-ttu-id="5db5e-105">Dans cette leçon, vous allez apprendre à fournir aux utilisateurs des commentaires sur la détection d’ancrage, les événements et l’état lors de l’utilisation d’ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="5db5e-105">In this lesson, you'll learn about how to provide users with feedback about anchor discovery, events, and status when using Azure Spatial Anchors.</span></span>

<span data-ttu-id="5db5e-106">Cherché</span><span class="sxs-lookup"><span data-stu-id="5db5e-106">Objectives:</span></span>

* <span data-ttu-id="5db5e-107">Découvrez comment configurer un panneau d’interface utilisateur qui affiche des informations importantes sur la session ASA actuelle.</span><span class="sxs-lookup"><span data-stu-id="5db5e-107">Learn how to set up a UI panel that displays important information about the current ASA session</span></span>

* <span data-ttu-id="5db5e-108">Comprendre et explorer les éléments de commentaires que le kit de développement logiciel (SDK) ASA met à la disposition des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="5db5e-108">Understand and explore feedback elements that the ASA SDK makes available to users</span></span>

## <a name="instructions"></a><span data-ttu-id="5db5e-109">Instructions</span><span class="sxs-lookup"><span data-stu-id="5db5e-109">Instructions</span></span>

### <a name="set-up-asa-feedback-ui-panel"></a><span data-ttu-id="5db5e-110">Panneau de l’interface utilisateur de configuration des commentaires ASA</span><span class="sxs-lookup"><span data-stu-id="5db5e-110">Set Up ASA Feedback UI Panel</span></span>

1. <span data-ttu-id="5db5e-111">Dans cette leçon, nous n’utilisons pas les boutons «SaveAnchorToDisk» et «ShareAnchor». pour ce faire, sélectionnez les deux boutons et désactivez la case à cocher dans le panneau inspecteur (comme indiqué ci-dessous) pour masquer ces boutons.</span><span class="sxs-lookup"><span data-stu-id="5db5e-111">In this lesson, we are not using the "SaveAnchorToDisk" and "ShareAnchor" buttons so select both buttons and uncheck the checkbox in the inspector panel (as shown below) to hide these buttons.</span></span>
   

![module2chapter3step1im](images/module2chapter3step1im.PNG)

2. <span data-ttu-id="5db5e-113">Ensuite, créez le panneau d’instructions.</span><span class="sxs-lookup"><span data-stu-id="5db5e-113">Next, create the instruction panel.</span></span> <span data-ttu-id="5db5e-114">Commencez par cliquer avec le bouton droit sur le bouton «instructions», pointez sur «objet 3D», puis sélectionnez «textmeshpro-Text».</span><span class="sxs-lookup"><span data-stu-id="5db5e-114">Start by right clicking the "instructions" button, hover over "3D Object" and select "textmeshpro-text."</span></span>

![module2chapter3step2im](images/module2chapter3step2im.PNG)

3. <span data-ttu-id="5db5e-116">Ajustez l’échelle et le positionnement du texte afin qu’il corresponde aux instructions de votre scène.</span><span class="sxs-lookup"><span data-stu-id="5db5e-116">Adjust the scale and the positioning of the text so that it matches with the instructions in your scene.</span></span> <span data-ttu-id="5db5e-117">En outre, assurez-vous que l’alignement de tout le texte est centré.</span><span class="sxs-lookup"><span data-stu-id="5db5e-117">Also, ensure the alignment for all of the text is centered.</span></span> <span data-ttu-id="5db5e-118">Ensuite, supprimez l’exemple de texte de l’éditeur de texte, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5db5e-118">Then delete the sample text from the text editor, as shown in in the image below.</span></span>

![module2chapter3step3im](images/module2chapter3step3im.PNG)

4. <span data-ttu-id="5db5e-120">Remplacez le nom de l’objet TextMeshPro par «FeedbackPanel».</span><span class="sxs-lookup"><span data-stu-id="5db5e-120">Change the name of the TextMeshPro object to "FeedbackPanel."</span></span>
   

![module2chapter3step4im](images/module2chapter3step4im.PNG)

5. <span data-ttu-id="5db5e-122">Dans le panneau projet, sélectionnez «ressources», cliquez avec le bouton droit, puis sélectionnez «Afficher dans l’Explorateur».</span><span class="sxs-lookup"><span data-stu-id="5db5e-122">In the project panel, select "assets" and right click, then select "show in explorer."</span></span>
   

![module2chapter3step4im](images/module2chapter3step5im.PNG)

<span data-ttu-id="5db5e-124">Cliquez [ici](https://onedrive.live.com/?authkey=%21ABXEC8PvyQu8Qd8&id=5B7335C4342BCB0E%21395636&cid=5B7335C4342BCB0E) pour télécharger les fichiers nécessaires dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="5db5e-124">Now, click [here](https://onedrive.live.com/?authkey=%21ABXEC8PvyQu8Qd8&id=5B7335C4342BCB0E%21395636&cid=5B7335C4342BCB0E) to download the files needed in the next few steps.</span></span>

6. <span data-ttu-id="5db5e-125">Une fois que l’Explorateur s’ouvre, sélectionnez le dossier ressources, puis le dossier «ASAmodulesAssets» et copiez le script de commentaires d’ancrage et les fichiers de script du module d’ancrage dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="5db5e-125">Once explorer opens, select the assets folder, then the "ASAmodulesAssets" folder, and copy the anchor feedback script and the anchor module script files into the folder.</span></span> 

![module2chapter3step5im](images/module2chapter3step6im.PNG)

> <span data-ttu-id="5db5e-127">Remarque: Si vous recevez un message vous demandant si vous souhaitez remplacer l’ancien ou conserver l’ancien, veillez à sélectionner remplacer.</span><span class="sxs-lookup"><span data-stu-id="5db5e-127">note: if you get a pop-up asking you if you would like to overwrite the old or keep the old make sure you select overwrite.</span></span>

7. <span data-ttu-id="5db5e-128">Revenez à présent au dossier Assets.</span><span class="sxs-lookup"><span data-stu-id="5db5e-128">Now return to the Assets folder.</span></span> <span data-ttu-id="5db5e-129">Ensuite, accédez au dossier «AzureSpatialAnchorsPlugin», puis au dossier exemples et enfin au dossier scripts, et copiez le wrapper de démonstration des ancres spatiales Azure dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="5db5e-129">Then, go into the "AzureSpatialAnchorsPlugin" folder, then the examples folder, and finally the scripts folder, and copy the Azure Spatial Anchors demo wrapper into that folder.</span></span> 

![module2chapter3step8im](images/module2chapter3step7im.PNG)

8. <span data-ttu-id="5db5e-131">Maintenant que les fichiers sont téléchargés, assurez-vous que le texte «feedbackpanel» est sélectionné, dans la hiérarchie ASA_feedback et cliquez sur «Ajouter un composant», puis ajoutez le script de commentaires d’ancrage en le recherchant et en le sélectionnant une fois qu’il apparaît.</span><span class="sxs-lookup"><span data-stu-id="5db5e-131">Now that the files are uploaded, ensure that the "feedbackpanel" text is selected, in the ASA_feedback hierarchy and click "add component" and add the anchor feedback script by searching for it and selecting it once it appears.</span></span> 

![module2chapter3step8im](images/module2chapter3step8im.PNG)

9. <span data-ttu-id="5db5e-133">Faites glisser l’objet de texte «feedbackPanel» de la hiérarchie ASA_Feedback vers l’emplacement vide sous le script, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5db5e-133">Drag the "feedbackPanel" text object from the ASA_Feedback hierarchy into the empty slot beneath the script as seen in the picture below.</span></span> 

![module2chapter3step9im](images/module2chapter3step9im.PNG)

## <a name="congratulations"></a><span data-ttu-id="5db5e-135">Félicitations</span><span class="sxs-lookup"><span data-stu-id="5db5e-135">Congratulations</span></span>

<span data-ttu-id="5db5e-136">Dans cette leçon, nous avons appris à créer un panneau d’interface utilisateur pour afficher l’état actuel de l’expérience d’ancrage spatial Azure pour fournir à l’utilisateur des commentaires en temps réel.</span><span class="sxs-lookup"><span data-stu-id="5db5e-136">In this lesson we learned how to create a UI panel to display the current status of the Azure Spatial Anchor experience for providing user with real-time feedback.</span></span>


