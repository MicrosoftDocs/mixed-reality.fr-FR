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
><span data-ttu-id="db734-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="db734-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="db734-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="db734-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="db734-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="db734-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="db734-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="db734-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="db734-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="db734-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="db734-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="db734-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

# <a name="mr-and-azure-312-bot-integration"></a><span data-ttu-id="db734-110">MR et Azure 312 : Intégration de robot</span><span class="sxs-lookup"><span data-stu-id="db734-110">MR and Azure 312: Bot integration</span></span>

<span data-ttu-id="db734-111">Dans ce cours, vous allez apprendre à créer et déployer un robot à l’aide de la V4 de Framework de Microsoft Bot et communiquer avec lui via une application Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="db734-111">In this course, you will learn how to create and deploy a bot using the Microsoft Bot Framework V4 and communicate with it through a Windows Mixed Reality application.</span></span> 

![](images/AzureLabs-Lab312-00.png)

<span data-ttu-id="db734-112">Le **Microsoft Bot Framework V4** est un ensemble d’API est conçue pour fournir aux développeurs les outils nécessaires pour générer un bot évolutive et extensible application.</span><span class="sxs-lookup"><span data-stu-id="db734-112">The **Microsoft Bot Framework V4** is a set of APIs designed to provide developers with the tools to build an extensible and scalable bot application.</span></span> <span data-ttu-id="db734-113">Pour plus d’informations, visitez le [page Microsoft Bot Framework](https://dev.botframework.com/) ou [V4 Git référentiel](https://github.com/Microsoft/botbuilder-dotnet/wiki).</span><span class="sxs-lookup"><span data-stu-id="db734-113">For more information, visit the [Microsoft Bot Framework page](https://dev.botframework.com/) or the [V4 Git Repository](https://github.com/Microsoft/botbuilder-dotnet/wiki).</span></span>

<span data-ttu-id="db734-114">À l’issue de ce cours, vous aurez créé une application Windows Mixed Reality, qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="db734-114">After completing this course, you will have built a Windows Mixed Reality application, which will be able to do the following:</span></span>

1. <span data-ttu-id="db734-115">Utilisez un **appuyez sur le mouvement** pour démarrer le robot à l’écoute de la voix d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="db734-115">Use a **Tap Gesture** to start the bot listening for the users voice.</span></span>
2. <span data-ttu-id="db734-116">Lorsque l’utilisateur dit quelque chose, le robot tente de fournir une réponse.</span><span class="sxs-lookup"><span data-stu-id="db734-116">When the user has said something, the bot will attempt to provide a response.</span></span>
3. <span data-ttu-id="db734-117">Afficher la réponse de robots sous forme de texte, positionné près du robot, dans la scène Unity.</span><span class="sxs-lookup"><span data-stu-id="db734-117">Display the bots reply as text, positioned near the bot, in the Unity Scene.</span></span>

<span data-ttu-id="db734-118">Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception.</span><span class="sxs-lookup"><span data-stu-id="db734-118">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="db734-119">Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="db734-119">This course is designed to teach you how to integrate an Azure Service with your Unity project.</span></span> <span data-ttu-id="db734-120">Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="db734-120">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

## <a name="device-support"></a><span data-ttu-id="db734-121">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="db734-121">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="db734-122">Cours</span><span class="sxs-lookup"><span data-stu-id="db734-122">Course</span></span></th><th style="width:150px"> <span data-ttu-id="db734-123"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="db734-123"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="db734-124"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="db734-124"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="db734-125">MR et Azure 312 : Intégration de robot</span><span class="sxs-lookup"><span data-stu-id="db734-125">MR and Azure 312: Bot integration</span></span></td><td style="text-align: center;"> <span data-ttu-id="db734-126">✔️</span><span class="sxs-lookup"><span data-stu-id="db734-126">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="db734-127">✔️</span><span class="sxs-lookup"><span data-stu-id="db734-127">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="db734-128">Si ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques Windows Mixed Reality IMMERSIFS (VR).</span><span class="sxs-lookup"><span data-stu-id="db734-128">While this course primarily focuses on HoloLens, you can also apply what you learn in this course to Windows Mixed Reality immersive (VR) headsets.</span></span> <span data-ttu-id="db734-129">Étant donné que des casques IMMERSIFS (VR) ne sont pas accessibles caméras, vous devez une caméra externe connectée à votre PC.</span><span class="sxs-lookup"><span data-stu-id="db734-129">Because immersive (VR) headsets do not have accessible cameras, you will need an external camera connected to your PC.</span></span> <span data-ttu-id="db734-130">Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge des casques IMMERSIFS (VR).</span><span class="sxs-lookup"><span data-stu-id="db734-130">As you follow along with the course, you will see notes on any changes you might need to employ to support immersive (VR) headsets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db734-131">Prérequis</span><span class="sxs-lookup"><span data-stu-id="db734-131">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="db734-132">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="db734-132">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="db734-133">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (juillet 2018).</span><span class="sxs-lookup"><span data-stu-id="db734-133">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (July 2018).</span></span> <span data-ttu-id="db734-134">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="db734-134">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you will find in newer software than what is listed below.</span></span>

<span data-ttu-id="db734-135">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="db734-135">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="db734-136">Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)</span><span class="sxs-lookup"><span data-stu-id="db734-136">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="db734-137">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="db734-137">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="db734-138">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="db734-138">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="db734-139">Unity 2017.4</span><span class="sxs-lookup"><span data-stu-id="db734-139">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="db734-140">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="db734-140">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="db734-141">Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="db734-141">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="db734-142">L’accès à Internet pour Azure et pour l’extraction de robot de Azure.</span><span class="sxs-lookup"><span data-stu-id="db734-142">Internet access for Azure, and for Azure Bot retrieval.</span></span> <span data-ttu-id="db734-143">Pour plus d’informations, [, suivez ce lien](https://dev.botframework.com/).</span><span class="sxs-lookup"><span data-stu-id="db734-143">For more information, [please follow this link](https://dev.botframework.com/).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="db734-144">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="db734-144">Before you start</span></span>

1.  <span data-ttu-id="db734-145">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="db734-145">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="db734-146">Configurer et tester votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="db734-146">Set up and test your HoloLens.</span></span> <span data-ttu-id="db734-147">Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="db734-147">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span> 
3.  <span data-ttu-id="db734-148">Il est judicieux d’effectuer l’étalonnage et le réglage de capteur lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="db734-148">It is a good idea to perform Calibration and Sensor Tuning when beginning developing a new HoloLens app (sometimes it can help to perform those tasks for each user).</span></span> 

<span data-ttu-id="db734-149">Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).</span><span class="sxs-lookup"><span data-stu-id="db734-149">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens).</span></span>

<span data-ttu-id="db734-150">Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="db734-150">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

## <a name="chapter-1--create-the-bot-application"></a><span data-ttu-id="db734-151">Chapitre 1 – créer l’application Bot</span><span class="sxs-lookup"><span data-stu-id="db734-151">Chapter 1 – Create the Bot application</span></span>

<span data-ttu-id="db734-152">La première étape consiste à créer votre robot en tant qu’une application Web ASP.Net Core locale.</span><span class="sxs-lookup"><span data-stu-id="db734-152">The first step is to create your bot as a local ASP.Net Core Web application.</span></span> <span data-ttu-id="db734-153">Une fois que vous avez terminé et testé, vous allez le publier sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="db734-153">Once you have finished and tested it, you will publish it to the Azure Portal.</span></span>

1.  <span data-ttu-id="db734-154">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db734-154">Open Visual Studio.</span></span> <span data-ttu-id="db734-155">Créez un projet, sélectionnez **ASP NET Core Web Application** comme type de projet (vous trouverez sous la sous-section .NET Core) et appelez-le **MyBot**.</span><span class="sxs-lookup"><span data-stu-id="db734-155">Create a new project, select **ASP NET Core Web Application** as the project type (you will find it under the subsection .NET Core) and call it **MyBot**.</span></span> <span data-ttu-id="db734-156">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="db734-156">Click **OK**.</span></span>

2.  <span data-ttu-id="db734-157">Dans la fenêtre qui s’affiche sélectionnez **vide**.</span><span class="sxs-lookup"><span data-stu-id="db734-157">In the Window that will appear select **Empty**.</span></span> <span data-ttu-id="db734-158">Également Assurez-vous que la cible est définie sur **ASP NET Core 2.0** et l’authentification est définie sur **aucune authentification**.</span><span class="sxs-lookup"><span data-stu-id="db734-158">Also make sure the target is set to **ASP NET Core 2.0** and the Authentication is set to **No Authentication**.</span></span> <span data-ttu-id="db734-159">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="db734-159">Click **OK**.</span></span>  

    ![Créer l’application bot](images/AzureLabs-Lab312-01.png)

3.  <span data-ttu-id="db734-161">La solution s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="db734-161">The solution will now open.</span></span> <span data-ttu-id="db734-162">Avec le bouton droit sur la Solution **Mybot** dans le **l’Explorateur de solutions** , puis cliquez sur **gérer les Packages NuGet pour la Solution**.</span><span class="sxs-lookup"><span data-stu-id="db734-162">Right-click on Solution **Mybot** in the **Solution Explorer** and click on **Manage NuGet Packages for Solution**.</span></span> 

    ![Créer l’application Bot](images/AzureLabs-Lab312-02.png)

