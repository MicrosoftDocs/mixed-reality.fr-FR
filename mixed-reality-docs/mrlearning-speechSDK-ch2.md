---
title: Module d’apprentissage de SpeechSDK-reconnaissance vocale et transcription
description: Suivez ce cours pour apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 06/27/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: e8dc5da5a089079ba38a26969df6070af8bc6200
ms.sourcegitcommit: c7c7e3c836373b65e319609b4e8389dea6b081de
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68460305"
---
# <a name="2----adding-an-offline-mode-for-local-speech-to-text-translation"></a><span data-ttu-id="c0aa6-104">2.    Ajout d’un mode hors connexion pour la traduction vocale locale en texte</span><span class="sxs-lookup"><span data-stu-id="c0aa6-104">2.    Adding an offline mode for local speech-to-text translation</span></span>

<span data-ttu-id="c0aa6-105">Dans ce didacticiel, nous allons ajouter un mode hors connexion qui vous permet d’effectuer des traductions vocales en texte local quand nous ne pouvons pas nous connecter au service Azure.</span><span class="sxs-lookup"><span data-stu-id="c0aa6-105">In this tutorial, we'll add an offline mode that lets you perform local speech-to-text translation when we are unable to connect to the Azure service.</span></span> <span data-ttu-id="c0aa6-106">Nous simulerons  également un état déconnecté.</span><span class="sxs-lookup"><span data-stu-id="c0aa6-106">We will also *simulate* a disconnected state.</span></span>

1. <span data-ttu-id="c0aa6-107">Sélectionnez l’objet Lunarcom_Base dans la hiérarchie, puis cliquez sur Ajouter un composant dans le panneau Inspecteur.</span><span class="sxs-lookup"><span data-stu-id="c0aa6-107">Select the Lunarcom_Base object in the hierarchy, and click Add Component in the Inspector panel.</span></span> <span data-ttu-id="c0aa6-108">Recherchez et sélectionnez la reconnaissance hors connexion Lunarcom.</span><span class="sxs-lookup"><span data-stu-id="c0aa6-108">Search for and select the Lunarcom Offline Recognition.</span></span>

![Module4Chapter2step1im](images/module4chapter2step1im.PNG)

2. <span data-ttu-id="c0aa6-110">Cliquez sur la liste déroulante dans LunarcomOfflineRecognizer, puis sélectionnez activé.</span><span class="sxs-lookup"><span data-stu-id="c0aa6-110">Click the drop-down in the LunarcomOfflineRecognizer, and select Enabled.</span></span> <span data-ttu-id="c0aa6-111">Cela programme le projet pour qu’il agisse comme l’utilisateur n’a pas de connexion.</span><span class="sxs-lookup"><span data-stu-id="c0aa6-111">This programs the project to act like the user doesn't have a connection.</span></span> 

![Module4Chapter2step1im](images/module4chapter2step2im.PNG)

3. <span data-ttu-id="c0aa6-113">Maintenant, appuyez sur la touche lecture dans l’éditeur Unity et testez-la.</span><span class="sxs-lookup"><span data-stu-id="c0aa6-113">Now, press play in Unity Editor, and test it.</span></span> <span data-ttu-id="c0aa6-114">Appuyez sur le microphone dans le coin inférieur gauche de la scène, puis commencez à parler.</span><span class="sxs-lookup"><span data-stu-id="c0aa6-114">Press the microphone in the bottom left hand corner in the scene, and begin speaking.</span></span> 

> [!NOTE]
> <span data-ttu-id="c0aa6-115">Étant donné que nous sommes hors connexion, la fonctionnalité de mise en éveil par mot a été désactivée.</span><span class="sxs-lookup"><span data-stu-id="c0aa6-115">Because we’re offline, wake word functionality has been disabled.</span></span> <span data-ttu-id="c0aa6-116">Vous devez cliquer sur le microphone chaque fois que vous souhaitez que votre voix soit reconnue en mode hors connexion.</span><span class="sxs-lookup"><span data-stu-id="c0aa6-116">You'll have to physically click the microphone every time you wish to have your speech recognized when offline.</span></span> 

<span data-ttu-id="c0aa6-117">Vous trouverez ci-dessous un exemple de ce à quoi peut ressembler votre scène.</span><span class="sxs-lookup"><span data-stu-id="c0aa6-117">Below is an example of what your scene could look like.</span></span>

![Module4Chapter2exampleim](images/module4chapter2exampleim.PNG)

## <a name="congratulations"></a><span data-ttu-id="c0aa6-119">Félicitations</span><span class="sxs-lookup"><span data-stu-id="c0aa6-119">Congratulations</span></span>

<span data-ttu-id="c0aa6-120">Le mode hors connexion a été activé.</span><span class="sxs-lookup"><span data-stu-id="c0aa6-120">The offline mode has been enabled.</span></span> <span data-ttu-id="c0aa6-121">Désormais, lorsque vous êtes hors connexion, vous pouvez continuer à travailler sur votre projet avec le kit de développement logiciel (SDK) Speech!</span><span class="sxs-lookup"><span data-stu-id="c0aa6-121">Now, when you're offline, you can still work on your project with the speech-SDK!</span></span> 


[<span data-ttu-id="c0aa6-122">Didacticiel suivant: 3.  Ajout du composant Azure Cognitive Services Speech translation</span><span class="sxs-lookup"><span data-stu-id="c0aa6-122">Next Tutorial: 3.  Adding the Azure Cognitive Services speech translation component</span></span>](mrlearning-speechSDK-ch3.md)

