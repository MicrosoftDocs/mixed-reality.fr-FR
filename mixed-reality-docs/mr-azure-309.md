---
title: MR et Azure 309-application Insights
description: Suivez ce cours pour apprendre à collecter des analyses concernant le comportement des utilisateurs au sein d’une application de réalité mixte, à l’aide du service Azure Application Insights.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Académie, Unity, didacticiel, API, application Insights, hololens, immersif, VR
ms.openlocfilehash: e14a32f9a38e3e8f3054d19310782f7c2d4784a1
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694570"
---
>[!NOTE]
><span data-ttu-id="58697-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="58697-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="58697-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="58697-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="58697-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="58697-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="58697-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="58697-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="58697-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="58697-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="58697-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="58697-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br> 

# <a name="mr-and-azure-309-application-insights"></a><span data-ttu-id="58697-110">MR et Azure 309: Application Insights</span><span class="sxs-lookup"><span data-stu-id="58697-110">MR and Azure 309: Application insights</span></span>

![produit final-début](images/AzureLabs-Lab309-00.png)

<span data-ttu-id="58697-112">Dans ce cours, vous allez apprendre à ajouter des fonctionnalités de Application Insights à une application de réalité mixte, à l’aide de l’API Azure Application Insights pour collecter des analyses concernant le comportement des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="58697-112">In this course, you will learn how to add Application Insights capabilities to a mixed reality application, using the Azure Application Insights API to collect analytics regarding user behavior.</span></span>

<span data-ttu-id="58697-113">Application Insights est un service Microsoft qui permet aux développeurs de collecter des analyses à partir de leurs applications et de les gérer à partir d’un portail facile à utiliser.</span><span class="sxs-lookup"><span data-stu-id="58697-113">Application Insights is a Microsoft service, allowing developers to collect analytics from their applications and manage it from an easy-to-use portal.</span></span> <span data-ttu-id="58697-114">Les analyses peuvent avoir n’importe quelle valeur, des performances aux informations personnalisées que vous souhaitez collecter.</span><span class="sxs-lookup"><span data-stu-id="58697-114">The analytics can be anything from performance to custom information you would like to collect.</span></span> <span data-ttu-id="58697-115">Pour plus d’informations, consultez la [page application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="58697-115">For more information, visit the [Application Insights page](https://azure.microsoft.com/services/application-insights/).</span></span>

<span data-ttu-id="58697-116">Une fois ce cours terminé, vous disposerez d’une application de casque immersif en réalité mixte, qui sera en mesure d’effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="58697-116">Having completed this course, you will have a mixed reality immersive headset application which will be able to do the following:</span></span>

1.  <span data-ttu-id="58697-117">Autorisez l’utilisateur à se déplacer dans une scène.</span><span class="sxs-lookup"><span data-stu-id="58697-117">Allow the user to gaze and move around a scene.</span></span>
2.  <span data-ttu-id="58697-118">Déclencher l’envoi des analyses au *Service application Insights*, par le biais de l’utilisation du regard et de la proximité des objets dans la scène.</span><span class="sxs-lookup"><span data-stu-id="58697-118">Trigger the sending of analytics to the *Application Insights Service*, through the use of Gaze and Proximity to in-scene objects.</span></span>
3.  <span data-ttu-id="58697-119">L’application appellera également sur le service, en extrayant les informations sur l’objet qui a été approché le plus par l’utilisateur au cours des dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="58697-119">The app will also call upon the Service, fetching information about which object has been approached the most by the user, within the last 24 hours.</span></span> <span data-ttu-id="58697-120">Cet objet va changer sa couleur en vert.</span><span class="sxs-lookup"><span data-stu-id="58697-120">That object will change its color to green.</span></span>

<span data-ttu-id="58697-121">Ce cours vous apprend à obtenir les résultats du service Application Insights, dans un exemple d’application à base d’Unity.</span><span class="sxs-lookup"><span data-stu-id="58697-121">This course will teach you how to get the results from the Application Insights Service, into a Unity-based sample application.</span></span> <span data-ttu-id="58697-122">Il vous faudra appliquer ces concepts à une application personnalisée que vous pouvez générer.</span><span class="sxs-lookup"><span data-stu-id="58697-122">It will be up to you to apply these concepts to a custom application you might be building.</span></span>

## <a name="device-support"></a><span data-ttu-id="58697-123">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="58697-123">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="58697-124">Course</span><span class="sxs-lookup"><span data-stu-id="58697-124">Course</span></span></th><th style="width:150px"> <span data-ttu-id="58697-125"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="58697-125"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="58697-126"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="58697-126"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="58697-127">MR et Azure 309: Application Insights</span><span class="sxs-lookup"><span data-stu-id="58697-127">MR and Azure 309: Application insights</span></span></td><td style="text-align: center;"> <span data-ttu-id="58697-128">✔️</span><span class="sxs-lookup"><span data-stu-id="58697-128">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="58697-129">✔️</span><span class="sxs-lookup"><span data-stu-id="58697-129">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="58697-130">Bien que ce cours se concentre principalement sur les casques de Windows Mixed Reality (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours à Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="58697-130">While this course primarily focuses on Windows Mixed Reality immersive (VR) headsets, you can also apply what you learn in this course to Microsoft HoloLens.</span></span> <span data-ttu-id="58697-131">À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge HoloLens.</span><span class="sxs-lookup"><span data-stu-id="58697-131">As you follow along with the course, you will see notes on any changes you might need to employ to support HoloLens.</span></span> <span data-ttu-id="58697-132">Lorsque vous utilisez HoloLens, vous remarquerez peut-être un écho pendant la capture vocale.</span><span class="sxs-lookup"><span data-stu-id="58697-132">When using HoloLens, you may notice some echo during voice capture.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58697-133">Prérequis</span><span class="sxs-lookup"><span data-stu-id="58697-133">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="58697-134">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="58697-134">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="58697-135">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de la rédaction (juillet 2018).</span><span class="sxs-lookup"><span data-stu-id="58697-135">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (July 2018).</span></span> <span data-ttu-id="58697-136">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="58697-136">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you will find in newer software than what is listed below.</span></span>

<span data-ttu-id="58697-137">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:</span><span class="sxs-lookup"><span data-stu-id="58697-137">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="58697-138">Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)</span><span class="sxs-lookup"><span data-stu-id="58697-138">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="58697-139">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="58697-139">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="58697-140">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="58697-140">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="58697-141">Unity 2017,4</span><span class="sxs-lookup"><span data-stu-id="58697-141">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="58697-142">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="58697-142">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="58697-143">Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="58697-143">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="58697-144">Un jeu de casque avec un microphone intégré (si le casque n’a pas de MIC et de haut-parleurs intégrés)</span><span class="sxs-lookup"><span data-stu-id="58697-144">A set of headphones with a built-in microphone (if the headset does not have a built-in mic and speakers)</span></span>
- <span data-ttu-id="58697-145">Accès Internet pour l’installation d’Azure et la récupération des données de Application Insights</span><span class="sxs-lookup"><span data-stu-id="58697-145">Internet access for Azure setup and Application Insights data retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="58697-146">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="58697-146">Before you start</span></span>

<span data-ttu-id="58697-147">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="58697-147">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>

> [!WARNING] 
> <span data-ttu-id="58697-148">N’oubliez pas que les données qui vont *application Insights* prennent du temps, donc soyez patient.</span><span class="sxs-lookup"><span data-stu-id="58697-148">Be aware, data going to *Application Insights* takes time, so be patient.</span></span> <span data-ttu-id="58697-149">Si vous souhaitez vérifier si le service a reçu vos données, consultez le [chapitre 14](#chapter-14---the-application-insights-service-portal), qui vous montrera comment naviguer dans le portail.</span><span class="sxs-lookup"><span data-stu-id="58697-149">If you want to check if the Service has received your data, check out [Chapter 14](#chapter-14---the-application-insights-service-portal), which will show you how to navigate the portal.</span></span>

## <a name="chapter-1---the-azure-portal"></a><span data-ttu-id="58697-150">Chapitre 1-portail Azure</span><span class="sxs-lookup"><span data-stu-id="58697-150">Chapter 1 - The Azure Portal</span></span>

<span data-ttu-id="58697-151">Pour utiliser *application Insights*, vous devez créer et configurer un *Service Application Insights* dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="58697-151">To use *Application Insights*, you will need to create and configure an *Application Insights Service* in the Azure portal.</span></span>

1.  <span data-ttu-id="58697-152">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="58697-152">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE]
    > <span data-ttu-id="58697-153">Si vous n’avez pas encore de compte Azure, vous devez en créer un.</span><span class="sxs-lookup"><span data-stu-id="58697-153">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="58697-154">Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="58697-154">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="58697-155">Une fois que vous êtes connecté, cliquez sur **nouveau** dans l’angle supérieur gauche, recherchez *application Insights*, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="58697-155">Once you are logged in, click on **New** in the top left corner, and search for *Application Insights*, and click **Enter**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="58697-156">Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.</span><span class="sxs-lookup"><span data-stu-id="58697-156">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-01.png)

3.  <span data-ttu-id="58697-158">La nouvelle page qui s’affiche à droite fournit une description du service *Azure application Insights* .</span><span class="sxs-lookup"><span data-stu-id="58697-158">The new page to the right will provide a description of the *Azure Application Insights* Service.</span></span> <span data-ttu-id="58697-159">En bas à gauche de cette page, cliquez sur le bouton **créer** pour créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="58697-159">At the bottom left of this page, select the **Create** button, to create an association with this Service.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-02.png)

4.  <span data-ttu-id="58697-161">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="58697-161">Once you have clicked on **Create**:</span></span>

    1.  <span data-ttu-id="58697-162">Insérez le **nom** de votre choix pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="58697-162">Insert your desired **Name** for this Service instance.</span></span>

    2.  <span data-ttu-id="58697-163">Pour **type d’application**, sélectionnez **général**.</span><span class="sxs-lookup"><span data-stu-id="58697-163">As **Application Type**, select **General**.</span></span>

    3.  <span data-ttu-id="58697-164">Sélectionnez un **abonnement**approprié.</span><span class="sxs-lookup"><span data-stu-id="58697-164">Select an appropriate **Subscription**.</span></span>

    4.  <span data-ttu-id="58697-165">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="58697-165">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="58697-166">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="58697-166">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="58697-167">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.</span><span class="sxs-lookup"><span data-stu-id="58697-167">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

        > <span data-ttu-id="58697-168">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="58697-168">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5.  <span data-ttu-id="58697-169">Sélectionnez un **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="58697-169">Select a **Location**.</span></span>

    6.  <span data-ttu-id="58697-170">Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.</span><span class="sxs-lookup"><span data-stu-id="58697-170">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    7.  <span data-ttu-id="58697-171">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="58697-171">Select **Create**.</span></span>

        ![Portail Azure](images/AzureLabs-Lab309-03.png)

5.  <span data-ttu-id="58697-173">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="58697-173">Once you have clicked on **Create**, you will have to wait for the Service to be created, this might take a minute.</span></span>

6.  <span data-ttu-id="58697-174">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="58697-174">A notification will appear in the portal once the Service instance is created.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-04.png)

7.  <span data-ttu-id="58697-176">Cliquez sur les notifications pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="58697-176">Click on the notifications to explore your new Service instance.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-05.png)