4.  <span data-ttu-id="db734-164">Dans le **Parcourir** onglet, recherchez **Microsoft.Bot.Builder.Integration.AspNet.Core** (Vérifiez que vous avez **inclure la version préliminaire** activée).</span><span class="sxs-lookup"><span data-stu-id="db734-164">In the **Browse** tab, search for **Microsoft.Bot.Builder.Integration.AspNet.Core** (make sure you have **Include pre-release** checked).</span></span> <span data-ttu-id="db734-165">Sélectionnez la version du package **4.0.1-preview**et cochez les cases du projet.</span><span class="sxs-lookup"><span data-stu-id="db734-165">Select the package version **4.0.1-preview**, and tick the project boxes.</span></span> <span data-ttu-id="db734-166">Cliquez ensuite sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="db734-166">Then click on **Install**.</span></span> <span data-ttu-id="db734-167">Vous avez installé les bibliothèques nécessaires pour le **Bot Framework v4**.</span><span class="sxs-lookup"><span data-stu-id="db734-167">You have now installed the libraries needed for the **Bot Framework v4**.</span></span> <span data-ttu-id="db734-168">Fermez la page NuGet.</span><span class="sxs-lookup"><span data-stu-id="db734-168">Close the NuGet page.</span></span>

    ![Créer l’application bot](images/AzureLabs-Lab312-03.png)

5.  <span data-ttu-id="db734-170">Avec le bouton droit sur votre *projet*, **MyBot**, dans le **l’Explorateur de solutions** , puis cliquez sur **ajouter** **|** **Classe**.</span><span class="sxs-lookup"><span data-stu-id="db734-170">Right-click on your *Project*, **MyBot**, in the **Solution Explorer** and click on **Add** **|** **Class**.</span></span>

    ![Créer l’application Bot](images/AzureLabs-Lab312-04.png)

6.  <span data-ttu-id="db734-172">Nommez la classe **MyBot** , puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="db734-172">Name the class **MyBot** and click on **Add**.</span></span>

    ![Créer l’application bot](images/AzureLabs-Lab312-05.png)

7.  <span data-ttu-id="db734-174">Répétez le point précédent, pour créer une autre classe nommée **ConversationContext**.</span><span class="sxs-lookup"><span data-stu-id="db734-174">Repeat the previous point, to create another class named **ConversationContext**.</span></span> 

8.  <span data-ttu-id="db734-175">Avec le bouton droit sur **wwwroot** dans le **l’Explorateur de solutions** , puis cliquez sur **ajouter** **|** **unnouvelélément**.</span><span class="sxs-lookup"><span data-stu-id="db734-175">Right-click on **wwwroot** in the **Solution Explorer** and click on **Add** **|** **New Item**.</span></span> <span data-ttu-id="db734-176">Sélectionnez **HTML Page** (vous trouverez sous la sous-section Web).</span><span class="sxs-lookup"><span data-stu-id="db734-176">Select  **HTML Page** (you will find it under the subsection Web).</span></span> <span data-ttu-id="db734-177">Nommez le fichier **default.html**.</span><span class="sxs-lookup"><span data-stu-id="db734-177">Name the file **default.html**.</span></span> <span data-ttu-id="db734-178">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="db734-178">Click **Add**.</span></span>

    ![Créer l’application bot](images/AzureLabs-Lab312-06.png)

9.  <span data-ttu-id="db734-180">La liste des classes / objets dans le **l’Explorateur de solutions** doit ressembler à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="db734-180">The list of classes / objects in the **Solution Explorer** should look like the image below.</span></span>

    ![Créer l’application bot](images/AzureLabs-Lab312-07.png)

10. <span data-ttu-id="db734-182">Double-cliquez sur le **ConversationContext** classe.</span><span class="sxs-lookup"><span data-stu-id="db734-182">Double-click on the **ConversationContext** class.</span></span> <span data-ttu-id="db734-183">Cette classe est chargée de conserver les variables utilisées par le robot de conserver le contexte de la conversation.</span><span class="sxs-lookup"><span data-stu-id="db734-183">This class is responsible for holding the variables used by the bot to maintain the context of the conversation.</span></span> <span data-ttu-id="db734-184">Ces valeurs de contexte de conversation sont conservées dans une instance de cette classe, car n’importe quelle instance de la **MyBot** classe sera actualisée à chaque fois qu’une activité est reçue.</span><span class="sxs-lookup"><span data-stu-id="db734-184">These conversation context values are maintained in an instance of this class, because any instance of the **MyBot** class will refresh each time an activity is received.</span></span> <span data-ttu-id="db734-185">Ajoutez le code suivant à la classe :</span><span class="sxs-lookup"><span data-stu-id="db734-185">Add the following code to the class:</span></span>

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

11. <span data-ttu-id="db734-186">Double-cliquez sur le **MyBot** classe.</span><span class="sxs-lookup"><span data-stu-id="db734-186">Double-click on the **MyBot** class.</span></span> <span data-ttu-id="db734-187">Cette classe héberge les gestionnaires appelées par n’importe quelle activité entrante du client.</span><span class="sxs-lookup"><span data-stu-id="db734-187">This class will host the handlers called by any incoming activity from the customer.</span></span> <span data-ttu-id="db734-188">Dans cette classe, vous ajouterez le code utilisé pour créer la conversation entre le robot et le client.</span><span class="sxs-lookup"><span data-stu-id="db734-188">In this class you will add the code used to build the conversation between the bot and the customer.</span></span> <span data-ttu-id="db734-189">Comme mentionné précédemment, une instance de cette classe est initialisée chaque fois qu’une activité est reçue.</span><span class="sxs-lookup"><span data-stu-id="db734-189">As mentioned earlier, an instance of this class is initialized each time an activity is received.</span></span> <span data-ttu-id="db734-190">Ajoutez le code suivant à cette classe :</span><span class="sxs-lookup"><span data-stu-id="db734-190">Add the following code to this class:</span></span>

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

12. <span data-ttu-id="db734-191">Double-cliquez sur le **démarrage** classe.</span><span class="sxs-lookup"><span data-stu-id="db734-191">Double-click on the **Startup** class.</span></span> <span data-ttu-id="db734-192">Cette classe initialisera le robot.</span><span class="sxs-lookup"><span data-stu-id="db734-192">This class will initialize the bot.</span></span> <span data-ttu-id="db734-193">Ajoutez le code suivant à la classe :</span><span class="sxs-lookup"><span data-stu-id="db734-193">Add the following code to the class:</span></span>

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

13. <span data-ttu-id="db734-194">Ouvrez le **programme** fichier de classe et de vérifier le code qu’il contient est identique à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="db734-194">Open the **Program** class file and verify the code in it is the same as the following:</span></span>

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

14. <span data-ttu-id="db734-195">N’oubliez pas d’enregistrer vos modifications, pour ce faire, accédez à **fichier** > **Enregistrer tout**, à partir de la barre d’outils en haut de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db734-195">Remember to save your changes, to do so, go to **File** > **Save All**, from the toolbar at the top of Visual Studio.</span></span>

## <a name="chapter-2---create-the-azure-bot-service"></a><span data-ttu-id="db734-196">Chapitre 2 : créer le Service de robot Azure</span><span class="sxs-lookup"><span data-stu-id="db734-196">Chapter 2 - Create the Azure Bot Service</span></span>

<span data-ttu-id="db734-197">Maintenant que vous avez généré le code pour votre bot, vous devez le publier sur une instance de la *Web App Bot* Service, sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="db734-197">Now that you have built the code for your bot, you have to publish it to an instance of the *Web App Bot* Service, on the Azure Portal.</span></span> <span data-ttu-id="db734-198">Ce chapitre sera vous montrer comment créer et configurer le Service de robot sur Azure et puis publiez votre code à ce dernier.</span><span class="sxs-lookup"><span data-stu-id="db734-198">This Chapter will show you how to create and configure the Bot Service on Azure and then publish your code to it.</span></span>

1.  <span data-ttu-id="db734-199">Tout d’abord, connectez-vous au portail Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="db734-199">First, log in to the Azure Portal (https://portal.azure.com).</span></span> 

    1. <span data-ttu-id="db734-200">Si vous n’avez pas déjà un compte Azure, vous devrez créer un.</span><span class="sxs-lookup"><span data-stu-id="db734-200">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="db734-201">Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="db734-201">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="db734-202">Une fois que vous êtes connecté, cliquez sur **créer une ressource** dans le coin supérieur gauche coin inférieur droit, puis recherchez *Web App bot*, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="db734-202">Once you are logged in, click on **Create a resource** in the top left corner, and search for *Web App bot*, and click **Enter**.</span></span>

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-08.png)
 
3.  <span data-ttu-id="db734-204">La nouvelle page doit fournir une description de la *Web App Bot* Service.</span><span class="sxs-lookup"><span data-stu-id="db734-204">The new page will provide a description of the *Web App Bot* Service.</span></span> <span data-ttu-id="db734-205">En bas à gauche de cette page, sélectionnez le **créer** bouton, pour créer une association avec ce Service.</span><span class="sxs-lookup"><span data-stu-id="db734-205">At the bottom left of this page, select the **Create** button, to create an association with this Service.</span></span>

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-09.png)
 
