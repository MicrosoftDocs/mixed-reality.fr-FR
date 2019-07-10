---
title: MR et Azure 311 - Microsoft Graph
description: Terminer ce cours pour apprendre à tirer parti de Microsoft Graph et se connecter aux données qui favorisent la productivité, au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, graph de microsoft, hololens, immersives, vr
ms.openlocfilehash: 04c72a7ef7724cfcc27867f7f003c171a6f7851f
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694525"
---
>[!NOTE]
><span data-ttu-id="909b9-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="909b9-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="909b9-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="909b9-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="909b9-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="909b9-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="909b9-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="909b9-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="909b9-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="909b9-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="909b9-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="909b9-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

# <a name="mr-and-azure-311---microsoft-graph"></a><span data-ttu-id="909b9-110">MR et Azure 311 - Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="909b9-110">MR and Azure 311 - Microsoft Graph</span></span>

<span data-ttu-id="909b9-111">Dans ce cours, vous allez apprendre à utiliser *Microsoft Graph* pour vous connecter à votre compte Microsoft à l’aide de l’authentification sécurisée dans une application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="909b9-111">In this course, you will learn how to use *Microsoft Graph* to log in into your Microsoft account using secure authentication within a mixed reality application.</span></span> <span data-ttu-id="909b9-112">Vous serez ensuite récupérer et afficher vos réunions planifiées dans l’interface de l’application.</span><span class="sxs-lookup"><span data-stu-id="909b9-112">You will then retrieve and display your scheduled meetings in the application interface.</span></span>

![](images/AzureLabs-Lab311-00.png)

<span data-ttu-id="909b9-113">*Microsoft Graph* est un ensemble d’API conçues pour permettre l’accès à de nombreux services de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="909b9-113">*Microsoft Graph* is a set of APIs designed to enable access to many of Microsoft's services.</span></span> <span data-ttu-id="909b9-114">Microsoft décrit Microsoft Graph comme étant une matrice des ressources connectées par des relations, ce qui signifie qu’il permet à une application à accéder à toutes sortes de données de l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="909b9-114">Microsoft describes Microsoft Graph as being a matrix of resources connected by relationships, meaning it allows an application to access all sorts of connected user data.</span></span> <span data-ttu-id="909b9-115">Pour plus d’informations, visitez le [page de Microsoft Graph](https://developer.microsoft.com/graph).</span><span class="sxs-lookup"><span data-stu-id="909b9-115">For more information, visit the [Microsoft Graph page](https://developer.microsoft.com/graph).</span></span>

<span data-ttu-id="909b9-116">Développement incluent la création d’une application où l’utilisateur sera invité à fixez du regard, puis appuyez sur une sphère, qui invitera l’utilisateur pour vous connecter en toute sécurité à un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="909b9-116">Development will include the creation of an app where the user will be instructed to gaze at and then tap a sphere, which will prompt the user to log in safely to a Microsoft account.</span></span> <span data-ttu-id="909b9-117">Une fois connecté à son compte, l’utilisateur sera en mesure de voir une liste de réunions planifiées pour la journée.</span><span class="sxs-lookup"><span data-stu-id="909b9-117">Once logged in to their account, the user will be able to see a list of meetings scheduled for the day.</span></span>

<span data-ttu-id="909b9-118">Avoir terminé ce cours, vous aurez une réalité mixte application HoloLens, qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="909b9-118">Having completed this course, you will have a mixed reality HoloLens application, which will be able to do the following:</span></span>

1.  <span data-ttu-id="909b9-119">À l’aide de l’action d’appuyer, appuyez sur un objet qui invitera l’utilisateur pour vous connecter à un Account Microsoft (déplacement hors de l’application pour vous connecter et inversement à l’application).</span><span class="sxs-lookup"><span data-stu-id="909b9-119">Using the Tap gesture, tap on an object, which will prompt the user to log into a Microsoft Account (moving out of the app to log in, and then back into the app again).</span></span>
2.  <span data-ttu-id="909b9-120">Afficher la liste des réunions planifiées pour la journée.</span><span class="sxs-lookup"><span data-stu-id="909b9-120">View a list of meetings scheduled for the day.</span></span> 

<span data-ttu-id="909b9-121">Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception.</span><span class="sxs-lookup"><span data-stu-id="909b9-121">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="909b9-122">Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="909b9-122">This course is designed to teach you how to integrate an Azure Service with your Unity project.</span></span> <span data-ttu-id="909b9-123">Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="909b9-123">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

## <a name="device-support"></a><span data-ttu-id="909b9-124">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="909b9-124">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="909b9-125">Cours</span><span class="sxs-lookup"><span data-stu-id="909b9-125">Course</span></span></th><th style="width:150px"> <span data-ttu-id="909b9-126"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="909b9-126"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="909b9-127"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="909b9-127"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="909b9-128">MR et Azure 311 : Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="909b9-128">MR and Azure 311: Microsoft Graph</span></span></td><td style="text-align: center;"> <span data-ttu-id="909b9-129">✔️</span><span class="sxs-lookup"><span data-stu-id="909b9-129">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="prerequisites"></a><span data-ttu-id="909b9-130">Prérequis</span><span class="sxs-lookup"><span data-stu-id="909b9-130">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="909b9-131">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="909b9-131">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="909b9-132">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (juillet 2018).</span><span class="sxs-lookup"><span data-stu-id="909b9-132">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (July 2018).</span></span> <span data-ttu-id="909b9-133">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="909b9-133">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you will find in newer software than what is listed below.</span></span>

<span data-ttu-id="909b9-134">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="909b9-134">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="909b9-135">Un PC de développement</span><span class="sxs-lookup"><span data-stu-id="909b9-135">A development PC</span></span>
- [<span data-ttu-id="909b9-136">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="909b9-136">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="909b9-137">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="909b9-137">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="909b9-138">Unity 2017.4</span><span class="sxs-lookup"><span data-stu-id="909b9-138">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="909b9-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="909b9-139">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="909b9-140">Un [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="909b9-140">A [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="909b9-141">Accès à Internet pour le programme d’installation Azure et l’extraction de données de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="909b9-141">Internet access for Azure setup and Microsoft Graph data retrieval</span></span>
- <span data-ttu-id="909b9-142">Valide **Account Microsoft** (personnel ou Professionnel ou scolaire)</span><span class="sxs-lookup"><span data-stu-id="909b9-142">A valid **Microsoft Account** (either personal or work/school)</span></span>
- <span data-ttu-id="909b9-143">Quelques réunions planifiées pour le jour actuel, à l’aide de la même Account Microsoft</span><span class="sxs-lookup"><span data-stu-id="909b9-143">A few meetings scheduled for the current day, using the same Microsoft Account</span></span>

### <a name="before-you-start"></a><span data-ttu-id="909b9-144">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="909b9-144">Before you start</span></span>

1.  <span data-ttu-id="909b9-145">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="909b9-145">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="909b9-146">Configurer et tester votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="909b9-146">Set up and test your HoloLens.</span></span> <span data-ttu-id="909b9-147">Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="909b9-147">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span> 
3.  <span data-ttu-id="909b9-148">Il est judicieux d’effectuer l’étalonnage et le réglage de capteur lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="909b9-148">It is a good idea to perform Calibration and Sensor Tuning when beginning developing a new HoloLens App (sometimes it can help to perform those tasks for each user).</span></span> 

<span data-ttu-id="909b9-149">Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).</span><span class="sxs-lookup"><span data-stu-id="909b9-149">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens).</span></span>

