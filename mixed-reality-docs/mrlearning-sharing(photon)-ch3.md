---
title: Didacticiels sur les fonctionnalités multi-utilisateur-3. Connexion de plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 9441cf7a9685b8a197bab1116202db4a9b026f2e
ms.sourcegitcommit: 23b130d03fea46a50a712b8301fe4e5deed6cf9c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2019
ms.locfileid: "75334299"
---
# <a name="3-connecting-multiple-users"></a>3. connexion de plusieurs utilisateurs

Dans cette leçon, nous allons apprendre à connecter plusieurs utilisateurs dans le cadre d’une expérience partagée en direct. À la fin de cette leçon, vous serez en mesure d’ouvrir l’application sur plusieurs appareils et de voir l’avatar, représenté par une sphère pour chaque personne qui rejoint.

## <a name="objectives"></a>Objectifs

* Configurer retentissante dans votre application
* Configurer les joueurs
* Découvrez comment connecter plusieurs utilisateurs dans un environnement partagé

## <a name="instructions"></a>Instructions

1. Dans le dossier Ressources-> Ressources-> Prefabs du panneau projet, glissez-déposez le Prefab NetworkLobby dans la hiérarchie, comme indiqué dans l’image ci-dessous.

    ![Module3Chapter3step1im](images/module3chapter3step1im.PNG)

2. Lorsque vous développez NetworkLobby, vous voyez un objet enfant appelé NetworkRoom. Avec NetworkRoom sélectionné, accédez au panneau de l’inspecteur, puis cliquez sur Ajouter un composant. Recherchez PhotonView et ajoutez le composant.

    ![Module3Chapter3tep2im](images/module3chapter3step2im.PNG)

3. Créez un nouvel objet de jeu vide dans la hiérarchie. Cliquez avec le bouton droit dans la hiérarchie et sélectionnez vide dans le menu contextuel. Assurez-vous que le positionnement est défini sur x = 0, y = 0, z = 0 et nommez l’objet, PhotonUser.

    ![Module3Chapter3step3im](images/module3chapter3step3im.PNG)

4. Cliquez sur Ajouter un composant et tapez Generic net Sync. Sélectionnez la classe Generic net Sync. Lorsque la classe s’affiche, cliquez sur la case à cocher utilisateur pour l’activer.

    ![module3chapter3updateStep4im](images/module3chapter3updateStep4im.png)

5. Cliquez à nouveau sur Ajouter un composant, puis tapez vue photon. Sélectionnez la classe de vue photons qui apparaît dans la liste déroulante.

    ![module3chapter3updateStep5im](images/module3chapter3updateStep5im.png)

6. Cliquez sur l’icône de fichier de la classe Generic net Sync. Faites-le glisser et déposez-le dans le champ composants observés de la vue photons.

    ![module3chapter3updateStep6im. png](images/module3chapter3updateStep6im.png)

7. Ensuite, nous créons des sphères pour représenter chaque personne qui rejoint une expérience partagée. Cliquez avec le bouton droit sur l’objet PhotonUser que vous venez de créer, faites défiler jusqu’à «objet 3D et cliquez sur sphère. Cela permet de créer un objet de jeu Sphere en tant qu’enfant de l’objet PhotonUser.

    ![Module3Chapter3step4im](images/module3chapter3step4im.PNG)

8. Mettez à l’échelle la sphère jusqu’à x = 0.06, y = 0.06, ad z = 0.06.

    ![Module3hapter3step5im](images/module3chapter3step5im.PNG)

9. Faites glisser l’objet de jeu PhotonUser dans le dossier Prefabs du panneau projet, puis supprimez-le de la scène. Vous avez maintenant créé un Prefab qui peut être utilisé lors de la génération ou de l’instanciation de nouveaux joueurs dans un environnement partagé.

    ![Module3Chapter3step6im](images/module3chapter3step6im.PNG)

    >[!NOTE]
    >Assurez-vous que l’objet de jeu a été copié dans le dossier Prefabs avant de le supprimer de votre hiérarchie.

10. Créez un nouvel objet dans la hiérarchie en suivant les instructions de l’étape 3 et nommez-le SharedPlayground. Ensuite, cliquez sur Ajouter un composant et recherchez gestionnaire de réseau générique.  Cliquez à nouveau dessus pour ajouter le composant Generic Network Manager. Remplacez la position de l’objet par x = 0, y = 0 et z = 0.

    ![Module3Chapter3step7im](images/module3chapter3step7im.PNG)

## <a name="congratulations"></a>Félicitations !

Une fois que toutes les étapes ci-dessus sont terminées et que le processus de génération est également terminé, appuyez sur le bouton de lecture et connectez votre HoloLens 2. Vous devriez voir une sphère se déplaçant au fur et à mesure que vous déplacez votre tête. Celui-ci s’affiche pour tout utilisateur qui rejoint votre projet Unity.

[Leçon suivante : 4. partage des mouvements d’objets avec plusieurs utilisateurs](mrlearning-sharing(photon)-ch4.md)
