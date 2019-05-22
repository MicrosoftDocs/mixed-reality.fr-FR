---
title: MR et Azure 311 - Microsoft Graph
description: Terminer ce cours pour apprendre à tirer parti de Microsoft Graph et se connecter aux données qui favorisent la productivité, au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, graph de microsoft, hololens, immersives, vr
ms.openlocfilehash: 98fe2c872f332a21fff3af6751ae555968073a24
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593290"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

# <a name="mr-and-azure-311---microsoft-graph"></a>MR et Azure 311 - Microsoft Graph

Dans ce cours, vous allez apprendre à utiliser *Microsoft Graph* pour vous connecter à votre compte Microsoft à l’aide de l’authentification sécurisée dans une application de réalité mixte. Vous serez ensuite récupérer et afficher vos réunions planifiées dans l’interface de l’application.

![](images/AzureLabs-Lab311-00.png)

*Microsoft Graph* est un ensemble d’API conçues pour permettre l’accès à de nombreux services de Microsoft. Microsoft décrit Microsoft Graph comme étant une matrice des ressources connectées par des relations, ce qui signifie qu’il permet à une application à accéder à toutes sortes de données de l’utilisateur connecté. Pour plus d’informations, visitez le [page de Microsoft Graph](https://developer.microsoft.com/graph).

Développement incluent la création d’une application où l’utilisateur sera invité à fixez du regard, puis appuyez sur une sphère, qui invitera l’utilisateur pour vous connecter en toute sécurité à un compte Microsoft. Une fois connecté à son compte, l’utilisateur sera en mesure de voir une liste de réunions planifiées pour la journée.

Avoir terminé ce cours, vous aurez une réalité mixte application HoloLens, qui sera en mesure d’effectuer les opérations suivantes :

1.  À l’aide de l’action d’appuyer, appuyez sur un objet qui invitera l’utilisateur pour vous connecter à un Account Microsoft (déplacement hors de l’application pour vous connecter et inversement à l’application).
2.  Afficher la liste des réunions planifiées pour la journée. 

Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception. Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity. Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> MR et Azure 311 : Microsoft Graph</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#. Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (juillet 2018). Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous.

Nous recommandons le matériel et logiciel pour ce cours suivants :

- Un PC de développement
- [Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé](install-the-tools.md#installation-checklist)
- [Le SDK Windows 10 dernières](install-the-tools.md#installation-checklist)
- [Unity 2017.4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé
- Accès à Internet pour le programme d’installation Azure et l’extraction de données de Microsoft Graph
- Valide **Account Microsoft** (personnel ou Professionnel ou scolaire)
- Quelques réunions planifiées pour le jour actuel, à l’aide de la même Account Microsoft

### <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).
2.  Configurer et tester votre HoloLens. Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup). 
3.  Il est judicieux d’effectuer l’étalonnage et le réglage de capteur lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur). 

Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).

Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).

## <a name="chapter-1---create-your-app-in-the-application-registration-portal"></a>Chapitre 1 - créer votre application dans le portail d’inscription des applications

Pour commencer, vous devez créer et inscrire votre application dans le **portail d’inscription des applications**.

Dans ce chapitre, vous trouverez également la clé de Service qui vous permet d’effectuer des appels vers *Microsoft Graph* pour accéder au contenu de votre compte.

