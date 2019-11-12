---
title: MR et Azure 303-compréhension du langage naturel (LUIS)
description: Suivez ce cours pour apprendre à implémenter Azure Language Understanding Intelligence Service (LUIS) dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Académie, Unity, didacticiel, API, Language Understanding Intelligence Service, Luis, hololens, immersif, VR
ms.openlocfilehash: 9b3e4f081dc8a054d783246554f904a38f43f26c
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926804"
---
>[!NOTE]
><span data-ttu-id="d4f12-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="d4f12-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="d4f12-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="d4f12-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="d4f12-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="d4f12-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="d4f12-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d4f12-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="d4f12-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="d4f12-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="d4f12-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="d4f12-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-and-azure-303-natural-language-understanding-luis"></a><span data-ttu-id="d4f12-110">MR et Azure 303 : compréhension du langage naturel (LUIS)</span><span class="sxs-lookup"><span data-stu-id="d4f12-110">MR and Azure 303: Natural language understanding (LUIS)</span></span>

<span data-ttu-id="d4f12-111">Dans ce cours, vous allez apprendre à intégrer Language Understanding dans une application de réalité mixte à l’aide d’Azure Cognitive Services, avec le API Language Understanding.</span><span class="sxs-lookup"><span data-stu-id="d4f12-111">In this course, you will learn how to integrate Language Understanding into a mixed reality application using Azure Cognitive Services, with the Language Understanding API.</span></span>

![résultat de l’atelier](images/AzureLabs-Lab3-000.png)

<span data-ttu-id="d4f12-113">*Language Understanding (Luis)* est un service Microsoft Azure, qui permet aux applications de tirer parti de l’entrée utilisateur, par exemple en extrayant ce qu’une personne peut souhaiter, dans ses propres mots.</span><span class="sxs-lookup"><span data-stu-id="d4f12-113">*Language Understanding (LUIS)* is a Microsoft Azure service, which provides applications with the ability to make meaning out of user input, such as through extracting what a person might want, in their own words.</span></span> <span data-ttu-id="d4f12-114">Cela est possible via Machine Learning, qui comprend et apprend les informations d’entrée, puis peut répondre avec des informations détaillées et pertinentes.</span><span class="sxs-lookup"><span data-stu-id="d4f12-114">This is achieved through machine learning, which understands and learns the input information, and then can reply with detailed, relevant, information.</span></span> <span data-ttu-id="d4f12-115">Pour plus d’informations, visitez la [page Azure Language Understanding (Luis)](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/).</span><span class="sxs-lookup"><span data-stu-id="d4f12-115">For more information, visit the [Azure Language Understanding (LUIS) page](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/).</span></span>

<span data-ttu-id="d4f12-116">Une fois ce cours terminé, vous disposerez d’une application de casque immersif en réalité mixte, qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4f12-116">Having completed this course, you will have a mixed reality immersive headset application which will be able to do the following:</span></span>

1.  <span data-ttu-id="d4f12-117">Capturez la parole d’entrée d’utilisateur à l’aide du microphone attaché au casque immersif.</span><span class="sxs-lookup"><span data-stu-id="d4f12-117">Capture user input speech, using the Microphone attached to the immersive headset.</span></span> 
2.  <span data-ttu-id="d4f12-118">Envoyez la dictée capturée au *Language Understanding intelligent service Azure* (*Luis*).</span><span class="sxs-lookup"><span data-stu-id="d4f12-118">Send the captured dictation the *Azure Language Understanding Intelligent Service* (*LUIS*).</span></span> 
3.  <span data-ttu-id="d4f12-119">Utilisez LUIS Extract la signification des informations d’envoi, qui sera analysée et tentera de déterminer l’objectif de la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d4f12-119">Have LUIS extract meaning from the send information, which will be analyzed, and attempt to determine the intent of the user’s request will be made.</span></span>

<span data-ttu-id="d4f12-120">Le développement inclut la création d’une application dans laquelle l’utilisateur peut utiliser la voix et/ou le point de regard pour modifier la taille et la couleur des objets dans la scène.</span><span class="sxs-lookup"><span data-stu-id="d4f12-120">Development will include the creation of an app where the user will be able to use voice and/or gaze to change the size and the color of the objects in the scene.</span></span> <span data-ttu-id="d4f12-121">L’utilisation de contrôleurs de mouvement n’est pas couverte.</span><span class="sxs-lookup"><span data-stu-id="d4f12-121">The use of motion controllers will not be covered.</span></span>

<span data-ttu-id="d4f12-122">Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception.</span><span class="sxs-lookup"><span data-stu-id="d4f12-122">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="d4f12-123">Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="d4f12-123">This course is designed to teach you how to integrate an Azure Service with your Unity Project.</span></span> <span data-ttu-id="d4f12-124">C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="d4f12-124">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

