---
title: MR et 302 Azure - vision par ordinateur
description: Terminer ce cours pour apprendre à reconnaître le contenu visuel au sein d’une image fournie, à l’aide de la vision par ordinateur de Azure dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, vision par ordinateur, hololens, immersives, vr
ms.openlocfilehash: 9d5288904dd6cae08a995ae40a31b00fea655776
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593382"
---
>[!NOTE]
><span data-ttu-id="7de65-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="7de65-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="7de65-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="7de65-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="7de65-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="7de65-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="7de65-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7de65-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="7de65-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="7de65-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="7de65-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="7de65-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-and-azure-302-computer-vision"></a><span data-ttu-id="7de65-110">MR et Azure 302 : Vision par ordinateur</span><span class="sxs-lookup"><span data-stu-id="7de65-110">MR and Azure 302: Computer vision</span></span>

<span data-ttu-id="7de65-111">Dans ce cours, vous allez apprendre à reconnaître le contenu visuel au sein d’une image fournie, à l’aide des fonctionnalités de vision par ordinateur de Azure dans une application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="7de65-111">In this course, you will learn how to recognize visual content within a provided image, using Azure Computer Vision capabilities in a mixed reality application.</span></span>

<span data-ttu-id="7de65-112">Résultats de la reconnaissance seront affichera sous forme de balises descriptives.</span><span class="sxs-lookup"><span data-stu-id="7de65-112">Recognition results will be displayed as descriptive tags.</span></span> <span data-ttu-id="7de65-113">Vous pouvez utiliser ce service sans avoir à former un modèle d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="7de65-113">You can use this service without needing to train a machine learning model.</span></span> <span data-ttu-id="7de65-114">Si votre implémentation requiert l’apprentissage d’un modèle d’apprentissage automatique, consultez [MR et Azure 302b](mr-azure-302b.md).</span><span class="sxs-lookup"><span data-stu-id="7de65-114">If your implementation requires training a machine learning model, see [MR and Azure 302b](mr-azure-302b.md).</span></span>

![résultat de laboratoire](images/AzureLabs-Lab2-000.png)

<span data-ttu-id="7de65-116">La vision par ordinateur de Microsoft est un ensemble d’API conçues pour offrir aux développeurs un traitement d’image et l’analyse (avec retour d’informations), à l’aide des algorithmes avancés, tout à partir du cloud.</span><span class="sxs-lookup"><span data-stu-id="7de65-116">The Microsoft Computer Vision is a set of APIs designed to provide developers with image processing and analysis (with return information), using advanced algorithms, all from the cloud.</span></span> <span data-ttu-id="7de65-117">Les développeurs charger une image ou une URL de l’image et les algorithmes d’API de vision par ordinateur Microsoft analyser le contenu visuel, en fonction des entrées choisies l’utilisateur, ce qui peut retourner ensuite des informations, y compris, identifiant le type et la qualité d’une image, détecter les visages humains ( retour de leurs coordonnées) et de marquage, ou classer des images.</span><span class="sxs-lookup"><span data-stu-id="7de65-117">Developers upload an image or image URL, and the Microsoft Computer Vision API algorithms analyze the visual content, based upon inputs chosen the user, which then can return information, including, identifying the type and quality of an image, detect human faces (returning their coordinates), and tagging, or categorizing images.</span></span> <span data-ttu-id="7de65-118">Pour plus d’informations, visitez le [page de l’API de vision par ordinateur Azure](https://azure.microsoft.com/services/cognitive-services/computer-vision/).</span><span class="sxs-lookup"><span data-stu-id="7de65-118">For more information, visit the [Azure Computer Vision API page](https://azure.microsoft.com/services/cognitive-services/computer-vision/).</span></span>

<span data-ttu-id="7de65-119">Avoir terminé ce cours, vous aurez une réalité mixte application HoloLens, qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7de65-119">Having completed this course, you will have a mixed reality HoloLens application, which will be able to do the following:</span></span>

1.  <span data-ttu-id="7de65-120">À l’aide de l’action d’appuyer, l’appareil photo de l’HoloLens capture une image.</span><span class="sxs-lookup"><span data-stu-id="7de65-120">Using the Tap gesture, the camera of the HoloLens will capture an image.</span></span>
2.  <span data-ttu-id="7de65-121">L’image sera envoyée au Service de API vision par ordinateur de Azure.</span><span class="sxs-lookup"><span data-stu-id="7de65-121">The image will be sent to the Azure Computer Vision API Service.</span></span> 
3.  <span data-ttu-id="7de65-122">Les objets reconnus seront afficheront dans un groupe de l’interface utilisateur simple positionné dans la scène Unity.</span><span class="sxs-lookup"><span data-stu-id="7de65-122">The objects recognized will be listed in a simple UI group positioned in the Unity Scene.</span></span>

<span data-ttu-id="7de65-123">Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception.</span><span class="sxs-lookup"><span data-stu-id="7de65-123">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="7de65-124">Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="7de65-124">This course is designed to teach you how to integrate an Azure Service with your Unity project.</span></span> <span data-ttu-id="7de65-125">Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="7de65-125">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

## <a name="device-support"></a><span data-ttu-id="7de65-126">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="7de65-126">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="7de65-127">Cours</span><span class="sxs-lookup"><span data-stu-id="7de65-127">Course</span></span></th><th style="width:150px"> <span data-ttu-id="7de65-128"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="7de65-128"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="7de65-129"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="7de65-129"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="7de65-130">MR et Azure 302 : Vision par ordinateur</span><span class="sxs-lookup"><span data-stu-id="7de65-130">MR and Azure 302: Computer vision</span></span></td><td style="text-align: center;"> <span data-ttu-id="7de65-131">✔️</span><span class="sxs-lookup"><span data-stu-id="7de65-131">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="7de65-132">✔️</span><span class="sxs-lookup"><span data-stu-id="7de65-132">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="7de65-133">Si ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques Windows Mixed Reality IMMERSIFS (VR).</span><span class="sxs-lookup"><span data-stu-id="7de65-133">While this course primarily focuses on HoloLens, you can also apply what you learn in this course to Windows Mixed Reality immersive (VR) headsets.</span></span> <span data-ttu-id="7de65-134">Étant donné que des casques IMMERSIFS (VR) ne sont pas accessibles caméras, vous devez une caméra externe connectée à votre PC.</span><span class="sxs-lookup"><span data-stu-id="7de65-134">Because immersive (VR) headsets do not have accessible cameras, you will need an external camera connected to your PC.</span></span> <span data-ttu-id="7de65-135">Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge des casques IMMERSIFS (VR).</span><span class="sxs-lookup"><span data-stu-id="7de65-135">As you follow along with the course, you will see notes on any changes you might need to employ to support immersive (VR) headsets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7de65-136">Prérequis</span><span class="sxs-lookup"><span data-stu-id="7de65-136">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="7de65-137">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="7de65-137">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="7de65-138">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="7de65-138">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="7de65-139">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous .</span><span class="sxs-lookup"><span data-stu-id="7de65-139">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="7de65-140">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="7de65-140">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="7de65-141">Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)</span><span class="sxs-lookup"><span data-stu-id="7de65-141">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="7de65-142">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="7de65-142">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="7de65-143">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="7de65-143">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="7de65-144">Unity 2017.4</span><span class="sxs-lookup"><span data-stu-id="7de65-144">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="7de65-145">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7de65-145">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="7de65-146">Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="7de65-146">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="7de65-147">Un appareil photo connecté à votre PC (pour le développement de casque immersives)</span><span class="sxs-lookup"><span data-stu-id="7de65-147">A camera connected to your PC (for immersive headset development)</span></span>
- <span data-ttu-id="7de65-148">Accès à Internet pour le programme d’installation Azure et l’extraction de l’API vision par ordinateur</span><span class="sxs-lookup"><span data-stu-id="7de65-148">Internet access for Azure setup and Computer Vision API retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="7de65-149">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7de65-149">Before you start</span></span>

1.  <span data-ttu-id="7de65-150">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="7de65-150">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="7de65-151">Configurer et tester votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="7de65-151">Set up and test your HoloLens.</span></span> <span data-ttu-id="7de65-152">Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="7de65-152">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span> 
3.  <span data-ttu-id="7de65-153">Il est judicieux d’effectuer l’étalonnage et le réglage de capteur lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="7de65-153">It is a good idea to perform Calibration and Sensor Tuning when beginning developing a new HoloLens App (sometimes it can help to perform those tasks for each user).</span></span> 

<span data-ttu-id="7de65-154">Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).</span><span class="sxs-lookup"><span data-stu-id="7de65-154">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens).</span></span>

<span data-ttu-id="7de65-155">Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="7de65-155">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

## <a name="chapter-1--the-azure-portal"></a><span data-ttu-id="7de65-156">Chapitre 1 – le portail Azure</span><span class="sxs-lookup"><span data-stu-id="7de65-156">Chapter 1 – The Azure Portal</span></span>

<span data-ttu-id="7de65-157">Pour utiliser le *API vision par ordinateur* service dans Azure, vous devez configurer une instance du service à être mis à disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="7de65-157">To use the *Computer Vision API* service in Azure, you will need to configure an instance of the service to be made available to your application.</span></span>

