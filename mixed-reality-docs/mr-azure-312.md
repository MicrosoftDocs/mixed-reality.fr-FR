---
title: Intégration de MR et Azure 312-bot
description: Suivez ce cours pour apprendre à créer et à déployer un robot à l’aide de Microsoft bot Framework v4 et à communiquer avec lui dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Académie, Unity, didacticiel, API, vision par ordinateur, hololens, immersif, VR, Microsoft bot Framework v4, application Web bot, robot Framework, Microsoft bot
ms.openlocfilehash: 481693b5af8c946e1cb45dda5144e78a175fa771
ms.sourcegitcommit: 3b32339c5d5c79eaecd84ed27254a8f4321731f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70047229"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

# <a name="mr-and-azure-312-bot-integration"></a>MR et Azure 312: Intégration de bot

Dans ce cours, vous allez apprendre à créer et à déployer un robot à l’aide de Microsoft bot Framework v4 et à communiquer avec lui via une application Windows Mixed Reality. 

![](images/AzureLabs-Lab312-00.png)

**Microsoft bot Framework v4** est un ensemble d’API conçu pour fournir aux développeurs les outils nécessaires à la création d’une application bot extensible et évolutive. Pour plus d’informations, consultez la [page Microsoft bot Framework](https://dev.botframework.com/) ou le [référentiel git de v4](https://github.com/Microsoft/botbuilder-dotnet/wiki).

À l’issue de ce cours, vous aurez créé une application Windows Mixed Reality, qui sera en mesure d’effectuer les opérations suivantes:

1. Utilisez un **geste TAP** pour démarrer le robot à l’écoute de la voix des utilisateurs.
2. Lorsque l’utilisateur a déclaré un événement, le bot tente de fournir une réponse.
3. Affichez la réponse des robots sous forme de texte, positionné près du bot, dans la scène Unity.

Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception. Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity. C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> MR et Azure 312: Intégration de bot</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Bien que ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques pour Windows Mixed Reality (VR). Étant donné que les casques immersifs ne disposent pas de caméras accessibles, vous aurez besoin d’une caméra externe connectée à votre PC. À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge les écouteurs immersifs (VR).

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et. Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de la rédaction (juillet 2018). Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.

Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:

- Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)
- [Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé](install-the-tools.md#installation-checklist)
- [Le dernier Kit de développement logiciel Windows 10](install-the-tools.md#installation-checklist)
- [Unity 2017,4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé
- Accès Internet pour Azure et récupération Azure bot. Pour plus d’informations, [veuillez suivre ce lien](https://dev.botframework.com/).

### <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).
2.  Configurez et testez votre HoloLens. Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup). 
3.  Il est judicieux d’effectuer un réglage de l’étalonnage et du capteur au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur). 

Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens-2).

Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).

## <a name="chapter-1--create-the-bot-application"></a>Chapitre 1: créer l’application bot

La première étape consiste à créer votre robot en tant qu’application Web ASP.Net Core locale. Une fois que vous avez terminé et testé, vous allez le publier sur le portail Azure.

1.  Ouvrez Visual Studio. Créez un nouveau projet, sélectionnez **application Web ASP.net Core ASP** comme type de projet (vous le trouverez sous la sous-section .net Core) et appelez-le **MyBot**. Cliquez sur **OK**.

2.  Dans la fenêtre qui s’affiche, sélectionnez **vide**. Assurez-vous également que la cible est définie sur **asp net Core 2,0** et que l’authentification est définie sur **aucune authentification**. Cliquez sur **OK**.  

    ![Créer l’application bot](images/AzureLabs-Lab312-01.png)

3.  La solution s’ouvre maintenant. Cliquez avec le bouton droit sur la solution **Mybot** dans le **Explorateur de solutions** , puis cliquez sur **gérer les packages NuGet pour la solution**. 

    ![Créer l’application bot](images/AzureLabs-Lab312-02.png)

4.  Sous l’onglet **Parcourir** , recherchez **Microsoft. Bot. Builder. Integration. Aspnet. Core** (Assurez-vous que l’option inclure la **version préliminaire** est activée). Sélectionnez la version **de package 4.0.1-preview**, puis cochez les cases du projet. Cliquez ensuite sur **installer**. Vous avez maintenant installé les bibliothèques nécessaires pour **bot Framework v4**. Fermez la page NuGet.

    ![Créer l’application bot](images/AzureLabs-Lab312-03.png)

5.  Cliquez avec le bouton droit sur votre *projet*, **MyBot**, dans le **Explorateur de solutions** , puis cliquez sur **Ajouter** **|** une **classe**.

    ![Créer l’application bot](images/AzureLabs-Lab312-04.png)

6.  Nommez la classe **MyBot** , puis cliquez sur **Ajouter**.

    ![Créer l’application bot](images/AzureLabs-Lab312-05.png)

7.  Répétez le point précédent pour créer une autre classe nommée **ConversationContext**. 

8.  Cliquez avec le bouton droit sur **wwwroot** dans le **Explorateur de solutions** , puis cliquez sur **Ajouter** **|** **un nouvel élément**. Sélectionnez **page HTML** (vous la trouverez sous la sous-section Web). Nommez le fichier **default. html**. Cliquez sur **Ajouter**.

    ![Créer l’application bot](images/AzureLabs-Lab312-06.png)

9.  La liste des classes/objets dans le **Explorateur de solutions** doit ressembler à l’image ci-dessous.

    ![Créer l’application bot](images/AzureLabs-Lab312-07.png)

10. Double-cliquez sur la classe **ConversationContext** . Cette classe est chargée de conserver les variables utilisées par le bot pour gérer le contexte de la conversation. Ces valeurs de contexte de conversation sont conservées dans une instance de cette classe, car toutes les instances de la classe **MyBot** sont actualisées chaque fois qu’une activité est reçue. Ajoutez le code suivant à la classe:

    ```csharp
    namespace MyBot
    {
        public static class ConversationContext
        {
            internal static string userName;

            internal static string userMsg;
        }
    }
    ```

