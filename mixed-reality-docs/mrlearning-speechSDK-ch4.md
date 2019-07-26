---
title: Module d’apprentissage de SpeechSDK-reconnaissance vocale et transcription
description: Suivez ce cours pour apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: b434b9c79a702067a9c3db6fb25b0f75cdc6030d
ms.sourcegitcommit: b086d7a62ee0c7913aa8f66c90e9d2527f270264
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68485779"
---
# <a name="4-setting-up-intent-and-natural-language-understanding"></a><span data-ttu-id="6d9a0-104">4. Configuration de l’intention et compréhension du langage naturel</span><span class="sxs-lookup"><span data-stu-id="6d9a0-104">4. Setting up intent and natural language understanding</span></span>

<span data-ttu-id="6d9a0-105">Dans cette leçon, nous allons explorer la fonctionnalité d’intention du service Azure Speech.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-105">In this lesson, we will explore the Azure Speech Service's Intent feature.</span></span> <span data-ttu-id="6d9a0-106">La fonctionnalité d’intention nous permet d’équiper notre application avec des commandes vocales en intelligence artificielle, où les utilisateurs peuvent indiquer des commandes vocales non spécifiques, tout en ayant l’intention de les interpréter par le système.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-106">The Intent feature allows us to equip our application with AI-powered voice commands, where users can say non-specific voice commands, and still have their intent understood by the system.</span></span> <span data-ttu-id="6d9a0-107">Au cours de cette leçon, nous allons configurer notre portail Azure LUIS, configurer nos intentions/entités/énoncés, publier notre ressource intentionnelle, connecter notre application Unity à notre ressource intentionnelle et effectuer notre premier appel d’API d’intention.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-107">During this lesson, we will set up our Azure LUIS Portal, setup our Intent/Entities/Utterances, publish our Intent Resource, connect our Unity app to our Intent Resource, and make our first Intent API call.</span></span>

## <a name="objectives"></a><span data-ttu-id="6d9a0-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="6d9a0-108">Objectives</span></span>

- <span data-ttu-id="6d9a0-109">Découvrez comment configurer l’intention et la compréhension du langage naturel dans notre application</span><span class="sxs-lookup"><span data-stu-id="6d9a0-109">Learn how to set up intent and natural language understanding in our application</span></span>
- <span data-ttu-id="6d9a0-110">Découvrez comment configurer le portail LUIS d’Azure</span><span class="sxs-lookup"><span data-stu-id="6d9a0-110">Learn how to set up Azure's LUIS Portal</span></span>
- <span data-ttu-id="6d9a0-111">Découvrez comment configurer l’intention, les entités et les énoncés sur Azure</span><span class="sxs-lookup"><span data-stu-id="6d9a0-111">Learn how to set up intent, entities, and utterances on Azure</span></span>

## <a name="instructions"></a><span data-ttu-id="6d9a0-112">Instructions</span><span class="sxs-lookup"><span data-stu-id="6d9a0-112">Instructions</span></span>
1. <span data-ttu-id="6d9a0-113">Autorisez votre ordinateur à activer la dictée. pour ce faire, accédez à paramètres Windows, sélectionnez «confidentialité», puis «parole» et enfin «entrée manuscrite & typage» et activez Speech services et suggestions de saisie.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-113">Allow your machine to enable Dictation, to do this, go to Windows Settings, select "privacy," then "speech," and finally "inking & typing" and turn on speech services and typing suggestions.</span></span>

![Module4Chapter4step1aim](images/module4chapter4step1aim.PNG)

![Module4Chapter4step1bim](images/module4chapter4step1bim.PNG)

![Module4Chapter4step1cim](images/module4chapter4step1cim.PNG)


2. <span data-ttu-id="6d9a0-117">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6d9a0-117">Log in to the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="6d9a0-118">Une fois que vous êtes connecté, cliquez sur créer une ressource, recherchez «Language Understanding», puis cliquez sur entrée.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-118">Once you are logged in, click on Create a resource, and search for "Language Understanding," and click enter.</span></span>

![Module4Chapter4step2im](images/module4chapter4step2im.PNG)

