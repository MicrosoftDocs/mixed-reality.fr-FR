---
title: MR et Azure 302-vision par ordinateur
description: Suivez ce cours pour apprendre à reconnaître le contenu visuel dans une image fournie, à l’aide d’Azure Vision par ordinateur dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, vision par ordinateur, hololens, immersif, VR
ms.openlocfilehash: d6f792a67adfd1038ca4cdbc44b2ef1bf12a1173
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437947"
---
>[!NOTE]
><span data-ttu-id="988a4-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="988a4-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="988a4-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="988a4-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="988a4-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="988a4-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="988a4-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="988a4-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="988a4-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="988a4-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="988a4-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="988a4-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-and-azure-302-computer-vision"></a><span data-ttu-id="988a4-110">MR et Azure 302 : vision par ordinateur</span><span class="sxs-lookup"><span data-stu-id="988a4-110">MR and Azure 302: Computer vision</span></span>

<span data-ttu-id="988a4-111">Dans ce cours, vous allez apprendre à reconnaître du contenu visuel dans une image fournie, à l’aide des fonctionnalités d’Azure Vision par ordinateur dans une application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="988a4-111">In this course, you will learn how to recognize visual content within a provided image, using Azure Computer Vision capabilities in a mixed reality application.</span></span>

<span data-ttu-id="988a4-112">Les résultats de la reconnaissance s’affichent sous forme de balises descriptives.</span><span class="sxs-lookup"><span data-stu-id="988a4-112">Recognition results will be displayed as descriptive tags.</span></span> <span data-ttu-id="988a4-113">Vous pouvez utiliser ce service sans avoir à former un modèle de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="988a4-113">You can use this service without needing to train a machine learning model.</span></span> <span data-ttu-id="988a4-114">Si votre implémentation nécessite l’apprentissage d’un modèle de Machine Learning, consultez [Mr et Azure 302b](mr-azure-302b.md).</span><span class="sxs-lookup"><span data-stu-id="988a4-114">If your implementation requires training a machine learning model, see [MR and Azure 302b](mr-azure-302b.md).</span></span>

![résultat de l’atelier](images/AzureLabs-Lab2-000.png)

<span data-ttu-id="988a4-116">Le Vision par ordinateur Microsoft est un ensemble d’API conçu pour fournir aux développeurs un traitement et une analyse d’image (avec des informations de retour), à l’aide d’algorithmes avancés, le tout à partir du Cloud.</span><span class="sxs-lookup"><span data-stu-id="988a4-116">The Microsoft Computer Vision is a set of APIs designed to provide developers with image processing and analysis (with return information), using advanced algorithms, all from the cloud.</span></span> <span data-ttu-id="988a4-117">Les développeurs téléchargent une URL d’image ou d’image, et les algorithmes de API Vision par ordinateur Microsoft analysent le contenu visuel, en fonction des entrées choisies par l’utilisateur, qui peuvent ensuite retourner des informations, notamment, identifier le type et la qualité d’une image, détecter les visages humains ( retour de leurs coordonnées) et balisage, ou catégorisation d’images.</span><span class="sxs-lookup"><span data-stu-id="988a4-117">Developers upload an image or image URL, and the Microsoft Computer Vision API algorithms analyze the visual content, based upon inputs chosen the user, which then can return information, including, identifying the type and quality of an image, detect human faces (returning their coordinates), and tagging, or categorizing images.</span></span> <span data-ttu-id="988a4-118">Pour plus d’informations, consultez la [page API vision par ordinateur Azure](https://azure.microsoft.com/services/cognitive-services/computer-vision/).</span><span class="sxs-lookup"><span data-stu-id="988a4-118">For more information, visit the [Azure Computer Vision API page](https://azure.microsoft.com/services/cognitive-services/computer-vision/).</span></span>

<span data-ttu-id="988a4-119">Une fois ce cours terminé, vous disposerez d’une application HoloLens de réalité mixte, qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="988a4-119">Having completed this course, you will have a mixed reality HoloLens application, which will be able to do the following:</span></span>

1.  <span data-ttu-id="988a4-120">À l’aide du mouvement TAP, l’appareil photo de HoloLens capture une image.</span><span class="sxs-lookup"><span data-stu-id="988a4-120">Using the Tap gesture, the camera of the HoloLens will capture an image.</span></span>
2.  <span data-ttu-id="988a4-121">L’image sera envoyée au service Azure API Vision par ordinateur.</span><span class="sxs-lookup"><span data-stu-id="988a4-121">The image will be sent to the Azure Computer Vision API Service.</span></span> 
3.  <span data-ttu-id="988a4-122">Les objets reconnus seront listés dans un groupe d’interface utilisateur simple positionné dans la scène Unity.</span><span class="sxs-lookup"><span data-stu-id="988a4-122">The objects recognized will be listed in a simple UI group positioned in the Unity Scene.</span></span>

<span data-ttu-id="988a4-123">Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception.</span><span class="sxs-lookup"><span data-stu-id="988a4-123">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="988a4-124">Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="988a4-124">This course is designed to teach you how to integrate an Azure Service with your Unity project.</span></span> <span data-ttu-id="988a4-125">C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="988a4-125">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

## <a name="device-support"></a><span data-ttu-id="988a4-126">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="988a4-126">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="988a4-127">Course</span><span class="sxs-lookup"><span data-stu-id="988a4-127">Course</span></span></th><th style="width:150px"> <span data-ttu-id="988a4-128"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="988a4-128"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="988a4-129"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="988a4-129"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="988a4-130">MR et Azure 302 : vision par ordinateur</span><span class="sxs-lookup"><span data-stu-id="988a4-130">MR and Azure 302: Computer vision</span></span></td><td style="text-align: center;"> <span data-ttu-id="988a4-131">✔️</span><span class="sxs-lookup"><span data-stu-id="988a4-131">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="988a4-132">✔️</span><span class="sxs-lookup"><span data-stu-id="988a4-132">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="988a4-133">Bien que ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques pour Windows Mixed Reality (VR).</span><span class="sxs-lookup"><span data-stu-id="988a4-133">While this course primarily focuses on HoloLens, you can also apply what you learn in this course to Windows Mixed Reality immersive (VR) headsets.</span></span> <span data-ttu-id="988a4-134">Étant donné que les casques immersifs ne disposent pas de caméras accessibles, vous aurez besoin d’une caméra externe connectée à votre PC.</span><span class="sxs-lookup"><span data-stu-id="988a4-134">Because immersive (VR) headsets do not have accessible cameras, you will need an external camera connected to your PC.</span></span> <span data-ttu-id="988a4-135">À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge les écouteurs immersifs (VR).</span><span class="sxs-lookup"><span data-stu-id="988a4-135">As you follow along with the course, you will see notes on any changes you might need to employ to support immersive (VR) headsets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="988a4-136">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="988a4-136">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="988a4-137">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="988a4-137">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="988a4-138">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="988a4-138">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="988a4-139">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="988a4-139">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="988a4-140">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours :</span><span class="sxs-lookup"><span data-stu-id="988a4-140">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="988a4-141">Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)</span><span class="sxs-lookup"><span data-stu-id="988a4-141">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="988a4-142">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="988a4-142">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="988a4-143">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="988a4-143">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="988a4-144">Unity 2017,4</span><span class="sxs-lookup"><span data-stu-id="988a4-144">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="988a4-145">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="988a4-145">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="988a4-146">Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="988a4-146">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="988a4-147">Appareil photo connecté à votre PC (pour le développement d’un casque immersif)</span><span class="sxs-lookup"><span data-stu-id="988a4-147">A camera connected to your PC (for immersive headset development)</span></span>
- <span data-ttu-id="988a4-148">Accès à Internet pour l’installation d’Azure et la récupération de API Vision par ordinateur</span><span class="sxs-lookup"><span data-stu-id="988a4-148">Internet access for Azure setup and Computer Vision API retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="988a4-149">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="988a4-149">Before you start</span></span>

1.  <span data-ttu-id="988a4-150">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="988a4-150">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="988a4-151">Configurez et testez votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="988a4-151">Set up and test your HoloLens.</span></span> <span data-ttu-id="988a4-152">Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="988a4-152">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span> 
3.  <span data-ttu-id="988a4-153">Il est judicieux d’effectuer un réglage de l’étalonnage et du capteur au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="988a4-153">It is a good idea to perform Calibration and Sensor Tuning when beginning developing a new HoloLens App (sometimes it can help to perform those tasks for each user).</span></span> 

<span data-ttu-id="988a4-154">Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens-2).</span><span class="sxs-lookup"><span data-stu-id="988a4-154">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens-2).</span></span>