8.  <span data-ttu-id="58697-178">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="58697-178">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="58697-179">Vous êtes dirigé vers votre nouvelle instance de *Service application Insights* .</span><span class="sxs-lookup"><span data-stu-id="58697-179">You will be taken to your new *Application Insights Service* instance.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-06.png)

    > [!NOTE]
    >  <span data-ttu-id="58697-181">Gardez cette page Web ouverte et facile à consulter. vous y reviendrez souvent pour voir les données collectées.</span><span class="sxs-lookup"><span data-stu-id="58697-181">Keep this web page open and easy to access, you will come back here often to see the data collected.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="58697-182">Pour implémenter Application Insights, vous devrez utiliser trois (3) valeurs spécifiques: **Clé**d’instrumentation, **ID d’application**et **clé API**.</span><span class="sxs-lookup"><span data-stu-id="58697-182">To implement Application Insights, you will need to use three (3) specific values: **Instrumentation Key**, **Application ID**, and **API Key**.</span></span> <span data-ttu-id="58697-183">Vous verrez ci-dessous comment récupérer ces valeurs à partir de votre service.</span><span class="sxs-lookup"><span data-stu-id="58697-183">Below you will see how to retrieve these values from your Service.</span></span> <span data-ttu-id="58697-184">Veillez à noter ces valeurs dans une page vide du *bloc-notes* , car vous les utiliserez bientôt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="58697-184">Make sure to note these values on a blank *Notepad* page, because you will use them soon in your code.</span></span>

9.  <span data-ttu-id="58697-185">Pour trouver la **clé**d’instrumentation, vous devez faire défiler la liste des fonctions de service, puis cliquer sur **Propriétés**. l’onglet affiché affiche la **clé de service**.</span><span class="sxs-lookup"><span data-stu-id="58697-185">To find the **Instrumentation Key**, you will need to scroll down the list of Service functions, and click on **Properties**, the tab displayed will reveal the **Service Key**.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-07.png)

10. <span data-ttu-id="58697-187">Une petite des **Propriétés**ci-dessous vous permet d' **accéder à l’API**, sur laquelle vous devez cliquer.</span><span class="sxs-lookup"><span data-stu-id="58697-187">A little below **Properties**, you will find **API Access**, which you need to click.</span></span> <span data-ttu-id="58697-188">Le panneau à droite fournit l’ID d' **application** de votre application.</span><span class="sxs-lookup"><span data-stu-id="58697-188">The panel to the right will provide the **Application ID** of your app.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-08.png)

11. <span data-ttu-id="58697-190">Si le panneau de l’ID de l' **application** est toujours ouvert, cliquez sur **créer une clé API**pour ouvrir le panneau *créer une clé API* .</span><span class="sxs-lookup"><span data-stu-id="58697-190">With the **Application ID** panel still open, click **Create API Key**, which will open the *Create API key* panel.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-09.png)

12. <span data-ttu-id="58697-192">Dans le volet créer maintenant une *clé d’API* , tapez une description et **cochez les trois cases**.</span><span class="sxs-lookup"><span data-stu-id="58697-192">Within the now open *Create API key* panel, type a description, and **tick the three boxes**.</span></span>

13. <span data-ttu-id="58697-193">Cliquez sur **générer la clé**.</span><span class="sxs-lookup"><span data-stu-id="58697-193">Click **Generate Key**.</span></span> <span data-ttu-id="58697-194">Votre **clé API** sera créée et affichée.</span><span class="sxs-lookup"><span data-stu-id="58697-194">Your **API Key** will be created and displayed.</span></span> 

    ![Portail Azure](images/AzureLabs-Lab309-10.png)
        
    > [!WARNING]
    > <span data-ttu-id="58697-196">Il s’agit de la seule fois où votre **clé de service** sera affichée. Veillez donc à en faire une copie maintenant.</span><span class="sxs-lookup"><span data-stu-id="58697-196">This is the only time your **Service Key** will be displayed, so ensure you make a copy of it now.</span></span>

## <a name="chapter-2---set-up-the-unity-project"></a><span data-ttu-id="58697-197">Chapitre 2-configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="58697-197">Chapter 2 - Set up the Unity project</span></span>

<span data-ttu-id="58697-198">Ce qui suit est une configuration classique pour le développement avec la réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="58697-198">The following is a typical set up for developing with the mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="58697-199">Ouvrez *Unity* et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="58697-199">Open *Unity* and click **New**.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab309-11.png)

2.  <span data-ttu-id="58697-201">Vous devez maintenant fournir un nom de projet Unity, insérer **Mr\_Azure\_application\_Insights**.</span><span class="sxs-lookup"><span data-stu-id="58697-201">You will now need to provide a Unity Project name, insert **MR\_Azure\_Application\_Insights**.</span></span> <span data-ttu-id="58697-202">Assurez-vous que le *modèle* est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="58697-202">Make sure the *Template* is set to **3D**.</span></span> <span data-ttu-id="58697-203">Définissez l' *emplacement* approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés).</span><span class="sxs-lookup"><span data-stu-id="58697-203">Set the *Location* to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="58697-204">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="58697-204">Then, click **Create project**.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab309-12.png)

3.  <span data-ttu-id="58697-206">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="58697-206">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="58697-207">Accédez à **modifier \> les préférences** , puis à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="58697-207">Go to **Edit \> Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="58697-208">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="58697-208">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="58697-209">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="58697-209">Close the **Preferences** window.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab309-13.png)

4.  <span data-ttu-id="58697-211">Ensuite, accédez à **fichier \> paramètres de build** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton **changer de plateforme** .</span><span class="sxs-lookup"><span data-stu-id="58697-211">Next, go to **File \> Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab309-14.png)

5.  <span data-ttu-id="58697-213">Accédez à **fichier \> paramètres de build** et assurez-vous que:</span><span class="sxs-lookup"><span data-stu-id="58697-213">Go to **File \> Build Settings** and make sure that:</span></span>

    1.  <span data-ttu-id="58697-214">L' **appareil cible** est défini sur **n’importe quel appareil**</span><span class="sxs-lookup"><span data-stu-id="58697-214">**Target Device** is set to **Any device**</span></span>

        > <span data-ttu-id="58697-215">Pour Microsoft HoloLens, définissez **appareil cible** sur *HoloLens*.</span><span class="sxs-lookup"><span data-stu-id="58697-215">For the Microsoft HoloLens, set **Target Device** to *HoloLens*.</span></span>

    2.  <span data-ttu-id="58697-216">Le **type de build** est **D3D**</span><span class="sxs-lookup"><span data-stu-id="58697-216">**Build Type** is set to **D3D**</span></span>

    3.  <span data-ttu-id="58697-217">Le **SDK** est configuré sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="58697-217">**SDK** is set to **Latest installed**</span></span>

    4.  <span data-ttu-id="58697-218">La **génération et l’exécution** sont définies sur l' **ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="58697-218">**Build and Run** is set to **Local Machine**</span></span>

    5.  <span data-ttu-id="58697-219">Enregistrez la scène et ajoutez-la à la Build.</span><span class="sxs-lookup"><span data-stu-id="58697-219">Save the scene and add it to the build.</span></span>

        1.  <span data-ttu-id="58697-220">Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="58697-220">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="58697-221">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="58697-221">A save window will appear.</span></span>

            ![Configurer le projet Unity](images/AzureLabs-Lab309-15.png)

        2. <span data-ttu-id="58697-223">Créez un nouveau dossier pour cela, ainsi que toute scène future, puis cliquez sur le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez-le Scenes.</span><span class="sxs-lookup"><span data-stu-id="58697-223">Create a new folder for this, and any future scene, then click the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![Configurer le projet Unity](images/AzureLabs-Lab309-16.png)

        3. <span data-ttu-id="58697-225">Ouvrez le dossier scenes nouvellement créé, puis dans le champ *nom de fichier:* , tapez **ApplicationInsightsScene**, puis cliquez sur  **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="58697-225">Open your newly created **Scenes** folder, and then in the *File name:* text field, type **ApplicationInsightsScene**, then click **Save**.</span></span>

            ![Configurer le projet Unity](images/AzureLabs-Lab309-17.png)

6.  <span data-ttu-id="58697-227">Les paramètres restants, dans **paramètres de build**, doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="58697-227">The remaining settings, in **Build Settings**, should be left as default for now.</span></span>

7.  <span data-ttu-id="58697-228">Dans la fenêtre **paramètres de build** , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="58697-228">In the **Build Settings** window, click on the **Player Settings** button, this will open the related panel in the space where the **Inspector** is located.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab309-18.png)

8. <span data-ttu-id="58697-230">Dans ce volet, quelques paramètres doivent être vérifiés:</span><span class="sxs-lookup"><span data-stu-id="58697-230">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="58697-231">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="58697-231">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="58697-232">**Scripts** La **version du runtime** doit être **expérimentale (.net 4,6 équivalent)** , qui déclenchera un redémarrage de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="58697-232">**Scripting** **Runtime Version** should be **Experimental (.NET 4.6 Equivalent)**, which will trigger a need to restart the Editor.</span></span>

        2.  <span data-ttu-id="58697-233">Le **backend de script** doit être **.net**</span><span class="sxs-lookup"><span data-stu-id="58697-233">**Scripting Backend** should be **.NET**</span></span>

        3.  <span data-ttu-id="58697-234">Le **niveau de compatibilité** de l’API doit être **.net 4,6**</span><span class="sxs-lookup"><span data-stu-id="58697-234">**API Compatibility Level** should be **.NET 4.6**</span></span>

        ![Configurer le projet Unity](images/AzureLabs-Lab309-19.png)

    2.  <span data-ttu-id="58697-236">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:</span><span class="sxs-lookup"><span data-stu-id="58697-236">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="58697-237">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="58697-237">**InternetClient**</span></span>     

            ![Configurer le projet Unity](images/AzureLabs-Lab309-20.png)

    3.  <span data-ttu-id="58697-239">Plus bas dans le panneau, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="58697-239">Further down the panel, in **XR Settings** (found below **Publishing Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Configurer le projet Unity](images/AzureLabs-Lab309-21.png)

9.  <span data-ttu-id="58697-241">De retour dans les **paramètres de build**, les **projets C# Unity** ne sont plus grisés. Cochez la case en regard de cette option.</span><span class="sxs-lookup"><span data-stu-id="58697-241">Back in **Build Settings**, **Unity C# Projects** is no longer greyed out; tick the checkbox next to this.</span></span>

10.  <span data-ttu-id="58697-242">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="58697-242">Close the Build Settings window.</span></span>

11.  <span data-ttu-id="58697-243">Enregistrez votre scène et votre projet (**fichier** > **Save Scene/file** > **Save Project**).</span><span class="sxs-lookup"><span data-stu-id="58697-243">Save your Scene and Project (**FILE** > **SAVE SCENE / FILE** > **SAVE PROJECT**).</span></span>


## <a name="chapter-3---import-the-unity-package"></a><span data-ttu-id="58697-244">Chapitre 3-importer le package Unity</span><span class="sxs-lookup"><span data-stu-id="58697-244">Chapter 3 - Import the Unity package</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58697-245">Si vous souhaitez ignorer les composants de *configuration* d’Unity de ce cours et continuer à accéder directement au code, n’hésitez pas à télécharger ce fichier [Azure-Mr-309. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20309%20-%20Application%20insights/Azure-MR-309.unitypackage), importez-le dans votre projet en tant que [**package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html).</span><span class="sxs-lookup"><span data-stu-id="58697-245">If you wish to skip the *Unity Set up* components of this course, and continue straight into code, feel free to download this [Azure-MR-309.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20309%20-%20Application%20insights/Azure-MR-309.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html).</span></span> <span data-ttu-id="58697-246">Elle contient également les dll du chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="58697-246">This will also contain the DLLs from the next Chapter.</span></span> <span data-ttu-id="58697-247">Après l’importation, passez [**au chapitre 6**](#chapter-6---create-the-applicationinsightstracker-class).</span><span class="sxs-lookup"><span data-stu-id="58697-247">After import, continue from [**Chapter 6**](#chapter-6---create-the-applicationinsightstracker-class).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58697-248">Pour utiliser Application Insights dans Unity, vous devez importer la DLL associée, ainsi que la DLL Newtonsoft.</span><span class="sxs-lookup"><span data-stu-id="58697-248">To use Application Insights within Unity, you need to import the DLL for it, along with the Newtonsoft DLL.</span></span> <span data-ttu-id="58697-249">Il existe actuellement un problème connu dans Unity qui nécessite que les plug-ins soient reconfigurés après l’importation.</span><span class="sxs-lookup"><span data-stu-id="58697-249">There is currently a known issue in Unity which requires plugins to be  reconfigured after import.</span></span> <span data-ttu-id="58697-250">Ces étapes (4-7 dans cette section) ne sont plus nécessaires une fois que le bogue a été résolu.</span><span class="sxs-lookup"><span data-stu-id="58697-250">These steps (4 - 7 in this section) will no longer be required after the bug has been resolved.</span></span>