1.  <span data-ttu-id="7de65-158">Tout d’abord, connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7de65-158">First, log in to the [Azure Portal](https://portal.azure.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="7de65-159">Si vous n’avez pas déjà un compte Azure, vous devrez créer un.</span><span class="sxs-lookup"><span data-stu-id="7de65-159">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="7de65-160">Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="7de65-160">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="7de65-161">Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez *API vision par ordinateur*, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="7de65-161">Once you are logged in, click on **New** in the top left corner, and search for *Computer Vision API*, and click **Enter**.</span></span>

    ![Créer une nouvelle ressource dans Azure](images/AzureLabs-Lab2-00.png)

    > [!NOTE]
    > <span data-ttu-id="7de65-163">Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.</span><span class="sxs-lookup"><span data-stu-id="7de65-163">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>
 
3.  <span data-ttu-id="7de65-164">La nouvelle page doit fournir une description de la *API vision par ordinateur* service.</span><span class="sxs-lookup"><span data-stu-id="7de65-164">The new page will provide a description of the *Computer Vision API* service.</span></span> <span data-ttu-id="7de65-165">En bas à gauche de cette page, sélectionnez le **créer** bouton permettant de créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="7de65-165">At the bottom left of this page, select the **Create** button, to create an association with this service.</span></span>

    ![Sur le service d’api de vision par ordinateur](images/AzureLabs-Lab2-01.png)
 
4.  <span data-ttu-id="7de65-167">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="7de65-167">Once you have clicked on **Create**:</span></span>

    1. <span data-ttu-id="7de65-168">Insérez votre souhaitée **nom** pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="7de65-168">Insert your desired **Name** for this service instance.</span></span>
    2. <span data-ttu-id="7de65-169">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="7de65-169">Select a **Subscription**.</span></span>
    3. <span data-ttu-id="7de65-170">Sélectionnez le **niveau tarifaire** appropriés pour vous, s’il s’agit du premier temps à créer un *API vision par ordinateur* Service, un niveau gratuit (nommé F0) doit être disponible pour vous.</span><span class="sxs-lookup"><span data-stu-id="7de65-170">Select the **Pricing Tier** appropriate for you, if this is the first time creating a *Computer Vision API* Service, a free tier (named F0) should be available to you.</span></span>
    4. <span data-ttu-id="7de65-171">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="7de65-171">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="7de65-172">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="7de65-172">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="7de65-173">Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="7de65-173">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span> 

        > <span data-ttu-id="7de65-174">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="7de65-174">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5. <span data-ttu-id="7de65-175">Déterminer l’emplacement de votre groupe de ressources (si vous créez un nouveau groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="7de65-175">Determine the Location for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="7de65-176">Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="7de65-176">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="7de65-177">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="7de65-177">Some Azure assets are only available in certain regions.</span></span>

    6. <span data-ttu-id="7de65-178">Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.</span><span class="sxs-lookup"><span data-stu-id="7de65-178">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>
    7. <span data-ttu-id="7de65-179">Cliquez sur Créer.</span><span class="sxs-lookup"><span data-stu-id="7de65-179">Click Create.</span></span>

        ![Informations sur la création de service](images/AzureLabs-Lab2-02.png)

5.  <span data-ttu-id="7de65-181">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="7de65-181">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>
6.  <span data-ttu-id="7de65-182">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="7de65-182">A notification will appear in the portal once the Service instance is created.</span></span>

    ![Consultez la notification de nouveau pour votre nouveau service](images/AzureLabs-Lab2-03.png) 
 
7.  <span data-ttu-id="7de65-184">Cliquez sur la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="7de65-184">Click on the notification to explore your new Service instance.</span></span> 

    ![Sélectionnez le bouton d’accéder à la ressource.](images/AzureLabs-Lab2-04.png)
 
8. <span data-ttu-id="7de65-186">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="7de65-186">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="7de65-187">Vous êtes redirigé vers votre nouvelle instance de service API vision par ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7de65-187">You will be taken to your new Computer Vision API service instance.</span></span> 

    ![Votre nouveau service de l’API vision par ordinateur](images/AzureLabs-Lab2-05.png)
 
9.  <span data-ttu-id="7de65-189">Dans ce didacticiel, votre application devra effectuer des appels à votre service, par l’intermédiaire à l’aide de la clé d’abonnement de votre service.</span><span class="sxs-lookup"><span data-stu-id="7de65-189">Within this tutorial, your application will need to make calls to your service, which is done through using your service’s Subscription Key.</span></span>
10. <span data-ttu-id="7de65-190">À partir de la *Guide de démarrage rapide* page, de votre *API vision par ordinateur* de service, accédez à la première étape, *récupérez vos clés*et cliquez sur **clés** () Vous pouvez également y parvenir en cliquant sur le lien hypertexte bleu clés, situé dans le menu de navigation de services, indiqué par l’icône de clé).</span><span class="sxs-lookup"><span data-stu-id="7de65-190">From the *Quick start* page, of your *Computer Vision API* service, navigate to the first step, *Grab your keys*, and click **Keys** (you can also achieve this by clicking the blue hyperlink Keys, located in the services navigation menu, denoted by the key icon).</span></span> <span data-ttu-id="7de65-191">Cela permet de révéler votre service *clés*.</span><span class="sxs-lookup"><span data-stu-id="7de65-191">This will reveal your service *Keys*.</span></span>
11. <span data-ttu-id="7de65-192">Effectuez une copie de l’une des clés affichées, car vous en aurez besoin plus loin dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="7de65-192">Take a copy of one of the displayed keys, as you will need this later in your project.</span></span> 

12. <span data-ttu-id="7de65-193">Revenez à la *Guide de démarrage rapide* page et à partir de là, fetch votre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="7de65-193">Go back to the *Quick start* page, and from there, fetch your endpoint.</span></span> <span data-ttu-id="7de65-194">N’oubliez pas la vôtre peut être différent, selon votre région (qui dans le cas, vous devez apporter une modification à votre code plus tard).</span><span class="sxs-lookup"><span data-stu-id="7de65-194">Be aware yours may be different, depending on your region (which if it is, you will need to make a change to your code later).</span></span> <span data-ttu-id="7de65-195">Effectuez une copie de ce point de terminaison pour une utilisation ultérieure :</span><span class="sxs-lookup"><span data-stu-id="7de65-195">Take a copy of this endpoint for use later:</span></span>

    ![Votre nouveau service de l’API vision par ordinateur](images/AzureLabs-Lab2-05-5.png)

    > [!TIP]
    > <span data-ttu-id="7de65-197">Vous pouvez vérifier quelles sont les différents points de terminaison [ici](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa).</span><span class="sxs-lookup"><span data-stu-id="7de65-197">You can check what the various endpoints are [HERE](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa).</span></span> 

## <a name="chapter-2--set-up-the-unity-project"></a><span data-ttu-id="7de65-198">Chapitre 2 : configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="7de65-198">Chapter 2 – Set up the Unity project</span></span>

<span data-ttu-id="7de65-199">Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="7de65-199">The following is a typical set up for developing with mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="7de65-200">Ouvrez *Unity* et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="7de65-200">Open *Unity* and click **New**.</span></span> 

    ![Démarrer un nouveau projet Unity.](images/AzureLabs-Lab2-06.png)

2.  <span data-ttu-id="7de65-202">Maintenant, vous devez fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="7de65-202">You will now need to provide a Unity Project name.</span></span> <span data-ttu-id="7de65-203">Insérer **MR_ComputerVision**.</span><span class="sxs-lookup"><span data-stu-id="7de65-203">Insert **MR_ComputerVision**.</span></span> <span data-ttu-id="7de65-204">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="7de65-204">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="7de65-205">Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="7de65-205">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="7de65-206">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="7de65-206">Then, click **Create project**.</span></span>

    ![Fournissent des détails pour un projet Unity.](images/AzureLabs-Lab2-07.png)

3.  <span data-ttu-id="7de65-208">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="7de65-208">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="7de65-209">Accédez à **Modifier > Préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="7de65-209">Go to **Edit > Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="7de65-210">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="7de65-210">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="7de65-211">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="7de65-211">Close the **Preferences** window.</span></span>

    ![Mettre à jour les préférences de l’éditeur de script.](images/AzureLabs-Lab2-08.png)

4.  <span data-ttu-id="7de65-213">Ensuite, accédez à **fichier > Paramètres de Build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le **plateforme de commutation** bouton pour appliquer votre sélection.</span><span class="sxs-lookup"><span data-stu-id="7de65-213">Next, go to **File > Build Settings** and select **Universal Windows Platform**, then click on the **Switch Platform** button to apply your selection.</span></span>

    ![Fenêtre Paramètres, plateforme de commutation à UWP de la génération.](images/AzureLabs-Lab2-10.png)

