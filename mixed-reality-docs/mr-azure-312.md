---
title: Intégration de MR et Azure 312-bot
description: Suivez ce cours pour apprendre à créer et à déployer un robot à l’aide de Microsoft bot Framework v4 et à communiquer avec lui dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Académie, Unity, didacticiel, API, vision par ordinateur, hololens, immersif, VR, Microsoft bot Framework v4, application Web bot, robot Framework, Microsoft bot
ms.openlocfilehash: b828aa4415103d280459bd2c666004c994b3e59d
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63542519"
---
>[!NOTE]
><span data-ttu-id="4342e-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="4342e-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="4342e-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="4342e-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="4342e-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="4342e-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="4342e-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4342e-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="4342e-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="4342e-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="4342e-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="4342e-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

# <a name="mr-and-azure-312-bot-integration"></a><span data-ttu-id="4342e-110">MR et Azure 312: Intégration de bot</span><span class="sxs-lookup"><span data-stu-id="4342e-110">MR and Azure 312: Bot integration</span></span>

<span data-ttu-id="4342e-111">Dans ce cours, vous allez apprendre à créer et à déployer un robot à l’aide de Microsoft bot Framework v4 et à communiquer avec lui via une application Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="4342e-111">In this course, you will learn how to create and deploy a bot using the Microsoft Bot Framework V4 and communicate with it through a Windows Mixed Reality application.</span></span> 

![](images/AzureLabs-Lab312-00.png)

<span data-ttu-id="4342e-112">**Microsoft bot Framework v4** est un ensemble d’API conçu pour fournir aux développeurs les outils nécessaires à la création d’une application bot extensible et évolutive.</span><span class="sxs-lookup"><span data-stu-id="4342e-112">The **Microsoft Bot Framework V4** is a set of APIs designed to provide developers with the tools to build an extensible and scalable bot application.</span></span> <span data-ttu-id="4342e-113">Pour plus d’informations, consultez la [page Microsoft bot Framework](https://dev.botframework.com/) ou le [référentiel git de v4](https://github.com/Microsoft/botbuilder-dotnet/wiki).</span><span class="sxs-lookup"><span data-stu-id="4342e-113">For more information, visit the [Microsoft Bot Framework page](https://dev.botframework.com/) or the [V4 Git Repository](https://github.com/Microsoft/botbuilder-dotnet/wiki).</span></span>

<span data-ttu-id="4342e-114">À l’issue de ce cours, vous aurez créé une application Windows Mixed Reality, qui sera en mesure d’effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="4342e-114">After completing this course, you will have built a Windows Mixed Reality application, which will be able to do the following:</span></span>

1. <span data-ttu-id="4342e-115">Utilisez un **geste TAP** pour démarrer le robot à l’écoute de la voix des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="4342e-115">Use a **Tap Gesture** to start the bot listening for the users voice.</span></span>
2. <span data-ttu-id="4342e-116">Lorsque l’utilisateur a déclaré un événement, le bot tente de fournir une réponse.</span><span class="sxs-lookup"><span data-stu-id="4342e-116">When the user has said something, the bot will attempt to provide a response.</span></span>
3. <span data-ttu-id="4342e-117">Affichez la réponse des robots sous forme de texte, positionné près du bot, dans la scène Unity.</span><span class="sxs-lookup"><span data-stu-id="4342e-117">Display the bots reply as text, positioned near the bot, in the Unity Scene.</span></span>

<span data-ttu-id="4342e-118">Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception.</span><span class="sxs-lookup"><span data-stu-id="4342e-118">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="4342e-119">Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="4342e-119">This course is designed to teach you how to integrate an Azure Service with your Unity project.</span></span> <span data-ttu-id="4342e-120">C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="4342e-120">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

## <a name="device-support"></a><span data-ttu-id="4342e-121">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="4342e-121">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="4342e-122">Course</span><span class="sxs-lookup"><span data-stu-id="4342e-122">Course</span></span></th><th style="width:150px"> <span data-ttu-id="4342e-123"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="4342e-123"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="4342e-124"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="4342e-124"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="4342e-125">MR et Azure 312: Intégration de bot</span><span class="sxs-lookup"><span data-stu-id="4342e-125">MR and Azure 312: Bot integration</span></span></td><td style="text-align: center;"> <span data-ttu-id="4342e-126">✔️</span><span class="sxs-lookup"><span data-stu-id="4342e-126">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="4342e-127">✔️</span><span class="sxs-lookup"><span data-stu-id="4342e-127">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="4342e-128">Bien que ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques pour Windows Mixed Reality (VR).</span><span class="sxs-lookup"><span data-stu-id="4342e-128">While this course primarily focuses on HoloLens, you can also apply what you learn in this course to Windows Mixed Reality immersive (VR) headsets.</span></span> <span data-ttu-id="4342e-129">Étant donné que les casques immersifs ne disposent pas de caméras accessibles, vous aurez besoin d’une caméra externe connectée à votre PC.</span><span class="sxs-lookup"><span data-stu-id="4342e-129">Because immersive (VR) headsets do not have accessible cameras, you will need an external camera connected to your PC.</span></span> <span data-ttu-id="4342e-130">À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge les écouteurs immersifs (VR).</span><span class="sxs-lookup"><span data-stu-id="4342e-130">As you follow along with the course, you will see notes on any changes you might need to employ to support immersive (VR) headsets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4342e-131">Prérequis</span><span class="sxs-lookup"><span data-stu-id="4342e-131">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="4342e-132">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="4342e-132">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="4342e-133">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de la rédaction (juillet 2018).</span><span class="sxs-lookup"><span data-stu-id="4342e-133">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (July 2018).</span></span> <span data-ttu-id="4342e-134">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4342e-134">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you will find in newer software than what is listed below.</span></span>

<span data-ttu-id="4342e-135">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:</span><span class="sxs-lookup"><span data-stu-id="4342e-135">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="4342e-136">Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)</span><span class="sxs-lookup"><span data-stu-id="4342e-136">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="4342e-137">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="4342e-137">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="4342e-138">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="4342e-138">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="4342e-139">Unity 2017,4</span><span class="sxs-lookup"><span data-stu-id="4342e-139">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="4342e-140">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4342e-140">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="4342e-141">Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="4342e-141">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="4342e-142">Accès Internet pour Azure et récupération Azure bot.</span><span class="sxs-lookup"><span data-stu-id="4342e-142">Internet access for Azure, and for Azure Bot retrieval.</span></span> <span data-ttu-id="4342e-143">Pour plus d’informations, [veuillez suivre ce lien](https://dev.botframework.com/).</span><span class="sxs-lookup"><span data-stu-id="4342e-143">For more information, [please follow this link](https://dev.botframework.com/).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="4342e-144">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4342e-144">Before you start</span></span>

1.  <span data-ttu-id="4342e-145">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="4342e-145">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="4342e-146">Configurez et testez votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="4342e-146">Set up and test your HoloLens.</span></span> <span data-ttu-id="4342e-147">Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="4342e-147">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span> 
3.  <span data-ttu-id="4342e-148">Il est judicieux d’effectuer un réglage de l’étalonnage et du capteur au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="4342e-148">It is a good idea to perform Calibration and Sensor Tuning when beginning developing a new HoloLens app (sometimes it can help to perform those tasks for each user).</span></span> 

<span data-ttu-id="4342e-149">Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).</span><span class="sxs-lookup"><span data-stu-id="4342e-149">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens).</span></span>

<span data-ttu-id="4342e-150">Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="4342e-150">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

## <a name="chapter-1--create-the-bot-application"></a><span data-ttu-id="4342e-151">Chapitre 1: créer l’application bot</span><span class="sxs-lookup"><span data-stu-id="4342e-151">Chapter 1 – Create the Bot application</span></span>

<span data-ttu-id="4342e-152">La première étape consiste à créer votre robot en tant qu’application Web ASP.Net Core locale.</span><span class="sxs-lookup"><span data-stu-id="4342e-152">The first step is to create your bot as a local ASP.Net Core Web application.</span></span> <span data-ttu-id="4342e-153">Une fois que vous avez terminé et testé, vous allez le publier sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4342e-153">Once you have finished and tested it, you will publish it to the Azure Portal.</span></span>

1.  <span data-ttu-id="4342e-154">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4342e-154">Open Visual Studio.</span></span> <span data-ttu-id="4342e-155">Créez un nouveau projet, sélectionnez **application Web ASP.net Core ASP** comme type de projet (vous le trouverez sous la sous-section .net Core) et appelez-le **MyBot**.</span><span class="sxs-lookup"><span data-stu-id="4342e-155">Create a new project, select **ASP NET Core Web Application** as the project type (you will find it under the subsection .NET Core) and call it **MyBot**.</span></span> <span data-ttu-id="4342e-156">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4342e-156">Click **OK**.</span></span>

2.  <span data-ttu-id="4342e-157">Dans la fenêtre qui s’affiche, sélectionnez **vide**.</span><span class="sxs-lookup"><span data-stu-id="4342e-157">In the Window that will appear select **Empty**.</span></span> <span data-ttu-id="4342e-158">Assurez-vous également que la cible est définie sur **asp net Core 2,0** et que l’authentification est définie sur **aucune authentification**.</span><span class="sxs-lookup"><span data-stu-id="4342e-158">Also make sure the target is set to **ASP NET Core 2.0** and the Authentication is set to **No Authentication**.</span></span> <span data-ttu-id="4342e-159">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4342e-159">Click **OK**.</span></span>  

    ![Créer l’application bot](images/AzureLabs-Lab312-01.png)

3.  <span data-ttu-id="4342e-161">La solution s’ouvre maintenant.</span><span class="sxs-lookup"><span data-stu-id="4342e-161">The solution will now open.</span></span> <span data-ttu-id="4342e-162">Cliquez avec le bouton droit sur la solution **Mybot** dans le **Explorateur de solutions** , puis cliquez sur **gérer les packages NuGet pour la solution**.</span><span class="sxs-lookup"><span data-stu-id="4342e-162">Right-click on Solution **Mybot** in the **Solution Explorer** and click on **Manage NuGet Packages for Solution**.</span></span> 

    ![Créer l’application bot](images/AzureLabs-Lab312-02.png)

