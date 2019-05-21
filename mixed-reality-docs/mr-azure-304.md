---
title: MR et Azure 304 - reconnaissance faciale
description: Terminer ce cours pour apprendre à implémenter la reconnaissance faciale de Azure au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, mixte réalité academy, unity, didacticiel, api, face à la reconnaissance, vr immersives, hololens,
ms.openlocfilehash: 6330d3e5c51d6b2cbc43ea795a3f953a5b14d6f1
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596466"
---
>[!NOTE]
><span data-ttu-id="9a6f6-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="9a6f6-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="9a6f6-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="9a6f6-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="9a6f6-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="9a6f6-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br> 

# <a name="mr-and-azure-304-face-recognition"></a><span data-ttu-id="9a6f6-110">MR et Azure 304 : Reconnaissance faciale</span><span class="sxs-lookup"><span data-stu-id="9a6f6-110">MR and Azure 304: Face recognition</span></span>

![résultat de cette formation](images/AzureLabs-Lab4-00.png)

<span data-ttu-id="9a6f6-112">Dans ce cours vous allez apprendre à ajouter des fonctionnalités de reconnaissance de face à une application de réalité mixte, à l’aide d’Azure Cognitive Services, avec l’API visage de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-112">In this course you will learn how to add face recognition capabilities to a mixed reality application, using Azure Cognitive Services, with the Microsoft Face API.</span></span>

