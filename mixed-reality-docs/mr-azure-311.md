---
title: MR et Azure 311-Microsoft Graph
description: Suivez ce cours pour apprendre à tirer parti des Microsoft Graph et à vous connecter aux données qui pilotent la productivité, au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, Microsoft Graph, hololens, immersif, VR
ms.openlocfilehash: 775971c4e4289d2dc963dfa2bf033192d9f3489e
ms.sourcegitcommit: 3b32339c5d5c79eaecd84ed27254a8f4321731f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70047202"
---
>[!NOTE]
><span data-ttu-id="a40a4-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="a40a4-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="a40a4-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="a40a4-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="a40a4-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="a40a4-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="a40a4-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a40a4-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="a40a4-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="a40a4-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="a40a4-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="a40a4-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

# <a name="mr-and-azure-311---microsoft-graph"></a><span data-ttu-id="a40a4-110">MR et Azure 311-Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="a40a4-110">MR and Azure 311 - Microsoft Graph</span></span>

<span data-ttu-id="a40a4-111">Dans ce cours, vous allez apprendre à utiliser *Microsoft Graph* pour vous connecter à votre compte Microsoft à l’aide de l’authentification sécurisée dans une application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="a40a4-111">In this course, you will learn how to use *Microsoft Graph* to log in into your Microsoft account using secure authentication within a mixed reality application.</span></span> <span data-ttu-id="a40a4-112">Vous allez ensuite récupérer et afficher vos réunions planifiées dans l’interface de l’application.</span><span class="sxs-lookup"><span data-stu-id="a40a4-112">You will then retrieve and display your scheduled meetings in the application interface.</span></span>

![](images/AzureLabs-Lab311-00.png)

<span data-ttu-id="a40a4-113">*Microsoft Graph* est un ensemble d’API conçues pour permettre l’accès à de nombreux services de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a40a4-113">*Microsoft Graph* is a set of APIs designed to enable access to many of Microsoft's services.</span></span> <span data-ttu-id="a40a4-114">Microsoft décrit Microsoft Graph comme une matrice de ressources connectées par des relations, ce qui signifie qu’elle permet à une application d’accéder à toutes sortes de données utilisateur connectées.</span><span class="sxs-lookup"><span data-stu-id="a40a4-114">Microsoft describes Microsoft Graph as being a matrix of resources connected by relationships, meaning it allows an application to access all sorts of connected user data.</span></span> <span data-ttu-id="a40a4-115">Pour plus d’informations, consultez la [page Microsoft Graph](https://developer.microsoft.com/graph).</span><span class="sxs-lookup"><span data-stu-id="a40a4-115">For more information, visit the [Microsoft Graph page](https://developer.microsoft.com/graph).</span></span>

<span data-ttu-id="a40a4-116">Le développement inclut la création d’une application dans laquelle l’utilisateur sera invité à pointer vers le regard, puis à appuyer sur une sphère, ce qui invite l’utilisateur à se connecter en toute sécurité à un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a40a4-116">Development will include the creation of an app where the user will be instructed to gaze at and then tap a sphere, which will prompt the user to log in safely to a Microsoft account.</span></span> <span data-ttu-id="a40a4-117">Une fois connecté à son compte, l’utilisateur est en mesure de consulter la liste des réunions planifiées pour la journée.</span><span class="sxs-lookup"><span data-stu-id="a40a4-117">Once logged in to their account, the user will be able to see a list of meetings scheduled for the day.</span></span>

<span data-ttu-id="a40a4-118">Une fois ce cours terminé, vous disposerez d’une application HoloLens de réalité mixte, qui sera en mesure d’effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="a40a4-118">Having completed this course, you will have a mixed reality HoloLens application, which will be able to do the following:</span></span>

1.  <span data-ttu-id="a40a4-119">À l’aide du geste TAP, appuyez sur un objet, qui invite l’utilisateur à se connecter à un compte Microsoft (en sortant de l’application pour se connecter, puis de nouveau dans l’application).</span><span class="sxs-lookup"><span data-stu-id="a40a4-119">Using the Tap gesture, tap on an object, which will prompt the user to log into a Microsoft Account (moving out of the app to log in, and then back into the app again).</span></span>
2.  <span data-ttu-id="a40a4-120">Affichez la liste des réunions planifiées pour la journée.</span><span class="sxs-lookup"><span data-stu-id="a40a4-120">View a list of meetings scheduled for the day.</span></span> 

<span data-ttu-id="a40a4-121">Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception.</span><span class="sxs-lookup"><span data-stu-id="a40a4-121">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="a40a4-122">Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="a40a4-122">This course is designed to teach you how to integrate an Azure Service with your Unity project.</span></span> <span data-ttu-id="a40a4-123">C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="a40a4-123">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

## <a name="device-support"></a><span data-ttu-id="a40a4-124">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="a40a4-124">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="a40a4-125">Course</span><span class="sxs-lookup"><span data-stu-id="a40a4-125">Course</span></span></th><th style="width:150px"> <span data-ttu-id="a40a4-126"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="a40a4-126"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="a40a4-127"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="a40a4-127"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="a40a4-128">MR et Azure 311: Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="a40a4-128">MR and Azure 311: Microsoft Graph</span></span></td><td style="text-align: center;"> <span data-ttu-id="a40a4-129">✔️</span><span class="sxs-lookup"><span data-stu-id="a40a4-129">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="prerequisites"></a><span data-ttu-id="a40a4-130">Prérequis</span><span class="sxs-lookup"><span data-stu-id="a40a4-130">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="a40a4-131">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="a40a4-131">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="a40a4-132">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de la rédaction (juillet 2018).</span><span class="sxs-lookup"><span data-stu-id="a40a4-132">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (July 2018).</span></span> <span data-ttu-id="a40a4-133">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a40a4-133">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you will find in newer software than what is listed below.</span></span>

<span data-ttu-id="a40a4-134">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:</span><span class="sxs-lookup"><span data-stu-id="a40a4-134">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="a40a4-135">Un PC de développement</span><span class="sxs-lookup"><span data-stu-id="a40a4-135">A development PC</span></span>
- [<span data-ttu-id="a40a4-136">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="a40a4-136">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="a40a4-137">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="a40a4-137">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="a40a4-138">Unity 2017,4</span><span class="sxs-lookup"><span data-stu-id="a40a4-138">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="a40a4-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a40a4-139">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="a40a4-140">[Microsoft HoloLens](hololens-hardware-details.md) avec mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="a40a4-140">A [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="a40a4-141">Accès Internet pour l’installation d’Azure et la récupération des données de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="a40a4-141">Internet access for Azure setup and Microsoft Graph data retrieval</span></span>
- <span data-ttu-id="a40a4-142">Un **compte Microsoft** valide (personnel ou professionnel/scolaire)</span><span class="sxs-lookup"><span data-stu-id="a40a4-142">A valid **Microsoft Account** (either personal or work/school)</span></span>
- <span data-ttu-id="a40a4-143">Quelques réunions planifiées pour la journée en cours, à l’aide du même compte Microsoft</span><span class="sxs-lookup"><span data-stu-id="a40a4-143">A few meetings scheduled for the current day, using the same Microsoft Account</span></span>

### <a name="before-you-start"></a><span data-ttu-id="a40a4-144">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a40a4-144">Before you start</span></span>

1.  <span data-ttu-id="a40a4-145">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="a40a4-145">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="a40a4-146">Configurez et testez votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="a40a4-146">Set up and test your HoloLens.</span></span> <span data-ttu-id="a40a4-147">Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="a40a4-147">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span> 
3.  <span data-ttu-id="a40a4-148">Il est judicieux d’effectuer un réglage de l’étalonnage et du capteur au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="a40a4-148">It is a good idea to perform Calibration and Sensor Tuning when beginning developing a new HoloLens App (sometimes it can help to perform those tasks for each user).</span></span> 

<span data-ttu-id="a40a4-149">Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens-2).</span><span class="sxs-lookup"><span data-stu-id="a40a4-149">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens-2).</span></span>