3. <span data-ttu-id="6d9a0-120">Sélectionnez le bouton créer pour créer une instance de ce service.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-120">Select the Create button, to create an instance of this service.</span></span> <span data-ttu-id="6d9a0-121">Nommez votre projet «Speech_SDK_Learning_Module» et sélectionnez «payer à l’accès».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-121">Name your project “Speech_SDK_Learning_Module” and select “Pay As You Go.”</span></span>

![Module4Chapter4step3aim](images/module4chapter4step3aim.png)

![Module4Chapter4step3bim](images/module4chapter4step3bim.PNG)

4. <span data-ttu-id="6d9a0-124">Sélectionnez votre région.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-124">Select your Region.</span></span>  <span data-ttu-id="6d9a0-125">Dans le cadre de ce didacticiel, sélectionnez «(US) Ouest des États-Unis».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-125">For the purpose of this tutorial, select "(US) West US."</span></span> <span data-ttu-id="6d9a0-126">Choisissez ensuite «F0» comme niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-126">Then choose "F0" for the pricing tier.</span></span> <span data-ttu-id="6d9a0-127">Cliquez maintenant sur «créer» (situé dans le coin inférieur gauche) pour créer la ressource.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-127">Now click "create" (located in the bottom left corner) to create the resource.</span></span>

>  <span data-ttu-id="6d9a0-128">Remarque: une fois que vous avez cliqué sur «créer», vous devez attendre que le service soit créé. cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-128">Note: once you have clicked on "create," you will have to wait for the service to be created, this might take a minute.</span></span>

5. <span data-ttu-id="6d9a0-129">Une notification s’affiche dans le portail une fois la ressource créée.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-129">A notification will appear in the portal once the Resource is created.</span></span> <span data-ttu-id="6d9a0-130">Cliquez sur cette notification et sélectionnez «atteindre la ressource».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-130">Click on this notification and select "Go to resource."</span></span>