4.  <span data-ttu-id="db734-207">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="db734-207">Once you have clicked on **Create**:</span></span>

    1. <span data-ttu-id="db734-208">Insérez votre souhaitée **nom** pour cette instance de Service.</span><span class="sxs-lookup"><span data-stu-id="db734-208">Insert your desired **Name** for this Service instance.</span></span>
    2. <span data-ttu-id="db734-209">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="db734-209">Select a **Subscription**.</span></span>
    3. <span data-ttu-id="db734-210">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="db734-210">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="db734-211">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="db734-211">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="db734-212">Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="db734-212">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

        > <span data-ttu-id="db734-213">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, [, suivez ce lien](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)</span><span class="sxs-lookup"><span data-stu-id="db734-213">If you wish to read more about Azure Resource Groups, [please follow this link](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)</span></span>

    4. <span data-ttu-id="db734-214">Déterminer l’emplacement de votre groupe de ressources (si vous créez un nouveau groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="db734-214">Determine the Location for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="db734-215">Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="db734-215">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="db734-216">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="db734-216">Some Azure assets are only available in certain regions.</span></span>
    5. <span data-ttu-id="db734-217">Sélectionnez le **niveau tarifaire** appropriés pour vous, s’il s’agit du premier temps à créer un *Web App Bot* Service, un niveau gratuit (nommé F0) doit être disponible pour vous</span><span class="sxs-lookup"><span data-stu-id="db734-217">Select the **Pricing Tier** appropriate for you, if this is the first time creating a *Web App Bot* Service, a free tier (named F0) should be available to you</span></span>
    6. <span data-ttu-id="db734-218">**Nom de l’application** peut simplement rester le même que le *nom du robot*.</span><span class="sxs-lookup"><span data-stu-id="db734-218">**App name** can just be left the same as the *Bot name*.</span></span> 
    7. <span data-ttu-id="db734-219">Laissez le *modèle de robot* comme **base (C#)**.</span><span class="sxs-lookup"><span data-stu-id="db734-219">Leave the *Bot template* as **Basic (C#)**.</span></span>
    8. <span data-ttu-id="db734-220">*Plan/emplacement app service* aurait dû être renseignées automatiquement pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="db734-220">*App service plan/Location* should have been auto-filled for your account.</span></span>
    9. <span data-ttu-id="db734-221">Définir le **stockage Azure** que vous souhaitez utiliser pour héberger votre robot.</span><span class="sxs-lookup"><span data-stu-id="db734-221">Set the **Azure Storage** that you wish to use to host your Bot.</span></span> <span data-ttu-id="db734-222">Si vous n’en avez pas, vous pouvez le créer ici.</span><span class="sxs-lookup"><span data-stu-id="db734-222">If you dont have one already, you can create it here.</span></span>
    10. <span data-ttu-id="db734-223">Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.</span><span class="sxs-lookup"><span data-stu-id="db734-223">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>
    11. <span data-ttu-id="db734-224">Cliquez sur Créer.</span><span class="sxs-lookup"><span data-stu-id="db734-224">Click Create.</span></span>
 
        ![Créer le Service de robot Azure](images/AzureLabs-Lab312-10.png)

5.  <span data-ttu-id="db734-226">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le Service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="db734-226">Once you have clicked on **Create**, you will have to wait for the Service to be created, this might take a minute.</span></span>

6.  <span data-ttu-id="db734-227">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="db734-227">A notification will appear in the Portal once the Service instance is created.</span></span>

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-11.png) 
 
7.  <span data-ttu-id="db734-229">Cliquez sur la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="db734-229">Click on the notification to explore your new Service instance.</span></span> 

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-12.png)
 
8. <span data-ttu-id="db734-231">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="db734-231">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="db734-232">Vous êtes redirigé vers votre nouvelle instance de Service Azure.</span><span class="sxs-lookup"><span data-stu-id="db734-232">You will be taken to your new Azure Service instance.</span></span> 

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-13.png)
 
9.  <span data-ttu-id="db734-234">À ce stade, vous devez configurer une fonctionnalité appelée **par ligne directe** pour autoriser votre application cliente communiquer avec ce Service de robot.</span><span class="sxs-lookup"><span data-stu-id="db734-234">At this point you need to setup a feature called **Direct Line** to allow your client application to communicate with this Bot Service.</span></span> <span data-ttu-id="db734-235">Cliquez sur **canaux**, puis dans le **ajouter un canal proposé** section, cliquez sur **canal de configurer par ligne directe**.</span><span class="sxs-lookup"><span data-stu-id="db734-235">Click on **Channels**, then in the **Add a featured channel** section, click on **Configure Direct Line channel**.</span></span>

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-14.png)

10. <span data-ttu-id="db734-237">Dans cette page, vous trouverez le **clés secrètes** qui permettra à votre application cliente pour s’authentifier auprès du robot.</span><span class="sxs-lookup"><span data-stu-id="db734-237">In this page you will find the **Secret keys** that will allow your client app to authenticate with the bot.</span></span> <span data-ttu-id="db734-238">Cliquez sur le **afficher** bouton et effectuez une copie de l’une des clés affichées, car vous en aurez besoin plus loin dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="db734-238">Click on the **Show** button and take a copy of one of the displayed Keys, as you will need this later in your project.</span></span> 

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-15.png)

## <a name="chapter-3--publish-the-bot-to-the-azure-web-app-bot-service"></a><span data-ttu-id="db734-240">Chapitre 3 : publier le Bot sur le Service de robot d’application Web Azure</span><span class="sxs-lookup"><span data-stu-id="db734-240">Chapter 3 – Publish the Bot to the Azure Web App Bot Service</span></span>

<span data-ttu-id="db734-241">Maintenant que votre Service est prêt, vous devez publier votre code de robot, que vous avez créée précédemment, à votre serveur Web App Bot Service nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="db734-241">Now that your Service is ready, you need to publish your Bot code, that you built previously, to your newly created Web App Bot Service.</span></span>

> [!NOTE] 
> <span data-ttu-id="db734-242">Vous devrez publier votre robot au Service Azure chaque fois que vous apportez des modifications à la solution Bot / code.</span><span class="sxs-lookup"><span data-stu-id="db734-242">You will have to publish your Bot to the Azure Service every time you make changes to the Bot solution / code.</span></span>

1.  <span data-ttu-id="db734-243">Revenez à votre Solution Visual Studio que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="db734-243">Go back to your Visual Studio Solution that you created previously.</span></span> 
2.  <span data-ttu-id="db734-244">Avec le bouton droit sur votre **MyBot** de projet, dans le **l’Explorateur de solutions**, puis cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="db734-244">Right-click on your **MyBot** project, in the **Solution Explorer**, then click on **Publish**.</span></span>

    ![Publier le Bot sur le Service de robot d’application Web Azure](images/AzureLabs-Lab312-16.png)

3.  <span data-ttu-id="db734-246">Sur le *choisir une cible de publication* , cliquez sur **App Service**, puis **sélectionner**, enfin cliquez sur **créer un profil** (vous devrez peut-être Cliquez sur la flèche déroulante en même temps que le *publier* bouton, si cela n’est pas visible).</span><span class="sxs-lookup"><span data-stu-id="db734-246">On the *Pick a publish target* page, click **App Service**, then **Select Existing**, lastly click on **Create Profile** (you may need to click on the dropdown arrow alongside the *Publish* button, if this is not visible).</span></span>

    ![Publier le Bot sur le Service de robot d’application Web Azure](images/AzureLabs-Lab312-17.png)

4. <span data-ttu-id="db734-248">Si vous n’êtes pas encore connecté à votre Account Microsoft, vous devez le faire ici.</span><span class="sxs-lookup"><span data-stu-id="db734-248">If you are not yet logged in into your Microsoft Account, you have to do it here.</span></span>
5. <span data-ttu-id="db734-249">Sur le **publier** vous trouverez que vous devez définir le même **abonnement** que vous avez utilisé pour le *Web App Bot* la création du Service.</span><span class="sxs-lookup"><span data-stu-id="db734-249">On the **Publish** page you will find you have to set the same **Subscription** that you used for the *Web App Bot* Service creation.</span></span> <span data-ttu-id="db734-250">Définissez ensuite la **vue** en tant que **groupe de ressources** et, dans la liste déroulante la structure de dossiers, sélectionnez le **groupe de ressources** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="db734-250">Then set the **View** as **Resource Group** and, in the drop down folder structure, select the **Resource Group** you have created previously.</span></span> <span data-ttu-id="db734-251">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="db734-251">Click **OK**.</span></span> 

    ![Publier le Bot sur le Service de robot d’application Web Azure](images/AzureLabs-Lab312-18.png)

6.  <span data-ttu-id="db734-253">Cliquez maintenant sur le **publier** bouton et attendez que le robot à publier (il peut prendre quelques minutes).</span><span class="sxs-lookup"><span data-stu-id="db734-253">Now click on the **Publish** button, and wait for the Bot to be published (it might take a few minutes).</span></span>

    ![Publier le Bot sur le Service de robot d’application Web Azure](images/AzureLabs-Lab312-19.png)


## <a name="chapter-4--set-up-the-unity-project"></a><span data-ttu-id="db734-255">Chapitre 4 : configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="db734-255">Chapter 4 – Set up the Unity project</span></span>

<span data-ttu-id="db734-256">Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="db734-256">The following is a typical set up for developing with mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="db734-257">Ouvrez *Unity* et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="db734-257">Open *Unity* and click **New**.</span></span> 

    ![Configurer le projet Unity](images/AzureLabs-Lab312-20.png)

2.  <span data-ttu-id="db734-259">Maintenant, vous devez fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="db734-259">You will now need to provide a Unity project name.</span></span> <span data-ttu-id="db734-260">Insérer **Hololens Bot**.</span><span class="sxs-lookup"><span data-stu-id="db734-260">Insert **Hololens Bot**.</span></span> <span data-ttu-id="db734-261">Assurez-vous que le modèle de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="db734-261">Make sure the project template is set to **3D**.</span></span> <span data-ttu-id="db734-262">Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="db734-262">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="db734-263">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="db734-263">Then, click **Create project**.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab312-21.png)

3.  <span data-ttu-id="db734-265">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="db734-265">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="db734-266">Accédez à **Modifier > Préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="db734-266">Go to **Edit > Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="db734-267">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="db734-267">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="db734-268">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="db734-268">Close the **Preferences** window.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab312-22.png)

4.  <span data-ttu-id="db734-270">Ensuite, accédez à **fichier > Paramètres de Build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le **plateforme de commutation** bouton pour appliquer votre sélection.</span><span class="sxs-lookup"><span data-stu-id="db734-270">Next, go to **File > Build Settings** and select **Universal Windows Platform**, then click on the **Switch Platform** button to apply your selection.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab312-23.png)

