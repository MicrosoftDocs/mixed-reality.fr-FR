---
title: Tutoriels sur les services Azure Speech - 3. Ajout du composant de traduction vocale Azure Cognitive Services
description: Dans ce cours, vous allez apprendre à implémenter le SDK Azure Speech au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: d8e73e24f0522ff71b95ea1886d59893216b0597
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "79028346"
---
# <a name="3-adding-the-azure-cognitive-services-speech-translation-component"></a><span data-ttu-id="dbb9d-105">3. Ajout du composant de traduction vocale Azure Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="dbb9d-105">3. Adding the Azure Cognitive Services speech translation component</span></span>

<span data-ttu-id="dbb9d-106">Dans ce tutoriel, vous allez ajouter la traduction vocale à votre projet, ce qui va vous permettre de traduire et transcrire votre parole en trois langues différentes.</span><span class="sxs-lookup"><span data-stu-id="dbb9d-106">In this tutorial, you will add speech translation to your project which will allow you to translate and transcribed your speech into three different languages.</span></span>

## <a name="objectives"></a><span data-ttu-id="dbb9d-107">Objectifs</span><span class="sxs-lookup"><span data-stu-id="dbb9d-107">Objectives</span></span>

* <span data-ttu-id="dbb9d-108">Apprendre à intégrer la traduction vocale Azure</span><span class="sxs-lookup"><span data-stu-id="dbb9d-108">Learn how to integrate Azure speech translation</span></span>

## <a name="instructions"></a><span data-ttu-id="dbb9d-109">Instructions</span><span class="sxs-lookup"><span data-stu-id="dbb9d-109">Instructions</span></span>

<span data-ttu-id="dbb9d-110">Dans la fenêtre Hierachy, sélectionnez l’objet **Lunarcom** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Lunarcom Translation Recognizer (Script)** à l’objet Lunarcom et configurez-le de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="dbb9d-110">In the Hierarchy window, select the **Lunarcom** object, then in the Inspector window, use the **Add Component** button to add the **Lunarcom Translation Recognizer (Script)** component to the Lunarcom object and configure it as follows:</span></span>

* <span data-ttu-id="dbb9d-111">Remplacez la valeur de **Target Language** par la langue de votre choix, par exemple, _German_.</span><span class="sxs-lookup"><span data-stu-id="dbb9d-111">Change the **Target Language** to a language of your choosing, for example, _German_</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial3-section1-step1-1.png)

> [!NOTE]
> <span data-ttu-id="dbb9d-113">Le composant Lunarcom Translation Recognizer (Script) ne fait pas partie de MRTK.</span><span class="sxs-lookup"><span data-stu-id="dbb9d-113">The Lunarcom Translation Recognizer (Script) component is not part of MRTK.</span></span> <span data-ttu-id="dbb9d-114">Il a été fourni avec les ressources de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="dbb9d-114">It was provided with this tutorial's assets.</span></span>

<span data-ttu-id="dbb9d-115">Si vous entrez maintenant en mode Game, vous pouvez tester la traduction vocale en commençant par appuyer sur le bouton du satellite.</span><span class="sxs-lookup"><span data-stu-id="dbb9d-115">If you now enter Game mode, you can test the speech translation by first pressing the satellite button.</span></span> <span data-ttu-id="dbb9d-116">Ensuite, en supposant que votre ordinateur est doté d’un microphone, quand vous dites quelque chose, votre parole est traduite dans la langue choisie et transcrite sur le panneau du terminal :</span><span class="sxs-lookup"><span data-stu-id="dbb9d-116">Then, assuming your computer has a microphone, when you say something, your speech will be translated into the chosen language and transcribed on the terminal panel:</span></span>

![mrlearning-speech](images/mrlearning-speech/tutorial3-section1-step1-2.png)

> [!CAUTION]
> <span data-ttu-id="dbb9d-118">L’application a besoin de se connecter à Azure, donc vérifiez que votre ordinateur/appareil est connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="dbb9d-118">The application needs to connect to Azure, so make sure your computer/device is connected to the internet.</span></span>

## <a name="congratulations"></a><span data-ttu-id="dbb9d-119">Félicitations</span><span class="sxs-lookup"><span data-stu-id="dbb9d-119">Congratulations</span></span>

<span data-ttu-id="dbb9d-120">Votre projet peut maintenant traduire correctement les mots que vous dites dans plusieurs langues différentes.</span><span class="sxs-lookup"><span data-stu-id="dbb9d-120">Your project can now successfully translate the words you speak into several different languages.</span></span> <span data-ttu-id="dbb9d-121">Exécutez l’application sur votre appareil pour vérifier que tout fonctionne bien.</span><span class="sxs-lookup"><span data-stu-id="dbb9d-121">Run the application on your device to ensure the feature is working properly.</span></span>

[<span data-ttu-id="dbb9d-122">Tutoriel suivant : 4. Configuration des intentions et compréhension du langage naturel</span><span class="sxs-lookup"><span data-stu-id="dbb9d-122">Next tutorial: 4. Setting up intent and natural language understanding</span></span>](mrlearning-speechSDK-ch4.md)
