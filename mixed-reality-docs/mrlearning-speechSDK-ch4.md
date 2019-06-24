## <a name="lesson-4"></a><span data-ttu-id="efde8-101">Leçon 4</span><span class="sxs-lookup"><span data-stu-id="efde8-101">Lesson 4</span></span>

<span data-ttu-id="efde8-102">Dans le chapitre 4, nous allons explorer la fonctionnalité intentionnelle de services de reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="efde8-102">In chapter 4, we will explore the Speech services Intent feature.</span></span> <span data-ttu-id="efde8-103">Nous configurer notre Azure LUIS Portal, le programme d’installation de notre intention/entités/énoncés, publier notre ressource intention, connecter notre application de Unity à notre intention de ressource et notre premier appel d’API d’intention.</span><span class="sxs-lookup"><span data-stu-id="efde8-103">We will set up our Azure LUIS Portal, setup our Intent/Entities/Utterances, publish our Intent Resource, connect our Unity app to our Intent Resource, and make our first Intent API call.</span></span>

1. <span data-ttu-id="efde8-104">Autoriser votre machine pour activer la dictée, pour ce faire, accédez aux paramètres de Windows, sélectionnez « confidentialité », puis « vocal » et enfin « écriture manuscrite & tapant » et activer les services de reconnaissance vocale et les suggestions de saisie.</span><span class="sxs-lookup"><span data-stu-id="efde8-104">Allow your machine to enable Dictation, to do this, go to Windows Settings, select "privacy," then "speech," and finally "inking & typing" and turn on speech services and typing suggestions.</span></span>

![Module4Chapter4step1aim](images/module4chapter4step1aim.PNG)

![Module4Chapter4step1bim](images/module4chapter4step1bim.PNG)

![Module4Chapter4step1cim](images/module4chapter4step1cim.PNG)

> <span data-ttu-id="efde8-108">Remarque : pour plus d’informations sur comment effectuer cette opération sur un Mac/Macbook, cliquez sur [ici](linkgoeshere).</span><span class="sxs-lookup"><span data-stu-id="efde8-108">note: for information on how to do this on a Mac/Macbook, click [here](linkgoeshere).</span></span>

