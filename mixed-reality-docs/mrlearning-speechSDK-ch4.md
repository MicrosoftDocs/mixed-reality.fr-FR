---
title: Didacticiels Azure Speech services-4. Configuration de l’intention et compréhension du langage naturel
description: Suivez ce cours pour apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: e712fc2fd66b1add5b16b7dd8e6c37551aefe43a
ms.sourcegitcommit: 9005b3fdfa87ac8fdc18a594a681e25c00ac5ce1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2019
ms.locfileid: "75003208"
---
# <a name="4-setting-up-intent-and-natural-language-understanding"></a>4. Configuration de l’intention et de la compréhension du langage naturel

Dans cette leçon, vous allez explorer la fonctionnalité d’intention du service Azure Speech. La fonctionnalité d’intention vous permet d’équiper notre application avec des commandes vocales en intelligence artificielle, où les utilisateurs peuvent indiquer des commandes vocales non spécifiques tout en gardant leur intention compréhensible par le système. Au cours de cette leçon, nous allons configurer notre portail Azure LUIS, configurer nos intentions/entités/énoncés, publier notre ressource intentionnelle, connecter notre application Unity à notre ressource intentionnelle et effectuer notre premier appel d’API d’intention.

## <a name="objectives"></a>Objectifs

- Découvrez comment configurer l’intention et la compréhension du langage naturel dans notre application
- Découvrez comment configurer le portail LUIS d’Azure
- Découvrez comment configurer l’intention, les entités et les énoncés sur Azure

## <a name="instructions"></a>Instructions

1. Autorisez votre ordinateur à activer la dictée. Pour ce faire, accédez à paramètres Windows, sélectionnez « confidentialité », puis « parole », suivi de « entrée manuscrite & typage » et activez Speech services et suggestions de saisie.

    ![Module4Chapter4step1aim](images/module4chapter4step1aim.PNG)

    ![Module4Chapter4step1bim](images/module4chapter4step1bim.PNG)

    ![Module4Chapter4step1cim](images/module4chapter4step1cim.PNG)

