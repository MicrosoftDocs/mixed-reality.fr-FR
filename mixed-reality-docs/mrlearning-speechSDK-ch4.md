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
# <a name="4-setting-up-intent-and-natural-language-understanding"></a><span data-ttu-id="9ec18-105">4. Configuration de l’intention et de la compréhension du langage naturel</span><span class="sxs-lookup"><span data-stu-id="9ec18-105">4. Setting up intent and natural language understanding</span></span>

<span data-ttu-id="9ec18-106">Dans cette leçon, vous allez explorer la fonctionnalité d’intention du service Azure Speech.</span><span class="sxs-lookup"><span data-stu-id="9ec18-106">In this lesson, you will explore the Azure Speech Service's Intent feature.</span></span> <span data-ttu-id="9ec18-107">La fonctionnalité d’intention vous permet d’équiper notre application avec des commandes vocales en intelligence artificielle, où les utilisateurs peuvent indiquer des commandes vocales non spécifiques tout en gardant leur intention compréhensible par le système.</span><span class="sxs-lookup"><span data-stu-id="9ec18-107">The Intent feature allows you to equip our application with AI-powered voice commands, where users can say non-specific voice commands and still have their intent understood by the system.</span></span> <span data-ttu-id="9ec18-108">Au cours de cette leçon, nous allons configurer notre portail Azure LUIS, configurer nos intentions/entités/énoncés, publier notre ressource intentionnelle, connecter notre application Unity à notre ressource intentionnelle et effectuer notre premier appel d’API d’intention.</span><span class="sxs-lookup"><span data-stu-id="9ec18-108">During this lesson, we will set up our Azure LUIS Portal, setup our Intent/Entities/Utterances, publish our Intent Resource, connect our Unity app to our Intent Resource, and make our first Intent API call.</span></span>

## <a name="objectives"></a><span data-ttu-id="9ec18-109">Objectifs</span><span class="sxs-lookup"><span data-stu-id="9ec18-109">Objectives</span></span>

- <span data-ttu-id="9ec18-110">Découvrez comment configurer l’intention et la compréhension du langage naturel dans notre application</span><span class="sxs-lookup"><span data-stu-id="9ec18-110">Learn how to set up intent and natural language understanding in our application</span></span>
- <span data-ttu-id="9ec18-111">Découvrez comment configurer le portail LUIS d’Azure</span><span class="sxs-lookup"><span data-stu-id="9ec18-111">Learn how to set up Azure's LUIS Portal</span></span>
- <span data-ttu-id="9ec18-112">Découvrez comment configurer l’intention, les entités et les énoncés sur Azure</span><span class="sxs-lookup"><span data-stu-id="9ec18-112">Learn how to set up intent, entities, and utterances on Azure</span></span>

## <a name="instructions"></a><span data-ttu-id="9ec18-113">Instructions</span><span class="sxs-lookup"><span data-stu-id="9ec18-113">Instructions</span></span>

1. <span data-ttu-id="9ec18-114">Autorisez votre ordinateur à activer la dictée.</span><span class="sxs-lookup"><span data-stu-id="9ec18-114">Allow your machine to enable Dictation.</span></span> <span data-ttu-id="9ec18-115">Pour ce faire, accédez à paramètres Windows, sélectionnez « confidentialité », puis « parole », suivi de « entrée manuscrite & typage » et activez Speech services et suggestions de saisie.</span><span class="sxs-lookup"><span data-stu-id="9ec18-115">To do this, go to Windows Settings, select "privacy," then "speech," followed by "inking & typing" and turn on speech services and typing suggestions.</span></span>

    ![Module4Chapter4step1aim](images/module4chapter4step1aim.PNG)

    ![Module4Chapter4step1bim](images/module4chapter4step1bim.PNG)

    ![Module4Chapter4step1cim](images/module4chapter4step1cim.PNG)

