---
title: Didacticiels Azure Speech Services-3. Ajout du composant Azure Cognitive Services Speech translation
description: Suivez ce cours pour apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: c7cbdca3c22253042a9be44a194fca8925f0f446
ms.sourcegitcommit: 599bbdd861ce6ff11b6cfb345a0a995f8b7bf85b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68977965"
---
# <a name="3-adding-the-azure-cognitive-services-speech-translation-component"></a><span data-ttu-id="5ae78-105">3. Ajout du composant Azure Cognitive Services Speech translation</span><span class="sxs-lookup"><span data-stu-id="5ae78-105">3. Adding the Azure Cognitive Services speech translation component</span></span>

<span data-ttu-id="5ae78-106">Dans ce didacticiel, nous allons découvrir le composant Azure Cognitive Services Speech translation dans notre projet et le traduire en trois langages différents.</span><span class="sxs-lookup"><span data-stu-id="5ae78-106">In this tutorial, we learn about the Azure Cognitive Services Speech Translation component in our project as well as translate into three different languages.</span></span> 

## <a name="instructions"></a><span data-ttu-id="5ae78-107">Instructions</span><span class="sxs-lookup"><span data-stu-id="5ae78-107">Instructions</span></span>

1. <span data-ttu-id="5ae78-108">Sélectionnez l’objet Lunarcom_Base dans la hiérarchie, puis cliquez sur Ajouter un composant dans le panneau Inspecteur.</span><span class="sxs-lookup"><span data-stu-id="5ae78-108">Select the Lunarcom_Base object in the hierarchy, and click Add Component in the inspector panel.</span></span> <span data-ttu-id="5ae78-109">Recherchez et sélectionnez LunarcomTranslationRecognizer.</span><span class="sxs-lookup"><span data-stu-id="5ae78-109">Search for and select LunarcomTranslationRecognizer.</span></span>

![Module4Chapter3step1im](images/module4chapter3step1im.PNG)

> <span data-ttu-id="5ae78-111">Remarque : Assurez-vous que le simulateur en mode hors connexion est désactivé avant de tester le traducteur Speech-SDK.</span><span class="sxs-lookup"><span data-stu-id="5ae78-111">Note: Ensure the offline mode simulator is disabled before testing the Speech-SDK translator.</span></span> <span data-ttu-id="5ae78-112">Pour pouvoir effectuer la conversion, vous devez être connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="5ae78-112">In order to translate, you must be connected to the internet.</span></span> <span data-ttu-id="5ae78-113">Consultez l’image ci-dessous, où trouver ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="5ae78-113">See image below on where to find this setting.</span></span> 
>
> ![Module4Chapter3noteim](images/module4chapter3noteim.PNG)

2. <span data-ttu-id="5ae78-115">Cliquez sur la liste déroulante dans LunarcomTranslationRecognizer, puis sélectionnez la langue vers laquelle vous souhaitez effectuer la conversion.</span><span class="sxs-lookup"><span data-stu-id="5ae78-115">Click the drop-down in the LunarcomTranslationRecognizer, and select the language you would like to translate to.</span></span>

![Module4Chapter3step2im](images/module4chapter3step2im.PNG)

3. <span data-ttu-id="5ae78-117">À présent, exécutez l’application et testez le convertisseur en cliquant sur le bouton satellite, puis commencez à parler.</span><span class="sxs-lookup"><span data-stu-id="5ae78-117">Now, run the application and test the translator by clicking the Satellite button, and begin speaking.</span></span> <span data-ttu-id="5ae78-118">Appuyez de nouveau sur le bouton satellite pour arrêter la reconnaissance.</span><span class="sxs-lookup"><span data-stu-id="5ae78-118">Press the Satellite button again to stop the recognition.</span></span> <span data-ttu-id="5ae78-119">Vous trouverez ci-dessous un exemple de ce à quoi doit ressembler votre scène.</span><span class="sxs-lookup"><span data-stu-id="5ae78-119">Below is an example of what your scene should look like.</span></span> <span data-ttu-id="5ae78-120">N’hésitez pas à modifier la langue sous la liste déroulante «langue cible» (Voir l’image ci-dessus) pour explorer la traduction dans d’autres langues.</span><span class="sxs-lookup"><span data-stu-id="5ae78-120">Feel free to change the language under the "Target Language" dropdown (see image above) to explore translation into other languages.</span></span>

> <span data-ttu-id="5ae78-121">Remarque : Avant de procéder à des tests, assurez-vous que le simulateur hors connexion est désactivé, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5ae78-121">Note: Before testing, ensure that the offline simulator is disabled, as shown in the image below.</span></span>
>
> ![Module4Chapter3noteim](images/module4chapter3noteim.PNG)

<span data-ttu-id="5ae78-123">Vous trouverez ci-dessous un exemple de ce à quoi votre scène devrait ressembler:</span><span class="sxs-lookup"><span data-stu-id="5ae78-123">Below is an example of what your scene should look like:</span></span>

![Module4Chapter3exampleim](images/module4chapter3exampleim.PNG)

## <a name="congratulations"></a><span data-ttu-id="5ae78-125">Félicitations</span><span class="sxs-lookup"><span data-stu-id="5ae78-125">Congratulations</span></span>

<span data-ttu-id="5ae78-126">À présent, votre projet peut traduire les mots que vous parlez dans plusieurs langues différentes.</span><span class="sxs-lookup"><span data-stu-id="5ae78-126">Now your project can translate the words you speak into several different languages.</span></span> <span data-ttu-id="5ae78-127">N’hésitez pas à vous amuser avec les langages et à tester l’exactitude de la traduction.</span><span class="sxs-lookup"><span data-stu-id="5ae78-127">Feel free to play around with the languages, and test the accuracy of the translation.</span></span> 

[<span data-ttu-id="5ae78-128">Didacticiel suivant: 4. Configuration des intentions et compréhension du langage naturel</span><span class="sxs-lookup"><span data-stu-id="5ae78-128">Next tutorial: 4. Setting up intent and natural language understanding</span></span>](mrlearning-speechSDK-ch4.md)

