---
title: Didacticiels Azure Speech services-4. Configuration de l’intention et compréhension du langage naturel
description: Suivez ce cours pour apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 5ca2df56eee3ae41d97de4e8b1e88a39d4d36718
ms.sourcegitcommit: af1602710c1ccb7ed870a491923350d387706129
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68701947"
---
# <a name="4-setting-up-intent-and-natural-language-understanding"></a><span data-ttu-id="757cd-105">4. Configuration de l’intention et compréhension du langage naturel</span><span class="sxs-lookup"><span data-stu-id="757cd-105">4. Setting up intent and natural language understanding</span></span>

<span data-ttu-id="757cd-106">Dans cette leçon, nous allons explorer la fonctionnalité d’intention du service Azure Speech.</span><span class="sxs-lookup"><span data-stu-id="757cd-106">In this lesson, we will explore the Azure Speech Service's Intent feature.</span></span> <span data-ttu-id="757cd-107">La fonctionnalité d’intention nous permet d’équiper notre application avec des commandes vocales en intelligence artificielle, où les utilisateurs peuvent indiquer des commandes vocales non spécifiques, tout en ayant l’intention de les interpréter par le système.</span><span class="sxs-lookup"><span data-stu-id="757cd-107">The Intent feature allows us to equip our application with AI-powered voice commands, where users can say non-specific voice commands, and still have their intent understood by the system.</span></span> <span data-ttu-id="757cd-108">Au cours de cette leçon, nous allons configurer notre portail Azure LUIS, configurer nos intentions/entités/énoncés, publier notre ressource intentionnelle, connecter notre application Unity à notre ressource intentionnelle et effectuer notre premier appel d’API d’intention.</span><span class="sxs-lookup"><span data-stu-id="757cd-108">During this lesson, we will set up our Azure LUIS Portal, setup our Intent/Entities/Utterances, publish our Intent Resource, connect our Unity app to our Intent Resource, and make our first Intent API call.</span></span>

## <a name="objectives"></a><span data-ttu-id="757cd-109">Objectifs</span><span class="sxs-lookup"><span data-stu-id="757cd-109">Objectives</span></span>

- <span data-ttu-id="757cd-110">Découvrez comment configurer l’intention et la compréhension du langage naturel dans notre application</span><span class="sxs-lookup"><span data-stu-id="757cd-110">Learn how to set up intent and natural language understanding in our application</span></span>
- <span data-ttu-id="757cd-111">Découvrez comment configurer le portail LUIS d’Azure</span><span class="sxs-lookup"><span data-stu-id="757cd-111">Learn how to set up Azure's LUIS Portal</span></span>
- <span data-ttu-id="757cd-112">Découvrez comment configurer l’intention, les entités et les énoncés sur Azure</span><span class="sxs-lookup"><span data-stu-id="757cd-112">Learn how to set up intent, entities, and utterances on Azure</span></span>

## <a name="instructions"></a><span data-ttu-id="757cd-113">Instructions</span><span class="sxs-lookup"><span data-stu-id="757cd-113">Instructions</span></span>
1. <span data-ttu-id="757cd-114">Autorisez votre ordinateur à activer la dictée. pour ce faire, accédez à paramètres Windows, sélectionnez «confidentialité», puis «parole» et enfin «entrée manuscrite & typage» et activez Speech services et suggestions de saisie.</span><span class="sxs-lookup"><span data-stu-id="757cd-114">Allow your machine to enable Dictation, to do this, go to Windows Settings, select "privacy," then "speech," and finally "inking & typing" and turn on speech services and typing suggestions.</span></span>

![Module4Chapter4step1aim](images/module4chapter4step1aim.PNG)

![Module4Chapter4step1bim](images/module4chapter4step1bim.PNG)

![Module4Chapter4step1cim](images/module4chapter4step1cim.PNG)