<span data-ttu-id="58697-251">Pour importer Application Insights dans votre propre projet, assurez-vous d’avoir [téléchargé «. pour Unity», contenant les plug-ins](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20309%20-%20Application%20insights/AppInsights_LabPlugins.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="58697-251">To import Application Insights into your own project, make sure you have [downloaded the '.unitypackage', containing the plugins](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20309%20-%20Application%20insights/AppInsights_LabPlugins.unitypackage).</span></span> <span data-ttu-id="58697-252">Ensuite, procédez comme suit:</span><span class="sxs-lookup"><span data-stu-id="58697-252">Then, do the following:</span></span>

1.  <span data-ttu-id="58697-253">Ajoutez le fichier **. pour Unity** à Unity à l’aide de l’option de menu **package personnalisé du \> package \> d’importation de ressources** .</span><span class="sxs-lookup"><span data-stu-id="58697-253">Add the **.unitypackage** to Unity by using the **Assets \> Import Package \> Custom Package** menu option.</span></span>

2.  <span data-ttu-id="58697-254">Dans la zone **importer le package Unity** qui s’affiche, vérifiez que tous les plug- **ins** sous (et y compris) sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="58697-254">In the **Import Unity Package** box that pops up, ensure everything under (and including) **Plugins** is selected.</span></span>

    ![Importer le package Unity](images/AzureLabs-Lab309-22.png)

3.  <span data-ttu-id="58697-256">Cliquez sur le bouton **Importer** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="58697-256">Click the **Import** button, to add the items to your project.</span></span>

4.  <span data-ttu-id="58697-257">Accédez au dossier **Insights** sous **plug-ins** dans la vue projet et sélectionnez les plug-ins suivants *uniquement*:</span><span class="sxs-lookup"><span data-stu-id="58697-257">Go to the **Insights** folder under **Plugins** in the Project view and select the following plugins *only*:</span></span>

    -   <span data-ttu-id="58697-258">Microsoft. ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="58697-258">Microsoft.ApplicationInsights</span></span>

    ![Importer le package Unity](images/AzureLabs-Lab309-23.png)

5.  <span data-ttu-id="58697-260">Si ce *plug-in* est sélectionné, assurez -vous que **toutes les plateformes** sont décochées, vérifiez que **WSAPlayer** est également **désactivé**, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="58697-260">With this *plugin* selected, ensure that **Any Platform** is **unchecked**, then ensure that **WSAPlayer** is also **unchecked**, then click **Apply**.</span></span> <span data-ttu-id="58697-261">Cela suffit pour confirmer que les fichiers sont correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="58697-261">Doing this is just to confirm that the files are configured correctly.</span></span>

    ![Importer le package Unity](images/AzureLabs-Lab309-24.png)

    > [!NOTE]
    > <span data-ttu-id="58697-263">Le marquage des plug-ins comme celui-ci permet de les configurer pour qu’ils soient utilisés uniquement dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="58697-263">Marking the plugins like this, configures them to only be used in the Unity Editor.</span></span> <span data-ttu-id="58697-264">Il existe un ensemble différent de dll dans le dossier WSA qui sera utilisé une fois que le projet est exporté d’Unity.</span><span class="sxs-lookup"><span data-stu-id="58697-264">There are a different set of DLLs in the WSA folder which will be used after the project is exported from Unity.</span></span>

6.  <span data-ttu-id="58697-265">Ensuite, vous devez ouvrir le dossier **WSA** , dans le dossier **Insights** .</span><span class="sxs-lookup"><span data-stu-id="58697-265">Next, you need to open the **WSA** folder, within the **Insights** folder.</span></span> <span data-ttu-id="58697-266">Vous verrez une copie du même fichier que celui que vous venez de configurer.</span><span class="sxs-lookup"><span data-stu-id="58697-266">You will see a copy of the same file you just configured.</span></span> <span data-ttu-id="58697-267">Sélectionnez ce fichier, puis, dans l’inspecteur, assurez-vous que  **toutes les plateformes** sont décochées, puis vérifiez que **seul** **WSAPlayer** est **activé**.</span><span class="sxs-lookup"><span data-stu-id="58697-267">Select this file, and then in the inspector, ensure that **Any Platform** is **unchecked**, then ensure that **only** **WSAPlayer** is **checked**.</span></span> <span data-ttu-id="58697-268">Cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="58697-268">Click **Apply**.</span></span>

    ![Importer le package Unity](images/AzureLabs-Lab309-25.png)

7. <span data-ttu-id="58697-270">Vous devez maintenant suivre les **étapes 4-6**, mais pour les plug-ins *Newtonsoft* à la place.</span><span class="sxs-lookup"><span data-stu-id="58697-270">You will now need to follow **steps 4-6**, but for the *Newtonsoft* plugins instead.</span></span> <span data-ttu-id="58697-271">Consultez la capture d’écran ci-dessous pour savoir à quoi doit ressembler le résultat.</span><span class="sxs-lookup"><span data-stu-id="58697-271">See the below screenshot for what the outcome should look like.</span></span>

    ![Importer le package Unity](images/AzureLabs-Lab309-25-5.png)    

## <a name="chapter-4---set-up-the-camera-and-user-controls"></a><span data-ttu-id="58697-273">Chapitre 4-configurer l’appareil photo et les contrôles utilisateur</span><span class="sxs-lookup"><span data-stu-id="58697-273">Chapter 4 - Set up the camera and user controls</span></span>

<span data-ttu-id="58697-274">Dans ce chapitre, vous allez configurer l’appareil photo et les contrôles pour permettre à l’utilisateur de voir et de se déplacer dans la scène.</span><span class="sxs-lookup"><span data-stu-id="58697-274">In this Chapter you will set up the camera and the controls to allow the user to see and move in the scene.</span></span>

1.  <span data-ttu-id="58697-275">Cliquez avec le bouton droit dans une zone vide du panneau hiérarchie, puis sur **créer** > **vide**.</span><span class="sxs-lookup"><span data-stu-id="58697-275">Right-click in an empty area in the Hierarchy Panel, then on **Create** > **Empty**.</span></span>

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-26.png)

2.  <span data-ttu-id="58697-277">Renommez le nouveau GameObject vide en **parent Camera**.</span><span class="sxs-lookup"><span data-stu-id="58697-277">Rename the new empty GameObject to **Camera Parent**.</span></span>

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-27.png)

3.  <span data-ttu-id="58697-279">Cliquez avec le bouton droit dans une zone vide du panneau hiérarchie, puis sur **objet 3D**, puis sur **sphère**.</span><span class="sxs-lookup"><span data-stu-id="58697-279">Right-click in an empty area in the Hierarchy Panel, then on **3D Object**, then on **Sphere**.</span></span>

4.  <span data-ttu-id="58697-280">Renommez la sphère **avec la main droite**.</span><span class="sxs-lookup"><span data-stu-id="58697-280">Rename the Sphere to **Right Hand**.</span></span>

5.  <span data-ttu-id="58697-281">Définissez l' **échelle de transformation** de la main droite sur **0,1, 0,1, 0,1**</span><span class="sxs-lookup"><span data-stu-id="58697-281">Set the **Transform Scale** of the Right Hand to **0.1, 0.1, 0.1**</span></span>

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-28.png)

6.  <span data-ttu-id="58697-283">Retirez le composant **Sphere collision** de la main droite en cliquant sur l' **engrenage** dans le composant *Sphere collision* , puis en supprimant le **composant**.</span><span class="sxs-lookup"><span data-stu-id="58697-283">Remove the **Sphere Collider** component from the Right Hand by clicking on the **Gear** in the *Sphere Collider* component, and then **Remove Component**.</span></span>

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-29.png)

7.  <span data-ttu-id="58697-285">Dans le panneau hiérarchie, faites glisser les objets main **Camera** et **Right main** sur l’objet **parent Camera** .</span><span class="sxs-lookup"><span data-stu-id="58697-285">In the Hierarchy Panel drag the **Main Camera** and the **Right Hand** objects onto the **Camera Parent** object.</span></span>

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-30.png)

8.  <span data-ttu-id="58697-287">Définissez la **position** de la transformation de la **caméra principale** et de l’objet de **droite** sur **0, 0,** 0.</span><span class="sxs-lookup"><span data-stu-id="58697-287">Set the **Transform Position** of both the **Main Camera** and the **Right Hand** object to **0, 0, 0**.</span></span>

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-31.png)

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-32.png)

## <a name="chapter-5---set-up-the-objects-in-the-unity-scene"></a><span data-ttu-id="58697-290">Chapitre 5-configurer les objets dans la scène Unity</span><span class="sxs-lookup"><span data-stu-id="58697-290">Chapter 5 - Set up the objects in the Unity scene</span></span>

<span data-ttu-id="58697-291">Vous allez maintenant créer des formes de base pour votre scène, avec lesquelles l’utilisateur peut interagir.</span><span class="sxs-lookup"><span data-stu-id="58697-291">You will now create some basic shapes for your scene, with which the user can interact.</span></span>

1.  <span data-ttu-id="58697-292">Cliquez avec le bouton droit dans une zone vide du *panneau hiérarchie*, puis sur **objet 3D**et sélectionnez **plan**.</span><span class="sxs-lookup"><span data-stu-id="58697-292">Right-click in an empty area in the *Hierarchy Panel*, then on **3D Object**, then select **Plane**.</span></span>

2.  <span data-ttu-id="58697-293">Définissez la position de la **transformation** du plan sur **0,-1, 0**.</span><span class="sxs-lookup"><span data-stu-id="58697-293">Set the Plane **Transform Position** to **0, -1, 0**.</span></span>

3.  <span data-ttu-id="58697-294">Affectez à l' **échelle de transformation** du plan la valeur **5, 1, 5**.</span><span class="sxs-lookup"><span data-stu-id="58697-294">Set the Plane **Transform Scale** to **5, 1, 5**.</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-33.png)

4.  <span data-ttu-id="58697-296">Créez un matériau de base à utiliser avec votre objet **plan** , afin que les autres formes soient plus faciles à voir.</span><span class="sxs-lookup"><span data-stu-id="58697-296">Create a basic material to use with your **Plane** object, so that the other shapes are easier to see.</span></span> <span data-ttu-id="58697-297">Accédez au *panneau Projet*, cliquez avec le bouton droit, puis **créez**, suivi de **dossier**, pour créer un nouveau dossier.</span><span class="sxs-lookup"><span data-stu-id="58697-297">Navigate to your *Project Panel*, right-click, then **Create**, followed by **Folder**, to create a new folder.</span></span> <span data-ttu-id="58697-298">Nommez-la **matériel**.</span><span class="sxs-lookup"><span data-stu-id="58697-298">Name it **Materials**.</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-34.png) ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-35.png)

