---
title: 5. Ajout d’un bouton et réinitialisation des positions des pièces
description: Partie 5 d’un tutoriel pour créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in UX Tools du Mixed Reality Toolkit
author: sw5813
ms.author: suwu
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: 77fe2b59db970a2ac4b531d69efec6794478f7d5
ms.sourcegitcommit: 09d9fa153cd9072f60e33a5f83ced8167496fcd7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/18/2020
ms.locfileid: "83519991"
---
# <a name="5-adding-a-button--resetting-piece-locations"></a>5. Ajout d’un bouton et réinitialisation des positions des pièces

Cette section continue la présentation des fonctionnalités du plug-in UX Tools du Mixed Reality Toolkit et le développement des fonctionnalités de votre application de jeu d’échecs. Vous allez créer une autre fonction et apprendre à obtenir des références aux acteurs de votre niveau dans un Blueprint.

## <a name="objectives"></a>Objectifs

* Ajouter un bouton à votre projet
* Créer une fonction « Reset Location » qui remet une pièce à sa position d’origine
* Lier le bouton pour déclencher la nouvelle fonction quand l’utilisateur appuie dessus

## <a name="create-a-function-to-reset-location"></a>Créer une fonction pour réinitialiser la position

1.  Ouvrez **WhiteKing**. Dans le panneau **My Blueprint**, cliquez sur le bouton « + » en regard de la section **Functions** pour créer une fonction. Nommez cette fonction « Reset Location ». 

2.  Dans le Blueprint **Reset Location** que vous venez de créer, faites glisser la broche d’exécution et relâchez-la n’importe où sur la grille du Blueprint pour appeler un nœud **SetActorRelativeTransform**. Cette fonction définit la transformation (position, rotation et échelle) d’un acteur par rapport à son parent. Nous allons utiliser cette fonction pour réinitialiser la position du roi sur l’échiquier, même si celui-ci a été déplacé de sa position d’origine. Créez un nœud **Make Transform** avec la position X = -26, Y = 4, Z = 0, et reliez-le à l’entrée New Relative Transform. 

![Fonction Reset Location](images/unreal-uxt/5-function.PNG)

3.  Compilez et enregistrez **WhiteKing**. Revenez dans la fenêtre principale. 

## <a name="add-a-button"></a>Ajouter un bouton

1.  Dans votre dossier **Blueprints**, créez un Blueprint dérivé de la classe SimpleButton. SimpleButton est un bouton 3D d’un acteur Blueprint qui est fourni dans le plug-in UX Tools. Nommez ce bouton « ResetButton » et double-cliquez pour ouvrir le Blueprint. 

![Nouveau Blueprint dérivé de la classe SimpleButton](images/unreal-uxt/5-subclass.PNG)

2.  Dans le volet **Components**, cliquez sur **PressableButton (Inherited)** . Dans le volet Details, faites défiler le contenu jusqu’à la section **Events**. Cliquez sur le bouton plus vert à côté de **On Button Pressed**. Cette action ajoute un événement **On Button Pressed** à l’Event Graph, qui est appelé quand l’utilisateur appuie sur le bouton. Maintenant, nous voulons appeler la fonction Reset Location de WhiteKing. Pour ce faire, nous devons d’abord obtenir une référence à l’acteur WhiteKing dans notre niveau. 

3.  Dans le volet **My Blueprint**, recherchez la section **Variables**, puis cliquez sur le bouton **+** pour ajouter une nouvelle variable. Nommez cette variable « WhiteKing ». Dans le volet Details, sélectionnez la liste déroulante à côté de **Variable Type**, recherchez « WhiteKing », puis sélectionnez **Object Reference**. Enfin, cochez la case **Instance Editable**. Cela permettra de définir la variable à partir du niveau principal (Main). 

![Créer une variable](images/unreal-uxt/5-var.PNG)

4.  Faites glisser la variable WhiteKing depuis **My Blueprint > Variables** vers l’Event Graph de Reset Button. Choisissez **Get WhiteKing**. 

5.  Faites glisser la broche de sortie WhiteKing et relâchez-la pour placer un nouveau nœud. Sélectionnez la fonction **Reset Location**. Pour finir, faites glisser la broche d’exécution sortante depuis **On Button Pressed** vers la broche d’exécution entrante sur **Reset Location**. **Compilez** et **enregistrez** le Blueprint ResetButton, puis revenez dans la fenêtre principale. 

![Appeler la fonction Reset Location à partir de l’événement On Button Pressed](images/unreal-uxt/5-callresetloc.PNG)

6.  Faites glisser **ResetButton** vers la fenêtre Viewport et définissez sa position sur X = 50, Y = -25, Z = 10. Sous **Default**, définissez la valeur de la variable WhiteKing sur **WhiteKing**.

![Définir la variable](images/unreal-uxt/5-buttonlevel.PNG)

Votre application de réalité mixte comporte maintenant un échiquier et une pièce saisissable, ainsi qu’un bouton opérationnel qui réinitialise la position de la pièce quand l’utilisateur appuie dessus. L’application terminée à ce stade est disponible sur [GitHub](https://github.com/microsoft/MixedReality-Unreal-Samples/tree/master/ChessApp). N’hésitez pas à aller plus loin que ce tutoriel et à configurer toutes les autres pièces du jeu d’échecs afin que leurs positions sur l’échiquier soient réinitialisées lorsque l’utilisateur appuie sur le bouton.

![Scène finale dans la fenêtre Viewport](images/unreal-uxt/5-endscene.PNG)

[Section suivante : 6. Empaquetage et déploiement sur un appareil ou un émulateur](unreal-uxt-ch6.md)