2. <span data-ttu-id="757cd-118">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="757cd-118">Log in to the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="757cd-119">Une fois que vous êtes connecté, cliquez sur créer une ressource, recherchez «Language Understanding», puis cliquez sur entrée.</span><span class="sxs-lookup"><span data-stu-id="757cd-119">Once you are logged in, click on Create a resource, and search for "Language Understanding," and click enter.</span></span>

![Module4Chapter4step2im](images/module4chapter4step2im.PNG)

3. <span data-ttu-id="757cd-121">Sélectionnez le bouton créer pour créer une instance de ce service.</span><span class="sxs-lookup"><span data-stu-id="757cd-121">Select the Create button, to create an instance of this service.</span></span> <span data-ttu-id="757cd-122">Nommez votre projet «Speech_SDK_Learning_Module» et sélectionnez «payer à l’accès».</span><span class="sxs-lookup"><span data-stu-id="757cd-122">Name your project “Speech_SDK_Learning_Module” and select “Pay As You Go.”</span></span>

![Module4Chapter4step3aim](images/module4chapter4step3aim.png)

![Module4Chapter4step3bim](images/module4chapter4step3bim.PNG)

4. <span data-ttu-id="757cd-125">Sélectionnez votre région.</span><span class="sxs-lookup"><span data-stu-id="757cd-125">Select your Region.</span></span>  <span data-ttu-id="757cd-126">Dans le cadre de ce didacticiel, sélectionnez «(US) Ouest des États-Unis».</span><span class="sxs-lookup"><span data-stu-id="757cd-126">For the purpose of this tutorial, select "(US) West US."</span></span> <span data-ttu-id="757cd-127">Choisissez ensuite «F0» comme niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="757cd-127">Then choose "F0" for the pricing tier.</span></span> <span data-ttu-id="757cd-128">Cliquez maintenant sur «créer» (situé dans le coin inférieur gauche) pour créer la ressource.</span><span class="sxs-lookup"><span data-stu-id="757cd-128">Now click "create" (located in the bottom left corner) to create the resource.</span></span>

>  <span data-ttu-id="757cd-129">Remarque: une fois que vous avez cliqué sur «créer», vous devez attendre que le service soit créé. cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="757cd-129">Note: once you have clicked on "create," you will have to wait for the service to be created, this might take a minute.</span></span>

5. <span data-ttu-id="757cd-130">Une notification s’affiche dans le portail une fois la ressource créée.</span><span class="sxs-lookup"><span data-stu-id="757cd-130">A notification will appear in the portal once the Resource is created.</span></span> <span data-ttu-id="757cd-131">Cliquez sur cette notification et sélectionnez «atteindre la ressource».</span><span class="sxs-lookup"><span data-stu-id="757cd-131">Click on this notification and select "Go to resource."</span></span>

