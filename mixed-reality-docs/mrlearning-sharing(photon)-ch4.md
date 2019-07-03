---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 2a4ea599fd4887f30589c2d839be305d3dc8d1bd
ms.sourcegitcommit: cf9f8ebbca0301e9d277853771ff6e47701ba1c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67523196"
---
# <a name="4-sharing-object-movements-with-multiple-users"></a>4. Partage des mouvements de l’objet avec plusieurs utilisateurs

Dans ce didacticiel, nous allez apprendre à partager les mouvements des objets afin que tous les participants d’une session partagée peuvent collaborer et afficher leurs interactions. Cette leçon repose sur le Lanceur lunaire qui a été créé dans le cadre de la [didacticiels de Module de Base](mrlearning-base.md).

Objectifs :

- Remettre dans le Lanceur lunaire que le modèle 3D à partager
- Configurer votre projet pour partager les mouvements d’un modèle 3D.
- Découvrez comment créer une application de collaboration multi-utilisateur base

### <a name="instructions"></a>Instructions


1. Enregistrer la scène à partir de la leçon précédente (contrôle + S). Vous pouvez le nommer, HLSharedProjectMainPart4.unity, afin qu’il soit plus facile à trouver lorsque vous en avez besoin.

2. À partir de la fenêtre projet, dans les ressources -> dossier Scripts, double-cliquez sur GenericNetSync pour l’ouvrir dans Visual Studio ou qui vous sont à l’aide de l’éditeur de code jamais.  ![](images/module3chapter4updatestep2.png)

3. Sur les lignes 34 et 38, supprimez les / / pour activer le code pour la table que nous utiliserons dans cette leçon. Ensuite, enregistrez le fichier. ![](images/module3chapter4updatestep3.png)

4. Dans la fenêtre projet, double-cliquez sur le fichier PhotonRoom.cs dans les ressources -> dossier de Scripts pour l’ouvrir dans Visual Studio. ![](images/module3chapter4updatestep4.png)

5. Comme à l’étape 3, nous devons supprimer les / / pour activer le code en lignes 25 et 26 106.![](images/module3chapter4updatestep5a.png) ![](images/module3chapter4updatestep5b.png)

6. Dans la vue de la hiérarchie, sélectionnez l’objet NetworkRoom.![](images/module3chapter4updatestep6.png)

7. Dans la vue du projet, accédez à ressources -> ressources -> Prefabs. Tout d’abord, faites glisser le préfabriqué de Table vers l’emplacement de Tableprefab sur la classe PhotonRoom. Ensuite glisser -déplacer le préfabriqué LunarModule vers l’emplacement de Module Prefab sur la classe PhotonRoom. ![](images/module3chapter4updatestep7.png)

   Remarque: Si vous cliquez sur l’un des objets prefab et mise en production, l’inspecteur passe à cet objet. Cliquez sur, faites glisser, déposer et libérer chaque objet de l’emplacement approprié.



8. Cliquez sur la flèche à gauche de MixedRealityPlayspace et déplacer l’objet de jeu d’enfant, MainCamera vers le bas dans le préfabriqué SharedPlayground. Ensuite, supprimez le préfabriqué, MixedRealityPlayspace, à supprimer, sélectionnez le préfabriqué, appuyez sur « delete » sur votre clavier).
![Module3hapter4step5im](images/module3chapter4step5im.PNG)

Remarque:  Assurez-vous que les positions de la Main Camera et SharedPlayground sont définies sur 0,0,0.

9. Créer un nouvel objet de jeu défini comme un objet enfant à l’objet parent de SharedPlayground pour créer un nouvel objet. Cliquez avec le bouton droit sur l’objet parent, puis sélectionnez Créer vide. 

10. Avec le nouvel objet sélectionné dans votre hiérarchie, modifier le nom de l’objet à TableAnchor dans le panneau de l’inspecteur. En outre, cliquez sur Ajouter un composant et recherchez le composant TableAnchor. Sélectionnez-le et ajoutez-le à l’objet. 

![Module3Chapter4step6im](images/module3chapter4step7im.PNG)

> Remarque: Définir le positionnement à x = 1, y =-0,55 et z = 2. En outre, la valeur est la rotation y = 90. 
>
> ![Module3Chapter4step6im](images/module3chapter4noteim.PNG)

11. Maintenant dans le volet de projet dans le dossier Prefabs, faites glisser le préfabriqué de Table dans l’objet enfant de « TableAnchor » vous venez de créer.

![Module3Chapter4step8im](images/module3chapter4step8im.PNG)



12. Enfin, dans l’objet DebugWindow, modifiez la largeur à 80 et la hauteur de 10.

![Module3Chapter4step9im](images/module3chapter4step11im.PNG)




## <a name="congratulations"></a>Félicitations


Une fois cette opération terminée, tous les utilisateurs qui rejoignent votre projet Unity peuvent déplacer le Lanceur lunaire. Tous les mouvements sont synchronisés afin que chaque utilisateur peut voir les uns des autres interactions. Ces concepts servent comme blocs de construction fondamentaux pour des expériences de collaboration complète, partagé. 

Bien que tous les utilisateurs sont connectés dans le cadre de l’expérience partagée et voyez les mouvements relatifs des objets, l’application est toujours Impossible d’aligner précisément les objets et les avatars afin que les utilisateurs locaux voient les uns des autres et les objets au même endroit dans physique World. Pour ancrer un expériences partagées local, chaque appareil nécessite une compréhension commune de l’environnement physique. Dans ce module, nous allons y parvenir en utilisant [ancres Spatial Azure](<https://azure.microsoft.com/en-us/services/spatial-anchors/>) (ASA) qui seront implémentés dans la leçon suivante.

Avant de passer à la leçon suivante, nous allons devoir effectuer le Module d’apprentissage ASA qui couvre des notions de base ASA, compte Azure et la création de ressources et d’autres blocs de bâtiments fondamentales nécessaires avant que nous pouvons intégrer cela dans notre expérience partagée.

[Leçon suivante : Sharing(Photon) leçon 5](mrlearning-sharing(photon)-ch5.md)

