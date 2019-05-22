---
title: MR et Azure 306 - diffusion en continu de vidéo
description: Terminer ce cours pour apprendre à implémenter Azure Media Services au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, streaming media services, vidéo, 360, immersives, vr
ms.openlocfilehash: f6974ab6a72828a557649d5dc65b4e505a7484ff
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594019"
---
>[!NOTE]
><span data-ttu-id="f720d-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="f720d-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="f720d-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="f720d-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="f720d-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="f720d-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="f720d-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f720d-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="f720d-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="f720d-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="f720d-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="f720d-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br> 

# <a name="mr-and-azure-306-streaming-video"></a><span data-ttu-id="f720d-110">MR et Azure 306 : Diffusion en continu de vidéo</span><span class="sxs-lookup"><span data-stu-id="f720d-110">MR and Azure 306: Streaming video</span></span>

<span data-ttu-id="f720d-111">![produit final-Démarrer](images/AzureLabs-Lab6-00.png)
![finale du produit-Démarrer](images/AzureLabs-Lab6-01.png)</span><span class="sxs-lookup"><span data-stu-id="f720d-111">![final product -start](images/AzureLabs-Lab6-00.png)
![final product -start](images/AzureLabs-Lab6-01.png)</span></span>

<span data-ttu-id="f720d-112">Dans ce cours, vous allez apprendre comment connecter votre Azure Media Services à une expérience de VR de réalité mixte Windows pour autoriser la lecture vidéo de 360 degrés sur des casques IMMERSIFS de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="f720d-112">In this course you will learn how connect your Azure Media Services to a Windows Mixed Reality VR experience to allow streaming 360 degree video playback on immersive headsets.</span></span> 

<span data-ttu-id="f720d-113">**Azure Media Services** sont une collection de services qui vous offre des services de streaming de vidéo de qualité télévisuelle pour atteindre un large public sur les appareils mobiles populaires d’aujourd'hui.</span><span class="sxs-lookup"><span data-stu-id="f720d-113">**Azure Media Services** are a collection of services that gives you broadcast-quality video streaming services to reach larger audiences on today’s most popular mobile devices.</span></span> <span data-ttu-id="f720d-114">Pour plus d’informations, visitez le [page d’Azure Media Services](https://azure.microsoft.com/services/media-services).</span><span class="sxs-lookup"><span data-stu-id="f720d-114">For more information, visit the [Azure Media Services page](https://azure.microsoft.com/services/media-services).</span></span>

<span data-ttu-id="f720d-115">Avoir terminé ce cours, vous disposez d’une application de casque immersives de réalité mixte, qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f720d-115">Having completed this course, you will have a mixed reality immersive headset application, which will be able to do the following:</span></span>

1. <span data-ttu-id="f720d-116">Récupérer une vidéo de 360 degrés à partir d’un **stockage Azure**, jusqu'à la **Azure Media Services**.</span><span class="sxs-lookup"><span data-stu-id="f720d-116">Retrieve a 360 degree video from an **Azure Storage**, through the **Azure Media Service**.</span></span>

2. <span data-ttu-id="f720d-117">Afficher la vidéo de 360 degrés récupérées dans une scène Unity.</span><span class="sxs-lookup"><span data-stu-id="f720d-117">Display the retrieved 360 degree video within a Unity scene.</span></span>

3. <span data-ttu-id="f720d-118">Naviguer entre les deux scènes, avec deux vidéos différents.</span><span class="sxs-lookup"><span data-stu-id="f720d-118">Navigate between two scenes, with two different videos.</span></span>

<span data-ttu-id="f720d-119">Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception.</span><span class="sxs-lookup"><span data-stu-id="f720d-119">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="f720d-120">Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="f720d-120">This course is designed to teach you how to integrate an Azure Service with your Unity Project.</span></span> <span data-ttu-id="f720d-121">Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="f720d-121">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

## <a name="device-support"></a><span data-ttu-id="f720d-122">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="f720d-122">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="f720d-123">Cours</span><span class="sxs-lookup"><span data-stu-id="f720d-123">Course</span></span></th><th style="width:150px"> <span data-ttu-id="f720d-124"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="f720d-124"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="f720d-125"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="f720d-125"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="f720d-126">MR et Azure 306 : Diffusion en continu de vidéo</span><span class="sxs-lookup"><span data-stu-id="f720d-126">MR and Azure 306: Streaming video</span></span></td><td style="text-align: center;"> </td><td style="text-align: center;"> <span data-ttu-id="f720d-127">✔️</span><span class="sxs-lookup"><span data-stu-id="f720d-127">✔️</span></span></td>
</tr>
</table>

## <a name="prerequisites"></a><span data-ttu-id="f720d-128">Prérequis</span><span class="sxs-lookup"><span data-stu-id="f720d-128">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="f720d-129">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="f720d-129">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="f720d-130">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="f720d-130">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="f720d-131">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer l’article outils](install-the-tools.md), mais il doit être pas supposé que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous .</span><span class="sxs-lookup"><span data-stu-id="f720d-131">You are free to use the latest software, as listed within the [install the tools article](install-the-tools.md), though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="f720d-132">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="f720d-132">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="f720d-133">Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)</span><span class="sxs-lookup"><span data-stu-id="f720d-133">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="f720d-134">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="f720d-134">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="f720d-135">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="f720d-135">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="f720d-136">Unity 2017.4</span><span class="sxs-lookup"><span data-stu-id="f720d-136">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="f720d-137">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f720d-137">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="f720d-138">Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md)</span><span class="sxs-lookup"><span data-stu-id="f720d-138">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md)</span></span>
- <span data-ttu-id="f720d-139">Accès à Internet pour la récupération de données et le programme d’installation Azure</span><span class="sxs-lookup"><span data-stu-id="f720d-139">Internet access for Azure setup and data retrieval</span></span>
- <span data-ttu-id="f720d-140">Deux vidéos à 360 degrés au format mp4 (vous trouverez des vidéos libres [à cette page de téléchargement](https://www.mettle.com/360vr-master-series-free-360-downloads-page))</span><span class="sxs-lookup"><span data-stu-id="f720d-140">Two 360-degree videos in mp4 format (you can find some royalty-free videos [at this download page](https://www.mettle.com/360vr-master-series-free-360-downloads-page))</span></span>

## <a name="before-you-start"></a><span data-ttu-id="f720d-141">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f720d-141">Before you start</span></span>

1.  <span data-ttu-id="f720d-142">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="f720d-142">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="f720d-143">Configurer et tester votre casque immersives de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="f720d-143">Set up and test your Mixed Reality Immersive Headset.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f720d-144">Vous allez **pas** nécessitent des contrôleurs de mouvement pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="f720d-144">You will **not** require Motion Controllers for this course.</span></span> <span data-ttu-id="f720d-145">Si vous avez besoin de prendre en charge de paramétrage le casque immersives, veuillez cliquer [lien sur la façon de configurer Windows Mixed Reality](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span><span class="sxs-lookup"><span data-stu-id="f720d-145">If you need support setting up the Immersive Headset, please click [link on how to set up Windows Mixed Reality](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span></span>

## <a name="chapter-1---the-azure-portal-creating-the-azure-storage-account"></a><span data-ttu-id="f720d-146">Chapitre 1 : le portail Azure : création du compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="f720d-146">Chapter 1 - The Azure Portal: creating the Azure Storage Account</span></span>

<span data-ttu-id="f720d-147">Pour utiliser le **Service de stockage Azure**, vous devez créer et configurer un **compte de stockage** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f720d-147">To use the **Azure Storage Service**, you will need to create and configure a **Storage Account** in the Azure portal.</span></span>

1.  <span data-ttu-id="f720d-148">Connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f720d-148">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE]
    > <span data-ttu-id="f720d-149">Si vous n’avez pas déjà un compte Azure, vous devrez créer un.</span><span class="sxs-lookup"><span data-stu-id="f720d-149">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="f720d-150">Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="f720d-150">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="f720d-151">Une fois que vous êtes connecté, cliquez sur **comptes de stockage** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="f720d-151">Once you are logged in, click on **Storage accounts** in the left menu.</span></span>

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab6-02.png)

3.  <span data-ttu-id="f720d-153">Sur le **comptes de stockage** onglet, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f720d-153">On the **Storage Accounts** tab, click on **Add**.</span></span>

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab6-03.png)

4.  <span data-ttu-id="f720d-155">Dans le **créer le compte de stockage** onglet :</span><span class="sxs-lookup"><span data-stu-id="f720d-155">In the **Create storage account** tab:</span></span>

    1.  <span data-ttu-id="f720d-156">Insérer un **nom** pour votre compte, n’oubliez pas ce champ accepte uniquement des lettres minuscules et chiffres.</span><span class="sxs-lookup"><span data-stu-id="f720d-156">Insert a **Name** for your account, be aware this field only accepts numbers, and lowercase letters.</span></span>

    2.  <span data-ttu-id="f720d-157">Pour **modèle de déploiement,** sélectionnez **Resource manager**.</span><span class="sxs-lookup"><span data-stu-id="f720d-157">For **Deployment model,** select **Resource manager**.</span></span>

    3.  <span data-ttu-id="f720d-158">Pour **type de compte**, sélectionnez **stockage (usage général v1)**.</span><span class="sxs-lookup"><span data-stu-id="f720d-158">For **Account kind**, select **Storage (general purpose v1)**.</span></span>

    4.  <span data-ttu-id="f720d-159">Pour **performances**, sélectionnez **Standard\*.**</span><span class="sxs-lookup"><span data-stu-id="f720d-159">For **Performance**, select **Standard\*.**</span></span>

    5.  <span data-ttu-id="f720d-160">Pour **réplication** sélectionnez **stockage localement redondant (LRS)**.</span><span class="sxs-lookup"><span data-stu-id="f720d-160">For **Replication** select **Locally-redundant storage (LRS)**.</span></span>

    6.  <span data-ttu-id="f720d-161">Laissez **transfert sécurisé requis** comme **désactivé**.</span><span class="sxs-lookup"><span data-stu-id="f720d-161">Leave **Secure transfer required** as **Disabled**.</span></span>

    7.  <span data-ttu-id="f720d-162">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="f720d-162">Select a **Subscription**.</span></span>

    8.  <span data-ttu-id="f720d-163">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="f720d-163">Choose a **Resource group** or create a new one.</span></span> <span data-ttu-id="f720d-164">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f720d-164">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span>

    9.  <span data-ttu-id="f720d-165">Déterminer le **emplacement** pour votre groupe de ressources (si vous créez un nouveau groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="f720d-165">Determine the **Location** for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="f720d-166">Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="f720d-166">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="f720d-167">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="f720d-167">Some Azure assets are only available in certain regions.</span></span>

5.  <span data-ttu-id="f720d-168">Vous devrez confirmer que vous avez compris les termes et Conditions appliquées à ce Service.</span><span class="sxs-lookup"><span data-stu-id="f720d-168">You will need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab6-04.png)