6. <span data-ttu-id="757cd-132">À partir de la page «Démarrage rapide» de votre service «API LUIS», accédez à la première étape, saisissez vos «clés», puis cliquez sur «clés» (vous pouvez également effectuer cette opération en cliquant sur le lien hypertexte bleu «clés», comme illustré dans l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="757cd-132">From the "Quick Start" page of your "LUIS API" service, navigate to the first step, grab your "keys," and click "keys" (you can also achieve this by clicking the blue hyperlink "keys," shown in the image below).</span></span> <span data-ttu-id="757cd-133">Cela permet de révéler votre service, «Keys».</span><span class="sxs-lookup"><span data-stu-id="757cd-133">This will reveal your service, "Keys."</span></span> <span data-ttu-id="757cd-134">Enregistrez une copie de l’une des clés afin de pouvoir l’utiliser ultérieurement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="757cd-134">Save a copy of one of the keys so you can use it later in the app.</span></span>

![Module4Chapter4step6im](images/module4chapter4step6im.PNG)

7. <span data-ttu-id="757cd-136">De retour dans la page «Démarrage rapide», sous la section 2B, cliquez sur «portail Language Understanding» (illustré dans l’image ci-dessus) pour être redirigé vers la page Web que vous utiliserez pour créer votre nouveau service, au sein de l’application LUIS.</span><span class="sxs-lookup"><span data-stu-id="757cd-136">Back in the "Quick Start" page under Section 2b, click on "Language Understanding Portal" (shown in the image above) to be redirected to the webpage which you will use to create your new service, within the LUIS application.</span></span>

> <span data-ttu-id="757cd-137">Remarque : Quand vous atteignez le «portail Language Understanding», vous devrez peut-être vous connecter, si ce n’est déjà fait, avec les mêmes informations d’identification que votre Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="757cd-137">Note: Upon reaching the "Language Understanding Portal," you may need to login, if you are not already, with the same credentials as your Azure portal.</span></span> <span data-ttu-id="757cd-138">Si vous utilisez LUIS pour la première fois, vous devez faire défiler vers le bas de la page d’accueil, pour rechercher et cliquer sur le bouton «créer une application LUIS».</span><span class="sxs-lookup"><span data-stu-id="757cd-138">If this is your first time using LUIS, you will need to scroll down to the bottom of the welcome page, to find and click on the "Create LUIS" app button.</span></span>

8. <span data-ttu-id="757cd-139">Une fois connecté, cliquez sur mes applications (si vous n’êtes pas actuellement dans cette section).</span><span class="sxs-lookup"><span data-stu-id="757cd-139">Once logged in, click My Apps (if you are not in that section currently).</span></span> <span data-ttu-id="757cd-140">Vous pouvez ensuite cliquer sur créer une nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="757cd-140">You can then click on Create new app.</span></span> <span data-ttu-id="757cd-141">Nommez la nouvelle application «Speech SDK Learning module».</span><span class="sxs-lookup"><span data-stu-id="757cd-141">Name the new app “Speech SDK Learning Module.”</span></span> <span data-ttu-id="757cd-142">Ajoutez également «module d’apprentissage du kit de développement logiciel (SDK) Speech» au champ Description.</span><span class="sxs-lookup"><span data-stu-id="757cd-142">Add “Speech SDK Learning Module" to the description field, as well.</span></span> <span data-ttu-id="757cd-143">Cliquez ensuite sur «terminé».</span><span class="sxs-lookup"><span data-stu-id="757cd-143">Then click "done."</span></span>

![Module4Chapter4step8aim](images/module4chapter4step8aim.PNG)

![Module4Chapter4step8bim](images/module4chapter4step8bim.PNG)

> <span data-ttu-id="757cd-146">observe Si votre application est censée comprendre une langue différente de l’anglais, vous devez remplacer la «culture» par la langue appropriée.</span><span class="sxs-lookup"><span data-stu-id="757cd-146">note: If your app is supposed to understand a language different from English, you should change the "Culture" to the appropriate language.</span></span>

9. <span data-ttu-id="757cd-147">Cliquez sur «Build» situé en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="757cd-147">Click “Build” located in the top right.</span></span>

10. <span data-ttu-id="757cd-148">Sous ressources de l’application sur la gauche, sélectionnez «intentions», puis cliquez sur «créer un nouvel objectif» et nommez-la «PressButton».</span><span class="sxs-lookup"><span data-stu-id="757cd-148">Under App Assets on the left, select “Intents” then click “Create New Intent” and name it “PressButton.”</span></span> 

![Module4Chapter4step10im](images/module4chapter4step10im.PNG)

> <span data-ttu-id="757cd-150">Remarque : Il est important d’utiliser les noms des intentions et des entités utilisées dans ce didacticiel, car l’application Lunarcom y fait référence par nom.</span><span class="sxs-lookup"><span data-stu-id="757cd-150">Note: It is important to use the names of Intents and Entities used in this tutorial because the Lunarcom app will be referencing them by name.</span></span> 
>
> <span data-ttu-id="757cd-151">Remarque: vous devez maintenant avoir 2 intentions-«PressButton» et «None».</span><span class="sxs-lookup"><span data-stu-id="757cd-151">Note: you should now have 2 Intents - “PressButton” and “None."</span></span>

11. <span data-ttu-id="757cd-152">Sous ressources de l’application sur la gauche, sélectionnez «entités», puis cliquez sur «créer une entité» et nommez-la «action» et conservez le type d’entité «simple».</span><span class="sxs-lookup"><span data-stu-id="757cd-152">Under App Assets on the left, select “Entities” and click “Create New Entity” and name it “Action” and keep the Entity Type as “Simple.”</span></span>

![Module4Chapter4step11im](images/module4chapter4step11im.PNG)

12. <span data-ttu-id="757cd-154">Cliquez de nouveau sur «créer une nouvelle entité» et nommez-la «cible» et conservez le type d’entité «simple».</span><span class="sxs-lookup"><span data-stu-id="757cd-154">Click “Create New Entity” again and name it “Target” and keep the Entity Type as “Simple” as well.</span></span>

![Module4Chapter4step12im](images/module4chapter4step12im.PNG)

13. <span data-ttu-id="757cd-156">Sous ressources de l’application sur la gauche, sélectionnez «intentions», puis cliquez sur l’intention «PressButton» que vous avez créée à l’étape 10.</span><span class="sxs-lookup"><span data-stu-id="757cd-156">Under App Assets on the left, select "Intents" then click on your "PressButton" Intent that you created in step 10.</span></span>

![Module4Chapter4step13im](images/module4chapter4step13im.PNG)

14. <span data-ttu-id="757cd-158">Cliquez sur la liste déroulante «Afficher les options» à droite, puis sélectionnez «Afficher les valeurs d’entité».</span><span class="sxs-lookup"><span data-stu-id="757cd-158">Click on the "View options" dropdown on the right and select "show entity values."</span></span> 

![Module4Chapter4step14aim](images/module4chapter4step14aim.PNG)<span data-ttu-id="757cd-160">Cliquez sur «Entrez un exemple...»</span><span class="sxs-lookup"><span data-stu-id="757cd-160">Click on the “Enter an example…”</span></span> <span data-ttu-id="757cd-161">entr.</span><span class="sxs-lookup"><span data-stu-id="757cd-161">textbox.</span></span> <span data-ttu-id="757cd-162">Ensuite, entrez les énoncés suivants:</span><span class="sxs-lookup"><span data-stu-id="757cd-162">Then, enter the following utterances:</span></span> 

![Module4Chapter4step14bim](images/module4chapter4step14bim.PNG)

15. <span data-ttu-id="757cd-164">Cliquez sur la liste déroulante «Afficher les options» à droite, puis sélectionnez «Afficher les noms d’entité».</span><span class="sxs-lookup"><span data-stu-id="757cd-164">Click on the "View options" dropdown on the right and select "Show entity names."</span></span>

![Module4Chapter4step15im](images/module4chapter4step15im.PNG)

16. <span data-ttu-id="757cd-166">Assurez-vous que chacun des 10 énoncés a les étiquettes d’entité suivantes dans les emplacements suivants, de 1.) en cliquant sur les mots dont l’étiquette est incorrecte et, dans le menu contextuel, sélectionnez «Supprimer l’étiquette» et 2.) en cliquant sur les mots qui doivent être étiquetés et, dans le menu contextuel, sélectionnez l’étiquette appropriée.</span><span class="sxs-lookup"><span data-stu-id="757cd-166">Ensure that each of the 10 Utterances have the following Entity labels in the following places by 1.) clicking on words that are mislabeled and, in the popup, selecting "remove label" and 2.) clicking on words that should be labeled and, in the popup, selecting the appropriate label.</span></span>

