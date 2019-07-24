---
title: RM et Azure 305-fonctions et stockage
description: Suivez ce cours pour apprendre à implémenter le stockage Azure et les fonctions dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Académie, Unity, didacticiel, API, fonctions, stockage, hololens, immersif, VR
ms.openlocfilehash: 5f3d0c6990249bc32e4c0f55c72dd884c4c2214e
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694557"
---
>[!NOTE]
><span data-ttu-id="016a3-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="016a3-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="016a3-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="016a3-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="016a3-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="016a3-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="016a3-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="016a3-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="016a3-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="016a3-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="016a3-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="016a3-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br> 

# <a name="mr-and-azure-305-functions-and-storage"></a><span data-ttu-id="016a3-110">MR et Azure 305: Fonctions et stockage</span><span class="sxs-lookup"><span data-stu-id="016a3-110">MR and Azure 305: Functions and storage</span></span>

![produit final-début](images/AzureLabs-Lab5-00.png)

<span data-ttu-id="016a3-112">Dans ce cours, vous allez apprendre à créer et à utiliser des Azure Functions et à stocker des données avec une ressource de stockage Azure, au sein d’une application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="016a3-112">In this course, you will learn how to create and use Azure Functions and store data with an Azure Storage resource, within a mixed reality application.</span></span>

<span data-ttu-id="016a3-113">*Azure Functions* est un service Microsoft, qui permet aux développeurs d’exécuter de petits morceaux de code, «functions», dans Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-113">*Azure Functions* is a Microsoft service, which allows developers to run small pieces of code, 'functions', in Azure.</span></span> <span data-ttu-id="016a3-114">Cela permet de déléguer le travail au Cloud, plutôt qu’à votre application locale, ce qui peut avoir de nombreux avantages.</span><span class="sxs-lookup"><span data-stu-id="016a3-114">This provides a way to delegate work to the cloud, rather than your local application, which can have many benefits.</span></span> <span data-ttu-id="016a3-115">*Azure Functions* prend en charge plusieurs langages de\#développement,\#notamment C, F, node. js, Java et php.</span><span class="sxs-lookup"><span data-stu-id="016a3-115">*Azure Functions* supports several development languages, including C\#, F\#, Node.js, Java, and PHP.</span></span> <span data-ttu-id="016a3-116">Pour plus d’informations, consultez l' [article Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span><span class="sxs-lookup"><span data-stu-id="016a3-116">For more information, visit the [Azure Functions article](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span></span>

<span data-ttu-id="016a3-117">Le *stockage Azure* est un service Cloud Microsoft qui permet aux développeurs de stocker des données, avec l’assurance qu’elles seront hautement disponibles, sécurisées, durables, évolutives et redondantes.</span><span class="sxs-lookup"><span data-stu-id="016a3-117">*Azure Storage* is a Microsoft cloud service, which allows developers to store data, with the insurance that it will be highly available, secure, durable, scalable, and redundant.</span></span> <span data-ttu-id="016a3-118">Cela signifie que Microsoft traitera toutes les tâches de maintenance et les problèmes critiques pour vous.</span><span class="sxs-lookup"><span data-stu-id="016a3-118">This means Microsoft will handle all maintenance, and critical problems for you.</span></span> <span data-ttu-id="016a3-119">Pour plus d’informations, consultez l' [article stockage Azure](https://docs.microsoft.com/azure/storage/common/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="016a3-119">For more information, visit the [Azure Storage article](https://docs.microsoft.com/azure/storage/common/storage-introduction).</span></span>

<span data-ttu-id="016a3-120">Une fois ce cours terminé, vous disposerez d’une application de casque immersif en réalité mixte, qui sera en mesure d’effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="016a3-120">Having completed this course, you will have a mixed reality immersive headset application which will be able to do the following:</span></span>

1.  <span data-ttu-id="016a3-121">Permet à l’utilisateur de faire un regard sur une scène.</span><span class="sxs-lookup"><span data-stu-id="016a3-121">Allow the user to gaze around a scene.</span></span>
2.  <span data-ttu-id="016a3-122">Déclencher la génération d’objets quand l’utilisateur passe d’un «bouton» en 3D.</span><span class="sxs-lookup"><span data-stu-id="016a3-122">Trigger the spawning of objects when the user gazes at a 3D 'button'.</span></span>
3.  <span data-ttu-id="016a3-123">Les objets générés sont choisis par une fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-123">The spawned objects will be chosen by an Azure Function.</span></span>
4.  <span data-ttu-id="016a3-124">À mesure que chaque objet est généré, l’application stocke le type d’objet dans un *fichier Azure*, situé dans le *stockage Azure*.</span><span class="sxs-lookup"><span data-stu-id="016a3-124">As each object is spawned, the application will store the object type in an *Azure File*, located in *Azure Storage*.</span></span>
5.  <span data-ttu-id="016a3-125">Lors du chargement d’une deuxième fois, les données du *fichier Azure* sont récupérées et utilisées pour relire les actions de génération à partir de l’instance précédente de l’application.</span><span class="sxs-lookup"><span data-stu-id="016a3-125">Upon loading a second time, the *Azure File* data will be retrieved, and used to replay the spawning actions from the previous instance of the application.</span></span>

<span data-ttu-id="016a3-126">Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception.</span><span class="sxs-lookup"><span data-stu-id="016a3-126">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="016a3-127">Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="016a3-127">This course is designed to teach you how to integrate an Azure Service with your Unity Project.</span></span> <span data-ttu-id="016a3-128">C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="016a3-128">It is your job to use the knowledge you gain from this course to enhance your mixed reality Application.</span></span>

## <a name="device-support"></a><span data-ttu-id="016a3-129">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="016a3-129">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="016a3-130">Course</span><span class="sxs-lookup"><span data-stu-id="016a3-130">Course</span></span></th><th style="width:150px"> <span data-ttu-id="016a3-131"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="016a3-131"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="016a3-132"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="016a3-132"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="016a3-133">MR et Azure 305: Fonctions et stockage</span><span class="sxs-lookup"><span data-stu-id="016a3-133">MR and Azure 305: Functions and storage</span></span></td><td style="text-align: center;"> <span data-ttu-id="016a3-134">✔️</span><span class="sxs-lookup"><span data-stu-id="016a3-134">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="016a3-135">✔️</span><span class="sxs-lookup"><span data-stu-id="016a3-135">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="016a3-136">Bien que ce cours se concentre principalement sur les casques de Windows Mixed Reality (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours à Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="016a3-136">While this course primarily focuses on Windows Mixed Reality immersive (VR) headsets, you can also apply what you learn in this course to Microsoft HoloLens.</span></span> <span data-ttu-id="016a3-137">À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge HoloLens.</span><span class="sxs-lookup"><span data-stu-id="016a3-137">As you follow along with the course, you will see notes on any changes you might need to employ to support HoloLens.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="016a3-138">Prérequis</span><span class="sxs-lookup"><span data-stu-id="016a3-138">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="016a3-139">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="016a3-139">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="016a3-140">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="016a3-140">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="016a3-141">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="016a3-141">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="016a3-142">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:</span><span class="sxs-lookup"><span data-stu-id="016a3-142">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="016a3-143">Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)</span><span class="sxs-lookup"><span data-stu-id="016a3-143">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="016a3-144">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="016a3-144">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="016a3-145">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="016a3-145">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="016a3-146">Unity 2017,4</span><span class="sxs-lookup"><span data-stu-id="016a3-146">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="016a3-147">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="016a3-147">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="016a3-148">Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="016a3-148">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="016a3-149">Abonnement à un compte Azure pour la création de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="016a3-149">A subscription to an Azure account for creating Azure resources</span></span>
- <span data-ttu-id="016a3-150">Accès Internet pour l’installation d’Azure et la récupération de données</span><span class="sxs-lookup"><span data-stu-id="016a3-150">Internet access for Azure setup and data retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="016a3-151">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="016a3-151">Before you start</span></span>

<span data-ttu-id="016a3-152">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="016a3-152">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>

## <a name="chapter-1---the-azure-portal"></a><span data-ttu-id="016a3-153">Chapitre 1-portail Azure</span><span class="sxs-lookup"><span data-stu-id="016a3-153">Chapter 1 - The Azure Portal</span></span>

<span data-ttu-id="016a3-154">Pour utiliser le **service de stockage Azure**, vous devez créer et configurer un **compte de stockage** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-154">To use the **Azure Storage Service**, you will need to create and configure a **Storage Account** in the Azure portal.</span></span>

1.  <span data-ttu-id="016a3-155">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="016a3-155">Log in to the  [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE]
    > <span data-ttu-id="016a3-156">Si vous n’avez pas encore de compte Azure, vous devez en créer un.</span><span class="sxs-lookup"><span data-stu-id="016a3-156">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="016a3-157">Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="016a3-157">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="016a3-158">Une fois que vous êtes connecté, cliquez sur **nouveau** dans l’angle supérieur gauche et recherchez *compte de stockage*, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="016a3-158">Once you are logged in, click on **New** in the top left corner, and search for *Storage account*, and click **Enter**.</span></span>

    ![recherche Azure Storage](images/AzureLabs-Lab5-01.png)

    > [!NOTE]
    > <span data-ttu-id="016a3-160">Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.</span><span class="sxs-lookup"><span data-stu-id="016a3-160">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

3.  <span data-ttu-id="016a3-161">La nouvelle page fournit une description du service de *compte de stockage Azure* .</span><span class="sxs-lookup"><span data-stu-id="016a3-161">The new page will provide a description of the *Azure Storage account* service.</span></span> <span data-ttu-id="016a3-162">En bas à gauche de cette invite, sélectionnez le bouton **créer** pour créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="016a3-162">At the bottom left of this prompt, select the **Create** button, to create an association with this service.</span></span>

    ![créer un service](images/AzureLabs-Lab5-02.png)

4.  <span data-ttu-id="016a3-164">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="016a3-164">Once you have clicked on **Create**:</span></span>

    1.  <span data-ttu-id="016a3-165">Insérez un *nom* pour votre compte. n’oubliez pas que ce champ accepte uniquement des chiffres et des lettres minuscules.</span><span class="sxs-lookup"><span data-stu-id="016a3-165">Insert a *Name* for your account, be aware this field only accepts numbers, and lowercase letters.</span></span>

    2.  <span data-ttu-id="016a3-166">Pour *modèle de déploiement*, sélectionnez Resource **Manager**.</span><span class="sxs-lookup"><span data-stu-id="016a3-166">For *Deployment model*, select **Resource manager**.</span></span>

    3.  <span data-ttu-id="016a3-167">Pour *type de compte*, sélectionnez **stockage (à usage général v1)** .</span><span class="sxs-lookup"><span data-stu-id="016a3-167">For *Account kind*, select **Storage (general purpose v1)**.</span></span>

    4.  <span data-ttu-id="016a3-168">Déterminez l' *emplacement* de votre groupe de ressources (si vous créez un groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="016a3-168">Determine the *Location* for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="016a3-169">L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait.</span><span class="sxs-lookup"><span data-stu-id="016a3-169">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="016a3-170">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="016a3-170">Some Azure assets are only available in certain regions.</span></span>

    5.  <span data-ttu-id="016a3-171">Pour *la réplication* , sélectionnez **Read-Access-géo-redondant Storage (RA-GRS)** .</span><span class="sxs-lookup"><span data-stu-id="016a3-171">For *Replication* select **Read-access-geo-redundant storage (RA-GRS)**.</span></span>

    6.  <span data-ttu-id="016a3-172">Pour *performances*, sélectionnez **standard**.</span><span class="sxs-lookup"><span data-stu-id="016a3-172">For *Performance*, select **Standard**.</span></span>

    7.  <span data-ttu-id="016a3-173">Laissez le *transfert sécurisé requis* comme **désactivé**.</span><span class="sxs-lookup"><span data-stu-id="016a3-173">Leave *Secure transfer required* as **Disabled**.</span></span>

    8.  <span data-ttu-id="016a3-174">Sélectionnez un *abonnement*.</span><span class="sxs-lookup"><span data-stu-id="016a3-174">Select a *Subscription*.</span></span>

    9. <span data-ttu-id="016a3-175">Choisissez un *groupe de ressources* ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="016a3-175">Choose a *Resource Group* or create a new one.</span></span> <span data-ttu-id="016a3-176">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-176">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="016a3-177">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun).</span><span class="sxs-lookup"><span data-stu-id="016a3-177">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span> 

        > <span data-ttu-id="016a3-178">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="016a3-178">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    10. <span data-ttu-id="016a3-179">Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.</span><span class="sxs-lookup"><span data-stu-id="016a3-179">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    11. <span data-ttu-id="016a3-180">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="016a3-180">Select **Create**.</span></span>

        ![informations sur le service d’entrée](images/AzureLabs-Lab5-03.png)