<span data-ttu-id="d4f12-125">Préparez-vous à former LUIS plusieurs fois, ce qui est abordé dans le [chapitre 12](#chapter-12--improving-your-luis-service).</span><span class="sxs-lookup"><span data-stu-id="d4f12-125">Be prepared to Train LUIS several times, which is covered in [Chapter 12](#chapter-12--improving-your-luis-service).</span></span> <span data-ttu-id="d4f12-126">Vous obtiendrez de meilleurs résultats le plus souvent, LUIS a été formé.</span><span class="sxs-lookup"><span data-stu-id="d4f12-126">You will get better results the more times LUIS has been trained.</span></span>

## <a name="device-support"></a><span data-ttu-id="d4f12-127">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="d4f12-127">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="d4f12-128">Course</span><span class="sxs-lookup"><span data-stu-id="d4f12-128">Course</span></span></th><th style="width:150px"> <span data-ttu-id="d4f12-129"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="d4f12-129"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="d4f12-130"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="d4f12-130"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="d4f12-131">MR et Azure 303 : compréhension du langage naturel (LUIS)</span><span class="sxs-lookup"><span data-stu-id="d4f12-131">MR and Azure 303: Natural language understanding (LUIS)</span></span></td><td style="text-align: center;"> <span data-ttu-id="d4f12-132">✔️</span><span class="sxs-lookup"><span data-stu-id="d4f12-132">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="d4f12-133">✔️</span><span class="sxs-lookup"><span data-stu-id="d4f12-133">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="d4f12-134">Bien que ce cours se concentre principalement sur les casques de Windows Mixed Reality (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours à Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d4f12-134">While this course primarily focuses on Windows Mixed Reality immersive (VR) headsets, you can also apply what you learn in this course to Microsoft HoloLens.</span></span> <span data-ttu-id="d4f12-135">À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d4f12-135">As you follow along with the course, you will see notes on any changes you might need to employ to support HoloLens.</span></span> <span data-ttu-id="d4f12-136">Lorsque vous utilisez HoloLens, vous remarquerez peut-être un écho pendant la capture vocale.</span><span class="sxs-lookup"><span data-stu-id="d4f12-136">When using HoloLens, you may notice some echo during voice capture.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4f12-137">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="d4f12-137">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="d4f12-138">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="d4f12-138">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="d4f12-139">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="d4f12-139">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="d4f12-140">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d4f12-140">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="d4f12-141">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours :</span><span class="sxs-lookup"><span data-stu-id="d4f12-141">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="d4f12-142">Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)</span><span class="sxs-lookup"><span data-stu-id="d4f12-142">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="d4f12-143">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="d4f12-143">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md)
- [<span data-ttu-id="d4f12-144">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="d4f12-144">The latest Windows 10 SDK</span></span>](install-the-tools.md)
- [<span data-ttu-id="d4f12-145">Unity 2017,4</span><span class="sxs-lookup"><span data-stu-id="d4f12-145">Unity 2017.4</span></span>](install-the-tools.md)
- [<span data-ttu-id="d4f12-146">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d4f12-146">Visual Studio 2017</span></span>](install-the-tools.md)
- <span data-ttu-id="d4f12-147">Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="d4f12-147">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="d4f12-148">Un jeu de casque avec un microphone intégré (si le casque n’a pas de MIC et de haut-parleurs intégrés)</span><span class="sxs-lookup"><span data-stu-id="d4f12-148">A set of headphones with a built-in microphone (if the headset doesn't have a built-in mic and speakers)</span></span>
- <span data-ttu-id="d4f12-149">Accès Internet pour l’installation d’Azure et la récupération LUIS</span><span class="sxs-lookup"><span data-stu-id="d4f12-149">Internet access for Azure setup and LUIS retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d4f12-150">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d4f12-150">Before you start</span></span>

1.  <span data-ttu-id="d4f12-151">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="d4f12-151">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span> 
2.  <span data-ttu-id="d4f12-152">Pour permettre à votre ordinateur d’activer la dictée, accédez à **Paramètres Windows > confidentialité > reconnaissance vocale, écriture manuscrite & typage** , puis appuyez sur le bouton **activer les services vocaux et les suggestions de saisie**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-152">To allow your machine to enable Dictation, go to **Windows Settings > Privacy > Speech, Inking & Typing** and press on the button **Turn On speech services and typing suggestions**.</span></span>
3.  <span data-ttu-id="d4f12-153">Le code de ce didacticiel vous permet d’enregistrer à partir de l’ensemble du **périphérique microphone par défaut** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d4f12-153">The code in this tutorial will allow you to record from the **Default Microphone Device** set on your machine.</span></span> <span data-ttu-id="d4f12-154">Assurez-vous que le périphérique microphone par défaut est défini comme celui que vous souhaitez utiliser pour capturer votre voix.</span><span class="sxs-lookup"><span data-stu-id="d4f12-154">Make sure the Default Microphone Device is set as the one you wish to use to capture your voice.</span></span>
4.  <span data-ttu-id="d4f12-155">Si votre casque dispose d’un microphone intégré, assurez-vous que l’option *« lors de l’usure du casque, basculez vers casque MIC »* est activée dans les paramètres du portail de la *réalité mixte* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-155">If your headset has a built-in microphone, make sure the option *“When I wear my headset, switch to headset mic”* is turned on in the *Mixed Reality Portal* settings.</span></span>

    ![Configuration du casque immersif](images/AzureLabs-Lab3-00.png)

## <a name="chapter-1--setup-azure-portal"></a><span data-ttu-id="d4f12-157">Chapitre 1-configurer le portail Azure</span><span class="sxs-lookup"><span data-stu-id="d4f12-157">Chapter 1 – Setup Azure Portal</span></span>

<span data-ttu-id="d4f12-158">Pour utiliser le service de *Language Understanding* dans Azure, vous devez configurer une instance du service qui sera mise à la disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="d4f12-158">To use the *Language Understanding* service in Azure, you will need to configure an instance of the service to be made available to your application.</span></span>

1.  <span data-ttu-id="d4f12-159">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d4f12-159">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE]
    > <span data-ttu-id="d4f12-160">Si vous n’avez pas encore de compte Azure, vous devez en créer un.</span><span class="sxs-lookup"><span data-stu-id="d4f12-160">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="d4f12-161">Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="d4f12-161">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="d4f12-162">Une fois que vous êtes connecté, cliquez sur **nouveau** dans l’angle supérieur gauche, recherchez *Language Understanding*, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-162">Once you are logged in, click on **New** in the top left corner, and search for *Language Understanding*, and click **Enter**.</span></span> 

    ![Créer une ressource LUIS](images/AzureLabs-Lab3-01.png)

    > [!NOTE]
    > <span data-ttu-id="d4f12-164">Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.</span><span class="sxs-lookup"><span data-stu-id="d4f12-164">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>
 
3.  <span data-ttu-id="d4f12-165">La nouvelle page qui s’affiche à droite fournit une description du service Language Understanding.</span><span class="sxs-lookup"><span data-stu-id="d4f12-165">The new page to the right will provide a description of the Language Understanding service.</span></span> <span data-ttu-id="d4f12-166">En bas à gauche de cette page, cliquez sur le bouton **créer** pour créer une instance de ce service.</span><span class="sxs-lookup"><span data-stu-id="d4f12-166">At the bottom left of this page, select the **Create** button, to create an instance of this service.</span></span>

    ![Création du service LUIS-Notice légale](images/AzureLabs-Lab3-02.png)
 
4.  <span data-ttu-id="d4f12-168">Une fois que vous avez cliqué sur créer :</span><span class="sxs-lookup"><span data-stu-id="d4f12-168">Once you have clicked on Create:</span></span>

    1. <span data-ttu-id="d4f12-169">Insérez le **nom** de votre choix pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="d4f12-169">Insert your desired **Name** for this service instance.</span></span>
    2. <span data-ttu-id="d4f12-170">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-170">Select a **Subscription**.</span></span>
    3. <span data-ttu-id="d4f12-171">Sélectionnez le **niveau tarifaire** approprié, s’il s’agit de la première fois que vous créez un *service Luis*, vous devez disposer d’un niveau gratuit (nommé F0).</span><span class="sxs-lookup"><span data-stu-id="d4f12-171">Select the **Pricing Tier** appropriate for you, if this is the first time creating a *LUIS Service*, a free tier (named F0) should be available to you.</span></span> <span data-ttu-id="d4f12-172">L’allocation gratuite doit être plus que suffisante pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="d4f12-172">The free allocation should be more than sufficient for this course.</span></span>
    4. <span data-ttu-id="d4f12-173">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="d4f12-173">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="d4f12-174">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d4f12-174">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="d4f12-175">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.</span><span class="sxs-lookup"><span data-stu-id="d4f12-175">It is recommended to keep all the Azure services associated with a single project (e.g. such as these courses) under a common resource group).</span></span> 

        > <span data-ttu-id="d4f12-176">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="d4f12-176">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5. <span data-ttu-id="d4f12-177">Déterminez l' **emplacement** de votre groupe de ressources (si vous créez un groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="d4f12-177">Determine the **Location** for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="d4f12-178">L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait.</span><span class="sxs-lookup"><span data-stu-id="d4f12-178">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="d4f12-179">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="d4f12-179">Some Azure assets are only available in certain regions.</span></span>
    6. <span data-ttu-id="d4f12-180">Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.</span><span class="sxs-lookup"><span data-stu-id="d4f12-180">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>
    7. <span data-ttu-id="d4f12-181">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-181">Select **Create**.</span></span>

        ![Créer un service LUIS-entrée utilisateur](images/AzureLabs-Lab3-03.png)
 
5.  <span data-ttu-id="d4f12-183">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="d4f12-183">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>
6.  <span data-ttu-id="d4f12-184">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="d4f12-184">A notification will appear in the portal once the Service instance is created.</span></span> 
 
    ![Nouvelle image de notification Azure](images/AzureLabs-Lab3-04.png)

7.  <span data-ttu-id="d4f12-186">Cliquez sur la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="d4f12-186">Click on the notification to explore your new Service instance.</span></span>

    ![Notification de création de ressource réussie](images/AzureLabs-Lab3-05.png)
 
8.  <span data-ttu-id="d4f12-188">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="d4f12-188">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="d4f12-189">Vous êtes dirigé vers votre nouvelle instance de service LUIS.</span><span class="sxs-lookup"><span data-stu-id="d4f12-189">You will be taken to your new LUIS service instance.</span></span> 
 
    ![Accès aux clés LUIS](images/AzureLabs-Lab3-06.png)

9.  <span data-ttu-id="d4f12-191">Dans ce didacticiel, votre application doit effectuer des appels à votre service, à l’aide de la clé d’abonnement de votre service.</span><span class="sxs-lookup"><span data-stu-id="d4f12-191">Within this tutorial, your application will need to make calls to your service, which is done through using your service’s Subscription Key.</span></span>
10. <span data-ttu-id="d4f12-192">À partir de la page *démarrage rapide* , de votre service *API Luis* , accédez à la première étape, *saisissez vos clés*, puis cliquez sur **clés** (vous pouvez également y parvenir en cliquant sur les touches de lien bleu, situées dans le menu de navigation services, indiqué par l’icône de clé).</span><span class="sxs-lookup"><span data-stu-id="d4f12-192">From the *Quick start* page, of your *LUIS API* service, navigate to the first step, *Grab your keys*, and click **Keys** (you can also achieve this by clicking the blue hyperlink Keys, located in the services navigation menu, denoted by the key icon).</span></span> <span data-ttu-id="d4f12-193">Cela permet de révéler vos *clés*de service.</span><span class="sxs-lookup"><span data-stu-id="d4f12-193">This will reveal your service *Keys*.</span></span>
11. <span data-ttu-id="d4f12-194">Prenez une copie de l’une des clés affichées, car vous en aurez besoin plus tard dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="d4f12-194">Take a copy of one of the displayed keys, as you will need this later in your project.</span></span> 
12. <span data-ttu-id="d4f12-195">Dans la page *service* , cliquez sur *Language Understanding portail* pour être redirigé vers la page Web que vous utiliserez pour créer votre nouveau service, au sein de l’application Luis.</span><span class="sxs-lookup"><span data-stu-id="d4f12-195">In the *Service* page, click on *Language Understanding Portal* to be redirected to the webpage which you will use to create your new Service, within the LUIS App.</span></span> 

## <a name="chapter-2--the-language-understanding-portal"></a><span data-ttu-id="d4f12-196">Chapitre 2 – portail Language Understanding</span><span class="sxs-lookup"><span data-stu-id="d4f12-196">Chapter 2 – The Language Understanding Portal</span></span>

<span data-ttu-id="d4f12-197">Dans cette section, vous allez apprendre à créer une application LUIS sur le portail LUIS.</span><span class="sxs-lookup"><span data-stu-id="d4f12-197">In this section you will learn how to make a LUIS App on the LUIS Portal.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d4f12-198">N’oubliez pas que la configuration des *entités*, des *intentions*et des *énoncés* dans ce chapitre n’est que la première étape de la création de votre service Luis : vous devrez également reformer le service, plusieurs fois, afin de le rendre plus précis.</span><span class="sxs-lookup"><span data-stu-id="d4f12-198">Please be aware, that setting up the *Entities*, *Intents*, and *Utterances* within this chapter is only the first step in building your LUIS service: you will also need to retrain the service, several times, so to make it more accurate.</span></span> <span data-ttu-id="d4f12-199">La reformation de votre service est traitée dans le [dernier chapitre](#chapter-12--improving-your-luis-service) de ce cours. Assurez-vous donc de l’effectuer.</span><span class="sxs-lookup"><span data-stu-id="d4f12-199">Retraining your service is covered in the [last Chapter](#chapter-12--improving-your-luis-service) of this course, so ensure that you complete it.</span></span>

1.  <span data-ttu-id="d4f12-200">Quand vous atteignez le *portail Language Understanding*, vous devrez peut-être vous connecter, si ce n’est déjà fait, avec les mêmes informations d’identification que votre portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d4f12-200">Upon reaching the *Language Understanding Portal*, you may need to login, if you are not already, with the same credentials as your Azure portal.</span></span> 

    ![Page de connexion LUIS](images/AzureLabs-Lab3-07.png)
 
2.  <span data-ttu-id="d4f12-202">Si vous utilisez LUIS pour la première fois, vous devez faire défiler vers le bas de la page d’accueil, pour rechercher et cliquer sur le bouton **créer une application Luis** .</span><span class="sxs-lookup"><span data-stu-id="d4f12-202">If this is your first time using LUIS, you will need to scroll down to the bottom of the welcome page, to find and click on the **Create LUIS app** button.</span></span>

    ![Page créer une application LUIS](images/AzureLabs-Lab3-08.png)
 
3.  <span data-ttu-id="d4f12-204">Une fois connecté, cliquez sur **mes applications** (si vous n’êtes pas actuellement dans cette section).</span><span class="sxs-lookup"><span data-stu-id="d4f12-204">Once logged in, click **My apps** (if you are not in that section currently).</span></span> <span data-ttu-id="d4f12-205">Vous pouvez ensuite cliquer sur **créer une nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-205">You can then click on **Create new app**.</span></span>

    ![LUIS-image de mon application](images/AzureLabs-Lab3-09.png)
 
4.  <span data-ttu-id="d4f12-207">Donnez un *nom*à votre application.</span><span class="sxs-lookup"><span data-stu-id="d4f12-207">Give your app a *Name*.</span></span>
5.  <span data-ttu-id="d4f12-208">Si votre application est censée comprendre une langue différente de l’anglais, vous devez modifier la *culture* en fonction de la langue appropriée.</span><span class="sxs-lookup"><span data-stu-id="d4f12-208">If your app is supposed to understand a language different from English, you should change the *Culture* to the appropriate language.</span></span>
6.  <span data-ttu-id="d4f12-209">Ici, vous pouvez également ajouter une *Description* de votre nouvelle application Luis.</span><span class="sxs-lookup"><span data-stu-id="d4f12-209">Here you can also add a *Description* of your new LUIS app.</span></span>

    ![LUIS-créer une application](images/AzureLabs-Lab3-10.png)

7.  <span data-ttu-id="d4f12-211">Une fois que vous avez **terminé**, vous accédez à la page de *génération* de votre nouvelle application *Luis* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-211">Once you press **Done**, you will enter the *Build* page of your new *LUIS* application.</span></span>
8.  <span data-ttu-id="d4f12-212">Voici quelques concepts importants à comprendre :</span><span class="sxs-lookup"><span data-stu-id="d4f12-212">There are a few important concepts to understand here:</span></span>

    -   <span data-ttu-id="d4f12-213">*Intentionnelle*, représente la méthode qui sera appelée à la suite d’une requête de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d4f12-213">*Intent*, represents the method that will be called following a query from the user.</span></span> <span data-ttu-id="d4f12-214">Une *intention* peut avoir une ou plusieurs *entités*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-214">An *INTENT* may have one or more *ENTITIES*.</span></span>
    -   <span data-ttu-id="d4f12-215">*Entité*, est un composant de la requête qui décrit les informations relatives à l' *intention*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-215">*Entity*, is a component of the query that describes information relevant to the *INTENT*.</span></span>
    -   <span data-ttu-id="d4f12-216">Les *énoncés*, sont des exemples de requêtes fournies par le développeur, que Luis utilise pour se former lui-même.</span><span class="sxs-lookup"><span data-stu-id="d4f12-216">*Utterances*, are examples of queries provided by the developer, that LUIS will use to train itself.</span></span>

<span data-ttu-id="d4f12-217">Si ces concepts ne sont pas parfaitement clairs, ne vous inquiétez pas, car ce cours les clarifie plus en détail dans ce chapitre.</span><span class="sxs-lookup"><span data-stu-id="d4f12-217">If these concepts are not perfectly clear, do not worry, as this course will clarify them further in this chapter.</span></span>

<span data-ttu-id="d4f12-218">Vous commencerez par créer les *entités* nécessaires à la création de ce cours.</span><span class="sxs-lookup"><span data-stu-id="d4f12-218">You will begin by creating the *Entities* needed to build this course.</span></span>

9.  <span data-ttu-id="d4f12-219">Sur le côté gauche de la page, cliquez sur *entités*, puis sur **créer une entité**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-219">On the left side of the page, click on *Entities*, then click on **Create new entity**.</span></span>

    ![Créer une entité](images/AzureLabs-Lab3-11.png)

10. <span data-ttu-id="d4f12-221">Appelez la nouvelle *couleur*d’entité, définissez son type sur *simple*, puis appuyez sur **terminé**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-221">Call the new Entity *color*, set its type to *Simple*, then press **Done**.</span></span>

    ![Créer une entité simple-couleur](images/AzureLabs-Lab3-12.png)
 
11. <span data-ttu-id="d4f12-223">Répétez ce processus pour créer trois (3) autres entités simples nommées :</span><span class="sxs-lookup"><span data-stu-id="d4f12-223">Repeat this process to create three (3) more Simple Entities named:</span></span>

    -   <span data-ttu-id="d4f12-224">*augmenter*</span><span class="sxs-lookup"><span data-stu-id="d4f12-224">*upsize*</span></span>
    -   <span data-ttu-id="d4f12-225">*réduire*</span><span class="sxs-lookup"><span data-stu-id="d4f12-225">*downsize*</span></span>
    -   <span data-ttu-id="d4f12-226">*Indicatif*</span><span class="sxs-lookup"><span data-stu-id="d4f12-226">*target*</span></span>

<span data-ttu-id="d4f12-227">Le résultat doit ressembler à l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d4f12-227">The result should look like the image below:</span></span>

![Résultat de la création de l’entité](images/AzureLabs-Lab3-13.png)
 
<span data-ttu-id="d4f12-229">À ce stade, vous pouvez commencer à créer des *intentions*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-229">At this point you can begin creating *Intents*.</span></span> 

> [!WARNING]
> <span data-ttu-id="d4f12-230">Ne supprimez pas l’intention **None** .</span><span class="sxs-lookup"><span data-stu-id="d4f12-230">Do not delete the **None** intent.</span></span>

12. <span data-ttu-id="d4f12-231">Sur le côté gauche de la page, cliquez sur **intentions**, puis sur **créer un nouvel objectif**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-231">On the left side of the page, click on **Intents**, then click on **Create new intent**.</span></span>

    ![Créer des intentions](images/AzureLabs-Lab3-14.png)

13. <span data-ttu-id="d4f12-233">Appelez le nouveau **ChangeObjectColor**d’intention.</span><span class="sxs-lookup"><span data-stu-id="d4f12-233">Call the new *Intent* **ChangeObjectColor**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d4f12-234">Ce nom d' *intention* est utilisé dans le code plus loin dans ce cours. pour obtenir de meilleurs résultats, utilisez ce nom exactement comme indiqué.</span><span class="sxs-lookup"><span data-stu-id="d4f12-234">This *Intent* name is used within the code later in this course, so for best results, use this name exactly as provided.</span></span>

<span data-ttu-id="d4f12-235">Une fois que vous avez confirmé le nom, vous êtes dirigé vers la page intentions.</span><span class="sxs-lookup"><span data-stu-id="d4f12-235">Once you confirm the name you will be directed to the Intents Page.</span></span>

![Page LUIS-intentions](images/AzureLabs-Lab3-15.png)

<span data-ttu-id="d4f12-237">Vous remarquerez qu’une zone de texte vous demande de taper 5 ou plusieurs *énoncés*différents.</span><span class="sxs-lookup"><span data-stu-id="d4f12-237">You will notice that there is a textbox asking you to type 5 or more different *Utterances*.</span></span>

> [!NOTE]
> <span data-ttu-id="d4f12-238">LUIS convertit tous les énoncés en minuscules.</span><span class="sxs-lookup"><span data-stu-id="d4f12-238">LUIS converts all Utterances to lower case.</span></span>

14. <span data-ttu-id="d4f12-239">Insérez l' *énoncé* suivant dans la zone de texte supérieure (actuellement avec le type de texte *environ 5 exemples...*</span><span class="sxs-lookup"><span data-stu-id="d4f12-239">Insert the following *Utterance* in the top textbox (currently with the text *Type about 5 examples…*</span></span> <span data-ttu-id="d4f12-240">) et appuyez sur **entrée**:</span><span class="sxs-lookup"><span data-stu-id="d4f12-240">), and press **Enter**:</span></span>

```
The color of the cylinder must be red
```

<span data-ttu-id="d4f12-241">Vous remarquerez que le nouvel *énoncé* s’affiche dans une liste sous.</span><span class="sxs-lookup"><span data-stu-id="d4f12-241">You will notice that the new *Utterance* will appear in a list underneath.</span></span>

<span data-ttu-id="d4f12-242">En suivant le même processus, insérez les six (6) énoncés suivants :</span><span class="sxs-lookup"><span data-stu-id="d4f12-242">Following the same process, insert the following six (6) Utterances:</span></span>

```
make the cube black

make the cylinder color white

change the sphere to red

change it to green

make this yellow

change the color of this object to blue
```

<span data-ttu-id="d4f12-243">Pour chaque énoncé que vous avez créé, vous devez identifier les mots qui doivent être utilisés par LUIS comme entités.</span><span class="sxs-lookup"><span data-stu-id="d4f12-243">For each Utterance you have created, you must identify which words should be used by LUIS as Entities.</span></span> <span data-ttu-id="d4f12-244">Dans cet exemple, vous devez étiqueter toutes les couleurs en tant qu’entité de *couleur* et toutes les références possibles à une cible en tant qu’entité *cible* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-244">In this example you need to label all the colors as a *color* Entity, and all the possible reference to a target as a *target* Entity.</span></span>

15. <span data-ttu-id="d4f12-245">Pour ce faire, essayez de cliquer sur le mot *Cylinder* dans le premier énoncé et sélectionnez *target (cible*).</span><span class="sxs-lookup"><span data-stu-id="d4f12-245">To do so, try clicking on the word *cylinder* in the first Utterance and select *target*.</span></span>

    ![Identifier les cibles d’énoncé](images/AzureLabs-Lab3-16.png)
 
16. <span data-ttu-id="d4f12-247">Cliquez maintenant sur le mot *Red* dans le premier énoncé et sélectionnez *couleur*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-247">Now click on the word *red* in the first Utterance and select *color*.</span></span>

    ![Identifier les entités énoncées](images/AzureLabs-Lab3-17.png)
 
17. <span data-ttu-id="d4f12-249">Étiquetez également la ligne suivante, où *cube* doit être une *cible*et *noir* doit être une *couleur*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-249">Label the next line also, where *cube* should be a *target*, and *black* should be a *color*.</span></span> <span data-ttu-id="d4f12-250">Notez également l’utilisation des mots *« This »* , *« IT »* et *« This Object »* , que nous fournissons, afin que les types de cibles non spécifiques soient également disponibles.</span><span class="sxs-lookup"><span data-stu-id="d4f12-250">Notice also the use of the words *‘this’*, *‘it’*, and *‘this object’*, which we are providing, so to have non-specific target types available also.</span></span> 

18. <span data-ttu-id="d4f12-251">Répétez le processus ci-dessus jusqu’à ce que tous les énoncés aient les entités étiquetées.</span><span class="sxs-lookup"><span data-stu-id="d4f12-251">Repeat the process above until all the Utterances have the Entities labelled.</span></span> <span data-ttu-id="d4f12-252">Si vous avez besoin d’aide, consultez l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d4f12-252">See the below image if you need help.</span></span>

    > [!TIP]
    > <span data-ttu-id="d4f12-253">Lorsque vous sélectionnez des mots pour les étiqueter en tant qu’entités :</span><span class="sxs-lookup"><span data-stu-id="d4f12-253">When selecting words to label them as entities:</span></span>
    > - <span data-ttu-id="d4f12-254">Pour les mots uniques, cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="d4f12-254">For single words just click them.</span></span>
    > - <span data-ttu-id="d4f12-255">Pour un ensemble de deux ou de plusieurs mots, cliquez au début et à la fin de l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="d4f12-255">For a set of two or more words, click at the beginning and then at the end of the set.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d4f12-256">Vous pouvez utiliser le bouton bascule de la *vue jetons* pour basculer entre les **entités/jetons**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-256">You can use the *Tokens View* toggle button to switch between **Entities / Tokens View**!</span></span>

19. <span data-ttu-id="d4f12-257">Les résultats doivent être affichés dans les images ci-dessous, avec la **vue entités/jetons**:</span><span class="sxs-lookup"><span data-stu-id="d4f12-257">The results should be as seen in the images below, showing the **Entities / Tokens View**:</span></span>

    ![Jetons & vues entités](images/AzureLabs-Lab3-18.png)
  
20. <span data-ttu-id="d4f12-259">À ce stade, appuyez sur le bouton **train** en haut à droite de la page et attendez que le petit indicateur rond soit vert.</span><span class="sxs-lookup"><span data-stu-id="d4f12-259">At this point press the **Train** button at the top-right of the page and wait for the small round indicator on it to turn green.</span></span> <span data-ttu-id="d4f12-260">Cela indique que LUIS a été correctement formé pour reconnaître cet objectif.</span><span class="sxs-lookup"><span data-stu-id="d4f12-260">This indicates that LUIS has been successfully trained to recognize this Intent.</span></span>

    ![Former LUIS](images/AzureLabs-Lab3-19.png)
 
21. <span data-ttu-id="d4f12-262">En guise d’exercice pour vous, créez une intention appelée **ChangeObjectSize**, en utilisant les entités *target*, Resize et *Resize*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-262">As an exercise for you, create a new Intent called **ChangeObjectSize**, using the Entities *target*, *upsize*, and *downsize*.</span></span>
22. <span data-ttu-id="d4f12-263">En suivant le même processus que l’intention précédente, insérez les huit (8) énoncés suivants pour la modification de la *taille* :</span><span class="sxs-lookup"><span data-stu-id="d4f12-263">Following the same process as the previous Intent, insert the following eight (8) Utterances for *Size* change:</span></span>

    ```
    increase the dimensions of that

    reduce the size of this

    i want the sphere smaller

    make the cylinder bigger

    size down the sphere

    size up the cube

    decrease the size of that object

    increase the size of this object
    ```

23. <span data-ttu-id="d4f12-264">Le résultat doit être similaire à celui de l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d4f12-264">The result should be like the one in the image below:</span></span>

    ![Configurer les jetons/entités ChangeObjectSize](images/AzureLabs-Lab3-20.png) 

24. <span data-ttu-id="d4f12-266">Une fois que les deux intentions, **ChangeObjectColor** et **ChangeObjectSize**, ont été créées et formés, cliquez sur le bouton **publier** situé en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="d4f12-266">Once both Intents, **ChangeObjectColor** and **ChangeObjectSize**, have been created and trained, click on the **PUBLISH** button on top of the page.</span></span>

    ![Publier le service LUIS](images/AzureLabs-Lab3-21.png)

25. <span data-ttu-id="d4f12-268">Sur la page de *publication* , vous allez finaliser et publier votre application Luis afin que votre code puisse y accéder.</span><span class="sxs-lookup"><span data-stu-id="d4f12-268">On the *Publish* page you will finalize and publish your LUIS App so that it can be accessed by your code.</span></span>

    1. <span data-ttu-id="d4f12-269">Définissez la *publication de* la liste déroulante sur **production**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-269">Set the drop down *Publish To* as **Production**.</span></span>
    2. <span data-ttu-id="d4f12-270">Définissez le *fuseau horaire sur votre* fuseau horaire.</span><span class="sxs-lookup"><span data-stu-id="d4f12-270">Set the *Timezone* to your time zone.</span></span>
    3. <span data-ttu-id="d4f12-271">Cochez la case **inclure tous les scores d’intention prédits**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-271">Check the box **Include all predicted intent scores**.</span></span>
    4. <span data-ttu-id="d4f12-272">Cliquez sur **publier dans l’emplacement de production**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-272">Click on **Publish to Production Slot**.</span></span>

        ![Paramètres de publication](images/AzureLabs-Lab3-22.png)

26. <span data-ttu-id="d4f12-274">Dans la section *ressources et clés*:</span><span class="sxs-lookup"><span data-stu-id="d4f12-274">In the section *Resources and Keys*:</span></span>

    1.  <span data-ttu-id="d4f12-275">Sélectionnez la région que vous définissez pour l’instance de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d4f12-275">Select the region you set for service instance in the Azure Portal.</span></span>
    2.  <span data-ttu-id="d4f12-276">Vous remarquerez un élément **Starter_Key** ci-dessous, ignorez-le.</span><span class="sxs-lookup"><span data-stu-id="d4f12-276">You will notice a **Starter_Key** element below, ignore it.</span></span>
    3.  <span data-ttu-id="d4f12-277">Cliquez sur **Ajouter une clé** et insérez la *clé* obtenue dans le portail Azure lors de la création de votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="d4f12-277">Click on **Add Key** and insert the *Key* that you obtained in the Azure Portal when you created your Service instance.</span></span> <span data-ttu-id="d4f12-278">Si votre Azure et le portail LUIS sont enregistrés dans le même utilisateur, vous trouverez des menus déroulants pour le *nom du client*, le nom de l' *abonnement*et la *clé* que vous souhaitez utiliser (le nom que vous avez fourni précédemment dans le portail Azure est le même que celui que vous avez fourni précédemment).</span><span class="sxs-lookup"><span data-stu-id="d4f12-278">If your Azure and the LUIS portal are logged into the same user, you will be provided drop-down menus for *Tenant name*, *Subscription Name*, and the *Key* you wish to use (will have the same name as you provided previously in the Azure Portal.</span></span>

    > [!IMPORTANT] 
    > <span data-ttu-id="d4f12-279">Sous *point de terminaison*, prenez une copie du point de terminaison correspondant à la clé que vous avez insérée, vous allez bientôt l’utiliser dans votre code.</span><span class="sxs-lookup"><span data-stu-id="d4f12-279">Underneath *Endpoint*, take a copy of the endpoint corresponding to the Key you have inserted, you will soon use it in your code.</span></span>
 
## <a name="chapter-3--set-up-the-unity-project"></a><span data-ttu-id="d4f12-280">Chapitre 3 : configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="d4f12-280">Chapter 3 – Set up the Unity project</span></span>

<span data-ttu-id="d4f12-281">Ce qui suit est une configuration classique pour le développement avec la réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="d4f12-281">The following is a typical set up for developing with the mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="d4f12-282">Ouvrez *Unity* et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-282">Open *Unity* and click **New**.</span></span> 

    ![Démarrez le nouveau projet Unity.](images/AzureLabs-Lab3-24.png)

2.  <span data-ttu-id="d4f12-284">Vous devez maintenant fournir un nom de projet Unity, insérer **MR_LUIS**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-284">You will now need to provide a Unity Project name, insert **MR_LUIS**.</span></span> <span data-ttu-id="d4f12-285">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-285">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="d4f12-286">Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés).</span><span class="sxs-lookup"><span data-stu-id="d4f12-286">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="d4f12-287">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-287">Then, click **Create project**.</span></span>

    ![Fournissez des détails pour le nouveau projet Unity.](images/AzureLabs-Lab3-25.png)
 
3.  <span data-ttu-id="d4f12-289">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-289">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="d4f12-290">Accédez à modifier > Préférences puis, dans la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-290">Go to Edit > Preferences and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="d4f12-291">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-291">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="d4f12-292">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="d4f12-292">Close the **Preferences** window.</span></span>

    ![Mettre à jour la préférence éditeur de script.](images/AzureLabs-Lab3-26.png)
 
4.  <span data-ttu-id="d4f12-294">Accédez ensuite à **fichier > paramètres de build** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton **changer de plateforme** .</span><span class="sxs-lookup"><span data-stu-id="d4f12-294">Next, go to **File > Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

    ![Fenêtre Paramètres de build, basculez plateforme vers UWP.](images/AzureLabs-Lab3-27.png)
 
5.  <span data-ttu-id="d4f12-296">Accédez à **fichier > paramètres de build** et assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="d4f12-296">Go to **File > Build Settings** and make sure that:</span></span>

    1. <span data-ttu-id="d4f12-297">L' **appareil cible** est défini sur **n’importe quel appareil**</span><span class="sxs-lookup"><span data-stu-id="d4f12-297">**Target Device** is set to **Any Device**</span></span>

        > <span data-ttu-id="d4f12-298">Pour Microsoft HoloLens, définissez **appareil cible** sur *HoloLens*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-298">For the Microsoft HoloLens, set **Target Device** to *HoloLens*.</span></span>

    2. <span data-ttu-id="d4f12-299">Le **type de build** est **D3D**</span><span class="sxs-lookup"><span data-stu-id="d4f12-299">**Build Type** is set to **D3D**</span></span>
    3. <span data-ttu-id="d4f12-300">Le **SDK** est configuré sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="d4f12-300">**SDK** is set to **Latest installed**</span></span>
    4. <span data-ttu-id="d4f12-301">**Version de Visual Studio** définie sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="d4f12-301">**Visual Studio Version** is set to **Latest installed**</span></span>
    5. <span data-ttu-id="d4f12-302">La **génération et l’exécution** sont définies sur l' **ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="d4f12-302">**Build and Run** is set to **Local Machine**</span></span>
    6. <span data-ttu-id="d4f12-303">Enregistrez la scène et ajoutez-la à la Build.</span><span class="sxs-lookup"><span data-stu-id="d4f12-303">Save the scene and add it to the build.</span></span>

        1. <span data-ttu-id="d4f12-304">Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-304">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="d4f12-305">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d4f12-305">A save window will appear.</span></span>
        
            ![Cliquez sur le bouton Ajouter des scènes ouvertes](images/AzureLabs-Lab3-28.png)

        2. <span data-ttu-id="d4f12-307">Créez un dossier pour cela, ainsi que toute nouvelle scène, puis sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez-le **scenes**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-307">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![Créer un dossier de scripts](images/AzureLabs-Lab3-29.png)

        3. <span data-ttu-id="d4f12-309">Ouvrez le dossier **scenes** nouvellement créé, puis dans le champ *nom de fichier*:, tapez **MR_LuisScene**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-309">Open your newly created **Scenes** folder, and then in the *File name*: text field, type **MR_LuisScene**, then press **Save**.</span></span>

            ![Donnez un nom à la nouvelle scène.](images/AzureLabs-Lab3-30.png)

    7. <span data-ttu-id="d4f12-311">Les paramètres restants, dans *paramètres de build*, doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="d4f12-311">The remaining settings, in *Build Settings*, should be left as default for now.</span></span>

6. <span data-ttu-id="d4f12-312">Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-312">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span> 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab3-31.png) 
 
7. <span data-ttu-id="d4f12-314">Dans ce volet, quelques paramètres doivent être vérifiés :</span><span class="sxs-lookup"><span data-stu-id="d4f12-314">In this panel, a few settings need to be verified:</span></span>

    1. <span data-ttu-id="d4f12-315">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="d4f12-315">In the **Other Settings** tab:</span></span>

        1. <span data-ttu-id="d4f12-316">La **version du runtime de script** doit être **stable** (équivalent .net 3,5).</span><span class="sxs-lookup"><span data-stu-id="d4f12-316">**Scripting Runtime Version** should be **Stable** (.NET 3.5 Equivalent).</span></span>
        2. <span data-ttu-id="d4f12-317">Le **backend de script** doit être **.net**</span><span class="sxs-lookup"><span data-stu-id="d4f12-317">**Scripting Backend** should be **.NET**</span></span>
        3. <span data-ttu-id="d4f12-318">Le **niveau de compatibilité** de l’API doit être **.net 4,6**</span><span class="sxs-lookup"><span data-stu-id="d4f12-318">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![Mettez à jour d’autres paramètres.](images/AzureLabs-Lab3-32.png)
      
    2. <span data-ttu-id="d4f12-320">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher :</span><span class="sxs-lookup"><span data-stu-id="d4f12-320">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        1. <span data-ttu-id="d4f12-321">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="d4f12-321">**InternetClient**</span></span>
        2. <span data-ttu-id="d4f12-322">**Cravate**</span><span class="sxs-lookup"><span data-stu-id="d4f12-322">**Microphone**</span></span>

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab3-33.png)

    3. <span data-ttu-id="d4f12-324">Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="d4f12-324">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Mettez à jour les paramètres X R.](images/AzureLabs-Lab3-34.png)