6.  <span data-ttu-id="f720d-170">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="f720d-170">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

7.  <span data-ttu-id="f720d-171">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="f720d-171">A notification will appear in the portal once the Service instance is created.</span></span>

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab6-05.png)

8.  <span data-ttu-id="f720d-173">À ce stade vous n’avez pas besoin de suivre la ressource, il suffit de déplacer le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="f720d-173">At this point you do not need to follow the resource, simply move to the next Chapter.</span></span>

## <a name="chapter-2---the-azure-portal-creating-the-media-service"></a><span data-ttu-id="f720d-174">Chapitre 2 : le portail Azure : création du Service de média</span><span class="sxs-lookup"><span data-stu-id="f720d-174">Chapter 2 - The Azure Portal: creating the Media Service</span></span>

<span data-ttu-id="f720d-175">Pour utiliser le Service de média Azure, vous devrez configurer une instance du service à être mis à disposition de votre application (où le titulaire du compte doit être un administrateur).</span><span class="sxs-lookup"><span data-stu-id="f720d-175">To use the Azure Media Service, you will need to configure an instance of the service to be made available to your application (wherein the account holder needs to be an Admin).</span></span>

1.  <span data-ttu-id="f720d-176">Dans le portail Azure, cliquez sur **créer une ressource** dans le coin supérieur gauche coin inférieur droit, puis recherchez **Service multimédia,** appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="f720d-176">In the Azure Portal, click on **Create a resource** in the top left corner, and search for **Media Service,** press **Enter**.</span></span> <span data-ttu-id="f720d-177">Sur la ressource actuellement possède une icône rose ; cliquez dessus, pour afficher une nouvelle page.</span><span class="sxs-lookup"><span data-stu-id="f720d-177">The resource you want currently has a pink icon; click this, to show a new page.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-06.png)

2.  <span data-ttu-id="f720d-179">La nouvelle page doit fournir une description de la **Service multimédia**.</span><span class="sxs-lookup"><span data-stu-id="f720d-179">The new page will provide a description of the **Media Service**.</span></span> <span data-ttu-id="f720d-180">En bas à gauche de cette invite, cliquez sur le **créer** bouton permettant de créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="f720d-180">At the bottom left of this prompt, click the **Create** button, to create an association with this service.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-07.png)

3.  <span data-ttu-id="f720d-182">Une fois que vous avez cliqué sur **créer** un panneau s’affiche où vous devez fournir des détails sur votre nouveau Service de support :</span><span class="sxs-lookup"><span data-stu-id="f720d-182">Once you have clicked on **Create** a panel will appear where you need to provide some details about your new Media Service:</span></span>

    1.  <span data-ttu-id="f720d-183">Insérez votre souhaitée **nom du compte** pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="f720d-183">Insert your desired **Account Name** for this service instance.</span></span>

    2.  <span data-ttu-id="f720d-184">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="f720d-184">Select a **Subscription**.</span></span>

    3. <span data-ttu-id="f720d-185">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="f720d-185">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="f720d-186">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f720d-186">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="f720d-187">Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="f720d-187">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span> 
    
    > <span data-ttu-id="f720d-188">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la gestion des groupes de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="f720d-188">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage Azure Resource Groups](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    4.  <span data-ttu-id="f720d-189">Déterminer le **emplacement** pour votre groupe de ressources (si vous créez un nouveau groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="f720d-189">Determine the **Location** for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="f720d-190">Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="f720d-190">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="f720d-191">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="f720d-191">Some Azure assets are only available in certain regions.</span></span>

    5.  <span data-ttu-id="f720d-192">Pour le **compte de stockage** , cliquez sur le **Veuillez sélectionner...**  section, puis cliquez sur le **compte de stockage** vous avez créé dans le dernier chapitre.</span><span class="sxs-lookup"><span data-stu-id="f720d-192">For the **Storage Account** section, click the **Please select...** section, then click the **Storage Account** you created in the last Chapter.</span></span>

    6.  <span data-ttu-id="f720d-193">Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.</span><span class="sxs-lookup"><span data-stu-id="f720d-193">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    7.  <span data-ttu-id="f720d-194">Cliquez sur **Create (Créer)**.</span><span class="sxs-lookup"><span data-stu-id="f720d-194">Click **Create**.</span></span>

        ![Le portail Azure](images/AzureLabs-Lab6-08.png)

4.  <span data-ttu-id="f720d-196">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="f720d-196">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

5.  <span data-ttu-id="f720d-197">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="f720d-197">A notification will appear in the portal once the Service instance is created.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-09.png)

6.  <span data-ttu-id="f720d-199">Cliquez sur la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="f720d-199">Click on the notification to explore your new Service instance.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-10.png)

7.  <span data-ttu-id="f720d-201">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="f720d-201">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span>

8.  <span data-ttu-id="f720d-202">Dans la nouvelle page de service de média, dans le volet gauche, cliquez sur le **actifs** lien, qui vise à mi-chemin vers le bas.</span><span class="sxs-lookup"><span data-stu-id="f720d-202">Within the new Media service page, within the panel on the left, click on the **Assets** link, which is about halfway down.</span></span>

9.  <span data-ttu-id="f720d-203">Dans la page suivante, dans l’angle supérieur gauche de la page, cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="f720d-203">On the next page, in the top-left corner of the page, click **Upload**.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-11.png)

10. <span data-ttu-id="f720d-205">Cliquez sur le **dossier** icône pour parcourir vos fichiers et sélectionnez la vidéo 360 tout d’abord que vous souhaitez diffuser en continu.</span><span class="sxs-lookup"><span data-stu-id="f720d-205">Click on the **Folder** icon to browse your files and select the first 360 Video that you would like to stream.</span></span> 
    
    > <span data-ttu-id="f720d-206">Vous pouvez suivre cette [lien pour télécharger un exemple de vidéo](https://vimeo.com/214401712).</span><span class="sxs-lookup"><span data-stu-id="f720d-206">You can follow this [link to download a sample video](https://vimeo.com/214401712).</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-12.png)

> [!WARNING]
> <span data-ttu-id="f720d-208">Noms de fichiers longs peut entraîner un problème avec l’encodeur : pour vous assurer de vidéos n’ont pas de problèmes, vous devez donc raccourcir la longueur des noms de votre fichier vidéo.</span><span class="sxs-lookup"><span data-stu-id="f720d-208">Long filenames may cause an issue with the encoder: so to ensure videos do not have issues, consider shortening the length of your video file names.</span></span>

11. <span data-ttu-id="f720d-209">La barre de progression devient verte lorsque la vidéo a fini de télécharger.</span><span class="sxs-lookup"><span data-stu-id="f720d-209">The progress bar will turn green when the video has finished uploading.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-13.png)

12. <span data-ttu-id="f720d-211">Cliquez sur le texte ci-dessus (**yourservicename - ressources**) pour revenir à la **actifs** page.</span><span class="sxs-lookup"><span data-stu-id="f720d-211">Click on the text above (**yourservicename - Assets**) to return to the **Assets** page.</span></span>

13. <span data-ttu-id="f720d-212">Vous remarquerez que votre vidéo a été téléchargée avec succès.</span><span class="sxs-lookup"><span data-stu-id="f720d-212">You will notice that your video has been successfully uploaded.</span></span> <span data-ttu-id="f720d-213">Cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="f720d-213">Click on it.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-14.png)

14. <span data-ttu-id="f720d-215">Affiche la page que vous êtes redirigé vers que vous des informations détaillées sur votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="f720d-215">The page you are redirected to will show you detailed information about your video.</span></span> <span data-ttu-id="f720d-216">Pour pouvoir utiliser votre vidéo, vous devez encoder, en cliquant sur le **Encode** bouton en haut à gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="f720d-216">To be able to use your video you need to encode it, by clicking the **Encode** button at the top-left of the page.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-15.png)

15. <span data-ttu-id="f720d-218">Un nouveau panneau s’affiche à droite, où vous serez en mesure de définir les options de codage pour votre fichier.</span><span class="sxs-lookup"><span data-stu-id="f720d-218">A new panel will appear to the right, where you will be able to set encoding options for your file.</span></span> <span data-ttu-id="f720d-219">Définissez les propriétés suivantes (certaines seront déjà défini par défaut) :</span><span class="sxs-lookup"><span data-stu-id="f720d-219">Set the following properties (some will be already set by default):</span></span>

    1.  <span data-ttu-id="f720d-220">**Nom de l’encodeur multimédia *Media Encoder Standard***</span><span class="sxs-lookup"><span data-stu-id="f720d-220">**Media encoder name *Media Encoder Standard***</span></span>

    2.  <span data-ttu-id="f720d-221">**Présélection d’encodage *contenu ADAPTATIF MP4 à plusieurs débits***</span><span class="sxs-lookup"><span data-stu-id="f720d-221">**Encoding preset *Content Adaptive Multiple Bitrate MP4***</span></span>

    3.  <span data-ttu-id="f720d-222">**Nom de la tâche *traitement Media Encoder Standard de Video1.mp4***</span><span class="sxs-lookup"><span data-stu-id="f720d-222">**Job name *Media Encoder Standard processing of Video1.mp4***</span></span>

    4.  <span data-ttu-id="f720d-223">**Nom du fichier multimédia sortie *Video1.mp4--Media Encoder Standard encodé***</span><span class="sxs-lookup"><span data-stu-id="f720d-223">**Output media asset name *Video1.mp4 -- Media Encoder Standard encoded***</span></span>

        ![Le portail Azure](images/AzureLabs-Lab6-16.png)

16. <span data-ttu-id="f720d-225">Cliquez sur le bouton **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f720d-225">Click the **Create** button.</span></span>

17. <span data-ttu-id="f720d-226">Vous remarquerez une barre avec **travail d’encodage ajouté**, cliquez sur cette barre et un panneau s’affiche avec la progression de l’encodage affichée dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="f720d-226">You will notice a bar with **Encoding job added**, click on that bar and a panel will appear with the Encoding progress displayed in it.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-17.png)

    ![Le portail Azure](images/AzureLabs-Lab6-18.png)

