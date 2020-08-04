---
title: Tutoriels sur le cloud Azure - 5. Intégration d’Azure Bot Service avec LUIS
description: Suivez ce cours pour découvrir comment implémenter Azure Bot Service et la compréhension du langage naturel dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens, hololens 2, azure bot service, luis, langage naturel, chatbot
ms.localizationpriority: high
ms.openlocfilehash: daf97cde1477a84c1776a069ec5b8d1a185b63cc
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376451"
---
# <a name="5-integrating-azure-bot-service"></a>5. Intégration d’Azure Bot Service

Dans ce tutoriel, vous allez apprendre à utiliser **Azure Bot Service** dans l’application de démonstration **HoloLens 2** pour ajouter LUIS (Language Understanding) et laisser le bot assister l’utilisateur lors de la recherche d’**objets suivis**. Il s’agit d’un tutoriel en deux parties. Dans la première, vous allez créer le bot avec la solution sans code [Bot Composer](https://docs.microsoft.com/composer/introduction), et examiner la fonction Azure qui alimente le bot avec les données nécessaires. Dans la deuxième partie, vous utiliserez le **BotManager (script)** dans le projet Unity pour consommer le service bot hébergé.

## <a name="objectives"></a>Objectifs

## <a name="part-1"></a>Partie 1

* Apprendre les bases d’Azure Bot Service
* Apprendre à utiliser Bot Composer pour créer un bot
* Apprendre à utiliser une fonction Azure pour fournir des données à partir de Stockage Azure

## <a name="part-2"></a>Partie 2

* Apprendre à configurer la scène pour utiliser Azure Bot Service dans ce projet
* Apprendre à définir et rechercher des objets par le biais de la conversation avec le bot

## <a name="understanding-azure-bot-service"></a>Présentation d’Azure Bot Service

**Azure Bot Service** permet aux développeurs de créer des bots intelligents capables de maintenir une conversation naturelle avec les utilisateurs grâce à **LUIS**. Un chatbot est un excellent moyen d’étendre les façons dont un utilisateur peut interagir avec votre application. Un bot peut faire office de base de connaissances avec un [QnA Marker](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-qna?view=azure-bot-service-4.0&tabs=cs) afin de maintenir une conversation sophistiquée grâce à la puissance de [LUIS (Language Understanding)](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-v4-luis?view=azure-bot-service-4.0&tabs=csharp).

Apprenez-en davantage sur [Azure Bot Service](https://docs.microsoft.com/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0).

## <a name="part-1---creating-the-bot"></a>Partie 1 : Création du bot

Avant de pouvoir utiliser le bot dans l’application Unity, vous devez le développer, lui fournir des données et l’héberger sur **Azure**.
L’objectif du bot est de pouvoir indiquer combien d’*objets suivis* sont stockés dans la base de données, de trouver un *objet suivi* d’après son nom, et de fournir à l’utilisateur certaines informations élémentaires à son sujet.

### <a name="a-quick-look-into-tracked-objects-azure-function"></a>Présentation rapide de Tracked Objects Azure Function

Vous êtes sur le point de créer le bot, mais pour qu’il soit utile, vous devez lui donner une ressource à partir de laquelle il peut extraire des données. Étant donné que le *bot* sera capable de compter le nombre d’**objets suivis**, de rechercher des objets spécifiques en fonction de leur nom et d’en indiquer les détails, vous allez utiliser une fonction Azure simple qui a accès au **stockage Table Azure**.

Téléchargez le projet de fonction Azure intitulé [Tracked Objects Azure Function](https://github.com/microsoft/MixedRealityLearning/releases/download/a-tag/AzureFunction_TrackedObjectsService.zip)

Cette fonction Azure a deux actions, **Count** et **Find**, qui peuvent être appelées par le biais d’appels *GET* *HTTP* simples. Vous pouvez inspecter le code dans **Visual Studio**.

Apprenez-en davantage sur [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview).

La fonction **Count** est très simple : elle interroge à partir du **stockage Table** tous les **TrackedObjects** de la table. La fonction **Find**, quant à elle, prend un paramètre de requête *name* à partir de la requête *GET*, interroge le **stockage Table** pour obtenir un **TrackedObject** correspondant et retourne un DTO au format JSON.

Vous pouvez déployer cette **fonction Azure** directement à partir de **Visual Studio**.
Vous trouverez toutes les informations relatives au déploiement de fonction Azure [ici](https://docs.microsoft.com/azure/devops/pipelines/targets/azure-functions?view=azure-devops&tabs=dotnet-core%2Cyaml).

Une fois le déploiement terminé, dans le **portail Azure**, ouvrez la ressource correspondante et cliquez sur **Configuration** dans la section *Paramètres*. Dans les **Paramètres d’application**, vous devez fournir la *Chaîne de connexion* au **Stockage Azure** où sont stockés les **objets suivis**. Cliquez sur **Nouveau paramètre d’application** et spécifiez **AzureStorageConnectionString** comme nom. En guise de valeur, spécifiez la *Chaîne de connexion* correcte. Après cela, cliquez sur **Enregistrer**. La **fonction Azure** est prête pour le *bot* que vous allez maintenant créer.

### <a name="creating-a-conversation-bot"></a>Création d’un chatbot

Il existe plusieurs façons de développer un chatbot basé sur le Bot Framework. Dans cette leçon, vous allez utiliser l’application de bureau [Bot Framework Composer](https://docs.microsoft.com/composer/), un concepteur visuel idéal pour le développement rapide.

Vous pouvez télécharger les dernières versions à partir du [dépôt GitHub](https://github.com/microsoft/BotFramework-Composer/releases). Il est disponible pour Windows, Mac et Linux.

Une fois **Bot Framework Composer** installé, démarrez l’application. L’interface suivante doit s’afficher :

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-1.png)

Vous avez préparé un projet bot composer qui fournit les dialogues et les déclencheurs nécessaires pour ce tutoriel.
Téléchargez le projet : [Projet Bot Framework Composer](https://github.com/microsoft/MixedRealityLearning/releases/download/a-tag/BotComposerProject_TrackedObjectsBot.zip)

Dans la barre supérieure, cliquez sur **Open** et sélectionnez le projet Bot Framework que vous avez téléchargé, nommé **TrackedObjectsBot**. Une fois le projet entièrement chargé, il est prêt à l’emploi.

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-2.png)

Concentrons-nous sur le côté gauche, où vous pouvez voir le **volet des dialogues**. Vous avez un dialogue nommé **TrackedObjectsBot** sous lequel figurent plusieurs **déclencheurs**.

Apprenez-en davantage sur les [concepts de Bot Framework](https://docs.microsoft.com/composer/concept-dialog).

Ces déclencheurs effectuent les opérations suivantes :

#### <a name="greeting"></a>Greeting

Il s’agit du point d’entrée du *chatbot* chaque fois qu’un *utilisateur* démarre une conversation.

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-3.png)

#### <a name="askingforcount"></a>AskingForCount

Ce dialogue est déclenché quand l’*utilisateur* demande le comptage de tous les **objets suivis**.
Voici les expressions de déclenchement :

>* count me all
>* how many are stored

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-4.png)

Grâce à [LUIS](https://docs.microsoft.com/composer/how-to-use-luis), l’*utilisateur* n’a pas besoin d’énoncer les expressions de cette manière exacte. La conversation est ainsi plus naturelle.

Dans ce dialogue, le *bot* communiquera également avec la fonction Azure **Count** (nous y reviendrons).

#### <a name="unknown-intent"></a>Unknown Intent

Ce dialogue est déclenché si l’entrée de l’*utilisateur* ne correspond à aucune autre condition de déclencheur. L’utilisateur est invité à reposer sa question.

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-5.png)

#### <a name="findentity"></a>FindEntity

Le dernier dialogue est plus complexe. Il implique une ramification et le stockage des données dans la *mémoire* du bot.
Il demande à l’utilisateur le *nom* de l’**objet suivi** au sujet duquel il souhaite en savoir plus, exécute une requête sur la fonction Azure **Find**, et utilise la réponse pour poursuivre la conversation.

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-6.png)

Si l’**objet suivi** est introuvable, l’utilisateur en est informé et la conversation se termine. Quand l’**objet suivi** en question est trouvé, le bot vérifie et signale quelles propriétés sont disponibles.

### <a name="adapting-the-bot"></a>Adaptation du bot

Les déclencheurs **AskingForCount** et **FindEntity** doivent communiquer avec le back-end. Cela signifie que vous devez ajouter l’URL correcte de la **fonction Azure** déployée précédemment.

Dans le volet de dialogue, cliquez sur **AskingForCount** et recherchez l’action *Send an HTTP request* (Envoyer une requête HTTP). Ici, vous pouvez voir le champ **URL**, dans lequel vous devez indiquer l’URL correcte du point de terminaison de la fonction **Count**.

![mr-learning-azure](images/mr-learning-azure/tutorial5-section5-step1-1.png)

Pour finir, recherchez le déclencheur **FindEntity** et l’action *Send an HTTP request*. Dans le champ **URL**, indiquez l’URL du point de terminaison de la fonction **Find**.

![mr-learning-azure](images/mr-learning-azure/tutorial5-section5-step1-2.png)

Vous êtes maintenant prêt à déployer le bot. Bot Framework Composer étant installé, vous pouvez publier le bot directement à partir de là.

Apprenez-en davantage sur la [publication d’un bot à partir de Bot Composer](https://docs.microsoft.com/composer/how-to-publish-bot).

> [!TIP]
> N’hésitez pas à vous amuser avec le bot en ajoutant des expressions de déclencheur ou de nouvelles réponses, ou en créant des branches de conversation.

## <a name="part-2---putting-everything-together-in-unity"></a>Partie 2 : Assemblage final dans Unity

### <a name="preparing-the-scene"></a>Préparation de la scène

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.AzureCloudServices** > **Prefabs** > **Manager**.

![mr-learning-azure](images/mr-learning-azure/tutorial5-section6-step1-1.png)

À partir de là, déplacez le préfabriqué **ChatBotManager** dans la hiérarchie de la scène.

Une fois que vous avez ajouté le ChatBotManager à la scène, cliquez sur le composant **Chat Bot Manager**.
Dans l’inspecteur, vous verrez qu’il existe un champ vide **Direct Line Secret Key** (Clé secrète directe) que vous devez renseigner.

> [!TIP]
> Vous pouvez récupérer la *clé secrète* à partir du portail Azure en recherchant la ressource de type **Inscription de chaînes de bot** que vous avez créée dans la première partie de ce tutoriel.

![mr-learning-azure](images/mr-learning-azure/tutorial5-section6-step1-2.png)

À présent, vous allez connecter l’objet **ChatBotManager** avec le composant **ChatBotController** attaché à l’objet **ChatBotPanel**. Dans la hiérarchie, sélectionnez le **ChatBotPanel**. Vous verrez un champ vide **Chat Bot Manager**. Faites glisser l’objet **ChatBotManager** de la hiérarchie vers le champ vide **Chat Bot Manager**.

![mr-learning-azure](images/mr-learning-azure/tutorial5-section6-step1-3.png)

Ensuite, vous avez besoin d’un moyen d’ouvrir le **ChatBotPanel** afin que l’utilisateur puisse interagir avec lui. Dans la fenêtre de scène, vous avez peut-être remarqué la présence d’un bouton latéral *Chat Bot* sur l’objet **MainMenu**. Vous l’utiliserez pour résoudre ce problème.

Dans la hiérarchie, recherchez **RootMenu** > **MainMenu** > **SideButtonCollection** > **ButtonChatBot**, puis recherchez le script *ButtonConfigHelper* dans l’inspecteur. Vous verrez un emplacement vide sur le rappel d’événement **OnClick()** . Glissez-déposez le **ChatBotPanel** sur l’emplacement d’événement. Dans la liste déroulante, accédez à *GameObject*, sélectionnez *SetActive (bool)* dans le sous-menu et cochez la case.

![mr-learning-azure](images/mr-learning-azure/tutorial5-section6-step1-4.png)

Maintenant, le chatbot peut être démarré à partir du menu principal et la scène est prête à être utilisée.

### <a name="putting-the-bot-to-a-test"></a>Tester le bot

#### <a name="asking-about-the-quantity-of-tracked-objects"></a>Demander la quantité d’objets suivis

Tout d’abord, nous allons demander au bot combien d’**objets suivis** sont stockés dans la base de données.

> [!NOTE]
> Cette fois, vous devez exécuter l’application à partir d’HoloLens 2, car il se peut que des services comme *Synthèse vocale* ne soient pas disponibles sur votre système.

Exécutez l’application sur votre HoloLens 2, puis cliquez sur le bouton *Chat Bot* à côté du menu principal.
Après avoir été salué par le bot, posez-lui la question **how many objects do we have?** (combien d’objets avons-nous ?).
Il doit vous indiquer la quantité et mettre fin à la conversation.

#### <a name="asking-about-a-tracked-object"></a>Poser une question sur un objet suivi

Réexécutez l’application, mais cette fois-ci demandez **find me a tracked object** (trouvez-moi un objet suivi). Le bot vous demandera le nom. Répondez « car » ou donnez le nom d’un autre *objet suivi* qui existe dans la base de données. Le bot vous indiquera des détails tels que la description, et s’il a une ancre spatiale assignée.

> [!TIP]
> Essayez de demander un **objet suivi** qui n’existe pas et découvrez comment le bot répond.

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez découvert comment utiliser Azure Bot Framework pour interagir avec l’application dans une conversation en langage naturel. Vous avez découvert comment développer votre propre bot et quels sont les différents éléments nécessaires à son fonctionnement.

## <a name="conclusion"></a>Conclusion

Tout au long de cette série de tutoriels, vous avez vu comment enrichir votre application de fonctionnalités nouvelles et passionnantes grâce aux **services cloud Azure**.
Vous pouvez désormais stocker des données et des images dans le cloud avec **Stockage Azure**, utiliser **Azure Custom Vision** pour associer des images et entraîner un modèle, placer des objets dans un contexte local avec **Azure Spatial Anchors**, et implémenter **Azure Bot Framework avec LUIS** pour ajouter un chatbot et obtenir un nouveau modèle d’interaction naturelle.
