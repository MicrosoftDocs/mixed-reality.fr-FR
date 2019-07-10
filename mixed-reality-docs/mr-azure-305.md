---
title: MR et Azure 305 - fonctions et stockage
description: Terminer ce cours pour apprendre à implémenter le stockage Azure et des fonctions dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, fonctions, stockage, hololens, réalité virtuelle immersive,
ms.openlocfilehash: 5f3d0c6990249bc32e4c0f55c72dd884c4c2214e
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694557"
---
>[!NOTE]
><span data-ttu-id="1c53f-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="1c53f-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="1c53f-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="1c53f-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="1c53f-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="1c53f-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="1c53f-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1c53f-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="1c53f-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="1c53f-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="1c53f-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="1c53f-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br> 

# <a name="mr-and-azure-305-functions-and-storage"></a><span data-ttu-id="1c53f-110">MR et Azure 305 : Fonctions et stockage</span><span class="sxs-lookup"><span data-stu-id="1c53f-110">MR and Azure 305: Functions and storage</span></span>

![produit final-Démarrer](images/AzureLabs-Lab5-00.png)

<span data-ttu-id="1c53f-112">Dans ce cours, vous allez apprendre à créer et utiliser Azure Functions et stocker des données avec une ressource de stockage Azure, dans une application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="1c53f-112">In this course, you will learn how to create and use Azure Functions and store data with an Azure Storage resource, within a mixed reality application.</span></span>

<span data-ttu-id="1c53f-113">*Azure Functions* est un service Microsoft, ce qui permet aux développeurs d’exécuter de petits morceaux de code, « fonctions », dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-113">*Azure Functions* is a Microsoft service, which allows developers to run small pieces of code, 'functions', in Azure.</span></span> <span data-ttu-id="1c53f-114">Cela fournit un moyen permettant de déléguer le cloud, plutôt que votre application locale, ce qui peut avoir de nombreux avantages.</span><span class="sxs-lookup"><span data-stu-id="1c53f-114">This provides a way to delegate work to the cloud, rather than your local application, which can have many benefits.</span></span> <span data-ttu-id="1c53f-115">*Azure Functions* prend en charge plusieurs langages de développement, y compris C\#, F\#, Node.js, Java et PHP.</span><span class="sxs-lookup"><span data-stu-id="1c53f-115">*Azure Functions* supports several development languages, including C\#, F\#, Node.js, Java, and PHP.</span></span> <span data-ttu-id="1c53f-116">Pour plus d’informations, visitez le [article d’Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span><span class="sxs-lookup"><span data-stu-id="1c53f-116">For more information, visit the [Azure Functions article](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span></span>