4.  <span data-ttu-id="4342e-164">Sous l’onglet **Parcourir** , recherchez **Microsoft. Bot. Builder. Integration. Aspnet. Core** (Assurez-vous que l’option inclure la **version préliminaire** est activée).</span><span class="sxs-lookup"><span data-stu-id="4342e-164">In the **Browse** tab, search for **Microsoft.Bot.Builder.Integration.AspNet.Core** (make sure you have **Include pre-release** checked).</span></span> <span data-ttu-id="4342e-165">Sélectionnez la version **de package 4.0.1-preview**, puis cochez les cases du projet.</span><span class="sxs-lookup"><span data-stu-id="4342e-165">Select the package version **4.0.1-preview**, and tick the project boxes.</span></span> <span data-ttu-id="4342e-166">Cliquez ensuite sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="4342e-166">Then click on **Install**.</span></span> <span data-ttu-id="4342e-167">Vous avez maintenant installé les bibliothèques nécessaires pour **bot Framework v4**.</span><span class="sxs-lookup"><span data-stu-id="4342e-167">You have now installed the libraries needed for the **Bot Framework v4**.</span></span> <span data-ttu-id="4342e-168">Fermez la page NuGet.</span><span class="sxs-lookup"><span data-stu-id="4342e-168">Close the NuGet page.</span></span>

    ![Créer l’application bot](images/AzureLabs-Lab312-03.png)

5.  <span data-ttu-id="4342e-170">Cliquez avec le bouton droit sur votre *projet*, **MyBot**, dans le **Explorateur de solutions** , puis cliquez sur **Ajouter** **|** une **classe**.</span><span class="sxs-lookup"><span data-stu-id="4342e-170">Right-click on your *Project*, **MyBot**, in the **Solution Explorer** and click on **Add** **|** **Class**.</span></span>

    ![Créer l’application bot](images/AzureLabs-Lab312-04.png)

6.  <span data-ttu-id="4342e-172">Nommez la classe **MyBot** , puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4342e-172">Name the class **MyBot** and click on **Add**.</span></span>

    ![Créer l’application bot](images/AzureLabs-Lab312-05.png)

7.  <span data-ttu-id="4342e-174">Répétez le point précédent pour créer une autre classe nommée **ConversationContext**.</span><span class="sxs-lookup"><span data-stu-id="4342e-174">Repeat the previous point, to create another class named **ConversationContext**.</span></span> 

8.  <span data-ttu-id="4342e-175">Cliquez avec le bouton droit sur **wwwroot** dans le **Explorateur de solutions** , puis cliquez sur **Ajouter** **|** **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="4342e-175">Right-click on **wwwroot** in the **Solution Explorer** and click on **Add** **|** **New Item**.</span></span> <span data-ttu-id="4342e-176">Sélectionnez **page HTML** (vous la trouverez sous la sous-section Web).</span><span class="sxs-lookup"><span data-stu-id="4342e-176">Select  **HTML Page** (you will find it under the subsection Web).</span></span> <span data-ttu-id="4342e-177">Nommez le fichier **default. html**.</span><span class="sxs-lookup"><span data-stu-id="4342e-177">Name the file **default.html**.</span></span> <span data-ttu-id="4342e-178">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4342e-178">Click **Add**.</span></span>

    ![Créer l’application bot](images/AzureLabs-Lab312-06.png)

9.  <span data-ttu-id="4342e-180">La liste des classes/objets dans le **Explorateur de solutions** doit ressembler à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4342e-180">The list of classes / objects in the **Solution Explorer** should look like the image below.</span></span>

    ![Créer l’application bot](images/AzureLabs-Lab312-07.png)

10. <span data-ttu-id="4342e-182">Double-cliquez sur la classe **ConversationContext** .</span><span class="sxs-lookup"><span data-stu-id="4342e-182">Double-click on the **ConversationContext** class.</span></span> <span data-ttu-id="4342e-183">Cette classe est chargée de conserver les variables utilisées par le bot pour gérer le contexte de la conversation.</span><span class="sxs-lookup"><span data-stu-id="4342e-183">This class is responsible for holding the variables used by the bot to maintain the context of the conversation.</span></span> <span data-ttu-id="4342e-184">Ces valeurs de contexte de conversation sont conservées dans une instance de cette classe, car toutes les instances de la classe **MyBot** sont actualisées chaque fois qu’une activité est reçue.</span><span class="sxs-lookup"><span data-stu-id="4342e-184">These conversation context values are maintained in an instance of this class, because any instance of the **MyBot** class will refresh each time an activity is received.</span></span> <span data-ttu-id="4342e-185">Ajoutez le code suivant à la classe:</span><span class="sxs-lookup"><span data-stu-id="4342e-185">Add the following code to the class:</span></span>

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

11. <span data-ttu-id="4342e-186">Double-cliquez sur la classe **MyBot** .</span><span class="sxs-lookup"><span data-stu-id="4342e-186">Double-click on the **MyBot** class.</span></span> <span data-ttu-id="4342e-187">Cette classe hébergera les gestionnaires appelés par toute activité entrante du client.</span><span class="sxs-lookup"><span data-stu-id="4342e-187">This class will host the handlers called by any incoming activity from the customer.</span></span> <span data-ttu-id="4342e-188">Dans cette classe, vous allez ajouter le code utilisé pour créer la conversation entre le bot et le client.</span><span class="sxs-lookup"><span data-stu-id="4342e-188">In this class you will add the code used to build the conversation between the bot and the customer.</span></span> <span data-ttu-id="4342e-189">Comme mentionné précédemment, une instance de cette classe est initialisée chaque fois qu’une activité est reçue.</span><span class="sxs-lookup"><span data-stu-id="4342e-189">As mentioned earlier, an instance of this class is initialized each time an activity is received.</span></span> <span data-ttu-id="4342e-190">Ajoutez le code suivant à cette classe:</span><span class="sxs-lookup"><span data-stu-id="4342e-190">Add the following code to this class:</span></span>

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

12. <span data-ttu-id="4342e-191">Double-cliquez sur la classe **Startup** .</span><span class="sxs-lookup"><span data-stu-id="4342e-191">Double-click on the **Startup** class.</span></span> <span data-ttu-id="4342e-192">Cette classe Initialise le bot.</span><span class="sxs-lookup"><span data-stu-id="4342e-192">This class will initialize the bot.</span></span> <span data-ttu-id="4342e-193">Ajoutez le code suivant à la classe:</span><span class="sxs-lookup"><span data-stu-id="4342e-193">Add the following code to the class:</span></span>

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

13. <span data-ttu-id="4342e-194">Ouvrez le fichier de classe de **programme** et vérifiez que le code est le même que celui-ci:</span><span class="sxs-lookup"><span data-stu-id="4342e-194">Open the **Program** class file and verify the code in it is the same as the following:</span></span>

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

14. <span data-ttu-id="4342e-195">N’oubliez pas d’enregistrer vos modifications. pour ce faire, accédez à **fichier** > **enregistrer tout**, à partir de la barre d’outils en haut de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4342e-195">Remember to save your changes, to do so, go to **File** > **Save All**, from the toolbar at the top of Visual Studio.</span></span>

## <a name="chapter-2---create-the-azure-bot-service"></a><span data-ttu-id="4342e-196">Chapitre 2-créer le Azure Bot Service</span><span class="sxs-lookup"><span data-stu-id="4342e-196">Chapter 2 - Create the Azure Bot Service</span></span>

<span data-ttu-id="4342e-197">Maintenant que vous avez généré le code de votre bot, vous devez le publier dans une instance du service *Web App bot* , sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4342e-197">Now that you have built the code for your bot, you have to publish it to an instance of the *Web App Bot* Service, on the Azure Portal.</span></span> <span data-ttu-id="4342e-198">Ce chapitre vous indique comment créer et configurer le service bot sur Azure, puis comment y publier votre code.</span><span class="sxs-lookup"><span data-stu-id="4342e-198">This Chapter will show you how to create and configure the Bot Service on Azure and then publish your code to it.</span></span>

1.  <span data-ttu-id="4342e-199">Tout d’abord, connectez-vous au portail https://portal.azure.com) Azure (.</span><span class="sxs-lookup"><span data-stu-id="4342e-199">First, log in to the Azure Portal (https://portal.azure.com).</span></span> 

    1. <span data-ttu-id="4342e-200">Si vous n’avez pas encore de compte Azure, vous devez en créer un.</span><span class="sxs-lookup"><span data-stu-id="4342e-200">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="4342e-201">Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="4342e-201">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="4342e-202">Une fois que vous êtes connecté, cliquez sur **créer une ressource** dans le coin supérieur gauche et recherchez *Web App bot*, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="4342e-202">Once you are logged in, click on **Create a resource** in the top left corner, and search for *Web App bot*, and click **Enter**.</span></span>

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-08.png)
 
3.  <span data-ttu-id="4342e-204">La nouvelle page fournit une description du service *Web App bot* .</span><span class="sxs-lookup"><span data-stu-id="4342e-204">The new page will provide a description of the *Web App Bot* Service.</span></span> <span data-ttu-id="4342e-205">En bas à gauche de cette page, cliquez sur le bouton **créer** pour créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="4342e-205">At the bottom left of this page, select the **Create** button, to create an association with this Service.</span></span>

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-09.png)
 
