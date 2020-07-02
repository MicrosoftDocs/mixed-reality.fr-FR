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
# <a name="5-adding-a-button--resetting-piece-locations"></a><span data-ttu-id="4ee1e-104">5. Ajout d’un bouton et réinitialisation des positions des pièces</span><span class="sxs-lookup"><span data-stu-id="4ee1e-104">5. Adding a button & resetting piece locations</span></span>


## <a name="overview"></a><span data-ttu-id="4ee1e-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="4ee1e-105">Overview</span></span>

<span data-ttu-id="4ee1e-106">Dans le tutoriel précédent, vous avez ajouté des acteurs d’interaction manuelle aux composants Pawn et Manipulator de l’échiquier pour les rendre interactifs.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-106">In the previous tutorial, you added Hand Interaction Actors to the Pawn and Manipulator components to the chess board to make them both interactive.</span></span> <span data-ttu-id="4ee1e-107">Dans cette section, vous allez continuer de travailler avec le plug-in Mixed Reality Toolkit UX Tools en développant les fonctionnalités de votre application de jeu d’échecs.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-107">In this section, you'll continue working with the Mixed Reality Toolkit UX Tools plugin by building out the features of your chess app.</span></span> <span data-ttu-id="4ee1e-108">Vous allez notamment créer une fonction et apprendre à obtenir des références aux acteurs dans un blueprint.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-108">This includes creating a new function and learning how to get references to Actors in a Blueprint.</span></span> <span data-ttu-id="4ee1e-109">À la fin de cette section, vous serez prêt à empaqueter et déployer l’application de réalité mixte sur un appareil ou un émulateur.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-109">By the end of this section, you'll be ready to package and deploy the mixed reality app on a device or emulator.</span></span>

## <a name="objectives"></a><span data-ttu-id="4ee1e-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="4ee1e-110">Objectives</span></span>

* <span data-ttu-id="4ee1e-111">Ajouter un bouton interactif</span><span class="sxs-lookup"><span data-stu-id="4ee1e-111">Adding an interactive button</span></span>
* <span data-ttu-id="4ee1e-112">Créer une fonction pour réinitialiser l’emplacement d’une pièce</span><span class="sxs-lookup"><span data-stu-id="4ee1e-112">Creating a function to reset a pieces' location</span></span>
* <span data-ttu-id="4ee1e-113">Lier le bouton pour déclencher la fonction quand l’utilisateur appuie dessus</span><span class="sxs-lookup"><span data-stu-id="4ee1e-113">Hooking the button up to trigger the function when pressed</span></span>

## <a name="creating-a-reset-function"></a><span data-ttu-id="4ee1e-114">Création d’une fonction de réinitialisation</span><span class="sxs-lookup"><span data-stu-id="4ee1e-114">Creating a reset function</span></span>
<span data-ttu-id="4ee1e-115">Votre première tâche consiste à créer un blueprint de fonction qui remet une pièce d’échec à sa position d’origine dans la scène.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-115">Your first task is to create a function blueprint that resets a chess piece to its original position in the scene.</span></span> 

1.  <span data-ttu-id="4ee1e-116">Ouvrez **WhiteKing**, cliquez sur l’icône **+** en regard de la section **Functions** de **My Blueprint**, puis nommez-la **Reset Location**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-116">Open **WhiteKing**, click the **+** icon next to the **Functions** section in the **My Blueprint** and name it **Reset Location**.</span></span> 

2.  <span data-ttu-id="4ee1e-117">Faites glisser l’exécution de **Drag and release** vers la grille Blueprint pour créer un nœud **SetActorRelativeTransform**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-117">Drag and release the execution from **Reset Location** on the Blueprint grid to create a **SetActorRelativeTransform** node.</span></span> 
    * <span data-ttu-id="4ee1e-118">Cette fonction définit la transformation (position, rotation et échelle) d’un acteur par rapport à son parent.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-118">This function sets the transform (location, rotation, and scale) of an actor relative to its parent.</span></span> <span data-ttu-id="4ee1e-119">Vous allez utiliser cette fonction pour réinitialiser la position du roi sur l’échiquier, même si celui-ci a été déplacé de sa position d’origine.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-119">You’ll use this function to reset the king’s position on the board, even if the board has been moved from its original position.</span></span> 
    
3. <span data-ttu-id="4ee1e-120">Cliquez avec le bouton droit dans le graphique d’événements, sélectionnez **Make Transform**, puis déplacez-le en définissant le paramètre **Location** comme suit : **X =-26**, **Y = 4**, **Z = 0**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-120">Right-click inside the Event Graph, select **Make Transform**, and change its **Location** to **X = -26**, **Y = 4**, **Z = 0**.</span></span>
    * <span data-ttu-id="4ee1e-121">Connectez sa valeur de retour (**Return Value**) au repère **New Relative Transform** dans **SetActorRelativeTransform**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-121">Connect its **Return Value** to the **New Relative Transform** pin in **SetActorRelativeTransform**.</span></span> 