2. Connectez-vous au [portail Azure](https://portal.azure.com/). Une fois que vous êtes connecté, cliquez sur créer une ressource, recherchez « Language Understanding », puis cliquez sur entrée.

    ![mrlearning-Speech-CH4-1-Step2. png](images/mrlearning-speech-ch4-1-step2.png)

3. Cliquez sur le bouton **créer** pour créer une instance de ce service.

    ![mrlearning-Speech-CH4-1-step3a. png](images/mrlearning-speech-ch4-1-step3a.png)

    Donnez un **nom**à votre ressource, par exemple *Speech-SDK-Learning-module*. Pour **abonnement**, sélectionnez *paiement à l'* enregistrement ou *fin* si vous disposez d’un compte d’évaluation. Ensuite, créez un nouveau **groupe de ressources** en cliquant sur le lien **créer** , entrez un nom, par exemple, *HoloLens-2-Tutorials-Resource-Group*, puis cliquez sur le bouton **OK** .

    ![mrlearning-Speech-CH4-1-step3b. png](images/mrlearning-speech-ch4-1-step3b.png)

4. Sélectionnez votre **emplacement de création** et l' **emplacement d’exécution**. Pour les besoins de ce didacticiel, utilisez *(États-Unis) Ouest des États-Unis*, puis choisissez *F0 (5 appels par seconde, 10 000 appels par mois)* pour le niveau **tarifaire de création** et le **niveau tarifaire d’exécution**. Enfin, cliquez sur le bouton **créer** pour créer la ressource, ainsi que sur le nouveau groupe de ressources.

    ![mrlearning-Speech-CH4-1-step4. png](images/mrlearning-speech-ch4-1-step4.png)

    >[!NOTE]
    >Après avoir cliqué sur le bouton créer, vous devez attendre que le service soit créé, ce qui peut prendre quelques minutes.

5. Une fois le processus de création de la ressource terminé, vous verrez le message **votre déploiement est terminé**.

    ![mrlearning-Speech-CH4-1-step5. png](images/mrlearning-speech-ch4-1-step5.png)

6. À l’aide du même compte d’utilisateur, connectez-vous au portail [Language Understanding intelligent service (Luis)](https://www.luis.ai/) , sélectionnez votre pays et acceptez les conditions d’utilisation.

    >[!NOTE]
    >Quand vous atteignez le portail Language Understanding, vous devrez peut-être vous connecter, si ce n’est déjà fait, avec les mêmes informations d’identification que votre Portail Azure. Si vous utilisez LUIS pour la première fois, vous devez faire défiler vers le bas de la page d’accueil pour rechercher et cliquer sur le bouton « créer une application LUIS ».

7. Une fois connecté, cliquez sur mes applications (si vous n’êtes pas actuellement dans cette section). Vous pouvez ensuite cliquer sur créer une nouvelle application. Nommez la nouvelle application « Speech SDK Learning module ». Ajoutez également « module d’apprentissage du kit de développement logiciel (SDK) Speech » au champ Description. Cliquez ensuite sur « terminé ».

    ![Module4Chapter4step8aim](images/module4chapter4step8aim.PNG)

    ![Module4Chapter4step8bim](images/module4chapter4step8bim.PNG)

    >[!NOTE]
    >Si votre application est censée comprendre une langue différente de l’anglais, vous devez remplacer la « culture » par la langue appropriée.

8. Cliquez sur « Build » situé en haut à droite.

9. Sous ressources de l’application sur la gauche, sélectionnez « intentions », puis cliquez sur « créer un nouvel objectif » et nommez-la « PressButton ».

    ![Module4Chapter4step10im](images/module4chapter4step10im.PNG)

    >[!NOTE]
    >Il est important d’utiliser les noms des intentions et des entités utilisées dans ce didacticiel, car l’application Lunarcom y fait référence par nom.

    >[!NOTE]
    >Vous devez maintenant avoir 2 intentions-« PressButton » et « None ».

10. Sous ressources de l’application sur la gauche, sélectionnez « entités », cliquez sur « créer une nouvelle entité », nommez-la « action » et conservez le type d’entité « simple ».

    ![Module4Chapter4step11im](images/module4chapter4step11im.PNG)

11. Cliquez à nouveau sur « créer une nouvelle entité » et nommez-la « cible ». Conservez également le type d’entité « simple ».

    ![Module4Chapter4step12im](images/module4chapter4step12im.PNG)

12. Sous ressources de l’application sur la gauche, sélectionnez « intentions », puis cliquez sur l’intention « PressButton » que vous avez créée à l’étape 10.

    ![Module4Chapter4step13im](images/module4chapter4step13im.PNG)

13. Cliquez sur la liste déroulante « Afficher les options » à droite et sélectionnez « Afficher les valeurs d’entité ».

    ![Module4Chapter4step14aim](images/module4chapter4step14aim.PNG)

    Cliquez sur « Entrez un exemple... » entr. Ensuite, entrez les énoncés suivants :

    ![Module4Chapter4step14bim](images/module4chapter4step14bim.PNG)

14. Cliquez sur la liste déroulante « Afficher les options » à droite, puis sélectionnez « Afficher les noms d’entité ».

    ![Module4Chapter4step15im](images/module4chapter4step15im.PNG)

15. Assurez-vous que chacun des 10 énoncés a les étiquettes d’entité suivantes dans les emplacements suivants, de 1.) en cliquant sur les mots dont l’étiquette est incorrecte et, dans le menu contextuel, sélectionnez « Supprimer l’étiquette » et 2.) en cliquant sur les mots qui doivent être étiquetés et, dans le menu contextuel, sélectionnez l’étiquette appropriée.

    ![Module4Chapter4step16im](images/module4chapter4step16im.PNG)

