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
# <a name="displaying-azure-spatial-anchor-feedback"></a>Affichage des commentaires d’ancrage Spatial Azure

Dans cette leçon, vous allez découvrir comment fournir aux utilisateurs avec des commentaires sur la découverte de point d’ancrage, événements et l’état lors de l’utilisation des ancres spatiale d’Azure.

Objectifs :

* Découvrez comment configurer un panneau de l’interface utilisateur qui affiche des informations importantes sur la session active de ASA

* Comprendre et Explorer les éléments de commentaires qui le SDK ASA rend disponible pour les utilisateurs

  

## <a name="instructions"></a>Instructions

### <a name="set-up-asa-feedback-ui-panel"></a>Configurer le volet de l’interface utilisateur de commentaires ASA

1. Dans cette leçon, nous n’utilisons pas le « SaveAnchorToDisk » et les boutons « ShareAnchor », par conséquent, sélectionnez les deux boutons et décochez la case à cocher dans le panneau Inspecteur (comme indiqué ci-dessous) pour masquer ces boutons.
   

![module2chapter3step1im](images/module2chapter3step1im.PNG)

2. Ensuite, créez le panneau d’instructions. Démarrez en cliquant avec le bouton avec le bouton droit sur le bouton « instructions », placez le curseur sur le « objet 3D » et sélectionnez « textmeshpro-texte ».

   

   ![module2chapter3step2im](images/module2chapter3step2im.PNG)

   3. Ajuster l’échelle et le positionnement du texte afin qu’elle corresponde avec les instructions de votre scène. En outre, vérifiez que l’alignement pour tout le texte est centré. Puis supprimez le texte d’exemple à partir de l’éditeur de texte, comme illustré dans l’image ci-dessous.


![module2chapter3step3im](images/module2chapter3step3im.PNG)

4. Remplacez le nom de l’objet TextMeshPro « FeedbackPanel ».
   
   ![module2chapter3step4im](images/module2chapter3step4im.PNG)
   
5. Dans le volet de projet, sélectionnez « actifs » et avec le bouton droit, puis sur « Afficher dans l’Explorateur de ».
   

![module2chapter3step4im](images/module2chapter3step5im.PNG)

Maintenant, cliquez sur [ici](https://onedrive.live.com/?authkey=%21ABXEC8PvyQu8Qd8&id=5B7335C4342BCB0E%21395636&cid=5B7335C4342BCB0E) pour télécharger les fichiers nécessaires dans les prochains quelques étapes.

6. Une fois que l’Explorateur s’ouvre, sélectionnez le dossier assets, puis le dossier « ASAmodulesAssets » et copiez le script de commentaires d’ancrage et les fichiers de script de module d’ancrage dans le dossier. 
   

![module2chapter3step5im](images/module2chapter3step6im.PNG)

> Remarque : Si vous obtenez une fenêtre contextuelle vous demandant si vous souhaitez remplacer l’ancien ou de conserver l’ancien veillez à sélectionner le remplacement.

7. Revenez dans le dossier de ressources. Ensuite, accédez dans le dossier « AzureSpatialAnchorsPlugin », puis le dossier d’exemples et enfin le dossier scripts et copiez le wrapper de démonstration ancres Spatial Azure dans ce dossier. 
   

![module2chapter3step8im](images/module2chapter3step7im.PNG)

8. Maintenant que les fichiers sont chargés, vérifiez que le texte « feedbackpanel » est sélectionné, dans la hiérarchie ASA_feedback et cliquez sur « Ajouter un composant » et ajouter le script de commentaires d’ancrage en recherchant et en le sélectionnant qu’il apparaît. 
   
   

![module2chapter3step8im](images/module2chapter3step8im.PNG)

9. Faites glisser l’objet de texte « feedbackPanel » à partir de la hiérarchie ASA_Feedback dans l’emplacement vide sous le script comme indiqué dans l’image ci-dessous. 
   

![module2chapter3step9im](images/module2chapter3step9im.PNG)

   

## <a name="congratulations"></a>Félicitations

Dans cette leçon, nous avons appris à créer un panneau de l’interface utilisateur pour afficher l’état actuel de l’expérience d’ancrage Spatial Azure pour fournir l’utilisateur avec des commentaires en temps réel.


