---
title: MR et Azure 309 - Application insights
description: Terminer ce cours pour apprendre à collecter analytique concernant le comportement des utilisateurs au sein d’une application de réalité mixte, à l’aide du Service Azure Application Insights.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, insights d’application, hololens, immersives, vr
ms.openlocfilehash: e14a32f9a38e3e8f3054d19310782f7c2d4784a1
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694570"
---
>[!NOTE]
><span data-ttu-id="c8471-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="c8471-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="c8471-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="c8471-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="c8471-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="c8471-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="c8471-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c8471-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="c8471-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="c8471-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="c8471-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="c8471-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br> 

# <a name="mr-and-azure-309-application-insights"></a><span data-ttu-id="c8471-110">MR et Azure 309 : Insights d’application</span><span class="sxs-lookup"><span data-stu-id="c8471-110">MR and Azure 309: Application insights</span></span>

![produit final-Démarrer](images/AzureLabs-Lab309-00.png)

<span data-ttu-id="c8471-112">Dans ce cours, vous allez apprendre à ajouter des fonctionnalités d’Application Insights à une application de réalité mixte, à l’aide de l’API Azure Application Insights pour collecter analytique concernant le comportement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c8471-112">In this course, you will learn how to add Application Insights capabilities to a mixed reality application, using the Azure Application Insights API to collect analytics regarding user behavior.</span></span>

<span data-ttu-id="c8471-113">Application Insights est un service Microsoft, permettant aux développeurs de collecter analytique à partir de leurs applications et de gérer à partir d’un portail facile à utiliser.</span><span class="sxs-lookup"><span data-stu-id="c8471-113">Application Insights is a Microsoft service, allowing developers to collect analytics from their applications and manage it from an easy-to-use portal.</span></span> <span data-ttu-id="c8471-114">L’analytique peut être des performances pour les informations personnalisées que vous souhaitez collecter.</span><span class="sxs-lookup"><span data-stu-id="c8471-114">The analytics can be anything from performance to custom information you would like to collect.</span></span> <span data-ttu-id="c8471-115">Pour plus d’informations, visitez le [page Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="c8471-115">For more information, visit the [Application Insights page](https://azure.microsoft.com/services/application-insights/).</span></span>

<span data-ttu-id="c8471-116">Avoir terminé ce cours, vous disposez d’une application de casque immersives de réalité mixte qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8471-116">Having completed this course, you will have a mixed reality immersive headset application which will be able to do the following:</span></span>

1.  <span data-ttu-id="c8471-117">Autoriser l’utilisateur à l’utilisation et vous déplacer dans une scène.</span><span class="sxs-lookup"><span data-stu-id="c8471-117">Allow the user to gaze and move around a scene.</span></span>
2.  <span data-ttu-id="c8471-118">Déclencher l’envoi d’analytique pour le *Service Application Insights*, via l’utilisation du pointage de regard et proximité avec les objets de contexte.</span><span class="sxs-lookup"><span data-stu-id="c8471-118">Trigger the sending of analytics to the *Application Insights Service*, through the use of Gaze and Proximity to in-scene objects.</span></span>
3.  <span data-ttu-id="c8471-119">L’application appellera également sur le Service, l’extraction d’informations sur l’objet a été a élaboré le meilleur par l’utilisateur, dans les dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="c8471-119">The app will also call upon the Service, fetching information about which object has been approached the most by the user, within the last 24 hours.</span></span> <span data-ttu-id="c8471-120">Cet objet sera modifier sa couleur verte.</span><span class="sxs-lookup"><span data-stu-id="c8471-120">That object will change its color to green.</span></span>

<span data-ttu-id="c8471-121">Ce cours va vous apprendre à obtenir les résultats à partir du Service Application Insights, dans une application basée sur Unity.</span><span class="sxs-lookup"><span data-stu-id="c8471-121">This course will teach you how to get the results from the Application Insights Service, into a Unity-based sample application.</span></span> <span data-ttu-id="c8471-122">Il le sera jusqu'à vous permettent d’appliquer ces concepts à une application personnalisée, que vous voudrez peut-être générer.</span><span class="sxs-lookup"><span data-stu-id="c8471-122">It will be up to you to apply these concepts to a custom application you might be building.</span></span>

## <a name="device-support"></a><span data-ttu-id="c8471-123">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="c8471-123">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="c8471-124">Cours</span><span class="sxs-lookup"><span data-stu-id="c8471-124">Course</span></span></th><th style="width:150px"> <span data-ttu-id="c8471-125"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="c8471-125"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="c8471-126"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="c8471-126"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="c8471-127">MR et Azure 309 : Insights d’application</span><span class="sxs-lookup"><span data-stu-id="c8471-127">MR and Azure 309: Application insights</span></span></td><td style="text-align: center;"> <span data-ttu-id="c8471-128">✔️</span><span class="sxs-lookup"><span data-stu-id="c8471-128">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="c8471-129">✔️</span><span class="sxs-lookup"><span data-stu-id="c8471-129">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="c8471-130">Si ce cours se concentre principalement sur des casques Windows Mixed Reality IMMERSIFS (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours pour Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="c8471-130">While this course primarily focuses on Windows Mixed Reality immersive (VR) headsets, you can also apply what you learn in this course to Microsoft HoloLens.</span></span> <span data-ttu-id="c8471-131">Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="c8471-131">As you follow along with the course, you will see notes on any changes you might need to employ to support HoloLens.</span></span> <span data-ttu-id="c8471-132">Lorsque vous utilisez HoloLens, vous pouvez remarquer quelques echo durant la capture de la voix.</span><span class="sxs-lookup"><span data-stu-id="c8471-132">When using HoloLens, you may notice some echo during voice capture.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8471-133">Prérequis</span><span class="sxs-lookup"><span data-stu-id="c8471-133">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="c8471-134">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="c8471-134">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="c8471-135">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (juillet 2018).</span><span class="sxs-lookup"><span data-stu-id="c8471-135">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (July 2018).</span></span> <span data-ttu-id="c8471-136">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c8471-136">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you will find in newer software than what is listed below.</span></span>

<span data-ttu-id="c8471-137">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="c8471-137">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="c8471-138">Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)</span><span class="sxs-lookup"><span data-stu-id="c8471-138">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="c8471-139">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="c8471-139">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="c8471-140">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="c8471-140">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="c8471-141">Unity 2017.4</span><span class="sxs-lookup"><span data-stu-id="c8471-141">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="c8471-142">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c8471-142">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="c8471-143">Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="c8471-143">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="c8471-144">Un ensemble de casque avec un microphone intégré (si le casque n’a pas un mic intégré et les haut-parleurs)</span><span class="sxs-lookup"><span data-stu-id="c8471-144">A set of headphones with a built-in microphone (if the headset does not have a built-in mic and speakers)</span></span>
- <span data-ttu-id="c8471-145">Accès à Internet pour le programme d’installation Azure et l’extraction de données Application Insights</span><span class="sxs-lookup"><span data-stu-id="c8471-145">Internet access for Azure setup and Application Insights data retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c8471-146">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="c8471-146">Before you start</span></span>

<span data-ttu-id="c8471-147">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="c8471-147">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>

> [!WARNING] 
> <span data-ttu-id="c8471-148">Gardez à l’esprit, données transférées vers *Application Insights* prend du temps, par conséquent, soyez patient.</span><span class="sxs-lookup"><span data-stu-id="c8471-148">Be aware, data going to *Application Insights* takes time, so be patient.</span></span> <span data-ttu-id="c8471-149">Si vous souhaitez vérifier si le Service a reçu vos données, consultez [chapitre 14](#chapter-14---the-application-insights-service-portal), qui illustrent comment naviguer dans le portail.</span><span class="sxs-lookup"><span data-stu-id="c8471-149">If you want to check if the Service has received your data, check out [Chapter 14](#chapter-14---the-application-insights-service-portal), which will show you how to navigate the portal.</span></span>

## <a name="chapter-1---the-azure-portal"></a><span data-ttu-id="c8471-150">Chapitre 1 : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="c8471-150">Chapter 1 - The Azure Portal</span></span>

<span data-ttu-id="c8471-151">Pour utiliser *Application Insights*, vous devez créer et configurer un *Service Application Insights* dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c8471-151">To use *Application Insights*, you will need to create and configure an *Application Insights Service* in the Azure portal.</span></span>

1.  <span data-ttu-id="c8471-152">Connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c8471-152">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE]
    > <span data-ttu-id="c8471-153">Si vous n’avez pas déjà un compte Azure, vous devrez créer un.</span><span class="sxs-lookup"><span data-stu-id="c8471-153">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="c8471-154">Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="c8471-154">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="c8471-155">Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez *Application Insights*, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="c8471-155">Once you are logged in, click on **New** in the top left corner, and search for *Application Insights*, and click **Enter**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c8471-156">Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.</span><span class="sxs-lookup"><span data-stu-id="c8471-156">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-01.png)

3.  <span data-ttu-id="c8471-158">La nouvelle page à droite fournit une description de la *Azure Application Insights* Service.</span><span class="sxs-lookup"><span data-stu-id="c8471-158">The new page to the right will provide a description of the *Azure Application Insights* Service.</span></span> <span data-ttu-id="c8471-159">En bas à gauche de cette page, sélectionnez le **créer** bouton, pour créer une association avec ce Service.</span><span class="sxs-lookup"><span data-stu-id="c8471-159">At the bottom left of this page, select the **Create** button, to create an association with this Service.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-02.png)

4.  <span data-ttu-id="c8471-161">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="c8471-161">Once you have clicked on **Create**:</span></span>

    1.  <span data-ttu-id="c8471-162">Insérez votre souhaitée **nom** pour cette instance de Service.</span><span class="sxs-lookup"><span data-stu-id="c8471-162">Insert your desired **Name** for this Service instance.</span></span>

    2.  <span data-ttu-id="c8471-163">En tant que **Type d’Application**, sélectionnez **général**.</span><span class="sxs-lookup"><span data-stu-id="c8471-163">As **Application Type**, select **General**.</span></span>

    3.  <span data-ttu-id="c8471-164">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="c8471-164">Select an appropriate **Subscription**.</span></span>

    4.  <span data-ttu-id="c8471-165">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="c8471-165">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="c8471-166">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="c8471-166">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="c8471-167">Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="c8471-167">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

        > <span data-ttu-id="c8471-168">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="c8471-168">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5.  <span data-ttu-id="c8471-169">Sélectionnez un **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="c8471-169">Select a **Location**.</span></span>

    6.  <span data-ttu-id="c8471-170">Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.</span><span class="sxs-lookup"><span data-stu-id="c8471-170">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    7.  <span data-ttu-id="c8471-171">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c8471-171">Select **Create**.</span></span>

        ![Portail Azure](images/AzureLabs-Lab309-03.png)

5.  <span data-ttu-id="c8471-173">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le Service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="c8471-173">Once you have clicked on **Create**, you will have to wait for the Service to be created, this might take a minute.</span></span>

6.  <span data-ttu-id="c8471-174">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="c8471-174">A notification will appear in the portal once the Service instance is created.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-04.png)

