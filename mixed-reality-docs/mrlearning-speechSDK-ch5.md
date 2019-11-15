---
title: Module d’apprentissage de SpeechSDK-reconnaissance vocale et transcription
description: Suivez ce cours pour apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: cf51505cab2db765325c2e7b78a52e4b790845c9
ms.sourcegitcommit: 781e47db2ca2f2c792c95e76ac309b44b3535555
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/15/2019
ms.locfileid: "74105954"
---
# <a name="speech-sdk-learning-module---rocket-launcher-control-using-speech-commands"></a><span data-ttu-id="af863-104">Module Speech SDK Learning-contrôle du lanceur Rocket utilisant des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="af863-104">Speech SDK Learning Module - Rocket Launcher Control Using Speech Commands</span></span>

<span data-ttu-id="af863-105">Dans cette leçon, nous allons utiliser la fonctionnalité d’intention du service Azure Speech pour comprendre l’objectif de la reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="af863-105">In this lesson, we will be using Azure Speech Service's Intent feature to understand the intent of the speech.</span></span> <span data-ttu-id="af863-106">Nous utiliserons l’intention de parole détectée comme commandes vocales pour contrôler le lanceur Rocket.</span><span class="sxs-lookup"><span data-stu-id="af863-106">We will be using the detected intent of speech as the voice commands to control the rocket launcher.</span></span> <span data-ttu-id="af863-107">Au cours de cette leçon, nous allons importer la ressource du lanceur Rocket et nous allons intermettre les commandes vocales intentionnelles détectées sur les boutons de contrôle prédéfinis pour contrôler la fusée.</span><span class="sxs-lookup"><span data-stu-id="af863-107">During this lesson, we will be importing the Rocket Launcher asset and We will interface the detected intent voice commands to predefined control buttons to control the rocket.</span></span>

## <a name="objectives"></a><span data-ttu-id="af863-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="af863-108">Objectives</span></span>

- <span data-ttu-id="af863-109">Découvrez comment connecter des intentions vocales en tant que commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="af863-109">Learn how to connect speech intent as voice commands.</span></span>
- <span data-ttu-id="af863-110">Découvrez comment utiliser les commandes vocales d’intention vocale comme commandes de contrôle de fusée.</span><span class="sxs-lookup"><span data-stu-id="af863-110">Learn how to use speech intent voice commands as rocket control input commands.</span></span>

## <a name="instructions"></a><span data-ttu-id="af863-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="af863-111">Instructions</span></span>