<span data-ttu-id="a40a4-150">Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="a40a4-150">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

## <a name="chapter-1---create-your-app-in-the-application-registration-portal"></a><span data-ttu-id="a40a4-151">Chapitre 1-créer votre application dans le portail d’inscription des applications</span><span class="sxs-lookup"><span data-stu-id="a40a4-151">Chapter 1 - Create your app in the Application Registration Portal</span></span>

<span data-ttu-id="a40a4-152">Pour commencer, vous devrez créer et inscrire votre application dans le **portail d’inscription des applications**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-152">To begin with, you will need to create and register your application in the **Application Registration Portal**.</span></span>

<span data-ttu-id="a40a4-153">Dans ce chapitre, vous trouverez également la clé de service qui vous permettra d’effectuer des appels à *Microsoft Graph* pour accéder au contenu de votre compte.</span><span class="sxs-lookup"><span data-stu-id="a40a4-153">In this Chapter you will also find the Service Key that will allow you to make calls to *Microsoft Graph* to access your account content.</span></span>

1.  <span data-ttu-id="a40a4-154">Accédez au [portail d’inscription des applications Microsoft](https://apps.dev.microsoft.com) et connectez-vous avec votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a40a4-154">Navigate to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com) and login with your Microsoft Account.</span></span> <span data-ttu-id="a40a4-155">Une fois que vous êtes connecté, vous êtes redirigé vers le **portail d’inscription des applications**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-155">Once you have logged in, you will be redirected to the **Application Registration Portal**.</span></span>

2.  <span data-ttu-id="a40a4-156">Dans la section **mes applications** , cliquez sur le bouton **Ajouter une application**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-156">In the **My applications** section, click on the button **Add an app**.</span></span>

    ![](images/AzureLabs-Lab311-01.png)![](images/AzureLabs-Lab311-02.png)

    > [!IMPORTANT]
    > <span data-ttu-id="a40a4-157">Le **portail d’inscription des applications** peut paraître différent, selon que vous avez déjà travaillé avec *Microsoft Graph*.</span><span class="sxs-lookup"><span data-stu-id="a40a4-157">The **Application Registration Portal** can look different, depending on whether you have previously worked with *Microsoft Graph*.</span></span> <span data-ttu-id="a40a4-158">Les captures d’écran ci-dessous affichent ces différentes versions.</span><span class="sxs-lookup"><span data-stu-id="a40a4-158">The below screenshots display these different versions.</span></span>

3.  <span data-ttu-id="a40a4-159">Ajoutez un nom pour votre application, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-159">Add a name for your application and click **Create**.</span></span>

    ![](images/AzureLabs-Lab311-03.png)

4.  <span data-ttu-id="a40a4-160">Une fois l’application créée, vous êtes redirigé vers la page principale de l’application.</span><span class="sxs-lookup"><span data-stu-id="a40a4-160">Once the application has been created, you will be redirected to the application main page.</span></span> <span data-ttu-id="a40a4-161">Copiez l’ID de l' **application** et veillez à noter cette valeur dans un endroit sûr. vous l’utiliserez bientôt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="a40a4-161">Copy the **Application Id** and make sure to note this value somewhere safe, you will use it soon in your code.</span></span>

    ![](images/AzureLabs-Lab311-04.png)

5.  <span data-ttu-id="a40a4-162">Dans la section plateformes, assurez **-** vous que **application native** est affiché.</span><span class="sxs-lookup"><span data-stu-id="a40a4-162">In the **Platforms** section, make sure **Native Application** is displayed.</span></span> <span data-ttu-id="a40a4-163">Si ce *n’est pas* le cas, cliquez sur Ajouter une **plateforme** , puis sélectionnez **application native**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-163">If *not* click on **Add Platform** and select **Native Application**.</span></span>

    ![](images/AzureLabs-Lab311-05.png)

6.  <span data-ttu-id="a40a4-164">Faites défiler la page vers le dessous et, dans la section intitulée **Microsoft Graph autorisations** , vous devez ajouter des autorisations supplémentaires pour l’application.</span><span class="sxs-lookup"><span data-stu-id="a40a4-164">Scroll down in the same page and in the section called **Microsoft Graph Permissions** you will need to add additional permissions for the application.</span></span> <span data-ttu-id="a40a4-165">Cliquez sur **Ajouter** en regard de **autorisations déléguées**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-165">Click on **Add** next to **Delegated Permissions**.</span></span>

    ![](images/AzureLabs-Lab311-06.png)

7.  <span data-ttu-id="a40a4-166">Étant donné que vous souhaitez que votre application accède au calendrier de l’utilisateur, activez la case à cocher **calendriers. lire** , puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-166">Since you want your application to access the user's Calendar, check the box called **Calendars.Read** and click **OK**.</span></span>

    ![](images/AzureLabs-Lab311-07.png)

8.  <span data-ttu-id="a40a4-167">Faites défiler vers le bas et cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a40a4-167">Scroll to the bottom and click the **Save** button.</span></span>

    ![](images/AzureLabs-Lab311-08.png)

9.  <span data-ttu-id="a40a4-168">Votre enregistrement sera confirmé et vous pourrez vous déconnecter du **portail d’inscription des applications**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-168">Your save will be confirmed, and you can log out from the **Application Registration Portal**.</span></span>

## <a name="chapter-2---set-up-the-unity-project"></a><span data-ttu-id="a40a4-169">Chapitre 2-configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="a40a4-169">Chapter 2 - Set up the Unity project</span></span>

<span data-ttu-id="a40a4-170">Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="a40a4-170">The following is a typical set up for developing with mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="a40a4-171">Ouvrez *Unity* et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-171">Open *Unity* and click **New**.</span></span>

    ![](images/AzureLabs-Lab311-09.png)

2.  <span data-ttu-id="a40a4-172">Vous devez fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="a40a4-172">You need to provide a Unity project name.</span></span> <span data-ttu-id="a40a4-173">Insérez **MSGraphMR**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-173">Insert **MSGraphMR**.</span></span> <span data-ttu-id="a40a4-174">Assurez-vous que le modèle de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-174">Make sure the project template is set to **3D**.</span></span> <span data-ttu-id="a40a4-175">Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés).</span><span class="sxs-lookup"><span data-stu-id="a40a4-175">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="a40a4-176">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-176">Then, click **Create project**.</span></span>

    ![](images/AzureLabs-Lab311-10.png)

3.  <span data-ttu-id="a40a4-177">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-177">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="a40a4-178">Accédez à **modifier** > les**Préférences** , puis à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-178">Go to **Edit** > **Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="a40a4-179">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-179">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="a40a4-180">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="a40a4-180">Close the **Preferences** window.</span></span>

    ![](images/AzureLabs-Lab311-11.png)

4.  <span data-ttu-id="a40a4-181">Accédez à **fichier** > **paramètres de build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le bouton **changer de plateforme** pour appliquer votre sélection.</span><span class="sxs-lookup"><span data-stu-id="a40a4-181">Go to **File** > **Build Settings** and select **Universal Windows Platform**, then click on the **Switch Platform** button to apply your selection.</span></span>

    ![](images/AzureLabs-Lab311-12.png)