2. <span data-ttu-id="9ec18-119">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9ec18-119">Log in to the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="9ec18-120">Une fois que vous êtes connecté, cliquez sur créer une ressource, recherchez « Language Understanding », puis cliquez sur entrée.</span><span class="sxs-lookup"><span data-stu-id="9ec18-120">Once you are logged in, click on Create a resource, search for "Language Understanding" and click Enter.</span></span>

    ![mrlearning-Speech-CH4-1-Step2. png](images/mrlearning-speech-ch4-1-step2.png)

3. <span data-ttu-id="9ec18-122">Cliquez sur le bouton **créer** pour créer une instance de ce service.</span><span class="sxs-lookup"><span data-stu-id="9ec18-122">Click the **Create** button to create an instance of this service.</span></span>

    ![mrlearning-Speech-CH4-1-step3a. png](images/mrlearning-speech-ch4-1-step3a.png)

    <span data-ttu-id="9ec18-124">Donnez un **nom**à votre ressource, par exemple *Speech-SDK-Learning-module*.</span><span class="sxs-lookup"><span data-stu-id="9ec18-124">Give your resource a **Name**, for example, *Speech-SDK-Learning-Module*.</span></span> <span data-ttu-id="9ec18-125">Pour **abonnement**, sélectionnez *paiement à l'* enregistrement ou *fin* si vous disposez d’un compte d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="9ec18-125">For **Subscription**, select *Pay As You Go* or *Free Trail* if you have a trial account.</span></span> <span data-ttu-id="9ec18-126">Ensuite, créez un nouveau **groupe de ressources** en cliquant sur le lien **créer** , entrez un nom, par exemple, *HoloLens-2-Tutorials-Resource-Group*, puis cliquez sur le bouton **OK** .</span><span class="sxs-lookup"><span data-stu-id="9ec18-126">Next, create a new **Resource Group** by clicking the **Create new** link, enter a name, for example, *HoloLens-2-Tutorials-Resource-Group*, and click the **OK** button.</span></span>

    ![mrlearning-Speech-CH4-1-step3b. png](images/mrlearning-speech-ch4-1-step3b.png)

4. <span data-ttu-id="9ec18-128">Sélectionnez votre **emplacement de création** et l' **emplacement d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="9ec18-128">Select your **Authoring location** and **Runtime location**.</span></span> <span data-ttu-id="9ec18-129">Pour les besoins de ce didacticiel, utilisez *(États-Unis) Ouest des États-Unis*, puis choisissez *F0 (5 appels par seconde, 10 000 appels par mois)* pour le niveau **tarifaire de création** et le **niveau tarifaire d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="9ec18-129">For the purpose of this tutorial, use *(US) West US*, then choose *F0 (5 Calls per second, 10K Calls per month)* for the **Authoring pricing tier** and **Runtime pricing tier**.</span></span> <span data-ttu-id="9ec18-130">Enfin, cliquez sur le bouton **créer** pour créer la ressource, ainsi que sur le nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="9ec18-130">Finally, click the **Create** button to create the resource, as well as the new resource group.</span></span>

    ![mrlearning-Speech-CH4-1-step4. png](images/mrlearning-speech-ch4-1-step4.png)

    >[!NOTE]
    ><span data-ttu-id="9ec18-132">Après avoir cliqué sur le bouton créer, vous devez attendre que le service soit créé, ce qui peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="9ec18-132">After you click the Create button, you will have to wait for the service to be created, which might take a few minutes.</span></span>

5. <span data-ttu-id="9ec18-133">Une fois le processus de création de la ressource terminé, vous verrez le message **votre déploiement est terminé**.</span><span class="sxs-lookup"><span data-stu-id="9ec18-133">Once the resource creation process is complete, you will see the message **Your deployment is complete**.</span></span>

    ![mrlearning-Speech-CH4-1-step5. png](images/mrlearning-speech-ch4-1-step5.png)