6. <span data-ttu-id="6d9a0-131">À partir de la page «Démarrage rapide» de votre service «API LUIS», accédez à la première étape, saisissez vos «clés», puis cliquez sur «clés» (vous pouvez également effectuer cette opération en cliquant sur le lien hypertexte bleu «clés», comme illustré dans l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="6d9a0-131">From the "Quick Start" page of your "LUIS API" service, navigate to the first step, grab your "keys," and click "keys" (you can also achieve this by clicking the blue hyperlink "keys," shown in the image below).</span></span> <span data-ttu-id="6d9a0-132">Cela permet de révéler votre service, «Keys».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-132">This will reveal your service, "Keys."</span></span> <span data-ttu-id="6d9a0-133">Enregistrez une copie de l’une des clés afin de pouvoir l’utiliser ultérieurement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-133">Save a copy of one of the keys so you can use it later in the app.</span></span>

![Module4Chapter4step6im](images/module4chapter4step6im.PNG)

7. <span data-ttu-id="6d9a0-135">De retour dans la page «Démarrage rapide», sous la section 2B, cliquez sur «portail Language Understanding» (illustré dans l’image ci-dessus) pour être redirigé vers la page Web que vous utiliserez pour créer votre nouveau service, au sein de l’application LUIS.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-135">Back in the "Quick Start" page under Section 2b, click on "Language Understanding Portal" (shown in the image above) to be redirected to the webpage which you will use to create your new service, within the LUIS application.</span></span>

> <span data-ttu-id="6d9a0-136">Remarque : Quand vous atteignez le «portail Language Understanding», vous devrez peut-être vous connecter, si ce n’est déjà fait, avec les mêmes informations d’identification que votre Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-136">Note: Upon reaching the "Language Understanding Portal," you may need to login, if you are not already, with the same credentials as your Azure portal.</span></span> <span data-ttu-id="6d9a0-137">Si vous utilisez LUIS pour la première fois, vous devez faire défiler vers le bas de la page d’accueil, pour rechercher et cliquer sur le bouton «créer une application LUIS».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-137">If this is your first time using LUIS, you will need to scroll down to the bottom of the welcome page, to find and click on the "Create LUIS" app button.</span></span>

8. <span data-ttu-id="6d9a0-138">Une fois connecté, cliquez sur mes applications (si vous n’êtes pas actuellement dans cette section).</span><span class="sxs-lookup"><span data-stu-id="6d9a0-138">Once logged in, click My Apps (if you are not in that section currently).</span></span> <span data-ttu-id="6d9a0-139">Vous pouvez ensuite cliquer sur créer une nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-139">You can then click on Create new app.</span></span> <span data-ttu-id="6d9a0-140">Nommez la nouvelle application «Speech SDK Learning module».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-140">Name the new app “Speech SDK Learning Module.”</span></span> <span data-ttu-id="6d9a0-141">Ajoutez également «module d’apprentissage du kit de développement logiciel (SDK) Speech» au champ Description.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-141">Add “Speech SDK Learning Module" to the description field, as well.</span></span> <span data-ttu-id="6d9a0-142">Cliquez ensuite sur «terminé».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-142">Then click "done."</span></span>

![Module4Chapter4step8aim](images/module4chapter4step8aim.PNG)

![Module4Chapter4step8bim](images/module4chapter4step8bim.PNG)

> <span data-ttu-id="6d9a0-145">observe Si votre application est censée comprendre une langue différente de l’anglais, vous devez remplacer la «culture» par la langue appropriée.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-145">note: If your app is supposed to understand a language different from English, you should change the "Culture" to the appropriate language.</span></span>

9. <span data-ttu-id="6d9a0-146">Cliquez sur «Build» situé en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-146">Click “Build” located in the top right.</span></span>

10. <span data-ttu-id="6d9a0-147">Sous ressources de l’application sur la gauche, sélectionnez «intentions», puis cliquez sur «créer un nouvel objectif» et nommez-la «PressButton».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-147">Under App Assets on the left, select “Intents” then click “Create New Intent” and name it “PressButton.”</span></span> 

![Module4Chapter4step10im](images/module4chapter4step10im.PNG)

> <span data-ttu-id="6d9a0-149">Remarque : Il est important d’utiliser les noms des intentions et des entités utilisées dans ce didacticiel, car l’application Lunarcom y fait référence par nom.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-149">Note: It is important to use the names of Intents and Entities used in this tutorial because the Lunarcom app will be referencing them by name.</span></span> 
>
> <span data-ttu-id="6d9a0-150">Remarque: vous devez maintenant avoir 2 intentions-«PressButton» et «None».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-150">Note: you should now have 2 Intents - “PressButton” and “None."</span></span>

11. <span data-ttu-id="6d9a0-151">Sous ressources de l’application sur la gauche, sélectionnez «entités», puis cliquez sur «créer une entité» et nommez-la «action» et conservez le type d’entité «simple».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-151">Under App Assets on the left, select “Entities” and click “Create New Entity” and name it “Action” and keep the Entity Type as “Simple.”</span></span>

![Module4Chapter4step11im](images/module4chapter4step11im.PNG)

12. <span data-ttu-id="6d9a0-153">Cliquez de nouveau sur «créer une nouvelle entité» et nommez-la «cible» et conservez le type d’entité «simple».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-153">Click “Create New Entity” again and name it “Target” and keep the Entity Type as “Simple” as well.</span></span>

![Module4Chapter4step12im](images/module4chapter4step12im.PNG)

13. <span data-ttu-id="6d9a0-155">Sous ressources de l’application sur la gauche, sélectionnez «intentions», puis cliquez sur l’intention «PressButton» que vous avez créée à l’étape 10.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-155">Under App Assets on the left, select "Intents" then click on your "PressButton" Intent that you created in step 10.</span></span>

![Module4Chapter4step13im](images/module4chapter4step13im.PNG)

14. <span data-ttu-id="6d9a0-157">Cliquez sur la liste déroulante «Afficher les options» à droite, puis sélectionnez «Afficher les valeurs d’entité».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-157">Click on the "View options" dropdown on the right and select "show entity values."</span></span> 

![Module4Chapter4step14aim](images/module4chapter4step14aim.PNG)<span data-ttu-id="6d9a0-159">Cliquez sur «Entrez un exemple...»</span><span class="sxs-lookup"><span data-stu-id="6d9a0-159">Click on the “Enter an example…”</span></span> <span data-ttu-id="6d9a0-160">entr.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-160">textbox.</span></span> <span data-ttu-id="6d9a0-161">Ensuite, entrez les énoncés suivants:</span><span class="sxs-lookup"><span data-stu-id="6d9a0-161">Then, enter the following utterances:</span></span> 

![Module4Chapter4step14bim](images/module4chapter4step14bim.PNG)

15. <span data-ttu-id="6d9a0-163">Cliquez sur la liste déroulante «Afficher les options» à droite, puis sélectionnez «Afficher les noms d’entité».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-163">Click on the "View options" dropdown on the right and select "Show entity names."</span></span>

![Module4Chapter4step15im](images/module4chapter4step15im.PNG)

16. <span data-ttu-id="6d9a0-165">Assurez-vous que chacun des 10 énoncés a les étiquettes d’entité suivantes dans les emplacements suivants, de 1.) en cliquant sur les mots dont l’étiquette est incorrecte et, dans le menu contextuel, sélectionnez «Supprimer l’étiquette» et 2.) en cliquant sur les mots qui doivent être étiquetés et, dans le menu contextuel, sélectionnez l’étiquette appropriée.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-165">Ensure that each of the 10 Utterances have the following Entity labels in the following places by 1.) clicking on words that are mislabeled and, in the popup, selecting "remove label" and 2.) clicking on words that should be labeled and, in the popup, selecting the appropriate label.</span></span>

