---
title: Tutoriels sur les services Azure Speech - 4. Configuration des intentions et compréhension du langage naturel
description: Suivez ce cours pour découvrir comment implémenter le SDK Azure Speech au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: b2342e7d0d502af2787ca311d18a44f8726acf2d
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "79028369"
---
# <a name="4-setting-up-intent-and-natural-language-understanding"></a>4. Configuration des intentions et compréhension du langage naturel

Dans ce tutoriel, vous allez découvrir la reconnaissance de l’intention du service Azure Speech. La reconnaissance de l’intention vous permet d’équiper notre application de commandes vocales optimisées par l’IA (intelligence artificielle). Ainsi, si les utilisateurs énoncent des commandes vocales imprécises, le système peut quand même comprendre leur intention.

## <a name="objectives"></a>Objectifs

* Découvrir comment configurer l’intention, les entités et les énoncés dans le portail LUIS
* Apprendre à implémenter la compréhension de l’intention et du langage naturel dans notre application

## <a name="preparing-the-scene"></a>Préparation de la scène

Dans la fenêtre Hierachy, sélectionnez l’objet **Lunarcom** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Lunarcom Intent Recognizer (Script)** à l’objet Lunarcom :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section1-step1-1.png)

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** > **RocketLauncher**, faites glisser le préfabriqué **RocketLauncher_Complete** dans la fenêtre Hierarchy et placez-le à un emplacement approprié devant la caméra, par exemple :

* Transform **Position** X = 0, Y = -0.4, Z = 1
* Transform **Rotation** X = 0, Y = 90, Z = 0

![mrlearning-speech](images/mrlearning-speech/tutorial4-section1-step1-2.png)

Dans la fenêtre Hierachy, re-sélectionnez l’objet **Lunarcom**, puis développez l’objet **RocketLauncher_Complete** > **Button** et affectez à chaque objet enfant de l’objet **Buttons** le champ **Lunar Launcher Buttons** correspondant :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section1-step1-3.png)

## <a name="creating-the-azure-language-understanding-resource"></a>Création de la ressource Azure Language Understanding

Dans cette section, vous allez créer une ressource de prédiction Azure pour l’application LUIS (Language Understanding Intelligent Service) que vous allez créer dans la section suivante.

Connectez-vous à <a href="https://portal.azure.com" target="_blank">Azure</a>, puis cliquez sur **Créer une ressource**. Ensuite, recherchez et sélectionnez **Language Understanding** :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section2-step1-1.png)

Cliquez sur le bouton **Créer** pour créer une instance de ce service :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section2-step1-2.png)

Dans la page Créer, cliquez sur l’option **Prédiction** et entrez les valeurs suivantes :

* Pour **Abonnement**, sélectionnez **Essai gratuit** si vous disposez d’un abonnement à l’essai, sinon, sélectionnez l’un de vos autres abonnements.
* Pour **Groupe de ressource**, cliquez sur le lien **Créer nouveau**, entrez un nom approprié, par exemple *MRKT-Tutorials*, puis cliquez sur **OK**.

![mrlearning-speech](images/mrlearning-speech/tutorial4-section2-step1-3.png)

> [!NOTE]
> Au moment de la rédaction de cet article, vous n’avez pas besoin de créer une ressource de création, car une clé d’essai de création est automatiquement générée dans LUIS quand vous créez l’application LUIS (Language Understanding Intelligent Service) dans la section suivante.

> [!TIP]
> Si vous avez déjà un autre groupe de ressources approprié dans votre compte Azure, par exemple, si vous avez suivi le tutoriel [Azure Spatial Anchors](mrlearning-asa-ch1.md), vous pouvez utiliser ce groupe de ressources au lieu d’en créer un.

Toujours dans la page Créer, entrez les valeurs suivantes :

* Pour **Nom**, entrez un nom approprié pour le service, par exemple, *MRTK-Tutorials-AzureSpeechServices*.
* Pour **Emplacement de prédiction**, choisissez un emplacement proche de l’emplacement physique des utilisateurs de votre application, par exemple, *USA Ouest*.
* Pour **Niveau tarifaire de prédiction**, dans le cadre de ce tutoriel, sélectionnez **F0 (5 appels par seconde, 10 000 appels par mois)**

![mrlearning-speech](images/mrlearning-speech/tutorial4-section2-step1-4.png)

Accédez ensuite à l’onglet **Vérifier + créer**, passez en revue les détails, puis cliquez sur le bouton **Créer**, situé au bas de la page, pour créer la ressource, ainsi que le nouveau groupe de ressources si vous en avez créé un :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section2-step1-5.png)

> [!NOTE]
> Après avoir cliqué sur le bouton Créer, vous devez attendre que le service soit créé, ce qui peut prendre quelques minutes.

