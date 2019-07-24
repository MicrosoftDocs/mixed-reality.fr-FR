---
title: RM et Azure 306-streaming video
description: Suivez ce cours pour apprendre à implémenter Azure Media Services dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, Media Services, streaming video, 360, immersif, VR
ms.openlocfilehash: f6974ab6a72828a557649d5dc65b4e505a7484ff
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63555880"
---
>[!NOTE]
><span data-ttu-id="e07eb-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="e07eb-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="e07eb-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="e07eb-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="e07eb-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="e07eb-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="e07eb-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e07eb-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="e07eb-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="e07eb-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="e07eb-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="e07eb-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br> 

# <a name="mr-and-azure-306-streaming-video"></a><span data-ttu-id="e07eb-110">MR et Azure 306: Diffusion vidéo en continu</span><span class="sxs-lookup"><span data-stu-id="e07eb-110">MR and Azure 306: Streaming video</span></span>

<span data-ttu-id="e07eb-111">![produit final-](images/AzureLabs-Lab6-00.png)
![début du produit final-début](images/AzureLabs-Lab6-01.png)</span><span class="sxs-lookup"><span data-stu-id="e07eb-111">![final product -start](images/AzureLabs-Lab6-00.png)
![final product -start](images/AzureLabs-Lab6-01.png)</span></span>

<span data-ttu-id="e07eb-112">Dans ce cours, vous allez apprendre comment connecter vos Azure Media Services à une expérience Windows Mixed Reality VR pour permettre une lecture vidéo en continu de 360 degrés sur des casques immersifs.</span><span class="sxs-lookup"><span data-stu-id="e07eb-112">In this course you will learn how connect your Azure Media Services to a Windows Mixed Reality VR experience to allow streaming 360 degree video playback on immersive headsets.</span></span> 

<span data-ttu-id="e07eb-113">**Azure Media Services** sont un ensemble de services qui vous offre des services de streaming vidéo de qualité broadcast pour atteindre un public plus large sur les appareils mobiles actuels les plus populaires.</span><span class="sxs-lookup"><span data-stu-id="e07eb-113">**Azure Media Services** are a collection of services that gives you broadcast-quality video streaming services to reach larger audiences on today’s most popular mobile devices.</span></span> <span data-ttu-id="e07eb-114">Pour plus d’informations, consultez la [page Azure Media Services](https://azure.microsoft.com/services/media-services).</span><span class="sxs-lookup"><span data-stu-id="e07eb-114">For more information, visit the [Azure Media Services page](https://azure.microsoft.com/services/media-services).</span></span>

<span data-ttu-id="e07eb-115">Une fois ce cours terminé, vous disposerez d’une application de casque d’immersion en réalité mixte, capable d’effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="e07eb-115">Having completed this course, you will have a mixed reality immersive headset application, which will be able to do the following:</span></span>

1. <span data-ttu-id="e07eb-116">Récupérez une vidéo de 360 degrés à partir d’un **stockage Azure**, via **Azure Media Service**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-116">Retrieve a 360 degree video from an **Azure Storage**, through the **Azure Media Service**.</span></span>

2. <span data-ttu-id="e07eb-117">Affichez la vidéo Récupérée de 360 degrés dans une scène Unity.</span><span class="sxs-lookup"><span data-stu-id="e07eb-117">Display the retrieved 360 degree video within a Unity scene.</span></span>

3. <span data-ttu-id="e07eb-118">Naviguer entre deux scènes, avec deux vidéos différentes.</span><span class="sxs-lookup"><span data-stu-id="e07eb-118">Navigate between two scenes, with two different videos.</span></span>

<span data-ttu-id="e07eb-119">Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception.</span><span class="sxs-lookup"><span data-stu-id="e07eb-119">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="e07eb-120">Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="e07eb-120">This course is designed to teach you how to integrate an Azure Service with your Unity Project.</span></span> <span data-ttu-id="e07eb-121">C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="e07eb-121">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

## <a name="device-support"></a><span data-ttu-id="e07eb-122">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="e07eb-122">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="e07eb-123">Course</span><span class="sxs-lookup"><span data-stu-id="e07eb-123">Course</span></span></th><th style="width:150px"> <span data-ttu-id="e07eb-124"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="e07eb-124"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="e07eb-125"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="e07eb-125"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="e07eb-126">MR et Azure 306: Diffusion vidéo en continu</span><span class="sxs-lookup"><span data-stu-id="e07eb-126">MR and Azure 306: Streaming video</span></span></td><td style="text-align: center;"> </td><td style="text-align: center;"> <span data-ttu-id="e07eb-127">✔️</span><span class="sxs-lookup"><span data-stu-id="e07eb-127">✔️</span></span></td>
</tr>
</table>

## <a name="prerequisites"></a><span data-ttu-id="e07eb-128">Prérequis</span><span class="sxs-lookup"><span data-stu-id="e07eb-128">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="e07eb-129">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="e07eb-129">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="e07eb-130">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="e07eb-130">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="e07eb-131">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l' [article installer les outils](install-the-tools.md), bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e07eb-131">You are free to use the latest software, as listed within the [install the tools article](install-the-tools.md), though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="e07eb-132">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:</span><span class="sxs-lookup"><span data-stu-id="e07eb-132">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="e07eb-133">Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)</span><span class="sxs-lookup"><span data-stu-id="e07eb-133">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="e07eb-134">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="e07eb-134">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="e07eb-135">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="e07eb-135">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="e07eb-136">Unity 2017,4</span><span class="sxs-lookup"><span data-stu-id="e07eb-136">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="e07eb-137">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e07eb-137">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="e07eb-138">Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md)</span><span class="sxs-lookup"><span data-stu-id="e07eb-138">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md)</span></span>
- <span data-ttu-id="e07eb-139">Accès Internet pour l’installation d’Azure et la récupération de données</span><span class="sxs-lookup"><span data-stu-id="e07eb-139">Internet access for Azure setup and data retrieval</span></span>
- <span data-ttu-id="e07eb-140">Vidéos de 2 360 degrés au format MP4 (vous trouverez des vidéos gratuites sur les redevances dans [cette page de téléchargement](https://www.mettle.com/360vr-master-series-free-360-downloads-page))</span><span class="sxs-lookup"><span data-stu-id="e07eb-140">Two 360-degree videos in mp4 format (you can find some royalty-free videos [at this download page](https://www.mettle.com/360vr-master-series-free-360-downloads-page))</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e07eb-141">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e07eb-141">Before you start</span></span>

1.  <span data-ttu-id="e07eb-142">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="e07eb-142">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="e07eb-143">Configurez et testez votre casque immersif en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="e07eb-143">Set up and test your Mixed Reality Immersive Headset.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e07eb-144">Vous n’aurez **pas** besoin de contrôleurs de mouvement pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="e07eb-144">You will **not** require Motion Controllers for this course.</span></span> <span data-ttu-id="e07eb-145">Si vous avez besoin de la prise en charge de la configuration du casque immersif, cliquez sur [le lien pour configurer Windows Mixed Reality](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span><span class="sxs-lookup"><span data-stu-id="e07eb-145">If you need support setting up the Immersive Headset, please click [link on how to set up Windows Mixed Reality](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span></span>

## <a name="chapter-1---the-azure-portal-creating-the-azure-storage-account"></a><span data-ttu-id="e07eb-146">Chapitre 1-portail Azure: création du compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="e07eb-146">Chapter 1 - The Azure Portal: creating the Azure Storage Account</span></span>

<span data-ttu-id="e07eb-147">Pour utiliser le **service de stockage Azure**, vous devez créer et configurer un **compte de stockage** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e07eb-147">To use the **Azure Storage Service**, you will need to create and configure a **Storage Account** in the Azure portal.</span></span>

1.  <span data-ttu-id="e07eb-148">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e07eb-148">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE]
    > <span data-ttu-id="e07eb-149">Si vous n’avez pas encore de compte Azure, vous devez en créer un.</span><span class="sxs-lookup"><span data-stu-id="e07eb-149">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="e07eb-150">Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="e07eb-150">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="e07eb-151">Une fois que vous êtes connecté, cliquez sur **comptes de stockage** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="e07eb-151">Once you are logged in, click on **Storage accounts** in the left menu.</span></span>

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab6-02.png)

3.  <span data-ttu-id="e07eb-153">Dans l’onglet **comptes de stockage** , cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-153">On the **Storage Accounts** tab, click on **Add**.</span></span>

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab6-03.png)

4.  <span data-ttu-id="e07eb-155">Dans l’onglet **créer un compte de stockage** :</span><span class="sxs-lookup"><span data-stu-id="e07eb-155">In the **Create storage account** tab:</span></span>

    1.  <span data-ttu-id="e07eb-156">Insérez un **nom** pour votre compte. n’oubliez pas que ce champ accepte uniquement des chiffres et des lettres minuscules.</span><span class="sxs-lookup"><span data-stu-id="e07eb-156">Insert a **Name** for your account, be aware this field only accepts numbers, and lowercase letters.</span></span>

    2.  <span data-ttu-id="e07eb-157">Pour **modèle de déploiement,** sélectionnez Resource **Manager**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-157">For **Deployment model,** select **Resource manager**.</span></span>

    3.  <span data-ttu-id="e07eb-158">Pour **type de compte**, sélectionnez **stockage (à usage général v1)** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-158">For **Account kind**, select **Storage (general purpose v1)**.</span></span>

    4.  <span data-ttu-id="e07eb-159">Pour **performances**, sélectionnez **Standard\*.**</span><span class="sxs-lookup"><span data-stu-id="e07eb-159">For **Performance**, select **Standard\*.**</span></span>

    5.  <span data-ttu-id="e07eb-160">Pour **la réplication** , sélectionnez **stockage localement redondant (LRS)** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-160">For **Replication** select **Locally-redundant storage (LRS)**.</span></span>

    6.  <span data-ttu-id="e07eb-161">Laissez le **transfert sécurisé requis** comme **désactivé**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-161">Leave **Secure transfer required** as **Disabled**.</span></span>

    7.  <span data-ttu-id="e07eb-162">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-162">Select a **Subscription**.</span></span>

    8.  <span data-ttu-id="e07eb-163">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="e07eb-163">Choose a **Resource group** or create a new one.</span></span> <span data-ttu-id="e07eb-164">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="e07eb-164">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span>

    9.  <span data-ttu-id="e07eb-165">Déterminez l' **emplacement** de votre groupe de ressources (si vous créez un groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="e07eb-165">Determine the **Location** for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="e07eb-166">L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait.</span><span class="sxs-lookup"><span data-stu-id="e07eb-166">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="e07eb-167">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="e07eb-167">Some Azure assets are only available in certain regions.</span></span>

5.  <span data-ttu-id="e07eb-168">Vous devrez confirmer que vous avez compris les conditions générales appliquées à ce service.</span><span class="sxs-lookup"><span data-stu-id="e07eb-168">You will need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab6-04.png)

6.  <span data-ttu-id="e07eb-170">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="e07eb-170">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

7.  <span data-ttu-id="e07eb-171">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="e07eb-171">A notification will appear in the portal once the Service instance is created.</span></span>

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab6-05.png)

8.  <span data-ttu-id="e07eb-173">À ce stade, vous n’avez pas besoin de suivre la ressource. passez simplement au chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="e07eb-173">At this point you do not need to follow the resource, simply move to the next Chapter.</span></span>

