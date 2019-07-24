---
title: MR et Azure 311-Microsoft Graph
description: Suivez ce cours pour apprendre à tirer parti des Microsoft Graph et à vous connecter aux données qui pilotent la productivité, au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, Microsoft Graph, hololens, immersif, VR
ms.openlocfilehash: 04c72a7ef7724cfcc27867f7f003c171a6f7851f
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694525"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

# <a name="mr-and-azure-311---microsoft-graph"></a>MR et Azure 311-Microsoft Graph

Dans ce cours, vous allez apprendre à utiliser *Microsoft Graph* pour vous connecter à votre compte Microsoft à l’aide de l’authentification sécurisée dans une application de réalité mixte. Vous allez ensuite récupérer et afficher vos réunions planifiées dans l’interface de l’application.

![](images/AzureLabs-Lab311-00.png)

*Microsoft Graph* est un ensemble d’API conçues pour permettre l’accès à de nombreux services de Microsoft. Microsoft décrit Microsoft Graph comme une matrice de ressources connectées par des relations, ce qui signifie qu’elle permet à une application d’accéder à toutes sortes de données utilisateur connectées. Pour plus d’informations, consultez la [page Microsoft Graph](https://developer.microsoft.com/graph).

Le développement inclut la création d’une application dans laquelle l’utilisateur sera invité à pointer vers le regard, puis à appuyer sur une sphère, ce qui invite l’utilisateur à se connecter en toute sécurité à un compte Microsoft. Une fois connecté à son compte, l’utilisateur est en mesure de consulter la liste des réunions planifiées pour la journée.

Une fois ce cours terminé, vous disposerez d’une application HoloLens de réalité mixte, qui sera en mesure d’effectuer les opérations suivantes:

1.  À l’aide du geste TAP, appuyez sur un objet, qui invite l’utilisateur à se connecter à un compte Microsoft (en sortant de l’application pour se connecter, puis de nouveau dans l’application).
2.  Affichez la liste des réunions planifiées pour la journée. 

Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception. Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity. C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> MR et Azure 311: Microsoft Graph</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et. Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de la rédaction (juillet 2018). Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.

Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:

- Un PC de développement
- [Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé](install-the-tools.md#installation-checklist)
- [Le dernier Kit de développement logiciel Windows 10](install-the-tools.md#installation-checklist)
- [Unity 2017,4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- [Microsoft HoloLens](hololens-hardware-details.md) avec mode développeur activé
- Accès Internet pour l’installation d’Azure et la récupération des données de Microsoft Graph
- Un **compte Microsoft** valide (personnel ou professionnel/scolaire)
- Quelques réunions planifiées pour la journée en cours, à l’aide du même compte Microsoft

### <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).
2.  Configurez et testez votre HoloLens. Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup). 
3.  Il est judicieux d’effectuer un réglage de l’étalonnage et du capteur au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur). 

Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).

Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).

## <a name="chapter-1---create-your-app-in-the-application-registration-portal"></a>Chapitre 1-créer votre application dans le portail d’inscription des applications

Pour commencer, vous devrez créer et inscrire votre application dans le **portail d’inscription des applications**.

Dans ce chapitre, vous trouverez également la clé de service qui vous permettra d’effectuer des appels à *Microsoft Graph* pour accéder au contenu de votre compte.

1.  Accédez au [portail d’inscription des applications Microsoft](https://apps.dev.microsoft.com) et connectez-vous avec votre compte Microsoft. Une fois que vous êtes connecté, vous êtes redirigé vers le **portail d’inscription des applications**.

2.  Dans la section **mes applications** , cliquez sur le bouton **Ajouter une application**.

    ![](images/AzureLabs-Lab311-01.png)![](images/AzureLabs-Lab311-02.png)

    > [!IMPORTANT]
    > Le **portail d’inscription des applications** peut paraître différent, selon que vous avez déjà travaillé avec *Microsoft Graph*. Les captures d’écran ci-dessous affichent ces différentes versions.

3.  Ajoutez un nom pour votre application, puis cliquez sur **créer**.

    ![](images/AzureLabs-Lab311-03.png)

4.  Une fois l’application créée, vous êtes redirigé vers la page principale de l’application. Copiez l’ID de l' **application** et veillez à noter cette valeur dans un endroit sûr. vous l’utiliserez bientôt dans votre code.

    ![](images/AzureLabs-Lab311-04.png)

5.  Dans la section plateformes, assurez **-** vous que **application native** est affiché. Si ce *n’est pas* le cas, cliquez sur Ajouter une **plateforme** , puis sélectionnez **application native**.

    ![](images/AzureLabs-Lab311-05.png)

6.  Faites défiler la page vers le dessous et, dans la section intitulée **Microsoft Graph autorisations** , vous devez ajouter des autorisations supplémentaires pour l’application. Cliquez sur **Ajouter** en regard de **autorisations déléguées**.

    ![](images/AzureLabs-Lab311-06.png)

7.  Étant donné que vous souhaitez que votre application accède au calendrier de l’utilisateur, activez la case à cocher **calendriers. lire** , puis cliquez sur **OK**.

    ![](images/AzureLabs-Lab311-07.png)

8.  Faites défiler vers le bas et cliquez sur le bouton **Enregistrer** .

    ![](images/AzureLabs-Lab311-08.png)

9.  Votre enregistrement sera confirmé et vous pourrez vous déconnecter du **portail d’inscription des applications**.

## <a name="chapter-2---set-up-the-unity-project"></a>Chapitre 2-configurer le projet Unity

Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **nouveau**.

    ![](images/AzureLabs-Lab311-09.png)

2.  Vous devez fournir un nom de projet Unity. Insérez **MSGraphMR**. Assurez-vous que le modèle de projet est défini sur **3D**. Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés). Ensuite, cliquez sur **créer un projet**.

    ![](images/AzureLabs-Lab311-10.png)