5.  <span data-ttu-id="db734-272">Lorsque vous êtes toujours dans **fichier > Paramètres de Build** et vous assurer que :</span><span class="sxs-lookup"><span data-stu-id="db734-272">While still in **File > Build Settings** and make sure that:</span></span>

    1.  <span data-ttu-id="db734-273">**Équipement cible** a la valeur **Hololens**</span><span class="sxs-lookup"><span data-stu-id="db734-273">**Target Device** is set to **Hololens**</span></span>

        > <span data-ttu-id="db734-274">Pour des casques IMMERSIFS, définissez **appareil cible** à *n’importe quel appareil*.</span><span class="sxs-lookup"><span data-stu-id="db734-274">For the immersive headsets, set **Target Device** to *Any Device*.</span></span>

    2.  <span data-ttu-id="db734-275">**Type de build** a la valeur **D3D**</span><span class="sxs-lookup"><span data-stu-id="db734-275">**Build Type** is set to **D3D**</span></span>

    3.  <span data-ttu-id="db734-276">**Kit de développement logiciel** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="db734-276">**SDK** is set to **Latest installed**</span></span>

    4.  <span data-ttu-id="db734-277">**Version de Visual Studio** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="db734-277">**Visual Studio Version** is set to **Latest installed**</span></span>

    5.  <span data-ttu-id="db734-278">**Générez et exécutez** est défini sur **ordinateur Local**</span><span class="sxs-lookup"><span data-stu-id="db734-278">**Build and Run** is set to **Local Machine**</span></span>

    6.  <span data-ttu-id="db734-279">Enregistrer la scène et l’ajouter à la build.</span><span class="sxs-lookup"><span data-stu-id="db734-279">Save the scene and add it to the build.</span></span> 

        1. <span data-ttu-id="db734-280">Cela en sélectionnant **ajouter un arrière-plan Open**.</span><span class="sxs-lookup"><span data-stu-id="db734-280">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="db734-281">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="db734-281">A save window will appear.</span></span>
        
            ![Configurer le projet Unity](images/AzureLabs-Lab312-24.png)

        2. <span data-ttu-id="db734-283">Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.</span><span class="sxs-lookup"><span data-stu-id="db734-283">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

             ![Configurer le projet Unity](images/AzureLabs-Lab312-25.png)

        3. <span data-ttu-id="db734-285">Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier*: champ de texte, tapez **BotScene**, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="db734-285">Open your newly created **Scenes** folder, and then in the *File name*: text field, type **BotScene**, then click on **Save**.</span></span>

            ![Configurer le projet Unity](images/AzureLabs-Lab312-26.png)

    7. <span data-ttu-id="db734-287">Les autres paramètres, dans **paramètres de Build**, doit être conservé comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="db734-287">The remaining settings, in **Build Settings**, should be left as default for now.</span></span>

6. <span data-ttu-id="db734-288">Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve.</span><span class="sxs-lookup"><span data-stu-id="db734-288">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span> 

    ![Configurer le projet Unity](images/AzureLabs-Lab312-27.png)

7. <span data-ttu-id="db734-290">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="db734-290">In this panel, a few settings need to be verified:</span></span>

    1. <span data-ttu-id="db734-291">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="db734-291">In the **Other Settings** tab:</span></span>

        1. <span data-ttu-id="db734-292">**Version du Runtime de script** doit être **expérimental (NET 4.6 équivalent)**; cette modification nécessite un redémarrage de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="db734-292">**Scripting Runtime Version** should be **Experimental (NET 4.6 Equivalent)**; changing this will require a restart of the Editor.</span></span>
        2. <span data-ttu-id="db734-293">**Script principal** doit être **.NET**</span><span class="sxs-lookup"><span data-stu-id="db734-293">**Scripting Backend** should be **.NET**</span></span>
        3. <span data-ttu-id="db734-294">**Niveau de compatibilité d’API** doit être **.NET 4.6**</span><span class="sxs-lookup"><span data-stu-id="db734-294">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![Configurer le projet Unity](images/AzureLabs-Lab312-28.png)
      
    2. <span data-ttu-id="db734-296">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="db734-296">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="db734-297">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="db734-297">**InternetClient**</span></span>
        - <span data-ttu-id="db734-298">**Microphone**</span><span class="sxs-lookup"><span data-stu-id="db734-298">**Microphone**</span></span>

            ![Configurer le projet Unity](images/AzureLabs-Lab312-29.png)

    3. <span data-ttu-id="db734-300">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.</span><span class="sxs-lookup"><span data-stu-id="db734-300">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Configurer le projet Unity](images/AzureLabs-Lab312-30.png)

8.  <span data-ttu-id="db734-302">Dans *paramètres de Build* _Unity C#_  projets est n’est plus grisée ; Cochez la case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="db734-302">Back in *Build Settings* _Unity C#_ Projects is no longer greyed out; tick the checkbox next to this.</span></span> 
9.  <span data-ttu-id="db734-303">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="db734-303">Close the Build Settings window.</span></span>
10. <span data-ttu-id="db734-304">Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="db734-304">Save your scene and project (**FILE > SAVE SCENE / FILE > SAVE PROJECT**).</span></span>


## <a name="chapter-5--camera-setup"></a><span data-ttu-id="db734-305">Chapitre 5 – programme d’installation de l’appareil photo</span><span class="sxs-lookup"><span data-stu-id="db734-305">Chapter 5 – Camera setup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db734-306">Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [Azure-MR-312-Package.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20312%20-%20Bot%20integration/Azure-MR-312.unitypackage), importez-le dans votre projet sous la forme d’un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 7](#chapter-7-–-create-the-botobjects-class).</span><span class="sxs-lookup"><span data-stu-id="db734-306">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to download this [Azure-MR-312-Package.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20312%20-%20Bot%20integration/Azure-MR-312.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 7](#chapter-7-–-create-the-botobjects-class).</span></span>