Une fois le processus de création de la ressource terminé, le message **Votre déploiement a été effectué** s’affiche :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section2-step1-6.png)

## <a name="creating-the-language-understanding-intelligent-service-luis"></a>Création de l’application LUIS (Language Understanding Intelligent Service)

Dans cette section, vous allez créer une application LUIS, configurer et entraîner son modèle de prédiction, puis la connecter à la ressource de prédiction Azure que vous avez créée à l’étape précédente.

Plus précisément, vous allez créer une intention qui veut que, si l’utilisateur déclare qu’une action doit être effectuée, l’application déclenche l’événement Interactable.OnClick() sur l’un des trois boutons rouges de la scène, en fonction de celui auquel l’utilisateur fait référence.

Par exemple, si l’utilisateur dit **procéder au lancement de la fusée**, l’application va prédire que **procéder** implique une **action** à effectuer, et que l’événement Interactable.OnClick() à **cibler** se trouve sur le bouton de **lancement**.

Voici les principales étapes à suivre pour y parvenir :

1. Créer une application LUIS
2. Créer des intentions
3. Créer des exemples d’énoncés
4. Créer des entités
5. Attribuer des entités aux exemples d’énoncés
6. Entraîner, tester et publier l’application
7. Attribuer une ressource de prédiction Azure à l’application

### <a name="1-create-a-luis-app"></a>1. Créer une application LUIS

À l’aide du même compte d’utilisateur que celui que vous avez utilisé pour créer la ressource Azure dans la section précédente, connectez-vous à <a href="https://www.luis.ai" target="_blank">LUIS</a>, sélectionnez votre pays et acceptez les conditions d’utilisation. À l’étape suivante, lorsque vous êtes invité à **lier votre compte Azure**, choisissez **Continuer à utiliser votre clé d’essai**, pour utiliser une ressource de création Azure à la place.

> [!NOTE]
> Si vous êtes déjà inscrit à LUIS et que votre clé d’essai de création a expiré, vous pouvez consulter la documentation [Migrer vers une clé de création de ressource Azure](https://docs.microsoft.com/azure/cognitive-services/luis/luis-migration-authoring) pour basculer votre ressource de création LUIS vers Azure.

Une fois connecté, accédez à la page **Mes applications**, puis cliquez sur **Créer une application** et entrez les valeurs suivantes dans la fenêtre contextuelle **Créer une application** :

* Pour **Nom**, entrez un nom approprié, par exemple, *MRTK Tutorials - AzureSpeechServices*.
* Pour **Culture**, sélectionnez **Anglais**.
* Pour **Description**, entrez éventuellement une description appropriée.

Cliquez ensuite sur le bouton **Terminé** pour créer l’application :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step1-1.png)

Une fois l’application créée, vous êtes dirigé vers sa page **Tableau de bord** :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step1-2.png)

### <a name="2-create-intents"></a>2. Créer des intentions

À partir de la page Tableau de bord, accédez à la page Générer > Ressources d’application > **Intentions**, puis cliquez sur **Créer une intention** et entrez la valeur suivante dans la fenêtre contextuelle **Créer une intention** :

* Pour **Nom de l’intention**, entrez **PressButton**.

Cliquez ensuite sur le bouton **Terminé** pour créer l’intention :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step2-1.png)

> [!CAUTION]
> Dans le cadre de ce tutoriel, votre projet Unity va référencer cette intention par son nom, c.-à-d. « PressButton ». Il est donc extrêmement important de nommer votre intention de manière strictement identique.

Une fois l’intention créée, vous êtes dirigé vers sa page :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step2-2.png)

### <a name="3-create-example-utterances"></a>3. Créer des exemples d’énoncés

À la liste des **exemples d’énoncés** de l’intention **PressButton**, ajoutez les exemples d’énoncés suivants :

* activer la séquence de lancement
* me montrer un indicateur de placement
* démarrer la séquence de lancement
* appuyer sur le bouton des indicateurs de placement
* me donner un indicateur
* appuyer sur le bouton de lancement
* j’ai besoin d’un indicateur
* appuyer sur le bouton de réinitialisation
* délai de réinitialisation de l’expérience
* procéder au lancement de la fusée

Une fois que tous les exemples d’énoncés ont été ajoutés, la page de l’intention PressButton doit ressembler à ceci :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step3-1.png)

> [!CAUTION]
> Dans le cadre de ce tutoriel, votre projet Unity va référencer les mots « indicateur », « indicateurs » « réinitialisation » et « lancement ». Il est donc extrêmement important de prononcer ces mots exactement de la même façon.

### <a name="4-create-entities"></a>4. Créer des entités