6. <span data-ttu-id="9ec18-135">À l’aide du même compte d’utilisateur, connectez-vous au portail [Language Understanding intelligent service (Luis)](https://www.luis.ai/) , sélectionnez votre pays et acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="9ec18-135">Using the same user account, sign in to the [Language Understanding Intelligent Service (LUIS)](https://www.luis.ai/) portal, select your country, and agree to the terms of use.</span></span>

    >[!NOTE]
    ><span data-ttu-id="9ec18-136">Quand vous atteignez le portail Language Understanding, vous devrez peut-être vous connecter, si ce n’est déjà fait, avec les mêmes informations d’identification que votre Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9ec18-136">Upon reaching the Language Understanding portal, you may need to log in, if you are not already, with the same credentials as your Azure portal.</span></span> <span data-ttu-id="9ec18-137">Si vous utilisez LUIS pour la première fois, vous devez faire défiler vers le bas de la page d’accueil pour rechercher et cliquer sur le bouton « créer une application LUIS ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-137">If this is your first time using LUIS, you will need to scroll down to the bottom of the Welcome page to find and click the "Create LUIS" app button.</span></span>

7. <span data-ttu-id="9ec18-138">Une fois connecté, cliquez sur mes applications (si vous n’êtes pas actuellement dans cette section).</span><span class="sxs-lookup"><span data-stu-id="9ec18-138">Once logged in, click My Apps (if you are not currently in that section).</span></span> <span data-ttu-id="9ec18-139">Vous pouvez ensuite cliquer sur créer une nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="9ec18-139">You can then click on Create new app.</span></span> <span data-ttu-id="9ec18-140">Nommez la nouvelle application « Speech SDK Learning module ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-140">Name the new app “Speech SDK Learning Module.”</span></span> <span data-ttu-id="9ec18-141">Ajoutez également « module d’apprentissage du kit de développement logiciel (SDK) Speech » au champ Description.</span><span class="sxs-lookup"><span data-stu-id="9ec18-141">Add “Speech SDK Learning Module" to the description field, as well.</span></span> <span data-ttu-id="9ec18-142">Cliquez ensuite sur « terminé ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-142">Then click "done."</span></span>

    ![Module4Chapter4step8aim](images/module4chapter4step8aim.PNG)

    ![Module4Chapter4step8bim](images/module4chapter4step8bim.PNG)

    >[!NOTE]
    ><span data-ttu-id="9ec18-145">Si votre application est censée comprendre une langue différente de l’anglais, vous devez remplacer la « culture » par la langue appropriée.</span><span class="sxs-lookup"><span data-stu-id="9ec18-145">If your app is supposed to understand a language different from English, you should change the "Culture" to the appropriate language.</span></span>

8. <span data-ttu-id="9ec18-146">Cliquez sur « Build » situé en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="9ec18-146">Click “Build” located in the top right.</span></span>

9. <span data-ttu-id="9ec18-147">Sous ressources de l’application sur la gauche, sélectionnez « intentions », puis cliquez sur « créer un nouvel objectif » et nommez-la « PressButton ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-147">Under App Assets on the left, select “Intents” then click “Create New Intent” and name it “PressButton.”</span></span>

    ![Module4Chapter4step10im](images/module4chapter4step10im.PNG)

    >[!NOTE]
    ><span data-ttu-id="9ec18-149">Il est important d’utiliser les noms des intentions et des entités utilisées dans ce didacticiel, car l’application Lunarcom y fait référence par nom.</span><span class="sxs-lookup"><span data-stu-id="9ec18-149">It is important to use the names of Intents and Entities used in this tutorial because the Lunarcom app will be referencing them by name.</span></span>

    >[!NOTE]
    ><span data-ttu-id="9ec18-150">Vous devez maintenant avoir 2 intentions-« PressButton » et « None ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-150">You should now have 2 Intents - “PressButton” and “None."</span></span>

10. <span data-ttu-id="9ec18-151">Sous ressources de l’application sur la gauche, sélectionnez « entités », cliquez sur « créer une nouvelle entité », nommez-la « action » et conservez le type d’entité « simple ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-151">Under App Assets on the left, select “Entities”, click “Create New Entity”, name it “Action” and keep the Entity Type as “Simple.”</span></span>

    ![Module4Chapter4step11im](images/module4chapter4step11im.PNG)

11. <span data-ttu-id="9ec18-153">Cliquez à nouveau sur « créer une nouvelle entité » et nommez-la « cible ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-153">Click “Create New Entity” again and name it “Target”.</span></span> <span data-ttu-id="9ec18-154">Conservez également le type d’entité « simple ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-154">Keep the Entity Type as “Simple”, as well.</span></span>

    ![Module4Chapter4step12im](images/module4chapter4step12im.PNG)

12. <span data-ttu-id="9ec18-156">Sous ressources de l’application sur la gauche, sélectionnez « intentions », puis cliquez sur l’intention « PressButton » que vous avez créée à l’étape 10.</span><span class="sxs-lookup"><span data-stu-id="9ec18-156">Under App Assets on the left, select "Intents" then click on your "PressButton" Intent that you created in step 10.</span></span>

    ![Module4Chapter4step13im](images/module4chapter4step13im.PNG)

13. <span data-ttu-id="9ec18-158">Cliquez sur la liste déroulante « Afficher les options » à droite et sélectionnez « Afficher les valeurs d’entité ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-158">Click the "View options" dropdown on the right and select "show entity values."</span></span>

    ![Module4Chapter4step14aim](images/module4chapter4step14aim.PNG)

    <span data-ttu-id="9ec18-160">Cliquez sur « Entrez un exemple... »</span><span class="sxs-lookup"><span data-stu-id="9ec18-160">Click the “Enter an example…”</span></span> <span data-ttu-id="9ec18-161">entr.</span><span class="sxs-lookup"><span data-stu-id="9ec18-161">textbox.</span></span> <span data-ttu-id="9ec18-162">Ensuite, entrez les énoncés suivants :</span><span class="sxs-lookup"><span data-stu-id="9ec18-162">Then, enter the following utterances:</span></span>

    ![Module4Chapter4step14bim](images/module4chapter4step14bim.PNG)

14. <span data-ttu-id="9ec18-164">Cliquez sur la liste déroulante « Afficher les options » à droite, puis sélectionnez « Afficher les noms d’entité ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-164">Click the "View options" dropdown on the right and select "Show entity names."</span></span>

    ![Module4Chapter4step15im](images/module4chapter4step15im.PNG)

15. <span data-ttu-id="9ec18-166">Assurez-vous que chacun des 10 énoncés a les étiquettes d’entité suivantes dans les emplacements suivants, de 1.) en cliquant sur les mots dont l’étiquette est incorrecte et, dans le menu contextuel, sélectionnez « Supprimer l’étiquette » et 2.) en cliquant sur les mots qui doivent être étiquetés et, dans le menu contextuel, sélectionnez l’étiquette appropriée.</span><span class="sxs-lookup"><span data-stu-id="9ec18-166">Ensure that each of the 10 Utterances have the following Entity labels in the following places by 1.) clicking on words that are mislabeled and, in the popup, selecting "remove label" and 2.) clicking on words that should be labeled and, in the popup, selecting the appropriate label.</span></span>

    ![Module4Chapter4step16im](images/module4chapter4step16im.PNG)

