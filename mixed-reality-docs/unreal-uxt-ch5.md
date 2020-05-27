---
title: 5. Ajout d’un bouton et réinitialisation des positions des pièces
description: Partie 5 d’un tutoriel pour créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in UX Tools du Mixed Reality Toolkit
author: sw5813
ms.author: suwu
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: df5ea22e7097fdd3b788ec298bc1cd78c315b585
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82840398"
---
# <a name="5-adding-a-button--resetting-piece-locations"></a><span data-ttu-id="6a6ab-104">5. Ajout d’un bouton et réinitialisation des positions des pièces</span><span class="sxs-lookup"><span data-stu-id="6a6ab-104">5. Adding a button & resetting piece locations</span></span>

<span data-ttu-id="6a6ab-105">Cette section continue la présentation des fonctionnalités du plug-in UX Tools du Mixed Reality Toolkit et le développement des fonctionnalités de votre application de jeu d’échecs.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-105">This section continues demonstrating the capabilities of the Mixed Reality Toolkit UX Tools plugin and building out the features of your chess app.</span></span> <span data-ttu-id="6a6ab-106">Vous allez créer une autre fonction et apprendre à obtenir des références aux acteurs de votre niveau dans un Blueprint.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-106">You’ll create a new function and learn how to get references to Actors from your Level into a Blueprint.</span></span>

## <a name="objectives"></a><span data-ttu-id="6a6ab-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="6a6ab-107">Objectives</span></span>

* <span data-ttu-id="6a6ab-108">Ajouter un bouton à votre projet</span><span class="sxs-lookup"><span data-stu-id="6a6ab-108">Add a button to your project</span></span>
* <span data-ttu-id="6a6ab-109">Créer une fonction « Reset Location » qui remet une pièce à sa position d’origine</span><span class="sxs-lookup"><span data-stu-id="6a6ab-109">Create a new “Reset Location” function that sends a piece back to its original location</span></span>
* <span data-ttu-id="6a6ab-110">Lier le bouton pour déclencher la nouvelle fonction quand l’utilisateur appuie dessus</span><span class="sxs-lookup"><span data-stu-id="6a6ab-110">Hook the button up to trigger the newly created function when pressed</span></span>

## <a name="create-a-function-to-reset-location"></a><span data-ttu-id="6a6ab-111">Créer une fonction pour réinitialiser la position</span><span class="sxs-lookup"><span data-stu-id="6a6ab-111">Create a function to reset location</span></span>

1.  <span data-ttu-id="6a6ab-112">Ouvrez **WhiteKing**.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-112">Open **WhiteKing**.</span></span> <span data-ttu-id="6a6ab-113">Dans le panneau **My Blueprint**, cliquez sur le bouton « + » en regard de la section **Functions** pour créer une fonction.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-113">In the **My Blueprint** panel, click the “+” button next to the **Functions** section to create a new function.</span></span> <span data-ttu-id="6a6ab-114">Nommez cette fonction « Reset Location ».</span><span class="sxs-lookup"><span data-stu-id="6a6ab-114">Name this function “Reset Location”.</span></span> 

2.  <span data-ttu-id="6a6ab-115">Dans le Blueprint **Reset Location** que vous venez de créer, faites glisser la broche d’exécution et relâchez-la n’importe où sur la grille du Blueprint pour appeler un nœud **SetActorRelativeTransform**.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-115">In your newly created **Reset Location** Blueprint, drag the execution pin and release anywhere on the Blueprint grid to call a **SetActorRelativeTransform** node.</span></span> <span data-ttu-id="6a6ab-116">Cette fonction définit la transformation (position, rotation et échelle) d’un acteur par rapport à son parent.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-116">This function sets the transform (location, rotation, and scale) of an actor relative to its parent.</span></span> <span data-ttu-id="6a6ab-117">Nous allons utiliser cette fonction pour réinitialiser la position du roi sur l’échiquier, même si celui-ci a été déplacé de sa position d’origine.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-117">We’ll use this function to reset the king’s position on the board, even if the board has been moved from its original position.</span></span> <span data-ttu-id="6a6ab-118">Créez un nœud **Make Transform** avec la position X = -26, Y = 4, Z = 0, et reliez-le à l’entrée New Relative Transform.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-118">Create a **Make Transform** node with Location X = -26, Y = 4, Z = 0, and connect it to the New Relative Transform input.</span></span> 

