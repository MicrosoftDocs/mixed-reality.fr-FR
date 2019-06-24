---
title: Module MR Learning ASA Azure spatiale de point d’ancrage sur HoloLens 2
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 4aabb4a35efebdd893cbb248365e534abd60f684
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67327094"
---
# <a name="displaying-azure-spatial-anchor-feedback"></a><span data-ttu-id="d5740-104">Affichage des commentaires d’ancrage Spatial Azure</span><span class="sxs-lookup"><span data-stu-id="d5740-104">Displaying Azure Spatial Anchor Feedback</span></span>

<span data-ttu-id="d5740-105">Dans cette leçon, vous allez découvrir comment fournir aux utilisateurs avec des commentaires sur la découverte de point d’ancrage, événements et l’état lors de l’utilisation des ancres spatiale d’Azure.</span><span class="sxs-lookup"><span data-stu-id="d5740-105">In this lesson, you'll learn about how to provide users with feedback about anchor discovery, events, and status when using Azure Spatial Anchors.</span></span>

<span data-ttu-id="d5740-106">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="d5740-106">Objectives:</span></span>

* <span data-ttu-id="d5740-107">Découvrez comment configurer un panneau de l’interface utilisateur qui affiche des informations importantes sur la session active de ASA</span><span class="sxs-lookup"><span data-stu-id="d5740-107">Learn how to set up a UI panel that displays important information about the current ASA session</span></span>

* <span data-ttu-id="d5740-108">Comprendre et Explorer les éléments de commentaires qui le SDK ASA rend disponible pour les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="d5740-108">Understand and explore feedback elements that the ASA SDK makes available to users</span></span>

  

## <a name="instructions"></a><span data-ttu-id="d5740-109">Instructions</span><span class="sxs-lookup"><span data-stu-id="d5740-109">Instructions</span></span>

### <a name="set-up-asa-feedback-ui-panel"></a><span data-ttu-id="d5740-110">Configurer le volet de l’interface utilisateur de commentaires ASA</span><span class="sxs-lookup"><span data-stu-id="d5740-110">Set Up ASA Feedback UI Panel</span></span>

1. <span data-ttu-id="d5740-111">Dans cette leçon, nous n’utilisons pas le « SaveAnchorToDisk » et les boutons « ShareAnchor », par conséquent, sélectionnez les deux boutons et décochez la case à cocher dans le panneau Inspecteur (comme indiqué ci-dessous) pour masquer ces boutons.</span><span class="sxs-lookup"><span data-stu-id="d5740-111">In this lesson, we are not using the "SaveAnchorToDisk" and "ShareAnchor" buttons so select both buttons and uncheck the checkbox in the inspector panel (as shown below) to hide these buttons.</span></span>
   

![module2chapter3step1im](images/module2chapter3step1im.PNG)

2. <span data-ttu-id="d5740-113">Ensuite, créez le panneau d’instructions.</span><span class="sxs-lookup"><span data-stu-id="d5740-113">Next, create the instruction panel.</span></span> <span data-ttu-id="d5740-114">Démarrez en cliquant avec le bouton avec le bouton droit sur le bouton « instructions », placez le curseur sur le « objet 3D » et sélectionnez « textmeshpro-texte ».</span><span class="sxs-lookup"><span data-stu-id="d5740-114">Start by right clicking the "instructions" button, hover over "3D Object" and select "textmeshpro-text."</span></span>

   

   ![module2chapter3step2im](images/module2chapter3step2im.PNG)

   3. <span data-ttu-id="d5740-116">Ajuster l’échelle et le positionnement du texte afin qu’elle corresponde avec les instructions de votre scène.</span><span class="sxs-lookup"><span data-stu-id="d5740-116">Adjust the scale and the positioning of the text so that it matches with the instructions in your scene.</span></span> <span data-ttu-id="d5740-117">En outre, vérifiez que l’alignement pour tout le texte est centré.</span><span class="sxs-lookup"><span data-stu-id="d5740-117">Also, ensure the alignment for all of the text is centered.</span></span> <span data-ttu-id="d5740-118">Puis supprimez le texte d’exemple à partir de l’éditeur de texte, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d5740-118">Then delete the sample text from the text editor, as shown in in the image below.</span></span>


![module2chapter3step3im](images/module2chapter3step3im.PNG)

4. <span data-ttu-id="d5740-120">Remplacez le nom de l’objet TextMeshPro « FeedbackPanel ».</span><span class="sxs-lookup"><span data-stu-id="d5740-120">Change the name of the TextMeshPro object to "FeedbackPanel."</span></span>
   
   ![module2chapter3step4im](images/module2chapter3step4im.PNG)
   