2. <span data-ttu-id="efde8-109">Connectez-vous à la [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="efde8-109">Log in to the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="efde8-110">Une fois que vous êtes connecté, cliquez sur Créer une ressource et recherchez « Compréhension du langage », puis cliquez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="efde8-110">Once you are logged in, click on Create a resource, and search for "Language Understanding," and click enter.</span></span>

![Module4Chapter4step2im](images/module4chapter4step2im.PNG)

3. <span data-ttu-id="efde8-112">Sélectionnez le bouton Créer, pour créer une instance de ce service.</span><span class="sxs-lookup"><span data-stu-id="efde8-112">Select the Create button, to create an instance of this service.</span></span> <span data-ttu-id="efde8-113">Nommez votre projet « Speech_SDK_Learning_Module » et sélectionnez « Paiement. »</span><span class="sxs-lookup"><span data-stu-id="efde8-113">Name your project “Speech_SDK_Learning_Module” and select “Pay As You Go.”</span></span>

![Module4Chapter4step3aim](images/module4chapter4step3aim.png)

![Module4Chapter4step3bim](images/module4chapter4step3bim.PNG)

4. <span data-ttu-id="efde8-116">Sélectionnez votre région.</span><span class="sxs-lookup"><span data-stu-id="efde8-116">Select your Region.</span></span>  <span data-ttu-id="efde8-117">Pour les besoins de ce didacticiel, sélectionnez « (US) ouest des États-Unis. »</span><span class="sxs-lookup"><span data-stu-id="efde8-117">For the purpose of this tutorial, select "(US) West US."</span></span> <span data-ttu-id="efde8-118">Puis choisissez « F0 » pour le niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="efde8-118">Then choose "F0" for the pricing tier.</span></span> <span data-ttu-id="efde8-119">Cliquez maintenant sur « Créer » (situé dans le coin inférieur gauche) pour créer la ressource.</span><span class="sxs-lookup"><span data-stu-id="efde8-119">Now click "create" (located in the bottom left corner) to create the resource.</span></span>

   >  <span data-ttu-id="efde8-120">Remarque : une fois que vous avez cliqué sur « Créer », vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="efde8-120">note: once you have clicked on "create," you will have to wait for the service to be created, this might take a minute.</span></span>

5. <span data-ttu-id="efde8-121">Une fois que la ressource est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="efde8-121">A notification will appear in the portal once the Resource is created.</span></span> <span data-ttu-id="efde8-122">Cliquez sur cette notification et sélectionnez « Accéder à la ressource ».</span><span class="sxs-lookup"><span data-stu-id="efde8-122">Click on this notification and select "Go to resource."</span></span>

6. <span data-ttu-id="efde8-123">Dans la page « Démarrage rapide » de votre service de « API LUIS », accédez à la première étape, récupérez vos « clés » et cliquez sur « clés » (vous pouvez également y parvenir en cliquant sur le lien hypertexte bleu « clés », illustrés dans l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="efde8-123">From the "Quick Start" page of your "LUIS API" service, navigate to the first step, grab your "keys," and click "keys" (you can also achieve this by clicking the blue hyperlink "keys," shown in the image below).</span></span> <span data-ttu-id="efde8-124">Cela permet de révéler votre service, « Clés ».</span><span class="sxs-lookup"><span data-stu-id="efde8-124">This will reveal your service, "Keys."</span></span> <span data-ttu-id="efde8-125">Enregistrer une copie de l’une des clés afin de pouvoir l’utiliser ultérieurement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="efde8-125">Save a copy of one of the keys so you can use it later in the app.</span></span>

![Module4Chapter4step6im](images/module4chapter4step6im.PNG)

7. <span data-ttu-id="efde8-127">Dans la page « Démarrage rapide » sous 2 b de Section, cliquez sur « Portail Language Understanding » (illustré dans l’image ci-dessus) pour être redirigé vers la page Web que vous utiliserez pour créer votre nouveau service, au sein de l’application LUIS.</span><span class="sxs-lookup"><span data-stu-id="efde8-127">Back in the "Quick Start" page under Section 2b, click on "Language Understanding Portal" (shown in the image above) to be redirected to the webpage which you will use to create your new service, within the LUIS application.</span></span>

> <span data-ttu-id="efde8-128">Remarque : Lorsque vous atteignez un « Portail Language Understanding », vous devrez peut-être pour vous connecter, si vous n’êtes pas déjà fait, avec les mêmes informations d’identification que votre portail Azure.</span><span class="sxs-lookup"><span data-stu-id="efde8-128">note: Upon reaching the "Language Understanding Portal," you may need to login, if you are not already, with the same credentials as your Azure portal.</span></span> <span data-ttu-id="efde8-129">S’il s’agit de la première fois à l’aide de LUIS, vous devez faire défiler jusqu’en bas de la page d’accueil, pour rechercher et cliquez sur le bouton d’application « LUIS créer ».</span><span class="sxs-lookup"><span data-stu-id="efde8-129">If this is your first time using LUIS, you will need to scroll down to the bottom of the welcome page, to find and click on the "Create LUIS" app button.</span></span>

8. <span data-ttu-id="efde8-130">Une fois connecté, cliquez sur mes applications (si vous n’êtes pas dans cette section).</span><span class="sxs-lookup"><span data-stu-id="efde8-130">Once logged in, click My Apps (if you are not in that section currently).</span></span> <span data-ttu-id="efde8-131">Vous pouvez ensuite cliquer sur Créer une nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="efde8-131">You can then click on Create new app.</span></span> <span data-ttu-id="efde8-132">Nommez la nouvelle application « Module de formation Speech SDK ».</span><span class="sxs-lookup"><span data-stu-id="efde8-132">Name the new app “Speech SDK Learning Module.”</span></span> <span data-ttu-id="efde8-133">Ajoutez « Speech SDK Learning Module » dans le champ de description.</span><span class="sxs-lookup"><span data-stu-id="efde8-133">Add “Speech SDK Learning Module" to the description field, as well.</span></span> <span data-ttu-id="efde8-134">Puis cliquez sur « terminé ».</span><span class="sxs-lookup"><span data-stu-id="efde8-134">Then click "done."</span></span>

![Module4Chapter4step8aim](images/module4chapter4step8aim.PNG)

![Module4Chapter4step8bim](images/module4chapter4step8bim.PNG)

> <span data-ttu-id="efde8-137">Remarque : Si votre application est censée pour comprendre une langue différente de l’anglais, vous devez modifier la section « Culture » à la langue appropriée.</span><span class="sxs-lookup"><span data-stu-id="efde8-137">note: If your app is supposed to understand a language different from English, you should change the "Culture" to the appropriate language.</span></span>

9. <span data-ttu-id="efde8-138">Cliquez sur « Build » situé dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="efde8-138">Click “Build” located in the top right.</span></span>

10. <span data-ttu-id="efde8-139">Sous ressources de l’application sur la gauche, sélectionnez « Intentions » puis cliquez sur « Créer nouveau intention » et nommez-le « PressButton. »</span><span class="sxs-lookup"><span data-stu-id="efde8-139">Under App Assets on the left, select “Intents” then click “Create New Intent” and name it “PressButton.”</span></span> 

![Module4Chapter4step10im](images/module4chapter4step10im.PNG)

> <span data-ttu-id="efde8-141">Remarque : il est important d’utiliser les noms des intentions et entités utilisées dans ce didacticiel, car l’application Lunarcom référencera les par nom.</span><span class="sxs-lookup"><span data-stu-id="efde8-141">note: it is important to use the names of Intents and Entities used in this tutorial because the Lunarcom app will be referencing them by name.</span></span>  <span data-ttu-id="efde8-142">Pour d’autres projets, les conventions d’affectation de noms peuvent être votre choix.</span><span class="sxs-lookup"><span data-stu-id="efde8-142">For other projects, naming conventions can be whatever you choose.</span></span> 
>
> <span data-ttu-id="efde8-143">Remarque : vous devez maintenant avoir des 2 intentions - « PressButton » et « None ».</span><span class="sxs-lookup"><span data-stu-id="efde8-143">note: you should now have 2 Intents - “PressButton” and “None."</span></span>

11. <span data-ttu-id="efde8-144">Sous ressources de l’application sur la gauche, sélectionnez « Entités » et cliquez sur « Créer une nouvelle entité » et nommez-le « Action » et conserver le Type d’entité en tant que « Simple ».</span><span class="sxs-lookup"><span data-stu-id="efde8-144">Under App Assets on the left, select “Entities” and click “Create New Entity” and name it “Action” and keep the Entity Type as “Simple.”</span></span>

![Module4Chapter4step11im](images/module4chapter4step11im.PNG)

12. <span data-ttu-id="efde8-146">Cliquez de nouveau sur « Créer une nouvelle entité » et nommez-le « Cible » et conserver le Type d’entité en tant que « Simple » ainsi.</span><span class="sxs-lookup"><span data-stu-id="efde8-146">Click “Create New Entity” again and name it “Target” and keep the Entity Type as “Simple” as well.</span></span>

![Module4Chapter4step12im](images/module4chapter4step12im.PNG)

13. <span data-ttu-id="efde8-148">Sous ressources de l’application sur la gauche, sélectionnez « Intentions », puis cliquez sur votre intention de « PressButton » que vous avez créé à l’étape 10.</span><span class="sxs-lookup"><span data-stu-id="efde8-148">Under App Assets on the left, select "Intents" then click on your "PressButton" Intent that you created in step 10.</span></span>

![Module4Chapter4step13im](images/module4chapter4step13im.PNG)

14. <span data-ttu-id="efde8-150">Cliquez sur la liste déroulante de « Afficher les options » à droite et sélectionnez « Afficher les valeurs d’entité ».</span><span class="sxs-lookup"><span data-stu-id="efde8-150">Click on the "View options" dropdown on the right and select "show entity values."</span></span> 

    ![Module4Chapter4step14aim](images/module4chapter4step14aim.PNG)<span data-ttu-id="efde8-152">Cliquez sur le « entrer un exemple... »</span><span class="sxs-lookup"><span data-stu-id="efde8-152">Click on the “Enter an example…”</span></span> <span data-ttu-id="efde8-153">zone de texte.</span><span class="sxs-lookup"><span data-stu-id="efde8-153">textbox.</span></span> <span data-ttu-id="efde8-154">Ensuite, entrez les énoncés suivants :</span><span class="sxs-lookup"><span data-stu-id="efde8-154">Then, enter the following utterances:</span></span> 

![Module4Chapter4step14bim](images/module4chapter4step14bim.PNG)

15. <span data-ttu-id="efde8-156">Cliquez sur la liste déroulante de « Afficher les options » à droite et sélectionnez « Afficher les noms d’entité ».</span><span class="sxs-lookup"><span data-stu-id="efde8-156">Click on the "View options" dropdown on the right and select "Show entity names."</span></span>

![Module4Chapter4step15im](images/module4chapter4step15im.PNG)

16. <span data-ttu-id="efde8-158">Vous assurer que chacun des 10 énoncés ont les étiquettes d’entité suivants aux emplacements suivants de 1.) cliquant sur les mots sont mal étiquetées et, dans le menu contextuel, en sélectionnant « Supprimer l’étiquette » et 2.) en cliquant sur les mots qui doivent être étiquetées et, dans le menu contextuel, sélectionnez l’étiquette appropriée.</span><span class="sxs-lookup"><span data-stu-id="efde8-158">Ensure that each of the 10 Utterances have the following Entity labels in the following places by 1.) clicking on words that are mislabeled and, in the popup, selecting "remove label" and 2.) clicking on words that should be labeled and, in the popup, selecting the appropriate label.</span></span>