1.  Accédez à la [portail d’inscription de Microsoft Application](https://apps.dev.microsoft.com) et connectez-vous avec votre Account de Microsoft. Une fois que vous êtes connecté, vous êtes redirigé vers la **portail d’inscription des applications**.

2.  Dans le **mes applications** section, cliquez sur le bouton **ajouter une application**.

    ![](images/AzureLabs-Lab311-01.png)![](images/AzureLabs-Lab311-02.png)

    > [!IMPORTANT]
    > Le **portail d’inscription des applications** peut être différente, selon que vous avez travaillé précédemment avec *Microsoft Graph*. Le ci-dessous des captures d’écran afficher ces différentes versions.

3.  Ajouter un nom pour votre application et le clic **créer**.

    ![](images/AzureLabs-Lab311-03.png)

4.  Une fois que l’application a été créée, vous serez redirigé vers la page principale d’application. Copie le **Id d’Application** et veillez à noter cette valeur dans un endroit sûr, vous l’utiliserez bientôt dans votre code.

    ![](images/AzureLabs-Lab311-04.png)

5.  Dans le **plateformes** section, assurez-vous que **Application Native** s’affiche. Si *pas* cliquez sur **ajouter une plateforme** et sélectionnez **Application Native**.

    ![](images/AzureLabs-Lab311-05.png)

6.  Défiler vers le bas dans la même page et dans la section intitulée **autorisations Microsoft Graph** vous devez ajouter des autorisations supplémentaires pour l’application. Cliquez sur **ajouter** regard **autorisations déléguées**.

    ![](images/AzureLabs-Lab311-06.png)

7.  Dans la mesure où vous souhaitez que votre application à accéder au calendrier de l’utilisateur, cochez la case appelée **Calendars.Read** et cliquez sur **OK**.

    ![](images/AzureLabs-Lab311-07.png)

8.  Faites défiler vers le bas et cliquez sur le **enregistrer** bouton.

    ![](images/AzureLabs-Lab311-08.png)

9.  Votre enregistrement confirmé, vous pouvez déconnecter à partir de la **portail d’inscription des applications**.

## <a name="chapter-2---set-up-the-unity-project"></a>Chapitre 2 : configurer le projet Unity

Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **New**.

    ![](images/AzureLabs-Lab311-09.png)

2.  Vous devez fournir un nom de projet Unity. Insérer **MSGraphMR**. Assurez-vous que le modèle de projet est défini sur **3D**. Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![](images/AzureLabs-Lab311-10.png)

3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Accédez à **Modifier > Préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

    ![](images/AzureLabs-Lab311-11.png)

4.  Accédez à **fichier > Paramètres de Build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le **plateforme de commutation** bouton pour appliquer votre sélection.

    ![](images/AzureLabs-Lab311-12.png)

5.  Lorsque vous êtes toujours dans **fichier > Paramètres de Build**, assurez-vous que :

    1. **Équipement cible** a la valeur **HoloLens**
    2. **Type de build** a la valeur **D3D**
    3. **Kit de développement logiciel** a la valeur **dernière installé**
    4. **Version de Visual Studio** a la valeur **dernière installé**
    5. **Générez et exécutez** est défini sur **ordinateur Local**
    6. Enregistrer la scène et l’ajouter à la build.

        1. Cela en sélectionnant **ajouter un arrière-plan Open**. Une fenêtre d’enregistrement s’affiche.

            ![](images/AzureLabs-Lab311-13.png)

        2. Pour cela et n’importe quel futur, votre scène, créez un dossier. Sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.

            ![](images/AzureLabs-Lab311-14.png)

        3. Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier*: champ de texte, tapez **MR_ComputerVisionScene**, puis cliquez sur **enregistrer** .

            ![](images/AzureLabs-Lab311-15.png)

            > [!IMPORTANT] 
            > N’oubliez pas, vous devez enregistrer vos séquences de Unity dans le *actifs* dossier, car ils doivent être associées au projet Unity. Création du dossier de scènes (et autres dossiers similaire) est un moyen classique de structurer un projet Unity.

    7.  Les autres paramètres, dans *paramètres de Build*, doit être conservé comme valeur par défaut pour l’instant.

6.  Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve. 

    ![](images/AzureLabs-Lab311-16.png)

7. Dans ce panneau, quelques paramètres doivent être vérifiées :

    1. Dans le **autres paramètres** onglet :

        1.  **Écriture de scripts** **Version du Runtime** doit être **expérimental** (.NET 4.6 équivalent), ce qui déclenchera une nécessité de redémarrer l’éditeur.

        2. **Script principal** doit être **.NET**

        3. **Niveau de compatibilité d’API** doit être **.NET 4.6**

            ![](images/AzureLabs-Lab311-17.png)

    2.  Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :

        - **InternetClient**

            ![](images/AzureLabs-Lab311-18.png)

    3.  Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), vérifiez **virtuel pris en charge de réalité**, assurez-vous que le **Windows Mixed Reality Kit de développement logiciel** est ajouté.

        ![](images/AzureLabs-Lab311-19.png)

