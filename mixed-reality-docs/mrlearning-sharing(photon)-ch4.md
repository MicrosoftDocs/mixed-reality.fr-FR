---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: a67eaef45582054b62198a563f0ee01724fd60db
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67327443"
---
# <a name="synchronizing-the-movements-of-shared-objects"></a>Synchronisation des mouvements des objets partagés

Dans cette leçon, nous allez apprendre à partager les mouvements des objets afin que tous les participants d’une session partagée peuvent collaborer et afficher leurs interactions. Cette leçon repose sur le Lanceur lunaire qui a été créé dans le cadre de la [didacticiels de Module de Base](mrlearning-base.md).

Objectifs :

- Importer le Lanceur lunaire terminé en tant que le modèle 3D à partager
- Configurer votre projet pour partager les mouvements d’un modèle 3D.
- Découvrez comment créer une application de collaboration multi-utilisateur base

### <a name="instructions"></a>Instructions

1. Enregistrer la scène à partir de la leçon précédente (CTRL + S). Vous pouvez le nommer « HLSharedProjectMainPart4.unity » afin qu’il soit plus facile à trouver lorsque vous en avez besoin à nouveau.

2. Supprimer l’objet « NetworkLobby » (en le sélectionnant et en appuyant sur Supprimer). En outre, accédez dans le dossier « prefabs » à partir de la leçon 2 et supprimer le préfabriqué « NetworkLobby » à partir de là aussi.

![Module3Chapter4tep2im](images/module3chapter4step2im.PNG)

3. Importer un nouveau package personnalisé (par exemple, l’étape 2 de la leçon 2) et importer le [LunarModule.unitypackage](linkforModule1 lesson with the lunar module) et [NetworkLobbyReplacement.unitypackage.](linkforNetworklobbyreplacement package here)

![Module3Chapter4step3im](images/module3chapter4step3im.PNG)

4. Maintenant, dans le dossier « prefabs », faites glisser la nouvelle préfabriqué « NetworkLobby » dans la hiérarchie. 

![Module3hapter4step4im](images/module3chapter4step4im.PNG)

> Remarque : les deux packages, nous avons importé dans les étapes précédentes mises à jour le préfabriqué « NetworkLobby ». Il vous évite beaucoup de saisie !

5. Maintenant, cliquez sur la flèche à gauche de « MixedRealityPlayspace » et déplacer l’objet de jeu d’enfant, « MainCamera » vers le bas dans le préfabriqué « SharedPlayground ». Ensuite, supprimez le prefab « MixedRealityPlayspace » (pour les supprimer, sélectionnez le préfabriqué et appuyez sur « Supprimer » de votre clavier).

![Module3hapter4step5im](images/module3chapter4step5im.PNG)

6. Créer un nouvel objet de jeu définie en tant qu’objet enfant à l’objet parent de « SharedPlayground » (pour créer un nouvel objet, cliquez avec le bouton droit sur l’objet parent et sélectionnez « Créer vide »).
7. Avec le nouvel objet sélectionné dans votre hiérarchie, modifier le nom de l’objet à « TableAnchor » dans le panneau de l’inspecteur. En outre, cliquez sur « Ajouter un composant » et recherchez le composant « TableAnchor ». Sélectionnez-le et ajoutez-le à l’objet.

![Module3Chapter4step6im](images/module3chapter4step7im.PNG)

> Remarque : définir le positionnement à x = 1, y =-0,55 et z = 2. En outre, la valeur est la rotation y = 90. 
>
> ![Module3Chapter4step6im](images/module3chapter4noteim.PNG)

8. Maintenant dans le volet de projet, dans le dossier « prefabs », faites glisser le préfabriqué « table » dans l’objet enfant de « TableAnchor » vous venez de créer.

   ![Module3Chapter4step8im](images/module3chapter4step8im.PNG)

9. Sélectionnez « NetworkRoom », un objet enfant sous « NetworkLobby » dans la hiérarchie et cliquez sur « Ajouter un composant » dans le panneau Inspecteur et recherchez « PhotonView » et ajoutez le script à la «*NetworkRoom*« objet.

![Module3Chapter4step9im](images/module3chapter4step9im.PNG)

11. Enfin, dans l’objet « DebugWindow », modifiez la largeur à 80 et la hauteur de 10.

![Module3Chapter4step9im](images/module3chapter4step11im.PNG)




## <a name="congratulations"></a>Félicitations

Une fois cette opération terminée, tous les utilisateurs qui rejoignent votre projet Unity peuvent déplacer le Lanceur lunaire. Tous les mouvements sont synchronisés afin que chaque utilisateur peut voir les uns des autres interactions. Ces concepts servent comme blocs de construction fondamentaux pour des expériences complètes de collaboration partagées. 

Bien que tous les utilisateurs sont connectés dans le cadre de l’expérience partagée et voyez les mouvements relatifs des objets, l’application est toujours Impossible d’aligner précisément les objets et les avatars afin que les utilisateurs locaux voient les uns des autres et les objets au même endroit dans physique World. Pour ancrer un expériences partagées local, chaque appareil nécessite une compréhension commune de l’environnement physique. Dans ce module, il peut y parvenir à l’aide de [ancres Spatial Azure](<https://azure.microsoft.com/en-us/services/spatial-anchors/>) (ASA), qui seront implémenté dans la leçon suivante.

Avant de passer à la leçon suivante, nous devrons effectuer le Module de formation ASA, qui couvre principes de base ASA, compte Azure et la création de ressources et d’autres blocs de bâtiments fondamentales nécessaires avant que nous pouvons intégrer cela dans notre expérience partagée.

[Leçon suivante : Sharing(Photon) leçon 5](mrlearning-sharing(photon)-ch5.md)