![Module4Chapter4step16im](images/module4chapter4step16im.PNG)

17. <span data-ttu-id="efde8-160">Maintenant, pour publier le modèle, cliquez sur « Train » dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="efde8-160">Now, to publish the model, click "Train" in the top right.</span></span> <span data-ttu-id="efde8-161">Ensuite, une fois le traitement terminé, cliquez sur « Test » dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="efde8-161">Then, once it has finished processing, click "Test" in the top right.</span></span>

![Module4Chapter4step17im](images/module4chapter4step17im.PNG)

18. <span data-ttu-id="efde8-163">Entrez dans « Sélectionner le bouton de lancement » dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="efde8-163">Enter in “select the launch button” in  the textbox.</span></span>

> <span data-ttu-id="efde8-164">Remarque : nous n’avez pas ajouté la « select » en tant qu’action dans un de nos énoncés - mais si vous cliquez sur « Inspecter », le modèle reconnu « sélectionner » comme une entité de l’action.</span><span class="sxs-lookup"><span data-stu-id="efde8-164">note: we did not add “select” as an action in any of our Utterances - but if you click on “Inspect,” the model recognized “select” as an action entity.</span></span>
>
> ![Module4Chapter4noteim](images/module4chapter4noteim.PNG)

19. <span data-ttu-id="efde8-166">Maintenant, cliquez sur « Publier » dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="efde8-166">Now, click "publish" in the top right.</span></span> <span data-ttu-id="efde8-167">Vérifiez que la liste déroulante intitulée « Production » et cliquez sur « Publier » dans la fenêtre contextuelle également.</span><span class="sxs-lookup"><span data-stu-id="efde8-167">Ensure the dropdown says “Production” and click "publish" on the popup as well.</span></span> 