![Fonction Reset Location](images/unreal-uxt/5-function.PNG)

<span data-ttu-id="4ee1e-123">**Compilez** et **enregistrez** le projet avant de revenir à la fenêtre principale.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-123">**Compile** and **Save** the project before returning to the Main window.</span></span> 


## <a name="adding-a-button"></a><span data-ttu-id="4ee1e-124">Ajouter un bouton</span><span class="sxs-lookup"><span data-stu-id="4ee1e-124">Adding a button</span></span>
<span data-ttu-id="4ee1e-125">Maintenant que la fonction est correctement configurée, la tâche suivante consiste à créer un bouton qui la déclenche quand le joueur appuie dessus.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-125">Now that the function is setup correctly, your next task is to create a button that fires it off when touched.</span></span> 

1.  <span data-ttu-id="4ee1e-126">Cliquez sur **Add New > Blueprint Class**, développez la section **All Classes**, puis recherchez **SimpleButton**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-126">Click **Add New > Blueprint Class**, expand the **All Classes** section, and search for **SimpleButton**.</span></span> 
    * <span data-ttu-id="4ee1e-127">Nommez ce bouton **ResetButton** et double-cliquez pour ouvrir le blueprint.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-127">Name it **ResetButton** and double click to open the Blueprint</span></span>

> [!NOTE]
> <span data-ttu-id="4ee1e-128">**SimpleButton** est un bouton 3D d’un acteur Blueprint qui est intégré au plug-in UX Tools.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-128">**SimpleButton** is a 3D button Blueprint Actor that's part of the UX Tools plugin.</span></span> <span data-ttu-id="4ee1e-129">.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-129">.</span></span> 

![Nouveau Blueprint dérivé de la classe SimpleButton](images/unreal-uxt/5-subclass.PNG)

2. <span data-ttu-id="4ee1e-131">Cliquez sur **Pressable Button (Inherited)** dans le panneau **Components** et faites défiler le volet **Details** jusqu’à la section **Events**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-131">Click **Pressable Button (Inherited)** from the **Components** panel and scroll down the **Details** panel to the **Events** section.</span></span> 
    * <span data-ttu-id="4ee1e-132">Cliquez sur le bouton vert **+** à côté de **On Button Pressed** pour ajouter un événement au graphique d’événements, qui est appelé quand le joueur appuie sur le bouton.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-132">Click the green **+** button next to **On Button Pressed** to add an event to the Event Graph, which will be called when the button is pressed.</span></span> 
    
<span data-ttu-id="4ee1e-133">À partir de là, vous devez appeler la fonction **Reset Location** de **WhiteKing**, qui a besoin d’une référence à l’acteur **WhiteKing** dans le niveau.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-133">From here, you’ll want to call **WhiteKing**’s **Reset Location** function, which needs a reference to the **WhiteKing** Actor in the Level.</span></span> 

1.  <span data-ttu-id="4ee1e-134">Accédez à la section **Variables** du panneau **Details**, cliquez sur le bouton **+** , puis nommez la variable **WhiteKing**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-134">Scroll to the **Variables** section in the **Details** panel, click the **+** button and name the variable **WhiteKing**.</span></span> 
    * <span data-ttu-id="4ee1e-135">Sélectionnez la liste déroulante à côté de **Variable Type**, recherchez **WhiteKing**, puis sélectionnez **Object Reference**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-135">Select the dropdown next to **Variable Type**, search for **WhiteKing**, and select the **Object Reference**.</span></span> 
    * <span data-ttu-id="4ee1e-136">Cochez la case à côté de **Instance Editable**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-136">Check the box next to **Instance Editable**.</span></span> <span data-ttu-id="4ee1e-137">Cela permettra de définir la variable à partir du niveau principal (Main).</span><span class="sxs-lookup"><span data-stu-id="4ee1e-137">This will allow the variable to be set from the Main Level.</span></span> 

![Créer une variable](images/unreal-uxt/5-var.PNG)

2.  <span data-ttu-id="4ee1e-139">Faites glisser la variable WhiteKing de **My Blueprint > Variables** vers le graphique d’événements de Reset Button et choisissez **Get WhiteKing**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-139">Drag the WhiteKing variable from **My Blueprint > Variables** onto the Reset Button Event Graph and choose **Get WhiteKing**.</span></span> 

