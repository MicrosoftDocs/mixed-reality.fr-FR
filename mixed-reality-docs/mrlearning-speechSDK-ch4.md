## <a name="lesson-4"></a>Leçon 4

Dans le chapitre 4, nous allons explorer la fonctionnalité intentionnelle de services de reconnaissance vocale. Nous configurer notre Azure LUIS Portal, le programme d’installation de notre intention/entités/énoncés, publier notre ressource intention, connecter notre application de Unity à notre intention de ressource et notre premier appel d’API d’intention.

1. Autoriser votre machine pour activer la dictée, pour ce faire, accédez aux paramètres de Windows, sélectionnez « confidentialité », puis « vocal » et enfin « écriture manuscrite & tapant » et activer les services de reconnaissance vocale et les suggestions de saisie.

![Module4Chapter4step1aim](images/module4chapter4step1aim.PNG)

![Module4Chapter4step1bim](images/module4chapter4step1bim.PNG)

![Module4Chapter4step1cim](images/module4chapter4step1cim.PNG)

> Remarque : pour plus d’informations sur comment effectuer cette opération sur un Mac/Macbook, cliquez sur [ici](linkgoeshere).

2. Connectez-vous à la [Azure Portal](https://portal.azure.com/). Une fois que vous êtes connecté, cliquez sur Créer une ressource et recherchez « Compréhension du langage », puis cliquez sur ENTRÉE.

![Module4Chapter4step2im](images/module4chapter4step2im.PNG)

3. Sélectionnez le bouton Créer, pour créer une instance de ce service. Nommez votre projet « Speech_SDK_Learning_Module » et sélectionnez « Paiement. »

![Module4Chapter4step3aim](images/module4chapter4step3aim.png)

![Module4Chapter4step3bim](images/module4chapter4step3bim.PNG)

4. Sélectionnez votre région.  Pour les besoins de ce didacticiel, sélectionnez « (US) ouest des États-Unis. » Puis choisissez « F0 » pour le niveau tarifaire. Cliquez maintenant sur « Créer » (situé dans le coin inférieur gauche) pour créer la ressource.

   >  Remarque : une fois que vous avez cliqué sur « Créer », vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.

5. Une fois que la ressource est créée, une notification s’affiche dans le portail. Cliquez sur cette notification et sélectionnez « Accéder à la ressource ».

6. Dans la page « Démarrage rapide » de votre service de « API LUIS », accédez à la première étape, récupérez vos « clés » et cliquez sur « clés » (vous pouvez également y parvenir en cliquant sur le lien hypertexte bleu « clés », illustrés dans l’image ci-dessous). Cela permet de révéler votre service, « Clés ». Enregistrer une copie de l’une des clés afin de pouvoir l’utiliser ultérieurement dans l’application.

![Module4Chapter4step6im](images/module4chapter4step6im.PNG)

7. Dans la page « Démarrage rapide » sous 2 b de Section, cliquez sur « Portail Language Understanding » (illustré dans l’image ci-dessus) pour être redirigé vers la page Web que vous utiliserez pour créer votre nouveau service, au sein de l’application LUIS.

> Remarque : Lorsque vous atteignez un « Portail Language Understanding », vous devrez peut-être pour vous connecter, si vous n’êtes pas déjà fait, avec les mêmes informations d’identification que votre portail Azure. S’il s’agit de la première fois à l’aide de LUIS, vous devez faire défiler jusqu’en bas de la page d’accueil, pour rechercher et cliquez sur le bouton d’application « LUIS créer ».

8. Une fois connecté, cliquez sur mes applications (si vous n’êtes pas dans cette section). Vous pouvez ensuite cliquer sur Créer une nouvelle application. Nommez la nouvelle application « Module de formation Speech SDK ». Ajoutez « Speech SDK Learning Module » dans le champ de description. Puis cliquez sur « terminé ».

![Module4Chapter4step8aim](images/module4chapter4step8aim.PNG)

![Module4Chapter4step8bim](images/module4chapter4step8bim.PNG)

> Remarque : Si votre application est censée pour comprendre une langue différente de l’anglais, vous devez modifier la section « Culture » à la langue appropriée.

9. Cliquez sur « Build » situé dans le coin supérieur droit.

10. Sous ressources de l’application sur la gauche, sélectionnez « Intentions » puis cliquez sur « Créer nouveau intention » et nommez-le « PressButton. » 

![Module4Chapter4step10im](images/module4chapter4step10im.PNG)

> Remarque : il est important d’utiliser les noms des intentions et entités utilisées dans ce didacticiel, car l’application Lunarcom référencera les par nom.  Pour d’autres projets, les conventions d’affectation de noms peuvent être votre choix. 
>
> Remarque : vous devez maintenant avoir des 2 intentions - « PressButton » et « None ».

11. Sous ressources de l’application sur la gauche, sélectionnez « Entités » et cliquez sur « Créer une nouvelle entité » et nommez-le « Action » et conserver le Type d’entité en tant que « Simple ».

![Module4Chapter4step11im](images/module4chapter4step11im.PNG)

12. Cliquez de nouveau sur « Créer une nouvelle entité » et nommez-le « Cible » et conserver le Type d’entité en tant que « Simple » ainsi.

![Module4Chapter4step12im](images/module4chapter4step12im.PNG)

13. Sous ressources de l’application sur la gauche, sélectionnez « Intentions », puis cliquez sur votre intention de « PressButton » que vous avez créé à l’étape 10.

![Module4Chapter4step13im](images/module4chapter4step13im.PNG)

14. Cliquez sur la liste déroulante de « Afficher les options » à droite et sélectionnez « Afficher les valeurs d’entité ». 

    ![Module4Chapter4step14aim](images/module4chapter4step14aim.PNG)Cliquez sur le « entrer un exemple... » zone de texte. Ensuite, entrez les énoncés suivants : 

![Module4Chapter4step14bim](images/module4chapter4step14bim.PNG)

15. Cliquez sur la liste déroulante de « Afficher les options » à droite et sélectionnez « Afficher les noms d’entité ».

![Module4Chapter4step15im](images/module4chapter4step15im.PNG)

16. Vous assurer que chacun des 10 énoncés ont les étiquettes d’entité suivants aux emplacements suivants de 1.) cliquant sur les mots sont mal étiquetées et, dans le menu contextuel, en sélectionnant « Supprimer l’étiquette » et 2.) en cliquant sur les mots qui doivent être étiquetées et, dans le menu contextuel, sélectionnez l’étiquette appropriée.