<span data-ttu-id="1c53f-117">*Stockage Azure* est un service de cloud Microsoft, ce qui permet aux développeurs de stocker des données, avec l’assurance qu’il sera hautement disponible, sécurisé, durable, évolutif et redondant.</span><span class="sxs-lookup"><span data-stu-id="1c53f-117">*Azure Storage* is a Microsoft cloud service, which allows developers to store data, with the insurance that it will be highly available, secure, durable, scalable, and redundant.</span></span> <span data-ttu-id="1c53f-118">Cela signifie que Microsoft gère toutes les maintenance et les problèmes critiques pour vous.</span><span class="sxs-lookup"><span data-stu-id="1c53f-118">This means Microsoft will handle all maintenance, and critical problems for you.</span></span> <span data-ttu-id="1c53f-119">Pour plus d’informations, visitez le [l’article Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="1c53f-119">For more information, visit the [Azure Storage article](https://docs.microsoft.com/azure/storage/common/storage-introduction).</span></span>

<span data-ttu-id="1c53f-120">Avoir terminé ce cours, vous disposez d’une application de casque immersives de réalité mixte qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1c53f-120">Having completed this course, you will have a mixed reality immersive headset application which will be able to do the following:</span></span>

1.  <span data-ttu-id="1c53f-121">Autoriser l’utilisateur à les regards autour d’une scène.</span><span class="sxs-lookup"><span data-stu-id="1c53f-121">Allow the user to gaze around a scene.</span></span>
2.  <span data-ttu-id="1c53f-122">Déclencher la génération dynamique des objets lors de son de l’utilisateur à une 3D « button ».</span><span class="sxs-lookup"><span data-stu-id="1c53f-122">Trigger the spawning of objects when the user gazes at a 3D 'button'.</span></span>
3.  <span data-ttu-id="1c53f-123">Les objets générées seront sélectionnées par une fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-123">The spawned objects will be chosen by an Azure Function.</span></span>
4.  <span data-ttu-id="1c53f-124">Comme chaque objet est généré, l’application stocke le type d’objet dans un *fichiers Azure*, situé dans *stockage Azure*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-124">As each object is spawned, the application will store the object type in an *Azure File*, located in *Azure Storage*.</span></span>
5.  <span data-ttu-id="1c53f-125">Lors du chargement d’une deuxième fois, le *fichiers Azure* données sont récupérées et permet de relire les actions de génération à partir de l’instance précédente de l’application.</span><span class="sxs-lookup"><span data-stu-id="1c53f-125">Upon loading a second time, the *Azure File* data will be retrieved, and used to replay the spawning actions from the previous instance of the application.</span></span>

<span data-ttu-id="1c53f-126">Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception.</span><span class="sxs-lookup"><span data-stu-id="1c53f-126">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="1c53f-127">Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="1c53f-127">This course is designed to teach you how to integrate an Azure Service with your Unity Project.</span></span> <span data-ttu-id="1c53f-128">Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre Application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="1c53f-128">It is your job to use the knowledge you gain from this course to enhance your mixed reality Application.</span></span>

## <a name="device-support"></a><span data-ttu-id="1c53f-129">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="1c53f-129">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="1c53f-130">Cours</span><span class="sxs-lookup"><span data-stu-id="1c53f-130">Course</span></span></th><th style="width:150px"> <span data-ttu-id="1c53f-131"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="1c53f-131"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="1c53f-132"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="1c53f-132"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="1c53f-133">MR et Azure 305 : Fonctions et stockage</span><span class="sxs-lookup"><span data-stu-id="1c53f-133">MR and Azure 305: Functions and storage</span></span></td><td style="text-align: center;"> <span data-ttu-id="1c53f-134">✔️</span><span class="sxs-lookup"><span data-stu-id="1c53f-134">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="1c53f-135">✔️</span><span class="sxs-lookup"><span data-stu-id="1c53f-135">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="1c53f-136">Si ce cours se concentre principalement sur des casques Windows Mixed Reality IMMERSIFS (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours pour Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="1c53f-136">While this course primarily focuses on Windows Mixed Reality immersive (VR) headsets, you can also apply what you learn in this course to Microsoft HoloLens.</span></span> <span data-ttu-id="1c53f-137">Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="1c53f-137">As you follow along with the course, you will see notes on any changes you might need to employ to support HoloLens.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c53f-138">Prérequis</span><span class="sxs-lookup"><span data-stu-id="1c53f-138">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="1c53f-139">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="1c53f-139">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="1c53f-140">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="1c53f-140">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="1c53f-141">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous .</span><span class="sxs-lookup"><span data-stu-id="1c53f-141">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="1c53f-142">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="1c53f-142">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="1c53f-143">Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)</span><span class="sxs-lookup"><span data-stu-id="1c53f-143">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="1c53f-144">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="1c53f-144">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="1c53f-145">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="1c53f-145">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="1c53f-146">Unity 2017.4</span><span class="sxs-lookup"><span data-stu-id="1c53f-146">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="1c53f-147">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1c53f-147">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="1c53f-148">Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="1c53f-148">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="1c53f-149">Un abonnement à un compte Azure pour la création de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="1c53f-149">A subscription to an Azure account for creating Azure resources</span></span>
- <span data-ttu-id="1c53f-150">Accès à Internet pour la récupération de données et le programme d’installation Azure</span><span class="sxs-lookup"><span data-stu-id="1c53f-150">Internet access for Azure setup and data retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="1c53f-151">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="1c53f-151">Before you start</span></span>

<span data-ttu-id="1c53f-152">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="1c53f-152">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>

## <a name="chapter-1---the-azure-portal"></a><span data-ttu-id="1c53f-153">Chapitre 1 : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1c53f-153">Chapter 1 - The Azure Portal</span></span>

<span data-ttu-id="1c53f-154">Pour utiliser le **Service de stockage Azure**, vous devez créer et configurer un **compte de stockage** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-154">To use the **Azure Storage Service**, you will need to create and configure a **Storage Account** in the Azure portal.</span></span>

1.  <span data-ttu-id="1c53f-155">Connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c53f-155">Log in to the  [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE]
    > <span data-ttu-id="1c53f-156">Si vous n’avez pas déjà un compte Azure, vous devrez créer un.</span><span class="sxs-lookup"><span data-stu-id="1c53f-156">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="1c53f-157">Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="1c53f-157">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="1c53f-158">Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez *compte de stockage*, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-158">Once you are logged in, click on **New** in the top left corner, and search for *Storage account*, and click **Enter**.</span></span>

    ![recherche de stockage Azure](images/AzureLabs-Lab5-01.png)

    > [!NOTE]
    > <span data-ttu-id="1c53f-160">Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.</span><span class="sxs-lookup"><span data-stu-id="1c53f-160">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

3.  <span data-ttu-id="1c53f-161">La nouvelle page doit fournir une description de la *compte de stockage Azure* service.</span><span class="sxs-lookup"><span data-stu-id="1c53f-161">The new page will provide a description of the *Azure Storage account* service.</span></span> <span data-ttu-id="1c53f-162">En bas à gauche de cette invite, sélectionnez le **créer** bouton permettant de créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="1c53f-162">At the bottom left of this prompt, select the **Create** button, to create an association with this service.</span></span>

    ![créer le service](images/AzureLabs-Lab5-02.png)

4.  <span data-ttu-id="1c53f-164">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="1c53f-164">Once you have clicked on **Create**:</span></span>

    1.  <span data-ttu-id="1c53f-165">Insérer un *nom* pour votre compte, n’oubliez pas ce champ accepte uniquement des lettres minuscules et chiffres.</span><span class="sxs-lookup"><span data-stu-id="1c53f-165">Insert a *Name* for your account, be aware this field only accepts numbers, and lowercase letters.</span></span>

    2.  <span data-ttu-id="1c53f-166">Pour *modèle de déploiement*, sélectionnez **Resource manager**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-166">For *Deployment model*, select **Resource manager**.</span></span>

    3.  <span data-ttu-id="1c53f-167">Pour *type de compte*, sélectionnez **stockage (usage général v1)** .</span><span class="sxs-lookup"><span data-stu-id="1c53f-167">For *Account kind*, select **Storage (general purpose v1)**.</span></span>

    4.  <span data-ttu-id="1c53f-168">Déterminer le *emplacement* pour votre groupe de ressources (si vous créez un nouveau groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="1c53f-168">Determine the *Location* for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="1c53f-169">Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="1c53f-169">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="1c53f-170">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="1c53f-170">Some Azure assets are only available in certain regions.</span></span>

    5.  <span data-ttu-id="1c53f-171">Pour *réplication* sélectionnez **en lecture-access-geo-redundant storage (RA-GRS)** .</span><span class="sxs-lookup"><span data-stu-id="1c53f-171">For *Replication* select **Read-access-geo-redundant storage (RA-GRS)**.</span></span>

    6.  <span data-ttu-id="1c53f-172">Pour *performances*, sélectionnez **Standard**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-172">For *Performance*, select **Standard**.</span></span>

    7.  <span data-ttu-id="1c53f-173">Laissez *transfert sécurisé requis* comme **désactivé**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-173">Leave *Secure transfer required* as **Disabled**.</span></span>

    8.  <span data-ttu-id="1c53f-174">Sélectionnez un *abonnement*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-174">Select a *Subscription*.</span></span>

    9. <span data-ttu-id="1c53f-175">Choisissez un *groupe de ressources* ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="1c53f-175">Choose a *Resource Group* or create a new one.</span></span> <span data-ttu-id="1c53f-176">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-176">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="1c53f-177">Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="1c53f-177">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span> 

        > <span data-ttu-id="1c53f-178">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="1c53f-178">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    10. <span data-ttu-id="1c53f-179">Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.</span><span class="sxs-lookup"><span data-stu-id="1c53f-179">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    11. <span data-ttu-id="1c53f-180">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-180">Select **Create**.</span></span>

        ![informations sur le service d’entrée](images/AzureLabs-Lab5-03.png)

5.  <span data-ttu-id="1c53f-182">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="1c53f-182">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

6.  <span data-ttu-id="1c53f-183">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="1c53f-183">A notification will appear in the portal once the Service instance is created.</span></span>

    ![nouvelle notification dans le portail azure](images/AzureLabs-Lab5-04.png)

7.  <span data-ttu-id="1c53f-185">Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="1c53f-185">Click on the notifications to explore your new Service instance.</span></span>

    ![accéder à la ressource](images/AzureLabs-Lab5-05.png)

8.  <span data-ttu-id="1c53f-187">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="1c53f-187">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="1c53f-188">Vous serez dirigé vers votre nouvelle *compte de stockage* instance de service.</span><span class="sxs-lookup"><span data-stu-id="1c53f-188">You will be taken to your new *Storage account* service instance.</span></span>

    ![touches d’accès rapide](images/AzureLabs-Lab5-06.png)

9.  <span data-ttu-id="1c53f-190">Cliquez sur *clés d’accès*, pour faire apparaître les points de terminaison pour ce service cloud.</span><span class="sxs-lookup"><span data-stu-id="1c53f-190">Click *Access keys*, to reveal the endpoints for this cloud service.</span></span> <span data-ttu-id="1c53f-191">Utilisez *le bloc-notes* ou similaire, de copier l’un de vos clés pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-191">Use *Notepad* or similar, to copy one of your keys for use later.</span></span> <span data-ttu-id="1c53f-192">En outre, notez le *chaîne de connexion* valeur, car il sera utilisé dans le *AzureServices* (classe), ce qui vous créerez ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="1c53f-192">Also, note the *Connection string* value, as it will be used in the *AzureServices* class, which you will create later.</span></span>

    ![Copiez la chaîne de connexion](images/AzureLabs-Lab5-07.png)

## <a name="chapter-2---setting-up-an-azure-function"></a><span data-ttu-id="1c53f-194">Chapitre 2 - Configuration d’une fonction Azure</span><span class="sxs-lookup"><span data-stu-id="1c53f-194">Chapter 2 - Setting up an Azure Function</span></span>

<span data-ttu-id="1c53f-195">Vous allez maintenant écrire un **Azure** **fonction** dans le Service Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-195">You will now write an **Azure** **Function** in the Azure Service.</span></span>

<span data-ttu-id="1c53f-196">Vous pouvez utiliser un **Azure Function** à faire presque tout ce que vous le feriez avec une fonction classique dans votre code, la différence étant que cette fonction est accessible par toute application qui a des informations d’identification pour accéder à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-196">You can use an **Azure Function** to do nearly anything that you would do with a classic function in your code, the difference being that this function can be accessed by any application that has credentials to access your Azure Account.</span></span>

<span data-ttu-id="1c53f-197">Pour créer une fonction Azure :</span><span class="sxs-lookup"><span data-stu-id="1c53f-197">To create an Azure Function:</span></span>

1.  <span data-ttu-id="1c53f-198">À partir de votre *Azure Portal*, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez *Function App*, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-198">From your *Azure Portal*, click on **New** in the top left corner, and search for *Function App*, and click **Enter**.</span></span>

    ![Créer l’application de fonction](images/AzureLabs-Lab5-08.png)

    > [!NOTE]
    > <span data-ttu-id="1c53f-200">Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.</span><span class="sxs-lookup"><span data-stu-id="1c53f-200">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

2.  <span data-ttu-id="1c53f-201">La nouvelle page doit fournir une description de la *Azure Function App* service.</span><span class="sxs-lookup"><span data-stu-id="1c53f-201">The new page will provide a description of the *Azure Function App* service.</span></span> <span data-ttu-id="1c53f-202">En bas à gauche de cette invite, sélectionnez le **créer** bouton permettant de créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="1c53f-202">At the bottom left of this prompt, select the **Create** button, to create an association with this service.</span></span>

    ![informations sur l’application (fonction)](images/AzureLabs-Lab5-09.png)

3.  <span data-ttu-id="1c53f-204">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="1c53f-204">Once you have clicked on **Create**:</span></span>

    1.  <span data-ttu-id="1c53f-205">Fournir un *nom de l’application*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-205">Provide an *App name*.</span></span> <span data-ttu-id="1c53f-206">Uniquement des lettres et des chiffres peuvent être utilisés ici (limite supérieure ou inférieure est autorisé).</span><span class="sxs-lookup"><span data-stu-id="1c53f-206">Only letters and numbers can be used here (either upper or lower case is allowed).</span></span>

    2.  <span data-ttu-id="1c53f-207">Sélectionnez votre *abonnement*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-207">Select your preferred *Subscription*.</span></span>

    3. <span data-ttu-id="1c53f-208">Choisissez un *groupe de ressources* ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="1c53f-208">Choose a *Resource Group* or create a new one.</span></span> <span data-ttu-id="1c53f-209">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-209">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="1c53f-210">Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="1c53f-210">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span> 

        > <span data-ttu-id="1c53f-211">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="1c53f-211">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    4.  <span data-ttu-id="1c53f-212">Dans cet exercice, sélectionnez *Windows* comme choisi **système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-212">For this exercise, select *Windows* as the chosen **OS**.</span></span>

    5.  <span data-ttu-id="1c53f-213">Sélectionnez *Plan de consommation* pour le **Plan d’hébergement**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-213">Select *Consumption Plan* for the **Hosting Plan**.</span></span>

    6.  <span data-ttu-id="1c53f-214">Déterminer le *emplacement* pour votre groupe de ressources (si vous créez un nouveau groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="1c53f-214">Determine the *Location* for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="1c53f-215">Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="1c53f-215">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="1c53f-216">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="1c53f-216">Some Azure assets are only available in certain regions.</span></span> <span data-ttu-id="1c53f-217">Pour des performances optimales, sélectionnez la même région que le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="1c53f-217">For optimal performance, select the same region as the storage account.</span></span>

    7.  <span data-ttu-id="1c53f-218">Pour *stockage*, sélectionnez **utiliser l’existant**, et puis en utilisant le menu déroulant, recherchez votre stockage créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="1c53f-218">For *Storage*, select **Use existing**, and then using the dropdown menu, find your previously created storage.</span></span>

    8.  <span data-ttu-id="1c53f-219">Laissez *Application Insights* désactivée pour cet exercice.</span><span class="sxs-lookup"><span data-stu-id="1c53f-219">Leave *Application Insights* off for this exercise.</span></span>

        ![Détails de l’application d’entrée (fonction)](images/AzureLabs-Lab5-10.png)

4.  <span data-ttu-id="1c53f-221">Cliquez sur le bouton **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-221">Click the **Create** button.</span></span>

5.  <span data-ttu-id="1c53f-222">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="1c53f-222">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

6.  <span data-ttu-id="1c53f-223">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="1c53f-223">A notification will appear in the portal once the Service instance is created.</span></span>

    ![nouvelle notification du portail azure](images/AzureLabs-Lab5-11.png)

7.  <span data-ttu-id="1c53f-225">Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="1c53f-225">Click on the notifications to explore your new Service instance.</span></span> 

    ![Accédez à l’application de ressource (fonction)](images/AzureLabs-Lab5-12.png)

8.  <span data-ttu-id="1c53f-227">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="1c53f-227">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="1c53f-228">Vous serez dirigé vers votre nouvelle *Function App* instance de service.</span><span class="sxs-lookup"><span data-stu-id="1c53f-228">You will be taken to your new *Function App* service instance.</span></span>

9.  <span data-ttu-id="1c53f-229">Sur le *Function App* tableau de bord, pointez votre souris sur *fonctions*, trouvé dans le volet gauche, puis cliquez sur le **+ (plus)** symbole.</span><span class="sxs-lookup"><span data-stu-id="1c53f-229">On the *Function App* dashboard, hover your mouse over *Functions*, found within the panel on the left, and then click the **+ (plus)** symbol.</span></span>

    ![Créer une nouvelle fonction](images/AzureLabs-Lab5-13.png)

10. <span data-ttu-id="1c53f-231">Sur la page suivante, vérifiez **Webhook + API** est sélectionnée et pour *choisir une langue,* sélectionnez **CSharp**, comme il s’agit de la langue utilisée pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1c53f-231">On the next page, ensure **Webhook + API** is selected, and for *Choose a language,* select **CSharp**, as this will be the language used for this tutorial.</span></span> <span data-ttu-id="1c53f-232">Enfin, cliquez sur le **créer cette fonction** bouton.</span><span class="sxs-lookup"><span data-stu-id="1c53f-232">Lastly, click the **Create this function** button.</span></span>

    ![Sélectionnez web raccordement csharp](images/AzureLabs-Lab5-14.png)

11. <span data-ttu-id="1c53f-234">Vous devez être dirigé vers le code page (run.csx), si ce n’est pas, cliquez sur la fonction qui vient d’être créée dans la liste des fonctions dans le panneau de gauche.</span><span class="sxs-lookup"><span data-stu-id="1c53f-234">You should be taken to the code page (run.csx), if not though, click on the newly created Function in the Functions list within the panel on the left.</span></span>

    ![Ouvrez la nouvelle fonction](images/AzureLabs-Lab5-15.png)

12. <span data-ttu-id="1c53f-236">Copiez le code suivant dans votre fonction.</span><span class="sxs-lookup"><span data-stu-id="1c53f-236">Copy the following code into your function.</span></span> <span data-ttu-id="1c53f-237">Cette fonction retourne simplement un entier aléatoire compris entre 0 et 2 lorsqu’elle est appelée.</span><span class="sxs-lookup"><span data-stu-id="1c53f-237">This function will simply return a random integer between 0 and 2 when called.</span></span> <span data-ttu-id="1c53f-238">Ne pas vous inquiétez pas sur le code existant, n’hésitez pas à coller au-dessus d’elle.</span><span class="sxs-lookup"><span data-stu-id="1c53f-238">Do not worry about the existing code, feel free to paste over the top of it.</span></span>

    ```csharp
        using System.Net;
        using System.Threading.Tasks;

        public static int Run(CustomObject req, TraceWriter log)
        {
            Random rnd = new Random();
            int randomInt = rnd.Next(0, 3);
            return randomInt;
        }

        public class CustomObject
        {
            public String name {get; set;}
        }
    ```

13. <span data-ttu-id="1c53f-239">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-239">Select **Save**.</span></span>

14. <span data-ttu-id="1c53f-240">Le résultat doit ressembler à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1c53f-240">The result should look like the image below.</span></span>

15. <span data-ttu-id="1c53f-241">Cliquez sur **obtenir l’URL de la fonction** et prenez note de la *point de terminaison* affiché.</span><span class="sxs-lookup"><span data-stu-id="1c53f-241">Click on **Get function URL** and take note of the *endpoint* displayed.</span></span> <span data-ttu-id="1c53f-242">Vous devez l’insérer dans le *AzureServices* classe que vous créerez plus loin dans ce cours.</span><span class="sxs-lookup"><span data-stu-id="1c53f-242">You will need to insert it into the *AzureServices* class that you will create later in this course.</span></span>

    ![obtenir le point de terminaison (fonction)](images/AzureLabs-Lab5-16.png)

    ![obtenir le point de terminaison (fonction)](images/AzureLabs-Lab5-16-5.png)

## <a name="chapter-3---setting-up-the-unity-project"></a><span data-ttu-id="1c53f-245">Chapitre 3 - Configuration du projet Unity</span><span class="sxs-lookup"><span data-stu-id="1c53f-245">Chapter 3 - Setting up the Unity project</span></span>

<span data-ttu-id="1c53f-246">Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="1c53f-246">The following is a typical set up for developing with Mixed Reality, and as such, is a good template for other projects.</span></span>

<span data-ttu-id="1c53f-247">Configurer et tester votre casque immersives de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="1c53f-247">Set up and test your mixed reality immersive headset.</span></span>

> [!NOTE]
> <span data-ttu-id="1c53f-248">Vous allez **pas** nécessitent des contrôleurs de mouvement pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="1c53f-248">You will **not** require Motion Controllers for this course.</span></span> <span data-ttu-id="1c53f-249">Si vous avez besoin de prendre en charge de paramétrage le casque immersif, veuillez [visitez la réalité mixte configurer article](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span><span class="sxs-lookup"><span data-stu-id="1c53f-249">If you need support setting up the immersive headset, please [visit the mixed reality set up article](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span></span>

1.  <span data-ttu-id="1c53f-250">Ouvrez Unity et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-250">Open Unity and click **New**.</span></span>

    ![créer un projet unity](images/AzureLabs-Lab5-17.png)

2.  <span data-ttu-id="1c53f-252">Maintenant, vous devez fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="1c53f-252">You will now need to provide a Unity Project name.</span></span> <span data-ttu-id="1c53f-253">Insérer **MR_Azure_Functions**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-253">Insert **MR_Azure_Functions**.</span></span> <span data-ttu-id="1c53f-254">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-254">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="1c53f-255">Définir le *emplacement* à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="1c53f-255">Set the *Location* to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="1c53f-256">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-256">Then, click **Create project**.</span></span>

    ![Donnez un nom à un projet unity](images/AzureLabs-Lab5-18.png)

3.  <span data-ttu-id="1c53f-258">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-258">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="1c53f-259">Accédez à **modifier** > **préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-259">Go to **Edit** > **Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="1c53f-260">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-260">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="1c53f-261">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="1c53f-261">Close the **Preferences** window.</span></span>

    ![ensemble de visual studio comme éditeur de script](images/AzureLabs-Lab5-19.png)

4.  <span data-ttu-id="1c53f-263">Ensuite, accédez à **fichier** > **paramètres de Build** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **basculer la plateforme**  bouton.</span><span class="sxs-lookup"><span data-stu-id="1c53f-263">Next, go to **File** > **Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

    ![plateforme de commutation vers uwp](images/AzureLabs-Lab5-20.png)

5.  <span data-ttu-id="1c53f-265">Accédez à **fichier** > **paramètres de Build** et vous assurer que :</span><span class="sxs-lookup"><span data-stu-id="1c53f-265">Go to **File** > **Build Settings** and make sure that:</span></span>

    1. <span data-ttu-id="1c53f-266">**Équipement cible** a la valeur **n’importe quel appareil**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-266">**Target Device** is set to **Any Device**.</span></span>

        > <span data-ttu-id="1c53f-267">Pour Microsoft HoloLens, définissez **appareil cible** à *HoloLens*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-267">For Microsoft HoloLens, set **Target Device** to *HoloLens*.</span></span>

    2. <span data-ttu-id="1c53f-268">**Type de build** a la valeur **D3D**</span><span class="sxs-lookup"><span data-stu-id="1c53f-268">**Build Type** is set to **D3D**</span></span>

    3. <span data-ttu-id="1c53f-269">**Kit de développement logiciel** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="1c53f-269">**SDK** is set to **Latest installed**</span></span>

    4. <span data-ttu-id="1c53f-270">**Version de Visual Studio** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="1c53f-270">**Visual Studio Version** is set to **Latest installed**</span></span>

    5. <span data-ttu-id="1c53f-271">**Générez et exécutez** est défini sur **ordinateur Local**</span><span class="sxs-lookup"><span data-stu-id="1c53f-271">**Build and Run** is set to **Local Machine**</span></span>

    6. <span data-ttu-id="1c53f-272">Enregistrer la scène et l’ajouter à la build.</span><span class="sxs-lookup"><span data-stu-id="1c53f-272">Save the scene and add it to the build.</span></span>

        1.  <span data-ttu-id="1c53f-273">Cela en sélectionnant **ajouter un arrière-plan Open**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-273">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="1c53f-274">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="1c53f-274">A save window will appear.</span></span>

            ![ajouter des scènes ouverts](images/AzureLabs-Lab5-21.png)

        2.  <span data-ttu-id="1c53f-276">Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-276">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![créer le dossier de scènes](images/AzureLabs-Lab5-22.png)

        3.  <span data-ttu-id="1c53f-278">Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le **nom de fichier :** champ de texte, tapez **FunctionsScene**, puis appuyez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-278">Open your newly created **Scenes** folder, and then in the **File name:** text field, type **FunctionsScene**, then press **Save**.</span></span>

            ![Enregistrer la scène de fonctions](images/AzureLabs-Lab5-23.png)

6.  <span data-ttu-id="1c53f-280">Les autres paramètres, dans **paramètres de Build**, doit être conservé comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="1c53f-280">The remaining settings, in **Build Settings**, should be left as default for now.</span></span>

    ![Enregistrer la scène de fonctions](images/AzureLabs-Lab5-24.png)

7.  <span data-ttu-id="1c53f-282">Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve.</span><span class="sxs-lookup"><span data-stu-id="1c53f-282">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span>

    ![paramètres du lecteur dans l’inspecteur](images/AzureLabs-Lab5-25.png)

8.  <span data-ttu-id="1c53f-284">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="1c53f-284">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="1c53f-285">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="1c53f-285">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="1c53f-286">**Version du Runtime de script** doit être **expérimental** (.NET 4.6 équivalent), ce qui déclenchera une nécessité de redémarrer l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="1c53f-286">**Scripting Runtime Version** should be **Experimental** (.NET 4.6 Equivalent), which will trigger a need to restart the Editor.</span></span>
        2.  <span data-ttu-id="1c53f-287">**Script principal** doit être **.NET**</span><span class="sxs-lookup"><span data-stu-id="1c53f-287">**Scripting Backend** should be **.NET**</span></span>
        3.  <span data-ttu-id="1c53f-288">**Niveau de compatibilité d’API** doit être **.NET 4.6**</span><span class="sxs-lookup"><span data-stu-id="1c53f-288">**API Compatibility Level** should be **.NET 4.6**</span></span>

    2.  <span data-ttu-id="1c53f-289">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="1c53f-289">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>
        
        -  <span data-ttu-id="1c53f-290">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="1c53f-290">**InternetClient**</span></span>

            ![jeu de fonctionnalités](images/AzureLabs-Lab5-26.png)

    3.  <span data-ttu-id="1c53f-292">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **Windows Mixed Reality Kit de développement logiciel** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="1c53f-292">Further down the panel, in **XR Settings** (found below **Publishing Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![définir les paramètres de XR](images/AzureLabs-Lab5-27.png)

9.  <span data-ttu-id="1c53f-294">Dans *paramètres de Build* *Unity C# projets* est n’est plus grisée ; Cochez la case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="1c53f-294">Back in *Build Settings* *Unity C# Projects* is no longer greyed out; tick the checkbox next to this.</span></span>

    ![projets c# graduation](images/AzureLabs-Lab5-28.png)

10.  <span data-ttu-id="1c53f-296">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="1c53f-296">Close the Build Settings window.</span></span>

11. <span data-ttu-id="1c53f-297">Enregistrer votre projet et la scène (**fichier** > **enregistrer la scène / fichier** > **enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="1c53f-297">Save your Scene and Project (**FILE** > **SAVE SCENE / FILE** > **SAVE PROJECT**).</span></span>

## <a name="chapter-4---setup-main-camera"></a><span data-ttu-id="1c53f-298">Chapitre 4 - la caméra principale le programme d’installation</span><span class="sxs-lookup"><span data-stu-id="1c53f-298">Chapter 4 - Setup Main Camera</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c53f-299">Si vous souhaitez ignorer la *Unity configurer* les composants de ce cours et continuer directement dans le code, n’hésitez pas à [télécharger cette .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20305%20-%20Functions%20and%20storage/Azure-MR-305.unitypackage)et l’importer dans votre projet en tant qu’un [personnalisé Package](https://docs.unity3d.com/Manual/AssetPackages.html).</span><span class="sxs-lookup"><span data-stu-id="1c53f-299">If you wish to skip the *Unity Set up* components of this course, and continue straight into code, feel free to [download this .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20305%20-%20Functions%20and%20storage/Azure-MR-305.unitypackage), and import it into your project as a [Custom Package](https://docs.unity3d.com/Manual/AssetPackages.html).</span></span> <span data-ttu-id="1c53f-300">Il contient également les DLL dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="1c53f-300">This will also contain the DLLs from the next Chapter.</span></span> <span data-ttu-id="1c53f-301">Après l’importation, continuer à partir de [chapitre 7](#chapter-7---create-the-azureservices-class).</span><span class="sxs-lookup"><span data-stu-id="1c53f-301">After import, continue from [Chapter 7](#chapter-7---create-the-azureservices-class).</span></span> 

1.  <span data-ttu-id="1c53f-302">Dans le *hiérarchie panneau*, vous trouverez un objet appelé **Main Camera**, cet objet représente votre point de vue du « head » une fois que vous êtes « à l’intérieur » de votre application.</span><span class="sxs-lookup"><span data-stu-id="1c53f-302">In the *Hierarchy Panel*, you will find an object called **Main Camera**, this object represents your "head" point of view once you are "inside" your application.</span></span>

2.  <span data-ttu-id="1c53f-303">Avec le tableau de bord Unity devant vous, sélectionnez le **GameObject de caméra principale**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-303">With the Unity Dashboard in front of you, select the **Main Camera GameObject**.</span></span> <span data-ttu-id="1c53f-304">Vous remarquerez que le *panneau Inspecteur* (généralement situé vers la droite, dans le tableau de bord) affiche les différents composants de qui *GameObject*, avec *transformer* en haut, suivie de *caméra*et certains autres composants.</span><span class="sxs-lookup"><span data-stu-id="1c53f-304">You will notice that the *Inspector Panel* (generally found to the right, within the Dashboard) will show the various components of that *GameObject*, with *Transform* at the top, followed by *Camera*, and some other components.</span></span> <span data-ttu-id="1c53f-305">Vous devez réinitialiser la transformation de la caméra principale, donc il est positionné correctement.</span><span class="sxs-lookup"><span data-stu-id="1c53f-305">You will need to reset the Transform of the Main Camera, so it is positioned correctly.</span></span>

3.  <span data-ttu-id="1c53f-306">Pour ce faire, sélectionnez le **ENGRENAGE** icône en regard de la caméra *transformer* composant, puis sélectionnez **réinitialiser**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-306">To do this, select the **Gear** icon next to the Camera's *Transform* component, and select **Reset**.</span></span>

    ![Réinitialiser la transformation](images/AzureLabs-Lab5-29.png)

4.  <span data-ttu-id="1c53f-308">Puis mettez à jour le **transformer** composant ressemble à :</span><span class="sxs-lookup"><span data-stu-id="1c53f-308">Then update the **Transform** component to look like:</span></span>

    |         |    <span data-ttu-id="1c53f-309">TRANSFORMATION - POSITION</span><span class="sxs-lookup"><span data-stu-id="1c53f-309">TRANSFORM - POSITION</span></span>   |       |
    | :-----: | :-----------------------: | :----:|
    | <span data-ttu-id="1c53f-310">**X**</span><span class="sxs-lookup"><span data-stu-id="1c53f-310">**X**</span></span>   | <span data-ttu-id="1c53f-311">**Y**</span><span class="sxs-lookup"><span data-stu-id="1c53f-311">**Y**</span></span>                     | <span data-ttu-id="1c53f-312">**Z**</span><span class="sxs-lookup"><span data-stu-id="1c53f-312">**Z**</span></span> |
    | <span data-ttu-id="1c53f-313">0</span><span class="sxs-lookup"><span data-stu-id="1c53f-313">0</span></span>       | <span data-ttu-id="1c53f-314">1</span><span class="sxs-lookup"><span data-stu-id="1c53f-314">1</span></span>                         | <span data-ttu-id="1c53f-315">0</span><span class="sxs-lookup"><span data-stu-id="1c53f-315">0</span></span>     |    

    |       | <span data-ttu-id="1c53f-316">TRANSFORMATION - ROTATION</span><span class="sxs-lookup"><span data-stu-id="1c53f-316">TRANSFORM - ROTATION</span></span> |       |
    | :---: | :------------------: | :----:|
    | <span data-ttu-id="1c53f-317">**X**</span><span class="sxs-lookup"><span data-stu-id="1c53f-317">**X**</span></span> | <span data-ttu-id="1c53f-318">**Y**</span><span class="sxs-lookup"><span data-stu-id="1c53f-318">**Y**</span></span>                | <span data-ttu-id="1c53f-319">**Z**</span><span class="sxs-lookup"><span data-stu-id="1c53f-319">**Z**</span></span> |
    | <span data-ttu-id="1c53f-320">0</span><span class="sxs-lookup"><span data-stu-id="1c53f-320">0</span></span>     | <span data-ttu-id="1c53f-321">0</span><span class="sxs-lookup"><span data-stu-id="1c53f-321">0</span></span>                    | <span data-ttu-id="1c53f-322">0</span><span class="sxs-lookup"><span data-stu-id="1c53f-322">0</span></span>     |

    |       | <span data-ttu-id="1c53f-323">TRANSFORMATION - MISE À L’ÉCHELLE</span><span class="sxs-lookup"><span data-stu-id="1c53f-323">TRANSFORM - SCALE</span></span> |       |
    | :---: | :---------------: | :---: |
    | <span data-ttu-id="1c53f-324">**X**</span><span class="sxs-lookup"><span data-stu-id="1c53f-324">**X**</span></span> | <span data-ttu-id="1c53f-325">**Y**</span><span class="sxs-lookup"><span data-stu-id="1c53f-325">**Y**</span></span>             | <span data-ttu-id="1c53f-326">**Z**</span><span class="sxs-lookup"><span data-stu-id="1c53f-326">**Z**</span></span> |
    | <span data-ttu-id="1c53f-327">1</span><span class="sxs-lookup"><span data-stu-id="1c53f-327">1</span></span>     | <span data-ttu-id="1c53f-328">1</span><span class="sxs-lookup"><span data-stu-id="1c53f-328">1</span></span>                 | <span data-ttu-id="1c53f-329">1</span><span class="sxs-lookup"><span data-stu-id="1c53f-329">1</span></span>     |

    ![transformation de la caméra](images/AzureLabs-Lab5-30.png)

## <a name="chapter-5---setting-up-the-unity-scene"></a><span data-ttu-id="1c53f-331">Chapitre 5 : configuration de la scène Unity</span><span class="sxs-lookup"><span data-stu-id="1c53f-331">Chapter 5 - Setting up the Unity scene</span></span>

1.  <span data-ttu-id="1c53f-332">Avec le bouton droit dans une zone vide de la *hiérarchie panneau*, sous **objet 3D**, ajoutez un **plan**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-332">Right-click in an empty area of the *Hierarchy Panel*, under **3D  Object**, add a **Plane**.</span></span>

    ![créer un nouveau plan](images/AzureLabs-Lab5-31.png)

2.  <span data-ttu-id="1c53f-334">Avec le **plan** de l’objet sélectionné, modifiez les paramètres suivants dans le *panneau Inspecteur*:</span><span class="sxs-lookup"><span data-stu-id="1c53f-334">With the **Plane** object selected, change the following parameters in the *Inspector Panel*:</span></span>

    |       | <span data-ttu-id="1c53f-335">TRANSFORMATION - POSITION</span><span class="sxs-lookup"><span data-stu-id="1c53f-335">TRANSFORM - POSITION</span></span> |       |
    | :---: | :------------------: | :---: |
    | <span data-ttu-id="1c53f-336">**X**</span><span class="sxs-lookup"><span data-stu-id="1c53f-336">**X**</span></span> | <span data-ttu-id="1c53f-337">**Y**</span><span class="sxs-lookup"><span data-stu-id="1c53f-337">**Y**</span></span>                | <span data-ttu-id="1c53f-338">**Z**</span><span class="sxs-lookup"><span data-stu-id="1c53f-338">**Z**</span></span> |
    | <span data-ttu-id="1c53f-339">0</span><span class="sxs-lookup"><span data-stu-id="1c53f-339">0</span></span>     | <span data-ttu-id="1c53f-340">0</span><span class="sxs-lookup"><span data-stu-id="1c53f-340">0</span></span>                    | <span data-ttu-id="1c53f-341">4</span><span class="sxs-lookup"><span data-stu-id="1c53f-341">4</span></span>     |

    |       | <span data-ttu-id="1c53f-342">TRANSFORMATION - MISE À L’ÉCHELLE</span><span class="sxs-lookup"><span data-stu-id="1c53f-342">TRANSFORM - SCALE</span></span> |       |
    | :---: | :---------------: | :---: |
    | <span data-ttu-id="1c53f-343">**X**</span><span class="sxs-lookup"><span data-stu-id="1c53f-343">**X**</span></span> | <span data-ttu-id="1c53f-344">**Y**</span><span class="sxs-lookup"><span data-stu-id="1c53f-344">**Y**</span></span>             | <span data-ttu-id="1c53f-345">**Z**</span><span class="sxs-lookup"><span data-stu-id="1c53f-345">**Z**</span></span> |
    | <span data-ttu-id="1c53f-346">10</span><span class="sxs-lookup"><span data-stu-id="1c53f-346">10</span></span>    | <span data-ttu-id="1c53f-347">1</span><span class="sxs-lookup"><span data-stu-id="1c53f-347">1</span></span>                 | <span data-ttu-id="1c53f-348">10</span><span class="sxs-lookup"><span data-stu-id="1c53f-348">10</span></span>    |

    ![position du jeu de plan et mise à l’échelle](images/AzureLabs-Lab5-32.png)

    ![vue de la scène du plan](images/AzureLabs-Lab5-33.png)

3.  <span data-ttu-id="1c53f-351">Avec le bouton droit dans une zone vide de la *hiérarchie panneau*, sous **objet 3D**, ajoutez un **Cube**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-351">Right-click in an empty area of the *Hierarchy Panel*, under **3D Object**, add a **Cube**.</span></span>

    1.  <span data-ttu-id="1c53f-352">Renommer le Cube à **GazeButton** (avec le Cube sélectionné, appuyez sur « F2 »).</span><span class="sxs-lookup"><span data-stu-id="1c53f-352">Rename the Cube to **GazeButton** (with the Cube selected, press 'F2').</span></span>

    2.  <span data-ttu-id="1c53f-353">Modifiez les paramètres suivants dans le *panneau Inspecteur*:</span><span class="sxs-lookup"><span data-stu-id="1c53f-353">Change the following parameters in the *Inspector Panel*:</span></span>

        |       | <span data-ttu-id="1c53f-354">TRANSFORMATION - POSITION</span><span class="sxs-lookup"><span data-stu-id="1c53f-354">TRANSFORM - POSITION</span></span> |       |
        | :---: | :------------------: |:-----:|
        | <span data-ttu-id="1c53f-355">**X**</span><span class="sxs-lookup"><span data-stu-id="1c53f-355">**X**</span></span> | <span data-ttu-id="1c53f-356">**Y**</span><span class="sxs-lookup"><span data-stu-id="1c53f-356">**Y**</span></span>                | <span data-ttu-id="1c53f-357">**Z**</span><span class="sxs-lookup"><span data-stu-id="1c53f-357">**Z**</span></span> |
        | <span data-ttu-id="1c53f-358">0</span><span class="sxs-lookup"><span data-stu-id="1c53f-358">0</span></span>     | <span data-ttu-id="1c53f-359">3</span><span class="sxs-lookup"><span data-stu-id="1c53f-359">3</span></span>                    | <span data-ttu-id="1c53f-360">5</span><span class="sxs-lookup"><span data-stu-id="1c53f-360">5</span></span>     |


        ![transformation de bouton regards de jeu](images/AzureLabs-Lab5-34.png)

        ![utilisation de vue de la scène bouton](images/AzureLabs-Lab5-35.png)

    3.  <span data-ttu-id="1c53f-363">Cliquez sur le **balise** bouton de liste déroulante, puis cliquez sur **ajouter une balise** pour ouvrir le *balises & volet couches*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-363">Click on the **Tag** drop-down button and click on **Add Tag** to open the *Tags & Layers Pane*.</span></span>

        ![Ajouter une nouvelle balise](images/AzureLabs-Lab5-36.png)

        ![Sélectionnez plus (+)](images/AzureLabs-Lab5-37.png)

    4.  <span data-ttu-id="1c53f-366">Sélectionnez le **+ (plus)** bouton, puis, dans le *nouveau nom de balise* , entrez **GazeButton**, puis appuyez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-366">Select the **+ (plus)** button, and in the *New Tag Name* field, enter **GazeButton**, and press **Save**.</span></span>

        ![nouvelle balise de nom](images/AzureLabs-Lab5-38.png)

    5.  <span data-ttu-id="1c53f-368">Cliquez sur le **GazeButton** de l’objet dans le *hiérarchie panneau*, puis, dans le *panneau Inspecteur*, affecter nouvellement créé **GazeButton** balise.</span><span class="sxs-lookup"><span data-stu-id="1c53f-368">Click on the **GazeButton** object in the *Hierarchy Panel*, and in the *Inspector Panel*, assign the newly created **GazeButton** tag.</span></span>

        ![affecter des regards bouton la nouvelle balise](images/AzureLabs-Lab5-39.png)

4.  <span data-ttu-id="1c53f-370">Avec le bouton droit sur le **GazeButton** de l’objet, dans le *Panneau de la hiérarchie*et ajoutez un **GameObject vide** (qui sera ajouté comme un *enfant* objet).</span><span class="sxs-lookup"><span data-stu-id="1c53f-370">Right-click on the **GazeButton** object, in the *Hierarchy Panel*, and add an **Empty GameObject** (which will be added as a *child* object).</span></span>

5.  <span data-ttu-id="1c53f-371">Sélectionnez le nouvel objet et renommez-la **ShapeSpawnPoint**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-371">Select the new object and rename it **ShapeSpawnPoint**.</span></span>

    1.  <span data-ttu-id="1c53f-372">Modifiez les paramètres suivants dans le *panneau Inspecteur*:</span><span class="sxs-lookup"><span data-stu-id="1c53f-372">Change the following parameters in the *Inspector Panel*:</span></span>

        |       | <span data-ttu-id="1c53f-373">TRANSFORMATION - POSITION</span><span class="sxs-lookup"><span data-stu-id="1c53f-373">TRANSFORM - POSITION</span></span> |       |
        | :---: | :------------------: |:----: |
        | <span data-ttu-id="1c53f-374">**X**</span><span class="sxs-lookup"><span data-stu-id="1c53f-374">**X**</span></span> |<span data-ttu-id="1c53f-375">**Y**</span><span class="sxs-lookup"><span data-stu-id="1c53f-375">**Y**</span></span>                 | <span data-ttu-id="1c53f-376">**Z**</span><span class="sxs-lookup"><span data-stu-id="1c53f-376">**Z**</span></span> |
        | <span data-ttu-id="1c53f-377">0</span><span class="sxs-lookup"><span data-stu-id="1c53f-377">0</span></span>     | <span data-ttu-id="1c53f-378">-1</span><span class="sxs-lookup"><span data-stu-id="1c53f-378">-1</span></span>                   | <span data-ttu-id="1c53f-379">0</span><span class="sxs-lookup"><span data-stu-id="1c53f-379">0</span></span>     |

        ![mettre à jour le point de la génération dynamique de forme Transformer](images/AzureLabs-Lab5-40.png)

        ![vue de la scène de forme de point de la génération dynamique](images/AzureLabs-Lab5-41.png)

6.  <span data-ttu-id="1c53f-382">Vous allez ensuite créer un **texte 3D** objet pour fournir des commentaires sur l’état du service Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-382">Next you will create a **3D Text** object to provide feedback on the status of the Azure service.</span></span>

    <span data-ttu-id="1c53f-383">Cliquez avec le bouton droit sur le **GazeButton** panneau à nouveau dans la hiérarchie et ajoutez un **objet 3D** > **texte 3D** de l’objet en tant qu’un *enfant*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-383">Right click on the **GazeButton** in the Hierarchy Panel again and add a **3D Object** > **3D Text** object as a *child*.</span></span>

    ![créer le nouvel objet de texte 3D](images/AzureLabs-Lab5-42.png)

7.  <span data-ttu-id="1c53f-385">Renommer le **texte 3D** objet **AzureStatusText**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-385">Rename the **3D Text** object to **AzureStatusText**.</span></span>

8.  <span data-ttu-id="1c53f-386">Modifier le **AzureStatusText** transformation de l’objet comme suit :</span><span class="sxs-lookup"><span data-stu-id="1c53f-386">Change the **AzureStatusText** object Transform as follows:</span></span>

    |       | <span data-ttu-id="1c53f-387">TRANSFORMATION - POSITION</span><span class="sxs-lookup"><span data-stu-id="1c53f-387">TRANSFORM - POSITION</span></span> |       |
    | :---: | :------------------: | :---: |
    | <span data-ttu-id="1c53f-388">**X**</span><span class="sxs-lookup"><span data-stu-id="1c53f-388">**X**</span></span> | <span data-ttu-id="1c53f-389">**Y**</span><span class="sxs-lookup"><span data-stu-id="1c53f-389">**Y**</span></span>                | <span data-ttu-id="1c53f-390">**Z**</span><span class="sxs-lookup"><span data-stu-id="1c53f-390">**Z**</span></span> |
    | <span data-ttu-id="1c53f-391">0</span><span class="sxs-lookup"><span data-stu-id="1c53f-391">0</span></span>     | <span data-ttu-id="1c53f-392">0</span><span class="sxs-lookup"><span data-stu-id="1c53f-392">0</span></span>                    | <span data-ttu-id="1c53f-393">-0.6</span><span class="sxs-lookup"><span data-stu-id="1c53f-393">-0.6</span></span>  |

    |       | <span data-ttu-id="1c53f-394">TRANSFORMATION - MISE À L’ÉCHELLE</span><span class="sxs-lookup"><span data-stu-id="1c53f-394">TRANSFORM - SCALE</span></span> |       |
    | :---: | :---------------: | :---: |
    | <span data-ttu-id="1c53f-395">**X**</span><span class="sxs-lookup"><span data-stu-id="1c53f-395">**X**</span></span> | <span data-ttu-id="1c53f-396">**Y**</span><span class="sxs-lookup"><span data-stu-id="1c53f-396">**Y**</span></span>             | <span data-ttu-id="1c53f-397">**Z**</span><span class="sxs-lookup"><span data-stu-id="1c53f-397">**Z**</span></span> |
    | <span data-ttu-id="1c53f-398">0.1</span><span class="sxs-lookup"><span data-stu-id="1c53f-398">0.1</span></span>   | <span data-ttu-id="1c53f-399">0.1</span><span class="sxs-lookup"><span data-stu-id="1c53f-399">0.1</span></span>               | <span data-ttu-id="1c53f-400">0.1</span><span class="sxs-lookup"><span data-stu-id="1c53f-400">0.1</span></span>   |


    > [!NOTE]
    > <span data-ttu-id="1c53f-401">Ne vous inquiétez pas si elle semble être hors tension-centre, que ce problème sera résolu lorsque la ci-dessous texte Mesh composant est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="1c53f-401">Do not worry if it appears to be off-centre, as this will be fixed when the below Text Mesh component is updated.</span></span>

9.  <span data-ttu-id="1c53f-402">Modifier le **texte maillage** composant pour faire correspondre le ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1c53f-402">Change the **Text Mesh** component to match the below:</span></span>

    ![composant de maillage de texte Set](images/AzureLabs-Lab5-43.png)

    > [!TIP]
    > <span data-ttu-id="1c53f-404">La couleur sélectionnée ici est de couleur hexadécimale : **000000FF**, mais n’hésitez pas à choisir votre propre, assurez-vous simplement qu’il est lisible.</span><span class="sxs-lookup"><span data-stu-id="1c53f-404">The selected color here is Hex color: **000000FF**, though feel free to choose your own, just ensure it is readable.</span></span>

10. <span data-ttu-id="1c53f-405">Votre structure de hiérarchie le panneau de configuration doit maintenant ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="1c53f-405">Your Hierarchy Panel structure should now look like this:</span></span>

    ![texte de maillage dans la vue de la scène](images/AzureLabs-Lab5-43b.png)

10. <span data-ttu-id="1c53f-407">Votre scène doit maintenant ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="1c53f-407">Your scene should now look like this:</span></span>

    ![texte de maillage dans la vue de la scène](images/AzureLabs-Lab5-44.png)


## <a name="chapter-6---import-azure-storage-for-unity"></a><span data-ttu-id="1c53f-409">Chapitre 6 - importer le stockage Azure pour Unity</span><span class="sxs-lookup"><span data-stu-id="1c53f-409">Chapter 6 - Import Azure Storage for Unity</span></span>

<span data-ttu-id="1c53f-410">Vous allez utiliser Azure Storage pour Unity (qui, elle s’appuie sur le kit SDK Azure .net).</span><span class="sxs-lookup"><span data-stu-id="1c53f-410">You will be using Azure Storage for Unity (which itself leverages the .Net SDK for Azure).</span></span> <span data-ttu-id="1c53f-411">Vous trouverez plus d’informations sur ce point dans le [stockage Azure pour l’article de Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).</span><span class="sxs-lookup"><span data-stu-id="1c53f-411">You can read more about this at the [Azure Storage for Unity article](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).</span></span>

<span data-ttu-id="1c53f-412">Il est actuellement un problème connu dans Unity qui nécessite des plug-ins à être reconfiguré après l’importation.</span><span class="sxs-lookup"><span data-stu-id="1c53f-412">There is currently a known issue in Unity which requires plugins to be reconfigured after import.</span></span> <span data-ttu-id="1c53f-413">Ces étapes (4-7 de cette section) ne sera plus nécessaires une fois que le bogue a été résolu.</span><span class="sxs-lookup"><span data-stu-id="1c53f-413">These steps (4 - 7 in this section) will no longer be required after the bug has been resolved.</span></span>

<span data-ttu-id="1c53f-414">Pour importer le SDK dans votre propre projet, assurez-vous que vous avez téléchargé la dernière version ['.unitypackage' à partir de GitHub](https://aka.ms/azstorage-unitysdk).</span><span class="sxs-lookup"><span data-stu-id="1c53f-414">To import the SDK into your own project, make sure you have downloaded the latest ['.unitypackage' from GitHub](https://aka.ms/azstorage-unitysdk).</span></span> <span data-ttu-id="1c53f-415">Ensuite, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1c53f-415">Then, do the following:</span></span>

1.  <span data-ttu-id="1c53f-416">Ajouter le **.unitypackage** fichier à Unity à l’aide de la **actifs** > **importer un Package** > **Package personnalisé**option de menu.</span><span class="sxs-lookup"><span data-stu-id="1c53f-416">Add the **.unitypackage** file to Unity by using the **Assets** > **Import Package** > **Custom Package** menu option.</span></span>

2.  <span data-ttu-id="1c53f-417">Dans le **importer un Package Unity** zone s’affiche, vous pouvez sélectionner tous les éléments sous **plug-in** > **stockage**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-417">In the **Import Unity Package** box that pops up, you can select everything under **Plugin** > **Storage**.</span></span> <span data-ttu-id="1c53f-418">Désactivez tout le reste, qu’il n’est pas nécessaire pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="1c53f-418">Uncheck everything else, as it is not needed for this course.</span></span>

    ![importer dans le package](images/AzureLabs-Lab5-45.png)

3.  <span data-ttu-id="1c53f-420">Cliquez sur le **importation** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="1c53f-420">Click the **Import** button to add the items to your project.</span></span>

4.  <span data-ttu-id="1c53f-421">Accédez à la *stockage* dossier sous *plug-ins*, dans la vue du projet, puis sélectionnez les plug-ins suivants *uniquement*:</span><span class="sxs-lookup"><span data-stu-id="1c53f-421">Go to the *Storage* folder under *Plugins*, in the Project view, and select the following plugins *only*:</span></span>

    -   <span data-ttu-id="1c53f-422">Microsoft.Data.Edm</span><span class="sxs-lookup"><span data-stu-id="1c53f-422">Microsoft.Data.Edm</span></span>
    -   <span data-ttu-id="1c53f-423">Microsoft.Data.OData</span><span class="sxs-lookup"><span data-stu-id="1c53f-423">Microsoft.Data.OData</span></span>
    -   <span data-ttu-id="1c53f-424">Microsoft.WindowsAzure.Storage</span><span class="sxs-lookup"><span data-stu-id="1c53f-424">Microsoft.WindowsAzure.Storage</span></span>
    -   <span data-ttu-id="1c53f-425">Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="1c53f-425">Newtonsoft.Json</span></span>
    -   <span data-ttu-id="1c53f-426">System.Spatial</span><span class="sxs-lookup"><span data-stu-id="1c53f-426">System.Spatial</span></span>

        ![Décochez la case n’importe quelle plateforme](images/AzureLabs-Lab5-46.png)

5.  <span data-ttu-id="1c53f-428">Avec *ces plug-ins spécifiques* sélectionné, **Décochez** *plateforme Any* et **Décochez** *WSAPlayer* puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-428">With *these specific plugins* selected, **uncheck** *Any Platform* and **uncheck** *WSAPlayer* then click **Apply**.</span></span>

    ![appliquer des DLL de plateforme](images/AzureLabs-Lab5-47.png)

    > [!NOTE]
    > <span data-ttu-id="1c53f-430">Nous allons marquer ces plug-ins particuliers à utiliser uniquement dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="1c53f-430">We are marking these particular plugins to only be used in the Unity Editor.</span></span> <span data-ttu-id="1c53f-431">Il s’agit, car il existe différentes versions des mêmes plug-ins dans le dossier WSA qui sera utilisé après que le projet est exporté à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="1c53f-431">This is because there are different versions of the same plugins in the WSA folder that will be used after the project is exported from Unity.</span></span>

6.  <span data-ttu-id="1c53f-432">Dans le *stockage* dossier de plug-in, sélectionnez uniquement :</span><span class="sxs-lookup"><span data-stu-id="1c53f-432">In the *Storage* plugin folder, select only:</span></span>

    -   <span data-ttu-id="1c53f-433">Microsoft.Data.Services.Client</span><span class="sxs-lookup"><span data-stu-id="1c53f-433">Microsoft.Data.Services.Client</span></span>

        ![jeu de ne pas traiter les DLL](images/AzureLabs-Lab5-48.png)

7.  <span data-ttu-id="1c53f-435">Vérifier le **processus ne** sous *paramètres de plateforme* et cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-435">Check the **Don't Process** box under *Platform Settings* and click **Apply**.</span></span>

    ![n’appliquer aucun traitement](images/AzureLabs-Lab5-49.png)

    > [!NOTE]
    > <span data-ttu-id="1c53f-437">Nous sommes marquage ce plug-in « Ne pas traiter », car l’utilitaire de correction Unity assembly a des difficultés à traiter ce plug-in.</span><span class="sxs-lookup"><span data-stu-id="1c53f-437">We are marking this plugin "Don't process" because the Unity assembly patcher has difficulty processing this plugin.</span></span> <span data-ttu-id="1c53f-438">Le plug-in continue de fonctionner même si elle n’est pas traitée.</span><span class="sxs-lookup"><span data-stu-id="1c53f-438">The plugin will still work even though it is not processed.</span></span>

## <a name="chapter-7---create-the-azureservices-class"></a><span data-ttu-id="1c53f-439">Chapitre 7 - créer la classe AzureServices</span><span class="sxs-lookup"><span data-stu-id="1c53f-439">Chapter 7 - Create the AzureServices class</span></span>

<span data-ttu-id="1c53f-440">La première classe que vous vous apprêtez à créer est le *AzureServices* classe.</span><span class="sxs-lookup"><span data-stu-id="1c53f-440">The first class you are going to create is the *AzureServices* class.</span></span>

<span data-ttu-id="1c53f-441">Le *AzureServices* classe sera chargée de :</span><span class="sxs-lookup"><span data-stu-id="1c53f-441">The *AzureServices* class will be responsible for:</span></span>

-   <span data-ttu-id="1c53f-442">Stockage des informations d’identification de compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-442">Storing Azure Account credentials.</span></span>

-   <span data-ttu-id="1c53f-443">Appel de votre application de fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-443">Calling your Azure App Function.</span></span>

-   <span data-ttu-id="1c53f-444">Le chargement et le téléchargement du fichier de données dans votre stockage de Cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-444">The upload and download of the data file in your Azure Cloud Storage.</span></span>

<span data-ttu-id="1c53f-445">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="1c53f-445">To create this Class:</span></span>

1.  <span data-ttu-id="1c53f-446">Avec le bouton droit dans le *Asset* dossier, situé dans le panneau de configuration de projet, **créer** > **dossier**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-446">Right-click in the *Asset* Folder, located in the Project Panel, **Create** > **Folder**.</span></span> <span data-ttu-id="1c53f-447">Nommez le dossier **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-447">Name the folder **Scripts**.</span></span>

    ![créer un nouveau dossier](images/AzureLabs-Lab5-50.png)

    ![appelons le dossier - scripts](images/AzureLabs-Lab5-51.png)

2.  <span data-ttu-id="1c53f-450">Double-cliquez sur le dossier venez de créer, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="1c53f-450">Double click on the folder just created, to open it.</span></span>

3.  <span data-ttu-id="1c53f-451">Avec le bouton droit dans le dossier, **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-451">Right-click inside the folder, **Create** > **C# Script**.</span></span> <span data-ttu-id="1c53f-452">Appeler le script *AzureServices*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-452">Call the script *AzureServices*.</span></span>

4.  <span data-ttu-id="1c53f-453">Double-cliquez sur le nouveau *AzureServices* classe pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-453">Double click on the new *AzureServices* class to open it with *Visual Studio*.</span></span>

5.  <span data-ttu-id="1c53f-454">Ajoutez les espaces de noms suivantes au début de la *AzureServices*:</span><span class="sxs-lookup"><span data-stu-id="1c53f-454">Add the following namespaces to the top of the *AzureServices*:</span></span>

    ```csharp
        using System;
        using System.Threading.Tasks;
        using UnityEngine;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.File;
        using System.IO;
        using System.Net;
    ```

6.  <span data-ttu-id="1c53f-455">Ajoutez les champs d’inspecteur suivants à l’intérieur de la *AzureServices* classe :</span><span class="sxs-lookup"><span data-stu-id="1c53f-455">Add the following Inspector Fields inside the *AzureServices* class:</span></span>

    ```csharp
        /// <summary>
        /// Provides Singleton-like behavior to this class.
        /// </summary>
        public static AzureServices instance;

        /// <summary>
        /// Reference Target for AzureStatusText Text Mesh object
        /// </summary>
        public TextMesh azureStatusText;
    ```

7.  <span data-ttu-id="1c53f-456">Puis ajoutez les variables de membre suivantes à l’intérieur de la *AzureServices* classe :</span><span class="sxs-lookup"><span data-stu-id="1c53f-456">Then add the following member variables inside the *AzureServices* class:</span></span>

    ```csharp
        /// <summary>
        /// Holds the Azure Function endpoint - Insert your Azure Function
        /// Connection String here.
        /// </summary>

        private readonly string azureFunctionEndpoint = "--Insert here you AzureFunction Endpoint--";

        /// <summary>
        /// Holds the Storage Connection String - Insert your Azure Storage
        /// Connection String here.
        /// </summary>
        private readonly string storageConnectionString = "--Insert here you AzureStorage Connection String--";

        /// <summary>
        /// Name of the Cloud Share - Hosts directories.
        /// </summary>
        private const string fileShare = "fileshare";

        /// <summary>
        /// Name of a Directory within the Share
        /// </summary>
        private const string storageDirectory = "storagedirectory";

        /// <summary>
        /// The Cloud File
        /// </summary>
        private CloudFile shapeIndexCloudFile;

        /// <summary>
        /// The Linked Storage Account
        /// </summary>
        private CloudStorageAccount storageAccount;

        /// <summary>
        /// The Cloud Client
        /// </summary>
        private CloudFileClient fileClient;

        /// <summary>
        /// The Cloud Share - Hosts Directories
        /// </summary>
        private CloudFileShare share;

        /// <summary>
        /// The Directory in the share that will host the Cloud file
        /// </summary>
        private CloudFileDirectory dir;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="1c53f-457">Veillez à remplacer le *point de terminaison* et *chaîne de connexion* valeurs avec les valeurs de votre stockage Azure, trouvé dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1c53f-457">Make sure you replace the *endpoint* and *connection string* values with the values from your Azure storage, found in the Azure Portal</span></span>

8.  <span data-ttu-id="1c53f-458">Code pour *Awake()* et *Start()* méthodes doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="1c53f-458">Code for *Awake()* and *Start()* methods now needs to be added.</span></span> <span data-ttu-id="1c53f-459">Ces méthodes seront appelées lors de l’initialisation de la classe :</span><span class="sxs-lookup"><span data-stu-id="1c53f-459">These methods will be called when the class initializes:</span></span>

    ```csharp
        private void Awake()
        {
            instance = this;
        }

        // Use this for initialization
        private void Start()
        {
            // Set the Status text to loading, whilst attempting connection to Azure.
            azureStatusText.text = "Loading...";
        }

        /// <summary>
        /// Call to the Azure Function App to request a Shape.
        /// </summary>
        public async void CallAzureFunctionForNextShape()
        {

        }
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="1c53f-460">Nous permet de renseigner le code pour *CallAzureFunctionForNextShape()* dans un [chapitre futures](#chapter-10---completing-the-azureservices-class).</span><span class="sxs-lookup"><span data-stu-id="1c53f-460">We will fill in the code for *CallAzureFunctionForNextShape()* in a [future Chapter](#chapter-10---completing-the-azureservices-class).</span></span>

9.  <span data-ttu-id="1c53f-461">Supprimer le *Update()* étant donné que cette classe ne l’utilise pas de méthode.</span><span class="sxs-lookup"><span data-stu-id="1c53f-461">Delete the *Update()* method since this class will not use it.</span></span>

10. <span data-ttu-id="1c53f-462">Enregistrez vos modifications dans Visual Studio, puis revenez à Unity.</span><span class="sxs-lookup"><span data-stu-id="1c53f-462">Save your changes in Visual Studio, and then return to Unity.</span></span>

11. <span data-ttu-id="1c53f-463">Cliquez et faites glisser le *AzureServices* classe à partir du dossier Scripts à l’objet Main Camera dans le *hiérarchie panneau*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-463">Click and drag the *AzureServices* class from the Scripts folder to the Main Camera object in the *Hierarchy Panel*.</span></span>

12. <span data-ttu-id="1c53f-464">Sélectionnez la caméra principale, puis saisissez le **AzureStatusText** objet enfant à partir de sous le **GazeButton** de l’objet et placez-le dans le **AzureStatusText** cible de référence champ dans le *inspecteur*, pour fournir la référence à la *AzureServices* script.</span><span class="sxs-lookup"><span data-stu-id="1c53f-464">Select the Main Camera, then grab the **AzureStatusText** child object from beneath the **GazeButton** object, and place it within the **AzureStatusText** reference target field, in the *Inspector*, to provide the reference to the *AzureServices* script.</span></span>

    ![affecter la cible de référence de texte de statut azure](images/AzureLabs-Lab5-52.png)

## <a name="chapter-8---create-the-shapefactory-class"></a><span data-ttu-id="1c53f-466">Chapitre 8 - créer la classe ShapeFactory</span><span class="sxs-lookup"><span data-stu-id="1c53f-466">Chapter 8 - Create the ShapeFactory class</span></span>

<span data-ttu-id="1c53f-467">Le script suivant pour créer, est la *ShapeFactory* classe.</span><span class="sxs-lookup"><span data-stu-id="1c53f-467">The next script to create, is the *ShapeFactory* class.</span></span> <span data-ttu-id="1c53f-468">Le rôle de cette classe consiste à créer une nouvelle forme lorsque demandé et conserver un historique des formes créées dans un *forme historique*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-468">The role of this class is to create a new shape, when requested, and keep a history of the shapes created in a *Shape History List*.</span></span> <span data-ttu-id="1c53f-469">Chaque fois qu’une forme est créée, le *forme historique* est mis à jour dans le *AzureService* classe et stockées dans votre *stockage Azure*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-469">Every time a shape is created, the *Shape History list* is updated in the *AzureService* class, and then stored in your *Azure Storage*.</span></span> <span data-ttu-id="1c53f-470">Lorsque l’application démarre, si un fichier stocké est trouvé dans votre *stockage Azure*, le *forme historique* est récupéré et relus, avec le **texte 3D** objet fournissant Indique si la forme générée est à partir du stockage, ou de nouvelles.</span><span class="sxs-lookup"><span data-stu-id="1c53f-470">When the application starts, if a stored file is found in your *Azure Storage*, the *Shape History list* is retrieved and replayed, with the **3D Text** object providing whether the generated shape is from storage, or new.</span></span>

<span data-ttu-id="1c53f-471">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="1c53f-471">To create this class:</span></span>

1.  <span data-ttu-id="1c53f-472">Accédez à la **Scripts** dossier que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="1c53f-472">Go to the **Scripts** folder you created previously.</span></span>

2.  <span data-ttu-id="1c53f-473">Avec le bouton droit dans le dossier, **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-473">Right-click inside the folder, **Create** > **C# Script**.</span></span> <span data-ttu-id="1c53f-474">Appeler le script *ShapeFactory*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-474">Call the script *ShapeFactory*.</span></span>

3.  <span data-ttu-id="1c53f-475">Double-cliquez sur le nouveau *ShapeFactory* script pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-475">Double click on the new *ShapeFactory* script to open it with *Visual Studio*.</span></span>

4.  <span data-ttu-id="1c53f-476">Vérifiez le *ShapeFactory* classe inclut des espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="1c53f-476">Ensure the *ShapeFactory* class includes the following namespaces:</span></span>

    ```csharp
        using System.Collections.Generic;
        using UnityEngine;
    ```

5.  <span data-ttu-id="1c53f-477">Ajoutez les variables ci-dessous pour le *ShapeFactory* classe, puis remplacez le *Start()* et *Awake()* fonctions avec ceux ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1c53f-477">Add the variables shown below to the *ShapeFactory* class, and replace the *Start()* and *Awake()* functions with those below:</span></span>

    ```csharp
        /// <summary>
        /// Provide this class Singleton-like behaviour
        /// </summary>
        [HideInInspector]
        public static ShapeFactory instance;

        /// <summary>
        /// Provides an Inspector exposed reference to ShapeSpawnPoint
        /// </summary>
        [SerializeField]
        public Transform spawnPoint;

        /// <summary>
        /// Shape History Index
        /// </summary>
        [HideInInspector]
        public List<int> shapeHistoryList;

        /// <summary>
        /// Shapes Enum for selecting required shape
        /// </summary>
        private enum Shapes { Cube, Sphere, Cylinder }

        private void Awake()
        {
            instance = this;
        }

        private void Start()
        {
            shapeHistoryList = new List<int>();
        }
    ```

6.  <span data-ttu-id="1c53f-478">Le *CreateShape()* méthode génère les formes primitifs, en fonction de la liste fournie *entier* paramètre.</span><span class="sxs-lookup"><span data-stu-id="1c53f-478">The *CreateShape()* method generates the primitive shapes, based upon the provided *integer* parameter.</span></span> <span data-ttu-id="1c53f-479">Le paramètre booléen est utilisé pour spécifier si la forme actuellement créée à partir du stockage, ou nouvelle.</span><span class="sxs-lookup"><span data-stu-id="1c53f-479">The Boolean parameter is used to specify whether the currently created shape is from storage, or new.</span></span> <span data-ttu-id="1c53f-480">Placez le code suivant dans votre *ShapeFactory* (classe), sous les méthodes précédentes :</span><span class="sxs-lookup"><span data-stu-id="1c53f-480">Place the following code in your *ShapeFactory* class, below the previous methods:</span></span>

    ```csharp
        /// <summary>
        /// Use the Shape Enum to spawn a new Primitive object in the scene
        /// </summary>
        /// <param name="shape">Enumerator Number for Shape</param>
        /// <param name="storageShape">Provides whether this is new or old</param>
        internal void CreateShape(int shape, bool storageSpace)
        {
            Shapes primitive = (Shapes)shape;
            GameObject newObject = null;
            string shapeText = storageSpace == true ? "Storage: " : "New: ";

            AzureServices.instance.azureStatusText.text = string.Format("{0}{1}", shapeText, primitive.ToString());

            switch (primitive)
            {
                case Shapes.Cube:
                newObject = GameObject.CreatePrimitive(PrimitiveType.Cube);
                break;

                case Shapes.Sphere:
                newObject = GameObject.CreatePrimitive(PrimitiveType.Sphere);
                break;

                case Shapes.Cylinder:
                newObject = GameObject.CreatePrimitive(PrimitiveType.Cylinder);
                break;
            }

            if (newObject != null)
            {
                newObject.transform.position = spawnPoint.position;

                newObject.transform.localScale = new Vector3(0.5f, 0.5f, 0.5f);

                newObject.AddComponent<Rigidbody>().useGravity = true;

                newObject.GetComponent<Renderer>().material.color = UnityEngine.Random.ColorHSV(0f, 1f, 1f, 1f, 0.5f, 1f);
            }
        }
    ```

7.  <span data-ttu-id="1c53f-481">Veillez à enregistrer vos modifications dans Visual Studio avant de retourner à Unity.</span><span class="sxs-lookup"><span data-stu-id="1c53f-481">Be sure to save your changes in Visual Studio before returning to Unity.</span></span>

8.  <span data-ttu-id="1c53f-482">Précédent dans l’éditeur Unity, cliquez et faites glisser le *ShapeFactory* classe à partir de la **Scripts** dossier pour le **Main Camera** de l’objet dans le *hiérarchie panneau*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-482">Back in the Unity Editor, click and drag the *ShapeFactory* class from the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span>

9. <span data-ttu-id="1c53f-483">Avec la caméra principale sélectionnée, vous remarquerez le *ShapeFactory* du composant script est manquant le *Spawn Point* référence.</span><span class="sxs-lookup"><span data-stu-id="1c53f-483">With the Main Camera selected you will notice the *ShapeFactory* script component is missing the *Spawn Point* reference.</span></span> <span data-ttu-id="1c53f-484">Pour corriger ce problème, faites glisser le **ShapeSpawnPoint** de l’objet à partir de la *Panneau de la hiérarchie* à la **Spawn Point** cible de référence.</span><span class="sxs-lookup"><span data-stu-id="1c53f-484">To fix it, drag the **ShapeSpawnPoint** object from the *Hierarchy Panel* to the **Spawn Point** reference target.</span></span>

    ![cible de référence de jeu forme factory](images/AzureLabs-Lab5-53.png)

## <a name="chapter-9---create-the-gaze-class"></a><span data-ttu-id="1c53f-486">Chapitre 9 - créer la classe du pointage de regard</span><span class="sxs-lookup"><span data-stu-id="1c53f-486">Chapter 9 - Create the Gaze class</span></span>

<span data-ttu-id="1c53f-487">Est le dernier script, vous devez créer le *les regards* classe.</span><span class="sxs-lookup"><span data-stu-id="1c53f-487">The last script you need to create is the *Gaze* class.</span></span>

<span data-ttu-id="1c53f-488">Cette classe est chargée pour la création d’un **Raycast** qui est projeté vers l’avant à partir de la caméra principale, pour détecter quel objet consulte l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1c53f-488">This class is responsible for creating a **Raycast** that will be projected forward from the Main Camera, to detect which object the user is looking at.</span></span> <span data-ttu-id="1c53f-489">Dans ce cas, le Raycast devrez déterminer si l’utilisateur consulte la **GazeButton** de l’objet dans la scène et déclencher un comportement.</span><span class="sxs-lookup"><span data-stu-id="1c53f-489">In this case, the Raycast will need to identify if the user is looking at the **GazeButton** object in the scene and trigger a behavior.</span></span>

<span data-ttu-id="1c53f-490">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="1c53f-490">To create this Class:</span></span>

1.  <span data-ttu-id="1c53f-491">Accédez à la **Scripts** dossier que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="1c53f-491">Go to the **Scripts** folder you created previously.</span></span>

2.  <span data-ttu-id="1c53f-492">Avec le bouton droit dans le volet de projet, **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-492">Right-click in the Project Panel, **Create** > **C# Script**.</span></span> <span data-ttu-id="1c53f-493">Appeler le script *les regards*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-493">Call the script *Gaze*.</span></span>

3.  <span data-ttu-id="1c53f-494">Double-cliquez sur le nouveau *les regards* script pour l’ouvrir avec *Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="1c53f-494">Double click on the new *Gaze* script to open it with *Visual Studio.*</span></span>

4.  <span data-ttu-id="1c53f-495">Vérifiez que l’espace de noms suivant est inclus en haut du script :</span><span class="sxs-lookup"><span data-stu-id="1c53f-495">Ensure the following namespace is included at the top of the script:</span></span>

    ```csharp
        using UnityEngine;
    ```

5.  <span data-ttu-id="1c53f-496">Puis ajoutez les variables suivantes à l’intérieur de la *les regards* classe :</span><span class="sxs-lookup"><span data-stu-id="1c53f-496">Then add the following variables inside the *Gaze* class:</span></span>

    ```csharp
        /// <summary>
        /// Provides Singleton-like behavior to this class.
        /// </summary>
        public static Gaze instance;

        /// <summary>
        /// The Tag which the Gaze will use to interact with objects. Can also be set in editor.
        /// </summary>
        public string InteractibleTag = "GazeButton";

        /// <summary>
        /// The layer which will be detected by the Gaze ('~0' equals everything).
        /// </summary>
        public LayerMask LayerMask = ~0;

        /// <summary>
        /// The Max Distance the gaze should travel, if it has not hit anything.
        /// </summary>
        public float GazeMaxDistance = 300;

        /// <summary>
        /// The size of the cursor, which will be created.
        /// </summary>
        public Vector3 CursorSize = new Vector3(0.05f, 0.05f, 0.05f);

        /// <summary>
        /// The color of the cursor - can be set in editor.
        /// </summary>
        public Color CursorColour = Color.HSVToRGB(0.0223f, 0.7922f, 1.000f);

        /// <summary>
        /// Provides when the gaze is ready to start working (based upon whether
        /// Azure connects successfully).
        /// </summary>
        internal bool GazeEnabled = false;

        /// <summary>
        /// The currently focused object.
        /// </summary>
        internal GameObject FocusedObject { get; private set; }

        /// <summary>
        /// The object which was last focused on.
        /// </summary>
        internal GameObject _oldFocusedObject { get; private set; }

        /// <summary>
        /// The info taken from the last hit.
        /// </summary>
        internal RaycastHit HitInfo { get; private set; }

        /// <summary>
        /// The cursor object.
        /// </summary>
        internal GameObject Cursor { get; private set; }

        /// <summary>
        /// Provides whether the raycast has hit something.
        /// </summary>
        internal bool Hit { get; private set; }

        /// <summary>
        /// This will store the position which the ray last hit.
        /// </summary>
        internal Vector3 Position { get; private set; }

        /// <summary>
        /// This will store the normal, of the ray from its last hit.
        /// </summary>
        internal Vector3 Normal { get; private set; }

        /// <summary>
        /// The start point of the gaze ray cast.
        /// </summary>
        private Vector3 _gazeOrigin;

        /// <summary>
        /// The direction in which the gaze should be.
        /// </summary>
        private Vector3 _gazeDirection;
    ```

> [!IMPORTANT]
> <span data-ttu-id="1c53f-497">Certaines de ces variables pourront être modifiées dans le *éditeur*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-497">Some of these variables will be able to be edited in the *Editor*.</span></span>

6.  <span data-ttu-id="1c53f-498">Code pour le *Awake()* et *Start()* méthodes doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="1c53f-498">Code for the *Awake()* and *Start()* methods now needs to be added.</span></span>

    ```csharp
        /// <summary>
        /// The method used after initialization of the scene, though before Start().
        /// </summary>
        private void Awake()
        {
            // Set this class to behave similar to singleton
            instance = this;
        }

        /// <summary>
        /// Start method used upon initialization.
        /// </summary>
        private void Start()
        {
            FocusedObject = null;
            Cursor = CreateCursor();
        }
    ```

7.  <span data-ttu-id="1c53f-499">Ajoutez le code suivant, qui crée un objet curseur au début, ainsi que la *Update()* (méthode), qui sera exécuté par la méthode Raycast, ainsi que d’en cours où la valeur booléenne GazeEnabled est activé ou désactivé :</span><span class="sxs-lookup"><span data-stu-id="1c53f-499">Add the following code, which will create a cursor object at start, along with the *Update()* method, which will run the Raycast method, along with being where the GazeEnabled boolean is toggled:</span></span>

    ```csharp
        /// <summary>
        /// Method to create a cursor object.
        /// </summary>
        /// <returns></returns>
        private GameObject CreateCursor()
        {
            GameObject newCursor = GameObject.CreatePrimitive(PrimitiveType.Sphere);
            newCursor.SetActive(false);

            // Remove the collider, so it doesn't block raycast.
            Destroy(newCursor.GetComponent<SphereCollider>());
            newCursor.transform.localScale = CursorSize;

            newCursor.GetComponent<MeshRenderer>().material = new Material(Shader.Find("Diffuse"))
            {
                color = CursorColour
            };

            newCursor.name = "Cursor";

            newCursor.SetActive(true);

            return newCursor;
        }

        /// <summary>
        /// Called every frame
        /// </summary>
        private void Update()
        {
            if(GazeEnabled == true)
            {
                _gazeOrigin = Camera.main.transform.position;

                _gazeDirection = Camera.main.transform.forward;

                UpdateRaycast();
            }
        }
    ```

8. <span data-ttu-id="1c53f-500">Ajoutez ensuite le *UpdateRaycast()* (méthode), ce qui permettra une Raycast de projet et détecter la cible du positionnement.</span><span class="sxs-lookup"><span data-stu-id="1c53f-500">Next add the *UpdateRaycast()* method, which will project a Raycast and detect the hit target.</span></span>

    ```csharp
        private void UpdateRaycast()
        {
            // Set the old focused gameobject.
            _oldFocusedObject = FocusedObject;

            RaycastHit hitInfo;

            // Initialise Raycasting.
            Hit = Physics.Raycast(_gazeOrigin,
                _gazeDirection,
                out hitInfo,
                GazeMaxDistance, LayerMask);

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

            // Check whether the previous focused object is this same 
            //    object. If so, reset the focused object.
            if (FocusedObject != _oldFocusedObject)
            {
                ResetFocusedObject();

                if (FocusedObject != null)
                {
                if (FocusedObject.CompareTag(InteractibleTag.ToString()))
                {
                        // Set the Focused object to green - success!
                        FocusedObject.GetComponent<Renderer>().material.color = Color.green;

                        // Start the Azure Function, to provide the next shape!
                        AzureServices.instance.CallAzureFunctionForNextShape();
                    }
                }
            }
        }
    ```

9. <span data-ttu-id="1c53f-501">Enfin, ajoutez le *ResetFocusedObject()* (méthode), ce qui active et désactive la couleur GazeButton objets actuelle, qui indique si elle crée une nouvelle forme ou non.</span><span class="sxs-lookup"><span data-stu-id="1c53f-501">Lastly, add the *ResetFocusedObject()* method, which will toggle the GazeButton objects current color, indicating whether it is creating a new shape or not.</span></span>

    ```csharp
        /// <summary>
        /// Reset the old focused object, stop the gaze timer, and send data if it
        /// is greater than one.
        /// </summary>
        private void ResetFocusedObject()
        {
            // Ensure the old focused object is not null.
            if (_oldFocusedObject != null)
            {
                if (_oldFocusedObject.CompareTag(InteractibleTag.ToString()))
                {
                    // Set the old focused object to red - its original state.
                    _oldFocusedObject.GetComponent<Renderer>().material.color = Color.red;
                }
            }
        }
    ```

10.  <span data-ttu-id="1c53f-502">Enregistrez vos modifications dans Visual Studio avant de retourner à Unity.</span><span class="sxs-lookup"><span data-stu-id="1c53f-502">Save your changes in Visual Studio before returning to Unity.</span></span>

11.  <span data-ttu-id="1c53f-503">Cliquez et faites glisser le *les regards* classe à partir du dossier Scripts à la **Main Camera** de l’objet dans le *hiérarchie panneau*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-503">Click and drag the *Gaze* class from the Scripts folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span>

## <a name="chapter-10---completing-the-azureservices-class"></a><span data-ttu-id="1c53f-504">Chapitre 10 - fin de la classe AzureServices</span><span class="sxs-lookup"><span data-stu-id="1c53f-504">Chapter 10 - Completing the AzureServices class</span></span>

<span data-ttu-id="1c53f-505">Avec les autres scripts en place, il est possible de *complète* le *AzureServices* classe.</span><span class="sxs-lookup"><span data-stu-id="1c53f-505">With the other scripts in place, it is now possible to *complete* the *AzureServices* class.</span></span> <span data-ttu-id="1c53f-506">Cela sera possible via :</span><span class="sxs-lookup"><span data-stu-id="1c53f-506">This will be achieved through:</span></span>

1.  <span data-ttu-id="1c53f-507">Ajout d’une nouvelle méthode nommée *CreateCloudIdentityAsync()* , pour définir les variables de l’authentification nécessaires pour communiquer avec Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-507">Adding a new method named *CreateCloudIdentityAsync()*, to set up the authentication variables needed for communicating with Azure.</span></span>

    > <span data-ttu-id="1c53f-508">Cette méthode vérifie également l’existence d’un fichier précédemment stocké qui contient la liste de forme.</span><span class="sxs-lookup"><span data-stu-id="1c53f-508">This method will also check for the existence of a previously stored File containing the Shape List.</span></span>
    >
    > <span data-ttu-id="1c53f-509">**Si le fichier se trouve**, il désactivera l’utilisateur *les regards*et déclencher la création de forme, selon le modèle de formes, tel que stocké dans le **fichier de stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-509">**If the file is found**, it will disable the user *Gaze*, and trigger Shape creation, according to the pattern of shapes, as stored in the **Azure Storage file**.</span></span> <span data-ttu-id="1c53f-510">L’utilisateur peut voir cela, comme le **texte Mesh** fournira l’affichage « Stockage » ou « Nouveau », en fonction de l’origine de formes.</span><span class="sxs-lookup"><span data-stu-id="1c53f-510">The user can see this, as the **Text Mesh** will provide display 'Storage' or 'New', depending on the shapes origin.</span></span>
    >
    > <span data-ttu-id="1c53f-511">**Si aucun fichier n’est trouvé**, il prend en charge la *les regards*, ce qui permet de créer des formes en examinant le **GazeButton** objet dans la scène.</span><span class="sxs-lookup"><span data-stu-id="1c53f-511">**If no file is found**, it will enable the *Gaze*, enabling the user to create shapes when looking at the **GazeButton** object in the scene.</span></span>

    ```csharp
        /// <summary>
        /// Create the references necessary to log into Azure
        /// </summary>
        private async void CreateCloudIdentityAsync()
        {
            // Retrieve storage account information from connection string
            storageAccount = CloudStorageAccount.Parse(storageConnectionString);

            // Create a file client for interacting with the file service.
            fileClient = storageAccount.CreateCloudFileClient();

            // Create a share for organizing files and directories within the storage account.
            share = fileClient.GetShareReference(fileShare);

            await share.CreateIfNotExistsAsync();

            // Get a reference to the root directory of the share.
            CloudFileDirectory root = share.GetRootDirectoryReference();

            // Create a directory under the root directory
            dir = root.GetDirectoryReference(storageDirectory);

            await dir.CreateIfNotExistsAsync();

            //Check if the there is a stored text file containing the list
            shapeIndexCloudFile = dir.GetFileReference("TextShapeFile");

            if (!await shapeIndexCloudFile.ExistsAsync())
            {
                // File not found, enable gaze for shapes creation
                Gaze.instance.GazeEnabled = true;

                azureStatusText.text = "No Shape\nFile!";
            }
            else
            {
                // The file has been found, disable gaze and get the list from the file
                Gaze.instance.GazeEnabled = false;

                azureStatusText.text = "Shape File\nFound!";

                await ReplicateListFromAzureAsync();
            }
        }
    ```

2.  <span data-ttu-id="1c53f-512">L’extrait de code suivant est depuis le *Start()* méthode ; où un appel sera le *CreateCloudIdentityAsync()* (méthode).</span><span class="sxs-lookup"><span data-stu-id="1c53f-512">The next code snippet is from within the *Start()* method; wherein a call will be made to the *CreateCloudIdentityAsync()* method.</span></span> <span data-ttu-id="1c53f-513">N’hésitez pas à copier sur votre actuel *Start()* (méthode), avec la ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1c53f-513">Feel free to copy over your current *Start()* method, with the below:</span></span>

    ```csharp
        private void Start()
        {
            // Disable TLS cert checks only while in Unity Editor (until Unity adds support for TLS)
    #if UNITY_EDITOR
            ServicePointManager.ServerCertificateValidationCallback = delegate { return true; };
    #endif

            // Set the Status text to loading, whilst attempting connection to Azure.
            azureStatusText.text = "Loading...";

            //Creating the references necessary to log into Azure and check if the Storage Directory is empty
            CreateCloudIdentityAsync();
        }
    ```

3.  <span data-ttu-id="1c53f-514">Renseignez le code pour la méthode *CallAzureFunctionForNextShape()* .</span><span class="sxs-lookup"><span data-stu-id="1c53f-514">Fill in the code for the method *CallAzureFunctionForNextShape()*.</span></span> <span data-ttu-id="1c53f-515">Vous allez utiliser l’élément précédemment créé *Azure Function App* pour demander un index de la forme.</span><span class="sxs-lookup"><span data-stu-id="1c53f-515">You will use the previously created *Azure Function App* to request a shape index.</span></span> <span data-ttu-id="1c53f-516">Une fois la nouvelle forme est reçue, cette méthode envoie la forme pour le *ShapeFactory* classe pour créer la nouvelle forme dans la scène.</span><span class="sxs-lookup"><span data-stu-id="1c53f-516">Once the new shape is received, this method will send the shape to the *ShapeFactory* class to create the new shape in the scene.</span></span> <span data-ttu-id="1c53f-517">Utilisez le code ci-dessous pour terminer le corps de *CallAzureFunctionForNextShape()* .</span><span class="sxs-lookup"><span data-stu-id="1c53f-517">Use the code below to complete the body of *CallAzureFunctionForNextShape()*.</span></span>

    ```csharp
        /// <summary>
        /// Call to the Azure Function App to request a Shape.
        /// </summary>
        public async void CallAzureFunctionForNextShape()
        {
            int azureRandomInt = 0;

            // Call Azure function
            HttpWebRequest webRequest = WebRequest.CreateHttp(azureFunctionEndpoint);

            WebResponse response = await webRequest.GetResponseAsync();

            // Read response as string
            using (Stream stream = response.GetResponseStream())
            {
                StreamReader reader = new StreamReader(stream);

                String responseString = reader.ReadToEnd();

                //parse result as integer
                Int32.TryParse(responseString, out azureRandomInt);
            }

            //add random int from Azure to the ShapeIndexList
            ShapeFactory.instance.shapeHistoryList.Add(azureRandomInt);

            ShapeFactory.instance.CreateShape(azureRandomInt, false);

            //Save to Azure storage
            await UploadListToAzureAsync();
        }
    ```

4.  <span data-ttu-id="1c53f-518">Ajoutez une méthode pour créer une chaîne, en concaténant les entiers stockés dans la liste d’historique de forme et l’enregistrer dans votre *Azure stockage fichier*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-518">Add a method to create a string, by concatenating the integers stored in the shape history list, and saving it in your *Azure Storage File*.</span></span>

    ```csharp
        /// <summary>
        /// Upload the locally stored List to Azure
        /// </summary>
        private async Task UploadListToAzureAsync()
        {
            // Uploading a local file to the directory created above
            string listToString = string.Join(",", ShapeFactory.instance.shapeHistoryList.ToArray());

            await shapeIndexCloudFile.UploadTextAsync(listToString);
        }
    ```

5.  <span data-ttu-id="1c53f-519">Ajoutez une méthode pour récupérer le texte stocké dans le fichier situé dans votre *Azure stockage fichier* et *désérialiser* dans une liste.</span><span class="sxs-lookup"><span data-stu-id="1c53f-519">Add a method to retrieve the text stored in the file located in your *Azure Storage File* and *deserialize* it into a list.</span></span>

6.  <span data-ttu-id="1c53f-520">Une fois ce processus est terminé, la méthode réactive les regards afin que l’utilisateur peut ajouter plusieurs formes à la scène.</span><span class="sxs-lookup"><span data-stu-id="1c53f-520">Once this process is completed, the method re-enables the gaze so that the user can add more shapes to the scene.</span></span>

    ```csharp
        ///<summary>
        /// Get the List stored in Azure and use the data retrieved to replicate 
        /// a Shape creation pattern
        ///</summary>
        private async Task ReplicateListFromAzureAsync()
        {
            string azureTextFileContent = await shapeIndexCloudFile.DownloadTextAsync();

            string[] shapes = azureTextFileContent.Split(new char[] { ',' });

            foreach (string shape in shapes)
            {
                int i;

                Int32.TryParse(shape.ToString(), out i);

                ShapeFactory.instance.shapeHistoryList.Add(i);

                ShapeFactory.instance.CreateShape(i, true);

                await Task.Delay(500);
            }

            Gaze.instance.GazeEnabled = true;

            azureStatusText.text = "Load Complete!";
        }
    ```

7.  <span data-ttu-id="1c53f-521">Enregistrez vos modifications dans Visual Studio avant de retourner à Unity.</span><span class="sxs-lookup"><span data-stu-id="1c53f-521">Save your changes in Visual Studio before returning to Unity.</span></span>

## <a name="chapter-11---build-the-uwp-solution"></a><span data-ttu-id="1c53f-522">Chapitre 11 - générer la Solution UWP</span><span class="sxs-lookup"><span data-stu-id="1c53f-522">Chapter 11 - Build the UWP Solution</span></span>

<span data-ttu-id="1c53f-523">Pour commencer le processus de génération :</span><span class="sxs-lookup"><span data-stu-id="1c53f-523">To begin the Build process:</span></span>

1.  <span data-ttu-id="1c53f-524">Accédez à **fichier** > **les paramètres de génération**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-524">Go to **File** > **Build Settings**.</span></span>

    ![Générez l’application](images/AzureLabs-Lab5-54.png)

2.  <span data-ttu-id="1c53f-526">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-526">Click **Build**.</span></span> <span data-ttu-id="1c53f-527">Unity lancera un *Explorateur de fichiers* fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans.</span><span class="sxs-lookup"><span data-stu-id="1c53f-527">Unity will launch a *File Explorer* window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="1c53f-528">Créez ce dossier, puis nommez-le *application*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-528">Create that folder now, and name it *App*.</span></span> <span data-ttu-id="1c53f-529">Ensuite avec le *application* dossier sélectionné, appuyez sur **sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-529">Then with the *App* folder selected, press **Select Folder**.</span></span>

3.  <span data-ttu-id="1c53f-530">Unity commencera à générer votre projet pour le *application* dossier.</span><span class="sxs-lookup"><span data-stu-id="1c53f-530">Unity will begin building your project to the *App* folder.</span></span>

4.  <span data-ttu-id="1c53f-531">Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un *Explorateur de fichiers* fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).</span><span class="sxs-lookup"><span data-stu-id="1c53f-531">Once Unity has finished building (it might take some time), it will open a *File Explorer* window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

## <a name="chapter-12---deploying-your-application"></a><span data-ttu-id="1c53f-532">Chapitre 12 - déploiement de votre application</span><span class="sxs-lookup"><span data-stu-id="1c53f-532">Chapter 12 - Deploying your application</span></span>

<span data-ttu-id="1c53f-533">Pour déployer votre application :</span><span class="sxs-lookup"><span data-stu-id="1c53f-533">To deploy your application:</span></span>

1.  <span data-ttu-id="1c53f-534">Accédez à la *application* dossier qui a été créé dans le [dernier chapitre](#chapter-11---build-the-uwp-solution).</span><span class="sxs-lookup"><span data-stu-id="1c53f-534">Navigate to the *App* folder which was created in the [last Chapter](#chapter-11---build-the-uwp-solution).</span></span> <span data-ttu-id="1c53f-535">Vous verrez un fichier avec le nom de votre applications, avec l’extension de « .sln », vous devez double-cliquer sur, par conséquent, pour l’ouvrir dans *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="1c53f-535">You will see a file with your apps name, with the '.sln' extension, which you should double-click, so to open it within *Visual Studio*.</span></span>

2.  <span data-ttu-id="1c53f-536">Dans le **plateforme de Solution**, sélectionnez **x86, Local Machine**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-536">In the **Solution Platform**, select **x86, Local Machine**.</span></span>

3.  <span data-ttu-id="1c53f-537">Dans le **Configuration de la Solution** sélectionnez **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-537">In the **Solution Configuration** select **Debug**.</span></span>

    > <span data-ttu-id="1c53f-538">Pour le Microsoft HoloLens, il peut s’avérer plus facile d’affecter à ce *Machine distante*, de sorte que vous ne sont pas attachés à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1c53f-538">For the Microsoft HoloLens, you may find it easier to set this to *Remote Machine*, so that you are not tethered to your computer.</span></span> <span data-ttu-id="1c53f-539">Cependant, vous devez également effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1c53f-539">Though, you will need to also do the following:</span></span>
    > - <span data-ttu-id="1c53f-540">Connaître le **adresse IP** de votre HoloLens, ce qui se trouve dans le **paramètres** > **réseau & Internet**  >   **Wi-Fi** > **Options avancées**; IPv4 est l’adresse que vous devez utiliser.</span><span class="sxs-lookup"><span data-stu-id="1c53f-540">Know the **IP Address** of your HoloLens, which can be found within the **Settings** > **Network & Internet** > **Wi-Fi** > **Advanced Options**; the IPv4 is the address you should use.</span></span> 
    > - <span data-ttu-id="1c53f-541">Vérifiez **Mode développeur** est **sur**; trouvé dans **paramètres** > **mise à jour & sécurité**  >  **Pour les développeurs**.</span><span class="sxs-lookup"><span data-stu-id="1c53f-541">Ensure **Developer Mode** is **On**; found in **Settings** > **Update & Security** > **For developers**.</span></span>

    ![déployer la solution](images/AzureLabs-Lab5-55.png)

4.  <span data-ttu-id="1c53f-543">Accédez à la **Build** menu et cliquez sur **déployer la Solution** à chargement indépendant de l’application sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1c53f-543">Go to the **Build** menu and click on **Deploy Solution** to sideload the application to your machine.</span></span>

5.  <span data-ttu-id="1c53f-544">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancé et testé !</span><span class="sxs-lookup"><span data-stu-id="1c53f-544">Your App should now appear in the list of installed apps, ready to be launched and tested!</span></span>

## <a name="your-finished-azure-functions-and-storage-application"></a><span data-ttu-id="1c53f-545">Votre Azure Functions terminé et votre Application de stockage</span><span class="sxs-lookup"><span data-stu-id="1c53f-545">Your finished Azure Functions and Storage Application</span></span>

<span data-ttu-id="1c53f-546">Félicitations, vous avez créé une application de réalité mixte qui tire parti des services Azure Functions et de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="1c53f-546">Congratulations, you built a mixed reality app that leverages both the Azure Functions and Azure Storage services.</span></span> <span data-ttu-id="1c53f-547">Votre application sera en mesure de dessiner sur les données stockées et de fournir une action basée sur ces données.</span><span class="sxs-lookup"><span data-stu-id="1c53f-547">Your app will be able to draw on stored data, and provide an action based on that data.</span></span>

![produit final-fin](images/AzureLabs-Lab5-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="1c53f-549">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="1c53f-549">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="1c53f-550">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="1c53f-550">Exercise 1</span></span>

<span data-ttu-id="1c53f-551">Créer un deuxième spawn point et un enregistrement qui a qu'un objet a été créé à partir de spawn.</span><span class="sxs-lookup"><span data-stu-id="1c53f-551">Create a second spawn point and record which spawn point an object was created from.</span></span> <span data-ttu-id="1c53f-552">Lorsque vous chargez le fichier de données, relire les formes généré de façon dynamique à partir de l’emplacement qu’ils ont été créés à l’origine.</span><span class="sxs-lookup"><span data-stu-id="1c53f-552">When you load the data file, replay the shapes being spawned from the location they originally were created.</span></span>

### <a name="exercise-2"></a><span data-ttu-id="1c53f-553">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="1c53f-553">Exercise 2</span></span>

<span data-ttu-id="1c53f-554">Créer une méthode pour redémarrer l’application, plutôt que de devoir rouvrez ce dernier chaque fois.</span><span class="sxs-lookup"><span data-stu-id="1c53f-554">Create a way to restart the app, rather than having to re-open it each time.</span></span> <span data-ttu-id="1c53f-555">**Chargement des scènes** est un bon endroit pour démarrer.</span><span class="sxs-lookup"><span data-stu-id="1c53f-555">**Loading Scenes** is a good spot to start.</span></span> <span data-ttu-id="1c53f-556">Après cela, créez une méthode pour effacer la liste stockée dans *stockage Azure*, ce qui peut être facilement réinitialisé à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="1c53f-556">After doing that, create a way to clear the stored list in *Azure Storage*, so that it can be easily reset from your app.</span></span> 