5.  <span data-ttu-id="58697-301">Ouvrez le dossier **matériaux** , cliquez avec le bouton droit sur, cliquez sur **créer**, puis sur **matériau**, pour créer un nouveau matériau.</span><span class="sxs-lookup"><span data-stu-id="58697-301">Open the **Materials** folder, then right-click, click **Create**, then **Material**, to create a new material.</span></span> <span data-ttu-id="58697-302">Nommez-le **Blue**.</span><span class="sxs-lookup"><span data-stu-id="58697-302">Name it **Blue**.</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-36.png) ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-37.png)

6.  <span data-ttu-id="58697-305">Une fois le nouveau matériau **bleu** sélectionné, examinez l' *inspecteur*, puis cliquez sur la fenêtre rectangulaire à côté de **Albedo**.</span><span class="sxs-lookup"><span data-stu-id="58697-305">With the new **Blue** material selected, look at the *Inspector*, and click the rectangular window alongside **Albedo**.</span></span> <span data-ttu-id="58697-306">Sélectionnez une couleur bleue (l’image ci-dessous **est une couleur hexadécimale: \#3592FFFF**).</span><span class="sxs-lookup"><span data-stu-id="58697-306">Select a blue color (the one picture below is **Hex Color: \#3592FFFF**).</span></span> <span data-ttu-id="58697-307">Cliquez sur le bouton Fermer une fois que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="58697-307">Click the close button once you have chosen.</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-38.png)

7.  <span data-ttu-id="58697-309">Faites glisser votre nouveau matériel à partir du dossier **matériaux** , sur le **plan**que vous venez de créer, dans votre scène (ou déposez-le sur l’objet **plan** dans la *hiérarchie*).</span><span class="sxs-lookup"><span data-stu-id="58697-309">Drag your new material from the **Materials** folder, onto your newly created **Plane**, within your scene (or drop it on the **Plane** object within the *Hierarchy*).</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-39.png)

8.  <span data-ttu-id="58697-311">Cliquez avec le bouton droit dans une zone vide du *panneau hiérarchie*, puis sur **objet 3D, capsule**.</span><span class="sxs-lookup"><span data-stu-id="58697-311">Right-click in an empty area in the *Hierarchy Panel*, then on **3D Object, Capsule**.</span></span>

    -  <span data-ttu-id="58697-312">Une fois la **capsule** sélectionnée, remplacez sa *position* de **transformation** par: **-10, 1,0**.</span><span class="sxs-lookup"><span data-stu-id="58697-312">With the **Capsule** selected, change its **Transform** *Position* to: **-10, 1, 0**.</span></span>

9.  <span data-ttu-id="58697-313">Cliquez avec le bouton droit dans une zone vide du *panneau hiérarchie*, puis sur **objet 3D, cube**.</span><span class="sxs-lookup"><span data-stu-id="58697-313">Right-click in an empty area in the *Hierarchy Panel*, then on **3D Object, Cube**.</span></span>

    -  <span data-ttu-id="58697-314">Une fois le **cube** sélectionné, remplacez sa *position* de **transformation** par: **0, 0, 10**.</span><span class="sxs-lookup"><span data-stu-id="58697-314">With the **Cube** selected, change its **Transform** *Position* to: **0, 0, 10**.</span></span>

10. <span data-ttu-id="58697-315">Cliquez avec le bouton droit dans une zone vide du *panneau hiérarchie*, puis sur **objet 3D, sphère**.</span><span class="sxs-lookup"><span data-stu-id="58697-315">Right-click in an empty area in the *Hierarchy Panel*, then on **3D Object, Sphere**.</span></span>

    -  <span data-ttu-id="58697-316">Une fois la **sphère** sélectionnée, modifiez sa *position* de **transformation** en: **10, 0, 0**.</span><span class="sxs-lookup"><span data-stu-id="58697-316">With the **Sphere** selected, change its **Transform** *Position* to: **10, 0, 0**.</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-40.png)

    > [!NOTE]
    > <span data-ttu-id="58697-318">Ces valeurs de *position* sont des *suggestions*.</span><span class="sxs-lookup"><span data-stu-id="58697-318">These *Position* values are *suggestions*.</span></span> <span data-ttu-id="58697-319">Vous êtes libre de définir la position des objets sur ce que vous souhaitez, bien qu’il soit plus facile pour l’utilisateur de l’application si les distances des objets ne sont pas trop éloignées de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="58697-319">You are free to set the positions of the objects to whatever you would like, though it is easier for the user of the application if the objects distances are not too far from the camera.</span></span>

11. <span data-ttu-id="58697-320">Lorsque votre application est en cours d’exécution, elle doit être en mesure d’identifier les objets dans la scène. pour ce faire, elle doit être marquée.</span><span class="sxs-lookup"><span data-stu-id="58697-320">When your application is running, it needs to be able to identify the objects within the scene, to achieve this, they need to be tagged.</span></span> <span data-ttu-id="58697-321">Sélectionnez l’un des objets, puis dans le panneau *inspecteur* , cliquez sur **Ajouter une étiquette...** , qui permutera l' *inspecteur* avec les balises **& panneau couches** .</span><span class="sxs-lookup"><span data-stu-id="58697-321">Select one of the objects, and in the *Inspector* panel, click **Add Tag...**, which will swap the *Inspector* with the **Tags & Layers** panel.</span></span>

    <span data-ttu-id="58697-322">![Configurer les objets dans la scène](images/AzureLabs-Lab309-41.png) Unity![](images/AzureLabs-Lab309-42.png)</span><span class="sxs-lookup"><span data-stu-id="58697-322">![Set up the objects in the Unity Scene](images/AzureLabs-Lab309-41.png) ![](images/AzureLabs-Lab309-42.png)</span></span>

12. <span data-ttu-id="58697-323">Cliquez sur le signe **+ (plus)** , puis tapez le nom de la balise en tant que **ObjectInScene**.</span><span class="sxs-lookup"><span data-stu-id="58697-323">Click the **+ (plus)** symbol, then type the tag name as **ObjectInScene**.</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-43.png)

    > [!WARNING]
    > <span data-ttu-id="58697-325">Si vous utilisez un nom différent pour votre balise, vous devez vous assurer que cette modification est également apportée aux scripts *DataFromAnalytics*, *ObjectTrigger* *et*pointage par la suite, afin que vos objets soient détectés et détectés dans votre scène.</span><span class="sxs-lookup"><span data-stu-id="58697-325">If you use a different name for your tag, you will need to ensure this change is also made the *DataFromAnalytics*, *ObjectTrigger*, and *Gaze*, scripts later, so that your objects are found, and detected, within your scene.</span></span>

13. <span data-ttu-id="58697-326">Une fois la balise créée, vous devez l’appliquer à tous les trois objets.</span><span class="sxs-lookup"><span data-stu-id="58697-326">With the tag created, you now need to apply it to all three of your objects.</span></span> <span data-ttu-id="58697-327">Dans la *hiérarchie*, maintenez la **touche Maj** enfoncée, cliquez sur les objets **capsule**, **cube**et **sphère**, puis dans l' *inspecteur*, cliquez sur le menu déroulant avec la **balise**, puis cliquez sur le *ObjectInScene* balise que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="58697-327">From the *Hierarchy*, hold the **Shift** key, then click the **Capsule**, **Cube**, and **Sphere**, objects, then in the *Inspector*, click the dropdown menu alongside **Tag**, then click the *ObjectInScene* tag you created.</span></span>

    <span data-ttu-id="58697-328">![Configurer les objets dans la scène](images/AzureLabs-Lab309-44.png) Unity![](images/AzureLabs-Lab309-45.png)</span><span class="sxs-lookup"><span data-stu-id="58697-328">![Set up the objects in the Unity Scene](images/AzureLabs-Lab309-44.png) ![](images/AzureLabs-Lab309-45.png)</span></span>

## <a name="chapter-6---create-the-applicationinsightstracker-class"></a><span data-ttu-id="58697-329">Chapitre 6-créer la classe ApplicationInsightsTracker</span><span class="sxs-lookup"><span data-stu-id="58697-329">Chapter 6 - Create the ApplicationInsightsTracker class</span></span>

<span data-ttu-id="58697-330">Le premier script que vous devez créer est **ApplicationInsightsTracker**, qui est responsable des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="58697-330">The first script you need to create is **ApplicationInsightsTracker**, which is responsible for:</span></span>

1.  <span data-ttu-id="58697-331">Création d’événements basés sur les interactions de l’utilisateur à envoyer à Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="58697-331">Creating events based on user interactions to submit to Azure Application Insights.</span></span>

2. <span data-ttu-id="58697-332">Création des noms d’événements appropriés, en fonction de l’interaction de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="58697-332">Creating appropriate Event names, depending on user interaction.</span></span>

3. <span data-ttu-id="58697-333">Envoi d’événements à l’instance de service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="58697-333">Submitting events to the Application Insights Service instance.</span></span>

<span data-ttu-id="58697-334">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="58697-334">To create this class:</span></span>

1.  <span data-ttu-id="58697-335">Cliquez avec le bouton droit dans le *panneau Projet*, puis **créez** > le**dossier**.</span><span class="sxs-lookup"><span data-stu-id="58697-335">Right-click in the *Project Panel*, then **Create** > **Folder**.</span></span> <span data-ttu-id="58697-336">Nommez le dossier **scripts**.</span><span class="sxs-lookup"><span data-stu-id="58697-336">Name the folder **Scripts**.</span></span>

    ![Créer la classe ApplicationInsightsTracker](images/AzureLabs-Lab309-46.png)  ![Créer la classe ApplicationInsightsTracker](images/AzureLabs-Lab309-47.png)

2.  <span data-ttu-id="58697-339">Une fois le dossier **scripts** créé, double-cliquez dessus pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="58697-339">With the **Scripts** folder created, double-click it, to open.</span></span> <span data-ttu-id="58697-340">Ensuite, dans ce dossier, cliquez avec le bouton droit sur **créer**  >   **C# un script**.</span><span class="sxs-lookup"><span data-stu-id="58697-340">Then, within that folder, right-click, **Create** > **C# Script**.</span></span> <span data-ttu-id="58697-341">Nommez le script **ApplicationInsightsTracker**.</span><span class="sxs-lookup"><span data-stu-id="58697-341">Name the script **ApplicationInsightsTracker**.</span></span>

3.  <span data-ttu-id="58697-342">Double-cliquez sur le nouveau script **ApplicationInsightsTracker** pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="58697-342">Double-click on the new **ApplicationInsightsTracker** script to open it with **Visual Studio**.</span></span>

4.  <span data-ttu-id="58697-343">Mettez à jour les espaces de noms en haut du script pour qu’ils soient comme indiqué ci-dessous:</span><span class="sxs-lookup"><span data-stu-id="58697-343">Update namespaces at the top of the script to be as below:</span></span>

    ```csharp
        using Microsoft.ApplicationInsights;
        using Microsoft.ApplicationInsights.DataContracts;
        using Microsoft.ApplicationInsights.Extensibility;
        using UnityEngine;
    ```

