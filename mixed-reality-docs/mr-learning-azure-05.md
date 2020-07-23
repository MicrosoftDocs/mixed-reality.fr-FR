---
title: Tutoriels sur le cloud Azure - 5. Intégration d’Azure Bot Service avec LUIS
description: Suivez ce cours pour découvrir comment implémenter Azure Bot Service et la compréhension du langage naturel dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens, hololens 2, azure bot service, luis, langage naturel, chatbot
ms.localizationpriority: high
ms.openlocfilehash: e3a64488b1d6d22ac52f798fe90356ce8e995e26
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86305574"
---
# <a name="5-integrating-azure-bot-service"></a><span data-ttu-id="890b3-105">5. Intégration d’Azure Bot Service</span><span class="sxs-lookup"><span data-stu-id="890b3-105">5. Integrating Azure Bot Service</span></span>

<span data-ttu-id="890b3-106">Dans ce tutoriel, vous allez apprendre à utiliser **Azure Bot Service** dans l’application de démonstration **HoloLens 2** pour ajouter LUIS (Language Understanding) et laisser le bot assister l’utilisateur lors de la recherche d’**objets suivis**.</span><span class="sxs-lookup"><span data-stu-id="890b3-106">In this tutorial, you will learn how to use **Azure Bot Service** in the **HoloLens 2** demo application to add Language Understanding (LUIS) and letting the Bot assist the user when searching for **Tracked Objects**.</span></span> <span data-ttu-id="890b3-107">Il s’agit d’un tutoriel en deux parties. Dans la première, vous allez créer le bot avec la solution sans code [Bot Composer](https://docs.microsoft.com/composer/introduction), et examiner la fonction Azure qui alimente le bot avec les données nécessaires.</span><span class="sxs-lookup"><span data-stu-id="890b3-107">This is a two part tutorial where in the first part you create the Bot with the [Bot Composer](https://docs.microsoft.com/composer/introduction) as a code free solution and take a quick look in the Azure Function that feeds the Bot with the needed data.</span></span> <span data-ttu-id="890b3-108">Dans la deuxième partie, vous utiliserez le **BotManager (script)** dans le projet Unity pour consommer le service bot hébergé.</span><span class="sxs-lookup"><span data-stu-id="890b3-108">In the second part you use the **BotManager (script)** in the Unity project to consume the hosted Bot Service.</span></span>

## <a name="objectives"></a><span data-ttu-id="890b3-109">Objectifs</span><span class="sxs-lookup"><span data-stu-id="890b3-109">Objectives</span></span>

## <a name="part-1"></a><span data-ttu-id="890b3-110">Partie 1</span><span class="sxs-lookup"><span data-stu-id="890b3-110">Part 1</span></span>

* <span data-ttu-id="890b3-111">Apprendre les bases d’Azure Bot Service</span><span class="sxs-lookup"><span data-stu-id="890b3-111">Learn the basics about Azure Bot Service</span></span>
* <span data-ttu-id="890b3-112">Apprendre à utiliser Bot Composer pour créer un bot</span><span class="sxs-lookup"><span data-stu-id="890b3-112">Learn how to use the Bot Composer to create a Bot</span></span>
* <span data-ttu-id="890b3-113">Apprendre à utiliser une fonction Azure pour fournir des données à partir de Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="890b3-113">Learn how to use an Azure Function to provide data from the Azure Storage</span></span>

## <a name="part-2"></a><span data-ttu-id="890b3-114">Partie 2</span><span class="sxs-lookup"><span data-stu-id="890b3-114">Part 2</span></span>

* <span data-ttu-id="890b3-115">Apprendre à configurer la scène pour utiliser Azure Bot Service dans ce projet</span><span class="sxs-lookup"><span data-stu-id="890b3-115">Learn how to setup the scene to use Azure Bot Service in this project</span></span>
* <span data-ttu-id="890b3-116">Apprendre à définir et rechercher des objets par le biais de la conversation avec le bot</span><span class="sxs-lookup"><span data-stu-id="890b3-116">Learn how to set and find objects via conversing with the Bot</span></span>

## <a name="understanding-azure-bot-service"></a><span data-ttu-id="890b3-117">Présentation d’Azure Bot Service</span><span class="sxs-lookup"><span data-stu-id="890b3-117">Understanding Azure Bot Service</span></span>

<span data-ttu-id="890b3-118">**Azure Bot Service** permet aux développeurs de créer des bots intelligents capables de maintenir une conversation naturelle avec les utilisateurs grâce à **LUIS**.</span><span class="sxs-lookup"><span data-stu-id="890b3-118">The **Azure Bot Service** empowers developers to create intelligent bots that can maintain natural conversation with users thanks to **LUIS**.</span></span> <span data-ttu-id="890b3-119">Un chatbot est un excellent moyen d’étendre les façons dont un utilisateur peut interagir avec votre application.</span><span class="sxs-lookup"><span data-stu-id="890b3-119">A conversational Bot is a great way to expand the ways a user can interact with your application.</span></span> <span data-ttu-id="890b3-120">Un bot peut faire office de base de connaissances avec un [QnA Marker](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-qna?view=azure-bot-service-4.0&tabs=cs) afin de maintenir une conversation sophistiquée grâce à la puissance de [LUIS (Language Understanding)](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-v4-luis?view=azure-bot-service-4.0&tabs=csharp).</span><span class="sxs-lookup"><span data-stu-id="890b3-120">A Bot can act as a knowledge base with a [QnA Marker](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-qna?view=azure-bot-service-4.0&tabs=cs) to maintaining sophisticated conversation with the power of [Language Understanding (LUIS)](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-v4-luis?view=azure-bot-service-4.0&tabs=csharp).</span></span>

<span data-ttu-id="890b3-121">Apprenez-en davantage sur [Azure Bot Service](https://docs.microsoft.com/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0).</span><span class="sxs-lookup"><span data-stu-id="890b3-121">Learn more about [Azure Bot Service](https://docs.microsoft.com/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0).</span></span>

## <a name="part-1---creating-the-bot"></a><span data-ttu-id="890b3-122">Partie 1 : Création du bot</span><span class="sxs-lookup"><span data-stu-id="890b3-122">Part 1 - Creating the Bot</span></span>

<span data-ttu-id="890b3-123">Avant de pouvoir utiliser le bot dans l’application Unity, vous devez le développer, lui fournir des données et l’héberger sur **Azure**.</span><span class="sxs-lookup"><span data-stu-id="890b3-123">Before you can use the bot in the Unity application, you need to develope it, provide it with data and host it on **Azure**.</span></span>
<span data-ttu-id="890b3-124">L’objectif du bot est de pouvoir indiquer combien d’*objets suivis* sont stockés dans la base de données, de trouver un *objet suivi* d’après son nom, et de fournir à l’utilisateur certaines informations élémentaires à son sujet.</span><span class="sxs-lookup"><span data-stu-id="890b3-124">The goal of the bot is to have the abilities to tell how many *Tracked Objects* are stored in the database, find a *Tracked Object* by its name, and tell the user some basic information about it.</span></span>

### <a name="a-quick-look-into-tracked-objects-azure-function"></a><span data-ttu-id="890b3-125">Présentation rapide de Tracked Objects Azure Function</span><span class="sxs-lookup"><span data-stu-id="890b3-125">A quick look into Tracked Objects Azure Function</span></span>

<span data-ttu-id="890b3-126">Vous êtes sur le point de créer le bot, mais pour qu’il soit utile, vous devez lui donner une ressource à partir de laquelle il peut extraire des données.</span><span class="sxs-lookup"><span data-stu-id="890b3-126">You are about to start creating the Bot, but to make it useful you need to give it a resource from which it can pull data.</span></span> <span data-ttu-id="890b3-127">Étant donné que le *bot* sera capable de compter le nombre d’**objets suivis**, de rechercher des objets spécifiques en fonction de leur nom et d’en indiquer les détails, vous allez utiliser une fonction Azure simple qui a accès au **stockage Table Azure**.</span><span class="sxs-lookup"><span data-stu-id="890b3-127">Since the *Bot* will be able to count the amount of **Tracked Objects**, find specific ones by name and tell details, you will use a simple Azure Function that has access to the **Azure Table storage**.</span></span>

<span data-ttu-id="890b3-128">Téléchargez le projet de fonction Azure intitulé [Tracked Objects Azure Function](https://github.com/microsoft/MixedRealityLearning/releases/download/a-tag/AzureFunction_TrackedObjectsService.zip)</span><span class="sxs-lookup"><span data-stu-id="890b3-128">Download the Azure Function Project: [Tracked Objects Azure Function](https://github.com/microsoft/MixedRealityLearning/releases/download/a-tag/AzureFunction_TrackedObjectsService.zip)</span></span>

<span data-ttu-id="890b3-129">Cette fonction Azure a deux actions, **Count** et **Find**, qui peuvent être appelées par le biais d’appels *GET* *HTTP* simples.</span><span class="sxs-lookup"><span data-stu-id="890b3-129">This Azure Function has two actions, **Count** and **Find** which can be invoked via basic *HTTP* *GET* calls.</span></span> <span data-ttu-id="890b3-130">Vous pouvez inspecter le code dans **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="890b3-130">You can inspect the code in **Visual Studio**.</span></span>

<span data-ttu-id="890b3-131">Apprenez-en davantage sur [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span><span class="sxs-lookup"><span data-stu-id="890b3-131">Learn more about [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span></span>

<span data-ttu-id="890b3-132">La fonction **Count** est très simple : elle interroge à partir du **stockage Table** tous les **TrackedObjects** de la table.</span><span class="sxs-lookup"><span data-stu-id="890b3-132">The **Count** function queries from the **Table storage** all **TrackedObjects** from the table, very simple.</span></span> <span data-ttu-id="890b3-133">La fonction **Find**, quant à elle, prend un paramètre de requête *name* à partir de la requête *GET*, interroge le **stockage Table** pour obtenir un **TrackedObject** correspondant et retourne un DTO au format JSON.</span><span class="sxs-lookup"><span data-stu-id="890b3-133">On the other hand the **Find** function takes a *name* query parameter from the *GET* request and queries the **Table storage** for a matching **TrackedObject** and returns a DTO as JSON.</span></span>

<span data-ttu-id="890b3-134">Vous pouvez déployer cette **fonction Azure** directement à partir de **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="890b3-134">You can deploy this **Azure Function** directly from **Visual Studio**.</span></span>
<span data-ttu-id="890b3-135">Vous trouverez toutes les informations relatives au déploiement de fonction Azure [ici](https://docs.microsoft.com/azure/devops/pipelines/targets/azure-functions?view=azure-devops&tabs=dotnet-core%2Cyaml).</span><span class="sxs-lookup"><span data-stu-id="890b3-135">Find here all information regarding [Azure Function deployment](https://docs.microsoft.com/azure/devops/pipelines/targets/azure-functions?view=azure-devops&tabs=dotnet-core%2Cyaml).</span></span>

<span data-ttu-id="890b3-136">Une fois le déploiement terminé, dans le **portail Azure**, ouvrez la ressource correspondante et cliquez sur **Configuration** dans la section *Paramètres*.</span><span class="sxs-lookup"><span data-stu-id="890b3-136">Once you have completed the deployment, in the **Azure Portal**, open the corresponding resource and click on **Configuration** which is under the *Settings* section.</span></span> <span data-ttu-id="890b3-137">Dans les **Paramètres d’application**, vous devez fournir la *Chaîne de connexion* au **Stockage Azure** où sont stockés les **objets suivis**.</span><span class="sxs-lookup"><span data-stu-id="890b3-137">There on **Application Settings** you need to provide the *Connection string* to the **Azure Storage** where the **Tracked Objects** are stored.</span></span> <span data-ttu-id="890b3-138">Cliquez sur **Nouveau paramètre d’application** et spécifiez **AzureStorageConnectionString** comme nom. En guise de valeur, spécifiez la *Chaîne de connexion* correcte.</span><span class="sxs-lookup"><span data-stu-id="890b3-138">Click on **New Application setting** and use for name: **AzureStorageConnectionString** and for value provide the correct *Connection string*.</span></span> <span data-ttu-id="890b3-139">Après cela, cliquez sur **Enregistrer**. La **fonction Azure** est prête pour le *bot* que vous allez maintenant créer.</span><span class="sxs-lookup"><span data-stu-id="890b3-139">After that click on **Save** and the **Azure Function** is ready to server the *Bot* which you will create next.</span></span>

### <a name="creating-a-conversation-bot"></a><span data-ttu-id="890b3-140">Création d’un chatbot</span><span class="sxs-lookup"><span data-stu-id="890b3-140">Creating a conversation Bot</span></span>

<span data-ttu-id="890b3-141">Il existe plusieurs façons de développer un chatbot basé sur le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="890b3-141">There are several ways to develope a Bot Framework based conversational bot.</span></span> <span data-ttu-id="890b3-142">Dans cette leçon, vous allez utiliser l’application de bureau [Bot Framework Composer](https://docs.microsoft.com/composer/), un concepteur visuel idéal pour le développement rapide.</span><span class="sxs-lookup"><span data-stu-id="890b3-142">In this lesson you will use the [Bot Framework Composer](https://docs.microsoft.com/composer/) desktop application which is a visual designer that is perfect for rapid development.</span></span>

<span data-ttu-id="890b3-143">Vous pouvez télécharger les dernières versions à partir du [dépôt GitHub](https://github.com/microsoft/BotFramework-Composer/releases).</span><span class="sxs-lookup"><span data-stu-id="890b3-143">You can download the latest releases from the [Github repository](https://github.com/microsoft/BotFramework-Composer/releases).</span></span> <span data-ttu-id="890b3-144">Il est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="890b3-144">It is available for Windows, Mac, and Linux.</span></span>

<span data-ttu-id="890b3-145">Une fois **Bot Framework Composer** installé, démarrez l’application. L’interface suivante doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="890b3-145">Once the **Bot Framework Composer** is installed, start the application and you should see this interface:</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-1.png)

<span data-ttu-id="890b3-147">Vous avez préparé un projet bot composer qui fournit les dialogues et les déclencheurs nécessaires pour ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="890b3-147">You have prepared a bot composer project which provides the needed dialogues and triggers for this tutorial.</span></span>
<span data-ttu-id="890b3-148">Téléchargez le projet : [Projet Bot Framework Composer](https://github.com/microsoft/MixedRealityLearning/releases/download/a-tag/BotComposerProject_TrackedObjectsBot.zip)</span><span class="sxs-lookup"><span data-stu-id="890b3-148">Download the project: [Bot Framework Composer project](https://github.com/microsoft/MixedRealityLearning/releases/download/a-tag/BotComposerProject_TrackedObjectsBot.zip)</span></span>

<span data-ttu-id="890b3-149">Dans la barre supérieure, cliquez sur **Open** et sélectionnez le projet Bot Framework que vous avez téléchargé, nommé **TrackedObjectsBot**.</span><span class="sxs-lookup"><span data-stu-id="890b3-149">On the top bar click on **Open** and select the Bot Framework project you have downloaded which is named **TrackedObjectsBot**.</span></span> <span data-ttu-id="890b3-150">Une fois le projet entièrement chargé, il est prêt à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="890b3-150">After the project is fully loaded, you should see the project ready.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-2.png)

<span data-ttu-id="890b3-152">Concentrons-nous sur le côté gauche, où vous pouvez voir le **volet des dialogues**.</span><span class="sxs-lookup"><span data-stu-id="890b3-152">Let's focus on the left side where you can see the **Dialogs Panel**.</span></span> <span data-ttu-id="890b3-153">Vous avez un dialogue nommé **TrackedObjectsBot** sous lequel figurent plusieurs **déclencheurs**.</span><span class="sxs-lookup"><span data-stu-id="890b3-153">There you have one dialog named **TrackedObjectsBot** under which you can see several **Triggers**.</span></span>

<span data-ttu-id="890b3-154">Apprenez-en davantage sur les [concepts de Bot Framework](https://docs.microsoft.com/composer/concept-dialog).</span><span class="sxs-lookup"><span data-stu-id="890b3-154">Learn more about [Bot Framework concepts](https://docs.microsoft.com/composer/concept-dialog).</span></span>

<span data-ttu-id="890b3-155">Ces déclencheurs effectuent les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="890b3-155">These triggers do the following:</span></span>

#### <a name="greeting"></a><span data-ttu-id="890b3-156">Greeting</span><span class="sxs-lookup"><span data-stu-id="890b3-156">Greeting</span></span>

<span data-ttu-id="890b3-157">Il s’agit du point d’entrée du *chatbot* chaque fois qu’un *utilisateur* démarre une conversation.</span><span class="sxs-lookup"><span data-stu-id="890b3-157">This is the entry point of the chat *bot* when ever a *user* initiates a conversation.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-3.png)

#### <a name="askingforcount"></a><span data-ttu-id="890b3-159">AskingForCount</span><span class="sxs-lookup"><span data-stu-id="890b3-159">AskingForCount</span></span>

<span data-ttu-id="890b3-160">Ce dialogue est déclenché quand l’*utilisateur* demande le comptage de tous les **objets suivis**.</span><span class="sxs-lookup"><span data-stu-id="890b3-160">This dialog is triggered when the *user* asks for counting all **Tracked Objects**.</span></span>
<span data-ttu-id="890b3-161">Voici les expressions de déclenchement :</span><span class="sxs-lookup"><span data-stu-id="890b3-161">These are the trigger phrases:</span></span>

>* <span data-ttu-id="890b3-162">count me all</span><span class="sxs-lookup"><span data-stu-id="890b3-162">count me all</span></span>
>* <span data-ttu-id="890b3-163">how many are stored</span><span class="sxs-lookup"><span data-stu-id="890b3-163">how many are stored</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-4.png)

<span data-ttu-id="890b3-165">Grâce à [LUIS](https://docs.microsoft.com/composer/how-to-use-luis), l’*utilisateur* n’a pas besoin d’énoncer les expressions de cette manière exacte. La conversation est ainsi plus naturelle.</span><span class="sxs-lookup"><span data-stu-id="890b3-165">Thanks to [LUIS](https://docs.microsoft.com/composer/how-to-use-luis) the *user* does not have to ask the phrases in that exact way which allows a natural conversation for the *user*.</span></span>

<span data-ttu-id="890b3-166">Dans ce dialogue, le *bot* communiquera également avec la fonction Azure **Count** (nous y reviendrons).</span><span class="sxs-lookup"><span data-stu-id="890b3-166">In this dialog the *bot* will also talk to the **Count** Azure Function, more about that later.</span></span>

#### <a name="unknown-intent"></a><span data-ttu-id="890b3-167">Unknown Intent</span><span class="sxs-lookup"><span data-stu-id="890b3-167">Unknown Intent</span></span>

<span data-ttu-id="890b3-168">Ce dialogue est déclenché si l’entrée de l’*utilisateur* ne correspond à aucune autre condition de déclencheur. L’utilisateur est invité à reposer sa question.</span><span class="sxs-lookup"><span data-stu-id="890b3-168">This dialogue is triggered if the input from the *user* does not fit any other trigger condition and responses the user with trying his question again.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-5.png)

#### <a name="findentity"></a><span data-ttu-id="890b3-170">FindEntity</span><span class="sxs-lookup"><span data-stu-id="890b3-170">FindEntity</span></span>

<span data-ttu-id="890b3-171">Le dernier dialogue est plus complexe. Il implique une ramification et le stockage des données dans la *mémoire* du bot.</span><span class="sxs-lookup"><span data-stu-id="890b3-171">The last dialogue is more complex with branching and storing data in the *bots* memory.</span></span>
<span data-ttu-id="890b3-172">Il demande à l’utilisateur le *nom* de l’**objet suivi** au sujet duquel il souhaite en savoir plus, exécute une requête sur la fonction Azure **Find**, et utilise la réponse pour poursuivre la conversation.</span><span class="sxs-lookup"><span data-stu-id="890b3-172">It asks the user for the *name* of the **Tracked Object** it want's to know more information about, performs a query to the **Find** Azure Function, and uses the response to proceed with the conversation.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial5-section4-step1-6.png)

<span data-ttu-id="890b3-174">Si l’**objet suivi** est introuvable, l’utilisateur en est informé et la conversation se termine.</span><span class="sxs-lookup"><span data-stu-id="890b3-174">If the **Tracked Object** is not found, the user is informed and the conversation ends.</span></span> <span data-ttu-id="890b3-175">Quand l’**objet suivi** en question est trouvé, le bot vérifie et signale quelles propriétés sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="890b3-175">When the **Tracked Object** in question is found, the boot will check what properties are available and report on them.</span></span>

### <a name="adapting-the-bot"></a><span data-ttu-id="890b3-176">Adaptation du bot</span><span class="sxs-lookup"><span data-stu-id="890b3-176">Adapting the Bot</span></span>

<span data-ttu-id="890b3-177">Les déclencheurs **AskingForCount** et **FindEntity** doivent communiquer avec le back-end. Cela signifie que vous devez ajouter l’URL correcte de la **fonction Azure** déployée précédemment.</span><span class="sxs-lookup"><span data-stu-id="890b3-177">The **AskingForCount** and **FindEntity** trigger need to talk to the backend, this means you have to add the correct URL of the **Azure Function** you deployed previously.</span></span>

<span data-ttu-id="890b3-178">Dans le volet de dialogue, cliquez sur **AskingForCount** et recherchez l’action *Send an HTTP request* (Envoyer une requête HTTP). Ici, vous pouvez voir le champ **URL**, dans lequel vous devez indiquer l’URL correcte du point de terminaison de la fonction **Count**.</span><span class="sxs-lookup"><span data-stu-id="890b3-178">On the dialog panel click on **AskingForCount** and locate the *Send an HTTP request* action, here you can see the field **URL** which you need to change the correct URL for the **Count** function endpoint.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial5-section5-step1-1.png)

<span data-ttu-id="890b3-180">Pour finir, recherchez le déclencheur **FindEntity** et l’action *Send an HTTP request*. Dans le champ **URL**, indiquez l’URL du point de terminaison de la fonction **Find**.</span><span class="sxs-lookup"><span data-stu-id="890b3-180">Finally, look for the **FindEntity** trigger and locate the *Send an HTTP request* action, in the **URL** field change the URL to the **Find** function endpoint.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial5-section5-step1-2.png)

<span data-ttu-id="890b3-182">Vous êtes maintenant prêt à déployer le bot.</span><span class="sxs-lookup"><span data-stu-id="890b3-182">With everything set you are now ready to deploy the Bot.</span></span> <span data-ttu-id="890b3-183">Bot Framework Composer étant installé, vous pouvez publier le bot directement à partir de là.</span><span class="sxs-lookup"><span data-stu-id="890b3-183">Since you have Bot Framework composer installed, you can publish it directly from there.</span></span>

<span data-ttu-id="890b3-184">Apprenez-en davantage sur la [publication d’un bot à partir de Bot Composer](https://docs.microsoft.com/composer/how-to-publish-bot).</span><span class="sxs-lookup"><span data-stu-id="890b3-184">Learn more about [Publish a bot from Bot Composer](https://docs.microsoft.com/composer/how-to-publish-bot).</span></span>

> [!TIP]
> <span data-ttu-id="890b3-185">N’hésitez pas à vous amuser avec le bot en ajoutant des expressions de déclencheur ou de nouvelles réponses, ou en créant des branches de conversation.</span><span class="sxs-lookup"><span data-stu-id="890b3-185">Feel free playing around with Bot by adding more trigger phrases, new responses or conversation branching.</span></span>

## <a name="part-2---putting-everything-together-in-unity"></a><span data-ttu-id="890b3-186">Partie 2 : Assemblage final dans Unity</span><span class="sxs-lookup"><span data-stu-id="890b3-186">Part 2 - Putting everything together in Unity</span></span>

### <a name="preparing-the-scene"></a><span data-ttu-id="890b3-187">Préparation de la scène</span><span class="sxs-lookup"><span data-stu-id="890b3-187">Preparing the scene</span></span>

<span data-ttu-id="890b3-188">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.AzureCloudServices** > **Prefabs** > **Manager**.</span><span class="sxs-lookup"><span data-stu-id="890b3-188">In the Project window, navigate to **Assets** > **MRTK.Tutorials.AzureCloudServices** > **Prefabs** > **Manager** folder.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial5-section6-step1-1.png)

<span data-ttu-id="890b3-190">À partir de là, déplacez le préfabriqué **ChatBotManager** dans la hiérarchie de la scène.</span><span class="sxs-lookup"><span data-stu-id="890b3-190">From there move the prefab **ChatBotManager** into the scene Hierarchy.</span></span>

<span data-ttu-id="890b3-191">Une fois que vous avez ajouté le ChatBotManager à la scène, cliquez sur le composant **Chat Bot Manager**.</span><span class="sxs-lookup"><span data-stu-id="890b3-191">Once you add the ChatBotManager to the scene, click on the **Chat Bot Manager** component.</span></span>
<span data-ttu-id="890b3-192">Dans l’inspecteur, vous verrez qu’il existe un champ vide **Direct Line Secret Key** (Clé secrète directe) que vous devez renseigner.</span><span class="sxs-lookup"><span data-stu-id="890b3-192">In the Inspector you will see that there is an empty **Direct Line Secret Key** field which you need to fill out.</span></span>

> [!TIP]
> <span data-ttu-id="890b3-193">Vous pouvez récupérer la *clé secrète* à partir du portail Azure en recherchant la ressource de type **Inscription de chaînes de bot** que vous avez créée dans la première partie de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="890b3-193">You can retrieve the *secret key* from the Azure portal by looking for the resource of type **Bot Channels Registration** you have created in the first part of this tutorial.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial5-section6-step1-2.png)

<span data-ttu-id="890b3-195">À présent, vous allez connecter l’objet **ChatBotManager** avec le composant **ChatBotController** attaché à l’objet **ChatBotPanel**.</span><span class="sxs-lookup"><span data-stu-id="890b3-195">Now you will connect the **ChatBotManager** object with the **ChatBotController** component that is attached to the **ChatBotPanel** object.</span></span> <span data-ttu-id="890b3-196">Dans la hiérarchie, sélectionnez le **ChatBotPanel**. Vous verrez un champ vide **Chat Bot Manager**. Faites glisser l’objet **ChatBotManager** de la hiérarchie vers le champ vide **Chat Bot Manager**.</span><span class="sxs-lookup"><span data-stu-id="890b3-196">In the Hierarchy select the **ChatBotPanel** and you will see an empty **Chat Bot Manager** field, drag from the Hierarchy the **ChatBotManager** object into the empty **Chat Bot Manager** field.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial5-section6-step1-3.png)

<span data-ttu-id="890b3-198">Ensuite, vous avez besoin d’un moyen d’ouvrir le **ChatBotPanel** afin que l’utilisateur puisse interagir avec lui.</span><span class="sxs-lookup"><span data-stu-id="890b3-198">Next you need a way to open the **ChatBotPanel** so that the user can interact with it.</span></span> <span data-ttu-id="890b3-199">Dans la fenêtre de scène, vous avez peut-être remarqué la présence d’un bouton latéral *Chat Bot* sur l’objet **MainMenu**. Vous l’utiliserez pour résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="890b3-199">From the Scene window you may have noticed that there is a *Chat Bot* side button on the **MainMenu** object, you will use it to solve this problem.</span></span>

<span data-ttu-id="890b3-200">Dans la hiérarchie, recherchez **RootMenu** > **MainMenu** > **SideButtonCollection** > **ButtonChatBot**, puis recherchez le script *ButtonConfigHelper* dans l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="890b3-200">In the Hierarchy locate **RootMenu** > **MainMenu** > **SideButtonCollection** > **ButtonChatBot** and locate in the Inspector the *ButtonConfigHelper* script.</span></span> <span data-ttu-id="890b3-201">Vous verrez un emplacement vide sur le rappel d’événement **OnClick()** .</span><span class="sxs-lookup"><span data-stu-id="890b3-201">There you will see an empty slot on the **OnClick()** event callback.</span></span> <span data-ttu-id="890b3-202">Glissez-déposez le **ChatBotPanel** sur l’emplacement d’événement. Dans la liste déroulante, accédez à *GameObject*, sélectionnez *SetActive (bool)* dans le sous-menu et cochez la case.</span><span class="sxs-lookup"><span data-stu-id="890b3-202">Drag and drop the **ChatBotPanel** to the event slot, from the dropdown list navigate *GameObject*, then select in the sub menu *SetActive (bool)* and enable the checkbox.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial5-section6-step1-4.png)

<span data-ttu-id="890b3-204">Maintenant, le chatbot peut être démarré à partir du menu principal et la scène est prête à être utilisée.</span><span class="sxs-lookup"><span data-stu-id="890b3-204">Now the chat bot can be stared from the main menu and with that the scene is ready for use.</span></span>

### <a name="putting-the-bot-to-a-test"></a><span data-ttu-id="890b3-205">Tester le bot</span><span class="sxs-lookup"><span data-stu-id="890b3-205">Putting the bot to a test</span></span>

#### <a name="asking-about-the-quantity-of-tracked-objects"></a><span data-ttu-id="890b3-206">Demander la quantité d’objets suivis</span><span class="sxs-lookup"><span data-stu-id="890b3-206">Asking about the quantity of tracked objects</span></span>

<span data-ttu-id="890b3-207">Tout d’abord, nous allons demander au bot combien d’**objets suivis** sont stockés dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="890b3-207">First you test asking the bot how many **Tracked Objects** are stored in the database.</span></span>

> [!NOTE]
> <span data-ttu-id="890b3-208">Cette fois, vous devez exécuter l’application à partir d’HoloLens 2, car il se peut que des services comme *Synthèse vocale* ne soient pas disponibles sur votre système.</span><span class="sxs-lookup"><span data-stu-id="890b3-208">This time you must run the application from the HoloLens 2 because services like *text-to-speech* may not be available on your system.</span></span>

<span data-ttu-id="890b3-209">Exécutez l’application sur votre HoloLens 2, puis cliquez sur le bouton *Chat Bot* à côté du menu principal.</span><span class="sxs-lookup"><span data-stu-id="890b3-209">Run the application on your HoloLens 2 and click on the *Chat Bot* button next to the main menu.</span></span>
<span data-ttu-id="890b3-210">Après avoir été salué par le bot, posez-lui la question **how many objects do we have?** (combien d’objets avons-nous ?).</span><span class="sxs-lookup"><span data-stu-id="890b3-210">The bot will be greeting you, now ask **how many objects do we have?**</span></span>
<span data-ttu-id="890b3-211">Il doit vous indiquer la quantité et mettre fin à la conversation.</span><span class="sxs-lookup"><span data-stu-id="890b3-211">It should tell you the quantity and end the conversation.</span></span>

#### <a name="asking-about-a-tracked-object"></a><span data-ttu-id="890b3-212">Poser une question sur un objet suivi</span><span class="sxs-lookup"><span data-stu-id="890b3-212">Asking about a tracked object</span></span>

<span data-ttu-id="890b3-213">Réexécutez l’application, mais cette fois-ci demandez **find me a tracked object** (trouvez-moi un objet suivi). Le bot vous demandera le nom. Répondez « car » ou donnez le nom d’un autre *objet suivi* qui existe dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="890b3-213">Now run the application again and this time ask **find me a tracked object**, the bot will be asking you the name to which you should respond with the "car" or the name of an other *Tracked Object* you know exists in the database.</span></span> <span data-ttu-id="890b3-214">Le bot vous indiquera des détails tels que la description, et s’il a une ancre spatiale assignée.</span><span class="sxs-lookup"><span data-stu-id="890b3-214">The bot will tell you details like description and if it has a spatial anchor assigned.</span></span>

> [!TIP]
> <span data-ttu-id="890b3-215">Essayez de demander un **objet suivi** qui n’existe pas et découvrez comment le bot répond.</span><span class="sxs-lookup"><span data-stu-id="890b3-215">Try out asking for an **Tracked Objects** that does not exist and hear how the bot responds.</span></span>

## <a name="congratulations"></a><span data-ttu-id="890b3-216">Félicitations</span><span class="sxs-lookup"><span data-stu-id="890b3-216">Congratulations</span></span>

<span data-ttu-id="890b3-217">Dans ce tutoriel, vous avez découvert comment utiliser Azure Bot Framework pour interagir avec l’application dans une conversation en langage naturel.</span><span class="sxs-lookup"><span data-stu-id="890b3-217">In this tutorial you learned how Azure Bot Framework can be used to interact with the application via conversation with natural language.</span></span> <span data-ttu-id="890b3-218">Vous avez découvert comment développer votre propre bot et quels sont les différents éléments nécessaires à son fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="890b3-218">You learned how to develope your own bot and what all the moving pieces are to get it running,</span></span>

## <a name="conclusion"></a><span data-ttu-id="890b3-219">Conclusion</span><span class="sxs-lookup"><span data-stu-id="890b3-219">Conclusion</span></span>

<span data-ttu-id="890b3-220">Tout au long de cette série de tutoriels, vous avez vu comment enrichir votre application de fonctionnalités nouvelles et passionnantes grâce aux **services cloud Azure**.</span><span class="sxs-lookup"><span data-stu-id="890b3-220">Through the course of this tutorial series you experienced how **Azure Cloud services** brought new and exciting features to your application.</span></span>
<span data-ttu-id="890b3-221">Vous pouvez désormais stocker des données et des images dans le cloud avec **Stockage Azure**, utiliser **Azure Custom Vision** pour associer des images et entraîner un modèle, placer des objets dans un contexte local avec **Azure Spatial Anchors**, et implémenter **Azure Bot Framework avec LUIS** pour ajouter un chatbot et obtenir un nouveau modèle d’interaction naturelle.</span><span class="sxs-lookup"><span data-stu-id="890b3-221">You can now store data and images in the cloud with **Azure Storage**, use **Azure Custom Vision** to associate images and train a model, bring objects to a local context with **Azure Spatial Anchors**, and implement **Azure Bot Framework powered by LUIS** to add a conversational bot for a new and natural interaction pattern.</span></span>