## <a name="chapter-2---the-azure-portal-creating-the-media-service"></a><span data-ttu-id="e07eb-174">Chapitre 2-portail Azure: création du service multimédia</span><span class="sxs-lookup"><span data-stu-id="e07eb-174">Chapter 2 - The Azure Portal: creating the Media Service</span></span>

<span data-ttu-id="e07eb-175">Pour utiliser Azure Media Service, vous devez configurer une instance du service à mettre à la disposition de votre application (où le détenteur du compte doit être un administrateur).</span><span class="sxs-lookup"><span data-stu-id="e07eb-175">To use the Azure Media Service, you will need to configure an instance of the service to be made available to your application (wherein the account holder needs to be an Admin).</span></span>

1.  <span data-ttu-id="e07eb-176">Dans le portail Azure, cliquez sur **créer une ressource** dans le coin supérieur gauche et recherchez **Media Service,** puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-176">In the Azure Portal, click on **Create a resource** in the top left corner, and search for **Media Service,** press **Enter**.</span></span> <span data-ttu-id="e07eb-177">La ressource à laquelle vous souhaitez appliquer actuellement une icône rose; Cliquez sur cette valeur pour afficher une nouvelle page.</span><span class="sxs-lookup"><span data-stu-id="e07eb-177">The resource you want currently has a pink icon; click this, to show a new page.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-06.png)

2.  <span data-ttu-id="e07eb-179">La nouvelle page fournit une description du **service multimédia**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-179">The new page will provide a description of the **Media Service**.</span></span> <span data-ttu-id="e07eb-180">En bas à gauche de cette invite, cliquez sur le bouton **créer** pour créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="e07eb-180">At the bottom left of this prompt, click the **Create** button, to create an association with this service.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-07.png)

3.  <span data-ttu-id="e07eb-182">Une fois que vous avez cliqué sur **créer** , un panneau s’affiche pour vous permettre de fournir des détails sur votre nouveau service multimédia:</span><span class="sxs-lookup"><span data-stu-id="e07eb-182">Once you have clicked on **Create** a panel will appear where you need to provide some details about your new Media Service:</span></span>

    1.  <span data-ttu-id="e07eb-183">Insérez le nom de votre **compte** souhaité pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="e07eb-183">Insert your desired **Account Name** for this service instance.</span></span>

    2.  <span data-ttu-id="e07eb-184">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-184">Select a **Subscription**.</span></span>

    3. <span data-ttu-id="e07eb-185">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="e07eb-185">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="e07eb-186">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="e07eb-186">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="e07eb-187">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun).</span><span class="sxs-lookup"><span data-stu-id="e07eb-187">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span> 
    
    > <span data-ttu-id="e07eb-188">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, cliquez [sur le lien suivant pour gérer les groupes de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="e07eb-188">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage Azure Resource Groups](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    4.  <span data-ttu-id="e07eb-189">Déterminez l' **emplacement** de votre groupe de ressources (si vous créez un groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="e07eb-189">Determine the **Location** for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="e07eb-190">L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait.</span><span class="sxs-lookup"><span data-stu-id="e07eb-190">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="e07eb-191">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="e07eb-191">Some Azure assets are only available in certain regions.</span></span>

    5.  <span data-ttu-id="e07eb-192">Pour la section **compte de stockage** , cliquez sur la section **Veuillez sélectionner..** ., puis cliquez sur le compte de **stockage** que vous avez créé dans le dernier chapitre.</span><span class="sxs-lookup"><span data-stu-id="e07eb-192">For the **Storage Account** section, click the **Please select...** section, then click the **Storage Account** you created in the last Chapter.</span></span>

    6.  <span data-ttu-id="e07eb-193">Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.</span><span class="sxs-lookup"><span data-stu-id="e07eb-193">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    7.  <span data-ttu-id="e07eb-194">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-194">Click **Create**.</span></span>

        ![Le portail Azure](images/AzureLabs-Lab6-08.png)

4.  <span data-ttu-id="e07eb-196">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="e07eb-196">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

5.  <span data-ttu-id="e07eb-197">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="e07eb-197">A notification will appear in the portal once the Service instance is created.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-09.png)

6.  <span data-ttu-id="e07eb-199">Cliquez sur la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="e07eb-199">Click on the notification to explore your new Service instance.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-10.png)

7.  <span data-ttu-id="e07eb-201">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="e07eb-201">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span>

8.  <span data-ttu-id="e07eb-202">Dans la page nouveau service multimédia, dans le volet de gauche, cliquez sur le lien **ressources** , qui est à mi-chemin.</span><span class="sxs-lookup"><span data-stu-id="e07eb-202">Within the new Media service page, within the panel on the left, click on the **Assets** link, which is about halfway down.</span></span>

9.  <span data-ttu-id="e07eb-203">Sur la page suivante, dans le coin supérieur gauche de la page, cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-203">On the next page, in the top-left corner of the page, click **Upload**.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-11.png)

10. <span data-ttu-id="e07eb-205">Cliquez sur l’icône de **dossier** pour parcourir vos fichiers et sélectionnez la première vidéo 360 que vous souhaitez diffuser en continu.</span><span class="sxs-lookup"><span data-stu-id="e07eb-205">Click on the **Folder** icon to browse your files and select the first 360 Video that you would like to stream.</span></span> 
    
    > <span data-ttu-id="e07eb-206">Vous pouvez suivre ce [lien pour télécharger un exemple de vidéo](https://vimeo.com/214401712).</span><span class="sxs-lookup"><span data-stu-id="e07eb-206">You can follow this [link to download a sample video](https://vimeo.com/214401712).</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-12.png)

> [!WARNING]
> <span data-ttu-id="e07eb-208">Les noms de fichiers longs peuvent entraîner un problème avec l’encodeur: ainsi, pour vous assurer que les vidéos n’ont pas de problèmes, envisagez de raccourcir la longueur des noms de vos fichiers vidéo.</span><span class="sxs-lookup"><span data-stu-id="e07eb-208">Long filenames may cause an issue with the encoder: so to ensure videos do not have issues, consider shortening the length of your video file names.</span></span>

11. <span data-ttu-id="e07eb-209">La barre de progression devient verte lorsque le chargement de la vidéo est terminé.</span><span class="sxs-lookup"><span data-stu-id="e07eb-209">The progress bar will turn green when the video has finished uploading.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-13.png)

12. <span data-ttu-id="e07eb-211">Cliquez sur le texte ci-dessus (**yourservicename-Assets**) pour revenir à la page **composants** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-211">Click on the text above (**yourservicename - Assets**) to return to the **Assets** page.</span></span>

13. <span data-ttu-id="e07eb-212">Vous remarquerez que votre vidéo a été chargée avec succès.</span><span class="sxs-lookup"><span data-stu-id="e07eb-212">You will notice that your video has been successfully uploaded.</span></span> <span data-ttu-id="e07eb-213">Cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="e07eb-213">Click on it.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-14.png)

14. <span data-ttu-id="e07eb-215">La page que vous avez redirigée affiche des informations détaillées sur votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="e07eb-215">The page you are redirected to will show you detailed information about your video.</span></span> <span data-ttu-id="e07eb-216">Pour pouvoir utiliser votre vidéo, vous devez l’encoder en cliquant sur le  bouton encoder en haut à gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="e07eb-216">To be able to use your video you need to encode it, by clicking the **Encode** button at the top-left of the page.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-15.png)

15. <span data-ttu-id="e07eb-218">Un nouveau panneau s’affiche à droite, dans lequel vous pouvez définir des options d’encodage pour votre fichier.</span><span class="sxs-lookup"><span data-stu-id="e07eb-218">A new panel will appear to the right, where you will be able to set encoding options for your file.</span></span> <span data-ttu-id="e07eb-219">Définissez les propriétés suivantes (certaines seront déjà définies par défaut):</span><span class="sxs-lookup"><span data-stu-id="e07eb-219">Set the following properties (some will be already set by default):</span></span>

    1.  <span data-ttu-id="e07eb-220">**Nom de l’encodeur multimédia *Media Encoder standard***</span><span class="sxs-lookup"><span data-stu-id="e07eb-220">**Media encoder name *Media Encoder Standard***</span></span>

    2.  <span data-ttu-id="e07eb-221">**Encodage de *contenu prédéfini données à débit binaire multiple MP4***</span><span class="sxs-lookup"><span data-stu-id="e07eb-221">**Encoding preset *Content Adaptive Multiple Bitrate MP4***</span></span>

    3.  <span data-ttu-id="e07eb-222">**Nom *du travail Media Encoder standard traitement de VIDEO1. MP4***</span><span class="sxs-lookup"><span data-stu-id="e07eb-222">**Job name *Media Encoder Standard processing of Video1.mp4***</span></span>

    4.  <span data-ttu-id="e07eb-223">**Output Media Media name *VIDEO1. MP4--Media Encoder standard encodé***</span><span class="sxs-lookup"><span data-stu-id="e07eb-223">**Output media asset name *Video1.mp4 -- Media Encoder Standard encoded***</span></span>

        ![Le portail Azure](images/AzureLabs-Lab6-16.png)

16. <span data-ttu-id="e07eb-225">Cliquez sur le bouton **Créer**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-225">Click the **Create** button.</span></span>

17. <span data-ttu-id="e07eb-226">Vous remarquerez une barre avec un **travail d’encodage ajouté**, cliquez sur cette barre et un panneau s’affichera avec la progression de l’encodage affichée.</span><span class="sxs-lookup"><span data-stu-id="e07eb-226">You will notice a bar with **Encoding job added**, click on that bar and a panel will appear with the Encoding progress displayed in it.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-17.png)

    ![Le portail Azure](images/AzureLabs-Lab6-18.png)

18. <span data-ttu-id="e07eb-229">Attendez que le travail soit terminé.</span><span class="sxs-lookup"><span data-stu-id="e07eb-229">Wait for the Job to be completed.</span></span> <span data-ttu-id="e07eb-230">Une fois l’opération terminée, n’hésitez pas à fermer le panneau avec le «X» en haut à droite de ce panneau.</span><span class="sxs-lookup"><span data-stu-id="e07eb-230">Once it is done, feel free to close the panel with the 'X' at the top right of that panel.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-19.png)

    ![Le portail Azure](images/AzureLabs-Lab6-20.png)

    > [!IMPORTANT]
    > <span data-ttu-id="e07eb-233">Le temps nécessaire dépend de la taille de fichier de votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="e07eb-233">The time this takes, depends on the file size of your video.</span></span> <span data-ttu-id="e07eb-234">Ce processus peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="e07eb-234">This process can take quite some time.</span></span>

19. <span data-ttu-id="e07eb-235">Maintenant que la version encodée de la vidéo a été créée, vous pouvez la publier pour la rendre accessible.</span><span class="sxs-lookup"><span data-stu-id="e07eb-235">Now that the encoded version of the video has been created, you can publish it to make it accessible.</span></span> <span data-ttu-id="e07eb-236">Pour ce faire, cliquez sur les **éléments** de lien Blue pour revenir à la page composants.</span><span class="sxs-lookup"><span data-stu-id="e07eb-236">To do so, click the blue link **Assets** to go back to the assets page.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-21.png)

