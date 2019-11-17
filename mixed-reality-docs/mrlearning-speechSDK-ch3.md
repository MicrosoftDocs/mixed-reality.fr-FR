---
title: Didacticiels Azure Speech Services-3. Ajout du composant Azure Cognitive Services Speech translation
description: Dans ce cours, vous allez apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: dc5300b51ccb151a2e38f9d15b84a4a9031e2bb4
ms.sourcegitcommit: 17427d4d8c3723d53540f1b7f5bc061bba08c1d6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/17/2019
ms.locfileid: "74143228"
---
# <a name="3-adding-the-azure-cognitive-services-speech-translation-component"></a>3. Ajout du composant Azure Cognitive Services Speech translation

Dans ce didacticiel, vous allez découvrir le composant Azure Cognitive Services Speech translation de votre projet, ainsi que la façon de traduire en trois langues différentes.

## <a name="instructions"></a>Instructions

1. Sélectionnez l’objet Lunarcom_Base dans la hiérarchie, puis cliquez sur Ajouter un composant dans le panneau Inspecteur. Recherchez et sélectionnez Lunarcom translation Recognizer.

    ![Module4Chapter3step1im](images/module4chapter3step1im.PNG)

    Désactivez le simulateur en mode hors connexion.

    ![Module4Chapter3noteim](images/module4chapter3noteim.PNG)

    >[!IMPORTANT]
    >Avant de poursuivre, assurez-vous que le simulateur en mode hors connexion est désactivé (comme indiqué dans l’image ci-dessus) avant de tester le traducteur du kit de développement logiciel (SDK) Speech. Pour pouvoir effectuer la conversion, vous devez être connecté à Internet.

2. Cliquez sur la liste déroulante dans le module de reconnaissance des traductions Lunarcom, puis sélectionnez la langue vers laquelle vous souhaitez effectuer la conversion.

    ![Module4Chapter3step2im](images/module4chapter3step2im.PNG)

3. Exécutez l’application et testez le convertisseur en cliquant sur le bouton satellite, puis commencez à parler. Appuyez de nouveau sur le bouton satellite pour arrêter la reconnaissance. Vous trouverez ci-dessous un exemple de ce à quoi doit ressembler votre scène. N’hésitez pas à modifier la langue sous la liste déroulante « langue cible » (Voir l’image ci-dessus) pour explorer la traduction dans d’autres langues.

    Vous trouverez ci-dessous un exemple de ce à quoi votre scène devrait ressembler :

    ![Module4Chapter3exampleim](images/module4chapter3exampleim.PNG)

## <a name="congratulations"></a>Félicitations !

Votre projet peut désormais traduire correctement les mots que vous parlez dans plusieurs langues différentes. N’hésitez pas à vous amuser avec les langages et à tester l’exactitude de la traduction.

[Didacticiel suivant : 4. Configuration de l’intention et compréhension du langage naturel](mrlearning-speechSDK-ch4.md)
