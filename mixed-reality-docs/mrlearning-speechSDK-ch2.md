## <a name="lesson-2"></a>Leçon 2

Dans la leçon 2, nous allons ajouter un mode hors connexion qui nous permettra d’effectuer la traduction de parole-texte locale lorsque nous ne pouvons pas vous connecter au service Azure et nous allons *simuler* un état déconnecté.

1. Sélectionnez l’objet « Lunarcom_Base » dans la hiérarchie et cliquez sur « Ajouter un composant » dans le panneau de l’inspecteur. Recherchez et sélectionnez « Reconnaissance hors connexion Lunarcom. »

![Module4Chapter2step1im](images/module4chapter2step1im.PNG)



2. Cliquez sur la liste déroulante dans la « LunarcomOfflineRecognizer » et sélectionnez « Activé ». Ce sera programme le projet d’agir comme si l’utilisateur n’a de connexion. 

![Module4Chapter2step1im](images/module4chapter2step2im.PNG)

3. Maintenant, appuyez sur play sur l’éditeur Unity et testez-le. Appuyez sur le microphone dans le coin inférieur gauche de la scène et commencez à parler. 

> Remarque : étant donné que nous sommes en mode hors connexion, la fonctionnalité d’éveil par le mot a été désactivée. Par conséquent, vous devrez physiquement cliquez sur le microphone, chaque fois que vous souhaitez que votre enregistrement vocal reconnu tandis que hors connexion. 

Voici un exemple de votre scène qui pourrait ressembler à :

![Module4Chapter2exampleim](images/module4chapter2exampleim.PNG)

## <a name="congratulations"></a>Félicitations

Le mode hors connexion a été activé ! Maintenant que vous soyez aucune forme d’internet, vous pouvez continuer à utiliser sur votre projet avec Speech SDK ! 

[Leçon suivante : SpeechSDK leçon 3](link placeholder)

