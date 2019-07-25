---
title: Module d’apprentissage de SpeechSDK-reconnaissance vocale et transcription
description: Suivez ce cours pour apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 0cffb9ac8f61f77b77fc5925264b95ba57d94ece
ms.sourcegitcommit: c7c7e3c836373b65e319609b4e8389dea6b081de
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68460344"
---
# <a name="speech-sdk-learning-module---intent-and-natural-language-understanding"></a>Module de formation Speech SDK-Intent et Language Understanding naturel

Dans cette leçon, nous allons explorer la fonctionnalité d’intention du service Azure Speech. La fonctionnalité d’intention nous permet d’équiper notre application avec des commandes vocales en intelligence artificielle, où les utilisateurs peuvent indiquer des commandes vocales non spécifiques, tout en ayant l’intention de les interpréter par le système. Au cours de cette leçon, nous allons configurer notre portail Azure LUIS, configurer nos intentions/entités/énoncés, publier notre ressource intentionnelle, connecter notre application Unity à notre ressource intentionnelle et effectuer notre premier appel d’API d’intention.

## <a name="objectives"></a>Objectifs

- Découvrez comment configurer l’intention et la compréhension du langage naturel dans notre application
- Découvrez comment configurer le portail LUIS d’Azure
- Découvrez comment configurer l’intention, les entités et les énoncés sur Azure

## <a name="instructions"></a>Instructions
1. Autorisez votre ordinateur à activer la dictée. pour ce faire, accédez à paramètres Windows, sélectionnez «confidentialité», puis «parole» et enfin «entrée manuscrite & typage» et activez Speech services et suggestions de saisie.

![Module4Chapter4step1aim](images/module4chapter4step1aim.PNG)

![Module4Chapter4step1bim](images/module4chapter4step1bim.PNG)

![Module4Chapter4step1cim](images/module4chapter4step1cim.PNG)


2. Connectez-vous au [portail Azure](https://portal.azure.com/). Une fois que vous êtes connecté, cliquez sur créer une ressource, recherchez «Language Understanding», puis cliquez sur entrée.

![Module4Chapter4step2im](images/module4chapter4step2im.PNG)

3. Sélectionnez le bouton créer pour créer une instance de ce service. Nommez votre projet «Speech_SDK_Learning_Module» et sélectionnez «payer à l’accès».

![Module4Chapter4step3aim](images/module4chapter4step3aim.png)

![Module4Chapter4step3bim](images/module4chapter4step3bim.PNG)

4. Sélectionnez votre région.  Dans le cadre de ce didacticiel, sélectionnez «(US) Ouest des États-Unis». Choisissez ensuite «F0» comme niveau tarifaire. Cliquez maintenant sur «créer» (situé dans le coin inférieur gauche) pour créer la ressource.

>  Remarque: une fois que vous avez cliqué sur «créer», vous devez attendre que le service soit créé. cette opération peut prendre une minute.

5. Une notification s’affiche dans le portail une fois la ressource créée. Cliquez sur cette notification et sélectionnez «atteindre la ressource».

6. À partir de la page «Démarrage rapide» de votre service «API LUIS», accédez à la première étape, saisissez vos «clés», puis cliquez sur «clés» (vous pouvez également effectuer cette opération en cliquant sur le lien hypertexte bleu «clés», comme illustré dans l’image ci-dessous). Cela permet de révéler votre service, «Keys». Enregistrez une copie de l’une des clés afin de pouvoir l’utiliser ultérieurement dans l’application.

![Module4Chapter4step6im](images/module4chapter4step6im.PNG)

7. De retour dans la page «Démarrage rapide», sous la section 2B, cliquez sur «portail Language Understanding» (illustré dans l’image ci-dessus) pour être redirigé vers la page Web que vous utiliserez pour créer votre nouveau service, au sein de l’application LUIS.

> Remarque : Quand vous atteignez le «portail Language Understanding», vous devrez peut-être vous connecter, si ce n’est déjà fait, avec les mêmes informations d’identification que votre Portail Azure. Si vous utilisez LUIS pour la première fois, vous devez faire défiler vers le bas de la page d’accueil, pour rechercher et cliquer sur le bouton «créer une application LUIS».

8. Une fois connecté, cliquez sur mes applications (si vous n’êtes pas actuellement dans cette section). Vous pouvez ensuite cliquer sur créer une nouvelle application. Nommez la nouvelle application «Speech SDK Learning module». Ajoutez également «module d’apprentissage du kit de développement logiciel (SDK) Speech» au champ Description. Cliquez ensuite sur «terminé».

![Module4Chapter4step8aim](images/module4chapter4step8aim.PNG)

![Module4Chapter4step8bim](images/module4chapter4step8bim.PNG)

> observe Si votre application est censée comprendre une langue différente de l’anglais, vous devez remplacer la «culture» par la langue appropriée.

9. Cliquez sur «Build» situé en haut à droite.

10. Sous ressources de l’application sur la gauche, sélectionnez «intentions», puis cliquez sur «créer un nouvel objectif» et nommez-la «PressButton». 

![Module4Chapter4step10im](images/module4chapter4step10im.PNG)

> Remarque : Il est important d’utiliser les noms des intentions et des entités utilisées dans ce didacticiel, car l’application Lunarcom y fait référence par nom. 
>
> Remarque: vous devez maintenant avoir 2 intentions-«PressButton» et «None».

11. Sous ressources de l’application sur la gauche, sélectionnez «entités», puis cliquez sur «créer une entité» et nommez-la «action» et conservez le type d’entité «simple».

![Module4Chapter4step11im](images/module4chapter4step11im.PNG)

12. Cliquez de nouveau sur «créer une nouvelle entité» et nommez-la «cible» et conservez le type d’entité «simple».

![Module4Chapter4step12im](images/module4chapter4step12im.PNG)

13. Sous ressources de l’application sur la gauche, sélectionnez «intentions», puis cliquez sur l’intention «PressButton» que vous avez créée à l’étape 10.

![Module4Chapter4step13im](images/module4chapter4step13im.PNG)

14. Cliquez sur la liste déroulante «Afficher les options» à droite, puis sélectionnez «Afficher les valeurs d’entité». 

![Module4Chapter4step14aim](images/module4chapter4step14aim.PNG)Cliquez sur «Entrez un exemple...» entr. Ensuite, entrez les énoncés suivants: 

![Module4Chapter4step14bim](images/module4chapter4step14bim.PNG)

15. Cliquez sur la liste déroulante «Afficher les options» à droite, puis sélectionnez «Afficher les noms d’entité».

![Module4Chapter4step15im](images/module4chapter4step15im.PNG)

16. Assurez-vous que chacun des 10 énoncés a les étiquettes d’entité suivantes dans les emplacements suivants, de 1.) en cliquant sur les mots dont l’étiquette est incorrecte et, dans le menu contextuel, sélectionnez «Supprimer l’étiquette» et 2.) en cliquant sur les mots qui doivent être étiquetés et, dans le menu contextuel, sélectionnez l’étiquette appropriée.