![Module4Chapter4step16im](images/module4chapter4step16im.PNG)

17. <span data-ttu-id="757cd-168">À présent, pour publier le modèle, cliquez sur «train» dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="757cd-168">Now, to publish the model, click "Train" in the top right.</span></span> <span data-ttu-id="757cd-169">Ensuite, une fois le traitement terminé, cliquez sur «test» dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="757cd-169">Then, once it has finished processing, click "Test" in the top right.</span></span>

![Module4Chapter4step17im](images/module4chapter4step17im.PNG)

18. <span data-ttu-id="757cd-171">Entrez dans la zone de texte «sélectionner le bouton lancer».</span><span class="sxs-lookup"><span data-stu-id="757cd-171">Enter in “select the launch button” in  the textbox.</span></span>

> <span data-ttu-id="757cd-172">Remarque: nous n’avons pas ajouté «Select» comme action dans l’un de nos énoncés, mais si vous cliquez sur «Inspect», le modèle a reconnu «Select» comme une entité d’action.</span><span class="sxs-lookup"><span data-stu-id="757cd-172">note: we did not add “select” as an action in any of our Utterances - but if you click on “Inspect,” the model recognized “select” as an action entity.</span></span>
>
> ![Module4Chapter4noteim](images/module4chapter4noteim.PNG)

