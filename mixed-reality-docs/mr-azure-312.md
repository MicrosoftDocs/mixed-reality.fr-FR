---
title: MR et 312 Azure - intégration de robot
description: Terminer ce cours pour apprendre à créer et déployer un robot, à l’aide de Microsoft Bot Framework v4 et communiquer avec lui dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, vision par ordinateur, vr immersives, hololens, microsoft bot framework v4, robot d’application web, infrastructure de robot, bot de microsoft
ms.openlocfilehash: b828aa4415103d280459bd2c666004c994b3e59d
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597077"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

# <a name="mr-and-azure-312-bot-integration"></a>MR et Azure 312 : Intégration de robot

Dans ce cours, vous allez apprendre à créer et déployer un robot à l’aide de la V4 de Framework de Microsoft Bot et communiquer avec lui via une application Windows Mixed Reality. 

![](images/AzureLabs-Lab312-00.png)

Le **Microsoft Bot Framework V4** est un ensemble d’API est conçue pour fournir aux développeurs les outils nécessaires pour générer un bot évolutive et extensible application. Pour plus d’informations, visitez le [page Microsoft Bot Framework](https://dev.botframework.com/) ou [V4 Git référentiel](https://github.com/Microsoft/botbuilder-dotnet/wiki).

À l’issue de ce cours, vous aurez créé une application Windows Mixed Reality, qui sera en mesure d’effectuer les opérations suivantes :

1. Utilisez un **appuyez sur le mouvement** pour démarrer le robot à l’écoute de la voix d’utilisateurs.
2. Lorsque l’utilisateur dit quelque chose, le robot tente de fournir une réponse.
3. Afficher la réponse de robots sous forme de texte, positionné près du robot, dans la scène Unity.

Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception. Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity. Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> MR et Azure 312 : Intégration de robot</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Si ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques Windows Mixed Reality IMMERSIFS (VR). Étant donné que des casques IMMERSIFS (VR) ne sont pas accessibles caméras, vous devez une caméra externe connectée à votre PC. Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge des casques IMMERSIFS (VR).

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#. Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (juillet 2018). Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous.

Nous recommandons le matériel et logiciel pour ce cours suivants :

- Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)
- [Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé](install-the-tools.md#installation-checklist)
- [Le SDK Windows 10 dernières](install-the-tools.md#installation-checklist)
- [Unity 2017.4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé
- L’accès à Internet pour Azure et pour l’extraction de robot de Azure. Pour plus d’informations, [, suivez ce lien](https://dev.botframework.com/).

### <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).
2.  Configurer et tester votre HoloLens. Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup). 
3.  Il est judicieux d’effectuer l’étalonnage et le réglage de capteur lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur). 

Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).

Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).

## <a name="chapter-1--create-the-bot-application"></a>Chapitre 1 – créer l’application Bot

La première étape consiste à créer votre robot en tant qu’une application Web ASP.Net Core locale. Une fois que vous avez terminé et testé, vous allez le publier sur le portail Azure.

1.  Ouvrez Visual Studio. Créez un projet, sélectionnez **ASP NET Core Web Application** comme type de projet (vous trouverez sous la sous-section .NET Core) et appelez-le **MyBot**. Cliquez sur **OK**.

2.  Dans la fenêtre qui s’affiche sélectionnez **vide**. Également Assurez-vous que la cible est définie sur **ASP NET Core 2.0** et l’authentification est définie sur **aucune authentification**. Cliquez sur **OK**.  

    ![Créer l’application bot](images/AzureLabs-Lab312-01.png)

3.  La solution s’ouvre. Avec le bouton droit sur la Solution **Mybot** dans le **l’Explorateur de solutions** , puis cliquez sur **gérer les Packages NuGet pour la Solution**. 

    ![Créer l’application Bot](images/AzureLabs-Lab312-02.png)

4.  Dans le **Parcourir** onglet, recherchez **Microsoft.Bot.Builder.Integration.AspNet.Core** (Vérifiez que vous avez **inclure la version préliminaire** activée). Sélectionnez la version du package **4.0.1-preview**et cochez les cases du projet. Cliquez ensuite sur **installer**. Vous avez installé les bibliothèques nécessaires pour le **Bot Framework v4**. Fermez la page NuGet.

    ![Créer l’application bot](images/AzureLabs-Lab312-03.png)

