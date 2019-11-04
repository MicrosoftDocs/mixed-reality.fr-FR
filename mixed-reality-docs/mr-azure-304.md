---
title: RM et Azure 304-reconnaissance faciale
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, reconnaissance faciale, hololens, immersif, VR
ms.openlocfilehash: ef75be5485f85538eb8b3db3eebec63b166f7aa3
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438493"
---
>[!NOTE]
><span data-ttu-id="3b7e8-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="3b7e8-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="3b7e8-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="3b7e8-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="3b7e8-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="3b7e8-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br> 

# <a name="mr-and-azure-304-face-recognition"></a><span data-ttu-id="3b7e8-110">MR et Azure 304 : reconnaissance faciale</span><span class="sxs-lookup"><span data-stu-id="3b7e8-110">MR and Azure 304: Face recognition</span></span>

![résultat de la fin de ce cours](images/AzureLabs-Lab4-00.png)

<span data-ttu-id="3b7e8-112">Dans ce cours, vous allez apprendre à ajouter des fonctionnalités de reconnaissance faciale à une application de réalité mixte, à l’aide d’Azure Cognitive Services, avec la API Visage Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-112">In this course you will learn how to add face recognition capabilities to a mixed reality application, using Azure Cognitive Services, with the Microsoft Face API.</span></span>