<span data-ttu-id="988a4-155">Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="988a4-155">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

## <a name="chapter-1--the-azure-portal"></a><span data-ttu-id="988a4-156">Chapitre 1 – portail Azure</span><span class="sxs-lookup"><span data-stu-id="988a4-156">Chapter 1 – The Azure Portal</span></span>

<span data-ttu-id="988a4-157">Pour utiliser le service de *API vision par ordinateur* dans Azure, vous devez configurer une instance du service qui sera mise à la disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="988a4-157">To use the *Computer Vision API* service in Azure, you will need to configure an instance of the service to be made available to your application.</span></span>

1.  <span data-ttu-id="988a4-158">Tout d’abord, connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="988a4-158">First, log in to the [Azure Portal](https://portal.azure.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="988a4-159">Si vous n’avez pas encore de compte Azure, vous devez en créer un.</span><span class="sxs-lookup"><span data-stu-id="988a4-159">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="988a4-160">Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="988a4-160">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="988a4-161">Une fois que vous êtes connecté, cliquez sur **nouveau** dans l’angle supérieur gauche, recherchez *API vision par ordinateur*, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="988a4-161">Once you are logged in, click on **New** in the top left corner, and search for *Computer Vision API*, and click **Enter**.</span></span>

    ![Créer une ressource dans Azure](images/AzureLabs-Lab2-00.png)

    > [!NOTE]
    > <span data-ttu-id="988a4-163">Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.</span><span class="sxs-lookup"><span data-stu-id="988a4-163">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>
 
3.  <span data-ttu-id="988a4-164">La nouvelle page fournit une description du service *API vision par ordinateur* .</span><span class="sxs-lookup"><span data-stu-id="988a4-164">The new page will provide a description of the *Computer Vision API* service.</span></span> <span data-ttu-id="988a4-165">En bas à gauche de cette page, cliquez sur le bouton **créer** pour créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="988a4-165">At the bottom left of this page, select the **Create** button, to create an association with this service.</span></span>

    ![À propos du service d’API vision par ordinateur](images/AzureLabs-Lab2-01.png)
 
4.  <span data-ttu-id="988a4-167">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="988a4-167">Once you have clicked on **Create**:</span></span>

    1. <span data-ttu-id="988a4-168">Insérez le **nom** de votre choix pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="988a4-168">Insert your desired **Name** for this service instance.</span></span>
    2. <span data-ttu-id="988a4-169">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="988a4-169">Select a **Subscription**.</span></span>
    3. <span data-ttu-id="988a4-170">Sélectionnez le **niveau tarifaire** approprié, s’il s’agit de la première fois que vous créez un service *API vision par ordinateur* , vous devez disposer d’un niveau gratuit (nommé F0).</span><span class="sxs-lookup"><span data-stu-id="988a4-170">Select the **Pricing Tier** appropriate for you, if this is the first time creating a *Computer Vision API* Service, a free tier (named F0) should be available to you.</span></span>
    4. <span data-ttu-id="988a4-171">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="988a4-171">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="988a4-172">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="988a4-172">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="988a4-173">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun).</span><span class="sxs-lookup"><span data-stu-id="988a4-173">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span> 

        > <span data-ttu-id="988a4-174">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="988a4-174">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5. <span data-ttu-id="988a4-175">Déterminez l’emplacement de votre groupe de ressources (si vous créez un groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="988a4-175">Determine the Location for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="988a4-176">L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait.</span><span class="sxs-lookup"><span data-stu-id="988a4-176">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="988a4-177">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="988a4-177">Some Azure assets are only available in certain regions.</span></span>

    6. <span data-ttu-id="988a4-178">Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.</span><span class="sxs-lookup"><span data-stu-id="988a4-178">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>
    7. <span data-ttu-id="988a4-179">Cliquez sur créer.</span><span class="sxs-lookup"><span data-stu-id="988a4-179">Click Create.</span></span>

        ![Informations sur la création du service](images/AzureLabs-Lab2-02.png)

5.  <span data-ttu-id="988a4-181">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="988a4-181">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>
6.  <span data-ttu-id="988a4-182">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="988a4-182">A notification will appear in the portal once the Service instance is created.</span></span>

    ![Consultez la nouvelle notification pour votre nouveau service](images/AzureLabs-Lab2-03.png) 
 
7.  <span data-ttu-id="988a4-184">Cliquez sur la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="988a4-184">Click on the notification to explore your new Service instance.</span></span> 

    ![Sélectionnez le bouton atteindre la ressource.](images/AzureLabs-Lab2-04.png)
 
8. <span data-ttu-id="988a4-186">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="988a4-186">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="988a4-187">Vous êtes dirigé vers votre nouvelle instance de service API Vision par ordinateur.</span><span class="sxs-lookup"><span data-stu-id="988a4-187">You will be taken to your new Computer Vision API service instance.</span></span> 

    ![Votre nouveau service API Vision par ordinateur](images/AzureLabs-Lab2-05.png)
 
9.  <span data-ttu-id="988a4-189">Dans ce didacticiel, votre application doit effectuer des appels à votre service, à l’aide de la clé d’abonnement de votre service.</span><span class="sxs-lookup"><span data-stu-id="988a4-189">Within this tutorial, your application will need to make calls to your service, which is done through using your service’s Subscription Key.</span></span>
10. <span data-ttu-id="988a4-190">Dans la page *démarrage rapide* de votre service *API vision par ordinateur* , accédez à la première étape, *saisissez vos clés*, puis cliquez sur **clés** (vous pouvez également y parvenir en cliquant sur les touches de lien bleu, situées dans le menu de navigation services, indiqué par l’icône de clé).</span><span class="sxs-lookup"><span data-stu-id="988a4-190">From the *Quick start* page, of your *Computer Vision API* service, navigate to the first step, *Grab your keys*, and click **Keys** (you can also achieve this by clicking the blue hyperlink Keys, located in the services navigation menu, denoted by the key icon).</span></span> <span data-ttu-id="988a4-191">Cela permet de révéler vos *clés*de service.</span><span class="sxs-lookup"><span data-stu-id="988a4-191">This will reveal your service *Keys*.</span></span>
11. <span data-ttu-id="988a4-192">Prenez une copie de l’une des clés affichées, car vous en aurez besoin plus tard dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="988a4-192">Take a copy of one of the displayed keys, as you will need this later in your project.</span></span> 

12. <span data-ttu-id="988a4-193">Revenez à la page de *démarrage rapide* et, à partir de là, récupérez votre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="988a4-193">Go back to the *Quick start* page, and from there, fetch your endpoint.</span></span> <span data-ttu-id="988a4-194">N’oubliez pas que la vôtre peut être différente, en fonction de votre région (si c’est le cas, vous devrez apporter une modification à votre code ultérieurement).</span><span class="sxs-lookup"><span data-stu-id="988a4-194">Be aware yours may be different, depending on your region (which if it is, you will need to make a change to your code later).</span></span> <span data-ttu-id="988a4-195">Prendre une copie de ce point de terminaison pour une utilisation ultérieure :</span><span class="sxs-lookup"><span data-stu-id="988a4-195">Take a copy of this endpoint for use later:</span></span>

    ![Votre nouveau service API Vision par ordinateur](images/AzureLabs-Lab2-05-5.png)

    > [!TIP]
    > <span data-ttu-id="988a4-197">Vous pouvez vérifier les différents points de terminaison [ici](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa).</span><span class="sxs-lookup"><span data-stu-id="988a4-197">You can check what the various endpoints are [HERE](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa).</span></span> 

## <a name="chapter-2--set-up-the-unity-project"></a><span data-ttu-id="988a4-198">Chapitre 2 : configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="988a4-198">Chapter 2 – Set up the Unity project</span></span>

<span data-ttu-id="988a4-199">Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="988a4-199">The following is a typical set up for developing with mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="988a4-200">Ouvrez *Unity* et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="988a4-200">Open *Unity* and click **New**.</span></span> 

    ![Démarrez le nouveau projet Unity.](images/AzureLabs-Lab2-06.png)

2.  <span data-ttu-id="988a4-202">Vous devez maintenant fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="988a4-202">You will now need to provide a Unity Project name.</span></span> <span data-ttu-id="988a4-203">Insérez **MR_ComputerVision**.</span><span class="sxs-lookup"><span data-stu-id="988a4-203">Insert **MR_ComputerVision**.</span></span> <span data-ttu-id="988a4-204">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="988a4-204">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="988a4-205">Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés).</span><span class="sxs-lookup"><span data-stu-id="988a4-205">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="988a4-206">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="988a4-206">Then, click **Create project**.</span></span>

    ![Fournissez des détails pour le nouveau projet Unity.](images/AzureLabs-Lab2-07.png)

