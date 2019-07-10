---
title: MR et Azure 308 - les notifications entre les périphériques
description: Terminer ce cours pour apprendre à implémenter Azure Notification Hubs, Azure Functions, stockage Azure et des Tables dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, notification, fonctions, tables, les concentrateurs de notification, vr immersives, hololens,
ms.openlocfilehash: 3b6e930acd81c7d6e3addc107ec0da605d38cad1
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694606"
---
>[!NOTE]
><span data-ttu-id="74c3c-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="74c3c-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="74c3c-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="74c3c-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="74c3c-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="74c3c-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="74c3c-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="74c3c-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="74c3c-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="74c3c-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="74c3c-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="74c3c-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-and-azure-308-cross-device-notifications"></a><span data-ttu-id="74c3c-110">MR et Azure 308 : Notifications entre les périphériques</span><span class="sxs-lookup"><span data-stu-id="74c3c-110">MR and Azure 308: Cross-device notifications</span></span>

![produit final-Démarrer](images/AzureLabs-Lab8-00.png)

<span data-ttu-id="74c3c-112">Dans ce cours, vous allez apprendre à ajouter des fonctionnalités des concentrateurs de Notification à une application de réalité mixte à l’aide d’Azure Notification Hubs, les Tables Azure et Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="74c3c-112">In this course, you will learn how to add Notification Hubs capabilities to a mixed reality application using Azure Notification Hubs, Azure Tables, and Azure Functions.</span></span>