À partir de la page de l’intention PressButton, accédez à la page Générer > Ressources d’application > **Entités**, puis cliquez sur **Créer une entité** et entrez les valeurs suivantes dans la fenêtre contextuelle **Créer une entité** :

* Pour **Nom de l’entité**, entrez **Action**.
* Pour **Type d’entité**, sélectionnez **Simple**.

Cliquez ensuite sur le bouton **Terminé** pour créer l’entité :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step4-1.png)

**Répétez** l’étape précédente pour créer une autre entité nommée **Cible**. Vous avez donc deux entités nommées Action et Cible :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step4-2.png)

> [!CAUTION]
> Dans le cadre de ce tutoriel, votre projet Unity va référencer ces entités par leurs noms, c.-à-d. « Action » et « Cible ». Il est donc extrêmement important de nommer vos entités de manière strictement identique.

### <a name="5-assign-entities-to-the-example-utterances"></a>5. Attribuer des entités aux exemples d’énoncés

À partir de la page Entités, revenez à la page de l’intention **PressButton**.

Dans cette page, cliquez sur le mot **procéder** et sur le mot **au**, puis sélectionnez **Action (Simple)** dans le menu contextuel pour étiqueter **procéder au** comme valeur d’entité **Action** :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step5-1.png)

La locution **procéder au** est maintenant définie en tant que valeur d’entité **Action**. Si vous placez le curseur de la souris au-dessus du nom de l’entité Action, vous pouvez voir la valeur d’entité Action associée :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step5-2.png)

> [!NOTE]
> La ligne rouge qui apparaît sous l’étiquette dans l’image ci-dessus indique que la valeur d’entité n’a pas été prédite, ce que vous allez résoudre quand vous entraînerez le modèle dans la section suivante.

Ensuite, cliquez sur le mot **lancement**, puis sélectionnez **Cible (Simple)** dans le menu contextuel pour étiqueter **lancement** comme valeur d’entité **Cible** :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step5-3.png)

Le mot **lancement** est maintenant défini en tant que valeur d’entité **Cible**. Si vous placez le curseur de la souris au-dessus du nom de l’entité Cible, vous pouvez voir la valeur d’entité Cible associée :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step5-4.png)

L’exemple d’énoncé de l’intention PressButton « procéder au lancement de la fusée » est maintenant configuré pour être prédit ainsi :

* Intention : PressButton
* Entité Action : procéder au
* Entité Cible : lancement

**Répétez** le processus en deux étapes précédent pour attribuer une étiquette d’entité Action et Cible à chacun des exemples d’énoncés, en gardant à l’esprit que les mots suivants doivent être étiquetés comme des entités **Cible** :

* **indicateur** (Cible HintsButton dans le projet Unity.)
* **indicateurs** (Cible HintsButton dans le projet Unity.)
* **réinitialisation** (Cible ResetButton dans le projet Unity.)
* **lancement** (Cible LaunchButton dans le projet Unity.)

Une fois que tous les exemples d’énoncés ont été étiquetés, la page de l’intention PressButton doit ressembler à ceci :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step5-5.png)

Pour revérifier que vous avez attribué les entités appropriées, cliquez sur le menu **Options d’affichage** et basculez l’affichage en mode **Afficher les valeurs d’entité** :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step5-6.png)

Maintenant, avec l’affichage défini de sorte à montrer les valeurs d’entité, vous pouvez placer le pointeur de la souris sur les mots et locutions étiquetés pour vérifier rapidement le nom de l’entité affectée :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step5-7.png)

### <a name="6-train-test-and-publish-the-app"></a>6. Entraîner, tester et publier l’application

Pour entraîner l’application, cliquez sur le bouton **Entraîner** et attendez que le processus d’entraînement se termine :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step6-1.png)

> [!NOTE]
> Comme vous pouvez le voir dans l’image ci-dessus, les lignes rouges situées sous toutes les étiquettes ont été supprimées, ce qui indique que toutes les valeurs d’entité ont été prédites. Remarquez également que l’icône d’état à gauche du bouton Entraîner est passée du rouge au vert.

Une fois le processus d’entraînement terminé, cliquez sur le bouton **Tester**, puis tapez **procéder au lancement de la fusée** et appuyez sur la touche Entrée :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step6-2.png)

Une fois l’énoncé de test traité, cliquez sur **Inspecter** pour voir le résultat du test :

* Intention : PressButton (avec une certitude de 98,5 %)
* Entité Action : procéder au
* Entité Cible : lancement

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step6-3.png)

Pour publier l’application, cliquez sur le bouton **Publier** situé en haut à droite, puis dans la fenêtre contextuelle **Choisir l’emplacement et les paramètres de publication**, sélectionnez **Production** et cliquez sur le bouton **Publier** :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step6-4.png)

Attendez que le processus de publication se termine :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step6-5.png)