20. <span data-ttu-id="e07eb-238">Vous verrez votre vidéo, ainsi que l’autre, ce qui est de \*\*Type de ressource \*MP4 multidébit\*\*\*.</span><span class="sxs-lookup"><span data-stu-id="e07eb-238">You will see your video along with another, which is of \*\*Asset Type \*Multi-Bitrate MP4\*\*\*.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-22.png)

    > [!NOTE] 
    > <span data-ttu-id="e07eb-240">Vous remarquerez peut-être que la nouvelle ressource, avec votre vidéo initiale, est *inconnue*et a une valeur de «0» octets pour sa **taille**, actualisez simplement votre fenêtre pour qu’elle soit mise à jour.</span><span class="sxs-lookup"><span data-stu-id="e07eb-240">You may notice that the new asset, alongside your initial video, is *Unknown*, and has '0' bytes for it's **Size**, just refresh your window for it to update.</span></span>

21. <span data-ttu-id="e07eb-241">Cliquez sur ce nouvel élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="e07eb-241">Click this new asset.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-23.png)

22. <span data-ttu-id="e07eb-243">Vous verrez un panneau similaire à celui que vous avez utilisé précédemment, mais il s’agit d’une autre ressource.</span><span class="sxs-lookup"><span data-stu-id="e07eb-243">You will see a similar panel to the one you used before, just this is a different asset.</span></span> <span data-ttu-id="e07eb-244">Cliquez sur le bouton **publier** situé en haut au centre de la page.</span><span class="sxs-lookup"><span data-stu-id="e07eb-244">Click the **Publish** button located at the top-center of the page.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-24.png)

23. <span data-ttu-id="e07eb-246">Vous serez invité à définir un **localisateur**, qui est le point d’entrée, dans les fichiers de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="e07eb-246">You will be prompted to set a **Locator**, which is the entry point, to file/s in your Assets.</span></span> <span data-ttu-id="e07eb-247">Pour votre scénario, définissez les propriétés suivantes:</span><span class="sxs-lookup"><span data-stu-id="e07eb-247">For your scenario set the following properties:</span></span>

    1.  <span data-ttu-id="e07eb-248">**Type de localisateur**progressif. > </span><span class="sxs-lookup"><span data-stu-id="e07eb-248">**Locator type** > **Progressive**.</span></span>

    2.  <span data-ttu-id="e07eb-249">La **Date** et l' **heure** seront définies pour vous, à partir de la date actuelle, à une heure future (100 ans dans le cas présent).</span><span class="sxs-lookup"><span data-stu-id="e07eb-249">The **date** and **time** will be set for you, from your current date, to a time in the future (one hundred years in this case).</span></span> <span data-ttu-id="e07eb-250">Laissez tel quel ou modifiez-le pour l’adapter à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="e07eb-250">Leave as is or change it to suit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e07eb-251">Pour plus d’informations sur les localisateurs et sur ce que vous pouvez choisir, consultez la [Documentation Azure Media Services](https://docs.microsoft.com/azure/media-services/media-services-concepts).</span><span class="sxs-lookup"><span data-stu-id="e07eb-251">For more information about Locators, and what you can choose, visit the [Azure Media Services Documentation](https://docs.microsoft.com/azure/media-services/media-services-concepts).</span></span>

24. <span data-ttu-id="e07eb-252">En bas de ce panneau, cliquez sur le bouton **Ajouter** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-252">At the bottom of that panel, click on the **Add** button.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-25.png)

25. <span data-ttu-id="e07eb-254">Votre vidéo est maintenant publiée et peut être diffusée en continu à l’aide de son point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="e07eb-254">Your video is now published and can be streamed by using its endpoint.</span></span> <span data-ttu-id="e07eb-255">Plus loin dans la page, il s’agit d’une section de **fichiers** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-255">Further down the page is a **Files** section.</span></span> <span data-ttu-id="e07eb-256">C’est là que se trouvent les différentes versions encodées de votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="e07eb-256">This is where the different encoded versions of your video will be.</span></span> <span data-ttu-id="e07eb-257">Sélectionnez la résolution la plus élevée possible (dans l’image ci-dessous est le fichier 1920x960), puis un panneau à droite s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e07eb-257">Select the highest possible resolution one (in the image below it is the 1920x960 file), and then a panel to the right will appear.</span></span> <span data-ttu-id="e07eb-258">Vous y trouverez une **URL de téléchargement**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-258">There you will find a **Download URL**.</span></span> <span data-ttu-id="e07eb-259">Copiez ce **point de terminaison** , car vous allez l’utiliser ultérieurement dans votre code.</span><span class="sxs-lookup"><span data-stu-id="e07eb-259">Copy this **Endpoint** as you will use it later in your code.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-26.png)    

    ![Le portail Azure](images/AzureLabs-Lab6-27.png)

    > [!NOTE] 
    > <span data-ttu-id="e07eb-262">Vous pouvez également appuyer sur le bouton de **lecture** pour lire votre vidéo et la tester.</span><span class="sxs-lookup"><span data-stu-id="e07eb-262">You can also press the **Play** button to play your video and test it.</span></span>

26. <span data-ttu-id="e07eb-263">Vous devez maintenant télécharger la deuxième vidéo que vous allez utiliser dans ce laboratoire.</span><span class="sxs-lookup"><span data-stu-id="e07eb-263">You now need to upload the second video that you will use in this Lab.</span></span> <span data-ttu-id="e07eb-264">Suivez les étapes ci-dessus, en répétant la même procédure pour la deuxième vidéo.</span><span class="sxs-lookup"><span data-stu-id="e07eb-264">Follow the steps above, repeating the same process for the second video.</span></span> <span data-ttu-id="e07eb-265">Veillez à copier également le deuxième **point de terminaison** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-265">Ensure you copy the second **Endpoint** also.</span></span> <span data-ttu-id="e07eb-266">Utilisez le [lien suivant pour télécharger une deuxième vidéo](https://vimeo.com/214402865).</span><span class="sxs-lookup"><span data-stu-id="e07eb-266">Use the following [link to download a second video](https://vimeo.com/214402865).</span></span>

27. <span data-ttu-id="e07eb-267">Une fois les deux vidéos publiées, vous êtes prêt à passer au chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="e07eb-267">Once both videos have been published, you are ready to move to the next Chapter.</span></span>

## <a name="chapter-3---setting-up-the-unity-project"></a><span data-ttu-id="e07eb-268">Chapitre 3-Configuration du projet Unity</span><span class="sxs-lookup"><span data-stu-id="e07eb-268">Chapter 3 - Setting up the Unity Project</span></span>

<span data-ttu-id="e07eb-269">Ce qui suit est une configuration classique pour le développement avec la réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="e07eb-269">The following is a typical set up for developing with the Mixed Reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="e07eb-270">Ouvrez **Unity** et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-270">Open **Unity** and click **New**.</span></span> 

    ![Le portail Azure](images/AzureLabs-Lab6-28.png)

2.  <span data-ttu-id="e07eb-272">Vous devez maintenant fournir un nom de projet Unity, insérer **Mr\_360VideoStreaming.** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-272">You will now need to provide a Unity Project name, insert **MR\_360VideoStreaming.**.</span></span> <span data-ttu-id="e07eb-273">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-273">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="e07eb-274">Définissez l’emplacement approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés).</span><span class="sxs-lookup"><span data-stu-id="e07eb-274">Set the Location to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="e07eb-275">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-275">Then, click **Create project**.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-29.png)

3.  <span data-ttu-id="e07eb-277">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="e07eb-277">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio.**</span></span> <span data-ttu-id="e07eb-278">Accédez à ***modifier* les *Préférences*** , puis à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-278">Go to ***Edit* *Preferences*** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="e07eb-279">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-279">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="e07eb-280">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-280">Close the **Preferences** window.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-30.png)

4.  <span data-ttu-id="e07eb-282">Ensuite, accédez à ***fichier* *paramètres de build*** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton **changer de plateforme** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-282">Next, go to ***File* *Build Settings*** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

5.  <span data-ttu-id="e07eb-283">Assurez-vous également que:</span><span class="sxs-lookup"><span data-stu-id="e07eb-283">Also make sure that:</span></span>

    1. <span data-ttu-id="e07eb-284">L' **appareil cible** est défini sur **n’importe quel appareil.**</span><span class="sxs-lookup"><span data-stu-id="e07eb-284">**Target Device** is set to **Any Device.**</span></span>
    
    2.  <span data-ttu-id="e07eb-285">Le **type de build** est **D3D.**</span><span class="sxs-lookup"><span data-stu-id="e07eb-285">**Build Type** is set to **D3D.**</span></span>

    3.  <span data-ttu-id="e07eb-286">Le **SDK** est configuré sur le **dernier installé.**</span><span class="sxs-lookup"><span data-stu-id="e07eb-286">**SDK** is set to **Latest installed.**</span></span>

    4.  <span data-ttu-id="e07eb-287">La **version de Visual Studio** est **installée sur le plus récent.**</span><span class="sxs-lookup"><span data-stu-id="e07eb-287">**Visual Studio Version** is set to **Latest installed.**</span></span>

    5.  <span data-ttu-id="e07eb-288">La **génération et l’exécution** sont définies sur l' **ordinateur local.**</span><span class="sxs-lookup"><span data-stu-id="e07eb-288">**Build and Run** is set to **Local Machine.**</span></span>

    6.  <span data-ttu-id="e07eb-289">Ne vous inquiétez pas de définir des **scènes** pour le moment, car vous allez les configurer ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="e07eb-289">Do not worry about setting up **Scenes** right now, as you will set these up later.</span></span>

    7.  <span data-ttu-id="e07eb-290">Les paramètres restants doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="e07eb-290">The remaining settings should be left as default for now.</span></span>

        ![Configuration du projet Unity](images/AzureLabs-Lab6-31.png)

6.  <span data-ttu-id="e07eb-292">Dans la fenêtre **paramètres de build** , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-292">In the **Build Settings** window, click on the **Player Settings** button, this will open the related panel in the space where the **Inspector** is located.</span></span> 

7. <span data-ttu-id="e07eb-293">Dans ce volet, quelques paramètres doivent être vérifiés:</span><span class="sxs-lookup"><span data-stu-id="e07eb-293">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="e07eb-294">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="e07eb-294">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="e07eb-295">**Scripts** La **version du runtime** doit être **stable** (équivalent .net 3,5).</span><span class="sxs-lookup"><span data-stu-id="e07eb-295">**Scripting** **Runtime Version** should be **Stable** (.NET 3.5 Equivalent).</span></span>

        2. <span data-ttu-id="e07eb-296">Le **serveur principal de script** doit être **.net.**</span><span class="sxs-lookup"><span data-stu-id="e07eb-296">**Scripting Backend** should be **.NET.**</span></span>

        3. <span data-ttu-id="e07eb-297">Le **niveau de compatibilité** de l’API doit être **.net 4,6.**</span><span class="sxs-lookup"><span data-stu-id="e07eb-297">**API Compatibility Level** should be **.NET 4.6.**</span></span>

            ![Configuration du projet Unity](images/AzureLabs-Lab6-32.png)

    2.  <span data-ttu-id="e07eb-299">Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="e07eb-299">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Configuration du projet Unity](images/AzureLabs-Lab6-33.png)

    3.  <span data-ttu-id="e07eb-301">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:</span><span class="sxs-lookup"><span data-stu-id="e07eb-301">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="e07eb-302">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="e07eb-302">**InternetClient**</span></span>

            ![Configuration du projet Unity](images/AzureLabs-Lab6-34.png)

