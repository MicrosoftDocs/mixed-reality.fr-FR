---
title: Tutoriels sur les fonctionnalités multiutilisateurs - 3. Connexion de plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multiutilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: cbe0d8d2db6c34ba262fe9c946b68366ed3dbb93
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79031229"
---
# <a name="3-connecting-multiple-users"></a>3. Connexion de plusieurs utilisateurs

Dans cette leçon, nous allons apprendre à connecter plusieurs utilisateurs dans le cadre d’une expérience partagée en direct. À la fin de cette leçon, vous pourrez ouvrir l’application sur plusieurs appareils et voir l’avatar, représenté par une sphère, de chaque personne rejoignant l’expérience.

## <a name="objectives"></a>Objectifs

* Configurer PUN dans votre application
* Configurer des joueurs
* Découvrir comment connecter plusieurs utilisateurs dans un environnement partagé

## <a name="instructions"></a>Instructions

1. Dans le dossier Assets > Resources > Prefabs du panneau Project, faites glisser-déposer le préfabriqué NetworkLobby dans la hiérarchie, comme illustré dans l’image ci-dessous.

    ![Module3Chapter3step1im](images/module3chapter3step1im.PNG)

2. Quand vous développez NetworkLobby, vous voyez un objet enfant appelé NetworkRoom. NetworkRoom étant sélectionné, accédez au panneau Inspector, puis cliquez sur Add Component. Recherchez PhotonView et ajoutez le composant.

    ![Module3Chapter3tep2im](images/module3chapter3step2im.PNG)

3. Créez un objet de jeu vide dans la hiérarchie. Cliquez avec le bouton droit dans la hiérarchie et sélectionnez Empty dans le menu contextuel. Vérifiez que le positionnement est défini avec les valeurs x=0, y=0 et z=0, puis nommez l’objet PhotonUser.

    ![Module3Chapter3step3im](images/module3chapter3step3im.PNG)

4. Cliquez sur Add Component et tapez Generic Net Sync. Sélectionnez la classe Generic Net Sync. Quand la classe s’affiche, cochez la case User pour l’activer.

    ![module3chapter3updateStep4im](images/module3chapter3updateStep4im.png)

5. Cliquez à nouveau sur Add Component, puis tapez Photon View. Sélectionnez la classe Photon View qui apparaît dans la liste déroulante.

    ![module3chapter3updateStep5im](images/module3chapter3updateStep5im.png)

6. Cliquez sur l’icône File de la classe Generic Net Sync. Faites-le glisser-déposer dans le champ Observed Components de Photon View.

    ![module3chapter3updateStep6im.png](images/module3chapter3updateStep6im.png)

7. Nous allons à présent créer des sphères pour représenter chaque personne rejoignant une expérience partagée. Cliquez avec le bouton droit sur l’objet PhotonUser que vous venez de créer, faites défiler jusqu’à 3D Object et cliquez sur Sphere. Un objet de jeu Sphere est créé en tant qu’enfant de l’objet PhotonUser.

    ![Module3Chapter3step4im](images/module3chapter3step4im.PNG)

8. Mettez à l’échelle la sphère avec les valeurs x=0,06, y=0,06 et z=0,06.

    ![Module3hapter3step5im](images/module3chapter3step5im.PNG)

9. Faites glisser l’objet de jeu PhotonUser dans le dossier Prefabs du panneau Project, puis supprimez-le de la scène. Vous disposez maintenant d’un élément fabriqué que vous pouvez utiliser lors de la génération ou de l’instanciation de nouveaux joueurs dans une expérience partagée.

    ![Module3Chapter3step6im](images/module3chapter3step6im.PNG)

    >[!NOTE]
    >Vérifiez que l’objet de jeu a bien été copié dans le dossier Prefabs avant de le supprimer de votre hiérarchie.

10. Créez un objet dans la hiérarchie en suivant les instructions de l’étape 3 et nommez-le SharedPlayground. Ensuite, cliquez sur Add Component et recherchez Generic Network Manager.  Cliquez à nouveau dessus pour ajouter le composant Generic Network Manager. Définissez la position de l’objet avec les valeurs x=0, y=0 et z=0.

    ![Module3Chapter3step7im](images/module3chapter3step7im.PNG)

## <a name="congratulations"></a>Félicitations

Au terme des étapes ci-dessus et du processus de génération, appuyez sur le bouton de lecture et connectez votre HoloLens 2. Vous devriez voir une sphère qui se déplace à mesure que vous bougez la tête. Tout utilisateur qui rejoint votre projet Unity peut la voir.

[Leçon suivante : 4. Partage de mouvements d’objet avec plusieurs utilisateurs](mrlearning-sharing(photon)-ch4.md)
