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
# <a name="displaying-azure-spatial-anchor-feedback"></a>Affichage des commentaires sur l’ancrage spatial Azure

Dans cette leçon, vous allez apprendre à fournir aux utilisateurs des commentaires sur la détection d’ancrage, les événements et l’état lors de l’utilisation d’ancres spatiales Azure.

Cherché

* Découvrez comment configurer un panneau d’interface utilisateur qui affiche des informations importantes sur la session ASA actuelle.

* Comprendre et explorer les éléments de commentaires que le kit de développement logiciel (SDK) ASA met à la disposition des utilisateurs

## <a name="instructions"></a>Instructions

### <a name="set-up-asa-feedback-ui-panel"></a>Panneau de l’interface utilisateur de configuration des commentaires ASA

1. Dans cette leçon, nous n’utilisons pas les boutons «SaveAnchorToDisk» et «ShareAnchor». pour ce faire, sélectionnez les deux boutons et désactivez la case à cocher dans le panneau inspecteur (comme indiqué ci-dessous) pour masquer ces boutons.
   

![module2chapter3step1im](images/module2chapter3step1im.PNG)

2. Ensuite, créez le panneau d’instructions. Commencez par cliquer avec le bouton droit sur le bouton «instructions», pointez sur «objet 3D», puis sélectionnez «textmeshpro-Text».

![module2chapter3step2im](images/module2chapter3step2im.PNG)

3. Ajustez l’échelle et le positionnement du texte afin qu’il corresponde aux instructions de votre scène. En outre, assurez-vous que l’alignement de tout le texte est centré. Ensuite, supprimez l’exemple de texte de l’éditeur de texte, comme indiqué dans l’image ci-dessous.

![module2chapter3step3im](images/module2chapter3step3im.PNG)

4. Remplacez le nom de l’objet TextMeshPro par «FeedbackPanel».
   

![module2chapter3step4im](images/module2chapter3step4im.PNG)

5. Dans le panneau projet, sélectionnez «ressources», cliquez avec le bouton droit, puis sélectionnez «Afficher dans l’Explorateur».
   

![module2chapter3step4im](images/module2chapter3step5im.PNG)

Cliquez [ici](https://onedrive.live.com/?authkey=%21ABXEC8PvyQu8Qd8&id=5B7335C4342BCB0E%21395636&cid=5B7335C4342BCB0E) pour télécharger les fichiers nécessaires dans les étapes suivantes.

6. Une fois que l’Explorateur s’ouvre, sélectionnez le dossier ressources, puis le dossier «ASAmodulesAssets» et copiez le script de commentaires d’ancrage et les fichiers de script du module d’ancrage dans le dossier. 

![module2chapter3step5im](images/module2chapter3step6im.PNG)

> Remarque: Si vous recevez un message vous demandant si vous souhaitez remplacer l’ancien ou conserver l’ancien, veillez à sélectionner remplacer.

7. Revenez à présent au dossier Assets. Ensuite, accédez au dossier «AzureSpatialAnchorsPlugin», puis au dossier exemples et enfin au dossier scripts, et copiez le wrapper de démonstration des ancres spatiales Azure dans ce dossier. 

![module2chapter3step8im](images/module2chapter3step7im.PNG)

8. Maintenant que les fichiers sont téléchargés, assurez-vous que le texte «feedbackpanel» est sélectionné, dans la hiérarchie ASA_feedback et cliquez sur «Ajouter un composant», puis ajoutez le script de commentaires d’ancrage en le recherchant et en le sélectionnant une fois qu’il apparaît. 

![module2chapter3step8im](images/module2chapter3step8im.PNG)

9. Faites glisser l’objet de texte «feedbackPanel» de la hiérarchie ASA_Feedback vers l’emplacement vide sous le script, comme indiqué dans l’image ci-dessous. 

![module2chapter3step9im](images/module2chapter3step9im.PNG)

## <a name="congratulations"></a>Félicitations

Dans cette leçon, nous avons appris à créer un panneau d’interface utilisateur pour afficher l’état actuel de l’expérience d’ancrage spatial Azure pour fournir à l’utilisateur des commentaires en temps réel.