18. <span data-ttu-id="f720d-229">Attendez la fin du travail.</span><span class="sxs-lookup"><span data-stu-id="f720d-229">Wait for the Job to be completed.</span></span> <span data-ttu-id="f720d-230">Une fois que cela est fait, n’hésitez pas à fermer le panneau avec le « X » en haut à droite de ce panneau.</span><span class="sxs-lookup"><span data-stu-id="f720d-230">Once it is done, feel free to close the panel with the 'X' at the top right of that panel.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-19.png)

    ![Le portail Azure](images/AzureLabs-Lab6-20.png)

    > [!IMPORTANT]
    > <span data-ttu-id="f720d-233">La durée, dépend de la taille du fichier de votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="f720d-233">The time this takes, depends on the file size of your video.</span></span> <span data-ttu-id="f720d-234">Ce processus peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="f720d-234">This process can take quite some time.</span></span>

19. <span data-ttu-id="f720d-235">Maintenant que la version codée de la vidéo a été créée, vous pouvez le publier pour le rendre accessible.</span><span class="sxs-lookup"><span data-stu-id="f720d-235">Now that the encoded version of the video has been created, you can publish it to make it accessible.</span></span> <span data-ttu-id="f720d-236">Pour ce faire, cliquez sur le lien bleu **actifs** pour revenir à la page de ressources.</span><span class="sxs-lookup"><span data-stu-id="f720d-236">To do so, click the blue link **Assets** to go back to the assets page.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-21.png)

20. <span data-ttu-id="f720d-238">Vous verrez votre vidéo, ainsi que l’autre, ce qui est de \*\*Type de ressource \*MP4 multidébit\*\*\*.</span><span class="sxs-lookup"><span data-stu-id="f720d-238">You will see your video along with another, which is of \*\*Asset Type \*Multi-Bitrate MP4\*\*\*.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-22.png)

    > [!NOTE] 
    > <span data-ttu-id="f720d-240">Vous pouvez remarquer que le nouvel élément multimédia, en même temps que votre vidéo initial, est *inconnu*, et a octets '0' pour qu’il est **taille**, actualisez simplement votre fenêtre pour pouvoir mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="f720d-240">You may notice that the new asset, alongside your initial video, is *Unknown*, and has '0' bytes for it's **Size**, just refresh your window for it to update.</span></span>

21. <span data-ttu-id="f720d-241">Cliquez sur cette nouvelle ressource.</span><span class="sxs-lookup"><span data-stu-id="f720d-241">Click this new asset.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-23.png)

22. <span data-ttu-id="f720d-243">Vous verrez un panneau semblable à celle que vous avez utilisé auparavant, simplement, il s’agit d’une autre ressource.</span><span class="sxs-lookup"><span data-stu-id="f720d-243">You will see a similar panel to the one you used before, just this is a different asset.</span></span> <span data-ttu-id="f720d-244">Cliquez sur le **publier** bouton situé au centre en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="f720d-244">Click the **Publish** button located at the top-center of the page.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-24.png)

23. <span data-ttu-id="f720d-246">Vous êtes invité à définir un **localisateur**, qui est le point d’entrée au fichier/s dans vos éléments multimédias.</span><span class="sxs-lookup"><span data-stu-id="f720d-246">You will be prompted to set a **Locator**, which is the entry point, to file/s in your Assets.</span></span> <span data-ttu-id="f720d-247">Pour votre scénario, définissez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="f720d-247">For your scenario set the following properties:</span></span>

    1.  <span data-ttu-id="f720d-248">**Type de localisateur** > **progressif**.</span><span class="sxs-lookup"><span data-stu-id="f720d-248">**Locator type** > **Progressive**.</span></span>

    2.  <span data-ttu-id="f720d-249">Le **date** et **temps** sont définies pour vous, à partir de votre date actuelle, à une heure dans le futur (cent ans dans le cas présent).</span><span class="sxs-lookup"><span data-stu-id="f720d-249">The **date** and **time** will be set for you, from your current date, to a time in the future (one hundred years in this case).</span></span> <span data-ttu-id="f720d-250">Laissez tel quel ou le modifier en fonction.</span><span class="sxs-lookup"><span data-stu-id="f720d-250">Leave as is or change it to suit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f720d-251">Pour plus d’informations sur les localisateurs, et vous pouvez choisir, visitez le [Documentation Azure Media Services](https://docs.microsoft.com/azure/media-services/media-services-concepts).</span><span class="sxs-lookup"><span data-stu-id="f720d-251">For more information about Locators, and what you can choose, visit the [Azure Media Services Documentation](https://docs.microsoft.com/azure/media-services/media-services-concepts).</span></span>

24. <span data-ttu-id="f720d-252">En bas de ce panneau, cliquez sur le **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="f720d-252">At the bottom of that panel, click on the **Add** button.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-25.png)

25. <span data-ttu-id="f720d-254">Votre vidéo est à présent publiée et puisse être diffusé en continu à l’aide de son point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="f720d-254">Your video is now published and can be streamed by using its endpoint.</span></span> <span data-ttu-id="f720d-255">Plus bas de la page est un **fichiers** section.</span><span class="sxs-lookup"><span data-stu-id="f720d-255">Further down the page is a **Files** section.</span></span> <span data-ttu-id="f720d-256">Ceci est l’emplacement codé en différentes versions de votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="f720d-256">This is where the different encoded versions of your video will be.</span></span> <span data-ttu-id="f720d-257">Sélectionnez la plus élevée possible une résolution (dans l’image ci-dessous est le 1920 x 960 fichier), et un volet à droite s’affichera.</span><span class="sxs-lookup"><span data-stu-id="f720d-257">Select the highest possible resolution one (in the image below it is the 1920x960 file), and then a panel to the right will appear.</span></span> <span data-ttu-id="f720d-258">Vous y trouverez un **URL de téléchargement**.</span><span class="sxs-lookup"><span data-stu-id="f720d-258">There you will find a **Download URL**.</span></span> <span data-ttu-id="f720d-259">Copiez cette **point de terminaison** car vous l’utiliserez ultérieurement dans votre code.</span><span class="sxs-lookup"><span data-stu-id="f720d-259">Copy this **Endpoint** as you will use it later in your code.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-26.png)    

    ![Le portail Azure](images/AzureLabs-Lab6-27.png)

    > [!NOTE] 
    > <span data-ttu-id="f720d-262">Vous pouvez également appuyer sur la **lire** bouton pour lire votre vidéo et le tester.</span><span class="sxs-lookup"><span data-stu-id="f720d-262">You can also press the **Play** button to play your video and test it.</span></span>

26. <span data-ttu-id="f720d-263">Vous devez maintenant télécharger la deuxième vidéo que vous utiliserez dans ce laboratoire.</span><span class="sxs-lookup"><span data-stu-id="f720d-263">You now need to upload the second video that you will use in this Lab.</span></span> <span data-ttu-id="f720d-264">Suivez les étapes ci-dessus, en répétant le même processus pour la deuxième vidéo.</span><span class="sxs-lookup"><span data-stu-id="f720d-264">Follow the steps above, repeating the same process for the second video.</span></span> <span data-ttu-id="f720d-265">Assurez-vous que vous copiez la deuxième **point de terminaison** également.</span><span class="sxs-lookup"><span data-stu-id="f720d-265">Ensure you copy the second **Endpoint** also.</span></span> <span data-ttu-id="f720d-266">Utilisez la commande suivante [lien pour télécharger une vidéo deuxième](https://vimeo.com/214402865).</span><span class="sxs-lookup"><span data-stu-id="f720d-266">Use the following [link to download a second video](https://vimeo.com/214402865).</span></span>

27. <span data-ttu-id="f720d-267">Une fois que les deux vidéos ont été publiés, vous êtes prêt à passer au chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="f720d-267">Once both videos have been published, you are ready to move to the next Chapter.</span></span>

## <a name="chapter-3---setting-up-the-unity-project"></a><span data-ttu-id="f720d-268">Chapitre 3 - Configuration du projet Unity</span><span class="sxs-lookup"><span data-stu-id="f720d-268">Chapter 3 - Setting up the Unity Project</span></span>

<span data-ttu-id="f720d-269">Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="f720d-269">The following is a typical set up for developing with the Mixed Reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="f720d-270">Ouvrez **Unity** et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="f720d-270">Open **Unity** and click **New**.</span></span> 

    ![Le portail Azure](images/AzureLabs-Lab6-28.png)

2.  <span data-ttu-id="f720d-272">Vous devez maintenant fournir un nom de projet Unity, insérer **MR\_360VideoStreaming.**.</span><span class="sxs-lookup"><span data-stu-id="f720d-272">You will now need to provide a Unity Project name, insert **MR\_360VideoStreaming.**.</span></span> <span data-ttu-id="f720d-273">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="f720d-273">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="f720d-274">Définissez l’emplacement d’un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="f720d-274">Set the Location to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="f720d-275">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="f720d-275">Then, click **Create project**.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-29.png)

3.  <span data-ttu-id="f720d-277">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="f720d-277">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio.**</span></span> <span data-ttu-id="f720d-278">Accédez à ***modifier* *préférences*** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="f720d-278">Go to ***Edit* *Preferences*** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="f720d-279">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="f720d-279">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="f720d-280">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f720d-280">Close the **Preferences** window.</span></span>

    ![Le portail Azure](images/AzureLabs-Lab6-30.png)

4.  <span data-ttu-id="f720d-282">Ensuite, accédez à ***fichier* *paramètres de Build*** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **Plateforme de commutation** bouton.</span><span class="sxs-lookup"><span data-stu-id="f720d-282">Next, go to ***File* *Build Settings*** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

5.  <span data-ttu-id="f720d-283">Assurez-vous également que :</span><span class="sxs-lookup"><span data-stu-id="f720d-283">Also make sure that:</span></span>

    1. <span data-ttu-id="f720d-284">**Équipement cible** a la valeur **n’importe quel appareil.**</span><span class="sxs-lookup"><span data-stu-id="f720d-284">**Target Device** is set to **Any Device.**</span></span>
    
    2.  <span data-ttu-id="f720d-285">**Type de build** a la valeur **D3D.**</span><span class="sxs-lookup"><span data-stu-id="f720d-285">**Build Type** is set to **D3D.**</span></span>

    3.  <span data-ttu-id="f720d-286">**Kit de développement logiciel** a la valeur **dernière installé.**</span><span class="sxs-lookup"><span data-stu-id="f720d-286">**SDK** is set to **Latest installed.**</span></span>

    4.  <span data-ttu-id="f720d-287">**Version de Visual Studio** a la valeur **dernière installé.**</span><span class="sxs-lookup"><span data-stu-id="f720d-287">**Visual Studio Version** is set to **Latest installed.**</span></span>

    5.  <span data-ttu-id="f720d-288">**Générez et exécutez** est défini sur **ordinateur Local.**</span><span class="sxs-lookup"><span data-stu-id="f720d-288">**Build and Run** is set to **Local Machine.**</span></span>

    6.  <span data-ttu-id="f720d-289">Ne vous inquiétez pas sur la configuration de **scènes** dès que vous allez configurer ces ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f720d-289">Do not worry about setting up **Scenes** right now, as you will set these up later.</span></span>

    7.  <span data-ttu-id="f720d-290">Les autres paramètres doivent être conservées comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="f720d-290">The remaining settings should be left as default for now.</span></span>

        ![Configuration du projet Unity](images/AzureLabs-Lab6-31.png)