5.  <span data-ttu-id="a40a4-182">Tout en conservant les**paramètres de génération**de **fichiers** > , assurez-vous que:</span><span class="sxs-lookup"><span data-stu-id="a40a4-182">While still in **File** > **Build Settings**, make sure that:</span></span>

    1. <span data-ttu-id="a40a4-183">L' **appareil cible** est défini sur **HoloLens**</span><span class="sxs-lookup"><span data-stu-id="a40a4-183">**Target Device** is set to **HoloLens**</span></span>
    2. <span data-ttu-id="a40a4-184">Le **type de build** est **D3D**</span><span class="sxs-lookup"><span data-stu-id="a40a4-184">**Build Type** is set to **D3D**</span></span>
    3. <span data-ttu-id="a40a4-185">Le **SDK** est configuré sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="a40a4-185">**SDK** is set to **Latest installed**</span></span>
    4. <span data-ttu-id="a40a4-186">**Version de Visual Studio** définie sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="a40a4-186">**Visual Studio Version** is set to **Latest installed**</span></span>
    5. <span data-ttu-id="a40a4-187">La **génération et l’exécution** sont définies sur l' **ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="a40a4-187">**Build and Run** is set to **Local Machine**</span></span>
    6. <span data-ttu-id="a40a4-188">Enregistrez la scène et ajoutez-la à la Build.</span><span class="sxs-lookup"><span data-stu-id="a40a4-188">Save the scene and add it to the build.</span></span>

        1. <span data-ttu-id="a40a4-189">Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-189">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="a40a4-190">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a40a4-190">A save window will appear.</span></span>

            ![](images/AzureLabs-Lab311-13.png)

        2. <span data-ttu-id="a40a4-191">Créez un dossier pour cela, ainsi que toute nouvelle scène.</span><span class="sxs-lookup"><span data-stu-id="a40a4-191">Create a new folder for this, and any future, scene.</span></span> <span data-ttu-id="a40a4-192">Sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez-le Scenes.</span><span class="sxs-lookup"><span data-stu-id="a40a4-192">Select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![](images/AzureLabs-Lab311-14.png)

        3. <span data-ttu-id="a40a4-193">Ouvrez le dossier scenes nouvellement créé, puis dans le champ *nom de fichier*:, tapez **MR_ComputerVisionScene**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-193">Open your newly created **Scenes** folder, and then in the *File name*: text field, type **MR_ComputerVisionScene**, then click **Save**.</span></span>

            ![](images/AzureLabs-Lab311-15.png)

            > [!IMPORTANT] 
            > <span data-ttu-id="a40a4-194">Sachez que vous devez enregistrer vos scènes Unity dans le dossier *ressources* , car elles doivent être associées au projet Unity.</span><span class="sxs-lookup"><span data-stu-id="a40a4-194">Be aware, you must save your Unity scenes within the *Assets* folder, as they must be associated with the Unity project.</span></span> <span data-ttu-id="a40a4-195">La création du dossier scenes (et d’autres dossiers similaires) est un moyen classique de structurer un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="a40a4-195">Creating the scenes folder (and other similar folders) is a typical way of structuring a Unity project.</span></span>

    7.  <span data-ttu-id="a40a4-196">Les paramètres restants, dans *paramètres de build*, doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="a40a4-196">The remaining settings, in *Build Settings*, should be left as default for now.</span></span>

6.  <span data-ttu-id="a40a4-197">Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* .</span><span class="sxs-lookup"><span data-stu-id="a40a4-197">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span> 

    ![](images/AzureLabs-Lab311-16.png)

7. <span data-ttu-id="a40a4-198">Dans ce volet, quelques paramètres doivent être vérifiés:</span><span class="sxs-lookup"><span data-stu-id="a40a4-198">In this panel, a few settings need to be verified:</span></span>

    1. <span data-ttu-id="a40a4-199">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="a40a4-199">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="a40a4-200">**Scripts** La **version du runtime** doit être **expérimentale** (.net 4,6 équivalent), qui déclenchera un redémarrage de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="a40a4-200">**Scripting** **Runtime Version** should be **Experimental** (.NET 4.6 Equivalent), which will trigger a need to restart the Editor.</span></span>

        2. <span data-ttu-id="a40a4-201">Le **backend de script** doit être **.net**</span><span class="sxs-lookup"><span data-stu-id="a40a4-201">**Scripting Backend** should be **.NET**</span></span>

        3. <span data-ttu-id="a40a4-202">Le **niveau de compatibilité** de l’API doit être **.net 4,6**</span><span class="sxs-lookup"><span data-stu-id="a40a4-202">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![](images/AzureLabs-Lab311-17.png)

    2.  <span data-ttu-id="a40a4-203">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:</span><span class="sxs-lookup"><span data-stu-id="a40a4-203">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="a40a4-204">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="a40a4-204">**InternetClient**</span></span>

            ![](images/AzureLabs-Lab311-18.png)

    3.  <span data-ttu-id="a40a4-205">Plus bas dans le panneau, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="a40a4-205">Further down the panel, in **XR Settings** (found below **Publish Settings**), check **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![](images/AzureLabs-Lab311-19.png)

8.  <span data-ttu-id="a40a4-206">De retour dans les *paramètres de build*, les *projets C# Unity* ne sont plus grisés. Cochez la case en regard de cette option.</span><span class="sxs-lookup"><span data-stu-id="a40a4-206">Back in *Build Settings*, *Unity C# Projects* is no longer greyed out; check the checkbox next to this.</span></span>

9.  <span data-ttu-id="a40a4-207">Fermez la fenêtre *paramètres de build* .</span><span class="sxs-lookup"><span data-stu-id="a40a4-207">Close the *Build Settings* window.</span></span>

10.  <span data-ttu-id="a40a4-208">Enregistrez votre scène et votre projet (**fichier** > **Save scenes/file** > **Save Project**).</span><span class="sxs-lookup"><span data-stu-id="a40a4-208">Save your scene and project (**FILE** > **SAVE SCENES / FILE** > **SAVE PROJECT**).</span></span>

## <a name="chapter-3---import-libraries-in-unity"></a><span data-ttu-id="a40a4-209">Chapitre 3-bibliothèques d’importation dans Unity</span><span class="sxs-lookup"><span data-stu-id="a40a4-209">Chapter 3 - Import Libraries in Unity</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a40a4-210">Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce fichier [Azure-Mr-311. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20311%20-%20Microsoft%20Graph/Azure-MR-311.unitypackage), à l’importer dans votre projet en tant que [**package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis à passer au [Chapitre 5. ](#chapter-5---create-meetingsui-class).</span><span class="sxs-lookup"><span data-stu-id="a40a4-210">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to download this [Azure-MR-311.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20311%20-%20Microsoft%20Graph/Azure-MR-311.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 5](#chapter-5---create-meetingsui-class).</span></span>

<span data-ttu-id="a40a4-211">Pour utiliser *Microsoft Graph* dans Unity, vous devez utiliser la dll **Microsoft. Identity. client** .</span><span class="sxs-lookup"><span data-stu-id="a40a4-211">To use *Microsoft Graph* within Unity you need to make use of the  **Microsoft.Identity.Client** DLL.</span></span> <span data-ttu-id="a40a4-212">Il est toutefois possible d’utiliser le kit de développement logiciel (SDK) Microsoft Graph, mais il nécessite l’ajout d’un package NuGet après la génération du projet Unity (c’est-à-dire la modification du projet après la génération).</span><span class="sxs-lookup"><span data-stu-id="a40a4-212">It is possible to use the Microsoft Graph SDK, however, it will require the addition of a NuGet package after you build the Unity project (meaning editing the project post-build).</span></span> <span data-ttu-id="a40a4-213">Il est considéré comme plus simple d’importer les dll requises directement dans Unity.</span><span class="sxs-lookup"><span data-stu-id="a40a4-213">It is considered simpler to import the required DLLs directly into Unity.</span></span>