5.  <span data-ttu-id="016a3-182">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="016a3-182">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

6.  <span data-ttu-id="016a3-183">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="016a3-183">A notification will appear in the portal once the Service instance is created.</span></span>

    ![nouvelle notification dans le portail Azure](images/AzureLabs-Lab5-04.png)

7.  <span data-ttu-id="016a3-185">Cliquez sur les notifications pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="016a3-185">Click on the notifications to explore your new Service instance.</span></span>

    ![Accéder à la ressource](images/AzureLabs-Lab5-05.png)

8.  <span data-ttu-id="016a3-187">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="016a3-187">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="016a3-188">Vous êtes dirigé vers votre nouvelle instance de service de *compte de stockage* .</span><span class="sxs-lookup"><span data-stu-id="016a3-188">You will be taken to your new *Storage account* service instance.</span></span>

    ![clés d'accès](images/AzureLabs-Lab5-06.png)

9.  <span data-ttu-id="016a3-190">Cliquez sur *clés d’accès*pour afficher les points de terminaison de ce service Cloud.</span><span class="sxs-lookup"><span data-stu-id="016a3-190">Click *Access keys*, to reveal the endpoints for this cloud service.</span></span> <span data-ttu-id="016a3-191">Utilisez *le bloc-notes* ou une version similaire pour copier l’une de vos clés pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="016a3-191">Use *Notepad* or similar, to copy one of your keys for use later.</span></span> <span data-ttu-id="016a3-192">Notez également la valeur de la *chaîne de connexion* , car elle sera utilisée dans la classe *AzureServices* , que vous allez créer ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="016a3-192">Also, note the *Connection string* value, as it will be used in the *AzureServices* class, which you will create later.</span></span>

    ![copier la chaîne de connexion](images/AzureLabs-Lab5-07.png)

## <a name="chapter-2---setting-up-an-azure-function"></a><span data-ttu-id="016a3-194">Chapitre 2-Configuration d’une fonction Azure</span><span class="sxs-lookup"><span data-stu-id="016a3-194">Chapter 2 - Setting up an Azure Function</span></span>

<span data-ttu-id="016a3-195">Vous allez maintenant écrire une  **fonction** Azure dans le service Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-195">You will now write an **Azure** **Function** in the Azure Service.</span></span>

<span data-ttu-id="016a3-196">Vous pouvez utiliser une **fonction Azure** pour effectuer presque tout ce que vous feriez avec une fonction classique dans votre code, à la différence que cette fonction est accessible par n’importe quelle application disposant d’informations d’identification pour accéder à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-196">You can use an **Azure Function** to do nearly anything that you would do with a classic function in your code, the difference being that this function can be accessed by any application that has credentials to access your Azure Account.</span></span>

<span data-ttu-id="016a3-197">Pour créer une fonction Azure:</span><span class="sxs-lookup"><span data-stu-id="016a3-197">To create an Azure Function:</span></span>

1.  <span data-ttu-id="016a3-198">À partir de votre *portail Azure*, cliquez sur **nouveau** dans l’angle supérieur gauche, recherchez *Function App*, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="016a3-198">From your *Azure Portal*, click on **New** in the top left corner, and search for *Function App*, and click **Enter**.</span></span>

    ![créer une application de fonction](images/AzureLabs-Lab5-08.png)

    > [!NOTE]
    > <span data-ttu-id="016a3-200">Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.</span><span class="sxs-lookup"><span data-stu-id="016a3-200">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

2.  <span data-ttu-id="016a3-201">La nouvelle page fournit une description du service *Azure Function App* .</span><span class="sxs-lookup"><span data-stu-id="016a3-201">The new page will provide a description of the *Azure Function App* service.</span></span> <span data-ttu-id="016a3-202">En bas à gauche de cette invite, sélectionnez le bouton **créer** pour créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="016a3-202">At the bottom left of this prompt, select the **Create** button, to create an association with this service.</span></span>

    ![informations sur l’application de fonction](images/AzureLabs-Lab5-09.png)

3.  <span data-ttu-id="016a3-204">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="016a3-204">Once you have clicked on **Create**:</span></span>

    1.  <span data-ttu-id="016a3-205">Fournissez un *nom d’application*.</span><span class="sxs-lookup"><span data-stu-id="016a3-205">Provide an *App name*.</span></span> <span data-ttu-id="016a3-206">Seuls des lettres et des chiffres peuvent être utilisés ici (majuscules ou minuscules).</span><span class="sxs-lookup"><span data-stu-id="016a3-206">Only letters and numbers can be used here (either upper or lower case is allowed).</span></span>

    2.  <span data-ttu-id="016a3-207">Sélectionnez votre *abonnement*préféré.</span><span class="sxs-lookup"><span data-stu-id="016a3-207">Select your preferred *Subscription*.</span></span>

    3. <span data-ttu-id="016a3-208">Choisissez un *groupe de ressources* ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="016a3-208">Choose a *Resource Group* or create a new one.</span></span> <span data-ttu-id="016a3-209">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-209">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="016a3-210">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun).</span><span class="sxs-lookup"><span data-stu-id="016a3-210">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span> 

        > <span data-ttu-id="016a3-211">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="016a3-211">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    4.  <span data-ttu-id="016a3-212">Pour cet exercice, sélectionnez *Windows* comme **système d’exploitation**choisi.</span><span class="sxs-lookup"><span data-stu-id="016a3-212">For this exercise, select *Windows* as the chosen **OS**.</span></span>

    5.  <span data-ttu-id="016a3-213">Sélectionnez le *plan de consommation* pour le plan d' **hébergement**.</span><span class="sxs-lookup"><span data-stu-id="016a3-213">Select *Consumption Plan* for the **Hosting Plan**.</span></span>

    6.  <span data-ttu-id="016a3-214">Déterminez l' *emplacement* de votre groupe de ressources (si vous créez un groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="016a3-214">Determine the *Location* for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="016a3-215">L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait.</span><span class="sxs-lookup"><span data-stu-id="016a3-215">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="016a3-216">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="016a3-216">Some Azure assets are only available in certain regions.</span></span> <span data-ttu-id="016a3-217">Pour des performances optimales, sélectionnez la même région que le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="016a3-217">For optimal performance, select the same region as the storage account.</span></span>

    7.  <span data-ttu-id="016a3-218">Pour *stockage*, sélectionnez **utiliser l’existant**, puis dans le menu déroulant, recherchez votre stockage créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="016a3-218">For *Storage*, select **Use existing**, and then using the dropdown menu, find your previously created storage.</span></span>

    8.  <span data-ttu-id="016a3-219">Laissez *application Insights* désactivés pour cet exercice.</span><span class="sxs-lookup"><span data-stu-id="016a3-219">Leave *Application Insights* off for this exercise.</span></span>

        ![Détails de l’application de fonction d’entrée](images/AzureLabs-Lab5-10.png)

4.  <span data-ttu-id="016a3-221">Cliquez sur le bouton **Créer**.</span><span class="sxs-lookup"><span data-stu-id="016a3-221">Click the **Create** button.</span></span>

5.  <span data-ttu-id="016a3-222">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="016a3-222">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

6.  <span data-ttu-id="016a3-223">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="016a3-223">A notification will appear in the portal once the Service instance is created.</span></span>

    ![nouvelle notification du portail Azure](images/AzureLabs-Lab5-11.png)

7.  <span data-ttu-id="016a3-225">Cliquez sur les notifications pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="016a3-225">Click on the notifications to explore your new Service instance.</span></span> 

    ![accéder à l’application de fonction de ressource](images/AzureLabs-Lab5-12.png)

8.  <span data-ttu-id="016a3-227">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="016a3-227">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="016a3-228">Vous êtes dirigé vers votre nouvelle instance de service *Function App* .</span><span class="sxs-lookup"><span data-stu-id="016a3-228">You will be taken to your new *Function App* service instance.</span></span>

9.  <span data-ttu-id="016a3-229">Dans le tableau de bord *Function App* , pointez avec la souris sur *fonctions*, situées dans le panneau de gauche, puis cliquez sur le symbole **+ (plus)** .</span><span class="sxs-lookup"><span data-stu-id="016a3-229">On the *Function App* dashboard, hover your mouse over *Functions*, found within the panel on the left, and then click the **+ (plus)** symbol.</span></span>

    ![créer une nouvelle fonction](images/AzureLabs-Lab5-13.png)

10. <span data-ttu-id="016a3-231">Dans la page suivante, vérifiez que **webhook + API** est sélectionné, et pour *choisir une langue,* sélectionnez **CSharp**, car il s’agit de la langue utilisée pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="016a3-231">On the next page, ensure **Webhook + API** is selected, and for *Choose a language,* select **CSharp**, as this will be the language used for this tutorial.</span></span> <span data-ttu-id="016a3-232">Enfin, cliquez sur le bouton **créer cette fonction** .</span><span class="sxs-lookup"><span data-stu-id="016a3-232">Lastly, click the **Create this function** button.</span></span>

    ![sélectionner le Web Hook CSharp](images/AzureLabs-Lab5-14.png)

11. <span data-ttu-id="016a3-234">Vous devez être dirigé vers la page de codes (Run. CSX). si ce n’est pas le cas, cliquez sur la fonction nouvellement créée dans la liste fonctions du volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="016a3-234">You should be taken to the code page (run.csx), if not though, click on the newly created Function in the Functions list within the panel on the left.</span></span>

    ![ouvrir une nouvelle fonction](images/AzureLabs-Lab5-15.png)

12. <span data-ttu-id="016a3-236">Copiez le code suivant dans votre fonction.</span><span class="sxs-lookup"><span data-stu-id="016a3-236">Copy the following code into your function.</span></span> <span data-ttu-id="016a3-237">Cette fonction retourne simplement un entier aléatoire compris entre 0 et 2 lorsqu’elle est appelée.</span><span class="sxs-lookup"><span data-stu-id="016a3-237">This function will simply return a random integer between 0 and 2 when called.</span></span> <span data-ttu-id="016a3-238">Ne vous inquiétez pas du code existant, n’hésitez pas à le coller en haut de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="016a3-238">Do not worry about the existing code, feel free to paste over the top of it.</span></span>

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

13. <span data-ttu-id="016a3-239">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="016a3-239">Select **Save**.</span></span>

14. <span data-ttu-id="016a3-240">Le résultat doit ressembler à l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="016a3-240">The result should look like the image below.</span></span>

15. <span data-ttu-id="016a3-241">Cliquez sur l’URL de la **fonction d’extraction** et prenez note du point de *terminaison* affiché.</span><span class="sxs-lookup"><span data-stu-id="016a3-241">Click on **Get function URL** and take note of the *endpoint* displayed.</span></span> <span data-ttu-id="016a3-242">Vous devez l’insérer dans la classe *AzureServices* que vous allez créer plus loin dans ce cours.</span><span class="sxs-lookup"><span data-stu-id="016a3-242">You will need to insert it into the *AzureServices* class that you will create later in this course.</span></span>

    ![Obtient le point de terminaison de fonction](images/AzureLabs-Lab5-16.png)

    ![Obtient le point de terminaison de fonction](images/AzureLabs-Lab5-16-5.png)

## <a name="chapter-3---setting-up-the-unity-project"></a><span data-ttu-id="016a3-245">Chapitre 3-Configuration du projet Unity</span><span class="sxs-lookup"><span data-stu-id="016a3-245">Chapter 3 - Setting up the Unity project</span></span>

<span data-ttu-id="016a3-246">Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="016a3-246">The following is a typical set up for developing with Mixed Reality, and as such, is a good template for other projects.</span></span>

<span data-ttu-id="016a3-247">Configurez et testez votre casque immersif en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="016a3-247">Set up and test your mixed reality immersive headset.</span></span>

> [!NOTE]
> <span data-ttu-id="016a3-248">Vous n’aurez **pas** besoin de contrôleurs de mouvement pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="016a3-248">You will **not** require Motion Controllers for this course.</span></span> <span data-ttu-id="016a3-249">Si vous avez besoin de la prise en charge de la configuration du casque immersif, consultez [l’article Configuration de la réalité mixte](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span><span class="sxs-lookup"><span data-stu-id="016a3-249">If you need support setting up the immersive headset, please [visit the mixed reality set up article](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span></span>

1.  <span data-ttu-id="016a3-250">Ouvrez Unity et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="016a3-250">Open Unity and click **New**.</span></span>

    ![créer un projet Unity](images/AzureLabs-Lab5-17.png)

2.  <span data-ttu-id="016a3-252">Vous devez maintenant fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="016a3-252">You will now need to provide a Unity Project name.</span></span> <span data-ttu-id="016a3-253">Insérez **MR_Azure_Functions**.</span><span class="sxs-lookup"><span data-stu-id="016a3-253">Insert **MR_Azure_Functions**.</span></span> <span data-ttu-id="016a3-254">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="016a3-254">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="016a3-255">Définissez l' *emplacement* approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés).</span><span class="sxs-lookup"><span data-stu-id="016a3-255">Set the *Location* to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="016a3-256">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="016a3-256">Then, click **Create project**.</span></span>

    ![Donnez un nom au nouveau projet Unity](images/AzureLabs-Lab5-18.png)

3.  <span data-ttu-id="016a3-258">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="016a3-258">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="016a3-259">Accédez à **modifier** > les**Préférences** , puis à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="016a3-259">Go to **Edit** > **Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="016a3-260">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="016a3-260">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="016a3-261">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="016a3-261">Close the **Preferences** window.</span></span>

    ![définir Visual Studio comme éditeur de script](images/AzureLabs-Lab5-19.png)

4.  <span data-ttu-id="016a3-263">Ensuite, accédez à **fichier** > **paramètres de build** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton **changer de plateforme** .</span><span class="sxs-lookup"><span data-stu-id="016a3-263">Next, go to **File** > **Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

    ![basculer la plateforme sur UWP](images/AzureLabs-Lab5-20.png)

5.  <span data-ttu-id="016a3-265">Accédez à **fichier** > **paramètres de build** et assurez-vous que:</span><span class="sxs-lookup"><span data-stu-id="016a3-265">Go to **File** > **Build Settings** and make sure that:</span></span>

    1. <span data-ttu-id="016a3-266">L' **appareil cible** est défini sur **n’importe quel appareil**.</span><span class="sxs-lookup"><span data-stu-id="016a3-266">**Target Device** is set to **Any Device**.</span></span>

        > <span data-ttu-id="016a3-267">Pour Microsoft HoloLens, définissez **appareil cible** sur *HoloLens*.</span><span class="sxs-lookup"><span data-stu-id="016a3-267">For Microsoft HoloLens, set **Target Device** to *HoloLens*.</span></span>

    2. <span data-ttu-id="016a3-268">Le **type de build** est **D3D**</span><span class="sxs-lookup"><span data-stu-id="016a3-268">**Build Type** is set to **D3D**</span></span>

    3. <span data-ttu-id="016a3-269">Le **SDK** est configuré sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="016a3-269">**SDK** is set to **Latest installed**</span></span>

    4. <span data-ttu-id="016a3-270">**Version de Visual Studio** définie sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="016a3-270">**Visual Studio Version** is set to **Latest installed**</span></span>

    5. <span data-ttu-id="016a3-271">La **génération et l’exécution** sont définies sur l' **ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="016a3-271">**Build and Run** is set to **Local Machine**</span></span>

    6. <span data-ttu-id="016a3-272">Enregistrez la scène et ajoutez-la à la Build.</span><span class="sxs-lookup"><span data-stu-id="016a3-272">Save the scene and add it to the build.</span></span>

        1.  <span data-ttu-id="016a3-273">Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="016a3-273">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="016a3-274">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="016a3-274">A save window will appear.</span></span>

            ![Ajouter des scènes ouvertes](images/AzureLabs-Lab5-21.png)

        2.  <span data-ttu-id="016a3-276">Créez un dossier pour cela, ainsi que toute nouvelle scène, puis sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez- le Scenes.</span><span class="sxs-lookup"><span data-stu-id="016a3-276">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![créer un dossier de scènes](images/AzureLabs-Lab5-22.png)

        3.  <span data-ttu-id="016a3-278">Ouvrez le dossier scenes nouvellement créé, puis dans le champ **nom de fichier:** , tapez **FunctionsScene**, puis cliquez sur  **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="016a3-278">Open your newly created **Scenes** folder, and then in the **File name:** text field, type **FunctionsScene**, then press **Save**.</span></span>

            ![enregistrer les fonctions, scène](images/AzureLabs-Lab5-23.png)

6.  <span data-ttu-id="016a3-280">Les paramètres restants, dans **paramètres de build**, doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="016a3-280">The remaining settings, in **Build Settings**, should be left as default for now.</span></span>

    ![enregistrer les fonctions, scène](images/AzureLabs-Lab5-24.png)

7.  <span data-ttu-id="016a3-282">Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* .</span><span class="sxs-lookup"><span data-stu-id="016a3-282">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span>

    ![paramètres du lecteur dans Inspector](images/AzureLabs-Lab5-25.png)

8.  <span data-ttu-id="016a3-284">Dans ce volet, quelques paramètres doivent être vérifiés:</span><span class="sxs-lookup"><span data-stu-id="016a3-284">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="016a3-285">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="016a3-285">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="016a3-286">La **version du runtime de script** doit être **expérimentale** (.net 4,6 équivalent), ce qui déclenche la nécessité de redémarrer l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="016a3-286">**Scripting Runtime Version** should be **Experimental** (.NET 4.6 Equivalent), which will trigger a need to restart the Editor.</span></span>
        2.  <span data-ttu-id="016a3-287">Le **backend de script** doit être **.net**</span><span class="sxs-lookup"><span data-stu-id="016a3-287">**Scripting Backend** should be **.NET**</span></span>
        3.  <span data-ttu-id="016a3-288">Le **niveau de compatibilité** de l’API doit être **.net 4,6**</span><span class="sxs-lookup"><span data-stu-id="016a3-288">**API Compatibility Level** should be **.NET 4.6**</span></span>

    2.  <span data-ttu-id="016a3-289">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:</span><span class="sxs-lookup"><span data-stu-id="016a3-289">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>
        
        -  <span data-ttu-id="016a3-290">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="016a3-290">**InternetClient**</span></span>

            ![définir les fonctionnalités](images/AzureLabs-Lab5-26.png)

    3.  <span data-ttu-id="016a3-292">Plus bas dans le panneau, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="016a3-292">Further down the panel, in **XR Settings** (found below **Publishing Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![définir les paramètres XR](images/AzureLabs-Lab5-27.png)

9.  <span data-ttu-id="016a3-294">De retour dans les *paramètres de build* , les *projets C# Unity* ne sont plus grisés. Cochez la case en regard de cette option.</span><span class="sxs-lookup"><span data-stu-id="016a3-294">Back in *Build Settings* *Unity C# Projects* is no longer greyed out; tick the checkbox next to this.</span></span>

    ![Tick (projets c#)](images/AzureLabs-Lab5-28.png)

10.  <span data-ttu-id="016a3-296">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="016a3-296">Close the Build Settings window.</span></span>

11. <span data-ttu-id="016a3-297">Enregistrez votre scène et votre projet (**fichier** > **Save Scene/file** > **Save Project**).</span><span class="sxs-lookup"><span data-stu-id="016a3-297">Save your Scene and Project (**FILE** > **SAVE SCENE / FILE** > **SAVE PROJECT**).</span></span>

## <a name="chapter-4---setup-main-camera"></a><span data-ttu-id="016a3-298">Chapitre 4-configurer l’appareil photo principal</span><span class="sxs-lookup"><span data-stu-id="016a3-298">Chapter 4 - Setup Main Camera</span></span>

> [!IMPORTANT]
> <span data-ttu-id="016a3-299">Si vous souhaitez ignorer les composants de la *configuration Unity* de ce cours et continuer directement dans le code, n’hésitez pas à [Télécharger ce fichier. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20305%20-%20Functions%20and%20storage/Azure-MR-305.unitypackage)et à l’importer dans votre projet en tant que [package personnalisé](https://docs.unity3d.com/Manual/AssetPackages.html).</span><span class="sxs-lookup"><span data-stu-id="016a3-299">If you wish to skip the *Unity Set up* components of this course, and continue straight into code, feel free to [download this .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20305%20-%20Functions%20and%20storage/Azure-MR-305.unitypackage), and import it into your project as a [Custom Package](https://docs.unity3d.com/Manual/AssetPackages.html).</span></span> <span data-ttu-id="016a3-300">Elle contient également les dll du chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="016a3-300">This will also contain the DLLs from the next Chapter.</span></span> <span data-ttu-id="016a3-301">Après l’importation, passez [au chapitre 7](#chapter-7---create-the-azureservices-class).</span><span class="sxs-lookup"><span data-stu-id="016a3-301">After import, continue from [Chapter 7](#chapter-7---create-the-azureservices-class).</span></span> 

1.  <span data-ttu-id="016a3-302">Dans le *volet hiérarchie*, vous trouverez un objet appelé **caméra principale**, cet objet représente le point de vue «Head» une fois que vous êtes «dans» votre application.</span><span class="sxs-lookup"><span data-stu-id="016a3-302">In the *Hierarchy Panel*, you will find an object called **Main Camera**, this object represents your "head" point of view once you are "inside" your application.</span></span>

2.  <span data-ttu-id="016a3-303">Avec le tableau de bord Unity devant vous, sélectionnez la **caméra principale gameobject**.</span><span class="sxs-lookup"><span data-stu-id="016a3-303">With the Unity Dashboard in front of you, select the **Main Camera GameObject**.</span></span> <span data-ttu-id="016a3-304">Vous remarquerez que le *panneau Inspecteur* (généralement situé à droite dans le tableau de bord) affichera les différents composants de ce *gameobject*, avec la *transformation* en haut, suivi de l' *appareil photo*et d’autres composants.</span><span class="sxs-lookup"><span data-stu-id="016a3-304">You will notice that the *Inspector Panel* (generally found to the right, within the Dashboard) will show the various components of that *GameObject*, with *Transform* at the top, followed by *Camera*, and some other components.</span></span> <span data-ttu-id="016a3-305">Vous devez réinitialiser la transformation de la caméra principale, afin qu’elle soit positionnée correctement.</span><span class="sxs-lookup"><span data-stu-id="016a3-305">You will need to reset the Transform of the Main Camera, so it is positioned correctly.</span></span>

3.  <span data-ttu-id="016a3-306">Pour ce faire, sélectionnez l’icône d' **engrenage** en regard du composant *transformer* de l’appareil photo, puis sélectionnez **Réinitialiser**.</span><span class="sxs-lookup"><span data-stu-id="016a3-306">To do this, select the **Gear** icon next to the Camera's *Transform* component, and select **Reset**.</span></span>

    ![réinitialiser la transformation](images/AzureLabs-Lab5-29.png)

4.  <span data-ttu-id="016a3-308">Ensuite, mettez à jour le composant **transformer** pour qu’il ressemble à ce qui suit:</span><span class="sxs-lookup"><span data-stu-id="016a3-308">Then update the **Transform** component to look like:</span></span>

    |         |    <span data-ttu-id="016a3-309">TRANSFORMATION-POSITION</span><span class="sxs-lookup"><span data-stu-id="016a3-309">TRANSFORM - POSITION</span></span>   |       |
    | :-----: | :-----------------------: | :----:|
    | <span data-ttu-id="016a3-310">**X**</span><span class="sxs-lookup"><span data-stu-id="016a3-310">**X**</span></span>   | <span data-ttu-id="016a3-311">**Y**</span><span class="sxs-lookup"><span data-stu-id="016a3-311">**Y**</span></span>                     | <span data-ttu-id="016a3-312">**Z**</span><span class="sxs-lookup"><span data-stu-id="016a3-312">**Z**</span></span> |
    | <span data-ttu-id="016a3-313">0</span><span class="sxs-lookup"><span data-stu-id="016a3-313">0</span></span>       | <span data-ttu-id="016a3-314">1</span><span class="sxs-lookup"><span data-stu-id="016a3-314">1</span></span>                         | <span data-ttu-id="016a3-315">0</span><span class="sxs-lookup"><span data-stu-id="016a3-315">0</span></span>     |    

    |       | <span data-ttu-id="016a3-316">TRANSFORMATION-ROTATION</span><span class="sxs-lookup"><span data-stu-id="016a3-316">TRANSFORM - ROTATION</span></span> |       |
    | :---: | :------------------: | :----:|
    | <span data-ttu-id="016a3-317">**X**</span><span class="sxs-lookup"><span data-stu-id="016a3-317">**X**</span></span> | <span data-ttu-id="016a3-318">**Y**</span><span class="sxs-lookup"><span data-stu-id="016a3-318">**Y**</span></span>                | <span data-ttu-id="016a3-319">**Z**</span><span class="sxs-lookup"><span data-stu-id="016a3-319">**Z**</span></span> |
    | <span data-ttu-id="016a3-320">0</span><span class="sxs-lookup"><span data-stu-id="016a3-320">0</span></span>     | <span data-ttu-id="016a3-321">0</span><span class="sxs-lookup"><span data-stu-id="016a3-321">0</span></span>                    | <span data-ttu-id="016a3-322">0</span><span class="sxs-lookup"><span data-stu-id="016a3-322">0</span></span>     |

    |       | <span data-ttu-id="016a3-323">TRANSFORMATION-METTRE À L’ÉCHELLE</span><span class="sxs-lookup"><span data-stu-id="016a3-323">TRANSFORM - SCALE</span></span> |       |
    | :---: | :---------------: | :---: |
    | <span data-ttu-id="016a3-324">**X**</span><span class="sxs-lookup"><span data-stu-id="016a3-324">**X**</span></span> | <span data-ttu-id="016a3-325">**Y**</span><span class="sxs-lookup"><span data-stu-id="016a3-325">**Y**</span></span>             | <span data-ttu-id="016a3-326">**Z**</span><span class="sxs-lookup"><span data-stu-id="016a3-326">**Z**</span></span> |
    | <span data-ttu-id="016a3-327">1</span><span class="sxs-lookup"><span data-stu-id="016a3-327">1</span></span>     | <span data-ttu-id="016a3-328">1</span><span class="sxs-lookup"><span data-stu-id="016a3-328">1</span></span>                 | <span data-ttu-id="016a3-329">1</span><span class="sxs-lookup"><span data-stu-id="016a3-329">1</span></span>     |

    ![définir la transformation de l’appareil photo](images/AzureLabs-Lab5-30.png)

## <a name="chapter-5---setting-up-the-unity-scene"></a><span data-ttu-id="016a3-331">Chapitre 5-Configuration de la scène Unity</span><span class="sxs-lookup"><span data-stu-id="016a3-331">Chapter 5 - Setting up the Unity scene</span></span>

1.  <span data-ttu-id="016a3-332">Cliquez avec le bouton droit dans une zone vide du *panneau hiérarchie*, sous **objet 3D**, ajoutez un **plan**.</span><span class="sxs-lookup"><span data-stu-id="016a3-332">Right-click in an empty area of the *Hierarchy Panel*, under **3D  Object**, add a **Plane**.</span></span>

    ![créer un plan](images/AzureLabs-Lab5-31.png)

2.  <span data-ttu-id="016a3-334">Une fois l’objet **plan** sélectionné, modifiez les paramètres suivants dans le *panneau Inspecteur*:</span><span class="sxs-lookup"><span data-stu-id="016a3-334">With the **Plane** object selected, change the following parameters in the *Inspector Panel*:</span></span>

    |       | <span data-ttu-id="016a3-335">TRANSFORMATION-POSITION</span><span class="sxs-lookup"><span data-stu-id="016a3-335">TRANSFORM - POSITION</span></span> |       |
    | :---: | :------------------: | :---: |
    | <span data-ttu-id="016a3-336">**X**</span><span class="sxs-lookup"><span data-stu-id="016a3-336">**X**</span></span> | <span data-ttu-id="016a3-337">**Y**</span><span class="sxs-lookup"><span data-stu-id="016a3-337">**Y**</span></span>                | <span data-ttu-id="016a3-338">**Z**</span><span class="sxs-lookup"><span data-stu-id="016a3-338">**Z**</span></span> |
    | <span data-ttu-id="016a3-339">0</span><span class="sxs-lookup"><span data-stu-id="016a3-339">0</span></span>     | <span data-ttu-id="016a3-340">0</span><span class="sxs-lookup"><span data-stu-id="016a3-340">0</span></span>                    | <span data-ttu-id="016a3-341">4</span><span class="sxs-lookup"><span data-stu-id="016a3-341">4</span></span>     |

    |       | <span data-ttu-id="016a3-342">TRANSFORMATION-METTRE À L’ÉCHELLE</span><span class="sxs-lookup"><span data-stu-id="016a3-342">TRANSFORM - SCALE</span></span> |       |
    | :---: | :---------------: | :---: |
    | <span data-ttu-id="016a3-343">**X**</span><span class="sxs-lookup"><span data-stu-id="016a3-343">**X**</span></span> | <span data-ttu-id="016a3-344">**Y**</span><span class="sxs-lookup"><span data-stu-id="016a3-344">**Y**</span></span>             | <span data-ttu-id="016a3-345">**Z**</span><span class="sxs-lookup"><span data-stu-id="016a3-345">**Z**</span></span> |
    | <span data-ttu-id="016a3-346">10</span><span class="sxs-lookup"><span data-stu-id="016a3-346">10</span></span>    | <span data-ttu-id="016a3-347">1</span><span class="sxs-lookup"><span data-stu-id="016a3-347">1</span></span>                 | <span data-ttu-id="016a3-348">10</span><span class="sxs-lookup"><span data-stu-id="016a3-348">10</span></span>    |

    ![définir la position et l’échelle du plan](images/AzureLabs-Lab5-32.png)

    ![vue scène du plan](images/AzureLabs-Lab5-33.png)

3.  <span data-ttu-id="016a3-351">Cliquez avec le bouton droit dans une zone vide du *panneau hiérarchie*, sous **objet 3D**, ajoutez un **cube**.</span><span class="sxs-lookup"><span data-stu-id="016a3-351">Right-click in an empty area of the *Hierarchy Panel*, under **3D Object**, add a **Cube**.</span></span>

    1.  <span data-ttu-id="016a3-352">Renommez le cube en **GazeButton** (avec le cube sélectionné, appuyez sur F2).</span><span class="sxs-lookup"><span data-stu-id="016a3-352">Rename the Cube to **GazeButton** (with the Cube selected, press 'F2').</span></span>

    2.  <span data-ttu-id="016a3-353">Modifiez les paramètres suivants dans le *panneau Inspecteur*:</span><span class="sxs-lookup"><span data-stu-id="016a3-353">Change the following parameters in the *Inspector Panel*:</span></span>

        |       | <span data-ttu-id="016a3-354">TRANSFORMATION-POSITION</span><span class="sxs-lookup"><span data-stu-id="016a3-354">TRANSFORM - POSITION</span></span> |       |
        | :---: | :------------------: |:-----:|
        | <span data-ttu-id="016a3-355">**X**</span><span class="sxs-lookup"><span data-stu-id="016a3-355">**X**</span></span> | <span data-ttu-id="016a3-356">**Y**</span><span class="sxs-lookup"><span data-stu-id="016a3-356">**Y**</span></span>                | <span data-ttu-id="016a3-357">**Z**</span><span class="sxs-lookup"><span data-stu-id="016a3-357">**Z**</span></span> |
        | <span data-ttu-id="016a3-358">0</span><span class="sxs-lookup"><span data-stu-id="016a3-358">0</span></span>     | <span data-ttu-id="016a3-359">3</span><span class="sxs-lookup"><span data-stu-id="016a3-359">3</span></span>                    | <span data-ttu-id="016a3-360">5\.</span><span class="sxs-lookup"><span data-stu-id="016a3-360">5</span></span>     |


        ![définir la transformation du bouton de pointage](images/AzureLabs-Lab5-34.png)

        ![mode scène de bouton en regard](images/AzureLabs-Lab5-35.png)

    3.  <span data-ttu-id="016a3-363">Cliquez sur le bouton **de liste** déroulante des balises et cliquez sur **Ajouter une étiquette** pour ouvrir le *volet balises & couches*.</span><span class="sxs-lookup"><span data-stu-id="016a3-363">Click on the **Tag** drop-down button and click on **Add Tag** to open the *Tags & Layers Pane*.</span></span>

        ![Ajouter une nouvelle balise](images/AzureLabs-Lab5-36.png)

        ![sélectionner plus](images/AzureLabs-Lab5-37.png)

    4.  <span data-ttu-id="016a3-366">Sélectionnez le bouton **+ (plus)** et, dans le champ nom de la *nouvelle balise* , entrez **GazeButton**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="016a3-366">Select the **+ (plus)** button, and in the *New Tag Name* field, enter **GazeButton**, and press **Save**.</span></span>

        ![nom de la nouvelle balise](images/AzureLabs-Lab5-38.png)

    5.  <span data-ttu-id="016a3-368">Cliquez sur l’objet **GazeButton** dans le *volet hiérarchie*, puis, dans le *panneau Inspecteur*, affectez la balise **GazeButton** nouvellement créée.</span><span class="sxs-lookup"><span data-stu-id="016a3-368">Click on the **GazeButton** object in the *Hierarchy Panel*, and in the *Inspector Panel*, assign the newly created **GazeButton** tag.</span></span>

        ![assigner un bouton de pointage à la nouvelle balise](images/AzureLabs-Lab5-39.png)

4.  <span data-ttu-id="016a3-370">Cliquez avec le bouton droit sur l’objet **GazeButton** , dans le *panneau hiérarchie*, puis ajoutez un **gameobject vide** (qui sera ajouté en tant qu’objet *enfant* ).</span><span class="sxs-lookup"><span data-stu-id="016a3-370">Right-click on the **GazeButton** object, in the *Hierarchy Panel*, and add an **Empty GameObject** (which will be added as a *child* object).</span></span>

5.  <span data-ttu-id="016a3-371">Sélectionnez le nouvel objet et renommez-le **ShapeSpawnPoint**.</span><span class="sxs-lookup"><span data-stu-id="016a3-371">Select the new object and rename it **ShapeSpawnPoint**.</span></span>

    1.  <span data-ttu-id="016a3-372">Modifiez les paramètres suivants dans le *panneau Inspecteur*:</span><span class="sxs-lookup"><span data-stu-id="016a3-372">Change the following parameters in the *Inspector Panel*:</span></span>

        |       | <span data-ttu-id="016a3-373">TRANSFORMATION-POSITION</span><span class="sxs-lookup"><span data-stu-id="016a3-373">TRANSFORM - POSITION</span></span> |       |
        | :---: | :------------------: |:----: |
        | <span data-ttu-id="016a3-374">**X**</span><span class="sxs-lookup"><span data-stu-id="016a3-374">**X**</span></span> |<span data-ttu-id="016a3-375">**Y**</span><span class="sxs-lookup"><span data-stu-id="016a3-375">**Y**</span></span>                 | <span data-ttu-id="016a3-376">**Z**</span><span class="sxs-lookup"><span data-stu-id="016a3-376">**Z**</span></span> |
        | <span data-ttu-id="016a3-377">0</span><span class="sxs-lookup"><span data-stu-id="016a3-377">0</span></span>     | <span data-ttu-id="016a3-378">-1</span><span class="sxs-lookup"><span data-stu-id="016a3-378">-1</span></span>                   | <span data-ttu-id="016a3-379">0</span><span class="sxs-lookup"><span data-stu-id="016a3-379">0</span></span>     |

        ![mettre à jour la transformation de point de génération de forme](images/AzureLabs-Lab5-40.png)

        ![vue scène du point de génération de forme](images/AzureLabs-Lab5-41.png)

6.  <span data-ttu-id="016a3-382">Vous allez ensuite créer un objet **texte 3D** pour fournir des commentaires sur l’état du service Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-382">Next you will create a **3D Text** object to provide feedback on the status of the Azure service.</span></span>

    <span data-ttu-id="016a3-383">Cliquez à nouveau avec le bouton droit sur **GazeButton** dans le panneau hiérarchie et ajoutez**un objet** **3D 3D Object** > en tant qu' *enfant*.</span><span class="sxs-lookup"><span data-stu-id="016a3-383">Right click on the **GazeButton** in the Hierarchy Panel again and add a **3D Object** > **3D Text** object as a *child*.</span></span>

    ![créer un objet texte 3D](images/AzureLabs-Lab5-42.png)

7.  <span data-ttu-id="016a3-385">Renommez l’objet **3D Text** en **AzureStatusText**.</span><span class="sxs-lookup"><span data-stu-id="016a3-385">Rename the **3D Text** object to **AzureStatusText**.</span></span>

8.  <span data-ttu-id="016a3-386">Modifiez la transformation de l’objet **AzureStatusText** comme suit:</span><span class="sxs-lookup"><span data-stu-id="016a3-386">Change the **AzureStatusText** object Transform as follows:</span></span>

    |       | <span data-ttu-id="016a3-387">TRANSFORMATION-POSITION</span><span class="sxs-lookup"><span data-stu-id="016a3-387">TRANSFORM - POSITION</span></span> |       |
    | :---: | :------------------: | :---: |
    | <span data-ttu-id="016a3-388">**X**</span><span class="sxs-lookup"><span data-stu-id="016a3-388">**X**</span></span> | <span data-ttu-id="016a3-389">**Y**</span><span class="sxs-lookup"><span data-stu-id="016a3-389">**Y**</span></span>                | <span data-ttu-id="016a3-390">**Z**</span><span class="sxs-lookup"><span data-stu-id="016a3-390">**Z**</span></span> |
    | <span data-ttu-id="016a3-391">0</span><span class="sxs-lookup"><span data-stu-id="016a3-391">0</span></span>     | <span data-ttu-id="016a3-392">0</span><span class="sxs-lookup"><span data-stu-id="016a3-392">0</span></span>                    | <span data-ttu-id="016a3-393">-0,6</span><span class="sxs-lookup"><span data-stu-id="016a3-393">-0.6</span></span>  |

    |       | <span data-ttu-id="016a3-394">TRANSFORMATION-METTRE À L’ÉCHELLE</span><span class="sxs-lookup"><span data-stu-id="016a3-394">TRANSFORM - SCALE</span></span> |       |
    | :---: | :---------------: | :---: |
    | <span data-ttu-id="016a3-395">**X**</span><span class="sxs-lookup"><span data-stu-id="016a3-395">**X**</span></span> | <span data-ttu-id="016a3-396">**Y**</span><span class="sxs-lookup"><span data-stu-id="016a3-396">**Y**</span></span>             | <span data-ttu-id="016a3-397">**Z**</span><span class="sxs-lookup"><span data-stu-id="016a3-397">**Z**</span></span> |
    | <span data-ttu-id="016a3-398">0.1</span><span class="sxs-lookup"><span data-stu-id="016a3-398">0.1</span></span>   | <span data-ttu-id="016a3-399">0.1</span><span class="sxs-lookup"><span data-stu-id="016a3-399">0.1</span></span>               | <span data-ttu-id="016a3-400">0.1</span><span class="sxs-lookup"><span data-stu-id="016a3-400">0.1</span></span>   |


    > [!NOTE]
    > <span data-ttu-id="016a3-401">Ne vous inquiétez pas si elle semble être décentrée, car cela sera résolu lorsque le composant de maillage de texte ci-dessous sera mis à jour.</span><span class="sxs-lookup"><span data-stu-id="016a3-401">Do not worry if it appears to be off-centre, as this will be fixed when the below Text Mesh component is updated.</span></span>

9.  <span data-ttu-id="016a3-402">Modifiez le composant de **maillage de texte** pour qu’il corresponde à ce qui suit:</span><span class="sxs-lookup"><span data-stu-id="016a3-402">Change the **Text Mesh** component to match the below:</span></span>

    ![définir le composant de maillage de texte](images/AzureLabs-Lab5-43.png)

    > [!TIP]
    > <span data-ttu-id="016a3-404">La couleur sélectionnée ici est la couleur hexadécimale: **000000FF**, cependant, n’hésitez pas à choisir les vôtres, assurez-vous simplement qu’elles sont lisibles.</span><span class="sxs-lookup"><span data-stu-id="016a3-404">The selected color here is Hex color: **000000FF**, though feel free to choose your own, just ensure it is readable.</span></span>

10. <span data-ttu-id="016a3-405">La structure de votre volet de hiérarchie doit maintenant ressembler à ceci:</span><span class="sxs-lookup"><span data-stu-id="016a3-405">Your Hierarchy Panel structure should now look like this:</span></span>

    ![maillage de texte en mode scène](images/AzureLabs-Lab5-43b.png)

10. <span data-ttu-id="016a3-407">Votre scène doit maintenant ressembler à ceci:</span><span class="sxs-lookup"><span data-stu-id="016a3-407">Your scene should now look like this:</span></span>

    ![maillage de texte en mode scène](images/AzureLabs-Lab5-44.png)


## <a name="chapter-6---import-azure-storage-for-unity"></a><span data-ttu-id="016a3-409">Chapitre 6-importer un stockage Azure pour Unity</span><span class="sxs-lookup"><span data-stu-id="016a3-409">Chapter 6 - Import Azure Storage for Unity</span></span>

<span data-ttu-id="016a3-410">Vous allez utiliser le stockage Azure pour Unity (qui utilise lui-même le kit de développement logiciel (SDK) .net pour Azure).</span><span class="sxs-lookup"><span data-stu-id="016a3-410">You will be using Azure Storage for Unity (which itself leverages the .Net SDK for Azure).</span></span> <span data-ttu-id="016a3-411">Pour plus d’informations à ce sujet, consultez l' [article stockage Azure pour Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).</span><span class="sxs-lookup"><span data-stu-id="016a3-411">You can read more about this at the [Azure Storage for Unity article](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).</span></span>

<span data-ttu-id="016a3-412">Il existe actuellement un problème connu dans Unity qui nécessite que les plug-ins soient reconfigurés après l’importation.</span><span class="sxs-lookup"><span data-stu-id="016a3-412">There is currently a known issue in Unity which requires plugins to be reconfigured after import.</span></span> <span data-ttu-id="016a3-413">Ces étapes (4-7 dans cette section) ne sont plus nécessaires une fois que le bogue a été résolu.</span><span class="sxs-lookup"><span data-stu-id="016a3-413">These steps (4 - 7 in this section) will no longer be required after the bug has been resolved.</span></span>

<span data-ttu-id="016a3-414">Pour importer le kit de développement logiciel (SDK) dans votre propre projet, assurez-vous d’avoir téléchargé la dernière version [de «. pour Unity» à partir de GitHub](https://aka.ms/azstorage-unitysdk).</span><span class="sxs-lookup"><span data-stu-id="016a3-414">To import the SDK into your own project, make sure you have downloaded the latest ['.unitypackage' from GitHub](https://aka.ms/azstorage-unitysdk).</span></span> <span data-ttu-id="016a3-415">Ensuite, procédez comme suit:</span><span class="sxs-lookup"><span data-stu-id="016a3-415">Then, do the following:</span></span>

1.  <span data-ttu-id="016a3-416">Ajoutez le fichier **. pour Unity** à Unity à l’aide de l’option de menu**package personnalisé** du**package** > d’importation de **ressources** > .</span><span class="sxs-lookup"><span data-stu-id="016a3-416">Add the **.unitypackage** file to Unity by using the **Assets** > **Import Package** > **Custom Package** menu option.</span></span>

2.  <span data-ttu-id="016a3-417">Dans la zone **importer le package Unity** qui s’affiche, vous pouvez tout sélectionner sous**stockage**du **plug-in** > .</span><span class="sxs-lookup"><span data-stu-id="016a3-417">In the **Import Unity Package** box that pops up, you can select everything under **Plugin** > **Storage**.</span></span> <span data-ttu-id="016a3-418">Décochez tout le reste, car il n’est pas nécessaire pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="016a3-418">Uncheck everything else, as it is not needed for this course.</span></span>

    ![importer dans le package](images/AzureLabs-Lab5-45.png)

3.  <span data-ttu-id="016a3-420">Cliquez sur le bouton **Importer** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="016a3-420">Click the **Import** button to add the items to your project.</span></span>

4.  <span data-ttu-id="016a3-421">Accédez au dossier *stockage* sous *plug-ins*, dans la vue projet, puis sélectionnez les plug-ins suivants *uniquement*:</span><span class="sxs-lookup"><span data-stu-id="016a3-421">Go to the *Storage* folder under *Plugins*, in the Project view, and select the following plugins *only*:</span></span>

    -   <span data-ttu-id="016a3-422">Microsoft.Data.Edm</span><span class="sxs-lookup"><span data-stu-id="016a3-422">Microsoft.Data.Edm</span></span>
    -   <span data-ttu-id="016a3-423">Microsoft.Data.OData</span><span class="sxs-lookup"><span data-stu-id="016a3-423">Microsoft.Data.OData</span></span>
    -   <span data-ttu-id="016a3-424">Microsoft.WindowsAzure.Storage</span><span class="sxs-lookup"><span data-stu-id="016a3-424">Microsoft.WindowsAzure.Storage</span></span>
    -   <span data-ttu-id="016a3-425">Newtonsoft. JSON</span><span class="sxs-lookup"><span data-stu-id="016a3-425">Newtonsoft.Json</span></span>
    -   <span data-ttu-id="016a3-426">System. spatial</span><span class="sxs-lookup"><span data-stu-id="016a3-426">System.Spatial</span></span>

        ![décocher une plateforme](images/AzureLabs-Lab5-46.png)

5.  <span data-ttu-id="016a3-428">Une fois *ces plug-ins spécifiques* sélectionnés, décochez  *toutes les plateformes* et décochez  *WSAPlayer* , puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="016a3-428">With *these specific plugins* selected, **uncheck** *Any Platform* and **uncheck** *WSAPlayer* then click **Apply**.</span></span>

    ![appliquer des dll de plateforme](images/AzureLabs-Lab5-47.png)

    > [!NOTE]
    > <span data-ttu-id="016a3-430">Nous marqueons ces plug-ins particuliers à utiliser uniquement dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="016a3-430">We are marking these particular plugins to only be used in the Unity Editor.</span></span> <span data-ttu-id="016a3-431">Cela est dû au fait qu’il existe différentes versions des mêmes plug-ins dans le dossier WSA qui seront utilisées après l’exportation du projet à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="016a3-431">This is because there are different versions of the same plugins in the WSA folder that will be used after the project is exported from Unity.</span></span>

6.  <span data-ttu-id="016a3-432">Dans le dossier de plug-in de *stockage* , sélectionnez uniquement:</span><span class="sxs-lookup"><span data-stu-id="016a3-432">In the *Storage* plugin folder, select only:</span></span>

    -   <span data-ttu-id="016a3-433">Microsoft. Data. services. client</span><span class="sxs-lookup"><span data-stu-id="016a3-433">Microsoft.Data.Services.Client</span></span>

        ![définir ne pas traiter pour les dll](images/AzureLabs-Lab5-48.png)

7.  <span data-ttu-id="016a3-435">Cochez la case **ne pas traiter** sous *paramètres de plateforme* , puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="016a3-435">Check the **Don't Process** box under *Platform Settings* and click **Apply**.</span></span>

    ![ne pas appliquer de traitement](images/AzureLabs-Lab5-49.png)

    > [!NOTE]
    > <span data-ttu-id="016a3-437">Nous marquant ce plug-in «ne pas traiter», car l’assembly Unity Patcher a des difficultés à traiter ce plug-in.</span><span class="sxs-lookup"><span data-stu-id="016a3-437">We are marking this plugin "Don't process" because the Unity assembly patcher has difficulty processing this plugin.</span></span> <span data-ttu-id="016a3-438">Le plug-in fonctionne toujours même s’il n’est pas traité.</span><span class="sxs-lookup"><span data-stu-id="016a3-438">The plugin will still work even though it is not processed.</span></span>

## <a name="chapter-7---create-the-azureservices-class"></a><span data-ttu-id="016a3-439">Chapitre 7-créer la classe AzureServices</span><span class="sxs-lookup"><span data-stu-id="016a3-439">Chapter 7 - Create the AzureServices class</span></span>

<span data-ttu-id="016a3-440">La première classe que vous allez créer est la classe *AzureServices* .</span><span class="sxs-lookup"><span data-stu-id="016a3-440">The first class you are going to create is the *AzureServices* class.</span></span>

<span data-ttu-id="016a3-441">La classe *AzureServices* est chargée des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="016a3-441">The *AzureServices* class will be responsible for:</span></span>

-   <span data-ttu-id="016a3-442">Stockage des informations d’identification du compte Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-442">Storing Azure Account credentials.</span></span>

-   <span data-ttu-id="016a3-443">Appel de votre fonction Azure App.</span><span class="sxs-lookup"><span data-stu-id="016a3-443">Calling your Azure App Function.</span></span>

-   <span data-ttu-id="016a3-444">Le chargement et le téléchargement du fichier de données dans votre stockage cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-444">The upload and download of the data file in your Azure Cloud Storage.</span></span>

<span data-ttu-id="016a3-445">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="016a3-445">To create this Class:</span></span>

1.  <span data-ttu-id="016a3-446">Cliquez avec le bouton droit dans le dossier *Asset* , situé dans le panneau projet, **créez** > le**dossier**.</span><span class="sxs-lookup"><span data-stu-id="016a3-446">Right-click in the *Asset* Folder, located in the Project Panel, **Create** > **Folder**.</span></span> <span data-ttu-id="016a3-447">Nommez le dossier **scripts**.</span><span class="sxs-lookup"><span data-stu-id="016a3-447">Name the folder **Scripts**.</span></span>

    ![créer un dossier](images/AzureLabs-Lab5-50.png)

    ![dossier d’appel-scripts](images/AzureLabs-Lab5-51.png)

2.  <span data-ttu-id="016a3-450">Double-cliquez sur le dossier que vous venez de créer pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="016a3-450">Double click on the folder just created, to open it.</span></span>

3.  <span data-ttu-id="016a3-451">Cliquez avec le bouton droit dans le dossier, puis **créez**  >   **C# le script**.</span><span class="sxs-lookup"><span data-stu-id="016a3-451">Right-click inside the folder, **Create** > **C# Script**.</span></span> <span data-ttu-id="016a3-452">Appelez le script *AzureServices*.</span><span class="sxs-lookup"><span data-stu-id="016a3-452">Call the script *AzureServices*.</span></span>

4.  <span data-ttu-id="016a3-453">Double-cliquez sur la nouvelle classe *AzureServices* pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="016a3-453">Double click on the new *AzureServices* class to open it with *Visual Studio*.</span></span>

5.  <span data-ttu-id="016a3-454">Ajoutez les espaces de noms suivants en haut de *AzureServices*:</span><span class="sxs-lookup"><span data-stu-id="016a3-454">Add the following namespaces to the top of the *AzureServices*:</span></span>

    ```csharp
        using System;
        using System.Threading.Tasks;
        using UnityEngine;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.File;
        using System.IO;
        using System.Net;
    ```

6.  <span data-ttu-id="016a3-455">Ajoutez les champs Inspector suivants à l’intérieur de la classe *AzureServices* :</span><span class="sxs-lookup"><span data-stu-id="016a3-455">Add the following Inspector Fields inside the *AzureServices* class:</span></span>

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

7.  <span data-ttu-id="016a3-456">Ajoutez ensuite les variables de membre suivantes à l’intérieur de la classe *AzureServices* :</span><span class="sxs-lookup"><span data-stu-id="016a3-456">Then add the following member variables inside the *AzureServices* class:</span></span>

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
    > <span data-ttu-id="016a3-457">Veillez à remplacer les valeurs de *point de terminaison* et de *chaîne de connexion* par les valeurs de votre stockage Azure, qui se trouvent dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-457">Make sure you replace the *endpoint* and *connection string* values with the values from your Azure storage, found in the Azure Portal</span></span>

8.  <span data-ttu-id="016a3-458">Vous devez maintenant ajouter le code des méthodes *éveillés ()* et *Start ()* .</span><span class="sxs-lookup"><span data-stu-id="016a3-458">Code for *Awake()* and *Start()* methods now needs to be added.</span></span> <span data-ttu-id="016a3-459">Ces méthodes sont appelées lorsque la classe est initialisée:</span><span class="sxs-lookup"><span data-stu-id="016a3-459">These methods will be called when the class initializes:</span></span>

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
    > <span data-ttu-id="016a3-460">Nous remplirons le code pour *CallAzureFunctionForNextShape ()* dans un [chapitre ultérieur](#chapter-10---completing-the-azureservices-class).</span><span class="sxs-lookup"><span data-stu-id="016a3-460">We will fill in the code for *CallAzureFunctionForNextShape()* in a [future Chapter](#chapter-10---completing-the-azureservices-class).</span></span>

9.  <span data-ttu-id="016a3-461">Supprimez la méthode *Update ()* puisque cette classe ne l’utilisera pas.</span><span class="sxs-lookup"><span data-stu-id="016a3-461">Delete the *Update()* method since this class will not use it.</span></span>

10. <span data-ttu-id="016a3-462">Enregistrez vos modifications dans Visual Studio, puis revenez à Unity.</span><span class="sxs-lookup"><span data-stu-id="016a3-462">Save your changes in Visual Studio, and then return to Unity.</span></span>

11. <span data-ttu-id="016a3-463">Cliquez et faites glisser la classe *AzureServices* du dossier scripts vers l’objet Camera principal dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="016a3-463">Click and drag the *AzureServices* class from the Scripts folder to the Main Camera object in the *Hierarchy Panel*.</span></span>

12. <span data-ttu-id="016a3-464">Sélectionnez l’appareil photo principal, puis saisissez l’objet enfant **AzureStatusText** sous l’objet **GazeButton** , et placez-le dans le champ cible de référence **AzureStatusText** , dans l' *inspecteur*, pour fournir la référence à l' *objet Script AzureServices* .</span><span class="sxs-lookup"><span data-stu-id="016a3-464">Select the Main Camera, then grab the **AzureStatusText** child object from beneath the **GazeButton** object, and place it within the **AzureStatusText** reference target field, in the *Inspector*, to provide the reference to the *AzureServices* script.</span></span>

    ![affecter une cible de référence de texte d’État Azure](images/AzureLabs-Lab5-52.png)

## <a name="chapter-8---create-the-shapefactory-class"></a><span data-ttu-id="016a3-466">Chapitre 8-créer la classe ShapeFactory</span><span class="sxs-lookup"><span data-stu-id="016a3-466">Chapter 8 - Create the ShapeFactory class</span></span>

<span data-ttu-id="016a3-467">Le prochain script à créer est la classe *ShapeFactory* .</span><span class="sxs-lookup"><span data-stu-id="016a3-467">The next script to create, is the *ShapeFactory* class.</span></span> <span data-ttu-id="016a3-468">Le rôle de cette classe est de créer une nouvelle forme, lorsqu’elle est demandée, et de conserver un historique des formes créées dans une *liste d’historique des formes*.</span><span class="sxs-lookup"><span data-stu-id="016a3-468">The role of this class is to create a new shape, when requested, and keep a history of the shapes created in a *Shape History List*.</span></span> <span data-ttu-id="016a3-469">Chaque fois qu’une forme est créée, la liste de l' *historique des formes* est mise à jour dans la classe *AzureService* , puis stockée dans votre *stockage Azure*.</span><span class="sxs-lookup"><span data-stu-id="016a3-469">Every time a shape is created, the *Shape History list* is updated in the *AzureService* class, and then stored in your *Azure Storage*.</span></span> <span data-ttu-id="016a3-470">Lorsque l’application démarre, si un fichier stocké est trouvé dans votre *stockage Azure*, la liste de l' *historique des formes* est récupérée et relue, avec l’objet **texte 3D** qui indique si la forme générée provient du stockage ou de la nouvelle.</span><span class="sxs-lookup"><span data-stu-id="016a3-470">When the application starts, if a stored file is found in your *Azure Storage*, the *Shape History list* is retrieved and replayed, with the **3D Text** object providing whether the generated shape is from storage, or new.</span></span>

<span data-ttu-id="016a3-471">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="016a3-471">To create this class:</span></span>

1.  <span data-ttu-id="016a3-472">Accédez au dossier **scripts** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="016a3-472">Go to the **Scripts** folder you created previously.</span></span>

2.  <span data-ttu-id="016a3-473">Cliquez avec le bouton droit dans le dossier, puis **créez**  >   **C# le script**.</span><span class="sxs-lookup"><span data-stu-id="016a3-473">Right-click inside the folder, **Create** > **C# Script**.</span></span> <span data-ttu-id="016a3-474">Appelez le script *ShapeFactory*.</span><span class="sxs-lookup"><span data-stu-id="016a3-474">Call the script *ShapeFactory*.</span></span>

3.  <span data-ttu-id="016a3-475">Double-cliquez sur le nouveau script *ShapeFactory* pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="016a3-475">Double click on the new *ShapeFactory* script to open it with *Visual Studio*.</span></span>

4.  <span data-ttu-id="016a3-476">Vérifiez que la classe *ShapeFactory* comprend les espaces de noms suivants:</span><span class="sxs-lookup"><span data-stu-id="016a3-476">Ensure the *ShapeFactory* class includes the following namespaces:</span></span>

    ```csharp
        using System.Collections.Generic;
        using UnityEngine;
    ```

5.  <span data-ttu-id="016a3-477">Ajoutez les variables ci-dessous à la classe *ShapeFactory* , puis remplacez les fonctions *Start ()* et *éveillé ()* par celles ci-dessous:</span><span class="sxs-lookup"><span data-stu-id="016a3-477">Add the variables shown below to the *ShapeFactory* class, and replace the *Start()* and *Awake()* functions with those below:</span></span>

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

6.  <span data-ttu-id="016a3-478">La méthode *createShape ()* génère les formes primitives, en fonction du paramètre *entier* fourni.</span><span class="sxs-lookup"><span data-stu-id="016a3-478">The *CreateShape()* method generates the primitive shapes, based upon the provided *integer* parameter.</span></span> <span data-ttu-id="016a3-479">Le paramètre booléen est utilisé pour spécifier si la forme actuellement créée provient d’un stockage ou d’une nouvelle.</span><span class="sxs-lookup"><span data-stu-id="016a3-479">The Boolean parameter is used to specify whether the currently created shape is from storage, or new.</span></span> <span data-ttu-id="016a3-480">Placez le code suivant dans votre classe *ShapeFactory* , sous les méthodes précédentes:</span><span class="sxs-lookup"><span data-stu-id="016a3-480">Place the following code in your *ShapeFactory* class, below the previous methods:</span></span>

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

7.  <span data-ttu-id="016a3-481">Veillez à enregistrer vos modifications dans Visual Studio avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="016a3-481">Be sure to save your changes in Visual Studio before returning to Unity.</span></span>

8.  <span data-ttu-id="016a3-482">De retour dans l’éditeur Unity, cliquez et faites glisser la classe *ShapeFactory* du dossier **scripts** vers l’objet **Camera principal** dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="016a3-482">Back in the Unity Editor, click and drag the *ShapeFactory* class from the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span>

9. <span data-ttu-id="016a3-483">Une fois l’appareil photo sélectionné, vous remarquerez que le composant script *ShapeFactory* ne contient pas la référence du *point de génération* .</span><span class="sxs-lookup"><span data-stu-id="016a3-483">With the Main Camera selected you will notice the *ShapeFactory* script component is missing the *Spawn Point* reference.</span></span> <span data-ttu-id="016a3-484">Pour résoudre ce problème, faites glisser l’objet **ShapeSpawnPoint** du volet de la *hiérarchie* vers la cible de référence de **point de génération** .</span><span class="sxs-lookup"><span data-stu-id="016a3-484">To fix it, drag the **ShapeSpawnPoint** object from the *Hierarchy Panel* to the **Spawn Point** reference target.</span></span>

    ![définir la cible de référence de fabrique de forme](images/AzureLabs-Lab5-53.png)

## <a name="chapter-9---create-the-gaze-class"></a><span data-ttu-id="016a3-486">Chapitre 9-créer la classe en regard</span><span class="sxs-lookup"><span data-stu-id="016a3-486">Chapter 9 - Create the Gaze class</span></span>

<span data-ttu-id="016a3-487">Le dernier script que vous devez créer est la classe de *regard* .</span><span class="sxs-lookup"><span data-stu-id="016a3-487">The last script you need to create is the *Gaze* class.</span></span>

<span data-ttu-id="016a3-488">Cette classe est chargée de créer un **Raycast** qui sera projeté à l’avance de la caméra principale, pour détecter l’objet que l’utilisateur examine.</span><span class="sxs-lookup"><span data-stu-id="016a3-488">This class is responsible for creating a **Raycast** that will be projected forward from the Main Camera, to detect which object the user is looking at.</span></span> <span data-ttu-id="016a3-489">Dans ce cas, le Raycast doit déterminer si l’utilisateur regarde l’objet **GazeButton** dans la scène et déclencher un comportement.</span><span class="sxs-lookup"><span data-stu-id="016a3-489">In this case, the Raycast will need to identify if the user is looking at the **GazeButton** object in the scene and trigger a behavior.</span></span>

<span data-ttu-id="016a3-490">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="016a3-490">To create this Class:</span></span>

1.  <span data-ttu-id="016a3-491">Accédez au dossier **scripts** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="016a3-491">Go to the **Scripts** folder you created previously.</span></span>

2.  <span data-ttu-id="016a3-492">Cliquez avec le bouton droit dans le panneau projet, puis **créez**  >   **C# script**.</span><span class="sxs-lookup"><span data-stu-id="016a3-492">Right-click in the Project Panel, **Create** > **C# Script**.</span></span> <span data-ttu-id="016a3-493">Appelez le point de *regard*du script.</span><span class="sxs-lookup"><span data-stu-id="016a3-493">Call the script *Gaze*.</span></span>

3.  <span data-ttu-id="016a3-494">Double-cliquez sur le nouveau script de *regard* pour l’ouvrir avec *Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="016a3-494">Double click on the new *Gaze* script to open it with *Visual Studio.*</span></span>

4.  <span data-ttu-id="016a3-495">Assurez-vous que l’espace de noms suivant est inclus en haut du script:</span><span class="sxs-lookup"><span data-stu-id="016a3-495">Ensure the following namespace is included at the top of the script:</span></span>

    ```csharp
        using UnityEngine;
    ```

5.  <span data-ttu-id="016a3-496">Ajoutez ensuite les variables suivantes à l’intérieur de la classe *regard* :</span><span class="sxs-lookup"><span data-stu-id="016a3-496">Then add the following variables inside the *Gaze* class:</span></span>

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
> <span data-ttu-id="016a3-497">Certaines de ces variables pourront être modifiées dans l' *éditeur*.</span><span class="sxs-lookup"><span data-stu-id="016a3-497">Some of these variables will be able to be edited in the *Editor*.</span></span>

6.  <span data-ttu-id="016a3-498">Vous devez maintenant ajouter du code pour les méthodes *éveillé ()* et *Start ()* .</span><span class="sxs-lookup"><span data-stu-id="016a3-498">Code for the *Awake()* and *Start()* methods now needs to be added.</span></span>

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

7.  <span data-ttu-id="016a3-499">Ajoutez le code suivant, qui créera un objet curseur au démarrage, avec la méthode *Update ()* , qui exécutera la méthode Raycast, ainsi que l’emplacement où la valeur booléenne GazeEnabled est basculée:</span><span class="sxs-lookup"><span data-stu-id="016a3-499">Add the following code, which will create a cursor object at start, along with the *Update()* method, which will run the Raycast method, along with being where the GazeEnabled boolean is toggled:</span></span>

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

8. <span data-ttu-id="016a3-500">Ensuite, ajoutez la méthode *UpdateRaycast ()* , qui projetera un Raycast et détectera la cible d’accès.</span><span class="sxs-lookup"><span data-stu-id="016a3-500">Next add the *UpdateRaycast()* method, which will project a Raycast and detect the hit target.</span></span>

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

9. <span data-ttu-id="016a3-501">Enfin, ajoutez la méthode *ResetFocusedObject ()* , qui va basculer la couleur active des objets GazeButton, en indiquant si elle crée ou non une nouvelle forme.</span><span class="sxs-lookup"><span data-stu-id="016a3-501">Lastly, add the *ResetFocusedObject()* method, which will toggle the GazeButton objects current color, indicating whether it is creating a new shape or not.</span></span>

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

10.  <span data-ttu-id="016a3-502">Enregistrez vos modifications dans Visual Studio avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="016a3-502">Save your changes in Visual Studio before returning to Unity.</span></span>

11.  <span data-ttu-id="016a3-503">Cliquez et faites glisser *la classe* pointage du dossier scripts vers l’objet **caméra principal** dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="016a3-503">Click and drag the *Gaze* class from the Scripts folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span>

## <a name="chapter-10---completing-the-azureservices-class"></a><span data-ttu-id="016a3-504">Chapitre 10-réalisation de la classe AzureServices</span><span class="sxs-lookup"><span data-stu-id="016a3-504">Chapter 10 - Completing the AzureServices class</span></span>

<span data-ttu-id="016a3-505">Avec les autres scripts en place, il est désormais possible d' *effectuer* la classe *AzureServices* .</span><span class="sxs-lookup"><span data-stu-id="016a3-505">With the other scripts in place, it is now possible to *complete* the *AzureServices* class.</span></span> <span data-ttu-id="016a3-506">Pour ce faire, procédez comme suit:</span><span class="sxs-lookup"><span data-stu-id="016a3-506">This will be achieved through:</span></span>

1.  <span data-ttu-id="016a3-507">Ajout d’une nouvelle méthode nommée *CreateCloudIdentityAsync ()* , pour configurer les variables d’authentification nécessaires à la communication avec Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-507">Adding a new method named *CreateCloudIdentityAsync()*, to set up the authentication variables needed for communicating with Azure.</span></span>

    > <span data-ttu-id="016a3-508">Cette méthode vérifie également l’existence d’un fichier précédemment stocké contenant la liste de formes.</span><span class="sxs-lookup"><span data-stu-id="016a3-508">This method will also check for the existence of a previously stored File containing the Shape List.</span></span>
    >
    > <span data-ttu-id="016a3-509">**Si le fichier est trouvé**, il désactive le point d’interdépendance de *l’utilisateur et*déclenche la création de la forme, en fonction du modèle de formes, tel qu’il est stocké dans le **fichier de stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="016a3-509">**If the file is found**, it will disable the user *Gaze*, and trigger Shape creation, according to the pattern of shapes, as stored in the **Azure Storage file**.</span></span> <span data-ttu-id="016a3-510">L’utilisateur peut voir cela, car la **maille de texte** fournira «stockage» ou «nouveau», en fonction de l’origine des formes.</span><span class="sxs-lookup"><span data-stu-id="016a3-510">The user can see this, as the **Text Mesh** will provide display 'Storage' or 'New', depending on the shapes origin.</span></span>
    >
    > <span data-ttu-id="016a3-511">**Si aucun fichier n’est trouvé**, il active le point de *regard*, ce qui permet à l’utilisateur de créer des formes lors de la recherche de l’objet **GazeButton** dans la scène.</span><span class="sxs-lookup"><span data-stu-id="016a3-511">**If no file is found**, it will enable the *Gaze*, enabling the user to create shapes when looking at the **GazeButton** object in the scene.</span></span>

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

2.  <span data-ttu-id="016a3-512">L’extrait de code suivant se trouve dans la méthode *Start ()* ; où un appel sera effectué à la méthode *CreateCloudIdentityAsync ()* .</span><span class="sxs-lookup"><span data-stu-id="016a3-512">The next code snippet is from within the *Start()* method; wherein a call will be made to the *CreateCloudIdentityAsync()* method.</span></span> <span data-ttu-id="016a3-513">N’hésitez pas à effectuer une copie sur votre méthode *Start ()* actuelle, avec les éléments suivants:</span><span class="sxs-lookup"><span data-stu-id="016a3-513">Feel free to copy over your current *Start()* method, with the below:</span></span>

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

3.  <span data-ttu-id="016a3-514">Renseignez le code de la méthode *CallAzureFunctionForNextShape ()* .</span><span class="sxs-lookup"><span data-stu-id="016a3-514">Fill in the code for the method *CallAzureFunctionForNextShape()*.</span></span> <span data-ttu-id="016a3-515">Vous allez utiliser la *Function App Azure* précédemment créée pour demander un index de forme.</span><span class="sxs-lookup"><span data-stu-id="016a3-515">You will use the previously created *Azure Function App* to request a shape index.</span></span> <span data-ttu-id="016a3-516">Une fois la nouvelle forme reçue, cette méthode envoie la forme à la classe *ShapeFactory* pour créer la nouvelle forme dans la scène.</span><span class="sxs-lookup"><span data-stu-id="016a3-516">Once the new shape is received, this method will send the shape to the *ShapeFactory* class to create the new shape in the scene.</span></span> <span data-ttu-id="016a3-517">Utilisez le code ci-dessous pour terminer le corps de *CallAzureFunctionForNextShape ()* .</span><span class="sxs-lookup"><span data-stu-id="016a3-517">Use the code below to complete the body of *CallAzureFunctionForNextShape()*.</span></span>

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

4.  <span data-ttu-id="016a3-518">Ajoutez une méthode pour créer une chaîne en concaténant les entiers stockés dans la liste de l’historique des formes et en l’enregistrant dans votre *fichier de stockage Azure*.</span><span class="sxs-lookup"><span data-stu-id="016a3-518">Add a method to create a string, by concatenating the integers stored in the shape history list, and saving it in your *Azure Storage File*.</span></span>

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

5.  <span data-ttu-id="016a3-519">Ajoutez une méthode pour récupérer le texte stocké dans le fichier situé dans votre *fichier de stockage Azure* et le désérialiser dans une liste.</span><span class="sxs-lookup"><span data-stu-id="016a3-519">Add a method to retrieve the text stored in the file located in your *Azure Storage File* and *deserialize* it into a list.</span></span>

6.  <span data-ttu-id="016a3-520">Une fois ce processus terminé, la méthode réactive le point de regard pour permettre à l’utilisateur d’ajouter des formes à la scène.</span><span class="sxs-lookup"><span data-stu-id="016a3-520">Once this process is completed, the method re-enables the gaze so that the user can add more shapes to the scene.</span></span>

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

7.  <span data-ttu-id="016a3-521">Enregistrez vos modifications dans Visual Studio avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="016a3-521">Save your changes in Visual Studio before returning to Unity.</span></span>

## <a name="chapter-11---build-the-uwp-solution"></a><span data-ttu-id="016a3-522">Chapitre 11-créer la solution UWP</span><span class="sxs-lookup"><span data-stu-id="016a3-522">Chapter 11 - Build the UWP Solution</span></span>

<span data-ttu-id="016a3-523">Pour commencer le processus de génération:</span><span class="sxs-lookup"><span data-stu-id="016a3-523">To begin the Build process:</span></span>

1.  <span data-ttu-id="016a3-524">Accédez à **fichier** > **paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="016a3-524">Go to **File** > **Build Settings**.</span></span>

    ![générer l’application](images/AzureLabs-Lab5-54.png)

2.  <span data-ttu-id="016a3-526">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="016a3-526">Click **Build**.</span></span> <span data-ttu-id="016a3-527">Unity lance une fenêtre de l' *Explorateur de fichiers* , dans laquelle vous devez créer, puis sélectionner un dossier dans lequel générer l’application.</span><span class="sxs-lookup"><span data-stu-id="016a3-527">Unity will launch a *File Explorer* window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="016a3-528">Créez ce dossier maintenant, puis nommez-le *application*.</span><span class="sxs-lookup"><span data-stu-id="016a3-528">Create that folder now, and name it *App*.</span></span> <span data-ttu-id="016a3-529">Ensuite, avec le dossier d' *application* sélectionné, appuyez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="016a3-529">Then with the *App* folder selected, press **Select Folder**.</span></span>

3.  <span data-ttu-id="016a3-530">Unity commence à générer votre projet dans le dossier de l' *application* .</span><span class="sxs-lookup"><span data-stu-id="016a3-530">Unity will begin building your project to the *App* folder.</span></span>

4.  <span data-ttu-id="016a3-531">Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' *Explorateur de fichiers* s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).</span><span class="sxs-lookup"><span data-stu-id="016a3-531">Once Unity has finished building (it might take some time), it will open a *File Explorer* window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

## <a name="chapter-12---deploying-your-application"></a><span data-ttu-id="016a3-532">Chapitre 12: déploiement de votre application</span><span class="sxs-lookup"><span data-stu-id="016a3-532">Chapter 12 - Deploying your application</span></span>

<span data-ttu-id="016a3-533">Pour déployer votre application:</span><span class="sxs-lookup"><span data-stu-id="016a3-533">To deploy your application:</span></span>

1.  <span data-ttu-id="016a3-534">Accédez au dossier de l' *application* qui a été créé dans le [dernier chapitre](#chapter-11---build-the-uwp-solution).</span><span class="sxs-lookup"><span data-stu-id="016a3-534">Navigate to the *App* folder which was created in the [last Chapter](#chapter-11---build-the-uwp-solution).</span></span> <span data-ttu-id="016a3-535">Vous verrez un fichier avec le nom de votre application, avec l’extension «. sln», que vous devez double-cliquer, afin de l’ouvrir dans *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="016a3-535">You will see a file with your apps name, with the '.sln' extension, which you should double-click, so to open it within *Visual Studio*.</span></span>

2.  <span data-ttu-id="016a3-536">Dans la **plateforme**de la solution, sélectionnez **x86, ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="016a3-536">In the **Solution Platform**, select **x86, Local Machine**.</span></span>

3.  <span data-ttu-id="016a3-537">Dans la **configuration** de la solution, sélectionnez Déboguer.</span><span class="sxs-lookup"><span data-stu-id="016a3-537">In the **Solution Configuration** select **Debug**.</span></span>

    > <span data-ttu-id="016a3-538">Pour Microsoft HoloLens, il peut s’avérer plus facile de définir cette valeur sur *machine*distante, afin de ne pas être attaché à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="016a3-538">For the Microsoft HoloLens, you may find it easier to set this to *Remote Machine*, so that you are not tethered to your computer.</span></span> <span data-ttu-id="016a3-539">Toutefois, vous devez également effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="016a3-539">Though, you will need to also do the following:</span></span>
    > - <span data-ttu-id="016a3-540">Vous devez connaître l' **adresse IP** de votre HoloLens, qui se trouve dans les **paramètres** > **réseau &**  > **Options avancées**de**Wi-Fi** > Internet. IPv4 correspond à l’adresse que vous devez utiliser.</span><span class="sxs-lookup"><span data-stu-id="016a3-540">Know the **IP Address** of your HoloLens, which can be found within the **Settings** > **Network & Internet** > **Wi-Fi** > **Advanced Options**; the IPv4 is the address you should use.</span></span> 
    > - <span data-ttu-id="016a3-541">Assurez-vous que le **mode développeur** est **activé**; trouvé dans **paramètres** > **mise à jour & sécurité** > **pour les développeurs**.</span><span class="sxs-lookup"><span data-stu-id="016a3-541">Ensure **Developer Mode** is **On**; found in **Settings** > **Update & Security** > **For developers**.</span></span>

    ![déployer la solution](images/AzureLabs-Lab5-55.png)

4.  <span data-ttu-id="016a3-543">Accédez au menu **générer** , puis cliquez sur **déployer la solution** pour chargement l’application sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="016a3-543">Go to the **Build** menu and click on **Deploy Solution** to sideload the application to your machine.</span></span>

5.  <span data-ttu-id="016a3-544">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancées et testées.</span><span class="sxs-lookup"><span data-stu-id="016a3-544">Your App should now appear in the list of installed apps, ready to be launched and tested!</span></span>

## <a name="your-finished-azure-functions-and-storage-application"></a><span data-ttu-id="016a3-545">Votre application de Azure Functions et de stockage terminée</span><span class="sxs-lookup"><span data-stu-id="016a3-545">Your finished Azure Functions and Storage Application</span></span>

<span data-ttu-id="016a3-546">Félicitations, vous avez créé une application de réalité mixte qui tire parti des services de stockage Azure Functions et Azure.</span><span class="sxs-lookup"><span data-stu-id="016a3-546">Congratulations, you built a mixed reality app that leverages both the Azure Functions and Azure Storage services.</span></span> <span data-ttu-id="016a3-547">Votre application sera en mesure de dessiner sur des données stockées et de fournir une action basée sur ces données.</span><span class="sxs-lookup"><span data-stu-id="016a3-547">Your app will be able to draw on stored data, and provide an action based on that data.</span></span>

![fin du produit final](images/AzureLabs-Lab5-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="016a3-549">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="016a3-549">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="016a3-550">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="016a3-550">Exercise 1</span></span>

<span data-ttu-id="016a3-551">Créez un deuxième point de lancement et un autre enregistrement à partir duquel un objet a été créé.</span><span class="sxs-lookup"><span data-stu-id="016a3-551">Create a second spawn point and record which spawn point an object was created from.</span></span> <span data-ttu-id="016a3-552">Lorsque vous chargez le fichier de données, relisez les formes générées à partir de l’emplacement où elles ont été créées à l’origine.</span><span class="sxs-lookup"><span data-stu-id="016a3-552">When you load the data file, replay the shapes being spawned from the location they originally were created.</span></span>

### <a name="exercise-2"></a><span data-ttu-id="016a3-553">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="016a3-553">Exercise 2</span></span>

<span data-ttu-id="016a3-554">Créez un moyen de redémarrer l’application, au lieu de la rouvrir à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="016a3-554">Create a way to restart the app, rather than having to re-open it each time.</span></span> <span data-ttu-id="016a3-555">Le **chargement des scènes** est un bon point de départ.</span><span class="sxs-lookup"><span data-stu-id="016a3-555">**Loading Scenes** is a good spot to start.</span></span> <span data-ttu-id="016a3-556">Après cela, créez un moyen d’effacer la liste stockée dans le *stockage Azure*, afin qu’elle puisse être facilement réinitialisée à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="016a3-556">After doing that, create a way to clear the stored list in *Azure Storage*, so that it can be easily reset from your app.</span></span> 
