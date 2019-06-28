---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 33f265c6333f12f7ec73ecb0c1e5730b168d4bde
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67415910"
---
# <a name="connecting-multiple-users"></a>**Plusieurs utilisateurs qui se connectent** 

Dans cette leçon, nous allez apprendre à vous connecter de plusieurs utilisateurs dans le cadre de l’expérience partagée en direct. À la fin de cette leçon, vous serez en mesure d’ouvrir l’application sur plusieurs appareils et consultez les représentations sous forme de « avatar » de chaque personne qui joint (avatars représentés par une sphère). 

Objectifs :

- Configurer le jeu de mots dans votre application
- Configurer des joueurs
- Découvrez comment vous connecter à plusieurs utilisateurs dans une expérience partagée

### <a name="instructions"></a>Instructions

1. Dans les ressources > ressources > Prefabs dossier du Panneau de configuration de projet, glisser- déposer le « NetworkLobby » prefab dans à la hiérarchie, comme illustré dans l’image ci-dessous.


   ![Module3Chapter3step1im](images/module3chapter3step1im.PNG)

2. Lorsque vous développez le prefab « NetworkLobby », vous devez voir un objet enfant appelé « NetworkRoom ». Avec qu’elle est sélectionnée, accédez au volet d’inspecteur, puis cliquez sur « Ajouter le composant ». Recherchez « PhotonView » et ajouter le composant.

   ![Module3Chapter3tep2im](images/module3chapter3step2im.PNG)

3. Créer un nouvel objet de jeu vide dans la hiérarchie (cliquez avec le bouton droit dans la hiérarchie et sélectionnez « Vide » dans le menu contextuel). Vérifiez le positionnement est défini sur x = 0, y = 0, z = 0 et nommer l’objet, « PhotonUser ».

   ![Module3Chapter3step3im](images/module3chapter3step3im.PNG)

4. Cliquez sur le bouton « Ajouter un composant » et tapez « Sync Net générique » et sélectionnez la classe générique synchronisation Net. Une fois que la classe s’affiche, cliquez sur la case à cocher « Utilisateur » pour l’activer. 

   ![module3chapter3updateStep4im](images/module3chapter3updateStep4im.png)

5. À nouveau cliquez sur « Ajouter un composant » et tapez « Vue Photon » puis sélectionnez la classe d’affichage de Photon qui s’affiche dans la liste déroulante.

   ![module3chapter3updateStep5im](images/module3chapter3updateStep5im.png)

6. Maintenant cliquez sur l’icône de fichier dans pour la classe générique synchronisation Net, puis faites glisser il au champ de « Composants observées » de la vue Photon. ![module3chapter3updateStep6im.png](images/module3chapter3updateStep6im.png) 

7. Ensuite, nous voulons créer des sphères pour représenter chaque personne qui rejoint une expérience partagée. Cliquez avec le bouton droit sur l’objet « PhotonUser » que vous venez de créer, descend jusqu’aux « objet 3D » et cliquez sur la « Sphère ». Cela créera un objet de jeu sphère en tant qu’enfant de l’objet PhotonUser.

   ![Module3Chapter3step4im](images/module3chapter3step4im.PNG)

8. Mettre à l’échelle de la sphère à x = 0,06, y = 0,06, ad z = 0,06.

   ![Module3hapter3step5im](images/module3chapter3step5im.PNG)

9. Faites glisser l’objet de jeu de « PhotonUser » dans le dossier « prefabs » dans le panneau de configuration de projet. Ensuite, le supprimer à partir de la scène. Nous avons maintenant créé un préfabriqué qui sera utilisé lors de la génération dynamique ou instanciation de nouveaux lecteurs dans un environnement partagé.

   ![Module3Chapter3step6im](images/module3chapter3step6im.PNG)

> Remarque : Assurez-vous que l’objet de jeu a copiée dans le dossier « prefabs » avant de le supprimer à partir de votre hiérarchie.

10. Créez un nouvel objet dans la hiérarchie (à l’aide des instructions similaires à celle de l’étape 3) et nommez-le « SharedPlayground. » Ensuite, cliquez sur « Ajouter un composant » et recherchez « gestionnaire réseau générique » et cliquez dessus pour ajouter le composant Gestionnaire de réseau générique. Modifier la position de l’objet à x = 0, y = 0 et z = 0.

    ![Module3Chapter3step7im](images/module3chapter3step7im.PNG)


## <a name="congratulations"></a>Félicitations

Une fois que toutes les étapes ci-dessus sont terminées, et le processus de génération est terminé, lorsque vous appuyez sur le bouton de lecture et que vous vous connectez votre 2 HoloLens, vous devez voir une sphère déplaçant à mesure que vous déplacez votre tête ! Elle sera visible pour tous les utilisateurs qui se joint à votre projet Unity !

[Leçon suivante : Sharing(Photon) leçon 4](mrlearning-sharing(photon)-ch4.md)