7.  <span data-ttu-id="c8471-176">Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="c8471-176">Click on the notifications to explore your new Service instance.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-05.png)

8.  <span data-ttu-id="c8471-178">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="c8471-178">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="c8471-179">Vous serez dirigé vers votre nouvelle *Service Application Insights* instance.</span><span class="sxs-lookup"><span data-stu-id="c8471-179">You will be taken to your new *Application Insights Service* instance.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-06.png)

    > [!NOTE]
    >  <span data-ttu-id="c8471-181">Ne fermez pas cette page web et faciles d’accès, vous serez revenez ici régulièrement pour voir les données collectées.</span><span class="sxs-lookup"><span data-stu-id="c8471-181">Keep this web page open and easy to access, you will come back here often to see the data collected.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c8471-182">Pour implémenter l’Application Insights, vous devez utiliser des valeurs spécifiques trois (3) : **Clé d’instrumentation**, **ID d’Application**, et **clé API**.</span><span class="sxs-lookup"><span data-stu-id="c8471-182">To implement Application Insights, you will need to use three (3) specific values: **Instrumentation Key**, **Application ID**, and **API Key**.</span></span> <span data-ttu-id="c8471-183">Ci-dessous, vous verrez comment récupérer ces valeurs à partir de votre Service.</span><span class="sxs-lookup"><span data-stu-id="c8471-183">Below you will see how to retrieve these values from your Service.</span></span> <span data-ttu-id="c8471-184">Veillez à noter ces valeurs sur une valeur vide *le bloc-notes* page, car vous les utiliserez bientôt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="c8471-184">Make sure to note these values on a blank *Notepad* page, because you will use them soon in your code.</span></span>

9.  <span data-ttu-id="c8471-185">Pour rechercher le **clé d’Instrumentation**, vous devez faire défiler vers le bas la liste des fonctions de Service, puis cliquez sur **propriétés**, révèle l’onglet affiché le **clé du Service**.</span><span class="sxs-lookup"><span data-stu-id="c8471-185">To find the **Instrumentation Key**, you will need to scroll down the list of Service functions, and click on **Properties**, the tab displayed will reveal the **Service Key**.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-07.png)

10. <span data-ttu-id="c8471-187">Un peu ci-dessous **propriétés**, vous trouverez **accès à l’API**, dont vous avez besoin de cliquer sur.</span><span class="sxs-lookup"><span data-stu-id="c8471-187">A little below **Properties**, you will find **API Access**, which you need to click.</span></span> <span data-ttu-id="c8471-188">Le volet à droite fournira la **ID d’Application** de votre application.</span><span class="sxs-lookup"><span data-stu-id="c8471-188">The panel to the right will provide the **Application ID** of your app.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-08.png)

11. <span data-ttu-id="c8471-190">Avec le **ID d’Application** panneau toujours ouverte, cliquez sur **créer une clé API**, qui ouvre le *créer une clé API* Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="c8471-190">With the **Application ID** panel still open, click **Create API Key**, which will open the *Create API key* panel.</span></span>

    ![Portail Azure](images/AzureLabs-Lab309-09.png)

12. <span data-ttu-id="c8471-192">Au sein de l’ouvrir maintenant *créer une clé API* panneau, tapez une description, et **Cochez les trois zones**.</span><span class="sxs-lookup"><span data-stu-id="c8471-192">Within the now open *Create API key* panel, type a description, and **tick the three boxes**.</span></span>

13. <span data-ttu-id="c8471-193">Cliquez sur **générer la clé**.</span><span class="sxs-lookup"><span data-stu-id="c8471-193">Click **Generate Key**.</span></span> <span data-ttu-id="c8471-194">Votre **clé API** sera créé et affiché.</span><span class="sxs-lookup"><span data-stu-id="c8471-194">Your **API Key** will be created and displayed.</span></span> 

    ![Portail Azure](images/AzureLabs-Lab309-10.png)
        
    > [!WARNING]
    > <span data-ttu-id="c8471-196">C’est la seule fois votre **clé Service** s’affiche, assurez-vous donc vous faire une copie de celle-ci maintenant.</span><span class="sxs-lookup"><span data-stu-id="c8471-196">This is the only time your **Service Key** will be displayed, so ensure you make a copy of it now.</span></span>

## <a name="chapter-2---set-up-the-unity-project"></a><span data-ttu-id="c8471-197">Chapitre 2 : configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="c8471-197">Chapter 2 - Set up the Unity project</span></span>

<span data-ttu-id="c8471-198">Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="c8471-198">The following is a typical set up for developing with the mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="c8471-199">Ouvrez *Unity* et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="c8471-199">Open *Unity* and click **New**.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab309-11.png)

2.  <span data-ttu-id="c8471-201">Vous devez maintenant fournir un nom de projet Unity, insérer **MR\_Azure\_Application\_Insights**.</span><span class="sxs-lookup"><span data-stu-id="c8471-201">You will now need to provide a Unity Project name, insert **MR\_Azure\_Application\_Insights**.</span></span> <span data-ttu-id="c8471-202">Assurez-vous que le *modèle* a la valeur **3D**.</span><span class="sxs-lookup"><span data-stu-id="c8471-202">Make sure the *Template* is set to **3D**.</span></span> <span data-ttu-id="c8471-203">Définir le *emplacement* à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="c8471-203">Set the *Location* to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="c8471-204">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="c8471-204">Then, click **Create project**.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab309-12.png)

3.  <span data-ttu-id="c8471-206">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c8471-206">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="c8471-207">Accédez à **modifier \> préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="c8471-207">Go to **Edit \> Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="c8471-208">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="c8471-208">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="c8471-209">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="c8471-209">Close the **Preferences** window.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab309-13.png)

4.  <span data-ttu-id="c8471-211">Ensuite, accédez à **fichier \> paramètres de Build** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **plateforme basculer** bouton.</span><span class="sxs-lookup"><span data-stu-id="c8471-211">Next, go to **File \> Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab309-14.png)

5.  <span data-ttu-id="c8471-213">Accédez à **fichier \> paramètres de Build** et vous assurer que :</span><span class="sxs-lookup"><span data-stu-id="c8471-213">Go to **File \> Build Settings** and make sure that:</span></span>

    1.  <span data-ttu-id="c8471-214">**Équipement cible** a la valeur **n’importe quel appareil**</span><span class="sxs-lookup"><span data-stu-id="c8471-214">**Target Device** is set to **Any device**</span></span>

        > <span data-ttu-id="c8471-215">Pour le Microsoft HoloLens, définissez **appareil cible** à *HoloLens*.</span><span class="sxs-lookup"><span data-stu-id="c8471-215">For the Microsoft HoloLens, set **Target Device** to *HoloLens*.</span></span>

    2.  <span data-ttu-id="c8471-216">**Type de build** a la valeur **D3D**</span><span class="sxs-lookup"><span data-stu-id="c8471-216">**Build Type** is set to **D3D**</span></span>

    3.  <span data-ttu-id="c8471-217">**Kit de développement logiciel** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="c8471-217">**SDK** is set to **Latest installed**</span></span>

    4.  <span data-ttu-id="c8471-218">**Générez et exécutez** est défini sur **ordinateur Local**</span><span class="sxs-lookup"><span data-stu-id="c8471-218">**Build and Run** is set to **Local Machine**</span></span>

    5.  <span data-ttu-id="c8471-219">Enregistrer la scène et l’ajouter à la build.</span><span class="sxs-lookup"><span data-stu-id="c8471-219">Save the scene and add it to the build.</span></span>

        1.  <span data-ttu-id="c8471-220">Cela en sélectionnant **ajouter un arrière-plan Open**.</span><span class="sxs-lookup"><span data-stu-id="c8471-220">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="c8471-221">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c8471-221">A save window will appear.</span></span>

            ![Configurer le projet Unity](images/AzureLabs-Lab309-15.png)

        2. <span data-ttu-id="c8471-223">Créez un dossier pour cela et toutes les scènes future, puis cliquez sur le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.</span><span class="sxs-lookup"><span data-stu-id="c8471-223">Create a new folder for this, and any future scene, then click the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![Configurer le projet Unity](images/AzureLabs-Lab309-16.png)

        3. <span data-ttu-id="c8471-225">Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier :* champ de texte, tapez **ApplicationInsightsScene**, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c8471-225">Open your newly created **Scenes** folder, and then in the *File name:* text field, type **ApplicationInsightsScene**, then click **Save**.</span></span>

            ![Configurer le projet Unity](images/AzureLabs-Lab309-17.png)

