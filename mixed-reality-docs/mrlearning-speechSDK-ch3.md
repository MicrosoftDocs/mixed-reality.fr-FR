---
title: Didacticiels Azure Speech Services-3. Ajout du composant Azure Cognitive Services Speech translation
description: Suivez ce cours pour apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 490b9f6142208a190748b6d76c57be493172c1e5
ms.sourcegitcommit: b6b76275fad90df6d9645dd2bc074b7b2168c7c8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/11/2019
ms.locfileid: "73913202"
---
# <a name="3-adding-the-azure-cognitive-services-speech-translation-component"></a><span data-ttu-id="bd724-105">3. Ajout du composant Azure Cognitive Services Speech translation</span><span class="sxs-lookup"><span data-stu-id="bd724-105">3. Adding the Azure Cognitive Services speech translation component</span></span>

<span data-ttu-id="bd724-106">Dans ce didacticiel, nous allons découvrir le composant Azure Cognitive Services Speech translation dans notre projet et le traduire en trois langages différents.</span><span class="sxs-lookup"><span data-stu-id="bd724-106">In this tutorial, we learn about the Azure Cognitive Services Speech Translation component in our project as well as translate into three different languages.</span></span>

## <a name="instructions"></a><span data-ttu-id="bd724-107">Instructions</span><span class="sxs-lookup"><span data-stu-id="bd724-107">Instructions</span></span>

1. <span data-ttu-id="bd724-108">Sélectionnez l’objet Lunarcom_Base dans la hiérarchie, puis cliquez sur Ajouter un composant dans le panneau Inspecteur.</span><span class="sxs-lookup"><span data-stu-id="bd724-108">Select the Lunarcom_Base object in the hierarchy, and click Add Component in the inspector panel.</span></span> <span data-ttu-id="bd724-109">Recherchez et sélectionnez Lunarcom translation Recognizer.</span><span class="sxs-lookup"><span data-stu-id="bd724-109">Search for and select Lunarcom Translation Recognizer.</span></span>

    ![Module4Chapter3step1im](images/module4chapter3step1im.PNG)

    <span data-ttu-id="bd724-111">Désactivez le simulateur en mode hors connexion.</span><span class="sxs-lookup"><span data-stu-id="bd724-111">Disable the offline mode simulator.</span></span>

    ![Module4Chapter3noteim](images/module4chapter3noteim.PNG)

    >[!IMPORTANT]
    ><span data-ttu-id="bd724-113">Avant de poursuivre, assurez-vous que le simulateur en mode hors connexion est désactivé, comme illustré dans l’image ci-dessus, avant de tester le traducteur du kit de développement logiciel (SDK) Speech.</span><span class="sxs-lookup"><span data-stu-id="bd724-113">Before moving on, ensure the offline mode simulator is disabled, as shown in the image above, before testing the Speech-SDK translator.</span></span> <span data-ttu-id="bd724-114">Pour pouvoir effectuer la conversion, vous devez être connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="bd724-114">In order to translate, you must be connected to the internet.</span></span>

2. <span data-ttu-id="bd724-115">Cliquez sur la liste déroulante dans le module de reconnaissance des traductions Lunarcom, puis sélectionnez la langue vers laquelle vous souhaitez effectuer la conversion.</span><span class="sxs-lookup"><span data-stu-id="bd724-115">Click the drop-down in the Lunarcom Translation Recognizer, and select the language you would like to translate to.</span></span>

    ![Module4Chapter3step2im](images/module4chapter3step2im.PNG)

3. <span data-ttu-id="bd724-117">À présent, exécutez l’application et testez le convertisseur en cliquant sur le bouton satellite, puis commencez à parler.</span><span class="sxs-lookup"><span data-stu-id="bd724-117">Now, run the application and test the translator by clicking the Satellite button, and begin speaking.</span></span> <span data-ttu-id="bd724-118">Appuyez de nouveau sur le bouton satellite pour arrêter la reconnaissance.</span><span class="sxs-lookup"><span data-stu-id="bd724-118">Press the Satellite button again to stop the recognition.</span></span> <span data-ttu-id="bd724-119">Vous trouverez ci-dessous un exemple de ce à quoi doit ressembler votre scène.</span><span class="sxs-lookup"><span data-stu-id="bd724-119">Below is an example of what your scene should look like.</span></span> <span data-ttu-id="bd724-120">N’hésitez pas à modifier la langue sous la liste déroulante « langue cible » (Voir l’image ci-dessus) pour explorer la traduction dans d’autres langues.</span><span class="sxs-lookup"><span data-stu-id="bd724-120">Feel free to change the language under the "Target Language" dropdown (see image above) to explore translation into other languages.</span></span>

    <span data-ttu-id="bd724-121">Vous trouverez ci-dessous un exemple de ce à quoi votre scène devrait ressembler :</span><span class="sxs-lookup"><span data-stu-id="bd724-121">Below is an example of what your scene should look like:</span></span>

    ![Module4Chapter3exampleim](images/module4chapter3exampleim.PNG)

## <a name="congratulations"></a><span data-ttu-id="bd724-123">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="bd724-123">Congratulations</span></span>

<span data-ttu-id="bd724-124">À présent, votre projet peut traduire les mots que vous parlez dans plusieurs langues différentes.</span><span class="sxs-lookup"><span data-stu-id="bd724-124">Now your project can translate the words you speak into several different languages.</span></span> <span data-ttu-id="bd724-125">N’hésitez pas à vous amuser avec les langages et à tester l’exactitude de la traduction.</span><span class="sxs-lookup"><span data-stu-id="bd724-125">Feel free to play around with the languages, and test the accuracy of the translation.</span></span>

[<span data-ttu-id="bd724-126">Didacticiel suivant : 4. Configuration de l’intention et compréhension du langage naturel</span><span class="sxs-lookup"><span data-stu-id="bd724-126">Next tutorial: 4. Setting up intent and natural language understanding</span></span>](mrlearning-speechSDK-ch4.md)