<span data-ttu-id="3b7e8-113">*Azure API visage* est un service Microsoft qui fournit aux développeurs les algorithmes les plus avancés, le tout dans le Cloud.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-113">*Azure Face API* is a Microsoft service, which provides developers with the most advanced face algorithms, all in the cloud.</span></span> <span data-ttu-id="3b7e8-114">La *API visage* a deux fonctions principales : la détection des visages avec les attributs et la reconnaissance faciale.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-114">The *Face API* has two main functions: face detection with attributes, and face recognition.</span></span> <span data-ttu-id="3b7e8-115">Cela permet aux développeurs de définir simplement un ensemble de groupes pour les visages, puis d’envoyer des images de requête au service ultérieurement, pour déterminer à qui appartient une face.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-115">This allows developers to simply set a set of groups for faces, and then, send query images to the service later, to determine to whom a face belongs.</span></span> <span data-ttu-id="3b7e8-116">Pour plus d’informations, consultez la [page reconnaissance des visages Azure](https://azure.microsoft.com/services/cognitive-services/face/).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-116">For more information, visit the [Azure Face Recognition page](https://azure.microsoft.com/services/cognitive-services/face/).</span></span>

<span data-ttu-id="3b7e8-117">Une fois ce cours terminé, vous disposerez d’une application HoloLens de réalité mixte, qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-117">Having completed this course, you will have a mixed reality HoloLens application, which will be able to do the following:</span></span>

1. <span data-ttu-id="3b7e8-118">Utilisez un **mouvement TAP** pour initier la capture d’une image à l’aide de l’appareil photo HoloLens intégré.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-118">Use a **Tap Gesture** to initiate the capture of an image using the on-board HoloLens camera.</span></span> 
2. <span data-ttu-id="3b7e8-119">Envoyez l’image capturée au service *Azure API visage* .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-119">Send the captured image to the *Azure Face API* service.</span></span>
3. <span data-ttu-id="3b7e8-120">Recevoir les résultats de l’algorithme *API visage* .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-120">Receive the results of the *Face API* algorithm.</span></span>
4. <span data-ttu-id="3b7e8-121">Utilisez une interface utilisateur simple pour afficher le nom des personnes mises en correspondance.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-121">Use a simple User Interface, to display the name of matched people.</span></span>

<span data-ttu-id="3b7e8-122">Cela vous apprend à obtenir les résultats du service API Visage dans votre application de réalité mixte basée sur Unity.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-122">This will teach you how to get the results from the Face API Service into your Unity-based mixed reality application.</span></span>

<span data-ttu-id="3b7e8-123">Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-123">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="3b7e8-124">Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-124">This course is designed to teach you how to integrate an Azure Service with your Unity Project.</span></span> <span data-ttu-id="3b7e8-125">C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-125">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

## <a name="device-support"></a><span data-ttu-id="3b7e8-126">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="3b7e8-126">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="3b7e8-127">Course</span><span class="sxs-lookup"><span data-stu-id="3b7e8-127">Course</span></span></th><th style="width:150px"> <span data-ttu-id="3b7e8-128"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="3b7e8-128"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="3b7e8-129"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="3b7e8-129"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="3b7e8-130">MR et Azure 304 : reconnaissance faciale</span><span class="sxs-lookup"><span data-stu-id="3b7e8-130">MR and Azure 304: Face recognition</span></span></td><td style="text-align: center;"> <span data-ttu-id="3b7e8-131">✔️</span><span class="sxs-lookup"><span data-stu-id="3b7e8-131">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="3b7e8-132">✔️</span><span class="sxs-lookup"><span data-stu-id="3b7e8-132">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="3b7e8-133">Bien que ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques pour Windows Mixed Reality (VR).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-133">While this course primarily focuses on HoloLens, you can also apply what you learn in this course to Windows Mixed Reality immersive (VR) headsets.</span></span> <span data-ttu-id="3b7e8-134">Étant donné que les casques immersifs ne disposent pas de caméras accessibles, vous aurez besoin d’une caméra externe connectée à votre PC.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-134">Because immersive (VR) headsets do not have accessible cameras, you will need an external camera connected to your PC.</span></span> <span data-ttu-id="3b7e8-135">À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge les écouteurs immersifs (VR).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-135">As you follow along with the course, you will see notes on any changes you might need to employ to support immersive (VR) headsets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b7e8-136">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="3b7e8-136">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="3b7e8-137">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-137">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="3b7e8-138">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-138">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="3b7e8-139">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-139">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="3b7e8-140">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-140">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="3b7e8-141">Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)</span><span class="sxs-lookup"><span data-stu-id="3b7e8-141">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="3b7e8-142">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="3b7e8-142">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md)
- [<span data-ttu-id="3b7e8-143">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="3b7e8-143">The latest Windows 10 SDK</span></span>](install-the-tools.md)
- [<span data-ttu-id="3b7e8-144">Unity 2017,4</span><span class="sxs-lookup"><span data-stu-id="3b7e8-144">Unity 2017.4</span></span>](install-the-tools.md)
- [<span data-ttu-id="3b7e8-145">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3b7e8-145">Visual Studio 2017</span></span>](install-the-tools.md)
- <span data-ttu-id="3b7e8-146">Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="3b7e8-146">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="3b7e8-147">Appareil photo connecté à votre PC (pour le développement d’un casque immersif)</span><span class="sxs-lookup"><span data-stu-id="3b7e8-147">A camera connected to your PC (for immersive headset development)</span></span>
- <span data-ttu-id="3b7e8-148">Accès à Internet pour l’installation d’Azure et la récupération de API Visage</span><span class="sxs-lookup"><span data-stu-id="3b7e8-148">Internet access for Azure setup and Face API retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="3b7e8-149">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="3b7e8-149">Before you start</span></span>

1.  <span data-ttu-id="3b7e8-150">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-150">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="3b7e8-151">Configurez et testez votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-151">Set up and test your HoloLens.</span></span> <span data-ttu-id="3b7e8-152">Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-152">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span> 
3.  <span data-ttu-id="3b7e8-153">Il est judicieux d’effectuer un réglage de l’étalonnage et du capteur au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-153">It is a good idea to perform Calibration and Sensor Tuning when beginning developing a new HoloLens App (sometimes it can help to perform those tasks for each user).</span></span> 

<span data-ttu-id="3b7e8-154">Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens-2).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-154">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens-2).</span></span>

<span data-ttu-id="3b7e8-155">Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-155">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

## <a name="chapter-1---the-azure-portal"></a><span data-ttu-id="3b7e8-156">Chapitre 1-portail Azure</span><span class="sxs-lookup"><span data-stu-id="3b7e8-156">Chapter 1 - The Azure Portal</span></span>

<span data-ttu-id="3b7e8-157">Pour utiliser le service de *API visage* dans Azure, vous devez configurer une instance du service qui sera mise à la disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-157">To use the *Face API* service in Azure, you will need to configure an instance of the service to be made available to your application.</span></span>

1.  <span data-ttu-id="3b7e8-158">Tout d’abord, connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-158">First, log in to the [Azure Portal](https://portal.azure.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="3b7e8-159">Si vous n’avez pas encore de compte Azure, vous devez en créer un.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-159">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="3b7e8-160">Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-160">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="3b7e8-161">Une fois que vous êtes connecté, cliquez sur **nouveau** dans l’angle supérieur gauche et recherchez *API visage*, appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-161">Once you are logged in, click on **New** in the top left corner, and search for *Face API*, press **Enter**.</span></span>

    ![Rechercher l’API visage](images/AzureLabs-Lab4-01.png)

    > [!NOTE]
    > <span data-ttu-id="3b7e8-163">Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-163">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

3.  <span data-ttu-id="3b7e8-164">La nouvelle page fournit une description du service *API visage* .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-164">The new page will provide a description of the *Face API* service.</span></span> <span data-ttu-id="3b7e8-165">En bas à gauche de cette invite, sélectionnez le bouton **créer** pour créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-165">At the bottom left of this prompt, select the **Create** button, to create an association with this service.</span></span>

    ![informations sur l’API visage](images/AzureLabs-Lab4-02.png)

4.  <span data-ttu-id="3b7e8-167">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="3b7e8-167">Once you have clicked on **Create**:</span></span>

    1. <span data-ttu-id="3b7e8-168">Insérez le nom de votre choix pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-168">Insert your desired name for this service instance.</span></span>

    2. <span data-ttu-id="3b7e8-169">Sélectionnez un abonnement.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-169">Select a subscription.</span></span>

    3. <span data-ttu-id="3b7e8-170">Sélectionnez le niveau tarifaire approprié, s’il s’agit de la première fois que vous créez un *Service API visage*, vous devez disposer d’un niveau gratuit (nommé F0).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-170">Select the pricing tier appropriate for you, if this is the first time creating a *Face API Service*, a free tier (named F0) should be available to you.</span></span>

    4. <span data-ttu-id="3b7e8-171">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-171">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="3b7e8-172">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-172">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="3b7e8-173">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-173">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span> 

        > <span data-ttu-id="3b7e8-174">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-174">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5. <span data-ttu-id="3b7e8-175">L’application UWP, **Person Maker**, que vous utilisez ultérieurement, requiert l’utilisation de « West US » pour l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-175">The UWP app, **Person Maker**, which you use later, requires the use of 'West US' for location.</span></span>

    6. <span data-ttu-id="3b7e8-176">Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-176">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    7. <span data-ttu-id="3b7e8-177">Sélectionnez \**créer *.**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-177">Select **Create\*.**</span></span>

        ![créer un service d’API visage](images/AzureLabs-Lab4-03.png)

5.  <span data-ttu-id="3b7e8-179">Une fois que vous avez cliqué sur \**créer *,** vous devez attendre que le service soit créé. cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-179">Once you have clicked on **Create\*,** you will have to wait for the service to be created, this might take a minute.</span></span>

6.  <span data-ttu-id="3b7e8-180">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-180">A notification will appear in the portal once the Service instance is created.</span></span>

    ![notification de création de service](images/AzureLabs-Lab4-04.png)

7.  <span data-ttu-id="3b7e8-182">Cliquez sur les notifications pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-182">Click on the notifications to explore your new Service instance.</span></span>

    ![accéder à la notification de ressource](images/AzureLabs-Lab4-05.png)

8.  <span data-ttu-id="3b7e8-184">Quand vous êtes prêt, cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-184">When you are ready, click **Go to resource** button in the notification to explore your new Service instance.</span></span>

    ![clés d’API de visage d’accès](images/AzureLabs-Lab4-06.png)

9.  <span data-ttu-id="3b7e8-186">Dans ce didacticiel, votre application doit effectuer des appels à votre service, ce qui est effectué via l’utilisation de la « clé » de l’abonnement de votre service.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-186">Within this tutorial, your application will need to make calls to your service, which is done through using your service's subscription 'key'.</span></span> <span data-ttu-id="3b7e8-187">Dans la page *démarrage rapide* de votre service *API visage* , le premier point est le numéro 1, pour *récupérer vos clés.*</span><span class="sxs-lookup"><span data-stu-id="3b7e8-187">From the *Quick start* page, of your *Face API* service, the first point is number 1, to *Grab your keys.*</span></span>

10. <span data-ttu-id="3b7e8-188">Sur la page *service* , sélectionnez le lien hypertexte **touches** bleues (si sur la page démarrage rapide) ou le lien **clés** dans le menu de navigation services (à gauche, indiqué par l’icône « clé »), pour révéler vos clés.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-188">On the *Service* page select either the blue **Keys** hyperlink (if on the Quick start page), or the **Keys** link in the services navigation menu (to the left, denoted by the 'key' icon), to reveal your keys.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3b7e8-189">Prenez note de l’une des clés et protégez-la, car vous en aurez besoin plus tard.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-189">Take note of either one of the keys and safeguard it, as you will need it later.</span></span>

## <a name="chapter-2---using-the-person-maker-uwp-application"></a><span data-ttu-id="3b7e8-190">Chapitre 2-utilisation de l’application UWP « person Maker »</span><span class="sxs-lookup"><span data-stu-id="3b7e8-190">Chapter 2 - Using the 'Person Maker' UWP application</span></span>

<span data-ttu-id="3b7e8-191">Veillez à télécharger l’application UWP prédéfinie appelée [Person Maker](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/PersonMaker.zip).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-191">Make sure to download the prebuilt UWP Application called [Person Maker](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/PersonMaker.zip).</span></span> <span data-ttu-id="3b7e8-192">Cette application n’est pas le produit final de ce cours. il ne s’agit là que d’un outil qui vous aide à créer vos entrées Azure, sur lesquelles repose le projet ultérieur.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-192">This app is not the end product for this course, just a tool to help you create your Azure entries, which the later project will rely upon.</span></span>

<span data-ttu-id="3b7e8-193">**Person Maker** vous permet de créer des entrées Azure, qui sont associées à des personnes et à des groupes de personnes.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-193">**Person Maker** allows you to create Azure entries, which are associated with people, and groups of people.</span></span> <span data-ttu-id="3b7e8-194">L’application place toutes les informations nécessaires dans un format qui peut ensuite être utilisé par le FaceAPI, afin de reconnaître les visages des personnes que vous avez ajoutées.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-194">The application will place all the needed information in a format which can then later be used by the FaceAPI, in order to recognize the faces of people whom you have added.</span></span> 

> <span data-ttu-id="3b7e8-195">PRÉCIEUSE **Person Maker** utilise une limitation de base pour s’assurer que vous ne dépassez pas le nombre d’appels de service par minute pour le **niveau d’abonnement gratuit**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-195">[IMPORTANT] **Person Maker** uses some basic throttling, to help ensure that you do not exceed the number of service calls per minute for the **free subscription tier**.</span></span> <span data-ttu-id="3b7e8-196">Le texte vert en haut devient rouge et met à jour comme « actif » lorsque la limitation se produit ; Si c’est le cas, il vous suffit d’attendre l’application (elle attendra jusqu’à ce qu’elle puisse continuer à accéder au service face, en la mettant à jour comme « en cours » lorsque vous pourrez l’utiliser à nouveau).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-196">The green text at the top will change to red and update as 'ACTIVE' when throttling is happening; if this is the case, simply wait for the application (it will wait until it can next continue accessing the face service, updating as 'IN-ACTIVE' when you can use it again).</span></span>

<span data-ttu-id="3b7e8-197">Cette application utilise les bibliothèques *Microsoft. ProjectOxford. face* , ce qui vous permet de tirer pleinement parti de la API visage.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-197">This application uses the *Microsoft.ProjectOxford.Face* libraries, which will allow you to make full use of the Face API.</span></span> <span data-ttu-id="3b7e8-198">Cette bibliothèque est disponible gratuitement en tant que package NuGet.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-198">This library is available for free as a NuGet Package.</span></span> <span data-ttu-id="3b7e8-199">Pour plus d’informations à ce sujet, et les API similaires, veillez [à consulter l’article de référence sur les API](https://docs.microsoft.com/azure/cognitive-services/face/apireference).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-199">For more information about this, and similar, APIs [make sure to visit the API reference article](https://docs.microsoft.com/azure/cognitive-services/face/apireference).</span></span>

> [!NOTE] 
> <span data-ttu-id="3b7e8-200">Il s’agit uniquement des étapes requises. pour plus d’informations sur la façon de procéder, retrouvez le document.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-200">These are just the steps required, instructions for how to do these things is further down the document.</span></span> <span data-ttu-id="3b7e8-201">L’application **Person Maker** vous permettra d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-201">The **Person Maker** app will allow you to:</span></span>
>
> - <span data-ttu-id="3b7e8-202">Créez un *groupe de personnes*, qui est un groupe composé de plusieurs personnes que vous souhaitez associer à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-202">Create a *Person Group*, which is a group composed of several people which you want to associate with it.</span></span> <span data-ttu-id="3b7e8-203">Avec votre compte Azure, vous pouvez héberger plusieurs groupes de personnes.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-203">With your Azure account you can host multiple Person Groups.</span></span>
>
> - <span data-ttu-id="3b7e8-204">Créez une *personne*, qui est membre d’un groupe de personnes.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-204">Create a *Person*, which is a member of a Person Group.</span></span> <span data-ttu-id="3b7e8-205">Chaque personne est associée à un certain nombre d’images de *face* .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-205">Each person has a number of *Face* images associated with it.</span></span>
>
> -  <span data-ttu-id="3b7e8-206">Attribuez des *images de visage* à une *personne*pour permettre à votre service Azure API visage de reconnaître une *personne* par la *face*correspondante.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-206">Assign *face images* to a *Person*, to allow your Azure Face API Service to recognize a *Person* by the corresponding *face*.</span></span>
>
> -  <span data-ttu-id="3b7e8-207">*Formez votre* *service Azure API visage*.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-207">*Train* your *Azure Face API Service*.</span></span>

<span data-ttu-id="3b7e8-208">N’oubliez pas que pour former cette application et reconnaître des personnes, vous aurez besoin de dix (10) photos proches de chaque personne que vous souhaitez ajouter à votre groupe de personnes.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-208">Be aware, so to train this app to recognize people, you will need ten (10) close-up photos of each person which you would like to add to your Person Group.</span></span> <span data-ttu-id="3b7e8-209">L’application Cam Windows 10 peut vous aider à prendre ces derniers.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-209">The Windows 10 Cam App can help you to take these.</span></span> <span data-ttu-id="3b7e8-210">Vous devez vous assurer que chaque photo est claire (éviter le flou, le masquage ou être trop éloigné, du sujet), que la photo est au format jpg ou png, avec une taille de fichier image supérieure à **4 Mo**et inférieure ou égale à **1 Ko**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-210">You must ensure that each photo is clear (avoid blurring, obscuring, or being too far, from the subject), have the photo in jpg or png file format, with the image file size being no larger **4 MB**, and no less than **1 KB**.</span></span>

> [!NOTE]
> <span data-ttu-id="3b7e8-211">Si vous suivez ce didacticiel, n’utilisez pas votre propre visage pour la formation, comme lorsque vous placez le HoloLens sur, vous ne pouvez pas vous lancer.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-211">If you are following this tutorial, do not use your own face for training, as when you put the HoloLens on, you cannot look at yourself.</span></span> <span data-ttu-id="3b7e8-212">Utilisez le visage d’un collègue ou d’un étudiant.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-212">Use the face of a colleague or fellow student.</span></span>

<span data-ttu-id="3b7e8-213">**Créateur de personne**en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-213">Running **Person Maker**:</span></span>

1.  <span data-ttu-id="3b7e8-214">Ouvrez le dossier **PersonMaker** et double-cliquez sur la *solution PersonMaker* pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-214">Open the **PersonMaker** folder and double click on the *PersonMaker solution* to open it with *Visual Studio*.</span></span>

2.  <span data-ttu-id="3b7e8-215">Une fois la *solution PersonMaker* ouverte, assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-215">Once the *PersonMaker solution* is open, make sure that:</span></span>

    1. <span data-ttu-id="3b7e8-216">La *configuration* de la solution est définie sur **Debug**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-216">The *Solution Configuration* is set to **Debug**.</span></span>

    2. <span data-ttu-id="3b7e8-217">La *plateforme de solution* est définie sur **x86**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-217">The *Solution Platform* is set to **x86**</span></span>

    3. <span data-ttu-id="3b7e8-218">La *plateforme cible* est l' **ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-218">The *Target Platform* is **Local Machine**.</span></span>

    4.  <span data-ttu-id="3b7e8-219">Vous devrez peut-être également *restaurer les packages NuGet* (cliquez avec le bouton droit sur la *solution* et sélectionnez **restaurer les packages NuGet**).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-219">You also may need to *Restore NuGet Packages* (right-click the *Solution* and select **Restore NuGet Packages**).</span></span>

3.  <span data-ttu-id="3b7e8-220">Cliquez sur *ordinateur local* pour démarrer l’application.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-220">Click *Local Machine* and the application will start.</span></span> <span data-ttu-id="3b7e8-221">Sachez que, sur des écrans plus petits, tout le contenu peut ne pas être visible, bien que vous puissiez le faire défiler plus loin pour l’afficher.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-221">Be aware, on smaller screens, all content may not be visible, though you can scroll further down to view it.</span></span>

    ![interface utilisateur person Maker](images/AzureLabs-Lab4-07.png)

4.  <span data-ttu-id="3b7e8-223">Insérez votre **clé d’authentification Azure**, que vous devez avoir, à partir de votre service *API visage* dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-223">Insert your **Azure Authentication Key**, which you should have, from your *Face API* service within Azure.</span></span>

5.  <span data-ttu-id="3b7e8-224">Insérer</span><span class="sxs-lookup"><span data-stu-id="3b7e8-224">Insert:</span></span>

    1. <span data-ttu-id="3b7e8-225">*ID* à affecter au *groupe de personnes*.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-225">The *ID* you want to assign to the *Person Group*.</span></span> <span data-ttu-id="3b7e8-226">L’ID doit être en minuscules, sans espace.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-226">The ID must be lowercase, with no spaces.</span></span> <span data-ttu-id="3b7e8-227">Notez cet ID, car il sera requis plus tard dans votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-227">Make note of this ID, as it will be required later in your Unity project.</span></span>
    2. <span data-ttu-id="3b7e8-228">*Nom* que vous souhaitez attribuer au groupe de *personnes* (peut avoir des espaces).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-228">The *Name* you want to assign to the *Person Group* (can have spaces).</span></span>


6.  <span data-ttu-id="3b7e8-229">Appuyez sur le bouton **créer un groupe de personnes** .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-229">Press **Create Person Group** button.</span></span> <span data-ttu-id="3b7e8-230">Un message de confirmation doit s’afficher sous le bouton.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-230">A confirmation message should appear underneath the button.</span></span>

> [!NOTE]
> <span data-ttu-id="3b7e8-231">Si vous avez une erreur « Accès refusé », vérifiez l’emplacement que vous avez défini pour votre service Azure.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-231">If you have an 'Access Denied' error, check the location you set for your Azure service.</span></span> <span data-ttu-id="3b7e8-232">Comme indiqué ci-dessus, cette application est conçue pour « ouest des États-Unis ».</span><span class="sxs-lookup"><span data-stu-id="3b7e8-232">As stated above, this app is designed for 'West US'.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b7e8-233">Vous remarquerez que vous pouvez également cliquer sur le bouton **récupérer un groupe connu** : Si vous avez déjà créé un groupe de personnes et que vous souhaitez l’utiliser, plutôt que d’en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-233">You will notice that you can also click the **Fetch a Known Group** button: this is for if you have already created a person group, and wish to use that, rather than create a new one.</span></span> <span data-ttu-id="3b7e8-234">Sachez que si vous cliquez sur *créer un groupe de personnes* avec un groupe connu, cela permet également de récupérer un groupe.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-234">Be aware, if you click *Create a Person Group* with a known group, this will also fetch a group.</span></span>

7.  <span data-ttu-id="3b7e8-235">Insérez le *nom* de la *personne* que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-235">Insert the *Name* of the *Person* you want to create.</span></span>

    1. <span data-ttu-id="3b7e8-236">Cliquez sur le bouton **créer une personne** .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-236">Click the **Create Person** button.</span></span>

    2. <span data-ttu-id="3b7e8-237">Un message de confirmation doit s’afficher sous le bouton.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-237">A confirmation message should appear underneath the button.</span></span>

    3. <span data-ttu-id="3b7e8-238">Si vous souhaitez supprimer une personne que vous avez créée précédemment, vous pouvez écrire le nom dans la zone de texte et appuyer sur **Supprimer la personne**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-238">If you wish to delete a person you have previously created, you can write the name into the textbox and press **Delete Person**</span></span>

8.  <span data-ttu-id="3b7e8-239">Assurez-vous de connaître l’emplacement des dix (10) photos de la personne que vous souhaitez ajouter à votre groupe.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-239">Make sure you know the location of ten (10) photos of the person you would like to add to your group.</span></span>

9.  <span data-ttu-id="3b7e8-240">Appuyez sur **créer et ouvrir le dossier** pour ouvrir l’Explorateur Windows dans le dossier associé à la personne.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-240">Press **Create and Open Folder** to open Windows Explorer to the folder associated to the person.</span></span> <span data-ttu-id="3b7e8-241">Ajoutez les dix (10) images dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-241">Add the ten (10) images in the folder.</span></span> <span data-ttu-id="3b7e8-242">Ils doivent être au format de fichier *jpg* ou *png* .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-242">These must be of *JPG* or *PNG* file format.</span></span>

10. <span data-ttu-id="3b7e8-243">Cliquez sur **Envoyer à Azure**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-243">Click on **Submit To Azure**.</span></span> <span data-ttu-id="3b7e8-244">Un compteur vous indique l’état de l’envoi, suivi d’un message lorsqu’il est terminé.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-244">A counter will show you the state of the submission, followed by a message when it has completed.</span></span>

11. <span data-ttu-id="3b7e8-245">Une fois le compteur terminé et un message de confirmation s’affiche, cliquez sur **former** pour former votre service.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-245">Once the counter has finished and a confirmation message has been displayed click on **Train** to train your Service.</span></span>

<span data-ttu-id="3b7e8-246">Une fois le processus terminé, vous êtes prêt à passer à Unity.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-246">Once the process has completed, you are ready to move into Unity.</span></span>

## <a name="chapter-3---set-up-the-unity-project"></a><span data-ttu-id="3b7e8-247">Chapitre 3-configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="3b7e8-247">Chapter 3 - Set up the Unity project</span></span>

<span data-ttu-id="3b7e8-248">Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-248">The following is a typical set up for developing with mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="3b7e8-249">Ouvrez *Unity* et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-249">Open *Unity* and click **New**.</span></span> 

    ![Démarrez le nouveau projet Unity.](images/AzureLabs-Lab4-08.png)

2.  <span data-ttu-id="3b7e8-251">Vous devez maintenant fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-251">You will now need to provide a Unity Project name.</span></span> <span data-ttu-id="3b7e8-252">Insérez **MR_FaceRecognition**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-252">Insert **MR_FaceRecognition**.</span></span> <span data-ttu-id="3b7e8-253">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-253">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="3b7e8-254">Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-254">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="3b7e8-255">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-255">Then, click **Create project**.</span></span>

    ![Fournissez des détails pour le nouveau projet Unity.](images/AzureLabs-Lab4-09.png)

3.  <span data-ttu-id="3b7e8-257">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-257">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="3b7e8-258">Accédez à **modifier > préférences** puis, dans la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-258">Go to **Edit > Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="3b7e8-259">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-259">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="3b7e8-260">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-260">Close the **Preferences** window.</span></span>

    ![Mettre à jour la préférence éditeur de script.](images/AzureLabs-Lab4-10.png)

4.  <span data-ttu-id="3b7e8-262">Accédez ensuite à **fichier > paramètres de build** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton **changer de plateforme** .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-262">Next, go to **File > Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

    ![Fenêtre Paramètres de build, basculez plateforme vers UWP.](images/AzureLabs-Lab4-11.png)

5.  <span data-ttu-id="3b7e8-264">Accédez à **fichier > paramètres de build** et assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-264">Go to **File > Build Settings** and make sure that:</span></span>

    1. <span data-ttu-id="3b7e8-265">L' **appareil cible** est défini sur **HoloLens**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-265">**Target Device** is set to **HoloLens**</span></span>

        > <span data-ttu-id="3b7e8-266">Pour les casques immersifs, définissez **appareil cible** sur *n’importe quel appareil*.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-266">For the immersive headsets, set **Target Device** to *Any Device*.</span></span>

    2. <span data-ttu-id="3b7e8-267">Le **type de build** est **D3D**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-267">**Build Type** is set to **D3D**</span></span>
    3. <span data-ttu-id="3b7e8-268">Le **SDK** est configuré sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-268">**SDK** is set to **Latest installed**</span></span>
    4. <span data-ttu-id="3b7e8-269">**Version de Visual Studio** définie sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-269">**Visual Studio Version** is set to **Latest installed**</span></span>
    5. <span data-ttu-id="3b7e8-270">La **génération et l’exécution** sont définies sur l' **ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-270">**Build and Run** is set to **Local Machine**</span></span>
    6. <span data-ttu-id="3b7e8-271">Enregistrez la scène et ajoutez-la à la Build.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-271">Save the scene and add it to the build.</span></span> 

        1. <span data-ttu-id="3b7e8-272">Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-272">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="3b7e8-273">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-273">A save window will appear.</span></span>

            ![Cliquez sur le bouton Ajouter des scènes ouvertes](images/AzureLabs-Lab4-12.png)

        2. <span data-ttu-id="3b7e8-275">Sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez-le **scenes**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-275">Select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![Créer un dossier de scripts](images/AzureLabs-Lab4-13.png)

        3. <span data-ttu-id="3b7e8-277">Ouvrez le dossier **scenes** nouvellement créé, puis dans le champ **nom de fichier**:, tapez **FaceRecScene**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-277">Open your newly created **Scenes** folder, and then in the **File name**: text field, type **FaceRecScene**, then press **Save**.</span></span>

            ![Donnez un nom à la nouvelle scène.](images/AzureLabs-Lab4-14.png)

    7. <span data-ttu-id="3b7e8-279">Les paramètres restants, dans *paramètres de build*, doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-279">The remaining settings, in *Build Settings*, should be left as default for now.</span></span>

6. <span data-ttu-id="3b7e8-280">Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-280">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span> 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab4-15.png)

7. <span data-ttu-id="3b7e8-282">Dans ce volet, quelques paramètres doivent être vérifiés :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-282">In this panel, a few settings need to be verified:</span></span>

    1. <span data-ttu-id="3b7e8-283">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-283">In the **Other Settings** tab:</span></span>

        1. <span data-ttu-id="3b7e8-284">La **version du runtime** de **script** doit être **expérimentale** (équivalent .net 4,6).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-284">**Scripting** **Runtime Version** should be **Experimental** (.NET 4.6 Equivalent).</span></span> <span data-ttu-id="3b7e8-285">La modification de cette opération déclenche un besoin de redémarrage de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-285">Changing this will trigger a need to restart the Editor.</span></span>
        2. <span data-ttu-id="3b7e8-286">Le **backend de script** doit être **.net**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-286">**Scripting Backend** should be **.NET**</span></span>
        3. <span data-ttu-id="3b7e8-287">Le **niveau de compatibilité** de l’API doit être **.net 4,6**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-287">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![Mettez à jour d’autres paramètres.](images/AzureLabs-Lab4-16.png)
      
    2. <span data-ttu-id="3b7e8-289">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-289">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="3b7e8-290">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-290">**InternetClient**</span></span>
        - <span data-ttu-id="3b7e8-291">**Webcam**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-291">**Webcam**</span></span>

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab4-17.png)

    3. <span data-ttu-id="3b7e8-293">Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-293">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Mettez à jour les paramètres X R.](images/AzureLabs-Lab4-18.png)

8.  <span data-ttu-id="3b7e8-295">De retour dans les *paramètres de build*, les  **C# projets Unity** ne sont plus grisés. Cochez la case en regard de cette option.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-295">Back in *Build Settings*, **Unity C# Projects** is no longer greyed out; tick the checkbox next to this.</span></span> 
9.  <span data-ttu-id="3b7e8-296">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-296">Close the Build Settings window.</span></span>
10. <span data-ttu-id="3b7e8-297">Enregistrez votre scène et votre projet (**fichier > enregistrer la scène/le fichier > enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-297">Save your Scene and Project (**FILE > SAVE SCENE / FILE > SAVE PROJECT**).</span></span>

## <a name="chapter-4---main-camera-setup"></a><span data-ttu-id="3b7e8-298">Chapitre 4-Configuration de l’appareil photo principal</span><span class="sxs-lookup"><span data-stu-id="3b7e8-298">Chapter 4 - Main Camera setup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b7e8-299">Si vous souhaitez ignorer le composant *Unity* configure de ce cours et continuer directement dans le code, n’hésitez pas à [Télécharger ce fichier. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/Azure-MR-304.unitypackage)et à l’importer dans votre projet en tant que [package personnalisé](https://docs.unity3d.com/Manual/AssetPackages.html).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-299">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to [download this .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/Azure-MR-304.unitypackage), and import it into your project as a [Custom Package](https://docs.unity3d.com/Manual/AssetPackages.html).</span></span> <span data-ttu-id="3b7e8-300">Sachez que ce package comprend également l’importation de la *dll Newtonsoft*, traitée dans le [Chapitre 5](#chapter-5--import-the-newtonsoftjson-library).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-300">Be aware that this package also includes the import of the *Newtonsoft DLL*, covered in [Chapter 5](#chapter-5--import-the-newtonsoftjson-library).</span></span> <span data-ttu-id="3b7e8-301">Une fois cette importation effectuée, vous pouvez passer [au chapitre 6](#chapter-6---create-the-faceanalysis-class).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-301">With this imported, you can continue from [Chapter 6](#chapter-6---create-the-faceanalysis-class).</span></span>

1.  <span data-ttu-id="3b7e8-302">Dans le panneau *hiérarchie* , sélectionnez l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-302">In the *Hierarchy* Panel, select the **Main Camera**.</span></span>

2.  <span data-ttu-id="3b7e8-303">Une fois sélectionné, vous pouvez voir tous les composants de la **caméra principale** dans le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-303">Once selected, you will be able to see all the components of the **Main Camera** in the *Inspector Panel*.</span></span>

    1. <span data-ttu-id="3b7e8-304">L' **objet Camera** doit être nommé **Camera main** (Notez l’orthographe !)</span><span class="sxs-lookup"><span data-stu-id="3b7e8-304">The **Camera object** must be named **Main Camera** (note the spelling!)</span></span>

    2. <span data-ttu-id="3b7e8-305">La **balise** principale de l’appareil photo doit être définie sur **MainCamera** (Notez l’orthographe !)</span><span class="sxs-lookup"><span data-stu-id="3b7e8-305">The Main Camera **Tag** must be set to **MainCamera** (note the spelling!)</span></span>

    3. <span data-ttu-id="3b7e8-306">Vérifiez que la **position** de la transformation est définie sur **0, 0,** 0</span><span class="sxs-lookup"><span data-stu-id="3b7e8-306">Make sure the **Transform Position** is set to **0, 0, 0**</span></span>

    4. <span data-ttu-id="3b7e8-307">Définir des **indicateurs clairs** sur **couleur unie**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-307">Set **Clear Flags** to **Solid Color**</span></span>

    5. <span data-ttu-id="3b7e8-308">Définir la couleur d' **arrière-plan** du composant Camera sur **Black, alpha 0 (Code hexadécimal : #00000000)**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-308">Set the **Background** Color of the Camera Component to **Black, Alpha 0 (Hex Code: #00000000)**</span></span>

        ![configurer les composants de l’appareil photo](images/AzureLabs-Lab4-19.png) 

## <a name="chapter-5--import-the-newtonsoftjson-library"></a><span data-ttu-id="3b7e8-310">Chapitre 5-importer la bibliothèque Newtonsoft. JSON</span><span class="sxs-lookup"><span data-stu-id="3b7e8-310">Chapter 5 – Import the Newtonsoft.Json library</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b7e8-311">Si vous avez importé le « . pour Unity » dans le [dernier chapitre](#chapter-4---main-camera-setup), vous pouvez ignorer ce chapitre.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-311">If you imported the '.unitypackage' in the [last Chapter](#chapter-4---main-camera-setup), you can skip this Chapter.</span></span>

<span data-ttu-id="3b7e8-312">Pour vous aider à désérialiser et à sérialiser les objets reçus et envoyés au service bot, vous devez télécharger la bibliothèque *Newtonsoft. JSON* .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-312">To help you deserialize and serialize objects received and sent to the Bot Service you need to download the *Newtonsoft.Json* library.</span></span> <span data-ttu-id="3b7e8-313">Vous trouverez une version compatible déjà organisée avec la structure de dossiers Unity correcte dans ce [fichier de package Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/newtonsoftDLL.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-313">You will find a compatible version already organized with the correct Unity folder structure in this [Unity package file](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/newtonsoftDLL.unitypackage).</span></span> 

<span data-ttu-id="3b7e8-314">Pour importer la bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-314">To import the library:</span></span>

1.  <span data-ttu-id="3b7e8-315">Téléchargez le package Unity.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-315">Download the Unity Package.</span></span>
2.  <span data-ttu-id="3b7e8-316">Cliquez sur **composants**, **Importer un package**, **package personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-316">Click on **Assets**, **Import Package**, **Custom Package**.</span></span>

    ![Importer la bibliothèque Newtonsoft. JSON](images/AzureLabs-Lab4-20.png)

3.  <span data-ttu-id="3b7e8-318">Recherchez le package Unity que vous avez téléchargé, puis cliquez sur Ouvrir.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-318">Look for the Unity Package you have downloaded, and click Open.</span></span>
4.  <span data-ttu-id="3b7e8-319">Assurez-vous que tous les composants du package sont cochés et cliquez sur **Importer**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-319">Make sure all the components of the package are ticked and click **Import**.</span></span>

    ![Importer la bibliothèque Newtonsoft. JSON](images/AzureLabs-Lab4-21.png)

## <a name="chapter-6---create-the-faceanalysis-class"></a><span data-ttu-id="3b7e8-321">Chapitre 6-créer la classe FaceAnalysis</span><span class="sxs-lookup"><span data-stu-id="3b7e8-321">Chapter 6 - Create the FaceAnalysis class</span></span>

<span data-ttu-id="3b7e8-322">L’objectif de la classe FaceAnalysis est d’héberger les méthodes nécessaires pour communiquer avec votre service de reconnaissance faciale Azure.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-322">The purpose of the FaceAnalysis class is to host the methods necessary to communicate with your Azure Face Recognition Service.</span></span> 

- <span data-ttu-id="3b7e8-323">Une fois que le service a envoyé une image de capture, il l’analyse et identifie les visages dans et détermine s’il appartient à une personne connue.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-323">After sending the service a capture image, it will analyse it and identify the faces within, and determine if any belong to a known person.</span></span> 
- <span data-ttu-id="3b7e8-324">Si une personne connue est trouvée, cette classe affiche son nom en tant que texte de l’interface utilisateur dans la scène.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-324">If a known person is found, this class will display its name as UI text in the scene.</span></span>

<span data-ttu-id="3b7e8-325">Pour créer la classe *FaceAnalysis* :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-325">To create the *FaceAnalysis* class:</span></span>

 1. <span data-ttu-id="3b7e8-326">Cliquez avec le bouton droit dans le *dossier ressources* situé dans le panneau projet, puis cliquez sur **créer** un **dossier**de > .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-326">Right-click in the *Assets Folder* located in the Project Panel, then click on **Create** > **Folder**.</span></span> <span data-ttu-id="3b7e8-327">Appelez le dossier **scripts**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-327">Call the folder **Scripts**.</span></span> 

    ![Créez la classe FaceAnalysis.](images/AzureLabs-Lab4-22.png)

2.  <span data-ttu-id="3b7e8-329">Double-cliquez sur le dossier que vous venez de créer pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-329">Double click on the folder just created, to open it.</span></span> 
3.  <span data-ttu-id="3b7e8-330">Cliquez avec le bouton droit dans le dossier, puis cliquez sur **créer** >  **C# script**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-330">Right-click inside the folder, then click on **Create** > **C# Script**.</span></span> <span data-ttu-id="3b7e8-331">Appelez le script *FaceAnalysis*.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-331">Call the script *FaceAnalysis*.</span></span> 
4.  <span data-ttu-id="3b7e8-332">Double-cliquez sur le nouveau script *FaceAnalysis* pour l’ouvrir avec Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-332">Double click on the new *FaceAnalysis* script to open it with Visual Studio 2017.</span></span>
5.  <span data-ttu-id="3b7e8-333">Entrez les espaces de noms suivants au-dessus de la classe *FaceAnalysis* :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-333">Enter the following namespaces above the *FaceAnalysis* class:</span></span>

    ```csharp
        using Newtonsoft.Json;
        using System.Collections;
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

6.  <span data-ttu-id="3b7e8-334">Vous devez maintenant ajouter tous les objets qui sont utilisés pour deserialising.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-334">You now need to add all of the objects which are used for deserialising.</span></span> <span data-ttu-id="3b7e8-335">Ces objets doivent être ajoutés **en dehors** du script *FaceAnalysis* (sous l’accolade inférieure).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-335">These objects need to be added **outside** of the *FaceAnalysis* script (beneath the bottom curly bracket).</span></span> 

    ```csharp
        /// <summary>
        /// The Person Group object
        /// </summary>
        public class Group_RootObject
        {
            public string personGroupId { get; set; }
            public string name { get; set; }
            public object userData { get; set; }
        }

        /// <summary>
        /// The Person Face object
        /// </summary>
        public class Face_RootObject
        {
            public string faceId { get; set; }
        }

        /// <summary>
        /// Collection of faces that needs to be identified
        /// </summary>
        public class FacesToIdentify_RootObject
        {
            public string personGroupId { get; set; }
            public List<string> faceIds { get; set; }
            public int maxNumOfCandidatesReturned { get; set; }
            public double confidenceThreshold { get; set; }
        }

        /// <summary>
        /// Collection of Candidates for the face
        /// </summary>
        public class Candidate_RootObject
        {
            public string faceId { get; set; }
            public List<Candidate> candidates { get; set; }
        }

        public class Candidate
        {
            public string personId { get; set; }
            public double confidence { get; set; }
        }

        /// <summary>
        /// Name and Id of the identified Person
        /// </summary>
        public class IdentifiedPerson_RootObject
        {
            public string personId { get; set; }
            public string name { get; set; }
        }
    ```
7. <span data-ttu-id="3b7e8-336">Les méthodes *Start ()* et *Update ()* ne seront pas utilisées. Supprimez-les maintenant.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-336">The *Start()* and *Update()* methods will not be used, so delete them now.</span></span> 

8.  <span data-ttu-id="3b7e8-337">À l’intérieur de la classe *FaceAnalysis* , ajoutez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-337">Inside the *FaceAnalysis* class, add the following variables:</span></span>

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static FaceAnalysis Instance;

        /// <summary>
        /// The analysis result text
        /// </summary>
        private TextMesh labelText;

        /// <summary>
        /// Bytes of the image captured with camera
        /// </summary>
        internal byte[] imageBytes;

        /// <summary>
        /// Path of the image captured with camera
        /// </summary>
        internal string imagePath;

        /// <summary>
        /// Base endpoint of Face Recognition Service
        /// </summary>
        const string baseEndpoint = "https://westus.api.cognitive.microsoft.com/face/v1.0/";

        /// <summary>
        /// Auth key of Face Recognition Service
        /// </summary>
        private const string key = "- Insert your key here -";

        /// <summary>
        /// Id (name) of the created person group 
        /// </summary>
        private const string personGroupId = "- Insert your group Id here -";
    ```

    > [!NOTE]
    > <span data-ttu-id="3b7e8-338">Remplacez la **clé** et le **PersonGroupId** par votre clé de service et l’ID du groupe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-338">Replace the **key** and the **personGroupId** with your Service Key and the Id of the group that you created previously.</span></span>

9.  <span data-ttu-id="3b7e8-339">Ajoutez la méthode *éveillé ()* , qui initialise la classe, en ajoutant la classe *ImageCapture* à la caméra principale et en appelant la méthode de création d’étiquette :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-339">Add the *Awake()* method, which initialises the class, adding the *ImageCapture* class to the Main Camera and calls the Label creation method:</span></span>

    ```csharp
        /// <summary>
        /// Initialises this class
        /// </summary>
        private void Awake()
        {
            // Allows this instance to behave like a singleton
            Instance = this;

            // Add the ImageCapture Class to this Game Object
            gameObject.AddComponent<ImageCapture>();

            // Create the text label in the scene
            CreateLabel();
        }
    ```

10. <span data-ttu-id="3b7e8-340">Ajoutez la méthode *CreateLabel ()* , qui crée l’objet *label* pour afficher le résultat de l’analyse :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-340">Add the *CreateLabel()* method, which creates the *Label* object to display the analysis result:</span></span>

    ```csharp
        /// <summary>
        /// Spawns cursor for the Main Camera
        /// </summary>
        private void CreateLabel()
        {
            // Create a sphere as new cursor
            GameObject newLabel = new GameObject();

            // Attach the label to the Main Camera
            newLabel.transform.parent = gameObject.transform;
            
            // Resize and position the new cursor
            newLabel.transform.localScale = new Vector3(0.4f, 0.4f, 0.4f);
            newLabel.transform.position = new Vector3(0f, 3f, 60f);

            // Creating the text of the Label
            labelText = newLabel.AddComponent<TextMesh>();
            labelText.anchor = TextAnchor.MiddleCenter;
            labelText.alignment = TextAlignment.Center;
            labelText.tabSize = 4;
            labelText.fontSize = 50;
            labelText.text = ".";       
        }
    ```

11. <span data-ttu-id="3b7e8-341">Ajoutez la méthode *DetectFacesFromImage ()* et *GetImageAsByteArray ()* .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-341">Add the *DetectFacesFromImage()* and *GetImageAsByteArray()* method.</span></span> <span data-ttu-id="3b7e8-342">La première demande au service de reconnaissance faciale de détecter tout visage possible dans l’image envoyée, tandis que ce dernier est nécessaire pour convertir l’image capturée en un tableau d’octets :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-342">The former will request the Face Recognition Service to detect any possible face in the submitted image, while the latter is necessary to convert the captured image into a bytes array:</span></span>

    ```csharp
        /// <summary>
        /// Detect faces from a submitted image
        /// </summary>
        internal IEnumerator DetectFacesFromImage()
        {
            WWWForm webForm = new WWWForm();
            string detectFacesEndpoint = $"{baseEndpoint}detect";

            // Change the image into a bytes array
            imageBytes = GetImageAsByteArray(imagePath);

            using (UnityWebRequest www = 
                UnityWebRequest.Post(detectFacesEndpoint, webForm))
            {
                www.SetRequestHeader("Ocp-Apim-Subscription-Key", key);
                www.SetRequestHeader("Content-Type", "application/octet-stream");
                www.uploadHandler.contentType = "application/octet-stream";
                www.uploadHandler = new UploadHandlerRaw(imageBytes);
                www.downloadHandler = new DownloadHandlerBuffer();

                yield return www.SendWebRequest();
                string jsonResponse = www.downloadHandler.text;
                Face_RootObject[] face_RootObject = 
                    JsonConvert.DeserializeObject<Face_RootObject[]>(jsonResponse);

                List<string> facesIdList = new List<string>();
                // Create a list with the face Ids of faces detected in image
                foreach (Face_RootObject faceRO in face_RootObject)
                {
                    facesIdList.Add(faceRO.faceId);
                    Debug.Log($"Detected face - Id: {faceRO.faceId}");
                }
                
                StartCoroutine(IdentifyFaces(facesIdList));
            }
        }

        /// <summary>
        /// Returns the contents of the specified file as a byte array.
        /// </summary>
        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
            BinaryReader binaryReader = new BinaryReader(fileStream);
            return binaryReader.ReadBytes((int)fileStream.Length);
        }
    ```

12. <span data-ttu-id="3b7e8-343">Ajoutez la méthode *IdentifyFaces ()* , qui demande au *service de reconnaissance faciale* d’identifier toute face connue précédemment détectée dans l’image soumise.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-343">Add the *IdentifyFaces()* method, which requests the *Face Recognition Service* to identify any known face previously detected in the submitted image.</span></span> <span data-ttu-id="3b7e8-344">La demande retourne un ID de la personne identifiée, mais pas le nom :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-344">The request will return an id of the identified person but not the name:</span></span>

    ```csharp
        /// <summary>
        /// Identify the faces found in the image within the person group
        /// </summary>
        internal IEnumerator IdentifyFaces(List<string> listOfFacesIdToIdentify)
        {
            // Create the object hosting the faces to identify
            FacesToIdentify_RootObject facesToIdentify = new FacesToIdentify_RootObject();
            facesToIdentify.faceIds = new List<string>();
            facesToIdentify.personGroupId = personGroupId;
            foreach (string facesId in listOfFacesIdToIdentify)
            {
                facesToIdentify.faceIds.Add(facesId);
            }
            facesToIdentify.maxNumOfCandidatesReturned = 1;
            facesToIdentify.confidenceThreshold = 0.5;

            // Serialise to Json format
            string facesToIdentifyJson = JsonConvert.SerializeObject(facesToIdentify);
            // Change the object into a bytes array
            byte[] facesData = Encoding.UTF8.GetBytes(facesToIdentifyJson);

            WWWForm webForm = new WWWForm();
            string detectFacesEndpoint = $"{baseEndpoint}identify";

            using (UnityWebRequest www = UnityWebRequest.Post(detectFacesEndpoint, webForm))
            {
                www.SetRequestHeader("Ocp-Apim-Subscription-Key", key);
                www.SetRequestHeader("Content-Type", "application/json");
                www.uploadHandler.contentType = "application/json";
                www.uploadHandler = new UploadHandlerRaw(facesData);
                www.downloadHandler = new DownloadHandlerBuffer();

                yield return www.SendWebRequest();
                string jsonResponse = www.downloadHandler.text;
                Debug.Log($"Get Person - jsonResponse: {jsonResponse}");
                Candidate_RootObject [] candidate_RootObject = JsonConvert.DeserializeObject<Candidate_RootObject[]>(jsonResponse);

                // For each face to identify that ahs been submitted, display its candidate
                foreach (Candidate_RootObject candidateRO in candidate_RootObject)
                {
                    StartCoroutine(GetPerson(candidateRO.candidates[0].personId));
                    
                    // Delay the next "GetPerson" call, so all faces candidate are displayed properly
                    yield return new WaitForSeconds(3);
                }           
            }
        }
    ```

13. <span data-ttu-id="3b7e8-345">Ajoutez la méthode *GetPerson ()* .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-345">Add the *GetPerson()* method.</span></span> <span data-ttu-id="3b7e8-346">En fournissant l’ID de personne, cette méthode demande au *service de reconnaissance faciale* de retourner le nom de la personne identifiée :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-346">By providing the person id, this method then requests for the *Face Recognition Service* to return the name of the identified person:</span></span>

    ```csharp
        /// <summary>
        /// Provided a personId, retrieve the person name associated with it
        /// </summary>
        internal IEnumerator GetPerson(string personId)
        {
            string getGroupEndpoint = $"{baseEndpoint}persongroups/{personGroupId}/persons/{personId}?";
            WWWForm webForm = new WWWForm();

            using (UnityWebRequest www = UnityWebRequest.Get(getGroupEndpoint))
            {
                www.SetRequestHeader("Ocp-Apim-Subscription-Key", key);
                www.downloadHandler = new DownloadHandlerBuffer();
                yield return www.SendWebRequest();
                string jsonResponse = www.downloadHandler.text;

                Debug.Log($"Get Person - jsonResponse: {jsonResponse}");
                IdentifiedPerson_RootObject identifiedPerson_RootObject = JsonConvert.DeserializeObject<IdentifiedPerson_RootObject>(jsonResponse);

                // Display the name of the person in the UI
                labelText.text = identifiedPerson_RootObject.name;
            }
        }
    ```

14.  <span data-ttu-id="3b7e8-347">N’oubliez pas d' **Enregistrer** les modifications avant de revenir à l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-347">Remember to **Save** the changes before going back to the Unity Editor.</span></span>
15.  <span data-ttu-id="3b7e8-348">Dans l’éditeur Unity, faites glisser le script FaceAnalysis du dossier scripts du panneau projet vers l’objet caméra principal dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-348">In the Unity Editor, drag the FaceAnalysis script from the Scripts folder in Project panel to the Main Camera object in the *Hierarchy panel*.</span></span> <span data-ttu-id="3b7e8-349">Le nouveau composant script sera ajouté à la caméra principale.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-349">The new script component will be so added to the Main Camera.</span></span> 

![Placer FaceAnalysis sur l’appareil photo principal](images/AzureLabs-Lab4-23.png)


## <a name="chapter-7---create-the-imagecapture-class"></a><span data-ttu-id="3b7e8-351">Chapitre 7-créer la classe ImageCapture</span><span class="sxs-lookup"><span data-stu-id="3b7e8-351">Chapter 7 - Create the ImageCapture class</span></span>

<span data-ttu-id="3b7e8-352">L’objectif de la classe *ImageCapture* est d’héberger les méthodes nécessaires pour communiquer avec votre *service de reconnaissance faciale Azure* afin d’analyser l’image que vous allez capturer, d’identifier les visages et de déterminer si elle appartient à une personne connue.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-352">The purpose of the *ImageCapture* class is to host the methods necessary to communicate with your *Azure Face Recognition Service* to analyse the image you will capture, identifying faces in it and determining if it belongs to a known person.</span></span> <span data-ttu-id="3b7e8-353">Si une personne connue est trouvée, cette classe affiche son nom en tant que texte de l’interface utilisateur dans la scène.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-353">If a known person is found, this class will display its name as UI text in the scene.</span></span>

<span data-ttu-id="3b7e8-354">Pour créer la classe *ImageCapture* :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-354">To create the *ImageCapture* class:</span></span>
 
1.  <span data-ttu-id="3b7e8-355">Cliquez avec le bouton droit dans le dossier **scripts** que vous avez créé précédemment, puis cliquez sur **créer**,  **C# script**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-355">Right-click inside the **Scripts** folder you have created previously, then click on **Create**, **C# Script**.</span></span> <span data-ttu-id="3b7e8-356">Appelez le script *ImageCapture*.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-356">Call the script *ImageCapture*.</span></span> 
2.  <span data-ttu-id="3b7e8-357">Double-cliquez sur le nouveau script *ImageCapture* pour l’ouvrir avec Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-357">Double click on the new *ImageCapture* script to open it with Visual Studio 2017.</span></span>
3.  <span data-ttu-id="3b7e8-358">Entrez les espaces de noms suivants au-dessus de la classe ImageCapture :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-358">Enter the following namespaces above the ImageCapture class:</span></span>

    ```csharp
        using System.IO;
        using System.Linq;
        using UnityEngine;
        using UnityEngine.XR.WSA.Input;
        using UnityEngine.XR.WSA.WebCam;
    ```

4.  <span data-ttu-id="3b7e8-359">À l’intérieur de la classe *ImageCapture* , ajoutez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-359">Inside the *ImageCapture* class, add the following variables:</span></span>

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static ImageCapture instance;

        /// <summary>
        /// Keeps track of tapCounts to name the captured images 
        /// </summary>
        private int tapsCount;

        /// <summary>
        /// PhotoCapture object used to capture images on HoloLens 
        /// </summary>
        private PhotoCapture photoCaptureObject = null;

        /// <summary>
        /// HoloLens class to capture user gestures
        /// </summary>
        private GestureRecognizer recognizer;
    ```

5.  <span data-ttu-id="3b7e8-360">Ajoutez les méthodes *éveillé ()* et *Start ()* nécessaires à l’initialisation de la classe et autorisez le HoloLens à capturer les mouvements de l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-360">Add the *Awake()* and *Start()* methods necessary to initialise the class and allow the HoloLens to capture the user's gestures:</span></span>

    ```csharp
        /// <summary>
        /// Initialises this class
        /// </summary>
        private void Awake()
        {
            instance = this;
        }

        /// <summary>
        /// Called right after Awake
        /// </summary>
        void Start()
        {
            // Initialises user gestures capture 
            recognizer = new GestureRecognizer();
            recognizer.SetRecognizableGestures(GestureSettings.Tap);
            recognizer.Tapped += TapHandler;
            recognizer.StartCapturingGestures();
        }
    ```

6.  <span data-ttu-id="3b7e8-361">Ajoutez le *TapHandler ()* qui est appelé lorsque l’utilisateur effectue un mouvement *Tap* :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-361">Add the *TapHandler()* which is called when the user performs a *Tap* gesture:</span></span>

    ```csharp
        /// <summary>
        /// Respond to Tap Input.
        /// </summary>
        private void TapHandler(TappedEventArgs obj)
        {
            tapsCount++;
            ExecuteImageCaptureAndAnalysis();
        }
    ```

7.  <span data-ttu-id="3b7e8-362">Ajoutez la méthode *ExecuteImageCaptureAndAnalysis ()* , qui va commencer le processus de capture d’image :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-362">Add the *ExecuteImageCaptureAndAnalysis()* method, which will begin the process of Image Capturing:</span></span>

    ```csharp
        /// <summary>
        /// Begin process of Image Capturing and send To Azure Computer Vision service.
        /// </summary>
        private void ExecuteImageCaptureAndAnalysis()
        {
            Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending
                ((res) => res.width * res.height).First();
            Texture2D targetTexture = new Texture2D(cameraResolution.width, cameraResolution.height);

            PhotoCapture.CreateAsync(false, delegate (PhotoCapture captureObject)
            {
                photoCaptureObject = captureObject;

                CameraParameters c = new CameraParameters();
                c.hologramOpacity = 0.0f;
                c.cameraResolutionWidth = targetTexture.width;
                c.cameraResolutionHeight = targetTexture.height;
                c.pixelFormat = CapturePixelFormat.BGRA32;

                captureObject.StartPhotoModeAsync(c, delegate (PhotoCapture.PhotoCaptureResult result)
                {
                    string filename = string.Format(@"CapturedImage{0}.jpg", tapsCount);
                    string filePath = Path.Combine(Application.persistentDataPath, filename);

                    // Set the image path on the FaceAnalysis class
                    FaceAnalysis.Instance.imagePath = filePath;

                    photoCaptureObject.TakePhotoAsync
                    (filePath, PhotoCaptureFileOutputFormat.JPG, OnCapturedPhotoToDisk);
                });
            });
        }
    ```

8.  <span data-ttu-id="3b7e8-363">Ajoutez les gestionnaires qui sont appelés lorsque le processus de capture de photos est terminé :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-363">Add the handlers that are called when the photo capture process has been completed:</span></span>

    ```csharp
        /// <summary>
        /// Called right after the photo capture process has concluded
        /// </summary>
        void OnCapturedPhotoToDisk(PhotoCapture.PhotoCaptureResult result)
        {
            photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
        }

        /// <summary>
        /// Register the full execution of the Photo Capture. If successfull, it will begin the Image Analysis process.
        /// </summary>
        void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
        {
            photoCaptureObject.Dispose();
            photoCaptureObject = null;

            // Request image caputer analysis
            StartCoroutine(FaceAnalysis.Instance.DetectFacesFromImage());
        }
    ```

9. <span data-ttu-id="3b7e8-364">N’oubliez pas d' **Enregistrer** les modifications avant de revenir à l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-364">Remember to **Save** the changes before going back to the Unity Editor.</span></span>

## <a name="chapter-8---building-the-solution"></a><span data-ttu-id="3b7e8-365">Chapitre 8-génération de la solution</span><span class="sxs-lookup"><span data-stu-id="3b7e8-365">Chapter 8 - Building the solution</span></span>

<span data-ttu-id="3b7e8-366">Pour effectuer un test minutieux de votre application, vous devez l’chargement sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-366">To perform a thorough test of your application you will need to sideload it onto your HoloLens.</span></span>

<span data-ttu-id="3b7e8-367">Avant cela, assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-367">Before you do, ensure that:</span></span>

-   <span data-ttu-id="3b7e8-368">Tous les paramètres mentionnés dans le chapitre 3 sont correctement définis.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-368">All the settings mentioned in the Chapter 3 are set correctly.</span></span> 
-   <span data-ttu-id="3b7e8-369">Le script *FaceAnalysis* est attaché à l’objet Camera principal.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-369">The script *FaceAnalysis* is attached to the Main Camera object.</span></span> 
-   <span data-ttu-id="3b7e8-370">La **clé d’authentification** et l' **ID de groupe** ont été définis dans le script *FaceAnalysis* .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-370">Both the **Auth Key** and **Group Id** have been set within the *FaceAnalysis* script.</span></span>

<span data-ttu-id="3b7e8-371">R ce point vous êtes prêt à générer la solution.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-371">A this point you are ready to build the Solution.</span></span> <span data-ttu-id="3b7e8-372">Une fois la solution générée, vous êtes prêt à déployer votre application.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-372">Once the Solution has been built, you will be ready to deploy your application.</span></span>

<span data-ttu-id="3b7e8-373">Pour commencer le processus de génération :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-373">To begin the Build process:</span></span>

1.  <span data-ttu-id="3b7e8-374">Enregistrez la scène en cours en cliquant sur fichier, puis sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-374">Save the current scene by clicking on File, Save.</span></span>
2.  <span data-ttu-id="3b7e8-375">Accédez à fichier, paramètres de build, puis cliquez sur Ajouter des scènes ouvertes.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-375">Go to File, Build Settings, click on Add Open Scenes.</span></span>
3.  <span data-ttu-id="3b7e8-376">Veillez à cocher C# les projets Unity.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-376">Make sure to tick Unity C# Projects.</span></span>

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab4-24.png)

4.  <span data-ttu-id="3b7e8-378">Appuyez sur générer.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-378">Press Build.</span></span> <span data-ttu-id="3b7e8-379">Dans ce cas, Unity lance une fenêtre de l’Explorateur de fichiers, où vous devez créer, puis sélectionner un dossier dans lequel créer l’application.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-379">Upon doing so, Unity will launch a File Explorer window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="3b7e8-380">Créez ce dossier maintenant, dans le projet Unity, et appelez-le.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-380">Create that folder now, within the Unity project, and call it App.</span></span> <span data-ttu-id="3b7e8-381">Ensuite, avec le dossier d’application sélectionné, appuyez sur Sélectionner un dossier.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-381">Then with the App folder selected, press Select Folder.</span></span> 
5.  <span data-ttu-id="3b7e8-382">Unity commence à générer votre projet, en dehors du dossier de l’application.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-382">Unity will begin building your project, out to the App folder.</span></span> 
6.  <span data-ttu-id="3b7e8-383">Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l’Explorateur de fichiers s’ouvre à l’emplacement de votre Build.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-383">Once Unity has finished building (it might take some time), it will open a File Explorer window at the location of your build.</span></span>

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab4-25.png)

7.  <span data-ttu-id="3b7e8-385">Ouvrez le dossier de votre application, puis ouvrez la solution nouveau projet (comme indiqué ci-dessus, MR_FaceRecognition. sln).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-385">Open your App folder, and then open the new Project Solution (as seen above, MR_FaceRecognition.sln).</span></span>


## <a name="chapter-9---deploying-your-application"></a><span data-ttu-id="3b7e8-386">Chapitre 9-déploiement de votre application</span><span class="sxs-lookup"><span data-stu-id="3b7e8-386">Chapter 9 - Deploying your application</span></span>

<span data-ttu-id="3b7e8-387">Pour effectuer un déploiement sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-387">To deploy on HoloLens:</span></span>

1.  <span data-ttu-id="3b7e8-388">Vous aurez besoin de l’adresse IP de votre HoloLens (pour le déploiement à distance) et vérifiez que votre HoloLens est en **mode développeur**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-388">You will need the IP Address of your HoloLens (for Remote Deploy), and to ensure your HoloLens is in **Developer Mode**.</span></span> <span data-ttu-id="3b7e8-389">Pour cela, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-389">To do this:</span></span>

    1. <span data-ttu-id="3b7e8-390">Tout en portant votre HoloLens, ouvrez les **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-390">Whilst wearing your HoloLens, open the **Settings**.</span></span>
    2. <span data-ttu-id="3b7e8-391">Accéder au **réseau & Internet > Wi-Fi > options avancées**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-391">Go to **Network & Internet > Wi-Fi > Advanced Options**</span></span>
    3. <span data-ttu-id="3b7e8-392">Notez l’adresse **IPv4** .</span><span class="sxs-lookup"><span data-stu-id="3b7e8-392">Note the **IPv4** address.</span></span>
    4. <span data-ttu-id="3b7e8-393">Ensuite, revenez aux **paramètres**, puis à **mettre à jour & > de sécurité pour les développeurs**</span><span class="sxs-lookup"><span data-stu-id="3b7e8-393">Next, navigate back to **Settings**, and then to **Update & Security > For Developers**</span></span> 
    5. <span data-ttu-id="3b7e8-394">Définissez le mode développeur sur.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-394">Set Developer Mode On.</span></span>

2.  <span data-ttu-id="3b7e8-395">Accédez à votre nouvelle build Unity (le dossier de l' *application* ) et ouvrez le fichier solution avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-395">Navigate to your new Unity build (the *App* folder) and open the solution file with *Visual Studio*.</span></span>
3.  <span data-ttu-id="3b7e8-396">Dans la configuration de la solution, sélectionnez **Déboguer**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-396">In the Solution Configuration select **Debug**.</span></span>
4.  <span data-ttu-id="3b7e8-397">Dans la plateforme de la solution, sélectionnez **x86**, **ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-397">In the Solution Platform, select **x86**, **Remote Machine**.</span></span> 

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab4-26.png)
 
5.  <span data-ttu-id="3b7e8-399">Accédez au **menu Générer** , puis cliquez sur **déployer la solution**pour chargement l’application à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-399">Go to the **Build menu** and click on **Deploy Solution**, to sideload the application to your HoloLens.</span></span>
6.  <span data-ttu-id="3b7e8-400">Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prête à être lancée.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-400">Your App should now appear in the list of installed apps on your HoloLens, ready to be launched!</span></span>

> [!NOTE]
> <span data-ttu-id="3b7e8-401">Pour effectuer un déploiement sur un casque immersif, définissez la plateforme de la **solution** sur *ordinateur local*et définissez la **configuration** sur *Déboguer*, avec *x86* comme **plateforme**.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-401">To deploy to immersive headset, set the **Solution Platform** to *Local Machine*, and set the **Configuration** to *Debug*, with *x86* as the **Platform**.</span></span> <span data-ttu-id="3b7e8-402">Déployez ensuite sur l’ordinateur local, à l’aide du **menu Générer**, en sélectionnant *déployer la solution*.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-402">Then deploy to the local machine, using the **Build menu**, selecting *Deploy Solution*.</span></span> 


## <a name="chapter-10---using-the-application"></a><span data-ttu-id="3b7e8-403">Chapitre 10-utilisation de l’application</span><span class="sxs-lookup"><span data-stu-id="3b7e8-403">Chapter 10 - Using the application</span></span>

1.  <span data-ttu-id="3b7e8-404">Porter le HoloLens, lancer l’application.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-404">Wearing the HoloLens, launch the app.</span></span>
2.  <span data-ttu-id="3b7e8-405">Examinez la personne que vous avez inscrite auprès du *API visage*.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-405">Look at the person that you have registered with the *Face API*.</span></span> <span data-ttu-id="3b7e8-406">Vérifiez que :</span><span class="sxs-lookup"><span data-stu-id="3b7e8-406">Make sure that:</span></span>

    -  <span data-ttu-id="3b7e8-407">Le visage de la personne n’est pas trop éloigné et clairement visible</span><span class="sxs-lookup"><span data-stu-id="3b7e8-407">The person's face is not too distant and clearly visible</span></span>
    -  <span data-ttu-id="3b7e8-408">L’éclairage de l’environnement n’est pas trop sombre</span><span class="sxs-lookup"><span data-stu-id="3b7e8-408">The environment lighting is not too dark</span></span>

3.  <span data-ttu-id="3b7e8-409">Utilisez le geste TAP pour capturer l’image de la personne.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-409">Use the tap gesture to capture the person's picture.</span></span>
4.  <span data-ttu-id="3b7e8-410">Attendez que l’application envoie la demande d’analyse et que vous receviez une réponse.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-410">Wait for the App to send the analysis request and receive a response.</span></span>
5.  <span data-ttu-id="3b7e8-411">Si la personne a été correctement reconnue, le nom de la personne s’affiche comme texte de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-411">If the person has been successfully recognized, the person's name will appear as UI text.</span></span>
6.  <span data-ttu-id="3b7e8-412">Vous pouvez répéter le processus de capture à l’aide du geste TAP (TAP) toutes les quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-412">You can repeat the capture process using the tap gesture every few seconds.</span></span>

## <a name="your-finished-azure-face-api-application"></a><span data-ttu-id="3b7e8-413">Votre application Azure API Visage terminée</span><span class="sxs-lookup"><span data-stu-id="3b7e8-413">Your finished Azure Face API Application</span></span>

<span data-ttu-id="3b7e8-414">Félicitations, vous avez créé une application de réalité mixte qui tire parti du service de reconnaissance faciale Azure pour détecter les visages au sein d’une image et identifier les visages connus.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-414">Congratulations, you built a mixed reality app that leverages the Azure Face Recognition service to detect faces within an image, and identify any known faces.</span></span>

![résultat de la fin de ce cours](images/AzureLabs-Lab4-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="3b7e8-416">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="3b7e8-416">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="3b7e8-417">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="3b7e8-417">Exercise 1</span></span>

<span data-ttu-id="3b7e8-418">Le **API visage Azure** est suffisamment puissant pour détecter jusqu’à 64 faces dans une image unique.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-418">The **Azure Face API** is powerful enough to detect up to 64 faces in a single image.</span></span> <span data-ttu-id="3b7e8-419">Étendez l’application afin qu’elle puisse reconnaître deux ou trois visages, parmi de nombreuses autres personnes.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-419">Extend the application, so that it could recognize two or three faces, amongst many other people.</span></span>

### <a name="exercise-2"></a><span data-ttu-id="3b7e8-420">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="3b7e8-420">Exercise 2</span></span>

<span data-ttu-id="3b7e8-421">Le **API visage Azure** est également en mesure de fournir toutes sortes d’informations sur les attributs.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-421">The **Azure Face API** is also able to provide back all kinds of attribute information.</span></span> <span data-ttu-id="3b7e8-422">Intégrez cela dans l’application.</span><span class="sxs-lookup"><span data-stu-id="3b7e8-422">Integrate this into the application.</span></span> <span data-ttu-id="3b7e8-423">Cela peut être encore plus intéressant, lorsqu’il est associé au [API émotion](https://azure.microsoft.com/services/cognitive-services/emotion/).</span><span class="sxs-lookup"><span data-stu-id="3b7e8-423">This could be even more interesting, when combined with the [Emotion API](https://azure.microsoft.com/services/cognitive-services/emotion/).</span></span>