8.  <span data-ttu-id="e07eb-304">Une fois ces modifications effectuées, fermez la fenêtre **paramètres de build** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-304">Once you have made those changes, close the **Build Settings** window.</span></span>

9.  <span data-ttu-id="e07eb-305">Enregistrer votre projet \**fichier* \*enregistrer projet \*\*.</span><span class="sxs-lookup"><span data-stu-id="e07eb-305">Save your Project \**File* \*Save Project\*\*.</span></span>



## <a name="chapter-4---importing-the-insideoutsphere-unity-package"></a><span data-ttu-id="e07eb-306">Chapitre 4-importation du package InsideOutSphere Unity</span><span class="sxs-lookup"><span data-stu-id="e07eb-306">Chapter 4 - Importing the InsideOutSphere Unity package</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e07eb-307">Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce fichier [. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20306%20-%20Streaming%20video/Azure-MR-306.unitypackage), à l’importer dans votre projet en tant que [**package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis à passer au **Chapitre 5**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-307">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to download this [.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20306%20-%20Streaming%20video/Azure-MR-306.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from **Chapter 5**.</span></span> <span data-ttu-id="e07eb-308">Vous devrez toujours créer un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="e07eb-308">You will still need to create a Unity Project.</span></span>

<span data-ttu-id="e07eb-309">Pour ce cours, vous devez télécharger un package d’actifs Unity appelé [**InsideOutSphere. pour Unity**](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20306%20-%20Streaming%20video/InsideOutSphere.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="e07eb-309">For this course you will need to download a Unity Asset Package called [**InsideOutSphere.unitypackage**](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20306%20-%20Streaming%20video/InsideOutSphere.unitypackage).</span></span>

<span data-ttu-id="e07eb-310">Comment importer les **pour Unity**:</span><span class="sxs-lookup"><span data-stu-id="e07eb-310">How-to import the **unitypackage**:</span></span>

1.  <span data-ttu-id="e07eb-311">Avec le tableau de bord Unity devant vous, cliquez sur **ressources** dans le menu en haut de l’écran, puis sur **importer le package > package personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-311">With the Unity dashboard in front of you, click on **Assets** in the menu at the top of the screen, then click on **Import Package > Custom Package**.</span></span>

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-35.png)

2.  <span data-ttu-id="e07eb-313">Utilisez le sélecteur de fichiers pour sélectionner le package **InsideOutSphere. pour Unity** , puis cliquez sur **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-313">Use the file picker to select the **InsideOutSphere.unitypackage** package and click **Open**.</span></span> <span data-ttu-id="e07eb-314">La liste des composants de cet élément multimédia vous est présentée.</span><span class="sxs-lookup"><span data-stu-id="e07eb-314">A list of components for this asset will be displayed to you.</span></span> <span data-ttu-id="e07eb-315">Confirmez l’importation en cliquant sur **Importer**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-315">Confirm the import by clicking **Import**.</span></span>

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-36.png)

3.  <span data-ttu-id="e07eb-317">Une fois l’importation terminée, vous remarquerez que trois nouveaux dossiers, **matériaux**, **modèles**et **Prefabs**ont été ajoutés à votre dossier de **ressources** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-317">Once it has finished importing, you will notice three new folders, **Materials**, **Models**, and **Prefabs**, have been added to your **Assets** folder.</span></span> <span data-ttu-id="e07eb-318">Ce type de structure de dossiers est courant pour un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="e07eb-318">This kind of folder structure is typical for a Unity project.</span></span>

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-37.png)

    1.  <span data-ttu-id="e07eb-320">Ouvrez le  dossier Models, et vous verrez que le modèle **InsideOutSphere** a été importé.</span><span class="sxs-lookup"><span data-stu-id="e07eb-320">Open the **Models** folder, and you will see that the **InsideOutSphere** model has been imported.</span></span>

    2.  <span data-ttu-id="e07eb-321">Dans le  dossier Materials, vous trouverez la *Lambert1*de matériau **InsideOutSpheres** , ainsi qu’un document appelé *ButtonMaterial*, qui est utilisé par le GazeButton, que vous verrez bientôt.</span><span class="sxs-lookup"><span data-stu-id="e07eb-321">Within the **Materials** folder you will find the **InsideOutSpheres** material  *lambert1*, along with a material called *ButtonMaterial*, which is used by the GazeButton, which you will see soon.</span></span>

    3.  <span data-ttu-id="e07eb-322">Le dossier **Prefabs** contient le Prefab **InsideOutSphere** qui contient à la fois le *modèle* **InsideOutSphere** et le *GazeButton*.</span><span class="sxs-lookup"><span data-stu-id="e07eb-322">The **Prefabs** folder contains the **InsideOutSphere** prefab which contains both the **InsideOutSphere** *model* and the *GazeButton*.</span></span>

    4.  <span data-ttu-id="e07eb-323">**Aucun code n’est inclus**, vous allez écrire le code en suivant ce cours.</span><span class="sxs-lookup"><span data-stu-id="e07eb-323">**No code is included**, you will write the code by following this course.</span></span>


4.  <span data-ttu-id="e07eb-324">Dans la **hiérarchie**, sélectionnez l’objet **Camera principal** et mettez à jour les composants suivants:</span><span class="sxs-lookup"><span data-stu-id="e07eb-324">Within the **Hierarchy**, select the **Main Camera** object, and update the following components:</span></span>

    1.  <span data-ttu-id="e07eb-325">**Modifiez**</span><span class="sxs-lookup"><span data-stu-id="e07eb-325">**Transform**</span></span>

        1.  <span data-ttu-id="e07eb-326">Position = **X**: 0, **Y**: 0, **Z**: 0.</span><span class="sxs-lookup"><span data-stu-id="e07eb-326">Position = **X**: 0, **Y**: 0, **Z**: 0.</span></span>

        2. <span data-ttu-id="e07eb-327">Rotation = **X**: 0, **Y**: 0, **Z**: 0.</span><span class="sxs-lookup"><span data-stu-id="e07eb-327">Rotation = **X**: 0, **Y**: 0, **Z**: 0.</span></span>

        3. <span data-ttu-id="e07eb-328">Échelle **X**: 1, **Y**: 1, **Z**: 1.</span><span class="sxs-lookup"><span data-stu-id="e07eb-328">Scale **X**: 1, **Y**: 1, **Z**: 1.</span></span>

    2.  <span data-ttu-id="e07eb-329">**Appareil photo**</span><span class="sxs-lookup"><span data-stu-id="e07eb-329">**Camera**</span></span>

        1. <span data-ttu-id="e07eb-330">**Indicateurs**d’effacement: Couleur unie.</span><span class="sxs-lookup"><span data-stu-id="e07eb-330">**Clear Flags**: Solid Color.</span></span>

        2.  <span data-ttu-id="e07eb-331">**Plans**de découpage: Située 0,1, Far: 6.</span><span class="sxs-lookup"><span data-stu-id="e07eb-331">**Clipping Planes**: Near: 0.1, Far: 6.</span></span>

            ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-38.png)

5.  <span data-ttu-id="e07eb-333">Accédez au dossier **Prefab** , puis faites glisser le Prefab **InsideOutSphere** dans le panneau de **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-333">Navigate to the **Prefab** folder, and then drag the **InsideOutSphere** prefab into the **Hierarchy** Panel.</span></span>

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-39.png)

6.  <span data-ttu-id="e07eb-335">Développez l’objet **InsideOutSphere** dans la **hiérarchie** en cliquant sur la petite flèche en regard de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="e07eb-335">Expand the **InsideOutSphere** object within the **Hierarchy** by clicking the little arrow next to it.</span></span> <span data-ttu-id="e07eb-336">Vous verrez un objet **enfant** sous celui-ci appelé **GazeButton**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-336">You will see a **child** object beneath it called **GazeButton**.</span></span> <span data-ttu-id="e07eb-337">Ce sera utilisé pour modifier les scènes et, par conséquent, les vidéos.</span><span class="sxs-lookup"><span data-stu-id="e07eb-337">This will be used to change scenes and thus videos.</span></span>

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-40.png)

7.  <span data-ttu-id="e07eb-339">Dans la fenêtre de l’inspecteur, cliquez sur le composant transformer du **InsideOutSphere**, vérifiez que les propriétés suivantes sont définies:</span><span class="sxs-lookup"><span data-stu-id="e07eb-339">In the Inspector Window click on the **InsideOutSphere**'s Transform component, ensure that the following properties are set:</span></span>

    |            |    <span data-ttu-id="e07eb-340">TRANSFORMATION-POSITION</span><span class="sxs-lookup"><span data-stu-id="e07eb-340">TRANSFORM - POSITION</span></span>   |           |
    | :---------:| :-----------------------: | :--------:|
    |   <span data-ttu-id="e07eb-341">**X** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-341">**X** 0</span></span>  |          <span data-ttu-id="e07eb-342">**Y** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-342">**Y** 0</span></span>          |  <span data-ttu-id="e07eb-343">**Z** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-343">**Z** 0</span></span>  |

    |            |    <span data-ttu-id="e07eb-344">TRANSFORMATION-ROTATION</span><span class="sxs-lookup"><span data-stu-id="e07eb-344">TRANSFORM - ROTATION</span></span>   |           |
    | :---------:| :-----------------------: | :--------:|
    |   <span data-ttu-id="e07eb-345">**X** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-345">**X** 0</span></span>  |          <span data-ttu-id="e07eb-346">**Y** -50</span><span class="sxs-lookup"><span data-stu-id="e07eb-346">**Y** -50</span></span>        |  <span data-ttu-id="e07eb-347">**Z** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-347">**Z** 0</span></span>  |

    |            |     <span data-ttu-id="e07eb-348">TRANSFORMATION-METTRE À L’ÉCHELLE</span><span class="sxs-lookup"><span data-stu-id="e07eb-348">TRANSFORM - SCALE</span></span>     |           |
    | :---------:| :-----------------------: | :--------:|
    |  <span data-ttu-id="e07eb-349">**X** 1</span><span class="sxs-lookup"><span data-stu-id="e07eb-349">**X** 1</span></span>   |          <span data-ttu-id="e07eb-350">**Y** 1</span><span class="sxs-lookup"><span data-stu-id="e07eb-350">**Y** 1</span></span>          |  <span data-ttu-id="e07eb-351">**Z** 1</span><span class="sxs-lookup"><span data-stu-id="e07eb-351">**Z** 1</span></span>  |

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-41.png)