5.  Avec le bouton droit sur votre *projet*, **MyBot**, dans le **l’Explorateur de solutions** , puis cliquez sur **ajouter** **|** **Classe**.

    ![Créer l’application Bot](images/AzureLabs-Lab312-04.png)

6.  Nommez la classe **MyBot** , puis cliquez sur **ajouter**.

    ![Créer l’application bot](images/AzureLabs-Lab312-05.png)

7.  Répétez le point précédent, pour créer une autre classe nommée **ConversationContext**. 

8.  Avec le bouton droit sur **wwwroot** dans le **l’Explorateur de solutions** , puis cliquez sur **ajouter** **|** **unnouvelélément**. Sélectionnez **HTML Page** (vous trouverez sous la sous-section Web). Nommez le fichier **default.html**. Cliquez sur **Ajouter**.

    ![Créer l’application bot](images/AzureLabs-Lab312-06.png)

9.  La liste des classes / objets dans le **l’Explorateur de solutions** doit ressembler à l’image ci-dessous.

    ![Créer l’application bot](images/AzureLabs-Lab312-07.png)

10. Double-cliquez sur le **ConversationContext** classe. Cette classe est chargée de conserver les variables utilisées par le robot de conserver le contexte de la conversation. Ces valeurs de contexte de conversation sont conservées dans une instance de cette classe, car n’importe quelle instance de la **MyBot** classe sera actualisée à chaque fois qu’une activité est reçue. Ajoutez le code suivant à la classe :

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

11. Double-cliquez sur le **MyBot** classe. Cette classe héberge les gestionnaires appelées par n’importe quelle activité entrante du client. Dans cette classe, vous ajouterez le code utilisé pour créer la conversation entre le robot et le client. Comme mentionné précédemment, une instance de cette classe est initialisée chaque fois qu’une activité est reçue. Ajoutez le code suivant à cette classe :

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

12. Double-cliquez sur le **démarrage** classe. Cette classe initialisera le robot. Ajoutez le code suivant à la classe :

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

13. Ouvrez le **programme** fichier de classe et de vérifier le code qu’il contient est identique à ce qui suit :

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

14. N’oubliez pas d’enregistrer vos modifications, pour ce faire, accédez à **fichier** > **Enregistrer tout**, à partir de la barre d’outils en haut de Visual Studio.

## <a name="chapter-2---create-the-azure-bot-service"></a>Chapitre 2 : créer le Service de robot Azure

Maintenant que vous avez généré le code pour votre bot, vous devez le publier sur une instance de la *Web App Bot* Service, sur le portail Azure. Ce chapitre sera vous montrer comment créer et configurer le Service de robot sur Azure et puis publiez votre code à ce dernier.

1.  Tout d’abord, connectez-vous au portail Azure (https://portal.azure.com). 

    1. Si vous n’avez pas déjà un compte Azure, vous devrez créer un. Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **créer une ressource** dans le coin supérieur gauche coin inférieur droit, puis recherchez *Web App bot*, puis cliquez sur **entrée**.

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-08.png)
 
3.  La nouvelle page doit fournir une description de la *Web App Bot* Service. En bas à gauche de cette page, sélectionnez le **créer** bouton, pour créer une association avec ce Service.

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-09.png)
 
4.  Une fois que vous avez cliqué sur **créer**:

    1. Insérez votre souhaitée **nom** pour cette instance de Service.
    2. Sélectionnez un **abonnement**.
    3. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, [, suivez ce lien](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)

    4. Déterminer l’emplacement de votre groupe de ressources (si vous créez un nouveau groupe de ressources). Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute. Certaines ressources Azure sont uniquement disponibles dans certaines régions.
    5. Sélectionnez le **niveau tarifaire** appropriés pour vous, s’il s’agit du premier temps à créer un *Web App Bot* Service, un niveau gratuit (nommé F0) doit être disponible pour vous
    6. **Nom de l’application** peut simplement rester le même que le *nom du robot*. 
    7. Laissez le *modèle de robot* comme **base (C#)**.
    8. *Plan/emplacement app service* aurait dû être renseignées automatiquement pour votre compte.
    9. Définir le **stockage Azure** que vous souhaitez utiliser pour héberger votre robot. Si vous n’en avez pas, vous pouvez le créer ici.
    10. Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.
    11. Cliquez sur Créer.
 
        ![Créer le Service de robot Azure](images/AzureLabs-Lab312-10.png)

5.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le Service doit être créé, cette opération peut prendre une minute.

6.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-11.png) 
 