3.  <span data-ttu-id="988a4-208">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="988a4-208">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="988a4-209">Accédez à **modifier > préférences** puis, dans la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="988a4-209">Go to **Edit > Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="988a4-210">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="988a4-210">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="988a4-211">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="988a4-211">Close the **Preferences** window.</span></span>

    ![Mettre à jour la préférence éditeur de script.](images/AzureLabs-Lab2-08.png)

4.  <span data-ttu-id="988a4-213">Accédez ensuite à **fichier > paramètres de build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le bouton **changer de plateforme** pour appliquer votre sélection.</span><span class="sxs-lookup"><span data-stu-id="988a4-213">Next, go to **File > Build Settings** and select **Universal Windows Platform**, then click on the **Switch Platform** button to apply your selection.</span></span>

    ![Fenêtre Paramètres de build, basculez plateforme vers UWP.](images/AzureLabs-Lab2-10.png)

5.  <span data-ttu-id="988a4-215">Tout en conservant les **paramètres de génération de > de fichiers** et assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="988a4-215">While still in **File > Build Settings** and make sure that:</span></span>

    1. <span data-ttu-id="988a4-216">L' **appareil cible** est défini sur **HoloLens**</span><span class="sxs-lookup"><span data-stu-id="988a4-216">**Target Device** is set to **HoloLens**</span></span>

        > <span data-ttu-id="988a4-217">Pour les casques immersifs, définissez **appareil cible** sur *n’importe quel appareil*.</span><span class="sxs-lookup"><span data-stu-id="988a4-217">For the immersive headsets, set **Target Device** to *Any Device*.</span></span>

    2. <span data-ttu-id="988a4-218">Le **type de build** est **D3D**</span><span class="sxs-lookup"><span data-stu-id="988a4-218">**Build Type** is set to **D3D**</span></span>
    3. <span data-ttu-id="988a4-219">Le **SDK** est configuré sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="988a4-219">**SDK** is set to **Latest installed**</span></span>
    4. <span data-ttu-id="988a4-220">**Version de Visual Studio** définie sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="988a4-220">**Visual Studio Version** is set to **Latest installed**</span></span>
    5. <span data-ttu-id="988a4-221">La **génération et l’exécution** sont définies sur l' **ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="988a4-221">**Build and Run** is set to **Local Machine**</span></span>
    6. <span data-ttu-id="988a4-222">Enregistrez la scène et ajoutez-la à la Build.</span><span class="sxs-lookup"><span data-stu-id="988a4-222">Save the scene and add it to the build.</span></span>

        1. <span data-ttu-id="988a4-223">Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="988a4-223">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="988a4-224">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="988a4-224">A save window will appear.</span></span>
        
            ![Cliquez sur le bouton Ajouter des scènes ouvertes](images/AzureLabs-Lab2-11.png)

        2. <span data-ttu-id="988a4-226">Créez un dossier pour cela, ainsi que toute nouvelle scène, puis sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez-le **scenes**.</span><span class="sxs-lookup"><span data-stu-id="988a4-226">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![Créer un dossier de scripts](images/AzureLabs-Lab2-12.png)

        3. <span data-ttu-id="988a4-228">Ouvrez le dossier **scenes** nouvellement créé, puis dans le champ *nom de fichier*:, tapez **MR_ComputerVisionScene**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="988a4-228">Open your newly created **Scenes** folder, and then in the *File name*: text field, type **MR_ComputerVisionScene**, then click **Save**.</span></span>

            ![Donnez un nom à la nouvelle scène.](images/AzureLabs-Lab2-13.png)

            > <span data-ttu-id="988a4-230">Sachez que vous devez enregistrer vos scènes Unity dans le dossier *ressources* , car elles doivent être associées au projet Unity.</span><span class="sxs-lookup"><span data-stu-id="988a4-230">Be aware, you must save your Unity scenes within the *Assets* folder, as they must be associated with the Unity Project.</span></span> <span data-ttu-id="988a4-231">La création du dossier scenes (et d’autres dossiers similaires) est un moyen classique de structurer un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="988a4-231">Creating the scenes folder (and other similar folders) is a typical way of structuring a Unity project.</span></span>

    7. <span data-ttu-id="988a4-232">Les paramètres restants, dans *paramètres de build*, doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="988a4-232">The remaining settings, in *Build Settings*, should be left as default for now.</span></span>

6. <span data-ttu-id="988a4-233">Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* .</span><span class="sxs-lookup"><span data-stu-id="988a4-233">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span> 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab2-14.png)

7. <span data-ttu-id="988a4-235">Dans ce volet, quelques paramètres doivent être vérifiés :</span><span class="sxs-lookup"><span data-stu-id="988a4-235">In this panel, a few settings need to be verified:</span></span>

    1. <span data-ttu-id="988a4-236">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="988a4-236">In the **Other Settings** tab:</span></span>

        1. <span data-ttu-id="988a4-237">La **version du runtime de script** doit être **stable** (équivalent .net 3,5).</span><span class="sxs-lookup"><span data-stu-id="988a4-237">**Scripting Runtime Version** should be **Stable** (.NET 3.5 Equivalent).</span></span>
        2. <span data-ttu-id="988a4-238">Le **backend de script** doit être **.net**</span><span class="sxs-lookup"><span data-stu-id="988a4-238">**Scripting Backend** should be **.NET**</span></span>
        3. <span data-ttu-id="988a4-239">Le **niveau de compatibilité** de l’API doit être **.net 4,6**</span><span class="sxs-lookup"><span data-stu-id="988a4-239">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![Mettez à jour d’autres paramètres.](images/AzureLabs-Lab2-15.png)
      
    2. <span data-ttu-id="988a4-241">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher :</span><span class="sxs-lookup"><span data-stu-id="988a4-241">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        1. <span data-ttu-id="988a4-242">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="988a4-242">**InternetClient**</span></span>
        2. <span data-ttu-id="988a4-243">**Webcam**</span><span class="sxs-lookup"><span data-stu-id="988a4-243">**Webcam**</span></span>

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab2-16.png)

    3. <span data-ttu-id="988a4-245">Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="988a4-245">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Mettez à jour les paramètres X R.](images/AzureLabs-Lab2-17.png)