<span data-ttu-id="9a6f6-113">*Azure API visage* est un service Microsoft, qui fournit aux développeurs avec les algorithmes de reconnaissance faciale plus avancées, tout cela dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-113">*Azure Face API* is a Microsoft service, which provides developers with the most advanced face algorithms, all in the cloud.</span></span> <span data-ttu-id="9a6f6-114">Le *API visage* a deux fonctions principales : détection avec des attributs de visage et doivent faire face de reconnaissance.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-114">The *Face API* has two main functions: face detection with attributes, and face recognition.</span></span> <span data-ttu-id="9a6f6-115">Cela permet aux développeurs de simplement définir un ensemble de groupes de visages et ensuite, envoyez des images de la requête au service ultérieurement, pour déterminer auxquels appartient un visage.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-115">This allows developers to simply set a set of groups for faces, and then, send query images to the service later, to determine to whom a face belongs.</span></span> <span data-ttu-id="9a6f6-116">Pour plus d’informations, visitez le [page de reconnaissance faciale de Azure](https://azure.microsoft.com/services/cognitive-services/face/).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-116">For more information, visit the [Azure Face Recognition page](https://azure.microsoft.com/services/cognitive-services/face/).</span></span>

<span data-ttu-id="9a6f6-117">Avoir terminé ce cours, vous aurez une réalité mixte application HoloLens, qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-117">Having completed this course, you will have a mixed reality HoloLens application, which will be able to do the following:</span></span>

1. <span data-ttu-id="9a6f6-118">Utilisez un **appuyez sur le mouvement** pour initier la capture d’une image à l’aide de la caméra HoloLens intégrée.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-118">Use a **Tap Gesture** to initiate the capture of an image using the on-board HoloLens camera.</span></span> 
2. <span data-ttu-id="9a6f6-119">Envoyer l’image capturée à le *API visage de Azure* service.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-119">Send the captured image to the *Azure Face API* service.</span></span>
3. <span data-ttu-id="9a6f6-120">Recevoir les résultats de la *API visage* algorithme.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-120">Receive the results of the *Face API* algorithm.</span></span>
4. <span data-ttu-id="9a6f6-121">Utiliser une Interface utilisateur simple, pour afficher le nom des personnes mise en correspondance.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-121">Use a simple User Interface, to display the name of matched people.</span></span>

<span data-ttu-id="9a6f6-122">Cela va vous apprendre à obtenir les résultats à partir du Service d’API visage dans votre application basée sur Unity de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-122">This will teach you how to get the results from the Face API Service into your Unity-based mixed reality application.</span></span>

<span data-ttu-id="9a6f6-123">Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-123">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="9a6f6-124">Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-124">This course is designed to teach you how to integrate an Azure Service with your Unity Project.</span></span> <span data-ttu-id="9a6f6-125">Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-125">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

## <a name="device-support"></a><span data-ttu-id="9a6f6-126">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="9a6f6-126">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="9a6f6-127">Cours</span><span class="sxs-lookup"><span data-stu-id="9a6f6-127">Course</span></span></th><th style="width:150px"> <span data-ttu-id="9a6f6-128"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="9a6f6-128"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="9a6f6-129"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="9a6f6-129"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="9a6f6-130">MR et Azure 304 : Reconnaissance faciale</span><span class="sxs-lookup"><span data-stu-id="9a6f6-130">MR and Azure 304: Face recognition</span></span></td><td style="text-align: center;"> <span data-ttu-id="9a6f6-131">✔️</span><span class="sxs-lookup"><span data-stu-id="9a6f6-131">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="9a6f6-132">✔️</span><span class="sxs-lookup"><span data-stu-id="9a6f6-132">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="9a6f6-133">Si ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques Windows Mixed Reality IMMERSIFS (VR).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-133">While this course primarily focuses on HoloLens, you can also apply what you learn in this course to Windows Mixed Reality immersive (VR) headsets.</span></span> <span data-ttu-id="9a6f6-134">Étant donné que des casques IMMERSIFS (VR) ne sont pas accessibles caméras, vous devez une caméra externe connectée à votre PC.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-134">Because immersive (VR) headsets do not have accessible cameras, you will need an external camera connected to your PC.</span></span> <span data-ttu-id="9a6f6-135">Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge des casques IMMERSIFS (VR).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-135">As you follow along with the course, you will see notes on any changes you might need to employ to support immersive (VR) headsets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a6f6-136">Prérequis</span><span class="sxs-lookup"><span data-stu-id="9a6f6-136">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="9a6f6-137">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-137">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="9a6f6-138">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-138">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="9a6f6-139">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous .</span><span class="sxs-lookup"><span data-stu-id="9a6f6-139">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="9a6f6-140">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-140">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="9a6f6-141">Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)</span><span class="sxs-lookup"><span data-stu-id="9a6f6-141">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="9a6f6-142">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="9a6f6-142">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md)
- [<span data-ttu-id="9a6f6-143">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="9a6f6-143">The latest Windows 10 SDK</span></span>](install-the-tools.md)
- [<span data-ttu-id="9a6f6-144">Unity 2017.4</span><span class="sxs-lookup"><span data-stu-id="9a6f6-144">Unity 2017.4</span></span>](install-the-tools.md)
- [<span data-ttu-id="9a6f6-145">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9a6f6-145">Visual Studio 2017</span></span>](install-the-tools.md)
- <span data-ttu-id="9a6f6-146">Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="9a6f6-146">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="9a6f6-147">Un appareil photo connecté à votre PC (pour le développement de casque immersives)</span><span class="sxs-lookup"><span data-stu-id="9a6f6-147">A camera connected to your PC (for immersive headset development)</span></span>
- <span data-ttu-id="9a6f6-148">Accès à Internet pour le programme d’installation Azure et l’extraction de l’API visage</span><span class="sxs-lookup"><span data-stu-id="9a6f6-148">Internet access for Azure setup and Face API retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="9a6f6-149">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9a6f6-149">Before you start</span></span>

1.  <span data-ttu-id="9a6f6-150">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-150">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="9a6f6-151">Configurer et tester votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-151">Set up and test your HoloLens.</span></span> <span data-ttu-id="9a6f6-152">Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-152">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span> 
3.  <span data-ttu-id="9a6f6-153">Il est judicieux d’effectuer l’étalonnage et le réglage de capteur lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-153">It is a good idea to perform Calibration and Sensor Tuning when beginning developing a new HoloLens App (sometimes it can help to perform those tasks for each user).</span></span> 

<span data-ttu-id="9a6f6-154">Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-154">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens).</span></span>

<span data-ttu-id="9a6f6-155">Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-155">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

## <a name="chapter-1---the-azure-portal"></a><span data-ttu-id="9a6f6-156">Chapitre 1 : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="9a6f6-156">Chapter 1 - The Azure Portal</span></span>

<span data-ttu-id="9a6f6-157">Pour utiliser le *API visage* service dans Azure, vous devez configurer une instance du service à être mis à disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-157">To use the *Face API* service in Azure, you will need to configure an instance of the service to be made available to your application.</span></span>

1.  <span data-ttu-id="9a6f6-158">Tout d’abord, connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-158">First, log in to the [Azure Portal](https://portal.azure.com).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="9a6f6-159">Si vous n’avez pas déjà un compte Azure, vous devrez créer un.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-159">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="9a6f6-160">Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-160">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="9a6f6-161">Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez *API visage*, appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-161">Once you are logged in, click on **New** in the top left corner, and search for *Face API*, press **Enter**.</span></span>

    ![Rechercher des api visage](images/AzureLabs-Lab4-01.png)

    > [!NOTE]
    > <span data-ttu-id="9a6f6-163">Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-163">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

3.  <span data-ttu-id="9a6f6-164">La nouvelle page doit fournir une description de la *API visage* service.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-164">The new page will provide a description of the *Face API* service.</span></span> <span data-ttu-id="9a6f6-165">En bas à gauche de cette invite, sélectionnez le **créer** bouton permettant de créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-165">At the bottom left of this prompt, select the **Create** button, to create an association with this service.</span></span>

    ![doivent faire face les informations sur l’api](images/AzureLabs-Lab4-02.png)

4.  <span data-ttu-id="9a6f6-167">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="9a6f6-167">Once you have clicked on **Create**:</span></span>

    1. <span data-ttu-id="9a6f6-168">Insérez votre nom souhaité pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-168">Insert your desired name for this service instance.</span></span>

    2. <span data-ttu-id="9a6f6-169">Sélectionnez un abonnement.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-169">Select a subscription.</span></span>

    3. <span data-ttu-id="9a6f6-170">Sélectionnez le niveau de tarification approprié pour vous, si c’est la première heure de création d’un *Service de l’API visage*, un niveau gratuit (nommé F0) doit être disponible pour vous.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-170">Select the pricing tier appropriate for you, if this is the first time creating a *Face API Service*, a free tier (named F0) should be available to you.</span></span>

    4. <span data-ttu-id="9a6f6-171">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-171">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="9a6f6-172">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-172">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="9a6f6-173">Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-173">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span> 

        > <span data-ttu-id="9a6f6-174">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-174">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5. <span data-ttu-id="9a6f6-175">L’application UWP, **personne Maker**, que vous utilisez une version ultérieure, requiert l’utilisation de « Ouest des États-Unis » pour l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-175">The UWP app, **Person Maker**, which you use later, requires the use of 'West US' for location.</span></span>

    6. <span data-ttu-id="9a6f6-176">Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-176">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    7. <span data-ttu-id="9a6f6-177">Sélectionnez **créer\*.**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-177">Select **Create\*.**</span></span>

        ![Créer face service api](images/AzureLabs-Lab4-03.png)

5.  <span data-ttu-id="9a6f6-179">Une fois que vous avez cliqué sur **créer**\* avoir à attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-179">Once you have clicked on **Create\*,** you will have to wait for the service to be created, this might take a minute.</span></span>

6.  <span data-ttu-id="9a6f6-180">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-180">A notification will appear in the portal once the Service instance is created.</span></span>

    ![notification de création de service](images/AzureLabs-Lab4-04.png)

7.  <span data-ttu-id="9a6f6-182">Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-182">Click on the notifications to explore your new Service instance.</span></span>

    ![Accédez à la notification de ressource](images/AzureLabs-Lab4-05.png)

8.  <span data-ttu-id="9a6f6-184">Lorsque vous êtes prêt, cliquez sur **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-184">When you are ready, click **Go to resource** button in the notification to explore your new Service instance.</span></span>

    ![accès doivent faire face les clés api](images/AzureLabs-Lab4-06.png)

9.  <span data-ttu-id="9a6f6-186">Dans ce didacticiel, votre application devra effectuer des appels à votre service, par l’intermédiaire à l’aide de l’abonnement de votre service 'key'.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-186">Within this tutorial, your application will need to make calls to your service, which is done through using your service's subscription 'key'.</span></span> <span data-ttu-id="9a6f6-187">À partir de la *Guide de démarrage rapide* page, de votre *API visage* de service, le premier point est le numéro 1, à *récupérez vos clés.*</span><span class="sxs-lookup"><span data-stu-id="9a6f6-187">From the *Quick start* page, of your *Face API* service, the first point is number 1, to *Grab your keys.*</span></span>

10. <span data-ttu-id="9a6f6-188">Sur le *Service* page Sélectionnez soit le bleu **clés** hyperlink (le cas sur la page de démarrage rapide), ou le **clés** lien dans le menu de navigation de services (à gauche, désigné par le ' clé ' icône), pour afficher vos clés.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-188">On the *Service* page select either the blue **Keys** hyperlink (if on the Quick start page), or the **Keys** link in the services navigation menu (to the left, denoted by the 'key' icon), to reveal your keys.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a6f6-189">Prenez note de l’une des clés et à la sauvegarde, car vous en aurez besoin plus tard.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-189">Take note of either one of the keys and safeguard it, as you will need it later.</span></span>

## <a name="chapter-2---using-the-person-maker-uwp-application"></a><span data-ttu-id="9a6f6-190">Chapitre 2 : à l’aide de l’application de la « Personne Maker » UWP</span><span class="sxs-lookup"><span data-stu-id="9a6f6-190">Chapter 2 - Using the 'Person Maker' UWP application</span></span>

<span data-ttu-id="9a6f6-191">Veillez à télécharger l’Application UWP prédéfini appelé [personne Maker](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/PersonMaker.zip).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-191">Make sure to download the prebuilt UWP Application called [Person Maker](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/PersonMaker.zip).</span></span> <span data-ttu-id="9a6f6-192">Cette application n’est pas le produit final de ce cours, un simple outil pour vous aider à créer vos entrées de Azure, le projet ultérieur se basent sur.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-192">This app is not the end product for this course, just a tool to help you create your Azure entries, which the later project will rely upon.</span></span>

<span data-ttu-id="9a6f6-193">**Personne Maker** vous permet de créer les entrées Azure, qui sont associées à des personnes et groupes d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-193">**Person Maker** allows you to create Azure entries, which are associated with people, and groups of people.</span></span> <span data-ttu-id="9a6f6-194">L’application place toutes les informations nécessaires dans un format qui peut ensuite être utilisé ultérieurement par le FaceAPI, afin de reconnaître les visages des personnes auxquelles vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-194">The application will place all the needed information in a format which can then later be used by the FaceAPI, in order to recognize the faces of people whom you have added.</span></span> 

> <span data-ttu-id="9a6f6-195">[IMPORTANT] **Personne Maker** utilise une limitation base, afin de garantir que vous ne dépassez pas le nombre d’appels de service par minute pour le **niveau d’abonnement gratuit**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-195">[IMPORTANT] **Person Maker** uses some basic throttling, to help ensure that you do not exceed the number of service calls per minute for the **free subscription tier**.</span></span> <span data-ttu-id="9a6f6-196">Le texte vert en haut modifie en rouge et mettre à jour « Active » lors de la limitation s’applique ; Si c’est le cas, attendez simplement l’application (il attend jusqu'à ce qu’il peut ensuite continuer d’accéder au service de visage, la mise à jour « IN-active » lorsque vous pouvez l’utiliser à nouveau).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-196">The green text at the top will change to red and update as 'ACTIVE' when throttling is happening; if this is the case, simply wait for the application (it will wait until it can next continue accessing the face service, updating as 'IN-ACTIVE' when you can use it again).</span></span>

<span data-ttu-id="9a6f6-197">Cette application utilise le *Microsoft.ProjectOxford.Face* utilisent des bibliothèques, ce qui vous permet de rendre complet de l’API visage.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-197">This application uses the *Microsoft.ProjectOxford.Face* libraries, which will allow you to make full use of the Face API.</span></span> <span data-ttu-id="9a6f6-198">Cette bibliothèque est disponible gratuitement en tant qu’un NuGet Package.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-198">This library is available for free as a NuGet Package.</span></span> <span data-ttu-id="9a6f6-199">Pour plus d’informations sur ce point et est similaire, API [veillez à consulter l’article de référence API](https://docs.microsoft.com/azure/cognitive-services/face/apireference).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-199">For more information about this, and similar, APIs [make sure to visit the API reference article](https://docs.microsoft.com/azure/cognitive-services/face/apireference).</span></span>

> [!NOTE] 
> <span data-ttu-id="9a6f6-200">Il s’agit simplement les étapes requises, des instructions pour savoir comment effectuer les opérations suivantes est plus bas dans le document.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-200">These are just the steps required, instructions for how to do these things is further down the document.</span></span> <span data-ttu-id="9a6f6-201">Le **personne Maker** application vous permettra de :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-201">The **Person Maker** app will allow you to:</span></span>
>
> - <span data-ttu-id="9a6f6-202">Créer un *groupe de personnes*, qui est un groupe composé de plusieurs personnes que vous souhaitez lui associer.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-202">Create a *Person Group*, which is a group composed of several people which you want to associate with it.</span></span> <span data-ttu-id="9a6f6-203">Avec votre compte Azure, vous pouvez héberger plusieurs groupes de personnes.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-203">With your Azure account you can host multiple Person Groups.</span></span>
>
> - <span data-ttu-id="9a6f6-204">Créer un *personne*, qui est un membre d’un groupe de personnes.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-204">Create a *Person*, which is a member of a Person Group.</span></span> <span data-ttu-id="9a6f6-205">Chaque personne dispose d’un nombre de *Face* images associées.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-205">Each person has a number of *Face* images associated with it.</span></span>
>
> -  <span data-ttu-id="9a6f6-206">Affecter *doivent faire face les images* à un *personne*pour permettre à votre Service d’API visage Azure de reconnaître un *personne* par correspondant *face*.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-206">Assign *face images* to a *Person*, to allow your Azure Face API Service to recognize a *Person* by the corresponding *face*.</span></span>
>
> -  <span data-ttu-id="9a6f6-207">*Train* votre *Azure doivent faire Face les API Service*.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-207">*Train* your *Azure Face API Service*.</span></span>

<span data-ttu-id="9a6f6-208">Sachez, pour former à reconnaître les personnes de cette application, vous devez en gros plan photos dix (10) de chaque personne pour laquelle vous souhaitez ajouter à votre groupe de personnes.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-208">Be aware, so to train this app to recognize people, you will need ten (10) close-up photos of each person which you would like to add to your Person Group.</span></span> <span data-ttu-id="9a6f6-209">L’application de FAO Windows 10 peuvent vous aider à prendre ceux-ci.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-209">The Windows 10 Cam App can help you to take these.</span></span> <span data-ttu-id="9a6f6-210">Vous devez vous assurer que chaque photo est désactivée (évitez flou, en masquant ou en cours trop loin, à partir de l’objet), ont la photo au format jpg ou png, avec la taille du fichier image en cours ne dépassant **4 Mo**et pas moins de **1 Ko**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-210">You must ensure that each photo is clear (avoid blurring, obscuring, or being too far, from the subject), have the photo in jpg or png file format, with the image file size being no larger **4 MB**, and no less than **1 KB**.</span></span>

> [!NOTE]
> <span data-ttu-id="9a6f6-211">Si vous suivez ce didacticiel, n’utilisez pas votre propre image pour l’apprentissage, comme quand vous placez le HoloLens, vous ne pouvez pas regarder vous-même.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-211">If you are following this tutorial, do not use your own face for training, as when you put the HoloLens on, you cannot look at yourself.</span></span> <span data-ttu-id="9a6f6-212">Utilisez la face d’un collègue ou fellow étudiant.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-212">Use the face of a colleague or fellow student.</span></span>

<span data-ttu-id="9a6f6-213">En cours d’exécution **personne Maker**:</span><span class="sxs-lookup"><span data-stu-id="9a6f6-213">Running **Person Maker**:</span></span>

1.  <span data-ttu-id="9a6f6-214">Ouvrez le **PersonMaker** dossier et double cliquez sur le *PersonMaker solution* pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-214">Open the **PersonMaker** folder and double click on the *PersonMaker solution* to open it with *Visual Studio*.</span></span>

2.  <span data-ttu-id="9a6f6-215">Une fois le *PersonMaker solution* est ouvert, assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-215">Once the *PersonMaker solution* is open, make sure that:</span></span>

    1. <span data-ttu-id="9a6f6-216">Le *Configuration de la Solution* a la valeur **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-216">The *Solution Configuration* is set to **Debug**.</span></span>

    2. <span data-ttu-id="9a6f6-217">Le *plateforme de Solution* a la valeur **x86**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-217">The *Solution Platform* is set to **x86**</span></span>

    3. <span data-ttu-id="9a6f6-218">Le *plateforme cible* est **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-218">The *Target Platform* is **Local Machine**.</span></span>

    4.  <span data-ttu-id="9a6f6-219">Vous devrez peut-être également *restaurer les Packages NuGet* (avec le bouton droit le *Solution* et sélectionnez **restaurer les Packages NuGet**).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-219">You also may need to *Restore NuGet Packages* (right-click the *Solution* and select **Restore NuGet Packages**).</span></span>

3.  <span data-ttu-id="9a6f6-220">Cliquez sur *ordinateur Local* et démarre l’application.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-220">Click *Local Machine* and the application will start.</span></span> <span data-ttu-id="9a6f6-221">N’oubliez pas, sur les petits écrans, tout le contenu n’est pas forcément visible, bien que vous pouvez faire défiler plus bas pour l’afficher.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-221">Be aware, on smaller screens, all content may not be visible, though you can scroll further down to view it.</span></span>

    ![interface utilisateur personne maker](images/AzureLabs-Lab4-07.png)

4.  <span data-ttu-id="9a6f6-223">Insérez votre **clé d’authentification Azure**, qui doit avoir, à partir de votre *API visage* service dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-223">Insert your **Azure Authentication Key**, which you should have, from your *Face API* service within Azure.</span></span>

5.  <span data-ttu-id="9a6f6-224">Insertion :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-224">Insert:</span></span>

    1. <span data-ttu-id="9a6f6-225">Le *ID* vous souhaitez affecter à la *groupe de personnes*.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-225">The *ID* you want to assign to the *Person Group*.</span></span> <span data-ttu-id="9a6f6-226">L’ID doit être en minuscules, sans espaces.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-226">The ID must be lowercase, with no spaces.</span></span> <span data-ttu-id="9a6f6-227">Notez cet ID, car il sera requis plus loin dans votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-227">Make note of this ID, as it will be required later in your Unity project.</span></span>
    2. <span data-ttu-id="9a6f6-228">Le *nom* vous souhaitez affecter à la *groupe de personnes* (peut avoir des espaces).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-228">The *Name* you want to assign to the *Person Group* (can have spaces).</span></span>


6.  <span data-ttu-id="9a6f6-229">Appuyez sur **créer un groupe de personnes** bouton.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-229">Press **Create Person Group** button.</span></span> <span data-ttu-id="9a6f6-230">Un message de confirmation doit apparaître sous le bouton.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-230">A confirmation message should appear underneath the button.</span></span>

> [!NOTE]
> <span data-ttu-id="9a6f6-231">Si vous avez une erreur « Accès refusé », vérifiez l’emplacement que vous définissez pour votre service Azure.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-231">If you have an 'Access Denied' error, check the location you set for your Azure service.</span></span> <span data-ttu-id="9a6f6-232">Comme indiqué ci-dessus, cette application est conçue pour les États-Unis de l’ouest.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-232">As stated above, this app is designed for 'West US'.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a6f6-233">Vous remarquerez que vous pouvez également cliquer sur le **extraire un groupe connu** bouton : il s’agit de si vous avez déjà créé une personne, groupe et qui souhaitent utiliser, plutôt que de créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-233">You will notice that you can also click the **Fetch a Known Group** button: this is for if you have already created a person group, and wish to use that, rather than create a new one.</span></span> <span data-ttu-id="9a6f6-234">N’oubliez pas, si vous cliquez sur *créer un groupe de personnes* avec un groupe connu, cette opération va également extraire un groupe.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-234">Be aware, if you click *Create a Person Group* with a known group, this will also fetch a group.</span></span>

7.  <span data-ttu-id="9a6f6-235">Insérer le *nom* de la *personne* vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-235">Insert the *Name* of the *Person* you want to create.</span></span>

    1. <span data-ttu-id="9a6f6-236">Cliquez sur le **personne créer** bouton.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-236">Click the **Create Person** button.</span></span>

    2. <span data-ttu-id="9a6f6-237">Un message de confirmation doit apparaître sous le bouton.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-237">A confirmation message should appear underneath the button.</span></span>

    3. <span data-ttu-id="9a6f6-238">Si vous souhaitez supprimer une personne que vous avez créé précédemment, vous pouvez écrire le nom dans la zone de texte et appuyez sur **supprimer la personne**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-238">If you wish to delete a person you have previously created, you can write the name into the textbox and press **Delete Person**</span></span>

8.  <span data-ttu-id="9a6f6-239">Assurez-vous que vous connaissez l’emplacement de photos dix (10) de la personne que vous souhaitez ajouter à votre groupe.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-239">Make sure you know the location of ten (10) photos of the person you would like to add to your group.</span></span>

9.  <span data-ttu-id="9a6f6-240">Appuyez sur **créer et ouvrir le dossier** pour ouvrir l’Explorateur Windows dans le dossier associé à la personne.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-240">Press **Create and Open Folder** to open Windows Explorer to the folder associated to the person.</span></span> <span data-ttu-id="9a6f6-241">Ajoutez les images de dix (10) dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-241">Add the ten (10) images in the folder.</span></span> <span data-ttu-id="9a6f6-242">Elles doivent être *JPG* ou *PNG* format de fichier.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-242">These must be of *JPG* or *PNG* file format.</span></span>

10. <span data-ttu-id="9a6f6-243">Cliquez sur **envoyer sur Azure**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-243">Click on **Submit To Azure**.</span></span> <span data-ttu-id="9a6f6-244">Un compteur vous montrera l’état de l’envoi, suivi d’un message lorsqu’il se termine.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-244">A counter will show you the state of the submission, followed by a message when it has completed.</span></span>

11. <span data-ttu-id="9a6f6-245">Une fois que le compteur est terminée et un message de confirmation a été affiché, cliquez sur **former** pour l’apprentissage de votre Service.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-245">Once the counter has finished and a confirmation message has been displayed click on **Train** to train your Service.</span></span>

<span data-ttu-id="9a6f6-246">Une fois le processus terminé, vous êtes prêt à passer dans Unity.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-246">Once the process has completed, you are ready to move into Unity.</span></span>

## <a name="chapter-3---set-up-the-unity-project"></a><span data-ttu-id="9a6f6-247">Chapitre 3 - configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="9a6f6-247">Chapter 3 - Set up the Unity project</span></span>

<span data-ttu-id="9a6f6-248">Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-248">The following is a typical set up for developing with mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="9a6f6-249">Ouvrez *Unity* et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-249">Open *Unity* and click **New**.</span></span> 

    ![Démarrer un nouveau projet Unity.](images/AzureLabs-Lab4-08.png)

2.  <span data-ttu-id="9a6f6-251">Maintenant, vous devez fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-251">You will now need to provide a Unity Project name.</span></span> <span data-ttu-id="9a6f6-252">Insérer **MR_FaceRecognition**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-252">Insert **MR_FaceRecognition**.</span></span> <span data-ttu-id="9a6f6-253">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-253">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="9a6f6-254">Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-254">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="9a6f6-255">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-255">Then, click **Create project**.</span></span>

    ![Fournissent des détails pour un projet Unity.](images/AzureLabs-Lab4-09.png)

3.  <span data-ttu-id="9a6f6-257">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-257">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="9a6f6-258">Accédez à **Modifier > Préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-258">Go to **Edit > Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="9a6f6-259">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-259">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="9a6f6-260">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-260">Close the **Preferences** window.</span></span>

    ![Mettre à jour les préférences de l’éditeur de script.](images/AzureLabs-Lab4-10.png)

4.  <span data-ttu-id="9a6f6-262">Ensuite, accédez à **fichier > Paramètres de Build** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **plateforme basculer** bouton.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-262">Next, go to **File > Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

    ![Fenêtre Paramètres, plateforme de commutation à UWP de la génération.](images/AzureLabs-Lab4-11.png)

5.  <span data-ttu-id="9a6f6-264">Accédez à **fichier > Paramètres de Build** et vous assurer que :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-264">Go to **File > Build Settings** and make sure that:</span></span>

    1. <span data-ttu-id="9a6f6-265">**Équipement cible** a la valeur **HoloLens**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-265">**Target Device** is set to **HoloLens**</span></span>

        > <span data-ttu-id="9a6f6-266">Pour des casques IMMERSIFS, définissez **appareil cible** à *n’importe quel appareil*.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-266">For the immersive headsets, set **Target Device** to *Any Device*.</span></span>

    2. <span data-ttu-id="9a6f6-267">**Type de build** a la valeur **D3D**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-267">**Build Type** is set to **D3D**</span></span>
    3. <span data-ttu-id="9a6f6-268">**Kit de développement logiciel** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-268">**SDK** is set to **Latest installed**</span></span>
    4. <span data-ttu-id="9a6f6-269">**Version de Visual Studio** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-269">**Visual Studio Version** is set to **Latest installed**</span></span>
    5. <span data-ttu-id="9a6f6-270">**Générez et exécutez** est défini sur **ordinateur Local**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-270">**Build and Run** is set to **Local Machine**</span></span>
    6. <span data-ttu-id="9a6f6-271">Enregistrer la scène et l’ajouter à la build.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-271">Save the scene and add it to the build.</span></span> 

        1. <span data-ttu-id="9a6f6-272">Cela en sélectionnant **ajouter un arrière-plan Open**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-272">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="9a6f6-273">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-273">A save window will appear.</span></span>

            ![Cliquez sur Ajouter un bouton scènes ouvert](images/AzureLabs-Lab4-12.png)

        2. <span data-ttu-id="9a6f6-275">Sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-275">Select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![Créer un nouveau dossier de scripts](images/AzureLabs-Lab4-13.png)

        3. <span data-ttu-id="9a6f6-277">Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le **nom de fichier**: champ de texte, tapez **FaceRecScene**, puis appuyez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-277">Open your newly created **Scenes** folder, and then in the **File name**: text field, type **FaceRecScene**, then press **Save**.</span></span>

            ![Donnez un nom à nouvelle scène.](images/AzureLabs-Lab4-14.png)

    7. <span data-ttu-id="9a6f6-279">Les autres paramètres, dans *paramètres de Build*, doit être conservé comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-279">The remaining settings, in *Build Settings*, should be left as default for now.</span></span>

6. <span data-ttu-id="9a6f6-280">Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-280">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span> 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab4-15.png)

7. <span data-ttu-id="9a6f6-282">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-282">In this panel, a few settings need to be verified:</span></span>

    1. <span data-ttu-id="9a6f6-283">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-283">In the **Other Settings** tab:</span></span>

        1. <span data-ttu-id="9a6f6-284">**Écriture de scripts** **Version du Runtime** doit être **expérimental** (équivalent .NET 4.6).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-284">**Scripting** **Runtime Version** should be **Experimental** (.NET 4.6 Equivalent).</span></span> <span data-ttu-id="9a6f6-285">Si vous modifiez cet déclenchera une nécessité de redémarrer l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-285">Changing this will trigger a need to restart the Editor.</span></span>
        2. <span data-ttu-id="9a6f6-286">**Script principal** doit être **.NET**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-286">**Scripting Backend** should be **.NET**</span></span>
        3. <span data-ttu-id="9a6f6-287">**Niveau de compatibilité d’API** doit être **.NET 4.6**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-287">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![Mettre à jour les autres paramètres.](images/AzureLabs-Lab4-16.png)
      
    2. <span data-ttu-id="9a6f6-289">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-289">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="9a6f6-290">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-290">**InternetClient**</span></span>
        - <span data-ttu-id="9a6f6-291">**Webcam**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-291">**Webcam**</span></span>

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab4-17.png)

    3. <span data-ttu-id="9a6f6-293">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-293">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Mettre à jour les paramètres de R X.](images/AzureLabs-Lab4-18.png)

8.  <span data-ttu-id="9a6f6-295">Dans *paramètres de Build*, **Unity C# projets** est n’est plus grisée ; Cochez la case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-295">Back in *Build Settings*, **Unity C# Projects** is no longer greyed out; tick the checkbox next to this.</span></span> 
9.  <span data-ttu-id="9a6f6-296">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-296">Close the Build Settings window.</span></span>
10. <span data-ttu-id="9a6f6-297">Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-297">Save your Scene and Project (**FILE > SAVE SCENE / FILE > SAVE PROJECT**).</span></span>

## <a name="chapter-4---main-camera-setup"></a><span data-ttu-id="9a6f6-298">Chapitre 4 - le programme d’installation de la caméra principale</span><span class="sxs-lookup"><span data-stu-id="9a6f6-298">Chapter 4 - Main Camera setup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a6f6-299">Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à [télécharger cette .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/Azure-MR-304.unitypackage)et l’importer dans votre projet en tant qu’un [personnalisé Package](https://docs.unity3d.com/Manual/AssetPackages.html).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-299">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to [download this .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/Azure-MR-304.unitypackage), and import it into your project as a [Custom Package](https://docs.unity3d.com/Manual/AssetPackages.html).</span></span> <span data-ttu-id="9a6f6-300">N’oubliez pas que ce package inclut également l’importation de la *DLL Newtonsoft*, comme indiqué dans [chapitre 5](#chapter-5--import-the-newtonsoft.json-library).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-300">Be aware that this package also includes the import of the *Newtonsoft DLL*, covered in [Chapter 5](#chapter-5--import-the-newtonsoft.json-library).</span></span> <span data-ttu-id="9a6f6-301">Avec cela importé, vous pouvez continuer à partir de [chapitre 6](#chapter-6-create-the-faceanalysis-class).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-301">With this imported, you can continue from [Chapter 6](#chapter-6-create-the-faceanalysis-class).</span></span>

1.  <span data-ttu-id="9a6f6-302">Dans le *hiérarchie* Panneau de configuration, sélectionnez le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-302">In the *Hierarchy* Panel, select the **Main Camera**.</span></span>

2.  <span data-ttu-id="9a6f6-303">Une fois sélectionné, vous serez en mesure de voir tous les composants de la **Main Camera** dans le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-303">Once selected, you will be able to see all the components of the **Main Camera** in the *Inspector Panel*.</span></span>

    1. <span data-ttu-id="9a6f6-304">Le **objet caméra** doit être nommé **Main Camera** (Notez l’orthographe !)</span><span class="sxs-lookup"><span data-stu-id="9a6f6-304">The **Camera object** must be named **Main Camera** (note the spelling!)</span></span>

    2. <span data-ttu-id="9a6f6-305">La caméra principale **balise** doit être définie sur **MainCamera** (Notez l’orthographe !)</span><span class="sxs-lookup"><span data-stu-id="9a6f6-305">The Main Camera **Tag** must be set to **MainCamera** (note the spelling!)</span></span>

    3. <span data-ttu-id="9a6f6-306">Assurez-vous que le **Position transformer** a la valeur **0, 0, 0**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-306">Make sure the **Transform Position** is set to **0, 0, 0**</span></span>

    4. <span data-ttu-id="9a6f6-307">Définissez **d’effacer les indicateurs** à **couleur unie**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-307">Set **Clear Flags** to **Solid Color**</span></span>

    5. <span data-ttu-id="9a6f6-308">Définir le **arrière-plan** couleur du composant de caméra à **noir, Alpha 0 (Hex Code : #00000000)**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-308">Set the **Background** Color of the Camera Component to **Black, Alpha 0 (Hex Code: #00000000)**</span></span>

        ![configurer les composants de l’appareil photo](images/AzureLabs-Lab4-19.png) 

## <a name="chapter-5--import-the-newtonsoftjson-library"></a><span data-ttu-id="9a6f6-310">Chapitre 5 : importer la bibliothèque de Newtonsoft.Json</span><span class="sxs-lookup"><span data-stu-id="9a6f6-310">Chapter 5 – Import the Newtonsoft.Json library</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a6f6-311">Si vous avez importé le « .unitypackage » dans le [dernier chapitre](#chapter-4--main-camera-setup), vous pouvez ignorer ce chapitre.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-311">If you imported the '.unitypackage' in the [last Chapter](#chapter-4--main-camera-setup), you can skip this Chapter.</span></span>

<span data-ttu-id="9a6f6-312">Pour vous aider à désérialiser et sérialiser des objets reçus et envoyés au Service Bot, vous devez télécharger le *Newtonsoft.Json* bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-312">To help you deserialize and serialize objects received and sent to the Bot Service you need to download the *Newtonsoft.Json* library.</span></span> <span data-ttu-id="9a6f6-313">Vous trouverez une version compatible déjà organisée avec la structure de dossiers Unity correcte dans ce [fichier de package Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/newtonsoftDLL.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-313">You will find a compatible version already organized with the correct Unity folder structure in this [Unity package file](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/newtonsoftDLL.unitypackage).</span></span> 

<span data-ttu-id="9a6f6-314">Pour importer la bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-314">To import the library:</span></span>

1.  <span data-ttu-id="9a6f6-315">Télécharger le Package Unity.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-315">Download the Unity Package.</span></span>
2.  <span data-ttu-id="9a6f6-316">Cliquez sur **actifs**, **importer un Package**, **Package personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-316">Click on **Assets**, **Import Package**, **Custom Package**.</span></span>

    ![Importer la bibliothèque de Newtonsoft.Json](images/AzureLabs-Lab4-20.png)

3.  <span data-ttu-id="9a6f6-318">Recherchez le Package Unity que vous avez téléchargé, puis cliquez sur Ouvrir.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-318">Look for the Unity Package you have downloaded, and click Open.</span></span>
4.  <span data-ttu-id="9a6f6-319">Assurez-vous que tous les composants du package sont cochés et cliquez sur **importation**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-319">Make sure all the components of the package are ticked and click **Import**.</span></span>

    ![Importer la bibliothèque de Newtonsoft.Json](images/AzureLabs-Lab4-21.png)

## <a name="chapter-6---create-the-faceanalysis-class"></a><span data-ttu-id="9a6f6-321">Chapitre 6 : créer la classe FaceAnalysis</span><span class="sxs-lookup"><span data-stu-id="9a6f6-321">Chapter 6 - Create the FaceAnalysis class</span></span>

<span data-ttu-id="9a6f6-322">L’objectif de la classe FaceAnalysis consiste à héberger les méthodes nécessaires pour communiquer avec votre Service de reconnaissance de visage Azure.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-322">The purpose of the FaceAnalysis class is to host the methods necessary to communicate with your Azure Face Recognition Service.</span></span> 

- <span data-ttu-id="9a6f6-323">Après l’envoi d’une image de capture le service, il analyse il et identifier des visages détectés et déterminer si une appartient à une personne connue.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-323">After sending the service a capture image, it will analyse it and identify the faces within, and determine if any belong to a known person.</span></span> 
- <span data-ttu-id="9a6f6-324">Si une personne connue est trouvée, cette classe affiche son nom sous forme de texte de l’interface utilisateur dans la scène.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-324">If a known person is found, this class will display its name as UI text in the scene.</span></span>

<span data-ttu-id="9a6f6-325">Pour créer le *FaceAnalysis* classe :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-325">To create the *FaceAnalysis* class:</span></span>

 1. <span data-ttu-id="9a6f6-326">Avec le bouton droit dans le *dossier Assets* situé dans le panneau de configuration de projet, puis cliquez sur **créer** > **dossier**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-326">Right-click in the *Assets Folder* located in the Project Panel, then click on **Create** > **Folder**.</span></span> <span data-ttu-id="9a6f6-327">Appelez le dossier **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-327">Call the folder **Scripts**.</span></span> 

    ![Créer la classe FaceAnalysis.](images/AzureLabs-Lab4-22.png)

2.  <span data-ttu-id="9a6f6-329">Double-cliquez sur le dossier venez de créer, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-329">Double click on the folder just created, to open it.</span></span> 
3.  <span data-ttu-id="9a6f6-330">Avec le bouton droit dans le dossier, puis cliquez sur **créer**  >   **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-330">Right-click inside the folder, then click on **Create** > **C# Script**.</span></span> <span data-ttu-id="9a6f6-331">Appeler le script *FaceAnalysis*.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-331">Call the script *FaceAnalysis*.</span></span> 
4.  <span data-ttu-id="9a6f6-332">Double-cliquez sur le nouveau *FaceAnalysis* script pour l’ouvrir avec Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-332">Double click on the new *FaceAnalysis* script to open it with Visual Studio 2017.</span></span>
5.  <span data-ttu-id="9a6f6-333">Entrez les espaces de noms suivants ci-dessus le *FaceAnalysis* classe :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-333">Enter the following namespaces above the *FaceAnalysis* class:</span></span>

    ```csharp
        using Newtonsoft.Json;
        using System.Collections;
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

6.  <span data-ttu-id="9a6f6-334">Vous devez maintenant ajouter tous les objets qui sont utilisés pour deserialising.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-334">You now need to add all of the objects which are used for deserialising.</span></span> <span data-ttu-id="9a6f6-335">Ces objets doivent être ajoutés **en dehors de** de la *FaceAnalysis* script (en dessous de l’accolade en bas).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-335">These objects need to be added **outside** of the *FaceAnalysis* script (beneath the bottom curly bracket).</span></span> 

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
7. <span data-ttu-id="9a6f6-336">Le *Start()* et *Update()* méthodes ne sera pas utilisé, donc les supprimer maintenant.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-336">The *Start()* and *Update()* methods will not be used, so delete them now.</span></span> 

8.  <span data-ttu-id="9a6f6-337">À l’intérieur de la *FaceAnalysis* de classe, ajoutez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-337">Inside the *FaceAnalysis* class, add the following variables:</span></span>

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
    > <span data-ttu-id="9a6f6-338">Remplacez le **clé** et **personGroupId** avec votre clé de Service et l’Id du groupe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-338">Replace the **key** and the **personGroupId** with your Service Key and the Id of the group that you created previously.</span></span>

9.  <span data-ttu-id="9a6f6-339">Ajouter le *Awake()* (méthode), lequel initialises la classe, ajout de la *ImageCapture* classe à la caméra principale et appelle la méthode de création d’étiquette :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-339">Add the *Awake()* method, which initialises the class, adding the *ImageCapture* class to the Main Camera and calls the Label creation method:</span></span>

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

10. <span data-ttu-id="9a6f6-340">Ajouter le *CreateLabel()* (méthode), ce qui crée le *étiquette* objet pour afficher le résultat de l’analyse :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-340">Add the *CreateLabel()* method, which creates the *Label* object to display the analysis result:</span></span>

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

11. <span data-ttu-id="9a6f6-341">Ajouter le *DetectFacesFromImage()* et *GetImageAsByteArray()* (méthode).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-341">Add the *DetectFacesFromImage()* and *GetImageAsByteArray()* method.</span></span> <span data-ttu-id="9a6f6-342">La première demande le Service de reconnaissance de visage pour détecter les visages possible dans l’image soumis, alors que ce dernier est nécessaire pour convertir l’image capturée dans un tableau d’octets :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-342">The former will request the Face Recognition Service to detect any possible face in the submitted image, while the latter is necessary to convert the captured image into a bytes array:</span></span>

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

12. <span data-ttu-id="9a6f6-343">Ajouter le *IdentifyFaces()* (méthode), qui demande le *Service de reconnaissance faciale* pour identifier toute face connu précédemment détecté dans l’image soumis.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-343">Add the *IdentifyFaces()* method, which requests the *Face Recognition Service* to identify any known face previously detected in the submitted image.</span></span> <span data-ttu-id="9a6f6-344">La demande renvoie un id de la personne identifiée mais pas le nom :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-344">The request will return an id of the identified person but not the name:</span></span>

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

13. <span data-ttu-id="9a6f6-345">Ajouter le *GetPerson()* (méthode).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-345">Add the *GetPerson()* method.</span></span> <span data-ttu-id="9a6f6-346">En fournissant son id, cette méthode, les demandes pour le *Service de reconnaissance faciale* pour retourner le nom de la personne identifié :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-346">By providing the person id, this method then requests for the *Face Recognition Service* to return the name of the identified person:</span></span>

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

14.  <span data-ttu-id="9a6f6-347">N’oubliez pas de **enregistrer** les modifications avant de revenir à l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-347">Remember to **Save** the changes before going back to the Unity Editor.</span></span>
15.  <span data-ttu-id="9a6f6-348">Dans l’éditeur Unity, faites glisser le script FaceAnalysis à partir du dossier Scripts dans le panneau de configuration de projet à l’objet Main Camera dans le *Panneau de la hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-348">In the Unity Editor, drag the FaceAnalysis script from the Scripts folder in Project panel to the Main Camera object in the *Hierarchy panel*.</span></span> <span data-ttu-id="9a6f6-349">Le nouveau composant de script sera être ainsi ajouté à la caméra principale.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-349">The new script component will be so added to the Main Camera.</span></span> 

![FaceAnalysis place sur la caméra principale](images/AzureLabs-Lab4-23.png)


## <a name="chapter-7---create-the-imagecapture-class"></a><span data-ttu-id="9a6f6-351">Chapitre 7 - créer la classe ImageCapture</span><span class="sxs-lookup"><span data-stu-id="9a6f6-351">Chapter 7 - Create the ImageCapture class</span></span>

<span data-ttu-id="9a6f6-352">L’objectif de la *ImageCapture* classe consiste à héberger les méthodes nécessaires pour communiquer avec votre *Service de reconnaissance de visage Azure* pour analyser l’image que vous allez capturer, identification des visages qu’il contient et déterminer s’il appartient à une personne connue.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-352">The purpose of the *ImageCapture* class is to host the methods necessary to communicate with your *Azure Face Recognition Service* to analyse the image you will capture, identifying faces in it and determining if it belongs to a known person.</span></span> <span data-ttu-id="9a6f6-353">Si une personne connue est trouvée, cette classe affiche son nom sous forme de texte de l’interface utilisateur dans la scène.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-353">If a known person is found, this class will display its name as UI text in the scene.</span></span>

<span data-ttu-id="9a6f6-354">Pour créer le *ImageCapture* classe :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-354">To create the *ImageCapture* class:</span></span>
 
1.  <span data-ttu-id="9a6f6-355">Avec le bouton droit à l’intérieur de la **Scripts** dossier que vous avez créé précédemment, puis cliquez sur **créer**,  **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-355">Right-click inside the **Scripts** folder you have created previously, then click on **Create**, **C# Script**.</span></span> <span data-ttu-id="9a6f6-356">Appeler le script *ImageCapture*.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-356">Call the script *ImageCapture*.</span></span> 
2.  <span data-ttu-id="9a6f6-357">Double-cliquez sur le nouveau *ImageCapture* script pour l’ouvrir avec Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-357">Double click on the new *ImageCapture* script to open it with Visual Studio 2017.</span></span>
3.  <span data-ttu-id="9a6f6-358">Entrez les espaces de noms suivantes au-dessus de la classe ImageCapture :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-358">Enter the following namespaces above the ImageCapture class:</span></span>

    ```csharp
        using System.IO;
        using System.Linq;
        using UnityEngine;
        using UnityEngine.XR.WSA.Input;
        using UnityEngine.XR.WSA.WebCam;
    ```

4.  <span data-ttu-id="9a6f6-359">À l’intérieur de la *ImageCapture* de classe, ajoutez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-359">Inside the *ImageCapture* class, add the following variables:</span></span>

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

5.  <span data-ttu-id="9a6f6-360">Ajouter le *Awake()* et *Start()* méthodes nécessaires pour initialiser la classe et de permettre la HoloLens capturer les mouvements de l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-360">Add the *Awake()* and *Start()* methods necessary to initialise the class and allow the HoloLens to capture the user's gestures:</span></span>

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

6.  <span data-ttu-id="9a6f6-361">Ajouter le *TapHandler()* qui est appelée lorsque l’utilisateur effectue un *appuyez sur* mouvements :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-361">Add the *TapHandler()* which is called when the user performs a *Tap* gesture:</span></span>

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

7.  <span data-ttu-id="9a6f6-362">Ajouter le *ExecuteImageCaptureAndAnalysis()* (méthode), qui commence le processus de capture d’Image :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-362">Add the *ExecuteImageCaptureAndAnalysis()* method, which will begin the process of Image Capturing:</span></span>

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

8.  <span data-ttu-id="9a6f6-363">Ajoutez les gestionnaires sont appelés quand le processus de capture photo est terminé :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-363">Add the handlers that are called when the photo capture process has been completed:</span></span>

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

9. <span data-ttu-id="9a6f6-364">N’oubliez pas de **enregistrer** les modifications avant de revenir à l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-364">Remember to **Save** the changes before going back to the Unity Editor.</span></span>

## <a name="chapter-8---building-the-solution"></a><span data-ttu-id="9a6f6-365">Chapitre 8 - Création d’une solution</span><span class="sxs-lookup"><span data-stu-id="9a6f6-365">Chapter 8 - Building the solution</span></span>

<span data-ttu-id="9a6f6-366">Pour effectuer une analyse minutieuse de votre application vous en aurez besoin pour effectuer un chargement indépendant sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-366">To perform a thorough test of your application you will need to sideload it onto your HoloLens.</span></span>

<span data-ttu-id="9a6f6-367">Avant de procéder, assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-367">Before you do, ensure that:</span></span>

-   <span data-ttu-id="9a6f6-368">Tous les paramètres mentionnés dans le chapitre 3 sont correctement définies.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-368">All the settings mentioned in the Chapter 3 are set correctly.</span></span> 
-   <span data-ttu-id="9a6f6-369">Le script *FaceAnalysis* est attaché à l’objet Main Camera.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-369">The script *FaceAnalysis* is attached to the Main Camera object.</span></span> 
-   <span data-ttu-id="9a6f6-370">Les deux le **Auth Key** et **Id de groupe** ont été définies dans le *FaceAnalysis* script.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-370">Both the **Auth Key** and **Group Id** have been set within the *FaceAnalysis* script.</span></span>

<span data-ttu-id="9a6f6-371">Ce point que vous êtes prêt à générer la Solution.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-371">A this point you are ready to build the Solution.</span></span> <span data-ttu-id="9a6f6-372">Une fois que la Solution a été créée, vous serez prêt à déployer votre application.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-372">Once the Solution has been built, you will be ready to deploy your application.</span></span>

<span data-ttu-id="9a6f6-373">Pour commencer le processus de génération :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-373">To begin the Build process:</span></span>

1.  <span data-ttu-id="9a6f6-374">En cliquant sur fichier, enregistrer, enregistrer la scène actuelle.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-374">Save the current scene by clicking on File, Save.</span></span>
2.  <span data-ttu-id="9a6f6-375">Accédez à fichier, les paramètres de Build, cliquez sur Ajouter un arrière-plan ouverte.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-375">Go to File, Build Settings, click on Add Open Scenes.</span></span>
3.  <span data-ttu-id="9a6f6-376">Veillez à l’autre Unity C# projets.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-376">Make sure to tick Unity C# Projects.</span></span>

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab4-24.png)

4.  <span data-ttu-id="9a6f6-378">Appuyez sur Build.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-378">Press Build.</span></span> <span data-ttu-id="9a6f6-379">Lors de cette façon, Unity lancera une fenêtre d’Explorateur de fichiers, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-379">Upon doing so, Unity will launch a File Explorer window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="9a6f6-380">À présent, de créer ce dossier au sein du projet Unity et l’appeler application.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-380">Create that folder now, within the Unity project, and call it App.</span></span> <span data-ttu-id="9a6f6-381">Le dossier d’application sélectionné, appuyez sur Sélectionner un dossier.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-381">Then with the App folder selected, press Select Folder.</span></span> 
5.  <span data-ttu-id="9a6f6-382">Unity commence la création de votre projet, dans le dossier d’application.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-382">Unity will begin building your project, out to the App folder.</span></span> 
6.  <span data-ttu-id="9a6f6-383">Une fois Unity a terminé la génération (il peut prendre un certain temps), il ouvre une fenêtre d’Explorateur de fichiers à l’emplacement de votre build.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-383">Once Unity has finished building (it might take some time), it will open a File Explorer window at the location of your build.</span></span>

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab4-25.png)

7.  <span data-ttu-id="9a6f6-385">Ouvrez le dossier d’application et ouvrez la nouvelle Solution de projet (comme indiqué ci-dessus, MR_FaceRecognition.sln).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-385">Open your App folder, and then open the new Project Solution (as seen above, MR_FaceRecognition.sln).</span></span>


## <a name="chapter-9---deploying-your-application"></a><span data-ttu-id="9a6f6-386">Chapitre 9 - déploiement de votre application</span><span class="sxs-lookup"><span data-stu-id="9a6f6-386">Chapter 9 - Deploying your application</span></span>

<span data-ttu-id="9a6f6-387">Pour déployer sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-387">To deploy on HoloLens:</span></span>

1.  <span data-ttu-id="9a6f6-388">Vous devez l’adresse IP de votre HoloLens (pour les déployer à distance) et pour vérifier que votre HoloLens est dans **Mode développeur**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-388">You will need the IP Address of your HoloLens (for Remote Deploy), and to ensure your HoloLens is in **Developer Mode**.</span></span> <span data-ttu-id="9a6f6-389">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-389">To do this:</span></span>

    1. <span data-ttu-id="9a6f6-390">Tout en portant vos HoloLens, ouvrez le **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-390">Whilst wearing your HoloLens, open the **Settings**.</span></span>
    2. <span data-ttu-id="9a6f6-391">Accédez à **réseau & Internet > Wi-Fi > Options avancées**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-391">Go to **Network & Internet > Wi-Fi > Advanced Options**</span></span>
    3. <span data-ttu-id="9a6f6-392">Remarque la **IPv4** adresse.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-392">Note the **IPv4** address.</span></span>
    4. <span data-ttu-id="9a6f6-393">Ensuite, accédez à **paramètres**, puis à **mise à jour & sécurité > pour les développeurs**</span><span class="sxs-lookup"><span data-stu-id="9a6f6-393">Next, navigate back to **Settings**, and then to **Update & Security > For Developers**</span></span> 
    5. <span data-ttu-id="9a6f6-394">Définir le Mode développeur.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-394">Set Developer Mode On.</span></span>

2.  <span data-ttu-id="9a6f6-395">Accédez à votre nouvelle build Unity (le *application* dossier) et ouvrez le fichier solution avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-395">Navigate to your new Unity build (the *App* folder) and open the solution file with *Visual Studio*.</span></span>
3.  <span data-ttu-id="9a6f6-396">Dans, sélectionnez la Configuration de Solution **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-396">In the Solution Configuration select **Debug**.</span></span>
4.  <span data-ttu-id="9a6f6-397">Dans la plateforme de Solution, sélectionnez **x86**, **Machine distante**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-397">In the Solution Platform, select **x86**, **Remote Machine**.</span></span> 

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab4-26.png)
 
5.  <span data-ttu-id="9a6f6-399">Accédez à la **menu Générer** , puis cliquez sur **déployer la Solution**, chargement de version test l’application à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-399">Go to the **Build menu** and click on **Deploy Solution**, to sideload the application to your HoloLens.</span></span>
6.  <span data-ttu-id="9a6f6-400">Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prêt à être lancé !</span><span class="sxs-lookup"><span data-stu-id="9a6f6-400">Your App should now appear in the list of installed apps on your HoloLens, ready to be launched!</span></span>

> [!NOTE]
> <span data-ttu-id="9a6f6-401">Pour déployer sur casque immersif, définissez le **plateforme de Solution** à *ordinateur Local*et définissez le **Configuration** à *déboguer*, avec *x86* en tant que le **plateforme**.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-401">To deploy to immersive headset, set the **Solution Platform** to *Local Machine*, and set the **Configuration** to *Debug*, with *x86* as the **Platform**.</span></span> <span data-ttu-id="9a6f6-402">Déployer sur l’ordinateur local d’ordinateur, à l’aide de la **menu Générer**, en sélectionnant *déployer la Solution*.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-402">Then deploy to the local machine, using the **Build menu**, selecting *Deploy Solution*.</span></span> 


## <a name="chapter-10---using-the-application"></a><span data-ttu-id="9a6f6-403">Chapitre 10 - à l’aide de l’application</span><span class="sxs-lookup"><span data-stu-id="9a6f6-403">Chapter 10 - Using the application</span></span>

1.  <span data-ttu-id="9a6f6-404">Porter le HoloLens, lancez l’application.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-404">Wearing the HoloLens, launch the app.</span></span>
2.  <span data-ttu-id="9a6f6-405">Examinez la personne que vous avez enregistrée avec le *API visage*.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-405">Look at the person that you have registered with the *Face API*.</span></span> <span data-ttu-id="9a6f6-406">Vérifiez que :</span><span class="sxs-lookup"><span data-stu-id="9a6f6-406">Make sure that:</span></span>

    -  <span data-ttu-id="9a6f6-407">Visage de la personne n’est pas trop éloignées et clairement visibles</span><span class="sxs-lookup"><span data-stu-id="9a6f6-407">The person's face is not too distant and clearly visible</span></span>
    -  <span data-ttu-id="9a6f6-408">L’éclairage d’environnement n’est pas trop sombre</span><span class="sxs-lookup"><span data-stu-id="9a6f6-408">The environment lighting is not too dark</span></span>

3.  <span data-ttu-id="9a6f6-409">Utilisez l’action d’appuyer pour capturer l’image de la personne.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-409">Use the tap gesture to capture the person's picture.</span></span>
4.  <span data-ttu-id="9a6f6-410">Attendez que l’application envoyer la demande d’analyse et de recevoir une réponse.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-410">Wait for the App to send the analysis request and receive a response.</span></span>
5.  <span data-ttu-id="9a6f6-411">Si la personne qui a été reconnue, le nom de personne s’affiche sous forme de texte de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-411">If the person has been successfully recognized, the person's name will appear as UI text.</span></span>
6.  <span data-ttu-id="9a6f6-412">Vous pouvez répéter le processus de capture à l’aide de l’action d’appuyer après quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-412">You can repeat the capture process using the tap gesture every few seconds.</span></span>

## <a name="your-finished-azure-face-api-application"></a><span data-ttu-id="9a6f6-413">Votre Application d’API de visage Azure terminée</span><span class="sxs-lookup"><span data-stu-id="9a6f6-413">Your finished Azure Face API Application</span></span>

<span data-ttu-id="9a6f6-414">Félicitations, vous avez créé une application de réalité mixte qui tire parti du service de reconnaissance faciale de Azure pour détecter les visages dans une image et identifier des visages connus.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-414">Congratulations, you built a mixed reality app that leverages the Azure Face Recognition service to detect faces within an image, and identify any known faces.</span></span>

![résultat de cette formation](images/AzureLabs-Lab4-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="9a6f6-416">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="9a6f6-416">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="9a6f6-417">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="9a6f6-417">Exercise 1</span></span>

<span data-ttu-id="9a6f6-418">Le **API visage de Azure** est suffisamment puissant pour détecter jusqu'à 64 visages dans une seule image.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-418">The **Azure Face API** is powerful enough to detect up to 64 faces in a single image.</span></span> <span data-ttu-id="9a6f6-419">Étendre l’application, afin qu’il peut reconnaître les visages de deux ou trois parmi de nombreuses autres personnes.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-419">Extend the application, so that it could recognize two or three faces, amongst many other people.</span></span>

### <a name="exercise-2"></a><span data-ttu-id="9a6f6-420">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="9a6f6-420">Exercise 2</span></span>

<span data-ttu-id="9a6f6-421">Le **API visage de Azure** est également en mesure de fournir de nouveau toutes sortes d’informations sur les attributs.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-421">The **Azure Face API** is also able to provide back all kinds of attribute information.</span></span> <span data-ttu-id="9a6f6-422">Intégrer cela dans l’application.</span><span class="sxs-lookup"><span data-stu-id="9a6f6-422">Integrate this into the application.</span></span> <span data-ttu-id="9a6f6-423">Cela pourrait être encore plus intéressant, lorsqu’elles sont combinées avec le [API émotion](https://azure.microsoft.com/en-au/services/cognitive-services/emotion/).</span><span class="sxs-lookup"><span data-stu-id="9a6f6-423">This could be even more interesting, when combined with the [Emotion API](https://azure.microsoft.com/en-au/services/cognitive-services/emotion/).</span></span>