8.  Dans *paramètres de Build*, *Unity C# projets* est n’est plus grisée ; case à cocher en regard de cela.

9.  Fermer le *paramètres de Build* fenêtre.

10.  Enregistrer votre projet et la scène (**fichier > Enregistrer les scènes / fichier > Enregistrer le projet**).

## <a name="chapter-3---import-libraries-in-unity"></a>Chapitre 3 - bibliothèques d’importation dans Unity

> [!IMPORTANT]
> Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [Azure-MR-311.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20311%20-%20Microsoft%20Graph/Azure-MR-311.unitypackage), importez-le dans votre projet en tant qu’un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 5](#chapter-5---create-meetingsui-class).

Pour utiliser *Microsoft Graph* dans Unity, vous devez vous utiliser le **Microsoft.Identity.Client** DLL. Il est possible d’utiliser le kit SDK Microsoft Graph, toutefois, il nécessite l’ajout d’un package NuGet une fois que vous générez le projet Unity (c'est-à-dire modification après la génération du projet). Il est considéré comme plus simple d’importer les DLL requises directement dans Unity.

> [!NOTE]
> Il est actuellement un problème connu dans Unity qui nécessite des plug-ins à être reconfiguré après l’importation. Ces étapes (4-7 de cette section) ne sera plus nécessaires une fois que le bogue a été résolu.

Pour importer *Microsoft Graph* dans votre propre projet, [télécharger le fichier MSGraph_LabPlugins.zip](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20311%20-%20Microsoft%20Graph/MSGraph_LabPlugins.unitypackage). Ce package a été créé avec les versions des bibliothèques qui ont été testés.

Si vous le souhaitez en savoir plus sur l’ajout de DLL personnalisées à votre projet Unity, [, suivez ce lien](https://docs.unity3d.com/Manual/UsingDLL.html).

Pour importer le package :

1.  Ajouter le Package Unity pour Unity à l’aide de la **actifs* > *importer un Package* > *Package personnalisé** option de menu. Sélectionnez le package que vous venez de télécharger.

2.  Dans le **importer un Package Unity** emballer qui apparaît, vérifiez tous les éléments sous (y compris) **plug-ins** est sélectionné.

    ![](images/AzureLabs-Lab311-20.png)

3.  Cliquez sur le **importation** pour ajouter les éléments à votre projet.

4.  Accédez à la **MSGraph** dossier sous **plug-ins** dans le *panneau projet* et sélectionnez le plug-in appelé **Microsoft.Identity.Client**.

    ![](images/AzureLabs-Lab311-21.png)

5.  Avec le *plug-in* sélectionnée, vérifiez que **plateforme Any** est désactivée, puis vérifiez que **WSAPlayer** est également désactivée, puis cliquez sur **appliquer**. Il s’agit juste pour confirmer que les fichiers sont correctement configurés.

    ![](images/AzureLabs-Lab311-22.png)

    > [!NOTE] 
    > Marquage de ces plug-ins les configure uniquement à être utilisé dans l’éditeur Unity. Il existe un autre ensemble de DLL dans le dossier WSA qui sera utilisée une fois que le projet est exporté à partir d’Unity comme une Application Windows universelle.

6.  Ensuite, vous devez ouvrir le **WSA** dossier, en respectant le **MSGraph** dossier. Vous verrez une copie du même fichier que vous venez de configurer. Sélectionnez le fichier, puis, dans l’inspecteur de :

    -   Vérifiez que **plateforme Any** est **unchecked**et qui **uniquement** **WSAPlayer** est **vérifiée**.

    -   Vérifiez **SDK** a la valeur **UWP**, et **back-end de script** a la valeur **Dot Net**

    -   Vérifiez que **ne pas traiter les** est **vérifiée**.

        ![](images/AzureLabs-Lab311-23.png)

7.  Cliquez sur **Appliquer**.

## <a name="chapter-4---camera-setup"></a>Chapitre 4 - programme d’installation de l’appareil photo

Au cours de ce chapitre, vous allez configurer la caméra principale de votre scène :

1.  Dans le *hiérarchie panneau*, sélectionnez le **Main Camera**.

2.  Une fois sélectionné, vous serez en mesure de voir tous les composants de la **Main Camera** dans le *inspecteur* Panneau de configuration.

    1.  Le **objet caméra** doit être nommé **Main Camera** (Notez l’orthographe !)

    2.  La caméra principale **balise** doit être définie sur **MainCamera** (Notez l’orthographe !)

    3.  Assurez-vous que le **Position transformer** a la valeur **0, 0, 0**

    4.  Définissez **d’effacer les indicateurs** à **couleur unie**

    5.  Définir le **couleur d’arrière-plan** du composant de caméra à **noir, Alpha 0** **(Hex Code : #00000000)**

        ![](images/AzureLabs-Lab311-24.png)

3.  La structure de l’objet final dans le *hiérarchie panneau* doit être semblable à celui illustré dans l’image ci-dessous :

    ![](images/AzureLabs-Lab311-25.png)

## <a name="chapter-5---create-meetingsui-class"></a>Chapitre 5 - créer MeetingsUI classe

Le premier script que vous créez est **MeetingsUI**, qui est responsable de l’hébergement et de remplissage de l’interface utilisateur de l’application (message de bienvenue, des instructions et les détails de réunions).

Pour créer cette classe :

1.  Avec le bouton droit sur le **actifs** dossier dans le *panneau projet*, puis sélectionnez **créer* > *dossier**. Nommez le dossier **Scripts**.

    ![](images/AzureLabs-Lab311-26.png)
    ![](images/AzureLabs-Lab311-27.png)

2.  Ouvrez le **Scripts** dossier puis, dans ce dossier, avec le bouton droit, **créer* > *C\# Script**. Nommez le script **MeetingsUI.**

    ![](images/AzureLabs-Lab311-28.png)

3.  Double-cliquez sur le nouveau **MeetingsUI** script pour l’ouvrir avec *Visual Studio*.

4.  Insérer des espaces de noms suivants :

    ```csharp
    using System;
    using UnityEngine;
    ```

5.  À l’intérieur de la classe, insérez les variables suivantes :

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

6.  Remplacez ensuite le **Start()** (méthode) et ajoutez un **Awake()** (méthode). Il seront appelées lors de l’initialisation de la classe :

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

7.  Ajoutez les méthodes chargées de créer le *l’interface utilisateur de réunions* et le remplir avec les réunions en cours lorsque demandé :

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

8. **Supprimer** le **Update()** (méthode), et **enregistrer vos modifications** dans Visual Studio avant de retourner à Unity. 

## <a name="chapter-6---create-the-graph-class"></a>Chapitre 6 : créer la classe de graphique

Le script suivant pour créer le **Graph** script. Ce script est chargé d’effectuer les appels pour authentifier l’utilisateur et de récupérer les réunions planifiées pour le jour actuel à partir du calendrier de l’utilisateur.

Pour créer cette classe :

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.

2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**  >   **C# Script**. Nommez le script **graphique**.

3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio.

4.  Insérer des espaces de noms suivants :

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
    > Vous remarquerez que les parties du code dans ce script sont wrappés autour de [précompiler les Directives](https://docs.unity3d.com/Manual/PlatformDependentCompilation.html), sert à éviter les problèmes rencontrés avec les bibliothèques lors de la création de la Solution Visual Studio.

5.  Supprimer le **Start()** et **Update()** méthodes, car ils ne seront pas utilisés.

6.  En dehors du **Graph** de classe, insérez les objets suivants, qui sont nécessaires pour désérialiser l’objet JSON représentant les réunions planifiées quotidiennes :

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

7.  À l’intérieur de la **Graph** de classe, ajoutez les variables suivantes :

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
    > Modifier le **appId** valeur soit la **Id d’application** que vous avez déjà notés dans  **[chapitre 1](#chapter-1---create-your-app-in-the-application-registration-portal), étape 4**. Cette valeur doit être identique à celui affiché dans le **portail d’inscription des applications,** dans la page d’inscription de votre application.

8.  Dans le **Graph** de classe, ajoutez les méthodes **SignInAsync()** et **AquireTokenAsync()**, qui invitera l’utilisateur d’insérer les informations de journal.

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

9.  Ajoutez les deux méthodes suivantes :

    1.  **BuildTodayCalendarEndpoint()**, quelles sont les builds l’URI spécifiant le jour et l’intervalle de temps, dans lequel les réunions planifiées sont récupérées.

    2.  **ListMeetingsAsync()**, qui demande les réunions planifiées à partir de *Microsoft Graph*.

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

10. Vous avez maintenant terminé la **Graph** script. **Enregistrez vos modifications** dans Visual Studio avant de retourner à Unity.

## <a name="chapter-7---create-the-gazeinput-script"></a>Chapitre 7 - créer le script GazeInput

Vous allez maintenant créer le **GazeInput**. Cette classe gère et effectue le suivi des regards de l’utilisateur, à l’aide un **Raycast** provenant de la **Main Camera**, projeter vers l’avant.

Pour créer le script :

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.

2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**  >   **C# Script**. Nommez le script **GazeInput**.

3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio.

4.  Modifier le code des espaces de noms pour correspondre à celui ci-dessous, ainsi que l’ajout de la '**\[System.Serializable\]**' balise ci-dessus votre **GazeInput** classe, afin qu’il puisse être sérialisé :

    ```csharp
    using UnityEngine;

    /// <summary>
    /// Class responsible for the User's Gaze interactions
    /// </summary>
    [System.Serializable]
    public class GazeInput : MonoBehaviour
    {
    ```

5.  À l’intérieur de la **GazeInput** de classe, ajoutez les variables suivantes :

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

6.  Ajouter le **CreateCursor()** pour créer le curseur HoloLens dans la scène et appelez la méthode depuis le **Start()** méthode :

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

7.  Les méthodes suivantes permettent les regards Raycast et de suivre les objets ayant le focus.

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

8.  **Enregistrez vos modifications** dans Visual Studio avant de retourner à Unity.

## <a name="chapter-8---create-the-interactions-class"></a>Chapitre 8 - créer la classe d’Interactions

Vous devez maintenant créer le **Interactions** script, qui est chargé de :

-   Gestion de la **appuyez sur** interaction et la **utilisation de l’appareil photo**, ce qui permet à l’utilisateur d’interagir avec le journal dans le « bouton » dans la scène.

-   Création du journal dans l’objet « bouton » dans la scène pour l’utilisateur d’interagir avec.

Pour créer le script :

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.

2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**  >   **C# Script**. Nommez le script **Interactions**.

3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio.

4.  Insérer des espaces de noms suivants :

    ```csharp
    using UnityEngine;
    using UnityEngine.XR.WSA.Input;
    ```

5.  Modifier l’héritage de la **Interaction** classe *MonoBehaviour* à **GazeInput**.

    ~~Interactions de classe publique : MonoBehaviour~~

    ```csharp
    public class Interactions : GazeInput
    ```

6.  À l’intérieur de la **Interaction** classe insérer la variable suivante :

    ```csharp
        /// <summary>
        /// Allows input recognition with the HoloLens
        /// </summary>
        private GestureRecognizer _gestureRecognizer;
    ```

7.  Remplacez le **Démarrer** méthode ; Notez qu’il est une méthode de remplacement, qui appelle la méthode de classe du pointage de regard 'base'. **Start()** sera appelé lors de l’initialisation de la classe, l’inscription pour la reconnaissance d’entrée et la création de la connexion *bouton* dans la scène :

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

8.  Ajouter le **CreateSignInButton()** méthode qui instancie le signe dans *bouton* dans la scène et définissez ses propriétés :

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

9.  Ajouter le **GestureRecognizer_Tapped()** (méthode), être répondre pour le *appuyez sur* événement utilisateur.

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

10. **Supprimer** le **Update()** (méthode), puis **enregistrer vos modifications** dans Visual Studio avant de retourner à Unity.

## <a name="chapter-9---set-up-the-script-references"></a>Chapitre 9 - configurer les références de script

Dans ce chapitre, vous devez placer le **Interactions** de script sur le **Main Camera**. Ce script gère à placer les autres scripts où ils doivent être.

-  À partir de la **Scripts** dossier dans le *panneau projet*, faites glisser le script **Interactions** à la **Main Camera** de l’objet, comme illustré ci-dessous.

    ![](images/AzureLabs-Lab311-29.png)

## <a name="chapter-10---setting-up-the-tag"></a>Chapitre 10 - Configuration de la balise

Le code qui gère les regards utilisera la balise **SignInButton** pour identifier quel objet de l’utilisateur interagit pour se connecter à *Microsoft Graph*.

Pour créer la balise :

1.  Dans l’éditeur Unity, cliquez sur le **Main Camera** dans le *hiérarchie panneau*.

2.  Dans le *panneau Inspecteur* cliquez sur le **MainCamera** *balise* pour ouvrir la liste déroulante. Cliquez sur **ajouter une balise...**

    ![](images/AzureLabs-Lab311-30.png)

3.  Cliquez sur le **+** bouton.

    ![](images/AzureLabs-Lab311-31.png)

4.  Écrivez le nom de balise en tant que **SignInButton** et cliquez sur Enregistrer.

    ![](images/AzureLabs-Lab311-32.png)

## <a name="chapter-11---build-the-unity-project-to-uwp"></a>Chapitre 11 - générer le projet Unity vers UWP

Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée, il est temps de générer à partir de Unity.

1.  Accédez à *les paramètres de génération* (**fichier* > *Build paramètres**).

    ![](images/AzureLabs-Lab311-33.png)

2.  Si pas déjà fait, cochez **Unity C\# projets**.

3.  Cliquez sur **Build**. Unity lancera un **Explorateur de fichiers** fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans. Créez ce dossier, puis nommez-le **application**. Ensuite avec le **application** dossier sélectionné, cliquez sur **sélectionner le dossier**.

4.  Unity commencera à générer votre projet pour le **application** dossier.

5.  Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un **Explorateur de fichiers** fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).

## <a name="chapter-12---deploy-to-hololens"></a>Chapitre 12 - déployer sur HoloLens

Pour déployer sur HoloLens :

1.  Vous devez l’adresse IP de votre HoloLens (pour les déployer à distance) et pour vérifier que votre HoloLens est dans **Mode développeur.** Pour ce faire :

    1.  Tout en portant vos HoloLens, ouvrez le **paramètres**.

    2.  Accédez à **réseau & Internet** > **Wi-Fi** > **les Options avancées**

    3.  Remarque la **IPv4** adresse.

    4.  Ensuite, accédez à **paramètres**, puis à **mise à jour & sécurité** > **pour les développeurs**

    5.  Définissez **Mode développeur sur**.

2.  Accédez à votre nouvelle build Unity (le **application** dossier) et ouvrez le fichier solution avec **Visual Studio**.

3.  Dans le **Configuration de la Solution** sélectionnez **déboguer**.

4.  Dans le **plateforme de Solution**, sélectionnez **x86, ordinateur distant**. Vous devrez insérer le **adresse IP** d’un appareil à distance (la HoloLens, dans ce cas, que vous avez notée).

    ![](images/AzureLabs-Lab311-34.png)

5.  Accédez à **Build** menu et cliquez sur **déployer la Solution** à chargement indépendant de l’application à votre HoloLens.

6.  Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prêt à être lancé !

## <a name="your-microsoft-graph-hololens-application"></a>Votre application Microsoft Graph HoloLens

Félicitations, vous avez créé une application de réalité mixte qui tire parti de Microsoft Graph pour lire et afficher les données de calendrier d’utilisateur.

![](images/AzureLabs-Lab311-00.png)

## <a name="bonus-exercises"></a>Exercices de bonus

### <a name="exercise-1"></a>Exercice 1

Microsoft Graph permet d’afficher d’autres informations sur l’utilisateur

-   E-mail de l’utilisateur / numéro de téléphone / image de profil

### <a name="exercise-1"></a>Exercice 1

Implémenter le contrôle de voix pour naviguer de l’interface utilisateur graphique de Microsoft.
