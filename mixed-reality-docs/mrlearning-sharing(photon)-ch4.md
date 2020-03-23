---
title: Tutoriels sur les fonctionnalités multi-utilisateurs - 4. Partage de mouvements d’objet avec plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: b0ddf0799fd94c29ce8f1221c55073cd77b63703
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79031249"
---
# <a name="4-sharing-object-movements-with-multiple-users"></a>4. Partage de mouvements d’objet avec plusieurs utilisateurs

Dans ce tutoriel, vous allez apprendre à partager les mouvements d’objet afin que tous les participants d’une session partagée puissent collaborer et voir les interactions des autres. Cette leçon s’appuie sur le lanceur lunaire créé dans le cadre des [tutoriels du module de base](mrlearning-base.md).

## <a name="objectives"></a>Objectifs

- Faire apparaître le lanceur lunaire en tant que modèle 3D à partager
- Configurer votre projet pour partager les mouvements du modèle 3D
- Apprendre à créer une application collaborative multi-utilisateur de base

## <a name="instructions"></a>Instructions

1. Enregistrez la scène de la leçon précédente (Ctrl+S). Vous pouvez la nommer HLSharedProjectMainPart4.unity pour la retrouver plus facilement quand vous en avez besoin.

2. Dans la fenêtre Project, dans le dossier Assets->Scripts, double-cliquez sur GenericNetSync pour l’ouvrir dans Visual Studio ou dans l’éditeur de code que vous utilisez, quel qu’il soit.  

    ![module3chapter4updatestep2](images/module3chapter4updatestep2.png)

3. Lignes 34 et 38, supprimez « // » pour activer le code pour la table que vous allez utiliser dans cette leçon. Enregistrez ensuite le fichier.

    ![module3chapter4updatestep3](images/module3chapter4updatestep3.png)

4. Dans la fenêtre Project, double-cliquez sur le fichier PhotonRoom.cs dans le dossier Assets->Scripts pour l’ouvrir dans Visual Studio.

    ![module3chapter4updatestep4](images/module3chapter4updatestep4.png)

5. Comme à l’étape 3, nous avons besoin de supprimer « // » pour activer le code aux lignes 25, 26 et 106.

    ![module3chapter4updatestep5a](images/module3chapter4updatestep5a.png)

    ![module3chapter4updatestep5b](images/module3chapter4updatestep5b.png)

6. Dans la vue Hierarchy, sélectionnez l’objet NetworkRoom.

    ![module3chapter4updatestep6](images/module3chapter4updatestep6.png)

7. Dans la vue Project, accédez à Assets->Resources->Prefabs. Tout d’abord, glissez-déposez le préfabriqué Table vers l’emplacement Tableprefab sur la classe PhotonRoom. Ensuite, glissez-déplacez RocketLauncherCompleteVariantprefab vers l’emplacement Module Prefab sur la classe PhotonRoom.

    ![module3chapter4updatestep7](images/module3chapter4updatestep7.png)

    >[!NOTE]
    >Si vous cliquez sur l’un des objets d’élément préfabriqué avant de relâcher le bouton de la souris, l’inspecteur bascule vers cet objet. Cliquez sur chaque objet, faites-les glisser, déposez-les et relâchez-les à l’emplacement approprié.

8. Cliquez sur la flèche située à gauche de MixedRealityPlayspace pour déplacer l’objet jeu enfant MainCamera jusqu’au préfabriqué SharedPlayground. Ensuite, supprimez le préfabriqué MixedRealityPlayspace en le sélectionnant et en appuyant sur « suppr » sur votre clavier.

    ![Module3hapter4step5im](images/module3chapter4step5im.PNG)

    >[!NOTE]
    >Assurez-vous que les positions de Main Camera et SharedPlayground sont définies sur 0, 0, 0.

9. Sélectionnez l’objet « SharedPlayground » et cliquez avec le bouton droit de la souris pour choisir l’option « create empty » afin de créer un objet jeu vide en tant qu’enfant de l’objet jeu « SharedPlayground ».

   ![Module3chapter4step6im](images/module3chapter4step6im.PNG)

10. Après avoir sélectionné le nouvel objet dans votre hiérarchie, remplacez son nom par TableAnchor dans le panneau Inspector. De plus, cliquez sur Ajouter un composant et recherchez le composant TableAnchor. Sélectionnez-le et ajoutez-le à l’objet.

    ![Module3Chapter4step7im](images/module3chapter4step7im.PNG)

11. À partir du panneau Project dans le dossier Prefabs, faites glisser le préfabriqué Table dans l’objet enfant « TableAnchor » que vous venez de créer.

    ![Module3Chapter4step8im](images/module3chapter4step8im.PNG)

## <a name="congratulations"></a>Félicitations

Une fois cette opération terminée, recherchez le module lunaire. À présent, tous les utilisateurs qui rejoignent votre projet Unity peuvent déplacer le lanceur lunaire.  Tous les mouvements sont synchronisés afin que chaque utilisateur puisse voir les interactions des autres. Ces concepts servent de composants fondamentaux aux expériences de collaboration complètes et partagées.

Bien que tous les utilisateurs soient connectés dans le cadre d’une expérience partagée et puissent voir les mouvements relatifs des objets, l’application n’est toujours pas en mesure d’aligner correctement les avatars et les objets, de sorte que les utilisateurs locaux ne peuvent pas se voir les uns les autres ni voir les objets situés au même endroit dans le monde physique. Pour ancrer des expériences partagées locales, chaque appareil nécessite une compréhension commune de l’environnement physique. Dans ce module, nous allons nous atteler à ce problème en utilisant [Azure Spatial Anchors](<https://azure.microsoft.com//services/spatial-anchors/>) (ASA) que nous allons implémenter dans la prochaine leçon.

Avant de passer à la leçon suivante, nous allons devoir suivre le module d’apprentissage ASA qui traite des principes fondamentaux d’ASA, de la création de comptes et de ressources Azure, ainsi que d’autres composants fondamentaux nécessaires avant de pouvoir intégrer ASA à notre expérience partagée.

[Leçon suivante : 5. Intégration d’ancres spatiales Azure dans une expérience partagée](mrlearning-sharing(photon)-ch5.md)