4.  <span data-ttu-id="4342e-207">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="4342e-207">Once you have clicked on **Create**:</span></span>

    1. <span data-ttu-id="4342e-208">Insérez le **nom** de votre choix pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="4342e-208">Insert your desired **Name** for this Service instance.</span></span>
    2. <span data-ttu-id="4342e-209">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="4342e-209">Select a **Subscription**.</span></span>
    3. <span data-ttu-id="4342e-210">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="4342e-210">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="4342e-211">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4342e-211">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="4342e-212">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.</span><span class="sxs-lookup"><span data-stu-id="4342e-212">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

        > <span data-ttu-id="4342e-213">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, [veuillez suivre ce lien](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)</span><span class="sxs-lookup"><span data-stu-id="4342e-213">If you wish to read more about Azure Resource Groups, [please follow this link](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)</span></span>

    4. <span data-ttu-id="4342e-214">Déterminez l’emplacement de votre groupe de ressources (si vous créez un groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="4342e-214">Determine the Location for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="4342e-215">L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait.</span><span class="sxs-lookup"><span data-stu-id="4342e-215">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="4342e-216">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="4342e-216">Some Azure assets are only available in certain regions.</span></span>
    5. <span data-ttu-id="4342e-217">Sélectionnez le **niveau tarifaire** approprié, s’il s’agit de la première fois que vous créez un service *Web App bot* , vous devez disposer d’un niveau gratuit (nommé F0).</span><span class="sxs-lookup"><span data-stu-id="4342e-217">Select the **Pricing Tier** appropriate for you, if this is the first time creating a *Web App Bot* Service, a free tier (named F0) should be available to you</span></span>
    6. <span data-ttu-id="4342e-218">Le nom de l' **application** peut simplement rester identique au *nom du robot*.</span><span class="sxs-lookup"><span data-stu-id="4342e-218">**App name** can just be left the same as the *Bot name*.</span></span> 
    7. <span data-ttu-id="4342e-219">Laissez le *modèle bot* de **base (C#)** .</span><span class="sxs-lookup"><span data-stu-id="4342e-219">Leave the *Bot template* as **Basic (C#)**.</span></span>
    8. <span data-ttu-id="4342e-220">Le *plan/emplacement App service* doit avoir été rempli automatiquement pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="4342e-220">*App service plan/Location* should have been auto-filled for your account.</span></span>
    9. <span data-ttu-id="4342e-221">Définissez le **stockage Azure** que vous souhaitez utiliser pour héberger votre robot.</span><span class="sxs-lookup"><span data-stu-id="4342e-221">Set the **Azure Storage** that you wish to use to host your Bot.</span></span> <span data-ttu-id="4342e-222">Si vous n’en avez pas déjà un, vous pouvez le créer ici.</span><span class="sxs-lookup"><span data-stu-id="4342e-222">If you dont have one already, you can create it here.</span></span>
    10. <span data-ttu-id="4342e-223">Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.</span><span class="sxs-lookup"><span data-stu-id="4342e-223">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>
    11. <span data-ttu-id="4342e-224">Cliquez sur créer.</span><span class="sxs-lookup"><span data-stu-id="4342e-224">Click Create.</span></span>
 
        ![Créer le Azure Bot Service](images/AzureLabs-Lab312-10.png)

5.  <span data-ttu-id="4342e-226">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="4342e-226">Once you have clicked on **Create**, you will have to wait for the Service to be created, this might take a minute.</span></span>

6.  <span data-ttu-id="4342e-227">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="4342e-227">A notification will appear in the Portal once the Service instance is created.</span></span>

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-11.png) 
 
7.  <span data-ttu-id="4342e-229">Cliquez sur la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="4342e-229">Click on the notification to explore your new Service instance.</span></span> 

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-12.png)
 
8. <span data-ttu-id="4342e-231">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="4342e-231">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="4342e-232">Vous êtes dirigé vers votre nouvelle instance de service Azure.</span><span class="sxs-lookup"><span data-stu-id="4342e-232">You will be taken to your new Azure Service instance.</span></span> 

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-13.png)
 
9.  <span data-ttu-id="4342e-234">À ce stade, vous devez configurer une fonctionnalité appelée **ligne directe** pour permettre à votre application cliente de communiquer avec ce service bot.</span><span class="sxs-lookup"><span data-stu-id="4342e-234">At this point you need to setup a feature called **Direct Line** to allow your client application to communicate with this Bot Service.</span></span> <span data-ttu-id="4342e-235">Cliquez sur **canaux**, puis dans la section **Ajouter un canal** à la une, cliquez sur **configurer le canal direct line**.</span><span class="sxs-lookup"><span data-stu-id="4342e-235">Click on **Channels**, then in the **Add a featured channel** section, click on **Configure Direct Line channel**.</span></span>

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-14.png)

10. <span data-ttu-id="4342e-237">Dans cette page, vous trouverez les **clés secrètes** qui permettront à votre application cliente de s’authentifier auprès du bot.</span><span class="sxs-lookup"><span data-stu-id="4342e-237">In this page you will find the **Secret keys** that will allow your client app to authenticate with the bot.</span></span> <span data-ttu-id="4342e-238">Cliquez sur le bouton **Afficher** et prenez une copie de l’une des clés affichées, car vous en aurez besoin plus tard dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="4342e-238">Click on the **Show** button and take a copy of one of the displayed Keys, as you will need this later in your project.</span></span> 

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-15.png)

## <a name="chapter-3--publish-the-bot-to-the-azure-web-app-bot-service"></a><span data-ttu-id="4342e-240">Chapitre 3: publier le robot sur le service bot de l’application Web Azure</span><span class="sxs-lookup"><span data-stu-id="4342e-240">Chapter 3 – Publish the Bot to the Azure Web App Bot Service</span></span>

<span data-ttu-id="4342e-241">Maintenant que votre service est prêt, vous devez publier votre code de robot, que vous avez créé précédemment, sur le service de robot d’application Web que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="4342e-241">Now that your Service is ready, you need to publish your Bot code, that you built previously, to your newly created Web App Bot Service.</span></span>

> [!NOTE] 
> <span data-ttu-id="4342e-242">Vous devez publier votre robot sur le service Azure chaque fois que vous apportez des modifications à la solution ou au code du bot.</span><span class="sxs-lookup"><span data-stu-id="4342e-242">You will have to publish your Bot to the Azure Service every time you make changes to the Bot solution / code.</span></span>

1.  <span data-ttu-id="4342e-243">Revenez à votre solution Visual Studio que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="4342e-243">Go back to your Visual Studio Solution that you created previously.</span></span> 
2.  <span data-ttu-id="4342e-244">Cliquez avec le bouton droit sur votre projet **MyBot** , dans le **Explorateur de solutions**, puis cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="4342e-244">Right-click on your **MyBot** project, in the **Solution Explorer**, then click on **Publish**.</span></span>

    ![Publier le robot sur le service bot de l’application Web Azure](images/AzureLabs-Lab312-16.png)

3.  <span data-ttu-id="4342e-246">Sur la page *choisir une cible de publication* , cliquez sur **app service**, puis **Sélectionnez existant**. Enfin, cliquez sur **créer un profil** (vous devrez peut-être cliquer sur la flèche déroulante à côté du bouton *publier* , si ce n’est pas visible).</span><span class="sxs-lookup"><span data-stu-id="4342e-246">On the *Pick a publish target* page, click **App Service**, then **Select Existing**, lastly click on **Create Profile** (you may need to click on the dropdown arrow alongside the *Publish* button, if this is not visible).</span></span>

    ![Publier le robot sur le service bot de l’application Web Azure](images/AzureLabs-Lab312-17.png)

4. <span data-ttu-id="4342e-248">Si vous n’êtes pas encore connecté à votre compte Microsoft, vous devez le faire ici.</span><span class="sxs-lookup"><span data-stu-id="4342e-248">If you are not yet logged in into your Microsoft Account, you have to do it here.</span></span>
5. <span data-ttu-id="4342e-249">Sur la page **publier** , vous devez définir le même **abonnement** que celui utilisé pour la création du service *Web App bot* .</span><span class="sxs-lookup"><span data-stu-id="4342e-249">On the **Publish** page you will find you have to set the same **Subscription** that you used for the *Web App Bot* Service creation.</span></span> <span data-ttu-id="4342e-250">Ensuite, définissez la **vue** en tant que **groupe de ressources** , puis, dans la structure de dossiers déroulante, sélectionnez le groupe de **ressources** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4342e-250">Then set the **View** as **Resource Group** and, in the drop down folder structure, select the **Resource Group** you have created previously.</span></span> <span data-ttu-id="4342e-251">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4342e-251">Click **OK**.</span></span> 

    ![Publier le robot sur le service bot de l’application Web Azure](images/AzureLabs-Lab312-18.png)

6.  <span data-ttu-id="4342e-253">Cliquez maintenant sur le bouton **publier** et attendez la publication du robot (cela peut prendre quelques minutes).</span><span class="sxs-lookup"><span data-stu-id="4342e-253">Now click on the **Publish** button, and wait for the Bot to be published (it might take a few minutes).</span></span>

    ![Publier le robot sur le service bot de l’application Web Azure](images/AzureLabs-Lab312-19.png)


## <a name="chapter-4--set-up-the-unity-project"></a><span data-ttu-id="4342e-255">Chapitre 4 – configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="4342e-255">Chapter 4 – Set up the Unity project</span></span>

<span data-ttu-id="4342e-256">Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="4342e-256">The following is a typical set up for developing with mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="4342e-257">Ouvrez *Unity* et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="4342e-257">Open *Unity* and click **New**.</span></span> 

    ![Configurer le projet Unity](images/AzureLabs-Lab312-20.png)

2.  <span data-ttu-id="4342e-259">Vous devez maintenant fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="4342e-259">You will now need to provide a Unity project name.</span></span> <span data-ttu-id="4342e-260">Insérez le **bot Hololens**.</span><span class="sxs-lookup"><span data-stu-id="4342e-260">Insert **Hololens Bot**.</span></span> <span data-ttu-id="4342e-261">Assurez-vous que le modèle de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="4342e-261">Make sure the project template is set to **3D**.</span></span> <span data-ttu-id="4342e-262">Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés).</span><span class="sxs-lookup"><span data-stu-id="4342e-262">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="4342e-263">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="4342e-263">Then, click **Create project**.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab312-21.png)

3.  <span data-ttu-id="4342e-265">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="4342e-265">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="4342e-266">Accédez à **modifier > préférences** puis, dans la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="4342e-266">Go to **Edit > Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="4342e-267">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="4342e-267">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="4342e-268">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="4342e-268">Close the **Preferences** window.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab312-22.png)

4.  <span data-ttu-id="4342e-270">Accédez ensuite à **fichier > paramètres de build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le bouton **changer de plateforme** pour appliquer votre sélection.</span><span class="sxs-lookup"><span data-stu-id="4342e-270">Next, go to **File > Build Settings** and select **Universal Windows Platform**, then click on the **Switch Platform** button to apply your selection.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab312-23.png)