7.  Cliquez sur la notification pour Explorer votre nouvelle instance de Service. 

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-12.png)
 
8. Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service. Vous êtes redirigé vers votre nouvelle instance de Service Azure. 

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-13.png)
 
9.  À ce stade, vous devez configurer une fonctionnalité appelée **par ligne directe** pour autoriser votre application cliente communiquer avec ce Service de robot. Cliquez sur **canaux**, puis dans le **ajouter un canal proposé** section, cliquez sur **canal de configurer par ligne directe**.

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-14.png)

10. Dans cette page, vous trouverez le **clés secrètes** qui permettra à votre application cliente pour s’authentifier auprès du robot. Cliquez sur le **afficher** bouton et effectuez une copie de l’une des clés affichées, car vous en aurez besoin plus loin dans votre projet. 

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-15.png)

## <a name="chapter-3--publish-the-bot-to-the-azure-web-app-bot-service"></a>Chapitre 3 : publier le Bot sur le Service de robot d’application Web Azure

Maintenant que votre Service est prêt, vous devez publier votre code de robot, que vous avez créée précédemment, à votre serveur Web App Bot Service nouvellement créé.

> [!NOTE] 
> Vous devrez publier votre robot au Service Azure chaque fois que vous apportez des modifications à la solution Bot / code.

1.  Revenez à votre Solution Visual Studio que vous avez créé précédemment. 
2.  Avec le bouton droit sur votre **MyBot** de projet, dans le **l’Explorateur de solutions**, puis cliquez sur **publier**.

    ![Publier le Bot sur le Service de robot d’application Web Azure](images/AzureLabs-Lab312-16.png)

3.  Sur le *choisir une cible de publication* , cliquez sur **App Service**, puis **sélectionner**, enfin cliquez sur **créer un profil** (vous devrez peut-être Cliquez sur la flèche déroulante en même temps que le *publier* bouton, si cela n’est pas visible).

    ![Publier le Bot sur le Service de robot d’application Web Azure](images/AzureLabs-Lab312-17.png)

4. Si vous n’êtes pas encore connecté à votre Account Microsoft, vous devez le faire ici.
5. Sur le **publier** vous trouverez que vous devez définir le même **abonnement** que vous avez utilisé pour le *Web App Bot* la création du Service. Définissez ensuite la **vue** en tant que **groupe de ressources** et, dans la liste déroulante la structure de dossiers, sélectionnez le **groupe de ressources** que vous avez créé précédemment. Cliquez sur **OK**. 

    ![Publier le Bot sur le Service de robot d’application Web Azure](images/AzureLabs-Lab312-18.png)

6.  Cliquez maintenant sur le **publier** bouton et attendez que le robot à publier (il peut prendre quelques minutes).

    ![Publier le Bot sur le Service de robot d’application Web Azure](images/AzureLabs-Lab312-19.png)


## <a name="chapter-4--set-up-the-unity-project"></a>Chapitre 4 : configurer le projet Unity

Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **New**. 

    ![Configurer le projet Unity](images/AzureLabs-Lab312-20.png)

2.  Maintenant, vous devez fournir un nom de projet Unity. Insérer **Hololens Bot**. Assurez-vous que le modèle de projet est défini sur **3D**. Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![Configurer le projet Unity](images/AzureLabs-Lab312-21.png)

3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Accédez à **Modifier > Préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

    ![Configurer le projet Unity](images/AzureLabs-Lab312-22.png)