![Fonction Reset Location](images/unreal-uxt/5-function.PNG)

3.  <span data-ttu-id="6a6ab-120">Compilez et enregistrez **WhiteKing**.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-120">Compile and Save **WhiteKing**.</span></span> <span data-ttu-id="6a6ab-121">Revenez dans la fenêtre principale.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-121">Return to the Main window.</span></span> 

## <a name="add-a-button"></a><span data-ttu-id="6a6ab-122">Ajouter un bouton</span><span class="sxs-lookup"><span data-stu-id="6a6ab-122">Add a button</span></span>

1.  <span data-ttu-id="6a6ab-123">Dans votre dossier **Blueprints**, créez un Blueprint dérivé de la classe SimpleButton.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-123">In your **Blueprints** folder, create a new Blueprint that subclasses SimpleButton.</span></span> <span data-ttu-id="6a6ab-124">SimpleButton est un bouton 3D d’un acteur Blueprint qui est fourni dans le plug-in UX Tools.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-124">SimpleButton is a 3D button Blueprint Actor that is provided as part of the UX Tools plugin.</span></span> <span data-ttu-id="6a6ab-125">Nommez ce bouton « ResetButton » et double-cliquez pour ouvrir le Blueprint.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-125">Name this button “ResetButton” and double click to open the Blueprint.</span></span> 

![Nouveau Blueprint dérivé de la classe SimpleButton](images/unreal-uxt/5-subclass.PNG)

2.  <span data-ttu-id="6a6ab-127">Dans le volet **Components**, cliquez sur **PressableButton (Inherited)** .</span><span class="sxs-lookup"><span data-stu-id="6a6ab-127">In the **Components** panel, click on **PressableButton (Inherited)**.</span></span> <span data-ttu-id="6a6ab-128">Dans le volet Details, faites défiler le contenu jusqu’à la section **Events**.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-128">In the Details panel, scroll until you see the **Events** section.</span></span> <span data-ttu-id="6a6ab-129">Cliquez sur le bouton plus vert à côté de **On Button Pressed**. Cette action ajoute un événement **On Button Pressed** à l’Event Graph, qui est appelé quand l’utilisateur appuie sur le bouton.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-129">Click the green plus button next to **On Button Pressed**- this will add an **On Button Pressed** event to the Event Graph, which will be called when the button is pressed.</span></span> <span data-ttu-id="6a6ab-130">Maintenant, nous voulons appeler la fonction Reset Location de WhiteKing.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-130">From here, we’ll want to call our WhiteKing’s Reset Location function.</span></span> <span data-ttu-id="6a6ab-131">Pour ce faire, nous devons d’abord obtenir une référence à l’acteur WhiteKing dans notre niveau.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-131">To do this, we’ll first need to get a reference to the WhiteKing Actor in our Level.</span></span> 

3.  <span data-ttu-id="6a6ab-132">Dans le volet **My Blueprint**, recherchez la section **Variables**, puis cliquez sur le bouton **+** pour ajouter une nouvelle variable.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-132">In the **My Blueprint** panel, find the **Variables** section and click the **+** button to add a new variable.</span></span> <span data-ttu-id="6a6ab-133">Nommez cette variable « WhiteKing ».</span><span class="sxs-lookup"><span data-stu-id="6a6ab-133">Name this variable “WhiteKing”.</span></span> <span data-ttu-id="6a6ab-134">Dans le volet Details, sélectionnez la liste déroulante à côté de **Variable Type**, recherchez « WhiteKing », puis sélectionnez **Object Reference**.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-134">In the Details panel, select the dropdown next to **Variable Type**, search for “WhiteKing”, and select the **Object Reference**.</span></span> <span data-ttu-id="6a6ab-135">Enfin, cochez la case **Instance Editable**.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-135">Finally, check the box next to **Instance Editable**.</span></span> <span data-ttu-id="6a6ab-136">Cela permettra de définir la variable à partir du niveau principal (Main).</span><span class="sxs-lookup"><span data-stu-id="6a6ab-136">This will allow the variable to be set from the Main Level.</span></span> 