5.  <span data-ttu-id="4342e-272">Tout en conservant les **paramètres de génération de > de fichiers** et assurez-vous que:</span><span class="sxs-lookup"><span data-stu-id="4342e-272">While still in **File > Build Settings** and make sure that:</span></span>

    1.  <span data-ttu-id="4342e-273">L' **appareil cible** est défini sur **Hololens**</span><span class="sxs-lookup"><span data-stu-id="4342e-273">**Target Device** is set to **Hololens**</span></span>

        > <span data-ttu-id="4342e-274">Pour les casques immersifs, définissez **appareil cible** sur *n’importe quel appareil*.</span><span class="sxs-lookup"><span data-stu-id="4342e-274">For the immersive headsets, set **Target Device** to *Any Device*.</span></span>

    2.  <span data-ttu-id="4342e-275">Le **type de build** est **D3D**</span><span class="sxs-lookup"><span data-stu-id="4342e-275">**Build Type** is set to **D3D**</span></span>

    3.  <span data-ttu-id="4342e-276">Le **SDK** est configuré sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="4342e-276">**SDK** is set to **Latest installed**</span></span>

    4.  <span data-ttu-id="4342e-277">**Version de Visual Studio** définie sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="4342e-277">**Visual Studio Version** is set to **Latest installed**</span></span>

    5.  <span data-ttu-id="4342e-278">La **génération et l’exécution** sont définies sur l' **ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="4342e-278">**Build and Run** is set to **Local Machine**</span></span>

    6.  <span data-ttu-id="4342e-279">Enregistrez la scène et ajoutez-la à la Build.</span><span class="sxs-lookup"><span data-stu-id="4342e-279">Save the scene and add it to the build.</span></span> 

        1. <span data-ttu-id="4342e-280">Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="4342e-280">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="4342e-281">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4342e-281">A save window will appear.</span></span>
        
            ![Configurer le projet Unity](images/AzureLabs-Lab312-24.png)

        2. <span data-ttu-id="4342e-283">Créez un dossier pour cela, ainsi que toute nouvelle scène, puis sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez- le Scenes.</span><span class="sxs-lookup"><span data-stu-id="4342e-283">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

             ![Configurer le projet Unity](images/AzureLabs-Lab312-25.png)

        3. <span data-ttu-id="4342e-285">Ouvrez le dossier scenes nouvellement créé, puis dans le champ *nom de fichier*:, tapez **BotScene**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4342e-285">Open your newly created **Scenes** folder, and then in the *File name*: text field, type **BotScene**, then click on **Save**.</span></span>

            ![Configurer le projet Unity](images/AzureLabs-Lab312-26.png)

    7. <span data-ttu-id="4342e-287">Les paramètres restants, dans **paramètres de build**, doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="4342e-287">The remaining settings, in **Build Settings**, should be left as default for now.</span></span>

6. <span data-ttu-id="4342e-288">Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* .</span><span class="sxs-lookup"><span data-stu-id="4342e-288">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span> 

    ![Configurer le projet Unity](images/AzureLabs-Lab312-27.png)

7. <span data-ttu-id="4342e-290">Dans ce volet, quelques paramètres doivent être vérifiés:</span><span class="sxs-lookup"><span data-stu-id="4342e-290">In this panel, a few settings need to be verified:</span></span>

    1. <span data-ttu-id="4342e-291">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="4342e-291">In the **Other Settings** tab:</span></span>

        1. <span data-ttu-id="4342e-292">La **version du runtime de script** doit être **expérimentale (net 4,6 équivalent)** ; la modification de cette opération nécessite un redémarrage de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="4342e-292">**Scripting Runtime Version** should be **Experimental (NET 4.6 Equivalent)**; changing this will require a restart of the Editor.</span></span>
        2. <span data-ttu-id="4342e-293">Le **backend de script** doit être **.net**</span><span class="sxs-lookup"><span data-stu-id="4342e-293">**Scripting Backend** should be **.NET**</span></span>
        3. <span data-ttu-id="4342e-294">Le **niveau de compatibilité** de l’API doit être **.net 4,6**</span><span class="sxs-lookup"><span data-stu-id="4342e-294">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![Configurer le projet Unity](images/AzureLabs-Lab312-28.png)
      
    2. <span data-ttu-id="4342e-296">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:</span><span class="sxs-lookup"><span data-stu-id="4342e-296">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="4342e-297">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="4342e-297">**InternetClient**</span></span>
        - <span data-ttu-id="4342e-298">**Cravate**</span><span class="sxs-lookup"><span data-stu-id="4342e-298">**Microphone**</span></span>

            ![Configurer le projet Unity](images/AzureLabs-Lab312-29.png)

    3. <span data-ttu-id="4342e-300">Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="4342e-300">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Configurer le projet Unity](images/AzureLabs-Lab312-30.png)