1. <span data-ttu-id="af863-112">Dans ce didacticiel, nous allons utiliser un élément multimédia « BaseModule » pour intégrer le lanceur Rocket avec les commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="af863-112">In this tutorial, we will be using a "BaseModule" asset to integrate rocket launcher with the speech commands.</span></span> <span data-ttu-id="af863-113">Pour ce faire, nous devons importer la ressource dans notre projet.</span><span class="sxs-lookup"><span data-stu-id="af863-113">For that, we need to import the asset into our project.</span></span> <span data-ttu-id="af863-114">Vous pouvez télécharger le composant « lanceur Rocket » à l’aide de ce [lien](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.1.0.0/Unity.HoloLens2.GettingStarted.Tutorials.Asset.2.1.0.0.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="af863-114">You can download the "Rocket Launcher" asset using this [link](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.1.0.0/Unity.HoloLens2.GettingStarted.Tutorials.Asset.2.1.0.0.unitypackage).</span></span>

2. <span data-ttu-id="af863-115">Pour importer l’élément multimédia, accédez à ressources-> Importer un package-> package personnalisé-> accédez au fichier téléchargé, puis cliquez sur Importer.</span><span class="sxs-lookup"><span data-stu-id="af863-115">To import the asset, please go to assets->Import package->Custom package-> navigate to the downloaded file and click import.</span></span>

    ![module4chapter5step1](images/module4chapter5step1.PNG)

3. <span data-ttu-id="af863-117">Après avoir importé le composant « ressources du module de base », naviguez dans le dossier « ressources du module de base »-> Prefabs-> sélectionnez « fusée Launcher_Complete », puis faites-le glisser vers la hiérarchie de la scène existante.</span><span class="sxs-lookup"><span data-stu-id="af863-117">After importing the  "Base Module Assets" asset, navigate inside the "Base Module Assets" folder->Prefabs-> Select "Rocket Launcher_Complete", and then drag and drop it into the existing scene Hierarchy.</span></span>

    ![module4chapter5step2](images/module4chapter5step2.PNG)

4. <span data-ttu-id="af863-119">Nous devons maintenant intégrer notre « lanceur Rocket » à notre projet LUIS que nous avons travaillé dans notre [leçon](mrlearning-speechSDK-ch4.md)précédente.</span><span class="sxs-lookup"><span data-stu-id="af863-119">Now we need to integrate our "Rocket Launcher" with our LUIS project that we worked in our previous lesson [lesson](mrlearning-speechSDK-ch4.md).</span></span> <span data-ttu-id="af863-120">Pour cela, développez le Prefab « fusée Launcher_Complete » dans la hiérarchie et recherchez les boutons « LaunchRoundButton », « ResetRoundButton » et « indicateurs de positionnement ».</span><span class="sxs-lookup"><span data-stu-id="af863-120">For that, expand the "Rocket Launcher_Complete" prefab in the hierarchy and find the "LaunchRoundButton", "ResetRoundButton" and "Placement Hints" buttons.</span></span>

    ![module4chapter5step3](images/module4chapter5step3.PNG)

5. <span data-ttu-id="af863-122">Sélectionnez « LaunchRoundButton » et dans le panneau de l’inspecteur, accédez à « interactive » et sous événements « OnClick () », faites glisser et déposez le Prefab « LunarModule ».</span><span class="sxs-lookup"><span data-stu-id="af863-122">Select "LaunchRoundButton" and in inspector panel, go to "Interactable" and under events "OnClick ()", drag and drop the "LunarModule" prefab.</span></span> <span data-ttu-id="af863-123">Sélectionnez ensuite la fonction déroulante et sélectionnez « LunarModule », puis accédez à la fonction « StartThruster () » et sélectionnez-la.</span><span class="sxs-lookup"><span data-stu-id="af863-123">Then, select the function drop down and select " LunarModule" and then navigate to "StartThruster()" function and select it.</span></span>

    ![module4chapter5step 3.0](images/module4chapter5step3.0.PNG)

    ![module4chapter5step3a](images/module4chapter5step3a.PNG)

6. <span data-ttu-id="af863-126">Sélectionnez « ResetRoundButton » et dans le panneau de l’inspecteur, accédez à « interactive » et sous événements « OnClick () », faites glisser et déposez le Prefab « LunarModule ».</span><span class="sxs-lookup"><span data-stu-id="af863-126">Select "ResetRoundButton" and in inspector panel, go to "Interactable" and under events "OnClick ()", drag and drop the "LunarModule" prefab.</span></span> <span data-ttu-id="af863-127">Sélectionnez ensuite la fonction déroulante et sélectionnez « LunarModule », puis accédez à la fonction « resetModule () » et sélectionnez-la.</span><span class="sxs-lookup"><span data-stu-id="af863-127">Then, select the function drop down and select " LunarModule" and then navigate to "resetModule()" function and select it.</span></span>

    ![module4chapter5step3b](images/module4chapter5step3b.PNG)

7. <span data-ttu-id="af863-129">Sélectionnez « indicateurs d’emplacement » et dans le panneau Inspecteur, accédez à « interactive » et sous événements « OnClick () », faites glisser et déposez le Prefab « LunarModule ».</span><span class="sxs-lookup"><span data-stu-id="af863-129">Select "Placement Hints" and in inspector panel, go to "Interactable" and under events "OnClick ()", drag and drop the "LunarModule" prefab.</span></span> <span data-ttu-id="af863-130">Ensuite, sélectionnez la liste déroulante de la fonction et sélectionnez « LunarModule », puis accédez à la fonction « TogglePlacementHints » et sélectionnez ToggleGameOBjects ().</span><span class="sxs-lookup"><span data-stu-id="af863-130">Then, select the function drop down and select " LunarModule" and then navigate to "TogglePlacementHints" function and select ToggleGameOBjects().</span></span>

    ![module4chapter5step3c](images/module4chapter5step3c.PNG)

8. <span data-ttu-id="af863-132">Ensuite, sélectionnez le Lunarcom_Completed Prefab dans la hiérarchie et accédez au script « Lunarcom intentr » dans Inspector, puis faites glisser et déposez les boutons « LaunchRoundButton », « ResetRoundButton » et « indicateurs de positionnement » à leurs emplacements respectifs.</span><span class="sxs-lookup"><span data-stu-id="af863-132">Next, Select the Lunarcom_Completed prefab in Hierarchy and navigate to "Lunarcom Intent Recognizer" script in Inspector and then drag and drop  "LaunchRoundButton", "ResetRoundButton" and "Placement Hints" buttons to their respective places.</span></span>

    ![module4chapter5step4](images/module4chapter5step4.PNG)

9. <span data-ttu-id="af863-134">Appuyez sur le bouton de lecture dans l’éditeur Unity et cliquez sur le bouton « Rocket » et indiquez les expressions telles que « pousser le bouton de lancement fusée », « afficher un indicateur de positionnement », « appuyer sur le bouton REST » ou toute autre expression relative au lancement, à la réinitialisation ou à l’indication du lanceur Rocket.</span><span class="sxs-lookup"><span data-stu-id="af863-134">Press the play button in Unity Editor and click on the "Rocket" button and utter the phrases like "Push rocket launch button","show me a placement hint", "press the rest button" or any other phrases related to launch, reset or hint's request for the rocket launcher.</span></span>

    ![module4chapter5step5a](images/module4chapter5step5a.PNG)

    ![module4chapter5step5b](images/module4chapter5step5b.PNG)

    ![module4chapter5step5c](images/module4chapter5step5c.PNG)

## <a name="congratulations"></a><span data-ttu-id="af863-138">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="af863-138">Congratulations</span></span>

<span data-ttu-id="af863-139">Dans cette leçon, nous avons appris comment connecter les commandes vocales en intelligence artificielle aux commandes vocales pour l’utiliser comme méthode d’entrée.</span><span class="sxs-lookup"><span data-stu-id="af863-139">In this lesson, we learned how to connect the AI-powered speech commands to voice commands to use it as an input method.</span></span> <span data-ttu-id="af863-140">À présent, notre programme peut utiliser l’intention des orateurs comme des commandes vocales pour fournir des entrées pour le lanceur Rocket.</span><span class="sxs-lookup"><span data-stu-id="af863-140">Now our program can use the speakers intent as voice commands to give inputs for the rocket launcher.</span></span>