![Module4Chapter4step19im](images/module4chapter4step19im.PNG)

20. <span data-ttu-id="efde8-169">Une fois publié, une barre verte doit apparaître en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="efde8-169">Once published, a green bar should appear at the top of the page.</span></span>  <span data-ttu-id="efde8-170">Cliquez sur la barre verte pour accéder à la page « Gérer ».</span><span class="sxs-lookup"><span data-stu-id="efde8-170">Click on the green bar to be taken to the "Manage" page.</span></span> 

![Module4Chapter4step20im](images/module4chapter4step20im.PNG)

21. <span data-ttu-id="efde8-172">Cliquez sur « Clés et points de terminaison » sous « Paramètres de l’Application » à gauche.</span><span class="sxs-lookup"><span data-stu-id="efde8-172">Click on "Keys and Endpoints" under “Application Settings” to the left.</span></span> <span data-ttu-id="efde8-173">Ensuite, définissez la liste déroulante « Publish To » en tant que « Production ».</span><span class="sxs-lookup"><span data-stu-id="efde8-173">Then, set the drop down "Publish To" as "Production."</span></span> <span data-ttu-id="efde8-174">Définir le fuseau horaire à correspondent aux vôtres, puis cochez la case pour inclure toutes les notes intentions prédites.</span><span class="sxs-lookup"><span data-stu-id="efde8-174">Set the time-zone to match yours, and check the box to include all predicted intent scores.</span></span> <span data-ttu-id="efde8-175">Enfin, cliquez sur « Ressource Assign. »</span><span class="sxs-lookup"><span data-stu-id="efde8-175">Lastly, Click on "Assign resource."</span></span>

![Module4Chapter4step21im](images/module4chapter4step21im.PNG)

22. <span data-ttu-id="efde8-177">Sélectionnez le client à partir de la première liste déroulante et sélectionnez « Paiement à l’utilisation » dans la liste déroulante Nom de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="efde8-177">Select tenant from the first dropdown, and select “Pay-as-you-go” in the Subscription Name dropdown.</span></span> <span data-ttu-id="efde8-178">Sous le nom de la ressource LUIS, choisissez la ressource que nous avons créé ci-dessus dans les étapes 1 à 5.</span><span class="sxs-lookup"><span data-stu-id="efde8-178">Under LUIS resource name, choose the resource that we created above in steps 1-5.</span></span> <span data-ttu-id="efde8-179">Ensuite, cliquez sur « Ressource Assign. »</span><span class="sxs-lookup"><span data-stu-id="efde8-179">Then, click on "Assign resource."</span></span> 

![Module4Chapter4step22im](images/module4chapter4step22im.PNG)