![Module4Chapter4step16im](images/module4chapter4step16im.PNG)

17. Maintenant, pour publier le modèle, cliquez sur « Train » dans le coin supérieur droit. Ensuite, une fois le traitement terminé, cliquez sur « Test » dans le coin supérieur droit.

![Module4Chapter4step17im](images/module4chapter4step17im.PNG)

18. Entrez dans « Sélectionner le bouton de lancement » dans la zone de texte.

> Remarque : nous n’avez pas ajouté la « select » en tant qu’action dans un de nos énoncés - mais si vous cliquez sur « Inspecter », le modèle reconnu « sélectionner » comme une entité de l’action.
>
> ![Module4Chapter4noteim](images/module4chapter4noteim.PNG)

19. Maintenant, cliquez sur « Publier » dans le coin supérieur droit. Vérifiez que la liste déroulante intitulée « Production » et cliquez sur « Publier » dans la fenêtre contextuelle également. 

![Module4Chapter4step19im](images/module4chapter4step19im.PNG)

20. Une fois publié, une barre verte doit apparaître en haut de la page.  Cliquez sur la barre verte pour accéder à la page « Gérer ». 

![Module4Chapter4step20im](images/module4chapter4step20im.PNG)

21. Cliquez sur « Clés et points de terminaison » sous « Paramètres de l’Application » à gauche. Ensuite, définissez la liste déroulante « Publish To » en tant que « Production ». Définir le fuseau horaire à correspondent aux vôtres, puis cochez la case pour inclure toutes les notes intentions prédites. Enfin, cliquez sur « Ressource Assign. »

![Module4Chapter4step21im](images/module4chapter4step21im.PNG)

22. Sélectionnez le client à partir de la première liste déroulante et sélectionnez « Paiement à l’utilisation » dans la liste déroulante Nom de l’abonnement. Sous le nom de la ressource LUIS, choisissez la ressource que nous avons créé ci-dessus dans les étapes 1 à 5. Ensuite, cliquez sur « Ressource Assign. » 

![Module4Chapter4step22im](images/module4chapter4step22im.PNG)

> Remarque : veillez à copier et enregistrer l’URL de point de terminaison associé à la ressource que nous avons attribués simplement afin qu’il soit facilement accessible pour la section suivante.
>
> Remarque : pour le nom du client, placez votre entreprise ou le profil que vous avez créé pour cette application.

23. À présent, ouvrez la nouvelle application dans Unity et sélectionnez l’objet Lunarcom_Base dans la hiérarchie. Cliquez sur « Ajouter un composant » dans le panneau d’inspecteur, recherchez puis sélectionnez « LunarcomIntentRecognizer ».

![Module4Chapter4step23im](images/module4chapter4step23im.PNG)

24. Dans le champ Luis Endpoint de « LunarcomIntentRecognizer » dans le panneau d’inspecteur, entrez l’URL de point de terminaison que vous avez enregistré à l’étape 22. 

![Module4Chapter4step24im](images/module4chapter4step24im.PNG)

>  Remarque : Dans le composant « LunarcomOfflineRecognizer » dans le panneau d’inspecteur, assurez-vous que « désactiver » est activée pour « SimulateOfflineMode » dans le cas contraire, le programme de test ne fonctionnera pas. 

25. Appuyez sur le bouton de lecture dans l’éditeur Unity, puis cliquez sur le bouton de fusée pour démarrer la reconnaissance des intentions. Prononcez la phrase « sélectionner le bouton de fusée lancement ».

>  Remarque : L’application reconnu la fonction souhaitée et activé le bouton de fusée.
>
> ![Module4Chapter4step24im](images/module4chapter4note2im.PNG)

## <a name="congratulations"></a>Félicitations

Vous avez officiellement appris comment ajouter des commandes vocales à partir du programme de kit de développement logiciel de reconnaissance vocale ! Maintenant, votre programme puisse reconnaître les commandes vocales de toutes sortes de variantes. Tester et amuser un peu avec lui !

[Leçon suivante : Kit de développement logiciel de reconnaissance vocale leçon 5](placeholderlink)

