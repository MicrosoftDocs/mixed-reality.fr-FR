---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 44cc41b10ed79d3085ec601ec9cf21af47b0fea5
ms.sourcegitcommit: cf9f8ebbca0301e9d277853771ff6e47701ba1c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67523305"
---
# <a name="connecting-multiple-users"></a>Plusieurs utilisateurs qui se connectent

Dans cette leçon, nous Découvrez comment connecter plusieurs utilisateurs dans le cadre de l’expérience partagée en direct. À la fin de cette leçon, vous serez en mesure d’ouvrir l’application sur plusieurs appareils et consultez avatar, représenté par une sphère, les représentations sous forme de chaque personne qui joint. 

Objectifs :

- Configurer le jeu de mots dans votre application
- Configurer des joueurs
- Découvrez comment vous connecter à plusieurs utilisateurs dans une expérience partagée

### <a name="instructions"></a>Instructions

1. Dans les ressources -> ressources -> dossier Prefabs dans le panneau de configuration de projet, faites glisser le préfabriqué NetworkLobby dans à la hiérarchie comme indiqué dans l’image ci-dessous.


   ![Module3Chapter3step1im](images/module3chapter3step1im.PNG)

2. Lorsque vous développez NetworkLobby, vous verrez un objet enfant appelé NetworkRoom. Avec NetworkRoom sélectionné, accédez au volet d’inspecteur, puis cliquez sur Ajouter un composant. Recherchez PhotonView et ajouter le composant.

   ![Module3Chapter3tep2im](images/module3chapter3step2im.PNG)

3. Créer un nouvel objet de jeu vide dans la hiérarchie. Cliquez avec le bouton droit dans la hiérarchie, puis sélectionnez vide dans le menu contextuel. Vérifiez le positionnement est défini sur x = 0, y = 0, z = 0 et nommer l’objet, PhotonUser.

   ![Module3Chapter3step3im](images/module3chapter3step3im.PNG)

4. Cliquez sur Ajouter un composant, puis tapez synchronisation Net générique. Sélectionnez la classe générique synchronisation Net. Lorsque la classe s’affiche, cliquez sur la case à cocher pour l’activer. 

   ![module3chapter3updateStep4im](images/module3chapter3updateStep4im.png)

5. Cliquez sur Ajouter un composant à nouveau et tapez Photon View. Sélectionnez la classe d’affichage de Photon qui s’affiche dans la liste déroulante.

   ![module3chapter3updateStep5im](images/module3chapter3updateStep5im.png)

6. Cliquez sur l’icône de fichier pour la classe générique synchronisation Net. Faites glisser dans le champ d’observé les composants de la vue Photon. ![module3chapter3updateStep6im.png](images/module3chapter3updateStep6im.png) 

7. Ensuite, nous créer sphères pour représenter chaque personne qui rejoint une expérience partagée. Avec le bouton droit sur l’objet de PhotonUser que vous venez de créer et scrolldown à « sphère objet 3D, puis cliquez sur. Cela créera un objet de jeu sphère en tant qu’enfant de l’objet PhotonUser.

   ![Module3Chapter3step4im](images/module3chapter3step4im.PNG)

8. Mettre à l’échelle de la sphère à x = 0,06, y = 0,06, ad z = 0,06.

   ![Module3hapter3step5im](images/module3chapter3step5im.PNG)

9. Faites glisser l’objet de jeu PhotonUser dans le dossier Prefabs dans le panneau de configuration de projet, puis supprimez-le de la scène. Nous avons maintenant créé un préfabriqué qui peut être utilisé lors de la génération dynamique ou instanciation de nouveaux lecteurs dans un environnement partagé.

   ![Module3Chapter3step6im](images/module3chapter3step6im.PNG)

> Remarque : Assurez-vous que l’objet de jeu a correctement copié dans le dossier Prefabs avant de le supprimer à partir de votre hiérarchie.

10. Créer un nouvel objet dans la hiérarchie en suivant les instructions à l’étape 3 et nommez-le SharedPlayground. Ensuite, cliquez sur Ajouter un composant, recherchez le Gestionnaire de réseau générique et cliquez dessus pour ajouter le composant Gestionnaire de réseau générique. Modifier la position de l’objet à x = 0, y = 0 et z = 0.

    ![Module3Chapter3step7im](images/module3chapter3step7im.PNG)


## <a name="congratulations"></a>Félicitations

Une fois toutes les étapes ci-dessus sont terminées, et le processus de génération est également terminé, appuyez sur le bouton de lecture et connecter votre 2 HoloLens. Vous devez voir une sphère déplaçant à mesure que vous déplacez votre tête. Elle sera visible pour tous les utilisateurs qui se joint à votre projet Unity !

[Leçon suivante : Sharing(Photon) leçon 4](mrlearning-sharing(photon)-ch4.md)