> <span data-ttu-id="efde8-181">Remarque : veillez à copier et enregistrer l’URL de point de terminaison associé à la ressource que nous avons attribués simplement afin qu’il soit facilement accessible pour la section suivante.</span><span class="sxs-lookup"><span data-stu-id="efde8-181">note: ensure to copy and save the Endpoint URL associated with the resource we just assigned so that it is easily accessible for the next section.</span></span>
>
> <span data-ttu-id="efde8-182">Remarque : pour le nom du client, placez votre entreprise ou le profil que vous avez créé pour cette application.</span><span class="sxs-lookup"><span data-stu-id="efde8-182">note: for the Tenant name, put your corporation or profile that you created for this application.</span></span>

23. <span data-ttu-id="efde8-183">À présent, ouvrez la nouvelle application dans Unity et sélectionnez l’objet Lunarcom_Base dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="efde8-183">Now, open the new app in Unity and select the Lunarcom_Base object in the hierarchy.</span></span> <span data-ttu-id="efde8-184">Cliquez sur « Ajouter un composant » dans le panneau d’inspecteur, recherchez puis sélectionnez « LunarcomIntentRecognizer ».</span><span class="sxs-lookup"><span data-stu-id="efde8-184">Click “Add Component” in the inspector panel and search for and select “LunarcomIntentRecognizer.”</span></span>

![Module4Chapter4step23im](images/module4chapter4step23im.PNG)

24. <span data-ttu-id="efde8-186">Dans le champ Luis Endpoint de « LunarcomIntentRecognizer » dans le panneau d’inspecteur, entrez l’URL de point de terminaison que vous avez enregistré à l’étape 22.</span><span class="sxs-lookup"><span data-stu-id="efde8-186">In the Luis Endpoint field of the "LunarcomIntentRecognizer" in the inspector panel, enter the Endpoint URL that you saved in step 22.</span></span> 

![Module4Chapter4step24im](images/module4chapter4step24im.PNG)

>  <span data-ttu-id="efde8-188">Remarque : Dans le composant « LunarcomOfflineRecognizer » dans le panneau d’inspecteur, assurez-vous que « désactiver » est activée pour « SimulateOfflineMode » dans le cas contraire, le programme de test ne fonctionnera pas.</span><span class="sxs-lookup"><span data-stu-id="efde8-188">note: In the "LunarcomOfflineRecognizer" component in the inspector panel, make sure that “disable” is selected for "SimulateOfflineMode" otherwise, testing the program will not work.</span></span> 

25. <span data-ttu-id="efde8-189">Appuyez sur le bouton de lecture dans l’éditeur Unity, puis cliquez sur le bouton de fusée pour démarrer la reconnaissance des intentions.</span><span class="sxs-lookup"><span data-stu-id="efde8-189">Press the Play button in the Unity Editor and click the rocket button to start intent recognition.</span></span> <span data-ttu-id="efde8-190">Prononcez la phrase « sélectionner le bouton de fusée lancement ».</span><span class="sxs-lookup"><span data-stu-id="efde8-190">Utter the phrase “select the launch rocket button.”</span></span>

>  <span data-ttu-id="efde8-191">Remarque : L’application reconnu la fonction souhaitée et activé le bouton de fusée.</span><span class="sxs-lookup"><span data-stu-id="efde8-191">note: The app recognized the desired function and activated the rocket button.</span></span>
>
> ![Module4Chapter4step24im](images/module4chapter4note2im.PNG)

## <a name="congratulations"></a><span data-ttu-id="efde8-193">Félicitations</span><span class="sxs-lookup"><span data-stu-id="efde8-193">Congratulations</span></span>

<span data-ttu-id="efde8-194">Vous avez officiellement appris comment ajouter des commandes vocales à partir du programme de kit de développement logiciel de reconnaissance vocale !</span><span class="sxs-lookup"><span data-stu-id="efde8-194">You officially learned how to add speech commands from the speech SDK program!</span></span> <span data-ttu-id="efde8-195">Maintenant, votre programme puisse reconnaître les commandes vocales de toutes sortes de variantes.</span><span class="sxs-lookup"><span data-stu-id="efde8-195">Now your program can recognize speech commands of all kinds of variants.</span></span> <span data-ttu-id="efde8-196">Tester et amuser un peu avec lui !</span><span class="sxs-lookup"><span data-stu-id="efde8-196">Test it out and have a little fun with it!</span></span>

[<span data-ttu-id="efde8-197">Leçon suivante : Kit de développement logiciel de reconnaissance vocale leçon 5</span><span class="sxs-lookup"><span data-stu-id="efde8-197">Next Lesson: Speech SDK Lesson 5</span></span>](placeholderlink)