<span data-ttu-id="74c3c-113">**Azure Notification Hubs** est un service Microsoft, qui permet aux développeurs d’envoyer des notifications push ciblées et personnalisées à n’importe quelle plateforme, tout mise hors tension dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="74c3c-113">**Azure Notification Hubs** is a Microsoft service, which allows developers to send targeted and personalized push notifications to any platform, all powered within the cloud.</span></span> <span data-ttu-id="74c3c-114">Cela peut efficacement permettent aux développeurs de communiquer avec les utilisateurs finaux, ou même communiquer entre différentes applications, en fonction du scénario.</span><span class="sxs-lookup"><span data-stu-id="74c3c-114">This can effectively allow developers to communicate with end users, or even communicate between various applications, depending on the scenario.</span></span> <span data-ttu-id="74c3c-115">Pour plus d’informations, visitez le **Azure Notification Hubs** [page](https://docs.microsoft.com/azure/notification-hubs/notification-hubs-push-notification-overview).</span><span class="sxs-lookup"><span data-stu-id="74c3c-115">For more information, visit the **Azure Notification Hubs** [page](https://docs.microsoft.com/azure/notification-hubs/notification-hubs-push-notification-overview).</span></span>

<span data-ttu-id="74c3c-116">**Azure Functions** est un service Microsoft, ce qui permet aux développeurs d’exécuter de petits morceaux de code, « fonctions », dans Azure.</span><span class="sxs-lookup"><span data-stu-id="74c3c-116">**Azure Functions** is a Microsoft service, which allows developers to run small pieces of code, 'functions', in Azure.</span></span> <span data-ttu-id="74c3c-117">Cela fournit un moyen permettant de déléguer le cloud, plutôt que votre application locale, ce qui peut avoir de nombreux avantages.</span><span class="sxs-lookup"><span data-stu-id="74c3c-117">This provides a way to delegate work to the cloud, rather than your local application, which can have many benefits.</span></span> <span data-ttu-id="74c3c-118">**Azure Functions** prend en charge plusieurs langages de développement, y compris C\#, F\#, Node.js, Java et PHP.</span><span class="sxs-lookup"><span data-stu-id="74c3c-118">**Azure Functions** supports several development languages, including C\#, F\#, Node.js, Java, and PHP.</span></span> <span data-ttu-id="74c3c-119">Pour plus d’informations, visitez le **Azure Functions** [page](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span><span class="sxs-lookup"><span data-stu-id="74c3c-119">For more information, visit the **Azure Functions** [page](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span></span>

<span data-ttu-id="74c3c-120">**Les Tables Azure** est un service de cloud Microsoft, ce qui permet aux développeurs de stocker des données non structurées-SQL dans le cloud, qu’il soit facilement accessible n’importe où.</span><span class="sxs-lookup"><span data-stu-id="74c3c-120">**Azure Tables** is a Microsoft cloud service, which allows developers to store structured non-SQL data in the cloud, making it easily accessible anywhere.</span></span> <span data-ttu-id="74c3c-121">Le service est doté d’une conception sans schéma, permettant ainsi l’évolution des tables en fonction des besoins et est donc très flexible.</span><span class="sxs-lookup"><span data-stu-id="74c3c-121">The service boasts a schemaless design, allowing for the evolution of tables as needed, and thus is very flexible.</span></span> <span data-ttu-id="74c3c-122">Pour plus d’informations, visitez le **Tables Azure** [page](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)</span><span class="sxs-lookup"><span data-stu-id="74c3c-122">For more information, visit the **Azure Tables** [page](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)</span></span>

<span data-ttu-id="74c3c-123">Avoir terminé ce cours, vous aurez une réalité mixte casque immersives et l’application un PC de bureau qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="74c3c-123">Having completed this course, you will have a mixed reality immersive headset application, and a Desktop PC application, which will be able to do the following:</span></span>

1. <span data-ttu-id="74c3c-124">L’application de bureau PC permet à l’utilisateur de déplacer un objet dans l’espace 2D (X et Y), à l’aide de la souris.</span><span class="sxs-lookup"><span data-stu-id="74c3c-124">The Desktop PC app will allow the user to move an object in 2D space (X and Y), using the mouse.</span></span>

2. <span data-ttu-id="74c3c-125">Le déplacement des objets au sein de l’application de PC sera envoyé vers le cloud à l’aide de JSON, qui sera sous la forme d’une chaîne, qui contient un ID d’objet, type et transformer les informations (coordonnées X et Y).</span><span class="sxs-lookup"><span data-stu-id="74c3c-125">The movement of objects within the PC app will be sent to the cloud using JSON, which will be in the form of a string, containing an object ID, type, and transform information (X and Y coordinates).</span></span> 

3. <span data-ttu-id="74c3c-126">L’application de réalité mixte, ce qui a une scène identique à l’application de bureau, recevra les notifications concernant le déplacement d’objets, à partir du service de Notification Hubs (qui a simplement été mis à jour par l’application de PC de bureau).</span><span class="sxs-lookup"><span data-stu-id="74c3c-126">The mixed reality app, which has an identical scene to the desktop app, will receive notifications regarding object movement, from the Notification Hubs service (which has just been updated by the Desktop PC app).</span></span> 

4. <span data-ttu-id="74c3c-127">Lors de la réception d’une notification, qui contiendra l’ID d’objet, type et les informations de transformation, l’application de réalité mixte appliquera les informations reçues à son propre scène.</span><span class="sxs-lookup"><span data-stu-id="74c3c-127">Upon receiving a notification, which will contain the object ID, type, and transform information, the mixed reality app will apply the received information to its own scene.</span></span>

<span data-ttu-id="74c3c-128">Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception.</span><span class="sxs-lookup"><span data-stu-id="74c3c-128">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="74c3c-129">Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="74c3c-129">This course is designed to teach you how to integrate an Azure Service with your Unity Project.</span></span> <span data-ttu-id="74c3c-130">Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="74c3c-130">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span> <span data-ttu-id="74c3c-131">Ce cours est un didacticiel autonome, ce qui n’implique pas directement de tous les autres laboratoires réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="74c3c-131">This course is a self-contained tutorial, which does not directly involve any other Mixed Reality Labs.</span></span>

## <a name="device-support"></a><span data-ttu-id="74c3c-132">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="74c3c-132">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="74c3c-133">Cours</span><span class="sxs-lookup"><span data-stu-id="74c3c-133">Course</span></span></th><th style="width:150px"> <span data-ttu-id="74c3c-134"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="74c3c-134"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="74c3c-135"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="74c3c-135"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="74c3c-136">MR et Azure 308 : Notifications entre les périphériques</span><span class="sxs-lookup"><span data-stu-id="74c3c-136">MR and Azure 308: Cross-device notifications</span></span></td><td style="text-align: center;"> <span data-ttu-id="74c3c-137">✔️</span><span class="sxs-lookup"><span data-stu-id="74c3c-137">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="74c3c-138">✔️</span><span class="sxs-lookup"><span data-stu-id="74c3c-138">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="74c3c-139">Si ce cours se concentre principalement sur des casques Windows Mixed Reality IMMERSIFS (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours pour Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="74c3c-139">While this course primarily focuses on Windows Mixed Reality immersive (VR) headsets, you can also apply what you learn in this course to Microsoft HoloLens.</span></span> <span data-ttu-id="74c3c-140">Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="74c3c-140">As you follow along with the course, you will see notes on any changes you might need to employ to support HoloLens.</span></span> <span data-ttu-id="74c3c-141">Lorsque vous utilisez HoloLens, vous pouvez remarquer quelques echo durant la capture de la voix.</span><span class="sxs-lookup"><span data-stu-id="74c3c-141">When using HoloLens, you may notice some echo during voice capture.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74c3c-142">Prérequis</span><span class="sxs-lookup"><span data-stu-id="74c3c-142">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="74c3c-143">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="74c3c-143">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="74c3c-144">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="74c3c-144">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="74c3c-145">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous .</span><span class="sxs-lookup"><span data-stu-id="74c3c-145">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="74c3c-146">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="74c3c-146">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="74c3c-147">Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)</span><span class="sxs-lookup"><span data-stu-id="74c3c-147">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="74c3c-148">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="74c3c-148">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="74c3c-149">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="74c3c-149">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="74c3c-150">Unity 2017.4</span><span class="sxs-lookup"><span data-stu-id="74c3c-150">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="74c3c-151">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="74c3c-151">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="74c3c-152">Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="74c3c-152">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="74c3c-153">Accès à Internet pour le programme d’installation Azure et d’accéder à des Hubs de Notification</span><span class="sxs-lookup"><span data-stu-id="74c3c-153">Internet access for Azure setup and to access Notification Hubs</span></span>

## <a name="before-you-start"></a><span data-ttu-id="74c3c-154">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="74c3c-154">Before you start</span></span>

- <span data-ttu-id="74c3c-155">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="74c3c-155">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
- <span data-ttu-id="74c3c-156">Vous devez être le propriétaire de votre portail des développeurs Microsoft et votre portail de l’enregistrement d’Application, sinon vous ne devez pas autorisé à accéder à l’application dans [chapitre 2](#chapter-2---retrieve-your-new-apps-credentials).</span><span class="sxs-lookup"><span data-stu-id="74c3c-156">You must be the owner of your Microsoft Developer Portal and your Application Registration Portal, otherwise you will not have permission to access the app in [Chapter 2](#chapter-2---retrieve-your-new-apps-credentials).</span></span>

## <a name="chapter-1---create-an-application-on-the-microsoft-developer-portal"></a><span data-ttu-id="74c3c-157">Chapitre 1 : créer une application sur le portail des développeurs Microsoft</span><span class="sxs-lookup"><span data-stu-id="74c3c-157">Chapter 1 - Create an application on the Microsoft Developer Portal</span></span>

<span data-ttu-id="74c3c-158">Pour utiliser le **Azure Notification Hubs** Service, vous devez créer une Application sur le portail des développeurs Microsoft, comme votre application doivent être inscrites, afin qu’il peut envoyer et recevoir des notifications.</span><span class="sxs-lookup"><span data-stu-id="74c3c-158">To use the **Azure Notification Hubs** Service, you will need to create an Application on the Microsoft Developer Portal, as your application will need to be registered, so that it can send and receive notifications.</span></span>

1.  <span data-ttu-id="74c3c-159">Connectez-vous à la [portail des développeurs de Microsoft](https://developer.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="74c3c-159">Log in to the [Microsoft Developer Portal](https://developer.microsoft.com/dashboard).</span></span>

    > <span data-ttu-id="74c3c-160">Vous devez vous connecter à votre Account de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="74c3c-160">You will need to log in to your Microsoft Account.</span></span>

2.  <span data-ttu-id="74c3c-161">Dans le tableau de bord, cliquez sur **créer une application**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-161">From the Dashboard, click **Create a new app**.</span></span>

    ![Créer une application](images/AzureLabs-Lab8-01.png)

3.  <span data-ttu-id="74c3c-163">Une fenêtre contextuelle s’affiche, dans laquelle vous devez réserver un nom pour votre nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="74c3c-163">A popup will appear, wherein you need to reserve a name for your new app.</span></span> <span data-ttu-id="74c3c-164">Dans la zone de texte, insérez un nom approprié ; Si le nom choisi est disponible, une coche s’affiche à droite de la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="74c3c-164">In the textbox, insert an appropriate name; if the chosen name is available, a tick will appear to the right of the textbox.</span></span> <span data-ttu-id="74c3c-165">Une fois que vous avez un nom disponible inséré, cliquez sur le **réserver le nom de produit** bouton vers le bas à gauche de la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="74c3c-165">Once you have an available name inserted, click the **Reserve product name** button to the bottom left of the popup.</span></span>

    ![un nom inverse](images/AzureLabs-Lab8-02.png)

4.  <span data-ttu-id="74c3c-167">Avec l’application est maintenant créée, vous êtes prêt à passer au chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="74c3c-167">With the app now created, you are ready to move to the next Chapter.</span></span>

## <a name="chapter-2---retrieve-your-new-apps-credentials"></a><span data-ttu-id="74c3c-168">Chapitre 2 - récupérer vos nouvelles informations d’identification des applications</span><span class="sxs-lookup"><span data-stu-id="74c3c-168">Chapter 2 - Retrieve your new apps credentials</span></span>

<span data-ttu-id="74c3c-169">Connectez-vous au portail de l’inscription d’Application, où votre nouvelle application sera répertorié et récupérer les informations d’identification qui seront utilisé pour le programme d’installation le **Service de Notification Hubs** au sein de la **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-169">Log into the Application Registration Portal, where your new app will be listed, and retrieve the credentials which will be used to setup the **Notification Hubs Service** within the **Azure Portal**.</span></span>

1.  <span data-ttu-id="74c3c-170">Accédez à la [portail d’inscription des applications](http://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="74c3c-170">Navigate to the [Application Registration Portal](http://apps.dev.microsoft.com).</span></span>

    ![portail d’inscription des applications](images/AzureLabs-Lab8-03.png)

    > [!WARNING] 
    > <span data-ttu-id="74c3c-172">Vous devez utiliser votre Account Microsoft pour se connecter.</span><span class="sxs-lookup"><span data-stu-id="74c3c-172">You will need to use your Microsoft Account to Login.</span></span>  
    > <span data-ttu-id="74c3c-173">Cela **doit** Account Microsoft que vous avez utilisées dans la précédente [chapitre](#chapter-1---create-an-application-on-the-microsoft-developer-portal), avec le portail des développeurs de Store Windows.</span><span class="sxs-lookup"><span data-stu-id="74c3c-173">This **must** be the Microsoft Account which you used in the previous [Chapter](#chapter-1---create-an-application-on-the-microsoft-developer-portal), with the Windows Store Developer portal.</span></span>

2.  <span data-ttu-id="74c3c-174">Vous trouverez votre application sous le **mes applications** section.</span><span class="sxs-lookup"><span data-stu-id="74c3c-174">You will find your app under the **My applications** section.</span></span> <span data-ttu-id="74c3c-175">Une fois que vous l’avez trouvé, cliquez dessus, vous êtes redirigé vers une nouvelle page qui possède l’application nom plu **inscription**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-175">Once you have found it, click on it and you will be taken to a new page which has the app name plus **Registration**.</span></span>

    ![votre application nouvellement inscrite](images/AzureLabs-Lab8-04.png)

3.  <span data-ttu-id="74c3c-177">Défilement vers le bas de la page d’inscription pour trouver votre **Secrets d’Application** section et la **SID du Package** pour votre application.</span><span class="sxs-lookup"><span data-stu-id="74c3c-177">Scroll down the registration page to find your **Application Secrets** section and the **Package SID** for your app.</span></span> <span data-ttu-id="74c3c-178">Copiez les deux pour une utilisation avec la configuration de la **Azure Notification Hubs Service** dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="74c3c-178">Copy both for use with setting up the **Azure Notification Hubs Service** in the next Chapter.</span></span>

    ![Secrets d’application](images/AzureLabs-Lab8-05.png)

## <a name="chapter-3---setup-azure-portal-create-notification-hubs-service"></a><span data-ttu-id="74c3c-180">Chapitre 3 - le programme d’installation portail : créer le Service de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="74c3c-180">Chapter 3 - Setup Azure Portal: create Notification Hubs Service</span></span>

<span data-ttu-id="74c3c-181">Avec vos informations d’identification des applications récupéré, vous devrez accéder au portail Azure, où vous allez créer un Service de concentrateurs de Notification Azure.</span><span class="sxs-lookup"><span data-stu-id="74c3c-181">With your apps credentials retrieved, you will need to go to the Azure Portal, where you will create an Azure Notification Hubs Service.</span></span>

1.  <span data-ttu-id="74c3c-182">Connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="74c3c-182">Log into the [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="74c3c-183">Si vous n’avez pas déjà un compte Azure, vous devrez créer un.</span><span class="sxs-lookup"><span data-stu-id="74c3c-183">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="74c3c-184">Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="74c3c-184">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="74c3c-185">Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez **Hub de Notification**, puis cliquez sur ***entrée***.</span><span class="sxs-lookup"><span data-stu-id="74c3c-185">Once you are logged in, click on **New** in the top left corner, and search for **Notification Hub**, and click ***Enter***.</span></span>

    ![Recherchez le hub de notification](images/AzureLabs-Lab8-06.png)

    > [!NOTE] 
    > <span data-ttu-id="74c3c-187">Le mot ***New*** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.</span><span class="sxs-lookup"><span data-stu-id="74c3c-187">The word ***New*** may have been replaced with **Create a resource**, in newer portals.</span></span>

3.  <span data-ttu-id="74c3c-188">La nouvelle page doit fournir une description de la *Notification Hubs* service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-188">The new page will provide a description of the *Notification Hubs* service.</span></span> <span data-ttu-id="74c3c-189">En bas à gauche de cette invite, sélectionnez le **créer** bouton permettant de créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-189">At the bottom left of this prompt, select the **Create** button, to create an association with this service.</span></span>

    ![créer l’instance de hub de notification](images/AzureLabs-Lab8-07.png)

4.  <span data-ttu-id="74c3c-191">Une fois que vous avez cliqué sur ***créer***:</span><span class="sxs-lookup"><span data-stu-id="74c3c-191">Once you have clicked on ***Create***:</span></span>

    1.  <span data-ttu-id="74c3c-192">Insérez votre nom souhaité pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-192">Insert your desired name for this service instance.</span></span>

    2.  <span data-ttu-id="74c3c-193">Fournir un **espace de noms** dont vous pourrez plus l’associer à cette application.</span><span class="sxs-lookup"><span data-stu-id="74c3c-193">Provide a **namespace** which you will be able to associate with this app.</span></span>

    3.  <span data-ttu-id="74c3c-194">Sélectionnez un **emplacement.**</span><span class="sxs-lookup"><span data-stu-id="74c3c-194">Select a **Location.**</span></span>

    4.  <span data-ttu-id="74c3c-195">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="74c3c-195">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="74c3c-196">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="74c3c-196">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="74c3c-197">Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="74c3c-197">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span>

        > <span data-ttu-id="74c3c-198">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la façon de gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="74c3c-198">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage a Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span> 

    5.  <span data-ttu-id="74c3c-199">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-199">Select an appropriate **Subscription**.</span></span>

    6.  <span data-ttu-id="74c3c-200">Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-200">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    7. <span data-ttu-id="74c3c-201">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-201">Select **Create**.</span></span>

        ![Renseignez les détails du service](images/AzureLabs-Lab8-08.png)

5.  <span data-ttu-id="74c3c-203">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="74c3c-203">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

6.  <span data-ttu-id="74c3c-204">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="74c3c-204">A notification will appear in the portal once the Service instance is created.</span></span>

    ![notification](images/AzureLabs-Lab8-09.png)

7.  <span data-ttu-id="74c3c-206">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-206">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="74c3c-207">Vous serez dirigé vers votre nouvelle **Hub de Notification** instance de service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-207">You will be taken to your new **Notification Hub** service instance.</span></span>

    ![accéder à la ressource](images/AzureLabs-Lab8-10.png)
    
8.  <span data-ttu-id="74c3c-209">Dans la page Vue d’ensemble, à mi-chemin dans la page, cliquez sur **Windows (WNS).**</span><span class="sxs-lookup"><span data-stu-id="74c3c-209">From the overview page, halfway down the page, click **Windows (WNS).**</span></span> <span data-ttu-id="74c3c-210">Le volet de droite changera aux champs de texte afficher deux, qui nécessitent votre **SID du Package** et **clé de sécurité**, à partir de l’application que vous avez configurés précédemment.</span><span class="sxs-lookup"><span data-stu-id="74c3c-210">The panel on the right will change to show two text fields, which require your **Package SID** and **Security Key**, from the app you set up previously.</span></span>

    ![qui vient d’être créé service hubs](images/AzureLabs-Lab8-11.png)

9. <span data-ttu-id="74c3c-212">Une fois que vous avez copié les détails dans les champs appropriés, cliquez sur **enregistrer**, et vous recevrez une notification lorsque le Hub de Notification a été mis à jour avec succès.</span><span class="sxs-lookup"><span data-stu-id="74c3c-212">Once you have copied the details into the correct fields, click **Save**, and you will receive a notification when the Notification Hub has been successfully updated.</span></span>

    ![copier les détails de la sécurité](images/AzureLabs-Lab8-12.png)

## <a name="chapter-4---setup-azure-portal-create-table-service"></a><span data-ttu-id="74c3c-214">Chapitre 4 - le programme d’installation portail : créer le Service de Table</span><span class="sxs-lookup"><span data-stu-id="74c3c-214">Chapter 4 - Setup Azure Portal: create Table Service</span></span>

<span data-ttu-id="74c3c-215">Après avoir créé votre instance de Service de Notification Hubs, accédez à votre portail Azure, où vous allez créer un Service de Tables Azure en créant une ressource de stockage.</span><span class="sxs-lookup"><span data-stu-id="74c3c-215">After creating your Notification Hubs Service instance, navigate back to your Azure Portal, where you will create an Azure Tables Service by creating a Storage Resource.</span></span>

1.  <span data-ttu-id="74c3c-216">Si pas déjà connecté, connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="74c3c-216">If not already signed in, log into the [Azure Portal](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="74c3c-217">Une fois connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez **compte de stockage**, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-217">Once logged in, click on **New** in the top left corner, and search for **Storage account**, and click **Enter**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="74c3c-218">Le mot ***New*** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.</span><span class="sxs-lookup"><span data-stu-id="74c3c-218">The word ***New*** may have been replaced with **Create a resource**, in newer portals.</span></span>

3.  <span data-ttu-id="74c3c-219">Sélectionnez **compte de stockage - blob, fichier, table, file d’attente** à partir de la liste.</span><span class="sxs-lookup"><span data-stu-id="74c3c-219">Select **Storage account - blob, file, table, queue** from the list.</span></span>

    ![Recherchez le compte de stockage](images/AzureLabs-Lab8-13.png)

4.  <span data-ttu-id="74c3c-221">La nouvelle page doit fournir une description de la **compte de stockage** service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-221">The new page will provide a description of the **Storage account** service.</span></span> <span data-ttu-id="74c3c-222">En bas à gauche de cette invite, sélectionnez le **créer** bouton, pour créer une instance de ce service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-222">At the bottom left of this prompt, select the **Create** button, to create an instance of this service.</span></span>

    ![créer l’instance de stockage](images/AzureLabs-Lab8-14.png)

5.  <span data-ttu-id="74c3c-224">Une fois que vous avez cliqué sur **créer**, un panneau s’affiche :</span><span class="sxs-lookup"><span data-stu-id="74c3c-224">Once you have clicked on **Create**, a panel will appear:</span></span>

    1. <span data-ttu-id="74c3c-225">Insérez votre souhaitée **nom** pour cette instance de service (doit être en minuscules).</span><span class="sxs-lookup"><span data-stu-id="74c3c-225">Insert your desired **Name** for this service instance (must be all lowercase).</span></span>

    2. <span data-ttu-id="74c3c-226">Pour **modèle de déploiement**, cliquez sur **Resource manager**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-226">For **Deployment model**, click **Resource manager**.</span></span>

    3.  <span data-ttu-id="74c3c-227">Pour **type de compte**, à l’aide de la liste déroulante, sélectionnez **stockage (usage général v1)** .</span><span class="sxs-lookup"><span data-stu-id="74c3c-227">For **Account kind**, using the dropdown menu, select **Storage (general purpose v1)**.</span></span>

    4. <span data-ttu-id="74c3c-228">Sélectionnez un **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-228">Select an appropriate **Location**.</span></span>
    
    5.  <span data-ttu-id="74c3c-229">Pour le **réplication** menu déroulant, sélectionnez **en lecture-access-geo-redundant storage (RA-GRS)** .</span><span class="sxs-lookup"><span data-stu-id="74c3c-229">For the **Replication** dropdown menu, select **Read-access-geo-redundant storage (RA-GRS)**.</span></span>

    6.  <span data-ttu-id="74c3c-230">Pour **performances**, cliquez sur **Standard**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-230">For **Performance**, click **Standard**.</span></span>

    7.  <span data-ttu-id="74c3c-231">Dans le **transfert sécurisé requis** section, sélectionnez **désactivé**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-231">Within the **Secure transfer required** section, select **Disabled**.</span></span>

    8.  <span data-ttu-id="74c3c-232">À partir de la **abonnement** menu déroulant, sélectionnez un abonnement approprié.</span><span class="sxs-lookup"><span data-stu-id="74c3c-232">From the **Subscription** dropdown menu, select an appropriate subscription.</span></span>

    9.  <span data-ttu-id="74c3c-233">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="74c3c-233">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="74c3c-234">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="74c3c-234">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="74c3c-235">Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="74c3c-235">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span>

        > <span data-ttu-id="74c3c-236">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la façon de gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="74c3c-236">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage a Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    10. <span data-ttu-id="74c3c-237">Laissez **réseaux virtuels** comme **désactivé** s’il s’agit d’une option pour vous.</span><span class="sxs-lookup"><span data-stu-id="74c3c-237">Leave **Virtual networks** as **Disabled** if this is an option for you.</span></span>

    11. <span data-ttu-id="74c3c-238">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-238">Click **Create**.</span></span>

        ![Renseignez les détails de stockage](images/AzureLabs-Lab8-15.png)

6.  <span data-ttu-id="74c3c-240">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="74c3c-240">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

7.  <span data-ttu-id="74c3c-241">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="74c3c-241">A notification will appear in the portal once the Service instance is created.</span></span> <span data-ttu-id="74c3c-242">Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-242">Click on the notifications to explore your new Service instance.</span></span>

    ![nouvelle notification de stockage](images/AzureLabs-Lab8-16.png)

8.  <span data-ttu-id="74c3c-244">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-244">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="74c3c-245">Vous êtes redirigé vers votre nouvelle page de vue d’ensemble instance de Service de stockage.</span><span class="sxs-lookup"><span data-stu-id="74c3c-245">You will be taken to your new Storage Service instance overview page.</span></span>

    ![accéder à la ressource](images/AzureLabs-Lab8-17.PNG)

9. <span data-ttu-id="74c3c-247">Dans la page Vue d’ensemble, à droite, cliquez sur **Tables**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-247">From the overview page, to the right-hand side, click **Tables**.</span></span>
    
    ![](images/AzureLabs-Lab8-18.PNG)

10. <span data-ttu-id="74c3c-248">Le volet de droite change et indique le **service de Table** plus d’informations, dans laquelle vous devez ajouter une nouvelle table.</span><span class="sxs-lookup"><span data-stu-id="74c3c-248">The panel on the right will change to show the **Table service** information, wherein you need to add a new table.</span></span> <span data-ttu-id="74c3c-249">Cela en cliquant sur le **+** **Table** bouton vers le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="74c3c-249">Do this by clicking the **+** **Table** button to the top-left corner.</span></span>

    ![ouvrir des Tables](images/AzureLabs-Lab8-19.png)

11. <span data-ttu-id="74c3c-251">Une nouvelle page s’affiche, dans laquelle vous devez entrer un **nom de la Table**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-251">A new page will be shown, wherein you need to enter a **Table name**.</span></span> <span data-ttu-id="74c3c-252">Il s’agit du nom que vous utiliserez pour faire référence aux données dans votre application dans les chapitres.</span><span class="sxs-lookup"><span data-stu-id="74c3c-252">This is the name you will use to refer to the data in your application in later Chapters.</span></span> <span data-ttu-id="74c3c-253">Insérez un nom approprié et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-253">Insert an appropriate name and click **OK**.</span></span>

    ![Créer la nouvelle table](images/AzureLabs-Lab8-20.png)    

12. <span data-ttu-id="74c3c-255">Une fois que la nouvelle table a été créée, vous serez en mesure de voir dans le **service de Table** page (en bas).</span><span class="sxs-lookup"><span data-stu-id="74c3c-255">Once the new table has been created, you will be able to see it within the **Table service** page (at the bottom).</span></span>

    ![nouvelle table créée](images/AzureLabs-Lab8-21.png)
    

## <a name="chapter-5---completing-the-azure-table-in-visual-studio"></a><span data-ttu-id="74c3c-257">Chapitre 5 - fin de la Table Azure dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="74c3c-257">Chapter 5 - Completing the Azure Table in Visual Studio</span></span>

<span data-ttu-id="74c3c-258">Maintenant que votre **service de Table** compte de stockage a été configuré, il est temps d’ajouter des données, qui sera utilisé pour stocker et récupérer des informations.</span><span class="sxs-lookup"><span data-stu-id="74c3c-258">Now that your **Table service** storage account has been setup, it is time to add data to it, which will be used to store and retrieve information.</span></span> <span data-ttu-id="74c3c-259">La modification de vos Tables peut être effectuée via **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-259">The editing of your Tables can be done through **Visual Studio**.</span></span>

1.  <span data-ttu-id="74c3c-260">Ouvrez **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-260">Open **Visual Studio**.</span></span>

2.  <span data-ttu-id="74c3c-261">Dans le menu, cliquez sur **vue** > **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-261">From the menu, click **View** > **Cloud Explorer**.</span></span>

    ![Ouvrez cloud explorer](images/AzureLabs-Lab8-22.png)

3.  <span data-ttu-id="74c3c-263">Le **Cloud Explorer** s’ouvre comme un élément ancré (patient, comme le chargement peut prendre un temps).</span><span class="sxs-lookup"><span data-stu-id="74c3c-263">The **Cloud Explorer** will open as a docked item (be patient, as loading may take time).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="74c3c-264">Si l’abonnement que vous avez utilisé pour créer votre *comptes de stockage* n’est pas visible, assurez-vous d’avoir :</span><span class="sxs-lookup"><span data-stu-id="74c3c-264">If the Subscription you used to create your *Storage Accounts* is not visible, ensure that you have:</span></span> 
    > - <span data-ttu-id="74c3c-265">Ouvert une session le même compte que celui utilisé pour le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="74c3c-265">Logged in to the same account as the one you used for the Azure Portal.</span></span>
    > - <span data-ttu-id="74c3c-266">Sélectionné de votre abonnement à partir de la Page de gestion de compte (vous devrez peut-être appliquer un filtre à partir de vos paramètres de compte) :</span><span class="sxs-lookup"><span data-stu-id="74c3c-266">Selected your Subscription from the Account Management Page (you may need to apply a filter from your account settings):</span></span>  
    >
    >   ![trouver un abonnement](images/AzureLabs-Lab8-22-5.png)

4.  <span data-ttu-id="74c3c-268">Vos services cloud Azure seront affichera.</span><span class="sxs-lookup"><span data-stu-id="74c3c-268">Your Azure cloud services will be shown.</span></span> <span data-ttu-id="74c3c-269">Rechercher **comptes de stockage** et cliquez sur la flèche à gauche de cette option pour développer vos comptes.</span><span class="sxs-lookup"><span data-stu-id="74c3c-269">Find **Storage Accounts** and click the arrow to the left of that to expand your accounts.</span></span>

    ![ouvrir des comptes de stockage](images/AzureLabs-Lab8-23.png)

5.  <span data-ttu-id="74c3c-271">Une fois développé, vous avez récemment créé **compte de stockage** doit être disponible.</span><span class="sxs-lookup"><span data-stu-id="74c3c-271">Once expanded, your newly created **Storage account** should be available.</span></span> <span data-ttu-id="74c3c-272">Cliquez sur la flèche à gauche de votre stockage et recherchez une fois qui est développé, **Tables** et cliquez sur la flèche à côté de cela, pour faire apparaître le **Table** vous avez créé dans le dernier chapitre.</span><span class="sxs-lookup"><span data-stu-id="74c3c-272">Click the arrow to the left of your storage, and then once that is expanded, find **Tables** and click the arrow next to that, to reveal the **Table** you created in the last Chapter.</span></span> <span data-ttu-id="74c3c-273">Double-cliquez sur votre **Table**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-273">Double click your **Table**.</span></span>

    ![Ouvrez le tableau d’objets de scène](images/AzureLabs-Lab8-24.png)

6.  <span data-ttu-id="74c3c-275">Votre table sera ouvert dans le centre de la fenêtre Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74c3c-275">Your table will be opened in the center of your Visual Studio window.</span></span> <span data-ttu-id="74c3c-276">Cliquez sur l’icône de table avec la **+** (plus) sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="74c3c-276">Click the table icon with the **+** (plus) on it.</span></span>

    ![Ajouter une nouvelle table](images/AzureLabs-Lab8-25.png)

7.  <span data-ttu-id="74c3c-278">Une fenêtre s’affiche invite pour pouvoir *ajouter une entité*.</span><span class="sxs-lookup"><span data-stu-id="74c3c-278">A window will appear prompting for you to *Add Entity*.</span></span> <span data-ttu-id="74c3c-279">Vous allez créer trois entités au total, chacune avec plusieurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="74c3c-279">You will create three entities in total, each with several properties.</span></span> <span data-ttu-id="74c3c-280">Vous remarquerez que *PartitionKey* et *RowKey* sont déjà fournies, car elles sont utilisées par la table à rechercher vos données.</span><span class="sxs-lookup"><span data-stu-id="74c3c-280">You will notice that *PartitionKey* and *RowKey* are already provided, as these are used by the table to find your data.</span></span> 

    ![clé de partition et de ligne](images/AzureLabs-Lab8-26.png)

8. <span data-ttu-id="74c3c-282">Mise à jour le *valeur* de la **PartitionKey** et **RowKey** comme suit (n’oubliez pas d’effectuer cette opération pour chaque propriété de ligne que vous ajoutez, cependant incrémenter l’attribut RowKey chaque fois) :</span><span class="sxs-lookup"><span data-stu-id="74c3c-282">Update the *Value* of the **PartitionKey** and **RowKey** as follows (remember to do this for each row property you add, though increment the RowKey each time):</span></span>

    ![ajouter des valeurs correctes](images/AzureLabs-Lab8-26-5.png)

9.  <span data-ttu-id="74c3c-284">Cliquez sur **ajouter une propriété** pour ajouter des lignes de données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="74c3c-284">Click **Add property** to add extra rows of data.</span></span> <span data-ttu-id="74c3c-285">Faites votre premier tableau vide correspondre le tableau ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="74c3c-285">Make your first empty table match the below table.</span></span>

10. <span data-ttu-id="74c3c-286">Cliquez sur **OK** lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="74c3c-286">Click **OK** when you are finished.</span></span>

    ![Cliquez sur OK lorsque vous avez terminé](images/AzureLabs-Lab8-27.png)

    > [!WARNING] 
    > <span data-ttu-id="74c3c-288">Vérifiez que vous avez modifié le **Type** de la **X**, **Y**, et **Z**, entrées à **Double**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-288">Ensure that you have changed the **Type** of the **X**, **Y**, and **Z**, entries to **Double**.</span></span> 

11. <span data-ttu-id="74c3c-289">Vous remarquerez que votre table a maintenant une ligne de données.</span><span class="sxs-lookup"><span data-stu-id="74c3c-289">You will notice your table now has a row of data.</span></span> <span data-ttu-id="74c3c-290">Cliquez sur le **+** (icône à nouveau pour ajouter une autre entité plus).</span><span class="sxs-lookup"><span data-stu-id="74c3c-290">Click the **+** (plus) icon again to add another entity.</span></span>

    ![première ligne](images/AzureLabs-Lab8-27-5.png)

12. <span data-ttu-id="74c3c-292">Créez une propriété supplémentaire et puis définissez les valeurs de la nouvelle entité pour correspondre à celles présentées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="74c3c-292">Create an additional property, and then set the values of the new entity to match those shown below.</span></span>

    ![ajouter le cube](images/AzureLabs-Lab8-28.png)

13. <span data-ttu-id="74c3c-294">Répétez la dernière étape pour ajouter une autre entité.</span><span class="sxs-lookup"><span data-stu-id="74c3c-294">Repeat the last step to add another entity.</span></span> <span data-ttu-id="74c3c-295">Définissez les valeurs pour cette entité à celles présentées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="74c3c-295">Set the values for this entity to those shown below.</span></span>

    ![Ajouter cylindre](images/AzureLabs-Lab8-29.png)

14. <span data-ttu-id="74c3c-297">Votre table doit maintenant ressembler à celui ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="74c3c-297">Your table should now look like the one below.</span></span>

    ![table complète](images/AzureLabs-Lab8-30.png)

15. <span data-ttu-id="74c3c-299">Vous avez terminé ce chapitre.</span><span class="sxs-lookup"><span data-stu-id="74c3c-299">You have completed this Chapter.</span></span> <span data-ttu-id="74c3c-300">Veillez à enregistrer.</span><span class="sxs-lookup"><span data-stu-id="74c3c-300">Make sure to save.</span></span>

## <a name="chapter-6---create-an-azure-function-app"></a><span data-ttu-id="74c3c-301">Chapitre 6 : créer une application de fonction Azure</span><span class="sxs-lookup"><span data-stu-id="74c3c-301">Chapter 6 - Create an Azure Function App</span></span>

<span data-ttu-id="74c3c-302">Créer une application de fonction Azure qui sera appelée par l’application de bureau pour mettre à jour le **Table** servir et envoyer une notification via le **Hub de Notification**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-302">Create an Azure Function App, which will be called by the Desktop application to update the **Table** service and send a notification through the **Notification Hub**.</span></span>

<span data-ttu-id="74c3c-303">Vous devez tout d’abord, créez un fichier qui permettra à votre fonction Azure charger les bibliothèques que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="74c3c-303">First, you need to create a file that will allow your Azure Function to load the libraries you need.</span></span>

1.  <span data-ttu-id="74c3c-304">Ouvrez **le bloc-notes** (appuyez sur Windows et tapez notepad).</span><span class="sxs-lookup"><span data-stu-id="74c3c-304">Open **Notepad** (press Windows Key and type notepad).</span></span>

    ![Ouvrez le bloc-notes](images/AzureLabs-Lab8-31.png)

2.  <span data-ttu-id="74c3c-306">Avec le bloc-notes ouvert, insérer la structure JSON ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="74c3c-306">With Notepad open, insert the JSON structure below into it.</span></span> <span data-ttu-id="74c3c-307">Une fois que vous avez terminé, enregistrez-le sur votre bureau en tant que **project.json**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-307">Once you have done that, save it on your desktop as **project.json**.</span></span> <span data-ttu-id="74c3c-308">Il est important que l’attribution de noms est correcte : faire en sorte qu’il cas **n’a pas un .txt** extension de fichier.</span><span class="sxs-lookup"><span data-stu-id="74c3c-308">It is important that the naming is correct: ensure it does **NOT have a .txt** file extension.</span></span> <span data-ttu-id="74c3c-309">Ce fichier définit les bibliothèques de que votre fonction utilisera, si vous avez utilisé NuGet, il doit vous paraître familier.</span><span class="sxs-lookup"><span data-stu-id="74c3c-309">This file defines the libraries your function will use, if you have used NuGet it will look familiar.</span></span>

    ```json
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "WindowsAzure.Storage": "7.0.0",
            "Microsoft.Azure.NotificationHubs" : "1.0.9",
            "Microsoft.Azure.WebJobs.Extensions.NotificationHubs" :"1.1.0"
        }
        }
    }
    }
    ```

3.  <span data-ttu-id="74c3c-310">Connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="74c3c-310">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

4.  <span data-ttu-id="74c3c-311">Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez **Function App**, appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-311">Once you are logged in, click on **New** in the top left corner, and search for **Function App**, press **Enter**.</span></span>

    ![recherche de l’application de fonction](images/AzureLabs-Lab8-32.png)

    > [!NOTE] 
    > <span data-ttu-id="74c3c-313">Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.</span><span class="sxs-lookup"><span data-stu-id="74c3c-313">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

5.  <span data-ttu-id="74c3c-314">La nouvelle page doit fournir une description de la **Function App** service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-314">The new page will provide a description of the **Function App** service.</span></span> <span data-ttu-id="74c3c-315">En bas à gauche de cette invite, sélectionnez le **créer** bouton permettant de créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-315">At the bottom left of this prompt, select the **Create** button, to create an association with this service.</span></span>

    ![instance d’application (fonction)](images/AzureLabs-Lab8-33.png)

6.  <span data-ttu-id="74c3c-317">Une fois que vous avez cliqué sur **créer**, renseignez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="74c3c-317">Once you have clicked on **Create**, fill in the following:</span></span>

    1. <span data-ttu-id="74c3c-318">Pour **nom de l’application**, insérez votre nom souhaité pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-318">For **App name**, insert your desired name for this service instance.</span></span>

    2. <span data-ttu-id="74c3c-319">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-319">Select a **Subscription**.</span></span>

    3. <span data-ttu-id="74c3c-320">Sélectionnez le niveau de tarification approprié pour vous, si c’est la première heure de création d’un **Service Function App**, un niveau gratuit doit être disponible pour vous.</span><span class="sxs-lookup"><span data-stu-id="74c3c-320">Select the pricing tier appropriate for you, if this is the first time creating a **Function App Service**, a free tier should be available to you.</span></span>

    4. <span data-ttu-id="74c3c-321">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="74c3c-321">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="74c3c-322">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="74c3c-322">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="74c3c-323">Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="74c3c-323">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span>

        > <span data-ttu-id="74c3c-324">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la façon de gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="74c3c-324">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage a Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5. <span data-ttu-id="74c3c-325">Pour **système d’exploitation**, cliquez sur Windows, car il s’agit de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="74c3c-325">For **OS**, click Windows, as that is the intended platform.</span></span>

    6. <span data-ttu-id="74c3c-326">Sélectionnez un **Plan d’hébergement** (à l’aide de ce didacticiel est un **Plan de consommation**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-326">Select a **Hosting Plan** (this tutorial is using a **Consumption Plan**.</span></span>

    7. <span data-ttu-id="74c3c-327">Sélectionnez un **emplacement** **(choisissez le même emplacement que le stockage que vous avez créé à l’étape précédente)**</span><span class="sxs-lookup"><span data-stu-id="74c3c-327">Select a **Location** **(choose the same location as the storage you have built in the previous step)**</span></span>

    8. <span data-ttu-id="74c3c-328">Pour le **stockage** section, **vous devez sélectionner le Service de stockage que vous avez créé à l’étape précédente**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-328">For the **Storage** section, **you must select the Storage Service you created in the previous step**.</span></span>

    9. <span data-ttu-id="74c3c-329">Vous n’aurez pas *Application Insights* dans cette application, par conséquent, n’hésitez pas à laisser **hors**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-329">You will not need *Application Insights* in this app, so feel free to leave it **Off**.</span></span>

    10. <span data-ttu-id="74c3c-330">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-330">Click **Create**.</span></span>

        ![créer la nouvelle instance](images/AzureLabs-Lab8-34.png)

7.  <span data-ttu-id="74c3c-332">Une fois que vous avez cliqué sur **créer** avoir à attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="74c3c-332">Once you have clicked on **Create** you will have to wait for the service to be created, this might take a minute.</span></span>

8.  <span data-ttu-id="74c3c-333">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="74c3c-333">A notification will appear in the portal once the Service instance is created.</span></span>

    ![nouvelle notification](images/AzureLabs-Lab8-35.png)

9.  <span data-ttu-id="74c3c-335">Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-335">Click on the notifications to explore your new Service instance.</span></span>

10. <span data-ttu-id="74c3c-336">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="74c3c-336">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> 

    ![accéder à la ressource](images/AzureLabs-Lab8-36.png)

11. <span data-ttu-id="74c3c-338">Cliquez sur le **+** (plus) de l’icône située à côté *fonctions*à *créer un nouveau*.</span><span class="sxs-lookup"><span data-stu-id="74c3c-338">Click the **+** (plus) icon next to *Functions*, to *Create new*.</span></span>

    ![ajouter la nouvelle fonction](images/AzureLabs-Lab8-37.png)

12. <span data-ttu-id="74c3c-340">Dans le volet central, le **fonction** fenêtre de création s’affiche.</span><span class="sxs-lookup"><span data-stu-id="74c3c-340">Within the central panel, the **Function** creation window will appear.</span></span> <span data-ttu-id="74c3c-341">Ignorer les informations contenues dans la partie supérieure du panneau, puis cliquez sur **fonction personnalisée**, qui se trouve près du bas (dans la zone bleue, comme indiqué ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="74c3c-341">Ignore the information in the upper half of the panel, and click **Custom function**, which is located near the bottom (in the blue area, as below).</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab8-38.png)

13. <span data-ttu-id="74c3c-343">La nouvelle page au sein de la fenêtre affiche différents types de fonction.</span><span class="sxs-lookup"><span data-stu-id="74c3c-343">The new page within the window will show various function types.</span></span> <span data-ttu-id="74c3c-344">Défiler vers le bas pour afficher les types violet, puis cliquez sur **HTTP PUT** élément.</span><span class="sxs-lookup"><span data-stu-id="74c3c-344">Scroll down to view the purple types, and click **HTTP PUT** element.</span></span>

    ![HTTP put de lien](images/AzureLabs-Lab8-39.png)

    > [!IMPORTANT]
    > <span data-ttu-id="74c3c-346">Vous devrez peut-être faire défiler vers le bas la page (et cette image soit exactement la même, si les mises à jour du portail Azure ont eu lieu), toutefois, que vous recherchez un élément appelé *HTTP PUT*.</span><span class="sxs-lookup"><span data-stu-id="74c3c-346">You may have to scroll further the down the page (and this image may not look exactly the same, if Azure Portal updates have taken place), however, you are looking for an element called *HTTP PUT*.</span></span>

14. <span data-ttu-id="74c3c-347">Le **HTTP PUT** fenêtre s’affiche, où vous devez configurer la fonction (voir image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="74c3c-347">The **HTTP PUT** window will appear, where you need to configure the function (see below for image).</span></span>

    1.  <span data-ttu-id="74c3c-348">Pour **Language,** à l’aide de la liste déroulante, sélectionnez C\#.</span><span class="sxs-lookup"><span data-stu-id="74c3c-348">For **Language,** using the dropdown menu, select C\#.</span></span>

    2.  <span data-ttu-id="74c3c-349">Pour **nom,** d’entrée d’un nom approprié.</span><span class="sxs-lookup"><span data-stu-id="74c3c-349">For **Name,** input an appropriate name.</span></span>

    3.  <span data-ttu-id="74c3c-350">Dans le **niveau d’authentification** menu déroulant, sélectionnez **fonction**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-350">In the **Authentication level** dropdown menu, select **Function**.</span></span>

    4.  <span data-ttu-id="74c3c-351">Pour le **nom de la Table** section, vous devez utiliser le nom exact que vous avez utilisé pour créer votre **Table** service (y compris la même casse).</span><span class="sxs-lookup"><span data-stu-id="74c3c-351">For the **Table name** section, you need to use the exact name you used to create your **Table** service previously (including the same letter case).</span></span>

    5.  <span data-ttu-id="74c3c-352">Dans le **connexion au compte de stockage** section, utilisez le menu déroulant et sélectionnez votre compte de stockage à partir de là.</span><span class="sxs-lookup"><span data-stu-id="74c3c-352">Within the **Storage account connection** section, use the dropdown menu, and select your storage account from there.</span></span> <span data-ttu-id="74c3c-353">Si elle n’est pas là, cliquez sur le **New** lien hypertexte en même temps que le titre de section pour afficher un autre panneau, où votre compte de stockage doit être répertorié.</span><span class="sxs-lookup"><span data-stu-id="74c3c-353">If it is not there, click the **New** hyperlink alongside the section title, to show another panel, where your storage account should be listed.</span></span>

        ![nouveau stockage](images/AzureLabs-Lab8-40.png)

15. <span data-ttu-id="74c3c-355">Cliquez sur **créer** et vous recevrez une notification que vos paramètres ont été mis à jour avec succès.</span><span class="sxs-lookup"><span data-stu-id="74c3c-355">Click **Create** and you will receive a notification that your settings have been updated successfully.</span></span>

    ![créer (fonction)](images/AzureLabs-Lab8-41.png)

16. <span data-ttu-id="74c3c-357">Après avoir cliqué sur **créer**, vous serez redirigé vers l’éditeur de fonction.</span><span class="sxs-lookup"><span data-stu-id="74c3c-357">After clicking **Create**, you will be redirected to the function editor.</span></span>

    ![mettre à jour le code de fonction](images/AzureLabs-Lab8-42.png)

17. <span data-ttu-id="74c3c-359">Insérez le code suivant dans l’éditeur (fonction) (en remplaçant le code dans la fonction) :</span><span class="sxs-lookup"><span data-stu-id="74c3c-359">Insert the following code into the function editor (replacing the code in the function):</span></span>

    ```csharp
    #r "Microsoft.WindowsAzure.Storage"

    using System;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Table;
    using Microsoft.Azure.NotificationHubs;
    using Newtonsoft.Json;

    public static async Task Run(UnityGameObject gameObj, CloudTable table, IAsyncCollector<Notification> notification, TraceWriter log)
    {
        //RowKey of the table object to be changed
        string rowKey = gameObj.RowKey;

        //Retrieve the table object by its RowKey
        TableOperation operation = TableOperation.Retrieve<UnityGameObject>("UnityPartitionKey", rowKey); 

        TableResult result = table.Execute(operation);

        //Create a UnityGameObject so to set its parameters
        UnityGameObject existingGameObj = (UnityGameObject)result.Result; 

        existingGameObj.RowKey = rowKey;
        existingGameObj.X = gameObj.X;
        existingGameObj.Y = gameObj.Y;
        existingGameObj.Z = gameObj.Z;

        //Replace the table appropriate table Entity with the value of the UnityGameObject
        operation = TableOperation.Replace(existingGameObj); 

        table.Execute(operation);

        log.Verbose($"Updated object position");

        //Serialize the UnityGameObject
        string wnsNotificationPayload = JsonConvert.SerializeObject(existingGameObj);
        
        log.Info($"{wnsNotificationPayload}");

        var headers = new Dictionary<string, string>();

        headers["X-WNS-Type"] = @"wns/raw";

        //Send the raw notification to subscribed devices
        await notification.AddAsync(new WindowsNotification(wnsNotificationPayload, headers)); 

        log.Verbose($"Sent notification");
    }

    // This UnityGameObject represent a Table Entity
    public class UnityGameObject : TableEntity
    {
        public string Type { get; set; }
        public double X { get; set; }
        public double Y { get; set; }
        public double Z { get; set; }
        public string RowKey { get; set; }
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="74c3c-360">Grâce aux bibliothèques inclus, la fonction reçoit le nom et l’emplacement de l’objet qui a été déplacé dans la scène Unity (comme un C# objet, appelé **UnityGameObject**).</span><span class="sxs-lookup"><span data-stu-id="74c3c-360">Using the included libraries, the function receives the name and location of the object which was moved in the Unity scene (as a C# object, called **UnityGameObject**).</span></span> <span data-ttu-id="74c3c-361">Cet objet est ensuite utilisé pour mettre à jour les paramètres de l’objet dans la table créée.</span><span class="sxs-lookup"><span data-stu-id="74c3c-361">This object is then used to update the object parameters within the created table.</span></span> <span data-ttu-id="74c3c-362">Ensuite, la fonction effectue un appel à votre service de Notification Hub créé, qui avertit les applications de tous les abonnés.</span><span class="sxs-lookup"><span data-stu-id="74c3c-362">Following this, the function makes a call to your created Notification Hub service, which notifies all subscribed applications.</span></span>

18. <span data-ttu-id="74c3c-363">Le code en place, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-363">With the code in place, click **Save**.</span></span>

19. <span data-ttu-id="74c3c-364">Ensuite, cliquez sur le **\<** icône (flèche), sur le côté droit de la page.</span><span class="sxs-lookup"><span data-stu-id="74c3c-364">Next, click the **\<** (arrow) icon, on the right-hand side of the page.</span></span>

    ![chargement ouvrir le panneau de configuration](images/AzureLabs-Lab8-43.png)

20. <span data-ttu-id="74c3c-366">Un glisser en partant de la droite.</span><span class="sxs-lookup"><span data-stu-id="74c3c-366">A panel will slide in from the right.</span></span> <span data-ttu-id="74c3c-367">Dans ce panneau, cliquez sur **télécharger**, et un Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="74c3c-367">In that panel, click **Upload**, and a File Browser will appear.</span></span>

21. <span data-ttu-id="74c3c-368">Accédez à, puis cliquez sur, la **project.json** fichier que vous avez créé dans **le bloc-notes** précédemment, puis cliquez sur le **Open** bouton.</span><span class="sxs-lookup"><span data-stu-id="74c3c-368">Navigate to, and click, the **project.json** file, which you created in **Notepad** previously, and then click the **Open** button.</span></span> <span data-ttu-id="74c3c-369">Ce fichier définit les bibliothèques utilisées par votre fonction.</span><span class="sxs-lookup"><span data-stu-id="74c3c-369">This file defines the libraries that your function will use.</span></span>

    ![Télécharger json](images/AzureLabs-Lab8-44.png)

22. <span data-ttu-id="74c3c-371">Quand le fichier a été chargé, il apparaît dans le volet de droite.</span><span class="sxs-lookup"><span data-stu-id="74c3c-371">When the file has uploaded, it will appear in the panel on the right.</span></span> <span data-ttu-id="74c3c-372">En cliquant sur il s’ouvre dans le **fonction** éditeur.</span><span class="sxs-lookup"><span data-stu-id="74c3c-372">Clicking it will open it within the **Function** editor.</span></span> <span data-ttu-id="74c3c-373">Il doit rechercher **exactement** identique à l’image suivante (sous l’étape 23).</span><span class="sxs-lookup"><span data-stu-id="74c3c-373">It must look **exactly** the same as the next image (below step 23).</span></span>

23. <span data-ttu-id="74c3c-374">Ensuite, dans le volet gauche, sous **fonctions**, cliquez sur le **intégrer** lien.</span><span class="sxs-lookup"><span data-stu-id="74c3c-374">Then, in the panel on the left, beneath **Functions**, click the **Integrate** link.</span></span>

    ![intégrer (fonction)](images/AzureLabs-Lab8-45.png)

24. <span data-ttu-id="74c3c-376">Dans la page suivante, dans l’angle supérieur droit, cliquez sur **éditeur avancé** (comme ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="74c3c-376">On the next page, in the top right corner, click **Advanced editor** (as below).</span></span>

    ![ouvrir l’éditeur avancé](images/AzureLabs-Lab8-46.png)

25. <span data-ttu-id="74c3c-378">Un **function.json** fichier sera ouvert dans le panneau central, ce qui doit être remplacé par l’extrait de code suivant.</span><span class="sxs-lookup"><span data-stu-id="74c3c-378">A **function.json** file will be opened in the center panel, which needs to be replaced with the following code snippet.</span></span> <span data-ttu-id="74c3c-379">Définit la fonction que vous générez et les paramètres transmis à la fonction.</span><span class="sxs-lookup"><span data-stu-id="74c3c-379">This defines the function you are building and the parameters passed into the function.</span></span>

    ```json
    {
    "bindings": [
        {
        "authLevel": "function",
        "type": "httpTrigger",
        "methods": [
            "get",
            "post"
        ],
        "name": "gameObj",
        "direction": "in"
        },
        {
        "type": "table",
        "name": "table",
        "tableName": "SceneObjectsTable",
        "connection": "mrnothubstorage_STORAGE",
        "direction": "in"
        },
        {
        "type": "notificationHub",
        "direction": "out",
        "name": "notification",
        "hubName": "MR_NotHub_ServiceInstance",
        "connection": "MRNotHubNS_DefaultFullSharedAccessSignature_NH",
        "platform": "wns"
        }
    ]
    }
    ```

26. <span data-ttu-id="74c3c-380">Votre éditeur doit maintenant ressembler à l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="74c3c-380">Your editor should now look like the image below:</span></span>

    ![Revenez à l’éditeur standard](images/AzureLabs-Lab8-47.png)

27. <span data-ttu-id="74c3c-382">Vous pouvez remarquer les paramètres d’entrée que vous venez d’insérer les détails de votre table et de stockage ne peuvent pas correspondre et par conséquent doit être mis à jour avec vos informations.</span><span class="sxs-lookup"><span data-stu-id="74c3c-382">You may notice the input parameters that you have just inserted might not match your table and storage details and therefore will need to be updated with your information.</span></span> <span data-ttu-id="74c3c-383">**Ne le faites pas ici**, car il est couvert ensuite.</span><span class="sxs-lookup"><span data-stu-id="74c3c-383">**Do not do this here**, as it is covered next.</span></span> <span data-ttu-id="74c3c-384">Cliquez simplement sur le **éditeur Standard** lien, dans l’angle supérieur droit de la page, pour revenir en arrière.</span><span class="sxs-lookup"><span data-stu-id="74c3c-384">Simply click the **Standard editor** link, in the top-right corner of the page, to go back.</span></span>

28. <span data-ttu-id="74c3c-385">Dans le **éditeur Standard**, cliquez sur **Azure Table Storage (table)** , sous **entrées**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-385">Back in the **Standard editor**, click **Azure Table Storage (table)**, under **Inputs**.</span></span> 
    
    ![Entrées de table](images/AzureLabs-Lab8-47-5.png)

29. <span data-ttu-id="74c3c-387">Garantir la correspondance suivante à **votre** plus d’informations, car ils peuvent être différents (une image se trouve ci-dessous les étapes suivantes) :</span><span class="sxs-lookup"><span data-stu-id="74c3c-387">Ensure the following match to **your** information, as they may be different (there is an image below the following steps):</span></span>

    1.  <span data-ttu-id="74c3c-388">**Nom de la table**: le nom de la table que vous avez créé dans votre stockage Azure, le service de Tables.</span><span class="sxs-lookup"><span data-stu-id="74c3c-388">**Table name**: the name of the table you created within your Azure Storage, Tables service.</span></span>

    2.  <span data-ttu-id="74c3c-389">**Connexion au compte de stockage :** cliquez sur **nouveau**, qui s’affiche en même temps que le menu déroulant et un panneau s’affiche à droite de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="74c3c-389">**Storage account connection:** click **new**, which appears alongside the dropdown menu, and a panel will appear to the right of the window.</span></span>

        ![nouveau stockage](images/AzureLabs-Lab8-48.png)

        1.  <span data-ttu-id="74c3c-391">Sélectionnez votre **compte de stockage**, que vous avez créé précédemment pour héberger le **applications de fonction.**</span><span class="sxs-lookup"><span data-stu-id="74c3c-391">Select your **Storage Account**, which you created previously to host the **Function Apps.**</span></span>

        2. <span data-ttu-id="74c3c-392">Vous remarquerez que le **compte de stockage** valeur de la connexion a été créée.</span><span class="sxs-lookup"><span data-stu-id="74c3c-392">You will notice that the **Storage Account** connection value has been created.</span></span>

        3. <span data-ttu-id="74c3c-393">Veillez à appuyer sur **enregistrer** une fois que vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="74c3c-393">Make sure to press **Save** once you are done.</span></span>

    3.  <span data-ttu-id="74c3c-394">Le **entrées** page doit maintenant correspondre à l’affichage ci-dessous, **votre** plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="74c3c-394">The **Inputs** page should now match the below, showing **your** information.</span></span>

        ![entrées terminée](images/AzureLabs-Lab8-49.png)

30. <span data-ttu-id="74c3c-396">Ensuite, cliquez sur **Azure Notification Hub (notification)** : sous **sorties**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-396">Next, click **Azure Notification Hub (notification)** - under **Outputs**.</span></span> <span data-ttu-id="74c3c-397">Vérifiez les éléments suivants sont mis en correspondance avec **votre** plus d’informations, car ils peuvent être différents (une image se trouve ci-dessous les étapes suivantes) :</span><span class="sxs-lookup"><span data-stu-id="74c3c-397">Ensure the following are matched to **your** information, as they may be different (there is an image below the following steps):</span></span>

    1.  <span data-ttu-id="74c3c-398">**Nom du Hub de notification**: il s’agit du nom de votre **Hub de Notification** instance de service, vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="74c3c-398">**Notification Hub Name**: this is the name of your **Notification Hub** service instance, which you created previously.</span></span>

    2.  <span data-ttu-id="74c3c-399">**Connexion d’espace de noms notification Hubs**: cliquez sur **nouveau**, qui s’affiche en même temps que le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="74c3c-399">**Notification Hubs namespace connection**: click **new**, which appears alongside the dropdown menu.</span></span>

        ![Vérifiez les sorties](images/AzureLabs-Lab8-50.png)

    3. <span data-ttu-id="74c3c-401">Le **connexion** fenêtre contextuelle s’affiche (voir l’image ci-dessous), où vous devez sélectionner le **Namespace** de la **Hub de Notification**, que vous avez configuré précédemment.</span><span class="sxs-lookup"><span data-stu-id="74c3c-401">The **Connection** popup will appear (see image below), where you need to select the **Namespace** of the **Notification Hub**, which you set up previously.</span></span>

    4. <span data-ttu-id="74c3c-402">Sélectionnez votre **Hub de Notification** nom dans le menu déroulant du milieu.</span><span class="sxs-lookup"><span data-stu-id="74c3c-402">Select your **Notification Hub** name from the middle dropdown menu.</span></span>

    5.  <span data-ttu-id="74c3c-403">Définir le **stratégie** menu déroulant à **DefaultFullSharedAccessSignature**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-403">Set the **Policy** dropdown menu to **DefaultFullSharedAccessSignature**.</span></span>

    6. <span data-ttu-id="74c3c-404">Cliquez sur le **sélectionnez** bouton revenir en arrière.</span><span class="sxs-lookup"><span data-stu-id="74c3c-404">Click the **Select** button to go back.</span></span>

        ![mise à jour de la sortie](images/AzureLabs-Lab8-51.png)

31.  <span data-ttu-id="74c3c-406">Le **sorties** page doit maintenant correspondre à la ci-dessous, mais avec **votre** informations à la place.</span><span class="sxs-lookup"><span data-stu-id="74c3c-406">The **Outputs** page should now match the below, but with **your** information instead.</span></span> <span data-ttu-id="74c3c-407">Veillez à appuyer sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-407">Make sure to press **Save**.</span></span>

> [!WARNING]
> <span data-ttu-id="74c3c-408">*Ne pas modifier directement le nom du Hub de Notification* (cela doit-elle tous être effectuée à l’aide de la **éditeur avancé**, à condition que vous avez suivi les étapes précédentes correctement.</span><span class="sxs-lookup"><span data-stu-id="74c3c-408">*Do not edit the Notification Hub name directly* (this should all be done using the **Advanced Editor**, provided you followed the previous steps correctly.</span></span>

![sorties terminée](images/AzureLabs-Lab8-50.png)

32. <span data-ttu-id="74c3c-410">À ce stade, vous devez tester la fonction, pour vous assurer qu’il fonctionne.</span><span class="sxs-lookup"><span data-stu-id="74c3c-410">At this point, you should test the function, to ensure it is working.</span></span> <span data-ttu-id="74c3c-411">Pour cela, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74c3c-411">To do this:</span></span> 

    1. <span data-ttu-id="74c3c-412">Accédez à la page de la fonction une fois de plus :</span><span class="sxs-lookup"><span data-stu-id="74c3c-412">Navigate to the function page once more:</span></span>

        ![sorties terminée](images/AzureLabs-Lab8-50-1.png)

    2. <span data-ttu-id="74c3c-414">Dans la page de la fonction, cliquez sur le **Test** onglet à l’extrémité droite de la page, pour ouvrir le *Test* panneau :</span><span class="sxs-lookup"><span data-stu-id="74c3c-414">Back on the function page, click the **Test** tab on the far right side of the page, to open the *Test* blade:</span></span>

        ![sorties terminée](images/AzureLabs-Lab8-50-2.png)

    3. <span data-ttu-id="74c3c-416">Dans le **corps de la demande** zone de texte du panneau, collez le code ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="74c3c-416">Within the **Request body** textbox of the blade, paste the below code:</span></span>

        ```
        {  
            "Type":null,
            "X":3,
            "Y":0,
            "Z":1,
            "PartitionKey":null,
            "RowKey":"Obj2",
            "Timestamp":"0001-01-01T00:00:00+00:00",
            "ETag":null
        }
        ```

    4. <span data-ttu-id="74c3c-417">Avec le code de test en place, cliquez sur le **exécuter** situé en bas à droite et le test sera exécuté.</span><span class="sxs-lookup"><span data-stu-id="74c3c-417">With the test code in place, click the **Run** button at the bottom right, and the test will be run.</span></span> <span data-ttu-id="74c3c-418">Les journaux de sortie du test seront affiche dans la zone de la console, sous votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="74c3c-418">The output logs of the test will appear in the console area, below your function code.</span></span>

        ![sorties terminée](images/AzureLabs-Lab8-50-3.png)

    > [!WARNING]
    > <span data-ttu-id="74c3c-420">Si le test ci-dessus échoue, vous devez vérifier que vous avez suivi les étapes ci-dessus en exactement, en particulier les paramètres dans le **intégrer panneau**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-420">If the above test fails, you will need to double check that you have followed the above steps exactly, particularly the settings within the **integrate panel**.</span></span> 

## <a name="chapter-7---set-up-desktop-unity-project"></a><span data-ttu-id="74c3c-421">Chapitre 7 - configuration de projet Unity de bureau</span><span class="sxs-lookup"><span data-stu-id="74c3c-421">Chapter 7 - Set up Desktop Unity Project</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74c3c-422">L’application de bureau que vous créez, **ne sera pas** Professionnel dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="74c3c-422">The Desktop application which you are now creating, **will not** work in the Unity Editor.</span></span> <span data-ttu-id="74c3c-423">Il doit être exécuté en dehors de l’éditeur, suivant la création de l’application, à l’aide de Visual Studio (ou l’application déployée).</span><span class="sxs-lookup"><span data-stu-id="74c3c-423">It needs to be run outside of the Editor, following the Building of the application, using Visual Studio (or the deployed application).</span></span> 

<span data-ttu-id="74c3c-424">Ce qui suit est un standard configurée pour le développement avec Unity et de réalité mixte et par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="74c3c-424">The following is a typical set up for developing with Unity and mixed reality, and as such, is a good template for other projects.</span></span>

<span data-ttu-id="74c3c-425">Configurer et tester votre casque immersives de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="74c3c-425">Set up and test your mixed reality immersive headset.</span></span>

> [!NOTE] 
> <span data-ttu-id="74c3c-426">Vous allez **pas** nécessitent des contrôleurs de mouvement pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="74c3c-426">You will **not** require Motion Controllers for this course.</span></span> <span data-ttu-id="74c3c-427">Si vous avez besoin de prendre en charge de paramétrage le casque immersif, veuillez suivre ce [lien sur la façon de configurer Windows Mixed Reality](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span><span class="sxs-lookup"><span data-stu-id="74c3c-427">If you need support setting up the immersive headset, please follow this [link on how to set up Windows Mixed Reality](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span></span>

1.  <span data-ttu-id="74c3c-428">Ouvrez **Unity** et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-428">Open **Unity** and click **New**.</span></span>

    ![nouveau projet unity](images/AzureLabs-Lab8-52.png)

2.  <span data-ttu-id="74c3c-430">Vous devez fournir un nom de projet Unity, insérez **UnityDesktopNotifHub**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-430">You need to provide a Unity Project name, insert **UnityDesktopNotifHub**.</span></span> <span data-ttu-id="74c3c-431">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-431">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="74c3c-432">Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="74c3c-432">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="74c3c-433">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-433">Then, click **Create project**.</span></span>

    ![créer le projet](images/AzureLabs-Lab8-53.png)

3.  <span data-ttu-id="74c3c-435">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-435">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="74c3c-436">Accédez à **modifier** > **préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-436">Go to **Edit** > **Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="74c3c-437">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-437">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="74c3c-438">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="74c3c-438">Close the **Preferences** window.</span></span>

    ![ensemble des outils externes Visual Studio](images/AzureLabs-Lab8-54.png)

4.  <span data-ttu-id="74c3c-440">Ensuite, accédez à **fichier** > **paramètres de Build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le **plateforme de commutation**bouton pour appliquer votre sélection.</span><span class="sxs-lookup"><span data-stu-id="74c3c-440">Next, go to **File** > **Build Settings** and select **Universal Windows Platform**, then click on the **Switch Platform** button to apply your selection.</span></span>

    ![changer de plate-forme](images/AzureLabs-Lab8-55.png)

5.  <span data-ttu-id="74c3c-442">Lorsque vous êtes toujours dans **fichier** > **paramètres de Build**, assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="74c3c-442">While still in **File** > **Build Settings**, make sure that:</span></span>

    1.  <span data-ttu-id="74c3c-443">**Équipement cible** a la valeur **n’importe quel appareil**</span><span class="sxs-lookup"><span data-stu-id="74c3c-443">**Target Device** is set to **Any Device**</span></span>

        > <span data-ttu-id="74c3c-444">Cette Application sera pour votre bureau, doivent donc être **n’importe quel appareil**</span><span class="sxs-lookup"><span data-stu-id="74c3c-444">This Application will be for your desktop, so must be **Any Device**</span></span>

    2.  <span data-ttu-id="74c3c-445">**Type de build** a la valeur **D3D**</span><span class="sxs-lookup"><span data-stu-id="74c3c-445">**Build Type** is set to **D3D**</span></span>

    3.  <span data-ttu-id="74c3c-446">**Kit de développement logiciel** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="74c3c-446">**SDK** is set to **Latest installed**</span></span>

    4.  <span data-ttu-id="74c3c-447">**Version de Visual Studio** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="74c3c-447">**Visual Studio Version** is set to **Latest installed**</span></span>

    5.  <span data-ttu-id="74c3c-448">**Générez et exécutez** est défini sur **ordinateur Local**</span><span class="sxs-lookup"><span data-stu-id="74c3c-448">**Build and Run** is set to **Local Machine**</span></span>

    6.  <span data-ttu-id="74c3c-449">Cet emplacement, il est important de l’enregistrement de la scène et en l’ajoutant à la build.</span><span class="sxs-lookup"><span data-stu-id="74c3c-449">While here, it is worth saving the scene, and adding it to the build.</span></span>

        1. <span data-ttu-id="74c3c-450">Cela en sélectionnant **ajouter un arrière-plan Open**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-450">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="74c3c-451">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="74c3c-451">A save window will appear.</span></span>

            ![ajouter des scènes ouverts](images/AzureLabs-Lab8-56.png)

        2. <span data-ttu-id="74c3c-453">Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-453">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![nouveau dossier de scènes](images/AzureLabs-Lab8-57.png)

        3. <span data-ttu-id="74c3c-455">Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le **nom de fichier :** champ de texte, tapez **NH\_Desktop\_scène**, puis appuyez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-455">Open your newly created **Scenes** folder, and then in the **File name:** text field, type **NH\_Desktop\_Scene**, then press **Save**.</span></span>

            ![nouvelle NH_Desktop_Scene](images/AzureLabs-Lab8-58.png)

    7.  <span data-ttu-id="74c3c-457">Les autres paramètres, dans **paramètres de Build**, doit être conservé comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="74c3c-457">The remaining settings, in **Build Settings**, should be left as default for now.</span></span>

6.  <span data-ttu-id="74c3c-458">Dans la même fenêtre, cliquez sur le **paramètres du lecteur** bouton, le panneau de configuration associée s’ouvre dans l’espace où le **inspecteur** se trouve.</span><span class="sxs-lookup"><span data-stu-id="74c3c-458">In the same window click on the **Player Settings** button, this will open the related panel in the space where the **Inspector** is located.</span></span>

7.  <span data-ttu-id="74c3c-459">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="74c3c-459">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="74c3c-460">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="74c3c-460">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="74c3c-461">**Version du Runtime de script** doit être **expérimental (équivalent .NET 4.6)**</span><span class="sxs-lookup"><span data-stu-id="74c3c-461">**Scripting Runtime Version** should be **Experimental (.NET 4.6 Equivalent)**</span></span>

        2. <span data-ttu-id="74c3c-462">**Script principal** doit être **.NET**</span><span class="sxs-lookup"><span data-stu-id="74c3c-462">**Scripting Backend** should be **.NET**</span></span>

        3. <span data-ttu-id="74c3c-463">**Niveau de compatibilité d’API** doit être **.NET 4.6**</span><span class="sxs-lookup"><span data-stu-id="74c3c-463">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![version de net 4.6](images/AzureLabs-Lab8-59.png)

    2.  <span data-ttu-id="74c3c-465">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="74c3c-465">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="74c3c-466">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="74c3c-466">**InternetClient**</span></span>

            ![client internet de graduation](images/AzureLabs-Lab8-60.png)

8.  <span data-ttu-id="74c3c-468">Dans **paramètres de Build** *Unity C\# projets* est n’est plus grisée ; Cochez la case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="74c3c-468">Back in **Build Settings** *Unity C\# Projects* is no longer greyed out; tick the checkbox next to this.</span></span>

9.  <span data-ttu-id="74c3c-469">Fermer le **paramètres de Build** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="74c3c-469">Close the **Build Settings** window.</span></span>

10. <span data-ttu-id="74c3c-470">Enregistrer votre projet et scène **fichier** > **enregistrer la scène / fichier** > **enregistrer le projet**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-470">Save your Scene and Project **File** > **Save Scene / File** > **Save Project**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="74c3c-471">Si vous souhaitez ignorer la *Unity configurer* composant pour ce projet (application de bureau) et toujours directement dans le code, n’hésitez pas à [télécharger cette .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20308%20-%20Cross-device%20notifications/Azure-MR-308-Desktop.unitypackage), importez-le dans votre projet en tant qu’un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).</span><span class="sxs-lookup"><span data-stu-id="74c3c-471">If you wish to skip the *Unity Set up* component for this project (Desktop App), and continue straight into code, feel free to [download this .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20308%20-%20Cross-device%20notifications/Azure-MR-308-Desktop.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).</span></span>  <span data-ttu-id="74c3c-472">Vous devrez toujours ajouter les composants de script.</span><span class="sxs-lookup"><span data-stu-id="74c3c-472">You will still need to add the script components.</span></span>

## <a name="chapter-8---importing-the-dlls-in-unity"></a><span data-ttu-id="74c3c-473">Chapitre 8 - importation des DLL dans Unity</span><span class="sxs-lookup"><span data-stu-id="74c3c-473">Chapter 8 - Importing the DLLs in Unity</span></span>

<span data-ttu-id="74c3c-474">Vous allez utiliser Azure Storage pour Unity (qui, elle s’appuie sur le kit SDK Azure .net).</span><span class="sxs-lookup"><span data-stu-id="74c3c-474">You will be using Azure Storage for Unity (which itself leverages the .Net SDK for Azure).</span></span> <span data-ttu-id="74c3c-475">Pour plus d’informations suivre ce [lien sur Azure Storage pour Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).</span><span class="sxs-lookup"><span data-stu-id="74c3c-475">For more information follow this [link about Azure Storage for Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).</span></span>

<span data-ttu-id="74c3c-476">Il est actuellement un problème connu dans Unity qui nécessite des plug-ins à être reconfiguré après l’importation.</span><span class="sxs-lookup"><span data-stu-id="74c3c-476">There is currently a known issue in Unity which requires plugins to be reconfigured after import.</span></span> <span data-ttu-id="74c3c-477">Ces étapes (4-7 de cette section) ne sera plus nécessaires une fois que le bogue a été résolu.</span><span class="sxs-lookup"><span data-stu-id="74c3c-477">These steps (4 - 7 in this section) will no longer be required after the bug has been resolved.</span></span>

<span data-ttu-id="74c3c-478">Pour importer le SDK dans votre propre projet, assurez-vous que vous avez téléchargé la dernière version [ **.unitypackage** ](https://aka.ms/azstorage-unitysdk) à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="74c3c-478">To import the SDK into your own project, make sure you have downloaded the latest [**.unitypackage**](https://aka.ms/azstorage-unitysdk) from GitHub.</span></span> <span data-ttu-id="74c3c-479">Ensuite, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74c3c-479">Then, do the following:</span></span>

1.  <span data-ttu-id="74c3c-480">Ajouter le **.unitypackage** à Unity à l’aide de la **actifs \> importer un Package \> Package personnalisé** option de menu.</span><span class="sxs-lookup"><span data-stu-id="74c3c-480">Add the **.unitypackage** to Unity by using the **Assets \> Import Package \> Custom Package** menu option.</span></span>

2.  <span data-ttu-id="74c3c-481">Dans le **importer un Package Unity** zone s’affiche, vous pouvez sélectionner tous les éléments sous \*\**plug-in* \> \*stockage\*\*\*.</span><span class="sxs-lookup"><span data-stu-id="74c3c-481">In the **Import Unity Package** box that pops up, you can select everything under \*\**Plugin* \> \*Storage\*\*\*.</span></span>  <span data-ttu-id="74c3c-482">Désactivez tout le reste, qu’il n’est pas nécessaire pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="74c3c-482">Uncheck everything else, as it is not needed for this course.</span></span>

    ![importer dans le package](images/AzureLabs-Lab8-61.png)

3.  <span data-ttu-id="74c3c-484">Cliquez sur le ***importation*** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="74c3c-484">Click the ***Import*** button to add the items to your project.</span></span>

4.  <span data-ttu-id="74c3c-485">Accédez à la **stockage** dossier sous **plug-ins** dans le projet afficher, puis sélectionnez les plug-ins suivants *uniquement*:</span><span class="sxs-lookup"><span data-stu-id="74c3c-485">Go to the **Storage** folder under **Plugins** in the Project view and select the following plugins *only*:</span></span>

    -   <span data-ttu-id="74c3c-486">Microsoft.Data.Edm</span><span class="sxs-lookup"><span data-stu-id="74c3c-486">Microsoft.Data.Edm</span></span>
    -   <span data-ttu-id="74c3c-487">Microsoft.Data.OData</span><span class="sxs-lookup"><span data-stu-id="74c3c-487">Microsoft.Data.OData</span></span>
    -   <span data-ttu-id="74c3c-488">Microsoft.WindowsAzure.Storage</span><span class="sxs-lookup"><span data-stu-id="74c3c-488">Microsoft.WindowsAzure.Storage</span></span>
    -   <span data-ttu-id="74c3c-489">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="74c3c-489">Newtonsoft.Json</span></span>
    -   <span data-ttu-id="74c3c-490">System.Spatial</span><span class="sxs-lookup"><span data-stu-id="74c3c-490">System.Spatial</span></span>

![Décochez la case n’importe quelle plateforme](images/AzureLabs-Lab8-62.png)

5.  <span data-ttu-id="74c3c-492">Avec *ces plug-ins spécifiques* sélectionné, **Décochez** **plateforme Any** et **Décochez** **WSAPlayer** puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-492">With *these specific plugins* selected, **uncheck** **Any Platform** and **uncheck** **WSAPlayer** then click **Apply**.</span></span>

    ![appliquer des DLL de plateforme](images/AzureLabs-Lab8-63.png)

    > [!NOTE] 
    > <span data-ttu-id="74c3c-494">Nous allons marquer ces plug-ins particuliers à utiliser uniquement dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="74c3c-494">We are marking these particular plugins to only be used in the Unity Editor.</span></span> <span data-ttu-id="74c3c-495">Il s’agit, car il existe différentes versions des mêmes plug-ins dans le dossier WSA qui sera utilisé après que le projet est exporté à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="74c3c-495">This is because there are different versions of the same plugins in the WSA folder that will be used after the project is exported from Unity.</span></span>

6.  <span data-ttu-id="74c3c-496">Dans le **stockage** dossier de plug-in, sélectionnez uniquement :</span><span class="sxs-lookup"><span data-stu-id="74c3c-496">In the **Storage** plugin folder, select only:</span></span>

    -   <span data-ttu-id="74c3c-497">Microsoft.Data.Services.Client</span><span class="sxs-lookup"><span data-stu-id="74c3c-497">Microsoft.Data.Services.Client</span></span>

        ![jeu de ne pas traiter les DLL](images/AzureLabs-Lab8-64.png)

7.  <span data-ttu-id="74c3c-499">Vérifier le **processus ne** sous **paramètres de plateforme** et cliquez sur ***appliquer***.</span><span class="sxs-lookup"><span data-stu-id="74c3c-499">Check the **Don't Process** box under **Platform Settings** and click ***Apply***.</span></span>

    ![n’appliquer aucun traitement](images/AzureLabs-Lab8-65.png)

    > [!NOTE] 
    > <span data-ttu-id="74c3c-501">Nous sommes marquage ce plug-in « Ne pas traiter les », car l’utilitaire de correction Unity assembly a des difficultés à traiter ce plug-in.</span><span class="sxs-lookup"><span data-stu-id="74c3c-501">We are marking this plugin "Don't process", because the Unity assembly patcher has difficulty processing this plugin.</span></span> <span data-ttu-id="74c3c-502">Le plug-in continue de fonctionner même si elle n’est pas traitée.</span><span class="sxs-lookup"><span data-stu-id="74c3c-502">The plugin will still work even though it is not processed.</span></span>

## <a name="chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project"></a><span data-ttu-id="74c3c-503">Chapitre 9 - créer la classe TableToScene dans le projet Unity de bureau</span><span class="sxs-lookup"><span data-stu-id="74c3c-503">Chapter 9 - Create the TableToScene class in the Desktop Unity project</span></span>

<span data-ttu-id="74c3c-504">Vous devez maintenant créer les scripts qui contient le code pour exécuter cette application.</span><span class="sxs-lookup"><span data-stu-id="74c3c-504">You now need to create the scripts containing the code to run this application.</span></span>

<span data-ttu-id="74c3c-505">Le premier script que vous créez est **TableToScene**, qui est chargé de :</span><span class="sxs-lookup"><span data-stu-id="74c3c-505">The first script you need to create is **TableToScene**, which is responsible for:</span></span>

-   <span data-ttu-id="74c3c-506">Lecture d’entités dans le stockage Table Azure.</span><span class="sxs-lookup"><span data-stu-id="74c3c-506">Reading entities within the Azure Table.</span></span>
-   <span data-ttu-id="74c3c-507">À l’aide de données de la Table, de déterminer les objets à générer et à quelle position.</span><span class="sxs-lookup"><span data-stu-id="74c3c-507">Using the Table data, determine which objects to spawn, and in which position.</span></span>

<span data-ttu-id="74c3c-508">Le deuxième script que vous créez est **CloudScene**, qui est chargé de :</span><span class="sxs-lookup"><span data-stu-id="74c3c-508">The second script you need to create is **CloudScene**, which is responsible for:</span></span>

-   <span data-ttu-id="74c3c-509">Enregistrement de l’événement de clic gauche, pour autoriser l’utilisateur à faire glisser des objets autour de la scène.</span><span class="sxs-lookup"><span data-stu-id="74c3c-509">Registering the left-click event, to allow the user to drag objects around the scene.</span></span>
-   <span data-ttu-id="74c3c-510">Sérialiser les données d’objet à partir de cette scène Unity et de les envoyer à l’application de fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="74c3c-510">Serializing the object data from this Unity scene, and sending it to the Azure Function App.</span></span>

<span data-ttu-id="74c3c-511">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="74c3c-511">To create this class:</span></span>

1.  <span data-ttu-id="74c3c-512">Avec le bouton droit dans le **Asset** dossier se trouve dans le volet de projet, **créer** > **dossier**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-512">Right-click in the **Asset** Folder located in the Project Panel, **Create** > **Folder**.</span></span> <span data-ttu-id="74c3c-513">Nommez le dossier **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-513">Name the folder **Scripts**.</span></span>

    ![créer le dossier de scripts](images/AzureLabs-Lab8-66.png)

    ![créer le dossier scripts 2](images/AzureLabs-Lab8-67.png)

2.  <span data-ttu-id="74c3c-516">Double-cliquez sur le dossier venez de créer, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="74c3c-516">Double click on the folder just created, to open it.</span></span>

3.  <span data-ttu-id="74c3c-517">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-517">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="74c3c-518">Nommez le script **TableToScene**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-518">Name the script **TableToScene**.</span></span>

    <span data-ttu-id="74c3c-519">![script c#](images/AzureLabs-Lab8-68.png)
    ![TableToScene le changement de nom](images/AzureLabs-Lab8-69.png)</span><span class="sxs-lookup"><span data-stu-id="74c3c-519">![new c# script](images/AzureLabs-Lab8-68.png)
![TableToScene rename](images/AzureLabs-Lab8-69.png)</span></span>

4.  <span data-ttu-id="74c3c-520">Double-cliquez sur le script pour l’ouvrir dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="74c3c-520">Double-click on the script to open it in Visual Studio 2017.</span></span>

5.  <span data-ttu-id="74c3c-521">Ajoutez les espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="74c3c-521">Add the following namespaces:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    using UnityEngine;
    ```

6.  <span data-ttu-id="74c3c-522">Dans la classe, insérez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="74c3c-522">Within the class, insert the following variables:</span></span>

    ```csharp
        /// <summary>    
        /// allows this class to behave like a singleton
        /// </summary>    
        public static TableToScene instance;

        /// <summary>    
        /// Insert here you Azure Storage name     
        /// </summary>    
        private string accountName = " -- Insert your Azure Storage name -- ";

        /// <summary>    
        /// Insert here you Azure Storage key    
        /// </summary>    
        private string accountKey = " -- Insert your Azure Storage key -- ";
    ```
    
    > [!NOTE] 
    > <span data-ttu-id="74c3c-523">Remplacez le **accountName** valeur avec le nom de votre Service de stockage Azure et **accountKey** valeur avec la valeur de clé trouvée dans le Service de stockage Azure, dans le portail Azure (voir Image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="74c3c-523">Substitute the **accountName** value with your Azure Storage Service name and **accountKey** value with the key value found in the Azure Storage Service, in the Azure Portal (See Image below).</span></span> 
    >
    > ![clé de compte d’extraction](images/AzureLabs-Lab8-70.png)

7.  <span data-ttu-id="74c3c-525">Ajoutez maintenant le **Start()** et **Awake()** méthodes pour initialiser la classe.</span><span class="sxs-lookup"><span data-stu-id="74c3c-525">Now add the **Start()** and **Awake()** methods to initialize the class.</span></span>

    ```csharp
        /// <summary>
        /// Triggers before initialization
        /// </summary>
        void Awake()
        {
            // static instance of this class
            instance = this;
        }

        /// <summary>
        /// Use this for initialization
        /// </summary>
        void Start()
        {  
            // Call method to populate the scene with new objects as 
            // pecified in the Azure Table
            PopulateSceneFromTableAsync();
        }
    ```

8.  <span data-ttu-id="74c3c-526">Dans le **TableToScene** de classe, ajoutez la méthode qui Récupère les valeurs à partir de la Table Azure et les utiliser pour générer dynamiquement les primitives appropriés dans la scène.</span><span class="sxs-lookup"><span data-stu-id="74c3c-526">Within the **TableToScene** class, add the method that will retrieve the values from the Azure Table and use them to spawn the appropriate primitives in the scene.</span></span>

    ```csharp
        /// <summary>    
        /// Populate the scene with new objects as specified in the Azure Table    
        /// </summary>    
        private async void PopulateSceneFromTableAsync()
        {
            // Obtain credentials for the Azure Storage
            StorageCredentials creds = new StorageCredentials(accountName, accountKey);

            // Storage account
            CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
            
            // Storage client
            CloudTableClient client = account.CreateCloudTableClient(); 
            
            // Table reference
            CloudTable table = client.GetTableReference("SceneObjectsTable");

            TableContinuationToken token = null;

            // Query the table for every existing Entity
            do
            {
                // Queries the whole table by breaking it into segments
                // (would happen only if the table had huge number of Entities)
                TableQuerySegment<AzureTableEntity> queryResult = await table.ExecuteQuerySegmentedAsync(new TableQuery<AzureTableEntity>(), token); 

                foreach (AzureTableEntity entity in queryResult.Results)
                {
                    GameObject newSceneGameObject = null;
                    Color newColor;

                    // check for the Entity Type and spawn in the scene the appropriate Primitive
                    switch (entity.Type)
                    {
                        case "Cube":
                            // Create a Cube in the scene
                            newSceneGameObject = GameObject.CreatePrimitive(PrimitiveType.Cube);
                            newColor = Color.blue;
                            break;

                        case "Sphere":
                            // Create a Sphere in the scene
                            newSceneGameObject = GameObject.CreatePrimitive(PrimitiveType.Sphere);
                            newColor = Color.red;
                            break;

                        case "Cylinder":
                            // Create a Cylinder in the scene
                            newSceneGameObject = GameObject.CreatePrimitive(PrimitiveType.Cylinder);
                            newColor = Color.yellow;
                            break;
                        default:
                            newColor = Color.white;
                            break;
                    }

                    newSceneGameObject.name = entity.RowKey;

                    newSceneGameObject.GetComponent<MeshRenderer>().material = new Material(Shader.Find("Diffuse"))
                    {
                        color = newColor
                    };

                    //check for the Entity X,Y,Z and move the Primitive at those coordinates
                    newSceneGameObject.transform.position = new Vector3((float)entity.X, (float)entity.Y, (float)entity.Z);
                }

                // if the token is null, it means there are no more segments left to query
                token = queryResult.ContinuationToken;
            }

            while (token != null);
        }
    ```

9.  <span data-ttu-id="74c3c-527">En dehors du **TableToScene** (classe), vous devez définir la classe utilisée par l’application pour sérialiser et désérialiser les **entités de Table**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-527">Outside the **TableToScene** class, you need to define the class used by the application to serialize and deserialize the **Table Entities**.</span></span>

    ```csharp
        /// <summary>
        /// This objects is used to serialize and deserialize the Azure Table Entity
        /// </summary>
        [System.Serializable]
        public class AzureTableEntity : TableEntity
        {
            public AzureTableEntity(string partitionKey, string rowKey)
                : base(partitionKey, rowKey) { }

            public AzureTableEntity() { }
            public string Type { get; set; }
            public double X { get; set; }
            public double Y { get; set; }
            public double Z { get; set; }
        }
    ```

10. <span data-ttu-id="74c3c-528">Assurez-vous que vous **enregistrer** avant de revenir à l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="74c3c-528">Make sure you **Save** before going back to the Unity Editor.</span></span>

11. <span data-ttu-id="74c3c-529">Cliquez sur le **Main Camera** à partir de la **hiérarchie** panneau, afin que ses propriétés s’affichent dans le **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-529">Click the **Main Camera** from the **Hierarchy** panel, so that its properties appear in the **Inspector**.</span></span>

12. <span data-ttu-id="74c3c-530">Avec le **Scripts** dossier ouvert, sélectionnez le script **TableToScene fichier** et faites-le glisser sur le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-530">With the **Scripts** folder open, select the script **TableToScene file** and drag it onto the **Main Camera**.</span></span> <span data-ttu-id="74c3c-531">Le résultat doit être comme suit :</span><span class="sxs-lookup"><span data-stu-id="74c3c-531">The result should be as below:</span></span>

    ![Ajouter un script à la caméra principale](images/AzureLabs-Lab8-71.png)

## <a name="chapter-10---create-the-cloudscene-class-in-the-desktop-unity-project"></a><span data-ttu-id="74c3c-533">Chapitre 10 - créer la classe CloudScene dans le projet Unity de bureau</span><span class="sxs-lookup"><span data-stu-id="74c3c-533">Chapter 10 - Create the CloudScene class in the Desktop Unity Project</span></span>

<span data-ttu-id="74c3c-534">Le deuxième script que vous créez est **CloudScene**, qui est chargé de :</span><span class="sxs-lookup"><span data-stu-id="74c3c-534">The second script you need to create is **CloudScene**, which is responsible for:</span></span>

-   <span data-ttu-id="74c3c-535">Enregistrement de l’événement de clic gauche, pour autoriser l’utilisateur à faire glisser des objets autour de la scène.</span><span class="sxs-lookup"><span data-stu-id="74c3c-535">Registering the left-click event, to allow the user to drag objects around the scene.</span></span>

-   <span data-ttu-id="74c3c-536">Sérialiser les données d’objet à partir de cette scène Unity et de les envoyer à l’application de fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="74c3c-536">Serializing the object data from this Unity scene, and sending it to the Azure Function App.</span></span>

<span data-ttu-id="74c3c-537">Pour créer le deuxième script :</span><span class="sxs-lookup"><span data-stu-id="74c3c-537">To create the second script:</span></span>

1.  <span data-ttu-id="74c3c-538">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**, **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-538">Right-click inside the **Scripts** folder, click **Create**, **C\# Script**.</span></span> <span data-ttu-id="74c3c-539">Nommez le script **CloudScene**</span><span class="sxs-lookup"><span data-stu-id="74c3c-539">Name the script **CloudScene**</span></span>
    
    <span data-ttu-id="74c3c-540">![script c#](images/AzureLabs-Lab8-72.png)
    ![renommer CloudScene](images/AzureLabs-Lab8-73.png)</span><span class="sxs-lookup"><span data-stu-id="74c3c-540">![new c# script](images/AzureLabs-Lab8-72.png)
![rename CloudScene](images/AzureLabs-Lab8-73.png)</span></span>

2.  <span data-ttu-id="74c3c-541">Ajoutez les espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="74c3c-541">Add the following namespaces:</span></span>

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.Text;
    using System.Threading.Tasks;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

3.  <span data-ttu-id="74c3c-542">Insérez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="74c3c-542">Insert the following variables:</span></span>

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static CloudScene instance;

        /// <summary>
        /// Insert here you Azure Function Url
        /// </summary>
        private string azureFunctionEndpoint = "--Insert here you Azure Function Endpoint--";

        /// <summary>
        /// Flag for object being moved
        /// </summary>
        private bool gameObjHasMoved;

        /// <summary>
        /// Transform of the object being dragged by the mouse
        /// </summary>
        private Transform gameObjHeld;

        /// <summary>
        /// Class hosted in the TableToScene script
        /// </summary>
        private AzureTableEntity azureTableEntity;
    ```

4.  <span data-ttu-id="74c3c-543">Remplacez le **azureFunctionEndpoint** valeur avec votre URL d’application de fonction Azure trouvée dans le Service d’application de fonction Azure, dans le portail Azure, comme illustré dans l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="74c3c-543">Substitute the **azureFunctionEndpoint** value with your Azure Function App URL found in the Azure Function App Service, in the Azure Portal, as shown in the image below:</span></span>

    ![obtenir l’URL de la fonction](images/AzureLabs-Lab8-74.png)

5.  <span data-ttu-id="74c3c-545">Ajoutez maintenant le **Start()** et **Awake()** méthodes pour initialiser la classe.</span><span class="sxs-lookup"><span data-stu-id="74c3c-545">Now add the **Start()** and **Awake()** methods to initialize the class.</span></span>

    ```csharp
        /// <summary>
        /// Triggers before initialization
        /// </summary>
        void Awake()
        {
            // static instance of this class
            instance = this;
        }

        /// <summary>
        /// Use this for initialization
        /// </summary>
        void Start()
        {
            // initialise an AzureTableEntity
            azureTableEntity = new AzureTableEntity();
        }
    ```

6.  <span data-ttu-id="74c3c-546">Dans le **Update()** (méthode), ajoutez le code suivant qui détecte l’entrée de la souris et faites glisser, qui à son tour déplacera GameObjects dans la scène.</span><span class="sxs-lookup"><span data-stu-id="74c3c-546">Within the **Update()** method, add the following code that will detect the mouse input and drag, which will in turn move GameObjects in the scene.</span></span> <span data-ttu-id="74c3c-547">Si l’utilisateur a glisser -déplacer un objet, il transmet le nom et les coordonnées de l’objet à la méthode **UpdateCloudScene()** , qui appelle le service d’application Azure Function App, qui met à jour la table Azure et le déclencheur le notification.</span><span class="sxs-lookup"><span data-stu-id="74c3c-547">If the user has dragged and dropped an object, it will pass the name and coordinates of the object to the method **UpdateCloudScene()**, which will call the Azure Function App service, which will update the Azure table and trigger the notification.</span></span>

    ```csharp
        /// <summary>
        /// Update is called once per frame
        /// </summary>
        void Update()
        {
            //Enable Drag if button is held down
            if (Input.GetMouseButton(0))
            {
                // Get the mouse position
                Vector3 mousePosition = new Vector3(Input.mousePosition.x, Input.mousePosition.y, 10);

                Vector3 objPos = Camera.main.ScreenToWorldPoint(mousePosition);

                Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);

                RaycastHit hit;

                // Raycast from the current mouse position to the object overlapped by the mouse
                if (Physics.Raycast(ray, out hit))
                {
                    // update the position of the object "hit" by the mouse
                    hit.transform.position = objPos;

                    gameObjHasMoved = true;

                    gameObjHeld = hit.transform;
                }
            }

            // check if the left button mouse is released while holding an object
            if (Input.GetMouseButtonUp(0) && gameObjHasMoved)
            {
                gameObjHasMoved = false;

                // Call the Azure Function that will update the appropriate Entity in the Azure Table
                // and send a Notification to all subscribed Apps
                Debug.Log("Calling Azure Function");

                StartCoroutine(UpdateCloudScene(gameObjHeld.name, gameObjHeld.position.x, gameObjHeld.position.y, gameObjHeld.position.z));
            }
        }
    ```

7.  <span data-ttu-id="74c3c-548">Ajoutez maintenant le **UpdateCloudScene()** méthode, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="74c3c-548">Now add the **UpdateCloudScene()** method, as below:</span></span>

    ```csharp
        private IEnumerator UpdateCloudScene(string objName, double xPos, double yPos, double zPos)
        {
            WWWForm form = new WWWForm();

            // set the properties of the AzureTableEntity
            azureTableEntity.RowKey = objName;

            azureTableEntity.X = xPos;

            azureTableEntity.Y = yPos;

            azureTableEntity.Z = zPos;

            // Serialize the AzureTableEntity object to be sent to Azure
            string jsonObject = JsonConvert.SerializeObject(azureTableEntity);

            using (UnityWebRequest www = UnityWebRequest.Post(azureFunctionEndpoint, jsonObject))
            {
                byte[] jsonToSend = new System.Text.UTF8Encoding().GetBytes(jsonObject);

                www.uploadHandler = new UploadHandlerRaw(jsonToSend);

                www.uploadHandler.contentType = "application/json";

                www.downloadHandler = new DownloadHandlerBuffer();

                www.SetRequestHeader("Content-Type", "application/json");

                yield return www.SendWebRequest();

                string response = www.responseCode.ToString();
            }
        }
    ```

8.  <span data-ttu-id="74c3c-549">Enregistrer le code et revenir à Unity</span><span class="sxs-lookup"><span data-stu-id="74c3c-549">Save the code and return to Unity</span></span>

9.  <span data-ttu-id="74c3c-550">Faites glisser le **CloudScene** de script sur le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-550">Drag the **CloudScene** script onto the **Main Camera**.</span></span> 

    1. <span data-ttu-id="74c3c-551">Cliquez sur le **Main Camera** à partir de la **hiérarchie** panneau, afin que ses propriétés s’affichent dans le **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-551">Click the **Main Camera** from the **Hierarchy** panel, so that its properties appear in the **Inspector**.</span></span> 

    2. <span data-ttu-id="74c3c-552">Avec le **Scripts** ouvert, sélectionnez de dossier le **CloudScene** de script et faites-le glisser sur le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-552">With the **Scripts** folder open, select the **CloudScene** script and drag it onto the **Main Camera**.</span></span> <span data-ttu-id="74c3c-553">Le résultat doit être comme suit :</span><span class="sxs-lookup"><span data-stu-id="74c3c-553">The result should be as below:</span></span>

        > ![faire glisser cloud script caméra principale](images/AzureLabs-Lab8-75.png)

## <a name="chapter-11---build-the-desktop-project-to-uwp"></a><span data-ttu-id="74c3c-555">Chapitre 11 - générer le projet de bureau vers UWP</span><span class="sxs-lookup"><span data-stu-id="74c3c-555">Chapter 11 - Build the Desktop Project to UWP</span></span>

<span data-ttu-id="74c3c-556">Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée.</span><span class="sxs-lookup"><span data-stu-id="74c3c-556">Everything needed for the Unity section of this project has now been completed.</span></span>

1.  <span data-ttu-id="74c3c-557">Accédez à **les paramètres de génération** (**fichier** > **paramètres de Build**).</span><span class="sxs-lookup"><span data-stu-id="74c3c-557">Navigate to **Build Settings** (**File** > **Build Settings**).</span></span>

2.  <span data-ttu-id="74c3c-558">À partir de la **paramètres de Build** fenêtre, cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-558">From the **Build Settings** window, click **Build**.</span></span>

    ![Générer le projet](images/AzureLabs-Lab8-76.png)

3.  <span data-ttu-id="74c3c-560">Un **Explorateur de fichiers** fenêtre va contextuelle, vous invite à entrer un emplacement de Build.</span><span class="sxs-lookup"><span data-stu-id="74c3c-560">A **File Explorer** window will popup, prompting you for a location to Build.</span></span> <span data-ttu-id="74c3c-561">Créez un dossier (en cliquant sur **nouveau dossier** dans l’angle supérieur gauche) et nommez-le **génère**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-561">Create a new folder (by clicking **New Folder** in the top-left corner), and name it **BUILDS**.</span></span>

    ![nouveau dossier de build](images/AzureLabs-Lab8-77.png)

    1.  <span data-ttu-id="74c3c-563">Ouvrez le nouveau **génère** dossier et créez un autre dossier (à l’aide de **nouveau dossier** une fois de plus) et nommez-le **NH\_Desktop\_application**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-563">Open the new **BUILDS** folder, and create another folder (using **New Folder** once more), and name it **NH\_Desktop\_App**.</span></span>

        ![nom du dossier NH_Desktop_App](images/AzureLabs-Lab8-78.png)

    2.  <span data-ttu-id="74c3c-565">Avec le **NH\_Desktop\_application** sélectionné.</span><span class="sxs-lookup"><span data-stu-id="74c3c-565">With the **NH\_Desktop\_App** selected.</span></span> <span data-ttu-id="74c3c-566">Cliquez sur **sélectionnez dossier**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-566">click **Select Folder**.</span></span> <span data-ttu-id="74c3c-567">Le projet prendra une minute ou donc en créer.</span><span class="sxs-lookup"><span data-stu-id="74c3c-567">The project will take a minute or so to build.</span></span>

4.  <span data-ttu-id="74c3c-568">Après la génération, **Explorateur de fichiers** s’affiche vous indiquant l’emplacement de votre nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="74c3c-568">Following build, **File Explorer** will appear showing you the location of your new project.</span></span> <span data-ttu-id="74c3c-569">Pas nécessaire pour l’ouvrir, bien que, comme vous avez besoin créer l’autre Unity projet tout d’abord, dans les prochains chapitres.</span><span class="sxs-lookup"><span data-stu-id="74c3c-569">No need to open it, though, as you need to create the other Unity project first, in the next few Chapters.</span></span>


## <a name="chapter-12---set-up-mixed-reality-unity-project"></a><span data-ttu-id="74c3c-570">Chapitre 12 - configurer des projets de Unity de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="74c3c-570">Chapter 12 - Set up Mixed Reality Unity Project</span></span>

<span data-ttu-id="74c3c-571">Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="74c3c-571">The following is a typical set up for developing with the mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="74c3c-572">Ouvrez **Unity** et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-572">Open **Unity** and click **New**.</span></span>

    ![nouveau projet unity](images/AzureLabs-Lab8-79.png)

2.  <span data-ttu-id="74c3c-574">Vous devez maintenant fournir un nom de projet Unity, insérer **UnityMRNotifHub**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-574">You will now need to provide a Unity Project name, insert **UnityMRNotifHub**.</span></span> <span data-ttu-id="74c3c-575">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-575">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="74c3c-576">Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="74c3c-576">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="74c3c-577">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-577">Then, click **Create project**.</span></span>

    ![name UnityMRNotifHub](images/AzureLabs-Lab8-80.png)

3.  <span data-ttu-id="74c3c-579">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-579">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="74c3c-580">Accédez à **modifier** > **préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-580">Go to **Edit** > **Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="74c3c-581">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-581">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="74c3c-582">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="74c3c-582">Close the **Preferences** window.</span></span>

    ![éditeur externe de jeu à Visual Studio](images/AzureLabs-Lab8-81.png)

4.  <span data-ttu-id="74c3c-584">Ensuite, accédez à **fichier** > **paramètres de Build** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **basculer la plateforme**  bouton.</span><span class="sxs-lookup"><span data-stu-id="74c3c-584">Next, go to **File** > **Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

    ![plateformes de commutateur vers UWP](images/AzureLabs-Lab8-82.png)

5.  <span data-ttu-id="74c3c-586">Accédez à **fichier** > **paramètres de Build** et vous assurer que :</span><span class="sxs-lookup"><span data-stu-id="74c3c-586">Go to **File** > **Build Settings** and make sure that:</span></span>

    1.  <span data-ttu-id="74c3c-587">**Équipement cible** a la valeur **n’importe quel appareil**</span><span class="sxs-lookup"><span data-stu-id="74c3c-587">**Target Device** is set to **Any Device**</span></span>

        > <span data-ttu-id="74c3c-588">Pour le Microsoft HoloLens, définissez **appareil cible** à *HoloLens*.</span><span class="sxs-lookup"><span data-stu-id="74c3c-588">For the Microsoft HoloLens, set **Target Device** to *HoloLens*.</span></span>

    2.  <span data-ttu-id="74c3c-589">**Type de build** a la valeur **D3D**</span><span class="sxs-lookup"><span data-stu-id="74c3c-589">**Build Type** is set to **D3D**</span></span>

    3.  <span data-ttu-id="74c3c-590">**Kit de développement logiciel** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="74c3c-590">**SDK** is set to **Latest installed**</span></span>

    4.  <span data-ttu-id="74c3c-591">**Version de Visual Studio** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="74c3c-591">**Visual Studio Version** is set to **Latest installed**</span></span>

    5.  <span data-ttu-id="74c3c-592">**Générez et exécutez** est défini sur **ordinateur Local**</span><span class="sxs-lookup"><span data-stu-id="74c3c-592">**Build and Run** is set to **Local Machine**</span></span>

    6.  <span data-ttu-id="74c3c-593">Cet emplacement, il est important de l’enregistrement de la scène et en l’ajoutant à la build.</span><span class="sxs-lookup"><span data-stu-id="74c3c-593">While here, it is worth saving the scene, and adding it to the build.</span></span>

        1. <span data-ttu-id="74c3c-594">Cela en sélectionnant **ajouter un arrière-plan Open**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-594">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="74c3c-595">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="74c3c-595">A save window will appear.</span></span>

            ![ajouter des scènes ouverts](images/AzureLabs-Lab8-83.png)

        2. <span data-ttu-id="74c3c-597">Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-597">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![nouveau dossier de scènes](images/AzureLabs-Lab8-84.png)

        3. <span data-ttu-id="74c3c-599">Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le **nom de fichier :** champ de texte, tapez **NH\_MR\_scène**, puis appuyez sur  **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-599">Open your newly created **Scenes** folder, and then in the **File name:** text field, type **NH\_MR\_Scene**, then press **Save**.</span></span>

            ![nouvelle scène - NH_MR_Scene](images/AzureLabs-Lab8-85.png)

    7.  <span data-ttu-id="74c3c-601">Les autres paramètres, dans **paramètres de Build**, doit être conservé comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="74c3c-601">The remaining settings, in **Build Settings**, should be left as default for now.</span></span>

6.  <span data-ttu-id="74c3c-602">Dans la même fenêtre, cliquez sur le **paramètres du lecteur** bouton, le panneau de configuration associée s’ouvre dans l’espace où le **inspecteur** se trouve.</span><span class="sxs-lookup"><span data-stu-id="74c3c-602">In the same window click on the **Player Settings** button, this will open the related panel in the space where the **Inspector** is located.</span></span>    

    ![Ouvrez les paramètres du lecteur](images/AzureLabs-Lab8-86.png)

7.  <span data-ttu-id="74c3c-604">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="74c3c-604">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="74c3c-605">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="74c3c-605">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="74c3c-606">**Version du Runtime de script** doit être **expérimental** (équivalent .NET 4.6)</span><span class="sxs-lookup"><span data-stu-id="74c3c-606">**Scripting Runtime Version** should be **Experimental** (.NET 4.6 Equivalent)</span></span>
        2.  <span data-ttu-id="74c3c-607">**Script principal** doit être ***.NET***</span><span class="sxs-lookup"><span data-stu-id="74c3c-607">**Scripting Backend** should be ***.NET***</span></span>
        3.  <span data-ttu-id="74c3c-608">**Niveau de compatibilité d’API** doit être **.NET 4.6**</span><span class="sxs-lookup"><span data-stu-id="74c3c-608">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![compatibilité d’API](images/AzureLabs-Lab8-87.png)

    2.  <span data-ttu-id="74c3c-610">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté</span><span class="sxs-lookup"><span data-stu-id="74c3c-610">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added</span></span>

        ![mettre à jour les paramètres xr](images/AzureLabs-Lab8-88.png)        

    3.  <span data-ttu-id="74c3c-612">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, diable :</span><span class="sxs-lookup"><span data-stu-id="74c3c-612">Within the **Publishing Settings** tab, under **Capabilities**, heck:</span></span>

        - <span data-ttu-id="74c3c-613">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="74c3c-613">**InternetClient**</span></span>           

            ![client internet de graduation](images/AzureLabs-Lab8-89.png)

8.  <span data-ttu-id="74c3c-615">Dans **paramètres de Build**, **Unity C# projets** est n’est plus grisée : cochez la case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="74c3c-615">Back in **Build Settings**, **Unity C# Projects** is no longer greyed out: tick the checkbox next to this.</span></span>

9.  <span data-ttu-id="74c3c-616">Avec ces modifications effectuées, fermez la fenêtre de paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="74c3c-616">With these changes done, close the Build Settings window.</span></span>

10. <span data-ttu-id="74c3c-617">Enregistrer votre projet et scène **fichier** > **enregistrer la scène / fichier** > **enregistrer le projet**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-617">Save your Scene and Project **File** > **Save Scene / File** > **Save Project**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="74c3c-618">Si vous souhaitez ignorer la *Unity configurer* composant pour ce projet (mixte réalité application) et toujours directement dans le code, n’hésitez pas à [télécharger cette .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20308%20-%20Cross-device%20notifications/Azure-MR-308-MR.unitypackage), importez-le dans votre projet sous la forme d’un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 14](#chapter-14---creating-the-tabletoscene-class-in-the-mixed-reality-unity-project).</span><span class="sxs-lookup"><span data-stu-id="74c3c-618">If you wish to skip the *Unity Set up* component for this project (mixed reality App), and continue straight into code, feel free to [download this .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20308%20-%20Cross-device%20notifications/Azure-MR-308-MR.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 14](#chapter-14---creating-the-tabletoscene-class-in-the-mixed-reality-unity-project).</span></span> <span data-ttu-id="74c3c-619">Vous devrez toujours ajouter les composants de script.</span><span class="sxs-lookup"><span data-stu-id="74c3c-619">You will still need to add the script components.</span></span>

### <a name="chapter-13---importing-the-dlls-in-the-mixed-reality-unity-project"></a><span data-ttu-id="74c3c-620">Chapitre 13 - importation des DLL dans le projet Unity de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="74c3c-620">Chapter 13 - Importing the DLLs in the Mixed Reality Unity Project</span></span>

<span data-ttu-id="74c3c-621">Vous utiliserez le stockage Azure pour bibliothèque Unity (qui utilise le kit SDK .net pour Azure).</span><span class="sxs-lookup"><span data-stu-id="74c3c-621">You will be using Azure Storage for Unity library (which uses the .Net SDK for Azure).</span></span> <span data-ttu-id="74c3c-622">Veuillez suivre ce [lien sur l’utilisation du stockage Azure avec Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).</span><span class="sxs-lookup"><span data-stu-id="74c3c-622">Please follow this [link on how to use Azure Storage with Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).</span></span>
<span data-ttu-id="74c3c-623">Il est actuellement un problème connu dans Unity qui nécessite des plug-ins à être reconfiguré après l’importation.</span><span class="sxs-lookup"><span data-stu-id="74c3c-623">There is currently a known issue in Unity which requires plugins to be reconfigured after import.</span></span> <span data-ttu-id="74c3c-624">Ces étapes (4-7 de cette section) ne sera plus nécessaires une fois que le bogue a été résolu.</span><span class="sxs-lookup"><span data-stu-id="74c3c-624">These steps (4 - 7 in this section) will no longer be required after the bug has been resolved.</span></span>

<span data-ttu-id="74c3c-625">Pour importer le SDK dans votre propre projet, assurez-vous que vous avez téléchargé la dernière version [.unitypackage](https://aka.ms/azstorage-unitysdk).</span><span class="sxs-lookup"><span data-stu-id="74c3c-625">To import the SDK into your own project, make sure you have downloaded the latest [.unitypackage](https://aka.ms/azstorage-unitysdk).</span></span> <span data-ttu-id="74c3c-626">Ensuite, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="74c3c-626">Then, do the following:</span></span>

1.  <span data-ttu-id="74c3c-627">Ajouter le .unitypackage que vous avez téléchargé à partir de l’exemple ci-dessus, à Unity à l’aide de la **actifs** > **importer un Package** > **Package personnalisé** option de menu .</span><span class="sxs-lookup"><span data-stu-id="74c3c-627">Add the .unitypackage you downloaded from the above, to Unity by using the **Assets** > **Import Package** > **Custom Package** menu option.</span></span>

2.  <span data-ttu-id="74c3c-628">Dans le **importer un Package Unity** zone s’affiche, vous pouvez sélectionner tous les éléments sous **plug-in** > **stockage**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-628">In the **Import Unity Package** box that pops up, you can select everything under **Plugin** > **Storage**.</span></span>

    ![importer un package](images/AzureLabs-Lab8-90.png)

3.  <span data-ttu-id="74c3c-630">Cliquez sur le **importation** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="74c3c-630">Click the **Import** button to add the items to your project.</span></span>

4.  <span data-ttu-id="74c3c-631">Accédez à la **stockage** dossier sous **plug-ins** dans le projet afficher, puis sélectionnez les plug-ins suivants *uniquement*:</span><span class="sxs-lookup"><span data-stu-id="74c3c-631">Go to the **Storage** folder under **Plugins** in the Project view and select the following plugins *only*:</span></span>

    -   <span data-ttu-id="74c3c-632">Microsoft.Data.Edm</span><span class="sxs-lookup"><span data-stu-id="74c3c-632">Microsoft.Data.Edm</span></span>
    -   <span data-ttu-id="74c3c-633">Microsoft.Data.OData</span><span class="sxs-lookup"><span data-stu-id="74c3c-633">Microsoft.Data.OData</span></span>
    -   <span data-ttu-id="74c3c-634">Microsoft.WindowsAzure.Storage</span><span class="sxs-lookup"><span data-stu-id="74c3c-634">Microsoft.WindowsAzure.Storage</span></span>
    -   <span data-ttu-id="74c3c-635">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="74c3c-635">Newtonsoft.Json</span></span>
    -   <span data-ttu-id="74c3c-636">System.Spatial</span><span class="sxs-lookup"><span data-stu-id="74c3c-636">System.Spatial</span></span>

    ![Sélectionnez les plug-ins](images/AzureLabs-Lab8-91.png)

5.  <span data-ttu-id="74c3c-638">Avec *ces plug-ins spécifiques* sélectionné, **Décochez** **plateforme Any** et **Décochez** **WSAPlayer** puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-638">With *these specific plugins* selected, **uncheck** **Any Platform** and **uncheck** **WSAPlayer** then click **Apply**.</span></span>

    ![appliquer les modifications de la plateforme](images/AzureLabs-Lab8-92.png)

    > [!NOTE] 
    > <span data-ttu-id="74c3c-640">Vous marquez ces plug-ins particuliers à utiliser uniquement dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="74c3c-640">You are marking these particular plugins to only be used in the Unity Editor.</span></span> <span data-ttu-id="74c3c-641">Il s’agit, car il existe différentes versions des mêmes plug-ins dans le dossier WSA qui sera utilisé après que le projet est exporté à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="74c3c-641">This is because there are different versions of the same plugins in the WSA folder that will be used after the project is exported from Unity.</span></span>

6.  <span data-ttu-id="74c3c-642">Dans le **stockage** dossier de plug-in, sélectionnez uniquement :</span><span class="sxs-lookup"><span data-stu-id="74c3c-642">In the **Storage** plugin folder, select only:</span></span>

    -   <span data-ttu-id="74c3c-643">Microsoft.Data.Services.Client</span><span class="sxs-lookup"><span data-stu-id="74c3c-643">Microsoft.Data.Services.Client</span></span>

        ![Sélectionnez le client des services de données](images/AzureLabs-Lab8-93.png)

7.  <span data-ttu-id="74c3c-645">Vérifier le **processus ne** sous **paramètres de plateforme** et cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-645">Check the **Don't Process** box under **Platform Settings** and click **Apply**.</span></span>

    ![ne pas traiter](images/AzureLabs-Lab8-94.png)

    > [!NOTE] 
    > <span data-ttu-id="74c3c-647">Vous marquez ce plug-in « Ne pas traiter », car l’utilitaire de correction Unity assembly a des difficultés à traiter ce plug-in.</span><span class="sxs-lookup"><span data-stu-id="74c3c-647">You are marking this plugin "Don't process" because the Unity assembly patcher has difficulty processing this plugin.</span></span> <span data-ttu-id="74c3c-648">Le plug-in continue de fonctionner même si elle n’est pas traitée.</span><span class="sxs-lookup"><span data-stu-id="74c3c-648">The plugin will still work even though it isn't processed.</span></span>

## <a name="chapter-14---creating-the-tabletoscene-class-in-the-mixed-reality-unity-project"></a><span data-ttu-id="74c3c-649">Chapitre 14 - Création de la classe de TableToScene dans le projet Unity de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="74c3c-649">Chapter 14 - Creating the TableToScene class in the mixed reality Unity project</span></span>

<span data-ttu-id="74c3c-650">Le **TableToScene** classe est identique à celle qui est expliquée dans [chapitre 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).</span><span class="sxs-lookup"><span data-stu-id="74c3c-650">The **TableToScene** class is identical to the one explained in [Chapter 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).</span></span> <span data-ttu-id="74c3c-651">Créer la même classe dans la réalité mixte projet Unity suivant la même procédure est expliquée dans [chapitre 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).</span><span class="sxs-lookup"><span data-stu-id="74c3c-651">Create the same class in the mixed reality Unity Project following the same procedure explained in [Chapter 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).</span></span>

<span data-ttu-id="74c3c-652">Une fois que vous avez terminé ce chapitre, à la fois de votre **projets Unity** aura cette classe configurée sur l’appareil photo de Main.</span><span class="sxs-lookup"><span data-stu-id="74c3c-652">Once you have completed this Chapter, both of your **Unity Projects** will have this class set up on the Main Camera.</span></span>

## <a name="chapter-15---creating-the-notificationreceiver-class-in-the-mixed-reality-unity-project"></a><span data-ttu-id="74c3c-653">Chapitre 15 - création de la classe de NotificationReceiver dans le projet Unity de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="74c3c-653">Chapter 15 - Creating the NotificationReceiver class in the Mixed Reality Unity Project</span></span>

<span data-ttu-id="74c3c-654">Le deuxième script que vous créez est **NotificationReceiver**, qui est chargé de :</span><span class="sxs-lookup"><span data-stu-id="74c3c-654">The second script you need to create is **NotificationReceiver**, which is responsible for:</span></span>

-   <span data-ttu-id="74c3c-655">L’inscription de l’application avec le Hub de Notification lors de l’initialisation.</span><span class="sxs-lookup"><span data-stu-id="74c3c-655">Registering the app with the Notification Hub at initialization.</span></span>
-   <span data-ttu-id="74c3c-656">Écouter les notifications provenant du Hub de Notification.</span><span class="sxs-lookup"><span data-stu-id="74c3c-656">Listening to notifications coming from the Notification Hub.</span></span>
-   <span data-ttu-id="74c3c-657">Désérialiser les données d’objet à partir des notifications reçues.</span><span class="sxs-lookup"><span data-stu-id="74c3c-657">Deserializing the object data from received notifications.</span></span>
-   <span data-ttu-id="74c3c-658">Déplacer les GameObjects dans la scène, selon les données désérialisées.</span><span class="sxs-lookup"><span data-stu-id="74c3c-658">Move the GameObjects in the scene, based on the deserialized data.</span></span>

<span data-ttu-id="74c3c-659">Pour créer le **NotificationReceiver** script :</span><span class="sxs-lookup"><span data-stu-id="74c3c-659">To create the **NotificationReceiver** script:</span></span>

1.  <span data-ttu-id="74c3c-660">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**, **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-660">Right-click inside the **Scripts** folder, click **Create**, **C\# Script**.</span></span> <span data-ttu-id="74c3c-661">Nommez le script **NotificationReceiver**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-661">Name the script **NotificationReceiver**.</span></span>

    <span data-ttu-id="74c3c-662">![création du nouveau script c#](images/AzureLabs-Lab8-95.png)
    ![nommez-le NotificationReceiver](images/AzureLabs-Lab8-96.png)</span><span class="sxs-lookup"><span data-stu-id="74c3c-662">![create new c# script](images/AzureLabs-Lab8-95.png)
![name it NotificationReceiver](images/AzureLabs-Lab8-96.png)</span></span>

2.  <span data-ttu-id="74c3c-663">Double-cliquez sur le script pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="74c3c-663">Double click on the script to open it.</span></span>

3.  <span data-ttu-id="74c3c-664">Ajoutez les espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="74c3c-664">Add the following namespaces:</span></span>

    ```csharp
    //using Microsoft.WindowsAzure.Messaging;
    using Newtonsoft.Json;
    using System;
    using System.Collections;
    using UnityEngine;

    #if UNITY_WSA_10_0 && !UNITY_EDITOR
    using Windows.Networking.PushNotifications;
    #endif
    ```

4.  <span data-ttu-id="74c3c-665">Insérez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="74c3c-665">Insert the following variables:</span></span>

    ```csharp
        /// <summary>
        /// allows this class to behave like a singleton
        /// </summary>
        public static NotificationReceiver instance;

        /// <summary>
        /// Value set by the notification, new object position
        /// </summary>
        Vector3 newObjPosition;

        /// <summary>
        /// Value set by the notification, object name
        /// </summary>
        string gameObjectName;

        /// <summary>
        /// Value set by the notification, new object position
        /// </summary>
        bool notifReceived;

        /// <summary>
        /// Insert here your Notification Hub Service name 
        /// </summary>
        private string hubName = " -- Insert the name of your service -- ";

        /// <summary>
        /// Insert here your Notification Hub Service "Listen endpoint"
        /// </summary>
        private string hubListenEndpoint = "-Insert your Notification Hub Service Listen endpoint-";
    ```

5.  <span data-ttu-id="74c3c-666">Remplacez le **hubName** valeur avec le nom de votre Service de Hub de Notification, et **hubListenEndpoint** valeur avec la valeur de point de terminaison située dans l’onglet de stratégies d’accès, le Service Azure Notification Hub, le Portail Azure (voir l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="74c3c-666">Substitute the **hubName** value with your Notification Hub Service name, and **hubListenEndpoint** value with the endpoint value found in the Access Policies tab, Azure Notification Hub Service, in the Azure Portal (see image below).</span></span>

    ![Insérer le point de terminaison de notification hubs stratégie](images/AzureLabs-Lab8-97.png)

6.  <span data-ttu-id="74c3c-668">Ajoutez maintenant le **Start()** et **Awake()** méthodes pour initialiser la classe.</span><span class="sxs-lookup"><span data-stu-id="74c3c-668">Now add the **Start()** and **Awake()** methods to initialize the class.</span></span>

    ```csharp
        /// <summary>
        /// Triggers before initialization
        /// </summary>
        void Awake()
        {
            // static instance of this class
            instance = this;
        }

        /// <summary>
        /// Use this for initialization
        /// </summary>
        void Start()
        {
            // Register the App at launch
            InitNotificationsAsync();

            // Begin listening for notifications
            StartCoroutine(WaitForNotification());
        }
    ```

7.  <span data-ttu-id="74c3c-669">Ajouter le **WaitForNotification** méthode pour autoriser l’application recevoir des notifications à partir de la bibliothèque de Hub de Notification sans conflit avec le Thread principal :</span><span class="sxs-lookup"><span data-stu-id="74c3c-669">Add the **WaitForNotification** method to allow the app to receive notifications from the Notification Hub Library without clashing with the Main Thread:</span></span>

    ```csharp
        /// <summary>
        /// This notification listener is necessary to avoid clashes 
        /// between the notification hub and the main thread   
        /// </summary>
        private IEnumerator WaitForNotification()
        {
            while (true)
            {
                // Checks for notifications each second
                yield return new WaitForSeconds(1f);

                if (notifReceived)
                {
                    // If a notification is arrived, moved the appropriate object to the new position
                    GameObject.Find(gameObjectName).transform.position = newObjPosition;

                    // Reset the flag
                    notifReceived = false;
                }
            }
        }
    ```

8.  <span data-ttu-id="74c3c-670">La méthode suivante, **InitNotificationAsync()** , inscription de l’application avec la Service de Hub de notification lors de l’initialisation.</span><span class="sxs-lookup"><span data-stu-id="74c3c-670">The following method, **InitNotificationAsync()**, will register the application with the notification Hub Service at initialization.</span></span> <span data-ttu-id="74c3c-671">Le code est commenté car Unity ne seront pas en mesure de générer le projet.</span><span class="sxs-lookup"><span data-stu-id="74c3c-671">The code is commented out as Unity will not be able to Build the project.</span></span> <span data-ttu-id="74c3c-672">Vous allez supprimer les commentaires lorsque vous importez le package Nuget de messagerie Azure dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74c3c-672">You will remove the comments when you import the Azure Messaging Nuget package in Visual Studio.</span></span>

    ```csharp
        /// <summary>
        /// Register this application to the Notification Hub Service
        /// </summary>
        private async void InitNotificationsAsync()
        {
            // PushNotificationChannel channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // NotificationHub hub = new NotificationHub(hubName, hubListenEndpoint);

            // Registration result = await hub.RegisterNativeAsync(channel.Uri);

            // If registration was successful, subscribe to Push Notifications
            // if (result.RegistrationId != null)
            // {
            //     Debug.Log($"Registration Successful: {result.RegistrationId}");
            //     channel.PushNotificationReceived += Channel_PushNotificationReceived;
            // }
        }
    ```

9.  <span data-ttu-id="74c3c-673">Le gestionnaire suivant, **canal\_PushNotificationReceived()** , sera déclenchée chaque fois qu’une notification est reçue.</span><span class="sxs-lookup"><span data-stu-id="74c3c-673">The following handler, **Channel\_PushNotificationReceived()**, will be triggered every time a notification is received.</span></span> <span data-ttu-id="74c3c-674">Il désérialise la notification, qui sera l’entité de Table Azure qui a été déplacé sur l’Application de bureau et puis déplacez le GameObject correspondant dans la scène MR vers la même position.</span><span class="sxs-lookup"><span data-stu-id="74c3c-674">It will deserialize the notification, which will be the Azure Table Entity that has been moved on the Desktop Application, and then move the corresponding GameObject in the MR scene to the same position.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="74c3c-675">Le code est commenté, car le code fait référence à la bibliothèque de messagerie Azure, vous allez ajouter après la génération du projet Unity à l’aide du Gestionnaire de Package Nuget dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74c3c-675">The code is commented out because the code references the Azure Messaging library, which you will add after building the Unity project using the Nuget Package Manager, within Visual Studio.</span></span> <span data-ttu-id="74c3c-676">Par conséquent, le projet Unity ne sera pas en mesure de générer, sauf si elle est commentée. Sachez que devez vous générez votre projet et que vous souhaitez ensuite revenir à Unity, vous devrez **nouveau commentaire** ce code.</span><span class="sxs-lookup"><span data-stu-id="74c3c-676">As such, the Unity project will not be able to build, unless it is commented out. Be aware, that should you build your project, and then wish to return to Unity, you will need to **re-comment** that code.</span></span>

    ```csharp
        ///// <summary>
        ///// Handler called when a Push Notification is received
        ///// </summary>
        //private void Channel_PushNotificationReceived(PushNotificationChannel sender, PushNotificationReceivedEventArgs args)    
        //{
        //    Debug.Log("New Push Notification Received");
        //
        //    if (args.NotificationType == PushNotificationType.Raw)
        //    {
        //        //  Raw content of the Notification
        //        string jsonContent = args.RawNotification.Content;
        //
        //        // Deserialise the Raw content into an AzureTableEntity object
        //        AzureTableEntity ate = JsonConvert.DeserializeObject<AzureTableEntity>(jsonContent);
        //
        //        // The name of the Game Object to be moved
        //        gameObjectName = ate.RowKey;          
        //
        //        // The position where the Game Object has to be moved
        //        newObjPosition = new Vector3((float)ate.X, (float)ate.Y, (float)ate.Z);
        //
        //        // Flag thats a notification has been received
        //        notifReceived = true;
        //    }
        //}
    ```

10. <span data-ttu-id="74c3c-677">Pensez à enregistrer vos modifications avant de revenir à l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="74c3c-677">Remember to save your changes before going back to the Unity Editor.</span></span>

11. <span data-ttu-id="74c3c-678">Cliquez sur le **Main Camera** à partir de la **hiérarchie** panneau, afin que ses propriétés s’affichent dans le **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-678">Click the **Main Camera** from the **Hierarchy** panel, so that its properties appear in the **Inspector**.</span></span>

12. <span data-ttu-id="74c3c-679">Avec le **Scripts** ouvert, sélectionnez de dossier le **NotificationReceiver** de script et faites-le glisser sur le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-679">With the **Scripts** folder open, select the **NotificationReceiver** script and drag it onto the **Main Camera**.</span></span> <span data-ttu-id="74c3c-680">Le résultat doit être comme suit :</span><span class="sxs-lookup"><span data-stu-id="74c3c-680">The result should be as below:</span></span>

    ![Faites glisser de script de récepteur de notification à l’appareil photo](images/AzureLabs-Lab8-98.png)

    > [!NOTE]
    > <span data-ttu-id="74c3c-682">Si vous développez cela pour le Microsoft HoloLens, vous devez mettre à jour le **Main Camera**de *caméra* composant, afin que :</span><span class="sxs-lookup"><span data-stu-id="74c3c-682">If you are developing this for the Microsoft HoloLens, you will need to update the **Main Camera**'s *Camera* component, so that:</span></span>
    > - <span data-ttu-id="74c3c-683">Effacer les indicateurs : Couleur unie</span><span class="sxs-lookup"><span data-stu-id="74c3c-683">Clear Flags: Solid Color</span></span>
    > - <span data-ttu-id="74c3c-684">Background : Noir</span><span class="sxs-lookup"><span data-stu-id="74c3c-684">Background: Black</span></span>

## <a name="chapter-16---build-the-mixed-reality-project-to-uwp"></a><span data-ttu-id="74c3c-685">Chapitre 16 - générer le projet de réalité mixte vers UWP</span><span class="sxs-lookup"><span data-stu-id="74c3c-685">Chapter 16 - Build the Mixed Reality Project to UWP</span></span>

<span data-ttu-id="74c3c-686">Ce chapitre est identique au processus pour le projet précédent de génération.</span><span class="sxs-lookup"><span data-stu-id="74c3c-686">This Chapter is identical to build process for the previous project.</span></span> <span data-ttu-id="74c3c-687">Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée, il est temps de générer à partir de Unity.</span><span class="sxs-lookup"><span data-stu-id="74c3c-687">Everything needed for the Unity section of this project has now been completed, so it is time to build it from Unity.</span></span>

1.  <span data-ttu-id="74c3c-688">Accédez à **les paramètres de génération** ( **fichier** > **paramètres de Build** ).</span><span class="sxs-lookup"><span data-stu-id="74c3c-688">Navigate to **Build Settings** ( **File** > **Build Settings** ).</span></span>

2.  <span data-ttu-id="74c3c-689">À partir de la **paramètres de Build** menu, vérifiez **Unity C# projets**\* est cochée (ce qui vous permettra de modifier les scripts dans ce projet, après génération).</span><span class="sxs-lookup"><span data-stu-id="74c3c-689">From the **Build Settings** menu, ensure **Unity C# Projects**\* is ticked (which will allow you to edit the scripts in this project, after build).</span></span>

3.  <span data-ttu-id="74c3c-690">Une fois cette opération est effectuée, cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-690">After this is done, click **Build**.</span></span>

    ![Générer le projet](images/AzureLabs-Lab8-99.png)

4.  <span data-ttu-id="74c3c-692">Un **Explorateur de fichiers** fenêtre va contextuelle, vous invite à entrer un emplacement de Build.</span><span class="sxs-lookup"><span data-stu-id="74c3c-692">A **File Explorer** window will popup, prompting you for a location to Build.</span></span> <span data-ttu-id="74c3c-693">Créez un dossier (en cliquant sur **nouveau dossier** dans l’angle supérieur gauche) et nommez-le **génère**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-693">Create a new folder (by clicking **New Folder** in the top-left corner), and name it **BUILDS**.</span></span>

    ![créer le dossier de builds](images/AzureLabs-Lab8-100.png)

    1.  <span data-ttu-id="74c3c-695">Ouvrez le nouveau **génère** dossier et créez un autre dossier (à l’aide de **nouveau dossier** une fois de plus) et nommez-le **NH\_MR\_application**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-695">Open the new **BUILDS** folder, and create another folder (using **New Folder** once more), and name it **NH\_MR\_App**.</span></span>

        ![créer le dossier de NH_MR_Apps](images/AzureLabs-Lab8-101.png)

    2.  <span data-ttu-id="74c3c-697">Avec le **NH\_MR\_application** sélectionné.</span><span class="sxs-lookup"><span data-stu-id="74c3c-697">With the **NH\_MR\_App** selected.</span></span> <span data-ttu-id="74c3c-698">Cliquez sur **sélectionnez dossier**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-698">click **Select Folder**.</span></span> <span data-ttu-id="74c3c-699">Le projet prendra une minute ou donc en créer.</span><span class="sxs-lookup"><span data-stu-id="74c3c-699">The project will take a minute or so to build.</span></span>

5.  <span data-ttu-id="74c3c-700">Suivant la génération, un **Explorateur de fichiers** fenêtre s’ouvre à l’emplacement de votre nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="74c3c-700">Following the build, a **File Explorer** window will open at the location of your new project.</span></span>



## <a name="chapter-17---add-nuget-packages-to-the-unitymrnotifhub-solution"></a><span data-ttu-id="74c3c-701">Chapitre 17 - ajouter des packages NuGet à la UnityMRNotifHub Solution</span><span class="sxs-lookup"><span data-stu-id="74c3c-701">Chapter 17 - Add NuGet packages to the UnityMRNotifHub Solution</span></span>

> [!WARNING] 
> <span data-ttu-id="74c3c-702">N’oubliez pas que, une fois que vous ajoutez les Packages NuGet suivants (et les commentaires du code dans les prochains [chapitre](#chapter-18---edit-unitymrnotifhub-application-notificationreceiver-class)), le Code, la réouverture du projet Unity, présentera des erreurs.</span><span class="sxs-lookup"><span data-stu-id="74c3c-702">Please remember that, once you add the following NuGet Packages (and uncomment the code in the next [Chapter](#chapter-18---edit-unitymrnotifhub-application-notificationreceiver-class)), the Code, when reopened within the Unity Project, will present errors.</span></span> <span data-ttu-id="74c3c-703">Si vous souhaitez revenir en arrière et continuer à modifier dans l’éditeur Unity, vous avez besoin de commenter ce code errosome et puis supprimez les commentaires plus tard, une fois que vous êtes de retour dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="74c3c-703">If you wish to go back and continue editing in the Unity Editor, you will need comment that errosome code, and then uncomment again later, once you are back in Visual Studio.</span></span> 

<span data-ttu-id="74c3c-704">Une fois la build de réalité mixte a été terminée, accédez au projet de réalité mixte, que vous avez créé, et double-cliquez sur le fichier solution (.sln) dans ce dossier, pour ouvrir votre solution avec Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="74c3c-704">Once the mixed reality build has been completed, navigate to the mixed reality project, which you built, and double click on the solution (.sln) file within that folder, to open your solution with Visual Studio 2017.</span></span>
<span data-ttu-id="74c3c-705">Vous devrez maintenant ajouter le **WindowsAzure.Messaging.managed** package NuGet ; il s’agit d’une bibliothèque qui est utilisée pour recevoir des Notifications à partir du Hub de Notification.</span><span class="sxs-lookup"><span data-stu-id="74c3c-705">You will now need to add the **WindowsAzure.Messaging.managed** NuGet package; this is a library that is used to receive Notifications from the Notification Hub.</span></span>

<span data-ttu-id="74c3c-706">Pour importer le package NuGet :</span><span class="sxs-lookup"><span data-stu-id="74c3c-706">To import the NuGet package:</span></span>

1.  <span data-ttu-id="74c3c-707">Dans le **l’Explorateur de solutions**, cliquez avec le bouton droit sur votre Solution</span><span class="sxs-lookup"><span data-stu-id="74c3c-707">In the **Solution Explorer**, right click on your Solution</span></span>

2.  <span data-ttu-id="74c3c-708">Cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-708">Click on **Manage NuGet Packages**.</span></span>

    ![Ouvrez le gestionnaire nuget](images/AzureLabs-Lab8-102.png)

3.  <span data-ttu-id="74c3c-710">Sélectionnez le ***Parcourir*** onglet et recherchez **WindowsAzure.Messaging.managed**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-710">Select the ***Browse*** tab and search for **WindowsAzure.Messaging.managed**.</span></span>

    ![Recherchez le package de messagerie windows azure](images/AzureLabs-Lab8-103.png)

4.  <span data-ttu-id="74c3c-712">Sélectionnez le résultat (comme indiqué ci-dessous) et dans la fenêtre à droite, sélectionnez la case à cocher à côté **projet**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-712">Select the result (as shown below), and in the window to the right, select the checkbox next to **Project**.</span></span> <span data-ttu-id="74c3c-713">Cela place un cycle dans la case à cocher à côté **projet**, ainsi que la case à cocher à côté du **Assembly-CSharp** et **UnityMRNotifHub** projet.</span><span class="sxs-lookup"><span data-stu-id="74c3c-713">This will place a tick in the checkbox next to **Project**, along with the checkbox next to the **Assembly-CSharp** and **UnityMRNotifHub** project.</span></span>

    ![Cochez tous les projets](images/AzureLabs-Lab8-104.png)

5.  <span data-ttu-id="74c3c-715">La version fournie initialement **ne peut pas** être compatible avec ce projet.</span><span class="sxs-lookup"><span data-stu-id="74c3c-715">The version initially provided **may not** be compatible with this project.</span></span> <span data-ttu-id="74c3c-716">Par conséquent, cliquez sur le menu déroulant à côté **Version**, puis cliquez sur **Version 0.1.7.9**, puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-716">Therefore, click on the dropdown menu next to **Version**, and click **Version 0.1.7.9**, then click **Install**.</span></span>

6.  <span data-ttu-id="74c3c-717">Vous avez maintenant terminé l’installation du package NuGet.</span><span class="sxs-lookup"><span data-stu-id="74c3c-717">You have now finished installing the NuGet package.</span></span> <span data-ttu-id="74c3c-718">Rechercher le code commenté que vous avez entré dans le **NotificationReceiver** classe et supprimez les commentaires...</span><span class="sxs-lookup"><span data-stu-id="74c3c-718">Find the commented code you entered in the **NotificationReceiver** class and remove the comments..</span></span>



## <a name="chapter-18---edit-unitymrnotifhub-application-notificationreceiver-class"></a><span data-ttu-id="74c3c-719">Chapitre 18 - application d’édition UnityMRNotifHub, NotificationReceiver classe</span><span class="sxs-lookup"><span data-stu-id="74c3c-719">Chapter 18 - Edit UnityMRNotifHub application, NotificationReceiver class</span></span>

<span data-ttu-id="74c3c-720">Après avoir ajouté le **les Packages NuGet**, vous devrez *supprimez les commentaires* partie du code dans le **NotificationReceiver** classe.</span><span class="sxs-lookup"><span data-stu-id="74c3c-720">Following having added the **NuGet Packages**, you will need to *uncomment* some of the code within the **NotificationReceiver** class.</span></span>

<span data-ttu-id="74c3c-721">Cela comprend les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="74c3c-721">This includes:</span></span>

1. <span data-ttu-id="74c3c-722">L’espace de noms en haut :</span><span class="sxs-lookup"><span data-stu-id="74c3c-722">The namespace at the top:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Messaging;
    ```

2. <span data-ttu-id="74c3c-723">Tout le code dans le **InitNotificationsAsync()** méthode :</span><span class="sxs-lookup"><span data-stu-id="74c3c-723">All the code within the **InitNotificationsAsync()** method:</span></span>

    ```csharp
        /// <summary>
        /// Register this application to the Notification Hub Service
        /// </summary>
        private async void InitNotificationsAsync()
        {
            PushNotificationChannel channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            NotificationHub hub = new NotificationHub(hubName, hubListenEndpoint);

            Registration result = await hub.RegisterNativeAsync(channel.Uri);

            // If registration was successful, subscribe to Push Notifications
            if (result.RegistrationId != null)
            {
                Debug.Log($"Registration Successful: {result.RegistrationId}");
                channel.PushNotificationReceived += Channel_PushNotificationReceived;
            }
        }
    ```

> [!WARNING]
> <span data-ttu-id="74c3c-724">Le code ci-dessus comporte un commentaire : Vérifiez que vous n’avez pas accidentellement *sans commentaire* qui commentaire (comme le code compilera pas si vous avez !).</span><span class="sxs-lookup"><span data-stu-id="74c3c-724">The code above has a comment in it: ensure that you have not accidentally *uncommented* that comment (as the code will not compile if you have!).</span></span>

3. <span data-ttu-id="74c3c-725">Et, enfin, le **Channel_PushNotificationReceived** événement :</span><span class="sxs-lookup"><span data-stu-id="74c3c-725">And, lastly, the **Channel_PushNotificationReceived** event:</span></span>

    ```csharp
        /// <summary>
        /// Handler called when a Push Notification is received
        /// </summary>
        private void Channel_PushNotificationReceived(PushNotificationChannel sender, PushNotificationReceivedEventArgs args)
        {
            Debug.Log("New Push Notification Received");

            if (args.NotificationType == PushNotificationType.Raw)
            {
                //  Raw content of the Notification
                string jsonContent = args.RawNotification.Content;

                // Deserialize the Raw content into an AzureTableEntity object
                AzureTableEntity ate = JsonConvert.DeserializeObject<AzureTableEntity>(jsonContent);

                // The name of the Game Object to be moved
                gameObjectName = ate.RowKey;

                // The position where the Game Object has to be moved
                newObjPosition = new Vector3((float)ate.X, (float)ate.Y, (float)ate.Z);

                // Flag thats a notification has been received
                notifReceived = true;
            }
        }
    ```

<span data-ttu-id="74c3c-726">Avec ces sans commentaire, assurez-vous que vous enregistrerez, puis passez au chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="74c3c-726">With these uncommented, ensure that you save, and then proceed to the next Chapter.</span></span>

## <a name="chapter-19---associate-the-mixed-reality-project-to-the-store-app"></a><span data-ttu-id="74c3c-727">Chapitre 19 - associer le projet de réalité mixte à l’application de Store</span><span class="sxs-lookup"><span data-stu-id="74c3c-727">Chapter 19 - Associate the mixed reality project to the Store app</span></span>

<span data-ttu-id="74c3c-728">Vous devez maintenant associer la **une réalité mixte** projet à l’application de Store que vous avez créé dans au début du laboratoire.</span><span class="sxs-lookup"><span data-stu-id="74c3c-728">You now need to associate the **mixed reality** project to the Store App you created in at the start of the lab.</span></span>

1.  <span data-ttu-id="74c3c-729">Ouvrez la solution.</span><span class="sxs-lookup"><span data-stu-id="74c3c-729">Open the solution.</span></span>

2.  <span data-ttu-id="74c3c-730">Cliquez avec le bouton droit sur l’application UWP projet dans le volet Explorateur de solutions, permettant d’atteindre **Store**, et **associer l’application avec le Store...** .</span><span class="sxs-lookup"><span data-stu-id="74c3c-730">Right click on the UWP app Project in the Solution Explorer panel, the go to **Store**, and **Associate App with the Store...**.</span></span>

    ![ouverture d’association de magasin](images/AzureLabs-Lab8-105.png)

3.  <span data-ttu-id="74c3c-732">Une nouvelle fenêtre s’affiche appelée **associer votre application du Windows Store**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-732">A new window will appear called **Associate Your App with the Windows Store**.</span></span> <span data-ttu-id="74c3c-733">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-733">Click **Next**.</span></span>

    ![Accédez à l’écran suivant](images/AzureLabs-Lab8-106.png)

4.  <span data-ttu-id="74c3c-735">Il charge toutes les applications associé au compte sur lequel vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="74c3c-735">It will load up all the Applications associated with the Account which you have logged in.</span></span> <span data-ttu-id="74c3c-736">Si vous n’êtes pas connecté votre compte, vous pouvez **Log In** sur cette page.</span><span class="sxs-lookup"><span data-stu-id="74c3c-736">If you are not logged in to your account, you can **Log In** on this page.</span></span>

5.  <span data-ttu-id="74c3c-737">Rechercher la **nom de l’application de Store** que vous avez créé au début de ce didacticiel et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="74c3c-737">Find the **Store App name** that you created at the start of this tutorial and select it.</span></span> <span data-ttu-id="74c3c-738">Ensuite, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-738">Then click **Next**.</span></span>

    ![Recherchez et sélectionnez votre nom de magasin](images/AzureLabs-Lab8-107.png)

6.  <span data-ttu-id="74c3c-740">Cliquez sur **associer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-740">Click **Associate**.</span></span>

    ![associer l’application](images/AzureLabs-Lab8-108.png)

7.  <span data-ttu-id="74c3c-742">Votre application est maintenant **associés** avec l’application de Store.</span><span class="sxs-lookup"><span data-stu-id="74c3c-742">Your App is now **Associated** with the Store App.</span></span> <span data-ttu-id="74c3c-743">Cela est nécessaire pour l’activation des Notifications.</span><span class="sxs-lookup"><span data-stu-id="74c3c-743">This is necessary for enabling Notifications.</span></span>

## <a name="chapter-20---deploy-unitymrnotifhub-and-unitydesktopnotifhub-applications"></a><span data-ttu-id="74c3c-744">Chapitre 20 - déployer des applications UnityMRNotifHub et UnityDesktopNotifHub</span><span class="sxs-lookup"><span data-stu-id="74c3c-744">Chapter 20 - Deploy UnityMRNotifHub and UnityDesktopNotifHub applications</span></span>

<span data-ttu-id="74c3c-745">Ce chapitre peut être plus facile avec deux personnes, comme le résultat inclut les applications en cours d’exécution, une en cours d’exécution sur votre ordinateur de bureau et l’autre au sein de votre casque immersive.</span><span class="sxs-lookup"><span data-stu-id="74c3c-745">This Chapter may be easier with two people, as the result will include both apps running, one running on your computer Desktop, and the other within your immersive headset.</span></span>

<span data-ttu-id="74c3c-746">L’application de casque immersives attend de recevoir des modifications à la scène (modifications de la position de la GameObjects local), et l’application de bureau apporter des modifications à leur scène local (changements de position), qui est partagé par l’application MR.</span><span class="sxs-lookup"><span data-stu-id="74c3c-746">The immersive headset app is waiting to receive changes to the scene (position changes of the local GameObjects), and the Desktop app will be making changes to their local scene (position changes), which will be shared to the MR app.</span></span> <span data-ttu-id="74c3c-747">Il judicieux pour déployer l’application MR en premier, suivie de l’application de bureau, afin que le récepteur peut commencer à écouter.</span><span class="sxs-lookup"><span data-stu-id="74c3c-747">It makes sense to deploy the MR app first, followed by the Desktop app, so that the receiver can begin listening.</span></span>

<span data-ttu-id="74c3c-748">Pour déployer le **UnityMRNotifHub** application sur votre ordinateur Local :</span><span class="sxs-lookup"><span data-stu-id="74c3c-748">To deploy the **UnityMRNotifHub** app on your Local Machine:</span></span>

1.  <span data-ttu-id="74c3c-749">Ouvrez le fichier de solution de votre **UnityMRNotifHub** app dans **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-749">Open the solution file of your **UnityMRNotifHub** app in **Visual Studio 2017**.</span></span>

2.  <span data-ttu-id="74c3c-750">Dans le **plateforme de Solution**, sélectionnez **x86, Local Machine**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-750">In the **Solution Platform**, select **x86, Local Machine**.</span></span>

3.  <span data-ttu-id="74c3c-751">Dans le **Configuration de la Solution** sélectionnez **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-751">In the **Solution Configuration** select **Debug**.</span></span>

    ![configuration de projet de jeu](images/AzureLabs-Lab8-109.png)

4.  <span data-ttu-id="74c3c-753">Accédez à **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="74c3c-753">Go to **Build menu** and click on **Deploy Solution** to sideload the application to your machine.</span></span>

5.  <span data-ttu-id="74c3c-754">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancée.</span><span class="sxs-lookup"><span data-stu-id="74c3c-754">Your App should now appear in the list of installed apps, ready to be launched.</span></span>

<span data-ttu-id="74c3c-755">Pour déployer le **UnityDesktopNotifHub** application sur l’ordinateur Local :</span><span class="sxs-lookup"><span data-stu-id="74c3c-755">To deploy the **UnityDesktopNotifHub** app on Local Machine:</span></span>

1.  <span data-ttu-id="74c3c-756">Ouvrez le fichier de solution de votre **UnityDesktopNotifHub** app dans **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-756">Open the solution file of your **UnityDesktopNotifHub** app in **Visual Studio 2017**.</span></span>

2.  <span data-ttu-id="74c3c-757">Dans le **plateforme de Solution**, sélectionnez **x86, Local Machine**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-757">In the **Solution Platform**, select **x86, Local Machine**.</span></span>

3.  <span data-ttu-id="74c3c-758">Dans le **Configuration de la Solution** sélectionnez **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="74c3c-758">In the **Solution Configuration** select **Debug**.</span></span>

    ![configuration de projet de jeu](images/AzureLabs-Lab8-110.png)

4.  <span data-ttu-id="74c3c-760">Accédez à **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="74c3c-760">Go to **Build menu** and click on **Deploy Solution** to sideload the application to your machine.</span></span>

5.  <span data-ttu-id="74c3c-761">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancée.</span><span class="sxs-lookup"><span data-stu-id="74c3c-761">Your App should now appear in the list of installed apps, ready to be launched.</span></span>

6.  <span data-ttu-id="74c3c-762">Lancez l’application de réalité mixte, suivie de l’application de bureau.</span><span class="sxs-lookup"><span data-stu-id="74c3c-762">Launch the mixed reality application, followed by the Desktop application.</span></span>

<span data-ttu-id="74c3c-763">Avec les deux applications en cours d’exécution, déplacer un objet dans la scène de postes de travail (en utilisant le bouton de la souris gauche).</span><span class="sxs-lookup"><span data-stu-id="74c3c-763">With both applications running, move an object in the desktop scene (using the Left Mouse Button).</span></span> <span data-ttu-id="74c3c-764">Ces changements de position seront être effectuées localement, sérialisés et envoyés au service d’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="74c3c-764">These positional changes will be made locally, serialized, and sent to the Function App service.</span></span> <span data-ttu-id="74c3c-765">Le service d’application de fonction sera puis mettez à jour la Table, ainsi que le Hub de Notification.</span><span class="sxs-lookup"><span data-stu-id="74c3c-765">The Function App service will then update the Table along with the Notification Hub.</span></span> <span data-ttu-id="74c3c-766">Ayant reçu une mise à jour, le Hub de Notification envoie les données mises à jour directement à toutes les applications inscrites (dans ce cas, l’application casque immersives) qui seront ensuite désérialiser les données entrantes et appliquer les nouvelles données positionnelles aux objets locales, en les déplaçant dans la scène.</span><span class="sxs-lookup"><span data-stu-id="74c3c-766">Having received an update, the Notification Hub will send the updated data directly to all the registered applications (in this case the immersive headset app), which will then deserialize the incoming data, and apply the new positional data to the local objects, moving them in scene.</span></span>


## <a name="your-finished-your-azure-notification-hubs-application"></a><span data-ttu-id="74c3c-767">Votre terminé votre application Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="74c3c-767">Your finished your Azure Notification Hubs application</span></span>
 
<span data-ttu-id="74c3c-768">Félicitations, vous avez créé une application de réalité mixte qui tire parti du Service de concentrateurs de Notification Azure et autorise la communication entre les applications.</span><span class="sxs-lookup"><span data-stu-id="74c3c-768">Congratulations, you built a mixed reality app that leverages the Azure Notification Hubs Service and allow communication between apps.</span></span>
 
![produit final-fin](images/AzureLabs-Lab8-00.png)
 
## <a name="bonus-exercises"></a><span data-ttu-id="74c3c-770">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="74c3c-770">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="74c3c-771">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="74c3c-771">Exercise 1</span></span>

<span data-ttu-id="74c3c-772">Vous pouvez imaginer comment modifier la couleur de la GameObjects et envoyer cette notification vers d’autres applications d’affichage de la scène</span><span class="sxs-lookup"><span data-stu-id="74c3c-772">Can you work out how to change the color of the GameObjects and send that notification to other apps viewing the scene?</span></span>

### <a name="exercise-2"></a><span data-ttu-id="74c3c-773">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="74c3c-773">Exercise 2</span></span>

<span data-ttu-id="74c3c-774">Possibilité d’ajouter le déplacement de la GameObjects à votre application MR et voir la scène mis à jour dans votre application de bureau ?</span><span class="sxs-lookup"><span data-stu-id="74c3c-774">Can you add movement of the GameObjects to your MR app and see the updated scene in your desktop app?</span></span>