6.  <span data-ttu-id="f720d-292">Dans le **paramètres de Build** fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le **inspecteur** se trouve.</span><span class="sxs-lookup"><span data-stu-id="f720d-292">In the **Build Settings** window, click on the **Player Settings** button, this will open the related panel in the space where the **Inspector** is located.</span></span> 

7. <span data-ttu-id="f720d-293">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="f720d-293">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="f720d-294">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="f720d-294">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="f720d-295">**Écriture de scripts** **Version du Runtime** doit être **Stable** (équivalent .NET 3.5).</span><span class="sxs-lookup"><span data-stu-id="f720d-295">**Scripting** **Runtime Version** should be **Stable** (.NET 3.5 Equivalent).</span></span>

        2. <span data-ttu-id="f720d-296">**Script principal** doit être **.NET.**</span><span class="sxs-lookup"><span data-stu-id="f720d-296">**Scripting Backend** should be **.NET.**</span></span>

        3. <span data-ttu-id="f720d-297">**Niveau de compatibilité d’API** doit être **.NET 4.6.**</span><span class="sxs-lookup"><span data-stu-id="f720d-297">**API Compatibility Level** should be **.NET 4.6.**</span></span>

            ![Configuration du projet Unity](images/AzureLabs-Lab6-32.png)

    2.  <span data-ttu-id="f720d-299">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.</span><span class="sxs-lookup"><span data-stu-id="f720d-299">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Configuration du projet Unity](images/AzureLabs-Lab6-33.png)

    3.  <span data-ttu-id="f720d-301">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="f720d-301">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="f720d-302">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="f720d-302">**InternetClient**</span></span>

            ![Configuration du projet Unity](images/AzureLabs-Lab6-34.png)

8.  <span data-ttu-id="f720d-304">Une fois que vous avez effectué ces modifications, fermez le **paramètres de Build** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f720d-304">Once you have made those changes, close the **Build Settings** window.</span></span>

9.  <span data-ttu-id="f720d-305">Enregistrer votre projet \**fichier* \*enregistrer projet \*\*.</span><span class="sxs-lookup"><span data-stu-id="f720d-305">Save your Project \**File* \*Save Project\*\*.</span></span>



## <a name="chapter-4---importing-the-insideoutsphere-unity-package"></a><span data-ttu-id="f720d-306">Chapitre 4 - Importation du package InsideOutSphere Unity</span><span class="sxs-lookup"><span data-stu-id="f720d-306">Chapter 4 - Importing the InsideOutSphere Unity package</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f720d-307">Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20306%20-%20Streaming%20video/Azure-MR-306.unitypackage), importez-le dans votre projet comme un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de **chapitre 5**.</span><span class="sxs-lookup"><span data-stu-id="f720d-307">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to download this [.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20306%20-%20Streaming%20video/Azure-MR-306.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from **Chapter 5**.</span></span> <span data-ttu-id="f720d-308">Vous devez toujours créer un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="f720d-308">You will still need to create a Unity Project.</span></span>

<span data-ttu-id="f720d-309">Pour ce cours, vous devez télécharger un Package de ressource Unity appelé [ **InsideOutSphere.unitypackage**](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20306%20-%20Streaming%20video/InsideOutSphere.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="f720d-309">For this course you will need to download a Unity Asset Package called [**InsideOutSphere.unitypackage**](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20306%20-%20Streaming%20video/InsideOutSphere.unitypackage).</span></span>

<span data-ttu-id="f720d-310">Importation de procédures relatives à la **package**:</span><span class="sxs-lookup"><span data-stu-id="f720d-310">How-to import the **unitypackage**:</span></span>

1.  <span data-ttu-id="f720d-311">Avec le tableau de bord Unity devant vous, cliquez sur **actifs** dans le menu en haut de l’écran, puis cliquez sur **importer un Package > Custom Package**.</span><span class="sxs-lookup"><span data-stu-id="f720d-311">With the Unity dashboard in front of you, click on **Assets** in the menu at the top of the screen, then click on **Import Package > Custom Package**.</span></span>

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-35.png)

2.  <span data-ttu-id="f720d-313">Utilisez le sélecteur de fichiers pour sélectionner le **InsideOutSphere.unitypackage** du package et cliquez sur **Open**.</span><span class="sxs-lookup"><span data-stu-id="f720d-313">Use the file picker to select the **InsideOutSphere.unitypackage** package and click **Open**.</span></span> <span data-ttu-id="f720d-314">Une liste des composants de cette ressource s’affichera pour vous.</span><span class="sxs-lookup"><span data-stu-id="f720d-314">A list of components for this asset will be displayed to you.</span></span> <span data-ttu-id="f720d-315">Confirmez l’importation en cliquant sur **importer**.</span><span class="sxs-lookup"><span data-stu-id="f720d-315">Confirm the import by clicking **Import**.</span></span>

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-36.png)

3.  <span data-ttu-id="f720d-317">Une fois l’importation terminée, vous remarquerez trois nouveaux dossiers, **matériaux**, **modèles**, et **Prefabs**, ont été ajoutées à votre **actifs**dossier.</span><span class="sxs-lookup"><span data-stu-id="f720d-317">Once it has finished importing, you will notice three new folders, **Materials**, **Models**, and **Prefabs**, have been added to your **Assets** folder.</span></span> <span data-ttu-id="f720d-318">Ce type de structure de dossiers est généralement utilisé pour un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="f720d-318">This kind of folder structure is typical for a Unity project.</span></span>

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-37.png)

    1.  <span data-ttu-id="f720d-320">Ouvrez le **modèles** dossier et vous verrez que le **InsideOutSphere** modèle a été importé.</span><span class="sxs-lookup"><span data-stu-id="f720d-320">Open the **Models** folder, and you will see that the **InsideOutSphere** model has been imported.</span></span>

    2.  <span data-ttu-id="f720d-321">Dans le **matériaux** dossier, vous trouverez le **InsideOutSpheres** matériau *lambert1*, ainsi que d’un matériau appelé *ButtonMaterial*, qui est utilisé par le GazeButton, que vous le verrez bientôt.</span><span class="sxs-lookup"><span data-stu-id="f720d-321">Within the **Materials** folder you will find the **InsideOutSpheres** material  *lambert1*, along with a material called *ButtonMaterial*, which is used by the GazeButton, which you will see soon.</span></span>

    3.  <span data-ttu-id="f720d-322">Le **Prefabs** dossier contient le **InsideOutSphere** préfabriqué qui contient à la fois le **InsideOutSphere** *modèle* et le  *GazeButton*.</span><span class="sxs-lookup"><span data-stu-id="f720d-322">The **Prefabs** folder contains the **InsideOutSphere** prefab which contains both the **InsideOutSphere** *model* and the *GazeButton*.</span></span>

    4.  <span data-ttu-id="f720d-323">**Aucun code n’est inclus**, vous allez écrire le code en suivant ce cours.</span><span class="sxs-lookup"><span data-stu-id="f720d-323">**No code is included**, you will write the code by following this course.</span></span>


4.  <span data-ttu-id="f720d-324">Dans le **hiérarchie**, sélectionnez le **Main Camera** l’objet et de mettre à jour les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="f720d-324">Within the **Hierarchy**, select the **Main Camera** object, and update the following components:</span></span>

    1.  <span data-ttu-id="f720d-325">**Transform**</span><span class="sxs-lookup"><span data-stu-id="f720d-325">**Transform**</span></span>

        1.  <span data-ttu-id="f720d-326">Position = **X**: 0, **Y**: 0, **Z**: 0.</span><span class="sxs-lookup"><span data-stu-id="f720d-326">Position = **X**: 0, **Y**: 0, **Z**: 0.</span></span>

        2. <span data-ttu-id="f720d-327">Rotation = **X**: 0, **Y**: 0, **Z**: 0.</span><span class="sxs-lookup"><span data-stu-id="f720d-327">Rotation = **X**: 0, **Y**: 0, **Z**: 0.</span></span>

        3. <span data-ttu-id="f720d-328">Mise à l’échelle **X**: 1, **Y**: 1, **Z**: 1.</span><span class="sxs-lookup"><span data-stu-id="f720d-328">Scale **X**: 1, **Y**: 1, **Z**: 1.</span></span>

    2.  <span data-ttu-id="f720d-329">**Appareil photo**</span><span class="sxs-lookup"><span data-stu-id="f720d-329">**Camera**</span></span>

        1. <span data-ttu-id="f720d-330">**Effacer les indicateurs**: Couleur unie.</span><span class="sxs-lookup"><span data-stu-id="f720d-330">**Clear Flags**: Solid Color.</span></span>

        2.  <span data-ttu-id="f720d-331">**Plans de détourage**: Près de : 0,1, à présent : 6.</span><span class="sxs-lookup"><span data-stu-id="f720d-331">**Clipping Planes**: Near: 0.1, Far: 6.</span></span>

            ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-38.png)

5.  <span data-ttu-id="f720d-333">Accédez à la **Prefab** dossier, puis faites glisser le **InsideOutSphere** prefab dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="f720d-333">Navigate to the **Prefab** folder, and then drag the **InsideOutSphere** prefab into the **Hierarchy** Panel.</span></span>

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-39.png)

6.  <span data-ttu-id="f720d-335">Développez le **InsideOutSphere** de l’objet dans le **hiérarchie** en cliquant sur la petite flèche située en regard de celle-ci.</span><span class="sxs-lookup"><span data-stu-id="f720d-335">Expand the **InsideOutSphere** object within the **Hierarchy** by clicking the little arrow next to it.</span></span> <span data-ttu-id="f720d-336">Vous verrez un **enfant** objet dessous appelé **GazeButton**.</span><span class="sxs-lookup"><span data-stu-id="f720d-336">You will see a **child** object beneath it called **GazeButton**.</span></span> <span data-ttu-id="f720d-337">Cela sera utilisé pour modifier l’arrière-plan et par conséquent, des vidéos.</span><span class="sxs-lookup"><span data-stu-id="f720d-337">This will be used to change scenes and thus videos.</span></span>

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-40.png)