8.  <span data-ttu-id="4342e-302">De retour dans les *paramètres de build* , les projets _Unity C#_  ne sont plus grisés. Cochez la case en regard de cette option.</span><span class="sxs-lookup"><span data-stu-id="4342e-302">Back in *Build Settings* _Unity C#_ Projects is no longer greyed out; tick the checkbox next to this.</span></span> 
9.  <span data-ttu-id="4342e-303">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="4342e-303">Close the Build Settings window.</span></span>
10. <span data-ttu-id="4342e-304">Enregistrez votre scène et votre projet (**fichier > enregistrer la scène/le fichier > enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="4342e-304">Save your scene and project (**FILE > SAVE SCENE / FILE > SAVE PROJECT**).</span></span>


## <a name="chapter-5--camera-setup"></a><span data-ttu-id="4342e-305">Chapitre 5 – Configuration de l’appareil photo</span><span class="sxs-lookup"><span data-stu-id="4342e-305">Chapter 5 – Camera setup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4342e-306">Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce fichier [Azure-Mr-312-package. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20312%20-%20Bot%20integration/Azure-MR-312.unitypackage), à l’importer dans votre projet en tant que [**package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis à [continuer Chapitre 7](#chapter-7-–-create-the-botobjects-class).</span><span class="sxs-lookup"><span data-stu-id="4342e-306">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to download this [Azure-MR-312-Package.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20312%20-%20Bot%20integration/Azure-MR-312.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 7](#chapter-7-–-create-the-botobjects-class).</span></span>

1.  <span data-ttu-id="4342e-307">Dans le *panneau hiérarchie*, sélectionnez l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="4342e-307">In the *Hierarchy panel*, select the **Main Camera**.</span></span> 
2.  <span data-ttu-id="4342e-308">Une fois sélectionné, vous pouvez voir tous les composants de la **caméra principale** dans le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="4342e-308">Once selected, you will be able to see all the components of the **Main Camera** in the *Inspector panel*.</span></span>

    1. <span data-ttu-id="4342e-309">L' **objet Camera** doit être nommé **Camera main** (Notez l’orthographe)</span><span class="sxs-lookup"><span data-stu-id="4342e-309">The **Camera object** must be named **Main Camera** (note the spelling)</span></span>
    2. <span data-ttu-id="4342e-310">La balise  principale de l’appareil photo doit être définie sur **MainCamera** (Notez l’orthographe)</span><span class="sxs-lookup"><span data-stu-id="4342e-310">The Main Camera **Tag** must be set to **MainCamera** (note the spelling)</span></span>
    3. <span data-ttu-id="4342e-311">Vérifiez que la **position** de la transformation est définie sur **0, 0,** 0</span><span class="sxs-lookup"><span data-stu-id="4342e-311">Make sure the **Transform Position** is set to **0, 0, 0**</span></span>
    4. <span data-ttu-id="4342e-312">Affectez à **effacer les indicateurs** la **couleur unie**.</span><span class="sxs-lookup"><span data-stu-id="4342e-312">Set **Clear Flags** to **Solid Color**.</span></span>
    5. <span data-ttu-id="4342e-313">Définir la couleur d' **arrière-plan** du composant Camera sur **Black, alpha 0 (Code hexadécimal: #00000000)**</span><span class="sxs-lookup"><span data-stu-id="4342e-313">Set the **Background** Color of the Camera component to **Black, Alpha 0 (Hex Code: #00000000)**</span></span>

    ![Configuration de l’appareil photo](images/AzureLabs-Lab312-31.png)
 

## <a name="chapter-6--import-the-newtonsoft-library"></a><span data-ttu-id="4342e-315">Chapitre 6-importer la bibliothèque Newtonsoft</span><span class="sxs-lookup"><span data-stu-id="4342e-315">Chapter 6 – Import the Newtonsoft library</span></span>

<span data-ttu-id="4342e-316">Pour vous aider à désérialiser et à sérialiser les objets reçus et envoyés au service bot, vous devez télécharger la bibliothèque **Newtonsoft** .</span><span class="sxs-lookup"><span data-stu-id="4342e-316">To help you deserialize and serialize objects received and sent to the Bot Service you need to download the **Newtonsoft** library.</span></span> <span data-ttu-id="4342e-317">Vous trouverez ici une [version compatible déjà organisée avec la structure de dossiers Unity correcte](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20312%20-%20Bot%20integration/NewtonsoftDLL.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="4342e-317">You will find a [compatible version already organized with the correct Unity folder structure here](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20312%20-%20Bot%20integration/NewtonsoftDLL.unitypackage).</span></span> 

<span data-ttu-id="4342e-318">Pour importer la bibliothèque Newtonsoft dans votre projet, utilisez le package Unity fourni avec ce cours.</span><span class="sxs-lookup"><span data-stu-id="4342e-318">To import the Newtonsoft library into your project, use the Unity Package which came with this course.</span></span>

1.  <span data-ttu-id="4342e-319">Ajoutez le fichier *. pour Unity* à Unity à l’aide de l’option de menu**package personnalisé** du**package** > d’importation de **ressources** > .</span><span class="sxs-lookup"><span data-stu-id="4342e-319">Add the *.unitypackage* to Unity by using the **Assets** > **Import Package** > **Custom Package** menu option.</span></span>

    ![Importer la bibliothèque Newtonsoft](images/AzureLabs-Lab312-34.png)

2.  <span data-ttu-id="4342e-321">Dans la zone **importer le package Unity** qui s’affiche, vérifiez que tous les plug- **ins** sous (et y compris) sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="4342e-321">In the **Import Unity Package** box that pops up, ensure everything under (and including) **Plugins** is selected.</span></span>

    ![Importer la bibliothèque Newtonsoft](images/AzureLabs-Lab312-35.png)

3.  <span data-ttu-id="4342e-323">Cliquez sur le bouton **Importer** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="4342e-323">Click the **Import** button to add the items to your project.</span></span>

4.  <span data-ttu-id="4342e-324">Accédez au dossier **Newtonsoft** sous **plug-ins** dans la vue projet et sélectionnez le plug-in Newtonsoft.</span><span class="sxs-lookup"><span data-stu-id="4342e-324">Go to the **Newtonsoft** folder under **Plugins** in the project view and select the Newtonsoft plugin.</span></span>

    ![](images/AzureLabs-Lab312-35b.png)

5.  <span data-ttu-id="4342e-325">Une fois le plug-in Newtonsoft sélectionné, assurez -vous que **toutes les plateformes** sont décochées, vérifiez que **WSAPlayer** est également **désactivé**, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="4342e-325">With the Newtonsoft plugin selected, ensure that **Any Platform** is **unchecked**, then ensure that **WSAPlayer** is also **unchecked**, then click **Apply**.</span></span> <span data-ttu-id="4342e-326">Cela vous permet de vérifier que les fichiers sont correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="4342e-326">This is just to confirm that the files are configured correctly.</span></span>

    ![](images/AzureLabs-Lab312-35c.png)

    > [!NOTE]
    > <span data-ttu-id="4342e-327">Le marquage de ces plug-ins permet de les configurer pour qu’ils soient utilisés uniquement dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="4342e-327">Marking these plugins configures them to only be used in the Unity Editor.</span></span> <span data-ttu-id="4342e-328">Il y en a un ensemble différent dans le dossier WSA qui sera utilisé une fois que le projet est exporté d’Unity.</span><span class="sxs-lookup"><span data-stu-id="4342e-328">There are a different set of them in the WSA folder which will be used after the project is exported from Unity.</span></span>

6.  <span data-ttu-id="4342e-329">Ensuite, vous devez ouvrir le dossier **WSA** , dans le dossier **Newtonsoft** .</span><span class="sxs-lookup"><span data-stu-id="4342e-329">Next, you need to open the **WSA** folder, within the **Newtonsoft** folder.</span></span> <span data-ttu-id="4342e-330">Vous verrez une copie du même fichier que celui que vous venez de configurer.</span><span class="sxs-lookup"><span data-stu-id="4342e-330">You will see a copy of the same file you just configured.</span></span> <span data-ttu-id="4342e-331">Sélectionnez le fichier, puis, dans l’inspecteur, vérifiez que</span><span class="sxs-lookup"><span data-stu-id="4342e-331">Select the file, and then in the inspector, ensure that</span></span>
    -   <span data-ttu-id="4342e-332">**Aucune plateforme** n'  est désactivée</span><span class="sxs-lookup"><span data-stu-id="4342e-332">**Any Platform** is **unchecked**</span></span> 
    -   <span data-ttu-id="4342e-333">**uniquement** **WSAPlayer** est **activé**</span><span class="sxs-lookup"><span data-stu-id="4342e-333">**only** **WSAPlayer** is **checked**</span></span>
    -   <span data-ttu-id="4342e-334">L’option ne pas **traiter le processus** est **activée**</span><span class="sxs-lookup"><span data-stu-id="4342e-334">**Dont process** is **checked**</span></span>

    ![](images/AzureLabs-Lab312-35d.png)

## <a name="chapter-7--create-the-bottag"></a><span data-ttu-id="4342e-335">Chapitre 7: créer le BotTag</span><span class="sxs-lookup"><span data-stu-id="4342e-335">Chapter 7 – Create the BotTag</span></span>

1.  <span data-ttu-id="4342e-336">Créez un nouvel objet **tag** appelé **BotTag**.</span><span class="sxs-lookup"><span data-stu-id="4342e-336">Create a new **Tag** object called **BotTag**.</span></span> <span data-ttu-id="4342e-337">Sélectionnez la caméra principale dans la scène.</span><span class="sxs-lookup"><span data-stu-id="4342e-337">Select the Main Camera in the scene.</span></span> <span data-ttu-id="4342e-338">Cliquez sur le menu déroulant des balises dans le panneau Inspecteur.</span><span class="sxs-lookup"><span data-stu-id="4342e-338">Click on the Tag drop down menu in the Inspector panel.</span></span> <span data-ttu-id="4342e-339">Cliquez sur **Ajouter une étiquette**.</span><span class="sxs-lookup"><span data-stu-id="4342e-339">Click on **Add Tag**.</span></span>

    ![Configuration de l’appareil photo](images/AzureLabs-Lab312-32.png)
 
2.  <span data-ttu-id="4342e-341">Cliquez sur le **+** symbole.</span><span class="sxs-lookup"><span data-stu-id="4342e-341">Click on the **+** symbol.</span></span> <span data-ttu-id="4342e-342">Nommez la  nouvelle balise **BotTag**, *Save*.</span><span class="sxs-lookup"><span data-stu-id="4342e-342">Name the new **Tag** as **BotTag**, *Save*.</span></span>

    ![Configuration de l’appareil photo](images/AzureLabs-Lab312-33.png)

> [!WARNING] 
> <span data-ttu-id="4342e-344">**N’appliquez pas** les **BotTag** à l’appareil photo principal.</span><span class="sxs-lookup"><span data-stu-id="4342e-344">**Do not** apply the **BotTag** to the Main Camera.</span></span> <span data-ttu-id="4342e-345">Si vous avez effectué cette opération par inadvertance, veillez à remplacer la balise d’appareil photo principale par *MainCamera*.</span><span class="sxs-lookup"><span data-stu-id="4342e-345">If you have accidentally done this, make sure to change the Main Camera tag back to *MainCamera*.</span></span>

## <a name="chapter-8--create-the-botobjects-class"></a><span data-ttu-id="4342e-346">Chapitre 8: créer la classe BotObjects</span><span class="sxs-lookup"><span data-stu-id="4342e-346">Chapter 8 – Create the BotObjects class</span></span>

<span data-ttu-id="4342e-347">Le premier script que vous devez créer est la classe **BotObjects** , qui est une classe vide créée afin qu’une série d’autres objets de classe puisse être stockée dans le même script et accessible par d’autres scripts dans la scène.</span><span class="sxs-lookup"><span data-stu-id="4342e-347">The first script you need to create is the **BotObjects** class, which is an empty class created so that a series of other class objects can be stored within the same script and accessed by other scripts in the scene.</span></span>

<span data-ttu-id="4342e-348">La création de cette classe est purement un choix architectural, ces objets peuvent plutôt être hébergés dans le script de bot que vous allez créer plus loin dans ce cours.</span><span class="sxs-lookup"><span data-stu-id="4342e-348">The creation of this class is purely an architectural choice, these objects could instead be hosted in the Bot script that you will create later in this course.</span></span>

<span data-ttu-id="4342e-349">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="4342e-349">To create this class:</span></span> 

1.  <span data-ttu-id="4342e-350">Cliquez avec le bouton droit dans le *panneau Projet*, puis **créez > dossier**.</span><span class="sxs-lookup"><span data-stu-id="4342e-350">Right-click in the *Project panel*, then **Create > Folder**.</span></span> <span data-ttu-id="4342e-351">Nommez le dossier **scripts**.</span><span class="sxs-lookup"><span data-stu-id="4342e-351">Name the folder **Scripts**.</span></span> 

    ![Créer un dossier de scripts.](images/AzureLabs-Lab312-36.png)

2.  <span data-ttu-id="4342e-353">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="4342e-353">Double-click on the **Scripts** folder to open it.</span></span> <span data-ttu-id="4342e-354">Ensuite, dans ce dossier, cliquez avec le bouton droit, puis sélectionnez **créer > C# script**.</span><span class="sxs-lookup"><span data-stu-id="4342e-354">Then within that folder, right-click, and select **Create > C# Script**.</span></span> <span data-ttu-id="4342e-355">Nommez le script **BotObjects**.</span><span class="sxs-lookup"><span data-stu-id="4342e-355">Name the script **BotObjects**.</span></span> 

3.  <span data-ttu-id="4342e-356">Double-cliquez sur le nouveau script **BotObjects** pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="4342e-356">Double-click on the new **BotObjects** script to open it with **Visual Studio**.</span></span>

4.  <span data-ttu-id="4342e-357">Supprimez le contenu du script et remplacez-le par le code suivant:</span><span class="sxs-lookup"><span data-stu-id="4342e-357">Delete the content of the script and replace it with the following code:</span></span>

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

6.  <span data-ttu-id="4342e-358">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="4342e-358">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-9--create-the-gazeinput-class"></a><span data-ttu-id="4342e-359">Chapitre 9: créer la classe GazeInput</span><span class="sxs-lookup"><span data-stu-id="4342e-359">Chapter 9 – Create the GazeInput class</span></span>

<span data-ttu-id="4342e-360">La classe suivante que vous allez créer est la classe **GazeInput** .</span><span class="sxs-lookup"><span data-stu-id="4342e-360">The next class you are going to create is the **GazeInput** class.</span></span> <span data-ttu-id="4342e-361">Cette classe est chargée des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="4342e-361">This class is responsible for:</span></span>

- <span data-ttu-id="4342e-362">Création d’un curseur qui représentera le point de *regard* du joueur.</span><span class="sxs-lookup"><span data-stu-id="4342e-362">Creating a cursor that will represent the *gaze* of the player.</span></span>
- <span data-ttu-id="4342e-363">Détection des objets atteints par le point de présence du joueur et maintien d’une référence aux objets détectés.</span><span class="sxs-lookup"><span data-stu-id="4342e-363">Detecting objects hit by the gaze of the player, and holding a reference to detected objects.</span></span>

<span data-ttu-id="4342e-364">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="4342e-364">To create this class:</span></span> 

1.  <span data-ttu-id="4342e-365">Accédez au dossier **scripts** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4342e-365">Go to the **Scripts** folder you created previously.</span></span> 
2.  <span data-ttu-id="4342e-366">Cliquez avec le bouton droit dans le dossier, **créez > C# script**.</span><span class="sxs-lookup"><span data-stu-id="4342e-366">Right-click inside the folder, **Create > C# Script**.</span></span> <span data-ttu-id="4342e-367">Appelez le script **GazeInput**.</span><span class="sxs-lookup"><span data-stu-id="4342e-367">Call the script **GazeInput**.</span></span> 
3.  <span data-ttu-id="4342e-368">Double-cliquez sur le nouveau script **GazeInput** pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="4342e-368">Double-click on the new **GazeInput** script to open it with **Visual Studio**.</span></span>
4.  <span data-ttu-id="4342e-369">Insérez la ligne suivante juste au-dessus du nom de la classe:</span><span class="sxs-lookup"><span data-stu-id="4342e-369">Insert the following line right on top of the class name:</span></span>

    ```csharp
    /// <summary>
    /// Class responsible for the User's gaze interactions
    /// </summary>
    [System.Serializable]
    public class GazeInput : MonoBehaviour
    ```

5.  <span data-ttu-id="4342e-370">Ajoutez ensuite les variables suivantes à l’intérieur de la classe **GazeInput** , au-dessus de la méthode **Start ()** :</span><span class="sxs-lookup"><span data-stu-id="4342e-370">Then add the following variables inside the **GazeInput** class, above the **Start()** method:</span></span>

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

6.  <span data-ttu-id="4342e-371">Le code de la méthode **Start ()** doit être ajouté.</span><span class="sxs-lookup"><span data-stu-id="4342e-371">Code for **Start()** method should be added.</span></span> <span data-ttu-id="4342e-372">Cette méthode est appelée lorsque la classe est initialisée:</span><span class="sxs-lookup"><span data-stu-id="4342e-372">This will be called when the class initializes:</span></span>

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

7.  <span data-ttu-id="4342e-373">Implémentez une méthode qui instanciera et configurera le curseur en regard:</span><span class="sxs-lookup"><span data-stu-id="4342e-373">Implement a method that will instantiate and setup the gaze cursor:</span></span> 

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

8.  <span data-ttu-id="4342e-374">Implémentez les méthodes qui configurent le Raycast à partir de l’appareil photo principal et effectueront le suivi de l’objet actif actuel.</span><span class="sxs-lookup"><span data-stu-id="4342e-374">Implement the methods that will setup the Raycast from the Main Camera and will keep track of the current focused object.</span></span>

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
 
9.  <span data-ttu-id="4342e-375">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="4342e-375">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-10--create-the-bot-class"></a><span data-ttu-id="4342e-376">Chapitre 10: créer la classe bot</span><span class="sxs-lookup"><span data-stu-id="4342e-376">Chapter 10 – Create the Bot class</span></span>

<span data-ttu-id="4342e-377">Le script que vous allez créer est maintenant appelé **bot**.</span><span class="sxs-lookup"><span data-stu-id="4342e-377">The script you are going to create now is called **Bot**.</span></span> <span data-ttu-id="4342e-378">Il s’agit de la classe de base de votre application. elle stocke les éléments suivants:</span><span class="sxs-lookup"><span data-stu-id="4342e-378">This is the core class of your application, it stores:</span></span> 

- <span data-ttu-id="4342e-379">Vos informations d’identification Web App bot</span><span class="sxs-lookup"><span data-stu-id="4342e-379">Your Web App Bot credentials</span></span>
- <span data-ttu-id="4342e-380">Méthode qui collecte les commandes vocales de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4342e-380">The method that collects the user voice commands</span></span>
- <span data-ttu-id="4342e-381">La méthode nécessaire pour initier des conversations avec votre robot d’application Web</span><span class="sxs-lookup"><span data-stu-id="4342e-381">The method necessary to initiate conversations with your Web App Bot</span></span> 
- <span data-ttu-id="4342e-382">La méthode nécessaire pour envoyer des messages à votre bot d’application Web</span><span class="sxs-lookup"><span data-stu-id="4342e-382">The method necessary to send messages to your Web App Bot</span></span> 

<span data-ttu-id="4342e-383">Pour envoyer des messages au service bot, la Coroutine **SendMessageToBot ()** génère une activité, qui est un objet reconnu par le robot Framework comme données envoyées par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4342e-383">To send messages to the Bot Service, the **SendMessageToBot()** coroutine will build an activity, which is an object recognized by the Bot Framework as data sent by the user.</span></span> 
 
<span data-ttu-id="4342e-384">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="4342e-384">To create this class:</span></span> 

1. <span data-ttu-id="4342e-385">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="4342e-385">Double-click on the **Scripts** folder, to open it.</span></span> 
2. <span data-ttu-id="4342e-386">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**.</span><span class="sxs-lookup"><span data-stu-id="4342e-386">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="4342e-387">Nommez le script **bot**.</span><span class="sxs-lookup"><span data-stu-id="4342e-387">Name the script **Bot**.</span></span> 
3. <span data-ttu-id="4342e-388">Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4342e-388">Double-click on the new script to open it with Visual Studio.</span></span>
4. <span data-ttu-id="4342e-389">Mettez à jour les espaces de noms pour qu’ils soient identiques à ce qui suit, en haut de la classe **bot** :</span><span class="sxs-lookup"><span data-stu-id="4342e-389">Update the namespaces to be the same as the following, at the top of the **Bot** class:</span></span>

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.Text;
    using UnityEngine;
    using UnityEngine.Networking;
    using UnityEngine.Windows.Speech;
    ```
 
5. <span data-ttu-id="4342e-390">À l’intérieur de la classe **bot** , ajoutez les variables suivantes:</span><span class="sxs-lookup"><span data-stu-id="4342e-390">Inside the **Bot** class add the following variables:</span></span>

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
    > <span data-ttu-id="4342e-391">Veillez à insérer la **clé secrète** de votre robot dans la variable **botSecret** .</span><span class="sxs-lookup"><span data-stu-id="4342e-391">Make sure you insert your **Bot Secret Key** into the **botSecret** variable.</span></span> <span data-ttu-id="4342e-392">Vous aurez noté la **clé secrète** de votre robot au début de ce cours, au  **[Chapitre 2](#chapter-2---create-the-azure-bot-service), étape 10**.</span><span class="sxs-lookup"><span data-stu-id="4342e-392">You will have noted your **Bot Secret Key** at the beginning of this course, in **[Chapter 2](#chapter-2---create-the-azure-bot-service), step 10**.</span></span>

7. <span data-ttu-id="4342e-393">Le code pour **éveillé ()** et **Start ()** doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="4342e-393">Code for **Awake()** and **Start()** now needs to be added.</span></span> 

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

8. <span data-ttu-id="4342e-394">Ajoutez les deux gestionnaires qui sont appelés par les bibliothèques vocales au début et à la fin de la capture vocale.</span><span class="sxs-lookup"><span data-stu-id="4342e-394">Add the two handlers that are called by the speech libraries when voice capture begins and ends.</span></span> <span data-ttu-id="4342e-395">Le *DictationRecognizer* arrête automatiquement la capture de la voix de l’utilisateur quand l’utilisateur cesse de parler.</span><span class="sxs-lookup"><span data-stu-id="4342e-395">The *DictationRecognizer* will automatically stop capturing the user voice when the user stops speaking.</span></span>

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

1. <span data-ttu-id="4342e-396">Le gestionnaire suivant collecte le résultat de l’entrée vocale de l’utilisateur et appelle la Coroutine responsable de l’envoi du message au service de l’application Web.</span><span class="sxs-lookup"><span data-stu-id="4342e-396">The following handler collects the result of the user voice input and calls the coroutine responsible for sending the message to the Web App Bot Service.</span></span>

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

10. <span data-ttu-id="4342e-397">La Coroutine suivante est appelée pour commencer une conversation avec le bot.</span><span class="sxs-lookup"><span data-stu-id="4342e-397">The following coroutine is called to begin a conversation with the Bot.</span></span> <span data-ttu-id="4342e-398">Vous remarquerez qu’une fois l’appel de conversation terminé, il appellera **SendMessageToCoroutine ()** en passant une série de paramètres qui définit l’activité à envoyer au service bot sous forme de message vide.</span><span class="sxs-lookup"><span data-stu-id="4342e-398">You will notice that once the conversation call is complete, it will call the **SendMessageToCoroutine()** by passing a series of parameters that will set the activity to be sent to the Bot Service as an empty message.</span></span> <span data-ttu-id="4342e-399">Cette opération est effectuée pour inviter le service bot à lancer la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4342e-399">This is done to prompt the Bot Service to initiate the dialogue.</span></span>

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

11. <span data-ttu-id="4342e-400">La Coroutine suivante est appelée pour générer l’activité à envoyer au service bot.</span><span class="sxs-lookup"><span data-stu-id="4342e-400">The following coroutine is called to build the activity to be sent to the Bot Service.</span></span> 

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

12. <span data-ttu-id="4342e-401">La Coroutine suivante est appelée pour demander une réponse après l’envoi d’une activité au service bot.</span><span class="sxs-lookup"><span data-stu-id="4342e-401">The following coroutine is called to request a response after sending an activity to the Bot Service.</span></span> 

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

13. <span data-ttu-id="4342e-402">La dernière méthode à ajouter à cette classe est requise pour afficher le message dans la scène:</span><span class="sxs-lookup"><span data-stu-id="4342e-402">The last method to be added to this class, is required to display the message in the scene:</span></span>

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
    > <span data-ttu-id="4342e-403">Une erreur peut s’afficher dans la console de l’éditeur Unity, à propos de la classe **SceneOrganiser** manquante.</span><span class="sxs-lookup"><span data-stu-id="4342e-403">You may see an error within the Unity Editor Console, about missing the **SceneOrganiser** class.</span></span> <span data-ttu-id="4342e-404">Ignorez ce message, car vous allez créer cette classe ultérieurement dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4342e-404">Disregard this message, as you will create this class later in the tutorial.</span></span>

14.  <span data-ttu-id="4342e-405">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="4342e-405">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-11--create-the-interactions-class"></a><span data-ttu-id="4342e-406">Chapitre 11: créer la classe interactions</span><span class="sxs-lookup"><span data-stu-id="4342e-406">Chapter 11 – Create the Interactions class</span></span>

<span data-ttu-id="4342e-407">La classe que vous allez créer maintenant est appelée **interactions**.</span><span class="sxs-lookup"><span data-stu-id="4342e-407">The class you are going to create now is called **Interactions**.</span></span> <span data-ttu-id="4342e-408">Cette classe est utilisée pour détecter l’entrée de pression HoloLens de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4342e-408">This class is used to detect the HoloLens Tap Input from the user.</span></span> 

<span data-ttu-id="4342e-409">Si l’utilisateur appuie tout en regardant l’objet *bot* dans la scène, et que le bot est prêt à écouter les entrées vocales, l’objet bot change la couleur en **rouge** et commence à écouter les entrées vocales.</span><span class="sxs-lookup"><span data-stu-id="4342e-409">If the user taps while looking at the *Bot* object in the scene, and the Bot is ready to listen for voice inputs, the Bot object will change color to **red** and begin listening for voice inputs.</span></span> 

<span data-ttu-id="4342e-410">Cette classe hérite de la classe **GazeInput** , et peut donc référencer la méthode **Start ()** et les variables de cette classe, dénotées par l’utilisation de **base**.</span><span class="sxs-lookup"><span data-stu-id="4342e-410">This class inherits from the **GazeInput** class, and so is able to reference the **Start()** method and variables from that class, denoted by the use of **base**.</span></span> 
 
<span data-ttu-id="4342e-411">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="4342e-411">To create this class:</span></span>

1.  <span data-ttu-id="4342e-412">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="4342e-412">Double-click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="4342e-413">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**.</span><span class="sxs-lookup"><span data-stu-id="4342e-413">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="4342e-414">Nommez les **interactions**de script.</span><span class="sxs-lookup"><span data-stu-id="4342e-414">Name the script **Interactions**.</span></span> 
3.  <span data-ttu-id="4342e-415">Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4342e-415">Double-click on the new script to open it with Visual Studio.</span></span>
4.  <span data-ttu-id="4342e-416">Mettez à jour les espaces de noms et l’héritage de la classe de façon à ce qu’ils soient identiques à ce qui suit, en haut de la classe **interactions** :</span><span class="sxs-lookup"><span data-stu-id="4342e-416">Update the namespaces and the class inheritance to be the same as the following, at the top of the **Interactions** class:</span></span>

    ```csharp
    using UnityEngine.XR.WSA.Input;

    public class Interactions : GazeInput
    {
    ```

5.  <span data-ttu-id="4342e-417">À l’intérieur de la classe **interactions** , ajoutez la variable suivante:</span><span class="sxs-lookup"><span data-stu-id="4342e-417">Inside the **Interactions** class add the following variable:</span></span>

    ```csharp
        /// <summary>
        /// Allows input recognition with the HoloLens
        /// </summary>
        private GestureRecognizer _gestureRecognizer;
    ```
6.  <span data-ttu-id="4342e-418">Ajoutez ensuite la méthode **Start ()** :</span><span class="sxs-lookup"><span data-stu-id="4342e-418">Then add the **Start()** method:</span></span>

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

7.  <span data-ttu-id="4342e-419">Ajoutez le gestionnaire qui sera déclenché lorsque l’utilisateur effectue le mouvement TAP devant l’appareil de caméra HoloLens.</span><span class="sxs-lookup"><span data-stu-id="4342e-419">Add the handler that will be triggered when the user performs the tap gesture in front of the HoloLens camera</span></span>

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

8. <span data-ttu-id="4342e-420">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="4342e-420">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-12--create-the-sceneorganiser-class"></a><span data-ttu-id="4342e-421">Chapitre 12: créer la classe SceneOrganiser</span><span class="sxs-lookup"><span data-stu-id="4342e-421">Chapter 12 – Create the SceneOrganiser class</span></span>

<span data-ttu-id="4342e-422">La dernière classe requise dans ce Lab est appelée **SceneOrganiser**.</span><span class="sxs-lookup"><span data-stu-id="4342e-422">The last class required in this Lab is called **SceneOrganiser**.</span></span> <span data-ttu-id="4342e-423">Cette classe configure la scène par programme, en ajoutant des composants et des scripts à l’appareil photo principal et en créant les objets appropriés dans la scène.</span><span class="sxs-lookup"><span data-stu-id="4342e-423">This class will setup the scene programmatically, by adding components and scripts to the Main Camera, and creating the appropriate objects in the scene.</span></span>
 
<span data-ttu-id="4342e-424">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="4342e-424">To create this class:</span></span>

1.  <span data-ttu-id="4342e-425">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="4342e-425">Double-click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="4342e-426">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**.</span><span class="sxs-lookup"><span data-stu-id="4342e-426">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="4342e-427">Nommez le script **SceneOrganiser**.</span><span class="sxs-lookup"><span data-stu-id="4342e-427">Name the script **SceneOrganiser**.</span></span> 
3.  <span data-ttu-id="4342e-428">Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4342e-428">Double-click on the new script to open it with Visual Studio.</span></span>
4.  <span data-ttu-id="4342e-429">À l’intérieur de la classe **SceneOrganiser** , ajoutez les variables suivantes:</span><span class="sxs-lookup"><span data-stu-id="4342e-429">Inside the **SceneOrganiser** class add the following variables:</span></span>

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

6.  <span data-ttu-id="4342e-430">Ajoutez ensuite les méthodes **éveillé ()** et **Start ()** :</span><span class="sxs-lookup"><span data-stu-id="4342e-430">Then add the **Awake()** and **Start()** methods:</span></span>

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

7.  <span data-ttu-id="4342e-431">Ajoutez la méthode suivante, responsable de la création de l’objet bot dans la scène et de la configuration des paramètres et des composants:</span><span class="sxs-lookup"><span data-stu-id="4342e-431">Add the following method, responsible for creating the Bot object in the scene and setting up the parameters and components:</span></span>

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

7.  <span data-ttu-id="4342e-432">Ajoutez la méthode suivante, chargée de créer l’objet d’interface utilisateur dans la scène, représentant les réponses du bot:</span><span class="sxs-lookup"><span data-stu-id="4342e-432">Add the following method, responsible for creating the UI object in the scene, representing the responses from the Bot:</span></span>

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

8.  <span data-ttu-id="4342e-433">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="4342e-433">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>
9.  <span data-ttu-id="4342e-434">Dans l’éditeur Unity, faites glisser le script **SceneOrganiser** du dossier scripts vers l’appareil photo principal.</span><span class="sxs-lookup"><span data-stu-id="4342e-434">In the Unity Editor, drag the **SceneOrganiser** script from the Scripts folder to the Main Camera.</span></span> <span data-ttu-id="4342e-435">Le composant organisateur de scène doit maintenant apparaître sur l’objet caméra principal, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4342e-435">The Scene Organiser component should now appear on the Main Camera object, as shown in the image below.</span></span>

    ![Créer le Azure Bot Service](images/AzureLabs-Lab312-37.png)

## <a name="chapter-13--before-building"></a><span data-ttu-id="4342e-437">Chapitre 13 – avant la génération</span><span class="sxs-lookup"><span data-stu-id="4342e-437">Chapter 13 – Before building</span></span>

<span data-ttu-id="4342e-438">Pour effectuer un test minutieux de votre application, vous devez l’chargement sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="4342e-438">To perform a thorough test of your application you will need to sideload it onto your HoloLens.</span></span>
<span data-ttu-id="4342e-439">Avant cela, assurez-vous que:</span><span class="sxs-lookup"><span data-stu-id="4342e-439">Before you do, ensure that:</span></span>

-   <span data-ttu-id="4342e-440">Tous les paramètres mentionnés dans le [**Chapitre 4**](#Chapter-4-–-Set-up-the-unity-project) sont correctement définis.</span><span class="sxs-lookup"><span data-stu-id="4342e-440">All the settings mentioned in the [**Chapter 4**](#Chapter-4-–-Set-up-the-unity-project) are set correctly.</span></span> 
-   <span data-ttu-id="4342e-441">Le script **SceneOrganiser** est attaché à l’objet **Camera principal** .</span><span class="sxs-lookup"><span data-stu-id="4342e-441">The script **SceneOrganiser** is attached to the **Main Camera** object.</span></span> 
-   <span data-ttu-id="4342e-442">Dans la classe **bot** , vérifiez que vous avez inséré la **clé secrète** de votre robot dans la variable **botSecret** .</span><span class="sxs-lookup"><span data-stu-id="4342e-442">In the **Bot** class, make sure you have inserted your **Bot Secret Key** into the **botSecret** variable.</span></span>

## <a name="chapter-14--build-and-sideload-to-the-hololens"></a><span data-ttu-id="4342e-443">Chapitre 14 – générer et chargement dans HoloLens</span><span class="sxs-lookup"><span data-stu-id="4342e-443">Chapter 14 – Build and Sideload to the HoloLens</span></span>

<span data-ttu-id="4342e-444">Tout ce qui est nécessaire pour la section Unity de ce projet est maintenant terminé. il est donc temps de la générer à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="4342e-444">Everything needed for the Unity section of this project has now been completed, so it is time to build it from Unity.</span></span>

1.  <span data-ttu-id="4342e-445">Accédez à **paramètres de build**, **fichier > paramètres de Build.** ...</span><span class="sxs-lookup"><span data-stu-id="4342e-445">Navigate to **Build Settings**, **File > Build Settings…**.</span></span>
2.  <span data-ttu-id="4342e-446">Dans la fenêtre **paramètres de build** , cliquez sur **générer**.</span><span class="sxs-lookup"><span data-stu-id="4342e-446">From the **Build Settings** window, click **Build**.</span></span>

    ![Génération de l’application à partir d’Unity](images/AzureLabs-Lab312-38.png)

3.  <span data-ttu-id="4342e-448">Si ce n’est pas déjà fait, les **projets C# Unity**.</span><span class="sxs-lookup"><span data-stu-id="4342e-448">If not already, tick **Unity C# Projects**.</span></span>
4.  <span data-ttu-id="4342e-449">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="4342e-449">Click **Build**.</span></span> <span data-ttu-id="4342e-450">Unity lance une fenêtre de l' **Explorateur de fichiers** , dans laquelle vous devez créer, puis sélectionner un dossier dans lequel générer l’application.</span><span class="sxs-lookup"><span data-stu-id="4342e-450">Unity will launch a **File Explorer** window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="4342e-451">Créez ce dossier maintenant, puis nommez-le **application**.</span><span class="sxs-lookup"><span data-stu-id="4342e-451">Create that folder now, and name it **App**.</span></span> <span data-ttu-id="4342e-452">Ensuite, avec le dossier d' **application** sélectionné, cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="4342e-452">Then with the **App** folder selected, click **Select Folder**.</span></span> 
5.  <span data-ttu-id="4342e-453">Unity commence à générer votre projet dans le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="4342e-453">Unity will begin building your project to the **App** folder.</span></span> 
6.  <span data-ttu-id="4342e-454">Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).</span><span class="sxs-lookup"><span data-stu-id="4342e-454">Once Unity has finished building (it might take some time), it will open a **File Explorer** window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

## <a name="chapter-15--deploy-to-hololens"></a><span data-ttu-id="4342e-455">Chapitre 15 – déployer dans HoloLens</span><span class="sxs-lookup"><span data-stu-id="4342e-455">Chapter 15 – Deploy to HoloLens</span></span>

<span data-ttu-id="4342e-456">Pour effectuer un déploiement sur HoloLens:</span><span class="sxs-lookup"><span data-stu-id="4342e-456">To deploy on HoloLens:</span></span>

1.  <span data-ttu-id="4342e-457">Vous aurez besoin de l’adresse IP de votre HoloLens (pour le déploiement à distance) et vérifiez que votre HoloLens est en **mode développeur**.</span><span class="sxs-lookup"><span data-stu-id="4342e-457">You will need the IP Address of your HoloLens (for Remote Deploy), and to ensure your HoloLens is in **Developer Mode**.</span></span> <span data-ttu-id="4342e-458">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="4342e-458">To do this:</span></span>

    1. <span data-ttu-id="4342e-459">Tout en portant votre HoloLens, ouvrez les **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="4342e-459">Whilst wearing your HoloLens, open the **Settings**.</span></span>
    2. <span data-ttu-id="4342e-460">Accéder au **réseau & Internet > Wi-Fi > options avancées**</span><span class="sxs-lookup"><span data-stu-id="4342e-460">Go to **Network & Internet > Wi-Fi > Advanced Options**</span></span>
    3. <span data-ttu-id="4342e-461">Notez l’adresse **IPv4** .</span><span class="sxs-lookup"><span data-stu-id="4342e-461">Note the **IPv4** address.</span></span>
    4. <span data-ttu-id="4342e-462">Ensuite, revenez aux **paramètres**, puis à **mettre à jour & > de sécurité pour les développeurs**</span><span class="sxs-lookup"><span data-stu-id="4342e-462">Next, navigate back to **Settings**, and then to **Update & Security > For Developers**</span></span> 
    5. <span data-ttu-id="4342e-463">Définissez le mode développeur sur.</span><span class="sxs-lookup"><span data-stu-id="4342e-463">Set Developer Mode On.</span></span>

2.  <span data-ttu-id="4342e-464">Accédez à votre nouvelle build Unity (le dossier de l' **application** ) et ouvrez le fichier solution avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="4342e-464">Navigate to your new Unity build (the **App** folder) and open the solution file with **Visual Studio**.</span></span>
3.  <span data-ttu-id="4342e-465">Dans la **configuration** de la solution, sélectionnez Déboguer.</span><span class="sxs-lookup"><span data-stu-id="4342e-465">In the **Solution Configuration** select **Debug**.</span></span>
4.  <span data-ttu-id="4342e-466">Dans la **plateforme**de la solution, sélectionnez **x86**, **ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="4342e-466">In the **Solution Platform**, select **x86**, **Remote Machine**.</span></span> 

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab312-39.png)
 
5.  <span data-ttu-id="4342e-468">Accédez au **menu Générer** , puis cliquez sur **déployer la solution**pour chargement l’application à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="4342e-468">Go to the **Build menu** and click on **Deploy Solution**, to sideload the application to your HoloLens.</span></span>
6.  <span data-ttu-id="4342e-469">Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prête à être lancée.</span><span class="sxs-lookup"><span data-stu-id="4342e-469">Your app should now appear in the list of installed apps on your HoloLens, ready to be launched!</span></span>

    > [!NOTE]
    > <span data-ttu-id="4342e-470">Pour effectuer un déploiement sur un casque immersif, définissez la plateforme de la **solution** sur *ordinateur local*et définissez la **configuration** sur déboguer, avec *x86* comme **plateforme**.</span><span class="sxs-lookup"><span data-stu-id="4342e-470">To deploy to immersive headset, set the **Solution Platform** to *Local Machine*, and set the **Configuration** to *Debug*, with *x86* as the **Platform**.</span></span> <span data-ttu-id="4342e-471">Déployez ensuite sur l’ordinateur local, à l’aide du **menu Générer**, en sélectionnant *déployer la solution*.</span><span class="sxs-lookup"><span data-stu-id="4342e-471">Then deploy to the local machine, using the **Build menu**, selecting *Deploy Solution*.</span></span> 

## <a name="chapter-16--using-the-application-on-the-hololens"></a><span data-ttu-id="4342e-472">Chapitre 16 – utilisation de l’application sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="4342e-472">Chapter 16 – Using the application on the HoloLens</span></span>

- <span data-ttu-id="4342e-473">Une fois que vous avez lancé l’application, vous verrez le robot comme une sphère bleue devant vous.</span><span class="sxs-lookup"><span data-stu-id="4342e-473">Once you have launched the application, you will see the Bot as a blue sphere in front of you.</span></span>

- <span data-ttu-id="4342e-474">Utilisez le **geste TAP** lorsque vous êtes Gazing de la sphère pour lancer une conversation.</span><span class="sxs-lookup"><span data-stu-id="4342e-474">Use the **Tap Gesture** while you are gazing at the sphere to initiate a conversation.</span></span> 
 
- <span data-ttu-id="4342e-475">Attendez le démarrage de la conversation (l’interface utilisateur affichera un message lorsqu’elle se produit).</span><span class="sxs-lookup"><span data-stu-id="4342e-475">Wait for the conversation to start (The UI will display a message when it happens).</span></span> <span data-ttu-id="4342e-476">Une fois que vous avez reçu le message d’introduction du bot, appuyez de nouveau sur le robot pour qu’il s’active et commence à écouter votre voix.</span><span class="sxs-lookup"><span data-stu-id="4342e-476">Once you receive the introductory message from the Bot, tap again on the Bot so it will turn red and begin to listen to your voice.</span></span> 

- <span data-ttu-id="4342e-477">Une fois que vous arrêtez de parler, votre application envoie votre message au bot. vous recevrez rapidement une réponse qui s’affichera dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4342e-477">Once you stop talking, your application will send your message to the Bot and you will promptly receive a response that will be displayed in the UI.</span></span> 

- <span data-ttu-id="4342e-478">Répétez le processus pour envoyer d’autres messages à votre bot (vous devez appuyer chaque fois que vous souhaitez envoyer un message).</span><span class="sxs-lookup"><span data-stu-id="4342e-478">Repeat the process to send more messages to your Bot (you have to tap each time you want to sen a message).</span></span>

<span data-ttu-id="4342e-479">Cette conversation démontre comment le bot peut conserver des informations (votre nom), tout en fournissant également des informations connues (telles que les éléments stockés).</span><span class="sxs-lookup"><span data-stu-id="4342e-479">This conversation demonstrates how the Bot can retain information (your name), whilst also providing known information (such as the items that are stocked).</span></span>

#### <a name="some-questions-to-ask-the-bot"></a><span data-ttu-id="4342e-480">Voici quelques questions à poser au robot:</span><span class="sxs-lookup"><span data-stu-id="4342e-480">Some questions to ask the Bot:</span></span>

```
what do you sell? 

how much are umbrellas?

how much are raincoats?
```

## <a name="your-finished-web-app-bot-v4-application"></a><span data-ttu-id="4342e-481">Votre application Web App bot (v4) terminée</span><span class="sxs-lookup"><span data-stu-id="4342e-481">Your finished Web App Bot (v4) application</span></span>

<span data-ttu-id="4342e-482">Félicitations, vous avez créé une application de réalité mixte qui s’appuie sur Azure Web App bot, Microsoft bot Framework v4.</span><span class="sxs-lookup"><span data-stu-id="4342e-482">Congratulations, you built a mixed reality app that leverages the Azure Web App Bot, Microsoft Bot Framework v4.</span></span>

![Produit final](images/AzureLabs-Lab312-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="4342e-484">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="4342e-484">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="4342e-485">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="4342e-485">Exercise 1</span></span>

<span data-ttu-id="4342e-486">La structure de la conversation dans ce laboratoire est très simple.</span><span class="sxs-lookup"><span data-stu-id="4342e-486">The conversation structure in this Lab is very basic.</span></span> <span data-ttu-id="4342e-487">Utilisez Microsoft LUIS pour offrir à vos robots des fonctionnalités de compréhension du langage naturel.</span><span class="sxs-lookup"><span data-stu-id="4342e-487">Use Microsoft LUIS to give your bot natural language understanding capabilities.</span></span>

### <a name="exercise-2"></a><span data-ttu-id="4342e-488">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="4342e-488">Exercise 2</span></span>

<span data-ttu-id="4342e-489">Cet exemple n’inclut pas l’arrêt d’une conversation et le redémarrage d’une nouvelle conversation.</span><span class="sxs-lookup"><span data-stu-id="4342e-489">This example does not include terminating a conversation and restarting a new one.</span></span> <span data-ttu-id="4342e-490">Pour que la fonctionnalité bot soit terminée, essayez d’implémenter la fermeture de la conversation.</span><span class="sxs-lookup"><span data-stu-id="4342e-490">To make the Bot feature complete, try to implement closure to the conversation.</span></span>