3.  Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**. Accédez à **modifier** > les**Préférences** , puis à partir de la nouvelle fenêtre, accédez à **outils externes**. Remplacez l' **éditeur de script externe** par **Visual Studio 2017**. Fermez la fenêtre **Préférences** .

    ![](images/AzureLabs-Lab311-11.png)

4.  Accédez à **fichier** > **paramètres de build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le bouton **changer de plateforme** pour appliquer votre sélection.

    ![](images/AzureLabs-Lab311-12.png)

5.  Tout en conservant les**paramètres de génération**de **fichiers** > , assurez-vous que:

    1. L' **appareil cible** est défini sur **HoloLens**
    2. Le **type de build** est **D3D**
    3. Le **SDK** est configuré sur le **dernier installé**
    4. **Version de Visual Studio** définie sur le **dernier installé**
    5. La **génération et l’exécution** sont définies sur l' **ordinateur local**
    6. Enregistrez la scène et ajoutez-la à la Build.

        1. Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**. Une fenêtre d’enregistrement s’affiche.

            ![](images/AzureLabs-Lab311-13.png)

        2. Créez un dossier pour cela, ainsi que toute nouvelle scène. Sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez -le Scenes.

            ![](images/AzureLabs-Lab311-14.png)

        3. Ouvrez le dossier scenes nouvellement créé, puis dans le champ *nom de fichier*:, tapez **MR_ComputerVisionScene**, puis cliquez sur **Enregistrer**.

            ![](images/AzureLabs-Lab311-15.png)

            > [!IMPORTANT] 
            > Sachez que vous devez enregistrer vos scènes Unity dans le dossier *ressources* , car elles doivent être associées au projet Unity. La création du dossier scenes (et d’autres dossiers similaires) est un moyen classique de structurer un projet Unity.

    7.  Les paramètres restants, dans *paramètres de build*, doivent être laissés par défaut pour le moment.

6.  Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* . 

    ![](images/AzureLabs-Lab311-16.png)

7. Dans ce volet, quelques paramètres doivent être vérifiés:

    1. Sous l’onglet **autres paramètres** :

        1.  **Scripts** La **version du runtime** doit être **expérimentale** (.net 4,6 équivalent), qui déclenchera un redémarrage de l’éditeur.

        2. Le **backend de script** doit être **.net**

        3. Le **niveau de compatibilité** de l’API doit être **.net 4,6**

            ![](images/AzureLabs-Lab311-17.png)

    2.  Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:

        - **InternetClient**

            ![](images/AzureLabs-Lab311-18.png)

    3.  Plus bas dans le panneau, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.

        ![](images/AzureLabs-Lab311-19.png)

8.  De retour dans les *paramètres de build*, les *projets C# Unity* ne sont plus grisés. Cochez la case en regard de cette option.

9.  Fermez la fenêtre *paramètres de build* .

10.  Enregistrez votre scène et votre projet (**fichier** > **Save scenes/file** > **Save Project**).

## <a name="chapter-3---import-libraries-in-unity"></a>Chapitre 3-bibliothèques d’importation dans Unity