7.  <span data-ttu-id="f720d-339">Dans la fenêtre Inspecteur, cliquez sur le **InsideOutSphere**du composant de transformation, assurez-vous que les propriétés suivantes sont définies :</span><span class="sxs-lookup"><span data-stu-id="f720d-339">In the Inspector Window click on the **InsideOutSphere**'s Transform component, ensure that the following properties are set:</span></span>

    |            |    <span data-ttu-id="f720d-340">TRANSFORMATION - POSITION</span><span class="sxs-lookup"><span data-stu-id="f720d-340">TRANSFORM - POSITION</span></span>   |           |
    | :---------:| :-----------------------: | :--------:|
    |   <span data-ttu-id="f720d-341">**X** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-341">**X** 0</span></span>  |          <span data-ttu-id="f720d-342">**Y** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-342">**Y** 0</span></span>          |  <span data-ttu-id="f720d-343">**Z** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-343">**Z** 0</span></span>  |

    |            |    <span data-ttu-id="f720d-344">TRANSFORMATION - ROTATION</span><span class="sxs-lookup"><span data-stu-id="f720d-344">TRANSFORM - ROTATION</span></span>   |           |
    | :---------:| :-----------------------: | :--------:|
    |   <span data-ttu-id="f720d-345">**X** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-345">**X** 0</span></span>  |          <span data-ttu-id="f720d-346">**Y** -50</span><span class="sxs-lookup"><span data-stu-id="f720d-346">**Y** -50</span></span>        |  <span data-ttu-id="f720d-347">**Z** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-347">**Z** 0</span></span>  |

    |            |     <span data-ttu-id="f720d-348">TRANSFORMATION - MISE À L’ÉCHELLE</span><span class="sxs-lookup"><span data-stu-id="f720d-348">TRANSFORM - SCALE</span></span>     |           |
    | :---------:| :-----------------------: | :--------:|
    |  <span data-ttu-id="f720d-349">**X** 1</span><span class="sxs-lookup"><span data-stu-id="f720d-349">**X** 1</span></span>   |          <span data-ttu-id="f720d-350">**Y** 1</span><span class="sxs-lookup"><span data-stu-id="f720d-350">**Y** 1</span></span>          |  <span data-ttu-id="f720d-351">**Z** 1</span><span class="sxs-lookup"><span data-stu-id="f720d-351">**Z** 1</span></span>  |

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-41.png)

8.  <span data-ttu-id="f720d-353">Cliquez sur le **GazeButton** objet enfant et définissez son **transformer** comme suit :</span><span class="sxs-lookup"><span data-stu-id="f720d-353">Click on the **GazeButton** child object, and set its **Transform** as follows:</span></span>

    |            |    <span data-ttu-id="f720d-354">TRANSFORMATION - POSITION</span><span class="sxs-lookup"><span data-stu-id="f720d-354">TRANSFORM - POSITION</span></span>   |           |
    | :---------:| :-----------------------: | :--------:|
    |   <span data-ttu-id="f720d-355">**X** 3.6</span><span class="sxs-lookup"><span data-stu-id="f720d-355">**X** 3.6</span></span>|          <span data-ttu-id="f720d-356">**Y** 1.3</span><span class="sxs-lookup"><span data-stu-id="f720d-356">**Y** 1.3</span></span>        |  <span data-ttu-id="f720d-357">**Z** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-357">**Z** 0</span></span>  |

    |            |    <span data-ttu-id="f720d-358">TRANSFORMATION - ROTATION</span><span class="sxs-lookup"><span data-stu-id="f720d-358">TRANSFORM - ROTATION</span></span>   |           |
    | :---------:| :-----------------------: | :--------:|
    |   <span data-ttu-id="f720d-359">**X** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-359">**X** 0</span></span>  |          <span data-ttu-id="f720d-360">**Y** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-360">**Y** 0</span></span>          |  <span data-ttu-id="f720d-361">**Z** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-361">**Z** 0</span></span>  |

    |            |     <span data-ttu-id="f720d-362">TRANSFORMATION - MISE À L’ÉCHELLE</span><span class="sxs-lookup"><span data-stu-id="f720d-362">TRANSFORM - SCALE</span></span>     |           |
    | :---------:| :-----------------------: | :--------:|
    |  <span data-ttu-id="f720d-363">**X** 1</span><span class="sxs-lookup"><span data-stu-id="f720d-363">**X** 1</span></span>   |          <span data-ttu-id="f720d-364">**Y** 1</span><span class="sxs-lookup"><span data-stu-id="f720d-364">**Y** 1</span></span>          |  <span data-ttu-id="f720d-365">**Z** 1</span><span class="sxs-lookup"><span data-stu-id="f720d-365">**Z** 1</span></span>  |

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-42.png)


## <a name="chapter-5---create-the-videocontroller-class"></a><span data-ttu-id="f720d-367">Chapitre 5 : créer la classe VideoController</span><span class="sxs-lookup"><span data-stu-id="f720d-367">Chapter 5 - Create the VideoController class</span></span>

<span data-ttu-id="f720d-368">Le **VideoController** classe héberge les deux points de terminaison vidéo permet de diffuser le contenu à partir du Service de média Azure.</span><span class="sxs-lookup"><span data-stu-id="f720d-368">The **VideoController** class hosts the two video endpoints that will be used to stream the content from the Azure Media Service.</span></span>

<span data-ttu-id="f720d-369">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="f720d-369">To create this class:</span></span>

1.  <span data-ttu-id="f720d-370">Avec le bouton droit dans le **dossier composants**, situé dans le **projet** Panneau de configuration, puis cliquez sur **créer > dossier**.</span><span class="sxs-lookup"><span data-stu-id="f720d-370">Right-click in the **Asset Folder**, located in the **Project** Panel, and click **Create > Folder**.</span></span> <span data-ttu-id="f720d-371">Nommez le dossier **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="f720d-371">Name the folder **Scripts**.</span></span>

    ![Créer la classe VideoController](images/AzureLabs-Lab6-43.png)

    ![Créer la classe VideoController](images/AzureLabs-Lab6-44.png)

2.  <span data-ttu-id="f720d-374">Double-cliquez sur le **Scripts** dossier pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="f720d-374">Double click on the **Scripts** folder to open it.</span></span>

3.  <span data-ttu-id="f720d-375">Avec le bouton droit dans le dossier, puis cliquez sur **créer > C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="f720d-375">Right-click inside the folder, then click **Create > C\# Script**.</span></span> <span data-ttu-id="f720d-376">Nommez le script **VideoController**.</span><span class="sxs-lookup"><span data-stu-id="f720d-376">Name the script **VideoController**.</span></span>

    ![Créer la classe VideoController](images/AzureLabs-Lab6-45.png)

4.  <span data-ttu-id="f720d-378">Double-cliquez sur le nouveau **VideoController** script pour l’ouvrir avec **Visual Studio 2017.**</span><span class="sxs-lookup"><span data-stu-id="f720d-378">Double click on the new **VideoController** script to open it with **Visual Studio 2017.**</span></span>

    ![Créer la classe VideoController](images/AzureLabs-Lab6-46.png)

5.  <span data-ttu-id="f720d-380">Mettre à jour les espaces de noms en haut du fichier de code comme suit :</span><span class="sxs-lookup"><span data-stu-id="f720d-380">Update the namespaces at the top of the code file as follows:</span></span>

    ```csharp
    using System.Collections;
    using UnityEngine;
    using UnityEngine.SceneManagement;
    using UnityEngine.Video;
    ```

6.  <span data-ttu-id="f720d-381">Entrez les variables suivantes dans le **VideoController** classe, ainsi que la **Awake()** méthode :</span><span class="sxs-lookup"><span data-stu-id="f720d-381">Enter the following variables in the **VideoController** class, along with the **Awake()** method:</span></span>

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

7.  <span data-ttu-id="f720d-382">Il est temps de saisir les points de terminaison de vos vidéos Azure Media Services :</span><span class="sxs-lookup"><span data-stu-id="f720d-382">Now is the time to enter the endpoints from your Azure Media Service videos:</span></span>

    1.  <span data-ttu-id="f720d-383">Le premier dans le *video1endpoint* variable.</span><span class="sxs-lookup"><span data-stu-id="f720d-383">The first into the *video1endpoint* variable.</span></span>
    
    2.  <span data-ttu-id="f720d-384">La seconde dans le *video2endpoint* variable.</span><span class="sxs-lookup"><span data-stu-id="f720d-384">The second into the *video2endpoint* variable.</span></span>

    > [!WARNING]
    > <span data-ttu-id="f720d-385">Il existe un problème connu avec à l’aide de *https* dans Unity, avec la version 2017.4.1f1.</span><span class="sxs-lookup"><span data-stu-id="f720d-385">There is a known issue with using *https* within Unity, with version 2017.4.1f1.</span></span> <span data-ttu-id="f720d-386">Si les vidéos fournissent une erreur sur play, essayez plutôt d’utiliser « http ».</span><span class="sxs-lookup"><span data-stu-id="f720d-386">If the videos provide an error on play, try using 'http' instead.</span></span>

8.  <span data-ttu-id="f720d-387">Ensuite, le **Start()** méthode doit être modifié.</span><span class="sxs-lookup"><span data-stu-id="f720d-387">Next, the **Start()** method needs to be edited.</span></span> <span data-ttu-id="f720d-388">Cette méthode est déclenchée chaque fois que l’utilisateur change de scène (basculement en conséquence de la vidéo) en examinant le bouton d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="f720d-388">This method will be triggered every time the user switches scene (consequently switching the video) by looking at the Gaze Button.</span></span>

    ```csharp
        // Use this for initialization
        void Start()
        {
            Application.runInBackground = true;
            StartCoroutine(PlayVideo());
        }
    ```

9.  <span data-ttu-id="f720d-389">Suivant le **Start()** (méthode), insérez le **PlayVideo()** *IEnumerator* (méthode), qui sera utilisé pour démarrer des vidéos en toute transparence (donc aucune interruption ne se produite).</span><span class="sxs-lookup"><span data-stu-id="f720d-389">Following the **Start()** method, insert the **PlayVideo()** *IEnumerator* method, which will be used to start videos seamlessly (so no stutter is seen).</span></span>

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

10. <span data-ttu-id="f720d-390">La dernière méthode que vous avez besoin de cette classe est la **ChangeScene()** (méthode), qui sera utilisé pour basculer entre deux séquences.</span><span class="sxs-lookup"><span data-stu-id="f720d-390">The last method you need for this class is the **ChangeScene()** method, which will be used to swap between scenes.</span></span>

    ```csharp
        public void ChangeScene()
        {
            SceneManager.LoadScene(SceneManager.GetActiveScene().name == "VideoScene1" ? "VideoScene2" : "VideoScene1");
        }
    ```

    > [!TIP] 
    > <span data-ttu-id="f720d-391">Le **ChangeScene()** méthode utilise une pratique C\# fonctionnalité appelée la *opérateur conditionnel*.</span><span class="sxs-lookup"><span data-stu-id="f720d-391">The **ChangeScene()** method uses a handy C\# feature called the *Conditional Operator*.</span></span> <span data-ttu-id="f720d-392">Ainsi, les conditions à vérifier, et puis valeurs retournées en fonction du résultat de la vérification, au sein d’une instruction unique.</span><span class="sxs-lookup"><span data-stu-id="f720d-392">This allows for conditions to be checked, and then values returned based on the outcome of the check, all within a single statement.</span></span> <span data-ttu-id="f720d-393">Suivez ce [lien en savoir plus sur l’opérateur conditionnel](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/conditional-operator).</span><span class="sxs-lookup"><span data-stu-id="f720d-393">Follow this [link to learn more about Conditional Operator](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/conditional-operator).</span></span>