8.  <span data-ttu-id="e07eb-353">Cliquez sur l’objet enfant **GazeButton** et définissez sa **transformation** comme suit:</span><span class="sxs-lookup"><span data-stu-id="e07eb-353">Click on the **GazeButton** child object, and set its **Transform** as follows:</span></span>

    |            |    <span data-ttu-id="e07eb-354">TRANSFORMATION-POSITION</span><span class="sxs-lookup"><span data-stu-id="e07eb-354">TRANSFORM - POSITION</span></span>   |           |
    | :---------:| :-----------------------: | :--------:|
    |   <span data-ttu-id="e07eb-355">**X** 3,6</span><span class="sxs-lookup"><span data-stu-id="e07eb-355">**X** 3.6</span></span>|          <span data-ttu-id="e07eb-356">**Y** 1,3</span><span class="sxs-lookup"><span data-stu-id="e07eb-356">**Y** 1.3</span></span>        |  <span data-ttu-id="e07eb-357">**Z** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-357">**Z** 0</span></span>  |

    |            |    <span data-ttu-id="e07eb-358">TRANSFORMATION-ROTATION</span><span class="sxs-lookup"><span data-stu-id="e07eb-358">TRANSFORM - ROTATION</span></span>   |           |
    | :---------:| :-----------------------: | :--------:|
    |   <span data-ttu-id="e07eb-359">**X** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-359">**X** 0</span></span>  |          <span data-ttu-id="e07eb-360">**Y** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-360">**Y** 0</span></span>          |  <span data-ttu-id="e07eb-361">**Z** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-361">**Z** 0</span></span>  |

    |            |     <span data-ttu-id="e07eb-362">TRANSFORMATION-METTRE À L’ÉCHELLE</span><span class="sxs-lookup"><span data-stu-id="e07eb-362">TRANSFORM - SCALE</span></span>     |           |
    | :---------:| :-----------------------: | :--------:|
    |  <span data-ttu-id="e07eb-363">**X** 1</span><span class="sxs-lookup"><span data-stu-id="e07eb-363">**X** 1</span></span>   |          <span data-ttu-id="e07eb-364">**Y** 1</span><span class="sxs-lookup"><span data-stu-id="e07eb-364">**Y** 1</span></span>          |  <span data-ttu-id="e07eb-365">**Z** 1</span><span class="sxs-lookup"><span data-stu-id="e07eb-365">**Z** 1</span></span>  |

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-42.png)


## <a name="chapter-5---create-the-videocontroller-class"></a><span data-ttu-id="e07eb-367">Chapitre 5-créer la classe VideoController</span><span class="sxs-lookup"><span data-stu-id="e07eb-367">Chapter 5 - Create the VideoController class</span></span>

<span data-ttu-id="e07eb-368">La classe **VideoController** héberge les deux points de terminaison vidéo qui seront utilisés pour diffuser le contenu à partir du service multimédia Azure.</span><span class="sxs-lookup"><span data-stu-id="e07eb-368">The **VideoController** class hosts the two video endpoints that will be used to stream the content from the Azure Media Service.</span></span>

<span data-ttu-id="e07eb-369">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="e07eb-369">To create this class:</span></span>

1.  <span data-ttu-id="e07eb-370">Cliquez avec le bouton droit sur le **dossier Asset**, situé dans le panneau **projet** , puis cliquez sur **créer un dossier >** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-370">Right-click in the **Asset Folder**, located in the **Project** Panel, and click **Create > Folder**.</span></span> <span data-ttu-id="e07eb-371">Nommez le dossier **scripts**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-371">Name the folder **Scripts**.</span></span>

    ![Créer la classe VideoController](images/AzureLabs-Lab6-43.png)

    ![Créer la classe VideoController](images/AzureLabs-Lab6-44.png)

2.  <span data-ttu-id="e07eb-374">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="e07eb-374">Double click on the **Scripts** folder to open it.</span></span>

3.  <span data-ttu-id="e07eb-375">Cliquez avec le bouton droit dans le dossier, puis cliquez sur **créer > script C\#** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-375">Right-click inside the folder, then click **Create > C\# Script**.</span></span> <span data-ttu-id="e07eb-376">Nommez le script **VideoController**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-376">Name the script **VideoController**.</span></span>

    ![Créer la classe VideoController](images/AzureLabs-Lab6-45.png)

4.  <span data-ttu-id="e07eb-378">Double-cliquez sur le nouveau script **VideoController** pour l’ouvrir avec **Visual Studio 2017.**</span><span class="sxs-lookup"><span data-stu-id="e07eb-378">Double click on the new **VideoController** script to open it with **Visual Studio 2017.**</span></span>

    ![Créer la classe VideoController](images/AzureLabs-Lab6-46.png)

5.  <span data-ttu-id="e07eb-380">Mettez à jour les espaces de noms en haut du fichier de code comme suit:</span><span class="sxs-lookup"><span data-stu-id="e07eb-380">Update the namespaces at the top of the code file as follows:</span></span>

    ```csharp
    using System.Collections;
    using UnityEngine;
    using UnityEngine.SceneManagement;
    using UnityEngine.Video;
    ```

6.  <span data-ttu-id="e07eb-381">Entrez les variables suivantes dans la classe **VideoController** , ainsi que la méthode **éveillé ()** :</span><span class="sxs-lookup"><span data-stu-id="e07eb-381">Enter the following variables in the **VideoController** class, along with the **Awake()** method:</span></span>

    ```csharp
        /// <summary> 
        /// Provides Singleton-like behaviour to this class. 
        /// </summary> 
        public static VideoController instance; 
        
        /// <summary> 
        /// Reference to the Camera VideoPlayer Component.
        /// </summary> 
        private VideoPlayer videoPlayer; 
        
        /// <summary>
        /// Reference to the Camera AudioSource Component.
        /// </summary> 
        private AudioSource audioSource; 
        
        /// <summary> 
        /// Reference to the texture used to project the video streaming 
        /// </summary> 
        private RenderTexture videoStreamRenderTexture;

        /// <summary>
        /// Insert here the first video endpoint
        /// </summary>
        private string video1endpoint = "-- Insert video 1 Endpoint here --";

        /// <summary>
        /// Insert here the second video endpoint
        /// </summary>
        private string video2endpoint = "-- Insert video 2 Endpoint here --";

        /// <summary> 
        /// Reference to the Inside-Out Sphere. 
        /// </summary> 
        public GameObject sphere;

        void Awake()
        {
            instance = this;
        }
    ```

7.  <span data-ttu-id="e07eb-382">Maintenant, vous pouvez entrer les points de terminaison à partir de vos vidéos Azure Media Services:</span><span class="sxs-lookup"><span data-stu-id="e07eb-382">Now is the time to enter the endpoints from your Azure Media Service videos:</span></span>

    1.  <span data-ttu-id="e07eb-383">Premier dans la variable *video1endpoint* .</span><span class="sxs-lookup"><span data-stu-id="e07eb-383">The first into the *video1endpoint* variable.</span></span>
    
    2.  <span data-ttu-id="e07eb-384">Deuxième dans la variable *video2endpoint* .</span><span class="sxs-lookup"><span data-stu-id="e07eb-384">The second into the *video2endpoint* variable.</span></span>

    > [!WARNING]
    > <span data-ttu-id="e07eb-385">Il existe un problème connu lié à  l’utilisation de https dans Unity, avec la version 2017.4.1 F1.</span><span class="sxs-lookup"><span data-stu-id="e07eb-385">There is a known issue with using *https* within Unity, with version 2017.4.1f1.</span></span> <span data-ttu-id="e07eb-386">Si les vidéos fournissent une erreur lors de la lecture, essayez d’utiliser «http» à la place.</span><span class="sxs-lookup"><span data-stu-id="e07eb-386">If the videos provide an error on play, try using 'http' instead.</span></span>

8.  <span data-ttu-id="e07eb-387">Ensuite, la méthode **Start ()** doit être modifiée.</span><span class="sxs-lookup"><span data-stu-id="e07eb-387">Next, the **Start()** method needs to be edited.</span></span> <span data-ttu-id="e07eb-388">Cette méthode est déclenchée chaque fois que l’utilisateur change de scène (en basculant la vidéo) en regardant le bouton de regard.</span><span class="sxs-lookup"><span data-stu-id="e07eb-388">This method will be triggered every time the user switches scene (consequently switching the video) by looking at the Gaze Button.</span></span>

    ```csharp
        // Use this for initialization
        void Start()
        {
            Application.runInBackground = true;
            StartCoroutine(PlayVideo());
        }
    ```

9.  <span data-ttu-id="e07eb-389">À la suite de la méthode **Start ()** , insérez la méthode **playVideo ()** *IEnumerator* , qui sera utilisée pour démarrer des vidéos de manière transparente (aucune interruption n’est détectée).</span><span class="sxs-lookup"><span data-stu-id="e07eb-389">Following the **Start()** method, insert the **PlayVideo()** *IEnumerator* method, which will be used to start videos seamlessly (so no stutter is seen).</span></span>

    ```csharp
        private IEnumerator PlayVideo()
        {
            // create a new render texture to display the video 
            videoStreamRenderTexture = new RenderTexture(2160, 1440, 32, RenderTextureFormat.ARGB32);

            videoStreamRenderTexture.Create();

            // assign the render texture to the object material 
            Material sphereMaterial = sphere.GetComponent<Renderer>().sharedMaterial;

            //create a VideoPlayer component 
            videoPlayer = gameObject.AddComponent<VideoPlayer>();

            // Set the video to loop. 
            videoPlayer.isLooping = true;

            // Set the VideoPlayer component to play the video from the texture 
            videoPlayer.renderMode = VideoRenderMode.RenderTexture;

            videoPlayer.targetTexture = videoStreamRenderTexture;

            // Add AudioSource 
            audioSource = gameObject.AddComponent<AudioSource>();

            // Pause Audio play on Awake 
            audioSource.playOnAwake = true;
            audioSource.Pause();

            // Set Audio Output to AudioSource 
            videoPlayer.audioOutputMode = VideoAudioOutputMode.AudioSource;
            videoPlayer.source = VideoSource.Url;

            // Assign the Audio from Video to AudioSource to be played 
            videoPlayer.EnableAudioTrack(0, true);
            videoPlayer.SetTargetAudioSource(0, audioSource);

            // Assign the video Url depending on the current scene 
            switch (SceneManager.GetActiveScene().name)
            {
                case "VideoScene1":
                    videoPlayer.url = video1endpoint;
                    break;

                case "VideoScene2":
                    videoPlayer.url = video2endpoint;
                    break;

                default:
                    break;
            }

            //Set video To Play then prepare Audio to prevent Buffering 
            videoPlayer.Prepare();

            while (!videoPlayer.isPrepared)
            {
                yield return null;
            }

            sphereMaterial.mainTexture = videoStreamRenderTexture;

            //Play Video 
            videoPlayer.Play();

            //Play Sound 
            audioSource.Play();

            while (videoPlayer.isPlaying)
            {
                yield return null;
            }
        }
    ```

10. <span data-ttu-id="e07eb-390">La dernière méthode dont vous avez besoin pour cette classe est la méthode **ChangeScene ()** , qui sera utilisée pour échanger des scènes.</span><span class="sxs-lookup"><span data-stu-id="e07eb-390">The last method you need for this class is the **ChangeScene()** method, which will be used to swap between scenes.</span></span>

    ```csharp
        public void ChangeScene()
        {
            SceneManager.LoadScene(SceneManager.GetActiveScene().name == "VideoScene1" ? "VideoScene2" : "VideoScene1");
        }
    ```

    > [!TIP] 
    > <span data-ttu-id="e07eb-391">La méthode **ChangeScene ()** utilise une fonctionnalité C\# pratique appelée *opérateur conditionnel*.</span><span class="sxs-lookup"><span data-stu-id="e07eb-391">The **ChangeScene()** method uses a handy C\# feature called the *Conditional Operator*.</span></span> <span data-ttu-id="e07eb-392">Cela permet de vérifier les conditions, puis les valeurs retournées en fonction du résultat de la vérification, dans une instruction unique.</span><span class="sxs-lookup"><span data-stu-id="e07eb-392">This allows for conditions to be checked, and then values returned based on the outcome of the check, all within a single statement.</span></span> <span data-ttu-id="e07eb-393">Suivez ce [lien pour en savoir plus sur l’opérateur conditionnel](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/conditional-operator).</span><span class="sxs-lookup"><span data-stu-id="e07eb-393">Follow this [link to learn more about Conditional Operator](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/conditional-operator).</span></span>

