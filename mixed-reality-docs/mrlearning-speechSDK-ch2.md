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
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79031631"
---
# <a name="2-using-speech-recognition-to-execute-commands"></a>2. Utilisation de la reconnaissance vocale pour exécuter des commandes

Dans ce tutoriel, vous allez ajouter la capacité d’exécuter des commandes en utilisant la reconnaissance vocale Azure, ce qui va vous permettre de déclencher une action en fonction du mot ou de l’expression que vous définissez.

## <a name="objectives"></a>Objectifs

* Découvrir comment la reconnaissance vocale Azure peut être utilisée pour exécuter des commandes

## <a name="instructions"></a>Instructions

Dans la fenêtre Hierachy, sélectionnez l’objet **Lunarcom** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Lunarcom Wake Word Recognizer (Script)** à l’objet Lunarcom et configurez-le de la manière suivante :

* Dans le champ **Wake Word**, entrez une expression appropriée, par exemple, _Activer le terminal_.
* Dans le champ **Dismiss Word**, entrez une expression appropriée, par exemple, _Désactiver le terminal_.

![mrlearning-speech](images/mrlearning-speech/tutorial2-section1-step1-1.png)

> [!NOTE]
> Le composant Lunarcom Wake Word Recognizer (Script) ne fait pas partie de MRTK. Il a été fourni avec les ressources de ce tutoriel.

Si vous entrez maintenant en mode Game, comme dans le tutoriel précédent, le panneau du terminal est activé par défaut, mais vous pouvez maintenant le désactiver en prononçant la valeur de Dismiss Word, **Désactiver le terminal** :

![mrlearning-speech](images/mrlearning-speech/tutorial2-section1-step1-2.png)

Et réactivez-le en prononçant la valeur de Wake Word, à savoir **Activer le terminal** :

![mrlearning-speech](images/mrlearning-speech/tutorial2-section1-step1-3.png)

> [!CAUTION]
> L’application a besoin de se connecter à Azure, donc vérifiez que votre ordinateur/appareil est connecté à Internet.

> [!TIP]
> Si vous prévoyez d’être souvent dans l’impossibilité de vous connecter à Azure, vous pouvez également implémenter des commandes vocales à l’aide de MRTK en suivant les instructions données dans [Activation des commandes vocales](mrlearning-base-ch5.md#enabling-voice-commands).

## <a name="congratulations"></a>Félicitations

Vous avez implémenté des commandes vocales Azure. Exécutez l’application sur votre appareil pour vérifier que tout fonctionne bien.

Dans le tutoriel suivant, vous allez apprendre à traduire la parole en utilisant la traduction vocale Azure.

[Tutoriel suivant : 3. Ajout du composant de traduction vocale Azure Cognitive Services](mrlearning-speechSDK-ch3.md)
