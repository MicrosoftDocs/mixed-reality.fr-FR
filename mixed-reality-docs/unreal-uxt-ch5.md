---
title: 5. Ajout d’un bouton et réinitialisation des positions des pièces
description: Cinquième tutoriel d’une série de six visant à créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in Mixed Reality Toolkit UX Tools
author: hferrone
ms.author: v-haferr
ms.date: 06/10/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: 473f47884bbc492451007436f80e8d9762cf1ab7
ms.sourcegitcommit: 45da0a056fa42088ff81ccdd11232830fbe8430f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84720255"
---
# <a name="5-adding-a-button--resetting-piece-locations"></a>5. Ajout d’un bouton et réinitialisation des positions des pièces


## <a name="overview"></a>Vue d’ensemble

Dans le tutoriel précédent, vous avez ajouté des acteurs d’interaction manuelle aux composants Pawn et Manipulator de l’échiquier pour les rendre interactifs. Dans cette section, vous allez continuer de travailler avec le plug-in Mixed Reality Toolkit UX Tools en développant les fonctionnalités de votre application de jeu d’échecs. Vous allez notamment créer une fonction et apprendre à obtenir des références aux acteurs dans un blueprint. À la fin de cette section, vous serez prêt à empaqueter et déployer l’application de réalité mixte sur un appareil ou un émulateur.

## <a name="objectives"></a>Objectifs

* Ajouter un bouton interactif
* Créer une fonction pour réinitialiser l’emplacement d’une pièce
* Lier le bouton pour déclencher la fonction quand l’utilisateur appuie dessus

## <a name="creating-a-reset-function"></a>Création d’une fonction de réinitialisation
Votre première tâche consiste à créer un blueprint de fonction qui remet une pièce d’échec à sa position d’origine dans la scène. 

1.  Ouvrez **WhiteKing**, cliquez sur l’icône **+** en regard de la section **Functions** de **My Blueprint**, puis nommez-la **Reset Location**. 

2.  Faites glisser l’exécution de **Drag and release** vers la grille Blueprint pour créer un nœud **SetActorRelativeTransform**. 
    * Cette fonction définit la transformation (position, rotation et échelle) d’un acteur par rapport à son parent. Vous allez utiliser cette fonction pour réinitialiser la position du roi sur l’échiquier, même si celui-ci a été déplacé de sa position d’origine. 
    
3. Cliquez avec le bouton droit dans le graphique d’événements, sélectionnez **Make Transform**, puis déplacez-le en définissant le paramètre **Location** comme suit : **X =-26**, **Y = 4**, **Z = 0**.
    * Connectez sa valeur de retour (**Return Value**) au repère **New Relative Transform** dans **SetActorRelativeTransform**. 

![Fonction Reset Location](images/unreal-uxt/5-function.PNG)

**Compilez** et **enregistrez** le projet avant de revenir à la fenêtre principale. 


## <a name="adding-a-button"></a>Ajouter un bouton
Maintenant que la fonction est correctement configurée, la tâche suivante consiste à créer un bouton qui la déclenche quand le joueur appuie dessus. 

1.  Cliquez sur **Add New > Blueprint Class**, développez la section **All Classes**, puis recherchez **SimpleButton**. 
    * Nommez ce bouton **ResetButton** et double-cliquez pour ouvrir le blueprint.

> [!NOTE]
> **SimpleButton** est un bouton 3D d’un acteur Blueprint qui est intégré au plug-in UX Tools. . 

![Nouveau Blueprint dérivé de la classe SimpleButton](images/unreal-uxt/5-subclass.PNG)

2. Cliquez sur **Pressable Button (Inherited)** dans le panneau **Components** et faites défiler le volet **Details** jusqu’à la section **Events**. 
    * Cliquez sur le bouton vert **+** à côté de **On Button Pressed** pour ajouter un événement au graphique d’événements, qui est appelé quand le joueur appuie sur le bouton. 
    
À partir de là, vous devez appeler la fonction **Reset Location** de **WhiteKing**, qui a besoin d’une référence à l’acteur **WhiteKing** dans le niveau. 

1.  Accédez à la section **Variables** du panneau **Details**, cliquez sur le bouton **+** , puis nommez la variable **WhiteKing**. 
    * Sélectionnez la liste déroulante à côté de **Variable Type**, recherchez **WhiteKing**, puis sélectionnez **Object Reference**. 
    * Cochez la case à côté de **Instance Editable**. Cela permettra de définir la variable à partir du niveau principal (Main). 

![Créer une variable](images/unreal-uxt/5-var.PNG)

2.  Faites glisser la variable WhiteKing de **My Blueprint > Variables** vers le graphique d’événements de Reset Button et choisissez **Get WhiteKing**. 

## <a name="firing-the-function"></a>Déclenchement de la fonction
Il ne reste plus qu’à déclencher expressément la fonction de réinitialisation dès lors que le joueur appuie sur le bouton.

1.  Faites glisser la broche de sortie WhiteKing et relâchez-la pour placer un nouveau nœud. Sélectionnez la fonction **Reset Location**. Pour finir, faites glisser la broche d’exécution sortante depuis **On Button Pressed** vers la broche d’exécution entrante sur **Reset Location**. **Compilez** et **enregistrez** le Blueprint ResetButton, puis revenez dans la fenêtre principale. 

![Appeler la fonction Reset Location à partir de l’événement On Button Pressed](images/unreal-uxt/5-callresetloc.PNG)

2.  Faites glisser **ResetButton** vers la fenêtre Viewport et définissez son emplacement sur **X = 50**, **Y = -25** et **Z = 10**. Sous **Default**, attribuez à la variable **WhiteKing** la valeur **WhiteKing**.

![Définir la variable](images/unreal-uxt/5-buttonlevel.PNG)

Exécutez l’application, déplacez la pièce d’échec vers son nouvel emplacement, puis appuyez sur le gros bouton rose pour voir la logique de réinitialisation en action.

Votre application de réalité mixte comporte maintenant un échiquier et une pièce avec laquelle vous pouvez interagir, ainsi qu’un bouton entièrement opérationnel qui réinitialise l’emplacement de la pièce. Vous trouverez l’application à ce stade d’avancement dans son dépôt [GitHub](https://github.com/microsoft/MixedReality-Unreal-Samples/tree/master/ChessApp). N’hésitez pas à aller au-delà de ce tutoriel et à configurer les autres pièces du jeu d’échecs en faisant en sorte que l’échiquier se réinitialise entièrement quand le joueur appuie sur le bouton.

![Scène finale dans la fenêtre Viewport](images/unreal-uxt/5-endscene.PNG)

Vous êtes prêt à passer à la dernière section de ce tutoriel, dans laquelle vous allez apprendre à empaqueter et déployer correctement l’application sur un appareil ou un émulateur.

[Section suivante : 6. Empaquetage et déploiement sur un appareil ou un émulateur](unreal-uxt-ch6.md)