16. À présent, pour publier le modèle, cliquez sur « train » dans le coin supérieur droit. Ensuite, une fois le traitement terminé, cliquez sur « test » dans le coin supérieur droit.

    ![Module4Chapter4step17im](images/module4chapter4step17im.PNG)

17. Entrez dans la zone de texte « sélectionner le bouton lancer ».

    >[!NOTE]
    >Nous n’avons pas ajouté « Select » comme action dans l’un de nos énoncés, mais si vous cliquez sur « Inspect », le modèle a reconnu « Select » comme une entité d’action.
    >
    > ![Module4Chapter4noteim](images/module4chapter4noteim.PNG)

18. Cliquez sur « publier » dans le coin supérieur droit. Assurez-vous que la liste déroulante indique « production », puis cliquez sur « publier » dans la fenêtre contextuelle.

    ![Module4Chapter4step19im](images/module4chapter4step19im.PNG)

19. Une fois publiée, une barre verte doit apparaître en haut de la page. Cliquez sur la barre verte pour afficher la page « gérer ».

    ![Module4Chapter4step20im](images/module4chapter4step20im.PNG)

20. Cliquez sur « clés et points de terminaison » sous « paramètres d’application » à gauche. Ensuite, définissez la liste déroulante « publier sur » sur « production ». Définissez le fuseau horaire en fonction de vos propres et cochez la case pour inclure tous les scores d’intention prédits. Enfin, cliquez sur « affecter une ressource ».

    ![Module4Chapter4step21im](images/module4chapter4step21im.PNG)

21. Sélectionnez locataire dans la première liste déroulante et sélectionnez « paiement à l’accès » dans la liste déroulante nom de l’abonnement. Sous LUIS nom de la ressource, choisissez la ressource que nous avons créée ci-dessus dans les étapes 1-5. Cliquez ensuite sur « affecter la ressource ».

    ![Module4Chapter4step22im](images/module4chapter4step22im.PNG)

    >[!NOTE]
    >Veillez à copier et à enregistrer l’URL de point de terminaison associée à la ressource que nous venons d’attribuer afin qu’elle soit facilement accessible pour la section suivante.

    >[!NOTE]
    >Pour le nom du locataire, mettez votre entreprise ou votre profil créé pour cette application.

22. À présent, ouvrez la nouvelle application dans Unity et sélectionnez l’objet Lunarcom_Base dans la hiérarchie. Cliquez sur « Ajouter un composant » dans le panneau inspecteur et recherchez et sélectionnez « LunarcomIntentRecognizer ».

    ![Module4Chapter4step23im](images/module4chapter4step23im.PNG)

23. Dans le champ de point de terminaison Luis de la « LunarcomIntentRecognizer » dans le panneau Inspecteur, entrez l’URL de point de terminaison que vous avez enregistrée à l’étape 22.

    ![Module4Chapter4step24im](images/module4chapter4step24im.PNG)

    >[!NOTE]
    >Dans le composant « LunarcomOfflineRecognizer » du volet de l’inspecteur, assurez-vous que l’option « désactiver » est sélectionnée pour « SimulateOfflineMode ». dans le cas contraire, le test du programme ne fonctionnera pas.

24. Appuyez sur le bouton lecture dans l’éditeur Unity et cliquez sur le bouton Rocket pour démarrer la reconnaissance intentionnelle. À l’expression « sélectionnez le bouton lancer Rocket ».

    >[!NOTE]
    >L’application a reconnu la fonction souhaitée et activé le bouton Rocket.
    >
    >![Module4Chapter4step24im](images/module4chapter4note2im.PNG)

## <a name="congratulations"></a>Félicitations !

Dans cette leçon, vous avez appris à ajouter des commandes vocales dotées de l’intelligence artificielle. À présent, votre programme peut reconnaître l’intention des utilisateurs, même s’ils ne sont pas en train de dicter des commandes vocales précises !
