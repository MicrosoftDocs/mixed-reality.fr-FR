## <a name="lesson-2"></a><span data-ttu-id="3f090-101">Leçon 2</span><span class="sxs-lookup"><span data-stu-id="3f090-101">Lesson 2</span></span>

<span data-ttu-id="3f090-102">Dans la leçon 2, nous allons ajouter un mode hors connexion qui nous permettra d’effectuer la traduction de parole-texte locale lorsque nous ne pouvons pas vous connecter au service Azure et nous allons *simuler* un état déconnecté.</span><span class="sxs-lookup"><span data-stu-id="3f090-102">In Lesson 2, we will add an Offline mode that will allow us to perform local speech-to-text translation when we are unable to connect to the Azure service and we will *simulate* a disconnected state.</span></span>

1. <span data-ttu-id="3f090-103">Sélectionnez l’objet « Lunarcom_Base » dans la hiérarchie et cliquez sur « Ajouter un composant » dans le panneau de l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="3f090-103">Select the "Lunarcom_Base" object in the hierarchy and click “Add Component” in the inspector panel.</span></span> <span data-ttu-id="3f090-104">Recherchez et sélectionnez « Reconnaissance hors connexion Lunarcom. »</span><span class="sxs-lookup"><span data-stu-id="3f090-104">Search for and select the "Lunarcom Offline Recognition."</span></span>

![Module4Chapter2step1im](images/module4chapter2step1im.PNG)



2. <span data-ttu-id="3f090-106">Cliquez sur la liste déroulante dans la « LunarcomOfflineRecognizer » et sélectionnez « Activé ».</span><span class="sxs-lookup"><span data-stu-id="3f090-106">Click the dropdown in the “LunarcomOfflineRecognizer” and select “Enabled.”</span></span> <span data-ttu-id="3f090-107">Ce sera programme le projet d’agir comme si l’utilisateur n’a de connexion.</span><span class="sxs-lookup"><span data-stu-id="3f090-107">This will program the project to act like the user doesn't have connection.</span></span> 

![Module4Chapter2step1im](images/module4chapter2step2im.PNG)

3. <span data-ttu-id="3f090-109">Maintenant, appuyez sur play sur l’éditeur Unity et testez-le.</span><span class="sxs-lookup"><span data-stu-id="3f090-109">Now, press play on the Unity Editor and test it.</span></span> <span data-ttu-id="3f090-110">Appuyez sur le microphone dans le coin inférieur gauche de la scène et commencez à parler.</span><span class="sxs-lookup"><span data-stu-id="3f090-110">Press the microphone in the bottom left hand corner in the scene and begin speaking.</span></span> 

> <span data-ttu-id="3f090-111">Remarque : étant donné que nous sommes en mode hors connexion, la fonctionnalité d’éveil par le mot a été désactivée.</span><span class="sxs-lookup"><span data-stu-id="3f090-111">note: because we’re offline, the Wake Word functionality has been disabled.</span></span> <span data-ttu-id="3f090-112">Par conséquent, vous devrez physiquement cliquez sur le microphone, chaque fois que vous souhaitez que votre enregistrement vocal reconnu tandis que hors connexion.</span><span class="sxs-lookup"><span data-stu-id="3f090-112">So, you will have to physically click the microphone every time you wish to have your speech recognized while offline.</span></span> 

<span data-ttu-id="3f090-113">Voici un exemple de votre scène qui pourrait ressembler à :</span><span class="sxs-lookup"><span data-stu-id="3f090-113">Below is an example of what your scene could look like:</span></span>

![Module4Chapter2exampleim](images/module4chapter2exampleim.PNG)

## <a name="congratulations"></a><span data-ttu-id="3f090-115">Félicitations</span><span class="sxs-lookup"><span data-stu-id="3f090-115">Congratulations</span></span>

<span data-ttu-id="3f090-116">Le mode hors connexion a été activé !</span><span class="sxs-lookup"><span data-stu-id="3f090-116">The offline mode has been enabled!</span></span> <span data-ttu-id="3f090-117">Maintenant que vous soyez aucune forme d’internet, vous pouvez continuer à utiliser sur votre projet avec Speech SDK !</span><span class="sxs-lookup"><span data-stu-id="3f090-117">Now when you're away from any form of internet, you can still work on your project with Speech-SDK!</span></span> 

[<span data-ttu-id="3f090-118">Leçon suivante : SpeechSDK leçon 3</span><span class="sxs-lookup"><span data-stu-id="3f090-118">Next Lesson: SpeechSDK Lesson 3</span></span>](link placeholder)

