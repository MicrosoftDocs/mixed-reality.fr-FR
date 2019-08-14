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
# <a name="3-adding-the-azure-cognitive-services-speech-translation-component"></a>3. Ajout du composant Azure Cognitive Services Speech translation

Dans ce didacticiel, nous allons découvrir le composant Azure Cognitive Services Speech translation dans notre projet et le traduire en trois langages différents. 

## <a name="instructions"></a>Instructions

1. Sélectionnez l’objet Lunarcom_Base dans la hiérarchie, puis cliquez sur Ajouter un composant dans le panneau Inspecteur. Recherchez et sélectionnez LunarcomTranslationRecognizer.

![Module4Chapter3step1im](images/module4chapter3step1im.PNG)

> Remarque : Assurez-vous que le simulateur en mode hors connexion est désactivé avant de tester le traducteur Speech-SDK. Pour pouvoir effectuer la conversion, vous devez être connecté à Internet. Consultez l’image ci-dessous, où trouver ce paramètre. 
>
> ![Module4Chapter3noteim](images/module4chapter3noteim.PNG)

2. Cliquez sur la liste déroulante dans LunarcomTranslationRecognizer, puis sélectionnez la langue vers laquelle vous souhaitez effectuer la conversion.

![Module4Chapter3step2im](images/module4chapter3step2im.PNG)

3. À présent, exécutez l’application et testez le convertisseur en cliquant sur le bouton satellite, puis commencez à parler. Appuyez de nouveau sur le bouton satellite pour arrêter la reconnaissance. Vous trouverez ci-dessous un exemple de ce à quoi doit ressembler votre scène. N’hésitez pas à modifier la langue sous la liste déroulante «langue cible» (Voir l’image ci-dessus) pour explorer la traduction dans d’autres langues.

> Remarque : Avant de procéder à des tests, assurez-vous que le simulateur hors connexion est désactivé, comme indiqué dans l’image ci-dessous.
>
> ![Module4Chapter3noteim](images/module4chapter3noteim.PNG)

Vous trouverez ci-dessous un exemple de ce à quoi votre scène devrait ressembler:

![Module4Chapter3exampleim](images/module4chapter3exampleim.PNG)

## <a name="congratulations"></a>Félicitations

À présent, votre projet peut traduire les mots que vous parlez dans plusieurs langues différentes. N’hésitez pas à vous amuser avec les langages et à tester l’exactitude de la traduction. 

[Didacticiel suivant: 4. Configuration des intentions et compréhension du langage naturel](mrlearning-speechSDK-ch4.md)

