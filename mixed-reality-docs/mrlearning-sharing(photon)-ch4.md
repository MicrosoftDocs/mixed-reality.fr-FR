---
title: Didacticiels sur les fonctionnalités multi-utilisateur-4. Partage des mouvements d’objets avec plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: f523aabd74b9267b3f7f5024d8af46110e43c32a
ms.sourcegitcommit: 23b130d03fea46a50a712b8301fe4e5deed6cf9c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2019
ms.locfileid: "75334284"
---
# <a name="4-sharing-object-movements-with-multiple-users"></a>4. partage des mouvements d’objets avec plusieurs utilisateurs

Dans ce didacticiel, vous allez apprendre à partager les mouvements d’objets afin que tous les participants d’une session partagée puissent collaborer et afficher les interactions entre eux. Cette leçon s’appuie sur le lanceur lunaire créé dans le cadre des [didacticiels du module de base](mrlearning-base.md).

## <a name="objectives"></a>Objectifs

- Amener le lanceur lunaire en tant que modèle 3D à partager
- Configurer votre projet pour partager les mouvements du modèle 3D
- Découvrez comment créer une application collaborative multi-utilisateur de base

## <a name="instructions"></a>Instructions

1. Enregistrez la scène de la leçon précédente (contrôle + S). Vous pouvez le nommer HLSharedProjectMainPart4. Unity pour qu’il soit plus facile à trouver lorsque vous en avez besoin.

2. Dans la fenêtre projet, dans le dossier Ressources-> scripts, double-cliquez sur GenericNetSync pour l’ouvrir dans Visual Studio ou dans l’éditeur de code que vous utilisez.  

    ![module3chapter4updatestep2](images/module3chapter4updatestep2.png)

3. Sur les lignes 34 et 38, supprimez « // » pour activer le code de la table que vous allez utiliser dans cette leçon. Ensuite, enregistrez le fichier.

    ![module3chapter4updatestep3](images/module3chapter4updatestep3.png)

4. Dans la fenêtre projet, double-cliquez sur le fichier PhotonRoom.cs dans le dossier Ressources-> scripts pour l’ouvrir dans Visual Studio.

    ![module3chapter4updatestep4](images/module3chapter4updatestep4.png)

5. Comme à l’étape 3, vous devez supprimer « // » pour activer le code aux lignes 25, 26 et 106.

    ![module3chapter4updatestep5a](images/module3chapter4updatestep5a.png)

    ![module3chapter4updatestep5b](images/module3chapter4updatestep5b.png)

6. Dans l’affichage des hiérarchies, sélectionnez l’objet NetworkRoom.

    ![module3chapter4updatestep6](images/module3chapter4updatestep6.png)

7. Dans la vue de projet, accédez à ressources-> Ressources-> Prefabs. Tout d’abord, glissez-déplacez la table Prefab vers l’emplacement Tableprefab sur la classe PhotonRoom. Ensuite, faites glisser et déposez RocketLauncherCompleteVariantprefab sur l’emplacement Prefab du module sur la classe PhotonRoom.

    ![module3chapter4updatestep7](images/module3chapter4updatestep7.png)

    >[!NOTE]
    >Si vous cliquez sur l’un des objets Prefab et que vous la libérez, l’inspecteur bascule sur cet objet. Cliquez sur, faites glisser, déposez et relâchez chaque objet à l’emplacement approprié.

8. Cliquez sur la flèche à gauche de MixedRealityPlayspace et déplacez l’objet de jeu enfant MainCamera vers le bas dans le Prefab SharedPlayground. Ensuite, supprimez le Prefab, MixedRealityPlayspace en sélectionnant le Prefab et appuyez sur « supprimer » sur votre clavier).

    ![Module3hapter4step5im](images/module3chapter4step5im.PNG)

    >[!NOTE]
    >Assurez-vous que les positions caméra principale et SharedPlayground sont définies sur 0, 0, 0.

9. Sélectionnez l’objet « SharedPlayground » et cliquez avec le bouton droit sur la souris pour choisir l’option « créer vide » afin de créer un objet de jeu vide en tant qu’enfant de l’objet de jeu « SharedPlayground ».

   ![Module3chapter4step6im](images/module3chapter4step6im.PNG)

10. Après avoir sélectionné le nouvel objet dans votre hiérarchie, remplacez le nom de l’objet par TableAnchor dans le panneau Inspecteur. En outre, cliquez sur Ajouter un composant et recherchez le composant TableAnchor. Sélectionnez-le et ajoutez-le à l’objet.

    ![Module3Chapter4step7im](images/module3chapter4step7im.PNG)

11. À partir du panneau projet dans le dossier Prefabs, faites glisser la table Prefab dans l’objet enfant « TableAnchor » que vous venez de créer.

    ![Module3Chapter4step8im](images/module3chapter4step8im.PNG)

12. Dans l’objet DebugWindow, remplacez la largeur par 50 et la hauteur par 20.

    ![Module3Chapter4step9im](images/module3chapter4step11im.PNG)

## <a name="congratulations"></a>Félicitations !

Une fois cette opération terminée, recherchez le module lunaire. Après cela, tous les utilisateurs qui rejoignent votre projet Unity peuvent déplacer le lanceur lunaire.  Tous les mouvements sont synchronisés afin que chaque utilisateur puisse voir les interactions entre eux. Ces concepts constituent les blocs de construction fondamentaux pour les expériences de collaboration complètes et partagées.

Bien que tous les utilisateurs soient connectés dans le cadre d’une expérience partagée et puissent voir les mouvements relatifs des objets, l’application n’est toujours pas en mesure d’aligner correctement les avatars et les objets, de sorte que les utilisateurs locaux n’ont pas pu voir les autres et les objets dans le même emplacement dans le monde physique. Pour pouvoir ancrer des expériences partagées locales, chaque appareil doit avoir une compréhension commune de l’environnement physique. Dans ce module, nous allons y parvenir en utilisant les [ancres spatiales Azure](<https://azure.microsoft.com//services/spatial-anchors/>) (ASA) qui seront implémentées dans la prochaine leçon.

Avant de passer à la leçon suivante, nous devrons suivre le module ASA Learning qui traite des principes fondamentaux de ASA, de la création de comptes et de ressources Azure, ainsi que d’autres blocs de construction fondamentaux nécessaires avant de pouvoir intégrer cela dans notre expérience partagée.

[Leçon suivante : 5. intégration des ancres spatiales Azure dans une expérience partagée](mrlearning-sharing(photon)-ch5.md)
