---
title: 2. Initialisation de votre projet et de votre première application
description: Partie 2 d’un tutoriel pour créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in UX Tools du Mixed Reality Toolkit
author: sw5813
ms.author: suwu
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: fc85f011ff3b186f3b4b5449b4f8ec49f0b6418f
ms.sourcegitcommit: 189a47b8712dd5b620e19815f5cf6d1ac0f29880
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2020
ms.locfileid: "82851573"
---
# <a name="2-initializing-your-project-and-first-application"></a>2. Initialisation de votre projet et de votre première application

Cette section vous aide à créer une application Unreal pour HoloLens 2. 

## <a name="objectives"></a>Objectifs

* Configurer Unreal pour le développement HoloLens
* Importer les ressources et configurer la scène

## <a name="create-a-new-unreal-project"></a>Créer un projet Unreal

1. Lancer Unreal Engine

2. Sous **New Project Categories**, sélectionnez **Games**, puis cliquez sur Next. Sélectionnez un modèle **Blank**, puis cliquez sur Next. 

![Sélectionner le modèle Blank](images/unreal-uxt/2-template.PNG)

3. Dans Project Settings, choisissez **C++, Scalable 3D or 2D, Mobile / Tablet**, et **No Starter Content**. Sélectionnez un emplacement où enregistrer votre projet, puis cliquez sur **Create Project**. Ceci ouvre vos fichiers C++ dans un projet Visual Studio et dans l’éditeur Unreal. 

![Paramètres du projet initial](images/unreal-uxt/2-project-settings.PNG)

4. Dans le coin supérieur gauche, accédez à **Edit > Plugins**. Sous Augmented Reality, cochez la case pour activer le plug-in **HoloLens**. Faites défiler jusqu’à la section Virtual Reality, puis cochez la case pour activer le plug-in **Microsoft Windows Mixed Reality**. Les deux plug-ins sont nécessaires pour le développement HoloLens 2. Redémarrez votre éditeur. 

![Plug-ins](images/unreal-uxt/2-plugins.PNG)

5. Dans le coin supérieur gauche, accédez à **File > New Level**. Sélectionnez **Empty Level**. La scène par défaut dans la fenêtre d’affichage doit maintenant être vide.

6. Faites glisser PlayerStart et déposez PlayerStart à partir du panneau Modes sur la gauche, situé sous l’onglet Basic. Dans le volet d’informations sur la droite, définissez l’emplacement sur X = 0, Y = 0, Z = 0 pour que l’utilisateur commence à l’origine quand l’application démarre.

![Fenêtre d’affichage avec PlayerStart](images/unreal-uxt/2-playerstart.PNG)

7. Faites glisser **Cube** à partir de l’onglet Basic du panneau Modes vers la fenêtre d’affichage. Dans le volet d’informations, définissez l’emplacement sur X = 50, Y = 0, Z = 0 pour placer le cube à 50 cm de distance du lecteur au moment du démarrage. Étant donné que le cube par défaut est assez grand, remplacez l’échelle du cube par (0,2 ; 0,2 ; 0,2). 

8. Vous ne pourrez pas voir le cube sauf si vous ajoutez une lumière à votre scène. Passez à l’onglet **Lights** dans le panneau Modes, puis faites glisser une **Directional Light** dans la scène, au-dessus du PlayerStart.

![Fenêtre d’affichage avec une lumière ajoutée](images/unreal-uxt/2-light.PNG)

9.  Appuyez sur le bouton **Play** dans la barre d’outils pour voir votre cube dans la fenêtre d’affichage ! Appuyez sur **Échap** pour arrêter le niveau. 

![Un cube dans la fenêtre d’affichage](images/unreal-uxt/2-cube.PNG)

10. Enregistrons votre niveau. Dans le coin supérieur gauche, cliquez sur **File > Save Current**. Nommez votre niveau « Main », puis cliquez sur **Save**. 

## <a name="set-up-a-chess-scene"></a>Configurer une scène de jeu d’échecs