4.  Ensuite, accédez à **fichier > Paramètres de Build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le **plateforme de commutation** bouton pour appliquer votre sélection.

    ![Configurer le projet Unity](images/AzureLabs-Lab312-23.png)

5.  Lorsque vous êtes toujours dans **fichier > Paramètres de Build** et vous assurer que :

    1.  **Équipement cible** a la valeur **Hololens**

        > Pour des casques IMMERSIFS, définissez **appareil cible** à *n’importe quel appareil*.

    2.  **Type de build** a la valeur **D3D**

    3.  **Kit de développement logiciel** a la valeur **dernière installé**

    4.  **Version de Visual Studio** a la valeur **dernière installé**

    5.  **Générez et exécutez** est défini sur **ordinateur Local**

    6.  Enregistrer la scène et l’ajouter à la build. 

        1. Cela en sélectionnant **ajouter un arrière-plan Open**. Une fenêtre d’enregistrement s’affiche.
        
            ![Configurer le projet Unity](images/AzureLabs-Lab312-24.png)

        2. Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.

             ![Configurer le projet Unity](images/AzureLabs-Lab312-25.png)

        3. Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier*: champ de texte, tapez **BotScene**, puis cliquez sur **enregistrer**.

            ![Configurer le projet Unity](images/AzureLabs-Lab312-26.png)

    7. Les autres paramètres, dans **paramètres de Build**, doit être conservé comme valeur par défaut pour l’instant.

6. Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve. 

    ![Configurer le projet Unity](images/AzureLabs-Lab312-27.png)

7. Dans ce panneau, quelques paramètres doivent être vérifiées :

    1. Dans le **autres paramètres** onglet :

        1. **Version du Runtime de script** doit être **expérimental (NET 4.6 équivalent)**; cette modification nécessite un redémarrage de l’éditeur.
        2. **Script principal** doit être **.NET**
        3. **Niveau de compatibilité d’API** doit être **.NET 4.6**

            ![Configurer le projet Unity](images/AzureLabs-Lab312-28.png)
      
    2. Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :

        - **InternetClient**
        - **Microphone**

            ![Configurer le projet Unity](images/AzureLabs-Lab312-29.png)

    3. Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.

        ![Configurer le projet Unity](images/AzureLabs-Lab312-30.png)

8.  Dans *paramètres de Build* _Unity C#_  projets est n’est plus grisée ; Cochez la case à cocher en regard de cela. 
9.  Fermez la fenêtre Paramètres de Build.
10. Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).


## <a name="chapter-5--camera-setup"></a>Chapitre 5 – programme d’installation de l’appareil photo