1.  <span data-ttu-id="db734-307">Dans le *Panneau de la hiérarchie*, sélectionnez le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="db734-307">In the *Hierarchy panel*, select the **Main Camera**.</span></span> 
2.  <span data-ttu-id="db734-308">Une fois sélectionné, vous serez en mesure de voir tous les composants de la **Main Camera** dans le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="db734-308">Once selected, you will be able to see all the components of the **Main Camera** in the *Inspector panel*.</span></span>

    1. <span data-ttu-id="db734-309">Le **objet caméra** doit être nommé **Main Camera** (Notez l’orthographe)</span><span class="sxs-lookup"><span data-stu-id="db734-309">The **Camera object** must be named **Main Camera** (note the spelling)</span></span>
    2. <span data-ttu-id="db734-310">La caméra principale **balise** doit être définie sur **MainCamera** (Notez l’orthographe)</span><span class="sxs-lookup"><span data-stu-id="db734-310">The Main Camera **Tag** must be set to **MainCamera** (note the spelling)</span></span>
    3. <span data-ttu-id="db734-311">Assurez-vous que le **Position transformer** a la valeur **0, 0, 0**</span><span class="sxs-lookup"><span data-stu-id="db734-311">Make sure the **Transform Position** is set to **0, 0, 0**</span></span>
    4. <span data-ttu-id="db734-312">Définissez **d’effacer les indicateurs** à **couleur unie**.</span><span class="sxs-lookup"><span data-stu-id="db734-312">Set **Clear Flags** to **Solid Color**.</span></span>
    5. <span data-ttu-id="db734-313">Définir le **arrière-plan** couleur du composant de caméra à **noir, Alpha 0 (Hex Code : #00000000)**</span><span class="sxs-lookup"><span data-stu-id="db734-313">Set the **Background** Color of the Camera component to **Black, Alpha 0 (Hex Code: #00000000)**</span></span>

    ![le programme d’installation de la caméra](images/AzureLabs-Lab312-31.png)
 

## <a name="chapter-6--import-the-newtonsoft-library"></a><span data-ttu-id="db734-315">Chapitre 6 – importer la bibliothèque Newtonsoft</span><span class="sxs-lookup"><span data-stu-id="db734-315">Chapter 6 – Import the Newtonsoft library</span></span>

<span data-ttu-id="db734-316">Pour vous aider à désérialiser et sérialiser des objets reçus et envoyés au Service Bot, vous devez télécharger le **Newtonsoft** bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="db734-316">To help you deserialize and serialize objects received and sent to the Bot Service you need to download the **Newtonsoft** library.</span></span> <span data-ttu-id="db734-317">Vous trouverez un [version compatible déjà organisée avec la structure de dossiers Unity correcte ici](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20312%20-%20Bot%20integration/NewtonsoftDLL.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="db734-317">You will find a [compatible version already organized with the correct Unity folder structure here](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20312%20-%20Bot%20integration/NewtonsoftDLL.unitypackage).</span></span> 

<span data-ttu-id="db734-318">Pour importer la bibliothèque Newtonsoft dans votre projet, utilisez le Package Unity qui accompagne ce cours.</span><span class="sxs-lookup"><span data-stu-id="db734-318">To import the Newtonsoft library into your project, use the Unity Package which came with this course.</span></span>

1.  <span data-ttu-id="db734-319">Ajouter le *.unitypackage* à Unity à l’aide de la **actifs** > **importer un Package** > **Package personnalisé** option de menu.</span><span class="sxs-lookup"><span data-stu-id="db734-319">Add the *.unitypackage* to Unity by using the **Assets** > **Import Package** > **Custom Package** menu option.</span></span>

    ![Importer la bibliothèque Newtonsoft](images/AzureLabs-Lab312-34.png)

2.  <span data-ttu-id="db734-321">Dans le **importer un Package Unity** emballer qui apparaît, vérifiez tous les éléments sous (y compris) **plug-ins** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="db734-321">In the **Import Unity Package** box that pops up, ensure everything under (and including) **Plugins** is selected.</span></span>

    ![Importer la bibliothèque Newtonsoft](images/AzureLabs-Lab312-35.png)

3.  <span data-ttu-id="db734-323">Cliquez sur le **importation** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="db734-323">Click the **Import** button to add the items to your project.</span></span>

4.  <span data-ttu-id="db734-324">Accédez à la **Newtonsoft** dossier sous **plug-ins** dans la vue de projet et sélectionnez le plug-in Newtonsoft.</span><span class="sxs-lookup"><span data-stu-id="db734-324">Go to the **Newtonsoft** folder under **Plugins** in the project view and select the Newtonsoft plugin.</span></span>

    ![](images/AzureLabs-Lab312-35b.png)

5.  <span data-ttu-id="db734-325">Avec le plug-in Newtonsoft sélectionné, vérifiez que **plateforme Any** est **unchecked**, puis assurez-vous que **WSAPlayer** est également **unchecked**, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="db734-325">With the Newtonsoft plugin selected, ensure that **Any Platform** is **unchecked**, then ensure that **WSAPlayer** is also **unchecked**, then click **Apply**.</span></span> <span data-ttu-id="db734-326">Il s’agit juste pour confirmer que les fichiers sont correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="db734-326">This is just to confirm that the files are configured correctly.</span></span>

    ![](images/AzureLabs-Lab312-35c.png)

    > [!NOTE]
    > <span data-ttu-id="db734-327">Marquage de ces plug-ins les configure uniquement à être utilisé dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="db734-327">Marking these plugins configures them to only be used in the Unity Editor.</span></span> <span data-ttu-id="db734-328">Il existe un ensemble différent d’eux dans le dossier WSA qui sera utilisé une fois que le projet est exporté à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="db734-328">There are a different set of them in the WSA folder which will be used after the project is exported from Unity.</span></span>

6.  <span data-ttu-id="db734-329">Ensuite, vous devez ouvrir le **WSA** dossier, en respectant le **Newtonsoft** dossier.</span><span class="sxs-lookup"><span data-stu-id="db734-329">Next, you need to open the **WSA** folder, within the **Newtonsoft** folder.</span></span> <span data-ttu-id="db734-330">Vous verrez une copie du même fichier que vous venez de configurer.</span><span class="sxs-lookup"><span data-stu-id="db734-330">You will see a copy of the same file you just configured.</span></span> <span data-ttu-id="db734-331">Sélectionnez le fichier et dans l’inspecteur, vérifiez que</span><span class="sxs-lookup"><span data-stu-id="db734-331">Select the file, and then in the inspector, ensure that</span></span>
    -   <span data-ttu-id="db734-332">**N’importe quelle plateforme** est **non contrôlé**</span><span class="sxs-lookup"><span data-stu-id="db734-332">**Any Platform** is **unchecked**</span></span> 
    -   <span data-ttu-id="db734-333">**uniquement** **WSAPlayer** est **activée**</span><span class="sxs-lookup"><span data-stu-id="db734-333">**only** **WSAPlayer** is **checked**</span></span>
    -   <span data-ttu-id="db734-334">**Ne pas traiter les** est **activée**</span><span class="sxs-lookup"><span data-stu-id="db734-334">**Dont process** is **checked**</span></span>

    ![](images/AzureLabs-Lab312-35d.png)

## <a name="chapter-7--create-the-bottag"></a><span data-ttu-id="db734-335">Chapitre 7 – créer la BotTag</span><span class="sxs-lookup"><span data-stu-id="db734-335">Chapter 7 – Create the BotTag</span></span>

1.  <span data-ttu-id="db734-336">Créer un nouveau **balise** objet appelé **BotTag**.</span><span class="sxs-lookup"><span data-stu-id="db734-336">Create a new **Tag** object called **BotTag**.</span></span> <span data-ttu-id="db734-337">Sélectionnez la caméra principale dans la scène.</span><span class="sxs-lookup"><span data-stu-id="db734-337">Select the Main Camera in the scene.</span></span> <span data-ttu-id="db734-338">Cliquez sur la balise de liste déroulante menu dans le panneau de l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="db734-338">Click on the Tag drop down menu in the Inspector panel.</span></span> <span data-ttu-id="db734-339">Cliquez sur **ajouter une balise**.</span><span class="sxs-lookup"><span data-stu-id="db734-339">Click on **Add Tag**.</span></span>

    ![le programme d’installation de la caméra](images/AzureLabs-Lab312-32.png)
 
2.  <span data-ttu-id="db734-341">Cliquez sur le **+** symbole.</span><span class="sxs-lookup"><span data-stu-id="db734-341">Click on the **+** symbol.</span></span> <span data-ttu-id="db734-342">Nommez le nouveau **balise** comme **BotTag**, *enregistrer*.</span><span class="sxs-lookup"><span data-stu-id="db734-342">Name the new **Tag** as **BotTag**, *Save*.</span></span>

    ![le programme d’installation de la caméra](images/AzureLabs-Lab312-33.png)

> [!WARNING] 
> <span data-ttu-id="db734-344">**Ne le faites pas** appliquer le **BotTag** à la caméra principale.</span><span class="sxs-lookup"><span data-stu-id="db734-344">**Do not** apply the **BotTag** to the Main Camera.</span></span> <span data-ttu-id="db734-345">Si vous avez accidentellement fait, veillez à modifier la balise au Main Camera *MainCamera*.</span><span class="sxs-lookup"><span data-stu-id="db734-345">If you have accidentally done this, make sure to change the Main Camera tag back to *MainCamera*.</span></span>

## <a name="chapter-8--create-the-botobjects-class"></a><span data-ttu-id="db734-346">Chapitre 8 : créer la classe BotObjects</span><span class="sxs-lookup"><span data-stu-id="db734-346">Chapter 8 – Create the BotObjects class</span></span>

<span data-ttu-id="db734-347">Est le premier script que vous avez besoin pour créer le **BotObjects** (classe), qui est une classe vide créé afin qu’une série d’autres objets de classe permettre être stockée dans le même script et accessible par d’autres scripts dans la scène.</span><span class="sxs-lookup"><span data-stu-id="db734-347">The first script you need to create is the **BotObjects** class, which is an empty class created so that a series of other class objects can be stored within the same script and accessed by other scripts in the scene.</span></span>

<span data-ttu-id="db734-348">La création de cette classe est purement un choix architecturaux, ces objets au lieu de cela peuvent être hébergés dans le script Bot que vous créerez plus loin dans ce cours.</span><span class="sxs-lookup"><span data-stu-id="db734-348">The creation of this class is purely an architectural choice, these objects could instead be hosted in the Bot script that you will create later in this course.</span></span>

<span data-ttu-id="db734-349">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="db734-349">To create this class:</span></span> 

1.  <span data-ttu-id="db734-350">Avec le bouton droit dans le *panneau projet*, puis **créer > dossier**.</span><span class="sxs-lookup"><span data-stu-id="db734-350">Right-click in the *Project panel*, then **Create > Folder**.</span></span> <span data-ttu-id="db734-351">Nommez le dossier **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="db734-351">Name the folder **Scripts**.</span></span> 

    ![Créez le dossier scripts.](images/AzureLabs-Lab312-36.png)

2.  <span data-ttu-id="db734-353">Double-cliquez sur le **Scripts** dossier pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="db734-353">Double-click on the **Scripts** folder to open it.</span></span> <span data-ttu-id="db734-354">Ensuite, dans ce dossier, avec le bouton droit, puis sélectionnez **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="db734-354">Then within that folder, right-click, and select **Create > C# Script**.</span></span> <span data-ttu-id="db734-355">Nommez le script **BotObjects**.</span><span class="sxs-lookup"><span data-stu-id="db734-355">Name the script **BotObjects**.</span></span> 

3.  <span data-ttu-id="db734-356">Double-cliquez sur le nouveau **BotObjects** script pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="db734-356">Double-click on the new **BotObjects** script to open it with **Visual Studio**.</span></span>

4.  <span data-ttu-id="db734-357">Supprimer le contenu du script et remplacez-le par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="db734-357">Delete the content of the script and replace it with the following code:</span></span>

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

6.  <span data-ttu-id="db734-358">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="db734-358">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-9--create-the-gazeinput-class"></a><span data-ttu-id="db734-359">Chapitre 9 – créer la classe GazeInput</span><span class="sxs-lookup"><span data-stu-id="db734-359">Chapter 9 – Create the GazeInput class</span></span>

<span data-ttu-id="db734-360">La classe suivante, vous allez créer est la **GazeInput** classe.</span><span class="sxs-lookup"><span data-stu-id="db734-360">The next class you are going to create is the **GazeInput** class.</span></span> <span data-ttu-id="db734-361">Cette classe est chargée de :</span><span class="sxs-lookup"><span data-stu-id="db734-361">This class is responsible for:</span></span>

- <span data-ttu-id="db734-362">Création d’un curseur qui représentera le *les regards* du lecteur.</span><span class="sxs-lookup"><span data-stu-id="db734-362">Creating a cursor that will represent the *gaze* of the player.</span></span>
- <span data-ttu-id="db734-363">Détection d’objets atteint par le regard du lecteur et contenant une référence aux objets détectés.</span><span class="sxs-lookup"><span data-stu-id="db734-363">Detecting objects hit by the gaze of the player, and holding a reference to detected objects.</span></span>

<span data-ttu-id="db734-364">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="db734-364">To create this class:</span></span> 

1.  <span data-ttu-id="db734-365">Accédez à la **Scripts** dossier que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="db734-365">Go to the **Scripts** folder you created previously.</span></span> 
2.  <span data-ttu-id="db734-366">Avec le bouton droit dans le dossier, **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="db734-366">Right-click inside the folder, **Create > C# Script**.</span></span> <span data-ttu-id="db734-367">Appeler le script **GazeInput**.</span><span class="sxs-lookup"><span data-stu-id="db734-367">Call the script **GazeInput**.</span></span> 
3.  <span data-ttu-id="db734-368">Double-cliquez sur le nouveau **GazeInput** script pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="db734-368">Double-click on the new **GazeInput** script to open it with **Visual Studio**.</span></span>
4.  <span data-ttu-id="db734-369">Insérez la ligne suivante juste au-dessus du nom de classe :</span><span class="sxs-lookup"><span data-stu-id="db734-369">Insert the following line right on top of the class name:</span></span>

    ```csharp
    /// <summary>
    /// Class responsible for the User's gaze interactions
    /// </summary>
    [System.Serializable]
    public class GazeInput : MonoBehaviour
    ```

5.  <span data-ttu-id="db734-370">Puis ajoutez les variables suivantes à l’intérieur de la **GazeInput** classe ci-dessus le **Start()** méthode :</span><span class="sxs-lookup"><span data-stu-id="db734-370">Then add the following variables inside the **GazeInput** class, above the **Start()** method:</span></span>

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

6.  <span data-ttu-id="db734-371">Code pour **Start()** méthode doit être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="db734-371">Code for **Start()** method should be added.</span></span> <span data-ttu-id="db734-372">Celui-ci sera appelé lors de l’initialisation de la classe :</span><span class="sxs-lookup"><span data-stu-id="db734-372">This will be called when the class initializes:</span></span>

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

7.  <span data-ttu-id="db734-373">Implémentez une méthode qui instancie et configurer le curseur du pointage de regard :</span><span class="sxs-lookup"><span data-stu-id="db734-373">Implement a method that will instantiate and setup the gaze cursor:</span></span> 

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

8.  <span data-ttu-id="db734-374">Implémenter les méthodes qui vous permettront de configurer le Raycast à partir de la caméra principale et de seront assurer le suivi de l’objet ayant le focus actuel.</span><span class="sxs-lookup"><span data-stu-id="db734-374">Implement the methods that will setup the Raycast from the Main Camera and will keep track of the current focused object.</span></span>

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
 
9.  <span data-ttu-id="db734-375">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="db734-375">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-10--create-the-bot-class"></a><span data-ttu-id="db734-376">Chapitre 10 – créer la classe Bot</span><span class="sxs-lookup"><span data-stu-id="db734-376">Chapter 10 – Create the Bot class</span></span>

<span data-ttu-id="db734-377">Le script que vous vous apprêtez à créer est maintenant appelé **Bot**.</span><span class="sxs-lookup"><span data-stu-id="db734-377">The script you are going to create now is called **Bot**.</span></span> <span data-ttu-id="db734-378">Il s’agit de la classe principale de votre application, il stocke :</span><span class="sxs-lookup"><span data-stu-id="db734-378">This is the core class of your application, it stores:</span></span> 

- <span data-ttu-id="db734-379">Vos informations d’identification de Web App Bot</span><span class="sxs-lookup"><span data-stu-id="db734-379">Your Web App Bot credentials</span></span>
- <span data-ttu-id="db734-380">La méthode qui collecte les commandes de voix utilisateur</span><span class="sxs-lookup"><span data-stu-id="db734-380">The method that collects the user voice commands</span></span>
- <span data-ttu-id="db734-381">La méthode nécessaire pour lancer des conversations avec votre robot d’application Web</span><span class="sxs-lookup"><span data-stu-id="db734-381">The method necessary to initiate conversations with your Web App Bot</span></span> 
- <span data-ttu-id="db734-382">La méthode nécessaire pour envoyer des messages à votre robot d’application Web</span><span class="sxs-lookup"><span data-stu-id="db734-382">The method necessary to send messages to your Web App Bot</span></span> 

<span data-ttu-id="db734-383">Pour envoyer des messages au Service Bot, la **SendMessageToBot()** coroutine générera une activité, qui est un objet reconnu par l’infrastructure de robot en tant que données envoyées par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db734-383">To send messages to the Bot Service, the **SendMessageToBot()** coroutine will build an activity, which is an object recognized by the Bot Framework as data sent by the user.</span></span> 
 
<span data-ttu-id="db734-384">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="db734-384">To create this class:</span></span> 

1. <span data-ttu-id="db734-385">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="db734-385">Double-click on the **Scripts** folder, to open it.</span></span> 
2. <span data-ttu-id="db734-386">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="db734-386">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="db734-387">Nommez le script **Bot**.</span><span class="sxs-lookup"><span data-stu-id="db734-387">Name the script **Bot**.</span></span> 
3. <span data-ttu-id="db734-388">Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db734-388">Double-click on the new script to open it with Visual Studio.</span></span>
4. <span data-ttu-id="db734-389">Mettre à jour les espaces de noms pour être le même que la commande suivante, en haut de la **Bot** classe :</span><span class="sxs-lookup"><span data-stu-id="db734-389">Update the namespaces to be the same as the following, at the top of the **Bot** class:</span></span>

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.Text;
    using UnityEngine;
    using UnityEngine.Networking;
    using UnityEngine.Windows.Speech;
    ```
 
5. <span data-ttu-id="db734-390">À l’intérieur de la **Bot** classe ajoutez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="db734-390">Inside the **Bot** class add the following variables:</span></span>

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
    > <span data-ttu-id="db734-391">Assurez-vous que vous insérez votre **clé secrète de robot** dans le **botSecret** variable.</span><span class="sxs-lookup"><span data-stu-id="db734-391">Make sure you insert your **Bot Secret Key** into the **botSecret** variable.</span></span> <span data-ttu-id="db734-392">Avoir noté votre **clé secrète de robot** au début de ce cours, dans  **[chapitre 2](#chapter-2---create-the-azure-bot-service), étape 10**.</span><span class="sxs-lookup"><span data-stu-id="db734-392">You will have noted your **Bot Secret Key** at the beginning of this course, in **[Chapter 2](#chapter-2---create-the-azure-bot-service), step 10**.</span></span>

7. <span data-ttu-id="db734-393">Code pour **Awake()** et **Start()** doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="db734-393">Code for **Awake()** and **Start()** now needs to be added.</span></span> 

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

8. <span data-ttu-id="db734-394">Ajoutez les deux gestionnaires sont appelés par les bibliothèques de reconnaissance vocale lors de la capture de la voix commence et se termine.</span><span class="sxs-lookup"><span data-stu-id="db734-394">Add the two handlers that are called by the speech libraries when voice capture begins and ends.</span></span> <span data-ttu-id="db734-395">Le *DictationRecognizer* arrête automatiquement la capture de la voix de l’utilisateur lorsque l’utilisateur arrête de parler.</span><span class="sxs-lookup"><span data-stu-id="db734-395">The *DictationRecognizer* will automatically stop capturing the user voice when the user stops speaking.</span></span>

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

1. <span data-ttu-id="db734-396">Le gestionnaire suivant collecte le résultat de l’entrée de voix utilisateur et appelle la coroutine chargé d’envoyer le message au Service Web App Bot.</span><span class="sxs-lookup"><span data-stu-id="db734-396">The following handler collects the result of the user voice input and calls the coroutine responsible for sending the message to the Web App Bot Service.</span></span>

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

10. <span data-ttu-id="db734-397">La coroutine suivante est appelée pour commencer une conversation avec le robot.</span><span class="sxs-lookup"><span data-stu-id="db734-397">The following coroutine is called to begin a conversation with the Bot.</span></span> <span data-ttu-id="db734-398">Vous remarquerez qu’une fois que l’appel de la conversation est terminée, elle peut appeler le **SendMessageToCoroutine()** en passant d’une série de paramètres qui définira l’activité à envoyer au Service de robot en tant qu’un message vide.</span><span class="sxs-lookup"><span data-stu-id="db734-398">You will notice that once the conversation call is complete, it will call the **SendMessageToCoroutine()** by passing a series of parameters that will set the activity to be sent to the Bot Service as an empty message.</span></span> <span data-ttu-id="db734-399">Pour cela, pour demander le Service de robot pour lancer la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="db734-399">This is done to prompt the Bot Service to initiate the dialogue.</span></span>

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

11. <span data-ttu-id="db734-400">La coroutine suivante est appelée pour générer l’activité à envoyer au Service de robot.</span><span class="sxs-lookup"><span data-stu-id="db734-400">The following coroutine is called to build the activity to be sent to the Bot Service.</span></span> 

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

12. <span data-ttu-id="db734-401">La coroutine suivante est appelée pour demander une réponse après l’envoi d’une activité pour le Service de robot.</span><span class="sxs-lookup"><span data-stu-id="db734-401">The following coroutine is called to request a response after sending an activity to the Bot Service.</span></span> 

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

13. <span data-ttu-id="db734-402">La dernière méthode à ajouter à cette classe, est requis pour afficher le message dans la scène :</span><span class="sxs-lookup"><span data-stu-id="db734-402">The last method to be added to this class, is required to display the message in the scene:</span></span>

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
    > <span data-ttu-id="db734-403">Vous pouvez rencontrer une erreur dans la Console de l’éditeur Unity, manquants le **SceneOrganiser** classe.</span><span class="sxs-lookup"><span data-stu-id="db734-403">You may see an error within the Unity Editor Console, about missing the **SceneOrganiser** class.</span></span> <span data-ttu-id="db734-404">Ignorez ce message, comme vous allez créer cette classe plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="db734-404">Disregard this message, as you will create this class later in the tutorial.</span></span>

14.  <span data-ttu-id="db734-405">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="db734-405">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-11--create-the-interactions-class"></a><span data-ttu-id="db734-406">Chapitre 11 – créer la classe d’Interactions</span><span class="sxs-lookup"><span data-stu-id="db734-406">Chapter 11 – Create the Interactions class</span></span>

<span data-ttu-id="db734-407">La classe que vous vous apprêtez à créer est maintenant appelée **Interactions**.</span><span class="sxs-lookup"><span data-stu-id="db734-407">The class you are going to create now is called **Interactions**.</span></span> <span data-ttu-id="db734-408">Cette classe est utilisée pour détecter l’entrée appuyez sur HoloLens à partir de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db734-408">This class is used to detect the HoloLens Tap Input from the user.</span></span> 

<span data-ttu-id="db734-409">Si l’utilisateur appuie sur tout en gardant le *Bot* objet dans la scène et le robot est prêt à l’écoute des entrées de la voix, l’objet Bot change de couleur pour **rouge** et commencer à écouter les entrées de la voix.</span><span class="sxs-lookup"><span data-stu-id="db734-409">If the user taps while looking at the *Bot* object in the scene, and the Bot is ready to listen for voice inputs, the Bot object will change color to **red** and begin listening for voice inputs.</span></span> 

<span data-ttu-id="db734-410">Cette classe hérite de la **GazeInput** classe et peut faire référence à la **Start()** (méthode) et les variables à partir de cette classe, indiqué par l’utilisation de **base**.</span><span class="sxs-lookup"><span data-stu-id="db734-410">This class inherits from the **GazeInput** class, and so is able to reference the **Start()** method and variables from that class, denoted by the use of **base**.</span></span> 
 
<span data-ttu-id="db734-411">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="db734-411">To create this class:</span></span>

1.  <span data-ttu-id="db734-412">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="db734-412">Double-click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="db734-413">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="db734-413">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="db734-414">Nommez le script **Interactions**.</span><span class="sxs-lookup"><span data-stu-id="db734-414">Name the script **Interactions**.</span></span> 
3.  <span data-ttu-id="db734-415">Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db734-415">Double-click on the new script to open it with Visual Studio.</span></span>
4.  <span data-ttu-id="db734-416">Mettre à jour les espaces de noms et l’héritage de classe pour être le même que la commande suivante, en haut de la **Interactions** classe :</span><span class="sxs-lookup"><span data-stu-id="db734-416">Update the namespaces and the class inheritance to be the same as the following, at the top of the **Interactions** class:</span></span>

    ```csharp
    using UnityEngine.XR.WSA.Input;

    public class Interactions : GazeInput
    {
    ```

5.  <span data-ttu-id="db734-417">À l’intérieur de la **Interactions** classe ajoutez la variable suivante :</span><span class="sxs-lookup"><span data-stu-id="db734-417">Inside the **Interactions** class add the following variable:</span></span>

    ```csharp
        /// <summary>
        /// Allows input recognition with the HoloLens
        /// </summary>
        private GestureRecognizer _gestureRecognizer;
    ```
6.  <span data-ttu-id="db734-418">Ajoutez ensuite le **Start()** méthode :</span><span class="sxs-lookup"><span data-stu-id="db734-418">Then add the **Start()** method:</span></span>

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

7.  <span data-ttu-id="db734-419">Ajoutez le gestionnaire qui est déclenché lorsque l’utilisateur effectue le geste d’appui devant la caméra HoloLens</span><span class="sxs-lookup"><span data-stu-id="db734-419">Add the handler that will be triggered when the user performs the tap gesture in front of the HoloLens camera</span></span>

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

8. <span data-ttu-id="db734-420">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="db734-420">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-12--create-the-sceneorganiser-class"></a><span data-ttu-id="db734-421">Chapitre 12 – créer la classe SceneOrganiser</span><span class="sxs-lookup"><span data-stu-id="db734-421">Chapter 12 – Create the SceneOrganiser class</span></span>

<span data-ttu-id="db734-422">La dernière classe requise dans ce laboratoire est appelée **SceneOrganiser**.</span><span class="sxs-lookup"><span data-stu-id="db734-422">The last class required in this Lab is called **SceneOrganiser**.</span></span> <span data-ttu-id="db734-423">Cette classe est le programme d’installation la scène par programmation, en ajoutant des composants et des scripts à la caméra principale et en créant les objets appropriés dans la scène.</span><span class="sxs-lookup"><span data-stu-id="db734-423">This class will setup the scene programmatically, by adding components and scripts to the Main Camera, and creating the appropriate objects in the scene.</span></span>
 
<span data-ttu-id="db734-424">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="db734-424">To create this class:</span></span>

1.  <span data-ttu-id="db734-425">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="db734-425">Double-click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="db734-426">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="db734-426">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="db734-427">Nommez le script **SceneOrganiser**.</span><span class="sxs-lookup"><span data-stu-id="db734-427">Name the script **SceneOrganiser**.</span></span> 
3.  <span data-ttu-id="db734-428">Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db734-428">Double-click on the new script to open it with Visual Studio.</span></span>
4.  <span data-ttu-id="db734-429">À l’intérieur de la **SceneOrganiser** classe ajoutez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="db734-429">Inside the **SceneOrganiser** class add the following variables:</span></span>

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

6.  <span data-ttu-id="db734-430">Ajoutez ensuite le **Awake()** et **Start()** méthodes :</span><span class="sxs-lookup"><span data-stu-id="db734-430">Then add the **Awake()** and **Start()** methods:</span></span>

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

7.  <span data-ttu-id="db734-431">Ajoutez la méthode suivante, responsable de la création de l’objet de Bot dans la scène et en définissant des paramètres et des composants :</span><span class="sxs-lookup"><span data-stu-id="db734-431">Add the following method, responsible for creating the Bot object in the scene and setting up the parameters and components:</span></span>

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

7.  <span data-ttu-id="db734-432">Ajoutez la méthode suivante, responsable de la création de l’objet de l’interface utilisateur dans la scène, représentant les réponses à partir du robot :</span><span class="sxs-lookup"><span data-stu-id="db734-432">Add the following method, responsible for creating the UI object in the scene, representing the responses from the Bot:</span></span>

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

8.  <span data-ttu-id="db734-433">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="db734-433">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>
9.  <span data-ttu-id="db734-434">Dans l’éditeur Unity, faites glisser le **SceneOrganiser** script à partir du dossier Scripts à la caméra principale.</span><span class="sxs-lookup"><span data-stu-id="db734-434">In the Unity Editor, drag the **SceneOrganiser** script from the Scripts folder to the Main Camera.</span></span> <span data-ttu-id="db734-435">Le composant d’un gestionnaire de scène doit maintenant apparaître sur l’objet Main Camera, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="db734-435">The Scene Organiser component should now appear on the Main Camera object, as shown in the image below.</span></span>

    ![Créer le Service de robot Azure](images/AzureLabs-Lab312-37.png)

## <a name="chapter-13--before-building"></a><span data-ttu-id="db734-437">Chapitre 13 – avant la génération</span><span class="sxs-lookup"><span data-stu-id="db734-437">Chapter 13 – Before building</span></span>

<span data-ttu-id="db734-438">Pour effectuer une analyse minutieuse de votre application vous en aurez besoin pour effectuer un chargement indépendant sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="db734-438">To perform a thorough test of your application you will need to sideload it onto your HoloLens.</span></span>
<span data-ttu-id="db734-439">Avant de procéder, assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="db734-439">Before you do, ensure that:</span></span>

-   <span data-ttu-id="db734-440">Tous les paramètres mentionnés dans le [ **chapitre 4** ](#Chapter-4-–-Set-up-the-unity-project) sont correctement définies.</span><span class="sxs-lookup"><span data-stu-id="db734-440">All the settings mentioned in the [**Chapter 4**](#Chapter-4-–-Set-up-the-unity-project) are set correctly.</span></span> 
-   <span data-ttu-id="db734-441">Le script **SceneOrganiser** est attaché à la **Main Camera** objet.</span><span class="sxs-lookup"><span data-stu-id="db734-441">The script **SceneOrganiser** is attached to the **Main Camera** object.</span></span> 
-   <span data-ttu-id="db734-442">Dans le **Bot** class, assurez-vous que vous avez inséré votre **clé secrète de robot** dans le **botSecret** variable.</span><span class="sxs-lookup"><span data-stu-id="db734-442">In the **Bot** class, make sure you have inserted your **Bot Secret Key** into the **botSecret** variable.</span></span>

## <a name="chapter-14--build-and-sideload-to-the-hololens"></a><span data-ttu-id="db734-443">Chapitre 14 – Build et chargement de version test pour le HoloLens</span><span class="sxs-lookup"><span data-stu-id="db734-443">Chapter 14 – Build and Sideload to the HoloLens</span></span>

<span data-ttu-id="db734-444">Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée, il est temps de générer à partir de Unity.</span><span class="sxs-lookup"><span data-stu-id="db734-444">Everything needed for the Unity section of this project has now been completed, so it is time to build it from Unity.</span></span>

1.  <span data-ttu-id="db734-445">Accédez à **les paramètres de génération**, **fichier > Paramètres de Build...** .</span><span class="sxs-lookup"><span data-stu-id="db734-445">Navigate to **Build Settings**, **File > Build Settings…**.</span></span>
2.  <span data-ttu-id="db734-446">À partir de la **paramètres de Build** fenêtre, cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="db734-446">From the **Build Settings** window, click **Build**.</span></span>

    ![Création de l’application à partir d’Unity](images/AzureLabs-Lab312-38.png)

3.  <span data-ttu-id="db734-448">Si pas déjà fait, cochez **Unity C# projets**.</span><span class="sxs-lookup"><span data-stu-id="db734-448">If not already, tick **Unity C# Projects**.</span></span>
4.  <span data-ttu-id="db734-449">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="db734-449">Click **Build**.</span></span> <span data-ttu-id="db734-450">Unity lancera un **Explorateur de fichiers** fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans.</span><span class="sxs-lookup"><span data-stu-id="db734-450">Unity will launch a **File Explorer** window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="db734-451">Créez ce dossier, puis nommez-le **application**.</span><span class="sxs-lookup"><span data-stu-id="db734-451">Create that folder now, and name it **App**.</span></span> <span data-ttu-id="db734-452">Ensuite avec le **application** dossier sélectionné, cliquez sur **sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="db734-452">Then with the **App** folder selected, click **Select Folder**.</span></span> 
5.  <span data-ttu-id="db734-453">Unity commencera à générer votre projet pour le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="db734-453">Unity will begin building your project to the **App** folder.</span></span> 
6.  <span data-ttu-id="db734-454">Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un **Explorateur de fichiers** fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).</span><span class="sxs-lookup"><span data-stu-id="db734-454">Once Unity has finished building (it might take some time), it will open a **File Explorer** window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

## <a name="chapter-15--deploy-to-hololens"></a><span data-ttu-id="db734-455">Chapitre 15 – déployer sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="db734-455">Chapter 15 – Deploy to HoloLens</span></span>

<span data-ttu-id="db734-456">Pour déployer sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="db734-456">To deploy on HoloLens:</span></span>

1.  <span data-ttu-id="db734-457">Vous devez l’adresse IP de votre HoloLens (pour les déployer à distance) et pour vérifier que votre HoloLens est dans **Mode développeur**.</span><span class="sxs-lookup"><span data-stu-id="db734-457">You will need the IP Address of your HoloLens (for Remote Deploy), and to ensure your HoloLens is in **Developer Mode**.</span></span> <span data-ttu-id="db734-458">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="db734-458">To do this:</span></span>

    1. <span data-ttu-id="db734-459">Tout en portant vos HoloLens, ouvrez le **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="db734-459">Whilst wearing your HoloLens, open the **Settings**.</span></span>
    2. <span data-ttu-id="db734-460">Accédez à **réseau & Internet > Wi-Fi > Options avancées**</span><span class="sxs-lookup"><span data-stu-id="db734-460">Go to **Network & Internet > Wi-Fi > Advanced Options**</span></span>
    3. <span data-ttu-id="db734-461">Remarque la **IPv4** adresse.</span><span class="sxs-lookup"><span data-stu-id="db734-461">Note the **IPv4** address.</span></span>
    4. <span data-ttu-id="db734-462">Ensuite, accédez à **paramètres**, puis à **mise à jour & sécurité > pour les développeurs**</span><span class="sxs-lookup"><span data-stu-id="db734-462">Next, navigate back to **Settings**, and then to **Update & Security > For Developers**</span></span> 
    5. <span data-ttu-id="db734-463">Définir le Mode développeur.</span><span class="sxs-lookup"><span data-stu-id="db734-463">Set Developer Mode On.</span></span>

2.  <span data-ttu-id="db734-464">Accédez à votre nouvelle build Unity (le **application** dossier) et ouvrez le fichier solution avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="db734-464">Navigate to your new Unity build (the **App** folder) and open the solution file with **Visual Studio**.</span></span>
3.  <span data-ttu-id="db734-465">Dans le **Configuration de la Solution** sélectionnez **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="db734-465">In the **Solution Configuration** select **Debug**.</span></span>
4.  <span data-ttu-id="db734-466">Dans le **plateforme de Solution**, sélectionnez **x86**, **Machine distante**.</span><span class="sxs-lookup"><span data-stu-id="db734-466">In the **Solution Platform**, select **x86**, **Remote Machine**.</span></span> 

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab312-39.png)
 
5.  <span data-ttu-id="db734-468">Accédez à la **menu Générer** , puis cliquez sur **déployer la Solution**, chargement de version test l’application à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="db734-468">Go to the **Build menu** and click on **Deploy Solution**, to sideload the application to your HoloLens.</span></span>
6.  <span data-ttu-id="db734-469">Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prêt à être lancé !</span><span class="sxs-lookup"><span data-stu-id="db734-469">Your app should now appear in the list of installed apps on your HoloLens, ready to be launched!</span></span>

    > [!NOTE]
    > <span data-ttu-id="db734-470">Pour déployer sur casque immersif, définissez le **plateforme de Solution** à *ordinateur Local*et définissez le **Configuration** à *déboguer*, avec *x86* en tant que le **plateforme**.</span><span class="sxs-lookup"><span data-stu-id="db734-470">To deploy to immersive headset, set the **Solution Platform** to *Local Machine*, and set the **Configuration** to *Debug*, with *x86* as the **Platform**.</span></span> <span data-ttu-id="db734-471">Déployer sur l’ordinateur local d’ordinateur, à l’aide de la **menu Générer**, en sélectionnant *déployer la Solution*.</span><span class="sxs-lookup"><span data-stu-id="db734-471">Then deploy to the local machine, using the **Build menu**, selecting *Deploy Solution*.</span></span> 

## <a name="chapter-16--using-the-application-on-the-hololens"></a><span data-ttu-id="db734-472">Chapitre 16 – à l’aide de l’application sur le HoloLens</span><span class="sxs-lookup"><span data-stu-id="db734-472">Chapter 16 – Using the application on the HoloLens</span></span>

- <span data-ttu-id="db734-473">Une fois que vous avez lancé l’application, vous verrez le robot en tant qu’une sphère bleu devant vous.</span><span class="sxs-lookup"><span data-stu-id="db734-473">Once you have launched the application, you will see the Bot as a blue sphere in front of you.</span></span>

- <span data-ttu-id="db734-474">Utilisez le **appuyez sur le mouvement** pendant que vous sont gazing à la sphère pour engager une conversation.</span><span class="sxs-lookup"><span data-stu-id="db734-474">Use the **Tap Gesture** while you are gazing at the sphere to initiate a conversation.</span></span> 
 
- <span data-ttu-id="db734-475">Attendez que la conversation Démarrer (l’interface utilisateur affiche un message lorsque cela se produit).</span><span class="sxs-lookup"><span data-stu-id="db734-475">Wait for the conversation to start (The UI will display a message when it happens).</span></span> <span data-ttu-id="db734-476">Une fois que vous recevez le message de présentation à partir du robot, appuyez à nouveau sur le Bot afin qu’il sera en rouge et commence à écouter votre voix.</span><span class="sxs-lookup"><span data-stu-id="db734-476">Once you receive the introductory message from the Bot, tap again on the Bot so it will turn red and begin to listen to your voice.</span></span> 

- <span data-ttu-id="db734-477">Une fois que vous arrêtez de parler, votre application enverra votre message au robot et vous recevrez rapidement une réponse qui sera affichée dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db734-477">Once you stop talking, your application will send your message to the Bot and you will promptly receive a response that will be displayed in the UI.</span></span> 

- <span data-ttu-id="db734-478">Répétez le processus pour envoyer plusieurs messages à votre robot (vous devez appuyer sur chaque fois que vous souhaitez envoyer un message).</span><span class="sxs-lookup"><span data-stu-id="db734-478">Repeat the process to send more messages to your Bot (you have to tap each time you want to sen a message).</span></span>

<span data-ttu-id="db734-479">Cette conversation montre comment le robot puisse conserver des informations (votre nom), tout en fournissant également des informations connues (par exemple, les éléments qui sont stockés).</span><span class="sxs-lookup"><span data-stu-id="db734-479">This conversation demonstrates how the Bot can retain information (your name), whilst also providing known information (such as the items that are stocked).</span></span>

#### <a name="some-questions-to-ask-the-bot"></a><span data-ttu-id="db734-480">Certaines questions à poser au robot :</span><span class="sxs-lookup"><span data-stu-id="db734-480">Some questions to ask the Bot:</span></span>

```
what do you sell? 

how much are umbrellas?

how much are raincoats?
```

## <a name="your-finished-web-app-bot-v4-application"></a><span data-ttu-id="db734-481">Votre application Web App Bot (v4) terminée</span><span class="sxs-lookup"><span data-stu-id="db734-481">Your finished Web App Bot (v4) application</span></span>

<span data-ttu-id="db734-482">Félicitations, vous avez créé une application de réalité mixte qui met à profit les Azure Web App Bot v4 de Microsoft Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="db734-482">Congratulations, you built a mixed reality app that leverages the Azure Web App Bot, Microsoft Bot Framework v4.</span></span>

![Produit final](images/AzureLabs-Lab312-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="db734-484">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="db734-484">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="db734-485">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="db734-485">Exercise 1</span></span>

<span data-ttu-id="db734-486">La structure de la conversation dans cet atelier est très simple.</span><span class="sxs-lookup"><span data-stu-id="db734-486">The conversation structure in this Lab is very basic.</span></span> <span data-ttu-id="db734-487">Utilisez Microsoft LUIS pour donner à votre robot de fonctionnalités de compréhension du langage naturel.</span><span class="sxs-lookup"><span data-stu-id="db734-487">Use Microsoft LUIS to give your bot natural language understanding capabilities.</span></span>

### <a name="exercise-2"></a><span data-ttu-id="db734-488">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="db734-488">Exercise 2</span></span>

<span data-ttu-id="db734-489">Cet exemple n’inclut pas une conversation de fin d’exécution et le redémarrage d’un autre.</span><span class="sxs-lookup"><span data-stu-id="db734-489">This example does not include terminating a conversation and restarting a new one.</span></span> <span data-ttu-id="db734-490">Pour rendre la fonctionnalité Bot terminées, essayez d’implémenter de fermeture à la conversation.</span><span class="sxs-lookup"><span data-stu-id="db734-490">To make the Bot feature complete, try to implement closure to the conversation.</span></span>