<span data-ttu-id="909b9-150">Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="909b9-150">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

## <a name="chapter-1---create-your-app-in-the-application-registration-portal"></a><span data-ttu-id="909b9-151">Chapitre 1 - créer votre application dans le portail d’inscription des applications</span><span class="sxs-lookup"><span data-stu-id="909b9-151">Chapter 1 - Create your app in the Application Registration Portal</span></span>

<span data-ttu-id="909b9-152">Pour commencer, vous devez créer et inscrire votre application dans le **portail d’inscription des applications**.</span><span class="sxs-lookup"><span data-stu-id="909b9-152">To begin with, you will need to create and register your application in the **Application Registration Portal**.</span></span>

<span data-ttu-id="909b9-153">Dans ce chapitre, vous trouverez également la clé de Service qui vous permet d’effectuer des appels vers *Microsoft Graph* pour accéder au contenu de votre compte.</span><span class="sxs-lookup"><span data-stu-id="909b9-153">In this Chapter you will also find the Service Key that will allow you to make calls to *Microsoft Graph* to access your account content.</span></span>

1.  <span data-ttu-id="909b9-154">Accédez à la [portail d’inscription de Microsoft Application](https://apps.dev.microsoft.com) et connectez-vous avec votre Account de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="909b9-154">Navigate to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com) and login with your Microsoft Account.</span></span> <span data-ttu-id="909b9-155">Une fois que vous êtes connecté, vous êtes redirigé vers la **portail d’inscription des applications**.</span><span class="sxs-lookup"><span data-stu-id="909b9-155">Once you have logged in, you will be redirected to the **Application Registration Portal**.</span></span>

2.  <span data-ttu-id="909b9-156">Dans le **mes applications** section, cliquez sur le bouton **ajouter une application**.</span><span class="sxs-lookup"><span data-stu-id="909b9-156">In the **My applications** section, click on the button **Add an app**.</span></span>

    ![](images/AzureLabs-Lab311-01.png)![](images/AzureLabs-Lab311-02.png)

    > [!IMPORTANT]
    > <span data-ttu-id="909b9-157">Le **portail d’inscription des applications** peut être différente, selon que vous avez travaillé précédemment avec *Microsoft Graph*.</span><span class="sxs-lookup"><span data-stu-id="909b9-157">The **Application Registration Portal** can look different, depending on whether you have previously worked with *Microsoft Graph*.</span></span> <span data-ttu-id="909b9-158">Le ci-dessous des captures d’écran afficher ces différentes versions.</span><span class="sxs-lookup"><span data-stu-id="909b9-158">The below screenshots display these different versions.</span></span>

3.  <span data-ttu-id="909b9-159">Ajouter un nom pour votre application et le clic **créer**.</span><span class="sxs-lookup"><span data-stu-id="909b9-159">Add a name for your application and click **Create**.</span></span>

    ![](images/AzureLabs-Lab311-03.png)

4.  <span data-ttu-id="909b9-160">Une fois que l’application a été créée, vous serez redirigé vers la page principale d’application.</span><span class="sxs-lookup"><span data-stu-id="909b9-160">Once the application has been created, you will be redirected to the application main page.</span></span> <span data-ttu-id="909b9-161">Copie le **Id d’Application** et veillez à noter cette valeur dans un endroit sûr, vous l’utiliserez bientôt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="909b9-161">Copy the **Application Id** and make sure to note this value somewhere safe, you will use it soon in your code.</span></span>

    ![](images/AzureLabs-Lab311-04.png)

5.  <span data-ttu-id="909b9-162">Dans le **plateformes** section, assurez-vous que **Application Native** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="909b9-162">In the **Platforms** section, make sure **Native Application** is displayed.</span></span> <span data-ttu-id="909b9-163">Si *pas* cliquez sur **ajouter une plateforme** et sélectionnez **Application Native**.</span><span class="sxs-lookup"><span data-stu-id="909b9-163">If *not* click on **Add Platform** and select **Native Application**.</span></span>

    ![](images/AzureLabs-Lab311-05.png)

6.  <span data-ttu-id="909b9-164">Défiler vers le bas dans la même page et dans la section intitulée **autorisations Microsoft Graph** vous devez ajouter des autorisations supplémentaires pour l’application.</span><span class="sxs-lookup"><span data-stu-id="909b9-164">Scroll down in the same page and in the section called **Microsoft Graph Permissions** you will need to add additional permissions for the application.</span></span> <span data-ttu-id="909b9-165">Cliquez sur **ajouter** regard **autorisations déléguées**.</span><span class="sxs-lookup"><span data-stu-id="909b9-165">Click on **Add** next to **Delegated Permissions**.</span></span>

    ![](images/AzureLabs-Lab311-06.png)

7.  <span data-ttu-id="909b9-166">Dans la mesure où vous souhaitez que votre application à accéder au calendrier de l’utilisateur, cochez la case appelée **Calendars.Read** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="909b9-166">Since you want your application to access the user's Calendar, check the box called **Calendars.Read** and click **OK**.</span></span>

    ![](images/AzureLabs-Lab311-07.png)

8.  <span data-ttu-id="909b9-167">Faites défiler vers le bas et cliquez sur le **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="909b9-167">Scroll to the bottom and click the **Save** button.</span></span>

    ![](images/AzureLabs-Lab311-08.png)

9.  <span data-ttu-id="909b9-168">Votre enregistrement confirmé, vous pouvez déconnecter à partir de la **portail d’inscription des applications**.</span><span class="sxs-lookup"><span data-stu-id="909b9-168">Your save will be confirmed, and you can log out from the **Application Registration Portal**.</span></span>

## <a name="chapter-2---set-up-the-unity-project"></a><span data-ttu-id="909b9-169">Chapitre 2 : configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="909b9-169">Chapter 2 - Set up the Unity project</span></span>

<span data-ttu-id="909b9-170">Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="909b9-170">The following is a typical set up for developing with mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="909b9-171">Ouvrez *Unity* et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="909b9-171">Open *Unity* and click **New**.</span></span>

    ![](images/AzureLabs-Lab311-09.png)

2.  <span data-ttu-id="909b9-172">Vous devez fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="909b9-172">You need to provide a Unity project name.</span></span> <span data-ttu-id="909b9-173">Insérer **MSGraphMR**.</span><span class="sxs-lookup"><span data-stu-id="909b9-173">Insert **MSGraphMR**.</span></span> <span data-ttu-id="909b9-174">Assurez-vous que le modèle de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="909b9-174">Make sure the project template is set to **3D**.</span></span> <span data-ttu-id="909b9-175">Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="909b9-175">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="909b9-176">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="909b9-176">Then, click **Create project**.</span></span>

    ![](images/AzureLabs-Lab311-10.png)

3.  <span data-ttu-id="909b9-177">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="909b9-177">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="909b9-178">Accédez à **modifier** > **préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="909b9-178">Go to **Edit** > **Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="909b9-179">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="909b9-179">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="909b9-180">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="909b9-180">Close the **Preferences** window.</span></span>

    ![](images/AzureLabs-Lab311-11.png)

4.  <span data-ttu-id="909b9-181">Accédez à **fichier** > **paramètres de Build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le **plateforme de commutation** bouton pour appliquer votre sélection.</span><span class="sxs-lookup"><span data-stu-id="909b9-181">Go to **File** > **Build Settings** and select **Universal Windows Platform**, then click on the **Switch Platform** button to apply your selection.</span></span>

    ![](images/AzureLabs-Lab311-12.png)

5.  <span data-ttu-id="909b9-182">Lorsque vous êtes toujours dans **fichier** > **paramètres de Build**, assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="909b9-182">While still in **File** > **Build Settings**, make sure that:</span></span>

    1. <span data-ttu-id="909b9-183">**Équipement cible** a la valeur **HoloLens**</span><span class="sxs-lookup"><span data-stu-id="909b9-183">**Target Device** is set to **HoloLens**</span></span>
    2. <span data-ttu-id="909b9-184">**Type de build** a la valeur **D3D**</span><span class="sxs-lookup"><span data-stu-id="909b9-184">**Build Type** is set to **D3D**</span></span>
    3. <span data-ttu-id="909b9-185">**Kit de développement logiciel** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="909b9-185">**SDK** is set to **Latest installed**</span></span>
    4. <span data-ttu-id="909b9-186">**Version de Visual Studio** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="909b9-186">**Visual Studio Version** is set to **Latest installed**</span></span>
    5. <span data-ttu-id="909b9-187">**Générez et exécutez** est défini sur **ordinateur Local**</span><span class="sxs-lookup"><span data-stu-id="909b9-187">**Build and Run** is set to **Local Machine**</span></span>
    6. <span data-ttu-id="909b9-188">Enregistrer la scène et l’ajouter à la build.</span><span class="sxs-lookup"><span data-stu-id="909b9-188">Save the scene and add it to the build.</span></span>

        1. <span data-ttu-id="909b9-189">Cela en sélectionnant **ajouter un arrière-plan Open**.</span><span class="sxs-lookup"><span data-stu-id="909b9-189">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="909b9-190">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="909b9-190">A save window will appear.</span></span>

            ![](images/AzureLabs-Lab311-13.png)

        2. <span data-ttu-id="909b9-191">Pour cela et n’importe quel futur, votre scène, créez un dossier.</span><span class="sxs-lookup"><span data-stu-id="909b9-191">Create a new folder for this, and any future, scene.</span></span> <span data-ttu-id="909b9-192">Sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.</span><span class="sxs-lookup"><span data-stu-id="909b9-192">Select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![](images/AzureLabs-Lab311-14.png)

        3. <span data-ttu-id="909b9-193">Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier*: champ de texte, tapez **MR_ComputerVisionScene**, puis cliquez sur **enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="909b9-193">Open your newly created **Scenes** folder, and then in the *File name*: text field, type **MR_ComputerVisionScene**, then click **Save**.</span></span>

            ![](images/AzureLabs-Lab311-15.png)

            > [!IMPORTANT] 
            > <span data-ttu-id="909b9-194">N’oubliez pas, vous devez enregistrer vos séquences de Unity dans le *actifs* dossier, car ils doivent être associées au projet Unity.</span><span class="sxs-lookup"><span data-stu-id="909b9-194">Be aware, you must save your Unity scenes within the *Assets* folder, as they must be associated with the Unity project.</span></span> <span data-ttu-id="909b9-195">Création du dossier de scènes (et autres dossiers similaire) est un moyen classique de structurer un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="909b9-195">Creating the scenes folder (and other similar folders) is a typical way of structuring a Unity project.</span></span>

    7.  <span data-ttu-id="909b9-196">Les autres paramètres, dans *paramètres de Build*, doit être conservé comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="909b9-196">The remaining settings, in *Build Settings*, should be left as default for now.</span></span>

6.  <span data-ttu-id="909b9-197">Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve.</span><span class="sxs-lookup"><span data-stu-id="909b9-197">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span> 

    ![](images/AzureLabs-Lab311-16.png)

7. <span data-ttu-id="909b9-198">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="909b9-198">In this panel, a few settings need to be verified:</span></span>

    1. <span data-ttu-id="909b9-199">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="909b9-199">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="909b9-200">**Écriture de scripts** **Version du Runtime** doit être **expérimental** (.NET 4.6 équivalent), ce qui déclenchera une nécessité de redémarrer l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="909b9-200">**Scripting** **Runtime Version** should be **Experimental** (.NET 4.6 Equivalent), which will trigger a need to restart the Editor.</span></span>

        2. <span data-ttu-id="909b9-201">**Script principal** doit être **.NET**</span><span class="sxs-lookup"><span data-stu-id="909b9-201">**Scripting Backend** should be **.NET**</span></span>

        3. <span data-ttu-id="909b9-202">**Niveau de compatibilité d’API** doit être **.NET 4.6**</span><span class="sxs-lookup"><span data-stu-id="909b9-202">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![](images/AzureLabs-Lab311-17.png)

    2.  <span data-ttu-id="909b9-203">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="909b9-203">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="909b9-204">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="909b9-204">**InternetClient**</span></span>

            ![](images/AzureLabs-Lab311-18.png)

    3.  <span data-ttu-id="909b9-205">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), vérifiez **virtuel pris en charge de réalité**, assurez-vous que le **Windows Mixed Reality Kit de développement logiciel** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="909b9-205">Further down the panel, in **XR Settings** (found below **Publish Settings**), check **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![](images/AzureLabs-Lab311-19.png)

