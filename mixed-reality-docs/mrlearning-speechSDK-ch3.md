---
title: Module d’apprentissage de SpeechSDK-reconnaissance vocale et transcription
description: Suivez ce cours pour apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: e5d0919a69c9e6b0c4233d23bf6d370f3def6576
ms.sourcegitcommit: c7c7e3c836373b65e319609b4e8389dea6b081de
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68460313"
---
# <a name="3----adding-the-azure-cognitive-services-speech-translation-component"></a><span data-ttu-id="527ab-104">3.    Ajout du composant Azure Cognitive Services Speech translation</span><span class="sxs-lookup"><span data-stu-id="527ab-104">3.    Adding the Azure Cognitive Services speech translation component</span></span>

<span data-ttu-id="527ab-105">Dans ce didacticiel, nous apprenons à aabout le composant Azure Cognitive Services Speech translation dans notre projet et à le traduire en trois langages différents.</span><span class="sxs-lookup"><span data-stu-id="527ab-105">In this tutorial, we learn aabout the Azure Cognitive Services Speech Translation component in our project as well as translate into three different languages.</span></span> 

1. <span data-ttu-id="527ab-106">Sélectionnez l’objet Lunarcom_Base dans la hiérarchie, puis cliquez sur Ajouter un composant dans le panneau Inspecteur.</span><span class="sxs-lookup"><span data-stu-id="527ab-106">Select the Lunarcom_Base object in the hierarchy, and click Add Component in the inspector panel.</span></span> <span data-ttu-id="527ab-107">Recherchez et sélectionnez LunarcomTranslationRecognizer.</span><span class="sxs-lookup"><span data-stu-id="527ab-107">Search for and select LunarcomTranslationRecognizer.</span></span>

![Module4Chapter3step1im](images/module4chapter3step1im.PNG)

> <span data-ttu-id="527ab-109">Remarque : Assurez-vous que le simulateur en mode hors connexion est désactivé avant de tester le traducteur Speech-SDK.</span><span class="sxs-lookup"><span data-stu-id="527ab-109">Note: Ensure the offline mode simulator is disabled before testing the Speech-SDK translator.</span></span> <span data-ttu-id="527ab-110">Pour pouvoir effectuer la conversion, vous devez être connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="527ab-110">In order to translate, you must be connected to the internet.</span></span> <span data-ttu-id="527ab-111">Consultez l’image ci-dessous, où trouver ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="527ab-111">See image below on where to find this setting.</span></span> 
>
> ![Module4Chapter3noteim](images/module4chapter3noteim.PNG)

2. <span data-ttu-id="527ab-113">Cliquez sur la liste déroulante dans LunarcomTranslationRecognizer, puis sélectionnez la langue vers laquelle vous souhaitez effectuer la conversion.</span><span class="sxs-lookup"><span data-stu-id="527ab-113">Click the drop-down in the LunarcomTranslationRecognizer, and select the language you would like to translate to.</span></span>

![Module4Chapter3step2im](images/module4chapter3step2im.PNG)

3. <span data-ttu-id="527ab-115">À présent, exécutez l’application et testez le convertisseur en cliquant sur le bouton satellite, puis commencez à parler.</span><span class="sxs-lookup"><span data-stu-id="527ab-115">Now, run the application and test the translator by clicking the Satellite button, and begin speaking.</span></span> <span data-ttu-id="527ab-116">Appuyez de nouveau sur le bouton satellite pour arrêter la reconnaissance.</span><span class="sxs-lookup"><span data-stu-id="527ab-116">Press the Satellite button again to stop the recognition.</span></span> <span data-ttu-id="527ab-117">Vous trouverez ci-dessous un exemple de ce à quoi doit ressembler votre scène.</span><span class="sxs-lookup"><span data-stu-id="527ab-117">Below is an example of what your scene should look like.</span></span> <span data-ttu-id="527ab-118">N’hésitez pas à modifier la langue sous la liste déroulante «langue cible» (Voir l’image ci-dessus) pour explorer la traduction dans d’autres langues.</span><span class="sxs-lookup"><span data-stu-id="527ab-118">Feel free to change the language under the "Target Language" dropdown (see image above) to explore translation into other languages.</span></span>

> <span data-ttu-id="527ab-119">Remarque : Avant de procéder à des tests, assurez-vous que le simulateur hors connexion est désactivé, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="527ab-119">Note: Before testing, ensure that the offline simulator is disabled, as shown in the image below.</span></span>
>
> ![Module4Chapter3noteim](images/module4chapter3noteim.PNG)

<span data-ttu-id="527ab-121">Vous trouverez ci-dessous un exemple de ce à quoi votre scène devrait ressembler:</span><span class="sxs-lookup"><span data-stu-id="527ab-121">Below is an example of what your scene should look like:</span></span>

![Module4Chapter3exampleim](images/module4chapter3exampleim.PNG)

## <a name="congratulations"></a><span data-ttu-id="527ab-123">Félicitations</span><span class="sxs-lookup"><span data-stu-id="527ab-123">Congratulations</span></span>

<span data-ttu-id="527ab-124">À présent, votre projet peut traduire les mots que vous parlez dans plusieurs langues différentes.</span><span class="sxs-lookup"><span data-stu-id="527ab-124">Now  your project can translate the words you speak into several different languages.</span></span> <span data-ttu-id="527ab-125">N’hésitez pas à vous amuser avec les langages et à tester l’exactitude de la traduction.</span><span class="sxs-lookup"><span data-stu-id="527ab-125">Feel free to play around with the languages, and test the accuracy of the translation.</span></span> 

[<span data-ttu-id="527ab-126">Didacticiel suivant: 4.  Configuration des intentions et compréhension du langage naturel</span><span class="sxs-lookup"><span data-stu-id="527ab-126">Next tutorial: 4.  Setting up intent and natural language understanding</span></span>](mrlearning-speechSDK-ch4.md)

