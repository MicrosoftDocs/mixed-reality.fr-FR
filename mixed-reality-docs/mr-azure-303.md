---
title: MR et Azure 303 - langage naturel (LUIS)
description: Terminer ce cours pour apprendre à implémenter Azure Intelligence Service LUIS (Language Understanding) au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, service d’intelligence language understanding, luis, vr immersives, hololens,
ms.openlocfilehash: fb00fe9079e49a7ada507e7407ef45fa7eeb0d7e
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595914"
---
>[!NOTE]
><span data-ttu-id="b6e6e-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="b6e6e-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="b6e6e-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="b6e6e-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="b6e6e-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="b6e6e-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-and-azure-303-natural-language-understanding-luis"></a><span data-ttu-id="b6e6e-110">MR et Azure 303 : Compréhension du langage naturel (LUIS)</span><span class="sxs-lookup"><span data-stu-id="b6e6e-110">MR and Azure 303: Natural language understanding (LUIS)</span></span>

<span data-ttu-id="b6e6e-111">Dans ce cours, vous allez apprendre à intégrer la compréhension du langage dans une application de réalité mixte à l’aide d’Azure Cognitive Services, avec l’API de compréhension du langage.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-111">In this course, you will learn how to integrate Language Understanding into a mixed reality application using Azure Cognitive Services, with the Language Understanding API.</span></span>

![résultat de laboratoire](images/AzureLabs-Lab3-000.png)