![Créer une variable](images/unreal-uxt/5-var.PNG)

4.  <span data-ttu-id="6a6ab-138">Faites glisser la variable WhiteKing depuis **My Blueprint > Variables** vers l’Event Graph de Simple Button.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-138">Drag the WhiteKing variable from **My Blueprint > Variables** onto the Simple Button Event Graph.</span></span> <span data-ttu-id="6a6ab-139">Choisissez **Get WhiteKing**.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-139">Choose **Get WhiteKing**.</span></span> 

5.  <span data-ttu-id="6a6ab-140">Faites glisser la broche de sortie WhiteKing et relâchez-la pour placer un nouveau nœud.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-140">Drag the WhiteKing output pin and release to place a new node.</span></span> <span data-ttu-id="6a6ab-141">Sélectionnez la fonction **Reset Location**.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-141">Select the **Reset Location** function.</span></span> <span data-ttu-id="6a6ab-142">Pour finir, faites glisser la broche d’exécution sortante depuis **On Button Pressed** vers la broche d’exécution entrante sur **Reset Location**.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-142">Finally, drag the outgoing execution pin from **On Button Pressed** to the incoming execution pin on **Reset Location**.</span></span> <span data-ttu-id="6a6ab-143">**Compilez** et **enregistrez** le Blueprint ResetButton, puis revenez dans la fenêtre principale.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-143">**Compile** and **Save** the ResetButton Blueprint, then return to the Main window.</span></span> 

![Appeler la fonction Reset Location à partir de l’événement On Button Pressed](images/unreal-uxt/5-callresetloc.PNG)

6.  <span data-ttu-id="6a6ab-145">Faites glisser **SimpleButton** vers la fenêtre Viewport et définissez sa position sur X = 50, Y = -25, Z = 10.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-145">Drag **SimpleButton** into the viewport and set its location to X = 50, Y = -25, Z = 10.</span></span> <span data-ttu-id="6a6ab-146">Sous **Default**, définissez la valeur de la variable WhiteKing sur **WhiteKing**.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-146">Under **Default**, set the value of the WhiteKing variable to **WhiteKing**.</span></span>

![Définir la variable](images/unreal-uxt/5-buttonlevel.PNG)

<span data-ttu-id="6a6ab-148">Votre application de réalité mixte comporte maintenant un échiquier et une pièce saisissable, ainsi qu’un bouton opérationnel qui réinitialise la position de la pièce quand l’utilisateur appuie dessus.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-148">You now have a mixed reality app with a grabbable chess piece and board, as well as a fully functioning button that will reset the piece’s location when pressed.</span></span> <span data-ttu-id="6a6ab-149">L’application terminée à ce stade est disponible sur [GitHub](https://github.com/microsoft/MixedReality-Unreal-Samples/tree/master/ChessApp).</span><span class="sxs-lookup"><span data-stu-id="6a6ab-149">The completed app up to this point can be found on [GitHub](https://github.com/microsoft/MixedReality-Unreal-Samples/tree/master/ChessApp).</span></span> <span data-ttu-id="6a6ab-150">N’hésitez pas à aller plus loin que ce tutoriel et à configurer toutes les autres pièces du jeu d’échecs afin que leurs positions sur l’échiquier soient réinitialisées lorsque l’utilisateur appuie sur le bouton.</span><span class="sxs-lookup"><span data-stu-id="6a6ab-150">Feel free to go beyond this tutorial and set up the remainder of the chess pieces, so that the entire board is reset when the user presses the button.</span></span>

![Scène finale dans la fenêtre Viewport](images/unreal-uxt/5-endscene.PNG)

[<span data-ttu-id="6a6ab-152">Section suivante : 6. Empaquetage et déploiement sur un appareil ou un émulateur</span><span class="sxs-lookup"><span data-stu-id="6a6ab-152">Next Section: 6. Packaging & deploying to device or emulator</span></span>](unreal-uxt-ch6.md)