---
title: RM et Azure 308-notifications entre appareils
description: Suivez ce cours pour apprendre à implémenter Azure Notification Hubs, Azure Functions et le stockage Azure et les tables dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Académie, Unity, didacticiel, API, notification, fonctions, tables, notification hubs, hololens, immersif, VR
ms.openlocfilehash: d65750f37815efecae85e7bff85318a234079af8
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438757"
---
>[!NOTE]
><span data-ttu-id="4d13f-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="4d13f-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="4d13f-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="4d13f-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="4d13f-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="4d13f-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="4d13f-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4d13f-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="4d13f-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="4d13f-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="4d13f-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="4d13f-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-and-azure-308-cross-device-notifications"></a><span data-ttu-id="4d13f-110">MR et Azure 308 : notifications entre appareils</span><span class="sxs-lookup"><span data-stu-id="4d13f-110">MR and Azure 308: Cross-device notifications</span></span>

![produit final-début](images/AzureLabs-Lab8-00.png)

<span data-ttu-id="4d13f-112">Dans ce cours, vous allez apprendre à ajouter des fonctionnalités de Notification Hubs à une application de réalité mixte à l’aide d’Azure Notification Hubs, de tables Azure et d’Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="4d13f-112">In this course, you will learn how to add Notification Hubs capabilities to a mixed reality application using Azure Notification Hubs, Azure Tables, and Azure Functions.</span></span>