1. Dans votre navigateur de contenu, cliquez sur l’icône sous Add New pour afficher le panneau des sources. Cliquez ensuite sur **Add New > New Folder** et nommez le dossier « ChessAssets ». Double-cliquez sur ce dossier pour y accéder. C’est là que nous allons importer les ressources 3D pour notre jeu d’échecs.

![Afficher ou masquer le panneau des sources](images/unreal-uxt/2-showhidesources.PNG)

2. Téléchargez le fichier zip des ressources depuis [GitHub](https://github.com/microsoft/MixedReality-Unreal-Samples/blob/master/ChessApp/ChessAssets.7z). Ce fichier contient les modèles 3D pour un échiquier et pour les pièces du jeu d’échecs. Décompressez ce fichier.

3. En haut du navigateur de contenu, cliquez sur **Import**. Accédez au dossier que vous venez de décompresser et sélectionnez tous les éléments qui s’y trouvent. Ce dossier contient des fichiers FBX qui sont les maillages des objets 3D pour notre échiquier et nos pièces, ainsi que des fichiers TGA qui sont les cartes de texture que nous allons utiliser pour créer des matériaux pour notre échiquier et nos pièces. Cliquez sur **Ouvrir**. 

4. Une fenêtre FBX Import Options s’ouvre. Dans la section **Material**, changez **Material Import Method** en **Do Not Create Material**. Ensuite, cliquez sur **Import All**.

![Options d’importation FBX](images/unreal-uxt/2-nocreatemat.PNG)

5. De retour dans votre dossier de contenu, créez un dossier nommé **Blueprints**. C’est là que nous allons stocker tous nos blueprints, qui sont des ressources spéciales qui fournissent une interface basée sur des nœuds pour créer des types d’acteurs et d’événements au niveau des scripts. 

6. Double-cliquez sur le dossier **Blueprints** pour y accéder, puis cliquez avec le bouton droit dans votre navigateur de contenu et sélectionnez **Blueprint Class**. Cliquez sur **Actor** et nommez le nouveau blueprint « Board ». Double-cliquez sur Board pour l’ouvrir. 

![Sélectionner une classe parente pour votre blueprint](images/unreal-uxt/2-bpparent.PNG)

![Le nouveau blueprint Board](images/unreal-uxt/2-bpboard.PNG)

7. Dans l’éditeur de blueprint, accédez au panneau Components, puis cliquez sur **Add Component > Scene**. Nommez la scène nouvellement créée « Root », puis cliquez et faites glisser Root sur DefaultSceneRoot. Cela va remplacer la racine de la scène par défaut et éliminer de la sphère dans la fenêtre d’affichage. 

![Remplacement de la racine](images/unreal-uxt/2-root.PNG)

8. Cliquez à nouveau sur **Add Component** et choisissez cette fois **Static Mesh**. Nommez le nouveau maillage statique « SM_Board ». 

![Ajout d’un maillage statique](images/unreal-uxt/2-sm-board.PNG)

9. Dans le panneau **Details**, recherchez la section **Static Mesh** et cliquez sur la liste déroulante. Sélectionnez **ChessBoard**. 

![Le maillage de l’échiquier dans la fenêtre d’affichage](images/unreal-uxt/2-sm-board-view.PNG)

10. Toujours dans le panneau **Details**, recherchez la section **Materials** et cliquez sur la liste déroulante. Sous **Create New Asset**, sélectionnez **Material**. Nommez cette ressource **M_ChessBoard** et enregistrez-la dans le dossier **ChessAssets**. 

![Créer un matériau](images/unreal-uxt/2-newmat.PNG)

11. Double-cliquez sur le carré en regard de la liste déroulante de M_ChessBoard pour ouvrir votre matériau M_ChessBoard nouvellement créé. Dans l’éditeur de matériau, cliquez avec le bouton droit et recherchez le nœud **Texture Sample**. Dans le panneau **Details** sous la section **Material Expression Texture Base**, cliquez sur la liste déroulante et sélectionnez **ChessBoard_Albedo**. Enfin, faites glisser la broche de sortie **RGB** vers la broche Base Color de **M_ChessBoard**. 

![Définir la couleur de base](images/unreal-uxt/2-boardalbedomat.PNG)

12. Procédez de même quatre fois de plus, en liant l’exemple de texture **ChessBoard_AO** à la broche**Ambient Occlusion**, l’exemple de texture **ChessBoard_Metal** à la broche **Metallic**, l’exemple de texture **ChessBoard_Normal** à la broche **Normal** et l’exemple de texture **ChessBoard_Rough** à la broche **Roughness**. Cliquez sur **Enregistrer**. 

![Raccorder les textures restantes](images/unreal-uxt/2-boardmat.PNG)

13. Ouvrez à votre blueprint **Board**. Vous voyez normalement que le matériau que vous venez de créer a été appliqué à votre blueprint. Pour que l’échiquier ait une taille et un emplacement raisonnables une fois que nous le plaçons dans notre scène, changez l’échelle **Scale** de l’échiquier en (0,05 ; 0,05 ; 0,05) et la **Rotation**  en Z = 90. Dans la barre d’outils du haut, cliquez sur **Compile**, puis sur **Save**. Revenez dans votre fenêtre principale. 

![Échiquier avec un matériau appliqué](images/unreal-uxt/2-chessboard.PNG)

14. Nous allons maintenant supprimer le cube et le remplacer par l’acteur Board que vous venez de créer. Dans le **World Outliner**, cliquez avec le bouton droit sur **Cube > Edit > Delete**. Faites l’échiquier de votre navigateur de contenu vers la fenêtre d’affichage. Définissez l’emplacement de l’échiquier sur X = 80, Y = 0, Z = -20. 

15. Cliquez sur le bouton **Play** pour afficher votre nouvel échiquier dans votre niveau. Appuyez sur **Échap** pour revenir à l’éditeur. 

16. Nous allons maintenant suivre les mêmes étapes pour créer une pièce du jeu d’échecs comme nous l’avons fait avec l’échiquier, en sélectionnant cette fois le maillage et le matériau pour la pièce :

    a) Accédez au dossier Blueprints dans le navigateur de contenu et créez une nouvelle classe Blueprint de type Actor. Nommez cet acteur « WhiteKing ».

    b) Double-cliquez sur WhiteKing pour l’ouvrir. Ajoutez un nouveau composant de scène nommé « Root » et utilisez-le pour remplacer DefaultSceneRoot. 

    c) Ajoutez un nouveau composant Static Mesh nommé « SM_King ». Dans le volet d’informations, définissez le **Static Mesh** sur **Chess_King** et **Material** sur un nouveau matériau appelé **M_ChessWhite**. 

    d) Ouvrez le nouveau matériau **M_ChessWhite** et raccordez les textures appropriées à leurs entrées de matériau correspondantes. 

    ![Créer le matériau pour le roi](images/unreal-uxt/2-chesskingmat.PNG)

    e) De retour dans votre blueprint **WhiteKing**, changez **Scale** en (0,05 ; 0,05 ; 0,05) et **Rotation** en Z = 90.

    f) Compilez et enregistrez votre blueprint, puis revenez à votre fenêtre principale. 

17. Faites glisser WhiteKing dans votre fenêtre d’affichage. Dans **World Outliner**, faites glisser WhiteKing sur Board, pour que WhiteKing soit désormais un enfant de Board. 

![World Outliner](images/unreal-uxt/2-child.PNG)

18. Dans le panneau **Details** sous **Transform**, définissez **Location** pour WhiteKing sur X =-26, Y = 4, Z = 0

19. Cliquez sur **Play** pour voir votre niveau. Appuyez sur **Échap** pour quitter. 

[Section suivante : 3. Configurer votre projet pour la réalité mixte](unreal-uxt-ch3.md)