![Module4Chapter4step16im](images/module4chapter4step16im.PNG)

17. À présent, pour publier le modèle, cliquez sur «train» dans le coin supérieur droit. Ensuite, une fois le traitement terminé, cliquez sur «test» dans le coin supérieur droit.

![Module4Chapter4step17im](images/module4chapter4step17im.PNG)

18. Entrez dans la zone de texte «sélectionner le bouton lancer».

> Remarque: nous n’avons pas ajouté «Select» comme action dans l’un de nos énoncés, mais si vous cliquez sur «Inspect», le modèle a reconnu «Select» comme une entité d’action.
>
> ![Module4Chapter4noteim](images/module4chapter4noteim.PNG)

19. À présent, cliquez sur «publier» dans le coin supérieur droit. Assurez-vous que la liste déroulante indique «production», puis cliquez sur «publier» dans la fenêtre contextuelle. 

![Module4Chapter4step19im](images/module4chapter4step19im.PNG)

20. Une fois publiée, une barre verte doit apparaître en haut de la page.  Cliquez sur la barre verte pour atteindre la page «gérer». 

![Module4Chapter4step20im](images/module4chapter4step20im.PNG)

21. Cliquez sur «clés et points de terminaison» sous «paramètres d’application» à gauche. Ensuite, définissez la liste déroulante «publier sur» sur «production». Définissez le fuseau horaire en fonction de vos propres et cochez la case pour inclure tous les scores d’intention prédits. Enfin, cliquez sur «affecter une ressource».

![Module4Chapter4step21im](images/module4chapter4step21im.PNG)

22. Sélectionnez locataire dans la première liste déroulante, puis sélectionnez paiement à l’accès dans la liste déroulante nom de l’abonnement. Sous LUIS nom de la ressource, choisissez la ressource que nous avons créée ci-dessus dans les étapes 1-5. Cliquez ensuite sur «affecter la ressource». 

![Module4Chapter4step22im](images/module4chapter4step22im.PNG)

> Remarque : Veillez à copier et à enregistrer l’URL de point de terminaison associée à la ressource que nous venons d’attribuer afin qu’elle soit facilement accessible pour la section suivante.
>
> Remarque : Pour le nom du locataire, mettez votre entreprise ou votre profil créé pour cette application.

23. À présent, ouvrez la nouvelle application dans Unity et sélectionnez l’objet Lunarcom_Base dans la hiérarchie. Cliquez sur «Ajouter un composant» dans le panneau inspecteur et recherchez et sélectionnez «LunarcomIntentRecognizer».

![Module4Chapter4step23im](images/module4chapter4step23im.PNG)

24. Dans le champ de point de terminaison Luis de la «LunarcomIntentRecognizer» dans le panneau Inspecteur, entrez l’URL de point de terminaison que vous avez enregistrée à l’étape 22. 

![Module4Chapter4step24im](images/module4chapter4step24im.PNG)

>  Remarque : Dans le composant «LunarcomOfflineRecognizer» du volet de l’inspecteur, assurez-vous que l’option «désactiver» est sélectionnée pour «SimulateOfflineMode». dans le cas contraire, le test du programme ne fonctionnera pas. 

25. Appuyez sur le bouton lecture dans l’éditeur Unity et cliquez sur le bouton Rocket pour démarrer la reconnaissance intentionnelle. À l’expression «sélectionnez le bouton lancer Rocket».

>  Remarque : L’application a reconnu la fonction souhaitée et activé le bouton Rocket.
>
> ![Module4Chapter4step24im](images/module4chapter4note2im.PNG)

## <a name="congratulations"></a>Félicitations

Dans cette leçon, nous avons appris à ajouter des commandes vocales dotées de l’intelligence artificielle. À présent, votre programme peut reconnaître l’intention des utilisateurs même s’ils ne dictent pas de commandes vocales précises.