11. Double-cliquez sur la classe **MyBot** . Cette classe hébergera les gestionnaires appelés par toute activité entrante du client. Dans cette classe, vous allez ajouter le code utilisé pour créer la conversation entre le bot et le client. Comme mentionné précédemment, une instance de cette classe est initialisée chaque fois qu’une activité est reçue. Ajoutez le code suivant à cette classe:

    ```csharp
    using Microsoft.Bot;
    using Microsoft.Bot.Builder;
    using Microsoft.Bot.Schema;
    using System.Threading.Tasks;

    namespace MyBot
    {
        public class MyBot : IBot
        {       
            public async Task OnTurn(ITurnContext context)
            {
                ConversationContext.userMsg = context.Activity.Text;

                if (context.Activity.Type is ActivityTypes.Message)
                {
                    if (string.IsNullOrEmpty(ConversationContext.userName))
                    {
                        ConversationContext.userName = ConversationContext.userMsg;
                        await context.SendActivity($"Hello {ConversationContext.userName}. Looks like today it is going to rain. \nLuckily I have umbrellas and waterproof jackets to sell!");
                    }
                    else
                    {
                        if (ConversationContext.userMsg.Contains("how much"))
                        {
                            if (ConversationContext.userMsg.Contains("umbrella")) await context.SendActivity($"Umbrellas are $13.");
                            else if (ConversationContext.userMsg.Contains("jacket")) await context.SendActivity($"Waterproof jackets are $30.");
                            else await context.SendActivity($"Umbrellas are $13. \nWaterproof jackets are $30.");
                        }
                        else if (ConversationContext.userMsg.Contains("color") || ConversationContext.userMsg.Contains("colour"))
                        {
                            await context.SendActivity($"Umbrellas are black. \nWaterproof jackets are yellow.");
                        }
                        else
                        {
                            await context.SendActivity($"Sorry {ConversationContext.userName}. I did not understand the question");
                        }
                    }
                }
                else
                {

                    ConversationContext.userMsg = string.Empty;
                    ConversationContext.userName = string.Empty;
                    await context.SendActivity($"Welcome! \nI am the Weather Shop Bot \nWhat is your name?");
                }

            }
        }
    }
    ```

12. Double-cliquez sur la classe **Startup** . Cette classe Initialise le bot. Ajoutez le code suivant à la classe:

    ```csharp
    using Microsoft.AspNetCore.Builder;
    using Microsoft.AspNetCore.Hosting;
    using Microsoft.Bot.Builder.BotFramework;
    using Microsoft.Bot.Builder.Integration.AspNet.Core;
    using Microsoft.Extensions.Configuration;
    using Microsoft.Extensions.DependencyInjection;

    namespace MyBot
    {
    public class Startup
        {
            public IConfiguration Configuration { get; }

            public Startup(IHostingEnvironment env)
            {
                var builder = new ConfigurationBuilder()
                    .SetBasePath(env.ContentRootPath)
                    .AddJsonFile("appsettings.json", optional: true, reloadOnChange: true)
                    .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true)
                    .AddEnvironmentVariables();
                Configuration = builder.Build();
            }

            // This method gets called by the runtime. Use this method to add services to the container.
            public void ConfigureServices(IServiceCollection services)
            {
                services.AddSingleton(_ => Configuration);
                services.AddBot<MyBot>(options =>
                {
                    options.CredentialProvider = new ConfigurationCredentialProvider(Configuration);
                });
            }

            // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
            public void Configure(IApplicationBuilder app, IHostingEnvironment env)
            {
                if (env.IsDevelopment())
                {
                    app.UseDeveloperExceptionPage();
                }

                app.UseDefaultFiles();
                app.UseStaticFiles();
                app.UseBotFramework();
            }
        }
    }
    ```

13. Ouvrez le fichier de classe de **programme** et vérifiez que le code est le même que celui-ci:

    ```csharp
    using Microsoft.AspNetCore;
    using Microsoft.AspNetCore.Hosting;

    namespace MyBot
    {
        public class Program
        {
            public static void Main(string[] args)
            {
                BuildWebHost(args).Run();
            }

            public static IWebHost BuildWebHost(string[] args) =>
                WebHost.CreateDefaultBuilder(args)
                    .UseStartup<Startup>()
                    .Build();
        }
    }
    ```

14. N’oubliez pas d’enregistrer vos modifications. pour ce faire, accédez à **fichier** > **enregistrer tout**, à partir de la barre d’outils en haut de Visual Studio.

## <a name="chapter-2---create-the-azure-bot-service"></a>Chapitre 2-créer le Azure Bot Service

Maintenant que vous avez généré le code de votre bot, vous devez le publier dans une instance du service *Web App bot* , sur le portail Azure. Ce chapitre vous indique comment créer et configurer le service bot sur Azure, puis comment y publier votre code.

1.  Tout d’abord, connectez-vous au portail https://portal.azure.com) Azure (. 

    1. Si vous n’avez pas encore de compte Azure, vous devez en créer un. Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **créer une ressource** dans le coin supérieur gauche et recherchez *Web App bot*, puis cliquez sur **entrée**.

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-08.png)
 
3.  La nouvelle page fournit une description du service *Web App bot* . En bas à gauche de cette page, cliquez sur le bouton **créer** pour créer une association avec ce service.

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-09.png)
 
4.  Une fois que vous avez cliqué sur **créer**:

    1. Insérez le **nom** de votre choix pour cette instance de service.
    2. Sélectionnez un **abonnement**.
    3. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, [veuillez suivre ce lien](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)

    4. Déterminez l’emplacement de votre groupe de ressources (si vous créez un groupe de ressources). L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait. Certaines ressources Azure sont uniquement disponibles dans certaines régions.
    5. Sélectionnez le **niveau tarifaire** approprié, s’il s’agit de la première fois que vous créez un service *Web App bot* , vous devez disposer d’un niveau gratuit (nommé F0).
    6. Le nom de l' **application** peut simplement rester identique au *nom du robot*. 
    7. Laissez le *modèle bot* de **base (C#)** .
    8. Le *plan/emplacement App service* doit avoir été rempli automatiquement pour votre compte.
    9. Définissez le **stockage Azure** que vous souhaitez utiliser pour héberger votre robot. Si vous n’en avez pas déjà un, vous pouvez le créer ici.
    10. Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.
    11. Cliquez sur créer.
 
        ![Créer le Azure Bot Service](images/AzureLabs-Lab312-10.png)

5.  Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.

6.  Une notification s’affichera dans le portail une fois l’instance de service créée.

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-11.png) 
 
7.  Cliquez sur la notification pour explorer votre nouvelle instance de service. 

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-12.png)
 
8. Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service. Vous êtes dirigé vers votre nouvelle instance de service Azure. 

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-13.png)
 