11. <span data-ttu-id="f720d-394">Enregistrez vos modifications dans Visual Studio avant de retourner à Unity.</span><span class="sxs-lookup"><span data-stu-id="f720d-394">Save your changes in Visual Studio before returning to Unity.</span></span>

12. <span data-ttu-id="f720d-395">Précédent dans l’éditeur Unity, cliquez et faites glisser le **VideoController** classe [from] {.underline} le **Scripts** dossier pour le **Main Camera** de l’objet dans le  **Hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="f720d-395">Back in the Unity Editor, click and drag the **VideoController** class [from]{.underline} the **Scripts** folder to the **Main Camera** object in the **Hierarchy** Panel.</span></span>

13. <span data-ttu-id="f720d-396">Cliquez sur le **Main Camera** et examinez le **panneau Inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="f720d-396">Click on the **Main Camera** and look at the **Inspector Panel**.</span></span> <span data-ttu-id="f720d-397">Vous remarquerez que dans le composant de Script qui vient d’être ajouté, est un champ avec une valeur vide.</span><span class="sxs-lookup"><span data-stu-id="f720d-397">You will notice that within the newly added Script component, there is a field with an empty value.</span></span> <span data-ttu-id="f720d-398">Il s’agit d’un champ de référence, qui cible les variables publiques dans votre code.</span><span class="sxs-lookup"><span data-stu-id="f720d-398">This is a reference field, which targets the public variables within your code.</span></span>

14. <span data-ttu-id="f720d-399">Faites glisser le **InsideOutSphere** à partir de l’objet le **hiérarchie panneau** à la **sphère** emplacement, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f720d-399">Drag the **InsideOutSphere** object from the **Hierarchy Panel** to the **Sphere** slot, as shown in the image below.</span></span>

    <span data-ttu-id="f720d-400">![Créer la classe VideoController](images/AzureLabs-Lab6-47.png)
    ![créer la classe VideoController](images/AzureLabs-Lab6-48.png)</span><span class="sxs-lookup"><span data-stu-id="f720d-400">![Create the VideoController class](images/AzureLabs-Lab6-47.png)
![Create the VideoController class](images/AzureLabs-Lab6-48.png)</span></span>

## <a name="chapter-6---create-the-gaze-class"></a><span data-ttu-id="f720d-401">Chapitre 6 : créer la classe du pointage de regard</span><span class="sxs-lookup"><span data-stu-id="f720d-401">Chapter 6 - Create the Gaze class</span></span>

<span data-ttu-id="f720d-402">Cette classe est chargée pour la création d’un **Raycast** que beprojected transfère à partir de la **Main Camera**, pour détecter quel objet consulte l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f720d-402">This class is responsible for creating a **Raycast** that will beprojected forward from the **Main Camera**, to detect which object the user is looking at.</span></span> <span data-ttu-id="f720d-403">Dans ce cas, le **Raycast** devra identifier si l’utilisateur consulte la **GazeButton** de l’objet dans la scène et déclencher un comportement.</span><span class="sxs-lookup"><span data-stu-id="f720d-403">In this case, the **Raycast** will need to identify if the user is looking at the **GazeButton** object in the scene and trigger a behavior.</span></span>

<span data-ttu-id="f720d-404">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="f720d-404">To create this Class:</span></span>

1.  <span data-ttu-id="f720d-405">Accédez à la **Scripts** dossier que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="f720d-405">Go to the **Scripts** folder you created previously.</span></span>

2.  <span data-ttu-id="f720d-406">Avec le bouton droit dans le **projet** panneau, \**créer* \*C\# Script\*\*.</span><span class="sxs-lookup"><span data-stu-id="f720d-406">Right-click in the **Project** Panel, \**Create* \*C\# Script\*\*.</span></span> <span data-ttu-id="f720d-407">Nommez le script **les regards**.</span><span class="sxs-lookup"><span data-stu-id="f720d-407">Name the script **Gaze**.</span></span>

3.  <span data-ttu-id="f720d-408">Double-cliquez sur le nouveau ***les regards*** script pour l’ouvrir avec **Visual Studio 2017.**</span><span class="sxs-lookup"><span data-stu-id="f720d-408">Double click on the new ***Gaze*** script to open it with **Visual Studio 2017.**</span></span>

4.  <span data-ttu-id="f720d-409">Vérifiez que l’espace de noms suivant s’affiche en haut du script et supprimez tous les autres :</span><span class="sxs-lookup"><span data-stu-id="f720d-409">Ensure the following namespace is at the top of the script, and remove any others:</span></span>

    ```csharp
    using UnityEngine;
    ```

5.  <span data-ttu-id="f720d-410">Puis ajoutez les variables suivantes à l’intérieur de la **les regards** classe :</span><span class="sxs-lookup"><span data-stu-id="f720d-410">Then add the following variables inside the **Gaze** class:</span></span>

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

6.  <span data-ttu-id="f720d-411">Code pour le **Awake()** et **Start()** méthodes doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="f720d-411">Code for the **Awake()** and **Start()** methods now needs to be added.</span></span>

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

7.  <span data-ttu-id="f720d-412">Ajoutez le code suivant dans le **Update()** méthode projeter une Raycast et de détecter le positionnement de la cible :</span><span class="sxs-lookup"><span data-stu-id="f720d-412">Add the following code in the **Update()** method to project a Raycast and detect the target hit:</span></span>

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

8.  <span data-ttu-id="f720d-413">Enregistrez vos modifications dans Visual Studio avant de retourner à Unity.</span><span class="sxs-lookup"><span data-stu-id="f720d-413">Save your changes in Visual Studio before returning to Unity.</span></span>

9.  <span data-ttu-id="f720d-414">Cliquez et faites glisser le **les regards** classe à partir du dossier Scripts à l’objet Main Camera dans le **hiérarchie** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="f720d-414">Click and drag the **Gaze** class from the Scripts folder to the Main Camera object in the **Hierarchy** Panel.</span></span>

## <a name="chapter-7---setup-the-two-unity-scenes"></a><span data-ttu-id="f720d-415">Chapitre 7 - le programme d’installation les deux Unity scènes</span><span class="sxs-lookup"><span data-stu-id="f720d-415">Chapter 7 - Setup the two Unity Scenes</span></span>

<span data-ttu-id="f720d-416">L’objectif de ce chapitre consiste à configurer les deux scènes, chacune hébergeant une vidéo au flux.</span><span class="sxs-lookup"><span data-stu-id="f720d-416">The purpose of this Chapter is to setup the two scenes, each hosting a video to stream.</span></span> <span data-ttu-id="f720d-417">Vous allez dupliquer la scène, vous avez déjà créé, afin qu’est inutile de l’ajouter à nouveau, bien que vous allez ensuite modifier la nouvelle scène, afin que le *GazeButton* objet est dans un emplacement différent et a une apparence différente.</span><span class="sxs-lookup"><span data-stu-id="f720d-417">You will duplicate the scene you have already created, so that you do not need to set it up again, though you will then edit the new scene, so that the *GazeButton* object is in a different location and has a different appearance.</span></span> <span data-ttu-id="f720d-418">Il s’agit de montrer comment changer entre les scènes.</span><span class="sxs-lookup"><span data-stu-id="f720d-418">This is to show how to change between scenes.</span></span>

1.  <span data-ttu-id="f720d-419">Cela en accédant à **fichier > Enregistrer la scène en tant que...** . Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f720d-419">Do this by going to **File > Save Scene as...**. A save window will appear.</span></span> <span data-ttu-id="f720d-420">Cliquez sur le **nouveau dossier** bouton.</span><span class="sxs-lookup"><span data-stu-id="f720d-420">Click the **New folder** button.</span></span>

    ![Chapitre 7 - le programme d’installation les deux Unity scènes](images/AzureLabs-Lab6-49.png)

2.  <span data-ttu-id="f720d-422">Nommez le dossier **scènes**.</span><span class="sxs-lookup"><span data-stu-id="f720d-422">Name the folder **Scenes**.</span></span>

3.  <span data-ttu-id="f720d-423">Le **enregistrer la scène** fenêtre sera toujours ouverte.</span><span class="sxs-lookup"><span data-stu-id="f720d-423">The **Save Scene** window will still be open.</span></span> <span data-ttu-id="f720d-424">Ouvrez votre nouvellement créé **scènes** dossier.</span><span class="sxs-lookup"><span data-stu-id="f720d-424">Open your newly created **Scenes** folder.</span></span>

4.  <span data-ttu-id="f720d-425">Dans le **nom de fichier :** champ de texte, tapez **VideoScene1**, puis appuyez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f720d-425">In the **File name:** text field, type **VideoScene1**, then press **Save**.</span></span>

5.  <span data-ttu-id="f720d-426">Dans Unity, ouvrez votre **scènes** dossier et cliquez sur votre **VideoScene1** fichier.</span><span class="sxs-lookup"><span data-stu-id="f720d-426">Back in Unity, open your **Scenes** folder, and left-click your **VideoScene1** file.</span></span> <span data-ttu-id="f720d-427">Utiliser le clavier, appuyez sur **Ctrl + D** vous allez dupliquer cette scène</span><span class="sxs-lookup"><span data-stu-id="f720d-427">Use your keyboard, and press **Ctrl + D** you will duplicate that scene</span></span>

    > [!TIP]
    > <span data-ttu-id="f720d-428">Le **dupliquer** commande peut également être effectuée en accédant à **Modifier > Dupliquer**.</span><span class="sxs-lookup"><span data-stu-id="f720d-428">The **Duplicate** command can also be performed by navigating to **Edit > Duplicate**.</span></span>

6.  <span data-ttu-id="f720d-429">Unity sera automatiquement incrémente le nombre de noms de scène, mais vérifier tout de même, pour vous assurer qu’il correspond au code inséré précédemment.</span><span class="sxs-lookup"><span data-stu-id="f720d-429">Unity will automatically increment the scene names number, but check it anyway, to ensure it matches the previously inserted code.</span></span>

    >  <span data-ttu-id="f720d-430">Vous devez avoir **VideoScene1** et **VideoScene2**.</span><span class="sxs-lookup"><span data-stu-id="f720d-430">You should have **VideoScene1** and **VideoScene2**.</span></span>

