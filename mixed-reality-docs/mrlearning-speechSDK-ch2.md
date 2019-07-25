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
# <a name="2----adding-an-offline-mode-for-local-speech-to-text-translation"></a>2.    Ajout d’un mode hors connexion pour la traduction vocale locale en texte

Dans ce didacticiel, nous allons ajouter un mode hors connexion qui vous permet d’effectuer des traductions vocales en texte local quand nous ne pouvons pas nous connecter au service Azure. Nous simulerons  également un état déconnecté.

1. Sélectionnez l’objet Lunarcom_Base dans la hiérarchie, puis cliquez sur Ajouter un composant dans le panneau Inspecteur. Recherchez et sélectionnez la reconnaissance hors connexion Lunarcom.

![Module4Chapter2step1im](images/module4chapter2step1im.PNG)

2. Cliquez sur la liste déroulante dans LunarcomOfflineRecognizer, puis sélectionnez activé. Cela programme le projet pour qu’il agisse comme l’utilisateur n’a pas de connexion. 

![Module4Chapter2step1im](images/module4chapter2step2im.PNG)

3. Maintenant, appuyez sur la touche lecture dans l’éditeur Unity et testez-la. Appuyez sur le microphone dans le coin inférieur gauche de la scène, puis commencez à parler. 

> [!NOTE]
> Étant donné que nous sommes hors connexion, la fonctionnalité de mise en éveil par mot a été désactivée. Vous devez cliquer sur le microphone chaque fois que vous souhaitez que votre voix soit reconnue en mode hors connexion. 

Vous trouverez ci-dessous un exemple de ce à quoi peut ressembler votre scène.

![Module4Chapter2exampleim](images/module4chapter2exampleim.PNG)

## <a name="congratulations"></a>Félicitations

Le mode hors connexion a été activé. Désormais, lorsque vous êtes hors connexion, vous pouvez continuer à travailler sur votre projet avec le kit de développement logiciel (SDK) Speech! 


[Didacticiel suivant: 3.  Ajout du composant Azure Cognitive Services Speech translation](mrlearning-speechSDK-ch3.md)