11. <span data-ttu-id="e07eb-394">Enregistrez vos modifications dans Visual Studio avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="e07eb-394">Save your changes in Visual Studio before returning to Unity.</span></span>

12. <span data-ttu-id="e07eb-395">De retour dans l’éditeur Unity, cliquez et faites glisser la classe **VideoController** [from] {. Underline} le dossier **scripts** vers l’objet **Camera principal** dans le panneau **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-395">Back in the Unity Editor, click and drag the **VideoController** class [from]{.underline} the **Scripts** folder to the **Main Camera** object in the **Hierarchy** Panel.</span></span>

13. <span data-ttu-id="e07eb-396">Cliquez sur l' **appareil photo principal** et observez le panneau de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-396">Click on the **Main Camera** and look at the **Inspector Panel**.</span></span> <span data-ttu-id="e07eb-397">Vous remarquerez que dans le composant script qui vient d’être ajouté, il existe un champ avec une valeur vide.</span><span class="sxs-lookup"><span data-stu-id="e07eb-397">You will notice that within the newly added Script component, there is a field with an empty value.</span></span> <span data-ttu-id="e07eb-398">Il s’agit d’un champ de référence qui cible les variables publiques dans votre code.</span><span class="sxs-lookup"><span data-stu-id="e07eb-398">This is a reference field, which targets the public variables within your code.</span></span>

14. <span data-ttu-id="e07eb-399">Faites glisser l’objet **InsideOutSphere** du **volet** de la hiérarchie vers l’emplacement **Sphere** , comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e07eb-399">Drag the **InsideOutSphere** object from the **Hierarchy Panel** to the **Sphere** slot, as shown in the image below.</span></span>

    <span data-ttu-id="e07eb-400">![Créer la classe](images/AzureLabs-Lab6-47.png)
    ![VideoController créer la classe VideoController](images/AzureLabs-Lab6-48.png)</span><span class="sxs-lookup"><span data-stu-id="e07eb-400">![Create the VideoController class](images/AzureLabs-Lab6-47.png)
![Create the VideoController class](images/AzureLabs-Lab6-48.png)</span></span>

## <a name="chapter-6---create-the-gaze-class"></a><span data-ttu-id="e07eb-401">Chapitre 6-créer la classe en regard</span><span class="sxs-lookup"><span data-stu-id="e07eb-401">Chapter 6 - Create the Gaze class</span></span>

<span data-ttu-id="e07eb-402">Cette classe est chargée de créer un **Raycast** qui se transmettra à l’avant à partir de la **caméra principale**, pour détecter l’objet que l’utilisateur examine.</span><span class="sxs-lookup"><span data-stu-id="e07eb-402">This class is responsible for creating a **Raycast** that will beprojected forward from the **Main Camera**, to detect which object the user is looking at.</span></span> <span data-ttu-id="e07eb-403">Dans ce cas, le **Raycast** doit déterminer si l’utilisateur regarde l’objet **GazeButton** dans la scène et déclencher un comportement.</span><span class="sxs-lookup"><span data-stu-id="e07eb-403">In this case, the **Raycast** will need to identify if the user is looking at the **GazeButton** object in the scene and trigger a behavior.</span></span>

<span data-ttu-id="e07eb-404">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="e07eb-404">To create this Class:</span></span>

1.  <span data-ttu-id="e07eb-405">Accédez au dossier **scripts** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="e07eb-405">Go to the **Scripts** folder you created previously.</span></span>

2.  <span data-ttu-id="e07eb-406">Avec le bouton droit dans le **projet** panneau, \**créer* \*C\# Script\*\*.</span><span class="sxs-lookup"><span data-stu-id="e07eb-406">Right-click in the **Project** Panel, \**Create* \*C\# Script\*\*.</span></span> <span data-ttu-id="e07eb-407">Nommez le script point de **regard**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-407">Name the script **Gaze**.</span></span>

3.  <span data-ttu-id="e07eb-408">Double-cliquez sur le nouveau script de ***regard*** pour l’ouvrir avec **Visual Studio 2017.**</span><span class="sxs-lookup"><span data-stu-id="e07eb-408">Double click on the new ***Gaze*** script to open it with **Visual Studio 2017.**</span></span>

4.  <span data-ttu-id="e07eb-409">Assurez-vous que l’espace de noms suivant figure en haut du script et supprimez les autres:</span><span class="sxs-lookup"><span data-stu-id="e07eb-409">Ensure the following namespace is at the top of the script, and remove any others:</span></span>

    ```csharp
    using UnityEngine;
    ```

5.  <span data-ttu-id="e07eb-410">Ajoutez ensuite les variables suivantes à l’intérieur de la classe **regard** :</span><span class="sxs-lookup"><span data-stu-id="e07eb-410">Then add the following variables inside the **Gaze** class:</span></span>

    ```csharp
        /// <summary> 
        /// Provides Singleton-like behaviour to this class. 
        /// </summary> 
        public static Gaze instance;

        /// <summary> 
        /// Provides a reference to the object the user is currently looking at. 
        /// </summary> 
        public GameObject FocusedGameObject { get; private set; }

        /// <summary> 
        /// Provides a reference to compare whether the user is still looking at 
        /// the same object (and has not looked away). 
        /// </summary> 
        private GameObject oldFocusedObject = null;

        /// <summary> 
        /// Max Ray Distance 
        /// </summary> 
        float gazeMaxDistance = 300;

        /// <summary> 
        /// Provides whether an object has been successfully hit by the raycast. 
        /// </summary> 
        public bool Hit { get; private set; }
    ```

6.  <span data-ttu-id="e07eb-411">Vous devez maintenant ajouter du code pour les méthodes **éveillé ()** et **Start ()** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-411">Code for the **Awake()** and **Start()** methods now needs to be added.</span></span>

    ```csharp
        private void Awake()
        {
            // Set this class to behave similar to singleton 
            instance = this;
        }

        void Start()
        {
            FocusedGameObject = null;
        }
    ```

7.  <span data-ttu-id="e07eb-412">Ajoutez le code suivant dans la méthode **Update ()** pour projeter un Raycast et détecter l’accès cible:</span><span class="sxs-lookup"><span data-stu-id="e07eb-412">Add the following code in the **Update()** method to project a Raycast and detect the target hit:</span></span>

    ```csharp
        void Update()
        {
            // Set the old focused gameobject. 
            oldFocusedObject = FocusedGameObject;
            RaycastHit hitInfo;

            // Initialise Raycasting. 
            Hit = Physics.Raycast(Camera.main.transform.position, Camera.main.transform.forward, out hitInfo, gazeMaxDistance);

            // Check whether raycast has hit. 
            if (Hit == true)
            {
                // Check whether the hit has a collider. 
                if (hitInfo.collider != null)
                {
                    // Set the focused object with what the user just looked at. 
                    FocusedGameObject = hitInfo.collider.gameObject;
                }
                else
                {
                    // Object looked on is not valid, set focused gameobject to null. 
                    FocusedGameObject = null;
                }
            }
            else
            {
                // No object looked upon, set focused gameobject to null.
                FocusedGameObject = null;
            }

            // Check whether the previous focused object is this same 
            // object (so to stop spamming of function). 
            if (FocusedGameObject != oldFocusedObject)
            {
                // Compare whether the new Focused Object has the desired tag we set previously. 
                if (FocusedGameObject.CompareTag("GazeButton"))
                {
                    FocusedGameObject.SetActive(false);
                    VideoController.instance.ChangeScene();
                }
            }
        }
    ```

8.  <span data-ttu-id="e07eb-413">Enregistrez vos modifications dans Visual Studio avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="e07eb-413">Save your changes in Visual Studio before returning to Unity.</span></span>

9.  <span data-ttu-id="e07eb-414">Cliquez et faites glisser **la classe** pointage du dossier scripts vers l’objet caméra principal dans le panneau **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-414">Click and drag the **Gaze** class from the Scripts folder to the Main Camera object in the **Hierarchy** Panel.</span></span>

## <a name="chapter-7---setup-the-two-unity-scenes"></a><span data-ttu-id="e07eb-415">Chapitre 7: configurer les deux scènes d’Unity</span><span class="sxs-lookup"><span data-stu-id="e07eb-415">Chapter 7 - Setup the two Unity Scenes</span></span>

<span data-ttu-id="e07eb-416">L’objectif de ce chapitre est de configurer les deux scènes, chacune hébergeant une vidéo à diffuser.</span><span class="sxs-lookup"><span data-stu-id="e07eb-416">The purpose of this Chapter is to setup the two scenes, each hosting a video to stream.</span></span> <span data-ttu-id="e07eb-417">Vous allez dupliquer la scène que vous avez déjà créée, afin de ne pas avoir à la reconfigurer, bien que vous modifiiez ensuite la nouvelle scène, afin que l’objet *GazeButton* se trouve à un emplacement différent et ait une apparence différente.</span><span class="sxs-lookup"><span data-stu-id="e07eb-417">You will duplicate the scene you have already created, so that you do not need to set it up again, though you will then edit the new scene, so that the *GazeButton* object is in a different location and has a different appearance.</span></span> <span data-ttu-id="e07eb-418">Il s’agit de montrer comment changer entre les scènes.</span><span class="sxs-lookup"><span data-stu-id="e07eb-418">This is to show how to change between scenes.</span></span>

1.  <span data-ttu-id="e07eb-419">Pour ce faire, accédez à **fichier > enregistrer la scène sous...** . Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e07eb-419">Do this by going to **File > Save Scene as...**. A save window will appear.</span></span> <span data-ttu-id="e07eb-420">Cliquez sur le bouton **nouveau dossier** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-420">Click the **New folder** button.</span></span>

    ![Chapitre 7: configurer les deux scènes d’Unity](images/AzureLabs-Lab6-49.png)

2.  <span data-ttu-id="e07eb-422">Nommez le dossier Scenes.</span><span class="sxs-lookup"><span data-stu-id="e07eb-422">Name the folder **Scenes**.</span></span>

3.  <span data-ttu-id="e07eb-423">La fenêtre **enregistrer la scène** est toujours ouverte.</span><span class="sxs-lookup"><span data-stu-id="e07eb-423">The **Save Scene** window will still be open.</span></span> <span data-ttu-id="e07eb-424">Ouvrez le dossier **scenes** que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="e07eb-424">Open your newly created **Scenes** folder.</span></span>

4.  <span data-ttu-id="e07eb-425">Dans le champ **nom de fichier:** , tapez **VideoScene1**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-425">In the **File name:** text field, type **VideoScene1**, then press **Save**.</span></span>

5.  <span data-ttu-id="e07eb-426">De retour dans Unity,  ouvrez votre dossier scenes, puis cliquez sur votre fichier **VideoScene1** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-426">Back in Unity, open your **Scenes** folder, and left-click your **VideoScene1** file.</span></span> <span data-ttu-id="e07eb-427">À l’aide de votre clavier, appuyez sur **Ctrl + D** pour dupliquer cette scène</span><span class="sxs-lookup"><span data-stu-id="e07eb-427">Use your keyboard, and press **Ctrl + D** you will duplicate that scene</span></span>

    > [!TIP]
    > <span data-ttu-id="e07eb-428">La  commande dupliquée peut également être exécutée en accédant à **Modifier > doublon**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-428">The **Duplicate** command can also be performed by navigating to **Edit > Duplicate**.</span></span>