<span data-ttu-id="4d13f-113">**Azure notification hubs** est un service Microsoft, qui permet aux développeurs d’envoyer des notifications push ciblées et personnalisées à n’importe quelle plateforme, toutes alimentées dans le Cloud.</span><span class="sxs-lookup"><span data-stu-id="4d13f-113">**Azure Notification Hubs** is a Microsoft service, which allows developers to send targeted and personalized push notifications to any platform, all powered within the cloud.</span></span> <span data-ttu-id="4d13f-114">Cela permet aux développeurs de communiquer efficacement avec les utilisateurs finaux, ou même de communiquer entre différentes applications, en fonction du scénario.</span><span class="sxs-lookup"><span data-stu-id="4d13f-114">This can effectively allow developers to communicate with end users, or even communicate between various applications, depending on the scenario.</span></span> <span data-ttu-id="4d13f-115">Pour plus d’informations, consultez la [page](https://docs.microsoft.com/azure/notification-hubs/notification-hubs-push-notification-overview) **notification hubs Azure** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-115">For more information, visit the **Azure Notification Hubs** [page](https://docs.microsoft.com/azure/notification-hubs/notification-hubs-push-notification-overview).</span></span>

<span data-ttu-id="4d13f-116">**Azure Functions** est un service Microsoft, qui permet aux développeurs d’exécuter de petits morceaux de code, « functions », dans Azure.</span><span class="sxs-lookup"><span data-stu-id="4d13f-116">**Azure Functions** is a Microsoft service, which allows developers to run small pieces of code, 'functions', in Azure.</span></span> <span data-ttu-id="4d13f-117">Cela permet de déléguer le travail au Cloud, plutôt qu’à votre application locale, ce qui peut avoir de nombreux avantages.</span><span class="sxs-lookup"><span data-stu-id="4d13f-117">This provides a way to delegate work to the cloud, rather than your local application, which can have many benefits.</span></span> <span data-ttu-id="4d13f-118">**Azure Functions** prend en charge plusieurs langages de développement, notamment C\#, F\#, node. js, Java et php.</span><span class="sxs-lookup"><span data-stu-id="4d13f-118">**Azure Functions** supports several development languages, including C\#, F\#, Node.js, Java, and PHP.</span></span> <span data-ttu-id="4d13f-119">Pour plus d’informations, consultez la [page](https://docs.microsoft.com/azure/azure-functions/functions-overview) **Azure Functions** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-119">For more information, visit the **Azure Functions** [page](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span></span>

<span data-ttu-id="4d13f-120">**Azure tables** est un service Cloud Microsoft qui permet aux développeurs de stocker des données non SQL structurées dans le Cloud, ce qui les rend facilement accessibles partout.</span><span class="sxs-lookup"><span data-stu-id="4d13f-120">**Azure Tables** is a Microsoft cloud service, which allows developers to store structured non-SQL data in the cloud, making it easily accessible anywhere.</span></span> <span data-ttu-id="4d13f-121">Le service dispose d’une conception sans schéma, ce qui permet l’évolution des tables en fonction des besoins et est donc très flexible.</span><span class="sxs-lookup"><span data-stu-id="4d13f-121">The service boasts a schemaless design, allowing for the evolution of tables as needed, and thus is very flexible.</span></span> <span data-ttu-id="4d13f-122">Pour plus d’informations, consultez la [page](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview) **tables Azure**</span><span class="sxs-lookup"><span data-stu-id="4d13f-122">For more information, visit the **Azure Tables** [page](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)</span></span>

<span data-ttu-id="4d13f-123">Une fois ce cours terminé, vous disposerez d’une application de casque et d’une application de PC de bureau, qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d13f-123">Having completed this course, you will have a mixed reality immersive headset application, and a Desktop PC application, which will be able to do the following:</span></span>

1. <span data-ttu-id="4d13f-124">L’application PC Desktop permet à l’utilisateur de déplacer un objet dans l’espace 2D (X et Y) à l’aide de la souris.</span><span class="sxs-lookup"><span data-stu-id="4d13f-124">The Desktop PC app will allow the user to move an object in 2D space (X and Y), using the mouse.</span></span>

2. <span data-ttu-id="4d13f-125">Le déplacement d’objets dans l’application PC est envoyé au Cloud à l’aide de JSON, qui se présente sous la forme d’une chaîne contenant un ID d’objet, un type et des informations de transformation (coordonnées X et Y).</span><span class="sxs-lookup"><span data-stu-id="4d13f-125">The movement of objects within the PC app will be sent to the cloud using JSON, which will be in the form of a string, containing an object ID, type, and transform information (X and Y coordinates).</span></span> 

3. <span data-ttu-id="4d13f-126">L’application de réalité mixte, qui a une scène identique à celle de l’application de bureau, recevra des notifications concernant le déplacement d’objets à partir du service Notification Hubs (qui vient d’être mis à jour par l’application du PC de bureau).</span><span class="sxs-lookup"><span data-stu-id="4d13f-126">The mixed reality app, which has an identical scene to the desktop app, will receive notifications regarding object movement, from the Notification Hubs service (which has just been updated by the Desktop PC app).</span></span> 

4. <span data-ttu-id="4d13f-127">Lors de la réception d’une notification, qui contient les informations relatives à l’ID d’objet, au type et à la transformation, l’application de réalité mixte applique les informations reçues à sa propre scène.</span><span class="sxs-lookup"><span data-stu-id="4d13f-127">Upon receiving a notification, which will contain the object ID, type, and transform information, the mixed reality app will apply the received information to its own scene.</span></span>

<span data-ttu-id="4d13f-128">Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception.</span><span class="sxs-lookup"><span data-stu-id="4d13f-128">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="4d13f-129">Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="4d13f-129">This course is designed to teach you how to integrate an Azure Service with your Unity Project.</span></span> <span data-ttu-id="4d13f-130">C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="4d13f-130">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span> <span data-ttu-id="4d13f-131">Ce cours est un didacticiel autonome qui n’implique pas directement d’autres laboratoires de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="4d13f-131">This course is a self-contained tutorial, which does not directly involve any other Mixed Reality Labs.</span></span>

## <a name="device-support"></a><span data-ttu-id="4d13f-132">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="4d13f-132">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="4d13f-133">Course</span><span class="sxs-lookup"><span data-stu-id="4d13f-133">Course</span></span></th><th style="width:150px"> <span data-ttu-id="4d13f-134"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="4d13f-134"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="4d13f-135"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="4d13f-135"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="4d13f-136">MR et Azure 308 : notifications entre appareils</span><span class="sxs-lookup"><span data-stu-id="4d13f-136">MR and Azure 308: Cross-device notifications</span></span></td><td style="text-align: center;"> <span data-ttu-id="4d13f-137">✔️</span><span class="sxs-lookup"><span data-stu-id="4d13f-137">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="4d13f-138">✔️</span><span class="sxs-lookup"><span data-stu-id="4d13f-138">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="4d13f-139">Bien que ce cours se concentre principalement sur les casques de Windows Mixed Reality (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours à Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="4d13f-139">While this course primarily focuses on Windows Mixed Reality immersive (VR) headsets, you can also apply what you learn in this course to Microsoft HoloLens.</span></span> <span data-ttu-id="4d13f-140">À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge HoloLens.</span><span class="sxs-lookup"><span data-stu-id="4d13f-140">As you follow along with the course, you will see notes on any changes you might need to employ to support HoloLens.</span></span> <span data-ttu-id="4d13f-141">Lorsque vous utilisez HoloLens, vous remarquerez peut-être un écho pendant la capture vocale.</span><span class="sxs-lookup"><span data-stu-id="4d13f-141">When using HoloLens, you may notice some echo during voice capture.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d13f-142">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="4d13f-142">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="4d13f-143">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="4d13f-143">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="4d13f-144">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="4d13f-144">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="4d13f-145">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4d13f-145">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="4d13f-146">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours :</span><span class="sxs-lookup"><span data-stu-id="4d13f-146">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="4d13f-147">Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)</span><span class="sxs-lookup"><span data-stu-id="4d13f-147">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="4d13f-148">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="4d13f-148">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="4d13f-149">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="4d13f-149">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="4d13f-150">Unity 2017,4</span><span class="sxs-lookup"><span data-stu-id="4d13f-150">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="4d13f-151">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4d13f-151">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="4d13f-152">Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="4d13f-152">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="4d13f-153">Accès Internet pour l’installation d’Azure et pour accéder Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="4d13f-153">Internet access for Azure setup and to access Notification Hubs</span></span>

## <a name="before-you-start"></a><span data-ttu-id="4d13f-154">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4d13f-154">Before you start</span></span>

- <span data-ttu-id="4d13f-155">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="4d13f-155">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
- <span data-ttu-id="4d13f-156">Vous devez être le propriétaire de votre portail des développeurs Microsoft et du portail d’inscription des applications. sinon, vous n’êtes pas autorisé à accéder à l’application dans le [Chapitre 2](#chapter-2---retrieve-your-new-apps-credentials).</span><span class="sxs-lookup"><span data-stu-id="4d13f-156">You must be the owner of your Microsoft Developer Portal and your Application Registration Portal, otherwise you will not have permission to access the app in [Chapter 2](#chapter-2---retrieve-your-new-apps-credentials).</span></span>

## <a name="chapter-1---create-an-application-on-the-microsoft-developer-portal"></a><span data-ttu-id="4d13f-157">Chapitre 1-créer une application sur le portail des développeurs Microsoft</span><span class="sxs-lookup"><span data-stu-id="4d13f-157">Chapter 1 - Create an application on the Microsoft Developer Portal</span></span>

<span data-ttu-id="4d13f-158">Pour utiliser le service **Azure notification hubs** , vous devez créer une application sur le portail des développeurs Microsoft, car votre application doit être inscrite, afin de pouvoir envoyer et recevoir des notifications.</span><span class="sxs-lookup"><span data-stu-id="4d13f-158">To use the **Azure Notification Hubs** Service, you will need to create an Application on the Microsoft Developer Portal, as your application will need to be registered, so that it can send and receive notifications.</span></span>

1.  <span data-ttu-id="4d13f-159">Connectez-vous au [portail des développeurs Microsoft](https://developer.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="4d13f-159">Log in to the [Microsoft Developer Portal](https://developer.microsoft.com/dashboard).</span></span>

    > <span data-ttu-id="4d13f-160">Vous devrez vous connecter à votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4d13f-160">You will need to log in to your Microsoft Account.</span></span>

2.  <span data-ttu-id="4d13f-161">Dans le tableau de bord, cliquez sur **créer une application**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-161">From the Dashboard, click **Create a new app**.</span></span>

    ![Créer une application](images/AzureLabs-Lab8-01.png)

3.  <span data-ttu-id="4d13f-163">Une fenêtre contextuelle s’affiche, dans laquelle vous devez réserver un nom pour votre nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="4d13f-163">A popup will appear, wherein you need to reserve a name for your new app.</span></span> <span data-ttu-id="4d13f-164">Dans la zone de texte, insérez un nom approprié ; Si le nom choisi est disponible, un cycle s’affiche à droite de la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4d13f-164">In the textbox, insert an appropriate name; if the chosen name is available, a tick will appear to the right of the textbox.</span></span> <span data-ttu-id="4d13f-165">Une fois que vous avez un nom disponible inséré, cliquez sur le bouton **réserver un nom de produit** en bas à gauche de la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="4d13f-165">Once you have an available name inserted, click the **Reserve product name** button to the bottom left of the popup.</span></span>

    ![inverser un nom](images/AzureLabs-Lab8-02.png)

4.  <span data-ttu-id="4d13f-167">Une fois l’application créée, vous êtes prêt à passer au chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="4d13f-167">With the app now created, you are ready to move to the next Chapter.</span></span>

## <a name="chapter-2---retrieve-your-new-apps-credentials"></a><span data-ttu-id="4d13f-168">Chapitre 2-récupération des informations d’identification de vos nouvelles applications</span><span class="sxs-lookup"><span data-stu-id="4d13f-168">Chapter 2 - Retrieve your new apps credentials</span></span>

<span data-ttu-id="4d13f-169">Connectez-vous au portail d’inscription des applications, où votre nouvelle application sera listée et récupérez les informations d’identification qui seront utilisées pour configurer le **Service notification hubs** dans le **portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-169">Log into the Application Registration Portal, where your new app will be listed, and retrieve the credentials which will be used to setup the **Notification Hubs Service** within the **Azure Portal**.</span></span>

1.  <span data-ttu-id="4d13f-170">Accédez au [portail d’inscription des applications](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="4d13f-170">Navigate to the [Application Registration Portal](https://apps.dev.microsoft.com).</span></span>

    ![portail d’inscription des applications](images/AzureLabs-Lab8-03.png)

    > [!WARNING] 
    > <span data-ttu-id="4d13f-172">Vous devrez utiliser votre compte Microsoft pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="4d13f-172">You will need to use your Microsoft Account to Login.</span></span>  
    > <span data-ttu-id="4d13f-173">Il **doit** s’agir du compte Microsoft que vous avez utilisé dans le [chapitre](#chapter-1---create-an-application-on-the-microsoft-developer-portal)précédent, avec le portail des développeurs du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="4d13f-173">This **must** be the Microsoft Account which you used in the previous [Chapter](#chapter-1---create-an-application-on-the-microsoft-developer-portal), with the Windows Store Developer portal.</span></span>

2.  <span data-ttu-id="4d13f-174">Votre application se trouve dans la section **mes applications** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-174">You will find your app under the **My applications** section.</span></span> <span data-ttu-id="4d13f-175">Une fois que vous l’avez trouvé, cliquez dessus pour afficher une nouvelle page qui contient le nom de l’application et l' **inscription**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-175">Once you have found it, click on it and you will be taken to a new page which has the app name plus **Registration**.</span></span>

    ![votre application nouvellement inscrite](images/AzureLabs-Lab8-04.png)

3.  <span data-ttu-id="4d13f-177">Faites défiler la page d’inscription pour trouver la section secrets de votre **application** et le **SID du package** pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4d13f-177">Scroll down the registration page to find your **Application Secrets** section and the **Package SID** for your app.</span></span> <span data-ttu-id="4d13f-178">Copiez-les pour les utiliser avec la configuration du **service Azure notification hubs** dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="4d13f-178">Copy both for use with setting up the **Azure Notification Hubs Service** in the next Chapter.</span></span>

    ![secrets d’application](images/AzureLabs-Lab8-05.png)

## <a name="chapter-3---setup-azure-portal-create-notification-hubs-service"></a><span data-ttu-id="4d13f-180">Chapitre 3-configurer le portail Azure : créer Notification Hubs service</span><span class="sxs-lookup"><span data-stu-id="4d13f-180">Chapter 3 - Setup Azure Portal: create Notification Hubs Service</span></span>

<span data-ttu-id="4d13f-181">Une fois les informations d’identification de vos applications récupérées, vous devez accéder au portail Azure, où vous allez créer un service Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="4d13f-181">With your apps credentials retrieved, you will need to go to the Azure Portal, where you will create an Azure Notification Hubs Service.</span></span>

1.  <span data-ttu-id="4d13f-182">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4d13f-182">Log into the [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4d13f-183">Si vous n’avez pas encore de compte Azure, vous devez en créer un.</span><span class="sxs-lookup"><span data-stu-id="4d13f-183">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="4d13f-184">Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="4d13f-184">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="4d13f-185">Une fois que vous êtes connecté, cliquez sur **nouveau** dans l’angle supérieur gauche et recherchez **notification Hub**, puis cliquez sur ***entrée***.</span><span class="sxs-lookup"><span data-stu-id="4d13f-185">Once you are logged in, click on **New** in the top left corner, and search for **Notification Hub**, and click ***Enter***.</span></span>

    ![Rechercher le hub de notification](images/AzureLabs-Lab8-06.png)

    > [!NOTE] 
    > <span data-ttu-id="4d13f-187">Le mot ***nouveau*** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.</span><span class="sxs-lookup"><span data-stu-id="4d13f-187">The word ***New*** may have been replaced with **Create a resource**, in newer portals.</span></span>

3.  <span data-ttu-id="4d13f-188">La nouvelle page fournit une description du service *notification hubs* .</span><span class="sxs-lookup"><span data-stu-id="4d13f-188">The new page will provide a description of the *Notification Hubs* service.</span></span> <span data-ttu-id="4d13f-189">En bas à gauche de cette invite, sélectionnez le bouton **créer** pour créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="4d13f-189">At the bottom left of this prompt, select the **Create** button, to create an association with this service.</span></span>

    ![créer une instance notification hubs](images/AzureLabs-Lab8-07.png)

4.  <span data-ttu-id="4d13f-191">Une fois que vous avez cliqué sur ***créer***:</span><span class="sxs-lookup"><span data-stu-id="4d13f-191">Once you have clicked on ***Create***:</span></span>

    1.  <span data-ttu-id="4d13f-192">Insérez le nom de votre choix pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="4d13f-192">Insert your desired name for this service instance.</span></span>

    2.  <span data-ttu-id="4d13f-193">Fournissez un **espace de noms** que vous pourrez associer à cette application.</span><span class="sxs-lookup"><span data-stu-id="4d13f-193">Provide a **namespace** which you will be able to associate with this app.</span></span>

    3.  <span data-ttu-id="4d13f-194">Sélectionnez un **emplacement.**</span><span class="sxs-lookup"><span data-stu-id="4d13f-194">Select a **Location.**</span></span>

    4.  <span data-ttu-id="4d13f-195">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="4d13f-195">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="4d13f-196">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4d13f-196">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="4d13f-197">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun).</span><span class="sxs-lookup"><span data-stu-id="4d13f-197">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span>

        > <span data-ttu-id="4d13f-198">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, cliquez [sur le lien suivant pour gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="4d13f-198">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage a Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span> 

    5.  <span data-ttu-id="4d13f-199">Sélectionnez un **abonnement**approprié.</span><span class="sxs-lookup"><span data-stu-id="4d13f-199">Select an appropriate **Subscription**.</span></span>

    6.  <span data-ttu-id="4d13f-200">Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.</span><span class="sxs-lookup"><span data-stu-id="4d13f-200">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    7. <span data-ttu-id="4d13f-201">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-201">Select **Create**.</span></span>

        ![renseigner les détails du service](images/AzureLabs-Lab8-08.png)

5.  <span data-ttu-id="4d13f-203">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="4d13f-203">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

6.  <span data-ttu-id="4d13f-204">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="4d13f-204">A notification will appear in the portal once the Service instance is created.</span></span>

    ![notification](images/AzureLabs-Lab8-09.png)

7.  <span data-ttu-id="4d13f-206">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="4d13f-206">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="4d13f-207">Vous êtes dirigé vers votre nouvelle instance de service **notification Hub** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-207">You will be taken to your new **Notification Hub** service instance.</span></span>

    ![accéder à la ressource](images/AzureLabs-Lab8-10.png)
    
8.  <span data-ttu-id="4d13f-209">Dans la page vue d’ensemble, à mi-chemin de la page, cliquez sur **Windows (WNS).**</span><span class="sxs-lookup"><span data-stu-id="4d13f-209">From the overview page, halfway down the page, click **Windows (WNS).**</span></span> <span data-ttu-id="4d13f-210">Le panneau à droite change pour afficher deux champs de texte, qui nécessitent votre **SID de package** et votre **clé de sécurité**, à partir de l’application que vous avez configurée précédemment.</span><span class="sxs-lookup"><span data-stu-id="4d13f-210">The panel on the right will change to show two text fields, which require your **Package SID** and **Security Key**, from the app you set up previously.</span></span>

    ![service hubs nouvellement créé](images/AzureLabs-Lab8-11.png)

9. <span data-ttu-id="4d13f-212">Une fois que vous avez copié les détails dans les champs appropriés, cliquez sur **Enregistrer**pour recevoir une notification lorsque le hub de notification a été correctement mis à jour.</span><span class="sxs-lookup"><span data-stu-id="4d13f-212">Once you have copied the details into the correct fields, click **Save**, and you will receive a notification when the Notification Hub has been successfully updated.</span></span>

    ![copier les détails de sécurité](images/AzureLabs-Lab8-12.png)

## <a name="chapter-4---setup-azure-portal-create-table-service"></a><span data-ttu-id="4d13f-214">Chapitre 4-configurer le portail Azure : créer un service de table</span><span class="sxs-lookup"><span data-stu-id="4d13f-214">Chapter 4 - Setup Azure Portal: create Table Service</span></span>

<span data-ttu-id="4d13f-215">Après avoir créé votre instance de service Notification Hubs, revenez à votre portail Azure, où vous allez créer un service de tables Azure en créant une ressource de stockage.</span><span class="sxs-lookup"><span data-stu-id="4d13f-215">After creating your Notification Hubs Service instance, navigate back to your Azure Portal, where you will create an Azure Tables Service by creating a Storage Resource.</span></span>

1.  <span data-ttu-id="4d13f-216">Si vous n’êtes pas déjà connecté, connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4d13f-216">If not already signed in, log into the [Azure Portal](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="4d13f-217">Une fois connecté, cliquez sur **nouveau** dans l’angle supérieur gauche et recherchez compte de **stockage**, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-217">Once logged in, click on **New** in the top left corner, and search for **Storage account**, and click **Enter**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4d13f-218">Le mot ***nouveau*** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.</span><span class="sxs-lookup"><span data-stu-id="4d13f-218">The word ***New*** may have been replaced with **Create a resource**, in newer portals.</span></span>

3.  <span data-ttu-id="4d13f-219">Sélectionnez **compte de stockage-BLOB, fichier, table, file d’attente** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="4d13f-219">Select **Storage account - blob, file, table, queue** from the list.</span></span>

    ![Rechercher le compte de stockage](images/AzureLabs-Lab8-13.png)

4.  <span data-ttu-id="4d13f-221">La nouvelle page fournit une description du service de **compte de stockage** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-221">The new page will provide a description of the **Storage account** service.</span></span> <span data-ttu-id="4d13f-222">En bas à gauche de cette invite, sélectionnez le bouton **créer** pour créer une instance de ce service.</span><span class="sxs-lookup"><span data-stu-id="4d13f-222">At the bottom left of this prompt, select the **Create** button, to create an instance of this service.</span></span>

    ![créer une instance de stockage](images/AzureLabs-Lab8-14.png)

5.  <span data-ttu-id="4d13f-224">Une fois que vous avez cliqué sur **créer**, un panneau s’affiche :</span><span class="sxs-lookup"><span data-stu-id="4d13f-224">Once you have clicked on **Create**, a panel will appear:</span></span>

    1. <span data-ttu-id="4d13f-225">Insérez le **nom** souhaité pour cette instance de service (doit être tout en minuscules).</span><span class="sxs-lookup"><span data-stu-id="4d13f-225">Insert your desired **Name** for this service instance (must be all lowercase).</span></span>

    2. <span data-ttu-id="4d13f-226">Pour **modèle de déploiement**, cliquez sur **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-226">For **Deployment model**, click **Resource manager**.</span></span>

    3.  <span data-ttu-id="4d13f-227">Pour **type de compte**, à l’aide du menu déroulant, sélectionnez **stockage (v1 à usage général)** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-227">For **Account kind**, using the dropdown menu, select **Storage (general purpose v1)**.</span></span>

    4. <span data-ttu-id="4d13f-228">Sélectionnez un **emplacement**approprié.</span><span class="sxs-lookup"><span data-stu-id="4d13f-228">Select an appropriate **Location**.</span></span>
    
    5.  <span data-ttu-id="4d13f-229">Dans la liste déroulante **réplication** , sélectionnez **stockage avec accès géo-redondant (RA-GRS)** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-229">For the **Replication** dropdown menu, select **Read-access-geo-redundant storage (RA-GRS)**.</span></span>

    6.  <span data-ttu-id="4d13f-230">Pour les **performances**, cliquez sur **standard**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-230">For **Performance**, click **Standard**.</span></span>

    7.  <span data-ttu-id="4d13f-231">Dans la section **transfert sécurisé requis** , sélectionnez **désactivé**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-231">Within the **Secure transfer required** section, select **Disabled**.</span></span>

    8.  <span data-ttu-id="4d13f-232">Dans le menu déroulant **abonnement** , sélectionnez un abonnement approprié.</span><span class="sxs-lookup"><span data-stu-id="4d13f-232">From the **Subscription** dropdown menu, select an appropriate subscription.</span></span>

    9.  <span data-ttu-id="4d13f-233">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="4d13f-233">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="4d13f-234">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4d13f-234">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="4d13f-235">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun).</span><span class="sxs-lookup"><span data-stu-id="4d13f-235">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span>

        > <span data-ttu-id="4d13f-236">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, cliquez [sur le lien suivant pour gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="4d13f-236">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage a Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    10. <span data-ttu-id="4d13f-237">Laissez les **réseaux virtuels** **désactivés** s’il s’agit d’une option pour vous.</span><span class="sxs-lookup"><span data-stu-id="4d13f-237">Leave **Virtual networks** as **Disabled** if this is an option for you.</span></span>

    11. <span data-ttu-id="4d13f-238">Cliquez sur **Create (Créer)** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-238">Click **Create**.</span></span>

        ![renseigner les détails du stockage](images/AzureLabs-Lab8-15.png)

6.  <span data-ttu-id="4d13f-240">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="4d13f-240">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

7.  <span data-ttu-id="4d13f-241">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="4d13f-241">A notification will appear in the portal once the Service instance is created.</span></span> <span data-ttu-id="4d13f-242">Cliquez sur les notifications pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="4d13f-242">Click on the notifications to explore your new Service instance.</span></span>

    ![nouvelle notification de stockage](images/AzureLabs-Lab8-16.png)

8.  <span data-ttu-id="4d13f-244">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="4d13f-244">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="4d13f-245">Vous êtes dirigé vers la page vue d’ensemble de votre nouvelle instance de service de stockage.</span><span class="sxs-lookup"><span data-stu-id="4d13f-245">You will be taken to your new Storage Service instance overview page.</span></span>

    ![accéder à la ressource](images/AzureLabs-Lab8-17.PNG)

9. <span data-ttu-id="4d13f-247">Dans la page vue d’ensemble, sur le côté droit, cliquez sur **tables**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-247">From the overview page, to the right-hand side, click **Tables**.</span></span>
    
    ![](images/AzureLabs-Lab8-18.PNG)

10. <span data-ttu-id="4d13f-248">Le panneau à droite change pour afficher les informations sur le **service de table** , où vous devez ajouter une nouvelle table.</span><span class="sxs-lookup"><span data-stu-id="4d13f-248">The panel on the right will change to show the **Table service** information, wherein you need to add a new table.</span></span> <span data-ttu-id="4d13f-249">Pour ce faire, cliquez sur le bouton **+** **table** dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="4d13f-249">Do this by clicking the **+** **Table** button to the top-left corner.</span></span>

    ![Tables ouvertes](images/AzureLabs-Lab8-19.png)

11. <span data-ttu-id="4d13f-251">Une nouvelle page s’affiche, dans laquelle vous devez entrer un nom de **table**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-251">A new page will be shown, wherein you need to enter a **Table name**.</span></span> <span data-ttu-id="4d13f-252">Il s’agit du nom que vous allez utiliser pour faire référence aux données de votre application dans les chapitres ultérieurs.</span><span class="sxs-lookup"><span data-stu-id="4d13f-252">This is the name you will use to refer to the data in your application in later Chapters.</span></span> <span data-ttu-id="4d13f-253">Insérez un nom approprié, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-253">Insert an appropriate name and click **OK**.</span></span>

    ![créer une nouvelle table](images/AzureLabs-Lab8-20.png)    

12. <span data-ttu-id="4d13f-255">Une fois la nouvelle table créée, vous pouvez la voir dans la page **service de table** (en bas).</span><span class="sxs-lookup"><span data-stu-id="4d13f-255">Once the new table has been created, you will be able to see it within the **Table service** page (at the bottom).</span></span>

    ![nouvelle table créée](images/AzureLabs-Lab8-21.png)
    

## <a name="chapter-5---completing-the-azure-table-in-visual-studio"></a><span data-ttu-id="4d13f-257">Chapitre 5-remplissage du tableau Azure dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d13f-257">Chapter 5 - Completing the Azure Table in Visual Studio</span></span>

<span data-ttu-id="4d13f-258">Maintenant que votre compte de stockage de **service de table** a été configuré, il est temps d’y ajouter des données qui seront utilisées pour stocker et récupérer des informations.</span><span class="sxs-lookup"><span data-stu-id="4d13f-258">Now that your **Table service** storage account has been setup, it is time to add data to it, which will be used to store and retrieve information.</span></span> <span data-ttu-id="4d13f-259">La modification de vos tables peut être effectuée par le biais de **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-259">The editing of your Tables can be done through **Visual Studio**.</span></span>

1.  <span data-ttu-id="4d13f-260">Ouvrez **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-260">Open **Visual Studio**.</span></span>

2.  <span data-ttu-id="4d13f-261">Dans le menu, cliquez sur **afficher** > **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-261">From the menu, click **View** > **Cloud Explorer**.</span></span>

    ![ouvrir Cloud Explorer](images/AzureLabs-Lab8-22.png)

3.  <span data-ttu-id="4d13f-263">Le **Cloud Explorer** s’ouvre en tant qu’élément ancré (patienter, car le chargement peut prendre du temps).</span><span class="sxs-lookup"><span data-stu-id="4d13f-263">The **Cloud Explorer** will open as a docked item (be patient, as loading may take time).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4d13f-264">Si l’abonnement que vous avez utilisé pour créer vos *comptes de stockage* n’est pas visible, vérifiez que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4d13f-264">If the Subscription you used to create your *Storage Accounts* is not visible, ensure that you have:</span></span> 
    > - <span data-ttu-id="4d13f-265">Connectez-vous au même compte que celui que vous avez utilisé pour le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4d13f-265">Logged in to the same account as the one you used for the Azure Portal.</span></span>
    > - <span data-ttu-id="4d13f-266">Sélectionnez votre abonnement dans la page de gestion des comptes (vous devrez peut-être appliquer un filtre à partir de vos paramètres de compte) :</span><span class="sxs-lookup"><span data-stu-id="4d13f-266">Selected your Subscription from the Account Management Page (you may need to apply a filter from your account settings):</span></span>  
    >
    >   ![Rechercher un abonnement](images/AzureLabs-Lab8-22-5.png)

4.  <span data-ttu-id="4d13f-268">Vos services Cloud Azure s’affichent.</span><span class="sxs-lookup"><span data-stu-id="4d13f-268">Your Azure cloud services will be shown.</span></span> <span data-ttu-id="4d13f-269">Recherchez les **comptes de stockage** et cliquez sur la flèche à gauche de celle-ci pour développer vos comptes.</span><span class="sxs-lookup"><span data-stu-id="4d13f-269">Find **Storage Accounts** and click the arrow to the left of that to expand your accounts.</span></span>

    ![ouvrir les comptes de stockage](images/AzureLabs-Lab8-23.png)

5.  <span data-ttu-id="4d13f-271">Une fois développé, le **compte de stockage** que vous venez de créer doit être disponible.</span><span class="sxs-lookup"><span data-stu-id="4d13f-271">Once expanded, your newly created **Storage account** should be available.</span></span> <span data-ttu-id="4d13f-272">Cliquez sur la flèche à gauche de votre stockage, puis une fois celle-ci développée, recherchez des **tables** , puis cliquez sur la flèche en regard de celle-ci pour afficher la **table** que vous avez créée dans le dernier chapitre.</span><span class="sxs-lookup"><span data-stu-id="4d13f-272">Click the arrow to the left of your storage, and then once that is expanded, find **Tables** and click the arrow next to that, to reveal the **Table** you created in the last Chapter.</span></span> <span data-ttu-id="4d13f-273">Double-cliquez sur votre **table**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-273">Double click your **Table**.</span></span>

    ![ouvrir la table d’objets de scène](images/AzureLabs-Lab8-24.png)

6.  <span data-ttu-id="4d13f-275">Votre table s’ouvre au centre de votre fenêtre Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d13f-275">Your table will be opened in the center of your Visual Studio window.</span></span> <span data-ttu-id="4d13f-276">Cliquez sur l’icône de table avec le **+** (plus).</span><span class="sxs-lookup"><span data-stu-id="4d13f-276">Click the table icon with the **+** (plus) on it.</span></span>

    ![Ajouter une nouvelle table](images/AzureLabs-Lab8-25.png)

7.  <span data-ttu-id="4d13f-278">Une fenêtre s’affiche pour vous inviter à *Ajouter une entité*.</span><span class="sxs-lookup"><span data-stu-id="4d13f-278">A window will appear prompting for you to *Add Entity*.</span></span> <span data-ttu-id="4d13f-279">Vous allez créer trois entités au total, chacune avec plusieurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="4d13f-279">You will create three entities in total, each with several properties.</span></span> <span data-ttu-id="4d13f-280">Vous remarquerez que *PartitionKey* et *RowKey* sont déjà fournis, car ils sont utilisés par la table pour rechercher vos données.</span><span class="sxs-lookup"><span data-stu-id="4d13f-280">You will notice that *PartitionKey* and *RowKey* are already provided, as these are used by the table to find your data.</span></span> 

    ![clé de partition et de ligne](images/AzureLabs-Lab8-26.png)

8. <span data-ttu-id="4d13f-282">Mettez à jour la *valeur* de **PartitionKey** et **RowKey** comme suit (n’oubliez pas d’effectuer cette opération pour chaque propriété de ligne que vous ajoutez, même si vous incrémentez le RowKey à chaque fois) :</span><span class="sxs-lookup"><span data-stu-id="4d13f-282">Update the *Value* of the **PartitionKey** and **RowKey** as follows (remember to do this for each row property you add, though increment the RowKey each time):</span></span>

    ![Ajouter les valeurs correctes](images/AzureLabs-Lab8-26-5.png)

9.  <span data-ttu-id="4d13f-284">Cliquez sur **Ajouter une propriété** pour ajouter des lignes de données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4d13f-284">Click **Add property** to add extra rows of data.</span></span> <span data-ttu-id="4d13f-285">Faites correspondre votre première table vide à la table ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4d13f-285">Make your first empty table match the below table.</span></span>

10. <span data-ttu-id="4d13f-286">Cliquez sur **OK** lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="4d13f-286">Click **OK** when you are finished.</span></span>

    ![Cliquez sur OK lorsque vous avez terminé](images/AzureLabs-Lab8-27.png)

    > [!WARNING] 
    > <span data-ttu-id="4d13f-288">Vérifiez que vous avez modifié le **type** des entrées **X**, **Y**et **Z**, puis **doublez**-les.</span><span class="sxs-lookup"><span data-stu-id="4d13f-288">Ensure that you have changed the **Type** of the **X**, **Y**, and **Z**, entries to **Double**.</span></span> 

11. <span data-ttu-id="4d13f-289">Vous remarquerez que votre table contient désormais une ligne de données.</span><span class="sxs-lookup"><span data-stu-id="4d13f-289">You will notice your table now has a row of data.</span></span> <span data-ttu-id="4d13f-290">Cliquez à nouveau sur l’icône **+** (plus) pour ajouter une autre entité.</span><span class="sxs-lookup"><span data-stu-id="4d13f-290">Click the **+** (plus) icon again to add another entity.</span></span>

    ![première ligne](images/AzureLabs-Lab8-27-5.png)

12. <span data-ttu-id="4d13f-292">Créez une propriété supplémentaire, puis définissez les valeurs de la nouvelle entité pour qu’elles correspondent à celles indiquées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4d13f-292">Create an additional property, and then set the values of the new entity to match those shown below.</span></span>

    ![Ajouter un cube](images/AzureLabs-Lab8-28.png)

13. <span data-ttu-id="4d13f-294">Répétez la dernière étape pour ajouter une autre entité.</span><span class="sxs-lookup"><span data-stu-id="4d13f-294">Repeat the last step to add another entity.</span></span> <span data-ttu-id="4d13f-295">Définissez les valeurs de cette entité sur celles indiquées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4d13f-295">Set the values for this entity to those shown below.</span></span>

    ![Ajouter un cylindre](images/AzureLabs-Lab8-29.png)

14. <span data-ttu-id="4d13f-297">Votre table doit maintenant ressembler à celle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4d13f-297">Your table should now look like the one below.</span></span>

    ![table terminée](images/AzureLabs-Lab8-30.png)

15. <span data-ttu-id="4d13f-299">Vous avez terminé ce chapitre.</span><span class="sxs-lookup"><span data-stu-id="4d13f-299">You have completed this Chapter.</span></span> <span data-ttu-id="4d13f-300">Veillez à enregistrer.</span><span class="sxs-lookup"><span data-stu-id="4d13f-300">Make sure to save.</span></span>

## <a name="chapter-6---create-an-azure-function-app"></a><span data-ttu-id="4d13f-301">Chapitre 6-créer un Function App Azure</span><span class="sxs-lookup"><span data-stu-id="4d13f-301">Chapter 6 - Create an Azure Function App</span></span>

<span data-ttu-id="4d13f-302">Créez un Function App Azure, qui sera appelé par l’application de bureau pour mettre à jour le service de **table** et envoyer une notification par le biais du **Hub de notification**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-302">Create an Azure Function App, which will be called by the Desktop application to update the **Table** service and send a notification through the **Notification Hub**.</span></span>

<span data-ttu-id="4d13f-303">Tout d’abord, vous devez créer un fichier qui permettra à votre fonction Azure de charger les bibliothèques dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="4d13f-303">First, you need to create a file that will allow your Azure Function to load the libraries you need.</span></span>

1.  <span data-ttu-id="4d13f-304">Ouvrez **le bloc-notes** (appuyez sur la touche Windows et tapez Notepad).</span><span class="sxs-lookup"><span data-stu-id="4d13f-304">Open **Notepad** (press Windows Key and type notepad).</span></span>

    ![ouvrir le bloc-notes](images/AzureLabs-Lab8-31.png)

2.  <span data-ttu-id="4d13f-306">Avec le bloc-notes ouvert, insérez la structure JSON ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4d13f-306">With Notepad open, insert the JSON structure below into it.</span></span> <span data-ttu-id="4d13f-307">Une fois que vous avez effectué cette opération, enregistrez-la sur votre bureau en tant que **Project. JSON**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-307">Once you have done that, save it on your desktop as **project.json**.</span></span> <span data-ttu-id="4d13f-308">Il est important que l’attribution de noms soit correcte : Assurez-vous qu’elle n' **a pas d’extension de fichier. txt** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-308">It is important that the naming is correct: ensure it does **NOT have a .txt** file extension.</span></span> <span data-ttu-id="4d13f-309">Ce fichier définit les bibliothèques que votre fonction utilisera, si vous avez utilisé NuGet, vous serez familier.</span><span class="sxs-lookup"><span data-stu-id="4d13f-309">This file defines the libraries your function will use, if you have used NuGet it will look familiar.</span></span>

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

3.  <span data-ttu-id="4d13f-310">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4d13f-310">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

4.  <span data-ttu-id="4d13f-311">Une fois que vous êtes connecté, cliquez sur **nouveau** dans l’angle supérieur gauche et recherchez **Function App**, appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-311">Once you are logged in, click on **New** in the top left corner, and search for **Function App**, press **Enter**.</span></span>

    ![Rechercher une application de fonction](images/AzureLabs-Lab8-32.png)

    > [!NOTE] 
    > <span data-ttu-id="4d13f-313">Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.</span><span class="sxs-lookup"><span data-stu-id="4d13f-313">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

5.  <span data-ttu-id="4d13f-314">La nouvelle page fournit une description du service **Function App** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-314">The new page will provide a description of the **Function App** service.</span></span> <span data-ttu-id="4d13f-315">En bas à gauche de cette invite, sélectionnez le bouton **créer** pour créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="4d13f-315">At the bottom left of this prompt, select the **Create** button, to create an association with this service.</span></span>

    ![instance de l’application de fonction](images/AzureLabs-Lab8-33.png)

6.  <span data-ttu-id="4d13f-317">Une fois que vous avez cliqué sur **créer**, renseignez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4d13f-317">Once you have clicked on **Create**, fill in the following:</span></span>

    1. <span data-ttu-id="4d13f-318">Pour **nom**de l’application, insérez le nom de votre choix pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="4d13f-318">For **App name**, insert your desired name for this service instance.</span></span>

    2. <span data-ttu-id="4d13f-319">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-319">Select a **Subscription**.</span></span>

    3. <span data-ttu-id="4d13f-320">Sélectionnez le niveau tarifaire approprié, s’il s’agit de la première fois que vous créez un **Service Function App**, vous devez disposer d’un niveau gratuit.</span><span class="sxs-lookup"><span data-stu-id="4d13f-320">Select the pricing tier appropriate for you, if this is the first time creating a **Function App Service**, a free tier should be available to you.</span></span>

    4. <span data-ttu-id="4d13f-321">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="4d13f-321">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="4d13f-322">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4d13f-322">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="4d13f-323">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun).</span><span class="sxs-lookup"><span data-stu-id="4d13f-323">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span>

        > <span data-ttu-id="4d13f-324">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, cliquez [sur le lien suivant pour gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="4d13f-324">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage a Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5. <span data-ttu-id="4d13f-325">Pour **système d’exploitation**, cliquez sur Windows, car il s’agit de la plateforme prévue.</span><span class="sxs-lookup"><span data-stu-id="4d13f-325">For **OS**, click Windows, as that is the intended platform.</span></span>

    6. <span data-ttu-id="4d13f-326">Sélectionnez un **plan d’hébergement** (ce didacticiel utilise un **plan de consommation**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-326">Select a **Hosting Plan** (this tutorial is using a **Consumption Plan**.</span></span>

    7. <span data-ttu-id="4d13f-327">Sélectionnez un **emplacement** **(choisissez le même emplacement que celui du stockage que vous avez créé à l’étape précédente)**</span><span class="sxs-lookup"><span data-stu-id="4d13f-327">Select a **Location** **(choose the same location as the storage you have built in the previous step)**</span></span>

    8. <span data-ttu-id="4d13f-328">Pour la section **stockage** , **vous devez sélectionner le service de stockage que vous avez créé à l’étape précédente**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-328">For the **Storage** section, **you must select the Storage Service you created in the previous step**.</span></span>

    9. <span data-ttu-id="4d13f-329">Vous n’aurez pas besoin de *application Insights* dans cette **application. n'** hésitez donc pas à la conserver.</span><span class="sxs-lookup"><span data-stu-id="4d13f-329">You will not need *Application Insights* in this app, so feel free to leave it **Off**.</span></span>

    10. <span data-ttu-id="4d13f-330">Cliquez sur **Create (Créer)** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-330">Click **Create**.</span></span>

        ![créer une nouvelle instance](images/AzureLabs-Lab8-34.png)

7.  <span data-ttu-id="4d13f-332">Une fois que vous avez cliqué sur **créer** , vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="4d13f-332">Once you have clicked on **Create** you will have to wait for the service to be created, this might take a minute.</span></span>

8.  <span data-ttu-id="4d13f-333">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="4d13f-333">A notification will appear in the portal once the Service instance is created.</span></span>

    ![nouvelle notification](images/AzureLabs-Lab8-35.png)

9.  <span data-ttu-id="4d13f-335">Cliquez sur les notifications pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="4d13f-335">Click on the notifications to explore your new Service instance.</span></span>

10. <span data-ttu-id="4d13f-336">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="4d13f-336">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> 

    ![accéder à la ressource](images/AzureLabs-Lab8-36.png)

11. <span data-ttu-id="4d13f-338">Cliquez sur l’icône **+** (plus) en regard de *fonctions*pour en *créer une nouvelle*.</span><span class="sxs-lookup"><span data-stu-id="4d13f-338">Click the **+** (plus) icon next to *Functions*, to *Create new*.</span></span>

    ![Ajouter une nouvelle fonction](images/AzureLabs-Lab8-37.png)

12. <span data-ttu-id="4d13f-340">Dans le panneau central, la fenêtre de création de **fonction** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4d13f-340">Within the central panel, the **Function** creation window will appear.</span></span> <span data-ttu-id="4d13f-341">Ignorez les informations dans la moitié supérieure du panneau, puis cliquez sur **fonction personnalisée**, située près du bas (dans la zone bleue, comme ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="4d13f-341">Ignore the information in the upper half of the panel, and click **Custom function**, which is located near the bottom (in the blue area, as below).</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab8-38.png)

13. <span data-ttu-id="4d13f-343">La nouvelle page de la fenêtre affiche différents types de fonction.</span><span class="sxs-lookup"><span data-stu-id="4d13f-343">The new page within the window will show various function types.</span></span> <span data-ttu-id="4d13f-344">Faites défiler la liste pour afficher les types violets, puis cliquez sur élément **http put** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-344">Scroll down to view the purple types, and click **HTTP PUT** element.</span></span>

    ![lien http put](images/AzureLabs-Lab8-39.png)

    > [!IMPORTANT]
    > <span data-ttu-id="4d13f-346">Vous devrez peut-être faire défiler la page vers le bas (et cette image risque de ne pas être exactement la même, si les mises à jour du portail Azure ont eu lieu). Toutefois, vous recherchez un élément appelé *http put*.</span><span class="sxs-lookup"><span data-stu-id="4d13f-346">You may have to scroll further the down the page (and this image may not look exactly the same, if Azure Portal updates have taken place), however, you are looking for an element called *HTTP PUT*.</span></span>

14. <span data-ttu-id="4d13f-347">La fenêtre **http put** s’affiche, dans laquelle vous devez configurer la fonction (Voir l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="4d13f-347">The **HTTP PUT** window will appear, where you need to configure the function (see below for image).</span></span>

    1.  <span data-ttu-id="4d13f-348">Pour **langue,** dans le menu déroulant, sélectionnez C\#.</span><span class="sxs-lookup"><span data-stu-id="4d13f-348">For **Language,** using the dropdown menu, select C\#.</span></span>

    2.  <span data-ttu-id="4d13f-349">Pour **nom,** entrez un nom approprié.</span><span class="sxs-lookup"><span data-stu-id="4d13f-349">For **Name,** input an appropriate name.</span></span>

    3.  <span data-ttu-id="4d13f-350">Dans le menu déroulant **niveau d’authentification** , sélectionnez **fonction**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-350">In the **Authentication level** dropdown menu, select **Function**.</span></span>

    4.  <span data-ttu-id="4d13f-351">Pour la section nom de la **table** , vous devez utiliser le nom exact que vous avez utilisé pour créer le service de **table** précédemment (y compris la même casse).</span><span class="sxs-lookup"><span data-stu-id="4d13f-351">For the **Table name** section, you need to use the exact name you used to create your **Table** service previously (including the same letter case).</span></span>

    5.  <span data-ttu-id="4d13f-352">Dans la section **connexion au compte de stockage** , utilisez le menu déroulant, puis sélectionnez votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="4d13f-352">Within the **Storage account connection** section, use the dropdown menu, and select your storage account from there.</span></span> <span data-ttu-id="4d13f-353">Si ce n’est pas le cas, cliquez sur **le lien hypertexte** à côté du titre de la section pour afficher un autre panneau, où votre compte de stockage doit être listé.</span><span class="sxs-lookup"><span data-stu-id="4d13f-353">If it is not there, click the **New** hyperlink alongside the section title, to show another panel, where your storage account should be listed.</span></span>

        ![nouveau stockage](images/AzureLabs-Lab8-40.png)

15. <span data-ttu-id="4d13f-355">Cliquez sur **créer** . vous recevrez une notification indiquant que vos paramètres ont été correctement mis à jour.</span><span class="sxs-lookup"><span data-stu-id="4d13f-355">Click **Create** and you will receive a notification that your settings have been updated successfully.</span></span>

    ![créer une fonction](images/AzureLabs-Lab8-41.png)

16. <span data-ttu-id="4d13f-357">Après avoir cliqué sur **créer**, vous êtes redirigé vers l’éditeur de fonction.</span><span class="sxs-lookup"><span data-stu-id="4d13f-357">After clicking **Create**, you will be redirected to the function editor.</span></span>

    ![mettre à jour le code de fonction](images/AzureLabs-Lab8-42.png)

17. <span data-ttu-id="4d13f-359">Insérez le code suivant dans l’éditeur de fonction (en remplaçant le code dans la fonction) :</span><span class="sxs-lookup"><span data-stu-id="4d13f-359">Insert the following code into the function editor (replacing the code in the function):</span></span>

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
    > <span data-ttu-id="4d13f-360">À l’aide des bibliothèques incluses, la fonction reçoit le nom et l’emplacement de l’objet qui a été déplacé dans la scène C# Unity (sous la forme d’un objet, appelé **UnityGameObject**).</span><span class="sxs-lookup"><span data-stu-id="4d13f-360">Using the included libraries, the function receives the name and location of the object which was moved in the Unity scene (as a C# object, called **UnityGameObject**).</span></span> <span data-ttu-id="4d13f-361">Cet objet est ensuite utilisé pour mettre à jour les paramètres d’objet dans la table créée.</span><span class="sxs-lookup"><span data-stu-id="4d13f-361">This object is then used to update the object parameters within the created table.</span></span> <span data-ttu-id="4d13f-362">Après cela, la fonction effectue un appel à votre service de notification Hub créé, qui avertit toutes les applications abonnées.</span><span class="sxs-lookup"><span data-stu-id="4d13f-362">Following this, the function makes a call to your created Notification Hub service, which notifies all subscribed applications.</span></span>

18. <span data-ttu-id="4d13f-363">Avec le code en place, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-363">With the code in place, click **Save**.</span></span>

19. <span data-ttu-id="4d13f-364">Ensuite, cliquez sur l’icône de **\<** (flèche), sur le côté droit de la page.</span><span class="sxs-lookup"><span data-stu-id="4d13f-364">Next, click the **\<** (arrow) icon, on the right-hand side of the page.</span></span>

    ![ouvrir le panneau de chargement](images/AzureLabs-Lab8-43.png)

20. <span data-ttu-id="4d13f-366">Un panneau s’affiche à partir de la droite.</span><span class="sxs-lookup"><span data-stu-id="4d13f-366">A panel will slide in from the right.</span></span> <span data-ttu-id="4d13f-367">Dans ce panneau, cliquez sur **Télécharger**et un Explorateur de fichiers s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4d13f-367">In that panel, click **Upload**, and a File Browser will appear.</span></span>

21. <span data-ttu-id="4d13f-368">Accédez à, puis cliquez sur le fichier **Project. JSON** que vous avez créé précédemment dans le **bloc-notes** , puis cliquez sur le bouton **ouvrir** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-368">Navigate to, and click, the **project.json** file, which you created in **Notepad** previously, and then click the **Open** button.</span></span> <span data-ttu-id="4d13f-369">Ce fichier définit les bibliothèques que votre fonction utilisera.</span><span class="sxs-lookup"><span data-stu-id="4d13f-369">This file defines the libraries that your function will use.</span></span>

    ![Télécharger JSON](images/AzureLabs-Lab8-44.png)

22. <span data-ttu-id="4d13f-371">Une fois le fichier chargé, il s’affiche dans le volet de droite.</span><span class="sxs-lookup"><span data-stu-id="4d13f-371">When the file has uploaded, it will appear in the panel on the right.</span></span> <span data-ttu-id="4d13f-372">Cliquez dessus pour l’ouvrir dans l’éditeur de **fonctions** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-372">Clicking it will open it within the **Function** editor.</span></span> <span data-ttu-id="4d13f-373">Elle doit ressembler **exactement** à l’image suivante (sous l’étape 23).</span><span class="sxs-lookup"><span data-stu-id="4d13f-373">It must look **exactly** the same as the next image (below step 23).</span></span>

23. <span data-ttu-id="4d13f-374">Ensuite, dans le volet de gauche, sous **fonctions**, cliquez sur le lien **intégrer** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-374">Then, in the panel on the left, beneath **Functions**, click the **Integrate** link.</span></span>

    ![fonction d’intégration](images/AzureLabs-Lab8-45.png)

24. <span data-ttu-id="4d13f-376">Sur la page suivante, dans le coin supérieur droit, cliquez sur **éditeur avancé** (comme ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="4d13f-376">On the next page, in the top right corner, click **Advanced editor** (as below).</span></span>

    ![ouvrir l’éditeur avancé](images/AzureLabs-Lab8-46.png)

25. <span data-ttu-id="4d13f-378">Un fichier **Function. JSON** s’ouvre dans le panneau central, qui doit être remplacé par l’extrait de code suivant.</span><span class="sxs-lookup"><span data-stu-id="4d13f-378">A **function.json** file will be opened in the center panel, which needs to be replaced with the following code snippet.</span></span> <span data-ttu-id="4d13f-379">Cela définit la fonction que vous générez et les paramètres transmis à la fonction.</span><span class="sxs-lookup"><span data-stu-id="4d13f-379">This defines the function you are building and the parameters passed into the function.</span></span>

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

26. <span data-ttu-id="4d13f-380">Votre éditeur doit maintenant ressembler à l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="4d13f-380">Your editor should now look like the image below:</span></span>

    ![Retour à l’éditeur standard](images/AzureLabs-Lab8-47.png)

27. <span data-ttu-id="4d13f-382">Vous pouvez remarquer que les paramètres d’entrée que vous venez d’insérer ne correspondent pas à votre table et à vos détails de stockage et doivent donc être mis à jour avec vos informations.</span><span class="sxs-lookup"><span data-stu-id="4d13f-382">You may notice the input parameters that you have just inserted might not match your table and storage details and therefore will need to be updated with your information.</span></span> <span data-ttu-id="4d13f-383">N' **effectuez pas cette opération ici**, car elle est décrite ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4d13f-383">**Do not do this here**, as it is covered next.</span></span> <span data-ttu-id="4d13f-384">Cliquez simplement sur le lien **éditeur standard** , dans le coin supérieur droit de la page, pour revenir en arrière.</span><span class="sxs-lookup"><span data-stu-id="4d13f-384">Simply click the **Standard editor** link, in the top-right corner of the page, to go back.</span></span>

28. <span data-ttu-id="4d13f-385">De retour dans l' **éditeur standard**, cliquez sur **stockage table Azure (table)** , sous **entrées**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-385">Back in the **Standard editor**, click **Azure Table Storage (table)**, under **Inputs**.</span></span> 
    
    ![Entrées de table](images/AzureLabs-Lab8-47-5.png)

29. <span data-ttu-id="4d13f-387">Vérifiez que les informations suivantes correspondent à **vos** informations, car elles peuvent être différentes (une image est présente en dessous des étapes suivantes) :</span><span class="sxs-lookup"><span data-stu-id="4d13f-387">Ensure the following match to **your** information, as they may be different (there is an image below the following steps):</span></span>

    1.  <span data-ttu-id="4d13f-388">**Nom**de la table : nom de la table que vous avez créée dans votre service de stockage Azure, tables.</span><span class="sxs-lookup"><span data-stu-id="4d13f-388">**Table name**: the name of the table you created within your Azure Storage, Tables service.</span></span>

    2.  <span data-ttu-id="4d13f-389">**Connexion au compte de stockage :** cliquez sur **nouveau**, qui apparaît en regard du menu déroulant, et un panneau s’affiche à droite de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4d13f-389">**Storage account connection:** click **new**, which appears alongside the dropdown menu, and a panel will appear to the right of the window.</span></span>

        ![nouveau stockage](images/AzureLabs-Lab8-48.png)

        1.  <span data-ttu-id="4d13f-391">Sélectionnez votre **compte de stockage**, que vous avez créé précédemment pour héberger les **applications de fonction.**</span><span class="sxs-lookup"><span data-stu-id="4d13f-391">Select your **Storage Account**, which you created previously to host the **Function Apps.**</span></span>

        2. <span data-ttu-id="4d13f-392">Vous remarquerez que la valeur de la connexion au **compte de stockage** a été créée.</span><span class="sxs-lookup"><span data-stu-id="4d13f-392">You will notice that the **Storage Account** connection value has been created.</span></span>

        3. <span data-ttu-id="4d13f-393">Veillez à cliquer sur **Enregistrer** une fois que vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="4d13f-393">Make sure to press **Save** once you are done.</span></span>

    3.  <span data-ttu-id="4d13f-394">La page **entrées** doit maintenant correspondre aux informations ci-dessous, qui illustrent **vos** informations.</span><span class="sxs-lookup"><span data-stu-id="4d13f-394">The **Inputs** page should now match the below, showing **your** information.</span></span>

        ![entrées terminées](images/AzureLabs-Lab8-49.png)

30. <span data-ttu-id="4d13f-396">Ensuite, cliquez sur **Azure notification Hub (notification)** -sous **sorties**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-396">Next, click **Azure Notification Hub (notification)** - under **Outputs**.</span></span> <span data-ttu-id="4d13f-397">Assurez-vous que les éléments suivants sont mis en correspondance avec **vos** informations, car ils peuvent être différents (une image est présente en dessous des étapes suivantes) :</span><span class="sxs-lookup"><span data-stu-id="4d13f-397">Ensure the following are matched to **your** information, as they may be different (there is an image below the following steps):</span></span>

    1.  <span data-ttu-id="4d13f-398">**Nom du Hub de notification**: il s’agit du nom de l’instance de service de votre **Hub de notification** que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="4d13f-398">**Notification Hub Name**: this is the name of your **Notification Hub** service instance, which you created previously.</span></span>

    2.  <span data-ttu-id="4d13f-399">**Notification hubs la connexion**à l’espace de noms : cliquez sur **nouveau**, qui apparaît en regard du menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="4d13f-399">**Notification Hubs namespace connection**: click **new**, which appears alongside the dropdown menu.</span></span>

        ![vérifier les sorties](images/AzureLabs-Lab8-50.png)

    3. <span data-ttu-id="4d13f-401">La fenêtre contextuelle de **connexion** s’affiche (Voir l’image ci-dessous), où vous devez sélectionner l' **espace de noms** du **Hub de notification**que vous avez configuré précédemment.</span><span class="sxs-lookup"><span data-stu-id="4d13f-401">The **Connection** popup will appear (see image below), where you need to select the **Namespace** of the **Notification Hub**, which you set up previously.</span></span>

    4. <span data-ttu-id="4d13f-402">Sélectionnez le nom de votre **Hub de notification** dans le menu déroulant du milieu.</span><span class="sxs-lookup"><span data-stu-id="4d13f-402">Select your **Notification Hub** name from the middle dropdown menu.</span></span>

    5.  <span data-ttu-id="4d13f-403">Définissez le menu déroulant **stratégie** sur **DefaultFullSharedAccessSignature**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-403">Set the **Policy** dropdown menu to **DefaultFullSharedAccessSignature**.</span></span>

    6. <span data-ttu-id="4d13f-404">Cliquez sur le bouton **Sélectionner** pour revenir en arrière.</span><span class="sxs-lookup"><span data-stu-id="4d13f-404">Click the **Select** button to go back.</span></span>

        ![mise à jour de sortie](images/AzureLabs-Lab8-51.png)

31.  <span data-ttu-id="4d13f-406">La page **sorties** doit maintenant correspondre aux informations ci-dessous, mais avec **vos** informations à la place.</span><span class="sxs-lookup"><span data-stu-id="4d13f-406">The **Outputs** page should now match the below, but with **your** information instead.</span></span> <span data-ttu-id="4d13f-407">Veillez à cliquer sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-407">Make sure to press **Save**.</span></span>

> [!WARNING]
> <span data-ttu-id="4d13f-408">*Ne modifiez pas directement le nom du Hub de notification* (cette opération doit être effectuée à l’aide de la **éditeur avancé**, à condition que vous ayez suivi correctement les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="4d13f-408">*Do not edit the Notification Hub name directly* (this should all be done using the **Advanced Editor**, provided you followed the previous steps correctly.</span></span>

![sorties terminées](images/AzureLabs-Lab8-50.png)

32. <span data-ttu-id="4d13f-410">À ce stade, vous devez tester la fonction pour vous assurer qu’elle fonctionne.</span><span class="sxs-lookup"><span data-stu-id="4d13f-410">At this point, you should test the function, to ensure it is working.</span></span> <span data-ttu-id="4d13f-411">Pour cela, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d13f-411">To do this:</span></span> 

    1. <span data-ttu-id="4d13f-412">Accédez à la page de fonction une fois de plus :</span><span class="sxs-lookup"><span data-stu-id="4d13f-412">Navigate to the function page once more:</span></span>

        ![sorties terminées](images/AzureLabs-Lab8-50-1.png)

    2. <span data-ttu-id="4d13f-414">De retour dans la page de fonction, cliquez sur l’onglet **test** situé à l’extrême droite de la page pour ouvrir le panneau *test* :</span><span class="sxs-lookup"><span data-stu-id="4d13f-414">Back on the function page, click the **Test** tab on the far right side of the page, to open the *Test* blade:</span></span>

        ![sorties terminées](images/AzureLabs-Lab8-50-2.png)

    3. <span data-ttu-id="4d13f-416">Dans la zone de texte **requête Body** du panneau, collez le code ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="4d13f-416">Within the **Request body** textbox of the blade, paste the below code:</span></span>

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

    4. <span data-ttu-id="4d13f-417">Une fois le code de test en place, cliquez sur le bouton **exécuter** en bas à droite pour exécuter le test.</span><span class="sxs-lookup"><span data-stu-id="4d13f-417">With the test code in place, click the **Run** button at the bottom right, and the test will be run.</span></span> <span data-ttu-id="4d13f-418">Les journaux de sortie du test s’affichent dans la zone de la console, sous le code de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="4d13f-418">The output logs of the test will appear in the console area, below your function code.</span></span>

        ![sorties terminées](images/AzureLabs-Lab8-50-3.png)

    > [!WARNING]
    > <span data-ttu-id="4d13f-420">Si le test ci-dessus échoue, vous devez vérifier exactement que vous avez suivi les étapes ci-dessus, en particulier les paramètres dans le **panneau intégrer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-420">If the above test fails, you will need to double check that you have followed the above steps exactly, particularly the settings within the **integrate panel**.</span></span> 

## <a name="chapter-7---set-up-desktop-unity-project"></a><span data-ttu-id="4d13f-421">Chapitre 7-configurer un projet Unity de bureau</span><span class="sxs-lookup"><span data-stu-id="4d13f-421">Chapter 7 - Set up Desktop Unity Project</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d13f-422">L’application de bureau que vous créez maintenant ne fonctionne **pas** dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="4d13f-422">The Desktop application which you are now creating, **will not** work in the Unity Editor.</span></span> <span data-ttu-id="4d13f-423">Elle doit être exécutée en dehors de l’éditeur, après la génération de l’application, à l’aide de Visual Studio (ou de l’application déployée).</span><span class="sxs-lookup"><span data-stu-id="4d13f-423">It needs to be run outside of the Editor, following the Building of the application, using Visual Studio (or the deployed application).</span></span> 

<span data-ttu-id="4d13f-424">Voici une configuration standard pour le développement avec Unity et la réalité mixte, et en tant que tel, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="4d13f-424">The following is a typical set up for developing with Unity and mixed reality, and as such, is a good template for other projects.</span></span>

<span data-ttu-id="4d13f-425">Configurez et testez votre casque immersif en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="4d13f-425">Set up and test your mixed reality immersive headset.</span></span>

> [!NOTE] 
> <span data-ttu-id="4d13f-426">Vous n’aurez **pas** besoin de contrôleurs de mouvement pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="4d13f-426">You will **not** require Motion Controllers for this course.</span></span> <span data-ttu-id="4d13f-427">Si vous avez besoin de la prise en charge de la configuration du casque immersif, suivez ce [lien pour savoir comment configurer Windows Mixed Reality](https://support.microsoft.com/help/4043101/windows-10-set-up-windows-mixed-reality).</span><span class="sxs-lookup"><span data-stu-id="4d13f-427">If you need support setting up the immersive headset, please follow this [link on how to set up Windows Mixed Reality](https://support.microsoft.com/help/4043101/windows-10-set-up-windows-mixed-reality).</span></span>

1.  <span data-ttu-id="4d13f-428">Ouvrez **Unity** et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-428">Open **Unity** and click **New**.</span></span>

    ![nouveau projet Unity](images/AzureLabs-Lab8-52.png)

2.  <span data-ttu-id="4d13f-430">Vous devez fournir un nom de projet Unity, insérer **UnityDesktopNotifHub**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-430">You need to provide a Unity Project name, insert **UnityDesktopNotifHub**.</span></span> <span data-ttu-id="4d13f-431">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-431">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="4d13f-432">Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés).</span><span class="sxs-lookup"><span data-stu-id="4d13f-432">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="4d13f-433">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-433">Then, click **Create project**.</span></span>

    ![créer un projet](images/AzureLabs-Lab8-53.png)

3.  <span data-ttu-id="4d13f-435">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-435">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="4d13f-436">Accédez à **modifier** > **Préférences** puis, dans la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-436">Go to **Edit** > **Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="4d13f-437">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-437">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="4d13f-438">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-438">Close the **Preferences** window.</span></span>

    ![définir les outils VS externes](images/AzureLabs-Lab8-54.png)

4.  <span data-ttu-id="4d13f-440">Accédez ensuite à **fichier** > **paramètres de Build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le bouton changer de **plateforme** pour appliquer votre sélection.</span><span class="sxs-lookup"><span data-stu-id="4d13f-440">Next, go to **File** > **Build Settings** and select **Universal Windows Platform**, then click on the **Switch Platform** button to apply your selection.</span></span>

    ![changer de plateformes](images/AzureLabs-Lab8-55.png)

5.  <span data-ttu-id="4d13f-442">Tout en conservant les **paramètres de génération**de > de **fichiers** , assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="4d13f-442">While still in **File** > **Build Settings**, make sure that:</span></span>

    1.  <span data-ttu-id="4d13f-443">L' **appareil cible** est défini sur **n’importe quel appareil**</span><span class="sxs-lookup"><span data-stu-id="4d13f-443">**Target Device** is set to **Any Device**</span></span>

        > <span data-ttu-id="4d13f-444">Cette application sera destinée à votre bureau. doit donc être **n’importe quel appareil**</span><span class="sxs-lookup"><span data-stu-id="4d13f-444">This Application will be for your desktop, so must be **Any Device**</span></span>

    2.  <span data-ttu-id="4d13f-445">Le **type de build** est **D3D**</span><span class="sxs-lookup"><span data-stu-id="4d13f-445">**Build Type** is set to **D3D**</span></span>

    3.  <span data-ttu-id="4d13f-446">Le **SDK** est configuré sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="4d13f-446">**SDK** is set to **Latest installed**</span></span>

    4.  <span data-ttu-id="4d13f-447">**Version de Visual Studio** définie sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="4d13f-447">**Visual Studio Version** is set to **Latest installed**</span></span>

    5.  <span data-ttu-id="4d13f-448">La **génération et l’exécution** sont définies sur l' **ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="4d13f-448">**Build and Run** is set to **Local Machine**</span></span>

    6.  <span data-ttu-id="4d13f-449">Dans ce cas, il convient d’enregistrer la scène et de l’ajouter à la Build.</span><span class="sxs-lookup"><span data-stu-id="4d13f-449">While here, it is worth saving the scene, and adding it to the build.</span></span>

        1. <span data-ttu-id="4d13f-450">Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-450">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="4d13f-451">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4d13f-451">A save window will appear.</span></span>

            ![Ajouter des scènes ouvertes](images/AzureLabs-Lab8-56.png)

        2. <span data-ttu-id="4d13f-453">Créez un dossier pour cela, ainsi que toute nouvelle scène, puis sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez-le **scenes**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-453">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![nouveau dossier scenes](images/AzureLabs-Lab8-57.png)

        3. <span data-ttu-id="4d13f-455">Ouvrez le dossier **scenes** nouvellement créé, puis dans le champ **nom de fichier :** texte, tapez **NH\_Desktop\_Scene**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-455">Open your newly created **Scenes** folder, and then in the **File name:** text field, type **NH\_Desktop\_Scene**, then press **Save**.</span></span>

            ![nouveau NH_Desktop_Scene](images/AzureLabs-Lab8-58.png)

    7.  <span data-ttu-id="4d13f-457">Les paramètres restants, dans **paramètres de build**, doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="4d13f-457">The remaining settings, in **Build Settings**, should be left as default for now.</span></span>

6.  <span data-ttu-id="4d13f-458">Dans la même fenêtre, cliquez sur le bouton **paramètres du lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-458">In the same window click on the **Player Settings** button, this will open the related panel in the space where the **Inspector** is located.</span></span>

7.  <span data-ttu-id="4d13f-459">Dans ce volet, quelques paramètres doivent être vérifiés :</span><span class="sxs-lookup"><span data-stu-id="4d13f-459">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="4d13f-460">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="4d13f-460">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="4d13f-461">La **version du runtime de script** doit être **expérimentale (équivalent .net 4,6)**</span><span class="sxs-lookup"><span data-stu-id="4d13f-461">**Scripting Runtime Version** should be **Experimental (.NET 4.6 Equivalent)**</span></span>

        2. <span data-ttu-id="4d13f-462">Le **backend de script** doit être **.net**</span><span class="sxs-lookup"><span data-stu-id="4d13f-462">**Scripting Backend** should be **.NET**</span></span>

        3. <span data-ttu-id="4d13f-463">Le **niveau de compatibilité** de l’API doit être **.net 4,6**</span><span class="sxs-lookup"><span data-stu-id="4d13f-463">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![version .net 4,6](images/AzureLabs-Lab8-59.png)

    2.  <span data-ttu-id="4d13f-465">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher :</span><span class="sxs-lookup"><span data-stu-id="4d13f-465">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="4d13f-466">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="4d13f-466">**InternetClient**</span></span>

            ![client Internet Tick](images/AzureLabs-Lab8-60.png)

8.  <span data-ttu-id="4d13f-468">De retour dans les **paramètres de build** *unity C\# les projets* ne sont plus grisés. Cochez la case en regard de cette option.</span><span class="sxs-lookup"><span data-stu-id="4d13f-468">Back in **Build Settings** *Unity C\# Projects* is no longer greyed out; tick the checkbox next to this.</span></span>

9.  <span data-ttu-id="4d13f-469">Fermez la fenêtre **paramètres de build** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-469">Close the **Build Settings** window.</span></span>

10. <span data-ttu-id="4d13f-470">Enregistrez votre scène et votre **fichier** projet > **enregistrer la séquence/le fichier** > enregistrer le **projet**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-470">Save your Scene and Project **File** > **Save Scene / File** > **Save Project**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4d13f-471">Si vous souhaitez ignorer le composant *unité* de configuration pour ce projet (application de bureau) et continuer directement dans le code, n’hésitez pas à [Télécharger ce fichier. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20308%20-%20Cross-device%20notifications/Azure-MR-308-Desktop.unitypackage), à l’importer dans votre projet en tant que [**package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis à continuer à partir du [chapitre 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).</span><span class="sxs-lookup"><span data-stu-id="4d13f-471">If you wish to skip the *Unity Set up* component for this project (Desktop App), and continue straight into code, feel free to [download this .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20308%20-%20Cross-device%20notifications/Azure-MR-308-Desktop.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).</span></span>  <span data-ttu-id="4d13f-472">Vous devrez toujours ajouter les composants script.</span><span class="sxs-lookup"><span data-stu-id="4d13f-472">You will still need to add the script components.</span></span>

## <a name="chapter-8---importing-the-dlls-in-unity"></a><span data-ttu-id="4d13f-473">Chapitre 8-importation des dll dans Unity</span><span class="sxs-lookup"><span data-stu-id="4d13f-473">Chapter 8 - Importing the DLLs in Unity</span></span>

<span data-ttu-id="4d13f-474">Vous allez utiliser le stockage Azure pour Unity (qui utilise lui-même le kit de développement logiciel (SDK) .net pour Azure).</span><span class="sxs-lookup"><span data-stu-id="4d13f-474">You will be using Azure Storage for Unity (which itself leverages the .Net SDK for Azure).</span></span> <span data-ttu-id="4d13f-475">Pour plus d’informations, consultez ce [lien sur le stockage Azure pour Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).</span><span class="sxs-lookup"><span data-stu-id="4d13f-475">For more information follow this [link about Azure Storage for Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).</span></span>

<span data-ttu-id="4d13f-476">Il existe actuellement un problème connu dans Unity qui nécessite que les plug-ins soient reconfigurés après l’importation.</span><span class="sxs-lookup"><span data-stu-id="4d13f-476">There is currently a known issue in Unity which requires plugins to be reconfigured after import.</span></span> <span data-ttu-id="4d13f-477">Ces étapes (4-7 dans cette section) ne sont plus nécessaires une fois que le bogue a été résolu.</span><span class="sxs-lookup"><span data-stu-id="4d13f-477">These steps (4 - 7 in this section) will no longer be required after the bug has been resolved.</span></span>

<span data-ttu-id="4d13f-478">Pour importer le kit de développement logiciel (SDK) dans votre propre projet, assurez-vous d’avoir téléchargé la dernière version de [**pour Unity**](https://aka.ms/azstorage-unitysdk) à partir de github.</span><span class="sxs-lookup"><span data-stu-id="4d13f-478">To import the SDK into your own project, make sure you have downloaded the latest [**.unitypackage**](https://aka.ms/azstorage-unitysdk) from GitHub.</span></span> <span data-ttu-id="4d13f-479">Ensuite, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d13f-479">Then, do the following:</span></span>

1.  <span data-ttu-id="4d13f-480">Ajoutez le fichier **. pour Unity** à Unity à l’aide de l’option de menu **ressources \> importer le package \> package personnalisé** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-480">Add the **.unitypackage** to Unity by using the **Assets \> Import Package \> Custom Package** menu option.</span></span>

2.  <span data-ttu-id="4d13f-481">Dans la zone **importer le package Unity** qui s’affiche, vous pouvez sélectionner tout ce qui se trouve sous \* \**plugin* \> \* Storage \* \* \*.</span><span class="sxs-lookup"><span data-stu-id="4d13f-481">In the **Import Unity Package** box that pops up, you can select everything under \*\**Plugin* \> \*Storage\*\*\*.</span></span>  <span data-ttu-id="4d13f-482">Décochez tout le reste, car il n’est pas nécessaire pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="4d13f-482">Uncheck everything else, as it is not needed for this course.</span></span>

    ![importer dans le package](images/AzureLabs-Lab8-61.png)

3.  <span data-ttu-id="4d13f-484">Cliquez sur le bouton ***Importer*** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="4d13f-484">Click the ***Import*** button to add the items to your project.</span></span>

4.  <span data-ttu-id="4d13f-485">Accédez au dossier **stockage** sous **plug-ins** dans la vue projet et sélectionnez les plug-ins suivants *uniquement*:</span><span class="sxs-lookup"><span data-stu-id="4d13f-485">Go to the **Storage** folder under **Plugins** in the Project view and select the following plugins *only*:</span></span>

    -   <span data-ttu-id="4d13f-486">Microsoft. Data. Edm</span><span class="sxs-lookup"><span data-stu-id="4d13f-486">Microsoft.Data.Edm</span></span>
    -   <span data-ttu-id="4d13f-487">Microsoft. Data. OData</span><span class="sxs-lookup"><span data-stu-id="4d13f-487">Microsoft.Data.OData</span></span>
    -   <span data-ttu-id="4d13f-488">Microsoft. WindowsAzure. Storage</span><span class="sxs-lookup"><span data-stu-id="4d13f-488">Microsoft.WindowsAzure.Storage</span></span>
    -   <span data-ttu-id="4d13f-489">Newtonsoft. JSON</span><span class="sxs-lookup"><span data-stu-id="4d13f-489">Newtonsoft.Json</span></span>
    -   <span data-ttu-id="4d13f-490">System. spatial</span><span class="sxs-lookup"><span data-stu-id="4d13f-490">System.Spatial</span></span>

![décocher une plateforme](images/AzureLabs-Lab8-62.png)

5.  <span data-ttu-id="4d13f-492">Une fois *ces plug-ins spécifiques* sélectionnés, **décochez** **toutes les plateformes** et **décochez** **WSAPlayer** , puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-492">With *these specific plugins* selected, **uncheck** **Any Platform** and **uncheck** **WSAPlayer** then click **Apply**.</span></span>

    ![appliquer des dll de plateforme](images/AzureLabs-Lab8-63.png)

    > [!NOTE] 
    > <span data-ttu-id="4d13f-494">Nous marqueons ces plug-ins particuliers à utiliser uniquement dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="4d13f-494">We are marking these particular plugins to only be used in the Unity Editor.</span></span> <span data-ttu-id="4d13f-495">Cela est dû au fait qu’il existe différentes versions des mêmes plug-ins dans le dossier WSA qui seront utilisées après l’exportation du projet à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="4d13f-495">This is because there are different versions of the same plugins in the WSA folder that will be used after the project is exported from Unity.</span></span>

6.  <span data-ttu-id="4d13f-496">Dans le dossier de plug-in de **stockage** , sélectionnez uniquement :</span><span class="sxs-lookup"><span data-stu-id="4d13f-496">In the **Storage** plugin folder, select only:</span></span>

    -   <span data-ttu-id="4d13f-497">Microsoft. Data. services. client</span><span class="sxs-lookup"><span data-stu-id="4d13f-497">Microsoft.Data.Services.Client</span></span>

        ![définir ne pas traiter pour les dll](images/AzureLabs-Lab8-64.png)

7.  <span data-ttu-id="4d13f-499">Cochez la case **ne pas traiter** sous **paramètres de plateforme** , puis cliquez sur ***appliquer***.</span><span class="sxs-lookup"><span data-stu-id="4d13f-499">Check the **Don't Process** box under **Platform Settings** and click ***Apply***.</span></span>

    ![ne pas appliquer de traitement](images/AzureLabs-Lab8-65.png)

    > [!NOTE] 
    > <span data-ttu-id="4d13f-501">Nous marquant ce plug-in « ne pas traiter », car l’assembly Unity Patcher a des difficultés à traiter ce plug-in.</span><span class="sxs-lookup"><span data-stu-id="4d13f-501">We are marking this plugin "Don't process", because the Unity assembly patcher has difficulty processing this plugin.</span></span> <span data-ttu-id="4d13f-502">Le plug-in fonctionne toujours même s’il n’est pas traité.</span><span class="sxs-lookup"><span data-stu-id="4d13f-502">The plugin will still work even though it is not processed.</span></span>

## <a name="chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project"></a><span data-ttu-id="4d13f-503">Chapitre 9-créer la classe TableToScene dans le projet Unity de bureau</span><span class="sxs-lookup"><span data-stu-id="4d13f-503">Chapter 9 - Create the TableToScene class in the Desktop Unity project</span></span>

<span data-ttu-id="4d13f-504">Vous devez maintenant créer les scripts contenant le code pour exécuter cette application.</span><span class="sxs-lookup"><span data-stu-id="4d13f-504">You now need to create the scripts containing the code to run this application.</span></span>

<span data-ttu-id="4d13f-505">Le premier script que vous devez créer est **TableToScene**, qui est responsable des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d13f-505">The first script you need to create is **TableToScene**, which is responsible for:</span></span>

-   <span data-ttu-id="4d13f-506">Lecture des entités dans la table Azure.</span><span class="sxs-lookup"><span data-stu-id="4d13f-506">Reading entities within the Azure Table.</span></span>
-   <span data-ttu-id="4d13f-507">À l’aide des données de la table, déterminez les objets à générer et leur position.</span><span class="sxs-lookup"><span data-stu-id="4d13f-507">Using the Table data, determine which objects to spawn, and in which position.</span></span>

<span data-ttu-id="4d13f-508">Le deuxième script que vous devez créer est **CloudScene**, qui est responsable des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d13f-508">The second script you need to create is **CloudScene**, which is responsible for:</span></span>

-   <span data-ttu-id="4d13f-509">Inscription de l’événement de clic gauche pour permettre à l’utilisateur de faire glisser des objets autour de la scène.</span><span class="sxs-lookup"><span data-stu-id="4d13f-509">Registering the left-click event, to allow the user to drag objects around the scene.</span></span>
-   <span data-ttu-id="4d13f-510">Sérialisation des données d’objet à partir de cette scène Unity et envoi de celles-ci au Function App Azure.</span><span class="sxs-lookup"><span data-stu-id="4d13f-510">Serializing the object data from this Unity scene, and sending it to the Azure Function App.</span></span>

<span data-ttu-id="4d13f-511">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="4d13f-511">To create this class:</span></span>

1.  <span data-ttu-id="4d13f-512">Cliquez avec le bouton droit sur le dossier **Asset** situé dans le panneau projet, puis **créez** > **dossier**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-512">Right-click in the **Asset** Folder located in the Project Panel, **Create** > **Folder**.</span></span> <span data-ttu-id="4d13f-513">Nommez le dossier **scripts**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-513">Name the folder **Scripts**.</span></span>

    ![créer un dossier de scripts](images/AzureLabs-Lab8-66.png)

    ![créer un dossier de scripts 2](images/AzureLabs-Lab8-67.png)

2.  <span data-ttu-id="4d13f-516">Double-cliquez sur le dossier que vous venez de créer pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="4d13f-516">Double click on the folder just created, to open it.</span></span>

3.  <span data-ttu-id="4d13f-517">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** >  **C# script**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-517">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="4d13f-518">Nommez le script **TableToScene**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-518">Name the script **TableToScene**.</span></span>

    <span data-ttu-id="4d13f-519">![nouveau](images/AzureLabs-Lab8-68.png)
    de script c# ![renommer le TableToScene](images/AzureLabs-Lab8-69.png)</span><span class="sxs-lookup"><span data-stu-id="4d13f-519">![new c# script](images/AzureLabs-Lab8-68.png)
![TableToScene rename](images/AzureLabs-Lab8-69.png)</span></span>

4.  <span data-ttu-id="4d13f-520">Double-cliquez sur le script pour l’ouvrir dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4d13f-520">Double-click on the script to open it in Visual Studio 2017.</span></span>

5.  <span data-ttu-id="4d13f-521">Ajoutez les espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="4d13f-521">Add the following namespaces:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    using UnityEngine;
    ```

6.  <span data-ttu-id="4d13f-522">Dans la classe, insérez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d13f-522">Within the class, insert the following variables:</span></span>

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
    > <span data-ttu-id="4d13f-523">Remplacez la valeur **AccountName** par le nom de votre service de stockage Azure et la valeur **accountKey** par la valeur de clé trouvée dans le service de stockage Azure, dans le portail Azure (Voir l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="4d13f-523">Substitute the **accountName** value with your Azure Storage Service name and **accountKey** value with the key value found in the Azure Storage Service, in the Azure Portal (See Image below).</span></span> 
    >
    > ![extraire la clé de compte](images/AzureLabs-Lab8-70.png)

7.  <span data-ttu-id="4d13f-525">Ajoutez maintenant les méthodes **Start ()** et **éveillé ()** pour initialiser la classe.</span><span class="sxs-lookup"><span data-stu-id="4d13f-525">Now add the **Start()** and **Awake()** methods to initialize the class.</span></span>

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

8.  <span data-ttu-id="4d13f-526">Dans la classe **TableToScene** , ajoutez la méthode qui permet de récupérer les valeurs de la table Azure et de les utiliser pour générer les primitives appropriées dans la scène.</span><span class="sxs-lookup"><span data-stu-id="4d13f-526">Within the **TableToScene** class, add the method that will retrieve the values from the Azure Table and use them to spawn the appropriate primitives in the scene.</span></span>

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

9.  <span data-ttu-id="4d13f-527">En dehors de la classe **TableToScene** , vous devez définir la classe utilisée par l’application pour sérialiser et désérialiser les **entités de table**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-527">Outside the **TableToScene** class, you need to define the class used by the application to serialize and deserialize the **Table Entities**.</span></span>

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

10. <span data-ttu-id="4d13f-528">Veillez à **Enregistrer** avant de revenir à l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="4d13f-528">Make sure you **Save** before going back to the Unity Editor.</span></span>

11. <span data-ttu-id="4d13f-529">Cliquez sur la **caméra principale** dans le volet de la **hiérarchie** , afin que ses propriétés s’affichent dans l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-529">Click the **Main Camera** from the **Hierarchy** panel, so that its properties appear in the **Inspector**.</span></span>

12. <span data-ttu-id="4d13f-530">Le dossier **scripts** étant ouvert, sélectionnez le fichier de script **TableToScene** et faites-le glisser sur l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-530">With the **Scripts** folder open, select the script **TableToScene file** and drag it onto the **Main Camera**.</span></span> <span data-ttu-id="4d13f-531">Le résultat doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d13f-531">The result should be as below:</span></span>

    ![Ajouter un script à l’appareil photo principal](images/AzureLabs-Lab8-71.png)

## <a name="chapter-10---create-the-cloudscene-class-in-the-desktop-unity-project"></a><span data-ttu-id="4d13f-533">Chapitre 10-créer la classe CloudScene dans le projet Unity de bureau</span><span class="sxs-lookup"><span data-stu-id="4d13f-533">Chapter 10 - Create the CloudScene class in the Desktop Unity Project</span></span>

<span data-ttu-id="4d13f-534">Le deuxième script que vous devez créer est **CloudScene**, qui est responsable des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d13f-534">The second script you need to create is **CloudScene**, which is responsible for:</span></span>

-   <span data-ttu-id="4d13f-535">Inscription de l’événement de clic gauche pour permettre à l’utilisateur de faire glisser des objets autour de la scène.</span><span class="sxs-lookup"><span data-stu-id="4d13f-535">Registering the left-click event, to allow the user to drag objects around the scene.</span></span>

-   <span data-ttu-id="4d13f-536">Sérialisation des données d’objet à partir de cette scène Unity et envoi de celles-ci au Function App Azure.</span><span class="sxs-lookup"><span data-stu-id="4d13f-536">Serializing the object data from this Unity scene, and sending it to the Azure Function App.</span></span>

<span data-ttu-id="4d13f-537">Pour créer le deuxième script :</span><span class="sxs-lookup"><span data-stu-id="4d13f-537">To create the second script:</span></span>

1.  <span data-ttu-id="4d13f-538">Cliquez avec le bouton droit dans le dossier **scripts** , cliquez sur **créer**, **C\# script**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-538">Right-click inside the **Scripts** folder, click **Create**, **C\# Script**.</span></span> <span data-ttu-id="4d13f-539">Nommez le script **CloudScene**</span><span class="sxs-lookup"><span data-stu-id="4d13f-539">Name the script **CloudScene**</span></span>
    
    <span data-ttu-id="4d13f-540">![nouveau](images/AzureLabs-Lab8-72.png)
    de script c# ![renommer CloudScene](images/AzureLabs-Lab8-73.png)</span><span class="sxs-lookup"><span data-stu-id="4d13f-540">![new c# script](images/AzureLabs-Lab8-72.png)
![rename CloudScene](images/AzureLabs-Lab8-73.png)</span></span>

2.  <span data-ttu-id="4d13f-541">Ajoutez les espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="4d13f-541">Add the following namespaces:</span></span>

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.Text;
    using System.Threading.Tasks;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

3.  <span data-ttu-id="4d13f-542">Insérez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d13f-542">Insert the following variables:</span></span>

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

4.  <span data-ttu-id="4d13f-543">Remplacez la valeur **azureFunctionEndpoint** par votre URL Azure Function App trouvée dans le Service Azure Function App, dans le portail Azure, comme indiqué dans l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="4d13f-543">Substitute the **azureFunctionEndpoint** value with your Azure Function App URL found in the Azure Function App Service, in the Azure Portal, as shown in the image below:</span></span>

    ![Obtient l’URL de la fonction](images/AzureLabs-Lab8-74.png)

5.  <span data-ttu-id="4d13f-545">Ajoutez maintenant les méthodes **Start ()** et **éveillé ()** pour initialiser la classe.</span><span class="sxs-lookup"><span data-stu-id="4d13f-545">Now add the **Start()** and **Awake()** methods to initialize the class.</span></span>

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

6.  <span data-ttu-id="4d13f-546">Dans la méthode **Update ()** , ajoutez le code suivant qui détecte l’entrée de la souris et glissent, ce qui déplace à son tour GameObjects dans la scène.</span><span class="sxs-lookup"><span data-stu-id="4d13f-546">Within the **Update()** method, add the following code that will detect the mouse input and drag, which will in turn move GameObjects in the scene.</span></span> <span data-ttu-id="4d13f-547">Si l’utilisateur a glissé et supprimé un objet, il passe le nom et les coordonnées de l’objet à la méthode **UpdateCloudScene ()** , qui appelle le service Azure Function App, qui met à jour la table Azure et déclenche la notification.</span><span class="sxs-lookup"><span data-stu-id="4d13f-547">If the user has dragged and dropped an object, it will pass the name and coordinates of the object to the method **UpdateCloudScene()**, which will call the Azure Function App service, which will update the Azure table and trigger the notification.</span></span>

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

7.  <span data-ttu-id="4d13f-548">Ajoutez maintenant la méthode **UpdateCloudScene ()** , comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="4d13f-548">Now add the **UpdateCloudScene()** method, as below:</span></span>

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

8.  <span data-ttu-id="4d13f-549">Enregistrer le code et revenir à Unity</span><span class="sxs-lookup"><span data-stu-id="4d13f-549">Save the code and return to Unity</span></span>

9.  <span data-ttu-id="4d13f-550">Faites glisser le script **CloudScene** sur l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-550">Drag the **CloudScene** script onto the **Main Camera**.</span></span> 

    1. <span data-ttu-id="4d13f-551">Cliquez sur la **caméra principale** dans le volet de la **hiérarchie** , afin que ses propriétés s’affichent dans l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-551">Click the **Main Camera** from the **Hierarchy** panel, so that its properties appear in the **Inspector**.</span></span> 

    2. <span data-ttu-id="4d13f-552">Le dossier **scripts** étant ouvert, sélectionnez le script **CloudScene** et faites-le glisser sur l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-552">With the **Scripts** folder open, select the **CloudScene** script and drag it onto the **Main Camera**.</span></span> <span data-ttu-id="4d13f-553">Le résultat doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d13f-553">The result should be as below:</span></span>

        > ![faire glisser le script Cloud sur l’appareil photo principal](images/AzureLabs-Lab8-75.png)

## <a name="chapter-11---build-the-desktop-project-to-uwp"></a><span data-ttu-id="4d13f-555">Chapitre 11-créer le projet de bureau dans UWP</span><span class="sxs-lookup"><span data-stu-id="4d13f-555">Chapter 11 - Build the Desktop Project to UWP</span></span>

<span data-ttu-id="4d13f-556">Tout ce qui est nécessaire pour la section Unity de ce projet est maintenant terminé.</span><span class="sxs-lookup"><span data-stu-id="4d13f-556">Everything needed for the Unity section of this project has now been completed.</span></span>

1.  <span data-ttu-id="4d13f-557">Accédez à **paramètres de build** (**fichier** > **paramètres de build**).</span><span class="sxs-lookup"><span data-stu-id="4d13f-557">Navigate to **Build Settings** (**File** > **Build Settings**).</span></span>

2.  <span data-ttu-id="4d13f-558">Dans la fenêtre **paramètres de build** , cliquez sur **générer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-558">From the **Build Settings** window, click **Build**.</span></span>

    ![générer le projet](images/AzureLabs-Lab8-76.png)

3.  <span data-ttu-id="4d13f-560">Une fenêtre de l' **Explorateur de fichiers** s’affiche et vous invite à entrer un emplacement à générer.</span><span class="sxs-lookup"><span data-stu-id="4d13f-560">A **File Explorer** window will popup, prompting you for a location to Build.</span></span> <span data-ttu-id="4d13f-561">Créez un nouveau dossier (en cliquant sur **nouveau dossier** dans l’angle supérieur gauche), puis nommez-le **Builds**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-561">Create a new folder (by clicking **New Folder** in the top-left corner), and name it **BUILDS**.</span></span>

    ![nouveau dossier pour la Build](images/AzureLabs-Lab8-77.png)

    1.  <span data-ttu-id="4d13f-563">Ouvrez le nouveau dossier **Builds** , puis créez un autre dossier (à l’aide d’un **nouveau dossier** ) et nommez-le **NH\_Desktop\_application**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-563">Open the new **BUILDS** folder, and create another folder (using **New Folder** once more), and name it **NH\_Desktop\_App**.</span></span>

        ![nom du dossier NH_Desktop_App](images/AzureLabs-Lab8-78.png)

    2.  <span data-ttu-id="4d13f-565">Avec l' **application de\_de bureau NH\_** sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="4d13f-565">With the **NH\_Desktop\_App** selected.</span></span> <span data-ttu-id="4d13f-566">Cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-566">click **Select Folder**.</span></span> <span data-ttu-id="4d13f-567">La génération du projet prendra quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4d13f-567">The project will take a minute or so to build.</span></span>

4.  <span data-ttu-id="4d13f-568">Après la génération, l' **Explorateur de fichiers** s’affiche et vous indique l’emplacement de votre nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="4d13f-568">Following build, **File Explorer** will appear showing you the location of your new project.</span></span> <span data-ttu-id="4d13f-569">Toutefois, il n’est pas nécessaire de l’ouvrir, car vous devez d’abord créer l’autre projet Unity, dans les chapitres suivants.</span><span class="sxs-lookup"><span data-stu-id="4d13f-569">No need to open it, though, as you need to create the other Unity project first, in the next few Chapters.</span></span>


## <a name="chapter-12---set-up-mixed-reality-unity-project"></a><span data-ttu-id="4d13f-570">Chapitre 12-configurer un projet Unity de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="4d13f-570">Chapter 12 - Set up Mixed Reality Unity Project</span></span>

<span data-ttu-id="4d13f-571">Ce qui suit est une configuration classique pour le développement avec la réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="4d13f-571">The following is a typical set up for developing with the mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="4d13f-572">Ouvrez **Unity** et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-572">Open **Unity** and click **New**.</span></span>

    ![nouveau projet Unity](images/AzureLabs-Lab8-79.png)

2.  <span data-ttu-id="4d13f-574">Vous devez maintenant fournir un nom de projet Unity, insérer **UnityMRNotifHub**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-574">You will now need to provide a Unity Project name, insert **UnityMRNotifHub**.</span></span> <span data-ttu-id="4d13f-575">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-575">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="4d13f-576">Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés).</span><span class="sxs-lookup"><span data-stu-id="4d13f-576">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="4d13f-577">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-577">Then, click **Create project**.</span></span>

    ![nom UnityMRNotifHub](images/AzureLabs-Lab8-80.png)

3.  <span data-ttu-id="4d13f-579">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-579">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="4d13f-580">Accédez à **modifier** > **Préférences** puis, dans la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-580">Go to **Edit** > **Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="4d13f-581">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-581">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="4d13f-582">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-582">Close the **Preferences** window.</span></span>

    ![définir l’éditeur externe sur VS](images/AzureLabs-Lab8-81.png)

4.  <span data-ttu-id="4d13f-584">Accédez ensuite à **fichier** > **paramètres de build** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton changer de **plateforme** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-584">Next, go to **File** > **Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

    ![basculer les plateformes sur UWP](images/AzureLabs-Lab8-82.png)

5.  <span data-ttu-id="4d13f-586">Accédez à **fichier** > **paramètres de build** et assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="4d13f-586">Go to **File** > **Build Settings** and make sure that:</span></span>

    1.  <span data-ttu-id="4d13f-587">L' **appareil cible** est défini sur **n’importe quel appareil**</span><span class="sxs-lookup"><span data-stu-id="4d13f-587">**Target Device** is set to **Any Device**</span></span>

        > <span data-ttu-id="4d13f-588">Pour Microsoft HoloLens, définissez **appareil cible** sur *HoloLens*.</span><span class="sxs-lookup"><span data-stu-id="4d13f-588">For the Microsoft HoloLens, set **Target Device** to *HoloLens*.</span></span>

    2.  <span data-ttu-id="4d13f-589">Le **type de build** est **D3D**</span><span class="sxs-lookup"><span data-stu-id="4d13f-589">**Build Type** is set to **D3D**</span></span>

    3.  <span data-ttu-id="4d13f-590">Le **SDK** est configuré sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="4d13f-590">**SDK** is set to **Latest installed**</span></span>

    4.  <span data-ttu-id="4d13f-591">**Version de Visual Studio** définie sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="4d13f-591">**Visual Studio Version** is set to **Latest installed**</span></span>

    5.  <span data-ttu-id="4d13f-592">La **génération et l’exécution** sont définies sur l' **ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="4d13f-592">**Build and Run** is set to **Local Machine**</span></span>

    6.  <span data-ttu-id="4d13f-593">Dans ce cas, il convient d’enregistrer la scène et de l’ajouter à la Build.</span><span class="sxs-lookup"><span data-stu-id="4d13f-593">While here, it is worth saving the scene, and adding it to the build.</span></span>

        1. <span data-ttu-id="4d13f-594">Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-594">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="4d13f-595">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4d13f-595">A save window will appear.</span></span>

            ![Ajouter des scènes ouvertes](images/AzureLabs-Lab8-83.png)

        2. <span data-ttu-id="4d13f-597">Créez un dossier pour cela, ainsi que toute nouvelle scène, puis sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez-le **scenes**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-597">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![nouveau dossier scenes](images/AzureLabs-Lab8-84.png)

        3. <span data-ttu-id="4d13f-599">Ouvrez le dossier **scenes** nouvellement créé, puis dans le champ **nom de fichier :** texte, tapez **NH\_Mr\_scène**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-599">Open your newly created **Scenes** folder, and then in the **File name:** text field, type **NH\_MR\_Scene**, then press **Save**.</span></span>

            ![nouvelle scène-NH_MR_Scene](images/AzureLabs-Lab8-85.png)

    7.  <span data-ttu-id="4d13f-601">Les paramètres restants, dans **paramètres de build**, doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="4d13f-601">The remaining settings, in **Build Settings**, should be left as default for now.</span></span>

6.  <span data-ttu-id="4d13f-602">Dans la même fenêtre, cliquez sur le bouton **paramètres du lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-602">In the same window click on the **Player Settings** button, this will open the related panel in the space where the **Inspector** is located.</span></span>    

    ![ouvrir les paramètres du lecteur](images/AzureLabs-Lab8-86.png)

7.  <span data-ttu-id="4d13f-604">Dans ce volet, quelques paramètres doivent être vérifiés :</span><span class="sxs-lookup"><span data-stu-id="4d13f-604">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="4d13f-605">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="4d13f-605">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="4d13f-606">La **version du runtime de script** doit être **expérimentale** (équivalent .net 4,6)</span><span class="sxs-lookup"><span data-stu-id="4d13f-606">**Scripting Runtime Version** should be **Experimental** (.NET 4.6 Equivalent)</span></span>
        2.  <span data-ttu-id="4d13f-607">Le **backend de script** doit être ***.net***</span><span class="sxs-lookup"><span data-stu-id="4d13f-607">**Scripting Backend** should be ***.NET***</span></span>
        3.  <span data-ttu-id="4d13f-608">Le **niveau de compatibilité** de l’API doit être **.net 4,6**</span><span class="sxs-lookup"><span data-stu-id="4d13f-608">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![compatibilité des API](images/AzureLabs-Lab8-87.png)

    2.  <span data-ttu-id="4d13f-610">Plus bas dans le panneau, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté</span><span class="sxs-lookup"><span data-stu-id="4d13f-610">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added</span></span>

        ![mettre à jour les paramètres XR](images/AzureLabs-Lab8-88.png)        

    3.  <span data-ttu-id="4d13f-612">Sous l’onglet **paramètres de publication** , sous **fonctionnalités**, conversez-le :</span><span class="sxs-lookup"><span data-stu-id="4d13f-612">Within the **Publishing Settings** tab, under **Capabilities**, heck:</span></span>

        - <span data-ttu-id="4d13f-613">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="4d13f-613">**InternetClient**</span></span>           

            ![client Internet Tick](images/AzureLabs-Lab8-89.png)

8.  <span data-ttu-id="4d13f-615">De retour dans les **paramètres de build**, les  **C# projets Unity** ne sont plus grisés : cochez la case en regard de celle-ci.</span><span class="sxs-lookup"><span data-stu-id="4d13f-615">Back in **Build Settings**, **Unity C# Projects** is no longer greyed out: tick the checkbox next to this.</span></span>

9.  <span data-ttu-id="4d13f-616">Une fois ces modifications effectuées, fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="4d13f-616">With these changes done, close the Build Settings window.</span></span>

10. <span data-ttu-id="4d13f-617">Enregistrez votre scène et votre **fichier** projet > **enregistrer la séquence/le fichier** > enregistrer le **projet**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-617">Save your Scene and Project **File** > **Save Scene / File** > **Save Project**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4d13f-618">Si vous souhaitez ignorer le composant *unité* de configuration pour ce projet (application de réalité mixte) et continuer directement dans le code, n’hésitez pas à [Télécharger ce fichier. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20308%20-%20Cross-device%20notifications/Azure-MR-308-MR.unitypackage), à l’importer dans votre projet en tant que [**package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis à [continuer Chapitre 14](#chapter-14---creating-the-tabletoscene-class-in-the-mixed-reality-unity-project).</span><span class="sxs-lookup"><span data-stu-id="4d13f-618">If you wish to skip the *Unity Set up* component for this project (mixed reality App), and continue straight into code, feel free to [download this .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20308%20-%20Cross-device%20notifications/Azure-MR-308-MR.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 14](#chapter-14---creating-the-tabletoscene-class-in-the-mixed-reality-unity-project).</span></span> <span data-ttu-id="4d13f-619">Vous devrez toujours ajouter les composants script.</span><span class="sxs-lookup"><span data-stu-id="4d13f-619">You will still need to add the script components.</span></span>

### <a name="chapter-13---importing-the-dlls-in-the-mixed-reality-unity-project"></a><span data-ttu-id="4d13f-620">Chapitre 13-importation des dll dans le projet Unity de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="4d13f-620">Chapter 13 - Importing the DLLs in the Mixed Reality Unity Project</span></span>

<span data-ttu-id="4d13f-621">Vous allez utiliser le stockage Azure pour la bibliothèque Unity (qui utilise le kit de développement logiciel (SDK) .net pour Azure).</span><span class="sxs-lookup"><span data-stu-id="4d13f-621">You will be using Azure Storage for Unity library (which uses the .Net SDK for Azure).</span></span> <span data-ttu-id="4d13f-622">Pour plus d' [informations sur l’utilisation du stockage Azure avec Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity), suivez ce lien.</span><span class="sxs-lookup"><span data-stu-id="4d13f-622">Please follow this [link on how to use Azure Storage with Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).</span></span>
<span data-ttu-id="4d13f-623">Il existe actuellement un problème connu dans Unity qui nécessite que les plug-ins soient reconfigurés après l’importation.</span><span class="sxs-lookup"><span data-stu-id="4d13f-623">There is currently a known issue in Unity which requires plugins to be reconfigured after import.</span></span> <span data-ttu-id="4d13f-624">Ces étapes (4-7 dans cette section) ne sont plus nécessaires une fois que le bogue a été résolu.</span><span class="sxs-lookup"><span data-stu-id="4d13f-624">These steps (4 - 7 in this section) will no longer be required after the bug has been resolved.</span></span>

<span data-ttu-id="4d13f-625">Pour importer le kit de développement logiciel (SDK) dans votre propre projet, assurez-vous d’avoir téléchargé la dernière version de [. pour Unity](https://aka.ms/azstorage-unitysdk).</span><span class="sxs-lookup"><span data-stu-id="4d13f-625">To import the SDK into your own project, make sure you have downloaded the latest [.unitypackage](https://aka.ms/azstorage-unitysdk).</span></span> <span data-ttu-id="4d13f-626">Ensuite, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d13f-626">Then, do the following:</span></span>

1.  <span data-ttu-id="4d13f-627">Ajoutez le fichier. pour Unity que vous avez téléchargé à partir de la version ci-dessus, à Unity à l’aide de l’option de menu **actifs** > **importer un package** > **package personnalisé** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-627">Add the .unitypackage you downloaded from the above, to Unity by using the **Assets** > **Import Package** > **Custom Package** menu option.</span></span>

2.  <span data-ttu-id="4d13f-628">Dans la zone **importer le package Unity** qui s’affiche, vous pouvez sélectionner tout dans le module de **stockage** > de **plug-in** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-628">In the **Import Unity Package** box that pops up, you can select everything under **Plugin** > **Storage**.</span></span>

    ![importer un package](images/AzureLabs-Lab8-90.png)

3.  <span data-ttu-id="4d13f-630">Cliquez sur le bouton **Importer** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="4d13f-630">Click the **Import** button to add the items to your project.</span></span>

4.  <span data-ttu-id="4d13f-631">Accédez au dossier **stockage** sous **plug-ins** dans la vue projet et sélectionnez les plug-ins suivants *uniquement*:</span><span class="sxs-lookup"><span data-stu-id="4d13f-631">Go to the **Storage** folder under **Plugins** in the Project view and select the following plugins *only*:</span></span>

    -   <span data-ttu-id="4d13f-632">Microsoft. Data. Edm</span><span class="sxs-lookup"><span data-stu-id="4d13f-632">Microsoft.Data.Edm</span></span>
    -   <span data-ttu-id="4d13f-633">Microsoft. Data. OData</span><span class="sxs-lookup"><span data-stu-id="4d13f-633">Microsoft.Data.OData</span></span>
    -   <span data-ttu-id="4d13f-634">Microsoft. WindowsAzure. Storage</span><span class="sxs-lookup"><span data-stu-id="4d13f-634">Microsoft.WindowsAzure.Storage</span></span>
    -   <span data-ttu-id="4d13f-635">Newtonsoft. JSON</span><span class="sxs-lookup"><span data-stu-id="4d13f-635">Newtonsoft.Json</span></span>
    -   <span data-ttu-id="4d13f-636">System. spatial</span><span class="sxs-lookup"><span data-stu-id="4d13f-636">System.Spatial</span></span>

    ![sélectionner les plug-ins](images/AzureLabs-Lab8-91.png)

5.  <span data-ttu-id="4d13f-638">Une fois *ces plug-ins spécifiques* sélectionnés, **décochez** **toutes les plateformes** et **décochez** **WSAPlayer** , puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-638">With *these specific plugins* selected, **uncheck** **Any Platform** and **uncheck** **WSAPlayer** then click **Apply**.</span></span>

    ![appliquer les modifications de la plateforme](images/AzureLabs-Lab8-92.png)

    > [!NOTE] 
    > <span data-ttu-id="4d13f-640">Vous marquez ces plug-ins particuliers à utiliser uniquement dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="4d13f-640">You are marking these particular plugins to only be used in the Unity Editor.</span></span> <span data-ttu-id="4d13f-641">Cela est dû au fait qu’il existe différentes versions des mêmes plug-ins dans le dossier WSA qui seront utilisées après l’exportation du projet à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="4d13f-641">This is because there are different versions of the same plugins in the WSA folder that will be used after the project is exported from Unity.</span></span>

6.  <span data-ttu-id="4d13f-642">Dans le dossier de plug-in de **stockage** , sélectionnez uniquement :</span><span class="sxs-lookup"><span data-stu-id="4d13f-642">In the **Storage** plugin folder, select only:</span></span>

    -   <span data-ttu-id="4d13f-643">Microsoft. Data. services. client</span><span class="sxs-lookup"><span data-stu-id="4d13f-643">Microsoft.Data.Services.Client</span></span>

        ![sélectionner le client des services de données](images/AzureLabs-Lab8-93.png)

7.  <span data-ttu-id="4d13f-645">Cochez la case **ne pas traiter** sous **paramètres de plateforme** , puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-645">Check the **Don't Process** box under **Platform Settings** and click **Apply**.</span></span>

    ![ne pas traiter](images/AzureLabs-Lab8-94.png)

    > [!NOTE] 
    > <span data-ttu-id="4d13f-647">Vous marquez ce plug-in « ne pas traiter », car l’assembly Unity Patcher a des difficultés à traiter ce plug-in.</span><span class="sxs-lookup"><span data-stu-id="4d13f-647">You are marking this plugin "Don't process" because the Unity assembly patcher has difficulty processing this plugin.</span></span> <span data-ttu-id="4d13f-648">Le plug-in fonctionne toujours même s’il n’est pas traité.</span><span class="sxs-lookup"><span data-stu-id="4d13f-648">The plugin will still work even though it isn't processed.</span></span>

## <a name="chapter-14---creating-the-tabletoscene-class-in-the-mixed-reality-unity-project"></a><span data-ttu-id="4d13f-649">Chapitre 14-création de la classe TableToScene dans le projet Unity de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="4d13f-649">Chapter 14 - Creating the TableToScene class in the mixed reality Unity project</span></span>

<span data-ttu-id="4d13f-650">La classe **TableToScene** est identique à celle expliquée dans le [chapitre 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).</span><span class="sxs-lookup"><span data-stu-id="4d13f-650">The **TableToScene** class is identical to the one explained in [Chapter 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).</span></span> <span data-ttu-id="4d13f-651">Créez la même classe dans le projet Unity de réalité mixte en suivant la même procédure que celle décrite dans le [chapitre 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).</span><span class="sxs-lookup"><span data-stu-id="4d13f-651">Create the same class in the mixed reality Unity Project following the same procedure explained in [Chapter 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).</span></span>

<span data-ttu-id="4d13f-652">Une fois que vous aurez terminé ce chapitre, cette classe sera configurée sur l’appareil photo de vos **projets Unity** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-652">Once you have completed this Chapter, both of your **Unity Projects** will have this class set up on the Main Camera.</span></span>

## <a name="chapter-15---creating-the-notificationreceiver-class-in-the-mixed-reality-unity-project"></a><span data-ttu-id="4d13f-653">Chapitre 15-création de la classe NotificationReceiver dans le projet Unity de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="4d13f-653">Chapter 15 - Creating the NotificationReceiver class in the Mixed Reality Unity Project</span></span>

<span data-ttu-id="4d13f-654">Le deuxième script que vous devez créer est **NotificationReceiver**, qui est responsable des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d13f-654">The second script you need to create is **NotificationReceiver**, which is responsible for:</span></span>

-   <span data-ttu-id="4d13f-655">Inscription de l’application auprès du Hub de notification lors de l’initialisation.</span><span class="sxs-lookup"><span data-stu-id="4d13f-655">Registering the app with the Notification Hub at initialization.</span></span>
-   <span data-ttu-id="4d13f-656">Écoute des notifications provenant du Hub de notification.</span><span class="sxs-lookup"><span data-stu-id="4d13f-656">Listening to notifications coming from the Notification Hub.</span></span>
-   <span data-ttu-id="4d13f-657">Désérialisation des données d’objet à partir des notifications reçues.</span><span class="sxs-lookup"><span data-stu-id="4d13f-657">Deserializing the object data from received notifications.</span></span>
-   <span data-ttu-id="4d13f-658">Déplacez le GameObjects dans la scène, en fonction des données désérialisées.</span><span class="sxs-lookup"><span data-stu-id="4d13f-658">Move the GameObjects in the scene, based on the deserialized data.</span></span>

<span data-ttu-id="4d13f-659">Pour créer le script **NotificationReceiver** :</span><span class="sxs-lookup"><span data-stu-id="4d13f-659">To create the **NotificationReceiver** script:</span></span>

1.  <span data-ttu-id="4d13f-660">Cliquez avec le bouton droit dans le dossier **scripts** , cliquez sur **créer**, **C\# script**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-660">Right-click inside the **Scripts** folder, click **Create**, **C\# Script**.</span></span> <span data-ttu-id="4d13f-661">Nommez le script **NotificationReceiver**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-661">Name the script **NotificationReceiver**.</span></span>

    <span data-ttu-id="4d13f-662">![créer un script c#](images/AzureLabs-Lab8-95.png)
    ![son nom NotificationReceiver](images/AzureLabs-Lab8-96.png)</span><span class="sxs-lookup"><span data-stu-id="4d13f-662">![create new c# script](images/AzureLabs-Lab8-95.png)
![name it NotificationReceiver](images/AzureLabs-Lab8-96.png)</span></span>

2.  <span data-ttu-id="4d13f-663">Double-cliquez sur le script pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="4d13f-663">Double click on the script to open it.</span></span>

3.  <span data-ttu-id="4d13f-664">Ajoutez les espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="4d13f-664">Add the following namespaces:</span></span>

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

4.  <span data-ttu-id="4d13f-665">Insérez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="4d13f-665">Insert the following variables:</span></span>

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

5.  <span data-ttu-id="4d13f-666">Remplacez la valeur **hubName** par le nom de votre service de hub de notification et la valeur de **hubListenEndpoint** par la valeur de point de terminaison de l’onglet stratégies d’accès, service Azure notification Hub, dans le portail Azure (Voir l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="4d13f-666">Substitute the **hubName** value with your Notification Hub Service name, and **hubListenEndpoint** value with the endpoint value found in the Access Policies tab, Azure Notification Hub Service, in the Azure Portal (see image below).</span></span>

    ![Insérer un point de terminaison de stratégie notification hubs](images/AzureLabs-Lab8-97.png)

6.  <span data-ttu-id="4d13f-668">Ajoutez maintenant les méthodes **Start ()** et **éveillé ()** pour initialiser la classe.</span><span class="sxs-lookup"><span data-stu-id="4d13f-668">Now add the **Start()** and **Awake()** methods to initialize the class.</span></span>

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

7.  <span data-ttu-id="4d13f-669">Ajoutez la méthode **WaitForNotification** pour permettre à l’application de recevoir des notifications de la bibliothèque du Hub de notification sans entrer en conflit avec le thread principal :</span><span class="sxs-lookup"><span data-stu-id="4d13f-669">Add the **WaitForNotification** method to allow the app to receive notifications from the Notification Hub Library without clashing with the Main Thread:</span></span>

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

8.  <span data-ttu-id="4d13f-670">La méthode suivante, **InitNotificationAsync ()** , inscrit l’application auprès du service de notification Hub lors de l’initialisation.</span><span class="sxs-lookup"><span data-stu-id="4d13f-670">The following method, **InitNotificationAsync()**, will register the application with the notification Hub Service at initialization.</span></span> <span data-ttu-id="4d13f-671">Le code est commenté, car Unity ne sera pas en mesure de générer le projet.</span><span class="sxs-lookup"><span data-stu-id="4d13f-671">The code is commented out as Unity will not be able to Build the project.</span></span> <span data-ttu-id="4d13f-672">Vous allez supprimer les commentaires lorsque vous importez le package NuGet Azure Messaging dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d13f-672">You will remove the comments when you import the Azure Messaging Nuget package in Visual Studio.</span></span>

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

9.  <span data-ttu-id="4d13f-673">Le gestionnaire suivant, **Channel\_PushNotificationReceived ()** , est déclenché chaque fois qu’une notification est reçue.</span><span class="sxs-lookup"><span data-stu-id="4d13f-673">The following handler, **Channel\_PushNotificationReceived()**, will be triggered every time a notification is received.</span></span> <span data-ttu-id="4d13f-674">Elle désérialisera la notification, qui sera l’entité de table Azure qui a été déplacée sur l’application de bureau, puis déplace le GameObject correspondant dans la scène MR vers la même position.</span><span class="sxs-lookup"><span data-stu-id="4d13f-674">It will deserialize the notification, which will be the Azure Table Entity that has been moved on the Desktop Application, and then move the corresponding GameObject in the MR scene to the same position.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="4d13f-675">Le code est mis en commentaire, car le code fait référence à la bibliothèque de messagerie Azure, que vous ajouterez après avoir créé le projet Unity à l’aide du gestionnaire de package NuGet, dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d13f-675">The code is commented out because the code references the Azure Messaging library, which you will add after building the Unity project using the Nuget Package Manager, within Visual Studio.</span></span> <span data-ttu-id="4d13f-676">Par conséquent, le projet Unity ne sera pas en mesure de générer, sauf s’il est mis en commentaire. N’oubliez pas que si vous générez votre projet et que vous souhaitez ensuite revenir à Unity, vous devez ajouter **un nouveau commentaire** à ce code.</span><span class="sxs-lookup"><span data-stu-id="4d13f-676">As such, the Unity project will not be able to build, unless it is commented out. Be aware, that should you build your project, and then wish to return to Unity, you will need to **re-comment** that code.</span></span>

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

10. <span data-ttu-id="4d13f-677">N’oubliez pas d’enregistrer vos modifications avant de revenir à l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="4d13f-677">Remember to save your changes before going back to the Unity Editor.</span></span>

11. <span data-ttu-id="4d13f-678">Cliquez sur la **caméra principale** dans le volet de la **hiérarchie** , afin que ses propriétés s’affichent dans l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-678">Click the **Main Camera** from the **Hierarchy** panel, so that its properties appear in the **Inspector**.</span></span>

12. <span data-ttu-id="4d13f-679">Le dossier **scripts** étant ouvert, sélectionnez le script **NotificationReceiver** et faites-le glisser sur l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-679">With the **Scripts** folder open, select the **NotificationReceiver** script and drag it onto the **Main Camera**.</span></span> <span data-ttu-id="4d13f-680">Le résultat doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d13f-680">The result should be as below:</span></span>

    ![faire glisser le script du récepteur de notification vers l’appareil photo](images/AzureLabs-Lab8-98.png)

    > [!NOTE]
    > <span data-ttu-id="4d13f-682">Si vous développez cela pour Microsoft HoloLens, vous devez mettre à jour le composant *camera* de l' **appareil photo principal**, afin que :</span><span class="sxs-lookup"><span data-stu-id="4d13f-682">If you are developing this for the Microsoft HoloLens, you will need to update the **Main Camera**'s *Camera* component, so that:</span></span>
    > - <span data-ttu-id="4d13f-683">Indicateurs d’effacement : couleur unie</span><span class="sxs-lookup"><span data-stu-id="4d13f-683">Clear Flags: Solid Color</span></span>
    > - <span data-ttu-id="4d13f-684">Arrière-plan : noir</span><span class="sxs-lookup"><span data-stu-id="4d13f-684">Background: Black</span></span>

## <a name="chapter-16---build-the-mixed-reality-project-to-uwp"></a><span data-ttu-id="4d13f-685">Chapitre 16 : créer le projet de réalité mixte sur UWP</span><span class="sxs-lookup"><span data-stu-id="4d13f-685">Chapter 16 - Build the Mixed Reality Project to UWP</span></span>

<span data-ttu-id="4d13f-686">Ce chapitre est identique au processus de génération pour le projet précédent.</span><span class="sxs-lookup"><span data-stu-id="4d13f-686">This Chapter is identical to build process for the previous project.</span></span> <span data-ttu-id="4d13f-687">Tout ce qui est nécessaire pour la section Unity de ce projet est maintenant terminé. il est donc temps de la générer à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="4d13f-687">Everything needed for the Unity section of this project has now been completed, so it is time to build it from Unity.</span></span>

1.  <span data-ttu-id="4d13f-688">Accédez à **paramètres de build** ( **fichier** > **paramètres de build** ).</span><span class="sxs-lookup"><span data-stu-id="4d13f-688">Navigate to **Build Settings** ( **File** > **Build Settings** ).</span></span>

2.  <span data-ttu-id="4d13f-689">Dans le menu **paramètres de build** , vérifiez que l’option  **C# projets Unity**\* est cochée (ce qui vous permet de modifier les scripts de ce projet, après la génération).</span><span class="sxs-lookup"><span data-stu-id="4d13f-689">From the **Build Settings** menu, ensure **Unity C# Projects**\* is ticked (which will allow you to edit the scripts in this project, after build).</span></span>

3.  <span data-ttu-id="4d13f-690">Une fois cette opération terminée, cliquez sur **générer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-690">After this is done, click **Build**.</span></span>

    ![générer le projet](images/AzureLabs-Lab8-99.png)

4.  <span data-ttu-id="4d13f-692">Une fenêtre de l' **Explorateur de fichiers** s’affiche et vous invite à entrer un emplacement à générer.</span><span class="sxs-lookup"><span data-stu-id="4d13f-692">A **File Explorer** window will popup, prompting you for a location to Build.</span></span> <span data-ttu-id="4d13f-693">Créez un nouveau dossier (en cliquant sur **nouveau dossier** dans l’angle supérieur gauche), puis nommez-le **Builds**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-693">Create a new folder (by clicking **New Folder** in the top-left corner), and name it **BUILDS**.</span></span>

    ![créer un dossier Builds](images/AzureLabs-Lab8-100.png)

    1.  <span data-ttu-id="4d13f-695">Ouvrez le nouveau dossier **Builds** , puis créez un autre dossier (en utilisant un **nouveau dossier** ) et nommez-le **NH\_l’application Mr\_** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-695">Open the new **BUILDS** folder, and create another folder (using **New Folder** once more), and name it **NH\_MR\_App**.</span></span>

        ![créer un dossier NH_MR_Apps](images/AzureLabs-Lab8-101.png)

    2.  <span data-ttu-id="4d13f-697">Avec l' **application NH\_MR\_** sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="4d13f-697">With the **NH\_MR\_App** selected.</span></span> <span data-ttu-id="4d13f-698">Cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-698">click **Select Folder**.</span></span> <span data-ttu-id="4d13f-699">La génération du projet prendra quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4d13f-699">The project will take a minute or so to build.</span></span>

5.  <span data-ttu-id="4d13f-700">Après la génération, une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="4d13f-700">Following the build, a **File Explorer** window will open at the location of your new project.</span></span>



## <a name="chapter-17---add-nuget-packages-to-the-unitymrnotifhub-solution"></a><span data-ttu-id="4d13f-701">Chapitre 17-ajouter des packages NuGet à la solution UnityMRNotifHub</span><span class="sxs-lookup"><span data-stu-id="4d13f-701">Chapter 17 - Add NuGet packages to the UnityMRNotifHub Solution</span></span>

> [!WARNING] 
> <span data-ttu-id="4d13f-702">N’oubliez pas que, une fois que vous ajoutez les packages NuGet suivants (et que vous supprimez les marques de commentaire du code dans le [chapitre](#chapter-18---edit-unitymrnotifhub-application-notificationreceiver-class)suivant), le code, lorsqu’il est rouvert dans le projet Unity, présente des erreurs.</span><span class="sxs-lookup"><span data-stu-id="4d13f-702">Please remember that, once you add the following NuGet Packages (and uncomment the code in the next [Chapter](#chapter-18---edit-unitymrnotifhub-application-notificationreceiver-class)), the Code, when reopened within the Unity Project, will present errors.</span></span> <span data-ttu-id="4d13f-703">Si vous souhaitez revenir en arrière et poursuivre la modification dans l’éditeur Unity, vous avez besoin d’un commentaire qui errosome le code, puis de supprimer les marques de commentaire ultérieurement, une fois que vous êtes à nouveau dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d13f-703">If you wish to go back and continue editing in the Unity Editor, you will need comment that errosome code, and then uncomment again later, once you are back in Visual Studio.</span></span> 

<span data-ttu-id="4d13f-704">Une fois la génération de la réalité mixte terminée, accédez au projet de réalité mixte que vous avez créé, puis double-cliquez sur le fichier de solution (. sln) dans ce dossier pour ouvrir votre solution avec Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4d13f-704">Once the mixed reality build has been completed, navigate to the mixed reality project, which you built, and double click on the solution (.sln) file within that folder, to open your solution with Visual Studio 2017.</span></span>
<span data-ttu-id="4d13f-705">Vous devez maintenant ajouter le package NuGet **WindowsAzure. Messaging. Managed** . Il s’agit d’une bibliothèque qui est utilisée pour recevoir des notifications du Hub de notification.</span><span class="sxs-lookup"><span data-stu-id="4d13f-705">You will now need to add the **WindowsAzure.Messaging.managed** NuGet package; this is a library that is used to receive Notifications from the Notification Hub.</span></span>

<span data-ttu-id="4d13f-706">Pour importer le package NuGet :</span><span class="sxs-lookup"><span data-stu-id="4d13f-706">To import the NuGet package:</span></span>

1.  <span data-ttu-id="4d13f-707">Dans le **Explorateur de solutions**, cliquez avec le bouton droit sur votre solution</span><span class="sxs-lookup"><span data-stu-id="4d13f-707">In the **Solution Explorer**, right click on your Solution</span></span>

2.  <span data-ttu-id="4d13f-708">Cliquez sur **gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-708">Click on **Manage NuGet Packages**.</span></span>

    ![Ouvrez le gestionnaire NuGet](images/AzureLabs-Lab8-102.png)

3.  <span data-ttu-id="4d13f-710">Sélectionnez l’onglet ***Parcourir*** et recherchez **WindowsAzure. Messaging. Managed**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-710">Select the ***Browse*** tab and search for **WindowsAzure.Messaging.managed**.</span></span>

    ![Rechercher le package de messagerie Windows Azure](images/AzureLabs-Lab8-103.png)

4.  <span data-ttu-id="4d13f-712">Sélectionnez le résultat (comme indiqué ci-dessous) et, dans la fenêtre de droite, activez la case à cocher en regard de **projet**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-712">Select the result (as shown below), and in the window to the right, select the checkbox next to **Project**.</span></span> <span data-ttu-id="4d13f-713">Une coche s’affiche dans la case à côté de **projet**, avec la case à cocher en regard du projet **assembly-CSharp** et **UnityMRNotifHub** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-713">This will place a tick in the checkbox next to **Project**, along with the checkbox next to the **Assembly-CSharp** and **UnityMRNotifHub** project.</span></span>

    ![cocher tous les projets](images/AzureLabs-Lab8-104.png)

5.  <span data-ttu-id="4d13f-715">La version initialement fournie **n’est peut-être pas** compatible avec ce projet.</span><span class="sxs-lookup"><span data-stu-id="4d13f-715">The version initially provided **may not** be compatible with this project.</span></span> <span data-ttu-id="4d13f-716">Par conséquent, cliquez sur le menu déroulant en regard de **version**, puis cliquez sur **version 0.1.7.9**, puis sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-716">Therefore, click on the dropdown menu next to **Version**, and click **Version 0.1.7.9**, then click **Install**.</span></span>

6.  <span data-ttu-id="4d13f-717">Vous avez maintenant terminé l’installation du package NuGet.</span><span class="sxs-lookup"><span data-stu-id="4d13f-717">You have now finished installing the NuGet package.</span></span> <span data-ttu-id="4d13f-718">Recherchez le code commenté que vous avez entré dans la classe **NotificationReceiver** et supprimez les commentaires.</span><span class="sxs-lookup"><span data-stu-id="4d13f-718">Find the commented code you entered in the **NotificationReceiver** class and remove the comments..</span></span>



## <a name="chapter-18---edit-unitymrnotifhub-application-notificationreceiver-class"></a><span data-ttu-id="4d13f-719">Chapitre 18-modifier l’application UnityMRNotifHub, classe NotificationReceiver</span><span class="sxs-lookup"><span data-stu-id="4d13f-719">Chapter 18 - Edit UnityMRNotifHub application, NotificationReceiver class</span></span>

<span data-ttu-id="4d13f-720">Après avoir ajouté les **packages NuGet**, vous devez supprimer les *marques de commentaire* d’une partie du code dans la classe **NotificationReceiver** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-720">Following having added the **NuGet Packages**, you will need to *uncomment* some of the code within the **NotificationReceiver** class.</span></span>

<span data-ttu-id="4d13f-721">Cela comprend les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4d13f-721">This includes:</span></span>

1. <span data-ttu-id="4d13f-722">Espace de noms en haut :</span><span class="sxs-lookup"><span data-stu-id="4d13f-722">The namespace at the top:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Messaging;
    ```

2. <span data-ttu-id="4d13f-723">Tout le code dans la méthode **InitNotificationsAsync ()** :</span><span class="sxs-lookup"><span data-stu-id="4d13f-723">All the code within the **InitNotificationsAsync()** method:</span></span>

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
> <span data-ttu-id="4d13f-724">Le code ci-dessus contient un commentaire : Assurez-vous que vous n’avez *pas accidentellement supprimé le commentaire de ce* commentaire (car le code ne se compilera pas si vous en avez !).</span><span class="sxs-lookup"><span data-stu-id="4d13f-724">The code above has a comment in it: ensure that you have not accidentally *uncommented* that comment (as the code will not compile if you have!).</span></span>

3. <span data-ttu-id="4d13f-725">Enfin, l’événement **Channel_PushNotificationReceived** :</span><span class="sxs-lookup"><span data-stu-id="4d13f-725">And, lastly, the **Channel_PushNotificationReceived** event:</span></span>

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

<span data-ttu-id="4d13f-726">Avec ces commentaires, veillez à enregistrer, puis passez au chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="4d13f-726">With these uncommented, ensure that you save, and then proceed to the next Chapter.</span></span>

## <a name="chapter-19---associate-the-mixed-reality-project-to-the-store-app"></a><span data-ttu-id="4d13f-727">Chapitre 19-associer le projet de réalité mixte à l’application du Windows Store</span><span class="sxs-lookup"><span data-stu-id="4d13f-727">Chapter 19 - Associate the mixed reality project to the Store app</span></span>

<span data-ttu-id="4d13f-728">Vous devez maintenant associer le projet de **réalité mixte** à l’application du Windows Store que vous avez créée dans au début du laboratoire.</span><span class="sxs-lookup"><span data-stu-id="4d13f-728">You now need to associate the **mixed reality** project to the Store App you created in at the start of the lab.</span></span>

1.  <span data-ttu-id="4d13f-729">Ouvrez la solution.</span><span class="sxs-lookup"><span data-stu-id="4d13f-729">Open the solution.</span></span>

2.  <span data-ttu-id="4d13f-730">Cliquez avec le bouton droit sur le projet d’application UWP dans le panneau Explorateur de solutions, accédez à **Store**et **associez l’application au Store...** .</span><span class="sxs-lookup"><span data-stu-id="4d13f-730">Right click on the UWP app Project in the Solution Explorer panel, the go to **Store**, and **Associate App with the Store...**.</span></span>

    ![ouvrir l’Association de magasins](images/AzureLabs-Lab8-105.png)

3.  <span data-ttu-id="4d13f-732">Une nouvelle fenêtre s’affiche, appelée **associer votre application au Windows Store**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-732">A new window will appear called **Associate Your App with the Windows Store**.</span></span> <span data-ttu-id="4d13f-733">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-733">Click **Next**.</span></span>

    ![accéder à l’écran suivant](images/AzureLabs-Lab8-106.png)

4.  <span data-ttu-id="4d13f-735">Il charge toutes les applications associées au compte que vous avez connecté.</span><span class="sxs-lookup"><span data-stu-id="4d13f-735">It will load up all the Applications associated with the Account which you have logged in.</span></span> <span data-ttu-id="4d13f-736">Si vous n’êtes pas connecté à votre compte, vous pouvez vous **connecter** à cette page.</span><span class="sxs-lookup"><span data-stu-id="4d13f-736">If you are not logged in to your account, you can **Log In** on this page.</span></span>

5.  <span data-ttu-id="4d13f-737">Recherchez le **nom** de l’application Windows Store que vous avez créé au début de ce didacticiel et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="4d13f-737">Find the **Store App name** that you created at the start of this tutorial and select it.</span></span> <span data-ttu-id="4d13f-738">Ensuite, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-738">Then click **Next**.</span></span>

    ![Recherchez et sélectionnez le nom de votre boutique](images/AzureLabs-Lab8-107.png)

6.  <span data-ttu-id="4d13f-740">Cliquez sur **associer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-740">Click **Associate**.</span></span>

    ![associer l’application](images/AzureLabs-Lab8-108.png)

7.  <span data-ttu-id="4d13f-742">Votre application est maintenant **associée** à l’application du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="4d13f-742">Your App is now **Associated** with the Store App.</span></span> <span data-ttu-id="4d13f-743">Cela est nécessaire pour activer les notifications.</span><span class="sxs-lookup"><span data-stu-id="4d13f-743">This is necessary for enabling Notifications.</span></span>

## <a name="chapter-20---deploy-unitymrnotifhub-and-unitydesktopnotifhub-applications"></a><span data-ttu-id="4d13f-744">Chapitre 20 : déployer des applications UnityMRNotifHub et UnityDesktopNotifHub</span><span class="sxs-lookup"><span data-stu-id="4d13f-744">Chapter 20 - Deploy UnityMRNotifHub and UnityDesktopNotifHub applications</span></span>

<span data-ttu-id="4d13f-745">Ce chapitre peut être plus facile avec deux personnes, car le résultat inclut les applications en cours d’exécution, l’une s’exécutant sur le Bureau de votre ordinateur et l’autre au sein de votre casque immersif.</span><span class="sxs-lookup"><span data-stu-id="4d13f-745">This Chapter may be easier with two people, as the result will include both apps running, one running on your computer Desktop, and the other within your immersive headset.</span></span>

<span data-ttu-id="4d13f-746">L’application de casque immersif attend de recevoir les modifications apportées à la scène (modifications de position du GameObjects local) et l’application de bureau apporte des modifications à leur scène locale (modifications de position), qui sont partagées avec l’application RM.</span><span class="sxs-lookup"><span data-stu-id="4d13f-746">The immersive headset app is waiting to receive changes to the scene (position changes of the local GameObjects), and the Desktop app will be making changes to their local scene (position changes), which will be shared to the MR app.</span></span> <span data-ttu-id="4d13f-747">Il est logique de déployer l’application RM en premier, puis l’application de bureau, afin que le récepteur puisse commencer à écouter.</span><span class="sxs-lookup"><span data-stu-id="4d13f-747">It makes sense to deploy the MR app first, followed by the Desktop app, so that the receiver can begin listening.</span></span>

<span data-ttu-id="4d13f-748">Pour déployer l’application **UnityMRNotifHub** sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="4d13f-748">To deploy the **UnityMRNotifHub** app on your Local Machine:</span></span>

1.  <span data-ttu-id="4d13f-749">Ouvrez le fichier solution de votre application **UnityMRNotifHub** dans **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-749">Open the solution file of your **UnityMRNotifHub** app in **Visual Studio 2017**.</span></span>

2.  <span data-ttu-id="4d13f-750">Dans la **plateforme**de la solution, sélectionnez **x86, ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-750">In the **Solution Platform**, select **x86, Local Machine**.</span></span>

3.  <span data-ttu-id="4d13f-751">Dans la **configuration** de la solution, sélectionnez **Déboguer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-751">In the **Solution Configuration** select **Debug**.</span></span>

    ![définir la configuration du projet](images/AzureLabs-Lab8-109.png)

4.  <span data-ttu-id="4d13f-753">Accédez au **menu Générer** , puis cliquez sur **déployer la solution** pour chargement l’application sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4d13f-753">Go to **Build menu** and click on **Deploy Solution** to sideload the application to your machine.</span></span>

5.  <span data-ttu-id="4d13f-754">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancées.</span><span class="sxs-lookup"><span data-stu-id="4d13f-754">Your App should now appear in the list of installed apps, ready to be launched.</span></span>

<span data-ttu-id="4d13f-755">Pour déployer l’application **UnityDesktopNotifHub** sur l’ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="4d13f-755">To deploy the **UnityDesktopNotifHub** app on Local Machine:</span></span>

1.  <span data-ttu-id="4d13f-756">Ouvrez le fichier solution de votre application **UnityDesktopNotifHub** dans **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-756">Open the solution file of your **UnityDesktopNotifHub** app in **Visual Studio 2017**.</span></span>

2.  <span data-ttu-id="4d13f-757">Dans la **plateforme**de la solution, sélectionnez **x86, ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-757">In the **Solution Platform**, select **x86, Local Machine**.</span></span>

3.  <span data-ttu-id="4d13f-758">Dans la **configuration** de la solution, sélectionnez **Déboguer**.</span><span class="sxs-lookup"><span data-stu-id="4d13f-758">In the **Solution Configuration** select **Debug**.</span></span>

    ![définir la configuration du projet](images/AzureLabs-Lab8-110.png)

4.  <span data-ttu-id="4d13f-760">Accédez au **menu Générer** , puis cliquez sur **déployer la solution** pour chargement l’application sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4d13f-760">Go to **Build menu** and click on **Deploy Solution** to sideload the application to your machine.</span></span>

5.  <span data-ttu-id="4d13f-761">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancées.</span><span class="sxs-lookup"><span data-stu-id="4d13f-761">Your App should now appear in the list of installed apps, ready to be launched.</span></span>

6.  <span data-ttu-id="4d13f-762">Lancez l’application de réalité mixte, suivie de l’application de bureau.</span><span class="sxs-lookup"><span data-stu-id="4d13f-762">Launch the mixed reality application, followed by the Desktop application.</span></span>

<span data-ttu-id="4d13f-763">Une fois les deux applications en cours d’exécution, déplacez un objet dans la scène du Bureau (à l’aide du bouton gauche de la souris).</span><span class="sxs-lookup"><span data-stu-id="4d13f-763">With both applications running, move an object in the desktop scene (using the Left Mouse Button).</span></span> <span data-ttu-id="4d13f-764">Ces modifications positionnelles seront effectuées localement, sérialisées et envoyées au service Function App.</span><span class="sxs-lookup"><span data-stu-id="4d13f-764">These positional changes will be made locally, serialized, and sent to the Function App service.</span></span> <span data-ttu-id="4d13f-765">Le service de Function App met ensuite à jour la table avec le hub de notification.</span><span class="sxs-lookup"><span data-stu-id="4d13f-765">The Function App service will then update the Table along with the Notification Hub.</span></span> <span data-ttu-id="4d13f-766">Une fois la mise à jour reçue, le hub de notification envoie les données mises à jour directement à toutes les applications inscrites (dans ce cas, l’application de casque immersif), qui désérialise ensuite les données entrantes et appliquent les nouvelles données positionnelles aux objets locaux. en les déplaçant dans la scène.</span><span class="sxs-lookup"><span data-stu-id="4d13f-766">Having received an update, the Notification Hub will send the updated data directly to all the registered applications (in this case the immersive headset app), which will then deserialize the incoming data, and apply the new positional data to the local objects, moving them in scene.</span></span>


## <a name="your-finished-your-azure-notification-hubs-application"></a><span data-ttu-id="4d13f-767">Votre application Azure Notification Hubs terminée</span><span class="sxs-lookup"><span data-stu-id="4d13f-767">Your finished your Azure Notification Hubs application</span></span>
 
<span data-ttu-id="4d13f-768">Félicitations, vous avez créé une application de réalité mixte qui tire parti du service Azure Notification Hubs et permet la communication entre les applications.</span><span class="sxs-lookup"><span data-stu-id="4d13f-768">Congratulations, you built a mixed reality app that leverages the Azure Notification Hubs Service and allow communication between apps.</span></span>
 
![fin du produit final](images/AzureLabs-Lab8-00.png)
 
## <a name="bonus-exercises"></a><span data-ttu-id="4d13f-770">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="4d13f-770">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="4d13f-771">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="4d13f-771">Exercise 1</span></span>

<span data-ttu-id="4d13f-772">Pouvez-vous utiliser la modification de la couleur du GameObjects et envoyer cette notification à d’autres applications en affichant la scène ?</span><span class="sxs-lookup"><span data-stu-id="4d13f-772">Can you work out how to change the color of the GameObjects and send that notification to other apps viewing the scene?</span></span>

### <a name="exercise-2"></a><span data-ttu-id="4d13f-773">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="4d13f-773">Exercise 2</span></span>

<span data-ttu-id="4d13f-774">Pouvez-vous ajouter le déplacement du GameObjects à votre application RM et voir la scène mise à jour dans votre application de bureau ?</span><span class="sxs-lookup"><span data-stu-id="4d13f-774">Can you add movement of the GameObjects to your MR app and see the updated scene in your desktop app?</span></span>
