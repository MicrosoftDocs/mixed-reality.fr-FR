---
title: Tutoriels sur les services Azure Speech - 2. Ajout d’un mode hors connexion pour la traduction locale de la reconnaissance vocale
description: Suivez ce cours pour apprendre à implémenter le SDK Azure Speech au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 06/27/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 75ddce9063bb9d33f5fe2343fe30178222a5f8ac
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "79031631"
---
# <a name="2-using-speech-recognition-to-execute-commands"></a><span data-ttu-id="99536-105">2. Utilisation de la reconnaissance vocale pour exécuter des commandes</span><span class="sxs-lookup"><span data-stu-id="99536-105">2. Using speech recognition to execute commands</span></span>

<span data-ttu-id="99536-106">Dans ce tutoriel, vous allez ajouter la capacité d’exécuter des commandes en utilisant la reconnaissance vocale Azure, ce qui va vous permettre de déclencher une action en fonction du mot ou de l’expression que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="99536-106">In this tutorial, you will add the ability to execute commands using Azure speech recognition which will allow you to make something happen based on the word or phrase you define.</span></span>

## <a name="objectives"></a><span data-ttu-id="99536-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="99536-107">Objectives</span></span>

* <span data-ttu-id="99536-108">Découvrir comment la reconnaissance vocale Azure peut être utilisée pour exécuter des commandes</span><span class="sxs-lookup"><span data-stu-id="99536-108">Learn how Azure speech recognition can be used to execute commands</span></span>

## <a name="instructions"></a><span data-ttu-id="99536-109">Instructions</span><span class="sxs-lookup"><span data-stu-id="99536-109">Instructions</span></span>

<span data-ttu-id="99536-110">Dans la fenêtre Hierachy, sélectionnez l’objet **Lunarcom** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Lunarcom Wake Word Recognizer (Script)** à l’objet Lunarcom et configurez-le de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="99536-110">In the Hierarchy window, select the **Lunarcom** object, then in the Inspector window, use the **Add Component** button to add the **Lunarcom Wake Word Recognizer (Script)** component to the Lunarcom object and configure it as follows:</span></span>

* <span data-ttu-id="99536-111">Dans le champ **Wake Word**, entrez une expression appropriée, par exemple, _Activer le terminal_.</span><span class="sxs-lookup"><span data-stu-id="99536-111">In the **Wake Word** field, enter a suitable phrase, for example, _Activate terminal_.</span></span>
* <span data-ttu-id="99536-112">Dans le champ **Dismiss Word**, entrez une expression appropriée, par exemple, _Désactiver le terminal_.</span><span class="sxs-lookup"><span data-stu-id="99536-112">In the **Dismiss Word** field, enter a suitable phrase, for example, _Dismiss terminal_.</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial2-section1-step1-1.png)

> [!NOTE]
> <span data-ttu-id="99536-114">Le composant Lunarcom Wake Word Recognizer (Script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="99536-114">The Lunarcom Wake Word Recognizer (Script) component is not part of MRTK.</span></span> <span data-ttu-id="99536-115">Il a été fourni avec les ressources de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="99536-115">It was provided with this tutorial's assets.</span></span>

<span data-ttu-id="99536-116">Si vous entrez maintenant en mode Game, comme dans le tutoriel précédent, le panneau du terminal est activé par défaut, mais vous pouvez maintenant le désactiver en prononçant la valeur de Dismiss Word, **Désactiver le terminal** :</span><span class="sxs-lookup"><span data-stu-id="99536-116">If you now enter Game mode, as in the previous tutorial, the terminal panel is enabled by default, but you can now disable it by saying the Dismiss Word, **Dismiss terminal**:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial2-section1-step1-2.png)

<span data-ttu-id="99536-118">Et réactivez-le en prononçant la valeur de Wake Word, à savoir **Activer le terminal** :</span><span class="sxs-lookup"><span data-stu-id="99536-118">And enable it again by saying the Wake Word, **Activate terminal**:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial2-section1-step1-3.png)

> [!CAUTION]
> <span data-ttu-id="99536-120">L’application a besoin de se connecter à Azure, donc vérifiez que votre ordinateur/appareil est connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="99536-120">The application needs to connect to Azure, so make sure your computer/device is connected to the internet.</span></span>

> [!TIP]
> <span data-ttu-id="99536-121">Si vous prévoyez d’être souvent dans l’impossibilité de vous connecter à Azure, vous pouvez également implémenter des commandes vocales à l’aide de MRTK en suivant les instructions données dans [Activation des commandes vocales](mrlearning-base-ch5.md#enabling-voice-commands).</span><span class="sxs-lookup"><span data-stu-id="99536-121">If you anticipate frequently not being able to connect to Azure, you can also implement speech commands using MRTK by following the [Enabling Voice Commands](mrlearning-base-ch5.md#enabling-voice-commands) instructions.</span></span>

## <a name="congratulations"></a><span data-ttu-id="99536-122">Félicitations</span><span class="sxs-lookup"><span data-stu-id="99536-122">Congratulations</span></span>

<span data-ttu-id="99536-123">Vous avez implémenté des commandes vocales Azure.</span><span class="sxs-lookup"><span data-stu-id="99536-123">You have implemented speech commands powered by Azure.</span></span> <span data-ttu-id="99536-124">Exécutez l’application sur votre appareil pour vérifier que tout fonctionne bien.</span><span class="sxs-lookup"><span data-stu-id="99536-124">Run the application on your device to ensure the feature is working properly.</span></span>

<span data-ttu-id="99536-125">Dans le tutoriel suivant, vous allez apprendre à traduire la parole en utilisant la traduction vocale Azure.</span><span class="sxs-lookup"><span data-stu-id="99536-125">In the next tutorial, you will learn how to translate speech using Azure speech translation.</span></span>

[<span data-ttu-id="99536-126">Tutoriel suivant : 3. Ajout du composant de traduction vocale Azure Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="99536-126">Next Tutorial: 3. Adding the Azure Cognitive Services speech translation component</span></span>](mrlearning-speechSDK-ch3.md)