> [!NOTE]
> <span data-ttu-id="a40a4-214">Il existe actuellement un problème connu dans Unity qui nécessite que les plug-ins soient reconfigurés après l’importation.</span><span class="sxs-lookup"><span data-stu-id="a40a4-214">There is currently a known issue in Unity which requires plugins to be reconfigured after import.</span></span> <span data-ttu-id="a40a4-215">Ces étapes (4-7 dans cette section) ne sont plus nécessaires une fois que le bogue a été résolu.</span><span class="sxs-lookup"><span data-stu-id="a40a4-215">These steps (4 - 7 in this section) will no longer be required after the bug has been resolved.</span></span>

<span data-ttu-id="a40a4-216">Pour importer *Microsoft Graph* dans votre propre projet, [Téléchargez le fichier MSGraph_LabPlugins. zip](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20311%20-%20Microsoft%20Graph/MSGraph_LabPlugins.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="a40a4-216">To import *Microsoft Graph* into your own project, [download the MSGraph_LabPlugins.zip file](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20311%20-%20Microsoft%20Graph/MSGraph_LabPlugins.unitypackage).</span></span> <span data-ttu-id="a40a4-217">Ce package a été créé avec les versions des bibliothèques qui ont été testées.</span><span class="sxs-lookup"><span data-stu-id="a40a4-217">This package has been created with versions of the libraries that have been tested.</span></span>

<span data-ttu-id="a40a4-218">Si vous souhaitez en savoir plus sur l’ajout de dll personnalisées à votre projet Unity, [suivez ce lien](https://docs.unity3d.com/Manual/UsingDLL.html).</span><span class="sxs-lookup"><span data-stu-id="a40a4-218">If you wish to know more about how to add custom DLLs to your Unity project, [follow this link](https://docs.unity3d.com/Manual/UsingDLL.html).</span></span>

<span data-ttu-id="a40a4-219">Pour importer le package:</span><span class="sxs-lookup"><span data-stu-id="a40a4-219">To import the package:</span></span>

1.  <span data-ttu-id="a40a4-220">Ajoutez le package Unity à Unity à > l’aide de l’option de menu package d'**importation de packages** > **personnalisés** .</span><span class="sxs-lookup"><span data-stu-id="a40a4-220">Add the Unity Package to Unity by using the **Assets** > **Import Package** > **Custom Package** menu option.</span></span> <span data-ttu-id="a40a4-221">Sélectionnez le package que vous venez de télécharger.</span><span class="sxs-lookup"><span data-stu-id="a40a4-221">Select the package you just downloaded.</span></span>

2.  <span data-ttu-id="a40a4-222">Dans la zone **importer le package Unity** qui s’affiche, vérifiez que tous les plug- **ins** sous (et y compris) sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="a40a4-222">In the **Import Unity Package** box that pops up, ensure everything under (and including) **Plugins** is selected.</span></span>

    ![](images/AzureLabs-Lab311-20.png)

3.  <span data-ttu-id="a40a4-223">Cliquez sur le bouton **Importer** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="a40a4-223">Click the **Import** button to add the items to your project.</span></span>

4.  <span data-ttu-id="a40a4-224">Accédez au dossier **MSGraph** sous **plug-ins** dans le *panneau Projet* et sélectionnez le plug-in appelé **Microsoft. Identity. client**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-224">Go to the **MSGraph** folder under **Plugins** in the *Project Panel* and select the plugin called **Microsoft.Identity.Client**.</span></span>

    ![](images/AzureLabs-Lab311-21.png)

5.  <span data-ttu-id="a40a4-225">Une fois *le plug-in* sélectionné, assurez-vous que **toutes les plateformes** sont décochées, vérifiez que **WSAPlayer** est également désactivé, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-225">With the *plugin* selected, ensure that **Any Platform** is unchecked, then ensure that **WSAPlayer** is also unchecked, then click **Apply**.</span></span> <span data-ttu-id="a40a4-226">Cela vous permet de vérifier que les fichiers sont correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="a40a4-226">This is just to confirm that the files are configured correctly.</span></span>

    ![](images/AzureLabs-Lab311-22.png)

    > [!NOTE] 
    > <span data-ttu-id="a40a4-227">Le marquage de ces plug-ins permet de les configurer pour qu’ils soient utilisés uniquement dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="a40a4-227">Marking these plugins configures them to only be used in the Unity Editor.</span></span> <span data-ttu-id="a40a4-228">Il existe un ensemble différent de dll dans le dossier WSA qui sera utilisé une fois que le projet est exporté d’Unity en tant qu’application Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="a40a4-228">There are a different set of DLLs in the WSA folder which will be used after the project is exported from Unity as a Universal Windows Application.</span></span>

6.  <span data-ttu-id="a40a4-229">Ensuite, vous devez ouvrir le dossier **WSA** , dans le dossier **MSGraph** .</span><span class="sxs-lookup"><span data-stu-id="a40a4-229">Next, you need to open the **WSA** folder, within the **MSGraph** folder.</span></span> <span data-ttu-id="a40a4-230">Vous verrez une copie du même fichier que celui que vous venez de configurer.</span><span class="sxs-lookup"><span data-stu-id="a40a4-230">You will see a copy of the same file you just configured.</span></span> <span data-ttu-id="a40a4-231">Sélectionnez le fichier, puis dans l’inspecteur:</span><span class="sxs-lookup"><span data-stu-id="a40a4-231">Select the file, and then in the inspector:</span></span>

    -   <span data-ttu-id="a40a4-232">Vérifiez que **toutes les plateformes** sont désactivéeset que **seul** **WSAPlayer** est **activé**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-232">ensure that **Any Platform** is **unchecked**, and that **only** **WSAPlayer** is **checked**.</span></span>

    -   <span data-ttu-id="a40a4-233">Vérifiez que le **Kit de développement logiciel (SDK)** a la valeur **UWP**et que le **serveur principal de script** est défini sur le **point net**</span><span class="sxs-lookup"><span data-stu-id="a40a4-233">Ensure **SDK** is set to **UWP**, and **Scripting Backend** is set to **Dot Net**</span></span>

    -   <span data-ttu-id="a40a4-234">Vérifiez que l’option **ne pas traiter** est **cochée**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-234">Ensure that **Don't process** is **checked**.</span></span>

        ![](images/AzureLabs-Lab311-23.png)

7.  <span data-ttu-id="a40a4-235">Cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-235">Click **Apply**.</span></span>

## <a name="chapter-4---camera-setup"></a><span data-ttu-id="a40a4-236">Chapitre 4-Configuration de l’appareil photo</span><span class="sxs-lookup"><span data-stu-id="a40a4-236">Chapter 4 - Camera Setup</span></span>

<span data-ttu-id="a40a4-237">Au cours de ce chapitre, vous allez configurer la caméra principale de votre scène:</span><span class="sxs-lookup"><span data-stu-id="a40a4-237">During this Chapter you will set up the Main Camera of your scene:</span></span>

1.  <span data-ttu-id="a40a4-238">Dans le *panneau hiérarchie*, sélectionnez l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-238">In the *Hierarchy Panel*, select the **Main Camera**.</span></span>

2.  <span data-ttu-id="a40a4-239">Une fois sélectionné, vous pouvez voir tous les composants de la **caméra principale** dans le panneau *inspecteur* .</span><span class="sxs-lookup"><span data-stu-id="a40a4-239">Once selected, you will be able to see all the components of the **Main Camera** in the *Inspector* panel.</span></span>

    1.  <span data-ttu-id="a40a4-240">L' **objet Camera** doit être nommé **Camera main** (Notez l’orthographe!)</span><span class="sxs-lookup"><span data-stu-id="a40a4-240">The **Camera object** must be named **Main Camera** (note the spelling!)</span></span>

    2.  <span data-ttu-id="a40a4-241">La balise principale de l’appareil photo doit être définie sur **MainCamera** (Notez l’orthographe!)</span><span class="sxs-lookup"><span data-stu-id="a40a4-241">The Main Camera **Tag** must be set to **MainCamera** (note the spelling!)</span></span>

    3.  <span data-ttu-id="a40a4-242">Vérifiez que la **position** de la transformation est définie sur **0, 0,** 0</span><span class="sxs-lookup"><span data-stu-id="a40a4-242">Make sure the **Transform Position** is set to **0, 0, 0**</span></span>

    4.  <span data-ttu-id="a40a4-243">Définir des **indicateurs clairs** sur **couleur unie**</span><span class="sxs-lookup"><span data-stu-id="a40a4-243">Set **Clear Flags** to **Solid Color**</span></span>

    5.  <span data-ttu-id="a40a4-244">Définir la **couleur d’arrière-plan** du composant Camera sur **Black, alpha 0** **(code hexadécimal: #00000000)**</span><span class="sxs-lookup"><span data-stu-id="a40a4-244">Set the **Background Color** of the Camera Component to **Black, Alpha 0** **(Hex Code: #00000000)**</span></span>

        ![](images/AzureLabs-Lab311-24.png)

3.  <span data-ttu-id="a40a4-245">La dernière structure de l’objet dans le volet de la *hiérarchie* doit être similaire à celle illustrée dans l’image ci-dessous:</span><span class="sxs-lookup"><span data-stu-id="a40a4-245">The final object structure in the *Hierarchy Panel* should be like the one shown in the image below:</span></span>

    ![](images/AzureLabs-Lab311-25.png)

## <a name="chapter-5---create-meetingsui-class"></a><span data-ttu-id="a40a4-246">Chapitre 5-créer une classe MeetingsUI</span><span class="sxs-lookup"><span data-stu-id="a40a4-246">Chapter 5 - Create MeetingsUI class</span></span>

<span data-ttu-id="a40a4-247">Le premier script que vous devez créer est **MeetingsUI**, qui est responsable de l’hébergement et du remplissage de l’interface utilisateur de l’application (message de bienvenue, instructions et détails des réunions).</span><span class="sxs-lookup"><span data-stu-id="a40a4-247">The first script you need to create is **MeetingsUI**, which is responsible for hosting and populating the UI of the application (welcome message, instructions and the meetings details).</span></span>

<span data-ttu-id="a40a4-248">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="a40a4-248">To create this class:</span></span>

1.  <span data-ttu-id="a40a4-249">Cliquez avec le bouton droit sur le dossier **ressources** dans le *panneau Projet*, puis sélectionnez **créer** > un**dossier**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-249">Right-click on the **Assets** folder in the *Project Panel*, then select **Create** > **Folder**.</span></span> <span data-ttu-id="a40a4-250">Nommez le dossier **scripts**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-250">Name the folder **Scripts**.</span></span>

    ![](images/AzureLabs-Lab311-26.png)
    ![](images/AzureLabs-Lab311-27.png)

2.  <span data-ttu-id="a40a4-251">Ouvrez le dossier **scripts** , puis, dans ce dossier, cliquez avec le bouton droit sur **créer**  >   **C# un script**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-251">Open the **Scripts** folder then, within that folder, right-click, **Create** > **C# Script**.</span></span> <span data-ttu-id="a40a4-252">Nommez le script **MeetingsUI.**</span><span class="sxs-lookup"><span data-stu-id="a40a4-252">Name the script **MeetingsUI.**</span></span>

    ![](images/AzureLabs-Lab311-28.png)

3.  <span data-ttu-id="a40a4-253">Double-cliquez sur le nouveau script **MeetingsUI** pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="a40a4-253">Double-click on the new **MeetingsUI** script to open it with *Visual Studio*.</span></span>

4.  <span data-ttu-id="a40a4-254">Insérez les espaces de noms suivants:</span><span class="sxs-lookup"><span data-stu-id="a40a4-254">Insert the following namespaces:</span></span>

    ```csharp
    using System;
    using UnityEngine;
    ```

5.  <span data-ttu-id="a40a4-255">À l’intérieur de la classe, insérez les variables suivantes:</span><span class="sxs-lookup"><span data-stu-id="a40a4-255">Inside the class insert the following variables:</span></span>

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

6.  <span data-ttu-id="a40a4-256">Remplacez ensuite la méthode **Start ()** et ajoutez une méthode **éveillé ()** .</span><span class="sxs-lookup"><span data-stu-id="a40a4-256">Then replace the **Start()** method and add an **Awake()** method.</span></span> <span data-ttu-id="a40a4-257">Ils sont appelés lorsque la classe est initialisée:</span><span class="sxs-lookup"><span data-stu-id="a40a4-257">These will be called when the class initializes:</span></span>

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

7.  <span data-ttu-id="a40a4-258">Ajoutez les méthodes responsables de la création de l' *interface utilisateur des réunions* et remplissez-la avec les réunions en cours lorsque vous y êtes invité:</span><span class="sxs-lookup"><span data-stu-id="a40a4-258">Add the methods responsible for creating the *Meetings UI* and populate it with the current meetings when requested:</span></span>

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

8. <span data-ttu-id="a40a4-259">**Supprimez** la méthode **Update ()** et **Enregistrez vos modifications** dans Visual Studio avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="a40a4-259">**Delete** the **Update()** method, and **save your changes** in Visual Studio before returning to Unity.</span></span> 

## <a name="chapter-6---create-the-graph-class"></a><span data-ttu-id="a40a4-260">Chapitre 6-créer la classe Graph</span><span class="sxs-lookup"><span data-stu-id="a40a4-260">Chapter 6 - Create the Graph class</span></span>

<span data-ttu-id="a40a4-261">Le script suivant à créer est le script **Graph** .</span><span class="sxs-lookup"><span data-stu-id="a40a4-261">The next script to create is the **Graph** script.</span></span> <span data-ttu-id="a40a4-262">Ce script est chargé d’effectuer les appels pour authentifier l’utilisateur et de récupérer les réunions planifiées pour le jour actuel à partir du calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a40a4-262">This script is responsible for making the calls to authenticate the user and retrieve the scheduled meetings for the current day from the user's calendar.</span></span>

<span data-ttu-id="a40a4-263">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="a40a4-263">To create this class:</span></span>

1.  <span data-ttu-id="a40a4-264">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="a40a4-264">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="a40a4-265">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer**  >   **C# un script**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-265">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="a40a4-266">Nommez le **graphique**de script.</span><span class="sxs-lookup"><span data-stu-id="a40a4-266">Name the script **Graph**.</span></span>

3.  <span data-ttu-id="a40a4-267">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a40a4-267">Double-click on the script to open it with Visual Studio.</span></span>

4.  <span data-ttu-id="a40a4-268">Insérez les espaces de noms suivants:</span><span class="sxs-lookup"><span data-stu-id="a40a4-268">Insert the following namespaces:</span></span>

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
    > <span data-ttu-id="a40a4-269">Vous remarquerez que certaines parties du code de ce script sont encapsulées autour des [directives](https://docs.unity3d.com/Manual/PlatformDependentCompilation.html)de précompilation. cela permet d’éviter les problèmes liés aux bibliothèques lors de la génération de la solution Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a40a4-269">You will notice that parts of the code in this script are wrapped around [Precompile Directives](https://docs.unity3d.com/Manual/PlatformDependentCompilation.html), this is to avoid issues with the libraries when building the Visual Studio Solution.</span></span>

5.  <span data-ttu-id="a40a4-270">Supprimez les méthodes **Start ()** et **Update ()** , car elles ne seront pas utilisées.</span><span class="sxs-lookup"><span data-stu-id="a40a4-270">Delete the **Start()** and **Update()** methods, as they will not be used.</span></span>

6.  <span data-ttu-id="a40a4-271">En dehors de la classe **Graph** , insérez les objets suivants, qui sont nécessaires pour désérialiser l’objet JSON représentant les réunions planifiées quotidiennement:</span><span class="sxs-lookup"><span data-stu-id="a40a4-271">Outside the **Graph** class, insert the following objects, which are necessary to deserialize the JSON object representing the daily scheduled meetings:</span></span>

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

7.  <span data-ttu-id="a40a4-272">À l’intérieur de la classe **Graph** , ajoutez les variables suivantes:</span><span class="sxs-lookup"><span data-stu-id="a40a4-272">Inside the **Graph** class, add the following variables:</span></span>

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
    > <span data-ttu-id="a40a4-273">Modifiez la valeur **AppID** pour qu’elle soit l' **ID d’application** que vous avez noté au  **[Chapitre 1](#chapter-1---create-your-app-in-the-application-registration-portal), étape 4**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-273">Change the **appId** value to be the **App Id** that you have noted in **[Chapter 1](#chapter-1---create-your-app-in-the-application-registration-portal), step 4**.</span></span> <span data-ttu-id="a40a4-274">Cette valeur doit être identique à celle affichée dans le **portail d’inscription des applications,** dans la page d’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="a40a4-274">This value should be the same as that displayed in the **Application Registration Portal,** in your application registration page.</span></span>

8.  <span data-ttu-id="a40a4-275">Dans la classe **Graph** , ajoutez les méthodes **SignInAsync ()** et **AquireTokenAsync ()** , qui invitent l’utilisateur à insérer les informations d’identification de connexion.</span><span class="sxs-lookup"><span data-stu-id="a40a4-275">Within the **Graph** class, add the methods **SignInAsync()** and **AquireTokenAsync()**, that will prompt the user to insert the log-in credentials.</span></span>

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

9.  <span data-ttu-id="a40a4-276">Ajoutez les deux méthodes suivantes:</span><span class="sxs-lookup"><span data-stu-id="a40a4-276">Add the following two methods:</span></span>

    1.  <span data-ttu-id="a40a4-277">**BuildTodayCalendarEndpoint ()** , qui génère l’URI spécifiant le jour et l’intervalle de temps pendant lesquels les réunions planifiées sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="a40a4-277">**BuildTodayCalendarEndpoint()**, which builds the URI specifying the day, and time span, in which the scheduled meetings are retrieved.</span></span>

    2.  <span data-ttu-id="a40a4-278">**ListMeetingsAsync ()** , qui demande les réunions planifiées à partir de *Microsoft Graph*.</span><span class="sxs-lookup"><span data-stu-id="a40a4-278">**ListMeetingsAsync()**, which requests the scheduled meetings from *Microsoft Graph*.</span></span>

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

10. <span data-ttu-id="a40a4-279">Vous avez maintenant terminé le script **Graph** .</span><span class="sxs-lookup"><span data-stu-id="a40a4-279">You have now completed the **Graph** script.</span></span> <span data-ttu-id="a40a4-280">**Enregistrez vos modifications** dans Visual Studio avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="a40a4-280">**Save your changes** in Visual Studio before returning to Unity.</span></span>

## <a name="chapter-7---create-the-gazeinput-script"></a><span data-ttu-id="a40a4-281">Chapitre 7-créer le script GazeInput</span><span class="sxs-lookup"><span data-stu-id="a40a4-281">Chapter 7 - Create the GazeInput script</span></span>

<span data-ttu-id="a40a4-282">Vous allez maintenant créer le **GazeInput**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-282">You will now create the **GazeInput**.</span></span> <span data-ttu-id="a40a4-283">Cette classe gère et effectue le suivi du point de regard de l’utilisateur à l’aide d’un **Raycast** provenant de la **caméra principale**, en projetant vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="a40a4-283">This class handles and keeps track of the user's gaze, using a **Raycast** coming from the **Main Camera**, projecting forward.</span></span>

<span data-ttu-id="a40a4-284">Pour créer le script:</span><span class="sxs-lookup"><span data-stu-id="a40a4-284">To create the script:</span></span>

1.  <span data-ttu-id="a40a4-285">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="a40a4-285">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="a40a4-286">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer**  >   **C# un script**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-286">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="a40a4-287">Nommez le script **GazeInput**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-287">Name the script **GazeInput**.</span></span>

3.  <span data-ttu-id="a40a4-288">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a40a4-288">Double-click on the script to open it with Visual Studio.</span></span>

4.  <span data-ttu-id="a40a4-289">Modifier le code des espaces de noms pour correspondre à celui ci-dessous, ainsi que l’ajout de la ' **\[System.Serializable\]** ' balise ci-dessus votre **GazeInput** classe, afin qu’il puisse être sérialisé :</span><span class="sxs-lookup"><span data-stu-id="a40a4-289">Change the namespaces code to match the one below, along with adding the '**\[System.Serializable\]**' tag above your **GazeInput** class, so that it can be serialized:</span></span>

    ```csharp
    using UnityEngine;

    /// <summary>
    /// Class responsible for the User's Gaze interactions
    /// </summary>
    [System.Serializable]
    public class GazeInput : MonoBehaviour
    {
    ```

5.  <span data-ttu-id="a40a4-290">À l’intérieur de la classe **GazeInput** , ajoutez les variables suivantes:</span><span class="sxs-lookup"><span data-stu-id="a40a4-290">Inside the **GazeInput** class, add the following variables:</span></span>

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

6.  <span data-ttu-id="a40a4-291">Ajoutez la méthode **CreateCursor ()** pour créer le curseur HoloLens dans la scène, puis appelez la méthode à partir de la méthode **Start ()** :</span><span class="sxs-lookup"><span data-stu-id="a40a4-291">Add the **CreateCursor()** method to create the HoloLens cursor in the scene, and call the method from the **Start()** method:</span></span>

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

7.  <span data-ttu-id="a40a4-292">Les méthodes suivantes activent le point de Raycast de regard et assurent le suivi des objets ayant le focus.</span><span class="sxs-lookup"><span data-stu-id="a40a4-292">The following methods enable the gaze Raycast and keep track of the focused objects.</span></span>

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

8.  <span data-ttu-id="a40a4-293">**Enregistrez vos modifications** dans Visual Studio avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="a40a4-293">**Save your changes** in Visual Studio before returning to Unity.</span></span>

## <a name="chapter-8---create-the-interactions-class"></a><span data-ttu-id="a40a4-294">Chapitre 8-créer la classe interactions</span><span class="sxs-lookup"><span data-stu-id="a40a4-294">Chapter 8 - Create the Interactions class</span></span>

<span data-ttu-id="a40a4-295">Vous devez maintenant créer le script **interactions** , qui est chargé des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="a40a4-295">You will now need to create the **Interactions** script, which is responsible for:</span></span>

-   <span data-ttu-id="a40a4-296">Gestion de l’interaction du **robinet** et du point d’interconnexion de l' **appareil photo**, qui permet à l’utilisateur d’interagir avec le «bouton» du journal dans la scène.</span><span class="sxs-lookup"><span data-stu-id="a40a4-296">Handling the **Tap** interaction and the **Camera Gaze**, which enables the user to interact with the log in "button" in the scene.</span></span>

-   <span data-ttu-id="a40a4-297">Création de l’objet de connexion «Button» dans la scène pour l’utilisateur avec lequel interagir.</span><span class="sxs-lookup"><span data-stu-id="a40a4-297">Creating the log in "button" object in the scene for the user to interact with.</span></span>

<span data-ttu-id="a40a4-298">Pour créer le script:</span><span class="sxs-lookup"><span data-stu-id="a40a4-298">To create the script:</span></span>

1.  <span data-ttu-id="a40a4-299">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="a40a4-299">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="a40a4-300">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer**  >   **C# un script**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-300">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="a40a4-301">Nommez les **interactions**de script.</span><span class="sxs-lookup"><span data-stu-id="a40a4-301">Name the script **Interactions**.</span></span>

3.  <span data-ttu-id="a40a4-302">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a40a4-302">Double-click on the script to open it with Visual Studio.</span></span>

4.  <span data-ttu-id="a40a4-303">Insérez les espaces de noms suivants:</span><span class="sxs-lookup"><span data-stu-id="a40a4-303">Insert the following namespaces:</span></span>

    ```csharp
    using UnityEngine;
    using UnityEngine.XR.WSA.Input;
    ```

5.  <span data-ttu-id="a40a4-304">Remplacez l’héritage de la classe **interaction** par *monocomportement* par **GazeInput**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-304">Change the inheritance of the **Interaction** class from *MonoBehaviour* to **GazeInput**.</span></span>

    <span data-ttu-id="a40a4-305">~~Interactions de classes publiques: MonoBehaviour~~</span><span class="sxs-lookup"><span data-stu-id="a40a4-305">~~public class Interactions : MonoBehaviour~~</span></span>

    ```csharp
    public class Interactions : GazeInput
    ```

6.  <span data-ttu-id="a40a4-306">À l’intérieur de la classe d' **interaction** , insérez la variable suivante:</span><span class="sxs-lookup"><span data-stu-id="a40a4-306">Inside the **Interaction** class insert the following variable:</span></span>

    ```csharp
        /// <summary>
        /// Allows input recognition with the HoloLens
        /// </summary>
        private GestureRecognizer _gestureRecognizer;
    ```

7.  <span data-ttu-id="a40a4-307">Remplacez la méthode **Start** . Notez qu’il s’agit d’une méthode override, qui appelle la méthode de la classe de pointage «base».</span><span class="sxs-lookup"><span data-stu-id="a40a4-307">Replace the **Start** method; notice it is an override method, which calls the 'base' Gaze class method.</span></span> <span data-ttu-id="a40a4-308">**Start ()** est appelé lors de l’initialisation de la classe, de l’inscription à la reconnaissance d’entrée et de la création du *bouton* de connexion dans la scène:</span><span class="sxs-lookup"><span data-stu-id="a40a4-308">**Start()** will be called when the class initializes, registering for input recognition and creating the sign in *button* in the scene:</span></span>

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

8.  <span data-ttu-id="a40a4-309">Ajoutez la méthode **CreateSignInButton ()** , qui instancie le *bouton* de connexion dans la scène et définit ses propriétés:</span><span class="sxs-lookup"><span data-stu-id="a40a4-309">Add the **CreateSignInButton()** method, which will instantiate the sign in *button* in the scene and set its properties:</span></span>

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

9.  <span data-ttu-id="a40a4-310">Ajoutez la méthode **GestureRecognizer_Tapped ()** , qui répond à l’événement *Tap* User.</span><span class="sxs-lookup"><span data-stu-id="a40a4-310">Add the **GestureRecognizer_Tapped()** method, which be respond for the *Tap* user event.</span></span>

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

10. <span data-ttu-id="a40a4-311">**Supprimez** la méthode **Update ()** , puis **Enregistrez vos modifications** dans Visual Studio avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="a40a4-311">**Delete** the **Update()** method, and then **save your changes** in Visual Studio before returning to Unity.</span></span>

## <a name="chapter-9---set-up-the-script-references"></a><span data-ttu-id="a40a4-312">Chapitre 9-configurer les références de script</span><span class="sxs-lookup"><span data-stu-id="a40a4-312">Chapter 9 - Set up the script references</span></span>

<span data-ttu-id="a40a4-313">Dans ce chapitre, vous devez placer le script **interactions** sur l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-313">In this Chapter you need to place the **Interactions** script onto the **Main Camera**.</span></span> <span data-ttu-id="a40a4-314">Ce script gère alors le placement des autres scripts là où ils doivent être.</span><span class="sxs-lookup"><span data-stu-id="a40a4-314">That script will then handle placing the other scripts where they need to be.</span></span>

-  <span data-ttu-id="a40a4-315">Dans le dossier **scripts** du *panneau Projet*, faites glisser les **interactions** de script vers l’objet **caméra principale** , comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a40a4-315">From the **Scripts** folder in the *Project Panel*, drag the script **Interactions** to the **Main Camera** object, as pictured below.</span></span>

    ![](images/AzureLabs-Lab311-29.png)

## <a name="chapter-10---setting-up-the-tag"></a><span data-ttu-id="a40a4-316">Chapitre 10-configuration de la balise</span><span class="sxs-lookup"><span data-stu-id="a40a4-316">Chapter 10 - Setting up the Tag</span></span>

<span data-ttu-id="a40a4-317">Le code qui gère le point de regard utilise la balise **SignInButton** pour identifier l’objet avec lequel l’utilisateur interagit pour se connecter à *Microsoft Graph*.</span><span class="sxs-lookup"><span data-stu-id="a40a4-317">The code handling the gaze will make use of the Tag **SignInButton** to identify which object the user will interact with to sign-in to *Microsoft Graph*.</span></span>

<span data-ttu-id="a40a4-318">Pour créer la balise:</span><span class="sxs-lookup"><span data-stu-id="a40a4-318">To create the Tag:</span></span>

1.  <span data-ttu-id="a40a4-319">Dans l’éditeur Unity, cliquez sur la **caméra principale** dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="a40a4-319">In the Unity Editor click on the **Main Camera** in the *Hierarchy Panel*.</span></span>

2.  <span data-ttu-id="a40a4-320">Dans le *volet* de l’inspecteur, cliquez sur la balise **MainCamera** pour ouvrir une liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="a40a4-320">In the *Inspector Panel* click on the **MainCamera** *Tag* to open a drop-down list.</span></span> <span data-ttu-id="a40a4-321">Cliquez sur **Ajouter une étiquette...**</span><span class="sxs-lookup"><span data-stu-id="a40a4-321">Click on **Add Tag...**</span></span>

    ![](images/AzureLabs-Lab311-30.png)

3.  <span data-ttu-id="a40a4-322">Cliquez sur le **+** bouton.</span><span class="sxs-lookup"><span data-stu-id="a40a4-322">Click on the **+** button.</span></span>

    ![](images/AzureLabs-Lab311-31.png)

4.  <span data-ttu-id="a40a4-323">Écrivez le nom de la balise en tant que **SignInButton** , puis cliquez sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="a40a4-323">Write the Tag name as **SignInButton** and click Save.</span></span>

    ![](images/AzureLabs-Lab311-32.png)

## <a name="chapter-11---build-the-unity-project-to-uwp"></a><span data-ttu-id="a40a4-324">Chapitre 11-créer le projet Unity dans UWP</span><span class="sxs-lookup"><span data-stu-id="a40a4-324">Chapter 11 - Build the Unity project to UWP</span></span>

<span data-ttu-id="a40a4-325">Tout ce qui est nécessaire pour la section Unity de ce projet est maintenant terminé. il est donc temps de la générer à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="a40a4-325">Everything needed for the Unity section of this project has now been completed, so it is time to build it from Unity.</span></span>

1.  <span data-ttu-id="a40a4-326">Accédez à *les paramètres de génération* (**fichier*>*Build paramètres**).</span><span class="sxs-lookup"><span data-stu-id="a40a4-326">Navigate to *Build Settings* (\**File* > \*Build Settings\*\*).</span></span>

    ![](images/AzureLabs-Lab311-33.png)

2.  <span data-ttu-id="a40a4-327">Si ce n’est pas déjà fait, cochez les **projets Unity C\#** .</span><span class="sxs-lookup"><span data-stu-id="a40a4-327">If not already, tick **Unity C\# Projects**.</span></span>

3.  <span data-ttu-id="a40a4-328">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-328">Click **Build**.</span></span> <span data-ttu-id="a40a4-329">Unity lance une fenêtre de l' **Explorateur de fichiers** , dans laquelle vous devez créer, puis sélectionner un dossier dans lequel générer l’application.</span><span class="sxs-lookup"><span data-stu-id="a40a4-329">Unity will launch a **File Explorer** window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="a40a4-330">Créez ce dossier maintenant, puis nommez-le **application**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-330">Create that folder now, and name it **App**.</span></span> <span data-ttu-id="a40a4-331">Ensuite, avec le dossier d' **application** sélectionné, cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-331">Then with the **App** folder selected, click **Select Folder**.</span></span>

4.  <span data-ttu-id="a40a4-332">Unity commence à générer votre projet dans le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="a40a4-332">Unity will begin building your project to the **App** folder.</span></span>

5.  <span data-ttu-id="a40a4-333">Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).</span><span class="sxs-lookup"><span data-stu-id="a40a4-333">Once Unity has finished building (it might take some time), it will open a **File Explorer** window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

## <a name="chapter-12---deploy-to-hololens"></a><span data-ttu-id="a40a4-334">Chapitre 12-déployer dans HoloLens</span><span class="sxs-lookup"><span data-stu-id="a40a4-334">Chapter 12 - Deploy to HoloLens</span></span>

<span data-ttu-id="a40a4-335">Pour effectuer un déploiement sur HoloLens:</span><span class="sxs-lookup"><span data-stu-id="a40a4-335">To deploy on HoloLens:</span></span>

1.  <span data-ttu-id="a40a4-336">Vous aurez besoin de l’adresse IP de votre HoloLens (pour le déploiement à distance) et vérifiez que votre HoloLens est en **mode développeur.**</span><span class="sxs-lookup"><span data-stu-id="a40a4-336">You will need the IP Address of your HoloLens (for Remote Deploy), and to ensure your HoloLens is in **Developer Mode.**</span></span> <span data-ttu-id="a40a4-337">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="a40a4-337">To do this:</span></span>

    1.  <span data-ttu-id="a40a4-338">Tout en portant votre HoloLens, ouvrez les **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-338">Whilst wearing your HoloLens, open the **Settings**.</span></span>

    2.  <span data-ttu-id="a40a4-339">Accéder au **réseau &**  > **Options avancées** **de Wi-Fi** > Internet</span><span class="sxs-lookup"><span data-stu-id="a40a4-339">Go to **Network & Internet** > **Wi-Fi** > **Advanced Options**</span></span>

    3.  <span data-ttu-id="a40a4-340">Notez l’adresse **IPv4** .</span><span class="sxs-lookup"><span data-stu-id="a40a4-340">Note the **IPv4** address.</span></span>

    4.  <span data-ttu-id="a40a4-341">Ensuite, revenez aux **paramètres**, puis pour **mettre à jour & sécurité** > **pour les développeurs**</span><span class="sxs-lookup"><span data-stu-id="a40a4-341">Next, navigate back to **Settings**, and then to **Update & Security** > **For Developers**</span></span>

    5.  <span data-ttu-id="a40a4-342">Définissez **le mode développeur sur**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-342">Set **Developer Mode On**.</span></span>

2.  <span data-ttu-id="a40a4-343">Accédez à votre nouvelle build Unity (le dossier de l' **application** ) et ouvrez le fichier solution avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-343">Navigate to your new Unity build (the **App** folder) and open the solution file with **Visual Studio**.</span></span>

3.  <span data-ttu-id="a40a4-344">Dans la **configuration** de lasolution, sélectionnez Déboguer.</span><span class="sxs-lookup"><span data-stu-id="a40a4-344">In the **Solution Configuration** select **Debug**.</span></span>

4.  <span data-ttu-id="a40a4-345">Dans la **plateforme**de la solution, sélectionnez **x86, ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="a40a4-345">In the **Solution Platform**, select **x86, Remote Machine**.</span></span> <span data-ttu-id="a40a4-346">Vous serez invité à insérer l' **adresse IP** d’un périphérique distant (le HoloLens, dans ce cas, que vous avez noté).</span><span class="sxs-lookup"><span data-stu-id="a40a4-346">You will be prompted to insert the **IP address** of a remote device (the HoloLens, in this case, which you noted).</span></span>

    ![](images/AzureLabs-Lab311-34.png)

5.  <span data-ttu-id="a40a4-347">Accédez au menu **générer** , puis cliquez sur **déployer la solution** pour chargement l’application à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="a40a4-347">Go to **Build** menu and click on **Deploy Solution** to sideload the application to your HoloLens.</span></span>

6.  <span data-ttu-id="a40a4-348">Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prête à être lancée.</span><span class="sxs-lookup"><span data-stu-id="a40a4-348">Your app should now appear in the list of installed apps on your HoloLens, ready to be launched!</span></span>

## <a name="your-microsoft-graph-hololens-application"></a><span data-ttu-id="a40a4-349">Votre application Microsoft Graph HoloLens</span><span class="sxs-lookup"><span data-stu-id="a40a4-349">Your Microsoft Graph HoloLens application</span></span>

<span data-ttu-id="a40a4-350">Félicitations, vous avez créé une application de réalité mixte qui tire parti de la Microsoft Graph pour lire et afficher les données de calendrier utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a40a4-350">Congratulations, you built a mixed reality app that leverages the Microsoft Graph, to read and display user Calendar data.</span></span>

![](images/AzureLabs-Lab311-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="a40a4-351">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="a40a4-351">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="a40a4-352">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="a40a4-352">Exercise 1</span></span>

<span data-ttu-id="a40a4-353">Utiliser Microsoft Graph pour afficher d’autres informations sur l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a40a4-353">Use Microsoft Graph to display other information about the user</span></span>

-   <span data-ttu-id="a40a4-354">Adresse de messagerie/numéro de téléphone/de profil utilisateur</span><span class="sxs-lookup"><span data-stu-id="a40a4-354">User email / phone number / profile picture</span></span>

### <a name="exercise-1"></a><span data-ttu-id="a40a4-355">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="a40a4-355">Exercise 1</span></span>

<span data-ttu-id="a40a4-356">Implémentez le contrôle vocal pour naviguer dans l’interface utilisateur Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="a40a4-356">Implement voice control to navigate the Microsoft Graph UI.</span></span>