6.  <span data-ttu-id="e07eb-429">Unity incrémente automatiquement le numéro de nom de la scène, mais vérifie tout de même qu’il correspond au code précédemment inséré.</span><span class="sxs-lookup"><span data-stu-id="e07eb-429">Unity will automatically increment the scene names number, but check it anyway, to ensure it matches the previously inserted code.</span></span>

    >  <span data-ttu-id="e07eb-430">Vous devez avoir **VideoScene1** et **VideoScene2**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-430">You should have **VideoScene1** and **VideoScene2**.</span></span>

7.  <span data-ttu-id="e07eb-431">Avec les deux scènes, accédez à **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-431">With your two scenes, go to **File > Build Settings**.</span></span> <span data-ttu-id="e07eb-432">Une fois la fenêtre des **paramètres de build** ouverte, faites glisser vos scènes jusqu’à la section scenes **dans la build** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-432">With the **Build Settings** window open, drag your scenes to the **Scenes in Build** section.</span></span>

    ![Chapitre 7: configurer les deux scènes Unity](images/AzureLabs-Lab6-50.png)

    > [!TIP] 
    > <span data-ttu-id="e07eb-434">Vous pouvez sélectionner les deux scènes dans votre dossier **scenes** tout en maintenant le bouton **CTRL** enfoncé, puis en cliquant avec le bouton gauche sur chaque scène et en faisant glisser les deux à la fois.</span><span class="sxs-lookup"><span data-stu-id="e07eb-434">You can select both of your scenes from your **Scenes** folder through holding the **Ctrl** button, and then left-clicking each scene, and finally drag both across.</span></span>

8.  <span data-ttu-id="e07eb-435">Fermez la fenêtre **paramètres de build** , puis double-cliquez sur **VideoScene2**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-435">Close the **Build Settings** window, and double click on **VideoScene2**.</span></span>

9.  <span data-ttu-id="e07eb-436">Une fois la deuxième scène ouverte, cliquez sur l’objet enfant **GazeButton** du **InsideOutSphere**et définissez sa transformation comme suit:</span><span class="sxs-lookup"><span data-stu-id="e07eb-436">With the second scene open, click on the **GazeButton** child object of the **InsideOutSphere**, and set its Transform as follows:</span></span>

    |            |    <span data-ttu-id="e07eb-437">TRANSFORMATION-POSITION</span><span class="sxs-lookup"><span data-stu-id="e07eb-437">TRANSFORM - POSITION</span></span>   |           |
    | :---------:| :-----------------------: | :--------:|
    |   <span data-ttu-id="e07eb-438">**X** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-438">**X** 0</span></span>  |         <span data-ttu-id="e07eb-439">**Y** 1,3</span><span class="sxs-lookup"><span data-stu-id="e07eb-439">**Y** 1.3</span></span>         | <span data-ttu-id="e07eb-440">**Z** 3,6</span><span class="sxs-lookup"><span data-stu-id="e07eb-440">**Z** 3.6</span></span> |

    |            |    <span data-ttu-id="e07eb-441">TRANSFORMATION-ROTATION</span><span class="sxs-lookup"><span data-stu-id="e07eb-441">TRANSFORM - ROTATION</span></span>   |           |
    | :---------:| :-----------------------: | :--------:|
    |   <span data-ttu-id="e07eb-442">**X** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-442">**X** 0</span></span>  |          <span data-ttu-id="e07eb-443">**Y** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-443">**Y** 0</span></span>          |  <span data-ttu-id="e07eb-444">**Z** 0</span><span class="sxs-lookup"><span data-stu-id="e07eb-444">**Z** 0</span></span>  |

    |            |     <span data-ttu-id="e07eb-445">TRANSFORMATION-METTRE À L’ÉCHELLE</span><span class="sxs-lookup"><span data-stu-id="e07eb-445">TRANSFORM - SCALE</span></span>     |           |
    | :---------:| :-----------------------: | :--------:|
    |  <span data-ttu-id="e07eb-446">**X** 1</span><span class="sxs-lookup"><span data-stu-id="e07eb-446">**X** 1</span></span>   |          <span data-ttu-id="e07eb-447">**Y** 1</span><span class="sxs-lookup"><span data-stu-id="e07eb-447">**Y** 1</span></span>          |  <span data-ttu-id="e07eb-448">**Z** 1</span><span class="sxs-lookup"><span data-stu-id="e07eb-448">**Z** 1</span></span>  |

10. <span data-ttu-id="e07eb-449">Avec l’enfant **GazeButton** toujours sélectionné, examinez l' **inspecteur** et le **filtre de maillage**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-449">With the **GazeButton** child still selected, look at the **Inspector** and at the **Mesh Filter**.</span></span> <span data-ttu-id="e07eb-450">Cliquez sur la petite cible en regard du champ de référence de **maillage** :</span><span class="sxs-lookup"><span data-stu-id="e07eb-450">Click the little target next to the **Mesh** reference field:</span></span>

    ![Chapitre 7: configurer les deux scènes Unity](images/AzureLabs-Lab6-51.png)

11. <span data-ttu-id="e07eb-452">Une fenêtre contextuelle **Sélectionner le maillage** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e07eb-452">A **Select Mesh** popup window will appear.</span></span> <span data-ttu-id="e07eb-453">Double-cliquez sur la maille du **cube** dans la liste des **ressources**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-453">Double click the **Cube** mesh from the list of **Assets**.</span></span>

    ![Chapitre 7: configurer les deux scènes Unity](images/AzureLabs-Lab6-52.png)

12. <span data-ttu-id="e07eb-455">Le **filtre de maillage** est mis à jour et est maintenant un **cube**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-455">The **Mesh Filter** will update, and now be a **Cube**.</span></span> <span data-ttu-id="e07eb-456">Maintenant, cliquez sur l’icône d' **engrenage** en regard de **Sphere collision** , puis cliquez sur **supprimer le composant**pour supprimer le conflit de cet objet.</span><span class="sxs-lookup"><span data-stu-id="e07eb-456">Now, click the **Gear** icon next to **Sphere Collider** and click **Remove Component**, to delete the collider from this object.</span></span>

    ![Chapitre 7: configurer les deux scènes Unity](images/AzureLabs-Lab6-53.png)

13. <span data-ttu-id="e07eb-458">Avec la **GazeButton** toujours sélectionnée, cliquez sur le bouton **Ajouter un composant** situé en bas de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-458">With the **GazeButton** still selected, click the **Add Component** button at the bottom of the **Inspector**.</span></span> <span data-ttu-id="e07eb-459">Dans le champ de recherche, la **zone**type et le **conflit de zone** sont une option qui permet d’ajouter un **conflit Box** à votre objet **GazeButton** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-459">In the search field, type **box**, and **Box Collider** will be an option -- click that, to add a **Box Collider** to your **GazeButton** object.</span></span>

    ![Chapitre 7: configurer les deux scènes Unity](images/AzureLabs-Lab6-54.png)

14. <span data-ttu-id="e07eb-461">Le **GazeButton** est maintenant partiellement mis à jour. Toutefois, vous allez maintenant créer un nouveau **matériau**, afin qu’il soit complètement différent et qu’il soit plus facile à reconnaître en tant qu’objet différent que l’objet dans la première scène.</span><span class="sxs-lookup"><span data-stu-id="e07eb-461">The **GazeButton** is now partially updated, to look different, however, you will now create a new **Material**, so that it looks completely different, and is easier to recognize as a different object, than the object in the first scene.</span></span>

15. <span data-ttu-id="e07eb-462">Accédez à votre  dossier Materials, dans le **panneau Projet**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-462">Navigate to your **Materials** folder, within the **Project Panel**.</span></span> <span data-ttu-id="e07eb-463">Dupliquez le matériel **ButtonMaterial** (appuyez sur **CTRL** + **D** sur le clavier ou cliquez sur le **matériau**, puis sélectionnez Dupliquer dans l’option de menu  **modifier** le fichier).</span><span class="sxs-lookup"><span data-stu-id="e07eb-463">Duplicate the **ButtonMaterial** Material (press **Ctrl** + **D** on the keyboard, or left-click the **Material**, then from the **Edit** file menu option, select **Duplicate**).</span></span>

    <span data-ttu-id="e07eb-464">![Chapitre 7--configurer les deux scènes](images/AzureLabs-Lab6-55.png)
    ![d’Unity chapitre 7--configurer les deux scènes d’Unity](images/AzureLabs-Lab6-56.png)</span><span class="sxs-lookup"><span data-stu-id="e07eb-464">![Chapter 7 -- Setup the two Unity Scenes](images/AzureLabs-Lab6-55.png)
![Chapter 7 -- Setup the two Unity Scenes](images/AzureLabs-Lab6-56.png)</span></span>

16. <span data-ttu-id="e07eb-465">Sélectionnez le nouveau matériel **ButtonMaterial** (nommé **ButtonMaterial 1**) et, dans l' **inspecteur**, cliquez sur la fenêtre de couleur **Albedo** .</span><span class="sxs-lookup"><span data-stu-id="e07eb-465">Select the new **ButtonMaterial** Material (here named **ButtonMaterial 1**), and within the **Inspector**, click the **Albedo** color window.</span></span> <span data-ttu-id="e07eb-466">Une fenêtre contextuelle s’affiche, dans laquelle vous pouvez sélectionner une autre couleur (choisissez celle qui vous plaît), puis fermer la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="e07eb-466">A popup will appear, where you can select another color (choose whichever you like), then close the popup.</span></span> <span data-ttu-id="e07eb-467">Le matériau sera sa propre instance et différent de l’original.</span><span class="sxs-lookup"><span data-stu-id="e07eb-467">The Material will be its own instance, and different to the original.</span></span>

    ![Chapitre 7: configurer les deux scènes Unity](images/AzureLabs-Lab6-57.png)

17. <span data-ttu-id="e07eb-469">Faites glisser le nouveau **matériau** sur l’enfant **GazeButton** pour mettre à jour complètement son apparence, afin qu’il soit facilement facile à distinguer du bouton premières scènes.</span><span class="sxs-lookup"><span data-stu-id="e07eb-469">Drag the new **Material** onto the **GazeButton** child, to now completely update its look, so that it is easily distinguishable from the first scenes button.</span></span>

    ![Chapitre 7: configurer les deux scènes Unity](images/AzureLabs-Lab6-58.png)

18. <span data-ttu-id="e07eb-471">À ce stade, vous pouvez tester le projet dans l’éditeur avant de générer le projet UWP.</span><span class="sxs-lookup"><span data-stu-id="e07eb-471">At this point you can test the project in the Editor before building the UWP project.</span></span>

    -  <span data-ttu-id="e07eb-472">Appuyez sur le bouton de **lecture** dans l' **éditeur** et portez votre casque.</span><span class="sxs-lookup"><span data-stu-id="e07eb-472">Press the **Play** button in the **Editor** and wear your headset.</span></span>

        ![Chapitre 7: configurer les deux scènes Unity](images/AzureLabs-Lab6-59.png)

