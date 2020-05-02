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
# <a name="3-adding-the-azure-cognitive-services-speech-translation-component"></a>3. Ajout du composant de traduction vocale Azure Cognitive Services

Dans ce tutoriel, vous allez ajouter la traduction vocale à votre projet, ce qui va vous permettre de traduire et transcrire votre parole en trois langues différentes.

## <a name="objectives"></a>Objectifs

* Apprendre à intégrer la traduction vocale Azure

## <a name="instructions"></a>Instructions

Dans la fenêtre Hierachy, sélectionnez l’objet **Lunarcom** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Lunarcom Translation Recognizer (Script)** à l’objet Lunarcom et configurez-le de la manière suivante :

* Remplacez la valeur de **Target Language** par la langue de votre choix, par exemple, _German_.

![mrlearning-speech](images/mrlearning-speech/tutorial3-section1-step1-1.png)

> [!NOTE]
> Le composant Lunarcom Translation Recognizer (Script) ne fait pas partie de MRTK. Il a été fourni avec les ressources de ce tutoriel.

Si vous entrez maintenant en mode Game, vous pouvez tester la traduction vocale en commençant par appuyer sur le bouton du satellite. Ensuite, en supposant que votre ordinateur est doté d’un microphone, quand vous dites quelque chose, votre parole est traduite dans la langue choisie et transcrite sur le panneau du terminal :

![mrlearning-speech](images/mrlearning-speech/tutorial3-section1-step1-2.png)

> [!CAUTION]
> L’application a besoin de se connecter à Azure, donc vérifiez que votre ordinateur/appareil est connecté à Internet.

## <a name="congratulations"></a>Félicitations

Votre projet peut maintenant traduire correctement les mots que vous dites dans plusieurs langues différentes. Exécutez l’application sur votre appareil pour vérifier que tout fonctionne bien.

[Tutoriel suivant : 4. Configuration des intentions et compréhension du langage naturel](mrlearning-speechSDK-ch4.md)