9.  À ce stade, vous devez configurer une fonctionnalité appelée **ligne directe** pour permettre à votre application cliente de communiquer avec ce service bot. Cliquez sur **canaux**, puis dans la section **Ajouter un canal** à la une, cliquez sur **configurer le canal direct line**.

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-14.png)

10. Dans cette page, vous trouverez les **clés secrètes** qui permettront à votre application cliente de s’authentifier auprès du bot. Cliquez sur le bouton **Afficher** et prenez une copie de l’une des clés affichées, car vous en aurez besoin plus tard dans votre projet. 

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-15.png)

## <a name="chapter-3--publish-the-bot-to-the-azure-web-app-bot-service"></a>Chapitre 3: publier le robot sur le service bot de l’application Web Azure

Maintenant que votre service est prêt, vous devez publier votre code de robot, que vous avez créé précédemment, sur le service de robot d’application Web que vous venez de créer.

> [!NOTE] 
> Vous devez publier votre robot sur le service Azure chaque fois que vous apportez des modifications à la solution ou au code du bot.

1.  Revenez à votre solution Visual Studio que vous avez créée précédemment. 
2.  Cliquez avec le bouton droit sur votre projet **MyBot** , dans le **Explorateur de solutions**, puis cliquez sur **publier**.

    ![Publier le robot sur le service bot de l’application Web Azure](images/AzureLabs-Lab312-16.png)

3.  Sur la page *choisir une cible de publication* , cliquez sur **app service**, puis **Sélectionnez existant**. Enfin, cliquez sur **créer un profil** (vous devrez peut-être cliquer sur la flèche déroulante à côté du bouton *publier* , si ce n’est pas visible).

    ![Publier le robot sur le service bot de l’application Web Azure](images/AzureLabs-Lab312-17.png)

4. Si vous n’êtes pas encore connecté à votre compte Microsoft, vous devez le faire ici.
5. Sur la page **publier** , vous devez définir le même **abonnement** que celui utilisé pour la création du service *Web App bot* . Ensuite, définissez la **vue** en tant que **groupe de ressources** , puis, dans la structure de dossiers déroulante, sélectionnez le groupe de **ressources** que vous avez créé précédemment. Cliquez sur **OK**. 

    ![Publier le robot sur le service bot de l’application Web Azure](images/AzureLabs-Lab312-18.png)

6.  Cliquez maintenant sur le bouton **publier** et attendez la publication du robot (cela peut prendre quelques minutes).

    ![Publier le robot sur le service bot de l’application Web Azure](images/AzureLabs-Lab312-19.png)


## <a name="chapter-4--set-up-the-unity-project"></a>Chapitre 4 – configurer le projet Unity

Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **nouveau**. 

    ![Configurer le projet Unity](images/AzureLabs-Lab312-20.png)

2.  Vous devez maintenant fournir un nom de projet Unity. Insérez le **bot Hololens**. Assurez-vous que le modèle de projet est défini sur **3D**. Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés). Ensuite, cliquez sur **créer un projet**.

    ![Configurer le projet Unity](images/AzureLabs-Lab312-21.png)

3.  Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**. Accédez à **modifier > préférences** puis, dans la nouvelle fenêtre, accédez à **outils externes**. Remplacez l' **éditeur de script externe** par **Visual Studio 2017**. Fermez la fenêtre **Préférences** .

    ![Configurer le projet Unity](images/AzureLabs-Lab312-22.png)

4.  Accédez ensuite à **fichier > paramètres de build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le bouton **changer de plateforme** pour appliquer votre sélection.

    ![Configurer le projet Unity](images/AzureLabs-Lab312-23.png)

5.  Tout en conservant les **paramètres de génération de > de fichiers** et assurez-vous que:

    1.  L' **appareil cible** est défini sur **Hololens**

        > Pour les casques immersifs, définissez **appareil cible** sur *n’importe quel appareil*.

    2.  Le **type de build** est **D3D**

    3.  Le **SDK** est configuré sur le **dernier installé**

    4.  **Version de Visual Studio** définie sur le **dernier installé**

    5.  La **génération et l’exécution** sont définies sur l' **ordinateur local**

    6.  Enregistrez la scène et ajoutez-la à la Build. 

        1. Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**. Une fenêtre d’enregistrement s’affiche.
        
            ![Configurer le projet Unity](images/AzureLabs-Lab312-24.png)

        2. Créez un dossier pour cela, ainsi que toute nouvelle scène, puis sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez-le Scenes.

             ![Configurer le projet Unity](images/AzureLabs-Lab312-25.png)

        3. Ouvrez le dossier scenes nouvellement créé, puis dans le champ *nom de fichier*:, tapez **BotScene**, puis cliquez sur **Enregistrer**.

            ![Configurer le projet Unity](images/AzureLabs-Lab312-26.png)

    7. Les paramètres restants, dans **paramètres de build**, doivent être laissés par défaut pour le moment.

6. Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* . 

    ![Configurer le projet Unity](images/AzureLabs-Lab312-27.png)

7. Dans ce volet, quelques paramètres doivent être vérifiés:

    1. Sous l’onglet **autres paramètres** :

        1. La **version du runtime de script** doit être **expérimentale (net 4,6 équivalent)** ; la modification de cette opération nécessite un redémarrage de l’éditeur.
        2. Le **backend de script** doit être **.net**
        3. Le **niveau de compatibilité** de l’API doit être **.net 4,6**

            ![Configurer le projet Unity](images/AzureLabs-Lab312-28.png)
      
    2. Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:

        - **InternetClient**
        - **Cravate**

            ![Configurer le projet Unity](images/AzureLabs-Lab312-29.png)

    3. Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.

        ![Configurer le projet Unity](images/AzureLabs-Lab312-30.png)

8.  De retour dans les *paramètres de build* , les projets _Unity C#_  ne sont plus grisés. Cochez la case en regard de cette option. 
9.  Fermez la fenêtre Paramètres de Build.
10. Enregistrez votre scène et votre projet (**fichier > enregistrer la scène/le fichier > enregistrer le projet**).


## <a name="chapter-5--camera-setup"></a>Chapitre 5 – Configuration de l’appareil photo