5.  <span data-ttu-id="58697-344">À l’intérieur de la classe, insérez les variables suivantes:</span><span class="sxs-lookup"><span data-stu-id="58697-344">Inside the class insert the following variables:</span></span>

    ```csharp
        /// <summary>
        /// Allows this class to behavior like a singleton
        /// </summary>
        public static ApplicationInsightsTracker Instance;
        
        /// <summary>
        /// Insert your Instrumentation Key here
        /// </summary>
        internal string instrumentationKey = "Insert Instrumentation Key here";

        /// <summary>
        /// Insert your Application Id here
        /// </summary>
        internal string applicationId = "Insert Application Id here";

        /// <summary>
        /// Insert your API Key here
        /// </summary>
        internal string API_Key = "Insert API Key here";

        /// <summary>
        /// Represent the Analytic Custom Event object
        /// </summary>
        private TelemetryClient telemetryClient;

        /// <summary>
        /// Represent the Analytic object able to host gaze duration
        /// </summary>
        private MetricTelemetry metric;
    ```

    > [!NOTE] 
    > <span data-ttu-id="58697-345">Définissez les valeurs **instrumentationKey, ApplicationId et API_Key** de manière appropriée, à l’aide des *clés de service* à partir du portail Azure, comme indiqué au [Chapitre 1](#chapter-1---the-azure-portal), étape 9.</span><span class="sxs-lookup"><span data-stu-id="58697-345">Set the **instrumentationKey, applicationId and API_Key** values appropriately, using the *Service Keys* from the Azure Portal as mentioned in [Chapter 1](#chapter-1---the-azure-portal), step 9 onwards.</span></span>

6.  <span data-ttu-id="58697-346">Ajoutez ensuite les méthodes **Start ()** et **éveillé ()** , qui seront appelées lorsque la classe est initialisée:</span><span class="sxs-lookup"><span data-stu-id="58697-346">Then add the **Start()** and **Awake()** methods, which will be called when the class initializes:</span></span>

    ```csharp
        /// <summary>
        /// Sets this class instance as a singleton
        /// </summary>
        void Awake()
        {
            Instance = this;
        }

        /// <summary>
        /// Use this for initialization
        /// </summary>
        void Start()
        {
            // Instantiate telemetry and metric
            telemetryClient = new TelemetryClient();

            metric = new MetricTelemetry();

            // Assign the Instrumentation Key to the Event and Metric objects
            TelemetryConfiguration.Active.InstrumentationKey = instrumentationKey;

            telemetryClient.InstrumentationKey = instrumentationKey;
        }
    ```

7.  <span data-ttu-id="58697-347">Ajoutez les méthodes responsables de l’envoi des événements et des métriques inscrits par votre application:</span><span class="sxs-lookup"><span data-stu-id="58697-347">Add the methods responsible for sending the events and metrics registered by your application:</span></span>

    ```csharp
        /// <summary>
        /// Submit the Event to Azure Analytics using the event trigger object
        /// </summary>
        public void RecordProximityEvent(string objectName)
        {
            telemetryClient.TrackEvent(CreateEventName(objectName));
        }

        /// <summary>
        /// Uses the name of the object involved in the event to create 
        /// and return an Event Name convention
        /// </summary>
        public string CreateEventName(string name)
        {
            string eventName = $"User near {name}";
            return eventName;
        }

        /// <summary>
        /// Submit a Metric to Azure Analytics using the metric gazed object
        /// and the time count of the gaze
        /// </summary>
        public void RecordGazeMetrics(string objectName, int time)
        {
            // Output Console information about gaze.
            Debug.Log($"Finished gazing at {objectName}, which went for <b>{time}</b> second{(time != 1 ? "s" : "")}");

            metric.Name = $"Gazed {objectName}";

            metric.Value = time;

            telemetryClient.TrackMetric(metric);
        }
    ```

8.  <span data-ttu-id="58697-348">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="58697-348">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-7---create-the-gaze-script"></a><span data-ttu-id="58697-349">Chapitre 7-créer le script de regard</span><span class="sxs-lookup"><span data-stu-id="58697-349">Chapter 7 - Create the Gaze script</span></span>

<span data-ttu-id="58697-350">Le script suivant à créer **est le script** de regard.</span><span class="sxs-lookup"><span data-stu-id="58697-350">The next script to create is the **Gaze** script.</span></span> <span data-ttu-id="58697-351">Ce script est chargé de créer un *Raycast* qui sera projeté à partir de l' *appareil photo principal*, afin de détecter l’objet que l’utilisateur examine.</span><span class="sxs-lookup"><span data-stu-id="58697-351">This script is responsible for creating a *Raycast* that will be projected forward from the *Main Camera*, to detect which object the user is looking at.</span></span> <span data-ttu-id="58697-352">Dans ce cas, le *Raycast* doit déterminer si l’utilisateur Regarde un objet avec la balise **ObjectInScene** , puis compter la durée pendant laquelle l’utilisateur fait un *regard* sur cet objet.</span><span class="sxs-lookup"><span data-stu-id="58697-352">In this case, the *Raycast* will need to identify if the user is looking at an object with the **ObjectInScene** tag, and then count how long the user *gazes* at that object.</span></span>

1.  <span data-ttu-id="58697-353">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="58697-353">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="58697-354">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer**  >   **C# un script**.</span><span class="sxs-lookup"><span data-stu-id="58697-354">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="58697-355">Nommez le script point de **regard**.</span><span class="sxs-lookup"><span data-stu-id="58697-355">Name the script **Gaze**.</span></span>

3.  <span data-ttu-id="58697-356">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58697-356">Double-click on the script to open it with Visual Studio.</span></span>

4.  <span data-ttu-id="58697-357">Remplacez le code existant par le code ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="58697-357">Replace the existing code with the following:</span></span>

    ```csharp
        using UnityEngine;

        public class Gaze : MonoBehaviour
        {
            /// <summary>
            /// Provides Singleton-like behavior to this class.
            /// </summary>
            public static Gaze Instance;

            /// <summary>
            /// Provides a reference to the object the user is currently looking at.
            /// </summary>
            public GameObject FocusedGameObject { get; private set; }

            /// <summary>
            /// Provides whether an object has been successfully hit by the raycast.
            /// </summary>
            public bool Hit { get; private set; }

            /// <summary>
            /// Provides a reference to compare whether the user is still looking at 
            /// the same object (and has not looked away).
            /// </summary>
            private GameObject _oldFocusedObject = null;

            /// <summary>
            /// Max Ray Distance
            /// </summary>
            private float _gazeMaxDistance = 300;

            /// <summary>
            /// Max Ray Distance
            /// </summary>
            private float _gazeTimeCounter = 0;

            /// <summary>
            /// The cursor object will be created when the app is running,
            /// this will store its values. 
            /// </summary>
            private GameObject _cursor;
        }
    ```

5.  <span data-ttu-id="58697-358">Vous devez maintenant ajouter du code pour les méthodes **éveillé ()** et **Start ()** .</span><span class="sxs-lookup"><span data-stu-id="58697-358">Code for the **Awake()** and **Start()** methods now needs to be added.</span></span>

    ```csharp
        private void Awake()
        {
            // Set this class to behave similar to singleton
            Instance = this;
            _cursor = CreateCursor();
        }

        void Start()
        {
            FocusedGameObject = null;
        }

        /// <summary>
        /// Create a cursor object, to provide what the user
        /// is looking at.
        /// </summary>
        /// <returns></returns>
        private GameObject CreateCursor()    
        {
            GameObject newCursor = GameObject.CreatePrimitive(PrimitiveType.Sphere);

            // Remove the collider, so it does not block raycast.
            Destroy(newCursor.GetComponent<SphereCollider>());

            newCursor.transform.localScale = new Vector3(0.1f, 0.1f, 0.1f);

            newCursor.GetComponent<MeshRenderer>().material.color = 
            Color.HSVToRGB(0.0223f, 0.7922f, 1.000f);

            newCursor.SetActive(false);
            return newCursor;
        }
    ```

6.  <span data-ttu-id="58697-359">À l’intérieur de la classe de **regard** , ajoutez le code suivant dans la méthode **Update ()** pour projeter un *Raycast* et détecter l’accès cible:</span><span class="sxs-lookup"><span data-stu-id="58697-359">Inside the **Gaze** class, add the following code in the **Update()** method to project a *Raycast* and detect the target hit:</span></span>

    ```csharp
        /// <summary>
        /// Called every frame
        /// </summary>
        void Update()
        {
            // Set the old focused gameobject.
            _oldFocusedObject = FocusedGameObject;

            RaycastHit hitInfo;

            // Initialize Raycasting.
            Hit = Physics.Raycast(Camera.main.transform.position, Camera.main.transform.forward, out hitInfo, _gazeMaxDistance);

            // Check whether raycast has hit.
            if (Hit == true)
            {
                // Check whether the hit has a collider.
                if (hitInfo.collider != null)
                {
                    // Set the focused object with what the user just looked at.
                    FocusedGameObject = hitInfo.collider.gameObject;

                    // Lerp the cursor to the hit point, which helps to stabilize the gaze.
                    _cursor.transform.position = Vector3.Lerp(_cursor.transform.position, hitInfo.point, 0.6f);

                    _cursor.SetActive(true);
                }
                else
                {
                    // Object looked on is not valid, set focused gameobject to null.
                    FocusedGameObject = null;

                    _cursor.SetActive(false);
                }
            }
            else
            {
                // No object looked upon, set focused gameobject to null.
                FocusedGameObject = null;

                _cursor.SetActive(false);
            }

            // Check whether the previous focused object is this same object. If so, reset the focused object.
            if (FocusedGameObject != _oldFocusedObject)
            {
                ResetFocusedObject();
            }
            // If they are the same, but are null, reset the counter. 
            else if (FocusedGameObject == null && _oldFocusedObject == null)
            {
                _gazeTimeCounter = 0;
            }
            // Count whilst the user continues looking at the same object.
            else
            {
                _gazeTimeCounter += Time.deltaTime;
            }
        }
    ```

7.  <span data-ttu-id="58697-360">Ajoutez la méthode **ResetFocusedObject ()** pour envoyer des données à **application Insights** lorsque l’utilisateur a regardé un objet.</span><span class="sxs-lookup"><span data-stu-id="58697-360">Add the **ResetFocusedObject()** method, to send data to **Application Insights** when the user has looked at an object.</span></span>

    ```csharp
        /// <summary>
        /// Reset the old focused object, stop the gaze timer, and send data if it
        /// is greater than one.
        /// </summary>
        public void ResetFocusedObject()
        {
            // Ensure the old focused object is not null.
            if (_oldFocusedObject != null)
            {
                // Only looking for objects with the correct tag.
                if (_oldFocusedObject.CompareTag("ObjectInScene"))
                {
                    // Turn the timer into an int, and ensure that more than zero time has passed.
                    int gazeAsInt = (int)_gazeTimeCounter;

                    if (gazeAsInt > 0)
                    {
                        //Record the object gazed and duration of gaze for Analytics
                        ApplicationInsightsTracker.Instance.RecordGazeMetrics(_oldFocusedObject.name, gazeAsInt);
                    }
                    //Reset timer
                    _gazeTimeCounter = 0;
                }
            }
        }
    ```

8.  <span data-ttu-id="58697-361">Vous avez maintenant terminé le script de **regard** .</span><span class="sxs-lookup"><span data-stu-id="58697-361">You have now completed the **Gaze** script.</span></span> <span data-ttu-id="58697-362">Enregistrez vos modifications dans *Visual Studio* avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="58697-362">Save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-8---create-the-objecttrigger-class"></a><span data-ttu-id="58697-363">Chapitre 8-créer la classe ObjectTrigger</span><span class="sxs-lookup"><span data-stu-id="58697-363">Chapter 8 - Create the ObjectTrigger class</span></span>

<span data-ttu-id="58697-364">Le prochain script que vous devez créer est **ObjectTrigger**, qui est responsable des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="58697-364">The next script you need to create is **ObjectTrigger**, which is responsible for:</span></span>

- <span data-ttu-id="58697-365">Ajout de composants nécessaires pour la collision à l’appareil photo principal.</span><span class="sxs-lookup"><span data-stu-id="58697-365">Adding components needed for collision to the Main Camera.</span></span>
- <span data-ttu-id="58697-366">Détection de si l’appareil photo est proche d’un objet marqué comme **ObjectInScene**.</span><span class="sxs-lookup"><span data-stu-id="58697-366">Detecting if the camera is near an object tagged as **ObjectInScene**.</span></span>

<span data-ttu-id="58697-367">Pour créer le script:</span><span class="sxs-lookup"><span data-stu-id="58697-367">To create the script:</span></span>

1.  <span data-ttu-id="58697-368">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="58697-368">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="58697-369">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer**  >   **C# un script**.</span><span class="sxs-lookup"><span data-stu-id="58697-369">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="58697-370">Nommez le script **ObjectTrigger**.</span><span class="sxs-lookup"><span data-stu-id="58697-370">Name the script **ObjectTrigger**.</span></span>

3.  <span data-ttu-id="58697-371">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58697-371">Double-click on the script to open it with Visual Studio.</span></span> <span data-ttu-id="58697-372">Remplacez le code existant par le code ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="58697-372">Replace the existing code with the following:</span></span>

    ```csharp
        using UnityEngine;

        public class ObjectTrigger : MonoBehaviour
        {
            private void Start()
            {
                // Add the Collider and Rigidbody components, 
                // and set their respective settings. This allows for collision.
                gameObject.AddComponent<SphereCollider>().radius = 1.5f;

                gameObject.AddComponent<Rigidbody>().useGravity = false;
            }

            /// <summary>
            /// Triggered when an object with a collider enters this objects trigger collider.
            /// </summary>
            /// <param name="collision">Collided object</param>
            private void OnCollisionEnter(Collision collision)
            {
                CompareTriggerEvent(collision, true);
            }

            /// <summary>
            /// Triggered when an object with a collider exits this objects trigger collider.
            /// </summary>
            /// <param name="collision">Collided object</param>
            private void OnCollisionExit(Collision collision)
            {
                CompareTriggerEvent(collision, false);
            }

            /// <summary>
            /// Method for providing debug message, and sending event information to InsightsTracker.
            /// </summary>
            /// <param name="other">Collided object</param>
            /// <param name="enter">Enter = true, Exit = False</param>
            private void CompareTriggerEvent(Collision other, bool enter)
            {
                if (other.collider.CompareTag("ObjectInScene"))
                {
                    string message = $"User is{(enter == true ? " " : " no longer ")}near <b>{other.gameObject.name}</b>";

                    if (enter == true)
                    {
                        ApplicationInsightsTracker.Instance.RecordProximityEvent(other.gameObject.name);
                    }
                    Debug.Log(message);
                }
            }
        }
    ```

4.  <span data-ttu-id="58697-373">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="58697-373">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-9---create-the-datafromanalytics-class"></a><span data-ttu-id="58697-374">Chapitre 9-créer la classe DataFromAnalytics</span><span class="sxs-lookup"><span data-stu-id="58697-374">Chapter 9 - Create the DataFromAnalytics class</span></span>

<span data-ttu-id="58697-375">Vous devez maintenant créer le script **DataFromAnalytics** , qui est responsable des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="58697-375">You will now need to create the **DataFromAnalytics** script, which is responsible for:</span></span>

- <span data-ttu-id="58697-376">Récupération des données d’analyse sur l’objet le plus proche de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="58697-376">Fetching analytics data about which object has been approached by the camera the most.</span></span>
- <span data-ttu-id="58697-377">À l’aide des *clés de service*, qui autorisent la communication avec votre instance de service Azure application Insights.</span><span class="sxs-lookup"><span data-stu-id="58697-377">Using the *Service Keys*, that allow communication with your Azure Application Insights Service instance.</span></span>
- <span data-ttu-id="58697-378">Tri des objets dans la scène, en fonction du nombre d’événements le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="58697-378">Sorting the objects in scene, according to which has the highest event count.</span></span>
- <span data-ttu-id="58697-379">La modification de la couleur matérielle, de l’objet le plus proche, en *vert*.</span><span class="sxs-lookup"><span data-stu-id="58697-379">Changing the material color, of the most approached object, to *green*.</span></span>

<span data-ttu-id="58697-380">Pour créer le script:</span><span class="sxs-lookup"><span data-stu-id="58697-380">To create the script:</span></span>

1.  <span data-ttu-id="58697-381">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="58697-381">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="58697-382">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer**  >   **C# un script**.</span><span class="sxs-lookup"><span data-stu-id="58697-382">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="58697-383">Nommez le script **DataFromAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="58697-383">Name the script **DataFromAnalytics**.</span></span>

3.  <span data-ttu-id="58697-384">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58697-384">Double-click on the script to open it with Visual Studio.</span></span>

4.  <span data-ttu-id="58697-385">Insérez les espaces de noms suivants:</span><span class="sxs-lookup"><span data-stu-id="58697-385">Insert the following namespaces:</span></span>

    ```csharp
        using Newtonsoft.Json;
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using System.Linq;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

5.  <span data-ttu-id="58697-386">Dans le script, insérez ce qui suit:</span><span class="sxs-lookup"><span data-stu-id="58697-386">Inside the script, insert the following:</span></span>

    ```csharp
        /// <summary>
        /// Number of most recent events to be queried
        /// </summary>
        private int _quantityOfEventsQueried = 10;

        /// <summary>
        /// The timespan with which to query. Needs to be in hours.
        /// </summary>
        private int _timepspanAsHours = 24;

        /// <summary>
        /// A list of the objects in the scene
        /// </summary>
        private List<GameObject> _listOfGameObjectsInScene;

        /// <summary>
        /// Number of queries which have returned, after being sent.
        /// </summary>
        private int _queriesReturned = 0;

        /// <summary>
        /// List of GameObjects, as the Key, with their event count, as the Value.
        /// </summary>
        private List<KeyValuePair<GameObject, int>> _pairedObjectsWithEventCount = new List<KeyValuePair<GameObject, int>>();

        // Use this for initialization
        void Start()
        {
            // Find all objects in scene which have the ObjectInScene tag (as there may be other GameObjects in the scene which you do not want).
            _listOfGameObjectsInScene = GameObject.FindGameObjectsWithTag("ObjectInScene").ToList();

            FetchAnalytics();
        }
    ```

6.  <span data-ttu-id="58697-387">Dans la classe **DataFromAnalytics** , juste après la méthode **Start ()** , ajoutez la méthode suivante appelée **FetchAnalytics ()** .</span><span class="sxs-lookup"><span data-stu-id="58697-387">Within the **DataFromAnalytics** class, right after the **Start()** method, add the following method called **FetchAnalytics()**.</span></span> <span data-ttu-id="58697-388">Cette méthode est chargée de remplir la liste des paires clé-valeur, avec un *gameobject* et un numéro d’événement d’espace réservé.</span><span class="sxs-lookup"><span data-stu-id="58697-388">This method is responsible for populating the list of key value pairs, with a *GameObject* and a placeholder event count number.</span></span> <span data-ttu-id="58697-389">Il initialise ensuite la Coroutine **GetWebRequest ()** .</span><span class="sxs-lookup"><span data-stu-id="58697-389">It then initializes the **GetWebRequest()** coroutine.</span></span> <span data-ttu-id="58697-390">La structure de requête de l’appel à *application Insights* se trouve également dans cette méthode, comme point de terminaison de l’URL de la *requête* .</span><span class="sxs-lookup"><span data-stu-id="58697-390">The query structure of the call to *Application Insights* can be found within this method also, as the *Query URL* endpoint.</span></span>

    ```csharp
        private void FetchAnalytics()
        {
            // Iterate through the objects in the list
            for (int i = 0; i < _listOfGameObjectsInScene.Count; i++)
            {
                // The current event number is not known, so set it to zero.
                int eventCount = 0;

                // Add new pair to list, as placeholder, until eventCount is known.
                _pairedObjectsWithEventCount.Add(new KeyValuePair<GameObject, int>(_listOfGameObjectsInScene[i], eventCount));

                // Set the renderer of the object to the default color, white
                _listOfGameObjectsInScene[i].GetComponent<Renderer>().material.color = Color.white;

                // Create the appropriate object name using Insights structure
                string objectName = _listOfGameObjectsInScene[i].name;
 
                // Build the queryUrl for this object.
                string queryUrl = Uri.EscapeUriString(string.Format(
                    "https://api.applicationinsights.io/v1/apps/{0}/events/$all?timespan=PT{1}H&$search={2}&$select=customMetric/name&$top={3}&$count=true",
                    ApplicationInsightsTracker.Instance.applicationId, _timepspanAsHours, "Gazed " + objectName, _quantityOfEventsQueried));


                // Send this object away within the WebRequest Coroutine, to determine it is event count.
                StartCoroutine("GetWebRequest", new KeyValuePair<string, int>(queryUrl, i));
            }
        }
    ```

7.  <span data-ttu-id="58697-391">Juste en dessous de la méthode **FetchAnalytics ()** , ajoutez une méthode appelée **GetWebRequest ()** , qui retourne un *IEnumerator*.</span><span class="sxs-lookup"><span data-stu-id="58697-391">Right below the **FetchAnalytics()** method, add a method called **GetWebRequest()**, which returns an *IEnumerator*.</span></span> <span data-ttu-id="58697-392">Cette méthode est chargée de demander le nombre de fois qu’un événement, correspondant à un *gameobject*spécifique, a été appelé dans *application Insights*.</span><span class="sxs-lookup"><span data-stu-id="58697-392">This method is responsible for requesting the number of times an event, corresponding with a specific *GameObject*, has been called within *Application Insights*.</span></span> <span data-ttu-id="58697-393">Lorsque toutes les requêtes envoyées ont été retournées, la méthode **DetermineWinner ()** est appelée.</span><span class="sxs-lookup"><span data-stu-id="58697-393">When all the sent queries have returned, the **DetermineWinner()** method is called.</span></span>

    ```csharp
        /// <summary>
        /// Requests the data count for number of events, according to the
        /// input query URL.
        /// </summary>
        /// <param name="webQueryPair">Query URL and the list number count.</param>
        /// <returns></returns>
        private IEnumerator GetWebRequest(KeyValuePair<string, int> webQueryPair)
        {
            // Set the URL and count as their own variables (for readibility).
            string url = webQueryPair.Key;
            int currentCount = webQueryPair.Value;

            using (UnityWebRequest unityWebRequest = UnityWebRequest.Get(url))
            {
                DownloadHandlerBuffer handlerBuffer = new DownloadHandlerBuffer();

                unityWebRequest.downloadHandler = handlerBuffer;

                unityWebRequest.SetRequestHeader("host", "api.applicationinsights.io");

                unityWebRequest.SetRequestHeader("x-api-key", ApplicationInsightsTracker.Instance.API_Key);

                yield return unityWebRequest.SendWebRequest();

                if (unityWebRequest.isNetworkError)
                {
                    // Failure with web request.
                    Debug.Log("<color=red>Error Sending:</color> " + unityWebRequest.error);
                }
                else
                {
                    // This query has returned, so add to the current count.
                    _queriesReturned++;

                    // Initialize event count integer.
                    int eventCount = 0;

                    // Deserialize the response with the custom Analytics class.
                    Analytics welcome = JsonConvert.DeserializeObject<Analytics>(unityWebRequest.downloadHandler.text);

                    // Get and return the count for the Event
                    if (int.TryParse(welcome.OdataCount, out eventCount) == false)
                    {
                        // Parsing failed. Can sometimes mean that the Query URL was incorrect.
                        Debug.Log("<color=red>Failure to Parse Data Results. Check Query URL for issues.</color>");
                    }
                    else
                    {
                        // Overwrite the current pair, with its actual values, now that the event count is known.
                        _pairedObjectsWithEventCount[currentCount] = new KeyValuePair<GameObject, int>(_pairedObjectsWithEventCount[currentCount].Key, eventCount);
                    }

                    // If all queries (compared with the number which was sent away) have 
                    // returned, then run the determine winner method. 
                    if (_queriesReturned == _pairedObjectsWithEventCount.Count)
                    {
                        DetermineWinner();
                    }
                }
            }
        }
    ```

8.  <span data-ttu-id="58697-394">La méthode suivante est **DetermineWinner ()** , qui trie la liste de paires *gameobject* et *int* , en fonction du nombre d’événements le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="58697-394">The next method is **DetermineWinner()**, which sorts the list of *GameObject* and *Int* pairs, according to the highest event count.</span></span> <span data-ttu-id="58697-395">Il modifie ensuite la couleur matérielle de ce *gameobject* en *vert* (en tant que commentaire pour qu’il ait le plus grand nombre).</span><span class="sxs-lookup"><span data-stu-id="58697-395">It then changes the material color of that *GameObject* to *green* (as feedback for it having the highest count).</span></span> <span data-ttu-id="58697-396">Un message s’affiche avec les résultats de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="58697-396">This displays a message with the analytics results.</span></span>

    ```csharp
        /// <summary>
        /// Call to determine the keyValue pair, within the objects list, 
        /// with the highest event count.
        /// </summary>
        private void DetermineWinner()
        {
            // Sort the values within the list of pairs.
            _pairedObjectsWithEventCount.Sort((x, y) => y.Value.CompareTo(x.Value));

            // Change its colour to green
            _pairedObjectsWithEventCount.First().Key.GetComponent<Renderer>().material.color = Color.green;

            // Provide the winner, and other results, within the console window. 
            string message = $"<b>Analytics Results:</b>\n " +
                $"<i>{_pairedObjectsWithEventCount.First().Key.name}</i> has the highest event count, " +
                $"with <i>{_pairedObjectsWithEventCount.First().Value.ToString()}</i>.\nFollowed by: ";

            for (int i = 1; i < _pairedObjectsWithEventCount.Count; i++)
            {
                message += $"{_pairedObjectsWithEventCount[i].Key.name}, " +
                    $"with {_pairedObjectsWithEventCount[i].Value.ToString()} events.\n";
            }

            Debug.Log(message);
        }
    ```

9.  <span data-ttu-id="58697-397">Ajoutez la structure de classe qui sera utilisée pour désérialiser l’objet JSON, reçu de *application Insights*.</span><span class="sxs-lookup"><span data-stu-id="58697-397">Add the class structure which will be used to deserialize the JSON object, received from *Application Insights*.</span></span> <span data-ttu-id="58697-398">Ajoutez ces classes au bas de votre fichier de classe **DataFromAnalytics** , **en dehors** de la définition de classe.</span><span class="sxs-lookup"><span data-stu-id="58697-398">Add these classes at the very bottom of your **DataFromAnalytics** class file, **outside** of the class definition.</span></span>

    ```csharp
        /// <summary>
        /// These classes represent the structure of the JSON response from Azure Insight
        /// </summary>
        [Serializable]
        public class Analytics
        {
            [JsonProperty("@odata.context")]
            public string OdataContext { get; set; }

            [JsonProperty("@odata.count")]
            public string OdataCount { get; set; }

            [JsonProperty("value")]
            public Value[] Value { get; set; }
        }

        [Serializable]
        public class Value
        {
            [JsonProperty("customMetric")]
            public CustomMetric CustomMetric { get; set; }
        }

        [Serializable]
        public class CustomMetric
        {
            [JsonProperty("name")]
            public string Name { get; set; }
        }
    ```

10. <span data-ttu-id="58697-399">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="58697-399">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-10---create-the-movement-class"></a><span data-ttu-id="58697-400">Chapitre 10-créer la classe de mouvement</span><span class="sxs-lookup"><span data-stu-id="58697-400">Chapter 10 - Create the Movement class</span></span>

<span data-ttu-id="58697-401">Le script de **déplacement** est le prochain script que vous devrez créer.</span><span class="sxs-lookup"><span data-stu-id="58697-401">The **Movement** script is the next script you will need to create.</span></span> <span data-ttu-id="58697-402">Il est responsable des tâches suivantes:</span><span class="sxs-lookup"><span data-stu-id="58697-402">It is responsible for:</span></span>

- <span data-ttu-id="58697-403">Déplacement de la caméra principale en fonction de la direction vers laquelle l’appareil photo regarde.</span><span class="sxs-lookup"><span data-stu-id="58697-403">Moving the Main Camera according to the direction the camera is looking towards.</span></span>
- <span data-ttu-id="58697-404">Ajout de tous les autres scripts aux objets de scène.</span><span class="sxs-lookup"><span data-stu-id="58697-404">Adding all other scripts to scene objects.</span></span>

<span data-ttu-id="58697-405">Pour créer le script:</span><span class="sxs-lookup"><span data-stu-id="58697-405">To create the script:</span></span>

1.  <span data-ttu-id="58697-406">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="58697-406">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="58697-407">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer**  >   **C# un script**.</span><span class="sxs-lookup"><span data-stu-id="58697-407">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="58697-408">Nommez le **mouvement**du script.</span><span class="sxs-lookup"><span data-stu-id="58697-408">Name the script **Movement**.</span></span>

3.  <span data-ttu-id="58697-409">Double-cliquez sur le script pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="58697-409">Double-click on the script to open it with *Visual Studio*.</span></span>

4.  <span data-ttu-id="58697-410">Remplacez le code existant par le code ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="58697-410">Replace the existing code with the following:</span></span>

    ```csharp
        using UnityEngine;
        using UnityEngine.XR.WSA.Input;

        public class Movement : MonoBehaviour
        {
            /// <summary>
            /// The rendered object representing the right controller.
            /// </summary>
            public GameObject Controller;

            /// <summary>
            /// The movement speed of the user.
            /// </summary>
            public float UserSpeed;

            /// <summary>
            /// Provides whether source updates have been registered.
            /// </summary>
            private bool _isAttached = false;

            /// <summary>
            /// The chosen controller hand to use. 
            /// </summary>
            private InteractionSourceHandedness _handness = InteractionSourceHandedness.Right;

            /// <summary>
            /// Used to calculate and proposes movement translation.
            /// </summary>
            private Vector3 _playerMovementTranslation;

            private void Start()
            {
                // You are now adding components dynamically 
                // to ensure they are existing on the correct object  

                // Add all camera related scripts to the camera. 
                Camera.main.gameObject.AddComponent<Gaze>();
                Camera.main.gameObject.AddComponent<ObjectTrigger>();
        
                // Add all other scripts to this object.
                gameObject.AddComponent<ApplicationInsightsTracker>();
                gameObject.AddComponent<DataFromAnalytics>();
            }

            // Update is called once per frame
            void Update()
            {
            
            }
        }
    ```

5.  <span data-ttu-id="58697-411">Dans la classe de **déplacement** , *sous* la méthode empty **Update ()** , insérez les méthodes suivantes qui permettent à l’utilisateur d’utiliser le contrôleur de main pour se déplacer dans l’espace virtuel:</span><span class="sxs-lookup"><span data-stu-id="58697-411">Within the **Movement** class, *below* the empty **Update()** method, insert the following methods that allow the user to use the hand controller to move in the virtual space:</span></span>

    ```csharp
        /// <summary>
        /// Used for tracking the current position and rotation of the controller.
        /// </summary>
        private void UpdateControllerState()
        {
    #if UNITY_WSA && UNITY_2017_2_OR_NEWER
            // Check for current connected controllers, only if WSA.
            string message = string.Empty;

            if (InteractionManager.GetCurrentReading().Length > 0)
            {
                foreach (var sourceState in InteractionManager.GetCurrentReading())
                {
                    if (sourceState.source.kind == InteractionSourceKind.Controller && sourceState.source.handedness == _handness)
                    {
                        // If a controller source is found, which matches the selected handness, 
                        // check whether interaction source updated events have been registered. 
                        if (_isAttached == false)
                        {
                            // Register events, as not yet registered.
                            message = "<color=green>Source Found: Registering Controller Source Events</color>";
                            _isAttached = true;

                            InteractionManager.InteractionSourceUpdated += InteractionManager_InteractionSourceUpdated;
                        }

                        // Update the position and rotation information for the controller.
                        Vector3 newPosition;
                        if (sourceState.sourcePose.TryGetPosition(out newPosition, InteractionSourceNode.Pointer) && ValidPosition(newPosition))
                        {
                            Controller.transform.localPosition = newPosition;
                        }

                        Quaternion newRotation;

                        if (sourceState.sourcePose.TryGetRotation(out newRotation, InteractionSourceNode.Pointer) && ValidRotation(newRotation))
                        {
                            Controller.transform.localRotation = newRotation;
                        }
                    }
                }
            }
            else
            {
                // Controller source not detected. 
                message = "<color=blue>Trying to detect controller source</color>";

                if (_isAttached == true)
                {
                    // A source was previously connected, however, has been lost. Disconnected
                    // all registered events. 

                    _isAttached = false;

                    InteractionManager.InteractionSourceUpdated -= InteractionManager_InteractionSourceUpdated;

                    message = "<color=red>Source Lost: Detaching Controller Source Events</color>";
                }
            }

            if(message != string.Empty)
            {
                Debug.Log(message);
            }
    #endif
        }
    ```

    ```csharp
        /// <summary>
        /// This registered event is triggered when a source state has been updated.
        /// </summary>
        /// <param name="obj"></param>
        private void InteractionManager_InteractionSourceUpdated(InteractionSourceUpdatedEventArgs obj)
        {
            if (obj.state.source.handedness == _handness)
            {
                if(obj.state.thumbstickPosition.magnitude > 0.2f)
                {
                    float thumbstickY = obj.state.thumbstickPosition.y;

                    // Vertical Input.
                    if (thumbstickY > 0.3f || thumbstickY < -0.3f)
                    {
                        _playerMovementTranslation = Camera.main.transform.forward;
                        _playerMovementTranslation.y = 0;
                        transform.Translate(_playerMovementTranslation * UserSpeed * Time.deltaTime * thumbstickY, Space.World);
                    }
                }
            }
        }
    ```

    ```csharp
        /// <summary>
        /// Check that controller position is valid. 
        /// </summary>
        /// <param name="inputVector3">The Vector3 to check</param>
        /// <returns>The position is valid</returns>
        private bool ValidPosition(Vector3 inputVector3)
        {
            return !float.IsNaN(inputVector3.x) && !float.IsNaN(inputVector3.y) && !float.IsNaN(inputVector3.z) && !float.IsInfinity(inputVector3.x) && !float.IsInfinity(inputVector3.y) && !float.IsInfinity(inputVector3.z);
        }

        /// <summary>
        /// Check that controller rotation is valid. 
        /// </summary>
        /// <param name="inputQuaternion">The Quaternion to check</param>
        /// <returns>The rotation is valid</returns>
        private bool ValidRotation(Quaternion inputQuaternion)
        {
            return !float.IsNaN(inputQuaternion.x) && !float.IsNaN(inputQuaternion.y) && !float.IsNaN(inputQuaternion.z) && !float.IsNaN(inputQuaternion.w) && !float.IsInfinity(inputQuaternion.x) && !float.IsInfinity(inputQuaternion.y) && !float.IsInfinity(inputQuaternion.z) && !float.IsInfinity(inputQuaternion.w);
        }   
    ```

6.  <span data-ttu-id="58697-412">Enfin, ajoutez l’appel de méthode dans la méthode **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="58697-412">Lastly add the method call within the **Update()** method.</span></span>

    ```csharp
        // Update is called once per frame
        void Update()
        {
            UpdateControllerState();
        }
    ```

7.  <span data-ttu-id="58697-413">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="58697-413">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-11---setting-up-the-scripts-references"></a><span data-ttu-id="58697-414">Chapitre 11-configuration des références de scripts</span><span class="sxs-lookup"><span data-stu-id="58697-414">Chapter 11 - Setting up the scripts references</span></span>

<span data-ttu-id="58697-415">Dans ce chapitre, vous devez placer le script de **déplacement** sur le parent de l' **appareil photo** et définir ses cibles de référence.</span><span class="sxs-lookup"><span data-stu-id="58697-415">In this Chapter you need to place the **Movement** script onto the **Camera Parent** and set its reference targets.</span></span> <span data-ttu-id="58697-416">Ce script gère alors le placement des autres scripts là où ils doivent être.</span><span class="sxs-lookup"><span data-stu-id="58697-416">That script will then handle placing the other scripts where they need to be.</span></span>

1.  <span data-ttu-id="58697-417">Dans le dossier **scripts** du *panneau Projet*, faites glisser le script de **déplacement** vers l’objet parent de l' **appareil photo** , situé dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="58697-417">From the **Scripts** folder in the *Project Panel*, drag the **Movement** script to the **Camera Parent** object, located in the *Hierarchy Panel*.</span></span>

    ![Configuration des références de scripts dans la scène Unity](images/AzureLabs-Lab309-48.png)

2.  <span data-ttu-id="58697-419">Cliquez sur le **parent de l’appareil photo**.</span><span class="sxs-lookup"><span data-stu-id="58697-419">Click on the **Camera Parent**.</span></span> <span data-ttu-id="58697-420">Dans le *volet hiérarchie*, faites glisser l’objet de **droite** du *volet* de la hiérarchie vers la cible de référence, **contrôleur**, dans le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="58697-420">In the *Hierarchy Panel*, drag the **Right Hand** object from the *Hierarchy Panel* to the reference target, **Controller**, in the *Inspector Panel*.</span></span> <span data-ttu-id="58697-421">Définissez la **Vitesse** de l’utilisateur sur **5**, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="58697-421">Set the **User Speed** to **5**, as shown in the image below.</span></span>

    ![Configuration des références de scripts dans la scène Unity](images/AzureLabs-Lab309-49.png)

## <a name="chapter-12---build-the-unity-project"></a><span data-ttu-id="58697-423">Chapitre 12-générer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="58697-423">Chapter 12 - Build the Unity project</span></span>

<span data-ttu-id="58697-424">Tout ce qui est nécessaire pour la section Unity de ce projet est maintenant terminé. il est donc temps de la générer à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="58697-424">Everything needed for the Unity section of this project has now been completed, so it is time to build it from Unity.</span></span>

1.  <span data-ttu-id="58697-425">Accédez à **paramètres de build**, (**paramètres de génération**de**fichier** > ).</span><span class="sxs-lookup"><span data-stu-id="58697-425">Navigate to **Build Settings**, (**File** > **Build Settings**).</span></span>

2.  <span data-ttu-id="58697-426">Dans la fenêtre **paramètres de build** , cliquez sur **générer**.</span><span class="sxs-lookup"><span data-stu-id="58697-426">From the **Build Settings** window, click **Build**.</span></span>

    ![Générer le projet Unity dans la solution UWP](images/AzureLabs-Lab309-50.png)

3.  <span data-ttu-id="58697-428">Une fenêtre de l' **Explorateur de fichiers** s’affiche et vous invite à entrer un emplacement pour la Build.</span><span class="sxs-lookup"><span data-stu-id="58697-428">A **File Explorer** window will pop-up, prompting you for a location for the build.</span></span> <span data-ttu-id="58697-429">Créez un nouveau dossier (en cliquant sur **nouveau dossier** dans l’angle supérieur gauche), puis nommez -le builds.</span><span class="sxs-lookup"><span data-stu-id="58697-429">Create a new folder (by clicking **New Folder** in the top-left corner), and name it **BUILDS**.</span></span>

    ![Générer le projet Unity dans la solution UWP](images/AzureLabs-Lab309-51.png)

    1.  <span data-ttu-id="58697-431">Ouvrez le nouveau  dossier Builds, puis créez un autre dossier (à l’aide d’un **nouveau dossier** ) et nommez-le **Mr\_\_Azure application\_Insights**.</span><span class="sxs-lookup"><span data-stu-id="58697-431">Open the new **BUILDS** folder, and create another folder (using **New Folder** once more), and name it **MR\_Azure\_Application\_Insights**.</span></span>

        ![Générer le projet Unity dans la solution UWP](images/AzureLabs-Lab309-52.png)

    2.  <span data-ttu-id="58697-433">Après avoir sélectionné le dossier **\_RM Azure\_application\_Insights** , cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="58697-433">With the **MR\_Azure\_Application\_Insights** folder selected, click **Select Folder**.</span></span> <span data-ttu-id="58697-434">La génération du projet prendra quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="58697-434">The project will take a minute or so to build.</span></span>

4.  <span data-ttu-id="58697-435">Après la *génération*, l' **Explorateur de fichiers** s’affiche et vous indique l’emplacement de votre nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="58697-435">Following *Build*, **File Explorer** will appear showing you the location of your new project.</span></span>

## <a name="chapter-13---deploy-mrazureapplicationinsights-app-to-your-machine"></a><span data-ttu-id="58697-436">Chapitre 13: déployer l’application MR_Azure_Application_Insights sur votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="58697-436">Chapter 13 - Deploy MR_Azure_Application_Insights app to your machine</span></span>

<span data-ttu-id="58697-437">Pour déployer l' **application\_Azure\_application\_Insights RM** sur votre ordinateur local:</span><span class="sxs-lookup"><span data-stu-id="58697-437">To deploy the **MR\_Azure\_Application\_Insights** app on your Local Machine:</span></span>

1.  <span data-ttu-id="58697-438">Ouvrez le fichier solution de votre **\_application Azure\_application\_Insights** dans **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="58697-438">Open the solution file of your **MR\_Azure\_Application\_Insights** app in **Visual Studio**.</span></span>

2.  <span data-ttu-id="58697-439">Dans la **plateforme**de la solution, sélectionnez **x86, ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="58697-439">In the **Solution Platform**, select **x86, Local Machine**.</span></span>

3.  <span data-ttu-id="58697-440">Dans la **configuration** de la solution, sélectionnez Déboguer.</span><span class="sxs-lookup"><span data-stu-id="58697-440">In the **Solution Configuration** select **Debug**.</span></span>

    ![Générer le projet Unity dans la solution UWP](images/AzureLabs-Lab309-53.png)

4.  <span data-ttu-id="58697-442">Accédez au **menu Générer** , puis cliquez sur **déployer la solution** pour chargement l’application sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="58697-442">Go to **Build menu** and click on **Deploy Solution** to sideload the application to your machine.</span></span>

5.  <span data-ttu-id="58697-443">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancées.</span><span class="sxs-lookup"><span data-stu-id="58697-443">Your app should now appear in the list of installed apps, ready to be launched.</span></span>

6. <span data-ttu-id="58697-444">Lancez l’application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="58697-444">Launch the mixed reality application.</span></span>

7. <span data-ttu-id="58697-445">Déplacez-vous dans la scène, en approchant les objets et en examinant ces derniers, lorsque le *service Azure Insight* a collecté suffisamment de données d’événement, il définit l’objet qui a été le plus proche du vert.</span><span class="sxs-lookup"><span data-stu-id="58697-445">Move around the scene, approaching objects and looking at them, when the *Azure Insight Service* has collected enough event data, it will set the object that has been approached the most to green.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="58697-446">Alors que le temps d’attente moyen pour les *événements et* les métriques à collecter par le service prend environ 15 minutes, dans certains cas, cela peut prendre jusqu’à 1 heure.</span><span class="sxs-lookup"><span data-stu-id="58697-446">While the average waiting time for the *Events and Metrics* to be collected by the Service takes around 15 min, in some occasions it might take up to 1 hour.</span></span>

## <a name="chapter-14---the-application-insights-service-portal"></a><span data-ttu-id="58697-447">Chapitre 14-Application Insights Service Portal</span><span class="sxs-lookup"><span data-stu-id="58697-447">Chapter 14 - The Application Insights Service portal</span></span>

<span data-ttu-id="58697-448">Une fois que vous avez accédé à la scène et que vous avez placé un regard sur plusieurs objets, vous pouvez voir les données collectées dans le portail de *Service application Insights* .</span><span class="sxs-lookup"><span data-stu-id="58697-448">Once you have roamed around the scene and gazed at several objects you can see the data collected in the *Application Insights Service* portal.</span></span>

1.  <span data-ttu-id="58697-449">Revenez à votre portail de service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="58697-449">Go back to your Application Insights Service portal.</span></span>

2.  <span data-ttu-id="58697-450">Cliquez sur *Metrics Explorer*.</span><span class="sxs-lookup"><span data-stu-id="58697-450">Click on *Metrics Explorer*.</span></span>

    ![Examen des données collectées](images/AzureLabs-Lab309-54.png)

3.  <span data-ttu-id="58697-452">Elle s’ouvre dans un onglet contenant le graphique qui représente les *événements et* les métriques associés à votre application.</span><span class="sxs-lookup"><span data-stu-id="58697-452">It will open in a tab containing the graph which represent the *Events and Metrics* related to your application.</span></span> <span data-ttu-id="58697-453">Comme indiqué ci-dessus, l’affichage des données dans le graphique peut prendre un certain temps (jusqu’à 1 heure).</span><span class="sxs-lookup"><span data-stu-id="58697-453">As mentioned above, it might take some time (up to 1 hour) for the data to be displayed in the graph</span></span>

    ![Examen des données collectées](images/AzureLabs-Lab309-55.png)

4.  <span data-ttu-id="58697-455">Cliquez sur la *barre des événements* dans le *total des événements* par version de l’application pour afficher une répartition détaillée des événements avec leurs noms.</span><span class="sxs-lookup"><span data-stu-id="58697-455">Click on the *Events bar* in the *Total of Events* by Application Version, to see a detailed breakdown of the events with their names.</span></span>

    ![Examen des données collectées](images/AzureLabs-Lab309-56.png)

## <a name="your-finished-your-application-insights-service-application"></a><span data-ttu-id="58697-457">Votre application de service Application Insights est terminée</span><span class="sxs-lookup"><span data-stu-id="58697-457">Your finished your Application Insights Service application</span></span>

<span data-ttu-id="58697-458">Félicitations, vous avez créé une application de réalité mixte qui tire parti du service Application Insights pour surveiller l’activité de l’utilisateur au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="58697-458">Congratulations, you built a mixed reality app that leverages the Application Insights Service to monitor user's activity within your app.</span></span>

![résultat du cours](images/AzureLabs-Lab309-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="58697-460">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="58697-460">Bonus Exercises</span></span>

<span data-ttu-id="58697-461">**Exercice 1**</span><span class="sxs-lookup"><span data-stu-id="58697-461">**Exercise 1**</span></span>

<span data-ttu-id="58697-462">Essayez de créer dynamiquement, plutôt que de créer manuellement les objets ObjectInScene et de définir leurs coordonnées sur le plan au sein de vos scripts.</span><span class="sxs-lookup"><span data-stu-id="58697-462">Try spawning, rather than manually creating, the ObjectInScene objects and set their coordinates on the plane within your scripts.</span></span> <span data-ttu-id="58697-463">De cette façon, vous pouvez demander à Azure ce que l’objet le plus populaire était (des résultats de proximité ou de proximité) et générer un *supplément* à l’un de ces objets.</span><span class="sxs-lookup"><span data-stu-id="58697-463">In this way, you could ask Azure what the most popular object was (either from gaze or proximity results) and spawn an *extra* one of those objects.</span></span>

<span data-ttu-id="58697-464">**Exercice 2**</span><span class="sxs-lookup"><span data-stu-id="58697-464">**Exercise 2**</span></span>

<span data-ttu-id="58697-465">Triez vos résultats Application Insights par heure, afin d’obtenir les données les plus pertinentes, et d’implémenter ces données sensibles au temps dans votre application.</span><span class="sxs-lookup"><span data-stu-id="58697-465">Sort your Application Insights results by time, so that you get the most relevant data, and implement that time sensitive data in your application.</span></span>