7.  <span data-ttu-id="f720d-431">Avec vos deux scènes, accédez à **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="f720d-431">With your two scenes, go to **File > Build Settings**.</span></span> <span data-ttu-id="f720d-432">Avec le **paramètres de Build** fenêtre ouverte, faites glisser votre arrière-plan pour le **scènes dans la Build** section.</span><span class="sxs-lookup"><span data-stu-id="f720d-432">With the **Build Settings** window open, drag your scenes to the **Scenes in Build** section.</span></span>

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-50.png)

    > [!TIP] 
    > <span data-ttu-id="f720d-434">Vous pouvez sélectionner les deux de vos scènes à partir de votre **scènes** dossier via contenant le **Ctrl** bouton, puis clic gauche chaque scène et enfin, faites glisser les deux sur.</span><span class="sxs-lookup"><span data-stu-id="f720d-434">You can select both of your scenes from your **Scenes** folder through holding the **Ctrl** button, and then left-clicking each scene, and finally drag both across.</span></span>

8.  <span data-ttu-id="f720d-435">Fermer le **paramètres de Build** fenêtre et double-clic sur **VideoScene2**.</span><span class="sxs-lookup"><span data-stu-id="f720d-435">Close the **Build Settings** window, and double click on **VideoScene2**.</span></span>

9.  <span data-ttu-id="f720d-436">Avec la seconde séquence ouverte, cliquez sur le **GazeButton** objet enfant de la **InsideOutSphere**et définissez sa transformation comme suit :</span><span class="sxs-lookup"><span data-stu-id="f720d-436">With the second scene open, click on the **GazeButton** child object of the **InsideOutSphere**, and set its Transform as follows:</span></span>

    |            |    <span data-ttu-id="f720d-437">TRANSFORMATION - POSITION</span><span class="sxs-lookup"><span data-stu-id="f720d-437">TRANSFORM - POSITION</span></span>   |           |
    | :---------:| :-----------------------: | :--------:|
    |   <span data-ttu-id="f720d-438">**X** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-438">**X** 0</span></span>  |         <span data-ttu-id="f720d-439">**Y** 1.3</span><span class="sxs-lookup"><span data-stu-id="f720d-439">**Y** 1.3</span></span>         | <span data-ttu-id="f720d-440">**Z** 3.6</span><span class="sxs-lookup"><span data-stu-id="f720d-440">**Z** 3.6</span></span> |

    |            |    <span data-ttu-id="f720d-441">TRANSFORMATION - ROTATION</span><span class="sxs-lookup"><span data-stu-id="f720d-441">TRANSFORM - ROTATION</span></span>   |           |
    | :---------:| :-----------------------: | :--------:|
    |   <span data-ttu-id="f720d-442">**X** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-442">**X** 0</span></span>  |          <span data-ttu-id="f720d-443">**Y** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-443">**Y** 0</span></span>          |  <span data-ttu-id="f720d-444">**Z** 0</span><span class="sxs-lookup"><span data-stu-id="f720d-444">**Z** 0</span></span>  |

    |            |     <span data-ttu-id="f720d-445">TRANSFORMATION - MISE À L’ÉCHELLE</span><span class="sxs-lookup"><span data-stu-id="f720d-445">TRANSFORM - SCALE</span></span>     |           |
    | :---------:| :-----------------------: | :--------:|
    |  <span data-ttu-id="f720d-446">**X** 1</span><span class="sxs-lookup"><span data-stu-id="f720d-446">**X** 1</span></span>   |          <span data-ttu-id="f720d-447">**Y** 1</span><span class="sxs-lookup"><span data-stu-id="f720d-447">**Y** 1</span></span>          |  <span data-ttu-id="f720d-448">**Z** 1</span><span class="sxs-lookup"><span data-stu-id="f720d-448">**Z** 1</span></span>  |

10. <span data-ttu-id="f720d-449">Avec le **GazeButton** enfants étant toujours sélectionnée, regardez à la **inspecteur** et à la **filtre Mesh**.</span><span class="sxs-lookup"><span data-stu-id="f720d-449">With the **GazeButton** child still selected, look at the **Inspector** and at the **Mesh Filter**.</span></span> <span data-ttu-id="f720d-450">Cliquez sur la cible peu en regard du **Mesh** champ de référence :</span><span class="sxs-lookup"><span data-stu-id="f720d-450">Click the little target next to the **Mesh** reference field:</span></span>

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-51.png)

11. <span data-ttu-id="f720d-452">Un **sélectionnez maillage** fenêtre contextuelle s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f720d-452">A **Select Mesh** popup window will appear.</span></span> <span data-ttu-id="f720d-453">Double-cliquez sur le **Cube** de maillage dans la liste des **ressources**.</span><span class="sxs-lookup"><span data-stu-id="f720d-453">Double click the **Cube** mesh from the list of **Assets**.</span></span>

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-52.png)

12. <span data-ttu-id="f720d-455">Le **filtre Mesh** met à jour et être maintenant un **Cube**.</span><span class="sxs-lookup"><span data-stu-id="f720d-455">The **Mesh Filter** will update, and now be a **Cube**.</span></span> <span data-ttu-id="f720d-456">Maintenant, cliquez sur le **ENGRENAGE** icône située à côté **sphère Collider** et cliquez sur **supprimer un composant**, permet de supprimer le collider de cet objet.</span><span class="sxs-lookup"><span data-stu-id="f720d-456">Now, click the **Gear** icon next to **Sphere Collider** and click **Remove Component**, to delete the collider from this object.</span></span>

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-53.png)

13. <span data-ttu-id="f720d-458">Avec le **GazeButton** toujours sélectionnée, cliquez sur le **ajouter un composant** bouton en bas de la **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="f720d-458">With the **GazeButton** still selected, click the **Add Component** button at the bottom of the **Inspector**.</span></span> <span data-ttu-id="f720d-459">Dans le champ de recherche, tapez **boîte**, et **Collider de la boîte de** sera l’option--cliquer ici, pour ajouter un **boîte Collider** à votre **GazeButton** objet .</span><span class="sxs-lookup"><span data-stu-id="f720d-459">In the search field, type **box**, and **Box Collider** will be an option -- click that, to add a **Box Collider** to your **GazeButton** object.</span></span>

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-54.png)

14. <span data-ttu-id="f720d-461">Le **GazeButton** est maintenant mis à jour partiellement, pour un aspect différent, toutefois, vous allez maintenant créer un nouveau **matériau**, afin qu’il est complètement différente et est plus facile à reconnaître qu’un autre objet, à la objet dans la première séquence.</span><span class="sxs-lookup"><span data-stu-id="f720d-461">The **GazeButton** is now partially updated, to look different, however, you will now create a new **Material**, so that it looks completely different, and is easier to recognize as a different object, than the object in the first scene.</span></span>

15. <span data-ttu-id="f720d-462">Accédez à votre **matériaux** dossier, en respectant le **panneau projet**.</span><span class="sxs-lookup"><span data-stu-id="f720d-462">Navigate to your **Materials** folder, within the **Project Panel**.</span></span> <span data-ttu-id="f720d-463">Dupliquer la **ButtonMaterial** matériau (appuyez sur **Ctrl** + **D** sur le clavier, ou cliquez sur le **matériau**, puis à partir de la **modifier** option de menu, sélectionnez fichier **dupliquer**).</span><span class="sxs-lookup"><span data-stu-id="f720d-463">Duplicate the **ButtonMaterial** Material (press **Ctrl** + **D** on the keyboard, or left-click the **Material**, then from the **Edit** file menu option, select **Duplicate**).</span></span>

    <span data-ttu-id="f720d-464">![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-55.png)
    ![chapitre 7 : configurer les deux scènes Unity](images/AzureLabs-Lab6-56.png)</span><span class="sxs-lookup"><span data-stu-id="f720d-464">![Chapter 7 -- Setup the two Unity Scenes](images/AzureLabs-Lab6-55.png)
![Chapter 7 -- Setup the two Unity Scenes](images/AzureLabs-Lab6-56.png)</span></span>

16. <span data-ttu-id="f720d-465">Sélectionnez la nouvelle **ButtonMaterial** matériau (ici nommé **ButtonMaterial 1**) et dans le **inspecteur**, cliquez sur le **Albedo** couleur fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f720d-465">Select the new **ButtonMaterial** Material (here named **ButtonMaterial 1**), and within the **Inspector**, click the **Albedo** color window.</span></span> <span data-ttu-id="f720d-466">Une fenêtre contextuelle s’affiche, dans laquelle vous pouvez sélectionner une autre couleur (choisissez celle que vous préférez), puis fermez la fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="f720d-466">A popup will appear, where you can select another color (choose whichever you like), then close the popup.</span></span> <span data-ttu-id="f720d-467">Le matériel d’être sa propre instance et l’autre à l’original.</span><span class="sxs-lookup"><span data-stu-id="f720d-467">The Material will be its own instance, and different to the original.</span></span>

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-57.png)

17. <span data-ttu-id="f720d-469">Faites glisser la nouvelle **matériau** sur le **GazeButton** enfant, désormais entièrement mis à jour son apparence, afin qu’il soit facilement reconnaissable à partir du premier bouton de scènes.</span><span class="sxs-lookup"><span data-stu-id="f720d-469">Drag the new **Material** onto the **GazeButton** child, to now completely update its look, so that it is easily distinguishable from the first scenes button.</span></span>

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-58.png)

18. <span data-ttu-id="f720d-471">À ce stade, vous pouvez tester le projet dans l’éditeur avant de générer le projet UWP.</span><span class="sxs-lookup"><span data-stu-id="f720d-471">At this point you can test the project in the Editor before building the UWP project.</span></span>

    -  <span data-ttu-id="f720d-472">Appuyez sur la **lire** situé dans le **éditeur** et porter votre casque.</span><span class="sxs-lookup"><span data-stu-id="f720d-472">Press the **Play** button in the **Editor** and wear your headset.</span></span>

        ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-59.png)

19. <span data-ttu-id="f720d-474">Examinez les deux **GazeButton** objets pour basculer entre la première et deuxième vidéo.</span><span class="sxs-lookup"><span data-stu-id="f720d-474">Look at the two **GazeButton** objects to switch between the first and second video.</span></span>

## <a name="chapter-8---build-the-uwp-solution"></a><span data-ttu-id="f720d-475">Chapitre 8 - générer la Solution UWP</span><span class="sxs-lookup"><span data-stu-id="f720d-475">Chapter 8 - Build the UWP Solution</span></span>