16. <span data-ttu-id="9ec18-168">À présent, pour publier le modèle, cliquez sur « train » dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="9ec18-168">Now, to publish the model, click "Train" in the top right.</span></span> <span data-ttu-id="9ec18-169">Ensuite, une fois le traitement terminé, cliquez sur « test » dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="9ec18-169">Then, once it has finished processing, click "Test" in the top right.</span></span>

    ![Module4Chapter4step17im](images/module4chapter4step17im.PNG)

17. <span data-ttu-id="9ec18-171">Entrez dans la zone de texte « sélectionner le bouton lancer ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-171">Enter in “select the launch button” in  the textbox.</span></span>

    >[!NOTE]
    ><span data-ttu-id="9ec18-172">Nous n’avons pas ajouté « Select » comme action dans l’un de nos énoncés, mais si vous cliquez sur « Inspect », le modèle a reconnu « Select » comme une entité d’action.</span><span class="sxs-lookup"><span data-stu-id="9ec18-172">We did not add “select” as an action in any of our Utterances, but if you click on “Inspect,” the model recognized “select” as an action entity.</span></span>
    >
    > ![Module4Chapter4noteim](images/module4chapter4noteim.PNG)

18. <span data-ttu-id="9ec18-174">Cliquez sur « publier » dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="9ec18-174">Click "publish" in the top right.</span></span> <span data-ttu-id="9ec18-175">Assurez-vous que la liste déroulante indique « production », puis cliquez sur « publier » dans la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="9ec18-175">Ensure the dropdown says “Production” and click "publish" on the popup, as well.</span></span>

    ![Module4Chapter4step19im](images/module4chapter4step19im.PNG)