> [!IMPORTANT]
> Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce fichier [Azure-Mr-312-package. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20312%20-%20Bot%20integration/Azure-MR-312.unitypackage), à l’importer dans votre projet en tant que [**package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis à [continuer Chapitre 7](#chapter-8--create-the-botobjects-class).

1.  Dans le *panneau hiérarchie*, sélectionnez l' **appareil photo principal**. 
2.  Une fois sélectionné, vous pouvez voir tous les composants de la **caméra principale** dans le *panneau Inspecteur*.

    1. L' **objet Camera** doit être nommé **Camera main** (Notez l’orthographe)
    2. La balise principale de l’appareil photo doit être définie sur **MainCamera** (Notez l’orthographe)
    3. Vérifiez que la **position** de la transformation est définie sur **0, 0,** 0
    4. Affectez à **effacer les indicateurs** la **couleur unie**.
    5. Définir la couleur d' **arrière-plan** du composant Camera sur **Black, alpha 0 (Code hexadécimal: #00000000)**

    ![Configuration de l’appareil photo](images/AzureLabs-Lab312-31.png)
 

## <a name="chapter-6--import-the-newtonsoft-library"></a>Chapitre 6-importer la bibliothèque Newtonsoft

Pour vous aider à désérialiser et à sérialiser les objets reçus et envoyés au service bot, vous devez télécharger la bibliothèque **Newtonsoft** . Vous trouverez ici une [version compatible déjà organisée avec la structure de dossiers Unity correcte](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20312%20-%20Bot%20integration/NewtonsoftDLL.unitypackage). 

Pour importer la bibliothèque Newtonsoft dans votre projet, utilisez le package Unity fourni avec ce cours.

1.  Ajoutez le fichier *. pour Unity* à Unity à l’aide de l’option de menu**package personnalisé** du**package** > d’importation de **ressources** > .

    ![Importer la bibliothèque Newtonsoft](images/AzureLabs-Lab312-34.png)

2.  Dans la zone **importer le package Unity** qui s’affiche, vérifiez que tous les plug- **ins** sous (et y compris) sont sélectionnés.

    ![Importer la bibliothèque Newtonsoft](images/AzureLabs-Lab312-35.png)

3.  Cliquez sur le bouton **Importer** pour ajouter les éléments à votre projet.

4.  Accédez au dossier **Newtonsoft** sous **plug-ins** dans la vue projet et sélectionnez le plug-in Newtonsoft.

    ![](images/AzureLabs-Lab312-35b.png)

5.  Une fois le plug-in Newtonsoft sélectionné, assurez-vous que **toutes les plateformes** sont décochées, vérifiez que **WSAPlayer** est également **désactivé**, puis cliquez sur **appliquer**. Cela vous permet de vérifier que les fichiers sont correctement configurés.

    ![](images/AzureLabs-Lab312-35c.png)

    > [!NOTE]
    > Le marquage de ces plug-ins permet de les configurer pour qu’ils soient utilisés uniquement dans l’éditeur Unity. Il y en a un ensemble différent dans le dossier WSA qui sera utilisé une fois que le projet est exporté d’Unity.

6.  Ensuite, vous devez ouvrir le dossier **WSA** , dans le dossier **Newtonsoft** . Vous verrez une copie du même fichier que celui que vous venez de configurer. Sélectionnez le fichier, puis, dans l’inspecteur, vérifiez que
    -   **Aucune plateforme** n' est désactivée 
    -   **uniquement** **WSAPlayer** est **activé**
    -   L’option ne pas **traiter le processus** est **activée**

    ![](images/AzureLabs-Lab312-35d.png)

## <a name="chapter-7--create-the-bottag"></a>Chapitre 7: créer le BotTag

1.  Créez un nouvel objet **tag** appelé **BotTag**. Sélectionnez la caméra principale dans la scène. Cliquez sur le menu déroulant des balises dans le panneau Inspecteur. Cliquez sur **Ajouter une étiquette**.

    ![Configuration de l’appareil photo](images/AzureLabs-Lab312-32.png)
 
2.  Cliquez sur le **+** symbole. Nommez la nouvelle balise **BotTag**, *Save*.

    ![Configuration de l’appareil photo](images/AzureLabs-Lab312-33.png)

> [!WARNING] 
> **N’appliquez pas** les **BotTag** à l’appareil photo principal. Si vous avez effectué cette opération par inadvertance, veillez à remplacer la balise d’appareil photo principale par *MainCamera*.

## <a name="chapter-8--create-the-botobjects-class"></a>Chapitre 8: créer la classe BotObjects

Le premier script que vous devez créer est la classe **BotObjects** , qui est une classe vide créée afin qu’une série d’autres objets de classe puisse être stockée dans le même script et accessible par d’autres scripts dans la scène.

La création de cette classe est purement un choix architectural, ces objets peuvent plutôt être hébergés dans le script de bot que vous allez créer plus loin dans ce cours.

Pour créer cette classe: 

1.  Cliquez avec le bouton droit dans le *panneau Projet*, puis **créez > dossier**. Nommez le dossier **scripts**. 

    ![Créer un dossier de scripts.](images/AzureLabs-Lab312-36.png)

2.  Double-cliquez sur le dossier **scripts** pour l’ouvrir. Ensuite, dans ce dossier, cliquez avec le bouton droit, puis sélectionnez **créer > C# script**. Nommez le script **BotObjects**. 

3.  Double-cliquez sur le nouveau script **BotObjects** pour l’ouvrir avec **Visual Studio**.

4.  Supprimez le contenu du script et remplacez-le par le code suivant:

    ```csharp
    using System;
    using System.Collections;
    using System.Collections.Generic;
    using UnityEngine;

    public class BotObjects : MonoBehaviour{}

    /// <summary>
    /// Object received when first opening a conversation
    /// </summary>
    [Serializable]
    public class ConversationObject
    {
        public string ConversationId;
        public string token;
        public string expires_in;
        public string streamUrl;
        public string referenceGrammarId;
    }

    /// <summary>
    /// Object including all Activities
    /// </summary>
    [Serializable]
    public class ActivitiesRootObject
    {
        public List<Activity> activities { get; set; }
        public string watermark { get; set; }
    }
    [Serializable]
    public class Conversation
    {
        public string id { get; set; }
    }
    [Serializable]
    public class From
    {
        public string id { get; set; }
        public string name { get; set; }
    }
    [Serializable]
    public class Activity
    {
        public string type { get; set; }
        public string channelId { get; set; }
        public Conversation conversation { get; set; }
        public string id { get; set; }
        public From from { get; set; }
        public string text { get; set; }
        public string textFormat { get; set; }
        public DateTime timestamp { get; set; }
        public string serviceUrl { get; set; }
    }
    ```

6.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenirà Unity.

## <a name="chapter-9--create-the-gazeinput-class"></a>Chapitre 9: créer la classe GazeInput

La classe suivante que vous allez créer est la classe **GazeInput** . Cette classe est chargée des opérations suivantes:

- Création d’un curseur qui représentera le point de *regard* du joueur.
- Détection des objets atteints par le point de présence du joueur et maintien d’une référence aux objets détectés.

Pour créer cette classe: 

1.  Accédez au dossier **scripts** que vous avez créé précédemment. 
2.  Cliquez avec le bouton droit dans le dossier, **créez > C# script**. Appelez le script **GazeInput**. 
3.  Double-cliquez sur le nouveau script **GazeInput** pour l’ouvrir avec **Visual Studio**.
4.  Insérez la ligne suivante juste au-dessus du nom de la classe:

    ```csharp
    /// <summary>
    /// Class responsible for the User's gaze interactions
    /// </summary>
    [System.Serializable]
    public class GazeInput : MonoBehaviour
    ```

5.  Ajoutez ensuite les variables suivantes à l’intérieur de la classe **GazeInput** , au-dessus de la méthode **Start ()** :

    ```csharp
        [Tooltip("Used to compare whether an object is to be interacted with.")]
        internal string InteractibleTag = "BotTag";

        /// <summary>
        /// Length of the gaze
        /// </summary>
        internal float GazeMaxDistance = 300;

        /// <summary>
        /// Object currently gazed
        /// </summary>
        internal GameObject FocusedObject { get; private set; }

        internal GameObject _oldFocusedObject { get; private set; }

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

6.  Le code de la méthode **Start ()** doit être ajouté. Cette méthode est appelée lorsque la classe est initialisée:

    ```csharp
        /// <summary>
        /// Start method used upon initialization.
        /// </summary>
        internal virtual void Start()
        {
            FocusedObject = null;
            Cursor = CreateCursor();
        }
    ```

7.  Implémentez une méthode qui instanciera et configurera le curseur en regard: 

    ```csharp
        /// <summary>
        /// Method to create a cursor object.
        /// </summary>
        internal GameObject CreateCursor()
        {
            GameObject newCursor = GameObject.CreatePrimitive(PrimitiveType.Sphere);
            newCursor.SetActive(false);
            // Remove the collider, so it does not block Raycast.
            Destroy(newCursor.GetComponent<SphereCollider>());
            newCursor.transform.localScale = new Vector3(0.05f, 0.05f, 0.05f);
            Material mat = new Material(Shader.Find("Diffuse"));
            newCursor.GetComponent<MeshRenderer>().material = mat;
            mat.color = Color.HSVToRGB(0.0223f, 0.7922f, 1.000f);
            newCursor.SetActive(true);

            return newCursor;
        }
    ```

8.  Implémentez les méthodes qui configurent le Raycast à partir de l’appareil photo principal et effectueront le suivi de l’objet actif actuel.

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
            if (_oldFocusedObject != null)
            {
                if (_oldFocusedObject.CompareTag(InteractibleTag))
                {
                    // Provide the OnGazeExited event.
                    _oldFocusedObject.SendMessage("OnGazeExited", 
                        SendMessageOptions.DontRequireReceiver);
                }
            }
        }


        private void UpdateRaycast()
        {
            // Set the old focused gameobject.
            _oldFocusedObject = FocusedObject;
            RaycastHit hitInfo;

            // Initialize Raycasting.
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
            if (FocusedObject != _oldFocusedObject)
            {
                ResetFocusedObject();
                if (FocusedObject != null)
                {
                    if (FocusedObject.CompareTag(InteractibleTag))
                    {
                        // Provide the OnGazeEntered event.
                        FocusedObject.SendMessage("OnGazeEntered",
                            SendMessageOptions.DontRequireReceiver);
                    }
                }
            }
        }
    ```
 
9.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenirà Unity.

## <a name="chapter-10--create-the-bot-class"></a>Chapitre 10: créer la classe bot

Le script que vous allez créer est maintenant appelé **bot**. Il s’agit de la classe de base de votre application. elle stocke les éléments suivants: 

- Vos informations d’identification Web App bot
- Méthode qui collecte les commandes vocales de l’utilisateur
- La méthode nécessaire pour initier des conversations avec votre robot d’application Web 
- La méthode nécessaire pour envoyer des messages à votre bot d’application Web 

Pour envoyer des messages au service bot, la Coroutine **SendMessageToBot ()** génère une activité, qui est un objet reconnu par le robot Framework comme données envoyées par l’utilisateur. 
 
Pour créer cette classe: 

1. Double-cliquez sur le dossier **scripts** pour l’ouvrir. 
2. Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**. Nommez le script **bot**. 
3. Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.
4. Mettez à jour les espaces de noms pour qu’ils soient identiques à ce qui suit, en haut de la classe **bot** :

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.Text;
    using UnityEngine;
    using UnityEngine.Networking;
    using UnityEngine.Windows.Speech;
    ```
 
5. À l’intérieur de la classe **bot** , ajoutez les variables suivantes:

    ```csharp
        /// <summary>
        /// Static instance of this class
        /// </summary>
        public static Bot Instance;

        /// <summary>
        /// Material of the sphere representing the Bot in the scene
        /// </summary>
        internal Material botMaterial;

        /// <summary>
        /// Speech recognizer class reference, which will convert speech to text.
        /// </summary>
        private DictationRecognizer dictationRecognizer;

        /// <summary>
        /// Use this variable to identify the Bot Id
        /// Can be any value
        /// </summary>
        private string botId = "MRBotId";

        /// <summary>
        /// Use this variable to identify the Bot Name
        /// Can be any value
        /// </summary>
        private string botName = "MRBotName";

        /// <summary>
        /// The Bot Secret key found on the Web App Bot Service on the Azure Portal
        /// </summary>
        private string botSecret = "-- Add your Secret Key here --"; 

        /// <summary>
        /// Bot Endpoint, v4 Framework uses v3 endpoint at this point in time
        /// </summary>
        private string botEndpoint = "https://directline.botframework.com/v3/directline";

        /// <summary>
        /// The conversation object reference
        /// </summary>
        private ConversationObject conversation;

        /// <summary>
        /// Bot states to regulate the application flow
        /// </summary>
        internal enum BotState {ReadyToListen, Listening, Processing}

        /// <summary>
        /// Flag for the Bot state
        /// </summary>
        internal BotState botState;

        /// <summary>
        /// Flag for the conversation status
        /// </summary>
        internal bool conversationStarted = false;
    ```

    > [!NOTE] 
    > Veillez à insérer la **clé secrète** de votre robot dans la variable **botSecret** . Vous aurez noté la **clé secrète** de votre robot au début de ce cours, au  **[Chapitre 2](#chapter-2---create-the-azure-bot-service), étape 10**.

7. Le code pour **éveillé ()** et **Start ()** doit maintenant être ajouté. 

    ```csharp
        /// <summary>
        /// Called on Initialization
        /// </summary>
        void Awake()
        {
            Instance = this;
        }

        /// <summary>
        /// Called immediately after Awake method
        /// </summary>
        void Start()
        {
            botState = BotState.ReadyToListen;
        }
    ```

8. Ajoutez les deux gestionnaires qui sont appelés par les bibliothèques vocales au début et à la fin de la capture vocale. Le *DictationRecognizer* arrête automatiquement la capture de la voix de l’utilisateur quand l’utilisateur cesse de parler.

    ```csharp
        /// <summary>
        /// Start microphone capture.
        /// </summary>
        public void StartCapturingAudio()
        {
            botState = BotState.Listening;
            botMaterial.color = Color.red;

            // Start dictation
            dictationRecognizer = new DictationRecognizer();
            dictationRecognizer.DictationResult += DictationRecognizer_DictationResult;
            dictationRecognizer.Start();
        }
        

        /// <summary>
        /// Stop microphone capture.
        /// </summary>
        public void StopCapturingAudio()
        {
            botState = BotState.Processing;
            dictationRecognizer.Stop();
        }
        
    ```

1. Le gestionnaire suivant collecte le résultat de l’entrée vocale de l’utilisateur et appelle la Coroutine responsable de l’envoi du message au service de l’application Web.

    ```csharp
        /// <summary>
        /// This handler is called every time the Dictation detects a pause in the speech. 
        /// </summary>
        private void DictationRecognizer_DictationResult(string text, ConfidenceLevel confidence)
        {
            // Update UI with dictation captured
            Debug.Log($"User just said: {text}");      

            // Send dictation to Bot
            StartCoroutine(SendMessageToBot(text, botId, botName, "message"));
            StopCapturingAudio();
        }     
    ```

10. La Coroutine suivante est appelée pour commencer une conversation avec le bot. Vous remarquerez qu’une fois l’appel de conversation terminé, il appellera **SendMessageToCoroutine ()** en passant une série de paramètres qui définit l’activité à envoyer au service bot sous forme de message vide. Cette opération est effectuée pour inviter le service bot à lancer la boîte de dialogue.

    ```csharp
        /// <summary>
        /// Request a conversation with the Bot Service
        /// </summary>
        internal IEnumerator StartConversation()
        {
            string conversationEndpoint = string.Format("{0}/conversations", botEndpoint);

            WWWForm webForm = new WWWForm();

            using (UnityWebRequest unityWebRequest = UnityWebRequest.Post(conversationEndpoint, webForm))
            {
                unityWebRequest.SetRequestHeader("Authorization", "Bearer " + botSecret);
                unityWebRequest.downloadHandler = new DownloadHandlerBuffer();

                yield return unityWebRequest.SendWebRequest();
                string jsonResponse = unityWebRequest.downloadHandler.text;
            
                conversation = new ConversationObject();
                conversation = JsonConvert.DeserializeObject<ConversationObject>(jsonResponse);
                Debug.Log($"Start Conversation - Id: {conversation.ConversationId}");
                conversationStarted = true; 
            }

            // The following call is necessary to create and inject an activity of type //"conversationUpdate" to request a first "introduction" from the Bot Service.
            StartCoroutine(SendMessageToBot("", botId, botName, "conversationUpdate"));
        }    
    ```

11. La Coroutine suivante est appelée pour générer l’activité à envoyer au service bot. 

    ```csharp
        /// <summary>
        /// Send the user message to the Bot Service in form of activity
        /// and call for a response
        /// </summary>
        private IEnumerator SendMessageToBot(string message, string fromId, string fromName, string activityType)
        {
            Debug.Log($"SendMessageCoroutine: {conversation.ConversationId}, message: {message} from Id: {fromId} from name: {fromName}");

            // Create a new activity here
            Activity activity = new Activity();
            activity.from = new From();
            activity.conversation = new Conversation();
            activity.from.id = fromId;
            activity.from.name = fromName;
            activity.text = message;
            activity.type = activityType;
            activity.channelId = "DirectLineChannelId";
            activity.conversation.id = conversation.ConversationId;     

            // Serialize the activity
            string json = JsonConvert.SerializeObject(activity);

            string sendActivityEndpoint = string.Format("{0}/conversations/{1}/activities", botEndpoint, conversation.ConversationId);
            
            // Send the activity to the Bot
            using (UnityWebRequest www = new UnityWebRequest(sendActivityEndpoint, "POST"))
            {
                www.uploadHandler = new UploadHandlerRaw(Encoding.UTF8.GetBytes(json));

                www.downloadHandler = new DownloadHandlerBuffer();
                www.SetRequestHeader("Authorization", "Bearer " + botSecret);
                www.SetRequestHeader("Content-Type", "application/json");

                yield return www.SendWebRequest();

                // extrapolate the response Id used to keep track of the conversation
                string jsonResponse = www.downloadHandler.text;
                string cleanedJsonResponse = jsonResponse.Replace("\r\n", string.Empty);
                string responseConvId = cleanedJsonResponse.Substring(10, 30);

                // Request a response from the Bot Service
                StartCoroutine(GetResponseFromBot(activity));
            }
        }
    ```

12. La Coroutine suivante est appelée pour demander une réponse après l’envoi d’une activité au service bot. 

    ```csharp
        /// <summary>
        /// Request a response from the Bot by using a previously sent activity
        /// </summary>
        private IEnumerator GetResponseFromBot(Activity activity)
        {
            string getActivityEndpoint = string.Format("{0}/conversations/{1}/activities", botEndpoint, conversation.ConversationId);

            using (UnityWebRequest unityWebRequest1 = UnityWebRequest.Get(getActivityEndpoint))
            {
                unityWebRequest1.downloadHandler = new DownloadHandlerBuffer();
                unityWebRequest1.SetRequestHeader("Authorization", "Bearer " + botSecret);

                yield return unityWebRequest1.SendWebRequest();

                string jsonResponse = unityWebRequest1.downloadHandler.text;

                ActivitiesRootObject root = new ActivitiesRootObject();
                root = JsonConvert.DeserializeObject<ActivitiesRootObject>(jsonResponse);

                foreach (var act in root.activities)
                {
                    Debug.Log($"Bot Response: {act.text}");
                    SetBotResponseText(act.text);
                }

                botState = BotState.ReadyToListen;
                botMaterial.color = Color.blue;
            }
        } 
    ```

13. La dernière méthode à ajouter à cette classe est requise pour afficher le message dans la scène:

    ```csharp
        /// <summary>
        /// Set the UI Response Text of the bot
        /// </summary>
        internal void SetBotResponseText(string responseString)
        {        
            SceneOrganiser.Instance.botResponseText.text =  responseString;
        }
    ```

    > [!NOTE] 
    > Une erreur peut s’afficher dans la console de l’éditeur Unity, à propos de la classe **SceneOrganiser** manquante. Ignorez ce message, car vous allez créer cette classe ultérieurement dans le didacticiel.

14.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenirà Unity.

## <a name="chapter-11--create-the-interactions-class"></a>Chapitre 11: créer la classe interactions

La classe que vous allez créer maintenant est appelée **interactions**. Cette classe est utilisée pour détecter l’entrée de pression HoloLens de l’utilisateur. 

Si l’utilisateur appuie tout en regardant l’objet *bot* dans la scène, et que le bot est prêt à écouter les entrées vocales, l’objet bot change la couleur en **rouge** et commence à écouter les entrées vocales. 

Cette classe hérite de la classe **GazeInput** , et peut donc référencer la méthode **Start ()** et les variables de cette classe, dénotées par l’utilisation de **base**. 
 
Pour créer cette classe:

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir. 
2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**. Nommez les **interactions**de script. 
3.  Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.
4.  Mettez à jour les espaces de noms et l’héritage de la classe de façon à ce qu’ils soient identiques à ce qui suit, en haut de la classe **interactions** :

    ```csharp
    using UnityEngine.XR.WSA.Input;

    public class Interactions : GazeInput
    {
    ```

5.  À l’intérieur de la classe **interactions** , ajoutez la variable suivante:

    ```csharp
        /// <summary>
        /// Allows input recognition with the HoloLens
        /// </summary>
        private GestureRecognizer _gestureRecognizer;
    ```
6.  Ajoutez ensuite la méthode **Start ()** :

    ```csharp
        /// <summary>
        /// Called on initialization, after Awake
        /// </summary>
        internal override void Start()
        {
            base.Start();

            //Register the application to recognize HoloLens user inputs
            _gestureRecognizer = new GestureRecognizer();
            _gestureRecognizer.SetRecognizableGestures(GestureSettings.Tap);
            _gestureRecognizer.Tapped += GestureRecognizer_Tapped;
            _gestureRecognizer.StartCapturingGestures();
        }
    ```

7.  Ajoutez le gestionnaire qui sera déclenché lorsque l’utilisateur effectue le mouvement TAP devant l’appareil de caméra HoloLens.

    ```csharp
        /// <summary>
        /// Detects the User Tap Input
        /// </summary>
        private void GestureRecognizer_Tapped(TappedEventArgs obj)
        {
            // Ensure the bot is being gazed upon.
            if(base.FocusedObject != null)
            {
                // If the user is tapping on Bot and the Bot is ready to listen
                if (base.FocusedObject.name == "Bot" && Bot.Instance.botState == Bot.BotState.ReadyToListen)
                {
                    // If a conversation has not started yet, request one
                    if(Bot.Instance.conversationStarted)
                    {
                        Bot.Instance.SetBotResponseText("Listening...");
                        Bot.Instance.StartCapturingAudio();
                    }
                    else
                    {
                        Bot.Instance.SetBotResponseText("Requesting Conversation...");
                        StartCoroutine(Bot.Instance.StartConversation());
                    }                                  
                }
            }
        }
    ```

8. Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenirà Unity.

## <a name="chapter-12--create-the-sceneorganiser-class"></a>Chapitre 12: créer la classe SceneOrganiser

La dernière classe requise dans ce Lab est appelée **SceneOrganiser**. Cette classe configure la scène par programme, en ajoutant des composants et des scripts à l’appareil photo principal et en créant les objets appropriés dans la scène.
 
Pour créer cette classe:

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir. 
2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**. Nommez le script **SceneOrganiser**. 
3.  Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.
4.  À l’intérieur de la classe **SceneOrganiser** , ajoutez les variables suivantes:

    ```csharp
        /// <summary>
        /// Static instance of this class
        /// </summary>
        public static SceneOrganiser Instance;

        /// <summary>
        /// The 3D text representing the Bot response
        /// </summary>
        internal TextMesh botResponseText;
    ```

6.  Ajoutez ensuite les méthodes **éveillé ()** et **Start ()** :

    ```csharp
        /// <summary>
        /// Called on Initialization
        /// </summary>
        private void Awake()
        {
            Instance = this;
        }

        /// <summary>
        /// Called immediately after Awake method
        /// </summary>
        void Start ()
        {
            // Add the GazeInput class to this object
            gameObject.AddComponent<GazeInput>();

            // Add the Interactions class to this object
            gameObject.AddComponent<Interactions>();

            // Create the Bot in the scene
            CreateBotInScene();
        }
    ```

7.  Ajoutez la méthode suivante, responsable de la création de l’objet bot dans la scène et de la configuration des paramètres et des composants:

    ```csharp
        /// <summary>
        /// Create the Sign In button object in the scene
        /// and sets its properties
        /// </summary>
        private void CreateBotInScene()
        {
            GameObject botObjInScene = GameObject.CreatePrimitive(PrimitiveType.Sphere);
            botObjInScene.name = "Bot";
            
            // Add the Bot class to the Bot GameObject
            botObjInScene.AddComponent<Bot>();

            // Create the Bot UI
            botResponseText = CreateBotResponseText();

            // Set properties of Bot GameObject
            Bot.Instance.botMaterial = new Material(Shader.Find("Diffuse"));
            botObjInScene.GetComponent<Renderer>().material = Bot.Instance.botMaterial;
            Bot.Instance.botMaterial.color = Color.blue;
            botObjInScene.transform.position = new Vector3(0f, 2f, 10f);
            botObjInScene.tag = "BotTag";
        }
    ```

7.  Ajoutez la méthode suivante, chargée de créer l’objet d’interface utilisateur dans la scène, représentant les réponses du bot:

    ```csharp
        /// <summary>
        /// Spawns cursor for the Main Camera
        /// </summary>
        private TextMesh CreateBotResponseText()
        {
            // Create a sphere as new cursor
            GameObject textObject = new GameObject();
            textObject.transform.parent = Bot.Instance.transform;
            textObject.transform.localPosition = new Vector3(0,1,0);

            // Resize the new cursor
            textObject.transform.localScale = new Vector3(0.1f, 0.1f, 0.1f);

            // Creating the text of the Label
            TextMesh textMesh = textObject.AddComponent<TextMesh>();
            textMesh.anchor = TextAnchor.MiddleCenter;
            textMesh.alignment = TextAlignment.Center;
            textMesh.fontSize = 50;
            textMesh.text = "Hi there, tap on me and I will start listening.";
            
            return textMesh;
        }
    ```

8.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenirà Unity.
9.  Dans l’éditeur Unity, faites glisser le script **SceneOrganiser** du dossier scripts vers l’appareil photo principal. Le composant organisateur de scène doit maintenant apparaître sur l’objet caméra principal, comme illustré dans l’image ci-dessous.

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-37.png)

## <a name="chapter-13--before-building"></a>Chapitre 13 – avant la génération

Pour effectuer un test minutieux de votre application, vous devez l’chargement sur votre HoloLens.
Avant cela, assurez-vous que:

-   Tous les paramètres mentionnés dans le [**Chapitre 4**](#chapter-4--set-up-the-unity-project) sont correctement définis. 
-   Le script **SceneOrganiser** est attaché à l’objet **Camera principal** . 
-   Dans la classe **bot** , vérifiez que vous avez inséré la **clé secrète** de votre robot dans la variable **botSecret** .

## <a name="chapter-14--build-and-sideload-to-the-hololens"></a>Chapitre 14 – générer et chargement dans HoloLens

Tout ce qui est nécessaire pour la section Unity de ce projet est maintenant terminé. il est donc temps de la générer à partir d’Unity.

1.  Accédez à **paramètres de build**, **fichier > paramètres de Build.** ...
2.  Dans la fenêtre **paramètres de build** , cliquez sur **générer**.

    ![Génération de l’application à partir d’Unity](images/AzureLabs-Lab312-38.png)

3.  Si ce n’est pas déjà fait, les **projets C# Unity**.
4.  Cliquez sur **Build**. Unity lance une fenêtre de l' **Explorateur de fichiers** , dans laquelle vous devez créer, puis sélectionner un dossier dans lequel générer l’application. Créez ce dossier maintenant, puis nommez-le **application**. Ensuite, avec le dossier d' **application** sélectionné, cliquez sur **Sélectionner un dossier**. 
5.  Unity commence à générer votre projet dans le dossier de l' **application** . 
6.  Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).

## <a name="chapter-15--deploy-to-hololens"></a>Chapitre 15 – déployer dans HoloLens

Pour effectuer un déploiement sur HoloLens:

1.  Vous aurez besoin de l’adresse IP de votre HoloLens (pour le déploiement à distance) et vérifiez que votre HoloLens est en **mode développeur**. Pour ce faire :

    1. Tout en portant votre HoloLens, ouvrez les **paramètres**.
    2. Accéder au **réseau & Internet > Wi-Fi > options avancées**
    3. Notez l’adresse **IPv4** .
    4. Ensuite, revenez aux **paramètres**, puis à **mettre à jour & > de sécurité pour les développeurs** 
    5. Définissez le mode développeur sur.

2.  Accédez à votre nouvelle build Unity (le dossier de l' **application** ) et ouvrez le fichier solution avec **Visual Studio**.
3.  Dans la **configuration** de lasolution, sélectionnez Déboguer.
4.  Dans la **plateforme**de la solution, sélectionnez **x86**, **ordinateur distant**. 

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab312-39.png)
 
5.  Accédez au **menu Générer** , puis cliquez sur **déployer la solution**pour chargement l’application à votre HoloLens.
6.  Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prête à être lancée.

    > [!NOTE]
    > Pour effectuer un déploiement sur un casque immersif, définissez la plateforme de la **solution** sur *ordinateur local*et définissez la **configuration** sur déboguer, avec *x86* comme **plateforme**. Déployez ensuite sur l’ordinateur local, à l’aide du **menu Générer**, en sélectionnant *déployer la solution*. 

## <a name="chapter-16--using-the-application-on-the-hololens"></a>Chapitre 16 – utilisation de l’application sur HoloLens

- Une fois que vous avez lancé l’application, vous verrez le robot comme une sphère bleue devant vous.

- Utilisez le **geste TAP** lorsque vous êtes Gazing de la sphère pour lancer une conversation. 
 
- Attendez le démarrage de la conversation (l’interface utilisateur affichera un message lorsqu’elle se produit). Une fois que vous avez reçu le message d’introduction du bot, appuyez de nouveau sur le robot pour qu’il s’active et commence à écouter votre voix. 

- Une fois que vous arrêtez de parler, votre application envoie votre message au bot. vous recevrez rapidement une réponse qui s’affichera dans l’interface utilisateur. 

- Répétez le processus pour envoyer d’autres messages à votre bot (vous devez appuyer chaque fois que vous souhaitez envoyer un message).

Cette conversation démontre comment le bot peut conserver des informations (votre nom), tout en fournissant également des informations connues (telles que les éléments stockés).

#### <a name="some-questions-to-ask-the-bot"></a>Voici quelques questions à poser au robot:

```
what do you sell? 

how much are umbrellas?

how much are raincoats?
```

## <a name="your-finished-web-app-bot-v4-application"></a>Votre application Web App bot (v4) terminée

Félicitations, vous avez créé une application de réalité mixte qui s’appuie sur Azure Web App bot, Microsoft bot Framework v4.

![Produit final](images/AzureLabs-Lab312-00.png)

## <a name="bonus-exercises"></a>Exercices bonus

### <a name="exercise-1"></a>Exercice 1

La structure de la conversation dans ce laboratoire est très simple. Utilisez Microsoft LUIS pour offrir à vos robots des fonctionnalités de compréhension du langage naturel.

### <a name="exercise-2"></a>Exercice 2

Cet exemple n’inclut pas l’arrêt d’une conversation et le redémarrage d’une nouvelle conversation. Pour que la fonctionnalité bot soit terminée, essayez d’implémenter la fermeture de la conversation.