6.  <span data-ttu-id="c8471-227">Les autres paramètres, dans **paramètres de Build**, doit être conservé comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="c8471-227">The remaining settings, in **Build Settings**, should be left as default for now.</span></span>

7.  <span data-ttu-id="c8471-228">Dans le **paramètres de Build** fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le **inspecteur** se trouve.</span><span class="sxs-lookup"><span data-stu-id="c8471-228">In the **Build Settings** window, click on the **Player Settings** button, this will open the related panel in the space where the **Inspector** is located.</span></span>

    ![Configurer le projet Unity](images/AzureLabs-Lab309-18.png)

8. <span data-ttu-id="c8471-230">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="c8471-230">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="c8471-231">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="c8471-231">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="c8471-232">**Écriture de scripts** **Version du Runtime** doit être **expérimental (équivalent .NET 4.6)** , ce qui déclenchera une nécessité de redémarrer l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="c8471-232">**Scripting** **Runtime Version** should be **Experimental (.NET 4.6 Equivalent)**, which will trigger a need to restart the Editor.</span></span>

        2.  <span data-ttu-id="c8471-233">**Script principal** doit être **.NET**</span><span class="sxs-lookup"><span data-stu-id="c8471-233">**Scripting Backend** should be **.NET**</span></span>

        3.  <span data-ttu-id="c8471-234">**Niveau de compatibilité d’API** doit être **.NET 4.6**</span><span class="sxs-lookup"><span data-stu-id="c8471-234">**API Compatibility Level** should be **.NET 4.6**</span></span>

        ![Configurer le projet Unity](images/AzureLabs-Lab309-19.png)

    2.  <span data-ttu-id="c8471-236">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="c8471-236">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="c8471-237">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="c8471-237">**InternetClient**</span></span>     

            ![Configurer le projet Unity](images/AzureLabs-Lab309-20.png)

    3.  <span data-ttu-id="c8471-239">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **Windows Mixed Reality Kit de développement logiciel** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="c8471-239">Further down the panel, in **XR Settings** (found below **Publishing Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Configurer le projet Unity](images/AzureLabs-Lab309-21.png)

9.  <span data-ttu-id="c8471-241">Dans **paramètres de Build**, **Unity C# projets** est n’est plus grisée ; Cochez la case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="c8471-241">Back in **Build Settings**, **Unity C# Projects** is no longer greyed out; tick the checkbox next to this.</span></span>

10.  <span data-ttu-id="c8471-242">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="c8471-242">Close the Build Settings window.</span></span>

11.  <span data-ttu-id="c8471-243">Enregistrer votre projet et la scène (**fichier** > **enregistrer la scène / fichier** > **enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="c8471-243">Save your Scene and Project (**FILE** > **SAVE SCENE / FILE** > **SAVE PROJECT**).</span></span>


## <a name="chapter-3---import-the-unity-package"></a><span data-ttu-id="c8471-244">Chapitre 3 - importer le package Unity</span><span class="sxs-lookup"><span data-stu-id="c8471-244">Chapter 3 - Import the Unity package</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8471-245">Si vous souhaitez ignorer le *Unity configurer* les composants de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [Azure-MR-309.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20309%20-%20Application%20insights/Azure-MR-309.unitypackage), importez-le dans votre projet en tant qu’un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html).</span><span class="sxs-lookup"><span data-stu-id="c8471-245">If you wish to skip the *Unity Set up* components of this course, and continue straight into code, feel free to download this [Azure-MR-309.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20309%20-%20Application%20insights/Azure-MR-309.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html).</span></span> <span data-ttu-id="c8471-246">Il contient également les DLL dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="c8471-246">This will also contain the DLLs from the next Chapter.</span></span> <span data-ttu-id="c8471-247">Après l’importation, continuer à partir de [ **chapitre 6**](#chapter-6---create-the-applicationinsightstracker-class).</span><span class="sxs-lookup"><span data-stu-id="c8471-247">After import, continue from [**Chapter 6**](#chapter-6---create-the-applicationinsightstracker-class).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8471-248">Pour utiliser Application Insights dans Unity, vous devez importer la DLL, ainsi que la DLL Newtonsoft.</span><span class="sxs-lookup"><span data-stu-id="c8471-248">To use Application Insights within Unity, you need to import the DLL for it, along with the Newtonsoft DLL.</span></span> <span data-ttu-id="c8471-249">Il est actuellement un problème connu dans Unity qui nécessite des plug-ins à être reconfiguré après l’importation.</span><span class="sxs-lookup"><span data-stu-id="c8471-249">There is currently a known issue in Unity which requires plugins to be  reconfigured after import.</span></span> <span data-ttu-id="c8471-250">Ces étapes (4-7 de cette section) ne sera plus nécessaires une fois que le bogue a été résolu.</span><span class="sxs-lookup"><span data-stu-id="c8471-250">These steps (4 - 7 in this section) will no longer be required after the bug has been resolved.</span></span>

<span data-ttu-id="c8471-251">Pour importer l’Application Insights dans votre propre projet, assurez-vous que vous avez [téléchargé '.unitypackage', qui contient les plug-ins](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20309%20-%20Application%20insights/AppInsights_LabPlugins.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="c8471-251">To import Application Insights into your own project, make sure you have [downloaded the '.unitypackage', containing the plugins](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20309%20-%20Application%20insights/AppInsights_LabPlugins.unitypackage).</span></span> <span data-ttu-id="c8471-252">Ensuite, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c8471-252">Then, do the following:</span></span>

1.  <span data-ttu-id="c8471-253">Ajouter le **.unitypackage** à Unity à l’aide de la **actifs \> importer un Package \> Package personnalisé** option de menu.</span><span class="sxs-lookup"><span data-stu-id="c8471-253">Add the **.unitypackage** to Unity by using the **Assets \> Import Package \> Custom Package** menu option.</span></span>

2.  <span data-ttu-id="c8471-254">Dans le **importer un Package Unity** emballer qui apparaît, vérifiez tous les éléments sous (y compris) **plug-ins** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="c8471-254">In the **Import Unity Package** box that pops up, ensure everything under (and including) **Plugins** is selected.</span></span>

    ![Importer le package Unity](images/AzureLabs-Lab309-22.png)

3.  <span data-ttu-id="c8471-256">Cliquez sur le **importation** bouton permettant d’ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="c8471-256">Click the **Import** button, to add the items to your project.</span></span>

4.  <span data-ttu-id="c8471-257">Accédez à la **Insights** dossier sous **plug-ins** dans le projet afficher, puis sélectionnez les plug-ins suivants *uniquement*:</span><span class="sxs-lookup"><span data-stu-id="c8471-257">Go to the **Insights** folder under **Plugins** in the Project view and select the following plugins *only*:</span></span>

    -   <span data-ttu-id="c8471-258">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="c8471-258">Microsoft.ApplicationInsights</span></span>

    ![Importer le package Unity](images/AzureLabs-Lab309-23.png)

5.  <span data-ttu-id="c8471-260">Avec cette *plug-in* sélectionnée, vérifiez que **plateforme Any** est **unchecked**, puis assurez-vous que **WSAPlayer** est également  **unchecked**, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="c8471-260">With this *plugin* selected, ensure that **Any Platform** is **unchecked**, then ensure that **WSAPlayer** is also **unchecked**, then click **Apply**.</span></span> <span data-ttu-id="c8471-261">Cette opération est juste pour confirmer que les fichiers sont correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="c8471-261">Doing this is just to confirm that the files are configured correctly.</span></span>

    ![Importer le package Unity](images/AzureLabs-Lab309-24.png)

    > [!NOTE]
    > <span data-ttu-id="c8471-263">Marquer les plug-ins comme suit, les configure uniquement à être utilisé dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="c8471-263">Marking the plugins like this, configures them to only be used in the Unity Editor.</span></span> <span data-ttu-id="c8471-264">Il existe un autre ensemble de DLL dans le dossier WSA qui sera utilisée une fois que le projet est exporté à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="c8471-264">There are a different set of DLLs in the WSA folder which will be used after the project is exported from Unity.</span></span>

6.  <span data-ttu-id="c8471-265">Ensuite, vous devez ouvrir le **WSA** dossier, en respectant le **Insights** dossier.</span><span class="sxs-lookup"><span data-stu-id="c8471-265">Next, you need to open the **WSA** folder, within the **Insights** folder.</span></span> <span data-ttu-id="c8471-266">Vous verrez une copie du même fichier que vous venez de configurer.</span><span class="sxs-lookup"><span data-stu-id="c8471-266">You will see a copy of the same file you just configured.</span></span> <span data-ttu-id="c8471-267">Sélectionnez ce fichier et dans l’inspecteur, vérifiez que **plateforme Any** est **unchecked**, puis assurez-vous que **uniquement** **WSAPlayer** est **vérifiée**.</span><span class="sxs-lookup"><span data-stu-id="c8471-267">Select this file, and then in the inspector, ensure that **Any Platform** is **unchecked**, then ensure that **only** **WSAPlayer** is **checked**.</span></span> <span data-ttu-id="c8471-268">Cliquez sur **Apply** (Appliquer).</span><span class="sxs-lookup"><span data-stu-id="c8471-268">Click **Apply**.</span></span>

    ![Importer le package Unity](images/AzureLabs-Lab309-25.png)

7. <span data-ttu-id="c8471-270">Vous devrez désormais suivre **les étapes 4 à 6**, mais pour le *Newtonsoft* plug-ins à la place.</span><span class="sxs-lookup"><span data-stu-id="c8471-270">You will now need to follow **steps 4-6**, but for the *Newtonsoft* plugins instead.</span></span> <span data-ttu-id="c8471-271">Consultez la capture d’écran de ce que le résultat doit se présenter comme ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c8471-271">See the below screenshot for what the outcome should look like.</span></span>

    ![Importer le package Unity](images/AzureLabs-Lab309-25-5.png)    

## <a name="chapter-4---set-up-the-camera-and-user-controls"></a><span data-ttu-id="c8471-273">Chapitre 4 - configurer des contrôles de l’appareil photo et l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="c8471-273">Chapter 4 - Set up the camera and user controls</span></span>

<span data-ttu-id="c8471-274">Dans ce chapitre, vous allez définir des contrôles et de l’appareil photo pour autoriser l’utilisateur de voir et déplacer dans la scène.</span><span class="sxs-lookup"><span data-stu-id="c8471-274">In this Chapter you will set up the camera and the controls to allow the user to see and move in the scene.</span></span>

1.  <span data-ttu-id="c8471-275">Avec le bouton droit dans une zone vide dans le volet de la hiérarchie, puis sur **créer** > **vide**.</span><span class="sxs-lookup"><span data-stu-id="c8471-275">Right-click in an empty area in the Hierarchy Panel, then on **Create** > **Empty**.</span></span>

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-26.png)

2.  <span data-ttu-id="c8471-277">Renommez le nouveau GameObject vide à **Parent de l’appareil photo**.</span><span class="sxs-lookup"><span data-stu-id="c8471-277">Rename the new empty GameObject to **Camera Parent**.</span></span>

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-27.png)