> [!IMPORTANT]
> Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce fichier [Azure-Mr-311. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20311%20-%20Microsoft%20Graph/Azure-MR-311.unitypackage), à l’importer dans votre projet en tant que [**package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis à passer au [Chapitre 5. ](#chapter-5---create-meetingsui-class).

Pour utiliser *Microsoft Graph* dans Unity, vous devez utiliser la dll **Microsoft. Identity. client** . Il est toutefois possible d’utiliser le kit de développement logiciel (SDK) Microsoft Graph, mais il nécessite l’ajout d’un package NuGet après la génération du projet Unity (c’est-à-dire la modification du projet après la génération). Il est considéré comme plus simple d’importer les dll requises directement dans Unity.

> [!NOTE]
> Il existe actuellement un problème connu dans Unity qui nécessite que les plug-ins soient reconfigurés après l’importation. Ces étapes (4-7 dans cette section) ne sont plus nécessaires une fois que le bogue a été résolu.

Pour importer *Microsoft Graph* dans votre propre projet, [Téléchargez le fichier MSGraph_LabPlugins. zip](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20311%20-%20Microsoft%20Graph/MSGraph_LabPlugins.unitypackage). Ce package a été créé avec les versions des bibliothèques qui ont été testées.

Si vous souhaitez en savoir plus sur l’ajout de dll personnalisées à votre projet Unity, [suivez ce lien](https://docs.unity3d.com/Manual/UsingDLL.html).

Pour importer le package:

1.  Ajoutez le package Unity à Unity à l’aide **de l'**  > option de menu package d'**importation de packages** > **personnalisés** . Sélectionnez le package que vous venez de télécharger.

2.  Dans la zone **importer le package Unity** qui s’affiche, vérifiez que tous les plug- **ins** sous (et y compris) sont sélectionnés.

    ![](images/AzureLabs-Lab311-20.png)

3.  Cliquez sur le bouton **Importer** pour ajouter les éléments à votre projet.

4.  Accédez au dossier **MSGraph** sous **plug-ins** dans le *panneau Projet* et sélectionnez le plug-in appelé **Microsoft. Identity. client**.

    ![](images/AzureLabs-Lab311-21.png)

5.  Une fois *le plug-in* sélectionné, assurez-vous que **toutes les plateformes** sont décochées, vérifiez que **WSAPlayer** est également désactivé, puis cliquez sur **appliquer**. Cela vous permet de vérifier que les fichiers sont correctement configurés.

    ![](images/AzureLabs-Lab311-22.png)

    > [!NOTE] 
    > Le marquage de ces plug-ins permet de les configurer pour qu’ils soient utilisés uniquement dans l’éditeur Unity. Il existe un ensemble différent de dll dans le dossier WSA qui sera utilisé une fois que le projet est exporté d’Unity en tant qu’application Windows universelle.

6.  Ensuite, vous devez ouvrir le dossier **WSA** , dans le dossier **MSGraph** . Vous verrez une copie du même fichier que celui que vous venez de configurer. Sélectionnez le fichier, puis dans l’inspecteur:

    -   Vérifiez que **toutes les plateformes** sont désactivées et que **seul** **WSAPlayer** est **activé**.

    -   Vérifiez que le **Kit de développement logiciel (SDK)** a la valeur **UWP**et que le **serveur principal de script** est défini sur le **point net**

    -   Vérifiez que l’option **ne pas traiter** est **cochée**.

        ![](images/AzureLabs-Lab311-23.png)

7.  Cliquez sur **Appliquer**.

## <a name="chapter-4---camera-setup"></a>Chapitre 4-Configuration de l’appareil photo

Au cours de ce chapitre, vous allez configurer la caméra principale de votre scène:

1.  Dans le *panneau hiérarchie*, sélectionnez l' **appareil photo principal**.

2.  Une fois sélectionné, vous pouvez voir tous les composants de la **caméra principale** dans le panneau *inspecteur* .

    1.  L' **objet Camera** doit être nommé **Camera main** (Notez l’orthographe!)

    2.  La balise  principale de l’appareil photo doit être définie sur **MainCamera** (Notez l’orthographe!)

    3.  Vérifiez que la **position** de la transformation est définie sur **0, 0,** 0

    4.  Définir des **indicateurs clairs** sur **couleur unie**

    5.  Définir la **couleur d’arrière-plan** du composant Camera sur **Black, alpha 0** **(code hexadécimal: #00000000)**

        ![](images/AzureLabs-Lab311-24.png)

3.  La dernière structure de l’objet dans le volet de la *hiérarchie* doit être similaire à celle illustrée dans l’image ci-dessous:

    ![](images/AzureLabs-Lab311-25.png)

## <a name="chapter-5---create-meetingsui-class"></a>Chapitre 5-créer une classe MeetingsUI

Le premier script que vous devez créer est **MeetingsUI**, qui est responsable de l’hébergement et du remplissage de l’interface utilisateur de l’application (message de bienvenue, instructions et détails des réunions).

Pour créer cette classe:

1.  Cliquez avec le bouton droit sur le dossier **ressources** dans le *panneau Projet*, puis sélectionnez **créer** > un**dossier**. Nommez le dossier **scripts**.

    ![](images/AzureLabs-Lab311-26.png)
    ![](images/AzureLabs-Lab311-27.png)

2.  Ouvrez le dossier **scripts** , puis, dans ce dossier, cliquez avec le bouton droit sur **créer**  >   **C# un script**. Nommez le script **MeetingsUI.**

    ![](images/AzureLabs-Lab311-28.png)

3.  Double-cliquez sur le nouveau script **MeetingsUI** pour l’ouvrir avec *Visual Studio*.

4.  Insérez les espaces de noms suivants:

    ```csharp
    using System;
    using UnityEngine;
    ```

5.  À l’intérieur de la classe, insérez les variables suivantes:

    ```csharp    
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static MeetingsUI Instance;

        /// <summary>
        /// The 3D text of the scene
        /// </summary>
        private TextMesh _meetingDisplayTextMesh;
    ```

6.  Remplacez ensuite la méthode **Start ()** et ajoutez une méthode **éveillé ()** . Ils sont appelés lorsque la classe est initialisée:

    ```csharp    
        /// <summary>
        /// Called on initialization
        /// </summary>
        void Awake()
        {
            Instance = this;
        }

        /// <summary>
        /// Called on initialization, after Awake
        /// </summary>
        void Start ()
        {
            // Creating the text mesh within the scene
            _meetingDisplayTextMesh = CreateMeetingsDisplay();
        }
    ```

7.  Ajoutez les méthodes responsables de la création de l' *interface utilisateur des réunions* et remplissez-la avec les réunions en cours lorsque vous y êtes invité:

    ```csharp    
        /// <summary>
        /// Set the welcome message for the user
        /// </summary>
        internal void WelcomeUser(string userName)
        {
            if(!string.IsNullOrEmpty(userName))
            {
                _meetingDisplayTextMesh.text = $"Welcome {userName}";
            }
            else 
            {
                _meetingDisplayTextMesh.text = "Welcome";
            }
        }

        /// <summary>
        /// Set up the parameters for the UI text
        /// </summary>
        /// <returns>Returns the 3D text in the scene</returns>
        private TextMesh CreateMeetingsDisplay()
        {
            GameObject display = new GameObject();
            display.transform.localScale = new Vector3(0.03f, 0.03f, 0.03f);
            display.transform.position = new Vector3(-3.5f, 2f, 9f);
            TextMesh textMesh = display.AddComponent<TextMesh>();
            textMesh.anchor = TextAnchor.MiddleLeft;
            textMesh.alignment = TextAlignment.Left;
            textMesh.fontSize = 80;
            textMesh.text = "Welcome! \nPlease gaze at the button" +
                "\nand use the Tap Gesture to display your meetings";

            return textMesh;
        }

        /// <summary>
        /// Adds a new Meeting in the UI by chaining the existing UI text
        /// </summary>
        internal void AddMeeting(string subject, DateTime dateTime, string location)
        {
            string newText = $"\n{_meetingDisplayTextMesh.text}\n\n Meeting,\nSubject: {subject},\nToday at {dateTime},\nLocation: {location}";

            _meetingDisplayTextMesh.text = newText;
        }
    ```

8. **Supprimez** la méthode **Update ()** et **Enregistrez vos modifications** dans Visual Studio avant de revenir à Unity. 

## <a name="chapter-6---create-the-graph-class"></a>Chapitre 6-créer la classe Graph

Le script suivant à créer est le script **Graph** . Ce script est chargé d’effectuer les appels pour authentifier l’utilisateur et de récupérer les réunions planifiées pour le jour actuel à partir du calendrier de l’utilisateur.

Pour créer cette classe:

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir.

2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer**  >   **C# un script**. Nommez le **graphique**de script.

3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio.

4.  Insérez les espaces de noms suivants:

    ```csharp
    using System.Collections.Generic;
    using UnityEngine;
    using Microsoft.Identity.Client;
    using System;
    using System.Threading.Tasks;
    
    #if !UNITY_EDITOR && UNITY_WSA
    using System.Net.Http;
    using System.Net.Http.Headers;
    using Windows.Storage;
    #endif
    ```

    > [!IMPORTANT]
    > Vous remarquerez que certaines parties du code de ce script sont encapsulées autour des [directives](https://docs.unity3d.com/Manual/PlatformDependentCompilation.html)de précompilation. cela permet d’éviter les problèmes liés aux bibliothèques lors de la génération de la solution Visual Studio.

5.  Supprimez les méthodes **Start ()** et **Update ()** , car elles ne seront pas utilisées.

6.  En dehors de la classe **Graph** , insérez les objets suivants, qui sont nécessaires pour désérialiser l’objet JSON représentant les réunions planifiées quotidiennement:

    ```csharp
    /// <summary>
    /// The object hosting the scheduled meetings
    /// </summary>
    [Serializable]
    public class Rootobject
    {
        public List<Value> value;
    }

    [Serializable]
    public class Value
    {
        public string subject { get; set; }
        public StartTime start { get; set; }
        public Location location { get; set; }
    }

    [Serializable]
    public class StartTime
    {
        public string dateTime;

        private DateTime? _startDateTime;
        public DateTime StartDateTime
        {
            get
            {
                if (_startDateTime != null)
                    return _startDateTime.Value;
                DateTime dt;
                DateTime.TryParse(dateTime, out dt);
                _startDateTime = dt;
                return _startDateTime.Value;
            }
        }
    }

    [Serializable]
    public class Location
    {
        public string displayName { get; set; }
    }
    ```

7.  À l’intérieur de la classe **Graph** , ajoutez les variables suivantes:

    ```csharp    
        /// <summary>
        /// Insert your Application Id here
        /// </summary>
        private string _appId = "-- Insert your Application Id here --";

        /// <summary>
        /// Application scopes, determine Microsoft Graph accessibility level to user account
        /// </summary>
        private IEnumerable<string> _scopes = new List<string>() { "User.Read", "Calendars.Read" };

        /// <summary>
        /// Microsoft Graph API, user reference
        /// </summary>
        private PublicClientApplication _client;

        /// <summary>
        /// Microsoft Graph API, authentication
        /// </summary>
        private AuthenticationResult _authResult;

    ```

    > [!NOTE]
    > Modifiez la valeur **AppID** pour qu’elle soit l' **ID d’application** que vous avez noté au  **[Chapitre 1](#chapter-1---create-your-app-in-the-application-registration-portal), étape 4**. Cette valeur doit être identique à celle affichée dans le **portail d’inscription des applications,** dans la page d’inscription de votre application.

8.  Dans la classe **Graph** , ajoutez les méthodes **SignInAsync ()** et **AquireTokenAsync ()** , qui invitent l’utilisateur à insérer les informations d’identification de connexion.

    ```csharp
        /// <summary>
        /// Begin the Sign In process using Microsoft Graph Library
        /// </summary>
        internal async void SignInAsync()
        {
    #if !UNITY_EDITOR && UNITY_WSA
            // Set up Grap user settings, determine if needs auth
            ApplicationDataContainer localSettings = ApplicationData.Current.LocalSettings;
            string userId = localSettings.Values["UserId"] as string;
            _client = new PublicClientApplication(_appId);

            // Attempt authentication
            _authResult = await AcquireTokenAsync(_client, _scopes, userId);

            // If authentication is successfull, retrieve the meetings
            if (!string.IsNullOrEmpty(_authResult.AccessToken))
            {
                // Once Auth as been completed, find the meetings for the day
                await ListMeetingsAsync(_authResult.AccessToken);
            }
    #endif
        }

        /// <summary>
        /// Attempt to retrieve the Access Token by either retrieving
        /// previously stored credentials or by prompting user to Login
        /// </summary>
        private async Task<AuthenticationResult> AcquireTokenAsync(
            IPublicClientApplication app, IEnumerable<string> scopes, string userId)
        {
            IUser user = !string.IsNullOrEmpty(userId) ? app.GetUser(userId) : null;
            string userName = user != null ? user.Name : "null";

            // Once the User name is found, display it as a welcome message
            MeetingsUI.Instance.WelcomeUser(userName);

            // Attempt to Log In the user with a pre-stored token. Only happens
            // in case the user Logged In with this app on this device previously
            try
            {
                _authResult = await app.AcquireTokenSilentAsync(scopes, user);
            }
            catch (MsalUiRequiredException)
            {
                // Pre-stored token not found, prompt the user to log-in 
                try
                {
                    _authResult = await app.AcquireTokenAsync(scopes);
                }
                catch (MsalException msalex)
                {
                    Debug.Log($"Error Acquiring Token: {msalex.Message}");
                    return _authResult;
                }
            }
            
            MeetingsUI.Instance.WelcomeUser(_authResult.User.Name);

    #if !UNITY_EDITOR && UNITY_WSA
            ApplicationData.Current.LocalSettings.Values["UserId"] = 
            _authResult.User.Identifier;
    #endif
            return _authResult;
        }
    ```

9.  Ajoutez les deux méthodes suivantes:

    1.  **BuildTodayCalendarEndpoint ()** , qui génère l’URI spécifiant le jour et l’intervalle de temps pendant lesquels les réunions planifiées sont récupérées.

    2.  **ListMeetingsAsync ()** , qui demande les réunions planifiées à partir de *Microsoft Graph*.

    ```csharp
        /// <summary>
        /// Build the endpoint to retrieve the meetings for the current day.
        /// </summary>
        /// <returns>Returns the Calendar Endpoint</returns>
        public string BuildTodayCalendarEndpoint()
        {
            DateTime startOfTheDay = DateTime.Today.AddDays(0);
            DateTime endOfTheDay = DateTime.Today.AddDays(1);
            DateTime startOfTheDayUTC = startOfTheDay.ToUniversalTime();
            DateTime endOfTheDayUTC = endOfTheDay.ToUniversalTime();

            string todayDate = startOfTheDayUTC.ToString("o");
            string tomorrowDate = endOfTheDayUTC.ToString("o");
            string todayCalendarEndpoint = string.Format(
                "https://graph.microsoft.com/v1.0/me/calendarview?startdatetime={0}&enddatetime={1}",
                todayDate,
                tomorrowDate);

            return todayCalendarEndpoint;
        }

        /// <summary>
        /// Request all the scheduled meetings for the current day.
        /// </summary>
        private async Task ListMeetingsAsync(string accessToken)
        {
    #if !UNITY_EDITOR && UNITY_WSA
            var http = new HttpClient();

            http.DefaultRequestHeaders.Authorization = 
            new AuthenticationHeaderValue("Bearer", accessToken);
            var response = await http.GetAsync(BuildTodayCalendarEndpoint());

            var jsonResponse = await response.Content.ReadAsStringAsync();

            Rootobject rootObject = new Rootobject();
            try
            {
                // Parse the JSON response.
                rootObject = JsonUtility.FromJson<Rootobject>(jsonResponse);

                // Sort the meeting list by starting time.
                rootObject.value.Sort((x, y) => DateTime.Compare(x.start.StartDateTime, y.start.StartDateTime));

                // Populate the UI with the meetings.
                for (int i = 0; i < rootObject.value.Count; i++)
                {
                    MeetingsUI.Instance.AddMeeting(rootObject.value[i].subject,
                                                rootObject.value[i].start.StartDateTime.ToLocalTime(),
                                                rootObject.value[i].location.displayName);
                }
            }
            catch (Exception ex)
            {
                Debug.Log($"Error = {ex.Message}");
                return;
            }
    #endif
        }
    ```

10. Vous avez maintenant terminé le script **Graph** . **Enregistrez vos modifications** dans Visual Studio avant de revenir à Unity.

## <a name="chapter-7---create-the-gazeinput-script"></a>Chapitre 7-créer le script GazeInput

Vous allez maintenant créer le **GazeInput**. Cette classe gère et effectue le suivi du point de regard de l’utilisateur à l’aide d’un **Raycast** provenant de la **caméra principale**, en projetant vers l’avant.

Pour créer le script:

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir.

2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer**  >   **C# un script**. Nommez le script **GazeInput**.

3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio.

4.  Modifier le code des espaces de noms pour correspondre à celui ci-dessous, ainsi que l’ajout de la ' **\[System.Serializable\]** ' balise ci-dessus votre **GazeInput** classe, afin qu’il puisse être sérialisé :

    ```csharp
    using UnityEngine;

    /// <summary>
    /// Class responsible for the User's Gaze interactions
    /// </summary>
    [System.Serializable]
    public class GazeInput : MonoBehaviour
    {
    ```

5.  À l’intérieur de la classe **GazeInput** , ajoutez les variables suivantes:

    ```csharp    
        [Tooltip("Used to compare whether an object is to be interacted with.")]
        internal string InteractibleTag = "SignInButton";

        /// <summary>
        /// Length of the gaze
        /// </summary>
        internal float GazeMaxDistance = 300;

        /// <summary>
        /// Object currently gazed
        /// </summary>
        internal GameObject FocusedObject { get; private set; }

        internal GameObject oldFocusedObject { get; private set; }

        internal RaycastHit HitInfo { get; private set; }

        /// <summary>
        /// Cursor object visible in the scene
        /// </summary>
        internal GameObject Cursor { get; private set; }

        internal bool Hit { get; private set; }

        internal Vector3 Position { get; private set; }

        internal Vector3 Normal { get; private set; }

        private Vector3 _gazeOrigin;

        private Vector3 _gazeDirection;
    ```

6.  Ajoutez la méthode **CreateCursor ()** pour créer le curseur HoloLens dans la scène, puis appelez la méthode à partir de la méthode **Start ()** :

    ```csharp    
        /// <summary>
        /// Start method used upon initialisation.
        /// </summary>
        internal virtual void Start()
        {
            FocusedObject = null;
            Cursor = CreateCursor();
        }

        /// <summary>
        /// Method to create a cursor object.
        /// </summary>
        internal GameObject CreateCursor()
        {
            GameObject newCursor = GameObject.CreatePrimitive(PrimitiveType.Sphere);
            newCursor.SetActive(false);
            // Remove the collider, so it doesn't block raycast.
            Destroy(newCursor.GetComponent<SphereCollider>());
            newCursor.transform.localScale = new Vector3(0.05f, 0.05f, 0.05f);
            Material mat = new Material(Shader.Find("Diffuse"));
            newCursor.GetComponent<MeshRenderer>().material = mat;
            mat.color = Color.HSVToRGB(0.0223f, 0.7922f, 1.000f);
            newCursor.SetActive(true);

            return newCursor;
        }
    ```

7.  Les méthodes suivantes activent le point de Raycast de regard et assurent le suivi des objets ayant le focus.

    ```csharp
    /// <summary>
    /// Called every frame
    /// </summary>
    internal virtual void Update()
    {
        _gazeOrigin = Camera.main.transform.position;

        _gazeDirection = Camera.main.transform.forward;

        UpdateRaycast();
    }
    /// <summary>
    /// Reset the old focused object, stop the gaze timer, and send data if it
    /// is greater than one.
    /// </summary>
    private void ResetFocusedObject()
    {
        // Ensure the old focused object is not null.
        if (oldFocusedObject != null)
        {
            if (oldFocusedObject.CompareTag(InteractibleTag))
            {
                // Provide the 'Gaze Exited' event.
                oldFocusedObject.SendMessage("OnGazeExited", SendMessageOptions.DontRequireReceiver);
            }
        }
    }
    ```

    ```csharp
        private void UpdateRaycast()
        {
            // Set the old focused gameobject.
            oldFocusedObject = FocusedObject;
            RaycastHit hitInfo;

            // Initialise Raycasting.
            Hit = Physics.Raycast(_gazeOrigin,
                _gazeDirection,
                out hitInfo,
                GazeMaxDistance);
                HitInfo = hitInfo;

            // Check whether raycast has hit.
            if (Hit == true)
            {
                Position = hitInfo.point;
                Normal = hitInfo.normal;

                // Check whether the hit has a collider.
                if (hitInfo.collider != null)
                {
                    // Set the focused object with what the user just looked at.
                    FocusedObject = hitInfo.collider.gameObject;
                }
                else
                {
                    // Object looked on is not valid, set focused gameobject to null.
                    FocusedObject = null;
                }
            }
            else
            {
                // No object looked upon, set focused gameobject to null.
                FocusedObject = null;

                // Provide default position for cursor.
                Position = _gazeOrigin + (_gazeDirection * GazeMaxDistance);

                // Provide a default normal.
                Normal = _gazeDirection;
            }

            // Lerp the cursor to the given position, which helps to stabilize the gaze.
            Cursor.transform.position = Vector3.Lerp(Cursor.transform.position, Position, 0.6f);

            // Check whether the previous focused object is this same. If so, reset the focused object.
            if (FocusedObject != oldFocusedObject)
            {
                ResetFocusedObject();
                if (FocusedObject != null)
                {
                    if (FocusedObject.CompareTag(InteractibleTag))
                    {
                        // Provide the 'Gaze Entered' event.
                        FocusedObject.SendMessage("OnGazeEntered", 
                            SendMessageOptions.DontRequireReceiver);
                    }
                }
            }
        }
    ```

8.  **Enregistrez vos modifications** dans Visual Studio avant de revenir à Unity.

## <a name="chapter-8---create-the-interactions-class"></a>Chapitre 8-créer la classe interactions

Vous devez maintenant créer le script **interactions** , qui est chargé des opérations suivantes:

-   Gestion de l’interaction du **robinet** et du point d’interconnexion de l' **appareil photo**, qui permet à l’utilisateur d’interagir avec le «bouton» du journal dans la scène.

-   Création de l’objet de connexion «Button» dans la scène pour l’utilisateur avec lequel interagir.

Pour créer le script:

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir.

2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer**  >   **C# un script**. Nommez les **interactions**de script.

3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio.

4.  Insérez les espaces de noms suivants:

    ```csharp
    using UnityEngine;
    using UnityEngine.XR.WSA.Input;
    ```

5.  Remplacez l’héritage de la classe **interaction** par *monocomportement* par **GazeInput**.

    ~~Interactions de classes publiques: MonoBehaviour~~

    ```csharp
    public class Interactions : GazeInput
    ```

6.  À l’intérieur de la classe d' **interaction** , insérez la variable suivante:

    ```csharp
        /// <summary>
        /// Allows input recognition with the HoloLens
        /// </summary>
        private GestureRecognizer _gestureRecognizer;
    ```

7.  Remplacez la méthode **Start** . Notez qu’il s’agit d’une méthode override, qui appelle la méthode de la classe de pointage «base». **Start ()** est appelé lors de l’initialisation de la classe, de l’inscription à la reconnaissance d’entrée et de la création du *bouton* de connexion dans la scène:

    ```csharp    
        /// <summary>
        /// Called on initialization, after Awake
        /// </summary>
        internal override void Start()
        {
            base.Start();

            // Register the application to recognize HoloLens user inputs
            _gestureRecognizer = new GestureRecognizer();
            _gestureRecognizer.SetRecognizableGestures(GestureSettings.Tap);
            _gestureRecognizer.Tapped += GestureRecognizer_Tapped;
            _gestureRecognizer.StartCapturingGestures();

            // Add the Graph script to this object
            gameObject.AddComponent<MeetingsUI>();
            CreateSignInButton();
        }
    ```

8.  Ajoutez la méthode **CreateSignInButton ()** , qui instancie le *bouton* de connexion dans la scène et définit ses propriétés:

    ```csharp    
        /// <summary>
        /// Create the sign in button object in the scene
        /// and sets its properties
        /// </summary>
        void CreateSignInButton()
        {
            GameObject signInButton = GameObject.CreatePrimitive(PrimitiveType.Sphere);

            Material mat = new Material(Shader.Find("Diffuse"));
            signInButton.GetComponent<Renderer>().material = mat;
            mat.color = Color.blue;

            signInButton.transform.position = new Vector3(3.5f, 2f, 9f);
            signInButton.tag = "SignInButton";
            signInButton.AddComponent<Graph>();
        }
    ```

9.  Ajoutez la méthode **GestureRecognizer_Tapped ()** , qui répond à l’événement *Tap* User.

    ```csharp   
        /// <summary>
        /// Detects the User Tap Input
        /// </summary>
        private void GestureRecognizer_Tapped(TappedEventArgs obj)
        {
            if(base.FocusedObject != null)
            {
                Debug.Log($"TAP on {base.FocusedObject.name}");
                base.FocusedObject.SendMessage("SignInAsync", SendMessageOptions.RequireReceiver);
            }
        }
    ```

10. **Supprimez** la méthode **Update ()** , puis **Enregistrez vos modifications** dans Visual Studio avant de revenir à Unity.

## <a name="chapter-9---set-up-the-script-references"></a>Chapitre 9-configurer les références de script

Dans ce chapitre, vous devez placer le script **interactions** sur l' **appareil photo principal**. Ce script gère alors le placement des autres scripts là où ils doivent être.

-  Dans le dossier **scripts** du *panneau Projet*, faites glisser les **interactions** de script vers l’objet **caméra principale** , comme illustré ci-dessous.

    ![](images/AzureLabs-Lab311-29.png)

## <a name="chapter-10---setting-up-the-tag"></a>Chapitre 10-configuration de la balise

Le code qui gère le point de regard utilise la balise **SignInButton** pour identifier l’objet avec lequel l’utilisateur interagit pour se connecter à *Microsoft Graph*.

Pour créer la balise:

1.  Dans l’éditeur Unity, cliquez sur la **caméra principale** dans le *panneau hiérarchie*.

2.  Dans le *volet* de l’inspecteur, cliquez sur la balise **MainCamera**  pour ouvrir une liste déroulante. Cliquez sur **Ajouter une étiquette...**

    ![](images/AzureLabs-Lab311-30.png)

3.  Cliquez sur le **+** bouton.

    ![](images/AzureLabs-Lab311-31.png)

4.  Écrivez le nom de la balise en tant que **SignInButton** , puis cliquez sur Enregistrer.

    ![](images/AzureLabs-Lab311-32.png)

## <a name="chapter-11---build-the-unity-project-to-uwp"></a>Chapitre 11-créer le projet Unity dans UWP

Tout ce qui est nécessaire pour la section Unity de ce projet est maintenant terminé. il est donc temps de la générer à partir d’Unity.

1.  Accédez à *les paramètres de génération* (**fichier*>*Build paramètres**).

    ![](images/AzureLabs-Lab311-33.png)

2.  Si ce n’est pas déjà fait, cochez les **projets Unity C\#** .

3.  Cliquez sur **Build**. Unity lance une fenêtre de l' **Explorateur de fichiers** , dans laquelle vous devez créer, puis sélectionner un dossier dans lequel générer l’application. Créez ce dossier maintenant, puis nommez-le **application**. Ensuite, avec le dossier d' **application** sélectionné, cliquez sur **Sélectionner un dossier**.

4.  Unity commence à générer votre projet dans le dossier de l' **application** .

5.  Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).

## <a name="chapter-12---deploy-to-hololens"></a>Chapitre 12-déployer dans HoloLens

Pour effectuer un déploiement sur HoloLens:

1.  Vous aurez besoin de l’adresse IP de votre HoloLens (pour le déploiement à distance) et vérifiez que votre HoloLens est en **mode développeur.** Pour ce faire :

    1.  Tout en portant votre HoloLens, ouvrez les **paramètres**.

    2.  Accéder au **réseau &**  > **Options avancées** **de Wi-Fi** > Internet

    3.  Notez l’adresse **IPv4** .

    4.  Ensuite, revenez aux **paramètres**, puis pour **mettre à jour & sécurité** > **pour les développeurs**

    5.  Définissez **le mode développeur sur**.

2.  Accédez à votre nouvelle build Unity (le dossier de l' **application** ) et ouvrez le fichier solution avec **Visual Studio**.

3.  Dans la **configuration** de la solution, sélectionnez Déboguer.

4.  Dans la **plateforme**de la solution, sélectionnez **x86, ordinateur distant**. Vous serez invité à insérer l' **adresse IP** d’un périphérique distant (le HoloLens, dans ce cas, que vous avez noté).

    ![](images/AzureLabs-Lab311-34.png)

5.  Accédez au menu **générer** , puis cliquez sur **déployer la solution** pour chargement l’application à votre HoloLens.

6.  Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prête à être lancée.

## <a name="your-microsoft-graph-hololens-application"></a>Votre application Microsoft Graph HoloLens

Félicitations, vous avez créé une application de réalité mixte qui tire parti de la Microsoft Graph pour lire et afficher les données de calendrier utilisateur.

![](images/AzureLabs-Lab311-00.png)

## <a name="bonus-exercises"></a>Exercices bonus

### <a name="exercise-1"></a>Exercice 1

Utiliser Microsoft Graph pour afficher d’autres informations sur l’utilisateur

-   Adresse de messagerie/numéro de téléphone/de profil utilisateur

### <a name="exercise-1"></a>Exercice 1

Implémentez le contrôle vocal pour naviguer dans l’interface utilisateur Microsoft Graph.
