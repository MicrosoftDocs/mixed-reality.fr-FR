---
title: Didacticiels sur les fonctionnalités multi-utilisateur-4. Partage des mouvements d’objets avec plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 2e676d319ba7221cf9549b200b3d748f26025aa7
ms.sourcegitcommit: af1602710c1ccb7ed870a491923350d387706129
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68701901"
---
# <a name="4-sharing-object-movements-with-multiple-users"></a>4. Partage des mouvements d’objets avec plusieurs utilisateurs

Dans ce didacticiel, nous apprenons à partager les mouvements d’objets afin que tous les participants d’une session partagée puissent collaborer et afficher les interactions entre eux. Cette leçon s’appuie sur le lanceur lunaire créé dans le cadre des [didacticiels du module de base](mrlearning-base.md).

Cherché

- Amener le lanceur lunaire en tant que modèle 3D à partager
- Configurez votre projet pour partager les mouvements du modèle 3D.
- Découvrez comment créer une application collaborative multi-utilisateur de base

## <a name="instructions"></a>Instructions


1. Enregistrez la scène de la leçon précédente (contrôle + S). Vous pouvez le nommer, HLSharedProjectMainPart4. Unity, afin qu’il soit plus facile à trouver lorsque vous en avez besoin.

2. Dans la fenêtre projet, dans le dossier Ressources-> scripts, double-cliquez sur GenericNetSync pour l’ouvrir dans Visual Studio ou dans l’éditeur de code que vous utilisez.  

![module3chapter4updatestep2](images/module3chapter4updatestep2.png)

3. Sur les lignes 34 et 38, supprimez le//pour activer le code de la table que nous allons utiliser dans cette leçon. Ensuite, enregistrez le fichier. 

![module3chapter4updatestep3](images/module3chapter4updatestep3.png)

4. Dans la fenêtre projet, double-cliquez sur le fichier PhotonRoom.cs dans le dossier Ressources-> scripts pour l’ouvrir dans Visual Studio. 

![module3chapter4updatestep4](images/module3chapter4updatestep4.png)

5. Comme à l’étape 3, vous devez supprimer le//pour activer le code aux lignes 25, 26 et 106.

![module3chapter4updatestep5a](images/module3chapter4updatestep5a.png) 

![module3chapter4updatestep5b](images/module3chapter4updatestep5b.png)

6. Dans l’affichage des hiérarchies, sélectionnez l’objet NetworkRoom.

![module3chapter4updatestep6](images/module3chapter4updatestep6.png)

7. Dans la vue de projet, accédez à ressources-> Ressources-> Prefabs. Tout d’abord, glissez-déplacez la table Prefab vers l’emplacement Tableprefab sur la classe PhotonRoom. Ensuite, glissez-déplacez le RocketLauncherCompleteVariantprefab vers l’emplacement Prefab du module sur la classe PhotonRoom.

![module3chapter4updatestep7](images/module3chapter4updatestep7.png)

   Remarque : Si vous cliquez sur l’un des objets Prefab et la version Release, l’inspecteur bascule sur cet objet. Cliquez sur, faites glisser, déposez et relâchez chaque objet à l’emplacement approprié.

8. Cliquez sur la flèche à gauche de MixedRealityPlayspace et déplacez l’objet de jeu enfant, MainCamera vers le bas dans le Prefab SharedPlayground. Ensuite, supprimez le Prefab, MixedRealityPlayspace, à supprimer, sélectionnez le Prefab, puis appuyez sur «supprimer» sur votre clavier).
![Module3hapter4step5im](images/module3chapter4step5im.PNG)

>Remarque :  Assurez-vous que les positions caméra principale et SharedPlayground sont définies sur 0, 0, 0.
>

9. Créez un nouvel objet de jeu défini en tant qu’objet enfant sur l’objet parent SharedPlayground pour créer un objet. Cliquez avec le bouton droit sur l’objet parent, puis sélectionnez Créer vide. 

10. Après avoir sélectionné le nouvel objet dans votre hiérarchie, remplacez le nom de l’objet par TableAnchor dans le panneau Inspecteur. En outre, cliquez sur Ajouter un composant, puis recherchez le composant TableAnchor. Sélectionnez-le et ajoutez-le à l’objet. 

![Module3Chapter4step6im](images/module3chapter4step7im.PNG)

11. À présent, à partir du panneau projet dans le dossier Prefabs, faites glisser la table Prefab dans l’objet enfant «TableAnchor» que vous venez de créer.

![Module3Chapter4step8im](images/module3chapter4step8im.PNG)

12. Enfin, dans l’objet DebugWindow, remplacez la largeur par 50 et la hauteur par 20.

![Module3Chapter4step9im](images/module3chapter4step11im.PNG)

## <a name="congratulations"></a>Félicitations


Une fois cette opération terminée, tous les utilisateurs qui rejoignent votre projet Unity peuvent déplacer le lanceur lunaire. Tous les mouvements sont synchronisés afin que chaque utilisateur puisse voir les interactions entre eux. Ces concepts constituent les blocs de construction fondamentaux pour les expériences de collaboration complètes et partagées. 

Bien que tous les utilisateurs soient connectés dans le cadre d’une expérience partagée et puissent voir les mouvements relatifs des objets, l’application n’est toujours pas en mesure d’aligner avec précision les avatars et les objets afin que les utilisateurs locaux puissent voir les objets et les objets dans le même emplacement au sein du réelles. Pour pouvoir ancrer des expériences partagées locales, chaque appareil doit avoir une compréhension commune de l’environnement physique. Dans ce module, nous allons y parvenir en utilisant les [ancres spatiales Azure](<https://azure.microsoft.com/en-us/services/spatial-anchors/>) (ASA) qui seront implémentées dans la prochaine leçon.

Avant de passer à la leçon suivante, nous devrons suivre le module ASA Learning qui traite des principes fondamentaux de ASA, de la création de comptes et de ressources Azure, ainsi que d’autres blocs de construction fondamentaux nécessaires avant de pouvoir les intégrer dans notre expérience partagée.

[Leçon suivante : 5. Intégration d’ancres spatiales Azure dans une expérience partagée](mrlearning-sharing(photon)-ch5.md)