<span data-ttu-id="b6e6e-113">*Reconnaissance vocale (LUIS)* est un service Microsoft Azure, qui fournit aux applications la possibilité d’effectuer la signification en dehors de l’entrée d’utilisateur, telles que via extraction qu’une personne peut le souhaitez, dans leurs propres mots.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-113">*Language Understanding (LUIS)* is a Microsoft Azure service, which provides applications with the ability to make meaning out of user input, such as through extracting what a person might want, in their own words.</span></span> <span data-ttu-id="b6e6e-114">Cela est possible via machine learning, qui comprend et apprend les informations d’entrée et qui peut ensuite répondre avec des informations détaillées et pertinentes.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-114">This is achieved through machine learning, which understands and learns the input information, and then can reply with detailed, relevant, information.</span></span> <span data-ttu-id="b6e6e-115">Pour plus d’informations, visitez le [page de Azure LUIS (Language Understanding)](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-115">For more information, visit the [Azure Language Understanding (LUIS) page](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/).</span></span>

<span data-ttu-id="b6e6e-116">Avoir terminé ce cours, vous disposez d’une application de casque immersives de réalité mixte qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-116">Having completed this course, you will have a mixed reality immersive headset application which will be able to do the following:</span></span>

1.  <span data-ttu-id="b6e6e-117">Capturer la voix d’entrée d’utilisateur, à l’aide du Microphone relié au casque immersif.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-117">Capture user input speech, using the Microphone attached to the immersive headset.</span></span> 
2.  <span data-ttu-id="b6e6e-118">Envoyer la dictée capturée le *Azure Language Understanding Intelligent Service* (*LUIS*).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-118">Send the captured dictation the *Azure Language Understanding Intelligent Service* (*LUIS*).</span></span> 
3.  <span data-ttu-id="b6e6e-119">Avoir extrait LUIS ce qui signifie que l’envoi d’informations, qui sera analysé et tente de déterminer que l’intention de demande de l’utilisateur sera.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-119">Have LUIS extract meaning from the send information, which will be analyzed, and attempt to determine the intent of the user’s request will be made.</span></span>

<span data-ttu-id="b6e6e-120">Développement incluent la création d’une application où l’utilisateur sera en mesure d’utiliser la voix et/ou les regards pour modifier la taille et la couleur des objets dans la scène.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-120">Development will include the creation of an app where the user will be able to use voice and/or gaze to change the size and the color of the objects in the scene.</span></span> <span data-ttu-id="b6e6e-121">L’utilisation de contrôleurs de mouvement n’est pas traitée.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-121">The use of motion controllers will not be covered.</span></span>

<span data-ttu-id="b6e6e-122">Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-122">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="b6e6e-123">Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-123">This course is designed to teach you how to integrate an Azure Service with your Unity Project.</span></span> <span data-ttu-id="b6e6e-124">Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-124">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

<span data-ttu-id="b6e6e-125">Soyez prêt à former LUIS plusieurs fois, ce qui est couvert dans [chapitre 12](#chapter-12--improving-your-luis-service).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-125">Be prepared to Train LUIS several times, which is covered in [Chapter 12](#chapter-12--improving-your-luis-service).</span></span> <span data-ttu-id="b6e6e-126">Vous obtiendrez meilleurs résultats les plus temps que Luis a été formé.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-126">You will get better results the more times LUIS has been trained.</span></span>

## <a name="device-support"></a><span data-ttu-id="b6e6e-127">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="b6e6e-127">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="b6e6e-128">Cours</span><span class="sxs-lookup"><span data-stu-id="b6e6e-128">Course</span></span></th><th style="width:150px"> <span data-ttu-id="b6e6e-129"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="b6e6e-129"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="b6e6e-130"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="b6e6e-130"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="b6e6e-131">MR et Azure 303 : Compréhension du langage naturel (LUIS)</span><span class="sxs-lookup"><span data-stu-id="b6e6e-131">MR and Azure 303: Natural language understanding (LUIS)</span></span></td><td style="text-align: center;"> <span data-ttu-id="b6e6e-132">✔️</span><span class="sxs-lookup"><span data-stu-id="b6e6e-132">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="b6e6e-133">✔️</span><span class="sxs-lookup"><span data-stu-id="b6e6e-133">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="b6e6e-134">Si ce cours se concentre principalement sur des casques Windows Mixed Reality IMMERSIFS (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours pour Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-134">While this course primarily focuses on Windows Mixed Reality immersive (VR) headsets, you can also apply what you learn in this course to Microsoft HoloLens.</span></span> <span data-ttu-id="b6e6e-135">Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-135">As you follow along with the course, you will see notes on any changes you might need to employ to support HoloLens.</span></span> <span data-ttu-id="b6e6e-136">Lorsque vous utilisez HoloLens, vous pouvez remarquer quelques echo durant la capture de la voix.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-136">When using HoloLens, you may notice some echo during voice capture.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6e6e-137">Prérequis</span><span class="sxs-lookup"><span data-stu-id="b6e6e-137">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="b6e6e-138">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-138">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="b6e6e-139">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-139">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="b6e6e-140">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous .</span><span class="sxs-lookup"><span data-stu-id="b6e6e-140">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="b6e6e-141">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-141">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="b6e6e-142">Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)</span><span class="sxs-lookup"><span data-stu-id="b6e6e-142">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="b6e6e-143">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="b6e6e-143">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md)
- [<span data-ttu-id="b6e6e-144">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="b6e6e-144">The latest Windows 10 SDK</span></span>](install-the-tools.md)
- [<span data-ttu-id="b6e6e-145">Unity 2017.4</span><span class="sxs-lookup"><span data-stu-id="b6e6e-145">Unity 2017.4</span></span>](install-the-tools.md)
- [<span data-ttu-id="b6e6e-146">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="b6e6e-146">Visual Studio 2017</span></span>](install-the-tools.md)
- <span data-ttu-id="b6e6e-147">Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="b6e6e-147">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="b6e6e-148">Un ensemble de casque avec un microphone intégré (si le casque n’a pas un mic intégré et les haut-parleurs)</span><span class="sxs-lookup"><span data-stu-id="b6e6e-148">A set of headphones with a built-in microphone (if the headset doesn't have a built-in mic and speakers)</span></span>
- <span data-ttu-id="b6e6e-149">Accès à Internet pour le programme d’installation Azure et l’extraction de LUIS</span><span class="sxs-lookup"><span data-stu-id="b6e6e-149">Internet access for Azure setup and LUIS retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="b6e6e-150">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="b6e6e-150">Before you start</span></span>

1.  <span data-ttu-id="b6e6e-151">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-151">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span> 
2.  <span data-ttu-id="b6e6e-152">Pour permettre à votre machine pour activer la dictée, accédez à **Windows Paramètres > confidentialité > vocale, la saisie manuscrite & tapant** et appuyez sur le bouton **sur Activer le services de reconnaissance vocale et les suggestions en tapant**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-152">To allow your machine to enable Dictation, go to **Windows Settings > Privacy > Speech, Inking & Typing** and press on the button **Turn On speech services and typing suggestions**.</span></span>
3.  <span data-ttu-id="b6e6e-153">Le code dans ce didacticiel vous permettra d’enregistrer à partir de la **par défaut un appareil Microphone** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-153">The code in this tutorial will allow you to record from the **Default Microphone Device** set on your machine.</span></span> <span data-ttu-id="b6e6e-154">Assurez-vous que l’appareil Microphone par défaut est défini comme celui que vous souhaitez utiliser pour capturer votre voix.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-154">Make sure the Default Microphone Device is set as the one you wish to use to capture your voice.</span></span>
4.  <span data-ttu-id="b6e6e-155">Si votre casque a un microphone intégré, assurez-vous que l’option *« Lorsque j’ai wear mon casque, basculez vers casque mic »* est activé dans le *Portal de réalité mixte* paramètres.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-155">If your headset has a built-in microphone, make sure the option *“When I wear my headset, switch to headset mic”* is turned on in the *Mixed Reality Portal* settings.</span></span>

    ![Configuration de casque immersive](images/AzureLabs-Lab3-00.png)

## <a name="chapter-1--setup-azure-portal"></a><span data-ttu-id="b6e6e-157">Chapitre 1 : configurer le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b6e6e-157">Chapter 1 – Setup Azure Portal</span></span>

<span data-ttu-id="b6e6e-158">Pour utiliser le *Language Understanding* service dans Azure, vous devez configurer une instance du service à être mis à disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-158">To use the *Language Understanding* service in Azure, you will need to configure an instance of the service to be made available to your application.</span></span>

1.  <span data-ttu-id="b6e6e-159">Connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-159">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6e6e-160">Si vous n’avez pas déjà un compte Azure, vous devrez créer un.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-160">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="b6e6e-161">Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-161">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="b6e6e-162">Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez *Language Understanding*, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-162">Once you are logged in, click on **New** in the top left corner, and search for *Language Understanding*, and click **Enter**.</span></span> 

    ![Créer une ressource de LUIS](images/AzureLabs-Lab3-01.png)

    > [!NOTE]
    > <span data-ttu-id="b6e6e-164">Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-164">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>
 
3.  <span data-ttu-id="b6e6e-165">La nouvelle page à droite fournit une description du service de reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-165">The new page to the right will provide a description of the Language Understanding service.</span></span> <span data-ttu-id="b6e6e-166">En bas à gauche de cette page, sélectionnez le **créer** bouton, pour créer une instance de ce service.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-166">At the bottom left of this page, select the **Create** button, to create an instance of this service.</span></span>

    ![Création du service LUIS - notice légale](images/AzureLabs-Lab3-02.png)
 
4.  <span data-ttu-id="b6e6e-168">Une fois que vous avez cliqué sur Créer :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-168">Once you have clicked on Create:</span></span>

    1. <span data-ttu-id="b6e6e-169">Insérez votre souhaitée **nom** pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-169">Insert your desired **Name** for this service instance.</span></span>
    2. <span data-ttu-id="b6e6e-170">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-170">Select a **Subscription**.</span></span>
    3. <span data-ttu-id="b6e6e-171">Sélectionnez le **niveau tarifaire** appropriés pour vous, s’il s’agit du premier temps à créer un *Service LUIS*, un niveau gratuit (nommé F0) doit être disponible pour vous.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-171">Select the **Pricing Tier** appropriate for you, if this is the first time creating a *LUIS Service*, a free tier (named F0) should be available to you.</span></span> <span data-ttu-id="b6e6e-172">L’allocation gratuite doit être plus que suffisante pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-172">The free allocation should be more than sufficient for this course.</span></span>
    4. <span data-ttu-id="b6e6e-173">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-173">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="b6e6e-174">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-174">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="b6e6e-175">Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-175">It is recommended to keep all the Azure services associated with a single project (e.g. such as these courses) under a common resource group).</span></span> 

        > <span data-ttu-id="b6e6e-176">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-176">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5. <span data-ttu-id="b6e6e-177">Déterminer le **emplacement** pour votre groupe de ressources (si vous créez un nouveau groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-177">Determine the **Location** for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="b6e6e-178">Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-178">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="b6e6e-179">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-179">Some Azure assets are only available in certain regions.</span></span>
    6. <span data-ttu-id="b6e6e-180">Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-180">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>
    7. <span data-ttu-id="b6e6e-181">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-181">Select **Create**.</span></span>

        ![Créer un service LUIS - entrée d’utilisateur](images/AzureLabs-Lab3-03.png)
 
5.  <span data-ttu-id="b6e6e-183">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-183">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>
6.  <span data-ttu-id="b6e6e-184">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-184">A notification will appear in the portal once the Service instance is created.</span></span> 
 
    ![Nouvelle image de notification Azure](images/AzureLabs-Lab3-04.png)

7.  <span data-ttu-id="b6e6e-186">Cliquez sur la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-186">Click on the notification to explore your new Service instance.</span></span>

    ![Notification de création de ressources](images/AzureLabs-Lab3-05.png)
 
8.  <span data-ttu-id="b6e6e-188">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-188">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="b6e6e-189">Vous êtes redirigé vers votre nouvelle instance de service LUIS.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-189">You will be taken to your new LUIS service instance.</span></span> 
 
    ![Accès aux clés de LUIS](images/AzureLabs-Lab3-06.png)

9.  <span data-ttu-id="b6e6e-191">Dans ce didacticiel, votre application devra effectuer des appels à votre service, par l’intermédiaire à l’aide de la clé d’abonnement de votre service.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-191">Within this tutorial, your application will need to make calls to your service, which is done through using your service’s Subscription Key.</span></span>
10. <span data-ttu-id="b6e6e-192">À partir de la *Guide de démarrage rapide* page, de votre *API LUIS* de service, accédez à la première étape, *récupérez vos clés*, puis cliquez sur **clés** (vous pouvez également parvenir en cliquant sur le lien hypertexte bleu clés, situé dans le menu de navigation de services, indiqué par l’icône de clé).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-192">From the *Quick start* page, of your *LUIS API* service, navigate to the first step, *Grab your keys*, and click **Keys** (you can also achieve this by clicking the blue hyperlink Keys, located in the services navigation menu, denoted by the key icon).</span></span> <span data-ttu-id="b6e6e-193">Cela permet de révéler votre service *clés*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-193">This will reveal your service *Keys*.</span></span>
11. <span data-ttu-id="b6e6e-194">Effectuez une copie de l’une des clés affichées, car vous en aurez besoin plus loin dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-194">Take a copy of one of the displayed keys, as you will need this later in your project.</span></span> 
12. <span data-ttu-id="b6e6e-195">Dans le *Service* page, cliquez sur *portail Language Understanding* d’être redirigé vers la page Web que vous utiliserez pour créer votre nouveau Service, au sein de l’application LUIS.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-195">In the *Service* page, click on *Language Understanding Portal* to be redirected to the webpage which you will use to create your new Service, within the LUIS App.</span></span> 

## <a name="chapter-2--the-language-understanding-portal"></a><span data-ttu-id="b6e6e-196">Chapitre 2 – portail Language Understanding</span><span class="sxs-lookup"><span data-stu-id="b6e6e-196">Chapter 2 – The Language Understanding Portal</span></span>

<span data-ttu-id="b6e6e-197">Dans cette section, vous allez apprendre à rendre une application LUIS sur LUIS Portal.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-197">In this section you will learn how to make a LUIS App on the LUIS Portal.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b6e6e-198">Notez que la configuration la *entités*, *intentions*, et *énoncés* au sein de ce chapitre n'est que la première étape dans la création de votre service LUIS : vous devrez également reformer le service, plusieurs fois, par conséquent, pour le rendre plus précis.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-198">Please be aware, that setting up the *Entities*, *Intents*, and *Utterances* within this chapter is only the first step in building your LUIS service: you will also need to retrain the service, several times, so to make it more accurate.</span></span> <span data-ttu-id="b6e6e-199">Reformation de votre service est couvert dans le [dernier chapitre](#chapter-12--improving-your-luis-service) de ce cours, par conséquent, assurez-vous de suivre la procédure.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-199">Retraining your service is covered in the [last Chapter](#chapter-12--improving-your-luis-service) of this course, so ensure that you complete it.</span></span>

1.  <span data-ttu-id="b6e6e-200">Lorsque vous atteignez le *portail Language Understanding*, vous devrez peut-être vous connecter, si vous n’êtes pas déjà fait, avec les mêmes informations d’identification que votre portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-200">Upon reaching the *Language Understanding Portal*, you may need to login, if you are not already, with the same credentials as your Azure portal.</span></span> 

    ![Page de connexion de LUIS](images/AzureLabs-Lab3-07.png)
 
2.  <span data-ttu-id="b6e6e-202">S’il s’agit de la première fois à l’aide de LUIS, vous devez faire défiler jusqu’en bas de la page d’accueil, à rechercher, puis cliquez sur le **application LUIS créer** bouton.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-202">If this is your first time using LUIS, you will need to scroll down to the bottom of the welcome page, to find and click on the **Create LUIS app** button.</span></span>

    ![Créer la page d’application LUIS](images/AzureLabs-Lab3-08.png)
 
3.  <span data-ttu-id="b6e6e-204">Une fois connecté, cliquez sur **mes applications** (si vous n’êtes pas dans cette section).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-204">Once logged in, click **My apps** (if you are not in that section currently).</span></span> <span data-ttu-id="b6e6e-205">Vous pouvez ensuite cliquer sur **créer une nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-205">You can then click on **Create new app**.</span></span>

    ![LUIS - mon image d’applications](images/AzureLabs-Lab3-09.png)
 
4.  <span data-ttu-id="b6e6e-207">Donnez à votre application un *nom*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-207">Give your app a *Name*.</span></span>
5.  <span data-ttu-id="b6e6e-208">Si votre application est censée pour comprendre une langue différente de l’anglais, vous devez modifier le *Culture* à la langue appropriée.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-208">If your app is supposed to understand a language different from English, you should change the *Culture* to the appropriate language.</span></span>
6.  <span data-ttu-id="b6e6e-209">Vous pouvez également y ajouter un *Description* de votre nouvelle application LUIS.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-209">Here you can also add a *Description* of your new LUIS app.</span></span>

    ![LUIS - créer une application](images/AzureLabs-Lab3-10.png)

7.  <span data-ttu-id="b6e6e-211">Une fois que vous appuyez sur **fait**, vous devez entrer le *Build* page de votre nouvelle *LUIS* application.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-211">Once you press **Done**, you will enter the *Build* page of your new *LUIS* application.</span></span>
8.  <span data-ttu-id="b6e6e-212">Il existe quelques concepts importants ici :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-212">There are a few important concepts to understand here:</span></span>

    -   <span data-ttu-id="b6e6e-213">*Intention*, représente la méthode qui sera appelée après une requête à partir de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-213">*Intent*, represents the method that will be called following a query from the user.</span></span> <span data-ttu-id="b6e6e-214">Un *intention* peut avoir un ou plusieurs *entités*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-214">An *INTENT* may have one or more *ENTITIES*.</span></span>
    -   <span data-ttu-id="b6e6e-215">*Entité*, est un composant de la requête qui décrit les informations relatives à la *intention*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-215">*Entity*, is a component of the query that describes information relevant to the *INTENT*.</span></span>
    -   <span data-ttu-id="b6e6e-216">*Énoncés*, sont des exemples de requêtes fournies par le développeur, ce LUIS utilisera pour effectuer l’apprentissage lui-même.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-216">*Utterances*, are examples of queries provided by the developer, that LUIS will use to train itself.</span></span>

<span data-ttu-id="b6e6e-217">Si ces concepts ne sont pas parfaitement effacer, ne vous inquiétez pas, comme ce cours sera clarifier les davantage dans ce chapitre.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-217">If these concepts are not perfectly clear, do not worry, as this course will clarify them further in this chapter.</span></span>

<span data-ttu-id="b6e6e-218">Vous allez commencer en créant le *entités* nécessaire pour générer ce cours.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-218">You will begin by creating the *Entities* needed to build this course.</span></span>

9.  <span data-ttu-id="b6e6e-219">Sur le côté gauche de la page, cliquez sur *entités*, puis cliquez sur **créer entité**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-219">On the left side of the page, click on *Entities*, then click on **Create new entity**.</span></span>

    ![Créer une nouvelle entité](images/AzureLabs-Lab3-11.png)

10. <span data-ttu-id="b6e6e-221">Appelez la nouvelle entité *couleur*, définissez son type sur *Simple*, puis appuyez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-221">Call the new Entity *color*, set its type to *Simple*, then press **Done**.</span></span>

    ![Créer une entité simple - couleur](images/AzureLabs-Lab3-12.png)
 
11. <span data-ttu-id="b6e6e-223">Répétez ce processus pour créer trois (3) plus Simple entités nommées :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-223">Repeat this process to create three (3) more Simple Entities named:</span></span>

    -   <span data-ttu-id="b6e6e-224">*upsize*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-224">*upsize*</span></span>
    -   <span data-ttu-id="b6e6e-225">*downsize*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-225">*downsize*</span></span>
    -   <span data-ttu-id="b6e6e-226">*target*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-226">*target*</span></span>

<span data-ttu-id="b6e6e-227">Le résultat doit ressembler à l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-227">The result should look like the image below:</span></span>

![Résultat de la création d’entités](images/AzureLabs-Lab3-13.png)
 
<span data-ttu-id="b6e6e-229">À ce stade vous pouvez commencer à créer *intentions*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-229">At this point you can begin creating *Intents*.</span></span> 

> [!WARNING]
> <span data-ttu-id="b6e6e-230">Ne supprimez pas le **aucun** intention.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-230">Do not delete the **None** intent.</span></span>

12. <span data-ttu-id="b6e6e-231">Sur le côté gauche de la page, cliquez sur **intentions**, puis cliquez sur **créer nouveau intention**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-231">On the left side of the page, click on **Intents**, then click on **Create new intent**.</span></span>

    ![Créer nouveau intentions](images/AzureLabs-Lab3-14.png)

13. <span data-ttu-id="b6e6e-233">Appelez la nouvelle *intention* **ChangeObjectColor**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-233">Call the new *Intent* **ChangeObjectColor**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b6e6e-234">Cela *intention* nom est utilisé dans le code plus loin dans ce cours, par conséquent, pour de meilleurs résultats, utilisez ce nom exactement comme prévu.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-234">This *Intent* name is used within the code later in this course, so for best results, use this name exactly as provided.</span></span>

<span data-ttu-id="b6e6e-235">Après avoir confirmé le nom que vous serez dirigé vers la Page d’intentions.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-235">Once you confirm the name you will be directed to the Intents Page.</span></span>

![LUIS - page d’intentions](images/AzureLabs-Lab3-15.png)

<span data-ttu-id="b6e6e-237">Vous remarquerez qu’il existe une zone de texte vous invitant à type 5 ou plus différent *énoncés*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-237">You will notice that there is a textbox asking you to type 5 or more different *Utterances*.</span></span>

> [!NOTE]
> <span data-ttu-id="b6e6e-238">LUIS convertit tous les énoncés en minuscules.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-238">LUIS converts all Utterances to lower case.</span></span>

14. <span data-ttu-id="b6e6e-239">Insérez le code suivant *énoncé* dans la zone de texte supérieur (actuellement avec le texte *Type exemples environ 5...*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-239">Insert the following *Utterance* in the top textbox (currently with the text *Type about 5 examples…*</span></span> <span data-ttu-id="b6e6e-240">), puis appuyez sur **entrée**:</span><span class="sxs-lookup"><span data-stu-id="b6e6e-240">), and press **Enter**:</span></span>

```
The color of the cylinder must be red
```

<span data-ttu-id="b6e6e-241">Vous remarquerez que la nouvelle *énoncé* s’affiche dans une liste en dessous.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-241">You will notice that the new *Utterance* will appear in a list underneath.</span></span>

<span data-ttu-id="b6e6e-242">Suivant le même processus, insérez les énoncés suivants de six (6) :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-242">Following the same process, insert the following six (6) Utterances:</span></span>

```
make the cube black

make the cylinder color white

change the sphere to red

change it to green

make this yellow

change the color of this object to blue
```

<span data-ttu-id="b6e6e-243">Pour chaque énoncé que vous avez créé, vous devez identifier quels mots doivent être utilisés par LUIS en tant qu’entités.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-243">For each Utterance you have created, you must identify which words should be used by LUIS as Entities.</span></span> <span data-ttu-id="b6e6e-244">Dans cet exemple, vous avez besoin étiqueter toutes les couleurs en tant qu’un *couleur* référence d’entité et toutes les la possible sur une cible, car un *cible* entité.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-244">In this example you need to label all the colors as a *color* Entity, and all the possible reference to a target as a *target* Entity.</span></span>

15. <span data-ttu-id="b6e6e-245">Pour ce faire, essayez de cliquer sur le mot *cylindre* dans la première énoncé, puis sélectionnez *cible*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-245">To do so, try clicking on the word *cylinder* in the first Utterance and select *target*.</span></span>

    ![Identifier les cibles d’énoncé](images/AzureLabs-Lab3-16.png)
 
16. <span data-ttu-id="b6e6e-247">Cliquez maintenant sur le mot *rouge* dans la première énoncé, puis sélectionnez *couleur*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-247">Now click on the word *red* in the first Utterance and select *color*.</span></span>

    ![Identifier les entités de l’énoncé](images/AzureLabs-Lab3-17.png)
 
17. <span data-ttu-id="b6e6e-249">En outre, l’étiquette de la ligne suivante où *cube* doit être un *cible*, et *noir* doit être un *couleur*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-249">Label the next line also, where *cube* should be a *target*, and *black* should be a *color*.</span></span> <span data-ttu-id="b6e6e-250">Notez également l’utilisation des mots *'this'*, *« it »*, et *'cet objet'*, ce qui nous mettons à disposition, par conséquent, pour que les types de cible non spécifique disponibles également.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-250">Notice also the use of the words *‘this’*, *‘it’*, and *‘this object’*, which we are providing, so to have non-specific target types available also.</span></span> 

18. <span data-ttu-id="b6e6e-251">Répétez le processus ci-dessus jusqu'à ce que tous les énoncés ont les entités étiquetées.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-251">Repeat the process above until all the Utterances have the Entities labelled.</span></span> <span data-ttu-id="b6e6e-252">Voir l’image si vous avez besoin d’aide ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-252">See the below image if you need help.</span></span>

    > [!TIP]
    > <span data-ttu-id="b6e6e-253">Lors de la sélection de mots à les étiqueter en tant qu’entités :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-253">When selecting words to label them as entities:</span></span>
    > - <span data-ttu-id="b6e6e-254">Pour les mots isolés cliquez simplement sur eux.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-254">For single words just click them.</span></span>
    > - <span data-ttu-id="b6e6e-255">Pour un ensemble de deux ou plusieurs mots, cliquez sur au début, à la fin de l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-255">For a set of two or more words, click at the beginning and then at the end of the set.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6e6e-256">Vous pouvez utiliser la *jetons vue* bouton bascule pour basculer entre les **entités ou jetons afficherez**!</span><span class="sxs-lookup"><span data-stu-id="b6e6e-256">You can use the *Tokens View* toggle button to switch between **Entities / Tokens View**!</span></span>

19. <span data-ttu-id="b6e6e-257">Les résultats doivent être comme indiqué dans les images ci-dessous, montrant la **entités ou jetons afficherez**:</span><span class="sxs-lookup"><span data-stu-id="b6e6e-257">The results should be as seen in the images below, showing the **Entities / Tokens View**:</span></span>

    ![Jetons et des vues d’entités](images/AzureLabs-Lab3-18.png)
  
20. <span data-ttu-id="b6e6e-259">À ce stade appuyez sur le **Train** bouton dans l’angle supérieur droit de la page et attendez que l’indicateur round petit dessus en vert.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-259">At this point press the **Train** button at the top-right of the page and wait for the small round indicator on it to turn green.</span></span> <span data-ttu-id="b6e6e-260">Cela indique que LUIS a été correctement formé pour reconnaître cette intention.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-260">This indicates that LUIS has been successfully trained to recognize this Intent.</span></span>

    ![Train LUIS](images/AzureLabs-Lab3-19.png)
 
21. <span data-ttu-id="b6e6e-262">En guise d’exercice pour vous, créer une intention de nouveau appelée **ChangeObjectSize**, à l’aide d’entités *cible*, *migrer*, et *réduire*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-262">As an exercise for you, create a new Intent called **ChangeObjectSize**, using the Entities *target*, *upsize*, and *downsize*.</span></span>
22. <span data-ttu-id="b6e6e-263">Suivant le même processus que l’intention précédente, insérez les énoncés suivants huit (8) pour *taille* modifier :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-263">Following the same process as the previous Intent, insert the following eight (8) Utterances for *Size* change:</span></span>

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

23. <span data-ttu-id="b6e6e-264">Le résultat doit être celle présentée dans l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-264">The result should be like the one in the image below:</span></span>

    ![Le programme d’installation les jetons ChangeObjectSize / entités](images/AzureLabs-Lab3-20.png) 

24. <span data-ttu-id="b6e6e-266">Une fois les deux modes, **ChangeObjectColor** et **ChangeObjectSize**, ont été créés et formé, cliquez sur le **publier** situé en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-266">Once both Intents, **ChangeObjectColor** and **ChangeObjectSize**, have been created and trained, click on the **PUBLISH** button on top of the page.</span></span>

    ![Publier le service LUIS](images/AzureLabs-Lab3-21.png)

25. <span data-ttu-id="b6e6e-268">Sur le *publier* page, vous allez finaliser et publier votre application LUIS afin qu’il est accessible par votre code.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-268">On the *Publish* page you will finalize and publish your LUIS App so that it can be accessed by your code.</span></span>

    1. <span data-ttu-id="b6e6e-269">Définir la liste *Publish To* comme **Production**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-269">Set the drop down *Publish To* as **Production**.</span></span>
    2. <span data-ttu-id="b6e6e-270">Définir le *fuseau horaire* sur votre fuseau horaire.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-270">Set the *Timezone* to your time zone.</span></span>
    3. <span data-ttu-id="b6e6e-271">Cochez la case **inclure tous les prédite scores intentions**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-271">Check the box **Include all predicted intent scores**.</span></span>
    4. <span data-ttu-id="b6e6e-272">Cliquez sur **publier à l’emplacement de Production**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-272">Click on **Publish to Production Slot**.</span></span>

        ![Paramètres de publication](images/AzureLabs-Lab3-22.png)

26. <span data-ttu-id="b6e6e-274">Dans la section *ressources et les clés*:</span><span class="sxs-lookup"><span data-stu-id="b6e6e-274">In the section *Resources and Keys*:</span></span>

    1.  <span data-ttu-id="b6e6e-275">Sélectionnez la région que vous définissez pour l’instance de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-275">Select the region you set for service instance in the Azure Portal.</span></span>
    2.  <span data-ttu-id="b6e6e-276">Vous remarquerez une **Starter_Key** élément ci-dessous, ignorez-la.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-276">You will notice a **Starter_Key** element below, ignore it.</span></span>
    3.  <span data-ttu-id="b6e6e-277">Cliquez sur **ajouter une clé** et insérez le *clé* que vous avez obtenue dans le portail Azure lorsque vous avez créé votre instance de Service.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-277">Click on **Add Key** and insert the *Key* that you obtained in the Azure Portal when you created your Service instance.</span></span> <span data-ttu-id="b6e6e-278">Si votre Azure et le portail de LUIS sont connectés au même utilisateur, vous bénéficiez de listes déroulantes pour *nom_client*, *nom de l’abonnement*et le *clé* vous souhaitez utiliser () aura le même nom que vous avez fourni précédemment dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-278">If your Azure and the LUIS portal are logged into the same user, you will be provided drop-down menus for *Tenant name*, *Subscription Name*, and the *Key* you wish to use (will have the same name as you provided previously in the Azure Portal.</span></span>

    > [!IMPORTANT] 
    > <span data-ttu-id="b6e6e-279">En dessous *point de terminaison*, effectuez une copie du point de terminaison correspondant à la clé que vous avez inséré, vous allez bientôt l’utiliser dans votre code.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-279">Underneath *Endpoint*, take a copy of the endpoint corresponding to the Key you have inserted, you will soon use it in your code.</span></span>
 
## <a name="chapter-3--set-up-the-unity-project"></a><span data-ttu-id="b6e6e-280">Chapitre 3 : configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="b6e6e-280">Chapter 3 – Set up the Unity project</span></span>

<span data-ttu-id="b6e6e-281">Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-281">The following is a typical set up for developing with the mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="b6e6e-282">Ouvrez *Unity* et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-282">Open *Unity* and click **New**.</span></span> 

    ![Démarrer un nouveau projet Unity.](images/AzureLabs-Lab3-24.png)

2.  <span data-ttu-id="b6e6e-284">Vous devez maintenant fournir un nom de projet Unity, insérer **MR_LUIS**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-284">You will now need to provide a Unity Project name, insert **MR_LUIS**.</span></span> <span data-ttu-id="b6e6e-285">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-285">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="b6e6e-286">Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-286">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="b6e6e-287">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-287">Then, click **Create project**.</span></span>

    ![Fournissent des détails pour un projet Unity.](images/AzureLabs-Lab3-25.png)
 
3.  <span data-ttu-id="b6e6e-289">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-289">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="b6e6e-290">Allez à modifier > Préférences, puis à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-290">Go to Edit > Preferences and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="b6e6e-291">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-291">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="b6e6e-292">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-292">Close the **Preferences** window.</span></span>

    ![Mettre à jour les préférences de l’éditeur de script.](images/AzureLabs-Lab3-26.png)
 
4.  <span data-ttu-id="b6e6e-294">Ensuite, accédez à **fichier > Paramètres de Build** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **plateforme basculer** bouton.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-294">Next, go to **File > Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

    ![Fenêtre Paramètres, plateforme de commutation à UWP de la génération.](images/AzureLabs-Lab3-27.png)
 
5.  <span data-ttu-id="b6e6e-296">Accédez à **fichier > Paramètres de Build** et vous assurer que :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-296">Go to **File > Build Settings** and make sure that:</span></span>

    1. <span data-ttu-id="b6e6e-297">**Équipement cible** a la valeur **n’importe quel appareil**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-297">**Target Device** is set to **Any Device**</span></span>

        > <span data-ttu-id="b6e6e-298">Pour le Microsoft HoloLens, définissez **appareil cible** à *HoloLens*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-298">For the Microsoft HoloLens, set **Target Device** to *HoloLens*.</span></span>

    2. <span data-ttu-id="b6e6e-299">**Type de build** a la valeur **D3D**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-299">**Build Type** is set to **D3D**</span></span>
    3. <span data-ttu-id="b6e6e-300">**Kit de développement logiciel** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-300">**SDK** is set to **Latest installed**</span></span>
    4. <span data-ttu-id="b6e6e-301">**Version de Visual Studio** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-301">**Visual Studio Version** is set to **Latest installed**</span></span>
    5. <span data-ttu-id="b6e6e-302">**Générez et exécutez** est défini sur **ordinateur Local**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-302">**Build and Run** is set to **Local Machine**</span></span>
    6. <span data-ttu-id="b6e6e-303">Enregistrer la scène et l’ajouter à la build.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-303">Save the scene and add it to the build.</span></span>

        1. <span data-ttu-id="b6e6e-304">Cela en sélectionnant **ajouter un arrière-plan Open**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-304">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="b6e6e-305">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-305">A save window will appear.</span></span>
        
            ![Cliquez sur Ajouter un bouton scènes ouvert](images/AzureLabs-Lab3-28.png)

        2. <span data-ttu-id="b6e6e-307">Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-307">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![Créer un nouveau dossier de scripts](images/AzureLabs-Lab3-29.png)

        3. <span data-ttu-id="b6e6e-309">Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier*: champ de texte, tapez **MR_LuisScene**, puis appuyez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-309">Open your newly created **Scenes** folder, and then in the *File name*: text field, type **MR_LuisScene**, then press **Save**.</span></span>

            ![Donnez un nom à nouvelle scène.](images/AzureLabs-Lab3-30.png)

    7. <span data-ttu-id="b6e6e-311">Les autres paramètres, dans *paramètres de Build*, doit être conservé comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-311">The remaining settings, in *Build Settings*, should be left as default for now.</span></span>

6. <span data-ttu-id="b6e6e-312">Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-312">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span> 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab3-31.png) 
 
7. <span data-ttu-id="b6e6e-314">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-314">In this panel, a few settings need to be verified:</span></span>

    1. <span data-ttu-id="b6e6e-315">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-315">In the **Other Settings** tab:</span></span>

        1. <span data-ttu-id="b6e6e-316">**Version du Runtime de script** doit être **Stable** (équivalent .NET 3.5).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-316">**Scripting Runtime Version** should be **Stable** (.NET 3.5 Equivalent).</span></span>
        2. <span data-ttu-id="b6e6e-317">**Script principal** doit être **.NET**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-317">**Scripting Backend** should be **.NET**</span></span>
        3. <span data-ttu-id="b6e6e-318">**Niveau de compatibilité d’API** doit être **.NET 4.6**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-318">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![Mettre à jour les autres paramètres.](images/AzureLabs-Lab3-32.png)
      
    2. <span data-ttu-id="b6e6e-320">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-320">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        1. <span data-ttu-id="b6e6e-321">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-321">**InternetClient**</span></span>
        2. <span data-ttu-id="b6e6e-322">**Microphone**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-322">**Microphone**</span></span>

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab3-33.png)

    3. <span data-ttu-id="b6e6e-324">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-324">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Mettre à jour les paramètres de R X.](images/AzureLabs-Lab3-34.png)

8.  <span data-ttu-id="b6e6e-326">Dans *paramètres de Build* _Unity C#_  projets est n’est plus grisée ; Cochez la case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-326">Back in *Build Settings* _Unity C#_ Projects is no longer greyed out; tick the checkbox next to this.</span></span> 
9.  <span data-ttu-id="b6e6e-327">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-327">Close the Build Settings window.</span></span>
10. <span data-ttu-id="b6e6e-328">Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-328">Save your Scene and Project (**FILE > SAVE SCENE / FILE > SAVE PROJECT**).</span></span>

## <a name="chapter-4--create-the-scene"></a><span data-ttu-id="b6e6e-329">Chapitre 4 : créer la scène</span><span class="sxs-lookup"><span data-stu-id="b6e6e-329">Chapter 4 – Create the scene</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6e6e-330">Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20303%20-%20Natural%20language%20understanding/Azure-MR-303.unitypackage), importez-le dans votre projet comme un [Package personnalisé ](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 5](#chapter-5--create-the-microphonemanager-class).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-330">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to download this [.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20303%20-%20Natural%20language%20understanding/Azure-MR-303.unitypackage), import it into your project as a [Custom Package](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 5](#chapter-5--create-the-microphonemanager-class).</span></span> 

1.  <span data-ttu-id="b6e6e-331">Avec le bouton droit dans une zone vide de la *hiérarchie panneau*, sous **objet 3D**, ajoutez un **plan**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-331">Right-click in an empty area of the *Hierarchy Panel*, under **3D Object**, add a **Plane**.</span></span>

    ![Créer un plan.](images/AzureLabs-Lab3-35.png)

2.  <span data-ttu-id="b6e6e-333">N’oubliez pas que lorsque vous cliquez sur dans le *hiérarchie* à nouveau pour créer des objets de plus, si vous avez toujours le dernier objet sélectionné, l’objet sélectionné sera le parent de votre nouvel objet.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-333">Be aware that when you right-click within the *Hierarchy* again to create more objects, if you still have the last object selected, the selected object will be the parent of your new object.</span></span> <span data-ttu-id="b6e6e-334">Éviter ce problème clic gauche dans un espace vide dans la hiérarchie et puis effectuant un clic droit.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-334">Avoid this left-clicking in an empty space within the Hierarchy, and then right-clicking.</span></span>

3.  <span data-ttu-id="b6e6e-335">Répétez la procédure ci-dessus pour ajouter les objets suivants :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-335">Repeat the above procedure to add the following objects:</span></span>

    1. <span data-ttu-id="b6e6e-336">*Sphere*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-336">*Sphere*</span></span>
    2. <span data-ttu-id="b6e6e-337">*Cylindre*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-337">*Cylinder*</span></span>
    3. <span data-ttu-id="b6e6e-338">*Cube*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-338">*Cube*</span></span>
    4. <span data-ttu-id="b6e6e-339">*Texte 3D*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-339">*3D Text*</span></span>

4.  <span data-ttu-id="b6e6e-340">La scène qui en résulte *hiérarchie* doit être semblable à celui de l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-340">The resulting scene *Hierarchy* should be like the one in the image below:</span></span>

    ![Paramètres de hiérarchie de scène.](images/AzureLabs-Lab3-36.png)
 
5.  <span data-ttu-id="b6e6e-342">Cliquez sur le **Main Camera** pour le sélectionner, examinez le *panneau Inspecteur* vous verrez l’objet caméra avec toutes le ses composants.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-342">Left click on the **Main Camera** to select it, look at the *Inspector Panel* you will see the Camera object with all the its components.</span></span>
6.  <span data-ttu-id="b6e6e-343">Cliquez sur le **ajouter un composant** bouton situé tout en bas de la *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-343">Click on the **Add Component** button located at the very bottom of the *Inspector Panel*.</span></span>

    ![Ajouter une Source Audio](images/AzureLabs-Lab3-37.png)
 
7.  <span data-ttu-id="b6e6e-345">Recherchez le composant appelé *Audio Source*, comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-345">Search for the component called *Audio Source*, as shown above.</span></span>
8.  <span data-ttu-id="b6e6e-346">Assurez-vous également que le *transformer* composant de la caméra principale est (0,0,0), cela est possible en appuyant sur la **ENGRENAGE** icône en regard de la caméra *transformer* composant et en sélectionnant **réinitialiser**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-346">Also make sure that the *Transform* component of the Main Camera is set to (0,0,0), this can be done by pressing the **Gear** icon next to the Camera’s *Transform* component and selecting **Reset**.</span></span> <span data-ttu-id="b6e6e-347">Le *transformer* composant doit alors ressembler :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-347">The *Transform* component should then look like:</span></span>

    1.  <span data-ttu-id="b6e6e-348">*Position* a la valeur **0, 0, 0**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-348">*Position* is set to **0, 0, 0**.</span></span>
    2.  <span data-ttu-id="b6e6e-349">*Rotation* a la valeur **0, 0, 0**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-349">*Rotation* is set to **0, 0, 0**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b6e6e-350">Pour le Microsoft HoloLens, vous devez également modifier les paramètres suivants, qui font partie de la **caméra** composant, qui se trouve sur votre **Main Camera**:</span><span class="sxs-lookup"><span data-stu-id="b6e6e-350">For the Microsoft HoloLens, you will need to also change the following, which are part of the **Camera** component, which is on your **Main Camera**:</span></span>
    > - <span data-ttu-id="b6e6e-351">**Effacer les indicateurs :** Couleur unie.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-351">**Clear Flags:** Solid Color.</span></span>
    > - <span data-ttu-id="b6e6e-352">**Arrière-plan** ' noir, Alpha 0' – couleur hexadécimale : #00000000.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-352">**Background** ‘Black, Alpha 0’ – Hex color: #00000000.</span></span>

9.  <span data-ttu-id="b6e6e-353">Cliquez sur le **plan** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-353">Left click on the **Plane** to select it.</span></span> <span data-ttu-id="b6e6e-354">Dans le *panneau Inspecteur* définir le *transformer* composant avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-354">In the *Inspector Panel* set the *Transform* component with the following values:</span></span>

    |       | <span data-ttu-id="b6e6e-355">Transformer - *Position*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-355">Transform - *Position*</span></span> |       |
    |:-----:|:----------------------:|:-----:|
    | <span data-ttu-id="b6e6e-356">**X**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-356">**X**</span></span> | <span data-ttu-id="b6e6e-357">**Y**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-357">**Y**</span></span>                  | <span data-ttu-id="b6e6e-358">**Z**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-358">**Z**</span></span> |
    | <span data-ttu-id="b6e6e-359">0</span><span class="sxs-lookup"><span data-stu-id="b6e6e-359">0</span></span>     | <span data-ttu-id="b6e6e-360">-1</span><span class="sxs-lookup"><span data-stu-id="b6e6e-360">-1</span></span>                     | <span data-ttu-id="b6e6e-361">0</span><span class="sxs-lookup"><span data-stu-id="b6e6e-361">0</span></span>     |


10. <span data-ttu-id="b6e6e-362">Cliquez sur le **sphère** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-362">Left click on the **Sphere** to select it.</span></span> <span data-ttu-id="b6e6e-363">Dans le *panneau Inspecteur* définir le *transformer* composant avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-363">In the *Inspector Panel* set the *Transform* component with the following values:</span></span>

    |       | <span data-ttu-id="b6e6e-364">Transformer - *Position*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-364">Transform - *Position*</span></span> |       |
    |:-----:|:----------------------:|:-----:|
    | <span data-ttu-id="b6e6e-365">**X**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-365">**X**</span></span> | <span data-ttu-id="b6e6e-366">**Y**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-366">**Y**</span></span>                  | <span data-ttu-id="b6e6e-367">**Z**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-367">**Z**</span></span> |
    | <span data-ttu-id="b6e6e-368">2</span><span class="sxs-lookup"><span data-stu-id="b6e6e-368">2</span></span>     | <span data-ttu-id="b6e6e-369">1</span><span class="sxs-lookup"><span data-stu-id="b6e6e-369">1</span></span>                      | <span data-ttu-id="b6e6e-370">2</span><span class="sxs-lookup"><span data-stu-id="b6e6e-370">2</span></span>     |

11. <span data-ttu-id="b6e6e-371">Cliquez sur le **cylindre** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-371">Left click on the **Cylinder** to select it.</span></span> <span data-ttu-id="b6e6e-372">Dans le *panneau Inspecteur* définir le *transformer* composant avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-372">In the *Inspector Panel* set the *Transform* component with the following values:</span></span>

    |       | <span data-ttu-id="b6e6e-373">Transformer - *Position*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-373">Transform - *Position*</span></span> |       |
    |:-----:|:----------------------:|:-----:|
    | <span data-ttu-id="b6e6e-374">**X**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-374">**X**</span></span> | <span data-ttu-id="b6e6e-375">**Y**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-375">**Y**</span></span>                  | <span data-ttu-id="b6e6e-376">**Z**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-376">**Z**</span></span> |
    | <span data-ttu-id="b6e6e-377">-2</span><span class="sxs-lookup"><span data-stu-id="b6e6e-377">-2</span></span>    | <span data-ttu-id="b6e6e-378">1</span><span class="sxs-lookup"><span data-stu-id="b6e6e-378">1</span></span>                      | <span data-ttu-id="b6e6e-379">2</span><span class="sxs-lookup"><span data-stu-id="b6e6e-379">2</span></span>     |

12. <span data-ttu-id="b6e6e-380">Cliquez sur le **Cube** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-380">Left click on the **Cube** to select it.</span></span> <span data-ttu-id="b6e6e-381">Dans le *panneau Inspecteur* définir le *transformer* composant avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-381">In the *Inspector Panel* set the *Transform* component with the following values:</span></span>

    |        | <span data-ttu-id="b6e6e-382">Transformer - *Position*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-382">Transform - *Position*</span></span> |       |  \| |       | <span data-ttu-id="b6e6e-383">Transformer - *Rotation*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-383">Transform - *Rotation*</span></span> |       |
    |:------:|:----------------------:|:-----:|:---:|:-----:|:----------------------:|:-----:|
    | <span data-ttu-id="b6e6e-384">**X**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-384">**X**</span></span> | <span data-ttu-id="b6e6e-385">**Y**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-385">**Y**</span></span>                   | <span data-ttu-id="b6e6e-386">**Z**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-386">**Z**</span></span> |  \| | <span data-ttu-id="b6e6e-387">**X**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-387">**X**</span></span> | <span data-ttu-id="b6e6e-388">**Y**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-388">**Y**</span></span>                  | <span data-ttu-id="b6e6e-389">**Z**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-389">**Z**</span></span> |
    | <span data-ttu-id="b6e6e-390">0</span><span class="sxs-lookup"><span data-stu-id="b6e6e-390">0</span></span>     | <span data-ttu-id="b6e6e-391">1</span><span class="sxs-lookup"><span data-stu-id="b6e6e-391">1</span></span>                       | <span data-ttu-id="b6e6e-392">4</span><span class="sxs-lookup"><span data-stu-id="b6e6e-392">4</span></span>     |  \| | <span data-ttu-id="b6e6e-393">45</span><span class="sxs-lookup"><span data-stu-id="b6e6e-393">45</span></span>    | <span data-ttu-id="b6e6e-394">45</span><span class="sxs-lookup"><span data-stu-id="b6e6e-394">45</span></span>                     | <span data-ttu-id="b6e6e-395">0</span><span class="sxs-lookup"><span data-stu-id="b6e6e-395">0</span></span>     | 

13. <span data-ttu-id="b6e6e-396">Cliquez sur le **nouveau texte** objet pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-396">Left click on the **New Text** object to select it.</span></span> <span data-ttu-id="b6e6e-397">Dans le *panneau Inspecteur* définir le *transformer* composant avec les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-397">In the *Inspector Panel* set the *Transform* component with the following values:</span></span>

    |       | <span data-ttu-id="b6e6e-398">Transformer - *Position*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-398">Transform - *Position*</span></span> |       |  \| |       | <span data-ttu-id="b6e6e-399">Transformer - *mise à l’échelle*</span><span class="sxs-lookup"><span data-stu-id="b6e6e-399">Transform - *Scale*</span></span> |       |
    |:-----:|:----------------------:|:-----:|:---:|:-----:|:-------------------:|:-----:|
    | <span data-ttu-id="b6e6e-400">**X**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-400">**X**</span></span> | <span data-ttu-id="b6e6e-401">**Y**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-401">**Y**</span></span>                  | <span data-ttu-id="b6e6e-402">**Z**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-402">**Z**</span></span> |  \| | <span data-ttu-id="b6e6e-403">**X**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-403">**X**</span></span> | <span data-ttu-id="b6e6e-404">**Y**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-404">**Y**</span></span>               | <span data-ttu-id="b6e6e-405">**Z**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-405">**Z**</span></span> |
    | <span data-ttu-id="b6e6e-406">-2</span><span class="sxs-lookup"><span data-stu-id="b6e6e-406">-2</span></span>    | <span data-ttu-id="b6e6e-407">6</span><span class="sxs-lookup"><span data-stu-id="b6e6e-407">6</span></span>                      | <span data-ttu-id="b6e6e-408">9</span><span class="sxs-lookup"><span data-stu-id="b6e6e-408">9</span></span>     |  \| | <span data-ttu-id="b6e6e-409">0.1</span><span class="sxs-lookup"><span data-stu-id="b6e6e-409">0.1</span></span>   | <span data-ttu-id="b6e6e-410">0.1</span><span class="sxs-lookup"><span data-stu-id="b6e6e-410">0.1</span></span>                 | <span data-ttu-id="b6e6e-411">0.1</span><span class="sxs-lookup"><span data-stu-id="b6e6e-411">0.1</span></span>   | 

14. <span data-ttu-id="b6e6e-412">Modification **la taille de police** dans le **texte Mesh** à **50**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-412">Change **Font Size** in the **Text Mesh** component to **50**.</span></span>
15. <span data-ttu-id="b6e6e-413">Modifier le *nom* de la **maillage de texte** objet **dictée texte**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-413">Change the *name* of the **Text Mesh** object to **Dictation Text**.</span></span>

    ![Création d’objet de texte 3D](images/AzureLabs-Lab3-38.png)
 
16. <span data-ttu-id="b6e6e-415">Votre structure de hiérarchie le panneau de configuration doit maintenant ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-415">Your Hierarchy Panel structure should now look like this:</span></span>

    ![texte de maillage dans la vue de la scène](images/AzureLabs-Lab3-38b.png)


17. <span data-ttu-id="b6e6e-417">La scène finale doit ressembler à l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-417">The final scene should look like the image below:</span></span>

    ![La vue de la scène.](images/AzureLabs-Lab3-39.png)
    
 
## <a name="chapter-5--create-the-microphonemanager-class"></a><span data-ttu-id="b6e6e-419">Chapitre 5 : créer la classe MicrophoneManager</span><span class="sxs-lookup"><span data-stu-id="b6e6e-419">Chapter 5 – Create the MicrophoneManager class</span></span>

<span data-ttu-id="b6e6e-420">Le premier Script que vous vous apprêtez à créer est le *MicrophoneManager* classe.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-420">The first Script you are going to create is the *MicrophoneManager* class.</span></span> <span data-ttu-id="b6e6e-421">Après cela, vous allez créer le *LuisManager*, le *comportements* (classe) et enfin la *les regards* classe (vous pouvez créer tous ces maintenant, bien que sera traité en tant que vous atteindre chaque chapitre).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-421">Following this, you will create the *LuisManager*, the *Behaviours* class, and lastly the *Gaze* class (feel free to create all these now, though it will be covered as you reach each Chapter).</span></span>

<span data-ttu-id="b6e6e-422">Le *MicrophoneManager* classe est chargée de :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-422">The *MicrophoneManager* class is responsible for:</span></span>

-   <span data-ttu-id="b6e6e-423">Détection du périphérique d’enregistrement attaché à l’ordinateur (selon celui qui est celle par défaut) ou un casque.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-423">Detecting the recording device attached to the headset or machine (whichever is the default one).</span></span>
-   <span data-ttu-id="b6e6e-424">Capturer l’audio (voix) et la dictée pour stocker en tant que chaîne.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-424">Capture the audio (voice) and use dictation to store it as a string.</span></span>
-   <span data-ttu-id="b6e6e-425">Une fois que la voix a été suspendu, soumettez la dictée pour le *LuisManager* classe.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-425">Once the voice has paused, submit the dictation to the *LuisManager* class.</span></span> 

<span data-ttu-id="b6e6e-426">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-426">To create this class:</span></span> 

1.  <span data-ttu-id="b6e6e-427">Avec le bouton droit dans le *Panneau de configuration de projet*, **créer > dossier**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-427">Right-click in the *Project Panel*, **Create > Folder**.</span></span> <span data-ttu-id="b6e6e-428">Appelez le dossier **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-428">Call the folder **Scripts**.</span></span> 

    ![Créez le dossier Scripts.](images/AzureLabs-Lab3-40.png)
 
2.  <span data-ttu-id="b6e6e-430">Avec le **Scripts** dossier créé, double-cliquez dessus, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-430">With the **Scripts** folder created, double click it, to open.</span></span> <span data-ttu-id="b6e6e-431">Ensuite, dans ce dossier, avec le bouton droit, **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-431">Then, within that folder, right-click, **Create > C# Script**.</span></span> <span data-ttu-id="b6e6e-432">Nommez le script *MicrophoneManager*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-432">Name the script *MicrophoneManager*.</span></span> 

3.  <span data-ttu-id="b6e6e-433">Double-cliquez sur *MicrophoneManager* pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-433">Double click on *MicrophoneManager* to open it with *Visual Studio*.</span></span>
4.  <span data-ttu-id="b6e6e-434">Ajoutez les espaces de noms suivantes au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-434">Add the following namespaces to the top of the file:</span></span>

    ```csharp
        using UnityEngine;
        using UnityEngine.Windows.Speech;
    ```

5.  <span data-ttu-id="b6e6e-435">Puis ajoutez les variables suivantes à l’intérieur de la *MicrophoneManager* classe :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-435">Then add the following variables inside the *MicrophoneManager* class:</span></span>

    ```csharp
        public static MicrophoneManager instance; //help to access instance of this object
        private DictationRecognizer dictationRecognizer;  //Component converting speech to text
        public TextMesh dictationText; //a UI object used to debug dictation result
    ``` 

6.  <span data-ttu-id="b6e6e-436">Code pour *Awake()* et *Start()* méthodes doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-436">Code for *Awake()* and *Start()* methods now needs to be added.</span></span> <span data-ttu-id="b6e6e-437">Il seront appelées lors de l’initialisation de la classe :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-437">These will be called when the class initializes:</span></span>

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
 
7.  <span data-ttu-id="b6e6e-438">Maintenant, vous devez la méthode utilisée par l’application à démarrer et arrêter la capture de la voix et transmettez-le à la *LuisManager* (classe), que vous allez générer plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-438">Now you need the method that the App uses to start and stop the voice capture, and pass it to the *LuisManager* class, that you will build soon.</span></span> 

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

8.  <span data-ttu-id="b6e6e-439">Ajouter un *dictée gestionnaire* qui sera appelé lorsque la voix est maintenu.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-439">Add a *Dictation Handler* that will be invoked when the voice pauses.</span></span> <span data-ttu-id="b6e6e-440">Cette méthode passe le texte de dictée à la *LuisManager* classe.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-440">This method will pass the dictation text to the *LuisManager* class.</span></span>

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
    > <span data-ttu-id="b6e6e-441">Supprimer le *Update()* étant donné que cette classe ne l’utilise pas de méthode.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-441">Delete the *Update()* method since this class will not use it.</span></span>

9.  <span data-ttu-id="b6e6e-442">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-442">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b6e6e-443">À ce stade, vous remarquerez une erreur qui apparaissent dans le *volet de Console Unity Editor*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-443">At this point you will notice an error appearing in the *Unity Editor Console Panel*.</span></span> <span data-ttu-id="b6e6e-444">Il s’agit, car le code fait référence le *LuisManager* classe que vous allez créer dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-444">This is because the code references the *LuisManager* class which you will create in the next Chapter.</span></span>

## <a name="chapter-6--create-the-luismanager-class"></a><span data-ttu-id="b6e6e-445">Chapitre 6 : créer la classe LUISManager</span><span class="sxs-lookup"><span data-stu-id="b6e6e-445">Chapter 6 – Create the LUISManager class</span></span>

<span data-ttu-id="b6e6e-446">Il est temps de créer le *LuisManager* (classe), ce qui rend l’appel au service Azure LUIS.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-446">It is time for you to create the *LuisManager* class, which will make the call to the Azure LUIS service.</span></span> 

<span data-ttu-id="b6e6e-447">L’objectif de cette classe consiste à recevoir le texte de dictée à partir de la *MicrophoneManager* classe et l’envoyer à la *API Azure Language Understanding* à analyser.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-447">The purpose of this class is to receive the dictation text from the *MicrophoneManager* class and send it to the *Azure Language Understanding API* to be analyzed.</span></span>

<span data-ttu-id="b6e6e-448">Cette classe désérialisera le *JSON* réponse et appeler les méthodes appropriées de la *comportements* classe pour déclencher une action.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-448">This class will deserialize the *JSON* response and call the appropriate methods of the *Behaviours* class to trigger an action.</span></span>

<span data-ttu-id="b6e6e-449">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-449">To create this class:</span></span> 

1.  <span data-ttu-id="b6e6e-450">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-450">Double click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="b6e6e-451">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-451">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="b6e6e-452">Nommez le script *LuisManager*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-452">Name the script *LuisManager*.</span></span> 
3.  <span data-ttu-id="b6e6e-453">Double-cliquez sur le script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-453">Double click on the script to open it with Visual Studio.</span></span>
4.  <span data-ttu-id="b6e6e-454">Ajoutez les espaces de noms suivantes au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-454">Add the following namespaces to the top of the file:</span></span>

    ```csharp
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using System.IO;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

5.  <span data-ttu-id="b6e6e-455">Vous allez commencer par créer trois classes **à l’intérieur** le *LuisManager* classe (dans le même fichier de script, au-dessus de la *Start()* méthode) qui représentera désérialisé Réponse JSON à partir d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-455">You will begin by creating three classes **inside** the *LuisManager* class (within the same script file, above the *Start()* method) that will represent the deserialized JSON response from Azure.</span></span>

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

6.  <span data-ttu-id="b6e6e-456">Ensuite, ajoutez les variables suivantes à l’intérieur de la *LuisManager* classe :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-456">Next, add the following variables inside the *LuisManager* class:</span></span>
 
    ```csharp
        public static LuisManager instance;

        //Substitute the value of luis Endpoint with your own End Point
        string luisEndpoint = "https://westus.api.cognitive... add your endpoint from the Luis Portal";
    ```

7.  <span data-ttu-id="b6e6e-457">Veillez à placer votre point de terminaison LUIS maintenant (ce qui vous aurez à partir de votre portail LUIS).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-457">Make sure to place your LUIS endpoint in now (which you will have from your LUIS portal).</span></span>

8.  <span data-ttu-id="b6e6e-458">Code pour le *Awake()* méthode doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-458">Code for the *Awake()* method now needs to be added.</span></span> <span data-ttu-id="b6e6e-459">Cette méthode est appelée lors de l’initialisation de la classe :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-459">This method will be called when the class initializes:</span></span>

    ```csharp
        private void Awake()
        {
            // allows this class instance to behave like a singleton
            instance = this;
        }
    ```

9.  <span data-ttu-id="b6e6e-460">Maintenant, vous devez les méthodes de cette application utilise pour envoyer la dictée reçue à partir de la *MicrophoneManager* classe *LUIS*, puis recevoir et désérialiser la réponse.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-460">Now you need the methods this application uses to send the dictation received from the *MicrophoneManager* class to *LUIS*, and then receive and deserialize the response.</span></span> 
10. <span data-ttu-id="b6e6e-461">Une fois que la valeur de l’objectif et les entités associées, ont été déterminées, ils sont passés à l’instance de la *comportements* classe déclenche l’action prévue.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-461">Once the value of the Intent, and associated Entities, have been determined, they are passed to the instance of the *Behaviours* class to trigger the intended action.</span></span>

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
 
11. <span data-ttu-id="b6e6e-462">Créer une nouvelle méthode appelée *AnalyseResponseElements()* qui lira résultant *AnalysedQuery* et déterminer les entités.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-462">Create a new method called *AnalyseResponseElements()* that will read the resulting *AnalysedQuery* and determine the Entities.</span></span> <span data-ttu-id="b6e6e-463">Une fois que ces entités sont déterminées, ils seront passés à l’instance de la *comportements* classe à utiliser dans les actions.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-463">Once those Entities are determined, they will be passed to the instance of the *Behaviours* class to use in the actions.</span></span>

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

            // Depending on the topmost recognised intent, read the entities name
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
    > <span data-ttu-id="b6e6e-464">Supprimer le *Start()* et *Update()* méthodes étant donné que cette classe ne les utiliserez pas.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-464">Delete the *Start()* and *Update()* methods since this class will not use them.</span></span>

12. <span data-ttu-id="b6e6e-465">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-465">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

> [!NOTE]
> <span data-ttu-id="b6e6e-466">À ce stade, vous remarquerez plusieurs erreurs survenues dans le *volet de Console Unity Editor*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-466">At this point you will notice several errors appearing in the *Unity Editor Console Panel*.</span></span> <span data-ttu-id="b6e6e-467">Il s’agit, car le code fait référence le *comportements* classe que vous allez créer dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-467">This is because the code references the *Behaviours* class which you will create in the next Chapter.</span></span>

## <a name="chapter-7--create-the-behaviours-class"></a><span data-ttu-id="b6e6e-468">Chapitre 7 – créer la classe de comportements</span><span class="sxs-lookup"><span data-stu-id="b6e6e-468">Chapter 7 – Create the Behaviours class</span></span>

<span data-ttu-id="b6e6e-469">Le *comportements* classe déclenche les actions à l’aide d’entités fournies par le *LuisManager* classe.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-469">The *Behaviours* class will trigger the actions using the Entities provided by the *LuisManager* class.</span></span>

<span data-ttu-id="b6e6e-470">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-470">To create this class:</span></span> 

1.  <span data-ttu-id="b6e6e-471">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-471">Double click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="b6e6e-472">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-472">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="b6e6e-473">Nommez le script *comportements*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-473">Name the script *Behaviours*.</span></span> 
3.  <span data-ttu-id="b6e6e-474">Double-cliquez sur le script pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-474">Double click on the script to open it with *Visual Studio*.</span></span>
4.  <span data-ttu-id="b6e6e-475">Puis ajoutez les variables suivantes à l’intérieur de la *comportements* classe :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-475">Then add the following variables inside the *Behaviours* class:</span></span>

    ```csharp
        public static Behaviours instance;

        // the following variables are references to possible targets
        public GameObject sphere;
        public GameObject cylinder;
        public GameObject cube;
        internal GameObject gazedTarget;
    ```
 
5.  <span data-ttu-id="b6e6e-476">Ajouter le *Awake()* code de la méthode.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-476">Add the *Awake()* method code.</span></span> <span data-ttu-id="b6e6e-477">Cette méthode est appelée lors de l’initialisation de la classe :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-477">This method will be called when the class initializes:</span></span>

    ```csharp
        void Awake()
        {
            // allows this class instance to behave like a singleton
            instance = this;
        }
    ```
 
6.  <span data-ttu-id="b6e6e-478">Les méthodes suivantes sont appelées par le *LuisManager* classe (que vous avez créé précédemment) pour déterminer quel objet est la cible de la requête, puis déclencher l’action appropriée.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-478">The following methods are called by the *LuisManager* class (which you have created previously) to determine which object is the target of the query and then trigger the appropriate action.</span></span>

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
 
7.  <span data-ttu-id="b6e6e-479">Ajouter le *FindTarget()* méthode pour déterminer quels de la *GameObjects* est la cible de l’objectif actuel.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-479">Add the *FindTarget()* method to determine which of the *GameObjects* is the target of the current Intent.</span></span> <span data-ttu-id="b6e6e-480">Cette méthode par défaut est la cible pour le *GameObject* en cours « gazed » si aucune cible explicite n’est définie dans les entités.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-480">This method defaults the target to the *GameObject* being “gazed” if no explicit target is defined in the Entities.</span></span>

    ```csharp
        /// <summary>
        /// Determines which obejct reference is the target GameObject by providing its name
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
    > <span data-ttu-id="b6e6e-481">Supprimer le *Start()* et *Update()* méthodes étant donné que cette classe ne les utiliserez pas.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-481">Delete the *Start()* and *Update()* methods since this class will not use them.</span></span>

8.  <span data-ttu-id="b6e6e-482">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-482">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-8--create-the-gaze-class"></a><span data-ttu-id="b6e6e-483">Chapitre 8 : créer la classe du pointage de regard</span><span class="sxs-lookup"><span data-stu-id="b6e6e-483">Chapter 8 – Create the Gaze Class</span></span>

<span data-ttu-id="b6e6e-484">La dernière classe dont vous aurez besoin pour terminer cette application est la *les regards* classe.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-484">The last class that you will need to complete this app is the *Gaze* class.</span></span> <span data-ttu-id="b6e6e-485">Cette classe met à jour la référence à la *GameObject* actuellement de focus visuels de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-485">This class updates the reference to the *GameObject* currently in the user’s visual focus.</span></span>

<span data-ttu-id="b6e6e-486">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-486">To create this Class:</span></span> 

1.  <span data-ttu-id="b6e6e-487">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-487">Double click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="b6e6e-488">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-488">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="b6e6e-489">Nommez le script *les regards*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-489">Name the script *Gaze*.</span></span> 
3.  <span data-ttu-id="b6e6e-490">Double-cliquez sur le script pour l’ouvrir avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-490">Double click on the script to open it with *Visual Studio*.</span></span>
4.  <span data-ttu-id="b6e6e-491">Insérez le code suivant pour cette classe :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-491">Insert the following code for this class:</span></span>

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
 
5.  <span data-ttu-id="b6e6e-492">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-492">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-9--completing-the-scene-setup"></a><span data-ttu-id="b6e6e-493">Chapitre 9 – fin de l’installation de la scène</span><span class="sxs-lookup"><span data-stu-id="b6e6e-493">Chapter 9 – Completing the scene setup</span></span>

1.  <span data-ttu-id="b6e6e-494">Pour terminer l’installation de la scène, faites glisser chaque script que vous avez créé à partir du dossier Scripts à la **Main Camera** de l’objet dans le *hiérarchie panneau*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-494">To complete the setup of the scene, drag each script that you have created from the Scripts Folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span>
2.  <span data-ttu-id="b6e6e-495">Sélectionnez le **Main Camera** et examinez le *panneau Inspecteur*, vous devez être en mesure de voir chaque script que vous avez associée, et vous remarquerez qu’il existe des paramètres qui doivent encore être définies sur chaque script.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-495">Select the **Main Camera** and look at the *Inspector Panel*, you should be able to see each script that you have attached, and you will notice that there are parameters on each script that are yet to be set.</span></span>

    ![La définition des cibles de référence de la caméra.](images/AzureLabs-Lab3-41.png)

3.  <span data-ttu-id="b6e6e-497">Pour définir correctement ces paramètres, suivez ces instructions :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-497">To set these parameters correctly, follow these instructions:</span></span>

    1. <span data-ttu-id="b6e6e-498">*MicrophoneManager*:</span><span class="sxs-lookup"><span data-stu-id="b6e6e-498">*MicrophoneManager*:</span></span>

        - <span data-ttu-id="b6e6e-499">À partir de la *hiérarchie panneau*, faites glisser le **dictée texte** de l’objet dans le **dictée texte** boîte valeur du paramètre.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-499">From the *Hierarchy Panel*, drag the **Dictation Text** object into the **Dictation Text** parameter value box.</span></span>

    2. <span data-ttu-id="b6e6e-500">*Comportements*, à partir de la *hiérarchie panneau*:</span><span class="sxs-lookup"><span data-stu-id="b6e6e-500">*Behaviours*, from the *Hierarchy Panel*:</span></span>

        - <span data-ttu-id="b6e6e-501">Faites glisser le **sphère** de l’objet dans le *sphère* zone cible de référence.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-501">Drag the **Sphere** object into the *Sphere* reference target box.</span></span>
        - <span data-ttu-id="b6e6e-502">Faites glisser le **cylindre** dans le *cylindre* zone cible de référence.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-502">Drag the **Cylinder** into the *Cylinder* reference target box.</span></span>
        - <span data-ttu-id="b6e6e-503">Faites glisser le **Cube** dans le *Cube* zone cible de référence.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-503">Drag the **Cube** into the *Cube* reference target box.</span></span>

    3. <span data-ttu-id="b6e6e-504">*Utilisation*:</span><span class="sxs-lookup"><span data-stu-id="b6e6e-504">*Gaze*:</span></span>

        - <span data-ttu-id="b6e6e-505">Définir le *les regards de Distance de Max* à **300** (s’il n’est pas déjà).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-505">Set the *Gaze Max Distance* to **300** (if it is not already).</span></span> 

4.  <span data-ttu-id="b6e6e-506">Le résultat doit ressembler à l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-506">The result should look like the image below:</span></span>

    ![Afficher les cibles de référence de caméra, maintenant définir.](images/AzureLabs-Lab3-42.png)
 
## <a name="chapter-10--test-in-the-unity-editor"></a><span data-ttu-id="b6e6e-508">Chapitre 10 – Test dans l’éditeur Unity</span><span class="sxs-lookup"><span data-stu-id="b6e6e-508">Chapter 10 – Test in the Unity Editor</span></span>

<span data-ttu-id="b6e6e-509">Vérifiez que le programme d’installation de la scène est correctement implémentée.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-509">Test that the Scene setup is properly implemented.</span></span>

<span data-ttu-id="b6e6e-510">Vérifiez que :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-510">Ensure that:</span></span>

-   <span data-ttu-id="b6e6e-511">Tous les scripts sont attachés à la **Main Camera** objet.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-511">All the scripts are attached to the **Main Camera** object.</span></span> 
-   <span data-ttu-id="b6e6e-512">Tous les champs dans le *panneau Inspecteur de caméra principal* sont affectées correctement.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-512">All the fields in the *Main Camera Inspector Panel* are assigned properly.</span></span>

1.  <span data-ttu-id="b6e6e-513">Appuyez sur la **lire** situé dans le *éditeur Unity*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-513">Press the **Play** button in the *Unity Editor*.</span></span> <span data-ttu-id="b6e6e-514">L’application doit s’exécuter dans le casque immersif attaché.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-514">The App should be running within the attached immersive headset.</span></span>

2.  <span data-ttu-id="b6e6e-515">Essayer quelques énoncés, telles que :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-515">Try a few utterances, such as:</span></span>

    ```
    make the cylinder red

    change the cube to yellow

    I want the sphere blue

    make this to green

    change it to white
    ```

    > [!NOTE]
    > <span data-ttu-id="b6e6e-516">Si vous voyez une erreur dans la console Unity sur le périphérique audio par défaut modification, la scène peut ne pas fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-516">If you see an error in the Unity console about the default audio device changing, the scene may not function as expected.</span></span> <span data-ttu-id="b6e6e-517">Cela est dû au mode que microphones intégrés pour les casques qui en sont munis porte sur le portail de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-517">This is due to the way the mixed reality portal deals with built-in microphones for headsets that have them.</span></span> <span data-ttu-id="b6e6e-518">Si vous cette erreur se produit, simplement arrêtez la scène et démarrez à nouveau et les choses peuvent fonctionner comme prévu.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-518">If you see this error, simply stop the scene and start it again and things should work as expected.</span></span>

## <a name="chapter-11--build-and-sideload-the-uwp-solution"></a><span data-ttu-id="b6e6e-519">Chapitre 11 – Build et chargement indépendant de la Solution UWP</span><span class="sxs-lookup"><span data-stu-id="b6e6e-519">Chapter 11 – Build and sideload the UWP Solution</span></span>

<span data-ttu-id="b6e6e-520">Une fois que vous vous assurez que l’application fonctionne dans l’éditeur Unity, vous êtes prêt à générer et déployer.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-520">Once you have ensured that the application is working in the Unity Editor, you are ready to Build and Deploy.</span></span>

<span data-ttu-id="b6e6e-521">Pour générer :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-521">To Build:</span></span>

1.  <span data-ttu-id="b6e6e-522">Enregistrer la scène actuelle en cliquant sur **fichier > Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-522">Save the current scene by clicking on **File > Save**.</span></span>
2.  <span data-ttu-id="b6e6e-523">Accédez à **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-523">Go to **File > Build Settings**.</span></span>
3.  <span data-ttu-id="b6e6e-524">Cochez la case appelée **Unity C# projets** (utile pour visualiser et de débogage de votre code une fois que le projet UWP est créé.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-524">Tick the box called **Unity C# Projects** (useful for seeing and debugging your code once the UWP project is created.</span></span>
4.  <span data-ttu-id="b6e6e-525">Cliquez sur **ajouter un arrière-plan Open**, puis cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-525">Click on **Add Open Scenes**, then click **Build**.</span></span>

    ![Fenêtre de paramètres de build](images/AzureLabs-Lab3-43.png)

4.  <span data-ttu-id="b6e6e-527">Vous êtes invité à sélectionner le dossier dans lequel vous souhaitez générer la Solution.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-527">You will be prompted to select the folder where you want to build the Solution.</span></span> 

5.  <span data-ttu-id="b6e6e-528">Créer un *génère* dossier et dans ce dossier, créez un autre dossier avec un nom approprié de votre choix.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-528">Create a *BUILDS* folder and within that folder create another folder with an appropriate name of your choice.</span></span> 
6.  <span data-ttu-id="b6e6e-529">Cliquez sur **sélectionner le dossier** pour commencer la génération à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-529">Click **Select Folder** to begin the build at that location.</span></span>
 
    <span data-ttu-id="b6e6e-530">![Créer le dossier Builds](images/AzureLabs-Lab3-44.png)
    ![sélectionnez crée le dossier](images/AzureLabs-Lab3-45.png)</span><span class="sxs-lookup"><span data-stu-id="b6e6e-530">![Create Builds Folder](images/AzureLabs-Lab3-44.png)
![Select Builds Folder](images/AzureLabs-Lab3-45.png)</span></span>
 
7.  <span data-ttu-id="b6e6e-531">Une fois Unity a terminé la génération (il peut prendre un certain temps), il doit s’ouvrir un **Explorateur de fichiers** fenêtre à l’emplacement de votre build.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-531">Once Unity has finished building (it might take some time), it should open a **File Explorer** window at the location of your build.</span></span>

<span data-ttu-id="b6e6e-532">Pour déployer sur l’ordinateur Local :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-532">To Deploy on Local Machine:</span></span>

1.  <span data-ttu-id="b6e6e-533">Dans *Visual Studio*, ouvrez le fichier solution qui a été créé dans le [chapitre précédent](#chapter-10--test-in-the-unity-editor).</span><span class="sxs-lookup"><span data-stu-id="b6e6e-533">In *Visual Studio*, open the solution file that has been created in the [previous Chapter](#chapter-10--test-in-the-unity-editor).</span></span>
2.  <span data-ttu-id="b6e6e-534">Dans le **plateforme de Solution**, sélectionnez **x86**, **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-534">In the **Solution Platform**, select **x86**, **Local Machine**.</span></span>
3.  <span data-ttu-id="b6e6e-535">Dans le **Configuration de la Solution** sélectionnez **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-535">In the **Solution Configuration** select **Debug**.</span></span>

    > <span data-ttu-id="b6e6e-536">Pour le Microsoft HoloLens, il peut s’avérer plus facile d’affecter à ce *Machine distante*, de sorte que vous ne sont pas attachés à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-536">For the Microsoft HoloLens, you may find it easier to set this to *Remote Machine*, so that you are not tethered to your computer.</span></span> <span data-ttu-id="b6e6e-537">Cependant, vous devez également effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6e6e-537">Though, you will need to also do the following:</span></span>
    > - <span data-ttu-id="b6e6e-538">Connaître le **adresse IP** de votre HoloLens, ce qui se trouve dans le *Paramètres > réseau & Internet > Wi-Fi > Options avancées*; IPv4 est l’adresse que vous devez utiliser.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-538">Know the **IP Address** of your HoloLens, which can be found within the *Settings > Network & Internet > Wi-Fi > Advanced Options*; the IPv4 is the address you should use.</span></span> 
    > - <span data-ttu-id="b6e6e-539">Vérifiez **Mode développeur** est **sur**; trouvé dans *Paramètres > mise à jour & sécurité > pour les développeurs*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-539">Ensure **Developer Mode** is **On**; found in *Settings > Update & Security > For developers*.</span></span>

    ![Déploiement d’une application](images/AzureLabs-Lab3-46.png)
 
4.  <span data-ttu-id="b6e6e-541">Accédez à la **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-541">Go to the **Build menu** and click on **Deploy Solution** to sideload the application to your machine.</span></span>
5.  <span data-ttu-id="b6e6e-542">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancé !</span><span class="sxs-lookup"><span data-stu-id="b6e6e-542">Your App should now appear in the list of installed apps, ready to be launched!</span></span>
6.  <span data-ttu-id="b6e6e-543">Une fois lancé, l’application vous invite à autoriser l’accès à la _Microphone_.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-543">Once launched, the App will prompt you to authorize access to the _Microphone_.</span></span> <span data-ttu-id="b6e6e-544">Utilisez le *contrôleurs de mouvement*, ou *entrée vocale*, ou le *clavier* d’appuyer sur le **Oui** bouton.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-544">Use the *Motion Controllers*, or *Voice Input*, or the *Keyboard* to press the **YES** button.</span></span> 

## <a name="chapter-12--improving-your-luis-service"></a><span data-ttu-id="b6e6e-545">Chapitre 12 – amélioration de votre service LUIS</span><span class="sxs-lookup"><span data-stu-id="b6e6e-545">Chapter 12 – Improving your LUIS service</span></span>

>[!IMPORTANT] 
> <span data-ttu-id="b6e6e-546">Ce chapitre est extrêmement important et peut devoir être interated à plusieurs reprises, car elle permet d’améliorer la précision de votre service LUIS : Vérifiez le terme de l’opération.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-546">This chapter is incredibly important, and may need to be interated upon several times, as it will help improve the accuracy of your LUIS service: ensure you complete this.</span></span>

<span data-ttu-id="b6e6e-547">Pour améliorer le niveau de présentation fourni par LUIS, vous devez capturer les énoncés nouvelle et utilisez-les pour recalculer votre application LUIS.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-547">To improve the level of understanding provided by LUIS you need to capture new utterances and use them to re-train your LUIS App.</span></span>

<span data-ttu-id="b6e6e-548">Par exemple, peut avoir effectué l’apprentissage LUIS pour comprendre « Increase » et « Migrer », mais vous ne voudriez pas que votre application afin de comprendre également des mots tels que « Agrandir » ?</span><span class="sxs-lookup"><span data-stu-id="b6e6e-548">For example, you might have trained LUIS to understand “Increase” and “Upsize”, but wouldn’t you want your app to also understand words like “Enlarge”?</span></span>

<span data-ttu-id="b6e6e-549">Une fois que vous avez utilisé votre application plusieurs fois, tout ce dont vous avez dit seront collectées par LUIS et disponibles dans le portail de LUIS.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-549">Once you have used your application a few times, everything you have said will be collected by LUIS and available in the LUIS PORTAL.</span></span>

1.  <span data-ttu-id="b6e6e-550">Accédez à votre application de portail suivant ce [lien](https://www.luis.ai/home)et se connecter.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-550">Go to your portal application following this [LINK](https://www.luis.ai/home), and Log In.</span></span>
2.  <span data-ttu-id="b6e6e-551">Une fois que vous êtes connecté avec vos Credentials MS, cliquez sur votre *nom de l’application*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-551">Once you are logged in with your MS Credentials, click on your *App name*.</span></span>
3.  <span data-ttu-id="b6e6e-552">Cliquez sur le **passez en revue les énoncés de point de terminaison** situé à gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-552">Click the **Review endpoint utterances** button on the left of the page.</span></span>

    ![Passez en revue les énoncés](images/AzureLabs-Lab3-47.png)
 
4.  <span data-ttu-id="b6e6e-554">Vous verrez une liste des énoncés qui lui ont été envoyés LUIS par votre Application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-554">You will be shown a list of the Utterances that have been sent to LUIS by your mixed reality Application.</span></span>

    ![Liste des énoncés](images/AzureLabs-Lab3-48.png)
 
<span data-ttu-id="b6e6e-556">Vous remarquerez certaines en surbrillance *entités*.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-556">You will notice some highlighted *Entities*.</span></span> 

<span data-ttu-id="b6e6e-557">En plaçant le curseur sur chaque mot en surbrillance, vous pouvez consulter chaque énoncé et déterminer quels entité a été reconnue correctement, qui sont des entités incorrectes et quelles entités ne sont pas incluses.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-557">By hovering over each highlighted word, you can review each Utterance and determine which Entity has been recognized correctly, which Entities are wrong and which Entities are missed.</span></span>

<span data-ttu-id="b6e6e-558">Dans l’exemple ci-dessus, il a été constaté que le mot « spear » avait été mis en surbrillance en tant que cible, par conséquent, il est nécessaire pour corriger l’erreur, ce qui est effectué en pointant sur le mot avec la souris et en cliquant sur **supprimer une étiquette**.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-558">In the example above, it was found that the word “spear” had been highlighted as a target, so it necessary to correct the mistake, which is done by hovering over the word with the mouse and clicking **Remove Label**.</span></span>

<span data-ttu-id="b6e6e-559">![Vérifier les énoncés](images/AzureLabs-Lab3-49.png)
![supprimer Image d’étiquette](images/AzureLabs-Lab3-50.png)</span><span class="sxs-lookup"><span data-stu-id="b6e6e-559">![Check utterances](images/AzureLabs-Lab3-49.png)
![Remove Label Image](images/AzureLabs-Lab3-50.png)</span></span>
 
5.  <span data-ttu-id="b6e6e-560">Si vous trouvez les énoncés qui sont complètement incorrect, vous pouvez les supprimer à l’aide de la **supprimer** bouton sur le côté droit de l’écran.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-560">If you find Utterances that are completely wrong, you can delete them using the **Delete** button on the right side of the screen.</span></span>

    ![Supprimer des énoncés incorrects](images/AzureLabs-Lab3-51.png)

6.  <span data-ttu-id="b6e6e-562">Ou si vous pensez que LUIS a interprété l’énoncé correctement, vous pouvez valider sa présentation à l’aide de la **ajouter l’intention aligné** bouton.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-562">Or if you feel that LUIS has interpreted the Utterance correctly, you can validate its understanding by using the **Add To Aligned Intent** button.</span></span>

    ![Ajouter à l’intention alignée](images/AzureLabs-Lab3-52.png)

7.  <span data-ttu-id="b6e6e-564">Une fois que vous avez trié de tous les énoncés affichées, essayez et rechargez la page pour voir si plusieurs sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-564">Once you have sorted all the displayed Utterances, try and reload the page to see if more are available.</span></span>
8.  <span data-ttu-id="b6e6e-565">Il est très important de répéter ce processus autant de fois que possible pour améliorer votre compréhension de l’application.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-565">It is very important to repeat this process as many times as possible to improve your application understanding.</span></span> 

<span data-ttu-id="b6e6e-566">**Amusez-vous !**</span><span class="sxs-lookup"><span data-stu-id="b6e6e-566">**Have fun!**</span></span>

## <a name="your-finished-luis-integrated-application"></a><span data-ttu-id="b6e6e-567">Votre application LUIS intégrée terminée</span><span class="sxs-lookup"><span data-stu-id="b6e6e-567">Your finished LUIS Integrated application</span></span>

<span data-ttu-id="b6e6e-568">Félicitations, vous avez créé une application de réalité mixte qui s’appuie sur Azure Language Understanding Intelligence Service, de comprendre ce qui indique un utilisateur et agir sur ces informations.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-568">Congratulations, you built a mixed reality app that leverages the Azure Language Understanding Intelligence Service, to understand what a user says, and act on that information.</span></span>

![résultat de laboratoire](images/AzureLabs-Lab3-000.png)

## <a name="bonus-exercises"></a><span data-ttu-id="b6e6e-570">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="b6e6e-570">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="b6e6e-571">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="b6e6e-571">Exercise 1</span></span>

<span data-ttu-id="b6e6e-572">Lors de l’utilisation de cette application, vous pouvez remarquer que si vous remplacez l’objet Floor et posez modifier sa couleur, il procédera ainsi.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-572">While using this application you might notice that if you gaze at the Floor object and ask to change its color, it will do so.</span></span> <span data-ttu-id="b6e6e-573">Vous pouvez imaginer comment arrêter votre application à partir de la modification de la couleur de l’étage</span><span class="sxs-lookup"><span data-stu-id="b6e6e-573">Can you work out how to stop your application from changing the Floor color?</span></span>

### <a name="exercise-2"></a><span data-ttu-id="b6e6e-574">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="b6e6e-574">Exercise 2</span></span>

<span data-ttu-id="b6e6e-575">Essayez d’étendre les fonctions LUIS et application, en ajoutant des fonctionnalités supplémentaires pour les objets de scène ; par exemple, créer de nouveaux objets aux regards indique un point d’accès, selon ce que l’utilisateur et puis être en mesure d’utiliser ces objets en même temps que les objets de scène actuels, avec les commandes existantes.</span><span class="sxs-lookup"><span data-stu-id="b6e6e-575">Try extending the LUIS and App capabilities, adding additional functionality for objects in scene; as an example, create new objects at the Gaze hit point, depending on what the user says, and then be able to use those objects alongside current scene objects, with the existing commands.</span></span> 