<span data-ttu-id="f720d-476">Une fois que vous vous assurez que l’éditeur n’a aucune erreur, vous êtes prêt à générer.</span><span class="sxs-lookup"><span data-stu-id="f720d-476">Once you have ensured that the editor has no errors, you are ready to Build.</span></span>

<span data-ttu-id="f720d-477">Pour générer :</span><span class="sxs-lookup"><span data-stu-id="f720d-477">To Build:</span></span>

1.  <span data-ttu-id="f720d-478">Enregistrer la scène actuelle en cliquant sur **fichier > Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f720d-478">Save the current scene by clicking on **File > Save**.</span></span>

2.  <span data-ttu-id="f720d-479">Cochez la case appelée **Unity C\# projets** (Ceci est important, car il vous permettra de modifier les classes après de la build est terminée).</span><span class="sxs-lookup"><span data-stu-id="f720d-479">Check the box called **Unity C\# Projects** (this is important because it will allow you to edit the classes after build is completed).</span></span>

3.  <span data-ttu-id="f720d-480">Accédez à **fichier > Paramètres de Build**, cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="f720d-480">Go to **File > Build Settings**, click on **Build**.</span></span>

4.  <span data-ttu-id="f720d-481">Vous êtes invité à sélectionner le dossier où vous souhaitez buildthe Solution.</span><span class="sxs-lookup"><span data-stu-id="f720d-481">You will be prompted to select the folder where you want to buildthe Solution.</span></span>

5.  <span data-ttu-id="f720d-482">Créer un **génère** dossier et dans ce dossier, créez un autre dossier avec un nom approprié de votre choix.</span><span class="sxs-lookup"><span data-stu-id="f720d-482">Create a **BUILDS** folder and within that folder create another folder with an appropriate name of your choice.</span></span>

6.  <span data-ttu-id="f720d-483">Cliquez sur votre nouveau dossier, puis **sélectionner le dossier**, par conséquent, pour choisir ce dossier, pour commencer la génération à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="f720d-483">Click your new folder and then click **Select Folder**, so to choose that folder, to begin the build at that location.</span></span>

    <span data-ttu-id="f720d-484">![Chapitre 8--Générer la Solution UWP](images/AzureLabs-Lab6-60.png)
    ![chapitre 8--générer la Solution UWP](images/AzureLabs-Lab6-61.png)</span><span class="sxs-lookup"><span data-stu-id="f720d-484">![Chapter 8 -- Build the UWP Solution](images/AzureLabs-Lab6-60.png)
![Chapter 8 -- Build the UWP Solution](images/AzureLabs-Lab6-61.png)</span></span>

7.  <span data-ttu-id="f720d-485">Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un **Explorateur de fichiers** fenêtre à l’emplacement de votre build.</span><span class="sxs-lookup"><span data-stu-id="f720d-485">Once Unity has finished building (it might take some time), it will open a **File Explorer** window at the location of your build.</span></span>

## <a name="chapter-9---deploy-on-local-machine"></a><span data-ttu-id="f720d-486">Chapitre 9 - déployer sur l’ordinateur Local</span><span class="sxs-lookup"><span data-stu-id="f720d-486">Chapter 9 - Deploy on Local Machine</span></span>

<span data-ttu-id="f720d-487">Une fois la build terminée, un **Explorateur de fichiers** fenêtre s’affiche à l’emplacement de votre build.</span><span class="sxs-lookup"><span data-stu-id="f720d-487">Once the build has been completed, a **File Explorer** window will appear at the location of your build.</span></span> <span data-ttu-id="f720d-488">Ouvrez le dossier que vous avez nommé et intégrées à, puis double-cliquez sur le fichier solution (.sln) dans ce dossier, pour ouvrir votre solution avec Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f720d-488">Open the Folder you named and built to, then double click on the solution (.sln) file within that folder, to open your solution with Visual Studio 2017.</span></span>

<span data-ttu-id="f720d-489">La seule chose à faire est de déployer votre application sur votre ordinateur (ou *ordinateur Local*).</span><span class="sxs-lookup"><span data-stu-id="f720d-489">The only thing left to do is deploy your app to your computer (or *Local Machine*).</span></span>

<span data-ttu-id="f720d-490">Pour déployer sur l’ordinateur Local :</span><span class="sxs-lookup"><span data-stu-id="f720d-490">To deploy to Local Machine:</span></span>

1.  <span data-ttu-id="f720d-491">Dans **Visual Studio 2017**, ouvrez le fichier solution qui vient d’être créé.</span><span class="sxs-lookup"><span data-stu-id="f720d-491">In **Visual Studio 2017**, open the solution file that has just been created.</span></span>

2.  <span data-ttu-id="f720d-492">Dans le **plateforme de Solution**, sélectionnez **x86, Local Machine**.</span><span class="sxs-lookup"><span data-stu-id="f720d-492">In the **Solution Platform**, select **x86, Local Machine**.</span></span>

3.  <span data-ttu-id="f720d-493">Dans le **Configuration de la Solution** sélectionnez **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="f720d-493">In the **Solution Configuration** select **Debug**.</span></span>

    ![Chapitre 9--Déployer sur l’ordinateur Local](images/AzureLabs-Lab6-62.png)

4.  <span data-ttu-id="f720d-495">Maintenant, vous devrez restaurer tous les packages à votre solution.</span><span class="sxs-lookup"><span data-stu-id="f720d-495">You will now need to restore any packages to your solution.</span></span> <span data-ttu-id="f720d-496">Avec le bouton droit sur votre **Solution**, puis cliquez sur **restaurer les Packages NuGet pour la Solution...**</span><span class="sxs-lookup"><span data-stu-id="f720d-496">Right-click on your **Solution**, and click **Restore NuGet Packages for Solution...**</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f720d-497">Pour cela, car les packages qui Unity généré doivent être ciblés pour fonctionner avec vos références de machines locales.</span><span class="sxs-lookup"><span data-stu-id="f720d-497">This is done because the packages which Unity built need to be targeted to work with your local machines references.</span></span>

5.  <span data-ttu-id="f720d-498">Accédez à **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f720d-498">Go to **Build menu** and click on **Deploy Solution** to sideload the application to your machine.</span></span> <span data-ttu-id="f720d-499">Visual Studio tout d’abord créer et déployer votre application.</span><span class="sxs-lookup"><span data-stu-id="f720d-499">Visual Studio will first build and then deploy your application.</span></span>

6.  <span data-ttu-id="f720d-500">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancée.</span><span class="sxs-lookup"><span data-stu-id="f720d-500">Your App should now appear in the list of installed apps, ready to be launched.</span></span>

    ![Chapitre 9--Déployer sur l’ordinateur Local](images/AzureLabs-Lab6-63.png)

<span data-ttu-id="f720d-502">Lorsque vous exécutez l’application de réalité mixte, vous allez vous se trouver dans le **InsideOutSphere** modèle que vous avez utilisées au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="f720d-502">When you run the Mixed Reality application, you will you be within the **InsideOutSphere** model which you used within your app.</span></span> <span data-ttu-id="f720d-503">Ce domaine sera où la vidéo est diffusée, en fournissant une vue à 360 degrés, de la vidéo entrante (qui a été filmée pour ce type de point de vue).</span><span class="sxs-lookup"><span data-stu-id="f720d-503">This sphere will be where the video will be streamed to, providing a 360-degree view, of the incoming video (which was filmed for this kind of perspective).</span></span> <span data-ttu-id="f720d-504">Ne soyez pas surpris que si la vidéo prend quelques secondes pour charger, votre application est soumis à vitesse de votre Internet disponible, comme la vidéo doit être extraite, puis téléchargées, par conséquent, pour diffuser en continu dans votre application.</span><span class="sxs-lookup"><span data-stu-id="f720d-504">Do not be surprised if the video takes a couple of seconds to load, your app is subject to your available Internet speed, as the video needs to be fetched and then downloaded, so to stream into your app.</span></span>
<span data-ttu-id="f720d-505">Lorsque vous êtes prêt, modifier l’arrière-plan et ouvrez votre deuxième vidéo, par gazing à la sphère rouge !</span><span class="sxs-lookup"><span data-stu-id="f720d-505">When you are ready, change scenes and open your second video, by gazing at the red sphere!</span></span> <span data-ttu-id="f720d-506">Puis n’hésitez pas à revenir en arrière à l’aide du cube bleu dans la seconde séquence !</span><span class="sxs-lookup"><span data-stu-id="f720d-506">Then feel free to go back, using the blue cube in the second scene!</span></span>

## <a name="your-finished-azure-media-service-application"></a><span data-ttu-id="f720d-507">Votre application Azure Media Services terminée</span><span class="sxs-lookup"><span data-stu-id="f720d-507">Your finished Azure Media Service application</span></span>
 
<span data-ttu-id="f720d-508">Félicitations, vous avez créé une application de réalité mixte qui tire parti du Service de média Azure pour diffuser des 360 vidéos.</span><span class="sxs-lookup"><span data-stu-id="f720d-508">Congratulations, you built a mixed reality app that leverages the Azure Media Service to stream 360 videos.</span></span>

![résultat de laboratoire](images/AzureLabs-Lab6-00.png)

![résultat de laboratoire](images/AzureLabs-Lab6-01.png)

## <a name="bonus-exercises"></a><span data-ttu-id="f720d-511">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="f720d-511">Bonus Exercises</span></span>

<span data-ttu-id="f720d-512">**Exercice 1**</span><span class="sxs-lookup"><span data-stu-id="f720d-512">**Exercise 1**</span></span>

<span data-ttu-id="f720d-513">Il est tout à fait possible d’utiliser uniquement une scène unique pour modifier des vidéos au sein de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f720d-513">It is entirely possible to only use a single scene to change videos within this tutorial.</span></span> <span data-ttu-id="f720d-514">Faire des essais avec votre application et la convertir en une scène unique !</span><span class="sxs-lookup"><span data-stu-id="f720d-514">Experiment with your application and make it into a single scene!</span></span> <span data-ttu-id="f720d-515">Peut-être même ajouter une autre vidéo à la combinaison.</span><span class="sxs-lookup"><span data-stu-id="f720d-515">Perhaps even add another video to the mix.</span></span>

<span data-ttu-id="f720d-516">**Exercice 2**</span><span class="sxs-lookup"><span data-stu-id="f720d-516">**Exercise 2**</span></span>

<span data-ttu-id="f720d-517">Faire des essais avec Azure et Unity et tentez de mettre en œuvre la possibilité pour l’application sélectionner automatiquement une vidéo avec une taille de fichier différent, en fonction du niveau d’une connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="f720d-517">Experiment with Azure and Unity, and attempt to implement the ability for the app to automatically select a video with a different file size, depending on the strength of an Internet connection.</span></span>