8.  <span data-ttu-id="d4f12-326">De retour dans les *paramètres de build* , les projets _Unity C#_  ne sont plus grisés. Cochez la case en regard de cette option.</span><span class="sxs-lookup"><span data-stu-id="d4f12-326">Back in *Build Settings* _Unity C#_ Projects is no longer greyed out; tick the checkbox next to this.</span></span> 
9.  <span data-ttu-id="d4f12-327">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="d4f12-327">Close the Build Settings window.</span></span>
10. <span data-ttu-id="d4f12-328">Enregistrez votre scène et votre projet (**fichier > enregistrer la scène/le fichier > enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="d4f12-328">Save your Scene and Project (**FILE > SAVE SCENE / FILE > SAVE PROJECT**).</span></span>

## <a name="chapter-4--create-the-scene"></a><span data-ttu-id="d4f12-329">Chapitre 4 : créer la scène</span><span class="sxs-lookup"><span data-stu-id="d4f12-329">Chapter 4 – Create the scene</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4f12-330">Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce fichier [. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20303%20-%20Natural%20language%20understanding/Azure-MR-303.unitypackage), à l’importer dans votre projet en tant que [package personnalisé](https://docs.unity3d.com/Manual/AssetPackages.html), puis à passer au [Chapitre 5](#chapter-5--create-the-microphonemanager-class).</span><span class="sxs-lookup"><span data-stu-id="d4f12-330">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to download this [.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20303%20-%20Natural%20language%20understanding/Azure-MR-303.unitypackage), import it into your project as a [Custom Package](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 5](#chapter-5--create-the-microphonemanager-class).</span></span> 

1.  <span data-ttu-id="d4f12-331">Cliquez avec le bouton droit dans une zone vide du *panneau hiérarchie*, sous **objet 3D**, ajoutez un **plan**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-331">Right-click in an empty area of the *Hierarchy Panel*, under **3D Object**, add a **Plane**.</span></span>

    ![Créez un plan.](images/AzureLabs-Lab3-35.png)

2.  <span data-ttu-id="d4f12-333">Sachez que lorsque vous cliquez à nouveau avec le bouton droit dans la *hiérarchie* pour créer d’autres objets, si le dernier objet est toujours sélectionné, l’objet sélectionné est le parent de votre nouvel objet.</span><span class="sxs-lookup"><span data-stu-id="d4f12-333">Be aware that when you right-click within the *Hierarchy* again to create more objects, if you still have the last object selected, the selected object will be the parent of your new object.</span></span> <span data-ttu-id="d4f12-334">Évitez de cliquer avec le bouton droit sur un espace vide dans la hiérarchie, puis cliquez avec le bouton droit.</span><span class="sxs-lookup"><span data-stu-id="d4f12-334">Avoid this left-clicking in an empty space within the Hierarchy, and then right-clicking.</span></span>

3.  <span data-ttu-id="d4f12-335">Répétez la procédure ci-dessus pour ajouter les objets suivants :</span><span class="sxs-lookup"><span data-stu-id="d4f12-335">Repeat the above procedure to add the following objects:</span></span>

    1. <span data-ttu-id="d4f12-336">*Cercle*</span><span class="sxs-lookup"><span data-stu-id="d4f12-336">*Sphere*</span></span>
    2. <span data-ttu-id="d4f12-337">*Éprouvette*</span><span class="sxs-lookup"><span data-stu-id="d4f12-337">*Cylinder*</span></span>
    3. <span data-ttu-id="d4f12-338">*Dernier*</span><span class="sxs-lookup"><span data-stu-id="d4f12-338">*Cube*</span></span>
    4. <span data-ttu-id="d4f12-339">*Texte 3D*</span><span class="sxs-lookup"><span data-stu-id="d4f12-339">*3D Text*</span></span>

4.  <span data-ttu-id="d4f12-340">La *hiérarchie* de scène qui en résulte doit être semblable à celle de l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d4f12-340">The resulting scene *Hierarchy* should be like the one in the image below:</span></span>

    ![Configuration de la hiérarchie de scène.](images/AzureLabs-Lab3-36.png)
 
5.  <span data-ttu-id="d4f12-342">Cliquez sur l' **appareil photo principal** pour le sélectionner, regardez dans le *panneau* de l’inspecteur, vous verrez l’objet Camera avec tous ses composants.</span><span class="sxs-lookup"><span data-stu-id="d4f12-342">Left click on the **Main Camera** to select it, look at the *Inspector Panel* you will see the Camera object with all the its components.</span></span>
6.  <span data-ttu-id="d4f12-343">Cliquez sur le bouton **Ajouter un composant** situé en bas du panneau de l' *inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-343">Click on the **Add Component** button located at the very bottom of the *Inspector Panel*.</span></span>

    ![Ajouter une source audio](images/AzureLabs-Lab3-37.png)
 
7.  <span data-ttu-id="d4f12-345">Recherchez le composant appelé *source audio*, comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d4f12-345">Search for the component called *Audio Source*, as shown above.</span></span>
8.  <span data-ttu-id="d4f12-346">Assurez-vous également que le composant *transformer* de l’appareil photo principal est défini sur (0, 0, 0). pour ce faire, appuyez sur l’icône d' **engrenage** en regard du composant *transformer* de l’appareil photo, puis sélectionnez **Réinitialiser**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-346">Also make sure that the *Transform* component of the Main Camera is set to (0,0,0), this can be done by pressing the **Gear** icon next to the Camera’s *Transform* component and selecting **Reset**.</span></span> <span data-ttu-id="d4f12-347">Le composant *transformer* doit alors ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="d4f12-347">The *Transform* component should then look like:</span></span>

    1.  <span data-ttu-id="d4f12-348">La *position* est définie sur **0, 0, 0**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-348">*Position* is set to **0, 0, 0**.</span></span>
    2.  <span data-ttu-id="d4f12-349">La *rotation* est définie sur **0, 0,** 0.</span><span class="sxs-lookup"><span data-stu-id="d4f12-349">*Rotation* is set to **0, 0, 0**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d4f12-350">Pour Microsoft HoloLens, vous devez également modifier les éléments suivants, qui font partie du composant **Camera** , qui se trouve sur votre **caméra principale**:</span><span class="sxs-lookup"><span data-stu-id="d4f12-350">For the Microsoft HoloLens, you will need to also change the following, which are part of the **Camera** component, which is on your **Main Camera**:</span></span>
    > - <span data-ttu-id="d4f12-351">**Indicateurs d’effacement :** Couleur unie.</span><span class="sxs-lookup"><span data-stu-id="d4f12-351">**Clear Flags:** Solid Color.</span></span>
    > - <span data-ttu-id="d4f12-352">**Arrière-plan** 'Black, alpha 0 ' – couleur hexadécimale : #00000000.</span><span class="sxs-lookup"><span data-stu-id="d4f12-352">**Background** ‘Black, Alpha 0’ – Hex color: #00000000.</span></span>

9.  <span data-ttu-id="d4f12-353">Cliquez avec le gauche sur le **plan** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="d4f12-353">Left click on the **Plane** to select it.</span></span> <span data-ttu-id="d4f12-354">Dans le *volet* de l’inspecteur, définissez le composant *transformer* avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4f12-354">In the *Inspector Panel* set the *Transform* component with the following values:</span></span>

    |       | <span data-ttu-id="d4f12-355">Transformation- *position*</span><span class="sxs-lookup"><span data-stu-id="d4f12-355">Transform - *Position*</span></span> |       |
    |:-----:|:----------------------:|:-----:|
    | <span data-ttu-id="d4f12-356">**X**</span><span class="sxs-lookup"><span data-stu-id="d4f12-356">**X**</span></span> | <span data-ttu-id="d4f12-357">**Y**</span><span class="sxs-lookup"><span data-stu-id="d4f12-357">**Y**</span></span>                  | <span data-ttu-id="d4f12-358">**Lettre**</span><span class="sxs-lookup"><span data-stu-id="d4f12-358">**Z**</span></span> |
    | <span data-ttu-id="d4f12-359">0</span><span class="sxs-lookup"><span data-stu-id="d4f12-359">0</span></span>     | <span data-ttu-id="d4f12-360">-1</span><span class="sxs-lookup"><span data-stu-id="d4f12-360">-1</span></span>                     | <span data-ttu-id="d4f12-361">0</span><span class="sxs-lookup"><span data-stu-id="d4f12-361">0</span></span>     |


10. <span data-ttu-id="d4f12-362">Cliquez sur la **sphère** à gauche pour la sélectionner.</span><span class="sxs-lookup"><span data-stu-id="d4f12-362">Left click on the **Sphere** to select it.</span></span> <span data-ttu-id="d4f12-363">Dans le *volet* de l’inspecteur, définissez le composant *transformer* avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4f12-363">In the *Inspector Panel* set the *Transform* component with the following values:</span></span>

    |       | <span data-ttu-id="d4f12-364">Transformation- *position*</span><span class="sxs-lookup"><span data-stu-id="d4f12-364">Transform - *Position*</span></span> |       |
    |:-----:|:----------------------:|:-----:|
    | <span data-ttu-id="d4f12-365">**X**</span><span class="sxs-lookup"><span data-stu-id="d4f12-365">**X**</span></span> | <span data-ttu-id="d4f12-366">**Y**</span><span class="sxs-lookup"><span data-stu-id="d4f12-366">**Y**</span></span>                  | <span data-ttu-id="d4f12-367">**Lettre**</span><span class="sxs-lookup"><span data-stu-id="d4f12-367">**Z**</span></span> |
    | <span data-ttu-id="d4f12-368">2</span><span class="sxs-lookup"><span data-stu-id="d4f12-368">2</span></span>     | <span data-ttu-id="d4f12-369">1</span><span class="sxs-lookup"><span data-stu-id="d4f12-369">1</span></span>                      | <span data-ttu-id="d4f12-370">2</span><span class="sxs-lookup"><span data-stu-id="d4f12-370">2</span></span>     |

11. <span data-ttu-id="d4f12-371">Cliquez avec le gauche sur le **cylindre** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="d4f12-371">Left click on the **Cylinder** to select it.</span></span> <span data-ttu-id="d4f12-372">Dans le *volet* de l’inspecteur, définissez le composant *transformer* avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4f12-372">In the *Inspector Panel* set the *Transform* component with the following values:</span></span>

    |       | <span data-ttu-id="d4f12-373">Transformation- *position*</span><span class="sxs-lookup"><span data-stu-id="d4f12-373">Transform - *Position*</span></span> |       |
    |:-----:|:----------------------:|:-----:|
    | <span data-ttu-id="d4f12-374">**X**</span><span class="sxs-lookup"><span data-stu-id="d4f12-374">**X**</span></span> | <span data-ttu-id="d4f12-375">**Y**</span><span class="sxs-lookup"><span data-stu-id="d4f12-375">**Y**</span></span>                  | <span data-ttu-id="d4f12-376">**Lettre**</span><span class="sxs-lookup"><span data-stu-id="d4f12-376">**Z**</span></span> |
    | <span data-ttu-id="d4f12-377">2</span><span class="sxs-lookup"><span data-stu-id="d4f12-377">-2</span></span>    | <span data-ttu-id="d4f12-378">1</span><span class="sxs-lookup"><span data-stu-id="d4f12-378">1</span></span>                      | <span data-ttu-id="d4f12-379">2</span><span class="sxs-lookup"><span data-stu-id="d4f12-379">2</span></span>     |

12. <span data-ttu-id="d4f12-380">Cliquez sur le **cube** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="d4f12-380">Left click on the **Cube** to select it.</span></span> <span data-ttu-id="d4f12-381">Dans le *volet* de l’inspecteur, définissez le composant *transformer* avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4f12-381">In the *Inspector Panel* set the *Transform* component with the following values:</span></span>

    |        | <span data-ttu-id="d4f12-382">Transformation- *position*</span><span class="sxs-lookup"><span data-stu-id="d4f12-382">Transform - *Position*</span></span> |       |  \| |       | <span data-ttu-id="d4f12-383">Transformation- *rotation*</span><span class="sxs-lookup"><span data-stu-id="d4f12-383">Transform - *Rotation*</span></span> |       |
    |:------:|:----------------------:|:-----:|:---:|:-----:|:----------------------:|:-----:|
    | <span data-ttu-id="d4f12-384">**X**</span><span class="sxs-lookup"><span data-stu-id="d4f12-384">**X**</span></span> | <span data-ttu-id="d4f12-385">**Y**</span><span class="sxs-lookup"><span data-stu-id="d4f12-385">**Y**</span></span>                   | <span data-ttu-id="d4f12-386">**Lettre**</span><span class="sxs-lookup"><span data-stu-id="d4f12-386">**Z**</span></span> |  \| | <span data-ttu-id="d4f12-387">**X**</span><span class="sxs-lookup"><span data-stu-id="d4f12-387">**X**</span></span> | <span data-ttu-id="d4f12-388">**Y**</span><span class="sxs-lookup"><span data-stu-id="d4f12-388">**Y**</span></span>                  | <span data-ttu-id="d4f12-389">**Lettre**</span><span class="sxs-lookup"><span data-stu-id="d4f12-389">**Z**</span></span> |
    | <span data-ttu-id="d4f12-390">0</span><span class="sxs-lookup"><span data-stu-id="d4f12-390">0</span></span>     | <span data-ttu-id="d4f12-391">1</span><span class="sxs-lookup"><span data-stu-id="d4f12-391">1</span></span>                       | <span data-ttu-id="d4f12-392">4</span><span class="sxs-lookup"><span data-stu-id="d4f12-392">4</span></span>     |  \| | <span data-ttu-id="d4f12-393">45</span><span class="sxs-lookup"><span data-stu-id="d4f12-393">45</span></span>    | <span data-ttu-id="d4f12-394">45</span><span class="sxs-lookup"><span data-stu-id="d4f12-394">45</span></span>                     | <span data-ttu-id="d4f12-395">0</span><span class="sxs-lookup"><span data-stu-id="d4f12-395">0</span></span>     | 

13. <span data-ttu-id="d4f12-396">Cliquez sur le **nouvel objet texte** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="d4f12-396">Left click on the **New Text** object to select it.</span></span> <span data-ttu-id="d4f12-397">Dans le *volet* de l’inspecteur, définissez le composant *transformer* avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4f12-397">In the *Inspector Panel* set the *Transform* component with the following values:</span></span>

    |       | <span data-ttu-id="d4f12-398">Transformation- *position*</span><span class="sxs-lookup"><span data-stu-id="d4f12-398">Transform - *Position*</span></span> |       |  \| |       | <span data-ttu-id="d4f12-399">Transformation-mettre à l' *échelle*</span><span class="sxs-lookup"><span data-stu-id="d4f12-399">Transform - *Scale*</span></span> |       |
    |:-----:|:----------------------:|:-----:|:---:|:-----:|:-------------------:|:-----:|
    | <span data-ttu-id="d4f12-400">**X**</span><span class="sxs-lookup"><span data-stu-id="d4f12-400">**X**</span></span> | <span data-ttu-id="d4f12-401">**Y**</span><span class="sxs-lookup"><span data-stu-id="d4f12-401">**Y**</span></span>                  | <span data-ttu-id="d4f12-402">**Lettre**</span><span class="sxs-lookup"><span data-stu-id="d4f12-402">**Z**</span></span> |  \| | <span data-ttu-id="d4f12-403">**X**</span><span class="sxs-lookup"><span data-stu-id="d4f12-403">**X**</span></span> | <span data-ttu-id="d4f12-404">**Y**</span><span class="sxs-lookup"><span data-stu-id="d4f12-404">**Y**</span></span>               | <span data-ttu-id="d4f12-405">**Lettre**</span><span class="sxs-lookup"><span data-stu-id="d4f12-405">**Z**</span></span> |
    | <span data-ttu-id="d4f12-406">2</span><span class="sxs-lookup"><span data-stu-id="d4f12-406">-2</span></span>    | <span data-ttu-id="d4f12-407">6</span><span class="sxs-lookup"><span data-stu-id="d4f12-407">6</span></span>                      | <span data-ttu-id="d4f12-408">9</span><span class="sxs-lookup"><span data-stu-id="d4f12-408">9</span></span>     |  \| | <span data-ttu-id="d4f12-409">0,1</span><span class="sxs-lookup"><span data-stu-id="d4f12-409">0.1</span></span>   | <span data-ttu-id="d4f12-410">0,1</span><span class="sxs-lookup"><span data-stu-id="d4f12-410">0.1</span></span>                 | <span data-ttu-id="d4f12-411">0,1</span><span class="sxs-lookup"><span data-stu-id="d4f12-411">0.1</span></span>   | 

14. <span data-ttu-id="d4f12-412">Remplacez la **taille de police** du composant de maillage de **texte** par **50**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-412">Change **Font Size** in the **Text Mesh** component to **50**.</span></span>
15. <span data-ttu-id="d4f12-413">Modifiez le *nom* de l’objet de **maillage de texte** en **texte de dictée**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-413">Change the *name* of the **Text Mesh** object to **Dictation Text**.</span></span>

    ![Créer un objet de texte 3D](images/AzureLabs-Lab3-38.png)
 
16. <span data-ttu-id="d4f12-415">La structure de votre volet de hiérarchie doit maintenant ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="d4f12-415">Your Hierarchy Panel structure should now look like this:</span></span>

    ![maillage de texte en mode scène](images/AzureLabs-Lab3-38b.png)


17. <span data-ttu-id="d4f12-417">La scène finale doit ressembler à l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d4f12-417">The final scene should look like the image below:</span></span>

    ![Vue scène.](images/AzureLabs-Lab3-39.png)
    
 
## <a name="chapter-5--create-the-microphonemanager-class"></a><span data-ttu-id="d4f12-419">Chapitre 5 : créer la classe MicrophoneManager</span><span class="sxs-lookup"><span data-stu-id="d4f12-419">Chapter 5 – Create the MicrophoneManager class</span></span>

<span data-ttu-id="d4f12-420">Le premier script que vous allez créer est la classe *MicrophoneManager* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-420">The first Script you are going to create is the *MicrophoneManager* class.</span></span> <span data-ttu-id="d4f12-421">À la suite de cela, vous allez créer le *LuisManager*, la classe des *comportements* et enfin la classe du *regard* (n’hésitez pas à créer tous ces éléments maintenant, bien qu’elle soit couverte à mesure que vous atteignez chaque chapitre).</span><span class="sxs-lookup"><span data-stu-id="d4f12-421">Following this, you will create the *LuisManager*, the *Behaviours* class, and lastly the *Gaze* class (feel free to create all these now, though it will be covered as you reach each Chapter).</span></span>

<span data-ttu-id="d4f12-422">La classe *MicrophoneManager* est chargée des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4f12-422">The *MicrophoneManager* class is responsible for:</span></span>

-   <span data-ttu-id="d4f12-423">Détection du périphérique d’enregistrement connecté au casque ou à l’ordinateur (selon la valeur par défaut).</span><span class="sxs-lookup"><span data-stu-id="d4f12-423">Detecting the recording device attached to the headset or machine (whichever is the default one).</span></span>
-   <span data-ttu-id="d4f12-424">Capturez l’audio (voix) et utilisez la dictée pour le stocker en tant que chaîne.</span><span class="sxs-lookup"><span data-stu-id="d4f12-424">Capture the audio (voice) and use dictation to store it as a string.</span></span>
-   <span data-ttu-id="d4f12-425">Une fois que la voix a été suspendue, soumettez la dictée à la classe *LuisManager* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-425">Once the voice has paused, submit the dictation to the *LuisManager* class.</span></span> 

<span data-ttu-id="d4f12-426">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="d4f12-426">To create this class:</span></span> 

1.  <span data-ttu-id="d4f12-427">Cliquez avec le bouton droit dans le *panneau Projet*, puis **créez > dossier**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-427">Right-click in the *Project Panel*, **Create > Folder**.</span></span> <span data-ttu-id="d4f12-428">Appelez le dossier **scripts**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-428">Call the folder **Scripts**.</span></span> 

    ![Créer un dossier de scripts.](images/AzureLabs-Lab3-40.png)
 
2.  <span data-ttu-id="d4f12-430">Après avoir créé le dossier **scripts** , double-cliquez dessus pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="d4f12-430">With the **Scripts** folder created, double click it, to open.</span></span> <span data-ttu-id="d4f12-431">Ensuite, dans ce dossier, cliquez avec le bouton droit sur, puis **créez > C# script**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-431">Then, within that folder, right-click, **Create > C# Script**.</span></span> <span data-ttu-id="d4f12-432">Nommez le script *MicrophoneManager*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-432">Name the script *MicrophoneManager*.</span></span> 

3.  <span data-ttu-id="d4f12-433">Double-cliquez sur *MicrophoneManager* pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-433">Double click on *MicrophoneManager* to open it with *Visual Studio*.</span></span>
4.  <span data-ttu-id="d4f12-434">Ajoutez les espaces de noms suivants au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="d4f12-434">Add the following namespaces to the top of the file:</span></span>

    ```csharp
        using UnityEngine;
        using UnityEngine.Windows.Speech;
    ```

5.  <span data-ttu-id="d4f12-435">Ajoutez ensuite les variables suivantes à l’intérieur de la classe *MicrophoneManager* :</span><span class="sxs-lookup"><span data-stu-id="d4f12-435">Then add the following variables inside the *MicrophoneManager* class:</span></span>

    ```csharp
        public static MicrophoneManager instance; //help to access instance of this object
        private DictationRecognizer dictationRecognizer;  //Component converting speech to text
        public TextMesh dictationText; //a UI object used to debug dictation result
    ``` 

6.  <span data-ttu-id="d4f12-436">Vous devez maintenant ajouter le code des méthodes *éveillés ()* et *Start ()* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-436">Code for *Awake()* and *Start()* methods now needs to be added.</span></span> <span data-ttu-id="d4f12-437">Ils sont appelés lorsque la classe est initialisée :</span><span class="sxs-lookup"><span data-stu-id="d4f12-437">These will be called when the class initializes:</span></span>

    ```csharp
        private void Awake()
        {
            // allows this class instance to behave like a singleton
            instance = this;
        }

        void Start()
        {
            if (Microphone.devices.Length > 0)
            {
                StartCapturingAudio();
                Debug.Log("Mic Detected");
            }
        }
    ```
 
7.  <span data-ttu-id="d4f12-438">À présent, vous avez besoin de la méthode utilisée par l’application pour démarrer et arrêter la capture vocale, et la passer à la classe *LuisManager* , que vous allez bientôt créer.</span><span class="sxs-lookup"><span data-stu-id="d4f12-438">Now you need the method that the App uses to start and stop the voice capture, and pass it to the *LuisManager* class, that you will build soon.</span></span> 

    ```csharp
        /// <summary>
        /// Start microphone capture, by providing the microphone as a continual audio source (looping),
        /// then initialise the DictationRecognizer, which will capture spoken words
        /// </summary>
        public void StartCapturingAudio()
        {
            if (dictationRecognizer == null)
            {
                dictationRecognizer = new DictationRecognizer
                {
                    InitialSilenceTimeoutSeconds = 60,
                    AutoSilenceTimeoutSeconds = 5
                };

                dictationRecognizer.DictationResult += DictationRecognizer_DictationResult;
                dictationRecognizer.DictationError += DictationRecognizer_DictationError;
            }
            dictationRecognizer.Start();
            Debug.Log("Capturing Audio...");
        }

        /// <summary>
        /// Stop microphone capture
        /// </summary>
        public void StopCapturingAudio()
        {
            dictationRecognizer.Stop();
            Debug.Log("Stop Capturing Audio...");
        }
    ```

8.  <span data-ttu-id="d4f12-439">Ajoutez un *Gestionnaire de dictée* qui sera appelé lorsque la voix sera interrompue.</span><span class="sxs-lookup"><span data-stu-id="d4f12-439">Add a *Dictation Handler* that will be invoked when the voice pauses.</span></span> <span data-ttu-id="d4f12-440">Cette méthode passera le texte de dictée à la classe *LuisManager* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-440">This method will pass the dictation text to the *LuisManager* class.</span></span>

    ```csharp
        /// <summary>
        /// This handler is called every time the Dictation detects a pause in the speech. 
        /// This method will stop listening for audio, send a request to the LUIS service 
        /// and then start listening again.
        /// </summary>
        private void DictationRecognizer_DictationResult(string dictationCaptured, ConfidenceLevel confidence)
        {
            StopCapturingAudio();
            StartCoroutine(LuisManager.instance.SubmitRequestToLuis(dictationCaptured, StartCapturingAudio));
            Debug.Log("Dictation: " + dictationCaptured);
            dictationText.text = dictationCaptured;
        }

        private void DictationRecognizer_DictationError(string error, int hresult)
        {
            Debug.Log("Dictation exception: " + error);
        }
    ```
 
    > [!IMPORTANT]
    > <span data-ttu-id="d4f12-441">Supprimez la méthode *Update ()* puisque cette classe ne l’utilisera pas.</span><span class="sxs-lookup"><span data-stu-id="d4f12-441">Delete the *Update()* method since this class will not use it.</span></span>

9.  <span data-ttu-id="d4f12-442">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-442">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d4f12-443">À ce stade, vous remarquerez qu’une erreur s’affiche dans le panneau de la console de l' *éditeur Unity*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-443">At this point you will notice an error appearing in the *Unity Editor Console Panel*.</span></span> <span data-ttu-id="d4f12-444">Cela est dû au fait que le code fait référence à la classe *LuisManager* que vous allez créer dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="d4f12-444">This is because the code references the *LuisManager* class which you will create in the next Chapter.</span></span>

## <a name="chapter-6--create-the-luismanager-class"></a><span data-ttu-id="d4f12-445">Chapitre 6 : créer la classe LUISManager</span><span class="sxs-lookup"><span data-stu-id="d4f12-445">Chapter 6 – Create the LUISManager class</span></span>

<span data-ttu-id="d4f12-446">Il est temps de créer la classe *LuisManager* , qui fera l’appel au service Azure Luis.</span><span class="sxs-lookup"><span data-stu-id="d4f12-446">It is time for you to create the *LuisManager* class, which will make the call to the Azure LUIS service.</span></span> 

<span data-ttu-id="d4f12-447">L’objectif de cette classe est de recevoir le texte de dictée de la classe *MicrophoneManager* et de l’envoyer au *API Language Understanding Azure* à analyser.</span><span class="sxs-lookup"><span data-stu-id="d4f12-447">The purpose of this class is to receive the dictation text from the *MicrophoneManager* class and send it to the *Azure Language Understanding API* to be analyzed.</span></span>

<span data-ttu-id="d4f12-448">Cette classe va désérialiser la réponse *JSON* et appeler les méthodes appropriées de la classe des *comportements* pour déclencher une action.</span><span class="sxs-lookup"><span data-stu-id="d4f12-448">This class will deserialize the *JSON* response and call the appropriate methods of the *Behaviours* class to trigger an action.</span></span>

<span data-ttu-id="d4f12-449">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="d4f12-449">To create this class:</span></span> 

1.  <span data-ttu-id="d4f12-450">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="d4f12-450">Double click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="d4f12-451">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-451">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="d4f12-452">Nommez le script *LuisManager*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-452">Name the script *LuisManager*.</span></span> 
3.  <span data-ttu-id="d4f12-453">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4f12-453">Double click on the script to open it with Visual Studio.</span></span>
4.  <span data-ttu-id="d4f12-454">Ajoutez les espaces de noms suivants au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="d4f12-454">Add the following namespaces to the top of the file:</span></span>

    ```csharp
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using System.IO;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

5.  <span data-ttu-id="d4f12-455">Vous commencerez par créer trois classes **à l’intérieur** de la classe *LuisManager* (dans le même fichier de script, au-dessus de la méthode *Start ()* ) qui représenteront la réponse JSON désérialisée d’Azure.</span><span class="sxs-lookup"><span data-stu-id="d4f12-455">You will begin by creating three classes **inside** the *LuisManager* class (within the same script file, above the *Start()* method) that will represent the deserialized JSON response from Azure.</span></span>

    ```csharp
        [Serializable] //this class represents the LUIS response
        public class AnalysedQuery
        {
            public TopScoringIntentData topScoringIntent;
            public EntityData[] entities;
            public string query;
        }

        // This class contains the Intent LUIS determines 
        // to be the most likely
        [Serializable]
        public class TopScoringIntentData
        {
            public string intent;
            public float score;
        }

        // This class contains data for an Entity
        [Serializable]
        public class EntityData
        {
            public string entity;
            public string type;
            public int startIndex;
            public int endIndex;
            public float score;
        }
    ```

6.  <span data-ttu-id="d4f12-456">Ensuite, ajoutez les variables suivantes à l’intérieur de la classe *LuisManager* :</span><span class="sxs-lookup"><span data-stu-id="d4f12-456">Next, add the following variables inside the *LuisManager* class:</span></span>
 
    ```csharp
        public static LuisManager instance;

        //Substitute the value of luis Endpoint with your own End Point
        string luisEndpoint = "https://westus.api.cognitive... add your endpoint from the Luis Portal";
    ```

7.  <span data-ttu-id="d4f12-457">Veillez à placer votre point de terminaison LUIS à l’heure actuelle (que vous aurez sur votre portail LUIS).</span><span class="sxs-lookup"><span data-stu-id="d4f12-457">Make sure to place your LUIS endpoint in now (which you will have from your LUIS portal).</span></span>

8.  <span data-ttu-id="d4f12-458">Le code de la méthode *éveillé ()* doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="d4f12-458">Code for the *Awake()* method now needs to be added.</span></span> <span data-ttu-id="d4f12-459">Cette méthode est appelée lorsque la classe est initialisée :</span><span class="sxs-lookup"><span data-stu-id="d4f12-459">This method will be called when the class initializes:</span></span>

    ```csharp
        private void Awake()
        {
            // allows this class instance to behave like a singleton
            instance = this;
        }
    ```

9.  <span data-ttu-id="d4f12-460">À présent, vous avez besoin des méthodes utilisées par cette application pour envoyer la dictée reçue de la classe *MicrophoneManager* à *Luis*, puis recevoir et désérialiser la réponse.</span><span class="sxs-lookup"><span data-stu-id="d4f12-460">Now you need the methods this application uses to send the dictation received from the *MicrophoneManager* class to *LUIS*, and then receive and deserialize the response.</span></span> 
10. <span data-ttu-id="d4f12-461">Une fois que la valeur de l’intention, et les entités associées, ont été déterminées, elles sont passées à l’instance de la classe des *comportements* pour déclencher l’action prévue.</span><span class="sxs-lookup"><span data-stu-id="d4f12-461">Once the value of the Intent, and associated Entities, have been determined, they are passed to the instance of the *Behaviours* class to trigger the intended action.</span></span>

    ```csharp
        /// <summary>
        /// Call LUIS to submit a dictation result.
        /// The done Action is called at the completion of the method.
        /// </summary>
        public IEnumerator SubmitRequestToLuis(string dictationResult, Action done)
        {
            string queryString = string.Concat(Uri.EscapeDataString(dictationResult));

            using (UnityWebRequest unityWebRequest = UnityWebRequest.Get(luisEndpoint + queryString))
            {
                yield return unityWebRequest.SendWebRequest();

                if (unityWebRequest.isNetworkError || unityWebRequest.isHttpError)
                {
                    Debug.Log(unityWebRequest.error);
                }
                else
                {
                    try
                    {
                        AnalysedQuery analysedQuery = JsonUtility.FromJson<AnalysedQuery>(unityWebRequest.downloadHandler.text);

                        //analyse the elements of the response 
                        AnalyseResponseElements(analysedQuery);
                    }
                    catch (Exception exception)
                    {
                        Debug.Log("Luis Request Exception Message: " + exception.Message);
                    }
                }

                done();
                yield return null;
            }
        }
    ```
 
11. <span data-ttu-id="d4f12-462">Créez une nouvelle méthode appelée *AnalyseResponseElements ()* qui lira les *AnalysedQuery* résultants et déterminez les entités.</span><span class="sxs-lookup"><span data-stu-id="d4f12-462">Create a new method called *AnalyseResponseElements()* that will read the resulting *AnalysedQuery* and determine the Entities.</span></span> <span data-ttu-id="d4f12-463">Une fois ces entités déterminées, elles sont transmises à l’instance de la classe des *comportements* à utiliser dans les actions.</span><span class="sxs-lookup"><span data-stu-id="d4f12-463">Once those Entities are determined, they will be passed to the instance of the *Behaviours* class to use in the actions.</span></span>

    ```csharp
        private void AnalyseResponseElements(AnalysedQuery aQuery)
        {
            string topIntent = aQuery.topScoringIntent.intent;

            // Create a dictionary of entities associated with their type
            Dictionary<string, string> entityDic = new Dictionary<string, string>();

            foreach (EntityData ed in aQuery.entities)
            {
                entityDic.Add(ed.type, ed.entity);
            }

            // Depending on the topmost recognized intent, read the entities name
            switch (aQuery.topScoringIntent.intent)
            {
                case "ChangeObjectColor":
                    string targetForColor = null;
                    string color = null;

                    foreach (var pair in entityDic)
                    {
                        if (pair.Key == "target")
                        {
                            targetForColor = pair.Value;
                        }
                        else if (pair.Key == "color")
                        {
                            color = pair.Value;
                        }
                    }

                    Behaviours.instance.ChangeTargetColor(targetForColor, color);
                    break;

                case "ChangeObjectSize":
                    string targetForSize = null;
                    foreach (var pair in entityDic)
                    {
                        if (pair.Key == "target")
                        {
                            targetForSize = pair.Value;
                        }
                    }

                    if (entityDic.ContainsKey("upsize") == true)
                    {
                        Behaviours.instance.UpSizeTarget(targetForSize);
                    }
                    else if (entityDic.ContainsKey("downsize") == true)
                    {
                        Behaviours.instance.DownSizeTarget(targetForSize);
                    }
                    break;
            }
        }
    ```
 
    > [!IMPORTANT]
    > <span data-ttu-id="d4f12-464">Supprimez les méthodes *Start ()* et *Update ()* puisque cette classe ne les utilise pas.</span><span class="sxs-lookup"><span data-stu-id="d4f12-464">Delete the *Start()* and *Update()* methods since this class will not use them.</span></span>

12. <span data-ttu-id="d4f12-465">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-465">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

> [!NOTE]
> <span data-ttu-id="d4f12-466">À ce stade, vous remarquerez que plusieurs erreurs apparaissent dans le panneau de la console de l' *éditeur Unity*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-466">At this point you will notice several errors appearing in the *Unity Editor Console Panel*.</span></span> <span data-ttu-id="d4f12-467">Cela est dû au fait que le code fait référence à la classe des *comportements* que vous allez créer dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="d4f12-467">This is because the code references the *Behaviours* class which you will create in the next Chapter.</span></span>

## <a name="chapter-7--create-the-behaviours-class"></a><span data-ttu-id="d4f12-468">Chapitre 7 : créer la classe des comportements</span><span class="sxs-lookup"><span data-stu-id="d4f12-468">Chapter 7 – Create the Behaviours class</span></span>

<span data-ttu-id="d4f12-469">La classe des *comportements* déclenchera les actions à l’aide des entités fournies par la classe *LuisManager* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-469">The *Behaviours* class will trigger the actions using the Entities provided by the *LuisManager* class.</span></span>

<span data-ttu-id="d4f12-470">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="d4f12-470">To create this class:</span></span> 

1.  <span data-ttu-id="d4f12-471">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="d4f12-471">Double click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="d4f12-472">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-472">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="d4f12-473">Nommez les *comportements*de script.</span><span class="sxs-lookup"><span data-stu-id="d4f12-473">Name the script *Behaviours*.</span></span> 
3.  <span data-ttu-id="d4f12-474">Double-cliquez sur le script pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-474">Double click on the script to open it with *Visual Studio*.</span></span>
4.  <span data-ttu-id="d4f12-475">Ajoutez ensuite les variables suivantes à l’intérieur de la classe des *comportements* :</span><span class="sxs-lookup"><span data-stu-id="d4f12-475">Then add the following variables inside the *Behaviours* class:</span></span>

    ```csharp
        public static Behaviours instance;

        // the following variables are references to possible targets
        public GameObject sphere;
        public GameObject cylinder;
        public GameObject cube;
        internal GameObject gazedTarget;
    ```
 
5.  <span data-ttu-id="d4f12-476">Ajoutez le code de la méthode *éveillé ()* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-476">Add the *Awake()* method code.</span></span> <span data-ttu-id="d4f12-477">Cette méthode est appelée lorsque la classe est initialisée :</span><span class="sxs-lookup"><span data-stu-id="d4f12-477">This method will be called when the class initializes:</span></span>

    ```csharp
        void Awake()
        {
            // allows this class instance to behave like a singleton
            instance = this;
        }
    ```
 
6.  <span data-ttu-id="d4f12-478">Les méthodes suivantes sont appelées par la classe *LuisManager* (que vous avez créée précédemment) pour déterminer l’objet qui est la cible de la requête, puis déclencher l’action appropriée.</span><span class="sxs-lookup"><span data-stu-id="d4f12-478">The following methods are called by the *LuisManager* class (which you have created previously) to determine which object is the target of the query and then trigger the appropriate action.</span></span>

    ```csharp
        /// <summary>
        /// Changes the color of the target GameObject by providing the name of the object
        /// and the name of the color
        /// </summary>
        public void ChangeTargetColor(string targetName, string colorName)
        {
            GameObject foundTarget = FindTarget(targetName);
            if (foundTarget != null)
            {
                Debug.Log("Changing color " + colorName + " to target: " + foundTarget.name);

                switch (colorName)
                {
                    case "blue":
                        foundTarget.GetComponent<Renderer>().material.color = Color.blue;
                        break;

                    case "red":
                        foundTarget.GetComponent<Renderer>().material.color = Color.red;
                        break;

                    case "yellow":
                        foundTarget.GetComponent<Renderer>().material.color = Color.yellow;
                        break;

                    case "green":
                        foundTarget.GetComponent<Renderer>().material.color = Color.green;
                        break;

                    case "white":
                        foundTarget.GetComponent<Renderer>().material.color = Color.white;
                        break;

                    case "black":
                        foundTarget.GetComponent<Renderer>().material.color = Color.black;
                        break;
                }          
            }
        }

        /// <summary>
        /// Reduces the size of the target GameObject by providing its name
        /// </summary>
        public void DownSizeTarget(string targetName)
        {
            GameObject foundTarget = FindTarget(targetName);
            foundTarget.transform.localScale -= new Vector3(0.5F, 0.5F, 0.5F);
        }

        /// <summary>
        /// Increases the size of the target GameObject by providing its name
        /// </summary>
        public void UpSizeTarget(string targetName)
        {
            GameObject foundTarget = FindTarget(targetName);
            foundTarget.transform.localScale += new Vector3(0.5F, 0.5F, 0.5F);
        }
    ```
 
7.  <span data-ttu-id="d4f12-479">Ajoutez la méthode *FindTarget ()* pour déterminer laquelle du *GameObjects* est la cible de l’intention actuelle.</span><span class="sxs-lookup"><span data-stu-id="d4f12-479">Add the *FindTarget()* method to determine which of the *GameObjects* is the target of the current Intent.</span></span> <span data-ttu-id="d4f12-480">Cette méthode définit par défaut la cible sur le *gameobject* « en regard » si aucune cible explicite n’est définie dans les entités.</span><span class="sxs-lookup"><span data-stu-id="d4f12-480">This method defaults the target to the *GameObject* being “gazed” if no explicit target is defined in the Entities.</span></span>

    ```csharp
        /// <summary>
        /// Determines which object reference is the target GameObject by providing its name
        /// </summary>
        private GameObject FindTarget(string name)
        {
            GameObject targetAsGO = null;

            switch (name)
            {
                case "sphere":
                    targetAsGO = sphere;
                    break;

                case "cylinder":
                    targetAsGO = cylinder;
                    break;

                case "cube":
                    targetAsGO = cube;
                    break;

                case "this": // as an example of target words that the user may use when looking at an object
                case "it":  // as this is the default, these are not actually needed in this example
                case "that":
                default: // if the target name is none of those above, check if the user is looking at something
                    if (gazedTarget != null) 
                    {
                        targetAsGO = gazedTarget;
                    }
                    break;
            }
            return targetAsGO;
        }
    ```
 
    > [!IMPORTANT]
    > <span data-ttu-id="d4f12-481">Supprimez les méthodes *Start ()* et *Update ()* puisque cette classe ne les utilise pas.</span><span class="sxs-lookup"><span data-stu-id="d4f12-481">Delete the *Start()* and *Update()* methods since this class will not use them.</span></span>

8.  <span data-ttu-id="d4f12-482">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-482">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-8--create-the-gaze-class"></a><span data-ttu-id="d4f12-483">Chapitre 8 : créer la classe en regard</span><span class="sxs-lookup"><span data-stu-id="d4f12-483">Chapter 8 – Create the Gaze Class</span></span>

<span data-ttu-id="d4f12-484">La dernière classe dont vous aurez besoin pour compléter cette application est la classe de *regard* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-484">The last class that you will need to complete this app is the *Gaze* class.</span></span> <span data-ttu-id="d4f12-485">Cette classe met à jour la référence au *gameobject* actuellement dans le focus visuel de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d4f12-485">This class updates the reference to the *GameObject* currently in the user’s visual focus.</span></span>

<span data-ttu-id="d4f12-486">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="d4f12-486">To create this Class:</span></span> 

1.  <span data-ttu-id="d4f12-487">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="d4f12-487">Double click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="d4f12-488">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-488">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="d4f12-489">Nommez le script point de *regard*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-489">Name the script *Gaze*.</span></span> 
3.  <span data-ttu-id="d4f12-490">Double-cliquez sur le script pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-490">Double click on the script to open it with *Visual Studio*.</span></span>
4.  <span data-ttu-id="d4f12-491">Insérez le code suivant pour cette classe :</span><span class="sxs-lookup"><span data-stu-id="d4f12-491">Insert the following code for this class:</span></span>

    ```csharp
        using UnityEngine;

        public class Gaze : MonoBehaviour
        {        
            internal GameObject gazedObject;
            public float gazeMaxDistance = 300;

            void Update()
            {
                // Uses a raycast from the Main Camera to determine which object is gazed upon.
                Vector3 fwd = gameObject.transform.TransformDirection(Vector3.forward);
                Ray ray = new Ray(Camera.main.transform.position, fwd);
                RaycastHit hit;
                Debug.DrawRay(Camera.main.transform.position, fwd);

                if (Physics.Raycast(ray, out hit, gazeMaxDistance) && hit.collider != null)
                {
                    if (gazedObject == null)
                    {
                        gazedObject = hit.transform.gameObject;

                        // Set the gazedTarget in the Behaviours class
                        Behaviours.instance.gazedTarget = gazedObject;
                    }
                }
                else
                {
                    ResetGaze();
                }         
            }

            // Turn the gaze off, reset the gazeObject in the Behaviours class.
            public void ResetGaze()
            {
                if (gazedObject != null)
                {
                    Behaviours.instance.gazedTarget = null;
                    gazedObject = null;
                }
            }
        }
    ```
 
5.  <span data-ttu-id="d4f12-492">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-492">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-9--completing-the-scene-setup"></a><span data-ttu-id="d4f12-493">Chapitre 9 : fin de la configuration de la scène</span><span class="sxs-lookup"><span data-stu-id="d4f12-493">Chapter 9 – Completing the scene setup</span></span>

1.  <span data-ttu-id="d4f12-494">Pour terminer la configuration de la scène, faites glisser chaque script que vous avez créé à partir du dossier scripts vers l’objet **caméra principale** dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-494">To complete the setup of the scene, drag each script that you have created from the Scripts Folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span>
2.  <span data-ttu-id="d4f12-495">Sélectionnez l' **appareil photo principal** et examinez le panneau de l' *inspecteur*, vous devez être en mesure de voir chaque script joint, et vous remarquerez qu’il existe des paramètres sur chaque script qui doivent être définis.</span><span class="sxs-lookup"><span data-stu-id="d4f12-495">Select the **Main Camera** and look at the *Inspector Panel*, you should be able to see each script that you have attached, and you will notice that there are parameters on each script that are yet to be set.</span></span>

    ![Définition des cibles de référence de l’appareil photo.](images/AzureLabs-Lab3-41.png)

3.  <span data-ttu-id="d4f12-497">Pour définir correctement ces paramètres, suivez ces instructions :</span><span class="sxs-lookup"><span data-stu-id="d4f12-497">To set these parameters correctly, follow these instructions:</span></span>

    1. <span data-ttu-id="d4f12-498">*MicrophoneManager*:</span><span class="sxs-lookup"><span data-stu-id="d4f12-498">*MicrophoneManager*:</span></span>

        - <span data-ttu-id="d4f12-499">À partir du *panneau hiérarchie*, faites glisser l’objet **texte de dictée** dans la zone valeur du paramètre de **texte de dictée** .</span><span class="sxs-lookup"><span data-stu-id="d4f12-499">From the *Hierarchy Panel*, drag the **Dictation Text** object into the **Dictation Text** parameter value box.</span></span>

    2. <span data-ttu-id="d4f12-500">*Comportements*, à partir du *volet hiérarchie*:</span><span class="sxs-lookup"><span data-stu-id="d4f12-500">*Behaviours*, from the *Hierarchy Panel*:</span></span>

        - <span data-ttu-id="d4f12-501">Faites glisser l’objet **Sphere** dans la zone de la cible de référence *Sphere* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-501">Drag the **Sphere** object into the *Sphere* reference target box.</span></span>
        - <span data-ttu-id="d4f12-502">Faites glisser le **cylindre** dans la zone de la cible de référence *cylindrique* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-502">Drag the **Cylinder** into the *Cylinder* reference target box.</span></span>
        - <span data-ttu-id="d4f12-503">Faites glisser le **cube** dans la zone de la cible de la référence du *cube* .</span><span class="sxs-lookup"><span data-stu-id="d4f12-503">Drag the **Cube** into the *Cube* reference target box.</span></span>

    3. <span data-ttu-id="d4f12-504">Point de *regard*:</span><span class="sxs-lookup"><span data-stu-id="d4f12-504">*Gaze*:</span></span>

        - <span data-ttu-id="d4f12-505">Définissez la *distance maximale* du point de regard sur **300** (si ce n’est pas déjà le cas).</span><span class="sxs-lookup"><span data-stu-id="d4f12-505">Set the *Gaze Max Distance* to **300** (if it is not already).</span></span> 

4.  <span data-ttu-id="d4f12-506">Le résultat doit ressembler à l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d4f12-506">The result should look like the image below:</span></span>

    ![L’indication des cibles de référence de l’appareil photo, désormais définie.](images/AzureLabs-Lab3-42.png)
 
## <a name="chapter-10--test-in-the-unity-editor"></a><span data-ttu-id="d4f12-508">Chapitre 10 – test dans l’éditeur Unity</span><span class="sxs-lookup"><span data-stu-id="d4f12-508">Chapter 10 – Test in the Unity Editor</span></span>

<span data-ttu-id="d4f12-509">Vérifiez que la configuration de la scène est correctement implémentée.</span><span class="sxs-lookup"><span data-stu-id="d4f12-509">Test that the Scene setup is properly implemented.</span></span>

<span data-ttu-id="d4f12-510">Vérifiez que :</span><span class="sxs-lookup"><span data-stu-id="d4f12-510">Ensure that:</span></span>

-   <span data-ttu-id="d4f12-511">Tous les scripts sont attachés à l’objet **Camera principal** .</span><span class="sxs-lookup"><span data-stu-id="d4f12-511">All the scripts are attached to the **Main Camera** object.</span></span> 
-   <span data-ttu-id="d4f12-512">Tous les champs du volet principal de l’inspecteur de l' *appareil photo* sont correctement affectés.</span><span class="sxs-lookup"><span data-stu-id="d4f12-512">All the fields in the *Main Camera Inspector Panel* are assigned properly.</span></span>

1.  <span data-ttu-id="d4f12-513">Appuyez sur le bouton **lecture** dans l' *éditeur Unity*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-513">Press the **Play** button in the *Unity Editor*.</span></span> <span data-ttu-id="d4f12-514">L’application doit s’exécuter au sein du casque immersif attaché.</span><span class="sxs-lookup"><span data-stu-id="d4f12-514">The App should be running within the attached immersive headset.</span></span>

2.  <span data-ttu-id="d4f12-515">Essayez quelques énoncés, tels que :</span><span class="sxs-lookup"><span data-stu-id="d4f12-515">Try a few utterances, such as:</span></span>

    ```
    make the cylinder red

    change the cube to yellow

    I want the sphere blue

    make this to green

    change it to white
    ```

    > [!NOTE]
    > <span data-ttu-id="d4f12-516">Si une erreur s’affiche dans la console Unity à propos du changement de périphérique audio par défaut, la scène peut ne pas fonctionner comme prévu.</span><span class="sxs-lookup"><span data-stu-id="d4f12-516">If you see an error in the Unity console about the default audio device changing, the scene may not function as expected.</span></span> <span data-ttu-id="d4f12-517">Cela est dû à la façon dont le portail de réalité mixte traite les microphones intégrés pour les casques.</span><span class="sxs-lookup"><span data-stu-id="d4f12-517">This is due to the way the mixed reality portal deals with built-in microphones for headsets that have them.</span></span> <span data-ttu-id="d4f12-518">Si vous voyez cette erreur, arrêtez simplement la scène et redémarrez-la et les choses devraient fonctionner comme prévu.</span><span class="sxs-lookup"><span data-stu-id="d4f12-518">If you see this error, simply stop the scene and start it again and things should work as expected.</span></span>

## <a name="chapter-11--build-and-sideload-the-uwp-solution"></a><span data-ttu-id="d4f12-519">Chapitre 11 : créer et chargement la solution UWP</span><span class="sxs-lookup"><span data-stu-id="d4f12-519">Chapter 11 – Build and sideload the UWP Solution</span></span>

<span data-ttu-id="d4f12-520">Une fois que vous avez vérifié que l’application fonctionne dans l’éditeur Unity, vous êtes prêt à créer et à déployer.</span><span class="sxs-lookup"><span data-stu-id="d4f12-520">Once you have ensured that the application is working in the Unity Editor, you are ready to Build and Deploy.</span></span>

<span data-ttu-id="d4f12-521">Pour générer :</span><span class="sxs-lookup"><span data-stu-id="d4f12-521">To Build:</span></span>

1.  <span data-ttu-id="d4f12-522">Enregistrez la scène en cours en cliquant sur **fichier > enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-522">Save the current scene by clicking on **File > Save**.</span></span>
2.  <span data-ttu-id="d4f12-523">Accédez à **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-523">Go to **File > Build Settings**.</span></span>
3.  <span data-ttu-id="d4f12-524">Cochez la case **projets Unity C#**  (utile pour afficher et déboguer votre code une fois le projet UWP créé.</span><span class="sxs-lookup"><span data-stu-id="d4f12-524">Tick the box called **Unity C# Projects** (useful for seeing and debugging your code once the UWP project is created.</span></span>
4.  <span data-ttu-id="d4f12-525">Cliquez sur **Ajouter des scènes ouvertes**, puis cliquez sur **générer**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-525">Click on **Add Open Scenes**, then click **Build**.</span></span>

    ![Fenêtre Paramètres de build](images/AzureLabs-Lab3-43.png)

4.  <span data-ttu-id="d4f12-527">Vous serez invité à sélectionner le dossier dans lequel vous souhaitez générer la solution.</span><span class="sxs-lookup"><span data-stu-id="d4f12-527">You will be prompted to select the folder where you want to build the Solution.</span></span> 

5.  <span data-ttu-id="d4f12-528">Créez un dossier *Builds* et, dans ce dossier, créez un autre dossier avec le nom approprié de votre choix.</span><span class="sxs-lookup"><span data-stu-id="d4f12-528">Create a *BUILDS* folder and within that folder create another folder with an appropriate name of your choice.</span></span> 
6.  <span data-ttu-id="d4f12-529">Cliquez sur **Sélectionner un dossier** pour commencer la build à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="d4f12-529">Click **Select Folder** to begin the build at that location.</span></span>
 
    <span data-ttu-id="d4f12-530">![dossier créer des builds](images/AzureLabs-Lab3-44.png)
    ![dossier de builds](images/AzureLabs-Lab3-45.png)</span><span class="sxs-lookup"><span data-stu-id="d4f12-530">![Create Builds Folder](images/AzureLabs-Lab3-44.png)
![Select Builds Folder](images/AzureLabs-Lab3-45.png)</span></span>
 
7.  <span data-ttu-id="d4f12-531">Une fois la génération de Unity terminée (cela peut prendre un certain temps), elle doit ouvrir une fenêtre de l' **Explorateur de fichiers** à l’emplacement de votre Build.</span><span class="sxs-lookup"><span data-stu-id="d4f12-531">Once Unity has finished building (it might take some time), it should open a **File Explorer** window at the location of your build.</span></span>

<span data-ttu-id="d4f12-532">Pour déployer sur l’ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="d4f12-532">To Deploy on Local Machine:</span></span>

1.  <span data-ttu-id="d4f12-533">Dans *Visual Studio*, ouvrez le fichier solution créé dans le [chapitre précédent](#chapter-10--test-in-the-unity-editor).</span><span class="sxs-lookup"><span data-stu-id="d4f12-533">In *Visual Studio*, open the solution file that has been created in the [previous Chapter](#chapter-10--test-in-the-unity-editor).</span></span>
2.  <span data-ttu-id="d4f12-534">Dans la **plateforme**de la solution, sélectionnez **x86**, **ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-534">In the **Solution Platform**, select **x86**, **Local Machine**.</span></span>
3.  <span data-ttu-id="d4f12-535">Dans la **configuration** de la solution, sélectionnez **Déboguer**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-535">In the **Solution Configuration** select **Debug**.</span></span>

    > <span data-ttu-id="d4f12-536">Pour Microsoft HoloLens, il peut s’avérer plus facile de définir cette valeur sur *machine distante*, afin de ne pas être attaché à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d4f12-536">For the Microsoft HoloLens, you may find it easier to set this to *Remote Machine*, so that you are not tethered to your computer.</span></span> <span data-ttu-id="d4f12-537">Toutefois, vous devez également effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d4f12-537">Though, you will need to also do the following:</span></span>
    > - <span data-ttu-id="d4f12-538">Identifiez l' **adresse IP** de votre HoloLens, qui se trouve dans les *paramètres > réseau & Internet > les options avancées du Wi-Fi >* ; IPv4 est l’adresse que vous devez utiliser.</span><span class="sxs-lookup"><span data-stu-id="d4f12-538">Know the **IP Address** of your HoloLens, which can be found within the *Settings > Network & Internet > Wi-Fi > Advanced Options*; the IPv4 is the address you should use.</span></span> 
    > - <span data-ttu-id="d4f12-539">Assurez-vous que le **mode développeur** est **activé**; trouvé dans *paramètres > mettre à jour & > de sécurité pour les développeurs*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-539">Ensure **Developer Mode** is **On**; found in *Settings > Update & Security > For developers*.</span></span>

    ![Déployer l’application](images/AzureLabs-Lab3-46.png)
 
4.  <span data-ttu-id="d4f12-541">Accédez au **menu Générer** , puis cliquez sur **déployer la solution** pour chargement l’application sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d4f12-541">Go to the **Build menu** and click on **Deploy Solution** to sideload the application to your machine.</span></span>
5.  <span data-ttu-id="d4f12-542">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancées.</span><span class="sxs-lookup"><span data-stu-id="d4f12-542">Your App should now appear in the list of installed apps, ready to be launched!</span></span>
6.  <span data-ttu-id="d4f12-543">Une fois lancé, l’application vous invite à autoriser l’accès au _microphone_.</span><span class="sxs-lookup"><span data-stu-id="d4f12-543">Once launched, the App will prompt you to authorize access to the _Microphone_.</span></span> <span data-ttu-id="d4f12-544">Utilisez les *contrôleurs de mouvement*ou l' *entrée vocale*, ou le *clavier* pour appuyer sur le bouton **Oui** .</span><span class="sxs-lookup"><span data-stu-id="d4f12-544">Use the *Motion Controllers*, or *Voice Input*, or the *Keyboard* to press the **YES** button.</span></span> 

## <a name="chapter-12--improving-your-luis-service"></a><span data-ttu-id="d4f12-545">Chapitre 12 : amélioration de votre service LUIS</span><span class="sxs-lookup"><span data-stu-id="d4f12-545">Chapter 12 – Improving your LUIS service</span></span>

>[!IMPORTANT] 
> <span data-ttu-id="d4f12-546">Ce chapitre est extrêmement important et devra peut-être être parcouru plusieurs fois, car cela permet d’améliorer la précision de votre service LUIS : Veillez à effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="d4f12-546">This chapter is incredibly important, and may need to be iterated upon several times, as it will help improve the accuracy of your LUIS service: ensure you complete this.</span></span>

<span data-ttu-id="d4f12-547">Pour améliorer le niveau de compréhension fourni par LUIS, vous devez capturer de nouveaux énoncés et les utiliser pour former à nouveau votre application LUIS.</span><span class="sxs-lookup"><span data-stu-id="d4f12-547">To improve the level of understanding provided by LUIS you need to capture new utterances and use them to re-train your LUIS App.</span></span>

<span data-ttu-id="d4f12-548">Par exemple, vous avez peut-être formé LUIS pour comprendre l’augmentation et la taille, mais ne souhaitez-vous pas que votre application comprenne également des mots tels que « agrandir » ?</span><span class="sxs-lookup"><span data-stu-id="d4f12-548">For example, you might have trained LUIS to understand “Increase” and “Upsize”, but wouldn’t you want your app to also understand words like “Enlarge”?</span></span>

<span data-ttu-id="d4f12-549">Une fois que vous avez utilisé votre application plusieurs fois, tout ce que vous avez dit est collecté par LUIS et disponible dans le portail LUIS.</span><span class="sxs-lookup"><span data-stu-id="d4f12-549">Once you have used your application a few times, everything you have said will be collected by LUIS and available in the LUIS PORTAL.</span></span>

1.  <span data-ttu-id="d4f12-550">Accédez à votre application de portail en suivant ce [lien](https://www.luis.ai/home)et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="d4f12-550">Go to your portal application following this [LINK](https://www.luis.ai/home), and Log In.</span></span>
2.  <span data-ttu-id="d4f12-551">Une fois que vous êtes connecté avec vos informations d’identification MS, cliquez sur le nom de votre *application*.</span><span class="sxs-lookup"><span data-stu-id="d4f12-551">Once you are logged in with your MS Credentials, click on your *App name*.</span></span>
3.  <span data-ttu-id="d4f12-552">Cliquez sur le bouton **vérifier les énoncés de point de terminaison** à gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="d4f12-552">Click the **Review endpoint utterances** button on the left of the page.</span></span>

    ![Passer en revue les énoncés](images/AzureLabs-Lab3-47.png)
 
4.  <span data-ttu-id="d4f12-554">Une liste des énoncés qui ont été envoyés à LUIS par votre application de réalité mixte s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d4f12-554">You will be shown a list of the Utterances that have been sent to LUIS by your mixed reality Application.</span></span>

    ![Liste des énoncés](images/AzureLabs-Lab3-48.png)
 
<span data-ttu-id="d4f12-556">Vous remarquerez certaines *entités*en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="d4f12-556">You will notice some highlighted *Entities*.</span></span> 

<span data-ttu-id="d4f12-557">En pointant sur chaque mot en surbrillance, vous pouvez examiner chaque énoncé et déterminer l’entité qui a été reconnue correctement, les entités qui sont incorrectes et les entités qui sont manquées.</span><span class="sxs-lookup"><span data-stu-id="d4f12-557">By hovering over each highlighted word, you can review each Utterance and determine which Entity has been recognized correctly, which Entities are wrong and which Entities are missed.</span></span>

<span data-ttu-id="d4f12-558">Dans l’exemple ci-dessus, il a été constaté que le mot « Spear » avait été mis en surbrillance comme cible. il est donc nécessaire de corriger l’erreur, ce qui se fait en pointant sur le mot avec la souris et en cliquant sur **Supprimer l’étiquette**.</span><span class="sxs-lookup"><span data-stu-id="d4f12-558">In the example above, it was found that the word “spear” had been highlighted as a target, so it necessary to correct the mistake, which is done by hovering over the word with the mouse and clicking **Remove Label**.</span></span>

<span data-ttu-id="d4f12-559">![vérifier les énoncés](images/AzureLabs-Lab3-49.png)
![supprimer l’image de l’étiquette](images/AzureLabs-Lab3-50.png)</span><span class="sxs-lookup"><span data-stu-id="d4f12-559">![Check utterances](images/AzureLabs-Lab3-49.png)
![Remove Label Image](images/AzureLabs-Lab3-50.png)</span></span>
 
5.  <span data-ttu-id="d4f12-560">Si vous trouvez des énoncés qui ne sont pas corrects, vous pouvez les supprimer à l’aide du bouton **supprimer** sur le côté droit de l’écran.</span><span class="sxs-lookup"><span data-stu-id="d4f12-560">If you find Utterances that are completely wrong, you can delete them using the **Delete** button on the right side of the screen.</span></span>

    ![Supprimer les énoncés erronés](images/AzureLabs-Lab3-51.png)

6.  <span data-ttu-id="d4f12-562">Ou si vous pensez que LUIS a interprété correctement l’énoncé, vous pouvez valider sa compréhension en utilisant le bouton **Ajouter à l’intention alignée** .</span><span class="sxs-lookup"><span data-stu-id="d4f12-562">Or if you feel that LUIS has interpreted the Utterance correctly, you can validate its understanding by using the **Add To Aligned Intent** button.</span></span>

    ![Ajouter à l’intention alignée](images/AzureLabs-Lab3-52.png)

7.  <span data-ttu-id="d4f12-564">Une fois que vous avez trié tous les énoncés affichés, essayez de recharger la page pour voir si d’autres sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="d4f12-564">Once you have sorted all the displayed Utterances, try and reload the page to see if more are available.</span></span>
8.  <span data-ttu-id="d4f12-565">Il est très important de répéter ce processus autant de fois que possible pour améliorer la compréhension de votre application.</span><span class="sxs-lookup"><span data-stu-id="d4f12-565">It is very important to repeat this process as many times as possible to improve your application understanding.</span></span> 

<span data-ttu-id="d4f12-566">**Amusez-vous!**</span><span class="sxs-lookup"><span data-stu-id="d4f12-566">**Have fun!**</span></span>

## <a name="your-finished-luis-integrated-application"></a><span data-ttu-id="d4f12-567">Votre application intégrée LUIS est terminée</span><span class="sxs-lookup"><span data-stu-id="d4f12-567">Your finished LUIS Integrated application</span></span>

<span data-ttu-id="d4f12-568">Félicitations, vous avez créé une application de réalité mixte qui s’appuie sur le service Azure Language Understanding intelligence pour comprendre ce que l’utilisateur dit, et agir sur ces informations.</span><span class="sxs-lookup"><span data-stu-id="d4f12-568">Congratulations, you built a mixed reality app that leverages the Azure Language Understanding Intelligence Service, to understand what a user says, and act on that information.</span></span>

![résultat de l’atelier](images/AzureLabs-Lab3-000.png)

## <a name="bonus-exercises"></a><span data-ttu-id="d4f12-570">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="d4f12-570">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="d4f12-571">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="d4f12-571">Exercise 1</span></span>

<span data-ttu-id="d4f12-572">Si vous utilisez cette application, vous remarquerez peut-être que si vous pointez sur l’objet Floor et que vous demandez à changer sa couleur, il le fera.</span><span class="sxs-lookup"><span data-stu-id="d4f12-572">While using this application you might notice that if you gaze at the Floor object and ask to change its color, it will do so.</span></span> <span data-ttu-id="d4f12-573">Pouvez-vous apprendre comment empêcher votre application de changer la couleur d’étage ?</span><span class="sxs-lookup"><span data-stu-id="d4f12-573">Can you work out how to stop your application from changing the Floor color?</span></span>

### <a name="exercise-2"></a><span data-ttu-id="d4f12-574">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="d4f12-574">Exercise 2</span></span>

<span data-ttu-id="d4f12-575">Essayez d’étendre les fonctionnalités de LUIS et de l’application, en ajoutant des fonctionnalités supplémentaires pour les objets dans la scène. par exemple, créez des objets au point d’accès en regard, en fonction de ce que l’utilisateur prétend, puis pouvez utiliser ces objets avec les objets de scène actuels, avec les commandes existantes.</span><span class="sxs-lookup"><span data-stu-id="d4f12-575">Try extending the LUIS and App capabilities, adding additional functionality for objects in scene; as an example, create new objects at the Gaze hit point, depending on what the user says, and then be able to use those objects alongside current scene objects, with the existing commands.</span></span> 