5.  <span data-ttu-id="7de65-215">Lorsque vous êtes toujours dans **fichier > Paramètres de Build** et vous assurer que :</span><span class="sxs-lookup"><span data-stu-id="7de65-215">While still in **File > Build Settings** and make sure that:</span></span>

    1. <span data-ttu-id="7de65-216">**Équipement cible** a la valeur **HoloLens**</span><span class="sxs-lookup"><span data-stu-id="7de65-216">**Target Device** is set to **HoloLens**</span></span>

        > <span data-ttu-id="7de65-217">Pour des casques IMMERSIFS, définissez **appareil cible** à *n’importe quel appareil*.</span><span class="sxs-lookup"><span data-stu-id="7de65-217">For the immersive headsets, set **Target Device** to *Any Device*.</span></span>

    2. <span data-ttu-id="7de65-218">**Type de build** a la valeur **D3D**</span><span class="sxs-lookup"><span data-stu-id="7de65-218">**Build Type** is set to **D3D**</span></span>
    3. <span data-ttu-id="7de65-219">**Kit de développement logiciel** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="7de65-219">**SDK** is set to **Latest installed**</span></span>
    4. <span data-ttu-id="7de65-220">**Version de Visual Studio** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="7de65-220">**Visual Studio Version** is set to **Latest installed**</span></span>
    5. <span data-ttu-id="7de65-221">**Générez et exécutez** est défini sur **ordinateur Local**</span><span class="sxs-lookup"><span data-stu-id="7de65-221">**Build and Run** is set to **Local Machine**</span></span>
    6. <span data-ttu-id="7de65-222">Enregistrer la scène et l’ajouter à la build.</span><span class="sxs-lookup"><span data-stu-id="7de65-222">Save the scene and add it to the build.</span></span>

        1. <span data-ttu-id="7de65-223">Cela en sélectionnant **ajouter un arrière-plan Open**.</span><span class="sxs-lookup"><span data-stu-id="7de65-223">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="7de65-224">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7de65-224">A save window will appear.</span></span>
        
            ![Cliquez sur Ajouter un bouton scènes ouvert](images/AzureLabs-Lab2-11.png)

        2. <span data-ttu-id="7de65-226">Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.</span><span class="sxs-lookup"><span data-stu-id="7de65-226">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![Créer un nouveau dossier de scripts](images/AzureLabs-Lab2-12.png)

        3. <span data-ttu-id="7de65-228">Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier*: champ de texte, tapez **MR_ComputerVisionScene**, puis cliquez sur **enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7de65-228">Open your newly created **Scenes** folder, and then in the *File name*: text field, type **MR_ComputerVisionScene**, then click **Save**.</span></span>

            ![Donnez un nom à nouvelle scène.](images/AzureLabs-Lab2-13.png)

            > <span data-ttu-id="7de65-230">N’oubliez pas, vous devez enregistrer vos séquences de Unity dans le *actifs* dossier, car ils doivent être associées au projet Unity.</span><span class="sxs-lookup"><span data-stu-id="7de65-230">Be aware, you must save your Unity scenes within the *Assets* folder, as they must be associated with the Unity Project.</span></span> <span data-ttu-id="7de65-231">Création du dossier de scènes (et autres dossiers similaire) est un moyen classique de structurer un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="7de65-231">Creating the scenes folder (and other similar folders) is a typical way of structuring a Unity project.</span></span>

    7. <span data-ttu-id="7de65-232">Les autres paramètres, dans *paramètres de Build*, doit être conservé comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="7de65-232">The remaining settings, in *Build Settings*, should be left as default for now.</span></span>

6. <span data-ttu-id="7de65-233">Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve.</span><span class="sxs-lookup"><span data-stu-id="7de65-233">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span> 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab2-14.png)

7. <span data-ttu-id="7de65-235">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="7de65-235">In this panel, a few settings need to be verified:</span></span>

    1. <span data-ttu-id="7de65-236">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="7de65-236">In the **Other Settings** tab:</span></span>

        1. <span data-ttu-id="7de65-237">**Version du Runtime de script** doit être **Stable** (équivalent .NET 3.5).</span><span class="sxs-lookup"><span data-stu-id="7de65-237">**Scripting Runtime Version** should be **Stable** (.NET 3.5 Equivalent).</span></span>
        2. <span data-ttu-id="7de65-238">**Script principal** doit être **.NET**</span><span class="sxs-lookup"><span data-stu-id="7de65-238">**Scripting Backend** should be **.NET**</span></span>
        3. <span data-ttu-id="7de65-239">**Niveau de compatibilité d’API** doit être **.NET 4.6**</span><span class="sxs-lookup"><span data-stu-id="7de65-239">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![Mettre à jour les autres paramètres.](images/AzureLabs-Lab2-15.png)
      
    2. <span data-ttu-id="7de65-241">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="7de65-241">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        1. <span data-ttu-id="7de65-242">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="7de65-242">**InternetClient**</span></span>
        2. <span data-ttu-id="7de65-243">**Webcam**</span><span class="sxs-lookup"><span data-stu-id="7de65-243">**Webcam**</span></span>

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab2-16.png)

    3. <span data-ttu-id="7de65-245">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.</span><span class="sxs-lookup"><span data-stu-id="7de65-245">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Mettre à jour les paramètres de R X.](images/AzureLabs-Lab2-17.png)

8.  <span data-ttu-id="7de65-247">Dans *paramètres de Build* _Unity C#_  projets est n’est plus grisée ; Cochez la case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="7de65-247">Back in *Build Settings* _Unity C#_ Projects is no longer greyed out; tick the checkbox next to this.</span></span> 
9.  <span data-ttu-id="7de65-248">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="7de65-248">Close the Build Settings window.</span></span>
10. <span data-ttu-id="7de65-249">Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="7de65-249">Save your Scene and Project (**FILE > SAVE SCENE / FILE > SAVE PROJECT**).</span></span>

## <a name="chapter-3--main-camera-setup"></a><span data-ttu-id="7de65-250">Chapitre 3 – le programme d’installation de la caméra principale</span><span class="sxs-lookup"><span data-stu-id="7de65-250">Chapter 3 – Main Camera setup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7de65-251">Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302%20-%20Computer%20vision/Azure-MR-302.unitypackage), importez-le dans votre projet comme un [Package personnalisé ](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 5](#chapter-5--create-the-resultslabel-class).</span><span class="sxs-lookup"><span data-stu-id="7de65-251">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to download this [.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302%20-%20Computer%20vision/Azure-MR-302.unitypackage), import it into your project as a [Custom Package](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 5](#chapter-5--create-the-resultslabel-class).</span></span>