3.  <span data-ttu-id="c8471-279">Avec le bouton droit dans une zone vide dans le volet de la hiérarchie, puis sur **objet 3D**, puis sur **sphère**.</span><span class="sxs-lookup"><span data-stu-id="c8471-279">Right-click in an empty area in the Hierarchy Panel, then on **3D Object**, then on **Sphere**.</span></span>

4.  <span data-ttu-id="c8471-280">Renommer la sphère à **droite**.</span><span class="sxs-lookup"><span data-stu-id="c8471-280">Rename the Sphere to **Right Hand**.</span></span>

5.  <span data-ttu-id="c8471-281">Définir le **transformer échelle** de la main droite pour **0.1, 0.1, 0.1**</span><span class="sxs-lookup"><span data-stu-id="c8471-281">Set the **Transform Scale** of the Right Hand to **0.1, 0.1, 0.1**</span></span>

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-28.png)

6.  <span data-ttu-id="c8471-283">Supprimer le **sphère Collider** composant à partir de la droite en cliquant sur le **ENGRENAGE** dans le *sphère Collider* composant, puis **supprimer un composant** .</span><span class="sxs-lookup"><span data-stu-id="c8471-283">Remove the **Sphere Collider** component from the Right Hand by clicking on the **Gear** in the *Sphere Collider* component, and then **Remove Component**.</span></span>

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-29.png)

7.  <span data-ttu-id="c8471-285">Dans l’opération de glisser du Panneau de la hiérarchie le **Main Camera** et **droite** objets sur le **Parent de l’appareil photo** objet.</span><span class="sxs-lookup"><span data-stu-id="c8471-285">In the Hierarchy Panel drag the **Main Camera** and the **Right Hand** objects onto the **Camera Parent** object.</span></span>

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-30.png)

8.  <span data-ttu-id="c8471-287">Définir le **Position transformer** des deux le **Main Camera** et le **droite** objet **0, 0, 0**.</span><span class="sxs-lookup"><span data-stu-id="c8471-287">Set the **Transform Position** of both the **Main Camera** and the **Right Hand** object to **0, 0, 0**.</span></span>

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-31.png)

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-32.png)

## <a name="chapter-5---set-up-the-objects-in-the-unity-scene"></a><span data-ttu-id="c8471-290">Chapitre 5 - configurer les objets dans la scène Unity</span><span class="sxs-lookup"><span data-stu-id="c8471-290">Chapter 5 - Set up the objects in the Unity scene</span></span>

<span data-ttu-id="c8471-291">Vous allez maintenant créer certaines formes de base pour votre scène, avec lesquels l’utilisateur peut interagir.</span><span class="sxs-lookup"><span data-stu-id="c8471-291">You will now create some basic shapes for your scene, with which the user can interact.</span></span>

1.  <span data-ttu-id="c8471-292">Avec le bouton droit dans une zone vide dans le *hiérarchie panneau*, puis sur **objet 3D**, puis sélectionnez **plan**.</span><span class="sxs-lookup"><span data-stu-id="c8471-292">Right-click in an empty area in the *Hierarchy Panel*, then on **3D Object**, then select **Plane**.</span></span>

2.  <span data-ttu-id="c8471-293">Définir le plan de **transformer Position** à **0, -1, 0**.</span><span class="sxs-lookup"><span data-stu-id="c8471-293">Set the Plane **Transform Position** to **0, -1, 0**.</span></span>

3.  <span data-ttu-id="c8471-294">Définir le plan de **transformer échelle** à **5, 1, 5**.</span><span class="sxs-lookup"><span data-stu-id="c8471-294">Set the Plane **Transform Scale** to **5, 1, 5**.</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-33.png)

4.  <span data-ttu-id="c8471-296">Créer un matériau de base à utiliser avec votre **plan** de l’objet, afin que les autres formes sont plus faciles à voir.</span><span class="sxs-lookup"><span data-stu-id="c8471-296">Create a basic material to use with your **Plane** object, so that the other shapes are easier to see.</span></span> <span data-ttu-id="c8471-297">Accédez à votre *panneau projet*, avec le bouton droit, puis **créer**, suivie **dossier**, pour créer un nouveau dossier.</span><span class="sxs-lookup"><span data-stu-id="c8471-297">Navigate to your *Project Panel*, right-click, then **Create**, followed by **Folder**, to create a new folder.</span></span> <span data-ttu-id="c8471-298">Nommez-le **matériaux**.</span><span class="sxs-lookup"><span data-stu-id="c8471-298">Name it **Materials**.</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-34.png) ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-35.png)

5.  <span data-ttu-id="c8471-301">Ouvrez le **matériaux** dossier, puis avec le bouton droit, cliquez **créer**, puis **matériau**, pour créer un nouveau matériau.</span><span class="sxs-lookup"><span data-stu-id="c8471-301">Open the **Materials** folder, then right-click, click **Create**, then **Material**, to create a new material.</span></span> <span data-ttu-id="c8471-302">Nommez-le **bleu**.</span><span class="sxs-lookup"><span data-stu-id="c8471-302">Name it **Blue**.</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-36.png) ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-37.png)

6.  <span data-ttu-id="c8471-305">Avec la nouvelle **bleu** matériel sélectionné, recherchez à le *inspecteur*, puis cliquez sur la fenêtre rectangulaire en même temps que **Albedo**.</span><span class="sxs-lookup"><span data-stu-id="c8471-305">With the new **Blue** material selected, look at the *Inspector*, and click the rectangular window alongside **Albedo**.</span></span> <span data-ttu-id="c8471-306">Sélectionnez une couleur bleu (l’une image ci-dessous est **couleur hexadécimale : \#3592FFFF**).</span><span class="sxs-lookup"><span data-stu-id="c8471-306">Select a blue color (the one picture below is **Hex Color: \#3592FFFF**).</span></span> <span data-ttu-id="c8471-307">Une fois que vous avez choisi, cliquez sur le bouton Fermer.</span><span class="sxs-lookup"><span data-stu-id="c8471-307">Click the close button once you have chosen.</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-38.png)

7.  <span data-ttu-id="c8471-309">Faites glisser votre nouveau matériel à partir de la **matériaux** dossier, sur votre nouvellement créé **plan**, au sein de votre scène (ou déposez-le sur le **plan** au sein de l’objet le  *Hiérarchie*).</span><span class="sxs-lookup"><span data-stu-id="c8471-309">Drag your new material from the **Materials** folder, onto your newly created **Plane**, within your scene (or drop it on the **Plane** object within the *Hierarchy*).</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-39.png)