## <a name="firing-the-function"></a><span data-ttu-id="4ee1e-140">Déclenchement de la fonction</span><span class="sxs-lookup"><span data-stu-id="4ee1e-140">Firing the function</span></span>
<span data-ttu-id="4ee1e-141">Il ne reste plus qu’à déclencher expressément la fonction de réinitialisation dès lors que le joueur appuie sur le bouton.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-141">All that's left is to officially fire off the reset function when the button is pressed.</span></span>

1.  <span data-ttu-id="4ee1e-142">Faites glisser la broche de sortie WhiteKing et relâchez-la pour placer un nouveau nœud.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-142">Drag the WhiteKing output pin and release to place a new node.</span></span> <span data-ttu-id="4ee1e-143">Sélectionnez la fonction **Reset Location**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-143">Select the **Reset Location** function.</span></span> <span data-ttu-id="4ee1e-144">Pour finir, faites glisser la broche d’exécution sortante depuis **On Button Pressed** vers la broche d’exécution entrante sur **Reset Location**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-144">Finally, drag the outgoing execution pin from **On Button Pressed** to the incoming execution pin on **Reset Location**.</span></span> <span data-ttu-id="4ee1e-145">**Compilez** et **enregistrez** le Blueprint ResetButton, puis revenez dans la fenêtre principale.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-145">**Compile** and **Save** the ResetButton Blueprint, then return to the Main window.</span></span> 

![Appeler la fonction Reset Location à partir de l’événement On Button Pressed](images/unreal-uxt/5-callresetloc.PNG)

2.  <span data-ttu-id="4ee1e-147">Faites glisser **ResetButton** vers la fenêtre Viewport et définissez son emplacement sur **X = 50**, **Y = -25** et **Z = 10**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-147">Drag **ResetButton** into the viewport and set its location to **X = 50**, **Y = -25**, and **Z = 10**.</span></span> <span data-ttu-id="4ee1e-148">Sous **Default**, attribuez à la variable **WhiteKing** la valeur **WhiteKing**.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-148">Under **Default**, set the value of the **WhiteKing** variable to **WhiteKing**.</span></span>

![Définir la variable](images/unreal-uxt/5-buttonlevel.PNG)

<span data-ttu-id="4ee1e-150">Exécutez l’application, déplacez la pièce d’échec vers son nouvel emplacement, puis appuyez sur le gros bouton rose pour voir la logique de réinitialisation en action.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-150">Run the app, move the chess piece to a new location, and press the big pink button to see the reset logic in action!</span></span>

<span data-ttu-id="4ee1e-151">Votre application de réalité mixte comporte maintenant un échiquier et une pièce avec laquelle vous pouvez interagir, ainsi qu’un bouton entièrement opérationnel qui réinitialise l’emplacement de la pièce.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-151">You now have a mixed reality app with a chess piece and board that you can interact with, as well as a fully functioning button that will reset the piece’s location.</span></span> <span data-ttu-id="4ee1e-152">Vous trouverez l’application à ce stade d’avancement dans son dépôt [GitHub](https://github.com/microsoft/MixedReality-Unreal-Samples/tree/master/ChessApp).</span><span class="sxs-lookup"><span data-stu-id="4ee1e-152">You can find the completed app up to this point in its [GitHub](https://github.com/microsoft/MixedReality-Unreal-Samples/tree/master/ChessApp) repo.</span></span> <span data-ttu-id="4ee1e-153">N’hésitez pas à aller au-delà de ce tutoriel et à configurer les autres pièces du jeu d’échecs en faisant en sorte que l’échiquier se réinitialise entièrement quand le joueur appuie sur le bouton.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-153">Feel free to go beyond this tutorial and set up the remainder of the chess pieces so that the entire board is reset when the button is pressed.</span></span>

![Scène finale dans la fenêtre Viewport](images/unreal-uxt/5-endscene.PNG)

<span data-ttu-id="4ee1e-155">Vous êtes prêt à passer à la dernière section de ce tutoriel, dans laquelle vous allez apprendre à empaqueter et déployer correctement l’application sur un appareil ou un émulateur.</span><span class="sxs-lookup"><span data-stu-id="4ee1e-155">You're ready to move on to the final section of this tutorial where you'll learn how to correctly package and deploy the app to a device or emulator.</span></span>

[<span data-ttu-id="4ee1e-156">Section suivante : 6. Empaquetage et déploiement sur un appareil ou un émulateur</span><span class="sxs-lookup"><span data-stu-id="4ee1e-156">Next Section: 6. Packaging & deploying to device or emulator</span></span>](unreal-uxt-ch6.md)