1.  <span data-ttu-id="7de65-252">Dans le *hiérarchie panneau*, sélectionnez le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="7de65-252">In the *Hierarchy Panel*, select the **Main Camera**.</span></span> 
2.  <span data-ttu-id="7de65-253">Une fois sélectionné, vous serez en mesure de voir tous les composants de la **Main Camera** dans le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="7de65-253">Once selected, you will be able to see all the components of the **Main Camera** in the *Inspector Panel*.</span></span>

    1. <span data-ttu-id="7de65-254">Le **objet caméra** doit être nommé **Main Camera** (Notez l’orthographe !)</span><span class="sxs-lookup"><span data-stu-id="7de65-254">The **Camera object** must be named **Main Camera** (note the spelling!)</span></span>
    2. <span data-ttu-id="7de65-255">La caméra principale **balise** doit être définie sur **MainCamera** (Notez l’orthographe !)</span><span class="sxs-lookup"><span data-stu-id="7de65-255">The Main Camera **Tag** must be set to **MainCamera** (note the spelling!)</span></span>
    3. <span data-ttu-id="7de65-256">Assurez-vous que le **Position transformer** a la valeur **0, 0, 0**</span><span class="sxs-lookup"><span data-stu-id="7de65-256">Make sure the **Transform Position** is set to **0, 0, 0**</span></span>
    4. <span data-ttu-id="7de65-257">Définissez **effacer les indicateurs** à **couleur unie** (ignorer cela pour casque immersif).</span><span class="sxs-lookup"><span data-stu-id="7de65-257">Set **Clear Flags** to **Solid Color** (ignore this for immersive headset).</span></span>
    5. <span data-ttu-id="7de65-258">Définir le **arrière-plan** couleur du composant de caméra à **noir, Alpha 0 (Hex Code : #00000000)** (ignorer cela pour casque immersif).</span><span class="sxs-lookup"><span data-stu-id="7de65-258">Set the **Background** Color of the Camera Component to **Black, Alpha 0 (Hex Code: #00000000)** (ignore this for immersive headset).</span></span>

        ![Mettre à jour des composants de l’appareil photo.](images/AzureLabs-Lab2-18.png)
 
3.  <span data-ttu-id="7de65-260">Ensuite, vous devrez créer un objet simple « curseur » attaché à la **Main Camera**, ce qui vous aident à positionner l’analyse d’image génère lorsque l’application est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7de65-260">Next, you will have to create a simple “Cursor” object attached to the **Main Camera**, which will help you position the image analysis output when the application is running.</span></span> <span data-ttu-id="7de65-261">Ce curseur déterminera le point central de la vue de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="7de65-261">This Cursor will determine the center point of the camera focus.</span></span>

<span data-ttu-id="7de65-262">Pour créer le curseur :</span><span class="sxs-lookup"><span data-stu-id="7de65-262">To create the Cursor:</span></span>

1.  <span data-ttu-id="7de65-263">Dans le *hiérarchie panneau*, avec le bouton droit sur le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="7de65-263">In the *Hierarchy Panel*, right-click on the **Main Camera**.</span></span> <span data-ttu-id="7de65-264">Sous **objet 3D**, cliquez sur **sphère**.</span><span class="sxs-lookup"><span data-stu-id="7de65-264">Under **3D Object**, click on **Sphere**.</span></span>

    ![Sélectionnez l’objet curseur.](images/AzureLabs-Lab2-19.png)
 
2.  <span data-ttu-id="7de65-266">Renommer le **sphère** à **curseur** (double-cliquez sur l’objet curseur ou appuyez sur le bouton de clavier « F2 » avec l’objet sélectionné) et assurez-vous qu’il se trouve en tant qu’enfant de le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="7de65-266">Rename the **Sphere** to **Cursor** (double click the Cursor object or press the ‘F2’ keyboard button with the object selected), and make sure it is located as child of the **Main Camera**.</span></span>

3.  <span data-ttu-id="7de65-267">Dans le *hiérarchie panneau*, cliquez sur le **curseur**.</span><span class="sxs-lookup"><span data-stu-id="7de65-267">In the *Hierarchy Panel*, left click on the **Cursor**.</span></span> <span data-ttu-id="7de65-268">Avec le curseur sélectionné, ajuster les variables suivantes dans le *panneau Inspecteur*:</span><span class="sxs-lookup"><span data-stu-id="7de65-268">With the Cursor selected, adjust the following variables in the *Inspector Panel*:</span></span>

    1. <span data-ttu-id="7de65-269">Définir le *transformer Position* à **0, 0, 5**</span><span class="sxs-lookup"><span data-stu-id="7de65-269">Set the *Transform Position* to **0, 0, 5**</span></span>
    2. <span data-ttu-id="7de65-270">Définir le *mise à l’échelle* à **0,02, 0,02, 0,02**</span><span class="sxs-lookup"><span data-stu-id="7de65-270">Set the *Scale* to **0.02, 0.02, 0.02**</span></span>

        ![Mettre à jour la Position de la transformation et de la mise à l’échelle.](images/AzureLabs-Lab2-20.png)
  
## <a name="chapter-4--setup-the-label-system"></a><span data-ttu-id="7de65-272">Chapitre 4 – programme d’installation du système d’étiquette</span><span class="sxs-lookup"><span data-stu-id="7de65-272">Chapter 4 – Setup the Label system</span></span>

<span data-ttu-id="7de65-273">Une fois que vous avez capturé une image avec l’appareil photo des HoloLens, cette image sera envoyée à votre *API de vision par ordinateur Azure* instance de Service pour l’analyse.</span><span class="sxs-lookup"><span data-stu-id="7de65-273">Once you have captured an image with the HoloLens’ camera, that image will be sent to your *Azure Computer Vision API* Service instance for analysis.</span></span> 

<span data-ttu-id="7de65-274">Les résultats de cette analyse sera une liste d’objets reconnus appelé **balises**.</span><span class="sxs-lookup"><span data-stu-id="7de65-274">The results of that analysis will be a list of recognized objects called **Tags**.</span></span> 

<span data-ttu-id="7de65-275">Vous utiliserez des étiquettes (comme un texte 3D dans l’espace universel) pour afficher ces balises à l’emplacement de que la photo a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="7de65-275">You will use Labels (as a 3D text in world space) to display these Tags at the location the photo was taken.</span></span>

<span data-ttu-id="7de65-276">Les étapes suivantes expliquent comment configurer le **étiquette** objet.</span><span class="sxs-lookup"><span data-stu-id="7de65-276">The following steps will show how to setup the **Label** object.</span></span>

1.  <span data-ttu-id="7de65-277">Avec le bouton droit n’importe où dans le volet de hiérarchie (l’emplacement n’a pas d’importance à ce stade), sous **objet 3D**, ajoutez un **texte 3D**.</span><span class="sxs-lookup"><span data-stu-id="7de65-277">Right-click anywhere in the Hierarchy Panel (the location does not matter at this point), under **3D Object**, add a **3D Text**.</span></span> <span data-ttu-id="7de65-278">Nommez-le **LabelText**.</span><span class="sxs-lookup"><span data-stu-id="7de65-278">Name it **LabelText**.</span></span>

    ![Créer un objet de texte 3D.](images/AzureLabs-Lab2-21.png)
 
2.  <span data-ttu-id="7de65-280">Dans le *hiérarchie panneau*, cliquez sur le **LabelText**.</span><span class="sxs-lookup"><span data-stu-id="7de65-280">In the *Hierarchy Panel*, left click on the **LabelText**.</span></span> <span data-ttu-id="7de65-281">Avec le **LabelText** sélectionnée, d’ajuster les variables suivantes dans le *panneau Inspecteur*:</span><span class="sxs-lookup"><span data-stu-id="7de65-281">With the **LabelText** selected, adjust the following variables in the *Inspector Panel*:</span></span>

    1. <span data-ttu-id="7de65-282">Définir le **Position** à **0,0,0**</span><span class="sxs-lookup"><span data-stu-id="7de65-282">Set the **Position** to **0,0,0**</span></span>
    2. <span data-ttu-id="7de65-283">Définir le **mise à l’échelle** à **0,01, 0,01, 0,01**</span><span class="sxs-lookup"><span data-stu-id="7de65-283">Set the **Scale** to **0.01, 0.01, 0.01**</span></span>
    3. <span data-ttu-id="7de65-284">Dans le composant **texte Mesh**:</span><span class="sxs-lookup"><span data-stu-id="7de65-284">In the component **Text Mesh**:</span></span>
    4. <span data-ttu-id="7de65-285">Remplacez tout le texte dans **texte**, avec «... »</span><span class="sxs-lookup"><span data-stu-id="7de65-285">Replace all the text within **Text**, with "..."</span></span>        
    5. <span data-ttu-id="7de65-286">Définir le **ancre** à **milieu centre**</span><span class="sxs-lookup"><span data-stu-id="7de65-286">Set the **Anchor** to **Middle Center**</span></span>
    6. <span data-ttu-id="7de65-287">Définir le **alignement** à **Center**</span><span class="sxs-lookup"><span data-stu-id="7de65-287">Set the **Alignment** to **Center**</span></span>
    7. <span data-ttu-id="7de65-288">Définir le **taille des tabulations** à **4**</span><span class="sxs-lookup"><span data-stu-id="7de65-288">Set the **Tab Size** to **4**</span></span>
    8. <span data-ttu-id="7de65-289">Définir le **la taille de police** à **50**</span><span class="sxs-lookup"><span data-stu-id="7de65-289">Set the **Font Size** to **50**</span></span>
    9. <span data-ttu-id="7de65-290">Définir le **couleur** à **#FFFFFFFF**</span><span class="sxs-lookup"><span data-stu-id="7de65-290">Set the **Color** to **#FFFFFFFF**</span></span>

    ![Composant de texte](images/AzureLabs-Lab2-21-5.png)

3.  <span data-ttu-id="7de65-292">Faites glisser le **LabelText** à partir de la *Panneau de la hiérarchie*, dans le *dossier composants*, en respectant dans le *Panneau de configuration de projet*.</span><span class="sxs-lookup"><span data-stu-id="7de65-292">Drag the **LabelText** from the *Hierarchy Panel*, into the *Asset Folder*, within in the *Project Panel*.</span></span> <span data-ttu-id="7de65-293">Cela rendra le **LabelText** un préfabriqué, afin qu’elle peut être instancié dans le code.</span><span class="sxs-lookup"><span data-stu-id="7de65-293">This will make the **LabelText** a Prefab, so that it can be instantiated in code.</span></span>

    ![Créer un préfabriqué de l’objet LabelText.](images/AzureLabs-Lab2-22.png)
 
4.  <span data-ttu-id="7de65-295">Vous devez supprimer le **LabelText** à partir de la *hiérarchie panneau*, afin qu’il s’affichera pas dans la scène d’ouverture.</span><span class="sxs-lookup"><span data-stu-id="7de65-295">You should delete the **LabelText** from the *Hierarchy Panel*, so that it will not be displayed in the opening scene.</span></span> <span data-ttu-id="7de65-296">Comme il est désormais un préfabriqué, qui vous appellera pour les instances individuelles de votre dossier de ressources, il n’est pas nécessaire pour conserver dans la scène.</span><span class="sxs-lookup"><span data-stu-id="7de65-296">As it is now a prefab, which you will call on for individual instances from your Assets folder, there is no need to keep it within the scene.</span></span> 
5.  <span data-ttu-id="7de65-297">La structure de l’objet final dans le *hiérarchie panneau* doit être semblable à celui illustré dans l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7de65-297">The final object structure in the *Hierarchy Panel* should be like the one shown in the image below:</span></span>

    ![Structure finale du Panneau de hiérarchie.](images/AzureLabs-Lab2-23.png)

## <a name="chapter-5--create-the-resultslabel-class"></a><span data-ttu-id="7de65-299">Chapitre 5 : créer la classe ResultsLabel</span><span class="sxs-lookup"><span data-stu-id="7de65-299">Chapter 5 – Create the ResultsLabel class</span></span>

<span data-ttu-id="7de65-300">Est le premier script que vous avez besoin pour créer le *ResultsLabel* (classe), qui est chargé pour les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7de65-300">The first script you need to create is the *ResultsLabel* class, which is responsible for the following:</span></span> 

- <span data-ttu-id="7de65-301">Créer les étiquettes dans l’espace de monde approprié, par rapport à la position de la caméra.</span><span class="sxs-lookup"><span data-stu-id="7de65-301">Creating the Labels in the appropriate world space, relative to the position of the Camera.</span></span>
- <span data-ttu-id="7de65-302">Afficher les balises à partir de l’analyse de l’Image.</span><span class="sxs-lookup"><span data-stu-id="7de65-302">Displaying the Tags from the Image Anaysis.</span></span>

<span data-ttu-id="7de65-303">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="7de65-303">To create this class:</span></span> 

1.  <span data-ttu-id="7de65-304">Avec le bouton droit dans le *Panneau de configuration de projet*, puis **créer > dossier**.</span><span class="sxs-lookup"><span data-stu-id="7de65-304">Right-click in the *Project Panel*, then **Create > Folder**.</span></span> <span data-ttu-id="7de65-305">Nommez le dossier **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="7de65-305">Name the folder **Scripts**.</span></span> 

    ![Créez le dossier scripts.](images/AzureLabs-Lab2-24.png)

2.  <span data-ttu-id="7de65-307">Avec le **Scripts** créer de dossier, double-cliquez dessus pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="7de65-307">With the **Scripts** folder create, double click it to open.</span></span> <span data-ttu-id="7de65-308">Ensuite, dans ce dossier, avec le bouton droit, puis sélectionnez **créer >** puis  **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="7de65-308">Then within that folder, right-click, and select **Create >** then **C# Script**.</span></span> <span data-ttu-id="7de65-309">Nommez le script *ResultsLabel*.</span><span class="sxs-lookup"><span data-stu-id="7de65-309">Name the script *ResultsLabel*.</span></span> 

3.  <span data-ttu-id="7de65-310">Double-cliquez sur le nouveau *ResultsLabel* script pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="7de65-310">Double click on the new *ResultsLabel* script to open it with **Visual Studio**.</span></span>

4.  <span data-ttu-id="7de65-311">À l’intérieur de la classe, insérez le code suivant dans le *ResultsLabel* classe :</span><span class="sxs-lookup"><span data-stu-id="7de65-311">Inside the Class insert the following code in the *ResultsLabel* class:</span></span>

    ```csharp
        using System.Collections.Generic;
        using UnityEngine;

        public class ResultsLabel : MonoBehaviour
        {   
            public static ResultsLabel instance;

            public GameObject cursor;

            public Transform labelPrefab;

            [HideInInspector]
            public Transform lastLabelPlaced;

            [HideInInspector]
            public TextMesh lastLabelPlacedText;

            private void Awake()
            {
                // allows this instance to behave like a singleton
                instance = this;
            }

            /// <summary>
            /// Instantiate a Label in the appropriate location relative to the Main Camera.
            /// </summary>
            public void CreateLabel()
            {
                lastLabelPlaced = Instantiate(labelPrefab, cursor.transform.position, transform.rotation);

                lastLabelPlacedText = lastLabelPlaced.GetComponent<TextMesh>();

                // Change the text of the label to show that has been placed
                // The final text will be set at a later stage
                lastLabelPlacedText.text = "Analysing...";
            }

            /// <summary>
            /// Set the Tags as Text of the last Label created. 
            /// </summary>
            public void SetTagsToLastLabel(Dictionary<string, float> tagsDictionary)
            {
                lastLabelPlacedText = lastLabelPlaced.GetComponent<TextMesh>();

                // At this point we go through all the tags received and set them as text of the label
                lastLabelPlacedText.text = "I see: \n";

                foreach (KeyValuePair<string, float> tag in tagsDictionary)
                {
                    lastLabelPlacedText.text += tag.Key + ", Confidence: " + tag.Value.ToString("0.00 \n");
                }    
            }
        }
    ```

6.  <span data-ttu-id="7de65-312">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="7de65-312">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>
7.  <span data-ttu-id="7de65-313">Dans le *éditeur Unity*, cliquez et faites glisser le *ResultsLabel* classe à partir de la **Scripts** dossier pour le **Main Camera** objet dans le  *Panneau de la hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="7de65-313">Back in the *Unity Editor*, click and drag the *ResultsLabel* class from the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span>
8.  <span data-ttu-id="7de65-314">Cliquez sur le **Main Camera** et examinez le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="7de65-314">Click on the **Main Camera** and look at the *Inspector Panel*.</span></span>

<span data-ttu-id="7de65-315">Vous remarquerez qu’à partir du script que vous venez de faire glisser dans l’appareil photo, il existe deux champs : **Curseur** et **étiquette Prefab**.</span><span class="sxs-lookup"><span data-stu-id="7de65-315">You will notice that from the script you just dragged into the Camera, there are two fields: **Cursor** and **Label Prefab**.</span></span>

9.  <span data-ttu-id="7de65-316">Faites glisser l’objet appelé **curseur** à partir de la *hiérarchie panneau* vers l’emplacement nommé **curseur**, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7de65-316">Drag the object called **Cursor** from the *Hierarchy Panel* to the slot named **Cursor**, as shown in the image below.</span></span>
10. <span data-ttu-id="7de65-317">Faites glisser l’objet appelé **LabelText** à partir de la *dossier Assets* dans le *panneau projet* vers l’emplacement nommé **Prefab étiquette**, comme illustré dans la image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7de65-317">Drag the object called **LabelText** from the *Assets Folder* in the *Project Panel* to the slot named **Label Prefab**, as shown in the image below.</span></span> 

    ![Définir les cibles de référence dans Unity.](images/AzureLabs-Lab2-25.png)

## <a name="chapter-6--create-the-imagecapture-class"></a><span data-ttu-id="7de65-319">Chapitre 6 : créer la classe ImageCapture</span><span class="sxs-lookup"><span data-stu-id="7de65-319">Chapter 6 – Create the ImageCapture class</span></span>

<span data-ttu-id="7de65-320">La classe suivante, vous allez créer est la *ImageCapture* classe.</span><span class="sxs-lookup"><span data-stu-id="7de65-320">The next class you are going to create is the *ImageCapture* class.</span></span> <span data-ttu-id="7de65-321">Cette classe est chargée de :</span><span class="sxs-lookup"><span data-stu-id="7de65-321">This class is responsible for:</span></span>

-   <span data-ttu-id="7de65-322">Capture d’une Image à l’aide de l’appareil photo HoloLens et en le stockant dans le dossier d’application.</span><span class="sxs-lookup"><span data-stu-id="7de65-322">Capturing an Image using the HoloLens Camera and storing it in the App Folder.</span></span>
-   <span data-ttu-id="7de65-323">Mouvements de drainage de capture à partir de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7de65-323">Capturing Tap gestures from the user.</span></span>

<span data-ttu-id="7de65-324">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="7de65-324">To create this class:</span></span> 

1.  <span data-ttu-id="7de65-325">Accédez à la **Scripts** dossier que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="7de65-325">Go to the **Scripts** folder you created previously.</span></span> 
2.  <span data-ttu-id="7de65-326">Avec le bouton droit dans le dossier, **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="7de65-326">Right-click inside the folder, **Create > C# Script**.</span></span> <span data-ttu-id="7de65-327">Appeler le script *ImageCapture*.</span><span class="sxs-lookup"><span data-stu-id="7de65-327">Call the script *ImageCapture*.</span></span> 
3.  <span data-ttu-id="7de65-328">Double-cliquez sur le nouveau *ImageCapture* script pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="7de65-328">Double click on the new *ImageCapture* script to open it with **Visual Studio**.</span></span>
4.  <span data-ttu-id="7de65-329">Ajoutez les espaces de noms suivantes au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="7de65-329">Add the following namespaces to the top of the file:</span></span>

    ```csharp
        using System.IO;
        using System.Linq;
        using UnityEngine;
        using UnityEngine.XR.WSA.Input;
        using UnityEngine.XR.WSA.WebCam;
    ```

5.  <span data-ttu-id="7de65-330">Puis ajoutez les variables suivantes à l’intérieur de la *ImageCapture* classe ci-dessus le *Start()* méthode :</span><span class="sxs-lookup"><span data-stu-id="7de65-330">Then add the following variables inside the *ImageCapture* class, above the *Start()* method:</span></span>

    ```csharp
        public static ImageCapture instance; 
        public int tapsCount;
        private PhotoCapture photoCaptureObject = null;
        private GestureRecognizer recognizer;
        private bool currentlyCapturing = false;
    ```
 
<span data-ttu-id="7de65-331">Le **tapsCount** variable stocke le nombre de mouvements tap capturées à partir de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7de65-331">The **tapsCount** variable will store the number of tap gestures captured from the user.</span></span> <span data-ttu-id="7de65-332">Ce nombre est utilisé dans l’affectation des noms des images capturées.</span><span class="sxs-lookup"><span data-stu-id="7de65-332">This number is used in the naming of the images captured.</span></span>

6.  <span data-ttu-id="7de65-333">Code pour *Awake()* et *Start()* méthodes doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="7de65-333">Code for *Awake()* and *Start()* methods now needs to be added.</span></span> <span data-ttu-id="7de65-334">Il seront appelées lors de l’initialisation de la classe :</span><span class="sxs-lookup"><span data-stu-id="7de65-334">These will be called when the class initializes:</span></span>

    ```csharp
        private void Awake()
        {
            // Allows this instance to behave like a singleton
            instance = this;
        }

        void Start()
        {
            // subscribing to the Hololens API gesture recognizer to track user gestures
            recognizer = new GestureRecognizer();
            recognizer.SetRecognizableGestures(GestureSettings.Tap);
            recognizer.Tapped += TapHandler;
            recognizer.StartCapturingGestures();
        }
    ```

7.  <span data-ttu-id="7de65-335">Implémentez un gestionnaire qui sera appelé lorsqu’une action d’appuyer se produit.</span><span class="sxs-lookup"><span data-stu-id="7de65-335">Implement a handler that will be called when a Tap gesture occurs.</span></span> 

    ```csharp
        /// <summary>
        /// Respond to Tap Input.
        /// </summary>
        private void TapHandler(TappedEventArgs obj)
        {
            // Only allow capturing, if not currently processing a request.
            if(currentlyCapturing == false)
            {
                currentlyCapturing = true;
            
                // increment taps count, used to name images when saving
                tapsCount++;

                // Create a label in world space using the ResultsLabel class
                ResultsLabel.instance.CreateLabel();

                // Begins the image capture and analysis procedure
                ExecuteImageCaptureAndAnalysis();
            }
        }
    ```
 
<span data-ttu-id="7de65-336">Le *TapHandler()* méthode incrémente le nombre de coefficients capturées à partir de l’utilisateur et utilise la position actuelle du curseur pour déterminer où positionner une nouvelle étiquette.</span><span class="sxs-lookup"><span data-stu-id="7de65-336">The *TapHandler()* method increments the number of taps captured from the user and uses the current Cursor position to determine where to position a new Label.</span></span>

<span data-ttu-id="7de65-337">Cette méthode appelle ensuite la *ExecuteImageCaptureAndAnalysis()* méthode pour commencer à la fonctionnalité principale de cette application.</span><span class="sxs-lookup"><span data-stu-id="7de65-337">This method then calls the *ExecuteImageCaptureAndAnalysis()* method to begin the core functionality of this application.</span></span>

8.  <span data-ttu-id="7de65-338">Une fois qu’une Image a été capturée et stockée, les gestionnaires suivants seront appelées.</span><span class="sxs-lookup"><span data-stu-id="7de65-338">Once an Image has been captured and stored, the following handlers will be called.</span></span> <span data-ttu-id="7de65-339">Si le processus réussit, le résultat est passé à la *VisionManager* (ce qui vous êtes encore à créer) pour l’analyse.</span><span class="sxs-lookup"><span data-stu-id="7de65-339">If the process is successful, the result is passed to the *VisionManager* (which you are yet to create) for analysis.</span></span>

    ```csharp
        /// <summary>
        /// Register the full execution of the Photo Capture. If successful, it will begin 
        /// the Image Analysis process.
        /// </summary>
        void OnCapturedPhotoToDisk(PhotoCapture.PhotoCaptureResult result)
        {
            // Call StopPhotoMode once the image has successfully captured
            photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
        }

        void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
        {
            // Dispose from the object in memory and request the image analysis 
            // to the VisionManager class
            photoCaptureObject.Dispose();
            photoCaptureObject = null;
            StartCoroutine(VisionManager.instance.AnalyseLastImageCaptured()); 
        }
    ```
 
9.  <span data-ttu-id="7de65-340">Ajoutez ensuite la méthode que l’application utilise pour démarrer le processus de capture d’Image et de stocker l’image.</span><span class="sxs-lookup"><span data-stu-id="7de65-340">Then add the method that the application uses to start the Image capture process and store the image.</span></span>

    ```csharp    
        /// <summary>    
        /// Begin process of Image Capturing and send To Azure     
        /// Computer Vision service.   
        /// </summary>    
        private void ExecuteImageCaptureAndAnalysis()  
        {    
            // Set the camera resolution to be the highest possible    
            Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending((res) => res.width * res.height).First();    

            Texture2D targetTexture = new Texture2D(cameraResolution.width, cameraResolution.height);
    
            // Begin capture process, set the image format    
            PhotoCapture.CreateAsync(false, delegate (PhotoCapture captureObject)    
            {    
                photoCaptureObject = captureObject;    
                CameraParameters camParameters = new CameraParameters();    
                camParameters.hologramOpacity = 0.0f;    
                camParameters.cameraResolutionWidth = targetTexture.width;    
                camParameters.cameraResolutionHeight = targetTexture.height;    
                camParameters.pixelFormat = CapturePixelFormat.BGRA32;
    
                // Capture the image from the camera and save it in the App internal folder    
                captureObject.StartPhotoModeAsync(camParameters, delegate (PhotoCapture.PhotoCaptureResult result)
                {    
                    string filename = string.Format(@"CapturedImage{0}.jpg", tapsCount);
    
                    string filePath = Path.Combine(Application.persistentDataPath, filename);

                    VisionManager.instance.imagePath = filePath;
    
                    photoCaptureObject.TakePhotoAsync(filePath, PhotoCaptureFileOutputFormat.JPG, OnCapturedPhotoToDisk);

                    currentlyCapturing = false;
                });   
            });    
        }
    ```
 
> [!WARNING] 
> <span data-ttu-id="7de65-341">À ce stade, vous remarquerez une erreur qui apparaissent dans le *volet de Console Unity Editor*.</span><span class="sxs-lookup"><span data-stu-id="7de65-341">At this point you will notice an error appearing in the *Unity Editor Console Panel*.</span></span> <span data-ttu-id="7de65-342">Il s’agit, car le code fait référence le *VisionManager* classe que vous allez créer dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="7de65-342">This is because the code references the *VisionManager* class which you will create in the next Chapter.</span></span>

## <a name="chapter-7--call-to-azure-and-image-analysis"></a><span data-ttu-id="7de65-343">Chapitre 7 – appel à Azure et d’analyse d’Image</span><span class="sxs-lookup"><span data-stu-id="7de65-343">Chapter 7 – Call to Azure and Image Analysis</span></span>

<span data-ttu-id="7de65-344">Est le dernier script, vous devez créer le *VisionManager* classe.</span><span class="sxs-lookup"><span data-stu-id="7de65-344">The last script you need to create is the *VisionManager* class.</span></span> 

<span data-ttu-id="7de65-345">Cette classe est chargée de :</span><span class="sxs-lookup"><span data-stu-id="7de65-345">This class is responsible for:</span></span>

-   <span data-ttu-id="7de65-346">Chargement de la dernière image capturée sous la forme d’un tableau d’octets.</span><span class="sxs-lookup"><span data-stu-id="7de65-346">Loading the latest image captured as an array of bytes.</span></span>
-   <span data-ttu-id="7de65-347">Envoi de tableau d’octets à votre *API de vision par ordinateur Azure* instance de Service pour l’analyse.</span><span class="sxs-lookup"><span data-stu-id="7de65-347">Sending the byte array to your *Azure Computer Vision API* Service instance for analysis.</span></span>
-   <span data-ttu-id="7de65-348">Recevoir une réponse sous forme de chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="7de65-348">Receiving the response as a JSON string.</span></span>
-   <span data-ttu-id="7de65-349">La désérialisation de la réponse et en passant les balises qui en résulte à la *ResultsLabel* classe.</span><span class="sxs-lookup"><span data-stu-id="7de65-349">Deserializing the response and passing the resulting Tags to the *ResultsLabel* class.</span></span>
 
<span data-ttu-id="7de65-350">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="7de65-350">To create this class:</span></span>

1.  <span data-ttu-id="7de65-351">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="7de65-351">Double click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="7de65-352">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="7de65-352">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="7de65-353">Nommez le script *VisionManager*.</span><span class="sxs-lookup"><span data-stu-id="7de65-353">Name the script *VisionManager*.</span></span> 
3.  <span data-ttu-id="7de65-354">Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7de65-354">Double click on the new script to open it with Visual Studio.</span></span>
4.  <span data-ttu-id="7de65-355">Mettre à jour les espaces de noms pour être le même que la commande suivante, en haut de la *VisionManager* classe :</span><span class="sxs-lookup"><span data-stu-id="7de65-355">Update the namespaces to be the same as the following, at the top of the *VisionManager* class:</span></span>

    ```csharp
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using System.IO;
        using UnityEngine;
        using UnityEngine.Networking;
    ```
 
5.  <span data-ttu-id="7de65-356">En haut de votre script, *à l’intérieur de* le *VisionManager* classe (au-dessus de la *Start()* méthode), vous devez maintenant créer deux *Classes* qui représente la réponse JSON désérialisée à partir d’Azure :</span><span class="sxs-lookup"><span data-stu-id="7de65-356">At the top of your script, *inside* the *VisionManager* class (above the *Start()* method), you now need to create two *Classes* that will represent the deserialized JSON response from Azure:</span></span>

    ```csharp
        [System.Serializable]
        public class TagData
        {
            public string name;
            public float confidence;
        }

        [System.Serializable]
        public class AnalysedObject
        {
            public TagData[] tags;
            public string requestId;
            public object metadata;
        }
    ```

    > [!NOTE] 
    > <span data-ttu-id="7de65-357">Le *TagData* et *AnalysedObject* classes ont besoin d’avoir le *[System.Serializable]* attribut ajouté avant la déclaration pour pouvoir être désérialisé avec la Unity bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="7de65-357">The *TagData* and *AnalysedObject* classes need to have the *[System.Serializable]* attribute added before the declaration to be able to be deserialized with the Unity libraries.</span></span>

6.  <span data-ttu-id="7de65-358">Dans la classe VisionManager, vous devez ajouter les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="7de65-358">In the VisionManager class, you should add the following variables:</span></span>

    ```csharp
        public static VisionManager instance;

        // you must insert your service key here!    
        private string authorizationKey = "- Insert your key here -";    
        private const string ocpApimSubscriptionKeyHeader = "Ocp-Apim-Subscription-Key";
        private string visionAnalysisEndpoint = "https://westus.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags";   // This is where you need to update your endpoint, if you set your location to something other than west-us.
  
        internal byte[] imageBytes;

        internal string imagePath;
    ```

    > [!WARNING] 
    > <span data-ttu-id="7de65-359">Assurez-vous que vous insérez votre **Auth Key** dans le **authorizationKey** variable.</span><span class="sxs-lookup"><span data-stu-id="7de65-359">Make sure you insert your **Auth Key** into the **authorizationKey** variable.</span></span> <span data-ttu-id="7de65-360">Avoir noté votre **Auth Key** au début de ce cours, [chapitre 1](#chapter-1--the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="7de65-360">You will have noted your **Auth Key** at the beginning of this course, [Chapter 1](#chapter-1--the-azure-portal).</span></span>

    > [!WARNING] 
    > <span data-ttu-id="7de65-361">Le **visionAnalysisEndpoint** variable peut-être différer de celle spécifiée dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="7de65-361">The **visionAnalysisEndpoint** variable might differ from the one specified in this example.</span></span> <span data-ttu-id="7de65-362">Le **west-us** strictement fait référence à des instances de Service créés pour la région ouest des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="7de65-362">The **west-us** strictly refers to Service instances created for the West US region.</span></span> <span data-ttu-id="7de65-363">Mettre à jour avec votre [URL de point de terminaison](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa); ici sont des exemples de ce que peuvent ressembler :</span><span class="sxs-lookup"><span data-stu-id="7de65-363">Update this with your [endpoint URL](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa); here are some examples of what that might look like:</span></span>
    > - <span data-ttu-id="7de65-364">Europe de l’ouest : `https://westeurope.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`</span><span class="sxs-lookup"><span data-stu-id="7de65-364">West Europe: `https://westeurope.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`</span></span>
    > - <span data-ttu-id="7de65-365">Asie du Sud-est : `https://southeastasia.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`</span><span class="sxs-lookup"><span data-stu-id="7de65-365">Southeast Asia: `https://southeastasia.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`</span></span>
    > - <span data-ttu-id="7de65-366">Est de l’Australie : `https://australiaeast.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`</span><span class="sxs-lookup"><span data-stu-id="7de65-366">Australia East: `https://australiaeast.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`</span></span>

7.  <span data-ttu-id="7de65-367">Code pour Awake doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="7de65-367">Code for Awake now needs to be added.</span></span> 

    ```csharp
        private void Awake()
        {
            // allows this instance to behave like a singleton
            instance = this;
        }
    ```

8.  <span data-ttu-id="7de65-368">Ensuite, ajoutez la coroutine (avec la méthode statique de flux en dessous), qui obtient les résultats de l’analyse de l’image capturée par le *ImageCapture* classe.</span><span class="sxs-lookup"><span data-stu-id="7de65-368">Next, add the coroutine (with the static stream method below it), which will obtain the results of the analysis of the image captured by the *ImageCapture* Class.</span></span> 

    ```csharp
        /// <summary>
        /// Call the Computer Vision Service to submit the image.
        /// </summary>
        public IEnumerator AnalyseLastImageCaptured()
        {
            WWWForm webForm = new WWWForm();
            using (UnityWebRequest unityWebRequest = UnityWebRequest.Post(visionAnalysisEndpoint, webForm))
            {
                // gets a byte array out of the saved image
                imageBytes = GetImageAsByteArray(imagePath);
                unityWebRequest.SetRequestHeader("Content-Type", "application/octet-stream");
                unityWebRequest.SetRequestHeader(ocpApimSubscriptionKeyHeader, authorizationKey);

                // the download handler will help receiving the analysis from Azure
                unityWebRequest.downloadHandler = new DownloadHandlerBuffer();

                // the upload handler will help uploading the byte array with the request
                unityWebRequest.uploadHandler = new UploadHandlerRaw(imageBytes);
                unityWebRequest.uploadHandler.contentType = "application/octet-stream";

                yield return unityWebRequest.SendWebRequest();

                long responseCode = unityWebRequest.responseCode;     

                try
                {
                    string jsonResponse = null;
                    jsonResponse = unityWebRequest.downloadHandler.text;

                    // The response will be in Json format
                    // therefore it needs to be deserialized into the classes AnalysedObject and TagData
                    AnalysedObject analysedObject = new AnalysedObject();
                    analysedObject = JsonUtility.FromJson<AnalysedObject>(jsonResponse);

                    if (analysedObject.tags == null)
                    {
                        Debug.Log("analysedObject.tagData is null");
                    }
                    else
                    {
                        Dictionary<string, float> tagsDictionary = new Dictionary<string, float>();

                        foreach (TagData td in analysedObject.tags)
                        {
                            TagData tag = td as TagData;
                            tagsDictionary.Add(tag.name, tag.confidence);                            
                        }

                        ResultsLabel.instance.SetTagsToLastLabel(tagsDictionary);
                    }
                }
                catch (Exception exception)
                {
                    Debug.Log("Json exception.Message: " + exception.Message);
                }

                yield return null;
            }
        }
    ```

    ```csharp
        /// <summary>
        /// Returns the contents of the specified file as a byte array.
        /// </summary>
        private static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
            BinaryReader binaryReader = new BinaryReader(fileStream);
            return binaryReader.ReadBytes((int)fileStream.Length);
        }  
    ```

9.  <span data-ttu-id="7de65-369">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="7de65-369">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>
10. <span data-ttu-id="7de65-370">Précédent dans l’éditeur Unity, cliquez et faites glisser le *VisionManager* et *ImageCapture* classes à partir de la **Scripts** dossier pour le **Main Camera**de l’objet dans le *hiérarchie panneau*.</span><span class="sxs-lookup"><span data-stu-id="7de65-370">Back in the Unity Editor, click and drag the *VisionManager* and *ImageCapture* classes from the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span> 

## <a name="chapter-8--before-building"></a><span data-ttu-id="7de65-371">Chapitre 8 – avant la génération</span><span class="sxs-lookup"><span data-stu-id="7de65-371">Chapter 8 – Before building</span></span>

<span data-ttu-id="7de65-372">Pour effectuer une analyse minutieuse de votre application vous en aurez besoin pour effectuer un chargement indépendant sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="7de65-372">To perform a thorough test of your application you will need to sideload it onto your HoloLens.</span></span>
<span data-ttu-id="7de65-373">Avant de procéder, assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="7de65-373">Before you do, ensure that:</span></span>

-   <span data-ttu-id="7de65-374">Tous les paramètres mentionnés dans [chapitre 2](#chapter-2--set-up-the-unity-project) sont correctement définies.</span><span class="sxs-lookup"><span data-stu-id="7de65-374">All the settings mentioned in [Chapter 2](#chapter-2--set-up-the-unity-project) are set correctly.</span></span> 
-   <span data-ttu-id="7de65-375">Tous les scripts sont attachés à la **Main Camera** objet.</span><span class="sxs-lookup"><span data-stu-id="7de65-375">All the scripts are attached to the **Main Camera** object.</span></span> 
-   <span data-ttu-id="7de65-376">Tous les champs dans le *panneau Inspecteur de caméra principal* sont affectées correctement.</span><span class="sxs-lookup"><span data-stu-id="7de65-376">All the fields in the *Main Camera Inspector Panel* are assigned properly.</span></span>
-   <span data-ttu-id="7de65-377">Assurez-vous que vous insérez votre **Auth Key** dans le **authorizationKey** variable.</span><span class="sxs-lookup"><span data-stu-id="7de65-377">Make sure you insert your **Auth Key** into the **authorizationKey** variable.</span></span>
-   <span data-ttu-id="7de65-378">Vérifiez que vous avez vérifié également votre point de terminaison votre *VisionManager* script et qu’il s’aligne sur *votre* région (ce document utilise *ouest des États-Unis-us* par défaut).</span><span class="sxs-lookup"><span data-stu-id="7de65-378">Ensure that you have also checked your endpoint in your *VisionManager* script, and that it aligns to *your* region (this document uses *west-us* by default).</span></span>

## <a name="chapter-9--build-the-uwp-solution-and-sideload-the-application"></a><span data-ttu-id="7de65-379">Chapitre 9 – générer la Solution de UWP et le chargement de version test, l’application</span><span class="sxs-lookup"><span data-stu-id="7de65-379">Chapter 9 – Build the UWP Solution and sideload the application</span></span>
<span data-ttu-id="7de65-380">Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée, il est temps de générer à partir de Unity.</span><span class="sxs-lookup"><span data-stu-id="7de65-380">Everything needed for the Unity section of this project has now been completed, so it is time to build it from Unity.</span></span>

1.  <span data-ttu-id="7de65-381">Accédez à *les paramètres de génération* - **fichier > Paramètres de Build...**</span><span class="sxs-lookup"><span data-stu-id="7de65-381">Navigate to *Build Settings* - **File > Build Settings…**</span></span>
2.  <span data-ttu-id="7de65-382">À partir de la *paramètres de Build* fenêtre, cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="7de65-382">From the *Build Settings* window, click **Build**.</span></span>

    ![Création de l’application à partir d’Unity](images/AzureLabs-Lab2-26.png)

3.  <span data-ttu-id="7de65-384">Si pas déjà fait, cochez **Unity C# projets**.</span><span class="sxs-lookup"><span data-stu-id="7de65-384">If not already, tick **Unity C# Projects**.</span></span>
4.  <span data-ttu-id="7de65-385">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="7de65-385">Click **Build**.</span></span> <span data-ttu-id="7de65-386">Unity lancera un *Explorateur de fichiers* fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans.</span><span class="sxs-lookup"><span data-stu-id="7de65-386">Unity will launch a *File Explorer* window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="7de65-387">Créez ce dossier, puis nommez-le *application*.</span><span class="sxs-lookup"><span data-stu-id="7de65-387">Create that folder now, and name it *App*.</span></span> <span data-ttu-id="7de65-388">Ensuite avec le *application* dossier sélectionné, appuyez sur **sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="7de65-388">Then with the *App* folder selected, press **Select Folder**.</span></span> 
5.  <span data-ttu-id="7de65-389">Unity commencera à générer votre projet pour le *application* dossier.</span><span class="sxs-lookup"><span data-stu-id="7de65-389">Unity will begin building your project to the *App* folder.</span></span> 
6.  <span data-ttu-id="7de65-390">Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un *Explorateur de fichiers* fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).</span><span class="sxs-lookup"><span data-stu-id="7de65-390">Once Unity has finished building (it might take some time), it will open a *File Explorer* window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

## <a name="chapter-10--deploy-to-hololens"></a><span data-ttu-id="7de65-391">Chapitre 10 – déployer sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="7de65-391">Chapter 10 – Deploy to HoloLens</span></span>

<span data-ttu-id="7de65-392">Pour déployer sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="7de65-392">To deploy on HoloLens:</span></span>

1.  <span data-ttu-id="7de65-393">Vous devez l’adresse IP de votre HoloLens (pour les déployer à distance) et pour vérifier que votre HoloLens est dans **Mode développeur**.</span><span class="sxs-lookup"><span data-stu-id="7de65-393">You will need the IP Address of your HoloLens (for Remote Deploy), and to ensure your HoloLens is in **Developer Mode**.</span></span> <span data-ttu-id="7de65-394">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="7de65-394">To do this:</span></span>

    1. <span data-ttu-id="7de65-395">Tout en portant vos HoloLens, ouvrez le **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="7de65-395">Whilst wearing your HoloLens, open the **Settings**.</span></span>
    2. <span data-ttu-id="7de65-396">Accédez à **réseau & Internet > Wi-Fi > Options avancées**</span><span class="sxs-lookup"><span data-stu-id="7de65-396">Go to **Network & Internet > Wi-Fi > Advanced Options**</span></span>
    3. <span data-ttu-id="7de65-397">Remarque la **IPv4** adresse.</span><span class="sxs-lookup"><span data-stu-id="7de65-397">Note the **IPv4** address.</span></span>
    4. <span data-ttu-id="7de65-398">Ensuite, accédez à **paramètres**, puis à **mise à jour & sécurité > pour les développeurs**</span><span class="sxs-lookup"><span data-stu-id="7de65-398">Next, navigate back to **Settings**, and then to **Update & Security > For Developers**</span></span> 
    5. <span data-ttu-id="7de65-399">Définir le Mode développeur.</span><span class="sxs-lookup"><span data-stu-id="7de65-399">Set Developer Mode On.</span></span>

2.  <span data-ttu-id="7de65-400">Accédez à votre nouvelle build Unity (le *application* dossier) et ouvrez le fichier solution avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="7de65-400">Navigate to your new Unity build (the *App* folder) and open the solution file with *Visual Studio*.</span></span>
3.  <span data-ttu-id="7de65-401">Dans, sélectionnez la Configuration de Solution **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="7de65-401">In the Solution Configuration select **Debug**.</span></span>
4.  <span data-ttu-id="7de65-402">Dans la plateforme de Solution, sélectionnez **x86**, **Machine distante**.</span><span class="sxs-lookup"><span data-stu-id="7de65-402">In the Solution Platform, select **x86**, **Remote Machine**.</span></span> 

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab2-27.png)
 
5.  <span data-ttu-id="7de65-404">Accédez à la **menu Générer** , puis cliquez sur **déployer la Solution**, chargement de version test l’application à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="7de65-404">Go to the **Build menu** and click on **Deploy Solution**, to sideload the application to your HoloLens.</span></span>
6.  <span data-ttu-id="7de65-405">Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prêt à être lancé !</span><span class="sxs-lookup"><span data-stu-id="7de65-405">Your App should now appear in the list of installed apps on your HoloLens, ready to be launched!</span></span>

> [!NOTE]
> <span data-ttu-id="7de65-406">Pour déployer sur casque immersif, définissez le **plateforme de Solution** à *ordinateur Local*et définissez le **Configuration** à *déboguer*, avec *x86* en tant que le **plateforme**.</span><span class="sxs-lookup"><span data-stu-id="7de65-406">To deploy to immersive headset, set the **Solution Platform** to *Local Machine*, and set the **Configuration** to *Debug*, with *x86* as the **Platform**.</span></span> <span data-ttu-id="7de65-407">Déployer sur l’ordinateur local d’ordinateur, à l’aide de la **menu Générer**, en sélectionnant *déployer la Solution*.</span><span class="sxs-lookup"><span data-stu-id="7de65-407">Then deploy to the local machine, using the **Build menu**, selecting *Deploy Solution*.</span></span> 

## <a name="your-finished-computer-vision-api-application"></a><span data-ttu-id="7de65-408">Votre application API vision par ordinateur terminée</span><span class="sxs-lookup"><span data-stu-id="7de65-408">Your finished Computer Vision API application</span></span>

<span data-ttu-id="7de65-409">Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’API de vision par ordinateur Azure pour reconnaître des objets du monde réel et afficher le niveau de confiance de ce qui a été vu.</span><span class="sxs-lookup"><span data-stu-id="7de65-409">Congratulations, you built a mixed reality app that leverages the Azure Computer Vision API to recognize real world objects, and display confidence of what has been seen.</span></span>

![résultat de laboratoire](images/AzureLabs-Lab2-000.png)

## <a name="bonus-exercises"></a><span data-ttu-id="7de65-411">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="7de65-411">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="7de65-412">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="7de65-412">Exercise 1</span></span>

<span data-ttu-id="7de65-413">Tout comme vous avez utilisé le *balises* paramètre (comme le démontre au sein de la *point de terminaison* utilisé dans le *VisionManager*), étendre l’application pour détecter d’autres informations ; un œil à les autres paramètres que vous avez accès à [ici](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa).</span><span class="sxs-lookup"><span data-stu-id="7de65-413">Just as you have used the *Tags* parameter (as evidenced within the *endpoint* used within the *VisionManager*), extend the app to detect other information; have a look at what other parameters you have access to [HERE](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa).</span></span>

### <a name="exercise-2"></a><span data-ttu-id="7de65-414">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="7de65-414">Exercise 2</span></span>

<span data-ttu-id="7de65-415">Afficher les données retournées Azure, de façon plus CONVERSATIONNELLE et lisible, peut-être masquer les numéros de.</span><span class="sxs-lookup"><span data-stu-id="7de65-415">Display the returned Azure data, in a more conversational, and readable way, perhaps hiding the numbers.</span></span> <span data-ttu-id="7de65-416">Comme si un robot peut-être parler à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7de65-416">As though a bot might be speaking to the user.</span></span>
