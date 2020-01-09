---
title: Didacticiels sur les ancres spatiales Azure-3. Affichage des commentaires sur l’ancrage spatial Azure
description: Suivez ce cours pour découvrir comment implémenter Reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 19529cbfebd74938395545c329097d42b5af9ff9
ms.sourcegitcommit: 23b130d03fea46a50a712b8301fe4e5deed6cf9c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2019
ms.locfileid: "75334408"
---
# <a name="3-displaying-azure-spatial-anchor-feedback"></a>3. affichage des commentaires sur l’ancrage spatial Azure

Dans cette leçon, vous allez apprendre à fournir aux utilisateurs des commentaires sur la découverte d’ancrage, les événements et l’état lors de l’utilisation d’ancres spatiales Azure.

## <a name="objectives"></a>Objectifs

* Découvrez comment configurer un panneau d’interface utilisateur qui affiche des informations importantes sur la session ASA actuelle.

* Comprendre et explorer les éléments de commentaires que le kit de développement logiciel (SDK) ASA met à la disposition des utilisateurs

## <a name="set-up-asa-feedback-ui-panel"></a>Panneau de l’interface utilisateur de configuration des commentaires ASA

1. Dans cette leçon, nous n’utilisons pas les boutons « SaveAnchorToDisk » et « ShareAnchor », donc sélectionnez les deux boutons et désactivez la case à cocher dans le panneau inspecteur (comme indiqué ci-dessous) pour masquer ces boutons.

    ![module2chapter3step1im](images/module2chapter3step1im.PNG)

2. Créez le panneau d’instructions. Commencez par cliquer avec le bouton droit sur le bouton « instructions », pointez sur « objet 3D », puis sélectionnez « textmeshpro-Text ».

    ![module2chapter3step2im](images/module2chapter3step2im.PNG)

3. Ajustez l’échelle et le positionnement du texte afin qu’il corresponde aux instructions de votre scène. En outre, assurez-vous que l’alignement de tout le texte est centré. Ensuite, supprimez l’exemple de texte de l’éditeur de texte, comme indiqué dans l’image ci-dessous.

    ![module2chapter3step3im](images/module2chapter3step3im.PNG)

4. Remplacez le nom de l’objet TextMeshPro par « FeedbackPanel ».

    ![module2chapter3step4im](images/module2chapter3step4im.PNG)

5. Assurez-vous que le texte « feedbackpanel » est sélectionné dans la hiérarchie ASA_feedback, cliquez sur « Ajouter un composant » et ajoutez le script d’ancrage de commentaires en le recherchant et en le sélectionnant une fois qu’il apparaît.

    ![module2chapter3step8im](images/module2chapter3step8im.PNG)

6. Faites glisser l’objet de texte « feedbackPanel » de la hiérarchie ASA_Feedback vers l’emplacement vide sous le script, comme indiqué dans l’image ci-dessous.

    ![module2chapter3step9im](images/module2chapter3step9im.PNG)

## <a name="congratulations"></a>Félicitations !

Dans cette leçon, nous avons appris à créer un panneau d’interface utilisateur pour afficher l’état actuel de l’expérience d’ancrage spatial Azure pour fournir aux utilisateurs des commentaires en temps réel.