8.  <span data-ttu-id="c8471-311">Avec le bouton droit dans une zone vide dans le *hiérarchie panneau*, puis sur **objet 3D, Capsule**.</span><span class="sxs-lookup"><span data-stu-id="c8471-311">Right-click in an empty area in the *Hierarchy Panel*, then on **3D Object, Capsule**.</span></span>

    -  <span data-ttu-id="c8471-312">Avec le **Capsule** sélectionné, affectez son **transformer** *Position* à : **-10, 1, 0**.</span><span class="sxs-lookup"><span data-stu-id="c8471-312">With the **Capsule** selected, change its **Transform** *Position* to: **-10, 1, 0**.</span></span>

9.  <span data-ttu-id="c8471-313">Avec le bouton droit dans une zone vide dans le *hiérarchie panneau*, puis sur **objet 3D, Cube**.</span><span class="sxs-lookup"><span data-stu-id="c8471-313">Right-click in an empty area in the *Hierarchy Panel*, then on **3D Object, Cube**.</span></span>

    -  <span data-ttu-id="c8471-314">Avec le **Cube** sélectionné, affectez son **transformer** *Position* à : **0, 0, 10**.</span><span class="sxs-lookup"><span data-stu-id="c8471-314">With the **Cube** selected, change its **Transform** *Position* to: **0, 0, 10**.</span></span>

10. <span data-ttu-id="c8471-315">Avec le bouton droit dans une zone vide dans le *hiérarchie panneau*, puis sur **objet 3D, de la sphère**.</span><span class="sxs-lookup"><span data-stu-id="c8471-315">Right-click in an empty area in the *Hierarchy Panel*, then on **3D Object, Sphere**.</span></span>

    -  <span data-ttu-id="c8471-316">Avec le **sphère** sélectionné, affectez son **transformer** *Position* à : **10, 0, 0**.</span><span class="sxs-lookup"><span data-stu-id="c8471-316">With the **Sphere** selected, change its **Transform** *Position* to: **10, 0, 0**.</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-40.png)

    > [!NOTE]
    > <span data-ttu-id="c8471-318">Ces *Position* sont des valeurs *suggestions*.</span><span class="sxs-lookup"><span data-stu-id="c8471-318">These *Position* values are *suggestions*.</span></span> <span data-ttu-id="c8471-319">Vous êtes libre de définir les positions des objets à ce que vous souhaitez que, bien qu’il soit plus facile pour l’utilisateur de l’application si les distances des objets ne sont pas trop loin de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="c8471-319">You are free to set the positions of the objects to whatever you would like, though it is easier for the user of the application if the objects distances are not too far from the camera.</span></span>

11. <span data-ttu-id="c8471-320">Lorsque votre application s’exécute, il doit être en mesure d’identifier les objets au sein de la scène, pour y parvenir, elles doivent être marqués.</span><span class="sxs-lookup"><span data-stu-id="c8471-320">When your application is running, it needs to be able to identify the objects within the scene, to achieve this, they need to be tagged.</span></span> <span data-ttu-id="c8471-321">Sélectionnez un des objets et dans le *inspecteur* du panneau, cliquez sur **ajouter une balise...** , qui vous remplacerez la *inspecteur* avec la **balises & couches** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="c8471-321">Select one of the objects, and in the *Inspector* panel, click **Add Tag...**, which will swap the *Inspector* with the **Tags & Layers** panel.</span></span>

    <span data-ttu-id="c8471-322">![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-41.png) ![](images/AzureLabs-Lab309-42.png)</span><span class="sxs-lookup"><span data-stu-id="c8471-322">![Set up the objects in the Unity Scene](images/AzureLabs-Lab309-41.png) ![](images/AzureLabs-Lab309-42.png)</span></span>

12. <span data-ttu-id="c8471-323">Cliquez sur le **+ (plus)** de symboles, puis tapez le nom de balise en tant que **ObjectInScene**.</span><span class="sxs-lookup"><span data-stu-id="c8471-323">Click the **+ (plus)** symbol, then type the tag name as **ObjectInScene**.</span></span>

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-43.png)

    > [!WARNING]
    > <span data-ttu-id="c8471-325">Si vous utilisez un autre nom pour votre étiquette, vous devez vous assurer que cette modification est également effectuée le *DataFromAnalytics*, *ObjectTrigger*, et *les regards*, scripts plus tard, afin que votre les objets sont trouvés et détectés, au sein de votre scène.</span><span class="sxs-lookup"><span data-stu-id="c8471-325">If you use a different name for your tag, you will need to ensure this change is also made the *DataFromAnalytics*, *ObjectTrigger*, and *Gaze*, scripts later, so that your objects are found, and detected, within your scene.</span></span>

13. <span data-ttu-id="c8471-326">Avec la balise est créée, il vous faut maintenant s’appliquent aux trois de vos objets.</span><span class="sxs-lookup"><span data-stu-id="c8471-326">With the tag created, you now need to apply it to all three of your objects.</span></span> <span data-ttu-id="c8471-327">À partir de la *hiérarchie*, maintenez la **MAJ** de clé, puis cliquez sur le **Capsule**, **Cube**, et **sphère**, objets, puis, dans le *inspecteur*, cliquez sur le menu déroulant en même temps que **balise**, puis cliquez sur le *ObjectInScene* balise que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="c8471-327">From the *Hierarchy*, hold the **Shift** key, then click the **Capsule**, **Cube**, and **Sphere**, objects, then in the *Inspector*, click the dropdown menu alongside **Tag**, then click the *ObjectInScene* tag you created.</span></span>

    <span data-ttu-id="c8471-328">![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-44.png) ![](images/AzureLabs-Lab309-45.png)</span><span class="sxs-lookup"><span data-stu-id="c8471-328">![Set up the objects in the Unity Scene](images/AzureLabs-Lab309-44.png) ![](images/AzureLabs-Lab309-45.png)</span></span>

## <a name="chapter-6---create-the-applicationinsightstracker-class"></a><span data-ttu-id="c8471-329">Chapitre 6 : créer la classe ApplicationInsightsTracker</span><span class="sxs-lookup"><span data-stu-id="c8471-329">Chapter 6 - Create the ApplicationInsightsTracker class</span></span>

<span data-ttu-id="c8471-330">Le premier script que vous créez est **ApplicationInsightsTracker**, qui est chargé de :</span><span class="sxs-lookup"><span data-stu-id="c8471-330">The first script you need to create is **ApplicationInsightsTracker**, which is responsible for:</span></span>

1.  <span data-ttu-id="c8471-331">Création d’événements en fonction des interactions de l’utilisateur à envoyer à Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c8471-331">Creating events based on user interactions to submit to Azure Application Insights.</span></span>

2. <span data-ttu-id="c8471-332">Création des noms d’événements appropriés, en fonction de l’interaction de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c8471-332">Creating appropriate Event names, depending on user interaction.</span></span>

3. <span data-ttu-id="c8471-333">Envoi des événements à l’instance de Service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c8471-333">Submitting events to the Application Insights Service instance.</span></span>

<span data-ttu-id="c8471-334">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="c8471-334">To create this class:</span></span>

1.  <span data-ttu-id="c8471-335">Avec le bouton droit dans le *Panneau de configuration de projet*, puis **créer** > **dossier**.</span><span class="sxs-lookup"><span data-stu-id="c8471-335">Right-click in the *Project Panel*, then **Create** > **Folder**.</span></span> <span data-ttu-id="c8471-336">Nommez le dossier **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="c8471-336">Name the folder **Scripts**.</span></span>

    ![Créer la classe ApplicationInsightsTracker](images/AzureLabs-Lab309-46.png)  ![Créer la classe ApplicationInsightsTracker](images/AzureLabs-Lab309-47.png)

2.  <span data-ttu-id="c8471-339">Avec le **Scripts** dossier créé, double-cliquez dessus pour ouvrir.</span><span class="sxs-lookup"><span data-stu-id="c8471-339">With the **Scripts** folder created, double-click it, to open.</span></span> <span data-ttu-id="c8471-340">Ensuite, dans ce dossier, avec le bouton droit, **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="c8471-340">Then, within that folder, right-click, **Create** > **C# Script**.</span></span> <span data-ttu-id="c8471-341">Nommez le script **ApplicationInsightsTracker**.</span><span class="sxs-lookup"><span data-stu-id="c8471-341">Name the script **ApplicationInsightsTracker**.</span></span>

3.  <span data-ttu-id="c8471-342">Double-cliquez sur le nouveau **ApplicationInsightsTracker** script pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c8471-342">Double-click on the new **ApplicationInsightsTracker** script to open it with **Visual Studio**.</span></span>

4.  <span data-ttu-id="c8471-343">Mettre à jour les espaces de noms en haut du script afin d’être comme suit :</span><span class="sxs-lookup"><span data-stu-id="c8471-343">Update namespaces at the top of the script to be as below:</span></span>

    ```csharp
        using Microsoft.ApplicationInsights;
        using Microsoft.ApplicationInsights.DataContracts;
        using Microsoft.ApplicationInsights.Extensibility;
        using UnityEngine;
    ```

