---
title: Module d’apprentissage de SpeechSDK-reconnaissance vocale et transcription
description: Suivez ce cours pour apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: da485f167ef3902dd75adf8da8181504fbc6c6df
ms.sourcegitcommit: b6b76275fad90df6d9645dd2bc074b7b2168c7c8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/11/2019
ms.locfileid: "73913165"
---
# <a name="speech-sdk-learning-module---rocket-launcher-control-using-speech-commands"></a>Module Speech SDK Learning-contrôle du lanceur Rocket utilisant des commandes vocales

Dans cette leçon, nous allons utiliser la fonctionnalité d’intention du service Azure Speech pour comprendre l’objectif de la reconnaissance vocale. Nous utiliserons l’intention de parole détectée comme commandes vocales pour contrôler le lanceur Rocket. Au cours de cette leçon, nous allons importer la ressource du lanceur Rocket et nous allons intermettre les commandes vocales intentionnelles détectées sur les boutons de contrôle prédéfinis pour contrôler la fusée.

## <a name="objectives"></a>Objectifs

- Découvrez comment connecter des intentions vocales en tant que commandes vocales.
- Découvrez comment utiliser les commandes vocales d’intention vocale comme commandes de contrôle de fusée.

## <a name="instructions"></a>Instructions

1. Dans ce didacticiel, nous allons utiliser un élément multimédia « BaseModule » pour intégrer le lanceur Rocket avec les commandes vocales. Pour ce faire, nous devons importer la ressource dans notre projet. Vous pouvez télécharger le composant « lanceur Rocket » à l’aide de ce [lien](https://github.com/Developer-OI/MixedRealityLearning/releases/download/1.2.1/BaseModuleAssets-1.2.1.unitypackage).

2. Pour importer l’élément multimédia, accédez à ressources-> Importer un package-> package personnalisé-> accédez au fichier téléchargé, puis cliquez sur Importer.

    ![module4chapter5step1](images/module4chapter5step1.PNG)

3. Après avoir importé le composant « ressources du module de base », naviguez dans le dossier « ressources du module de base »-> Prefabs-> sélectionnez « fusée Launcher_Complete », puis faites-le glisser vers la hiérarchie de la scène existante.

    ![module4chapter5step2](images/module4chapter5step2.PNG)

4. Nous devons maintenant intégrer notre « lanceur Rocket » à notre projet LUIS que nous avons travaillé dans notre [leçon](mrlearning-speechSDK-ch4.md)précédente. Pour cela, développez le Prefab « fusée Launcher_Complete » dans la hiérarchie et recherchez les boutons « LaunchRoundButton », « ResetRoundButton » et « indicateurs de positionnement ».

    ![module4chapter5step3](images/module4chapter5step3.PNG)

5. Sélectionnez « LaunchRoundButton » et dans le panneau de l’inspecteur, accédez à « interactive » et sous événements « OnClick () », faites glisser et déposez le Prefab « LunarModule ». Sélectionnez ensuite la fonction déroulante et sélectionnez « LunarModule », puis accédez à la fonction « StartThruster () » et sélectionnez-la.

    ![module4chapter5step 3.0](images/module4chapter5step3.0.PNG)

    ![module4chapter5step3a](images/module4chapter5step3a.PNG)

6. Sélectionnez « ResetRoundButton » et dans le panneau de l’inspecteur, accédez à « interactive » et sous événements « OnClick () », faites glisser et déposez le Prefab « LunarModule ». Sélectionnez ensuite la fonction déroulante et sélectionnez « LunarModule », puis accédez à la fonction « resetModule () » et sélectionnez-la.

    ![module4chapter5step3b](images/module4chapter5step3b.PNG)

7. Sélectionnez « indicateurs d’emplacement » et dans le panneau Inspecteur, accédez à « interactive » et sous événements « OnClick () », faites glisser et déposez le Prefab « LunarModule ». Ensuite, sélectionnez la liste déroulante de la fonction et sélectionnez « LunarModule », puis accédez à la fonction « TogglePlacementHints » et sélectionnez ToggleGameOBjects ().

    ![module4chapter5step3c](images/module4chapter5step3c.PNG)

8. Ensuite, sélectionnez le Lunarcom_Completed Prefab dans la hiérarchie et accédez au script « Lunarcom intentr » dans Inspector, puis faites glisser et déposez les boutons « LaunchRoundButton », « ResetRoundButton » et « indicateurs de positionnement » à leurs emplacements respectifs.

    ![module4chapter5step4](images/module4chapter5step4.PNG)

9. Appuyez sur le bouton de lecture dans l’éditeur Unity et cliquez sur le bouton « Rocket » et indiquez les expressions telles que « pousser le bouton de lancement fusée », « afficher un indicateur de positionnement », « appuyer sur le bouton REST » ou toute autre expression relative au lancement, à la réinitialisation ou à l’indication du lanceur Rocket.

    ![module4chapter5step5a](images/module4chapter5step5a.PNG)

    ![module4chapter5step5b](images/module4chapter5step5b.PNG)

    ![module4chapter5step5c](images/module4chapter5step5c.PNG)

## <a name="congratulations"></a>Félicitations !

Dans cette leçon, nous avons appris comment connecter les commandes vocales en intelligence artificielle aux commandes vocales pour l’utiliser comme méthode d’entrée. À présent, notre programme peut utiliser l’intention des orateurs comme des commandes vocales pour fournir des entrées pour le lanceur Rocket.