19. <span data-ttu-id="757cd-174">À présent, cliquez sur «publier» dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="757cd-174">Now, click "publish" in the top right.</span></span> <span data-ttu-id="757cd-175">Assurez-vous que la liste déroulante indique «production», puis cliquez sur «publier» dans la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="757cd-175">Ensure the dropdown says “Production” and click "publish" on the popup as well.</span></span> 

![Module4Chapter4step19im](images/module4chapter4step19im.PNG)

20. <span data-ttu-id="757cd-177">Une fois publiée, une barre verte doit apparaître en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="757cd-177">Once published, a green bar should appear at the top of the page.</span></span>  <span data-ttu-id="757cd-178">Cliquez sur la barre verte pour atteindre la page «gérer».</span><span class="sxs-lookup"><span data-stu-id="757cd-178">Click on the green bar to be taken to the "Manage" page.</span></span> 

![Module4Chapter4step20im](images/module4chapter4step20im.PNG)

21. <span data-ttu-id="757cd-180">Cliquez sur «clés et points de terminaison» sous «paramètres d’application» à gauche.</span><span class="sxs-lookup"><span data-stu-id="757cd-180">Click on "Keys and Endpoints" under “Application Settings” to the left.</span></span> <span data-ttu-id="757cd-181">Ensuite, définissez la liste déroulante «publier sur» sur «production».</span><span class="sxs-lookup"><span data-stu-id="757cd-181">Then, set the drop down "Publish To" as "Production."</span></span> <span data-ttu-id="757cd-182">Définissez le fuseau horaire en fonction de vos propres et cochez la case pour inclure tous les scores d’intention prédits.</span><span class="sxs-lookup"><span data-stu-id="757cd-182">Set the time-zone to match yours, and check the box to include all predicted intent scores.</span></span> <span data-ttu-id="757cd-183">Enfin, cliquez sur «affecter une ressource».</span><span class="sxs-lookup"><span data-stu-id="757cd-183">Lastly, Click on "Assign resource."</span></span>

![Module4Chapter4step21im](images/module4chapter4step21im.PNG)

22. <span data-ttu-id="757cd-185">Sélectionnez locataire dans la première liste déroulante, puis sélectionnez paiement à l’accès dans la liste déroulante nom de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="757cd-185">Select tenant from the first dropdown, and select “Pay-as-you-go” in the Subscription Name dropdown.</span></span> <span data-ttu-id="757cd-186">Sous LUIS nom de la ressource, choisissez la ressource que nous avons créée ci-dessus dans les étapes 1-5.</span><span class="sxs-lookup"><span data-stu-id="757cd-186">Under LUIS resource name, choose the resource that we created above in steps 1-5.</span></span> <span data-ttu-id="757cd-187">Cliquez ensuite sur «affecter la ressource».</span><span class="sxs-lookup"><span data-stu-id="757cd-187">Then, click on "Assign resource."</span></span> 

![Module4Chapter4step22im](images/module4chapter4step22im.PNG)