5. <span data-ttu-id="d5740-122">Dans le volet de projet, sélectionnez « actifs » et avec le bouton droit, puis sur « Afficher dans l’Explorateur de ».</span><span class="sxs-lookup"><span data-stu-id="d5740-122">In the project panel, select "assets" and right click, then select "show in explorer."</span></span>
   

![module2chapter3step4im](images/module2chapter3step5im.PNG)

<span data-ttu-id="d5740-124">Maintenant, cliquez sur [ici](https://onedrive.live.com/?authkey=%21ABXEC8PvyQu8Qd8&id=5B7335C4342BCB0E%21395636&cid=5B7335C4342BCB0E) pour télécharger les fichiers nécessaires dans les prochains quelques étapes.</span><span class="sxs-lookup"><span data-stu-id="d5740-124">Now, click [here](https://onedrive.live.com/?authkey=%21ABXEC8PvyQu8Qd8&id=5B7335C4342BCB0E%21395636&cid=5B7335C4342BCB0E) to download the files needed in the next few steps.</span></span>

6. <span data-ttu-id="d5740-125">Une fois que l’Explorateur s’ouvre, sélectionnez le dossier assets, puis le dossier « ASAmodulesAssets » et copiez le script de commentaires d’ancrage et les fichiers de script de module d’ancrage dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="d5740-125">Once explorer opens, select the assets folder, then the "ASAmodulesAssets" folder, and copy the anchor feedback script and the anchor module script files into the folder.</span></span> 
   

![module2chapter3step5im](images/module2chapter3step6im.PNG)

> <span data-ttu-id="d5740-127">Remarque : Si vous obtenez une fenêtre contextuelle vous demandant si vous souhaitez remplacer l’ancien ou de conserver l’ancien veillez à sélectionner le remplacement.</span><span class="sxs-lookup"><span data-stu-id="d5740-127">note: if you get a pop-up asking you if you would like to overwrite the old or keep the old make sure you select overwrite.</span></span>

7. <span data-ttu-id="d5740-128">Revenez dans le dossier de ressources.</span><span class="sxs-lookup"><span data-stu-id="d5740-128">Now return to the Assets folder.</span></span> <span data-ttu-id="d5740-129">Ensuite, accédez dans le dossier « AzureSpatialAnchorsPlugin », puis le dossier d’exemples et enfin le dossier scripts et copiez le wrapper de démonstration ancres Spatial Azure dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="d5740-129">Then, go into the "AzureSpatialAnchorsPlugin" folder, then the examples folder, and finally the scripts folder, and copy the Azure Spatial Anchors demo wrapper into that folder.</span></span> 
   

![module2chapter3step8im](images/module2chapter3step7im.PNG)

8. <span data-ttu-id="d5740-131">Maintenant que les fichiers sont chargés, vérifiez que le texte « feedbackpanel » est sélectionné, dans la hiérarchie ASA_feedback et cliquez sur « Ajouter un composant » et ajouter le script de commentaires d’ancrage en recherchant et en le sélectionnant qu’il apparaît.</span><span class="sxs-lookup"><span data-stu-id="d5740-131">Now that the files are uploaded, ensure that the "feedbackpanel" text is selected, in the ASA_feedback hierarchy and click "add component" and add the anchor feedback script by searching for it and selecting it once it appears.</span></span> 
   
   

![module2chapter3step8im](images/module2chapter3step8im.PNG)

9. <span data-ttu-id="d5740-133">Faites glisser l’objet de texte « feedbackPanel » à partir de la hiérarchie ASA_Feedback dans l’emplacement vide sous le script comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d5740-133">Drag the "feedbackPanel" text object from the ASA_Feedback hierarchy into the empty slot beneath the script as seen in the picture below.</span></span> 
   

![module2chapter3step9im](images/module2chapter3step9im.PNG)

   

## <a name="congratulations"></a><span data-ttu-id="d5740-135">Félicitations</span><span class="sxs-lookup"><span data-stu-id="d5740-135">Congratulations</span></span>

<span data-ttu-id="d5740-136">Dans cette leçon, nous avons appris à créer un panneau de l’interface utilisateur pour afficher l’état actuel de l’expérience d’ancrage Spatial Azure pour fournir l’utilisateur avec des commentaires en temps réel.</span><span class="sxs-lookup"><span data-stu-id="d5740-136">In this lesson we learned how to create a UI panel to display the current status of the Azure Spatial Anchor experience for providing user with real-time feedback.</span></span>