8.  <span data-ttu-id="988a4-247">De retour dans les *paramètres de build* , les projets _Unity C#_  ne sont plus grisés. Cochez la case en regard de cette option.</span><span class="sxs-lookup"><span data-stu-id="988a4-247">Back in *Build Settings* _Unity C#_ Projects is no longer greyed out; tick the checkbox next to this.</span></span> 
9.  <span data-ttu-id="988a4-248">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="988a4-248">Close the Build Settings window.</span></span>
10. <span data-ttu-id="988a4-249">Enregistrez votre scène et votre projet (**fichier > enregistrer la scène/le fichier > enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="988a4-249">Save your Scene and Project (**FILE > SAVE SCENE / FILE > SAVE PROJECT**).</span></span>

## <a name="chapter-3--main-camera-setup"></a><span data-ttu-id="988a4-250">Chapitre 3 – Configuration de l’appareil photo principal</span><span class="sxs-lookup"><span data-stu-id="988a4-250">Chapter 3 – Main Camera setup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="988a4-251">Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce fichier [. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302%20-%20Computer%20vision/Azure-MR-302.unitypackage), à l’importer dans votre projet en tant que [package personnalisé](https://docs.unity3d.com/Manual/AssetPackages.html), puis à passer au [Chapitre 5](#chapter-5--create-the-resultslabel-class).</span><span class="sxs-lookup"><span data-stu-id="988a4-251">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to download this [.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302%20-%20Computer%20vision/Azure-MR-302.unitypackage), import it into your project as a [Custom Package](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 5](#chapter-5--create-the-resultslabel-class).</span></span>

1.  <span data-ttu-id="988a4-252">Dans le *panneau hiérarchie*, sélectionnez l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="988a4-252">In the *Hierarchy Panel*, select the **Main Camera**.</span></span> 
2.  <span data-ttu-id="988a4-253">Une fois sélectionné, vous pouvez voir tous les composants de la **caméra principale** dans le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="988a4-253">Once selected, you will be able to see all the components of the **Main Camera** in the *Inspector Panel*.</span></span>

    1. <span data-ttu-id="988a4-254">L' **objet Camera** doit être nommé **Camera main** (Notez l’orthographe !)</span><span class="sxs-lookup"><span data-stu-id="988a4-254">The **Camera object** must be named **Main Camera** (note the spelling!)</span></span>
    2. <span data-ttu-id="988a4-255">La **balise** principale de l’appareil photo doit être définie sur **MainCamera** (Notez l’orthographe !)</span><span class="sxs-lookup"><span data-stu-id="988a4-255">The Main Camera **Tag** must be set to **MainCamera** (note the spelling!)</span></span>
    3. <span data-ttu-id="988a4-256">Vérifiez que la **position** de la transformation est définie sur **0, 0,** 0</span><span class="sxs-lookup"><span data-stu-id="988a4-256">Make sure the **Transform Position** is set to **0, 0, 0**</span></span>
    4. <span data-ttu-id="988a4-257">Affectez à **effacer les indicateurs** la **couleur unie** (ignorer ce point pour le casque immersif).</span><span class="sxs-lookup"><span data-stu-id="988a4-257">Set **Clear Flags** to **Solid Color** (ignore this for immersive headset).</span></span>
    5. <span data-ttu-id="988a4-258">Définissez la couleur d' **arrière-plan** du composant Camera sur **Black, alpha 0 (Code hex : #00000000)** (ignorez-le pour le casque immersif).</span><span class="sxs-lookup"><span data-stu-id="988a4-258">Set the **Background** Color of the Camera Component to **Black, Alpha 0 (Hex Code: #00000000)** (ignore this for immersive headset).</span></span>

        ![Mettez à jour les composants de l’appareil photo.](images/AzureLabs-Lab2-18.png)
 
3.  <span data-ttu-id="988a4-260">Ensuite, vous devez créer un objet « Cursor » simple attaché à l' **appareil photo principal**, ce qui vous aidera à positionner la sortie de l’analyse d’image lorsque l’application est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="988a4-260">Next, you will have to create a simple “Cursor” object attached to the **Main Camera**, which will help you position the image analysis output when the application is running.</span></span> <span data-ttu-id="988a4-261">Ce curseur détermine le point central du focus de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="988a4-261">This Cursor will determine the center point of the camera focus.</span></span>

<span data-ttu-id="988a4-262">Pour créer le curseur :</span><span class="sxs-lookup"><span data-stu-id="988a4-262">To create the Cursor:</span></span>

1.  <span data-ttu-id="988a4-263">Dans le *panneau hiérarchie*, cliquez avec le bouton droit sur l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="988a4-263">In the *Hierarchy Panel*, right-click on the **Main Camera**.</span></span> <span data-ttu-id="988a4-264">Sous **objet 3D**, cliquez sur **sphère**.</span><span class="sxs-lookup"><span data-stu-id="988a4-264">Under **3D Object**, click on **Sphere**.</span></span>

    ![Sélectionnez l’objet curseur.](images/AzureLabs-Lab2-19.png)
 
2.  <span data-ttu-id="988a4-266">Renommez la **sphère** en **curseur** (double-cliquez sur l’objet curseur ou appuyez sur le bouton clavier F2 avec l’objet sélectionné) et vérifiez qu’il est situé en tant qu’enfant de l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="988a4-266">Rename the **Sphere** to **Cursor** (double click the Cursor object or press the ‘F2’ keyboard button with the object selected), and make sure it is located as child of the **Main Camera**.</span></span>

3.  <span data-ttu-id="988a4-267">Dans le *volet*de la hiérarchie, cliquez sur le **curseur**à gauche.</span><span class="sxs-lookup"><span data-stu-id="988a4-267">In the *Hierarchy Panel*, left click on the **Cursor**.</span></span> <span data-ttu-id="988a4-268">Après avoir sélectionné le curseur, ajustez les variables suivantes dans le *panneau Inspecteur*:</span><span class="sxs-lookup"><span data-stu-id="988a4-268">With the Cursor selected, adjust the following variables in the *Inspector Panel*:</span></span>

    1. <span data-ttu-id="988a4-269">Définir la *position* de la transformation sur **0, 0,5**</span><span class="sxs-lookup"><span data-stu-id="988a4-269">Set the *Transform Position* to **0, 0, 5**</span></span>
    2. <span data-ttu-id="988a4-270">Définir l' *échelle* sur **0,02, 0,02, 0,02**</span><span class="sxs-lookup"><span data-stu-id="988a4-270">Set the *Scale* to **0.02, 0.02, 0.02**</span></span>

        ![Mettez à jour la position et l’échelle de la transformation.](images/AzureLabs-Lab2-20.png)
  
## <a name="chapter-4--setup-the-label-system"></a><span data-ttu-id="988a4-272">Chapitre 4-configurer le système d’étiquette</span><span class="sxs-lookup"><span data-stu-id="988a4-272">Chapter 4 – Setup the Label system</span></span>

<span data-ttu-id="988a4-273">Une fois que vous avez capturé une image à l’aide de la caméra HoloLens, cette image est envoyée à votre instance *Azure API vision par ordinateur* service à des fins d’analyse.</span><span class="sxs-lookup"><span data-stu-id="988a4-273">Once you have captured an image with the HoloLens’ camera, that image will be sent to your *Azure Computer Vision API* Service instance for analysis.</span></span> 

<span data-ttu-id="988a4-274">Les résultats de cette analyse seront une liste d’objets reconnus appelés **balises**.</span><span class="sxs-lookup"><span data-stu-id="988a4-274">The results of that analysis will be a list of recognized objects called **Tags**.</span></span> 

<span data-ttu-id="988a4-275">Vous allez utiliser des étiquettes (comme du texte 3D dans l’espace universel) pour afficher ces balises à l’emplacement où la photo a été prise.</span><span class="sxs-lookup"><span data-stu-id="988a4-275">You will use Labels (as a 3D text in world space) to display these Tags at the location the photo was taken.</span></span>

<span data-ttu-id="988a4-276">Les étapes suivantes montrent comment configurer l’objet **label** .</span><span class="sxs-lookup"><span data-stu-id="988a4-276">The following steps will show how to setup the **Label** object.</span></span>

1.  <span data-ttu-id="988a4-277">Cliquez avec le bouton droit n’importe où dans le volet de la hiérarchie (l’emplacement n’a pas d’importance à ce stade), sous **objet 3D**, ajoutez un **texte 3D**.</span><span class="sxs-lookup"><span data-stu-id="988a4-277">Right-click anywhere in the Hierarchy Panel (the location does not matter at this point), under **3D Object**, add a **3D Text**.</span></span> <span data-ttu-id="988a4-278">Nommez-le **LabelText**.</span><span class="sxs-lookup"><span data-stu-id="988a4-278">Name it **LabelText**.</span></span>

    ![Créez un objet de texte 3D.](images/AzureLabs-Lab2-21.png)
 
2.  <span data-ttu-id="988a4-280">Dans le *volet*de la hiérarchie, cliquez sur le **LabelText**.</span><span class="sxs-lookup"><span data-stu-id="988a4-280">In the *Hierarchy Panel*, left click on the **LabelText**.</span></span> <span data-ttu-id="988a4-281">Une fois le **LabelText** sélectionné, ajustez les variables suivantes dans le *panneau Inspecteur*:</span><span class="sxs-lookup"><span data-stu-id="988a4-281">With the **LabelText** selected, adjust the following variables in the *Inspector Panel*:</span></span>

    1. <span data-ttu-id="988a4-282">Définir la **position** sur **0, 0, 0**</span><span class="sxs-lookup"><span data-stu-id="988a4-282">Set the **Position** to **0,0,0**</span></span>
    2. <span data-ttu-id="988a4-283">Définir l' **échelle** sur **0,01, 0,01, 0,01**</span><span class="sxs-lookup"><span data-stu-id="988a4-283">Set the **Scale** to **0.01, 0.01, 0.01**</span></span>
    3. <span data-ttu-id="988a4-284">Dans la **maille du texte**du composant :</span><span class="sxs-lookup"><span data-stu-id="988a4-284">In the component **Text Mesh**:</span></span>
    4. <span data-ttu-id="988a4-285">Remplacer tout le texte dans le **texte**par « ... »</span><span class="sxs-lookup"><span data-stu-id="988a4-285">Replace all the text within **Text**, with "..."</span></span>        
    5. <span data-ttu-id="988a4-286">Définir le **point d’ancrage** au **milieu** central</span><span class="sxs-lookup"><span data-stu-id="988a4-286">Set the **Anchor** to **Middle Center**</span></span>
    6. <span data-ttu-id="988a4-287">Définir l' **alignement** sur **Center**</span><span class="sxs-lookup"><span data-stu-id="988a4-287">Set the **Alignment** to **Center**</span></span>
    7. <span data-ttu-id="988a4-288">Définir la **taille des tabulations** sur **4**</span><span class="sxs-lookup"><span data-stu-id="988a4-288">Set the **Tab Size** to **4**</span></span>
    8. <span data-ttu-id="988a4-289">Définir la **taille** de la police sur **50**</span><span class="sxs-lookup"><span data-stu-id="988a4-289">Set the **Font Size** to **50**</span></span>
    9. <span data-ttu-id="988a4-290">Définir la **couleur** sur **#FFFFFFFF**</span><span class="sxs-lookup"><span data-stu-id="988a4-290">Set the **Color** to **#FFFFFFFF**</span></span>

    ![Composant de texte](images/AzureLabs-Lab2-21-5.png)

3.  <span data-ttu-id="988a4-292">Faites glisser le **LabelText** à partir du *panneau*de la hiérarchie, dans le *dossier Asset*, dans le *panneau Projet*.</span><span class="sxs-lookup"><span data-stu-id="988a4-292">Drag the **LabelText** from the *Hierarchy Panel*, into the *Asset Folder*, within in the *Project Panel*.</span></span> <span data-ttu-id="988a4-293">Cela rend le **LabelText** Prefab, afin qu’il puisse être instancié dans le code.</span><span class="sxs-lookup"><span data-stu-id="988a4-293">This will make the **LabelText** a Prefab, so that it can be instantiated in code.</span></span>

    ![Créez un Prefab de l’objet LabelText.](images/AzureLabs-Lab2-22.png)
 
4.  <span data-ttu-id="988a4-295">Vous devez supprimer le **LabelText** du *panneau de hiérarchie*, afin qu’il ne s’affiche pas dans la scène d’ouverture.</span><span class="sxs-lookup"><span data-stu-id="988a4-295">You should delete the **LabelText** from the *Hierarchy Panel*, so that it will not be displayed in the opening scene.</span></span> <span data-ttu-id="988a4-296">Comme il s’agit maintenant d’un Prefab, que vous allez appeler pour des instances individuelles à partir de votre dossier de ressources, il n’est pas nécessaire de le conserver dans la scène.</span><span class="sxs-lookup"><span data-stu-id="988a4-296">As it is now a prefab, which you will call on for individual instances from your Assets folder, there is no need to keep it within the scene.</span></span> 
5.  <span data-ttu-id="988a4-297">La dernière structure de l’objet dans le volet de la *hiérarchie* doit être similaire à celle illustrée dans l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="988a4-297">The final object structure in the *Hierarchy Panel* should be like the one shown in the image below:</span></span>

    ![Structure finale du panneau de la hiérarchie.](images/AzureLabs-Lab2-23.png)

## <a name="chapter-5--create-the-resultslabel-class"></a><span data-ttu-id="988a4-299">Chapitre 5 : créer la classe ResultsLabel</span><span class="sxs-lookup"><span data-stu-id="988a4-299">Chapter 5 – Create the ResultsLabel class</span></span>

<span data-ttu-id="988a4-300">Le premier script que vous devez créer est la classe *ResultsLabel* , qui est chargée des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="988a4-300">The first script you need to create is the *ResultsLabel* class, which is responsible for the following:</span></span> 

- <span data-ttu-id="988a4-301">Création des étiquettes dans l’espace universel approprié, par rapport à la position de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="988a4-301">Creating the Labels in the appropriate world space, relative to the position of the Camera.</span></span>
- <span data-ttu-id="988a4-302">Affichage des balises à partir de l’image analyse.</span><span class="sxs-lookup"><span data-stu-id="988a4-302">Displaying the Tags from the Image Anaysis.</span></span>

<span data-ttu-id="988a4-303">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="988a4-303">To create this class:</span></span> 

1.  <span data-ttu-id="988a4-304">Cliquez avec le bouton droit dans le *panneau Projet*, puis **créez > dossier**.</span><span class="sxs-lookup"><span data-stu-id="988a4-304">Right-click in the *Project Panel*, then **Create > Folder**.</span></span> <span data-ttu-id="988a4-305">Nommez le dossier **scripts**.</span><span class="sxs-lookup"><span data-stu-id="988a4-305">Name the folder **Scripts**.</span></span> 

    ![Créer un dossier de scripts.](images/AzureLabs-Lab2-24.png)

2.  <span data-ttu-id="988a4-307">Avec le dossier **scripts** créer, double-cliquez dessus pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="988a4-307">With the **Scripts** folder create, double click it to open.</span></span> <span data-ttu-id="988a4-308">Ensuite, dans ce dossier, cliquez avec le bouton droit, puis sélectionnez **créer >**  **C# script**.</span><span class="sxs-lookup"><span data-stu-id="988a4-308">Then within that folder, right-click, and select **Create >** then **C# Script**.</span></span> <span data-ttu-id="988a4-309">Nommez le script *ResultsLabel*.</span><span class="sxs-lookup"><span data-stu-id="988a4-309">Name the script *ResultsLabel*.</span></span> 

3.  <span data-ttu-id="988a4-310">Double-cliquez sur le nouveau script *ResultsLabel* pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="988a4-310">Double click on the new *ResultsLabel* script to open it with **Visual Studio**.</span></span>

4.  <span data-ttu-id="988a4-311">À l’intérieur de la classe, insérez le code suivant dans la classe *ResultsLabel* :</span><span class="sxs-lookup"><span data-stu-id="988a4-311">Inside the Class insert the following code in the *ResultsLabel* class:</span></span>

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

6.  <span data-ttu-id="988a4-312">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="988a4-312">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>
7.  <span data-ttu-id="988a4-313">De retour dans l' *éditeur Unity*, cliquez et faites glisser la classe *ResultsLabel* du dossier **scripts** vers l’objet **Camera principal** dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="988a4-313">Back in the *Unity Editor*, click and drag the *ResultsLabel* class from the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span>
8.  <span data-ttu-id="988a4-314">Cliquez sur l' **appareil photo principal** et observez le panneau de l' *inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="988a4-314">Click on the **Main Camera** and look at the *Inspector Panel*.</span></span>

<span data-ttu-id="988a4-315">Vous remarquerez qu’à partir du script que vous venez de faire glisser dans l’appareil photo, il y a deux champs : **Cursor** et **label Prefab**.</span><span class="sxs-lookup"><span data-stu-id="988a4-315">You will notice that from the script you just dragged into the Camera, there are two fields: **Cursor** and **Label Prefab**.</span></span>

9.  <span data-ttu-id="988a4-316">Faites glisser l’objet appelé **Cursor** du *volet* de la hiérarchie vers l’emplacement nommé **Cursor**, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="988a4-316">Drag the object called **Cursor** from the *Hierarchy Panel* to the slot named **Cursor**, as shown in the image below.</span></span>
10. <span data-ttu-id="988a4-317">Faites glisser l’objet appelé **LabelText** du *dossier composants* du *panneau projet* vers l’emplacement nommé **étiquette Prefab**, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="988a4-317">Drag the object called **LabelText** from the *Assets Folder* in the *Project Panel* to the slot named **Label Prefab**, as shown in the image below.</span></span> 

    ![Définissez les cibles de référence dans Unity.](images/AzureLabs-Lab2-25.png)

## <a name="chapter-6--create-the-imagecapture-class"></a><span data-ttu-id="988a4-319">Chapitre 6 : créer la classe ImageCapture</span><span class="sxs-lookup"><span data-stu-id="988a4-319">Chapter 6 – Create the ImageCapture class</span></span>

<span data-ttu-id="988a4-320">La classe suivante que vous allez créer est la classe *ImageCapture* .</span><span class="sxs-lookup"><span data-stu-id="988a4-320">The next class you are going to create is the *ImageCapture* class.</span></span> <span data-ttu-id="988a4-321">Cette classe est chargée des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="988a4-321">This class is responsible for:</span></span>

-   <span data-ttu-id="988a4-322">Capture d’une image à l’aide de la caméra HoloLens et stockage dans le dossier de l’application.</span><span class="sxs-lookup"><span data-stu-id="988a4-322">Capturing an Image using the HoloLens Camera and storing it in the App Folder.</span></span>
-   <span data-ttu-id="988a4-323">Capture des gestes TAP de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="988a4-323">Capturing Tap gestures from the user.</span></span>

<span data-ttu-id="988a4-324">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="988a4-324">To create this class:</span></span> 

1.  <span data-ttu-id="988a4-325">Accédez au dossier **scripts** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="988a4-325">Go to the **Scripts** folder you created previously.</span></span> 
2.  <span data-ttu-id="988a4-326">Cliquez avec le bouton droit dans le dossier, **créez > C# script**.</span><span class="sxs-lookup"><span data-stu-id="988a4-326">Right-click inside the folder, **Create > C# Script**.</span></span> <span data-ttu-id="988a4-327">Appelez le script *ImageCapture*.</span><span class="sxs-lookup"><span data-stu-id="988a4-327">Call the script *ImageCapture*.</span></span> 
3.  <span data-ttu-id="988a4-328">Double-cliquez sur le nouveau script *ImageCapture* pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="988a4-328">Double click on the new *ImageCapture* script to open it with **Visual Studio**.</span></span>
4.  <span data-ttu-id="988a4-329">Ajoutez les espaces de noms suivants au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="988a4-329">Add the following namespaces to the top of the file:</span></span>

    ```csharp
        using System.IO;
        using System.Linq;
        using UnityEngine;
        using UnityEngine.XR.WSA.Input;
        using UnityEngine.XR.WSA.WebCam;
    ```

5.  <span data-ttu-id="988a4-330">Ajoutez ensuite les variables suivantes à l’intérieur de la classe *ImageCapture* , au-dessus de la méthode *Start ()* :</span><span class="sxs-lookup"><span data-stu-id="988a4-330">Then add the following variables inside the *ImageCapture* class, above the *Start()* method:</span></span>

    ```csharp
        public static ImageCapture instance; 
        public int tapsCount;
        private PhotoCapture photoCaptureObject = null;
        private GestureRecognizer recognizer;
        private bool currentlyCapturing = false;
    ```
 
<span data-ttu-id="988a4-331">La variable **tapsCount** stocke le nombre de gestes TAP capturés par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="988a4-331">The **tapsCount** variable will store the number of tap gestures captured from the user.</span></span> <span data-ttu-id="988a4-332">Ce nombre est utilisé pour nommer les images capturées.</span><span class="sxs-lookup"><span data-stu-id="988a4-332">This number is used in the naming of the images captured.</span></span>

6.  <span data-ttu-id="988a4-333">Vous devez maintenant ajouter le code des méthodes *éveillés ()* et *Start ()* .</span><span class="sxs-lookup"><span data-stu-id="988a4-333">Code for *Awake()* and *Start()* methods now needs to be added.</span></span> <span data-ttu-id="988a4-334">Ils sont appelés lorsque la classe est initialisée :</span><span class="sxs-lookup"><span data-stu-id="988a4-334">These will be called when the class initializes:</span></span>

    ```csharp
        private void Awake()
        {
            // Allows this instance to behave like a singleton
            instance = this;
        }

        void Start()
        {
            // subscribing to the HoloLens API gesture recognizer to track user gestures
            recognizer = new GestureRecognizer();
            recognizer.SetRecognizableGestures(GestureSettings.Tap);
            recognizer.Tapped += TapHandler;
            recognizer.StartCapturingGestures();
        }
    ```

7.  <span data-ttu-id="988a4-335">Implémentez un gestionnaire qui sera appelé quand un mouvement TAP se produit.</span><span class="sxs-lookup"><span data-stu-id="988a4-335">Implement a handler that will be called when a Tap gesture occurs.</span></span> 

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
 
<span data-ttu-id="988a4-336">La méthode *TapHandler ()* incrémente le nombre de clics capturés à l’utilisateur et utilise la position actuelle du curseur pour déterminer où positionner une nouvelle étiquette.</span><span class="sxs-lookup"><span data-stu-id="988a4-336">The *TapHandler()* method increments the number of taps captured from the user and uses the current Cursor position to determine where to position a new Label.</span></span>

<span data-ttu-id="988a4-337">Cette méthode appelle ensuite la méthode *ExecuteImageCaptureAndAnalysis ()* pour commencer les fonctionnalités principales de cette application.</span><span class="sxs-lookup"><span data-stu-id="988a4-337">This method then calls the *ExecuteImageCaptureAndAnalysis()* method to begin the core functionality of this application.</span></span>

8.  <span data-ttu-id="988a4-338">Une fois qu’une image a été capturée et stockée, les gestionnaires suivants sont appelés.</span><span class="sxs-lookup"><span data-stu-id="988a4-338">Once an Image has been captured and stored, the following handlers will be called.</span></span> <span data-ttu-id="988a4-339">Si le processus réussit, le résultat est passé au *VisionManager* (que vous êtes en train de créer) à des fins d’analyse.</span><span class="sxs-lookup"><span data-stu-id="988a4-339">If the process is successful, the result is passed to the *VisionManager* (which you are yet to create) for analysis.</span></span>

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
 
9.  <span data-ttu-id="988a4-340">Ajoutez ensuite la méthode utilisée par l’application pour démarrer le processus de capture d’image et stocker l’image.</span><span class="sxs-lookup"><span data-stu-id="988a4-340">Then add the method that the application uses to start the Image capture process and store the image.</span></span>

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
> <span data-ttu-id="988a4-341">À ce stade, vous remarquerez qu’une erreur s’affiche dans le panneau de la console de l' *éditeur Unity*.</span><span class="sxs-lookup"><span data-stu-id="988a4-341">At this point you will notice an error appearing in the *Unity Editor Console Panel*.</span></span> <span data-ttu-id="988a4-342">Cela est dû au fait que le code fait référence à la classe *VisionManager* que vous allez créer dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="988a4-342">This is because the code references the *VisionManager* class which you will create in the next Chapter.</span></span>

## <a name="chapter-7--call-to-azure-and-image-analysis"></a><span data-ttu-id="988a4-343">Chapitre 7 – appel à Azure et à l’analyse des images</span><span class="sxs-lookup"><span data-stu-id="988a4-343">Chapter 7 – Call to Azure and Image Analysis</span></span>

<span data-ttu-id="988a4-344">Le dernier script que vous devez créer est la classe *VisionManager* .</span><span class="sxs-lookup"><span data-stu-id="988a4-344">The last script you need to create is the *VisionManager* class.</span></span> 

<span data-ttu-id="988a4-345">Cette classe est chargée des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="988a4-345">This class is responsible for:</span></span>

-   <span data-ttu-id="988a4-346">Chargement de la dernière image capturée sous la forme d’un tableau d’octets.</span><span class="sxs-lookup"><span data-stu-id="988a4-346">Loading the latest image captured as an array of bytes.</span></span>
-   <span data-ttu-id="988a4-347">Envoi du tableau d’octets à votre instance *Azure API vision par ordinateur* service à des fins d’analyse.</span><span class="sxs-lookup"><span data-stu-id="988a4-347">Sending the byte array to your *Azure Computer Vision API* Service instance for analysis.</span></span>
-   <span data-ttu-id="988a4-348">Réception de la réponse sous forme de chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="988a4-348">Receiving the response as a JSON string.</span></span>
-   <span data-ttu-id="988a4-349">Désérialisation de la réponse et transmission des balises résultantes à la classe *ResultsLabel* .</span><span class="sxs-lookup"><span data-stu-id="988a4-349">Deserializing the response and passing the resulting Tags to the *ResultsLabel* class.</span></span>
 
<span data-ttu-id="988a4-350">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="988a4-350">To create this class:</span></span>

1.  <span data-ttu-id="988a4-351">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="988a4-351">Double click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="988a4-352">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**.</span><span class="sxs-lookup"><span data-stu-id="988a4-352">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="988a4-353">Nommez le script *VisionManager*.</span><span class="sxs-lookup"><span data-stu-id="988a4-353">Name the script *VisionManager*.</span></span> 
3.  <span data-ttu-id="988a4-354">Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="988a4-354">Double click on the new script to open it with Visual Studio.</span></span>
4.  <span data-ttu-id="988a4-355">Mettez à jour les espaces de noms pour qu’ils soient identiques à ce qui suit, en haut de la classe *VisionManager* :</span><span class="sxs-lookup"><span data-stu-id="988a4-355">Update the namespaces to be the same as the following, at the top of the *VisionManager* class:</span></span>

    ```csharp
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using System.IO;
        using UnityEngine;
        using UnityEngine.Networking;
    ```
 
5.  <span data-ttu-id="988a4-356">En haut de votre script, à l' *intérieur* de la classe *VisionManager* (au-dessus de la méthode *Start ()* ), vous devez maintenant créer deux *classes* qui représenteront la réponse JSON désérialisée à partir d’Azure :</span><span class="sxs-lookup"><span data-stu-id="988a4-356">At the top of your script, *inside* the *VisionManager* class (above the *Start()* method), you now need to create two *Classes* that will represent the deserialized JSON response from Azure:</span></span>

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
    > <span data-ttu-id="988a4-357">Les classes *TagData* et *AnalysedObject* doivent avoir l’attribut *[System. Serializable]* ajouté avant la déclaration pour pouvoir être désérialisées avec les bibliothèques Unity.</span><span class="sxs-lookup"><span data-stu-id="988a4-357">The *TagData* and *AnalysedObject* classes need to have the *[System.Serializable]* attribute added before the declaration to be able to be deserialized with the Unity libraries.</span></span>

6.  <span data-ttu-id="988a4-358">Dans la classe VisionManager, vous devez ajouter les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="988a4-358">In the VisionManager class, you should add the following variables:</span></span>

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
    > <span data-ttu-id="988a4-359">Veillez à insérer votre **clé d’authentification** dans la variable **authorizationKey** .</span><span class="sxs-lookup"><span data-stu-id="988a4-359">Make sure you insert your **Auth Key** into the **authorizationKey** variable.</span></span> <span data-ttu-id="988a4-360">Vous aurez noté votre **clé d’authentification** au début de ce cours, [Chapitre 1](#chapter-1--the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="988a4-360">You will have noted your **Auth Key** at the beginning of this course, [Chapter 1](#chapter-1--the-azure-portal).</span></span>

    > [!WARNING] 
    > <span data-ttu-id="988a4-361">La variable **visionAnalysisEndpoint** peut être différente de celle spécifiée dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="988a4-361">The **visionAnalysisEndpoint** variable might differ from the one specified in this example.</span></span> <span data-ttu-id="988a4-362">L' **ouest des États-Unis** fait strictement référence aux instances de service créées pour la région États-Unis de l’Ouest.</span><span class="sxs-lookup"><span data-stu-id="988a4-362">The **west-us** strictly refers to Service instances created for the West US region.</span></span> <span data-ttu-id="988a4-363">Mettez-le à jour avec votre [URL de point de terminaison](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa); Voici quelques exemples de ce qui peut ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="988a4-363">Update this with your [endpoint URL](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa); here are some examples of what that might look like:</span></span>
    > - <span data-ttu-id="988a4-364">Europe de l’Ouest : `https://westeurope.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`</span><span class="sxs-lookup"><span data-stu-id="988a4-364">West Europe: `https://westeurope.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`</span></span>
    > - <span data-ttu-id="988a4-365">Asie du sud-est : `https://southeastasia.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`</span><span class="sxs-lookup"><span data-stu-id="988a4-365">Southeast Asia: `https://southeastasia.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`</span></span>
    > - <span data-ttu-id="988a4-366">Est de l’Australie : `https://australiaeast.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`</span><span class="sxs-lookup"><span data-stu-id="988a4-366">Australia East: `https://australiaeast.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`</span></span>

7.  <span data-ttu-id="988a4-367">Le code pour éveillé doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="988a4-367">Code for Awake now needs to be added.</span></span> 

    ```csharp
        private void Awake()
        {
            // allows this instance to behave like a singleton
            instance = this;
        }
    ```

8.  <span data-ttu-id="988a4-368">Ensuite, ajoutez la Coroutine (avec la méthode de flux statique ci-dessous), qui obtiendra les résultats de l’analyse de l’image capturée par la classe *ImageCapture* .</span><span class="sxs-lookup"><span data-stu-id="988a4-368">Next, add the coroutine (with the static stream method below it), which will obtain the results of the analysis of the image captured by the *ImageCapture* Class.</span></span> 

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

9.  <span data-ttu-id="988a4-369">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="988a4-369">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>
10. <span data-ttu-id="988a4-370">De retour dans l’éditeur Unity, cliquez et faites glisser les classes *VisionManager* et *ImageCapture* du dossier **scripts** vers l’objet **Camera principal** dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="988a4-370">Back in the Unity Editor, click and drag the *VisionManager* and *ImageCapture* classes from the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span> 

## <a name="chapter-8--before-building"></a><span data-ttu-id="988a4-371">Chapitre 8 – avant la génération</span><span class="sxs-lookup"><span data-stu-id="988a4-371">Chapter 8 – Before building</span></span>

<span data-ttu-id="988a4-372">Pour effectuer un test minutieux de votre application, vous devez l’chargement sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="988a4-372">To perform a thorough test of your application you will need to sideload it onto your HoloLens.</span></span>
<span data-ttu-id="988a4-373">Avant cela, assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="988a4-373">Before you do, ensure that:</span></span>

-   <span data-ttu-id="988a4-374">Tous les paramètres mentionnés dans le [Chapitre 2](#chapter-2--set-up-the-unity-project) sont correctement définis.</span><span class="sxs-lookup"><span data-stu-id="988a4-374">All the settings mentioned in [Chapter 2](#chapter-2--set-up-the-unity-project) are set correctly.</span></span> 
-   <span data-ttu-id="988a4-375">Tous les scripts sont attachés à l’objet **Camera principal** .</span><span class="sxs-lookup"><span data-stu-id="988a4-375">All the scripts are attached to the **Main Camera** object.</span></span> 
-   <span data-ttu-id="988a4-376">Tous les champs du volet principal de l’inspecteur de l' *appareil photo* sont correctement affectés.</span><span class="sxs-lookup"><span data-stu-id="988a4-376">All the fields in the *Main Camera Inspector Panel* are assigned properly.</span></span>
-   <span data-ttu-id="988a4-377">Veillez à insérer votre **clé d’authentification** dans la variable **authorizationKey** .</span><span class="sxs-lookup"><span data-stu-id="988a4-377">Make sure you insert your **Auth Key** into the **authorizationKey** variable.</span></span>
-   <span data-ttu-id="988a4-378">Vérifiez que vous avez également vérifié votre point de terminaison dans votre script *VisionManager* et qu’il est aligné sur *votre* région (ce document utilise par défaut *West-US* ).</span><span class="sxs-lookup"><span data-stu-id="988a4-378">Ensure that you have also checked your endpoint in your *VisionManager* script, and that it aligns to *your* region (this document uses *west-us* by default).</span></span>

## <a name="chapter-9--build-the-uwp-solution-and-sideload-the-application"></a><span data-ttu-id="988a4-379">Chapitre 9 : créer la solution UWP et chargement l’application</span><span class="sxs-lookup"><span data-stu-id="988a4-379">Chapter 9 – Build the UWP Solution and sideload the application</span></span>
<span data-ttu-id="988a4-380">Tout ce qui est nécessaire pour la section Unity de ce projet est maintenant terminé. il est donc temps de la générer à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="988a4-380">Everything needed for the Unity section of this project has now been completed, so it is time to build it from Unity.</span></span>

1.  <span data-ttu-id="988a4-381">Accédez à *paramètres de build* - **fichier > paramètres de Build...**</span><span class="sxs-lookup"><span data-stu-id="988a4-381">Navigate to *Build Settings* - **File > Build Settings…**</span></span>
2.  <span data-ttu-id="988a4-382">Dans la fenêtre *paramètres de build* , cliquez sur **générer**.</span><span class="sxs-lookup"><span data-stu-id="988a4-382">From the *Build Settings* window, click **Build**.</span></span>

    ![Génération de l’application à partir d’Unity](images/AzureLabs-Lab2-26.png)

3.  <span data-ttu-id="988a4-384">Si ce n’est pas déjà fait, les **projets Unity C#** .</span><span class="sxs-lookup"><span data-stu-id="988a4-384">If not already, tick **Unity C# Projects**.</span></span>
4.  <span data-ttu-id="988a4-385">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="988a4-385">Click **Build**.</span></span> <span data-ttu-id="988a4-386">Unity lance une fenêtre de l' *Explorateur de fichiers* , dans laquelle vous devez créer, puis sélectionner un dossier dans lequel générer l’application.</span><span class="sxs-lookup"><span data-stu-id="988a4-386">Unity will launch a *File Explorer* window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="988a4-387">Créez ce dossier maintenant, puis nommez-le *application*.</span><span class="sxs-lookup"><span data-stu-id="988a4-387">Create that folder now, and name it *App*.</span></span> <span data-ttu-id="988a4-388">Ensuite, avec le dossier d' *application* sélectionné, appuyez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="988a4-388">Then with the *App* folder selected, press **Select Folder**.</span></span> 
5.  <span data-ttu-id="988a4-389">Unity commence à générer votre projet dans le dossier de l' *application* .</span><span class="sxs-lookup"><span data-stu-id="988a4-389">Unity will begin building your project to the *App* folder.</span></span> 
6.  <span data-ttu-id="988a4-390">Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' *Explorateur de fichiers* s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).</span><span class="sxs-lookup"><span data-stu-id="988a4-390">Once Unity has finished building (it might take some time), it will open a *File Explorer* window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

## <a name="chapter-10--deploy-to-hololens"></a><span data-ttu-id="988a4-391">Chapitre 10 – déployer dans HoloLens</span><span class="sxs-lookup"><span data-stu-id="988a4-391">Chapter 10 – Deploy to HoloLens</span></span>

<span data-ttu-id="988a4-392">Pour effectuer un déploiement sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="988a4-392">To deploy on HoloLens:</span></span>

1.  <span data-ttu-id="988a4-393">Vous aurez besoin de l’adresse IP de votre HoloLens (pour le déploiement à distance) et vérifiez que votre HoloLens est en **mode développeur**.</span><span class="sxs-lookup"><span data-stu-id="988a4-393">You will need the IP Address of your HoloLens (for Remote Deploy), and to ensure your HoloLens is in **Developer Mode**.</span></span> <span data-ttu-id="988a4-394">Pour cela, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="988a4-394">To do this:</span></span>

    1. <span data-ttu-id="988a4-395">Tout en portant votre HoloLens, ouvrez les **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="988a4-395">Whilst wearing your HoloLens, open the **Settings**.</span></span>
    2. <span data-ttu-id="988a4-396">Accéder au **réseau & Internet > Wi-Fi > options avancées**</span><span class="sxs-lookup"><span data-stu-id="988a4-396">Go to **Network & Internet > Wi-Fi > Advanced Options**</span></span>
    3. <span data-ttu-id="988a4-397">Notez l’adresse **IPv4** .</span><span class="sxs-lookup"><span data-stu-id="988a4-397">Note the **IPv4** address.</span></span>
    4. <span data-ttu-id="988a4-398">Ensuite, revenez aux **paramètres**, puis à **mettre à jour & > de sécurité pour les développeurs**</span><span class="sxs-lookup"><span data-stu-id="988a4-398">Next, navigate back to **Settings**, and then to **Update & Security > For Developers**</span></span> 
    5. <span data-ttu-id="988a4-399">Définissez le mode développeur sur.</span><span class="sxs-lookup"><span data-stu-id="988a4-399">Set Developer Mode On.</span></span>

2.  <span data-ttu-id="988a4-400">Accédez à votre nouvelle build Unity (le dossier de l' *application* ) et ouvrez le fichier solution avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="988a4-400">Navigate to your new Unity build (the *App* folder) and open the solution file with *Visual Studio*.</span></span>
3.  <span data-ttu-id="988a4-401">Dans la configuration de la solution, sélectionnez **Déboguer**.</span><span class="sxs-lookup"><span data-stu-id="988a4-401">In the Solution Configuration select **Debug**.</span></span>
4.  <span data-ttu-id="988a4-402">Dans la plateforme de la solution, sélectionnez **x86**, **ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="988a4-402">In the Solution Platform, select **x86**, **Remote Machine**.</span></span> 

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab2-27.png)
 
5.  <span data-ttu-id="988a4-404">Accédez au **menu Générer** , puis cliquez sur **déployer la solution**pour chargement l’application à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="988a4-404">Go to the **Build menu** and click on **Deploy Solution**, to sideload the application to your HoloLens.</span></span>
6.  <span data-ttu-id="988a4-405">Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prête à être lancée.</span><span class="sxs-lookup"><span data-stu-id="988a4-405">Your App should now appear in the list of installed apps on your HoloLens, ready to be launched!</span></span>

> [!NOTE]
> <span data-ttu-id="988a4-406">Pour effectuer un déploiement sur un casque immersif, définissez la plateforme de la **solution** sur *ordinateur local*et définissez la **configuration** sur *Déboguer*, avec *x86* comme **plateforme**.</span><span class="sxs-lookup"><span data-stu-id="988a4-406">To deploy to immersive headset, set the **Solution Platform** to *Local Machine*, and set the **Configuration** to *Debug*, with *x86* as the **Platform**.</span></span> <span data-ttu-id="988a4-407">Déployez ensuite sur l’ordinateur local, à l’aide du **menu Générer**, en sélectionnant *déployer la solution*.</span><span class="sxs-lookup"><span data-stu-id="988a4-407">Then deploy to the local machine, using the **Build menu**, selecting *Deploy Solution*.</span></span> 

## <a name="your-finished-computer-vision-api-application"></a><span data-ttu-id="988a4-408">Votre application API Vision par ordinateur terminée</span><span class="sxs-lookup"><span data-stu-id="988a4-408">Your finished Computer Vision API application</span></span>

<span data-ttu-id="988a4-409">Félicitations, vous avez créé une application de réalité mixte qui tire parti de la API Vision par ordinateur Azure pour reconnaître des objets réels, et afficher la confiance de ce qui a été observé.</span><span class="sxs-lookup"><span data-stu-id="988a4-409">Congratulations, you built a mixed reality app that leverages the Azure Computer Vision API to recognize real world objects, and display confidence of what has been seen.</span></span>

![résultat de l’atelier](images/AzureLabs-Lab2-000.png)

## <a name="bonus-exercises"></a><span data-ttu-id="988a4-411">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="988a4-411">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="988a4-412">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="988a4-412">Exercise 1</span></span>

<span data-ttu-id="988a4-413">Tout comme vous avez utilisé le paramètre *Tags* (tel qu’il est prouvé dans le *point de terminaison* utilisé dans *VisionManager*), étendez l’application pour détecter d’autres informations. Examinez les autres paramètres auxquels vous avez accès [ici](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa).</span><span class="sxs-lookup"><span data-stu-id="988a4-413">Just as you have used the *Tags* parameter (as evidenced within the *endpoint* used within the *VisionManager*), extend the app to detect other information; have a look at what other parameters you have access to [HERE](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa).</span></span>

### <a name="exercise-2"></a><span data-ttu-id="988a4-414">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="988a4-414">Exercise 2</span></span>

<span data-ttu-id="988a4-415">Affichez les données Azure retournées, d’une manière plus conversationnele et lisible, en masquant éventuellement les nombres.</span><span class="sxs-lookup"><span data-stu-id="988a4-415">Display the returned Azure data, in a more conversational, and readable way, perhaps hiding the numbers.</span></span> <span data-ttu-id="988a4-416">Comme si un bot était en contact avec l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="988a4-416">As though a bot might be speaking to the user.</span></span>