### <a name="7-assign-an-azure-prediction-resource-to-the-app"></a>7. Attribuer une ressource de prédiction Azure à l’application

Accédez à la page Gérer > Paramètres d’application >  **Ressources Azure** :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step7-1.png)

Dans la page Ressources Azure, cliquez sur le bouton **Ajouter une ressource de prédiction** et sélectionnez les valeurs suivantes dans la fenêtre contextuelle **Attribuer une ressource à votre application** :

* Pour **Nom du locataire**, sélectionnez le nom de votre locataire.
* Pour **Nom de l’abonnement**, sélectionnez l’abonnement que vous avez utilisé précédemment lors de la [création de la ressource Azure Language Understanding](mrlearning-speechSDK-ch4.md#creating-the-azure-language-understanding-resource).
* Pour **Nom de la ressource LUIS**, sélectionnez la ressource de prédiction que vous avez créée précédemment lors de la [création de la ressource Azure Language Understanding](mrlearning-speechSDK-ch4.md#creating-the-azure-language-understanding-resource).

Cliquez ensuite sur le bouton **Attribuer la ressource** pour attribuer la ressource de prédiction Azure à votre application :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step7-2.png)

Une fois la ressource attribuée, votre page Ressources Azure doit ressembler à ceci :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section3-step7-3.png)

## <a name="connecting-the-unity-project-to-the-luis-app"></a>Connexion du projet Unity à l’application LUIS

Dans la page Gérer > Paramètres d’application > **Ressources Azure**, cliquez sur l’icône **Copier** pour copier l’**exemple de requête** :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section4-step1-1.png)

De retour dans votre projet Unity, dans la fenêtre Hierarchy, sélectionnez l’objet **Lunarcom**, puis dans la fenêtre Inspector, localisez le composant **Lunarcom Intent Recognizer (Script)** et configurez-le de la façon suivante :

* Dans le champ **LUIS Endpoint**, collez l’**exemple de requête** que vous avez copié à l’étape précédente :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section4-step1-2.png)

## <a name="testing-and-improving-the-intent-recognition"></a>Test et amélioration de la reconnaissance de l’intention

Pour utiliser la reconnaissance de l’intention directement dans l’éditeur Unity, vous devez autoriser votre ordinateur de développement à utiliser la dictée. Pour vérifier ce paramètre, ouvrez **Paramètres Windows**, puis choisissez **Confidentialité** > **Voix** et vérifiez que l’option **Reconnaissance vocale en ligne** est activée :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section5-step1-1.png)

Si vous entrez maintenant en mode Game, vous pouvez tester la reconnaissance de l’intention en commençant par appuyer sur le bouton de la fusée. Ensuite, en supposant que votre ordinateur est doté d’un microphone, quand vous prononcez le premier exemple d’énoncé, **procéder au lancement de la fusée**, vous pouvez voir le lancement du module lunaire dans l’espace :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section5-step1-2.png)

Testez tous les **exemples d’énoncés**, puis quelques **variations des exemples d’énoncés**, ainsi que quelques **énoncés aléatoires**.

Ensuite, revenez à <a href="https://www.luis.ai" target="_blank">LUIS</a> et accédez à la page Générer > Améliorer les performances de l’application > **Vérifier les énoncés de point de terminaison**, utilisez le bouton **bascule** pour passer de l’affichage des entités par défaut à celui des **jetons**, puis vérifiez les énoncés :

* Dans la colonne **Énoncé**, modifiez et supprimez les étiquettes attribuées en fonction des besoins pour les adapter à votre intention.
* Dans la colonne **Intention alignée**, vérifiez que l’intention est correcte.
* Dans la colonne **Ajouter/Supprimer**, cliquez sur la coche verte pour ajouter l’énoncé ou sur le x rouge pour le supprimer.

Quand vous avez vérifié autant d’énoncés que vous le voulez, cliquez sur le bouton **Entraîner** pour entraîner de nouveau le modèle, puis sur le bouton **Publier** pour republier l’application mise à jour :

![mrlearning-speech](images/mrlearning-speech/tutorial4-section5-step1-3.png)

> [!NOTE]
> Si un énoncé de point de terminaison ne correspond pas à l’intention PressButton, mais que vous voulez que votre modèle sache que cet énoncé n’a aucune intention, vous pouvez définir l’option Intention alignée sur Aucune.

**Répétez** ce processus autant de fois que vous le souhaitez pour améliorer votre modèle d’application.

## <a name="congratulations"></a>Félicitations

Votre projet comporte désormais des commandes vocales optimisées par l’IA, ce qui permet à votre application de reconnaître l’intention des utilisateurs même s’ils ne prononcent pas des commandes précises. Exécutez l’application sur votre appareil pour vérifier que tout fonctionne bien.