![Module4Chapter4step16im](images/module4chapter4step16im.PNG)

17. <span data-ttu-id="6d9a0-167">À présent, pour publier le modèle, cliquez sur «train» dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-167">Now, to publish the model, click "Train" in the top right.</span></span> <span data-ttu-id="6d9a0-168">Ensuite, une fois le traitement terminé, cliquez sur «test» dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-168">Then, once it has finished processing, click "Test" in the top right.</span></span>

![Module4Chapter4step17im](images/module4chapter4step17im.PNG)

18. <span data-ttu-id="6d9a0-170">Entrez dans la zone de texte «sélectionner le bouton lancer».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-170">Enter in “select the launch button” in  the textbox.</span></span>

> <span data-ttu-id="6d9a0-171">Remarque: nous n’avons pas ajouté «Select» comme action dans l’un de nos énoncés, mais si vous cliquez sur «Inspect», le modèle a reconnu «Select» comme une entité d’action.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-171">note: we did not add “select” as an action in any of our Utterances - but if you click on “Inspect,” the model recognized “select” as an action entity.</span></span>
>
> ![Module4Chapter4noteim](images/module4chapter4noteim.PNG)

19. <span data-ttu-id="6d9a0-173">À présent, cliquez sur «publier» dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-173">Now, click "publish" in the top right.</span></span> <span data-ttu-id="6d9a0-174">Assurez-vous que la liste déroulante indique «production», puis cliquez sur «publier» dans la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-174">Ensure the dropdown says “Production” and click "publish" on the popup as well.</span></span> 

![Module4Chapter4step19im](images/module4chapter4step19im.PNG)

20. <span data-ttu-id="6d9a0-176">Une fois publiée, une barre verte doit apparaître en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-176">Once published, a green bar should appear at the top of the page.</span></span>  <span data-ttu-id="6d9a0-177">Cliquez sur la barre verte pour atteindre la page «gérer».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-177">Click on the green bar to be taken to the "Manage" page.</span></span> 

![Module4Chapter4step20im](images/module4chapter4step20im.PNG)

21. <span data-ttu-id="6d9a0-179">Cliquez sur «clés et points de terminaison» sous «paramètres d’application» à gauche.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-179">Click on "Keys and Endpoints" under “Application Settings” to the left.</span></span> <span data-ttu-id="6d9a0-180">Ensuite, définissez la liste déroulante «publier sur» sur «production».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-180">Then, set the drop down "Publish To" as "Production."</span></span> <span data-ttu-id="6d9a0-181">Définissez le fuseau horaire en fonction de vos propres et cochez la case pour inclure tous les scores d’intention prédits.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-181">Set the time-zone to match yours, and check the box to include all predicted intent scores.</span></span> <span data-ttu-id="6d9a0-182">Enfin, cliquez sur «affecter une ressource».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-182">Lastly, Click on "Assign resource."</span></span>

![Module4Chapter4step21im](images/module4chapter4step21im.PNG)