19. <span data-ttu-id="e07eb-474">Examinez les deux objets **GazeButton** pour basculer entre la première et la deuxième vidéo.</span><span class="sxs-lookup"><span data-stu-id="e07eb-474">Look at the two **GazeButton** objects to switch between the first and second video.</span></span>

## <a name="chapter-8---build-the-uwp-solution"></a><span data-ttu-id="e07eb-475">Chapitre 8-créer la solution UWP</span><span class="sxs-lookup"><span data-stu-id="e07eb-475">Chapter 8 - Build the UWP Solution</span></span>

<span data-ttu-id="e07eb-476">Une fois que vous avez vérifié que l’éditeur n’a pas d’erreurs, vous êtes prêt à générer.</span><span class="sxs-lookup"><span data-stu-id="e07eb-476">Once you have ensured that the editor has no errors, you are ready to Build.</span></span>

<span data-ttu-id="e07eb-477">Pour générer:</span><span class="sxs-lookup"><span data-stu-id="e07eb-477">To Build:</span></span>

1.  <span data-ttu-id="e07eb-478">Enregistrez la scène en cours en cliquant sur **fichier > enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-478">Save the current scene by clicking on **File > Save**.</span></span>

2.  <span data-ttu-id="e07eb-479">Cochez la case **projets Unity\# C** (cette opération est importante car elle vous permettra de modifier les classes une fois la génération terminée).</span><span class="sxs-lookup"><span data-stu-id="e07eb-479">Check the box called **Unity C\# Projects** (this is important because it will allow you to edit the classes after build is completed).</span></span>

3.  <span data-ttu-id="e07eb-480">Accédez à **fichier > paramètres de build**, puis cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-480">Go to **File > Build Settings**, click on **Build**.</span></span>

4.  <span data-ttu-id="e07eb-481">Vous serez invité à sélectionner le dossier dans lequel vous souhaitez buildThe la solution.</span><span class="sxs-lookup"><span data-stu-id="e07eb-481">You will be prompted to select the folder where you want to buildthe Solution.</span></span>

5.  <span data-ttu-id="e07eb-482">Créez un  dossier Builds et, dans ce dossier, créez un autre dossier avec le nom approprié de votre choix.</span><span class="sxs-lookup"><span data-stu-id="e07eb-482">Create a **BUILDS** folder and within that folder create another folder with an appropriate name of your choice.</span></span>

6.  <span data-ttu-id="e07eb-483">Cliquez sur votre nouveau dossier, puis sur **Sélectionner un dossier**, afin de choisir ce dossier, pour commencer la build à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="e07eb-483">Click your new folder and then click **Select Folder**, so to choose that folder, to begin the build at that location.</span></span>

    <span data-ttu-id="e07eb-484">![Chapitre 8--créer la solution](images/AzureLabs-Lab6-60.png)
    ![UWP chapitre 8--créer la solution UWP](images/AzureLabs-Lab6-61.png)</span><span class="sxs-lookup"><span data-stu-id="e07eb-484">![Chapter 8 -- Build the UWP Solution](images/AzureLabs-Lab6-60.png)
![Chapter 8 -- Build the UWP Solution](images/AzureLabs-Lab6-61.png)</span></span>

7.  <span data-ttu-id="e07eb-485">Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre Build.</span><span class="sxs-lookup"><span data-stu-id="e07eb-485">Once Unity has finished building (it might take some time), it will open a **File Explorer** window at the location of your build.</span></span>

## <a name="chapter-9---deploy-on-local-machine"></a><span data-ttu-id="e07eb-486">Chapitre 9-déployer sur l’ordinateur local</span><span class="sxs-lookup"><span data-stu-id="e07eb-486">Chapter 9 - Deploy on Local Machine</span></span>

<span data-ttu-id="e07eb-487">Une fois la génération terminée, une fenêtre de l' **Explorateur de fichiers** s’affiche à l’emplacement de votre Build.</span><span class="sxs-lookup"><span data-stu-id="e07eb-487">Once the build has been completed, a **File Explorer** window will appear at the location of your build.</span></span> <span data-ttu-id="e07eb-488">Ouvrez le dossier que vous avez nommé et créé, puis double-cliquez sur le fichier de solution (. sln) dans ce dossier pour ouvrir votre solution avec Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e07eb-488">Open the Folder you named and built to, then double click on the solution (.sln) file within that folder, to open your solution with Visual Studio 2017.</span></span>

<span data-ttu-id="e07eb-489">La seule chose à faire est de déployer votre application sur votre ordinateur (ou *ordinateur local*).</span><span class="sxs-lookup"><span data-stu-id="e07eb-489">The only thing left to do is deploy your app to your computer (or *Local Machine*).</span></span>

<span data-ttu-id="e07eb-490">Pour effectuer le déploiement sur l’ordinateur local:</span><span class="sxs-lookup"><span data-stu-id="e07eb-490">To deploy to Local Machine:</span></span>

1.  <span data-ttu-id="e07eb-491">Dans **Visual Studio 2017**, ouvrez le fichier solution qui vient d’être créé.</span><span class="sxs-lookup"><span data-stu-id="e07eb-491">In **Visual Studio 2017**, open the solution file that has just been created.</span></span>

2.  <span data-ttu-id="e07eb-492">Dans la **plateforme**de la solution, sélectionnez **x86, ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="e07eb-492">In the **Solution Platform**, select **x86, Local Machine**.</span></span>

3.  <span data-ttu-id="e07eb-493">Dans la **configuration** de la solution, sélectionnez Déboguer.</span><span class="sxs-lookup"><span data-stu-id="e07eb-493">In the **Solution Configuration** select **Debug**.</span></span>

    ![Chapitre 9--déployer sur l’ordinateur local](images/AzureLabs-Lab6-62.png)

4.  <span data-ttu-id="e07eb-495">Vous devez à présent restaurer les packages dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="e07eb-495">You will now need to restore any packages to your solution.</span></span> <span data-ttu-id="e07eb-496">Cliquez avec le bouton droit sur votre **solution**, puis cliquez sur **restaurer les packages NuGet pour la solution...**</span><span class="sxs-lookup"><span data-stu-id="e07eb-496">Right-click on your **Solution**, and click **Restore NuGet Packages for Solution...**</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e07eb-497">Cela est dû au fait que les packages créés par Unity doivent être ciblés pour fonctionner avec vos références d’ordinateurs locaux.</span><span class="sxs-lookup"><span data-stu-id="e07eb-497">This is done because the packages which Unity built need to be targeted to work with your local machines references.</span></span>

5.  <span data-ttu-id="e07eb-498">Accédez au **menu Générer** , puis cliquez sur **déployer la solution** pour chargement l’application sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e07eb-498">Go to **Build menu** and click on **Deploy Solution** to sideload the application to your machine.</span></span> <span data-ttu-id="e07eb-499">Visual Studio commence par générer, puis déployer votre application.</span><span class="sxs-lookup"><span data-stu-id="e07eb-499">Visual Studio will first build and then deploy your application.</span></span>

6.  <span data-ttu-id="e07eb-500">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancées.</span><span class="sxs-lookup"><span data-stu-id="e07eb-500">Your App should now appear in the list of installed apps, ready to be launched.</span></span>

    ![Chapitre 9--déployer sur l’ordinateur local](images/AzureLabs-Lab6-63.png)

<span data-ttu-id="e07eb-502">Lorsque vous exécutez l’application de réalité mixte, vous êtes dans le modèle **InsideOutSphere** que vous avez utilisé dans votre application.</span><span class="sxs-lookup"><span data-stu-id="e07eb-502">When you run the Mixed Reality application, you will you be within the **InsideOutSphere** model which you used within your app.</span></span> <span data-ttu-id="e07eb-503">Cette sphère sera l’endroit où la vidéo sera diffusée, en fournissant une vue 360 de la vidéo entrante (qui a été filmée pour ce type de perspective).</span><span class="sxs-lookup"><span data-stu-id="e07eb-503">This sphere will be where the video will be streamed to, providing a 360-degree view, of the incoming video (which was filmed for this kind of perspective).</span></span> <span data-ttu-id="e07eb-504">Ne soyez pas surpris si le chargement de la vidéo prend quelques secondes, votre application est soumise à votre vitesse Internet disponible, car la vidéo doit être récupérée, puis téléchargée, afin de diffuser dans votre application.</span><span class="sxs-lookup"><span data-stu-id="e07eb-504">Do not be surprised if the video takes a couple of seconds to load, your app is subject to your available Internet speed, as the video needs to be fetched and then downloaded, so to stream into your app.</span></span>
<span data-ttu-id="e07eb-505">Quand vous êtes prêt, modifiez les scènes et ouvrez votre deuxième vidéo, par Gazing à la sphère rouge!</span><span class="sxs-lookup"><span data-stu-id="e07eb-505">When you are ready, change scenes and open your second video, by gazing at the red sphere!</span></span> <span data-ttu-id="e07eb-506">N’hésitez pas à revenir en arrière, en utilisant le cube bleu dans la deuxième scène!</span><span class="sxs-lookup"><span data-stu-id="e07eb-506">Then feel free to go back, using the blue cube in the second scene!</span></span>

## <a name="your-finished-azure-media-service-application"></a><span data-ttu-id="e07eb-507">Votre application Azure Media service terminée</span><span class="sxs-lookup"><span data-stu-id="e07eb-507">Your finished Azure Media Service application</span></span>
 
<span data-ttu-id="e07eb-508">Félicitations, vous avez créé une application de réalité mixte qui tire parti d’Azure Media service pour diffuser des vidéos 360.</span><span class="sxs-lookup"><span data-stu-id="e07eb-508">Congratulations, you built a mixed reality app that leverages the Azure Media Service to stream 360 videos.</span></span>

![résultat de l’atelier](images/AzureLabs-Lab6-00.png)

![résultat de l’atelier](images/AzureLabs-Lab6-01.png)

## <a name="bonus-exercises"></a><span data-ttu-id="e07eb-511">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="e07eb-511">Bonus Exercises</span></span>

<span data-ttu-id="e07eb-512">**Exercice 1**</span><span class="sxs-lookup"><span data-stu-id="e07eb-512">**Exercise 1**</span></span>

<span data-ttu-id="e07eb-513">Il est tout à fait possible d’utiliser une seule scène pour modifier les vidéos de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e07eb-513">It is entirely possible to only use a single scene to change videos within this tutorial.</span></span> <span data-ttu-id="e07eb-514">Expérimentez votre application et faites-en une seule scène!</span><span class="sxs-lookup"><span data-stu-id="e07eb-514">Experiment with your application and make it into a single scene!</span></span> <span data-ttu-id="e07eb-515">Peut-être même ajouter une autre vidéo à la combinaison.</span><span class="sxs-lookup"><span data-stu-id="e07eb-515">Perhaps even add another video to the mix.</span></span>

<span data-ttu-id="e07eb-516">**Exercice 2**</span><span class="sxs-lookup"><span data-stu-id="e07eb-516">**Exercise 2**</span></span>

<span data-ttu-id="e07eb-517">Expérimentez Azure et Unity et tentez d’implémenter la possibilité pour l’application de sélectionner automatiquement une vidéo avec une taille de fichier différente, en fonction de la force d’une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="e07eb-517">Experiment with Azure and Unity, and attempt to implement the ability for the app to automatically select a video with a different file size, depending on the strength of an Internet connection.</span></span>