5.  <span data-ttu-id="c8471-344">À l’intérieur de la classe, insérez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8471-344">Inside the class insert the following variables:</span></span>

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
    > <span data-ttu-id="c8471-345">Définir le **instrumentationKey, applicationId et API_Key** des valeurs de manière appropriée, en utilisant le *Service clés* à partir du portail Azure, comme indiqué dans [chapitre 1](#chapter-1---the-azure-portal), étape 9 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="c8471-345">Set the **instrumentationKey, applicationId and API_Key** values appropriately, using the *Service Keys* from the Azure Portal as mentioned in [Chapter 1](#chapter-1---the-azure-portal), step 9 onwards.</span></span>

6.  <span data-ttu-id="c8471-346">Ajoutez ensuite le **Start()** et **Awake()** méthodes, qui seront appelées lors de l’initialisation de la classe :</span><span class="sxs-lookup"><span data-stu-id="c8471-346">Then add the **Start()** and **Awake()** methods, which will be called when the class initializes:</span></span>

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

7.  <span data-ttu-id="c8471-347">Ajoutez les méthodes chargés d’envoyer les événements et les métriques inscrit par votre application :</span><span class="sxs-lookup"><span data-stu-id="c8471-347">Add the methods responsible for sending the events and metrics registered by your application:</span></span>

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

8.  <span data-ttu-id="c8471-348">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="c8471-348">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-7---create-the-gaze-script"></a><span data-ttu-id="c8471-349">Chapitre 7 - créer le script du pointage de regard</span><span class="sxs-lookup"><span data-stu-id="c8471-349">Chapter 7 - Create the Gaze script</span></span>

<span data-ttu-id="c8471-350">Le script suivant pour créer le **les regards** script.</span><span class="sxs-lookup"><span data-stu-id="c8471-350">The next script to create is the **Gaze** script.</span></span> <span data-ttu-id="c8471-351">Ce script est chargé de créer un *Raycast* qui est projeté vers l’avant à partir de la *Main Camera*, pour détecter quel objet consulte l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c8471-351">This script is responsible for creating a *Raycast* that will be projected forward from the *Main Camera*, to detect which object the user is looking at.</span></span> <span data-ttu-id="c8471-352">Dans ce cas, le *Raycast* devra identifier si l’utilisateur consulte un objet avec le **ObjectInScene** balise, puis compter combien de temps l’utilisateur *son* à cet objet.</span><span class="sxs-lookup"><span data-stu-id="c8471-352">In this case, the *Raycast* will need to identify if the user is looking at an object with the **ObjectInScene** tag, and then count how long the user *gazes* at that object.</span></span>

1.  <span data-ttu-id="c8471-353">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="c8471-353">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="c8471-354">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="c8471-354">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="c8471-355">Nommez le script **les regards**.</span><span class="sxs-lookup"><span data-stu-id="c8471-355">Name the script **Gaze**.</span></span>

3.  <span data-ttu-id="c8471-356">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c8471-356">Double-click on the script to open it with Visual Studio.</span></span>

4.  <span data-ttu-id="c8471-357">Remplacez le code existant par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="c8471-357">Replace the existing code with the following:</span></span>

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

5.  <span data-ttu-id="c8471-358">Code pour le **Awake()** et **Start()** méthodes doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="c8471-358">Code for the **Awake()** and **Start()** methods now needs to be added.</span></span>

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

6.  <span data-ttu-id="c8471-359">À l’intérieur de la **les regards** de classe, ajoutez le code suivant dans le **Update()** méthode au projet un *Raycast* et détecter la baisse de la cible :</span><span class="sxs-lookup"><span data-stu-id="c8471-359">Inside the **Gaze** class, add the following code in the **Update()** method to project a *Raycast* and detect the target hit:</span></span>

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

7.  <span data-ttu-id="c8471-360">Ajouter le **ResetFocusedObject()** (méthode), pour envoyer des données à **Application Insights** lorsque l’utilisateur a examiné un objet.</span><span class="sxs-lookup"><span data-stu-id="c8471-360">Add the **ResetFocusedObject()** method, to send data to **Application Insights** when the user has looked at an object.</span></span>

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

8.  <span data-ttu-id="c8471-361">Vous avez maintenant terminé la **les regards** script.</span><span class="sxs-lookup"><span data-stu-id="c8471-361">You have now completed the **Gaze** script.</span></span> <span data-ttu-id="c8471-362">Enregistrez vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="c8471-362">Save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-8---create-the-objecttrigger-class"></a><span data-ttu-id="c8471-363">Chapitre 8 - créer la classe ObjectTrigger</span><span class="sxs-lookup"><span data-stu-id="c8471-363">Chapter 8 - Create the ObjectTrigger class</span></span>

<span data-ttu-id="c8471-364">Le script suivant, vous devez créer est **ObjectTrigger**, qui est chargé de :</span><span class="sxs-lookup"><span data-stu-id="c8471-364">The next script you need to create is **ObjectTrigger**, which is responsible for:</span></span>

- <span data-ttu-id="c8471-365">Ajout de composants nécessaires de collision à la caméra principale.</span><span class="sxs-lookup"><span data-stu-id="c8471-365">Adding components needed for collision to the Main Camera.</span></span>
- <span data-ttu-id="c8471-366">Détecter si l’appareil photo est près d’un objet marqué comme **ObjectInScene**.</span><span class="sxs-lookup"><span data-stu-id="c8471-366">Detecting if the camera is near an object tagged as **ObjectInScene**.</span></span>

<span data-ttu-id="c8471-367">Pour créer le script :</span><span class="sxs-lookup"><span data-stu-id="c8471-367">To create the script:</span></span>

1.  <span data-ttu-id="c8471-368">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="c8471-368">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="c8471-369">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="c8471-369">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="c8471-370">Nommez le script **ObjectTrigger**.</span><span class="sxs-lookup"><span data-stu-id="c8471-370">Name the script **ObjectTrigger**.</span></span>

3.  <span data-ttu-id="c8471-371">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c8471-371">Double-click on the script to open it with Visual Studio.</span></span> <span data-ttu-id="c8471-372">Remplacez le code existant par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="c8471-372">Replace the existing code with the following:</span></span>

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

4.  <span data-ttu-id="c8471-373">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="c8471-373">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-9---create-the-datafromanalytics-class"></a><span data-ttu-id="c8471-374">Chapitre 9 - créer la classe DataFromAnalytics</span><span class="sxs-lookup"><span data-stu-id="c8471-374">Chapter 9 - Create the DataFromAnalytics class</span></span>

<span data-ttu-id="c8471-375">Vous devez maintenant créer le **DataFromAnalytics** script, qui est chargé de :</span><span class="sxs-lookup"><span data-stu-id="c8471-375">You will now need to create the **DataFromAnalytics** script, which is responsible for:</span></span>

- <span data-ttu-id="c8471-376">Extraction des données d’analytique sur les objets a été approché par l’appareil photo le plus.</span><span class="sxs-lookup"><span data-stu-id="c8471-376">Fetching analytics data about which object has been approached by the camera the most.</span></span>
- <span data-ttu-id="c8471-377">À l’aide de la *clés du Service*, qui autorise la communication avec votre instance de Service Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c8471-377">Using the *Service Keys*, that allow communication with your Azure Application Insights Service instance.</span></span>
- <span data-ttu-id="c8471-378">Trier les objets dans la scène, selon ce qui a le nombre d’événements le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="c8471-378">Sorting the objects in scene, according to which has the highest event count.</span></span>
- <span data-ttu-id="c8471-379">Modification de la couleur du matériau, de l’objet plus approached, à *vert*.</span><span class="sxs-lookup"><span data-stu-id="c8471-379">Changing the material color, of the most approached object, to *green*.</span></span>

<span data-ttu-id="c8471-380">Pour créer le script :</span><span class="sxs-lookup"><span data-stu-id="c8471-380">To create the script:</span></span>

1.  <span data-ttu-id="c8471-381">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="c8471-381">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="c8471-382">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="c8471-382">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="c8471-383">Nommez le script **DataFromAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="c8471-383">Name the script **DataFromAnalytics**.</span></span>

3.  <span data-ttu-id="c8471-384">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c8471-384">Double-click on the script to open it with Visual Studio.</span></span>

4.  <span data-ttu-id="c8471-385">Insérer des espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="c8471-385">Insert the following namespaces:</span></span>

    ```csharp
        using Newtonsoft.Json;
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using System.Linq;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

5.  <span data-ttu-id="c8471-386">Dans le script, insérez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c8471-386">Inside the script, insert the following:</span></span>

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

6.  <span data-ttu-id="c8471-387">Dans le **DataFromAnalytics** class, juste après le **Start()** (méthode), ajoutez la méthode suivante nommée **FetchAnalytics()** .</span><span class="sxs-lookup"><span data-stu-id="c8471-387">Within the **DataFromAnalytics** class, right after the **Start()** method, add the following method called **FetchAnalytics()**.</span></span> <span data-ttu-id="c8471-388">Cette méthode est chargée de remplir la liste des paires clé / valeur, avec un *GameObject* et un numéro de nombre d’événement espace réservé.</span><span class="sxs-lookup"><span data-stu-id="c8471-388">This method is responsible for populating the list of key value pairs, with a *GameObject* and a placeholder event count number.</span></span> <span data-ttu-id="c8471-389">Il initialise ensuite les **GetWebRequest()** coroutine.</span><span class="sxs-lookup"><span data-stu-id="c8471-389">It then initializes the **GetWebRequest()** coroutine.</span></span> <span data-ttu-id="c8471-390">La structure de la requête de l’appel à *Application Insights* peut se trouver dans cette méthode, comme le *URL de la requête* point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="c8471-390">The query structure of the call to *Application Insights* can be found within this method also, as the *Query URL* endpoint.</span></span>

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

7.  <span data-ttu-id="c8471-391">Juste en dessous du **FetchAnalytics()** (méthode), ajoutez une méthode appelée **GetWebRequest()** , qui retourne un *IEnumerator*.</span><span class="sxs-lookup"><span data-stu-id="c8471-391">Right below the **FetchAnalytics()** method, add a method called **GetWebRequest()**, which returns an *IEnumerator*.</span></span> <span data-ttu-id="c8471-392">Cette méthode est chargée pour demander le nombre de fois où un événement, correspondant avec un spécifique *GameObject*, a été appelée au sein de *Application Insights*.</span><span class="sxs-lookup"><span data-stu-id="c8471-392">This method is responsible for requesting the number of times an event, corresponding with a specific *GameObject*, has been called within *Application Insights*.</span></span> <span data-ttu-id="c8471-393">Lorsque toutes les requêtes envoyées ont été retournés, le **DetermineWinner()** méthode est appelée.</span><span class="sxs-lookup"><span data-stu-id="c8471-393">When all the sent queries have returned, the **DetermineWinner()** method is called.</span></span>

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

8.  <span data-ttu-id="c8471-394">La méthode suivante est **DetermineWinner()** , qui trie la liste des *GameObject* et *Int* paires, selon le nombre d’événements le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="c8471-394">The next method is **DetermineWinner()**, which sorts the list of *GameObject* and *Int* pairs, according to the highest event count.</span></span> <span data-ttu-id="c8471-395">Il remplace ensuite la couleur du matériau de qui *GameObject* à *vert* (en tant que commentaires pour lui avoir le nombre le plus élevé).</span><span class="sxs-lookup"><span data-stu-id="c8471-395">It then changes the material color of that *GameObject* to *green* (as feedback for it having the highest count).</span></span> <span data-ttu-id="c8471-396">Cela affiche un message avec les résultats d’analytique.</span><span class="sxs-lookup"><span data-stu-id="c8471-396">This displays a message with the analytics results.</span></span>

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

9.  <span data-ttu-id="c8471-397">Ajouter la structure de classe qui sera utilisée pour désérialiser l’objet JSON, reçu de *Application Insights*.</span><span class="sxs-lookup"><span data-stu-id="c8471-397">Add the class structure which will be used to deserialize the JSON object, received from *Application Insights*.</span></span> <span data-ttu-id="c8471-398">Ajoutez ces classes tout en bas de votre **DataFromAnalytics** fichier de classe, **en dehors de** de la définition de classe.</span><span class="sxs-lookup"><span data-stu-id="c8471-398">Add these classes at the very bottom of your **DataFromAnalytics** class file, **outside** of the class definition.</span></span>

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

10. <span data-ttu-id="c8471-399">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="c8471-399">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-10---create-the-movement-class"></a><span data-ttu-id="c8471-400">Chapitre 10 - créer la classe de mouvement</span><span class="sxs-lookup"><span data-stu-id="c8471-400">Chapter 10 - Create the Movement class</span></span>

<span data-ttu-id="c8471-401">Le **mouvement** script est le prochain script, vous devez créer.</span><span class="sxs-lookup"><span data-stu-id="c8471-401">The **Movement** script is the next script you will need to create.</span></span> <span data-ttu-id="c8471-402">Il est chargé de :</span><span class="sxs-lookup"><span data-stu-id="c8471-402">It is responsible for:</span></span>

- <span data-ttu-id="c8471-403">Déplacement de la caméra principale en fonction de la direction de l’appareil photo recherche vers.</span><span class="sxs-lookup"><span data-stu-id="c8471-403">Moving the Main Camera according to the direction the camera is looking towards.</span></span>
- <span data-ttu-id="c8471-404">Ajout de tous les autres scripts aux objets de scène.</span><span class="sxs-lookup"><span data-stu-id="c8471-404">Adding all other scripts to scene objects.</span></span>

<span data-ttu-id="c8471-405">Pour créer le script :</span><span class="sxs-lookup"><span data-stu-id="c8471-405">To create the script:</span></span>

1.  <span data-ttu-id="c8471-406">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="c8471-406">Double-click on the **Scripts** folder, to open it.</span></span>

2.  <span data-ttu-id="c8471-407">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="c8471-407">Right-click inside the **Scripts** folder, click **Create** > **C# Script**.</span></span> <span data-ttu-id="c8471-408">Nommez le script **mouvement**.</span><span class="sxs-lookup"><span data-stu-id="c8471-408">Name the script **Movement**.</span></span>

3.  <span data-ttu-id="c8471-409">Double-cliquez sur le script pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="c8471-409">Double-click on the script to open it with *Visual Studio*.</span></span>

4.  <span data-ttu-id="c8471-410">Remplacez le code existant par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="c8471-410">Replace the existing code with the following:</span></span>

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

5.  <span data-ttu-id="c8471-411">Dans le **mouvement** (classe), *ci-dessous* vide **Update()** (méthode), insérer les méthodes suivantes permettant aux utilisateurs d’utiliser le contrôleur de main pour déplacer dans l’espace virtuel :</span><span class="sxs-lookup"><span data-stu-id="c8471-411">Within the **Movement** class, *below* the empty **Update()** method, insert the following methods that allow the user to use the hand controller to move in the virtual space:</span></span>

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

6.  <span data-ttu-id="c8471-412">Ajoutez enfin l’appel de méthode dans le **Update()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c8471-412">Lastly add the method call within the **Update()** method.</span></span>

    ```csharp
        // Update is called once per frame
        void Update()
        {
            UpdateControllerState();
        }
    ```

7.  <span data-ttu-id="c8471-413">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="c8471-413">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-11---setting-up-the-scripts-references"></a><span data-ttu-id="c8471-414">Chapitre 11 - configurer les références de scripts</span><span class="sxs-lookup"><span data-stu-id="c8471-414">Chapter 11 - Setting up the scripts references</span></span>

<span data-ttu-id="c8471-415">Dans ce chapitre, vous devez placer le **mouvement** de script sur le **Parent de l’appareil photo** et définissez ses cibles de référence.</span><span class="sxs-lookup"><span data-stu-id="c8471-415">In this Chapter you need to place the **Movement** script onto the **Camera Parent** and set its reference targets.</span></span> <span data-ttu-id="c8471-416">Ce script gère à placer les autres scripts où ils doivent être.</span><span class="sxs-lookup"><span data-stu-id="c8471-416">That script will then handle placing the other scripts where they need to be.</span></span>

1.  <span data-ttu-id="c8471-417">À partir de la **Scripts** dossier dans le *panneau projet*, faites glisser le **le déplacement des** un script pour le **Parent de l’appareil photo** objet, se trouvant dans le  *Panneau de la hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="c8471-417">From the **Scripts** folder in the *Project Panel*, drag the **Movement** script to the **Camera Parent** object, located in the *Hierarchy Panel*.</span></span>

    ![Configurer les références de scripts dans la scène Unity](images/AzureLabs-Lab309-48.png)

2.  <span data-ttu-id="c8471-419">Cliquez sur le **Parent de l’appareil photo**.</span><span class="sxs-lookup"><span data-stu-id="c8471-419">Click on the **Camera Parent**.</span></span> <span data-ttu-id="c8471-420">Dans le *hiérarchie panneau*, faites glisser le **droite** à partir de l’objet le *Panneau de la hiérarchie* à la cible de référence, **contrôleur**, dans le *Panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="c8471-420">In the *Hierarchy Panel*, drag the **Right Hand** object from the *Hierarchy Panel* to the reference target, **Controller**, in the *Inspector Panel*.</span></span> <span data-ttu-id="c8471-421">Définir le **utilisateur vitesse** à **5**, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c8471-421">Set the **User Speed** to **5**, as shown in the image below.</span></span>

    ![Configurer les références de scripts dans la scène Unity](images/AzureLabs-Lab309-49.png)

## <a name="chapter-12---build-the-unity-project"></a><span data-ttu-id="c8471-423">Chapitre 12 - générer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="c8471-423">Chapter 12 - Build the Unity project</span></span>

<span data-ttu-id="c8471-424">Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée, il est temps de générer à partir de Unity.</span><span class="sxs-lookup"><span data-stu-id="c8471-424">Everything needed for the Unity section of this project has now been completed, so it is time to build it from Unity.</span></span>

1.  <span data-ttu-id="c8471-425">Accédez à **les paramètres de génération**, (**fichier** > **paramètres de Build**).</span><span class="sxs-lookup"><span data-stu-id="c8471-425">Navigate to **Build Settings**, (**File** > **Build Settings**).</span></span>

2.  <span data-ttu-id="c8471-426">À partir de la **paramètres de Build** fenêtre, cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="c8471-426">From the **Build Settings** window, click **Build**.</span></span>

    ![Générez le projet Unity à UWP Solution](images/AzureLabs-Lab309-50.png)

3.  <span data-ttu-id="c8471-428">Un **Explorateur de fichiers** fenêtre va fenêtre contextuelle s’affiche, vous demandant de spécifier un emplacement pour la build.</span><span class="sxs-lookup"><span data-stu-id="c8471-428">A **File Explorer** window will pop-up, prompting you for a location for the build.</span></span> <span data-ttu-id="c8471-429">Créez un dossier (en cliquant sur **nouveau dossier** dans l’angle supérieur gauche) et nommez-le **génère**.</span><span class="sxs-lookup"><span data-stu-id="c8471-429">Create a new folder (by clicking **New Folder** in the top-left corner), and name it **BUILDS**.</span></span>

    ![Générez le projet Unity à UWP Solution](images/AzureLabs-Lab309-51.png)

    1.  <span data-ttu-id="c8471-431">Ouvrez le nouveau **génère** dossier et créez un autre dossier (à l’aide de **nouveau dossier** une fois de plus) et nommez-le **MR\_Azure\_Application\_ Insights**.</span><span class="sxs-lookup"><span data-stu-id="c8471-431">Open the new **BUILDS** folder, and create another folder (using **New Folder** once more), and name it **MR\_Azure\_Application\_Insights**.</span></span>

        ![Générez le projet Unity à UWP Solution](images/AzureLabs-Lab309-52.png)

    2.  <span data-ttu-id="c8471-433">Avec le **MR\_Azure\_Application\_Insights** dossier sélectionné, cliquez sur **sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="c8471-433">With the **MR\_Azure\_Application\_Insights** folder selected, click **Select Folder**.</span></span> <span data-ttu-id="c8471-434">Le projet prendra une minute ou donc en créer.</span><span class="sxs-lookup"><span data-stu-id="c8471-434">The project will take a minute or so to build.</span></span>

4.  <span data-ttu-id="c8471-435">Suivant *Build*, **Explorateur de fichiers** s’affiche vous indiquant l’emplacement de votre nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="c8471-435">Following *Build*, **File Explorer** will appear showing you the location of your new project.</span></span>

## <a name="chapter-13---deploy-mrazureapplicationinsights-app-to-your-machine"></a><span data-ttu-id="c8471-436">Chapitre 13 - déployer l’application de MR_Azure_Application_Insights sur votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="c8471-436">Chapter 13 - Deploy MR_Azure_Application_Insights app to your machine</span></span>

<span data-ttu-id="c8471-437">Pour déployer le **MR\_Azure\_Application\_Insights** application sur votre ordinateur Local :</span><span class="sxs-lookup"><span data-stu-id="c8471-437">To deploy the **MR\_Azure\_Application\_Insights** app on your Local Machine:</span></span>

1.  <span data-ttu-id="c8471-438">Ouvrez le fichier de solution de votre **MR\_Azure\_Application\_Insights** app dans **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c8471-438">Open the solution file of your **MR\_Azure\_Application\_Insights** app in **Visual Studio**.</span></span>

2.  <span data-ttu-id="c8471-439">Dans le **plateforme de Solution**, sélectionnez **x86, Local Machine**.</span><span class="sxs-lookup"><span data-stu-id="c8471-439">In the **Solution Platform**, select **x86, Local Machine**.</span></span>

3.  <span data-ttu-id="c8471-440">Dans le **Configuration de la Solution** sélectionnez **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="c8471-440">In the **Solution Configuration** select **Debug**.</span></span>

    ![Générez le projet Unity à UWP Solution](images/AzureLabs-Lab309-53.png)

4.  <span data-ttu-id="c8471-442">Accédez à **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c8471-442">Go to **Build menu** and click on **Deploy Solution** to sideload the application to your machine.</span></span>

5.  <span data-ttu-id="c8471-443">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancée.</span><span class="sxs-lookup"><span data-stu-id="c8471-443">Your app should now appear in the list of installed apps, ready to be launched.</span></span>

6. <span data-ttu-id="c8471-444">Lancez l’application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="c8471-444">Launch the mixed reality application.</span></span>

7. <span data-ttu-id="c8471-445">Déplacer la scène, l’approche des objets et en recherchant les, lorsque le *Azure Insight Service* a collecté suffisamment de données événement, il définit l’objet qui a été a élaboré le plus au vert.</span><span class="sxs-lookup"><span data-stu-id="c8471-445">Move around the scene, approaching objects and looking at them, when the *Azure Insight Service* has collected enough event data, it will set the object that has been approached the most to green.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="c8471-446">Alors que la durée d’attente moyenne pour le *événements et mesures* soit collecté par le Service prend environ 15 minutes, dans certains cas, il peut prendre jusqu'à 1 heure.</span><span class="sxs-lookup"><span data-stu-id="c8471-446">While the average waiting time for the *Events and Metrics* to be collected by the Service takes around 15 min, in some occasions it might take up to 1 hour.</span></span>

## <a name="chapter-14---the-application-insights-service-portal"></a><span data-ttu-id="c8471-447">Chapitre 14 - le portail de Service Application Insights</span><span class="sxs-lookup"><span data-stu-id="c8471-447">Chapter 14 - The Application Insights Service portal</span></span>

<span data-ttu-id="c8471-448">Une fois que vous avez itinérante autour de la scène et gazed à plusieurs objets, vous pouvez voir les données collectées dans le *Service Application Insights* portail.</span><span class="sxs-lookup"><span data-stu-id="c8471-448">Once you have roamed around the scene and gazed at several objects you can see the data collected in the *Application Insights Service* portal.</span></span>

1.  <span data-ttu-id="c8471-449">Revenez à votre portail Service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c8471-449">Go back to your Application Insights Service portal.</span></span>

2.  <span data-ttu-id="c8471-450">Cliquez sur *Metrics Explorer*.</span><span class="sxs-lookup"><span data-stu-id="c8471-450">Click on *Metrics Explorer*.</span></span>

    ![Examinez les données collectées](images/AzureLabs-Lab309-54.png)

3.  <span data-ttu-id="c8471-452">Il s’ouvre dans un onglet contenant le graphique qui représentent le *événements et mesures* relatives à votre application.</span><span class="sxs-lookup"><span data-stu-id="c8471-452">It will open in a tab containing the graph which represent the *Events and Metrics* related to your application.</span></span> <span data-ttu-id="c8471-453">Comme mentionné ci-dessus, il peut prendre un certain temps (jusqu'à 1 heure) pour les données à afficher dans le graphique</span><span class="sxs-lookup"><span data-stu-id="c8471-453">As mentioned above, it might take some time (up to 1 hour) for the data to be displayed in the graph</span></span>

    ![Examinez les données collectées](images/AzureLabs-Lab309-55.png)

4.  <span data-ttu-id="c8471-455">Cliquez sur le *barre d’événements* dans le *Total d’événements* par la Version de l’Application pour afficher une description détaillée des événements avec leurs noms.</span><span class="sxs-lookup"><span data-stu-id="c8471-455">Click on the *Events bar* in the *Total of Events* by Application Version, to see a detailed breakdown of the events with their names.</span></span>

    ![Examinez les données collectées](images/AzureLabs-Lab309-56.png)

## <a name="your-finished-your-application-insights-service-application"></a><span data-ttu-id="c8471-457">Votre terminé votre application de Service Application Insights</span><span class="sxs-lookup"><span data-stu-id="c8471-457">Your finished your Application Insights Service application</span></span>

<span data-ttu-id="c8471-458">Félicitations, vous avez créé une application de réalité mixte qui tire parti du Service Application Insights pour surveiller l’activité de l’utilisateur au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="c8471-458">Congratulations, you built a mixed reality app that leverages the Application Insights Service to monitor user's activity within your app.</span></span>

![résultat de cours](images/AzureLabs-Lab309-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="c8471-460">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="c8471-460">Bonus Exercises</span></span>

<span data-ttu-id="c8471-461">**Exercice 1**</span><span class="sxs-lookup"><span data-stu-id="c8471-461">**Exercise 1**</span></span>

<span data-ttu-id="c8471-462">Essayez de génération dynamique, plutôt que de création manuelle, les objets ObjectInScene et définir leurs coordonnées sur le plan dans vos scripts.</span><span class="sxs-lookup"><span data-stu-id="c8471-462">Try spawning, rather than manually creating, the ObjectInScene objects and set their coordinates on the plane within your scripts.</span></span> <span data-ttu-id="c8471-463">De cette façon, vous pouvez demander à Azure populaires l’objet a été (soit à partir des résultats du pointage de regard ou proximité) et générer un *supplémentaire* un de ces objets.</span><span class="sxs-lookup"><span data-stu-id="c8471-463">In this way, you could ask Azure what the most popular object was (either from gaze or proximity results) and spawn an *extra* one of those objects.</span></span>

<span data-ttu-id="c8471-464">**Exercice 2**</span><span class="sxs-lookup"><span data-stu-id="c8471-464">**Exercise 2**</span></span>

<span data-ttu-id="c8471-465">Trier les résultats de votre Application Insights en temps, afin que vous obtenez les données les plus pertinentes et implémentez les temps des données sensibles dans votre application.</span><span class="sxs-lookup"><span data-stu-id="c8471-465">Sort your Application Insights results by time, so that you get the most relevant data, and implement that time sensitive data in your application.</span></span>