19. <span data-ttu-id="9ec18-177">Une fois publiée, une barre verte doit apparaître en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="9ec18-177">Once published, a green bar should appear at the top of the page.</span></span> <span data-ttu-id="9ec18-178">Cliquez sur la barre verte pour afficher la page « gérer ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-178">Click the green bar to view the "Manage" page.</span></span>

    ![Module4Chapter4step20im](images/module4chapter4step20im.PNG)

20. <span data-ttu-id="9ec18-180">Cliquez sur « clés et points de terminaison » sous « paramètres d’application » à gauche.</span><span class="sxs-lookup"><span data-stu-id="9ec18-180">Click "Keys and Endpoints" under “Application Settings” to the left.</span></span> <span data-ttu-id="9ec18-181">Ensuite, définissez la liste déroulante « publier sur » sur « production ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-181">Then, set the drop down "Publish To" as "Production."</span></span> <span data-ttu-id="9ec18-182">Définissez le fuseau horaire en fonction de vos propres et cochez la case pour inclure tous les scores d’intention prédits.</span><span class="sxs-lookup"><span data-stu-id="9ec18-182">Set the time-zone to match yours, and check the box to include all predicted intent scores.</span></span> <span data-ttu-id="9ec18-183">Enfin, cliquez sur « affecter une ressource ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-183">Lastly, click "Assign resource."</span></span>

    ![Module4Chapter4step21im](images/module4chapter4step21im.PNG)

21. <span data-ttu-id="9ec18-185">Sélectionnez locataire dans la première liste déroulante et sélectionnez « paiement à l’accès » dans la liste déroulante nom de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="9ec18-185">Select tenant from the first dropdown and select “Pay-as-you-go” in the Subscription Name dropdown.</span></span> <span data-ttu-id="9ec18-186">Sous LUIS nom de la ressource, choisissez la ressource que nous avons créée ci-dessus dans les étapes 1-5.</span><span class="sxs-lookup"><span data-stu-id="9ec18-186">Under LUIS resource name, choose the resource that we created above in steps 1-5.</span></span> <span data-ttu-id="9ec18-187">Cliquez ensuite sur « affecter la ressource ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-187">Then, click on "Assign resource."</span></span>

    ![Module4Chapter4step22im](images/module4chapter4step22im.PNG)

    >[!NOTE]
    ><span data-ttu-id="9ec18-189">Veillez à copier et à enregistrer l’URL de point de terminaison associée à la ressource que nous venons d’attribuer afin qu’elle soit facilement accessible pour la section suivante.</span><span class="sxs-lookup"><span data-stu-id="9ec18-189">Ensure to copy and save the Endpoint URL associated with the resource we just assigned so it is easily accessible for the next section.</span></span>

    >[!NOTE]
    ><span data-ttu-id="9ec18-190">Pour le nom du locataire, mettez votre entreprise ou votre profil créé pour cette application.</span><span class="sxs-lookup"><span data-stu-id="9ec18-190">For the Tenant name, put your corporation or profile that you created for this application.</span></span>