8.  <span data-ttu-id="909b9-206">Dans *paramètres de Build*, *Unity C# projets* est n’est plus grisée ; case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="909b9-206">Back in *Build Settings*, *Unity C# Projects* is no longer greyed out; check the checkbox next to this.</span></span>

9.  <span data-ttu-id="909b9-207">Fermer le *paramètres de Build* fenêtre.</span><span class="sxs-lookup"><span data-stu-id="909b9-207">Close the *Build Settings* window.</span></span>

10.  <span data-ttu-id="909b9-208">Enregistrer votre projet et la scène (**fichier** > **enregistrer les scènes / fichier** > **enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="909b9-208">Save your scene and project (**FILE** > **SAVE SCENES / FILE** > **SAVE PROJECT**).</span></span>

## <a name="chapter-3---import-libraries-in-unity"></a><span data-ttu-id="909b9-209">Chapitre 3 - bibliothèques d’importation dans Unity</span><span class="sxs-lookup"><span data-stu-id="909b9-209">Chapter 3 - Import Libraries in Unity</span></span>

> [!IMPORTANT]
> <span data-ttu-id="909b9-210">Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [Azure-MR-311.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20311%20-%20Microsoft%20Graph/Azure-MR-311.unitypackage), importez-le dans votre projet en tant qu’un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 5](#chapter-5---create-meetingsui-class).</span><span class="sxs-lookup"><span data-stu-id="909b9-210">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to download this [Azure-MR-311.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20311%20-%20Microsoft%20Graph/Azure-MR-311.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 5](#chapter-5---create-meetingsui-class).</span></span>

<span data-ttu-id="909b9-211">Pour utiliser *Microsoft Graph* dans Unity, vous devez vous utiliser le **Microsoft.Identity.Client** DLL.</span><span class="sxs-lookup"><span data-stu-id="909b9-211">To use *Microsoft Graph* within Unity you need to make use of the  **Microsoft.Identity.Client** DLL.</span></span> <span data-ttu-id="909b9-212">Il est possible d’utiliser le kit SDK Microsoft Graph, toutefois, il nécessite l’ajout d’un package NuGet une fois que vous générez le projet Unity (c'est-à-dire modification après la génération du projet).</span><span class="sxs-lookup"><span data-stu-id="909b9-212">It is possible to use the Microsoft Graph SDK, however, it will require the addition of a NuGet package after you build the Unity project (meaning editing the project post-build).</span></span> <span data-ttu-id="909b9-213">Il est considéré comme plus simple d’importer les DLL requises directement dans Unity.</span><span class="sxs-lookup"><span data-stu-id="909b9-213">It is considered simpler to import the required DLLs directly into Unity.</span></span>

> [!NOTE]
> <span data-ttu-id="909b9-214">Il est actuellement un problème connu dans Unity qui nécessite des plug-ins à être reconfiguré après l’importation.</span><span class="sxs-lookup"><span data-stu-id="909b9-214">There is currently a known issue in Unity which requires plugins to be reconfigured after import.</span></span> <span data-ttu-id="909b9-215">Ces étapes (4-7 de cette section) ne sera plus nécessaires une fois que le bogue a été résolu.</span><span class="sxs-lookup"><span data-stu-id="909b9-215">These steps (4 - 7 in this section) will no longer be required after the bug has been resolved.</span></span>

<span data-ttu-id="909b9-216">Pour importer *Microsoft Graph* dans votre propre projet, [télécharger le fichier MSGraph_LabPlugins.zip](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20311%20-%20Microsoft%20Graph/MSGraph_LabPlugins.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="909b9-216">To import *Microsoft Graph* into your own project, [download the MSGraph_LabPlugins.zip file](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20311%20-%20Microsoft%20Graph/MSGraph_LabPlugins.unitypackage).</span></span> <span data-ttu-id="909b9-217">Ce package a été créé avec les versions des bibliothèques qui ont été testés.</span><span class="sxs-lookup"><span data-stu-id="909b9-217">This package has been created with versions of the libraries that have been tested.</span></span>

<span data-ttu-id="909b9-218">Si vous le souhaitez en savoir plus sur l’ajout de DLL personnalisées à votre projet Unity, [, suivez ce lien](https://docs.unity3d.com/Manual/UsingDLL.html).</span><span class="sxs-lookup"><span data-stu-id="909b9-218">If you wish to know more about how to add custom DLLs to your Unity project, [follow this link](https://docs.unity3d.com/Manual/UsingDLL.html).</span></span>

<span data-ttu-id="909b9-219">Pour importer le package :</span><span class="sxs-lookup"><span data-stu-id="909b9-219">To import the package:</span></span>

1.  <span data-ttu-id="909b9-220">Ajouter le Package Unity pour Unity à l’aide de la **actifs** > **importer un Package** > **Package personnalisé** option de menu.</span><span class="sxs-lookup"><span data-stu-id="909b9-220">Add the Unity Package to Unity by using the **Assets** > **Import Package** > **Custom Package** menu option.</span></span> <span data-ttu-id="909b9-221">Sélectionnez le package que vous venez de télécharger.</span><span class="sxs-lookup"><span data-stu-id="909b9-221">Select the package you just downloaded.</span></span>

2.  <span data-ttu-id="909b9-222">Dans le **importer un Package Unity** emballer qui apparaît, vérifiez tous les éléments sous (y compris) **plug-ins** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="909b9-222">In the **Import Unity Package** box that pops up, ensure everything under (and including) **Plugins** is selected.</span></span>

    ![](images/AzureLabs-Lab311-20.png)

3.  <span data-ttu-id="909b9-223">Cliquez sur le **importation** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="909b9-223">Click the **Import** button to add the items to your project.</span></span>

4.  <span data-ttu-id="909b9-224">Accédez à la **MSGraph** dossier sous **plug-ins** dans le *panneau projet* et sélectionnez le plug-in appelé **Microsoft.Identity.Client**.</span><span class="sxs-lookup"><span data-stu-id="909b9-224">Go to the **MSGraph** folder under **Plugins** in the *Project Panel* and select the plugin called **Microsoft.Identity.Client**.</span></span>

    ![](images/AzureLabs-Lab311-21.png)

5.  <span data-ttu-id="909b9-225">Avec le *plug-in* sélectionnée, vérifiez que **plateforme Any** est désactivée, puis vérifiez que **WSAPlayer** est également désactivée, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="909b9-225">With the *plugin* selected, ensure that **Any Platform** is unchecked, then ensure that **WSAPlayer** is also unchecked, then click **Apply**.</span></span> <span data-ttu-id="909b9-226">Il s’agit juste pour confirmer que les fichiers sont correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="909b9-226">This is just to confirm that the files are configured correctly.</span></span>

    ![](images/AzureLabs-Lab311-22.png)

    > [!NOTE] 
    > <span data-ttu-id="909b9-227">Marquage de ces plug-ins les configure uniquement à être utilisé dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="909b9-227">Marking these plugins configures them to only be used in the Unity Editor.</span></span> <span data-ttu-id="909b9-228">Il existe un autre ensemble de DLL dans le dossier WSA qui sera utilisée une fois que le projet est exporté à partir d’Unity comme une Application Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="909b9-228">There are a different set of DLLs in the WSA folder which will be used after the project is exported from Unity as a Universal Windows Application.</span></span>

6.  <span data-ttu-id="909b9-229">Ensuite, vous devez ouvrir le **WSA** dossier, en respectant le **MSGraph** dossier.</span><span class="sxs-lookup"><span data-stu-id="909b9-229">Next, you need to open the **WSA** folder, within the **MSGraph** folder.</span></span> <span data-ttu-id="909b9-230">Vous verrez une copie du même fichier que vous venez de configurer.</span><span class="sxs-lookup"><span data-stu-id="909b9-230">You will see a copy of the same file you just configured.</span></span> <span data-ttu-id="909b9-231">Sélectionnez le fichier, puis, dans l’inspecteur de :</span><span class="sxs-lookup"><span data-stu-id="909b9-231">Select the file, and then in the inspector:</span></span>

    -   <span data-ttu-id="909b9-232">Vérifiez que **plateforme Any** est **unchecked**et qui **uniquement** **WSAPlayer** est **vérifiée**.</span><span class="sxs-lookup"><span data-stu-id="909b9-232">ensure that **Any Platform** is **unchecked**, and that **only** **WSAPlayer** is **checked**.</span></span>

    -   <span data-ttu-id="909b9-233">Vérifiez **SDK** a la valeur **UWP**, et **back-end de script** a la valeur **Dot Net**</span><span class="sxs-lookup"><span data-stu-id="909b9-233">Ensure **SDK** is set to **UWP**, and **Scripting Backend** is set to **Dot Net**</span></span>

    -   <span data-ttu-id="909b9-234">Vérifiez que **ne pas traiter les** est **vérifiée**.</span><span class="sxs-lookup"><span data-stu-id="909b9-234">Ensure that **Don't process** is **checked**.</span></span>

        ![](images/AzureLabs-Lab311-23.png)

7.  <span data-ttu-id="909b9-235">Cliquez sur **Apply** (Appliquer).</span><span class="sxs-lookup"><span data-stu-id="909b9-235">Click **Apply**.</span></span>

## <a name="chapter-4---camera-setup"></a><span data-ttu-id="909b9-236">Chapitre 4 - programme d’installation de l’appareil photo</span><span class="sxs-lookup"><span data-stu-id="909b9-236">Chapter 4 - Camera Setup</span></span>

<span data-ttu-id="909b9-237">Au cours de ce chapitre, vous allez configurer la caméra principale de votre scène :</span><span class="sxs-lookup"><span data-stu-id="909b9-237">During this Chapter you will set up the Main Camera of your scene:</span></span>

1.  <span data-ttu-id="909b9-238">Dans le *hiérarchie panneau*, sélectionnez le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="909b9-238">In the *Hierarchy Panel*, select the **Main Camera**.</span></span>

2.  <span data-ttu-id="909b9-239">Une fois sélectionné, vous serez en mesure de voir tous les composants de la **Main Camera** dans le *inspecteur* Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="909b9-239">Once selected, you will be able to see all the components of the **Main Camera** in the *Inspector* panel.</span></span>

    1.  <span data-ttu-id="909b9-240">Le **objet caméra** doit être nommé **Main Camera** (Notez l’orthographe !)</span><span class="sxs-lookup"><span data-stu-id="909b9-240">The **Camera object** must be named **Main Camera** (note the spelling!)</span></span>

    2.  <span data-ttu-id="909b9-241">La caméra principale **balise** doit être définie sur **MainCamera** (Notez l’orthographe !)</span><span class="sxs-lookup"><span data-stu-id="909b9-241">The Main Camera **Tag** must be set to **MainCamera** (note the spelling!)</span></span>

    3.  <span data-ttu-id="909b9-242">Assurez-vous que le **Position transformer** a la valeur **0, 0, 0**</span><span class="sxs-lookup"><span data-stu-id="909b9-242">Make sure the **Transform Position** is set to **0, 0, 0**</span></span>

    4.  <span data-ttu-id="909b9-243">Définissez **d’effacer les indicateurs** à **couleur unie**</span><span class="sxs-lookup"><span data-stu-id="909b9-243">Set **Clear Flags** to **Solid Color**</span></span>

    5.  <span data-ttu-id="909b9-244">Définir le **couleur d’arrière-plan** du composant de caméra à **noir, Alpha 0** **(Hex Code : #00000000)**</span><span class="sxs-lookup"><span data-stu-id="909b9-244">Set the **Background Color** of the Camera Component to **Black, Alpha 0** **(Hex Code: #00000000)**</span></span>

        ![](images/AzureLabs-Lab311-24.png)

3.  <span data-ttu-id="909b9-245">La structure de l’objet final dans le *hiérarchie panneau* doit être semblable à celui illustré dans l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="909b9-245">The final object structure in the *Hierarchy Panel* should be like the one shown in the image below:</span></span>

    ![](images/AzureLabs-Lab311-25.png)

## <a name="chapter-5---create-meetingsui-class"></a><span data-ttu-id="909b9-246">Chapitre 5 - créer MeetingsUI classe</span><span class="sxs-lookup"><span data-stu-id="909b9-246">Chapter 5 - Create MeetingsUI class</span></span>

<span data-ttu-id="909b9-247">Le premier script que vous créez est **MeetingsUI**, qui est responsable de l’hébergement et de remplissage de l’interface utilisateur de l’application (message de bienvenue, des instructions et les détails de réunions).</span><span class="sxs-lookup"><span data-stu-id="909b9-247">The first script you need to create is **MeetingsUI**, which is responsible for hosting and populating the UI of the application (welcome message, instructions and the meetings details).</span></span>

<span data-ttu-id="909b9-248">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="909b9-248">To create this class:</span></span>

1.  <span data-ttu-id="909b9-249">Avec le bouton droit sur le **actifs** dossier dans le *panneau projet*, puis sélectionnez **créer** > **dossier**.</span><span class="sxs-lookup"><span data-stu-id="909b9-249">Right-click on the **Assets** folder in the *Project Panel*, then select **Create** > **Folder**.</span></span> <span data-ttu-id="909b9-250">Nommez le dossier **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="909b9-250">Name the folder **Scripts**.</span></span>

    ![](images/AzureLabs-Lab311-26.png)
    ![](images/AzureLabs-Lab311-27.png)

2.  <span data-ttu-id="909b9-251">Ouvrez le **Scripts** dossier puis, dans ce dossier, avec le bouton droit, **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="909b9-251">Open the **Scripts** folder then, within that folder, right-click, **Create** > **C# Script**.</span></span> <span data-ttu-id="909b9-252">Nommez le script **MeetingsUI.**</span><span class="sxs-lookup"><span data-stu-id="909b9-252">Name the script **MeetingsUI.**</span></span>

    ![](images/AzureLabs-Lab311-28.png)

3.  <span data-ttu-id="909b9-253">Double-cliquez sur le nouveau **MeetingsUI** script pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="909b9-253">Double-click on the new **MeetingsUI** script to open it with *Visual Studio*.</span></span>

4.  <span data-ttu-id="909b9-254">Insérer des espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="909b9-254">Insert the following namespaces:</span></span>

    ```csharp
    using System;
    using UnityEngine;
    ```

5.  <span data-ttu-id="909b9-255">À l’intérieur de la classe, insérez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="909b9-255">Inside the class insert the following variables:</span></span>

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

6.  <span data-ttu-id="909b9-256">Remplacez ensuite le **Start()** (méthode) et ajoutez un **Awake()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="909b9-256">Then replace the **Start()** method and add an **Awake()** method.</span></span> <span data-ttu-id="909b9-257">Il seront appelées lors de l’initialisation de la classe :</span><span class="sxs-lookup"><span data-stu-id="909b9-257">These will be called when the class initializes:</span></span>

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

7.  <span data-ttu-id="909b9-258">Ajoutez les méthodes chargées de créer le *l’interface utilisateur de réunions* et le remplir avec les réunions en cours lorsque demandé :</span><span class="sxs-lookup"><span data-stu-id="909b9-258">Add the methods responsible for creating the *Meetings UI* and populate it with the current meetings when requested:</span></span>

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

8. <span data-ttu-id="909b9-259">**Supprimer** le **Update()** (méthode), et **enregistrer vos modifications** dans Visual Studio avant de retourner à Unity.</span><span class="sxs-lookup"><span data-stu-id="909b9-259">**Delete** the **Update()** method, and **save your changes** in Visual Studio before returning to Unity.</span></span> 

## <a name="chapter-6---create-the-graph-class"></a><span data-ttu-id="909b9-260">Chapitre 6 : créer la classe de graphique</span><span class="sxs-lookup"><span data-stu-id="909b9-260">Chapter 6 - Create the Graph class</span></span>

<span data-ttu-id="909b9-261">Le script suivant pour créer le **Graph** script.</span><span class="sxs-lookup"><span data-stu-id="909b9-261">The next script to create is the **Graph** script.</span></span> <span data-ttu-id="909b9-262">Ce script est chargé d’effectuer les appels pour authentifier l’utilisateur et de récupérer les réunions planifiées pour le jour actuel à partir du calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="909b9-262">This script is responsible for making the calls to authenticate the user and retrieve the scheduled meetings for the current day from the user's calendar.</span></span>

<span data-ttu-id="909b9-263">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="909b9-263">To create this class:</span></span>

1.  <span data-ttu-id="909b9-264">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="909b9-264">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="909b9-265">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="909b9-265">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="909b9-266">Nommez le script **graphique**.</span><span class="sxs-lookup"><span data-stu-id="909b9-266">Name the script **Graph**.</span></span>

3.  <span data-ttu-id="909b9-267">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="909b9-267">Double-click on the script to open it with Visual Studio.</span></span>

4.  <span data-ttu-id="909b9-268">Insérer des espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="909b9-268">Insert the following namespaces:</span></span>

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
    > <span data-ttu-id="909b9-269">Vous remarquerez que les parties du code dans ce script sont wrappés autour de [précompiler les Directives](https://docs.unity3d.com/Manual/PlatformDependentCompilation.html), sert à éviter les problèmes rencontrés avec les bibliothèques lors de la création de la Solution Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="909b9-269">You will notice that parts of the code in this script are wrapped around [Precompile Directives](https://docs.unity3d.com/Manual/PlatformDependentCompilation.html), this is to avoid issues with the libraries when building the Visual Studio Solution.</span></span>

5.  <span data-ttu-id="909b9-270">Supprimer le **Start()** et **Update()** méthodes, car ils ne seront pas utilisés.</span><span class="sxs-lookup"><span data-stu-id="909b9-270">Delete the **Start()** and **Update()** methods, as they will not be used.</span></span>

6.  <span data-ttu-id="909b9-271">En dehors du **Graph** de classe, insérez les objets suivants, qui sont nécessaires pour désérialiser l’objet JSON représentant les réunions planifiées quotidiennes :</span><span class="sxs-lookup"><span data-stu-id="909b9-271">Outside the **Graph** class, insert the following objects, which are necessary to deserialize the JSON object representing the daily scheduled meetings:</span></span>

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

7.  <span data-ttu-id="909b9-272">À l’intérieur de la **Graph** de classe, ajoutez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="909b9-272">Inside the **Graph** class, add the following variables:</span></span>

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
    > <span data-ttu-id="909b9-273">Modifier le **appId** valeur soit la **Id d’application** que vous avez déjà notés dans  **[chapitre 1](#chapter-1---create-your-app-in-the-application-registration-portal), étape 4**.</span><span class="sxs-lookup"><span data-stu-id="909b9-273">Change the **appId** value to be the **App Id** that you have noted in **[Chapter 1](#chapter-1---create-your-app-in-the-application-registration-portal), step 4**.</span></span> <span data-ttu-id="909b9-274">Cette valeur doit être identique à celui affiché dans le **portail d’inscription des applications,** dans la page d’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="909b9-274">This value should be the same as that displayed in the **Application Registration Portal,** in your application registration page.</span></span>

8.  <span data-ttu-id="909b9-275">Dans le **Graph** de classe, ajoutez les méthodes **SignInAsync()** et **AquireTokenAsync()** , qui invitera l’utilisateur d’insérer les informations de journal.</span><span class="sxs-lookup"><span data-stu-id="909b9-275">Within the **Graph** class, add the methods **SignInAsync()** and **AquireTokenAsync()**, that will prompt the user to insert the log-in credentials.</span></span>

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

9.  <span data-ttu-id="909b9-276">Ajoutez les deux méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="909b9-276">Add the following two methods:</span></span>

    1.  <span data-ttu-id="909b9-277">**BuildTodayCalendarEndpoint()** , quelles sont les builds l’URI spécifiant le jour et l’intervalle de temps, dans lequel les réunions planifiées sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="909b9-277">**BuildTodayCalendarEndpoint()**, which builds the URI specifying the day, and time span, in which the scheduled meetings are retrieved.</span></span>

    2.  <span data-ttu-id="909b9-278">**ListMeetingsAsync()** , qui demande les réunions planifiées à partir de *Microsoft Graph*.</span><span class="sxs-lookup"><span data-stu-id="909b9-278">**ListMeetingsAsync()**, which requests the scheduled meetings from *Microsoft Graph*.</span></span>

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

10. <span data-ttu-id="909b9-279">Vous avez maintenant terminé la **Graph** script.</span><span class="sxs-lookup"><span data-stu-id="909b9-279">You have now completed the **Graph** script.</span></span> <span data-ttu-id="909b9-280">**Enregistrez vos modifications** dans Visual Studio avant de retourner à Unity.</span><span class="sxs-lookup"><span data-stu-id="909b9-280">**Save your changes** in Visual Studio before returning to Unity.</span></span>

## <a name="chapter-7---create-the-gazeinput-script"></a><span data-ttu-id="909b9-281">Chapitre 7 - créer le script GazeInput</span><span class="sxs-lookup"><span data-stu-id="909b9-281">Chapter 7 - Create the GazeInput script</span></span>

<span data-ttu-id="909b9-282">Vous allez maintenant créer le **GazeInput**.</span><span class="sxs-lookup"><span data-stu-id="909b9-282">You will now create the **GazeInput**.</span></span> <span data-ttu-id="909b9-283">Cette classe gère et effectue le suivi des regards de l’utilisateur, à l’aide un **Raycast** provenant de la **Main Camera**, projeter vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="909b9-283">This class handles and keeps track of the user's gaze, using a **Raycast** coming from the **Main Camera**, projecting forward.</span></span>

<span data-ttu-id="909b9-284">Pour créer le script :</span><span class="sxs-lookup"><span data-stu-id="909b9-284">To create the script:</span></span>

1.  <span data-ttu-id="909b9-285">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="909b9-285">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="909b9-286">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="909b9-286">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="909b9-287">Nommez le script **GazeInput**.</span><span class="sxs-lookup"><span data-stu-id="909b9-287">Name the script **GazeInput**.</span></span>

3.  <span data-ttu-id="909b9-288">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="909b9-288">Double-click on the script to open it with Visual Studio.</span></span>

4.  <span data-ttu-id="909b9-289">Modifier le code des espaces de noms pour correspondre à celui ci-dessous, ainsi que l’ajout de la ' **\[System.Serializable\]** ' balise ci-dessus votre **GazeInput** classe, afin qu’il puisse être sérialisé :</span><span class="sxs-lookup"><span data-stu-id="909b9-289">Change the namespaces code to match the one below, along with adding the '**\[System.Serializable\]**' tag above your **GazeInput** class, so that it can be serialized:</span></span>

    ```csharp
    using UnityEngine;

    /// <summary>
    /// Class responsible for the User's Gaze interactions
    /// </summary>
    [System.Serializable]
    public class GazeInput : MonoBehaviour
    {
    ```

5.  <span data-ttu-id="909b9-290">À l’intérieur de la **GazeInput** de classe, ajoutez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="909b9-290">Inside the **GazeInput** class, add the following variables:</span></span>

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

6.  <span data-ttu-id="909b9-291">Ajouter le **CreateCursor()** pour créer le curseur HoloLens dans la scène et appelez la méthode depuis le **Start()** méthode :</span><span class="sxs-lookup"><span data-stu-id="909b9-291">Add the **CreateCursor()** method to create the HoloLens cursor in the scene, and call the method from the **Start()** method:</span></span>

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

7.  <span data-ttu-id="909b9-292">Les méthodes suivantes permettent les regards Raycast et de suivre les objets ayant le focus.</span><span class="sxs-lookup"><span data-stu-id="909b9-292">The following methods enable the gaze Raycast and keep track of the focused objects.</span></span>

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

8.  <span data-ttu-id="909b9-293">**Enregistrez vos modifications** dans Visual Studio avant de retourner à Unity.</span><span class="sxs-lookup"><span data-stu-id="909b9-293">**Save your changes** in Visual Studio before returning to Unity.</span></span>

## <a name="chapter-8---create-the-interactions-class"></a><span data-ttu-id="909b9-294">Chapitre 8 - créer la classe d’Interactions</span><span class="sxs-lookup"><span data-stu-id="909b9-294">Chapter 8 - Create the Interactions class</span></span>

<span data-ttu-id="909b9-295">Vous devez maintenant créer le **Interactions** script, qui est chargé de :</span><span class="sxs-lookup"><span data-stu-id="909b9-295">You will now need to create the **Interactions** script, which is responsible for:</span></span>

-   <span data-ttu-id="909b9-296">Gestion de la **appuyez sur** interaction et la **utilisation de l’appareil photo**, ce qui permet à l’utilisateur d’interagir avec le journal dans le « bouton » dans la scène.</span><span class="sxs-lookup"><span data-stu-id="909b9-296">Handling the **Tap** interaction and the **Camera Gaze**, which enables the user to interact with the log in "button" in the scene.</span></span>

-   <span data-ttu-id="909b9-297">Création du journal dans l’objet « bouton » dans la scène pour l’utilisateur d’interagir avec.</span><span class="sxs-lookup"><span data-stu-id="909b9-297">Creating the log in "button" object in the scene for the user to interact with.</span></span>

<span data-ttu-id="909b9-298">Pour créer le script :</span><span class="sxs-lookup"><span data-stu-id="909b9-298">To create the script:</span></span>

1.  <span data-ttu-id="909b9-299">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="909b9-299">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="909b9-300">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="909b9-300">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="909b9-301">Nommez le script **Interactions**.</span><span class="sxs-lookup"><span data-stu-id="909b9-301">Name the script **Interactions**.</span></span>

3.  <span data-ttu-id="909b9-302">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="909b9-302">Double-click on the script to open it with Visual Studio.</span></span>

4.  <span data-ttu-id="909b9-303">Insérer des espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="909b9-303">Insert the following namespaces:</span></span>

    ```csharp
    using UnityEngine;
    using UnityEngine.XR.WSA.Input;
    ```

5.  <span data-ttu-id="909b9-304">Modifier l’héritage de la **Interaction** classe *MonoBehaviour* à **GazeInput**.</span><span class="sxs-lookup"><span data-stu-id="909b9-304">Change the inheritance of the **Interaction** class from *MonoBehaviour* to **GazeInput**.</span></span>

    <span data-ttu-id="909b9-305">~~Interactions de classe publique : MonoBehaviour~~</span><span class="sxs-lookup"><span data-stu-id="909b9-305">~~public class Interactions : MonoBehaviour~~</span></span>

    ```csharp
    public class Interactions : GazeInput
    ```

6.  <span data-ttu-id="909b9-306">À l’intérieur de la **Interaction** classe insérer la variable suivante :</span><span class="sxs-lookup"><span data-stu-id="909b9-306">Inside the **Interaction** class insert the following variable:</span></span>

    ```csharp
        /// <summary>
        /// Allows input recognition with the HoloLens
        /// </summary>
        private GestureRecognizer _gestureRecognizer;
    ```

7.  <span data-ttu-id="909b9-307">Remplacez le **Démarrer** méthode ; Notez qu’il est une méthode de remplacement, qui appelle la méthode de classe du pointage de regard 'base'.</span><span class="sxs-lookup"><span data-stu-id="909b9-307">Replace the **Start** method; notice it is an override method, which calls the 'base' Gaze class method.</span></span> <span data-ttu-id="909b9-308">**Start()** sera appelé lors de l’initialisation de la classe, l’inscription pour la reconnaissance d’entrée et la création de la connexion *bouton* dans la scène :</span><span class="sxs-lookup"><span data-stu-id="909b9-308">**Start()** will be called when the class initializes, registering for input recognition and creating the sign in *button* in the scene:</span></span>

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

8.  <span data-ttu-id="909b9-309">Ajouter le **CreateSignInButton()** méthode qui instancie le signe dans *bouton* dans la scène et définissez ses propriétés :</span><span class="sxs-lookup"><span data-stu-id="909b9-309">Add the **CreateSignInButton()** method, which will instantiate the sign in *button* in the scene and set its properties:</span></span>

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

9.  <span data-ttu-id="909b9-310">Ajouter le **GestureRecognizer_Tapped()** (méthode), être répondre pour le *appuyez sur* événement utilisateur.</span><span class="sxs-lookup"><span data-stu-id="909b9-310">Add the **GestureRecognizer_Tapped()** method, which be respond for the *Tap* user event.</span></span>

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

10. <span data-ttu-id="909b9-311">**Supprimer** le **Update()** (méthode), puis **enregistrer vos modifications** dans Visual Studio avant de retourner à Unity.</span><span class="sxs-lookup"><span data-stu-id="909b9-311">**Delete** the **Update()** method, and then **save your changes** in Visual Studio before returning to Unity.</span></span>

## <a name="chapter-9---set-up-the-script-references"></a><span data-ttu-id="909b9-312">Chapitre 9 - configurer les références de script</span><span class="sxs-lookup"><span data-stu-id="909b9-312">Chapter 9 - Set up the script references</span></span>

<span data-ttu-id="909b9-313">Dans ce chapitre, vous devez placer le **Interactions** de script sur le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="909b9-313">In this Chapter you need to place the **Interactions** script onto the **Main Camera**.</span></span> <span data-ttu-id="909b9-314">Ce script gère à placer les autres scripts où ils doivent être.</span><span class="sxs-lookup"><span data-stu-id="909b9-314">That script will then handle placing the other scripts where they need to be.</span></span>

-  <span data-ttu-id="909b9-315">À partir de la **Scripts** dossier dans le *panneau projet*, faites glisser le script **Interactions** à la **Main Camera** de l’objet, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="909b9-315">From the **Scripts** folder in the *Project Panel*, drag the script **Interactions** to the **Main Camera** object, as pictured below.</span></span>

    ![](images/AzureLabs-Lab311-29.png)

## <a name="chapter-10---setting-up-the-tag"></a><span data-ttu-id="909b9-316">Chapitre 10 - Configuration de la balise</span><span class="sxs-lookup"><span data-stu-id="909b9-316">Chapter 10 - Setting up the Tag</span></span>

<span data-ttu-id="909b9-317">Le code qui gère les regards utilisera la balise **SignInButton** pour identifier quel objet de l’utilisateur interagit pour se connecter à *Microsoft Graph*.</span><span class="sxs-lookup"><span data-stu-id="909b9-317">The code handling the gaze will make use of the Tag **SignInButton** to identify which object the user will interact with to sign-in to *Microsoft Graph*.</span></span>

<span data-ttu-id="909b9-318">Pour créer la balise :</span><span class="sxs-lookup"><span data-stu-id="909b9-318">To create the Tag:</span></span>

1.  <span data-ttu-id="909b9-319">Dans l’éditeur Unity, cliquez sur le **Main Camera** dans le *hiérarchie panneau*.</span><span class="sxs-lookup"><span data-stu-id="909b9-319">In the Unity Editor click on the **Main Camera** in the *Hierarchy Panel*.</span></span>

2.  <span data-ttu-id="909b9-320">Dans le *panneau Inspecteur* cliquez sur le **MainCamera** *balise* pour ouvrir la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="909b9-320">In the *Inspector Panel* click on the **MainCamera** *Tag* to open a drop-down list.</span></span> <span data-ttu-id="909b9-321">Cliquez sur **ajouter une balise...**</span><span class="sxs-lookup"><span data-stu-id="909b9-321">Click on **Add Tag...**</span></span>

    ![](images/AzureLabs-Lab311-30.png)

3.  <span data-ttu-id="909b9-322">Cliquez sur le **+** bouton.</span><span class="sxs-lookup"><span data-stu-id="909b9-322">Click on the **+** button.</span></span>

    ![](images/AzureLabs-Lab311-31.png)

4.  <span data-ttu-id="909b9-323">Écrivez le nom de balise en tant que **SignInButton** et cliquez sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="909b9-323">Write the Tag name as **SignInButton** and click Save.</span></span>

    ![](images/AzureLabs-Lab311-32.png)

## <a name="chapter-11---build-the-unity-project-to-uwp"></a><span data-ttu-id="909b9-324">Chapitre 11 - générer le projet Unity vers UWP</span><span class="sxs-lookup"><span data-stu-id="909b9-324">Chapter 11 - Build the Unity project to UWP</span></span>

<span data-ttu-id="909b9-325">Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée, il est temps de générer à partir de Unity.</span><span class="sxs-lookup"><span data-stu-id="909b9-325">Everything needed for the Unity section of this project has now been completed, so it is time to build it from Unity.</span></span>

1.  <span data-ttu-id="909b9-326">Accédez à *les paramètres de génération* (\**fichier* > \*Build paramètres\*\*).</span><span class="sxs-lookup"><span data-stu-id="909b9-326">Navigate to *Build Settings* (\**File* > \*Build Settings\*\*).</span></span>

    ![](images/AzureLabs-Lab311-33.png)

2.  <span data-ttu-id="909b9-327">Si pas déjà fait, cochez **Unity C\# projets**.</span><span class="sxs-lookup"><span data-stu-id="909b9-327">If not already, tick **Unity C\# Projects**.</span></span>

3.  <span data-ttu-id="909b9-328">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="909b9-328">Click **Build**.</span></span> <span data-ttu-id="909b9-329">Unity lancera un **Explorateur de fichiers** fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans.</span><span class="sxs-lookup"><span data-stu-id="909b9-329">Unity will launch a **File Explorer** window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="909b9-330">Créez ce dossier, puis nommez-le **application**.</span><span class="sxs-lookup"><span data-stu-id="909b9-330">Create that folder now, and name it **App**.</span></span> <span data-ttu-id="909b9-331">Ensuite avec le **application** dossier sélectionné, cliquez sur **sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="909b9-331">Then with the **App** folder selected, click **Select Folder**.</span></span>

4.  <span data-ttu-id="909b9-332">Unity commencera à générer votre projet pour le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="909b9-332">Unity will begin building your project to the **App** folder.</span></span>

5.  <span data-ttu-id="909b9-333">Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un **Explorateur de fichiers** fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).</span><span class="sxs-lookup"><span data-stu-id="909b9-333">Once Unity has finished building (it might take some time), it will open a **File Explorer** window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

## <a name="chapter-12---deploy-to-hololens"></a><span data-ttu-id="909b9-334">Chapitre 12 - déployer sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="909b9-334">Chapter 12 - Deploy to HoloLens</span></span>

<span data-ttu-id="909b9-335">Pour déployer sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="909b9-335">To deploy on HoloLens:</span></span>

1.  <span data-ttu-id="909b9-336">Vous devez l’adresse IP de votre HoloLens (pour les déployer à distance) et pour vérifier que votre HoloLens est dans **Mode développeur.**</span><span class="sxs-lookup"><span data-stu-id="909b9-336">You will need the IP Address of your HoloLens (for Remote Deploy), and to ensure your HoloLens is in **Developer Mode.**</span></span> <span data-ttu-id="909b9-337">Pour cela, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="909b9-337">To do this:</span></span>

    1.  <span data-ttu-id="909b9-338">Tout en portant vos HoloLens, ouvrez le **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="909b9-338">Whilst wearing your HoloLens, open the **Settings**.</span></span>

    2.  <span data-ttu-id="909b9-339">Accédez à **réseau & Internet** > **Wi-Fi** > **les Options avancées**</span><span class="sxs-lookup"><span data-stu-id="909b9-339">Go to **Network & Internet** > **Wi-Fi** > **Advanced Options**</span></span>

    3.  <span data-ttu-id="909b9-340">Remarque la **IPv4** adresse.</span><span class="sxs-lookup"><span data-stu-id="909b9-340">Note the **IPv4** address.</span></span>

    4.  <span data-ttu-id="909b9-341">Ensuite, accédez à **paramètres**, puis à **mise à jour & sécurité** > **pour les développeurs**</span><span class="sxs-lookup"><span data-stu-id="909b9-341">Next, navigate back to **Settings**, and then to **Update & Security** > **For Developers**</span></span>

    5.  <span data-ttu-id="909b9-342">Définissez **Mode développeur sur**.</span><span class="sxs-lookup"><span data-stu-id="909b9-342">Set **Developer Mode On**.</span></span>

2.  <span data-ttu-id="909b9-343">Accédez à votre nouvelle build Unity (le **application** dossier) et ouvrez le fichier solution avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="909b9-343">Navigate to your new Unity build (the **App** folder) and open the solution file with **Visual Studio**.</span></span>

3.  <span data-ttu-id="909b9-344">Dans le **Configuration de la Solution** sélectionnez **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="909b9-344">In the **Solution Configuration** select **Debug**.</span></span>

4.  <span data-ttu-id="909b9-345">Dans le **plateforme de Solution**, sélectionnez **x86, ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="909b9-345">In the **Solution Platform**, select **x86, Remote Machine**.</span></span> <span data-ttu-id="909b9-346">Vous devrez insérer le **adresse IP** d’un appareil à distance (la HoloLens, dans ce cas, que vous avez notée).</span><span class="sxs-lookup"><span data-stu-id="909b9-346">You will be prompted to insert the **IP address** of a remote device (the HoloLens, in this case, which you noted).</span></span>

    ![](images/AzureLabs-Lab311-34.png)

5.  <span data-ttu-id="909b9-347">Accédez à **Build** menu et cliquez sur **déployer la Solution** à chargement indépendant de l’application à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="909b9-347">Go to **Build** menu and click on **Deploy Solution** to sideload the application to your HoloLens.</span></span>

6.  <span data-ttu-id="909b9-348">Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prêt à être lancé !</span><span class="sxs-lookup"><span data-stu-id="909b9-348">Your app should now appear in the list of installed apps on your HoloLens, ready to be launched!</span></span>

## <a name="your-microsoft-graph-hololens-application"></a><span data-ttu-id="909b9-349">Votre application Microsoft Graph HoloLens</span><span class="sxs-lookup"><span data-stu-id="909b9-349">Your Microsoft Graph HoloLens application</span></span>

<span data-ttu-id="909b9-350">Félicitations, vous avez créé une application de réalité mixte qui tire parti de Microsoft Graph pour lire et afficher les données de calendrier d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="909b9-350">Congratulations, you built a mixed reality app that leverages the Microsoft Graph, to read and display user Calendar data.</span></span>

![](images/AzureLabs-Lab311-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="909b9-351">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="909b9-351">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="909b9-352">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="909b9-352">Exercise 1</span></span>

<span data-ttu-id="909b9-353">Microsoft Graph permet d’afficher d’autres informations sur l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="909b9-353">Use Microsoft Graph to display other information about the user</span></span>

-   <span data-ttu-id="909b9-354">E-mail de l’utilisateur / numéro de téléphone / image de profil</span><span class="sxs-lookup"><span data-stu-id="909b9-354">User email / phone number / profile picture</span></span>

### <a name="exercise-1"></a><span data-ttu-id="909b9-355">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="909b9-355">Exercise 1</span></span>

<span data-ttu-id="909b9-356">Implémenter le contrôle de voix pour naviguer de l’interface utilisateur graphique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="909b9-356">Implement voice control to navigate the Microsoft Graph UI.</span></span>