> <span data-ttu-id="757cd-189">Remarque : Veillez à copier et à enregistrer l’URL de point de terminaison associée à la ressource que nous venons d’attribuer afin qu’elle soit facilement accessible pour la section suivante.</span><span class="sxs-lookup"><span data-stu-id="757cd-189">Note: Ensure to copy and save the Endpoint URL associated with the resource we just assigned so that it is easily accessible for the next section.</span></span>
>
> <span data-ttu-id="757cd-190">Remarque : Pour le nom du locataire, mettez votre entreprise ou votre profil créé pour cette application.</span><span class="sxs-lookup"><span data-stu-id="757cd-190">Note: For the Tenant name, put your corporation or profile that you created for this application.</span></span>

23. <span data-ttu-id="757cd-191">À présent, ouvrez la nouvelle application dans Unity et sélectionnez l’objet Lunarcom_Base dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="757cd-191">Now, open the new app in Unity and select the Lunarcom_Base object in the hierarchy.</span></span> <span data-ttu-id="757cd-192">Cliquez sur «Ajouter un composant» dans le panneau inspecteur et recherchez et sélectionnez «LunarcomIntentRecognizer».</span><span class="sxs-lookup"><span data-stu-id="757cd-192">Click “Add Component” in the inspector panel and search for and select “LunarcomIntentRecognizer.”</span></span>

![Module4Chapter4step23im](images/module4chapter4step23im.PNG)

24. <span data-ttu-id="757cd-194">Dans le champ de point de terminaison Luis de la «LunarcomIntentRecognizer» dans le panneau Inspecteur, entrez l’URL de point de terminaison que vous avez enregistrée à l’étape 22.</span><span class="sxs-lookup"><span data-stu-id="757cd-194">In the Luis Endpoint field of the "LunarcomIntentRecognizer" in the inspector panel, enter the Endpoint URL that you saved in step 22.</span></span> 

![Module4Chapter4step24im](images/module4chapter4step24im.PNG)

>  <span data-ttu-id="757cd-196">Remarque : Dans le composant «LunarcomOfflineRecognizer» du volet de l’inspecteur, assurez-vous que l’option «désactiver» est sélectionnée pour «SimulateOfflineMode». dans le cas contraire, le test du programme ne fonctionnera pas.</span><span class="sxs-lookup"><span data-stu-id="757cd-196">Note: In the "LunarcomOfflineRecognizer" component in the inspector panel, make sure that “disable” is selected for "SimulateOfflineMode" otherwise, testing the program will not work.</span></span> 

25. <span data-ttu-id="757cd-197">Appuyez sur le bouton lecture dans l’éditeur Unity et cliquez sur le bouton Rocket pour démarrer la reconnaissance intentionnelle.</span><span class="sxs-lookup"><span data-stu-id="757cd-197">Press the Play button in the Unity Editor and click the rocket button to start intent recognition.</span></span> <span data-ttu-id="757cd-198">À l’expression «sélectionnez le bouton lancer Rocket».</span><span class="sxs-lookup"><span data-stu-id="757cd-198">Utter the phrase “select the launch rocket button.”</span></span>

>  <span data-ttu-id="757cd-199">Remarque : L’application a reconnu la fonction souhaitée et activé le bouton Rocket.</span><span class="sxs-lookup"><span data-stu-id="757cd-199">Note: The app recognized the desired function and activated the rocket button.</span></span>
>
> ![Module4Chapter4step24im](images/module4chapter4note2im.PNG)

## <a name="congratulations"></a><span data-ttu-id="757cd-201">Félicitations</span><span class="sxs-lookup"><span data-stu-id="757cd-201">Congratulations</span></span>

<span data-ttu-id="757cd-202">Dans cette leçon, nous avons appris à ajouter des commandes vocales dotées de l’intelligence artificielle.</span><span class="sxs-lookup"><span data-stu-id="757cd-202">In this lesson, we learned how to add AI-powered speech commands!</span></span> <span data-ttu-id="757cd-203">À présent, votre programme peut reconnaître l’intention des utilisateurs même s’ils ne dictent pas de commandes vocales précises.</span><span class="sxs-lookup"><span data-stu-id="757cd-203">Now your program can recognize users' intent even if they do not utter precise voice commands.</span></span>