22. <span data-ttu-id="9ec18-191">À présent, ouvrez la nouvelle application dans Unity et sélectionnez l’objet Lunarcom_Base dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="9ec18-191">Now, open the new app in Unity and select the Lunarcom_Base object in the hierarchy.</span></span> <span data-ttu-id="9ec18-192">Cliquez sur « Ajouter un composant » dans le panneau inspecteur et recherchez et sélectionnez « LunarcomIntentRecognizer ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-192">Click “Add Component” in the inspector panel and search for and select “LunarcomIntentRecognizer.”</span></span>

    ![Module4Chapter4step23im](images/module4chapter4step23im.PNG)

23. <span data-ttu-id="9ec18-194">Dans le champ de point de terminaison Luis de la « LunarcomIntentRecognizer » dans le panneau Inspecteur, entrez l’URL de point de terminaison que vous avez enregistrée à l’étape 22.</span><span class="sxs-lookup"><span data-stu-id="9ec18-194">In the Luis Endpoint field of the "LunarcomIntentRecognizer" in the inspector panel, enter the Endpoint URL that you saved in step 22.</span></span>

    ![Module4Chapter4step24im](images/module4chapter4step24im.PNG)

    >[!NOTE]
    ><span data-ttu-id="9ec18-196">Dans le composant « LunarcomOfflineRecognizer » du volet de l’inspecteur, assurez-vous que l’option « désactiver » est sélectionnée pour « SimulateOfflineMode ». dans le cas contraire, le test du programme ne fonctionnera pas.</span><span class="sxs-lookup"><span data-stu-id="9ec18-196">In the "LunarcomOfflineRecognizer" component in the inspector panel, make sure that “disable” is selected for "SimulateOfflineMode" otherwise, testing the program will not work.</span></span>

24. <span data-ttu-id="9ec18-197">Appuyez sur le bouton lecture dans l’éditeur Unity et cliquez sur le bouton Rocket pour démarrer la reconnaissance intentionnelle.</span><span class="sxs-lookup"><span data-stu-id="9ec18-197">Press the Play button in the Unity Editor and click the rocket button to start intent recognition.</span></span> <span data-ttu-id="9ec18-198">À l’expression « sélectionnez le bouton lancer Rocket ».</span><span class="sxs-lookup"><span data-stu-id="9ec18-198">Utter the phrase “select the launch rocket button.”</span></span>

    >[!NOTE]
    ><span data-ttu-id="9ec18-199">L’application a reconnu la fonction souhaitée et activé le bouton Rocket.</span><span class="sxs-lookup"><span data-stu-id="9ec18-199">The app recognized the desired function and activated the rocket button.</span></span>
    >
    >![Module4Chapter4step24im](images/module4chapter4note2im.PNG)

## <a name="congratulations"></a><span data-ttu-id="9ec18-201">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9ec18-201">Congratulations</span></span>

<span data-ttu-id="9ec18-202">Dans cette leçon, vous avez appris à ajouter des commandes vocales dotées de l’intelligence artificielle.</span><span class="sxs-lookup"><span data-stu-id="9ec18-202">In this lesson, you learned how to add AI-powered speech commands.</span></span> <span data-ttu-id="9ec18-203">À présent, votre programme peut reconnaître l’intention des utilisateurs, même s’ils ne sont pas en train de dicter des commandes vocales précises !</span><span class="sxs-lookup"><span data-stu-id="9ec18-203">Now your program can recognize users' intent, even if they do not utter precise voice commands!</span></span>