22. <span data-ttu-id="6d9a0-184">Sélectionnez locataire dans la première liste déroulante, puis sélectionnez paiement à l’accès dans la liste déroulante nom de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-184">Select tenant from the first dropdown, and select “Pay-as-you-go” in the Subscription Name dropdown.</span></span> <span data-ttu-id="6d9a0-185">Sous LUIS nom de la ressource, choisissez la ressource que nous avons créée ci-dessus dans les étapes 1-5.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-185">Under LUIS resource name, choose the resource that we created above in steps 1-5.</span></span> <span data-ttu-id="6d9a0-186">Cliquez ensuite sur «affecter la ressource».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-186">Then, click on "Assign resource."</span></span> 

![Module4Chapter4step22im](images/module4chapter4step22im.PNG)

> <span data-ttu-id="6d9a0-188">Remarque : Veillez à copier et à enregistrer l’URL de point de terminaison associée à la ressource que nous venons d’attribuer afin qu’elle soit facilement accessible pour la section suivante.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-188">Note: Ensure to copy and save the Endpoint URL associated with the resource we just assigned so that it is easily accessible for the next section.</span></span>
>
> <span data-ttu-id="6d9a0-189">Remarque : Pour le nom du locataire, mettez votre entreprise ou votre profil créé pour cette application.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-189">Note: For the Tenant name, put your corporation or profile that you created for this application.</span></span>

23. <span data-ttu-id="6d9a0-190">À présent, ouvrez la nouvelle application dans Unity et sélectionnez l’objet Lunarcom_Base dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-190">Now, open the new app in Unity and select the Lunarcom_Base object in the hierarchy.</span></span> <span data-ttu-id="6d9a0-191">Cliquez sur «Ajouter un composant» dans le panneau inspecteur et recherchez et sélectionnez «LunarcomIntentRecognizer».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-191">Click “Add Component” in the inspector panel and search for and select “LunarcomIntentRecognizer.”</span></span>

![Module4Chapter4step23im](images/module4chapter4step23im.PNG)

24. <span data-ttu-id="6d9a0-193">Dans le champ de point de terminaison Luis de la «LunarcomIntentRecognizer» dans le panneau Inspecteur, entrez l’URL de point de terminaison que vous avez enregistrée à l’étape 22.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-193">In the Luis Endpoint field of the "LunarcomIntentRecognizer" in the inspector panel, enter the Endpoint URL that you saved in step 22.</span></span> 

![Module4Chapter4step24im](images/module4chapter4step24im.PNG)

>  <span data-ttu-id="6d9a0-195">Remarque : Dans le composant «LunarcomOfflineRecognizer» du volet de l’inspecteur, assurez-vous que l’option «désactiver» est sélectionnée pour «SimulateOfflineMode». dans le cas contraire, le test du programme ne fonctionnera pas.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-195">Note: In the "LunarcomOfflineRecognizer" component in the inspector panel, make sure that “disable” is selected for "SimulateOfflineMode" otherwise, testing the program will not work.</span></span> 

25. <span data-ttu-id="6d9a0-196">Appuyez sur le bouton lecture dans l’éditeur Unity et cliquez sur le bouton Rocket pour démarrer la reconnaissance intentionnelle.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-196">Press the Play button in the Unity Editor and click the rocket button to start intent recognition.</span></span> <span data-ttu-id="6d9a0-197">À l’expression «sélectionnez le bouton lancer Rocket».</span><span class="sxs-lookup"><span data-stu-id="6d9a0-197">Utter the phrase “select the launch rocket button.”</span></span>

>  <span data-ttu-id="6d9a0-198">Remarque : L’application a reconnu la fonction souhaitée et activé le bouton Rocket.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-198">Note: The app recognized the desired function and activated the rocket button.</span></span>
>
> ![Module4Chapter4step24im](images/module4chapter4note2im.PNG)

## <a name="congratulations"></a><span data-ttu-id="6d9a0-200">Félicitations</span><span class="sxs-lookup"><span data-stu-id="6d9a0-200">Congratulations</span></span>

<span data-ttu-id="6d9a0-201">Dans cette leçon, nous avons appris à ajouter des commandes vocales dotées de l’intelligence artificielle.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-201">In this lesson, we learned how to add AI-powered speech commands!</span></span> <span data-ttu-id="6d9a0-202">À présent, votre programme peut reconnaître l’intention des utilisateurs même s’ils ne dictent pas de commandes vocales précises.</span><span class="sxs-lookup"><span data-stu-id="6d9a0-202">Now your program can recognize users' intent even if they do not utter precise voice commands.</span></span>