> [!IMPORTANT]
> Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [Azure-MR-312-Package.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20312%20-%20Bot%20integration/Azure-MR-312.unitypackage), importez-le dans votre projet sous la forme d’un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 7](#chapter-7-–-create-the-botobjects-class).

1.  Dans le *Panneau de la hiérarchie*, sélectionnez le **Main Camera**. 
2.  Une fois sélectionné, vous serez en mesure de voir tous les composants de la **Main Camera** dans le *panneau Inspecteur*.

    1. Le **objet caméra** doit être nommé **Main Camera** (Notez l’orthographe)
    2. La caméra principale **balise** doit être définie sur **MainCamera** (Notez l’orthographe)
    3. Assurez-vous que le **Position transformer** a la valeur **0, 0, 0**
    4. Définissez **d’effacer les indicateurs** à **couleur unie**.
    5. Définir le **arrière-plan** couleur du composant de caméra à **noir, Alpha 0 (Hex Code : #00000000)**

    ![le programme d’installation de la caméra](images/AzureLabs-Lab312-31.png)
 

## <a name="chapter-6--import-the-newtonsoft-library"></a>Chapitre 6 – importer la bibliothèque Newtonsoft

Pour vous aider à désérialiser et sérialiser des objets reçus et envoyés au Service Bot, vous devez télécharger le **Newtonsoft** bibliothèque. Vous trouverez un [version compatible déjà organisée avec la structure de dossiers Unity correcte ici](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20312%20-%20Bot%20integration/NewtonsoftDLL.unitypackage). 

Pour importer la bibliothèque Newtonsoft dans votre projet, utilisez le Package Unity qui accompagne ce cours.

1.  Ajouter le *.unitypackage* à Unity à l’aide de la **actifs** > **importer un Package** > **Package personnalisé** option de menu.

    ![Importer la bibliothèque Newtonsoft](images/AzureLabs-Lab312-34.png)

2.  Dans le **importer un Package Unity** emballer qui apparaît, vérifiez tous les éléments sous (y compris) **plug-ins** est sélectionné.

    ![Importer la bibliothèque Newtonsoft](images/AzureLabs-Lab312-35.png)

3.  Cliquez sur le **importation** pour ajouter les éléments à votre projet.

4.  Accédez à la **Newtonsoft** dossier sous **plug-ins** dans la vue de projet et sélectionnez le plug-in Newtonsoft.

    ![](images/AzureLabs-Lab312-35b.png)

5.  Avec le plug-in Newtonsoft sélectionné, vérifiez que **plateforme Any** est **unchecked**, puis assurez-vous que **WSAPlayer** est également **unchecked**, puis cliquez sur **appliquer**. Il s’agit juste pour confirmer que les fichiers sont correctement configurés.

    ![](images/AzureLabs-Lab312-35c.png)

    > [!NOTE]
    > Marquage de ces plug-ins les configure uniquement à être utilisé dans l’éditeur Unity. Il existe un ensemble différent d’eux dans le dossier WSA qui sera utilisé une fois que le projet est exporté à partir d’Unity.

6.  Ensuite, vous devez ouvrir le **WSA** dossier, en respectant le **Newtonsoft** dossier. Vous verrez une copie du même fichier que vous venez de configurer. Sélectionnez le fichier et dans l’inspecteur, vérifiez que
    -   **N’importe quelle plateforme** est **non contrôlé** 
    -   **uniquement** **WSAPlayer** est **activée**
    -   **Ne pas traiter les** est **activée**

    ![](images/AzureLabs-Lab312-35d.png)

## <a name="chapter-7--create-the-bottag"></a>Chapitre 7 – créer la BotTag

1.  Créer un nouveau **balise** objet appelé **BotTag**. Sélectionnez la caméra principale dans la scène. Cliquez sur la balise de liste déroulante menu dans le panneau de l’inspecteur. Cliquez sur **ajouter une balise**.

    ![le programme d’installation de la caméra](images/AzureLabs-Lab312-32.png)
 
2.  Cliquez sur le **+** symbole. Nommez le nouveau **balise** comme **BotTag**, *enregistrer*.

    ![le programme d’installation de la caméra](images/AzureLabs-Lab312-33.png)

> [!WARNING] 
> **Ne le faites pas** appliquer le **BotTag** à la caméra principale. Si vous avez accidentellement fait, veillez à modifier la balise au Main Camera *MainCamera*.

## <a name="chapter-8--create-the-botobjects-class"></a>Chapitre 8 : créer la classe BotObjects

Est le premier script que vous avez besoin pour créer le **BotObjects** (classe), qui est une classe vide créé afin qu’une série d’autres objets de classe permettre être stockée dans le même script et accessible par d’autres scripts dans la scène.

La création de cette classe est purement un choix architecturaux, ces objets au lieu de cela peuvent être hébergés dans le script Bot que vous créerez plus loin dans ce cours.

Pour créer cette classe : 

1.  Avec le bouton droit dans le *panneau projet*, puis **créer > dossier**. Nommez le dossier **Scripts**. 

    ![Créez le dossier scripts.](images/AzureLabs-Lab312-36.png)

2.  Double-cliquez sur le **Scripts** dossier pour l’ouvrir. Ensuite, dans ce dossier, avec le bouton droit, puis sélectionnez **créer > C# Script**. Nommez le script **BotObjects**. 

3.  Double-cliquez sur le nouveau **BotObjects** script pour l’ouvrir avec **Visual Studio**.

4.  Supprimer le contenu du script et remplacez-le par le code suivant :

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

6.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-9--create-the-gazeinput-class"></a>Chapitre 9 – créer la classe GazeInput

La classe suivante, vous allez créer est la **GazeInput** classe. Cette classe est chargée de :

- Création d’un curseur qui représentera le *les regards* du lecteur.
- Détection d’objets atteint par le regard du lecteur et contenant une référence aux objets détectés.

Pour créer cette classe : 

1.  Accédez à la **Scripts** dossier que vous avez créé précédemment. 
2.  Avec le bouton droit dans le dossier, **créer > C# Script**. Appeler le script **GazeInput**. 
3.  Double-cliquez sur le nouveau **GazeInput** script pour l’ouvrir avec **Visual Studio**.
4.  Insérez la ligne suivante juste au-dessus du nom de classe :

    ```csharp
    /// <summary>
    /// Class responsible for the User's gaze interactions
    /// </summary>
    [System.Serializable]
    public class GazeInput : MonoBehaviour
    ```

5.  Puis ajoutez les variables suivantes à l’intérieur de la **GazeInput** classe ci-dessus le **Start()** méthode :

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

6.  Code pour **Start()** méthode doit être ajoutée. Celui-ci sera appelé lors de l’initialisation de la classe :

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

7.  Implémentez une méthode qui instancie et configurer le curseur du pointage de regard : 

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

8.  Implémenter les méthodes qui vous permettront de configurer le Raycast à partir de la caméra principale et de seront assurer le suivi de l’objet ayant le focus actuel.

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
 
9.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-10--create-the-bot-class"></a>Chapitre 10 – créer la classe Bot

Le script que vous vous apprêtez à créer est maintenant appelé **Bot**. Il s’agit de la classe principale de votre application, il stocke : 

- Vos informations d’identification de Web App Bot
- La méthode qui collecte les commandes de voix utilisateur
- La méthode nécessaire pour lancer des conversations avec votre robot d’application Web 
- La méthode nécessaire pour envoyer des messages à votre robot d’application Web 

Pour envoyer des messages au Service Bot, la **SendMessageToBot()** coroutine générera une activité, qui est un objet reconnu par l’infrastructure de robot en tant que données envoyées par l’utilisateur. 
 
Pour créer cette classe : 

1. Double-cliquez sur le **Scripts** dossier, pour l’ouvrir. 
2. Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**. Nommez le script **Bot**. 
3. Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.
4. Mettre à jour les espaces de noms pour être le même que la commande suivante, en haut de la **Bot** classe :

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.Text;
    using UnityEngine;
    using UnityEngine.Networking;
    using UnityEngine.Windows.Speech;
    ```
 
5. À l’intérieur de la **Bot** classe ajoutez les variables suivantes :

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
    > Assurez-vous que vous insérez votre **clé secrète de robot** dans le **botSecret** variable. Avoir noté votre **clé secrète de robot** au début de ce cours, dans  **[chapitre 2](#chapter-2---create-the-azure-bot-service), étape 10**.

7. Code pour **Awake()** et **Start()** doit maintenant être ajouté. 

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

8. Ajoutez les deux gestionnaires sont appelés par les bibliothèques de reconnaissance vocale lors de la capture de la voix commence et se termine. Le *DictationRecognizer* arrête automatiquement la capture de la voix de l’utilisateur lorsque l’utilisateur arrête de parler.

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

1. Le gestionnaire suivant collecte le résultat de l’entrée de voix utilisateur et appelle la coroutine chargé d’envoyer le message au Service Web App Bot.

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

10. La coroutine suivante est appelée pour commencer une conversation avec le robot. Vous remarquerez qu’une fois que l’appel de la conversation est terminée, elle peut appeler le **SendMessageToCoroutine()** en passant d’une série de paramètres qui définira l’activité à envoyer au Service de robot en tant qu’un message vide. Pour cela, pour demander le Service de robot pour lancer la boîte de dialogue.

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

11. La coroutine suivante est appelée pour générer l’activité à envoyer au Service de robot. 

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

12. La coroutine suivante est appelée pour demander une réponse après l’envoi d’une activité pour le Service de robot. 

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

13. La dernière méthode à ajouter à cette classe, est requis pour afficher le message dans la scène :

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
    > Vous pouvez rencontrer une erreur dans la Console de l’éditeur Unity, manquants le **SceneOrganiser** classe. Ignorez ce message, comme vous allez créer cette classe plus loin dans le didacticiel.

14.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-11--create-the-interactions-class"></a>Chapitre 11 – créer la classe d’Interactions

La classe que vous vous apprêtez à créer est maintenant appelée **Interactions**. Cette classe est utilisée pour détecter l’entrée appuyez sur HoloLens à partir de l’utilisateur. 

Si l’utilisateur appuie sur tout en gardant le *Bot* objet dans la scène et le robot est prêt à l’écoute des entrées de la voix, l’objet Bot change de couleur pour **rouge** et commencer à écouter les entrées de la voix. 

Cette classe hérite de la **GazeInput** classe et peut faire référence à la **Start()** (méthode) et les variables à partir de cette classe, indiqué par l’utilisation de **base**. 
 
Pour créer cette classe :

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir. 
2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**. Nommez le script **Interactions**. 
3.  Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.
4.  Mettre à jour les espaces de noms et l’héritage de classe pour être le même que la commande suivante, en haut de la **Interactions** classe :

    ```csharp
    using UnityEngine.XR.WSA.Input;

    public class Interactions : GazeInput
    {
    ```

5.  À l’intérieur de la **Interactions** classe ajoutez la variable suivante :

    ```csharp
        /// <summary>
        /// Allows input recognition with the HoloLens
        /// </summary>
        private GestureRecognizer _gestureRecognizer;
    ```
6.  Ajoutez ensuite le **Start()** méthode :

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

7.  Ajoutez le gestionnaire qui est déclenché lorsque l’utilisateur effectue le geste d’appui devant la caméra HoloLens

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

8. Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-12--create-the-sceneorganiser-class"></a>Chapitre 12 – créer la classe SceneOrganiser

La dernière classe requise dans ce laboratoire est appelée **SceneOrganiser**. Cette classe est le programme d’installation la scène par programmation, en ajoutant des composants et des scripts à la caméra principale et en créant les objets appropriés dans la scène.
 
Pour créer cette classe :

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir. 
2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**. Nommez le script **SceneOrganiser**. 
3.  Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.
4.  À l’intérieur de la **SceneOrganiser** classe ajoutez les variables suivantes :

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

6.  Ajoutez ensuite le **Awake()** et **Start()** méthodes :

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

7.  Ajoutez la méthode suivante, responsable de la création de l’objet de Bot dans la scène et en définissant des paramètres et des composants :

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

7.  Ajoutez la méthode suivante, responsable de la création de l’objet de l’interface utilisateur dans la scène, représentant les réponses à partir du robot :

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

8.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.
9.  Dans l’éditeur Unity, faites glisser le **SceneOrganiser** script à partir du dossier Scripts à la caméra principale. Le composant d’un gestionnaire de scène doit maintenant apparaître sur l’objet Main Camera, comme illustré dans l’image ci-dessous.

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-37.png)

## <a name="chapter-13--before-building"></a>Chapitre 13 – avant la génération

Pour effectuer une analyse minutieuse de votre application vous en aurez besoin pour effectuer un chargement indépendant sur votre HoloLens.
Avant de procéder, assurez-vous que :

-   Tous les paramètres mentionnés dans le [ **chapitre 4** ](#Chapter-4-–-Set-up-the-unity-project) sont correctement définies. 
-   Le script **SceneOrganiser** est attaché à la **Main Camera** objet. 
-   Dans le **Bot** class, assurez-vous que vous avez inséré votre **clé secrète de robot** dans le **botSecret** variable.

## <a name="chapter-14--build-and-sideload-to-the-hololens"></a>Chapitre 14 – Build et chargement de version test pour le HoloLens

Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée, il est temps de générer à partir de Unity.

1.  Accédez à **les paramètres de génération**, **fichier > Paramètres de Build...** .
2.  À partir de la **paramètres de Build** fenêtre, cliquez sur **Build**.

    ![Création de l’application à partir d’Unity](images/AzureLabs-Lab312-38.png)

3.  Si pas déjà fait, cochez **Unity C# projets**.
4.  Cliquez sur **Build**. Unity lancera un **Explorateur de fichiers** fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans. Créez ce dossier, puis nommez-le **application**. Ensuite avec le **application** dossier sélectionné, cliquez sur **sélectionner le dossier**. 
5.  Unity commencera à générer votre projet pour le **application** dossier. 
6.  Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un **Explorateur de fichiers** fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).

## <a name="chapter-15--deploy-to-hololens"></a>Chapitre 15 – déployer sur HoloLens

Pour déployer sur HoloLens :

1.  Vous devez l’adresse IP de votre HoloLens (pour les déployer à distance) et pour vérifier que votre HoloLens est dans **Mode développeur**. Pour ce faire :

    1. Tout en portant vos HoloLens, ouvrez le **paramètres**.
    2. Accédez à **réseau & Internet > Wi-Fi > Options avancées**
    3. Remarque la **IPv4** adresse.
    4. Ensuite, accédez à **paramètres**, puis à **mise à jour & sécurité > pour les développeurs** 
    5. Définir le Mode développeur.

2.  Accédez à votre nouvelle build Unity (le **application** dossier) et ouvrez le fichier solution avec **Visual Studio**.
3.  Dans le **Configuration de la Solution** sélectionnez **déboguer**.
4.  Dans le **plateforme de Solution**, sélectionnez **x86**, **Machine distante**. 

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab312-39.png)
 
5.  Accédez à la **menu Générer** , puis cliquez sur **déployer la Solution**, chargement de version test l’application à votre HoloLens.
6.  Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prêt à être lancé !

    > [!NOTE]
    > Pour déployer sur casque immersif, définissez le **plateforme de Solution** à *ordinateur Local*et définissez le **Configuration** à *déboguer*, avec *x86* en tant que le **plateforme**. Déployer sur l’ordinateur local d’ordinateur, à l’aide de la **menu Générer**, en sélectionnant *déployer la Solution*. 

## <a name="chapter-16--using-the-application-on-the-hololens"></a>Chapitre 16 – à l’aide de l’application sur le HoloLens

- Une fois que vous avez lancé l’application, vous verrez le robot en tant qu’une sphère bleu devant vous.

- Utilisez le **appuyez sur le mouvement** pendant que vous sont gazing à la sphère pour engager une conversation. 
 
- Attendez que la conversation Démarrer (l’interface utilisateur affiche un message lorsque cela se produit). Une fois que vous recevez le message de présentation à partir du robot, appuyez à nouveau sur le Bot afin qu’il sera en rouge et commence à écouter votre voix. 

- Une fois que vous arrêtez de parler, votre application enverra votre message au robot et vous recevrez rapidement une réponse qui sera affichée dans l’interface utilisateur. 

- Répétez le processus pour envoyer plusieurs messages à votre robot (vous devez appuyer sur chaque fois que vous souhaitez envoyer un message).

Cette conversation montre comment le robot puisse conserver des informations (votre nom), tout en fournissant également des informations connues (par exemple, les éléments qui sont stockés).

#### <a name="some-questions-to-ask-the-bot"></a>Certaines questions à poser au robot :

```
what do you sell? 

how much are umbrellas?

how much are raincoats?
```

## <a name="your-finished-web-app-bot-v4-application"></a>Votre application Web App Bot (v4) terminée

Félicitations, vous avez créé une application de réalité mixte qui met à profit les Azure Web App Bot v4 de Microsoft Bot Framework.

![Produit final](images/AzureLabs-Lab312-00.png)

## <a name="bonus-exercises"></a>Exercices de bonus

### <a name="exercise-1"></a>Exercice 1

La structure de la conversation dans cet atelier est très simple. Utilisez Microsoft LUIS pour donner à votre robot de fonctionnalités de compréhension du langage naturel.

### <a name="exercise-2"></a>Exercice 2

Cet exemple n’inclut pas une conversation de fin d’exécution et le redémarrage d’un autre. Pour rendre la fonctionnalité Bot terminées, essayez d’implémenter de fermeture à la conversation.
